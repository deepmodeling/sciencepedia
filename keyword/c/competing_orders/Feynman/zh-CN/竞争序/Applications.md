## 应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)联系

想象一个宏伟的舞厅。一些客人想跳华尔兹，成双成对地优雅滑过舞池。另一些人则希望组成一个静态的大型造型来拍集体照。还有一些人想把椅子排成引人注目的新图案。所有这些活动怎能同时进行？它们不能，至少不会不相互干扰。跳华尔兹者的空间被拍照人群侵占；椅子的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)则阻碍了两者。舞厅的最终状态——无论是跳舞、拍照、新的座位安排，还是三者混乱的混合——都是这些愿望之间*竞争*的结果。

[量子材料](@keyword=quantum_materials|lang=zh-CN|style=Feynman)的世界与这个舞厅非常相似。在低温下，电子不再是无序的人群，而常常会“密谋”进入一个更有序的状态。但是选择哪一个呢？它们可能配对形成[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，一种完美导电的状态。它们可能将其内禀磁矩，或称“自旋”，对齐以形成铁磁体或[反铁磁体](@keyword=antiferromagnets|lang=zh-CN|style=Feynman)。或者，它们可能聚集在一起，形成一种高低密度周期性交替的模式，即所谓的“电荷密度波”。在过去几十年发现的许多最引人入胜的材料中，电子同时被其中几种可能性所诱惑。

在上一章中，我们探讨了支配这些有序态的基本原理。现在，我们将看到，竞争——有时是协作——这一简单概念，并不仅仅是理论上的好奇心，而是解开真实材料最深层秘密的根本钥匙。它解释了它们令人困惑的行为，描绘了它们复杂的[相图](@keyword=phase_portraits|lang=zh-CN|style=Feynman)，并引导我们寻找新的量子现象。

### 竞争的语言：一种唯象的观点

为了讨论这场量子斗争，物理学家们发展出一种通用性极强的语言，即[金兹堡-朗道理论](@keyword=ginzburg_landau_theory|lang=zh-CN|style=Feynman)。我们无需深入其完整的数学严谨性；其核心思想惊人地简单而强大。我们想象材料有一个“能量景观”，其中山谷代表稳定、有序的状态。两种不同序之间的竞争，比如超导（由序参量 $\psi$ 描述）和[密度波](@keyword=density_wave|lang=zh-CN|style=Feynman)（$\phi$），可以被编码在自由能表达式中的一个单独项里，其形式通常为 $g |\psi|^2 \phi^2$。

耦合常数 $g$ 的符号决定了它们之间的关系。如果 $g > 0$，这两种序就是竞争者。一种序的存在会使另一种序的[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)变得更陡峭，增加了其出现的能量成本。推向极致，一个强大且预先存在的[密度波](@keyword=density_wave|lang=zh-CN|style=Feynman)可以通过使其能量谷无法企及，从而完全禁止超导的形成[@problem_id:121151]。这个简单的耦合项解释了为什么在许多材料中，超导只有在竞争的[磁序](@keyword=magnetic_ordering|lang=zh-CN|style=Feynman)或[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)序被抑制（例如通过施加压力或化学掺杂）之后才能被发现。通过调控这些外部参数，我们可以绘制出相图，甚至可以预测分隔纯磁性相与磁性超导共存相的边界线的斜率[@problem_id:62787]。

但如果 $g < 0$ 呢？这就引出了更诱人的可能性——*协作*。在这种情况下，一种[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)可以为另一种“挖掘更深的能量谷”，从而主动帮助其出现。一种本身可能在 28 K 成为[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的材料，在友好的[密度波](@keyword=density_wave|lang=zh-CN|style=Feynman)存在下，可能会发现自己在更高的温度下变为[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)[@problem_id:2534535]。这个想法非常深刻。它表明，伴随一种有序的量子涨落本身，可能为另一种有序提供了将电子粘合在一起形成超导对的“胶水”。竞争者与创造者之间的界线确实可能非常模糊。

### [量子材料](@keyword=quantum_materials|lang=zh-CN|style=Feynman)的“群英谱”

这个关于竞争与协作的故事并非虚构。它在一大批处于现代物理学研究前沿的真实材料中上演。

**铜氧化物（The Cuprates）：** 这些[铜氧化物](@keyword=cuprates|lang=zh-CN|style=Feynman)材料是首批打破[高温超导](@keyword=high_temperature_superconductivity|lang=zh-CN|style=Feynman)记录的物质。它们的相图都呈现出一个神秘而标志性的“[超导穹顶](@keyword=superconducting_dome|lang=zh-CN|style=Feynman)”。当你添加更多载流子（一个称为“掺杂”的过程）时，[超导转变](@keyword=superconducting_transition|lang=zh-CN|style=Feynman)温度 $T_c$ 并不会简单地增加。它会上升，达到一个峰值，然后再次下降。为什么？竞争序提供了答案。在穹顶的“欠掺杂”一侧，超导正在与一个被称为“[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)”的神秘对手作斗争，这个相可能涉及初生的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)序或自旋序，它们减少了可用于配对的电子数量。而在“过掺杂”一侧，基本的[配对相互作用](@keyword=pairing_interaction|lang=zh-CN|style=Feynman)本身似乎在减弱。穹顶顶点的最佳 $T_c$ 代表了这场多方面拉锯战中的一个微妙妥协，一个最佳[平衡点](@keyword=equilibrium_points|lang=zh-CN|style=Feynman)[@problem_id:3009361]。

**[铁基超导体](@keyword=iron_based_superconductors|lang=zh-CN|style=Feynman)（The Iron Pnictides）：** 如果说铜氧化物是一场优雅的决斗，那么[铁基超导体](@keyword=iron_based_superconductors|lang=zh-CN|style=Feynman)就是一场皇家大混战。在像 BaFe$_2$As$_2$ 这样的材料中，至少有三种序在争夺地位：一种条纹状的[自旋密度波](@keyword=spin_density_wave_2|lang=zh-CN|style=Feynman)（SDW）磁性、一种破坏晶体[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性的结构畸变（称为“向列性”），当然，还有超导。这三种序错综复杂地耦合在一起，导致了极其复杂的相图。当通过替换不同原子来调控材料时，可以看到磁性和结构转变温度分离开来，两者都受到抑制，然后一个[超导穹顶](@keyword=superconducting_dome|lang=zh-CN|style=Feynman)出现，并与磁性相部分重叠，从而允许微观共存[@problem_id:2996848]。

正是在这些材料中，竞争最违反直觉的后果之一显现出来。通常，人们会[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)引入无序——用杂质扰乱完美的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)——对超导这样精细的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)是有害的。但在竞争序的领地里，我敌人的敌人可能就是我的朋友。事实证明，[铁基超导体](@keyword=iron_based_superconductors|lang=zh-CN|style=Feynman)中的 SDW 序对无序的脆弱性甚至超过了超导。因此，加入可控量的杂质可以有效地压制竞争的磁性，以至于超导从其对手的压迫性影响中解脱出来，实际上可以变得*更强*，具有更高的转变温度[@problem_id:2831452]。这个美丽的悖论是潜在竞争的直接印记。

**重费米子（Heavy Fermions）：** 竞争原理远不止于超导。在一类被称为重费米子的材料中，上演着一场不同的战斗。这些材料包含一个局域磁性原子（通常是铈或镱等[稀土元素](@keyword=rare_earth_elements_2|lang=zh-CN|style=Feynman)）的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，[浸没](@keyword=submersions|lang=zh-CN|style=Feynman)在[传导电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)的海洋中。这些原子的磁矩面临两种截然不同的命运。一种可能性是 [Ruderman-Kittel-Kasuya-Yosida](@keyword=ruderman_kittel_kasuya_yosida|lang=zh-CN|style=Feynman)（RKKY）相互作用，这是一种通过传导电子介导的、磁矩之间的长程对话，驱使它们锁定成一个集体的、长程反铁磁模式。与之竞争的可能性是近藤效应（Kondo effect），这是一个局域过程，[传导电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)会包围每个单独的磁矩，屏蔽并淬灭其磁性，形成一种新颖的非磁性状态。

哪种命运会获胜？这取决于[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)与电子之间基本耦合 $J$ 的强度。在弱耦合时，RKKY 相互作用（${\propto} J^2$）获胜，[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)是磁性的。在强耦合时，[近藤屏蔽](@keyword=kondo_screening|lang=zh-CN|style=Feynman)（其能量标度呈[指数增长](@keyword=exponential_growth|lang=zh-CN|style=Feynman)，${\propto} \exp(-1/J)$）占主导，导致一个非磁性的“[重费米液体](@keyword=heavy_fermi_liquid|lang=zh-CN|style=Feynman)”[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。这两种本质上不同的物质[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)之间的转变发生在耦合的一个临界值，是竞争驱动的量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)的经典例子，并被著名的 Doniach 相图所概括[@problem_id:3018922]。

### 微观足迹与更广阔的视野

这场争夺主导地位的宏大战役在电子态的结构上留下了印记。如果我们能戴上量子护目镜，观察电子允许的能级，我们会看到什么？在一个电荷密度波与超导共存的系统中，每种序都试图在费米面上打开一个“[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)”——一个能量的禁区。在动量空间中被称为“热点”的特殊位置，两种序都处于活跃状态，由此产生的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)不是一个简单的加和，而是遵循一个类似勾股定理的法则：$E_{gap} = \sqrt{\Delta_{SC}^2 + V_{CDW}^2}$ [@problem_id:93705]。总[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)是两种竞争序[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的[平方和](@keyword=sum_of_squares|lang=zh-CN|style=Feynman)的平方根，这是它们交织在一起的本性在最基本的[电子层](@keyword=electron_shells|lang=zh-CN|style=Feynman)面上留下的印记。

最终，我们用来调控这些材料的所有旋钮——压力、化学掺杂、[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)——都是通过改变支配竞争的潜在微观参数来起作用的。施加压力可能会使晶格振动（[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）变硬，或降低费米能级上可用的[电子态密度](@keyword=electronic_density_of_states|lang=zh-CN|style=Feynman)，这通常会同时削弱超导和[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)序[@problem_id:2818833]。这为我们提供了一个强大的工具箱，不仅可以观察，还可以[主动控制](@keyword=proactive_control|lang=zh-CN|style=Feynman)这些量子相。

最后，我们必须认识到竞争可以有多种形式。它不仅可以发生在性质上完全不同的序之间（如磁性 vs 超导），也可以发生在同一种序的不同*模式*之间。在一个由两个耦合的原子层组成的系统（如双层石墨烯）中，磁性不稳定性可能面临一个选择：是形成一个自旋在每个平面*内部*交替的反铁磁模式更有利，还是一个自旋在平面*之间*交替的模式更有利？系统的选择将取决于层内[电子跳跃](@keyword=electron_hopping|lang=zh-CN|style=Feynman)与层间[电子跳跃](@keyword=electron_hopping|lang=zh-CN|style=Feynman)的相对强度。通过调整这个比率，人们可以驱动从一种磁性织构到另一种的转变，这是竞争序在另一个微妙层面上的体现[@problem_id:1233900]。

### 一条新的统一原理

从高温超导体的奇异穹顶到奇异重电子金属的行为，竞争序的概念提供了一个强大而统一的叙事。它将我们对固体的认知从静态、惰性的原子[排列](@keyword=permutation|lang=zh-CN|style=Feynman)提升到了一个动态的舞台，在这个舞台上，不同的集体量子命运竞相争夺霸权。这场持续的斗争催生了我们在量子物质中观察到的大部分丰富性和复杂性。

理解、预测并最终控制这些竞争的结果是现代科学的重大挑战之一。这是一条或许有一天能让我们设计出具有前所未有的、可按需定制性质的材料——甚至可能是梦寐以求的室温[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)——的道路。舞厅已经开放，音乐正在奏响，而这场量子之舞才刚刚开始。