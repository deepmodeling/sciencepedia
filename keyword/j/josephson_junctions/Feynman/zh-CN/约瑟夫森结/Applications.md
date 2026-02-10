## 应用与跨学科联系

既然我们已经窥探了[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)奇特的量子核心，你可能会留下这样的印象：它只是一个精密的实验室奇物，物理学家的玩具。事实远非如此。这个诞生于量子理论深处的非凡器件，已经发展成为物理学家和工程师武库中最通用、最强大的工具之一。正是那看似抽象的量子相干性，被证明是其惊人效用的源泉。这些应用并非小众；它们是基础性的，范围从我们定义日常单位的方式，到我们构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机最大胆的尝试，甚至延伸到探索物质与宇宙本身的本质。

### 终极标尺：重新定义伏特

让我们从一个看似平淡无奇但却极其重要的问题开始：什么是伏特？在很长一段时间里，标准伏特是基于一组化学电池定义的，但它们性能不稳定、容易漂移，并且难以完美复现。[交流约瑟夫森效应](@keyword=ac_josephson_effect|lang=zh-CN|style=Feynman)改变了一切。

回想那个惊人简洁的关系：在结两端施加直流电压 $V$，它会辐射出频率为 $f$ 的[电磁波](@keyword=electromagnetic_waves|lang=zh-CN|style=Feynman)，满足 $hf = 2eV$。这意味着你可以将电压直接转换为频率 [@problem_id:1812687] [@problem_id:1812730]。为什么这如此具有革命性？因为我们可以使用[原子钟](@keyword=atomic_clocks|lang=zh-CN|style=Feynman)——有史以来最精确的计时设备——以惊人的精度测量频率。通过将电压与频率联系起来，约瑟夫森结使我们能够将这种精度转移到电学世界。

在实践中，计量学实验室的做法正好相反。他们采用一个高度稳定的微波源，比如一个锁定到[原子钟](@keyword=atomic_clocks|lang=zh-CN|style=Feynman)的微波源，将其照射在约瑟夫森结上。结不仅仅是吸收辐射，它以一种壮观的量子方式响应。它的[电流-电压特性](@keyword=i_v_characteristics|lang=zh-CN|style=Feynman)不再是平滑的，而是分解成一系列完全平坦、间距完美的电压台阶。这些就是著名的“[夏皮罗台阶](@keyword=shapiro_steps|lang=zh-CN|style=Feynman)” [@problem_id:560913]。

任何两个相邻台阶之间的电压差 $\Delta V$ 由一个优美简洁的公式给出：$\Delta V = \frac{hf}{2e}$ [@problem_id:1812729]。注意这个方程里有什么：普朗克常数 $h$、[基本电荷](@keyword=elementary_charge|lang=zh-CN|style=Feynman) $e$ 以及微波的频率 $f$。前两者是自然界的基本常数，而第三个是我们能最精确控制的量。具体结的属性——其材料、尺寸、温度——都无关紧要了！这就是它的魔力所在。世界上任何地方的任何两个实验室，都可以构建一个[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)，用相同频率的微波照射它，并以令人难以置信的准确度产生完全相同的电压台阶。这个系统现在正式定义了伏特。它是一把用于电势的完美量子力学标尺，反过来也可以用作频率或微波辐射的极其灵敏的探测器 [@problem_id:1812691]。

### [量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的核心

让我们定义伏特的那种量子精度，同样可以被用来实现一个更宏伟的目标：构建一台[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机。但为此，我们必须停止将结仅仅看作一个[频率-电压转换器](@keyword=frequency_to_voltage_converter|lang=zh-CN|style=Feynman)，而开始将其视为它的真正本质——一个宏观量子物体。

一个约瑟夫森结不仅仅是一个电阻或一个简单的二极管。由于有[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)流过，它的行为像一种特殊的电感——一种非线性[电感](@keyword=inductance|lang=zh-CN|style=Feynman)。并且，像任何真实的物理物体一样，它也有一些电容。因此，一个结的行为就像一个量子[LC电路](@keyword=lc_circuits|lang=zh-CN|style=Feynman)。如果你给它一个小的“推动”（一点电流），它两端的[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman) $\phi$ 将会以一个特定的“[等离子体频率](@keyword=plasma_frequency|lang=zh-CN|style=Feynman)”来回[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，很像弹簧上的一个质量块 [@problem_id:97135]。

关键在于：因为它是一个*量子*[振荡器](@keyword=oscillators|lang=zh-CN|style=Feynman)，它的能量不是连续的。它只能存在于离散的、量子化的能级上。并且因为结的“电感”是非线性的（由于那个 $\sin(\phi)$ 关系），这些能级不是均匀间隔的。这是一个巨大的天赋！这意味着我们可以单独挑出最低的两个能级——[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)和第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)——并用它们来表示一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)（qubit）的 $|0\rangle$ 和 $|1\rangle$。这个器件，一个由[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)并联的简单[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)，就是著名的“transmon”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，是当今许多领先的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的主力。

我们如何控制和读出这个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)呢？我们利用的正是[交流约瑟夫森效应](@keyword=ac_josephson_effect|lang=zh-CN|style=Feynman)本身！我们将[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)放置在一个[微波谐振器](@keyword=microwave_resonator|lang=zh-CN|style=Feynman)（一种光的“回音室”）内。通过以精确的频率——对应于 $|0\rangle$ 和 $|1\rangle$ 之间[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的频率——发送微波脉冲，我们可以驱动[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)从一个状态转换到另一个状态。当[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)弛豫回[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)时，它会发射一个相同频率的微波[光子](@keyword=photon|lang=zh-CN|style=Feynman)，谐振器会接收到这个[光子](@keyword=photon|lang=zh-CN|style=Feynman)。[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)如何向其环境发射功率的复杂物理过程是一个深入研究的课题，因为它对于设计高保真度量子操作至关重要 [@problem_id:52611]。从本质上讲，[约瑟夫森关系式](@keyword=josephson_relation|lang=zh-CN|style=Feynman)为我们提供了对这些我们从零开始构建的[人造原子](@keyword=artificial_atoms|lang=zh-CN|style=Feynman)进行写入、操控和读取的语言。

### 深入物质结构的窗口

[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)不仅用于构建事物，它们还用于*发现*事物。通过巧妙地布置它们，我们可以制造出对量子世界最微妙属性敏感的仪器，从而让我们能够检验关于物质本质的最深刻理论。

一个优美的例子来自高温超导体的长期谜题。在它们被发现后不久，一个关键问题出现了：这些材料中库珀对的[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)是像[常规超导体](@keyword=conventional_superconductors|lang=zh-CN|style=Feynman)那样呈球对称（“$s$波”态），还是具有更复杂的四叶草形状（“$d$波”态）？

[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)提供了答案。物理学家们在[高温超导体](@keyword=high_temperature_superconductors|lang=zh-CN|style=Feynman)的单晶上构建了一个[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)——一个包含两个[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)路。但他们巧妙地做了一个改变：一个结被放置在晶体的“侧面”，另一个在“顶面”，形成一个拐角。在$d$波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，库珀对的量子相位在一个轴向上是正的，在另一个轴向上是负的。这种拐角结的设置迫使SQUID的两个臂去采样这些不同的相位。结果是，其中一个结的行为就好像它内部天生就有一个 $\pi$ 的相移。

这个“$\pi$结”产生了显著的效果。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)的量子干涉图样——即其最大电流随[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)变化的轨迹——与普通[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)相比，会移动半个周期。它在零[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)下不是出现最大电流，而是出现最小值。这个预测的[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)在实验中被观察到，为这些奇异材料的$d$波性质提供了决定性的证据 [@problem_id:2994155]。更引人注目的是，制造一个包含奇数个此类结的环，会导致一种量子“阻挫”状态，其中环的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)在零外场下会自发产生一个恰好等于基本磁通量子*一半*的磁通量，即 $\Phi_0/2$ [@problem_id:2994155]。这是[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)底层量子力学的一个惊人的宏观体现。

### 拓展前沿：自旋电子学与宇宙学

故事并未就此结束。[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)的原理是如此基础，以至于它们不断在物理学的新兴领域中找到新的用武之地。

其中一个前沿是[自旋电子学](@keyword=spintronics|lang=zh-CN|style=Feynman)，其目标是利用电子的自旋而不仅仅是其[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)来承载信息。事实证明，如果你构建一个绝缘势垒具有强自旋轨道耦合的约瑟夫森结，会发生一件非凡的事情。由直流电压驱动的结两端[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的相位差，不仅会泵浦出[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)电流，还会泵浦出[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的*自旋流* [@problem_id:230771]。这种“交流自旋[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)”为创造能将电信号直接转换为自旋波的器件打开了大门，有可能将超导的无耗散世界与[自旋电子学](@keyword=spintronics|lang=zh-CN|style=Feynman)的快速、低[功耗](@keyword=dissipated_power|lang=zh-CN|style=Feynman)世界融合在一起。

最后，让我们进行一次真正宏大的飞跃，将我们的量子器件与宇宙本身联系起来。这是一个思想实验，但却是那种 Feynman 会因其统一物理学不同部分的力量而喜爱的实验。想象一下，我们将一个电压偏置的约瑟夫森结放置在一颗致密恒星（如白矮星）的表面上。这个结遵循量子力学定律，忠实地以[约瑟夫森频率](@keyword=josephson_frequency|lang=zh-CN|style=Feynman) $f_{em} = 2eV/h$ 发射辐射。现在，地球上的一位天文学家，在远离恒星的地方观察这种辐射。根据爱因斯坦的广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)，光线从恒星巨大的[引力势](@keyword=gravitational_potential|lang=zh-CN|style=Feynman)阱中爬出时会损失能量，其频率会发生[红移](@keyword=redshift|lang=zh-CN|style=Feynman)。天文学家观测到的频率 $f_{obs}$ 将低于 $f_{em}$。红移的精确量取决于恒星的质量和半径。

最终的观测频率方程优美地将量子世界与宇宙交织在一起 [@problem_id:560828]。它包含了支配量子领域的普朗克常数 $h$ 和支配宇宙最大尺度的[引力常数](@keyword=gravitational_constant|lang=zh-CN|style=Feynman) $G$。这一个单一的、尽管是假设性的测量，将量子力学、[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)和广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)联系在了一起。它是物理定律统一性的深刻证明，也是对[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)——一个不仅是得力工具，也是无尽灵感与发现源泉的器件——的恰当致敬。