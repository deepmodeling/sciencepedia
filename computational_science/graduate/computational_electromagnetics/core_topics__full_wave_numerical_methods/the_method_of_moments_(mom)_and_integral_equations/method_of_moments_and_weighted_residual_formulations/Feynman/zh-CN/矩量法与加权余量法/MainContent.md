## 引言
在[计算电磁学](@keyword=numerical_electromagnetics|lang=zh-CN|style=Feynman)的广阔领域中，精确预测[电磁波](@keyword=electromagnetic_wave|lang=zh-CN|style=Feynman)与复杂物体（如天线、飞机或人体组织）的相互作用是一项核心挑战。虽然[麦克斯韦方程组](@keyword=maxwell_s_equations|lang=zh-CN|style=Feynman)为我们提供了完美的理论描述，但直接求解它们对于任意形状的物体几乎是不可能的。[积分方程方法](@keyword=integral_equation_methods|lang=zh-CN|style=Feynman)提供了一条优雅的途径，它将问题从整个空间简化到物体的表面或体积上，但随之而来的是如何高效、准确地求解这些复杂的[积分方程](@keyword=integral_equations|lang=zh-CN|style=Feynman)。这正是[矩量法](@keyword=moment_methods|lang=zh-CN|style=Feynman)（Method of Moments, MoM）及其更普适的框架——[加权残差法](@keyword=weighted_residuals_method|lang=zh-CN|style=Feynman)（Weighted Residual Method）——发挥关键作用的地方，它已成为现代[电磁仿真](@keyword=electromagnetic_simulation|lang=zh-CN|style=Feynman)不可或缺的基石。

然而，仅仅了解其基本概念是远远不够的。工程师和科学家们在实践中常常面临诸如数值不稳定、[奇异积分](@keyword=singular_integrals|lang=zh-CN|style=Feynman)、计算成本过高等棘手问题。本文旨在填补理论与实践之间的鸿沟，系统性地揭示[矩量法](@keyword=moment_methods|lang=zh-CN|style=Feynman)的深层机制与高级应用。

在接下来的内容中，我们将分三步深入探索这一强大的数值工具。在“原理与机制”一章中，我们将从最基本的近似思想出发，揭示如何通过[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)和检验函数将一个连续的物理问题转化为一个有限维的[矩阵方程](@keyword=matrix_equations|lang=zh-CN|style=Feynman)，并直面奇异性与稳定性这两大核心挑战。接着，在“应用与交叉学科联系”一章，我们将领略[矩量法](@keyword=moment_methods|lang=zh-CN|style=Feynman)在解决实际工程问题中的威力，从克服内部谐振等“顽疾”，到构建连接不同物理模型的混合方法。最后，“动手实践”部分将通过精心设计的问题，帮助您将理论知识转化为解决实际问题的能力。

让我们首先深入其核心，探究[矩量法](@keyword=moment_methods|lang=zh-CN|style=Feynman)背后的基本原理与精妙机制。

## 原理与机制

想象一下，你想要精确描绘一座复杂雕塑的表面。你该如何着手？你无法用无限个尘埃微粒来描述它——那将是一个无穷无尽的任务。一个更聪明的办法是使用一组有限的、形状简单的“积木”，比如乐高砖块或粘土块，来搭建一个近似的模型。计算科学，特别是我们在此探讨的[矩量法](@keyword=moment_methods|lang=zh-CN|style=Feynman)，其核心思想与此如出一辙。我们不是去求解一个物理量（比如物体表面的电流）在每一点的精确值——这是一个无限维的问题——而是用一组有限的、简单的“构建模块”来近似它。

### 近似的艺术：从无限到有限

在电磁学中，当[电磁波](@keyword=electromagnetic_wave|lang=zh-CN|style=Feynman)撞击一个物体（比如一架飞机或一个天线）时，会在其表面感应出电流。这个电流的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)是连续的，包含了无限多的信息。为了让计算机能够处理这个问题，我们必须将其“有限化”。我们将这个未知的、复杂的电[流函数](@keyword=stream_function|lang=zh-CN|style=Feynman) $\boldsymbol{J}$，近似地表示为一组预先选定的、更简单的**[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)**（basis functions）$\boldsymbol{v}_j$ 的线性组合：

$$
\boldsymbol{J}(\boldsymbol{r}) \approx \boldsymbol{J}_N(\boldsymbol{r}) = \sum_{j=1}^{N} a_j \boldsymbol{v}_j(\boldsymbol{r})
$$

这里的 $\boldsymbol{v}_j$ 就是我们的“积木”，它们是已知的、定义在物体表面上的[简单函数](@keyword=simple_functions|lang=zh-CN|style=Feynman)。而 $a_j$ 则是未知的系数，代表了我们需要使用“第 $j$ 块积木”的数量。如此一来，求解一个[连续函数](@keyword=continuous_function|lang=zh-CN|style=Feynman) $\boldsymbol{J}(\boldsymbol{r})$ 的无穷难题，就转化为了求解 $N$ 个未知系数 $a_j$ 的有限问题。

那么，这些“积木”长什么样呢？在计算电磁学中，一个最著名也最成功的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)是**Rao-Wilton-Glisson (RWG) [基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)** [@problem_id:3330355]。想象我们将物体的表面剖分成许多小的三角形网格。一个 RWG [基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)与网格中的一条公共边相关联。它巧妙地描述了一股电流从这条边相邻的一个三角形 $T^+$ 流向另一个三角形 $T^-$ 的过程。这个函数在其他任何地方都为零，仅在这一对三角形上是分段线性的。它的一个优美特性是，其表面散度——即电流的“源”或“汇”，对应于[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的积累——是两个大小相等、符号相反的常数，分别位于两个三角形的内部。这种简洁而物理意义明确的构造，使得 RWG [基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)成为将抽象理论付诸实践的完美工具。

### [加权残差法](@keyword=weighted_residuals_method|lang=zh-CN|style=Feynman)：让误差“安分守己”

用有限的积木去搭建复杂的雕塑，总会存在误差。同样，当我们将近似解 $\boldsymbol{J}_N$ 代入到描述物理规律的原始方程（我们用一个抽象的算子 $\mathcal{L}$ 表示，即 $\mathcal{L}(\boldsymbol{J}) = \boldsymbol{f}$）中时，方程通常不会被完美满足。我们会得到一个**残差**（residual），或者说误差函数：

$$
\boldsymbol{r} = \mathcal{L}(\boldsymbol{J}_N) - \boldsymbol{f}
$$

这个残差 $\boldsymbol{r}$ 在大部分地方都不是零。我们无法让它在每一点都为零，因为那就意味着我们找到了精确解。那么，我们该如何处理这个误差呢？

**[加权残差法](@keyword=weighted_residuals_method|lang=zh-CN|style=Feynman)**（Weighted Residual Method）提供了一个优雅的答案。它的核心思想是：我们不要求误差本身处处为零，而是要求它在某种“平均”意义下为零。具体来说，我们选取另一组被称为**[检验函数](@keyword=test_functions|lang=zh-CN|style=Feynman)**（testing functions）或权重函数（weighting functions）的函数 $\boldsymbol{w}_i$，并强制要求残差 $\boldsymbol{r}$ 与每一个[检验函数](@keyword=test_functions|lang=zh-CN|style=Feynman)都**正交**（orthogonal）[@problem_id:3330359]。

在数学上，两个[函数的正交性](@keyword=orthogonality_of_functions|lang=zh-CN|style=Feynman)通过它们的**[内积](@keyword=interior_product|lang=zh-CN|style=Feynman)**（inner product）来定义，记作 $\langle \boldsymbol{w}_i, \boldsymbol{r} \rangle = 0$。[内积](@keyword=interior_product|lang=zh-CN|style=Feynman)是一种广义的度量，衡量一个函数在另一个函数上的“投影”或“重叠”程度。要求 $\langle \boldsymbol{w}_i, \boldsymbol{r} \rangle = 0$ 就好比是说：“从函数 $\boldsymbol{w}_i$ 的‘视角’看，误差 $\boldsymbol{r}$ 是不可见的。” 如果我们为每一个未知的系数 $a_j$ 都选取一个独立的检验函数 $\boldsymbol{w}_i$ 并施加这个正交性要求，我们就能得到一个包含 $N$ 个方程的[方程组](@keyword=simultaneous_equations|lang=zh-CN|style=Feynman)，足以确定所有的 $N$ 个未知系数。

这个过程出奇地直接。将近似解代入，我们得到：

$$
\left\langle \boldsymbol{w}_i, \mathcal{L}\left(\sum_{j=1}^{N} a_j \boldsymbol{v}_j\right) - \boldsymbol{f} \right\rangle = 0
$$

利用算子 $\mathcal{L}$ 的线性和[内积](@keyword=interior_product|lang=zh-CN|style=Feynman)的性质，上式可以重新[排列](@keyword=permutation|lang=zh-CN|style=Feynman)为我们所熟悉的线性方程组形式 $\boldsymbol{Z}\boldsymbol{a} = \boldsymbol{b}$，其中：

$$
Z_{ij} = \langle \boldsymbol{w}_i, \mathcal{L}(\boldsymbol{v}_j) \rangle \quad \text{和} \quad b_i = \langle \boldsymbol{w}_i, \boldsymbol{f} \rangle
$$

就这样，一个复杂的、定义在[连续函数空间](@keyword=space_of_continuous_functions|lang=zh-CN|style=Feynman)中的物理问题，被转化成了一个计算机可以高效求解的、有限维的线性代数问题。这正是**[矩量法](@keyword=moment_methods|lang=zh-CN|style=Feynman)**（Method of Moments）的精髓，它本质上是[加权残差法](@keyword=weighted_residuals_method|lang=zh-CN|style=Feynman)在电磁[积分方程](@keyword=integral_equations|lang=zh-CN|style=Feynman)领域的一个杰出应用。

### 方法的“流派”：Galerkin、[配置点](@keyword=collocation_points|lang=zh-CN|style=Feynman)法及其他

[加权残差法](@keyword=weighted_residuals_method|lang=zh-CN|style=Feynman)提供了一个通用的框架，而具体的“流派”则取决于我们如何[选择检验](@keyword=test_for_selection|lang=zh-CN|style=Feynman)函数 $\boldsymbol{w}_i$。

*   **Galerkin 法**：最自然、最常用的一种选择是让检验函数与[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)完全相同，即 $\boldsymbol{w}_i = \boldsymbol{v}_i$。这种方法被称为 **Galerkin 法**（或 Bubnov-Galerkin 法）[@problem_id:3616481]。当物理问题本身具有某些对称性时（例如，由自伴算子描述），Galerkin 法通常能生成一个对称的矩阵 $\boldsymbol{Z}$，这在计算上十分有利。

*   **点[配置法](@keyword=collocation_methods|lang=zh-CN|style=Feynman)**（Point Collocation）：另一种看似简单直接的选择是，让[检验函数](@keyword=test_functions|lang=zh-CN|style=Feynman)成为在空间中某些特定点上无限尖锐的“脉冲”，即**狄拉克-德尔塔函数**（Dirac delta functions），$\boldsymbol{w}_i = \boldsymbol{\delta}(\boldsymbol{r} - \boldsymbol{r}_i)$ [@problem_id:3330359]。在这种情况下，[内积](@keyword=interior_product|lang=zh-CN|style=Feynman) $\langle \boldsymbol{\delta}(\boldsymbol{r} - \boldsymbol{r}_i), \boldsymbol{r} \rangle$ 就简化为在 $\boldsymbol{r}_i$ 点处对残差的取值，即 $\boldsymbol{r}(\boldsymbol{r}_i)$。于是，[正交性条件](@keyword=orthogonality_condition|lang=zh-CN|style=Feynman)就变成了 $\boldsymbol{r}(\boldsymbol{r}_i) = 0$。这意味着我们强迫误差在选定的一系列离散点（称为[配置点](@keyword=collocation_points|lang=zh-CN|style=Feynman)）上精确为零。这种方法直观易懂，但在稳定性和精度方面可能不如其他方法。

*   **[Petrov-Galerkin](@keyword=petrov_galerkin|lang=zh-CN|style=Feynman) 法**：当检验函数与[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)不同（且不是狄拉克函数）时，我们称之为 **[Petrov-Galerkin](@keyword=petrov_galerkin|lang=zh-CN|style=Feynman) 法**。你可能会问，为什么我们需要“舍近求远”，不使用最简单的 Galerkin 法呢？事实证明，在处理某些复杂的物理问题（如[电场积分方程](@keyword=electric_field_integral_equation|lang=zh-CN|style=Feynman)）时，Galerkin 法会遭遇稳定性瓶颈。而精心设计的 [Petrov-Galerkin](@keyword=petrov_galerkin|lang=zh-CN|style=Feynman) 法，通过为特定的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)“量身定做”一套不同的[检验函数](@keyword=test_functions|lang=zh-CN|style=Feynman)，能够克服这些困难，获得稳定而精确的解。这将在后面变得至关重要。

### 波的语言：[积分方程](@keyword=integral_equations|lang=zh-CN|style=Feynman)与格林函数

对于发生在无界空间中的波散射问题（例如雷达波探测目标），直接对整个空间中的[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)（如[麦克斯韦方程组](@keyword=maxwell_s_equations|lang=zh-CN|style=Feynman)）进行离散化，会面临一个棘手的问题：如何处理无限大的计算区域？一个更强大的工具是**积分方程**（Integral Equation）。它的巨大优势在于，方程本身只定义在散射物体的表面上，从而将一个三维空间问题降维到了二维表面问题。

构建积分方程的“魔法配方”是**格林函数**（Green's function）。你可以将[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)想象为宇宙对一个无穷小点源的响应 [@problem_id:3330406]。对于描述[时谐波](@keyword=time_harmonic_waves|lang=zh-CN|style=Feynman)动的[亥姆霍兹方程](@keyword=helmholtz_equation|lang=zh-CN|style=Feynman)，其三维自由空间格林函数形式优美而简洁：

$$
g(\boldsymbol{r}, \boldsymbol{r}') = \frac{\exp(ik|\boldsymbol{r}-\boldsymbol{r}'|)}{4\pi|\boldsymbol{r}-\boldsymbol{r}'|}
$$

这个公式描述了一个从源点 $\boldsymbol{r}'$ 发出的、向外传播的[球面波](@keyword=spherical_waves|lang=zh-CN|style=Feynman)。请特别注意指数项 $\exp(ikR)$（其中 $R=|\boldsymbol{r}-\boldsymbol{r}'|$）。它代表着能量从源头向无穷远处辐射的**出射波**。这一物理要求被严格地表述为**[索末菲辐射条件](@keyword=sommerfeld_radiation_condition|lang=zh-CN|style=Feynman)**（Sommerfeld radiation condition）[@problem_id:3330414]。通过在我们的[积分方程](@keyword=integral_equations|lang=zh-CN|style=Feynman)中采用这个特定的格林函数，我们就自动地、隐式地将散射波必须向外传播这一物理规律融入了数学模型中，无需再为无穷远处的边界条件而烦恼。

利用[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)，我们可以为未知的[表面电流](@keyword=surface_current|lang=zh-CN|style=Feynman) $\boldsymbol{J}$ 建立方程。最著名的两个是**[电场积分方程](@keyword=electric_field_integral_equation|lang=zh-CN|style=Feynman)（EFIE）**和**[磁场积分方程](@keyword=magnetic_field_integral_equation|lang=zh-CN|style=Feynman)（MFIE）**[@problem_id:3330375]。

*   **EFIE** 是一种**第一类 Fredholm [积分方程](@keyword=integral_equations|lang=zh-CN|style=Feynman)**。未知量 $\boldsymbol{J}$ 完全“埋藏”在[积分算子](@keyword=integrator_operator|lang=zh-CN|style=Feynman) $\mathcal{T}$ 内部，形式为 $\mathcal{T}[\boldsymbol{J}] = \boldsymbol{V}$。它在物理上非常通用，但其数学性质也更为“桀骜不驯”，尤其是在低频时会变得不稳定。

*   **MFIE** 是一种**第二类 Fredholm [积分方程](@keyword=integral_equations|lang=zh-CN|style=Feynman)**。未知量同时出现在积分内外，形式为 $\frac{1}{2}\boldsymbol{J} + \mathcal{K}[\boldsymbol{J}] = \boldsymbol{V}$。这个显式出现的“单位算子”项 $\frac{1}{2}\boldsymbol{J}$ 极大地改善了方程的数学性质，使得最终的矩阵通常是“[对角占优](@keyword=diagonally_dominant|lang=zh-CN|style=Feynman)”的，从而更容易求解。然而，MFIE 也有其“阿喀琉斯之踵”：它会在对应于物体内部空腔谐振的特定频率上失效。这些所谓的**内部谐振**是纯粹的数学“幽灵”，在真实物理世界中并不存在 [@problem_id:3330375] [@problem_id:3330414]。这提醒我们，数学模型虽然强大，但有时也会带来一些需要我们用更深的洞察力去甄别和克服的“人造”问题。

### 魔鬼在细节中：奇异性与稳定性

理论框架看似完美，但在将其转化为可靠的计算机代码时，我们会遇到两个“拦路虎”：奇异性和稳定性。

#### 驯服奇异性的“野兽”

在计算矩阵元素 $Z_{ij} = \langle \boldsymbol{w}_i, \mathcal{L}(\boldsymbol{v}_j) \rangle$ 时，我们需要计算涉及格林函数的双重积分。当源点和观测点靠得非常近（$R \to 0$）时，[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)会“爆炸”。$1/R$ 这种行为被称为**弱奇异性**。而格林函数的导数则更加“狂野”：其梯度表现为 $1/R^2$ 的**强奇异性**，[二阶导数](@keyword=second_derivative|lang=zh-CN|style=Feynman)（Hessian 矩阵）更是高达 $1/R^3$ 的**超奇异性**（hypersingularity）[@problem_id:3330406] [@problem_id:3330347]。如果直接将这些[奇异函数](@keyword=singular_functions|lang=zh-CN|style=Feynman)交给标准的[数值积分](@keyword=numerical_quadrature|lang=zh-CN|style=Feynman)程序，结果将是灾难性的。

幸运的是，物理学家和数学家们已经发展出了一套精妙的“驯兽”技巧：

*   **[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)（[分部积分](@keyword=integration_by_parts|lang=zh-CN|style=Feynman)）**：正如之前提到的，通过一个类似于分部积分的数学恒等式（高斯散度定理的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)版本），我们可以巧妙地将导数从奇异的格林函数身上“转移”到光滑的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)和[检验函数](@keyword=test_functions|lang=zh-CN|style=Feynman)上。这一步操作至关重要，它将强奇异和超奇异的难题，转化为一个只需处理弱奇异性的、更容易处理的问题 [@problem_id:3330347]。

*   **奇异性减除**（Singularity Subtraction）：对于剩下的 $1/R$ 弱奇异性，我们可以采用“先减后加”的策略。我们将奇异项分解为两部分：一部分是纯粹的静态（$k=0$）奇异核 $1/(4\pi R)$，这部分的积分可以通过复杂的解析公式精确计算；另一部分是原始核与静态核的差值，这个差值函数在 $R=0$ 处是光滑且有界的，可以用标准的[数值积分方法](@keyword=numerical_integration_methods|lang=zh-CN|style=Feynman)轻松搞定 [@problem_id:3330347]。

*   **Duffy 变换**：这是另一种充满几何巧思的方法。它通过一个[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)的坐标变换，将原本在[尖点](@keyword=cusps|lang=zh-CN|style=Feynman)或边上存在奇异性的积分区域，映射到一个规则的正方形或立方体上。这个变换的[雅可比行列式](@keyword=jacobian_determinant|lang=zh-CN|style=Feynman)（Jacobian）恰好可以抵消掉 $1/R$ 形式的奇异性，使得变换后的被积函数变得平滑，从而可以进行高精度[数值积分](@keyword=numerical_quadrature|lang=zh-CN|style=Feynman) [@problem_id:3330347]。

#### 追求稳定性的“圣杯”

即便我们精确地计算了所有积分，得到的解就一定可靠吗？答案是否定的。[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)和[检验函数](@keyword=test_functions|lang=zh-CN|style=Feynman)的选择对解的稳定性起着决定性作用。

*   **[inf-sup 条件](@keyword=inf_sup_condition|lang=zh-CN|style=Feynman)**：对于像 EFIE 这样非强制（non-coercive）的问题，其数值稳定性的“试金石”是所谓的 **[inf-sup 条件](@keyword=inf_sup_condition|lang=zh-CN|style=Feynman)**（或 Ladyzhenskaya–Babuška–Brezzi, LBB 条件）[@problem_id:3330357]。这个条件可以通过一个常数 $\beta_h$ 来量化，它衡量了[检验函数](@keyword=test_functions|lang=zh-CN|style=Feynman)空间“洞察”或“感知”基[函数空间](@keyword=function_spaces|lang=zh-CN|style=Feynman)中每一个非零函数的能力。如果 $\beta_h$ 很小或趋于零，就意味着存在某些[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)组合，它们几乎不与任何[检验函数](@keyword=test_functions|lang=zh-CN|style=Feynman)发生作用，就像是检验函数们的“盲点”。这样的系统将极不稳定，微小的扰动都可能导致解的巨大偏差。从算子的角度看，inf-sup 常数 $\beta_h$ 正是系统算子的最小[奇异值](@keyword=singular_values|lang=zh-CN|style=Feynman) [@problem_id:3330357]。

*   **不稳定的 Galerkin 法**：令人沮丧的是，最直观的 Galerkin 法——使用 RWG 函数同时作为[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)和检验函数——恰恰无法满足一个对网格和频率一致成立的 [inf-sup 条件](@keyword=inf_sup_condition|lang=zh-CN|style=Feynman)。这导致了臭名昭著的**低频崩溃**和**密网格崩溃**问题 [@problem_id:3330357]。

*   **稳定的 [Petrov-Galerkin](@keyword=petrov_galerkin|lang=zh-CN|style=Feynman) 法**：这正是 [Petrov-Galerkin](@keyword=petrov_galerkin|lang=zh-CN|style=Feynman) 法大放异彩的地方。现代计算电磁学的一大突破，就是发现了与 RWG [基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)“天生一对”的检验函数——**Buffa-Christiansen (BC) 函数**。RWG/BC 这一对基/检验函数组合被严格证明能够满足一个强健的、不随网格加密或频率降低而退化的 [inf-sup 条件](@keyword=inf_sup_condition|lang=zh-CN|style=Feynman) [@problem_id:3330357]。这一成就的背后，是[泛函分析](@keyword=functional_analysis|lang=zh-CN|style=Feynman)的深刻理论（例如，在诸如 $H^{-1/2}(\text{div})$ 和 $H^{-1/2}(\text{curl})$ 这样的分数阶 Sobolev 空间中分析算子性质 [@problem_id:3330378]），它为解决一个困扰多年的工程难题提供了坚实的数学基础。

*   **[内积](@keyword=interior_product|lang=zh-CN|style=Feynman)的微妙角色**：甚至我们定义“正交性”所用的[内积](@keyword=interior_product|lang=zh-CN|style=Feynman) $\langle \cdot, \cdot \rangle$ 本身，也对结果有影响。标准的 $L^2$ [内积](@keyword=interior_product|lang=zh-CN|style=Feynman)（即函数的逐点乘积再积分）虽然简单，但未必是最佳选择。有时，选择一个与物理量（如功率）相关联的[加权内积](@keyword=weighted_inner_product|lang=zh-CN|style=Feynman)，可以改善矩阵的条件数，并使得“将误差投影为零”这一操作具有更清晰的物理意义 [@problem_id:3330351]。

从近似思想到加权残差，从[积分方程](@keyword=integral_equations|lang=zh-CN|style=Feynman)到格林函数，再到与奇异性和稳定性的“搏斗”，[矩量法](@keyword=moment_methods|lang=zh-CN|style=Feynman)的发展历程展现了科学与工程的完美结合。它始于一个简单的想法，却引出了一系列深刻的数学问题和精妙的解决方案，最终成为现代[电磁仿真](@keyword=electromagnetic_simulation|lang=zh-CN|style=Feynman)不可或缺的强大工具。