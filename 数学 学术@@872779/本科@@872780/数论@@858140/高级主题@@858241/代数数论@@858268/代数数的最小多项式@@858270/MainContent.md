## 引言
代数数，如 $\sqrt{2}$ 和[黄金分割](@entry_id:139097)比例 $\phi$，是数学中一类迷人而基础的对象。然而，如何系统地捕捉并研究这些数的内在[代数结构](@entry_id:137052)，是一个核心问题。答案的关键在于一个强大的工具——[最小多项式](@entry_id:153598)。它如同一个[代数数](@entry_id:150888)的“数字指纹”，唯一地编码了其所有的代数信息，成为连接数论、[抽象代数](@entry_id:145216)与几何学的桥梁。

本文旨在全面解析代数数的[最小多项式](@entry_id:153598)。我们将从三个层面展开：

首先，在“原理与机制”一章中，我们将从基本定义出发，严格建立[最小多项式](@entry_id:153598)的存在性、唯一性及其不可约性等核心性质，并揭示它与[域扩张](@entry_id:153187)、共轭元、[迹和范数](@entry_id:155207)之间的深刻联系。

接着，在“应用与跨学科联系”一章中，我们将展示这一理论工具的巨大威力，看它如何被用于证明数的无理性、判定几何可作图性，以及系统性地计算和分析[代数数域](@entry_id:637592)的结构。

最后，通过“动手实践”部分提供的精选练习，你将有机会亲手计算和分析最小多项式，将抽象理论转化为解决具体问题的能力。

## 原理与机制

在介绍代数数的基本概念之后，本章将深入探讨其核心工具——最小多项式。我们将从最基本的定义出发，系统地建立最小多项式的存在性、唯一性及其关键性质。通过分析最小多项式与域扩张、共轭元、[迹和范数](@entry_id:155207)等概念之间的深刻联系，我们将揭示其在[代数数论](@entry_id:148067)中的原理和机制。

### [代数元](@entry_id:153893)及其最小多项式的定义

我们从最基础的定义开始。一个复数 $\alpha$ 被称为**代数数** (algebraic number)，如果它是有理[数域](@entry_id:155558) $\mathbb{Q}$ 上的[代数元](@entry_id:153893)，即存在一个非零的、系数在 $\mathbb{Q}$ 中的多项式 $p(x) \in \mathbb{Q}[x]$，使得 $p(\alpha) = 0$。例如，$\sqrt{2}$ 是一个[代数数](@entry_id:150888)，因为它是多项式 $x^2 - 2$ 的根。反之，若不存在这样的多项式，则称该数为**超越数** (transcendental number)，如 $\pi$ 和 $e$。

为了系统地研究代数数 $\alpha$，我们考虑所有以 $\alpha$ 为根的有理系数多项式的集合。这个集合在代数上具有优美的结构。考虑从多项式环 $\mathbb{Q}[x]$ 到包含 $\alpha$ 的域（例如复数域 $\mathbb{C}$）的**[求值同态](@entry_id:153415)** (evaluation homomorphism) $\varphi_\alpha: \mathbb{Q}[x] \to \mathbb{C}$，其定义为 $\varphi_\alpha(p(x)) = p(\alpha)$。这个映射的**核** (kernel)，记为 $\ker(\varphi_\alpha)$，恰好就是所有以 $\alpha$ 为根的 $\mathbb{Q}[x]$ 中多项式的集合：
$$ I_\alpha = \ker(\varphi_\alpha) = \{ p(x) \in \mathbb{Q}[x] \mid p(\alpha) = 0 \} $$
在[环论](@entry_id:143825)中，[同态的核](@entry_id:145895)总是一个**理想** (ideal)。由于 $\alpha$ 是[代数数](@entry_id:150888)，这个理想 $I_\alpha$ 至少包含一个非零多项式，因此它是一个非零理想。

[多项式环](@entry_id:152854) $\mathbb{Q}[x]$ 有一个非常重要的性质：它是一个**[主理想整环](@entry_id:152359)** (Principal Ideal Domain, [PID](@entry_id:174286))。这意味着它的每一个理想都可以由单个元素生成。因此，非零理想 $I_\alpha$ 必然可以写成 $I_\alpha = \langle m(x) \rangle$ 的形式，其中 $m(x)$ 是 $I_\alpha$ 中的一个非零多项式。这个生成元 $m(x)$ 在 $I_\alpha$ 中具有最小的正次数。[@problem_id:3087152]

这个生成元并不是唯一的。任何与 $m(x)$ 相差一个非零常数倍（即 $\mathbb{Q}[x]$ 中的一个单位）的多项式也能生成同一个理想。为了得到一个唯一的代表，我们规定这个生成元必须是**[首一多项式](@entry_id:152311)** (monic polynomial)，即其最高次项系数为 $1$。这个唯一的、首一的、[生成理想](@entry_id:151554) $I_\alpha$ 的多项式，就被定义为 $\alpha$ 在 $\mathbb{Q}$ 上的**最小多项式** (minimal polynomial)，记作 $m_{\alpha,\mathbb{Q}}(x)$。

综上所述，[代数数](@entry_id:150888) $\alpha$ 在 $\mathbb{Q}$ 上的最小多项式 $m_{\alpha,\mathbb{Q}}(x)$ 是满足以下条件的**唯一**多项式 [@problem_id:3087122] [@problem_id:3087161]：
1.  $m_{\alpha,\mathbb{Q}}(x)$ 是一个[首一多项式](@entry_id:152311)，且其系数均为有理数 ($m_{\alpha,\mathbb{Q}}(x) \in \mathbb{Q}[x]$)。
2.  $m_{\alpha,\mathbb{Q}}(\alpha) = 0$。
3.  对于任何满足 $p(\alpha) = 0$ 的多项式 $p(x) \in \mathbb{Q}[x]$，都有 $m_{\alpha,\mathbb{Q}}(x)$ 整除 $p(x)$。

第三个性质，即**[整除性](@entry_id:190902)**，是[最小多项式](@entry_id:153598)最强大的特征之一。它表明，所有湮没 $\alpha$ 的多项式都必须是其最小多项式的倍式。这也意味着最小多项式是所有以 $\alpha$ 为根的有理系数多项式中次数最低的那个。

### [最小多项式](@entry_id:153598)的核心性质

#### 不可约性

[最小多项式](@entry_id:153598)的一个核心性质是它在基域上是**不可约的** (irreducible)。也就是说，$m_{\alpha,\mathbb{Q}}(x)$ 不能被分解为两个次数更低的有理系数多项式的乘积。

我们可以用[反证法](@entry_id:276604)来证明这一点。假设 $m_{\alpha,\mathbb{Q}}(x)$ 在 $\mathbb{Q}[x]$ 中是可约的，即 $m_{\alpha,\mathbb{Q}}(x) = g(x)h(x)$，其中 $g(x)$ 和 $h(x)$ 都是 $\mathbb{Q}[x]$ 中的多项式，且它们的次数都小于 $\deg(m_{\alpha,\mathbb{Q}})$。将 $\alpha$ 代入，我们得到 $m_{\alpha,\mathbb{Q}}(\alpha) = g(\alpha)h(\alpha) = 0$。由于[复数域](@entry_id:153768)是一个[整环](@entry_id:155321)，这意味着 $g(\alpha)=0$ 或 $h(\alpha)=0$。但这与 $m_{\alpha,\mathbb{Q}}(x)$ 是以 $\alpha$ 为根的次数最低的多项式相矛盾。因此，我们的假设不成立，$m_{\alpha,\mathbb{Q}}(x)$ 必须是不可约的。[@problem_id:3087161]

这个性质至关重要，它将一个代数数与一个特定的不[可约多项式](@entry_id:148759)唯一地联系起来。

#### [域扩张的次数](@entry_id:149430)

最小多项式与[域论](@entry_id:155241)中的一个核心概念——**[域扩张的次数](@entry_id:149430)** (degree of a field extension)——紧密相连。给定代数数 $\alpha$，我们可以构造包含 $\mathbb{Q}$ 和 $\alpha$ 的最小的域，记为 $\mathbb{Q}(\alpha)$。这个域可以看作是 $\mathbb{Q}$ 上的一个[向量空间](@entry_id:151108)。这个[向量空间](@entry_id:151108)的维数，记为 $[\mathbb{Q}(\alpha):\mathbb{Q}]$，就是[域扩张的次数](@entry_id:149430)。

一个基础而深刻的定理指出，[域扩张的次数](@entry_id:149430)等于 $\alpha$ 的最小多项式的次数：
$$ [\mathbb{Q}(\alpha):\mathbb{Q}] = \deg(m_{\alpha,\mathbb{Q}}(x)) $$
这个定理的证明思路是构造一个 $\mathbb{Q}(\alpha)$ 在 $\mathbb{Q}$ 上的基。如果设 $n = \deg(m_{\alpha,\mathbb{Q}}(x))$，我们可以证明集合 $\{1, \alpha, \alpha^2, \dots, \alpha^{n-1}\}$ 构成了 $\mathbb{Q}(\alpha)$ 的一个基。任何 $\alpha$ 的更高次幂都可以通过 $m_{\alpha,\mathbb{Q}}(\alpha)=0$ 这个关系式降次，表示为这个基的线性组合。而这个集合的[线性无关](@entry_id:148207)性则源于 $m_{\alpha,\mathbb{Q}}(x)$ 的次数最小性。[@problem_id:3087140]

例如，对于 $\alpha = \sqrt[3]{2}$，我们很快会看到其[最小多项式](@entry_id:153598)是 $x^3-2$，次数为 $3$。因此，域扩张 $[\mathbb{Q}(\sqrt[3]{2}):\mathbb{Q}]$ 的次数为 $3$，并且 $\mathbb{Q}(\sqrt[3]{2})$ 中的任何元素都可以唯一地表示为 $a + b\sqrt[3]{2} + c(\sqrt[3]{2})^2$ 的形式，其中 $a,b,c \in \mathbb{Q}$。

### 最小多项式的计算与判定

理论上，寻找一个[代数数](@entry_id:150888) $\alpha$ 的最小多项式分为两步：
1.  找到一个以 $\alpha$ 为根的首一有理系数多项式 $p(x)$。
2.  证明 $p(x)$ 在 $\mathbb{Q}[x]$ 中是不可约的。

如果成功，那么 $p(x)$ 就是 $m_{\alpha,\mathbb{Q}}(x)$。

#### 对基域的依赖性

一个关键点是，最小多项式是**相对于基域而言的**。改变基域会改变[最小多项式](@entry_id:153598)。

我们以 $\alpha = \sqrt{2}$ 为例。
-   在基域 $F_1 = \mathbb{Q}$ 上，$\sqrt{2}$ 不是有理数。我们发现 $x^2-2$ 是一个以 $\sqrt{2}$ 为根的首一有理系数多项式。我们可以通过**[有理根定理](@entry_id:150684)** (Rational Root Theorem) 证明它在 $\mathbb{Q}$ 上没有根，因此对于一个二次多项式而言，它在 $\mathbb{Q}$ 上是不可约的。所以，$m_{\sqrt{2},\mathbb{Q}}(x) = x^2 - 2$。
-   然而，如果我们将基域扩大到 $F_2 = \mathbb{Q}(\sqrt{2})$，即包含 $\sqrt{2}$ 本身的域，情况就完全不同了。此时，$\alpha = \sqrt{2}$ 已经是基域中的一个元素。多项式 $x - \sqrt{2}$ 的系数 $1$ 和 $-\sqrt{2}$ 都在 $\mathbb{Q}(\sqrt{2})$ 中。这个一次多项式是首一的，以 $\sqrt{2}$ 为根，并且任何一次多项式都是不可约的。因此，$m_{\sqrt{2},\mathbb{Q}(\sqrt{2})}(x) = x - \sqrt{2}$。[@problem_id:3087164]

这个例子清晰地表明，当我们说“最小多项式”时，必须指明是“在哪一个域上的”[最小多项式](@entry_id:153598)。

#### 常用不可约性判别法

在实践中，证明多项式的不可约性是关键步骤。
- **艾森斯坦判别法 (Eisenstein's Criterion)**：对于整系数多项式 $a_n x^n + \dots + a_1 x + a_0$，如果存在一个素数 $p$ 满足：
    1. $p$ 不整除 $a_n$；
    2. $p$ 整除 $a_{n-1}, \dots, a_0$；
    3. $p^2$ 不整除 $a_0$。
  则该多项式在 $\mathbb{Q}$ 上不可约。例如，对于 $x^3-2$，取素数 $p=2$ 即可证明其不可约性。因此，$m_{\sqrt[3]{2},\mathbb{Q}}(x) = x^3 - 2$。[@problem_id:3087140]

- **[有理根定理](@entry_id:150684)**：对于一个 $n$ 次整系数多项式，如果它在 $\mathbb{Q}$ 上可约，那么它必然有一个次数小于 $n$ 的有理系数因式。特别地，对于二次或三次多项式，如果它在 $\mathbb{Q}$ 上没有有理根，那么它一定是不可约的。

#### 复杂[代数数](@entry_id:150888)的计算

对于更复杂的代数数，例如 $\alpha = \sqrt{2} + \sqrt{3}$，寻找其最小多项式需要一些代数技巧。
1.  令 $x = \sqrt{2} + \sqrt{3}$。
2.  平方得 $x^2 = (\sqrt{2} + \sqrt{3})^2 = 2 + 3 + 2\sqrt{6} = 5 + 2\sqrt{6}$。
3.  分离根式项：$x^2 - 5 = 2\sqrt{6}$。
4.  再次平方以消去根式：$(x^2 - 5)^2 = (2\sqrt{6})^2 = 24$。
5.  展开并整理：$x^4 - 10x^2 + 25 = 24 \implies x^4 - 10x^2 + 1 = 0$。

我们得到了一个首一整系数多项式 $p(x) = x^4 - 10x^2 + 1$，它以 $\alpha$ 为根。接下来需要证明其在 $\mathbb{Q}$ 上不可约。可以验证它没有有理根。然后，尝试将其分解为两个二次因式 $(x^2+ax+b)(x^2+cx+d)$，通过比较系数可以发现不存在整数解，根据**[高斯引理](@entry_id:149771) (Gauss's Lemma)**，这也意味着不存在有理数解。因此，$p(x)$ 不可约，即为 $\alpha$ 的[最小多项式](@entry_id:153598) $m_{\sqrt{2}+\sqrt{3}, \mathbb{Q}}(x) = x^4 - 10x^2 + 1$。[@problem_id:3087122]

### 共轭、迹与范数

[最小多项式](@entry_id:153598)的根之间存在着深刻的对称性。

#### 共轭元

给定一个[代数数](@entry_id:150888) $\alpha$ 在域 $F$ 上的最小多项式 $m_{\alpha,F}(x)$，它在一个[代数闭包](@entry_id:151964) $\overline{F}$（例如 $\mathbb{C}$）中的所有根，被称为 $\alpha$ 在 $F$ 上的**共轭元** (conjugates)。[@problem_id:3087138]

例如，$m_{\sqrt{2},\mathbb{Q}}(x) = x^2-2$ 的两个根是 $\sqrt{2}$ 和 $-\sqrt{2}$，所以它们互为在 $\mathbb{Q}$ 上的共轭。$m_{\sqrt[3]{2},\mathbb{Q}}(x) = x^3-2$ 的三个根是 $\sqrt[3]{2}$, $\sqrt[3]{2}e^{2\pi i/3}$, 和 $\sqrt[3]{2}e^{4\pi i/3}$，这三个数互为在 $\mathbb{Q}$ 上的共轭。

从更抽象的角度看，$\alpha$ 在 $F$ 上的共轭元集合是 $\{\sigma(\alpha) \mid \sigma: F(\alpha) \hookrightarrow \overline{F} \text{ 是一个 } F\text{-嵌入}\}$，即所有保持 $F$ 不动的从 $F(\alpha)$ 到 $\overline{F}$ 的域嵌入映射下 $\alpha$ 的像的集合。可以证明，这个集合恰好就是 $m_{\alpha,F}(x)$ 在 $\overline{F}$ 中的所有不同根的集合。[@problem_id:3087147]

如果 $L/F$ 是一个伽罗瓦扩张（例如，一个不[可约多项式](@entry_id:148759)在 $F$ 上的[分裂域](@entry_id:151552)），那么伽罗瓦群 $\operatorname{Gal}(L/F)$ 在 $m_{\alpha,F}(x)$ 的根集上的作用是**传递的** (transitive)。这意味着对于任意两个根 $\beta_1, \beta_2$，都存在一个群元素 $\sigma \in \operatorname{Gal}(L/F)$ 使得 $\sigma(\beta_1) = \beta_2$。因此，在这种情况下，$\alpha$ 的伽罗瓦共轭类就是其[最小多项式](@entry_id:153598)的完整根集。[@problem_id:3087134]

#### 迹与范数

与[代数数](@entry_id:150888) $\alpha$ 及其共轭元相关联的两个重要[不变量](@entry_id:148850)是**迹** (trace) 和**范数** (norm)。对于域扩张 $L = F(\alpha)$，$\alpha$ 的迹 $\operatorname{Tr}_{L/F}(\alpha)$ 和范数 $\operatorname{N}_{L/F}(\alpha)$ 在线性代数中被定义为“乘以 $\alpha$”这个 $F$-线性变换 $m_\alpha: L \to L$ 的[迹和行列式](@entry_id:149685)。[@problem_id:3087114]

幸运的是，它们可以直接从[最小多项式](@entry_id:153598)的系数中读出。设 $m_{\alpha,F}(x) = x^n + a_{n-1}x^{n-1} + \dots + a_1 x + a_0$，则：
$$ \operatorname{Tr}_{F(\alpha)/F}(\alpha) = -a_{n-1} $$
$$ \operatorname{N}_{F(\alpha)/F}(\alpha) = (-1)^n a_0 $$
这些公式的成立，是因为[线性变换](@entry_id:149133) $m_\alpha$ 在基 $\{1, \alpha, \dots, \alpha^{n-1}\}$ 下的矩阵（即[友矩阵](@entry_id:148203)）的特征多项式恰好就是[最小多项式](@entry_id:153598) $m_{\alpha,F}(x)$。

例如，对于 $m_{\alpha,F}(t) = t^{4} - 3 t^{3} + 2 t - 5$，我们有 $n=4, a_3=-3, a_0=-5$。因此：
- $\operatorname{Tr}_{F(\alpha)/F}(\alpha) = -a_3 = -(-3) = 3$
- $\operatorname{N}_{F(\alpha)/F}(\alpha) = (-1)^4 a_0 = 1 \cdot (-5) = -5$
[@problem_id:3087114]

当扩张是可分的（在特征为零的域上总是如此），迹等于所有共轭元之和，而范数等于所有共轭元之积。这与[多项式根](@entry_id:150265)与系数的关系（[韦达定理](@entry_id:150627)）是完全一致的。

### [域扩张](@entry_id:153187)塔中的最小多项式

[最小多项式](@entry_id:153598)的次数揭示了域扩张的结构。一个优美的结果来自于[域扩张](@entry_id:153187)的**塔法则** (Tower Law)。

考虑一个[域塔](@entry_id:153606) $F \subseteq E \subseteq K$。塔法则表明，[域扩张的次数](@entry_id:149430)是可乘的：$[K:F] = [K:E][E:F]$。

现在，假设 $\alpha$ 是 $F$ 上的[代数元](@entry_id:153893)，而 $\beta$ 是[中间域](@entry_id:153550) $F(\alpha)$ 中的一个元素，即 $\beta \in F(\alpha)$。由于 $F(\beta)$ 是包含 $F$ 和 $\beta$ 的最小域，我们有[域塔](@entry_id:153606) $F \subseteq F(\beta) \subseteq F(\alpha)$。

应用塔法则，我们得到：
$$ [F(\alpha):F] = [F(\alpha):F(\beta)][F(\beta):F] $$
利用域扩张次数与最小多项式次数之间的等价关系，上式可以改写为：
$$ \deg(m_{\alpha,F}) = [F(\alpha):F(\beta)] \cdot \deg(m_{\beta,F}) $$
由于所有的次数都是正整数，这个等式直接表明 $\deg(m_{\beta,F})$ 必须整除 $\deg(m_{\alpha,F})$。[@problem_id:3087145]

这个定理非常强大。例如，我们知道 $m_{\sqrt{2}+\sqrt{3}, \mathbb{Q}}(x)$ 的次数是 $4$。考虑元素 $\beta = \sqrt{6} = (\alpha^2-5)/2 \in \mathbb{Q}(\alpha)$。我们知道 $\beta$ 的最小多项式是 $x^2-6$，次数为 $2$。根据塔法则， $2$ 必须整除 $4$，这与事实相符。这个定理为探索[代数数域](@entry_id:637592)的子域结构提供了有力的约束。