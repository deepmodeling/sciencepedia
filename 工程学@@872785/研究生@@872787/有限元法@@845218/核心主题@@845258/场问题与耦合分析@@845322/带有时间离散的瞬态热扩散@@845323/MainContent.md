## 引言
[瞬态热扩散](@entry_id:176511)是描述物体内部温度场随时间演化的基本物理过程，其在从航空航天工程中的[热防护系统](@entry_id:154016)设计，到微电子芯片的散[热管理](@entry_id:146042)，再到地球物理学中的气候演变模拟等众多科学与工程领域中都扮演着核心角色。精确预测和控制这些瞬态热行为对于确保系统性能、安全性和可靠性至关重要。然而，描述这些现象的[偏微分方程](@entry_id:141332)往往形式复杂，难以求得解析解，这为我们理解和设计实际系统带来了巨大的知识鸿沟。

有限元方法（FEM）为解决这一难题提供了强大而通用的数值工具。本文旨在系统地引导读者走过从物理原理到可[计算模型](@entry_id:152639)的全过程，填补理论与实践之间的差距。通过学习本文，您将掌握如何将一个连续的时空问题转化为计算机可以求解的一系列[代数方程](@entry_id:272665)。文章分为三个核心部分：
*   **原理与机制** 将从第一性原理出发，推导[瞬态热传导](@entry_id:170260)的控制方程及其弱形式，并构建有限元[半离散系统](@entry_id:754680)，最终深入探讨时间积分方案的选择及其稳定性，为您奠定坚实的理论基础。
*   **应用与跨学科联系** 将展示如何将基本理论框架扩展到处理复杂的现实世界问题，如[非线性](@entry_id:637147)材料、[相变过程](@entry_id:147919)、移动边界，并揭示其在[计算流体力学](@entry_id:747620)、气候科学等领域的广泛联系。
*   **动手实践** 则通过一系列精心设计的编程练习，帮助您将理论知识转化为实际的编程能力和问题解决技巧。

现在，让我们从构建解决[瞬态热扩散](@entry_id:176511)问题的数学和数值基础开始，深入探讨其背后的原理与机制。

## 原理与机制

在上一章中，我们介绍了[瞬态热扩散](@entry_id:176511)问题的背景和重要性。本章将深入探讨控制这一现象的物理原理和数学模型，并为后续章节中有限元方法的应用奠定理论基础。我们将从[能量守恒](@entry_id:140514)定律出发，建立控制[偏微分方程](@entry_id:141332)，然后通过有限元方法将其转化为一个[常微分方程组](@entry_id:266774)，最后讨论求解该[方程组](@entry_id:193238)的[时间离散化](@entry_id:169380)方法及其稳定性。

### [瞬态热传导](@entry_id:170260)的控制方程

[瞬态热传导](@entry_id:170260)问题的数学描述源于[热力学](@entry_id:141121)中的[能量守恒](@entry_id:140514)基本定律。考虑一个任意控制体 $V$，其内部能量的变化率等于流入该[控制体](@entry_id:143882)的净热量与内部热源产生的热量之和。

#### 强形式的建立

我们将这一定律表述为数学形式。在没有力学功的情况下，控制体 $V$ 内部热能的变化率可以表示为：

$$
\frac{d}{dt} \int_V \rho c T \,dV
$$

其中，$\rho$ 是材料的 **质量密度**（单位：$\mathrm{kg} \cdot \mathrm{m}^{-3}$），$c$ 是 **比[热容](@entry_id:137594)**（单位：$\mathrm{J} \cdot \mathrm{kg}^{-1} \cdot \mathrm{K}^{-1}$），$T$ 是温度场。假设材料属性不随时间变化，该表达式变为 $\int_V \rho c \frac{\partial T}{\partial t} \,dV$。

热量通过[控制体](@entry_id:143882)边界 $\partial V$ 的净流入速率由热[通量矢量](@entry_id:273577) $\mathbf{q}$ 的[面积分](@entry_id:275394)给出，即 $-\oint_{\partial V} \mathbf{q} \cdot \mathbf{n} \,dS$，其中 $\mathbf{n}$ 是指向外部的[单位法向量](@entry_id:178851)，负号表示指向外的[热通量](@entry_id:138471)对应于热量的流失。根据[高斯散度定理](@entry_id:188065)，这个面积分可以转换成[体积分](@entry_id:171119) $-\int_V \nabla \cdot \mathbf{q} \,dV$。

此外，控制体内部可能存在体积热源 $q$（单位：$\mathrm{W} \cdot \mathrm{m}^{-3}$），其总生热率为 $\int_V q \,dV$。

综合以上各项，[能量守恒的积分形式](@entry_id:202417)为：

$$
\int_V \rho c \frac{\partial T}{\partial t} \,dV = -\int_V \nabla \cdot \mathbf{q} \,dV + \int_V q \,dV
$$

由于此等式对任意[控制体](@entry_id:143882) $V$ 都成立，因此被积函数必须处处相等，从而得到[能量守恒](@entry_id:140514)的局部（[微分](@entry_id:158718)）形式：

$$
\rho c \frac{\partial T}{\partial t} = - \nabla \cdot \mathbf{q} + q
$$

为了封闭这个方程，我们需要一个描述[热通量](@entry_id:138471) $\mathbf{q}$ 与温度场 $T$ 之间关系的[本构方程](@entry_id:138559)。**[傅里叶热传导定律](@entry_id:138911) (Fourier's law)** 指出，热量倾向于从高温区域流向低温区域，且热通量大小与温度梯度成正比：

$$
\mathbf{q} = -k \nabla T
$$

这里，$k$ 是材料的 **[导热系数](@entry_id:147276)**（对于[各向同性材料](@entry_id:170678)是一个标量，单位：$\mathrm{W} \cdot \mathrm{m}^{-1} \cdot \mathrm{K}^{-1}$；对于各向异性材料则是一个对称正定张量）。它量化了材料传导热量的能力。

将傅里叶定律代入[能量守恒方程](@entry_id:748978)，我们得到[瞬态热扩散](@entry_id:176511)的控制[偏微分方程](@entry_id:141332)，也称为[热方程](@entry_id:144435)：

$$
\rho c \frac{\partial T}{\partial t} - \nabla \cdot (k \nabla T) = q \quad \text{在 } \Omega \times (0, t_f]
$$

这是一个描述温度场 $T(\mathbf{x}, t)$ 在空间域 $\Omega$ 和时间区间 $(0, t_f]$ 内演化的方程。为了得到唯一解，该方程必须辅以初始条件和边界条件 [@problem_id:2607748]。

#### 初始条件与边界条件

**[初始条件](@entry_id:152863)** 指定了在初始时刻 $t=0$ 时域内的温度[分布](@entry_id:182848)：

$$
T(\mathbf{x}, 0) = T_0(\mathbf{x}) \quad \text{在 } \Omega
$$

**边界条件** 则描述了系统与外界环境的相互作用，通常分为三类：

1.  **[第一类边界条件](@entry_id:142800)（狄利克雷，Dirichlet）**：在边界的某一部分 $\Gamma_D$ 上直接指定温度值 $\overline{T}$。
    $$
    T = \overline{T} \quad \text{在 } \Gamma_D \times (0, t_f]
    $$

2.  **第二类边界条件（诺伊曼，Neumann）**：在边界的某一部分 $\Gamma_N$ 上指定法向[热通量](@entry_id:138471) $\overline{q}_n$。根据[傅里叶定律](@entry_id:136311)，法向热通量为 $\mathbf{q} \cdot \mathbf{n} = -k \nabla T \cdot \mathbf{n}$。因此，指定向外的法向热通量为 $\overline{q}_n$ 意味着：
    $$
    - k \nabla T \cdot \mathbf{n} = \overline{q}_n \quad \text{在 } \Gamma_N \times (0, t_f]
    $$
    其中 $\overline{q}_n$ 的单位是 $\mathrm{W} \cdot \mathrm{m}^{-2}$。一个特殊情况是[绝热边界](@entry_id:162724)，此时 $\overline{q}_n = 0$。

3.  **第三类边界条件（罗宾，Robin）**：在边界的某一部分 $\Gamma_R$ 上，热通量与物体表面温度 $T$ 和环境温度 $T_\infty$ 之差成正比，这通常用来模拟[对流换热](@entry_id:151349)。
    $$
    - k \nabla T \cdot \mathbf{n} = h (T - T_\infty) \quad \text{在 } \Gamma_R \times (0, t_f]
    $$
    这里的 $h$ 是 **[对流换热系数](@entry_id:151029)**（单位：$\mathrm{W} \cdot \mathrm{m}^{-2} \cdot \mathrm{K}^{-1}$），$T_\infty$ 是环境温度。

这些方程和条件共同构成了[瞬态热传导](@entry_id:170260)问题的完整数学模型（即 **强形式**）。

### 空间[半离散化](@entry_id:163562)：从[偏微分方程](@entry_id:141332)到[常微分方程组](@entry_id:266774)

直接[求解偏微分方程](@entry_id:138485)通常是困难的。有限元方法的核心思想是先将其在空间上进行离散，得到一个关于时间的常微分方程 (ODE) 系统，这个过程称为 **[半离散化](@entry_id:163562) (semi-discretization)**。

#### 弱形式的推导

[半离散化](@entry_id:163562)的第一步是建立问题的 **弱形式 (weak form)**。我们将强形式的 PDE 乘以一个任意的、满足一定光滑性的 **[检验函数](@entry_id:166589) (test function)** $v$，然后在整个计算域 $\Omega$ 上积分：

$$
\int_{\Omega} v \left( \rho c \frac{\partial T}{\partial t} - \nabla \cdot (k \nabla T) \right) d\Omega = \int_{\Omega} v q \, d\Omega
$$

利用分部积分（即[高斯散度定理](@entry_id:188065)的推论）处理包含[二阶导数](@entry_id:144508)的[扩散](@entry_id:141445)项：

$$
- \int_{\Omega} v \nabla \cdot (k \nabla T) \, d\Omega = \int_{\Omega} \nabla v \cdot (k \nabla T) \, d\Omega - \oint_{\partial \Omega} v (k \nabla T \cdot \mathbf{n}) \, dS
$$

将此式代回原积分方程，得到：

$$
\int_{\Omega} \rho c v \frac{\partial T}{\partial t} \, d\Omega + \int_{\Omega} k \nabla v \cdot \nabla T \, d\Omega = \int_{\Omega} v q \, d\Omega + \oint_{\partial \Omega} v (k \nabla T \cdot \mathbf{n}) \, dS
$$

[弱形式](@entry_id:142897)的巧妙之处在于它降低了对解的[光滑性](@entry_id:634843)要求（从二阶可导降为一阶可导），并且边界积分项 $\oint_{\partial \Omega} v (k \nabla T \cdot \mathbf{n}) \, dS$ 提供了一个自然的方式来施加诺伊曼和[罗宾边界条件](@entry_id:163914)。对于诺伊曼边界 $\Gamma_N$，我们用指定的通量 $\overline{q}_n$ 替换 $-k \nabla T \cdot \mathbf{n}$；对于罗宾边界 $\Gamma_R$，我们用 $h(T - T_\infty)$ 替换 $-k \nabla T \cdot \mathbf{n}$ [@problem_id:2607762]。

以[罗宾边界条件](@entry_id:163914)为例，代入后边界积分项变为：

$$
\oint_{\partial \Omega} v (k \nabla T \cdot \mathbf{n}) \, dS = \dots - \int_{\Gamma_R} v h (T-T_\infty) \, dS
$$

将弱形式方程整理，把所有包含未知温度 $T$ 的项放在左边，已知项放在右边，得到：

$$
\underbrace{\int_{\Omega} \rho c v \frac{\partial T}{\partial t} d\Omega}_{\text{瞬态项}} + \underbrace{\int_{\Omega} k \nabla v \cdot \nabla T d\Omega}_{\text{扩散项}} + \underbrace{\int_{\Gamma_R} v h T dS}_{\text{罗宾边界刚度项}} = \underbrace{\int_{\Omega} v q d\Omega}_{\text{体积热源项}} + \underbrace{\int_{\Gamma_R} v h T_\infty dS}_{\text{罗宾边界载荷项}} + \dots
$$

#### [伽辽金法](@entry_id:749698)与[半离散系统](@entry_id:754680)

接下来，我们采用 **[伽辽金法](@entry_id:749698) (Galerkin method)**。我们将未知温度场 $T(\mathbf{x}, t)$ 近似为一系列已知 **[基函数](@entry_id:170178)** (或形函数) $N_j(\mathbf{x})$ 的线性组合，其系数为随时间变化的未知节点温度 $U_j(t)$：

$$
T(\mathbf{x}, t) \approx T_h(\mathbf{x}, t) = \sum_{j} U_j(t) N_j(\mathbf{x})
$$

[伽辽金法](@entry_id:749698)的核心是选择与[基函数](@entry_id:170178)相同的函数空间作为检验函数，即取 $v = N_i(\mathbf{x})$。将此近似代入弱形式，并对每一个[基函数](@entry_id:170178) $N_i$ 应用该方程，我们得到一个耦合的[常微分方程组](@entry_id:266774) [@problem_id:2607731]：

$$
\mathbf{M} \frac{d\mathbf{U}(t)}{dt} + \mathbf{K} \mathbf{U}(t) = \mathbf{F}(t)
$$

其中 $\mathbf{U}(t)$ 是所有未知节点温度组成的列向量。这个[方程组](@entry_id:193238)就是[半离散系统](@entry_id:754680)，其中：

*   **质量矩阵 (Mass Matrix)** $\mathbf{M}$，其元素为 $M_{ij} = \int_{\Omega} \rho c N_i N_j d\Omega$。它反映了系统的热容，即存储热能的能力。因为 $N_i N_j$ 项的存在，这个矩阵通常是非对角的，称为 **[一致质量矩阵](@entry_id:174630) (consistent mass matrix)**。

*   **刚度矩阵 (Stiffness Matrix)** $\mathbf{K}$，其元素为 $K_{ij} = \int_{\Omega} k \nabla N_i \cdot \nabla N_j d\Omega + \int_{\Gamma_R} h N_i N_j dS$。它由两部分组成：一部分来自域内的热传导，另一部分（如果存在）来自罗宾边界上的[对流换热](@entry_id:151349) [@problem_id:2607762]。该矩阵反映了系统内热量传递的难易程度。

*   **[载荷向量](@entry_id:635284) (Load Vector)** $\mathbf{F}$，其元素为 $F_i = \int_{\Omega} q N_i d\Omega - \int_{\Gamma_N} \overline{q}_n N_i dS + \int_{\Gamma_R} h T_\infty N_i dS$。它汇集了所有外部热作用，包括体积热源、指定的边界热通量和来自[对流](@entry_id:141806)环境的热量。

至此，我们成功地将一个复杂的时空[偏微分方程](@entry_id:141332)转化为了一个结构清晰的[线性常微分方程组](@entry_id:163837)。下一步是求解这个 ODE 系统。

### [时间离散化](@entry_id:169380)：从常微分方程到[代数方程](@entry_id:272665)

[半离散系统](@entry_id:754680) $\mathbf{M} \dot{\mathbf{U}} + \mathbf{K} \mathbf{U} = \mathbf{F}$ 仍然是连续时间的。为了在计算机上求解，我们必须在时间维度上进行离散化，将其转化为一系列代数方程。

#### $\theta$-方法

一个通用且强大的[时间积分方法](@entry_id:136323)族是 **$\theta$-方法**。该方法通过在时间步 $[t^n, t^{n+1}]$ 内的某个加权平均点 $t^{n+\theta} = t^n + \theta \Delta t$ 处来近似常微分方程，其中 $\Delta t = t^{n+1} - t^n$ 是时间步长，$\theta \in [0, 1]$ 是加权因子 [@problem_id:2607781]。

我们将时间导数 $\dot{\mathbf{U}}$ 用[一阶差分](@entry_id:275675)近似：$\dot{\mathbf{U}} \approx (\mathbf{U}^{n+1} - \mathbf{U}^n) / \Delta t$。而其他项则通过 $\theta$ 加权平均来近似：

$$
\mathbf{M} \frac{\mathbf{U}^{n+1} - \mathbf{U}^n}{\Delta t} + \mathbf{K} \left( \theta \mathbf{U}^{n+1} + (1-\theta) \mathbf{U}^n \right) = \theta \mathbf{F}^{n+1} + (1-\theta) \mathbf{F}^n
$$

其中 $\mathbf{U}^n$ 是在 $t^n$ 时刻的节点温度向量。整理此方程，将未知的 $\mathbf{U}^{n+1}$ 移到左侧，已知的 $\mathbf{U}^n$ 和载荷项移到右侧，我们得到在每个时间步需要求解的线性代数方程组：

$$
(\mathbf{M} + \theta \Delta t \mathbf{K}) \mathbf{U}^{n+1} = (\mathbf{M} - (1-\theta) \Delta t \mathbf{K}) \mathbf{U}^{n} + \Delta t \left( \theta \mathbf{F}^{n+1} + (1-\theta) \mathbf{F}^n \right)
$$

这个方程给出了从已知时刻 $t^n$ 的解 $\mathbf{U}^n$ 计算下一时刻 $t^{n+1}$ 的解 $\mathbf{U}^{n+1}$ 的更新规则 [@problem_id:2607787]。

通过选择不同的 $\theta$ 值，我们可以得到几种经典的[时间积分](@entry_id:267413)方案：

*   **[前向欧拉法](@entry_id:141238) (Forward Euler, $\theta=0$)**：这是一个 **显式** 方法，因为左侧的矩阵仅为 $\mathbf{M}$，$\mathbf{U}^{n+1}$ 无需解方程即可直接计算。但它的稳定性较差。
*   **[后向欧拉法](@entry_id:139674) (Backward Euler, $\theta=1$)**：这是一个 **隐式** 方法，每一步都需要求解一个线性方程组。它的优点是具有非常好的稳定性。例如，在一个一维杆的瞬态冷却问题中，我们可以组装矩阵 $\mathbf{M}$ 和 $\mathbf{K}$，然后通过[求解线性系统](@entry_id:146035) $(\mathbf{M} + \Delta t \mathbf{K})\mathbf{U}^1 = \mathbf{M} \mathbf{U}^0 + \Delta t \mathbf{F}^1$ 来计算第一个时间步后的温度[分布](@entry_id:182848) [@problem_id:2607731] [@problem_id:2607748]。
*   **Crank-Nicolson 法 ($\theta=0.5$)**：这也是一个隐式方法，通常被认为在时间和空间上具有平衡的精度（[二阶精度](@entry_id:137876)），因此在许多应用中非常受欢迎。

### 时间积分的稳定性分析

选择[时间积分](@entry_id:267413)方案时，一个至关重要的考量是其 **稳定性**。一个不稳定的数值方案可能会导致计算结果出现无界的、非物理的[振荡](@entry_id:267781)，最终使求解失败。

#### [模态分析](@entry_id:163921)与[放大因子](@entry_id:144315)

为了分析稳定性，我们考察无外力情况下的系统 $\mathbf{M} \dot{\mathbf{U}} + \mathbf{K} \mathbf{U} = \mathbf{0}$。该系统的解可以分解为一系列 **模态** 的叠加。每个模态对应于[广义特征值问题](@entry_id:151614) $\mathbf{K} \boldsymbol{\phi} = \mu \mathbf{M} \boldsymbol{\phi}$ 的一个[特征向量](@entry_id:151813) $\boldsymbol{\phi}$ 和[特征值](@entry_id:154894) $\mu \ge 0$。对于[热传导](@entry_id:147831)问题，这些[特征值](@entry_id:154894) $\mu$ 都是实数且非负的。在这些[模态基](@entry_id:752055)下，复杂的耦合系统可以[解耦](@entry_id:637294)为一系列独立的标量方程 $\dot{a}(t) = -\mu a(t)$，其中 $a(t)$ 是模态振幅 [@problem_id:2607787] [@problem_id:2607756]。

将 $\theta$-方法应用于这个标量方程，我们可以推导出单步的模态振幅变化关系 $a^{n+1} = g(\mu, \Delta t, \theta) a^n$。其中 $g$ 被称为 **放大因子 (amplification factor)**：

$$
g(z) = \frac{1 - (1-\theta)z}{1 + \theta z}, \quad \text{其中 } z = \mu \Delta t \ge 0
$$

为了保证数值解的稳定性，要求在任何情况下[放大因子](@entry_id:144315)的[绝对值](@entry_id:147688)都不超过 1，即 $|g(z)| \le 1$。违反此条件意味着该模态的振幅会随时间步的推进而被放大，导致不稳定。

#### [A-稳定性与L-稳定性](@entry_id:746183)

在更广泛的[数值分析](@entry_id:142637)理论中，稳定性通常通过 **[A-稳定性](@entry_id:144367) (A-stability)** 来衡量。一个方法是 A-稳定的，如果当它应用于稳定的标量测试方程 $\dot{y} = \lambda y$（其中 $\mathrm{Re}(\lambda) \le 0$）时，对于任意时间步长 $\Delta t > 0$，其数值解都不会增长 [@problem_id:2607756]。对于[热传导](@entry_id:147831)问题，由于系统[特征值](@entry_id:154894) $\lambda = -\mu$ 是实数且非正，[A-稳定性](@entry_id:144367)保证了无条件的稳定性。

通过分析[放大因子](@entry_id:144315)，可以证明当且仅当 $\theta \ge 0.5$ 时，$\theta$-方法是 A-稳定的 [@problem_id:2607795]。这意味着：

*   **[前向欧拉法](@entry_id:141238) ($\theta=0$)** 是 **条件稳定** 的。它只有在时间步长 $\Delta t$ 小于某个临界值（通常与空间网格尺寸的平方成正比）时才稳定。这对于精细网格来说是一个非常苛刻的限制。
*   **[后向欧拉法](@entry_id:139674) ($\theta=1$)** 和 **Crank-Nicolson 法 ($\theta=0.5$)** 都是 **A-稳定** 的，因此对于任意大的时间步长，数值解都不会发散。这使得它们在处理所谓的 **刚性 (stiff)** 问题（即系统中包含衰减速率差异巨大的模态）时特别有价值。

然而，[A-稳定性](@entry_id:144367)并不能完全描述数值解的质量。一个更强的性质是 **[L-稳定性](@entry_id:143644) (L-stability)**。一个方法是 L-稳定的，如果它是 A-稳定的，并且当 $z \to \infty$ 时（对应于衰减极快的“高频”或“刚性”模态），其[放大因子](@entry_id:144315)趋于零，即 $\lim_{z \to \infty} |g(z)| = 0$ [@problem_id:2607756]。

*   **[后向欧拉法](@entry_id:139674) ($\theta=1$)** 的放大因子为 $g(z) = 1/(1+z)$。当 $z \to \infty$ 时，$g(z) \to 0$。因此，它是 **L-稳定** 的。这表明后向欧拉法具有很强的 **数值耗散 (numerical diffusion)**，能够迅速衰减掉那些由[空间离散化](@entry_id:172158)引入的、物理意义不大但可能污染解的高频模态 [@problem_id:2607734]。

*   **Crank-Nicolson 法 ($\theta=0.5$)** 的放大因子为 $g(z) = (1-z/2)/(1+z/2)$。当 $z \to \infty$ 时，$g(z) \to -1$ [@problem_id:2607735]。因此，它 **不是 L-稳定** 的。这意味着，尽管高频模态的振幅不会被放大（[A-稳定性](@entry_id:144367)），但它们也不会被有效衰减，而是在每个时间步都以接近-1的因子进行缩放，表现为持续的、符号交替的 **非物理[振荡](@entry_id:267781)**。在求解包含突变或不光滑初始条件的[刚性问题](@entry_id:142143)时，这种[振荡](@entry_id:267781)尤为明显。

### 解的定性性质：[离散最大值原理](@entry_id:748510)

除了稳定性和精度，数值解是否能保持原物理问题的一些重要定性特征也值得关注。[热传导](@entry_id:147831)过程的一个基本物理特性是 **[最大值原理](@entry_id:138611) (maximum principle)**，即在没有热源的情况下，物体内部的温度极值只会出现在初始时刻或在边界上。

然而，标准的有限元方法并不能自动保证其数值解也满足类似的 **[离散最大值原理](@entry_id:748510) (Discrete Maximum Principle, DMP)**。研究表明，[半离散系统](@entry_id:754680) $\dot{\mathbf{U}} = -\mathbf{M}^{-1}\mathbf{K} \mathbf{U}$ 满足 DMP 的一个充分条件是系统矩阵 $-\mathbf{M}^{-1}\mathbf{K}$ 是一个 **梅茨勒矩阵 (Metzler matrix)**，即其所有非对角元素都为非负数 [@problem_id:2507754]。

要满足这一条件，通常需要两个方面的配合：

1.  **网格几何**：[刚度矩阵](@entry_id:178659) $\mathbf{K}$ 的非对角元素 $K_{ij}$ ($i \neq j$) 必须全部为非正数（这样的矩阵称为 Z-矩阵）。对于线性三角形或[四面体单元](@entry_id:168311)，这通常要求网格是 **非钝角** 的（例如，在二维中所有三角形的内角均不大于 $90^\circ$），或者满足一个稍弱的 **德劳内 (Delaunay)** 条件。如果网格中存在钝角过大的单元，可能会导致某些非对角 $K_{ij}$ 为正，从而破坏条件。

2.  **质量矩阵形式**：[质量矩阵](@entry_id:177093) $\mathbf{M}$ 必须是 **对角的 (diagonal)**。通过 **[质量集中](@entry_id:175432) (mass lumping)** 技术，可以将[一致质量矩阵](@entry_id:174630)近似为一个[对角矩阵](@entry_id:637782)，其[逆矩阵](@entry_id:140380)也是对角且正定的。如果使用[一致质量矩阵](@entry_id:174630)，其[逆矩阵](@entry_id:140380) $\mathbf{M}^{-1}$ 通常是满阵，导致 $-\mathbf{M}^{-1}\mathbf{K}$ 的非对角元素符号不定，从而破坏 DMP。

因此，为了获得满足[最大值原理](@entry_id:138611)的数值解，往往需要在精度（[一致质量矩阵](@entry_id:174630)通常更精确）和解的定性行为（[质量集中](@entry_id:175432)有助于满足 DMP）之间做出权衡。

综上所述，从建立物理模型到[空间离散化](@entry_id:172158)，再到时间积分及其[稳定性分析](@entry_id:144077)，我们已经构建了求解[瞬态热扩散](@entry_id:176511)问题的完整有限元框架。在后续章节中，我们将把这些原理应用于具体的工程问题中。