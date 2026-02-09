## 引言
在抽象代数的宏伟版图中，分圆扩张（Cyclotomic Extensions）占据着一个核心且迷人的位置。它不仅是伽罗瓦理论最优美的教学范例之一，更是连接代数、数论与几何学等多个数学分支的关键桥梁。分圆域源于一个看似简单的问题——研究方程 $x^n=1$ 的根，但其背后却蕴藏着深刻的对称性与丰富的代数结构。本文旨在系统地揭开分圆扩张的神秘面纱，解答它是如何被构建、其结构有何特征以及为何它在解决一些数学史上最著名的问题中扮演了如此重要的角色。

为了全面掌握这一主题，我们将分三个核心章节进行探索。首先，在“原理与机制”一章中，我们将深入探讨分圆扩张的基本构造块，从单位根和分圆多项式入手，精确刻画其扩张次数和伽罗瓦群的结构。接着，在“应用与交叉学科联系”一章中，我们将展示该理论的强大威力，看它如何为费马大定理的研究提供思路，如何解决经典的尺规作图问题，并如何引出深刻的克罗内克-韦伯定理。最后，通过“动手实践”部分，你将有机会运用所学知识解决具体问题，从而巩固理解。让我们首先进入第一部分，探索构成这些非凡代数结构的基础原理与机制。

## 原理与机制

在介绍性章节之后，我们现在深入探讨分圆扩张的内部工作原理。本章将系统地阐述定义分圆域的核心概念，分析其结构，并揭示其伽罗瓦群的深刻性质。我们将从单位根的基础知识开始，逐步构建起分圆多项式、分圆域的度以及其伽罗瓦群的理论。

### 单位根与本原单位根

在复数域 $\mathbb{C}$ 中，代数方程 $x^n = 1$（其中 $n$ 为正整数）的解被称为 **$n$ 次单位根**。根据代数学基本定理，这个方程恰好有 $n$ 个复数解。利用欧拉公式，这些解可以明确地表示为：
$$
z_k = \exp\left(\frac{2\pi i k}{n}\right) = \cos\left(\frac{2\pi k}{n}\right) + i\sin\left(\frac{2\pi k}{n}\right), \quad \text{对于 } k = 0, 1, \dots, n-1
$$
这些单位根在复平面的单位圆上构成一个正 $n$ 边形的顶点。

在所有 $n$ 次单位根中，有一类特别重要，它们被称为**本原 $n$ 次单位根**。一个 $n$ 次单位根 $\zeta$ 是本原的，如果 $\zeta^n = 1$ 且对于所有满足 $0  k  n$ 的正整数 $k$，都有 $\zeta^k \neq 1$。换言之，本原 $n$ 次单位根的阶（order）恰好是 $n$。一个 $n$ 次单位根 $\zeta_k = \exp\left(\frac{2\pi i k}{n}\right)$ 是本原的，当且仅当整数 $k$ 与 $n$ 互质，即 $\gcd(k, n) = 1$。

例如，我们来确定 6 次本原单位根 [@problem_id:1785936]。我们需要找到满足 $1 \le k  6$ 且 $\gcd(k, 6) = 1$ 的所有整数 $k$。这些值是 $k=1$ 和 $k=5$。因此，存在两个 6 次本原单位根：
$$
\zeta_1 = \exp\left(\frac{2\pi i}{6}\right) = \exp\left(\frac{\pi i}{3}\right) = \cos\left(\frac{\pi}{3}\right) + i\sin\left(\frac{\pi}{3}\right) = \frac{1}{2} + i\frac{\sqrt{3}}{2}
$$
$$
\zeta_5 = \exp\left(\frac{10\pi i}{6}\right) = \exp\left(\frac{5\pi i}{3}\right) = \cos\left(\frac{5\pi}{3}\right) + i\sin\left(\frac{5\pi}{3}\right) = \frac{1}{2} - i\frac{\sqrt{3}}{2}
$$
注意，$\zeta_5 = \overline{\zeta_1} = \zeta_1^{-1}$。这个性质对于所有本原单位根都成立，即如果 $\zeta$ 是一个本原单位根，那么它的复共轭 $\overline{\zeta}$ 和逆 $\zeta^{-1}$ 也是。

另一个例子是 8 次本原单位根 [@problem_id:1785999]。满足 $1 \le k  8$ 且 $\gcd(k, 8) = 1$ 的 $k$ 值为 $1, 3, 5, 7$。因此，有四个 8 次本原单位根：
$$
\zeta_8^1 = \frac{1}{\sqrt{2}} + \frac{i}{\sqrt{2}}, \quad \zeta_8^3 = -\frac{1}{\sqrt{2}} + \frac{i}{\sqrt{2}}, \quad \zeta_8^5 = -\frac{1}{\sqrt{2}} - \frac{i}{\sqrt{2}}, \quad \zeta_8^7 = \frac{1}{\sqrt{2}} - \frac{i}{\sqrt{2}}
$$
非本原的 8 次单位根，如 $i = \exp(\frac{2\pi i}{4}) = \exp(\frac{4\pi i}{8})$，它的阶是 4 而不是 8。

通过将任意一个本原 $n$ 次单位根 $\zeta_n$ 添加到有理数域 $\mathbb{Q}$ 中，我们构造出**第 $n$ 个分圆域**，记为 $\mathbb{Q}(\zeta_n)$。这是一个包含 $\mathbb{Q}$ 和 $\zeta_n$ 的最小的域。由于所有 $n$ 次单位根都可以表示为 $\zeta_n$ 的幂，因此 $\mathbb{Q}(\zeta_n)$ 包含了所有的 $n$ 次单位根，并且是多项式 $x^n-1$ 在 $\mathbb{Q}$ 上的分裂域。

### 分圆多项式与分圆扩张的度

我们自然会问：本原 $n$ 次单位根在有理数域 $\mathbb{Q}$ 上的最小多项式是什么？答案是**第 $n$ 个分圆多项式**，记为 $\Phi_n(x)$。它定义为以所有本原 $n$ 次单位根为根的首一多项式：
$$
\Phi_n(x) = \prod_{\substack{1 \le k \le n \\ \gcd(k, n) = 1}} (x - \zeta_n^k)
$$
由于多项式 $x^n - 1$ 的根恰好是所有的 $n$ 次单位根（包括本原和非本原的），我们可以将这些根按其阶数进行分类。一个 $n$ 次单位根的阶必然是 $n$ 的某个因子 $d$。因此，我们可以将 $x^n-1$ 分解为所有分圆多项式 $\Phi_d(x)$ 的乘积，其中 $d$ 是 $n$ 的所有正因子：
$$
x^n - 1 = \prod_{d|n} \Phi_d(x)
$$
这个重要的恒等式提供了一种递归计算分圆多项式的方法。例如，要计算 $\Phi_{12}(x)$ [@problem_id:1785934]，我们知道 12 的因子是 1, 2, 3, 4, 6, 12。通过依次计算低阶的分圆多项式，例如 $\Phi_1(x) = x-1$, $\Phi_2(x) = \frac{x^2-1}{x-1} = x+1$, $\Phi_4(x) = \frac{x^4-1}{\Phi_1(x)\Phi_2(x)} = x^2+1$，我们可以通过多项式除法得到更高阶的多项式。对于 $\Phi_{12}(x)$，我们有：
$$
\Phi_{12}(x) = \frac{x^6+1}{\Phi_4(x)} = \frac{x^6+1}{x^2+1} = x^4 - x^2 + 1
$$
我们可以证明 $\Phi_n(x)$ 是一个系数在 $\mathbb{Z}$ 中的首一多项式。更关键的是一个深刻的定理：**对于任意正整数 $n$，$\Phi_n(x)$ 在 $\mathbb{Q}$ 上是不可约的。**

这意味着 $\Phi_n(x)$ 就是任意一个本原 $n$ 次单位根 $\zeta_n$ 在 $\mathbb{Q}$ 上的最小多项式。这个结论是分圆域理论的基石。其证明通常比较复杂，但对于素数 $p$ 的情况，我们可以用一个巧妙的技巧来证明 $\Phi_p(x)$ 的不可约性 [@problem_id:1785989]。考虑 $n=5$ 的情况，$\Phi_5(x) = \frac{x^5-1}{x-1} = x^4 + x^3 + x^2 + x + 1$。直接应用艾森斯坦判别法是无效的。但是，一个多项式 $f(x)$ 是不可约的当且仅当 $f(x+c)$ 是不可约的。我们考察 $\Phi_5(x+1)$:
$$
\Phi_5(x+1) = \frac{(x+1)^5 - 1}{(x+1)-1} = \frac{x^5 + 5x^4 + 10x^3 + 10x^2 + 5x}{x} = x^4 + 5x^3 + 10x^2 + 10x + 5
$$
对于这个新的多项式，我们可以应用艾森斯坦判别法，取素数 $p=5$。我们观察到：
1.  $p=5$ 整除除了首项系数 1 以外的所有系数 (5, 10, 10, 5)。
2.  $p=5$ 不整除首项系数 1。
3.  $p^2=25$ 不整除常数项 5。
所有条件均满足，因此 $\Phi_5(x+1)$ 在 $\mathbb{Q}$ 上是不可约的，从而 $\Phi_5(x)$ 也是不可约的。

既然 $\Phi_n(x)$ 是 $\zeta_n$ 的最小多项式，那么分圆扩张 $\mathbb{Q}(\zeta_n)/\mathbb{Q}$ 的次数就等于这个多项式的次数：
$$
[\mathbb{Q}(\zeta_n) : \mathbb{Q}] = \deg(\Phi_n(x))
$$
从 $\Phi_n(x)$ 的定义可知，其次数等于本原 $n$ 次单位根的个数。这个数目由**欧拉函数** $\phi(n)$ 给出，它计算小于 $n$ 且与 $n$ 互质的正整数的个数。因此，我们得到了分圆扩张次数的一个优美公式：
$$
[\mathbb{Q}(\zeta_n) : \mathbb{Q}] = \phi(n)
$$
例如，要计算扩张 $\mathbb{Q}(\zeta_{12})$ 的次数 [@problem_id:1785953]，我们只需计算 $\phi(12)$。利用欧拉函数的积性性质和公式 $\phi(p^k) = p^k - p^{k-1}$：
$$
\phi(12) = \phi(2^2 \cdot 3) = \phi(2^2) \phi(3) = (2^2 - 2^1)(3^1 - 3^0) = 2 \cdot 2 = 4
$$
因此，$[\mathbb{Q}(\zeta_{12}) : \mathbb{Q}] = 4$，这与我们之前计算出 $\deg(\Phi_{12}(x)) = 4$ 相符。

### 分圆扩张的伽罗瓦群

分圆扩张 $\mathbb{Q}(\zeta_n)/\mathbb{Q}$ 是一个伽罗瓦扩张，其伽罗瓦群记为 $\text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$。这个群的元素是 $\mathbb{Q}(\zeta_n)$ 的所有自同构 $\sigma$，这些自同构逐点固定 $\mathbb{Q}$ 中的元素。

任何一个这样的自同构 $\sigma$ 完全由它对生成元 $\zeta_n$ 的作用所决定。由于 $\sigma$ 必须保持代数关系，它必须将 $\zeta_n$ 映射到其最小多项式 $\Phi_n(x)$ 的另一个根上。这意味着 $\sigma(\zeta_n)$ 必须是另一个本原 $n$ 次单位根。因此，对于任意 $\sigma \in \text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$，存在一个唯一的整数 $k$ 满足 $1 \le k  n$ 且 $\gcd(k, n) = 1$，使得：
$$
\sigma(\zeta_n) = \zeta_n^k
$$
我们可以用 $\sigma_k$ 来表示这个自同构。这个发现揭示了一个深刻的联系。考虑两个自同构 $\sigma_j$ 和 $\sigma_k$ 的复合：
$$
(\sigma_j \circ \sigma_k)(\zeta_n) = \sigma_j(\sigma_k(\zeta_n)) = \sigma_j(\zeta_n^k) = (\sigma_j(\zeta_n))^k = (\zeta_n^j)^k = \zeta_n^{jk}
$$
这表明自同构的复合对应于下标的乘法（模 $n$）。这引导我们建立了如下的群同构：
$$
\text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q}) \cong (\mathbb{Z}/n\mathbb{Z})^\times
$$
其中 $(\mathbb{Z}/n\mathbb{Z})^\times$ 是模 $n$ 的整数环的乘法群（单位群），其元素是所有与 $n$ 互质的模 $n$ 的同余类。这个同构是分圆域理论的核心成果之一。

一个直接的推论是，由于 $(\mathbb{Z}/n\mathbb{Z})^\times$ 对任何 $n$ 都是一个**阿贝尔群**（交换群），所以任何在 $\mathbb{Q}$ 上的分圆扩张的伽罗瓦群都是阿贝尔群。这是一个意义深远的结果，它构成了克罗内克-韦伯定理的一部分，该定理指出任何 $\mathbb{Q}$ 上的阿贝尔扩张都包含在某个分圆域中。

让我们通过一个例子来理解这个同构关系 [@problem_id:1785951]。考虑 $\mathbb{Q}(\zeta_7)/\mathbb{Q}$，其伽罗瓦群同构于 $(\mathbb{Z}/7\mathbb{Z})^\times = \{1, 2, 3, 4, 5, 6\}$。这是一个 6 阶循环群。考虑自同构 $\sigma_3$，它定义为 $\sigma_3(\zeta_7) = \zeta_7^3$。$\sigma_3$ 在伽罗瓦群中的阶，等于 3 在群 $(\mathbb{Z}/7\mathbb{Z})^\times$ 中的阶。我们需要找到最小的正整数 $m$ 使得 $3^m \equiv 1 \pmod{7}$。
$$
3^1 \equiv 3 \pmod{7} \\
3^2 \equiv 2 \pmod{7} \\
3^3 \equiv 6 \pmod{7} \\
3^4 \equiv 4 \pmod{7} \\
3^5 \equiv 5 \pmod{7} \\
3^6 \equiv 1 \pmod{7}
$$
因此，$\sigma_3$ 的阶是 6。

### 伽罗瓦群的结构与子域

虽然分圆伽罗瓦群总是阿贝尔群，但它不一定是循环群。群 $(\mathbb{Z}/n\mathbb{Z})^\times$ 是循环的当且仅当 $n$ 的形式为 $2, 4, p^k$ 或 $2p^k$，其中 $p$ 是一个奇素数。对于其他形式的 $n$，该群就不是循环的。

我们可以通过考察具体的例子来发现这一点 [@problem_id:1785932] [@problem_id:1832936]。
-   对于 $n=8$，群是 $(\mathbb{Z}/8\mathbb{Z})^\times = \{1, 3, 5, 7\}$。其阶为 $\phi(8)=4$。我们检查每个非单位元素的阶：$3^2 \equiv 1 \pmod{8}$，$5^2 \equiv 1 \pmod{8}$，$7^2 \equiv 1 \pmod{8}$。所有非单位元素的阶都是 2。因此，这个群没有 4 阶元素，不是循环群。它同构于克莱因四元群 $C_2 \times C_2$。因此，8 是使 $\text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$ 不为循环群的最小整数 $n>2$。
-   对于 $n=12$，群是 $(\mathbb{Z}/12\mathbb{Z})^\times = \{1, 5, 7, 11\}$。其阶为 $\phi(12)=4$。我们检查元素的阶：$5^2 \equiv 1 \pmod{12}$，$7^2 \equiv 1 \pmod{12}$，$11^2 \equiv 1 \pmod{12}$。同样，这个群同构于 $C_2 \times C_2$。

根据伽罗瓦理论基本定理，伽罗瓦群的子群与域扩张的中间域之间存在一一对应关系。由于 $\text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$ 是阿贝尔群，它的所有子群都是正规子群，这意味着所有的中间域也都是 $\mathbb{Q}$ 上的伽罗瓦扩张。

一个特别重要的自同构是**复共轭** $\tau: z \mapsto \bar{z}$ [@problem_id:1832914]。它在 $\text{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$ 中对应于哪个元素？我们有：
$$
\tau(\zeta_n) = \overline{\exp\left(\frac{2\pi i}{n}\right)} = \exp\left(-\frac{2\pi i}{n}\right) = \zeta_n^{-1} = \zeta_n^{n-1}
$$
所以复共轭自同构就是 $\sigma_{n-1}$。这是一个 2 阶自同构（除非 $n=2$），因为它作用两次会得到恒等变换：$\tau(\tau(\zeta_n)) = \zeta_n^{(n-1)^2} = \zeta_n^{n^2 - 2n + 1} = (\zeta_n^n)^{n-2} \cdot \zeta_n = \zeta_n$。

由复共轭生成的 2 阶子群 $\{\text{id}, \tau\}$ 所固定的子域是 $\mathbb{Q}(\zeta_n)$ 中所有实数的集合，即 $\mathbb{Q}(\zeta_n) \cap \mathbb{R}$。这个子域被称为**最大实子域**，它可以由元素 $\zeta_n + \zeta_n^{-1}$ 生成。注意到：
$$
\zeta_n + \zeta_n^{-1} = \exp\left(\frac{2\pi i}{n}\right) + \exp\left(-\frac{2\pi i}{n}\right) = 2\cos\left(\frac{2\pi}{n}\right)
$$
这是一个实数。例如，在 $\mathbb{Q}(\zeta_5)$ 中，考虑元素 $\alpha = \zeta_5 + \zeta_5^{-1}$ [@problem_id:1785988]。它是一个实数。我们可以通过利用 $\Phi_5(\zeta_5) = 1 + \zeta_5 + \zeta_5^2 + \zeta_5^3 + \zeta_5^4 = 0$ 来找到 $\alpha$ 的最小多项式。将该式除以 $\zeta_5^2$ 得到 $(\zeta_5^2 + \zeta_5^{-2}) + (\zeta_5 + \zeta_5^{-1}) + 1 = 0$。由于 $\alpha^2 = (\zeta_5+\zeta_5^{-1})^2 = \zeta_5^2+2+\zeta_5^{-2}$，我们有 $\zeta_5^2+\zeta_5^{-2} = \alpha^2-2$。代入得到 $(\alpha^2-2) + \alpha + 1 = 0$，即 $\alpha^2 + \alpha - 1 = 0$。这个二次多项式在 $\mathbb{Q}$ 上不可约，因此 $\alpha$ 是一个无理数，并且 $[\mathbb{Q}(\alpha):\mathbb{Q}]=2$。这与伽罗瓦对应关系一致：$\text{Gal}(\mathbb{Q}(\zeta_5)/\mathbb{Q}) \cong (\mathbb{Z}/5\mathbb{Z})^\times$ 是一个 4 阶循环群，而固定 $\mathbb{Q}(\alpha)$ 的子群是 2 阶的 $\{\text{id}, \sigma_4\}$（$\sigma_4$ 即复共轭），其指数 $[G:H] = 4/2 = 2$。

伽罗瓦对应关系让我们能够精确地识别出分圆域的所有子域。例如，在 $\mathbb{Q}(\zeta_8)$ 中，我们知道 $\sqrt{2}$ 是一个元素，因为它等于 $\zeta_8 + \zeta_8^{-1} = 2\cos(\pi/4) = \sqrt{2}$。那么，哪个子群固定了子域 $\mathbb{Q}(\sqrt{2})$ 呢 [@problem_id:1785976]？我们需要找到所有满足 $\sigma_k(\sqrt{2}) = \sqrt{2}$ 的自同构 $\sigma_k \in \text{Gal}(\mathbb{Q}(\zeta_8)/\mathbb{Q}) = \{\sigma_1, \sigma_3, \sigma_5, \sigma_7\}$。
$$
\sigma_k(\sqrt{2}) = \sigma_k(\zeta_8 + \zeta_8^{-1}) = \sigma_k(\zeta_8) + \sigma_k(\zeta_8)^{-1} = \zeta_8^k + \zeta_8^{-k} = 2\cos\left(\frac{2\pi k}{8}\right) = 2\cos\left(\frac{k\pi}{4}\right)
$$
我们逐一检验 $k \in \{1, 3, 5, 7\}$：
-   $k=1$: $2\cos(\pi/4) = \sqrt{2}$。所以 $\sigma_1$ 固定 $\sqrt{2}$。
-   $k=3$: $2\cos(3\pi/4) = -\sqrt{2}$。所以 $\sigma_3$ 不固定 $\sqrt{2}$。
-   $k=5$: $2\cos(5\pi/4) = -\sqrt{2}$。所以 $\sigma_5$ 不固定 $\sqrt{2}$。
-   $k=7$: $2\cos(7\pi/4) = \sqrt{2}$。所以 $\sigma_7$ 固定 $\sqrt{2}$。
因此，固定子域 $\mathbb{Q}(\sqrt{2})$ 的子群是 $\{\sigma_1, \sigma_7\}$。这是一个 2 阶子群，与 $[\mathbb{Q}(\sqrt{2}):\mathbb{Q}]=2$ 的事实完全吻合。这个例子完美地展示了分圆域丰富的内部结构，以及伽罗瓦理论作为探索这种结构的强大工具。