## 引言
在现代科学与工程领域，高保真数值仿真已成为理解复杂物理现象和进行产品设计的关键工具。然而，这些仿真——无论是模拟[湍流](@entry_id:151300)、预测天气，还是分析结构响应——通常涉及求解维度高达数百万甚至更高的[方程组](@entry_id:193238)，其巨大的计算成本往往成为创新的瓶颈。如何能在不牺牲关键精度的前提下，大幅提升仿真效率？这正是[降阶模型](@entry_id:754172)（Reduced-order Modeling, ROM）旨在解决的核心问题。ROM是一种强大的方法论，旨在从高维复杂系统中提炼出其内在的低维动态结构，从而构建出计算极其高效的“代理模型”。

本文将系统性地引导读者进入降阶建模的世界。在“原理与机制”一章中，我们将深入探讨其数学基础，揭示如何通过[本征正交分解](@entry_id:165074)（POD）从数据中提取主导模态，以及如何利用[伽辽金投影](@entry_id:145611)构建低维动力学系统。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将通过丰富的案例，展示[降阶模型](@entry_id:754172)如何在[计算流体力学](@entry_id:747620)、[热管理](@entry_id:146042)、图像处理乃至生物学等多个领域发挥关键作用。最后，“动手实践”部分将提供具体的编程练习，帮助读者将理论知识转化为实践技能，并体会其中的关键挑战。

现在，让我们一同启程，首先深入探索构成[降阶模型](@entry_id:754172)基石的数学原理与实现机制。

## 原理与机制

继前一章对降阶模型（Reduced-order Model, ROM）的背景和意义进行介绍之后，本章将深入探讨其核心的数学原理与实现机制。我们将系统性地回答构建一个有效的[降阶模型](@entry_id:754172)所必须解决的两个根本问题：第一，如何为高维系统识别并构建一个“最优”的低维近似[子空间](@entry_id:150286)？第二，在确定了[子空间](@entry_id:150286)后，如何在该空间内求解出最能逼近真实物理过程的近似解？本章将围绕这两个问题，从基本概念出发，层层递进，揭示降阶建模的精髓。

### 降阶的核心思想：投影

几乎所有复杂的物理系统，无论是流体流动、[结构振动](@entry_id:174415)还是热量传递，在通过[有限元法](@entry_id:749389)（FEM）或有限差分法（FDM）等方法进行[空间离散化](@entry_id:172158)后，都会转化为一个维度极高（通常为 $N$ 维，其中 $N$ 可达百万乃至更高）的常微分方程（ODE）或[代数方程](@entry_id:272665)组。降阶建模的根本出发点在于一个关键假设：尽管[状态向量](@entry_id:154607) $\boldsymbol{u}(t) \in \mathbb{R}^{N}$ 所在的[向量空间维度](@entry_id:200442)极高，但在参数和[时间演化](@entry_id:153943)过程中，系统实际探索的“状态空间”区域，即**解[流形](@entry_id:153038)**（Solution Manifold），本质上是一个嵌入在高维空间中的低维几何结构。

因此，我们不必在整个 $\mathbb{R}^{N}$ 空间中求解，而是可以寻找一个低维的[线性子空间](@entry_id:151815) $\mathcal{V}_{r}$（维度为 $r \ll N$），并假设真实解可以被该[子空间](@entry_id:150286)中的向量很好地近似。如果我们将这个[子空间](@entry_id:150286)的一组[基向量](@entry_id:199546)（或称**模态**）[排列](@entry_id:136432)成矩阵 $\boldsymbol{V} \in \mathbb{R}^{N \times r}$ 的列，那么任何近似解 $\boldsymbol{u}_{r}(t)$ 都可以表示为这些[基向量](@entry_id:199546)的线性组合：

$$
\boldsymbol{u}(t) \approx \boldsymbol{u}_{r}(t) = \boldsymbol{V} \boldsymbol{a}(t)
$$

其中，$\boldsymbol{a}(t) \in \mathbb{R}^{r}$ 是一个随时间变化的低维向量，称为**降阶坐标**或**[广义坐标](@entry_id:156576)**。如此一来，求解高维状态 $\boldsymbol{u}(t)$ 的问题就转化为了求解低维坐标 $\boldsymbol{a}(t)$ 的问题。这个过程在几何上可以理解为将高维空间中的解“投影”到我们精心选择的低维[子空间](@entry_id:150286)上。

### 确定最佳近似：[伽辽金投影](@entry_id:145611)

在拥有一个降阶[子空间](@entry_id:150286) $\mathcal{V}_{r}$ 后，我们面临第二个问题：如何确定降阶坐标 $\boldsymbol{a}(t)$ 的演化规律？答案蕴含在**[伽辽金投影](@entry_id:145611)**（Galerkin Projection）的原理之中。

考虑一个一般的（可能[非线性](@entry_id:637147)的）控制方程，其离散形式可以写成一个残差方程 $\boldsymbol{\mathcal{R}}(\boldsymbol{u}, \dot{\boldsymbol{u}}, \ddot{\boldsymbol{u}}, t) = \boldsymbol{0}$。当我们将近似解 $\boldsymbol{u}_{r} = \boldsymbol{V}\boldsymbol{a}$ 代入时，残差通常不再为零：

$$
\boldsymbol{\mathcal{R}}(\boldsymbol{V}\boldsymbol{a}, \boldsymbol{V}\dot{\boldsymbol{a}}, \boldsymbol{V}\ddot{\boldsymbol{a}}, t) \neq \boldsymbol{0}
$$

[伽辽金原理](@entry_id:167636)要求这个[残差向量](@entry_id:165091)与我们选定的近似[子空间](@entry_id:150286) $\mathcal{V}_{r}$ 中的所有向量**正交**。因为[子空间](@entry_id:150286)中的任何向量都可以由[基向量](@entry_id:199546) $\boldsymbol{V}$ 的列[线性表示](@entry_id:139970)，所以这个要求等价于让残差与 $\boldsymbol{V}$ 的每一列都正交。在数学上，这可以简洁地表示为：

$$
\boldsymbol{V}^{\top} \boldsymbol{\mathcal{R}}(\boldsymbol{V}\boldsymbol{a}, \boldsymbol{V}\dot{\boldsymbol{a}}, \boldsymbol{V}\ddot{\boldsymbol{a}}, t) = \boldsymbol{0}
$$

这个方程是一个关于降阶坐标 $\boldsymbol{a}$ 的 $r$ 维[方程组](@entry_id:193238)，其维度远小于原始的 $N$ 维系统，因此可以被高效求解。

从更深层次看，[伽辽金投影](@entry_id:145611)并非一种随意的选择，它具有深刻的变分法背景。要求残差与近似[子空间](@entry_id:150286)正交，本质上是在该[子空间](@entry_id:150286)内强制执行原方程的**[弱形式](@entry_id:142897)**（Weak Form）。对于对称正定（Symmetric Positive-Definite, SPD）的线性问题，[伽辽金投影](@entry_id:145611)给出的近似解是在**能量范数**意义下，[子空间](@entry_id:150286) $\mathcal{V}_{r}$ 中距离真实解“最近”的解，即最优近似解。

#### 在广义[内积](@entry_id:158127)下的投影

[伽辽金投影](@entry_id:145611)的“正交”概念依赖于所选的[内积](@entry_id:158127)。虽然最常用的是标准的欧几里得[内积](@entry_id:158127) $\langle \boldsymbol{x}, \boldsymbol{y} \rangle = \boldsymbol{x}^{\top}\boldsymbol{y}$，但在许多物理问题中，使用与系统物理特性（如能量）相关的[加权内积](@entry_id:163877)更为自然。例如，一个由对称正定矩阵 $\boldsymbol{M}$ 定义的[内积](@entry_id:158127)为 $\langle \boldsymbol{x}, \boldsymbol{y} \rangle_{\boldsymbol{M}} = \boldsymbol{x}^{\top}\boldsymbol{M}\boldsymbol{y}$。

在这种情况下，[伽辽金投影](@entry_id:145611)要求误差向量 $\boldsymbol{x} - \hat{\boldsymbol{x}}$ 在 $\boldsymbol{M}$-[内积](@entry_id:158127)下与[子空间](@entry_id:150286) $\mathcal{U}$ 正交，即 $\langle \boldsymbol{x} - \hat{\boldsymbol{x}}, \boldsymbol{v} \rangle_{\boldsymbol{M}} = 0$ 对所有 $\boldsymbol{v} \in \mathcal{U}$ 成立。这最终会导出一个求解降阶坐标的线性方程组，其[系数矩阵](@entry_id:151473)（[格拉姆矩阵](@entry_id:203297)）和右端项均由该特定[内积](@entry_id:158127)定义。选择与物理结构匹配的[内积](@entry_id:158127)对于保持模型的稳定性和准确性至关重要。

#### 实例：线性[结构动力学](@entry_id:172684)系统的降阶

让我们以一个典型的线性[结构动力学](@entry_id:172684)系统为例，其控制方程为：
$$
\boldsymbol{M} \ddot{\boldsymbol{u}}(t) + \boldsymbol{C} \dot{\boldsymbol{u}}(t) + \boldsymbol{K} \boldsymbol{u}(t) = \boldsymbol{f}(t)
$$
其中 $\boldsymbol{M}, \boldsymbol{C}, \boldsymbol{K}$ 分别为质量、阻尼和刚度矩阵。将近似 $\boldsymbol{u} \approx \boldsymbol{V} \boldsymbol{a}$ 代入，残差为 $\boldsymbol{\mathcal{R}}(t) = \boldsymbol{M}\boldsymbol{V}\ddot{\boldsymbol{a}} + \boldsymbol{C}\boldsymbol{V}\dot{\boldsymbol{a}} + \boldsymbol{K}\boldsymbol{V}\boldsymbol{a} - \boldsymbol{f}(t)$。施加标准欧几里得[内积](@entry_id:158127)下的[伽辽金条件](@entry_id:173975) $\boldsymbol{V}^{\top}\boldsymbol{\mathcal{R}}(t) = \boldsymbol{0}$，我们得到：

$$
(\boldsymbol{V}^{\top}\boldsymbol{M}\boldsymbol{V}) \ddot{\boldsymbol{a}}(t) + (\boldsymbol{V}^{\top}\boldsymbol{C}\boldsymbol{V}) \dot{\boldsymbol{a}}(t) + (\boldsymbol{V}^{\top}\boldsymbol{K}\boldsymbol{V}) \boldsymbol{a}(t) = \boldsymbol{V}^{\top}\boldsymbol{f}(t)
$$

这便是一个 $r$ 维的降阶模型，其降阶算子为：
$\boldsymbol{M}_{r} = \boldsymbol{V}^{\top}\boldsymbol{M}\boldsymbol{V}$, $\boldsymbol{C}_{r} = \boldsymbol{V}^{\top}\boldsymbol{C}\boldsymbol{V}$, $\boldsymbol{K}_{r} = \boldsymbol{V}^{\top}\boldsymbol{K}\boldsymbol{V}$，以及降阶载荷 $\boldsymbol{f}_{r}(t) = \boldsymbol{V}^{\top}\boldsymbol{f}(t)$。

一个至关重要的特性是，如果全阶矩阵 $\boldsymbol{M}$ 和 $\boldsymbol{K}$ 是[对称正定](@entry_id:145886)的（这在物理上对应于正质量和稳定结构），并且降阶基矩阵 $\boldsymbol{V}$ 是列满秩的，那么通过[伽辽金投影](@entry_id:145611)得到的降阶矩阵 $\boldsymbol{M}_{r}$ 和 $\boldsymbol{K}_{r}$ 也必然是对称正定的。这意味着投影过程保持了系统的基本物理属性，这是保证[降阶模型](@entry_id:754172)稳定可靠的基础。

### 构建降阶[子空间](@entry_id:150286)：基于数据的[模态分解](@entry_id:637725)

现在我们回到第一个，也是更核心的问题：如何找到一个“好”的基 $\boldsymbol{V}$？一个好的[子空间](@entry_id:150286)应该能够以很小的维度 $r$ 就精确地捕获系统状态的主要变化特征。

#### 解[流形](@entry_id:153038)的可近似性：柯尔莫哥洛夫n-宽度

理论上，一个参数化系统所有可能解的集合构成了一个**解[流形](@entry_id:153038)** $\mathcal{M} = \{\boldsymbol{u}(\boldsymbol{\mu}) : \boldsymbol{\mu} \in \mathcal{P}\}$。一个降阶模型是否有效，取决于这个[流形](@entry_id:153038)是否可以用低维[线性子空间](@entry_id:151815)很好地近似。**柯尔莫哥洛夫n-宽度**（Kolmogorov n-width），$d_{n}(\mathcal{M})$，为我们提供了衡量这种可近似性的理论工具。它度量了用最优的 $n$ 维[子空间](@entry_id:150286)去近似[流形](@entry_id:153038) $\mathcal{M}$ 时，可能出现的[最坏情况误差](@entry_id:169595)。

$d_{n}(\mathcal{M})$ 的衰减速度至关重要：
- **指数衰减**：如果 $d_{n}(\mathcal{M})$ 随 $n$ 呈指数衰减（如 $e^{-cn}$），表明解[流形](@entry_id:153038)非常“平坦”和“规则”，通常对应于解对参数是解析的情形。这意味着存在一个低维[子空间](@entry_id:150286)能够以极高的精度逼近整个[流形](@entry_id:153038)。这类问题非常适合标准的线性降阶方法。
- **代数衰减**：如果 $d_{n}(\mathcal{M})$ 仅呈代数速度衰减（如 $n^{-\alpha}$），表明解[流形](@entry_id:153038)具有更复杂的结构，例如包含激波、[边界层](@entry_id:139416)移动或[分岔](@entry_id:273973)等强[非线性](@entry_id:637147)或低正则性特征。这意味着需要非常多的[基向量](@entry_id:199546)才能达到可接受的精度，标准的线性降阶方法效果会大打折扣。

#### [本征正交分解](@entry_id:165074)（POD）

在实践中，我们无法直接计算解[流形](@entry_id:153038)及其n-宽度。**[本征正交分解](@entry_id:165074)**（Proper Orthogonal Decomposition, POD），在[流体力学](@entry_id:136788)中也称卡洛南-洛伊（Karhunen-Loève）分解，是一种从数据中提取最优[线性子空间](@entry_id:151815)的强大算法。其基本思想是：
1.  通过对[全阶模型](@entry_id:171001)进行多次模拟（在不同时间点或不同参数下），收集一系列典型的解，称为**快照**（snapshots），$\{\boldsymbol{u}_{k}\}_{k=1}^{m}$。
2.  将这些快照向量作为列，构建一个**快照矩阵** $\boldsymbol{X} = [\boldsymbol{u}_{1}, \boldsymbol{u}_{2}, \dots, \boldsymbol{u}_{m}]$。
3.  寻找一个 $r$ 维正交基，使得所有快照投影到这个基上的平均能量最大化，或者等价地，使得快照与它们的投影之间的平均重构[误差最小化](@entry_id:163081)。

这个最[优化问题](@entry_id:266749)的解可以通过对快照矩阵进行**奇异值分解**（Singular Value Decomposition, SVD）得到：$\boldsymbol{X} = \boldsymbol{U}\boldsymbol{\Sigma}\boldsymbol{V}^{\top}$。

- **[左奇异向量](@entry_id:751233)** $\boldsymbol{U}$ 的前 $r$ 列构成了最优的 $r$ 维POD基。它们就是我们寻找的降阶基矩阵 $\boldsymbol{V}$。
- **奇异值** $\sigma_{i}$（矩阵 $\boldsymbol{\Sigma}$ 的对角元）的平方 $\sigma_{i}^{2}$ 代表了每个对应[基向量](@entry_id:199546) $\boldsymbol{u}_{i}$ 所捕获的“能量”。奇异值的衰减速度直接反映了数据（也即解[流形](@entry_id:153038)）的[可压缩性](@entry_id:144559)。
- 在实践中，选择降阶维度 $r$ 的一个常用标准是**能量捕获阈值**。我们计算累积能量占总能量的比例 $\mathcal{E}(r) = \frac{\sum_{i=1}^{r} \sigma_i^2}{\sum_{j=1}^{\text{rank}(\boldsymbol{X})} \sigma_j^2}$，并选择满足 $\mathcal{E}(r) \ge \eta$（例如 $\eta=0.999$）的最小 $r$。这个能量比例等于秩-$r$ 近似所捕获的快照矩阵的[弗罗贝尼乌斯范数](@entry_id:143384)的平方分数。

值得注意的是，POD所捕获的“能量”取决于定义它的[内积](@entry_id:158127)。为了捕获特定的物理量，如动能或应变能，我们必须使用由质量矩阵 $\boldsymbol{M}$ 或刚度矩阵 $\boldsymbol{K}$ 定义的[加权内积](@entry_id:163877)来执行POD过程。

### 提升[降阶模型](@entry_id:754172)效率与应对挑战

构建了[子空间](@entry_id:150286)并通过[伽辽金投影](@entry_id:145611)得到降阶方程后，我们还需面对一些使其在实际应用中变得高效和可靠的关键挑战。

#### [仿射参数](@entry_id:260625)依赖性与离线-在线计算分解

对于参数化的[降阶模型](@entry_id:754172)，一个核心目标是实现极速的“在线”计算。即对于一个新的参数 $\boldsymbol{\mu}$，能够瞬时得到降阶解。然而，如果降阶算子 $A_{r}(\boldsymbol{\mu}) = \boldsymbol{V}^{\top}A(\boldsymbol{\mu})\boldsymbol{V}$ 的计算需要每次都生成并操作高维算子 $A(\boldsymbol{\mu})$，那么在线阶段的计算成本仍然依赖于高维系统的规模 $N$，降阶的优势将荡然无存。

解决这一瓶颈的关键是问题的**[仿射参数](@entry_id:260625)依赖性**（Affine Parameter Dependence）。如果高维算子可以分解为少数几个与参数无关的算子 $A_{q}$ 和仅与参数相关的标量函数 $\Theta_{q}^{a}(\boldsymbol{\mu})$ 的线性组合：
$$
A(\boldsymbol{\mu}) = \sum_{q=1}^{Q_{a}} \Theta_{q}^{a}(\boldsymbol{\mu}) A_{q}
$$
那么降阶算子也相应地具有仿射结构：
$$
A_{r}(\boldsymbol{\mu}) = \sum_{q=1}^{Q_{a}} \Theta_{q}^{a}(\boldsymbol{\mu}) (\boldsymbol{V}^{\top} A_{q} \boldsymbol{V})
$$
这使得一种高效的**离线-在线**（Offline-Online）计算策略成为可能：
- **离线阶段**：进行所有耗时且依赖于 $N$ 的计算。我们预先计算并存储所有小的、与参数无关的降阶矩阵 $\boldsymbol{A}_{q}^{r} = \boldsymbol{V}^{\top} A_{q} \boldsymbol{V}$。
- **在线阶段**：对于任何给定的新参数 $\boldsymbol{\mu}$，我们只需计算标量系数 $\Theta_{q}^{a}(\boldsymbol{\mu})$，然后将预先存储的小矩阵 $\boldsymbol{A}_{q}^{r}$ 进行[线性组合](@entry_id:154743)，即可快速构建出 $r \times r$ 的降阶系统。这一阶段的计算成本完全与高维系统的维度 $N$ 无关。

对于不具有天然仿射结构的问题，可以采用**[经验插值法](@entry_id:748957)**（EIM）或其离散版本（DEIM）等技术来构造一个近似的仿射表示。

#### [非线性](@entry_id:637147)项的“[维度灾难](@entry_id:143920)”与超降阶

当系统包含[非线性](@entry_id:637147)项 $\boldsymbol{f}(\boldsymbol{u})$ 时，降阶模型中会出现 $\boldsymbol{V}^{\top}\boldsymbol{f}(\boldsymbol{V}\boldsymbol{a})$ 这样的项。在在线阶段计算它时，我们必须首先通过 $\boldsymbol{V}\boldsymbol{a}$ 从低维坐标重构出高维状态 $\boldsymbol{u}_{r}$，然后在这个 $N$ 维向量上计算[非线性](@entry_id:637147)函数 $\boldsymbol{f}$，最后再投影回低维空间。计算 $\boldsymbol{f}(\boldsymbol{V}\boldsymbol{a})$ 的成本通常与高维系统的维度 $N$ 成正比。这个计算瓶颈被称为[非线性降阶模型](@entry_id:172252)中的“[维度灾难](@entry_id:143920)”，因为它使得在线计算的效率受限于高维系统的规模。

**超降阶**（Hyper-reduction）技术，如DEIM，旨在解决这一问题。其核心思想是，[非线性](@entry_id:637147)项 $\boldsymbol{f}(\boldsymbol{u})$ 本身也可能存在于一个低维[流形](@entry_id:153038)上。因此，我们可以通过仅计算 $\boldsymbol{f}(\boldsymbol{u}_{r})$ 的少数几个（$m \ll N$）关键分量，并利用一个预先计算好的基，来近似重构整个[非线性](@entry_id:637147)向量。这使得[非线性](@entry_id:637147)项的在线计算成本只与 $m$ 和 $r$ 相关，而与 $N$ 无关，从而消除了[维度灾难](@entry_id:143920)。

#### [降阶模型](@entry_id:754172)的稳定性问题

一个常见的误区是认为只要[全阶模型](@entry_id:171001)是稳定的，其[降阶模型](@entry_id:754172)也必然是稳定的。事实并非如此。降阶过程，作为一种信息压缩，可能会破坏原始系统赖以维持稳定的[精细结构](@entry_id:140861)，从而导致不稳定的降阶模型。主要的失稳机制包括：
1.  **耗散尺度截断**：在像[湍流](@entry_id:151300)这样的多尺度系统中，能量主要由大尺度模态承载，而耗散则主要发生于小尺度模态。POD倾向于保留高能量的大尺度模态，而截断低能量的小尺度模态。这切断了能量从大尺度向小尺度传递并最终耗散的物理路径，导致能量在[降阶模型](@entry_id:754172)中虚假地累积，引发不稳定。
2.  **物理约束的破坏**：许多系统的稳定性依赖于物理约束，如[不可压缩流](@entry_id:140301)动的“[无散度](@entry_id:190991)”约束。如果POD基本身不满足这些约束，那么降阶解 $\boldsymbol{V}\boldsymbol{a}$ 也会违反约束，可能导致原本为零的[非线性](@entry_id:637147)项变为非零，从而向系统注入虚假能量。
3.  **[非正规算子](@entry_id:752588)的投影**：即使一个[线性算子](@entry_id:149003) $L$ 的所有[特征值](@entry_id:154894)都在[左半平面](@entry_id:270729)（保证了渐进稳定），但如果 $L$ 是高度非正规的（其[特征向量](@entry_id:151813)接近线性相关），那么它在某个[子空间](@entry_id:150286)上的[伽辽金投影](@entry_id:145611) $L_{r}$ 可能会产生具有正实部的[特征值](@entry_id:154894)，从而导致线性不稳定。
4.  **不一致的投影**：如果[伽辽金投影](@entry_id:145611)所用的[内积](@entry_id:158127)与系统能量或稳定结构所依赖的[内积](@entry_id:158127)不匹配（例如，对一个由[质量矩阵](@entry_id:177093) $M$ 定义能量的系统使用标准欧几里得投影），可能会破坏算子的对称性或[反对称性](@entry_id:261893)等关键结构，从而引入不稳定性。

### 两类主要的降阶方法：一个总结

至此，我们详细讨论的都属于**[基于投影的降阶模型](@entry_id:753809)**。这类方法的核心是对系统的控制方程（物理定律的数学表达）进行[伽辽金投影](@entry_id:145611)，从而得到一个规模更小但结构相似的“微型”物理模型。它们是“侵入式”（intrusive）的，因为我们需要访问并操作[全阶模型](@entry_id:171001)的算子（如质量、[刚度矩阵](@entry_id:178659)）。

与此相对的是另一大类方法：**非侵入式[降阶模型](@entry_id:754172)**（Non-intrusive ROMs）。这类方法将[全阶模型](@entry_id:171001)视为一个“黑箱”。它们不关心内部的控制方程，而是通过运行[全阶模型](@entry_id:171001)生成一组输入-输出数据对（例如，参数 $\boldsymbol{\mu}$ 与对应的解 $\boldsymbol{u}$ 或关心量 $s$），然后使用机器学习或统计回归技术（如[神经网](@entry_id:276355)络、[高斯过程回归](@entry_id:276025)、[多项式混沌展开](@entry_id:162793)等）来学习这个从输入到输出的**解映射**（solution map）。非侵入式模型直接逼近问题的“答案”，而不是逼近问题的“方程”。

这两类方法各有优劣。基于投影的模型通常能更好地保持物理结构，并且可以借助严谨的[后验误差估计](@entry_id:167288)来保证其预测的可靠性。非侵入式模型则更容易实现（无需修改现有的大型仿真代码），并且在处理极其复杂的[非线性](@entry_id:637147)或非仿射问题时可能更具灵活性。在现代计算科学与工程中，这两类方法以及它们的混合使用，共同构成了降阶建模的丰富工具箱。