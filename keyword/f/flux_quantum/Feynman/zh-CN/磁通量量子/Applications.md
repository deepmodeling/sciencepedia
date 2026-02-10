## 应用与跨学科联系

在揭示了磁通量量子优美的量子力学起源之后，你可能会倾向于将其归类为一种虽优雅但深奥的物理学知识。但事实远非如此！这个离散的磁性包裹不仅仅是一个理论上的奇珍；它是一个自然界的[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)，已经成为一个强大的工具、一种诊断探针和一项设计原则，横跨了惊人广泛的科学技术领域。它的发现不仅打开了理解超导性的大门，也开启了在宏观尺度上操控量子世界的大门。让我们来了解其中一些引人入胜的应用。

### 终极磁传感器：SQUID

想象一下，你想测量一个极其微弱的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)——比如人脑中[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)放电时发出的微弱信号。你传统的磁力计对这种微弱的信号完全无能为力。你所需要的是一种其灵敏度仅受量子力学定律本身限制的设备。这正是[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)（SQUID）的精髓所在。

[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的核心是一个简单的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)。正如我们所学到的，任何被困在这个环内的磁通量都不能取任意值。相反，它必须是磁通量量子$\Phi_0 = h/(2e)$的整数倍。允许的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)值形成一个阶梯，每个梯级之间[相差](@keyword=phase_contrast|lang=zh-CN|style=Feynman)一个磁通量量子 [@problem_id:1828341]。如果你测量了一个被困的磁通量，你可以立即知道有多少个量子“卡”在环中，就像数离散粒子一样 [@problem_id:1828413]。

SQUID以一种极其巧妙的方式利用了这种离散性。它不仅能测量静态的[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman)量，而且对外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的*变化*极为敏感。通过在环路中加入称为[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)的特殊元件，设备两端的电压成为穿过它的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的[振荡函数](@keyword=oscillating_functions|lang=zh-CN|style=Feynman)。至关重要的是，这些[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的周期恰好是一个[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子$\Phi_0$ [@problem_id:1775616]。每当外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的变化足以使穿过环路的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)增加或减少一个磁通量量子时，SQUID的输出电压就完成一个完整的周期。

通过计算这些[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，我们可以以惊人的精度测量[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的变化。SQUID的理论分辨率取决于多小的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)变化$\Delta B$对应于一个磁通量量子穿过其面积为$A$的探测环。一个简单的计算表明，这个值是$\Delta B = \Phi_0 / A$ [@problem_id:1828385]。对于一个面积为几平方毫米的环路，这对应着比地球[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)小数十亿倍的灵敏度。这使得[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)在医学（用于脑磁图（MEG），通过探测其[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)来绘制大脑活动图）、[地质学](@keyword=geology|lang=zh-CN|style=Feynman)（用于勘探和探测地下结构）以及基础物理研究等不同领域成为不可或缺的工具。

### [超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的核心：涡旋与临界场

[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子不仅仅是[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)的一个属性；它被编织在超导态本身的结构之中。当我们观察所谓的II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)时，这一点变得尤为清晰。

与它们的I类“表亲”试图完全排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)（迈斯纳效应）不同，II类材料达成了一种更有趣的折衷。在超过某个[磁场强度](@keyword=magnetic_field_intensity|lang=zh-CN|style=Feynman)（$B_{c1}$）时，它们允许[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)穿透，但穿透方式是高度组织化和量子化的。[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)以微小、离散的[线束](@keyword=pencil_of_lines|lang=zh-CN|style=Feynman)（称为磁通涡旋或磁通子）穿过材料。这些涡旋中的每一个都精确地携带一个[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子$\Phi_0$ [@problem_id:1812485]。

你可以将处于这种“混合态”的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)想象成一块瑞士奶酪，其大部分材料保持超导，但被一系列正常态的核心刺穿，磁通线从中穿过。外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)越强，这些涡旋就越密集地堆积在一起。实际上，材料内部的平均[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)$B$就是涡旋密度乘以磁通量量子。这在宏观尺度上提供了[磁通量量子化](@keyword=quantized_flux|lang=zh-CN|style=Feynman)的直接、可视化的体现。

[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子与材料性质之间的这种联系甚至更为深刻。[上临界场](@keyword=upper_critical_field|lang=zh-CN|style=Feynman)$B_{c2}$是涡旋变得如此密集以至于它们的正常态核心重叠，从而完全破坏超导性的点。[超导理论](@keyword=superconductivity_theory|lang=zh-CN|style=Feynman)的一大成就是，我们可以用一个优美而简单的论证来估算这个基本[材料属性](@keyword=material_properties|lang=zh-CN|style=Feynman)。当与电子在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中运动相关的特征量子面积变得与超导态的基本面积（一个半径为相干长度$\xi$的圆）相当时，超导性就会消失。这个简单的物理论证直接导出了$B_{c2}$与$\Phi_0 / \xi^2$成正比的结论 [@problem_id:1121923]。源于电子对量子力学的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子，决定了一种材料超导寿命的最终极限。

### 一个通用的量子标尺

尽管我们一直在谈论[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，但至关重要的是要记住磁通量量子来自何处：$\Phi_0 = h/q$。我们一直使用的值$\Phi_0 = h/(2e)$是[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)特有的，因为其载流子库珀对的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为$q=2e$。这提出了一个引人入胜的问题：如果载流子不同会怎样？

答案揭示了[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子是一种通用的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)探针。考虑量子霍尔效应，这是在[二维电子气](@keyword=2d_electron_gas|lang=zh-CN|style=Feynman)（2DEG）中观察到的另一个壮观的[宏观量子现象](@keyword=macroscopic_quantum_phenomena|lang=zh-CN|style=Feynman)。在这里，载流子是单个电子，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为$q=e$。确实，该系统中的自然磁通单位是$\Phi = h/e$，这个值是超导磁通量量子的两倍 [@problem_id:1820493]。事实上，观察到超导磁通量量子基于$2e$的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，是支持[BCS超导理论](@keyword=bcs_theory_superconductivity|lang=zh-CN|style=Feynman)及其激进的电子配对提议的基石性实验证据之一。通过测量一个系统中的“磁通单位”，我们实际上是在以一种非常直接的方式测量其载流子的[基本电荷](@keyword=elementary_charge|lang=zh-CN|style=Feynman)。

### 设计新的量子世界：[莫尔材料](@keyword=moiré_materials|lang=zh-CN|style=Feynman)

磁通量量子的故事仍在书写之中，其最新篇章将我们带到了[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的前沿：[扭转二维材料](@keyword=twisted_2d_materials|lang=zh-CN|style=Feynman)。当两片原子级薄的材料（如[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)）以微小的扭转角堆叠在一起时，会出现一种名为[莫尔超晶格](@keyword=moiré_superlattices|lang=zh-CN|style=Feynman)的优美新周期性图案。这种人造[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的长度尺度远大于原始原子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，为电子创造了一个全新的“量子景观”以供栖居。

在这个令人兴奋的“[扭转电子学](@keyword=twistronics|lang=zh-CN|style=Feynman)”新领域中，磁通量量子已重生为一个基本的设计参数。研究人员现在通过施加[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)来研究这些系统，并提出问题：穿过单个莫尔晶胞的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)何时等于一个磁通量量子？在这个条件下，磁长度尺度与莫尔[晶格间距](@keyword=lattice_spacing|lang=zh-CN|style=Feynman)变得可公度，最有趣的物理现象便在此发生 [@problem_id:19268]。将系统调谐到每个莫尔晶胞一个[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子，已导致发现了各种奇异的[物态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)，从非常规超导到新形式的磁性。

从SQUID的核心到体材料中的涡旋[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，从对基本电荷的检验到设计新量子物质的调谐旋钮，[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子是物理学统一性与力量的深刻证明。它是来自量子世界的一个离散信息，我们已经学会了阅读、解释，并且现在用它来书写科学和技术的新篇章。