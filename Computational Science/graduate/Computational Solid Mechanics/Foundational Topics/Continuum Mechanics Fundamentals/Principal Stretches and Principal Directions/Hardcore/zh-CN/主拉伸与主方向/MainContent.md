## 引言
在描述和分析物体如何在外力作用下变形时，主拉伸与[主方向](@entry_id:276187)是[连续介质力学](@entry_id:155125)中两个最核心、最基本的概念。它们超越了[坐标系](@entry_id:156346)的选择，以一种内在的方式精确量化了材料任意一点的局部拉伸与压缩。理解这些概念不仅是理论学习的基石，更是解决从工程结构设计到地球科学现象分析等复杂问题的关键。然而，许多工程师和研究人员虽然熟悉其定义，但对其深刻的物理内涵、稳健的数值计算方法以及在现代计算力学中的核心作用缺乏系统性的认识，这在处理大变形、[材料非线性](@entry_id:162855)和数值不稳定性问题时会成为瓶颈。本文旨在填补这一知识鸿沟。我们将通过三个章节，带领读者从理论基础走向前沿应用。第一章“原理与机制”将深入剖析主拉伸与主方向的[运动学](@entry_id:173318)定义、数学推导、与极分解的联系以及关键的数值计算挑战。第二章“应用与交叉学科联系”将展示这些概念如何在[超弹性本构模型](@entry_id:191665)、有限元算法设计、[生物力学](@entry_id:153973)和地球物理学等领域发挥关键作用。最后，第三章“动手实践”将通过一系列精心设计的编程练习，将理论知识转化为解决实际问题的能力。现在，让我们从构建这些概念的坚实基础开始，深入探讨其背后的原理与机制。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，理解一个物体如何变形是分析其力学响应的基础。变形的核心在于长度和角度的变化。主拉伸和主方向是描述这种几何变化的内在且基本的方式。本章将深入探讨主拉伸和主方向的运动学定义、物理意义、数学表述及其在计算方法中的关键问题。

### 从拉伸到变形张量：量化局部变形

考虑一个物体从其参考构型 $\mathcal{B}_0$ 运动到当前构型 $\mathcal{B}$。这个过程可以通过一个光滑的映射 $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X})$ 来描述，其中 $\boldsymbol{X}$ 是参考构型中的一个物[质点](@entry_id:186768)，而 $\boldsymbol{x}$ 是其在当前构型中的空间位置。为了量化这个映射在局部对几何形状的影响，我们引入**变形梯度**（deformation gradient）张量 $\boldsymbol{F}$ 。

变形梯度 $\boldsymbol{F}$ 是映射 $\boldsymbol{\varphi}$ 在点 $\boldsymbol{X}$ 的[切线](@entry_id:268870)映射，它将参考构型中一个无限小的物质[线元](@entry_id:196833) $d\boldsymbol{X}$ 线性地映射到当前构型中的空间[线元](@entry_id:196833) $d\boldsymbol{x}$：
$$
d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}
$$
在[坐标系](@entry_id:156346)中，其分量形式为 $F_{iJ} = \frac{\partial \varphi_i}{\partial X_J}$。为了保证变形在物理上是可接受的，即物质不会相互穿透且体积为正，我们要求 $\boldsymbol{F}$ 属于具有正[行列式](@entry_id:142978)的广义线性群 $GL^+(3)$，即 $\det(\boldsymbol{F}) > 0$。这个条件确保了映射的[局部可逆性](@entry_id:143266)和保[向性](@entry_id:144651) 。

变形的直接后果是[线元](@entry_id:196833)的长度变化。我们定义一个方向为 $\boldsymbol{N}$ (单位矢量) 的物质[线元](@entry_id:196833)的**拉伸比**（stretch ratio）$\lambda(\boldsymbol{N})$ 为其变形后与变形前长度之比：
$$
\lambda(\boldsymbol{N}) = \frac{\|d\boldsymbol{x}\|}{\|d\boldsymbol{X}\|} = \frac{\|\boldsymbol{F} d\boldsymbol{X}\|}{\|d\boldsymbol{X}\|} = \|\boldsymbol{F} \boldsymbol{N}\|
$$
为了便于分析，我们通常考察拉伸比的平方：
$$
\lambda^2(\boldsymbol{N}) = \|\boldsymbol{F} \boldsymbol{N}\|^2 = (\boldsymbol{F} \boldsymbol{N}) \cdot (\boldsymbol{F} \boldsymbol{N}) = (\boldsymbol{F} \boldsymbol{N})^{\top}(\boldsymbol{F} \boldsymbol{N}) = \boldsymbol{N}^{\top} \boldsymbol{F}^{\top} \boldsymbol{F} \boldsymbol{N}
$$
这个表达式自然地引出了一个核心的[对称张量](@entry_id:148092)——**右柯西-格林变形张量**（Right Cauchy-Green deformation tensor）$\boldsymbol{C}$ ：
$$
\boldsymbol{C} = \boldsymbol{F}^{\top} \boldsymbol{F}
$$
于是，拉伸比的平方可以简洁地写成一个二次型：
$$
\lambda^2(\boldsymbol{N}) = \boldsymbol{N}^{\top} \boldsymbol{C} \boldsymbol{N}
$$
$\boldsymbol{C}$ 张量完全定义了从参考构型度量的长度如何在当前构型中体现。同样，两个初始方向为 $d\boldsymbol{X}_1$ 和 $d\boldsymbol{X}_2$ 的[线元](@entry_id:196833)，在变形后其夹角 $\theta$ 的余弦值也可以通过 $\boldsymbol{C}$ 来表示 ：
$$
\cos\theta = \frac{d\boldsymbol{x}_1 \cdot d\boldsymbol{x}_2}{\|d\boldsymbol{x}_1\| \|d\boldsymbol{x}_2\|} = \frac{d\boldsymbol{X}_1 \cdot \boldsymbol{C} d\boldsymbol{X}_2}{\sqrt{(d\boldsymbol{X}_1 \cdot \boldsymbol{C} d\boldsymbol{X}_1)(d\boldsymbol{X}_2 \cdot \boldsymbol{C} d\boldsymbol{X}_2)}}
$$

**主拉伸**（principal stretches）被运动学地定义为拉伸比 $\lambda(\boldsymbol{N})$ 在所有可能的物质方向 $\boldsymbol{N}$ 上所能取得的极值（最大值、最小值和[鞍点](@entry_id:142576)值）。而这些[极值](@entry_id:145933)所对应的物质方向 $\boldsymbol{N}$ 就被称为**物质[主方向](@entry_id:276187)**（material principal directions）。

寻找 $\lambda^2(\boldsymbol{N})$ 在约束 $\boldsymbol{N} \cdot \boldsymbol{N}=1$ 下的[极值](@entry_id:145933)，是一个经典的[约束优化](@entry_id:635027)问题。其解表明，$\lambda^2$ 的极值是张量 $\boldsymbol{C}$ 的[特征值](@entry_id:154894)，而对应的方向 $\boldsymbol{N}$ 是 $\boldsymbol{C}$ 的[特征向量](@entry_id:151813)。因此，我们可以通过求解 $\boldsymbol{C}$ 的[特征值问题](@entry_id:142153)来确定主拉伸和主方向：
$$
\boldsymbol{C} \boldsymbol{N}_i = \lambda_i^2 \boldsymbol{N}_i \quad (\text{对 } i \text{ 不求和})
$$
这里，$\lambda_i^2$ 是 $\boldsymbol{C}$ 的三个[特征值](@entry_id:154894)，而主拉伸 $\lambda_i$ 则是它们的正平方根。对应的单位[特征向量](@entry_id:151813) $\boldsymbol{N}_i$ 就是三个相互正交的物质主方向。

**示例：** 假设一个均匀变形由以下变形梯度描述 ：
$$
\boldsymbol{F} = \begin{bmatrix} 2  1  0 \\ 0  2  0 \\ 0  0  \frac{1}{2} \end{bmatrix}
$$
首先计算[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C} = \boldsymbol{F}^{\top}\boldsymbol{F}$：
$$
\boldsymbol{C} = \begin{bmatrix} 2  0  0 \\ 1  2  0 \\ 0  0  \frac{1}{2} \end{bmatrix} \begin{bmatrix} 2  1  0 \\ 0  2  0 \\ 0  0  \frac{1}{2} \end{bmatrix} = \begin{bmatrix} 4  2  0 \\ 2  5  0 \\ 0  0  \frac{1}{4} \end{bmatrix}
$$
求解 $\boldsymbol{C}$ 的[特征值](@entry_id:154894) $(\lambda^2)$，我们得到 $\lambda_1^2 = \frac{9 + \sqrt{17}}{2}$, $\lambda_2^2 = \frac{9 - \sqrt{17}}{2}$ 以及 $\lambda_3^2 = \frac{1}{4}$。因此，三个主拉伸为：
$$
\lambda_1 = \sqrt{\frac{9 + \sqrt{17}}{2}}, \quad \lambda_2 = \sqrt{\frac{9 - \sqrt{17}}{2}}, \quad \lambda_3 = \frac{1}{2}
$$
对应的[特征向量](@entry_id:151813)（物质主方向）$\boldsymbol{N}_1, \boldsymbol{N}_2, \boldsymbol{N}_3$ 也可以通过求解 $(\boldsymbol{C} - \lambda_i^2 \boldsymbol{I})\boldsymbol{N}_i = \boldsymbol{0}$ 得到。

### 极分解与[谱分解](@entry_id:173707)：主拉伸的物理内涵

虽然我们可以通过 $\boldsymbol{C}$ 张量来计算主拉伸，但为了更深刻地理解其物理意义，**极分解**（polar decomposition）定理提供了更清晰的视角。任何满足 $\det(\boldsymbol{F})>0$ 的变形梯度 $\boldsymbol{F}$ 都可以唯一地分解为纯转动和纯拉伸的乘积：
$$
\boldsymbol{F} = \boldsymbol{R} \boldsymbol{U} = \boldsymbol{V} \boldsymbol{R}
$$
这里，$\boldsymbol{R}$ 是一个**转动张量**（rotation tensor），为正常正交张量（$\boldsymbol{R}^{\top}\boldsymbol{R} = \boldsymbol{I}, \det(\boldsymbol{R})=1$）。$\boldsymbol{U}$ 和 $\boldsymbol{V}$ 分别是**右[拉伸张量](@entry_id:193200)**（right stretch tensor）和**左[拉伸张量](@entry_id:193200)**（left stretch tensor），它们都是[对称正定](@entry_id:145886)张量。

将分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$ 代入 $\boldsymbol{C}$ 的定义，我们发现：
$$
\boldsymbol{C} = \boldsymbol{F}^{\top}\boldsymbol{F} = (\boldsymbol{R}\boldsymbol{U})^{\top}(\boldsymbol{R}\boldsymbol{U}) = \boldsymbol{U}^{\top}\boldsymbol{R}^{\top}\boldsymbol{R}\boldsymbol{U} = \boldsymbol{U}^{\top}\boldsymbol{U} = \boldsymbol{U}^2
$$
这个关系揭示了 $\boldsymbol{U}$ 是 $\boldsymbol{C}$ 的唯一[对称正定](@entry_id:145886)平方根，即 $\boldsymbol{U}=\sqrt{\boldsymbol{C}}$。由于 $\boldsymbol{U}$ 和 $\boldsymbol{C}$ 仅通过平方关系相连，它们共享相同的[特征向量](@entry_id:151813)（即物质[主方向](@entry_id:276187) $\boldsymbol{N}_i$），且 $\boldsymbol{U}$ 的[特征值](@entry_id:154894)恰好是主拉伸 $\lambda_i$。这赋予了 $\boldsymbol{U}$ 明确的物理意义：它是一个完全描述参考构型中纯拉伸变形的张量。

同样，我们可以定义**左柯西-格林变形张量**（Left Cauchy-Green deformation tensor）$\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\top}$。可以证明 $\boldsymbol{B} = \boldsymbol{V}^2$，且 $\boldsymbol{B}$ 的[特征值](@entry_id:154894)与 $\boldsymbol{C}$ 相同（均为 $\lambda_i^2$），因此 $\boldsymbol{V}$ 的[特征值](@entry_id:154894)也是主拉伸 $\lambda_i$ 。

一个重要的结论是，主拉伸是**右[拉伸张量](@entry_id:193200)** $\boldsymbol{U}$（或左[拉伸张量](@entry_id:193200) $\boldsymbol{V}$）的[特征值](@entry_id:154894)，而不是变形梯度 $\boldsymbol{F}$ 本身的[特征值](@entry_id:154894)。$\boldsymbol{F}$ 通常是非对称的，其[特征值](@entry_id:154894)可以是复数，而拉伸比必须是实数和正数。例如，对于一个纯[刚体转动](@entry_id:191086) $\boldsymbol{F}=\boldsymbol{R}$，没有任何拉伸，因此所有主拉伸都为1，但这时的 $\boldsymbol{F}$ 的[特征值](@entry_id:154894)可能是复数 $e^{\pm i\theta}$  。

从线性代数的角度看，主拉伸是变形梯度 $\boldsymbol{F}$ 的**[奇异值](@entry_id:152907)**（singular values）。任何矩阵 $\boldsymbol{F}$ 都可以进行奇异值分解（SVD）：$\boldsymbol{F} = \boldsymbol{W} \boldsymbol{\Sigma} \boldsymbol{Q}^{\top}$，其中 $\boldsymbol{W}$ 和 $\boldsymbol{Q}$ 是正交矩阵，$\boldsymbol{\Sigma}$ 是一个对角矩阵，其对角元为非负的[奇异值](@entry_id:152907)。可以证明，$\boldsymbol{C}$ 的[特征值](@entry_id:154894)是 $\boldsymbol{F}$ 奇异值的平方，因此主拉伸 $\lambda_i$ 就是 $\boldsymbol{F}$ 的[奇异值](@entry_id:152907) 。

### [主方向](@entry_id:276187)：物质视角与空间视角

我们已经确定，物质主方向 $\boldsymbol{N}_i$ 是 $\boldsymbol{U}$ 和 $\boldsymbol{C}$ 的[特征向量](@entry_id:151813)，它们定义在参考构型中，并且是正交的。这些方向代表了材料内部经历纯拉伸而没有剪切变形的三个初始方向。

那么，这些方向在变形后会变成什么样呢？考虑一个沿着物质主方向 $\boldsymbol{N}_i$ 的[线元](@entry_id:196833) $d\boldsymbol{X}_i$，其变形后的像为 $d\boldsymbol{x}_i$：
$$
d\boldsymbol{x}_i = \boldsymbol{F} d\boldsymbol{X}_i = (\boldsymbol{R}\boldsymbol{U}) \boldsymbol{N}_i = \boldsymbol{R} (\boldsymbol{U}\boldsymbol{N}_i) = \boldsymbol{R} (\lambda_i \boldsymbol{N}_i) = \lambda_i (\boldsymbol{R} \boldsymbol{N}_i)
$$
这个结果的几何意义非常清晰：一个初始沿着主方向 $\boldsymbol{N}_i$ 的[线元](@entry_id:196833)，首先被拉伸了 $\lambda_i$ 倍（由 $\boldsymbol{U}$ 作用），然后随着周围的材料一起被刚性地旋转了 $\boldsymbol{R}$ 。

变形后的方向由单位矢量 $\boldsymbol{n}_i = \boldsymbol{R}\boldsymbol{N}_i$ 给出。这些 $\boldsymbol{n}_i$ 被称为**空间[主方向](@entry_id:276187)**（spatial principal directions）。它们是左[拉伸张量](@entry_id:193200) $\boldsymbol{V}$ 和[左柯西-格林张量](@entry_id:186163) $\boldsymbol{B}$ 的[特征向量](@entry_id:151813)，并且也构成一个[正交系](@entry_id:184795)。

**示例：** 考虑一个变形，其转动张量 $\boldsymbol{R}$ 是绕 $\boldsymbol{e}_3$ 轴旋转 $\pi/3$。若一个物质主方向为 $\boldsymbol{N}_1 = \frac{1}{\sqrt{2}}(1, 1, 0)^{\top}$，则对应的空间[主方向](@entry_id:276187) $\boldsymbol{n}_1$ 就是 ：
$$
\boldsymbol{n}_1 = \boldsymbol{R}\boldsymbol{N}_1 = \begin{pmatrix} \cos(\pi/3)  -\sin(\pi/3)  0 \\ \sin(\pi/3)  \cos(\pi/3)  0 \\ 0  0  1 \end{pmatrix} \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix} = \frac{1}{2\sqrt{2}} \begin{pmatrix} 1-\sqrt{3} \\ 1+\sqrt{3} \\ 0 \end{pmatrix}
$$
这清楚地表明，空间[主方向](@entry_id:276187)就是物质[主方向](@entry_id:276187)经过变形中的[刚体转动](@entry_id:191086) $\boldsymbol{R}$ 后的方向。

### 客观性与[不变量](@entry_id:148850)

在连续介质力学中，一个量如果是**客观的**（objective）或称**标架无关的**（frame-indifferent），意味着它在叠加一个任意的[刚体运动](@entry_id:193355)（即改变观察者）后保持不变。一个叠加的[刚体转动](@entry_id:191086)由一个正交张量 $\boldsymbol{Q}$ 描述，它使当前位置 $\boldsymbol{x}$ 变为 $\boldsymbol{x}^* = \boldsymbol{Q}\boldsymbol{x}$。在这种变换下，新的变形梯度变为 $\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}$。

我们来考察各个变形张量的变换规律 ：
- 新的[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}^* = (\boldsymbol{F}^*)^{\top}\boldsymbol{F}^* = (\boldsymbol{Q}\boldsymbol{F})^{\top}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\top}\boldsymbol{Q}^{\top}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\top}\boldsymbol{F} = \boldsymbol{C}$。
- 新的[左柯西-格林张量](@entry_id:186163) $\boldsymbol{B}^* = \boldsymbol{F}^*(\boldsymbol{F}^*)^{\top} = (\boldsymbol{Q}\boldsymbol{F})(\boldsymbol{Q}\boldsymbol{F})^{\top} = \boldsymbol{Q}\boldsymbol{F}\boldsymbol{F}^{\top}\boldsymbol{Q}^{\top} = \boldsymbol{Q}\boldsymbol{B}\boldsymbol{Q}^{\top}$。

由于 $\boldsymbol{C}$ 在叠加刚体运动后保持不变，它的[特征值](@entry_id:154894)（$\lambda_i^2$）和[特征向量](@entry_id:151813)（$\boldsymbol{N}_i$）也都不变。这意味着**主拉伸**和**物质主方向**都是客观量，它们是变形的内在度量，与观察者无关  。相反，空间[主方向](@entry_id:276187) $\boldsymbol{n}_i$ 却会跟随观察者一起转动（$\boldsymbol{n}_i^* = \boldsymbol{Q}\boldsymbol{n}_i$），这正是一个客观矢量的变换规则。

从主拉伸可以构造出不随[坐标系](@entry_id:156346)旋转而改变的标量，即**[主不变量](@entry_id:193522)**（principal invariants）。对于 $\boldsymbol{C}$ 张量，其三个[主不变量](@entry_id:193522) $I_1(\boldsymbol{C}), I_2(\boldsymbol{C}), I_3(\boldsymbol{C})$ 可以用主拉伸表示为 ：
$$
I_1(\boldsymbol{C}) = \mathrm{tr}(\boldsymbol{C}) = \lambda_1^2 + \lambda_2^2 + \lambda_3^2
$$
$$
I_2(\boldsymbol{C}) = \frac{1}{2}[(\mathrm{tr}(\boldsymbol{C}))^2 - \mathrm{tr}(\boldsymbol{C}^2)] = \lambda_1^2 \lambda_2^2 + \lambda_2^2 \lambda_3^2 + \lambda_3^2 \lambda_1^2
$$
$$
I_3(\boldsymbol{C}) = \det(\boldsymbol{C}) = \lambda_1^2 \lambda_2^2 \lambda_3^2
$$
这些[不变量](@entry_id:148850)在构建**[应变能密度函数](@entry_id:755490)**（strain energy density functions）时至关重要。

体积变化率 $J = \det(\boldsymbol{F})$ 也与主拉伸直接相关。利用极分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$，我们有：
$$
J = \det(\boldsymbol{F}) = \det(\boldsymbol{R}\boldsymbol{U}) = \det(\boldsymbol{R})\det(\boldsymbol{U}) = 1 \cdot (\lambda_1 \lambda_2 \lambda_3) = \lambda_1 \lambda_2 \lambda_3
$$
体积变化率就是三个主拉伸的乘积。因此，第三[主不变量](@entry_id:193522)可以写为 $I_3(\boldsymbol{C}) = J^2$。对于体积不可压缩（或称等容）变形，我们有 $J=1$，即 $\lambda_1 \lambda_2 \lambda_3 = 1$ 。

### 计算方法与数值问题

在[计算固体力学](@entry_id:169583)中，特别是在有限元分析的每个积分点上，我们需要高效且准确地计算主拉伸和[主方向](@entry_id:276187)。主要有两种途径 ：

1.  **基于 $\boldsymbol{C}$ 的[特征值分解](@entry_id:272091)**：首先计算 $\boldsymbol{C} = \boldsymbol{F}^{\top}\boldsymbol{F}$，然后对其进行[特征值分解](@entry_id:272091)。
2.  **基于 $\boldsymbol{F}$ 的[奇异值分解 (SVD)](@entry_id:172448)**：直接对 $\boldsymbol{F}$ 进行 SVD 分解，$\boldsymbol{F} = \boldsymbol{W} \boldsymbol{\Sigma} \boldsymbol{Q}^{\top}$。

比较这两种方法：
- **数值稳定性**：SVD 方法通常更为稳健。计算 $\boldsymbol{C}$ 的过程会平方 $\boldsymbol{F}$ 的[奇异值](@entry_id:152907)，从而平方其条件数（$\kappa(\boldsymbol{C}) = \kappa(\boldsymbol{F})^2$）。当变形高度各向异性时（即最大和最小主拉伸相差悬殊），$\boldsymbol{F}$ 的[条件数](@entry_id:145150)已经很大，计算 $\boldsymbol{C}$ 会使问题变得更加病态，可能导致小[特征值](@entry_id:154894)的精度损失 。
- **计算需求**：如果计算任务只需要主拉伸和物质[主方向](@entry_id:276187)（例如，用于各向同性[弹塑性](@entry_id:193198)本构），对[对称矩阵](@entry_id:143130) $\boldsymbol{C}$ 进行[特征值分解](@entry_id:272091)可能在计算上略微便宜。然而，如果还需要转动张量 $\boldsymbol{R}$（例如，在更新各向异性材料的织构张量时），SVD 方法则更具优势，因为它直接提供了 $\boldsymbol{R} = \boldsymbol{W}\boldsymbol{Q}^{\top}$，避免了先计算 $\boldsymbol{U}=\sqrt{\boldsymbol{C}}$ 再通过 $\boldsymbol{R}=\boldsymbol{F}\boldsymbol{U}^{-1}$ 求解的复杂步骤 。

一个更微妙但至关重要的数值问题出现在**主拉伸重复或几乎重复**的情况下 。
- **非唯一性**：当两个或三个主拉伸相等时（例如，$\lambda_1=\lambda_2$），$\boldsymbol{C}$ 的[特征值](@entry_id:154894)出现重根。此时，与该[重复特征值](@entry_id:154579)对应的特征[子空间](@entry_id:150286)是多维的（例如，一个二维平面）。该[子空间](@entry_id:150286)内的**任何**一组[正交基](@entry_id:264024)都可以作为有效的[主方向](@entry_id:276187)。这意味着[主方向](@entry_id:276187)的选取变得非唯一。
- **敏感性**：当主拉伸非常接近但又不完全相等时（“几乎简并”），主方向会变得对 $\boldsymbol{F}$ 的微小扰动极其敏感。一个微小的[剪切变形](@entry_id:170920)就可能导致[主方向](@entry_id:276187)发生剧烈的转动。我们可以量化这种敏感性。考虑一个2D变形，其主拉伸之差由小参数 $\delta$ 控制，而一个剪切扰动由 $\varepsilon$ 控制。可以推导出，主方向角 $\theta$ 对扰动的敏感度 $S(\delta) = \frac{d\theta}{d\varepsilon}|_{\varepsilon=0}$ 与 $\delta$ 成反比 ：
$$
S(\delta) = \frac{1+\delta}{4\delta}
$$
当 $\delta \to 0$ 时，$S(\delta) \to \infty$。这意味着对于几乎重复的主拉伸，数值计算中不可避免的微小误差都可能导致[主方向](@entry_id:276187)的剧烈、非物理的[振荡](@entry_id:267781)，从而破坏[迭代算法](@entry_id:160288)（如[牛顿-拉弗森法](@entry_id:140620)）的收敛性。

为了解决这个问题，必须采用一个**一致的选取规则**。纯粹的代数规则（如按分量大小排序）是不可取的，因为它不满足[旋转不变性](@entry_id:137644)。正确的做法是基于物理或几何的连续性。在数值实现中，这通常意味着利用加载历史：在出现[重复特征值](@entry_id:154579)的点，选择一组[主方向](@entry_id:276187)，使其与上一个增量步或迭代步中的[主方向](@entry_id:276187)“最接近”。这可以通过求解一个小型的Procrustes问题来实现，或者通过对一个微扰问题取极限来定义唯一的方向，确保主方向场在变形过程中是连续的 。这种处理对于开发稳健的有限元代码至关重要。