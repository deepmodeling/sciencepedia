## 引言
对称性是几何学与物理学中的一个基本而深刻的指导原则，从晶体的规则[排列](@entry_id:136432)到基本粒子的守恒律，对称性无处不在。在描述弯曲空间（如[黎曼流形](@entry_id:261160)）的几何学中，一个核心问题是如何精确地刻画其连续的“刚性”对称性。[基灵向量场](@entry_id:161770)（Killing vector field）正是为解决这一问题而生的关键数学工具，它为我们提供了一种描述空间如何在其自身内部连续移动而不改变其任何几何性质（如距离和角度）的语言。本文旨在系统地阐述[基灵向量场](@entry_id:161770)的理论及其在多个学科中的重要应用，为读者构建一个从基本定义到前沿应用的完整知识框架。

在接下来的内容中，我们将分三步深入探索[基灵向量场](@entry_id:161770)的世界。首先，在“**原理与机制**”一章中，我们将从[等距变换](@entry_id:150881)的无穷小生成元这一根本思想出发，建立[基灵向量场](@entry_id:161770)的严格定义，并推导出其等价的[微分方程](@entry_id:264184)——[基灵方程](@entry_id:161633)。我们还将揭示它与[测地线](@entry_id:269969)[守恒量](@entry_id:150267)以及[流形曲率](@entry_id:187680)之间深刻的内在联系。随后，在“**应用与交叉学科联系**”一章中，我们将展示[基灵向量场](@entry_id:161770)如何作为强大的分析工具，被用于探测几何结构、识别[对称空间](@entry_id:181790)，以及在广义相对论和理论物理中建立基本的[守恒定律](@entry_id:269268)。最后，通过“**动手实践**”部分，读者将有机会将理论应用于具体计算，巩固对概念的理解。

现在，让我们从第一性原理出发，深入探讨[基灵向量场](@entry_id:161770)的数学构造及其基本性质。

## 原理与机制

在“引言”章节中，我们初步了解了对称性在几何学中的核心地位。本章将深入探讨描述黎曼流形连续对称性的关键数学对象——**[基灵向量场](@entry_id:161770)（Killing vector fields）**。我们将从其定义出发，揭示其等价的数学刻画，并探讨其与[守恒定律](@entry_id:269268)、曲率及[流形](@entry_id:153038)全局性质之间深刻的内在联系。

### [基灵向量场](@entry_id:161770)：等距的[无穷小生成元](@entry_id:270424)

从最直观的角度看，[黎曼流形](@entry_id:261160) $(M,g)$ 的一个对称性是一种保持其几何结构不变的变换。一个保持度量张量 $g$ 不变的微分同胚 $f: M \to M$ 被称为**等距变换（isometry）**。这意味着对于任意点 $p \in M$ 和任意[切向量](@entry_id:265494) $v, w \in T_p M$，我们有 $g_p(v,w) = g_{f(p)}(df_p(v), df_p(w))$。用[拉回](@entry_id:160816)映射（pullback）的语言来说，这个条件等价于 $f^*g = g$。

现在，考虑一个由向量场 $X$ 生成的**流（flow）**，即一个单参数变换群 $\varphi_t$。如果对于所有 $t$，每个映射 $\varphi_t$ 都是一个等距变换，那么这个流就代表了[流形](@entry_id:153038)的一个连续对称性。这意味着对于所有定义了流的 $t$，我们都有 $\varphi_t^* g = g$ [@problem_id:1649433]。

然而，在[微分几何](@entry_id:145818)中，我们常常更关心“无穷小”的行为。与其要求度量在流的每一步都保持不变，我们可以考察度量在 $t=0$ 时刻沿流的无穷小变化率。这个变化率正是由**李导数（Lie derivative）** $\mathcal{L}_X g$ 描述的。根据定义，李导数是[拉回度量](@entry_id:161465)对参数 $t$ 的导数在 $t=0$ 处的值：
$$
(\mathcal{L}_X g)_p = \left. \frac{d}{dt} \right|_{t=0} (\varphi_t^* g)_p
$$
这个定义精确地捕捉了度量 $g$ 在点 $p$ 处沿着 $X$ 的流的无穷小变化。如果流 $\varphi_t$ 的每一步都是[等距变换](@entry_id:150881)，那么 $\varphi_t^* g$ 是一个常数[张量场](@entry_id:190170)（等于 $g$），其导数自然为零。反之，如果 $\mathcal{L}_X g = 0$，则表明度量在无穷小意义下是不变的。通过求解微分方程 $\frac{d}{dt}(\varphi_t^*g) = \varphi_t^*(\mathcal{L}_X g)$，我们可以看到，$\mathcal{L}_X g = 0$ 意味着 $\varphi_t^*g$ 对于所有 $t$ 都是常数，并且等于其在 $t=0$ 的值 $g$。因此，这两个条件是等价的 [@problem_id:2982402]。

这一观察引出了[基灵向量场](@entry_id:161770)的核心定义。

**定义：** 黎曼流形 $(M,g)$ 上的一个光滑向量场 $X$ 被称为**[基灵向量场](@entry_id:161770)**，如果它关于度量 $g$ 的李导数为零，即：
$$
\mathcal{L}_X g = 0
$$

从定义可知，$\mathcal{L}_X g$ 是一个 $(0,2)$ 型[张量场](@entry_id:190170)。在点 $p \in M$，$(\mathcal{L}_X g)_p$ 作用于一对切向量 $v, w \in T_p M$。因此，$\mathcal{L}_X g = 0$ 的条件等价于对任意点 $p$ 和任意[切向量](@entry_id:265494) $v, w$，都有 $(\mathcal{L}_X g)_p(v,w) = 0$。根据李导数的定义，这又等价于：
$$
\left. \frac{d}{dt} \right|_{t=0} g_{\varphi_t(p)}(d\varphi_t(v), d\varphi_t(w)) = 0
$$
这恰恰说明了，由 $X$ 生成的流在无穷小意义下保持了所有[内积](@entry_id:158127)。这就是为什么[基灵向量场](@entry_id:161770)被视为**等距的无穷小生成元** [@problem_id:2982413]。

作为一个具体的例子，考虑[庞加莱上半平面模型](@entry_id:262810) $M = \{(x,y) \in \mathbb{R}^2 \mid y > 0\}$，其度量为 $g = \frac{1}{y^2}(dx \otimes dx + dy \otimes dy)$。向量场 $X = k \frac{\partial}{\partial x}$（其中 $k$ 为非零常数）描述了沿 $x$ 轴的平移。它的流是 $\varphi_t(x,y) = (x+kt, y)$。我们可以直接计算度量的[拉回](@entry_id:160816)。流的[雅可比矩阵](@entry_id:264467)是单位矩阵 $J = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$。在变换后的点 $\varphi_t(x,y)$，度量矩阵为 $g(\varphi_t(x,y)) = \begin{pmatrix} 1/y^2 & 0 \\ 0 & 1/y^2 \end{pmatrix}$，因为它只依赖于不变的 $y$ 坐标。因此，[拉回度量](@entry_id:161465)为 $(\varphi_t^* g) = J^T \cdot g(\varphi_t(p)) \cdot J = g$。由于对于任意 $t$，$\varphi_t^*g = g$ 都成立，所以 $X = k \frac{\partial}{\partial x}$ 是一个[基灵向量场](@entry_id:161770) [@problem_id:1649433]。

### 等价表述：[基灵方程](@entry_id:161633)

定义 $\mathcal{L}_X g = 0$ 虽然在概念上十分优雅，但在实际计算中往往不便使用。一个更具操作性的等价条件，可以通过引入[列维-奇维塔联络](@entry_id:161107) $\nabla$ 来获得。

我们知道，对于任意向量场 $Y, Z$，[李导数](@entry_id:171745)的表达式为：
$$
(\mathcal{L}_X g)(Y,Z) = X(g(Y,Z)) - g([X,Y], Z) - g(Y, [X,Z])
$$
利用列维-奇维塔联络的两个基本性质——[度量兼容性](@entry_id:265910)（$\nabla g=0$）和无挠性（$[Y,Z] = \nabla_Y Z - \nabla_Z Y$），我们可以重写上式。[度量兼容性](@entry_id:265910)意味着 $X(g(Y,Z)) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z)$。代入并展开整理后，我们得到一个至关重要的恒等式 [@problem_id:2982402]：
$$
(\mathcal{L}_X g)(Y,Z) = g(\nabla_Y X, Z) + g(Y, \nabla_Z X)
$$
因此，$\mathcal{L}_X g = 0$ 的条件等价于以下方程，它被称为**[基灵方程](@entry_id:161633)（Killing's equation）**：
$$
g(\nabla_Y X, Z) + g(Y, \nabla_Z X) = 0 \quad \text{对所有向量场 } Y, Z \text{ 成立}
$$
这个方程表明，[张量场](@entry_id:190170) $Y \mapsto \nabla_Y X$ （可以看作一个在每一点都作用于切空间的线性算子）关于度量 $g$ 是**斜伴随的（skew-adjoint）**或**反对称的**。

在[局部坐标](@entry_id:181200) $\{x^i\}$ 中，令 $X = X^i \partial_i$，其对偶1-形式为 $X_j = g_{jk}X^k$。取 $Y=\partial_i$ 和 $Z=\partial_j$，[基灵方程](@entry_id:161633)就变成了分量形式：
$$
\nabla_i X_j + \nabla_j X_i = 0
$$
这个简洁的方程意味着[协变张量](@entry_id:634493) $\nabla_i X_j$ 关于其指标 $i,j$ 是反对称的 [@problem_id:1649447]。这个形式在具体计算中非常有用。

从[基灵方程](@entry_id:161633)的一个直接推论是，任何[基灵向量场](@entry_id:161770)都是**无散度（divergence-free）**的。一个向量场 $X$ 的散度定义为 $\text{div}X = \text{tr}(\nabla X) = g^{ij}\nabla_i X_j$。利用[基灵方程](@entry_id:161633)和度量[张量的对称性](@entry_id:202126)，我们有：
$$
\text{div}X = g^{ij}\nabla_i X_j = -g^{ij}\nabla_j X_i = -g^{ji}\nabla_j X_i = -\text{div}X
$$
因此，$2\text{div}X = 0$，即 $\text{div}X = 0$。然而，需要特别强调的是，这个条件只是必要条件，而非充分条件。存在许多[无散度](@entry_id:190991)的向量场并非[基灵向量场](@entry_id:161770) [@problem_id:2982402]。

让我们通过一个例子来应用这些计算工具。考虑一个由度规 $ds^2 = \frac{1}{z^\alpha} (dx^2 + dy^2) + \frac{1}{z^\beta} dz^2$ 描述的[三维流形](@entry_id:193484)。我们希望确定参数 $\alpha, \beta$ 的值，使得缩放向量场 $X = x \frac{\partial}{\partial x} + y \frac{\partial}{\partial y} + z \frac{\partial}{\partial z}$ 是一个[基灵向量场](@entry_id:161770) [@problem_id:1649437]。我们可以使用李导数的坐标表达式 $(\mathcal{L}_{X} g)_{ij} = X^{k} \partial_{k} g_{ij} + g_{ik} \partial_{j} X^{k} + g_{jk} \partial_{i} X^{k} = 0$。
对于 $xx$ 分量：
$$
(\mathcal{L}_{X} g)_{xx} = X^z \partial_z g_{xx} + 2g_{xx}\partial_x X^x = z(-\alpha z^{-\alpha-1}) + 2(z^{-\alpha})(1) = (-\alpha+2)z^{-\alpha}
$$
要使其为零，必须有 $\alpha=2$。
对于 $zz$ 分量：
$$
(\mathcal{L}_{X} g)_{zz} = X^z \partial_z g_{zz} + 2g_{zz}\partial_z X^z = z(-\beta z^{-\beta-1}) + 2(z^{-\beta})(1) = (-\beta+2)z^{-\beta}
$$
这要求 $\beta=2$。因此，我们发现当 $\alpha=2$ 且 $\beta=2$ 时，$X$ 是一个[基灵向量场](@entry_id:161770)，此时度量为 $ds^2 = \frac{1}{z^2}(dx^2+dy^2+dz^2)$，这正是[双曲空间](@entry_id:268092) $\mathbb{H}^3$ 的庞加莱上半空间模型。

### [基灵向量场](@entry_id:161770)与[守恒量](@entry_id:150267)：[诺特定理](@entry_id:145690)

[对称性与守恒律](@entry_id:160300)之间的深刻联系是物理学和几何学中的一个基本主题，其最精确的表述是[诺特定理](@entry_id:145690)。在黎曼几何的框架下，[基灵向量场](@entry_id:161770)（代表[几何对称性](@entry_id:189059)）直接导致了沿[测地线](@entry_id:269969)（粒子在没有外力作用下的路径）的守恒量。

**定理：** 若 $X$ 是[黎曼流形](@entry_id:261160) $(M,g)$ 上的一个[基灵向量场](@entry_id:161770)，$\gamma(t)$ 是 $M$ 上的一条[测地线](@entry_id:269969)，则[内积](@entry_id:158127) $g(X_{\gamma(t)}, \dot{\gamma}(t))$ 沿 $\gamma(t)$ 是一个常数。

**证明：** 为了证明这个量是守恒的，我们计算它对参数 $t$ 的导数：
$$
\frac{d}{dt} g(X, \dot{\gamma}) = g(\nabla_{\dot{\gamma}}X, \dot{\gamma}) + g(X, \nabla_{\dot{\gamma}}\dot{\gamma})
$$
由于 $\gamma$ 是一条[测地线](@entry_id:269969)，其加速度为零，即 $\nabla_{\dot{\gamma}}\dot{\gamma} = 0$。因此，上式第二项消失。剩下第一项 $g(\nabla_{\dot{\gamma}}X, \dot{\gamma})$。现在，我们利用 $X$ 是[基灵向量场](@entry_id:161770)这一事实。根据[基灵方程](@entry_id:161633)，对于任意向量场 $Y$，都有 $g(\nabla_Y X, Y) + g(Y, \nabla_Y X) = 0$。由于 $g$ 是对称的，这简化为 $2g(\nabla_Y X, Y)=0$，即 $g(\nabla_Y X, Y)=0$。将 $Y$ 替换为[测地线](@entry_id:269969)的切向量 $\dot{\gamma}$，我们得到 $g(\nabla_{\dot{\gamma}}X, \dot{\gamma})=0$。
因此，$\frac{d}{dt} g(X, \dot{\gamma}) = 0$，这证明了 $g(X, \dot{\gamma})$ 是一个守恒量 [@problem_id:2982402]。

这个[守恒量](@entry_id:150267)具有重要的物理意义。例如，在广义相对论中，时空是一个[洛伦兹流形](@entry_id:162024)。如果时空度规存在一个类时的[基灵向量场](@entry_id:161770)，那么沿着自由下落粒子（[测地线](@entry_id:269969)）的世界线，$g(X, \dot{\gamma})$ 的守恒对应于[能量守恒](@entry_id:140514)。如果存在一个与空间旋转相关的[轴对称](@entry_id:173333)[基灵向量场](@entry_id:161770)，其[守恒量](@entry_id:150267)则对应于角动量守恒。

让我们通过一个实例来计算这个[守恒量](@entry_id:150267)。再次考虑[庞加莱上半平面](@entry_id:264005) $H^2$，其度量为 $g_{ij} = \frac{1}{y^2}\delta_{ij}$。已知向量场 $X = (x^2 - y^2) \frac{\partial}{\partial x} + 2xy \frac{\partial}{\partial y}$ 是一个[基灵向量场](@entry_id:161770)。假设一条由[弧长参数化](@entry_id:634139)的[测地线](@entry_id:269969) $\gamma(s)$ 经过点 $P=(3, 2)$，且在该点的切向量是垂直向上的 [@problem_id:1649467]。
守恒量为 $C = g(\dot{\gamma}(s), X(\gamma(s)))$。由于它是常数，我们只需在点 $P$ 计算它的值即可。
在 $P=(3,2)$ 处，[基灵向量场](@entry_id:161770)的值为 $X_P = (3^2-2^2)\partial_x + 2(3)(2)\partial_y = 5\partial_x + 12\partial_y$。
[测地线](@entry_id:269969)的[切向量](@entry_id:265494) $\dot{\gamma}$ 是垂直向上的，所以 $\dot{\gamma}^x = 0$。由于[测地线](@entry_id:269969)由[弧长参数化](@entry_id:634139)，其速度范数为1，即 $g(\dot{\gamma}, \dot{\gamma})=1$。在点 $P$：
$$
1 = g_P(\dot{\gamma}, \dot{\gamma}) = \frac{1}{2^2}((\dot{\gamma}^x)^2 + (\dot{\gamma}^y)^2) = \frac{1}{4}(0 + (\dot{\gamma}^y)^2)
$$
解得 $\dot{\gamma}^y = 2$（因为[切向量](@entry_id:265494)向上）。所以，在 $P$ 点的切向量是 $\dot{\gamma}_P = 2\partial_y$。
现在计算守恒量的值：
$$
C = g_P(\dot{\gamma}_P, X_P) = \frac{1}{2^2}(\dot{\gamma}^x X^x + \dot{\gamma}^y X^y) = \frac{1}{4}(0 \cdot 5 + 2 \cdot 12) = \frac{24}{4} = 6
$$
这个值为6的量将在这条特定[测地线](@entry_id:269969)的每一点上都保持不变。

### [基灵向量场](@entry_id:161770)空间的结构

[流形](@entry_id:153038)上所有[基灵向量场](@entry_id:161770)的集合，记为 $\mathfrak{k}(M)$，具有丰富的[代数结构](@entry_id:137052)。

首先，$\mathfrak{k}(M)$ 是一个[实数域](@entry_id:151347)上的**[向量空间](@entry_id:151108)**。如果 $X$ 和 $Y$ 是[基灵向量场](@entry_id:161770)，那么对于任意常数 $a, b \in \mathbb{R}$，$aX+bY$ 也是一个[基灵向量场](@entry_id:161770)。这是因为李导数是线性的：$\mathcal{L}_{aX+bY}g = a\mathcal{L}_X g + b\mathcal{L}_Y g = 0$。

更进一步，$\mathfrak{k}(M)$ 在李括号运算下是封闭的。也就是说，如果 $X$ 和 $Y$ 是[基灵向量场](@entry_id:161770)，那么它们的**李括号** $[X,Y]$ 也是一个[基灵向量场](@entry_id:161770)。这可以利用[李导数](@entry_id:171745)与李括号的雅可比恒等式来证明：$\mathcal{L}_{[X,Y]}g = [\mathcal{L}_X, \mathcal{L}_Y]g = \mathcal{L}_X(\mathcal{L}_Y g) - \mathcal{L}_Y(\mathcal{L}_X g)$。由于 $\mathcal{L}_X g=0$ 且 $\mathcal{L}_Y g=0$，显然有 $\mathcal{L}_{[X,Y]}g = 0$ [@problem_id:1649429]。
一个在[李括号](@entry_id:636461)运算下封闭的[向量空间](@entry_id:151108)被称为**[李代数](@entry_id:137954)（Lie algebra）**。因此，[流形](@entry_id:153038)上所有[基灵向量场](@entry_id:161770)的集合构成一个[李代数](@entry_id:137954)。

关于[基灵场](@entry_id:188681)的一个最深刻的性质是它的“刚性”。一个[基灵向量场](@entry_id:161770)由其在**任意一点**的**初始数据**完全确定。这里的初始数据指的是向量场在该点的值及其一阶[协变导数](@entry_id:152476)。
具体来说，一个定义在点 $p$ 邻域上的[基灵向量场](@entry_id:161770) $X$ 由其在点 $p$ 的值 $v = X_p \in T_p M$ 和其[协变导数](@entry_id:152476) $A = (\nabla X)_p \in \text{End}(T_p M)$ 唯一确定。
这些初始数据并不是完全自由的。[基灵方程](@entry_id:161633) $g_p(Au, w) + g_p(u, Aw) = 0$ 必须在点 $p$ 成立。这要求算子 $A$ 必须是关于[内积](@entry_id:158127) $g_p$ 的斜[伴随算子](@entry_id:140236)。然而，[基灵方程](@entry_id:161633)本身并未对向量场的值 $v=X_p$ 施加任何代数约束 [@problem_id:2982403]。

这个性质导致了一个惊人的结论：$\mathfrak{k}(M)$ 是一个有限维李代数。其维数受限于初始数据的自由度。在 $n$ 维[流形](@entry_id:153038)中，初始值 $v \in T_p M$ 的选择有 $n$ 个自由度。斜[伴随算子](@entry_id:140236) $A$ 构成的空间（即[正交群](@entry_id:152531)的[李代数](@entry_id:137954) $\mathfrak{so}(n)$）的维数是 $\binom{n}{2} = \frac{n(n-1)}{2}$。因此，[基灵向量场](@entry_id:161770)[李代数](@entry_id:137954)的维数有一个上界：
$$
\dim \mathfrak{k}(M) \le n + \frac{n(n-1)}{2} = \frac{n(n+1)}{2}
$$
达到这个维数上界的[流形](@entry_id:153038)被称为**[最大对称空间](@entry_id:160477)（maximally symmetric spaces）**，它们必然是[常曲率空间](@entry_id:161841)，例如[欧氏空间](@entry_id:138052)、球面和[双曲空间](@entry_id:268092) [@problem_id:2982403]。

### [基灵向量场](@entry_id:161770)、曲率与全局性质

既然[基灵向量场](@entry_id:161770)生成等距变换，而[等距变换](@entry_id:150881)保持所有内蕴几何性质，那么它们必然也保持由度量导出的一切曲率量，包括黎曼曲率张量（Riem）、[里奇曲率张量](@entry_id:271424)（Ric）和标量曲率（$R$）。这意味着，如果 $X$ 是一个[基灵向量场](@entry_id:161770)，那么我们有：
$$
\mathcal{L}_X \text{Riem} = 0, \quad \mathcal{L}_X \text{Ric} = 0, \quad \mathcal{L}_X R = 0
$$
这个性质表明，沿着[基灵向量场](@entry_id:161770)的流，曲率是保持不变的 [@problem_id:1649476]。

[基灵向量场](@entry_id:161770)与曲率之间还存在更深刻的[微分](@entry_id:158718)恒等式。一个重要的例子是**[博赫纳恒等式](@entry_id:193184)（Bochner identity）**。通过交换协变导数的顺序并利用[基灵方程](@entry_id:161633)，可以推导出如下关系式：
$$
\nabla_j \nabla^j X_i = -R_{ik}X^k
$$
这里 $\nabla^j = g^{jk}\nabla_k$ 是[升指标](@entry_id:265340)后的[协变导数](@entry_id:152476)，$R_{ik}$ 是[里奇曲率张量](@entry_id:271424)的分量。这个恒等式将[基灵向量场](@entry_id:161770)的[拉普拉斯算子](@entry_id:146319)与其自身通过[里奇张量](@entry_id:159336)联系起来 [@problem_id:1649411]。

另一个形式的[博赫纳公式](@entry_id:187951)作用于[基灵场](@entry_id:188681)范数的平方 $|X|^2=g(X,X)$：
$$
\frac{1}{2} \Delta(|X|^2) = |\nabla X|^2 - \text{Ric}(X, X)
$$
其中 $\Delta$ 是作用于函数的[拉普拉斯-贝尔特拉米算子](@entry_id:267002)，$|\nabla X|^2$ 是[协变导数](@entry_id:152476)张量 $\nabla X$ 的范数平方，而 $\text{Ric}(X, X) = R_{ij}X^i X^j$ 是里奇曲率作用于向量场 $X$。

这个公式是连接局部曲率与[流形](@entry_id:153038)全局性质的强大桥梁。作为一个应用的范例，我们可以证明以下令人瞩目的定理 [@problem_id:1649417]。

**定理：** 一个紧致、可定向且里奇曲率处处严格为负（即对任意非零向量 $v$，$\text{Ric}(v,v)  0$）的[黎曼流形](@entry_id:261160) $(M,g)$，不容许任何非平凡的（即非零的）[基灵向量场](@entry_id:161770)。

**证明：** 假设 $X$ 是这样一个[流形](@entry_id:153038)上的任意一个[基灵向量场](@entry_id:161770)。我们将上述[博赫纳公式](@entry_id:187951)在整个[流形](@entry_id:153038) $M$ 上积分：
$$
\int_M \frac{1}{2} \Delta(|X|^2) \, dV = \int_M |\nabla X|^2 \, dV - \int_M \text{Ric}(X, X) \, dV
$$
其中 $dV$ 是黎曼[体积元](@entry_id:267802)。根据散度定理（或[格林公式](@entry_id:173118)），对于紧致无边的[流形](@entry_id:153038)，任何函数[拉普拉斯算子](@entry_id:146319)的积分为零。因此，左边项为零。我们得到：
$$
\int_M |\nabla X|^2 \, dV = \int_M \text{Ric}(X, X) \, dV
$$
现在考察这个等式的两边。左边积分项 $|\nabla X|^2$ 是一个范数的平方，因此在 $M$ 上处处非负，其积分也必然非负。
对于右边，根据假设，[流形](@entry_id:153038)的里奇曲率是严格负定的。这意味着，在 $X(p) \neq 0$ 的任意点 $p$，被积函数 $\text{Ric}(X,X)$ 的值严格为负。在 $X(p)=0$ 的点，该值为零。因此，右边的积分值必然小于或等于零。
$$
\underbrace{\int_M |\nabla X|^2 \, dV}_{\ge 0} = \underbrace{\int_M \text{Ric}(X, X) \, dV}_{\le 0}
$$
唯一能使这个等式成立的可能性是两边同时为零。
$\int_M |\nabla X|^2 \, dV = 0$ 意味着 $|\nabla X|^2$ 处处为零，即 $\nabla X = 0$。
$\int_M \text{Ric}(X, X) \, dV = 0$ 意味着 $\text{Ric}(X,X)$ 必须处处为零。由于[里奇曲率](@entry_id:162038)是严格负定的，这只能在 $X$ 处处为零时发生。
因此，我们得出结论：$X$ 必须是[零向量](@entry_id:156189)场。这意味着该[流形](@entry_id:153038)上不存在任何非平凡的[基灵向量场](@entry_id:161770)。这个结果完美地展示了局部几何（[负曲率](@entry_id:159335)）如何[对流](@entry_id:141806)形的全局对称性施加强大的限制。