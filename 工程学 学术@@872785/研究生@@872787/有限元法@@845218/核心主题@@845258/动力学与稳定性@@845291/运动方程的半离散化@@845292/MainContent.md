## 引言
在工程与科学领域，对结构在动载荷下的响应进行预测至关重要。有限元方法（FEM）为分析复杂系统的动力学行为提供了强大的工具，但其核心挑战在于如何将描述连续介质运动的复杂[偏微分方程](@entry_id:141332)（PDE）转化为可计算的代数形式。解决这一挑战的关键一步，便是本文将要深入探讨的主题：[运动方程](@entry_id:170720)的[半离散化](@entry_id:163562)。这一过程是连接连续[体力](@entry_id:174230)学理论与数值计算实践的桥梁，它将无限维的物理问题投影到有限维的数学模型上，但暂时保留了时间的连续性。

本文旨在系统性地揭示[半离散化](@entry_id:163562)过程的原理、机制及其深远影响。通过学习，您将不仅理解这一过程的数学推导，更能洞察其背后深刻的物理意义。我们将分为三个章节进行阐述：

在“原理与机制”一章中，我们将从[虚功原理](@entry_id:138749)出发，运用[伽辽金法](@entry_id:749698)逐步推导出标准的[二阶常微分方程](@entry_id:204212)组。您将学习到[质量矩阵](@entry_id:177093)、[刚度矩阵](@entry_id:178659)和阻尼矩阵是如何从第一性原理中自然产生的，并深入理解它们的对称性、[正定性](@entry_id:149643)等数学性质如何反映了系统的[能量守恒](@entry_id:140514)与物理特性。

接着，在“应用与跨学科[交叉](@entry_id:147634)”一章中，我们将展示[半离散化](@entry_id:163562)方程的巨大威力。从基础的[模态分析](@entry_id:163921)、阻尼建模，到高级的非线性动力学、稳定性问题（如[屈曲](@entry_id:162815)和[颤振](@entry_id:749473)），再到前沿的拓扑优化和[物质点法](@entry_id:144728)（MPM），您将看到这同一个数学框架如何在不同领域中得到应用和发展。

最后，“动手实践”部分将通过一系列精心设计的练习，引导您将理论知识付诸实践，巩固对矩阵推导、[刚体模态](@entry_id:754366)和数值频散等核心概念的理解。

现在，让我们从第一章开始，踏上将连续世界离散化的旅程，首先探索其基本原理与内在机制。

## 原理与机制

在上一章中，我们介绍了利用有限元方法分析动力学问题的总体思路。本章我们将深入探讨其核心步骤之一：[运动方程](@entry_id:170720)的[半离散化](@entry_id:163562)。这一过程将描述连续体力学行为的[偏微分方程](@entry_id:141332)（PDE）转化为一个常微分方程（ODE）组，为后续的时间积分计算奠定了数学基础。我们将从第一性原理出发，系统地推导这一过程，并详细阐释所得到的离散系统中各个矩阵的物理意义、数学性质及其对系统动态响应的影响。

### 从连续介质到离散系统：[半离散化](@entry_id:163562)过程

我们考虑一个占据有界域 $\Omega \subset \mathbb{R}^d$（$d \in \{2,3\}$）的弹性体。其运动由线动量[守恒定律](@entry_id:269268)（即[牛顿第二定律](@entry_id:274217)的连续介质形式）描述。在小应变假设下，其强形式为：
$$
\rho(\mathbf{x})\,\ddot{\mathbf{u}}(\mathbf{x},t) - \nabla\cdot\boldsymbol{\sigma}(\mathbf{x},t) = \mathbf{b}(\mathbf{x},t) \quad \text{in } \Omega \times (0,T)
$$
其中，$\rho(\mathbf{x})$ 是质量密度，$\mathbf{u}(\mathbf{x},t)$ 是位移场，$\ddot{\mathbf{u}}$ 是其对时间的[二阶导数](@entry_id:144508)（加速度），$\boldsymbol{\sigma}$ 是柯西应力张量，$\mathbf{b}$ 是单位体积的[体力](@entry_id:174230)。此外，系统还需满足在边界 $\partial\Omega$ 上的位移（本质）边界条件和力（自然）边界条件 [@problem_id:2594260]。

直接求解此[偏微分方程](@entry_id:141332)通常非常困难。有限元方法通过其[弱形式](@entry_id:142897)（或[变分形式](@entry_id:166033)）来寻求近似解。[弱形式](@entry_id:142897)是通过[虚功原理](@entry_id:138749)得到的，即我们将上述强形式方程乘以一个任意的、满足[运动学](@entry_id:173318)许可条件的[虚位移](@entry_id:168781)（或称测试函数）$\mathbf{v}(\mathbf{x})$，并在整个求解域 $\Omega$ 上积分。通过应用[散度定理](@entry_id:143110)（[分部积分](@entry_id:136350)），我们将应力[张量的散度](@entry_id:191736)项转化为一个[体积分](@entry_id:171119)和一个[面积分](@entry_id:275394)，从而得到[虚功原理](@entry_id:138749)的数学表述：
$$
\int_{\Omega} \mathbf{v} \cdot (\rho \ddot{\mathbf{u}}) \, dV + \int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, dV = \int_{\Omega} \mathbf{v} \cdot \mathbf{b} \, dV + \int_{\Gamma_N} \mathbf{v} \cdot \bar{\mathbf{t}} \, dS
$$
其中，左边第一项是惯性力所做的[虚功](@entry_id:176403)，第二项是内力所做的[虚功](@entry_id:176403)（$\boldsymbol{\varepsilon}(\mathbf{v})$ 是与[虚位移](@entry_id:168781)对应的虚应变），右边则是外力（体力 $\mathbf{b}$ 和在边界 $\Gamma_N$ 上给定的面力 $\bar{\mathbf{t}}$）所做的[虚功](@entry_id:176403)。

**[半离散化](@entry_id:163562)**的核心思想在于，将无限维的[解空间](@entry_id:200470)（所有可能的[位移场](@entry_id:141476) $\mathbf{u}$）投影到一个有限维的[子空间](@entry_id:150286)上。具体而言，我们用一组预先选定的、仅与空间位置 $\mathbf{x}$ 有关的[基函数](@entry_id:170178)（称为**形函数**或**[基函数](@entry_id:170178)**）$\mathbf{N}(\mathbf{x})$ 的[线性组合](@entry_id:154743)来近似真实的[位移场](@entry_id:141476)：
$$
\mathbf{u}(\mathbf{x}, t) \approx \mathbf{u}_h(\mathbf{x}, t) = \mathbf{N}(\mathbf{x})\mathbf{d}(t)
$$
这里，$\mathbf{d}(t)$ 是一个列向量，包含了所有节点在时刻 $t$ 的未知位移（或称[广义坐标](@entry_id:156576)），是只依赖于时间的未知量。[伽辽金法](@entry_id:749698)（Galerkin method）是一种选择测试函数 $\mathbf{v}$ 的系统性方法，它要求测试函数与试验函数（即位移的近似函数）来自同一个函数空间，即 $\mathbf{v}(\mathbf{x}) = \mathbf{N}(\mathbf{x})\mathbf{c}$，其中 $\mathbf{c}$ 是任意的常数向量。

将此近似代入[弱形式](@entry_id:142897)，并利用 $\mathbf{c}$ 的任意性，我们便将原来描述连续体的[偏微分方程](@entry_id:141332)转化为了一个关于节点未知量 $\mathbf{d}(t)$ 的矩阵形式的[常微分方程组](@entry_id:266774) [@problem_id:2594279]：
$$
\mathbf{M}\ddot{\mathbf{d}}(t) + \mathbf{C}\dot{\mathbf{d}}(t) + \mathbf{K}\mathbf{d}(t) = \mathbf{F}(t)
$$
这个过程被称为**空间[半离散化](@entry_id:163562)**，因为它仅对空间变量进行了离散化，而时间变量 $t$ 仍然是连续的。这个[二阶常微分方程](@entry_id:204212)组是[结构动力学](@entry_id:172684)[有限元分析](@entry_id:138109)的出发点。与之相对的**全离散化**，则是在此基础上进一步采用某种[时间积分算法](@entry_id:756002)（如[Newmark-β法](@entry_id:173101)或[中心差分法](@entry_id:163679)）对时间域进行离散，最终得到一个[代数方程](@entry_id:272665)组。

### [系统矩阵](@entry_id:172230)：物理与数学的诠释

上述半离散方程中的矩阵 $\mathbf{M}$、$\mathbf{C}$、$\mathbf{K}$ 和向量 $\mathbf{F}$ 并非凭空产生，它们分别对应着系统的惯性、耗散、弹性和外部激励，其定义源于虚功原理中的各项积分。

#### 刚度矩阵 $\mathbf{K}$：弹性恢复力

**[刚度矩阵](@entry_id:178659)** $\mathbf{K}$ 源于[内力](@entry_id:167605)[虚功](@entry_id:176403)项 $\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, dV$。对于线弹性材料，[应力与应变](@entry_id:137374)通过本构关系 $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u})$ 联系，其中 $\mathbb{C}$ 是[四阶弹性张量](@entry_id:188318)。将[有限元近似](@entry_id:166278)代入，我们得到刚度矩阵的元素表达式：
$$
K_{ij} = a(\boldsymbol{\phi}_i, \boldsymbol{\phi}_j) = \int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{\phi}_i) : (\mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{\phi}_j)) \, dV
$$
其中 $a(\cdot, \cdot)$ 是与弹性相关的[双线性](@entry_id:146819)型，$\boldsymbol{\phi}_i$ 和 $\boldsymbol{\phi}_j$ 是与第 $i$ 和第 $j$ 个自由度相关的矢量[基函数](@entry_id:170178)。这个矩阵描述了节点位移 $\mathbf{d}$ 与其产生的节点恢复力 $\mathbf{f}_{\text{int}} = \mathbf{K}\mathbf{d}$ 之间的[线性关系](@entry_id:267880)。

一个至关重要的性质是刚度矩阵的**对称性**（$K_{ij} = K_{ji}$）。这一性质并非理所当然，它深刻地根植于材料的物理特性 [@problem_id:2594261]。首先，角动量守恒要求柯西[应力张量](@entry_id:148973)是对称的（$\boldsymbol{\sigma} = \boldsymbol{\sigma}^\mathsf{T}$），这使得内力[虚功](@entry_id:176403)只依赖于[位移梯度](@entry_id:165352)的对称部分，即[应变张量](@entry_id:193332)。然而，这还不足以保证 $\mathbf{K}$ 的对称。$\mathbf{K}$ 的对称性最终要求[弹性张量](@entry_id:170728) $\mathbb{C}$ 具有**主对称性**（Major Symmetry），即 $C_{ijkl} = C_{klij}$。物理上，这一对称性等价于材料存在一个[应变能密度函数](@entry_id:755490) $\Psi(\boldsymbol{\varepsilon})$，使得应力可以由其对应变的导数得到（$\boldsymbol{\sigma} = \partial\Psi/\partial\boldsymbol{\varepsilon}$）。对于线性材料，这意味着[应变能](@entry_id:162699)是一个关于应变的二次型：$U = \frac{1}{2}\mathbf{d}^\mathsf{T}\mathbf{K}\mathbf{d}$。因此，对称的刚度矩阵是系统能量保守（无耗散）特性的直接体现。

在数学上，如果约束了[刚体运动](@entry_id:193355)，刚度矩阵 $\mathbf{K}$ 是**对称正定**的。正定性保证了任何非零的变形都会储存正的[应变能](@entry_id:162699)，确保了静态问题的解是唯一且稳定的 [@problem_id:2594260]。

#### 质量矩阵 $\mathbf{M}$：惯性力

**质量矩阵** $\mathbf{M}$ 源于[惯性力](@entry_id:169104)[虚功](@entry_id:176403)项 $\int_{\Omega} \rho \mathbf{v} \cdot \ddot{\mathbf{u}} \, dV$。其元素表达式为：
$$
M_{ij} = \int_{\Omega} \rho(\mathbf{x}) \, \boldsymbol{\phi}_i(\mathbf{x}) \cdot \boldsymbol{\phi}_j(\mathbf{x}) \, dV
$$
这个矩阵被称为**[一致质量矩阵](@entry_id:174630)** (Consistent Mass Matrix)，因为它与推导刚度矩阵时所用的[基函数](@entry_id:170178) $\boldsymbol{\phi}$ 是一致的。

与刚度矩阵不同，[质量矩阵](@entry_id:177093)的性质更为优良 [@problem_id:2594310]。
1.  **对称性**：由于标量[点积](@entry_id:149019)的交换律，显然有 $M_{ij} = M_{ji}$，因此 $\mathbf{M}$ 总是对称的。
2.  **[正定性](@entry_id:149643)**：只要质量密度 $\rho(\mathbf{x})$ 处处为正，并且[基函数](@entry_id:170178)是线性无关的，质量矩阵 $\mathbf{M}$ 就是**对称正定**的。这一点与[刚度矩阵](@entry_id:178659)形成对比，$\mathbf{K}$ 的[正定性](@entry_id:149643)依赖于边界条件的设置（是否约束了刚体运动），而 $\mathbf{M}$ 的[正定性](@entry_id:149643)是内禀的。任何非零的节点速度向量 $\dot{\mathbf{d}}$ 都对应一个非零的运动场，因而具有正的动能。

物理上，质量矩阵将节点速度与系统的总动能联系起来：$T = \frac{1}{2}\dot{\mathbf{d}}^\mathsf{T}\mathbf{M}\dot{\mathbf{d}}$。矩阵的对角项 $M_{ii}$ 主要反映了与节点 $i$ 相关的质量惯性，而非对角项 $M_{ij}$ 则体现了节点 $i$ 和节点 $j$ 之间的**惯性耦合**。这种耦合效应是连续体质量分布在离散模型中的自然结果。

为了更具体地理解，我们考虑一个长度为 $L$、[截面](@entry_id:154995)积为 $A$、[杨氏模量](@entry_id:140430)为 $E$、密度为 $\rho$ 的[一维杆单元](@entry_id:171268) [@problem_id:2676289]。使用线性形函数 $N_1(x) = 1-x/L$ 和 $N_2(x) = x/L$，可以精确计算出其[一致质量矩阵](@entry_id:174630)为：
$$
\mathbf{M}_c = \int_{0}^{L} \rho A \begin{pmatrix} N_1^2  N_1 N_2 \\ N_2 N_1  N_2^2 \end{pmatrix} dx = \frac{\rho A L}{6} \begin{pmatrix} 2  1 \\ 1  2 \end{pmatrix}
$$
这个简单的例子清晰地展示了非对角项的存在，即节点1的加速度会通过质量矩阵影响到节点2所受的[惯性力](@entry_id:169104)。

#### 阻尼矩阵 $\mathbf{C}$ 和外力向量 $\mathbf{F}$

**阻尼矩阵** $\mathbf{C}$ 代表系统中的能量耗散机制。与 $\mathbf{M}$ 和 $\mathbf{K}$ 不同，$\mathbf{C}$ 很少能从材料本构的第一性原理直接导出，通常采用[唯象模型](@entry_id:273816)来构建。在[结构动力学](@entry_id:172684)中，最常见的模型是**[瑞利阻尼](@entry_id:172362)** (Rayleigh Damping)，它假设阻尼矩阵是[质量矩阵](@entry_id:177093)和刚度矩阵的[线性组合](@entry_id:154743) [@problem_id:2563517]：
$$
\mathbf{C} = \alpha \mathbf{M} + \beta \mathbf{K}
$$
其中 $\alpha$ 和 $\beta$ 是通过实验数据或经验确定的常数。这种形式在数学上处理方便，特别是它保证了阻尼矩阵与质量、[刚度矩阵](@entry_id:178659)具有相同的[本征向量](@entry_id:151813)，从而简化了[模态分析](@entry_id:163921)。

**外力向量** $\mathbf{F}(t)$ 整合了所有施加在结构上的外部作用，其表达式源于外力[虚功](@entry_id:176403)项：
$$
\mathbf{F}(t) = \int_{\Omega} \mathbf{N}^\mathsf{T} \mathbf{b}(t) \, dV + \int_{\Gamma_t} \mathbf{N}^\mathsf{T} \bar{\mathbf{t}}(t) \, dS
$$
这个表达式明确显示，体力 $\mathbf{b}$ 和在自然边界 $\Gamma_t$ 上施加的面力 $\bar{\mathbf{t}}$ 都通过与形函数 $\mathbf{N}$ 的加权积分，等效地分配到各个节点上，形成节点力向量 $\mathbf{F}$ [@problem_id:2594260]。

### 离散系统中的边界条件

在有限元方法中，两类边界条件的处理方式截然不同，理解其区别至关重要 [@problem_id:2594245]。

**自然边界条件 (Natural Boundary Conditions)**：这类条件涉及力或流量（如面力 $\boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}}$）。它们在推导[弱形式](@entry_id:142897)的分部积分过程中“自然”地出现，并最终成为外力向量 $\mathbf{F}(t)$ 的一部分。我们无需对离散系统进行特殊操作来施加它们，因为它们已经被内含在方程的右端项中。

**[本质边界条件](@entry_id:173524) (Essential Boundary Conditions)**：这类条件直接约束场变量本身（如位移 $\mathbf{u} = \bar{\mathbf{u}}$）。它们必须在求解过程中被精确满足，因此是对函数[解空间](@entry_id:200470)的强约束。在标准的[伽辽金法](@entry_id:749698)中，这通过构造[有限元基函数](@entry_id:749279)来实现，即要求[基函数](@entry_id:170178)本身在本质边界上满足齐次条件（$w=0$ on $\Gamma_u$）。在得到代数方程组后，非齐次条件通过直接修改[方程组](@entry_id:193238)来施加，例如，将已知节点位移代入，然后将相关项移到方程右侧，并从[方程组](@entry_id:193238)中移除对应的行和列。

除了这种标准方法，还存在其他施加[本质边界条件](@entry_id:173524)的**弱约[束方法](@entry_id:636307)**：
*   **罚函数法 (Penalty Method)**：通过在[弱形式](@entry_id:142897)中增加一个罚项 $\alpha \int_{\Gamma_u} (u-\bar{u}) \cdot w \, d\Gamma$（$\alpha$ 是一个大的罚参数），来近似满足位移约束。这会在刚度矩阵上增加一个与边界相关的“[罚刚度](@entry_id:753321)”项，并在力向量上增加一个相应的载荷项。
*   **拉格朗日乘子法 (Lagrange Multiplier Method)**：引入一个新的未知场（拉格朗日乘子），将位移约束作为附加的方程加入到整个系统。这会得到一个更大的、[鞍点形式](@entry_id:754477)的[方程组](@entry_id:193238)，但能精确满足约束。

### [半离散系统](@entry_id:754680)的性质与推论

由[半离散化](@entry_id:163562)得到的[常微分方程组](@entry_id:266774) $\mathbf{M}\ddot{\mathbf{d}} + \mathbf{C}\dot{\mathbf{d}} + \mathbf{K}\mathbf{d} = \mathbf{F}$ 本身具有一系列重要的物理和数学性质，这些性质决定了离散模型的动态行为。

#### [能量守恒](@entry_id:140514)

对于一个无阻尼（$\mathbf{C}=\mathbf{0}$）、无外力（$\mathbf{F}=\mathbf{0}$）的系统，其[总机械能](@entry_id:167353) $E(t)$ 为动能与势能之和：
$$
E(t) = T(t) + U(t) = \frac{1}{2}\dot{\mathbf{d}}^\mathsf{T}\mathbf{M}\dot{\mathbf{d}} + \frac{1}{2}\mathbf{d}^\mathsf{T}\mathbf{K}\mathbf{d}
$$
由于质量矩阵 $\mathbf{M}$ 和[刚度矩阵](@entry_id:178659) $\mathbf{K}$ 都是对称的，对能量求时间导数可以得到 $\frac{dE}{dt} = \dot{\mathbf{d}}^\mathsf{T}(\mathbf{M}\ddot{\mathbf{d}} + \mathbf{K}\mathbf{d})$。根据运动方程 $\mathbf{M}\ddot{\mathbf{d}} + \mathbf{K}\mathbf{d} = \mathbf{0}$，我们发现 $\frac{dE}{dt}=0$。这意味着，[半离散系统](@entry_id:754680)在时间上是连续的，并且完美地继承了其所模拟的无耗散连续介质的**[能量守恒](@entry_id:140514)**特性。这一结论不依赖于任何后续的[时间离散化](@entry_id:169380)格式 [@problem_id:2594279] [@problem_id:2594261]。

#### 质量集总：一种实用的近似

尽管[一致质量矩阵](@entry_id:174630) $\mathbf{M}_c$ 在理论上最为精确（它能精确表示由形[函数空间](@entry_id:143478)所能描述的任何[速度场](@entry_id:271461)的动能），但它的非对角特性（即“满”矩阵）在计算上可能带来不便，特别是在[显式时间积分](@entry_id:165797)算法中需要求 $\mathbf{M}^{-1}$。

为了简化计算，工程实践中常常采用**[集总质量矩阵](@entry_id:173011)** (Lumped Mass Matrix) $\mathbf{M}_l$ 来替代 $\mathbf{M}_c$。$\mathbf{M}_l$ 是一个对角矩阵，其基本思想是将单元的总质量以某种方式分配到各个节点上。一种常见的构造方法是“[行和集总](@entry_id:754439)”，即将[一致质量矩阵](@entry_id:174630)每行的元素加总，然后放到对角线上。对于前面提到的[一维杆单元](@entry_id:171268)，其[集总质量矩阵](@entry_id:173011)为 [@problem_id:2594284]：
$$
\mathbf{M}_l = \frac{\rho A L}{2} \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}
$$
与[一致质量矩阵](@entry_id:174630)相比，[集总质量矩阵](@entry_id:173011)具有以下特点 [@problem_id:2594284] [@problem_id:2578893]：
*   **保持总质量**：两种矩阵的总质量（所有元素之和）是相同的，都等于单元的物理总质量 $\rho A L$。
*   **动能近似**：对于刚体[平动](@entry_id:187700)，两种矩阵都能给出精确的动能。但对于变形运动，[集总质量矩阵](@entry_id:173011)通常只能提供动能的近似值。
*   **计算优势**：作为对角矩阵，$\mathbf{M}_l$ 的[逆矩阵](@entry_id:140380)极易求得，这对于[显式动力学](@entry_id:171710)分析至关重要。

#### 对系统动力特性的影响：[模态分析](@entry_id:163921)

结构的固有动力特性由其**自然频率**（或称固有频率）$\omega$ 和对应的**振型**（模态）$\boldsymbol{\phi}$ 决定。它们是无[阻尼自由振动](@entry_id:166590)方程的[特解](@entry_id:149080)，通过求解[广义特征值问题](@entry_id:151614)得到：
$$
\mathbf{K}\boldsymbol{\phi} = \omega^2 \mathbf{M}\boldsymbol{\phi}
$$
由于 $\mathbf{K}$ 和 $\mathbf{M}$ 均为对称正定矩阵，该问题保证有实数且非负的[特征值](@entry_id:154894) $\omega^2$。

使用[集总质量矩阵](@entry_id:173011)会改变这个[特征值问题](@entry_id:142153)，从而影响计算出的自然频率和振型 [@problem_id:2578893]。
*   **频率的改变**：对于给定的网格，由 $\mathbf{M}_l$ 计算出的频率通常不同于由 $\mathbf{M}_c$ 计算出的频率。一般而言，质量集总会使得离散系统的动力学模型在某种意义上“更软”，从而倾向于**降低**[高阶模](@entry_id:750331)态的自然频率。
*   **对不同模态的影响**：低阶模态（对应于平滑、长波长的[振型](@entry_id:179030)）对质量集总不敏感。而[高阶模](@entry_id:750331)态（对应于波长与单元尺寸相当的剧烈[振荡](@entry_id:267781)）对[质量矩阵](@entry_id:177093)的近似更为敏感，因此其频率受质量集总的影响更大。
*   **收敛性**：随着网格的加密，无论使用一致质量还是集总质量，计算出的频率都会收敛于真实的连续体频率，两者之间的差异也会随之减小。

一个重要的理论结果是模态的**正交性**。对于不同的[特征值](@entry_id:154894) $\omega_i \neq \omega_j$，其对应的[振型](@entry_id:179030) $\boldsymbol{\phi}_i$ 和 $\boldsymbol{\phi}_j$ 不仅关于[质量矩阵](@entry_id:177093)是正交的（$\boldsymbol{\phi}_i^\mathsf{T}\mathbf{M}\boldsymbol{\phi}_j = 0$），也关于[刚度矩阵](@entry_id:178659)是正交的（$\boldsymbol{\phi}_i^\mathsf{T}\mathbf{K}\boldsymbol{\phi}_j = 0$）。这个结论的成立仅依赖于 $\mathbf{M}$ 和 $\mathbf{K}$ 的对称性。因此，无论是使用对称的[一致质量矩阵](@entry_id:174630) $\mathbf{M}_c$ 还是对称的[集总质量矩阵](@entry_id:173011) $\mathbf{M}_l$，所得到的振型向量都同时满足 $\mathbf{M}$-正交和 $\mathbf{K}$-正交 [@problem_id:2578893]。

#### 高级主题：数值频散

[半离散化](@entry_id:163562)虽然在数学上是严谨的，但它终究是一种近似。这种近似引入的一个重要后果是**数值频散** (Numerical Dispersion)。在真实的连续介质中（如[一维波动方程](@entry_id:164824) $u_{tt} = c^2 u_{xx}$），所有频率的波都以相同的相速度 $c$ 传播。然而，在有限元半离散模型中，[波的传播](@entry_id:144063)速度会依赖于其频率（或波数）。

通过对均匀网格下的半离散方程进行[谐波分析](@entry_id:198768)（一种[冯·诺依曼稳定性分析](@entry_id:145718)的变体），可以推导出离散系统的频散关系 $\omega(k)$，其中 $k$ 是波数 [@problem_id:2594248]。这个关系通常是[非线性](@entry_id:637147)的，表明数值相速度 $c_p = \omega/k$ 和群速度 $v_g = d\omega/dk$ 并非一个常数，而是 $k$ 的函数。这意味着不同波长的波在离散网格中会以不同的速度传播，导致[波包](@entry_id:154698)在传播过程中发生变形和展宽。频散分析是评估不同离散格式（如不同单元类型或[质量矩阵](@entry_id:177093)类型）对波传播问题保真度的强有力工具，它揭示了离散化在动力学问题中引入的更深层次的误差。