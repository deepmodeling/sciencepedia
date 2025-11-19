## 引言
[修正贝塞尔函数](@entry_id:184177)是数学物理方程中的一类重要[特殊函数](@entry_id:143234)，广泛出现在从[热传导](@entry_id:147831)、[流体力学](@entry_id:136788)到[量子场论](@entry_id:138177)的众多科学与工程问题中。它们的深刻价值不仅在于作为修正亥姆霍兹方程的解，更在于其在自变量趋于两个极端——零和无穷大——时的独特[渐近行为](@entry_id:160836)。然而，许多学习者和研究者往往只将它们视为复杂的数学公式，未能充分理解这些极限行为如何直接转化为对物理系统在不同尺度下行为的深刻洞察。本文旨在弥合这一知识鸿沟。

本文将系统性地剖析[修正贝塞尔函数](@entry_id:184177)在小宗量与大宗量极限下的行为。在第一章“原理与机制”中，我们将深入探讨其级数展开和[渐近展开](@entry_id:173196)的数学基础，揭示函数在原点附近的奇异性以及在无穷远处的[指数增长](@entry_id:141869)或衰减特性。接下来的第二章“应用与[交叉](@entry_id:147634)学科联系”将展示这些数学原理如何在物理学、生命科学、工程学乃至纯粹数学等多个领域中，成为解释屏蔽效应、扩散过程和相互作用的关键工具。最后，通过第三章“动手实践”，读者将有机会通过具体问题演练，将理论知识转化为解决实际问题的能力。现在，让我们从这些函数的基本数学原理开始，深入探索它们的内在机制。

## 原理与机制

在介绍性章节之后，我们现在深入探讨[修正贝塞尔函数](@entry_id:184177)的具体数学特性。这些函数在物理和工程领域的普遍应用，源于它们在变量趋近于零或无穷大时的独特渐近行为。理解这些极限情况下的行为，对于求解微分方程、评估物理量以及在特定条件下简化复杂模型至关重要。本章将系统地阐述这些函数在[自变量](@entry_id:267118)取小值和大值时的核心原理和分析机制。

### 小自变量行为 ($z \to 0$): 级数展开

对于[修正贝塞尔方程](@entry_id:165309)而言，原点 $z=0$ 是一个[正则奇点](@entry_id:165348)。因此，解的行为可以通过[幂级数](@entry_id:146836)或广义幂级数（Frobenius级数）来精确描述。这种方法为我们提供了在小[自变量](@entry_id:267118)极限下分析函数性质的坚实基础。

#### 第一类[修正贝塞尔函数](@entry_id:184177) $I_\nu(z)$

第一类[修正贝塞尔函数](@entry_id:184177) $I_\nu(z)$ 以其在原点的正则性而著称（除非 $\nu$ 是负整数）。其标准级数展开式定义为：
$$
I_\nu(z) = \left(\frac{z}{2}\right)^\nu \sum_{k=0}^{\infty} \frac{(z^2/4)^k}{k! \Gamma(\nu+k+1)}
$$
其中 $\Gamma(x)$ 是欧拉伽马函数。

从这个级数中，我们可以立即看出当 $z \to 0$ 时的主导项。对于 $k=0$ 的项，我们得到函数的首项近似：
$$
I_\nu(z) \sim \frac{1}{\Gamma(\nu+1)} \left(\frac{z}{2}\right)^\nu \quad (z \to 0)
$$
这表明，在原点附近，$I_\nu(z)$ 的行为类似于 $z^\nu$。对于最常见的整数阶情况，例如 $\nu=0$ 和 $\nu=1$，我们有：
$$
I_0(z) = 1 + \frac{z^2}{4} + \frac{z^4}{64} + \dots \to 1
$$
$$
I_1(z) = \frac{z}{2} + \frac{z^3}{16} + \frac{z^5}{768} + \dots \to 0
$$
级数展开不仅给出了主导行为，还允许我们对涉及这些函数的表达式进行精确的代数运算。例如，我们可以通过对级数进行[逐项微分](@entry_id:142985)来分析相关函数的泰勒展开。考虑函数 $f(z) = \frac{d}{dz}(z^{-1} I_1(z))$ [@problem_id:768663]。首先，我们写出 $z^{-1} I_1(z)$ 的级数：
$$
z^{-1} I_1(z) = z^{-1} \sum_{k=0}^{\infty} \frac{z^{2k+1}}{2^{2k+1} k! (k+1)!} = \sum_{k=0}^{\infty} \frac{z^{2k}}{2^{2k+1} k! (k+1)!} = \frac{1}{2} + \frac{z^2}{16} + \frac{z^4}{384} + \dots
$$
现在对该级数逐项求导：
$$
f(z) = \frac{d}{dz} \left( \sum_{k=0}^{\infty} \frac{z^{2k}}{2^{2k+1} k! (k+1)!} \right) = \sum_{k=1}^{\infty} \frac{2k \cdot z^{2k-1}}{2^{2k+1} k! (k+1)!}
$$
我们希望找到 $f(z)$ 展开式中 $z^1$ 项的系数。这对应于级数中 $2k-1=1$，即 $k=1$ 的那一项。代入 $k=1$，我们得到该项的系数为：
$$
\frac{2 \cdot 1}{2^{2(1)+1} \cdot 1! \cdot (1+1)!} = \frac{2}{2^3 \cdot 1 \cdot 2} = \frac{2}{16} = \frac{1}{8}
$$
这个例子展示了如何利用基础的级数定义来精确推导函数在原点附近的局部行为。

#### [第二类修正贝塞尔函数](@entry_id:201421) $K_\nu(z)$

与 $I_\nu(z)$ 不同，$K_\nu(z)$ 在原点 $z=0$ 处总是奇异的。其行为的性质取决于阶数 $\nu$ 是否为整数。

**非整数阶 $\nu$**

当 $\nu$ 不是整数时，$I_\nu(z)$ 和 $I_{-\nu}(z)$ 是[修正贝塞尔方程](@entry_id:165309)的两个[线性无关解](@entry_id:185441)。$K_\nu(z)$ 可以通过它们的[线性组合](@entry_id:154743)来定义：
$$
K_\nu(z) = \frac{\pi}{2} \frac{I_{-\nu}(z) - I_{\nu}(z)}{\sin(\nu \pi)}
$$
由于 $I_\nu(z) \sim z^\nu$ 而 $I_{-\nu}(z) \sim z^{-\nu}$，当 $\nu > 0$ 且 $z \to 0$ 时，$I_{-\nu}(z)$ 项占主导地位。因此，$K_\nu(z)$ 的行为类似于 $z^{-\nu}$：
$$
K_\nu(z) \sim \frac{\pi}{2 \sin(\nu \pi)} I_{-\nu}(z) \sim \frac{\pi}{2 \sin(\nu \pi) \Gamma(1-\nu)} \left(\frac{z}{2}\right)^{-\nu}
$$
这种[幂律](@entry_id:143404)[奇点](@entry_id:137764)是一个关键特征。我们可以通过计算一个极限来验证这一行为 [@problem_id:768556]。考虑表达式 $z \frac{K'_\nu(z)}{K_\nu(z)}$ 在 $z \to 0^+$ 时的极限。如果 $K_\nu(z) \sim A z^{-\nu}$，其中 $A$ 是一个常数，那么 $K'_\nu(z) \sim A(-\nu)z^{-\nu-1}$。因此，比值为：
$$
\frac{K'_\nu(z)}{K_\nu(z)} \sim \frac{A(-\nu)z^{-\nu-1}}{A z^{-\nu}} = -\frac{\nu}{z}
$$
从而，我们得到一个与阶数直接相关的普适结果：
$$
\lim_{z\to 0^+} z \frac{K'_\nu(z)}{K_\nu(z)} = -\nu
$$
对于 $\nu=1/3$ 的情况，这个极限值就是 $-1/3$。

**整数阶 $\nu=n$**

当 $\nu$ 趋于一个整数 $n$ 时，$I_n(z) = (-1)^n I_{-n}(z)$，导致上述 $K_\nu(z)$ 的定义式变为 $\frac{0}{0}$ 的[不定形式](@entry_id:150990)。通过[洛必达法则](@entry_id:147503)处理这个极限，会引入对数项。最重要的整数阶情况是 $\nu=0$。
对于 $z \to 0^+$，$I_0(z)$ 和 $K_0(z)$ 的行为是：
$$
I_0(z) = 1 + O(z^2)
$$
$$
K_0(z) = -(\ln(\frac{z}{2}) + \gamma)I_0(z) + O(z^2 \ln z)
$$
这里，$\gamma \approx 0.5772$ 是[欧拉-马歇罗尼常数](@entry_id:146205)。$K_0(z)$ 在原点有一个对数[奇点](@entry_id:137764)。为了更清晰地理解这个[奇点](@entry_id:137764)的性质，我们可以考察极限 $L = \lim_{z \to 0^+} \frac{K_0(z)}{I_0(z)\ln z}$ [@problem_id:768539]。将 $K_0(z)$ 的展开式代入：
$$
L = \lim_{z \to 0^+} \frac{-(\ln(z/2) + \gamma)I_0(z) + O(z^2 \ln z)}{I_0(z)\ln z} = \lim_{z \to 0^+} \left( \frac{-(\ln z - \ln 2 + \gamma)}{\ln z} + \frac{O(z^2 \ln z)}{I_0(z) \ln z} \right)
$$
当 $z \to 0^+$ 时，$I_0(z) \to 1$ 且 $\ln z \to -\infty$。第一项变为：
$$
\lim_{z \to 0^+} \left( -1 + \frac{\ln 2 - \gamma}{\ln z} \right) = -1
$$
第二项 $O(z^2)$ 趋于零。因此，极限值为 $-1$。这个结果定量地描述了 $K_0(z)$ 的对数[奇点](@entry_id:137764)强度，即 $K_0(z) \sim -\ln z$。

#### 小自变量展开的高阶课题

对小[自变量](@entry_id:267118)行为的分析可以扩展到更复杂的场景，例如函[数乘](@entry_id:155971)积的展开或对阶数 $\nu$ 的导数。

一个有趣的例子是分析乘积 $I_0(z)K_1(z)$ 在 $z \to 0$ 附近的行为，特别是寻找 $z \log z$ 项的系数 [@problem_id:768510]。这需要 $K_1(z)$ 的小自变量展开。我们可以利用[递推关系](@entry_id:189264) $K'_0(z) = -K_1(z)$。通过对 $K_0(z)$ 的展开式求导，我们得到：
$$
K'_0(z) = -\frac{d}{dz}\left[\ln\left(\frac{z}{2}\right)I_0(z)\right] - \dots = -\frac{1}{z}I_0(z) - \ln\left(\frac{z}{2}\right)I'_0(z) - \dots
$$
利用 $I'_0(z) = I_1(z)$，我们有 $K_1(z) = -K'_0(z) = \frac{1}{z}I_0(z) + \ln(\frac{z}{2})I_1(z) + \dots$。现在，我们将 $I_0(z)$ 和 $I_1(z)$ 的级数代入：
$$
I_0(z) = 1 + O(z^2)
$$
$$
I_1(z) = \frac{z}{2} + O(z^3)
$$
$$
K_1(z) = \frac{1}{z}(1 + O(z^2)) + (\ln z - \ln 2)(\frac{z}{2} + O(z^3)) + \dots = \frac{1}{z} + \frac{z}{2}\ln z + O(z)
$$
现在计算乘积 $I_0(z)K_1(z)$：
$$
I_0(z)K_1(z) = (1 + O(z^2)) \left(\frac{1}{z} + \frac{z}{2}\ln z + O(z)\right)
$$
要得到 $z \ln z$ 项，我们将 $I_0(z)$ 中的常数项 $1$ 与 $K_1(z)$ 中的 $\frac{z}{2}\ln z$ 项相乘。这给出了 $\frac{1}{2} z \ln z$。更高阶的项不会产生 $z \ln z$ 项。因此，所求系数是 $\frac{1}{2}$。

另一个高级主题是研究函数对阶数 $\nu$ 的导数，这在理论推导中非常重要，例如在定义整数阶第二类普通贝塞尔函数 $Y_n(z)$ 时。考虑函数 $G(\nu, z) = (z/2)^{-\nu} I_\nu(z)$。对 $\nu$ 求导并取 $\nu=0$ [@problem_id:768704]。
$$
G(\nu, z) = \sum_{k=0}^{\infty} \frac{1}{k! \Gamma(\nu+k+1)} \left(\frac{z}{2}\right)^{2k}
$$
对 $\nu$ 逐项求导：
$$
\frac{\partial G}{\partial \nu} = \sum_{k=0}^{\infty} \frac{-\psi(\nu+k+1)}{k! \Gamma(\nu+k+1)} \left(\frac{z}{2}\right)^{2k}
$$
其中 $\psi(x) = \Gamma'(x)/\Gamma(x)$ 是[双伽玛函数](@entry_id:174427)。在 $\nu=0$ 处求值：
$$
\left. \frac{\partial G}{\partial \nu} \right|_{\nu=0} = \sum_{k=0}^{\infty} \frac{-\psi(k+1)}{k! \Gamma(k+1)} \left(\frac{z}{2}\right)^{2k} = \sum_{k=0}^{\infty} \frac{-\psi(k+1)}{(k!)^2} \left(\frac{z}{2}\right)^{2k}
$$
我们寻找 $z^2$ 项的系数，这对应于 $k=1$。该系数为：
$$
\frac{-\psi(2)}{(1!)^2} \cdot \left(\frac{1}{2}\right)^2 = -\frac{\psi(2)}{4}
$$
利用[双伽玛函数](@entry_id:174427)的性质 $\psi(n) = H_{n-1} - \gamma$（其中 $H_n$ 是[调和数](@entry_id:268421)），我们有 $\psi(2) = H_1 - \gamma = 1-\gamma$。因此，系数是 $-(1-\gamma)/4 = (\gamma-1)/4$。

### 大[自变量](@entry_id:267118)行为 ($z \to \infty$): [渐近展开](@entry_id:173196)

当自变量 $z$ 很大时，使用完整的[级数展开](@entry_id:142878)是不切实际的。此时，我们转而使用[渐近展开](@entry_id:173196)。一个函数 $f(z)$ 的渐近级数是一个（可能发散的）级数，其有限部分和能够很好地近似 $f(z)$。

#### $I_\nu(z)$ 和 $K_\nu(z)$ 的[渐近展开](@entry_id:173196)

对于大的正实数 $z$，第一类和[第二类修正贝塞尔函数](@entry_id:201421)具有以下形式的[渐近展开](@entry_id:173196)：
$$
I_\nu(z) \sim \frac{e^z}{\sqrt{2\pi z}} \sum_{k=0}^{\infty} \frac{(-1)^k a_k(\nu)}{z^k} \sim \frac{e^z}{\sqrt{2\pi z}} \left( 1 - \frac{4\nu^2-1}{8z} + \frac{(4\nu^2-1)(4\nu^2-9)}{2!(8z)^2} - \dots \right)
$$
$$
K_\nu(z) \sim \sqrt{\frac{\pi}{2z}} e^{-z} \sum_{k=0}^{\infty} \frac{a_k(\nu)}{z^k} \sim \sqrt{\frac{\pi}{2z}} e^{-z} \left( 1 + \frac{4\nu^2-1}{8z} + \frac{(4\nu^2-1)(4\nu^2-9)}{2!(8z)^2} + \dots \right)
$$
其中 $a_k(\nu)$ 是依赖于 $\nu$ 的系数。

这些公式揭示了深刻的物理洞察：$I_\nu(z)$ 呈[指数增长](@entry_id:141869)，而 $K_\nu(z)$ 呈指数衰减。在许多物理问题中，如[柱坐标系](@entry_id:266798)下的热传导或[波导理论](@entry_id:264627)，物理上有意义的解在远离源的区域（$z \to \infty$）必须保持有界或衰减为零。因此，$K_\nu(z)$ 通常是描述这些外部场或衰减过程的解。

一个直接的应用是计算[渐近展开](@entry_id:173196)式中特定项的系数。例如，确定 $I_{1/6}(z)$ 展开式中 $e^z z^{-3/2}$ 项的系数 [@problem_id:768563]。$I_\nu(z)$ 的展开式可写为 $\frac{e^z}{\sqrt{2\pi z}} \sum_{k=0}^{\infty} C_k z^{-k}$。$e^z z^{-3/2}$ 项来自前置因子 $e^z z^{-1/2}$ 与和式中 $z^{-1}$ 项的乘积，这对应于 $k=1$。
对于 $k=1$，级数项为 $-\frac{4\nu^2-1}{8z}$。代入 $\nu=1/6$，我们有 $4\nu^2-1 = 4(1/36)-1 = 1/9-1 = -8/9$。
因此，级数中的项是 $-\frac{-8/9}{8z} = \frac{1}{9z}$。
将此前置因子 $\frac{e^z}{\sqrt{2\pi z}}$ 乘上此项，我们得到 $\frac{e^z}{\sqrt{2\pi z}} \cdot \frac{1}{9z} = \frac{1}{9\sqrt{2\pi}} e^z z^{-3/2}$。所以，系数是 $\frac{1}{9\sqrt{2\pi}}$。

更有趣的应用出现在处理函数比率时。考虑极限 $\lim_{z\to\infty} z (1 - \frac{I_1(z)}{I_0(z)})$ [@problem_id:768549]。在这里，主导的指数项 $e^z/\sqrt{2\pi z}$ 在比率中被消去，使我们能够探究更高阶的代数行为。
对于 $I_0(z)$（$\nu=0, \mu=4\nu^2=0$）：
$$
I_0(z) \sim \frac{e^z}{\sqrt{2\pi z}} \left(1 - \frac{-1}{8z} + \dots \right) = \frac{e^z}{\sqrt{2\pi z}} \left(1 + \frac{1}{8z} + \dots \right)
$$
对于 $I_1(z)$（$\nu=1, \mu=4\nu^2=4$）：
$$
I_1(z) \sim \frac{e^z}{\sqrt{2\pi z}} \left(1 - \frac{3}{8z} + \dots \right)
$$
计算它们的比率：
$$
\frac{I_1(z)}{I_0(z)} \sim \frac{1 - \frac{3}{8z} + O(z^{-2})}{1 + \frac{1}{8z} + O(z^{-2})}
$$
利用近似 $(1-a)/(1+b) \approx (1-a)(1-b) \approx 1-a-b$ 对小量 $a,b$ 成立，我们得到：
$$
\frac{I_1(z)}{I_0(z)} \sim 1 - \frac{3}{8z} - \frac{1}{8z} + O(z^{-2}) = 1 - \frac{4}{8z} + O(z^{-2}) = 1 - \frac{1}{2z} + O(z^{-2})
$$
因此，
$$
z \left(1 - \frac{I_1(z)}{I_0(z)}\right) \sim z \left(1 - \left(1 - \frac{1}{2z}\right)\right) = z \left(\frac{1}{2z}\right) = \frac{1}{2}
$$
极限值为 $1/2$。这表明，虽然 $I_1(z)/I_0(z)$ 在无穷远处趋于1，但它以与 $1/z$ 成正比的速率收敛。

#### [渐近展开](@entry_id:173196)的乘积与积分

我们还可以分析函数乘积的[渐近行为](@entry_id:160836)。例如，考虑乘积 $P(z) = I_\nu(z) K_\nu(z)$ [@problem_id:768503]。
$$
P(z) \sim \left[ \frac{e^z}{\sqrt{2\pi z}} \left(1 - \frac{\mu-1}{8z} + \frac{(\mu-1)(\mu-9)}{128z^2} - \dots \right) \right] \left[ \sqrt{\frac{\pi}{2z}} e^{-z} \left(1 + \frac{\mu-1}{8z} + \frac{(\mu-1)(\mu-9)}{128z^2} + \dots \right) \right]
$$
其中 $\mu=4\nu^2$。$e^z$ 和 $e^{-z}$ 项相乘为1。合并常数和 $z$ 的因子，得到：
$$
P(z) \sim \frac{1}{2z} \left(1 - \frac{\mu-1}{8z} + \dots \right) \left(1 + \frac{\mu-1}{8z} + \dots \right)
$$
展开括号内的乘积，形式为 $(1-a+b)(1+a+b)$，其中 $a=\frac{\mu-1}{8z}$，$b=\frac{(\mu-1)(\mu-9)}{128z^2}$。展开到 $z^{-2}$ 阶：
$$
(1+b)^2 - a^2 \approx 1+2b - a^2 = 1 + \frac{(\mu-1)(\mu-9)}{64z^2} - \left(\frac{\mu-1}{8z}\right)^2 = 1 + \frac{(\mu-1)(\mu-9) - (\mu-1)^2}{64z^2}
$$
$$
= 1 + \frac{(\mu-1)(\mu-9 - (\mu-1))}{64z^2} = 1 + \frac{-8(\mu-1)}{64z^2} = 1 - \frac{\mu-1}{8z^2}
$$
所以 $P(z) \sim \frac{1}{2z} \left(1 - \frac{\mu-1}{8z^2} + \dots \right) = \frac{1}{2z} - \frac{\mu-1}{16z^3} + \dots$。
对于 $\nu = 1/4$，$\mu = 4(1/16) = 1/4$。$z^{-3}$ 项的系数是 $-\frac{\mu-1}{16} = -\frac{1/4-1}{16} = -\frac{-3/4}{16} = \frac{3}{64}$。

更高级的分析涉及对包含贝塞尔函数的积分进行渐近评估。考虑积分 $I(z) = \int_z^\infty \sqrt{t} K_{1/3}(t)^2 dt$ [@problem_id:768492]。首先，我们需要被积函数 $\sqrt{t} K_{1/3}(t)^2$ 的大宗量展开。
对于 $\nu=1/3$, $4\nu^2-1 = 4/9-1 = -5/9$。
$$
K_{1/3}(t) \sim \sqrt{\frac{\pi}{2t}} e^{-t} \left( 1 - \frac{5/9}{8t} + \dots \right) = \sqrt{\frac{\pi}{2t}} e^{-t} \left( 1 - \frac{5}{72t} + \dots \right)
$$
平方后乘以 $\sqrt{t}$：
$$
\sqrt{t} K_{1/3}(t)^2 \sim \sqrt{t} \frac{\pi}{2t} e^{-2t} \left( 1 - \frac{5}{72t} \right)^2 \sim \frac{\pi}{2\sqrt{t}} e^{-2t} \left( 1 - \frac{10}{72t} + \dots \right) = \frac{\pi}{2} e^{-2t} t^{-1/2} - \frac{5\pi}{72} e^{-2t} t^{-3/2} + \dots
$$
现在我们需要对这个渐近级数进行积分。利用标准渐近积分公式（通过分部积分得到）：
$$
\int_z^\infty t^p e^{-at} dt \sim \frac{z^p e^{-az}}{a} \left( 1 + \frac{p}{az} + \dots \right)
$$
对于第一项（$p=-1/2, a=2$）：
$$
\frac{\pi}{2} \int_z^\infty e^{-2t} t^{-1/2} dt \sim \frac{\pi}{2} \left[ \frac{z^{-1/2}e^{-2z}}{2} \left(1 + \frac{-1/2}{2z} + \dots \right) \right] = \frac{\pi}{4} z^{-1/2}e^{-2z} - \frac{\pi}{16} z^{-3/2}e^{-2z} + \dots
$$
对于第二项（$p=-3/2, a=2$），我们只需要其主导项：
$$
-\frac{5\pi}{72} \int_z^\infty e^{-2t} t^{-3/2} dt \sim -\frac{5\pi}{72} \left[ \frac{z^{-3/2}e^{-2z}}{2} + \dots \right] = -\frac{5\pi}{144} z^{-3/2}e^{-2z} + \dots
$$
合并所有 $e^{-2z}z^{-3/2}$ 项的系数：
$$
C = -\frac{\pi}{16} - \frac{5\pi}{144} = \frac{-9\pi - 5\pi}{144} = -\frac{14\pi}{144} = -\frac{7\pi}{72}
$$
这个复杂的例子展示了组合使用函数[渐近展开](@entry_id:173196)和积分[渐近展开](@entry_id:173196)的强大威力。

### 纯虚自变量的行为

最后，我们探讨[修正贝塞尔函数](@entry_id:184177)在纯虚数轴上的行为。这通过一个深刻的恒等式将它们与普通贝塞尔函数 $J_\nu(z)$ 联系起来：
$$
I_\nu(z) = i^{-\nu} J_\nu(iz)
$$
这个关系意味着 $I_\nu(z)$ 在[虚轴](@entry_id:262618)上的行为本质上是 $J_\nu(z)$ 在[实轴](@entry_id:148276)上的行为。我们知道，对于大的实数 $x$，$J_\nu(x)$ 是一个衰减的[振荡](@entry_id:267781)函数：
$$
J_\nu(x) \sim \sqrt{\frac{2}{\pi x}} \cos\left(x - \frac{\nu\pi}{2} - \frac{\pi}{4}\right) \quad (x \to \infty)
$$
因此，$I_\nu(iy)$（对于实数 $y$）也将表现出[振荡](@entry_id:267781)行为，而不是指数增长。这在信号处理和波动问题中有重要应用。

让我们通过一个例子来具体说明 [@problem_id:768596]。我们想计算一个积分的平均值：$L = \lim_{Y\to\infty} \frac{1}{Y} \int_{0}^{Y} y |I_{1/3}(iy)|^2 dy$。
首先，利用上述恒等式：
$$
I_{1/3}(iy) = i^{-1/3} J_{1/3}(i^2 y) = i^{-1/3} J_{1/3}(-y)
$$
利用 $J_\nu(e^{im\pi}z) = e^{im\nu\pi}J_\nu(z)$，对于正实数 $y$ 我们有 $-y = y e^{i\pi}$，因此 $J_{1/3}(-y) = e^{i\pi/3} J_{1/3}(y)$。所以：
$$
I_{1/3}(iy) = e^{-i\pi/6} e^{i\pi/3} J_{1/3}(y) = e^{i\pi/6} J_{1/3}(y)
$$
取其模的平方：
$$
|I_{1/3}(iy)|^2 = |e^{i\pi/6}|^2 |J_{1/3}(y)|^2 = J_{1/3}(y)^2
$$
（假设 $y$ 是实数，所以 $J_{1/3}(y)$ 是实数）。积分变成了：
$$
L = \lim_{Y\to\infty} \frac{1}{Y} \int_{0}^{Y} y J_{1/3}(y)^2 dy
$$
对于大的 $y$，被积函数 $y J_{1/3}(y)^2$ 的行为由 $J_{1/3}(y)$ 的渐近形式决定：
$$
y J_{1/3}(y)^2 \sim y \left[ \sqrt{\frac{2}{\pi y}} \cos\left(y - \frac{\pi}{6} - \frac{\pi}{4}\right) \right]^2 = \frac{2}{\pi} \cos^2\left(y - \frac{5\pi}{12}\right)
$$
这是一个周期性[振荡](@entry_id:267781)的函数，其平均值是 $\frac{2}{\pi} \cdot \frac{1}{2} = \frac{1}{\pi}$。因此，当 $Y \to \infty$时，积分 $\int_0^Y y J_{1/3}(y)^2 dy$ 的主导项是 $\frac{Y}{\pi}$。所以，极限值为：
$$
L = \lim_{Y\to\infty} \frac{1}{Y} \left( \frac{Y}{\pi} + O(1) \right) = \frac{1}{\pi}
$$
这个结果漂亮地连接了[修正贝塞尔函数](@entry_id:184177)和普通贝塞尔函数的渐近世界，展示了它们之间深刻的内在联系。