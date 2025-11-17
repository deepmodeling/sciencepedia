## 引言
在三维空间的几何探索中，二次曲面不仅因其优美的对称性而引人注目，更因其在科学与工程领域的广泛应用而占据核心地位。然而，要真正驾驭这些[曲面](@entry_id:267450)，我们不能仅仅满足于它们的[代数方程](@entry_id:272665)，而必须深入理解其在每一点的局部几何特性。一个基本问题随之而来：我们如何精确描述一个[曲面](@entry_id:267450)在特定点的“朝向”？这正是切平面与法线概念所要解决的核心知识空白。一个[切平面](@entry_id:136914)如同[曲面](@entry_id:267450)在该点的[局部线性近似](@entry_id:263289)，而[法线](@entry_id:167651)则指明了其最陡峭的增长方向。

本文将系统地引导您掌握二次曲面的[切平面](@entry_id:136914)与法线。我们首先在“原理与机制”一章中，揭示梯度向量作为计算[法向量](@entry_id:264185)的万能钥匙，并运用它来推导[切平面](@entry_id:136914)与法线的方程，解决一系列带有几何约束的经典问题。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将视野扩展到理论之外，探讨这些几何概念如何在光学设计、[材料科学](@entry_id:152226)、计算物理等前沿领域中发挥关键作用。最后，通过“动手实践”部分提供的精选问题，您将有机会亲手应用所学知识，巩固并深化理解。让我们从最基本的原理出发，一步步揭开[二次曲面](@entry_id:264390)局部几何的奥秘。

## 原理与机制

在深入探讨[二次曲面](@entry_id:264390)的[切平面](@entry_id:136914)和法线之前，我们必须首先掌握一个核心的[微分几何](@entry_id:145818)工具：梯度。对于一个由隐[函数方程](@entry_id:199663) $F(x, y, z) = c$ 定义的[曲面](@entry_id:267450)，其中 $c$ 为常数，在[曲面](@entry_id:267450)上任意一点 $P_0(x_0, y_0, z_0)$，该函数的梯度向量 $\nabla F(P_0)$ 提供了一个至关重要的方向信息：它垂直于该点处的[曲面](@entry_id:267450)。这个性质是后续所有讨论的基石。

### 梯度向量：切平面与[法线](@entry_id:167651)的基石

[梯度向量](@entry_id:141180) $\nabla F$ 定义为包含函数 $F$ 对各变量偏导数的向量：
$$ \nabla F(x, y, z) = \left\langle \frac{\partial F}{\partial x}, \frac{\partial F}{\partial y}, \frac{\partial F}{\partial z} \right\rangle $$
在[曲面](@entry_id:267450)上的一点 $P_0(x_0, y_0, z_0)$，梯度向量 $\nabla F(P_0)$ 提供了该点处[曲面](@entry_id:267450)的**[法向量](@entry_id:264185) (normal vector)**。这个向量垂直于所有穿过 $P_0$ 且位于[曲面上的曲线](@entry_id:635690)的切向量，从而定义了[曲面](@entry_id:267450)在该点的“方向”。

有了法向量，我们可以立即定义两个核心的几何对象：

1.  **切平面 (Tangent Plane)**：在点 $P_0$ 处与[曲面](@entry_id:267450)“相切”的平面。它由所有与[法向量](@entry_id:264185) $\nabla F(P_0)$ 正交且穿过 $P_0$ 的向量构成。若令 $\mathbf{n} = \nabla F(P_0) = \langle A, B, C \rangle$ 且 $P(x,y,z)$ 是[切平面](@entry_id:136914)上的任意一点，则向量 $\vec{P_0 P} = \langle x-x_0, y-y_0, z-z_0 \rangle$ 位于[切平面](@entry_id:136914)内，因此与法向量正交。它们的[点积](@entry_id:149019)为零，从而得到[切平面](@entry_id:136914)的方程：
    $$ A(x-x_0) + B(y-y_0) + C(z-z_0) = 0 $$

2.  **[法线](@entry_id:167651) (Normal Line)**：穿过点 $P_0$ 且平行于法向量 $\nabla F(P_0)$ 的直线。它的方向由[法向量](@entry_id:264185)确定，其[参数方程](@entry_id:172360)为：
    $$ \mathbf{L}(t) = \langle x_0, y_0, z_0 \rangle + t \nabla F(P_0) $$

为了具体说明这一过程，考虑一个场景：一个粒子沿直线轨迹运动，我们需要确定在其穿过一个[双曲抛物面](@entry_id:275753)时，该点处的[切平面方程](@entry_id:171837) [@problem_id:2161501]。假设[曲面](@entry_id:267450)由 $z = x^2 - 2y^2$ 给出，粒子的轨迹为 $\mathbf{r}(t) = \langle 1+2t, -1+2t, -5+12t \rangle$。

首先，我们将[曲面](@entry_id:267450)方程写成隐函数形式 $F(x, y, z) = x^2 - 2y^2 - z = 0$。然后，通过将粒子的[参数方程](@entry_id:172360)代入[曲面](@entry_id:267450)方程来寻找交点：
$$ (1+2t)^2 - 2(-1+2t)^2 - (-5+12t) = 0 $$
化简后得到 $t^2 = 1$。若问题规定 $t$ 为正，则我们取 $t=1$。将 $t=1$ 代回[粒子轨迹](@entry_id:204827)方程，得到交点 $P_0 = (3, 1, 7)$。

接下来，我们计算[梯度向量](@entry_id:141180)以找到法向量。
$$ \nabla F(x, y, z) = \langle 2x, -4y, -1 \rangle $$
在交点 $P_0(3, 1, 7)$ 处，法向量为：
$$ \mathbf{n} = \nabla F(3, 1, 7) = \langle 2(3), -4(1), -1 \rangle = \langle 6, -4, -1 \rangle $$
最后，利用[点法式](@entry_id:167023)方程，我们可以写出[切平面](@entry_id:136914)的方程：
$$ 6(x-3) - 4(y-1) - 1(z-7) = 0 $$
整理后得到 $6x - 4y - z = 7$。这个过程清晰地展示了如何从一个隐式定义的[曲面](@entry_id:267450)和一个特定点出发，系统地确定其切平面。

### 几何约束下的特殊点

[切平面](@entry_id:136914)和[法线](@entry_id:167651)的基本定义使我们能够解决更复杂的问题，即在[曲面](@entry_id:267450)上寻找满足特定几何约束的点。这些问题通常转化为关于梯度向量的代数方程组。

#### [法向量](@entry_id:264185)与给定方向平行

一个常见的约束是要求[曲面](@entry_id:267450)在某点的[法向量](@entry_id:264185)平行于一个已知的[方向向量](@entry_id:169562) $\mathbf{v} = \langle L, M, N \rangle$。如果两个向量平行，则其中一个是另一个的标量倍。因此，在待求点 $P_0(x_0, y_0, z_0)$，必须满足：
$$ \nabla F(x_0, y_0, z_0) = k \mathbf{v} $$
其中 $k$ 是一个非零的比例常数。

一个典型的应用场景是，一个探测器在椭球体表面 $\frac{x^2}{a^2} + \frac{y^2}{b^2} + \frac{z^2}{c^2} = 1$ 上航行，需要将其推力器（沿法线方向）对准一个特定的方向 $\mathbf{v} = \langle L, M, N \rangle$ [@problem_id:2161475]。

首先定义 $F(x,y,z) = \frac{x^2}{a^2} + \frac{y^2}{b^2} + \frac{z^2}{c^2} - 1 = 0$。其梯度为：
$$ \nabla F(x, y, z) = \left\langle \frac{2x}{a^2}, \frac{2y}{b^2}, \frac{2z}{c^2} \right\rangle $$
平行条件 $\nabla F = k \mathbf{v}$ 给出三个分量方程：
$$ \frac{2x_0}{a^2} = kL, \quad \frac{2y_0}{b^2} = kM, \quad \frac{2z_0}{c^2} = kN $$
我们可以从中解出点 $P_0$ 的坐标 $(x_0, y_0, z_0)$（用 $k$ 表示）：
$$ x_0 = \frac{kLa^2}{2}, \quad y_0 = \frac{kMb^2}{2}, \quad z_0 = \frac{kNc^2}{2} $$
由于 $P_0$ 必须在[椭球面](@entry_id:165811)上，我们将这些坐标代入椭[球面方程](@entry_id:177405)，以求解 $k$：
$$ \frac{1}{a^2}\left(\frac{kLa^2}{2}\right)^2 + \frac{1}{b^2}\left(\frac{kMb^2}{2}\right)^2 + \frac{1}{c^2}\left(\frac{kNc^2}{2}\right)^2 = 1 $$
$$ \frac{k^2}{4}(L^2 a^2 + M^2 b^2 + N^2 c^2) = 1 \implies k = \pm \frac{2}{\sqrt{L^2 a^2 + M^2 b^2 + N^2 c^2}} $$
两个 $k$ 值对应了椭球面上满足条件的两个点，它们关于[原点对称](@entry_id:172995)。通过这两个点，我们可以进一步计算它们之间的距离等几何量。

#### [法线](@entry_id:167651)穿过原点

一个重要的特殊情况是，[法线](@entry_id:167651)本身穿过坐标原点 $(0,0,0)$。这意味着从原点到[切点](@entry_id:172885) $P_0(x_0, y_0, z_0)$ 的位置向量 $\mathbf{x}_0 = \langle x_0, y_0, z_0 \rangle$ 必须与[法向量](@entry_id:264185) $\nabla F(P_0)$ 平行。也就是说，$\nabla F(P_0)$ 必须与 $\mathbf{x}_0$ 共线：
$$ \nabla F(x_0, y_0, z_0) = k \mathbf{x}_0 $$

让我们考察[单叶双曲面](@entry_id:261150) $\frac{x^2}{a^2} + \frac{y^2}{b^2} - \frac{z^2}{c^2} = 1$ 上的这种情况 [@problem_id:2161482]。其[梯度向量](@entry_id:141180)为 $\nabla F = \langle \frac{2x}{a^2}, \frac{2y}{b^2}, -\frac{2z}{c^2} \rangle$。法线穿过原点的条件是存在一个标量 $\lambda$ (这里用 $\lambda$ 代替 $k$ 以避免混淆)，使得 $\nabla F = \lambda \langle x, y, z \rangle$。
$$ \frac{2x}{a^2} = \lambda x, \quad \frac{2y}{b^2} = \lambda y, \quad -\frac{2z}{c^2} = \lambda z $$
这可以写作：
$$ x\left(\frac{2}{a^2} - \lambda\right) = 0, \quad y\left(\frac{2}{b^2} - \lambda\right) = 0, \quad z\left(-\frac{2}{c^2} - \lambda\right) = 0 $$
为了使点 $(x,y,z)$ 非原点，其至少一个分量不为零。
-   若 $x \neq 0$，则 $\lambda = \frac{2}{a^2}$。
-   若 $y \neq 0$，则 $\lambda = \frac{2}{b^2}$。
-   若 $z \neq 0$，则 $\lambda = -\frac{2}{c^2}$。

由于 $a, b, c$ 都是正数，$\lambda = \frac{2}{a^2}$ 和 $\lambda = \frac{2}{b^2}$ 为正，而 $\lambda = -\frac{2}{c^2}$ 为负。因此，这三个条件是互斥的。此外，如果 $a \neq b$ (如题目所设)，则 $x$ 和 $y$ 不能同时非零。这意味着满足条件的点最多只有一个非零坐标。
-   $y=z=0$：代入[曲面](@entry_id:267450)方程得 $\frac{x^2}{a^2} = 1 \implies x = \pm a$。得到点 $(\pm a, 0, 0)$。
-   $x=z=0$：代入[曲面](@entry_id:267450)方程得 $\frac{y^2}{b^2} = 1 \implies y = \pm b$。得到点 $(0, \pm b, 0)$。
-   $x=y=0$：代入[曲面](@entry_id:267450)方程得 $-\frac{z^2}{c^2} = 1$，这在实数域内无解。
因此，在[单叶双曲面](@entry_id:261150)上，只有四个点的法线穿过原点。

#### [切平面](@entry_id:136914)穿过原点

另一个有趣的约束是要求[切平面](@entry_id:136914)本身穿过原点。如果[切平面方程](@entry_id:171837)为 $\nabla F(P_0) \cdot (\mathbf{x} - \mathbf{x}_0) = 0$，代入原点坐标 $\mathbf{x} = \langle 0, 0, 0 \rangle$ 必须满足方程：
$$ \nabla F(P_0) \cdot (0 - \mathbf{x}_0) = 0 \implies \nabla F(P_0) \cdot \mathbf{x}_0 = 0 $$
这个条件意味着，在切点 $P_0$ 处，[法向量](@entry_id:264185) $\nabla F(P_0)$ 与位置向量 $\mathbf{x}_0$ 相互垂直。

考虑一个一般形式的[二次曲面](@entry_id:264390) $F(x,y,z) = Ax^2 + By^2 + \dots + Gx + Hy + Iz + J = 0$。我们可以将 $F$ 分解为不同次数的齐次部分：$F = F_2 + F_1 + F_0$，其中 $F_2$ 是二次项， $F_1$ 是一次项，$F_0$ 是常数项。根据[欧拉齐次函数定理](@entry_id:186434)，$\mathbf{x} \cdot \nabla F_k = k F_k$。因此，$\mathbf{x} \cdot \nabla F = \mathbf{x} \cdot \nabla F_2 + \mathbf{x} \cdot \nabla F_1 + \mathbf{x} \cdot \nabla F_0 = 2F_2 + F_1$。
切平面穿过原点的条件 $\nabla F(P_0) \cdot \mathbf{x}_0 = 0$ 变为 $2F_2(\mathbf{x}_0) + F_1(\mathbf{x}_0) = 0$。
同时，点 $P_0$ 在[曲面](@entry_id:267450)上，所以 $F(\mathbf{x}_0) = F_2(\mathbf{x}_0) + F_1(\mathbf{x}_0) + F_0 = 0$。
我们可以从第二个方程解出 $F_2 = -F_1 - F_0$，并代入第一个方程：
$$ 2(-F_1 - F_0) + F_1 = 0 \implies -F_1 - 2F_0 = 0 $$
这揭示了一个深刻的结果：所有满足“切平面穿过原点”条件的点，都必须位于一个由 $F_1+2F_0=0$ 定义的平面上。这个平面在[射影几何](@entry_id:156239)中被称为**极平面 (polar plane)**。

例如，对于[曲面](@entry_id:267450) $x^2 + 2y^2 + 3z^2 - 4x - 8y + 6z + 5 = 0$ [@problem_id:2161499]，我们有 $F_1 = -4x - 8y + 6z$ 和 $F_0 = 5$。满足条件的点所在的[平面方程](@entry_id:152977)为：
$$ (-4x - 8y + 6z) + 2(5) = 0 \implies -4x - 8y + 6z + 10 = 0 $$
化简后得到 $2x + 4y - 3z - 5 = 0$。

### [曲面](@entry_id:267450)间的相互作用

[梯度向量](@entry_id:141180)的概念同样适用于分析两个或多个[曲面](@entry_id:267450)之间的几何关系，例如它们如何相交。

#### [曲面](@entry_id:267450)的正交性

两个[曲面](@entry_id:267450) $F(x,y,z)=0$ 和 $G(x,y,z)=0$ 在一个交点 $P_0$ 处**正交 (orthogonal)**，如果它们在该点处的[切平面](@entry_id:136914)相互垂直。这等价于它们的[法向量](@entry_id:264185)在该点处相互正交。数学上，这个条件表示为它们梯度向量的[点积](@entry_id:149019)为零：
$$ \nabla F(P_0) \cdot \nabla G(P_0) = 0 $$
所有满足此条件的交点构成的集合，是两个[曲面](@entry_id:267450)正交相交的轨迹。

例如，考虑以球心为原点的球面 $x^2+y^2+z^2=R^2$。其上任意一点 $P(x,y,z)$ 的[法向量](@entry_id:264185)与位置向量 $(x,y,z)$ 平行。考虑北极点 $P_0(0,0,R)$，其法向量平行于 $z$ 轴，即 $\mathbf{n}_0 = \langle 0,0,1 \rangle$。若要找到球面上所有点 $P$，使其切平面与 $P_0$ 处的切平面正交，我们需求解 $\mathbf{n}_P \cdot \mathbf{n}_0 = 0$ [@problem_id:2161498]。这给出：
$$ \langle x,y,z \rangle \cdot \langle 0,0,1 \rangle = z = 0 $$
这意味着所有满足条件的点都位于平面 $z=0$ 上。这些点与[球面方程](@entry_id:177405) $x^2+y^2+z^2=R^2$ 的交集是 $x^2+y^2=R^2$，即赤道大圆。

在一个更复杂的例子中，一个双曲面 $x^2+y^2-z^2=k^2$ 和一个[抛物面](@entry_id:264713) $x^2+y^2+z=m$ 正交相交 [@problem_id:2161473]。令 $F = x^2+y^2-z^2-k^2$ 和 $G = x^2+y^2+z-m$。它们的梯度为：
$$ \nabla F = \langle 2x, 2y, -2z \rangle, \quad \nabla G = \langle 2x, 2y, 1 \rangle $$
正交条件 $\nabla F \cdot \nabla G = 0$ 给出：
$$ (2x)(2x) + (2y)(2y) + (-2z)(1) = 0 \implies 4x^2 + 4y^2 - 2z = 0 \implies z = 2(x^2+y^2) $$
这个条件本身定义了另一个[抛物面](@entry_id:264713)。正交相交的点必须同时满足三个方程（两个[曲面](@entry_id:267450)方程和正交条件）。通过[联立方程](@entry_id:193238)，我们可以解出这些点所在的特定轨迹，例如一个位于特定高度的圆。

#### [曲面](@entry_id:267450)的相切

两个[曲面](@entry_id:267450) $F=0$ 和 $G=0$ 在一点 $P_0$ **相切 (tangent)**，如果它们在该点共享同一个[切平面](@entry_id:136914)。这等价于它们的法向量在该点平行，即一个[梯度向量](@entry_id:141180)是另一个的标量倍数：
$$ \nabla F(P_0) = \lambda \nabla G(P_0) $$
其中 $\lambda$ 是一个非零标量。

考虑一个球面 $S: x^2+y^2+z^2=7$ 和另一个二次曲面 $Q: x^2+y^2-z^2=k$ 相切的情况 [@problem_id:2161472]。令 $f=x^2+y^2+z^2-7$ 和 $g=x^2+y^2-z^2-k$。它们的梯度是：
$$ \nabla f = \langle 2x, 2y, 2z \rangle, \quad \nabla g = \langle 2x, 2y, -2z \rangle $$
在[切点](@entry_id:172885) $(x_0, y_0, z_0)$，$\nabla g = \lambda \nabla f$ 给出：
$$ 2x_0 = \lambda(2x_0), \quad 2y_0 = \lambda(2y_0), \quad -2z_0 = \lambda(2z_0) $$
-   如果 $x_0$ 或 $y_0$ 不为零，则前两个方程要求 $\lambda=1$。代入第三个方程得到 $-2z_0 = 2z_0 \implies z_0=0$。将 $z_0=0$ 代入两个[曲面](@entry_id:267450)方程，我们得到 $x_0^2+y_0^2=7$ 和 $x_0^2+y_0^2=k$。因此，$k=7$。
-   如果 $x_0=y_0=0$，则[曲面](@entry_id:267450)方程给出 $z_0^2=7$ 和 $-z_0^2=k$，这意味着 $k=-7$。然而，当 $k=-7$ 时，[曲面](@entry_id:267450) $Q$ 是[双叶双曲面](@entry_id:173020)，而不是题目中指定的[单叶双曲面](@entry_id:261150)。因此，该情况被排除。

所以，唯一使[单叶双曲面](@entry_id:261150)与球面相切的可[能值](@entry_id:187992)是 $k=7$。

### 高等主题与延伸

切平面和[法线](@entry_id:167651)的概念还可以引导我们探索[曲面](@entry_id:267450)更深层次的结构特性和它们与其他几何对象的复杂关系。

#### [切平面](@entry_id:136914)与[曲面](@entry_id:267450)的内在性质：[直纹面](@entry_id:276204)

一个[曲面](@entry_id:267450)在某点 $P$ 的性质，可以通过研究该点的切平面与[曲面](@entry_id:267450)本身的交集来揭示。对于大多数[曲面](@entry_id:267450)（如椭球面），这个交集在局部仅仅是点 $P$ 本身。然而，对于某些[曲面](@entry_id:267450)，交集可能是一对直线。具有这种性质的点被称为**[双曲点](@entry_id:272292) (hyperbolic point)**。如果一个[曲面](@entry_id:267450)的所有点都是[双曲点](@entry_id:272292)，则称该[曲面](@entry_id:267450)为**[双直纹面](@entry_id:170336) (doubly ruled surface)**。这意味着[曲面](@entry_id:267450)上任意一点都有两条直线穿过且完全包含于[曲面](@entry_id:267450)之内。[单叶双曲面](@entry_id:261150)和双曲抛物面是[双直纹面](@entry_id:170336)的两个典型例子。

[曲面](@entry_id:267450)是否为[双直纹面](@entry_id:170336)与其[代数结构](@entry_id:137052)密切相关。对于中心二次曲面 $X^T M X = 1$（其中 $X=(x,y,z)^T$，$M$ 为对称矩阵），它是一个[单叶双曲面](@entry_id:261150)的充要条件是矩阵 $M$ 的[特征值](@entry_id:154894)有两个为正，一个为负（即 signature 为 $(2,1)$）。

例如，考虑由 $x^2 + \alpha xy + y^2 - z^2 = 1$ 定义的[二次曲面](@entry_id:264390)族 [@problem_id:2161487]。其对应的矩阵为：
$$ M = \begin{pmatrix} 1  \alpha/2  0 \\ \alpha/2  1  0 \\ 0  0  -1 \end{pmatrix} $$
该[曲面](@entry_id:267450)为非退化的条件是 $\det(M) = -(1 - \alpha^2/4) \neq 0$，即 $\alpha \neq \pm 2$。
要成为[双直纹面](@entry_id:170336)，矩阵 $M$ 的签名需为 $(2,1)$。由于已有一个负[特征值](@entry_id:154894) $-1$，这要求左上角的 $2 \times 2$ 子矩阵 $B = \begin{pmatrix} 1  \alpha/2 \\ \alpha/2  1 \end{pmatrix}$ 是正定的。根据西尔维斯特判据，这要求 $B$ 的主子式均为正，即 $1>0$ 和 $\det(B) = 1-\alpha^2/4 > 0$。后者化简为 $\alpha^2  4$，即 $|\alpha|  2$。因此，参数 $\alpha$ 在区间 $(-2, 2)$ 内取值时，该[曲面](@entry_id:267450)是一个[单叶双曲面](@entry_id:261150)，也就是一个[双直纹面](@entry_id:170336)。

#### 锥面的恒定夹角性质

锥面具有一个显著的几何特性：其上任意一点（非顶点）的切平面与锥面轴线之间的夹角是恒定的。我们可以通过分析一个顶点在原点的圆锥 $z^2 = k(x^2+y^2)$ 来验证这一点 [@problem_id:2161481]。
令 $F(x,y,z) = kx^2 + ky^2 - z^2 = 0$ (假设 $z>0$)。法向量为 $\nabla F = \langle 2kx, 2ky, -2z \rangle$。锥面的轴线是 $z$ 轴，其方向向量为 $\mathbf{v} = \langle 0,0,1 \rangle$。[切平面](@entry_id:136914)与 $xy$ 平面（垂直于轴线）的夹角 $\theta$ 可由它们的法向量的[点积](@entry_id:149019)确定：
$$ \cos\theta = \frac{|\nabla F \cdot \mathbf{v}|}{\|\nabla F\| \|\mathbf{v}\|} = \frac{|-2z|}{\sqrt{(2kx)^2+(2ky)^2+(-2z)^2}} = \frac{2z}{\sqrt{4k^2(x^2+y^2)+4z^2}} $$
利用[曲面](@entry_id:267450)方程 $k(x^2+y^2)=z^2$，我们可以替换掉 $x$ 和 $y$：
$$ \cos\theta = \frac{2z}{\sqrt{4kz^2+4z^2}} = \frac{2z}{\sqrt{4z^2(k+1)}} = \frac{2z}{2z\sqrt{k+1}} = \frac{1}{\sqrt{k+1}} $$
结果是一个只依赖于参数 $k$ 的常数，与点 $(x,y,z)$ 的具体位置无关。这证明了恒定夹角性质。

#### 与[空间曲线](@entry_id:262621)的关联：[密切平面](@entry_id:167179)

当一条[空间曲线](@entry_id:262621) $\mathbf{r}(t)$ 完全位于一个[曲面](@entry_id:267450) $S$ 上时，我们可以研究曲线的几何性质与[曲面](@entry_id:267450)的几何性质之间的关系。曲线在一点 $P = \mathbf{r}(t)$ 的**[密切平面](@entry_id:167179) (osculating plane)** 是包含该点处速度向量 $\mathbf{r}'(t)$ 和加速度向量 $\mathbf{r}''(t)$ 的平面。它是在该点附近与曲线“吻合”得最好的平面。[密切平面](@entry_id:167179)的[法向量](@entry_id:264185)由 $\mathbf{n}_{\text{osc}}(t) = \mathbf{r}'(t) \times \mathbf{r}''(t)$ 给出。

一个自然的问题是：在曲线上的哪些点，曲线的[密切平面](@entry_id:167179)恰好与[曲面](@entry_id:267450)的[切平面](@entry_id:136914)重合？这两个平面重合的条件是它们的法向量平行，即 $\mathbf{n}_{\text{osc}}(t)$ 与[曲面](@entry_id:267450)的梯度 $\nabla F(\mathbf{r}(t))$ 平行。

考虑一个例子，曲线为 $\mathbf{r}(t) = \langle t, t^2, t^3 \rangle$，[曲面](@entry_id:267450)为 $S: xy - y^2 + xz - z = 0$ [@problem_id:2161506]。
首先计算[密切平面](@entry_id:167179)的[法向量](@entry_id:264185)：
$$ \mathbf{r}'(t) = \langle 1, 2t, 3t^2 \rangle, \quad \mathbf{r}''(t) = \langle 0, 2, 6t \rangle $$
$$ \mathbf{n}_{\text{osc}}(t) = \mathbf{r}'(t) \times \mathbf{r}''(t) = \langle 12t^2 - 6t^2, 0 - 6t, 2 - 0 \rangle = \langle 6t^2, -6t, 2 \rangle $$
然后计算[曲面](@entry_id:267450)在 $\mathbf{r}(t)$ 点的[法向量](@entry_id:264185)。令 $F(x,y,z) = xy - y^2 + xz - z$。
$$ \nabla F = \langle y+z, x-2y, x-1 \rangle $$
$$ \mathbf{n}_{S}(t) = \nabla F(t, t^2, t^3) = \langle t^2+t^3, t-2t^2, t-1 \rangle $$
令 $\mathbf{n}_{\text{osc}}(t) = \alpha \mathbf{n}_{S}(t)$，我们得到[方程组](@entry_id:193238)：
$$ 6t^2 = \alpha(t^2+t^3), \quad -6t = \alpha(t-2t^2), \quad 2 = \alpha(t-1) $$
通过解这个关于 $t$ 和 $\alpha$ 的[方程组](@entry_id:193238)，我们可以找到所有满足条件的点。对于此例，解为 $t=0$ 和 $t=2$。这些点代表了曲[线与](@entry_id:177118)[曲面](@entry_id:267450)几何特征高度吻合的特殊位置。