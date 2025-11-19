## 引言
李群，作为同时具备光滑流形结构和群结构的数学对象，是描述自然界中[连续对称性](@entry_id:137257)的通用语言。从[刚体转动](@entry_id:191086)到基本粒子的[内禀对称性](@entry_id:168727)，[李群](@entry_id:137659)无处不在。然而，其[非线性](@entry_id:637147)的几何与[代数结构](@entry_id:137052)交织在一起，使得直接研究颇具挑战。本文旨在解决这一难题，通过引入其“线性化”的对应物——[李代数](@entry_id:137954)，来揭示李群的深刻内涵。

本文将引导读者踏上一段从具体到抽象、从理论到应用的探索之旅。在第一章“原理与机制”中，我们将学习如何从李群出发，通过“求导”得到其在[单位元处的切空间](@entry_id:266468)，即李代数，并探索如何通过[指数映射](@entry_id:137184)反向构建群的局部结构。我们将深入理解李括号如何捕捉群的[非交换性](@entry_id:153545)。随后，在第二章“应用与跨学科联系”中，我们将见证这些抽象概念在理论物理、[微分几何](@entry_id:145818)等领域的强大威力，看它们如何成为解决实际问题的关键工具。最后，“实践练习”部分将提供具体的计算问题，帮助读者巩固所学知识，亲身体验理论的运作方式。通过这趟旅程，读者将掌握连接宏观群结构与微观[代数结构](@entry_id:137052)的桥梁，从而能够运用[李群](@entry_id:137659)和[李代数](@entry_id:137954)这一强大框架来分析复杂的对称性问题。

## 原理与机制

在前一章介绍李群作为同时是群和[光滑流形](@entry_id:160799)的迷人对象之后，本章将深入探讨其核心原理和机制。我们将探索如何从一个李群中提取其“无穷小”结构，即李代数，并研究这种[代数结构](@entry_id:137052)如何反过来决定了群的局部性质。这一深刻的联系是理解连续对称性的关键。我们将从[矩阵李群](@entry_id:145968)的具体例子入手，逐步建立起[李群](@entry_id:137659)与其对应李代数之间的基本桥梁。

### 从群到代数：[单位元处的切空间](@entry_id:266468)

李群的本质在于其光滑的几何结构与[代数结构](@entry_id:137052)完美融合。为了研究这种结构，我们从分析群在单位元（identity element）附近的性质开始。[李群](@entry_id:137659) $G$ 在其单位元 $e$ 处的[切空间](@entry_id:199137)，记为 $T_eG$，是一个[向量空间](@entry_id:151108)。这个[切空间](@entry_id:199137)，被赋予一个额外的[代数结构](@entry_id:137052)后，就构成了[李群](@entry_id:137659) $G$ 的 **李代数（Lie algebra）**，通常用对应的小写哥特字母 $\mathfrak{g}$ 表示。

那么，这个[切空间](@entry_id:199137)中的向量究竟是什么呢？在[矩阵李群](@entry_id:145968)（即元素为矩阵的[李群](@entry_id:137659)）的语境下，这个概念变得非常直观。李代数 $\mathfrak{g}$ 的元素可以被看作是矩阵，它们是群中通过单位元的“路径”的“速度”向量。

更形式地说，考虑 $G$ 中的一条光滑曲线 $g(t)$，其中 $t$ 是一个实数参数，且满足 $g(0) = e$。这条曲线在 $t=0$ 处的[切向量](@entry_id:265494)就是对 $t$ 求导并在 $t=0$ 处取值：

$$
X = \left. \frac{d}{dt} g(t) \right|_{t=0}
$$

这个矩阵 $X$ 就是[李代数](@entry_id:137954) $\mathfrak{g}$ 的一个元素。特别重要的一类曲线是**[单参数子群](@entry_id:181957)（one-parameter subgroups）**，它们是光滑的[群同态](@entry_id:140603) $g: (\mathbb{R}, +) \to G$。这意味着它们满足 $g(t_1 + t_2) = g(t_1)g(t_2)$ 且 $g(0) = e$。[李代数](@entry_id:137954)中的每一个元素 $X$ 都唯一地确定一个[单参数子群](@entry_id:181957)，这个元素 $X$ 被称为该[子群](@entry_id:146164)的**生成元（generator）**。

让我们通过一个具体的例子来阐明这一点。考虑一个描述二维空间中变换的单参数矩阵族 [@problem_id:1523128]：

$$
g(t) = \begin{pmatrix} \cosh t  \sinh t \\ \sinh t  \cosh t \end{pmatrix}
$$

这里 $t \in \mathbb{R}$，$\cosh t$ 和 $\sinh t$ 分别是双曲余弦和[双曲正弦函数](@entry_id:167630)。不难验证 $g(0) = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} = I$，即单位元。为了找到这个[单参数子群](@entry_id:181957)的生成元，我们计算其在 $t=0$ 处的导数：

$$
X = \left. \frac{d}{dt} g(t) \right|_{t=0} = \left. \begin{pmatrix} \sinh t  \cosh t \\ \cosh t  \sinh t \end{pmatrix} \right|_{t=0} = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}
$$

因此，矩阵 $X = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$ 是这个李群的李代数中的一个元素。它捕捉了群在单位元附近沿 $g(t)$ 方向的无穷小行为。这种从群到代数的“求导”过程，使我们能够用线性代数的工具——[向量空间](@entry_id:151108)和矩阵——来研究复杂的[非线性](@entry_id:637147)[群结构](@entry_id:146855)。

### 从代数到群：[指数映射](@entry_id:137184)

我们已经看到如何通过求导从李群得到其[李代数](@entry_id:137954)。一个自然的问题是：我们能否逆转这个过程？给定一个李代数元素 $X$，我们能否重建它生成的（至少是局部的）群？答案是肯定的，其关键工具是**[指数映射](@entry_id:137184)（exponential map）**。

对于一个[矩阵李代数](@entry_id:204591) $\mathfrak{g}$，[指数映射](@entry_id:137184) $\exp: \mathfrak{g} \to G$ 对于任意 $X \in \mathfrak{g}$ 定义为标准的矩阵指数：

$$
\exp(X) = \sum_{k=0}^{\infty} \frac{X^k}{k!} = I + X + \frac{X^2}{2!} + \frac{X^3}{3!} + \dots
$$

这个映射将李代数中的一个“无穷小生成元” $X$ 转换为李群中的一个“有限”变换 $\exp(X)$。事实上，由生成元 $X$ 产生的[单参数子群](@entry_id:181957) $g(t)$ 正是由 $g(t) = \exp(tX)$ 给出的。指数映射因此构成了从代数到群的桥梁。

让我们来看一个经典的例子：平面旋转群 $SO(2)$ [@problem_id:1523125]。这个群由所有形如 $\begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix}$ 的 $2 \times 2$ [旋转矩阵](@entry_id:140302)构成。其李代数 $\mathfrak{so}(2)$ 是所有 $2 \times 2$ 实反对称矩阵的集合。这个代数是一维的，其一个典型基元（生成元）是：

$$
X = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}
$$

这个矩阵 $X$ 代表了一个无穷小的逆时针旋转。为了得到一个有限的旋转角度 $\theta$，我们计算 $\exp(\theta X)$。为此，我们先计算 $X$ 的幂：

$X^0 = I = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}$

$X^1 = X = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$

$X^2 = \begin{pmatrix} -1  0 \\ 0  -1 \end{pmatrix} = -I$

$X^3 = -X$

$X^4 = I$

这个幂次序列以 4 为周期循环。现在，我们将指数级数展开，并按 $I$ 和 $X$ 分组：

$$
\exp(\theta X) = \sum_{n=0}^{\infty} \frac{(\theta X)^n}{n!} = \left( 1 - \frac{\theta^2}{2!} + \frac{\theta^4}{4!} - \dots \right)I + \left( \theta - \frac{\theta^3}{3!} + \frac{\theta^5}{5!} - \dots \right)X
$$

我们立刻认出括号中的级数是 $\cos\theta$ 和 $\sin\theta$ 的[泰勒展开](@entry_id:145057)。因此：

$$
\exp(\theta X) = (\cos\theta)I + (\sin\theta)X = \cos\theta\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + \sin\theta\begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix} = \begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix}
$$

这正是 $SO(2)$ 中的一个通用旋转矩阵！这个计算完美地展示了指数映射如何从一个无穷小生成元重建整个[单参数子群](@entry_id:181957)，从而揭示了李代数作为[李群](@entry_id:137659)“蓝图”的深刻作用。

### [李括号](@entry_id:636461)：捕捉群的结构

[李代数](@entry_id:137954)不仅仅是一个[向量空间](@entry_id:151108)，它还有一个额外的结构，使其成为一个真正的“代数”。这个结构就是**李括号（Lie bracket）**，记为 $[X, Y]$。李括号是一个双线性运算，它捕捉了李群乘法的[非交换性](@entry_id:153545)。如果群是交换的（abelian），其李代数的[李括号](@entry_id:636461)恒为零。

从根本上说，[李括号](@entry_id:636461)是从群的几何结构中产生的。对于李群 $G$ 上的任意一个[李代数](@entry_id:137954)元素 $A \in \mathfrak{g}$，我们可以定义一个遍布全群的[左不变向量场](@entry_id:637116) $X_A$。李括号 $[A, B]$ 被定义为与[向量场的李括号](@entry_id:193400) $[X_A, X_B]$ 在单位元处对应的值。

幸运的是，对于[矩阵李群](@entry_id:145968)，这个看似抽象的定义有一个极其简单的等价形式。[李括号](@entry_id:636461)就是**矩阵[交换子](@entry_id:158878)（matrix commutator）**：

$$
[A, B] = AB - BA
$$

其中 $A, B \in \mathfrak{g}$。我们可以通过显式计算向量场来验证这一点。例如，在 $GL(2, \mathbb{R})$ 中，与矩阵 $A$ 相关的[左不变向量场](@entry_id:637116)算子是 $X_A = \sum_{i,j} (gA)_{ij} \frac{\partial}{\partial x_{ij}}$。通过计算 $X_A(X_B(f)) - X_B(X_A(f))$ 并求其在单位元处的值，可以证明它恰好对应于矩阵 $C = AB - BA$ [@problem_id:1678771]。这一结果至关重要，因为它允许我们在处理[矩阵李群](@entry_id:145968)时，将[李括号](@entry_id:636461)的计算简化为简单的[矩阵乘法](@entry_id:156035)和减法。

[李括号](@entry_id:636461)必须满足以下三个基本性质：
1.  **[双线性](@entry_id:146819)（Bilinearity）**: $[aX+bY, Z] = a[X,Z] + b[Y,Z]$ 和 $[X, aY+bZ] = a[X,Y] + b[X,Z]$。
2.  **反对称性（Anti-symmetry）**: $[X, Y] = -[Y, X]$。这意味着 $[X, X] = 0$。
3.  **[雅可比恒等式](@entry_id:140480)（Jacobi Identity）**: $[X, [Y, Z]] + [Y, [Z, X]] + [Z, [X, Y]] = 0$。

[雅可比恒等式](@entry_id:140480)是李括号最关键的性质，它类似于乘法[结合律](@entry_id:151180)的某种推广，并确保了[李代数](@entry_id:137954)具有一致的[代数结构](@entry_id:137052)。

### 李代数的结构：基与[结构常数](@entry_id:157960)

由于[李代数](@entry_id:137954)是一个[向量空间](@entry_id:151108)，我们可以为其选择一组基 $\{X_1, X_2, \dots, X_n\}$，其中 $n$ 是代数的维数。由于李括号运算的**[闭包](@entry_id:148169)性**，任意两个[基向量](@entry_id:199546)的李括号仍然是该[李代数](@entry_id:137954)的一个元素，因此可以表示为[基向量](@entry_id:199546)的线性组合：

$$
[X_i, X_j] = \sum_{k=1}^{n} c^k_{ij} X_k
$$

这里的系数 $c^k_{ij}$ 被称为[李代数](@entry_id:137954)在该基下的**[结构常数](@entry_id:157960)（structure constants）**。这些常数完全编码了[李代数](@entry_id:137954)的[代数结构](@entry_id:137052)。一旦我们知道了所有[基向量](@entry_id:199546)之间的括号关系，我们就可以通过双线性计算出任意两个元素之间的括号。

让我们通过计算一维仿射群 $Aff(1, \mathbb{R})$ 的[李代数](@entry_id:137954) $\mathfrak{aff}(1, \mathbb{R})$ 的[结构常数](@entry_id:157960)来理解这个概念 [@problem_id:1523082]。假设我们为这个二维李代数选择了一组非标准的基：

$$
X_1 = \begin{pmatrix} 3  2 \\ 0  0 \end{pmatrix}, \quad X_2 = \begin{pmatrix} 1  -4 \\ 0  0 \end{pmatrix}
$$

我们想计算 $[X_1, X_2] = c^1_{12}X_1 + c^2_{12}X_2$ 中的[结构常数](@entry_id:157960) $c^2_{12}$。首先，计算交换子：

$$
[X_1, X_2] = X_1 X_2 - X_2 X_1 = \begin{pmatrix} 3  2 \\ 0  0 \end{pmatrix}\begin{pmatrix} 1  -4 \\ 0  0 \end{pmatrix} - \begin{pmatrix} 1  -4 \\ 0  0 \end{pmatrix}\begin{pmatrix} 3  2 \\ 0  0 \end{pmatrix}
$$

$$
= \begin{pmatrix} 3  -12 \\ 0  0 \end{pmatrix} - \begin{pmatrix} 3  2 \\ 0  0 \end{pmatrix} = \begin{pmatrix} 0  -14 \\ 0  0 \end{pmatrix}
$$

接下来，我们将结果表示为 $X_1$ 和 $X_2$ 的[线性组合](@entry_id:154743)：

$$
\begin{pmatrix} 0  -14 \\ 0  0 \end{pmatrix} = c^1_{12} \begin{pmatrix} 3  2 \\ 0  0 \end{pmatrix} + c^2_{12} \begin{pmatrix} 1  -4 \\ 0  0 \end{pmatrix} = \begin{pmatrix} 3c^1_{12} + c^2_{12}  2c^1_{12} - 4c^2_{12} \\ 0  0 \end{pmatrix}
$$

通过比较[矩阵元](@entry_id:186505)素，我们得到一个线性方程组：
$3c^1_{12} + c^2_{12} = 0$
$2c^1_{12} - 4c^2_{12} = -14$

解这个[方程组](@entry_id:193238)得到 $c^1_{12} = -1$ 和 $c^2_{12} = 3$。因此，所求的[结构常数](@entry_id:157960)为 $3$。

在李代数中，我们还关心其子结构。一个子[向量空间](@entry_id:151108) $\mathfrak{h} \subset \mathfrak{g}$ 如果对[李括号](@entry_id:636461)运算封闭（即对所有 $X, Y \in \mathfrak{h}$，都有 $[X, Y] \in \mathfrak{h}$），则称其为**李子代数（Lie subalgebra）**。一个更强的概念是**理想（ideal）**。一个子代数 $\mathfrak{h}$ 如果对所有 $X \in \mathfrak{g}$ 和 $Y \in \mathfrak{h}$，都有 $[X, Y] \in \mathfrak{h}$，则称其为理想。例如，所有 $n \times n$ 迹为零的矩阵构成的[李代数](@entry_id:137954) $\mathfrak{sl}(n, \mathbb{R})$ 是所有 $n \times n$ 矩阵的李代数 $\mathfrak{gl}(n, \mathbb{R})$ 的一个理想 [@problem_id:1523085]。这是因为对于任意 $X \in \mathfrak{gl}(n, \mathbb{R})$ 和 $Y \in \mathfrak{sl}(n, \mathbb{R})$（即 $\operatorname{tr}(Y) = 0$），它们的交换子的迹为：

$$
\operatorname{tr}([X, Y]) = \operatorname{tr}(XY - YX) = \operatorname{tr}(XY) - \operatorname{tr}(YX) = 0
$$

由于[迹的循环性质](@entry_id:153103)，$[X, Y]$ 的迹也为零，所以 $[X, Y] \in \mathfrak{sl}(n, \mathbb{R})$。这证明了 $\mathfrak{sl}(n, \mathbb{R})$ 是 $\mathfrak{gl}(n, \mathbb{R})$ 的一个理想。

### 表示：伴随映射

为了更深入地理解李代数的结构，我们常常将其“表示”为我们更熟悉的线性变换（即矩阵）。李代数 $\mathfrak{g}$ 的一个**表示（representation）** 是一个从 $\mathfrak{g}$ 到某个[向量空间](@entry_id:151108) $V$ 上的线性变换代数 $\mathfrak{gl}(V)$ 的[李代数](@entry_id:137954)同态。

每个李代数都有一个与生俱来的、作用于其自身的表示，称为**伴随表示（adjoint representation）**。对于 $\mathfrak{g}$ 中的每一个元素 $X$，我们定义一个[线性映射](@entry_id:185132) $\text{ad}_X: \mathfrak{g} \to \mathfrak{g}$，其作用方式为：

$$
\text{ad}_X(Y) = [X, Y]
$$

这个映射 $\text{ad}_X$ 本身是[李代数](@entry_id:137954) $\mathfrak{g}$ 上的一个[线性算子](@entry_id:149003)。如果我们为 $\mathfrak{g}$ 选择一个基，我们就可以将 $\text{ad}_X$ 表示为一个矩阵。

让我们以三维[李代数](@entry_id:137954) $\mathfrak{sl}(2, \mathbb{R})$（所有 $2 \times 2$ 实数迹零矩阵）为例 [@problem_id:1523104]。它的一组标准基是：

$$
E = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}, \quad F = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}, \quad H = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$

我们来求 $\text{ad}_H$ 在基 $(E, F, H)$ 下的[矩阵表示](@entry_id:146025)。为此，我们计算 $H$ 与每个[基向量](@entry_id:199546)的[李括号](@entry_id:636461)：

$\text{ad}_H(E) = [H, E] = HE - EH = 2E = 2E + 0F + 0H$
$\text{ad}_H(F) = [H, F] = HF - FH = -2F = 0E - 2F + 0H$
$\text{ad}_H(H) = [H, H] = 0 = 0E + 0F + 0H$

这些结果的[坐标向量](@entry_id:153319) $(2, 0, 0)^T$, $(0, -2, 0)^T$, $(0, 0, 0)^T$ 构成了 $\text{ad}_H$ 的[矩阵表示](@entry_id:146025)的列。因此，该矩阵为：

$$
[\text{ad}_H] = \begin{pmatrix} 2  0  0 \\ 0  -2  0 \\ 0  0  0 \end{pmatrix}
$$

更进一步，映射 $X \mapsto \text{ad}_X$ 本身就是一个[李代数表示](@entry_id:196776)，这意味着它保持[李括号](@entry_id:636461)结构：

$$
\text{ad}_{[X, Y]} = [\text{ad}_X, \text{ad}_Y]
$$

这里的右边是[线性算子](@entry_id:149003)（或其[矩阵表示](@entry_id:146025)）的[交换子](@entry_id:158878)。这个重要的属性直接源于[雅可比恒等式](@entry_id:140480)。我们可以通过计算来验证它。例如，在 $\mathfrak{sl}(2, \mathbb{R})$ 中，我们可以计算出 $\text{ad}_E$ 和 $\text{ad}_H$ 的矩阵表示，然后计算它们的矩阵交换子，结果会与 $\text{ad}_{[E,H]}$ 的矩阵表示相符 [@problem_id:1523106]。伴随表示在李群和李代数的理论中扮演着核心角色，它将抽象的[代数结构](@entry_id:137052)与具体的[矩阵代数](@entry_id:153824)联系起来。

### 局部[群结构](@entry_id:146855)：[Baker-Campbell-Hausdorff公式](@entry_id:197600)

我们已经建立了李群与[李代数](@entry_id:137954)之间的基本对应关系：指数映射从代数到群，求导从群到代数。现在我们来探讨一个更精细的问题：[李群](@entry_id:137659)的乘法运算如何在其[李代数](@entry_id:137954)中反映出来？

给定两个[李代数](@entry_id:137954)元素 $X$ 和 $Y$，我们知道 $\exp(tX)$ 和 $\exp(tY)$ 是群中的元素。它们的乘积 $\exp(tX)\exp(tY)$ 也是群中的一个元素。由于指数映射在单位元附近是可逆的，这个乘积可以写成 $\exp(Z)$ 的形式，其中 $Z$ 是[李代数](@entry_id:137954)中的某个元素。**Baker-Campbell-Hausdorff (BCH) 公式**给出了 $Z$ 的一个表达式，完全由 $X$ 和 $Y$ 以及它们的迭代李括号构成。

完整的[BCH公式](@entry_id:197600)相当复杂，但其最重要的部分是低阶项，它揭示了群乘法与代数运算之间的深刻联系。截断到二阶项，公式为：

$$
Z = \log(\exp(X)\exp(Y)) = X + Y + \frac{1}{2}[X, Y] + \dots (\text{高阶项})
$$

这个公式告诉我们，在无穷小尺度上（即当 $X$ 和 $Y$ 很小时），群的乘法近似于[李代数](@entry_id:137954)中的[向量加法](@entry_id:155045)。[李括号](@entry_id:636461)项 $\frac{1}{2}[X, Y]$ 则是对这种近似的第一个修正，它精确地量化了由于群的[非交换性](@entry_id:153545)而产生的偏差。

考虑 $SO(3)$ 中的小旋转 [@problem_id:3056606]。其李代数 $\mathfrak{so}(3)$ 的基 $E_1, E_2, E_3$ 分别对应于围绕 $x, y, z$ 轴的[无穷小旋转](@entry_id:166635)，并满足 $[E_i, E_j] = \varepsilon_{ijk} E_k$。设 $X = \alpha E_1$ 是一个绕 $x$ 轴的微小旋转，而 $Y = \beta E_2$ 是一个绕 $y$ 轴的微小旋转。它们复合后的结果是什么？

使用[BCH公式](@entry_id:197600)的[二阶近似](@entry_id:141277)：

$$
Z \approx X + Y + \frac{1}{2}[X, Y] = \alpha E_1 + \beta E_2 + \frac{1}{2}[\alpha E_1, \beta E_2]
$$

利用[李括号](@entry_id:636461)的双线性和 $\mathfrak{so}(3)$ 的结构关系 $[E_1, E_2] = E_3$：

$$
Z \approx \alpha E_1 + \beta E_2 + \frac{\alpha\beta}{2} E_3
$$

这个结果非常直观：首先执行一个绕 $x$ 轴的微小旋转，然后执行一个绕 $y$ 轴的微小旋转，其结果近似为一个绕 $x$ 轴的旋转 $\alpha$、一个绕 $y$ 轴的旋转 $\beta$，外加一个绕 $z$ 轴的、量级为二阶小量 $\frac{\alpha\beta}{2}$ 的额外旋转。这个额外的 $E_3$ 项正是群乘法非交换性的直接体现，并由李括号精确捕捉。

### 局部与全局：整体图景

[李代数](@entry_id:137954)完美地捕捉了李群在单位元附近的**局部**结构。然而，李代数无法完全反映[李群](@entry_id:137659)的**全局**[拓扑性质](@entry_id:141605)。这意味着两个不同的[李群](@entry_id:137659)可能拥有同构的（即[代数结构](@entry_id:137052)完全相同的）李代数。

一个经典的例子是[旋转群](@entry_id:204412) $SO(2)$ 和实数加法群 $\mathbb{R}$ [@problem_id:1523066]。$SO(2)$ 的李代数 $\mathfrak{so}(2)$ 和 $\mathbb{R}$ 的[李代数](@entry_id:137954)（就是 $\mathbb{R}$ 本身）都是一维的，并且由于其中任意两个元素的李括号都为零（因为群是交换的），所以它们的李代数是同构的，都同构于具有零括号的 $\mathbb{R}$。

然而，这两个李群本身并不同构。一个根本性的区别在于它们的[拓扑性质](@entry_id:141605)：
- $SO(2)$ 在拓扑上是一个圆 $S^1$。它是一个**紧致（compact）**空间，因为它在欧氏空间中是闭合且有界的。
- $\mathbb{R}$ 在拓扑上是一条直线。它是一个**非紧致（non-compact）**空间，因为它是无界的。

由于[群同构](@entry_id:147371)必须是微分同胚，从而也是[同胚](@entry_id:146933)，它必须保持[拓扑性质](@entry_id:141605)，如紧致性。一个[紧致空间](@entry_id:155073)和一个非紧致空间不可能是[同胚](@entry_id:146933)的。因此，$SO(2)$ 和 $\mathbb{R}$ 不可能同构为[李群](@entry_id:137659)，尽管它们的局部结构（李代数）是相同的。

另一个更精妙的例子是[特殊酉群](@entry_id:138145) $SU(2)$ 和[特殊正交群](@entry_id:146418) $SO(3)$ [@problem_id:1678765]。这两个群在物理学和几何学中都至关重要。它们的李代数 $\mathfrak{su}(2)$ 和 $\mathfrak{so}(3)$ 是同构的。这个同构可以通过一个从 $SU(2)$ 到 $SO(3)$ 的[群同态](@entry_id:140603)（一个2对1的[覆盖映射](@entry_id:169347)）的[微分](@entry_id:158718)来建立。事实上，这个[微分](@entry_id:158718)映射 $d\pi_e: \mathfrak{su}(2) \to \mathfrak{so}(3)$ 与我们之前讨论的伴随表示密切相关。

尽管它们的李代数相同，$SU(2)$ 和 $SO(3)$ 作为李群并不同构。它们的全局拓扑性质不同：$SU(2)$ 在拓扑上是[三维球面](@entry_id:261323) $S^3$，它是**单连通的**（simply connected），意味着其中任何闭合回路都可以连续地收缩到一个点。而 $SO(3)$ 不是单连通的，它包含不能收缩的回路（例如，旋转 $360^\circ$ 的路径无法收缩，但旋转 $720^\circ$ 的路径可以）。

这些例子深刻地表明，李代数是研究[李群](@entry_id:137659)的强大工具，但它只揭示了故事的一部分。要完全理解一个[李群](@entry_id:137659)，我们必须将其[代数结构](@entry_id:137052)（由[李代数](@entry_id:137954)编码）与其全局拓扑结构结合起来。正是这种局部代数与全局拓扑的交织，赋予了[李群](@entry_id:137659)理论其独特的深度和魅力。