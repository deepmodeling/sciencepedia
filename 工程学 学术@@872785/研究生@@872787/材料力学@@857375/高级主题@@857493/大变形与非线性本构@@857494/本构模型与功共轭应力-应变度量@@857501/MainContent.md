## 引言
当材料承受的变形不再是微小时，传统的[线性弹性](@entry_id:166983)理论便宣告失效。精确描述和预测材料在拉伸、压缩、扭转等[大变形](@entry_id:167243)下的复杂力学行为，是现代工程与科学研究（从橡胶部件设计到生物组织模拟）面临的核心挑战。其关键在于建立能够捕捉几何与[材料非线性](@entry_id:162855)的**[本构模型](@entry_id:174726)**。然而，构建一个物理上合理且数学上严谨的大变形[本构模型](@entry_id:174726)，远非将小应变公式简单外推。它要求我们必须在一个统一的框架内，审慎地定义和区分多种应变与应力度量，并理解它们之间深刻的内在联系，其中**[功共轭](@entry_id:194957)**原理扮演着核心的桥梁角色。

本文旨在系统性地梳理这一关键领域。在第一章“原理与机制”中，我们将奠定[大变形](@entry_id:167243)[运动学](@entry_id:173318)和动力学的基础，并揭示[功共轭](@entry_id:194957)原理的本质。随后的第二章“应用与跨学科联系”将展示这些理论如何在计算力学、[有限应变塑性](@entry_id:185352)以及生物力学等前沿领域中发挥关键作用。最后，第三章“动手实践”提供了一系列精心设计的问题，旨在加深读者对核心概念的理解和应用能力。让我们首先从描述变形的语言——大变形运动学——开始，步入这个严谨而迷人的理论世界。

## 原理与机制

本章旨在系统性地阐述描述材料在[大变形](@entry_id:167243)下力学行为的本构模型的核心原理。我们将从变形的[运动学](@entry_id:173318)描述出发，引入各种应变和[应力张量](@entry_id:148973)，并在此基础上建立它们之间至关重要的**[功共轭](@entry_id:194957)**关系。最终，我们将探讨构建一个物理上和数学上均合理的本构模型所必须遵循的基本公理，例如物质标架无关性（客观性）和[材料对称性](@entry_id:190289)。

### [大变形](@entry_id:167243)运动学：[应变度量](@entry_id:755495)

为了精确描述一个连续体从其初始构型（或称**参考构型**）到当前构型（或称**空间构型**）的几何变化，我们需要超越在线性弹性理论中使用的微小应变假设。这一过程的核心是**变形梯度**张量。

#### 变形梯度

变形梯度张量 $\mathbf{F}$ 是[大变形](@entry_id:167243)运动学的基础。它将参考构型中一个无穷小向量 $d\mathbf{X}$ 映射到当前构型中对应的向量 $d\mathbf{x}$，即 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$。其分量形式定义为 $F_{iJ} = \partial x_i / \partial X_J$，其中 $x_i$ 是当前坐标，$X_J$ 是参考坐标。$\mathbf{F}$ 包含了关于局部变形（拉伸、剪切和[刚体转动](@entry_id:191086)）的全部信息。

#### 材料[应变度量](@entry_id:755495)（[拉格朗日描述](@entry_id:264498)）

为了只量化变形（即去除[刚体转动](@entry_id:191086)的影响），我们引入了基于参考构型的[应变度量](@entry_id:755495)。

首先是**[右柯西-格林张量](@entry_id:174156)**（Right Cauchy-Green Tensor），定义为 $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$。我们可以通过考察参考构型中两个向量 $d\mathbf{X}_1$ 和 $d\mathbf{X}_2$ 的[内积](@entry_id:158127)在变形前后的变化来理解其物理意义。变形后，它们的[内积](@entry_id:158127)变为 $d\mathbf{x}_1 \cdot d\mathbf{x}_2 = (\mathbf{F} d\mathbf{X}_1) \cdot (\mathbf{F} d\mathbf{X}_2) = d\mathbf{X}_1^{\mathsf{T}} \mathbf{F}^{\mathsf{T}} \mathbf{F} d\mathbf{X}_2 = d\mathbf{X}_1 \cdot (\mathbf{C} d\mathbf{X}_2)$。特别地，一个无穷小线段的长度平方的变化由 $\mathbf{C}$ 描述：$|d\mathbf{x}|^2 = d\mathbf{X} \cdot \mathbf{C} d\mathbf{X}$。因此，$\mathbf{C}$ 完全描述了物[质点](@entry_id:186768)邻域内的长度和角度变化，它是一个定义在参考构型上的[对称张量](@entry_id:148092)。

虽然 $\mathbf{C}$ 描述了变形，但对于无变形状态（即刚体运动），$\mathbf{F}$ 是一个正交张量，此时 $\mathbf{C} = \mathbf{I}$（单位张量）。为了使[应变度量](@entry_id:755495)在无变形时为零，我们定义了**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange Strain Tensor）：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I})
$$
这个张量是线性[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^{\mathsf{T}})$ 在有限变形框架下的直接推广。

例如，考虑一个沿 $X_1$ 轴的[单轴拉伸](@entry_id:188287)，其变形梯度为 $\mathbf{F} = \mathrm{diag}(\lambda, 1, 1)$, 其中 $\lambda$ 是主拉伸比 [@problem_id:2872369]。[右柯西-格林张量](@entry_id:174156)为：
$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \begin{pmatrix} \lambda  0  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix} \begin{pmatrix} \lambda  0  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix} = \begin{pmatrix} \lambda^2  0  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix}
$$
相应的[格林-拉格朗日应变](@entry_id:170427)为：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \begin{pmatrix} \frac{1}{2}(\lambda^2 - 1)  0  0 \\ 0  0  0 \\ 0  0  0 \end{pmatrix}
$$
可以看到，当变形微小时（即 $\lambda \approx 1$），$E_{11} = \frac{1}{2}(\lambda^2 - 1) = \frac{1}{2}(\lambda-1)(\lambda+1) \approx \lambda-1$，这恰好是工程应变的定义。

#### 空间[应变度量](@entry_id:755495)（[欧拉描述](@entry_id:264722)）

与材料描述相对应，我们也可以在当前构型中定义[应变度量](@entry_id:755495)。**[左柯西-格林张量](@entry_id:186163)**（Left Cauchy-Green Tensor），或称芬格张量（Finger tensor），定义为 $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}}$。它同样是 对称正定 的，并且与 $\mathbf{C}$ 有相同的[特征值](@entry_id:154894)，但定义在空间构型上。

相应的空间[应变度量](@entry_id:755495)是**[欧拉-阿尔曼西应变张量](@entry_id:194948)**（Euler-Almansi Strain Tensor），定义为：
$$
\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{B}^{-1})
$$
它测量的是相对于当前构型的应变。

考虑一个简单[剪切变形](@entry_id:170920)，其运动映射为 $\mathbf{x} = (X_1 + \gamma X_2, X_2, X_3)$ [@problem_id:2872332]。变形梯度和[左柯西-格林张量](@entry_id:186163)分别为：
$$
\mathbf{F} = \begin{pmatrix} 1  \gamma  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix}, \quad \mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}} = \begin{pmatrix} 1+\gamma^2  \gamma  0 \\ \gamma  1  0 \\ 0  0  1 \end{pmatrix}
$$
由此可计算出[欧拉-阿尔曼西应变张量](@entry_id:194948)为：
$$
\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{B}^{-1}) = \frac{1}{2}\begin{pmatrix} 0  \gamma  0 \\ \gamma  -\gamma^2  0 \\ 0  0  0 \end{pmatrix}
$$
注意，即使在简单剪切中，也会出现[法向应变](@entry_id:204633)分量 $e_{22}$，这是[大变形](@entry_id:167243)的典型[非线性](@entry_id:637147)效应。

#### 变形率

在处理黏塑性等速率相关材料或进行增量分析时，变形的[时间演化](@entry_id:153943)至关重要。**[空间速度梯度](@entry_id:187198)** $\mathbf{L}$ 定义为[速度场](@entry_id:271461) $\mathbf{v}(\mathbf{x}, t)$ 对当前空间坐标 $\mathbf{x}$ 的梯度，$\mathbf{L} = \nabla_{\mathbf{x}}\mathbf{v}$。通过[链式法则](@entry_id:190743)，可以推导出它与变形梯度率 $\dot{\mathbf{F}}$ 的重要关系 [@problem_id:2872368]：
$$
\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}
$$
与小应变理论类似，$\mathbf{L}$ 可以分解为对称[部分和](@entry_id:162077)反对称部分：
$$
\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}}), \quad \mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\mathsf{T}})
$$
其中，**变形率张量** $\mathbf{D}$ 描述了材料的拉伸和[剪切变形](@entry_id:170920)速率，而**[自旋张量](@entry_id:187346)** $\mathbf{W}$ 描述了材料点的刚性转动速率。对于简单剪切变形，以恒定剪切率 $\dot{\gamma}$ 进行，其[速度梯度](@entry_id:261686)、变形率和[自旋张量](@entry_id:187346)分别为 [@problem_id:2872368]：
$$
\mathbf{L} = \begin{pmatrix} 0  \dot{\gamma}  0 \\ 0  0  0 \\ 0  0  0 \end{pmatrix}, \quad \mathbf{D} = \begin{pmatrix} 0  \frac{\dot{\gamma}}{2}  0 \\ \frac{\dot{\gamma}}{2}  0  0 \\ 0  0  0 \end{pmatrix}, \quad \mathbf{W} = \begin{pmatrix} 0  \frac{\dot{\gamma}}{2}  0 \\ -\frac{\dot{\gamma}}{2}  0  0 \\ 0  0  0 \end{pmatrix}
$$
变形率张量 $\mathbf{D}$ 的[不变量](@entry_id:148850)，例如其偏量部分的第二[不变量](@entry_id:148850) $J_2 = \frac{1}{2}\mathbf{D}':\mathbf{D}'$，在塑性理论中扮演着核心角色，常用于定义屈服准则。

### [大变形](@entry_id:167243)动力学：应力度量

在有限变形中，由于面积元和[法向量](@entry_id:264185)都会随着变形而改变，单一的应力度量（如[小变形理论](@entry_id:174991)中的[应力张量](@entry_id:148973)）已不足够。我们需要引入多种应力度量，它们分别服务于不同的物理和数学目的。

#### 柯西应力（Cauchy Stress）

**柯西应力张量** $\boldsymbol{\sigma}$ 是最符合物理直觉的应力度量，常被称为“真实应力”。它定义在**当前构型**上，描述了当前变形体内部单位面积上所受的力。根据柯西定理，作用在[法向量](@entry_id:264185)为 $\mathbf{n}$ 的[截面](@entry_id:154995)上的应力矢量 $\mathbf{t}$ 为 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$。在没有[体力](@entry_id:174230)偶和面力偶的情况下，[角动量守恒](@entry_id:156798)要求柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$ [@problem_id:2872377]。由于柯西应力定义在不断变化的当前构型上，直接用它来建立本构关系（即应力与应变历史的关系）会很复杂。

#### 名义应力与拉格朗日应力

为了方便[本构方程](@entry_id:138559)的建立，我们通常希望将应力与定义在固定参考构型上的[应变度量](@entry_id:755495)联系起来。这催生了拉格朗日应力度量。

**[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量**（First Piola-Kirchhoff Stress, PK1），记作 $\mathbf{P}$，是一个“两点张量”。它将参考构型中的名义面力（作用在当前构型上的力）与参考构型中的[面积元](@entry_id:263205)联系起来。具体而言，$\mathbf{t}_R = \mathbf{P}\mathbf{N}$，其中 $\mathbf{N}$ 是参考构型中的[单位法向量](@entry_id:178851)，$\mathbf{t}_R$ 是单位参考面积上的力。$\mathbf{P}$ 与 $\boldsymbol{\sigma}$ 的关系可以通过力的等效性以及[Nanson公式](@entry_id:195566)（联系变形前后面积元的公式）推导得出 [@problem_id:2872377]：
$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}}
$$
其中 $J = \det(\mathbf{F})$ 是变形梯度的[雅可比行列式](@entry_id:137120)。一个重要的特性是，即使 $\boldsymbol{\sigma}$ 是对称的，$\mathbf{P}$ 通常也**不对称**。

为了获得一个完全定义在参考构型上且对称的应力度量，我们引入了**[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量**（Second Piola-Kirchhoff Stress, PK2），记作 $\mathbf{S}$。它通过将 $\mathbf{P}$ [拉回](@entry_id:160816)到参考构型得到：
$$
\mathbf{S} = \mathbf{F}^{-1}\mathbf{P} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}}
$$
可以证明，如果 $\boldsymbol{\sigma}$ 是对称的，那么 $\mathbf{S}$ 也必然是**对称的**。$\mathbf{S}$ 缺乏直接的物理图像，但它在数学上极为便利，因为它与同样定义在参考构型上的[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 形成了优美的共轭关系。

#### [基尔霍夫应力](@entry_id:751039)（Kirchhoff Stress）

**[基尔霍夫应力](@entry_id:751039)张量** $\boldsymbol{\tau}$ 是柯西应力的一个加权版本，定义为 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$。它仍然是一个[空间张量](@entry_id:185799)，其主要用途在于简化功率表达式中的体积积分转换。从当前[体积元](@entry_id:267802) $dv$ 到参考[体积元](@entry_id:267802) $dV_0$ 的转换关系是 $dv = J dV_0$。因此，$\int_{\Omega_t} \boldsymbol{\sigma}:\mathbf{D} \, dv = \int_{\Omega_0} J\boldsymbol{\sigma}:\mathbf{D} \, dV_0 = \int_{\Omega_0} \boldsymbol{\tau}:\mathbf{D} \, dV_0$ [@problem_id:2872377]。

这些应力度量之间可以通过推拉操作（push-forward and pull-back）相互转换。例如，从 $\mathbf{S}$ 恢复“真实”的柯西应力 $\boldsymbol{\sigma}$ 的关系为 $\boldsymbol{\sigma} = J^{-1}\mathbf{F}\mathbf{S}\mathbf{F}^{\mathsf{T}}$。

### [功共轭](@entry_id:194957)原理

[功共轭](@entry_id:194957)原理是连接[运动学](@entry_id:173318)（应变）和动力学（应力）的桥梁，也是建立[热力学一致的](@entry_id:755906)本构模型的基础。其核心思想是，[应力张量](@entry_id:148973)和某个[应变率张量](@entry_id:266108)的[双点积](@entry_id:748648)应该等于单位体积的[功率密度](@entry_id:194407)。

#### [应力功率](@entry_id:182907)与[功共轭](@entry_id:194957)对

单位**当前体积**的内[功率密度](@entry_id:194407)（或称[应力功率](@entry_id:182907)）由柯西应力 $\boldsymbol{\sigma}$ 和变形率张量 $\mathbf{D}$ 给出：
$$
\dot{w}_v = \boldsymbol{\sigma} : \mathbf{D}
$$
由于 $\boldsymbol{\sigma}$ 是对称的而[自旋张量](@entry_id:187346) $\mathbf{W}$ 是反对称的，它们的[双点积](@entry_id:748648)恒为零，$\boldsymbol{\sigma} : \mathbf{W} = 0$。这意味着材料的刚性转动不消耗能量，功率完全由变形率贡献 [@problem_id:2872340]。因此，$(\boldsymbol{\sigma}, \mathbf{D})$ 构成一个定义在当前构型上的**[功共轭](@entry_id:194957)对**。

为了方便与材料[本构定律](@entry_id:178936)（通常在参考构型中定义）结合，我们更关心单位**参考体积**的[功率密度](@entry_id:194407) $\dot{w}_0$。通过体积元关系 $dv=J dV_0$，我们有 $\dot{w}_0 = J\dot{w}_v = J\boldsymbol{\sigma}:\mathbf{D}$。利用前面介绍的各种应力和[应变度量](@entry_id:755495)，我们可以推导出几组重要的[功共轭](@entry_id:194957)关系 [@problem_id:2872340] [@problem_id:2872369] [@problem_id:2872377]：
$$
\dot{w}_0 = \boldsymbol{\tau} : \mathbf{D} = \mathbf{P} : \dot{\mathbf{F}} = \mathbf{S} : \dot{\mathbf{E}}
$$
这些等式表明：
- **[基尔霍夫应力](@entry_id:751039)** $\boldsymbol{\tau}$ 与**变形率张量** $\mathbf{D}$ 是[功共轭](@entry_id:194957)的。
- **第一PK应力** $\mathbf{P}$ 与**变形梯度率** $\dot{\mathbf{F}}$ 是[功共轭](@entry_id:194957)的。
- **第二PK应力** $\mathbf{S}$ 与**[格林-拉格朗日应变](@entry_id:170427)率** $\dot{\mathbf{E}}$ 是[功共轭](@entry_id:194957)的。

$(\mathbf{S}, \mathbf{E})$ 这对组合尤为重要，因为两者都是对称的、纯粹的拉格朗日量，非常适合用于发展[超弹性](@entry_id:159356)等材料模型。

#### 应用：[超弹性](@entry_id:159356)与[路径无关性](@entry_id:163750)

[功共轭](@entry_id:194957)原理在**超弹性**（hyperelasticity）理论中得到完美体现。[超弹性材料](@entry_id:190241)被定义为存在一个**[应变能密度函数](@entry_id:755490)** $\Psi$ 的弹性材料，该函数仅是应变状态的函数，例如 $\Psi = \Psi(\mathbf{E})$。根据[能量守恒](@entry_id:140514)，应变能的增加率必须等于[应力功率](@entry_id:182907)：
$$
\dot{\Psi} = \dot{w}_0
$$
利用链式法则，$\dot{\Psi} = \frac{\partial\Psi}{\partial\mathbf{E}} : \dot{\mathbf{E}}$。与[功共轭](@entry_id:194957)关系 $\dot{w}_0 = \mathbf{S}:\dot{\mathbf{E}}$ 比较，我们立即得到[超弹性材料](@entry_id:190241)的[本构方程](@entry_id:138559) [@problem_id:2872345]：
$$
\mathbf{S} = \frac{\partial\Psi}{\partial\mathbf{E}}
$$
这意味着，一旦[应变能函数](@entry_id:178435) $\Psi(\mathbf{E})$ 确定，[应力-应变关系](@entry_id:274093)就完全确定了。

从状态 $\mathbf{E}_1$ 到 $\mathbf{E}_2$ 的应变能变化量是 $\Delta \Psi = \int_{t_1}^{t_2} \dot{w}_0 \, dt = \int_{\mathbf{E}_1}^{\mathbf{E}_2} \mathbf{S} : d\mathbf{E}$。对于[超弹性材料](@entry_id:190241)，这变为 $\int_{\mathbf{E}_1}^{\mathbf{E}_2} d\Psi = \Psi(\mathbf{E}_2) - \Psi(\mathbf{E}_1)$。这是一个[全微分](@entry_id:171747)的积分，其值仅取决于起点和终点，而与连接它们的应变路径无关。因此，对于[超弹性材料](@entry_id:190241)，做功和储存的能量是**路径无关的** [@problem_id:2872345]。

我们可以通过一个具体的计算来感受[应力功率](@entry_id:182907)的量级。假设某材料点的状态为 [@problem_id:2872345]：
$$
\mathbf{S} = \begin{pmatrix} 120  15  -10 \\ 15  80  5 \\ -10  5  60 \end{pmatrix} \text{MPa}, \quad \dot{\mathbf{E}} = \begin{pmatrix} 1.5  -0.2  0.3 \\ -0.2  1.0  -0.15 \\ 0.3  -0.15  0.8 \end{pmatrix} \times 10^{-3} \text{ s}^{-1}
$$
单位参考体积的[功率密度](@entry_id:194407)为 $\dot{w}_0 = \mathbf{S}:\dot{\mathbf{E}} = \sum_{I,J} S_{IJ}\dot{E}_{IJ} \approx 2.945 \times 10^5 \text{ W/m}^3$。

### 本构模型的基本公理

为了确保[本构模型](@entry_id:174726)在物理上是现实的、在数学上是良定的，它必须遵循一系列基本公理。

#### 物质标架无关性（客观性）

**物质标架无关性**（Material Frame Indifference），或称**客观性**（Objectivity），是一条普适的物理原理。它要求材料的[本构定律](@entry_id:178936)（即材料的内在属性）不能依赖于观察者。观察者的变换在数学上表现为在当前构型上叠加一个[刚体运动](@entry_id:193355) $\mathbf{x}^* = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}$，其中 $\mathbf{Q}(t)$ 是一个时间相关的[旋转张量](@entry_id:191990)。

在此变换下，变形梯度变为 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$。客观性要求[应变能函数](@entry_id:178435)对于任意旋转 $\mathbf{Q}$ 都不变，即 [@problem_id:2872375]：
$$
\Psi(\mathbf{F}) = \Psi(\mathbf{Q}\mathbf{F})
$$
这一要求极大地限制了 $\Psi$ 的函数形式。可以证明，要满足此条件，$\Psi$ 必须只能通过[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 来依赖于 $\mathbf{F}$，因为 $\mathbf{C}^* = (\mathbf{Q}\mathbf{F})^{\mathsf{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{C}$，它对叠加的旋转是天然免疫的。因此，所有客观的[应变能函数](@entry_id:178435)都必须可以写成 $\Psi = \hat{\Psi}(\mathbf{C})$ 或等价地 $\Psi = \tilde{\Psi}(\mathbf{E})$ 的形式。

一个直接依赖于 $\mathbf{F}$ 的函数通常会违反客观性。例如，考虑一个假设的能量函数 $\Psi(\mathbf{F}) = \mu(\operatorname{tr}\mathbf{F})^2$ [@problem_id:2872366]。在未变形状态 $\mathbf{F}=\mathbf{I}$ 下，$\Psi(\mathbf{I})=9\mu$。施加一个绕 $z$ 轴旋转 $\theta$ 的变换后，$\mathbf{F}'=\mathbf{Q}(\theta)\mathbf{I}=\mathbf{Q}(\theta)$。此时，$\Psi(\mathbf{F}') = \mu(\operatorname{tr}\mathbf{Q})^2 = \mu(2\cos\theta+1)^2$。显然，当 $\theta \neq 0$ 时，$\Psi(\mathbf{F}') \neq \Psi(\mathbf{F})$。因此，该模型不具备客观性，物理上是不可接受的。

#### [材料对称性](@entry_id:190289)

与客观性不同，**[材料对称性](@entry_id:190289)**（Material Symmetry）不是普适原理，而是描述特定材料内部微观结构对称性的属性。它体现在，对**参考构型**进行某些特定的旋转（或反射）后，材料的力学响应保持不变。这些变换构成了材料的[对称群](@entry_id:146083) $G$。

如果 $\mathbf{R}$ 是一个属于 $G$ 的对称性变换，那么本构关系必须满足：
$$
\hat{\Psi}(\mathbf{C}) = \hat{\Psi}(\mathbf{R}^{\mathsf{T}}\mathbf{C}\mathbf{R}) \quad \text{for all } \mathbf{R} \in G
$$
- 如果材料是**各向同性**的（Isotropic），那么 $G$ 包含所有旋转，即 $G = SO(3)$。此时，$\Psi$ 必须是 $\mathbf{C}$ 的[主不变量](@entry_id:193522)的函数，即 $\Psi = \Psi(I_1, I_2, I_3)$，其中 $I_1=\operatorname{tr}(\mathbf{C}), I_2=\frac{1}{2}[(\operatorname{tr}\mathbf{C})^2 - \operatorname{tr}(\mathbf{C}^2)], I_3=\det(\mathbf{C})$。
- 如果材料是**各向异性**的（Anisotropic），例如**[正交各向异性](@entry_id:196967)**（Orthotropic），其对称群只包含绕三个相互正交的材料轴旋转 $\pi$ 的变换。此时，$\Psi$ 除了依赖于[主不变量](@entry_id:193522)，还必须依赖于与材料方向相关的伪[不变量](@entry_id:148850)。例如，一个典型的[正交各向异性](@entry_id:196967)能量函数可以写成 [@problem_id:2872375]：
$$
\Psi(\mathbf{C}) = \Psi_{\text{iso}}(I_1, I_2, I_3) + \sum_{i=1}^3 \Psi_{\text{aniso}}^i(I_4^i, I_5^i, \dots)
$$
其中 $I_4^i = \mathbf{a}_i \cdot \mathbf{C}\mathbf{a}_i$ 等伪[不变量](@entry_id:148850)描述了沿材料轴 $\mathbf{a}_i$ 的变形。

#### 高级[功共轭](@entry_id:194957)对与[材料稳定性](@entry_id:183933)

[功共轭](@entry_id:194957)的概念可以进一步扩展。例如，通过对变形梯度进行**极分解** $\mathbf{F} = \mathbf{R}\mathbf{U}$，其中 $\mathbf{R}$ 是[旋转张量](@entry_id:191990)，$\mathbf{U}$ 是对称的右[拉伸张量](@entry_id:193200)，我们可以寻找与拉伸率 $\dot{\mathbf{U}}$ [功共轭](@entry_id:194957)的应力度量。可以证明，这个应力度量是第二PK应力 $\mathbf{S}$ 和右[拉伸张量](@entry_id:193200) $\mathbf{U}$ 的对称化乘积，即 $\mathbf{T}_U = \frac{1}{2}(\mathbf{U}\mathbf{S} + \mathbf{S}\mathbf{U})$ [@problem_id:2872312]。

最后，为了保证材料的稳定性（例如，受压时不会自发膨胀），[应变能函数](@entry_id:178435) $\Psi$ 必须满足一定的数学[凸性](@entry_id:138568)条件。简单的[凸性](@entry_id:138568) $W(\mathbf{F})$ 是一个过强的要求，它会排除许多物理上合理的材料行为。在现代[非线性弹性](@entry_id:185743)理论中，引入了更弱的[凸性](@entry_id:138568)概念 [@problem_id:2872359]：
- **[秩一凸性](@entry_id:191019)** (Rank-one convexity)：要求 $\Psi$ 在任意秩一方向上是凸的。这是保证[偏微分方程](@entry_id:141332)椭圆性的必要条件。
- **拟凸性** (Quasiconvexity)：这是一个与变分法相关的[积分不等式](@entry_id:139182)条件，对于确保能量泛函存在最小值至关重要。
- **[多凸性](@entry_id:185154)** (Polyconvexity)：这是一个更强的、更易于验证的条件。如果存在一个凸函数 $G$，使得 $\Psi(\mathbf{F}) = G(\mathbf{F}, \operatorname{cof}\mathbf{F}, \det\mathbf{F})$，则称 $\Psi$ 是多凸的。$\operatorname{cof}\mathbf{F}$ 是 $\mathbf{F}$ 的余子式矩阵。

这些凸性条件之间存在如下蕴含关系：
$$
\text{凸性} \implies \text{多凸性} \implies \text{拟凸性} \implies \text{秩一凸性}
$$
[多凸性](@entry_id:185154)为我们提供了一种构造数学上“行为良好”的[应变能函数](@entry_id:178435)的实用方法。例如，形如 $W(\mathbf{F}) = \alpha \lVert \mathbf{F} \rVert^{2} + \beta \lVert \operatorname{cof} \mathbf{F} \rVert^{2} + g(\det \mathbf{F})$ 的函数，如果 $g$ 是一个凸函数，那么 $W$ 就是一个多[凸函数](@entry_id:143075) [@problem_id:2872359]。这类函数形式在[计算力学](@entry_id:174464)中被广泛应用。