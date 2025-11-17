## 引言
在工程与科学领域，理解物体如何在外力作用下变形是分析其行为的基础。微[小应变张量](@entry_id:754968)是[连续介质力学](@entry_id:155125)中描述变形的核心工具，它为量化材料内部的拉伸、压缩和扭曲提供了简洁而强大的数学框架。然而，如何从复杂的物体运动中精确分离出真正引起内力变化的“纯变形”，并忽略不产生应力的[刚体运动](@entry_id:193355)，是[运动学](@entry_id:173318)分析中的一个关键问题。本文旨在系统性地解决这一问题。

本文将分为三个部分，引导读者全面掌握微[小应变张量](@entry_id:754968)。在“原理与机制”一章中，我们将从[位移场](@entry_id:141476)出发，严格推导应变张量的定义，阐明其各分量的物理意义，并探讨其数学性质与适用边界。接着，在“应用与交叉学科联系”一章中，我们将展示该理论如何在固体力学、实验测量、[计算模拟](@entry_id:146373)等多个领域中发挥关键作用。最后，通过一系列“动手实践”练习，读者将有机会将理论知识应用于具体问题的求解。现在，让我们从其最基本的运动学原理开始，深入探索微[小应变张量](@entry_id:754968)的构建过程。

## 原理与机制

在连续介质力学中，理解物体如何因受力而变形是核心任务之一。变形的局部几何特征由应变来量化。对于位移和[位移梯度](@entry_id:165352)足够小的情况，我们可以采用一种线性化的[应变度量](@entry_id:755495)，即**微[小应变张量](@entry_id:754968)**（infinitesimal strain tensor）。本章将系统地阐述微[小应变张量](@entry_id:754968)的定义、物理意义、数学性质及其适用范围，为后续的[本构关系](@entry_id:186508)和[应力分析](@entry_id:168804)奠定坚实的运动学基础。

### 从变形到应变：[运动学](@entry_id:173318)描述

考虑一个连续体，其物质点在参考构型中的位置由矢量 $\mathbf{X}$ 描述。经过变形后，该物[质点](@entry_id:186768)移动到当前构型中的位置 $\mathbf{x}$。[位移矢量场](@entry_id:196067) $\mathbf{u}$ 定义为当前位置与[参考位](@entry_id:754187)置之差：$\mathbf{u}(\mathbf{X}) = \mathbf{x} - \mathbf{X}$。在[小变形理论](@entry_id:174991)中，我们通常不区分物质坐标 $\mathbf{X}$ 和空间坐标 $\mathbf{x}$，因此将位移场写为 $\mathbf{u}(\mathbf{x})$。

变形的局部变化由**[位移梯度张量](@entry_id:748571)**（displacement gradient tensor）捕捉，其分量定义为 $u_{i,j} := \partial u_i / \partial x_j$。这个[二阶张量](@entry_id:199780)包含了关于局部拉伸、剪切和[刚体转动](@entry_id:191086)的全部信息。然而，要建立一个纯粹度量“变形”（即排除刚体运动）的物理量，我们需要进一步处理。

度量变形的一个自然方法是考察材料微元的长度变化。考虑参考构型中连接两个相邻物质点的微元矢量 $d\mathbf{x}$。它的初始长度平方为 $ds^2 = d\mathbf{x} \cdot d\mathbf{x} = dx_i dx_i$。变形后，这个微元矢量变为 $d\mathbf{x}'$。根据[位移场](@entry_id:141476)的定义，有 $\mathbf{x}' = \mathbf{x} + \mathbf{u}(\mathbf{x})$，因此 $d\mathbf{x}' = d\mathbf{x} + d\mathbf{u}$。利用链式法则，$d u_i = (\partial u_i / \partial x_j) dx_j = u_{i,j} dx_j$。于是，变形后的微元矢量为：
$dx'_i = dx_i + u_{i,j} dx_j = (\delta_{ij} + u_{i,j}) dx_j$
其中 $\delta_{ij}$ 是克罗内克符号。

变形后微元的长度平方为 $ds'^2 = dx'_k dx'_k$。代入上式并展开：
$ds'^2 = (\delta_{ki} + u_{k,i}) dx_i (\delta_{kj} + u_{k,j}) dx_j = (\delta_{ij} + u_{j,i} + u_{i,j} + u_{k,i}u_{k,j}) dx_i dx_j$

长度平方的改变量为 $\Delta(ds^2) = ds'^2 - ds^2$。注意到 $ds^2 = \delta_{ij} dx_i dx_j$，我们得到：
$\Delta(ds^2) = (u_{i,j} + u_{j,i} + u_{k,i}u_{k,j}) dx_i dx_j$

这个表达式是精确的。微小应变理论的核心在于**线性化**，即假设[位移梯度](@entry_id:165352) $u_{i,j}$ 的分量远小于1。在此假设下，我们可以忽略所有关于 $u_{i,j}$ 的二次项（或更高次项）。因此，二次项 $u_{k,i}u_{k,j}$ 被舍弃，长度平方的改变量近似为：
$\Delta(ds^2) \approx (u_{i,j} + u_{j,i}) dx_i dx_j$

我们定义一个张量 $\epsilon_{ij}$ 来描述这种线性化的变形，使得 $\Delta(ds^2) = 2 \epsilon_{ij} dx_i dx_j$。比较上式，我们便得到了**微[小应变张量](@entry_id:754968)**（或称柯西[应变张量](@entry_id:193332)）的定义 [@problem_id:2697893]：
$$ \boldsymbol{\epsilon}_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i}) $$

从定义可知，$\epsilon_{ij}$ 是[位移梯度张量](@entry_id:748571) $u_{i,j}$ 的对称部分。通过构造，$\epsilon_{ij}$ 是一个**对称张量**，即 $\epsilon_{ij} = \epsilon_{ji}$。相应地，位移梯度[张量的反对称部分](@entry_id:193562)定义为**微小转动张量**（infinitesimal rotation tensor）：
$$ \boldsymbol{\omega}_{ij} = \frac{1}{2}(u_{i,j} - u_{j,i}) $$

任何[位移梯度张量](@entry_id:748571)都可以唯一地分解为其对称和反对称部分之和，这被称为**[亥姆霍兹分解](@entry_id:181767)**（Helmholtz decomposition）：
$u_{i,j} = \epsilon_{ij} + \omega_{ij}$

这个分解至关重要，因为它将局部的运动学变化分离为纯变形（由 $\epsilon_{ij}$ 描述）和纯[刚体转动](@entry_id:191086)（由 $\omega_{ij}$ 描述）。一个关键性质是，对于任意微小的刚体运动（平动加转动），其位移场为 $u_i = c_i + \Omega_{ik}x_k$（其中 $c_i$ 是常数[平动](@entry_id:187700)，$\Omega_{ik}$ 是常数反对称转动张量），[位移梯度](@entry_id:165352)为 $u_{i,j} = \Omega_{ij}$。此时，应变张量为 $\epsilon_{ij} = \frac{1}{2}(\Omega_{ij} + \Omega_{ji}) = \frac{1}{2}(\Omega_{ij} - \Omega_{ij}) = 0$。这证实了微[小应变张量](@entry_id:754968)是一个客观的变形度量，它能有效地“过滤”掉[刚体转动](@entry_id:191086)的影响，只保留引起长度和角度变化的真实变形。

### 应变分量的物理诠释

微[小应变张量](@entry_id:754968)的九个分量具有清晰的几何意义，可分为**[正应变](@entry_id:204633)**（normal strain）和**[剪应变](@entry_id:175241)**（shear strain）。

#### [正应变](@entry_id:204633)

张量的对角分量，如 $\epsilon_{xx}$、$\epsilon_{yy}$ 和 $\epsilon_{zz}$，被称为**[正应变](@entry_id:204633)**。它们度量了材料微元在相应坐标轴方向上的相对伸长或缩短。根据定义：
$\epsilon_{xx} = \frac{1}{2}(u_{x,x} + u_{x,x}) = \frac{\partial u_x}{\partial x}$
类似地，$\epsilon_{yy} = \partial u_y/\partial y$ 和 $\epsilon_{zz} = \partial u_z/\partial z$。

考虑一个初始时沿 $x$ 轴、长度为 $L$ 的材料线段。变形后，其长度变为 $L'$。通过线性化分析可以证明，其相对长度变化为 [@problem_id:2697900]：
$$ \frac{L' - L}{L} \approx \epsilon_{xx} $$
因此，$\epsilon_{xx}$ 就是材料沿 $x$ 方向的单位长度伸长率。正值为拉伸，负值为压缩。

#### [剪应变](@entry_id:175241)

张量的非对角分量，如 $\epsilon_{xy}$、$\epsilon_{yz}$ 和 $\epsilon_{zx}$，被称为**张量[剪应变](@entry_id:175241)**（tensorial shear strain）。它们度量了初始时相互垂直的两个材料线段之间夹角的变化。

考虑初始时分别沿 $x$ 轴和 $y$ 轴的两个材料线段，它们之间的夹角为 $\pi/2$。变形后，这两条线段之间的夹角变为 $\theta_{xy}$。可以证明，在[一阶近似](@entry_id:147559)下，原直角的减小量（以弧度计）为 [@problem_id:2697900]：
$$ \frac{\pi}{2} - \theta_{xy} \approx \frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x} $$
这个量在工程领域被定义为**工程[剪应变](@entry_id:175241)**（engineering shear strain），记作 $\gamma_{xy}$。
$$ \gamma_{xy} = \frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x} $$

比较工程[剪应变](@entry_id:175241)与张量[剪应变](@entry_id:175241)的定义 $\epsilon_{xy} = \frac{1}{2}(\partial u_x/\partial y + \partial u_y/\partial x)$，我们得到它们之间重要的关系：
$$ \gamma_{xy} = 2\epsilon_{xy} $$
类似地，$\gamma_{yz} = 2\epsilon_{yz}$ 和 $\gamma_{zx} = 2\epsilon_{zx}$。

这个因子 2 的来源具有深刻的几何意义 [@problem_id:2697916]。角度变化 $\gamma_{xy}$ 是由两个独立的转动贡献之和构成的：初始沿 $y$ 轴的线段因位移分量 $u_x$ 的变化而向 $x$ 轴方向转动了角度近似为 $\partial u_x/\partial y$；同时，初始沿 $x$ 轴的线段因位移分量 $u_y$ 的变化而向 $y$ 轴方向转动了角度近似为 $\partial u_y/\partial x$。总的角度变化是这两者之和。而张量分量 $\epsilon_{xy}$ 则代表了这两个转动贡献的平均值，这使得[应变能](@entry_id:162699)够作为一个真正的张量在不同[坐标系](@entry_id:156346)下进行正确的变换。

为了更具体地理解[位移梯度](@entry_id:165352)、应变和转动的关系，我们考察一个**简单剪切**（simple shear）的例子 [@problem_id:2697919]。考虑位移场 $u_1 = \gamma x_2, u_2 = 0, u_3 = 0$，其中 $\gamma$ 是一个小的无量纲参数。
[位移梯度张量](@entry_id:748571)矩阵为：
$$ [u_{i,j}] = \begin{pmatrix} 0  \gamma  0 \\ 0  0  0 \\ 0  0  0 \end{pmatrix} $$
[应变张量](@entry_id:193332)（对称部分）为：
$$ [\epsilon_{ij}] = \begin{pmatrix} 0  \gamma/2  0 \\ \gamma/2  0  0 \\ 0  0  0 \end{pmatrix} $$
转动张量（反对称部分）为：
$$ [\omega_{ij}] = \begin{pmatrix} 0  \gamma/2  0 \\ -\gamma/2  0  0 \\ 0  0  0 \end{pmatrix} $$
这个例子清晰地表明，简单剪切可以被分解为一个**纯剪切**（pure shear，由 $\epsilon_{ij}$ 描述，它使正方形变形为菱形）和一个[刚体转动](@entry_id:191086)（由 $\omega_{ij}$ 描述）。转动张量 $[\omega_{ij}]$ 对应于绕 $x_3$ 轴顺时针旋转一个微小角度 $\theta = \gamma/2$，即旋转角度为 $-\gamma/2$。

### 体积应变与[偏应变](@entry_id:201263)的分解

任何变形状态都可以被分解为两部分的叠加：一部分只改变体积而不改变形状，另一部分只改变形状而不改变体积。这种分解在数学上对应于将[应变张量](@entry_id:193332) $\epsilon_{ij}$ 分解为其**球量部分**（spherical part，或称各向同性部分）和**偏量部分**（deviatoric part）。

[应变张量](@entry_id:193332)的迹，记为 $\epsilon_{kk} = \epsilon_{xx} + \epsilon_{yy} + \epsilon_{zz}$，具有特殊的物理意义。在一阶近似下，它等于材料微元的相对体积变化，被称为**体积应变**或**膨胀**（dilatation）：
$$ \frac{\Delta V}{V} \approx \epsilon_{kk} = \nabla \cdot \mathbf{u} $$

根据这个概念，我们可以将[应变张量分解](@entry_id:184653)如下 [@problem_id:2697930]：
$$ \epsilon_{ij} = \epsilon_{ij}^{\text{vol}} + s_{ij} $$
其中：
- $\epsilon_{ij}^{\text{vol}} = \frac{1}{3}\epsilon_{kk}\delta_{ij}$ 是应变的**球量部分**或**体积应变张量**。它是一个各向同性的张量，代表了在所有方向上均匀的拉伸或压缩，只引起体积变化而不改变形状。它的迹等于总体积应变 $\epsilon_{mm}^{\text{vol}} = \frac{1}{3}\epsilon_{kk}\delta_{mm} = \epsilon_{kk}$。
- $s_{ij} = \epsilon_{ij} - \frac{1}{3}\epsilon_{kk}\delta_{ij}$ 是应变的**偏量部分**或**偏应变张量**。通过构造，它的迹恒为零 ($s_{kk} = 0$)。因此，偏应变张量描述的是一种**[等容变形](@entry_id:196451)**（isochoric deformation），即只改变物体的形状（扭曲）而不改变其体积。

这种分解在[材料科学](@entry_id:152226)和[流体力学](@entry_id:136788)中极为重要，因为许多材料（如金属在塑性变形时，或[不可压缩流体](@entry_id:181066)）对体积变化和形状变化的响应方式截然不同。

### [应变不变量](@entry_id:190518)与[主应变](@entry_id:197797)

由于[应变张量](@entry_id:193332) $\epsilon_{ij}$ 是对称的，它在每个物[质点](@entry_id:186768)都存在一个特殊的[坐标系](@entry_id:156346)，使得在该[坐标系](@entry_id:156346)下，[剪应变](@entry_id:175241)分量全部为零。这个[坐标系](@entry_id:156346)的方向被称为**主方向**（principal directions），而在这些方向上的[正应变](@entry_id:204633)被称为**[主应变](@entry_id:197797)**（principal strains），记为 $\epsilon_1, \epsilon_2, \epsilon_3$。它们是[应变张量](@entry_id:193332)矩阵的[特征值](@entry_id:154894)。[主应变](@entry_id:197797)代表了该点处材料所经历的最大和最小的拉伸或压缩。

尽管应变张量的分量会随着[坐标系](@entry_id:156346)的旋转而改变，但某些组合量在任何[坐标系](@entry_id:156346)下都保持不变。这些量被称为**[应变不变量](@entry_id:190518)**（strain invariants）。对于一个三维[应变张量](@entry_id:193332)，有三个基本[不变量](@entry_id:148850) [@problem_id:2697880]：
- **第一[不变量](@entry_id:148850)** $I_1 = \text{tr}(\boldsymbol{\epsilon}) = \epsilon_{kk} = \epsilon_1 + \epsilon_2 + \epsilon_3$
- **第二[不变量](@entry_id:148850)** $I_2 = \frac{1}{2}[(\text{tr}(\boldsymbol{\epsilon}))^2 - \text{tr}(\boldsymbol{\epsilon}^2)] = \frac{1}{2}[\epsilon_{kk}^2 - \epsilon_{ij}\epsilon_{ij}] = \epsilon_1\epsilon_2 + \epsilon_2\epsilon_3 + \epsilon_3\epsilon_1$
- **第三[不变量](@entry_id:148850)** $I_3 = \det(\boldsymbol{\epsilon}) = \epsilon_1\epsilon_2\epsilon_3$

这些[不变量](@entry_id:148850)的“[不变性](@entry_id:140168)”意味着它们是描述应变状态的内在属性，不依赖于观察者的[坐标系](@entry_id:156346)选择 [@problem_id:2697880]。它们的物理意义如下：
- $I_1$ 直接与体积变化相关，即 $I_1 \approx \Delta V/V$。
- 对于[等容变形](@entry_id:196451)（$I_1=0$），第二[不变量](@entry_id:148850)简化为 $I_2 = -\frac{1}{2}\epsilon_{ij}\epsilon_{ij}$。这个量总是非正的，其大小与[偏应变](@entry_id:201263)的程度相关，并与材料的[畸变能](@entry_id:198925)（shape distortion energy）有关。
- $I_3$ 是[主应变](@entry_id:197797)的乘积。在小应变理论中，体积变化主要由 $I_1$ 决定。$I_2$ 和 $I_3$ 的贡献是高阶小量，通常可以忽略 [@problem_id:2697880]。例如，一个纯剪切应变状态，其矩阵为 $\begin{pmatrix} 0  \gamma/2  0 \\ \gamma/2  0  0 \\ 0  0  0 \end{pmatrix}$，我们有 $I_1 = 0$, $I_3 = 0$，但 $I_2 = -(\gamma/2)^2 \neq 0$。

### 线性化的局限：适用条件与[失效机制](@entry_id:184047)

微小应变理论的简洁性和实用性是建立在严格的数学假设之上的。理解其适用范围和[失效机制](@entry_id:184047)至关重要。

#### 理论的正式推导与假设

微[小应变张量](@entry_id:754968) $\boldsymbol{\epsilon}$ 是更普适的[有限应变理论](@entry_id:176941)在线性化极限下的产物。在有限变形理论中，一个常用的[应变度量](@entry_id:755495)是**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange strain tensor）$\mathbf{E}$。它与[位移梯度](@entry_id:165352) $\mathbf{H}$（即 $u_{i,j}$）的精确关系为 [@problem_id:2697912]：
$$ \mathbf{E} = \frac{1}{2}(\mathbf{H} + \mathbf{H}^T + \mathbf{H}^T\mathbf{H}) = \boldsymbol{\epsilon} + \frac{1}{2}\mathbf{H}^T\mathbf{H} $$
这个关系是纯粹的[运动学](@entry_id:173318)恒等式，不依赖于任何材料属性。

微小应变理论的有效性依赖于用 $\boldsymbol{\epsilon}$ 来近似 $\mathbf{E}$ 的合理性，即忽略[非线性](@entry_id:637147)的二次项 $\frac{1}{2}\mathbf{H}^T\mathbf{H}$。这一近似成立的充要条件是，[位移梯度张量](@entry_id:748571)的所有分量都必须是小量 [@problem_id:2697869]，即对于所有 $i,j$，满足 $|\partial u_i / \partial x_j| \ll 1$。用范数可以表示为 $\|\mathbf{H}\| \ll 1$。

由于 $\mathbf{H}$ 可以分解为应变 $\boldsymbol{\epsilon}$ 和转动 $\boldsymbol{\omega}$，$\|\mathbf{H}\| \ll 1$ 的条件意味着**应变和转动都必须是微小的**。

#### [失效机制](@entry_id:184047)：大转动问题

微小应变理论最常见的失效场景是**小应变伴随大转动**。在许多工程问题中，例如细长梁或薄壳的大挠度弯曲，材料本身的拉伸和剪切（应变）可能非常小，在弹性范围内，但结构的几何形状发生了显著改变，导致材料微元经历了大幅度的[刚体转动](@entry_id:191086)。

在这种情况下，虽然 $\|\boldsymbol{\epsilon}\|$ 很小，但 $\|\boldsymbol{\omega}\|$ 可能达到甚至超过1。这导致[位移梯度](@entry_id:165352) $\|\mathbf{H}\|$ 不再是小量，线性化假设失效。若强行使用微[小应变张量](@entry_id:754968)，它会错误地将[刚体转动](@entry_id:191086)的一部分解释为应变。例如，一个纯[刚体转动](@entry_id:191086) $\theta$ 会产生虚假的、非零的[正应变](@entry_id:204633)分量，其大小约为 $-\theta^2/2$ [@problem_id:2697869]。这显然是非物理的，因为[刚体转动](@entry_id:191086)不应引起任何应变。

这一局限性与**[物质客观性原理](@entry_id:191727)**（principle of material objectivity，或称物质标架无关性）密切相关 [@problem_id:2697885]。该原理要求材料的本构关系（如[应力-应变关系](@entry_id:274093)）不能依赖于观察者的[刚体运动](@entry_id:193355)。微[小应变张量](@entry_id:754968) $\boldsymbol{\epsilon}$ 在叠加一个任意[刚体转动](@entry_id:191086)时，其值会发生改变，因此它不是一个**客观张量**。相比之下，[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 以及基于右[拉伸张量](@entry_id:193200) $\mathbf{U}$（来自极分解 $\mathbf{F}=\mathbf{R}\mathbf{U}$）定义的[应变度量](@entry_id:755495)（如[亨基应变](@entry_id:191329) $\mathbf{h} = \ln \mathbf{U}$）都是客观的，因为它们在定义中已经剔除了[刚体转动](@entry_id:191086) $\mathbf{R}$ 的影响。因此，对于存在大转动的问题，必须采用这些[非线性](@entry_id:637147)的、客观的[应变度量](@entry_id:755495)。一种常用的处理方法是**[共旋坐标法](@entry_id:747415)**（corotational approach），即在跟随材料微元一起转动的[坐标系](@entry_id:156346)中度量应变，从而将大转动效应分离出去 [@problem_id:2697885]。

### [应变协调性](@entry_id:199659)

微[小应变张量](@entry_id:754968)的六个独立分量是通过对三个位移分量求导得到的。这意味着这六个分量并非完全独立，它们必须满足一定的[微分](@entry_id:158718)约束关系，才能保证存在一个与之对应的、单值连续的位移场。这些约束关系被称为**[圣维南协调条件](@entry_id:173493)**（Saint-Venant compatibility conditions）。

如果一个给定的对称二阶张量场 $\epsilon_{ij}(\mathbf{x})$ 处处满足协调条件，则称该应变场是**协调的**（compatible）。反之，如果条件不满足，则应变场是**不协调的**（incompatible），这意味着不可能在整个区域内找到一个光滑的[位移场](@entry_id:141476)来产生这个应变场。

以二维[平面应变](@entry_id:167046)为例，三个应变分量 $\epsilon_{xx}, \epsilon_{yy}, \epsilon_{xy}$ 必须满足以下协调方程 [@problem_id:2697883]：
$$ \frac{\partial^2 \epsilon_{xx}}{\partial y^2} + \frac{\partial^2 \epsilon_{yy}}{\partial x^2} = 2 \frac{\partial^2 \epsilon_{xy}}{\partial x \partial y} $$
这个方程是通过对 $\epsilon_{ij}$ 的定义式进行二[次微分](@entry_id:175641)并消去位移分量得到的。

考虑一个假设的应变场，其唯一的非零分量为 $\epsilon_{xy} = \frac{\alpha}{2}xy$（$\alpha$为非零常数）。将它代入上述协调方程，我们得到 $0+0 = 2(\alpha/2)$，即 $0 = \alpha$。这与 $\alpha \neq 0$ 的前提矛盾，说明该应变场是不协调的 [@problem_id:2697883]。

在三维空间中，协调条件更为复杂，可以用**不协调张量** $\eta_{ij}$ 来统一表达。当且仅当一个应变场是协调的，其不协调张量处处为零。不协调的应变场在物理上并非毫无意义；它通常与材料内部的非弹性变形源有关，例如晶体中的[位错](@entry_id:157482)、不均匀的温度变化或[相变](@entry_id:147324)。这些情况会在没有外力的情况下产生所谓的“内应力”。

总之，微[小应变张量](@entry_id:754968)是线性固体力学的基石，它为描述小变形提供了一个简洁而强大的工具。然而，作为一名严谨的科学家或工程师，必须深刻理解其推导过程、物理意义、数学性质，并时刻警惕其在处理大转动问题时的局限性以及协调性条件的内在要求。