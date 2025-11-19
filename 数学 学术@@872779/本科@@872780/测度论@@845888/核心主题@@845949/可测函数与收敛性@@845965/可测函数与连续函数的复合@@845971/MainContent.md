## 引言
在[测度论](@entry_id:139744)的学习中，当我们熟悉了[可测函数](@entry_id:159040)的基本定义后，一个自然而然的问题浮出水面：由已知的可测函数通过[函数复合](@entry_id:144881)这一基本运算构造出的新函数，其[可测性](@entry_id:199191)是否得以保持？这一问题不仅是理论上的好奇，更关乎整个[测度论](@entry_id:139744)大厦的稳固性，因为它直接影响着我们能否自由地对可测函数进行变换和代数运算。本文旨在系统性地解答这一核心问题，填补从单个可测函数到其复杂组合之间的知识鸿沟。

本文将分为三个主要部分，带领读者层层深入。在“原理与机制”一章，我们将剖析[函数复合](@entry_id:144881)[可测性](@entry_id:199191)的基本结构，阐明经典定理（如[连续函数](@entry_id:137361)与可测函数复合的可测性），并通过关键示例和深刻反例，揭示其中的精妙之处与潜在陷阱，特别是[勒贝格可测](@entry_id:192844)与波莱尔可测之间的关键区别。随后，在“应用与跨学科联系”一章，我们将展示这一理论原理如何作为基石，在概率论、[随机过程](@entry_id:159502)、[泛函分析](@entry_id:146220)和[微分方程](@entry_id:264184)等领域发挥着不可或缺的作用。最后，“动手实践”部分将提供一系列精选问题，帮助读者巩固理论知识并将其应用于具体情境。通过这一结构化的学习路径，读者将全面掌握[函数复合](@entry_id:144881)的[可测性](@entry_id:199191)理论，并深刻理解其在现代数学中的重要地位。

## 原理与机制

在上一章介绍[可测函数](@entry_id:159040)的基本概念之后，我们自然会问：通过基本运算（如算术运算或[函数复合](@entry_id:144881)）组合可测函数，得到的新函数是否仍然是可测的？本章将深入探讨[函数复合](@entry_id:144881)的可测性问题。我们将系统地阐述其核心原理，明确其成立的条件，并通过关键示例和深刻的反例来揭示其中的精妙之处与潜在的陷阱。

### 基础：[函数复合](@entry_id:144881)与[可测性](@entry_id:199191)

假设我们有两个函数 $f: (X, \mathcal{M}) \to (Y, \mathcal{N})$ 和 $g: (Y, \mathcal{N}) \to (Z, \mathcal{P})$，其中 $(X, \mathcal{M})$、$(Y, \mathcal{N})$ 和 $(Z, \mathcal{P})$ 是[可测空间](@entry_id:189701)。它们的[复合函数](@entry_id:147347) $h = g \circ f$ 定义为 $h(x) = g(f(x))$，它是一个从 $X$ 到 $Z$ 的映射。

要判断 $h$ 是否是 $\mathcal{M}/\mathcal{P}$-可测的，我们必须根据定义来验证：对于任意一个目标 $\sigma$-代数 $\mathcal{P}$ 中的集合 $S$，其原像 $h^{-1}(S)$ 是否属于定义域的 $\sigma$-代数 $\mathcal{M}$。复合函数的[原像](@entry_id:150899)运算具有一个关键的结构性特质：
$$
h^{-1}(S) = (g \circ f)^{-1}(S) = f^{-1}(g^{-1}(S))
$$
这个等式是理解复合函数[可测性](@entry_id:199191)的核心。它表明，将一个集合 $S$ 通过 $h$ “[拉回](@entry_id:160816)”到 $X$ 的过程，等价于一个两步操作：首先，将 $S$ 通过外函数 $g$ [拉回](@entry_id:160816)到中间空间 $Y$，得到集合 $g^{-1}(S)$；然后，再将这个新集合通过内函数 $f$ [拉回](@entry_id:160816)到初始空间 $X$，得到 $f^{-1}(g^{-1}(S))$。

因此，$g \circ f$ 的可测性取决于这一系列“[拉回](@entry_id:160816)”操作是否能保持[可测性](@entry_id:199191)。具体来说，我们关心的是：
1. 对于我们关心的目标集 $S \in \mathcal{P}$，$g^{-1}(S)$ 是否是 $\mathcal{N}$ 中的一个“好”集合（即，一个可测集）？
2. 如果是，那么 $f$ 能否保证将这个“好”集合 $g^{-1}(S)$ [拉回](@entry_id:160816)到 $\mathcal{M}$ 中的一个[可测集](@entry_id:159173)？

当 $X, Y, Z$ 都是实数集 $\mathbb{R}$，且 $\sigma$-代数是标准的 Borel $\sigma$-代数 $\mathcal{B}(\mathbb{R})$ 或 Lebesgue $\sigma$-代数 $\mathcal{L}$ 时，上述问题变得尤为具体和重要。

### 经典结果：涉及[连续函数的复合](@entry_id:139194)

在分析学中，[连续函数](@entry_id:137361)是最基本也是性质最良好的一类函数。它们与[可测性](@entry_id:199191)的相互作用构成了本主题的基石。一个核心事实是：**任何定义在 $\mathbb{R}$ 上的[连续函数](@entry_id:137361)都是 Borel 可测的**。这是因为根据拓扑定义，[连续函数](@entry_id:137361)将开集（Borel $\sigma$-代数的生成元）的原像映射为开集，而开集本身就是 Borel 集。通过一个简单的 $\sigma$-代数论证，可以证明[连续函数](@entry_id:137361)将任意 Borel 集的[原像](@entry_id:150899)映射为 Borel 集。

#### 外函数为[连续函数](@entry_id:137361)

一个最基本且应用广泛的定理是，当外函数连续时，[复合函数](@entry_id:147347)保持[可测性](@entry_id:199191)。

**定理**：设 $f: (X, \mathcal{M}) \to (\mathbb{R}, \mathcal{B}(\mathbb{R}))$ 是一个可测函数，$g: \mathbb{R} \to \mathbb{R}$ 是一个[连续函数](@entry_id:137361)。则复合函数 $h = g \circ f$ 是 $\mathcal{M}$-可测的。

**证明**：为了证明 $h$ 是可测的，我们需要证明对于任意 Borel 集 $B \in \mathcal{B}(\mathbb{R})$，集合 $h^{-1}(B)$ 都属于 $\mathcal{M}$。根据复合函数的原像公式，我们有 $h^{-1}(B) = f^{-1}(g^{-1}(B))$。

证明的关键在于分析 $g^{-1}(B)$ 的性质 [@problem_id:1410540]。因为 $g$ 是[连续函数](@entry_id:137361)，它不仅将开集[拉回](@entry_id:160816)到开集，而且可以将任意 Borel 集[拉回](@entry_id:160816)到 Borel 集。我们可以通过如下方式严格证明这一点：定义一个集合族 $\mathcal{C} = \{ S \subseteq \mathbb{R} \mid g^{-1}(S) \in \mathcal{B}(\mathbb{R}) \}$。不难验证 $\mathcal{C}$ 是一个 $\sigma$-代数。由于 $g$ 连续，对任意开集 $O \subseteq \mathbb{R}$，$g^{-1}(O)$ 是开集，因此是 Borel 集，即 $O \in \mathcal{C}$。因为 $\mathcal{B}(\mathbb{R})$ 是包含所有开集的最小 $\sigma$-代数，所以必然有 $\mathcal{B}(\mathbb{R}) \subseteq \mathcal{C}$。这恰恰说明，对于任意 Borel 集 $B \in \mathcal{B}(\mathbb{R})$，其[原像](@entry_id:150899) $g^{-1}(B)$ 也是一个 Borel 集。

现在，回到我们的[复合函数](@entry_id:147347)。由于 $g^{-1}(B)$ 是一个 Borel 集，而函数 $f$ 本身是可测的（即它将任何 Borel 集的原像映射到 $\mathcal{M}$ 中的集合），因此 $f^{-1}(g^{-1}(B))$ 必然属于 $\mathcal{M}$。这就完成了证明。

#### 内函数为[连续函数](@entry_id:137361)

当内函数为[连续函数](@entry_id:137361)时，情况变得更加微妙。考虑[复合函数](@entry_id:147347) $k = g \circ f$，其中 $g: (X, \mathcal{M}) \to (\mathbb{R}, \mathcal{B}(\mathbb{R}))$ 是一个可测函数，$f: \mathbb{R} \to \mathbb{R}$ 是一个[连续函数](@entry_id:137361)。

我们考察[原像](@entry_id:150899) $k^{-1}(B) = f^{-1}(g^{-1}(B))$。由于 $g$ 是可测函数，$g^{-1}(B)$ 是 $\mathcal{M}$-可测集（这里假设 $\mathcal{M}$ 是 Lebesgue $\sigma$-代数）。然而，问题在于[连续函数](@entry_id:137361) $f$ 是否保证将一个 Lebesgue [可测集](@entry_id:159173)（不一定是 Borel 集）的原像映射回一个 Lebesgue [可测集](@entry_id:159173)。答案是否定的。

因此，“Lebesgue 可测函数 $\circ$ [连续函数](@entry_id:137361)”的可测性并不总是成立。这个重要的结论将在稍后的“一个重要的警示”一节中通过一个经典反例来详细阐述 [@problem_id:1410558]。

### 推广与拓展

连续性是一个很强的条件。实际上，保证复合函数[可测性](@entry_id:199191)的更本质的属性是 Borel 可测性。

#### Borel [可测函数的复合](@entry_id:204359)

**定理**：若 $f: \mathbb{R} \to \mathbb{R}$ 和 $g: \mathbb{R} \to \mathbb{R}$ 都是 Borel [可测函数](@entry_id:159040)，则其复合 $g \circ f$ 和 $f \circ g$ 也都是 Borel 可测的 [@problem_id:1410547] [@problem_id:1410558]。

证明是直接的。以 $g \circ f$ 为例：对任意 Borel 集 $B$，由于 $g$ 是 Borel 可测的，$g^{-1}(B)$ 是一个 Borel 集。又因为 $f$ 是 Borel 可测的，它将 Borel 集的原像映射为 Borel 集，所以 $f^{-1}(g^{-1}(B))$ 是一个 Borel 集。因此，$g \circ f$ 是 Borel 可测的。

由于[连续函数](@entry_id:137361)必为 Borel 可测函数，上一节的两个经典结果都可以看作是这个更[一般性](@entry_id:161765)定理的直接推论。

#### 单调性的角色

除了[连续函数](@entry_id:137361)，另一类常见的保证 Borel 可测性的函数是单调函数。一个在 $\mathbb{R}$ 上定义的[单调函数](@entry_id:145115)（不必是严格单调或连续的）一定是 Borel 可测的 [@problem_id:1410537]。

其理由在于，对于任意单调函数 $g$ 和任意实数 $c$，其水平[子集](@entry_id:261956)（sublevel set）$\{y \in \mathbb{R} \mid g(y) \le c\}$ 必然是一个区间（或射线，如 $(-\infty, a]$ 或 $(-\infty, a)$）。区间都是 Borel 集。由于形如 $(-\infty, c]$ 的集合能够生成 Borel $\sigma$-代数，这足以证明 $g$ 是 Borel 可测的。

因此，我们有以下推论：
**推论**：若 $f$ 是[可测函数](@entry_id:159040)，$g$ 是单调函数，则 $g \circ f$ 是[可测函数](@entry_id:159040)。

#### 可测函数的代数组合

[函数复合](@entry_id:144881)是组合函数的一种方式，另一种常见方式是代数运算，如加法和乘法。这些运算也可以看作复合的一种形式。例如，两个函数 $f$ 和 $g$ 的和 $h(x) = f(x) + g(x)$ 可以看作是先通过映射 $x \mapsto (f(x), g(x))$ 将 $x$ 映到 $\mathbb{R}^2$ 中，然后再将结果通过加法映射 $A(u,v) = u+v$ 映回 $\mathbb{R}$。

**定理**：若 $f$ 和 $g$ 都是（Borel 或 Lebesgue）[可测函数](@entry_id:159040)，则它们的和 $f+g$、积 $f \cdot g$ 也是可测的 [@problem_id:1410547]。

证明的要点在于：
1. 映射 $H(x) = (f(x), g(x))$ 是从 $(\mathbb{R}, \mathcal{M})$ 到 $(\mathbb{R}^2, \mathcal{B}(\mathbb{R}^2))$ 的可测函数。
2. 加法运算 $A(u,v) = u+v$ 和乘法运算 $M(u,v) = uv$ 都是从 $\mathbb{R}^2$到 $\mathbb{R}$ 的[连续函数](@entry_id:137361)，因此它们是 Borel 可测的。
3. 于是 $f+g = A \circ H$ 和 $f \cdot g = M \circ H$ 都是可测函数与连续（[Borel可测](@entry_id:140719)）[函数复合](@entry_id:144881)的结果，因此它们是可测的。

### 示例解析与应用

理论的生命力在于应用。让我们通过一系列具体的例子来巩固和深化对上述原理的理解。

**示例 1：判断各种[复合函数](@entry_id:147347)的可测性 [@problem_id:1410553]**
- 令 $h_1(x) = \begin{cases} 1  \text{ if } \sin(x) \in \mathbb{Q} \\ 0  \text{ if } \sin(x) \notin \mathbb{Q} \end{cases}$。这可以写成 $h_1 = \mathbb{1}_{\mathbb{Q}} \circ \sin$。函数 $\sin(x)$ 是连续的，而有理数集 $\mathbb{Q}$ 是 Borel 集，其[指示函数](@entry_id:186820) $\mathbb{1}_{\mathbb{Q}}$ 是 Borel 可测的。根据“Borel 可测 $\circ$ 连续”的原则，$h_1$ 是 Borel 可测的。

- 令 $h_2(x) = \lfloor \exp(-x^2) \rfloor$。函数 $x \mapsto \exp(-x^2)$ 是连续的，其值域为 $(0, 1]$。[取整函数](@entry_id:265373) $\lfloor \cdot \rfloor$ 是一个阶梯函数，它是 Borel 可测的。因此，$h_2$ 作为 Borel [可测函数](@entry_id:159040)与[连续函数的复合](@entry_id:139194)，是 Borel 可测的。事实上，我们可以直接计算出 $h_2(x)$ 在 $x=0$ 时为 $1$，在 $x \ne 0$ 时为 $0$，即 $h_2 = \mathbb{1}_{\{0\}}$，这显然是可测的。

- 考虑 Thomae 函数 $f(y)$（在有理点取非零值，无理点取零值）与 $g(x)=x^4$ 的复合 $h_5(x)=f(x^4)$。Thomae 函数是 Borel 可测的，而 $x^4$ 是连续的，因此其复合 $h_5$ 是 Borel 可测的。

**示例 2：计算[复合函数](@entry_id:147347)的积分 [@problem_id:1410556]**
考虑 $f(x) = \exp(\cos(x)) - 1$ 和一个[简单函数](@entry_id:137521) $s(y)$。我们想计算集合 $E = \{x \in [0, 2\pi] : s(f(x)) = 5\}$ 的 Lebesgue 测度。假设 $s(y)=5$ 的条件是 $y \in [0, \sqrt{e}-1]$。

要找到集合 $E$，我们只需“解开”复合：
$$
s(f(x)) = 5 \iff f(x) \in [0, \sqrt{e}-1]
$$
代入 $f(x)$ 的定义，我们得到：
$$
0 \le \exp(\cos(x)) - 1 \le \sqrt{e}-1
$$
整理后得到：
$$
1 \le \exp(\cos(x)) \le \sqrt{e}
$$
对不等式取自然对数，我们得到关于 $\cos(x)$ 的条件：
$$
0 \le \cos(x) \le \frac{1}{2}
$$
现在问题转化为一个基本问题：在 $[0, 2\pi]$ 上找出满足此条件的 $x$ 的集合，并计算其测度。该集合为 $[\frac{\pi}{3}, \frac{\pi}{2}] \cup [\frac{3\pi}{2}, \frac{5\pi}{3}]$，其总长度（Lebesgue 测度）为 $(\frac{\pi}{2} - \frac{\pi}{3}) + (\frac{5\pi}{3} - \frac{3\pi}{2}) = \frac{\pi}{3}$。这个例子生动地展示了如何通过反向追溯复合过程来处理与[可测性](@entry_id:199191)相关的问题。

### 一个重要的警示：复合运算的局限性

到目前为止，我们建立的图像似乎非常和谐：[可测函数](@entry_id:159040)与 Borel 可测函数（特别是连续和单调函数）的复合总是产生可测函数。然而，这个美好的图景有一个至关重要的例外，它源于 Lebesgue 可测集与 Borel [可测集](@entry_id:159173)之间的微妙差异。

#### Lebesgue 可测性与 Borel 可测性的区别

Borel $\sigma$-代数 $\mathcal{B}(\mathbb{R})$ 是由所有开集生成的最小 $\sigma$-代数。而 Lebesgue $\sigma$-代数 $\mathcal{L}$ 是对 $\mathcal{B}(\mathbb{R})$ 的完备化。这意味着 $\mathcal{L}$ 不仅包含所有 Borel 集，还包含了所有 Lebesgue 测度为零的 Borel 集的[子集](@entry_id:261956)。因此，我们有严格的包含关系 $\mathcal{B}(\mathbb{R}) \subsetneq \mathcal{L}$。存在一些集合，它们是 Lebesgue 可测的，但不是 Borel 集。例如，一个标准 Cantor 集的测度为零，它的任何[子集](@entry_id:261956)（即使是像 Vitali 集那样高度病态的集合的变体）都是 Lebesgue 可测的，但通常不是 Borel 集。

一个函数是 Borel 可测的，如果它[拉回](@entry_id:160816)的 Borel 集总是 Borel 集。一个函数是 Lebesgue 可测的，如果它[拉回](@entry_id:160816)的 Borel 集是 Lebesgue 可测集。由于 $\mathcal{B}(\mathbb{R}) \subset \mathcal{L}$，任何 Borel [可测函数](@entry_id:159040)也必然是 Lebesgue 可测的。但反之不成立。一个函数的[原像](@entry_id:150899)可能是 Lebesgue 可测集而非 Borel 集，这样的函数就是 Lebesgue 可测而非 Borel 可测的。

#### 一个反例：当复合运算失效时

现在，让我们考虑以下情况：Lebesgue [可测函数](@entry_id:159040) $\circ$ [连续函数](@entry_id:137361)。我们的直觉可能会认为这也是可测的，但事实并非如此。

**定理（反例）**：存在一个 Lebesgue 可测函数 $f: \mathbb{R} \to \mathbb{R}$ 和一个[连续函数](@entry_id:137361) $g: \mathbb{R} \to \mathbb{R}$，使得其复合 $f \circ g$ 不是 Lebesgue 可测的 [@problem_id:1410565] [@problem_id:1410558]。

这个经典反例的构造相当精巧，其核心思想如下：
1. 构造一个特殊的[连续函数](@entry_id:137361) $g$（通常基于 Cantor-Lebesgue 函数），它是一个[同胚](@entry_id:146933)（即连续、[双射](@entry_id:138092)且逆也连续），但它会将一个测度为零的 Borel 集（如 Cantor 集 $C$）映射到一个测度为正的集合 $g(C)$。
2. 因为 $g(C)$ 测度为正，它必然包含一个非 Lebesgue 可测的[子集](@entry_id:261956)，我们称之为 $E$。
3. 定义一个集合 $A = g^{-1}(E)$。由于 $E \subset g(C)$，所以 $A \subset C$。因为 Cantor 集 $C$ 的 Lebesgue [测度为零](@entry_id:137864)，并且 Lebesgue 测度是完备的，所以它的任何[子集](@entry_id:261956)（包括 $A$）都是 Lebesgue 可测的，且测度为零。
4. 定义函数 $f = \mathbb{1}_A$。由于 $A$ 是 Lebesgue [可测集](@entry_id:159173)，所以 $f$ 是一个 Lebesgue [可测函数](@entry_id:159040)。
5. 现在考察复合函数 $f \circ g$。对于任意 $x$，$(f \circ g)(x) = f(g(x)) = \mathbb{1}_A(g(x))$。这个值等于 $1$ 当且仅当 $g(x) \in A$，即 $g(x) \in g^{-1}(E)$，这等价于 $x \in E$。因此，$f \circ g = \mathbb{1}_E$。
6. 由于我们从一开始就选择了 $E$ 作为一个非 Lebesgue [可测集](@entry_id:159173)，它的指示函数 $\mathbb{1}_E$ 也就不是 Lebesgue 可测函数。

这个反例揭示了问题的根源：当 $f$ 仅是 Lebesgue 可测而非 Borel 可测时，$f^{-1}(\text{Borel})$ 得到的是一个 Lebesgue [可测集](@entry_id:159173) $L$，它可能不是 Borel 集。当我们再用[连续函数](@entry_id:137361) $g$ 将其[拉回](@entry_id:160816)时，我们得到 $g^{-1}(L)$。然而，[连续函数](@entry_id:137361)只保证将 Borel 集[拉回](@entry_id:160816)到 Borel 集，它并不保证将一个普通的 Lebesgue [可测集](@entry_id:159173)[拉回](@entry_id:160816)到 Lebesgue 可测集。因此，链条在此断裂。

总结一下关于复合的规则（以 Lebesgue [可测性](@entry_id:199191)为标准）：
- **Borel 可测 $\circ$ Lebesgue 可测 $\implies$ Lebesgue 可测** (特别地, **连续 $\circ$ Lebesgue 可测 $\implies$ Lebesgue 可测**) [@problem_id:1410558]。
- **Lebesgue 可测 $\circ$ Borel 可测 $\implies$ 不一定可测** (特别地, **Lebesgue 可测 $\circ$ 连续 $\implies$ 不一定可测**)。

这种不对称性是[测度论](@entry_id:139744)中一个深刻而重要的教训。

### 高阶视角与特殊情况

#### 一种通过逼近的替代证明

对于“连续 $\circ$ 可测”得到可测这一经典结果，除了使用原像和 $\sigma$-代数的标准证明外，还有一种基于[函数逼近](@entry_id:141329)的替代思路 [@problem_id:1410559]。我们可以利用分析学中的强大工具来证明 $g \circ f$ 的[可测性](@entry_id:199191)（其中 $g$ 连续，$f$ 可测）。

该策略的步骤如下：
1. **逼近**：根据 Weierstrass 逼近定理，任何在[闭区间](@entry_id:136474)上连续的函数都可以被多项式[一致逼近](@entry_id:159809)。我们可以将此推广到整个实轴：对于[连续函数](@entry_id:137361) $g$，可以找到一列多项式函数 $\{p_n\}_{n=1}^{\infty}$，使得对于任意 $t \in \mathbb{R}$，都有 $\lim_{n \to \infty} p_n(t) = g(t)$。
2. **构造复合序列**：定义 $h_n = p_n \circ f$。由于 $p_n$ 是多项式，形如 $p_n(t) = \sum_{k=0}^m a_k t^k$。因此，$h_n(x) = \sum_{k=0}^m a_k (f(x))^k$。
3. **证明每一项的[可测性](@entry_id:199191)**：因为 $f$ 是可测的，根据可测函数的代数性质，它的任意次幂 $f^k$ 也是可测的，常数倍和有限和也保持可测性。因此，每个 $h_n$ 都是[可测函数](@entry_id:159040)。
4. **取极限**：复合函数 $h = g \circ f$ 是函数序列 $\{h_n\}$ 的[逐点极限](@entry_id:193549)。由于[可测函数的逐点极限](@entry_id:186907)仍然是[可测函数](@entry_id:159040)，我们得出结论 $h$ 是可测的。

这个证明路径不仅巧妙地绕开了对原像的直接操作，而且还将[可测性](@entry_id:199191)理论与函数逼近理论紧密地联系在一起，展示了数学不同分支之间的内在统一性。

#### 当不可测部分产生可测结果时

我们已经看到，函数的复合可能会因为其中一个组分是“坏”的（例如非 Lebesgue 可测）而导致结果也是“坏”的。然而，一个“坏”的组分并不必然导致“坏”的结果。

考虑这样一个问题：是否可以构造一个非[可测函数](@entry_id:159040) $f$ 和一个连续的非恒定函数 $g$，使得它们的复合 $g \circ f$ 是一个常数函数（因此是可测的）？[@problem_id:1410548]

答案是肯定的。设 $V \subset [0,1]$ 是一个非 Lebesgue 可测的 Vitali 集。定义 $f: \mathbb{R} \to \{0,1\}$ 为 $f(x) = \mathbb{1}_V(x - \lfloor x \rfloor)$。这个函数是周期的，并且它在一个周期内的可测性等价于 $V$ 的[可测性](@entry_id:199191)，因此 $f$ 是一个非可测函数。

现在，选择一个连续且非恒定的函数 $g: [0,1] \to \mathbb{R}$，但它在 $f$ 的值域 $\{0, 1\}$ 上取值相同。一个绝佳的选择是 $g(y) = \cos(2\pi y)$。这个函数是连续且非恒定的。

我们来计算[复合函数](@entry_id:147347) $h = g \circ f$：
$$
h(x) = g(f(x)) = \cos(2\pi f(x))
$$
由于 $f(x)$ 的取值只能是 $0$ 或 $1$，我们有：
- 如果 $f(x)=0$，则 $h(x) = \cos(0) = 1$。
- 如果 $f(x)=1$，则 $h(x) = \cos(2\pi) = 1$。
因此，无论 $f(x)$ 取何值，复合函数 $h(x)$ 始终为 $1$。这是一个[常数函数](@entry_id:152060)，所以它是可测的（甚至是连续的）。

这个例子提醒我们，关于复合[可测性](@entry_id:199191)的定理通常提供的是**充分条件**。当条件不满足时（例如内函数非可测），我们不能断定复合函数一定非可测。最终的结果取决于函数间的具体相互作用，例如外函数可能将其定义域中的“病态”部分“压缩”掉。