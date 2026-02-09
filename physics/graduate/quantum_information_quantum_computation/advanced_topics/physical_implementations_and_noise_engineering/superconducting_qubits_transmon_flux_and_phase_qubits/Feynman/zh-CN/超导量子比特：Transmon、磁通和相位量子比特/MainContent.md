## 引言

[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)是当前最有前景的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)实现方案之一，它利用[集成电路](@keyword=integrated_circuits|lang=zh-CN|style=Feynman)技术的可扩展性和设计灵活性，为解决[经典计算](@keyword=classical_computation|lang=zh-CN|style=Feynman)机无法企及的复杂问题带来了希望。然而，从一个抽象的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)概念到一个真正可操作的物理器件，其间横亘着巨大的挑战。要驾驭这些“人造原子”的强大能力，我们必须深入理解其背后精妙而脆弱的量子物理规律——从它们如何在接近绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)的芯片上“诞生”，到如何被精确操控，再到它们为何会因与环境的无情互动而最终“消亡”。本文旨在为读者搭建一座沟通理论与实践的桥梁，系统地解析[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)的世界。

在第一章“原理与机制”中，我们将像钟表匠一样，拆解[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的核心，探究如何从一个经典电路中锻造出量子双能级系统，理解约瑟夫森结如何赋予其“量子灵魂”，并直面退相干这一无处不在的敌人。随后的第二章“应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系”，我们将视野从单个比特扩展到整个系统，学习如何编排[量子门](@keyword=quantum_computing_gates|lang=zh-CN|style=Feynman)操作以执行[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，分析各种误差的来源，并探索超导电路作为量子模拟器和传感器的广阔应用前景，揭示其与凝聚态物理、[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)等领域的深刻联系。最后，通过一系列“动手实践”练习，您将有机会亲手应用所学知识，解决具体的研究问题。现在，让我们启程，首先深入[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)的内部，探寻其运行的核心原理与机制。

## 原理与机制

在上一章中，我们邂逅了[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)的奇妙世界。现在，是时候卷起袖子，深入其内部，探寻其运行的核心原理与机制了。我们将像一位钟表匠拆解一枚瑞士表那样，仔细审视每一个齿轮与弹簧，只不过我们的研究对象是栖身于接近绝对零度的金属孤岛中的量子现象。我们将看到，一个[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)的诞生、操控与消亡，本质上是一曲由非线性、[相干控制](@keyword=coherent_control|lang=zh-CN|style=Feynman)与环境噪声共同谱写的交响乐。

### 从经典[振荡器](@keyword=oscillators|lang=zh-CN|style=Feynman)到[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的锻造

想象一根吉他弦。拨动它，它会以一个[基频](@keyword=fundamental_frequency|lang=zh-CN|style=Feynman)和一系列[泛音](@keyword=overtones|lang=zh-CN|style=Feynman)（也就是频率为基频整数倍的[谐波](@keyword=harmonic_waves|lang=zh-CN|style=Feynman)）[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。这是一个典型的**谐波[振荡器](@keyword=oscillators|lang=zh-CN|style=Feynman)**。在量子世界里，一个理想的[谐波](@keyword=harmonic_waves|lang=zh-CN|style=Feynman)[振荡器](@keyword=oscillators|lang=zh-CN|style=Feynman)，比如一个由普通[电感](@keyword=inductance|lang=zh-CN|style=Feynman)（$L$）和电容（$C$）组成的$LC$电路，其能级是等间距的。就像一个梯子，每一级之间的高度都完全相同。如果我们用一个特定频率的能量脉冲去激励它，它会吸收能量并跃迁到更高的能级。但问题是，由于[能级间距](@keyword=energy_level_spacing|lang=zh-CN|style=Feynman)相等，我们无法只精确地激发它从[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（第0级）到第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)（第1级），而不影响它继续跃迁到第二、第三[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)。这样的系统无法成为一个好的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，因为它无法将信息稳定地编码在两个特定的能级上。

要创造一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，我们需要打破这种单调的和谐。我们需要一个**[非谐性](@keyword=anharmonicity|lang=zh-CN|style=Feynman)[振荡器](@keyword=oscillators|lang=zh-CN|style=Feynman)**（anharmonic oscillator），它的能级阶梯不再等高，而是越往上走，梯级间的高度差会发生变化。这样，我们就可以用一个精确频率的微波脉冲，像一把钥匙配一把锁一样，专门驱动[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|0\rangle$ 和第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) $|1\rangle$ 之间的跃迁，而不会意外地“打开”通往更高能级 $|2\rangle, |3\rangle, \dots$ 的大门。

那么，这把打破和谐的“锤子”是什么呢？它就是超导电路的灵魂——**约瑟夫森结**（Josephson junction）。这个小小的、由两层[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)夹着一层薄绝缘层构成的器件，表现为一个**非线性[电感](@keyword=inductance|lang=zh-CN|style=Feynman)**。它的能量不再是电流的二次方，而是与流过它的磁通量（或者说[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman) $\hat{\varphi}$）的余弦函数成正比。一个典型的“[Transmon](@keyword=transmon|lang=zh-CN|style=Feynman)”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的哈密顿量（系统的总能量表达式）可以简洁地写为：
$$
H = 4 E_{C} \hat{n}^{2} - E_{J} \cos \hat{\varphi}
$$
其中，$E_C$ 是与电容相关的**[充电能](@keyword=charging_energy|lang=zh-CN|style=Feynman)**，代表了将一个库珀对（Cooper pair）转移到电容孤岛上所需的能量。$\hat{n}$ 则是[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)数量的算符。而 $E_J$ 则是**约瑟夫森能**，代表了[库珀对隧穿](@keyword=cooper_pair_tunneling|lang=zh-CN|style=Feynman)过结的难易程度。[@problem_id:2832144]

这个 $\cos\hat{\varphi}$ 项是关键。它创造了一个所谓的“洗衣板势”（washboard potential）。在[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)的底部，这个[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)看起来很像一个抛物线，就像一个[谐波](@keyword=harmonic_waves|lang=zh-CN|style=Feynman)[振荡器](@keyword=oscillators|lang=zh-CN|style=Feynman)。但当相位 $\hat{\varphi}$ 偏离平衡位置稍远时，势能的增长会变缓，不再是严格的二次关系。正是这种偏离，引入了我们梦寐以求的[非谐性](@keyword=anharmonicity|lang=zh-CN|style=Feynman)。通过对这个哈密顿量进行一番数学上的“近似处理”，我们可以得到从[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|0\rangle$ 跃迁到第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) $|1\rangle$ 的频率 $f_{01}$：
$$
f_{01} \approx \frac{1}{h}(\sqrt{8 E_{J} E_{C}} - E_{C})
$$
这里的 $h$ 是普朗克常数。你看到了吗？这个频率不仅仅是谐波部分 $\sqrt{8 E_{J} E_{C}}$，还减去了一个小的修正项 $E_C$。这个 $-E_C$ 就是**非谐性**的量度，它确保了 $|0\rangle \to |1\rangle$ 的跃迁频率与 $|1\rangle \to |2\rangle$ 的跃迁频率不同，从而使我们能够精确地操控这个[两能级系统](@keyword=two_level_system|lang=zh-CN|style=Feynman)，一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)就此诞生。[@problem_id:2832144] 其他类型的[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)，如**相位比特**（phase qubit）[@problem_id:139397]和**[磁通量子比特](@keyword=flux_qubit|lang=zh-CN|style=Feynman)**（flux qubit）[@problem_id:139408]，虽然设计和参数不同，但其核心都是利用[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)的非线性来创造一个可控的量子[两能级系统](@keyword=two_level_system|lang=zh-CN|style=Feynman)。

### 拨动量子的琴弦：操控与控制

拥有了一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，我们如何去“弹奏”它——也就是执行[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)操作呢？我们需要一些“控制杆”来精确地改变它的状态。

一个最强大、最常用的控制杆是**[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)**。想象一下，我们将单个的[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)换成一个由两个结[并联](@keyword=parallel_connection|lang=zh-CN|style=Feynman)组成的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)路，这就是所谓的**[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)**（[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)）。当我们将一束[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)线（[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi$）穿过这个环路时，奇妙的事情发生了。这两个结的有效总[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman) $E_{J, \mathrm{eff}}$ 会随着磁通量的变化而周期性地改变。对于一个对称的[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)，这个关系优美而简洁：
$$
E_{J, \mathrm{eff}}(\Phi) = 2E_{J0}\left|\cos\left(\frac{\pi\Phi}{\Phi_0}\right)\right|
$$
其中 $\Phi_0$ 是[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)，一个自然界的基本常数。[@problem_id:2997597] 因为[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的频率 $f_{01}$ 直接依赖于 $E_J$，这意味着我们可以通过调节外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，像调收音机旋钮一样，精确地“调谐”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的频率。这种频率的可调性是实现[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)间相互作用和执行两比特量子门的关键。

除了静态的调谐，我们还可以用更“动态”的方式来操控[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。想象一下，我们用一个频率远高于[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)自身频率的微波场去“摇晃”它。这并不一定会把[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)从[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)激发到[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)，但它会给[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)“穿上一件新衣”，改变它的内在属性。这个过程被称为**[弗洛凯工程](@keyword=floquet_engineering|lang=zh-CN|style=Feynman)**（Floquet engineering）。例如，当我们对一个[磁通量子比特](@keyword=flux_qubit|lang=zh-CN|style=Feynman)施加一个快速[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的纵向[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)时，它的有效隧穿能量 $\Delta_{eff}$ 会被“重整化”，其大小由贝塞尔函数（Bessel functions）决定：
$$
\Delta_{eff} = \Delta J_0\left(\frac{A_1}{\hbar\omega_1}\right) J_0\left(\frac{A_2}{\hbar\omega_2}\right)
$$
这里 $A_i$ 和 $\omega_i$ 是驱动场的振幅和频率。[@problem_id:139413] 令人惊叹的是，通过调节驱动的振幅，我们甚至可以让贝塞尔函数的值变为零，从而在动态中完全“关闭”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的隧穿！这为我们提供了一种高速、全电学控制[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)参数的强大手段。

### 宇宙的呢喃：无处不在的[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)

[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的世界是脆弱的。就像一个置于嘈杂房间里的音叉，它的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)会逐渐减弱并消失，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的相干性也会被周围环境无情地侵蚀。这个过程，我们称之为**[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)**（decoherence），是[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)面临的最大挑战。它主要通过两条途径发生。

#### [能量弛豫](@keyword=energy_relaxation|lang=zh-CN|style=Feynman) ($T_1$)：能量的流失

第一条途径是**[能量弛豫](@keyword=energy_relaxation|lang=zh-CN|style=Feynman)**，以时间常数 $T_1$ 来表征。处于[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) $|1\rangle$ 的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)会自发地或受激地跃迁回[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|0\rangle$，并释放出一个能量量子。这个过程就像一个微型天线在向外辐射能量。

- **[珀塞尔效应](@keyword=purcell_effect|lang=zh-CN|style=Feynman)**（Purcell effect）：[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)为了被控制和读出，必须连接到外部的微波线路。这条线路就像一个能量的“高速公路”，为[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的能量提供了一个逃逸通道。[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)可以被看作一个微小的量子天线，它会自发地将能量以微波[光子](@keyword=photon|lang=zh-CN|style=Feynman)的形式辐射到[传输线](@keyword=transmission_lines|lang=zh-CN|style=Feynman)中。其衰变速率正比于[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)与线路的耦合强度，反比于一个被称为品质因数 $Q_c$ 的量。[@problem_id:139355]
- **[热噪声](@keyword=johnson_nyquist_noise|lang=zh-CN|style=Feynman)**: 我们的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机位于一个极度寒冷的[稀释制冷机](@keyword=dilution_refrigerator|lang=zh-CN|style=Feynman)中，但制冷机的其他部分温度相对较高。这些温热部分会像一个微型“太阳”一样，发出黑体辐射。即使经过层层衰减，仍会有一些[热光](@keyword=thermal_light|lang=zh-CN|style=Feynman)子像“热子弹”一样顺着传输线传播下来，撞击[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。如果[热光](@keyword=thermal_light|lang=zh-CN|style=Feynman)子的频率恰好等于比特的跃迁频率，它将**受激**（stimulate）[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)从 $|1\rangle$ 跃迁到 $|0\rangle$，从而加速[能量弛豫](@keyword=energy_relaxation|lang=zh-CN|style=Feynman)。这就是为什么保持[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)环境的极度“寒冷”和“黑暗”至关重要。[@problem_id:139350]
- **意想不到的通道**: 能量的泄漏途径有时会出乎我们的意料。例如，许多[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)被制作在[压电材料](@keyword=piezoelectric_materials|lang=zh-CN|style=Feynman)（如蓝宝石）的衬底上。当[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)时，它周围的电场也会随之[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。在[压电材料](@keyword=piezoelectric_materials|lang=zh-CN|style=Feynman)中，这种电场[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)会耦合到[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的机械振动，产生[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)（即**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**），像[水波](@keyword=water_waves|lang=zh-CN|style=Feynman)一样带走能量。这是一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的电能转化为声能并散失掉的迷人例子。[@problem_id:139440]
- **多模环境**: [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)所处的环境也可能很复杂，比如同时耦合到多个不同频率的谐振器。在这种情况下，总的衰变速率是各个衰变通道速率的总和。每个通道的贡献大小取决于[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的频率与该通道谐振频率的接近程度，形成一个洛伦兹形状的依赖关系。[@problem_id:139357]


#### 相位退相干 ($T_2$)：相位的遗忘

第二条途径是**相位[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)**，或称**[退相](@keyword=dephasing|lang=zh-CN|style=Feynman)**，以[时间常数](@keyword=time_constant|lang=zh-CN|style=Feynman) $T_2$ 表征。在这种情况下，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)不一定损失能量，但其处于叠加态（例如 $\frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$）时， $|0\rangle$ 和 $|1\rangle$ 之间的确定相位关系会逐渐变得随机。这就像两个步伐一致的舞者，其中一个的节拍器忽快忽慢，最终他们的舞步变得不再同步。

退相的根源在于**[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)频率的随机波动**。任何能够影响比特频率的噪声源都会导致退相。

- **参数噪声**: 正如我们前面看到的，比特频率 $f_{01}$ 依赖于 $E_J$ 和 $E_C$。而 $E_J$ 又与约瑟夫森结的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman) $I_c$ 成正比。如果 $I_c$ 或外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi$ 受到无处不在的**$1/f$ 噪声**（一种低频噪声）的干扰而发生随机起伏，那么比特的频率就会随之“[抖动](@keyword=dither|lang=zh-CN|style=Feynman)”，导致相位的[随机化](@keyword=randomization|lang=zh-CN|style=Feynman)。[@problem_id:2832144] 工程师们通常会将[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的工作点设置在所谓的“甜蜜点”（sweet spot），在这些点上，比特频率对某一特定噪声源（如磁通噪声）的敏感度为一阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)零。但这往往是一个权衡，可能会增加对特其他噪声源（如[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)噪声）的敏感度。[@problem_id:139365]
- **[两能级系统](@keyword=two_level_system|lang=zh-CN|style=Feynman)缺陷 (TLS)**: 一个更阴险的噪声源潜伏在构成[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的材料本身之中。在[非晶态](@keyword=amorphous_state|lang=zh-CN|style=Feynman)的绝缘层或衬底表面，存在着原子尺度的缺陷，它们自身也表现为微小的量子**[两能级系统](@keyword=two_level_system|lang=zh-CN|style=Feynman)**（Two-Level System, TLS）。这些“野生”的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)就像一群吵闹的邻居。如果某个TLS恰好与我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)发生耦合，它就会随机地“拉扯”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的能级，使其频率发生波动。[@problem_id:139338] 更糟糕的是，如果这个TLS本身是耗散的（即它自己有很短的$T_1$时间），它还会通过耦合把这种“坏品质”传染给我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，为[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)提供一个额外的[能量弛豫](@keyword=energy_relaxation|lang=zh-CN|style=Feynman)通道。[@problem_id:139361]

### 被观测的量子之“锅”

在经典世界里，观测是被动的。你看一个月亮，月亮并不会因为你看了它一眼而改变轨道。但在量子世界，观测是一种主动的、会产生深刻影响的行为。

想象一下，我们不再用一个强脉冲去“猛击”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)以确定其状态，而是通过一个弱耦合的谐振器来**连续而微弱地“窃听”**它。我们从谐振器反射回来的信号中，随着时间的推移，一点一点地提取关于[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)状态的信息。这个过程是随机的，每次实验的测量记录都像一段独特的噪声信号。然而，通过分析这段信号，我们可以逐渐推断出[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的状态。随着我们获得的信息越来越多，我们对[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)状态的不确定性就会减小，其冯·诺伊曼熵（von Neumann entropy）就会平均地降低，[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)也因此变得越来越“纯”。[@problem_id:139390] 这揭示了量子测量的本质：一个通过与环境（测量仪器）的相互作用，逐步获取信息并减少[系统不确定性](@keyword=systematic_uncertainty|lang=zh-CN|style=Feynman)的过程。

然而，获取信息是有代价的，这个代价就是**测量反作用**（measurement back-action）。我们的“窃听”行为本身就会干扰[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。一个引人入胜的极端例子是**[量子芝诺效应](@keyword=zeno_phenomenon|lang=zh-CN|style=Feynman)**（Quantum Zeno effect）。想象一个[磁通量子比特](@keyword=flux_qubit|lang=zh-CN|style=Feynman)，其状态可以在左旋电[流态](@keyword=flow_regimes|lang=zh-CN|style=Feynman) $|L\rangle$ 和右旋电[流态](@keyword=flow_regimes|lang=zh-CN|style=Feynman) $|R\rangle$ 之间隧穿[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。如果我们以极高的频率、极强的强度去测量“比特现在处于哪个态？”，我们每次测量都会迫使比特“选择”一个确定的态（$|L\rangle$ 或 $|R\rangle$）。这种持续不断的“逼问”会有效地冻结系统的演化，极大地抑制[相干隧穿](@keyword=coherent_tunneling|lang=zh-CN|style=Feynman)的发生。其结果正如一句古老的谚语所说：“A watched pot never boils”（常被看管的锅永远烧不开）。在量子世界里，一个被持续观测的系统，其演化会被“定格”。[@problem_id:139417]

### 量子社交网络：相互作用与纠缠

单个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)固然有趣，但[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的真正威力来自于它们之间的相互作用与**纠缠**（entanglement）。让两个原本独立的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)“感知”到彼此的存在，是构建[量子逻辑门](@keyword=quantum_logic_gates|lang=zh-CN|style=Feynman)的基础。

当两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)通过电容或[电感耦合](@keyword=inductive_coupling|lang=zh-CN|style=Feynman)在一起时，它们的[非谐性](@keyword=anharmonicity|lang=zh-CN|style=Feynman)与相互作用会产生一种称为**[ZZ相互作用](@keyword=zz_interaction|lang=zh-CN|style=Feynman)**的效应。这听起来很神秘，但其物理图像非常直观：[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)A的跃迁频率，会因为[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)B是处于[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|0\rangle$ 还是[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) $|1\rangle$ 而发生一个微小的移动。[@problem_id:139354] 这种能量的“条件性”移动是实现 CPHASE（受控相位）等关键两比特[量子门](@keyword=quantum_computing_gates|lang=zh-CN|style=Feynman)的核心机制。深入分析会发现，这种效应来源于[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)之间的“虚拟[光子](@keyword=photon|lang=zh-CN|style=Feynman)”交换，即系统在极短的时间内“借用”能量，跃迁到诸如 $|2\rangle$ 态等计算空间之外的更高能级，然后再返回。

当我们把[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)与另一个量子系统（如一个谐振器）之间的耦合推向**[超强耦合](@keyword=ultrastrong_coupling|lang=zh-CN|style=Feynman)**（ultrastrong coupling）乃至**深强耦合**（deep-strong coupling）的极致时，物理图像会变得更加离奇和深刻。在这一区域下，系统的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)——我们通常认为是“真空”或“空无一物”的状态——不再是简单的“比特处于[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，谐振器里没有[光子](@keyword=photon|lang=zh-CN|style=Feynman)”。相反，[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)本身就是一个复杂的[纠缠态](@keyword=entangled_state|lang=zh-CN|style=Feynman)，其中充满了不断产生和湮灭的“虚拟[光子](@keyword=photon|lang=zh-CN|style=Feynman)”。[@problem_id:139399] 物质与光之间的界限开始模糊，真空本身也展现出丰富的内在结构。这不仅为[量子信息处理](@keyword=quantum_information_processing|lang=zh-CN|style=Feynman)开辟了全新的可能性，也让我们得以窥见量子[场论](@keyword=field_theory|lang=zh-CN|style=Feynman)在凝聚态物理系统中的迷人展现。

至此，我们已经探索了[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)从构建到操控，再到与环境和测量相互作用的核心物理原理。正是这些原理的交织，构成了这个充满挑战与希望的领域的基础。在下一章，我们将看看科学家们如何利用这些原理，来对抗[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)，并最终构建出更强大、更可靠的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机。
