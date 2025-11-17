## 引言
中国剩余定理（Chinese Remainder Theorem, CRT）是数论中一个古老而深刻的定理，它不仅揭示了整数[同余方程组](@entry_id:154048)解的奥秘，更在现代计算领域扮演着意想不到的关键角色。然而，许多学习者常常将其视为一个孤立的纯数学结论，未能充分认识其在解决实际计算问题中的巨大威力。本文旨在填补这一认知鸿沟，系统性地展示[中国剩余定理](@entry_id:144030)从理论到实践的完整图景。

本文将分为三个核心部分。首先，在“原理与机制”一章中，我们将深入探讨CRT的数学基础，从[存在性与唯一性](@entry_id:263101)证明出发，详细介绍两种核心的重构算法——显式求和公式和伽纳算法，并分析其计算效率。接着，在“应用与跨学科联系”一章中，我们将穿越不同学科的边界，探索CRT如何在[密码学](@entry_id:139166)（如加速RSA）、并行计算（剩余数系统）、[容错](@entry_id:142190)系统和高效[算法设计](@entry_id:634229)中成为基石。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者将理论知识转化为解决具体计算挑战的实践能力。通过这段旅程，您将发现CRT不仅是一个优美的数学定理，更是一个解决复杂计算问题的强大“分而治之”工具。

## 原理与机制

本章旨在深入探讨[中国剩余定理](@entry_id:144030) (Chinese Remainder Theorem, CRT) 的核心原理及其在计算问题中的具体应用机制。我们将从该定理的[存在性与唯一性](@entry_id:263101)证明出发，介绍几种关键的重构算法，并对其计算效率进行分析。最后，我们会将讨论扩展到该定理的一般化形式，以处理更为复杂的计算情境。

### [中国剩余定理](@entry_id:144030)：[存在性与唯一性](@entry_id:263101)

[中国剩余定理](@entry_id:144030)是数论中一个关于求解[同余方程组](@entry_id:154048)的深刻结论。它为特定的[同余方程组](@entry_id:154048)提供了存在唯一解的保证，这在理论和实践中都至关重要。

#### 定理的数论表述

[中国剩余定理](@entry_id:144030)的经典表述如下：

设 $k \ge 2$ 为整数，$m_1, m_2, \dots, m_k$ 为一组[两两互质](@entry_id:154147)（pairwise coprime）的正整数，即对于所有 $i \neq j$，均有 $\gcd(m_i, m_j) = 1$。对于任意给定的整数 $a_1, a_2, \dots, a_k$，[同余方程组](@entry_id:154048)：
$$
\begin{cases}
x \equiv a_1 \pmod{m_1} \\
x \equiv a_2 \pmod{m_2} \\
\vdots \\
x \equiv a_k \pmod{m_k}
\end{cases}
$$
在模 $M = \prod_{i=1}^k m_i$ 的意义下有唯一解。

“模 $M$ 唯一解”的精确含义是，若 $x_0$ 是该[方程组](@entry_id:193238)的一个解，那么所有解的集合恰好构成一个[同余类](@entry_id:635978) $\{x_0 + tM \mid t \in \mathbb{Z}\}$。[@problem_id:3081052] 在计算应用中，这使得我们可以通过返回一个唯一的代表元（例如，区间 $[0, M-1]$ 内的最小非负整数）来明确地表示这个解。如果两个整数 $x$ 和 $x'$ 都满足该[方程组](@entry_id:193238)，那么它们的差 $x' - x$ 必然能被每一个 $m_i$ 整除。由于诸 $m_i$ [两两互质](@entry_id:154147)，它们的差也必然能被其乘积 $M$ 整除，即 $x' \equiv x \pmod M$。反之，若 $x$ 是一个解，那么 $x+tM$ 对任意整数 $t$ 都是解，因为 $M$ 是每个 $m_i$ 的倍数，所以 $tM \equiv 0 \pmod{m_i}$。[@problem_id:3081052]

#### 定理的代数视角

从[抽象代数](@entry_id:145216)的角度看，[中国剩余定理](@entry_id:144030)揭示了一个深刻的环结构关系。考虑两个环：整数模 $M$ 的环 $\mathbb{Z}/M\mathbb{Z}$ 和 $k$ 个[环的直积](@entry_id:151334) $\prod_{i=1}^k \mathbb{Z}/m_i\mathbb{Z}$。我们可以定义一个映射 $\phi$：
$$
\phi: \mathbb{Z}/M\mathbb{Z} \to \prod_{i=1}^k \mathbb{Z}/m_i\mathbb{Z}
$$
其定义为 $\phi(x \pmod M) = (x \pmod{m_1}, x \pmod{m_2}, \dots, x \pmod{m_k})$。

中国剩余定理的代数形式断言：当模 $m_i$ [两两互质](@entry_id:154147)时，该映射 $\phi$ 是一个**[环同构](@entry_id:147982) (ring isomorphism)**。[@problem_id:3081009]

一个映射是同构，意味着它是一个保持环运算（加法和乘法）的双射（既是[单射](@entry_id:183792)又是满射）。
- **满射性 (Surjectivity)** 意味着对于目标环中的任意一个元素——即任意一个余数组 $(a_1, \dots, a_k)$——在源环 $\mathbb{Z}/M\mathbb{Z}$ 中都存在一个原象 $x$。这恰恰是数论表述中的“解的存在性”。
- **[单射性](@entry_id:147722) (Injectivity)** 意味着不同的元素 $x$ 和 $y$ 会被映射到不同的余数组。这等价于，如果 $\phi(x) = \phi(y)$，则必有 $x=y$（在 $\mathbb{Z}/M\mathbb{Z}$ 环中）。这保证了解的“模 $M$ 唯一性”。

我们可以通过考察 $\phi$ 的核 (kernel) 来证明其[单射性](@entry_id:147722)。核被定义为所有被映射到目标环零元的元素集合。在我们的情境中，$\ker(\phi)$ 包含所有满足 $x \equiv 0 \pmod{m_i}$ （对所有 $i$）的 $x \in \mathbb{Z}/M\mathbb{Z}$。由于 $m_i$ [两两互质](@entry_id:154147)，这要求 $x$ 必须是它们的最小公倍数 $\operatorname{lcm}(m_1, \dots, m_k) = \prod m_i = M$ 的倍数。在 $\mathbb{Z}/M\mathbb{Z}$ 中，唯一的 $M$ 的倍数是 $0$。因此，$\ker(\phi) = \{0\}$，这证明了 $\phi$ 是[单射](@entry_id:183792)的。由于源环和目标环都是有限环且基数（元素个数）均为 $M$，一个单射的同态必然是满射，从而构成同构。[@problem_id:3081009]

如果模 $m_i$ 不满足[两两互质](@entry_id:154147)的条件，这个同构关系就不再成立。映射 $\phi$ 将既不是单射也不是满射。[@problem_id:3081052]

### 重构解的构造性算法

中国剩余定理不仅保证了解的存在性和唯一性，其[构造性证明](@entry_id:157587)本身也提供了求解的算法。在计算中，从一组余数 $(a_1, \dots, a_k)$ 重构出整数 $x$ 是核心任务。我们介绍两种主流的算法。

#### 显式求和公式（[拉格朗日插值](@entry_id:167052)法形式）

这种方法背后的思想是构建一组“基底”，其中每个基底元素在一个模下为 $1$，在其他所有模下为 $0$。

我们定义一组特殊的元素 $e_1, e_2, \dots, e_k \in \mathbb{Z}/M\mathbb{Z}$，它们被称为**正交[幂等元](@entry_id:153117) (orthogonal idempotents)**。每个 $e_i$ 满足如下[同余](@entry_id:143700)系统：
$$
e_i \equiv 1 \pmod{m_i}, \qquad e_i \equiv 0 \pmod{m_j} \quad \text{for all } j \neq i
$$
根据中国剩余定理，对于每个 $i$，这样的 $e_i$ 在模 $M$ 下是唯一存在的。在[环同构](@entry_id:147982) $\phi$ 的视角下，每个 $e_i$ 正好对应于目标积环 $\prod \mathbb{Z}/m_j\mathbb{Z}$ 中的[标准基向量](@entry_id:152417) $(0, \dots, 1, \dots, 0)$（第 $i$ 个分量为 $1$）。[@problem_id:3081047]

这些[幂等元](@entry_id:153117)具有优美的代数性质：
1.  **[幂等性](@entry_id:190768)**: $e_i^2 \equiv e_i \pmod M$
2.  **正交性**: $e_i e_j \equiv 0 \pmod M$ (对于 $i \neq j$)
3.  **完备性**: $\sum_{i=1}^k e_i \equiv 1 \pmod M$

这些性质都可以通过 $\phi$ 同构来轻松验证。例如，$\phi(e_i^2) = \phi(e_i)^2 = (0,\dots,1,\dots,0)^2 = (0,\dots,1,\dots,0) = \phi(e_i)$，由于 $\phi$ 是同构，因此 $e_i^2 \equiv e_i \pmod M$。[@problem_id:3081047]

利用这组正交[幂等元](@entry_id:153117)，[同余方程组](@entry_id:154048)的解可以被优雅地表示为：
$$
x \equiv \sum_{i=1}^k a_i e_i \pmod M
$$
要验证这个解的正确性，只需考察其在每个模 $m_j$ 下的余数。由于 $e_i \pmod{m_j}$ 当 $i=j$ 时为 $1$，当 $i \neq j$ 时为 $0$，上述和在模 $m_j$ 下简化为 $a_j \cdot 1 = a_j$，这正是我们所需要的。[@problem_id:3081047]

为了在实际中计算 $x$，我们需要 $e_i$ 的具体表达式。设 $M_i = M/m_i$。由于 $m_j$ [两两互质](@entry_id:154147)，$\gcd(M_i, m_i) = 1$。因此，$M_i$ 存在模 $m_i$ 的乘法[逆元](@entry_id:140790)，我们记为 $y_i \equiv M_i^{-1} \pmod{m_i}$。这个[逆元](@entry_id:140790)可以通过**[扩展欧几里得算法](@entry_id:153449) (Extended Euclidean Algorithm)** 求得。

此时，元素 $M_i y_i$ 满足：
- $M_i y_i \equiv 1 \pmod{m_i}$ （根据 $y_i$ 的定义）
- $M_i y_i \equiv 0 \pmod{m_j}$ （对于 $j \neq i$，因为 $m_j$ 是 $M_i$ 的因子）

这正是 $e_i$ 的定义！因此，我们得到了 $e_i$ 的构造性公式：$e_i \equiv M_i y_i \pmod M$。[@problem_id:3081047] 将其代入解的表达式，我们便获得了最终的**显式求和公式**：
$$
x \equiv \sum_{i=1}^k a_i (M/m_i) y_i \pmod M
$$
其中 $y_i \equiv (M/m_i)^{-1} \pmod{m_i}$。这是一个确定性的算法，其时间复杂度在输入规模的对数上是多项式的。[@problem_id:3081009]

**示例：** 求解[同余方程组](@entry_id:154048) [@problem_id:3081011]
$$
x \equiv 3 \pmod 7, \quad x \equiv 5 \pmod 9, \quad x \equiv 7 \pmod{10}
$$
1.  模数[两两互质](@entry_id:154147)。$M = 7 \cdot 9 \cdot 10 = 630$。
2.  计算各分量：
    - $m_1=7, a_1=3$: $M_1 = 630/7 = 90$。求 $90^{-1} \pmod 7$。$90 \equiv 6 \equiv -1 \pmod 7$。所以 $y_1 \equiv -1 \equiv 6 \pmod 7$。
    - $m_2=9, a_2=5$: $M_2 = 630/9 = 70$。求 $70^{-1} \pmod 9$。$70 \equiv 7 \pmod 9$。由[扩展欧几里得算法](@entry_id:153449)或观察得 $7 \cdot 4 = 28 \equiv 1 \pmod 9$，所以 $y_2 = 4$。
    - $m_3=10, a_3=7$: $M_3 = 630/10 = 63$。求 $63^{-1} \pmod{10}$。$63 \equiv 3 \pmod{10}$。由 $3 \cdot 7 = 21 \equiv 1 \pmod{10}$，所以 $y_3 = 7$。
3.  组合解：
    $$
    x \equiv a_1 M_1 y_1 + a_2 M_2 y_2 + a_3 M_3 y_3 \pmod{630}
    $$
    $$
    x \equiv 3 \cdot 90 \cdot 6 + 5 \cdot 70 \cdot 4 + 7 \cdot 63 \cdot 7 \pmod{630}
    $$
    $$
    x \equiv 1620 + 1400 + 3087 = 6107 \pmod{630}
    $$
4.  化简：$6107 = 9 \times 630 + 437$。因此，$x \equiv 437 \pmod{630}$。最小非负解为 $437$。

#### 伽纳算法：混合[基数](@entry_id:754020)表示

另一种重要的重构算法是**伽纳算法 (Garner's Algorithm)**，它基于数的**混合基数表示 (Mixed Radix Representation)**。任何一个在 $[0, M-1]$ 范围内的整数 $x$ 都可以被唯一地表示为：
$$
x = c_1 + c_2 m_1 + c_3 m_1 m_2 + \dots + c_k m_1 m_2 \cdots m_{k-1}
$$
其中系数 $c_i$（称为混合基数数字）满足 $0 \le c_i  m_i$。[@problem_id:3081018] 伽纳算法的目标就是从已知的余数 $a_i$ 计算出这些系数 $c_i$。

系数可以被归纳地计算：
1.  **计算 $c_1$**:
    对方程两边模 $m_1$：$x \equiv c_1 \pmod{m_1}$。结合 $x \equiv a_1 \pmod{m_1}$，我们得到 $c_1 \equiv a_1 \pmod{m_1}$。由于 $0 \le c_1  m_1$，$c_1$ 被唯一确定为 $a_1 \pmod{m_1}$ 的最小非负余数。

2.  **计算 $c_2$**:
    对方程两边模 $m_2$：$x \equiv c_1 + c_2 m_1 \pmod{m_2}$。结合 $x \equiv a_2 \pmod{m_2}$，我们有 $a_2 \equiv c_1 + c_2 m_1 \pmod{m_2}$。
    解出 $c_2$：$c_2 m_1 \equiv a_2 - c_1 \pmod{m_2}$。
    由于 $\gcd(m_1, m_2) = 1$，$m_1$ 存在模 $m_2$ 的[逆元](@entry_id:140790)。因此 $c_2 \equiv (a_2 - c_1) m_1^{-1} \pmod{m_2}$。

3.  **计算 $c_j$ (一般步骤)**:
    归纳地，假设我们已经求得 $c_1, \dots, c_{j-1}$。考虑 $x$ 模 $m_j$：
    $$
    x \equiv c_1 + c_2 m_1 + \dots + c_{j-1} (m_1 \cdots m_{j-2}) + c_j (m_1 \cdots m_{j-1}) \pmod{m_j}
    $$
    令 $P_{j-1} = m_1 \cdots m_{j-1}$。我们得到：
    $$
    a_j \equiv \left( \sum_{i=1}^{j-1} c_i \prod_{t=1}^{i-1} m_t \right) + c_j P_{j-1} \pmod{m_j}
    $$
    解出 $c_j$：
    $$
    c_j \equiv \left( a_j - \sum_{i=1}^{j-1} c_i \prod_{t=1}^{i-1} m_t \right) \cdot (P_{j-1})^{-1} \pmod{m_j}
    $$
    由于所有模[两两互质](@entry_id:154147)，$\gcd(P_{j-1}, m_j) = 1$，[逆元](@entry_id:140790)总是存在。[@problem_id:3081018]

**示例：** 求解 $x \equiv 2 \pmod 3, x \equiv 1 \pmod 4, x \equiv 3 \pmod 5$。[@problem_id:3081018]
这里 $m_1=3, m_2=4, m_3=5$。$x = c_1 + 3c_2 + 12c_3$。
- $c_1 \equiv 2 \pmod 3 \implies c_1=2$。
- $c_2 \equiv (a_2 - c_1) \cdot m_1^{-1} \pmod{m_2} \equiv (1-2) \cdot 3^{-1} \pmod 4$。
  $3^{-1} \equiv 3 \pmod 4$。所以 $c_2 \equiv (-1) \cdot 3 \equiv 1 \pmod 4 \implies c_2=1$。
- $c_3 \equiv (a_3 - (c_1 + c_2 m_1)) \cdot (m_1 m_2)^{-1} \pmod{m_3} \equiv (3 - (2 + 1 \cdot 3)) \cdot 12^{-1} \pmod 5$。
  $12 \equiv 2 \pmod 5$, $12^{-1} \equiv 2^{-1} \equiv 3 \pmod 5$。
  $c_3 \equiv (3 - 5) \cdot 3 \equiv (-2) \cdot 3 \equiv -6 \equiv 4 \pmod 5 \implies c_3=4$。

混合[基数](@entry_id:754020)数字为 $(c_1, c_2, c_3) = (2, 1, 4)$。
重构 $x = 2 + 1 \cdot 3 + 4 \cdot (3 \cdot 4) = 2 + 3 + 48 = 53$。

### 计算考量

在实际应用中，选择哪种算法取决于具体的性能要求，特别是对中间值大小的敏感度。

#### 复杂度与性能比较

假设我们有 $k$ 个模数，每个模数的比特长度最多为 $b$。总模数 $M$ 的比特长度将是 $\Theta(kb)$。

- **显式求和公式**: 这个方法在开始时就需要计算 $M$ 和 $k$ 个[辅因子](@entry_id:137503) $M_i = M/m_i$。这些都是大数，比特长度为 $\Theta(kb)$。之后的求和 $\sum a_i M_i y_i$ 也是在大数上进行的。这意味着算法从一开始就需要处理 $\Theta(kb)$ 比特的整数。[@problem_id:3081015]

- **伽纳算法**: 此算法分为两阶段。第一阶段是计算混合[基数](@entry_id:754020)系数 $c_i$。如上述推导所示，每个 $c_j$ 的计算都可以在模 $m_j$ 的环中完成。这意味着所有中间计算（求和、求逆）都只涉及比特长度为 $O(b)$ 的小整数。第二阶段是根据 $x = c_1 + m_1(c_2 + m_2(\dots))$ 的形式（通常使用霍纳法则）重构 $x$。在这个阶段，数值的大小会逐步增长，但只有在最后一步才会达到 $\Theta(kb)$ 的完整比特长度。[@problem_id:3081015]

这种**[渐进式增长](@entry_id:637580) (progressive growth)** 的特性是伽纳算法相对于显式求和公式的主要计算优势，尤其是在多精度算术环境中，[大数运算](@entry_id:635364)的成本非常高。

从[位复杂度](@entry_id:634832)来看，若使用经典的“教科书”算法，一次[模逆元](@entry_id:149786)运算（使用[扩展欧几里得算法](@entry_id:153449)）和一次模乘法（对 $b$ 比特的数）的成本均为 $\Theta(b^2)$。在显式求和公式的核心计算中，我们需要进行 $k$ 次[模逆元](@entry_id:149786)运算，这些运算都是在各自的模 $m_i$ 下进行的。因此，这些核心步骤的总[位复杂度](@entry_id:634832)为 $\Theta(\sum_{i=1}^k b_i^2)$。[@problem_id:3081039] 伽纳算法通过朴素求和方式计算系数的复杂度为 $\Theta(k^2)$ 次模运算，但由于这些运算都是在小模数上进行，因此在处理大数时通常更受欢迎。[@problem_id:3081018]

### [中国剩余定理](@entry_id:144030)的推广

标准CRT要求模数[两两互质](@entry_id:154147)。当这个条件不满足时，我们需要一个更广义的理论。

#### 可解性条件

考虑[同余方程组](@entry_id:154048) $x \equiv a_i \pmod{m_i}$，其中 $m_i$ 不一定[两两互质](@entry_id:154147)。

一个解 $x$ 若存在，它必须同时满足任意两个[同余](@entry_id:143700)式，比如 $x \equiv a_i \pmod{m_i}$ 和 $x \equiv a_j \pmod{m_j}$。这意味着 $x$ 在模 $\gcd(m_i, m_j)$ 下的余数必须是明确的。从第一个[同余](@entry_id:143700)式，我们有 $x \equiv a_i \pmod{\gcd(m_i, m_j)}$；从第二个，我们有 $x \equiv a_j \pmod{\gcd(m_i, m_j)}$。为了使这两者不矛盾，必须有：
$$
a_i \equiv a_j \pmod{\gcd(m_i, m_j)}
$$
这个**[一致性条件](@entry_id:637057)**必须对所有的 $i, j$ 对都成立。事实证明，这不仅是必要条件，也是充分条件。

**广义中国剩余定理**: [同余方程组](@entry_id:154048) $x \equiv a_i \pmod{m_i}$ ($i=1, \dots, k$) 有解，当且仅当对于所有的 $1 \le i  j \le k$，都有一致性条件 $a_i \equiv a_j \pmod{\gcd(m_i, m_j)}$ 成立。若有解，则解在模 $L = \operatorname{lcm}(m_1, m_2, \dots, m_k)$ 的意义下是唯一的。[@problem_id:3081030]

#### 广义情况的算法

**方法一：[素数幂](@entry_id:636094)分解**

如果所有模数 $m_i$ 的素因子分解是已知的，我们可以将问题转化回标准CRT。
1.  **分解**: 将每个[同余](@entry_id:143700)式 $x \equiv a_i \pmod{m_i}$ 分解为一组关于 $m_i$ 的[素数幂](@entry_id:636094)因子的[同余](@entry_id:143700)式。例如， $x \equiv 10 \pmod{12}$ 等价于 $x \equiv 10 \pmod 4$ 和 $x \equiv 10 \pmod 3$。
2.  **整合**: 对每个素数 $p$，收集所有关于 $p$ 的幂次的[同余](@entry_id:143700)式，例如 $x \equiv b_j \pmod{p^{e_j}}$。
3.  **化简**: 检查这组关于同一素数的同余式是否一致。例如，若有 $x \equiv b_1 \pmod{p^{e_1}}$ 和 $x \equiv b_2 \pmod{p^{e_2}}$ 且 $e_1 \le e_2$，必须满足 $b_2 \equiv b_1 \pmod{p^{e_1}}$。若一致，则这组[同余](@entry_id:143700)式等价于其中幂次最高的那个，即 $x \equiv b_2 \pmod{p^{e_2}}$。[@problem_id:3080991]
4.  **重组**: 经过化简，我们为每个素[数基](@entry_id:634389)底 $p$ 都得到了一个唯一的同余式。这个新的[同余方程组](@entry_id:154048)的模数（均为素数幂）是[两两互质](@entry_id:154147)的，因此可以使用标准的CRT算法求解。

**示例:** 求解 $x \equiv 10 \pmod{12}$ 和 $x \equiv 4 \pmod{18}$ [@problem_id:3081030]。
- $\gcd(12, 18) = 6$。一致性检验：$10 \equiv 4 \pmod 6$ 成立，因为 $10-4=6$。系统有解。
- 分解：
  - $x \equiv 10 \pmod{12} \implies x \equiv 2 \pmod 4, x \equiv 1 \pmod 3$
  - $x \equiv 4 \pmod{18} \implies x \equiv 4 \pmod 2, x \equiv 4 \pmod 9$
- 整合与化简：
  - 对素数2: $x \equiv 2 \pmod 4$ 和 $x \equiv 4 \pmod 2 \equiv 0 \pmod 2$。$2 \equiv 0 \pmod 2$ 成立，取幂次高的，得 $x \equiv 2 \pmod 4$。
  - 对素数3: $x \equiv 1 \pmod 3$ 和 $x \equiv 4 \pmod 9$。$4 \equiv 1 \pmod 3$ 成立，取幂次高的，得 $x \equiv 4 \pmod 9$。
- 新系统: $x \equiv 2 \pmod 4$ 和 $x \equiv 4 \pmod 9$。模数4和9互质，可应用标准CRT求解。

**方法二：迭代合并**

此方法不需要[因子分解](@entry_id:150389)，它通过迭代地将两个同余式合并为一个来工作。
**合并步骤**: 合并 $x \equiv a_1 \pmod{m_1}$ 和 $x \equiv a_2 \pmod{m_2}$。
1.  计算 $g = \gcd(m_1, m_2)$。
2.  检查一致性：如果 $a_1 \not\equiv a_2 \pmod g$，则报告无解。
3.  如果有解，从第一个[同余](@entry_id:143700)式我们知道 $x = a_1 + k m_1$。代入第二个[同余](@entry_id:143700)式：$a_1 + k m_1 \equiv a_2 \pmod{m_2}$，即 $k m_1 \equiv a_2 - a_1 \pmod{m_2}$。
4.  这是一个关于 $k$ 的[线性同余](@entry_id:150485)方程。根据[线性同余](@entry_id:150485)理论，解存在且可求。一个解 $t$ 满足 $t \equiv \frac{a_2-a_1}{g} \cdot (\frac{m_1}{g})^{-1} \pmod{\frac{m_2}{g}}$。
5.  将 $k$ 的一个[特解](@entry_id:149080) $t$ 代回，得到 $x = a_1 + t m_1$。此解在模 $\operatorname{lcm}(m_1, m_2)$ 下唯一。
6.  最终，两个[同余](@entry_id:143700)式被合并为一个新的同余式：$x \equiv a_1 + t m_1 \pmod{\operatorname{lcm}(m_1, m_2)}$。[@problem_id:3081041]

重复此过程 $k-1$ 次，即可将整个系统合并为单个同余式。
例如，对于前面 $x \equiv 10 \pmod{12}, x \equiv 4 \pmod{18}$ 的例子，合并后得到 $x \equiv 22 \pmod{36}$。再将此结果与 $x \equiv 2 \pmod{20}$ 合并，最终得到 $x \equiv 22 \pmod{180}$。[@problem_id:3081030]

本章系统地阐述了中国剩余定理的数学原理、核心算法、计算特性及其推广。这些工具不仅在纯数学中占有重要地位，也在密码学、计算机代数和[并行计算](@entry_id:139241)等领域扮演着不可或缺的角色。