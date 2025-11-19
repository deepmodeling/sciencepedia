## 引言
在[统计力](@entry_id:194984)学中，精确计算由[费米子](@entry_id:146235)（如[金属中的电子](@entry_id:138687)）组成的量子系统的宏观性质是一项核心任务。内能、[热容](@entry_id:137594)、化学势等关键[热力学](@entry_id:141121)量通常通过包含[费米-狄拉克分布](@entry_id:138909)函数的积分来确定。然而，在非零温度下，该分布函数复杂的形式使得这些积分大多没有解析解，这构成了一个重要的理论挑战。我们如何才能在低温下系统地、精确地分析这些系统的行为呢？

[索末菲展开](@entry_id:149655)（Sommerfeld expansion）为解决这一难题提供了强大而优雅的理论工具。它是一种在低温极限下 ($k_B T \ll \epsilon_F$) 对费米积分进行近似计算的系统方法，深刻揭示了系统的[热力学性质](@entry_id:146047)如何由[费米能级](@entry_id:143215)附近的低能激发所主导。

本文将系统地引导读者掌握[索末菲展开](@entry_id:149655)的精髓。在“原理与机制”一章中，我们将深入探讨其数学推导，揭示其依赖于费米函数导数峰值特性的物理本质，并阐明其在[计算化学](@entry_id:143039)势和[电子热容](@entry_id:144815)等基本问题中的应用。接着，在“应用与跨学科联系”一章中，我们将展示该理论如何被广泛应用于解释凝聚态物理中的输运和磁学现象，甚至延伸到天体物理学中对[白矮星](@entry_id:159122)结构的描述。最后，“动手实践”部分将通过具体问题，帮助读者巩固理论知识并将其付诸实践。

让我们首先从[索末菲展开](@entry_id:149655)的基本原理与机制开始，探究其如何将复杂的积分问题转化为一个直观的物理图像和简洁的数学形式。

## 原理与机制

在研究由[费米子](@entry_id:146235)（如金属中的电子）组成的系统中，许多宏观[热力学性质](@entry_id:146047)，如内能和热容，都是通过对所有单粒子能态进行积分来确定的。这类积分通常具有以下形式：

$$ I = \int_{0}^{\infty} H(\epsilon) f(\epsilon) d\epsilon $$

其中，$H(\epsilon)$ 是一个与能量相关的函数，通常是[态密度](@entry_id:147894) $g(\epsilon)$ 与某个能量函数的乘积（例如，计算总能量时为 $H(\epsilon) = \epsilon g(\epsilon)$）。$f(\epsilon)$ 是[费米-狄拉克分布](@entry_id:138909)函数：

$$ f(\epsilon) = \frac{1}{\exp\left(\frac{\epsilon - \mu}{k_B T}\right) + 1} $$

这里，$\mu$ 是化学势，$T$ 是绝对温度，$k_B$ 是[玻尔兹曼常数](@entry_id:142384)。在绝对零度（$T=0$）时，[费米-狄拉克分布](@entry_id:138909)函数退化为一个简单的[阶跃函数](@entry_id:159192)：当 $\epsilon \le \epsilon_F$ 时 $f(\epsilon)=1$，当 $\epsilon > \epsilon_F$ 时 $f(\epsilon)=0$，其中 $\epsilon_F$ 是费米能，即零温下的化学势。在这种情况下，积分计算变得非常简单，积分上限直接取为 $\epsilon_F$ [@problem_id:2009215]。然而，当温度 $T > 0$ 时，由于 $f(\epsilon)$ 中存在指数项，这个积分通常没有解析解。

[索末菲展开](@entry_id:149655)（Sommerfeld expansion）为在低温条件下（即 $k_B T \ll \epsilon_F$）近似计算此类积分提供了一个强大而系统的方法。其核心思想是，在低温下，[热激发](@entry_id:275697)只会影响[费米能级](@entry_id:143215)附近一个狭窄能量范围内的[费米子](@entry_id:146235)，因此积分的[温度依赖性](@entry_id:147684)主要由被积函数在化学势 $\mu$ 附近的性质决定。

### 展开的核心：费米函数[导数的性质](@entry_id:141529)

[索末菲展开](@entry_id:149655)的巧妙之处在于利用了[费米-狄拉克分布](@entry_id:138909)函数导数的特殊性质。让我们考察函数 $g(\epsilon) = -\frac{\partial f}{\partial \epsilon}$。通过链式法则，我们可以得到：

$$ -\frac{\partial f}{\partial \epsilon} = \frac{1}{k_B T} \frac{\exp\left(\frac{\epsilon - \mu}{k_B T}\right)}{\left[\exp\left(\frac{\epsilon - \mu}{k_B T}\right) + 1\right]^2} $$

这个函数具有非常显著的特征。通过简单的代数变形，可以将其写成更对称的形式：

$$ -\frac{\partial f}{\partial \epsilon} = \frac{1}{4k_B T} \cosh^{-2}\left(\frac{\epsilon - \mu}{2k_B T}\right) $$

其中 $\cosh(x) = (\exp(x) + \exp(-x))/2$ 是双曲余弦函数。这个函数具有以下重要性质：

1.  **峰值特性**：它是一个以化学势 $\mu$ 为中心的尖锐峰。当 $\epsilon = \mu$ 时，它达到最大值 $\frac{1}{4k_B T}$。
2.  **能量宽度**：峰的宽度与热能 $k_B T$ 成正比。一个常用的衡量标准是半峰全宽（FWHM），即函数值为其最大值一半时对应的两个能量值之差。通过计算可以发现，这个宽度为 $4k_B T \arccosh(\sqrt{2})$，这表明能量的弥散范围直接由温度决定 [@problem_id:2009218]。
3.  **对称性**：该函数关于 $\epsilon = \mu$ 是一个偶函数。这意味着在化学势两侧能量相同距离处的函数值相等。
4.  **极限行为**：当温度 $T \to 0$ 时，这个峰变得无限高和无限窄，其总积分为1，因此它趋向于狄拉克 $\delta$ 函数 $\delta(\epsilon - \mu)$。

这些性质的物理意义是深远的：函数 $-\frac{\partial f}{\partial \epsilon}$ 就像一个“采样窗口”，它只在化学势 $\mu$ 附近一个宽度约为 $k_B T$ 的能量区间内有显著值。因此，任何与 $f(\epsilon)$ 相关的积分的温度依赖性，都可以通过考察被积函数在 $\mu$ 附近的局部行为来近似。

### [索末菲展开](@entry_id:149655)公式

通过对原积分进行[分部积分](@entry_id:136350)，并利用 $-\frac{\partial f}{\partial \epsilon}$ 的峰值特性，我们可以将被积函数 $H(\epsilon)$ 在 $\epsilon=\mu$ 处进行[泰勒展开](@entry_id:145057)。经过一系列数学推导，得到[索末菲展开](@entry_id:149655)式：

$$ \int_{0}^{\infty} H(\epsilon) f(\epsilon) d\epsilon \approx \int_{0}^{\mu} H(\epsilon) d\epsilon + \frac{\pi^2}{6}(k_B T)^2 H'(\mu) + \mathcal{O}(T^4) $$

其中 $H'(\mu)$ 是函数 $H(\epsilon)$ 对能量求导后在 $\epsilon = \mu$ 处的值。这个公式包含了几个关键点：

*   **零温项**：第一项 $\int_{0}^{\mu} H(\epsilon) d\epsilon$ 是零温下的结果，只是积分上限从[费米能](@entry_id:143977) $\epsilon_F$ 换成了有限温度下的化学势 $\mu$。
*   **温度修正项**：第二项是最低阶的温度修正，它与温度的平方 $T^2$ 成正比。系数中包含了 $H(\epsilon)$ 在化学势处的一阶导数 $H'(\mu)$，这表明温度效应的大小取决于被积函数在[费米能级](@entry_id:143215)附近的“坡度”。
*   **偶次幂**：展开式中只包含温度 $T$ 的偶数次幂（$T^2, T^4, \dots$）。奇数次幂项的缺失是一个普遍特征，其数学根源在于 $-\frac{\partial f}{\partial \epsilon}$ 关于 $(\epsilon - \mu)$ 的偶[函数对称性](@entry_id:168571)。在展开过程中，涉及到形如 $\int_{-\infty}^{\infty} (\epsilon-\mu)^n (-\frac{\partial f}{\partial \epsilon}) d\epsilon$ 的积分。当 $n$ 为奇数时，被积函数是一个奇函数，其在对称区间 $(-\infty, \infty)$ 上的积分严格为零，因此所有奇数阶的温度修正项都消失了 [@problem_id:2009173]。

### 应用：[费米气体](@entry_id:145305)的低温[热力学](@entry_id:141121)

[索末菲展开](@entry_id:149655)在理解金属[电子气](@entry_id:140692)等简并费米系统的低温行为方面取得了巨大成功。

#### 物理图像：[粒子-空穴激发](@entry_id:137289)

在深入数学细节之前，我们可以通过一个简单的物理模型来理解为何能量的温度修正项是 $T^2$ 依赖的。当温度从绝对零度升高时，只有能量在费米能级附近约 $k_B T$ 范围内的电子才会被热激发到费米能级之上的空态。

1.  **受激发的电子数**：能够参与热过程的电子数量正比于这个能量窗口的宽度 $k_B T$ 和[费米能级](@entry_id:143215)处的态密度 $g(\epsilon_F)$。因此，被激发的电子数 $N_{ex} \propto g(\epsilon_F) k_B T$。
2.  **[平均激发能](@entry_id:160327)量**：每个被激发的电子，其获得的[平均能量](@entry_id:145892)也正比于热[能标](@entry_id:196201)度 $k_B T$。

因此，系统的总内能增量 $\Delta U$，即这些粒子-空穴对的总能量，将是这两者的乘积：

$$ \Delta U \propto (g(\epsilon_F) k_B T) \times (k_B T) = g(\epsilon_F) (k_B T)^2 $$

这个简单的[启发式](@entry_id:261307)论证 [@problem_id:2009199] 直观地揭示了费米气体低温内能与 $T^2$ 成正比的物理根源，即[泡利不相容原理](@entry_id:141850)限制了只有费米面附近的粒子才能参与[热激发](@entry_id:275697)。

#### 化学势的[温度依赖性](@entry_id:147684)

在大多数物理系统中（如一块金属），粒子数 $N$ 是固定的。当温度升高时，电子被激发到更高的能级，为了保持总粒子数不变，化学势 $\mu$ 必须随温度 $T$ 变化。我们可以利用[索末菲展开](@entry_id:149655)来精确计算这个变化。

总粒子数 $N$ 由积分 $N = \int_0^\infty g(\epsilon) f(\epsilon) d\epsilon$ 给出。将[索末菲展开](@entry_id:149655)应用于此（令 $H(\epsilon) = g(\epsilon)$），我们得到：

$$ N \approx \int_0^\mu g(\epsilon) d\epsilon + \frac{\pi^2}{6}(k_B T)^2 g'(\mu) $$

由于 $N$ 是一个常数，它也等于其零温时的值 $N = \int_0^{\epsilon_F} g(\epsilon) d\epsilon$。令两者相等，并注意到 $\int_0^\mu g(\epsilon) d\epsilon = \int_0^{\epsilon_F} g(\epsilon) d\epsilon + \int_{\epsilon_F}^\mu g(\epsilon) d\epsilon \approx N + (\mu - \epsilon_F) g(\epsilon_F)$，我们得到：

$$ 0 \approx (\mu - \epsilon_F) g(\epsilon_F) + \frac{\pi^2}{6}(k_B T)^2 g'(\epsilon_F) $$

（在此近似中，我们已将 $g'(\mu)$ 近似为 $g'(\epsilon_F)$，因为 $\mu - \epsilon_F$ 本身是 $T^2$ 量级）。求解 $\mu(T) - \epsilon_F$，我们得到一个普适的结果 [@problem_id:2009179]：

$$ \mu(T) - \epsilon_F \approx -\frac{\pi^2}{6} \frac{g'(\epsilon_F)}{g(\epsilon_F)} (k_B T)^2 $$

这个结果的物理含义非常清晰 [@problem_id:1821363]：化学势的移动方向取决于[费米能级](@entry_id:143215)处态密度的“斜率”$g'(\epsilon_F)$。

*   如果 $g'(\epsilon_F) > 0$，即费米能级以上的态密度比其下方更大，那么为了在[热激发](@entry_id:275697)时保持总粒子数不变，化学势必须**向下移动**（$\mu(T)  \epsilon_F$）。因为向上激发到态密度更高的区域比从态密度较低的区域移走粒子更容易，需要降低化学势来“抑制”这种不对称的布居。对于标准的三维[自由电子气](@entry_id:145649)（$g(\epsilon) \propto \epsilon^{1/2}$）[@problem_id:2009193]，有 $g'(\epsilon_F) > 0$，因此其化学势随温度升高而降低。

*   反之，如果 $g'(\epsilon_F)  0$，化学势则必须**向上移动**（$\mu(T) > \epsilon_F$）以补偿布居。

#### 内能与[热容](@entry_id:137594)

现在我们计算系统的内能 $U = \int_0^\infty \epsilon g(\epsilon) f(\epsilon) d\epsilon$。这里 $H(\epsilon) = \epsilon g(\epsilon)$。应用[索末菲展开](@entry_id:149655)：

$$ U(T) \approx \int_0^\mu \epsilon g(\epsilon) d\epsilon + \frac{\pi^2}{6}(k_B T)^2 \left. \frac{d(\epsilon g(\epsilon))}{d\epsilon} \right|_{\epsilon=\mu} $$

将 $\mu(T)$ 的表达式代入并展开到 $T^2$ 阶，经过仔细的计算，许多项会相互抵消，最终得到一个简洁的结果：

$$ U(T) \approx U(0) + \frac{\pi^2}{6} g(\epsilon_F) (k_B T)^2 $$

其中 $U(0) = \int_0^{\epsilon_F} \epsilon g(\epsilon) d\epsilon$ 是零温下的[基态能量](@entry_id:263704)。

电子对[热容](@entry_id:137594)的贡献 $C_V$ 定义为 $C_V = \left(\frac{\partial U}{\partial T}\right)_V$。对上式求导，我们立即得到：

$$ C_V = \frac{\pi^2}{3} g(\epsilon_F) k_B^2 T = \gamma T $$

这个结果是固体物理学中的一个里程碑。它预言了金属的[电子热容](@entry_id:144815)在低温下与温度成线性关系，这与实验观测完美吻合。常数 $\gamma = \frac{\pi^2}{3} g(\epsilon_F) k_B^2$ 被称为[索末菲参数](@entry_id:180630)。这个关系极为重要，因为它将一个宏观可测量的量（热容）与一个微观的关键物理量（[费米能级](@entry_id:143215)处的[态密度](@entry_id:147894) $g(\epsilon_F)$）直接联系起来。例如，通过实验测量金属钾的 $\gamma$ 值，就可以推算出其费米能级处的[电子态密度](@entry_id:182354) [@problem_id:1821329]。

### 展开的有效性与局限性

尽管[索末菲展开](@entry_id:149655)功能强大，但它的应用并非无条件的。理解其局限性对于正确使用该工具至关重要。

#### 低温条件

[索末菲展开](@entry_id:149655)是一个[渐近级数](@entry_id:168392)，其有效性的前提是展开项逐级减小。以电子内能为例，要求温度修正项远小于零温项 [@problem_id:2009178]：

$$ \frac{\pi^2}{4} \frac{(k_B T)^2}{\epsilon_F} \ll \frac{3}{5} \epsilon_F \implies (k_B T)^2 \ll \frac{12}{5\pi^2} \epsilon_F^2 $$

这个条件本质上等价于 $k_B T \ll \epsilon_F$，或者说 $T \ll T_F$，其中 $T_F = \epsilon_F/k_B$ 是[费米温度](@entry_id:148320)。对于大多数金属，[费米温度](@entry_id:148320)高达数万开尔文，因此在室温及以下，这一条件通常是满足的。

#### 对态密度的要求

[索末菲展开](@entry_id:149655)的数学推导依赖于将被积函数 $H(\epsilon)$ 在 $\epsilon = \mu$ 附近进行泰勒展开。这隐含了一个核心假设：**$H(\epsilon)$（及其导数）在化学势附近必须是光滑且缓变的函数**。如果这个条件不满足，展开就会失效。

1.  **离散能谱**：考虑一个能级是离散的系统，例如[量子点](@entry_id:143385) [@problem_id:2009223]。其态密度 $g(\epsilon)$ 是一系列狄拉克 $\delta$ 函数的和。在这种情况下，$H(\epsilon) = \epsilon g(\epsilon)$ 是一个[分布](@entry_id:182848)，而不是一个[光滑函数](@entry_id:267124)。它的导数在数学上没有良好定义，因此无法进行[泰勒展开](@entry_id:145057)。系统的热力学性质由分立能级的布居变化决定，表现为阶跃行为，不能用 $T$ 的[幂级数](@entry_id:146836)来描述。

2.  **[能隙](@entry_id:191975)与[奇点](@entry_id:137764)**：另一个重要例子是BCS理论描述的[超导体](@entry_id:191025) [@problem_id:1821326]。在费米能级附近，[超导体](@entry_id:191025)的[准粒子](@entry_id:136584)态密度存在一个宽度为 $2\Delta$ 的[能隙](@entry_id:191975)，即在 $|\epsilon - E_F| \le \Delta$ 范围内 $g(\epsilon)=0$。此外，在[能隙](@entry_id:191975)的边缘，[态密度](@entry_id:147894)发散（呈现平方根[奇点](@entry_id:137764)）。对于这样的系统，函数 $H(\epsilon) = \epsilon g(\epsilon)$ 在化学势 $E_F$ 处及其附近区域内为零，其所有阶的导数在 $E_F$ 处也都为零。机械地应用[索末菲展开](@entry_id:149655)公式会得出[热容](@entry_id:137594)在所有 $T$ 的幂次上都为零的错误结论。而实际上，[超导体](@entry_id:191025)的[低温热容](@entry_id:142131)由跨越[能隙](@entry_id:191975)的[热激活过程](@entry_id:274558)主导，表现为指数依赖关系，如 $\exp(-\Delta/k_B T)$。这种非解析行为是[索末菲展开](@entry_id:149655)（一个[幂级数展开](@entry_id:273325)）从根本上无法捕捉的。

综上所述，[索末菲展开](@entry_id:149655)是一个深刻揭示简并费米系统低温物理的强大理论工具。它不仅提供了[计算热力学](@entry_id:148023)量的实用方法，更重要的是，它将宏观的热行为与费米面附近的微观[电子结构](@entry_id:145158)（即[态密度](@entry_id:147894)及其导数）紧密联系起来。然而，其应用范围仅限于那些在费米能级附近具有光滑、[连续态](@entry_id:197473)密度的系统。