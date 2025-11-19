## 引言
[麦克斯韦方程组](@entry_id:150940)是经典电磁学的基石，它以无与伦比的优雅统一了电、磁与光的现象。然而，当爱因斯坦的狭义相对论揭示了时空的新本质后，经典形式的麦克斯韦方程与所有惯性系中物理定律形式不变的[相对性原理](@entry_id:271855)之间出现了看似的矛盾。解决这一矛盾，并揭示电磁学深层次的[洛伦兹协变性](@entry_id:161987)，正是本篇文章的核心任务。我们将看到，通过引入四维时空的张量语言，[电场](@entry_id:194326)与[磁场](@entry_id:153296)不再是独立的实体，而是被统一在一个更为基本的对象——电磁场张量之中。

本文旨在系统地介绍[麦克斯韦方程组的张量形式](@entry_id:204782)，带领读者领略其数学上的简洁之美与物理上的深刻内涵。通过学习本文，你将理解电磁理论的相对论性本质。
*   第一章“**原理与机制**”将从基本定义入手，构建电磁场张量与[四维流密度](@entry_id:262568)，并推导出两个核心的张量方程，同时阐明其中蕴含的[电荷](@entry_id:275494)与[能量-动量守恒](@entry_id:194427)定律。
*   第二章“**应用与[交叉](@entry_id:147634)学科联系**”将展示这一强大工具的实际应用，从相对论粒子动力学到理想导体，再到广义相对论中[弯曲时空](@entry_id:159822)下的电磁现象，揭示其在凝聚态物理和天体物理学等领域的广泛影响。
*   最后，“**动手实践**”部分将提供一系列精心设计的问题，帮助你巩固理论知识，并将抽象的张量运算与具体的物理情景联系起来。

现在，让我们一同踏上这段旅程，进入由张量语言描绘的[协变](@entry_id:634097)电磁世界。

## 原理与机制

在狭义相对论的框架下，[电场和磁场](@entry_id:261347)不再是各自独立的实体，而是被统一为时空中的一个单一对象。这种统一不仅是数学上的优雅，更深刻地揭示了电磁现象的内在结构和对称性。本章将系统地阐述[麦克斯韦方程组的张量形式](@entry_id:204782)，从[核心张量](@entry_id:747891)的定义出发，推导其[动力学方程](@entry_id:751029)，并探讨其中蕴含的基本[守恒定律](@entry_id:269268)。

### [电磁场张量](@entry_id:158921) ($F^{\mu\nu}$): 统一[电场](@entry_id:194326)与[磁场](@entry_id:153296)

描述[电磁场](@entry_id:265881)的第一个核心概念是**电磁场张量**（或称**[法拉第张量](@entry_id:158921)**），它是一个二阶[反对称张量](@entry_id:199349)，记作 $F^{\mu\nu}$。在一个惯性参考系中，我们使用时空坐标 $x^\mu = (x^0, x^1, x^2, x^3) = (ct, x, y, z)$，其中 $c$ 是[真空中的光速](@entry_id:272753)。[电磁场张量](@entry_id:158921)的**逆变（contravariant）**形式 $F^{\mu\nu}$ 将[电场](@entry_id:194326)三分量 $\vec{E} = (E_x, E_y, E_z)$ 和[磁场](@entry_id:153296)三分量 $\vec{B} = (B_x, B_y, B_z)$ 组合在一个 $4 \times 4$ 矩阵中：

$$
F^{\mu\nu} = 
\begin{pmatrix}
0  -E_x/c  -E_y/c  -E_z/c \\
E_x/c  0  -B_z  B_y \\
E_y/c  B_z  0  -B_x \\
E_z/c  -B_y  B_x  0
\end{pmatrix}
$$

从这个结构中可以清晰地看到：
- **时空分量** ($F^{0i}$ 和 $F^{i0}$，其中 $i=1,2,3$) 对应于[电场](@entry_id:194326) $\vec{E}$。
- **空间-空间分量** ($F^{ij}$) 对应于[磁场](@entry_id:153296) $\vec{B}$。
- 张量的**反对称性** ($F^{\mu\nu} = -F^{\nu\mu}$) 是其一个基本属性，这直接导致了对角线元素为零。

为了在张量方程中正确地进行缩并，我们还需要引入其**[协变](@entry_id:634097)（covariant）**形式 $F_{\mu\nu}$。这通过使用**[闵可夫斯基度规张量](@entry_id:180802)** $\eta_{\mu\nu}$ 来“降低”指标实现。在本文中，我们采用 $(+,-,-,-)$ 的度规符号约定，此时[度规张量](@entry_id:160222)及其逆矩阵均为：

$$
\eta_{\mu\nu} = \eta^{\mu\nu} = 
\begin{pmatrix}
1  0  0  0 \\
0  -1  0  0 \\
0  0  -1  0 \\
0  0  0  -1
\end{pmatrix}
$$

[协变张量](@entry_id:634493)通过以下关系式获得：$F_{\mu\nu} = \eta_{\mu\alpha}\eta_{\nu\beta}F^{\alpha\beta}$。由于度规是对角的，计算过程简化为 $F_{\mu\nu} = \eta_{\mu\mu}\eta_{\nu\nu}F^{\mu\nu}$（这里不使用爱因斯坦求和约定）。具体来说 [@problem_id:1525342]：
- 时空分量：$F_{0i} = \eta_{00}\eta_{ii}F^{0i} = (1)(-1)F^{0i} = -F^{0i}$。
- 空间-空间分量：$F_{ij} = \eta_{ii}\eta_{jj}F^{ij} = (-1)(-1)F^{ij} = F^{ij}$。

这导致 $F_{\mu\nu}$ 的矩阵形式为：

$$
F_{\mu\nu} = 
\begin{pmatrix}
0  E_x/c  E_y/c  E_z/c \\
-E_x/c  0  -B_z  B_y \\
-E_y/c  B_z  0  -B_x \\
-E_z/c  -B_y  B_x  0
\end{pmatrix}
$$

比较 $F^{\mu\nu}$ 和 $F_{\mu\nu}$，我们发现[电场](@entry_id:194326)分量的符号发生了反转，而[磁场](@entry_id:153296)分量保持不变。这个符号差异在后续的计算中至关重要。

为了将这个抽象的定义与具体的物理情景联系起来，我们考虑一个只有沿 $y$ 轴正方向的均匀静[磁场](@entry_id:153296) $\vec{B} = B_0 \hat{y}$ 的区域。此时，[电场](@entry_id:194326)为零（$\vec{E}=0$）。根据 $F_{\mu\nu}$ 的定义 [@problem_id:1525361]：
- 时空分量 $F_{0i}$ 与[电场](@entry_id:194326)成正比，因此 $F_{0i} = 0$。
- 空间-空间分量由 $F_{ij} = -\epsilon_{ijk}B_k$ 给出（在我们的坐标定义下），其中 $\epsilon_{ijk}$ 是三维[列维-奇维塔符号](@entry_id:193594)。由于 $\vec{B} = (0, B_0, 0)$，我们有 $B_1=0, B_2=B_0, B_3=0$。因此：
  - $F_{13} = -\epsilon_{132}B_2 = -(-1)B_0 = B_0$。
  - $F_{31} = -F_{13} = -B_0$。
  - 其他所有不含 $B_2$ 的空间分量，如 $F_{12}$，均为零。

这具体展示了如何从给定的物理场构建[电磁场张量](@entry_id:158921)的分量。

### 源：[四维流密度](@entry_id:262568) ($J^\mu$)

正如场被统一在一个四维张量中一样，场的源——[电荷](@entry_id:275494)和电流——也被统一在一个称为**[四维流密度](@entry_id:262568)**的[四维矢量](@entry_id:275085) $J^\mu$ 中。它的分量是：

$$
J^\mu = (\rho c, J_x, J_y, J_z) = (\rho c, \vec{J})
$$

其中 $\rho$ 是电荷密度，$\vec{J}$ 是三维电流密度矢量。$J^\mu$ 的引入优美地体现了[电荷密度](@entry_id:144672)和电流密度在相对论中是同一物理实体在不同[参考系](@entry_id:169232)下的不同表现。

一个经典的例子可以阐明这一点 [@problem_id:1525324]。设想一个在自身[静止参考系](@entry_id:262703) $S'$ 中位于 $x'y'$ 平面的无限大薄[电荷](@entry_id:275494)片，其固有的均匀[表面电荷密度](@entry_id:272693)为 $\sigma$。在 $S'$ 系中，[电荷](@entry_id:275494)是静止的，所以三维电流为零。其[四维流密度](@entry_id:262568)为 $J'^\mu = (\rho' c, 0, 0, 0) = (\sigma c \delta(z'), 0, 0, 0)$，其中 $\delta(z')$ 是狄拉克 $\delta$ 函数，表示[电荷](@entry_id:275494)集中在 $z'=0$ 的平面上。

现在，从一个[实验室参考系](@entry_id:166991) $S$ 观察，该[电荷](@entry_id:275494)片以恒定速度 $\vec{v} = v\hat{x}$ 运动。根据[洛伦兹变换](@entry_id:176827)，$J^\mu$ 作为一个四维矢量进行变换。变换后的分量为：
- $J^0 = \gamma(J'^0 + \frac{v}{c}J'^1) = \gamma (\sigma c \delta(z')) = \gamma \sigma c \delta(z)$
- $J^1 = \gamma(J'^1 + \frac{v}{c}J'^0) = \gamma \frac{v}{c} (\sigma c \delta(z')) = \gamma \sigma v \delta(z)$
- $J^2 = J'^2 = 0$
- $J^3 = J'^3 = 0$

其中 $\gamma = (1 - v^2/c^2)^{-1/2}$ 是洛伦兹因子，并且由于沿 $x$ 方向的助推，$z=z'$。在[实验室参考系](@entry_id:166991) $S$ 中，我们测得的[电荷密度](@entry_id:144672)是 $\rho = J^0/c = \gamma \sigma \delta(z)$，电流密度是 $J_x = J^1 = \gamma \sigma v \delta(z)$。这表明，在 $S$ 系中，我们不仅观察到一个因[长度收缩](@entry_id:154351)效应而增加的电荷密度（$\rho = \gamma \rho'$），还观察到一个由[电荷](@entry_id:275494)运动产生的电流。这个例子完美地展示了[电荷](@entry_id:275494)和电流是如何被统一在[四维流](@entry_id:199021) $J^\mu$ 之中的。

### 动力学方程：张量形式的[麦克斯韦方程组](@entry_id:150940)

有了场 ($F^{\mu\nu}$) 和源 ($J^\mu$) 的相对论性描述，我们现在可以将四个麦克斯韦方程写成两个异常简洁的张量方程。

#### 非齐次方程

高斯定律和[安培-麦克斯韦定律](@entry_id:266368)这两个包含源的方程，被合并为如下的**非齐次麦克斯韦方程**:

$$
\partial_\mu F^{\mu\nu} = \mu_0 J^\nu
$$

这里，$\partial_\mu = \frac{\partial}{\partial x^\mu} = (\frac{1}{c}\frac{\partial}{\partial t}, \nabla)$ 是四维梯度算符，$\mu_0$ 是[真空磁导率](@entry_id:186031)。爱因斯坦求和约定在此处被使用，即对重复出现的指标 $\mu$ 进行求和。

这个单一的矢量方程等价于两个经典矢量方程。我们可以通过考察它的不同分量来验证这一点：

- **时间分量 ($\nu=0$)**: 该分量对应于[高斯定律](@entry_id:141493) [@problem_id:1525331]。
  $$
  \partial_\mu F^{\mu 0} = \mu_0 J^0
  $$
  展开左边的求和：
  $$
  \partial_0 F^{00} + \partial_1 F^{10} + \partial_2 F^{20} + \partial_3 F^{30} = \mu_0 (c\rho)
  $$
  代入 $F^{\mu\nu}$ 的分量 ($F^{00}=0, F^{i0} = E_i/c$) 和 $\partial_\mu$ 的定义：
  $$
  0 + \frac{\partial}{\partial x}\left(\frac{E_x}{c}\right) + \frac{\partial}{\partial y}\left(\frac{E_y}{c}\right) + \frac{\partial}{\partial z}\left(\frac{E_z}{c}\right) = \mu_0 c\rho
  $$
  $$
  \frac{1}{c}(\nabla \cdot \vec{E}) = \mu_0 c\rho
  $$
  使用关系式 $c^2 = 1/(\mu_0 \epsilon_0)$，其中 $\epsilon_0$ 是[真空介电常数](@entry_id:204253)，我们得到 $\nabla \cdot \vec{E} = \rho / \epsilon_0$，这正是高斯定律。

- **空间分量 ($\nu=i$, $i=1,2,3$)**: 这些分量对应于[安培-麦克斯韦定律](@entry_id:266368) [@problem_id:1525314]。以 $x$ 分量 ($\nu=1$) 为例：
  $$
  \partial_\mu F^{\mu 1} = \mu_0 J^1
  $$
  $$
  \partial_0 F^{01} + \partial_1 F^{11} + \partial_2 F^{21} + \partial_3 F^{31} = \mu_0 J_x
  $$
  代入 $F^{\mu\nu}$ 的分量 ($F^{01}=-E_x/c, F^{11}=0, F^{21}=B_z, F^{31}=-B_y$)：
  $$
  \frac{1}{c}\frac{\partial}{\partial t}\left(-\frac{E_x}{c}\right) + \frac{\partial}{\partial y}(B_z) - \frac{\partial}{\partial z}(B_y) = \mu_0 J_x
  $$
  $$
  (\nabla \times \vec{B})_x - \frac{1}{c^2}\frac{\partial E_x}{\partial t} = \mu_0 J_x
  $$
  将三个空间分量组合起来，我们得到矢量形式的[安培-麦克斯韦定律](@entry_id:266368)：
  $$
  \nabla \times \vec{B} - \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t} = \mu_0 \vec{J}
  $$

#### 齐次方程

另外两个不含源的麦克斯韦方程（[法拉第感应定律](@entry_id:146175)和[磁高斯定律](@entry_id:182418)）也有其紧凑的张量形式。有两种等价且都富有启发性的表述方式。

- **方法一：对偶张量**

  我们可以定义一个**对偶[电磁场张量](@entry_id:158921)** $G^{\mu\nu}$，其定义为 $G^{\mu\nu} = \frac{1}{2}\epsilon^{\mu\nu\rho\sigma}F_{\rho\sigma}$，其中 $\epsilon^{\mu\nu\rho\sigma}$ 是四维[列维-奇维塔符号](@entry_id:193594)（$\epsilon^{0123}=1$）。其矩阵形式为：

  $$
  G^{\mu\nu} = 
  \begin{pmatrix}
  0  -B_x  -B_y  -B_z \\
  B_x  0  E_z/c  -E_y/c \\
  B_y  -E_z/c  0  E_x/c \\
  B_z  E_y/c  -E_x/c  0
  \end{pmatrix}
  $$

  可以看到，对偶张量是通过在原张量 $F^{\mu\nu}$ 中进行 $\vec{E}/c \to \vec{B}$ 和 $\vec{B} \to -\vec{E}/c$ 的替换得到的。[齐次方程](@entry_id:163650)于是可以写作：

  $$
  \partial_\mu G^{\mu\nu} = 0
  $$

  这个方程同样可以分解。例如，考察其时间分量 $\nu=0$ [@problem_id:1525328]：
  $$
  \partial_\mu G^{\mu 0} = \partial_0 G^{00} + \partial_i G^{i0} = 0
  $$
  由于 $G^{00}=0$ 且 $G^{i0} = B_i$，我们得到 $\partial_i B_i = \nabla \cdot \vec{B} = 0$，这正是[磁高斯定律](@entry_id:182418)，表明[磁单极子](@entry_id:142817)不存在。类似地，其空间分量会导出[法拉第感应定律](@entry_id:146175)。

- **方法二：[四维势](@entry_id:188407)**

  一个更深刻的方法是引入**[四维势](@entry_id:188407)** $A^\mu = (\phi/c, \vec{A})$，其中 $\phi$ 是电标势，$\vec{A}$ 是磁矢势。如果我们将[电磁场张量](@entry_id:158921)定义为[四维势](@entry_id:188407)的“旋度”：

  $$
  F_{\mu\nu} = \partial_\mu A_\nu - \partial_\nu A_\mu
  $$

  那么[齐次方程](@entry_id:163650)将被**自动满足**。这是因为一个数学恒等式，称为**[比安基恒等式](@entry_id:261685)（Bianchi identity）**，在此形式下自然成立 [@problem_id:1525336]：

  $$
  \partial_\lambda F_{\mu\nu} + \partial_\mu F_{\nu\lambda} + \partial_\nu F_{\lambda\mu} = 0
  $$

  我们可以通过直接计算来验证。例如，对于分量 $(\lambda, \mu, \nu) = (1, 2, 3)$：
  $$
  \partial_1 F_{23} + \partial_2 F_{31} + \partial_3 F_{12} = \partial_1(\partial_2 A_3 - \partial_3 A_2) + \partial_2(\partial_3 A_1 - \partial_1 A_3) + \partial_3(\partial_1 A_2 - \partial_2 A_1)
  $$
  重新组合各项，我们得到：
  $$
  (\partial_1\partial_2 A_3 - \partial_2\partial_1 A_3) + (\partial_2\partial_3 A_1 - \partial_3\partial_2 A_1) + (\partial_3\partial_1 A_2 - \partial_1\partial_3 A_2)
  $$
  假设[四维势](@entry_id:188407)是足够光滑的场，根据[克莱罗定理](@entry_id:139814)，[偏导数](@entry_id:146280)的顺序可以交换（例如 $\partial_1\partial_2 = \partial_2\partial_1$）。因此，上式中的每一对括号内的项都相互抵消，结果恒等于零。这个恒等式正是法拉第定律和[磁高斯定律](@entry_id:182418)的紧凑形式。这种表述方式将[齐次方程](@entry_id:163650)的成立归结于场可以由一个更基本的[势场](@entry_id:143025)导出，为[规范场](@entry_id:159627)论奠定了基础。

### 基本原理与[守恒定律](@entry_id:269268)

张量形式不仅统一了方程，其数学结构本身也蕴含了深刻的物理[守恒定律](@entry_id:269268)。

#### [电荷守恒](@entry_id:264158)

电荷守恒是电动力学的一条基本定律，它在张量形式中是理论内在[自洽性](@entry_id:160889)的直接体现。对非[齐次方程](@entry_id:163650) $\partial_\mu F^{\mu\nu} = \mu_0 J^\nu$ 两边同时作用四维散度算符 $\partial_\nu$ [@problem_id:1525357]：

$$
\partial_\nu (\partial_\mu F^{\mu\nu}) = \mu_0 (\partial_\nu J^\nu)
$$

现在我们来考察左边这项 $\partial_\nu \partial_\mu F^{\mu\nu}$。由于普通[偏导数](@entry_id:146280)是可交换的（$\partial_\nu \partial_\mu = \partial_\mu \partial_\nu$），所以算符 $\partial_\nu \partial_\mu$ 对于指标 $\mu, \nu$ 的交换是对称的。然而，[电磁场张量](@entry_id:158921)是反对称的（$F^{\mu\nu} = -F^{\nu\mu}$）。一个对称算符和一个[反对称张量](@entry_id:199349)的缩并恒等于零。证明如下：
$$
\partial_\nu \partial_\mu F^{\mu\nu} = \partial_\mu \partial_\nu F^{\mu\nu} \quad (\text{交换偏导数顺序})
$$
$$
= -\partial_\mu \partial_\nu F^{\nu\mu} \quad (\text{利用 } F \text{ 的反对称性})
$$
通过重新标记[哑指标](@entry_id:188070) $(\mu, \nu) \to (\nu, \mu)$，上式变为：
$$
= -\partial_\nu \partial_\mu F^{\mu\nu}
$$
因此，我们证明了 $\partial_\nu \partial_\mu F^{\mu\nu} = -\partial_\nu \partial_\mu F^{\mu\nu}$，这意味着 $\partial_\nu \partial_\mu F^{\mu\nu} \equiv 0$。

既然方程的左边恒为零，那么右边也必须为零：

$$
\partial_\nu J^\nu = 0
$$

这就是**电荷守恒的[连续性方程](@entry_id:195013)**。展开它，我们得到 $\frac{1}{c}\frac{\partial (c\rho)}{\partial t} + \nabla \cdot \vec{J} = 0$，即 $\frac{\partial \rho}{\partial t} + \nabla \cdot \vec{J} = 0$。这个方程的物理意义是：任何一个体积内[电荷](@entry_id:275494)量的变化率，都等于通过该体积表面的净电流。[电荷](@entry_id:275494)不会凭空产生或消失。

#### [能量-动量守恒](@entry_id:194427)

[电磁场](@entry_id:265881)自身携带能量和动量。这些物理量以及它们在空间中的流动（能流和动量流/应力）被统一在**[电磁应力-能量张量](@entry_id:267456)** $T^{\mu\nu}$ 中。[电磁场](@entry_id:265881)与带电物质之间的能量和动量交换由以下[守恒定律](@entry_id:269268)描述：

$$
\partial_\mu T^{\mu\nu} = -f^\nu
$$

这里，$f^\nu$ 是[电磁场](@entry_id:265881)施加在[电荷](@entry_id:275494)上的**洛伦兹[四维力](@entry_id:273918)密度**，其定义为 $f^\nu = F^{\nu\mu}J_\mu$。负号表示场的能量和动量的减少量等于其转移给物质的量。

让我们考察这个[守恒定律](@entry_id:269268)的时间分量（$\nu=0$），它描述了[能量守恒](@entry_id:140514) [@problem_id:1525363]。
- 左边为 $\partial_\mu T^{\mu 0} = \partial_0 T^{00} + \partial_i T^{i0}$。其中 $T^{00} = u_{em} = \frac{1}{2}\epsilon_0 E^2 + \frac{1}{2\mu_0} B^2$ 是[电磁场](@entry_id:265881)的能量密度，$T^{i0} = S_i/c$ 是能流密度（[坡印廷矢量](@entry_id:269386) $\vec{S} = \frac{1}{\mu_0}(\vec{E} \times \vec{B})$）的分量。因此，左边等于 $\frac{1}{c}(\frac{\partial u_{em}}{\partial t} + \nabla \cdot \vec{S})$。
- 右边为 $-f^0 = -F^{0\mu}J_\mu = -F^{0i}J_i$。根据$F^{\mu\nu}$的定义，$F^{0i} = -E_i/c$。协变分量 $J_i = -J^i$ (其中$J^i$是三维电流$\vec{J}$的分量)。因此，$f^0 = \sum_i F^{0i} J_i = \sum_i (-E_i/c)(-J^i) = \frac{1}{c}\vec{E}\cdot\vec{J}$。[守恒定律](@entry_id:269268)的右边项则为 $-f^0 = -\frac{1}{c}\vec{E}\cdot\vec{J}$。

令两边相等，我们得到：
$$
\frac{1}{c}\left(\frac{\partial u_{em}}{\partial t} + \nabla \cdot \vec{S}\right) = -\frac{1}{c} \vec{E} \cdot \vec{J}
$$
两边同乘以 $c$ 即得：
$$
\frac{\partial u_{em}}{\partial t} + \nabla \cdot \vec{S} = -\vec{J} \cdot \vec{E}
$$

这就是著名的**[坡印廷定理](@entry_id:261580)**的[微分形式](@entry_id:146747)。它是一个[能量平衡方程](@entry_id:191484)：左边第一项是单位体积内场能量的变化率，第二项是流出该体积的能量（能量通量散度）；右边是场对[电荷](@entry_id:275494)做功的[功率密度](@entry_id:194407)的负值。$\vec{J} \cdot \vec{E}$ 项代表了[电磁场](@entry_id:265881)将能量转移给带电物质的速率。这个结果表明，张量形式能够优雅地统一和描述电磁系统的能量动力学。

### [电场](@entry_id:194326)与[磁场](@entry_id:153296)的[协变](@entry_id:634097)定义

到目前为止，我们对电场和磁场的定义似乎都依赖于一个特定的[坐标系](@entry_id:156346)。然而，相对论的核心思想是寻找与观察者无关的物理规律。[电磁场张量](@entry_id:158921) $F^{\mu\nu}$ 本身就是这样一个不依赖于[坐标系](@entry_id:156346)的对象，而我们通常所说的[电场和磁场](@entry_id:261347)，实际上是这个统一的场在特定观察者看来所呈现的不同侧面。

我们可以通过一个观察者的**[四维速度](@entry_id:269673)** $u^\mu$ 来给[电场和磁场](@entry_id:261347)一个[协变](@entry_id:634097)的、与观察者相关的定义。对于一个惯性观察者，其[四维速度](@entry_id:269673)是一个单位时间like矢量，满足 $u_\mu u^\mu = 1$。相对于这个观察者，[电场和磁场](@entry_id:261347)的四维矢量定义如下 [@problem_id:1525329]：

- **[电场](@entry_id:194326)[四维矢量](@entry_id:275085)**: $E^\mu = F^{\mu\nu} u_\nu$
- **[磁场](@entry_id:153296)四维矢量**: $B^\mu = \frac{1}{2} \epsilon^{\mu\nu\rho\sigma} u_\nu F_{\rho\sigma} = G^{\mu\nu}u_\nu$

这些定义的一个至关重要的特性是，由它们定义的 $E^\mu$ 和 $B^\mu$ 在该观察者自身的[静止参考系](@entry_id:262703)中是纯空间的。数学上，这表现为它们都与观察者的[四维速度](@entry_id:269673) $u^\mu$ 正交。我们可以通过计算它们的[标量积](@entry_id:138996)来证明这一点。

- 对于[电场](@entry_id:194326) $E^\mu$：
  $$
  E_\mu u^\mu = (g_{\mu\alpha} E^\alpha) u^\mu = (g_{\mu\alpha} F^{\alpha\nu} u_\nu) u^\mu = u_\alpha F^{\alpha\nu} u_\nu
  $$
  利用 $F^{\alpha\nu}$ 的反对称性 $F^{\alpha\nu} = -F^{\nu\alpha}$：
  $$
  u_\alpha F^{\alpha\nu} u_\nu = -u_\alpha F^{\nu\alpha} u_\nu
  $$
  交换[哑指标](@entry_id:188070) $\alpha \leftrightarrow \nu$：
  $$
  = -u_\nu F^{\alpha\nu} u_\alpha = -u_\alpha F^{\alpha\nu} u_\nu
  $$
  我们得到了 $E_\mu u^\mu = -E_\mu u^\mu$，这必然意味着 $E_\mu u^\mu = 0$。

- 对于[磁场](@entry_id:153296) $B^\mu$：
  $$
  B_\mu u^\mu = u_\mu B^\mu = u_\mu \left(\frac{1}{2} \epsilon^{\mu\nu\rho\sigma} u_\nu F_{\rho\sigma}\right) = \frac{1}{2} \epsilon^{\mu\nu\rho\sigma} u_\mu u_\nu F_{\rho\sigma}
  $$
  张量 $\epsilon^{\mu\nu\rho\sigma}$ 对于指标 $\mu, \nu$ 的交换是反对称的，而张量 $u_\mu u_\nu$ 对于这两个指标的交换是对称的。一个[反对称张量](@entry_id:199349)和一个[对称张量](@entry_id:148092)在这些指标上的缩并结果恒为零。因此，$B_\mu u^\mu = 0$。

这两个结果 ($E_\mu u^\mu = 0$ 和 $B_\mu u^\mu = 0$) 具有深刻的物理意义。它们表明，对于任何观察者，其测量到的电场和磁场（作为[四维矢量](@entry_id:275085)）都位于与自身时间方向正交的“瞬时空间”中。这为“[电场](@entry_id:194326)”和“[磁场](@entry_id:153296)”这两个依赖于观察者的概念，提供了一个严谨而普适的相对论性定义，并再次强调了 $F^{\mu\nu}$ 作为独立于观察者的、更基本的物理实在的地位。