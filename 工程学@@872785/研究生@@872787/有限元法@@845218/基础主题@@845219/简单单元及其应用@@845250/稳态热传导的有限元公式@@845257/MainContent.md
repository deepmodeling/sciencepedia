## 引言
有限元方法 (FEM) 是现代工程与[科学计算](@entry_id:143987)中解决[热传导](@entry_id:147831)问题不可或缺的强大工具。从电子芯片的散热设计到航空发动机的温度场分析，其应用无处不在。然而，要真正掌握并有效运用这一方法，必须深入理解其背后的数学原理与实现细节，将抽象的理论与具体的代码实现联系起来。本文旨在系统性地构建[稳态热传导](@entry_id:177666)问题的有限元公式，填补物理方程与最终数值解之间的知识鸿沟。

本文将通过三个核心章节，引领读者完成从理论到实践的完整学习路径。在“原理与机制”一章中，我们将从物理问题的控制方程出发，详细推导其等价的[弱形式](@entry_id:142897)，并介绍如何通过单元离散、[等参映射](@entry_id:173239)等技术，最终将其转化为可计算的代数方程组。随后的“应用与跨学科联系”一章将展示该方法强大的灵活性，探讨如何处理复杂的边界条件、[非均质材料](@entry_id:196262)，并揭示其与生物[热传导](@entry_id:147831)、热-力耦合等前沿领域的深刻联系。最后，“动手实践”部分提供了一系列精心设计的编程练习，帮助读者将理论知识转化为实际的编程能力，亲手构建并验证自己的有限元求解器。

通过学习本篇文章，您将不仅理解[稳态热传导](@entry_id:177666)有限元分析的“如何做”，更能深刻领会其“为什么”如此构建，为解决更复杂的工程与科学问题奠定坚实的基础。

## 原理与机制

本章旨在系统性地阐述[稳态热传导](@entry_id:177666)问题有限元公式的理论基础与核心机制。我们将从物理问题的数学描述（即强形式）出发，推导出适用于数值计算的[变分形式](@entry_id:166033)（即[弱形式](@entry_id:142897)），并为其建立严格的数学基础。随后，我们将详细探讨从连续介质问题到离散代数系统的转化过程，包括单元的离散化、[等参映射](@entry_id:173239)、单元矩阵的形成以及全局系统的组装。最后，我们将讨论解的后处理及其物理解释。

### 控制方程：强形式

有限元分析的起点是待求解物理问题的数学描述，即由[偏微分方程](@entry_id:141332)和边界条件构成的定解问题，我们称之为**强形式 (strong form)**。对于[稳态热传导](@entry_id:177666)问题，其强形式建立在[能量守恒](@entry_id:140514)定律和[傅里叶热传导定律](@entry_id:138911)两大物理原则之上。

考虑一个位于 $\mathbb{R}^d$ ($d=2$ 或 $3$) 空间中的有界域 $\Omega$。在[稳态](@entry_id:182458)条件下，即系统中各点的温度不随时间变化，[能量守恒](@entry_id:140514)定律要求任何一个控制体内热量的产生率必须与通过其表面的净热流出率[相平衡](@entry_id:136822)。结合傅里叶定律，我们可以推导出控制区域 $\Omega$ 内部的温度场 $T(\mathbf{x})$ 所满足的控制[偏微分方程](@entry_id:141332)：

$$
-\nabla \cdot \big(\mathbf{k}(\mathbf{x}) \nabla T(\mathbf{x})\big) = Q(\mathbf{x}) \quad \text{在 } \Omega \text{ 内}
$$

让我们逐一解析此方程中的各项物理意义 [@problem_id:2599181]：

*   $T(\mathbf{x})$ 是空间点 $\mathbf{x}$ 处的**温度场**，是该问题的基本未知量。
*   $Q(\mathbf{x})$ 是单位体积的**内部热源**。当 $Q > 0$ 时，表示该处有热量生成（如[化学反应](@entry_id:146973)放热、电流热效应等）；当 $Q  0$ 时，则表示该处为“热汇”，有热量被吸收。
*   $\nabla T$ 是温度梯度，一个指向温度最快上升方向的向量。
*   $\mathbf{k}(\mathbf{x})$ 是**[热导率](@entry_id:147276)张量**，描述了材料在不同方向上的导热性能。对于[各向同性材料](@entry_id:170678)，$\mathbf{k}$ 是一个标量乘以单位矩阵；而对于[各向异性材料](@entry_id:184874)（如[复合材料](@entry_id:139856)、晶体等），$\mathbf{k}$ 是一个对称的[正定张量](@entry_id:204409)。
    *   **对称性** ($\mathbf{k} = \mathbf{k}^\top$) 是由非[平衡热力学](@entry_id:139780)的昂萨格 (Onsager) 倒易关系保证的，是输运系数矩阵的一个基本性质。
    *   **[正定性](@entry_id:149643)** (positive definiteness) 保证了热量总是从高温区流向低温区，这与[热力学第二定律](@entry_id:142732)相符。数学上，这意味着对于任意非零向量 $\boldsymbol{\xi}$，都有 $\boldsymbol{\xi}^\top \mathbf{k} \boldsymbol{\xi}  0$。为了保证[偏微分方程](@entry_id:141332)的椭圆性和解的良定性，我们通常要求 $\mathbf{k}$ 是**一致正定**的，即存在一个常数 $\alpha  0$，使得 $\boldsymbol{\xi}^\top \mathbf{k}(\mathbf{x}) \boldsymbol{\xi} \ge \alpha |\boldsymbol{\xi}|^2$ 对几乎所有的 $\mathbf{x} \in \Omega$ 成立。
*   热流密度向量 $\mathbf{q}$ 由**[傅里叶定律](@entry_id:136311) (Fourier's law)** 定义：$\mathbf{q} = -\mathbf{k} \nabla T$。负号表明热流方向与温度梯度方向相反。
*   $-\nabla \cdot (\mathbf{k} \nabla T)$ 这一项实际上是 $-\nabla \cdot \mathbf{q}$，代表了热流密度的负散度。整个方程 $-\nabla \cdot \mathbf{q} = Q$ 精确地表达了[能量守恒](@entry_id:140514)：热流的净流出率等于内部热源的生成率。

一个完整的定解问题除了控制方程，还必须包含定义在区域边界 $\partial\Omega$ 上的**边界条件**。设 $\mathbf{n}$ 为边界上的单位外法向向量。常见的热边界条件有三类：

1.  **[第一类边界条件](@entry_id:142800)（[狄利克雷条件](@entry_id:137096), Dirichlet condition）**：在边界部分 $\Gamma_D$ 上直接给定温度值 $\bar{T}$。
    $$
    T = \bar{T} \quad \text{在 } \Gamma_D \text{ 上}
    $$
    这类边界条件也被称为**[本质边界条件](@entry_id:173524) (essential boundary condition)**。

2.  **第二类边界条件（[诺伊曼条件](@entry_id:165471), Neumann condition）**：在边界部分 $\Gamma_N$ 上给定沿外法线方向的[热通量](@entry_id:138471) $\bar{q}$。离开物体的热通量为 $\mathbf{q} \cdot \mathbf{n}$。根据[傅里叶定律](@entry_id:136311)，这等于 $(-\mathbf{k} \nabla T) \cdot \mathbf{n}$。因此，若规定 $\bar{q}  0$ 表示热量流出物体，则有：
    $$
    -\mathbf{n} \cdot (\mathbf{k} \nabla T) = \bar{q} \quad \text{在 } \Gamma_N \text{ 上}
    $$
    这类边界条件也被称为**自然边界条件 (natural boundary condition)**。

3.  **第三类边界条件（[罗宾条件](@entry_id:153384), Robin condition）**：在边界部分 $\Gamma_R$ 上，物体与温度为 $T_\infty$ 的外部环境发生[对流换热](@entry_id:151349)。根据[牛顿冷却定律](@entry_id:142531)，[对流](@entry_id:141806)带走的热通量为 $h(T - T_\infty)$，其中 $h$ 是[对流换热系数](@entry_id:151029)。该[热通量](@entry_id:138471)必须与从物体内部传导至表面的[热通量](@entry_id:138471)相等。因此：
    $$
    -\mathbf{n} \cdot (\mathbf{k} \nabla T) = h(T - T_\infty) \quad \text{在 } \Gamma_R \text{ 上}
    $$
    当物体表面温度 $T$ 高于环境温度 $T_\infty$ 时，热量流出，右侧为正，与左侧的热流出定义一致。[罗宾条件](@entry_id:153384)同样属于自然边界条件。

强形式要求解 $T(\mathbf{x})$ 具有足够的连续性和可微性（例如，二次连续可微），以便方程中的所有导数都有经典的定义。然而，在处理复杂几何形状或非光滑材料属性时，这种要求过于苛刻，促使我们转向一种更灵活的数学框架——弱形式。

### 变分表述：[弱形式](@entry_id:142897)

弱形式 (weak form) 是有限元方法的核心，它通过降低对解的[光滑性](@entry_id:634843)要求，将[微分方程](@entry_id:264184)问题转化为等价的积分方程问题。其推导过程基于**[加权余量法](@entry_id:165159) (method of weighted residuals)**。

我们从强形式的控制方程出发，将其乘以一个任意的、满足特定条件的“测试函数” (test function) $w$，并在整个求解域 $\Omega$ 上进行积分。这个测试函数也称为权重函数。

$$
\int_{\Omega} w \left( -\nabla \cdot (\mathbf{k} \nabla T) - Q \right) d\Omega = 0
$$

为了降低对解 $T$ 的可微性要求，我们使用**分部积分 (integration by parts)**（即[高斯散度定理](@entry_id:188065)或[格林第一恒等式](@entry_id:170345)）来处理包含[二阶导数](@entry_id:144508)的项。

$$
-\int_{\Omega} w \big(\nabla \cdot (\mathbf{k} \nabla T)\big) d\Omega = \int_{\Omega} \nabla w \cdot (\mathbf{k} \nabla T) d\Omega - \int_{\partial\Omega} w (\mathbf{n} \cdot \mathbf{k} \nabla T) d\Gamma
$$

通过这个操作，我们将对 $T$ 的[二阶导数](@entry_id:144508)要求转移为对 $T$ 和 $w$ 各自的[一阶导数](@entry_id:749425)要求。将上式代入加权余量积分式，并整理可得：

$$
\int_{\Omega} \nabla w \cdot (\mathbf{k} \nabla T) d\Omega = \int_{\Omega} w Q d\Omega + \int_{\partial\Omega} w (-\mathbf{n} \cdot \mathbf{k} \nabla T) d\Gamma
$$

这个方程是弱形式的雏形。其中的边界积分项 $\int_{\partial\Omega} w (-\mathbf{n} \cdot \mathbf{k} \nabla T) d\Gamma$ 是连接强形式和[弱形式](@entry_id:142897)的关键。正是通过处理这个边界项，我们得以区分[本质边界条件和自然边界条件](@entry_id:168198) [@problem_id:2599235, @problem_id:2599209]。

#### [本质边界条件与自然边界条件](@entry_id:146051)

*   **[本质边界条件](@entry_id:173524) (Essential Boundary Conditions)**：对于狄利克雷边界 $\Gamma_D$ 上的条件 $T = \bar{T}$，温度值是直接给定的。然而，维持这个温度所需的“反作用热流” $-\mathbf{n} \cdot (\mathbf{k} \nabla T)$ 是未知的。为了在[弱形式](@entry_id:142897)中消除这个未知项，我们巧妙地选择测试函数 $w$，强制其在狄利克雷边界 $\Gamma_D$ 上为零，即 $w|_{\Gamma_D} = 0$。这样一来，边界积分在 $\Gamma_D$ 上的部分就自动消失了。因此，[狄利克雷条件](@entry_id:137096)必须通过限制解函数和测试函数所在的函数空间来**强行施加**，故称为本质边界条件。

*   **自然边界条件 (Natural Boundary Conditions)**：对于诺伊曼边界 $\Gamma_N$ 和罗宾边界 $\Gamma_R$，边界条件本身就规定了热通量 $-\mathbf{n} \cdot (\mathbf{k} \nabla T)$。因此，我们可以直接将这些已知的关系代入边界积分中。
    *   在 $\Gamma_N$ 上，$-\mathbf{n} \cdot (\mathbf{k} \nabla T) = \bar{q}$，边界积分项变为 $\int_{\Gamma_N} w \bar{q} d\Gamma$。
    *   在 $\Gamma_R$ 上，$-\mathbf{n} \cdot (\mathbf{k} \nabla T) = h(T - T_\infty)$，边界积分项变为 $\int_{\Gamma_R} w h(T - T_\infty) d\Gamma$。

这些边界条件通过[变分方程](@entry_id:635018)本身得到满足，仿佛是“自然而然”地融入了方程中，因此被称为自然边界条件。

将边界条件代入后，我们得到最终的**[弱形式](@entry_id:142897)**：寻找一个满足本质边界条件 $T = \bar{T}$ on $\Gamma_D$ 的解 $T$，使得对于所有满足 $w=0$ on $\Gamma_D$ 的测试函数 $w$，下式恒成立：

$$
\int_{\Omega} \nabla w \cdot (\mathbf{k} \nabla T) d\Omega + \int_{\Gamma_R} w h T d\Gamma = \int_{\Omega} w Q d\Omega + \int_{\Gamma_N} w \bar{q} d\Gamma + \int_{\Gamma_R} w h T_\infty d\Gamma
$$

为了书写简洁，我们通常将上式整理为[标准形式](@entry_id:153058) $a(w, T) = L(w)$，其中：

*   **双线性形式 (Bilinear form)** $a(w, T)$ 包含了所有与未知解 $T$ 相关的项：
    $$
    a(w, T) = \int_{\Omega} \nabla w \cdot (\mathbf{k} \nabla T) d\Omega + \int_{\Gamma_R} w h T d\Gamma
    $$
*   **线性泛函 (Linear functional)** $L(w)$ 包含了所有“载荷”项，即不依赖于未知解 $T$ 的项：
    $$
    L(w) = \int_{\Omega} w Q d\Omega + \int_{\Gamma_N} w \bar{q} d\Gamma + \int_{\Gamma_R} w h T_\infty d\Gamma
    $$

### 数学基础：索博列夫空间与变分原理

弱形式的推导虽然直观，但其严谨性依赖于现代数学中的泛函分析理论。

#### 索博列夫空间 (Sobolev Spaces)

弱[形式的积分](@entry_id:158607)表达式（如 $\int \nabla w \cdot \mathbf{k} \nabla T \, d\Omega$）要求函数及其一阶导数都是平方可积的。传统的[连续可微函数](@entry_id:200349)空间 $C^1(\Omega)$ 无法涵盖所有物理上有意义的解（例如，在[材料界面](@entry_id:751731)处温度梯度可能发生跳跃，导致解是“尖的”）。为此，我们引入**[索博列夫空间](@entry_id:141995) $H^1(\Omega)$**。

$H^1(\Omega)$ 空间的定义如下 [@problem_id:2599182]：
$$
H^1(\Omega) = \left\{ u \in L^2(\Omega) \, : \, \frac{\partial u}{\partial x_i} \in L^2(\Omega) \text{ for } i=1,\dots,d \text{ (在弱导数意义下)} \right\}
$$
其中 $L^2(\Omega)$ 是[平方可积函数](@entry_id:200316)空间。简而言之，$H^1(\Omega)$ 包含了自身平方可积且其“弱”一阶导数也平方可积的所有函数。这个空间是[弱形式](@entry_id:142897)表述的自然舞台。

对于边界值的处理，[泛函分析](@entry_id:146220)中的**[迹定理](@entry_id:203967) (trace theorem)** 保证了对于定义在足够光滑（例如，Lipschitz）区域上的 $H^1$ 函数，其在边界上的“值”（即迹）是有良好定义的，并且属于边界上的[平方可积函数](@entry_id:200316)空间 $L^2(\partial\Omega)$。这为严格定义 $T|_{\Gamma_D} = \bar{T}$ 和 $w|_{\Gamma_D} = 0$ 提供了理论依据。施加了齐次[本质边界条件](@entry_id:173524)的测试[函数空间](@entry_id:143478)因此被严谨地定义为 $H^1_{0,\Gamma_D}(\Omega) = \{ v \in H^1(\Omega) : v|_{\Gamma_D} = 0 \text{ in the trace sense} \}$。这个空间也可以等价地定义为在 $H^1$ 范数下，所有在 $\Gamma_D$ 上为零的[光滑函数](@entry_id:267124)的闭包 [@problem_id:2599182, @problem_id:2599182]。

#### [变分原理](@entry_id:198028) (Variational Principle)

对于热导率张量 $\mathbf{k}$ 对称的问题，求解[弱形式](@entry_id:142897) $a(w, T) = L(w)$ 与求解一个等价的最小化问题是完全一致的。我们可以构造一个**能量泛函 (energy functional)** $\Pi(T)$ [@problem_id:2599183]：

$$
\Pi(T) = \frac{1}{2} a(T, T) - L(T) = \frac{1}{2} \int_{\Omega} \nabla T \cdot \mathbf{k} \nabla T d\Omega - \int_{\Omega} T Q d\Omega - \dots
$$

可以证明，在满足本质边界条件的许可[函数空间](@entry_id:143478)中，找到一个函数 $T$ 使得[能量泛函](@entry_id:170311) $\Pi(T)$ 达到最小值，这个函数 $T$ 正是[弱形式](@entry_id:142897)的解。弱形式方程 $a(w, T) = L(w)$ 实际上是泛函 $\Pi(T)$ 取极小值的[一阶必要条件](@entry_id:170730)（即其在任意方向 $w$ 上的[Gâteaux导数](@entry_id:164612)为零）。

这个等价性不仅提供了对有限元方法的深刻物理解释（系统趋向于能量最低状态），也为解的存在性和唯一性提供了保证。如果[双线性形式](@entry_id:746794) $a(\cdot, \cdot)$ 是**强制的 (coercive)** 并且泛函 $\Pi(T)$ 是**严格凸的 (strictly convex)**，那么最小值存在且唯一。这两个性质正是由热导率张量 $\mathbf{k}$ 的一致正定性以及在有狄利克雷边界（即 $\Gamma_D$ 测度大于零）时成立的[庞加莱不等式](@entry_id:142086) (Poincaré's inequality) 所保证的 [@problem_id:2599183]。如果 $\mathbf{k}$ 不对称，则该问题不再对应一个[能量最小化](@entry_id:147698)原理。

### 离散化：从连续到代数

有限元方法通过将求解域 $\Omega$ 剖分为有限数量的、简单的子域——**单元 (elements)** $\Omega_e$，并将连续的[弱形式](@entry_id:142897)问题转化为一个大型代数方程组，从而实现数值求解。

#### 单元内插与[等参映射](@entry_id:173239)

在每个单元 $\Omega_e$ 内部，未知的温度场 $T$ 被近似为单元节点温度 $T_i$ 的线性组合：
$$
T_h(\mathbf{x}) \approx \sum_{i=1}^{n_{en}} N_i(\mathbf{x}) T_i = \mathbf{N}(\mathbf{x}) \mathbf{T}_e
$$
其中 $N_i$ 是**形函数 (shape functions)**，$\mathbf{T}_e$ 是包含单元所有节点温度的列向量。相应地，温度梯度可以表示为：
$$
\nabla T_h(\mathbf{x}) = \sum_{i=1}^{n_{en}} (\nabla N_i(\mathbf{x})) T_i = \mathbf{B}(\mathbf{x}) \mathbf{T}_e
$$
这里的 $\mathbf{B}$ 矩阵由形函数梯度的列向量构成，是连接节点温度和单元内应变（在此为温度梯度）的关键。

为了处理不规则的几何形状，我们通常采用**[等参映射](@entry_id:173239) (isoparametric mapping)** [@problem_id:2599239]。其思想是将任意形状的物理单元 $\Omega_e$（位于物理[坐标系](@entry_id:156346) $\mathbf{x}=(x,y)$ 中）映射到一个规则的、简单的“父单元” $\hat{\Omega}$（位于参数[坐标系](@entry_id:156346) $\boldsymbol{\xi}=(\xi,\eta)$ 中，例如一个边长为2的正方形）。这个映射本身也使用相同的形函数来描述：
$$
\mathbf{x}(\boldsymbol{\xi}) = \sum_{i=1}^{n_{en}} N_i(\boldsymbol{\xi}) \mathbf{x}_i
$$
其中 $\mathbf{x}_i$ 是物理单元的节点坐标。这种几何与场变量使用相同插值的思想即为“等参”。

在父单元中进行计算，需要[坐标变换](@entry_id:172727)关系。根据[链式法则](@entry_id:190743)，物理[坐标系](@entry_id:156346)下的梯度 $\nabla$ 和参数[坐标系](@entry_id:156346)下的梯度 $\nabla_{\xi}$ 通过**雅可比矩阵 (Jacobian matrix)** $\mathbf{J} = \partial \mathbf{x} / \partial \boldsymbol{\xi}$ 联系起来：
$$
\nabla N_i = (\mathbf{J}^{-1})^\top \nabla_{\xi} N_i = \mathbf{J}^{-\top} \nabla_{\xi} N_i
$$
同时，积分微元也需要变换：$d\Omega = \det(\mathbf{J}) d\hat{\Omega}$。通过这些变换，所有在物理单元上的复杂积分都可以转化为在规则父单元上的简单[数值积分](@entry_id:136578)。

#### [单元刚度矩阵](@entry_id:139369)与[载荷向量](@entry_id:635284)

将单元近似代入[弱形式](@entry_id:142897) $a(w,T)=L(w)$，并选择测试函数 $w$ 为每个形函数 $N_i$，我们便可以得到单元级别的代数方程组 $\mathbf{K}_e \mathbf{T}_e = \mathbf{F}_e$。

**[单元刚度矩阵](@entry_id:139369) (element stiffness matrix)** $\mathbf{K}_e$ 的分量为：
$$
(K_e)_{ij} = a(N_i, N_j) = \int_{\Omega_e} \nabla N_i \cdot (\mathbf{k} \nabla N_j) d\Omega + \int_{\Gamma_{R,e}} h N_i N_j d\Gamma
$$
这里 $\Gamma_{R,e}$ 是单元边界上属于罗宾边界的部分。对于线性三角单元，$\mathbf{B}$ 矩阵是常数，若 $\mathbf{k}$ 也为常数，则体积积分项可简化为 $A_e (\mathbf{B}^\top \mathbf{k} \mathbf{B})$，其中 $A_e$ 是单元面积 [@problem_id:2599160]。由于 $\mathbf{k}$ 的对称性，双线性形式 $a(N_i, N_j) = a(N_j, N_i)$，因此[单元刚度矩阵](@entry_id:139369) $\mathbf{K}_e$ 也是对称的。

**[单元载荷向量](@entry_id:748928) (element load vector)** $\mathbf{F}_e$ 的分量为：
$$
(F_e)_i = L(N_i) = \int_{\Omega_e} N_i Q d\Omega + \int_{\Gamma_{N,e}} N_i \bar{q} d\Gamma + \int_{\Gamma_{R,e}} N_i h T_\infty d\Gamma
$$
它综合了来自体热源 $Q$、诺伊曼边界通量 $\bar{q}$ 和罗宾边界[对流](@entry_id:141806)环境温度 $T_\infty$ 的贡献 [@problem_id:2599185]。注意，[罗宾边界条件](@entry_id:163914) $h(T-T_\infty)$ 被拆分：与 $T$ 相关的部分 $hT$ 贡献给了刚度矩阵，而与 $T_\infty$ 相关的部分 $hT_\infty$ 贡献给了[载荷向量](@entry_id:635284)。

### 组装与求解

计算出每个单元的 $\mathbf{K}_e$ 和 $\mathbf{F}_e$ 后，下一步是**[全局组装](@entry_id:749916) (global assembly)**，将它们“拼接”成一个描述整个系统的大型[代数方程](@entry_id:272665)组 $\mathbf{K}\mathbf{T} = \mathbf{F}$。

组装过程依据单元的**连接关系 (connectivity)** 进行，即每个单元的局部节点号与全局节点号的对应关系。这个过程可以被形式化地描述为“散点-相加”(scatter-add) 操作 [@problem_id:2599150]：
$$
K_{IJ} \mathrel{+}= (K_e)_{ij}, \quad F_{I} \mathrel{+}= (F_e)_{i}
$$
其中 $i,j$ 是单元的局部节点号，$I,J$ 是它们对应的全局节点号。对于共享节点的相邻单元，它们的贡献会在全局矩阵和向量的相应位置上叠加。这种叠加在物理上正体现了节点处的热流平衡和[温度连续性](@entry_id:755837)。

组装完成后，得到的全局[方程组](@entry_id:193238) $\mathbf{K}\mathbf{T} = \mathbf{F}$ 尚不能直接求解，因为我们还未施加本质（狄利克雷）边界条件。一种标准方法是对[方程组](@entry_id:193238)进行**分区 (partitioning)** [@problem_id:2599150]。将自由度分为未知的自由度 $\mathcal{F}$ 和已知的（给定温度的）约束自由度 $\mathcal{C}$，[方程组](@entry_id:193238)可以写成：
$$
\begin{pmatrix} \mathbf{K}_{\mathcal{FF}}  \mathbf{K}_{\mathcal{FC}} \\ \mathbf{K}_{\mathcal{CF}}  \mathbf{K}_{\mathcal{CC}} \end{pmatrix}
\begin{pmatrix} \mathbf{T}_{\mathcal{F}} \\ \mathbf{T}_{\mathcal{C}} \end{pmatrix}
=
\begin{pmatrix} \mathbf{F}_{\mathcal{F}} \\ \mathbf{F}_{\mathcal{C}} \end{pmatrix}
$$
由于 $\mathbf{T}_{\mathcal{C}}$ 是已知的规定值 $\bar{\mathbf{T}}$，我们只需解耦合并求解关于未知温度 $\mathbf{T}_{\mathcal{F}}$ 的方程：
$$
\mathbf{K}_{\mathcal{FF}} \mathbf{T}_{\mathcal{F}} = \mathbf{F}_{\mathcal{F}} - \mathbf{K}_{\mathcal{FC}} \bar{\mathbf{T}}
$$
求解这个[线性方程组](@entry_id:148943)（通常规模很大且稀疏）后，就得到了所有未知节点的温度值。

### 后处理与结果解读

获得节点温度向量 $\mathbf{T}$ 并不是分析的终点。我们常常关心一些导出量，例如热流密度。

在每个单元内部，热流密度可以通过傅里叶定律和单元的温度近似来计算 [@problem_id:2599196]：
$$
\mathbf{q}_h|_{\Omega_e} = -\mathbf{k}_e \nabla T_h|_{\Omega_e} = -\mathbf{k}_e \mathbf{B}_e \mathbf{T}_e
$$

一个至关重要的特性是，对于标准的 $C^0$ 连续有限元（例如，拉格朗日单元），近似温度场 $T_h$ 在单元边界是连续的，但其梯度 $\nabla T_h$ 通常是**不连续的**。由于计算出的热流 $\mathbf{q}_h$ 与梯度成正比，因此 $\mathbf{q}_h$ 在单元边界上通常也会出现跳跃。这意味着，直接后处理得到的应力或热流场是分片、不连续的。

尽管热流在点上不连续，但有限元解在弱形式意义上保证了跨单元边界的热流是守恒的。即热流法向分量的跳跃在积分意义下为零。若要获得法向分量连续的热流场，需要采用更高级的有限元方法，如**[混合有限元法](@entry_id:165231) (mixed FEM)**，它将热流作为独立的未知量，并在 $H(\text{div})$ 空间中进行近似 [@problem_id:2599196]。

在特定情况下，例如当精确解是线性场且采用线性单元时，有限元解可以精确地捕捉到解，此时计算出的热流场是常数，因而在全局都是连续的。这被称为通过了**“[分片检验](@entry_id:162864)” (patch test)** [@problem_id:2599196]。