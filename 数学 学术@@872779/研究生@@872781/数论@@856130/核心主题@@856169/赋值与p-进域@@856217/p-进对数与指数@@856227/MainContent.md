## 引言
p-adic对数函数与[指数函数](@entry_id:161417)是p-adic分析的核心工具，它们在数论中的地位堪比其在[实分析](@entry_id:137229)与复分析中的对应物。尽管它们的[幂级数](@entry_id:146836)定义在形式上完全相同，但在非阿基米德的p-adic世界中，它们的行为、收敛性质以及所揭示的[代数结构](@entry_id:137052)却截然不同。本文旨在填补从形式定义到深刻理解其内在机制与强大应用之间的鸿沟，系统性地阐述这些函数为何是现代数论研究中不可或缺的一部分。

在接下来的内容中，读者将踏上一段从基础到前沿的探索之旅。在“原理与机制”一章，我们将深入剖析这两个函数的级数定义，精确推导其[收敛域](@entry_id:269722)，并揭示它们在p-adic加法群与乘法群之间建立深刻同构关系的核心作用。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将展示这些理论如何在更广阔的舞台上发挥作用，从赋予[p-adic单位](@entry_id:188533)群新的[代数结构](@entry_id:137052)，到在p-adic李群理论中扮演关键角色，再到解决经典的丢番图方程。最后，“动手实践”部分将提供具体的计算问题，帮助读者将理论知识转化为实践能力。让我们首先从这些函数最基本的原理与机制开始。

## 原理与机制

在上一章引言的基础上，本章将深入探讨 $p$-adic [指数函数](@entry_id:161417)和对数函数的核心数学原理与机制。我们将从它们的级数定义出发，精确推导其[收敛域](@entry_id:269722)，并揭示它们在 $p$-adic [加法群](@entry_id:151801)与乘法群之间建立深刻同构关系的核心作用。此外，我们还将探讨这些函数的关键性质、应用，并将其与它们在实数和[复数域](@entry_id:153768)中的对应物进行比较，以突显 $p$-adic 分析的独特性。

### $p$-adic 指数和对数函数的级数定义

在形式上，$p$-adic [指数函数](@entry_id:161417) $\exp_p(x)$ 和 $p$-adic 对数函数 $\log_p(1+x)$ 由与它们在实数和复数分析中完全相同的泰勒级数定义：

$$
\exp_p(x) = \sum_{n=0}^{\infty} \frac{x^n}{n!} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \dots
$$

$$
\log_p(1+x) = \sum_{n=1}^{\infty} \frac{(-1)^{n+1}}{n} x^n = x - \frac{x^2}{2} + \frac{x^3}{3} - \dots
$$

尽管形式上相同，但这些函数在 $p$-adic 域 $\mathbb{Q}_p$ 中的行为与在 $\mathbb{R}$ 或 $\mathbb{C}$ 中截然不同。其性质，尤其是收敛性，完全由 $p$-adic 范数 $| \cdot |_p$ 的非阿基米德特性决定。在[非阿基米德域](@entry_id:161951)中，一个无穷级数 $\sum c_n$ 收敛的充分必要条件是其通项趋于零，即当 $n \to \infty$ 时， $|c_n|_p \to 0$。这个看似简单却极为强大的准则，将引导我们揭示这两个函数深刻的内在结构。

### 收敛域的分析

确定一个[幂级数](@entry_id:146836) $\sum a_n x^n$ 的收敛域，就是要找到所有使得 $|a_n x^n|_p = |a_n|_p |x|_p^n \to 0$ 的 $x \in \mathbb{Q}_p$。这等价于 $v_p(a_n x^n) = v_p(a_n) + n v_p(x) \to \infty$。

#### $p$-adic 对数函数

对于对数级数 $\log_p(1+x) = \sum_{n=1}^{\infty} a_n x^n$，其系数为 $a_n = \frac{(-1)^{n+1}}{n}$。我们来分析其 $p$-adic 范数：
$$
|a_n|_p = \left| \frac{(-1)^{n+1}}{n} \right|_p = \frac{|-1|_p^{n+1}}{|n|_p} = \frac{1}{|n|_p} = p^{v_p(n)}
$$
收敛的条件是 $|a_n|_p |x|_p^n = p^{v_p(n)} |x|_p^n \to 0$。

如果 $|x|_p  1$，那么 $v_p(x)  0$。级数通项的 $p$-adic 估值 $v_p(a_n x^n) = n v_p(x) - v_p(n)$。由于 $p^{v_p(n)} \le n$，我们有 $v_p(n) \le \log_p(n)$。因此，
$$
\frac{v_p(a_n x^n)}{n} = v_p(x) - \frac{v_p(n)}{n}
$$
当 $n \to \infty$ 时，$\frac{\log_p(n)}{n} \to 0$，根据[夹逼定理](@entry_id:147218)，$\frac{v_p(n)}{n} \to 0$。因此 $v_p(a_n x^n)$ 的增长趋势由 $n v_p(x)$ 主导，线性趋向于无穷大。故级数收敛。

如果 $|x|_p \ge 1$，则 $v_p(x) \le 0$。通项的估值 $n v_p(x) - v_p(n) \le -v_p(n)$，它不趋于无穷大。例如，若 $|x|_p=1$，取 $n=p^k$，则通项的范数 $|a_{p^k} x^{p^k}|_p = |1/p^k|_p |x|_p^{p^k} = p^k \cdot 1^{p^k} = p^k$，它不趋于零。

因此，$p$-adic 对数级数 $\log_p(1+x)$ 的收敛域是 $|x|_p  1$。这个集合在 $\mathbb{Z}_p$ 中就是 $p\mathbb{Z}_p$。这意味着 $\log_p(z)$ 函数是自然地定义在[乘法群](@entry_id:155975)的[子群](@entry_id:146164) $1+p\mathbb{Z}_p$ 上的。其收敛半径为 $1$。[@problem_id:3020581] [@problem_id:3028658]

#### $p$-adic [指数函数](@entry_id:161417)

对于指数级数 $\exp_p(x) = \sum_{n=0}^{\infty} b_n x^n$，其系数为 $b_n = \frac{1}{n!}$。其 $p$-adic 范数为：
$$
|b_n|_p = \left| \frac{1}{n!} \right|_p = \frac{1}{|n!|_p} = p^{v_p(n!)}
$$
收敛的条件是 $|b_n|_p |x|_p^n = p^{v_p(n!)} |x|_p^n \to 0$。这等价于 $v_p(b_n x^n) = n v_p(x) - v_p(n!) \to \infty$。

为了分析这个条件，我们需要 $v_p(n!)$ 的增长行为。根据[勒让德公式](@entry_id:266714) (Legendre's formula)：
$$
v_p(n!) = \sum_{k=1}^{\infty} \left\lfloor \frac{n}{p^k} \right\rfloor
$$
这个公式的一个重要推论是 $v_p(n!) = \frac{n - S_p(n)}{p-1}$，其中 $S_p(n)$ 是 $n$ 的 $p$ 进制表示的各位数字之和。由于 $1 \le S_p(n) \le (p-1)(\lfloor\log_p n\rfloor + 1)$， $S_p(n)$ 的增长速度远慢于 $n$。因此，我们有：
$$
\lim_{n \to \infty} \frac{v_p(n!)}{n} = \lim_{n \to \infty} \frac{1}{n} \left( \frac{n - S_p(n)}{p-1} \right) = \frac{1}{p-1}
$$
[收敛条件](@entry_id:166121) $n v_p(x) - v_p(n!) = n \left( v_p(x) - \frac{v_p(n!)}{n} \right) \to \infty$ 成立，当且仅当括号内的项最终为正，即 $v_p(x)  \lim_{n \to \infty} \frac{v_p(n!)}{n}$。所以，收敛的充要条件是 $v_p(x)  \frac{1}{p-1}$。[@problem_id:3020581]

这等价于 $|x|_p  p^{-1/(p-1)}$。这就是 $p$-adic 指数[函数的收敛](@entry_id:152305)半径。[@problem_id:3028651]

#### 比较与 $p=2$ 的特殊性

我们看到，$\log_p$ 和 $\exp_p$ 的收敛半径不同，这与它们在复数域中截然不同（$\log(1+z)$ 半径为 $1$，$\exp(z)$ 半径为无穷大）。$p$-adic 域的差异根源于系数分母的 $p$-adic 估值增长率：$v_p(n)$ 呈对数增长（次线性），而 $v_p(n!)$ 呈[线性增长](@entry_id:157553)。[@problem_id:3028658]

指数[函数的[收](@entry_id:152305)敛条件](@entry_id:166121) $v_p(x)  \frac{1}{p-1}$ 揭示了一个关于素数 $p$ 的关键[二分法](@entry_id:140816)：
*   **当 $p \ge 3$ 时**，$p-1 \ge 2$，所以 $0  \frac{1}{p-1} \le \frac{1}{2}$。由于 $v_p(x)$ 是整数，不等式 $v_p(x)  \frac{1}{p-1}$ 等价于 $v_p(x) \ge 1$。这意味着 $\exp_p(x)$ 的[收敛域](@entry_id:269722)是 $p\mathbb{Z}_p$。
*   **当 $p = 2$ 时**，$p-1=1$，不等式变为 $v_2(x)  1$，这等价于 $v_2(x) \ge 2$。这意味着 $\exp_2(x)$ 的收敛域是 $4\mathbb{Z}_2$。

这个差异是 $p$-adic 分析中许多现象的根源，其中 $p=2$ 的行为常常是例外的。[@problem_id:1779452]

### 加法群与[乘法群](@entry_id:155975)之间的同构

$p$-adic [指数和](@entry_id:199860)对数函数最重要的性质是它们在特定的 $p$-adic 群之间建立了桥梁。具体来说，它们构成了加法群 $(p^{k_p}\mathbb{Z}_p, +)$ 和[乘法群](@entry_id:155975) $(1+p^{k_p}\mathbb{Z}_p, \times)$ 之间的[群同构](@entry_id:147371)，其中 $k_p$ 是一个取决于 $p$ 的整数。

#### 情形 $p \ge 3$

当 $p \ge 3$ 时，$k_p=1$。$\exp_p$ 和 $\log_p$ 在[加法群](@entry_id:151801) $(p\mathbb{Z}_p, +)$ 和[乘法群](@entry_id:155975) $(1+p\mathbb{Z}_p, \times)$ 之间建立了一个保持拓扑结构的同构。

我们可以验证这两个映射确实在这些群之间进行：
1.  **$\exp_p: p\mathbb{Z}_p \to 1+p\mathbb{Z}_p$**:
    如前所述，对于 $x \in p\mathbb{Z}_p$ (即 $v_p(x) \ge 1$)，$\exp_p(x)$ [级数收敛](@entry_id:142638)。我们需要证明 $\exp_p(x) \in 1+p\mathbb{Z}_p$，即 $v_p(\exp_p(x)-1) \ge 1$。
    $$
    \exp_p(x)-1 = x + \frac{x^2}{2!} + \frac{x^3}{3!} + \dots
    $$
    通项 $T_n = \frac{x^n}{n!}$ 的估值为 $v_p(T_n) = n v_p(x) - v_p(n!) \ge n - v_p(n!)$。对于 $n=1$, $v_p(T_1) = v_p(x) \ge 1$。对于 $n \ge 2$ 和 $p \ge 3$，可以证明 $v_p(T_n)$ 严格大于 $v_p(T_1)$。根据非阿基米德范数的[强三角不等式](@entry_id:637536)，$v_p(\exp_p(x)-1) = \min_{n \ge 1} \{v_p(T_n)\} = v_p(x) \ge 1$。因此 $\exp_p(x) \in 1+p\mathbb{Z}_p$。

2.  **$\log_p: 1+p\mathbb{Z}_p \to p\mathbb{Z}_p$**:
    对于 $z \in 1+p\mathbb{Z}_p$，我们可以写成 $z=1+x$，其中 $x \in p\mathbb{Z}_p$ (即 $v_p(x) \ge 1$)。我们已经知道 $\log_p(1+x)$ 在此收敛。我们需要证明 $\log_p(1+x) \in p\mathbb{Z}_p$，即 $v_p(\log_p(1+x)) \ge 1$。
    $$
    \log_p(1+x) = x - \frac{x^2}{2} + \frac{x^3}{3} - \dots
    $$
    通项 $U_n = \frac{x^n}{n}$ 的估值为 $v_p(U_n) = n v_p(x) - v_p(n) \ge n - v_p(n)$。可以验证对于所有 $n \ge 1$，$n-v_p(n) \ge 1$。因此所有项的估值都至少为 $1$，从而和的估值也至少为 $1$。

由于 $\exp_p$ 和 $\log_p$ 的形式级数互为逆，并且它们在各自的定义域内满足函数方程 $\exp_p(a+b) = \exp_p(a)\exp_p(b)$ 和 $\log_p(uv) = \log_p(u)+\log_p(v)$，所以它们是互为逆的[群同构](@entry_id:147371)。[@problem_id:3028650]

为了具体感受同构的威力，让我们在一个实例中验证其同态性质。设 $p=5$, $x=10, y=5$。我们来验证 $\exp_5(10+5) \equiv \exp_5(10)\exp_5(5) \pmod{5^3}$。由于 $v_5(z^n/n!) \ge 3$ 对所有 $n \ge 3$ 成立（当 $v_5(z)=1$ 时），我们可以将级数截断至 $n=2$ 项：
*   $\exp_5(15) \equiv 1 + 15 + \frac{15^2}{2} = 16 + \frac{225}{2} \equiv 16 + 100 \cdot 63 \equiv 16 + 50 = 66 \pmod{125}$。
*   $\exp_5(10) \equiv 1 + 10 + \frac{10^2}{2} = 11 + 50 = 61 \pmod{125}$。
*   $\exp_5(5) \equiv 1 + 5 + \frac{5^2}{2} = 6 + \frac{25}{2} \equiv 6 + 25 \cdot 63 = 6+1575 \equiv 6+75 = 81 \pmod{125}$。
*   $\exp_5(10)\exp_5(5) \equiv 61 \cdot 81 = 4941 = 39 \cdot 125 + 66 \equiv 66 \pmod{125}$。
计算结果完全吻合，直观地展示了同构关系。[@problem_id:3028662]

#### 例外情形 $p=2$

当 $p=2$ 时，情况变得更为复杂，$(2\mathbb{Z}_2, +)$ 和 $(1+2\mathbb{Z}_2, \times)$ 之间不存在由 $\exp_2$ 和 $\log_2$ 诱导的同构。这背后有多重障碍：

1.  **收敛性障碍**：如前所述，$\exp_2(x)$ 的[收敛域](@entry_id:269722)是 $4\mathbb{Z}_2$，它严格小于 $2\mathbb{Z}_2$。因此，$\exp_2$ 甚至不能在整个 $2\mathbb{Z}_2$ 上定义，无法成为从 $2\mathbb{Z}_2$ 出发的同构的逆。[@problem_id:3028405] [@problem_id:1779452]

2.  **[代数结构](@entry_id:137052)障碍 ([挠元](@entry_id:148301))**：乘法群 $1+2\mathbb{Z}_2 = \mathbb{Z}_2^\times$ 包含元素 $-1$。它是一个 2-[挠元](@entry_id:148301)，因为 $(-1)^2 = 1$。然而，加法群 $2\mathbb{Z}_2$ 是[无挠的](@entry_id:161664)（任何非零元素乘以任何非零整数都不等于零）。[群同构](@entry_id:147371)必须保持[挠元](@entry_id:148301)结构，因此这两个群不可能是同构的。$\log_2$ 在此的非[单射性](@entry_id:147722)也体现了这一点：$\log_2(-1)=0$（因为 $2\log_2(-1) = \log_2((-1)^2) = \log_2(1) = 0$），所以 $\log_2$ 的核至少包含 $\{\pm 1\}$，故不是单射。[@problem_id:3028405]

3.  **非满射性**：可以证明，对于任何 $u \in 1+2\mathbb{Z}_2$，其对数值 $\log_2(u)$ 落在 $4\mathbb{Z}_2$ 中。由于 $4\mathbb{Z}_2$ 是 $2\mathbb{Z}_2$ 的一个[真子群](@entry_id:141915)（例如 $2 \in 2\mathbb{Z}_2$ 但 $2 \notin 4\mathbb{Z}_2$），所以 $\log_2$ 的像无法覆盖整个 $2\mathbb{Z}_2$，故不是满射。[@problem_id:3028405]

正确的同构关系存在于更小的[子群](@entry_id:146164)之间。$2$-adic 单位群有一个结构分解 $\mathbb{Z}_2^\times \cong \{\pm 1\} \times (1+4\mathbb{Z}_2)$。$\log_2$ 函数实际上是作用在 $1+4\mathbb{Z}_2$ 这个因子上的，并将 $\{\pm 1\}$ 映为 $0$。正确的同构是：
$$
\exp_2: (4\mathbb{Z}_2, +) \xrightarrow{\sim} (1+4\mathbb{Z}_2, \times)
$$
及其逆 $\log_2$。[@problem_id:3028405] [@problem_id:3028650]

### 基本性质与应用

#### 求解方程

$p$-adic [指数和](@entry_id:199860)对数函数之间的同构关系为求解形如 $\exp_p(y)=x$ 的方程提供了直接的方法。给定一个 $x$ 位于相应的乘法群中（例如，当 $p \ge 3$ 时，$x \in 1+p\mathbb{Z}_p$），方程在对应的[加法群](@entry_id:151801)中（$p\mathbb{Z}_p$）存在唯一解。这个解就是 $y = \log_p(x)$。
$$
y = \log_p(x) = \log_p(1 + (x-1)) = \sum_{n=1}^{\infty} \frac{(-1)^{n+1}}{n} (x-1)^n
$$
由于 $x \in 1+p\mathbb{Z}_p$，我们有 $x-1 \in p\mathbb{Z}_p$，这确保了上述对数级数是收敛的。因此，解的存在性和唯一性在这些特定域内得到保证。[@problem_id:3028650]

#### [等距同构](@entry_id:273188)性质

在足够小的 $p$-adic 圆盘上，[指数映射](@entry_id:137184)表现出一种**[等距同构](@entry_id:273188) (isometry)** 的性质，即 $|\exp_p(x) - 1|_p = |x|_p$。这等价于 $v_p(\exp_p(x)-1) = v_p(x)$。

这个性质的根源在于，当 $v_p(x)$ 足够大时，$\exp_p(x)-1$ 的级数展开式 $x + \frac{x^2}{2!} + \dots$ 中，首项 $x$ 的估值严格小于所有后续项的估值。根据[强三角不等式](@entry_id:637536)，和的估值就等于各项估值的最小值，即 $v_p(x)$。

让我们以 $x=p^2 a$ ($p \ge 3, a \in \mathbb{Z}_p$) 为例来说明。此时 $v_p(x) = 2+v_p(a) \ge 2$。
$$
\exp_p(p^2 a) - 1 = p^2 a + \frac{(p^2 a)^2}{2!} + \frac{(p^2 a)^3}{3!} + \dots
$$
我们来分析各项的估值：
*   $v_p(p^2 a) = 2+v_p(a)$。
*   $v_p\left(\frac{(p^2 a)^2}{2!}\right) = v_p(p^4 a^2/2) = 4+2v_p(a)-v_p(2) = 4+2v_p(a)$ (因为 $p \ge 3$, $v_p(2)=0$）。
*   对于 $n \ge 2$，可以证明 $v_p\left(\frac{(p^2 a)^n}{n!}\right) > v_p(p^2 a)$。

因此，所有 $n \ge 2$ 的项的估值都严格大于首项 $p^2 a$ 的估值。这意味着，模去估值至少为 $3$ 的项，我们有 $\exp_p(p^2 a) \equiv 1+p^2 a$。[@problem_id:3028666]
更重要的是，这揭示了 $v_p(\exp_p(p^2 a) - 1) = v_p(p^2 a)$，从而 $| \exp_p(p^2 a) - 1 |_p = |p^2 a|_p$。这个计算清晰地展示了在 $v_p(x)$ 较大的小圆盘上，指数映射如何充当一个[等距映射](@entry_id:150881)。

#### $p$-adic [微分方程](@entry_id:264184)

在 $p$-adic 域中，解析[函数的[微](@entry_id:274991)分](@entry_id:158718)可以像在[实数域](@entry_id:151347)中一样逐项进行。考虑初始值问题：
$$
h'(x) = \frac{1}{1+x}, \quad h(0)=0
$$
在开[单位圆盘](@entry_id:172324) $D = \{x \in \mathbb{Q}_p : |x|_p  1\}$ 内寻找解析解。在 $D$ 上，$1/(1+x)$ 可以展开为[几何级数](@entry_id:158490) $\sum_{k=0}^\infty (-1)^k x^k$。若设解析解为 $h(x) = \sum_{n=0}^\infty a_n x^n$，则 $h(0)=0$ 意味着 $a_0=0$。逐项求导并与几何级数比较系数，我们唯一地确定了 $a_n = \frac{(-1)^{n+1}}{n}$。这正是 $\log_p(1+x)$ 的级数。因此，在解析函数的范畴内，$\log_p(1+x)$ 是该[微分方程](@entry_id:264184)的唯一解。[@problem_id:3028648]

这一结论与实数分析形成鲜明对比，也揭示了 $p$-adic 域的独特性质。在实数域中，根据均值定理，任何满足 $g'(x)=0$ 的[可微函数](@entry_id:144590)必为常数，从而保证了上述初值问题的唯一性，即使不要求函数是解析的。然而，在 $p$-adic 域中，[均值定理](@entry_id:141085)不成立。由于 $\mathbb{Q}_p$ 是[完全不连通的](@entry_id:149247)，存在非平凡的局部常值函数，它们处处可微且导数为零。例如，函数 $f(x)=1$ 如果 $x \in \mathbb{Z}_p$，$f(x)=0$ 如果 $x \notin \mathbb{Z}_p$。这个函数非恒定，但其导数处处为零。因此，在 $p$-adic 分析中，仅仅可微不足以保证[微分方程](@entry_id:264184)[解的唯一性](@entry_id:143619)，必须施加更强的“解析性”条件。[@problem_id:3028648]

### 拓扑学观点与全局扩展

#### 与[复对数](@entry_id:174857)函数的比较

$p$-adic 对数函数的性质与[复对数](@entry_id:174857)函数 $\log_{\mathbb{C}}(z)$ 的性质差异巨大，其根源在于底层空间的拓扑结构。
[复对数](@entry_id:174857)函数的多值性及其对**支割线 (branch cuts)** 的需求，源于乘法群 $\mathbb{C}^\times = \mathbb{C} \setminus \{0\}$ 的拓扑结构。$\mathbb{C}^\times$ 是一个[路径连通](@entry_id:148704)但非单连通的空间，其[基本群](@entry_id:146111) $\pi_1(\mathbb{C}^\times)$ 同构于 $\mathbb{Z}$。这意味着存在环绕原点的非平凡闭路。沿着这样的闭路对 $1/z$ 进行积分，结果为 $2\pi i \ne 0$，这构成了定义一个单值全纯对数函数的**[单值性](@entry_id:174849)障碍 ([monodromy](@entry_id:174849) obstruction)**。支割线的作用是移除一条射线，使得剩余的区域变为单连通，从而消除此障碍。

相比之下，$\mathbb{Q}_p^\times$ 的拓扑结构是[完全不连通的](@entry_id:149247)。其中不存在任何非平凡的路径或闭路。因此，基于路径积分的[单值性](@entry_id:174849)障碍根本不存在。$p$-adic 对数函数 $\log_p$ 的定义域之所以被限制在一个以 $1$ 为中心的小圆盘 $1+p\mathbb{Z}_p$ 内，完全是其[幂级数收敛](@entry_id:160068)性的分析结果，而非拓扑障碍。[@problem_id:3028663]

#### 全局扩展

尽管 $\log_p$ 的幂级数只在局部收敛，我们仍然可以将其扩展为一个定义在整个乘法群 $\mathbb{Q}_p^\times$ 上的连续[群同态](@entry_id:140603)，但这个扩展不是通过解析延拓，而是通过代数和拓扑结构。

任何一个非零的 $p$-adic 数 $x \in \mathbb{Q}_p^\times$ 都可以唯一地分解为：
$$
x = p^{v_p(x)} \cdot \omega(x) \cdot \langle x \rangle
$$
其中 $v_p(x) \in \mathbb{Z}$ 是 $x$ 的估值，$\omega(x)$ 是一个 $(p-1)$-次单位根（属于[挠元](@entry_id:148301)群 $\mu_{p-1}$），而 $\langle x \rangle$ 属于[主单位](@entry_id:188721)群 $1+p\mathbb{Z}_p$。

一个从乘法群 $(\mathbb{Q}_p^\times, \times)$ 到[加法群](@entry_id:151801) $(\mathbb{Q}_p, +)$ 的连续同态 $\mathcal{L}$ 必须满足 $\mathcal{L}(xy) = \mathcal{L}(x)+\mathcal{L}(y)$。为了保持同态性质，它必须将 $\mathbb{Q}_p^\times$ 中的所有[挠元](@entry_id:148301)（即[单位根](@entry_id:143302) $\mu_{p-1}$）映到加法群中唯一的[挠元](@entry_id:148301)—— $0$。此外，我们可以做出选择，将 $p$ 也映为 $0$。这样，我们就定义了所谓的**岩泽对数 (Iwasawa logarithm)**：
$$
\log_{p, \text{Iwa}}(x) = \log_p(\langle x \rangle)
$$
这个函数在整个 $\mathbb{Q}_p^\times$ 上有定义，是一个连续的[群同态](@entry_id:140603)，并且在 $1+p\mathbb{Z}_p$ 上与原始的[幂级数](@entry_id:146836)定义一致。这个构造过程再次凸显了 $p$-adic 分析的一个核心主题：全局对象往往是通过代数和拓扑手段构建的，而不是像复分析中那样通过路径延拓。[@problem_id:3028663]