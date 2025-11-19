## 引言
在计算岩[土力学](@entry_id:180264)领域，准确预测滑坡、地基失稳、[地震液化](@entry_id:748774)等涉及[大变形](@entry_id:167243)和复杂加载路径的现象，是工程实践与科学研究面临的核心挑战。当材料经历显著的位移和转动时，基于小应变理论的传统分析方法便显得力不从心。问题的关键在于，我们必须从关注静态的“位移”转向描述动态的“运动速率”。这便将我们引向了[连续介质运动学](@entry_id:747813)分析的核心——[速度梯度张量](@entry_id:270928)及其分解。

本文旨在系统地阐释描述连续体瞬时运动的两个基本量：**应变率张量** (rate-of-deformation tensor) 与**[自旋张量](@entry_id:187346)** (spin tensor)。这两个张量分别捕捉了材料单元最本质的两种运动模式：形状与体积的改变（变形）以及[刚体转动](@entry_id:191086)。理解它们不仅是掌握[大变形理论](@entry_id:188422)的基石，更是构建能够在极端条件下保持物理真实性的高等本构模型的关键。本文将填补从基础理论到高级应用的知识鸿沟，帮助读者深入理解为何简单的[刚体转动](@entry_id:191086)会对[数值模拟](@entry_id:137087)的准确性产生致命影响，以及如何通过正确的[运动学分解](@entry_id:751020)来克服这一挑战。

在接下来的内容中，我们将分三个章节展开探讨：
- **原理与机制**：我们将从[速度梯度张量](@entry_id:270928)的定义出发，详细阐述其如何分解为[应变率张量](@entry_id:266108)和[自旋张量](@entry_id:187346)，并深入探讨它们的物理意义、[客观性原理](@entry_id:185412)，以及为何必须引入[客观应力率](@entry_id:199282)来构建正确的[本构关系](@entry_id:186508)。
- **应用与交叉学科联系**：本章将展示这些理论概念在实践中的强大威力，内容涵盖它们在岩土[弹塑性](@entry_id:193198)[本构模型](@entry_id:174726)构建、非共轴性现象解释、[多尺度模拟](@entry_id:752335)（离散元-连续介质耦合）以及与[流体力学](@entry_id:136788)、[地震工程](@entry_id:748777)等多物理场耦合中的具体应用。
- **动手实践**：通过一系列精心设计的计算练习，读者将有机会亲手计算这些张量，并在编程中实现[客观应力率](@entry_id:199282)，从而将抽象的理论知识转化为坚实的计算技能。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，理解物体的运动和变形需要精确的数学描述。当变形很大时，仅仅追踪位移已不足够，我们必须转而关注变形的“速率”。本章深入探讨描述连续体瞬时运动的两个核心[运动学](@entry_id:173318)量：**[应变率张量](@entry_id:266108)**（rate-of-deformation tensor）和**[自旋张量](@entry_id:187346)**（spin tensor）。这两个张量源于对[速度场](@entry_id:271461)的局部梯度分解，前者捕捉了材料单元的拉伸和剪切（形状与体积的变化率），后者则描述了其刚性转动。我们将从基本定义出发，揭示它们的物理意义，并阐明它们在建立适用于大变形[地质力学](@entry_id:175967)问题的客观[本构模型](@entry_id:174726)中的关键作用。

### [速度梯度张量](@entry_id:270928)：速率[运动学](@entry_id:173318)的基础

在[欧拉描述](@entry_id:264722)（Eulerian description）中，我们关注空间中[固定点](@entry_id:156394) `$\mathbf{x}$` 的物理量随时间 `t` 的变化。连续体的运动由定义在当前构型上的**速度场** `$\mathbf{v}(\mathbf{x}, t)$` 描述。为了理解一个物[质点](@entry_id:186768)邻域内的相对运动，我们考察速度场在空间中的变化率，这由**[速度梯度张量](@entry_id:270928)** `$\mathbf{L}$` 来量化，其定义为速度 `$\mathbf{v}$` 对空间坐标 `$\mathbf{x}$` 的梯度：

$$
\mathbf{L} = \nabla_{\mathbf{x}} \mathbf{v}
$$

在[笛卡尔坐标系](@entry_id:169789)中，其分量形式为 $L_{ij} = \frac{\partial v_i}{\partial x_j}$。`$\mathbf{L}$` 完整地描述了某一点附近速度场的线性部分，从而捕捉了该点邻域内材料的瞬时运动，包括拉伸、压缩、剪切和旋转。[@problem_id:3564004]

[速度梯度张量](@entry_id:270928) `$\mathbf{L}$` 是一个纯粹的欧拉量，它与描述从参考构型到当前构型映射的**变形梯度张量** `$\mathbf{F}$` 密切相关。通过链式法则可以证明，`$\mathbf{L}$` 是 `$\mathbf{F}$` 的[物质时间导数](@entry_id:190892) `$\dot{\mathbf{F}}$` 映射回当前构型的结果：

$$
\mathbf{L} = \dot{\mathbf{F}} \mathbf{F}^{-1}
$$

这个关系式是连接[拉格朗日描述](@entry_id:264498)（Lagrangian description）和[欧拉描述](@entry_id:264722)的桥梁，凸显了 `$\mathbf{L}$` 作为变形“速率”度量的核心地位。[@problem_id:3564004]

### 运动的分解：拉伸与自旋

[速度梯度张量](@entry_id:270928) `$\mathbf{L}$` 本身包含了两种截然不同的运动模式：材料单元的变形（形状和尺寸的改变）和刚性转动。为了将这两种效應分离开来，我们可以将任何二阶张量 `$\mathbf{L}$`唯一地分解为其对称部分和反对稱部分。

$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$

**[应变率张量](@entry_id:266108)** `$\mathbf{D}$` 是 `$\mathbf{L}$` 的对称部分，定义为：

$$
\mathbf{D} = \frac{1}{2} (\mathbf{L} + \mathbf{L}^{\mathsf{T}})
$$

`$\mathbf{D}$` 量化了材料单元的瞬时拉伸和剪切变形速率，因此又称为**变形率张量**或**[拉伸张量](@entry_id:193200)**。

**[自旋张量](@entry_id:187346)** `$\mathbf{W}$` 是 `$\mathbf{L}$` 的反对稱部分（或称斜对称部分），定义为：

$$
\mathbf{W} = \frac{1}{2} (\mathbf{L} - \mathbf{L}^{\mathsf{T}})
$$

`$\mathbf{W}$` 描述了材料单元作为一个刚体的瞬时转动速率，因此也常被称为**[涡量张量](@entry_id:189621)**。[@problem_id:3564004]

为了具体理解这种分解，我们考虑一个经典的**简单[剪切流](@entry_id:266817)**（simple shear flow）。假设一个[二维流](@entry_id:266853)动的[速度场](@entry_id:271461)为 `$\mathbf{v} = (\dot{\gamma}y, 0)$`，其中 `$\dot{\gamma}$` 是一个常数剪切率。[@problem_id:3563994] [@problem_id:3564004] [速度梯度张量](@entry_id:270928) `$\mathbf{L}$` 为：

$$
\mathbf{L} = \begin{pmatrix} 0 & \dot{\gamma} \\ 0 & 0 \end{pmatrix}
$$

将其分解，我们得到：

$$
\mathbf{D} = \frac{1}{2} \left( \begin{pmatrix} 0 & \dot{\gamma} \\ 0 & 0 \end{pmatrix} + \begin{pmatrix} 0 & 0 \\ \dot{\gamma} & 0 \end{pmatrix} \right) = \begin{pmatrix} 0 & \dot{\gamma}/2 \\ \dot{\gamma}/2 & 0 \end{pmatrix}
$$

$$
\mathbf{W} = \frac{1}{2} \left( \begin{pmatrix} 0 & \dot{\gamma} \\ 0 & 0 \end{pmatrix} - \begin{pmatrix} 0 & 0 \\ \dot{\gamma} & 0 \end{pmatrix} \right) = \begin{pmatrix} 0 & \dot{\gamma}/2 \\ -\dot{\gamma}/2 & 0 \end{pmatrix}
$$

这个结果表明，简单剪切运动同时包含纯粹的[剪切变形](@entry_id:170920)（由 `$\mathbf{D}$` 描述）和刚性转动（由 `$\mathbf{W}$` 描述）。我们可以使用张量的[弗罗贝尼乌斯范数](@entry_id:143384) $||\cdot||_F$ 来量化这两种运动的“强度”。由于[对称张量](@entry_id:148092)和反对稱张量在该范数下是正交的，我们有 $||\mathbf{L}||_F^2 = ||\mathbf{D}||_F^2 + ||\mathbf{W}||_F^2$。对于上述简单[剪切流](@entry_id:266817)：

$||\mathbf{L}||_F^2 = \dot{\gamma}^2$

$||\mathbf{D}||_F^2 = (\dot{\gamma}/2)^2 + (\dot{\gamma}/2)^2 = \dot{\gamma}^2/2$

$||\mathbf{W}||_F^2 = (\dot{\gamma}/2)^2 + (-\dot{\gamma}/2)^2 = \dot{\gamma}^2/2$

变形部分所占的能量（范数平方）比例为 $||\mathbf{D}||_F^2 / ||\mathbf{L}||_F^2 = 1/2$。这意味着在简单剪切中，由[速度梯度](@entry_id:261686)所描述的运动“能量”恰好一半用于变形，另一半用于旋转。[@problem_id:3563994]

### [运动学](@entry_id:173318)张量的物理解释

`$\mathbf{D}$` 和 `$\mathbf{W}$` 张量各自拥有深刻的物理含义，是连接[运动学](@entry_id:173318)和材料本构响应的桥梁。

#### 应变率张量 `$\mathbf{D}$` 的物理意义

`$\mathbf{D}$` 直接描述了材料的变形速率。

**[体积应变率](@entry_id:272471)**：`$\mathbf{D}$` 的迹 `$\mathrm{tr}(\mathbf{D})$` 表示材料单元的体积变化率，即**[体积应变率](@entry_id:272471)** `$\dot{\epsilon}_v$`。可以证明，`$\mathrm{tr}(\mathbf{D})$` 等于速度场的散度 `$\nabla \cdot \mathbf{v}$`。[@problem_id:3564025]
*   若 `$\mathrm{tr}(\mathbf{D}) > 0$`，材料发生膨胀（[扩容](@entry_id:201001)）。
*   若 `$\mathrm{tr}(\mathbf{D})  0$`，材料发生压缩（剪缩）。
*   若 `$\mathrm{tr}(\mathbf{D}) = 0$`，运动是**不可压缩的**（isochoric），即变形过程中[体积保持](@entry_id:141001)不变。

考虑一个纯[拉伸流](@entry_id:198535)，其[速度场](@entry_id:271461)为 `$\mathbf{v} = (\dot{\epsilon}_x x, \dot{\epsilon}_y y, \dot{\epsilon}_z z)$`，其中 `$\dot{\epsilon}_i$` 是沿各坐标轴的[应变率](@entry_id:154778)常数。计算可得：

$$
\mathbf{L} = \mathbf{D} = \begin{pmatrix} \dot{\epsilon}_x  0  0 \\ 0  \dot{\epsilon}_y  0 \\ 0  0  \dot{\epsilon}_z \end{pmatrix}, \quad \mathbf{W} = \mathbf{0}
$$

这种运动是无旋的（irrotational），所有的运动都表现为拉伸。其[体积应变率](@entry_id:272471)为 `$\mathrm{tr}(\mathbf{D}) = \dot{\epsilon}_x + \dot{\epsilon}_y + \dot{\epsilon}_z$`。因此，该流动不可壓縮的条件是 `$\dot{\epsilon}_x + \dot{\epsilon}_y + \dot{\epsilon}_z = 0$`。[@problem_id:3564025]

**[主应变率](@entry_id:264248)**：作为一个[对称张量](@entry_id:148092)，`$\mathbf{D}$` 拥有一组实[特征值](@entry_id:154894)和对应的[正交特征向量](@entry_id:155522)。这些[特征值](@entry_id:154894)被称为**[主应变率](@entry_id:264248)**（`$\dot{\epsilon}_1, \dot{\epsilon}_2, \dot{\epsilon}_3$`），它们表示材料在三个相互垂直的主方向上伸长或缩短的最快速率。在这些主方向上，[剪切应变率](@entry_id:276945)为零。[主应变率](@entry_id:264248)的和等于[张量的迹](@entry_id:190669)，即[体积应变率](@entry_id:272471)：

$$
\dot{\epsilon}_v = \mathrm{tr}(\mathbf{D}) = \dot{\epsilon}_1 + \dot{\epsilon}_2 + \dot{\epsilon}_3
$$

这个关系式至关重要。它表明，体积的变化是由所有[主方向](@entry_id:276187)上的拉伸/压缩共同决定的。一个运动是否导致体积变化，取决于[主应变率](@entry_id:264248)的代数和，而非其中任何一个。例如，即使最大的[主应变率](@entry_id:264248)为正（拉伸），但如果被足够大的负[主应变率](@entry_id:264248)（压缩）所抵消，总体积仍然可能减小。反之，不可压缩运动（`$\dot{\epsilon}_v=0$`）并不意味着所有[主应变率](@entry_id:264248)都为零，而仅表示它们的和为零。这种情况下，变形是纯粹的形状改变，即**畸变**（distortion）。[@problem_id:3564039]

#### [自旋张量](@entry_id:187346) `$\mathbf{W}$` 的物理意义

`$\mathbf{W}$` 描述了材料点的局部刚性转动。这个概念与[流体力学](@entry_id:136788)中的**[涡量](@entry_id:142747)**（vorticity）密切相关。[涡量矢量](@entry_id:187667) `$\boldsymbol{\omega}_{\text{vec}}$` 定义为[速度场的旋度](@entry_id:183606) `$\nabla \times \mathbf{v}$`。可以证明，[自旋张量](@entry_id:187346) `$\mathbf{W}$` 与[涡量矢量](@entry_id:187667) `$\boldsymbol{\omega}_{\text{vec}}$` 是等价的，它们之间通过轴矢映射（axial vector mapping）相关联。例如，对于[二维流](@entry_id:266853)动 `$\mathbf{v}=(v_x(x,y), v_y(x,y))$`，其涡量是一个标量 `$\omega_z = \frac{\partial v_y}{\partial x} - \frac{\partial v_x}{\partial y}$`。对应的[自旋张量](@entry_id:187346)为：

$$
\mathbf{W} = \begin{pmatrix} 0  -\omega_z/2 \\ \omega_z/2  0 \end{pmatrix}
$$

这表明 `$\mathbf{W}$` 的分量直接反映了材料单元的平均转动角速度。对于一个速度场 `$\mathbf{v} = (0, \Omega x)$`，计算可得 `$\mathbf{L} = \begin{pmatrix} 0  0 \\ \Omega  0 \end{pmatrix}$`，`$\mathbf{W} = \begin{pmatrix} 0  -\Omega/2 \\ \Omega/2  0 \end{pmatrix}$`，而其[涡量](@entry_id:142747) `$\omega_z = \Omega$`。两者通过 `$\omega_z/2 = \Omega/2$` 的关系完全一致。[@problem_id:3563998]

### [客观性原理](@entry_id:185412)及其影响

在建立描述材料行为的[本构关系](@entry_id:186508)时，一个基本物理原则是**物质[坐标系](@entry_id:156346)无关性**（material frame indifference），或称**[客观性原理](@entry_id:185412)**（principle of objectivity）。该原理指出，[本构方程](@entry_id:138559)（即[应力与应变](@entry_id:137374)或应变率之间的关系）必须独立于观察者的刚体运动。换句话说，材料的响应只应取决于其自身的变形，而不应取决于我们从哪个旋转或平移的[参考系](@entry_id:169232)去观察它。

应用这个原理，我们可以检验各种[运动学](@entry_id:173318)张量的客观性。一个[二阶张量](@entry_id:199780) `$\mathbf{A}$` 被认为是客观的，如果在一个叠加了[刚体转动](@entry_id:191086) `$\mathbf{Q}(t)$` 的[坐标系](@entry_id:156346)中，它变换为 `$\mathbf{A}^* = \mathbf{Q} \mathbf{A} \mathbf{Q}^{\mathsf{T}}$`。通过严格的推导可以证明：[@problem_id:3564004]

*   **应变率张量** `$\mathbf{D}$` 是**客观的**。
*   **[速度梯度张量](@entry_id:270928)** `$\mathbf{L}$` 是**非客观的**。
*   **[自旋张量](@entry_id:187346)** `$\mathbf{W}$` 是**非客观的**。

`$\mathbf{D}$` 的客观性是其成为[本构模型](@entry_id:174726)核心变量的根本原因。材料的应力响应理应由其真实的变形速率 `$\mathbf{D}$` 决定。

`$\mathbf{L}$` 和 `$\mathbf{W}$` 的非客观性则带来了深刻的挑战。尤其是，它导致了柯西应力张量 `$\boldsymbol{\sigma}$` 的[物质时间导数](@entry_id:190892) `$\dot{\boldsymbol{\sigma}}$` 也是非客观的。在一个纯刚性转动（`$\mathbf{D}=\mathbf{0}$`）下，一个受应力的物体其应力状态并未改变，但从一个固定的空间[坐标系](@entry_id:156346)看，其应力张量的分量会因为旋转而变化，导致 `$\dot{\boldsymbol{\sigma}} \neq \mathbf{0}$`。具体来说，`$\dot{\boldsymbol{\sigma}} = \mathbf{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{W}$`。[@problem_id:3564036]

如果在 本构关系 中错误地使用非客观的 `$\dot{\boldsymbol{\sigma}}$`，例如写成 `$\dot{\boldsymbol{\sigma}} = f(\mathbf{D}, \boldsymbol{\sigma})$`，就会导致灾难性的后果。在纯刚体旋转下（`$\mathbf{D}=\mathbf{0}$`），这个错误的模型会预测 `$\dot{\boldsymbol{\sigma}}=\mathbf{0}$`，意味着应力张量在空间[坐标系](@entry_id:156346)中保持不变。然而，物体本身在旋转，这意味着在与物体固连的材料[坐标系](@entry_id:156346)中，应力状态会发生虚假的变化，凭空产生或消失应力。这严重违反了物理现实。[@problem_id:3563996]

为了解决这个问题，我们必须使用**[客观应力率](@entry_id:199282)**。一个[客观应力率](@entry_id:199282)通过从 `$\dot{\boldsymbol{\sigma}}$` 中移除由自旋 `$\mathbf{W}$` 引起的非客观部分来构造。最著名的[客观率](@entry_id:198692)之一是**Jaumann率** `$\overset{\triangle}{\boldsymbol{\sigma}}$`，定义为：

$$
\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\boldsymbol{W} - \boldsymbol{W}\boldsymbol{\sigma}
$$

Jaumann率代表了在与材料一起以角速度 `$\mathbf{W}$` 旋转的[参考系](@entry_id:169232)（即[共转参考系](@entry_id:158071)）中观察到的应力变化率。通过引入 `$\mathbf{W}$` 进行修正，Jaumann率在纯[刚体转动](@entry_id:191086)下为零，恢复了物理上的客观性。因此，客观的[弹塑性](@entry_id:193198)[本构关系](@entry_id:186508)通常写成 `$\overset{\triangle}{\boldsymbol{\sigma}} = f(\mathbf{D}, \boldsymbol{\sigma})$` 的形式。这种构造确保了塑性功等物理量只依赖于变形 `$\mathbf{D}$`，而与观察者的旋转无关。[@problem_id:3563976]

### [地质力学](@entry_id:175967)中的高等应用

`$\mathbf{D}$` 和 `$\mathbf{W}$` 的分解不仅对建立客观[本构模型](@entry_id:174726)至关重要，也为我们理解[地质材料](@entry_id:749838)在复杂加载下的行为提供了深刻见解。

#### 简单剪切中的非共轴性

我们再次审视简单剪切流 `$\mathbf{v} = (\dot{\gamma}y, 0)$`。我们已经计算出 `$\mathbf{D} = \begin{pmatrix} 0  \dot{\gamma}/2 \\ \dot{\gamma}/2  0 \end{pmatrix}$`。这个[应变率张量](@entry_id:266108) `$\mathbf{D}$` 的[主方向](@entry_id:276187)（[特征向量](@entry_id:151813)方向）是与 `x` 轴成 `$\pm 45^{\circ}$` 的方向。由于 `$\mathbf{D}$` 是一个常数张量，这些[主方向](@entry_id:276187)在空间中是固定的。

然而，[自旋张量](@entry_id:187346) `$\mathbf{W}$` 描述了材料单元本身正在以 `$\omega_m = -\dot{\gamma}/2$` 的角速度顺时针旋转。这意味着，当材料变形时，构成材料的物质线（material lines）在旋转，但最大拉伸率的方向（`$\mathbf{D}$` 的主方向）却保持固定。因此，**[应变率](@entry_id:154778)的主轴与物质线之间存在相对转动**。这种现象被称为**非共轴性**（non-coaxiality），即应力张量（通常与[应变率张量](@entry_id:266108) `$\mathbf{D}$` 共轴）的[主轴](@entry_id:172691)与材料结构的[主轴](@entry_id:172691)不重合。这在[地质材料](@entry_id:749838)（如砂土）的大剪切变形中是一个关键特征。[@problem_id:3564021]

#### [客观率](@entry_id:198692)的选择

虽然Jaumann率是实现客观性的标准方法，但它并非完美无缺。在模拟[大应变](@entry_id:751152)简单剪切时，使用Jaumann率的[本构模型](@entry_id:174726)会预测出应力分量随应变增加而发生不符合物理实际的[振荡](@entry_id:267781)。

这个问题的根源在于，Jaumann率所使用的“共转”[参考系](@entry_id:169232)的旋转速率由连续体自旋 `$\mathbf{W}$` 定义，但这并不总是描述材料内部物理旋转的最佳选择。一个更物理的选择是使用由变形梯度 `$\mathbf{F}$` 的极分解 `$\mathbf{F}=\mathbf{R}\mathbf{U}$` 中的[旋转张量](@entry_id:191990) `$\mathbf{R}$` 所定义的自旋 `$\dot{\mathbf{R}}\mathbf{R}^{\mathsf{T}}$`。基于此自旋定义的[客观率](@entry_id:198692)被称为**[Green-Naghdi率](@entry_id:190839)**。

在简单剪切中，可以证明 `$\mathbf{W}$` 是常数，而 `$\dot{\mathbf{R}}\mathbf{R}^{\mathsf{T}}$` 会随着剪切应变 `k` 的增加而趋于零。[Green-Naghdi率](@entry_id:190839)的这种特性使其能够避免Jaumann率的[虚假振荡](@entry_id:152404)问题，从而更适合模拟[地质材料](@entry_id:749838)中的大[剪切带](@entry_id:183352)等现象。[@problem_id:3564031] 另一个性能优越的[客观率](@entry_id:198692)是基于[对数应变](@entry_id:751438)的**对数率**（logarithmic rate），在[平面应变](@entry_id:167046)问题中，它与[Green-Naghdi率](@entry_id:190839)等价。

#### [微极连续体](@entry_id:751972)模型

对于[颗粒材料](@entry_id:750005)（如砂土、谷物），除了连续体的宏观变形外，颗粒自身的旋转也是一个重要的自由度。经典的连续介质力学无法描述这种独立的颗粒旋转。**[微极连续体](@entry_id:751972)**（micropolar continuum）或**[Cosserat连续体](@entry_id:163213)**理论通过引入一个独立的运动学场——**微观转动角[速度矢量](@entry_id:269648)** `$\boldsymbol{\omega}$`——来解决这个问题。

在这种扩展理论中，材料的旋转行为由两部分贡献：宏观的连续体自旋 `$\mathbf{W}$` 和独立的微观转动 `$\boldsymbol{\omega}$`。真正驱动材料内部力偶和[非对称应力](@entry_id:191550)的是两者之差，即**相对[自旋张量](@entry_id:187346)** `$\boldsymbol{\Gamma}$`：

$$
\boldsymbol{\Gamma} = \mathbf{W} - [\boldsymbol{\omega}]_{\times}
$$

其中 `$[\boldsymbol{\omega}]_{\times}$` 是微观转动角速度矢量对应的反对稱张量。这个推广的运动学量 `$\boldsymbol{\Gamma}$` 取代了 `$\mathbf{W}$` 在本构关系中的部分角色，使得模型能够捕捉由颗粒旋转引起的更复杂的力学行为。[@problem_id:3564002]

总之，对应变率张量 `$\mathbf{D}$` 和[自旋张量](@entry_id:187346) `$\mathbf{W}$` 的深刻理解，是掌握现代[计算地质力学](@entry_id:747617)不可或缺的一环。`$\mathbf{D}$` 主导变形和能量耗散，而 `$\mathbf{W}$` 则关联着旋转和客观性，二者的正确区分与运用是进行精确、可靠的大变形数值模拟的基石。