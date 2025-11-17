## 引言
在数学和物理学的广阔天地中，对称性是一个无处不在的指导原则。从晶体的规则[排列](@entry_id:136432)到基本粒子相互作用的定律，对称性的概念为我们提供了理解和预测自然现象的强大工具。当对称性是连续的——例如旋转一个球体或时空中的平移——描述它们的数学语言便是**[李群](@entry_id:137659)**。然而，[李群](@entry_id:137659)作为一种弯曲的几何对象（[流形](@entry_id:153038)），其结构可能相当复杂，直接处理它们往往颇具挑战性。

那么，我们如何才能驯服这些描述连续对称性的强大却复杂的对象呢？本文旨在填补这一认知鸿沟，揭示一个深刻而优美的思想：每一个复杂的李群都紧密关联着一个相对简单的线性结构——它的**[李代数](@entry_id:137954)**。这个[代数结构](@entry_id:137052)就像是群在单位元附近的一个“线性快照”，捕捉了其所有的无穷小行为。理解了这种代数，我们便掌握了解析整个群的关键。

在接下来的内容中，你将踏上一段从几何到代数再回到应用的旅程。
- 在**“原理与机制”**一章中，我们将建立[李群](@entry_id:137659)与[李代数](@entry_id:137954)之间的核心联系，探索如何通过求导从群走向代数，并利用指数映射从代数返回到群。我们将揭示李括号如何捕捉群的[非对易性](@entry_id:153545)，并将这些抽象概念具体化。
- 接着，在**“应用与跨学科联系”**一章中，我们将见证这些理论的威力，看它们如何为经典力学、量子自旋、[规范场](@entry_id:159627)论和机器人学等不同领域的问题提供统一而深刻的见解。
- 最后，在**“动手实践”**部分，你将有机会通过解决具体问题来巩固所学知识，亲手计算[结构常数](@entry_id:157960)和生成群的路径，从而真正内化这些强大的数学工具。

## 原理与机制

继前一章对[李群](@entry_id:137659)作为[连续对称性](@entry_id:137257)的介绍之后，本章将深入探讨其内在的[代数结构](@entry_id:137052)——李代数。我们将阐明[李群](@entry_id:137659)与其[李代数](@entry_id:137954)之间的基本联系，探索如何从群的结构导出代数的结构，反之亦然。本章的核心目标是建立一个坚实的理论框架，揭示这些优雅的数学对象背后的原理与机制。

### 从李群到[李代数](@entry_id:137954)：[单位元处的切空间](@entry_id:266468)

理解李群的关键在于认识到，尽管它们是可能非常复杂的弯曲[流形](@entry_id:153038)，但其在单位元附近的局部结构可以由一个[线性空间](@entry_id:151108)——即其[李代数](@entry_id:137954)——来近似。这个[线性空间](@entry_id:151108)捕捉了群的“无穷小”行为。

一个**李代数（Lie algebra）** $\mathfrak{g}$ 最直观的定义是其对应[李群](@entry_id:137659) $G$ 在单位元 $I$ 处的[切空间](@entry_id:199137) $T_I G$。切空间的元素，即切向量，可以被看作是穿过单位元的路径的瞬时速度。

考虑一个[矩阵李群](@entry_id:145968)中的一条光滑路径（或称为曲线） $g(t)$，其中 $t$ 是一个实数参数，并且路径在 $t=0$ 时通过单位元，即 $g(0) = I$。该路径在单位元处的**切向量（tangent vector）**就是此路径在该点的导数，定义为：

$$
X = \left. \frac{d}{dt} \right|_{t=0} g(t)
$$

这个切向量 $X$ 就是李代数 $\mathfrak{g}$ 的一个元素。[李代数](@entry_id:137954)包含了所有这样路径的切向量，并且它自身构成一个[向量空间](@entry_id:151108)。

为了使这个概念更具体，让我们考察一个实例。考虑由形式为 $g(a, b) = \begin{pmatrix} a  b \\ 0  1 \end{pmatrix}$ 的可逆 $2 \times 2$ 矩阵构成的[李群](@entry_id:137659)，其中 $a \gt 0$ 且 $b \in \mathbb{R}$。群的单位元是 $a=1, b=0$ 时的[单位矩阵](@entry_id:156724) $I$。现在，我们定义一条穿过此单位元的特定路径：

$$
g(t) = \begin{pmatrix} \exp(t)  t \\ 0  1 \end{pmatrix}
$$

显然，$g(0) = \begin{pmatrix} \exp(0)  0 \\ 0  1 \end{pmatrix} = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} = I$。为了找到属于该群[李代数](@entry_id:137954)的[切向量](@entry_id:265494)，我们计算 $g(t)$ 对 $t$ 的导数，并在 $t=0$ 处取值 [@problem_id:1523083]：

$$
\frac{d}{dt} g(t) = \frac{d}{dt} \begin{pmatrix} \exp(t)  t \\ 0  1 \end{pmatrix} = \begin{pmatrix} \exp(t)  1 \\ 0  0 \end{pmatrix}
$$

在 $t=0$ 处求值，我们得到[李代数](@entry_id:137954)中的一个元素：

$$
X = \left. \frac{d}{dt} \right|_{t=0} g(t) = \begin{pmatrix} \exp(0)  1 \\ 0  0 \end{pmatrix} = \begin{pmatrix} 1  1 \\ 0  0 \end{pmatrix}
$$

这个矩阵 $X$ 就是[李群](@entry_id:137659)在单位元附近沿 $g(t)$ 方向的“无穷小生成元”。李代数正是由所有这些无穷小生成元构成的集合。

### [指数映射](@entry_id:137184)：从代数回到群

如果[李代数](@entry_id:137954)描述了李群的无穷小行为，那么我们自然会问：能否通过这些无穷小生成元来重构群中的有限变换？答案是肯定的，而连接李代数 $\mathfrak{g}$ 和[李群](@entry_id:137659) $G$ 的桥梁就是**[指数映射](@entry_id:137184)（exponential map）**。

对于[矩阵李群](@entry_id:145968)，指数映射就是**矩阵指数**，对于任意矩阵 $X$，其定义为以下[幂级数](@entry_id:146836)：

$$
\exp(X) = \sum_{k=0}^{\infty} \frac{X^k}{k!} = I + X + \frac{X^2}{2!} + \frac{X^3}{3!} + \dots
$$

对于任意[李代数](@entry_id:137954)元素 $X \in \mathfrak{g}$，曲线 $\gamma(t) = \exp(tX)$ 是[李群](@entry_id:137659) $G$ 中的一条路径，称为由 $X$ 生成的**[单参数子群](@entry_id:181957)（one-parameter subgroup）**。这条路径满足 $\gamma(0) = I$ 且其在 $t=0$ 处的[切向量](@entry_id:265494)正是 $X$ 本身。

这个过程最经典的例子是从二维旋转的无穷小生成元重构有限旋转。二维[旋转群](@entry_id:204412) $SO(2)$ 的[李代数](@entry_id:137954) $\mathfrak{so}(2)$ 是由[反对称矩阵](@entry_id:155998)构成的。其一个基底是 $X = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$。让我们通过指数映射来生成一个有限旋转 [@problem_id:1523125]。为此，我们计算 $R(\theta) = \exp(\theta X)$。首先，我们计算 $X$ 的幂：
$X^0 = I = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}$
$X^1 = X = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$
$X^2 = \begin{pmatrix} -1  0 \\ 0  -1 \end{pmatrix} = -I$
$X^3 = -X$
$X^4 = I$
这个幂次序列以 4 为周期。将此模式代入指数级数：

$$
\begin{align*}
\exp(\theta X)  &= I + \theta X + \frac{(\theta X)^2}{2!} + \frac{(\theta X)^3}{3!} + \frac{(\theta X)^4}{4!} + \dots \\
 &= \left(1 - \frac{\theta^2}{2!} + \frac{\theta^4}{4!} - \dots\right)I + \left(\theta - \frac{\theta^3}{3!} + \frac{\theta^5}{5!} - \dots\right)X \\
 &= \cos(\theta)I + \sin(\theta)X \\
 &= \cos(\theta)\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + \sin(\theta)\begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix} = \begin{pmatrix} \cos(\theta)  -\sin(\theta) \\ \sin(\theta)  \cos(\theta) \end{pmatrix}
\end{align*}
$$

这正是绕原点旋转角度 $\theta$ 的标准旋转矩阵。这个例子完美地展示了李代数元素（[无穷小旋转](@entry_id:166635)）如何通过[指数映射](@entry_id:137184)生成李群中的元素（有限旋转）。

[指数映射](@entry_id:137184)也是确定一个李群对应的[李代数](@entry_id:137954)具体形式的强大工具。一个重要的矩阵恒等式是**[雅可比公式](@entry_id:142453)**：$\det(\exp(A)) = \exp(\text{tr}(A))$，其中 $\text{tr}(A)$ 是矩阵 $A$ 的迹。我们可以利用这个公式来确定[特殊线性群](@entry_id:139538) $SL(2, \mathbb{R})$（所有[行列式](@entry_id:142978)为 1 的 $2 \times 2$ 实矩阵构成的群）的[李代数](@entry_id:137954) $\mathfrak{sl}(2, \mathbb{R})$。根据定义，一个矩阵 $X$ 属于 $\mathfrak{sl}(2, \mathbb{R})$ 当且仅当由它生成的[单参数子群](@entry_id:181957) $\exp(tX)$ 对所有 $t$ 都位于 $SL(2, \mathbb{R})$ 中 [@problem_id:1678773]。这意味着对于所有 $t \in \mathbb{R}$，必须满足 $\det(\exp(tX))=1$。利用[雅可比公式](@entry_id:142453)，我们得到：

$$
\det(\exp(tX)) = \exp(\text{tr}(tX)) = \exp(t \cdot \text{tr}(X)) = 1
$$

这个等式对所有 $t$ 都成立的唯一条件是 $\text{tr}(X) = 0$。因此，$\mathfrak{sl}(2, \mathbb{R})$ 就是所有迹为零的 $2 \times 2$ 实矩阵的集合。这是一个三维[向量空间](@entry_id:151108)，一个常见的基底是：
$$
H = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}, \quad E = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}, \quad F = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}
$$

### 李括号：捕捉非对易性

我们已经看到李代数是一个[向量空间](@entry_id:151108)，但它还有额外的[代数结构](@entry_id:137052)，使其能够完全捕捉[李群](@entry_id:137659)的局部非对易性。这个结构由**李括号（Lie bracket）**提供。

对于[矩阵李代数](@entry_id:204591)，李括号就是矩阵的**对易子（commutator）**，定义为：

$$
[X, Y] = XY - YX
$$

[李括号](@entry_id:636461) $[X, Y]$ 衡量了 $X$ 和 $Y$ 的乘法顺序交换后产生的差异。如果 $[X, Y] = 0$，则称 $X$ 和 $Y$ 是可交换的。如果一个[李代数](@entry_id:137954)中所有元素的[李括号](@entry_id:636461)都为零，则称该李代数为**阿贝尔（abelian）**的。

李括号的本质是捕捉群层面非对易性的无穷小表现。为了理解这一点，可以考虑群中两个元素的乘积 $\exp(tX)\exp(tY)$。如果群是可交换的，这应该等于 $\exp(t(X+Y))$。然而，对于[非对易](@entry_id:136599)群，这并不成立，而[李括号](@entry_id:636461)恰好描述了其一阶偏离：$\exp(tX)\exp(tY) \approx \exp(t(X+Y) + \frac{t^2}{2}[X,Y])$。

让我们计算 $\mathfrak{sl}(2, \mathbb{R})$ 中两个基底元素的[李括号](@entry_id:636461)。设 $X = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}$ 和 $Y = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}$ [@problem_id:1523080]。

$$
XY = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix} \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix} = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix}
$$

$$
YX = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix} \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix} = \begin{pmatrix} 0  0 \\ 0  1 \end{pmatrix}
$$

因此，[李括号](@entry_id:636461)为：

$$
[X, Y] = XY - YX = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix} - \begin{pmatrix} 0  0 \\ 0  1 \end{pmatrix} = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$

我们发现结果恰好是 $\mathfrak{sl}(2, \mathbb{R})$ 的另一个基底元素 $H$。这个非零的结果表明，由 $X$ 和 $Y$ 生成的无穷小变换是不可交换的。

抽象地说，一个[李代数](@entry_id:137954)是一个[向量空间](@entry_id:151108) $\mathfrak{g}$ 配备了一个[二元运算](@entry_id:152272) $[\cdot, \cdot]: \mathfrak{g} \times \mathfrak{g} \to \mathfrak{g}$，满足以下公理：
1.  **[双线性性](@entry_id:146819)**：对所有 $a, b \in \mathbb{R}$ 和 $X, Y, Z \in \mathfrak{g}$，有 $[aX+bY, Z] = a[X,Z] + b[Y,Z]$ 和 $[Z, aX+bY] = a[Z,X] + b[Z,Y]$。
2.  **反交换性**：对所有 $X, Y \in \mathfrak{g}$，有 $[X, Y] = -[Y, X]$。这意味着 $[X, X] = 0$。
3.  **雅可比恒等式**：对所有 $X, Y, Z \in \mathfrak{g}$，有 $[X, [Y, Z]] + [Y, [Z, X]] + [Z, [X, Y]] = 0$。

雅可比恒等式是李括号作为导子的性质的体现，它确保了李[代数结构](@entry_id:137052)的自洽性。

### [结构常数](@entry_id:157960)与伴随表示

李代数的完整结构可以通过其在一组基底下的李括号运算来描述。对于一个[李代数](@entry_id:137954) $\mathfrak{g}$，如果我们选取一组基底 $\{X_1, X_2, \dots, X_n\}$，那么任意两个基底元素的李括号必定可以表示为这组基底的[线性组合](@entry_id:154743)：

$$
[X_i, X_j] = \sum_{k=1}^{n} c^k_{ij} X_k
$$

这里的系数 $c^k_{ij}$ 被称为[李代数](@entry_id:137954)的**[结构常数](@entry_id:157960)（structure constants）**。它们唯一地确定了[李代数](@entry_id:137954)的乘法结构，并且依赖于基底的选择。反交换性意味着 $c^k_{ij} = -c^k_{ji}$，而[雅可比恒等式](@entry_id:140480)则对[结构常数](@entry_id:157960)施加了更复杂的二次关系。

让我们看一个计算[结构常数](@entry_id:157960)的例子。考虑一维仿射群 $\text{Aff}(1, \mathbb{R})$ 对应的[李代数](@entry_id:137954) $\mathfrak{aff}(1, \mathbb{R})$。假设我们选定了一个非标准的基底 [@problem_id:1523082]：
$$
X_1 = \begin{pmatrix} 3  2 \\ 0  0 \end{pmatrix}, \quad X_2 = \begin{pmatrix} 1  -4 \\ 0  0 \end{pmatrix}
$$
我们来计算 $[X_1, X_2]$：
$$
[X_1, X_2] = X_1 X_2 - X_2 X_1 = \begin{pmatrix} 3  -12 \\ 0  0 \end{pmatrix} - \begin{pmatrix} 3  2 \\ 0  0 \end{pmatrix} = \begin{pmatrix} 0  -14 \\ 0  0 \end{pmatrix}
$$
现在，我们需要将这个结果表示为 $X_1$ 和 $X_2$ 的[线性组合](@entry_id:154743)：$[X_1, X_2] = c^1_{12} X_1 + c^2_{12} X_2$。
$$
\begin{pmatrix} 0  -14 \\ 0  0 \end{pmatrix} = c^1_{12} \begin{pmatrix} 3  2 \\ 0  0 \end{pmatrix} + c^2_{12} \begin{pmatrix} 1  -4 \\ 0  0 \end{pmatrix} = \begin{pmatrix} 3c^1_{12} + c^2_{12}  2c^1_{12} - 4c^2_{12} \\ 0  0 \end{pmatrix}
$$
这给出了一个线性方程组：
$3c^1_{12} + c^2_{12} = 0$
$2c^1_{12} - 4c^2_{12} = -14$
解得 $c^1_{12} = -1$ 和 $c^2_{12} = 3$。因此，在这个特定基底下，我们找到了其中一个[结构常数](@entry_id:157960) $c^2_{12}=3$。

研究李[代数结构](@entry_id:137052)的一个极其有力的工具是**伴随表示（adjoint representation）**。对于[李代数](@entry_id:137954) $\mathfrak{g}$中的任意元素 $X$，我们可以定义一个从 $\mathfrak{g}$到自身的[线性映射](@entry_id:185132) $\text{ad}_X$，其定义为：

$$
\text{ad}_X(Y) = [X, Y]
$$

由于 $\text{ad}_X$ 是一个[线性变换](@entry_id:149133)，一旦我们选定 $\mathfrak{g}$ 的一个基底，就可以将其表示为一个矩阵。这个矩阵的第 $j$ 列是 $\text{ad}_X$ 作用在第 $j$ 个[基向量](@entry_id:199546)上的结果在该基底下的坐标。

例如，我们来构建 $\mathfrak{sl}(2, \mathbb{R})$ 中元素 $H = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$ 的伴随表示矩阵。我们使用基底 $\mathcal{B} = (E, F, H)$ [@problem_id:1523104]。我们需要计算 $H$ 与每个[基向量](@entry_id:199546)的[李括号](@entry_id:636461)：
$$
\text{ad}_H(E) = [H, E] = HE - EH = E - (-E) = 2E = 2E + 0F + 0H
$$
$$
\text{ad}_H(F) = [H, F] = HF - FH = -F - F = -2F = 0E - 2F + 0H
$$
$$
\text{ad}_H(H) = [H, H] = 0 = 0E + 0F + 0H
$$
将结果 $(2,0,0)$, $(0,-2,0)$, $(0,0,0)$ 作为列向量，我们得到 $\text{ad}_H$ 在基底 $\mathcal{B}$ 下的[矩阵表示](@entry_id:146025)：
$$
M_H = \begin{pmatrix} 2  0  0 \\ 0  -2  0 \\ 0  0  0 \end{pmatrix}
$$
这个矩阵 $M_H$ 完整地描述了 $H$ 通过李括号运算对整个代数的作用。

伴随表示本身也构成一个[李代数表示](@entry_id:196776)，这意味着映射 $X \mapsto \text{ad}_X$ 保持李括号结构，即 $\text{ad}_{[X,Y]} = [\text{ad}_X, \text{ad}_Y]$，其中右侧是映射（矩阵）的对易子 [@problem_id:1523106]。这为研究李代数的内在对称性提供了深刻的见解。

### 更深层次的联系：[BCH公式](@entry_id:197600)与全局拓扑

[李代数](@entry_id:137954)与李群之间的联系通过**Baker-Campbell-Hausdorff (BCH) 公式**得到了最精确的阐述。这个公式给出了 $\log(\exp(X)\exp(Y))$ 的一个级数展开，其表达式完全由 $X$ 和 $Y$ 的[李括号](@entry_id:636461)以及嵌套[李括号](@entry_id:636461)构成：

$$
\log(\exp(X)\exp(Y)) = X + Y + \frac{1}{2}[X,Y] + \frac{1}{12}[X,[X,Y]] - \frac{1}{12}[Y,[X,Y]] + \dots
$$

这个公式表明，群的乘法结构在局部完全由其李代数的李括号结构决定。对于可交换的[李代数](@entry_id:137954)（$[X,Y]=0$），[BCH公式](@entry_id:197600)简化为 $X+Y$，此时[指数映射](@entry_id:137184)是一个局部同态。然而，当李括号非零时，它贡献了对群乘法[非对易性](@entry_id:153545)的[一阶修正](@entry_id:155896)。

一个能清晰展示此效应的例子是[海森堡代数](@entry_id:204103) $\mathfrak{h}_3$，它由如下形式的 $3 \times 3$ 矩阵构成：
$$
\begin{pmatrix} 0  a  c \\ 0  0  b \\ 0  0  0 \end{pmatrix}
$$
这是一个**二步幂零（2-step nilpotent）**代数，意味着任何三个元素的嵌套李括号都为零。在这种情况下，[BCH公式](@entry_id:197600)会截断。对于 $X, Y \in \mathfrak{h}_3$ 且 $[X,[X,Y]]=[Y,[X,Y]]=0$，公式精确地变为：$\exp(X)\exp(Y) = \exp(X+Y + \frac{1}{2}[X,Y])$。

我们可以用这个精确形式来衡量群的非对易性。考虑 $X = \begin{pmatrix} 0  \alpha  0 \\ 0  0  0 \\ 0  0  0 \end{pmatrix}$ 和 $Y = \begin{pmatrix} 0  0  0 \\ 0  0  \beta \\ 0  0  0 \end{pmatrix}$ [@problem_id:1523068]。它们的李括号是 $[X,Y] = \alpha\beta \begin{pmatrix} 0  0  1 \\ 0  0  0 \\ 0  0  0 \end{pmatrix}$。由于 $[X,Y]$ 与 $X$ 和 $Y$ 的[李括号](@entry_id:636461)都为零，我们可以应用截断的[BCH公式](@entry_id:197600)。衡量非对易性的量 $M = (\exp(X+Y))^{-1} \exp(X) \exp(Y)$ 可以计算如下：
$$
\begin{align*}
M &= \exp(-(X+Y)) \exp(X+Y + \frac{1}{2}[X,Y]) \\
&= \exp\left(-(X+Y) + (X+Y + \frac{1}{2}[X,Y])\right) \\
&= \exp\left(\frac{1}{2}[X,Y]\right)
\end{align*}
$$
这里我们用到了当 $[A,B]=0$ 时 $\exp(A)\exp(B)=\exp(A+B)$ 的性质。代入 $[X,Y]$ 并展开指数（因为 $([X,Y])^2=0$），我们得到：
$$
M = I + \frac{1}{2}[X,Y] = \begin{pmatrix} 1  0  \frac{1}{2}\alpha\beta \\ 0  1  0 \\ 0  0  1 \end{pmatrix}
$$
因此，矩阵 $M$ 的 $(1,3)$ 元 $M_{13} = \frac{1}{2}\alpha\beta$，它直接由[李括号](@entry_id:636461)决定。

然而，李代数只捕捉了李群的**局部**信息。具有同构李代数的[李群](@entry_id:137659)在**全局拓扑**上可能有显著差异。一个经典的例子是旋转群 $SO(2)$ 和实数[加法群](@entry_id:151801) $\mathbb{R}$ [@problem_id:1523066]。它们的[李代数](@entry_id:137954)都是一维的（因此同构于 $\mathbb{R}$，其李括号为零）。但是，$SO(2)$ 在拓扑上是一个圆 $S^1$，是**紧致（compact）**的（即闭合且有界）。而 $\mathbb{R}$ 是非紧致的。由于紧致性是[拓扑不变量](@entry_id:138526)，任何同胚（更不用说李[群同构](@entry_id:147371)所要求的微分同胚）都必须保持它。因此，$SO(2)$ 和 $\mathbb{R}$不可能是同构的[李群](@entry_id:137659)。

这种全局性质的差异能否通过[李代数](@entry_id:137954)的结构来探测呢？答案部分是肯定的，通过**[基灵型](@entry_id:161046)（Killing form）**可以实现。[基灵型](@entry_id:161046)是李代数上一个內蕴的[对称双线性形式](@entry_id:148281)，定义为：
$$
K(X, Y) = \text{tr}(\text{ad}_X \text{ad}_Y)
$$
[基灵型](@entry_id:161046)是[李代数](@entry_id:137954)的一个深刻[不变量](@entry_id:148850)，它不依赖于基底的选择。

**嘉当紧致性判据（Cartan's criterion for compactness）**指出：一个连通半单李群是紧致的，当且仅当其李代数上的[基灵型](@entry_id:161046)是**负定（negative definite）**的。

我们可以通过两个例子来验证这一点 [@problem_id:1678766]。
1.  **[紧致群](@entry_id:146287) SU(2)**：其[李代数](@entry_id:137954) $\mathfrak{su}(2)$ 的[基灵型](@entry_id:161046)可以计算出来是负定的。例如，在一个标准基底下，其[矩阵表示](@entry_id:146025)为 $\text{diag}(-2, -2, -2)$。
2.  **非[紧致群](@entry_id:146287) SL(2, $\mathbb{R}$)**：其李代数 $\mathfrak{sl}(2, \mathbb{R})$ 的[基灵型](@entry_id:161046)是**不定（indefinite）**的，拥有正、负[特征值](@entry_id:154894)（例如，在一个标准基底下，其矩阵表示的[特征值](@entry_id:154894)为 $\{8, 4, -4\}$）。

这个强大的结果揭示了[李代数](@entry_id:137954)的纯[代数结构](@entry_id:137052)（通过伴随表示和迹运算定义的[基灵型](@entry_id:161046)）如何蕴含了其对应[李群](@entry_id:137659)深刻的全局拓扑性质。它标志着我们从理解李群与[李代数](@entry_id:137954)的基本机制，迈向了利用代数工具解决几何与拓扑问题的更高层面。