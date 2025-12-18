## 引言
[线性动量守恒](@entry_id:165717)是物理学的基石定律之一，在连续介质力学中，它化身为宏伟的[柯西运动方程](@entry_id:204126)。该方程以其深刻的物理内涵和普适的数学形式，成为了描述从空气流动、[海洋环流](@entry_id:195237)到细胞运动和地质构造演化等万千现象的统一语言。然而，对于初学者和研究人员而言，一个关键的挑战在于理解如何从这一基本原理出发，通过构建恰当的应力[本构关系](@entry_id:186508)和耦合其他物理定律，来精确捕捉特定材料（如聚合物、生物组织）的复杂行为，并将其转化为可靠的[计算模型](@entry_id:637456)。

本文旨在系统性地解决这一问题。我们将带领读者深入探索[柯西运动方程](@entry_id:204126)的世界，不仅仅是推导其数学形式，更重要的是揭示其背后的物理机制和其在现代科学与工程计算中的强大生命力。

- 在“原理与机制”一章中，我们将从[牛顿第二定律](@entry_id:274217)出发，循序渐进地推导出[柯西运动方程](@entry_id:204126)，并深入剖析[物质导数](@entry_id:262900)、[应力张量](@entry_id:148973)等核心概念的物理意义及其对数值方法的影响。
- 接着，在“应用与跨学科联系”一章中，我们将展示该方程如何通过不同的简化和扩展，应用于经典流体力学、[非牛顿流体](@entry_id:154737)、多孔介质、[活性物质](@entry_id:186169)乃至[固体力学](@entry_id:164042)等广阔领域，彰显其作为连接不同学科桥梁的非凡能力。
- 最后，在“动手实践”部分，您将通过三个精心设计的计算问题，将理论知识应用于实际的解析推导和数值编程中，从而巩固和深化您的理解。

通过本次学习，您将建立起一个从基本物理原理到高级计算应用的完整知识框架，为您在[复杂流体](@entry_id:198415)及相关领域的深入研究奠定坚实的基础。

## 原理与机制

在对[复杂流体](@entry_id:198415)的计算研究中，[动量守恒](@entry_id:149964)定律构成了[流体动力学分析](@entry_id:268621)的核心。作为牛顿第二定律在连续介质中的体现，该定律最终以[柯西运动方程](@entry_id:204126)的形式呈现。本章旨在深入阐述该方程的物理原理与内在机制，从其基本推导到各组成部分的深刻含义，再到其在计算方法中的具体应用。

### [柯西运动方程](@entry_id:204126)：牛顿第二定律的局域表述

我们从一个在空间中运动的任意物质体（一个由相同流体质点组成的集合）$V(t)$ 出发。根据牛顿第二定律，该物质体总线性动量的变化率等于作用在其上的所有外力之和。这些外力可分为两类：作用于整个体积的**[体力](@entry_id:174230)**（如重力）和作用于其边界 $\partial V(t)$ 的**面力**（如压力和粘性力）。其积分形式可写作：

$$
\frac{d}{dt} \int_{V(t)} \rho \mathbf{v} \, dV = \int_{V(t)} \rho \mathbf{b} \, dV + \oint_{\partial V(t)} \mathbf{t} \, dS
$$

其中，$\rho$ 是流体的质量密度，$\mathbf{v}$ 是速度场，$\mathbf{b}$ 是单位质量的[体力](@entry_id:174230)，而 $\mathbf{t}$ 是作用在边界微元 $dS$ 上的[面力矢量](@entry_id:189429)，也称为**牵[引力](@entry_id:189550)矢量**。

为了得到一个适用于空间固定点（[欧拉描述](@entry_id:264722)）的[偏微分](@entry_id:194612)方程，我们需要将上式中的各项进行转换。首先，牵[引力](@entry_id:189550)矢量的概念通过**柯西应力原理**得到了深化。该原理指出，对于给定点和给定时刻，牵[引力](@entry_id:189550)矢量 $\mathbf{t}$ 仅依赖于该点处表面的法向矢量 $\mathbf{n}$，并且这种依赖关系是线性的。这种[线性映射](@entry_id:185132)由一个[二阶张量](@entry_id:199780)——**柯西应力张量** $\boldsymbol{\sigma}$ 来描述  。这一关系式，即**柯西公式**，写作：

$$
\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n}
$$

或者在分量形式下为 $t_i = \sigma_{ij} n_j$（采用 $\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$ 的约定）。应力张量 $\sigma_{ij}$ 的物理意义是作用在法向为第 $j$ 个坐标轴方向的面元上，力矢量的第 $i$ 个分量。

借助[高斯散度定理](@entry_id:188065)，我们可以将作用于边界的面力积分转换成一个体积积分：

$$
\oint_{\partial V(t)} \mathbf{t} \, dS = \oint_{\partial V} (\boldsymbol{\sigma} \cdot \mathbf{n}) \, dS = \int_{V} (\nabla \cdot \boldsymbol{\sigma}) \, dV
$$

同时，方程左侧对物质体积积分的时间导数可以通过**[雷诺输运定理](@entry_id:191217)**转换到空间固定体积 $V$ 上：

$$
\frac{d}{dt} \int_{V(t)} \rho \mathbf{v} \, dV = \int_{V} \left( \frac{\partial (\rho \mathbf{v})}{\partial t} + \nabla \cdot (\rho \mathbf{v} \otimes \mathbf{v}) \right) dV
$$

将这些转换后的表达式代入原始的[动量平衡](@entry_id:1128118)方程，我们得到一个对任意固定体积 $V$ 都成立的[积分方程](@entry_id:138643)。根据**局域化原理**，如果一个[连续函数](@entry_id:137361)的积分在任意体积上都为零，那么这个函数本身必然处处为零。由此，我们得到了[动量守恒](@entry_id:149964)的微分形式，也称为[动量方程](@entry_id:197225)的**守恒形式**：

$$
\frac{\partial (\rho \mathbf{v})}{\partial t} + \nabla \cdot (\rho \mathbf{v} \otimes \mathbf{v}) = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$

这里，$\rho \mathbf{v} \otimes \mathbf{v}$ 是一个[二阶张量](@entry_id:199780)，表示动量的[对流输运](@entry_id:149512)。

为了进一步理解方程的物理意义，我们可以利用[质量守恒定律](@entry_id:147377)（[连续性方程](@entry_id:195013)）$\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0$ 来展开上式左侧。经过变换，我们得到：

$$
\rho \left( \frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla) \mathbf{v} \right) = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$

括号中的项 $\frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla) \mathbf{v}$ 定义了一个新的导数，即**[物质导数](@entry_id:262900)**（或称[随体导数](@entry_id:204621)），记作 $\frac{D\mathbf{v}}{Dt}$。于是，我们得到了**柯西第一运动定律**的最终形式 ：

$$
\rho \frac{D\mathbf{v}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$

这个方程优雅地阐述了：单位体积内流体微元的质量乘以其加速度（左侧），等于作用在该微元上的[表面力](@entry_id:188034)（应力[梯度的散度](@entry_id:270716)）与[体力](@entry_id:174230)之和（右侧）。

### 物质导数：捕捉流场中的加速度

在[欧拉描述](@entry_id:264722)下，一个流体质点的加速度并不能简单地用速度场在固定点的[局部时](@entry_id:194383)间变化率 $\frac{\partial \mathbf{v}}{\partial t}$ 来衡量。一个[质点](@entry_id:186768)在运动时，其速度的变化来源于两个方面：一是流场本身随时间演化（非定常效应）；二是因为质点运动到了流场中速度不同的新位置（空间不均匀效应）。

物质导数精确地捕捉了这两个效应。考虑一个跟随流体运动的[质点](@entry_id:186768)，其轨迹为 $\mathbf{x}_p(t)$。其速度定义为 $\mathbf{v}_p(t) = \mathbf{v}(\mathbf{x}_p(t), t)$。根据[多元函数](@entry_id:145643)求导的[链式法则](@entry_id:190743)，该[质点](@entry_id:186768)的加速度为：

$$
\mathbf{a}_p = \frac{d\mathbf{v}_p}{dt} = \frac{d}{dt} \mathbf{v}(\mathbf{x}_p(t), t) = \frac{\partial \mathbf{v}}{\partial t} + \left( \frac{d\mathbf{x}_p}{dt} \cdot \nabla \right) \mathbf{v}
$$

由于 $\frac{d\mathbf{x}_p}{dt}$ 正是该质点的速度 $\mathbf{v}$，我们得到了物质导数的完整表达式 ：

$$
\frac{D\mathbf{v}}{Dt} = \underbrace{\frac{\partial \mathbf{v}}{\partial t}}_{\text{局部加速度}} + \underbrace{(\mathbf{v} \cdot \nabla) \mathbf{v}}_{\text{对流加速度}}
$$

**[局部加速度](@entry_id:272847)** $\frac{\partial \mathbf{v}}{\partial t}$ 衡量在空间固定点上速度随时间的变化，它仅在[非定常流](@entry_id:269993)动中非零。而**[对流加速度](@entry_id:263153)** $(\mathbf{v} \cdot \nabla) \mathbf{v}$ 则描述了[质点](@entry_id:186768)因移动到速度场中不同位置而经历的速度变化，即使在[定常流](@entry_id:191654)（$\frac{\partial \mathbf{v}}{\partial t} = \mathbf{0}$）中，只要速度场在空间上不均匀，[对流加速度](@entry_id:263153)也可以非零。

例如，考虑一个一维[定常流](@entry_id:191654)动，其速度场为 $\mathbf{v}(\mathbf{x}) = \gamma x \hat{\mathbf{e}}_x$（其中 $\gamma$ 为正常数）。在此流场中，任何固定点 $x$ 的速度都不随时间变化，因此[局部加速度](@entry_id:272847) $\frac{\partial \mathbf{v}}{\partial t} = \mathbf{0}$。然而，一个流体[质点](@entry_id:186768)在运动时，其加速度为：

$$
\frac{D\mathbf{v}}{Dt} = (\mathbf{v} \cdot \nabla) \mathbf{v} = \left( (\gamma x) \frac{\partial}{\partial x} \right) (\gamma x \hat{\mathbf{e}}_x) = \gamma^2 x \hat{\mathbf{e}}_x
$$

这表明，尽[管流](@entry_id:189531)场是定常的，但由于质点流向 $x$ 增大的方向时速度不断增加，它仍然在经历着非零的加速度 。

通过将[柯西运动方程](@entry_id:204126)写成包含瞬态和对流贡献的显式形式，即 $\rho \frac{\partial \mathbf{v}}{\partial t} + \rho (\mathbf{v} \cdot \nabla)\mathbf{v} = \dots$，我们可以通过[量纲分析](@entry_id:140259)来比较这两项[惯性力](@entry_id:169104)的相对重要性。定义[特征速度](@entry_id:165394)为 $U$，特征长度为 $L$，特征时间为 $T$，则瞬态惯性力尺度为 $\rho U/T$，对流惯性力尺度为 $\rho U^2/L$。两者的比值定义了**[斯特劳哈尔数](@entry_id:139591) (Strouhal number, St)**：

$$
St = \frac{L}{UT}
$$

当 $St \ll 1$ 时，表明对流惯性项远大于瞬态惯性项，此时流动主要由空间变化主导，而非时间变化 。

### 柯西[应力张量](@entry_id:148973)：连续介质内部的力

应力张量 $\boldsymbol{\sigma}$ 概括了连续介质内部所有[接触力](@entry_id:165079)的复杂性。它的性质直接决定了流体的力学行为。

#### 应力张量的意义与对称性

正如我们已经看到的，柯西应力张量通过柯西公式将表面法向与牵[引力](@entry_id:189550)联系起来。然而，这个张量还有一个至关重要的内禀属性：**对称性**。

在经典连续介质理论中，除了线动量守恒外，角动量也必须守恒。对于一个没有[体力](@entry_id:174230)矩和面力矩（即没有所谓的“偶应力”）的系统，[角动量守恒](@entry_id:156798)定律的局域化形式最终会导出一个纯代数约束：

$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\top} \quad \text{或} \quad \sigma_{ij} = \sigma_{ji}
$$

这被称为**柯西第二运动定律** 。这个结论意味着，在经典框架下，应力张量必然是对称的。如果 $\boldsymbol{\sigma}$ 不是对称的，其反对称部分将产生一个净的内部体力矩密度 $\boldsymbol{\tau}_{\sigma}$，其分量为 $(\boldsymbol{\tau}_{\sigma})_i = \epsilon_{ijk} \sigma_{kj}$，其中 $\epsilon_{ijk}$ 是[列维-奇维塔符号](@entry_id:193594)。例如，对于一个假设的[非对称应力张量](@entry_id:184161)，其反对称部分会导致一个非零的力矩，这在没有相应物理机制（如偶应力）来平衡的情况下，会违反[角动量守恒](@entry_id:156798) 。

值得注意的是，在更高级的连续介质模型中，如**微极流体 (micropolar fluid)** 或 **Cosserat 连续介质**理论，物质点被认为具有独立的[转动自由度](@entry_id:141502)（微观旋转）。这些理论引入了偶应力张量 $\mathbf{m}$ 和体力矩密度 $\mathbf{c}$。在这种情况下，[角动量平衡](@entry_id:181848)方程会发生改变，应力[张量的反对称部分](@entry_id:193562)由偶[应力的散度](@entry_id:185633)、体力矩以及微观转动的惯性项来平衡，因此 $\boldsymbol{\sigma}$ 不再必须对称 。然而，本课程主要关注经典的柯西连续介质。

#### [应力分解](@entry_id:272862)：压力与[偏应力](@entry_id:163323)

为了更好地分析流体的行为，通常将柯西[应力张量](@entry_id:148973)分解为其**球量部分**和**偏量部分**：

$$
\boldsymbol{\sigma} = -p \mathbf{I} + \boldsymbol{\tau}
$$

其中，$\mathbf{I}$ 是单位张量。标量 $p$ 被定义为**[机械压力](@entry_id:263227)**，它代表了各向同性的[正应力](@entry_id:260622)（约定正压力产生压缩）。在[静止流体](@entry_id:187621)中，$p$ 就是[热力学压力](@entry_id:1133073)。[二阶张量](@entry_id:199780) $\boldsymbol{\tau}$ 被称为**[偏应力张量](@entry_id:267642)**或**附加应力张量**，它描述了由流体运动引起的偏离[各向同性压力](@entry_id:269937)的所有应力，主要包括[粘性应力](@entry_id:261328)。由于 $\mathbf{I}$ 是对称的，$\boldsymbol{\sigma}$ 的对称性要求 $\boldsymbol{\tau}$ 也必须是对称的。

将此分解代入[柯西运动方程](@entry_id:204126)，我们得到一个更为熟悉的形式：

$$
\rho \frac{D\mathbf{v}}{Dt} = -\nabla p + \nabla \cdot \boldsymbol{\tau} + \rho \mathbf{b}
$$

这个形式明确地分开了压力[梯度力](@entry_id:166847)、由[偏应力](@entry_id:163323)产生的力（通常是[粘性力](@entry_id:263294)）和体力。对于[理想流体](@entry_id:1126341)（无粘性），[偏应力张量](@entry_id:267642) $\boldsymbol{\tau} = \mathbf{0}$，方程简化为著名的**欧拉方程** 。对于牛顿流体，[偏应力张量](@entry_id:267642)与[应变率张量](@entry_id:266108)成线性关系。而对于非牛顿[复杂流体](@entry_id:198415)，$\boldsymbol{\tau}$ 的[本构关系](@entry_id:186508)则要复杂得多。

#### 应力、变形与能量耗散

[动量方程](@entry_id:197225)与能量守恒之间存在着深刻的联系。通过将动量方程与[速度矢量](@entry_id:269648) $\mathbf{v}$ 做点积，我们可以得到机械能（此处为动能）的平衡方程。在这个过程中，应力所做的功率项以 $\boldsymbol{\sigma} : \nabla\mathbf{v}$ 的形式出现，这代表单位体积内应力做功的速率 。

为了理解这一项的物理意义，我们将[速度梯度张量](@entry_id:270928) $\nabla\mathbf{v}$ 分解为对称[部分和](@entry_id:162077)反对称部分：
*   **[应变率张量](@entry_id:266108)** $\mathbf{D} = \frac{1}{2}(\nabla\mathbf{v} + (\nabla\mathbf{v})^\top)$，描述了流体微元的拉伸和[剪切变形](@entry_id:170920)速率。
*   **[自旋张量](@entry_id:187346)** $\mathbf{W} = \frac{1}{2}(\nabla\mathbf{v} - (\nabla\mathbf{v})^\top)$，描述了流体微元的刚性旋转速率。

于是，[应力功率](@entry_id:182907)可以写作：
$$
\boldsymbol{\sigma} : \nabla\mathbf{v} = \boldsymbol{\sigma} : (\mathbf{D} + \mathbf{W}) = \boldsymbol{\sigma} : \mathbf{D} + \boldsymbol{\sigma} : \mathbf{W}
$$

由于 $\boldsymbol{\sigma}$ 是[对称张量](@entry_id:148092)而 $\mathbf{W}$ 是[反对称张量](@entry_id:199349)，它们之间的[双点积](@entry_id:748648)恒为零，即 $\boldsymbol{\sigma} : \mathbf{W} = 0$ 。这意味着，对于经典连续介质，**应力在纯刚性转动中不做功**。所有内功都由变形产生。

进一步代入[应力分解](@entry_id:272862)式 $\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}$：
$$
\boldsymbol{\sigma} : \mathbf{D} = (-p\mathbf{I} + \boldsymbol{\tau}) : \mathbf{D} = -p (\mathbf{I} : \mathbf{D}) + \boldsymbol{\tau} : \mathbf{D} = -p (\nabla \cdot \mathbf{v}) + \boldsymbol{\tau} : \mathbf{D}
$$
这表明，[应力功率](@entry_id:182907)由两部分组成：压力在体积变化（由 $\nabla \cdot \mathbf{v}$ 衡量）中所做的功，以及[偏应力](@entry_id:163323)在变形中所做的功。

对于**不可压缩流体**，$\nabla \cdot \mathbf{v} = 0$，压力项消失，[应力功率](@entry_id:182907)完全来自于[偏应力](@entry_id:163323)：
$$
\boldsymbol{\sigma} : \nabla\mathbf{v} = \boldsymbol{\tau} : \mathbf{D}
$$
根据[热力学](@entry_id:172368)第二定律，对于纯粹耗散的流体，粘性力所做的功必须转化为内能（热量），而不能从内能中凭空产生[机械能](@entry_id:162989)。这意味着[应力功率](@entry_id:182907)项必须非负，即：
$$
\boldsymbol{\tau} : \mathbf{D} \ge 0
$$
这一条件被称为**[耗散不等式](@entry_id:188634)**，它要求将应变率 $\mathbf{D}$ 映射到[偏应力](@entry_id:163323) $\boldsymbol{\tau}$ 的本构关系必须是**半正定的**。这为[复杂流体](@entry_id:198415)的本构模型施加了重要的[热力学约束](@entry_id:755911) 。

### [不可压缩流](@entry_id:140301)动的特殊情况

对于许多液体和低速气体流动，不可压缩假设（$\rho = \text{常数}$，从而 $\nabla \cdot \mathbf{v} = 0$）是一个极好的近似。在这种情况下，压力 $p$ 的角色发生了根本性的变化。

在可压缩流动中，压力、密度和温度通过状态方程（如理想气体定律）相互关联。然而，在不可压缩模型中，密度是固定的，压力与密度[解耦](@entry_id:160890)。此时，压力不再是一个[热力学状态变量](@entry_id:151686)，而变成一个纯粹的力学变量。它的作用是充当一个**拉格朗日乘子**，其值会瞬时调整，以确保速度场在任何时候都满足**不可压缩约束** $\nabla \cdot \mathbf{v} = 0$ 。

由于压力 $p$ 在[动量方程](@entry_id:197225)中仅以其梯度 $\nabla p$ 的形式出现，这意味着如果 $(\mathbf{v}, p)$ 是一个解，那么 $(\mathbf{v}, p+C)$（其中 $C$ 是任意[空间常数](@entry_id:193491)）也必然是一个解。因此，[不可压缩流](@entry_id:140301)动的压[力场](@entry_id:147325)只能被确定到一个任意的附加常数 。在实际计算中，通常通过在某一点指定压力值或施加一个全局约束（如域内压力平均值为零）来消除这种不确定性。

### 对计算方法的影响

[柯西运动方程](@entry_id:204126)的数学结构深刻地影响了[计算流体动力学](@entry_id:142614)（CFD）中的数值离散方法。

#### [守恒形式](@entry_id:1122899)与[有限体积法 (FVM)](@entry_id:749403)

将[动量方程](@entry_id:197225)写成其守恒形式对于**[有限体积法](@entry_id:141374) (Finite Volume Method, FVM)** 尤为重要：

$$
\frac{\partial (\rho \mathbf{v})}{\partial t} + \nabla \cdot (\rho \mathbf{v} \otimes \mathbf{v} - \boldsymbol{\sigma}) = \rho \mathbf{b}
$$

在 FVM 中，我们对空间中的每个控制体积（网格单元）对该方程进行积分。通过[散度定理](@entry_id:143110)，体积内的散度项被转换为通过单元边界的**通量**之和。这种离散化的核心优势在于，对于任意两个相邻的单元，从一个单元流出的通量精确地等于流入另一个单元的通量。这保证了离散动量在整个计算域内的**严格局部守恒**。这一性质对于任意形状的网格都成立，并且对于正确捕捉含有激波或接触间断的流动（即方程的[弱解](@entry_id:161732)）至关重要 。

对于上述守恒形式，通过单元面 $f$ 的动量通量矢量 $\mathbf{F}_f$ 可以表示为对流项和应力项之和。若面 $f$ 的面积矢量为 $\mathbf{S}_f$，则其离散形式为：

$$
\mathbf{F}_f = \underbrace{(\rho_f (\mathbf{v}_f \cdot \mathbf{S}_f)) \mathbf{v}_f}_{\text{对流通量}} - \underbrace{\boldsymbol{\sigma}_f \cdot \mathbf{S}_f}_{\text{应力（扩散）通量}}
$$

其中，下标 $f$ 表示在面上插值得到的物理量。第一项代表通过该面的质量流率乘以速度，即动量的对流输运；第二项代表作用在该面上的总面力 。

#### 弱形式与[有限元法 (FEM)](@entry_id:176633)

对于**有限元法 (Finite Element Method, FEM)**，我们通常从方程的**弱形式**或[变分形式](@entry_id:166033)出发。这是通过将[动量方程](@entry_id:197225)乘以一个**检验函数**（或称[虚位移](@entry_id:168781)/虚速度）$\mathbf{w}$，然后在整个计算域 $\Omega$ 上积分得到的。

对应力项 $\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \cdot \mathbf{w} \, dV$ 进行分部积分，可以将其转换为：

$$
\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \cdot \mathbf{w} \, dV = -\int_{\Omega} \boldsymbol{\sigma} : \nabla \mathbf{w} \, dV + \oint_{\partial\Omega} (\boldsymbol{\sigma} \cdot \mathbf{n}) \cdot \mathbf{w} \, dS
$$

体积积分项 $\int_{\Omega} \boldsymbol{\sigma} : \nabla \mathbf{w} \, dV$ 代表了应力在虚[速度梯度](@entry_id:261686)场上所做的**虚内功**。正如我们之前推导的，由于[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的对称性，我们有恒等式 $\boldsymbol{\sigma} : \nabla \mathbf{w} = \boldsymbol{\sigma} : \mathbf{D}(\mathbf{w})$ 。

这一关系在 FEM 中至关重要。它确保了离散系统在物理上是一致的，即[虚功](@entry_id:176403)仅由变形产生，而不会因刚性转动产生。对于许多[本构模型](@entry_id:174726)（如牛顿流体），这会使得最终离散系统产生的[刚度矩阵](@entry_id:178659)是对称的，从而极大地提高了[计算效率](@entry_id:270255)和稳定性。

此外，在[不可压缩流](@entry_id:140301)动的弱形式中，压力 $p$ 作为[拉格朗日乘子](@entry_id:142696)，与[检验函数](@entry_id:166589)速度场的散度 $\nabla \cdot \mathbf{w}$ 相乘出现，即 $\int_{\Omega} p (\nabla \cdot \mathbf{w}) \, dV$，从而在弱意义下强制施加了不可压缩约束 。