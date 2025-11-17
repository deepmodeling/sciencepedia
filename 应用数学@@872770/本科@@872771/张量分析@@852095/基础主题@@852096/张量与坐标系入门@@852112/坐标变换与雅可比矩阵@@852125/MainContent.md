## 引言
物理学的基本原则之一是自然定律的普适性——它们的数学形式不应因我们选择的观察视角或[坐标系](@entry_id:156346)而改变。然而，从描述直线运动的[笛卡尔坐标系](@entry_id:169789)到描绘[旋转对称](@entry_id:137077)性的球坐标系，不同的[坐标系](@entry_id:156346)为解决特定问题提供了极大的便利。这就引出了一个核心问题：我们如何系统地、精确地在不同[坐标系](@entry_id:156346)之间进行转换，并确保物理量（如矢量和张量）在此过程中得到正确的表述？

本文旨在深入探讨解决这一问题的关键数学工具：**坐标变换与[雅可比矩阵](@entry_id:264467)**。通过学习本文，您将不仅掌握计算和运用[雅可比矩阵](@entry_id:264467)的技巧，更能理解其在现代科学与工程中的深刻意义。

*   在**“原理与机制”**一章中，我们将从第一性原理出发，介绍[雅可比矩阵](@entry_id:264467)作为[坐标变换](@entry_id:172727)[局部线性近似](@entry_id:263289)的定义，并揭示其[行列式](@entry_id:142978)在度量体积变化中的几何直觉。您将学习到它如何成为定义[协变与逆变](@entry_id:189600)[张量变换法则](@entry_id:185176)的基石。
*   接下来，在**“应用与跨学科联系”**一章中，我们将跨出纯数学的范畴，探索[雅可比矩阵](@entry_id:264467)在连续介质力学、狭义相对论、[热力学](@entry_id:141121)和统计学等多个领域的实际应用，展示其作为连接不同学科的统一语言的强大功能。
*   最后，**“动手实践”**部分提供了一系列精心设计的问题，旨在巩固您的理论知识，帮助您将抽象概念应用于解决具体计算问题。

通过这趟旅程，您将建立起对坐标变换的坚实理解，为进一步学习[张量分析](@entry_id:161423)、[微分几何](@entry_id:145818)以及更广泛的理论物理打下至关重要的基础。让我们从理解[雅可比矩阵](@entry_id:264467)的根本原理开始。

## 原理与机制

物理定律的表述不应依赖于我们碰巧选择的特定[坐标系](@entry_id:156346)。从一个[坐标系转换](@entry_id:263003)到另一个[坐标系](@entry_id:156346)的能力是现代物理学和工程学的核心，而雅可比矩阵正是实现这一转换的关键数学工具。本章将深入探讨[雅可比矩阵](@entry_id:264467)的原理和机制，阐明它如何量化坐标变换，并揭示其在向量和[张量变换](@entry_id:183453)中的根本作用。

### 雅可比矩阵：变换的线性近似

想象一下，空间中的一个点可以由一套坐标 $(x^1, x^2, \ldots, x^n)$ 描述。现在，我们引入一套新的坐标 $(y^1, y^2, \ldots, y^n)$，它们与旧坐标通过一组函数关系相关联：
$$ y^j = y^j(x^1, x^2, \ldots, x^n) \quad \text{for } j = 1, \ldots, n $$
这些函数构成了从 $x$ [坐标系](@entry_id:156346)到 $y$ [坐标系](@entry_id:156346)的**[坐标变换](@entry_id:172727)**。

为了理解这种变换的局部行为，我们考虑在旧[坐标系](@entry_id:156346)中一个无穷小的位移 $dx^i$。这个位移会导致新[坐标系](@entry_id:156346)中的相应变化 $dy^j$。根据多元微积分的链式法则，这些变化之间的关系是线性的：
$$ dy^j = \frac{\partial y^j}{\partial x^1} dx^1 + \frac{\partial y^j}{\partial x^2} dx^2 + \cdots + \frac{\partial y^j}{\partial x^n} dx^n = \sum_{i=1}^{n} \frac{\partial y^j}{\partial x^i} dx^i $$
这个关系可以优雅地用矩阵形式表示。我们定义**[雅可比矩阵](@entry_id:264467)** (Jacobian matrix)，记作 $J$，其元素 $(J)_{ji}$ 就是偏导数 $\frac{\partial y^j}{\partial x^i}$。于是，上述[线性关系](@entry_id:267880)变为：
$$ \begin{pmatrix} dy^1 \\ dy^2 \\ \vdots \\ dy^n \end{pmatrix} = \begin{pmatrix} \frac{\partial y^1}{\partial x^1}  \frac{\partial y^1}{\partial x^2}  \cdots  \frac{\partial y^1}{\partial x^n} \\ \frac{\partial y^2}{\partial x^1}  \frac{\partial y^2}{\partial x^2}  \cdots  \frac{\partial y^2}{\partial x^n} \\ \vdots  \vdots  \ddots  \vdots \\ \frac{\partial y^n}{\partial x^1}  \frac{\partial y^n}{\partial x^2}  \cdots  \frac{\partial y^n}{\partial x^n} \end{pmatrix} \begin{pmatrix} dx^1 \\ dx^2 \\ \vdots \\ dx^n \end{pmatrix} $$
因此，雅可比矩阵是在任何给定点上对[非线性](@entry_id:637147)坐标变换的最佳**线性近似**。它捕捉了旧坐标的微小变化如何“拉伸”、“旋转”和“剪切”以产生新坐标的微小变化。

一个经典且重要的例子是从二维极坐标 $(r, \theta)$ 到笛卡尔坐标 $(x, y)$ 的变换 [@problem_id:37798]。变换方程为：
$$ x(r, \theta) = r \cos \theta $$
$$ y(r, \theta) = r \sin \theta $$
要构建从 $(r, \theta)$ 到 $(x, y)$ 的[雅可比矩阵](@entry_id:264467) $J = \frac{\partial(x, y)}{\partial(r, \theta)}$，我们计算所有一阶[偏导数](@entry_id:146280)：
$$ \frac{\partial x}{\partial r} = \cos\theta, \quad \frac{\partial x}{\partial \theta} = -r\sin\theta $$
$$ \frac{\partial y}{\partial r} = \sin\theta, \quad \frac{\partial y}{\partial \theta} = r\cos\theta $$
将这些导数[排列](@entry_id:136432)成矩阵，我们得到：
$$ J = \begin{pmatrix} \frac{\partial x}{\partial r}  \frac{\partial x}{\partial \theta} \\ \frac{\partial y}{\partial r}  \frac{\partial y}{\partial \theta} \end{pmatrix} = \begin{pmatrix} \cos\theta  -r\sin\theta \\ \sin\theta  r\cos\theta \end{pmatrix} $$
这个矩阵精确地描述了在极坐标空间中沿着 $r$ 方向和 $\theta$ 方向的微小移动如何映射到笛卡尔空间中。

同样，在三维空间中，从柱坐标 $(\rho, \phi, z)$ 到[笛卡尔坐标](@entry_id:167698) $(x, y, z)$ 的变换也是一个常见的例子，其变换方程为 $x = \rho \cos(\phi)$，$y = \rho \sin(\phi)$，$z=z$。相应的[雅可比矩阵](@entry_id:264467)的元素将在后续讨论中发挥重要作用 [@problem_id:1500364]。

### [雅可比行列式](@entry_id:137120)：体积元素的度量

如果雅可比矩阵描述了变换的局部拉伸和旋转，那么它的[行列式](@entry_id:142978)，即**雅可比行列式** (Jacobian determinant)，则有一个更为深刻的几何意义：它度量了变换如何改变无穷小的体积（或面积）。

考虑一个 $n$ 维空间中的无穷小[体积元](@entry_id:267802) $dV_x = dx^1 dx^2 \cdots dx^n$。经过[坐标变换](@entry_id:172727)后，这个[体积元](@entry_id:267802)会映射到一个新的无穷小[体积元](@entry_id:267802) $dV_y$。线性代数告诉我们，一个线性变换（由[雅可比矩阵](@entry_id:264467) $J$ 近似）对体积的缩放因子正是其[行列式](@entry_id:142978)的[绝对值](@entry_id:147688)。因此，我们有：
$$ dV_y = |\det(J)| dV_x $$
或者更常见地写作：
$$ dy^1 dy^2 \cdots dy^n = \left| \det\left(\frac{\partial(y^1, \ldots, y^n)}{\partial(x^1, \ldots, x^n)}\right) \right| dx^1 dx^2 \cdots dx^n $$
这个关系是多元积分中换元法的基础。

为了建立直观理解，让我们考虑一个非常简单的变换：三维空间中的[均匀缩放](@entry_id:267671)，这可以模拟材料的均匀[热膨胀](@entry_id:137427) [@problem_id:1500358]。新坐标 $(x', y', z')$ 与旧坐标 $(x, y, z)$ 的关系为：
$$ x' = \lambda x, \quad y' = \lambda y, \quad z' = \lambda z $$
其中 $\lambda$ 是线性膨胀因子。该变换的雅可比矩阵是：
$$ J = \frac{\partial(x', y', z')}{\partial(x, y, z)} = \begin{pmatrix} \lambda  0  0 \\ 0  \lambda  0 \\ 0  0  \lambda \end{pmatrix} $$
其[行列式](@entry_id:142978)为 $\det(J) = \lambda^3$。这完美地符合我们的物理直觉：如果一个物体的所有线性尺寸都乘以因子 $\lambda$，其体积将乘以因子 $\lambda^3$。一个无穷小的立方体体积元 $dxdydz$ 将变为一个体积为 $\lambda^3 dxdydz$ 的新立方体。

当[雅可比行列式](@entry_id:137120)在某一点为零时，坐标变换在该点被称为**奇异的** (singular)。这意味着在该点，[体积元](@entry_id:267802)被压缩为零维度的对象（例如，一个面或一条线），并且变换不再是局部一对一的。一个单一的目标点可能对应于源[坐标系](@entry_id:156346)中的多个甚至无限多个点。

球面[坐标系](@entry_id:156346)提供了一个关于奇异性的绝佳例子 [@problem_id:1500354]。从球面坐标 $(r, \theta, \phi)$ 到笛卡尔坐标 $(x, y, z)$ 的雅可比行列式可以计算得出，其值为 $r^2 \sin\theta$。
$$ \det(J) = r^2 \sin\theta = 0 \quad \Leftrightarrow \quad r=0 \text{ 或 } \sin\theta=0 $$
这个条件对应于笛卡尔空间中的两个位置：
1.  $r=0$：这是坐标原点 $(0,0,0)$。在原点，极角 $\theta$ 和方位角 $\phi$ 都是未定义的。
2.  $\sin\theta=0$：这意味着 $\theta=0$ 或 $\theta=\pi$。这对应于整个 $z$ 轴 ($x=0, y=0$)。在 $z$ 轴上的任何一点（非原点），方位角 $\phi$ 都是未定义的。例如，点 $(x=0, y=0, z=5)$ 可以用 $(r=5, \theta=0)$ 和任意 $\phi$ 值来描述。
因此，在 $z$ 轴上，从球面坐标到笛卡尔坐标的映射不是一对一的，我们称该[坐标系](@entry_id:156346)在 $z$ 轴上是奇异的。

### 雅可比矩阵的性质与运算法则

[雅可比矩阵](@entry_id:264467)遵循一些强大的代数规则，这些规则极大地简化了对复杂变换的分析。

#### [链式法则](@entry_id:190743)

当一个变换是多个连续[变换的复合](@entry_id:149828)时，总变换的雅可比矩阵就是各个变换[雅可比矩阵](@entry_id:264467)的乘积。这个规则被称为**链式法则** (Chain Rule)。如果存在一个从 $\mathbf{x}$ 到 $\mathbf{y}$ 的变换，以及另一个从 $\mathbf{y}$ 到 $\mathbf{z}$ 的变换，那么复合变换 $\mathbf{x} \to \mathbf{z}$ 的雅可比矩阵 $J_{\mathbf{x} \to \mathbf{z}}$ 满足：
$$ J_{\mathbf{x} \to \mathbf{z}} = J_{\mathbf{y} \to \mathbf{z}} J_{\mathbf{x} \to \mathbf{y}} $$
在分量形式中，这表示为：
$$ \frac{\partial z^k}{\partial x^i} = \sum_{j=1}^{n} \frac{\partial z^k}{\partial y^j} \frac{\partial y^j}{\partial x^i} $$
这正是多元微积分中我们熟悉的[链式法则](@entry_id:190743)。

为了清晰地说明这一点，我们可以看一个一维的例子 [@problem_id:1500324]。考虑变换 $y = x^3$ 和 $u = \sin(y)$。
- 从 $x$ 到 $y$ 的[雅可比](@entry_id:264467)“矩阵”（在这种情况下是一个标量）是 $J_{x \to y} = \frac{dy}{dx} = 3x^2$。
- 从 $y$ 到 $u$ 的[雅可比](@entry_id:264467)是 $J_{y \to u} = \frac{du}{dy} = \cos(y)$。
- 复合变换 $u(x) = \sin(x^3)$ 的[雅可比](@entry_id:264467)是 $J_{x \to u} = \frac{du}{dx} = 3x^2 \cos(x^3)$。
我们可以清楚地看到，$J_{x \to u} = (J_{y \to u}|_{y=x^3}) \cdot J_{x \to y}$，验证了链式法则。

[链式法则](@entry_id:190743)在更复杂的场景中显示出其威力，例如在连续介质力学中分析多阶段变形 [@problem_id:1500359]。假设一个初始构型 $\mathbf{x}$ 首先经过一个线性变换 $\mathbf{y} = A\mathbf{x}$（其中 $A$ 是一个常数矩阵），然后经过一个[非线性变换](@entry_id:636115) $\mathbf{z} = \mathbf{z}(\mathbf{y})$。
- $\mathbf{x} \to \mathbf{y}$ 变换的雅可比矩阵就是矩阵 $A$ 本身，即 $J_{\mathbf{y}/\mathbf{x}} = A$。
- $\mathbf{y} \to \mathbf{z}$ 变换的[雅可比矩阵](@entry_id:264467) $J_{\mathbf{z}/\mathbf{y}}$ 则由[偏导数](@entry_id:146280) $\frac{\partial z_k}{\partial y_i}$ 构成。
根据链式法则，复合变换 $\mathbf{x} \to \mathbf{z}$ 的[雅可比矩阵](@entry_id:264467)为 $J_{\mathbf{z}/\mathbf{x}} = J_{\mathbf{z}/\mathbf{y}} J_{\mathbf{y}/\mathbf{x}} = J_{\mathbf{z}/\mathbf{y}} A$。利用[行列式的乘法性质](@entry_id:148055)，总的雅可比行列式为 $\det(J_{\mathbf{z}/\mathbf{x}}) = \det(J_{\mathbf{z}/\mathbf{y}}) \det(A)$，这大大简化了对复合变形中体积变化的计算。

#### 反变换

如果一个[坐标变换](@entry_id:172727)是可逆的，那么从 $y$ [坐标系](@entry_id:156346)回到 $x$ [坐标系](@entry_id:156346)的**反变换**也存在。假设前向变换的雅可比矩阵是 $J$，反变换的[雅可比矩阵](@entry_id:264467)是 $K$。那么 $K$ 与 $J$ 之间有什么关系呢？[@problem_id:1500344]

我们可以将反变换和前向变换复合起来，这会得到一个[恒等变换](@entry_id:264671)（即 $x^i \to x^i$）。[恒等变换](@entry_id:264671)的[雅可比矩阵](@entry_id:264467)显然是单位矩阵 $I$。根据[链式法则](@entry_id:190743)：
$$ J_{\mathbf{x} \to \mathbf{x}} = J_{\mathbf{y} \to \mathbf{x}} J_{\mathbf{x} \to \mathbf{y}} = K J = I $$
同样地，$J_{\mathbf{y} \to \mathbf{y}} = J_{\mathbf{x} \to \mathbf{y}} J_{\mathbf{y} \to \mathbf{x}} = J K = I$。
这表明，反变换的[雅可比矩阵](@entry_id:264467)正是原变换雅可比矩阵的**逆矩阵**：
$$ K = J^{-1} $$
这个优美的结果再次强调了[雅可比矩阵](@entry_id:264467)在坐标变换理论中的核心[代数结构](@entry_id:137052)。

### [雅可比矩阵](@entry_id:264467)：[张量变换](@entry_id:183453)的引擎

张量的精髓在于其分量在[坐标变换](@entry_id:172727)下的特定行为方式。正是[雅可比矩阵](@entry_id:264467)及其逆矩阵的元素，构成了这些变换法则的基石。

#### [协变矢量](@entry_id:263917)（一阶[协变张量](@entry_id:634493)）

一个**[协变矢量](@entry_id:263917)** (covariant vector) 或称**[1-形式](@entry_id:270392)** (one-form) 的分量 $V_j$ 在从[坐标系](@entry_id:156346) $x^j$ 变换到 $\bar{x}^i$ 时，遵循以下法则：
$$ \bar{V}_i = \sum_{j=1}^{n} \frac{\partial x^j}{\partial \bar{x}^i} V_j $$
请注意，这里的变换系数 $\frac{\partial x^j}{\partial \bar{x}^i}$ 是**反变换**（从 $\bar{x}$ 到 $x$）的[雅可比矩阵](@entry_id:264467)的元素。一个典型的[协变矢量](@entry_id:263917)是[标量场的梯度](@entry_id:270765)。

让我们通过一个实例来理解这一点。考虑一个标量势场 $\psi(x, y, z) = C(x^2 + y^2 + z^2)$ [@problem_id:1500332]。在笛卡尔坐标系中，其梯度 $\nabla\psi$ 的分量为：
$$ (V_x, V_y, V_z) = \left(\frac{\partial \psi}{\partial x}, \frac{\partial \psi}{\partial y}, \frac{\partial \psi}{\partial z}\right) = (2Cx, 2Cy, 2Cz) $$
我们想知道在球面坐标 $(r, \theta, \phi)$ 中，这个梯度矢量场的分量 $(\bar{V}_r, \bar{V}_\theta, \bar{V}_\phi)$ 是什么。为此，我们需要从球面到笛卡尔的变换 $x = r \sin\theta \cos\phi$ 等，并计算 $\frac{\partial x}{\partial r}, \frac{\partial x}{\partial \theta}, \ldots$ 等导数。例如，要计算径向分量 $\bar{V}_r$：
$$ \bar{V}_r = \frac{\partial x}{\partial r} V_x + \frac{\partial y}{\partial r} V_y + \frac{\partial z}{\partial r} V_z $$
将笛卡尔梯度分量和[偏导数](@entry_id:146280)代入并化简，会发现一个简洁的结果：$(\bar{V}_r, \bar{V}_\theta, \bar{V}_\phi) = (2Cr, 0, 0)$。这与直接在球面坐标中计算梯度（$r^2 = x^2+y^2+z^2 \Rightarrow \psi = Cr^2$, $\nabla\psi = \frac{\partial\psi}{\partial r}\mathbf{e}_r = 2Cr\mathbf{e}_r$）的结果一致，有力地展示了[协变变换](@entry_id:198397)法则的正确性。

#### [逆变](@entry_id:192290)矢量（一阶[逆变张量](@entry_id:636697)）

与[协变矢量](@entry_id:263917)相对的是**逆变矢量** (contravariant vector)，其分量 $V^j$ 在坐标变换下遵循不同的法则：
$$ \bar{V}^i = \sum_{j=1}^{n} \frac{\partial \bar{x}^i}{\partial x^j} V^j $$
这里的变换系数 $\frac{\partial \bar{x}^i}{\partial x^j}$ 是**前向变换**（从 $x$ 到 $\bar{x}$）的雅可比矩阵的元素。[无穷小位移](@entry_id:202209)矢量 $dx^i$ 就是逆变矢量的原型。

考虑一个二维笛卡尔坐标系 $(x^1, x^2) = (x, y)$ 中的常数矢量场 $V=(V^1, V^2)=(1, 1)$ [@problem_id:1500366]。现在我们引入一个新[坐标系](@entry_id:156346) $(\bar{x}^1, \bar{x}^2) = (u, v)$，定义为 $u = (x^1)^2, v = x^2$。新[坐标系](@entry_id:156346)中的分量 $(\bar{V}^1, \bar{V}^2)$ 是什么？
我们需要计算前向变换的[雅可比矩阵](@entry_id:264467)元素：
$$ \frac{\partial u}{\partial x} = 2x, \quad \frac{\partial u}{\partial y} = 0, \quad \frac{\partial v}{\partial x} = 0, \quad \frac{\partial v}{\partial y} = 1 $$
应用[逆变](@entry_id:192290)变换法则：
$$ \bar{V}^1 = \frac{\partial u}{\partial x} V^1 + \frac{\partial u}{\partial y} V^2 = (2x)(1) + (0)(1) = 2x $$
$$ \bar{V}^2 = \frac{\partial v}{\partial x} V^1 + \frac{\partial v}{\partial y} V^2 = (0)(1) + (1)(1) = 1 $$
最后，将结果用新坐标表示。因为 $u = x^2$（且 $x>0$），我们有 $x = \sqrt{u}$。所以，新[坐标系](@entry_id:156346)中的矢量分量为 $(\bar{V}^1, \bar{V}^2) = (2\sqrt{u}, 1)$。这个例子生动地说明，即使在原始[坐标系](@entry_id:156346)中一个矢量的分量是常数，在经过[非线性](@entry_id:637147)坐标变换后，其在新[坐标系](@entry_id:156346)中的分量也可能依赖于位置。

#### [高阶张量](@entry_id:200122)

这些变换法则可以自然地推广到更高阶的张量。例如，一个二阶[协变张量](@entry_id:634493) $T_{kl}$ 的变换法则为：
$$ \bar{T}_{ij} = \sum_{k,l} \frac{\partial x^k}{\partial \bar{x}^i} \frac{\partial x^l}{\partial \bar{x}^j} T_{kl} $$
它对每个指标都应用一次[协变变换](@entry_id:198397)。度规张量 $g_{ij}$ 就是一个二阶[协变张量](@entry_id:634493)的典范。从平直的[笛卡尔坐标系](@entry_id:169789)（度规为克罗内克符号 $\delta_{kl}$）变换到一个新的[曲线坐标系](@entry_id:172561) $q^i$ 时，新度规的分量 $g_{ij}$ 就是通过上述法则得到的：
$$ g_{ij} = \sum_{k,l} \frac{\partial x^k}{\partial q^i} \frac{\partial x^l}{\partial q^j} \delta_{kl} = \sum_{k=1}^n \frac{\partial x^k}{\partial q^i} \frac{\partial x^k}{\partial q^j} $$
这正是计算[曲线坐标系](@entry_id:172561)中[度规张量](@entry_id:160222)分量的标准公式。例如，在[柱坐标系](@entry_id:266798) $(\rho, \phi, z)$ 中计算分量 $g_{\phi\phi}$ 时 [@problem_id:1500364]，我们需要计算[偏导数](@entry_id:146280) $\frac{\partial x}{\partial \phi}, \frac{\partial y}{\partial \phi}, \frac{\partial z}{\partial \phi}$，然后将它们的平方相加，最终得到 $g_{\phi\phi} = \rho^2$。

### 深入探讨：何为张量，何又非张量？

一个对象是否为张量，并不取决于它有多少个分量或指标，而**完全取决于其分量在坐标变换下是否遵循特定的[张量变换法则](@entry_id:185176)**。任何不遵循这些法则的对象，无论其形式如何，都不是张量。

一个重要的反例是[标量场](@entry_id:151443)的**黑塞矩阵** (Hessian matrix)，其元素为[二阶偏导数](@entry_id:635213) $H_{ij} = \frac{\partial^2 \phi}{\partial x^i \partial x^j}$。它看起来像一个二阶[协变张量](@entry_id:634493)，但它并不是。

我们可以通过一个具体的例子来证明这一点 [@problem_id:1500360]。考虑一个二维[标量场](@entry_id:151443) $\phi(x, y) = x^2+y$ 和一个[非线性](@entry_id:637147)坐标变换 $x = u^2 - v^2, y = 2uv$。
1.  首先，在[笛卡尔坐标](@entry_id:167698)中直接计算黑塞矩阵 $H_{ij}$。我们会得到一个常数矩阵 $H = \begin{pmatrix} 2  0 \\ 0  0 \end{pmatrix}$。
2.  然后，假设 $H_{ij}$ 是一个二阶[协变张量](@entry_id:634493)，我们应用其变换法则计算它在 $(u,v)$ [坐标系](@entry_id:156346)中的 $(1,1)$ 分量，记为 $B_{11} = \sum_{i,j} \frac{\partial x^i}{\partial u} \frac{\partial x^j}{\partial u} H_{ij}$。计算结果为 $B_{11} = 8u^2$。
3.  最后，我们直接在 $(u,v)$ [坐标系](@entry_id:156346)中计算黑塞矩阵的 $(1,1)$ 分量。首先将 $\phi$ 表示为 $u,v$ 的函数 $\phi(u,v) = (u^2-v^2)^2 + 2uv$，然后求[二阶偏导数](@entry_id:635213) $A_{11} = \frac{\partial^2 \phi}{\partial u^2}$。计算结果为 $A_{11} = 12u^2 - 4v^2$。

由于 $A_{11} \neq B_{11}$，这明确地证明了黑塞矩阵不遵循二阶[协变张量](@entry_id:634493)的变换法则。根本原因在于，[二阶导数](@entry_id:144508)的变换法则比张量法则更复杂，它还包含一个涉及[坐标变换](@entry_id:172727)[二阶导数](@entry_id:144508)的附加项（这个附加项与克里斯托费尔符号密切相关，是黎曼几何的核心概念）。这个例子深刻地提醒我们，张量的定义是严格且精确的，而雅可比矩阵正是通往这个精确世界的看门人。