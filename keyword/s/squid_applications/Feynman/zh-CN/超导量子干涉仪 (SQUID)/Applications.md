## 应用与跨学科联系

我们已经探索了支配一个由一到两个“弱连接”中断的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)——我们的[超导量子干涉仪 (SQUID)](@keyword=superconducting_quantum_interference_device_(squid)|lang=zh-CN|style=Feynman)——的奇特而美丽的量子力学。在纸面上，它似乎是一个精巧、抽象的东西，一个接近绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)的寒冷世界的产物。那么，它到底有什么用呢？

事实证明，这个小小的环路不亚于一把万能钥匙，在众多领域中解开了秘密。它探测比任何其他设备都小得多的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的能力，使其从一个实验室的奇珍异物提升为一种普适的发现工具。在本章中，我们将探索这一历程，看看一个纯粹的量子现象如何提供一双新的眼睛，让我们得以窥探磁性世界，从分子中电子的微妙舞蹈到[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的前沿。

### 测量的艺术：表征磁性世界

在其核心，SQUID 是终极的磁力计。每种材料都以其自身的方式对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)做出响应，这是其电子复杂舞蹈的标志。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 让我们能够以前所未有的保真度窃听这种舞蹈。

想象一下你是一位化学家，合成了一种新分子，比如一种钴[配合物](@keyword=coordination_compound|lang=zh-CN|style=Feynman)，你想了解其[电子结构](@keyword=electronic_structure|lang=zh-CN|style=Feynman) [@problem_id:2956479]。磁性是关键。你将一小份化合物样品放入 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 磁力计中。机器轻轻地将样品移动通过一个超导拾取线圈。当来自你样品的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)穿过线圈时，它会感应出微小的电流，然后由 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 读取。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的输出是一个与你样品磁矩成正比的电压。

通过这个测量，你可以计算出一个叫做磁化率的属性，它告诉你材料对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的响应强度。但原始测量只是故事的开始。总磁化率有几个贡献部分。有一个“抗磁性”部分，是所有[核心电子](@keyword=core_level_electrons|lang=zh-CN|style=Feynman)的轨道运动引起的对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的微弱排斥。还有一个微妙的量子力学效应，称为[温度无关顺磁性](@keyword=temperature_independent_paramagnetism|lang=zh-CN|style=Feynman) (TIP)，它源于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)轻微扭曲电子轨道。你真正追求的是“[居里顺磁性](@keyword=curie_paramagnetism|lang=zh-CN|style=Feynman)”，这部分来自于你钴原子中未配对[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。这是揭示化学信息的术语。要找到它，你必须小心地减去另外两个效应，层层剥离，以揭示你分子的磁性核心。从这个校正后的值，你可以计算出“[有效磁矩](@keyword=effective_magnetic_moment|lang=zh-CN|style=Feynman)” $\mu_{\mathrm{eff}}$，这个数字直接说明了未配对电子的数量和状态。

但真正的测量是一门艺术，充满了细微差别。你微小样品的信号可能会被样品架本身的磁响应所淹没！因此，一个优秀的科学家首先会测量“空”样品架，并从主测量中减去这个背景信号。此外，当你将材料置于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中时，它会被磁化，其自身新产生的场会扭曲你正在施加的场！这个“[退磁场](@keyword=demagnetizing_field|lang=zh-CN|style=Feynman)”取决于你样品的形状；球体对场的扭曲与薄而平的薄膜不同。一个严谨的物理学家或[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)家必须考虑到这一点，通过数学方法剥离掉这个自生场，以揭示材料真实的、固有的体[磁化率](@keyword=susceptibility|lang=zh-CN|style=Feynman) $\chi$ [@problem_id:2838672]。只有在穿越了这一系列修正之后，SQUID 才能揭示其珍宝：对材料内部磁性生命的精确、定量的测量。

### 工程化量子传感器：控制的交响曲

一个“原始”的 SQUID 本身并不是一个非常实用的仪器。其输出电压是[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的周期性非线性函数。它的[动态范围](@keyword=dynamic_range|lang=zh-CN|style=Feynman)很小——远小于地球[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)就能使其“饱和”。为了将这个挑剔的量子设备变成一个坚固、耐用的主力仪器，工程师们开发了一套优美的技术，这是一曲真正的控制交响乐。

首先，SQUID 主要有两大类。射频 (RF) SQUID，带有一个[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)，结构更简单，但通常噪声更大，带宽也较小。它的工作原理是将 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 耦合到一个谐振“[槽路](@keyword=tank_circuit|lang=zh-CN|style=Feynman)”，并通过 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的磁状态如何影响谐振来读出信号。直流 (DC) [SQUID](@keyword=squid|lang=zh-CN|style=Feynman)，带有两个结，结构更复杂，但性能更优。一个关键的工程选择是决定为特定任务使用哪种架构，在带宽、噪声和[动态范围](@keyword=dynamic_range|lang=zh-CN|style=Feynman)等[性能指标](@keyword=performance_index|lang=zh-CN|style=Feynman)之间进行权衡 [@problem_id:2862949] [@problem_id:2862974]。

驯服 SQUID 的真正魔力是一个所有现代工程的核心概念：[反馈回路](@keyword=feedback_loop|lang=zh-CN|style=Feynman)。大多数高性能 SQUID 系统在所谓的“[磁通锁定环](@keyword=flux_locked_loop|lang=zh-CN|style=Feynman)”(FLL) 中运行。这个想法简单而深刻。你不是简单地读取 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的输出电压，而是利用该电压生成一个反馈电流。这个电流通过一个线圈，产生一个与你试图测量的输入磁通量完全相反的磁通量。电子设备不知疲倦地工作，以将通过 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的总[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)保持为零，将其“锁定”在一个恒定的[工作点](@keyword=operating_point|lang=zh-CN|style=Feynman)上。

那你测量的是什么呢？你测量的是反馈电流！这个电流现在与输入磁通量成完美的正比关系。这个方案有两个巨大的优势。首先，它[线性化](@keyword=linearization|lang=zh-CN|style=Feynman)了 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的响应。其次，它将动态范围扩大了数千甚至数百万倍。SQUID 本身始终看到零[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)，而[反馈系统](@keyword=feedback_systems|lang=zh-CN|style=Feynman)则愉快地跟踪从无穷小到相对较大的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) [@problem_id:2862974]。

但是，这首电子交响乐也有其自身的复杂性。连接冷端 SQUID 与室温电子设备的导线并非完美；它们有[电感](@keyword=inductance|lang=zh-CN|style=Feynman) $L_{\ell}$ 和电容 $C_{\ell}$。这些杂散元件形成了一个谐振 RLC 电路，会给信号着色，更关键的是，如果反馈增益过高，可能导致整个[反馈回路](@keyword=feedback_loop|lang=zh-CN|style=Feynman)变得不稳定并剧烈[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。工程师必须仔细分析系统的稳定性，通常使用控制理论中的工具，如 Routh-Hurwitz 判据，来找到[最大稳定增益](@keyword=maximum_stable_gain|lang=zh-CN|style=Feynman) $K_{i,\mathrm{crit}}$，确保量子传感器及其经典电子设备和谐共处 [@problem_id:3017997]。

最后，是什么限制了最终的灵敏度？最好的直流 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 并非受其电子设备的限制，而是受基本物理学的限制。SQUID 能听到的最轻微低语的最终“噪声基底”，是由其自身分流电阻中电子的随机热扰动（约翰逊-奈奎斯特噪声）设定的。这种噪声的能量与温度 $T$ 成正比。一个有用的[品质因数](@keyword=q_factor_2|lang=zh-CN|style=Feynman)，[能量分辨率](@keyword=energy_resolution|lang=zh-CN|style=Feynman) $\varepsilon$，与此温度成正比。相比之下，射频 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 通常受其放大器噪声的限制，该放大器具有高得多的有效“[噪声温度](@keyword=noise_temperature|lang=zh-CN|style=Feynman)” $T_n$。因为 $T_n$ 几乎总是远大于液氦浴的物理温度 $T$，所以直流 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 可以实现根本上更好的[能量分辨率](@keyword=energy_resolution|lang=zh-CN|style=Feynman) [@problem_id:3017994]。这是一个美丽的例证，说明了[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)如何设定了测量的最终极限。

### 驯服噪声：探寻真实信号

要欣赏 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的强大，就要理解在一个极其“嘈杂”的世界中测量极小事物的巨大挑战。我们的星球充满了波动的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)——从 50 或 60 赫兹的电线嗡嗡声和电梯马达的轰鸣声，到地球自身[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的缓慢漂移。这种环境噪声可能比你试图探测的信号大数百万倍。你如何能在飓风中听到一根针掉落的声音呢？

这就是一些最巧妙的实验技术发挥作用的地方，这是一套驯服噪声的工具包 [@problem_id:2498055]。

首先，你可以建造一个安静的房间。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 被放置在低温恒温器中，然后置于多层高[磁导率](@keyword=magnetic_permeability|lang=zh-CN|style=Feynman)材料（如 μ-金属）和通常是超导屏蔽（如铅或铌罐）内部。这些屏蔽层就像一座堡垒，将外部磁通线绕过敏感的探测器。

其次，你可以使用一个巧妙的几何技巧。与其使用单一的拾取环路（它对来自远处的均匀场非常敏感），不如构建一个“梯度计”。一阶梯度计由两个完全相同但反向缠绕的环路组成。一个均匀的背景场会在每个环路中感应出大小相等、方向相反的电流，净信号为零。然而，一个附近的源将在一个环路中产生比另一个稍强的场，从而产生一个非零信号。因此，梯度计对远处的噪声是“盲”的，但对感兴趣的局部信号是敏感的。这相当于使用两个麦克风来消除背景噪音并专注于附近的说话者。

最后，还有 SQUID 自身的内部魔鬼。在低频下，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 存在所谓的“$1/f$ 噪声”或“[闪烁噪声](@keyword=flicker_noise|lang=zh-CN|style=Feynman)”——一种神秘的噪声源，其功率随着频率的降低而增加。它源于约瑟夫森结中的缺陷导致其[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)波动，或是微小的磁通涡旋被困在超导薄膜中并四处跳跃。为了克服这个问题，工程师们使用调制技术。其思想是把你非常慢（直流或低频）的信号“斩波”或编码到一个高频，在那个频率上 SQUID 的 $1/f$ 噪声已经消失。一种方法是“磁通[调制](@keyword=modulation|lang=zh-CN|style=Feynman)”，即加入一个小的、快速的交流磁通，并用[锁相放大器](@keyword=lock_in_amplifier|lang=zh-CN|style=Feynman)检测信号。另一种是“[偏置电流](@keyword=bias_current|lang=zh-CN|style=Feynman)反转”，即快速地将直流偏置电流从正切换到负，这有助于抵消某些类型的缓慢漂移。这就像通过吹高音哨来避开城市交通的低频轰鸣。正是通过结合所有这些策略——屏蔽、梯度计和调制——[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 惊人的内在灵敏度才能在真实的实验中得以实现。

### 新前沿：从内部空间到量子空间

凭借这种极致的灵敏度和一套抗噪声技术，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 已经挺进到新的前沿，让我们能以前所未有的方式看待世界。

旅程始于设备本身。SQUID 的核心是约瑟夫森结，这是[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)和纳米技术的奇迹。最可靠的结是通过沉积一层超纯的铌、然后是一层极薄的铝（仅几纳米厚）、再然后是更多的铌制成的“三层膜”。然后将铝层暴露在受控剂量的氧气中，形成一个近乎完美、无针孔的氧化铝 (AlO$_x$) 绝缘势垒，厚度仅为几个原子。这个势垒的质量——它的电阻和均匀性——决定了 SQUID 的性能。在整个晶片上以一致的特性制造这些器件，需要对材料纯度、沉积速率和氧化条件进行巨大的控制，因为即使氧化剂量的微小变化也会显著改变结的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman) [@problem_id:2862919]。

一旦建成，这些微小的 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 可以安装在尖锐探针的顶端，并在表面上扫描，从而创建一台“扫描 SQUID 显微镜”。这就像有一根磁性“手指”，可以感知表面的磁性景观，绘制出磁畴的杂散场，跟踪流过[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)芯片的电流，甚至成像单个被俘获的磁通量子。但这也是一个多学科的挑战。显微镜容易受到[机械振动](@keyword=mechanical_vibrations|lang=zh-CN|style=Feynman)的影响，这会导致探针高度波动。由于来自小源的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)随距离的增加而急剧衰减，即使是纳米级的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)也会产生巨大的噪声信号。为了应对这个问题，工程师构建了另一个[反馈回路](@keyword=feedback_loop|lang=zh-CN|style=Feynman)：一个电容传感器测量探针高度，一个[压电致动器](@keyword=piezoelectric_actuators|lang=zh-CN|style=Feynman)实时调整它，[主动抑制](@keyword=active_repression|lang=zh-CN|style=Feynman)[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)并保持高度恒定。这需要一个[最优控制](@keyword=optimal_control|lang=zh-CN|style=Feynman)策略，在抑制实际[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)与注入来自高度传感器的噪声之间取得平衡 [@problem_id:3018088]。

然而，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 最深远的应用或许是当它被用来探测它所源自的量子世界时。在寻求拓扑量子计算机的过程中，物理学家们正在探索称为“[马约拉纳模](@keyword=majorana_modes|lang=zh-CN|style=Feynman) (Majorana modes)”的[奇特物质](@keyword=exotic_matter|lang=zh-CN|style=Feynman)状态。这些是奇特的、幽灵般的粒子，它们是自身的[反粒子](@keyword=antiparticles|lang=zh-CN|style=Feynman)。最近的一项理论发现是，在一个周期驱动的系统中，它们可以作为具有不同对称性的“弗洛凯[马约拉纳模](@keyword=majorana_modes|lang=zh-CN|style=Feynman) (Floquet Majorana modes)”存在。一种类型，“$0$ 模”，在半周期[时间平移](@keyword=time_shifting_2|lang=zh-CN|style=Feynman)下是对称的，而另一种，“$\pi$ 模”，则会改变符号。但是人们如何才能“看到”这种抽象的对称性呢？

[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 提供了答案。通过构建一个包含两个这种特殊结的 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 环路，就为这些奇特状态创建了一个干涉仪。通过控制施加到每个结上的[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)的相对相位，可以改变它们的量子贡献如何对[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)进行干涉。对于 $\pi$ 的特定[相对相位](@keyword=relative_phase|lang=zh-CN|style=Feynman)，来自两个 $\pi$ 模的电流将[相消干涉](@keyword=destructive_interference|lang=zh-CN|style=Feynman)并完全抵消，而来自两个 $0$ 模的电流将相长干涉并加倍。这提供了一个明确无误的、“确凿的”证据 [@problem_id:3003985]。在这里，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 不再只是一个测量经典场的被动传感器；它已经成为一个旨在测试量子物质基本对称性的实验中的一个复杂、主动的组件。

从化学家的工具到系统工程的基石，再到探索量子现实结构的探针，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 是科学力量与统一性的证明。它是量子力学的孩子，长大后成为其最强大的探索者之一，为我们打开了一扇观察无形世界的新奇窗口。