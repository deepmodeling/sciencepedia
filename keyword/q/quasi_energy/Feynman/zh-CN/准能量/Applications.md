## 应用与跨学科联系

在我们迄今为止的旅程中，我们在量子力学的舞台上遇到了一个奇特的新角色：[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)。我们已经看到，对于一个被周期性力抛来抛去的系统，旧的、舒适的固定能级概念让位于一个闪烁的、动态的准能量景观。你可能会认为这只是一个数学技巧，一个为处理混乱情况而设的方便的虚构。但事实远非如此！这个概念不仅仅是一个计算工具；它是一把钥匙，开启了一个新的物理学领域，一个我们不仅能找到具有有趣性质的材料，而且能通过用时间“雕刻”物质来*按需创造*这些性质的领域。我们即将看到这个思想如何让我们使粒子停下脚步，锻造自然界中不存在的奇异材料，甚至制造以新方式滴答作响的时钟。

### 一次一脉冲，控制量子世界

让我们从一个单一的原子开始。在它安静、未受扰动的状态下，它有一系列清晰的能级阶梯。一个电子可以通过吸收一个恰好能量的[光子](@keyword=photon|lang=zh-CN|style=Feynman)从较低的梯级跳到较高的梯级——不多也不少。这赋予了原子特有的、尖锐的吸收光谱，即它们独特的指纹。但是，如果我们不只是用温和的探测光轻推原子，而是用强大的、有节奏[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的激光场轰击它，会发生什么？

原子不再是自己的主宰。原子和强大的光场变成了一个不可分割的整体——一个“[缀饰原子](@keyword=dressed_atoms|lang=zh-CN|style=Feynman)”。这个新的复合体有它*自己*的能级，而这些正是我们一直在讨论的[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)。如果我们现在用第二束弱探测光来进行[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)研究，我们会发现一些非凡的现象。旧的吸收线发生了位移，新的吸收线凭空出现了！原子现在可以在吸收一个探测[光子](@keyword=photon|lang=zh-CN|style=Feynman)的同时，吸收或发射一个、两个或更多个来自强驱动场的[光子](@keyword=photon|lang=zh-CN|style=Feynman)。这些就是“边带”，它们的存在直接证实了[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)态是物理上真实的。这些新跃迁的强度可以计算出来，并且它们被著名的贝塞尔函数完美地描述，这些函数依赖于驱动场的强度和频率 [@problem_id:482295]。我们实际上已经用光重新设计了原子的能量结构。

这种控制可以导致更惊人的效应。想象一个在[半导体超晶格](@keyword=semiconductor_superlattices|lang=zh-CN|style=Feynman)中的电子，这就像一个[排列](@keyword=permutation|lang=zh-CN|style=Feynman)完美的蛋托，一长串量子阱。一个置于某个阱中的电子通常可以“隧穿”过势垒到达它的邻居。这种隧穿是产生电流的原因。现在，让我们通过施加一个均匀的、[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的电场来摇晃整个系统。你[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)发生什么？当然，摇晃系统应该会让电子晃动得更厉害，帮助它移动。但实际情况并非如此。

在某些精细调整的条件下，会发生完全相反的情况：隧穿被完全抑制了！电子被冻结在它的阱中，无法移动到邻近的阱，材料实际上变成了一个绝缘体。这个奇异的现象被称为**动力学局域化** [@problem_id:2135017]。[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)在一个完整周期内平均后，会产生一个可调的有效隧穿率。就像你可以用恰到好处的时机推一个荡秋千的孩子让他们停下来一样，驱动场也可以被调整到使有效隧穿率精确为零。同样，这个美妙效应的条件由一个[贝塞尔函数的零点](@keyword=zeros_of_bessel_functions|lang=zh-CN|style=Feynman)决定，$J_0(\alpha) = 0$，其中 $\alpha$ 是一个关联场强与其频率的参数。摇晃一个系统让它静止——这就是 Floquet 工程所能实现的深刻而反直觉的魔法。

### 锻造新的物相

[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)的力量远不止于操纵单个粒子。它使我们能够创造全新的、物质的集体相——具有在任何静态、平衡系统中都不可能实现的性质的材料。

也许最引人注目的成功案例是**Floquet [拓扑绝缘体](@keyword=topological_insulators|lang=zh-CN|style=Feynman)**的创造。如你所知，正常的绝缘体不导电。拓扑绝缘体是一种奇怪的野兽：它的体态是绝缘的，但根据量子拓扑定律，其表面或边缘必须是完美的导体。这些边缘流非常稳健；它们可以绕过缺陷流动而不会发生散射。

令人震惊的发现是，人们可以从一种完全普通的、“平庸的”绝缘材料开始，仅仅通过用精心设计的光栅激光照射它，就能将其转变为[拓扑绝缘体](@keyword=topological_insulators|lang=zh-CN|style=Feynman) [@problem_id:2867330]。[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)从根本上改写了系统的拓扑特性。这种[拓扑性质](@keyword=topological_property|lang=zh-CN|style=Feynman)不是在任何瞬间的哈密顿量“快照”中找到的，而是在一个完整周期内量子演化扭曲、缠绕的性质中体现的。通过驱动系统跨越一个[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，系统可以从拓扑平庸变为非平庸，这个[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)的标志是[准能](@keyword=quasienergy|lang=zh-CN|style=Feynman)谱中[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的关闭和重新打开 [@problem_id:1254150] [@problem_id:697600]。

这为“按需”制造[拓扑材料](@keyword=topological_materials|lang=zh-CN|style=Feynman)打开了一扇门。我们可以用一个[激光脉冲](@keyword=laser_pulses|lang=zh-CN|style=Feynman)来开启和关闭这些奇异的边缘态。这个想法不仅仅适用于电子。在**[拓扑光子学](@keyword=topological_photonics|lang=zh-CN|style=Feynman)**中，类似的原理被用来为光创造稳健的通道，引导[光子](@keyword=photon|lang=zh-CN|style=Feynman)沿着对缺陷免疫的路径前进 [@problem_id:782174]。更令人兴奋的是，这些技术可能是一条在驱动的超导线中实现**Majorana [费米子](@keyword=fermion|lang=zh-CN|style=Feynman)**——即它们自身的[反粒子](@keyword=antiparticles|lang=zh-CN|style=Feynman)的奇异粒子——的途径 [@problem_id:1139558]。由于 Majorana [费米子](@keyword=fermion|lang=zh-CN|style=Feynman)被预测是构建容错量子计算机的关键成分，Floquet 工程已将我们置于这场技术革命的最前沿。

仿佛这还不够，[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)催生了一种曾被认为不可能的物相：**[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)**。我们熟悉空间中的晶体，比如盐晶体，其中原[子图](@keyword=subgraph|lang=zh-CN|style=Feynman)案一遍又一遍地重复。[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)是一个其最低能量态表现出在*时间*上重复的图案的系统。在[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)的量子系统中实现的[离散时间晶体](@keyword=discrete_time_crystals|lang=zh-CN|style=Feynman)则更加奇特。当你用周期 $T$ 驱动它时，它不会以周期 $T$ 响应。相反，它会自发地选择以 $2T$、$3T$ 或驱动周期的某个整数倍的周期[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。它自发地打破了驱动的离散[时间平移对称性](@keyword=time_translation_symmetry_2|lang=zh-CN|style=Feynman)。这种亚[谐波](@keyword=harmonic_waves|lang=zh-CN|style=Feynman)的滴答声是一种稳健的物相，而不仅仅是简单的共振，其稳定性受到其[准能](@keyword=quasienergy|lang=zh-CN|style=Feynman)谱中[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的保护 [@problem_id:1207232]。这是一种根本上新的序，一种以其自身内部节奏滴答作响的集体[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。

### [量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的新视角

一个伟大物理概念的统一力量，在于它会出现在意想不到的地方。[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)的思想为[量子算法](@keyword=quantum_algorithms|lang=zh-CN|style=Feynman)提供了一个令人惊讶而深刻的新视角。

考虑 Grover [算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，这是一个著名的量子秘籍，用于搜索一个非结构化数据库，就像在一个巨大的电话簿中寻找一个特定的名字。该[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)包括一遍又一遍地应用同一个两步操作——一个“[预言机](@keyword=oracle_machines|lang=zh-CN|style=Feynman)”踢，然后是一个“扩散”混合。每一次应用都是一次迭代，是时间上的一个步骤。

但是等等！一个一遍又一遍重复相同操作的过程，正是在 Floquet 系统中看到的频闪动力学。因此，我们可以将 Grover 算符视为一个 Floquet 算符，即在一个[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)“周期”内演化系统的幺正矩阵 [@problem_id:90457]。从这个视角看，寻找标记态变成了一个 Floquet 物理学问题！对[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)而言重要的两个特殊[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)（起始态和标记态）定义了这个 Floquet 算符的两个特殊本征态，每个都有其自身的[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)。整个搜索的动力学只不过是在这两个[本征态](@keyword=eigenstates|lang=zh-CN|style=Feynman)张成的二维空间中的简单旋转，旋转角度与[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)差直接相关。这个美妙的联系为我们理解该[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)如何工作及其速度为何如此提供了强大的物理直觉。它表明，量子动力学的深刻思想已经融入了[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)的结构之中。

从控制原子到锻造新的物态，再到理解[量子算法](@keyword=quantum_algorithms|lang=zh-CN|style=Feynman)，[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)的概念已经证明它远不止是一个数学上的奇物。它是一种新物理学的语言——一种由时间本身塑造和构筑的运动中系统的物理学。它证明了有时候，通过搅动事物，我们会发现一种比我们想象中更深刻、更美丽的秩序。