## 引言
[纤维增强](@entry_id:194439)软组织，如动脉壁、皮肤和大脑白质，其卓越的力学功能源于其复杂的微观结构，尤其是其中胶原或神经纤维的精妙排布。然而，在[连续介质力学](@entry_id:155125)的框架内，如何精确地描述这些离散纤维网络（特别是其方向的分散性），并将其与材料的宏观力学行为联系起来，始终是生物力学领域的一个核心挑战。本文旨在系统性地解决这一知识鸿沟，为读者提供一个关于微观结构与纤维分散建模的全面指南。

本文将分为三个核心章节，引导读者从基础理论逐步深入到前沿应用与实践。在“原理与机制”一章中，我们将建立描述纤维方向分布的数学语言，引入结构张量的概念，并探讨如何通过均匀化方法构建基于微观结构的[本构模型](@entry_id:174726)。接着，在“应用与交叉学科联系”一章中，我们将展示这些理论模型在心血管生物力学、神经科学、医学成像和工程材料等领域的强大应用价值，揭示“结构-功能”关系的核心联系。最后，在“动手实践”部分，我们将通过一系列计算练习，帮助读者将理论知识转化为解决实际问题的编程与建模技能。通过本文的学习，读者将掌握连接微观结构与宏观性能的关键建模思想和技术。

## 原理与机制

在对[纤维增强](@entry_id:194439)软组织（如动脉壁、皮肤和韧带）进行[生物力学建模](@entry_id:923560)时，一个核心挑战在于如何将离散的、具有复杂空间排布的微观结构（如胶原纤维）与宏观的连续介质力学描述联系起来。本章旨在系统地阐述描述和建模纤维网络微观结构的关键原理与机制。我们将从纤维方向分布的基本数学描述出发，逐步深入到如何将这些分布整合到本构方程中，并探讨一些使模型更贴近生物学现实的必要高级概念。

### 纤维方向的概率描述

生物软组织中的胶原纤维通常并非整齐划一地排列，而是以一定的分散程度分布在组织中。为了在[连续介质力学](@entry_id:155125)的框架内捕捉这种微观结构特征，我们首先需要一种数学语言来描述纤维的方向分布。

#### 方向[分布函数](@entry_id:145626) (ODF)

我们将每根纤维的方向理想化为一个三维[单位向量](@entry_id:165907) $\mathbf{a}$，满足 $\|\mathbf{a}\|=1$。因此，所有可能的纤维方向构成了[单位球](@entry_id:142558)面 $S^2$。纤维网络的方向分散性可以通过一个定义在[单位球](@entry_id:142558)面上的**方向分布函数 (Orientation Distribution Function, ODF)** $p(\mathbf{a})$ 来进行统计描述。

作为一个概率密度函数 (PDF)，$p(\mathbf{a})$ 必须满足两个基本条件 ：
1.  **非负性**: 对于任意方向 $\mathbf{a} \in S^2$，[概率密度](@entry_id:175496)必须是非负的，即 $p(\mathbf{a}) \ge 0$。
2.  **归一化**: 在整个[样本空间](@entry_id:275301)（即[单位球](@entry_id:142558)面）上对 $p(\mathbf{a})$ 进行积分，总概率必须为1。这表示为：
    $$
    \int_{S^2} p(\mathbf{a})\,\mathrm{d}\Omega = 1
    $$
    其中 $\mathrm{d}\Omega$ 是[单位球](@entry_id:142558)面上的面元。在[球坐标系](@entry_id:167517)中，若用极角 $\theta \in [0, \pi]$ 和[方位角](@entry_id:164011) $\varphi \in [0, 2\pi)$ 来[参数化](@entry_id:265163)[单位向量](@entry_id:165907) $\mathbf{a}$，则面元为 $\mathrm{d}\Omega = \sin\theta\,\mathrm{d}\theta\,\mathrm{d}\varphi$。整个[单位球](@entry_id:142558)面的面积为 $\int_{S^2} \mathrm{d}\Omega = 4\pi$。

此外，对于大多数生物纤维（如胶原纤维），其力学行为不区分方向的“头”和“尾”。这意味着沿 $\mathbf{a}$ 方向和沿 $-\mathbf{a}$ 方向的纤维是物理上等效的。这一特性被称为**头尾对称性 (head-tail symmetry)**。为了使 ODF 反映这一物理现实，它必须是一个[偶函数](@entry_id:163605)，满足：
$$
p(\mathbf{a}) = p(-\mathbf{a})
$$
这一对称性对纤维网络的力学行为有着深远的影响。例如，它直接导致所有奇数阶的方向矩张量为零。最简单的例子是一阶矩，它代表了平均纤维[方向向量](@entry_id:169562)：
$$
\langle \mathbf{a} \rangle = \int_{S^2} p(\mathbf{a})\,\mathbf{a}\,\mathrm{d}\Omega = \mathbf{0}
$$
这个积分之所以为零，是因为对于球面上每一点 $\mathbf{a}$ 的贡献 $p(\mathbf{a})\mathbf{a}$，总有其对跖点 $-\mathbf{a}$ 的一个贡献 $p(-\mathbf{a})(-\mathbf{a}) = -p(\mathbf{a})\mathbf{a}$ 与之抵消 。

最简单的 ODF 是**各向同性 (isotropic)** 或均匀分布，此时纤维在所有方向上出现的概率均等。为了满足[归一化条件](@entry_id:156486)，其[概率密度](@entry_id:175496)必须是一个常数 $p(\mathbf{a}) = 1/(4\pi)$。

### 结构张量：量化方向分布

虽然 ODF 提供了纤维方向分布的完整信息，但在本构模型中直接使用它往往会导致复杂的积分运算。一种更简洁且实用的方法是使用 ODF 的矩，即**结构张量 (structure tensors)** 或方向张量，来表征微观结构的各向异性。

第 $n$ 阶结构张量定义为 $\mathbf{a}$ 的 $n$ 次[张量积](@entry_id:140694)的统计平均值：
$$
\mathbb{A}^{(n)} = \langle \underbrace{\mathbf{a} \otimes \mathbf{a} \otimes \dots \otimes \mathbf{a}}_{n \text{ times}} \rangle = \int_{S^2} (\mathbf{a} \otimes \dots \otimes \mathbf{a})\, p(\mathbf{a})\,\mathrm{d}\Omega
$$

在生物力学中，最常用的是二阶和四阶结构张量。

#### 二阶结构张量

二阶结构张量 $\mathbf{A} \equiv \mathbb{A}^{(2)}$ 定义为：
$$
\mathbf{A} = \langle \mathbf{a} \otimes \mathbf{a} \rangle = \int_{S^2} (\mathbf{a} \otimes \mathbf{a})\, p(\mathbf{a})\,\mathrm{d}\Omega
$$
它是一个[对称张量](@entry_id:148092) ($\mathbf{A} = \mathbf{A}^\top$)，其迹为1，因为 $\mathrm{tr}(\mathbf{A}) = \langle \mathrm{tr}(\mathbf{a} \otimes \mathbf{a}) \rangle = \langle \mathbf{a} \cdot \mathbf{a} \rangle = \langle 1 \rangle = 1$。$\mathbf{A}$ 的本征值和[本征向量](@entry_id:151813)描述了纤维分布的主要方向和离散程度。

-   对于**各向同性**分布，$p(\mathbf{a})=1/(4\pi)$，二阶结构张量为 ：
    $$
    \mathbf{A}_{\text{iso}} = \frac{1}{4\pi} \int_{S^2} (\mathbf{a} \otimes \mathbf{a})\,\mathrm{d}\Omega = \frac{1}{3}\mathbf{I}
    $$
    其中 $\mathbf{I}$ 是二阶单位张量。

-   对于**完美单向排列**，即所有纤维都沿一个优先方向 $\mathbf{m}$ 排列，ODF 为狄拉克 $\delta$ 函数 $p(\mathbf{a}) = \delta(\mathbf{a}-\mathbf{m})$。此时的二阶结构张量为：
    $$
    \mathbf{A}_{\text{aligned}} = \int_{S^2} (\mathbf{a} \otimes \mathbf{a})\, \delta(\mathbf{a}-\mathbf{m})\,\mathrm{d}\Omega = \mathbf{m} \otimes \mathbf{m}
    $$

#### 四阶结构张量

四阶结构张量 $\mathbb{A}^{(4)}$ 在推导材料的[切线](@entry_id:268870)模量时至关重要，其定义为 ：
$$
\mathbb{A}^{(4)} = \langle \mathbf{a} \otimes \mathbf{a} \otimes \mathbf{a} \otimes \mathbf{a} \rangle
$$
其分量形式为 $\mathbb{A}_{ijkl} = \langle a_i a_j a_k a_l \rangle$。这个张量具有完全的索引对称性。对于各向同性分布，其形式可以被唯一确定。通过[张量表示](@entry_id:180492)定理和适当的缩并运算，可以证明其形式为：
$$
\mathbb{A}^{(4)}_{\text{iso}, ijkl} = \frac{1}{15} (\delta_{ij}\delta_{kl} + \delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk})
$$
其中 $\delta_{ij}$ 是克罗内克符号。这个结果的正确性可以通过一次缩并来验证：$\mathbb{A}^{(4)}_{\text{iso}, ijkk} = \langle a_i a_j (\mathbf{a}\cdot\mathbf{a}) \rangle = \langle a_i a_j \rangle = A_{\text{iso}, ij} = \frac{1}{3}\delta_{ij}$，与对上式进行缩并的结果一致 。在后续的本构模型推导中，我们会看到这个张量如何自然地出现。

### 纤维方向分布的具体模型

为了进行定量计算，我们需要为 ODF $p(\mathbf{a})$ 设定具体函数形式。这主要有两种途径：一种是基于统计力学的显式[分布函数](@entry_id:145626)，另一种是基于唯象观察的结构张量[参数化](@entry_id:265163)。

#### 显式 ODF 模型：von Mises–Fisher 分布

对于具有一个优先方向 $\mathbf{m}$ 的横观[各向同性材料](@entry_id:170678)，**von Mises–Fisher (vMF) 分布** 是一个广泛应用的模型 。它的形式类似于正态分布在球面上的推广：
$$
p(\mathbf{a}; \kappa, \mathbf{m}) = c(\kappa) \exp(\kappa\, \mathbf{m} \cdot \mathbf{a})
$$
这里的 $\kappa \ge 0$ 是一个**集中参数**，它描述了纤维方向在优先方向 $\mathbf{m}$ 附近的集中程度。$\kappa$ 越大，分布越集中。$c(\kappa)$ 是[归一化常数](@entry_id:752675)，通过对 $p(\mathbf{a})$ 在整个球[面积分](@entry_id:275394)为1来确定。通过在以 $\mathbf{m}$ 为极轴的[球坐标系](@entry_id:167517)中进行积分，可以推导出 ：
$$
c(\kappa) = \frac{\kappa}{4\pi\sinh(\kappa)}
$$

vMF 分布的两个极限情况清晰地揭示了参数 $\kappa$ 的物理意义：
-   **最大[分散度](@entry_id:163107) ($\kappa \to 0$)**: 当 $\kappa \to 0$ 时，$\sinh(\kappa) \approx \kappa$，因此 $c(\kappa) \to 1/(4\pi)$。此时 $p(\mathbf{a}) \to 1/(4\pi)$，分布趋于各向同性。这代表了完全随机的纤维取向。
-   **最小[分散度](@entry_id:163107) ($\kappa \to \infty$)**: 当 $\kappa \to \infty$ 时，分布变得在 $\mathbf{m}$ 方向上高度集中。利用[小角度近似](@entry_id:145423) $\cos\theta \approx 1-\theta^2/2$，可以证明 ODF 趋于一个以 $\mathbf{m}$ 为中心的狄拉克 $\delta$ 函数，代表所有纤维完美对齐。

#### [唯象模型](@entry_id:1129607)：Gasser-Ogden-Holzapfel (GOH) 结构张量

在许多应用中，尤其是动脉[血管力学](@entry_id:1133731)，研究者们发现直接对二阶结构张量进行[参数化](@entry_id:265163)是一种高效且有效的方法。**Gasser-Ogden-Holzapfel (GOH)** 模型采用的就是这种思路 。它假设二阶结构张量（在GOH文献中常记为 $\mathbf{H}$）具有如下形式：
$$
\mathbf{H} = \kappa \mathbf{I} + (1-3\kappa) (\mathbf{m} \otimes \mathbf{m})
$$
这里的 $\kappa \in [0, 1/3]$ 是一个唯象的**分散参数**（注意此处的 $\kappa$ 与 vMF 分布的集中参数不同，其物理意义更接近于[分散度](@entry_id:163107)）。这个简洁的表达式巧妙地在两个极端情况之间进行[线性插值](@entry_id:137092)：
-   当 $\kappa=0$ 时，$\mathbf{H} = \mathbf{m} \otimes \mathbf{m}$，代表**完美对齐**。
-   当 $\kappa=1/3$ 时，$\mathbf{H} = \frac{1}{3}\mathbf{I}$，代表**各向同性**。

通过分析该张量的谱（即本征值和[本征向量](@entry_id:151813)），可以更深入地理解其结构。$\mathbf{H}$ 的一个[本征向量](@entry_id:151813)是优先方向 $\mathbf{m}$，对应的本征值为 $1-2\kappa$；另外两个本征值相等，均为 $\kappa$，对应的[本征空间](@entry_id:147356)是垂直于 $\mathbf{m}$ 的平面 。只要 $\kappa \in [0, 1/3]$，本征值 $1-2\kappa$ 就大于 $\kappa$，表明纤维分布在方向 $\mathbf{m}$ 上更为集中。

#### 连接显式与[唯象模型](@entry_id:1129607)

这两种看似不同的方法实际上是紧密相连的。我们可以通过计算 vMF 分布的二阶矩张量 $\mathbf{A}$，并将其与GOH模型中的[参数化](@entry_id:265163)形式进行比较，从而在两种模型的参数之间建立联系 。

对 vMF 分布进行积分可以得到其二阶矩张量 $\mathbf{A}$。由于其关于 $\mathbf{m}$ [轴对称](@entry_id:1130776)，$\mathbf{A}$ 必然具有横观各向同性的形式：
$$
\mathbf{A} = A_\perp \mathbf{I} + (A_\| - A_\perp) (\mathbf{m} \otimes \mathbf{m})
$$
其中 $A_\|$ 和 $A_\perp$ 分别是沿 $\mathbf{m}$ 方向和垂直于 $\mathbf{m}$ 方向的对角分量。通过复杂的积分运算可以得到它们的具体表达式，它们都是 vMF 集中参数 $\kappa_{vMF}$ 的函数。

另一方面，我们可以引入一个**对齐参数** $\alpha \in [0,1]$ 来重新[参数化](@entry_id:265163)这个张量，使其形式更直观：
$$
\mathbf{A} = \frac{1-\alpha}{3} \mathbf{I} + \alpha (\mathbf{m} \otimes \mathbf{m})
$$
这种形式清楚地表示了 $\mathbf{A}$ 是各向同性部分 ($\frac{1}{3}\mathbf{I}$) 和完美对齐部分 ($\mathbf{m}\otimes\mathbf{m}$) 的加权平均。当 $\alpha=0$ 时为各向同性，$\alpha=1$ 时为完美对齐。通过比较两种形式的系数，我们可以建立起 vMF 集中参数 $\kappa_{vMF}$ 和对齐参数 $\alpha$ 之间的一一对应关系 ：
$$
\alpha(\kappa_{vMF}) = 1 + \frac{3}{\kappa_{vMF}^2} - \frac{3\cosh(\kappa_{vMF})}{\kappa_{vMF}\sinh(\kappa_{vMF})}
$$
这个关系式为看似抽象的统计分布参数赋予了清晰的物理和几何意义，并允许研究者在基于物理的 ODF 模型和计算上更便捷的[唯象模型](@entry_id:1129607)之间进行切换。

### 微观结构在宏观本构中的体现

描述了微观结构之后，我们的最终目标是构建能够预测材料宏观力学行为的本构模型。这通常通过**均匀化 (homogenization)** 方法实现。

#### 能量平均与应变能函数

均匀化理论的一个核心假设是**[尺度分离](@entry_id:270204) (separation of scales)** 。它假定存在一个代表性体积元 (RVE)，这个 RVE 足够大，能够包含具有统计代表性的微观结构特征（如大量纤维）；同时又足够小，使得宏观的变形梯度 $\mathbf{F}$ 在该单元内可被视为常数。

基于此假设，复合材料的宏观[应变能密度](@entry_id:200085) $W_{\text{hom}}$ 可以通过对各组分应变能的[体积平均](@entry_id:1133895)（或在我们的例子中，方向平均）得到。对于一个由基质和纤维组成的复合材料，其[应变能](@entry_id:162699)可以写为两部分之和：
$$
W_{\text{hom}} = W_{\text{matrix}} + \overline{W}_{\text{fiber}}
$$
其中 $\overline{W}_{\text{fiber}}$ 是纤维贡献的平均[应变能](@entry_id:162699)，通过对单根纤维的[应变能](@entry_id:162699) $w_f$ 在所有方向上进行积分得到：
$$
\overline{W}_{\text{fiber}} = \langle w_f \rangle = \int_{S^2} w_f(\mathbf{a}, \mathbf{C})\,p(\mathbf{a})\,\mathrm{d}\Omega
$$
这里 $\mathbf{C} = \mathbf{F}^\top\mathbf{F}$ 是右柯西-格林变形张量。单根纤维的应变通常取决于其自身方向上的拉伸。在最简单的**仿射运动假设 (affine kinematics assumption)**下，纤维的拉伸比 $\lambda_f$ 直接由宏观变形决定：$\lambda_f = \sqrt{\mathbf{a}\cdot\mathbf{C}\cdot\mathbf{a}}$。这个量也常写作伪不变量 $I_4(\mathbf{a}) = \lambda_f^2 = \mathbf{a}\cdot\mathbf{C}\cdot\mathbf{a}$。

以一个各向同性分布的纤维网络为例，假设单根纤维的[应变能](@entry_id:162699)为 $w_f = \frac{\gamma}{2}(I_4-1)^2$ 。为了计算平均纤维能 $\overline{W}_{\text{fiber}}$，我们需要计算 $\langle (I_4-1)^2 \rangle = \langle I_4^2 \rangle - 2\langle I_4 \rangle + 1$。这需要计算 $I_4$ 的一阶和二阶矩：
-   $\langle I_4 \rangle = \langle \mathbf{a}\cdot\mathbf{C}\cdot\mathbf{a} \rangle = C_{ij}\langle a_i a_j \rangle = \mathbf{C}:\mathbb{A}^{(2)}$
-   $\langle I_4^2 \rangle = \langle (\mathbf{a}\cdot\mathbf{C}\cdot\mathbf{a})^2 \rangle = C_{ij}C_{kl}\langle a_i a_j a_k a_l \rangle = (\mathbf{C}\otimes\mathbf{C}):\mathbb{A}^{(4)}$

对于各向同性情况，$\mathbb{A}^{(2)} = \frac{1}{3}\mathbf{I}$，$\mathbb{A}^{(4)}$ 采用我们之前导出的形式。代入后即可得到 $\overline{W}_{\text{fiber}}$ 完全由 $\mathbf{C}$ 的不变量 (如 $I_1=\mathrm{tr}(\mathbf{C})$ 和 $\mathrm{tr}(\mathbf{C}^2)$) 表达的宏观[应变能函数](@entry_id:178435) 。

#### 数值实现：微球模型

直接对 ODF 进行连续积分在[有限元分析](@entry_id:138109)等数值计算中是不可行的。**微球模型 (microsphere model)** 提供了一种高效的[数值近似方法](@entry_id:169303) 。其核心思想是用一个基于特定方向 $\mathbf{a}_i$ 和相应权重 $w_i$ 的离散求和来代替球面积分：
$$
\int_{S^2} f(\mathbf{a})\, p(\mathbf{a})\,\mathrm{d}\Omega \approx \sum_{i=1}^N w_i f(\mathbf{a}_i)
$$
为了保证[数值积分](@entry_id:136578)的精度，积分点和权重的选择需要满足一定的**[矩匹配](@entry_id:144382) (moment matching)** 条件。即，对于一组选定的基函数（通常是 $\mathbf{a}$ 的[笛卡尔](@entry_id:925811)分量的多项式），离散求和必须能精确地重现连续积分的结果。例如，为了精确模拟[各向同性材料](@entry_id:170678)直到四阶多项式的积分，积分方案 $\{\mathbf{a}_i, w_i\}$ 必须满足 ：
-   零阶矩: $\sum w_i = \int p(\mathbf{a}) \mathrm{d}\Omega = 1$ (如果 $p(\mathbf{a})$ 已经包含在 $w_i$ 中)。
-   二阶矩: $\sum w_i (\mathbf{a}_i \otimes \mathbf{a}_i) = \mathbb{A}^{(2)}_{\text{iso}} = \frac{1}{3}\mathbf{I}$。
-   四阶矩: $\sum w_i (\mathbf{a}_i \otimes \mathbf{a}_i \otimes \mathbf{a}_i \otimes \mathbf{a}_i) = \mathbb{A}^{(4)}_{\text{iso}}$。

有多种对称的积分方案可以满足这些条件。一个经典的例子是基于正二十面体顶点的12点积分格式，它可以精确到5阶多项式，因此足以满足上述要求。找到满足特定阶数精度且积分点数 $N$ 最少的方案是球面设计理论中的一个重要问题。对于四阶精度，理论上最少需要12个点 。

### 模型的生物学改进

上述基本框架为构建微观结构模型奠定了基础。然而，为了更准确地模拟真实生物组织的行为，还需要引入一些更精细的物理机制。

#### 纤维卷曲与募集

生物组织中的胶原纤维在无载荷状态下通常不是绷直的，而是呈波浪状或卷曲状。这意味着纤维只有在被拉伸到超过其初始卷曲长度后，才能开始承受拉力。这个开始承力的拉伸比被称为**松弛拉伸比 (slack stretch)** $\lambda_s \ge 1$。

由于组织中纤维的卷曲程度各不相同，我们可以引入一个**松弛拉伸比分布** $\rho(\lambda_s)$ 来描述这种差异性 。这个分布可以从更基本的微观结构特征（如卷[曲波](@entry_id:748118)幅 $a$）的分布 $f_a(a)$，通过变量变换得到。例如，如果假设 $\lambda_s = 1 + \kappa a$，其中 $a$ 服从[瑞利分布](@entry_id:184867)，我们就可以推导出 $\rho(\lambda_s)$ 的具体形式。

在给定的纤维拉伸比 $\lambda_f$ 下，只有那些松弛拉伸比 $\lambda_s \le \lambda_f$ 的纤维被“募集”并参与承载。被**募集的纤维比例** $F(\lambda_f)$ 就等于 $\rho(\lambda_s)$ 的[累积分布函数 (CDF)](@entry_id:264700)：
$$
F(\lambda_f) = P(\lambda_s \le \lambda_f) = \int_1^{\lambda_f} \rho(x)\,\mathrm{d}x
$$
这个**渐进募集 (progressive recruitment)** 机制是解释软组织典型的“J”形[应力-应变曲线](@entry_id:159459)的关键，即材料在小变形时非常柔软，随着变形增加，越来越多的纤维被募集，导致刚度急剧增加 。将募集模型整合到应变能函数中，通常需要对单纤维能量进行双重积分（对方向和松弛拉伸比积分）。

#### 非仿射运动

标准的仿射运动假设虽然简化了计算，但可能不完全符合物理现实，尤其是在基质非常柔软而纤维非常坚硬的复合材料中 。仿射假设强制纤维跟随宏观变形，这会过度惩罚与纤维方向横向的变形。例如，在[单轴拉伸](@entry_id:188287)下，一个横向排列的纤维会被强制承受压缩，而在真实材料中，柔软的基质很可能会通过[剪切变形](@entry_id:170920)来“绕开”这根硬纤维，从而使纤维本身几乎不发生变形。

因此，仿射假设往往会**高估材料的横向刚度**。为了修正这一点，可以引入**非仿射运动 (non-affine kinematics)** 的概念。一种简单的方法是引入一个依赖于方向的修正因子 $\eta(\mathbf{a})$，来调整纤维感受到的实际变形：
$$
I_{4}^{\text{na}} = 1 + \eta(\mathbf{a}) (I_4 - 1)
$$
其中 $\eta(\mathbf{a}) \in [0,1]$ 代表了仿射变形被“传递”给纤维的比例。$\eta=1$ 恢复仿射假设，$\eta=0$ 表示纤维完全不随宏观变形而变形。$\eta$ 的物理性质应该遵循以下原则 ：
-   它应取决于纤维与基质的相对刚度。基质越硬，变形越接近仿射，$\eta \to 1$。
-   它应取决于纤维的方向。当纤维方向与主拉伸方向一致时，变形接近仿射，$\eta \approx 1$。当纤维方向与主拉伸方向垂直时，非仿射效应最显著，$\eta$ 最小。

一个符合这些物理直觉的唯象模型可以写作：
$$
\eta(\theta) = \frac{G_m}{G_m + E_f \sin^2\theta}
$$
其中 $G_m$ 和 $E_f$ 分别是基质和纤维的模量，$\theta$ 是纤维与主拉伸方向的夹角。这个模型正确地捕捉了非仿射效应随方向和材料属性变化的趋势，为构建更具物理真实感的[本构模型](@entry_id:174726)提供了重要思路。