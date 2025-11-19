## 引言
[黎曼zeta函数](@entry_id:161915) $\zeta(s)$ 是数论乃至整个数学领域的核心基石。一个令人着迷的现象是，尽管它在正奇数点上的取值至今仍是深邃的谜团，其在正偶数整数点（$\zeta(2), \zeta(4), \dots$）上的取值却遵循着一个优美而精确的模式，均表现为 $\pi$ 的偶次幂的有理数倍。本文旨在系统性地解答这一现象背后的“为什么”和“如何计算”的问题，填补从知晓结果到理解其深刻内涵之间的知识鸿沟。

在接下来的内容中，我们将踏上一段精彩的数学之旅。第一章“原理与机制”将带您回顾Euler对巴塞尔问题的革命性解法，探索[傅里叶分析](@entry_id:137640)的威力，并最终揭示[伯努利数](@entry_id:177442)如何统一所有偶数zeta值的计算。第二章“应用与跨学科联系”将展示这些数值如何超越纯数学的范畴，在物理学、概率论和现代分析中扮演着关键角色。最后的“动手实践”部分则提供了精心设计的问题，帮助您将理论知识转化为实践能力。

## 原理与机制

继引言之后，本章旨在深入探讨[黎曼zeta函数](@entry_id:161915)在正偶数整数点上取值的内在原理与机制。[黎曼zeta函数](@entry_id:161915)，定义为 $\zeta(s) = \sum_{n=1}^\infty \frac{1}{n^s}$（对于实部 $\text{Re}(s) > 1$），在数论及其他数学分支中扮演着核心角色。尽管其在奇数点上的取值至今仍是深邃的谜团，但它在偶数点上的取值却呈现出令人惊叹的规律性，即均为 $\pi$ 的幂的有理数倍。本章将通过多种深刻而优美的方法，揭示这些数值的计算方式及其背后的数学结构。

### 巴塞尔问题与Euler的洞察：复分析方法

我们探索的起点是著名的**巴塞尔问题**（Basel problem），即求解级数 $\sum_{n=1}^\infty \frac{1}{n^2}$ 的精确值，也就是 $\zeta(2)$。这个问题在17世纪被提出后，困扰了数学家们数十年，直到 Leonhard Euler 在1734年给出了一个革命性的解答。Euler的非凡之处在于他将一个看似纯粹的数论问题置于复分析的框架下，通过研究一个函数的两种不同展开形式来解决。

考虑函数 $f(z) = \frac{\sin(\pi z)}{\pi z}$。一方面，我们可以利用 $\sin(x)$ 的[麦克劳林级数](@entry_id:146685)展开：
$$ \sin(x) = \sum_{k=0}^{\infty} (-1)^k \frac{x^{2k+1}}{(2k+1)!} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \dots $$
将 $x$ 替换为 $\pi z$ 并除以 $\pi z$，我们得到 $f(z)$ 的[麦克劳林级数](@entry_id:146685)：
$$ \frac{\sin(\pi z)}{\pi z} = \sum_{k=0}^{\infty} (-1)^k \frac{(\pi z)^{2k}}{(2k+1)!} = 1 - \frac{\pi^2}{6}z^2 + \frac{\pi^4}{120}z^4 - \dots $$
从这个展开式中，我们清晰地看到 $z^2$ 项的系数是 $-\frac{\pi^2}{6}$。

另一方面，根据魏尔斯特拉斯分解定理（Weierstrass factorization theorem），一个[整函数](@entry_id:176232)（在整个复平面上解析的函数）可以由其零点构造成一个无穷乘积。函数 $f(z) = \frac{\sin(\pi z)}{\pi z}$ 的零点恰好是所有非零整数 $z = \pm 1, \pm 2, \pm 3, \dots$。因此，它可以表示为如下的无穷乘积形式：
$$ \frac{\sin(\pi z)}{\pi z} = \prod_{n=1}^{\infty} \left(1 - \frac{z^2}{n^2}\right) = \left(1 - \frac{z^2}{1^2}\right) \left(1 - \frac{z^2}{2^2}\right) \left(1 - \frac{z^2}{3^2}\right) \dots $$
将这个无穷乘积展开，我们同样可以得到一个关于 $z$ 的幂级数。展开式的前几项为：
$$ \prod_{n=1}^{\infty} \left(1 - \frac{z^2}{n^2}\right) = 1 - \left(\sum_{n=1}^{\infty} \frac{1}{n^2}\right) z^2 + \left(\sum_{1 \le n_1  n_2}^\infty \frac{1}{n_1^2 n_2^2}\right) z^4 - \dots $$
这里 $z^2$ 项的系数是 $-\sum_{n=1}^{\infty} \frac{1}{n^2}$，也即 $-\zeta(2)$。

由于函数的[麦克劳林级数](@entry_id:146685)和无穷乘积展开在[收敛域](@entry_id:269722)内是等价的，它们对应幂次的系数必须相等。通过比较 $z^2$ 项的系数，我们立即得到 Euler 的辉煌成果 [@problem_id:794071]：
$$ -\zeta(2) = -\frac{\pi^2}{6} \quad \Longrightarrow \quad \zeta(2) = \sum_{n=1}^{\infty} \frac{1}{n^2} = \frac{\pi^2}{6} $$
这一方法不仅解决了巴塞尔问题，更开启了一扇大门。原则上，通过比较更高次项（如 $z^4$）的系数，我们可以建立起不同偶数zeta值之间的复杂关系，并最终确定它们的值。

### 傅里叶分析的威力

傅里叶分析为计算zeta值提供了另一条截然不同的路径，它展示了数学不同分支间的深刻联系。其核心思想是，周期函数的傅里叶级数展开常常自然地包含我们感兴趣的数论级数。

#### [傅里叶级数](@entry_id:139455)的直接积分

考虑一个定义在 $(0, 2\pi)$ 区间上的[锯齿波](@entry_id:159756)函数 $f(x) = \pi - x$，并将其以 $2\pi$ 为周期进行延拓。其傅里叶级数展开式为：
$$ \pi - x = \sum_{n=1}^{\infty} \frac{2}{n} \sin(nx) $$
对这个等式两边从 $0$ 到 $x$ 进行[逐项积分](@entry_id:138696)，我们得到：
$$ \int_0^x (\pi - t) dt = \sum_{n=1}^{\infty} \int_0^x \frac{2}{n} \sin(nt) dt $$
计算左边的积分，得到 $\pi x - \frac{x^2}{2}$。计算右边的积分，得到：
$$ \sum_{n=1}^{\infty} \frac{2}{n} \left[-\frac{\cos(nt)}{n}\right]_0^x = \sum_{n=1}^{\infty} \frac{2}{n^2} (1 - \cos(nx)) = 2\sum_{n=1}^{\infty} \frac{1}{n^2} - 2\sum_{n=1}^{\infty} \frac{\cos(nx)}{n^2} $$
于是我们建立了一个新的恒等式：
$$ \pi x - \frac{x^2}{2} = 2\zeta(2) - 2\sum_{n=1}^{\infty} \frac{\cos(nx)}{n^2} $$
这个恒等式包含着我们想要的值 $\zeta(2)$。为了求解它，我们可以巧妙地选取一个 $x$ 值。例如，取 $x=\pi$，此时 $\cos(n\pi) = (-1)^n$，等式变为：
$$ \pi^2 - \frac{\pi^2}{2} = \frac{\pi^2}{2} = 2\zeta(2) - 2\sum_{n=1}^{\infty} \frac{(-1)^n}{n^2} $$
这里的级数 $\sum_{n=1}^{\infty} \frac{(-1)^n}{n^2}$ 可以通过 $\zeta(2)$ 表示。注意到所有偶数项为正，奇数项为负，我们可以将其拆分：
$$ \sum_{n=1}^{\infty} \frac{(-1)^n}{n^2} = -\frac{1}{1^2} + \frac{1}{2^2} - \frac{1}{3^2} + \dots = \left(\frac{1}{2^2} + \frac{1}{4^2} + \dots\right) - \left(\frac{1}{1^2} + \frac{1}{3^2} + \dots\right) $$
$$ = \frac{1}{4}\zeta(2) - \left(\zeta(2) - \frac{1}{4}\zeta(2)\right) = -\frac{1}{2}\zeta(2) $$
代回原式，我们解得 $\frac{\pi^2}{2} = 2\zeta(2) - 2(-\frac{1}{2}\zeta(2)) = 3\zeta(2)$，从而再次得到 $\zeta(2) = \frac{\pi^2}{6}$ [@problem_id:794151]。

#### [帕塞瓦尔定理](@entry_id:139215)的应用

[帕塞瓦尔定理](@entry_id:139215)（Parseval's theorem）是[傅里叶分析](@entry_id:137640)中的一个[能量守恒](@entry_id:140514)定律，它将函数的能量（其模平方的积分）与它的[傅里叶系数](@entry_id:144886)的能量（系数模平方和）联系起来。对于定义在 $[0, 1]$ 上的函数 $g(x)$，其[傅里叶级数](@entry_id:139455)为 $g(x) \sim \frac{a_0}{2} + \sum_{n=1}^\infty (a_n \cos(2\pi nx) + b_n \sin(2\pi nx))$，[帕塞瓦尔定理](@entry_id:139215)表明：
$$ \int_0^1 |g(x)|^2 dx = \left(\frac{a_0}{2}\right)^2 + \frac{1}{2} \sum_{n=1}^{\infty} (a_n^2 + b_n^2) $$
这个定理是计算偶数zeta值的强大工具。让我们考虑定义在 $[0, 1]$ 上的二次多项式 $P(x) = x^2 - x + \frac{1}{6}$。这个多项式实际上是第二个[伯努利多项式](@entry_id:203273) $B_2(x)$。它的傅里叶级数（只含余弦项）为：
$$ x^2 - x + \frac{1}{6} = \sum_{n=1}^{\infty} \frac{\cos(2\pi nx)}{\pi^2 n^2} $$
在这个展开式中，常数项 $a_0=0$，正弦系数 $b_n=0$，余弦系数 $a_n = \frac{1}{\pi^2 n^2}$。为了应用[帕塞瓦尔定理](@entry_id:139215)，我们分别计算等式两边 [@problem_id:794175]。
左边是函数平方的积分：
$$ \int_0^1 \left(x^2 - x + \frac{1}{6}\right)^2 dx = \int_0^1 \left(x^4 - 2x^3 + \frac{4}{3}x^2 - \frac{1}{3}x + \frac{1}{36}\right) dx = \left[\frac{x^5}{5} - \frac{x^4}{2} + \frac{4x^3}{9} - \frac{x^2}{6} + \frac{x}{36}\right]_0^1 = \frac{1}{180} $$
右边是[傅里叶系数](@entry_id:144886)的平方和：
$$ \left(\frac{a_0}{2}\right)^2 + \frac{1}{2} \sum_{n=1}^{\infty} a_n^2 = 0 + \frac{1}{2} \sum_{n=1}^{\infty} \left(\frac{1}{\pi^2 n^2}\right)^2 = \frac{1}{2\pi^4} \sum_{n=1}^{\infty} \frac{1}{n^4} = \frac{\zeta(4)}{2\pi^4} $$
令两边相等，我们得到：
$$ \frac{1}{180} = \frac{\zeta(4)}{2\pi^4} $$
解出 $\zeta(4)$，我们便得到了它的精确值：
$$ \zeta(4) = \frac{2\pi^4}{180} = \frac{\pi^4}{90} $$

### [伯努利数](@entry_id:177442)的统一作用

尽管上述方法巧妙而富有启发性，但它们似乎是针对特定情况的“孤立技巧”。一个更深刻、更具普遍性的结构将所有偶数zeta值联系在一起，而这个结构的核心就是**[伯努利数](@entry_id:177442)**（Bernoulli numbers）。

[伯努利数](@entry_id:177442) $B_m$ 是一串有理数，可以通过它们的指数[生成函数](@entry_id:146702)来定义：
$$ \frac{x}{e^x - 1} = \sum_{m=0}^{\infty} B_m \frac{x^m}{m!} $$
前几个[伯努利数](@entry_id:177442)是 $B_0 = 1, B_1 = -\frac{1}{2}, B_2 = \frac{1}{6}, B_3=0, B_4 = -\frac{1}{30}, \dots$。除了 $B_1$ 外，所有奇数项[伯努利数](@entry_id:177442)均为零。

Euler 发现了连接偶数zeta值和[伯努利数](@entry_id:177442)的通用公式：
$$ \zeta(2k) = (-1)^{k+1} \frac{(2\pi)^{2k}}{2(2k)!} B_{2k} \quad \text{for } k \in \{1, 2, 3, \dots\} $$
这个公式是数论中的一块基石。它揭示了 $\zeta(2k)$ 的值本质上是由[伯努利数](@entry_id:177442) $B_{2k}$ 控制的。例如，当 $k=1$ 时，使用 $B_2 = 1/6$，我们得到 $\zeta(2) = (-1)^2 \frac{(2\pi)^2 B_2}{2(2!)} = \frac{4\pi^2 (1/6)}{4} = \frac{\pi^2}{6}$。当 $k=2$ 时，使用 $B_4 = -1/30$，我们得到 $\zeta(4) = (-1)^3 \frac{(2\pi)^4 B_4}{2(4!)} = -\frac{16\pi^4(-1/30)}{48} = \frac{\pi^4}{90}$。

我们可以利用这个公式直接计算更高阶的zeta值。例如，已知第八个[伯努利数](@entry_id:177442) $B_8 = -1/30$，我们可以计算 $\zeta(8)$ [@problem_id:794027]：
$$ \zeta(8) = (-1)^{4+1} \frac{(2\pi)^8 B_8}{2(8!)} = - \frac{256\pi^8 (-1/30)}{2 \cdot 40320} = \frac{256\pi^8}{60 \cdot 40320} = \frac{\pi^8}{9450} $$

[Euler公式](@entry_id:176440)的推导本身也极具启发性。一种标准方法是考虑函数 $\pi z \coth(\pi z)$ 的两种展开。一方面，利用[伯努利数](@entry_id:177442)的生成函数可以得到其[麦克劳林级数](@entry_id:146685) [@problem_id:794120]：
$$ \pi z \coth(\pi z) = \pi z \frac{e^{\pi z} + e^{-\pi z}}{e^{\pi z} - e^{-\pi z}} = \frac{2\pi z}{e^{2\pi z}-1} + \pi z = 1 + \sum_{k=1}^{\infty} B_{2k} \frac{(2\pi z)^{2k}}{(2k)!} $$
另一方面，利用 Mittag-Leffler 展开，可以将 $\pi z \coth(\pi z)$ 表示为一个与zeta函数值相关的级数：
$$ \pi z \coth(\pi z) = 1 + 2 \sum_{n=1}^{\infty} \frac{z^2}{z^2+n^2} = 1 + 2 \sum_{k=1}^{\infty} (-1)^{k-1} \zeta(2k) z^{2k} $$
比较这两个级数中 $z^{2k}$ 的系数，就直接导出了[Euler公式](@entry_id:176440)。

[伯努利数](@entry_id:177442)自身也满足深刻的递推关系，这些关系可以用来计算它们的值，进而计算zeta值。例如，[伯努利数](@entry_id:177442)满足一个卷积恒等式，它揭示了[伯努利数](@entry_id:177442)之间的[代数结构](@entry_id:137052)。利用 $B_4 = -1/30$ 和 $B_6 = 1/42$，可以从一个关于[除数函数](@entry_id:194945)的恒等式中推导出 $B_{10} = 5/66$，进而求得 $\zeta(10) = \frac{\pi^{10}}{93555}$ [@problem_id:794100]。这些关系还允许我们推导不同zeta值之间的比例，例如，可以证明 $\frac{\zeta(2)\zeta(4)}{\zeta(6)} = \frac{7}{4}$，这完全由 $B_2, B_4, B_6$ 的值决定 [@problem_id:794142]。

### 积分表示与其他联系

除了[级数展开](@entry_id:142878)，积分表示也为研究zeta函数提供了有力的视角。一个核心的积分表示将zeta函数与Gamma函数 $\Gamma(s) = \int_0^\infty x^{s-1} e^{-x} dx$ 联系起来：
$$ \Gamma(s)\zeta(s) = \int_0^\infty \frac{x^{s-1}}{e^x - 1} dx $$
这个公式在物理学中尤为重要，因为它与普朗克[黑体辐射](@entry_id:137223)定律中的积分形式直接相关。利用这个公式和已知的zeta值，我们可以计算一些看似复杂的定积分。例如，为了计算积分 $I = \int_0^\infty \frac{x^5}{e^x - 1} dx$，我们只需在公式中令 $s=6$ [@problem_id:794033]：
$$ I = \Gamma(6)\zeta(6) $$
由于 $\Gamma(6) = 5! = 120$，且我们已经知道 $\zeta(6) = \frac{\pi^6}{945}$（可由 $B_6=1/42$ 推出），我们可以立即得到：
$$ I = 120 \cdot \frac{\pi^6}{945} = \frac{8\pi^6}{63} $$

还有其他巧妙的积分技巧。例如，考虑双重积分 $I = \int_0^1 \int_0^1 \frac{\ln(x)\ln(y)}{1-xy} dx dy$。通过将分母 $\frac{1}{1-xy}$ 展开为几何级数 $\sum_{n=0}^\infty (xy)^n$，并将[积分与求和交换](@entry_id:199288)顺序，我们可以得到 [@problem_id:794101]：
$$ I = \sum_{n=0}^\infty \int_0^1 \int_0^1 x^n y^n \ln(x) \ln(y) dx dy = \sum_{n=0}^\infty \left(\int_0^1 x^n \ln(x) dx\right) \left(\int_0^1 y^n \ln(y) dy\right) $$
通过分部积分可以求得 $\int_0^1 x^n \ln(x) dx = -\frac{1}{(n+1)^2}$。因此，积分 $I$ 等于：
$$ I = \sum_{n=0}^\infty \left(-\frac{1}{(n+1)^2}\right)^2 = \sum_{n=0}^\infty \frac{1}{(n+1)^4} = \sum_{m=1}^\infty \frac{1}{m^4} = \zeta(4) $$
这个优美的结果再次确认了 $\zeta(4) = \frac{\pi^4}{90}$，展示了[多重积分](@entry_id:146170)与zeta函数之间的精妙联系。

### 展望：多重Zeta值

对[黎曼zeta函数](@entry_id:161915)的研究并未止步于单变量。一个自然的推广是**多重Zeta值**（Multiple Zeta Values, MZVs）。对于正整数 $s_1, s_2, \dots, s_k$ 且 $s_1  1$，MZV定义为：
$$ \zeta(s_1, s_2, \dots, s_k) = \sum_{n_1  n_2  \dots  n_k \ge 1} \frac{1}{n_1^{s_1} n_2^{s_2} \dots n_k^{s_k}} $$
这些多重级数构成的世界拥有比经典zeta函数远为丰富的[代数结构](@entry_id:137052)。例如，两个单变量zeta函数的乘积可以分解为MZVs的和。一个基本的乘积恒等式是：
$$ \zeta(p)\zeta(q) = \zeta(p,q) + \zeta(q,p) + \zeta(p+q) $$
这个恒等式说明，虽然 $\zeta(p)\zeta(q)$ 是两个简单和的乘积，但它本身对应着一个更复杂的、包含有序求和的结构。我们可以利用这个关系以及已知的偶数zeta值来计算某些MZV的和。例如，为了计算 $\zeta(2,4) + \zeta(4,2)$，我们设置 $p=2, q=4$ [@problem_id:794021]：
$$ \zeta(2,4) + \zeta(4,2) = \zeta(2)\zeta(4) - \zeta(6) $$
代入已知的 $\zeta(2)=\frac{\pi^2}{6}$，$\zeta(4)=\frac{\pi^4}{90}$ 和 $\zeta(6)=\frac{\pi^6}{945}$，我们得到：
$$ \zeta(2,4) + \zeta(4,2) = \left(\frac{\pi^2}{6}\right)\left(\frac{\pi^4}{90}\right) - \frac{\pi^6}{945} = \frac{\pi^6}{540} - \frac{\pi^6}{945} = \frac{\pi^6}{1260} $$
这表明，我们对经典偶数zeta值的理解，是探索更广阔的MZV[代数结构](@entry_id:137052)的基石。