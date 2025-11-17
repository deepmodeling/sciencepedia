## 引言
在物理学和工程学中，张量是描述连续介质（如固体和流体）内部复杂状态的强大数学工具。然而，一个完整的应力或[应变张量](@entry_id:193332)包含的信息是多维的，直接分析其物理效应可能相当困难。为了获得更深刻的物理洞察，我们常常需要将这些复杂的[张量分解](@entry_id:173366)为更简单、物理意义更明确的组成部分。本文聚焦于其中最基本也最重要的一种分解方法：球量-偏量分解。这一强大的技术解决了如何将一个通用的变形或应力状态，清晰地分离为两种截然不同的物理行为——均匀的体积变化与保持体积不变的形状畸变——的问题。

通过本文的学习，读者将全面掌握球量-偏量分解的核心思想及其应用。在“原理与机制”章节中，我们将深入探讨该分解的数学定义、物理含义、几何解释及其在[坐标变换](@entry_id:172727)下的客观性。接下来的“应用与跨学科联系”章节将展示这一概念如何在[连续介质力学](@entry_id:155125)、[材料塑性](@entry_id:186852)、[流体力学](@entry_id:136788)乃至计算力学等多个领域中发挥关键作用，成为连接理论与实践的桥梁。最后，通过“动手实践”部分提供的具体计算和概念问题，读者将有机会巩固所学知识。现在，让我们从其最基本的数学原理和物理机制开始。

## 原理与机制

在对连续介质（如固体和流体）的力学行为进行数学描述时，我们经常使用二阶张量来表示物理量，例如应力张量 $\boldsymbol{\sigma}$ 和应变张量 $\boldsymbol{\epsilon}$。这些张量捕捉了材料内部某一点的完整状态。然而，为了更深入地理解材料的响应，将这些复杂的[张量分解](@entry_id:173366)为更简单、物理意义更明确的部分是至关重要的。其中最基本也最重要的分解之一，便是将一个[张量分解](@entry_id:173366)为其**球量部分（volumetric part）**和**偏量部分（deviatoric part）**。这种分解在概念上将一个通用的变形或应力状态分离为两个独立的部分：一个引起体积变化的均匀（各向同性）分量和一个只引起形状畸变（剪切）而保持体积不变的分量。

### 球量张量：各向同性的体积变化

任何一个二阶张量 $\mathbf{T}$ 都可以唯一地写成一个球量张量和一个偏量张量之和。我们首先关注球量部分，它代表了均匀的膨胀或压缩。

对于一个在三维空间中的[二阶张量](@entry_id:199780) $\mathbf{T}$，其**球量部分**，记作 $\text{vol}(\mathbf{T})$，定义为：
$$
\text{vol}(\mathbf{T}) = \frac{1}{3}\text{tr}(\mathbf{T})\mathbf{I}
$$
其中 $\text{tr}(\mathbf{T})$ 是张量 $\mathbf{T}$ 的迹（即其在任意[坐标系](@entry_id:156346)下矩阵表示的主对角[线元](@entry_id:196833)素之和），而 $\mathbf{I}$ 是二阶单位张量。

这个定义蕴含了深刻的物理意义。

当张量 $\mathbf{T}$ 是柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 时，其迹的三分之一被称为**[平均应力](@entry_id:751819)**或**[静水压力](@entry_id:275365)** $p$：
$$
p = \frac{1}{3}\text{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33})
$$
因此，[应力张量](@entry_id:148973)的球量部分 $\boldsymbol{\sigma}_{\text{vol}} = p\mathbf{I}$。这个张量描述了一种在所有方向上都相等的拉伸或压缩状态，类似于物体[浸没](@entry_id:159709)在流体中所受到的静水压力。一个纯球量（或称静水）应力状态，例如 $\boldsymbol{\sigma} = k\mathbf{I}$，其偏量部分为零 [@problem_id:1505995]。

当张量 $\mathbf{T}$ 是[小应变张量](@entry_id:754968) $\boldsymbol{\epsilon}$ 时，其迹 $\text{tr}(\boldsymbol{\epsilon})$ 代表了材料微元的**体应变**（volumetric strain），即单位体积的改变量。对于许多材料，如工程应用中常见的[不可压缩材料](@entry_id:159741)（如橡胶或某些饱和土壤），其变形过程中体积几乎不变。这意味着它们的体应变为零，即 $\text{tr}(\boldsymbol{\epsilon}) = 0$。例如，如果一个不可压缩聚合物材料的平面应变状态由矩阵 $\boldsymbol{\epsilon} = \begin{pmatrix} k_{1}  k_{3}  0 \\ k_{3}  k_{2}  0 \\ 0  0  0 \end{pmatrix}$ 描述，那么不可压缩性要求 $\text{tr}(\boldsymbol{\epsilon}) = k_1 + k_2 = 0$ [@problem_id:1505979]。

球量张量的一个关键特性是其**各向同性**。一个张量如果其分量在[坐标系](@entry_id:156346)的所有旋转下都保持不变，则称其为[各向同性张量](@entry_id:195105)。球量张量 $p\mathbf{I}$ 正是如此。在任何旋转后的[坐标系](@entry_id:156346)中，它的分量矩阵仍然是 $p\mathbf{I}$ [@problem_id:1505958]。这一性质也体现在其[本征值](@entry_id:154894)上：一个纯球量张量 $p\mathbf{I}$ 的三个[特征值](@entry_id:154894)是完全相同的，均为 $p$，即 $\lambda_1 = \lambda_2 = \lambda_3 = p$ [@problem_id:1506007]。这从物理上意味着，在[主方向](@entry_id:276187)上，其[主应力](@entry_id:176761)或[主应变](@entry_id:197797)在各个方向上是均等的。

### 偏量张量：量化形状畸变

从原始张量 $\mathbf{T}$ 中减去其球量部分后，剩下的便是**偏量部分**，记作 $\text{dev}(\mathbf{T})$：
$$
\text{dev}(\mathbf{T}) = \mathbf{T} - \text{vol}(\mathbf{T}) = \mathbf{T} - \frac{1}{3}\text{tr}(\mathbf{T})\mathbf{I}
$$
偏量张量捕捉了材料微元在保持体积不变的情况下的形状变化，即**剪切变形**或**剪应力**。例如，在[金属塑性](@entry_id:176585)理论中，材料的屈服（开始永久变形）通常是由偏应力的大小决定的，而与[静水压力](@entry_id:275365)无关。

偏量张量最根本的数学特性是其**迹恒为零**。这是一个无论原始张量 $\mathbf{T}$ 是什么都成立的普适性质。我们可以轻易证明这一点：
$$
\text{tr}(\text{dev}(\mathbf{T})) = \text{tr}\left(\mathbf{T} - \frac{1}{3}\text{tr}(\mathbf{T})\mathbf{I}\right)
$$
利用[迹算子](@entry_id:183665)的线性性质，我们得到：
$$
\text{tr}(\text{dev}(\mathbf{T})) = \text{tr}(\mathbf{T}) - \text{tr}\left(\frac{1}{3}\text{tr}(\mathbf{T})\mathbf{I}\right) = \text{tr}(\mathbf{T}) - \frac{1}{3}\text{tr}(\mathbf{T})\text{tr}(\mathbf{I})
$$
在三维空间中，单位张量 $\mathbf{I}$ 的迹为 $\text{tr}(\mathbf{I}) = 1+1+1 = 3$。因此：
$$
\text{tr}(\text{dev}(\mathbf{T})) = \text{tr}(\mathbf{T}) - \frac{1}{3}\text{tr}(\mathbf{T}) \cdot 3 = \text{tr}(\mathbf{T}) - \text{tr}(\mathbf{T}) = 0
$$
这个结论非常重要，它意味着偏量张量代表的是一种“纯剪切”的状态，没有任何体积膨胀或收缩的贡献 [@problem_id:1506014]。

一个有趣的特例是，如果一个张量 $\mathbf{T}$ 本身的迹就为零，那么它的球量部分为零，该张量与其偏量部分完全相同，即 $\text{dev}(\mathbf{T}) = \mathbf{T}$。这类张量被称为**纯偏量张量** [@problem_id:1505956]。

为了更具体地理解这个分解，让我们计算一个实例。考虑一个[应力张量](@entry_id:148973) [@problem_id:1505975]：
$$
[\boldsymbol{\sigma}] = \begin{pmatrix} 150  20  -10 \\ 20  75  30 \\ -10  30  45 \end{pmatrix} \text{ MPa}
$$
首先，计算[平均应力](@entry_id:751819) $p$：
$$
p = \frac{1}{3}\text{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(150 + 75 + 45) = \frac{270}{3} = 90 \text{ MPa}
$$
球量部分为 $\boldsymbol{\sigma}_{\text{vol}} = 90\mathbf{I}$。[偏应力张量](@entry_id:267642) $\boldsymbol{\sigma}_{\text{dev}}$ 的矩阵为：
$$
[\boldsymbol{\sigma}_{\text{dev}}] = [\boldsymbol{\sigma}] - 90[\mathbf{I}] = \begin{pmatrix} 150-90  20  -10 \\ 20  75-90  30 \\ -10  30  45-90 \end{pmatrix} = \begin{pmatrix} 60  20  -10 \\ 20  -15  30 \\ -10  30  -45 \end{pmatrix} \text{ MPa}
$$
可以看到，[偏应力张量](@entry_id:267642)的对角分量 $\sigma_{\text{dev}, 22}$ 是 $75 - 90 = -15$ MPa。同时，我们可以验证其迹为 $60 + (-15) + (-45) = 0$。

### 几何解释与正交性

球量-偏量分解不仅在物理上有清晰的意义，在数学上也有优美的几何结构。我们可以将所有[二阶张量](@entry_id:199780)的集合视为一个[向量空间](@entry_id:151108)（具体来说是一个九维[向量空间](@entry_id:151108)）。在这个空间中，可以定义一个类似于向量[点积](@entry_id:149019)的**[内积](@entry_id:158127)**，即**[弗罗贝尼乌斯内积](@entry_id:153693)（Frobenius inner product）**：
$$
\langle \mathbf{A}, \mathbf{B} \rangle = \text{tr}(\mathbf{A}^T \mathbf{B}) = \sum_{i,j} A_{ij}B_{ij}
$$
其中 $\mathbf{A}^T$ 是 $\mathbf{A}$ 的转置。这个[内积](@entry_id:158127)诱导出一个范数，称为[弗罗贝尼乌斯范数](@entry_id:143384)，其平方为 $||\mathbf{A}||_F^2 = \langle \mathbf{A}, \mathbf{A} \rangle = \sum_{i,j} A_{ij}^2$。

利用这个[内积](@entry_id:158127)，我们可以证明球量部分和偏量部分是**正交**的，即它们的[内积](@entry_id:158127)为零：
$$
\langle \text{vol}(\mathbf{T}), \text{dev}(\mathbf{T}) \rangle = \left\langle \frac{1}{3}\text{tr}(\mathbf{T})\mathbf{I}, \mathbf{T} - \frac{1}{3}\text{tr}(\mathbf{T})\mathbf{I} \right\rangle
$$
为简化记号，令 $p = \frac{1}{3}\text{tr}(\mathbf{T})$，我们需计算 $\text{tr}((p\mathbf{I})^T(\mathbf{T} - p\mathbf{I}))$。由于 $p\mathbf{I}$ 是对称的，这等于 $\text{tr}(p\mathbf{I}(\mathbf{T} - p\mathbf{I})) = \text{tr}(p\mathbf{T} - p^2\mathbf{I})$。
$$
\text{tr}(p\mathbf{T} - p^2\mathbf{I}) = p\text{tr}(\mathbf{T}) - p^2\text{tr}(\mathbf{I}) = p(3p) - p^2(3) = 3p^2 - 3p^2 = 0
$$
正交性意味着，球量张量和偏量张量在张量空间中是“相互垂直”的。这导致了一个类似于[勾股定理](@entry_id:264352)的优美关系：
$$
||\mathbf{T}||_F^2 = ||\text{vol}(\mathbf{T}) + \text{dev}(\mathbf{T})||_F^2 = ||\text{vol}(\mathbf{T})||_F^2 + ||\text{dev}(\mathbf{T})||_F^2
$$
这个关系在[连续介质力学](@entry_id:155125)中非常有用，例如，它允许我们将总的弹性[能量分解](@entry_id:193582)为体积改变引起的能量和形状改变引起的能量。

从更抽象的角度看，这种分解实际上是一个**正交投影** [@problem_id:1506013]。所有迹为零的张量构成一个[子空间](@entry_id:150286)（偏量[子空间](@entry_id:150286)），所有球量张量（形式为 $k\mathbf{I}$）构成另一个[子空间](@entry_id:150286)。这两个[子空间](@entry_id:150286)是正交的。一个张量 $\mathbf{T}$ 的偏量部分 $\text{dev}(\mathbf{T})$ 是 $\mathbf{T}$ 在偏量[子空间](@entry_id:150286)上的[正交投影](@entry_id:144168)，而球量部分 $\text{vol}(\mathbf{T})$ 是 $\mathbf{T}$ 在球量[子空间](@entry_id:150286)上的正交投影。这意味着，在一个张量的所有迹为零的“近似”中，其偏量部分是最佳近似（即距离最近）[@problem_id:1506013]。

例如，我们可以计算给定[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的偏量部分的[弗罗贝尼乌斯范数](@entry_id:143384)的平方 [@problem_id:1505984]。

### 分解的客观性

物理定律不应依赖于观察者所选择的[坐标系](@entry_id:156346)。这一基本原理被称为**[物质客观性原理](@entry_id:191727)**。在数学上，这意味着描述物理定律的张量方程必须在[坐标系](@entry_id:156346)[旋转变换](@entry_id:200017)下保持形式不变（即具有[协变](@entry_id:634097)性）。

一个[坐标系](@entry_id:156346)旋转可以用一个正交张量 $\mathbf{Q}$（满足 $\mathbf{Q}\mathbf{Q}^T = \mathbf{Q}^T\mathbf{Q} = \mathbf{I}$）来描述。在旋转后的新[坐标系](@entry_id:156346)中，一个[二阶张量](@entry_id:199780) $\mathbf{S}$ 的分量会变为 $\mathbf{S}' = \mathbf{Q}\mathbf{S}\mathbf{Q}^T$。

一个重要的问题是：对变换后的张量 $\mathbf{S}'$ 进行分解，是否与先对 $\mathbf{S}$ 分解再对各部分进行变换得到的结果相同？答案是肯定的，这表明球量-偏量分解是**客观的**。

我们来证明偏量部分的客观性，即 $\text{dev}(\mathbf{Q}\mathbf{S}\mathbf{Q}^T) = \mathbf{Q}(\text{dev}(\mathbf{S}))\mathbf{Q}^T$ [@problem_id:1505961]。
根据定义：
$$
\text{dev}(\mathbf{S}') = \text{dev}(\mathbf{Q}\mathbf{S}\mathbf{Q}^T) = \mathbf{Q}\mathbf{S}\mathbf{Q}^T - \frac{1}{3}\text{tr}(\mathbf{Q}\mathbf{S}\mathbf{Q}^T)\mathbf{I}
$$
我们知道迹在相似变换下是[不变量](@entry_id:148850)，所以 $\text{tr}(\mathbf{Q}\mathbf{S}\mathbf{Q}^T) = \text{tr}(\mathbf{S})$。同时，单位张量 $\mathbf{I}$ 在任何[正交变换](@entry_id:155650)下也是不变的，因为 $\mathbf{Q}\mathbf{I}\mathbf{Q}^T = \mathbf{Q}\mathbf{Q}^T = \mathbf{I}$。利用这一点，我们可以巧妙地改写上式中的单位张量：
$$
\mathbf{I} = \mathbf{Q}\mathbf{I}\mathbf{Q}^T
$$
代入偏量张量的定义中：
$$
\text{dev}(\mathbf{S}') = \mathbf{Q}\mathbf{S}\mathbf{Q}^T - \frac{1}{3}\text{tr}(\mathbf{S})(\mathbf{Q}\mathbf{I}\mathbf{Q}^T)
$$
将 $\mathbf{Q}$ 和 $\mathbf{Q}^T$ 从右侧和左侧提出：
$$
\text{dev}(\mathbf{S}') = \mathbf{Q} \left( \mathbf{S} - \frac{1}{3}\text{tr}(\mathbf{S})\mathbf{I} \right) \mathbf{Q}^T = \mathbf{Q}(\text{dev}(\mathbf{S}))\mathbf{Q}^T
$$
同理可以证明 $\text{vol}(\mathbf{S}') = \mathbf{Q}(\text{vol}(\mathbf{S}))\mathbf{Q}^T$。

分解的客观性确保了“静水压力”和“剪应力”这些概念具有不依赖于[坐标系](@entry_id:156346)的物理意义。无论我们如何旋转我们的观察视角，一个给定的应力状态所对应的体积改变部分和形状改变部分是确定不变的。这为此分解在建立普适的材料本构关系（如[弹塑性](@entry_id:193198)模型）中奠定了坚实的理论基础。