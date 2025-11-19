## 引言
在现代科学与工程中，从结构力学到[流体动力学](@entry_id:136788)，许多复杂物理系统都可以通过高保真度的数学模型来描述，例如由[有限元法](@entry_id:749389)产生的包含数百万自由度的[方程组](@entry_id:193238)。尽管这些[全阶模型](@entry_id:171001)（FOM）极为精确，但其高昂的计算成本往往限制了它们在需要多次或实时仿真的场景中的应用，如优化设计、[不确定性量化](@entry_id:138597)和[实时控制](@entry_id:754131)。

降阶建模（Reduced-Order Modeling, ROM）应运而生，旨在解决这一根本性挑战。其核心思想在于，复杂系统在高维[状态空间](@entry_id:177074)中的动态行为，通常被限制在一个低维的[流形](@entry_id:153038)上。降阶建模通过系统地构建一个维度极小但能精确捕捉系统关键特性的“代理”模型，从而在保证可接受精度的前提下，将计算效率提升数个[数量级](@entry_id:264888)。

本文旨在为读者提供一个关于降阶建模的全面而深入的理解。我们将从其基本原理出发，逐步深入到高级技术和前沿应用。在接下来的章节中，您将学习到：

*   **原理与机制**：我们将深入剖析降阶建模的核心思想——[投影法](@entry_id:144836)，探讨如何构建高效的降阶基（如[本征正交分解](@entry_id:165074)POD），并介绍超降阶等技术如何克服[非线性系统](@entry_id:168347)带来的计算瓶颈。
*   **应用与交叉学科联系**：我们将展示降阶建模如何在固体力学、控制理论、数据科学等多个领域中发挥关键作用，将抽象的理论与具体的工程问题联系起来。
*   **Hands-On Practices**：通过一系列精心设计的实践案例，您将有机会亲手实现从数据中构建基、生成降阶模型到处理[非线性](@entry_id:637147)问题的完整流程，巩固理论知识。

通过本次学习，您将掌握一套强大的工具，以应对日益复杂的模拟与分析挑战。让我们首先进入第一章，探索降阶建[模的基](@entry_id:156416)石——其核心原理与机制。

## 原理与机制

本章旨在深入探讨降阶建模 (Reduced-Order Modeling, ROM) 的核心原理与关键机制。我们将从[降阶模型](@entry_id:754172)的基本构建方法——[投影法](@entry_id:144836)——出发，系统地阐述如何将一个高维度的复杂系统转化为一个低维度的、计算上易于处理的等效系统。随后，我们将探讨如何生成高效的降阶基，这是决定模型精度的关键。最后，我们将剖析在处理[非线性](@entry_id:637147)和参数化问题时遇到的计算瓶颈，并介绍相应的先进技术，包括超降阶和专门为保证稳定性而设计的投影方法。

### 核心思想：[投影法](@entry_id:144836)

几乎所有工程和物理系统都可以通过一组控制方程来描述，在经过有限元等方法进行[空间离散化](@entry_id:172158)后，这些方程通常可以写成一个大规模的代数或[常微分方程组](@entry_id:266774)。我们将其抽象地表示为一个残差方程：

$ \boldsymbol{R}(\boldsymbol{u}, \dot{\boldsymbol{u}}, \ddot{\boldsymbol{u}}; t, \boldsymbol{\mu}) = \boldsymbol{0} $

其中，$ \boldsymbol{u} \in \mathbb{R}^{N} $ 是系统状态向量（例如，节点位移），$ N $ 是系统的自由度总数，通常非常巨大。$ t $ 代表时间，$ \boldsymbol{\mu} $ 代表系统参数（如材料属性、几何尺寸或载荷大小）。求解这个高维度的[全阶模型](@entry_id:171001) (Full-Order Model, FOM) 在计算上可能极为昂贵，尤其是在需要进行多次仿真（例如，在优化、[不确定性量化](@entry_id:138597)或控制设计中）的场景下。

降阶建模的核心思想在于，尽管状态向量 $ \boldsymbol{u} $ 存在于一个高维空间 $ \mathbb{R}^{N} $ 中，但对于给定的参数和激励范围，其演化轨迹实际上被限制在一个维度远低于 $ N $ 的低维[流形](@entry_id:153038)上。如果我们能找到一个能够有效逼近这个[流形](@entry_id:153038)的低维[线性子空间](@entry_id:151815)，我们就可以极大地简化问题。

这一思想通过一个核心的**近似假设 (ansatz)** 来实现：

$ \boldsymbol{u}(t) \approx \boldsymbol{V} \boldsymbol{q}(t) $

这里，$ \boldsymbol{V} \in \mathbb{R}^{N \times r} $ 是一个列满秩的矩阵，其列向量 $ \{\boldsymbol{v}_1, \boldsymbol{v}_2, \dots, \boldsymbol{v}_r\} $ 构成了一个**降阶基 (reduced basis)**，张成一个 $ r $ 维的[子空间](@entry_id:150286)（其中 $ r \ll N $）。向量 $ \boldsymbol{q}(t) \in \mathbb{R}^{r} $ 则是新的、低维的**[广义坐标](@entry_id:156576)**或**降阶坐标**。这个 ansatz 的本质是将求解高维状态 $ \boldsymbol{u} $ 的问题，转化为求解低维坐标 $ \boldsymbol{q} $ 的问题。

然而，我们如何确定 $ \boldsymbol{q}(t) $ 的演化规律呢？将上述近似代入原始残差方程，通常无法使其恰好为零。我们得到的将是一个非零的近似残差：

$ \boldsymbol{R}_{\text{approx}} = \boldsymbol{R}(\boldsymbol{V}\boldsymbol{q}, \boldsymbol{V}\dot{\boldsymbol{q}}, \boldsymbol{V}\ddot{\boldsymbol{q}}; t, \boldsymbol{\mu}) \neq \boldsymbol{0} $

为了得到一个关于 $ \boldsymbol{q} $ 的封闭[方程组](@entry_id:193238)，我们必须施加一个额外的准则。**[投影法](@entry_id:144836) (Projection Methods)** 提供了一个系统性的框架。其核心思想是，虽然我们不能让近似残差在整个 $ \mathbb{R}^{N} $ 空间中为零，但我们可以要求它在一个精心挑选的 $ r $ 维**测试[子空间](@entry_id:150286) (test subspace)** 上为零，即要求残差与测试[子空间](@entry_id:150286)中的所有向量正交。

设测试[子空间](@entry_id:150286)由一个基矩阵 $ \boldsymbol{W} \in \mathbb{R}^{N \times r} $ 的列向量张成。[正交性条件](@entry_id:168905)可以表示为：

$ \boldsymbol{W}^{T} \boldsymbol{R}_{\text{approx}} = \boldsymbol{0} $

这就是所谓的**[彼得罗夫-伽辽金](@entry_id:174072)投影 ([Petrov-Galerkin](@entry_id:174072) Projection)**。当测试[子空间](@entry_id:150286)与试验[子空间](@entry_id:150286)相同时，即 $ \boldsymbol{W} = \boldsymbol{V} $，该方法特化为**[伽辽金投影](@entry_id:145611) (Galerkin Projection)**，也称为[布勃诺夫-伽辽金方法](@entry_id:747000)。

让我们以一个典型的线性[结构动力学](@entry_id:172684)问题为例来说明这个过程 [@problem_id:2679849]。其[全阶模型](@entry_id:171001)为：

$ \boldsymbol{M} \ddot{\boldsymbol{u}}(t) + \boldsymbol{C} \dot{\boldsymbol{u}}(t) + \boldsymbol{K} \boldsymbol{u}(t) = \boldsymbol{f}(t) $

其中 $ \boldsymbol{M} $、$ \boldsymbol{C} $ 和 $ \boldsymbol{K} $ 分别是质量、阻尼和刚度矩阵。其残差为 $ \boldsymbol{R} = \boldsymbol{M} \ddot{\boldsymbol{u}} + \boldsymbol{C} \dot{\boldsymbol{u}} + \boldsymbol{K} \boldsymbol{u} - \boldsymbol{f} $。将近似 $ \boldsymbol{u} \approx \boldsymbol{V}\boldsymbol{q} $ 代入并应用[伽辽金投影](@entry_id:145611) ($ \boldsymbol{V}^{T} \boldsymbol{R}_{\text{approx}} = \boldsymbol{0} $)，我们得到：

$ \boldsymbol{V}^{T} (\boldsymbol{M} \boldsymbol{V} \ddot{\boldsymbol{q}} + \boldsymbol{C} \boldsymbol{V} \dot{\boldsymbol{q}} + \boldsymbol{K} \boldsymbol{V} \boldsymbol{q} - \boldsymbol{f}) = \boldsymbol{0} $

整理后得到一个关于 $ \boldsymbol{q} $ 的 $ r $ 维[常微分方程组](@entry_id:266774)，即**降阶模型 (Reduced-Order Model, ROM)**：

$ \boldsymbol{M}_{r} \ddot{\boldsymbol{q}}(t) + \boldsymbol{C}_{r} \dot{\boldsymbol{q}}(t) + \boldsymbol{K}_{r} \boldsymbol{q}(t) = \boldsymbol{f}_{r}(t) $

其中，降阶算子定义为：

$ \boldsymbol{M}_{r} = \boldsymbol{V}^{T} \boldsymbol{M} \boldsymbol{V} \in \mathbb{R}^{r \times r} $
$ \boldsymbol{C}_{r} = \boldsymbol{V}^{T} \boldsymbol{C} \boldsymbol{V} \in \mathbb{R}^{r \times r} $
$ \boldsymbol{K}_{r} = \boldsymbol{V}^{T} \boldsymbol{K} \boldsymbol{V} \in \mathbb{R}^{r \times r} $
$ \boldsymbol{f}_{r}(t) = \boldsymbol{V}^{T} \boldsymbol{f}(t) \in \mathbb{R}^{r} $

[伽辽金投影](@entry_id:145611)的一个优美特性是它能够**保持结构**。例如，如果全阶的质量矩阵 $ \boldsymbol{M} $ 和刚度矩阵 $ \boldsymbol{K} $ 是[对称正定](@entry_id:145886)的 (Symmetric Positive Definite, SPD)，并且降阶基 $ \boldsymbol{V} $ 是列满秩的，那么相应的降阶矩阵 $ \boldsymbol{M}_r $ 和 $ \boldsymbol{K}_r $ 也将是 SPD 的。这保证了[降阶模型](@entry_id:754172)在物理上是稳定且有意义的 [@problem_id:2679849]。

值得注意的是，[投影法](@entry_id:144836)是一种**侵入式 (intrusive)** 方法，因为它需要我们能够访问并操作[全阶模型](@entry_id:171001)的系统矩阵（如 $ \boldsymbol{M}, \boldsymbol{K} $）和内部力向量。与之相对的是**非侵入式 (non-intrusive)** 方法，或称**代理模型 (surrogate models)**。这类方法将[全阶模型](@entry_id:171001)视为一个“黑箱”，通[过采样](@entry_id:270705)一组输入（如参数 $ \boldsymbol{\mu} $）和对应的输出（如解 $ \boldsymbol{u} $ 或关心量 $ s $），直接学习输入到输出的映射关系，例如 $ \mathcal{S}: \boldsymbol{\mu} \mapsto \boldsymbol{u}(\boldsymbol{\mu}) $。[神经网](@entry_id:276355)络、[径向基函数](@entry_id:754004)和[多项式混沌展开](@entry_id:162793)是常见的非侵入式方法。其关键区别在于：侵入式[投影法](@entry_id:144836)近似的是**控制方程本身**，而非侵入式代理模型近似的是控制方程的**解映射** [@problem_id:2679811]。

### 构建降阶基 $V$

降阶基 $ \boldsymbol{V} $ 的质量直接决定了[降阶模型](@entry_id:754172)的预测精度。选择一个能够以尽可能小的维度 $ r $ 捕捉系统主要动态特征的基是降阶建模的核心挑战。

#### 基于物理洞察的基：线性法向模态

对于许多[结构动力学](@entry_id:172684)问题，一个自然的选择是使用系统的**线性法向模态 (Linear Normal Modes)** 作为基。这些模态是系统在其[平衡点](@entry_id:272705)附近线性化后得到的[特征向量](@entry_id:151813) $ \boldsymbol{\phi}_i $，满足[广义特征值问题](@entry_id:151614) $ \boldsymbol{K} \boldsymbol{\phi}_i = \omega_i^2 \boldsymbol{M} \boldsymbol{\phi}_i $。通常，系统的[低频响应](@entry_id:276602)由少数几个低阶模态主导，因此选择前 $ r $ 个最低频率的模态作为基 $ \boldsymbol{V} = [\boldsymbol{\phi}_1, \dots, \boldsymbol{\phi}_r] $ 是一种常见的做法。

然而，这种方法的有效性仅限于线性或弱[非线性](@entry_id:637147)区域。在强[非线性动力学](@entry_id:190195)中，系统的行为会发生质变。线性模态所张成的[子空间](@entry_id:150286)在[非线性](@entry_id:637147)动力作用下通常**不是不变的**。即使[初始条件](@entry_id:152863)完全位于由前 $ r $ 个模态构成的[子空间](@entry_id:150286)内，[非线性](@entry_id:637147)耦合项（例如，[几何非线性](@entry_id:169896)引起的二次或三次项）也会将能量从这些低阶模态“泄漏”到被截断的[高阶模](@entry_id:750331)态中，从而产生显著的误差 [@problem_id:2679802]。例如，在存在 $2:1$ [内共振](@entry_id:750753)的情况下，一个仅包含第一阶模态的模型从结构上就无法捕捉到与第二阶模态之间的能量交换现象 [@problem_id:2679802]。

#### 数据驱动的基：[本征正交分解](@entry_id:165074) (POD)

为了克服线性模态在[非线性](@entry_id:637147)问题中的局限性，我们可以采用一种数据驱动的方法来“学习”[最优基](@entry_id:752971)。**[本征正交分解](@entry_id:165074) (Proper Orthogonal Decomposition, POD)** 是其中最流行和最强大的技术。其思想是，我们首先通过一次或数次高保真的[全阶模型](@entry_id:171001)仿真，在系统典型的运行工况下采集一系列状态“快照” (snapshots)，$ \{\boldsymbol{u}(t_k)\}_{k=1}^{m} $。然后，我们将这些快照向量作为列，构成一个快照矩阵 $ \boldsymbol{X} = [\boldsymbol{u}(t_1), \dots, \boldsymbol{u}(t_m)] \in \mathbb{R}^{N \times m} $。

POD的目标是寻找一个 $ r $ 维的正交基，使得所有快照投影到这个基上产生的平均重构误差最小。这个[优化问题](@entry_id:266749)可以被证明等价于对快照矩阵 $ \boldsymbol{X} $ 进行**奇异值分解 (Singular Value Decomposition, SVD)** [@problem_id:2679843]。

$ \boldsymbol{X} = \boldsymbol{U} \boldsymbol{\Sigma} \boldsymbol{W}^{T} $

其中，$ \boldsymbol{U} $ 的列向量（[左奇异向量](@entry_id:751233)）构成了最优的POD基。也就是说，我们可以取 $ \boldsymbol{V} = [\boldsymbol{u}_1, \dots, \boldsymbol{u}_r] $。奇异值 $ \sigma_i $ 的大小量化了每个[对应模](@entry_id:200367)态 $ \boldsymbol{u}_i $ 在快照数据中所包含的“能量”或重要性。[奇异值](@entry_id:152907)的快速衰减意味着数据可以被一个低维[子空间](@entry_id:150286)高度压缩，这预示着一个高效的[降阶模型](@entry_id:754172)是可能存在的。

由于POD基是从真实非线性动力学轨迹的快照中提取的，它能够捕捉到线性模态无法描述的、依赖于振幅的复杂变形模式和模态间的耦合效应。因此，在强[非线性](@entry_id:637147)区域，对于相同的基维度 $ r $，POD基通常比线性[模态基](@entry_id:752055)提供高得多的精度 [@problem_id:2679802]。

此外，POD框架可以自然地推广到不同的物理度量。标准POD（基于[欧几里得范数](@entry_id:172687)）对于位移场本身是最优的。如果我们更关心动能（其范数由质量矩阵 $ \boldsymbol{M} $ 定义）或[应变能](@entry_id:162699)（其范数由[刚度矩阵](@entry_id:178659) $ \boldsymbol{K} $ 定义），我们可以通过对加权后的快照矩阵（例如 $ \boldsymbol{M}^{1/2}\boldsymbol{X} $）进行SVD来构建一个在相应[能量范数](@entry_id:274966)意义下最优的基 [@problem_id:2679843]。

#### 理论基础：降阶可行性

降阶建模的成功并非理所当然。其可行性取决于系统解[流形](@entry_id:153038)的内在几何结构。**科尔莫戈罗夫 n-宽度 (Kolmogorov n-width)** 为此提供了一个严格的数学度量。它衡量了一个给定的解集（[流形](@entry_id:153038)）可以被一个最优选择的 $ n $ 维[线性子空间](@entry_id:151815)所逼近的最佳程度。如果一个解[流形](@entry_id:153038)的 n-宽度随着 $ n $ 的增加而快速衰减，那么它就具有很好的“线性可逼近性”，意味着低维[线性子空间](@entry_id:151815)（如POD基）可以非常有效地表示它。

研究表明，解[流形](@entry_id:153038)的“平滑性”决定了 n-宽度的衰减速率 [@problem_id:2679864]。
*   对于参数依赖平滑（例如，解析依赖）的椭圆型或抛物型问题，解映射通常也是解析的，这导致 n-宽度呈**指数衰减**。这类问题是降阶建模的理想对象。
*   对于包含移动激波、前沿或其他输运主导特征的[对流](@entry_id:141806)主导问题，解[流形](@entry_id:153038)往往是高度弯曲或“非连接”的。这导致 n-宽度衰减缓慢（通常是**代数衰减**），使得标准的线性降阶方法效率低下。
*   当问题失去稳定性时（例如，在接[近不可压缩](@entry_id:752387)极限时未使用稳定化配方的弹性问题），解[算子范数](@entry_id:752960)可能随参数变化而爆炸，破坏了解[流形](@entry_id:153038)的[光滑结构](@entry_id:159394)，同样导致 n-宽度缓慢衰减 [@problem_id:2679864]。

### 应对计算挑战

即使我们构建了一个精确的降阶基 $ \boldsymbol{V} $ 并得到了一个 $ r $ 维的降阶系统，我们仍可能面临严峻的计算挑战，尤其是在[非线性](@entry_id:637147)和参数化问题中。

#### [非线性](@entry_id:637147)瓶颈与超降阶

考虑一个具有[非线性](@entry_id:637147)内力 $ \boldsymbol{f}_{\text{int}}(\boldsymbol{u}) $ 的系统。通过[伽辽金投影](@entry_id:145611)，我们得到的降阶[非线性](@entry_id:637147)项为 $ \boldsymbol{V}^{T} \boldsymbol{f}_{\text{int}}(\boldsymbol{V}\boldsymbol{q}) $。在每次仿真时间步中“直接”计算这个项的流程如下 [@problem_id:2679796]：
1.  **重构**：从降阶坐标 $ \boldsymbol{q} \in \mathbb{R}^{r} $ 计算全阶状态 $ \boldsymbol{u} = \boldsymbol{V}\boldsymbol{q} \in \mathbb{R}^{N} $。此步骤的计算成本为 $ O(Nr) $。
2.  **求值**：在全阶空间中计算[非线性](@entry_id:637147)力向量 $ \boldsymbol{f}_{\text{int}}(\boldsymbol{u}) $。此步骤的成本依赖于全阶自由度数 $ N $，并且对于复杂的[本构关系](@entry_id:186508)，这通常是计算的瓶颈。
3.  **投影**：将全阶力[向量投影](@entry_id:147046)回降阶空间 $ \boldsymbol{V}^{T} \boldsymbol{f}_{\text{int}}(\boldsymbol{u}) $。此步骤的成本为 $ O(Nr) $。

由于步骤2的存在，整个[降阶模型](@entry_id:754172)的在线计算成本仍然依赖于[全阶模型](@entry_id:171001)的维度 $ N $，这使得降阶带来的计算优势大打折扣，甚至完全丧失。这就是所谓的**[非线性](@entry_id:637147)计算瓶颈**。

**超降阶 (Hyper-reduction)** 是一类旨在解决这一瓶颈的技术。其核心思想是，我们不仅要对状态进行降阶，还要对计算[非线性](@entry_id:637147)项的过程本身进行近似。一个普遍的策略是**采样 (sampling)**。例如，在有限元中，[非线性](@entry_id:637147)[内力](@entry_id:167605)通常通过在所有 $ M $ 个高斯积分点上计算应力并进行[数值积分](@entry_id:136578)得到。超降阶方法通过只在一小部分 $ s $ 个（$ s \ll M $）精心挑选的积分点上执行这些计算，并用一个加权和来近似整个积分，从而将计算成本从与 $ M $（通常与 $ N $ 同阶）成正比降低到与 $ s $ 成正比，实现了与 $ N $ 无关的在线计算 [@problem_id:2679797]。

**[离散经验插值法](@entry_id:748503) (Discrete Empirical Interpolation Method, DEIM)** 是一种强大且通用的超降阶技术 [@problem_id:2679793]。它首先为[非线性](@entry_id:637147)函数本身（例如 $ \boldsymbol{f}_{\text{int}} $）构建一个数据驱动的基 $ \boldsymbol{U} $（通常也通过对[非线性](@entry_id:637147)力快照进行POD得到）。然后，它通过强制在少数几个（$ m $ 个）“插值点”（即向量分量索引）上精确匹配原函数值，来确定该函数在基 $ \boldsymbol{U} $ 上的近似。DEIM的近似公式为 $ \boldsymbol{g}(\boldsymbol{u}) \approx \boldsymbol{U} (\boldsymbol{P}^{T} \boldsymbol{U})^{-1} \boldsymbol{P}^{T} \boldsymbol{g}(\boldsymbol{u}) $，其中 $ \boldsymbol{P} $ 是一个选择插值点的采样矩阵。其关键优势在于，计算 $ \boldsymbol{P}^{T} \boldsymbol{g}(\boldsymbol{u}) $ 仅需要评估 $ \boldsymbol{g}(\boldsymbol{u}) $ 的 $ m $ 个分量，从而将计算复杂度从 $ O(N) $ 降低到 $ O(m) $。

#### [参数化](@entry_id:272587)问题与[离线-在线分解](@entry_id:177117)

对于参数依赖问题，降阶建模的目标是实现**实时 (real-time)** 或**多次查询 (many-query)** 的计算能力。这意味着，对于任何一个新的参数值 $ \boldsymbol{\mu} $，我们都希望能够极快地得到降阶模型的解。这通过一种称为**[离线-在线分解](@entry_id:177117) (offline-online decomposition)** 的计算策略来实现 [@problem_id:2679819]。

该策略的前提是系统的算子（如[刚度矩阵](@entry_id:178659)和力向量）对参数具有**仿射依赖 (affine parameter dependence)** 结构。这意味着算子可以表示为一系列参数无关的算子与参数依赖的标量函数的线性组合：

$ \boldsymbol{A}(\boldsymbol{\mu}) = \sum_{q=1}^{Q_a} \Theta_q^a(\boldsymbol{\mu}) \boldsymbol{A}_q $
$ \boldsymbol{f}(\boldsymbol{\mu}) = \sum_{q=1}^{Q_f} \Theta_q^f(\boldsymbol{\mu}) \boldsymbol{f}_q $

在这种结构下，计算可以分为两个阶段：
*   **离线阶段 (Offline Stage)**：这是一个计算密集、但只需执行一次的预计算阶段。我们对每个参数无关的算子 $ \boldsymbol{A}_q $ 和 $ \boldsymbol{f}_q $ 计算并存储它们对应的、小的降阶矩阵和向量，例如 $ \boldsymbol{A}_{r,q} = \boldsymbol{V}^{T} \boldsymbol{A}_q \boldsymbol{V} $。
*   **在线阶段 (Online Stage)**：对于任何给定的新参数 $ \boldsymbol{\mu} $，这个阶段的计算极其廉价。我们只需计算标量函数 $ \Theta_q(\boldsymbol{\mu}) $，然后通过简单的[线性组合](@entry_id:154743)快速“组装”出最终的降阶系统：$ \boldsymbol{A}_r(\boldsymbol{\mu}) = \sum_q \Theta_q^a(\boldsymbol{\mu}) \boldsymbol{A}_{r,q} $。之后求解这个小的 $ r \times r $ 系统。整个在线阶段的计算成本与全阶维度 $ N $ 无关。

这种[离线-在线分解](@entry_id:177117)是[认证降阶基方法](@entry_id:747215) (Certified Reduced Basis Method, RBM) 的基石，它使得处理复杂的[参数化](@entry_id:272587)问题成为可能。对于不具有天然仿射结构的问题，可以借助DEIM等技术来构造一个仿射近似。

### 稳定性与高级投影技术

在某些情况下，标准的[伽辽金投影](@entry_id:145611)（$ \boldsymbol{W} = \boldsymbol{V} $）可能导致不稳定的降阶模型，即使原始的[全阶模型](@entry_id:171001)是稳定的。这种情况尤其容易发生在当系统算子是非对称或非正规 (non-normal) 的时候，例如在包含强[对流](@entry_id:141806)项的[流体力学](@entry_id:136788)问题或受[非保守力](@entry_id:163431)作用的结构中。

在这些系统中，算子的左右[特征向量](@entry_id:151813)不再重合。[伽辽金投影](@entry_id:145611)到一个由右[特征向量](@entry_id:151813)（或其近似）张成的[子空间](@entry_id:150286)上，可能会产生一个[条件数](@entry_id:145150)很差甚至不稳定的降阶算子。

**[彼得罗夫-伽辽金](@entry_id:174072)投影** ($ \boldsymbol{W} \neq \boldsymbol{V} $) 提供了克服这一困难的途径 [@problem_id:2679836]。通过精心选择测试基 $ \boldsymbol{W} $，我们可以主动地为降阶模型注入稳定性。一个理论上最优的选择是，如果试验基 $ \boldsymbol{V} $ 近似了系统的右[特征向量](@entry_id:151813)，那么测试基 $ \boldsymbol{W} $ 应该近似相应的左[特征向量](@entry_id:151813)（即伴随算子的[特征向量](@entry_id:151813)）。这会产生一个双正交的降阶系统，从而保证稳定性。在实践中，这可以通过对伴随系统进行仿真并采集快照来构造 $ \boldsymbol{W} $ 来实现。

另一种重要的[彼得罗夫-伽辽金方法](@entry_id:753372)是**最小二乘[彼得罗夫-伽辽金](@entry_id:174072) (Least-Squares [Petrov-Galerkin](@entry_id:174072), LSPG)** 方法。对于[稳态](@entry_id:182458)问题 $ \boldsymbol{A}\boldsymbol{u}=\boldsymbol{b} $，通过选择测试基为 $ \boldsymbol{W} = \boldsymbol{A}\boldsymbol{V} $，得到的降阶系统等价于求解最小二乘问题 $ \min_{\boldsymbol{q}} \|\boldsymbol{A}\boldsymbol{V}\boldsymbol{q} - \boldsymbol{b}\|_2^2 $。这种方法通过最小化残差的范数来保证解的质量 [@problem_id:2679836]。

综上所述，降阶建模是一个涉及多个层面、原理与技术紧密结合的领域。从[投影法](@entry_id:144836)的基本思想到基的构建，再到应对[非线性](@entry_id:637147)和参数化挑战的超降阶与离线-在线策略，以及保证稳定性的高级投影方法，这些机制共同构成了一个强大而灵活的框架，旨在以可接受的计算成本，对复杂的物理系统进行高效、可靠的仿真和分析。