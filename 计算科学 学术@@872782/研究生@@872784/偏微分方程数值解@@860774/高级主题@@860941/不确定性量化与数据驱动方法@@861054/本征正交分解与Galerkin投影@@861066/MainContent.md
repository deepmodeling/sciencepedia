## 引言
在现代科学与工程中，高保真度的数值模拟已成为理解、预测和设计复杂物理系统的基石。然而，这些通常由[偏微分方程](@entry_id:141332)（PDEs）描述的模型，在离散化后会产生维度极高（可达数百万甚至更高）的动力系统，直接求解它们需要巨大的计算资源，使得[实时控制](@entry_id:754131)、多查询优化或不确定性量化等任务变得遥不可及。如何弥合高精度与高效率之间的鸿沟？答案在于构建降阶模型（Reduced-Order Models, ROMs），这正是本文将要深入探讨的核心主题。

本文旨在系统性地介绍一种强大而应用广泛的降阶技术：基于[本征正交分解](@entry_id:165074)（POD）与[伽辽金投影](@entry_id:145611)的建模方法。通过学习本文，读者将掌握从复杂系统中提取关键动力学行为并构建快速、可靠代理模型的全过程。
*   在**“原理与机制”**一章中，我们将深入剖析该方法的数学基础。您将学习[伽辽金投影](@entry_id:145611)如何定义[子空间](@entry_id:150286)中的“最佳逼近”，以及[本征正交分解](@entry_id:165074)如何从数据中找到最优的降阶基。我们还将探讨处理[非线性](@entry_id:637147)、参数依赖性以及保证[模型稳定性](@entry_id:636221)的关键策略。
*   在**“应用与交叉学科联系”**一章中，我们将展示这些理论在实践中的巨大威力，通过横跨[流体力学](@entry_id:136788)、[结构工程](@entry_id:152273)、[生物力学](@entry_id:153973)乃至天体物理学的丰富案例，揭示降阶模型如何解决真实世界中的挑战性问题。
*   最后，在**“动手实践”**部分，我们提供了一系列精心设计的练习，旨在帮助您巩固理论知识，并深入理解降阶模型在实际应用中可能遇到的细微之处与挑战。

让我们首先从构建[降阶模型](@entry_id:754172)的基本构件——[伽辽金投影](@entry_id:145611)与[本征正交分解](@entry_id:165074)——的原理与机制开始。

## 原理与机制

本章旨在深入阐述将高维动力系统简化为低维、计算高效的降阶模型（Reduced-Order Models, ROMs）的核心原理与机制。我们将重点关注两种协同工作的关键技术：用于构造[最优基](@entry_id:752971)的**[本征正交分解](@entry_id:165074)（Proper Orthogonal Decomposition, POD）**，以及用于将原系统方程投影到低维[子空间](@entry_id:150286)的**[伽辽金投影](@entry_id:145611)（Galerkin Projection）**。本章将从基本原理出发，逐步揭示这些方法的内在机制、实际应用中的计算策略，及其固有的局限性和相应的解决方案。

### [伽辽金投影](@entry_id:145611)：[子空间](@entry_id:150286)中的最佳逼近

[降阶建模](@entry_id:177038)的核心思想是在一个精心挑选的低维[子空间](@entry_id:150286)中寻找高维系统状态的最佳逼近。[伽辽金投影](@entry_id:145611)为此提供了数学上严谨的框架，它定义了何为“最佳”。

假设我们有一个定义在某个高维[内积空间](@entry_id:271570) $V$ 中的[状态向量](@entry_id:154607) $\mathbf{x}$，我们希望在 $V$ 的一个低维[子空间](@entry_id:150286) $\mathcal{U}$ 中找到它的最佳逼近 $\widehat{\mathbf{x}}$。[伽辽金原理](@entry_id:167636)规定，最佳逼近 $\widehat{\mathbf{x}}$ 应满足一个关键条件：逼近误差向量 $\mathbf{x} - \widehat{\mathbf{x}}$ 必须与逼近[子空间](@entry_id:150286) $\mathcal{U}$ 中的**所有**向量**正交**。

这里的“正交”概念取决于空间所定义的**[内积](@entry_id:158127)**。对于[向量空间](@entry_id:151108) $\mathbb{R}^{n}$，标准欧几里得[内积](@entry_id:158127) $\langle \mathbf{u}, \mathbf{w} \rangle = \mathbf{u}^{\top} \mathbf{w}$ 只是众多可能性中的一种。在[偏微分方程](@entry_id:141332)（PDE）的[有限元离散化](@entry_id:193156)等应用中，我们经常遇到由一个对称正定（Symmetric Positive-Definite, SPD）矩阵 $M$ 定义的[加权内积](@entry_id:163877)：
$$
\langle \mathbf{u}, \mathbf{w} \rangle_{M} \equiv \mathbf{u}^{\top} M \mathbf{w}
$$
这个[内积](@entry_id:158127)通常与 underlying PDE 的物理或数学结构（如 $L^2$ 范数）直接相关。

[伽辽金条件](@entry_id:173975)因此可以形式化地写为：
$$
\langle \mathbf{x} - \widehat{\mathbf{x}}, \mathbf{v} \rangle_{M} = 0, \quad \forall \mathbf{v} \in \mathcal{U}
$$

为了求解 $\widehat{\mathbf{x}}$，我们首先需要为[子空间](@entry_id:150286) $\mathcal{U}$ 找到一组基。假设 $\mathcal{U}$ 由一组线性无关的向量 $\{\boldsymbol{\phi}_{1}, \boldsymbol{\phi}_{2}, \dots, \boldsymbol{\phi}_{r}\}$ 张成，那么 $\widehat{\mathbf{x}}$ 可以表示为这些[基向量](@entry_id:199546)的[线性组合](@entry_id:154743)：
$$
\widehat{\mathbf{x}} = \sum_{j=1}^{r} c_j \boldsymbol{\phi}_{j}
$$
其中 $c_j$ 是待定的标量系数。要满足对所有 $\mathbf{v} \in \mathcal{U}$ 的正交条件，我们只需保证误差对每个[基向量](@entry_id:199546) $\boldsymbol{\phi}_{i}$ 都正交即可。将上式代入[伽辽金条件](@entry_id:173975)，我们得到一个关于系数 $c_j$ 的线性方程组：
$$
\sum_{j=1}^{r} c_j \langle \boldsymbol{\phi}_{j}, \boldsymbol{\phi}_{i} \rangle_{M} = \langle \mathbf{x}, \boldsymbol{\phi}_{i} \rangle_{M}, \quad \text{for } i=1, \dots, r
$$
这个[方程组](@entry_id:193238)可以写成一个更紧凑的矩阵形式，称为**格拉姆系统 (Gram system)**：
$$
\mathbf{G} \mathbf{c} = \mathbf{b}
$$
其中 $\mathbf{G}$ 是[格拉姆矩阵](@entry_id:203297)，其元素为 $G_{ij} = \langle \boldsymbol{\phi}_{j}, \boldsymbol{\phi}_{i} \rangle_{M}$；$\mathbf{c}$ 是系数向量 $[c_1, \dots, c_r]^{\top}$；$\mathbf{b}$ 是右侧向量，其元素为 $b_i = \langle \mathbf{x}, \boldsymbol{\phi}_{i} \rangle_{M}$。由于[基向量](@entry_id:199546)线性无关且[内积](@entry_id:158127)正定，格拉姆矩阵 $\mathbf{G}$ 可逆，从而保证了系数 $\mathbf{c}$ 的唯一解，进而得到唯一的最佳逼近 $\widehat{\mathbf{x}}$。

**示例：非标准[内积](@entry_id:158127)下的几何投影 [@problem_id:2432132]**

为了具体理解这一过程，考虑一个在 $\mathbb{R}^3$ 空间中的投影问题。设[内积](@entry_id:158127)由 SPD 矩阵 $M = \text{diag}(2, 1, 3)$ 定义。我们要将向量 $\mathbf{x} = (3, -2, 4)^{\top}$ 投影到由[基向量](@entry_id:199546) $\boldsymbol{\phi}_1 = (1, 2, 0)^{\top}$ 和 $\boldsymbol{\phi}_2 = (0, 1, 2)^{\top}$ 张成的平面 $\mathcal{U}$ 上。

按照上述步骤，我们首先构建 $2 \times 2$ 的格拉姆系统。为此，需要计算[基向量](@entry_id:199546)之间以及目标向量与[基向量](@entry_id:199546)之间的 $M$-[内积](@entry_id:158127)：
-   $\langle \boldsymbol{\phi}_{1}, \boldsymbol{\phi}_{1} \rangle_{M} = \boldsymbol{\phi}_{1}^{\top}M\boldsymbol{\phi}_{1} = 6$
-   $\langle \boldsymbol{\phi}_{2}, \boldsymbol{\phi}_{2} \rangle_{M} = \boldsymbol{\phi}_{2}^{\top}M\boldsymbol{\phi}_{2} = 13$
-   $\langle \boldsymbol{\phi}_{1}, \boldsymbol{\phi}_{2} \rangle_{M} = \boldsymbol{\phi}_{1}^{\top}M\boldsymbol{\phi}_{2} = 2$
-   $\langle \mathbf{x}, \boldsymbol{\phi}_{1} \rangle_{M} = \mathbf{x}^{\top}M\boldsymbol{\phi}_{1} = 2$
-   $\langle \mathbf{x}, \boldsymbol{\phi}_{2} \rangle_{M} = \mathbf{x}^{\top}M\boldsymbol{\phi}_{2} = 22$

[线性系统](@entry_id:147850)为：
$$
\begin{pmatrix} 6  2 \\ 2  13 \end{pmatrix} \begin{pmatrix} c_1 \\ c_2 \end{pmatrix} = \begin{pmatrix} 2 \\ 22 \end{pmatrix}
$$
解得 $c_1 = -9/37$ 和 $c_2 = 64/37$。因此，$\mathbf{x}$ 在 $\mathcal{U}$ 上的[伽辽金投影](@entry_id:145611)为：
$$
\widehat{\mathbf{x}} = c_1 \boldsymbol{\phi}_1 + c_2 \boldsymbol{\phi}_2 = -\frac{9}{37} \begin{pmatrix} 1 \\ 2 \\ 0 \end{pmatrix} + \frac{64}{37} \begin{pmatrix} 0 \\ 1 \\ 2 \end{pmatrix} = \begin{pmatrix} -9/37 \\ 46/37 \\ 128/37 \end{pmatrix}
$$
这个例子清晰地展示了[伽辽金投影](@entry_id:145611)的几何意义和代数步骤，并强调了[内积](@entry_id:158127)在定义“正交”和“最佳”中的核心作用。

### [本征正交分解](@entry_id:165074)：构造最优降阶[子空间](@entry_id:150286)

[伽辽金投影](@entry_id:145611)告诉我们如何在**给定**的[子空间](@entry_id:150286)上进行最佳逼近，但它没有回答一个更基本的问题：如何找到**最优**的降阶[子空间](@entry_id:150286)？[本征正交分解](@entry_id:165074)（POD）正是解决这一问题的强大工具。

POD旨在从一组代表系统演化过程的“快照”（snapshots）数据中，提取出一个低维[子空间](@entry_id:150286)，该[子空间](@entry_id:150286)能够在平均意义上最好地“捕获”这组数据的能量或[方差](@entry_id:200758)。形式上，POD寻找一个 $r$ 维的正交基 $\{\boldsymbol{\phi}_i\}_{i=1}^r$，使得所有快照投影到这个基所张成的[子空间](@entry_id:150286)上的平均投影误差最小。

#### [内积](@entry_id:158127)的关键作用

“误差”和“能量”的度量完全取决于所选择的[内积](@entry_id:158127)。这个选择并非随意的，而应反映系统背后的物理或数学结构。

-   **[连续函数空间](@entry_id:150395)中的[内积](@entry_id:158127)**：对于定义在区域 $\Omega$ 上的 PDE 解，两个常见的 Hilbert 空间是 $L^2(\Omega)$ 和 $H^1(\Omega)$。
    -   $L^2(\Omega)$ [内积](@entry_id:158127)：$\langle u, v \rangle_{L^2} = \int_{\Omega} uv \, dx$。基于此[内积](@entry_id:158127)的 POD 旨在捕获解的“能量”或幅度的主要变化。
    -   $H^1(\Omega)$ [内积](@entry_id:158127)：$\langle u, v \rangle_{H^1} = \int_{\Omega} (uv + \nabla u \cdot \nabla v) \, dx$。基于此[内积](@entry_id:158127)的 POD 会同时关注解本身及其梯度的变化，这对于需要精确捕捉解的平滑性的问题至关重要。

    一个用 $H^1$ [内积](@entry_id:158127)构造的 POD 基，对于 $H^1$ 范数下的误差是最优的，但对于 $L^2$ 范数则不一定是最优的，反之亦然。因此，POD 基的最优性是相对于特定[内积](@entry_id:158127)而言的，不存在普适的[最优基](@entry_id:752971) [@problem_id:3435958]。

-   **[有限元离散化](@entry_id:193156)后的[内积](@entry_id:158127)**：当 PDE通过有限元方法（FEM）离散化后，[连续函数](@entry_id:137361) $u_h(\mathbf{x},t) = \sum_{i=1}^n x_i(t) \varphi_i(\mathbf{x})$ 由其系数向量 $\mathbf{x}(t) \in \mathbb{R}^n$ 表示。此时，连续函数空间的[内积](@entry_id:158127)会转化为系数[向量空间](@entry_id:151108)中的[加权内积](@entry_id:163877) [@problem_id:3435968]。
    -   $L^2(\Omega)$ [内积](@entry_id:158127)对应于**[质量矩阵](@entry_id:177093) $M$** 定义的[内积](@entry_id:158127)：$\langle u_h, v_h \rangle_{L^2} = \mathbf{x}^{\top} M \mathbf{y}$。
    -   $H^1(\Omega)$ [内积](@entry_id:158127)则对应于由**[质量矩阵](@entry_id:177093) $M$ 和刚度矩阵 $K$** 共同定义的[内积](@entry_id:158127)：$\langle u_h, v_h \rangle_{H^1} = \mathbf{x}^{\top}(M+K)\mathbf{y}$。

    因此，为了使离散的 POD 问题忠实地反映原始连续问题的物理意义，我们必须使用与 PDE 弱形式相对应的[加权内积](@entry_id:163877)（例如 $M$-[内积](@entry_id:158127)），而不是简单地使用方便但物理意义不明确的欧几里得[内积](@entry_id:158127)（即 $M=I$）。$M$-[内积](@entry_id:158127)是[坐标系](@entry_id:156346)无关的，它反映了[函数空间](@entry_id:143478)内在的几何结构，而欧几里得[内积](@entry_id:158127)则依赖于特定的网格和[基函数](@entry_id:170178)选择 [@problem_id:3435968]。

#### POD的数值计算

计算关于[加权内积](@entry_id:163877) $\langle \cdot, \cdot \rangle_W$（其中 $W$ 是 SPD 矩阵，如 $M$ 或 $M+K$）的 POD 基，可以通过一个巧妙的变换，回归到标准的欧几里得[内积](@entry_id:158127)下的[奇异值分解](@entry_id:138057)（SVD）。

设快照矩阵为 $X = [\mathbf{x}_1, \dots, \mathbf{x}_m] \in \mathbb{R}^{n \times m}$。我们的目标是找到一个基 $U=[\boldsymbol{\phi}_1, \dots, \boldsymbol{\phi}_r]$，使得 $\boldsymbol{\phi}_i^{\top} W \boldsymbol{\phi}_j = \delta_{ij}$，并且投影误差最小。这个问题等价于对加权后的快照矩阵 $Y = W^{1/2}X$ 进行标准 SVD [@problem_id:3435958] [@problem_id:3435999]。

具体步骤如下：
1.  计算 $W$ 的 Cholesky 分解或[对称平方](@entry_id:137676)根 $W^{1/2}$。
2.  构造加权快照矩阵 $Y = W^{1/2} X$。
3.  对 $Y$ 进行“经济型”SVD分解：$Y = \tilde{U} \Sigma V^{\top}$。其中，$\tilde{U}$ 的列是标准正交的（$\tilde{U}^{\top}\tilde{U}=I$），它们是 $Y$ 的[左奇异向量](@entry_id:751233)。
4.  将 $\tilde{U}$ 的列变换回原始空间，得到 $W$-正交的 POD 基：$\Phi = W^{-1/2} \tilde{U}$。

这样得到的基 $\Phi$ 的列向量即为所求的 POD 模态。这种方法确保了我们找到的基在物理上有意义的范数下是最优的。

### POD-Galerkin 降阶模型

将 POD 和[伽辽金投影](@entry_id:145611)结合，我们就得到了 POD-Galerkin 降阶模型。其核心步骤是：

1.  **POD阶段（离线）**：通过求解一个或多个高维模型，收集足够多的状态快照，然后使用 POD 提取出一组最优的低维基 $U_r = [\boldsymbol{\phi}_1, \dots, \boldsymbol{\phi}_r]$。
2.  **[伽辽金投影](@entry_id:145611)阶段（在线）**：将高维系统的状态近似为这组基的[线性组合](@entry_id:154743)，$x(t) \approx U_r a(t)$，其中 $a(t) \in \mathbb{R}^r$ 是新的低维坐标。然后将此近似代入原始的（半）离散控制方程（例如，$M\dot{x} = A x + f$），并要求残差与基 $U_r$ 张成的空间正交。

这导致了一个关于低维坐标 $a(t)$ 的小得多的动力系统：
$$
(U_r^{\top} M U_r) \dot{a}(t) = (U_r^{\top} A U_r) a(t) + U_r^{\top} f(t)
$$
我们称 $M_r = U_r^{\top} M U_r$ 为**降阶质量矩阵**，$A_r = U_r^{\top} A U_r$ 为**降阶刚度矩阵**，$f_r = U_r^{\top} f$ 为**降阶[载荷向量](@entry_id:635284)**。如果 POD 基是 $M$-正交的，即 $U_r^{\top} M U_r = I_r$，那么降阶[质量矩阵](@entry_id:177093)就简化为单位阵，使得系统求解更为便捷 [@problem_id:3435968]。

### 实际应用中的计算策略与挑战

#### 离线-在线计算分解

降阶模型的巨大优势在于其计算效率，这通过所谓的**离线-在线（Offline-Online）**分解得以实现。其核心思想是，将所有依赖于高维系统规模 $n$ 的昂贵计算，都在“离线”阶段一次性完成。而在“在线”阶段，当需要针对新的参数或输入求解模型时，只执行与低维规模 $r$相关的廉价计算。

这种分解的**关键**是系统的参数依赖性是**仿射的（affine）** [@problem_id:3435978]。也就是说，系统矩阵 $K(\mu)$ 和[载荷向量](@entry_id:635284) $f(\mu)$可以表示为参数依赖的标量函数与参数无关的矩阵/向量的线性组合：
$$
K(\mu) = \sum_{q=1}^{Q} \theta_q(\mu) K_q, \quad f(\mu) = \sum_{p=1}^{P} \psi_p(\mu) f_p
$$
在这种情况下，降阶矩阵 $K_r(\mu) = U_r^{\top} K(\mu) U_r$ 也能写成仿射形式：
$$
K_r(\mu) = \sum_{q=1}^{Q} \theta_q(\mu) (U_r^{\top} K_q U_r)
$$
-   **离线阶段**：我们预先计算并存储所有参数无关的降阶[分块矩阵](@entry_id:148435) $K_{r,q} = U_r^{\top} K_q U_r$。这个过程很慢，因为它涉及 $n \times n$ 矩阵的运算。
-   **在线阶段**：对于一个新的参数 $\mu$，我们只需：(1) 计算标量函数 $\theta_q(\mu)$；(2) 通过简单的标量乘法和矩阵加法组合出 $r \times r$ 的小矩阵 $K_r(\mu)$，其计算成本约为 $\mathcal{O}(Q r^2)$；(3) 求解 $r \times r$ 的线性系统。整个在线过程的计算量与高维系统的规模 $n$ **无关**，从而实现了巨大的加速。

#### [非线性](@entry_id:637147)项的挑战与超降阶

当系统中存在**[非线性](@entry_id:637147)项** $g(u)$ 时，上述高效的[离线-在线分解](@entry_id:177117)会遇到瓶颈。在计算降阶[非线性](@entry_id:637147)项 $U_r^{\top} g(U_r a(t))$ 时，我们似乎无法避免以下步骤：
1.  通过 $U_r a(t)$ 将低维坐标 $a(t)$ 重构回高维[状态向量](@entry_id:154607)（成本 $\mathcal{O}(nr)$）。
2.  对这个 $n$ 维向量逐点或逐单元地计算[非线性](@entry_id:637147)函数 $g(\cdot)$（成本至少 $\mathcal{O}(n)$）。
3.  将得到的 $n$ 维结果向量通过 $U_r^{\top}$ 投影回 $r$ 维空间（成本 $\mathcal{O}(nr)$）。

在线计算成本中对 $n$ 的依赖性破坏了[降阶模型](@entry_id:754172)的效率，这个问题被称为[非线性](@entry_id:637147)项处理中的“**维度灾难**” [@problem_id:2432086]。

**超降阶（Hyper-reduction）**技术应运而生，旨在克服这一障碍。其核心思想是，不仅要对状态变量进行降阶，也要对[非线性](@entry_id:637147)项的计算过程进行近似。**[离散经验插值法](@entry_id:748503)（Discrete Empirical Interpolation Method, DEIM）**是其中一种代表性方法 [@problem_id:3435961]。DEIM 的机制如下：
1.  **构造[非线性](@entry_id:637147)基**：除了状态快照，我们还收集[非线性](@entry_id:637147)项 $g(u)$ 的快照，并从中提取出一个低维的 POD 基 $W \in \mathbb{R}^{n \times m}$（$m \ll n$）。
2.  **插值近似**：假设[非线性](@entry_id:637147)项向量近似地位于基 $W$ 的张成空间中，即 $g(U_r a) \approx W c$，其中 $c \in \mathbb{R}^m$ 是待定系数。
3.  **确定系数**：DEIM 不求解一个大的[最小二乘问题](@entry_id:164198)，而是巧妙地选择 $m$ 个“插值点”（即向量的索引），并要求近似值在这些点上与真实值完全相等。这形成了一个 $m \times m$ 的小线性系统来求解系数 $c$。
4.  **高效计算**：最终的 DEIM 近似公式为 $g(U_r a) \approx W (P^{\top}W)^{-1} P^{\top} g(U_r a)$，其中 $P$ 是一个选取 $m$ 个插值点的“选择矩阵”。关键在于，在线计算时，我们只需要计算 $g(U_r a)$ 在 $m$ 个插值点上的值（即 $P^{\top}g(\cdot)$），而不是整个 $n$ 维向量。这使得在线计算成本只依赖于 $m$ 和 $r$，而与 $n$ 无关，从而恢复了计算效率。

此外，对于参数非仿射的系统，EIM/DEIM 也可以用来构造一个近似的仿射表达式，从而将问题转化为可以使用[离线-在线分解](@entry_id:177117)的形式 [@problem_id:3435978]。

#### 边界条件的处理

对于[非齐次边界条件](@entry_id:750645)（如非零的 Dirichlet 边界条件），直接对快照进行 POD 处理会导致 POD 基不满足[齐次边界条件](@entry_id:750371)，这会给后续的[伽辽金投影](@entry_id:145611)带来麻烦。一个标准做法是**提升法（lifting）** [@problem_id:3435999]。我们将解分解为两部分 $u = w + \ell$，其中 $\ell$ 是一个满足[非齐次边界条件](@entry_id:750645)的已知“[提升函数](@entry_id:175709)”，而 $w$ 则满足对应的[齐次边界条件](@entry_id:750371)。我们对 $w$ 的快照进行 POD，这样得到的基就自然满足[齐次边界条件](@entry_id:750371)。在[降阶模型](@entry_id:754172)中，这种分解会引入依赖于 $\ell$ 及其时间导数 $\dot{\ell}$ 的额外项，使降阶系统变为非齐次的。

### 局限性与高级主题

虽然 POD-Galerkin 方法功能强大，但理解其局限性对于避免误用和进行深入研究至关重要。

#### [能量截断](@entry_id:177594)准则的陷阱

在实践中，我们通常通过一个**[能量截断](@entry_id:177594)准则**来选择 POD 基的维度 $r$。我们计算每个模态捕获的能量（由 POD 过程中的[特征值](@entry_id:154894) $\lambda_i$ 或奇异值 $\sigma_i^2$ 给出），然[后选择](@entry_id:154665)最小的 $r$ 使得捕获的累积能量占总能量的比例超过一个阈值 $\eta$（如 $99.9\%$） [@problem_id:3435995]：
$$
\frac{\sum_{i=1}^r \lambda_i}{\sum_{i=1}^{\text{rank}} \lambda_i} \ge \eta
$$
这个准则虽然直观，但有重大局限性：
1.  **仅保证样本内精度**：高能量捕获率仅表示 POD 基能够很好地**重构**用于生成它的那组**训练快照**。它**不提供任何关于模型对样本外（out-of-sample）**新参数或新输入的**预测精度**的保证 [@problem_id:3435995] [@problem_id:3435987]。一个在训练集上看似完美的模型，在预测新情况时可能会产生巨大误差。
2.  **对[非正规系统](@entry_id:270295)的脆弱性**：在许多物理系统（尤其是[流体力学](@entry_id:136788)）中，系统的演化算子是**非正规的（non-normal）**。这意味着系统的短期动态或稳定性可能由那些能量很低、但在 POD 排序中被忽略的模态所主导。这些系统可能表现出显著的瞬态增长，而基于能量的 POD 会错过这些关键的动力学行为，导致模型预测失真 [@problem_id:3435995]。

#### 稳定性问题与 [Petrov-Galerkin](@entry_id:174072) 方法

标准的[伽辽金投影](@entry_id:145611)（即测试空间与试验空间相同）并非总能保证[降阶模型](@entry_id:754172)的稳定性，即便原始的全维模型是稳定的。

-   对于**对称、强制性（coercive）**的系统（如标准的椭圆或抛物线问题），稳定性是自动继承的。降阶问题仍然是强制性的，因此是稳定的 [@problem_id:3435972]。
-   对于**非对称或不定号**的系统（如[对流](@entry_id:141806)占优问题、波动问题或[鞍点问题](@entry_id:174221)如 Stokes 方程），[伽辽金投影](@entry_id:145611)可能会破坏稳定性。其根本原因在于，保证连续问题稳定性的 [inf-sup 条件](@entry_id:174538)，在投影到低维[子空间](@entry_id:150286)后可能不再满足。POD 基虽然对于逼近解是最优的，但它不保证能稳定地逼近算子本身 [@problem_id:3435972]。

为了解决稳定性问题，人们引入了**[Petrov-Galerkin](@entry_id:174072)**方法，其核心思想是使用与试验空间 $V_r$ **不同**的测试空间 $W_r$。通过精心构造测试空间，可以强制保证降阶模型的稳定性。例如：
-   对于一般的非对称问题，可以选择一个与算子 $A$ 相关的测试空间 $W_r = A V_r$，这导致了最小残差（minimal residual）类方法，能够保证稳定性 [@problem_id:3435972]。
-   对于像 Stokes 方程这样的[鞍点问题](@entry_id:174221)，标准 POD-Galerkin 方法通常是不稳定的。一种有效的稳定化策略是向速度试验空间中添加所谓的“**supremizer**”函数来丰富测试空间，这些函数是为保证速度-压力耦合的 [inf-sup 条件](@entry_id:174538)而专门构造的 [@problem_id:3435972]。

#### [后验误差估计](@entry_id:167288)

既然我们无法先验地保证 ROM 的预测精度，那么如何在不求解昂贵的全维模型的情况下，评估一个 ROM 在线预测结果的可信度呢？**[后验误差估计](@entry_id:167288)（a posteriori error estimation）**提供了答案。

其关键工具是 ROM 解的**残差（residual）**。对于一个 ROM 解 $x_{\text{ROM}}$，其代入全维方程后产生的残差为：
$$
r(t) = M \dot{x}_{\text{ROM}}(t) - A x_{\text{ROM}}(t) - f(t)
$$
根据[伽辽金投影](@entry_id:145611)的定义，这个残差向量 $r(t)$ 与降阶[子空间](@entry_id:150286) $\text{span}(U_k)$ 是正交的。然而，它本身通常不是[零向量](@entry_id:156189)，其范数的大小反映了 ROM 解偏离全维解的程度 [@problem_id:3435987]。

对于稳定系统，可以从理论上证明，真实[误差范数](@entry_id:176398) $\|x - x_{\text{ROM}}\|$ 被残差的某个范数（通常是[对偶范数](@entry_id:200340)）所界定。因此，通过在线计算[残差范数](@entry_id:754273)，我们可以得到一个关于真实误差大小的可计算的、可靠的指示器。如果[残差范数](@entry_id:754273)很小，我们可以相信 ROM 的预测；如果它很大，则表明模型在该参数点下是不可信的 [@problem_id:3435987]。这为 ROM 的可靠应用提供了必不可少的“安全网”。