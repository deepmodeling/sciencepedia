## 引言
间断Galerkin (Discontinuous Galerkin, DG) 方法因其在处理复杂几何、局部[网格加密](@entry_id:168565)和不同阶次近似方面的卓越灵活性，已成为计算科学与工程领域中一种强大的数值工具。然而，这种灵活性来自于其允许解在单元边界上存在间断，这也引出了一个核心的理论问题：我们如何构建一个既一致又稳定的离散格式，以保证数值解的收敛性和可靠性？具体而言，如何控制这些间断，并确保整个数值方案是良定的？

本文旨在系统性地回答这一问题，深入剖析了应用最为广泛的一类DG方法——内部罚分 (Interior Penalty, IP) 方法的理论基石：稳定性、一致性与强制性。通过学习本文，读者将全面掌握这些抽象但至关重要的概念如何转化为可靠的[数值算法](@entry_id:752770)。

文章的结构安排如下：
在第一章“原理与机制”中，我们将从间断方法所依赖的破碎Sobolev[函数空间](@entry_id:143478)出发，逐步推导出内部罚分方法的[变分形式](@entry_id:166033)，并详细分析其[双线性形式](@entry_id:746794)中的各个组成部分——特别是罚分项——是如何确保方法强制性的。
第二章“应用与交叉学科联系”将理论付诸实践，探讨如何在多样化的应用场景中设计稳健的[DG格式](@entry_id:178043)，包括处理复杂的边界条件、应对材料与几何的各向异性，并揭示了该方法与[优化理论](@entry_id:144639)、离散极值原理等前沿领域的深刻联系。
最后，在“动手实践”部分，通过一系列精心设计的引导性练习，读者将有机会亲手计算和分析关键的理论环节，将抽象的理论知识内化为具体的分析技能。

## 原理与机制

本章旨在深入探讨间断 Galerkin (DG) 方法的核心理论基础，特别是内部罚分 (Interior Penalty, IP) 方法的稳定性、一致性和强制性。我们将从 DG 方法所使用的函数空间开始，逐步推导其[变分形式](@entry_id:166033)，并详细分析其关键性质。

### 用于间断方法的[函数空间](@entry_id:143478)

与要求全局连续性的标准连续 Galerkin 方法不同，间断 Galerkin 方法在一个更广阔的[函数空间](@entry_id:143478)中寻找近似解。这个空间的构建放宽了对函数在单元边界上连续性的严格要求，从而为处理复杂几何、局部加密和不同阶次多项式提供了极大的灵活性。

为了精确描述这个空间，我们首先引入**破碎 Sobolev 空间 (broken Sobolev space)** 的概念。给定一个有界 Lipschitz 区域 $\Omega \subset \mathbb{R}^d$ 及其一个形状规则的网格剖分 $\mathcal{T}_h = \{K\}$，破碎 Sobolev 空间 $H^1(\mathcal{T}_h)$ 定义为：
$$
H^1(\mathcal{T}_h) := \{\,v \in L^2(\Omega) \,:\, v|_K \in H^1(K) \text{ for all } K \in \mathcal{T}_h \,\}
$$
其中 $v|_K$ 表示函数 $v$ 在单元 $K$ 上的限制。该定义表明，属于 $H^1(\mathcal{T}_h)$ 的函数仅需在每个单元 $K$ 内部具备 $H^1$ 正则性（即函数本身及其[弱导数](@entry_id:189356)均在 $K$ 上平方可积），但不必在单元之间的交界面上保持连续。与此相伴，我们定义**破碎梯度 (broken gradient)** $\nabla_h v$，其在每个单元上的作用等同于标准梯度，即 $(\nabla_h v)|_K := \nabla(v|_K)$。

这个破碎空间与标准的 conforming Sobolev 空间 $H^1(\Omega)$ 及其满足齐次 Dirichlet 边界条件的[子空间](@entry_id:150286) $H_0^1(\Omega)$ 有着本质区别。$H^1(\Omega)$ 中的函数在整个区域 $\Omega$ 上具有全局的弱可微性，这意味着在任意内部界面 $F$ 上，相邻单元的迹是单值的，即它们重合。而 $H^1(\mathcal{T}_h)$ 中的函数由于缺乏跨单元的连续性约束，其在内部界面 $F$ 上通常具有两个不同的**迹 (traces)**，分别来自相邻的两个单元。从另一个角度看，$H^1(\mathcal{T}_h)$ 可以等同于所有单元上 $H^1(K)$ [空间的笛卡尔积](@entry_id:276174) $\prod_{K \in \mathcal{T}_h} H^1(K)$。显然，任何全局连续的函数都满足逐单元的正则性要求，因此我们有如下的空间包含关系：
$$
H_0^1(\Omega) \subset H^1(\Omega) \subset H^1(\mathcal{T}_h)
$$

在 DG 方法的实践中，我们通常在 $H^1(\mathcal{T}_h)$ 的一个有限维[子空间](@entry_id:150286)中寻找数值解。这个[子空间](@entry_id:150286)由分片多项式构成，定义为：
$$
V_h := \{\,v \in L^2(\Omega) \,:\, v|_K \in \mathbb{P}_p(K) \text{ for all } K \in \mathcal{T}_h \,\}
$$
其中 $\mathbb{P}_p(K)$ 表示在单元 $K$ 上的次数最高为 $p$ 的多项式空间（对于四边形或[六面体单元](@entry_id:174602)，则常使用 $\mathbb{Q}_p(K)$ [张量积](@entry_id:140694)[多项式空间](@entry_id:144410)）。这个空间 $V_h$ 是 DG 方法的离散[试探空间](@entry_id:756166)和检验空间。

### 从[分部积分](@entry_id:136350)到 DG [变分形式](@entry_id:166033)

DG 方法的[变分形式](@entry_id:166033)源于在每个单元上对[偏微分方程](@entry_id:141332)进行处理。考虑一个典型的二阶椭圆模型问题：
$$
-\nabla \cdot (\boldsymbol{A} \nabla u) = f \quad \text{in } \Omega
$$
其中 $\boldsymbol{A}(x)$ 是一个[对称正定](@entry_id:145886)的[扩散张量](@entry_id:748421)。我们首先将该方程乘以一个检验函数 $v \in V_h$，并在任意单元 $K \in \mathcal{T}_h$ 上积分。然后，应用[格林公式](@entry_id:173118)（即[分部积分](@entry_id:136350)）可得：
$$
\int_{K} \boldsymbol{A} \nabla u \cdot \nabla v \,\mathrm{d}x = - \int_{K} \nabla \cdot (\boldsymbol{A} \nabla u)\, v \,\mathrm{d}x + \int_{\partial K} (\boldsymbol{A} \nabla u \cdot \boldsymbol{n}_K)\, v \,\mathrm{d}s
$$
其中 $\boldsymbol{n}_K$ 是单元 $K$ 的外法向[单位向量](@entry_id:165907)。将方程 $-\nabla \cdot (\boldsymbol{A} \nabla u) = f$ 代入并对所有单元 $K \in \mathcal{T}_h$ 求和，我们得到：
$$
\sum_{K \in \mathcal{T}_h} \int_K \boldsymbol{A} \nabla u \cdot \nabla v \,\mathrm{d}x - \sum_{K \in \mathcal{T}_h} \int_{\partial K} (\boldsymbol{A} \nabla u \cdot \boldsymbol{n}_K)\, v \,\mathrm{d}s = \int_\Omega f v \,\mathrm{d}x
$$
这里的核心在于如何处理边界积分项 $\sum_{K \in \mathcal{T}_h} \int_{\partial K}$。这个求和可以重组为对网格中所有**面 (faces)** 的积分求和。为了系统地处理这些面上的积分，我们引入**跃度 (jump)** 和**平均 (average)** 算子。

对于一个内部面 $F$，它由两个相邻单元 $K^-$ 和 $K^+$ 共享。设 $\boldsymbol{n}^-$ 和 $\boldsymbol{n}^+$ 分别为 $F$ 相对于 $K^-$ 和 $K^+$ 的外法向单位向量（注意 $\boldsymbol{n}^- = -\boldsymbol{n}^+$）。对于一个标量函数 $z$ 和一个向量场 $\boldsymbol{\tau}$，我们在 $F$ 上定义：
- **平均 (Average)**: $\{z\} = \frac{1}{2}(z^- + z^+)$, $\quad \{\boldsymbol{\tau}\} = \frac{1}{2}(\boldsymbol{\tau}^- + \boldsymbol{\tau}^+)$
- **跃度 (Jump)**: $\llbracket z \rrbracket = z^- \boldsymbol{n}^- + z^+ \boldsymbol{n}^+$, $\quad \llbracket \boldsymbol{\tau} \rrbracket = \boldsymbol{\tau}^- \cdot \boldsymbol{n}^- + \boldsymbol{\tau}^+ \cdot \boldsymbol{n}^+$

其中 $z^\pm$ 和 $\boldsymbol{\tau}^\pm$ 表示从 $K^\pm$ 取得的迹。利用这些定义，对所有单元边界的求和可以转化为对所有内部面的求和，例如：
$$
\sum_{K \in \mathcal{T}_h} \int_{\partial K} (\boldsymbol{A} \nabla u \cdot \boldsymbol{n}_K)\, v \,\mathrm{d}s = \sum_{F \in \mathcal{F}_h^i} \int_F \left( \{\boldsymbol{A} \nabla u\} \cdot \llbracket v \rrbracket + \llbracket \boldsymbol{A} \nabla u \rrbracket \{v\} \right) \,\mathrm{d}s + \text{边界项}
$$
这个恒等式是推导所有 DG 方法的出发点。

### 内部罚分 (IP) 方法族

直接使用上述由[分部积分](@entry_id:136350)得到的公式是不够的，因为它依赖于精确解的通量 $\boldsymbol{A} \nabla u$，而这在离散函数 $u_h \in V_h$ 中是多值的。DG 方法通过引入**[数值通量](@entry_id:752791) (numerical flux)** 来替代物理通量，从而定义一个适定的离散格式。

#### [对称内部罚](@entry_id:755719)分 Galerkin (SIPG) 方法

SIPG 方法是一种广泛应用的 IPDG 变体，其构造的目的是为了获得一个对称的[双线性形式](@entry_id:746794)。其[双线性形式](@entry_id:746794) $a_h(u,v)$ 由以下四部分构成：
$$
a_h(u,v) = \sum_{K\in\mathcal{T}_h}\int_K \boldsymbol{A}\nabla u\cdot \nabla v \,\mathrm{d}x - \sum_{F\in\mathcal{F}_h}\int_F \big(\{\boldsymbol{A}\nabla u\}\cdot \llbracket v\rrbracket + \{\boldsymbol{A}\nabla v\}\cdot \llbracket u\rrbracket \big) \,\mathrm{d}s + \sum_{F\in\mathcal{F}_h}\int_F \sigma_F \llbracket u\rrbracket\cdot \llbracket v\rrbracket \,\mathrm{d}s
$$
我们将逐一解析这些项的来源与作用：

1.  **体积项 (Volume Term)**: $\sum_{K\in\mathcal{T}_h}\int_K \boldsymbol{A}\nabla u\cdot \nabla v \,\mathrm{d}x$。这一项直接来自逐单元[分部积分](@entry_id:136350)，是标准的 Galerkin 项，反映了单元内部的扩散过程。

2.  **一致性项 (Consistency Terms)**: $-\sum_{F\in\mathcal{F}_h}\int_F \big(\{\boldsymbol{A}\nabla u\}\cdot \llbracket v\rrbracket + \{\boldsymbol{A}\nabla v\}\cdot \llbracket u\rrbracket \big)\,\mathrm{d}s$。这些项源于对单元边界积分的重写。第一部分 $-\int_F \{\boldsymbol{A}\nabla u\}\cdot \llbracket v\rrbracket$ 是确保方法**一致性**的核心，它将解的梯度（通过平均通量）与检验函数的跃度耦合起来。第二部分 $-\int_F \{\boldsymbol{A}\nabla v\}\cdot \llbracket u\rrbracket$ 是为了使双线性形式对称而添加的，它也被称为**伴随一致性项**。

3.  **罚分项 (Penalty Term)**: $+\sum_{F\in\mathcal{F}_h}\int_F \sigma_F \llbracket u\rrbracket\cdot \llbracket v\rrbracket \,\mathrm{d}s$。这是 IP 方法的标志性部分。此项通过惩罚解在界面上的跃度来弱形式地强制连续性。更重要的是，它是确保[双线性形式](@entry_id:746794)**强制性 (coercivity)**，从而保证数值方法稳定性的关键。$\sigma_F > 0$ 是一个逐面定义的罚分参数。

#### NIPG 和 IIPG 方法

SIPG 只是 IP 方法族中的一员。通过调整一致性项，可以得到其他变体：

- **非[对称内部罚](@entry_id:755719)分 Galerkin (NIPG)** 方法将伴随一致性项的符号反转 ($\theta=-1$):
  $$
  -\sum_{F\in\mathcal{F}_h}\int_F \big(\{\boldsymbol{A}\nabla u\}\cdot \llbracket v\rrbracket - \{\boldsymbol{A}\nabla v\}\cdot \llbracket u\rrbracket \big)\,\mathrm{d}s
  $$
  这导致[双线性形式](@entry_id:746794)非对称。NIPG 的一个优点是，它有时可以在没有罚分项的情况下（或用较小的罚分）保持强制性。

- **不完全内部罚分 Galerkin (IIPG)** 方法则完全省略了伴随一致性项 ($\theta=0$):
  $$
  -\sum_{F\in\mathcal{F}_h}\int_F \{\boldsymbol{A}\nabla u\}\cdot \llbracket v\rrbracket \,\mathrm{d}s
  $$
  这种方法也是非对称的。

尽管这些方法在对称性上有所不同，但它们都是**（原始）一致的 (primal consistent)**，即当精确解代入时，离散方程仍然成立。然而，只有 SIPG 是**伴随一致的 (adjoint consistent)**，这对于自伴随问题（如[泊松方程](@entry_id:143763)）的[误差分析](@entry_id:142477)（特别是超收敛性）具有重要意义。

### 基本性质：一致性、稳定性与强制性

一个可靠的数值方法必须具备一致性和稳定性。对于 Galerkin 方法，稳定性通常通过证明[双线性形式](@entry_id:746794)的**强制性**来建立。

根据 **Lax-Milgram 引理**，如果一个双线性形式 $a_h(\cdot, \cdot)$ 在某个[赋范空间](@entry_id:137032) $(V_h, \|\cdot\|)$ 上是**连续的 (continuous)** 和**强制的 (coercive)**，那么离散问题 $a_h(u_h, v_h) = l_h(v_h)$ 存在唯一解 $u_h$，并且该解满足[稳定性估计](@entry_id:755306)：
$$
\|u_h\| \le \frac{1}{\alpha} \|l_h\|_{V_h^*}
$$
其中 $\alpha$ 是强制性常数，$\|l_h\|_{V_h^*}$ 是线性泛函 $l_h$ 的[对偶范数](@entry_id:200340)。

**强制性**的精确定义是：存在一个常数 $\alpha > 0$（不依赖于网格尺寸 $h$），使得对于所有 $v_h \in V_h$ 都成立：
$$
a_h(v_h, v_h) \ge \alpha \|v_h\|^2
$$
为了证明强制性，我们首先需要定义一个合适的范数。对于 IPDG 方法，一个自然的选择是 **DG [能量范数](@entry_id:274966)**，其定义源于 $a_h(v_h, v_h)$ 的形式：
$$
\|v_h\|_{DG}^2 := \sum_{K \in \mathcal{T}_h} \|\nabla v_h\|_{L^2(K)}^2 + \sum_{F \in \mathcal{F}_h} \sigma_F \|\llbracket v_h \rrbracket\|_{L^2(F)}^2
$$
这个范数由两部分组成：一部分是破碎 $H^1$ [半范数](@entry_id:264573) $|v_h|_{1,h}^2 = \sum_K \|\nabla v_h\|_{L^2(K)}^2$，衡量单元内部的梯度；另一部分是所有面上解的跃度的加权平方和，用于[控制函数](@entry_id:183140)的[不连续性](@entry_id:144108)。

现在我们来考察 SIPG 的强制性。将 $u=v$ 代入 $a_h(u,v)$ 的表达式中，我们得到：
$$
a_h(v_h, v_h) = \sum_{K} \int_K \boldsymbol{A}\nabla v_h \cdot \nabla v_h \,\mathrm{d}x - 2\sum_{F} \int_F \{\boldsymbol{A}\nabla v_h\} \cdot \llbracket v_h \rrbracket \,\mathrm{d}s + \sum_{F} \int_F \sigma_F |\llbracket v_h \rrbracket|^2 \,\mathrm{d}s
$$
第一项和第三项是非负的。然而，中间的一致性项（[交叉](@entry_id:147634)项）可能是负的，并可能破坏整体的[正定性](@entry_id:149643)。为了确保强制性，我们必须证明正的罚分项足以控制这个可能为负的交叉项。这正是罚分参数 $\sigma_F$ 发挥关键作用的地方。

通过应用 Cauchy-Schwarz 不等式和 Young 不等式，[交叉](@entry_id:147634)项可以被界定为：
$$
\left| 2\int_F \{\boldsymbol{A}\nabla v_h\} \cdot \llbracket v_h \rrbracket \,\mathrm{d}s \right| \le \frac{1}{\eta_F} \|\{\boldsymbol{A}\nabla v_h\}\|_{L^2(F)}^2 + \eta_F \|\llbracket v_h \rrbracket\|_{L^2(F)}^2
$$
这里的挑战在于如何用体积项（即 $|v_h|_{1,h}^2$）来控制 $\|\{\boldsymbol{A}\nabla v_h\}\|_{L^2(F)}^2$。这需要借助**[迹不等式](@entry_id:756082) (trace inequality)** 和**[逆不等式](@entry_id:750800) (inverse inequality)**。对于形状规则的网格上的次数为 $p$ 的多项式，一个关键的不等式是：
$$
\|w\|_{L^2(\partial K)}^2 \le C_{\mathrm{tr}} \, \frac{p^2}{h_K} \, \|w\|_{L^2(K)}^2
$$
其中 $h_K$ 是单元 $K$ 的特征尺寸。这个不等式表明，多项式在边界上的范数可以通过其在单元内部的范数来控制，但代价是一个依赖于 $p^2/h_K$ 的因子。这个不等式的成立依赖于网格的**[形状规则性](@entry_id:754733) (shape-regularity)**，即单元不能被任意地挤压或拉伸。

将[迹不等式](@entry_id:756082)应用于通量项 $\{\boldsymbol{A}\nabla v_h\}$，经过一系列推导，可以证明为了使 $a_h(v_h, v_h) \ge \alpha \|v_h\|_{DG}^2$ 成立，罚分参数 $\sigma_F$ 必须足够大，以抵消交叉项的影响。具体而言，它必须满足如下的尺度关系：
$$
\sigma_F \ge C \cdot \kappa_F \cdot \frac{p^2}{h_F}
$$
其中：
- $C$ 是一个仅依赖于网格[形状规则性](@entry_id:754733)和[迹不等式](@entry_id:756082)常数的正常数。
- $h_F$ 是面 $F$ 的特征尺寸。$h_F^{-1}$ 的依赖关系源于[迹不等式](@entry_id:756082)。
- $p^2$ 的依赖关系也直接来自[迹不等式](@entry_id:756082)中的多项式次数依赖性。
- $\kappa_F$ 是一个与[扩散张量](@entry_id:748421) $\boldsymbol{A}$ 相关的权重，用于处理异性或[非均匀介质](@entry_id:750241)。一个稳健的选择是取 $\boldsymbol{A}$ 在[法线](@entry_id:167651)方向分量的最大值或调和平均值，例如 $\kappa_F = \max( \boldsymbol{n}_F^\top \boldsymbol{A}|_{K^-} \boldsymbol{n}_F, \boldsymbol{n}_F^\top \boldsymbol{A}|_{K^+} \boldsymbol{n}_F )$。

正确选择罚分参数是确保 IPDG 方法稳定且收敛的基石。过小的罚分会导致不稳定，而过大的罚分则会增加刚度矩阵的条件数并引入过多的数值耗散，影响精度。

### 边界条件的弱施加

DG 方法的一个显著优点是其**[弱形式](@entry_id:142897)施加边界条件 (weak imposition of boundary conditions)** 的能力，这与标准有限元方法中的强施加形成对比。我们以 Dirichlet 边界条件 $u=g$ on $\partial\Omega$ 为例来说明。

其核心思想是将边界外的区域看作一个“幽灵单元”，并将给定的边界数据 $g$ 视为来自这个幽灵单元的迹。对于一个位于 $\partial\Omega$ 上的边界邻面 $F$，设其内部单元为 $K$，外法向为 $\boldsymbol{n}$。我们将内部迹记为 $(\cdot)$，而外部（幽灵）迹则由边界数据定义。
- 对于[检验函数](@entry_id:166589) $v_h \in V_h$，我们总是在其不出现的项中取其值为零，所以其外部迹为 $0$。跃度和[平均算子](@entry_id:746605)在边界上的定义相应地变为：
  - $\llbracket v_h \rrbracket = v_h \boldsymbol{n} + 0(-\boldsymbol{n}) = v_h \boldsymbol{n}$
  - $\{\boldsymbol{A}\nabla v_h\} = \boldsymbol{A}\nabla v_h$ （因为外部没有贡献）
- 对于解 $u_h$，其外部迹被认为是给定的边界数据 $g$。

将这些边界定义代入 SIPG [双线性形式](@entry_id:746794)的通用[面积分](@entry_id:275394)项中，即
$$
-\int_F \big(\{\boldsymbol{A}\nabla u_h\}\cdot \llbracket v_h\rrbracket + \{\boldsymbol{A}\nabla v_h\}\cdot \llbracket u_h\rrbracket \big) \,\mathrm{d}s + \int_F \sigma_F \llbracket u_h\rrbracket\cdot \llbracket v_h\rrbracket \,\mathrm{d}s
$$
我们会发现，包含已知数据 $g$ 的项可以被移到[变分方程](@entry_id:635018)的右端，形成线性泛函 $l_h(v_h)$ 的一部分。最终，对于非齐次 [Dirichlet 问题](@entry_id:274408)，线性泛函的形式为：
$$
l_h(v_h) = \int_\Omega f v_h \,\mathrm{d}x - \int_{\partial\Omega} (\boldsymbol{A}\nabla v_h \cdot \boldsymbol{n}) g \,\mathrm{d}s + \int_{\partial\Omega} \sigma_F g v_h \,\mathrm{d}s
$$
而双线性形式 $a_h(u_h,v_h)$ 则只包含未知函数 $u_h$ 和检验函数 $v_h$ 的项，其形式与内部面的形式保持一致。通过这种方式，边界条件不是通过对[离散空间](@entry_id:155685)施加约束，而是作为[变分问题](@entry_id:756445)的一部分被自然地、弱形式地包含进来。这种处理方式极大地简化了复杂几何和[非匹配网格](@entry_id:168552)下的编程实现。