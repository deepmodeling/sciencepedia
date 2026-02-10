## 应用与跨学科联系

所以，我们有了这个关于顺磁体熵的绝妙想法。我们已经看到，一堆微小磁矩（我们的小罗盘针）的序是如何被外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)和温度改变的。但这一切到底有何*用处*？这个关于自旋无序的抽象概念在现实世界中有任何实际价值吗？答案是肯定的，而且它将带领我们踏上一段从实际工程到现代物理学最深前沿的旅程。[顺磁体的熵](@keyword=entropy_of_a_paramagnet|lang=zh-CN|style=Feynman)不仅仅是一个理论上的奇观；它是一个强大的工具，一个我们可以用来操控热学世界的把手，若非如此则无法实现。

### [磁制冷](@keyword=magnetic_cooling|lang=zh-CN|style=Feynman)艺术

这一原理最直接和著名的应用是[磁制冷](@keyword=magnetic_cooling|lang=zh-CN|style=Feynman)技术，即*[绝热去磁](@keyword=adiabatic_demagnetization|lang=zh-CN|style=Feynman)*。这个想法既简单又深刻。想象你有一块顺磁盐。首先，你将它置于强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中，比如 $B_i$，同时让它与温度为 $T_i$ 的“冷浴”（如[液氦](@keyword=liquid_helium|lang=zh-CN|style=Feynman)）保持接触。[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)迫使微小的原子磁体对齐，从而产生序，并因此*降低*磁熵。这个有序化过程产生的热量，即“磁化热”，会无害地流入冷浴中被带走。

现在是见证奇迹的时刻。你对盐进行热隔离——可以说，你用一个完美的保温瓶把它包裹起来——然后你慢慢地关掉[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。自旋现在摆脱了[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的束缚，会急切地回到随机无序的状态。但正如热力学第二定律告诉我们的，在一个可逆过程中，熵不能凭空产生。系统的总熵必须保持不变。为了增加它们的磁熵，自旋需要从别处寻找熵。它们通过从材料自身的原子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中窃取热能来做到这一点。通过吸收晶格振动（[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）的能量，自旋将整个材料冷却到一个最终的、低得多的温度 $T_f$ [@problem_id:1880530] [@problem_id:1874938]。这就是*磁热效应*的本质：在绝热条件下，[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的变化引起温度的变化 [@problem_id:92769]。

当然，一次性的制冷是一回事，但一个实用的制冷机必须能连续运行。通过巧妙地安排材料在不同[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中移动，同时与热源和[冷源](@keyword=cold_sink|lang=zh-CN|style=Feynman)建立和断开热接触，工程师可以设计出连续的[制冷循环](@keyword=refrigeration_cycle|lang=zh-CN|style=Feynman)。人们可以想象一个*磁[斯特林循环](@keyword=stirling_cycle|lang=zh-CN|style=Feynman)* (magnetic Stirling cycle)，这是经典发动机的一个类似物，它利用等温磁化和去磁步骤，结合等[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)冷却和加热，将热量从冷源泵送到热沉 [@problem_id:1874924]。这类设备不仅仅是思想实验；它们对于实现科学研究和先进技术中所需的超低温度至关重要。

### 对绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)的追求

这项技术是我们达到低于1开尔文，进入毫开尔文范围乃至更低温度的主要方法。当我们向绝对零度推进时，材料的细节变得至关重要。例如，为什么要使用顺磁“盐”而不是一块纯的顺磁元素？在纯固体中，磁性离子紧密地堆积在一起。即使在外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)为零时，它们仍然能感觉到来自邻居的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。这个微小但持续存在的*内场*为温度能降到多低设定了一个下限；如果自旋之间仍在进行磁性“窃窃私语”，它们就无法变得那么无序。通过使用盐，其中磁性离子稀疏地分布在非磁性[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中，我们可以使这些相互作用变得可以忽略不计，从而让我们能够达到更低的最终温度 [@problem_id:1874898]。

为了进一步推进，我们可以从电子的磁矩转向小得多的原子*核*的磁矩。因为[核磁矩](@keyword=nuclear_magnetic_moment|lang=zh-CN|style=Feynman)比电子磁矩弱数千倍，所以它们更难与[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)对齐，并且与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的耦合也更弱。这意味着核去磁可以在电子去磁停止的地方接力，将我们从毫开尔文温度带入微[开尔文](@keyword=kelvin|lang=zh-CN|style=Feynman)甚至纳开尔文的范围 [@problem_id:57393]。

当然，现实世界并非如此理想。减小[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的过程需要时间，而且没有完美的绝热措施。总会有来自较暖环境的微小*漏热*。这产生了一个有趣的竞争：去磁过程在主动冷却样品，而漏热在不断地给它加热。可达到的最低温度不是在零[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)下实现的，而是在一个点上，此时来自减小[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的[制冷](@keyword=refrigeration|lang=zh-CN|style=Feynman)功率恰好与进入的热量相平衡。理解这些非理想效应是低温工程的一个关键方面 [@problem_id:57364]。

### 用于量子世界的“熵海绵”

也许顺磁熵最美妙的应用不仅仅是让物体变冷，而是利用这种寒冷来揭示新的物理学。顺磁体可以被看作是一个“熵海绵”。在高温下，它有很大的能力在其无序的自旋中储存熵。通过磁化它，我们把这些熵“挤压”到一个[热库](@keyword=heat_reservoir|lang=zh-CN|style=Feynman)中。然后，当我们去磁化它时，饥渴的、无序的自旋会从任何与它们有热接触的物体中吸收熵。

现在，想象一下，我们将这个熵海绵与我们想要研究的一种奇异材料接触——这种材料脆弱的量子特性只有在极低温度下才可见。

考虑一种*[量子自旋液体](@keyword=quantum_spin_liquids|lang=zh-CN|style=Feynman)*（QSL）。这是一种奇特的物质状态，即使在绝对零度下，磁矩也拒绝有序化，而保持在一种高度纠缠、波动的“液体”状态。或者考虑一种*[拓扑绝缘体](@keyword=topological_insulators|lang=zh-CN|style=Feynman)*（TI），这是一种在其体材料内是绝缘体，但在其表面上拥有奇特的、完美导电的状态的材料。这些量子系统有其独特的[热力学特征](@keyword=thermodynamic_signature|lang=zh-CN|style=Feynman)；例如，它们在低温下的[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)可能按 $C \propto T^2$ 的规律变化，这是它们[无能](@keyword=anergy|lang=zh-CN|style=Feynman)隙、涌现的激发的独特指纹 [@problem_id:57330] [@problem_id:57337]。为了观察这些微妙的效应，我们必须将样品冷却到一个温度，使得这些奇异激发的熵与普通[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)的熵相当。通过将顺磁体与QSL或TI进行热接触并执行[绝热去磁](@keyword=adiabatic_demagnetization|lang=zh-CN|style=Feynman)，我们可以有效地利用顺磁体从量子系统中吸出热熵，从而揭示其内在的量子行为。

这项技术的终极愿景位于凝聚态物理和量子信息的[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)点。在一些拓扑系统中，基本激发不是电子或[光子](@keyword=photon|lang=zh-CN|style=Feynman)，而是一种称为*[非阿贝尔任意子](@keyword=non_abelian_anyons|lang=zh-CN|style=Feynman)* (non-Abelian anyons) 的奇特[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。这些[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)有一个显著的特性，即它们的集体状态取决于它们相互编织（braided）的顺序，这使它们成为构建[容错量子计算机](@keyword=fault_tolerant_quantum_computer|lang=zh-CN|style=Feynman)的潜在平台。这样一个系统的熵与其[量子简并](@keyword=quantum_degeneracy|lang=zh-CN|style=Feynman)度——即它拥有的不同[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的数量——直接相关，而[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)就储存在这里。通过将这些[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)与顺磁盐耦合，原则上可以使用[绝热去磁](@keyword=adiabatic_demagnetization|lang=zh-CN|style=Feynman)来冷却[任意子](@keyword=anyons|lang=zh-CN|style=Feynman)系统，降低其熵，并将其初始化到一个特定的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)——这是执行[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的关键第一步 [@problem_id:57382]。

从一个简单的制冷机到一个操控[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的工具，[顺磁体的熵](@keyword=entropy_of_a_paramagnet|lang=zh-CN|style=Feynman)提供了一个惊人的例子，说明一个诞生于[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的概念如何成为开启新世界的钥匙，展示了物理学深刻而又常常令人惊讶的统一性。