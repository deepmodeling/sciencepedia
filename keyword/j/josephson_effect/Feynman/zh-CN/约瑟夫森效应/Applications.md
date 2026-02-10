## 应用与跨学科联系

在我们穿越了隧穿[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)和[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)相位的微观世界之后，你可能会感到惊奇，但也许会有一个问题：这一切究竟有什么用？物理学的美妙真理之一是，其最深刻、最玄奥的原理常常以最惊人、最实用和最深远的方式进入我们的世界。[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)就是这方面的一个典型例子。它不仅仅是量子领域的一个奇特现象，更是一把万能钥匙，开启了测量、技术以及我们对宇宙基本统一性理解的新前沿。

### 终极发条装置：重新定义伏特

想象你有一个完美的时钟。不仅仅是好时钟，而是一个计时速率由不变的自然法则决定的时钟。现在，如果我告诉你我们可以制造这样一个小到可以放在芯片上的时钟，并且它的“滴答”声与一个电压以绝对精确的方式联系在一起，会怎么样？这正是[交流约瑟夫森效应](@keyword=ac_josephson_effect|lang=zh-CN|style=Feynman)带给我们的。

正如我们所见，在[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)两端施加一个直流电压 $V$ 会使其奏响一曲量子乐章——它会辐射出频率为 $f$ 的交流电，该频率由不可动摇的关系式 $hf = 2eV$ 给出。这意味着一个稳定的电压会产生一个完美的稳定[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)[@problem_id:1812687] [@problem_id:1785402] [@problem_id:1812730]。这仿佛大自然给了我们一个完美的齿轮箱，即约瑟夫森常数 $K_J = 2e/h$，用于将电压转换为频率。对于仅几微伏的微小电压，结就会在吉赫兹范围内嗡嗡作响，这个频率我们可以以惊人的精度进行测量和稳定。

现在，让我们反向思考。如果我们测量频率的精度远高于制造一个可靠的“标准伏特”的精度，为什么不利用频率来*定义*电压呢？这正是[计量学](@keyword=metrology|lang=zh-CN|style=Feynman)家——物理世界的总会计师们——所做的事情。通过将一束高度稳定的微波（其频率由原子钟校准）照射到约瑟夫森结上，我们可以迫使该量子系统[锁相](@keyword=phase_locking_2|lang=zh-CN|style=Feynman)。这产生的不仅仅是一个电压，而是一整列间距完美的量子化电压阶梯，称为[夏皮罗台阶](@keyword=shapiro_steps|lang=zh-CN|style=Feynman)（Shapiro steps）[@problem_id:560913]。第 $n$ 级台阶的电压就是 $V_n = n (hf/2e)$。因此，任意两个相邻台阶之间的电压差 $\Delta V = hf/2e$ 由所施加的频率和[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)固定[@problem_id:1812729]。

这是一场革命。我们用量子食谱中一个永恒不变的配方，取代了像旧化学电池标准那样的物理实物。伏特不再是需要保存在罐子里的东西；它是一种我们可以根据需求在世界任何地方创造的东西，其精度仅受我们计算[原子钟](@keyword=atomic_clocks|lang=zh-CN|style=Feynman)“滴答”次数的能力限制。

### 聆听[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的低语：[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)（[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)）

[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)的优雅之处不仅限于电压和频率。通过将两个结精巧地组合在一起，我们可以创造出一种对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)具有近乎超自然灵敏度的设备。这个设备就是[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)（Superconducting Quantum Interference Device），简称[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)。

想象一个被两个约瑟夫son结中断的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)路。一股接近这个环路的[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)电流面临一个选择：通过左边的结还是右边的结。在量子世界里，它两者都做。但它所走的路径很重要。如果一个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)穿过环路，它会给[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)带来一个微小的[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)。事实证明，两条路径之间的总相位差与穿过环路的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi$ 成正比[@problem_id:3018030]。

来自两条路径的两股[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)电流现在相遇并发生干涉。就像[双缝实验](@keyword=double_slit_experiment|lang=zh-CN|style=Feynman)中的光波一样，它们可以相长干涉，也可以相消干涉。结果是，SQUID所能承载的最大[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)，即其[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)，会随着磁通量的变化而[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。这种调制遵循一个优美简洁的[余弦定律](@keyword=law_of_cosines|lang=zh-CN|style=Feynman)：$I_c(\Phi) = 2 I_0 |\cos(\pi \Phi/\Phi_0)|$。

真正的魔力在于这种[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的周期。它不是任意一个值，而是[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman) $\Phi_0 = h/2e$——一个极其微小的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)。一个相当于小型冰箱磁铁产生磁通量十亿分之一的变化，就能使SQUID的电流从最大值摆动到零。这使得SQUID成为有史以来最灵敏的磁力计。它们是现代科学的耳朵，能够聆听宇宙中最微弱的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)低语。它们被用于绘制人脑产生的微小[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)（脑磁图），勘探地球深处的矿产，以及在前沿实验中搜寻神秘的[暗物质](@keyword=dark_matter|lang=zh-CN|style=Feynman)粒子。

### [量子相干性](@keyword=quantum_coherence|lang=zh-CN|style=Feynman)的统一性：物理学中的类似现象

人们可能认为[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)是[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中电子的专属俱乐部。但大自然喜欢押韵。该效应是一个关于量子[相位相干性](@keyword=phase_coherence|lang=zh-CN|style=Feynman)的普遍故事，其回响在最令人惊讶的地方被发现。

考虑冷却到接近绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)的液氦。它会进入一种奇异的物质状态，称为[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)，在这种状态下，它流动时没有任何粘性。如果你取两个[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)储存器，并用一个小孔——一个“弱连接”——将它们连接起来，你就创造了一个[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)。两个储存器之间的压力差（相当于电压）不会导致稳定的流动。相反，它会产生一个[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的[质量流](@keyword=mass_flow|lang=zh-CN|style=Feynman)！[@problem_id:1214926] [@problem_id:1994368] 描述[氦原子](@keyword=helium_atom|lang=zh-CN|style=Feynman)这种晃动的方程，其形式与[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中电子的方程完全相同。这种惊人的相似性揭示了其底层物理是相同的：一个具有相干相位的[宏观量子态](@keyword=macroscopic_quantum_state|lang=zh-CN|style=Feynman)。

故事在超冷原子的纯净世界中继续。物理学家现在可以将真空中的原子云冷却到纳[开尔文](@keyword=kelvin|lang=zh-CN|style=Feynman)温度，从而创造出[玻色-爱因斯坦凝聚](@keyword=bose_einstein_condensation|lang=zh-CN|style=Feynman)体（BEC），其中数百万个原子表现得像一个单一的量子实体。通过使用激光制造一个薄的势垒，他们可以将一个BEC一分为二，形成一个近乎完美的约瑟夫森结。通过用[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)控制原子间的相互作用，他们甚至可以用特殊制作的[双原子分子](@keyword=diatomic_molecules|lang=zh-CN|style=Feynman)来构建这些结[@problem_id:1274553]。这些“定制”的量子系统提供了一个干净且可调的实验平台，以前所未有的控制力来检验[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)的预测，并探索其在多体量子物理学这幅丰富织锦中的作用。

### 探测现实的结构

[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)的极高灵敏度使其不仅仅是一个工具，更是一个基础性的探针。因为[约瑟夫森频率](@keyword=josephson_frequency|lang=zh-CN|style=Feynman)与*能量*差相关联，它可以对任何能产生[势场](@keyword=potential_field|lang=zh-CN|style=Feynman)的场作出响应，包括引力和惯性。

想象一个安装在旋转转盘上的约瑟夫森结。即使没有连接电池，也可能出现[电势差](@keyword=potential_difference|lang=zh-CN|style=Feynman)。为什么？在旋转坐标系中，一个[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)（它有质量！）感受到[离心力](@keyword=centrifugal_force|lang=zh-CN|style=Feynman)，从而产生[离心势](@keyword=centrifugal_potential|lang=zh-CN|style=Feynman)。同时，地球的引力产生[引力势](@keyword=gravitational_potential|lang=zh-CN|style=Feynman)。根据结的取向，这两种效应可以叠加或相互抵消。存在一个特定的角度，引力对隧穿的[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)所做的功恰好被惯性“力”所做的功完全抵消[@problem_id:1812731]。在这个神奇的角度，净电势差为零，量子时钟停止“滴答”，交流辐射消失。一个小小的量子器件变成了一个感知引力与旋转相互作用的传感器，这是对[等效原理](@keyword=principle_of_equivalence|lang=zh-CN|style=Feynman)的一个优美微型展示。

让我们将这个想法推向其宇宙级的结论。在一个极富想象力且大胆的思想实验中，考虑一个放置在巨大白矮星表面并由局部电池供电的[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)。它将以其特征频率 $\nu_{em} = 2eV/h$ 发射辐射。但远处的观察者会看到什么呢？根据爱因斯坦的广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)，在强[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)中，时间本身流逝得更慢。时钟走得更慢，发射出的[光子](@keyword=photon|lang=zh-CN|style=Feynman)在爬出恒星的“引力井”时能量会减少。[约瑟夫森频率](@keyword=josephson_frequency|lang=zh-CN|style=Feynman)，由于其与能量的根本联系，也不例外。远处的观察者会测量到一个更低的、[引力红移](@keyword=gravitational_redshift|lang=zh-CN|style=Feynman)的频率[@problem_id:560828]。这个假设情景优美地展示了我们物理定律的一致性，将[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的量子力学与广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)所描述的宏伟、弯曲的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)舞台联系起来。原则上，约瑟夫森结成为了探测[时空结构](@keyword=spacetime_structure|lang=zh-CN|style=Feynman)本身的探针。

从在我们实验室中定义伏特，到感知大脑的低语，甚至连接到宇宙的曲率，[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)都是对物理学力量和统一性的深刻证明。它揭示了对量子世界一个小角落的深刻理解，如何能为我们提供横跨整个科学领域的工具和见解。