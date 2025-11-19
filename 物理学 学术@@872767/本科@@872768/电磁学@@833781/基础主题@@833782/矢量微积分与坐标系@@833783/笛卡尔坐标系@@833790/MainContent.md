## 引言
在描述和分析复杂的电磁现象时，建立一个精确的数学框架是不可或缺的。[笛卡尔坐标](@entry_id:167698)系，凭借其直观的正交性和恒定的[基矢](@entry_id:199546)量，构成了我们理解[电场](@entry_id:194326)、[磁场](@entry_id:153296)及其相互作用的基石。然而，从抽象的物理概念（如场和源）到能够解决实际问题的具体数学计算，其间存在一道需要跨越的鸿沟。本文旨在系统地填补这一空白，为读者提供一套在[笛卡尔坐标](@entry_id:167698)系中分析电磁问题的完整方法。

文章首先在**“原理与机制”**一章中，详细阐述如何表示矢量场与[标量场](@entry_id:151443)，并介绍[梯度、散度、旋度](@entry_id:269893)等核心[微分算子](@entry_id:140145)以及积分方法，揭示麦克斯韦方程组的微观物理意义。随后，在**“应用与跨学科联系”**一章中，我们将这些工具应用于静电学、[静磁学](@entry_id:140120)和[电动力学](@entry_id:158759)中的经典问题，如镜像法、[波导理论](@entry_id:264627)和[带电粒子运动](@entry_id:262424)，并探讨其与力学及现代物理的联系。最后，通过**“动手实践”**部分，读者将有机会通过解决具体问题来巩固和深化理解。

通过本次学习，你将掌握在电磁学中运用[笛卡尔坐标](@entry_id:167698)系这一基本而强大工具的核心技能。

## 原理与机制

在电磁学中，为了精确描述和分析空间中任意一点的[电场](@entry_id:194326)、[磁场](@entry_id:153296)及其源（[电荷](@entry_id:275494)和电流）的行为，我们必须建立一个[坐标系](@entry_id:156346)。笛卡尔坐标系，或称直角[坐标系](@entry_id:156346)，以其简洁性和普适性，成为我们首选的数学框架。本章将系统地阐述如何在笛卡尔坐标系中表示物理量、运用积分和[微分算子](@entry_id:140145)，并最终揭示[电磁场](@entry_id:265881)的基本原理和内在机制。

### 场的表示与源的[分布](@entry_id:182848)

在三维空间中，一个点的位置由其坐标 $(x, y, z)$ 唯一确定。相应地，一个矢量 $\vec{A}$ 可以分解为沿三个相互垂直的轴的分量：
$$
\vec{A} = A_x \hat{x} + A_y \hat{y} + A_z \hat{z}
$$
其中 $\hat{x}, \hat{y}, \hat{z}$ 是沿 $x, y, z$ 轴的单位矢量。

电磁现象中的物理量通常以场的形式存在。**[标量场](@entry_id:151443)**是在空间每一点都只有一个数值的函数，例如[电势](@entry_id:267554) $V(x, y, z)$。**矢量场**则是在空间每一点都对应一个矢量（即大小和方向）的函数，例如[电场](@entry_id:194326) $\vec{E}(x, y, z)$ 和[磁场](@entry_id:153296) $\vec{B}(x, y, z)$。

这些场的源头是[电荷](@entry_id:275494)和电流。根据其[分布](@entry_id:182848)方式，我们可以定义**[体电荷密度](@entry_id:264747)** $\rho(x, y, z)$（单位体积的[电荷](@entry_id:275494)量）、**面[电荷密度](@entry_id:144672)** $\sigma(x, y)$（单位面积的[电荷](@entry_id:275494)量）和**[线电荷密度](@entry_id:267995)** $\lambda(x)$（单位长度的[电荷](@entry_id:275494)量）。同样，电流也可以用**[体电流密度](@entry_id:268648)** $\vec{J}(x, y, z)$ 来描述，它表示单位时间穿过单位面积的[电荷](@entry_id:275494)量，是一个矢量场。

### 通过积分计算宏观量

为了从微观的密度[分布](@entry_id:182848)计算出宏观的总量，例如总[电荷](@entry_id:275494)、总电流或磁通量，我们需要运用积分。

#### [标量场](@entry_id:151443)的积分：计算总[电荷](@entry_id:275494)

当电荷分布在一个表面上时，如果面电荷密度 $\sigma$ 是不均匀的，总[电荷](@entry_id:275494) $Q$ 就需要通过对整个表面 $S$ 进行[面积分](@entry_id:275394)来求得：
$$
Q = \iint_S \sigma \, dA
$$
在笛卡尔坐标系中，[面积元](@entry_id:263205) $dA$ 通常取为 $dx\,dy$、$dx\,dz$ 或 $dy\,dz$，具体取决于[曲面](@entry_id:267450)在哪个平面上或如何参数化。

作为一个具体的例子，考虑一个位于 $z=0$ 平面、由 $0 \le x \le a$ 和 $0 \le y \le b$ 限定的矩形薄板。假设其面[电荷密度](@entry_id:144672)随 $x$ 坐标线性变化，即 $\sigma(x, y) = kx$，其中 $k$ 是一个常数。为了计算板上的总[电荷](@entry_id:275494)，我们需执行以下[二重积分](@entry_id:198869)：
$$
Q = \int_{0}^{b} \int_{0}^{a} kx \, dx \, dy = k \int_{0}^{b} dy \int_{0}^{a} x \, dx = k \cdot b \cdot \left[ \frac{x^2}{2} \right]_0^a = \frac{kba^2}{2}
$$
这个积分过程体现了将无穷小的[电荷](@entry_id:275494)元 $dq = \sigma \, dA$ 在整个表面上累加的思想。

我们还可以进一步计算这个电荷分布的**电荷中心** $(x_c, y_c)$，它代表了[电荷分布](@entry_id:144400)的等效作用点。其坐标是[电荷](@entry_id:275494)加权的平均位置：
$$
x_c = \frac{1}{Q} \iint_S x \sigma \, dA, \quad y_c = \frac{1}{Q} \iint_S y \sigma \, dA
$$
对于上述矩形板，我们可以计算出其[电荷中心](@entry_id:267066)：
$$
x_c = \frac{1}{Q} \int_0^b \int_0^a x(kx) \, dx \, dy = \frac{k}{Q} \int_0^b dy \int_0^a x^2 \, dx = \frac{k b (a^3/3)}{kba^2/2} = \frac{2a}{3}
$$
$$
y_c = \frac{1}{Q} \int_0^b \int_0^a y(kx) \, dx \, dy = \frac{k}{Q} \left( \int_0^a x \, dx \right) \left( \int_0^b y \, dy \right) = \frac{k(a^2/2)(b^2/2)}{kba^2/2} = \frac{b}{2}
$$
电荷中心位于 $(\frac{2a}{3}, \frac{b}{2})$。这个结果直观地告诉我们，由于电荷密度随 $x$ 增大而增加，[电荷中心](@entry_id:267066)在 $x$ 方向上偏向了[电荷](@entry_id:275494)更密集的一侧（$x=a$），而在 $y$ 方向上则因对称性位于中点。[@problem_id:1787688]

#### 矢量场的积分：计算通量

矢量场的[面积分](@entry_id:275394)，即**通量**，在电磁学中具有核心地位。通量描述了一个矢量场“穿过”一个给定[曲面](@entry_id:267450)的总量。其通用定义为：
$$
\Phi_{\vec{F}} = \iint_S \vec{F} \cdot d\vec{A}
$$
这里的 $d\vec{A}$ 是一个矢量[面积元](@entry_id:263205)，其大小等于微小面积 $dA$，方向垂直于该[面积元](@entry_id:263205)，即 $d\vec{A} = \hat{n} \, dA$，其中 $\hat{n}$ 是法向单位矢量。

一个直接的应用是计算总电流。流过一个[曲面](@entry_id:267450) $S$ 的总电流 $I$ 是[电流密度](@entry_id:190690)矢量 $\vec{J}$ 在该[曲面](@entry_id:267450)上的通量。
$$
I = \iint_S \vec{J} \cdot d\vec{A}
$$
例如，考虑一根沿 $x$ 轴延伸的长直棒，其在 $y-z$ 平面上的[横截面](@entry_id:154995)为 $0 \le y \le a$ 和 $0 \le z \le b$ 的矩形。若棒内的[电流密度](@entry_id:190690)为 $\vec{J} = C z^3 \hat{x}$，其中 $C$ 为常数，那么流过该[横截面](@entry_id:154995)的总电流是多少？这里的[积分曲面](@entry_id:175238)是 $y-z$ 平面上的矩形，其法向指向 $x$ 轴正方向，因此 $d\vec{A} = \hat{x} \, dy \, dz$。总电流的计算如下：
$$
I = \int_0^a \int_0^b (C z^3 \hat{x}) \cdot (\hat{x} \, dy \, dz) = C \int_0^a dy \int_0^b z^3 \, dz = C \cdot a \cdot \frac{b^4}{4} = \frac{Cab^4}{4}
$$
这个例子清楚地展示了如何通[过积分](@entry_id:753033)一个非均匀的矢量场来获得一个宏观物理量。[@problem_id:1570777]

另一个关键的通量是**磁通量** $\Phi_B$，定义为[磁场](@entry_id:153296) $\vec{B}$ 穿过一个[曲面](@entry_id:267450)的通量：
$$
\Phi_B = \iint_S \vec{B} \cdot d\vec{A}
$$
当[磁场](@entry_id:153296) $\vec{B}$ 是均匀的且[曲面](@entry_id:267450) $S$ 是平面时，积分可以简化为 $\Phi_B = \vec{B} \cdot \vec{A}$，其中 $\vec{A}$ 是整个平面的面积矢量。

考虑一个更复杂的情况：一个均匀[磁场](@entry_id:153296) $\vec{B} = B_0(\hat{x} + 2\hat{y} + 3\hat{z})$ 穿过一个由顶点 $V_1 = (L, 0, 0)$, $V_2 = (0, W, 0)$, 和 $V_3 = (0, 0, H)$ 定义的三角形平板。首先，我们需要确定这个三角形的面积矢量 $\vec{A}$。对于由三个顶点矢量 $\vec{r}_1, \vec{r}_2, \vec{r}_3$ 定义的三角形，其面积矢量可以通过两个边矢量的叉乘得到：
$$
\vec{A} = \frac{1}{2} [(\vec{r}_2 - \vec{r}_1) \times (\vec{r}_3 - \vec{r}_1)]
$$
在本例中，$\vec{r}_1 = L\hat{x}$, $\vec{r}_2 = W\hat{y}$, $\vec{r}_3 = H\hat{z}$。两个边矢量为 $\vec{r}_2 - \vec{r}_1 = -L\hat{x} + W\hat{y}$ 和 $\vec{r}_3 - \vec{r}_1 = -L\hat{x} + H\hat{z}$。它们的叉乘是：
$$
(\vec{r}_2 - \vec{r}_1) \times (\vec{r}_3 - \vec{r}_1) = \begin{vmatrix} \hat{x}  \hat{y}  \hat{z} \\ -L  W  0 \\ -L  0  H \end{vmatrix} = WH\hat{x} + LH\hat{y} + WL\hat{z}
$$
因此，面积矢量为 $\vec{A} = \frac{1}{2}(WH\hat{x} + LH\hat{y} + WL\hat{z})$。根据题目要求，其 $z$ 分量需为正，此结果满足条件。现在，我们可以计算磁通量：
$$
\Phi_B = \vec{B} \cdot \vec{A} = B_0(\hat{x} + 2\hat{y} + 3\hat{z}) \cdot \frac{1}{2}(WH\hat{x} + LH\hat{y} + WL\hat{z}) = \frac{B_0}{2}(WH + 2LH + 3WL)
$$
这个计算过程展示了笛卡尔坐标系下矢量运算（特别是叉乘和点乘）在解决实际物理问题中的威力。[@problem_id:1787702]

### [微分算子](@entry_id:140145)：揭示场的局域性质

积分使我们能从微观[分布](@entry_id:182848)得到宏观总量，而微分算子则让我们能够探究场的局域（逐点）行为。在笛卡尔坐标系中，最重要的[微分算子](@entry_id:140145)是**del算子** $\nabla$：
$$
\nabla = \hat{x}\frac{\partial}{\partial x} + \hat{y}\frac{\partial}{\partial y} + \hat{z}\frac{\partial}{\partial z}
$$
$\nabla$ 算子本身不是一个矢量，但它可以作用于标量场或矢量场，产生三种重要的物理量：梯度、[散度和旋度](@entry_id:270881)。

#### 梯度（Gradient）：从势到场

当 $\nabla$ 作用于一个标量场 $V(x, y, z)$ 时，它产生一个矢量场，称为 $V$ 的**梯度**，记作 $\nabla V$：
$$
\nabla V = \frac{\partial V}{\partial x}\hat{x} + \frac{\partial V}{\partial y}\hat{y} + \frac{\partial V}{\partial z}\hat{z}
$$
梯度的方向指向[标量场](@entry_id:151443) $V$ 增长最快的方向，其大小表示该方向上的增长率。在静电学中，[电场](@entry_id:194326) $\vec{E}$ 与[电势](@entry_id:267554) $V$ 之间的关系正是通过梯度来联系的：
$$
\vec{E} = -\nabla V
$$
负号表示[电场](@entry_id:194326)指向[电势](@entry_id:267554)降低最快的方向。

例如，若某区域的[电势](@entry_id:267554)为 $V(x, y, z) = -E_0(x + 2y)$，其中 $E_0$ 是一个正常数。我们可以通过计算梯度的负值来求得对应的[电场](@entry_id:194326)：
$$
\vec{E} = - \left( \frac{\partial V}{\partial x}\hat{x} + \frac{\partial V}{\partial y}\hat{y} + \frac{\partial V}{\partial z}\hat{z} \right) = - \left( (-E_0)\hat{x} + (-2E_0)\hat{y} + 0\hat{z} \right) = E_0\hat{x} + 2E_0\hat{y}
$$
这是一个均匀[电场](@entry_id:194326)，其大小为 $|\vec{E}| = \sqrt{E_0^2 + (2E_0)^2} = E_0\sqrt{5}$。它与 $x$ 轴正方向的夹角 $\theta$ 满足 $\tan\theta = E_y/E_x = 2E_0/E_0 = 2$，因此 $\theta = \arctan(2) \approx 63.4^{\circ}$。这个例子说明了梯度是如何将标量的势场转化为矢量的[力场](@entry_id:147325)。[@problem_id:1570770]

#### 散度（Divergence）：场的源

当 $\nabla$ 与一个矢量场 $\vec{F}$ 作点乘时，得到一个[标量场](@entry_id:151443)，称为 $\vec{F}$ 的**散度**，记作 $\nabla \cdot \vec{F}$：
$$
\nabla \cdot \vec{F} = \frac{\partial F_x}{\partial x} + \frac{\partial F_y}{\partial y} + \frac{\partial F_z}{\partial z}
$$
散度衡量了一个矢量场从某一点“流出”或“汇入”的净程度。正散度表示一个源点，负散度表示一个汇点。

在电学中，[电场的散度](@entry_id:272995)与[电荷密度](@entry_id:144672)直接相关，这便是**[微分形式的高斯定律](@entry_id:267348)**：
$$
\nabla \cdot \vec{E} = \frac{\rho}{\epsilon_0}
$$
其中 $\epsilon_0$ 是[真空介电常数](@entry_id:204253)。这一定律揭示了[电荷](@entry_id:275494)是[电场](@entry_id:194326)的“源”。假设一个静态[电场](@entry_id:194326)由 $\vec{E} = K(2x\hat{x} - y\hat{y} + 5z\hat{z})$ 给出，其中 $K$ 为常数，我们可以通过计算其散度来找到产生该场的[体电荷密度](@entry_id:264747) $\rho$：
$$
\nabla \cdot \vec{E} = \frac{\partial}{\partial x}(2Kx) + \frac{\partial}{\partial y}(-Ky) + \frac{\partial}{\partial z}(5Kz) = 2K - K + 5K = 6K
$$
根据[高斯定律](@entry_id:141493)，$\rho = \epsilon_0 (\nabla \cdot \vec{E}) = 6K\epsilon_0$。这表明该[电场](@entry_id:194326)是由一个均匀的体[电荷分布](@entry_id:144400)产生的。[@problem_id:1787695]

对于[磁场](@entry_id:153296)，一个基本定律是**[高斯磁定律](@entry_id:182942)**，其微分形式为：
$$
\nabla \cdot \vec{B} = 0
$$
这个定律的物理解释是宇宙中不存在**[磁单极子](@entry_id:142817)**——[磁场](@entry_id:153296)线总是闭合的，既无起点也无终点。因此，任何物理上可能的[磁场](@entry_id:153296)，其散度必须处处为零。我们可以利用这一点来检验一个假设的[磁场](@entry_id:153296)是否“合法”。例如，考虑一个假设的[静态磁场](@entry_id:195560) $\vec{B} = C(z\hat{x} + x\hat{y} + y\hat{z})$。其散度为：
$$
\nabla \cdot \vec{B} = \frac{\partial}{\partial x}(Cz) + \frac{\partial}{\partial y}(Cx) + \frac{\partial}{\partial z}(Cy) = 0 + 0 + 0 = 0
$$
由于其散度为零，该场满足[高斯磁定律](@entry_id:182942)，因此它至少在这一点上是物理上可能的。[@problem_id:1787685]

#### 旋度（Curl）：场的环流

当 $\nabla$ 与一个矢量场 $\vec{F}$ 作叉乘时，得到另一个矢量场，称为 $\vec{F}$ 的**旋度**，记作 $\nabla \times \vec{F}$：
$$
\nabla \times \vec{F} = \begin{vmatrix} \hat{x}  \hat{y}  \hat{z} \\ \frac{\partial}{\partial x}  \frac{\partial}{\partial y}  \frac{\partial}{\partial z} \\ F_x  F_y  F_z \end{vmatrix} = \left(\frac{\partial F_z}{\partial y} - \frac{\partial F_y}{\partial z}\right)\hat{x} + \left(\frac{\partial F_x}{\partial z} - \frac{\partial F_z}{\partial x}\right)\hat{y} + \left(\frac{\partial F_y}{\partial x} - \frac{\partial F_x}{\partial y}\right)\hat{z}
$$
旋度描述了矢量场在某一点周围的“涡旋”或“环流”特性。

在磁学中，旋度扮演着双重角色。首先，由于 $\nabla \cdot \vec{B} = 0$ 恒成立，我们可以引入一个**磁矢量势** $\vec{A}$，使得 $\vec{B} = \nabla \times \vec{A}$。这个关系是自动满足[高斯磁定律](@entry_id:182942)的，因为任何[旋度的散度](@entry_id:271562)恒为零（$\nabla \cdot (\nabla \times \vec{A}) \equiv 0$）。

一个重要的特性是，对于给定的[磁场](@entry_id:153296) $\vec{B}$，其矢量势 $\vec{A}$ 并不唯一。例如，对于一个沿 $z$ 轴方向的均匀[磁场](@entry_id:153296) $\vec{B} = B_0 \hat{z}$，以下几个矢量势都是有效的，因为它们的旋度都是 $B_0 \hat{z}$：
*   $\vec{A} = \frac{B_0}{2}(-y\hat{x} + x\hat{y})$ （对称形式）
*   $\vec{A} = B_0 x \hat{y}$
*   $\vec{A} = -B_0 y \hat{x}$
计算其中第一个选项的旋度：
$$
\nabla \times \vec{A} = \left(\frac{\partial}{\partial x}(\frac{B_0}{2}x) - \frac{\partial}{\partial y}(-\frac{B_0}{2}y)\right)\hat{z} = \left(\frac{B_0}{2} - (-\frac{B_0}{2})\right)\hat{z} = B_0\hat{z} = \vec{B}
$$
这种选择 $\vec{A}$ 的灵活性被称为**规范自由度** (gauge freedom)，在高等电磁理论中是一个深刻且重要的概念。[@problem_id:1570766]

其次，[磁场的旋度](@entry_id:261797)与[电流密度](@entry_id:190690)相关，这便是**[安培定律](@entry_id:140092)**的[微分形式](@entry_id:146747)：
$$
\nabla \times \vec{B} = \mu_0 \vec{J}
$$
其中 $\mu_0$ 是[真空磁导率](@entry_id:186031)。这表明，[稳恒电流](@entry_id:271551)是静[磁场](@entry_id:153296)的“旋涡源”。回到之前那个散度为零的假设[磁场](@entry_id:153296) $\vec{B} = C(z\hat{x} + x\hat{y} + y\hat{z})$，我们可以计算其旋度：
$$
\nabla \times \vec{B} = \left(\frac{\partial(Cy)}{\partial y} - \frac{\partial(Cx)}{\partial z}\right)\hat{x} + \left(\frac{\partial(Cz)}{\partial z} - \frac{\partial(Cy)}{\partial x}\right)\hat{y} + \left(\frac{\partial(Cx)}{\partial x} - \frac{\partial(Cz)}{\partial y}\right)\hat{z} = C\hat{x} + C\hat{y} + C\hat{z}
$$
这个非零的旋度意味着该[磁场](@entry_id:153296)是由一个均匀的[体电流密度](@entry_id:268648) $\vec{J} = \frac{1}{\mu_0}(\nabla \times \vec{B}) = \frac{C}{\mu_0}(\hat{x} + \hat{y} + \hat{z})$ 产生的。因此，这个场不仅满足 $\nabla \cdot \vec{B} = 0$，也符合安培定律（只要存在相应的电流源），所以它是物理上完全可能的。[@problem_id:1787685]

### 动态场与[电磁波](@entry_id:269629)

当电场和磁场随时间变化时，它们之间的耦合通过麦克斯韦方程组的另外两个方程来描述。

**[法拉第感应定律](@entry_id:146175)**的微分形式将[电场的旋度](@entry_id:182875)与[磁场](@entry_id:153296)的变化率联系起来：
$$
\nabla \times \vec{E} = - \frac{\partial \vec{B}}{\partial t}
$$
这一定律表明，一个随时间变化的[磁场](@entry_id:153296)会产生一个“涡旋状”的[电场](@entry_id:194326)（即有旋度的[电场](@entry_id:194326)），这是电磁感应现象的微观基础。设想一个空间均匀但时间变化的[磁场](@entry_id:153296) $\vec{B}(t) = B_0 (\frac{t}{\tau})^3 \hat{x}$，其中 $B_0$ 和 $\tau$ 是常数。这个变化的[磁场](@entry_id:153296)会在空间中感生出[电场](@entry_id:194326)。该感应[电场的旋度](@entry_id:182875)为：
$$
\nabla \times \vec{E} = - \frac{\partial}{\partial t} \left( B_0 \frac{t^3}{\tau^3} \hat{x} \right) = - \frac{3B_0t^2}{\tau^3} \hat{x}
$$
即使[磁场](@entry_id:153296)在空间上是均匀的，只要它随时间变化，就会产生一个非保守的、有旋度的[电场](@entry_id:194326)。[@problem_id:1787675]

在没有[电荷](@entry_id:275494)和电流的自由空间中，麦克斯韦方程组可以组合成一个描述[电场和磁场](@entry_id:261347)的**[波动方程](@entry_id:139839)**。例如，对于[磁场](@entry_id:153296) $\vec{B}$，其在一维情况下的波动方程为：
$$
\frac{\partial^2 \vec{B}}{\partial x^2} = \frac{1}{c^2} \frac{\partial^2 \vec{B}}{\partial t^2}
$$
其中 $c = 1/\sqrt{\epsilon_0 \mu_0}$ 是[真空中的光速](@entry_id:272753)。任何描述[电磁波](@entry_id:269629)的函数都必须满足这个方程。

考虑一个沿 $x$ 轴传播的驻波[磁场](@entry_id:153296) $\vec{B}(x, t) = B_0 \sin(kx) \cos(\omega t) \hat{y}$。这里 $k$ 是[波数](@entry_id:172452)，$\omega$ 是[角频率](@entry_id:261565)。我们将它代入波动方程来检验其有效性。首先计算空间[二阶偏导数](@entry_id:635213)：
$$
\frac{\partial^2 \vec{B}}{\partial x^2} = -k^2 [B_0 \sin(kx) \cos(\omega t) \hat{y}] = -k^2 \vec{B}
$$
然后计算时间[二阶偏导数](@entry_id:635213)：
$$
\frac{\partial^2 \vec{B}}{\partial t^2} = -\omega^2 [B_0 \sin(kx) \cos(\omega t) \hat{y}] = -\omega^2 \vec{B}
$$
将这两个结果代入波动方程：
$$
-k^2 \vec{B} = \frac{1}{c^2} (-\omega^2 \vec{B})
$$
为了使该等式对所有 $x$ 和 $t$ 成立，必须有 $k^2 = \omega^2 / c^2$。取[正根](@entry_id:199264)后，我们得到一个基本关系：
$$
\frac{\omega}{k} = c
$$
这表明，[电磁波](@entry_id:269629)的相速度（角频率与[波数](@entry_id:172452)之比）必须等于光速 $c$。这个例子揭示了笛卡尔坐标系下的[偏微分](@entry_id:194612)运算是如何约束[电磁波](@entry_id:269629)的属性的。[@problem_id:1787712]

### 在[非均匀介质](@entry_id:750241)中的应用

[笛卡尔坐标](@entry_id:167698)系的强大之处在于它同样适用于处理介质属性在空间中变化的复杂情况。考虑一个[平行板电容器](@entry_id:266922)，极板位于 $x=0$ 和 $x=d$，其间填充了一种非均匀的[介电材料](@entry_id:147163)，其[介电常数](@entry_id:146714)随位置变化，$\epsilon(x) = \epsilon_0 (1 + x/d)$。

在这种情况下，使用[电位移矢量](@entry_id:197092) $\vec{D}$ 更为方便。在没有自由电荷的介质区域，[高斯定律](@entry_id:141493)写作 $\nabla \cdot \vec{D} = 0$。由于场只随 $x$ 变化，这意味着 $\frac{d D_x}{dx} = 0$，所以 $D_x$ 是一个常数，记为 $D$。

[电场](@entry_id:194326) $\vec{E}$ 与 $\vec{D}$ 通过[本构关系](@entry_id:186508)（constitutive relation）$\vec{D} = \epsilon(x) \vec{E}$ 联系。因此，[电场](@entry_id:194326)是不均匀的：
$$
E_x(x) = \frac{D_x}{\epsilon(x)} = \frac{D}{\epsilon_0 (1 + x/d)}
$$
两极板间的电势差 $V$ 通过对[电场](@entry_id:194326)积分得到：
$$
V = \int_0^d E_x(x) \, dx = \frac{D}{\epsilon_0} \int_0^d \frac{dx}{1 + x/d} = \frac{Dd}{\epsilon_0} [\ln(1 + x/d)]_0^d = \frac{Dd}{\epsilon_0} \ln(2)
$$
极板上的自由面电荷密度 $\sigma_f$ 等于[电位移矢量](@entry_id:197092)的大小 $D$。电容的定义是 $C = Q/V = (\sigma_f A) / V$。因此，单位面积的电容为：
$$
\frac{C}{A} = \frac{\sigma_f}{V} = \frac{D}{V} = \frac{D}{(Dd/\epsilon_0)\ln(2)} = \frac{\epsilon_0}{d \ln(2)}
$$
这个问题综合运用了[高斯定律](@entry_id:141493)、本构关系以及积分，完美展示了如何利用[笛卡尔坐标](@entry_id:167698)系下的微积[分工](@entry_id:190326)具来分析[非均匀介质](@entry_id:750241)中的静电问题，得出了一个与均匀介质情况（$C/A = \epsilon/d$）形式不同但逻辑一致的结果。[@problem_id:1570750]

综上所述，笛卡尔坐标系为我们提供了一套完整而强大的语言和工具集。从简单的矢量表示到复杂的积分与[微分](@entry_id:158718)运算，再到描述动态的波动现象，它构成了我们理解和解决电磁学问题的坚实基础。