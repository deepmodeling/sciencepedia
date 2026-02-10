## 应用与跨学科联系

在前一章中，我们探讨了[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)背后优美的量子力学，即两个[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)结两端的电压会产生一个频率极其精确的交流电。我们发现这个关系非常简单：一个库珀对穿过电压 $V$ 获得的能量 $2eV$ 转化为一个发射[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量 $hf$。这就得到了著名的[约瑟夫森频率](@keyword=josephson_frequency|lang=zh-CN|style=Feynman) $f_J = \frac{2e}{h}V$。

现在，你可能会认为这只是一个相当深奥的物理学知识，一个局限于[液氦](@keyword=liquid_helium|lang=zh-CN|style=Feynman)超低温世界的奇特现象。但事实远非如此。这个简单的方程是一扇门，将量子领域与众多领域联系起来。它已成为工程师的得力工具，基础理论的试验场，以及贯穿整个物理学的深刻类比的源泉。让我们踏上旅程，看看这个简单的想法[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)我们走向何方。

### 终极标尺：[量子计量学](@keyword=quantum_metrology|lang=zh-CN|style=Feynman)

第一个也是最直接的应用是在测量的科学本身——[计量学](@keyword=metrology|lang=zh-CN|style=Feynman)中。我们如何知道“一伏特”是多少？很长一段时间里，这个定义基于化学电池，而化学电池容易受到漂移和环境变化的影响。[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)改变了一切。方程 $f_J = \frac{2e}{h}V$ 只包含电压 $V$、频率 $f_J$ 和两个自然[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)：电子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $e$ 和普朗克常数 $h$。据我们所知，这些常数在任何地方、任何时间都是相同的。

这给了我们两个极其强大的工具。首先，如果我们能施加一个非常稳定的直流电压，我们就创造了一个近乎完美的频率源。例如，要产生任何[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的微波频率，只需施加一个相应微小且稳定的直流电压，通常在微伏或毫伏量级 [@problem_id:1812687]。这将结变成一个“量子广播电台”，其广播频率仅由[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)决定。

但真正的革命来自于逆向思考这个问题。如果我们用已知稳定频率的微波*照射*结会怎样？一件奇妙的事情发生了：结内部[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)可以将其相位锁定到外部辐射上。当这种情况发生时，结的电流-电压曲线上会出现一系列完全平坦的恒压台阶。这些被称为[夏皮罗台阶](@keyword=shapiro_steps|lang=zh-CN|style=Feynman)。这些台阶的电压是量子化的，只出现在 $V_n = n \frac{h}{2e} f$ 的值上，其中 $f$ 是外部微波的频率，$n$ 是一个整数 [@problem_id:560913]。

想一想这意味着什么。任意两个相邻台阶之间的电压差恰好是 $\Delta V = \frac{hf}{2e}$ [@problem_id:1812682]。由于我们可以使用[原子钟](@keyword=atomic_clocks|lang=zh-CN|style=Feynman)以极高的精度测量频率，我们现在可以根据对这些台阶的计数来定义伏特。这就是现代约瑟夫森[电压标准](@keyword=voltage_standard|lang=zh-CN|style=Feynman)的基础。我们已将宏观的电气标准与量子力学坚如磐石的基础联系起来。它是一把由基本常数锻造的、具有完美普适精度的标尺。

### 普适的和谐：其他量子系统中的[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)

物理学最美妙的方面之一，是相同的基本思想在完全不同的背景下重现。[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)就是一个典型的例子。其核心并非关于超导性或电学；而是关于两个弱耦合[宏观量子态](@keyword=macroscopic_quantum_state|lang=zh-CN|style=Feynman)之间的量子力学[相位相干性](@keyword=phase_coherence|lang=zh-CN|style=Feynman)。

例如，考虑两个被置于双阱势中的[玻色-爱因斯坦凝聚](@keyword=bose_einstein_condensation|lang=zh-CN|style=Feynman)体（BECs）——它们是已经全部塌缩到单一[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的超冷原子云。如果我们在两个阱之间制造一个化学势差 $\Delta\mu$（相当于电学中的电压），原子不会简单地从高[势流](@keyword=potential_flow|lang=zh-CN|style=Feynman)向低势。相反，它们会在两个阱之间来回“晃荡”，呈现出[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)行为。这种原子流的频率由一个惊人熟悉的关系给出：$\omega = \frac{\Delta\mu}{\hbar}$。这是[交流约瑟夫森效应](@keyword=ac_josephson_effect|lang=zh-CN|style=Feynman)的直接类比，其中库珀对的能量 $2eV$ 被原子势能差 $\Delta\mu$ 所取代 [@problem_id:1252161]。

即使没有外加势，这些系统也表现出类约瑟夫森动力学。原子间的相互作用，加上阱间的[量子隧穿](@keyword=quantum_mechanical_tunneling|lang=zh-CN|style=Feynman)，可以导致两侧粒子数不平衡的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。这些“内部”约瑟夫森[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)是耦合系统的基本属性，其频率由[相互作用强度](@keyword=interaction_strength|lang=zh-CN|style=Feynman)和隧穿速率决定 [@problem_id:974699]。这种现象不仅限于原子；在[激子-极化激元](@keyword=exciton_polaritons|lang=zh-CN|style=Feynman)（一种半光半物质的奇异[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)）的凝聚体中也已观察到 [@problem_id:1180983]。看来，不同的量子乐团演奏着同一首乐曲。

### 来自前沿的回响：探测奇异物理

由于[约瑟夫森频率](@keyword=josephson_frequency|lang=zh-CN|style=Feynman)对载流子的基本性质如此敏感，它可以被用作探索新的奇异物质态的工具。标准效应源于携带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $2e$ 的[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的隧穿。但如果隧穿的是其他东西呢？

这个问题是寻找[马约拉纳费米子](@keyword=majorana_fermions|lang=zh-CN|style=Feynman)的核心，这是一种神秘的、自身即是其反粒子的粒子。理论预测，这些粒子可以存在于“[拓扑超导体](@keyword=topological_superconductors|lang=zh-CN|style=Feynman)”的末端。如果用两种这样的材料构建一个[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)，低能电流将不再由库珀对承载，而是由一个[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)从一个马约拉纳态到另一个的“传送”过程承载。这个过程转移一个单一的基本电荷，$e$。

其结果是一个戏剧性且明确无误的特征：[电流-相位关系](@keyword=current_phase_relation|lang=zh-CN|style=Feynman)将具有 $4\pi$ 的周期性，而不是通常的 $2\pi$，并且在电压 $V$ 下产生的交流[约瑟夫森频率](@keyword=josephson_frequency|lang=zh-CN|style=Feynman)将是 $\omega = \frac{eV}{\hbar}$。这恰好是标准[约瑟夫森频率](@keyword=josephson_frequency|lang=zh-CN|style=Feynman)的*一半* [@problem_id:1158055]。找到这种“[分数约瑟夫森效应](@keyword=fractional_josephson_effect|lang=zh-CN|style=Feynman)”将是马约拉纳费米子存在的铁证，为新型[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)打开大门。从某种意义上说，我们正在聆听量子和谐中的一个不同音符，一个预示着一种全新粒子存在的音符。

### 量子时钟、[时空](@keyword=space_time|lang=zh-CN|style=Feynman)与引力

到目前为止，我们方程中的“电压”都是电学的。但其基本原理是关于能量。任何能在结两端产生能量差的势，原则上都可以驱动约瑟夫森[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)不仅有[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，还有质量。这开启了与力学甚至广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)世界的惊人联系。

想象一个垂直放置在[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)中的[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)。顶部的[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)比底部的库珀对具有稍高的引力势能。这个微小的能量差 $\Delta E = (2m_e) g d$ 充当一个等效电压，产生交流[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)。在旋转坐标系中也是如此，离心力会产生一个势差。原则上，[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)可以作为一种极其灵敏的引力和旋转探测器，其频率可以告诉你局部的等效[引力势](@keyword=gravitational_potential|lang=zh-CN|style=Feynman) [@problem_id:1812731]。

让我们将这个想法推向极致。考虑一个思想实验，将一个约瑟夫森结放置在一个像[白矮星](@keyword=white_dwarfs|lang=zh-CN|style=Feynman)这样的大质量物体表面，并维持一个恒定的局部电压 $V$。该结将忠实地以局部频率 $\nu_{em} = 2eV/h$ 发射辐射。然而，为了让这些辐射到达远处的观察者，它必须爬出恒星巨大的引力势阱。正如爱因斯坦的广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)所预测的那样，辐射在此过程中会损失能量，其频率会降低——它会发生[引力红移](@keyword=gravitational_redshift|lang=zh-CN|style=Feynman)。远处的宇航员会测量到一个频率 $\nu_{obs} = \nu_{em} \sqrt{1 - 2GM/Rc^2}$ [@problem_id:560828]。在这里，我们看到了量子力学定律（[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)）和广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)（[引力红移](@keyword=gravitational_redshift|lang=zh-CN|style=Feynman)）在完美和谐中协同工作。

与机械能的联系是深刻的。约瑟夫森结辐射的能量不必以电磁波的形式逸出。它也可以直接耦合到其所在的材料[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中，产生具有精确可预测能量和动量的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)——[声子](@keyword=phonons|lang=zh-CN|style=Feynman) [@problem_id:182840]。

从在我们的实验室中定义伏特，到探测奇异粒子的存在，再到阐释[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的曲率，[约瑟夫森频率](@keyword=josephson_frequency|lang=zh-CN|style=Feynman)远不止一个公式。它是一条将物理学中一些最深刻的思想编织在一起的线索，是自然世界深刻、内在统一性的证明。