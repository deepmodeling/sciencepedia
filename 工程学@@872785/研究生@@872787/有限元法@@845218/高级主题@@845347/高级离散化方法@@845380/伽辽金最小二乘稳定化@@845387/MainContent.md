## 引言
有限元法是求解工程与科学领域中[偏微分方程](@entry_id:141332)的强大工具。然而，当将其应用于[对流](@entry_id:141806)效应远[超扩散](@entry_id:155498)效应的流动问题，或处理不可压缩流体的速度-压力耦合时，标准的伽辽金[有限元法](@entry_id:749389)会遭遇严重的[数值不稳定性](@entry_id:137058)，导致解中出现非物理的[振荡](@entry_id:267781)，从而破坏结果的可靠性。这一缺陷暴露了标准[伽辽金法](@entry_id:749698)在特定问题类别中的内在局限性，构成了计算力学领域一个亟待解决的知识空白。

为应对这一挑战，伽辽金/最小二乘（Galerkin/Least-Squares, GLS）稳定化方法应运而生。它是一种通用且功能强大的技术，通过在原始[弱形式](@entry_id:142897)中巧妙地引入一个基于方程残差的附加项来恢复稳定性，同时不破坏方法的一致性。本文将系统地引导读者深入理解GLS方法。在“原理与机制”一章中，我们将剖析不稳定的根源，构建GLS的数学框架，并揭示其稳定化机制。接着，在“应用与跨学科连接”一章中，我们将展示GLS思想如何应用于[计算流体动力学](@entry_id:147500)、[固体力学](@entry_id:164042)乃至更广泛的[多物理场](@entry_id:164478)问题。最后，通过一系列“动手实践”练习，您将有机会将理论知识转化为实际的编程和分析技能。

## 原理与机制

在上一章中，我们介绍了[有限元法](@entry_id:749389)作为求解偏微分方程的通用框架。标准[伽辽金法](@entry_id:749698)在应用于自伴、正定的[椭圆问题](@entry_id:146817)（如纯[扩散](@entry_id:141445)问题）时表现出色。然而，当我们将这一方法应用于更复杂的问题，特别是那些包含显著[对流](@entry_id:141806)项或具有[鞍点](@entry_id:142576)结构（如[不可压缩流体](@entry_id:181066)）的问题时，其内在的局限性便会显现。标准的伽辽金离散格式可能会变得不稳定，产生非物理的、剧烈的[数值振荡](@entry_id:163720)，从而严重污染计算结果的精度和可靠性。

本章旨在深入探讨一种强大而通用的稳定化技术——伽辽金/最小二乘法（Galerkin/Least-Squares, GLS）。我们将从问题的根源出发，揭示标准[伽辽金法](@entry_id:749698)在[对流](@entry_id:141806)主导问题中失效的根本原因。在此基础上，我们将系统地构建GLS方法的数学形式，并剖析其稳定化机制。通过理论分析、傅里叶[模态分析](@entry_id:163921)以及与其它稳定化方法的关联，我们将阐明GLS方法如何通过在[变分形式](@entry_id:166033)中引入基于残差的一致性项，来恢复离散系统的稳定性，同时保持数值格式的[高阶精度](@entry_id:750325)潜力。

### [对流](@entry_id:141806)主导问题的挑战：为何需要稳定化？

为了理解稳定化方法的必要性，我们首先考察一个典型的[对流-扩散](@entry_id:148742)-反应模型。考虑在有界区域 $\Omega \subset \mathbb{R}^d$ 上带有齐次狄利克雷边界条件的定常问题：

$$
\mathcal{L} u := - \varepsilon \Delta u + \boldsymbol{b} \cdot \nabla u + c u = f \quad \text{in } \Omega,
$$
$$
u = 0 \quad \text{on } \partial \Omega.
$$

其中，$\varepsilon > 0$ 是[扩散](@entry_id:141445)系数，$\boldsymbol{b}$ 是给定的[对流](@entry_id:141806)速度场，$c \ge 0$ 是反应系数，$f$ 是[源项](@entry_id:269111)。该方程描述了由[扩散](@entry_id:141445)（$-\varepsilon \Delta u$）、[对流](@entry_id:141806)（$\boldsymbol{b} \cdot \nabla u$）和反应（$c u$）共同作用的物理过程。

标准[伽辽金法](@entry_id:749698)的弱形式寻求 $u \in H_0^1(\Omega)$，使得对于所有[检验函数](@entry_id:166589) $v \in H_0^1(\Omega)$，均有 $a(u,v) = \ell(v)$，其中[双线性形式](@entry_id:746794) $a(\cdot,\cdot)$ 和线性泛函 $\ell(\cdot)$ 定义为：

$$
a(u,v) := \int_\Omega \varepsilon (\nabla u \cdot \nabla v) \, dx + \int_\Omega (\boldsymbol{b} \cdot \nabla u) v \, dx + \int_\Omega c u v \, dx,
$$
$$
\ell(v) := \int_\Omega f v \, dx.
$$

[伽辽金法](@entry_id:749698)稳定性的核心在于[双线性形式](@entry_id:746794) $a(\cdot,\cdot)$ 的**[矫顽性](@entry_id:159399)(coercivity)**。一个[双线性形式](@entry_id:746794)被称为矫顽的，如果存在一个常数 $\alpha > 0$，使得对于空间中所有的非零函数 $v$，都有 $a(v,v) \ge \alpha \|v\|^2$，其中 $\|\cdot\|$ 是该函数空间上的范数。对于 $H_0^1(\Omega)$ 空间，我们通常使用能量范数，其等价于 $H^1$-[半范数](@entry_id:264573)，即 $\|v\|_{H_0^1} = \|\nabla v\|_{L^2}$。

我们来分析 $a(v,v)$ 的各项贡献 [@problem_id:2557974]：

$$
a(v,v) = \varepsilon \int_\Omega |\nabla v|^2 \, dx + \int_\Omega (\boldsymbol{b} \cdot \nabla v) v \, dx + \int_\Omega c v^2 \, dx.
$$

[扩散](@entry_id:141445)项是正定的，提供了 $\varepsilon \|\nabla v\|_{L^2}^2$ 的正贡献。由于 $c \ge 0$，反应项也是非负的。问题的关键在于[对流](@entry_id:141806)项 $\int_\Omega (\boldsymbol{b} \cdot \nabla v) v \, dx$。利用[分部积分](@entry_id:136350)和 $v|_{\partial\Omega}=0$ 的边界条件，我们可以得到：

$$
\int_\Omega (\boldsymbol{b} \cdot \nabla v) v \, dx = \frac{1}{2} \int_\Omega \boldsymbol{b} \cdot \nabla(v^2) \, dx = - \frac{1}{2} \int_\Omega (\nabla \cdot \boldsymbol{b}) v^2 \, dx.
$$

于是，能量平衡关系为：

$$
a(v,v) = \varepsilon \|\nabla v\|_{L^2}^2 + \int_\Omega \left(c - \frac{1}{2}\nabla \cdot \boldsymbol{b}\right) v^2 \, dx.
$$

在一个常见且重要的情况下，即[对流](@entry_id:141806)场无散（$\nabla \cdot \boldsymbol{b} = 0$），[对流](@entry_id:141806)项的积分为零。这意味着[对流](@entry_id:141806)项本身是**反对称(skew-symmetric)**的，它对 $a(v,v)$ 的贡献为零，不提供任何对能量范数的控制。此时，我们有 $a(v,v) \ge \varepsilon \|\nabla v\|_{L^2}^2$。虽然对于任意固定的 $\varepsilon > 0$，双线性形式都是矫顽的，但矫顽性常数 $\alpha$ 的大小与[扩散](@entry_id:141445)系数 $\varepsilon$ 成正比。

当问题为**[对流](@entry_id:141806)主导(advection-dominated)**时，即 $\varepsilon$ 相对于 $\|\boldsymbol{b}\|$ 非常小，[矫顽性](@entry_id:159399)常数 $\alpha \sim \mathcal{O}(\varepsilon)$ 会变得非常小。根据[Céa引理](@entry_id:165386)，伽辽金解的误差满足 $\|u - u_h\|_{H_0^1} \le \frac{C}{\alpha} \inf_{v_h \in V_h} \|u - v_h\|_{H_0^1}$。当 $\alpha \to 0$ 时，[误差估计](@entry_id:141578)中的常数 $\frac{C}{\alpha}$ 会发生“爆炸”，使得该理论估计失去意义。这正是标准[伽辽金法](@entry_id:749698)在[对流](@entry_id:141806)主导问题中失效的理论根源。

在离散层面，这一不稳定性的表现形式是，当网格尺寸 $h$ 不足够小以解析[边界层](@entry_id:139416)或内部层时（即网格[佩克莱数](@entry_id:141791) $\mathrm{Pe}_h = \frac{\|\boldsymbol{b}\| h}{2\varepsilon} \gg 1$），数值解会出现沿[流线](@entry_id:266815)方向传播的、非物理的剧烈[振荡](@entry_id:267781)。因此，我们必须对标准伽辽金方法进行修正，以恢复其在[对流](@entry_id:141806)主导情况下的稳定性，这就是稳定化方法的核心任务。

### 伽辽金/最小二乘 (GLS) 方法的构建

GLS方法的核心思想是在标准伽辽金公式的基础上，额外增加一个惩罚每个单元内部强形式方程残差的项。这个附加项被精心设计，旨在增强稳定性的同时，不破坏原始方法的一致性。

对于一般的二阶[线性微分算子](@entry_id:174781) $\mathcal{L}$，[GLS稳定化](@entry_id:170505)的[弱形式](@entry_id:142897)可以统一地写出。考虑如下边值问题及其算子形式：
$$
\mathcal{L} u := -\nabla \cdot (\kappa \nabla u) + \boldsymbol{\beta} \cdot \nabla u + c u = f \quad \text{in } \Omega, \qquad u=0 \quad \text{on }\partial\Omega.
$$

我们定义伽辽金有限元解 $u_h$ 和检验函数 $v_h$ 属于定义在网格 $\mathcal{T}_h$ 上的有限元[子空间](@entry_id:150286) $V_h \subset H_0^1(\Omega)$。[GLS稳定化](@entry_id:170505)方法寻求 $u_h \in V_h$，使得对于所有 $v_h \in V_h$，下式成立 [@problem_id:2561124]：

$$
(\kappa \nabla u_h, \nabla v_h)_\Omega + (\boldsymbol{\beta}\cdot \nabla u_h, v_h)_\Omega + (c u_h, v_h)_\Omega + \sum_{K\in \mathcal{T}_h} \tau_K ( \mathcal{L}u_h - f, \mathcal{L}v_h )_K = (f, v_h)_\Omega.
$$

这里 $(\cdot, \cdot)_\Omega$ 表示在整个区域 $\Omega$ 上的 $L^2$ [内积](@entry_id:158127)，而 $(\cdot, \cdot)_K$ 表示在单个单元 $K \in \mathcal{T}_h$ 上的 $L^2$ [内积](@entry_id:158127)。此方程的前三项和右端项构成了标准的伽辽金弱形式。新增的第四项即为 **[GLS稳定化](@entry_id:170505)项**，其具有以下关键特征：

1.  **基于残差**: 稳定化项作用于强形式的**残差** $R(u_h) = \mathcal{L}u_h - f$。这意味着如果有限元解 $u_h$ 恰好是[强解](@entry_id:198344)，残差为零，稳定化项也为零。

2.  **单元[内积](@entry_id:158127)分**: 稳定化项是在每个单元 $K$ 上独立计算然后求和得到的。这使得该方法易于在标准有限元程序框架内实现。

3.  **最小二乘形式**: 在每个单元内，稳定化项具有最小二乘的结构，即残差的 $L^2$ 范数的平方。更准确地说，它是通过将算子 $\mathcal{L}$ 同时作用在[试探函数](@entry_id:756165) $u_h$ 和检验函数 $v_h$ 上来构造的。

4.  **稳定化参数 $\tau_K$**: 这是一个在每个单元 $K$ 上定义的正数，称为**稳定化参数**。$\tau_K$ 的量纲被选择用来确保 $\tau_K (\mathcal{L}w, \mathcal{L}z)_K$ 具有能量的量纲。$\tau_K$ 的取值至关重要，它控制着稳定化项的强度，必须能够自适应地平衡[对流](@entry_id:141806)和[扩散](@entry_id:141445)的相对重要性。

### GLS方法的基本性质

GLS方法的设计使其具有若干优良的数学性质，这些性质是其成功应用的基础。

#### 一致性 (Consistency)

一个数值方法被称为**一致的**，如果原始[偏微分方程](@entry_id:141332)的精确解也满足该数值方法的离散方程。GLS方法天生就是一致的。为了证明这一点，我们假设 $u$ 是[微分方程](@entry_id:264184)的足够光滑的精确解，即 $\mathcal{L}u = f$ 在 $\Omega$ 中处处成立。将 $u$ 代入GLS方程的左侧，稳定化项变为 [@problem_id:2603889]：

$$
\sum_{K\in \mathcal{T}_h} \tau_K ( \mathcal{L}u - f, \mathcal{L}v_h )_K = \sum_{K\in \mathcal{T}_h} \tau_K ( f - f, \mathcal{L}v_h )_K = \sum_{K\in \mathcal{T}_h} \tau_K ( 0, \mathcal{L}v_h )_K = 0.
$$

这意味着，对于精确解 $u$，GLS方程退化为标准伽辽金方程，而我们知道精确解本身就满足标准伽辽金方程。因此，GLS方法是一致的。这个性质至关重要，因为它保证了当[网格加密](@entry_id:168565)（$h \to 0$）时，只要解足够光滑，数值解将收敛到正确的物理真解。

#### 稳定性和对称性

[GLS稳定化](@entry_id:170505)项对整个系统的[双线性形式](@entry_id:746794) $a_h(\cdot,\cdot)$ 有直接影响。考虑齐次问题（$f=0$），总的双线性形式为：
$$
a_h(u_h, v_h) = a(u_h, v_h) + s(u_h, v_h)
$$
其中 $a(\cdot,\cdot)$ 是标准伽辽金[双线性形式](@entry_id:746794)，$s(u_h, v_h) = \sum_K \tau_K (\mathcal{L}u_h, \mathcal{L}v_h)_K$ 是稳定化项。

考察 $a_h(u_h, u_h)$：
$$
a_h(u_h, u_h) = a(u_h, u_h) + \sum_{K\in \mathcal{T}_h} \tau_K \|\mathcal{L}u_h\|_{0,K}^2.
$$
由于 $(\cdot, \cdot)_K$ 是[内积](@entry_id:158127)，$\|\mathcal{L}u_h\|_{0,K}^2 \ge 0$。因此，为了保证稳定化项对系统的能量（或矫顽性）有非负的贡献，我们必须要求 $\tau_K > 0$。如果错误地选择了 $\tau_K  0$，稳定化项反而会从系统中“抽取”能量，导致更严重的不稳定性。

我们可以通过一个简单的例子来说明这一点。考虑一维纯[对流](@entry_id:141806)问题 $\beta u' = f$，在一个仅包含一个内部节点的网格上，[基函数](@entry_id:170178)为[帽子函数](@entry_id:171677) $\varphi$。可以计算出稳定化后的[双线性形式](@entry_id:746794)为 $a_h(\varphi, \varphi) = 4\tau\beta^2$ [@problem_id:2561161]。为了保证系统的矫顽性，即 $a_h(\varphi, \varphi)  0$，我们必须有 $\tau  0$。若取 $\tau=-1$ 和 $\beta=1$，则 $a_h(\varphi, \varphi)=-4$，[系统矩阵](@entry_id:172230)将不是正定的，数值方法会彻底失败。

关于对称性，稳定化项 $s(u_h, v_h)$ 本身是**对称的**，因为 $s(u_h, v_h) = \sum_K \tau_K (\mathcal{L}u_h, \mathcal{L}v_h)_K = \sum_K \tau_K (\mathcal{L}v_h, \mathcal{L}u_h)_K = s(v_h, u_h)$。然而，整个[双线性形式](@entry_id:746794) $a_h(\cdot, \cdot)$ 的对称性取决于标准伽辽金部分 $a(\cdot, \cdot)$。如前所述，[对流](@entry_id:141806)项 $\int_\Omega (\boldsymbol{\beta} \cdot \nabla u) v \, dx$ 是反对称的。因此，除非[对流](@entry_id:141806)项消失（即 $\boldsymbol{\beta}=0$），否则整个GLS系统仍然是非对称的 [@problem_id:2603889]。GLS方法通过增加一个对称的正定项来增强稳定性，但它并不改变原始问题的非自伴性质。

### 稳定化机制的深入剖析

我们已经建立了GLS方法的数学形式，现在需要理解它究竟是如何抑制[数值振荡](@entry_id:163720)的。我们可以从两个互补的角度来剖析其工作机制：[傅里叶分析](@entry_id:137640)和与经典差分格式的联系。

#### 傅里叶分析视角：引入[数值耗散](@entry_id:168584)

[对流](@entry_id:141806)主导问题中的非物理[振荡](@entry_id:267781)主要是由标准[伽辽金法](@entry_id:749698)无法抑制高频（短波长）误差模态引起的。我们可以通过[傅里叶分析](@entry_id:137640)（或[冯·诺依曼稳定性分析](@entry_id:145718)）来量化[数值格式](@entry_id:752822)对不同频率模态的影响。

考虑一个一维线性[对流](@entry_id:141806)方程 $u_t + \beta u_x = 0$，采用线性有限元进行空间离散，并用[前向欧拉法](@entry_id:141238)进行时间离散。我们可以分析一个具有波数 $k$ 的离散傅里叶模态 $U_j^n = \widehat{U}^n e^{i j \theta}$（其中 $\theta=kh$ 是无量纲波数）在一个时间步长 $\Delta t$ 内的演化。其振幅的变化由**放大因子** $g(\theta) = U_j^{n+1} / U_j^n$ 描述。如果 $|g(\theta)|  1$，该模态不稳定；如果 $|g(\theta)| = 1$，该模态是中性稳定的，无衰减地传播；如果 $|g(\theta)|  1$，该模态被耗散或衰减。

对于标准[伽辽金法](@entry_id:749698)（即 $\tau=0$），可以推导出其[放大因子](@entry_id:144315)为 [@problem_id:2561125]：

$$
g_{\mathrm{G}}(\theta) = 1 - \frac{3i\beta\Delta t \sin\theta}{h(2+\cos\theta)}.
$$

由于这是一个纯虚数加1，其模长 $|g_{\mathrm{G}}(\theta)|$ 在前向欧拉法的稳定性极限内约等于1。这意味着所有频率的误差模态都不会被衰减，高频[振荡](@entry_id:267781)一旦产生就会持续存在。

而对于[GLS稳定化](@entry_id:170505)的格式，其放大因子变为：

$$
g_{\mathrm{GLS}}(\theta) = 1 - \Delta t \frac{i\beta\sin\theta + \frac{2\tau \beta^2}{h}(1-\cos\theta)}{h\frac{2+\cos\theta}{3} - i \tau \beta \sin\theta}.
$$

这个表达式的分子中多出了一项 $\frac{2\tau \beta^2}{h}(1-\cos\theta)$，它是一个实数项。这一项的出现使得 $g_{\mathrm{GLS}}(\theta)$ 的模长严格小于1（对于 $\theta \neq 0$）。这个实数项正比于 $(1-\cos\theta)$，对于高频模态（例如 $\theta=\pi$，对应网格尺度上的最短波），该项达到最大值。这表明GLS方法引入了**数值耗散 (numerical dissipation)**，并且这种耗散是**选择性的**：它主要作用于导致[振荡](@entry_id:267781)的高频模态，而对低频的长波模态影响较小，从而在抑制[振荡](@entry_id:267781)和保持精度之间取得了良好的平衡。

#### 与迎风格式的联系

稳定化机制的另一个直观理解来自于它与经典[迎风](@entry_id:756372)（upwind）差分格式的联系。[迎风格式](@entry_id:756374)通过在离散[对流](@entry_id:141806)项时偏向信息来源（上游）的节点来保证稳定性。

考虑一维定常[对流](@entry_id:141806)[扩散](@entry_id:141445)问题 $-\kappa u'' + \beta u' = f$。我们可以推导GLS方法在内部节点上形成的离散[代数方程](@entry_id:272665)（即差分格式）。在纯[对流](@entry_id:141806)极限下（$\kappa \to 0^+$），对于正的[对流](@entry_id:141806)速度 $\beta  0$（信息从左向右传播），我们希望离散格式中节点 $i$ 的值主要受其上游邻居 $i-1$ 的影响，而下游邻居 $i+1$ 的权重应该很小甚至为零。

通过详细的推导可以发现，GLS格式在节点 $i$ 处对下游节点 $i+1$ 的贡献系数为 $C_{i+1} = -\frac{\tau\beta^2}{h} + \frac{\beta}{2}$（在 $\kappa \to 0$ 的极限下）。为了实现迎风特性，我们要求这个系数为零 [@problem_id:2561138]：

$$
-\frac{\tau\beta^2}{h} + \frac{\beta}{2} = 0 \quad \implies \quad \tau = \frac{h}{2\beta}.
$$

这个结果非常深刻。它表明，当稳定化参数 $\tau$ 被恰当地选择为 $\frac{h}{2\beta}$ 时，GLS方法在纯[对流](@entry_id:141806)极限下等价于一阶迎风[有限差分格式](@entry_id:749361)。这为我们如何选择稳定化参数提供了重要的指导，并揭示了[GLS稳定化](@entry_id:170505)项在效果上等同于引入了沿流线方向的、有控制的[人工黏性](@entry_id:756576)。

### 稳定化参数 $\tau_K$ 的选择

前面的讨论表明，稳定化参数 $\tau_K$ 的选择是GLS方法成功的关键。$\tau_K$ 必须能够适应局部流动和网格的特性，即在[对流](@entry_id:141806)主导的区域表现出迎风特性，而在[扩散](@entry_id:141445)主导的区域减弱其影响，以免过度耗散。

一个广泛使用的 $\tau_K$ 设计准则是基于对单元内不同物理过程的[特征时间尺度](@entry_id:276738)进行平衡。对于[对流-扩散](@entry_id:148742)问题，我们有两个关键的时间尺度：

-   **[对流](@entry_id:141806)时间尺度**: 粒子穿越一个尺寸为 $h_K$ 的单元所需的时间，$\tau_{\text{adv}} \sim h_K / |\boldsymbol{\beta}|$.
-   **[扩散时间尺度](@entry_id:264558)**: 物理量通过[扩散](@entry_id:141445)作用传播一个距离 $h_K$ 所需的时间，$\tau_{\text{diff}} \sim h_K^2 / \kappa$.

稳定化参数 $\tau_K$ 应该在这两种尺度之间平滑过渡。一种常见的构造方法是使用这些时间尺度的倒数（即频率）的平方和的平方根的倒数 [@problem_id:2561126]：

$$
\tau_K = \left( \left(\frac{1}{\tau_{\text{adv}}}\right)^2 + \left(\frac{1}{\tau_{\text{diff}}}\right)^2 \right)^{-1/2}
$$

通过与一维迎风格式的精确关系以及对[拉普拉斯算子](@entry_id:146319)的符号分析，可以确定该公式中的无量纲常数。对于线性元，一个被广泛采用的公式是：

$$
\tau_K = \left( \left(\frac{2|\boldsymbol{\beta}|}{h_K}\right)^2 + \left(\frac{4\kappa}{h_K^2}\right)^2 \right)^{-1/2}.
$$

我们来检验这个公式的极限行为：
-   **[对流](@entry_id:141806)主导 ($\kappa \to 0$)**: $\tau_K \approx \left( (\frac{2|\boldsymbol{\beta}|}{h_K})^2 \right)^{-1/2} = \frac{h_K}{2|\boldsymbol{\beta}|}$。这恰好是我们之[前推](@entry_id:158718)导出的能产生迎风格式的参数值。
-   **[扩散](@entry_id:141445)主导 ($|\boldsymbol{\beta}| \to 0$)**: $\tau_K \approx \left( (\frac{4\kappa}{h_K^2})^2 \right)^{-1/2} = \frac{h_K^2}{4\kappa}$。这个尺度与处理纯二阶问题的[最小二乘法](@entry_id:137100)所要求的参数尺度相匹配。

因此，这个统一的公式能够在[对流](@entry_id:141806)主导和[扩散](@entry_id:141445)主导的极限情况下自动恢复到正确的标度，并在过渡区域提供平滑的插值，使其成为一个非常实用和鲁棒的选择。

### 理论诠释与推广

GLS方法不仅是一个实用的计算工具，其背后还有更深刻的理论支撑，并且其核心思想可以推广到更广泛的问题。

#### 与SUPG方法的关系

[流线](@entry_id:266815)迎风/皮特洛夫-伽辽金 (Streamline-Upwind/[Petrov-Galerkin](@entry_id:174072), SUPG) 方法是另一种著名的稳定化技术。它通过修改[检验函数](@entry_id:166589)空间来引入稳定性，其稳定化项的形式为：
$$
S_{\mathrm{SUPG}}(u_h,v_h) = \sum_{K\in \mathcal{T}_h} \tau_K (\mathcal{L}u_h - f, \boldsymbol{\beta}\cdot\nabla v_h)_K.
$$
SUPG与GLS的主要区别在于作用于检验函数 $v_h$ 的算子：SUPG中使用的是[流线](@entry_id:266815)[方向导数](@entry_id:189133)算子 $\boldsymbol{\beta}\cdot\nabla$，而GLS中使用的是完整的[微分算子](@entry_id:140145) $\mathcal{L}$。

然而，在特定条件下，两者是等价的。对于[常系数](@entry_id:269842)问题，如果采用线性元（$P^1$元），并且反应系数 $c=0$，那么GLS和SUPG方法是完全相同的 [@problem_id:2561169]。这是因为对于线性函数 $v_h$，其[二阶导数](@entry_id:144508)在单元内部恒为零，即 $\Delta v_h|_K = 0$。因此，在单元内部：
$$
\mathcal{L}v_h = -\varepsilon \Delta v_h + \boldsymbol{\beta}\cdot\nabla v_h + c v_h = 0 + \boldsymbol{\beta}\cdot\nabla v_h + 0 = \boldsymbol{\beta}\cdot\nabla v_h.
$$
在这种情况下，两种方法的稳定化项完全一致。这表明，GLS可以看作是SUPG的一种推广，它自然地包含了[扩散](@entry_id:141445)项对稳定性的影响，使其在理论上更加完善。

#### 与无残差[气泡函数](@entry_id:176111)的等价性

[GLS稳定化](@entry_id:170505)还有一个更深刻的解释，即它与多尺度方法中的**无残差[气泡函数](@entry_id:176111) (residual-free bubbles)** 方法等价 [@problem_id:2561116]。其思想是在标准的有限元空间（例如线性元）上，为每个单元增加一个“[气泡函数](@entry_id:176111)”。这个[气泡函数](@entry_id:176111)是在单元内部不为零，但在单元边界上为零的更高阶多项式。

这个[气泡函数](@entry_id:176111)被特殊地定义为在单元内部精确地满足一个以粗尺度解的残差为[源项](@entry_id:269111)的局部[微分方程](@entry_id:264184)。然后，通过一个称为**[静态凝聚](@entry_id:176722) (static condensation)** 的过程，在单元层面将[气泡函数](@entry_id:176111)的自由度精确地消去。令人惊讶的是，这个过程最终得到的关于粗尺度未知量（如线性元的节点值）的修正方程，与使用某个特定 $\tau_K$ 的GLS方程完全相同。

例如，对于一维[对流](@entry_id:141806)[扩散](@entry_id:141445)问题，通过[静态凝聚](@entry_id:176722)推导出的等效稳定化参数为：
$$
\tau_K = \frac{h}{2a}\coth\left(\frac{ah}{2\kappa}\right) - \frac{\kappa}{a^{2}}.
$$
这个表达式被称为“最优”参数，因为它源于一个更底层的子尺度模型。这个等价性揭示了GLS方法的本质：它并非简单地在方程中添加一个人工项，而是隐式地将标准粗网格无法捕捉到的“[子网](@entry_id:156282)格尺度”信息重新引入到离散系统中，从而对粗尺度解进行修正。

#### 推广：皮特洛夫-伽辽金思想的应用

GLS/SUPG方法所体现的“通过惩罚残差来稳定不满足[inf-sup条件](@entry_id:746626)的离散格式”这一哲学思想，具有极大的普适性。一个重要的例子是其在计算流体力学中对不可压缩斯托克斯（Stokes）方程的应用。

当使用等阶（例如，$P_1$-$P_1$）的单元来近似速度和压力时，离散格式不满足LBB（Ladyzhenskaya-Babuška-Brezzi）或[inf-sup条件](@entry_id:746626)，导致压力解出现棋盘状的[伪振荡](@entry_id:152404)。为了解决这个问题，可以引入压力稳定/皮特洛夫-伽辽金 (Pressure-Stabilizing [Petrov-Galerkin](@entry_id:174072), PSPG) 方法 [@problem_id:2561118]。[PSPG方法](@entry_id:163536)在[斯托克斯方程](@entry_id:196346)的弱形式中增加了一个稳定化项，该项惩罚[动量方程](@entry_id:197225)的残差，并用压力的梯度作为检验函数：
$$
\sum_{K \in \mathcal{T}_h} \tau_K ( -\mu \Delta \boldsymbol{u}_h + \nabla p_h - \boldsymbol{f}, \nabla q_h )_{K}.
$$
为了保证方法的稳定性并获得压力鲁棒的[误差估计](@entry_id:141578)（即[误差界](@entry_id:139888)不依赖于压力的大小），稳定化参数 $\tau_K$ 的标度必须正确。通过量纲分析或更严格的稳定性分析可以推导出，其正确的标度为 $\tau_K \propto h_K^2/\mu$。

这个例子有力地证明了，从[对流](@entry_id:141806)[扩散](@entry_id:141445)问题发展而来的基于残差的稳定化思想，是一个可以灵活应用于各种不同物理问题和数值挑战的强大[范式](@entry_id:161181)。它为处理那些标准伽辽金方法失效的复杂问题提供了一个系统性的设计框架。