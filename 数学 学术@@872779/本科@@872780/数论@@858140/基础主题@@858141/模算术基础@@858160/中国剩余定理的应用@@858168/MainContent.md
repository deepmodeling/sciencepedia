## 引言
中国剩余定理（Chinese Remainder Theorem, CRT），一个源自古代中国的数学瑰宝，是数论中关于求解线性[同余[方程](@entry_id:154048)组](@entry_id:193238)的基石性成果。它的意义远不止于一个优美的理论，更在于其为现代科学技术中许多看似无关的问题提供了统一的解决框架。然而，人们往往只关注其理论表述，而忽略了其在现实世界中解决问题的巨大威力。本文旨在弥合理论与实践之间的鸿沟，系统地揭示[中国剩余定理](@entry_id:144030)的深刻内涵及其在多个领域的广泛应用。

在接下来的内容中，我们将分三个章节展开探索。首先，在**“原理与机制”**一章，我们将深入剖析定理的数学核心，从[互质模数](@entry_id:274776)的经典形式出发，借助抽象代数的语言揭示其背后的[环同构](@entry_id:147982)结构，并介绍实用的构造性求解算法。随后，在**“应用与跨学科联系”**一章，我们将把目光投向更广阔的领域，展示CRT如何在密码学、数字信号处理、计算几何和算法设计中扮演关键角色，将抽象理论转化为强大的计算工具。最后，在**“动手实践”**部分，我们提供了一系列精心设计的问题，旨在通过实际操作加深读者对定理的理解和应用能力。通过这一系列的学习，读者将全面掌握[中国剩余定理](@entry_id:144030)的精髓，并能将其思想应用于解决实际问题。

## 原理与机制

在介绍章节之后，我们现在深入探讨中国剩余定理（Chinese Remainder Theorem, CRT）的数学原理及其应用机制。本章将从该定理最核心的表述出发，逐步揭示其背后的[代数结构](@entry_id:137052)，介绍求解[同余方程组](@entry_id:154048)的构造性算法，并最终将其推广至更一般的情形。

### 中国剩余定理：[存在性与唯一性](@entry_id:263101)

[中国剩余定理](@entry_id:144030)是数论中一个关于求解线性[同余[方程](@entry_id:154048)组](@entry_id:193238)的深刻结果。它不仅保证了在特定条件下解的存在性和唯一性，还揭示了[整数环](@entry_id:181003)的模算术结构。

#### [互质](@entry_id:143119)模的经典陈述

[中国剩余定理](@entry_id:144030)的经典形式处理的是模数[两两互质](@entry_id:154147)（pairwise coprime）的情形。其内容可以表述如下：

**定理（[中国剩余定理](@entry_id:144030)）：** 设 $n_1, n_2, \dots, n_k$ 是 $k$ 个大于 $1$ 的[两两互质](@entry_id:154147)的正整数。对于任意给定的整数 $a_1, a_2, \dots, a_k$，[同余方程组](@entry_id:154048)
$$
\begin{cases}
x \equiv a_1 \pmod{n_1} \\
x \equiv a_2 \pmod{n_2} \\
\vdots \\
x \equiv a_k \pmod{n_k}
\end{cases}
$$
总是有解的。若 $x_0$ 是一个解，则该[方程组](@entry_id:193238)的通解可以表示为 $x \equiv x_0 \pmod{N}$，其中 $N = n_1 n_2 \cdots n_k$。换言之，该[方程组](@entry_id:193238)在模 $N$ 的意义下有唯一解。

#### [环论](@entry_id:143825)视角

中国剩余定理的深刻内涵可以通过抽象代数的语言得到更清晰的揭示。考虑一个整数 $x$ 模 $N$ 的[剩余类](@entry_id:185226) $[x]_N$。我们可以定义一个映射 $\varphi$，它将 $[x]_N$ 同时映射到其模 $n_i$ 的各个[剩余类](@entry_id:185226)上：
$$
\varphi: \mathbb{Z}/N\mathbb{Z} \to \prod_{i=1}^k \mathbb{Z}/n_i\mathbb{Z}
$$
其定义为
$$
\varphi([x]_N) = ([x]_{n_1}, [x]_{n_2}, \dots, [x]_{n_k})
$$
这个映射 $\varphi$ 是一个**[环同态](@entry_id:153804)**，意味着它同时保持了加法和乘法结构。中国剩余定理的本质是，当模数 $n_1, \dots, n_k$ [两两互质](@entry_id:154147)时，这个[环同态](@entry_id:153804) $\varphi$ 实际上是一个**[环同构](@entry_id:147982)**（ring isomorphism）[@problem_id:3081329]。

“同构”意味着 $\varphi$ 是一个[双射](@entry_id:138092)（bijection），即它既是[单射](@entry_id:183792)（injective）又是满射（surjective）。
- **满射性**意味着对于目标环 $\prod \mathbb{Z}/n_i\mathbb{Z}$ 中的任意一个元素——即任意一个余数组 $([a_1]_{n_1}, \dots, [a_k]_{n_k})$——都存在一个源环 $\mathbb{Z}/N\mathbb{Z}$ 中的元素 $[x]_N$ 映射到它。这恰恰是说，对于任意的 $a_i$，[同余方程组](@entry_id:154048) $x \equiv a_i \pmod{n_i}$ 总是有解。
- **[单射性](@entry_id:147722)**意味着如果两个元素 $[x]_N$ 和 $[y]_N$ 映射到同一个余数组，那么它们必然是同一个元素。这保证了解在模 $N$ 意义下的唯一性。如果 $x$ 和 $y$ 都是解，则它们模 $N$ [同余](@entry_id:143700)，而不是模 $n_1 + \dots + n_k$ [同余](@entry_id:143700) [@problem_id:3081329]。

#### 模数[互质](@entry_id:143119)的必要性

如果模数 $n_i$ 不满足[两两互质](@entry_id:154147)的条件，那么映射 $\varphi$ 将不再是同构。具体来说，它既不是[单射](@entry_id:183792)，也不是满射 [@problem_id:3081325]。

**[单射性](@entry_id:147722)的失效**：一个同态是单射的，当且仅当其核（kernel）是平凡的（只包含零元素）。$\varphi$ 的核由所有映射到零元组 $([0]_{n_1}, \dots, [0]_{n_k})$ 的 $[x]_N$ 构成。这意味着 $x$ 必须是所有 $n_i$ 的公倍数，即 $x$ 是 $\operatorname{lcm}(n_1, \dots, n_k)$ 的倍数。当 $n_i$ [两两互质](@entry_id:154147)时，$\operatorname{lcm}(n_1, \dots, n_k) = n_1 \cdots n_k = N$，所以核中的元素必须是 $N$ 的倍数，这意味着在 $\mathbb{Z}/N\mathbb{Z}$ 中只有 $[0]_N$。

然而，当存在某对 $(i, j)$ 使得 $\gcd(n_i, n_j) > 1$ 时，$\operatorname{lcm}(n_1, \dots, n_k)$ 将严格小于 $N$。例如，考虑 $n_1=6, n_2=10$。则 $N=60$，但 $\operatorname{lcm}(6, 10)=30$。这意味着 $[30]_{60}$ 是一个非零元素，但 $\varphi([30]_{60}) = ([30]_6, [30]_{10}) = ([0]_6, [0]_{10})$，即 $[30]_{60}$ 在核中。这证明了映射不是[单射](@entry_id:183792)的 [@problem_id:3081325]。

**满射性的失效**：由于源集和目标集的大小均为 $N$，根据[有限集](@entry_id:145527)之间的映射原理，一个非单射的映射也必然非满射。这意味着并非所有的余数组 $(a_1, \dots, a_k)$ 都能作为[同余方程组](@entry_id:154048)的右侧，并得到解。一个解 $x$ 必须同时满足 $x \equiv a_i \pmod{n_i}$ 和 $x \equiv a_j \pmod{n_j}$。这蕴含着 $x-a_i$ 是 $n_i$ 的倍数， $x-a_j$ 是 $n_j$ 的倍数。因此，它们的差 $a_j-a_i = (x-a_i)-(x-a_j)$ 必须是 $\gcd(n_i, n_j)$ 的倍数。这导出一个**[相容性条件](@entry_id:637057)**：
$$
a_i \equiv a_j \pmod{\gcd(n_i, n_j)}
$$
对于所有 $i, j$ 都必须成立。当 $\gcd(n_i, n_j) > 1$ 时，这是一个非平凡的限制。例如，对于 $n_1=6, n_2=10$，$\gcd(6,10)=2$。余数组 $([1]_6, [0]_{10})$ 就不满足[相容性条件](@entry_id:637057)，因为 $1 \not\equiv 0 \pmod 2$。因此，[同余方程组](@entry_id:154048) $x \equiv 1 \pmod 6, x \equiv 0 \pmod{10}$ 无解，这表明 $\varphi$ 不是满射的 [@problem_id:3081325]。

### 求解[同余方程组](@entry_id:154048)的构造性算法

中国剩余定理不仅是一个[存在性定理](@entry_id:261096)，其经典证明本身就提供了一种构造解的算法。此外，还有其他算法，如 Garner 算法，在计算上更具优势。

#### 经典构造法（基于裴蜀等式）

该方法的目标是构造一个解 $x$。其核心思想是为每个同余方程 $x \equiv a_i \pmod{n_i}$ 构造一个“[基本解](@entry_id:184782)” $e_i$，这个[基本解](@entry_id:184782)满足：
$$
e_i \equiv 1 \pmod{n_i} \quad \text{且} \quad e_i \equiv 0 \pmod{n_j} \text{ for } j \neq i
$$
一旦我们找到了这样的 $k$ 个基本解 $e_1, \dots, e_k$，那么[方程组](@entry_id:193238)的一个[特解](@entry_id:149080)就可以通过[线性组合](@entry_id:154743)得到：
$$
x_0 = a_1 e_1 + a_2 e_2 + \dots + a_k e_k
$$
验证这个解是容易的：当我们对 $x_0$ 模 $n_i$ 时，所有 $j \neq i$ 的项 $a_j e_j$ 都因 $e_j \equiv 0 \pmod{n_i}$ 而消失，只剩下 $a_i e_i$。由于 $e_i \equiv 1 \pmod{n_i}$，我们得到 $x_0 \equiv a_i \pmod{n_i}$。

构造 $e_i$ 的步骤如下：
1.  令 $M_i = N/n_i = n_1 \cdots n_{i-1} n_{i+1} \cdots n_k$。由于 $n_j$ [两两互质](@entry_id:154147)，我们有 $\gcd(M_i, n_i) = 1$。
2.  根据裴蜀（Bézout）等式，既然 $M_i$ 和 $n_i$ [互质](@entry_id:143119)，则存在整数 $y_i$ 和 $z_i$ 使得 $y_i M_i + z_i n_i = 1$。这意味着 $y_i M_i \equiv 1 \pmod{n_i}$。这个 $y_i$ 就是 $M_i$ 模 $n_i$ 的乘法[逆元](@entry_id:140790)。我们可以使用**[扩展欧几里得算法](@entry_id:153449)**（Extended Euclidean Algorithm）来高效地计算 $y_i$ [@problem_id:3081341]。
3.  令 $e_i = y_i M_i$。根据 $y_i$ 的定义，我们有 $e_i \equiv 1 \pmod{n_i}$。同时，对于任何 $j \neq i$，$n_j$ 是 $M_i$ 的一个因子，因此 $M_i \equiv 0 \pmod{n_j}$，从而 $e_i \equiv 0 \pmod{n_j}$。这正是我们所需要的性质。

这些元素 $e_i$ 在更广泛的代数背景下被称为**正交[幂等元](@entry_id:153117)**（orthogonal idempotents），它们满足 $\overline{e_i}^2 = \overline{e_i}$，$\overline{e_i}\overline{e_j} = \overline{0}$（对于 $i \neq j$），以及 $\sum \overline{e_i} = \overline{1}$（在环 $\mathbb{Z}/N\mathbb{Z}$ 中） [@problem_id:3081341] [@problem_id:3081357]。

**示例：** 求解[同余方程组](@entry_id:154048) [@problem_id:3081361]
$$
\begin{cases}
x \equiv 54 \pmod{77} \\
x \equiv 27 \pmod{64} \\
x \equiv 13 \pmod{45}
\end{cases}
$$
这里 $n_1=77, n_2=64, n_3=45$ [两两互质](@entry_id:154147)。$N = 77 \cdot 64 \cdot 45 = 221760$。
1.  $M_1 = 64 \cdot 45 = 2880$。我们需求解 $2880 y_1 \equiv 1 \pmod{77}$。即 $31 y_1 \equiv 1 \pmod{77}$。通过[扩展欧几里得算法](@entry_id:153449)得 $y_1=5$。所以 $e_1 = 5 \cdot 2880 = 14400$。
2.  $M_2 = 77 \cdot 45 = 3465$。我们需求解 $3465 y_2 \equiv 1 \pmod{64}$。即 $9 y_2 \equiv 1 \pmod{64}$。得 $y_2 = 57$。所以 $e_2 = 57 \cdot 3465 = 197505$。
3.  $M_3 = 77 \cdot 64 = 4928$。我们需求解 $4928 y_3 \equiv 1 \pmod{45}$。即 $23 y_3 \equiv 1 \pmod{45}$。得 $y_3=2$。所以 $e_3 = 2 \cdot 4928 = 9856$。

[特解](@entry_id:149080)为 $x_0 = 54 e_1 + 27 e_2 + 13 e_3 = 54(14400) + 27(197505) + 13(9856) = 6238363$。
最小非负解为 $x = 6238363 \pmod{221760} = 29083$。

#### Garner 算法（混合基数表示）

经典构造法中的中间数 $e_i$ 和 $x_0$ 可能会非常大。Garner 算法提供了一种迭代方法，可以有效控制中间计算结果的大小。其思想是将解 $x$ 表示为一种**混合基数形式**（mixed-radix representation）：
$$
x = v_1 + v_2 n_1 + v_3 n_1 n_2 + \dots + v_k n_1 \cdots n_{k-1}
$$
其中系数 $v_i$ 满足 $0 \le v_i \lt n_i$。我们可以逐个确定这些系数。

1.  **求 $v_1$**：对[方程组](@entry_id:193238)的第一个[同余](@entry_id:143700)式 $x \equiv a_1 \pmod{n_1}$ 应用混合[基数](@entry_id:754020)表达式，我们得到 $v_1 \equiv a_1 \pmod{n_1}$。由于 $0 \le v_1 \lt n_1$，所以 $v_1 = a_1 \pmod{n_1}$ 的最小非负余数。
2.  **求 $v_2$**：利用第二个[同余](@entry_id:143700)式 $x \equiv a_2 \pmod{n_2}$，我们有 $v_1 + v_2 n_1 \equiv a_2 \pmod{n_2}$。这是一个关于 $v_2$ 的[线性同余](@entry_id:150485)方程，可以解出 $v_2 \equiv (a_2 - v_1) (n_1^{-1} \pmod{n_2}) \pmod{n_2}$。
3.  **求 $v_i$**：依此类推，对于第 $i$ 个同余式，我们有 $v_1 + v_2 n_1 + \dots + v_i n_1 \cdots n_{i-1} \equiv a_i \pmod{n_i}$。这可以解出 $v_i$。

这种方法将一个大的[联立方程](@entry_id:193238)组[问题分解](@entry_id:272624)为一系列小的、独立的[模逆元](@entry_id:149786)和[线性同余](@entry_id:150485)方程求解问题，在计算机实现中尤为高效 [@problem_id:3081314]。

### 同构的结构性推论与应用

CRT 揭示的[环同构](@entry_id:147982) $\mathbb{Z}/N\mathbb{Z} \cong \prod \mathbb{Z}/n_i\mathbb{Z}$ 具有深远的结构性推论，使其在数论和密码学中有广泛应用。

#### [单位群](@entry_id:184012)的分解

一个[环同构](@entry_id:147982)会诱导其单位群（group of units）之间的同构。环 $R$ 的[单位群](@entry_id:184012) $R^\times$ 是由 $R$ 中所有可逆元素构成的乘法群。一个元素 $[x]_N \in \mathbb{Z}/N\mathbb{Z}$ 是可逆的（即是一个单位），当且仅当 $\gcd(x, N) = 1$。

由于 $\varphi$ 是[环同构](@entry_id:147982)，它保持乘法和乘法单位元。可以证明，一个元素 $[x]_N$ 在 $\mathbb{Z}/N\mathbb{Z}$ 中可逆，当且仅当其像 $\varphi([x]_N) = ([x]_{n_1}, \dots, [x]_{n_k})$ 在积环 $\prod \mathbb{Z}/n_i\mathbb{Z}$ 中可逆。而积环中的元素可逆，当且仅当它的每一个分量都在各自的环中可逆。因此，$[x]_N$ 可逆当且仅当每一个 $[x]_{n_i}$ 都在 $\mathbb{Z}/n_i\mathbb{Z}$ 中可逆 [@problem_id:3081354]。
这导出了[单位群](@entry_id:184012)之间的[群同构](@entry_id:147371)：
$$
(\mathbb{Z}/N\mathbb{Z})^\times \cong \prod_{i=1}^k (\mathbb{Z}/n_i\mathbb{Z})^\times
$$
取群的阶（元素个数），我们就得到了欧拉 $\phi$ 函数的**[乘性](@entry_id:187940)**：如果 $n_1, \dots, n_k$ [两两互质](@entry_id:154147)，则 $\phi(n_1 \cdots n_k) = \phi(n_1) \cdots \phi(n_k)$。

#### 求解[多项式同余](@entry_id:195961)方程

CRT 可以将一个模 $N$ 的[多项式同余](@entry_id:195961)方程 $f(x) \equiv 0 \pmod N$ 分解为一组模 $n_i$ 的子问题。
$$
f(x) \equiv 0 \pmod N \iff
\begin{cases}
f(x) \equiv 0 \pmod{n_1} \\
\vdots \\
f(x) \equiv 0 \pmod{n_k}
\end{cases}
$$
我们可以分别求解每个子问题，然后用 CRT 将解组合起来。

例如，求解 $x^2 \equiv 1 \pmod{1001}$ [@problem_id:3081329]。由于 $1001 = 7 \cdot 11 \cdot 13$，该问题等价于[求解方程组](@entry_id:152624)：
$$
\begin{cases}
x^2 \equiv 1 \pmod{7}  \text{解为 } x \equiv \pm 1 \pmod 7 \\
x^2 \equiv 1 \pmod{11}  \text{解为 } x \equiv \pm 1 \pmod {11} \\
x^2 \equiv 1 \pmod{13}  \text{解为 } x \equiv \pm 1 \pmod {13}
\end{cases}
$$
每个子方程都有 $2$ 个解。根据 CRT，每一种解的组合（例如 $x \equiv 1 \pmod 7, x \equiv -1 \pmod{11}, x \equiv 1 \pmod{13}$）都对应着模 $1001$ 的一个唯一解。因此，总共有 $2 \times 2 \times 2 = 8$ 个不同的解。

#### 推广至一般[交换环](@entry_id:148261)

CRT 的思想可以被推广到任意带单位元的[交换环](@entry_id:148261) $R$。此时，“模数”由环的**理想**（ideals）代替，“互质”条件由**互最大**（comaximal）条件代替。两个理想 $I, J$ 称为互最大，如果 $I+J=R$。对于[整数环](@entry_id:181003) $\mathbb{Z}$，理想 $(n_i)$ 和 $(n_j)$ 互最大当且仅当 $\gcd(n_i, n_j)=1$。

**定理（一般形式的 CRT）：** 若 $R$ 是一个[交换环](@entry_id:148261)， $I_1, \dots, I_k$ 是 $R$ 的一组两两互最大的理想，则存在[环同构](@entry_id:147982)：
$$
R / (I_1 \cap \dots \cap I_k) \cong R/I_1 \times \dots \times R/I_k
$$
这个同构由自然映射 $r + \bigcap I_j \mapsto (r+I_1, \dots, r+I_k)$ 给出 [@problem_id:3081357]。

### 广义[中国剩余定理](@entry_id:144030)（非[互质](@entry_id:143119)模）

当模数不[两两互质](@entry_id:154147)时，我们已经看到[同余方程组](@entry_id:154048)不一定有解。广义[中国剩余定理](@entry_id:144030)给出了有解的充要条件以及解的结构。

#### 存在性条件与唯一性

对于一个一般的[同余方程组](@entry_id:154048) $x \equiv a_i \pmod{n_i}$（$i=1, \dots, k$）：
1.  **存在性**：该[方程组](@entry_id:193238)有解的充要条件是，对于任意一对下标 $(i, j)$，都满足[相容性条件](@entry_id:637057) $a_i \equiv a_j \pmod{\gcd(n_i, n_j)}$ [@problem_id:3081363]。
2.  **唯一性**：如果存在解，则解在模 $N = \operatorname{lcm}(n_1, \dots, n_k)$ 意义下是唯一的。

从几何上看，每个同余方程 $x \equiv a_i \pmod{n_i}$ 的[解集](@entry_id:154326)是整数集 $\mathbb{Z}$ 上的一个[等差数列](@entry_id:265070)，或称为一个陪集（coset）$a_i + n_i\mathbb{Z}$。[求解方程组](@entry_id:152624)就是寻找这些等差数列的交集。当[相容性条件](@entry_id:637057)满足时，这个交集本身也是一个等差数列，其公差为 $\operatorname{lcm}(n_1, \dots, n_k)$ [@problem_id:3081324]。

#### 广义情况的求解算法

##### 方法一：[迭代法](@entry_id:194857)

我们可以通过迭代的方式求解非[互质](@entry_id:143119)模的[方程组](@entry_id:193238)。首先求解前两个[同余](@entry_id:143700)方程：
$$
\begin{cases}
x \equiv a_1 \pmod{n_1} \\
x \equiv a_2 \pmod{n_2}
\end{cases}
$$
如果 $a_1 \equiv a_2 \pmod{\gcd(n_1, n_2)}$，则存在唯一解 $x \equiv b_1 \pmod{\operatorname{lcm}(n_1, n_2)}$。然后，我们将这个新的[同余](@entry_id:143700)方程与第三个方程 $x \equiv a_3 \pmod{n_3}$ 联立求解。重复此过程，直到所有方程都被合并。

**示例：** [求解方程组](@entry_id:152624) [@problem_id:3081324]
$$
x \equiv 3 \pmod{8}, \qquad x \equiv 11 \pmod{12}, \qquad x \equiv 5 \pmod{9}
$$
-   **合并前两个**：$n_1=8, n_2=12, \gcd(8,12)=4$。相容性：$3 \equiv 11 \pmod 4$（因为 $3 \equiv 3, 11 \equiv 3$），成立。解在模 $\operatorname{lcm}(8,12)=24$ 下唯一。由 $x \equiv 3 \pmod 8$ 可知 $x$ 的形式为 $8k+3$。代入第二个方程：$8k+3 \equiv 11 \pmod{12} \implies 8k \equiv 8 \pmod{12}$。此方程的解为 $k \equiv 1 \pmod 3$。取 $k=1$，得 $x = 8(1)+3=11$。故前两个方程的解为 $x \equiv 11 \pmod{24}$。
-   **合并结果与第三个**：现在求解 $x \equiv 11 \pmod{24}$ 和 $x \equiv 5 \pmod{9}$。$n_1'=24, n_3=9, \gcd(24,9)=3$。相容性：$11 \equiv 5 \pmod 3$（因为 $11 \equiv 2, 5 \equiv 2$），成立。解在模 $\operatorname{lcm}(24,9)=72$ 下唯一。由 $x \equiv 11 \pmod{24}$ 可知 $x=24j+11$。代入第三个方程：$24j+11 \equiv 5 \pmod 9 \implies 6j \equiv -6 \pmod 9 \implies 6j \equiv 3 \pmod 9$。此方程解为 $j \equiv 2 \pmod 3$。取 $j=2$，得 $x = 24(2)+11=59$。

最终解为 $x \equiv 59 \pmod{72}$。

##### 方法二：[素数幂](@entry_id:636094)分解法

这是一个更系统化、更强大的方法，特别适合算法实现 [@problem_id:3081352]。
1.  **分解**：将每个模数 $n_i$ 进行[素数幂](@entry_id:636094)分解， $n_i = \prod_p p^{e_{i,p}}$。将每个同余方程 $x \equiv a_i \pmod{n_i}$ 替换为一组等价的[同余](@entry_id:143700)方程 $x \equiv a_i \pmod{p^{e_{i,p}}}$，其中 $p^{e_{i,p}}$ 是 $n_i$ 的素数幂因子。
2.  **重组**：将所有得到的同余方程按素数 $p$ 分组。对于每个素数 $p$，我们得到一个关于该素数的幂为模的子系统。
3.  **求解子系统**：对于每个素数 $p$ 的子系统，检查其内部的相容性：$a_i \equiv a_j \pmod{p^{\min(e_{i,p}, e_{j,p})}}$。如果任何一个子系统不相容，则原[方程组](@entry_id:193238)无解。如果相容，该子系统等价于一个单一的同余方程 $x \equiv b_p \pmod{p^{E_p}}$，其中 $E_p = \max_i(e_{i,p})$ 是该素数的最高次幂。
4.  **合并**：最后，我们得到一个形如 $x \equiv b_p \pmod{p^{E_p}}$ 的新[方程组](@entry_id:193238)。由于不同素数的幂是[两两互质](@entry_id:154147)的，我们可以使用经典的中国剩余定理（例如，使用前述的构造法或 Garner 算法）来求解这个最终的[方程组](@entry_id:193238)，得到模 $\operatorname{lcm}(n_1, \dots, n_k)$ 的唯一解。

这个方法将一个复杂的问题系统地分解为一组标准化的、更容易处理的子问题，充分体现了数学中“分解-解决-合并”的重要思想。