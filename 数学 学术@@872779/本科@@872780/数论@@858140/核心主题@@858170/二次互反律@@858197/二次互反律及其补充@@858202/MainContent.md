## 引言
[二次互反律](@entry_id:183186)是数论领域一块璀璨的基石，它以惊人的简洁与对称性，揭示了不同素数模下二次同余方程解的存在性之间的深刻联系。这一理论源于一个古老而基本的问题：对于给定的模，一个整数能否表示为另一个整数的平方？尽管问题形式简单，其答案却引向了数论中最优美和影响深远的思想。本文旨在系统地引导读者穿越[二次互反律](@entry_id:183186)的理论世界，从基本原理到前沿应用，全面掌握其精髓。

在接下来的章节中，我们将首先在“原理与机制”一章中，从二次剩余和[勒让德符号](@entry_id:194530)的定义出发，详细阐述[二次互反律](@entry_id:183186)的主定律及其补充定律，并将其推广至[雅可比符号](@entry_id:191224)。随后，在“应用与跨学科联系”一章中，我们将展示这些理论如何作为强大的计算工具，应用于[密码学](@entry_id:139166)、[代数数论](@entry_id:148067)等多个领域。最后，通过“动手实践”部分，读者将有机会将所学知识付诸实践，巩固理解。

## 原理与机制

本章旨在深入探讨[二次互反律](@entry_id:183186)的核心原理与机制。我们将从最基本的定义出发，系统地构建理解这一优美理论所需的全部概念工具。我们将定义二次剩余，引入[勒让德符号](@entry_id:194530)，并阐述其基本判别法。在此基础上，我们将详细介绍[二次互反律](@entry_id:183186)的主体内容及其两个重要的补充定律，并通过实例展示其强大的计算能力。最后，我们将把这一理论推广至复合模，引入[雅可比符号](@entry_id:191224)，并探讨其应用与局限。

### 二次剩余与二次非剩余

二次互反理论的研究对象根植于一个非常基本的问题：对于一个给定的奇素数模 $p$，哪些数是另一个数的平方？为了精确地描述这个问题，我们引入**二次剩余**（quadratic residue）和**二次非剩余**（quadratic non-residue）的概念。

设 $p$ 是一个奇素数。对于整数 $a$，如果[同余](@entry_id:143700)方程 $x^2 \equiv a \pmod{p}$ 有解，则称 $a$ 是模 $p$ 的一个**二次剩余**。如果该同余方程无解，则称 $a$ 是模 $p$ 的一个**二次非剩余**。

首先，我们考虑 $a \equiv 0 \pmod{p}$ 的平凡情况。由于 $x=0$ 使得 $x^2 = 0 \equiv 0 \pmod{p}$，因此 $0$ 总是模任何素数 $p$ 的二次剩余。[@problem_id:3089027]

更有趣的是非零的情况。我们考虑模 $p$ 的非零[剩余类](@entry_id:185226)构成的[乘法群](@entry_id:155975) $(\mathbb{Z}/p\mathbb{Z})^\times = \{1, 2, \dots, p-1\}$。这是一个阶为 $p-1$ 的循环群。群内的二次剩余是哪些元素呢？我们可以通过考察平方映射 $f: (\mathbb{Z}/p\mathbb{Z})^\times \to (\mathbb{Z}/p\mathbb{Z})^\times$，其定义为 $f(x) = x^2 \pmod{p}$，来回答这个问题。

这个映射是一个[群同态](@entry_id:140603)，因为 $f(xy) = (xy)^2 = x^2y^2 = f(x)f(y)$。其像集 $\text{Im}(f)$ 正是 $(\mathbb{Z}/p\mathbb{Z})^\times$ 中所有二次剩余构成的集合。根据群论的[第一同构定理](@entry_id:146795)，像集的大小为 $|(\mathbb{Z}/p\mathbb{Z})^\times| / |\ker(f)|$。

映射的核 $\ker(f)$ 由所有满足 $x^2 \equiv 1 \pmod{p}$ 的元素 $x$ 构成。这个方程可以写作 $(x-1)(x+1) \equiv 0 \pmod{p}$。由于 $\mathbb{Z}/p\mathbb{Z}$ 是一个域（因此是整环），我们必然有 $x-1 \equiv 0 \pmod{p}$ 或 $x+1 \equiv 0 \pmod{p}$。因此，解为 $x \equiv 1 \pmod{p}$ 和 $x \equiv -1 \pmod{p}$。因为 $p$ 是奇素数，$p > 2$，所以 $1 \not\equiv -1 \pmod{p}$。这意味着核恰好包含两个元素 $\{1, -1\}$，即 $|\ker(f)| = 2$。

由此，我们得出非零二次剩余的数量为：
$$ |\text{Im}(f)| = \frac{|(\mathbb{Z}/p\mathbb{Z})^\times|}{|\ker(f)|} = \frac{p-1}{2} $$
这也表明，非零二次剩余的集合是 $(\mathbb{Z}/p\mathbb{Z})^\times$ 的一个指数为 $2$ 的[子群](@entry_id:146164)。[@problem_id:3089027]

群 $(\mathbb{Z}/p\mathbb{Z})^\times$ 中剩下的元素，即那些不在像集中的元素，就是二次非剩余。其数量同样为 $(p-1) - \frac{p-1}{2} = \frac{p-1}{2}$。

总结一下：对于一个奇素数 $p$，在模 $p$ 的 $p$ 个[剩余类](@entry_id:185226) $\{0, 1, \dots, p-1\}$ 中：
- 有 $1$ 个二次剩余是 $0$。
- 有 $\frac{p-1}{2}$ 个非零的二次剩余。
- 有 $\frac{p-1}{2}$ 个二次非剩余。
- 因此，总共有 $1 + \frac{p-1}{2} = \frac{p+1}{2}$ 个二次剩余。

### [勒让德符号](@entry_id:194530)：一个强大的记号

为了系统地研究二次剩余，法国数学家 Adrien-Marie Legendre 引入了一个极为方便的记号，即**[勒让德符号](@entry_id:194530)**（Legendre symbol）。

对于一个奇素数 $p$ 和一个整数 $a$，[勒让德符号](@entry_id:194530) $\left(\frac{a}{p}\right)$ 定义如下：
$$
\left(\frac{a}{p}\right) =
\begin{cases}
1  &\text{如果 } a \text{ 是模 } p \text{ 的非零二次剩余} \\
-1 &\text{如果 } a \text{ 是模 } p \text{ 的二次非剩余} \\
0  &\text{如果 } p \mid a \quad (\text{即 } a \equiv 0 \pmod{p})
\end{cases}
$$
这个符号优雅地将一个数是否为二次剩余的问题转化为了一个取值为 $\{1, -1, 0\}$ 的函数值的计算问题。[@problem_id:3089062]

[勒让德符号](@entry_id:194530)的一个美妙性质是它直接关联着[同余](@entry_id:143700)方程 $x^2 \equiv a \pmod{p}$ 的解的个数。[@problem_id:3089021]
- 如果 $\left(\frac{a}{p}\right) = 1$，意味着 $a$ 是一个非零二次剩余。设 $x_0$ 是一个解，即 $x_0^2 \equiv a \pmod{p}$。由于 $a \not\equiv 0 \pmod{p}$，我们必有 $x_0 \not\equiv 0 \pmod{p}$。那么 $(-x_0)^2 = x_0^2 \equiv a \pmod{p}$，所以 $-x_0$ 也是一个解。由于 $p$ 是奇素数，$x_0 \not\equiv -x_0 \pmod{p}$。根据拉格朗日定理，一个二次多项式在域 $\mathbb{Z}/p\mathbb{Z}$ 中至多有两个根，所以方程恰好有 $2$ 个解。
- 如果 $\left(\frac{a}{p}\right) = -1$，根据定义，方程无解，即有 $0$ 个解。
- 如果 $\left(\frac{a}{p}\right) = 0$，意味着 $a \equiv 0 \pmod{p}$。方程变为 $x^2 \equiv 0 \pmod{p}$，其唯一解为 $x \equiv 0 \pmod{p}$。所以方程恰好有 $1$ 个解。

我们可以将这三种情况统一成一个简洁的公式：[同余](@entry_id:143700)方程 $x^2 \equiv a \pmod{p}$ 的解的个数为 $1 + \left(\frac{a}{p}\right)$。

[勒让德符号](@entry_id:194530)最重要的性质之一是其**完全积性**：如果 $a, b$ 是任意整数，则
$$ \left(\frac{ab}{p}\right) = \left(\frac{a}{p}\right)\left(\frac{b}{p}\right) $$
这个性质源于 $(\mathbb{Z}/p\mathbb{Z})^\times$ 中二次剩余[子群](@entry_id:146164)的性质：两个二次剩余的乘积是二次剩余（$1 \cdot 1 = 1$），一个二次剩余与一个非剩余的乘积是非剩余（$1 \cdot (-1) = -1$），而两个非剩余的乘积是二次剩余（$(-1) \cdot (-1) = 1$）。这一性质使我们能将计算 $\left(\frac{a}{p}\right)$ 的[问题分解](@entry_id:272624)为计算其素因子的[勒让德符号](@entry_id:194530)。

### 判定[勒让德符号](@entry_id:194530)的基本判别法

有了[勒让德符号](@entry_id:194530)，我们的下一个目标是找到计算它的有效方法。直接检查 $x^2 \equiv a \pmod p$ 是否有解在 $p$ 很大时是不可行的。幸运的是，我们有两个强大的理论工具：欧拉判别法和[高斯引理](@entry_id:149771)。

**欧拉判别法 (Euler's Criterion)**
欧拉判别法给出了一个计算[勒让德符号](@entry_id:194530)的代数公式。它断言，对于奇素数 $p$ 和整数 $a$ 且 $p \nmid a$：
$$ \left(\frac{a}{p}\right) \equiv a^{\frac{p-1}{2}} \pmod{p} $$
由于 $\left(\frac{a}{p}\right)$ 的取值为 $1$ 或 $-1$，且在模 $p$ ($p>2$) 的意义下 $1$ 和 $-1$ 是不相等的，这个[同余](@entry_id:143700)式实际上是一个等式。欧拉判别法是连接[勒让德符号](@entry_id:194530)和模 $p$ [乘法群](@entry_id:155975)结构的桥梁。

**[高斯引理](@entry_id:149771) (Gauss's Lemma)**
[高斯引理](@entry_id:149771)则从一个更组合的角度来判定[勒让德符号](@entry_id:194530)。对于一个与奇素数 $p$ [互素](@entry_id:143119)的整数 $a$，考虑集合 $S = \{a, 2a, 3a, \dots, \frac{p-1}{2}a\}$。我们将集合中每个元素对 $p$ 取其**最小[绝对值](@entry_id:147688)剩余**（即落在区间 $(-\frac{p}{2}, \frac{p}{2})$ 内的剩余）。记这些最小[绝对值](@entry_id:147688)剩余中负数的个数为 $N$。[高斯引理](@entry_id:149771)指出：
$$ \left(\frac{a}{p}\right) = (-1)^N $$
[高斯引理](@entry_id:149771)虽然形式上比欧拉判别法复杂，但它却是证明[二次互反律](@entry_id:183186)主定律和其第二补充定律的基石。

在逻辑上，欧拉判别法和[高斯引理](@entry_id:149771)是等价的。从[高斯引理](@entry_id:149771)出发，通过考虑乘积 $\prod_{k=1}^{(p-1)/2} (ka) \pmod p$ 的两种不同计算方式，可以推导出欧拉判别法。反之，从欧拉判别法出发，同样可以推导出[高斯引理](@entry_id:149771)。因此，它们可以被视为二次剩余理论的两个等价的出发点。[@problem_id:3089049]

### [二次互反律](@entry_id:183186)及其补充定律

[二次互反律](@entry_id:183186)及其补充定律是数论中最深刻和最有用的结果之一，它们极大地简化了[勒让德符号](@entry_id:194530)的计算。[@problem_id:3089012]

**第一补充定律 (First Supplement)**
第一补充定律回答了 $-1$ 何时是模 $p$ 的二次剩余。利用欧拉判别法，我们可以轻易证明它。令 $a = -1$：
$$ \left(\frac{-1}{p}\right) = (-1)^{\frac{p-1}{2}} $$
这个结果的含义是：
- 如果 $p \equiv 1 \pmod{4}$，那么 $\frac{p-1}{2}$ 是偶数，所以 $\left(\frac{-1}{p}\right) = 1$。
- 如果 $p \equiv 3 \pmod{4}$，那么 $\frac{p-1}{2}$ 是奇数，所以 $\left(\frac{-1}{p}\right) = -1$。
也就是说，$-1$ 是模 $p$ 的二次剩余当且仅当 $p$ 是 $4k+1$ 型的素数。[@problem_id:3089016]

**第二补充定律 (Second Supplement)**
第二补充定律确定了 $2$ 何时是模 $p$ 的二次剩余。这个定律的证明通常依赖于[高斯引理](@entry_id:149771)。通过在[高斯引理](@entry_id:149771)中令 $a=2$，并仔细计算集合 $\{2, 4, 6, \dots, p-1\}$ 中最小[绝对值](@entry_id:147688)剩余为负数的个数，可以得到以下结论：[@problem_id:3089057]
$$ \left(\frac{2}{p}\right) = (-1)^{\frac{p^2-1}{8}} $$
这个公式等价于：
- 如果 $p \equiv 1 \pmod{8}$ 或 $p \equiv 7 \pmod{8}$，那么 $\frac{p^2-1}{8}$ 是偶数，所以 $\left(\frac{2}{p}\right) = 1$。
- 如果 $p \equiv 3 \pmod{8}$ 或 $p \equiv 5 \pmod{8}$，那么 $\frac{p^2-1}{8}$ 是奇数，所以 $\left(\frac{2}{p}\right) = -1$。
即 $2$ 是模 $p$ 的二次剩余当且仅当 $p \equiv \pm 1 \pmod{8}$。

**[二次互反律](@entry_id:183186)主定律 (The Main Law of Quadratic Reciprocity)**
对于两个不同的奇素数 $p$ 和 $q$，[二次互反律](@entry_id:183186)主定律揭示了[勒让德符号](@entry_id:194530) $\left(\frac{p}{q}\right)$ 和 $\left(\frac{q}{p}\right)$ 之间惊人的对称关系。其最简洁的数学形式为：
$$ \left(\frac{p}{q}\right) \left(\frac{q}{p}\right) = (-1)^{\frac{p-1}{2} \frac{q-1}{2}} $$
这个公式的指数部分仅当 $\frac{p-1}{2}$ 和 $\frac{q-1}{2}$ 均为奇数时才是奇数，这等价于 $p \equiv 3 \pmod{4}$ 且 $q \equiv 3 \pmod{4}$。因此，我们可以用语言描述这个定律：
- 如果 $p$ 或 $q$ 中至少有一个形如 $4k+1$，则 $\left(\frac{p}{q}\right) = \left(\frac{q}{p}\right)$。
- 如果 $p$ 和 $q$ 都形如 $4k+3$，则 $\left(\frac{p}{q}\right) = -\left(\frac{q}{p}\right)$。

主定律的证明相当精妙，最经典的初等证明之一（由 Eisenstein 给出）正是基于[高斯引理](@entry_id:149771)。例如，为了计算 $\left(\frac{3}{p}\right)$，我们可以应用[高斯引理](@entry_id:149771)，计算集合 $\{3, 6, \dots, 3\frac{p-1}{2}\}$ 中，有多少个数的最小[绝对值](@entry_id:147688)剩余是负数。通过分析 $k$ 的取值范围，可以发现这个数目 $N$ 的奇偶性取决于 $p \pmod{12}$ 的值，最终得到 $\left(\frac{3}{p}\right) = 1$ 当且仅当 $p \equiv \pm 1 \pmod{12}$。[@problem_id:3089051] 这种方法虽然繁琐，但揭示了[高斯引理](@entry_id:149771)在证明具体互反关系时的威力。

### 应用：计算[勒让德符号](@entry_id:194530)

[二次互反律](@entry_id:183186)及其补充定律之所以强大，是因为它们提供了一种“翻转”并“化简”[勒让德符号](@entry_id:194530)的算法。计算 $\left(\frac{a}{p}\right)$ 的一般策略是：
1.  **约化**：将分子 $a$ 对模 $p$ 取余，即 $\left(\frac{a}{p}\right) = \left(\frac{a \pmod p}{p}\right)$。
2.  **分解**：利用[积性](@entry_id:187940)将分子分解为素数的乘积，$\left(\frac{a_1 a_2}{p}\right) = \left(\frac{a_1}{p}\right)\left(\frac{a_2}{p}\right)$。
3.  **处理特殊因子**：使用补充定律计算 $\left(\frac{-1}{p}\right)$ 和 $\left(\frac{2}{p}\right)$。
4.  **翻转**：对于奇素数因子 $q$，使用主定律将 $\left(\frac{q}{p}\right)$ 替换为 $\pm\left(\frac{p}{q}\right)$。
5.  **重复**：对新的符号 $\left(\frac{p}{q}\right)$ 重复步骤1-4，直到所有符号都可直接求值。

我们以确定模 $23$ 的所有二次剩余为例，展示这个过程。[@problem_id:3089028] 我们需要计算 $\left(\frac{a}{23}\right)$ 对于 $a=1, 2, \dots, 22$ 的值。
- $a=1$: $\left(\frac{1}{23}\right)=1$ (1总是二次剩余)。
- $a=2$: $23 \equiv -1 \pmod 8$，根据第二补充定律，$\left(\frac{2}{23}\right)=1$。
- $a=3$: 令 $p=3, q=23$。由于 $3 \equiv 3 \pmod 4$ 且 $23 \equiv 3 \pmod 4$，$\left(\frac{3}{23}\right) = -\left(\frac{23}{3}\right) = -\left(\frac{2}{3}\right)$。因为 $2$ 不是模 $3$ 的二次剩余，$\left(\frac{2}{3}\right)=-1$。所以 $\left(\frac{3}{23}\right) = -(-1)=1$。
- $a=4$: $\left(\frac{4}{23}\right) = \left(\frac{2^2}{23}\right) = 1$。
- $a=5$: 令 $p=5, q=23$。由于 $5 \equiv 1 \pmod 4$，$\left(\frac{5}{23}\right) = \left(\frac{23}{5}\right) = \left(\frac{3}{5}\right)$。再次应用定律，$5 \equiv 1 \pmod 4$，$\left(\frac{3}{5}\right) = \left(\frac{5}{3}\right) = \left(\frac{2}{3}\right) = -1$。所以 $\left(\frac{5}{23}\right)=-1$。
- $a=6$: $\left(\frac{6}{23}\right) = \left(\frac{2}{23}\right)\left(\frac{3}{23}\right) = (1)(1)=1$。

通过系统地应用这些定律，我们可以计算出所有 $a$ 的[勒让德符号](@entry_id:194530)值。最终，模 $23$ 的二次剩余（包括 $0$）是 $\{0, 1, 2, 3, 4, 6, 8, 9, 12, 13, 16, 18\}$。

### 推广：[雅可比符号](@entry_id:191224)

[勒让德符号](@entry_id:194530)的定义要求分母必须是奇素数。在计算中，这意味着我们必须对分子进行素数分解。为了避免这一步，德国数学家 [Carl Gustav Jacob Jacobi](@entry_id:185667) 引入了**[雅可比符号](@entry_id:191224)**（Jacobi symbol），将[勒让德符号](@entry_id:194530)推广到奇数合数分母。

设 $n$ 是一个大于 $1$ 的奇数，其素数分解为 $n = p_1^{e_1} p_2^{e_2} \cdots p_k^{e_k}$。对于任意整数 $a$，[雅可比符号](@entry_id:191224) $\left(\frac{a}{n}\right)$ 定义为：
$$ \left(\frac{a}{n}\right) = \prod_{i=1}^k \left(\frac{a}{p_i}\right)^{e_i} $$
其中右边的 $\left(\frac{a}{p_i}\right)$ 是[勒让德符号](@entry_id:194530)。如果 $n$ 本身是素数，[雅可比符号](@entry_id:191224)的定义与[勒让德符号](@entry_id:194530)一致。[@problem_id:3089022]

[雅可比符号](@entry_id:191224)的神奇之处在于，[二次互反律](@entry_id:183186)及其补充定律对于它依然成立：
- $\left(\frac{-1}{n}\right) = (-1)^{\frac{n-1}{2}}$
- $\left(\frac{2}{n}\right) = (-1)^{\frac{n^2-1}{8}}$
- 对于[互素](@entry_id:143119)的奇数 $m, n$，$\left(\frac{m}{n}\right)\left(\frac{n}{m}\right) = (-1)^{\frac{m-1}{2}\frac{n-1}{2}}$

这使得[雅可比符号](@entry_id:191224)成为一个强大的计算工具。在计算 $\left(\frac{a}{n}\right)$ 时，我们可以“翻转”符号，而无需对 $a$ 或 $n$ 进行素数分解。

然而，使用[雅可比符号](@entry_id:191224)时必须格外小心一个关键点。[勒让德符号](@entry_id:194530) $\left(\frac{a}{p}\right)=1$ 意味着 $a$ 是模 $p$ 的二次剩余。但是，对于合数 $n$，**[雅可比符号](@entry_id:191224) $\left(\frac{a}{n}\right)=1$ 并不保证 $a$ 是模 $n$ 的二次剩余**。[@problem_id:3089022]

一个经典的例子是 $\left(\frac{2}{15}\right)$。根据定义和计算：
$$ \left(\frac{2}{15}\right) = \left(\frac{2}{3}\right)\left(\frac{2}{5}\right) = (-1)(-1) = 1 $$
然而，同余方程 $x^2 \equiv 2 \pmod{15}$ 并无解。因为根据[中国剩余定理](@entry_id:144030)，它等价于[方程组](@entry_id:193238) $x^2 \equiv 2 \pmod 3$ 和 $x^2 \equiv 2 \pmod 5$ 同时有解。但我们知道 $x^2 \equiv 2 \pmod 3$ 是无解的。

因此，[雅可比符号](@entry_id:191224)是一个纯粹的计算辅助工具。如果 $\left(\frac{a}{n}\right)=-1$，我们可以确定 $a$ 不是模 $n$ 的二次剩余（因为至少有一个素因子 $p_i$ 使得 $\left(\frac{a}{p_i}\right)=-1$）。但如果 $\left(\frac{a}{n}\right)=1$，我们无法得出任何关于 $a$ 是否是模 $n$ 二次剩余的结论。这个问题，即所谓的“伪平方”测试，在[现代密码学](@entry_id:274529)的[素性测试](@entry_id:266856)等领域中扮演着重要角色。