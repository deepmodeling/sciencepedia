## 引言
在固体力学领域，精确描述物体的变形是进行[应力分析](@entry_id:168804)和结构设计的基石。当一个物体受到外力作用时，其内部各点会发生相对位移，导致形状和尺寸的改变。然而，位移本身并不能直接反映引起材料内部抵抗力（即应力）的局部变形。关键问题在于如何从复杂的[位移场](@entry_id:141476)中分离出纯粹的“形变”，并滤除不产生应力的刚体平移和转动。[无穷小应变](@entry_id:197162)张量正是为解决这一核心问题而引入的关键物理量，它为线性弹性理论和大多数工程应用提供了简洁而强大的[运动学](@entry_id:173318)基础。

本文旨在为读者构建一个关于[无穷小应变](@entry_id:197162)张量的完整知识体系。通过以下三个章节的深入探讨，你将不仅掌握其数学定义，更能理解其物理内涵和工程价值：

-   **第一章：原理与机制** 将从最基本的位移场出发，系统推导[无穷小应变](@entry_id:197162)张量的定义，阐明其与[位移梯度](@entry_id:165352)、[格林-拉格朗日应变张量](@entry_id:187745)的关系。本章将详细解读[正应变](@entry_id:204633)和剪[应变的物理意义](@entry_id:203292)，并探讨该理论成立的假设前提与关键局限性。

-   **第二章：应用与交叉学科联系** 将展示[无穷小应变](@entry_id:197162)张量如何在平面应变、[平面应力](@entry_id:172193)等经典简化模型中发挥作用，并揭示其如何作为桥梁，连接材料的本构行为（如各向异性、[粘弹性](@entry_id:148045)）与更前沿的理论（如[本征应变](@entry_id:198120)和应变梯度弹性）。

-   **第三章：动手实践** 提供了一系列精心设计的计算问题，引导读者将理论知识应用于具体场景，从基本分量计算到[坐标系](@entry_id:156346)变换，再到与[有限应变理论](@entry_id:176941)的对比分析，旨在通过实践加深对核心概念的理解。

让我们从变形的局部描述开始，深入探索[无穷小应变](@entry_id:197162)张量的世界。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，描述物体变形的关键在于量化其内部各点相对于彼此的位移。虽然[位移场](@entry_id:141476) $\mathbf{u}$ 本身描述了物体从初始构型到当前构型的整体运动，但它并未直接揭示导致应力产生的局部形状变化。为了捕捉这种局部变形，我们必须考察位移场在空间中的变化率，这引导我们引入[位移梯度](@entry_id:165352)和[应变张量](@entry_id:193332)的概念。本章旨在系统地阐述[无穷小应变](@entry_id:197162)张量的定义、物理意义、应用范畴及其数学基础，为[计算固体力学](@entry_id:169583)中的线弹性分析奠定坚实的运动学基础。

### [位移梯度](@entry_id:165352)：变形的局部描述

考虑一个连续体，其物质点在参考构型中的位置由向量 $\mathbf{X}$ 表示。经过变形后，该物[质点](@entry_id:186768)移动到当前构型中的位置 $\mathbf{x}$。位移向量 $\mathbf{u}$ 定义为这两个位置之差：
$$
\mathbf{x} = \mathbf{X} + \mathbf{u}(\mathbf{X})
$$
为了解一个点邻域内的相对变形，我们考察一个从 $\mathbf{X}$ 点出发的无穷小物质[线元](@entry_id:196833) $d\mathbf{X}$。在变形后，这个[线元](@entry_id:196833)变为 $d\mathbf{x}$。通过对变形映射 $\mathbf{x}(\mathbf{X})$ 进行泰勒展开，我们可以建立 $d\mathbf{x}$ 与 $d\mathbf{X}$ 之间的线性关系：
$$
d\mathbf{x} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} d\mathbf{X} = \mathbf{F} d\mathbf{X}
$$
其中，二阶张量 $\mathbf{F}$ 被称为**变形梯度** (deformation gradient)。它将参考构型中的无穷小向量映射到当前构型中的对应向量。将 $\mathbf{x} = \mathbf{X} + \mathbf{u}$ 代入，我们得到：
$$
\mathbf{F} = \frac{\partial (\mathbf{X} + \mathbf{u})}{\partial \mathbf{X}} = \mathbf{I} + \frac{\partial \mathbf{u}}{\partial \mathbf{X}} = \mathbf{I} + \nabla \mathbf{u}
$$
这里的 $\nabla \mathbf{u}$ 是**[位移梯度张量](@entry_id:748571)** (displacement gradient tensor)，其分量为 $(\nabla \mathbf{u})_{ij} = \partial u_i / \partial X_j$。[位移梯度张量](@entry_id:748571) $\nabla \mathbf{u}$ 包含了关于变形的所有局部信息，包括拉伸、剪切和[刚体转动](@entry_id:191086)。

任何一个[二阶张量](@entry_id:199780)都可以唯一地分解为其对称[部分和](@entry_id:162077)反对称部分。对于[位移梯度](@entry_id:165352) $\nabla \mathbf{u}$，这种分解尤为重要：
$$
\nabla \mathbf{u} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^T) + \frac{1}{2}(\nabla \mathbf{u} - (\nabla \mathbf{u})^T)
$$
右边的第一项是[对称张量](@entry_id:148092)，它与物体的形状改变（即应变）直接相关。第二项是[反对称张量](@entry_id:199349)，它描述了物体的无穷小[刚体转动](@entry_id:191086)。

考虑一个仿射位移场 $\mathbf{u}(\mathbf{x}) = \mathbf{A}\mathbf{x} + \mathbf{b}$，其中 $\mathbf{A}$ 是一个常数张量，$\mathbf{b}$ 是一个常数向量。这种位移场对应于均匀变形。其[位移梯度](@entry_id:165352)为 $\nabla \mathbf{u} = \mathbf{A}$。根据上述分解，变形可以分为由 $\mathbf{A}$ 的对称部分 $\frac{1}{2}(\mathbf{A} + \mathbf{A}^T)$ 描述的纯应变和由其反对称部分 $\frac{1}{2}(\mathbf{A} - \mathbf{A}^T)$ 描述的纯转动 。

### [无穷小应变](@entry_id:197162)张量的定义

应变的核心是量化材料纤维长度和角度的变化。一个精确的、适用于任意大变形的应变量是**[格林-拉格朗日应变张量](@entry_id:187745)** (Green-Lagrange strain tensor) $\mathbf{E}$，它通过比较变形前后无穷小[线元](@entry_id:196833)长度的平[方差](@entry_id:200758)来定义：
$$
ds^2 - dS^2 = d\mathbf{X}^T ( \mathbf{F}^T \mathbf{F} - \mathbf{I} ) d\mathbf{X} = 2 d\mathbf{X}^T \mathbf{E} d\mathbf{X}
$$
由此可得，
$$
\mathbf{E} = \frac{1}{2}(\mathbf{F}^T \mathbf{F} - \mathbf{I})
$$
将 $\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$ 代入并展开，我们得到：
$$
\mathbf{E} = \frac{1}{2} \left( (\mathbf{I} + \nabla \mathbf{u})^T (\mathbf{I} + \nabla \mathbf{u}) - \mathbf{I} \right) = \frac{1}{2} \left( \nabla \mathbf{u} + (\nabla \mathbf{u})^T + (\nabla \mathbf{u})^T \nabla \mathbf{u} \right)
$$
这个表达式是完全[非线性](@entry_id:637147)的。

在许多工程应用中，位移和转动都非常小，这构成了**小变形**或**无穷小运动** (infinitesimal kinematics) 的假设。数学上，这意味着[位移梯度](@entry_id:165352)的所有分量的[绝对值](@entry_id:147688)都远小于1，即 $\| \nabla \mathbf{u} \| \ll 1$。在此假设下，$\mathbf{E}$ 表达式中的二次项 $(\nabla \mathbf{u})^T \nabla \mathbf{u}$ 相对于线性项是高阶小量，可以忽略。通过对[格林-拉格朗日应变张量](@entry_id:187745)进行线性化，我们得到了**[无穷小应变](@entry_id:197162)张量** (infinitesimal strain tensor) $\boldsymbol{\varepsilon}$，也称为柯西应变张量：
$$
\boldsymbol{\varepsilon} = \frac{1}{2} \left( \nabla \mathbf{u} + (\nabla \mathbf{u})^T \right)
$$
这个定义表明，[无穷小应变](@entry_id:197162)张量就是位移梯度[张量的对称部分](@entry_id:182434)  。根据定义，$\boldsymbol{\varepsilon}$ 是一个[对称张量](@entry_id:148092)，即 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^T$。

一个关键的性质是，纯[刚体运动](@entry_id:193355)不会产生应变。刚体运动包括平移和转动。
-   对于纯平移，$\mathbf{u} = \mathbf{c}$（常向量），则 $\nabla \mathbf{u} = \mathbf{0}$，因此 $\boldsymbol{\varepsilon} = \mathbf{0}$。
-   对于绕 $z$ 轴的微小[刚体转动](@entry_id:191086)，角度为 $\alpha \ll 1$，位移场可以线性化为 $\mathbf{u} = (-\alpha y, \alpha x, 0)$。其[位移梯度](@entry_id:165352)为：
    $$
    \nabla \mathbf{u} = \begin{pmatrix} 0  -\alpha  0 \\ \alpha  0  0 \\ 0  0  0 \end{pmatrix}
    $$
    这是一个[反对称张量](@entry_id:199349)。计算其对称部分得到 $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^T) = \mathbf{0}$ 。这证实了[无穷小应变](@entry_id:197162)张量确实只度量变形，而滤除了刚体运动的影响。

### 应变分量的物理解释

为了直观地理解应变张量的含义，我们考察其在[笛卡尔坐标系](@entry_id:169789)下的各个分量。设位移场为 $\mathbf{u} = (u_x, u_y, u_z)$，[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 的矩阵形式为：
$$
\boldsymbol{\varepsilon} = 
\begin{pmatrix}
\varepsilon_{xx}  \varepsilon_{xy}  \varepsilon_{xz} \\
\varepsilon_{yx}  \varepsilon_{yy}  \varepsilon_{yz} \\
\varepsilon_{zx}  \varepsilon_{zy}  \varepsilon_{zz}
\end{pmatrix}
=
\begin{pmatrix}
\frac{\partial u_x}{\partial x}  \frac{1}{2}\left(\frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x}\right)  \frac{1}{2}\left(\frac{\partial u_x}{\partial z} + \frac{\partial u_z}{\partial x}\right) \\
\frac{1}{2}\left(\frac{\partial u_y}{\partial x} + \frac{\partial u_x}{\partial y}\right)  \frac{\partial u_y}{\partial y}  \frac{1}{2}\left(\frac{\partial u_y}{\partial z} + \frac{\partial u_z}{\partial y}\right) \\
\frac{1}{2}\left(\frac{\partial u_z}{\partial x} + \frac{\partial u_x}{\partial z}\right)  \frac{1}{2}\left(\frac{\partial u_z}{\partial y} + \frac{\partial u_y}{\partial z}\right)  \frac{\partial u_z}{\partial z}
\end{pmatrix}
$$
由于其对称性 $\varepsilon_{ij} = \varepsilon_{ji}$，这个 $3 \times 3$ 的矩阵只有6个独立分量 。

#### [正应变](@entry_id:204633)与体积变化

对角线上的分量 $\varepsilon_{xx}, \varepsilon_{yy}, \varepsilon_{zz}$ 被称为**[正应变](@entry_id:204633)** (normal strains)。它们描述了材料纤维沿坐标轴方向的伸长或缩短。例如，$\varepsilon_{xx} = \partial u_x / \partial x$ 代表了沿 $x$ 方向的单位长度变化率。

[应变张量](@entry_id:193332)的第一[不变量](@entry_id:148850)，即其迹 $I_1 = \text{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz}$，具有特殊的物理意义。它代表了材料微元的**线性化[体积应变](@entry_id:267252)** (linearized volumetric strain)，即单位体积的变化量。我们可以通过考察变形后单位立方体的体积变化来证明这一点。变形后，边长为1的立方体近似变为边长为 $1+\varepsilon_{xx}$, $1+\varepsilon_{yy}$, $1+\varepsilon_{zz}$ 的长方体，其体积为 $(1+\varepsilon_{xx})(1+\varepsilon_{yy})(1+\varepsilon_{zz})$。在忽略应变分量的二阶及以上乘积项后，体积变化量 $\Delta V / V$ 近似为：
$$
\frac{\Delta V}{V} \approx (1+\varepsilon_{xx})(1+\varepsilon_{yy})(1+\varepsilon_{zz}) - 1 \approx \varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz} = \text{tr}(\boldsymbol{\varepsilon}) = I_1
$$
这一结论也可以从变形梯度[行列式](@entry_id:142978) $J = \det(\mathbf{F})$ 的线性化得到。体积比 $J = \det(\mathbf{I} + \nabla \mathbf{u})$，对于小梯度，有 $J \approx 1 + \text{tr}(\nabla \mathbf{u})$。由于[反对称张量](@entry_id:199349)的迹为零，$\text{tr}(\nabla \mathbf{u}) = \text{tr}(\boldsymbol{\varepsilon} + \boldsymbol{\omega}) = \text{tr}(\boldsymbol{\varepsilon})$。因此，工程体积应变 $J-1$ 在线性近似下等于 $I_1$ 。

#### [剪应变](@entry_id:175241)与角度变化

非对角线上的分量 $\varepsilon_{xy}, \varepsilon_{xz}, \varepsilon_{yz}$ 被称为**[剪应变](@entry_id:175241)** (shear strains)。它们描述了初始时刻相互垂直的两个[线元](@entry_id:196833)之间的夹角变化。

考虑初始时分别沿 $x_i$ 和 $x_j$ 轴的两个线元。变形后，它们之间的夹角将不再是 $\pi/2$。可以证明，这个角度的减小量（即初始角 $\pi/2$ 减去新角度）等于 $2\varepsilon_{ij}$。这个量 $2\varepsilon_{ij}$ 通常被称为**工程[剪应变](@entry_id:175241)** (engineering shear strain)，记为 $\gamma_{ij}$：
$$
\gamma_{ij} = 2\varepsilon_{ij} = \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \quad (i \neq j)
$$
这个关系 $\Delta\theta_{ij} \approx \gamma_{ij}$（其中 $\Delta\theta_{ij}$ 是角度的减小量）为[剪应变](@entry_id:175241)分量提供了清晰的几何解释 。例如，$\gamma_{xy}$ 表示 $xy$ 平面内初始沿 $x$ 轴和 $y$ 轴方向的线元夹角从 $90^\circ$ 变化的程度。一个正的 $\gamma_{xy}$ 对应于该夹角的减小。

### [无穷小应变](@entry_id:197162)理论的局限性

[无穷小应变](@entry_id:197162)理论的基石是假设[位移梯度](@entry_id:165352)很小，从而忽略了[格林-拉格朗日应变](@entry_id:170427)中的二次项 $\frac{1}{2}(\nabla\mathbf{u})^T\nabla\mathbf{u}$。当这一假设不成立时，该理论便会失效。

一个典型的失效场景是**小应变、大转动**问题。例如，[悬臂梁](@entry_id:174096)的大挠度弯曲。梁的[轴向应变](@entry_id:160811)可能很小，但其[截面](@entry_id:154995)的转动角度却可能很大。考虑一个二维平面内的纯转动，其位移场可由 $\mathbf{u}(\mathbf{x}) = \theta(-y, x, 0)$ 来近似描述，其中 $\theta$ 是转动角。如果 $\theta$ 不是小量（例如 $\theta=O(1)$），我们来比较[无穷小应变](@entry_id:197162) $\boldsymbol{\varepsilon}$ 和[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$。
-   [位移梯度](@entry_id:165352)为 $\nabla\mathbf{u} = \begin{pmatrix} 0  -\theta  0 \\ \theta  0  0 \\ 0  0  0 \end{pmatrix}$。
-   [无穷小应变](@entry_id:197162)为 $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T) = \mathbf{0}$。
-   然而，[格林-拉格朗日应变](@entry_id:170427)为 $\mathbf{E} = \boldsymbol{\varepsilon} + \frac{1}{2}(\nabla\mathbf{u})^T\nabla\mathbf{u} = \mathbf{0} + \frac{1}{2}\begin{pmatrix} \theta^2  0  0 \\ 0  \theta^2  0 \\ 0  0  0 \end{pmatrix}$。

可见，[无穷小应变](@entry_id:197162)理论预测变形为零，而[有限应变理论](@entry_id:176941)正确地捕捉到了由于大转动引起的[非线性](@entry_id:637147)效应（伪应变）。两者之差的范数 $\| \mathbf{E} - \boldsymbol{\varepsilon} \|_F = \frac{\sqrt{2}}{2}\theta^2$，表明误差随转动角度的平方增长 。

在计算力学实践中，即使整体位移很小，在**几何[奇异点](@entry_id:199525)**（如凹角）或**接触界面**附近，[位移梯度](@entry_id:165352)也可能变得非常大。这会导致线性化假设在局部失效。因此，在有限元分析中，有必要设置一个诊断标准来检验小应变假设的有效性。一个实用的判据是比较被忽略的二次项和保留的线性项的大小。我们可以定义一个比率 $r$：
$$
r = \frac{\left\| \frac{1}{2}(\nabla \mathbf{u})^T\nabla \mathbf{u} \right\|_F}{\| \boldsymbol{\varepsilon} \|_F}
$$
其中 $\|\cdot\|_F$ 表示 Frobenius 范数。当这个比率 $r$ 超过某个阈值（例如 $0.1$ 到 $0.2$）时，表明二次项不再可以忽略，小应变模型的结果可能不再可靠，需要转向有限变形理论 。

### 高等数学与物理框架

为了更深入地理解应变张量，我们需要考察其背后的数学结构和物理联系。

#### [相容性条件](@entry_id:637057)

我们从位移场 $\mathbf{u}$ 定义了应变场 $\boldsymbol{\varepsilon}$。现在反过来思考一个问题：给定一个对称的、二次连续可微的[张量场](@entry_id:190170) $\boldsymbol{\varepsilon}(\mathbf{x})$，它是否一定能成为某个单值位移场 $\mathbf{u}(\mathbf{x})$ 的应变场？答案是否定的。$\boldsymbol{\varepsilon}$ 的六个分量是通过对 $\mathbf{u}$ 的三个分量求导得到的，因此它们不是完全独立的，必须满足一定的约束条件。

这些约束条件被称为**圣维南相容性方程** (Saint-Venant compatibility equations)。通过对 $\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$ 进行二次求导并利用[偏导数](@entry_id:146280)的[可交换性](@entry_id:263314)（例如 $u_{i,jkl} = u_{i,kjl}$），可以消去[位移场](@entry_id:141476) $u_i$，得到一组只包含应变分量及其[二阶导数](@entry_id:144508)的方程：
$$
\varepsilon_{ij,kl} + \varepsilon_{kl,ij} - \varepsilon_{ik,jl} - \varepsilon_{jl,ik} = 0
$$
这组方程是应变场能够积分得到一个（在相差一个刚体位移的意义上）单值位移场的**必要条件**。在一个**单连通区域**（没有孔洞的区域）内，它们也是**充分条件** 。如果区域是多连通的（例如带孔的板），则除了满足相容性方程外，还需要满足一些关于[环路积分](@entry_id:164828)的附加条件，否则积分出的位移场可能是多值的，这与[位错](@entry_id:157482)等晶体缺陷的连续介质模型有关。此外，由给定的相容应变场积分得到的[位移场](@entry_id:141476)，其解不是唯一的，相差一个任意的无穷小刚体位移 $ \mathbf{c} + \boldsymbol{\omega} \times \mathbf{x} $ (其中 $\mathbf{c}$ 为常向量，$\boldsymbol{\omega}$ 为常数转动向量) 的位移场，都会产生相同的应变场 。

#### 位移场的正则性要求

在现代计算力学中，特别是在有限元法中，我们通常处理的是不满足经典光滑性假设的**弱解**。在这种数学框架下，我们要求位移场及其导数是[可积函数](@entry_id:191199)，而不是处处连续。为了使[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}(\mathbf{x})$ 作为一个“[几乎处处](@entry_id:146631)”有定义的函数场（而非更广义的[分布](@entry_id:182848)）是良定的，[位移梯度](@entry_id:165352) $\nabla \mathbf{u}$ 的分量至少需要是局部可积的。这对应的最小正则性要求是位移场 $\mathbf{u}$ 属于局部[索博列夫空间](@entry_id:141995) $W^{1,1}_{\text{loc}}(\Omega; \mathbb{R}^3)$。这意味着 $\mathbf{u}$ 及其一阶[弱导数](@entry_id:189356)在任何紧[子集](@entry_id:261956)上都是 $L^1$ 可积的 。更强的正则性，如 $\mathbf{u} \in H^1 = W^{1,2}$（在能量泛函中有界）或 $\mathbf{u} \in C^1$（经典解），是充分但非必要的条件。

#### 能量共轭与本构关系

应变张量不仅是[运动学](@entry_id:173318)量，它在材料的本构关系和能量原理中也扮演核心角色。在[等温过程](@entry_id:143096)中，单位体积的内[功率密度](@entry_id:194407)（应力做功的速率）由柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 和速度梯度 $\mathbf{L} = \nabla\mathbf{v}$ 的[点积](@entry_id:149019)给出：$\boldsymbol{\sigma} : \mathbf{L}$。由于动量矩平衡要求柯西[应力张量](@entry_id:148973)是对称的 ($\boldsymbol{\sigma}=\boldsymbol{\sigma}^T$)，而速度梯度可以分解为对称的变形率张量 $\mathbf{D}$ 和反对称的[自旋张量](@entry_id:187346) $\mathbf{W}$，即 $\mathbf{L} = \mathbf{D} + \mathbf{W}$。因此，内[功率密度](@entry_id:194407)可以写作：
$$
\boldsymbol{\sigma} : \mathbf{L} = \boldsymbol{\sigma} : (\mathbf{D} + \mathbf{W}) = \boldsymbol{\sigma} : \mathbf{D} + \boldsymbol{\sigma} : \mathbf{W} = \boldsymbol{\sigma} : \mathbf{D}
$$
其中 $\boldsymbol{\sigma} : \mathbf{W} = 0$ 因为一个[对称张量](@entry_id:148092)和一个[反对称张量](@entry_id:199349)的[双点积](@entry_id:748648)恒为零。对于小应变情况，变形率张量 $\mathbf{D}$ 恰好是[无穷小应变](@entry_id:197162)张量的时间变化率 $\dot{\boldsymbol{\varepsilon}}$。因此，内[功率密度](@entry_id:194407)为 $\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}$。

这表明，应力张量 $\boldsymbol{\sigma}$ 和[应变率张量](@entry_id:266108) $\dot{\boldsymbol{\varepsilon}}$ 在能量上是**共轭**的。这一共轭关系是建立弹性[本构模型](@entry_id:174726)的基础。对于一个[超弹性材料](@entry_id:190241)，存在一个**[应变能密度函数](@entry_id:755490)** (stored energy density function) $\psi(\boldsymbol{\varepsilon})$，使得应力可以由该函数对应变求导得到：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$
这确保了变形过程是路径无关的，且所做的功完全存储为弹性能，没有能量耗散 。

#### [广义坐标](@entry_id:156576)系下的应变

到目前为止的讨论都基于[笛卡尔坐标系](@entry_id:169789)。当处理[曲面](@entry_id:267450)（如壳体）或使用非正交的[曲线坐标系](@entry_id:172561)（如圆柱或[球坐标系](@entry_id:167517)）时，应变的定义需要推广。在广义[曲线坐标系](@entry_id:172561) $x^i$ 中，[基向量](@entry_id:199546) $e_i$ 不再是常数，它们随空间位置变化。[位移梯度](@entry_id:165352) $\nabla \mathbf{u}$ 的计算必须考虑[基向量](@entry_id:199546)的导数。这引入了**[克里斯托费尔符号](@entry_id:159831)** (Christoffel symbols) $\Gamma^k{}_{ij}$，它编码了[基向量](@entry_id:199546)的变化规律。[位移梯度](@entry_id:165352)的分量（协变导数）变为：
$$
(\nabla u)^i{}_j = u^i{}_{;j} = \partial_j u^i + \Gamma^i{}_{jk} u^k
$$
其中 $u^i$ 是位移的[逆变分量](@entry_id:185440)，$\partial_j$ 是对坐标 $x^j$ 的[偏导数](@entry_id:146280)。这个表达式确保了[位移梯度](@entry_id:165352)是一个真正的张量，其在坐标变换下具有正确的变换性质，而[偏导数](@entry_id:146280) $\partial_j u^i$ 本身则不具备这一性质。相应地，[无穷小应变](@entry_id:197162)张量的[协变](@entry_id:634097)分量为：
$$
\varepsilon_{ij} = \frac{1}{2}(u_{i;j} + u_{j;i}) = \frac{1}{2}(\partial_i u_j + \partial_j u_i - 2\Gamma^k{}_{ij} u_k)
$$
其中 $u_i$ 是位移的协变分量。在平直的欧几里得空间中，如果我们采用笛卡尔坐标系，所有的[克里斯托费尔符号](@entry_id:159831)均为零，这些复杂的表达式就退化为我们之前熟悉的形式 。