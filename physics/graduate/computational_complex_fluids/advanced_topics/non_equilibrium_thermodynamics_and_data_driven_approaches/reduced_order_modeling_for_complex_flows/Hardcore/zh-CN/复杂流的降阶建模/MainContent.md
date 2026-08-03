## 引言
复杂流动，如湍流、粘弹性流体和多相流，其行为跨越多个时空尺度，是众多科学与工程领域的核心挑战。对其进行高保真数值模拟，尽管能够提供精确的物理洞察，但往往需要巨大的计算资源，限制了其在设计优化、实时控制和不确定性量化等“多查询”场景中的应用。因此，学术界与工业界迫切需要开发能够以极低计算成本捕捉系统关键动力学的模型。降阶建模（Reduced-Order Modeling, ROM）应运而生，它通过将大规模的动力学系统压缩到低维空间，为这一挑战提供了强有力的解决方案。

本文旨在系统性地介绍复杂流动降阶建模的核心理论与前沿应用。读者将从基础原理出发，逐步深入到高级技术与实际工程问题中。在“**原理与机制**”一章，我们将揭示降阶模型背后的数学基础，探讨如何通过本征正交分解（POD）和动态模态分解（DMD）等方法从数据中提取主导模式，并利用Galerkin投影构建低维动力学系统。随后，在“**应用与跨学科连接**”一章，我们将展示这些理论如何转化为解决实际问题的工具，涵盖从流体不稳定性分析、工程优化到构建数字孪生等广泛应用。最后，“**动手实践**”部分将提供具体的编程练习，帮助读者将理论知识转化为实践技能。通过这三章的学习，本文将为读者构建一个从理论到实践的完整降阶建模知识体系。

## 原理与机制

继前一章介绍降阶模型（Reduced-Order Models, ROMs）在复杂流体模拟中的重要性之后，本章将深入探讨其核心的数学原理与实现机制。复杂流体的行为跨越多个时空尺度，其控制方程（如Navier-Stokes方程与本构关系耦合）的非线性与多物理场特性为建模带来了巨大挑战。例如，在剪切驱动的通道流中，系统的行为由不同的物理主导平衡所决定，这些平衡可以通过关键的无量纲数来表征，如雷诺数（$Re$）、魏森伯格数（$Wi$）和溶剂粘度比（$\beta$）[@problem_id:4101569]。一个有效的降阶模型必须能够精确捕捉这些在不同流态（例如，惯性主导、粘性溶剂主导或弹性聚合物主导）下起决定性作用的动力学特征。本章将系统地阐述如何构建、改进和应用降阶模型，以应对这些挑战。

### 基础：基于投影的降阶

降阶建模的出发点通常是一个高维度的半离散系统。通过对流体控制偏微分方程进行空间离散化（例如，使用有限元或有限体积法），我们得到一个大规模的常微分方程（ODE）组。对于一个自治系统，其形式可写为：
$$
\dot{\boldsymbol{x}}(t) = \boldsymbol{f}(\boldsymbol{x}(t))
$$
其中，$\boldsymbol{x}(t) \in \mathbb{R}^{n}$ 是状态向量，它包含了在离散网格上所有点的速度、压力、应力等自由度，其维度 $n$ 通常非常大（可达数百万甚至更多）。函数 $\boldsymbol{f}: \mathbb{R}^{n} \to \mathbb{R}^{n}$ 代表了系统的非线性动力学演化规律。

降阶的核心思想是，尽管状态向量 $\boldsymbol{x}(t)$ 存在于一个高维空间中，但其演化轨迹通常局限于一个低维的**流形**（manifold）上。这意味着我们可以用少数几个关键模态（或模式）的线性组合来近似地表示系统的状态。我们寻求一个近似解 $\tilde{\boldsymbol{x}}(t)$，它位于一个由 $r$ 个基向量张成的低维子空间中，其中 $r \ll n$：
$$
\boldsymbol{x}(t) \approx \tilde{\boldsymbol{x}}(t) = \boldsymbol{V}\boldsymbol{a}(t)
$$
在这里，$\boldsymbol{V} \in \mathbb{R}^{n \times r}$ 是一个矩阵，其列向量 $\{\boldsymbol{v}_1, \dots, \boldsymbol{v}_r\}$ 构成了该低维子空间的一组基。向量 $\boldsymbol{a}(t) \in \mathbb{R}^{r}$ 则是这个近似解在基底 $\boldsymbol{V}$下的坐标，被称为广义坐标或模态系数。

下一步是推导这些模态系数 $\boldsymbol{a}(t)$ 的演化方程。**Galerkin投影**是一种系统性的方法。其基本思想是，虽然近似解 $\tilde{\boldsymbol{x}}(t)$ 通常不能精确满足原始的动力学方程，但我们可以要求其产生的**残差**（residual）与我们选择的基底空间正交。残差定义为：
$$
\boldsymbol{\mathcal{R}}(\tilde{\boldsymbol{x}}(t)) = \dot{\tilde{\boldsymbol{x}}}(t) - \boldsymbol{f}(\tilde{\boldsymbol{x}}(t)) = \boldsymbol{V}\dot{\boldsymbol{a}}(t) - \boldsymbol{f}(\boldsymbol{V}\boldsymbol{a}(t))
$$
Galerkin方法要求这个 $n$ 维的残差向量与构成我们近似空间的每一个基向量都正交。在数学上，这等价于将残差投影到由 $\boldsymbol{V}$ 的列向量张成的子空间上，并令其投影为零。如果基向量关于欧几里得内积是标准正交的（即 $\boldsymbol{V}^T \boldsymbol{V} = \boldsymbol{I}_r$），这个正交性条件可以简洁地表示为 [@problem_id:4101518]：
$$
\boldsymbol{V}^T \boldsymbol{\mathcal{R}}(\tilde{\boldsymbol{x}}(t)) = \boldsymbol{0}
$$
将残差的表达式代入，我们得到：
$$
\boldsymbol{V}^T (\boldsymbol{V}\dot{\boldsymbol{a}}(t) - \boldsymbol{f}(\boldsymbol{V}\boldsymbol{a}(t))) = \boldsymbol{0}
$$
利用基底的正交性 $\boldsymbol{V}^T \boldsymbol{V} = \boldsymbol{I}_r$，我们最终得到一个关于模态系数 $\boldsymbol{a}(t)$ 的低维常微分方程系统，这就是我们的**降阶模型 (ROM)**：
$$
\dot{\boldsymbol{a}}(t) = \boldsymbol{V}^T \boldsymbol{f}(\boldsymbol{V}\boldsymbol{a}(t))
$$
这个方程组的维度为 $r$，远小于原始系统的维度 $n$，因此求解它在计算上要高效得多。这个过程将高维动力学问题投影到了一个低维的子空间中，从而实现了降阶。

### 构建基底：本征正交分解 (POD)

Galerkin投影框架的有效性在很大程度上取决于基底 $\boldsymbol{V}$ 的选择。一个好的基底应该能够以最少的模态数量“捕获”系统绝大部分的能量或关键动力学特征。**本征正交分解 (Proper Orthogonal Decomposition, POD)**，在流体力学领域也被称为Karhunen-Loève分解，是目前应用最广泛的、从数据中提取最优基底的方法。

POD的目标是找到一组标准正交基，使得从高维仿真或实验中采集的**快照**（snapshots）数据投影到这组基底上时，其能量（或方差）最大化。假设我们有 $m$ 个状态快照 $\boldsymbol{x}_1, \dots, \boldsymbol{x}_m$，并将它们排列成一个快照矩阵 $\boldsymbol{X} = [\boldsymbol{x}_1, \dots, \boldsymbol{x}_m] \in \mathbb{R}^{n \times m}$。对于一个由有限元离散化得到的系统，其能量内积通常由质量矩阵 $\boldsymbol{M}$ 定义，即 $\langle \boldsymbol{u}, \boldsymbol{v} \rangle_{\boldsymbol{M}} = \boldsymbol{u}^T \boldsymbol{M} \boldsymbol{v}$。第一个POD模态 $\boldsymbol{\phi}_1$ 的目标就是最大化所有快照在其上的投影能量之和，同时保持自身模长为1：
$$
\boldsymbol{\phi}_1 = \arg\max_{\boldsymbol{\phi}} \sum_{k=1}^{m} |\langle \boldsymbol{x}_k, \boldsymbol{\phi} \rangle_{\boldsymbol{M}}|^2 \quad \text{subject to} \quad \|\boldsymbol{\phi}\|_{\boldsymbol{M}}^2 = 1
$$
直接求解这个 $n$ 维的优化问题是困难的。然而，通过一个被称为“快照法”（method of snapshots）的技巧，我们可以证明，最优的POD模态总是位于快照所张成的子空间中，即 $\boldsymbol{\phi} = \boldsymbol{X}\boldsymbol{a}$。通过这一代换，上述优化问题可以转化为一个关于系数向量 $\boldsymbol{a}$ 的 $m$ 维特征值问题 [@problem_id:4101473]：
$$
\boldsymbol{C}\boldsymbol{a} = \lambda\boldsymbol{a}
$$
其中，$\boldsymbol{C} = \boldsymbol{X}^T \boldsymbol{M} \boldsymbol{X} \in \mathbb{R}^{m \times m}$ 是快照的**相关矩阵**（correlation matrix）。这个矩阵的维度 $m \times m$ 通常远小于原始维度 $n \times n$。该特征值问题的特征值 $\lambda_i$ 直接对应于每个POD模态所捕获的能量，而特征向量 $\boldsymbol{a}_i$ 则给出了构建相应POD模态 $\boldsymbol{\phi}_i$ 的系数。总能量是相关矩阵的迹（trace），即所有特征值之和。因此，第 $i$ 个模态捕获的能量分数是 $\lambda_i / \text{trace}(\boldsymbol{C})$。

在实践中，POD通常通过对快照矩阵 $\boldsymbol{X}$（或适当加权的矩阵 $\boldsymbol{M}^{1/2}\boldsymbol{X}$）进行**奇异值分解 (Singular Value Decomposition, SVD)** 来计算。SVD提供了与POD等价的基底（左奇异向量）和能量信息（奇异值），并且在数值上更为稳健。通过选取与最大奇异值相对应的少数几个左奇异向量作为基底 $\boldsymbol{V}$，我们便获得了一个在能量意义上最优的低维子空间。

### 另一种范式：动态模态分解 (DMD)

POD-Galerkin方法是“侵入式”的，因为它需要我们访问并投影原始的控制方程 $\boldsymbol{f}(\boldsymbol{x})$。在某些情况下，我们可能只有测量数据而没有精确的方程模型，或者方程极其复杂难以处理。在这种背景下，**动态模态分解 (Dynamic Mode Decomposition, DMD)** 提供了一种强大的、纯数据驱动的“非侵入式”建模方法。

DMD的核心思想是，假设系统的动力学演化在两个连续的快照集合之间可以由一个线性算子 $\boldsymbol{A}$ 来近似。给定两组快照矩阵 $\boldsymbol{X}_1 = [\boldsymbol{x}_1, \dots, \boldsymbol{x}_{r}]$ 和 $\boldsymbol{X}_2 = [\boldsymbol{x}_2, \dots, \boldsymbol{x}_{r+1}]$，其中 $\boldsymbol{X}_2$ 的每一列是 $\boldsymbol{X}_1$ 对应列在下一个时间步的状态，DMD旨在寻找一个最佳拟合的线性算子 $\boldsymbol{A}$，使得 $\boldsymbol{X}_2 \approx \boldsymbol{A}\boldsymbol{X}_1$。这个算子 $\boldsymbol{A}$ 是高维空间中的Koopman算子的一个有限维近似。

在最小二乘意义下，最优的算子 $\boldsymbol{A}$ 由 $\boldsymbol{A} = \boldsymbol{X}_2 \boldsymbol{X}_1^{\dagger}$ 给出，其中 $\boldsymbol{X}_1^{\dagger}$ 是 $\boldsymbol{X}_1$ 的Moore-Penrose伪逆。直接计算和存储高维算子 $\boldsymbol{A}$ 是不现实的。**精确DMD** (Exact DMD) 算法通过将这个高维算子投影到由 $\boldsymbol{X}_1$ 的POD基底（即其左奇异向量 $\boldsymbol{U}_r$）张成的子空间上来解决这个问题。这样可以得到一个低维的算子 $\tilde{\boldsymbol{A}} \in \mathbb{R}^{r \times r}$ [@problem_id:4101538]：
$$
\tilde{\boldsymbol{A}} = \boldsymbol{U}_r^T \boldsymbol{A} \boldsymbol{U}_r = \boldsymbol{U}_r^T \boldsymbol{X}_2 \boldsymbol{V}_r \boldsymbol{\Sigma}_r^{-1}
$$
其中 $\boldsymbol{U}_r$, $\boldsymbol{\Sigma}_r$, $\boldsymbol{V}_r$ 来自于 $\boldsymbol{X}_1$ 的SVD分解 $\boldsymbol{X}_1 = \boldsymbol{U}_r \boldsymbol{\Sigma}_r \boldsymbol{V}_r^T$。

这个低维算子 $\tilde{\boldsymbol{A}}$ 的特征值和特征向量揭示了系统的动力学特性。$\tilde{\boldsymbol{A}}$ 的每个特征值 $\lambda_j$（**DMD特征值**）代表了一个动态模式的增长/衰减率和振荡频率。对应的特征向量 $\boldsymbol{w}_j$ 通过 $\boldsymbol{\phi}_j = \boldsymbol{U}_r \boldsymbol{w}_j$ 映射回高维空间，得到**DMD模态** $\boldsymbol{\phi}_j$，它代表了与该频率和增长率相关的相干空间结构。因此，DMD提供了一种完全从数据中提取时空相干结构的方法，是分析和理解复杂流动的有力工具。

### 应对计算与物理挑战

构建一个基础的POD-Galerkin模型只是第一步。在应用于真实的复杂流体问题时，我们会遇到一系列挑战，这些挑战催生了各种高级的降阶技术。

#### 非线性问题：使用 DEIM 进行超降阶

在非线性系统的ROM $\dot{\boldsymbol{a}} = \boldsymbol{V}^T \boldsymbol{f}(\boldsymbol{V}\boldsymbol{a})$ 中，每一步时间积分都需要计算非线性项 $\boldsymbol{f}(\boldsymbol{V}\boldsymbol{a})$。这个计算过程包括：首先将低维系数 $\boldsymbol{a}$ "提升"回高维空间（$\boldsymbol{V}\boldsymbol{a}$），然后对这个 $n$ 维向量施加非线性函数 $\boldsymbol{f}$，最后再将其投影回低维空间（$\boldsymbol{V}^T \dots$）。当 $n$ 非常大时，这一过程的计算成本会抵消降阶带来的优势。

**超降阶 (Hyper-reduction)** 技术旨在解决这一瓶颈。**离散经验插值法 (Discrete Empirical Interpolation Method, DEIM)** 是其中一种主流方法。DEIM 的思想是，非线性项 $\boldsymbol{g}(\boldsymbol{x}) = \boldsymbol{f}(\boldsymbol{x})$ 本身也可能存在于一个低维子空间中。因此，我们可以为非线性项本身构建一个POD基底，记为 $\boldsymbol{U} \in \mathbb{R}^{n \times m}$。然后，我们用这个基底的线性组合来近似非线性项：
$$
\boldsymbol{g}(\boldsymbol{V}\boldsymbol{a}) \approx \boldsymbol{U}\boldsymbol{c}(t)
$$
为了确定系数 $\boldsymbol{c}(t)$，DEIM并不进行投影，而是巧妙地选择 $m$ 个“插值点”（物理空间中的网格点），并要求近似值在这些点上与真实值完全相等。这个选择过程由一个采样矩阵 $\boldsymbol{P} \in \mathbb{R}^{n \times m}$ 来表示。通过求解一个小的线性系统，可以得到系数 $\boldsymbol{c}$ 的表达式，并最终得到非线性项的DEIM近似。将其代入到ROM的投影项中，我们得到DEIM近似下的降阶非线性残差 [@problem_id:4101562]：
$$
\boldsymbol{r}_{\mathrm{nl}}^{\mathrm{DEIM}}(\boldsymbol{a}) = (\boldsymbol{W}^{T}\boldsymbol{U}) (\boldsymbol{P}^{T}\boldsymbol{U})^{-1} \boldsymbol{P}^{T} \boldsymbol{g}(\boldsymbol{V}\boldsymbol{a})
$$
这里 $\boldsymbol{W}$ 是测试基底（在Galerkin方法中 $\boldsymbol{W}=\boldsymbol{V}$）。这个表达式的计算优势在于，它只需要计算非线性函数 $\boldsymbol{g}(\boldsymbol{V}\boldsymbol{a})$ 在 $m$ 个插值点上的值（通过 $\boldsymbol{P}^T$ 实现），而 $m$ 通常远小于 $n$。这极大地降低了在线计算的成本。

#### 稳定性问题：Petrov-Galerkin 方法

对于对流主导的流动问题，标准的Galerkin投影（其中测试空间与试验空间相同，即 $\boldsymbol{W}=\boldsymbol{V}$）往往会导致数值不稳定性，产生非物理的振荡。即使原始的半离散系统具有能量耗散或守恒的性质（例如，对流算子是反对称的），并且Galerkin投影能够在其降阶版本中保留这一性质，但这并不能保证模型在所有情况下都是稳定的。

问题的根源在于，对流算子通常是**非正规的 (non-normal)**，这意味着它的特征向量并非正交。非正规系统即使所有特征值都表明其是长期稳定的，也可能在短期内表现出巨大的**瞬态增长 (transient growth)**。Galerkin投影继承了这种非正规性，导致降阶模型对扰动非常敏感，从而产生振荡。

**Petrov-Galerkin方法**通过选择一个不同于试验基底 $\boldsymbol{V}$ 的测试基底 $\boldsymbol{W}$（即 $\boldsymbol{W} \neq \boldsymbol{V}$）来解决这个问题。这种方法的灵活性允许我们为降阶系统引入额外的、有益的数值特性。例如，在**流线迎风Petrov-Galerkin (Streamline-Upwind Petrov-Galerkin, SUPG)** 方法中，测试基底是通过在试验基底的基础上沿流线方向增加一个扰动来构造的。这种“迎风”的偏置有效地在模型中引入了人工的、具有物理一致性的数值耗散，专门用于抑制由对流主导引起的振荡 [@problem_id:4101472]。这种额外的耗散对于物理扩散很弱的系统至关重要，它能显著提高模型的稳定性和鲁棒性。

#### 截断问题：湍流的闭合建模

在模拟湍流时，我们面临一个更根本的物理问题。湍流的一个核心特征是**能量级串 (energy cascade)**：能量从大尺度的涡结构（可由ROM中的模态 $\boldsymbol{u}_m$ 表示）不断地传递到小尺度的涡结构（被ROM截断的模态 $\boldsymbol{u}'$），并最终在最小尺度上通过粘性耗散掉。

标准的Galerkin投影只保留了已解析模态之间的相互作用，完全忽略了已解析模态与被截断模态之间的能量交换。这相当于切断了能量从大尺度向小尺度传递的物理路径。其后果是，能量会在已解析的模态中不切实际地累积，特别是在分辨率最高（即波数最大）的模态上，最终导致模型发散。

为了解决这个问题，必须引入**闭合模型 (closure model)** 来近似被截断模态对已解析模态的平均效应。这种效应主要是耗散性的，即从已解析尺度中“抽走”能量。一种简单而有效的闭合方法是**涡粘模型 (eddy-viscosity model)**。其思想是，被截断的小尺度涡对大尺度运动的影响，类似于一个增强的分子粘性。我们可以为ROM增加一个额外的耗散项 $-\nu_e \boldsymbol{D}\boldsymbol{a}$。这里的涡粘系数 $\nu_e$ 不是一个固定的物理参数，而是需要根据流动状态动态调整。一种方法是通过校准能量收支来实现。我们可以要求闭合后的ROM的能量耗散率与从高精度直接数值模拟（DNS）中观测到的已解析尺度的真实能量耗散率相匹配。通过这个能量收支的差额，我们可以推导出涡粘系数 $\nu_e$ 的表达式 [@problem_id:4101471]：
$$
\nu_e = \frac{\left.\frac{dE}{dt}\right|_{\mathrm{ROM}} - \left.\frac{dE}{dt}\right|_{\mathrm{DNS}}}{\sum_{i=1}^{m} \beta_{i} a_{i}^{2}(t)}
$$
其中分子是未闭合ROM和DNS参考解之间的能量耗散率差值，分母代表了涡粘项的耗散能力。这种方法确保了ROM在能量上更加符合物理实际。

### 复杂流体降阶模型的高级主题

当我们将ROM应用于复杂的非牛顿流体，如聚合物溶液或熔体时，会出现更多独特的挑战和相应的先进技术。

#### 耦合多物理场系统建模

复杂流体通常涉及多个物理场的紧密耦合。例如，在Oldroyd-B粘弹性流体模型中，流场速度 $\boldsymbol{u}$ 的演化与聚合物构象张量 $\boldsymbol{A}$ 的演化是相互耦合的：速度场通过对流和拉伸来改变聚合物构象，而构象张量产生的弹性应力则反过来作用于流场，改变其动量平衡。

为这类系统构建ROM时，我们需要为每个物理场定义各自的基底。例如，我们可以为速度场构建一组无散度的POD基底 $\boldsymbol{V}_u = \{\boldsymbol{\phi}_i(\boldsymbol{x})\}$，同时为构象张量的扰动部分（$\boldsymbol{A} - \boldsymbol{I}$）构建另一组对称张量场基底 $\boldsymbol{V}_A = \{\boldsymbol{\Psi}_k(\boldsymbol{x})\}$。然后，通过对耦合的动量方程和本构方程同时进行Galerkin投影，我们可以得到一个关于速度模态系数 $a_i(t)$ 和构象模态系数 $b_k(t)$ 的耦合ODE系统 [@problem_id:4101476]。这个系统的结构会清晰地反映出物理场之间的耦合关系，例如，动量方程中会出现由 $b_k$ 驱动的聚合物应力项，而构象方程中则会出现由 $a_i$ 和 $b_k$ 共同决定的对流和拉伸项。

#### 保持物理结构

许多物理量必须满足特定的数学约束。例如，粘弹性模型中的构象张量或形变张量必须是**对称正定 (Symmetric Positive-Definite, SPD)** 的。这个约束源于热力学第二定律，保证了熵增和物理现实性。然而，标准的线性Galerkin投影方法无法自动保证这一关键属性。一个SPD矩阵的近似解 $\boldsymbol{C}_r(t) = \sum b_k(t) \boldsymbol{B}_k$，作为基矩阵的线性组合，其自身通常不是SPD的。这可能导致模型产生非物理的结果甚至崩溃。

**保结构 (structure-preserving)** ROM旨在解决这一问题。其核心思想是通过一个非线性映射，将受约束的变量变换到一个无约束的空间中进行演化，然后再映射回来。对于SPD张量，一个有效的方法是**对数构象映射 (logarithmic conformation mapping)** [@problem_id:4101541]。我们不直接对SPD张量 $C$ 进行降阶，而是对其矩阵对数 $s = \log C$ 进行降阶。对于任何SPD矩阵 $C$，其矩阵对数 $s$ 是一个唯一的实对称矩阵。反之，对于任何实对称矩阵 $s$，其矩阵指数 $C = \exp(s)$ 必然是一个SPD矩阵。

因此，我们可以将ROM构建在无约束的对数空间中，即近似 $s_r(t) = \sum a_k(t) \boldsymbol{B}_k$。通过链式法则推导并投影 $s$ 的演化方程，我们可以得到关于系数 $a_k(t)$ 的ROM。在每个时间步，我们通过矩阵指数运算 $C_r(t) = \exp(s_r(t))$ 来重构构象张量，从而自动保证其SPD性质。这种方法虽然在数学上更为复杂（需要计算矩阵指数、对数及其导数），但它从根本上保证了模型的物理相容性。

#### 处理刚性问题

复杂流体模型，特别是粘弹性模型，往往包含多个特征时间尺度。例如，流体的对流时间尺度可能与聚合物的多个松弛时间尺度存在巨大差异。当这些时间尺度相差悬殊时，描述其动力学的ODE系统就会变得**刚性 (stiff)**。刚性系统对显式时间积分格式的稳定性提出了极为苛刻的要求。

对于一个包含多个松弛时间 $\lambda_i$ 的ROM，若使用像前向欧拉这样的显式格式，其最大稳定时间步长 $\Delta t$ 将受到**最小**松弛时间 $\lambda_{\min}$ 的严格限制，即 $\Delta t \propto \lambda_{\min}$ [@problem_id:4101527]。这意味着为了保证数值稳定，我们必须使用非常小的时间步长来捕捉最快的物理过程，即使我们更关心的是由慢过程主导的长期演化，这导致了巨大的计算浪费。

**隐式-显式 (Implicit-Explicit, IMEX)** 时间积分格式是处理此类刚性问题的有效策略。其思想是将ODE的右端项分解为刚性部分和非刚性部分。对于ROM，刚性部分通常是线性的松弛项（如 $-\Lambda^{-1}\boldsymbol{a}$），而非刚性部分则是非线性的对流和拉伸项。IMEX格式对刚性部分采用无条件稳定的隐式处理，而对计算昂贵的非刚性部分则采用计算高效的显式处理。通过这种分裂，IMEX格式可以显著放宽对时间步长的限制，甚至在某些条件下实现无条件稳定，从而在保证稳定性的同时大幅提高计算效率。