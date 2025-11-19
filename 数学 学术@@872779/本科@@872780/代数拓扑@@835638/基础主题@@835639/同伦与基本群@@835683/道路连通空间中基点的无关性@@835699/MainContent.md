## 引言
基本群 $\pi_1(X, x_0)$ 是代数拓扑中用以探测空间“洞”的强大代数[不变量](@entry_id:148850)，但其定义本身却似乎存在一个内在的局限：它依赖于基点 $x_0$ 的选择。这引出了一个至关重要的问题：如果我们更换空间中的基点，基本群的[代数结构](@entry_id:137052)会随之改变吗？还是说，在某些条件下，这种选择并不会影响其核心特性？本文旨在系统性地回答这一问题，为读者揭示代数拓扑中的一个基石性定理——[路径连通空间](@entry_id:152443)的基本群在同构意义下是[独立于基点](@entry_id:273050)选择的。

为了全面掌握这一概念，我们将分三个章节展开探讨。在“原理与机制”一章中，我们将详细构造连接不同基点基本群的同构映射，并严格证明其性质，揭示[路径连通性](@entry_id:142695)在其中扮演的关键角色。随后，在“应用与交叉学科联系”一章中，我们将展示该定理如何为“单连通”等重要概念提供坚实基础，并探讨它与同调论、[覆叠空间理论](@entry_id:273250)等其他拓扑学核心工具的深刻联系。最后，通过“动手实践”部分的具体习题，读者将有机会将理论知识应用于解决实际问题，从而巩固和深化理解。

## 原理与机制

我们在之前的章节中定义了[拓扑空间](@entry_id:155056) $X$ 在指定基点 $x_0$ 上的[基本群](@entry_id:146111) $\pi_1(X, x_0)$。这个定义明确地依赖于基点 $x_0$ 的选择。一个自然而深刻的问题随之而来：如果更换基点，基本群会发生怎样的变化？它在[代数结构](@entry_id:137052)上是会发生根本性的改变，还是在某种意义上保持不变？本章将系统地探讨这一问题，并揭示在道路[连通空间](@entry_id:156017)中，[基本群](@entry_id:146111)在同构意义下是[独立于基点](@entry_id:273050)选择的。

### [基点变换](@entry_id:154068)映射：构造

要比较不同基点的基本群，我们首先需要建立它们之间的联系。直观上，如果一个空间是**道路连通的 (path-connected)**，意味着空间中任意两点之间都存在一条连续的路径。这为我们“移动”基点提供了可能。

假设我们有两个基点 $x_0$ 和 $x_1$，并且存在一条从 $x_0$ 到 $x_1$ 的路径 $\gamma$。对于任何一个以 $x_1$ 为基点的闭路（loop） $f$，我们如何利用路径 $\gamma$ 将其变换为一个以 $x_0$ 为基点的闭路呢？一个非常自然的想法是：
1.  从新的基点 $x_0$ 出发，沿着路径 $\gamma$ 行进至旧的基点 $x_1$。
2.  在 $x_1$ 处，完整地走一遍闭路 $f$。
3.  最后，沿着 $\gamma$ 的**逆路径 (inverse path)** $\gamma^{-1}$ 从 $x_1$ 返回到 $x_0$。

这三个步骤的连续执行，即路径的**[串联](@entry_id:141009) (concatenation)**，构成了一个新的、以 $x_0$ 为基点的闭路。我们将这个新闭路记为 $g = \gamma \cdot f \cdot \gamma^{-1}$。

为了精确描述这个过程，我们给出路径[串联](@entry_id:141009)的数学定义。回忆一下，一条路径是一个从单位区间 $I = [0, 1]$ 到空间 $X$ 的[连续映射](@entry_id:153855)。逆路径 $\gamma^{-1}$ 定义为 $\gamma^{-1}(t) = \gamma(1-t)$。三条路径 $p_1, p_2, p_3$ 的[串联](@entry_id:141009)（在端点匹配的情况下）可以定义为将时间区间 $[0,1]$ 分成三段，每段分别执行一条路径：
$$ (p_1 \cdot p_2 \cdot p_3)(t) = \begin{cases} p_1(3t)  \text{若 } 0 \le t \le 1/3 \\ p_2(3t-1)  \text{若 } 1/3 \le t \le 2/3 \\ p_3(3t-2)  \text{若 } 2/3 \le t \le 1 \end{cases} $$
根据这个定义，我们为上述构造的闭路 $g = \gamma \cdot f \cdot \gamma^{-1}$ 写出其显式表达式 [@problem_id:1657810] [@problem_id:1657836]：
$$ g(t) = \begin{cases} \gamma(3t)  \text{若 } 0 \le t \le 1/3 \\ f(3t-1)  \text{若 } 1/3 \le t \le 2/3 \\ \gamma^{-1}(3t-2)  \text{若 } 2/3 \le t \le 1 \end{cases} $$
对于第三段，利用逆路径的定义 $\gamma^{-1}(s) = \gamma(1-s)$，我们代入 $s = 3t-2$，得到 $\gamma^{-1}(3t-2) = \gamma(1 - (3t-2)) = \gamma(3-3t)$。因此，新闭路的完整表达式为：
$$ g(t) = (\gamma \cdot f \cdot \gamma^{-1})(t) = \begin{cases} \gamma(3t)  \text{若 } 0 \le t \le \frac{1}{3} \\ f(3t-1)  \text{若 } \frac{1}{3} \le t \le \frac{2}{3} \\ \gamma(3-3t)  \text{若 } \frac{2}{3} \le t \le 1 \end{cases} $$
这个构造是建立不同基点基本群之间关系的核心。由于基本群的元素是闭路的[同伦类](@entry_id:149365)，我们需要验证这个构造在[同伦类](@entry_id:149365)层面是良定义的。可以证明，如果 $f_1$ 和 $f_2$ 是两个在 $x_1$ 处同伦的闭路，那么构造出的新闭路 $\gamma \cdot f_1 \cdot \gamma^{-1}$ 和 $\gamma \cdot f_2 \cdot \gamma^{-1}$ 在 $x_0$ 处也是同伦的。这使得我们可以定义一个从 $\pi_1(X, x_1)$ 到 $\pi_1(X, x_0)$ 的映射。

我们定义**[基点变换](@entry_id:154068)映射 (change-of-basepoint map)** $\beta_\gamma: \pi_1(X, x_1) \to \pi_1(X, x_0)$ 为：
$$ \beta_\gamma([f]) = [\gamma \cdot f \cdot \gamma^{-1}] $$
其中 $[f]$ 是 $\pi_1(X, x_1)$ 中的一个元素，$\gamma$ 是一条从 $x_0$ 到 $x_1$ 的路径。这个映射通过路径 $\gamma$ 将 $x_1$ 处的闭路[同伦类](@entry_id:149365)“[拉回](@entry_id:160816)”到 $x_0$ 处的闭路[同伦类](@entry_id:149365)。

### 证明同构关系

现在我们来证明，上文定义的映射 $\beta_\gamma$ 不仅仅是一个普通的映射，而是一个**[群同构](@entry_id:147371) (group isomorphism)**。为此，我们需要证明它既是[群同态](@entry_id:140603)，又是双射。

#### 同态性质

我们需要验证 $\beta_\gamma$ 保持群的乘法结构，即对于 $\pi_1(X, x_1)$ 中的任意两个元素 $[f]$ 和 $[g]$，应有 $\beta_\gamma([f] \cdot [g]) = \beta_\gamma([f]) \cdot \beta_\gamma([g])$。

让我们展开这个等式。左边是：
$$ \beta_\gamma([f] \cdot [g]) = \beta_\gamma([f \cdot g]) = [\gamma \cdot (f \cdot g) \cdot \gamma^{-1}] $$
右边是：
$$ \beta_\gamma([f]) \cdot \beta_\gamma([g]) = [\gamma \cdot f \cdot \gamma^{-1}] \cdot [\gamma \cdot g \cdot \gamma^{-1}] = [\gamma \cdot f \cdot \gamma^{-1} \cdot \gamma \cdot g \cdot \gamma^{-1}] $$
要证明左右两边相等，我们需要说明闭路 $\gamma \cdot (f \cdot g) \cdot \gamma^{-1}$ 和 $\gamma \cdot f \cdot \gamma^{-1} \cdot \gamma \cdot g \cdot \gamma^{-1}$ 是同伦的。观察右边的表达式，中间含有一部分 $\gamma^{-1} \cdot \gamma$。这是一个从 $x_1$ 出发沿 $\gamma^{-1}$ 到 $x_0$ 再沿 $\gamma$ 回到 $x_1$ 的闭路。这个闭路与 $x_1$ 处的常闭路 $e_{x_1}$ 是同伦的。在基本群中，与单位元（常闭路[同伦类](@entry_id:149365)）的乘积不改变元素。因此：
$$ [\gamma \cdot f \cdot \gamma^{-1} \cdot \gamma \cdot g \cdot \gamma^{-1}] = [\gamma \cdot f \cdot e_{x_1} \cdot g \cdot \gamma^{-1}] = [\gamma \cdot f \cdot g \cdot \gamma^{-1}] $$
这恰好等于等式的左边。所以，$\beta_\gamma$ 是一个[群同态](@entry_id:140603) [@problem_id:1657821]。

这个证明也揭示了 $\beta_\gamma$ 如何处理单位元。$\pi_1(X, x_1)$ 的单位元是常闭路 $[e_{x_1}]$。它的像是：
$$ \beta_\gamma([e_{x_1}]) = [\gamma \cdot e_{x_1} \cdot \gamma^{-1}] = [\gamma \cdot \gamma^{-1}] $$
而闭路 $\gamma \cdot \gamma^{-1}$ 与 $x_0$ 处的常闭路 $e_{x_0}$ 是同伦的，所以 $\beta_\gamma([e_{x_1}]) = [e_{x_0}]$。这表明 $\beta_\gamma$ 将一个群的单位元映射到另一个群的单位元，这是[群同态](@entry_id:140603)的一个必要条件 [@problem_id:1657832]。

#### 双射性质

为了证明 $\beta_\gamma$ 是[双射](@entry_id:138092)，最直接的方法是构造它的逆映射。路径 $\gamma$ 是从 $x_0$ 到 $x_1$ 的，它的逆路径 $\gamma^{-1}$ 是从 $x_1$ 到 $x_0$ 的。因此，路径 $\gamma^{-1}$ 同样可以诱导一个[基点变换](@entry_id:154068)映射，这次是从 $\pi_1(X, x_0)$ 到 $\pi_1(X, x_1)$：
$$ \beta_{\gamma^{-1}}: \pi_1(X, x_0) \to \pi_1(X, x_1), \quad \beta_{\gamma^{-1}}([g]) = [\gamma^{-1} \cdot g \cdot (\gamma^{-1})^{-1}] = [\gamma^{-1} \cdot g \cdot \gamma] $$
我们来验证 $\beta_{\gamma^{-1}}$ 是否为 $\beta_\gamma$ 的逆。考虑它们的复合：
$$ (\beta_{\gamma^{-1}} \circ \beta_\gamma)([f]) = \beta_{\gamma^{-1}}([\gamma \cdot f \cdot \gamma^{-1}]) = [\gamma^{-1} \cdot (\gamma \cdot f \cdot \gamma^{-1}) \cdot \gamma] $$
利用路径[串联](@entry_id:141009)的[结合律](@entry_id:151180)（在[同伦](@entry_id:139266)意义下），上式等于：
$$ [(\gamma^{-1} \cdot \gamma) \cdot f \cdot (\gamma^{-1} \cdot \gamma)] = [e_{x_1} \cdot f \cdot e_{x_1}] = [f] $$
因此，$\beta_{\gamma^{-1}} \circ \beta_\gamma$ 是 $\pi_1(X, x_1)$ 上的[恒等映射](@entry_id:634191)。同理可证 $\beta_\gamma \circ \beta_{\gamma^{-1}}$ 是 $\pi_1(X, x_0)$ 上的恒等映射。这证明了 $\beta_\gamma$ 是一个[双射](@entry_id:138092)，其逆映射就是 $\beta_{\gamma^{-1}}$。

综合以上两点，我们得出以下重要定理：

**定理：** 若 $X$ 是一个道路连通的[拓扑空间](@entry_id:155056)，则对于 $X$ 中的任意两个点 $x_0$ 和 $x_1$，它们的[基本群](@entry_id:146111)是同构的，即 $\pi_1(X, x_0) \cong \pi_1(X, x_1)$。

这个定理意味着，对于道路[连通空间](@entry_id:156017)，[基本群](@entry_id:146111)的[代数结构](@entry_id:137052)不依赖于基点的选择。因此，我们常常可以省略基点，直接谈论“空间 $X$ 的基本群”，并用 $\pi_1(X)$ 来表示。

### [道路连通性](@entry_id:154325)的关键作用

上述整个构造和证明都依赖于连接基点 $x_0$ 和 $x_1$ 的路径 $\gamma$ 的存在。如果空间不是道路连通的，情况会如何？

让我们考虑一个由两个不相交的圆 $C_1$ 和 $C_2$ 组成的[拓扑空间](@entry_id:155056) $X = C_1 \sqcup C_2$。这是一个非道路[连通空间](@entry_id:156017)，它有两个[道路连通分支](@entry_id:155468)。设 $p_1 \in C_1$ 和 $p_2 \in C_2$。由于 $p_1$ 和 $p_2$ 位于不同的连通分支中，它们之间不存在任何路径。因此，我们无法构造出连接 $\pi_1(X, p_1)$ 和 $\pi_1(X, p_2)$ 的[基点变换](@entry_id:154068)映射 $\beta_\gamma$ [@problem_id:1657831]。

在这种情况下，[基本群](@entry_id:146111)确实依赖于基点。以 $p_1$ 为基点的所有闭路都必须完全位于 $C_1$ 内部，因此 $\pi_1(X, p_1) \cong \pi_1(C_1, p_1) \cong \mathbb{Z}$。同理，$\pi_1(X, p_2) \cong \pi_1(C_2, p_2) \cong \mathbb{Z}$。

这里需要注意一个微妙之处：虽然我们无法在它们之间构造一个典范的（由路径诱导的）同构，但作为抽象群，$\pi_1(X, p_1)$ 和 $\pi_1(X, p_2)$ 恰好是同构的（它们都同构于整数[加法群](@entry_id:151801) $\mathbb{Z}$）。然而，如果我们考虑另一个例子，比如 $X = S^1 \sqcup \{*\}$（一个圆和一个点的无交并），并取 $x_0 \in S^1$ 和 $x_1 = *$，那么 $\pi_1(X, x_0) \cong \mathbb{Z}$，而 $\pi_1(X, x_1)$ 是只包含单位元的平凡群。这两个群显然不同构。

这引导我们对基点无关性定理做出更精确的陈述 [@problem_id:1657835]：
**对于任意拓扑空间 $X$，若两点 $x_0$ 和 $x_1$ 位于同一个[道路连通分支](@entry_id:155468)中，则 $\pi_1(X, x_0) \cong \pi_1(X, x_1)$。**

基本群的[同构类](@entry_id:147854)在每个[道路连通分支](@entry_id:155468)上是恒定的。因此，一个空间的[基本群](@entry_id:146111)集合 $\{\pi_1(X, x) \mid x \in X\}$ 在同构关系下被空间的[道路连通分支](@entry_id:155468)所划分。

### 同构对路径的依赖性

我们已经证明，在道路[连通空间](@entry_id:156017)中，任意两个基点的基本群都是同构的。这个同构是通过选取一条连接基点的路径 $\gamma$ 来具体实现的。下一个自然的问题是：如果我们在相同的两个基点 $x_0$ 和 $x_1$ 之间选择另一条不同的路径 $\delta$，那么由 $\delta$ 诱导的同构 $\beta_\delta$ 是否与 $\beta_\gamma$ 相同？

答案是：不一定。同构本身依赖于所选路径的[同伦类](@entry_id:149365)。

让我们来分析两个同构 $\beta_\gamma, \beta_\delta: \pi_1(X, x_1) \to \pi_1(X, x_0)$ 之间的关系。为此，我们考察复合映射 $\beta_\delta \circ \beta_\gamma^{-1}$，这是一个从 $\pi_1(X, x_0)$ 到自身的自同构。
对于任意 $[g] \in \pi_1(X, x_0)$：
$$ (\beta_\delta \circ \beta_\gamma^{-1})([g]) = \beta_\delta(\beta_{\gamma^{-1}}([g])) = \beta_\delta([\gamma^{-1} \cdot g \cdot \gamma]) = [\delta \cdot (\gamma^{-1} \cdot g \cdot \gamma) \cdot \delta^{-1}] $$
利用路径[串联](@entry_id:141009)的[结合律](@entry_id:151180)，上式可重写为：
$$ [(\delta \cdot \gamma^{-1}) \cdot g \cdot (\gamma \cdot \delta^{-1})] $$
我们注意到，$k = \delta \cdot \gamma^{-1}$ 是一条从 $x_0$ 出发，沿 $\delta$ 到 $x_1$，再沿 $\gamma^{-1}$ 回到 $x_0$ 的闭路。因此，$k$ 代表了 $\pi_1(X, x_0)$ 中的一个元素 $[k]$。而 $\gamma \cdot \delta^{-1}$ 正是 $k$ 的逆路径，它代表了 $[k]^{-1}$。因此，上述表达式可以写成群内的运算形式：
$$ (\beta_\delta \circ \beta_\gamma^{-1})([g]) = [k] \cdot [g] \cdot [k]^{-1} $$
这是一个由元素 $[k]$ 决定的**[内自同构](@entry_id:142697) (inner automorphism)** [@problem_id:1657827]。

这个结果非常重要，它揭示了：
1.  由不同路径 $\gamma$ 和 $\delta$ 诱导的[基点变换](@entry_id:154068)同构 $\beta_\gamma$ 和 $\beta_\delta$ 之间的关系，是通过 $\pi_1(X, x_0)$ 的一个[内自同构](@entry_id:142697)来描述的。具体来说，$\beta_\delta = c_{[k]} \circ \beta_\gamma$，其中 $c_{[k]}$ 是指由元素 $[k] = [\delta \cdot \gamma^{-1}]$ 进行的共轭变换。

2.  同构 $\beta_\gamma$ 和 $\beta_\delta$ 何时相等？当且仅当这个[内自同构](@entry_id:142697)是恒等映射时，即对于所有 $[g] \in \pi_1(X, x_0)$，都有 $[k][g][k]^{-1} = [g]$。这等价于要求元素 $[k]$ 必须与群中的所有元素都交换，也就是说，$[k]$ 必须属于 $\pi_1(X, x_0)$ 的**中心 (center)** $Z(\pi_1(X, x_0))$ [@problem_id:1657815]。

3.  一个重要的特例是，如果路径 $\gamma$ 和 $\delta$ 本身是（保持端点）同伦的 ($\gamma \simeq \delta$)。在这种情况下，闭路 $k = \delta \cdot \gamma^{-1}$ 将与常闭路 $e_{x_0}$同伦，因此 $[k]$ 就是群中的单位元。单位元总是在[群的中心](@entry_id:141952)，并且由它引导的共轭变换是恒等映射。所以，**如果两条路径是[同伦](@entry_id:139266)的，那么它们诱导的[基点变换](@entry_id:154068)同构是完全相同的** [@problem_id:1657814]。这意味着，同构映射实际上只依赖于连接两基点的路径的**[同伦类](@entry_id:149365)**。

4.  另一个重要的推论是，如果基本群 $\pi_1(X, x_0)$ 是一个**阿贝尔群 (Abelian group)**（即[交换群](@entry_id:145145)），那么它的中心就是整个群。这意味着任何元素 $[k]$ 都位于中心内。因此，对于任何两条路径 $\gamma$ 和 $\delta$，它们诱导的同构都是相同的。在这种情况下，基点之间的同构是典范的，不依赖于路径的选择。

### [函子性](@entry_id:150069)

[基点变换](@entry_id:154068)的构造还有一个优美的代数性质，即它与路径的[串联](@entry_id:141009)运算相容，这体现了一种**[函子性](@entry_id:150069) (functoriality)**。

假设我们有三个点 $x_0, x_1, x_2$ 以及两条路径 $\gamma_1: x_0 \to x_1$ 和 $\gamma_2: x_1 \to x_2$。我们可以得到三个同构映射：
- $\beta_{\gamma_1}: \pi_1(X, x_1) \to \pi_1(X, x_0)$
- $\beta_{\gamma_2}: \pi_1(X, x_2) \to \pi_1(X, x_1)$
- $\beta_{\gamma_1 \cdot \gamma_2}: \pi_1(X, x_2) \to \pi_1(X, x_0)$

它们之间的关系是什么？让我们计算复合映射 $\beta_{\gamma_1} \circ \beta_{\gamma_2}$。对于任意 $[f] \in \pi_1(X, x_2)$：
$$ (\beta_{\gamma_1} \circ \beta_{\gamma_2})([f]) = \beta_{\gamma_1}(\beta_{\gamma_2}([f])) = \beta_{\gamma_1}([\gamma_2 \cdot f \cdot \gamma_2^{-1}]) = [\gamma_1 \cdot (\gamma_2 \cdot f \cdot \gamma_2^{-1}) \cdot \gamma_1^{-1}] $$
利用结合律，上式为：
$$ [(\gamma_1 \cdot \gamma_2) \cdot f \cdot (\gamma_2^{-1} \cdot \gamma_1^{-1})] $$
我们知道，复合路径的逆等于逆路径的反向复合，即 $(\gamma_1 \cdot \gamma_2)^{-1} = \gamma_2^{-1} \cdot \gamma_1^{-1}$。因此，上式恰好是：
$$ [(\gamma_1 \cdot \gamma_2) \cdot f \cdot (\gamma_1 \cdot \gamma_2)^{-1}] = \beta_{\gamma_1 \cdot \gamma_2}([f]) $$
这表明，$\beta_{\gamma_1 \cdot \gamma_2} = \beta_{\gamma_1} \circ \beta_{\gamma_2}$ [@problem_id:1657802]。这个性质说明，沿复合路径的[基点变换](@entry_id:154068)，等于沿各分段路径的[基点变换](@entry_id:154068)的依次复合。这进一步强化了路径、闭路和[基本群](@entry_id:146111)之间深刻的[代数结构](@entry_id:137052)联系。