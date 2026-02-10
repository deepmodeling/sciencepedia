## 引言
当两个[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)碰撞或一颗[大质量恒星](@keyword=massive_stars|lang=zh-CN|style=Feynman)爆炸时，这一事件会在宇宙中掀起涟漪。这些引力波携带着关于这场灾变“新闻”，但我们如何才能精确地解读这则宇宙信息呢？挑战在于定义和量化这些[时空结构](@keyword=spacetime_structure|lang=zh-CN|style=Feynman)本身的畸变所携带的信息和能量。本文将介绍邦迪[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)，这是源自广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的一个深刻概念，它充当着[引力辐射](@keyword=gravitational_radiation|lang=zh-CN|style=Feynman)的语言。通过理解[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)，我们能够破译来自宇宙最剧烈事件的广播报道。

第一部分“原理与机制”将带领我们前往[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的边缘，将[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)定义为渐近[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)的变化。我们将探讨它在数学上如何从邦迪剪切导出，以及它如何与引力波带走的能量、动量和角动量直接相关。

随后，“应用与跨学科联系”部分将展示[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)在实践中的威力。我们将看到它如何充当[能量损失](@keyword=energy_loss|lang=zh-CN|style=Feynman)的宇宙会计，解释辐射系统受到的“反冲”，并揭示[引力记忆效应](@keyword=gravitational_memory_effect|lang=zh-CN|style=Feynman)——一种留在[时空](@keyword=space_time|lang=zh-CN|style=Feynman)上的永久性伤疤。这一部分还将[升华](@keyword=sublimation|lang=zh-CN|style=Feynman)这个概念，将其与宇宙的[基本对称性](@keyword=fundamental_symmetries|lang=zh-CN|style=Feynman)及其在解决[黑洞信息](@keyword=black_hole_information|lang=zh-CN|style=Feynman)佯谬中的潜在作用联系起来，从而架起经典[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)与[量子引力](@keyword=quantum_gravity|lang=zh-CN|style=Feynman)之间的桥梁。

## 原理与机制

想象一下，在一个风平浪静的日子里，你站在田野里。突然，一阵强风吹过。是什么告诉你风在吹？不是空气本身——空气一直都在那里。是*变化*：沙沙作响的树叶，皮肤上的感觉，云的运动。风的“新闻”在于它的运动及其所产生的影响。

与此非常相似，穿过[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的引力波并非一块飞过的物质。[时空](@keyword=space_time|lang=zh-CN|style=Feynman)无处不在。引力波的“新闻”在于[时空](@keyword=space_time|lang=zh-CN|style=Feynman)状态如何*变化*。要理解这一点，我们必须前往一个非常特殊的地方：宇宙的边缘，一个被称为**未来类光无穷远**（future null infinity）或 $\mathscr{I}^+$ 的概念性边界。这是所有外行辐射的最终目的地，是宇宙投射其最剧烈事件的宇宙银幕。

### [天球](@keyword=celestial_sphere|lang=zh-CN|style=Feynman)银幕及其图像

为了研究辐射，我们希望离源无限远，那里的波纯净无扰。在 $\mathscr{I}^+$，我们可以建立一个非常适合此目的的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)，即 Bondi-Sachs [坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman) $(u, r, \theta, \phi)$。这里，$r$ 是距离的度量，而 $(\theta, \phi)$ 是我们熟悉的、在源周围勾画出“[天球](@keyword=celestial_sphere|lang=zh-CN|style=Feynman)”的角度。关键坐标是 $u = t - r$，即**[推迟时间](@keyword=retarded_time|lang=zh-CN|style=Feynman)**。可以把它想象成[波前](@keyword=wavefront|lang=zh-CN|style=Feynman)上的一个标签。同一个球面上具有相同 $u$ 值的所有点，都在同一瞬间接收到来自某个事件的“新闻”。

那么，这个[天球](@keyword=celestial_sphere|lang=zh-CN|style=Feynman)银幕上的“图像”是什么呢？它是对[时空](@keyword=space_time|lang=zh-CN|style=Feynman)如何被扭曲的描述。对于引力波来说，这种扭曲是一种[潮汐力](@keyword=tidal_forces|lang=zh-CN|style=Feynman)；它拉伸和挤压物体。我们用一个称为**邦迪剪切**（Bondi shear）的量 $\sigma(u, \theta, \phi)$ 来捕捉这一点。你可以这样想象剪切：想象一个由尘埃粒子组成的完美圆形漂浮在太空中。当引力波经过时，剪切描述了这个圆形如何被扭曲成一个椭圆，在一个方向上被挤压，在另一个方向上被拉伸。复数 $\sigma$ 巧妙地编码了[天球](@keyword=celestial_sphere|lang=zh-CN|style=Feynman)上每一点、在每个[推迟时间](@keyword=retarded_time|lang=zh-CN|style=Feynman) $u$ 时刻这个椭圆的方向和离心率。

### “新闻”即是变化

如果一个系统静静地待着，完全不辐射，那么[天球](@keyword=celestial_sphere|lang=zh-CN|style=Feynman)上的剪切模式将是静态的。图像会是凝固的。什么也没有发生。但如果发生了一场灾难性事件——例如两个[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)相互旋入——[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的涟漪会向外传播。当它们到达我们的[天球](@keyword=celestial_sphere|lang=zh-CN|style=Feynman)银幕时，剪切模式会随时间变化。扭曲的椭圆会[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)、旋转和演化。

这正是问题的核心。引力波的物理实在，即能量正从源头被带走的这一“新闻”本身，就包含在*剪切的时间[导数](@keyword=derivative|lang=zh-CN|style=Feynman)*中。我们给这个深刻的量起了一个简单而优美的名字：**[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)**（news function），$N(u, \theta, \phi)$。

$$
N(u, \theta, \phi) = \frac{\partial \sigma(u, \theta, \phi)}{\partial u}
$$

如果[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman) $N$ 为零，剪切 $\sigma$ 就不随时间变化。没有新闻抵达。没有辐射经过。如果 $N$ 非零，剪切就在变化，而这种变化*就是*引力波。它是来自源的信息和能量的载体。在非常真实的意义上，[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)*就是*无穷远处的[辐射场](@keyword=radiation_field|lang=zh-CN|style=Feynman)。[时空曲率](@keyword=spacetime_curvature|lang=zh-CN|style=Feynman)本身的主导分量，即外尔标量 (Weyl scalar) $\Psi_4^0$，与[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)复共轭的时间[导数](@keyword=derivative|lang=zh-CN|style=Feynman)成正比（$\Psi_4^0 = -\dot{\bar{N}}$），[@problem_id:917635] 中的原理解释了这一美妙关系。新闻不仅仅是一个类比；它是以光速抵达的物理时空曲率。

### 能量流：为产生涟漪付出的代价

在[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中制造涟漪需要消耗能量。要让一个源产生引力波，它必须放弃自身的一部分质能。[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)精确地告诉我们这个量是多少。总[辐射功率](@keyword=radiation_power|lang=zh-CN|style=Feynman)，即源的质能损失率，由异常简洁的[邦迪质量损失公式](@keyword=bondi_mass_loss_formula|lang=zh-CN|style=Feynman)给出：

$$
P(u) = -\frac{dM_B}{du} = \frac{1}{4\pi} \int_{S^2} |N(u, \theta, \phi)|^2 d\Omega
$$

这里，$M_B$ 是系统的总质能（[邦迪质量](@keyword=bondi_mass|lang=zh-CN|style=Feynman)），积分是在整个[天球](@keyword=celestial_sphere|lang=zh-CN|style=Feynman)上进行的。

这不是很奇妙吗？[辐射功率](@keyword=radiation_power|lang=zh-CN|style=Feynman)与新闻的模的平方成正比，并在整个天穹上进行平均。这与[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)中光的功率与电场强度的平方成正比完全类似。一个强烈的“新闻报道”——即一个大的 $|N|$——意味着巨大的能量正在宇宙中广播出去。

天体物理系统可以通过不同方式进行辐射。一个双星系统可能会产生连续的周期性波，导致如 [@problem_id:917542] 中计算的稳定的、[时间平均](@keyword=time_averaging|lang=zh-CN|style=Feynman)的功率损失。相比之下，两个[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的剧烈并合会产生短暂而强烈的辐射爆发。通过对这种爆发期间的功率进行积分，我们可以求出转换成引力波的总质能——这可能相当于我们太阳质量的数倍，并且在不到一秒的时间内全部释放 [@problem_id:1001224] [@problem_id:1010028]。$|N|^2$ 在[天球](@keyword=celestial_sphere|lang=zh-CN|style=Feynman)上的具体模式完全取决于源的性质，通过分析这些模式，我们可以推断出是哪种宇宙引擎产生了它们 [@problem_id:503428]。

### 波的反冲与扭转：辐射动量

波带走的不仅仅是能量。它们还可以携带[线动量](@keyword=linear_momentum|lang=zh-CN|style=Feynman)和角动量。这会带来惊人的后果。

想象一个系统，它在一个方向上辐射的引力波比另一个方向更强。就像火箭通过喷射废气来推动自己前进一样，这个系统会发生反冲。它会受到自身[引力辐射](@keyword=gravitational_radiation|lang=zh-CN|style=Feynman)的“反冲”（kick）。[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)如何解释这一点呢？沿某个方向（比如 $z$ 方向）的线[动量通量](@keyword=momentum_flux|lang=zh-CN|style=Feynman)由以下公式给出：

$$
\frac{dP^z}{du} = \frac{1}{4\pi} \int_{S^2} |N(u, \theta, \phi)|^2 \cos\theta \, d\Omega
$$

注意多出来的因子 $\cos\theta$，它是方向矢量在 $z$ 方向上的分量。要使积分为非零，辐射模式 $|N|^2$ 在北半球（$\cos\theta > 0$）和南半球（$\cos\theta  0$）之间不能对称。这要求源具有一种特殊的非对称性，通常源于不同辐射模式之间的干涉，例如在 [@problem_id:877654] 中探讨的 `l=2` 和 `l=3` 模式。结果是产生了净辐射动量，导致源在太空中加速——一个引力火箭！

类似地，如果波以某种特定的方式“旋转”，它们可以带走角动量，导致源自旋减慢。计算这个的公式更为精妙，它不仅取决于某一瞬间的新闻 $N$，还取决于瞬时新闻与所有过去新闻积累的剪切 $\sigma$ 之间的相位关系 [@problem_id:877691]。这告诉我们，波对其自身历史的“记忆”对于带走自旋至关重要。

### 解读新闻：涟漪在说什么

所以，这个奇妙的[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman) $N$ 告诉我们从一个系统流出的能量、动量和角动量。但又是什么决定了[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)本身呢？新闻是*关于*源的报告。这种联系是通过**辐射[多极矩](@keyword=multipole_moments|lang=zh-CN|style=Feynman)**建立的。

正如一个复杂的声音可以分解为纯音的总和（其[频谱](@keyword=frequency_spectrum|lang=zh-CN|style=Feynman)），[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)的复杂角向模式也可以分解为称为**自旋加权球谐函数** ${}_{-2}Y_{lm}(\theta, \phi)$ 的[基本模式](@keyword=fundamental_mode|lang=zh-CN|style=Feynman)的总和。

$$
N(u, \theta, \phi) = \sum_{l=2}^{\infty} \sum_{m=-l}^{l} N_{lm}(u) {}_{-2}Y_{lm}(\theta, \phi)
$$

奇妙之处在于，每个系数 $N_{lm}(u)$ 都与源的行为直接相关。源的形状变化由**质量[多极矩](@keyword=multipole_moments|lang=zh-CN|style=Feynman)** $M_{lm}(u)$ 描述，其[旋转流](@keyword=rotating_flows|lang=zh-CN|style=Feynman)由**流[多极矩](@keyword=multipole_moments|lang=zh-CN|style=Feynman)** $S_{lm}(u)$ 描述。它们之间的关系直接得惊人 [@problem_id:877660]：

$$
N_{lm}(u) = \frac{d^2 M_{lm}(u)}{du^2} - i \frac{d S_{lm}(u)}{du}
$$

我们从远处接收到的新闻是源的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)形状的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)和其[旋转流](@keyword=rotating_flows|lang=zh-CN|style=Feynman)的一阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)！这是[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)基本原理——加速[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)产生辐射——的引力类似物。在这里，加速的质量和变化的[质量流](@keyword=mass_flow|lang=zh-CN|style=Feynman)辐射引力波。通过测量新闻，我们实际上是在观看一部关于源最内在动力学的电影。

### 持久的印记：[记忆效应](@keyword=memory_effect|lang=zh-CN|style=Feynman)

一阵风吹过之后，树叶可能会停在一个新的位置。风已经消失，但它留下了永久性的改变。引力波也能做到同样的事情。

[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman) $N$ 是剪切的*[导数](@keyword=derivative|lang=zh-CN|style=Feynman)*，$N = \partial_u \sigma$。因此，在一阵波爆发经过后，剪切的总变化是新闻在整个事件期间的积分：

$$
\Delta\sigma = \sigma(u=+\infty) - \sigma(u=-\infty) = \int_{-\infty}^{\infty} N(u, \theta, \phi) \, du
$$

对于一个简单的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)波，这个积分可能为零。但对于许多现实事件，例如碰撞的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)或超[新星爆发](@keyword=nova_explosion|lang=zh-CN|style=Feynman)，新闻的总积分是非零的。这导致了剪切的永久性变化，$\Delta\sigma$。这就是**[引力波记忆效应](@keyword=gravitational_wave_memory_effect|lang=zh-CN|style=Feynman)** [@problem_id:219352]。一圈探测器在被引力波扰动后，不会恢复成圆形，而是会留下一个永久扭曲的椭圆形。[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身因波的通过而被永久地留下了折痕。这种效应是爱因斯坦理论非[线性性质](@keyword=linearity_property|lang=zh-CN|style=Feynman)的深刻标志，并成为创造它的事件的一座永久丰碑。

从告诉我们离开恒星的能量，到在[时空结构](@keyword=spacetime_structure|lang=zh-CN|style=Feynman)上留下永久的伤疤，[新闻函数](@keyword=news_function|lang=zh-CN|style=Feynman)是[引力辐射](@keyword=gravitational_radiation|lang=zh-CN|style=Feynman)故事中的核心角色。它是一个具有深刻美感和统一性的概念，不仅适用于引力的自旋为2的波，也适用于任何[无质量场](@keyword=massless_fields|lang=zh-CN|style=Feynman)的辐射 [@problem_id:877667]。通过学习阅读这些宇宙新闻报道，我们正在为宇宙打开一扇新的窗户，聆听[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身的交响乐。