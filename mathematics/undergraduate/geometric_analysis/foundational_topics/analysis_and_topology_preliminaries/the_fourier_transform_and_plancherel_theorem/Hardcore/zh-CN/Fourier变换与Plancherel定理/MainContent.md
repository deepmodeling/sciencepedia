## 引言
傅里叶变换是现代数学与应用科学中一块不可或缺的基石，它提供了一种强有力的视角，将函数或信号分解为其基本的频率分量。这种从时域（或空域）到频域的转换，不仅简化了许多复杂问题，也揭示了现象背后的深层结构。然而，傅里叶变换的严谨理论并非一蹴而就，其定义、性质乃至逆变换的存在性都高度依赖于所作用的函数空间。从行为良好的函数到更广泛、更具挑战性的函数类别，如何建立一个完备且自洽的理论框架，是理解其全部威力的关键所在。

本文旨在系统地引导读者穿越傅里叶分析的核心地带，最终聚焦于其在 $L^2$ 空间上的巅峰理论——普朗歇尔定理。我们将回答一系列根本性问题：为什么需要Schwartz空间作为理论的起点？将理论推广到更常见的 $L^1$ 和 $L^2$ 空间会遇到哪些困难，又是如何通过普朗歇尔定理克服的？这个定理所蕴含的“能量守恒”究竟意味着什么？

为了回答这些问题，文章将分为三个部分展开：
-   在**原理与机制**一章中，我们将从Schwartz空间出发，建立傅里叶变换的基本性质，特别是“光滑-衰减对偶性”，然后逐步过渡到 $L^1$ 和 $L^2$ 理论，最终深入阐释普朗歇尔定理的证明思路与核心内涵。
-   在**应用与跨学科联系**一章中，我们将展示这些抽象理论如何在求解偏微分方程、算子理论、信号处理和量子力学等领域大放异彩。
-   最后，在**动手实践**部分，读者将通过具体问题，亲手运用普朗歇尔定理解决实际计算，加深对理论的理解。

现在，让我们从傅里叶变换最理想的舞台——Schwartz空间——开始，逐步揭开其背后的原理与机制。

## 原理与机制

本章旨在深入探讨傅里叶变换的核心原理，重点关注其在不同函数空间上的行为，最终引出其在 $L^2$ 空间上的完备理论，即 Plancherel 定理。我们将从行为最良好、运算最封闭的函数空间——Schwartz 空间——开始，逐步揭示傅里叶变换的基本性质，特别是其标志性的“光滑-衰减对偶性”。随后，我们将展示将这套理论推广到更广泛的 $L^1$ 和 $L^2$ 空间时所面临的挑战与解决方案，并最终阐明 Plancherel 定理作为能量守恒定律的深刻内涵。最后，我们将从几何与分布理论的视角，为傅里叶变换提供更广阔的理论图景。

### Schwartz 空间上的傅里叶变换

为了研究傅里叶变换的分析性质，我们首先需要一个“理想”的函数空间，其中函数及其傅里叶变换都具有足够好的性质，使得所有分析运算（如微分、积分交换次序等）都是适定的。**Schwartz 空间**，记作 $\mathcal{S}(\mathbb{R}^n)$，正是为此而生。

#### 定义与约定

对于 $\mathbb{R}^n$ 上的一个函数 $f$，其傅里叶变换 $\widehat{f}$（或 $\mathcal{F}f$）在根本上是将其分解为不同频率的正弦波分量。傅里叶变换的定义存在多种约定，其差异主要在于常数 $2\pi$ 的位置。在本章中，我们主要采用以下“对称”约定，因为它能使 Plancherel 定理的形式最为简洁：
$$
\widehat{f}(\xi) = \int_{\mathbb{R}^n} f(x) e^{-2\pi i x \cdot \xi} \,dx, \quad \xi \in \mathbb{R}^n
$$
其中 $x \cdot \xi$ 表示 $\mathbb{R}^n$ 中的欧几里得内积。相应地，其逆变换为：
$$
f(x) = \int_{\mathbb{R}^n} \widehat{f}(\xi) e^{2\pi i x \cdot \xi} \,d\xi
$$
这种约定的优点在于，它将所有的归一化因子都“吸收”到了指数的相位中，使得傅里叶变换与其逆变换的公式非常对称，并且在后续的 Plancherel 恒等式中不会出现额外的常数因子 [@problem_id:3069446]。

其他常见的约定包括：
1.  物理学和工程学中常用的约定：$\widehat{f}(\omega) = \int_{\mathbb{R}^n} f(t) e^{-i \omega \cdot t} \,dt$。在这种约定下，逆变换为 $f(t) = \frac{1}{(2\pi)^n} \int_{\mathbb{R}^n} \widehat{f}(\omega) e^{i \omega \cdot t} \,d\omega$。Plancherel 恒等式则变为 $\int |f(t)|^2 dt = \frac{1}{(2\pi)^n} \int |\widehat{f}(\omega)|^2 d\omega$ [@problem_id:3069437]。
2.  另一种“幺正”约定：$\widehat{f}(\xi) = (2\pi)^{-n/2} \int_{\mathbb{R}^n} f(x) e^{-i x \cdot \xi} \,dx$。此约定的傅里叶变换算子 $\mathcal{F}$ 直接就是一个幺正算子，其逆算子 $\mathcal{F}^{-1}$ 形式上与 $\mathcal{F}^*$（伴随算子）一致，但指数项的符号相反 [@problem_id:3069462]。

理解这些约定之间的差异至关重要，因为它们直接影响着微分方程求解、卷积定理以及 Plancherel 定理等核心公式的具体形式。在本章中，除非特别说明，我们将始终遵循第一个给出的对称约定。

#### Schwartz 空间及其在傅里叶变换下的不变性

**Schwartz 空间** $\mathcal{S}(\mathbb{R}^n)$ 被定义为由所有无穷次可微（即 $C^\infty$）的函数 $f: \mathbb{R}^n \to \mathbb{C}$ 构成的集合，这些函数及其所有偏导数在无穷远处的衰减速度都快于任何多项式的倒数。形式上，对于任意多重指标 $\alpha, \beta \in \mathbb{N}_0^n$，其半范数
$$
p_{\alpha,\beta}(f) := \sup_{x \in \mathbb{R}^n} |x^\alpha \partial^\beta f(x)|
$$
都是有限的。其中 $x^\alpha = x_1^{\alpha_1} \cdots x_n^{\alpha_n}$ 且 $\partial^\beta = \partial_{x_1}^{\beta_1} \cdots \partial_{x_n}^{\beta_n}$。高斯函数 $f(x) = e^{-c|x|^2}$（其中 $c>0$）是 Schwartz 函数的典型例子。

Schwartz 空间之所以是研究傅里叶变换的理想场所，是因为傅里叶变换是 $\mathcal{S}(\mathbb{R}^n)$ 上的一个同构映射，即 $\mathcal{F}: \mathcal{S}(\mathbb{R}^n) \to \mathcal{S}(\mathbb{R}^n)$ 是一个双射。这一非凡性质的根源在于傅里叶变换将两种基本运算——微分和乘以多项式——相互转换 [@problem_id:3069431]。

具体来说，我们可以通过在积分号下微分和分部积分来证明这一点。
首先，考虑 $\widehat{f}$ 的导数。由于 $f \in \mathcal{S}(\mathbb{R}^n)$，函数 $x^\beta f(x)$ 对于任意 $\beta$ 都是绝对可积的，这保证了我们可以在积分号下对 $\xi$ 求任意阶导数：
$$
\partial^\beta \widehat{f}(\xi) = \int_{\mathbb{R}^n} \partial^\beta_{\xi} (f(x) e^{-2\pi i x \cdot \xi}) \,dx = \int_{\mathbb{R}^n} (-2\pi i x)^\beta f(x) e^{-2\pi i x \cdot \xi} \,dx = \mathcal{F}((-2\pi i x)^\beta f(x))(\xi)
$$
这个关系表明，$f$ 的多项式加权变成了 $\widehat{f}$ 的微分。由于 $(-2\pi i x)^\beta f(x)$ 仍然是 Schwartz 函数，其傅里叶变换是连续且有界的。这意味着 $\widehat{f}$ 是无穷次可微的。

其次，考虑用 $\xi^\alpha$ 乘以 $\widehat{f}$。利用恒等式 $\xi_j e^{-2\pi i x \cdot \xi} = \frac{i}{2\pi} \frac{\partial}{\partial x_j} e^{-2\pi i x \cdot \xi}$ 和分部积分（由于 $f$ 快速衰减，边界项为零），我们得到：
$$
\xi^\alpha \widehat{f}(\xi) = \mathcal{F}\left( \left(\frac{1}{2\pi i}\right)^{|\alpha|} \partial^\alpha f \right)(\xi)
$$
这个关系表明，$f$ 的微分变成了 $\widehat{f}$ 的多项式加权。

综合这两个关系，我们可以考察 $\widehat{f}$ 的任一半范数：
$$
\sup_{\xi \in \mathbb{R}^n} |\xi^\alpha \partial^\beta \widehat{f}(\xi)| = \sup_{\xi \in \mathbb{R}^n} \left| \mathcal{F}\left( \left(\frac{1}{2\pi i}\right)^{|\alpha|} \partial^\alpha ((-2\pi i x)^\beta f(x)) \right)(\xi) \right|
$$
由于 $f \in \mathcal{S}(\mathbb{R}^n)$，函数 $H(x) = \left(\frac{1}{2\pi i}\right)^{|\alpha|} \partial^\alpha ((-2\pi i x)^\beta f(x))$ 仍然属于 $\mathcal{S}(\mathbb{R}^n)$，因此它必定是 $L^1$ 可积的。利用傅里叶变换的基本估计 $|\widehat{H}(\xi)| \le \|H\|_{L^1}$，我们得出结论：
$$
\sup_{\xi \in \mathbb{R}^n} |\xi^\alpha \partial^\beta \widehat{f}(\xi)| \le \|H\|_{L^1}  \infty
$$
这证明了 $\widehat{f}$ 的所有 Schwartz 半范数都是有限的，故 $\widehat{f} \in \mathcal{S}(\mathbb{R}^n)$。由于 $\mathcal{F}^{-1}$ 具有相似的结构，同样的过程也证明了逆映射也保持 Schwartz 空间。因此，傅里叶变换是 $\mathcal{S}(\mathbb{R}^n)$ 上的一个拓扑同构 [@problem_id:3069431]。

#### 光滑-衰减对偶原理

上述运算性质揭示了傅里叶分析中的一个核心原理：**一个函数的正则性（光滑度）与其傅里叶变换的衰减速度密切相关**。具体而言：
-   **函数越光滑，其傅里叶变换衰减得越快。** 如果一个函数 $f$ 及其直到 $k$ 阶的导数都属于 $L^1(\mathbb{R})$，即 $f \in W^{k,1}(\mathbb{R})$，那么其傅里叶变换满足如下衰减估计 [@problem_id:3069467]：
    $$
    |\widehat{f}(\xi)| \le (2\pi |\xi|)^{-k} \|f^{(k)}\|_{L^1} \quad (\text{for } \xi \neq 0)
    $$
    对于 Schwartz 函数而言，由于它无穷次可微且所有导数都可积，这个结论对任意整数 $k \ge 0$ 都成立。这意味着 $\widehat{f}(\xi)$ 的衰减速度快于任何多项式 $|\xi|^{-k}$ 的倒数，这正是我们所说的**快速衰减**。
-   **函数衰减得越快，其傅里叶变换越光滑。** 反过来，如果 $x f(x) \in L^1(\mathbb{R})$，那么 $\widehat{f}$ 就是连续可微的，并且其导数由下式给出 [@problem_id:3069467]：
    $$
    \partial_\xi \widehat{f}(\xi) = \mathcal{F}(-2\pi i x f(x))(\xi)
    $$
    由于 $x f(x) \in L^1(\mathbb{R})$，根据 Riemann-Lebesgue 引理，其傅里叶变换 $\partial_\xi \widehat{f}(\xi)$ 是一个连续函数。这表明 $\widehat{f}$ 是 $C^1$ 的。这个原理可以推广到高阶：$x^\alpha f(x)$ 的可积性保证了 $\widehat{f}$ 的高阶光滑性。

这种对偶性是傅里叶分析在偏微分方程、信号处理和量子力学等领域中威力巨大的根本原因。

### 从 $L^1$ 到 $L^2$：傅里叶变换的推广

Schwartz 空间为傅里叶变换提供了一个完美的理论框架，但它过于严格，排除了许多在应用中十分重要的函数，例如不连续的方波信号。因此，我们需要将傅里叶变换理论推广到更广泛的函数空间，如 Lebesgue 空间 $L^p(\mathbb{R}^n)$。

#### $L^1$ 理论及其局限性

对于任何**可积函数** $f \in L^1(\mathbb{R}^n)$，其傅里叶变换的定义积分 $\int f(x) e^{-2\pi i x \cdot \xi} dx$ 是绝对收敛的，因此 $\widehat{f}(\xi)$ 是一个定义良好的有界函数。**Riemann-Lebesgue 引理**进一步指出，$\widehat{f}$ 是连续的，并且在无穷远处趋于零，即 $\lim_{|\xi| \to \infty} \widehat{f}(\xi) = 0$。

然而，$L^1$ 理论存在一个根本性的缺陷：**$L^1(\mathbb{R}^n)$ 在傅里叶变换下不是封闭的**。也就是说，一个 $L^1$ 函数的傅里叶变换不一定是 $L^1$ 函数。一个经典的例子可以说明这一点 [@problem_id:3069437]。考虑一维空间中的指示函数 $f(x) = \chi_{[-1, 1]}(x)$，即在 $[-1, 1]$ 上为 $1$，在其他地方为 $0$。这个函数显然属于 $L^1(\mathbb{R})$（其积分为 $2$）。它的傅里叶变换为：
$$
\widehat{f}(\xi) = \int_{-1}^{1} e^{-2\pi i x\xi} dx = \frac{e^{-2\pi i\xi} - e^{2\pi i\xi}}{-2\pi i\xi} = \frac{\sin(2\pi\xi)}{\pi\xi}
$$
这个函数被称为 **sinc 函数**。尽管当 $|\xi| \to \infty$ 时它确实趋于零，但它的衰减速度不够快，导致其绝对值不可积：
$$
\int_{-\infty}^{\infty} \left| \frac{\sin(2\pi\xi)}{\pi\xi} \right| d\xi = \infty
$$
因此，$\widehat{f} \notin L^1(\mathbb{R})$。

这个例子揭示了 $L^1$ 理论的两个主要问题：
1.  **非封闭性**：$\mathcal{F}(L^1) \not\subset L^1$。
2.  **逆变换问题**：傅里叶逆变换的标准定理之一要求 $\widehat{f}$ 本身也是 $L^1$ 函数，以保证逆变换积分 $\int \widehat{f}(\xi) e^{2\pi i x \cdot \xi} d\xi$ 绝对收敛 [@problem_id:3069468]。对于上面例子中的 $f(x) = \chi_{[-1, 1]}(x)$，由于 $\widehat{f} \notin L^1$，我们无法通过绝对收敛积分来恢复原函数。

这些局限性促使我们寻找一个更适合傅里叶变换的舞台，一个在此变换下具有“对称性”或“守恒性”的空间。这个空间就是 $L^2(\mathbb{R}^n)$。

### Plancherel 定理与 $L^2$ 理论

$L^2(\mathbb{R}^n)$ 空间由所有平方可积的函数（的等价类）构成，它是一个 **Hilbert 空间**，其内积定义为：
$$
\langle f, g \rangle = \int_{\mathbb{R}^n} f(x) \overline{g(x)} \,dx
$$
范数（或“能量”）则为 $\|f\|_{L^2} = \sqrt{\langle f, f \rangle} = \left( \int_{\mathbb{R}^n} |f(x)|^2 \,dx \right)^{1/2}$。

$L^2$ 理论的关键在于，尽管对一个任意的 $L^2$ 函数 $f$（它甚至不一定是 $L^1$ 的），其傅里叶变换的定义积分可能不收敛，但我们可以通过一个极限过程来定义它。**Plancherel 定理**正是这一构造的核心。

#### Plancherel 定理的陈述

Plancherel 定理指出，傅里叶变换算子 $\mathcal{F}$，最初定义在 $L^2(\mathbb{R}^n)$ 的一个稠密子空间 $\mathcal{S}(\mathbb{R}^n)$ 上，可以唯一地延拓为整个 $L^2(\mathbb{R}^n)$ 空间上的一个**幺正算子** (unitary operator)。

“幺正”是一个来自 Hilbert 空间理论的深刻概念，它包含以下核心性质：

1.  **等距性 (Isometry)**：算子保持范数不变。对于任意 $f \in L^2(\mathbb{R}^n)$，我们有：
    $$
    \|\widehat{f}\|_{L^2} = \|f\|_{L^2}
    $$
    写成积分形式，这就是著名的 **Plancherel 恒等式**或**能量守恒方程**：
    $$
    \int_{\mathbb{R}^n} |\widehat{f}(\xi)|^2 \,d\xi = \int_{\mathbb{R}^n} |f(x)|^2 \,dx
    $$
    这可以被物理解释为：一个信号在时域（或空域）的总能量等于其在频域的总能量 [@problem_id:3069446] [@problem_id:3069457]。

2.  **内积保持性 (Parseval 恒等式)**：作为等距性的推广，幺正算子保持内积不变。对于任意 $f, g \in L^2(\mathbb{R}^n)$：
    $$
    \langle \widehat{f}, \widehat{g} \rangle = \langle f, g \rangle
    $$
    即
    $$
    \int_{\mathbb{R}^n} \widehat{f}(\xi) \overline{\widehat{g}(\xi)} \,d\xi = \int_{\mathbb{R}^n} f(x) \overline{g(x)} \,dx
    $$
    这个恒等式是 Plancherel 定理最完整的表述 [@problem_id:3069462]。

3.  **可逆性与伴随关系**：作为一个幺正算子，$\mathcal{F}$ 在 $L^2$ 上是可逆的，并且其逆算子等于其 Hilbert 空间中的**伴随算子** (adjoint operator) $\mathcal{F}^*$。即 $\mathcal{F}^{-1} = \mathcal{F}^*$ [@problem_id:3069470]。伴随算子的定义是 $\langle \mathcal{F}f, g \rangle = \langle f, \mathcal{F}^*g \rangle$。结合 Parseval 恒等式 $\langle \mathcal{F}f, \mathcal{F}g \rangle = \langle f, g \rangle$，可以验证 $\mathcal{F}^*$ 的作用确实是计算逆傅里叶变换。

#### $L^2$ 空间中的傅里叶逆变换

Plancherel 定理保证了 $L^2$ 逆变换的存在性，但其收敛方式与通常的积分不同。对于 $f \in L^2(\mathbb{R}^n)$，其傅里叶逆变换通常不是通过一个绝对收敛的积分来计算的（因为 $\widehat{f}$ 可能不在 $L^1$ 中），而是作为一个**在 $L^2$ 范数下的极限**来理解 [@problem_id:3069468]：
$$
f = \lim_{R \to \infty} \int_{|\xi| \le R} \widehat{f}(\xi) e^{2\pi i x \cdot \xi} \,d\xi \quad (\text{in } L^2(\mathbb{R}^n))
$$
这意味着，截断的傅里叶逆变换积分所构成的函数序列 $f_R(x) = \int_{|\xi| \le R} \widehat{f}(\xi) e^{2\pi i x \cdot \xi} \,d\xi$ 在 $L^2$ 范数下收敛到 $f$，即：
$$
\lim_{R \to \infty} \|f - f_R\|_{L^2} = \lim_{R \to \infty} \left( \int_{\mathbb{R}^n} |f(x) - f_R(x)|^2 \,dx \right)^{1/2} = 0
$$
等式 $\mathcal{F}^{-1}(\mathcal{F}f) = f$ 应该被理解为在 $L^2$ 空间中的相等，即它们代表了同一个等价类。这意味着，我们可以找到 $f$ 的一个代表元 $\tilde{f}$，使得 $(\mathcal{F}^{-1}\widehat{f})(x) = \tilde{f}(x)$ 对于**几乎所有** $x \in \mathbb{R}^n$ 成立 [@problem_id:3069470]。

#### $L^2$ 理论与 $L^1$ 理论的对比

$L^2$ 理论的一个惊人之处在于，它对函数 $\widehat{f}$ 的局部性质（如连续性或点态收敛）提供的保证远少于 $L^1$ 理论。Riemann-Lebesgue 引理保证了 $L^1$ 函数的傅里叶变换是连续的且在无穷远处消失。然而，对于 $L^2$ 函数，这并不成立。

我们可以构造一个函数 $\widehat{f} \in L^2(\mathbb{R})$，它在无穷远处不趋于零。例如，考虑一系列在整数点 $n$ 附近宽度递减、高度为 $1$ 的不相交的矩形脉冲之和 [@problem_id:3069451]：
$$
\widehat{f}(\xi) = \sum_{n=1}^{\infty} \mathbf{1}_{[n-\delta_n, n+\delta_n]}(\xi), \quad \text{with} \quad \delta_n = \frac{1}{4n^2}
$$
这个函数的 $L^2$ 范数的平方是 $\int |\widehat{f}(\xi)|^2 d\xi = \sum 2\delta_n = \sum \frac{1}{2n^2} = \frac{\pi^2}{12}  \infty$，因此 $\widehat{f} \in L^2(\mathbb{R})$。根据 Plancherel 定理，存在一个 $f \in L^2(\mathbb{R})$ 以此为傅里叶变换。然而，对于任意整数 $n$，$\widehat{f}(n) = 1$。这意味着 $\limsup_{|\xi|\to\infty} |\widehat{f}(\xi)| = 1$，$\widehat{f}$ 根本没有在无穷远处消失。

这个例子鲜明地说明了 $L^1$ 和 $L^2$ 理论的区别：
-   $f \in L^1 \implies \widehat{f}$ 连续且在无穷远处消失（点态）。
-   $f \in L^2 \implies \widehat{f} \in L^2$。这只保证了 $\widehat{f}$ 在无穷远处的“平均”衰减（因为其平方可积），但并不保证其点态行为。

### 几何与分布视角

最后，我们从两个更抽象的视角来审视傅里叶变换，以揭示其更深层次的结构。

#### 几何解释：旋转不变性

Plancherel 恒等式表明傅里叶变换保持了 $L^2$ 范数，这是一种能量守恒。这个性质与空间中的几何变换（如旋转）有着深刻的联系。

考虑一个正交矩阵 $R \in O(n)$（代表一个旋转或反射）。如果我们将一个函数 $f(x)$ 旋转，得到 $g(x) = f(Rx)$，那么它的傅里叶变换会如何变化？通过在积分中做变量替换 $y=Rx$，并利用正交变换保持内积 ($x \cdot \xi = R^{-1}y \cdot \xi = y \cdot R\xi$) 和测度 ($|det(R)|=1$) 的性质，我们得到一个优美的关系 [@problem_id:3069457]：
$$
\widehat{g}(\xi) = \widehat{f(Rx)}(\xi) = \widehat{f}(R\xi)
$$
这意味着，**对函数进行旋转，等价于对其傅里叶变换进行相同的旋转**。

结合 Plancherel 定理，这导出了一个关于能量在频域中分布的几何性质。由于正交变换保持测度，我们有：
$$
\int_{\mathbb{R}^n} |\widehat{f}(R\xi)|^2 d\xi = \int_{\mathbb{R}^n} |\widehat{f}(\eta)|^2 d\eta = \int_{\mathbb{R}^n} |\widehat{f}(\xi)|^2 d\xi
$$
这表明，一个信号的频谱能量在频域中的分布是**旋转不变的** [@problem_id:3069457]。无论我们如何旋转坐标系来观察频谱，其总能量始终不变。值得注意的是，这个不变性对于非正交的一般可逆线性变换 $A$ 不成立，除非 $|det(A)|=1$。

#### 分布理论：推广到广义函数

傅里叶变换的最终极、最强大的形式体现在**缓增广义函数 (tempered distributions)** 的理论中，记为 $\mathcal{S}'(\mathbb{R}^n)$。这个空间是 Schwartz 空间的连续对偶空间，包含了像 Dirac delta 函数 $\delta_a$ 这样的“理想化”对象，它们本身不是传统意义上的函数。

傅里叶变换可以通过对偶性自然地从 $\mathcal{S}(\mathbb{R}^n)$ 推广到 $\mathcal{S}'(\mathbb{R}^n)$。对于一个缓增广义函数 $T \in \mathcal{S}'(\mathbb{R}^n)$，其傅里叶变换 $\widehat{T}$ 被定义为这样一个广义函数，它作用于任何检验函数 $\varphi \in \mathcal{S}(\mathbb{R}^n)$ 的结果如下 [@problem_id:3069466]：
$$
\langle \widehat{T}, \varphi \rangle := \langle T, \widehat{\varphi} \rangle
$$
这个定义优雅地将傅里叶变换算子从检验函数“转移”到了广义函数上。在这个框架下，傅里叶变换成为 $\mathcal{S}'(\mathbb{R}^n)$ 上的一个同构，并且许多经典的运算规则以更普遍的形式得以保留。

-   **微分法则**：微分与多项式乘法之间的对偶关系完美地延续到了分布领域：
    $$
    \widehat{\partial^\alpha T} = (2\pi i \xi)^\alpha \widehat{T}
    $$

-   **经典例子的新诠释**：分布理论为一些经典的傅里叶变换对提供了严格的数学基础。例如，位于原点的 Dirac delta 函数 $\delta_0$（定义为 $\langle \delta_0, \varphi \rangle = \varphi(0)$）的傅里叶变换是常数函数 $1$：
    $$
    \langle \widehat{\delta_0}, \varphi \rangle = \langle \delta_0, \widehat{\varphi} \rangle = \widehat{\varphi}(0) = \int_{\mathbb{R}^n} \varphi(x) dx = \langle 1, \varphi \rangle
    $$
    因此，$\widehat{\delta_0} = 1$。反之，常数函数 $1$ 的傅里叶变换是 Dirac delta 函数 $\delta_0$（乘以一个常数，具体取决于约定）。这完美体现了“极端局部化”（$\delta_0$）和“极端非局部化”（常数函数）之间的对偶性。

-   **逆变换**：在分布理论中，两次傅里叶变换的结果是反射，而非恒等。即 $\widehat{\widehat{T}} = T_{\mathcal{R}}$，其中 $T_{\mathcal{R}}$ 是 $T$ 的反射，定义为 $\langle T_{\mathcal{R}}, \varphi \rangle = \langle T, \varphi(-\cdot) \rangle$ [@problem_id:3069466]。

通过将傅里叶变换推广到广义函数，我们不仅能够处理像点源和平面波这样的物理理想模型，而且还获得了一个在数学上极为优美和强大的运算框架。