## 引言
间断伽辽金 (Discontinuous Galerkin, DG) 方法是现代计算力学中一种功能强大且日益流行的数值技术。与要求解在整个区域内连续的传统有限元方法 (FEM) 不同，DG 方法通过允许单元间的间断，为处理复杂几何、[非协调网格](@entry_id:752550)以及材料属性突变等难题提供了前所未有的灵活性，尤其在弹性力学领域展现出巨大潜力。然而，这种灵活性也带来了理论和实践上的挑战，例如如何构建稳定且一致的离散格式，如何处理[体积锁定](@entry_id:172606)等数值难题，以及如何将其有效应用于多物理场耦合等复杂工程场景。本文旨在系统性地填补这一知识空白，为读者提供一个从理论到实践的完整指南。

本文将引导读者深入探索弹性力学中的DG世界。在“原理与机制”一章，我们将从基本[变分原理](@entry_id:198028)出发，详细推导[DG方法](@entry_id:748369)的数学框架，并探讨其稳定性和收敛性。接着，“应用与跨学科交叉”一章将展示DG方法如何应用于模拟复杂材料行为、[非线性动力学](@entry_id:190195)、[断裂力学](@entry_id:141480)和多物理场耦合等前沿问题。最后，“动手实践”部分将通过具体的计算练习，帮助读者将理论知识转化为实际的编程技能。通过这三章的学习，读者将全面掌握[DG方法](@entry_id:748369)的核心思想及其在解决复杂弹性力学问题中的强大能力。

## 原理与机制

本章旨在深入探讨弹性力学问题的间断伽辽金 (Discontinuous Galerkin, DG) 方法背后的核心原理与关键机制。我们将从经典的弹性力学[变分形式](@entry_id:166033)出发，逐步构建 DG 方法的数学框架，阐明其设计理念，并分析其稳定性和收敛性等理论性质。最后，我们将讨论一些在实际应用中至关重要的高等议题，如[体积锁定](@entry_id:172606)和可杂交间断伽辽金 (HDG) 方法。

### 从强形式到弱形式：弹性力学问题的[变分原理](@entry_id:198028)

在深入研究 DG 方法之前，我们必须首先回顾线弹性问题的数学描述。一个弹性体占据一个有界区域 $\Omega \subset \mathbb{R}^d$。在小应变和静态假设下，其行为由三个基本方程控制：

1.  **运动学关系**：位移场 $\boldsymbol{u}$ 与[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 之间的关系。为了保证[应变度量](@entry_id:755495)在[刚体转动](@entry_id:191086)下为零，我们使用对称梯度来定义应变 [@problem_id:3559004]：
    $$
    \boldsymbol{\varepsilon}(\boldsymbol{u}) = \frac{1}{2} \left( \nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top} \right)
    $$
    其分量形式为 $\varepsilon_{ij}(\boldsymbol{u}) = \frac{1}{2}(\partial_i u_j + \partial_j u_i)$。

2.  **本构关系**：[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 与应变张量 $\boldsymbol{\varepsilon}$ 之间的关系，即胡克定律 (Hooke's law)。对于一般的线性各向异性材料，这由一个[四阶弹性张量](@entry_id:188318) $\mathbb{C}$ 描述：
    $$
    \boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{u})
    $$
    对于均匀各向同性材料，该关系简化为依赖于两个拉梅参数 (Lamé parameters) $\lambda$ 和 $\mu$ 的形式 [@problem_id:3558993]：
    $$
    \boldsymbol{\sigma}(\boldsymbol{u}) = 2\mu \boldsymbol{\varepsilon}(\boldsymbol{u}) + \lambda \operatorname{tr}(\boldsymbol{\varepsilon}(\boldsymbol{u})) \boldsymbol{I}
    $$
    其中 $\boldsymbol{I}$ 是二阶单位张量。在这里，我们使用了Voigt-free的[张量表示法](@entry_id:272140)，其中四阶各向同性本构张量可以写作 $\mathbb{C} = 2\mu \boldsymbol{I}_s + \lambda (\boldsymbol{I} \otimes \boldsymbol{I})$，$\boldsymbol{I}_s$ 是四阶对称单位张量，其作用是提取任意二阶[张量的对称部分](@entry_id:182434)。

3.  **[动量平衡](@entry_id:193575)**：在没有惯性效应的情况下，应[力场](@entry_id:147325)必须与[体力](@entry_id:174230) $\boldsymbol{f}$ 平衡：
    $$
    -\nabla \cdot \boldsymbol{\sigma} = \boldsymbol{f} \quad \text{在 } \Omega \text{ 内}
    $$

这些[偏微分方程](@entry_id:141332)，连同在边界 $\partial\Omega$ 上施加的边界条件，共同构成了弹性力学问题的**强形式** (strong form)。边界通常被划分为两部分：位移（Dirichlet）边界 $\Gamma_D$ 和力（Neumann）边界 $\Gamma_N$。相应的边界条件为 [@problem_id:3558934]：
$$
\begin{cases}
    \boldsymbol{u} = \bar{\boldsymbol{u}}  \text{在 } \Gamma_D \text{ 上}, \\
    \boldsymbol{\sigma} \boldsymbol{n} = \bar{\boldsymbol{t}}  \text{在 } \Gamma_N \text{ 上}.
\end{cases}
$$
其中 $\bar{\boldsymbol{u}}$ 是给定的位移，$\bar{\boldsymbol{t}}$ 是给定的面力（traction），$\boldsymbol{n}$ 是边界上的单位外法向量。

强形式要求解 $\boldsymbol{u}$ 具有足够的正则性（例如，二次可微），这在许多工程问题中难以满足。因此，我们转向**[弱形式](@entry_id:142897)** (weak form) 或[变分形式](@entry_id:166033)。通过将[动量平衡](@entry_id:193575)方程与一个任意的、满足齐次[位移边界条件](@entry_id:203261)的**[虚位移](@entry_id:168781)**或**检验函数** (test function) $\boldsymbol{v}$ 作[内积](@entry_id:158127)，并在整个区域 $\Omega$ 上积分，我们得到：
$$
\int_{\Omega} (-\nabla \cdot \boldsymbol{\sigma}) \cdot \boldsymbol{v} \, dx = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, dx
$$

应用分部积分（即[格林公式](@entry_id:173118)或散度定理），我们将导数从[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 转移到检验函数 $\boldsymbol{v}$ 上：
$$
\int_{\Omega} \boldsymbol{\sigma} : \nabla \boldsymbol{v} \, dx - \int_{\partial\Omega} (\boldsymbol{\sigma} \boldsymbol{n}) \cdot \boldsymbol{v} \, ds = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, dx
$$

一个至关重要的步骤是利用应力[张量的对称性](@entry_id:202126)。在没有[体力](@entry_id:174230)矩的经典柯西连续介质中，角动量守恒的直接推论是柯西[应力张量](@entry_id:148973)必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\top}$ [@problem_id:3559004]。因此，[应力张量](@entry_id:148973)与任意[二阶张量](@entry_id:199780) $\nabla \boldsymbol{v}$ 的[双点积](@entry_id:748648)可以简化为其与 $\nabla \boldsymbol{v}$ 的对称部分的[双点积](@entry_id:748648)，即应变张量 $\boldsymbol{\varepsilon}(\boldsymbol{v})$：
$$
\boldsymbol{\sigma} : \nabla \boldsymbol{v} = \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\boldsymbol{v})
$$
这表明对称应力 $\boldsymbol{\sigma}$ 的[功共轭](@entry_id:194957)量是对称应变 $\boldsymbol{\varepsilon}$。这一性质确保了对于任何刚体运动（其应变为零），内部[虚功](@entry_id:176403)自动为零，从而在离散层面也自然地满足了[角动量守恒](@entry_id:156798)。

将本构关系代入并处理边界项，我们得到标准的[弱形式](@entry_id:142897)：求[试探函数](@entry_id:756165) (trial function) $\boldsymbol{u}$，使其满足[本质边界条件](@entry_id:173524) $\boldsymbol{u} = \bar{\boldsymbol{u}}$ on $\Gamma_D$，并且对于所有满足 $\boldsymbol{v} = \boldsymbol{0}$ on $\Gamma_D$ 的检验函数 $\boldsymbol{v}$，下式成立：
$$
\int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{v}) : \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{u}) \, dx = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, dx + \int_{\Gamma_N} \bar{\boldsymbol{t}} \cdot \boldsymbol{v} \, ds
$$
在这个过程中，[位移边界条件](@entry_id:203261) $\boldsymbol{u}=\bar{\boldsymbol{u}}$ 被称为**[本质边界条件](@entry_id:173524)** (essential boundary condition)，因为它必须被强加于[试探函数](@entry_id:756165)空间。而力边界条件 $\boldsymbol{\sigma}\boldsymbol{n}=\bar{\boldsymbol{t}}$ 则作为**自然边界条件** (natural boundary condition) "自然地"出现在[变分方程](@entry_id:635018)的右端项中，它无需在[函数空间](@entry_id:143478)上强加，而是通过弱形式的解被满足 [@problem_id:3558934]。

### 间断伽辽金框架

标准有限元方法（[连续伽辽金方法](@entry_id:747805)）要求[试探函数](@entry_id:756165)和[检验函数](@entry_id:166589)在整个区域 $\Omega$ 上是连续的。间断伽辽金 (DG) 方法的核心思想是放宽这一限制。我们将区域 $\Omega$ 剖分成一个由互不重叠的单元 $K$ 组成的网格 $\mathcal{T}_h$，并允许函数在单元边界上存在间断。

#### [间断函数](@entry_id:143848)空间、迹、平均与跳跃

DG 方法在所谓的**破碎 Sobolev 空间** (broken Sobolev space) 中寻找解。对于弹性力学问题，该空间定义为：
$$
[H^1(\mathcal{T}_h)]^d := \{ \boldsymbol{v} \in [L^2(\Omega)]^d : \boldsymbol{v}|_K \in [H^1(K)]^d \text{ for all } K \in \mathcal{T}_h \}
$$
离散的 DG 空间 $V_h$ 是这个空间的一个有限维[子空间](@entry_id:150286)，通常由每个单元上的分片多项式构成。例如，对于单纯形网格（二维的三角形，三维的四面体），我们可以选择 $V_h$ 为所有分片 $p$ 次多项式向量场的集合，其中 $p \ge 1$ [@problem_id:3558956]。

由于函数在单元间可能是间断的，对于一个共享两个单元 $K^+$ 和 $K^-$ 的内部界面 $F$，一个函数 $\boldsymbol{v}$ 在 $F$ 上有两个**迹** (trace)：从 $K^+$ 逼近的 $\boldsymbol{v}^+$ 和从 $K^-$ 逼近的 $\boldsymbol{v}^-$。为了系统地处理这些间断，我们定义**平均** (average) 和**跳跃** (jump) 算子。给定一个从 $K^+$ 指向 $K^-$ 的[单位法向量](@entry_id:178851) $\boldsymbol{n}$，我们定义在 $F$ 上的两个方向的法向量为 $\boldsymbol{n}^+ = \boldsymbol{n}$ 和 $\boldsymbol{n}^- = -\boldsymbol{n}$。
- **[平均算子](@entry_id:746605)** $\{\!\{ \cdot \}\!\}$ 通常是两个迹的[算术平均值](@entry_id:165355)：
  $$
  \{\!\{ \boldsymbol{v} \}\!\} = \frac{1}{2}(\boldsymbol{v}^+ + \boldsymbol{v}^-), \quad \{\!\{ \boldsymbol{\sigma} \}\!\} = \frac{1}{2}(\boldsymbol{\sigma}^+ + \boldsymbol{\sigma}^-)
  $$
- **跳跃算子** $[\![\cdot]\!]$ 的定义则更为精巧。在现代 DG 文献中，为了得到优雅且对称的弱形式，跳跃算子的输出秩通常会提升。对于向量场 $\boldsymbol{v}$，其跳跃被定义为一个二阶张量 [@problem_id:3558956] [@problem_id:3558939]：
  $$
  [\![\boldsymbol{v}]\!] := \boldsymbol{v}^+ \otimes \boldsymbol{n}^+ + \boldsymbol{v}^- \otimes \boldsymbol{n}^- = (\boldsymbol{v}^+ - \boldsymbol{v}^-) \otimes \boldsymbol{n}
  $$
  类似地，对于一个[张量场](@entry_id:190170) $\boldsymbol{\tau}$，其跳跃（通常指其法向分量的跳跃）是一个向量：
  $$
  [\![\boldsymbol{\tau} \boldsymbol{n}]\!] := \boldsymbol{\tau}^+ \boldsymbol{n}^+ + \boldsymbol{\tau}^- \boldsymbol{n}^- = (\boldsymbol{\tau}^+ - \boldsymbol{\tau}^-) \boldsymbol{n}
  $$
这些定义的一个重要性质是，它们与简单的差值相关联，例如 $[\![\boldsymbol{v}]\!] \boldsymbol{n} = \boldsymbol{v}^+ - \boldsymbol{v}^-$。

#### 破碎[弱形式](@entry_id:142897)

通过在每个单元 $K$ 上应用分部积分，然后对所有单元求和，我们得到一个包含单元[内部积](@entry_id:158127)分和所有界面上积分的“破碎”[弱形式](@entry_id:142897)。内部界面 $F$ 上的积分项形如：
$$
\int_F ((\boldsymbol{\sigma}^+ \boldsymbol{n}) \cdot \boldsymbol{v}^+ - (\boldsymbol{\sigma}^- \boldsymbol{n}) \cdot \boldsymbol{v}^-) \, ds
$$
利用跳跃和[平均算子](@entry_id:746605)，这个表达式可以被系统地分解为：
$$
\int_F ( \{\!\{\boldsymbol{\sigma}\boldsymbol{n}\}\!\} \cdot [\![\boldsymbol{v}]\!] + [\![\boldsymbol{\sigma}\boldsymbol{n}]\!] \cdot \{\!\{\boldsymbol{v}\}\!\} ) \, ds
$$
（这里为了简化，我们使用了标量形式的跳跃 $[\![\boldsymbol{v}]\!] = \boldsymbol{v}^+ - \boldsymbol{v}^-$）。DG 方法的核心就是如何用离散解的跳跃和平均来近似这些界面项，从而构建一个全局的、耦合的离散系统。

### 内罚 (IP) 方法的设计

内罚 (Interior Penalty, IP) 方法是一类广泛使用的 DG 方法。其设计围绕着如何定义单元界面上的**数值通量** (numerical flux) 来近似物理上的位移和力，并满足**一致性** (consistency)、**稳定性** (stability) 和**对称性** (symmetry) 等关键性质。

- **一致性**：当将问题的精确解代入离散格式时，离散方程应能精确满足。对于[数值通量](@entry_id:752791)，这意味着当精确解代入时，数值通量应退化为精确的物理量（位移和力）[@problem_id:3558947]。
- **稳定性**：离散格式必须是良定的，保证[解的存在唯一性](@entry_id:177406)，并抑制[数值振荡](@entry_id:163720)。这通常通过证明离散双线性形式的**[矫顽性](@entry_id:159399)** (coercivity) 来实现。
- **对称性**：如果离散双线性形式是对称的，即 $a_h(\boldsymbol{u}_h, \boldsymbol{v}_h) = a_h(\boldsymbol{v}_h, \boldsymbol{u}_h)$，则最终产生的线性系统（[刚度矩阵](@entry_id:178659)）是对称的，这在计算上是有利的。

#### 对称内罚伽辽金 (SIPG) 方法

对称内罚伽辽金 (Symmetric Interior Penalty Galerkin, SIPG) 方法是 IP 家族中最著名和最常用的成员。其双线性形式 $a_h(\boldsymbol{u}_h, \boldsymbol{v}_h)$ 由三部分组成 [@problem_id:3558994] [@problem_id:3558939]：

1.  **单元积分项**：与标准弱形式相同，在所有单元上对 $\boldsymbol{\sigma}(\boldsymbol{u}_h) : \boldsymbol{\varepsilon}(\boldsymbol{v}_h)$ 求和。
    $$
    \sum_{K \in \mathcal{T}_h} \int_K \boldsymbol{\sigma}(\boldsymbol{u}_h) : \boldsymbol{\varepsilon}(\boldsymbol{v}_h) \, dx
    $$
2.  **一致性与伴随一致性项**：这些项用于耦合相邻单元。它们源自分部积分，并以对称的方式构造：
    $$
    - \sum_{F \in \mathcal{F}_h^{\mathrm{int}}} \int_F \left( \{\!\{\boldsymbol{\sigma}(\boldsymbol{u}_h)\}\!} : [\![\boldsymbol{v}_h]\!] + \{\!\{\boldsymbol{\sigma}(\boldsymbol{v}_h)\}\!} : [\![\boldsymbol{u}_h]\!] \right) ds
    $$
    第一个子项确保了一致性，第二个（交换了 $\boldsymbol{u}_h$ 和 $\boldsymbol{v}_h$）确保了整个 bilinear form 的对称性。

3.  **罚项**：该项通过惩罚位移的跳跃来弱化地施加连续性，并确保方法的稳定性。它必须是对称且正定的：
    $$
    + \sum_{F \in \mathcal{F}_h^{\mathrm{int}}} \int_F \eta_F \, [\![\boldsymbol{u}_h]\!] : [\![\boldsymbol{v}_h]\!] \, ds
    $$
    其中 $\eta_F > 0$ 是一个**罚参数**，其取值至关重要。

将这三部分加在一起，就得到了 SIPG 方法的双线性形式。由于每一项都是对称的，所以整个形式也是对称的 [@problem_id:3558939]。

#### 其他 IP 变体 (NIPG, IIPG)

通过调整一致性项，可以得到其他 IP 方法的变体 [@problem_id:3558939]：

- **非对称内罚伽辽金 (NIPG) 方法**：通过改变伴随一致性项的符号，得到一个非对称的[双线性形式](@entry_id:746794)：
  $$
  a_h^{\mathrm{NIPG}}(F) = \dots - \int_F \{\!\{\boldsymbol{\sigma}(\boldsymbol{u}_h)\}\!} : [\![\boldsymbol{v}_h]\!] \, ds + \int_F \{\!\{\boldsymbol{\sigma}(\boldsymbol{v}_h)\}\!} : [\![\boldsymbol{u}_h]\!] \, ds + \text{罚项}
  $$
- **不完全内罚伽辽金 (IIPG) 方法**：完全省略伴随一致性项，也得到一个非对称的形式：
  $$
  a_h^{\mathrm{IIPG}}(F) = \dots - \int_F \{\!\{\boldsymbol{\sigma}(\boldsymbol{u}_h)\}\!} : [\![\boldsymbol{v}_h]\!] \, ds + \text{罚项}
  $$
尽管这些方法是非对称的，但在某些情况下（如[对流](@entry_id:141806)占优问题）可能具有优势。对于弹性力学等自伴问题，SIPG 通常是首选。

### 稳定性与收敛性

#### 罚参数的选择与标定

罚参数 $\eta_F$ 的选择对 IP 方法的成败至关重要。如果太小，方法将不稳定；如果太大，则会过度惩罚跳跃，导致所谓的“过约束”现象，并恶化刚度矩阵的条件数。

为了确保稳定性（[矫顽性](@entry_id:159399)），罚参数 $\eta_F$ 必须足够大，以“控制”来自一致性项的负定贡献。通过使用[迹不等式](@entry_id:756082)和[逆不等式](@entry_id:750800)，可以证明 $\eta_F$ 必须满足一定的标度率 (scaling law) [@problem_id:3558970]。对于 $p$ 次多项式，在直径为 $h_F$ 的界面上，罚参数的正确标度为：
$$
\eta_F \ge C \frac{(p+1)(p+d)}{h_F} (2\mu + \lambda)
$$
其中 $C$ 是一个只依赖于网格形状正则性的常数。这个标度反映了：
- 与 $p^2$（或 $(p+1)(p+d)$）成正比，以应对更高次多项式在界面上可能产生的更大[振荡](@entry_id:267781)。
- 与 $h_F^{-1}$ 成反比，以平衡单元尺寸的影响。
- 与材料刚度 $(2\mu+\lambda)$ 成正比，以应对更硬材料产生的更大应力。

这个选择确保了方法的稳定性常数不随网格加密 ($h \to 0$) 或多项式次数增加 ($p \to \infty$) 而退化。

#### [误差估计](@entry_id:141578)

在罚参数选择得当且精确解足够光滑（例如 $\boldsymbol{u} \in [H^{p+1}(\Omega)]^d$）的假设下，SIPG 方法可以达到最优的[收敛阶](@entry_id:146394)。

- **[先验误差估计](@entry_id:170366)** (A Priori Error Estimates)：这些估计给出了误差与网格尺寸 $h$ 和多项式次数 $p$ 之间的关系。对于 SIPG 方法，我们有 [@problem_id:3559000]：
  - **[能量范数误差](@entry_id:170379)**: $\| \boldsymbol{u} - \boldsymbol{u}_h \|_{\mathrm{DG}} \le C h^{p} \| \boldsymbol{u} \|_{H^{p+1}(\Omega)^d}$
  - **$L^2$ 范数误差**: $\| \boldsymbol{u} - \boldsymbol{u}_h \|_{L^2(\Omega)^d} \le C h^{p+1} \| \boldsymbol{u} \|_{H^{p+1}(\Omega)^d}$
  $L^2$ 范数的更高一阶[收敛率](@entry_id:146534)是通过 Aubin-Nitsche 对偶技巧获得的。

- **[后验误差估计](@entry_id:167288)** (A Posteriori Error Estimates)：这些估计器在计算完成后，利用已求得的数值解 $\boldsymbol{u}_h$ 来[估计误差](@entry_id:263890)的大小，常用于指导[自适应网格加密](@entry_id:143852) ([AMR](@entry_id:204220))。一个典型的基于残差的后验估计器形式如下 [@problem_id:3559000]：
  $$
  \eta^2 := \sum_{K \in \mathcal{T}_h} h_K^2 \| \boldsymbol{f} + \nabla \cdot \boldsymbol{\sigma}(\boldsymbol{u}_h) \|_{L^2(K)^d}^2 + \sum_{F \in \mathcal{F}_h} h_F \| [\![ \boldsymbol{\sigma}(\boldsymbol{u}_h) \boldsymbol{n} ]\!] \|_{L^2(F)^d}^2 + \dots
  $$
  这样的估计器通常是**可靠的** (reliable，误差被估计器从上方控制) 和**高效的** (efficient，估计器被误差从上方控制)，为自适应计算提供了坚实的理论基础。

### 高等议题与实践考量

#### [体积锁定](@entry_id:172606)现象

在处理不可压缩或[近不可压缩材料](@entry_id:752388)（即[泊松比](@entry_id:158876) $\nu \to 0.5$ 或 $\lambda \to \infty$）时，许多标准的位移有限元方法会遭遇**[体积锁定](@entry_id:172606)** (volumetric locking) 现象。此时，离散系统会变得过度刚硬，导致解的精度严重恶化 [@problem_id:3558964]。这是因为离散的位移空间无法很好地满足近似的无散（即[体积守恒](@entry_id:276587)）约束 $\nabla \cdot \boldsymbol{u} \approx 0$。

DG 方法提供了几种避免[体积锁定](@entry_id:172606)的有效途径 [@problem_id:3558964]：

1.  **混合 DG 公式**：引入一个独立的压力变量 $p$ 来作为[拉格朗日乘子](@entry_id:142696)，弱形式地强制不可压缩约束。这种方法将问题转化为一个关于 $(\boldsymbol{u}, p)$ 的[鞍点问题](@entry_id:174221)。为了保证稳定性，位移和压力的离散空间必须满足 Ladyzhenskaya–Babuška–Brezzi (LBB) [inf-sup 条件](@entry_id:174538)。
2.  **改进的原始 DG 公式**：在仅有位移变量的原始公式框架内，通过特殊设计来缓解锁定。例如，可以将罚参数进行各向异性分解，对法向跳跃（与体积变形相关）和切向跳跃（与剪切变形相关）施加不同尺度的惩罚 [@problem_id:3558970]。另一种策略是使用投影稳定化，例如，用 $\nabla \cdot \boldsymbol{u}_h$ 在一个低阶多项式空间上的 $L^2$ 投影来代替其自身，从而减少约束的数量。

#### 可杂交间断伽辽金 (HDG) 方法

HDG 方法是 DG 家族中的一个重要变体，其核心思想是通过引入一个定义在网格骨架（所有界面的集合）上的新未知量——**杂交迹** (hybrid trace) $\hat{\boldsymbol{u}}_h$——来解耦单元内部的计算 [@problem_id:3558942]。

在 HDG 框架下，未知量变为单元内部的 $(\boldsymbol{u}_h, \boldsymbol{\sigma}_h)$ 和界面上的 $\hat{\boldsymbol{u}}_h$。该方法包含三个主要部分：
1.  一组在每个单元上独立的局部方程，它们与原始的 PDE 形式上一致。
2.  一个定义在单元边界上的**数值力通量**，它将单元内部的解与杂交迹 $\hat{\boldsymbol{u}}_h$ 联系起来。
3.  一个只涉及杂交迹 $\hat{\boldsymbol{u}}_h$ 的全局方程，通过要求数值力通量在内部界面上是单值的来建立。

HDG 的一个关键优势是，一旦全局的 $\hat{\boldsymbol{u}}_h$ 被求解出来，单元内部的变量 $(\boldsymbol{u}_h, \boldsymbol{\sigma}_h)$ 就可以通过在每个单元上并行地求解一个局部问题来完全重构。这大大减少了全局耦合自由度的数量。

HDG 方法的稳定性和精度同样依赖于[数值通量](@entry_id:752791)的巧妙设计。一个典型的数值力[通量形式](@entry_id:273811)为 [@problem_id:3558942]：
$$
\widehat{\boldsymbol{\sigma}}_h \boldsymbol{n} = \boldsymbol{\sigma}_h \boldsymbol{n} + \boldsymbol{\tau}_F ( \boldsymbol{u}_h - \hat{\boldsymbol{u}}_h )
$$
这里的 $\boldsymbol{\tau}_F$ 是一个对称正定的稳定化张量。其正号和与 SIPG 罚参数相似的标度率（$\boldsymbol{\tau}_F \propto E p^2 / h_F$）对于保证方法的稳定性至关重要。