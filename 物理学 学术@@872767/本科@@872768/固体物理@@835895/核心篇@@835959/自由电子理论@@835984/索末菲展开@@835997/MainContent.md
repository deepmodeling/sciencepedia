## 引言
在凝聚态物理中，理解由大量[费米子](@entry_id:146235)（如[金属中的电子](@entry_id:138687)）组成的系统的[热力学性质](@entry_id:146047)至关重要。这些性质，如内能和[热容](@entry_id:137594)，通常通过对某个能量依赖的物理量与[费米-狄拉克分布](@entry_id:138909)函数乘积的积分来计算。在绝对[零度](@entry_id:156285)下，这个计算因费米[分布](@entry_id:182848)的[阶跃函数](@entry_id:159192)形式而变得简单。然而，在任何有限温度下，费米分布函数在化学势附近的平滑过渡使得积分变得异常复杂，通常无法得到解析解。这一挑战构成了理论物理学中的一个关键知识缺口：我们如何系统地量化温度对简并费米系统性质的微小影响？

[索末菲展开](@entry_id:149655)（Sommerfeld expansion）正是为了解决这一问题而发展的强大数学框架。它提供了一种在低温极限下（$k_B T \ll \mu$）对这些积分进行系统性近似的方法，将复杂的积分转化为关于温度 $T$ 的幂级数。本文将带你深入探索[索末菲展开](@entry_id:149655)的奥秘。在“原理与机制”一章中，我们将揭示其数学推导的精髓和“费米窗口”的物理图像。接着，在“应用与交叉学科联系”中，我们将展示这一工具如何被广泛应用于解释金属的[电子热容](@entry_id:144815)、化学势的温度漂移，乃至天体物理学和介观物理中的现象。最后，通过“动手实践”部分，你将有机会亲自运用[索末菲展开](@entry_id:149655)解决具体物理问题，从而巩固所学知识。现在，让我们从[索末菲展开](@entry_id:149655)的基本原理开始。

## 原理与机制

在研究金属等[费米子](@entry_id:146235)系统时，我们经常需要计算各种宏观[热力学](@entry_id:141121)量，例如总粒子数 $N$、内能 $U$ 或[热容](@entry_id:137594) $C_V$。这些量通常可以表示为某个能量依赖函数 $H(\epsilon)$ 与[费米-狄拉克分布](@entry_id:138909)函数 $f(\epsilon)$ 乘积的积分形式：

$$ I = \int_{0}^{\infty} H(\epsilon) f(\epsilon) \, d\epsilon $$

其中，$f(\epsilon)$ 是[费米-狄拉克分布](@entry_id:138909)函数：

$$ f(\epsilon) = \frac{1}{\exp\left(\frac{\epsilon - \mu}{k_B T}\right) + 1} $$

这里，$\mu$ 是化学势，$T$ 是绝对温度，$k_B$ 是[玻尔兹曼常数](@entry_id:142384)。在绝对[零度](@entry_id:156285)（$T=0$）时，$f(\epsilon)$ 是一个简单的[阶跃函数](@entry_id:159192)：当 $\epsilon  \epsilon_F$ 时 $f(\epsilon)=1$，当 $\epsilon > \epsilon_F$ 时 $f(\epsilon)=0$，其中 $\epsilon_F$ 是[费米能](@entry_id:143977)。这使得积分计算变得非常简单 [@problem_id:2009215]。例如，三维[自由电子气](@entry_id:145649)在 $T=0$ 时的粒子[数密度](@entry_id:268986) $n$ 可以通过对[态密度](@entry_id:147894) $g(\epsilon)$ 在能量从 $0$ 到 $\epsilon_F$ 的区间[内积](@entry_id:158127)分得到。

然而，在任意有限温度 $T > 0$ 时，[费米-狄拉克分布](@entry_id:138909)函数在化学势 $\mu$ 附近变得平滑，使得上述积分通常没有解析解。[索末菲展开](@entry_id:149655)（Sommerfeld expansion）提供了一个在低温条件下（即 $k_B T \ll \mu$）对这类积分进行系统性近似计算的强大数学工具。本章将深入探讨[索末菲展开](@entry_id:149655)的原理、关键机制及其在固态物理中的重要应用。

### [索末菲展开](@entry_id:149655)的核心思想：费米窗口

[索末菲展开](@entry_id:149655)的物理基础在于一个关键的观察：在低温下，热激发只会影响能量在化学势 $\mu$ 附近一个很窄范围内的电子。远离 $\mu$ 的深能级电子由于[泡利不相容原理](@entry_id:141850)没有空的末态可供跃迁，而远高于 $\mu$ 的能级由于玻尔兹曼因子 $\exp(-(\epsilon-\mu)/k_B T)$ 的指数抑制而几乎不可能被占据。因此，所有与温度相关的[物理变化](@entry_id:136242)都发生在一个以 $\mu$ 为中心、宽度约为 $k_B T$ 的“**费米窗口**”（Fermi window）内。

这个物理图像可以通过考察[费米-狄拉克分布](@entry_id:138909)函数对能量的导数来精确化。我们定义一个函数 $g_{FD}(\epsilon) = -\frac{\partial f}{\partial \epsilon}$。这个函数描述了当温度从零微小增加时，各个能级 $\epsilon$ 上粒子占据数发生变化的“敏感度”。通过[链式法则](@entry_id:190743)，我们可以得到：

$$ g_{FD}(\epsilon) = -\frac{\partial f}{\partial \epsilon} = \frac{1}{k_B T} \frac{\exp\left(\frac{\epsilon - \mu}{k_B T}\right)}{\left[\exp\left(\frac{\epsilon - \mu}{k_B T}\right) + 1\right]^2} $$

通过变量代换 $x = (\epsilon - \mu)/(2k_B T)$，上式可以被重写为一个更对称的形式：

$$ g_{FD}(\epsilon) = \frac{1}{4k_B T} \text{sech}^2\left(\frac{\epsilon - \mu}{2k_B T}\right) $$

这个函数是一个在 $\epsilon = \mu$ 处达到峰值的钟形曲线。它的峰值为 $\frac{1}{4k_B T}$，并且随着温度 $T$ 的降低而变得越来越高、越来越窄。我们可以通过计算其半峰全宽（Full Width at Half Maximum, FWHM）来量化其宽度 [@problem_id:2009218]。通过求解 $g_{FD}(\epsilon) = \frac{1}{2} g_{FD}(\mu)$，我们发现 FWHM 为：

$$ \text{FWHM} = 4k_B T \operatorname{arccosh}(\sqrt{2}) \approx 3.52 k_B T $$

这个结果精确地表明，在低温下，函数 $-\frac{\partial f}{\partial \epsilon}$ 的行为非常像一个以 $\mu$ 为中心的、宽度正比于 $k_B T$ 的脉冲。在数学上，当 $T \to 0$ 时，它趋向于一个狄拉克 $\delta$ 函数 $\delta(\epsilon - \mu)$。正是因为 $-\frac{\partial f}{\partial \epsilon}$ 的这种尖锐峰形特性，使得我们可以将平滑变化的函数 $H(\epsilon)$ 在 $\epsilon=\mu$ 处进行泰勒展开，从而得到一个关于温度 $T$ 的[幂级数](@entry_id:146836)近似，这就是[索末菲展开](@entry_id:149655)的本质。

### [索末菲展开](@entry_id:149655)的数学形式与结构

通过对原积分进行[分部积分](@entry_id:136350)，并利用 $-\frac{\partial f}{\partial \epsilon}$ 的性质，可以推导出[索末菲展开](@entry_id:149655)的通用公式。对于一个在积分下限处为零的光滑函数 $H(\epsilon)$，其标准展开式到四阶项为：

$$ \int_{0}^{\infty} H(\epsilon) f(\epsilon) d\epsilon \approx \int_{0}^{\mu} H(\epsilon) d\epsilon + \frac{\pi^2}{6}(k_B T)^2 H'(\mu) + \frac{7\pi^4}{360}(k_B T)^4 H'''(\mu) + \mathcal{O}(T^6) $$

其中 $H'(\mu)$ 和 $H'''(\mu)$ 分别是函数 $H(\epsilon)$ 对能量的一阶和三阶导数在 $\epsilon=\mu$ 处的值。

让我们分析这个展开式的结构：

1.  **零阶项**: $\int_{0}^{\mu} H(\epsilon) d\epsilon$ 是主要贡献项。它非常类似于在绝对[零度](@entry_id:156285)下的积分 $\int_{0}^{\epsilon_F} H(\epsilon) d\epsilon$，唯一的区别是用温度依赖的化学势 $\mu(T)$ 替换了费米能 $\epsilon_F$。在低温下，$\mu(T)$ 与 $\epsilon_F$ 非常接近，因此这一项代表了系统的“[基态](@entry_id:150928)”贡献。

2.  **温度修正项**: 后续项是温度的[幂级数](@entry_id:146836)。一个显著的特征是，展开式中只包含温度 $T$ 的**偶数次幂**（$T^2, T^4, \dots$），而没有任何奇数次幂项（如 $T^1, T^3, \dots$）。这并非偶然，而是源于物理过程的对称性 [@problem_id:2009173]。在推导过程中，修正项来自于对形如 $\int_{-\infty}^{\infty} x^n \text{sech}^2(x/2) dx$ 的积分求值，其中 $x = (\epsilon-\mu)/k_B T$。由于 $\text{sech}^2(x/2)$ 是一个关于 $x$ 的[偶函数](@entry_id:163605)，当 $n$ 为奇数时，整个被积函数 $x^n \text{sech}^2(x/2)$ 是[奇函数](@entry_id:173259)。[奇函数](@entry_id:173259)在对称区间 $(-\infty, \infty)$ 上的积分为零。因此，所有对应于奇数阶导数和奇数次幂 $T$ 的项都精确地消失了。

### 物理应用：[电子热容](@entry_id:144815)与化学势的温度漂移

[索末菲展开](@entry_id:149655)在理解金属电子的[热力学性质](@entry_id:146047)方面取得了巨大成功。下面我们探讨两个最重要的应用。

#### [电子热容](@entry_id:144815)

[经典物理学](@entry_id:150394)预言金属中自由电子对[热容](@entry_id:137594)的贡献应为 $\frac{3}{2}Nk_B$，这是一个与温度无关的常数。然而，实验在低温下观测到[电子热容](@entry_id:144815)与温度成[线性关系](@entry_id:267880)，$C_e = \gamma T$。[索末菲模型](@entry_id:145532)完美地解释了这一现象。

系统的内能 $U$ 由积分 $U = \int_{0}^{\infty} \epsilon g(\epsilon) f(\epsilon) d\epsilon$ 给出，其中 $g(\epsilon)$ 是[电子态密度](@entry_id:182354)。这里，$H(\epsilon) = \epsilon g(\epsilon)$。应用[索末菲展开](@entry_id:149655)到二阶，我们得到：

$$ U(T) \approx \int_{0}^{\mu} \epsilon g(\epsilon) d\epsilon + \frac{\pi^2}{6}(k_B T)^2 \left. \frac{d(\epsilon g(\epsilon))}{d\epsilon} \right|_{\epsilon=\mu} $$

在低温下，我们可以近似 $\mu \approx \epsilon_F$，并且通常 $g(\epsilon)$ 在费米能附近变化缓慢，因此 $\left. \frac{d(\epsilon g(\epsilon))}{d\epsilon} \right|_{\epsilon=\mu} \approx g(\epsilon_F)$。所以内能的增量为：

$$ \Delta U = U(T) - U(0) \approx \frac{\pi^2}{6}(k_B T)^2 g(\epsilon_F) $$

这个 $T^2$ 依赖关系有一个直观的物理解释 [@problem_id:2009199]。只有在[费米能](@entry_id:143977)附近能量范围约为 $k_B T$ 内的电子才能被[热激发](@entry_id:275697)。这些电子的数量正比于 $g(\epsilon_F) k_B T$。每个被激发的电子平均获得的能量也正比于 $k_B T$。因此，总的能量增加 $\Delta U$ 就正比于这两者的乘积，即 $\Delta U \propto (g(\epsilon_F) k_B T) \times (k_B T) = g(\epsilon_F) (k_B T)^2$。

[电子热容](@entry_id:144815)是内能对温度的导数，$C_e = \frac{\partial U}{\partial T}$。对上式求导，我们立即得到：

$$ C_e = \left( \frac{\pi^2}{3} k_B^2 g(\epsilon_F) \right) T $$

这导出了[电子热容](@entry_id:144815)与温度的[线性关系](@entry_id:267880) $C_e = \gamma T$，并且给出了索末菲常数 $\gamma$ 的微观表达式：

$$ \gamma = \frac{\pi^2}{3} k_B^2 g(\epsilon_F) $$

这个关系极为重要，因为它将一个宏观可测量的量（$\gamma$，通过[低温热容](@entry_id:142131)实验得到）与一个关键的微观材料参数（[费米能级的态密度](@entry_id:161911) $g(\epsilon_F)$）直接联系起来。例如，通过测量钾金属的 $\gamma$ 值，我们可以实验性地推算出其[费米能级的态密度](@entry_id:161911) [@problem_id:1821329]。

#### 化学势的温度漂移

另一个微妙但重要的效应是化学势本身随温度的变化。为了保持系统总粒子数 $N$ 守恒，当温度升高、电子被激发到更高能级时，化学势 $\mu$ 必须进行微小的调整。

粒子总数由 $N = \int_{0}^{\infty} g(\epsilon) f(\epsilon) d\epsilon$ 给出，其中 $H(\epsilon) = g(\epsilon)$。由于 $N$ 不随温度变化，它在任意温度 $T$ 的值都必须等于其在 $T=0$ 时的值 $N = \int_{0}^{\epsilon_F} g(\epsilon) d\epsilon$。利用[索末菲展开](@entry_id:149655)，我们有：

$$ \int_{0}^{\epsilon_F} g(\epsilon) d\epsilon \approx \int_{0}^{\mu} g(\epsilon) d\epsilon + \frac{\pi^2}{6}(k_B T)^2 g'(\mu) $$

将 $\int_{0}^{\mu} g(\epsilon) d\epsilon$ 在 $\epsilon_F$ 附近展开为 $\int_{0}^{\epsilon_F} g(\epsilon) d\epsilon + (\mu - \epsilon_F)g(\epsilon_F) + \dots$，并近似 $g'(\mu) \approx g'(\epsilon_F)$，我们得到：

$$ 0 \approx (\mu - \epsilon_F)g(\epsilon_F) + \frac{\pi^2}{6}(k_B T)^2 g'(\epsilon_F) $$

解出化学势的温度漂移 $\mu(T) - \epsilon_F$，我们得到一个普适的结果 [@problem_id:2009179]：

$$ \mu(T) - \epsilon_F \approx -\frac{\pi^2}{6} \frac{g'(\epsilon_F)}{g(\epsilon_F)} (k_B T)^2 $$

这个结果揭示了化学势漂移的方向取决于费米能级处[态密度](@entry_id:147894)的变化趋势 [@problem_id:1821363]：

*   如果 $g'(\epsilon_F) > 0$（即[费米能级](@entry_id:143215)以上的态密度更大），热激发会使更多电子占据 $\epsilon_F$ 上方的能级。为了维持总粒子数不变，化学势必须**向下**移动（$\mu  \epsilon_F$），以略微减少高[态密度](@entry_id:147894)区域的占据。
*   如果 $g'(\epsilon_F)  0$（即费米能级以下的态密度更大），[热激发](@entry_id:275697)主要是在 $\epsilon_F$ 下方产生空穴。为了补偿，化学势必须**向上**移动（$\mu > \epsilon_F$），以占据更多的态。
*   对于标准的三维[自由电子气](@entry_id:145649)，$g(\epsilon) \propto \epsilon^{1/2}$，因此 $g'(\epsilon_F) > 0$，其化学势总是随温度升高而降低。具体计算可得 $\mu(T) = \epsilon_F \left[1 - \frac{\pi^2}{12}\left(\frac{k_B T}{\epsilon_F}\right)^2\right]$ [@problem_id:2009193]。

### 展开的有效性与局限性

任何近似方法都有其[适用范围](@entry_id:636189)，[索末菲展开](@entry_id:149655)也不例外。

首先，它是一个在小参数 $(k_B T/\mu)$ 下的[渐近展开](@entry_id:173196)。这意味着只有在低温极限下，即热能 $k_B T$ 远小于化学势 $\mu$（或[费米能](@entry_id:143977) $\epsilon_F$）时，展开才收敛得很好。我们可以通过比较 $T^4$ 修正项和 $T^2$ 修正项的比例来量化这一点。对于三维[自由电子气](@entry_id:145649)的内能，这个比例正比于 $(k_B T / \mu)^2$ [@problem_id:1821361]。这表明只要 $k_B T \ll \mu$，高阶项的贡献就会迅速减小，保证了展开的准确性。

其次，也是最根本的局限性，[索末菲展开](@entry_id:149655)要求被积函数 $H(\epsilon)$ 在化学势 $\mu$ 的一个邻域内是**光滑的**（即拥有所需阶数的导数且没有[奇点](@entry_id:137764)）。如果 $H(\epsilon)$ 在 $\mu$ 附近存在[奇点](@entry_id:137764)、不连续或快速变化，展开就会失效 [@problem_id:1821326]。

一个典型的例子是具有[能隙](@entry_id:191975)的系统，如BCS理论描述的[超导体](@entry_id:191025)。在这种系统中，费米能级位于一个宽度为 $2\Delta$ 的[能隙](@entry_id:191975)中央，因此在 $\epsilon_F$ 附近的态密度 $g(\epsilon)$ 精确为零。此外，$g(\epsilon)$ 在[能隙](@entry_id:191975)边缘（$\epsilon = E_F \pm \Delta$）具有平方根[奇点](@entry_id:137764)。

在这种情况下，函数 $H(\epsilon)=\epsilon g(\epsilon)$ 及其在 $\epsilon = E_F$ 处的所有阶导数都为零。机械地应用[索末菲展开](@entry_id:149655)公式会得到所有温度修正项都为零的错误结论，即 $U(T)=U(0)$。而物理上，系统的[热力学性质](@entry_id:146047)是由电子[热激发](@entry_id:275697)**跨越[能隙](@entry_id:191975)** $\Delta$ 所主导的。这导致内能等物理量表现出与温度相关的指数激活行为，例如 $\Delta U \propto \exp(-\Delta/k_B T)$。这种非解析的行为（在 $T=0$ 处无法展开为[幂级数](@entry_id:146836)）完全超出了[索末菲展开](@entry_id:149655)的能力范围。

综上所述，[索末菲展开](@entry_id:149655)是处理简金属等在费米能级处具有有限且光滑态密度的[费米子](@entry_id:146235)系统的强大工具。它深刻地揭示了低温下电子热力学性质的[幂律](@entry_id:143404)行为。然而，对于[半导体](@entry_id:141536)、绝缘体和[超导体](@entry_id:191025)等存在[能隙](@entry_id:191975)的系统，其物理过程由不同的机制主导，[索末菲展开](@entry_id:149655)不再适用。理解这一局限性与理解其应用本身同样重要。