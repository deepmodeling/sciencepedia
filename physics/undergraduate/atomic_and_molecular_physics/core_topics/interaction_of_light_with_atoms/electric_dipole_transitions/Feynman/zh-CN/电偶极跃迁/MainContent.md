## 引言
原子和分子如何吸收或释放[光子](@keyword=photon|lang=zh-CN|style=Feynman)，在不同的能级之间“跳跃”？这一看似简单的现象是[光与物质相互作用](@keyword=light_matter_interaction|lang=zh-CN|style=Feynman)的核心，也是[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)、天体物理和量子技术等众多学科的基石。然而，并非所有能级之间的跃迁都能够发生。当我们观察[原子光谱](@keyword=atomic_spectra|lang=zh-CN|style=Feynman)时，会发现清晰、离散的[谱线](@keyword=spectral_line|lang=zh-CN|style=Feynman)，这意味着存在一套严格的“交通规则”在控制着这些量子过程。为什么某些跃迁被自然所“允许”，而另一些则被“禁止”？这些规则背后的深刻物理原理又是什么？

本文旨在系统地回答这些问题，带您深入探索电偶极跃迁的世界。我们将揭示这些规则并非孤立的经验总结，而是源自量子力学中最美妙、最核心的概念：[对称性与守恒律](@keyword=symmetry_and_conservation_laws|lang=zh-CN|style=Feynman)。

旅程将分为两大部分。在第一部分“原理与机制”中，我们将从最简单的模型出发，通过思想实验一步步推导出关于宇称和角动量的[选择定则](@keyword=selection_rules|lang=zh-CN|style=Feynman)，并理解这些规则并非绝对，它们如何在更复杂的现实情况（如非谐效应、外场扰动甚至弱相互作用）下被修正或“打破”。在第二部分“应用与跨学科连接”中，我们将看到这些抽象的规则如何在解读宇宙星光、分析分子结构、设计[半导体器件](@keyword=semiconductor_devices|lang=zh-CN|style=Feynman)以及构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机等前沿领域中发挥着至关重要的作用。

现在，让我们一同启程，首先深入探究这些规则的原理与机制，揭开光与物质“握手”的奥秘。

## 原理与机制

在上一章中，我们已经对原子和分子如何通过与光相互作用来“跳跃”能级有了初步的印象。但这个过程并非随心所欲。大自然有一套自己的规则，一套决定哪些跳跃被允许、哪些被禁止的深刻法则。这些规则被称为“选择定则”。现在，让我们像物理学家一样，不仅仅满足于知道这些规则是什么，更要去探寻它们为何如此。这趟旅程将带我们从最简单的模型出发，一路窥见物理学最深邃的统一与和谐之美。

### 万物之始：对称性与“握手”的艺术

想象一下，一个原子要吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)，从一个能级跃迁到另一个能级。这就像两个人要完成一次成功的握手。首先，他们得在正确的时间、正确的位置伸出正确的手。在量子世界里，这次“握手”由一个称为“跃迁偶极矩”的量来描述。如果这个量是零，就意味着“握手”无法完成，跃迁就被“禁止”了；反之，如果它不为零，跃迁就是“允许”的。

那么，这个跃迁偶极矩何时为零呢？答案隐藏在一个美丽而强大的概念中：对称性。

让我们从一个最简单的思想实验开始：一个被限制在一维“盒子”里的电子 [@problem_id:1989602]。它的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)由[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman) $\psi_n(x)$ 描述，这些[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)就像驻波，具有非常明确的对称性。以盒子的中心为[对称中心](@keyword=center_of_inversion|lang=zh-CN|style=Feynman)，[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（$n=1$）的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)是偶对称的（像一个山包），第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)（$n=2$）是[奇对称](@keyword=ungerade|lang=zh-CN|style=Feynman)的（像一个S形），以此类推，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的对称性随着[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman) $n$ 的增加而交替变换。

现在，一束光照过来，其电场与电子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)相互作用，这个相互作用力正比于电子的位置 $x$。从数学上看，位置算符 $x$ 是一个奇函数（即 $f(-x) = -f(x)$）。决定跃迁能否发生的“握手”积分是 $\int \psi_{n'}^* (x) \cdot x \cdot \psi_n(x) \, dx$。

这里奇迹发生了。数学告诉我们，一个[偶函数](@keyword=even_functions|lang=zh-CN|style=Feynman)与一个[奇函数](@keyword=odd_functions|lang=zh-CN|style=Feynman)的乘积是奇函数，而两个[奇函数](@keyword=odd_functions|lang=zh-CN|style=Feynman)或两个[偶函数](@keyword=even_functions|lang=zh-CN|style=Feynman)的乘积是[偶函数](@keyword=even_functions|lang=zh-CN|style=Feynman)。为了使整个积分不为零，被积函数 $\psi_{n'}^* \cdot x \cdot \psi_n$ 必须整体上是[偶函数](@keyword=even_functions|lang=zh-CN|style=Feynman)。

-   如果初态 $\psi_n$ 和末态 $\psi_{n'}$ 具有相同的宇称（同为偶或同为奇），那么 $\psi_{n'}^* \cdot \psi_n$ 是一个偶函数。再乘以[奇函数](@keyword=odd_functions|lang=zh-CN|style=Feynman) $x$，整个被积函数就变成了奇函数。一个奇函数在一个对称区间上的积分（从 $-L/2$ 到 $L/2$）恒为零！这意味着，相同宇称的态之间无法通过电偶极跃迁相互“握手”。
-   只有当 $\psi_n$ 和 $\psi_{n'}$ 具有相反的宇称时，$\psi_{n'}^* \cdot \psi_n$ 才是一个[奇函数](@keyword=odd_functions|lang=zh-CN|style=Feynman)。再乘以奇函数 $x$，整个被积函数变成偶函数，积分值不为零！

这直接导出了一个[选择定则](@keyword=selection_rules|lang=zh-CN|style=Feynman)：宇称必须改变！对于一维[无限深势阱](@keyword=infinite_potential_well|lang=zh-CN|style=Feynman)，这意味着[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman) $n$ 的变化量 $\Delta n = n' - n$ 必须是奇数。这不仅仅是一个数学技巧，它揭示了一个深刻的物理原理：电[偶极相互作用](@keyword=dipole_interaction|lang=zh-CN|style=Feynman)本身具有[奇宇称](@keyword=odd_parity|lang=zh-CN|style=Feynman)，因此它只能连接宇称相反的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。

### 旋转之舞：[角动量守恒](@keyword=conservation_of_angular_momentum|lang=zh-CN|style=Feynman)

现在，让我们把舞台从一维直线扩展到一个二维[圆环](@keyword=annulus|lang=zh-CN|style=Feynman) [@problem_id:1989611]。想象一个电子被束缚在一个[圆环](@keyword=annulus|lang=zh-CN|style=Feynman)上运动。它的状态由[角量子数](@keyword=l_quantum_number|lang=zh-CN|style=Feynman) $m$ 描述，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)是 $\psi_m(\phi) = \frac{1}{\sqrt{2\pi}} e^{im\phi}$。当一束沿 $x$ 轴方向线偏振的光射向这个环时，会发生什么？

我们知道，[光子](@keyword=photon|lang=zh-CN|style=Feynman)本身携带角动量。一个圆偏振光子携带一个单位（$\hbar$）的角动量，而[线偏振光](@keyword=linearly_polarized_light|lang=zh-CN|style=Feynman)可以看作是左旋和右旋圆偏振光的叠加。当电子吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)时，整个系统的角动量必须守恒。这意味着电子的角动量必须改变，其改变量正好等于它所吸收的[光子](@keyword=photon|lang=zh-CN|style=Feynman)的角动量。

这个物理直觉能否在数学中得到印证呢？当然可以！沿 $x$ 轴的电场与电子的相互作用项正比于 $x$ 坐标，在圆环上即为 $x = R\cos(\phi)$。利用欧拉公式，我们可以把这个相互作用写成 $R\cos(\phi) = \frac{R}{2}(e^{i\phi} + e^{-i\phi})$。这里，$e^{i\phi}$ 和 $e^{-i\phi}$ 这两项，就像是代表着携带 $+1$ 和 $-1$ 单位角动量的“量子”一样。

跃迁的“握手”积分变成了 $\int_0^{2\pi} (e^{-im_f\phi}) \cdot \cos(\phi) \cdot (e^{im_i\phi}) \, d\phi$。当我们把 $\cos(\phi)$ 展开后，这个积分只有在 $m_f - m_i - 1 = 0$ 或者 $m_f - m_i + 1 = 0$ 时才不为零。换句话说，选择定则赫然呈现在我们面前：

$$
\Delta m = m_f - m_i = \pm 1
$$

这完美地印证了我们的物理直觉！$\Delta m = +1$ 对应吸收了一个携带 $+1$ 单位角动量的“[光子](@keyword=photon|lang=zh-CN|style=Feynman)分量”，$\Delta m = -1$ 对应吸收了另一个。对于更普适的三维原子，这个规则演变成了[轨道角动量量子数](@keyword=l_quantum_number|lang=zh-CN|style=Feynman) $\Delta l = \pm 1$。这就是为什么在氢原子中，电子只能从 $S$ 轨道 ($l=0$) 跳到 $P$ 轨道 ($l=1$)，而不能直接跳到 $D$ 轨道 ($l=2$) 或跳回 $S$ 轨道。

### “规则”亦是“准则”：当模型不再完美

到目前为止，我们看到的规则似乎非常严格。但真实世界远比我们理想化的模型要复杂和有趣。当我们考虑这些“不完美”时，新的物理现象便会涌现出来，而所谓的“禁止”也往往变成了“不太可能”而已。

#### 不谐和的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)：[泛音](@keyword=overtones|lang=zh-CN|style=Feynman)的诞生

我们常把双原子分子中的[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)比作一[根理想](@keyword=radical_ideals|lang=zh-CN|style=Feynman)的弹簧，遵循[胡克定律](@keyword=hooke_s_law|lang=zh-CN|style=Feynman)。在这个“[简谐振子](@keyword=simple_harmonic_oscillator|lang=zh-CN|style=Feynman)”模型下，振动能级间的跃迁严格遵守 $\Delta v = \pm 1$ 的规则 [@problem_id:1989612]。然而，真实的[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)更像一根会拉伸、最终会断裂的弹簧。描述这种真实情况的“莫尔势”就引入了所谓的“力学非谐性”。此外，分子的偶极矩也并非严格随着键长线性变化，这带来了“电学非谐性”。

这两种“[非谐性](@keyword=anharmonicity|lang=zh-CN|style=Feynman)”共同作用，打破了简谐模型的完美对称性。其结果是，除了最强的 $\Delta v = \pm 1$ （基频）跃迁外，那些原本被禁止的 $\Delta v = \pm 2, \pm 3, \ldots$ 跃迁也变得可能了，尽管强度依次减弱。这些跃迁被称为“泛音”，它们在分子光谱中是可以被明确观测到的。这就像一把小提琴，除了[基音](@keyword=fundamental_tone|lang=zh-CN|style=Feynman)，正是那些丰富的[泛音](@keyword=overtones|lang=zh-CN|style=Feynman)赋予了它美妙的音色。现实世界的不完美，反而造就了它的丰富多彩。

#### 双[光子](@keyword=photon|lang=zh-CN|style=Feynman)华尔兹：另辟蹊径的跃迁

如果一次“握手”不行，那两次呢？单[光子](@keyword=photon|lang=zh-CN|style=Feynman)跃迁之所以要求宇称改变，是因为[光子](@keyword=photon|lang=zh-CN|style=Feynman)（电[偶极相互作用](@keyword=dipole_interaction|lang=zh-CN|style=Feynman)）本身是[奇宇称](@keyword=odd_parity|lang=zh-CN|style=Feynman)的。那么，如果原子同时吸收 *两个* [光子](@keyword=photon|lang=zh-CN|style=Feynman)会怎么样？[@problem_id:1989600]

两个奇宇称的相互作用叠加在一起，其总体效果就是一个[偶宇称](@keyword=even_parity|lang=zh-CN|style=Feynman)的相互作用！这就好像两次“取反”操作等于没有操作一样。因此，[双光子吸收](@keyword=two_photon_absorption|lang=zh-CN|style=Feynman)过程遵循一个全新的选择定则：宇称必须保持不变！例如，对于[谐振子](@keyword=harmonic_oscillator|lang=zh-CN|style=Feynman)，这意味着 $\Delta l$ 可以是 $0$ 或 $\pm 2$。

这为我们打开了一个全新的世界。那些在单[光子](@keyword=photon|lang=zh-CN|style=Feynman)过程中被严格禁止的跃迁（比如从 $l=0$ 到 $l=2$），在双[光子](@keyword=photon|lang=zh-CN|style=Feynman)过程中却是完全允许的。这告诉我们，“禁止”这个词在物理学中往往是有语境的。一个跃迁可能在一阶近似下被禁止，但在更高阶的过程中却是畅通无阻的。

### 当规则被外力扭曲

原子并非总是孤立地存在于虚空中。它周围的环境可以深刻地改变它的行为，甚至扭曲那些看似神圣的规则。

#### [斯塔克效应](@keyword=stark_effect|lang=zh-CN|style=Feynman)：电场施加的“微扰”

氢原子的 $2S$ 态是一个著名的“[亚稳态](@keyword=metastable_states|lang=zh-CN|style=Feynman)”。它无法通过单[光子](@keyword=photon|lang=zh-CN|style=Feynman)电偶极跃迁回到 $1S$ [基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，因为两者都是 $S$ 态（$l=0$），具有相同的正宇称。在孤立状态下，它只能通过非常缓慢的双[光子](@keyword=photon|lang=zh-CN|style=Feynman)过程衰变，寿命长达约七分之一秒——这在原子世界里是名副其实的“永恒”了。

然而，如果我们把这个氢原子放进一个静电场中，情况就完全不同了 [@problem_id:1989607]。电场会轻微地“拉扯”原子。由于 $2S$ 态和 $2P$ 态在能量上非常接近，这个微小的拉扯足以让 $2S$ 态“混入”一点点 $2P$ 态的成分。原来的纯 $2S$ 态变成了一个“$|2S\rangle + \epsilon |2P\rangle$”的混合态，这里 $\epsilon$ 是一个很小的系数。

现在，奇迹发生了。虽然 $|2S\rangle$ 部分仍然无法跃迁，但那个微小的 $|2P\rangle$ 成分却可以！$2P \to 1S$ 是一个完全被允许的、极快的跃迁。于是，这个[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)就有了一条新的、快速的衰变通道。原本被锁住的门，被外电场撬开了一条缝。仅仅需要每米几伏特的微弱电场，就足以让这条新通道的衰变速率与它原本的双[光子](@keyword=photon|lang=zh-CN|style=Feynman)速率相媲美。这就是斯塔克效应（Stark effect）的威力，它向我们展示了如何通过外部场来操控原子的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)和跃迁规则。

#### 量子真空的幻影：与镜中自我对话

甚至我们眼中的“真空”也并非一无所有。根据量子电动力学（QED），真空充满了瞬生瞬灭的“[虚光子](@keyword=virtual_photons|lang=zh-CN|style=Feynman)”，即[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)的[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)。一个原子的自发辐射，正是它与这些[真空涨落](@keyword=vacuum_fluctuations|lang=zh-CN|style=Feynman)“握手”的结果。

那么，如果我们改变真空的结构会怎样？想象一下，我们把一个激发的原子放在一面完美的镜子（导体表面）前 [@problem_id:1989606]。这面镜子会改变原子周围的[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)模式。一个非常直观的理解方式是“[镜像法](@keyword=method_of_images|lang=zh-CN|style=Feynman)”：原子不仅与自己相互作用，还与它在镜中的“镜像”相互作用。

-   如果原子的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)偶极矩平行于镜面，它的镜像偶极矩会反向[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。在原子所在的位置，镜像发出的[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)会与原子自身的场发生相消干涉，从而抑制了原子的辐射。原子“看到”自己的反向镜像，便“不想”辐射了。
-   反之，如果原子的偶极矩垂直于镜面，它的镜像会同向[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。这会造成相长干涉，辐射速率被增强了！

这个惊人的效应（被称为[珀塞尔效应](@keyword=purcell_effect|lang=zh-CN|style=Feynman)，Purcell effect）表明，连自发辐射这种看似原子固有的属性，都可以被其所处的环境所改变。真空并非一个被动的舞台，而是一个可以被塑造、并反过来影响物质行为的动态实体。

#### [阿哈罗诺夫-玻姆效应](@keyword=aharonov_bohm_effect|lang=zh-CN|style=Feynman)：无形之中的有形之力

这里有一个更加诡异的例子。让我们再次回到圆环上的电子，但这次在[环的中心](@keyword=center_of_a_ring|lang=zh-CN|style=Feynman)放置一个无限长的螺线管，管内有[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，而管外（电子所在处）[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)为零 [@problem_id:1989614]。根据经典物理，电子感觉不到任何[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，它的运动应该不受影响。

但在量子世界，情况并非如此。虽然[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $\vec{B}$ 为零，但磁[矢势](@keyword=vector_potential|lang=zh-CN|style=Feynman) $\vec{A}$ 并不为零。这个磁矢势会给电子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)附加一个额外的相位。其结果是，电子的能级发生了平移，平移量正比于穿过圆环的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi$！这就是著名的阿哈罗诺夫-玻姆（Aharonov-Bohm）效应。

那么，这个“幽灵般”的相互作用是否会改变我们的[选择定则](@keyword=selection_rules|lang=zh-CN|style=Feynman) $\Delta m = \pm 1$ 呢？答案是：不会！计算表明，尽管能级被移动了，但决定“握手”规则的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)角向[部分和](@keyword=partial_sums|lang=zh-CN|style=Feynman)相互作用算符 $x = R\cos(\phi)$ 的形式都没有改变。因此，跃迁规则依然如故。这是一个极其深刻的结论，它告诉我们阿哈罗诺夫-玻姆效应是一种纯粹的量子相位效应，它改变了系统的动力学（能量），却没有改变跃迁的对称性要求。

### 更深层次的统一与“阴谋”

现在，我们将深入到物质结构的核心，去看截然不同的物理规律如何交织在一起，共同谱写一曲宏伟的交响乐。

#### [振动](@keyword=oscillation|lang=zh-CN|style=Feynman)与电子的“共谋”

在像苯这样的高度对称的分子中，某些电子跃迁由于对称性的原因可能是严格禁止的 [@problem_id:1989615]。例如，苯的第一个紫外吸收带，从[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) ${}^1A_{1g}$ 到[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) ${}^1B_{2u}$ 的跃迁，按电偶极规则就是“禁止”的。然而，实验上却能观测到这个吸收带，尽管很弱。

这是怎么回事？原来是分子内部上演了一场电子与原子[核振动](@keyword=nuclear_vibrations|lang=zh-CN|style=Feynman)的“共谋”。分子中存在着各种特定对称性的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)模式。当一个具有特定对称性（比如 $e_{2g}$ 对称性）的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)被激发时，它会瞬间扭曲分子的几何构型，从而暂时打破了分子原有的高度对称性。在这一瞬间，原本“禁止”的电子跃迁能“借用”另一个能量更高、跃迁被强烈允许的电子态（如 ${}^1E_{1u}$ 态）的“跃迁强度”。

这个过程被称为赫兹伯格-泰勒（Herzberg-Teller）[振动耦合](@keyword=vibronic_coupling|lang=zh-CN|style=Feynman)。它精妙地展示了在分子内部，电子运动和原子[核振动](@keyword=nuclear_vibrations|lang=zh-CN|style=Feynman)是如何紧密地耦合在一起，彼此影响，共同决定了分子的光谱特性。

#### 弱力的裂痕：打破宇称之镜

我们故事的最高潮，来自于一个意想不到的地方：[粒子物理学](@keyword=particle_physics|lang=zh-CN|style=Feynman)的核心。到目前为止，我们讨论的所有电磁跃迁都严格遵守[宇称守恒](@keyword=parity_conservation|lang=zh-CN|style=Feynman)。这似乎是电磁相互作用一个不可动摇的定律。

然而，[宇称守恒](@keyword=parity_conservation|lang=zh-CN|style=Feynman)并非宇宙的普适定律。自然界中存在四种基本力，除了引力和[电磁力](@keyword=electromagnetic_forces|lang=zh-CN|style=Feynman)，还有[强核力](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)和[弱核力](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)。早在20世纪中叶，物理学家就震惊地发现，[弱核力](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)在它所主导的过程中（如放射性衰变）是 *不* 遵守[宇称守恒](@keyword=parity_conservation|lang=zh-CN|style=Feynman)的！它无法区分左和右。

这个效应虽然微弱，但它确实存在于原子内部。电子会通过弱相互作用与原子核（中的质子和中子）发生极其微弱的相互作用。这个相互作用势 $V_{PV}$（PV代表Parity Violating）具有破坏宇称的性质 [@problem_id:1989616]。

回到我们熟悉的氢原子 $2S \to 1S$ 跃迁。我们说过，它因为宇称相同而被[电磁力](@keyword=electromagnetic_forces|lang=zh-CN|style=Feynman)所禁止。但是，这个来自原子核内部的、微弱的“弱力之手”，就像之前讨论的外部电场一样，也会在 $2S$ 态中混入极其微小的 $2P$ 态成分。这个混合完全是原子内部自发的，不需要任何外部干预。

正是这微乎其微的混合，使得 $2S \to 1S$ 跃迁得以通过电偶极机制发生。这个跃迁的速率极其微小，与完全允许的 $2P \to 1S$ [跃迁速率](@keyword=transition_rates|lang=zh-CN|style=Feynman)之比大约只有 $10^{-23}$ 量级！然而，现代[实验物理学](@keyword=experimental_physics|lang=zh-CN|style=Feynman)的精度已经足以探测到这种由弱力“诱发”的[宇称破缺](@keyword=parity_violation|lang=zh-CN|style=Feynman)效应。这是一个震撼人心的例子，它雄辩地证明了物理学的统一性：最深奥的粒子物理规律，居然在最经典的[原子光谱学](@keyword=atomic_spectroscopy|lang=zh-CN|style=Feynman)中留下了可以被测量的蛛丝马迹。

### 终极法则：总和的守恒

我们已经看到了各种各样的规则和“例外”。规则源于理想模型的对称性，而“例外”则来自于现实世界的不完美、高阶过程、外部场的扰动，甚至是其他基本力的“客串”。这会不会让人觉得物理学充满了补丁和特例呢？

绝非如此。在这一切纷繁复杂的表象之下，隐藏着一个简单而又美丽的秩序。这就是托马斯-赖歇-库恩（Thomas-Reiche-Kuhn）求和规则 [@problem_id:1989594]。这个规则告诉我们，对于一个含有 $Z$ 个电子的原子，从任何一个初始态出发，到所有可能的终态的跃迁“强度”（用一个称为“[振子强度](@keyword=oscillator_strength|lang=zh-CN|style=Feynman)”的无量纲量来衡量）的总和，恒等于一个简单的整数：

$$
\sum_k f_{nk} = Z
$$

无论跃迁是允许的还是禁止的，是强的还是弱的，是单[光子](@keyword=photon|lang=zh-CN|style=Feynman)的还是多[光子](@keyword=photon|lang=zh-CN|style=Feynman)的，是自然的还是被外场诱导的……当我们将所有可能性加在一起时，总的“跃迁预算”是固定的，就等于体系中的电子总数。

这就像一个关于跃迁几率的“守恒定律”。它告诉我们，尽管跃迁强度可以在不同通道之间重新分配，但总量是恒定的。这一定则如同一根定海神针，在纷繁复杂的[原子光谱](@keyword=atomic_spectra|lang=zh-CN|style=Feynman)现象背后，彰显了量子力学内在的、深刻的结构性和确定性。这，正是物理学永恒的魅力所在。