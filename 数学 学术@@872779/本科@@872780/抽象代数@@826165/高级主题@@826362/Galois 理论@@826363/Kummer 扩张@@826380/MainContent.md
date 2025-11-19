## 引言
库默尔扩张是抽象代数，特别是伽罗瓦理论中的一块基石。它在域扩张的[代数结构](@entry_id:137052)与群论的对称性之间架起了一座具体而优美的桥梁。这一理论的核心贡献在于，它为一类重要的[域扩张](@entry_id:153187)——[阿贝尔扩张](@entry_id:152984)——提供了清晰、可构造的描述，从而解决了如何显式地理解和构建这些扩张的难题。通过将抽象的伽罗瓦群与基域中具体的元素（[单位根](@entry_id:143302)）联系起来，[库默尔理论](@entry_id:154912)不仅深化了我们对[代数结构](@entry_id:137052)本身的理解，还为其他数学分支提供了强有力的分析工具。

本文将系统地引导您深入库默尔扩张的世界。在第一章“原理与机制”中，我们将从基本定义出发，剖析库默尔扩张的核心条件、伽罗瓦群的结构，并学习如何通过拉格朗日[预解式](@entry_id:199555)从[循环群](@entry_id:138668)构造出[根式扩张](@entry_id:150072)。接下来的“应用与跨学科联系”一章将展示该理论如何在伽罗瓦理论、数论和[代数几何](@entry_id:156300)等领域大放异彩，解决从方程可解性到数域算术的诸多问题。最后，在“动手实践”部分，您将通过解决一系列精心设计的问题，将理论知识转化为实际的计算和证明能力，从而真正掌握[库默尔理论](@entry_id:154912)的精髓。

## 原理与机制

在本章中，我们将深入探讨库默尔扩张的基本原理和内在机制。我们将从其严格定义出发，阐明一个[域扩张](@entry_id:153187)成为库默尔扩张的核心条件。随后，我们将剖析这类扩张的典型例子——[根式扩张](@entry_id:150072)，并揭示其伽罗瓦群的独特结构。这一分析将引出[库默尔理论](@entry_id:154912)的核心内容：伽罗瓦群与基域中元素的乘法群之间深刻的对偶关系。我们还将探讨如何确定库默尔[扩张的次数](@entry_id:151271)，并最终展示其逆定理的[构造性证明](@entry_id:157587)，即如何将一个循环扩张显式地表达为[根式扩张](@entry_id:150072)。

### 库默尔扩张的定义与条件

一个域扩张 $L/K$ 被称为 **库默尔扩张 (Kummer extension)**，需满足以下两个条件：
1.  基域 $K$ 包含一个本原 $n$ 次[单位根](@entry_id:143302) $\zeta_n$，其中 $n \gt 1$ 是一个正整数。本原 $n$ 次[单位根](@entry_id:143302)是指满足 $\zeta_n^n = 1$ 但对所有 $0 \lt k \lt n$ 都有 $\zeta_n^k \neq 1$ 的元素。这个条件意味着 $K$ 中包含了由所有 $n$ 次[单位根](@entry_id:143302)构成的循环群 $\mu_n = \{1, \zeta_n, \zeta_n^2, \dots, \zeta_n^{n-1}\}$。
2.  扩张 $L/K$ 是一个伽罗瓦扩张，且其伽罗瓦群 $\text{Gal}(L/K)$ 是一个[阿贝尔群](@entry_id:150284)，其指数（exponent）整除 $n$。[群的指数](@entry_id:145655)是指群中所有[元素的阶](@entry_id:145276)（order）的[最小公倍数](@entry_id:140942)。

除了这两个核心定义外，还有一个至关重要的前提条件，它通常在[库默尔理论](@entry_id:154912)的叙述中被明确要求：基域 $K$ 的特征（characteristic）不整除 $n$，记作 $\text{char}(K) \nmid n$。对于我们常见的特征为 0 的域（如有理数域 $\mathbb{Q}$、实数域 $\mathbb{R}$、复数域 $\mathbb{C}$），这个条件永远成立。然而，在[有限域](@entry_id:142106)等特征为素数 $p$ 的情况下，这个条件则排除了 $n$是 $p$ 的倍数的情形。

这个特征条件为何如此关键？让我们考虑多项式 $f(x) = x^n - a$。其导数为 $f'(x) = nx^{n-1}$。一个多项式是可分的（separable），即在[代数闭包](@entry_id:151964)中没有重根，当且仅当它与其导数互素。如果 $\text{char}(K) \mid n$，那么在域 $K$ 中 $n=0$，导致 $f'(x)$ 恒为零。这意味着 $f(x)$ 与 $f'(x)$ 有非平凡的公因子，从而 $f(x)$ 是不可分的。例如，在特征为 $p$ 的域 $K$ 中，若 $a$ 不是 $K$ 中任何元素的 $p$ 次幂，则多项式 $x^p - a$ 是不可约的。然而，由于 Freshman's Dream 法则，我们有 $(x-\alpha)^p = x^p - \alpha^p = x^p - a$，其中 $\alpha$ 是 $a$ 的一个 $p$ 次根。这表明 $x^p - a$ 在其[分裂域](@entry_id:151552)中只有一个根 $\alpha$，但其[重数](@entry_id:136466)为 $p$。这样的扩张是纯不可分的（purely inseparable），而非伽罗瓦扩张所要求的[可分扩张](@entry_id:150569)。因此，$\text{char}(K) \nmid n$ 的条件确保了我们所研究的核心多项式是可分的，这是伽罗瓦理论得以应用的基础 [@problem_id:1807094]。

### [根式扩张](@entry_id:150072)：典型的库默尔扩张

[库默尔理论](@entry_id:154912)最直接的应用体现在形如 $L = K(\sqrt[n]{a})$ 的 **[根式扩张](@entry_id:150072)** 中，其中 $a$ 是基域 $K$ 中的一个非零元。这里的 $\sqrt[n]{a}$ 表示多项式 $x^n - a$ 的任意一个根。[库默尔理论](@entry_id:154912)的一个基本结论是：

**定理**：设 $K$ 是一个包含本原 $n$ 次[单位根](@entry_id:143302) $\zeta_n$ 的域，且 $\text{char}(K) \nmid n$。对于任意 $a \in K^\times$（$K$ 的乘法群），扩张 $L = K(\sqrt[n]{a})$ 是一个循环伽罗瓦扩张，其次数 $[L:K]$ 整除 $n$。

这个定理完美地说明了为何这类[根式扩张](@entry_id:150072)是库默尔扩张的原型。让我们分析其背后的原因：
1.  **正规性 (Normality)**：扩张 $L/K$ 是多项式 $p(x) = x^n - a$ 的[分裂域](@entry_id:151552)。为什么？因为 $p(x)$ 的根为 $\sqrt[n]{a}, \zeta_n\sqrt[n]{a}, \zeta_n^2\sqrt[n]{a}, \dots, \zeta_n^{n-1}\sqrt[n]{a}$。由于我们假设了 $\zeta_n \in K$，一旦我们在 $K$ 中添加了其中一个根 $\sqrt[n]{a}$，所有其他的根（它们都是 $\sqrt[n]{a}$ 与 $K$ 中元素的乘积）也自动地包含在 $K(\sqrt[n]{a})$ 中了。因此，$L = K(\sqrt[n]{a})$ 是 $p(x)$ 的[分裂域](@entry_id:151552)，这意味着 $L/K$ 是一个[正规扩张](@entry_id:156398) [@problem_id:1807114]。

2.  **可分性 (Separability)**：由于 $\text{char}(K) \nmid n$，$p(x) = x^n - a$ 是可分的，因为它的所有根 $\zeta_n^k\sqrt[n]{a}$ 都是互不相同的。

3.  **伽罗瓦扩张**：一个既正规又可分的扩张就是伽罗瓦扩张。

4.  **阿贝尔伽罗瓦群**：我们将在下一节详细证明，其伽罗瓦群不仅是阿贝尔的，而且是循环的。

要应用这个定理，关键是检验基域 $K$ 是否包含所需的[单位根](@entry_id:143302)。这常常是判断一个扩张是否为库默尔扩张的首要步骤。

**例 1**：考虑扩张 $\mathbb{Q}(\omega, \sqrt{5}) / \mathbb{Q}(\omega)$，其中 $\omega$ 是一个本原 3 次[单位根](@entry_id:143302)。我们可以将其视为 $L/K$，其中 $K=\mathbb{Q}(\omega)$，$L = K(\sqrt{5})$。这是一个 $n=2$ 的[根式扩张](@entry_id:150072)。要使其成为库默尔扩张，基域 $K$ 必须包含本原 2 次单位根，即 $-1$。由于 $\mathbb{Q}(\omega)$ 是一个域，它包含了 $\mathbb{Q}$，因此必然包含 $-1$。所有条件都满足，故这是一个库默尔扩张 [@problem_id:1807135]。

**例 2**：考虑扩张 $\mathbb{C}/\mathbb{R}$。我们可以写成 $\mathbb{C} = \mathbb{R}(i) = \mathbb{R}(\sqrt{-1})$。这是一个 $n=2, a=-1$ 的[根式扩张](@entry_id:150072)。基域 $\mathbb{R}$ 包含本原 2 次[单位根](@entry_id:143302) $-1$。因此，$\mathbb{C}/\mathbb{R}$ 是一个库默尔扩张。其伽罗瓦群为 $\{\text{id}, \text{conjugation}\} \cong \mathbb{Z}/2\mathbb{Z}$，是阶为 2 的循环群 [@problem_id:1807135]。

**反例 1**：扩张 $\mathbb{Q}(\sqrt[3]{7})/\mathbb{Q}$ 是否为库默尔扩张？这里 $n=3$。要成为库默尔扩张，基域 $\mathbb{Q}$ 必须包含本原 3 次单位根 $\omega = \frac{-1+i\sqrt{3}}{2}$。显然，$\mathbb{Q}$ 是实数域的[子域](@entry_id:155812)，不包含非实数的 $\omega$。因此，尽管该扩张由一个根式生成，但它不是一个库默尔扩张 [@problem_id:1807095]。事实上，$\mathbb{Q}(\sqrt[3]{7})$ 甚至不是一个伽罗瓦扩张，因为它不包含 $x^3-7$ 的另外两个[复根](@entry_id:172941) $\omega\sqrt[3]{7}$ 和 $\omega^2\sqrt[3]{7}$。其[分裂域](@entry_id:151552) $\mathbb{Q}(\omega, \sqrt[3]{7})$ 的伽罗瓦群是 $S_3$，一个非阿贝尔群 [@problem_id:1807097]。

### 伽罗瓦群的结构与库默尔对应

[库默尔理论](@entry_id:154912)最精妙之处在于它精确地描述了[根式扩张](@entry_id:150072) $L = K(\sqrt[n]{a})$ 的伽罗瓦群结构。设 $\sigma \in \text{Gal}(L/K)$ 是一个 $K$-[自同构](@entry_id:155390)。
-   由于 $\sigma$ 保持 $K$ 中元素不变，我们有 $\sigma(a)=a$。
-   令 $\alpha = \sqrt[n]{a}$。将 $\sigma$ 作用于方程 $\alpha^n = a$ 的两边，我们得到 $\sigma(\alpha^n) = \sigma(a)$，即 $(\sigma(\alpha))^n = a$。
-   这表明 $\sigma(\alpha)$ 也必须是多项式 $x^n - a$ 的一个根。
-   如前所述， $x^n-a$ 的所有根的形式为 $\zeta_n^k \alpha$。因此，对于任意的 $\sigma \in \text{Gal}(L/K)$，必然存在一个整数 $k$ (依赖于 $\sigma$)，使得 $\sigma(\alpha) = \zeta_n^k \alpha$。
-   这里的 $\zeta_n^k$ 是 $K$ 中的一个元素。这个 $n$ 次单位根 $\zeta_n^k$ 完全由[自同构](@entry_id:155390) $\sigma$ 决定。

这启发我们定义一个映射：
$$ \phi: \text{Gal}(L/K) \to \mu_n $$
其定义为 $\phi(\sigma) = \frac{\sigma(\alpha)}{\alpha}$。

这个映射 $\phi$ 具有非凡的性质：
1.  **它是一个[群同态](@entry_id:140603)**：对于任意 $\sigma, \tau \in \text{Gal}(L/K)$，
    $$ (\sigma \circ \tau)(\alpha) = \sigma(\tau(\alpha)) = \sigma(\phi(\tau)\alpha) = \phi(\tau)\sigma(\alpha) = \phi(\tau)\phi(\sigma)\alpha = (\phi(\sigma)\phi(\tau))\alpha $$
    因此，$\phi(\sigma \circ \tau) = \phi(\sigma)\phi(\tau)$。

2.  **它是[单射](@entry_id:183792)的 (injective)**：如果 $\phi(\sigma) = 1$，那么 $\sigma(\alpha) = 1 \cdot \alpha = \alpha$。由于 $L=K(\alpha)$，一个固定了基域 $K$ 和生成元 $\alpha$ 的[自同构](@entry_id:155390)必然是恒等[自同构](@entry_id:155390)，即 $\sigma = \text{id}$。因此，$\phi$ 的核是平凡的。

根据群论的基本[同构定理](@entry_id:145702)，$\text{Gal}(L/K)$ 同构于 $\mu_n$ 的一个[子群](@entry_id:146164)。因为 $\mu_n$ 是一个 $n$ 阶循环群，它的任何[子群](@entry_id:146164)也都是循环群。这证明了 $\text{Gal}(L/K)$ 是一个循环群，其阶数整除 $n$。这就是为什么库默尔扩张的伽罗瓦群是阿贝尔的（实际上是循环的）根本原因 [@problem_id:1807097]。

这个同构关系 $\phi$ 是[库默尔理论](@entry_id:154912)的核心机制。它在伽罗瓦群的抽象元素 $\sigma$ 与基域中具体的[单位根](@entry_id:143302) $\phi(\sigma)$ 之间建立了一座桥梁。

**例 3**：设 $K=\mathbb{Q}(\omega)$，$L=K(\sqrt[3]{7})$。这是一个 $n=3$ 的库默尔扩张。其伽罗瓦群 $G=\text{Gal}(L/K)$ 同构于 $\mu_3 = \{1, \omega, \omega^2\}$。同构 $\phi: G \to \mu_3$ 由 $\sigma(\sqrt[3]{7}) = \phi(\sigma)\sqrt[3]{7}$ 定义。如果我们考虑与 $\omega$ 对应的那个[自同构](@entry_id:155390) $\sigma_\omega$，那么 $\phi(\sigma_\omega) = \omega$。这意味着 $\sigma_\omega$ 的作用是 $\sigma_\omega(\sqrt[3]{7}) = \omega\sqrt[3]{7}$。由于 $\sigma_\omega$ 是 $K$-自同构，它固定 $K$ 中的所有元素，例如 $\sigma_\omega(3)=3$ 和 $\sigma_\omega(\omega)=\omega$。利用[自同构](@entry_id:155390)的性质，我们可以计算它对 $L$ 中任意元素的作用：
$$ \sigma_\omega(\sqrt[3]{7} - 3\omega) = \sigma_\omega(\sqrt[3]{7}) - \sigma_\omega(3\omega) = \omega\sqrt[3]{7} - \sigma_\omega(3)\sigma_\omega(\omega) = \omega\sqrt[3]{7} - 3\omega $$
这个具体的计算过程清晰地展示了伽罗瓦群成员如何通过与单位根相乘来作用于被添加的根 [@problem_id:1807129]。

### 扩张次数的确定

我们已经知道 $[K(\sqrt[n]{a}):K]$ 整除 $n$。但它具体等于多少呢？[扩张的次数](@entry_id:151271)等于伽罗瓦[群的阶](@entry_id:137115)，也就是同构映射 $\phi$ 的像群的大小。这个次数 $d = [K(\sqrt[n]{a}):K]$ 与元素 $a$ 在商群 $K^\times / (K^\times)^n$ 中的性质密切相关。其中 $(K^\times)^n = \{b^n \mid b \in K^\times\}$ 是 $K$ 中所有非零元素的 $n$ 次幂构成的群。

**定理**：设 $K$ 是一个包含 $\zeta_n$ 的域，且 $\text{char}(K) \nmid n$。扩张 $L = K(\sqrt[n]{a})$ 的次数 $d = [L:K]$ 是元素 $a$ 在商群 $K^\times / (K^\times)^n$ 中所代表的[陪集](@entry_id:147145)（coset）的阶。也就是说，$d$ 是满足 $a^d \in (K^\times)^n$ 的最小正整数。

这个定理在实践中可能不易直接使用。一个更具操作性的判据如下：扩张次数 $d$ 是整除 $n$ 的最小正整数，使得 $x^d-a$ 在 $K$ 中是可约的。然而，最实用的方法往往是分析 $a$ 是否为 $K$ 中某些[元素的幂](@entry_id:143058)。

**例 4**：设 $K = \mathbb{Q}(\omega)$，其中 $\omega$ 是本原 3 次[单位根](@entry_id:143302)。该域也包含了本原 6 次[单位根](@entry_id:143302) $\zeta_6 = 1+\omega$。我们来确定扩张 $L=K(\sqrt[6]{a})$ 的次数，其中 $a$ 是 $K$ 中的元素。我们想知道对于哪些 $a$，扩张次数恰好为 3 [@problem_id:1807085]。

扩张次数为 3 意味着 $L/K$ 是一个 3 次循环扩张。这相当于 $L$ 可以被写成 $K(\sqrt[3]{b})$ 的形式，其中 $b$ 不是 $K$ 中的立方数。由于 $L=K(\sqrt[6]{a})$，这意味着 $K(\sqrt[6]{a}) = K(\sqrt[3]{b})$。
-   如果 $a$ 是 $K$ 中的一个[平方数](@entry_id:635622)，即 $a=c^2$ 对于某个 $c \in K^\times$，那么 $L=K(\sqrt[6]{c^2}) = K(\sqrt[3]{c})$。只要 $c$ 不是 $K$ 中的立方数，这个[扩张的次数](@entry_id:151271)就是 3（因为它大于 1 且整除 3）。
-   反过来，如果扩张次数为 3，那么伽罗瓦群是 $\mu_6$ 中唯一的 3 阶[子群](@entry_id:146164)，即 $\mu_3=\{1, \omega, \omega^2\}$。这意味着 $(\sigma(\alpha)/\alpha)^3=1$ 对所有 $\sigma$ 成立，其中 $\alpha=\sqrt[6]{a}$。这导出 $\sigma(\alpha^2) = \alpha^2$，即 $\alpha^2 = \sqrt[3]{a}$ 被伽罗瓦群的所有元素固定，因此 $\sqrt[3]{a} \in K$。这意味着 $a$ 是 $K$ 中的一个立方数。这与我们的期望相悖。

让我们重新审视逻辑。扩张次数 $d$ 是 $|\text{Gal}(L/K)|$。这个[群同构](@entry_id:147371)于 $\mu_n$ 的一个[子群](@entry_id:146164)。如果次数为 3（在 $n=6$ 的情况下），这个[子群](@entry_id:146164)必须是 $\mu_3$。这意味着 $\sigma(\alpha) = \omega^k \alpha$。那么 $\sigma(\alpha^2) = (\omega^k \alpha)^2 = \omega^{2k} \alpha^2 \neq \alpha^2$。但是 $\sigma(\alpha^3) = (\omega^k \alpha)^3 = (\omega^3)^k \alpha^3 = \alpha^3$。这意味着 $\alpha^3 = \sqrt{a}$ 被伽罗瓦群固定，所以 $\sqrt{a} \in K$。因此，$a$ 必须是 $K$ 中的一个平方数。
结合这两个观察，我们得到一个清晰的判据：对于 $n=6$ 的情形，$L=K(\sqrt[6]{a})$ 的次数为 3，当且仅当 $a$ 是 $K^\times$ 中的一个平方数但不是一个立方数。

让我们用这个判据来检验几个例子：
-   $a=4$：由于 $4=2^2$，它在 $K$ 中是[平方数](@entry_id:635622)。由于 $2$ 在 $K = \mathbb{Q}(\omega)$ 中是素元，它的因子分解中 $2$ 的指数是 1，不能被 3 整除，所以 $2$ 不是立方数，$4=2^2$ 也不是立方数。因此 $[K(\sqrt[6]{4}):K]=3$。
-   $a=\omega$：在 $K$ 中，$\omega$ 是一个单位根。它是[平方数](@entry_id:635622)吗？是的，因为 $\zeta_6^2 = (1+\omega)^2=1+2\omega+\omega^2=1+2\omega+(-1-\omega)=\omega$。它是立方数吗？不是，因为 $K$ 中的[单位根](@entry_id:143302)的立方只能是 $1$ 或 $-1$。所以 $[K(\sqrt[6]{\omega}):K]=3$ [@problem_id:1807085]。

### 逆定理：从循环扩张到[根式扩张](@entry_id:150072)

[库默尔理论](@entry_id:154912)的另一半内容是其逆定理，它断言任何满足条件的循环扩张都必定是[根式扩张](@entry_id:150072)。

**逆定理 (Kummer's Theorem)**：设 $K$ 是一个包含本原 $n$ 次单位根 $\zeta_n$ 的域，且 $\text{char}(K) \nmid n$。如果 $L/K$ 是一个 $n$ 次循环伽罗瓦扩张，那么存在某个元素 $a \in K$，使得 $L = K(\sqrt[n]{a})$。

这个定理是一个强大的存在性结论。更重要的是，其证明是构造性的，它提供了一种方法来找到所需的元素 $a$。这个构造依赖于一种称为 **拉格朗日[预解式](@entry_id:199555) (Lagrange resolvent)** 的特殊元素，其思想可追溯至希尔伯特第九十定理。

设 $\sigma$ 是循环伽罗瓦群 $\text{Gal}(L/K)$ 的一个生成元，其阶为 $n$。根据正规基定理，存在一个元素 $\theta \in L$，使得其伽罗瓦[轨道](@entry_id:137151) $\{\theta, \sigma(\theta), \sigma^2(\theta), \dots, \sigma^{n-1}(\theta)\}$ 构成 $L$ 作为 $K$-[向量空间](@entry_id:151108)的一组基。我们利用这个 $\theta$ 和[单位根](@entry_id:143302) $\zeta_n$ 来构造拉格朗日[预解式](@entry_id:199555) $\alpha$：
$$ \alpha = \theta + \zeta_n^{-1}\sigma(\theta) + \zeta_n^{-2}\sigma^2(\theta) + \dots + \zeta_n^{-(n-1)}\sigma^{n-1}(\theta) = \sum_{k=0}^{n-1} \zeta_n^{-k}\sigma^k(\theta) $$
这个构造的巧妙之处在于 $\alpha$ 对 $\sigma$ 的作用具有非常简单的形式。让我们来计算 $\sigma(\alpha)$：
$$ \sigma(\alpha) = \sum_{k=0}^{n-1} \zeta_n^{-k}\sigma^{k+1}(\theta) $$
令 $j=k+1$，并利用 $\sigma^n = \text{id}$ 和 $\zeta_n^{-n}=1$，我们得到：
$$ \sigma(\alpha) = \sum_{j=1}^{n} \zeta_n^{-(j-1)}\sigma^j(\theta) = \zeta_n \sum_{j=1}^{n} \zeta_n^{-j}\sigma^j(\theta) = \zeta_n \left( \sum_{j=0}^{n-1} \zeta_n^{-j}\sigma^j(\theta) \right) = \zeta_n \alpha $$
这个结果 $\sigma(\alpha) = \zeta_n \alpha$ 是关键。它表明 $\alpha$ 是 $\sigma$ 作用下的一个“[特征向量](@entry_id:151813)”，其“[特征值](@entry_id:154894)”是单位根 $\zeta_n$。由于 $\zeta_n \neq 1$，我们知道 $\sigma(\alpha) \neq \alpha$，这意味着 $\alpha \notin K$。

现在考虑元素 $\alpha^n$。将其在 $\sigma$ 下的像计算出来：
$$ \sigma(\alpha^n) = (\sigma(\alpha))^n = (\zeta_n \alpha)^n = \zeta_n^n \alpha^n = 1 \cdot \alpha^n = \alpha^n $$
这意味着 $\alpha^n$ 被伽罗瓦[群的生成元](@entry_id:137215) $\sigma$ 固定，因此它被整个伽罗瓦群固定。根据[伽罗瓦理论基本定理](@entry_id:149647)，被整个伽罗瓦群固定的元素必然属于基域 $K$。因此，我们找到了一个元素 $a = \alpha^n \in K$。

我们已经构造了一个元素 $\alpha \in L \setminus K$，其 $n$ 次幂 $a = \alpha^n$ 在 $K$ 中。这表明 $K(\alpha)$ 是 $L$ 的一个子扩张。$K(\alpha)/K$ 的伽罗瓦群是循环的，由 $\alpha \mapsto \zeta_n \alpha$ 生成，其阶为 $n$。因此 $[K(\alpha):K]=n$。由于 $K(\alpha) \subseteq L$ 且 $[L:K]=n$，我们必然有 $L=K(\alpha) = K(\sqrt[n]{a})$。

**例 5**：设 $K = \mathbb{Q}(i)$，它包含本原 4 次[单位根](@entry_id:143302) $i$。考虑扩张 $L = K(\beta)$，其中 $\beta$ 是多项式 $x^4+8=0$ 的一个根。已知这是一个 4 次循环扩张，其伽罗瓦群的一个生成元 $\sigma$ 满足 $\sigma(\beta)=i\beta$。我们来构造使 $L = K(\sqrt[4]{a})$ 成立的元素 $a$ [@problem_id:1807089]。
我们选择一个简单的元素 $\theta = 1+\beta \in L$。本原 4 次单位根是 $i$，我们需要 $\zeta_4^{-1} = -i$。构造拉格朗日[预解式](@entry_id:199555)：
$$ \alpha = \theta + (-i)\sigma(\theta) + (-i)^2\sigma^2(\theta) + (-i)^3\sigma^3(\theta) $$
我们有 $\sigma^k(\theta) = \sigma^k(1+\beta) = 1 + \sigma^k(\beta) = 1 + i^k\beta$。代入得：
$$ \alpha = (1+\beta) - i(1+i\beta) - (1+i^2\beta) + i(1+i^3\beta) $$
$$ \alpha = (1-i-1+i) + (1 - i(i) - (i^2) + i(i^3))\beta = 0 + (1+1+1+1)\beta = 4\beta $$
我们找到了[预解式](@entry_id:199555) $\alpha = 4\beta$。现在计算 $a = \alpha^4$：
$$ a = (4\beta)^4 = 4^4 \beta^4 = 256(-8) = -2048 $$
这个 $a = -2048$ 确实是 $K = \mathbb{Q}(i)$ 中的元素。因此，我们验证了 $L=K(\beta)=K(\sqrt[4]{-2048})$，成功地将一个给定的循环扩张表示成了[根式扩张](@entry_id:150072)。

最后值得注意的是，这种表示不是唯一的。如果 $L = K(\sqrt[n]{a})$，那么对于任何 $c \in K^\times$，扩张 $K(\sqrt[n]{ac^n}) = K(c\sqrt[n]{a}) = K(\sqrt[n]{a})$ 是同一个域。因此，能够生成同一扩张的元素 $a$ 和 $a'$，它们在商群 $K^\times / (K^\times)^n$ 中属于同一个陪集 [@problem_id:1807106]。

综上所述，[库默尔理论](@entry_id:154912)在包含[单位根](@entry_id:143302)的基域上，为[阿贝尔扩张](@entry_id:152984)（特别是循环扩张）与[根式扩张](@entry_id:150072)之间建立了一座坚实的桥梁。它不仅阐明了伽罗瓦群的结构，还提供了计算扩张次数和从抽象群论描述构造具体[代数元](@entry_id:153893)素的有力工具。