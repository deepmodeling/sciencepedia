## 引言
伽马函数是[数学分析](@entry_id:139664)和应用科学中最重要的特殊函数之一。虽然其经典的积分定义广为人知，但它在整个复平面上的结构却更为复杂，尤其是在非正整数处的极点行为。为了全面理解伽马函数的性质，我们需要一个能精确捕捉其[全局解](@entry_id:180992)析结构的工具。这正是魏尔斯特拉斯乘积表示所要解决的问题：通过将其倒数 $1/\Gamma(z)$——一个整函数——表示为无穷乘积，我们可以从其零点的[分布](@entry_id:182848)来“构建”整个函数。

本文将带领读者深入探索伽马函数的这一核心表示。在第一章“原则与机理”中，我们将从哈达马分解定理出发，一步步推导出魏尔斯特拉斯乘积的完整形式，并剖析其每一个组成部分的精确作用。接着，在第二章“应用与跨学科联系”中，我们将展示这一理论的强大威力，看它如何被用来推导著名的函数恒等式、计算复杂的级数与积分，甚至与理论物理学的基本概念产生深刻的联系。最后，在“动手实践”部分，您将有机会通过解决具体问题来巩固和应用所学知识。让我们从这一优美乘积的构建原理开始。

## 原则与机理

在本章中，我们将深入探讨伽马函数（Gamma function）的一个核心表示——魏尔斯特拉斯乘积（Weierstrass product）。伽马函数 $\Gamma(z)$ 本身在复平面上并非整函数，因为它在非正整数处有极点。然而，其倒数 $1/\Gamma(z)$ 是一个[整函数](@entry_id:176232)，这为我们运用复分析中的强大工具——[无穷乘积表示](@entry_id:174133)——提供了可能。通过解构这个乘积的每一个组成部分，我们将揭示其深刻的数学内涵，并展示它如何与伽马函数的其他基本性质（如[函数方程](@entry_id:199663)和特殊值）完美契合。

### 伽马函数的魏尔斯特拉斯乘积表示

伽马函数的倒数可以表示为以下优美的无穷乘积形式：
$$
\frac{1}{\Gamma(z)} = z e^{\gamma z} \prod_{n=1}^{\infty} \left(1 + \frac{z}{n}\right) e^{-z/n}
$$
这个公式对所有复数 $z$ 都成立。公式中的各个组成部分都具有明确的意义：
*   因子 $z$ 对应于 $1/\Gamma(z)$ 在 $z=0$ 处的一个简单零点。
*   无穷乘积 $\prod_{n=1}^{\infty} \left(1 + \frac{z}{n}\right)$ 揭示了 $1/\Gamma(z)$ 在所有负整数 $z = -1, -2, -3, \dots$ 处的简单零点。
*   $\gamma$ 是著名的[欧拉-马歇罗尼常数](@entry_id:146205)（Euler-Mascheroni constant），定义为 $\gamma = \lim_{N \to \infty} \left( \sum_{k=1}^{N} \frac{1}{k} - \ln N \right) \approx 0.577$。因子 $e^{\gamma z}$ 是一个归一化因子。
*   因子 $e^{-z/n}$ 被称为收敛因子，它的存在是为了确保无穷乘积在整个复平面上[一致收敛](@entry_id:146084)。

### 从哈达马分解定理推导

这个乘积形式并非凭空而来，而是可以从哈达马分解定理（Hadamar[d'](@entry_id:189153)s factorization theorem）系统地推导出来。该定理为整函数提供了一种通过其零点进行分解的方法。

首先，我们必须确定 $1/\Gamma(z)$ 的基本属性。它是一个[整函数](@entry_id:176232)，其增长阶（order of growth）为1。它的零点恰好位于所有非正整数处 [@problem_id:2284149]。具体来说：
*   当 $z=0$ 时，$1/\Gamma(z) \to 0$。
*   对于任何正整数 $n$，$1/\Gamma(-n) = 0$。

由于 $\Gamma(z)$ 的极点都是简单极点，因此 $1/\Gamma(z)$ 的这些零点也都是简单零点。

根据哈达马分解定理，一个增长阶为1、在 $z=0$ 有一个简单零点且在 $z_n = -n$ ($n=1, 2, \dots$) 处有简单零点的[整函数](@entry_id:176232) $f(z)$，可以表示为以下一般形式：
$$
f(z) = z e^{A+Bz} \prod_{n=1}^{\infty} \left(1 - \frac{z}{z_n}\right) e^{z/z_n}
$$
将 $f(z) = 1/\Gamma(z)$ 和零点 $z_n = -n$ 代入，我们得到：
$$
\frac{1}{\Gamma(z)} = z e^{A+Bz} \prod_{n=1}^{\infty} \left(1 + \frac{z}{n}\right) e^{-z/n}
$$
这与我们之前给出的最终形式非常接近，现在我们的任务是确定常数 $A$ 和 $B$ [@problem_id:2284158] [@problem_id:810614]。

**确定常数 A**

为了确定 $A$，我们考察 $z \to 0$ 时的行为。伽马函数的一个基本性质是 $\Gamma(1)=1$。利用其[函数方程](@entry_id:199663) $\Gamma(z+1) = z\Gamma(z)$，我们得到 $\lim_{z\to 0} z\Gamma(z) = \Gamma(1) = 1$。这意味着：
$$
\lim_{z\to 0} \frac{1}{z\Gamma(z)} = \lim_{z\to 0} \frac{1/\Gamma(z)}{z} = 1
$$
现在，我们对乘积表示进行同样的操作：
$$
\frac{1/\Gamma(z)}{z} = e^{A+Bz} \prod_{n=1}^{\infty} \left(1 + \frac{z}{n}\right) e^{-z/n}
$$
当 $z \to 0$ 时，等式右边的指数项 $e^{A+Bz} \to e^A$，而[无穷乘积](@entry_id:176333)中的每一项都趋于1，因此整个[无穷乘积](@entry_id:176333)也趋于1。于是我们得到：
$$
\lim_{z\to 0} \frac{1/\Gamma(z)}{z} = e^A
$$
比较两个极限结果，我们得出 $e^A = 1$，这意味着 $A=0$。

**确定常数 B**

确定 $B$ 的过程更为精妙。我们可以再次利用伽马函数的[函数方程](@entry_id:199663) $\Gamma(z+1)=z\Gamma(z)$。对于其倒数 $f(z)=1/\Gamma(z)$，这个方程意味着 $f(z+1) = \frac{1}{\Gamma(z+1)} = \frac{1}{z\Gamma(z)} = \frac{f(z)}{z}$。因此，比值 $\frac{f(z+1)}{f(z)} = \frac{1}{z}$。

现在，我们利用已确定 $A=0$ 的乘积表示来计算这个比值：
$$
\frac{f(z+1)}{f(z)} = \frac{(z+1)e^{B(z+1)}\prod_{n=1}^{\infty} (1+\frac{z+1}{n})e^{-\frac{z+1}{n}}}{z e^{Bz}\prod_{n=1}^{\infty} (1+\frac{z}{n})e^{-\frac{z}{n}}} = \frac{z+1}{z} e^B \prod_{n=1}^{\infty} \frac{(1+\frac{z+1}{n})e^{-\frac{1}{n}}}{(1+\frac{z}{n})}
$$
我们来分析这个[无穷乘积](@entry_id:176333)。其部分乘积为：
$$
\prod_{n=1}^{N} \frac{1+\frac{z+1}{n}}{1+\frac{z}{n}} = \prod_{n=1}^{N} \frac{n+z+1}{n+z} = \frac{(z+2)(z+3)\cdots(z+N+1)}{(z+1)(z+2)\cdots(z+N)} = \frac{z+N+1}{z+1}
$$
因此，包含收敛因子的部分乘积为：
$$
\lim_{N\to\infty} \frac{z+N+1}{z+1} \prod_{n=1}^{N} e^{-1/n} = \lim_{N\to\infty} \frac{z+N+1}{z+1} e^{-\sum_{n=1}^{N} 1/n}
$$
利用[欧拉-马歇罗尼常数](@entry_id:146205)的定义，$\sum_{n=1}^{N} \frac{1}{n} \approx \ln N + \gamma$。因此 $e^{-\sum_{n=1}^{N} 1/n} \approx e^{-(\ln N + \gamma)} = \frac{e^{-\gamma}}{N}$。
$$
\lim_{N\to\infty} \frac{N(1 + (z+1)/N)}{z+1} \frac{e^{-\gamma}}{N} = \frac{e^{-\gamma}}{z+1}
$$
将此结果代回比值表达式：
$$
\frac{f(z+1)}{f(z)} = \frac{z+1}{z} e^B \frac{e^{-\gamma}}{z+1} = \frac{e^{B-\gamma}}{z}
$$
将这个结果与从[函数方程](@entry_id:199663)得到的 $\frac{f(z+1)}{f(z)} = \frac{1}{z}$ 相比较，我们必须有 $e^{B-\gamma} = 1$，这表明 $B = \gamma$。

至此，我们已经通过严格的推导确定了 $A=0$ 和 $B=\gamma$ [@problem_id:2284158]。这与直接比较一般形式和特定形式所得出的结论一致 [@problem_id:2284141]。最终，我们得到了伽马函数倒数的魏尔斯特拉斯乘积表示：
$$
\frac{1}{\Gamma(z)} = z e^{\gamma z} \prod_{n=1}^{\infty} \left(1 + \frac{z}{n}\right) e^{-z/n}
$$

### 乘积形式的[结构分析](@entry_id:153861)

现在我们来剖析这个公式的各个组成部分，理解它们各自扮演的角色。

**零点因子与[伽马函数的极点](@entry_id:188704)**

如前所述，因子 $z$ 和[无穷乘积](@entry_id:176333)中的每一项 $\left(1 + \frac{z}{n}\right)$ 都直接对应于 $1/\Gamma(z)$ 的一个零点。由于 $\Gamma(z) = 1/(1/\Gamma(z))$，这些零点正是 $\Gamma(z)$ 的极点。因此，魏尔斯特拉斯乘积直观地告诉我们，$\Gamma(z)$ 在所有非正整数 $z=0, -1, -2, \dots$ 处有极点 [@problem_id:2284149]。

**收敛因子的必要性**

为什么需要 $e^{-z/n}$ 这个因子？考虑一个没有这些收敛因子的“朴素”乘积 $\prod_{n=1}^{\infty} (1 + z/n)$。对数泰勒展开告诉我们 $\ln(1+x) = x - \frac{x^2}{2} + \dots$。一个[无穷乘积](@entry_id:176333) $\prod(1+a_n)$ [收敛的必要条件](@entry_id:157681)是 $\sum a_n$ 收敛。在我们的例子中，$a_n = z/n$，而级数 $\sum z/n = z\sum 1/n$ 是发散的（与调和级数一样）。因此，朴素乘积是发散的。

收敛因子 $e^{-z/n}$ 的作用就是“修正”这种发散。考察乘积项的对数：
$$
\ln\left[ \left(1 + \frac{z}{n}\right) e^{-z/n} \right] = \ln\left(1 + \frac{z}{n}\right) - \frac{z}{n}
$$
当 $n$ 很大时，$\frac{z}{n}$ 很小，所以 $\ln\left(1 + \frac{z}{n}\right) \approx \frac{z}{n} - \frac{z^2}{2n^2}$。因此：
$$
\ln\left[ \left(1 + \frac{z}{n}\right) e^{-z/n} \right] \approx \left(\frac{z}{n} - \frac{z^2}{2n^2}\right) - \frac{z}{n} = -\frac{z^2}{2n^2}
$$
由于级数 $\sum_{n=1}^{\infty} \frac{1}{n^2}$ 是收敛的（等于 $\pi^2/6$），所以修正后的乘积的对数级数 $\sum \ln[\dots]$ 是绝对收敛的，这保证了原[无穷乘积](@entry_id:176333)对所有 $z$ 都收敛。问题 [@problem_id:2284151] 的分析表明，不含收敛因子的部分乘积 $\prod_{n=1}^{N}(1+z/n)$ 的增长行为近似于 $N^z$，这清晰地展示了发散性，而收敛因子 $e^{-z \sum 1/n} \approx e^{-z \ln N} = N^{-z}$ 正好抵消了这种发散。

**归一化因子与 $\Gamma(1)=1$**

即使[无穷乘积收敛](@entry_id:177632)，我们还需要确保它的值是正确的。因子 $e^{\gamma z}$ 的作用是进行归一化，以满足基本条件 $\Gamma(1)=1$。

让我们考虑一个没有 $e^{\gamma z}$ 因子的函数会怎样 [@problem_id:2284144]。设 $G(z) = z \prod_{n=1}^{\infty} \left(1 + \frac{z}{n}\right) e^{-z/n}$。那么 $1/\Gamma(z) = G(z) e^{\gamma z}$。在 $z=1$ 处，我们有 $1/\Gamma(1) = G(1)e^{\gamma}$。由于 $\Gamma(1)=1$，我们得到 $1 = G(1)e^{\gamma}$，即 $G(1) = e^{-\gamma}$。这意味着，如果没有 $e^{\gamma z}$ 这个因子，我们会得到一个“伪伽马函数”，它在 $z=1$ 处的值是 $e^{\gamma}$ 而不是1。因此，$e^{\gamma z}$ 这个看似复杂的因子，其作用恰恰是为了满足最基本的[归一化条件](@entry_id:156486)。

**与[函数方程](@entry_id:199663)的一致性**

魏尔斯特拉斯乘积也完美地内嵌了函数方程 $\Gamma(z+1) = z\Gamma(z)$。通过直接计算乘积形式的比值 $P(z)/P(z+1)$，其中 $P(z) = \prod_{n=1}^{\infty} (1 + z/n)e^{-z/n}$，可以验证这种一致性。计算表明，该比值等于 $(z+1)e^{\gamma}$ [@problem_id:2284153]，这与我们之前用于推导常数 $B$ 的中间步骤相符，并最终确保了函数方程的成立。

### 应用：[对数导数](@entry_id:169238)与多伽马函数

魏尔斯特拉斯乘积的一个强大应用是推导伽马函数的[对数导数](@entry_id:169238)——多伽马函数（Polygamma functions）的[级数表示](@entry_id:175860)。

**双伽马函数**

双伽马函数（Digamma function）$\psi(z)$ 定义为 $\psi(z) = \frac{d}{dz}\ln\Gamma(z)$。我们可以通过对 $1/\Gamma(z)$ 的乘积表示取对数然后求导来得到它的级数形式。
$$
\ln\left(\frac{1}{\Gamma(z)}\right) = -\ln\Gamma(z) = \ln z + \gamma z + \sum_{n=1}^{\infty} \left[ \ln\left(1+\frac{z}{n}\right) - \frac{z}{n} \right]
$$
两边对 $z$ 求导（由于级数的一致收敛性，可以逐项求导）：
$$
-\psi(z) = \frac{1}{z} + \gamma + \sum_{n=1}^{\infty} \left( \frac{1/(n)}{1+z/n} - \frac{1}{n} \right) = \frac{1}{z} + \gamma + \sum_{n=1}^{\infty} \left( \frac{1}{z+n} - \frac{1}{n} \right)
$$
整理后得到 $\psi(z)$ 的经典[级数表示](@entry_id:175860)：
$$
\psi(z) = -\gamma - \frac{1}{z} + \sum_{n=1}^{\infty} \left( \frac{1}{n} - \frac{1}{z+n} \right)
$$
这个公式非常有用，例如，它可以用来计算一些特殊的无穷级数。比如，我们可以计算 $S = \sum_{n=1}^{\infty} \left( \frac{1}{n} - \frac{1}{n + 1/2} \right)$。根据上述公式，这个和就是 $\psi(1/2) + \gamma + 1/(1/2) = \psi(1/2) + \gamma + 2$。利用已知的特殊值 $\psi(1/2) = -\gamma - 2\ln(2)$，我们立即得到 $S = 2 - 2\ln(2)$ [@problem_id:2284142]。

**三伽马函数及更高阶**

三伽马函数（Trigamma function）定义为 $\psi_1(z) = \psi'(z)$。通过对 $\psi(z)$ 的[级数表示](@entry_id:175860)再次逐项求导，我们可以轻松得到 $\psi_1(z)$ 的[级数表示](@entry_id:175860) [@problem_id:2284163]：
$$
\psi_1(z) = \frac{d}{dz} \left( -\gamma - \frac{1}{z} + \sum_{n=1}^{\infty} \left( \frac{1}{n} - \frac{1}{z+n} \right) \right) = \frac{1}{z^2} + \sum_{n=1}^{\infty} \frac{1}{(z+n)^2}
$$
这个级数可以更紧凑地写为：
$$
\psi_1(z) = \sum_{n=0}^{\infty} \frac{1}{(z+n)^2}
$$
这个过程可以无限进行下去，得到所有高阶多伽马函数的[级数表示](@entry_id:175860)。

### 应用：极点与留数

最后，魏尔斯特拉斯乘积也为我们提供了一种计算 $\Gamma(z)$ 在其极点处留数（residue）的有效方法。我们已经知道极点位于 $z = -k$（其中 $k$ 为非负整数）。由于 $1/\Gamma(z)$ 在这些点的零点是简单的，所以 $\Gamma(z)$ 的极点也是简单极点。

在简单极点 $z=-k$ 处的留数定义为 $\text{Res}(\Gamma, -k) = \lim_{z \to -k} (z+k)\Gamma(z)$。我们可以利用 $1/\Gamma(z)$ 的乘积来计算这个极限。
$$
\frac{1}{\Gamma(z)} = \left(1+\frac{z}{k}\right) \cdot z e^{\gamma z} \prod_{n=1, n\neq k}^{\infty} \left(1 + \frac{z}{n}\right) e^{-z/n} = \frac{z+k}{k} \cdot z e^{\gamma z} \prod_{n=1, n\neq k}^{\infty} (\dots)
$$
因此：
$$
(z+k)\Gamma(z) = \frac{k}{z e^{\gamma z} \prod_{n=1, n\neq k}^{\infty} \left(1 + \frac{z}{n}\right) e^{-z/n}}
$$
取 $z \to -k$ 的极限，我们得到：
$$
\text{Res}(\Gamma, -k) = \frac{k}{(-k) e^{-\gamma k} \prod_{n=1, n\neq k}^{\infty} \left(1 - \frac{k}{n}\right) e^{k/n}}
$$
经过更细致的计算，可以得到一个更简洁的结果。一个更直接的方法是利用函数方程。例如，我们来计算在 $z=-2$ 处的留数 [@problem_id:2284171]。
$$
\text{Res}(\Gamma, -2) = \lim_{z \to -2} (z+2)\Gamma(z)
$$
利用 $\Gamma(z) = \frac{\Gamma(z+1)}{z} = \frac{\Gamma(z+2)}{z(z+1)} = \frac{\Gamma(z+3)}{z(z+1)(z+2)}$。
$$
\text{Res}(\Gamma, -2) = \lim_{z \to -2} (z+2) \frac{\Gamma(z+3)}{z(z+1)(z+2)} = \lim_{z \to -2} \frac{\Gamma(z+3)}{z(z+1)} = \frac{\Gamma(1)}{(-2)(-1)} = \frac{1}{2}
$$
通过类似的方法，可以推导出在 $z=-k$ 处的留数的通用公式：
$$
\text{Res}(\Gamma, -k) = \frac{(-1)^k}{k!}
$$
这个结果优美地将伽马函数在其极点处的局部行为与[阶乘](@entry_id:266637)联系起来，再次展示了数学结构之间的深刻统一。