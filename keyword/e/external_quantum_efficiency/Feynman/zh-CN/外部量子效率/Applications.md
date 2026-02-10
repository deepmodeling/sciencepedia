## 应用与跨学科联系

在阐明了外部量子效率 (EQE) 背后的原理之后，我们现在可以踏上一段旅程，看看这个优雅的概念将我们引向何方。EQE 远非仅仅是学术上的好奇心，它是连接基础物理学与塑造我们世界的众多惊人技术的关键。无论我们是在捕获太阳能、照亮我们的城市，还是窥探物质本身的微妙缺陷，它都充当着量化光与电之间对话的通用语言。

### 光传感与能量转换的核心

在其最基础的层面上，EQE 关乎[光子计数](@keyword=photon_counting|lang=zh-CN|style=Feynman)。想象一个数码相机传感器或[光纤](@keyword=fiber_optics|lang=zh-CN|style=Feynman)网络中的接收器。它的工作是将入射的光子流转换为可测量的电信号。它做得有多好？EQE 直接给出了答案。对于每一百个到达的光子，0.85 的 EQE 意味着成功产生并收集了八十五个电子。工程师们经常使用一个相关的度量标准，称为[响应度](@keyword=responsivity|lang=zh-CN|style=Feynman)，单位是安培/瓦特，它告诉他们在给定的[光功率](@keyword=optical_power|lang=zh-CN|style=Feynman)下产生的电流。这两个量密切相关；如果光的波长已知，一个可以从另一个计算出来，为表征任何光电探测器提供了一种实用的方法[@problem_id:1795727]。

现在，让我们将雄心从简单地探测光扩大到收集其能量。这就把我们带到了太阳能发电的巨大挑战面前。[太阳能电池](@keyword=solar_cell|lang=zh-CN|style=Feynman)本质上是一个为发电而优化的巨型[光电探测器](@keyword=photodetector|lang=zh-CN|style=Feynman)。然而，太阳发出的光并非单一波长；它提供了一个广泛的颜色光谱。[太阳能电池](@keyword=solar_cell|lang=zh-CN|style=Feynman)的 EQE 不是一个单一的数字，而是一个函数，一条描述其在每个特定波长下效率的曲线。为了预测[太阳能电池](@keyword=solar_cell|lang=zh-CN|style=Feynman)将产生的总电流，我们必须同时考虑太阳光谱——太阳提供了多少每种颜色的光子——和电池的 EQE 光谱。

为了公平比较，科学家们建立了一个标准的“人造太阳”，称为 AM1.5G (Air Mass 1.5 Global) 光谱。该标准代表了地球中纬度地区表面接收到的平均太阳光，考虑了直射光和散射漫射光。短路电流密度 ($J_{sc}$)，一个衡量[电池性能](@keyword=battery_performance|lang=zh-CN|style=Feynman)的关键指标，是通过将 EQE 光谱与 AM1G [光子通量](@keyword=photon_flux|lang=zh-CN|style=Feynman)光谱的乘积在所有波长上积分得到的。这是一个优美而强大的计算：在每个波长处，你将可用光子的数量乘以电池转换它们的概率，然后将所有贡献相加，得到总电流[@problem id:2850620]。

### 硬币的另一面：从电到光

物理学钟爱对称性。如果一个过程可以朝一个方向运行，它通常也可以反向运行。一个理想的[太阳能电池](@keyword=solar_cell|lang=zh-CN|style=Feynman)，擅长将光子转换为电子-空穴对，当这些对由外部电压提供时，也应该是一个高效的发光体。这就是发光二极管 (LED) 背后的原理。

在 LED 或有机 LED ([OLED](@keyword=oleds|lang=zh-CN|style=Feynman)) 中，角色是颠倒的。我们向器件注入电子，并想知道有多少光子出来。在这里，EQE 也是关键的品质因数，现在定义为发射的光子数与注入的电子数之比。高 EQE 是实现高效光源的第一步。总体的[功率转换效率](@keyword=power_conversion_efficiency|lang=zh-CN|style=Feynman)——输出[光功率](@keyword=optical_power|lang=zh-CN|style=Feynman)与输入[电功率](@keyword=electrical_power|lang=zh-CN|style=Feynman)之比——不仅取决于产生了多少光子（EQE），还取决于每个光子的能量相对于产生它的每个电子的能量。这种关系可以优雅地表达出来，将功率效率直接与 EQE、工作电压 $V$ 和[峰值发射波长](@keyword=peak_emission_wavelength|lang=zh-CN|style=Feynman) $\lambda_{peak}$ 联系起来[@problem_id:39465]。这种吸收与发射之间的互易性是一个深刻且反复出现的主题，我们将会再次遇到。

### 工程完美：挑战效率极限

EQE 并非材料固定不变的属性；它是一个可以通过精湛的工程技术进行调控的参数。科学家和工程师已经开发出巧妙的策略，通过操纵光和物质来提高 EQE。

一个主要挑战是确保每一个可能的光子都被吸收。较厚的吸收层会捕捉更多的光，但产生的电荷载流子在丢失之前到达触点的难度会增加。一个聪明的解决方案是将光困在器件内部。[谐振腔](@keyword=resonant_cavity|lang=zh-CN|style=Feynman)增强 (RCE) 型光电探测器正是通过将薄吸收层置于两面镜子之间，形成一个[光学腔](@keyword=optical_cavity|lang=zh-CN|style=Feynman)体来实现这一点。特定波长的光在镜子之间来回反弹，多次穿过吸收层。这种“镜厅”效应极大地增加了[吸收概率](@keyword=absorption_probability|lang=zh-CN|style=Feynman)，即使吸收层比传统设计薄十倍，也能在目标波长实现近乎 единицa 的 EQE [@problem_id:1795734]。

对于 LED 而言，问题通常是相反的：如何让产生的光*离开*器件。在高折射率半导体内部产生的光子，当它撞击到与低[折射](@keyword=refraction|lang=zh-CN|style=Feynman)率空气的界面时，可能会被[全内反射](@keyword=total_internal_reflection_(tir)|lang=zh-CN|style=Feynman) (TIR) 困住。对于以陡峭角度撞击此边界的光子来说，该表面就像一面完美的镜子，将其反射回内部。这种效应可以困住超过一半的光。一个优雅的解决方案是在器件表面添加一个半球形圆顶或散射膜。通过使用具有中等折射率的材料，这些结构改变了光与最终[界面相](@keyword=interfacial_complexions|lang=zh-CN|style=Feynman)遇的角度，扩大了光子的“逃逸锥”，并显著提高了[光提取效率](@keyword=light_extraction_efficiency|lang=zh-CN|style=Feynman)，从而直接提高了器件的整体 EQE [@problem_id:2504532]。

### 先进架构与奇异物理学

随着我们对[光电子学](@keyword=optoelectronics|lang=zh-CN|style=Feynman)掌握程度的提高，我们开始涉足更复杂、更强大的器件设计，其中 EQE 扮演着更为微妙的角色。

为了克服单材料[太阳能电池](@keyword=solar_cell|lang=zh-CN|style=Feynman)的理论效率极限，科学家们将具有不同[带隙](@keyword=band_gap|lang=zh-CN|style=Feynman)的多个电池以串联或多结结构堆叠起来。具有宽带隙的顶部电池吸收高能（蓝色）光，而具有窄[带隙](@keyword=band_gap|lang=zh-CN|style=Feynman)的底部电池吸收穿过的低能（红色）光。如果这些电池串联连接，它们就像链条中的环节。根据基尔霍夫定律，相同的电流必须流过每个环节。这意味着串联器件的总电流受到产生*最少*电流量的子电池的限制。中心设计挑战，即“电流匹配”，是仔细选择材料和厚度，使得每个子电池在太阳光谱下产生相同的[光电流](@keyword=photocurrent|lang=zh-CN|style=Feynman)。因此，理解每个子电池的在叠层中的 EQE 对于预测和优化这些创纪录器件的性能至关重要[@problem_id:2510066]。

但如果我们能打破基本的“一个光子，一个电子”规则呢？在某些有机材料中，会发生一种称为[单线态](@keyword=singlet_state|lang=zh-CN|style=Feynman)裂分的非凡量子力学过程。一个高能光子被吸收，产生一个激发态（一个[单线态](@keyword=singlet_state|lang=zh-CN|style=Feynman)[激子](@keyword=excitons|lang=zh-CN|style=Feynman)）。如果条件合适，这个[单线态](@keyword=singlet_state|lang=zh-CN|style=Feynman)可以自发地分裂成*两个*低能量的三线态激子。如果这两个三线态都能被收集以产生[自由电荷](@keyword=free_charge|lang=zh-CN|style=Feynman)，那么一个光子就可以产生两个电子，从而在该光谱区域内有效地使 EQE 加倍。这个过程为绕过传统效率极限提供了一条诱人的途径。总体的 EQE 增强取决于[单线态](@keyword=singlet_state|lang=zh-CN|style=Feynman)裂分速率、不同激子种类向界面的扩散以及它们最终解离为电荷之间的复杂竞争，所有这些都可以通过建模来预测潜在的增益[@problem_id:211722]。

### EQE 作为窥探量子世界的窗口

也许 EQE 最深刻的应用不是作为器件的性能指标，而是作为探测物质基本属性的诊断工具。

即使是最完美的晶体也有缺陷。这种结构和热无序会在材料的禁带中产生一个微弱的允许电子态“尾巴”。这些“Urbach 边”允许材料吸收能量略低于[带隙](@keyword=band_gap|lang=zh-CN|style=Feynman)的光子。通过测量这个亚[带隙](@keyword=band_gap|lang=zh-CN|style=Feynman)区域的 EQE——通常在百万分之一或更低的水平上——我们可以表征这个尾巴。EQE 光谱遵循一个独特的指数衰减，在[半对数图](@keyword=semi_log_plot|lang=zh-CN|style=Feynman)上这个衰减的斜率给出了 Urbach 能量 ($E_U$)，这是材料无序度的直接量度。此外，[带隙](@keyword=band_gap|lang=zh-CN|style=Feynman)深处一个平坦、变化微弱的 EQE 信号可以揭示更严重的[带隙](@keyword=band_gap|lang=zh-CN|style=Feynman)中缺陷态的存在和密度。通过这种方式，EQE 测量成为一种强大的、非破坏性的显微镜，用于观察半导体内部的电子景观[@problem_id:2510069]。

这种诊断能力在吸收与发射之间的深刻联系中达到了顶峰，这种联系植根于热力学原理。Kirchhoff 在 19 世纪提出的热辐射定律指出，在给定温度下，好的吸收体也是好的发射体。这种细致平衡原则在[光电子学](@keyword=optoelectronics|lang=zh-CN|style=Feynman)中找到了一个惊人的现代类比。可以证明，[太阳能电池](@keyword=solar_cell|lang=zh-CN|style=Feynman)在正向偏压下发出的光谱（电致发光）由其 EQE 光谱、温度和施加的电压直接决定。这两种现象，吸收和发射，是同一枚硬币的两面，通过[热力学](@keyword=thermo_mechanics|lang=zh-CN|style=Feynman)互易性紧密相连。了解一个器件的 EQE，就可以以惊人的准确性预测它将发出的光[@problem_id:163153]。

最后，在最反直觉和最美妙的应用之一中，EQE 是固体[激光冷却](@keyword=laser_cooling|lang=zh-CN|style=Feynman)概念的核心。通过用特定能量的光子泵浦一个物体，并设计它发射更高[平均能量](@keyword=average_energy|lang=zh-CN|style=Feynman)的光子（一个称为反斯托克斯荧光的过程），可以用光来冷却这个物体。额外的能量是从材料的热振动（声子）中窃取的，导致其冷却。然而，这个冷却过程必须与[非辐射衰变](@keyword=non_radiative_decay|lang=zh-CN|style=Feynman)产生的热量竞争。胜负由 EQE 决定。要实现净冷却，外部[量子效率](@keyword=quantum_efficiency|lang=zh-CN|style=Feynman)必须超过一个由平均荧光波长与泵浦波长之比定义的临界阈值，即 $\eta_{ext} > \bar{\lambda}_f / \lambda_p$。这将这个谦逊的“光子输出/光子输入”比率置于[量子热](@keyword=quantum_heat|lang=zh-CN|style=Feynman)管理的核心，恰如其分地证明了外部[量子效率](@keyword=quantum_efficiency|lang=zh-CN|style=Feynman)概念深远的力量和优雅[@problem_id:1335503]。