## 引言
在生物力学、材料科学及工程领域，理解物体内部力的分布与传递方式是分析其行为、预测其性能和确保其[结构完整性](@entry_id:165319)的核心。当一块骨骼承受体重，或当血管壁抵抗血压时，其内部的每一个点都处在一个复杂的、多方向的受力状态中。如何精确地量化并分析这种内部力的状态？这正是连续介质力学所要解决的根本问题，而柯西应力张量理论为我们提供了优雅而强大的解答。

本文旨在系统性地介绍描述应力状态的核心工具。我们将深入探讨柯西应力张量、[主应力](@entry_id:176761)以及[莫尔圆](@entry_id:168131)这些基石性概念。我们将分三个层次展开：首先，在“原理和机制”一章中，我们将从第一性原理出发，建立[应力张量](@entry_id:148973)的数学框架，并探讨其内在属性。接着，在“应用与交叉学科联系”一章中，我们将通过丰富的实例，展示这些理论如何在生物力学、临床医学及工程实践中发挥关键作用，将抽象的数学工具与具体问题联系起来。最后，在“动手实践”部分，您将有机会通过解决实际问题来巩固和应用所学知识。

让我们首先从构建这些概念的基础——应力的基本原理和机制开始。

## 原理和机制

本章旨在阐述描述连续介质内部力状态的核心概念。我们将从第一性原理出发，系统地建立柯西[应力张量](@entry_id:148973)的概念，探讨其基本属性，并介绍分析应力状态的关键工具——[主应力](@entry_id:176761)和[莫尔圆](@entry_id:168131)。这些工具对于理解生物组织（如骨骼、肌腱和血管）在生理载荷下的力学行为至关重要。

### 应力的基本概念

#### 牵[引力](@entry_id:189550)矢量

想象一个连续介质（例如一块生物软组织）内部的一个点。如果我们通过这个点做一个假想的切割，将物体分为两部分，那么这两部分之间会通过这个切割面相互作用。根据牛顿第三定律，作用在切面上“正”侧材料上的力与作用在“负”侧材料上的力大小相等，方向相反。

在连续介质力学中，我们假设这种分布在表面上的接触力可以用一个场来描述。对于通过某一点并具有特定方向的任意一个小表面元 $\Delta A$，作用在其上的[接触力](@entry_id:165079)为 $\Delta \mathbf{F}$。我们定义**牵[引力](@entry_id:189550)矢量**（traction vector）$\mathbf{t}$ 为单位面积上的力，它是在 $\Delta A$ 趋向于零时的极限：

$$
\mathbf{t} = \lim_{\Delta A \to 0} \frac{\Delta \mathbf{F}}{\Delta A}
$$

牵[引力](@entry_id:189550)矢量依赖于其作用点的位置 $\mathbf{x}$ 和该点处表面的方向。表面的方向由其[单位法向量](@entry_id:178851) $\mathbf{n}$ 定义。因此，我们将牵[引力](@entry_id:189550)矢量记为 $\mathbf{t}(\mathbf{x}, \mathbf{n})$。在讨论单一点的应力状态时，我们通常简化为 $\mathbf{t}(\mathbf{n})$。值得注意的是，牵[引力](@entry_id:189550)矢量 $\mathbf{t}$ 通常不与法向量 $\mathbf{n}$ 平行。它可以被分解为垂直于表面的**[正应力](@entry_id:260622)**（normal stress）分量和与表面相切的**剪应力**（shear stress）分量。

#### 柯西应力定理与应力张量

一个核心问题是，牵[引力](@entry_id:189550)矢量 $\mathbf{t}(\mathbf{n})$ 是如何依赖于[法向量](@entry_id:264185) $\mathbf{n}$ 的？答案由**柯西应力定理**（Cauchy's Stress Theorem）给出，该定理是[连续介质力学](@entry_id:155125)的一个基石。

我们可以通过分析一个无限小的[四面体单元](@entry_id:168311)的动量平衡来推导此定理 。考虑一个顶点位于我们感兴趣的点 $\mathbf{x}$ 处的四面体。它的三个面分别垂直于笛卡尔坐标轴 $\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3$，第四个斜面的[单位法向量](@entry_id:178851)为 $\mathbf{n}$。对这个四面体应用[牛顿第二定律](@entry_id:274217)（[线性动量平衡](@entry_id:193575)），并取其尺寸趋向于零的极限。在这个极限下，与体积相关的力（如重力、[惯性力](@entry_id:169104)）比与面积相关的力（牵[引力](@entry_id:189550)）更快地趋向于零。因此，在点 $\mathbf{x}$ 处，[表面力](@entry_id:188034)必须自身达到平衡。

这个平衡关系最终表明，作用在任意平面 $\mathbf{n}$ 上的牵[引力](@entry_id:189550)矢量 $\mathbf{t}(\mathbf{n})$ 是作用在三个坐标平面上的牵[引力](@entry_id:189550)矢量 $\mathbf{t}(\mathbf{e}_1), \mathbf{t}(\mathbf{e}_2), \mathbf{t}(\mathbf{e}_3)$ 的[线性组合](@entry_id:154743)，其系数恰好是[法向量](@entry_id:264185) $\mathbf{n}$ 的分量：

$$
\mathbf{t}(\mathbf{n}) = n_1 \mathbf{t}(\mathbf{e}_1) + n_2 \mathbf{t}(\mathbf{e}_2) + n_3 \mathbf{t}(\mathbf{e}_3) = \sum_{j=1}^{3} n_j \mathbf{t}(\mathbf{e}_j)
$$

这个结果揭示了一个深刻的性质：$\mathbf{t}(\mathbf{n})$ 是 $\mathbf{n}$ 的一个线性函数。任何将一个矢量[线性映射](@entry_id:185132)到另一个矢量的算子都可以用一个[二阶张量](@entry_id:199780)来表示。这个张量被称为**柯西应力张量**（Cauchy stress tensor），记为 $\boldsymbol{\sigma}$。如果我们将三个坐标牵[引力](@entry_id:189550)矢量 $\mathbf{t}(\mathbf{e}_j)$ 作为张量 $\boldsymbol{\sigma}$ 表示矩阵的列，即第 $j$ 列是矢量 $\mathbf{t}(\mathbf{e}_j)$ 的分量，那么上述线性关系可以优雅地写作：

$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}
$$

在分量形式中，这表示为 $t_i = \sum_{j=1}^{3} \sigma_{ij} n_j$。分量 $\sigma_{ij}$ 的物理意义是：作用在[法向量](@entry_id:264185)为 $\mathbf{e}_j$ 的平面上，沿 $\mathbf{e}_i$ 方向的牵[引力](@entry_id:189550)分量。因此，柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 完全描述了在连续体中某一点的应力状态。一旦我们知道了在某一点的 $\boldsymbol{\sigma}$，我们就可以计算出作用在通过该点的任何方向平面上的牵[引力](@entry_id:189550)。这个关系是普适的，对所有连续介质都成立，无论是各向同性还是[各向异性材料](@entry_id:184874) 。

### 柯西应力张量的基本性质

#### [角动量平衡](@entry_id:181848)与对称性

在经典[连续介质力学](@entry_id:155125)中，除了[线性动量平衡](@entry_id:193575)外，[角动量平衡](@entry_id:181848)也必须满足。对于一个没有内禀体偶（body couples）或面偶（couple stresses）的微元，[角动量平衡](@entry_id:181848)定律要求柯西[应力张量](@entry_id:148973)必须是**对称的** ，即：

$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}} \quad \text{或} \quad \sigma_{ij} = \sigma_{ji}
$$

这意味着 $\sigma_{12} = \sigma_{21}, \sigma_{13} = \sigma_{31}, \sigma_{23} = \sigma_{32}$。因此，一个三维应力张量只有6个独立的标量分量。对称性是柯西应力张量的一个核心属性，它极大地简化了[应力分析](@entry_id:168804)，并具有重要的数学推论，我们将在后面看到。

在某些[广义连续介质理论](@entry_id:193621)中，例如**哥沙列（Cosserat）理论**或微极性介质理论，对称性假设被放宽。当材料的微观结构（如骨单位的[层状结构](@entry_id:913477)）在宏观尺度上能够传递力偶时，就需要考虑**偶应力**（couple stress）。在这种情况下，广义的[角动量平衡](@entry_id:181848)方程允许 $\boldsymbol{\sigma}$ 是非对称的，其反对称部分与偶[应力的散度](@entry_id:185633)[相平衡](@entry_id:136822)。然而，在大多数生物力学应用中，经典（非极性）连续介质模型和对称[应力张量](@entry_id:148973)的假设是充分且标准的。

#### 客观性与坐标变换

物理定律不应依赖于观察者，这一原理被称为**物质[坐标无关性](@entry_id:159715)**（material frame-indifference）或**客观性**（objectivity）。在力学中，这意味着描述材料行为的[本构方程](@entry_id:138559)在叠加一个任意的刚体运动后应保持形式不变。

牵[引力](@entry_id:189550)矢量作为一个真实的物理力，是客观的。这意味着，如果一个观察者通过一个旋转 $\mathbf{Q}$ 来改变参考系，新的牵[引力](@entry_id:189550)矢量 $\mathbf{t}^*$ 与旧的 $\mathbf{t}$ 的关系为 $\mathbf{t}^* = \mathbf{Q}\mathbf{t}$。从这个基本要求和关系式 $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma}\mathbf{n}$ 出发，可以推导出柯西应力张量在这样一个观察者变换下的变换法则 ：

$$
\boldsymbol{\sigma}^* = \mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^{\mathsf{T}}
$$

这是一个客观的二阶欧拉张量的标准变换法则。它确保了应力状态的物理实在性，独立于我们用以描述它的坐标系。需要强调的是，客观性并不意味着 $\boldsymbol{\sigma}^* = \boldsymbol{\sigma}$（即张量分量不变）。后者是一种更强的条件，称为各向同性，只有在非常特殊的情况下（如[静水压力](@entry_id:275365)状态）才成立。

### [主应力与主方向](@entry_id:193792)

对于在一点处的给定应力状态 $\boldsymbol{\sigma}$，一个自然的问题是：是否存在某些平面，其上的牵[引力](@entry_id:189550)完全是法向的（即没有剪切）？

#### 应力的特征值问题

如果存在这样一个平面，其[单位法向量](@entry_id:178851)为 $\mathbf{n}$，那么作用其上的牵[引力](@entry_id:189550)矢量 $\mathbf{t}(\mathbf{n})$ 必须与 $\mathbf{n}$ 平行。这意味着 $\mathbf{t}(\mathbf{n}) = \lambda \mathbf{n}$，其中 $\lambda$ 是一个标量，表示该平面上的[正应力](@entry_id:260622)大小。结合柯西公式 $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma}\mathbf{n}$，我们得到：

$$
\boldsymbol{\sigma}\mathbf{n} = \lambda \mathbf{n}
$$

这正是线性代数中的一个[标准特征值问题](@entry_id:755346) 。这里的解具有特殊的物理意义：
-   特征值 $\lambda$ 被称为**[主应力](@entry_id:176761)**（principal stresses）。
-   对应的单位[特征向量](@entry_id:151813) $\mathbf{n}$（通常记为 $\mathbf{v}$）被称为**[主方向](@entry_id:276187)**（principal directions）。
-   由[主方向](@entry_id:276187)定义的平面被称为**[主平面](@entry_id:164488)**（principal planes）。

由于柯西应力张量 $\boldsymbol{\sigma}$ 是对称的，[谱定理](@entry_id:136620)保证了以下重要性质 ：
1.  存在三个[主应力](@entry_id:176761)（$\lambda_1, \lambda_2, \lambda_3$），它们都是实数。
2.  对应的三个[主方向](@entry_id:276187)（$\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3$）是相互正交的（成直角）。

因此，在任何一点，我们总能找到一个[正交坐标](@entry_id:166074)系（主坐标系），在该坐标系中，应力张量的[矩阵表示](@entry_id:146025)是对角的，其对角线元素就是三个[主应力](@entry_id:176761)：
$$
\boldsymbol{\sigma}_{\text{principal}} = \begin{pmatrix} \lambda_1 & 0 & 0 \\ 0 & \lambda_2 & 0 \\ 0 & 0 & \lambda_3 \end{pmatrix}
$$
[主应力](@entry_id:176761)和[主方向](@entry_id:276187)是应力状态的内在属性，不依赖于坐标系的选择。它们代表了在一点处拉伸和压缩的[极值](@entry_id:145933)。按照惯例，[主应力](@entry_id:176761)被排序为 $\lambda_1 \ge \lambda_2 \ge \lambda_3$。

值得注意的是，[主应力](@entry_id:176761)和[主方向](@entry_id:276187)的计算是一个纯粹的代数过程，仅依赖于该点的应力张量 $\boldsymbol{\sigma}$ 的分量。材料的属性，如各向异性，决定了在给定变形下会产生怎样的应力状态 $\boldsymbol{\sigma}$，但一旦 $\boldsymbol{\sigma}$ 被确定，其[主值](@entry_id:189577)的分析就与材料的[本构定律](@entry_id:178936)无关了 。然而，在高等生物力学中，一个重要的课题是研究应力的[主方向](@entry_id:276187)与应变或拉伸的[主方向](@entry_id:276187)之间的关系。在[各向同性材料](@entry_id:170678)中，它们是共轴的；但在[各向异性材料](@entry_id:184874)（如[纤维增强](@entry_id:194439)的动脉壁）中，由于材料的优选方向，应力[主轴](@entry_id:172691)和[应变主轴](@entry_id:188315)通常不重合 。

### 应力状态的分析

#### [静水应力](@entry_id:186327)与[偏应力](@entry_id:163323)

为了更好地理解应力状态对[材料变形](@entry_id:169356)的不同影响，将[应力张量](@entry_id:148973)分解为其**静水**（isotropic）部分和**偏**（deviatoric）部分是极其有用的。

[应力张量](@entry_id:148973)的**静水部分**（或球量部分）与[平均应力](@entry_id:751819)有关，它在所有方向上都相等。我们定义**平均[正应力](@entry_id:260622)**（mean normal stress）为：

$$
\sigma_m = \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3} (\sigma_{11} + \sigma_{22} + \sigma_{33}) = \frac{1}{3} (\lambda_1 + \lambda_2 + \lambda_3)
$$

**静水压力**（hydrostatic pressure）则定义为 $p = -\sigma_m$。[静水应力](@entry_id:186327)张量为 $\sigma_m \mathbf{I}$。

[应力张量](@entry_id:148973)的**[偏应力](@entry_id:163323)部分** $\mathbf{s}$ 定义为总应力减去其静水部分：

$$
\mathbf{s} = \boldsymbol{\sigma} - \sigma_m \mathbf{I}
$$

根据定义，[偏应力张量](@entry_id:267642)是无迹的，即 $\mathrm{tr}(\mathbf{s}) = 0$。

这种分解具有深刻的物理意义，尤其对于像软组织这样近似不可压缩的材料 。[静水应力](@entry_id:186327)部分主要引起材料的体积变化（膨胀或收缩），而[偏应力](@entry_id:163323)部分则引起材料的形状变化（畸变或剪切）。对于几乎不可压缩的材料，产生微小体积变化需要巨大的[静水压力](@entry_id:275365)，因此静水项主要起着维持体积不变的约束作用。而形状的改变，如细胞的拉伸或胶原纤维的重定向，则主要由[偏应力](@entry_id:163323)驱动。

一个重要的推论是，叠加一个均匀的[静水应力](@entry_id:186327)（如压力 $p_0$）只会平移[主应力](@entry_id:176761)的谱，而不会改变它们的差值或[主方向](@entry_id:276187) 。如果 $\boldsymbol{\sigma}_{\text{new}} = \boldsymbol{\sigma} - p_0 \mathbf{I}$，那么新的[主应力](@entry_id:176761)为 $\lambda_{i, \text{new}} = \lambda_i - p_0$。这意味着所有与剪切相关的量，如[最大剪应力](@entry_id:181794)，都独立于[静水压力](@entry_id:275365)。

#### [莫尔圆](@entry_id:168131)：应力状态的可视化

[莫尔圆](@entry_id:168131)（Mohr's Circle）是一种强大的图形工具，用于可视化在一点处二维或三维应力状态下，[正应力与剪应力](@entry_id:201088)随平面方向变化的规律。

对于一个三维应力状态，其[主应力](@entry_id:176761)为 $\lambda_1 \ge \lambda_2 \ge \lambda_3$，我们可以绘制三个**主[莫尔圆](@entry_id:168131)** 。在以正应力 $\sigma_n$ 为横轴、剪应力 $\tau_n$ 为纵轴的平面上，这三个圆分别对应于[主方向](@entry_id:276187)对 $(1,2)$, $(2,3)$ 和 $(1,3)$：
-   圆1-2：圆心位于 $\left( \frac{\lambda_1+\lambda_2}{2}, 0 \right)$，半径为 $R_{12} = \frac{\lambda_1-\lambda_2}{2}$。
-   圆2-3：圆心位于 $\left( \frac{\lambda_2+\lambda_3}{2}, 0 \right)$，半径为 $R_{23} = \frac{\lambda_2-\lambda_3}{2}$。
-   圆1-3：圆心位于 $\left( \frac{\lambda_1+\lambda_3}{2}, 0 \right)$，半径为 $R_{13} = \frac{\lambda_1-\lambda_3}{2}$。

这些圆的交点在[横轴](@entry_id:177453)上，坐标分别为 $\lambda_1, \lambda_2, \lambda_3$，代表在[主平面](@entry_id:164488)上剪应力为零的状态 。一个关键结论是，通过该点的**任何**平面上的应力状态 $(\sigma_n, \tau_n)$ 都对应于这三个圆所围成的阴影区域内的一个点。

最大的[莫尔圆](@entry_id:168131)（由极值[主应力](@entry_id:176761) $\lambda_1$ 和 $\lambda_3$ 形成）尤其重要。它的半径等于该点处的**绝对[最大剪应力](@entry_id:181794)** $\tau_{\text{max}}$：

$$
\tau_{\text{max}} = R_{13} = \frac{\lambda_1 - \lambda_3}{2}
$$

这个值在预测材料的屈服或失效中起着核心作用。例如，对于一个给定的应力状态，如 $\boldsymbol{\sigma} = \begin{pmatrix} 120 & 30 & -10 \\ 30 & 80 & 20 \\ -10 & 20 & 60 \end{pmatrix} \text{ kPa}$ ，我们可以计算出其[主应力](@entry_id:176761)约为 $\lambda_1 \approx 136.0 \text{ kPa}, \lambda_2 \approx 84.5 \text{ kPa}, \lambda_3 \approx 39.5 \text{ kPa}$。由此，[最大剪应力](@entry_id:181794)为 $\tau_{\text{max}} = (136.0 - 39.5)/2 \approx 48.3 \text{ kPa}$，这对应于最大[莫尔圆](@entry_id:168131)的半径。

[静水应力](@entry_id:186327)的叠加只会使这三个[莫尔圆](@entry_id:168131)作为一个整体沿 $\sigma_n$ 轴平移，而它们的半径和相对位置保持不变  。这图形化地证明了剪应力状态完全由[偏应力张量](@entry_id:267642)决定。

### 延伸概念：有限变形中的应力

到目前为止，我们讨论的柯西应力是**真实应力**（true stress），因为它定义为作用在**当前**（变形后）构形单位面积上的力。在生物力学中，软组织常经历显著的形状和尺寸变化，这属于**有限变形**（finite deformation）的范畴。

在有限变形理论中，引入了其他应力张量，它们将力与**参考**（变形前）构形的几何量联系起来。一个重要的例子是**第二皮奥拉-基尔霍夫（Second Piola-Kirchhoff, PK2）应力张量** $\mathbf{S}$。它与柯西应力 $\boldsymbol{\sigma}$ 通过变形梯度张量 $\mathbf{F}$ 和其行列式 $J = \det(\mathbf{F})$ 相互关联 ：

$$
\boldsymbol{\sigma} = \frac{1}{J} \mathbf{F} \mathbf{S} \mathbf{F}^{\mathsf{T}}
$$

这个关系被称为**前推（push-forward）**操作。PK2[应力张量](@entry_id:148973)在建立材料本构模型时非常有用，因为它与参考构形中的[应变度量](@entry_id:755495)（如[格林-拉格朗日应变张量](@entry_id:187745)）是[功共轭](@entry_id:194957)的。然而，一旦通过本构模型和该变换关系计算出当前构形中的柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$，本章中讨论的所有分析方法——如计算[主应力](@entry_id:176761)、进行静水/偏[应力分解](@entry_id:272862)以及构建[莫尔圆](@entry_id:168131)——都同样适用。