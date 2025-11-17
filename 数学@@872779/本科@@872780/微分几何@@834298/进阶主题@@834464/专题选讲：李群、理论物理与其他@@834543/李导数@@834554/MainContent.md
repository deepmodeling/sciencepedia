## 引言
在探索弯曲空间和[流形](@entry_id:153038)的几何学时，一个核心问题是如何描述各种物理量或几何对象的变化。[协变导数](@entry_id:152476)提供了一种在空间中沿特定方向衡量变化的方法，但它并非唯一的方式。当我们关注的不再是[固定点](@entry_id:156394)的变化，而是跟随一种“流动”（如水流或系统随时间的演化）时所经历的变化，我们需要一种新的[微分](@entry_id:158718)工具。这个工具就是**[李导数](@entry_id:171745)（Lie derivative）**，它是现代微分几何和理论物理中不可或缺的基石。

本文旨在系统地阐明李导数的概念，填补仅依赖[协变导数](@entry_id:152476)所留下的认知空白。它解决了如何精确量化一个[张量场](@entry_id:190170)被另一个[矢量场的流](@entry_id:180235)“拖拽”时所产生的变化这一根本问题。通过学习本文，读者将掌握一种与对称性、守恒律和几何形变紧密相连的强大语言。

文章将分为三个核心部分展开：第一章“**原理与机制**”将从直观的“拖曳”思想出发，建立李导数对[标量场](@entry_id:151443)、矢量场（李括号）和微分形式的严格定义，并揭示其与流的非对易性的深刻几何联系。第二章“**应用与交叉学科联系**”将展示李导数如何在物理学中描述[对称性与守恒律](@entry_id:160300)（如[Killing场](@entry_id:188681)和[诺特定理](@entry_id:145690)），在[连续介质力学](@entry_id:155125)中刻画形变，并在控制理论等领域发挥作用。最后，在“**动手实践**”部分，读者将通过具体计算问题，将理论知识转化为解决实际几何与物理问题的能力。

## 原理与机制

在[微分几何](@entry_id:145818)中，我们经常需要量化一个几何对象（如标量场、矢量场或张量场）如何在一个点附近变化。[协变导数](@entry_id:152476)提供了一种方法，用于衡量当我们在特定方向上进行[无穷小位移](@entry_id:202209)时张量的变化率。然而，还有另一种截然不同但同样重要的变化概念，它与矢量场的“流”密切相关。这就是**李导数（Lie derivative）**。

[李导数](@entry_id:171745)的核心思想是衡量一个[张量场](@entry_id:190170)沿着另一个矢量场的[积分曲线](@entry_id:161858)（或称“流”）被“拖曳”时的变化。想象一下，一条河流（由矢量场 $X$ 描述其速度）中溶解着一种化学物质（由[标量场](@entry_id:151443) $f$ 描述其浓度）。要了解一个随波逐流的观察者感受到的浓度变化率，我们不能简单地在空间中的一个[固定点](@entry_id:156394)测量变化，而必须比较观察者在不同时刻所处位置的浓度。李导数正是将这一物理直觉精确化的数学工具。它通过比较一个点 $p$ 处的张量值与被流带到 $p$ 点的邻近点上的张量值（经过适当的“[拉回](@entry_id:160816)”操作）来定义变化。

### [标量场](@entry_id:151443)的李导数

我们从最简单的情形开始：一个光滑标量函数（或0阶张量场）$f: M \to \mathbb{R}$ 在一个光滑矢量场 $X$ 方向上的[李导数](@entry_id:171745)。设 $\phi_t^X$ 是矢量场 $X$ 的流，它将[流形](@entry_id:153038) $M$ 上的点 $p$ 沿着 $X$ 的[积分曲线](@entry_id:161858)移动时间 $t$，得到点 $\phi_t^X(p)$。那么，函数 $f$ 沿 $X$ 的李导数 $\mathcal{L}_X f$ 在点 $p$ 的值被定义为当一个点从 $p$ 沿着流移动时 $f$ 值的[瞬时变化率](@entry_id:141382)：

$$
(\mathcal{L}_X f)(p) = \lim_{t \to 0} \frac{f(\phi_t^X(p)) - f(p)}{t}
$$

这正是函数 $f$ 在 $X$ 方向上的[方向导数](@entry_id:189133)的定义。因此，对于[标量场](@entry_id:151443)，$\mathcal{L}_X f$ 就是 $X$ 作用在 $f$ 上的结果：

$$
\mathcal{L}_X f = X(f)
$$

在[局部坐标](@entry_id:181200) $(x^1, \dots, x^n)$ 中，如果 $X = \sum_i X^i \frac{\partial}{\partial x^i}$，那么 $\mathcal{L}_X f = \sum_i X^i \frac{\partial f}{\partial x^i}$。

例如，考虑一个在柱坐标 $(\rho, \phi, z)$ 下描述的物理系统，其中一个[标量场](@entry_id:151443) $f(\rho, \phi, z) = C \rho^{2} \cos(k \phi)$ 描述某个[守恒量](@entry_id:150267)。系统的演化由矢量场 $X = v_{0} \frac{\rho}{R} \frac{\partial}{\partial \rho} + \omega \frac{\partial}{\partial \phi}$ 描述。要计算当 $f$ 沿着流 $X$ 被输运时的变化率，我们只需计算李导数 $\mathcal{L}_X f = X(f)$ [@problem_id:1553883]。根据定义：

$$
\mathcal{L}_X f = \left(v_{0} \frac{\rho}{R} \frac{\partial}{\partial \rho} + \omega \frac{\partial}{\partial \phi}\right) (C \rho^{2} \cos(k \phi))
$$
$$
= v_{0} \frac{\rho}{R} (2C\rho \cos(k\phi)) + \omega (-Ck\rho^2 \sin(k\phi))
$$
$$
= C \rho^{2} \left( \frac{2 v_{0}}{R} \cos(k \phi) - k \omega \sin(k \phi) \right)
$$

这个结果描述了随流运动的观察者所测得的 $f$ 值的瞬时变化。

### 矢量场的李导数：李括号

对于矢量场，情况变得更加复杂。为了比较点 $p$ 处的矢量 $Y(p)$ 与点 $q = \phi_t^X(p)$ 处的矢量 $Y(q)$，我们不能直接相减，因为它们位于不同点的切空间中。我们需要一种方法将 $Y(q)$ “带回”到 $p$ 点的[切空间](@entry_id:199137)。流 $\phi_t^X$ 的[微分](@entry_id:158718)映射 $(d\phi_t^X)_p: T_p M \to T_q M$ 可以将矢量从 $p$ 推向 $q$。它的逆过程，即“[拉回](@entry_id:160816)”操作，是通过其逆[映射的微分](@entry_id:269524) $(d\phi_{-t}^X)_q: T_q M \to T_p M$ 来实现的。这个[微分](@entry_id:158718)映射也常记作 $(\phi_{-t}^X)_*$。

因此，矢量场 $Y$ 相对于 $X$ 的[李导数](@entry_id:171745) $\mathcal{L}_X Y$ 定义为：

$$
(\mathcal{L}_X Y)(p) = \lim_{t \to 0} \frac{(\phi_{-t}^X)_* Y(\phi_t^X(p)) - Y(p)}{t}
$$

这个定义虽然直观，但在计算上并不方便。一个核心的结论是，这个看似复杂的操作等价于两个矢量场的**[李括号](@entry_id:636461)（Lie bracket）**：

$$
\mathcal{L}_X Y = [X, Y]
$$

李括号 $[X, Y]$ 本身也是一个矢量场，它作用在一个光滑函数 $f$ 上的效果定义为 $[X, Y](f) = X(Y(f)) - Y(X(f))$。在[局部坐标](@entry_id:181200)中，如果 $X = X^i \frac{\partial}{\partial x^i}$ 和 $Y = Y^j \frac{\partial}{\partial x^j}$（使用爱因斯坦求和约定），则李括号的第 $k$ 个分量为：

$$
([X, Y])^k = X^i \frac{\partial Y^k}{\partial x^i} - Y^i \frac{\partial X^k}{\partial x^i}
$$

这个公式为我们提供了一个直接计算李导数的有效方法。例如，在 $\mathbb{R}^2$ 上给定两个矢量场 $X = (x^2 + y) \frac{\partial}{\partial x} + (xy) \frac{\partial}{\partial y}$ 和 $Y = y \frac{\partial}{\partial x} - x \frac{\partial}{\partial y}$ [@problem_id:1679287]。我们可以利用上述分量公式计算它们的李括号 $[X, Y]$。设 $[X, Y] = Z^1 \frac{\partial}{\partial x} + Z^2 \frac{\partial}{\partial y}$，其分量为：

$$
Z^1 = X^x \frac{\partial Y^x}{\partial x} + X^y \frac{\partial Y^x}{\partial y} - \left(Y^x \frac{\partial X^x}{\partial x} + Y^y \frac{\partial X^x}{\partial y}\right)
$$
$$
= (x^2+y)(0) + (xy)(1) - \left(y(2x) + (-x)(1)\right) = xy - 2xy + x = x(1-y)
$$

$$
Z^2 = X^x \frac{\partial Y^y}{\partial x} + X^y \frac{\partial Y^y}{\partial y} - \left(Y^x \frac{\partial X^y}{\partial x} + Y^y \frac{\partial X^y}{\partial y}\right)
$$
$$
= (x^2+y)(-1) + (xy)(0) - \left(y(y) + (-x)(x)\right) = -x^2 - y - y^2 + x^2 = -y - y^2
$$

因此，矢量场 $Y$ 沿着 $X$ 的流的变化率由新的矢量场 $\mathcal{L}_X Y = [X, Y] = x(1-y) \frac{\partial}{\partial x} - (y+y^2) \frac{\partial}{\partial y}$ 给出。

### [李括号](@entry_id:636461)的几何诠释

[李括号](@entry_id:636461) $[X, Y]$ 具有深刻的几何意义：它衡量了两个[矢量场的流](@entry_id:180235)在多大程度上**不对易（fail to commute）**。如果 $[X, Y] = 0$，那么沿 $X$ 流动一段参数时间 $s$，再沿 $Y$ 流动一段参数时间 $t$，与先沿 $Y$ 流动时间 $t$ 再沿 $X$ 流动时间 $s$ 到达的是同一点。

当 $[X, Y] \neq 0$ 时，这个过程会产生一个位移。考虑从点 $p_0$ 出发，依次执行四步操作：沿 $X$ 流动时间 $s$，再沿 $Y$ 流动时间 $t$，然后沿 $X$ 的反方向流动时间 $s$（即沿 $-X$ 流动时间 $s$），最后沿 $Y$ 的反方向流动时间 $t$。这个过程的最终点 $p_f$ 由复合流给出：

$$
p_f = (\phi_{-t}^Y \circ \phi_{-s}^X \circ \phi_t^Y \circ \phi_s^X)(p_0)
$$

当 $s$ 和 $t$ 都很小时，这个闭合路径描绘出一个无穷小的“平行四边形”。如果流是可交换的，那么 $p_f$ 将精确地回到 $p_0$。然而，在一般情况下，终点与起点之间存在一个位移 $\vec{D} = p_f - p_0$。这个位移的最低阶非零项正比于 $st$，其系数恰好是李括号 $[X, Y]$ 在 $p_0$ 的值：

$$
p_f - p_0 = st [X, Y](p_0) + \mathcal{O}(3)
$$

其中 $\mathcal{O}(3)$ 表示在 $s, t$ 中的三阶及更高阶无穷小量。

我们可以通过一个具体的例子来验证这一点 [@problem_id:1553888]。设 $X = \frac{\partial}{\partial x}$ 和 $Y = x \frac{\partial}{\partial y}$。它们的流分别为 $\phi_s^X(x, y) = (x+s, y)$ 和 $\phi_t^Y(x, y) = (x, y+tx)$。从 $p_0 = (x_0, y_0)$ 开始，我们依次计算：
1. $p_1 = \phi_s^X(p_0) = (x_0+s, y_0)$
2. $p_2 = \phi_t^Y(p_1) = (x_0+s, y_0 + t(x_0+s))$
3. $p_3 = \phi_{-s}^X(p_2) = (x_0, y_0 + t(x_0+s))$
4. $p_f = \phi_{-t}^Y(p_3) = (x_0, y_0 + t(x_0+s) - tx_0) = (x_0, y_0+st)$

总位移为 $\vec{D} = p_f - p_0 = (0, st) = \begin{pmatrix} 0 \\ 1 \end{pmatrix} st$。另一方面，我们计算李括号：
$$
[X, Y] = \left[\frac{\partial}{\partial x}, x \frac{\partial}{\partial y}\right] = \frac{\partial}{\partial x}\left(x \frac{\partial}{\partial y}\right) - x \frac{\partial}{\partial y}\left(\frac{\partial}{\partial x}\right) = 1 \cdot \frac{\partial}{\partial y} + x \frac{\partial^2}{\partial x \partial y} - x \frac{\partial^2}{\partial y \partial x} = \frac{\partial}{\partial y}
$$
在任意点 $(x_0, y_0)$，这个矢量对应于 $\begin{pmatrix} 0 \\ 1 \end{pmatrix}$。因此，我们验证了位移向量 $\vec{D}$ 的最低阶项确实是 $st[X, Y]$。这个结果直观地揭示了[李括号](@entry_id:636461)是流非对易性的度量。

### 李导数的核心性质

李导数作为一个导数算子，满足一些关键的代数性质，这些性质使其成为一个强大的分析工具。

1.  **线性性**：$\mathcal{L}_X(aT_1 + bT_2) = a \mathcal{L}_X T_1 + b \mathcal{L}_X T_2$ 对任意张量 $T_1, T_2$ 和常数 $a, b$ 成立。
2.  **Leibniz 法则**：[李导数](@entry_id:171745)对张量积满足[Leibniz法则](@entry_id:157949)，例如 $\mathcal{L}_X(T_1 \otimes T_2) = (\mathcal{L}_X T_1) \otimes T_2 + T_1 \otimes (\mathcal{L}_X T_2)$。

一个特别重要的特例是矢量场与函数的乘积 $fY$ 的[李导数](@entry_id:171745) [@problem_id:1679302]。根据[Leibniz法则](@entry_id:157949)，我们有：

$$
\mathcal{L}_X(fY) = (\mathcal{L}_X f)Y + f(\mathcal{L}_X Y)
$$

这个性质非常有用，可以将复杂对象的[李导数](@entry_id:171745)分解为更简单部分的导数。我们可以通过直接计算来验证它。例如，考虑 $M = \mathbb{R}^2$，取 $f(x,y)=x^2$, $X = y \frac{\partial}{\partial x}$ 和 $Y = x \frac{\partial}{\partial y}$。

一方面，我们直接计算 $\mathcal{L}_X(fY)$。首先 $fY = x^2(x \frac{\partial}{\partial y}) = x^3 \frac{\partial}{\partial y}$。然后计算[李括号](@entry_id:636461)：
$$
\mathcal{L}_X(fY) = [X, fY] = \left[y \frac{\partial}{\partial x}, x^3 \frac{\partial}{\partial y}\right]
$$
其 $x$ 分量为 $y \frac{\partial(0)}{\partial x} - x^3 \frac{\partial(y)}{\partial y} = -x^3$。
其 $y$ 分量为 $y \frac{\partial(x^3)}{\partial x} - x^3 \frac{\partial(0)}{\partial y} = y(3x^2) = 3x^2y$。
所以 $\mathcal{L}_X(fY) = -x^3 \frac{\partial}{\partial x} + 3x^2y \frac{\partial}{\partial y}$。

另一方面，我们使用[Leibniz法则](@entry_id:157949)：
- $\mathcal{L}_X f = X(f) = y \frac{\partial(x^2)}{\partial x} = 2xy$。因此 $(\mathcal{L}_X f)Y = (2xy)(x \frac{\partial}{\partial y}) = 2x^2y \frac{\partial}{\partial y}$。
- $\mathcal{L}_X Y = [X, Y] = [y \frac{\partial}{\partial x}, x \frac{\partial}{\partial y}] = -x \frac{\partial}{\partial x} + y \frac{\partial}{\partial y}$。因此 $f(\mathcal{L}_X Y) = x^2(-x \frac{\partial}{\partial x} + y \frac{\partial}{\partial y}) = -x^3 \frac{\partial}{\partial x} + x^2y \frac{\partial}{\partial y}$。

两者相加得到 $(\mathcal{L}_X f)Y + f(\mathcal{L}_X Y) = (2x^2y \frac{\partial}{\partial y}) + (-x^3 \frac{\partial}{\partial x} + x^2y \frac{\partial}{\partial y}) = -x^3 \frac{\partial}{\partial x} + 3x^2y \frac{\partial}{\partial y}$。两种方法得到的结果完全一致，验证了[Leibniz法则](@entry_id:157949)的正确性。

### [微分形式](@entry_id:146747)的[李导数](@entry_id:171745)与[嘉当公式](@entry_id:157961)

李导数也可以作用于[微分形式](@entry_id:146747)（covector fields or p-forms）。对于[微分形式](@entry_id:146747)，存在一个极其优美且强大的公式，即**嘉当魔法公式（Cartan's magic formula）**，它将[李导数](@entry_id:171745)与另外两个基本算子——**外微分（exterior derivative）** $d$ 和**[内积](@entry_id:158127)（interior product）** $i_X$ 联系起来。对于任意 $p$-形式 $\omega$，该公式为：

$$
\mathcal{L}_X \omega = d(i_X \omega) + i_X(d\omega)
$$

这里，$i_X \omega$ 是将矢量场 $X$ 缩并到 $\omega$ 的第一个参数中，从而得到一个 $(p-1)$-形式。这个公式避免了使用流和[拉回](@entry_id:160816)的极限定义，为计算提供了极大的便利。

例如，在 $\mathbb{R}^3$ 中，考虑矢量场 $X = y \frac{\partial}{\partial x} + z \frac{\partial}{\partial y}$ 和 [1-形式](@entry_id:270392) $\omega = x dz$ [@problem_id:1679311]。我们使用[嘉当公式](@entry_id:157961)计算 $\mathcal{L}_X \omega$：
1.  计算 $i_X \omega$：$i_X \omega = \omega(X) = (x dz)(y \frac{\partial}{\partial x} + z \frac{\partial}{\partial y}) = x \cdot dz(y \frac{\partial}{\partial x} + z \frac{\partial}{\partial y}) = 0$。因此 $d(i_X \omega) = 0$。
2.  计算 $d\omega$：$d\omega = d(x dz) = dx \wedge dz$。
3.  计算 $i_X(d\omega)$：$i_X(dx \wedge dz) = (i_X dx) \wedge dz - dx \wedge (i_X dz)$。我们有 $i_X dx = dx(X) = y$ 和 $i_X dz = dz(X) = 0$。所以 $i_X(d\omega) = y dz - dx \wedge 0 = y dz$。

将两部分加起来，得到 $\mathcal{L}_X \omega = 0 + y dz = y dz$。

[嘉当公式](@entry_id:157961)的一个直接推论是李导数与外[微分算子](@entry_id:140145)**对易（commute）**：

$$
\mathcal{L}_X(d\omega) = d(\mathcal{L}_X \omega)
$$

这是因为 $d(d\omega) = d^2\omega = 0$，所以 $\mathcal{L}_X(d\omega) = i_X(d(d\omega)) + d(i_X d\omega) = d(i_X d\omega)$。另一方面，$d(\mathcal{L}_X \omega) = d(i_X d\omega + d(i_X \omega)) = d(i_X d\omega)$，因为 $d^2=0$。这条性质 $\mathcal{L}_X d = d \mathcal{L}_X$ 是[微分几何](@entry_id:145818)中的一个基本恒等式。我们可以对一个0-形式（即一个函数 $f$）来验证它。该性质表明 $\mathcal{L}_X(df) = d(\mathcal{L}_X f)$ [@problem_id:1679298]。对于给定的 $f(x, y) = \exp(x) \cos(y)$ 和 $X = y^2 \frac{\partial}{\partial x} - x \frac{\partial}{\partial y}$，我们可以分别计算等式两边。
- 左边：$df = \exp(x)\cos(y)dx - \exp(x)\sin(y)dy$。$\mathcal{L}_X(df) = d(i_X df) = d(X(f))$。$X(f) = y^2(\exp(x)\cos(y)) - x(-\exp(x)\sin(y)) = \exp(x)(y^2\cos(y) + x\sin(y))$。然后取外微分得到 $\mathcal{L}_X(df) = d(\exp(x)(y^2\cos(y) + x\sin(y)))$。
- 右边：$\mathcal{L}_X f = X(f) = \exp(x)(y^2\cos(y) + x\sin(y))$。$d(\mathcal{L}_X f) = d(\exp(x)(y^2\cos(y) + x\sin(y)))$。
两边显然相等，验证了李导数和[外微分](@entry_id:161900)的对易性。

### 应用：对称性、[李代数](@entry_id:137954)与联络

李导数不仅是理论上的一个优美概念，它在几何和物理的许多领域都有着至关重要的应用。

#### 度量[张量的李导数](@entry_id:204198)与Killing矢量场

在黎曼几何和广义相对论中，[流形](@entry_id:153038)的几何结构由度量张量 $g$ 决定。度量张量沿矢量场 $V$ 的[李导数](@entry_id:171745) $\mathcal{L}_V g$ 衡量了当我们沿着 $V$ 的流移动时，度量（即长度和角度的测量方式）如何被扭曲。其分量形式为：

$$
(\mathcal{L}_V g)_{ij} = V^k \frac{\partial g_{ij}}{\partial x^k} + g_{kj} \frac{\partial V^k}{\partial x^i} + g_{ik} \frac{\partial V^k}{\partial x^j}
$$

如果 $\mathcal{L}_V g = 0$，这意味着度量在沿 $V$ 的流拖曳时保持不变。这样的矢量场 $V$ 被称为**Killing矢量场（Killing vector field）**。Killing[矢量场的流](@entry_id:180235)是**[等距变换](@entry_id:150881)（isometry）**，即保持距离的变换。因此，Killing矢量场对应于空间的[连续对称性](@entry_id:137257)。例如，欧氏空间中的平移和旋转都对应于Killing矢量场。

在[庞加莱上半平面模型](@entry_id:262810)中，度量为 $g = \frac{1}{y^2}(dx^2+dy^2)$。我们可以检验一个矢量场是否为Killing矢量场 [@problem_id:1679329]。例如，对于常数矢量场 $V = \alpha \frac{\partial}{\partial x} + \beta \frac{\partial}{\partial y}$，其分量 $V^1=\alpha, V^2=\beta$ 的导数均为零。代入公式计算 $(\mathcal{L}_V g)_{11}$：

$$
(\mathcal{L}_V g)_{11} = V^k \frac{\partial g_{11}}{\partial x^k} = V^1 \frac{\partial (1/y^2)}{\partial x} + V^2 \frac{\partial (1/y^2)}{\partial y} = \alpha \cdot 0 + \beta \cdot (-2y^{-3}) = -2\beta y^{-3}
$$

除非 $\beta=0$，否则 $(\mathcal{L}_V g)_{11}$ 不为零。这表明一般的常数矢量场不是庞加莱度量的Killing矢量场。只有当 $\beta=0$ 时（即纯水平平移 $V = \alpha \frac{\partial}{\partial x}$），我们才有可能得到一个Killing矢量场。事实上，可以证明 $\mathcal{L}_{\partial_x} g = 0$，说明水平平移是[庞加莱上半平面](@entry_id:264005)的一种对称性。

#### 矢量场构成的[李代数](@entry_id:137954)

[流形](@entry_id:153038) $M$ 上的所有光滑矢量场的集合，记作 $\mathfrak{X}(M)$，在矢量加法和标量乘法下构成一个无穷维矢量空间。更重要的是，[李括号](@entry_id:636461)运算 $[ \cdot, \cdot ]$ 赋予了这个空间一个**李代数（Lie algebra）**结构。这意味着李括号是[双线性](@entry_id:146819)的、反对称的（$[X, Y] = -[Y, X]$），并且满足**[Jacobi恒等式](@entry_id:140480)**：
$$
[X, [Y, Z]] + [Y, [Z, X]] + [Z, [X, Y]] = 0
$$

在许多情况下，一个有限的矢量场集合在李括号运算下是封闭的，即任意两个矢量场的[李括号](@entry_id:636461)仍然是该集合中矢量场的[线性组合](@entry_id:154743)。这样的集合构成一个有限维李代数，它通常是某个李群（连续对称性群）的“无穷小生成元”的代数。

一个经典的例子是三维欧氏空间 $\mathbb{R}^3$ 中的旋转群 $SO(3)$ 的李代数 $\mathfrak{so}(3)$ [@problem_id:1553915]。绕 $x, y, z$ 轴的[无穷小旋转](@entry_id:166635)可以由以下矢量场生成：
$$
L_x = y \frac{\partial}{\partial z} - z \frac{\partial}{\partial y}, \quad L_y = z \frac{\partial}{\partial x} - x \frac{\partial}{\partial z}, \quad L_z = x \frac{\partial}{\partial y} - y \frac{\partial}{\partial x}
$$
计算它们的[李括号](@entry_id:636461)，可以发现：
$$
[L_x, L_y] = -L_z, \quad [L_y, L_z] = -L_x, \quad [L_z, L_x] = -L_y
$$
这些关系表明 $\{L_x, L_y, L_z\}$ 在[李括号](@entry_id:636461)下是封闭的，它们张成了一个三维李代数，即 $\mathfrak{so}(3)$。这些对易关系中的系数（这里是 $\pm 1$ 或 $0$）被称为李代数的**[结构常数](@entry_id:157960)**，它们完全刻画了代数的结构。

#### 联络的[李导数](@entry_id:171745) (高等主题)

李导数的概念还可以推广到更抽象的几何对象上，例如[仿射联络](@entry_id:160152)。我们知道，[Christoffel符号](@entry_id:159831) $\Gamma^k_{ij}$ 在[坐标变换](@entry_id:172727)下并不像张量那样变换。然而，一个深刻的结果是，[Christoffel符号](@entry_id:159831)关于矢量场 $X$ 的[李导数](@entry_id:171745) $(\mathcal{L}_X \Gamma)^k_{ij}$ **确实**构成一个(1,2)型张量的分量。其表达式为 [@problem_id:1553923]：

$$
T^k_{ij} = (\mathcal{L}_X \Gamma)^k_{ij} = X^p \partial_p \Gamma^k_{ij} - \Gamma^p_{ij} \partial_p X^k + \Gamma^k_{pj} \partial_i X^p + \Gamma^k_{ip} \partial_j X^p + \partial_i \partial_j X^k
$$

这个张量 $T$ 描述了沿 $X$ 的流移动时，[协变导数](@entry_id:152476)自身的无穷小变化。这个事实突显了[李导数](@entry_id:171745)在构造[几何不变量](@entry_id:178611)和张量场方面的强大能力，即便作用对象本身不是张量。例如，在半径为 $R$ 的球面上，对于矢量场 $X = \theta \frac{\partial}{\partial \phi}$，可以计算出张量 $T$ 的分量 $T^2_{11} = 2\cot(\theta)$。这是一个良定义的张量分量，描述了在球面上沿纬线方向的流如何改变了联络的结构。

总之，李导数提供了一个与[协变导数](@entry_id:152476)互补的视角来理解[流形](@entry_id:153038)上的变化。它通过[矢量场的流](@entry_id:180235)来定义变化，天然地与对称性、守恒律和几何结构的变形联系在一起，是现代微分几何与理论物理中不可或缺的核心工具。