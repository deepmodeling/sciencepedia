## 应用与跨学科联系

在我们穿越超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)基本原理的旅程之后，人们可能在感到惊奇的同时，也会提出一个实际问题：这一切到底有什么用？“行为理想”的I类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)和“复杂”的II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)之间的区别，似乎只是物理学家们争论的[分类学](@keyword=systematics|lang=zh-CN|style=Feynman)细节。事实远非如此。实际上，正是II类材料丰富而复杂的行为——那些使其偏离I类同类简单、完美[抗磁性](@keyword=diamagnetism|lang=zh-CN|style=Feynman)的特性——为革命性技术和对量子世界的深刻新见解打开了大门。

它们的应用故事，就是驯服[量子涡旋](@keyword=quantum_vortices|lang=zh-CN|style=Feynman)的故事。一个最初只是理论上的奇思——携带单个磁通量子 $\Phi_0$ 的微小[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)漩涡——最终成为医院MRI设备、巨型[粒子加速器](@keyword=particle_accelerators|lang=zh-CN|style=Feynman)以及[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)研究前沿领域中上演的大戏的主角。

### 实验的艺术：锁定现实

在我们能够利用一种新现象进行建设之前，我们必须首先测量它。我们在教科书上绘制的相图，其清晰的线条标志着临界场 $H_{c1}$ 和 $H_{c2}$ 的边界，是一种理想化。在真实的实验室里，测量这些值是一门精细的艺术，是理论与实验相互作用的美好范例。

想象一下，你拿到了一块新发现的II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。一位理论家告诉你，如果你将其磁化强度 $M$ 对外加[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $H$ 作图，你应该会看到一条笔直的[抗磁性](@keyword=diamagnetism|lang=zh-CN|style=Feynman)直线，直到 $H_{c1}$ 处，此时线条会突然弯曲，因为涡旋开始进入。然后它会向上弯曲，直到在 $H_{c2}$ 处与正常态线相交，此时超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)消失。这听起来很简单。但当你尝试时，你得到的是一个混乱的、依赖于历史的磁滞回线。为什么？

第一个罪魁祸首是样品自身的磁性。任何磁化的物体都会产生自己的“退磁”场，这会改变材料*内部*的场。[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)不关心你在实验室施加的场；它只对自己实际感受到的总场做出响应。对于形状不规则的样品，这个内场是一个复杂的混乱局面。实验学家们早就知道，解决方案是小心地将你的样品塑造成一个椭球体。对于这种特殊形状，内场保持均匀，从而可以干净地减去退磁效应，找到材料真正响应的场。

第二个，也是更深层次的复杂性在于，真实的材料并非完美无瑕。它们有缺陷：原子缺失、杂质、[晶界](@keyword=grain_boundary|lang=zh-CN|style=Feynman)。这些缺陷可以充当涡旋的粘[滞点](@keyword=stagnation_points|lang=zh-CN|style=Feynman)。这种“钉扎”意味着需要额外的推力才能让涡旋进入材料，而一旦进入就很难让它们出来。这就是[磁滞](@keyword=magnetic_hysteresis|lang=zh-CN|style=Feynman)的起源，那个取决于你是增加还是减少[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的混乱回线。为了测量真正的*[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)*临界场，实验者必须使用非常干净、高质量的晶体，其钉扎效应最小，并且以极慢的速度扫描[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，确保系统始终处于平衡状态。通过一丝不苟地校正这些效应，人们最终可以揭示隐藏在真实世界测量复杂性之下的理想化[相界](@keyword=phase_boundary|lang=zh-CN|style=Feynman)[@problem_id:2869234]。这种理论与实验现实之间的精妙互动是任何应用的第一步。

### 用涡旋进行工程：双刃剑

对基础物理学家来说是麻烦的东西，对工程师来说可能是一座金矿。正是这个让 $H_{c1}$ 的测量变得复杂的[涡旋钉扎](@keyword=vortex_pinning|lang=zh-CN|style=Feynman)，成为了超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)最重要应用的关键。

首先，让我们考虑涡旋的“坏”的一面。假设你用II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)制成一根导线，并试图让电流通过它。如果这根导线处于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中（即使是其自身电流产生的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)），其内部就会有涡旋。你推过导线的输运电流会对这些涡旋施加洛伦兹力。如果涡旋可以自由移动，电流就会将它们拖过导线。但根据[法拉第感应定律](@keyword=faraday_s_law_of_induction|lang=zh-CN|style=Feynman)，移动的磁涡旋伴随着电场。平行于电流的电场意味着功率耗散（$P = \vec{J} \cdot \vec{E}$）！[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)不再是无损的；它产生了“[磁通流](@keyword=flux_flow|lang=zh-CN|style=Feynman)阻”。这就像试图趟过沼泽地——推动涡旋穿过粘滞的电子流体的努力会产生热量并浪费能量[@problem_id:27571]。为了让[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)能够无损耗地承载大电流，涡旋*必须*被固定住。

这就把我们带到了“好”的一面：我们可以设计材料来做到这一点。通过有意引入密集的缺陷阵列——纳米尺度的析出物、[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)、晶界——我们可以创造出强大的钉扎中心来固定涡旋[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。这种材料被称为“硬”[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。在硬[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，即使电流对涡旋施加强大的[洛伦兹力](@keyword=lorentz_force|lang=zh-CN|style=Feynman)，它们仍然被困住。[磁通流](@keyword=flux_flow|lang=zh-CN|style=Feynman)阻降至零，材料可以再次无耗散地承载巨大的电流。

这种捕获磁通的能力使得II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)成为强力磁体的基础。当你对硬[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)施加强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，然后关闭外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)时，涡旋被钉扎住无法逃逸。材料保留了强大的内部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，成为一块强[永磁体](@keyword=permanent_magnets|lang=zh-CN|style=Feynman)。著名的[Bean临界态模型](@keyword=bean_critical_state_model|lang=zh-CN|style=Feynman)为这一过程提供了一个优美简洁的图景：在磁通穿透的区域，屏蔽电流以其可能的最大值，即[临界电流密度](@keyword=critical_current_density|lang=zh-CN|style=Feynman) $J_c$ 流动，形成了一个可以计算和工程设计的俘获场分布[@problem_id:2968334]。这就是MRI设备中用于成像我们身体的[超导磁体](@keyword=superconducting_magnets|lang=zh-CN|style=Feynman)，以及[大型强子对撞机](@keyword=large_hadron_collider|lang=zh-CN|style=Feynman)中用于引导质子以接近光速运动的磁体的原理。

当然，天下没有免费的午餐。捕获磁通的强钉扎效应也导致了大的[磁滞](@keyword=magnetic_hysteresis|lang=zh-CN|style=Feynman)。磁化回线所包围的面积代表了在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的一个循环中，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中以热量形式耗散的能量。对于一个开启后保持不变的直流磁体来说，这不是一个主要问题。但对于任何交流应用，如故障电流限制器或[变压器](@keyword=transformers|lang=zh-CN|style=Feynman)，这种耗散都是一个必须管理的严峻工程挑战[@problem_id:1783092]。

### 通往量子灵魂的窗口

到目前为止，我们一直将涡旋视为可为技术所用的经典对象。但它们的行为也为我们提供了一个极其灵敏的窗口，以窥探超导态深层的量子力学。当今物理学前沿的宏大问题是：所有的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)都一样吗？它们都遵循最初的Bardeen-Cooper-Schrieffer（BCS）理论，该理论描述了电子配对形成一个具有完整、各向同性[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)（[s波](@keyword=s_waves|lang=zh-CN|style=Feynman)态）的状态吗？或者是否存在“非常规”[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，其配对更为奇特，导致[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)存在节点——即[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)在某些方向上消失（如d波态）？

涡旋[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)为解开这个谜题提供了关键。让我们思考一下低能[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)——那些未被束缚在[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)中的电子。在一个传统的、全[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，在极低的温度下，这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)只能存在于涡旋的正常核心内部。由于涡旋的数量与[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $H$ 成正比，低能态的数量（以及像比热这样的性质）应该随 $H$ 线性增长。

在有节点的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，情况完全不同。在这里，即使在[零场](@keyword=null_field|lang=zh-CN|style=Feynman)下，低能[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)也可以存在于[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的节点处。当施加[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)时，涡旋周围旋转的[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)会产生一个奇妙的效应。穿过这个超流的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)会经历能量的[多普勒频移](@keyword=doppler_shift|lang=zh-CN|style=Feynman)。这种频移可以产生大量的零能态，不仅在核心中，而且遍布整个材料体。仔细的理论分析表明，这种机制导致的低能态数量不是随 $H$ 线性增长，而是随 $\sqrt{H}$ 增长[@problem_id:2988278]。

通过测量像[比热](@keyword=specific_heat|lang=zh-CN|style=Feynman)或[磁穿透深度](@keyword=magnetic_penetration_depth|lang=zh-CN|style=Feynman)这样的性质随温度和微小[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的变化，实验学家可以寻找这种标志性的 $\sqrt{H}$ 依赖关系，以区别于线性的 $H$ 依赖关系。这已成为鉴定新材料中非常规超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)的基准技术。这是一个协同作用的绝佳例子：涡旋[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的宏观结构，作为II类行为的结果，充当了诊断[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)微观[量子力学对称性](@keyword=quantum_mechanics_symmetry|lang=zh-CN|style=Feynman)的工具[@problem_id:2840845]。

### 当世界碰撞：超导与磁性

也许对我们所讨论原理最引人注目的展示，来自于那些固态物理中两种最强大的集体现象——超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)和磁性——试图共存的材料。乍一看，这似乎不可能。传统的自旋单态超导涉及自旋相反的电子配对，而铁磁性则涉及自旋对齐。一种材料怎么能同时做到这两点？

答案再次在于仔细考虑区分I类和II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的[特征长度尺度](@keyword=characteristic_length_scales|lang=zh-CN|style=Feynman)：相干长度 $\xi$（[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的“尺寸”）和[磁穿透深度](@keyword=magnetic_penetration_depth|lang=zh-CN|style=Feynman) $\lambda$。

想象一种材料，在冷却时，首先变得有[磁序](@keyword=magnetic_ordering|lang=zh-CN|style=Feynman)，然后在更低的温度下，想要变成[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。假设这种磁性不是简单的铁磁体，而是一种[螺旋结构](@keyword=helical_structure|lang=zh-CN|style=Feynman)，其磁化方向以一个非常短的波长 $\ell_m$ 旋转。现在，如果库珀对的尺寸 $\xi$ 比这个磁波长*大得多*（$\ell_m \ll \xi$），奇妙的事情发生了。组成一个库珀对的两个电子，分布在 $\xi$ 的距离上，经历了[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的多次完整[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。它们感受到的净磁交换场平均下来几乎为零！库珀对实际上对快速[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的磁性是“盲”的，可以形成而不会被撕裂。这就像看一个旋转的轮子：如果它转得足够快，个别颜色会模糊成中性的灰色。

但如果除了这个[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)分量，磁性还有一个小的、净的均匀分量呢？材料现在发现自己内部有一个它自己产生的均匀[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。如果它是一个强II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)（$\kappa = \lambda/\xi \gg 1$），并且这个内场强于 $B_{c1}$ 但弱于 $B_{c2}$，那么材料的响应既合乎逻辑又令人惊奇：它通过形成一个自发的[阿布里科索夫涡旋晶格](@keyword=abrikosov_vortex_lattice|lang=zh-CN|style=Feynman)来允许其自身的磁通穿透。这个“自发涡旋相”是一个美丽的、自组织的[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)，其中超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)和磁性达到了量子妥协，而这一切完全是由II类[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)的灵活性所促成的[@problem_id:2862576]。

从测量的实际挑战到强大磁体的工程设计，从探测物质的量子本性到见证两种截然相反的电子序的结合，II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的物理学是一个丰富而充满活力的领域。始于一个简单的问题——当磁通穿透[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)时会发生什么？——最终展开成一幅宏伟的画卷，交织着现代科学中一些最深刻和最有用的思想。