## 引言

在弯曲的空间中，“直线”是什么？这个看似简单的问题是黎曼几何学的核心。正如在地球表面上，最短的航线并非一条“笔直”的线，而是沿着地球[弧度](@entry_id:171693)的[大圆](@entry_id:268970)路径，我们需要一个普适的框架来描述任意[曲面](@entry_id:267450)或[流形](@entry_id:153038)上的“最直路径”。这个概念就是**[测地线](@entry_id:269969)**。然而，简单地将欧氏空间中直线加速度为零的条件 $\ddot{x}=0$ 直接搬到[流形](@entry_id:153038)上是行不通的，因为这个条件会随着[坐标系](@entry_id:156346)的选择而改变，缺乏内在的几何意义。

本文旨在解决这一根本问题，系统地阐述如何通过**协变加速度**这一强大工具，为[测地线](@entry_id:269969)建立一个严谨且坐标无关的定义。通过学习本文，读者将能够深刻理解[测地线](@entry_id:269969)作为“[协变](@entry_id:634097)加速度为零的曲线”的本质。我们将分三个章节展开：

- **第一章：原理与机制** 将深入探讨[协变导数](@entry_id:152476)和[克里斯托费尔符号](@entry_id:159831)的机制，从第一性原理推导出著名的[测地线方程](@entry_id:264349)，并阐明其几何与物理内涵。
- **第二章：应用与跨学科联系** 将展示[测地线](@entry_id:269969)概念的非凡力量，重点剖析其在广义相对论中如何重新定义[引力](@entry_id:175476)，并探索其在[理论化学](@entry_id:199050)和计算科学等前沿领域的应用。
- **第三章：动手实践** 将通过一系列精心设计的计算和编程问题，帮助读者将抽象的理论转化为具体的计算技能，加深对测地线方程和相关概念的理解。

让我们首先进入第一章，从重新思考“直”的定义开始，建立起描述弯曲空间中运动的语言。

## 原理与机制

在引言中，我们提出了在弯曲[流形](@entry_id:153038)上严谨定义“直线”的必要性。现在，我们将深入探讨[黎曼几何](@entry_id:160508)中最核心的概念之一：[测地线](@entry_id:269969)。直观上，[测地线](@entry_id:269969)是[欧氏空间](@entry_id:138052)中“直线”概念在弯曲空间中的推广。然而，要在弯曲的[流形](@entry_id:153038)上严谨地定义“最直的路径”，我们需要发展一套不依赖于特定[坐标系](@entry_id:156346)的语言。本章的目标是阐明[测地线](@entry_id:269969)作为[协变](@entry_id:634097)加速度为零的曲线的内在原理与机制。

### 从欧氏空间到[流形](@entry_id:153038)：对“直”的再思考

在[欧氏空间](@entry_id:138052) $\mathbb{R}^n$ 中，一条直线可以由一个参数 $t$ 线性地描述，例如 $\gamma(t) = p + tv$，其中 $p$ 和 $v$ 是常向量。在标准的[笛卡尔坐标系](@entry_id:169789) $\{x^i\}$ 中，这意味着曲线的每个坐标分量 $x^i(t)$ 都是 $t$ 的[仿射函数](@entry_id:635019)（即形如 $at+b$ 的线性函数）。其直接推论是，直线的[二阶导数](@entry_id:144508)恒为零：$\frac{d^2x^i}{dt^2} = 0$。

一个自然的想法是，我们能否将这个简单的条件 $\frac{d^2x^i}{dt^2} = 0$ 作为[流形](@entry_id:153038)上“直线”的定义？答案是否定的。原因在于，这个条件并非**坐标不变的(coordinate-invariant)**。一个在某个[坐标系](@entry_id:156346)下看起来是“直”的曲线，在另一个[坐标系](@entry_id:156346)下几乎肯定会变成“弯”的。

让我们通过一个思想实验来验证这一点 [@problem_id:2976961]。假设我们有一个[光滑流形](@entry_id:160799) $M$ 和一条曲线 $\gamma(t)$。在某个[局部坐标](@entry_id:181200)卡 $(U, x)$ 中，这条曲线满足 $\frac{d^2x^i}{dt^2}=0$。现在，我们切换到一个新的[坐标系](@entry_id:156346) $(V, y)$，其[坐标变换](@entry_id:172727)函数为 $y^\alpha = y^\alpha(x^1, \dots, x^n)$。根据[链式法则](@entry_id:190743)，新坐标下的速度分量为：
$$
\frac{dy^\alpha}{dt} = \sum_{i=1}^n \frac{\partial y^\alpha}{\partial x^i} \frac{dx^i}{dt}
$$

对时间 $t$ 再次求导，应用乘法法则和[链式法则](@entry_id:190743)，我们得到新坐标下的加速度分量：
$$
\frac{d^2 y^\alpha}{dt^2} = \sum_{i=1}^n \frac{\partial y^\alpha}{\partial x^i} \frac{d^2 x^i}{dt^2} + \sum_{i,j=1}^n \frac{\partial^2 y^\alpha}{\partial x^i \partial x^j} \frac{dx^i}{dt} \frac{dx^j}{dt}
$$
由于我们假设在 $x$ [坐标系](@entry_id:156346)下 $\frac{d^2x^i}{dt^2}=0$，上式简化为：
$$
\frac{d^2 y^\alpha}{dt^2} = \sum_{i,j=1}^n \frac{\partial^2 y^\alpha}{\partial x^i \partial x^j} \frac{dx^i}{dt} \frac{dx^j}{dt}
$$
这个结果表明，除非坐标变换是[仿射变换](@entry_id:144885)（即所有二阶偏导 $\frac{\partial^2 y^\alpha}{\partial x^i \partial x^j}$ 都为零），否则即使原始曲线在 $x$ [坐标系](@entry_id:156346)下是“直”的，它在 $y$ [坐标系](@entry_id:156346)下的[二阶导数](@entry_id:144508)通常也不为零 [@problem_id:2977055]。因此，$\frac{d^2x^i}{dt^2}=0$ 这个[条件依赖](@entry_id:267749)于[坐标系](@entry_id:156346)的选择，它描述的是坐标网格的性质，而非曲线本身的内在几何性质。要定义一个真正几何意义上的“直”路径，我们需要一个不依赖于[坐标系](@entry_id:156346)的加速度概念。

### [沿曲线的协变导数](@entry_id:192566)

微分几何通过引入**联络(connection)**和**[协变导数](@entry_id:152476)(covariant derivative)**来解决上述问题。一个联络 $\nabla$ 提供了一种在[流形](@entry_id:153038)上对向量场进行[微分](@entry_id:158718)的方法。给定两个向量场 $X, Y \in \mathfrak{X}(M)$，协变导数 $\nabla_X Y$ 描述了 $Y$ 沿 $X$ 方向的变化率，其结果仍然是一个向量场。

我们关心的是如何定义一个向量场**沿一条曲线**的变化率。设 $\gamma: [a,b] \to M$ 是一条光滑曲线，其切向量（或速度向量）为 $\dot{\gamma}(t) \in T_{\gamma(t)}M$。设 $V(t)$ 是一个沿 $\gamma$ 的光滑向量场，即对每个 $t \in [a,b]$，$V(t) \in T_{\gamma(t)}M$。我们无法直接计算 $\nabla_{\dot{\gamma}(t)}V(t)$，因为 $\nabla$ 的定义要求其第二个参数是一个在开集上定义的向量场，而 $V(t)$ 仅定义在曲线 $\gamma$ 上。

解决方法是，我们可以将 $V(t)$ **扩张(extend)** 成一个定义在 $\gamma$ 的某个邻域上的光滑向量场 $\widetilde{V}$，使得在曲线上 $\widetilde{V}(\gamma(t)) = V(t)$。然后，我们可以定义 $V$ 沿 $\gamma$ 的协变导数，记作 $\frac{D}{dt}V(t)$ 或 $\nabla_{\dot{\gamma}(t)}V$，为：
$$
\frac{D}{dt}V(t) := \nabla_{\dot{\gamma}(t)}\widetilde{V}
$$
这个定义的关键在于，其结果与扩张 $\widetilde{V}$ 的选择无关 [@problem_id:2976990]。如果 $\widehat{V}$ 是另一个扩张，那么差值向量场 $Z = \widetilde{V} - \widehat{V}$ 在曲线上恒为零。可以证明，$\nabla_{\dot{\gamma}(t)}Z$ 在曲线上也恒为零，从而保证了定义的良性。从更抽象的角度看，这个操作 $\frac{D}{dt}$ 实际上是在[拉回丛](@entry_id:159346) $\gamma^*(TM)$ 上定义了一个唯一的联络。

现在，我们在局部坐标系中推导[协变导数](@entry_id:152476)的表达式。设 $\gamma(t)$ 的坐标为 $x^i(t)$，[切向量](@entry_id:265494)为 $\dot{\gamma}(t) = \dot{x}^j(t) \partial_j|_{\gamma(t)}$。向量场 $V(t)$ 可以写成 $V(t) = V^k(t) \partial_k|_{\gamma(t)}$。利用协变导数的[莱布尼茨法则](@entry_id:157949)，我们有：
$$
\frac{D}{dt}V = \frac{D}{dt}(V^k \partial_k) = \frac{dV^k}{dt}\partial_k + V^k \frac{D}{dt}\partial_k
$$
其中 $\frac{D}{dt}\partial_k = \nabla_{\dot{\gamma}}\partial_k = \nabla_{\dot{x}^j\partial_j}\partial_k = \dot{x}^j \nabla_{\partial_j}\partial_k$。根据[联络系数](@entry_id:157618)（或称**[克里斯托费尔符号](@entry_id:159831)(Christoffel symbols)**）$\Gamma^i_{jk}$ 的定义 $\nabla_{\partial_j}\partial_k = \Gamma^i_{jk}\partial_i$，我们得到：
$$
\frac{D}{dt}V = \frac{dV^k}{dt}\partial_k + V^j \dot{x}^i \Gamma^k_{ij} \partial_k = \left( \frac{dV^k}{dt} + \Gamma^k_{ij} \dot{x}^i(t) V^j(t) \right) \partial_k
$$
因此，向量场 $V(t)$ 沿曲线 $\gamma(t)$ 的协变导数的第 $k$ 个分量是 [@problem_id:2976990]：
$$
\left(\frac{D}{dt}V\right)^k(t) = \frac{dV^k}{dt}(t) + \Gamma^k_{ij}(\gamma(t)) \dot{x}^i(t) V^j(t)
$$
这个表达式由两部分组成：第一项 $\frac{dV^k}{dt}$ 是向量分量自身的变化率，第二项 $\Gamma^k_{ij} \dot{x}^i V^j$ 是一个修正项，它说明了[坐标基](@entry_id:270149)矢 $\partial_j$ 本身是如何随着曲线的行进而变化的。正是这个修正项，确保了协变导数是一个真正的几何对象（即一个向量），其存在与[坐标系](@entry_id:156346)的选择无关。

### 协变加速度与[测地线](@entry_id:269969)的定义

有了[沿曲线的协变导数](@entry_id:192566)这一工具，我们便可以定义曲线的**[协变](@entry_id:634097)加速度(covariant acceleration)**。协变加速度就是曲线的切向量场 $\dot{\gamma}(t)$ 沿其自身方向的协变导数，即 $\nabla_{\dot{\gamma}}\dot{\gamma}$。

这个量精确地捕捉了曲线偏离“直线”的程度，且其定义是完全内在和坐标无关的。如果[协变](@entry_id:634097)加速度为零，我们便称这条曲线是一条**[测地线](@entry_id:269969)(geodesic)**。

**定义 ([测地线](@entry_id:269969)):** 一条光滑曲线 $\gamma(t)$ 被称为[测地线](@entry_id:269969)，如果它的[协变](@entry_id:634097)加速度处处为零，即：
$$
\nabla_{\dot{\gamma}(t)}\dot{\gamma}(t) = 0 \quad \text{for all } t
$$
这个条件有时也被称为**自平行(autoparallel)**，因为它意味着曲线的[切向量](@entry_id:265494)在沿曲线移动时保持“平行于自身”。这正是我们寻求的、对“最直路径”的严谨数学刻画 [@problem_id:2976990]。

### 测地线方程的坐标表示

我们可以利用[协变导数](@entry_id:152476)的坐标表达式来推导测地线方程的坐标形式。在[协变导数](@entry_id:152476)公式
$$
\left(\frac{D}{dt}V\right)^k = \frac{dV^k}{dt} + \Gamma^k_{ij} \dot{x}^i V^j
$$
中，令 $V = \dot{\gamma}$，这意味着 $V^j = \dot{x}^j$。于是 $\frac{dV^k}{dt} = \frac{d}{dt}(\dot{x}^k) = \ddot{x}^k$。代入后，我们得到协变加速度的分量：
$$
(\nabla_{\dot{\gamma}}\dot{\gamma})^k = \frac{d^2x^k}{dt^2} + \Gamma^k_{ij}(\gamma(t)) \dot{x}^i(t) \dot{x}^j(t)
$$
因此，[测地线](@entry_id:269969)条件 $\nabla_{\dot{\gamma}}\dot{\gamma}=0$ 等价于其在任意局部坐标系中的所有分量都为零。这就给出了著名的**测地线方程(geodesic equation)** [@problem_id:2977055]：
$$
\frac{d^2x^k}{dt^2} + \Gamma^k_{ij}(x) \frac{dx^i}{dt} \frac{dx^j}{dt} = 0 \quad \text{for } k=1, \dots, n
$$
这是一个关于[曲线坐标](@entry_id:178535)函数 $x^k(t)$ 的[二阶常微分方程](@entry_id:204212)组。给定一个初始点和初始方向（即一个初始[切向量](@entry_id:265494)），根据常微分方程的基本理论，存在唯一的[测地线](@entry_id:269969)。

### 理解[测地线方程](@entry_id:264349)

#### 方程的坐标不变性

一个深刻的问题是：[测地线方程](@entry_id:264349)中的克里斯托费尔符号 $\Gamma^k_{ij}$ 本身并不是一个张量，它在坐标变换下的变换法则相当复杂。那么，为何由它构成的测地线方程 $\nabla_{\dot\gamma}\dot\gamma=0$ 却是一个坐标无关的几何条件呢？[@problem_id:2977015]

答案在于一个精妙的抵消。我们之前看到，普通的[二阶导数](@entry_id:144508) $\ddot{x}^k$ 在[坐标变换](@entry_id:172727)下会产生一个非张量的项（含坐标变换的[二阶导数](@entry_id:144508)）。而[克里斯托费尔符号](@entry_id:159831)的变换法则中，也恰好包含一个类似的非齐次项。当我们将这两项组合成[协变](@entry_id:634097)加速度 $(\nabla_{\dot{\gamma}}\dot{\gamma})^k$ 时，这两个非张量的部分正好相互抵消了。

具体来说，可以证明[协变](@entry_id:634097)加速度的各个分量 $(A)^k = \ddot{x}^k + \Gamma^k_{ij}\dot{x}^i\dot{x}^j$ 在[坐标变换](@entry_id:172727) $x \to x'$ 下，其变换规律如同一个向量的分量：
$$
(A')^k = \sum_r \frac{\partial x'^k}{\partial x^r} (A)^r
$$
这意味着，如果[协变](@entry_id:634097)加速度在一个[坐标系](@entry_id:156346)中为零向量，那么它在任何其他[坐标系](@entry_id:156346)中也必然是[零向量](@entry_id:156189)。因此，条件 $\nabla_{\dot{\gamma}}\dot{\gamma}=0$ 是一个真正内在的、几何的陈述。

#### 联络的物理诠释：惯性力

测地线方程与[牛顿第二定律](@entry_id:274217) $F=ma$ 有着深刻的类比 [@problem_id:2977033]。我们可以将测地线方程改写为：
$$
m\frac{d^2x^k}{dt^2} = -m \Gamma^k_{ij} \frac{dx^i}{dt} \frac{dx^j}{dt}
$$
如果我们将左边的 $m\ddot{x}^k$ 视为“质量乘以[坐标加速度](@entry_id:264260)”，那么右边的项就扮演了“力”的角色。然而，[测地线](@entry_id:269969)描述的是在没有外力情况下的“自由”运动。因此，右边的项 $-m \Gamma^k_{ij} \dot{x}^i \dot{x}^j$ 不应被看作是真实的物理力，而应被理解为**[惯性力](@entry_id:169104)(inertial force)**或**虚拟力(fictitious force)**。

这与在经典力学中处理[非惯性参考系](@entry_id:169712)（如[旋转坐标系](@entry_id:170324)）时遇到的情况完全类似。在[旋转坐标系](@entry_id:170324)中，即使没有外力，物体也会因为[科里奥利力](@entry_id:160096)和离心力的作用而表现出加速度。这些力源于[坐标系](@entry_id:156346)本身的运动，而非物体间的相互作用。同样，在[流形](@entry_id:153038)上，$\Gamma$ 项代表的“力”源于两方面：一是所选[坐标系](@entry_id:156346)的“弯曲”（例如，即便在平直的[欧氏空间](@entry_id:138052)里，使用极坐标也会导致非零的 $\Gamma$），二是空间本身的内在曲率。

几何上更优雅的观点是，$\nabla_{\dot{\gamma}}\dot{\gamma}$ 才是物体“真实”的、内在的加速度。因此，对于[自由粒子](@entry_id:148748)，其运动方程就是“真实加速度为零”，即 $m \nabla_{\dot{\gamma}}\dot{\gamma} = 0$。

#### 联络与度量：[Levi-Civita联络](@entry_id:161107)

到目前为止，我们的讨论适用于任何给定的线性联络。然而，在[黎曼几何](@entry_id:160508)中，我们通常处理的是配备了黎曼度量 $g$ 的[流形](@entry_id:153038)。度量 $g$ 自然地引出了一种特殊的、唯一的联络，称为**Levi-Civita联络**。

**[黎曼几何基本定理](@entry_id:189185)**断言：在任意[黎曼流形](@entry_id:261160) $(M,g)$ 上，存在唯一一个线性联络 $\nabla$，它同时满足以下两个条件 [@problem_id:2976997]：
1.  **无挠(Torsion-free):** $\nabla_X Y - \nabla_Y X = [X,Y]$ 对所有向量场 $X,Y$ 成立。这意味着 $\Gamma^k_{ij} = \Gamma^k_{ji}$。
2.  **度量兼容(Metric-compatible):** $\nabla g = 0$。这意味着在对向量进行[协变微分](@entry_id:263981)时，它们之间的度量关系（如长度、角度）保持不变。

这个唯一确定的Levi-Civita联络的克里斯托费尔符号完全由度量张量 $g_{ij}$ 及其一阶导数决定。其显式表达式可以通过**[Koszul公式](@entry_id:181356)**推导得出：
$$
\Gamma^k_{ij} = \frac{1}{2} g^{k\ell} \left( \frac{\partial g_{j\ell}}{\partial x^i} + \frac{\partial g_{i\ell}}{\partial x^j} - \frac{\partial g_{ij}}{\partial x^\ell} \right)
$$
其中 $g^{k\ell}$ 是度量张量矩阵 $(g_{ij})$ 的[逆矩阵](@entry_id:140380)的元素。

值得注意的是，[测地线方程](@entry_id:264349) $\ddot{x}^k + \Gamma^k_{ij}\dot{x}^i\dot{x}^j=0$ 中的求和项 $\Gamma^k_{ij}\dot{x}^i\dot{x}^j$ 由于 $\dot{x}^i\dot{x}^j$ 对指标 $i,j$ 是对称的，所以只有 $\Gamma^k_{ij}$ 的对称部分会对此项有贡献。这意味着，即使一个联络有挠（即 $\Gamma^k_{ij} \neq \Gamma^k_{ji}$），其定义的[自平行曲线](@entry_id:269969)（[测地线](@entry_id:269969)）也仅依赖于其无挠部分。因此，研究[测地线](@entry_id:269969)时，通常可以直接假设联络是[无挠的](@entry_id:161664) [@problem_id:2977028]。

### 实例分析

#### [平直空间](@entry_id:204618)中的[测地线](@entry_id:269969)

让我们在一个最简单的情形下验证这些概念：三维[欧氏空间](@entry_id:138052) $\mathbb{R}^3$ 配备标准[笛卡尔坐标](@entry_id:167698) $(x^1, x^2, x^3)$ 和欧氏度量 [@problem_id:2976993]。在这种情况下，度量张量为常数矩阵 $g_{ij} = \delta_{ij}$（克罗内克符号）。

由于度量的所有分量都是常数，它们的偏导数处处为零。根据[克里斯托费尔符号](@entry_id:159831)的公式，我们立即得到：
$$
\Gamma^k_{ij} = \frac{1}{2} \sum_{\ell=1}^3 \delta^{k\ell} (0 + 0 - 0) = 0
$$
所有的[克里斯托费尔符号](@entry_id:159831)在笛卡尔坐标系下都为零。因此，测地线方程 $\ddot{x}^k + \Gamma^k_{ij}\dot{x}^i\dot{x}^j = 0$ 简化为：
$$
\frac{d^2x^k}{dt^2} = 0
$$
积分两次，我们得到 $x^k(t) = a^k t + b^k$，其中 $a^k, b^k$ 是常数。这正是欧氏空间中[直线的参数方程](@entry_id:172613)。这表明，我们抽象的[测地线](@entry_id:269969)定义，在[平直空间](@entry_id:204618)和特殊[坐标系](@entry_id:156346)下，完美地还原了我们对“直线”的朴素认知。此时，协变加速度 $\nabla_{\dot\gamma}\dot\gamma$ 就等于普通的[坐标加速度](@entry_id:264260) $\ddot\gamma$。

#### 曲空间上的加速度

现在考虑一个真正的弯曲空间：一个半径为 $R$ 的球面。我们来看一条非[测地线](@entry_id:269969)的曲线——一个纬线圈。设球面坐标为 $(\phi, \theta)$，其中 $\phi$ 是从北极点度量的极角，$\theta$ 是方位角。一条纬线由 $\phi = \phi_0$ (常数) 定义。假设一个漫游车以恒定的速率 $v$ 沿此纬线圈运动 [@problem_id:1656897]。

在球面度量 $ds^2 = R^2 d\phi^2 + R^2\sin^2\phi \, d\theta^2$ 下，可以计算出相关的非零克里斯托费尔符号，例如 $\Gamma^{\phi}_{\theta\theta} = -\sin\phi\cos\phi$。漫游车的路径为 $\phi(t) = \phi_0$, $\dot{\phi}=0$, $\ddot{\phi}=0$。其[角速度](@entry_id:192539) $\dot{\theta}$ 由速率 $v$ 决定。

计算其协变加速度 $\nabla_{\dot\gamma}\dot\gamma$ 的分量，我们发现 $\theta$ 分量为零，而 $\phi$ 分量不为零：
$$
(\nabla_{\dot\gamma}\dot\gamma)^\phi = \ddot{\phi} + \Gamma^\phi_{\theta\theta}\dot{\theta}^2 = 0 - \sin\phi_0\cos\phi_0 \, \dot{\theta}^2 \neq 0
$$
（除非 $\phi_0 = \pi/2$ 或 $\phi_0=0,\pi$）。这非零的[协变](@entry_id:634097)加速度指向极点或赤道的方向，它代表了为了维持在纬线圈上运动所必需的“转向”。其大小可以计算为：
$$
|\nabla_{\dot{\gamma}}\dot{\gamma}| = \frac{v^2}{R} |\cot\phi_0|
$$
这个结果告诉我们，除了赤道（$\phi_0 = \pi/2$，此时 $\cot\phi_0=0$）以外，所有的纬线圈都不是[测地线](@entry_id:269969)。赤道是一个大圆，而[球面上的测地线](@entry_id:275643)正是所有的[大圆](@entry_id:268970)。这个例子清晰地展示了[协变](@entry_id:634097)加速度如何量化一条路径偏离“最直”状态的程度。

### [测地线](@entry_id:269969)的性质：[参数化](@entry_id:272587)与速率

测地线方程的一个重要性质与其参数化方式紧密相关。满足方程 $\ddot{x}^k + \Gamma^k_{ij}\dot{x}^i\dot{x}^j = 0$ 的参数 $t$ 被称为**[仿射参数](@entry_id:260625)(affine parameter)**。

一个关键的结论是：对于一条以[仿射参数](@entry_id:260625) $t$ [参数化](@entry_id:272587)的[测地线](@entry_id:269969) $\gamma(t)$，其速率 $\| \dot{\gamma}(t) \| = \sqrt{g(\dot{\gamma}(t), \dot{\gamma}(t))}$ 是一个常数 [@problem_id:2977042]。这可以利用[度量兼容性](@entry_id:265910)[直接证明](@entry_id:141172)：
$$
\frac{d}{dt} g(\dot{\gamma}, \dot{\gamma}) = g(\nabla_{\dot{\gamma}}\dot{\gamma}, \dot{\gamma}) + g(\dot{\gamma}, \nabla_{\dot{\gamma}}\dot{\gamma}) = 2g(0, \dot{\gamma}) = 0
$$
既然速率的平方是常数，速率本身也是常数。

这个性质连接了[仿射参数](@entry_id:260625)和另一个重要的[参数化](@entry_id:272587)方式——**[弧长参数化](@entry_id:634139)(arc-length parametrization)**。[弧长](@entry_id:191173)参数 $s$ 定义为 $s(t) = \int_{t_0}^t \|\dot{\gamma}(u)\| du$。如果 $t$ 是一个[仿射参数](@entry_id:260625)，则 $\|\dot{\gamma}(u)\|$ 是一个常数，记为 $a$。于是：
$$
s(t) = a(t-t_0) = at + b
$$
其中 $b = -at_0$ 是常数。这表明，弧长 $s$ 和[仿射参数](@entry_id:260625) $t$ 之间是线性（仿射）关系。

反过来，如果两个参数 $t$ 和 $\tau$ 都是某条[测地线](@entry_id:269969)的[仿射参数](@entry_id:260625)，那么它们之间也必然是仿射关系，即 $t = A\tau + B$（$A, B$为常数，$A\neq 0$）[@problem_id:2977028]。[弧长参数化](@entry_id:634139)是[仿射参数](@entry_id:260625)化的一种特殊情况，即速率恒为1的情况。因此，我们可以说，[弧长](@entry_id:191173)参数是“单位速率的[仿射参数](@entry_id:260625)”。

总结来说，[测地线](@entry_id:269969)不仅是几何上“最直”的路径，它们也具有优美的[运动学](@entry_id:173318)性质：[自由粒子](@entry_id:148748)沿[测地线](@entry_id:269969)运动时，其速率（相对于[仿射参数](@entry_id:260625)，如时间或[弧长](@entry_id:191173)）保持恒定。这一深刻的联系是[黎曼几何](@entry_id:160508)理论和谐与力量的又一体现。