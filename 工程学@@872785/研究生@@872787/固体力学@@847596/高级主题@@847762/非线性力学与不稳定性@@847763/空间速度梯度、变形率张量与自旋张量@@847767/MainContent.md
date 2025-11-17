## 引言
在描述物体运动时，我们如何精确地区分形状的改变与整体的旋转？这个问题在连续介质力学中至关重要，无论我们研究的是流体的流动、固体的变形还是复杂材料的响应。答案的核心在于理解一组强大的[运动学](@entry_id:173318)概念：[空间速度梯度](@entry_id:187198)、变形率张量和[自旋张量](@entry_id:187346)。这些张量为我们提供了一套数学语言，用以量化和解析材料点邻域内最微小的运动细节。它们是连接宏观观测与微观物理机制的桥梁，也是构建预测材料行为的[本构模型](@entry_id:174726)的基石。本文旨在深入剖析这些基本概念，填补直观理解与严谨数学表述之间的鸿沟。

在接下来的内容中，我们将系统地探索这一主题。首先，在“原理与机制”一章中，我们将建立这些张量的精确定义，阐明它们的物理意义以及它们之间深刻的内在联系，并探讨[客观性原理](@entry_id:185412)这一基本物理约束。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论工具如何在[流体动力学](@entry_id:136788)、[热力学](@entry_id:141121)、[材料科学](@entry_id:152226)和有限塑性理论等不同领域中发挥关键作用，解决从计算壁面剪应力到预测材料织构演化等实际问题。最后，在“动手实践”部分，您将有机会通过具体的计算和分析练习，将理论知识转化为解决问题的实践能力。通过本次学习，您将对连续体的运动学描述建立起一个全面而深入的理解。

## 原理与机制

在本章中，我们将深入探讨[连续介质运动学](@entry_id:747813)中的核心概念：[空间速度梯度](@entry_id:187198)、变形率张量和[自旋张量](@entry_id:187346)。这些量构成了描述材料点局部运动、变形和旋转的数学基础。理解它们的定义、物理意义以及它们之间的关系，对于建立适用于大变形和[复杂流动](@entry_id:747569)问题的[本构模型](@entry_id:174726)至关重要。

### [空间速度梯度](@entry_id:187198)张量

连续体中物质点的运动可以通过[速度场](@entry_id:271461) $\mathbf{v}(\mathbf{x}, t)$ 来描述，该速度场定义了在当前构型中，空间位置 $\mathbf{x}$ 处的物[质点](@entry_id:186768)在时间 $t$ 的速度。为了理解一个物质点邻域内的相对运动，我们必须考察[速度场](@entry_id:271461)是如何随空间位置变化的。这种空间变化由**[空间速度梯度](@entry_id:187198)张量** $\mathbf{L}$ 来量化，其定义为速度向量场 $\mathbf{v}$ 对空间坐标 $\mathbf{x}$ 的梯度。

在笛卡尔坐标系中，其分量形式为：
$$
L_{ij} = \frac{\partial v_i}{\partial x_j}
$$
其中 $v_i$ 是[速度矢量](@entry_id:269648)的第 $i$ 个分量，$x_j$ 是空间坐标的第 $j$ 个分量。因此，对于两个由无穷小向量 $\mathrm{d}\mathbf{x}$ 分隔的相邻物质点，它们的相对速度 $\mathrm{d}\mathbf{v}$ 可以线性近似为：
$$
\mathrm{d}\mathbf{v} = \mathbf{L} \mathrm{d}\mathbf{x}
$$
这个关系表明，$\mathbf{L}$ 描述了速度场在一个点附近的[线性变换](@entry_id:149133)。

[空间速度梯度](@entry_id:187198)张量 $\mathbf{L}$ 与描述从参考构型到当前构型的映射的**变形梯度张量** $\mathbf{F}$ 密切相关。变形梯度的[物质时间导数](@entry_id:190892) $\dot{\mathbf{F}}$ 描述了变形的速率，它与 $\mathbf{L}$ 之间存在一个基本关系：
$$
\dot{\mathbf{F}} = \mathbf{L} \mathbf{F}
$$
这个关系式连接了[欧拉描述](@entry_id:264722)（通过 $\mathbf{L}$）和[拉格朗日描述](@entry_id:264498)（通过 $\mathbf{F}$）的运动学。需要注意的是，$\mathbf{L}$ 是一个作用于当前构型中向量的单点张量，而 $\dot{\mathbf{F}}$ 是一个将向量从参考构型映射到当前构型的两点张量。因此，尽管它们在概念上相关，但通常情况下 $\mathbf{L} \neq \dot{\mathbf{F}}$。

### 基本分解：变形率与自旋

[空间速度梯度](@entry_id:187198) $\mathbf{L}$ 捕捉了物质点邻域内所有的运动信息，包括形状的改变（拉伸和剪切）和刚体旋转。为了将这两种效应分离开来，可以将任何二阶张量唯一地分解为其对称[部分和](@entry_id:162077)反对称部分。对于 $\mathbf{L}$，这种分解具有深刻的物理意义。

$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$

其中，
- **变形率张量** $\mathbf{D}$ 是 $\mathbf{L}$ 的对称部分：$\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}})$。
- **[自旋张量](@entry_id:187346)** $\mathbf{W}$ 是 $\mathbf{L}$ 的反对称部分：$\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\mathsf{T}})$。

这个分解是[连续介质运动学](@entry_id:747813)中最基本的概念之一，因为它将变形速率（由 $\mathbf{D}$ 描述）与刚性转动速率（由 $\mathbf{W}$ 描述）清晰地分离开来。

#### 变形率张量 D 的物理意义

**变形率张量** $\mathbf{D}$ 描述了材料单元体形状和尺寸的瞬时变化率。它的物理意义可以通过考察材料[线元](@entry_id:196833)、面元和体元的几何变化率来精确阐明。

考虑一个长度为 $l$、方向为单位向量 $\mathbf{n}$ 的材料[线元](@entry_id:196833)。其长度的瞬时分数变化率（即拉伸率）仅由 $\mathbf{D}$ 决定：
$$
\frac{1}{l}\frac{\mathrm{d}l}{\mathrm{d}t} = \mathbf{n} \cdot (\mathbf{D}\mathbf{n})
$$
这个二次型表明，拉伸率取决于材料线的方向。$\mathbf{D}$ 的[主值](@entry_id:189577)（[特征值](@entry_id:154894)）$d_1, d_2, d_3$ 代表了沿其对应主方向（[特征向量](@entry_id:151813)）$\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3$ 的拉伸率，它们是该点拉伸率的极值。

材料[体元](@entry_id:267802)的瞬时分数体积变化率由 $\mathbf{D}$ 的迹（trace）给出，它等于[速度场](@entry_id:271461)的散度：
$$
\frac{1}{V}\frac{\mathrm{d}V}{\mathrm{d}t} = \operatorname{tr}(\mathbf{D}) = \nabla \cdot \mathbf{v}
$$
如果一个运动是**等容的**（volume-preserving）或**不可压缩的**，那么其体积变化率为零，即 $\operatorname{tr}(\mathbf{D}) = 0$。例如，在一个[速度场](@entry_id:271461)中，如果 $\mathbf{D}$ 的[主值](@entry_id:189577)为 $a, b, -a-b$，那么体积变化率为 $a+b+(-a-b)=0$，表示该变形是等容的。

对于一个法向为 $\mathbf{n}$ 的材料面元，其面积 $A$ 的分数变化率为：
$$
\frac{1}{A}\frac{\mathrm{d}A}{\mathrm{d}t} = \operatorname{tr}(\mathbf{D}) - \mathbf{n} \cdot (\mathbf{D}\mathbf{n})
$$
这可以解释为总体积膨胀率减去垂直于该表面的线拉伸率。例如，对于一个法向为 $\mathbf{e}_1$ 的面，其面积变化率为 $d_2 + d_3$。

值得注意的是，在所有这些几何变化率的表达式中，[自旋张量](@entry_id:187346) $\mathbf{W}$ 都没有出现。这证实了 $\mathbf{D}$ 确实是唯一描述材料变形的量。

#### [自旋张量](@entry_id:187346) W 的物理意义

**[自旋张量](@entry_id:187346)** $\mathbf{W}$ 是一个[反对称张量](@entry_id:199349)，它描述了材料单元体的平均瞬时[刚体转动](@entry_id:191086)速率。任何三维[反对称张量](@entry_id:199349) $\mathbf{W}$ 都存在一个对应的**[轴矢量](@entry_id:196296)**（axial vector）$\boldsymbol{\omega}$，使得对于任意向量 $\mathbf{a}$，都有 $\mathbf{W}\mathbf{a} = \boldsymbol{\omega} \times \mathbf{a}$。这个[轴矢量](@entry_id:196296)代表了瞬时转动的角[速度矢量](@entry_id:269648)。

这个[轴矢量](@entry_id:196296) $\boldsymbol{\omega}$ 与速度场的**涡度**（vorticity）$\boldsymbol{\zeta} = \nabla \times \mathbf{v}$ 密切相关。可以证明，它们之间的关系为：
$$
\boldsymbol{\omega} = \frac{1}{2} (\nabla \times \mathbf{v}) = \frac{1}{2}\boldsymbol{\zeta}
$$
因此，[自旋张量](@entry_id:187346)代表了材料点的局部[角速度](@entry_id:192539)，其大小是涡度的一半。

一个经典的例子是刚体绕 $z$ 轴的定常转动，其[速度场](@entry_id:271461)为 $\mathbf{v} = (-\alpha y, \alpha x, 0)$。计算可得，其[空间速度梯度](@entry_id:187198)为 $\mathbf{L} = \begin{pmatrix} 0  -\alpha  0 \\ \alpha  0  0 \\ 0  0  0 \end{pmatrix}$。这是一个[反对称张量](@entry_id:199349)，因此变形率张量 $\mathbf{D} = \mathbf{0}$，而[自旋张量](@entry_id:187346) $\mathbf{W} = \mathbf{L}$。这表明该运动是纯旋转，没有任何变形，这与我们对[刚体运动](@entry_id:193355)的直觉相符。其角速度矢量为 $\boldsymbol{\omega} = (0, 0, \alpha)$。

### 局部流动的分类

通过考察 $\mathbf{D}$ 和 $\mathbf{W}$ 的性质，我们可以对不同类型的局部流动进行分类：
- **刚体运动**: 变形率为零，$\mathbf{D} = \mathbf{0}$。[速度梯度](@entry_id:261686)是纯反对称的，$\mathbf{L} = \mathbf{W}$。
- **无旋运动 (纯变形流)**: 自旋为零，$\mathbf{W} = \mathbf{0}$。[速度梯度](@entry_id:261686)是纯对称的，$\mathbf{L} = \mathbf{D}$。
- **等容运动**: 体积变化率为零，$\operatorname{tr}(\mathbf{D}) = 0$。
- **简单剪切**: 例如速度场 $\mathbf{v} = (ky, 0, 0)$，其 $\mathbf{D}$ 和 $\mathbf{W}$ 均不为零，表明这种流动既包含变形也包含旋转。

### [客观性原理](@entry_id:185412)（物质标架无关性）

在建立本构关系（即应力与变形之间的关系）时，一个至关重要的物理原理是**物质标架无关性**，也称为**[客观性原理](@entry_id:185412)**。该原理指出，[本构定律](@entry_id:178936)的形式不能依赖于观察者。不同的观察者可能相对于彼此进行刚体运动，但他们观察到的材料响应规律必须是相同的。

考虑一个观察者（标架）相对于另一个观察者进行[刚体运动](@entry_id:193355)，其位置通过 $\mathbf{x}'(t) = \mathbf{Q}(t)\mathbf{x}(t) + \mathbf{c}(t)$ 变换，其中 $\mathbf{Q}(t)$ 是一个时间相关的正交[旋转张量](@entry_id:191990)。我们可以推导出各个运动学张量在此变换下的法则：
- 变形率张量 $\mathbf{D}$ 是**客观的**：$\mathbf{D}' = \mathbf{Q}\mathbf{D}\mathbf{Q}^{\mathsf{T}}$。
- [空间速度梯度](@entry_id:187198) $\mathbf{L}$ 不是客观的：$\mathbf{L}' = \mathbf{Q}\mathbf{L}\mathbf{Q}^{\mathsf{T}} + \dot{\mathbf{Q}}\mathbf{Q}^{\mathsf{T}}$。
- [自旋张量](@entry_id:187346) $\mathbf{W}$ 不是客观的：$\mathbf{W}' = \mathbf{Q}\mathbf{W}\mathbf{Q}^{\mathsf{T}} + \dot{\mathbf{Q}}\mathbf{Q}^{\mathsf{T}}$。

$\dot{\mathbf{Q}}\mathbf{Q}^{\mathsf{T}}$ 项代表了观察者标架自身的旋转速率。$\mathbf{D}$ 的客观性意味着它所测量的变形率是独立于观察者旋转的内在属性。相反，$\mathbf{W}$ 的非客观性表明，测得的旋转速率是材料旋转和观察者自身旋转的叠加。

一个生动的例子可以说明这一点。考虑一个简单剪切流 $\mathbf{v} = kx_2 \mathbf{e}_1$，并叠加一个刚体旋转。新的[速度场](@entry_id:271461)为 $\mathbf{v}^\sharp = \mathbf{v} + \boldsymbol{\Omega}\mathbf{x}$，其中 $\boldsymbol{\Omega}$ 是刚体旋转的[自旋张量](@entry_id:187346)。计算表明，新的变形率张量 $\mathbf{D}^\sharp$ 与原始的 $\mathbf{D}$ 完全相同 ($\mathbf{D}^\sharp = \mathbf{D}$)，而新的[自旋张量](@entry_id:187346)则是两者之和 ($\mathbf{W}^\sharp = \mathbf{W} + \boldsymbol{\Omega}$)。这清晰地证明了变形率的客观性和自旋的非客观性。

[客观性原理](@entry_id:185412)的直接推论是，任何有效的[本构方程](@entry_id:138559)都必须关联客观的张量。
- **[应力功率](@entry_id:182907)**: 单位体积的内功率耗散 $p = \boldsymbol{\sigma} : \mathbf{L}$。由于柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是对称的，而 $\mathbf{W}$ 是反对称的，它们的缩并 $\boldsymbol{\sigma} : \mathbf{W}$ 恒为零。因此，功率耗散简化为 $p = \boldsymbol{\sigma} : \mathbf{D}$。这意味着只有变形（由 $\mathbf{D}$ 描述）才能产生功，而刚性旋转（由 $\mathbf{W}$ 描述）则不产生功。
- **本构模型**: [本构模型](@entry_id:174726)必须关联客观的应力张量（或其[客观率](@entry_id:198692)）和客观的变形率张量。例如，一个简单的关系式 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{D}$ 是不客观的，因为应力的物质导数 $\dot{\boldsymbol{\sigma}}$ 本身不是一个客观的张量率。为了克服这个问题，需要引入**[客观应力率](@entry_id:199282)**，如**Jaumann率**：$\boldsymbol{\sigma}^{\triangledown_J} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\mathbf{W} - \mathbf{W}\boldsymbol{\sigma}$。这个率是客观的，因此，一个客观的**[亚弹性](@entry_id:204371)**本构关系可以写成 $\boldsymbol{\sigma}^{\triangledown_J} = \mathbb{C}:\mathbf{D}$。这里，[自旋张量](@entry_id:187346) $\mathbf{W}$ 的作用是“修正”[物质导数](@entry_id:172646)，以消除材料刚性转动的影响，从而得到一个客观的率。

### 从速率到有限变形

到目前为止，我们的讨论都集中在[瞬时速率](@entry_id:182981)上。然而，这些速率可以被积分以描述随时间累积的有限变形。

从关系式 $\dot{\mathbf{F}} = \mathbf{L} \mathbf{F}$ 出发，如果[空间速度梯度](@entry_id:187198) $\mathbf{L}$ 是常数，这个[线性常微分方程](@entry_id:276013)的解为：
$$
\mathbf{F}(t) = \exp(\mathbf{L}t)
$$
其中 $\exp(\cdot)$ 是矩阵指数函数。这为从速度梯度直接计算有限变形梯度提供了一个强大的工具。利用恒等式 $\det(\exp(\mathbf{A})) = \exp(\operatorname{tr}(\mathbf{A}))$，我们可以计算体积比 $J = \det(\mathbf{F}) = \exp(\operatorname{tr}(\mathbf{L}t)) = \exp(t \cdot \operatorname{tr}(\mathbf{D}))$，再次证实了只有变形率的迹影响体积变化。

在一种特殊但重要的情况下，即当 $\mathbf{D}$ 和 $\mathbf{W}$ 交换时（$[\mathbf{D}, \mathbf{W}] = \mathbf{D}\mathbf{W} - \mathbf{W}\mathbf{D} = \mathbf{0}$），[矩阵指数](@entry_id:139347)可以分解：
$$
\mathbf{F}(t) = \exp((\mathbf{D}+\mathbf{W})t) = \exp(\mathbf{D}t)\exp(\mathbf{W}t)
$$
令 $\mathbf{U}(t) = \exp(\mathbf{D}t)$ 和 $\mathbf{R}(t) = \exp(\mathbf{W}t)$。可以证明 $\mathbf{U}(t)$ 是一个[对称正定](@entry_id:145886)张量（代表纯拉伸），而 $\mathbf{R}(t)$ 是一个正交[旋转张量](@entry_id:191990)。因此，当 $\mathbf{D}$ 和 $\mathbf{W}$ 可交换时，运动可以分解为一个纯拉伸和一个刚性旋转的相继作用，这与有限变形的极分解定理相呼应。这种情况的物理意义是，变形的[主轴](@entry_id:172691)与材料一起做刚性旋转，即主轴是**共转的**。

然而，在一般情况下，$\mathbf{D}$ 和 $\mathbf{W}$ 并不可交换 ($[\mathbf{D}, \mathbf{W}] \neq \mathbf{0}$)。这导致了更为复杂的运动学，即**非共轴性** (non-coaxiality)。这意味着变形率的主轴方向并不会简单地随材料一起旋转。实际上，$\mathbf{D}$ 的[主轴](@entry_id:172691)的旋转速率（即其[特征向量](@entry_id:151813)的旋转速率）不仅取决于材料的平均[刚体转动](@entry_id:191086)速率（由 $\mathbf{W}$ 描述），还取决于 $\mathbf{D}$ 和 $\mathbf{W}$ 的非共轴性。当且仅当 $\mathbf{D}$ 和 $\mathbf{W}$ 的[主轴](@entry_id:172691)对齐（即它们可交换）时，$\mathbf{D}$ 的[主轴](@entry_id:172691)才会与材料的平均转动（自旋）“共转”。在一般流动中，变形[主轴](@entry_id:172691)的旋转速率与材料自旋之间的差异是理解材料在大变形下[织构演变](@entry_id:194385)的关键，尤其在塑性力学和[非牛顿流体力学](@entry_id:266914)中至关重要。