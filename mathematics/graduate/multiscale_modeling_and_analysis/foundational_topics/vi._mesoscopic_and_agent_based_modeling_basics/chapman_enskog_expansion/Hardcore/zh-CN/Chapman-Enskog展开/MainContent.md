## 引言
在多尺度物理学的广阔图景中，一个核心且持久的挑战是如何在描述单个粒子行为的微观定律与描述物质宏观集体行为的连续介质模型之间建立一座严谨的桥梁。气体动理论正是应对这一挑战的理论前沿，它试图回答：我们日常经验中熟悉的流体黏性、热传导等现象，其微观起源究竟是什么？为何纳维-斯托克斯方程能够如此成功地描述空气和水的流动？查普曼-恩斯科格（Chapman-Enskog, CE）展开正是为回答这些问题而生，它提供了一个强大而系统的数学框架，解决了从统计力学的玻尔兹曼方程推导宏观流体动力学方程这一关键的知识鸿沟。

本文旨在深入剖析查普曼-恩斯科格展开的理论精髓与应用价值。读者将通过三个层次的学习，逐步掌握这一跨尺度分析的核心工具。首先，在“原理与机制”一章中，我们将奠定理论基础，从玻尔兹曼方程的物理假设出发，阐明局部平衡态与克努森数的概念，并详细拆解CE展开的独特程序，见证欧拉方程与纳维-斯托克斯方程如何从中自然浮现。接着，在“应用与跨学科联系”一章中，我们将展示该理论的强大威力，探索如何利用它从第一性原理计算黏度、热导率等输运系数，并将其应用扩展至微流控、等离子体物理和非平衡态热力学等前沿领域。最后，通过“动手实践”部分提供的精选问题，读者将有机会亲手应用所学知识，解决具体的理论推导问题，从而巩固和深化理解。本文将引导您开启一段从微观碰撞到宏观流动的智识之旅。

## 原理与机制

在“引言”部分，我们已经概述了从微观的粒子动力学推导宏观连续介质模型的挑战与意义。本章将深入探讨实现这一跨尺度联系的核心工具——Chapman-Enskog (CE) 展开。我们将系统地阐述其基本原理、数学构造和物理内涵，揭示它如何从描述单个粒子行为的玻尔兹曼方程中，严谨地导出描述流体运动的纳维-斯托克斯-傅里叶（Navier-Stokes-Fourier, NSF）方程。

### 气体动力学理论的基石：玻尔兹曼方程

Chapman-Enskog展开的出发点是**玻尔兹曼方程**，它是描述稀薄气体中单粒子分布函数 $f(\boldsymbol{x}, \boldsymbol{v}, t)$ 演化的基本动力学方程。分布函数 $f$ 定量地描述了在时间 $t$、空间位置 $\boldsymbol{x}$ 附近，速度处于 $\boldsymbol{v}$ 附近的单位相空间体积内的粒子数。玻尔兹曼方程的一般形式为：
$$
\frac{\partial f}{\partial t} + \boldsymbol{v} \cdot \nabla_{\boldsymbol{x}} f + \boldsymbol{a} \cdot \nabla_{\boldsymbol{v}} f = Q(f, f)
$$
方程左边描述了粒子在相空间中的“流（streaming）”：第一项是时间演化，第二项是空间迁移（自由飞行），第三项是外力加速度 $\boldsymbol{a} = \boldsymbol{F}/m$ 引起的相空间漂移。方程右边的 $Q(f, f)$ 是**碰撞算符**，描述了粒子间碰撞对分布函数的改变。

玻尔兹曼方程并非一个基本物理原理，而是从牛顿力学和统计假设推导出的模型。其推导依赖于几个关键的物理假设，这些假设界定了其适用范围 [@problem_id:3742332]。首先，它适用于**稀薄气体**，即粒子自身的体积远小于气体占据的总体积，粒子间的平均距离远大于其相互作用的力程。其次，它基于**二体碰撞**假设，认为在稀薄气体中，三个或更多粒子同时发生碰撞的概率可以忽略不计。最后，也是最核心的统计假设，是**分子混沌（Molecular Chaos）**或称**Stosszahlansatz**。该假设认为，在任何一次碰撞发生前，两个参与碰撞的粒子的速度是完全不相关的。这使得我们可以将描述两个粒子联合分布的二体分布函数 $f^{(2)}$ 近似为两个单粒子分布函数 $f$ 的乘积，即 $f^{(2)} \approx f \cdot f$，从而封闭了从刘维尔方程（Liouville equation）经过BBGKY（Bogoliubov–Born–Green–Kirkwood–Yvon）层级推导出的动力学方程。

正是这些假设，使得复杂的N体问题被简化为一个关于单粒子分布函数的、非线性的积微分方程。碰撞算符 $Q(f, f)$ 具有几个至关重要的性质：
1.  它是 $f$ 的双线性积分算符。
2.  它在空间和时间上是局域的。
3.  它确保了在每次碰撞中**质量、动量和能量**这三个**碰撞不变量**的守恒。这意味着，对于任意函数 $\psi(\boldsymbol{v})$，当且仅当 $\psi$ 是这三个不变量（$m$, $m\boldsymbol{v}$, $\frac{1}{2}m|\boldsymbol{v}|^2$）的线性组合时，积分 $\int \psi(\boldsymbol{v}) Q(f, f) d\boldsymbol{v} = 0$ 成立。
4.  它满足玻尔兹曼的**H-定理**，即 $\int \ln(f) Q(f, f) d\boldsymbol{v} \le 0$，这保证了系统熵的增加和向平衡态的演化。等号成立的唯一条件是 $f$ 处于平衡态。

### 从微观到宏观：流体动力学场与平衡态

流体动力学关心的是宏观物理量，如密度、速度和温度。这些量可以从微观的分布函数 $f$ 通过取速度矩得到 [@problem_id:3742350]。对于一个单原子气体，我们定义：

-   **数密度 $n(\boldsymbol{x}, t)$**：单位体积内的粒子数，通过对 $f$ 在整个速度空间积分得到。
    $$
    n(\boldsymbol{x}, t) = \int_{\mathbb{R}^3} f(\boldsymbol{x}, \boldsymbol{v}, t) \, d\boldsymbol{v}
    $$

-   **流体速度 $\boldsymbol{u}(\boldsymbol{x}, t)$**：粒子的平均速度，即粒子动量密度的平均值。
    $$
    \boldsymbol{u}(\boldsymbol{x}, t) = \frac{1}{n} \int_{\mathbb{R}^3} \boldsymbol{v} f(\boldsymbol{x}, \boldsymbol{v}, t) \, d\boldsymbol{v}
    $$

-   **温度 $T(\boldsymbol{x}, t)$**：与粒子相对于平均速度的随机运动（即**奇特速度** $\boldsymbol{c} = \boldsymbol{v} - \boldsymbol{u}$）的平均动能相关。根据能量均分定理，对于单原子气体，单位体积的内能（随机动能）为 $\frac{3}{2} n k_B T$。因此，温度的定义为：
    $$
    \frac{3}{2} n k_B T(\boldsymbol{x}, t) = \int_{\mathbb{R}^3} \frac{1}{2} m |\boldsymbol{v} - \boldsymbol{u}|^2 f(\boldsymbol{x}, \boldsymbol{v}, t) \, d\boldsymbol{v}
    $$
    整理后得到：
    $$
    T(\boldsymbol{x}, t) = \frac{m}{3 n k_B} \int_{\mathbb{R}^3} |\boldsymbol{v} - \boldsymbol{u}|^2 f(\boldsymbol{x}, \boldsymbol{v}, t) \, d\boldsymbol{v}
    $$
    其中 $m$ 是粒子质量，$k_B$ 是玻尔兹曼常数。有时也使用比气体常数 $R = k_B/m$ 来表达。

这些宏观场是Chapman-Enskog展开的核心，因为该方法旨在推导出这些场自身的演化方程。

接下来，我们需要区分两种平衡态 [@problem_id:3742358]。当一个孤立系统达到**全局热力学平衡**时，其宏观性质在空间上均匀且不随时间变化。此时，流体速度 $\boldsymbol{u}$ 和温度 $T$ 均为常数，密度 $n$ 也为常数。在这种状态下，不仅碰撞算符为零（$Q(f,f)=0$），流项也因梯度为零而消失（$\partial_t f + \boldsymbol{v} \cdot \nabla_{\boldsymbol{x}} f = 0$）。此时的分布函数是全局的**麦克斯韦分布**。

然而，在大多数实际流动问题中，系统并未达到全局平衡，但可能处于一种更普遍的状态，即**局部热力学平衡（Local Thermodynamic Equilibrium, LTE）**。在这种状态下，宏观场 $n, \boldsymbol{u}, T$ 随空间和时间缓慢变化。在任何一个时空点 $(\boldsymbol{x}, t)$，我们可以认为气体在一个极小的邻域内近似处于平衡。这意味着在该点，分布函数 $f$ 可以很好地由一个**局域麦克斯韦分布** $\mathcal{M}[n, \boldsymbol{u}, T]$ 来描述：
$$
\mathcal{M}[n, \boldsymbol{u}, T](\boldsymbol{v}) = n \left( \frac{m}{2\pi k_B T} \right)^{3/2} \exp\left( - \frac{m|\boldsymbol{v}-\boldsymbol{u}|^2}{2 k_B T} \right)
$$
这个分布的参数 $n, \boldsymbol{u}, T$ 是空间和时间的函数。由于局域麦克斯韦分布是碰撞算符的零点，即 $Q(\mathcal{M}, \mathcal{M}) = 0$，因此在LTE状态下，即使存在宏观梯度（$\nabla n, \nabla \boldsymbol{u}, \nabla T \neq 0$），碰撞算符在主导阶上仍然为零。正是这些梯度，通过玻尔兹曼方程的流项，驱动系统偏离LTE，从而产生耗散效应，如黏性和热传导。Chapman-Enskog展开正是围绕着这种偏离LTE的小扰动进行的。

### Chapman-Enskog展开的理论依据：流体动力学区

Chapman-Enskog展开并非在所有情况下都有效。它的有效性取决于一个关键的无量纲参数——**克努森数 (Knudsen number)** $Kn$。克努森数定义为分子的平均自由程 $\lambda$ 与系统宏观特征长度 $L$ 的比值：
$$
Kn = \frac{\lambda}{L}
$$
$\lambda$ 代表了分子在连续两次碰撞之间平均飞行的距离，是微观尺度；$L$ 代表了宏观物理量（如温度、速度）发生显著变化的典型长度，是宏观尺度。因此，$Kn$ 数衡量了系统的尺度分离程度。

我们可以根据 $Kn$ 数的大小划分不同的流动区域 [@problem_id:3742337]：
-   **连续流区/流体动力学区 ($Kn \lesssim 10^{-3}$)**：此时，分子的平均自由程远小于宏观尺度，粒子碰撞极其频繁。这使得气体行为可以被连续介质模型（如NSF方程）精确描述。
-   **滑移流区 ($10^{-3} \lesssim Kn \lesssim 10^{-1}$)**：当 $Kn$ 数稍大时，气体主体行为仍可用连续介质模型描述，但在边界附近，气体分子与壁面的相互作用变得重要，导致速度滑移和温度跳跃现象。
-   **过渡流区 ($10^{-1} \lesssim Kn \lesssim 10$)**：在此区域，碰撞频率与粒子穿越系统的频率相当，连续介质假设完全失效，必须直接求解玻尔兹曼方程或使用粒子模拟方法（如DSMC）。
-   **自由分子流区 ($Kn \gtrsim 10$)**：粒子间的碰撞变得极为稀少，主要与边界发生碰撞。此时可以忽略玻尔兹曼方程中的碰撞项。

Chapman-Enskog展开正是在**流体动力学区**（即 $Kn \ll 1$）的极限下进行的**渐近展开**。为了看清这一点，我们可以对玻尔兹曼方程进行无量纲化。使用特征长度 $L$、特征速度（如热速度 $v_{th}$）和特征时间 $L/v_{th}$ 对变量进行缩放，玻尔兹曼方程可以写成如下形式：
$$
\frac{\partial f}{\partial t} + \boldsymbol{v} \cdot \nabla_{\boldsymbol{x}} f \sim \frac{1}{Kn} Q(f, f)
$$
在这个形式下，左边的流项是 $\mathcal{O}(1)$ 的，而右边的碰撞项是 $\mathcal{O}(1/Kn)$ 的。当 $Kn \to 0$ 时，碰撞项占据绝对主导地位。这强大的“碰撞力”会迅速将分布函数“推向”碰撞算符的零空间，即局域麦克斯韦分布。因此，将系统描述为对局域麦克斯韦分布的一个小偏离，并以 $Kn$ 作为小参数进行展开，就成了一种自然且数学上合理的选择。

例如，对于一个尺寸为 $L=1\,\mathrm{mm}$ 的微通道，在标准温压下，空气的平均自由程约为 $\lambda \approx 65\,\mathrm{nm}$。计算得到的克努森数为 $Kn = \frac{65 \times 10^{-9}\,\mathrm{m}}{10^{-3}\,\mathrm{m}} = 6.5 \times 10^{-5}$。这个数值远小于 $1$，明确地表明流动处于流体动力学区，Chapman-Enskog展开是描述该系统的有效理论工具 [@problem_id:3742337]。

### Chapman-Enskog方法的程序

Chapman-Enskog方法的核心是一种特殊的微扰展开方案，它巧妙地处理了时间和空间的多尺度特性。其基本假设被称为“**范式解（normal solution）**”假设 [@problem_id:3742345]：在经过短暂的初始瞬态（约几个碰撞时间）后，分布函数 $f$ 的所有时空依赖性都完全通过宏观流体动力学场 $(n, \boldsymbol{u}, T)$ 及其空间梯度来体现。换言之，$f$ 是这些宏观量的一个泛函：
$$
f(\boldsymbol{x}, \boldsymbol{v}, t) = \mathcal{F}(\boldsymbol{v}; n(\boldsymbol{x},t), \boldsymbol{u}(\boldsymbol{x},t), T(\boldsymbol{x},t), \nabla n, \nabla \boldsymbol{u}, \nabla T, \dots)
$$
这个“**奴役原理 (enslaving principle)**”意味着微观状态被宏观状态完全“控制”。这一假设与更为直接的**希尔伯特展开 (Hilbert expansion)** 形成对比。希尔伯特展开直接将 $f$ 展开为 $f = f^{(0)} + \epsilon f^{(1)} + \dots$，并分别求解各阶分布函数，导致宏观场本身也成为级数 $n = n^{(0)} + \epsilon n^{(1)} + \dots$，这在物理上和操作上都较为繁琐。

Chapman-Enskog方法通过以下步骤实施 [@problem_id:3742336] [@problem_id:3742372]：

1.  **展开分布函数和时间导数**：设小参数 $\epsilon \propto Kn$。我们将分布函数 $f$ 和时间导数算子 $\partial_t$ 同时展开为 $\epsilon$ 的幂级数：
    $$
    f = f^{(0)} + \epsilon f^{(1)} + \epsilon^2 f^{(2)} + \dots
    $$
    $$
    \frac{\partial}{\partial t} = \frac{\partial^{(0)}}{\partial t} + \epsilon \frac{\partial^{(1)}}{\partial t} + \epsilon^2 \frac{\partial^{(2)}}{\partial t} + \dots
    $$
    展开时间导数是CE方法的精髓，它体现了不同时间尺度上的动力学。$\partial^{(0)}/\partial t$ 描述最慢的、主导性的时间演化，而高阶项则描述更快的修正。

2.  **施加约束条件**：为了保证 $(n, \boldsymbol{u}, T)$ 是完整的宏观场，我们要求它们完全由零阶分布函数 $f^{(0)}$ 确定。这意味着所有高阶修正项 $f^{(k)}$ ($k \ge 1$) 对碰撞不变量的矩的贡献为零：
    $$
    \int \psi(\boldsymbol{v}) f^{(k)}(\boldsymbol{v}) \, d\boldsymbol{v} = 0, \quad \text{for } k \ge 1 \text{ and } \psi \in \{1, m\boldsymbol{v}, \frac{1}{2}m|\boldsymbol{v}|^2\}
    $$

3.  **代入玻尔兹曼方程并分离各阶**：将上述展开代入无量纲化的玻尔兹曼方程 $\epsilon(\partial_t f + \boldsymbol{v}\cdot\nabla f) = Q(f,f)$，并按 $\epsilon$ 的幂次逐级匹配，得到一个方程层级。

### 推导流体动力学方程：方程层级

通过上述程序，我们可以逐阶求解并推导出宏观方程。

#### 零阶近似：欧拉方程

在最低阶（$\epsilon^0$ 阶），我们得到：
$$
Q(f^{(0)}, f^{(0)}) = 0
$$
这表明 $f^{(0)}$ 必须是一个局域麦克斯韦分布 $\mathcal{M}[n, \boldsymbol{u}, T]$。根据约束条件，这里的 $(n, \boldsymbol{u}, T)$ 就是完整的宏观场。

在下一阶（$\epsilon^1$ 阶），方程的形式为：
$$
\left(\frac{\partial^{(0)}}{\partial t} + \boldsymbol{v} \cdot \nabla \right) f^{(0)} = L[f^{(1)}]
$$
其中 $L[g] = Q(f^{(0)}, g) + Q(g, f^{(0)})$ 是围绕 $f^{(0)}$ 的**线性化碰撞算符**。这是一个关于未知函数 $f^{(1)}$ 的线性积分方程。根据Fredholm择一定理，此方程有解的**可解性条件**是，其左边项必须与线性化算符 $L$ 的零空间正交。$L$ 的零空间由碰撞不变量张成。将方程左边对碰撞不变量 $\{m, m\boldsymbol{v}, \frac{1}{2}m|\boldsymbol{v}|^2\}$ 取矩并令其为零，我们恰好得到一组关于 $(n, \boldsymbol{u}, T)$ 的宏观守恒定律——**可压缩欧拉方程** [@problem_id:3742337] [@problem_id:3742336]。
$$
\begin{aligned}
\frac{\partial^{(0)} \rho}{\partial t} + \nabla \cdot (\rho \boldsymbol{u}) = 0 \\
\frac{\partial^{(0)} (\rho \boldsymbol{u})}{\partial t} + \nabla \cdot (\rho \boldsymbol{u} \otimes \boldsymbol{u} + p\boldsymbol{I}) = 0 \\
\frac{\partial^{(0)} E}{\partial t} + \nabla \cdot ((E+p)\boldsymbol{u}) = 0
\end{aligned}
$$
其中 $\rho=mn$ 是质量密度，$p=nk_BT$ 是压强，$E$ 是总能量密度。这组方程描述了无黏性、无热传导的理想流体。$\partial^{(0)}/\partial t$ 的作用因此被确定为由欧拉方程所描述的时间演化。

#### 一阶近似：纳维-斯托克斯-傅里叶方程

一旦可解性条件（欧拉方程）得到满足，我们就可以求解 $f^{(1)}$。$f^{(1)}$ 捕捉了分布函数对局部平衡的第一次偏离，它与宏观场的**一阶梯度**成线性关系。

为了清晰地展示结果，我们考虑一个简化的碰撞模型——**BGK（Bhatnagar-Gross-Krook）模型** [@problem_id:3742301]。在此模型下，$Q(f,f)$ 被替换为一个简单的弛豫项 $\frac{1}{\tau}(f^{\text{eq}}-f)$，其中 $\tau$ 是碰撞时间。在这种情况下，$f^{(1)}$ 的解可以直接写出：
$$
f^{(1)} = -\tau \left( \frac{\partial^{(0)}}{\partial t} + \boldsymbol{v} \cdot \nabla \right) f^{(0)}
$$
利用欧拉方程将 $\partial^{(0)}/\partial t$ 替换为空间梯度，可以得到 $f^{(1)}$ 是关于 $\nabla \boldsymbol{u}$ 和 $\nabla T$ 的线性函数。

接下来，我们计算由 $f = f^{(0)} + \epsilon f^{(1)}$ 产生的宏观通量，即**黏性应力张量** $\sigma_{ij}$ 和**热流矢量** $q_i$。
$$
\sigma_{ij} = \int m c_i c_j f \, d\boldsymbol{v} - p\delta_{ij} \approx \int m c_i c_j (\epsilon f^{(1)}) \, d\boldsymbol{v}
$$
$$
q_i = \int \frac{1}{2} m c^2 c_i f \, d\boldsymbol{v} \approx \int \frac{1}{2} m c^2 c_i (\epsilon f^{(1)}) \, d\boldsymbol{v}
$$
计算这些矩可以得到**本构关系**：
-   **牛顿黏性定律**：黏性应力与应变率张量成正比。
    $$
    \sigma_{ij} = -2\mu \left( \frac{1}{2}\left(\frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i}\right) - \frac{1}{3}(\nabla \cdot \boldsymbol{u})\delta_{ij} \right) - \zeta (\nabla \cdot \boldsymbol{u})\delta_{ij}
    $$
    其中 $\mu$ 是**剪切黏度**，$\zeta$ 是**体积黏度**。
-   **傅里叶热传导定律**：热流与温度梯度成正比。
    $$
    q_i = -\kappa \frac{\partial T}{\partial x_i}
    $$
    其中 $\kappa$ 是**热导率**。

Chapman-Enskog展开不仅给出了本构关系的形式，还从动力学理论出发，给出了输运系数 $\mu, \zeta, \kappa$ 的具体表达式。对于BGK模型，可以得到体积黏度 $\zeta=0$，并且普朗特数 $Pr = c_p \mu / \kappa = 1$ [@problem_id:3742301]。将这些本构关系代入宏观守恒律，我们就得到了**纳维-斯托克斯-傅里叶（NSF）方程**，这是描述真实流体（如水和空气）在大多数工程应用中行为的基石模型。

### 高阶修正、局限性与改进

Chapman-Enskog展开原则上可以继续进行下去。计算二阶修正 $f^{(2)}$ 的矩，会得到包含宏观场二阶梯度或一阶梯度乘积的项，这对应于**伯内特（Burnett）方程** [@problem_id:3742301]。

然而，这种“朴素的”高阶展开并非没有问题。一个严重的困难是，由标准CE方法推导出的伯内特方程在数学上是**不适定的（ill-posed）** [@problem_id:3742329]。对线性化的伯内特方程进行平面波稳定性分析会发现，其色散关系包含一个正的 $k^4$ 项（$k$ 是波数），这意味着短波（大 $k$）扰动会无限增长，导致解的崩溃。这表明CE展开是一个**渐近级数**，而非收敛级数，截取更多项并不总能提高精度，尤其是在描述高频或大梯度现象时。为了克服这一困难，研究者们提出了多种**正则化策略**，例如Bobylev提出的保留某些时间导数项以引入双曲性，或通过修改碰撞模型来抑制高阶矩的不稳定性。

CE展开的另一个根本局限性在于其无法处理**边界**附近的行为 [@problem_id:3742343]。在气体与固体壁面接触处，入射和反射的分子遵循不同的分布，导致总分布函数严重偏离任何单一的麦克斯韦分布。这种 $\mathcal{O}(1)$ 的偏离使得以 $f^{(0)}$ 为麦克斯韦分布的CE展开在边界处失效。

正确的处理方法是采用**匹配渐近展开**。在离壁面约一个平均自由程厚的薄层内，即**克努森层 (Knudsen layer)**，我们需要直接求解一个简化的玻尔兹曼方程，以捕捉剧烈的动力学变化。这个内层解必须满足真实的壁面动力学边界条件。然后，将这个内层解与远离壁面的“外层”CE解（即流体动力学解）进行匹配。匹配过程会对外层的流体动力学解施加约束，这些约束表现为有效的宏观边界条件，即**速度滑移**和**温度跳跃**。例如，流体在壁面处的速度并不等于壁面速度，其差值（滑移速度）正比于壁面处的剪切率。这些由动力学理论推导出的滑移/跳跃边界条件，是NSF方程在稀薄气体效应不可忽略时必须配备的。

### 与其他方法的比较

最后，值得将Chapman-Enskog方法与另一类重要的模型降阶方法——**矩方法 (Method of Moments)** 进行比较，其中最著名的是**Grad的13矩方法** [@problem_id:3742384]。

两种方法的哲学截然不同：
-   **CE展开**是一种**渐近方法**。它假设解的形式（范式解），并通过在小参数 $Kn$ 下的系统展开，将高阶矩（如应力、热流）表示为低阶矩（$n, \boldsymbol{u}, T$）及其空间梯度的函数。它最终得到一组关于少数几个宏观场的封闭方程（如NSF方程）。
-   **Grad的矩方法**是一种**截断方法**。它不进行渐近展开，而是直接假设分布函数 $f$ 本身可以由一个截断的埃尔米特多项式级数来近似。例如，在13矩方法中，$f$ 被近似为一个依赖于13个宏观矩（密度、速度、温度、应力张量、热流矢量）的函数。然后，通过对玻尔兹曼方程取这13个矩，得到一个关于这13个宏观变量的封闭的偏微分方程组。

这导致了它们在适用范围和性质上的差异：
-   CE展开（如NSF方程）是抛物型的，本质上是为近平衡、小 $Kn$ 数情况设计的。它无法捕捉到所有双曲效应（如有限速度传播）。
-   Grad的13矩方程是双曲型的，能够描述更偏离平衡的状态（中等 $Kn$ 数），并能正确预测某些高频现象（如声波在稀薄气体中的色散和衰减）。
-   在近平衡极限下（小 $Kn$），对Grad方程组进行CE展开，可以恢复NSF方程。对于麦克斯韦分子（一种特殊的相互作用模型），两种方法给出完全相同的输运系数。

总而言之，Chapman-Enskog展开是一个强大而深刻的理论框架，它不仅为宏观流体动力学方程提供了坚实的微观基础，也揭示了输运现象的物理本质。尽管存在局限性，但理解其原理、机制和适用边界，对于在多尺度建模中正确地选择和应用物理模型至关重要。