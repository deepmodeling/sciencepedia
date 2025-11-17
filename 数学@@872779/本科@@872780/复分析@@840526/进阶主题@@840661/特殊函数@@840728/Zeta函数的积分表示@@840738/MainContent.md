## 引言
黎曼Zeta函数$\zeta(s)$是[解析数论](@entry_id:158402)乃至整个数学领域的基石之一，其定义为一个简单的无穷级数，却蕴含着关于素数分布的深刻奥秘。然而，其级数定义$\sum_{n=1}^\infty n^{-s}$仅在复半平面$\text{Re}(s) > 1$上收敛，这极大地限制了我们对其全局性质的探索。为了突破这一边界，数学家们发展出了强大的解析延拓技术，其中，积分表示法是最为核心和富有洞察力的工具之一。

本文旨在系统地探讨[Zeta函数的积分表示](@entry_id:171633)，揭示它如何成为连接离散求和与连续积分、数论与复分析、纯粹数学与理论物理的桥梁。我们将看到，这一表示不仅为Zeta函数提供了在整个复平面上的定义，还成为计算其特殊值、证明其基本性质（如函数方程）的钥匙。

在接下来的内容中，读者将踏上一段从基础到应用的探索之旅。在“原理与机制”一章中，我们将详细推导Zeta函数与Gamma函数的积分关联，分析其收敛性，并展示如何利用它实现解析延拓。随后，在“应用与跨学科联系”一章，我们将见证这一数学工具在解决量子统计物理中的黑体辐射问题，以及在揭示数论中[伯努利数](@entry_id:177442)与Zeta值之间惊人关系等方面的威力。最后，“动手实践”部分将提供具体的计算问题，帮助读者巩固所学，将理论知识转化为解决问题的能力。

## 原理与机制

继前一章对黎曼Zeta函数$\zeta(s)$的基本属性进行介绍之后，本章将深入探讨其分析理论中的一个核心工具：积分表示。通过将$\zeta(s)$与Gamma函数$\Gamma(s)$联系起来，积分表示不仅为计算与$\zeta$函数相关的特定积分值提供了途径，更重要的是，它为我们将$\zeta$函数从其级数定义收敛的半平面（$\text{Re}(s) > 1$）解析延拓至整个复平面奠定了基础。本章将系统地推导这一表示，分析其收敛性，并展示如何利用它来揭示$\zeta$函数的深刻性质。

### Zeta 函数与 Gamma 函数的积分关联

我们首先建立$\zeta(s)$与$\Gamma(s)$之间的积分联系。回忆一下，对于[复变量](@entry_id:175312)$s$且其实部$\text{Re}(s) > 0$，Gamma函数由积分定义：
$$
\Gamma(s) = \int_0^\infty t^{s-1} e^{-t} dt
$$
而对于$\text{Re}(s) > 1$，黎曼Zeta函数由Dirichlet级数定义：
$$
\zeta(s) = \sum_{n=1}^\infty \frac{1}{n^s}
$$
为了将这两个函数联系起来，我们考察一个特定的积分形式。考虑积分$\int_0^\infty x^{s-1} e^{-nx} dx$，其中$n$是一个正整数。通过一个简单的变量代换，令$t = nx$，则$x = t/n$且$dx = dt/n$。积分上下限不变，我们得到：
$$
\int_0^\infty x^{s-1} e^{-nx} dx = \int_0^\infty \left(\frac{t}{n}\right)^{s-1} e^{-t} \frac{dt}{n} = \frac{1}{n^s} \int_0^\infty t^{s-1} e^{-t} dt = \frac{\Gamma(s)}{n^s}
$$
这个优美的结果揭示了Gamma函数积分与Zeta[函数级数](@entry_id:139536)项之间的直接关系。

现在，我们可以将这个关系对所有正整数$n$求和。假设我们可以交换求和与积分的次序，对于$\text{Re}(s) > 1$，我们得到 [@problem_id:2246956]：
$$
\Gamma(s) \zeta(s) = \Gamma(s) \sum_{n=1}^\infty \frac{1}{n^s} = \sum_{n=1}^\infty \frac{\Gamma(s)}{n^s} = \sum_{n=1}^\infty \int_0^\infty x^{s-1} e^{-nx} dx
$$
交换次序后，表达式变为：
$$
\Gamma(s) \zeta(s) = \int_0^\infty x^{s-1} \left( \sum_{n=1}^\infty e^{-nx} \right) dx
$$
括号内的级数是一个首项为$e^{-x}$、[公比](@entry_id:275383)为$e^{-x}$的几何级数。由于积分变量$x$在$(0, \infty)$上，我们有$0  e^{-x}  1$，因此[级数收敛](@entry_id:142638)，其和为：
$$
\sum_{n=1}^\infty (e^{-x})^n = \frac{e^{-x}}{1 - e^{-x}} = \frac{1}{e^x - 1}
$$
将此结果代回积分，我们便得到了黎曼Zeta函数最著名的积分表示之一：
$$
\Gamma(s)\zeta(s) = \int_0^\infty \frac{x^{s-1}}{e^x - 1} dx
$$
这个恒等式将数论中的离散求和（$\zeta$函数）与分析中的连续积分联系在了一起，是[解析数论](@entry_id:158402)中的一个基石。

### [收敛性分析](@entry_id:151547)：积分表示的有效范围

尽管上述推导形式上简洁明了，但其有效性依赖于一个关键假设：求和与积分次序的可交换性，以及右侧积分本身的收敛性。现在我们必须严格确定此积分表示成立的条件，即确定积分$I(s) = \int_0^\infty \frac{x^{s-1}}{e^x - 1} dx$的收敛域。

这是一个[瑕积分](@entry_id:138794)，我们需要分别考察积分区间两端（$x \to 0^+$和$x \to \infty$）的收敛情况 [@problem_id:2246979]。令$s = \sigma + i\tau$，其中$\sigma = \text{Re}(s)$。积分的[绝对收敛](@entry_id:146726)性取决于积分$\int_0^\infty |\frac{x^{s-1}}{e^x - 1}| dx$的收敛性。由于$|x^{s-1}| = |e^{(s-1)\ln x}| = e^{(\sigma-1)\ln x} = x^{\sigma-1}$，被积函数的模为$\frac{x^{\sigma-1}}{e^x - 1}$。

**1. 在$x \to \infty$处的行为**

当$x$很大时，$e^x - 1$的行为与$e^x$非常接近。更精确地说，$e^x - 1 \sim e^x$。因此，被积函数的行为类似于$x^{\sigma-1}e^{-x}$。由于指数衰减项$e^{-x}$会压倒任何[多项式增长](@entry_id:177086)项$x^{\sigma-1}$，积分$\int_1^\infty x^{\sigma-1}e^{-x} dx$对任意实数$\sigma$都是收敛的。因此，原积分在无穷远处的收敛性对$\text{Re}(s)$没有任何限制 [@problem_id:2246980]。

**2. 在$x \to 0^+$处的行为**

当$x$趋向于0时，情况则大为不同。我们使用[指数函数](@entry_id:161417)的泰勒展开：$e^x - 1 = x + \frac{x^2}{2!} + O(x^3)$。因此，当$x \to 0^+$时，$e^x - 1 \sim x$。被积函数的行为近似为：
$$
\frac{x^{\sigma-1}}{e^x - 1} \sim \frac{x^{\sigma-1}}{x} = x^{\sigma-2}
$$
我们知道，[p-积分](@entry_id:136518)$\int_0^\delta x^p dx$（其中$\delta > 0$）收敛当且仅当$p > -1$。在我们的例子中，$p = \sigma - 2$，因此[收敛条件](@entry_id:166121)为$\sigma - 2 > -1$，即$\sigma > 1$ [@problem_id:2246954]。

综合两方面分析，我们得出结论：积分$\int_0^\infty \frac{x^{s-1}}{e^x - 1} dx$收敛当且仅当$\text{Re}(s) > 1$。这恰好是$\zeta(s)$的级数定义收敛的区域。因此，恒等式$\Gamma(s)\zeta(s) = \int_0^\infty \frac{x^{s-1}}{e^x - 1} dx$在$\text{Re}(s) > 1$的半平面内是严格成立的。当$\text{Re}(s) \le 1$时，积分由于在原点附近的奇异性而发散，故此表示失效 [@problem_id:2246953]。

有趣的是，我们可以将此[积分的收敛](@entry_id:187300)域$D_\zeta = \{s \in \mathbb{C} : \text{Re}(s) > 1\}$与Gamma函数自身的[积分收敛](@entry_id:139742)域$D_\Gamma = \{s \in \mathbb{C} : \text{Re}(s) > 0\}$进行比较。显然，$D_\zeta$是$D_\Gamma$的一个[真子集](@entry_id:152276) [@problem_id:2246955]。这表明，是分母中的$-1$项（即$\zeta$函数的结构）而非$\Gamma$函数的结构，对[积分收敛](@entry_id:139742)域施加了更强的限制。

### 相关积分与Dirichlet Eta函数

我们建立的积分方法具有广泛的适用性。例如，考虑一个结构相似的积分：
$$
I(s) = \int_0^\infty \frac{x^{s-1}}{e^x + 1} dx
$$
我们可以采用完全相同的策略。首先，将被积函数中的分式改写并展开为几何级数。对于$x>0$，我们有$0  e^{-x}  1$，因此：
$$
\frac{1}{e^x + 1} = \frac{e^{-x}}{1 + e^{-x}} = e^{-x} \sum_{k=0}^\infty (-e^{-x})^k = \sum_{k=0}^\infty (-1)^k e^{-(k+1)x}
$$
令$n = k+1$，级数变为$\sum_{n=1}^\infty (-1)^{n-1} e^{-nx}$。将其代入积分并交换求和与积分次序（在$\text{Re}(s)>1$时同样成立），我们得到 [@problem_id:2246976]：
$$
I(s) = \sum_{n=1}^\infty (-1)^{n-1} \int_0^\infty x^{s-1} e^{-nx} dx = \sum_{n=1}^\infty (-1)^{n-1} \frac{\Gamma(s)}{n^s}
$$
$$
I(s) = \Gamma(s) \sum_{n=1}^\infty \frac{(-1)^{n-1}}{n^s}
$$
这个[交错级数](@entry_id:143758)定义了另一个重要的函数，即[Dirichlet eta函数](@entry_id:183462)$\eta(s)$。因此，$I(s) = \Gamma(s)\eta(s)$。$\eta(s)$与$\zeta(s)$之间有一个简单的关系：
$$
\eta(s) = \sum_{n=1}^\infty \frac{(-1)^{n-1}}{n^s} = \left( \sum_{n=1}^\infty \frac{1}{n^s} \right) - 2 \left( \sum_{k=1}^\infty \frac{1}{(2k)^s} \right) = \zeta(s) - \frac{2}{2^s} \zeta(s) = (1 - 2^{1-s})\zeta(s)
$$
最终，我们得到：
$$
\int_0^\infty \frac{x^{s-1}}{e^x + 1} dx = (1 - 2^{1-s})\Gamma(s)\zeta(s)
$$
值得注意的是，$\eta(s)$的级数定义在更广的区域$\text{Re}(s) > 0$上收敛。因此，关系式$\zeta(s) = (1-2^{1-s})^{-1}\eta(s)$为$\zeta(s)$提供了一个到半平面$\text{Re}(s) > 0$（除去$s=1+2k\pi i/\ln 2$处的点）的解析延拓。

### [解析延拓](@entry_id:147225)：超越收敛边界

我们已经看到，积分表示$\Gamma(s)\zeta(s) = \int_0^\infty \frac{x^{s-1}}{e^x-1} dx$仅在$\text{Re}(s) > 1$时有效。然而，$\zeta(s)$本身可以被延拓为一个在整个复平面上（除$s=1$处的单极点外）的[亚纯函数](@entry_id:171058)。积分方法是否也能帮助我们实现这种延拓呢？答案是肯定的，其关键在于处理导致积分发散的“病灶”——原点处的奇异性。

#### 通过减去奇异项进行延拓

积分在$\text{Re}(s) \le 1$时发散的根源在于$x \to 0$时被积函数的行为。为了更精确地分析这一点，我们使用函数$\frac{1}{e^x-1}$在$x=0$附近的Laurent展开式，这与[Bernoulli数](@entry_id:177442)$B_k$密切相关：
$$
\frac{1}{e^x - 1} = \frac{1}{x} - \frac{1}{2} + \frac{B_2}{2!}x - \frac{B_4}{4!}x^3 + \dots = \frac{1}{x} - \frac{1}{2} + \frac{1}{12}x - \frac{1}{720}x^3 + \dots
$$
将此展开式代入积分（并暂时忽略严谨性），我们看到：
$$
\Gamma(s)\zeta(s) \approx \int_0^\delta x^{s-1}\left(\frac{1}{x} - \frac{1}{2} + \dots\right)dx = \int_0^\delta \left(x^{s-2} - \frac{1}{2}x^{s-1} + \dots\right)dx
$$
正是第一项$x^{s-2}$导致了积分在$\text{Re}(s) \le 1$时发散。这个简单的观察启发了一个深刻的想法：如果我们从被积函数中减去这些导致发散的奇异项，得到的修正积分或许会在更广阔的区域上收敛。

这个想法不仅可以用于延拓，还可以用来揭示延拓后函数的值。例如，我们来考察$I(s) = \Gamma(s)\zeta(s)$在$s=0$处的行为。将积分拆分为$\int_0^1 + \int_1^\infty$，其中$\int_1^\infty$的部分定义了一个[整函数](@entry_id:176232)。对于$\int_0^1$部分，我们有：
$$
\int_0^1 \frac{x^{s-1}}{e^x-1} dx = \int_0^1 x^{s-1} \left(\frac{1}{x} - \frac{1}{2} + O(x)\right) dx = \int_0^1 x^{s-2} dx - \frac{1}{2}\int_0^1 x^{s-1} dx + \dots
$$
对于$\text{Re}(s)>1$，这等于$\frac{1}{s-1} - \frac{1}{2s} + (\text{在 } s=0 \text{ 附近解析的部分})$。这个表达式给出了$I(s)$在$s=0$附近的Laurent展开。可以看到，$I(s)$在$s=0$有一个简单极点，其留数为$-\frac{1}{2}$ [@problem_id:2246949]。另一方面，我们知道$\Gamma(s)$在$s=0$有一个留数为1的简单极点（$\Gamma(s) \sim 1/s$），且$\zeta(s)$在$s=0$处是解析的。因此$I(s) = \Gamma(s)\zeta(s) \sim \frac{\zeta(0)}{s}$。比较留数，我们立即得到一个深刻的结果：$\zeta(0) = -1/2$。

更进一步，我们可以构造一个收敛区域更广的积分。考虑下面的修正积分：
$$
I_{\text{reg}}(s) = \int_{0}^{\infty} x^{s-1} \left( \frac{1}{e^x - 1} - \frac{1}{x} + \frac{1}{2} \right) dx
$$
我们分析其收敛性 [@problem_id:2246963]：
- **当$x \to 0^+$时**，括号内的表达式行为如$\frac{x}{12}$。因此被积函数行为如$x^{s-1} \cdot \frac{x}{12} = \frac{1}{12}x^s$。[积分收敛](@entry_id:139742)需要$\text{Re}(s) > -1$。
- **当$x \to \infty$时**，括号内的表达式$(\frac{1}{e^x-1} - \frac{1}{x} + \frac{1}{2})$实际上呈指数级衰减。因此，被积函数$x^{s-1}$乘以一个指数衰减项，使得积分在无穷远处对任意复数$s$都收敛。

结合两点，我们发现这个修正后的积分在半平面$\text{Re}(s) > -1$内收敛。这个积分定义了$\Gamma(s)\zeta(s)$在此区域的解析延拓。通过不断减去[Laurent级数](@entry_id:170999)的更多项，原则上我们可以将[收敛域](@entry_id:269722)一步步向左推进。

#### Hankel 围[线积分](@entry_id:141417)：全局[解析延拓](@entry_id:147225)

逐项减去奇异项的方法虽然有效，但略显笨拙。一个更强大、更统一的方法是使用复分析中的围线积分来从一开始就避开[奇点](@entry_id:137764)。这引出了$\zeta(s)$的Hankel围[线积分](@entry_id:141417)表示。

考虑如下积分：
$$
\zeta(s) = -\frac{\Gamma(1-s)}{2\pi i} \int_{H} \frac{(-z)^{s-1}}{e^{z}-1} dz
$$
这里的积分路径$H$是一个**Hankel围线**：它从$+\infty$处沿无穷贴近正[实轴](@entry_id:148276)上方的路径行进至原点附近，逆时针绕原点一周，然后沿无穷贴近正[实轴](@entry_id:148276)下方的路径返回到$+\infty$。项$(-z)^{s-1}$定义为$\exp((s-1)\text{Log}(-z))$，其中对数函数$\text{Log}$的[分支切割](@entry_id:174657)选择在正[实轴](@entry_id:148276)上。这条路径的精妙之处在于它“包裹”了导致我们麻烦的$x=0$点，但从未穿过它，从而避免了[奇点](@entry_id:137764)。这个积分对所有$s \in \mathbb{C}$都收敛，因此为$\zeta(s)$提供了一个全局的解析延拓（除了由$\Gamma(1-s)$引入的在正整数处的极点，但这些极点会被积分的零点抵消）。

这个强大的表示不仅完成了延拓，还能用来推导$\zeta$函数的基本性质。作为一个绝佳的例子，我们用它来计算$\zeta(s)$在$s=1$处的留数 [@problem_id:2246974]。

当$s \to 1$时，我们可以分析此表达式的行为。首先，Hankel围线积分可以被看作是沿正实轴上下两侧路径的积分之差。在上侧路径，$z=x+i\epsilon$，$\arg(-z) \to -\pi$；在下侧路径，$z=x-i\epsilon$，$\arg(-z) \to \pi$。小圆环绕原点的积分在$\text{Re}(s)>1$时趋于零。因此，积分可以写为：
$$
\int_H \frac{(-z)^{s-1}}{e^z-1} dz = \int_\infty^0 \frac{x^{s-1}e^{-i\pi(s-1)}}{e^x-1}dx + \int_0^\infty \frac{x^{s-1}e^{i\pi(s-1)}}{e^x-1}dx
$$
$$
= (e^{i\pi(s-1)} - e^{-i\pi(s-1)}) \int_0^\infty \frac{x^{s-1}}{e^x-1}dx = 2i\sin(\pi(s-1)) \int_0^\infty \frac{x^{s-1}}{e^x-1}dx
$$
代入$\zeta(s)$的表示式，并利用$\sin(\pi(s-1)) = -\sin(\pi s)$和Gamma函数的[反射公式](@entry_id:198841)$\Gamma(s)\Gamma(1-s) = \frac{\pi}{\sin(\pi s)}$，我们得到：
$$
\zeta(s) = -\frac{\Gamma(1-s)}{2\pi i} \cdot (2i(-\sin(\pi s))) \int_0^\infty \frac{x^{s-1}}{e^x-1}dx = \frac{\Gamma(1-s)\sin(\pi s)}{\pi} \int_0^\infty \frac{x^{s-1}}{e^x-1}dx
$$
$$
\zeta(s) = \frac{1}{\Gamma(s)} \int_0^\infty \frac{x^{s-1}}{e^x-1}dx
$$
令人惊讶的是，我们通过一个适用于所有$s$的表示，又回到了我们最初的、仅在$\text{Re}(s)>1$中推导出的积分表示！但现在，这个关系式在[解析延拓](@entry_id:147225)的意义下是全局成立的。

为了求$s=1$处的留数，我们计算$\lim_{s \to 1}(s-1)\zeta(s)$。我们需要分析积分在$s \to 1$时的行为。如前所述，积分的主要奇异部分来自$\int_0^\delta x^{s-2}dx = \frac{\delta^{s-1}}{s-1}$。因此，$\int_0^\infty \frac{x^{s-1}}{e^x-1}dx$在$s=1$处有一个简单极点，其留数为1。即，在$s=1$附近，$\int_0^\infty \frac{x^{s-1}}{e^x-1}dx = \frac{1}{s-1} + A(s)$，其中$A(s)$在$s=1$解析。
于是：
$$
\text{Res}_{s=1} \zeta(s) = \lim_{s \to 1} (s-1)\zeta(s) = \lim_{s \to 1} \frac{s-1}{\Gamma(s)} \left( \frac{1}{s-1} + A(s) \right) = \lim_{s \to 1} \left( \frac{1}{\Gamma(s)} + \frac{(s-1)A(s)}{\Gamma(s)} \right)
$$
由于$\Gamma(1)=1$且$A(s)$在$s=1$解析，第二项在极限中为零。我们得到：
$$
\text{Res}_{s=1} \zeta(s) = \frac{1}{\Gamma(1)} = 1
$$
这一经典结果的推导，完美地展示了积分表示法在[解析延拓](@entry_id:147225)和揭示黎曼Zeta函数深刻结构方面的强大威力。