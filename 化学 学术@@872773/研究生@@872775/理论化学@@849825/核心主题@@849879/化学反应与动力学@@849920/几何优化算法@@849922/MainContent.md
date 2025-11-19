## 引言
在现代计算科学的广阔图景中，[几何优化](@entry_id:151817)算法是连接抽象量子力学定律与具体化学现实的核心支柱。无论是预测一个新分子的稳定构型，阐明一个复杂[化学反应](@entry_id:146973)的路径，还是设计具有特定功能的材料，其第一步几乎总是要回答一个基本问题：在[原子核](@entry_id:167902)所有可能的排布中，哪一种构型能量最低？这个在多维[势能面](@entry_id:147441)上寻找能量极小点或[鞍点](@entry_id:142576)的过程，就是[几何优化](@entry_id:151817)的任务。它不仅是理论与计算化学的基石，也是物理、[材料科学](@entry_id:152226)和生物学等领域不可或缺的研究工具。

然而，对于许多研究者而言，[几何优化](@entry_id:151817)算法常常被视为一个“黑箱”：我们输入一个初始猜测结构，然后得到一个优化后的结果，但对其内部的数学原理、不同方法的优劣以及在真实世界应用中可能遇到的陷阱知之甚少。本文旨在打开这个“黑箱”，系统地弥合理论与实践之间的鸿沟。我们将带领读者深入探索控制这些强大算法的底层逻辑，理解它们为何能高效地在复杂的地形图上导航，以及如何应对各种实际挑战。

为实现这一目标，本文将分为三个核心章节。在“原理与机制”中，我们将从[势能面](@entry_id:147441)的基本概念出发，循序渐进地剖析从最速下降法、[牛顿法](@entry_id:140116)到准牛顿法和[信赖域方法](@entry_id:138393)的数学精髓，揭示它们如何构建和利用[势能面](@entry_id:147441)的局部模型。随后，在“应用与交叉学科联系”中，我们将展示这些算法在解决真实科学问题时的威力，探讨它们如何被用于定位过渡态、处理[约束系统](@entry_id:164587)、研究[激发态](@entry_id:261453)，以及它们与先进[电子结构理论](@entry_id:172375)之间深刻的相互依赖关系。最后，通过一系列精心设计的“动手实践”，读者将有机会亲手计算关键的优化步骤，将理论知识转化为解决实际问题的能力。

## 原理与机制

在“引言”章节中，我们已经了解，[几何优化](@entry_id:151817)是理论与[计算化学](@entry_id:143039)的核心任务之一，其目标是在分子的[势能面](@entry_id:147441)上定位能量极小点（对应稳定构型）和[一阶鞍点](@entry_id:165164)（对应过渡态）。本章将深入探讨控制这些优化过程的数学原理和计算机制。我们将从[势能面](@entry_id:147441)的基本特性出发，系统地介绍从最简单的一阶方法到复杂的二阶和准牛顿方法，并讨论如何通过信赖域等策略确保算法的稳定性和效率，最后以实际计算中的[收敛判据](@entry_id:158093)作为结尾。

### [势能面](@entry_id:147441)与[驻点](@entry_id:136617)

在**玻恩–奥本海默近似 (Born–Oppenheimer Approximation)** 下，[原子核](@entry_id:167902)的运动与电子的运动可以被分离。对于一个给定的[原子核](@entry_id:167902)构型 $\mathbf{R}$，我们可以求解[电子薛定谔方程](@entry_id:177999)，得到一个电子能量。这个电子能量，再加上[原子核](@entry_id:167902)之间的经典[库仑排斥](@entry_id:181876)能，就定义了**[势能面](@entry_id:147441) (Potential Energy Surface, PES)**，记为 $E(\mathbf{R})$。具体而言，它是电子[哈密顿算符](@entry_id:144286) $\hat{H}_{e}(\mathbf{R})$ 的[基态](@entry_id:150928)[本征值](@entry_id:154894) $E_{0}^{(e)}(\mathbf{R})$ 与核-核排斥能 $V_{nn}(\mathbf{R})$ 之和 [@problem_id:2894195]：
$$
E(\mathbf{R}) = E_{0}^{(e)}(\mathbf{R}) + V_{nn}(\mathbf{R})
$$
这个 $E(\mathbf{R})$ 是一个关于 $3N$ 个[原子核](@entry_id:167902)坐标（$N$ 为[原子数](@entry_id:746561)）的标量函数，它构成了分子[几何优化](@entry_id:151817)的“[地形图](@entry_id:202940)”。

在经典力学中，作用在[原子核](@entry_id:167902)上的[力是势能的负梯度](@entry_id:168705)，$\mathbf{F} = -\nabla E(\mathbf{R})$。当分子处于一个平衡构型时，每个[原子核](@entry_id:167902)上的净力都为零。这些力为零的点被称为**驻点 (Stationary Points)**，其数学定义为[势能的梯度](@entry_id:173126)向量为零：
$$
\nabla E(\mathbf{R}^{*}) = \mathbf{0}
$$
然而，梯度为零只说明该点是平的，但并未揭示其稳定性。为了区分不同类型的[驻点](@entry_id:136617)，例如稳定的分子结构（**能量极小点**, local minima）和反应的过渡态（**[鞍点](@entry_id:142576)**, saddle points），我们必须考察[势能面](@entry_id:147441)在该点的**曲率 (curvature)**。曲率信息蕴含在能量对坐标的[二阶导数](@entry_id:144508)矩阵中，即**[海森矩阵](@entry_id:139140) (Hessian matrix)**，$\mathbf{H} = \nabla^{2} E(\mathbf{R})$。

对于一个在三维空间中自由运动的分子，其整体的平移和转动并不会改变其内部能量。这意味着[势能面](@entry_id:147441)在对应这些运动的方向上是平的。因此，对于一个[非线性分子](@entry_id:175085)，其 $3N \times 3N$ 的[海森矩阵](@entry_id:139140)总是有6个零[本征值](@entry_id:154894)（3个对应平移，3个对应转动）；对于线性分子则有5个零[本征值](@entry_id:154894)（3个平移，2个转动）。这些零[本征值](@entry_id:154894)对于判断分子内部结构的稳定性没有意义。因此，我们必须在排除了这些外部运动的**内禀坐标 (internal coordinates)** 空间中分析[海森矩阵](@entry_id:139140)。这在数学上等价于将海森矩阵投影到由 $3N-6$（或 $3N-5$）个内禀坐标构成的[子空间](@entry_id:150286)上，并分析这个**投影海森矩阵**的[本征值](@entry_id:154894)。[驻点](@entry_id:136617)的分类如下 [@problem_id:2894195]：

*   **能量极小点 (Local Minimum)**：投影海森矩阵的所有[本征值](@entry_id:154894)均为正。这意味着在任何内部形变方向上，能量都会上升。这对应于一个稳定的分子构型。其海森指数（负[本征值](@entry_id:154894)的数量）为0。

*   **[一阶鞍点](@entry_id:165164) (First-Order Saddle Point)** 或 **过渡态 (Transition State)**：投影海森矩阵恰好有一个负[本征值](@entry_id:154894)。这意味着该结构在一个方向（对应[反应坐标](@entry_id:156248)）上是能量极大点，而在所有其他与之正交的内禀方向上是能量极小点。其海森指数为1。

*   **高阶[鞍点](@entry_id:142576) (Higher-Order Saddle Point)**：投影[海森矩阵](@entry_id:139140)有多于一个（$k \ge 2$）的负[本征值](@entry_id:154894)。这类点在化学中较少作为研究[焦点](@entry_id:174388)。其海森指数为 $k$。

根据西尔维斯特惯性定理(Sylvester’s law of inertia)，矩阵的负、正、零[本征值](@entry_id:154894)的数量在非奇异的[坐标变换](@entry_id:172727)下是不变的。因此，无论我们使用[笛卡尔坐标](@entry_id:167698)、内禀坐标还是[质量加权坐标](@entry_id:164904)，通过海森指数对驻点的分类都是一致的。

### [优化算法](@entry_id:147840)的核心：构建[势能面](@entry_id:147441)的局域模型

所有[几何优化](@entry_id:151817)算法的共同策略，都是在当[前几何](@entry_id:191573)点 $\mathbf{x}_k$ 附近构建一个简化的**局域模型 (local model)** 来近似真实的[势能面](@entry_id:147441)，然后寻找这个模型的极小点作为下一步的位移方向 $\mathbf{p}$。这个局域模型通常通过在 $\mathbf{x}_k$ 点的**泰勒展开 (Taylor expansion)** 得到：
$$
E(\mathbf{x}_k + \mathbf{p}) \approx E(\mathbf{x}_k) + \mathbf{g}_k^{\top}\mathbf{p} + \frac{1}{2}\mathbf{p}^{\top}\mathbf{B}_k\mathbf{p}
$$
其中，$\mathbf{g}_k = \nabla E(\mathbf{x}_k)$ 是梯度，$\mathbf{B}_k$ 是对真实海森矩阵 $\nabla^2 E(\mathbf{x}_k)$ 的一个近似。不同优化算法的区别，本质上在于它们如何构建和使用这个模型。

*   **一阶方法 (First-order methods)**：仅使用到梯度项，即[线性模型](@entry_id:178302) $E(\mathbf{x}_k + \mathbf{p}) \approx E(\mathbf{x}_k) + \mathbf{g}_k^{\top}\mathbf{p}$。
*   **二阶方法 (Second-order methods)**：使用到二阶项，即二次模型。

### 基于梯度的一阶方法与度规

一阶方法只依赖于梯度信息。如果我们试图最小化[线性模型](@entry_id:178302) $E_k + \mathbf{g}_k^{\top}\mathbf{p}$，会发现只要 $\mathbf{p}$ 与 $\mathbf{g}_k$ 的夹角大于90度，$\mathbf{p}$ 的模长越大，能量就越低，这个问题没有有限解。因此，必须对步长 $\|\mathbf{p}\|$ 施加一个约束。**最速下降法 (Steepest Descent, SD)** 正是基于此思想：寻找一个单位长度的步长方向 $\mathbf{u}$，使得能量下降最快。

能量在 $\mathbf{u}$ 方向的[瞬时变化率](@entry_id:141382)（[方向导数](@entry_id:189133)）为 $\nabla E(\mathbf{x})^{\top}\mathbf{u}$。我们的目标是最小化此值，约束条件是步长为单位长度。这里的关键在于，“单位长度”是如何定义的。这引出了**度规 (metric)** 的概念，它定义了我们如何衡量向量的长度和向量之间的距离。

在一个由对称正定矩阵 $\mathbf{M}$ 定义的度规中，向量 $\mathbf{u}$ 的范数（长度）平方为 $\|\mathbf{u}\|_{\mathbf{M}}^2 = \mathbf{u}^{\top}\mathbf{M}\mathbf{u}$。为了找到[最速下降](@entry_id:141858)方向，我们需要求解以下约束优化问题 [@problem_id:2774749]：
$$
\min_{\mathbf{u}} \mathbf{g}^{\top}\mathbf{u} \quad \text{subject to} \quad \mathbf{u}^{\top}\mathbf{M}\mathbf{u} = 1
$$
利用拉格朗日乘子法可以证明，最优方向 $\mathbf{u}$ 与 $-\mathbf{M}^{-1}\mathbf{g}$ 共线。因此，在 $\mathbf{M}$-度规下的最速下降方向为：
$$
\mathbf{p}_{\mathrm{SD}} \propto -\mathbf{M}^{-1}\mathbf{g}
$$
当使用标准的欧几里得度规时，$\mathbf{M}$ 为[单位矩阵](@entry_id:156724) $\mathbf{I}$，[最速下降](@entry_id:141858)方向就是负梯度方向 $-\mathbf{g}$。

在[分子模拟](@entry_id:182701)中，一个物理意义特别重要的度规是**质量加权度规 (mass-weighted metric)**。在这种度规下，原子[质量矩阵](@entry_id:177093) $\mathbf{M}$ 被用作度规张量。这相当于在[质量加权坐标](@entry_id:164904)中采用欧几里得度规。这样做的好处是，优化路径在某种程度上能模拟分子的真实动力学路径，因为[原子核](@entry_id:167902)的惯性被考虑了进来。

最速下降法可以看作是一个离散的迭代过程。如果我们将步长无限缩小，这个过程就演变为一个连续的轨迹，称为**[梯度流](@entry_id:635964) (Gradient Flow)**。该轨迹由一个[常微分方程](@entry_id:147024)描述 [@problem_id:2774749]：
$$
\frac{d\mathbf{q}}{d\tau} = -\mathbf{M}^{-1}\nabla E(\mathbf{q})
$$
其中 $\tau$ 是一个虚拟的“算法时间”。对于一个二次[势能面](@entry_id:147441) $V(\mathbf{q}) = \frac{1}{2}\mathbf{q}^{\top}\mathbf{H}\mathbf{q}$，其梯度为 $\mathbf{H}\mathbf{q}$，[梯度流](@entry_id:635964)方程即为 $\frac{d\mathbf{q}}{d\tau} = -\mathbf{M}^{-1}\mathbf{H}\mathbf{q}$。

#### [坐标系](@entry_id:156346)与度规的联系：Wilson B/G 矩阵

在实践中，我们常常在方便的**内禀坐标**（如键长、键角）中进行思考和分析，而[量子化学](@entry_id:140193)程序则通常在**笛卡尔坐标**中计算能量和梯度。连接这两个[坐标系](@entry_id:156346)的是**威尔逊 B 矩阵 (Wilson B-matrix)**，它定义了内禀坐标的无穷小变化 $d\mathbf{q}$ 与笛卡尔坐标变化 $d\mathbf{R}$ 之间的[线性关系](@entry_id:267880)：$d\mathbf{q} = \mathbf{B}d\mathbf{R}$。

质量加权笛卡尔度规 $ds^2 = d\mathbf{R}^{\top}\mathbf{M}d\mathbf{R}$ 会在内禀坐标空间中诱导出一种新的度规。这个[诱导度规](@entry_id:160616) $\mathbf{g}_{\mathrm{IC}}$ 使得在内禀空间中测量的步长平方 $d\ell^2 = d\mathbf{q}^{\top}\mathbf{g}_{\mathrm{IC}}d\mathbf{q}$ 等于所有能够产生相同 $d\mathbf{q}$ 的笛卡尔位移 $d\mathbf{R}$ 中，质量加权长度最小的那个。可以证明，这个[诱导度规](@entry_id:160616)恰好是**威尔逊 G 矩阵 (Wilson G-matrix)** 的逆 [@problem_id:2774752]：
$$
\mathbf{g}_{\mathrm{IC}} = (\mathbf{B}\mathbf{M}^{-1}\mathbf{B}^{\top})^{-1} = \mathbf{G}^{-1}
$$
这个关系深刻地揭示了分子内部运动的几何结构是如何由原子质量和[分子连接性](@entry_id:182740)共同决定的。例如，对于一个[线性三原子分子](@entry_id:174604) A-B-C，给定原子质量和内禀坐标位移（如一个键伸长，另一个键缩短），我们可以利用 G 矩阵的逆精确计算出这个复合[振动](@entry_id:267781)在质量加[权空间](@entry_id:195741)中的“长度” [@problem_id:2774752]。

### 二阶方法：牛顿-拉夫逊法

[最速下降法](@entry_id:140448)虽然保证能量下降，但在狭长山谷状的[势能面](@entry_id:147441)上会表现出效率低下的“之”字形收敛行为。二阶方法通过利用[势能面](@entry_id:147441)的曲率信息来加速收敛。

**牛顿-拉夫逊法 ([Newton-Raphson](@entry_id:177436), NR)** 直接最小化二次模型 $E_{quad}(\mathbf{p}) = E_k + \mathbf{g}_k^{\top}\mathbf{p} + \frac{1}{2}\mathbf{p}^{\top}\mathbf{H}_k\mathbf{p}$，其中 $\mathbf{H}_k$ 是当前点的**精确**海森矩阵。通过令模型的梯度为零 $\nabla_{\mathbf{p}} E_{quad}(\mathbf{p}) = \mathbf{g}_k + \mathbf{H}_k\mathbf{p} = \mathbf{0}$，我们得到[牛顿步长](@entry_id:177069) $\mathbf{p}_{\mathrm{NR}}$ 的计算公式 [@problem_id:2774735]：
$$
\mathbf{H}_k \mathbf{p}_{\mathrm{NR}} = -\mathbf{g}_k \quad \text{或} \quad \mathbf{p}_{\mathrm{NR}} = -\mathbf{H}_k^{-1}\mathbf{g}_k
$$
将[牛顿步长](@entry_id:177069)代入二次模型，可以得到能量下降的预测值。一个简洁的表达式是 [@problem_id:2774735]：
$$
E_{\text{pred}} = E(\mathbf{x}_k + \mathbf{p}_{\mathrm{NR}}) = E_k + \frac{1}{2}\mathbf{g}_k^{\top}\mathbf{p}_{\mathrm{NR}}
$$
例如，对于一个由伸缩和弯曲坐标描述的二维体系，如果我们知道其在某点的能量、梯度和海森矩阵，就可以通过求解上述线性方程组得到[牛顿步长](@entry_id:177069)，并预测优化一步后的能量 [@problem_id:2774735]。

NR方法的优点是在能量极小点附近具有**二次收敛**性，速度非常快。但其缺点也同样显著：
1.  计算和存储完整的[海森矩阵](@entry_id:139140)成本高昂，对于[大分子](@entry_id:150543)体系几乎不可行。
2.  需要求解一个线性方程组，即对海森矩阵求逆，这本身也是一个计算瓶颈。
3.  如果海森矩阵不是正定的（例如在[鞍点](@entry_id:142576)附近或远离极小点时），[牛顿步长](@entry_id:177069)可能指向能量更高的地方，导致优化失败。

在继续讨论如何克服这些缺点之前，有必要简要提及梯度和[海森矩阵](@entry_id:139140)的来源。根据**海尔曼–费曼定理 (Hellmann–Feynman theorem)**，对于一个精确的[波函数](@entry_id:147440)，作用在[原子核](@entry_id:167902)上的力（梯度的负值）可以通过对[哈密顿算符](@entry_id:144286)求导后取[期望值](@entry_id:153208)得到。然而，在实际计算中，我们通常使用依赖于[原子核](@entry_id:167902)位置的[基组](@entry_id:160309)（例如[高斯基组](@entry_id:198430)）。这时，[基函数](@entry_id:170178)本身对核坐标的导数会引入额外的项，这部分贡献被称为**[普莱力](@entry_id:167194) (Pulay force)**。因此，只有当[基组](@entry_id:160309)不依赖于核坐标（如[平面波基组](@entry_id:178287)）或在[完备基组极限](@entry_id:200862)下，[普莱力](@entry_id:167194)才会消失，梯度计算才简化为简单的海尔曼–费曼形式 [@problem_id:2894232]。

### 准牛顿方法：在成本与效率间取得平衡

为了克服[牛顿法](@entry_id:140116)的缺点，**准牛顿法 (Quasi-Newton, QN)** 应运而生。其核心思想是，不直接计算和存储精确的[海森矩阵](@entry_id:139140)，而是通过优化过程中的梯度信息来**迭代地构建**一个对海森矩阵（或其逆矩阵）的近似。

在每一步迭代中，我们从点 $\mathbf{x}_k$ 移动到 $\mathbf{x}_{k+1} = \mathbf{x}_k + \mathbf{s}_k$，梯度从 $\mathbf{g}_k$ 变为 $\mathbf{g}_{k+1}$。令步长向量 $\mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k$，梯度变化向量 $\mathbf{y}_k = \mathbf{g}_{k+1} - \mathbf{g}_k$。一个好的海森逆[矩阵近似](@entry_id:149640) $\mathbf{H}_{k+1}$ 应该能再现最近一次迭代的梯度变化信息，即满足**[割线条件](@entry_id:164914) (secant condition)** [@problem_id:2774745]：
$$
\mathbf{H}_{k+1}\mathbf{y}_k = \mathbf{s}_k
$$
这个条件有无穷多解。不同的准牛顿方法通过引入额外的约束（如保持对称性、正定性，以及使 $\mathbf{H}_{k+1}$ 与 $\mathbf{H}_{k}$ “尽可能接近”）来确定唯一的更新公式。最著名的几种更新方法包括：

*   **BFGS (Broyden–Fletcher–Goldfarb–Shanno)**：被认为是目前最高效的准牛顿更新方法之一。其逆海森矩阵更新公式为：
    $$
    \mathbf{H}_{k+1}^{\mathrm{BFGS}} = \mathbf{H}_{k} - \frac{\mathbf{H}_{k}\mathbf{y}_{k}\mathbf{s}_{k}^{\top} + \mathbf{s}_{k}\mathbf{y}_{k}^{\top}\mathbf{H}_{k}}{\mathbf{y}_{k}^{\top}\mathbf{s}_{k}} + \left(1 + \frac{\mathbf{y}_{k}^{\top}\mathbf{H}_{k}\mathbf{y}_{k}}{\mathbf{y}_{k}^{\top}\mathbf{s}_{k}}\right) \frac{\mathbf{s}_{k}\mathbf{s}_{k}^{\top}}{\mathbf{y}_{k}^{\top}\mathbf{s}_{k}}
    $$

*   **DFP (Davidon–Fletcher–Powell)**：历史上早于BFGS，结构上与BFGS有对偶关系。
    $$
    \mathbf{H}_{k+1}^{\mathrm{DFP}} = \mathbf{H}_{k} + \frac{\mathbf{s}_{k}\mathbf{s}_{k}^{\top}}{\mathbf{s}_{k}^{\top}\mathbf{y}_{k}} - \frac{\mathbf{H}_{k}\mathbf{y}_{k}\mathbf{y}_{k}^{\top}\mathbf{H}_{k}}{\mathbf{y}_{k}^{\top}\mathbf{H}_{k}\mathbf{y}_{k}}
    $$

*   **SR1 (Symmetric Rank-One)**：最简单的对称更新公式，但不保证[正定性](@entry_id:149643)。
    $$
    \mathbf{H}_{k+1}^{\mathrm{SR1}} = \mathbf{H}_{k} + \frac{(\mathbf{s}_{k} - \mathbf{H}_{k}\mathbf{y}_{k})(\mathbf{s}_{k} - \mathbf{H}_{k}\mathbf{y}_{k})^{\top}}{(\mathbf{s}_{k} - \mathbf{H}_{k}\mathbf{y}_{k})^{\top}\mathbf{y}_{k}}
    $$

通过一个具体的二维例子，我们可以清楚地看到，即使从相同的初始近似（如[单位矩阵](@entry_id:156724)）出发，这三种方法在经历完全相同的步长 $\mathbf{s}_k$ 和梯度变化 $\mathbf{y}_k$ 后，会产生不同的[逆海森矩阵近似](@entry_id:634022) [@problem_id:2774745]。

对于非常大的分子体系，即使是存储 $N \times N$ 的近似海森矩阵也变得不切实际。为此，**[有限内存BFGS](@entry_id:167263) (Limited-memory BFGS, [L-BFGS](@entry_id:167263))** 方法被开发出来。[L-BFGS](@entry_id:167263) 不存储完整的 $\mathbf{H}_k$ 矩阵，而只存储最近的 $m$ 个步长向量 $\{\mathbf{s}_i\}$ 和梯度变化向量 $\{\mathbf{y}_i\}$（$m$ 通常是一个小数，如5-20）。然后，通过一个巧妙的**两圈[递归算法](@entry_id:636816) (two-loop recursion)**，它可以直接计算出搜索方向 $\mathbf{p}_k = -\mathbf{H}_k\mathbf{g}_k$，而无需显式地构建 $\mathbf{H}_k$。这个过程仅涉及向量的[点积](@entry_id:149019)和[线性组合](@entry_id:154743)，其计算成本与体系大小成线性关系，极大地扩展了准牛顿方法在高维问题中的应用范围 [@problem_id:2774737]。

### [信赖域方法](@entry_id:138393)：确保算法的[全局收敛性](@entry_id:635436)

无论是[牛顿法](@entry_id:140116)还是准牛顿法，它们所依赖的二次模型都只是一个局域近似。当优化进行到远离能量极小点的区域，或者在曲率复杂的区域（如[鞍点](@entry_id:142576)附近），这个模型可能非常不准确。直接采用模型给出的步长（如[牛顿步长](@entry_id:177069)）可能会导致能量上升，使优化发散。

**[信赖域方法](@entry_id:138393) (Trust-Region, TR)** 提供了一个强大的框架来解决这个问题。其核心思想是：我们只在相信二次模型足够准确的“信赖域”内部来最小化它。这个信赖域通常是一个以当前点为中心、半径为 $\Delta$ 的球形区域。因此，每一步的优化都转化为求解一个**[信赖域子问题](@entry_id:168153)**：
$$
\min_{\mathbf{p}} m(\mathbf{p}) = E_k + \mathbf{g}_k^{\top}\mathbf{p} + \frac{1}{2}\mathbf{p}^{\top}\mathbf{B}_k\mathbf{p} \quad \text{subject to} \quad \|\mathbf{p}\| \le \Delta
$$
信赖域半径 $\Delta$ 会根据上一步模型预测的能量下降与实际能量下降的吻合程度动态调整。如果吻合得好，说明模型可靠，可以扩大信赖域；如果吻合得差，则说明模型不可靠，需要缩小信赖域。

[信赖域子问题](@entry_id:168153)的精确解可以通过[拉格朗日乘子法](@entry_id:176596)得到。其 [Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)要求[最优步长](@entry_id:143372) $\mathbf{p}^*$ 满足：
$$
(\mathbf{B}_k + \lambda \mathbf{I})\mathbf{p}^* = -\mathbf{g}_k
$$
其中 $\lambda \ge 0$ 是拉格朗日乘子，且满足 $\lambda(\Delta^2 - \|\mathbf{p}^*\|^2) = 0$（互补松弛条件）。一个至关重要的特性是，矩阵 $(\mathbf{B}_k + \lambda \mathbf{I})$ 必须是半正定的。这意味着，即使原始的 $\mathbf{B}_k$ 含有负[本征值](@entry_id:154894)（例如在[鞍点](@entry_id:142576)附近），通过增加一个足够大的 $\lambda$，TR框架也能自动“修正”曲率，找到一个有效的下降方向。一个在[鞍点](@entry_id:142576)附近的[优化步长](@entry_id:752988)计算清楚地展示了这一点：当[牛顿法](@entry_id:140116)因[海森矩阵](@entry_id:139140)不定而失效时，[信赖域方法](@entry_id:138393)通过在边界上寻找解，并由一个正的[拉格朗日乘子](@entry_id:142696) $\lambda=2$ 来保证有效[海森矩阵](@entry_id:139140)的正定性，从而得到一个合理的步长 [@problem_id:2774743]。

精确求解[信赖域子问题](@entry_id:168153)可能很复杂。在实践中，人们常常使用近似策略，**[狗腿法](@entry_id:139912) (dogleg method)** 就是其中最流行的一种。它通过构造一条连接[最速下降](@entry_id:141858)点和牛顿点的折线路径来近似[最优步长](@entry_id:143372)。
1.  计算**[柯西点](@entry_id:177064) (Cauchy point)** $\mathbf{p}_u$，它是在最速下降方向上（即 $-\mathbf{g}_k$ 方向）二次模型的极小点。
2.  计算**牛顿点 (Newton point)** $\mathbf{p}_B = -\mathbf{B}_k^{-1}\mathbf{g}_k$。
3.  狗腿路径就是从原点到 $\mathbf{p}_u$，再从 $\mathbf{p}_u$ 到 $\mathbf{p}_B$ 的折线。
最终的步长就是这条路径与信赖域边界的交点。例如，当信赖域半径介于[柯西点](@entry_id:177064)和牛顿点的模长之间时（$\|\mathbf{p}_u\| \lt \Delta \lt \|\mathbf{p}_B\|$），步长就位于连接 $\mathbf{p}_u$ 和 $\mathbf{p}_B$ 的线段上，其具体位置可以通过求解一个简单的[二次方程](@entry_id:163234)来确定 [@problem_id:2774747]。

### 终点线：[收敛判据](@entry_id:158093)

[几何优化](@entry_id:151817)是一个迭代过程，那么我们应该在什么时候停止呢？选择合适的**[收敛判据](@entry_id:158093) (convergence criteria)** 至关重要。一个好的判据不仅要确认算法已经无法再取得进展，更要确保找到的点在[数值精度](@entry_id:173145)范围内满足[驻点](@entry_id:136617)的物理和数学条件。

不充分的判据，例如仅判断能量变化或步长大小，是不可靠的。能量变化很小可能只是因为[势能面](@entry_id:147441)平坦，或者算法陷入了停滞，而此时梯度可能依然很大。一个鲁棒的[收敛判据](@entry_id:158093)通常会同时检查多个条件 [@problem_id:2774748]：

1.  **梯度的模长**：梯度（力）应该足够小。考虑到梯度计算本身存在数值噪声（例如，由于电子自洽场收敛不完全），一个合理的判据是要求梯度的最大分量（或[均方根](@entry_id:263605)）小于某个阈值，这个阈值通常是梯度计算噪声的几倍。例如，当梯度的最大分量 $\lVert \mathbf{g}_{k+1}\rVert_{\infty}$ 小于 $3 \times \epsilon_g$（$\epsilon_g$是[梯度噪声](@entry_id:165895)的界限）时，我们可以认为梯度在数值上已经为零。

2.  **步长的模长**：最后一步的位移应该足够小。这表明优化过程已经收敛到一个点附近。

3.  **能量的变化**：连续几步的能量变化应该非常小。

对于寻找**能量极小点**，除了上述条件，还必须满足**[二阶条件](@entry_id:635610)**，即确认[海森矩阵](@entry_id:139140)是正定的。这可以通过检查其最低[本征值](@entry_id:154894)是否为正来实现。在实际操作中，可以对近似[海森矩阵](@entry_id:139140)的最低[本征值](@entry_id:154894)进行估算，并确保其在考虑了[数值不确定性](@entry_id:752838)后仍然是正的。例如，如果估算的最小曲率 $\kappa_{\min}$ 及其不确定度为 $0.04 \pm 0.01$，那么只要 $0.04 - 0.01 = 0.03 > 0$，我们就可以相信该点是一个真正的能量极小点 [@problem_id:2774748]。

只有当这些基于梯度、步长、能量和曲率的条件同时得到满足时，我们才能有信心地宣布，优化算法已经成功地定位了一个符合理论定义的[驻点](@entry_id:136617)。