## 引言
向量场是贯穿现代数学与物理学的基本概念，从描述[流体运动](@entry_id:182721)的速度场、电磁学的[力场](@entry_id:147325)，到定义[微分方程](@entry_id:264184)的动力学流，其身影无处不在。然而，为了在弯曲的几何空间（即[光滑流形](@entry_id:160799)）上严谨地处理向量场，我们需要一个不依赖于特定[坐标系](@entry_id:156346)的内蕴定义。传统的、基于坐标分量的描述在坐标变换下显得繁琐且缺乏几何直观，这构成了我们理解其深层结构的知识鸿沟。

本文旨在填补这一鸿沟，系统地建立将向量场视为其[切丛](@entry_id:161294)（Tangent Bundle）的光滑[截面](@entry_id:154995)这一现代理念。这一视角不仅提供了一个优雅且坐标无关的定义，更重要的是，它揭示了向量场与[流形](@entry_id:153038)自身的拓扑、度量以及其他几何结构之间深刻而壮丽的联系。

在接下来的内容中，读者将踏上一段从局部到全局、从代数到几何的探索之旅：
*   在**“原理与机制”**一章中，我们将从单个切向量出发，构建切丛这一核心舞台，并正式将向量场定义为其光滑[截面](@entry_id:154995)。我们还将揭示向量场的双重身份——作为几何[截面](@entry_id:154995)与代数导子，并探讨其在坐标变换下的[不变性](@entry_id:140168)。
*   在**“应用与[交叉](@entry_id:147634)学科联系”**一章中，我们将展示这一理论框架的强大威力，探讨[黎曼度量](@entry_id:754359)和对称性如何催生出重要的向量场，研究李括号与协变导数等关键运算，并最终触及深刻的拓扑约束，如著名的“[毛球定理](@entry_id:151079)”。
*   最后，在**“动手实践”**部分，你将通过具体的计算和证明，将这些抽象的理论概念转化为扎实的解题能力。

现在，让我们首先深入探讨向量场作为[切丛截面](@entry_id:261939)的基本原理与机制，为后续的探索奠定坚实的基础。

## 原理与机制

继前一章对[光滑流形](@entry_id:160799)的基本介绍之后，本章将深入探讨其上一个至关重要的几何结构：向量场。从物理学中描述流体速度或[力场](@entry_id:147325)[分布](@entry_id:182848)，到几何学中定义[微分方程](@entry_id:264184)的流动，向量场的概念无处不在。我们将从[切丛](@entry_id:161294)的几何框架出发，系统地建立向量场作为其光滑[截面](@entry_id:154995)的现代理念，并揭示这一概念如何与[流形](@entry_id:153038)的[局部坐标](@entry_id:181200)表示、[代数结构](@entry_id:137052)以及深刻的全局拓扑性质紧密相连。

### 从切向量到[切丛](@entry_id:161294)

我们首先回顾切向量的概念。在[流形](@entry_id:153038) $M$ 上的任意一点 $p$，其**[切空间](@entry_id:199137)** $T_pM$ 是一个[向量空间](@entry_id:151108)，它捕捉了所有经过点 $p$ 的光滑曲线在该点的瞬时速度信息。更具体地说，任何一条光滑曲线 $\gamma: I \to M$（其中 $I \subseteq \mathbb{R}$ 是一个[开区间](@entry_id:157577)）且满足 $\gamma(0) = p$，其在 $t=0$ 的速度向量 $\gamma'(0)$ 就是 $T_pM$ 中的一个元素。反之，$T_pM$ 中的每一个向量都可以被某条穿过 $p$ 的曲线的速度向量所实现。

例如，考虑二维欧氏空间 $M = \mathbb{R}^2$，其上的一个向量场可以表示为 $X(x,y) = y \frac{\partial}{\partial x} - x \frac{\partial}{\partial y}$。这个向量场在每一点 $(x,y)$ 指定了一个方向和大小。若我们关注点 $p = (1, \pi)$，该点的切向量为 $X_p = X(1, \pi) = \pi \frac{\partial}{\partial x} - 1 \frac{\partial}{\partial y}$，在标准[坐标基](@entry_id:270149)下对应于向量 $(\pi, -1)$。一条曲线 $\gamma(t)$ 若要在 $p$ 点“实现”这个向量场，就必须满足两个条件：$\gamma(0) = p$ 且 $\gamma'(0) = X_p$。在众多穿过点 $(1, \pi)$ 的曲线中，例如曲线 $\gamma_B(t) = (1+\pi t, \pi - t)$ 就满足这两个条件，因为 $\gamma_B(0) = (1, \pi)$ 并且其速度向量 $\gamma_B'(t) = (\pi, -1)$ 在 $t=0$ 时恰好等于 $X_p$ [@problem_id:1688374]。这个例子直观地展示了向量场的核心作用：在[流形](@entry_id:153038)的每一点上精确地指定一个“运动趋势”。

为了系统地研究这种遍布于整个[流形](@entry_id:153038)之上的向量集合，我们需要引入**[切丛](@entry_id:161294) (Tangent Bundle)** 的概念。[切丛](@entry_id:161294) $TM$ 被定义为所有[切空间](@entry_id:199137)的**不交并 (disjoint union)**：
$$
TM = \bigsqcup_{p \in M} T_pM
$$
$TM$ 中的一个元素是一个偶对 $(p, v)$，其中 $p \in M$ 是基点，而 $v \in T_pM$ 是附着在该点的一个切向量。我们还有一个自然的**[投影映射](@entry_id:153398) (projection map)** $\pi: TM \to M$，它将任意一个[切向量](@entry_id:265494) $(p,v)$ 映射回其基点 $p$，即 $\pi(p,v) = p$。对于[流形](@entry_id:153038)上的任意一点 $p_0 \in M$，其在切丛中的**[原像](@entry_id:150899) (preimage)**，被称为在 $p_0$ 处的**纤维 (fiber)**，即是集合 $\pi^{-1}(p_0) = \{ (p_0, v) \mid v \in T_{p_0}M \}$。这个纤维与切空间 $T_{p_0}M$ 存在自然的同构关系，可以看作是[流形](@entry_id:153038)在 $p_0$ 点所有可能的“[切向量](@entry_id:265494)状态”的集合 [@problem_id:1688387]。

至关重要的是，$TM$ 本身不仅仅是一个集合，它具有一个自然的 $2n$ 维[光滑流形](@entry_id:160799)结构（假设 $M$ 是 $n$ 维的）。这个[光滑结构](@entry_id:159394)是通过 $M$ 上的图卡（atlas）来诱导的。对 $M$ 上的任意一个[坐标卡](@entry_id:262338) $(U, \varphi)$，其中 $\varphi: U \to \mathbb{R}^n$ 是一个同胚映射，我们可以为 $TM$ 定义一个对应的[坐标卡](@entry_id:262338) $(\pi^{-1}(U), \widetilde{\varphi})$。这个映射 $\widetilde{\varphi}: \pi^{-1}(U) \to \mathbb{R}^n \times \mathbb{R}^n$ 的定义如下：
$$
\widetilde{\varphi}(p, v) = (\varphi(p), d\varphi_p(v))
$$
这里，$p \in U$，$v \in T_pM$，$d\varphi_p: T_pM \to T_{\varphi(p)}\mathbb{R}^n \cong \mathbb{R}^n$ 是映射 $\varphi$ 在点 $p$ 的**[微分](@entry_id:158718) (differential)**。它将抽象的切向量 $v$ 映射为其在 $\mathbb{R}^n$ [坐标系](@entry_id:156346)下的分量表示。如果两个图卡 $(U, \varphi)$ 和 $(V, \psi)$ 在 $M$ 上重叠，那么它们在 $TM$ 上诱导的图卡之间的**转移映射 (transition map)** $\widetilde{\psi} \circ \widetilde{\varphi}^{-1}$ 也是光滑的。这个转移映射作用在一个点 $(x, \xi) \in \varphi(U \cap V) \times \mathbb{R}^n$ 上，其表达式为：
$$
(x, \xi) \longmapsto \Big(\psi \circ \varphi^{-1}(x), D(\psi \circ \varphi^{-1})(x) \cdot \xi\Big)
$$
其中 $D(\psi \circ \varphi^{-1})(x)$ 是 $M$ 上转移映射 $\psi \circ \varphi^{-1}$ 在点 $x$ 的[雅可比矩阵](@entry_id:264467)。由于 $M$ 是光滑流形，其转移映射是光滑的，因此该[雅可比矩阵](@entry_id:264467)的各项均是 $x$ 的光滑函数，从而保证了 $TM$ 上的转移映射也是光滑的。这样，$TM$ 就被赋予了一个良定义的[光滑流形](@entry_id:160799)结构 [@problem_id:3006127]。

### 作为光滑[截面](@entry_id:154995)的向量场

有了切丛 $TM$ 这个[光滑流形](@entry_id:160799)的舞台，我们可以给出向量场的现代几何定义。一个在[流形](@entry_id:153038) $M$ 上的**光滑向量场 (smooth vector field)** $X$ 是一个从 $M$ 到其[切丛](@entry_id:161294) $TM$ 的[光滑映射](@entry_id:203730)，并且它是一个**[截面](@entry_id:154995) (section)**。[截面](@entry_id:154995)条件指的是该映射 $X$ 必须满足：
$$
\pi \circ X = \text{id}_M
$$
其中 $\text{id}_M$ 是 $M$ 上的[恒等映射](@entry_id:634191)。这个条件等价于说，对于 $M$ 中的每一点 $p$，向量场在该点的值 $X(p)$ 必须是 $p$ 点自身的切空间 $T_pM$ 中的一个向量。换言之，一个向量场是在每个纤维 $\pi^{-1}(p)$ 中进行一次光滑的、一致性的选择。

例如，在 $M=\mathbb{R}^3$ 上，一个向量场 $X(x, y, z) = (z^2 \cos(x), x y - z, e^{y} + x)$ 对应的[截面](@entry_id:154995)映射为 $\sigma_X(p) = (p, X(p))$。对于点 $p_0 = (\pi, 0, -3)$，纤维 $\pi^{-1}(p_0)$ 是整个切空间 $T_{p_0}\mathbb{R}^3 \cong \mathbb{R}^3$。而[截面](@entry_id:154995) $\sigma_X$ 从这个无穷集合中挑选出了唯一一个向量：
$$
X(p_0) = ((-3)^2 \cos(\pi), \pi \cdot 0 - (-3), e^0 + \pi) = (-9, 3, 1+\pi)
$$
因此，[截面](@entry_id:154995)在该点的值是 $TM \cong \mathbb{R}^3 \times \mathbb{R}^3$ 中的点 $(\pi, 0, -3, -9, 3, 1+\pi)$ [@problem_id:1688387]。

必须强调，向量场 $X: M \to TM$ 与一条曲线的[速度图](@entry_id:195718) $V_\gamma: I \to TM$ 有着本质区别。向量场的定义域是整个[流形](@entry_id:153038) $M$（或其开[子集](@entry_id:261956)），而[速度图](@entry_id:195718)的定义域是时间区间 $I$。尽管[速度图](@entry_id:195718) $V_\gamma(t) = \gamma'(t)$ 的值也落在切丛中，但它描绘的是单个[质点](@entry_id:186768)沿轨迹 $\gamma(t)$ 运动时，其速度向量在切丛这个“相空间”中的演化轨迹，即一条位于 $TM$ 中的曲线。它不满足作为[截面](@entry_id:154995)的定义，因为它的定义域不是 $M$ [@problem_id:1688372]。

向量场的**光滑性 (smoothness)** 是其定义的核心部分。在[局部坐标](@entry_id:181200)卡 $(U, (x^1, \dots, x^n))$ 中，任何一个向量场 $X$ 都可以唯一地分解为[基向量](@entry_id:199546) $\{\frac{\partial}{\partial x^i}\}$ 的线性组合：
$$
X(p) = \sum_{i=1}^{n} X^i(p) \frac{\partial}{\partial x^i}\bigg|_p \quad \text{for } p \in U
$$
这里的 $X^i: U \to \mathbb{R}$ 被称为 $X$ 在该[坐标系](@entry_id:156346)下的**分量函数 (component functions)**。向量场 $X$ 的[光滑性](@entry_id:634843)被定义为其在任意光滑坐标卡下的所有分量函数 $X^i$ 都是光滑函数（即 $C^\infty$ 函数）。

考察一个具体例子可以加深对光滑性条件的理解。假设在 $\mathbb{R}^2$ 上定义一个向量场 $X$，其分量为：
$$ X^1(x, y) = \begin{cases} \exp\left(-\frac{1}{(x^2+y^2)^\alpha}\right)  \text{if } (x,y) \neq (0,0) \\ 0  \text{if } (x,y) = (0,0) \end{cases}, \quad X^2(x, y) = |x|^\beta $$
为了使 $X$ 在整个 $\mathbb{R}^2$ 上光滑，两个分量函数都必须是 $C^\infty$ 的。对于 $X^1$，只有当 $\alpha  0$ 时，函数在原点才是“平坦的”，即它和它的所有阶导数在原点都为零，从而保证了在原点的[光滑性](@entry_id:634843)。对于 $X^2$，函数 $|x|^\beta$ 要在 $x=0$ 处无限可微，$\beta$ 必须是一个非负偶数（例如 $|x|^2=x^2$, $|x|^4=x^4$ 等都是光滑的），否则在某阶导数上会出现不连续或不可导的情况。因此，该向量场 $X$ 光滑的充要条件是 $\alpha  0$ 且 $\beta$ 是一个非负偶数 [@problem_id:1688369]。

一个最基本的光滑向量场是**零向量场 (zero vector field)**，记作 $Z$，它将每一点 $p \in M$ 映射到该点切空间中的[零向量](@entry_id:156189) $0_p \in T_pM$。在任意[局部坐标系](@entry_id:751394)中，我们有 $Z(p) = \sum_{i=1}^n Z^i(p) \frac{\partial}{\partial x^i}|_p = 0_p$。由于[基向量](@entry_id:199546) $\{\frac{\partial}{\partial x^i}|_p\}$ 是[线性无关](@entry_id:148207)的，这唯一确定了所有分量函数 $Z^i(p)$ 必须恒等于0。因为零函数是光滑的，所以零向量场在任何[坐标系](@entry_id:156346)下的分量都是光滑的，这证明了 $Z$ 是一个全局定义在任何光滑流形上的光滑向量场 [@problem_id:1688350]。

### 向量场的双重身份：[截面](@entry_id:154995)与导子

向量场除了作为切丛的几何[截面](@entry_id:154995)外，还具有一个等价的代数身份：作用在[光滑函数](@entry_id:267124)代数上的**导子 (derivation)**。回顾一下，单个[切向量](@entry_id:265494) $v \in T_pM$ 可以被视为一个作用在 $p$ 点光滑函数芽上的导子，它计算函数在 $v$ 方向上的[方向导数](@entry_id:189133)。

这个思想可以全局化。一个光滑向量场 $X$ 可以定义一个从[光滑函数](@entry_id:267124)代数 $C^\infty(M)$ 到其自身的线性映射，通常也记作 $X$。对于任意光滑函数 $f \in C^\infty(M)$，它产生一个新的光滑函数 $X[f]$，其在任意点 $p \in M$ 的值定义为：
$$
(X[f])(p) := X_p(f)
$$
其中 $X_p$ 是向量场在 $p$ 点的向量值，它作为一个导子作用在函数 $f$ 上。

这两种观点之间的联系在[局部坐标](@entry_id:181200)中尤为清晰。如果向量场 $X$ 的局部表示为 $X = \sum_{i=1}^n X^i \frac{\partial}{\partial x^i}$，那么它作为导子作用在函数 $f$ 上的结果就是：
$$
X[f] = \left(\sum_{i=1}^n X^i \frac{\partial}{\partial x^i}\right)[f] = \sum_{i=1}^n X^i \frac{\partial f}{\partial x^i}
$$
这正是函数 $f$ 沿着向量场 $X$ 方向的[李导数](@entry_id:171745)。例如，考虑 $\mathbb{R}^3$ 上的向量场 $X = z^2 \frac{\partial}{\partial x} - 2xy \frac{\partial}{\partial y} + x \frac{\partial}{\partial z}$ 和函数 $f(x, y, z) = xy^2 + z^3$。我们可以通过计算[偏导数](@entry_id:146280) $\frac{\partial f}{\partial x} = y^2$, $\frac{\partial f}{\partial y} = 2xy$, $\frac{\partial f}{\partial z} = 3z^2$ 来确定 $X[f]$。代入上式，得到新的函数：
$$
X[f] = (z^2)(y^2) + (-2xy)(2xy) + (x)(3z^2) = y^2z^2 - 4x^2y^2 + 3xz^2
$$
这个计算过程完美地展示了如何从向量场的[截面](@entry_id:154995)表示（由其分量 $X^i$ 给出）过渡到其作为[微分算子](@entry_id:140145)（导子）的具体作用 [@problem_id:1688368]。向量场的这两种等价观点在[微分几何](@entry_id:145818)中都至关重要，前者提供了几何直观，后者则为计算和代数操作提供了强有力的工具。

### [坐标变换](@entry_id:172727)与[几何不变性](@entry_id:637068)

向量场是一个内蕴的几何对象，它的定义不依赖于任何特定的[坐标系](@entry_id:156346)。然而，它的分量表示却依赖于[坐标系](@entry_id:156346)的选择。理解分量在不同[坐标系](@entry_id:156346)下如何变换，是掌握[张量分析](@entry_id:161423)和确保[几何不变量](@entry_id:178611)性的关键。

假设在两个重叠的[坐标卡](@entry_id:262338) $(U, (x^1, \dots, x^n))$ 和 $(V, (y^1, \dots, y^n))$ 中，同一个向量场 $X$ 有两种不同的表示：
$$
X = \sum_{i=1}^{n} X^{i} \frac{\partial}{\partial x^{i}} = \sum_{j=1}^{n} \tilde{X}^{j} \frac{\partial}{\partial y^{j}}
$$
我们的目标是找到分量 $X^i$ 和 $\tilde{X}^j$ 之间的关系。关键在于[基向量](@entry_id:199546)之间的变换关系。根据多元微积分的链式法则，对于任意光滑函数 $f$，我们有：
$$
\frac{\partial f}{\partial x^i} = \sum_{j=1}^n \frac{\partial y^j}{\partial x^i} \frac{\partial f}{\partial y^j}
$$
将[基向量](@entry_id:199546)视为作用于函数的导子算子，上述关系式意味着算子本身满足：
$$
\frac{\partial}{\partial x^i} = \sum_{j=1}^n \frac{\partial y^j}{\partial x^i} \frac{\partial}{\partial y^j}
$$
其中 $\frac{\partial y^j}{\partial x^i}$ 是[坐标变换](@entry_id:172727) $y(x)$ 的雅可比矩阵的元素。现在，我们将此变换关系代入 $X$ 在 $x$-[坐标系](@entry_id:156346)下的表达式：
$$
X = \sum_{i=1}^n X^i \left( \sum_{j=1}^n \frac{\partial y^j}{\partial x^i} \frac{\partial}{\partial y^j} \right) = \sum_{j=1}^n \left( \sum_{i=1}^n X^i \frac{\partial y^j}{\partial x^i} \right) \frac{\partial}{\partial y^j}
$$
将这个结果与 $X$ 在 $y$-[坐标系](@entry_id:156346)下的表达式 $\sum_j \tilde{X}^j \frac{\partial}{\partial y^j}$ 进行比较，由于[基向量](@entry_id:199546) $\{\frac{\partial}{\partial y^j}\}$ 是线性无关的，两边的系数必须相等。因此，我们得到了向量场分量的**变换法则 (transformation law)**：
$$
\tilde{X}^{j} = \sum_{i=1}^{n} X^{i} \frac{\partial y^{j}}{\partial x^{i}}
$$
这个法则被称为**[逆变](@entry_id:192290) (contravariant)** 变换，因为它使用了从 $x$ 到 $y$ 坐标变换的雅可比矩阵，而不是其逆矩阵。这个变换法则精确地抵消了[基向量](@entry_id:199546)的变换，从而保证了向量场 $X$ 作为一个几何整体的不变性 [@problem_id:3006112]。

### 全局性质：[截面](@entry_id:154995)的存在性与[流形](@entry_id:153038)拓扑

到目前为止，我们的讨论主要集中在向量场的局部性质。现在，我们转向一个更深刻的全局性问题：一个给定的光滑流形 $M$ 是否允许存在一个**处处非零 (nowhere-vanishing)** 的光滑向量场？这个问题的答案惊人地与[流形的拓扑](@entry_id:267834)性质紧密相关。

我们已经知道，任何[流形](@entry_id:153038)上都存在一个全局光滑向量场——零向量场。但寻找一个处处非零的向量场则要困难得多。让我们通过两个经典的例子来感受其中的差异。

考虑一个嵌入在 $\mathbb{R}^3$ 中的**环面 (torus)** $T^2$，其[参数化](@entry_id:272587)为 $\mathbf{r}(\alpha, \beta) = ((R+r\cos\alpha)\cos\beta, (R+r\cos\alpha)\sin\beta, r\sin\alpha)$。我们可以定义一个沿着 $\beta$ 方向的向量场 $V_T = \frac{\partial \mathbf{r}}{\partial \beta}$。计算其大小的平方：
$$
|V_T|^2 = |(-(R+r\cos\alpha)\sin\beta, (R+r\cos\alpha)\cos\beta, 0)|^2 = (R+r\cos\alpha)^2
$$
由于我们假设 $R  r  0$，所以 $R+r\cos\alpha \ge R-r  0$。这意味着 $|V_T|$ 永远不会为零。因此，我们在环面上成功地构造了一个处处非零的光滑向量场。

现在，让我们转向**球面 (sphere)** $S^2$。一个看似自然的选择是，将 $\mathbb{R}^3$ 中一个恒定的背景向量场（例如 $\mathbf{F} = (0,0,1)$）投影到球面上每一点的[切空间](@entry_id:199137)。在球面上任意一点 $p$，其[法向量](@entry_id:264185)为 $p$ 本身。投影向量场 $V_S$ 由公式 $V_S(p) = \mathbf{F} - (\mathbf{F} \cdot p)p$ 给出。要使 $V_S(p) = 0$，必须有 $\mathbf{F} = (\mathbf{F} \cdot p)p$，这意味着 $p$ 必须与 $\mathbf{F}$ 平行。在[单位球](@entry_id:142558)面上，满足这个条件的只有两个点：北极点 $(0,0,1)$ 和南极点 $(0,0,-1)$。因此，这个看似自然的向量场在两个点上必然为零 [@problem_id:1688364]。

这个例子引出了著名的**[毛球定理](@entry_id:151079) (Hairy Ball Theorem)**，它断言：任何在偶数维球面（如 $S^2$）上的光滑向量场，都必然至少有一个零点。直观地说，你无法“抚平”一个毛球上的所有毛发而不留下至少一个“旋”或“尖顶”。

这个拓扑障碍可以用向量丛的语言来精确描述。一个向量丛上存在处处非零的[截面](@entry_id:154995)，意味着这个丛在某种意义上是“可分解的”。具体而言，如果一个秩为 $k$ 的向量丛 $E$ 有一个处处非零的[截面](@entry_id:154995)，那么它可以分解为平凡线丛 $\underline{\mathbb{R}}$ 与一个秩为 $k-1$ 的丛 $F$ 的**惠特尼和 (Whitney sum)**：$E \cong \underline{\mathbb{R}} \oplus F$。对于球面 $S^2$，其上的任何实线丛都是平凡的（因为其第一[上同调群](@entry_id:142450) $H^1(S^2; \mathbb{Z}_2) = 0$）。因此，如果 $TS^2$ 存在一个处处非零的[截面](@entry_id:154995)，它将分解为 $TS^2 \cong \underline{\mathbb{R}} \oplus \underline{\mathbb{R}}$，这意味着 $TS^2$ 必须是**平凡丛 (trivial bundle)** [@problem_id:3006108]。

判断一个向量丛是否平凡，可以通过其**特征类 (characteristic classes)** 来进行。对于一个定向的秩为2的实向量丛 $E \to M$（$M$ 是一个二维闭[流形](@entry_id:153038)），其存在处处非零[截面](@entry_id:154995)的根本障碍是**[欧拉类](@entry_id:161259) (Euler class)** $e(E) \in H^2(M; \mathbb{Z})$。该丛存在处处非零[截面](@entry_id:154995)的充要条件是其[欧拉类](@entry_id:161259)为零，$e(E)=0$。

通过深刻的**[高斯-博内-陈定理](@entry_id:262776) (Gauss-Bonnet-Chern Theorem)**，[流形](@entry_id:153038)切丛的[欧拉类](@entry_id:161259)与其内蕴的几何——曲率——联系起来。该定理指出，[欧拉类](@entry_id:161259)在基本同调类 $[M]$ 上的配对值等于[流形](@entry_id:153038)的**欧拉示性数 (Euler characteristic)** $\chi(M)$：
$$
\langle e(TM), [M] \rangle = \frac{1}{2\pi} \int_M K \, dA = \chi(M)
$$
其中 $K$ 是高斯曲率，$dA$ 是面积元。对于球面 $S^2$，我们知道 $\chi(S^2) = 2$。因此，$\langle e(TS^2), [S^2] \rangle = 2 \neq 0$。这[直接证明](@entry_id:141172)了[欧拉类](@entry_id:161259) $e(TS^2)$ 非零。既然[欧拉类](@entry_id:161259)这个拓扑不变量非零，就意味着 $TS^2$ 不可能存在处处非零的[截面](@entry_id:154995)。因此，$TS^2$ 是一个非平凡的向量丛，这为[毛球定理](@entry_id:151079)提供了坚实的[拓扑基](@entry_id:261506)础 [@problem_id:3006108]。

综上所述，从将向量场视为[切丛截面](@entry_id:261939)这一几何观点出发，我们不仅统一了其局部和代数的描述，更重要的是，它为我们揭示了[流形](@entry_id:153038)的[微分](@entry_id:158718)结构和其深刻的全局[拓扑性质](@entry_id:141605)之间的壮丽桥梁。