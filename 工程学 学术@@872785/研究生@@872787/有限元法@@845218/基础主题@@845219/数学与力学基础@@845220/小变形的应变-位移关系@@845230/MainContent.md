## 引言
在[固体力学](@entry_id:164042)和工程分析中，理解物体如何在外力作用下变形是核心任务之一。连接宏观位移与内部变形的桥梁，正是[应变-位移关系](@entry_id:173321)。这一基本[运动学](@entry_id:173318)关系描述了物体内任意一点的位移场如何导致局部材料的拉伸、压缩和剪切。然而，精确的非[线性关系](@entry_id:267880)在数学上非常复杂，给解析和计算带来了巨大挑战。因此，在绝大多数工程应用中，我们都依赖一个关键的简化——“小变形假设”。本文旨在系统性地阐明[小变形理论](@entry_id:174991)的内涵，填补从抽象数学定义到实际工程计算应用之间的知识鸿沟。

本文将引导读者完成一次从理论到实践的完整旅程。在第一章“原理与机制”中，我们将从最基本的变形几何出发，推导出精确的[格林-拉格朗日应变张量](@entry_id:187745)，然后通过线性化得到在工程中广泛使用的[无穷小应变张量](@entry_id:167211)，并详细讨论其适用条件与物理意义。接下来的“应用与跨学科联系”一章将展示这些原理的强大生命力，探讨它们如何构筑起[有限元法](@entry_id:749389)的离散化基础，如何简化为梁、板等结构理论，以及如何帮助解决[体积锁定](@entry_id:172606)等高级数值难题。最后，“动手实践”部分将通过具体的计算练习，巩固理论知识并将其付诸实践。现在，让我们首先深入探讨描述变形的基本原理与核心机制。

## 原理与机制

在连续介质力学和[有限元分析](@entry_id:138109)中，描述物体变形的核心是建立变形几何与物体内部各点位移之间的数学关系。本章旨在深入阐述小变形假设下应变与位移关系的基本原理和关键机制。我们将从最基本的[运动学](@entry_id:173318)概念出发，推导出线性应变张量，探讨其适用范围，并最终将其与[有限元法](@entry_id:749389)的离散化框架相结合。

### 应变的定义：从变形到张量

当一个连续体在外力、温度变化或其他因素作用下发生变形时，其内部各点会发生相对位移，从而导致局部尺寸和形状的改变。**应变 (strain)** 正是用于定量描述这种局部变形的物理量。一个严谨的[应变度量](@entry_id:755495)必须能够反映材料[线元](@entry_id:196833)长度和角度的变化，并且在刚体运动（即只有平移和旋转，没有形状改变）下其值应为零。

为了建立一个普适的度量，我们考虑变形前物体中两个无限接近的点，其位置矢量分别为 $\boldsymbol{X}$ 和 $\boldsymbol{X} + d\boldsymbol{X}$。它们之间距离的平方为 $ds_0^2 = d\boldsymbol{X} \cdot d\boldsymbol{X}$。经过一个变形映射 $\boldsymbol{x} = \boldsymbol{x}(\boldsymbol{X})$，这两点移动到新的位置 $\boldsymbol{x}$ 和 $\boldsymbol{x} + d\boldsymbol{x}$。位移场定义为 $\boldsymbol{u}(\boldsymbol{X}) = \boldsymbol{x}(\boldsymbol{X}) - \boldsymbol{X}$。

变形后两点间的距离平方为 $ds^2 = d\boldsymbol{x} \cdot d\boldsymbol{x}$。利用链式法则，我们有 $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$，其中 $\boldsymbol{F} = \partial \boldsymbol{x} / \partial \boldsymbol{X}$ 是**变形梯度张量 (deformation gradient tensor)**。因此，$ds^2 = (\boldsymbol{F} d\boldsymbol{X}) \cdot (\boldsymbol{F} d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}) d\boldsymbol{X}$。

距离平方的改变值 $ds^2 - ds_0^2$ 直接反映了变形。我们可以定义一个张量来描述这种改变：
$$
ds^2 - ds_0^2 = d\boldsymbol{X} \cdot (\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} - \boldsymbol{I}) d\boldsymbol{X} = 2 d\boldsymbol{X} \cdot \boldsymbol{E} d\boldsymbol{X}
$$
其中 $\boldsymbol{I}$ 是单位张量，而 $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} - \boldsymbol{I})$ 被称为**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)**。它是一个在有限变形理论中被广泛使用的精确[应变度量](@entry_id:755495)。

若以[位移梯度](@entry_id:165352) $u_{i,j} = \partial u_i / \partial X_j$ 来表示，变形梯度为 $F_{ij} = \delta_{ij} + u_{i,j}$，其中 $\delta_{ij}$ 是克罗内克符号。代入 $\boldsymbol{E}$ 的定义可得其分量形式 [@problem_id:2601645]：
$$
E_{ij} = \frac{1}{2} (u_{i,j} + u_{j,i} + u_{k,i} u_{k,j})
$$
这个表达式由线性项 $\frac{1}{2}(u_{i,j} + u_{j,i})$ 和[非线性](@entry_id:637147)的二次项 $\frac{1}{2}u_{k,i} u_{k,j}$ 组成。[格林-拉格朗日应变张量](@entry_id:187745)对于任意大小的位移和转动都是精确的，并且在刚体运动下其值为零。

### 小变形假设与线性化

在许多工程问题中，物体的变形非常小，这意味着[位移梯度](@entry_id:165352) $u_{i,j}$ 的分量远小于1。这个**小变形假设 (small deformation assumption)**，或更准确地说是**小[位移梯度](@entry_id:165352)假设 (small displacement gradient assumption)**，极大地简化了运动学关系。在此假设下，[位移梯度](@entry_id:165352)的二次项 $u_{k,i} u_{k,j}$ 是一个高阶小量，可以被忽略。同时，参考构型与当前构型之间的差异也很小，因此对参考坐标 $X_j$ 的[偏导数](@entry_id:146280)可以近似为对当前坐标 $x_j$ 的[偏导数](@entry_id:146280)。

通过忽略[格林-拉格朗日应变张量](@entry_id:187745)中的二次项，我们得到了**[无穷小应变张量](@entry_id:167211) (infinitesimal strain tensor)**，也称为**线性化应变张量 (linearized strain tensor)** 或柯西应变张量，其分量 $\epsilon_{ij}$ 定义为 [@problem_id:2601644]：
$$
\epsilon_{ij} = \frac{1}{2} (u_{i,j} + u_{j,i})
$$
其中 $u_{i,j}$ 代表 $\partial u_i / \partial x_j$。按照张量记法的惯例，下标 $i$ 表示[位移矢量场](@entry_id:196067) $\boldsymbol{u}$ 的分量，而逗号后的下标 $j$ 表示进行[偏微分](@entry_id:194612)所依据的空间坐标 $x_j$。从定义可以看出，该张量是对称的，即 $\epsilon_{ij} = \epsilon_{ji}$。对角分量 $\epsilon_{ii}$（无求和）表示沿 $x_i$ 轴方向的**[正应变](@entry_id:204633) (normal strain)**，即单位长度的伸长或缩短。非对角分量 $\epsilon_{ij}$ ($i \neq j$) 表示 $x_i$ 和 $x_j$ 轴之间夹角变化的一半，称为**张量[剪应变](@entry_id:175241) (tensorial shear strain)**。在工程应用中，更常用的是**工程[剪应变](@entry_id:175241) (engineering shear strain)** $\gamma_{ij} = 2\epsilon_{ij} = u_{i,j} + u_{j,i}$。

线性化近似的有效性取决于[位移梯度](@entry_id:165352)的大小。我们可以通过一个[尺度分析](@entry_id:153681)来理解这一点 [@problem_id:2601645]。假设一个物体的特征长度为 $L$，[特征位移](@entry_id:140262)为 $U$，特征转动角为 $\Theta$。那么，应变部分的特征尺度约为 $U/L$，而转动部分的特征尺度约为 $\Theta$。[位移梯度](@entry_id:165352)的整体尺度为 $\mathcal{O}(U/L + \Theta)$。线性项 $\epsilon_{ij}$ 的尺度为 $\mathcal{O}(U/L)$，而被忽略的二次项的尺度为 $\mathcal{O}((U/L + \Theta)^2)$。要使线性化成立，必须满足：
$$
\mathcal{O}((U/L + \Theta)^2) \ll \mathcal{O}(U/L)
$$
这要求[位移梯度](@entry_id:165352)的所有分量都必须是小量，即 $||\nabla \boldsymbol{u}|| \ll 1$，这等价于要求**应变和转动都必须是小量** ($U/L \ll 1$ 且 $\Theta \ll 1$)。

一个特别重要且微妙的情况是**大转动、小应变 (large rotations, small strains)**，例如细长梁的大挠度弯曲。在这种情况下，尽管材料本身的拉伸或压缩很小（$\epsilon \approx U/L \ll 1$），但物体的整体转动可能很大（$\theta = \mathcal{O}(1)$）。此时，[位移梯度](@entry_id:165352)不再是小量，线性化应变张量 $\epsilon_{ij}$ 会产生完全错误的、非物理的“伪应变” [@problem_id:2601696]。而精确的[格林-拉格朗日应变张量](@entry_id:187745) $E_{ij}$ 之所以依然能够正确描述变形，是因为其[非线性](@entry_id:637147)的二次项 $u_{k,i} u_{k,j}$ 在大转动情况下会精确地抵消由转动在线性项中引入的伪应变，从而正确地报告出真实的零应变（对于纯[刚体转动](@entry_id:191086)）或小应变。因此，[无穷小应变](@entry_id:197162)理论仅适用于[几何线性](@entry_id:203076)问题。

### [位移梯度](@entry_id:165352)的分解：应变与转动

[位移梯度张量](@entry_id:748571) $u_{i,j}$ 包含了物体局部运动的全部信息，包括形状的改变和刚性的转动。任何一个[二阶张量](@entry_id:199780)都可以唯一地分解为一个对称[部分和](@entry_id:162077)一个反对称部分。将此分解应用于[位移梯度张量](@entry_id:748571) [@problem_id:2601615]：
$$
u_{i,j} = \epsilon_{ij} + \omega_{ij}
$$
其中，
$$
\epsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i}) \quad (\text{对称部分, 无穷小应变张量})
$$
$$
\omega_{ij} = \frac{1}{2}(u_{i,j} - u_{j,i}) \quad (\text{反对称部分, 无穷小转动张量})
$$
这个分解具有清晰的物理意义。对称部分 $\epsilon_{ij}$ 正是我们之前定义的应变张量，它完全描述了材料单元的拉伸和剪切变形。反对称部分 $\omega_{ij}$ 则描述了材料单元的**无穷小[刚体转动](@entry_id:191086) (infinitesimal rigid-body rotation)**。对于一个小的刚体运动，应变张量 $\epsilon_{ij}$ 的值为零，这再次证实了它是衡量真实变形的[正确度](@entry_id:197374)量。

在二维平面应变问题中，绕 $z$ 轴的转动分量可以表示为一个标量 $\omega = \frac{1}{2}(u_{y,x} - u_{x,y})$，其中 $u_{y,x} = \partial u_y / \partial x$ [@problem_id:2601615]。

这种分解在[有限元法](@entry_id:749389)的变分原理中至关重要。在[虚功原理](@entry_id:138749)中，内力[虚功](@entry_id:176403)密度由应力与虚[位移梯度](@entry_id:165352)的缩并给出：$\delta W_{int} = \sigma_{ij} \delta u_{i,j}$。由于柯西应力张量 $\sigma_{ij}$ 是对称的，而虚转动张量 $\delta \omega_{ij}$ 是反对称的，它们之间的缩并恒为零：
$$
\sigma_{ij} \delta \omega_{ij} = 0
$$
因此，内力[虚功](@entry_id:176403)密度可以简化为 $\delta W_{int} = \sigma_{ij} \delta \epsilon_{ij}$。这意味着，在经典[弹性理论](@entry_id:184142)中，只有变形（应变）才做功，[刚体转动](@entry_id:191086)不做内功。这为应力与应变是共轭能量变量提供了理论基础。

### [应变协调性](@entry_id:199659)：从应变场到唯一[位移场](@entry_id:141476)的条件

到目前为止，我们都是从一个已知的[位移场](@entry_id:141476) $\boldsymbol{u}$ 出发来计算应变场 $\boldsymbol{\epsilon}$。现在我们提出一个[逆问题](@entry_id:143129)：给定一个在定义域 $\Omega$ 内的对称二阶张量场 $\epsilon_{ij}(\boldsymbol{x})$，是否存在一个单值的[位移场](@entry_id:141476) $u_i(\boldsymbol{x})$，使得该应变场可以由这个[位移场](@entry_id:141476)通过 $\epsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$ 导出？这个问题被称为**[应变协调性](@entry_id:199659) (strain compatibility)** 问题 [@problem_id:2601686]。

如果位移场 $u_i$ 存在且足够光滑（例如 $C^3$ 类），那么其偏导数的求导次序可以交换。这一数学事实对应变场 $\epsilon_{ij}$ 的导数施加了严格的约束。这些约束条件被称为**[圣维南协调方程](@entry_id:754487) (Saint-Venant compatibility equations)**。其张量形式为 [@problem_id:2601686]：
$$
\epsilon_{ij,kl} + \epsilon_{kl,ij} - \epsilon_{il,kj} - \epsilon_{kj,il} = 0
$$
对于一个**单连通 (simply connected)** 的区域（即区域中任何闭合回路都可以[连续收缩](@entry_id:154115)到一点而不断裂），[圣维南协调方程](@entry_id:754487)是应变场存在对应位移场的充分必要条件。如果存在这样的位移场，它也不是唯一的，可以相差一个任意的刚体位移 $r_i(\boldsymbol{x}) = c_i + W_{ij}x_j$（其中 $c_i$ 是常数平移， $W_{ij}$ 是常数[反对称张量](@entry_id:199349)）。

在有限元法中，这个问题有其特殊的体现。对于标准的位移法有限元，我们使用 $C^0$ 连续的[插值函数](@entry_id:262791)（即位移在单元边界上连续，但其导数不一定连续）。我们从一个全局连续的[位移场](@entry_id:141476) $\boldsymbol{u}_h$ 出发，通过求导来计算每个单元内的应变场 $\boldsymbol{\epsilon}_h$。因为 $\boldsymbol{\epsilon}_h$ 是从一个全局单值的[位移场](@entry_id:141476) $\boldsymbol{u}_h$ 派生出来的，所以根据定义，这个应变场是**自动协调的 (compatible by construction)** [@problem_id:2601692]。尽管由于位移导数在单元边界上的[不连续性](@entry_id:144108)，计算出的应变场通常在单元间是不连续的，但这并不违反协调性的基本定义。然而，在一些高级的[混合有限元法](@entry_id:165231)中，应变和位移被当作独立的插值场，此时协调性就不再被自动满足，需要额外施加约束。

### 体积应变与不可压缩性

应变张量可以进一步分解为描述体积变化的部分和描述形状变化（剪切）的部分。**[体积应变](@entry_id:267252) (volumetric strain)** $\epsilon_v$ 定义为[应变张量](@entry_id:193332)的迹（或第一[不变量](@entry_id:148850)）[@problem_id:2601621]：
$$
\epsilon_v = \epsilon_{kk} = \epsilon_{11} + \epsilon_{22} + \epsilon_{33}
$$
对于小变形，[体积应变](@entry_id:267252)等于[位移场](@entry_id:141476)的散度，$\epsilon_v = \nabla \cdot \boldsymbol{u}$，它精确地代表了单位体积的相对变化量。

一些材料（如橡胶、水）在变形过程中体积几乎不变，这种性质被称为**不可压缩性 (incompressibility)**。在理想的[不可压缩材料](@entry_id:159741)中，体积应变为零，即 $\epsilon_v = 0$。这成了一个施加在位移场上的运动学约束。

在[有限元分析](@entry_id:138109)中，处理近似[不可压缩材料](@entry_id:159741)（即[泊松比](@entry_id:158876) $\nu$ 接近0.5）是一个巨大的挑战。对于标准的、完全积分的低阶单元，$\epsilon_v \approx 0$ 这个强约束会导致系统矩阵病态，产生非物理的、过高的刚度，使得单元无法正常变形。这种现象被称为**[体积锁定](@entry_id:172606) (volumetric locking)** [@problem_id:2601621]。为了解决这个问题，必须采用特殊的数值技术，例如[选择性减缩积分](@entry_id:168281)、[B-bar方法](@entry_id:169265)，或更高级的混合位移-压力（u-p）公式。在混合公式中，压力 $p$ 被引入作为一个独立的场变量，以拉格朗日乘子的形式弱化地施加不可压缩约束。

### 有限元中的[应变-位移关系](@entry_id:173321)

为了在计算机中实施[应变-位移关系](@entry_id:173321)，需要将其从连续的偏微分形式转化为离散的代数形式。

首先，为了方便矩阵运算，通常使用**Voigt记法 (Voigt notation)**，将对称的 $3 \times 3$ [应变张量](@entry_id:193332)（6个独立分量）写成一个 $6 \times 1$ 的列向量。例如，在三维情况下：
$$
\boldsymbol{\epsilon} = \begin{bmatrix} \epsilon_{xx}  \epsilon_{yy}  \epsilon_{zz}  \gamma_{yz}  \gamma_{xz}  \gamma_{xy} \end{bmatrix}^{\mathsf{T}}
$$
通过这种表示，连续的[应变-位移关系](@entry_id:173321) $\epsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$ 可以写成一个矩阵-[微分算子](@entry_id:140145)形式 $\boldsymbol{\epsilon} = \mathbf{L} \mathbf{u}$ [@problem_id:2601620]。其中 $\mathbf{u} = \begin{bmatrix} u_x  u_y  u_z \end{bmatrix}^{\mathsf{T}}$ 是位移向量，$\mathbf{L}$ 是一个由偏微分算子组成的矩阵。例如，在三维情况下，$\mathbf{L}$ 是一个 $6 \times 3$ 的矩阵：
$$
\mathbf{L} = \begin{bmatrix}
\frac{\partial}{\partial x}  0  0 \\
0  \frac{\partial}{\partial y}  0 \\
0  0  \frac{\partial}{\partial z} \\
0  \frac{\partial}{\partial z}  \frac{\partial}{\partial y} \\
\frac{\partial}{\partial z}  0  \frac{\partial}{\partial x} \\
\frac{\partial}{\partial y}  \frac{\partial}{\partial x}  0
\end{bmatrix}
$$
在有限元单元内部，位移场 $\mathbf{u}$ 是通过节点位移向量 $\mathbf{d}$ 和形函数矩阵 $\mathbf{N}$ 插值得到的：$\mathbf{u} = \mathbf{N} \mathbf{d}$。将此代入算子方程，我们得到有限元中最核心的几何关系式：
$$
\boldsymbol{\epsilon} = \mathbf{L}(\mathbf{N}\mathbf{d}) = (\mathbf{L}\mathbf{N})\mathbf{d} = \mathbf{B}\mathbf{d}
$$
矩阵 $\mathbf{B} = \mathbf{L}\mathbf{N}$ 被称为**[应变-位移矩阵](@entry_id:163451) (strain-displacement matrix)** 或简称为[B矩阵](@entry_id:178522)。它直接将单元的节点位移与单元内任意一点的应变联系起来。[B矩阵](@entry_id:178522)的构建是计算[单元刚度矩阵](@entry_id:139369)的基础。

以一个二维四节点四边形（Q4）单元为例 [@problem_id:2601630]，其节点位移向量为 $\mathbf{d} \in \mathbb{R}^8$，应变向量为 $\boldsymbol{\epsilon} \in \mathbb{R}^3$。[B矩阵](@entry_id:178522)是一个 $3 \times 8$ 的矩阵，其分量由形函数对物理坐标 $(x,y)$ 的[偏导数](@entry_id:146280)组成：
$$
\mathbf{B} = \begin{pmatrix}
N_{1,x}  0        N_{2,x}  0        N_{3,x}  0        N_{4,x}  0       \\
0        N_{1,y}  0        N_{2,y}  0        N_{3,y}  0        N_{4,y} \\
N_{1,y}  N_{1,x}  N_{2,y}  N_{2,x}  N_{3,y}  N_{3,x}  N_{4,y}  N_{4,x}
\end{pmatrix}
$$
这里，$N_{i,x} = \partial N_i / \partial x$，$N_{i,y} = \partial N_i / \partial y$。

然而，形函数 $N_i$ 通常是在一个简单的、规则的父单元域（例如，对于[Q4单元](@entry_id:176936)是 $(\xi, \eta) \in [-1,1] \times [-1,1]$）中定义的。为了得到对物理坐标的导数，必须使用**[等参映射](@entry_id:173239) (isoparametric mapping)** 和微积分的[链式法则](@entry_id:190743) [@problem_id:2601668]。形函数对物理坐标的导数向量可以通过求解以下线性方程组得到：
$$
\begin{pmatrix} \partial N_i / \partial \xi \\ \partial N_i / \partial \eta \end{pmatrix} =
\begin{pmatrix} \partial x / \partial \xi  \partial y / \partial \xi \\ \partial x / \partial \eta  \partial y / \partial \eta \end{pmatrix}
\begin{pmatrix} \partial N_i / \partial x \\ \partial N_i / \partial y \end{pmatrix}
= \mathbf{J}
\begin{pmatrix} \partial N_i / \partial x \\ \partial N_i / \partial y \end{pmatrix}
$$
其中 $\mathbf{J}$ 是**[雅可比矩阵](@entry_id:264467) (Jacobian matrix)**，它描述了从父坐标到物理坐标的映射。因此，物理导数可以通过下式计算：
$$
\begin{pmatrix} \partial N_i / \partial x \\ \partial N_i / \partial y \end{pmatrix} = \mathbf{J}^{-1} \begin{pmatrix} \partial N_i / \partial \xi \\ \partial N_i / \partial \eta \end{pmatrix}
$$
这一过程是所有[等参单元](@entry_id:173863)公式的核心，它将抽象的形函数与单元的实际几何形状联系起来，从而使得我们能够在任意形状的单元上进行计算。