## 应用与跨学科联系

我们已经穿过镜子，进入了[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)的奇异世界，理解了允许物质自发打破[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)的离散节律的基本原理。我们已经看到，与我们的日常直觉相反，量子系统不一定会升温并“融化”成毫无特征的均匀汤。但这引出了一系列新问题。这仅仅是一个理论上的奇观，一个用方程玩出的巧妙把戏吗？还是说这个概念有实际意义？我们可能在何处找到这些物质相，它们又能教给我们关于更广阔的物理学世界什么呢？

本章正是为了回答这些问题而展开的旅程。我们将看到物理学家们如何学习在实验室中构建和验证[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)。然后，我们将进一步探索，了解打破时间对称性这个简单的想法如何与其他看似无关的科学领域——从玻璃和磁体的物理学到关于对称性的最深刻定理，甚至到奇异的[拓扑物质](@keyword=topological_matter|lang=zh-CN|style=Feynman)领域——建立起强大的桥梁。这不仅是一个关于应用的故事，也是一个关于统一的故事。

### 创造与探测的艺术：工程构筑物质相

如何建造一个时钟，其滴答声不是由任何外部齿轮决定，而是由其自身量子组分的集体意愿决定？最被充分理解的一种[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)的配方包含三个关键要素：一组相互作用的[量子自旋](@keyword=quantum_spin|lang=zh-CN|style=Feynman)，一个周期性的“踢”来向系统注入能量，以及一种特殊类型的绝缘材料来防止它“沸腾”。

“踢”通常是一个经过精心校准的能量脉冲，旨在翻转系统中的所有自旋，即所谓的 $\pi$ 脉冲 [@problem_id:3021727]。在这些踢之间，自旋被留下来自行相互作用。直观地看，你会[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)重复的踢会向系统倾倒能量，直到它加热到无限温度，抹去任何记忆或秩序。这就是关键的第三个要素发挥作用的地方：**[多体局域化 (MBL)](@keyword=many_body_localization_(mbl)|lang=zh-CN|style=Feynman)**。在某些无序、相互作用的系统中，MBL 充当完美的量子绝缘体，阻止能量和信息的传输。它将系统“冻结”在一个非热状态，保护它免于升温，并使其能够保留记忆。MBL 相为[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)的存在提供了必要的刚性 [@problem_id:3021727]。

但仅仅观察到两倍于驱动周期的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)是不够的。一个荡秋千的孩子可以每隔一个周期被推一次；但这并不能使这个孩子成为一个[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)。关键在于相的*鲁棒性*。一个真正的[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)不是一个精细调节的噱头。它是一个稳定的物质相，就像冰或水一样。为了证明这一点，实验物理学家必须进行一系列严格的压力测试。他们可能会稍微[失谐](@keyword=detuning|lang=zh-CN|style=Feynman)脉冲，使其成为一个“近$\pi$”脉冲而不是完美的脉冲。或者他们可能会在驱动中引入小的、静态的不完美性 [@problem_id:3021768]。一个真正的[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)会在这些不完美性的一定范围内，顽固地将其节律锁定在双[倍周期](@keyword=period_doubling|lang=zh-CN|style=Feynman)上。它的[振荡频率](@keyword=oscillation_frequency|lang=zh-CN|style=Feynman)不会漂移；它被钉住了。此外，这种行为必须持续极长的时间——时间有序的寿命应随系统尺寸的增大而增长——并且它不应依赖于你开始时所处的特定初始状态 [@problem_id:3021762]。只有通过这些严格的测试，我们才能自信地将自发时间[对称性破缺](@keyword=symmetry_breaking|lang=zh-CN|style=Feynman)与微不足道的[受迫响应](@keyword=forced_response|lang=zh-CN|style=Feynman)区分开来。

### 扩展家族：超越MBL[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)

虽然 MBL 为[稳定时间](@keyword=settling_time|lang=zh-CN|style=Feynman)晶体提供了一种鲁棒的机制，但大自然一如既往地比我们最初的猜测更有创造力。[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)家族比那些需要完美隔离的种类更为广泛。

家族中一个迷人的分支生活在**[开放量子系统](@keyword=open_quantum_systems|lang=zh-CN|style=Feynman)**的世界里。如果我们不试图完美地隔离我们的系统，而是有意识地将其与环境耦合，会怎么样？这就引出了**耗散[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)**的概念。在这里，驱动和耗散（能量损失）之间精心设计的平衡可以将系统引导到一个非平衡稳态，这个[稳态](@keyword=steady_state_2|lang=zh-CN|style=Feynman)不是静态的，而是一个稳定的[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)。系统在多种状态间永恒地循环运动，其周期是驱动周期的整数倍。其稳定性不是由局域化提供的，而是因为这个极限环是一个*[吸引子](@keyword=attractors|lang=zh-CN|style=Feynman)*：任何附近的状态最终都会被吸引到这个亚谐波之舞中，就像大理石螺旋落入碗底一样 [@problem_id:3021730]。这表明，通常作为[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)和衰变来源的耗散，可以被用来创造和保护奇异的量子序形式。

另一种变体出现在具有长程相互作用的系统中，其中每个粒子都能感受到其他所有粒子的影响，即使是远处的粒子。在这样的系统中，可以形成**[预热](@keyword=preheating|lang=zh-CN|style=Feynman)[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)**。这里的稳定性来自于一种让人联想到经典[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的能量论证。创建一个“缺陷”——一个与[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)节律不同步的小区域——的能量成本可以被证明会随着缺陷尺寸的增大而无限增长。这使得可能融化[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)的大尺度涨落变得代价高昂。[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)在最终热化之前，可以在一个参数上很长的时间内保持稳定。我们甚至可以为[长程相互作用](@keyword=long_range_interactions|lang=zh-CN|style=Feynman)定义一个临界衰减指数，超过这个指数，稳定性就会丧失，这描绘了一幅由与[平衡态](@keyword=equilibrium_states|lang=zh-CN|style=Feynman)物质惊人相似的原理所支配的[非平衡相变](@keyword=nonequilibrium_phase_transitions|lang=zh-CN|style=Feynman)图景 [@problem_id:1258617]。

### 物理学殿堂中的回响：跨学科的桥梁

或许[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)最深刻的贡献在于它们与物理学中其他基本概念的共鸣方式，揭示了我们理论结构中更深层次的统一性。

**通向[无序系统](@keyword=disordered_systems|lang=zh-CN|style=Feynman)的桥梁：时间中的自旋玻璃**

“冻结”而又无序的状态是[自旋玻璃](@keyword=spin_glass|lang=zh-CN|style=Feynman)物理学的中心主题。自旋玻璃是一种磁体，其中相互竞争的相互作用和无序阻止了自旋铁磁性地[排列](@keyword=permutation|lang=zh-CN|style=Feynman)，而是使它们冻结成一个复杂但静态的随机模式。一个[多体局域化](@keyword=many_body_localization|lang=zh-CN|style=Feynman)的[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)，在深层次上，就是一种“时间中的自旋玻璃”。局域属性被冻结，永久保留其初始状态的记忆，但它们也以一个刚性的周期[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。

这种类比不仅仅是诗意的。物理学家已经借用自旋玻璃的概念工具包来分析[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)。例如，用于测量传统[自旋玻璃](@keyword=spin_glass|lang=zh-CN|style=Feynman)中冻结程度的 **Edwards-Anderson 序参量**，可以被改编成一个*时间的* Edwards-Anderson 参量。这个新工具 $q_T$ 测量局域关联的长时记忆，在任何避免[热化](@keyword=thermalization|lang=zh-CN|style=Feynman)的相中都变为非零，这包括[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)以及“时间玻璃”——即冻结但不[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的相 [@problem_id:3021743]。为了专门诊断一个在空间上也是自旋玻璃的[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)（一个“$\pi$-自旋玻璃”），人们必须发明一个更专门的[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)，它对空间随机性和[倍周期](@keyword=period_doubling|lang=zh-CN|style=Feynman)时间[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)都敏感 [@problem_id:3021749]。这种思想的[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)授粉丰富了这两个领域。

**通向基本对称性的桥梁：Goldstone 的幽灵**

物理学中最优美的结果之一是 [Goldstone 定理](@keyword=goldstone_s_theorem|lang=zh-CN|style=Feynman)。它指出，每当一个*连续*对称性被自发破缺时，就必须出现一个无质量（或无能隙）的激发，称为 [Goldstone 玻色子](@keyword=goldstone_bosons|lang=zh-CN|style=Feynman)。经典的例子是铁磁体：支配定律不偏好任何方向，但磁体的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)却偏好一个方向，从而打破了旋转对称性。由此产生的 Goldstone 模是长波长的[自旋波](@keyword=spin_waves|lang=zh-CN|style=Feynman)，其产生几乎不耗费能量。

然而，[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)打破的是一个*离散*对称性——即由一个驱动周期 $T$ 进行的[时间平移对称性](@keyword=time_translation_symmetry_2|lang=zh-CN|style=Feynman)。系统选择以 $2T$ 而不是 $T$ 的周期响应。[Goldstone 定理](@keyword=goldstone_s_theorem|lang=zh-CN|style=Feynman)对此有何说明？该定理以一种优美的方式被修正了。与破缺对称性相关的集体模仍然存在，但它不再是无能隙的。激发这个模需要有限的能量。这个“有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的赝 [Goldstone 模](@keyword=goldstone_modes|lang=zh-CN|style=Feynman)”可以被认为是一个有质量的粒子，其质量由破缺对称性的离散性所赋予。这一普适原理，将破缺对称性的性质与其激发的[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)联系起来，在[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)的动力学中得到了具体而优雅的实现 [@problem_id:1992876]。

**通向[拓扑物质](@keyword=topological_matter|lang=zh-CN|style=Feynman)的桥梁：奇异物质的二重奏**

在过去的几十年里，[拓扑物质](@keyword=topological_matter|lang=zh-CN|style=Feynman)相的发现彻底改变了物理学。这些相的性质是鲁棒的，因为它们被编码在系统[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的全局拓扑结构中，这著名地导致了在绝缘体块材边缘出现受保护的导电态。

一个大胆的问题出现了：我们能将这两个奇异的概念结合起来吗？**拓扑[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)**能否存在？答案似乎是肯定的。可以设想一个由两个相互关联的部分构成的系统。一部分是一个无序、相互作用的自旋系统——[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)的引擎——它在块材内部提供鲁棒的、受 MBL 保护的亚谐波[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。另一部分是一个非相互作用的系统，被设计成一个*[弗洛凯拓扑绝缘体](@keyword=floquet_topological_insulators|lang=zh-CN|style=Feynman)*，这是一个驱动系统，其性质包括特殊的边缘模，这些边缘模天然地以恰好两倍于驱动周期的频率[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)（所谓的 $\pi$-模）。

通过将这两个系统耦合在一起，可以创造出一个单一、统一的物质相，它同时是一个[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)和一个拓扑相。整个材料的块体以[倍周期](@keyword=period_doubling|lang=zh-CN|style=Feynman)节律脉动，在其边界上存在鲁棒的[拓扑边缘态](@keyword=topological_edge_states|lang=zh-CN|style=Feynman)，它们也加入了这个亚谐波交响乐。这样的相展示了物理原理的非凡模块化特性，允许我们将一层奇异的物理学叠加在另一层之上，从而创造出全新的、双重奇异的东西 [@problem_id:3021745]。

对[自发时间平移对称性破缺](@keyword=spontaneous_time_translation_symmetry_breaking|lang=zh-CN|style=Feynman)的研究仍处于起步阶段。它已经迫使我们重新思考“物质相”可以是什么的概念，并揭示了物理学版图上意想不到的联系。它强有力地提醒我们，即使是最熟悉的概念，如时间和秩序，在丰富而反直觉的量子世界中探索时，也蕴藏着深刻的惊喜。