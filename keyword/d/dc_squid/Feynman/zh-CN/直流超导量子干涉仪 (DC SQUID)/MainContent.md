## 引言
测量极其微弱的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)一直是科学领域一项长期存在的挑战，它限制了我们对从人[脑神经](@keyword=cranial_nerves|lang=zh-CN|style=Feynman)活动到新奇材料细微量子特性等各种现象的认知。受[经典物理学](@keyword=classical_physics|lang=zh-CN|style=Feynman)热噪声的限制，传统磁力计通常不足以胜任这些任务。那么，我们该如何窃听这些微弱的磁私语呢？答案不在于改进旧方法，而在于接纳一套完全不同的规则：超导和量子力学那些奇异而强大的原理。这就是[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)（Superconducting Quantum Interference Device，简称 SQUID）的领域，它是人类有史以来构想出的最灵敏的探测器之一。

本文将全面探讨作为量子测量基石的直流 SQUID。我们将从第一章“**原理与机制**”开始我们的旅程，剖析该器件的结构。我们将探索[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)和电子对的[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)如何产生对磁通量的极高灵敏度，这一现象由自然界的基本常数所支配。随后，第二章“**应用与跨学科联系**”将揭示这种非凡的灵敏度是如何被利用的。我们将考察 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 作为从神经科学到[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)等领域的大师级工具所扮演的角色，将其与传统技术进行比较，并展望其在[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)前沿的未来。通过这次探索，您将深刻体会到一个源于基础量子理论的器件，如何成为推动科学发现不可或缺的仪器。

## 原理与机制

想象你是一位身处异域的旅人，这里的规则截然不同。这就是超导的世界，一个电流可以无阻流动的领域；在这里，通常仅限于原子和电子微观范畴的量子力学，展现到了我们能够看见并操控的宏观尺度。[直流超导量子干涉仪](@keyword=dc_squid|lang=zh-CN|style=Feynman)（DC [SQUID](@keyword=squid|lang=zh-CN|style=Feynman)）不仅仅是一个器件，它更是一个宏伟的舞台，让我们能以一种惊人直接的方式，见证这些量子规则的运作。

### 量子十字路口

DC SQUID 的核心结构出奇地简单。它由一个闭合的[超导材料](@keyword=superconducting_materials|lang=zh-CN|style=Feynman)环路构成，但这个环路在两处被有意地断开。这些断点并非完全的间隙，而是超薄的绝缘势垒——薄到超导电子可以“隧穿”过去。每一个这样的特殊弱连接被称为一个**约瑟夫森结** (Josephson junction) [@problem_id:1806317]。

现在，让我们向这个装置中注入一股电流。当电流到达环路时，它面临一个岔路口。在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，载流子不是单个电子，而是被称为**库珀对** (Cooper pairs) 的束缚电子对。这些电子对如同单个量子力学实体一样行动。当一个[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)到达环路入口时，有两条路径可以通往出口：它可以隧穿通过第一个结，或者隧穿通过第二个结 [@problem_id:1806369]。

这正是量子基础教科书中的经典场景，与著名的[双缝实验](@keyword=double_slit_experiment|lang=zh-CN|style=Feynman)惊人地相似。在那个实验中，单个电子面对两条狭缝，却不可思议地似乎同时穿过了两条缝，从而产生了干涉图样。在这里，在我们的 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 中，库珀对面临两条量子路径。正如电子的情况一样，其结果并非两条路径可能性的简单加和，而是一种美妙而深刻的[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)。

### 干涉的法则

要理解这种干涉，我们必须使用量子力学的语言：波和相位的语言。每个库珀对都可以用一个[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)来描述，和任何波一样，它有振幅和相位。当我们的电流分开时，能够无阻通过该器件的总电流（即**[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)**，$I_c$）取决于两条路径的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在出口处如何叠加。

主导这种干涉的神奇要素是[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。如果一个[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi_{ext}$ 穿过[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)路，它会改变沿两条不同路径行进的库珀对之间的[相对相位](@keyword=relative_phase|lang=zh-CN|style=Feynman)。这是[阿哈罗诺夫-玻姆效应](@keyword=aharonov_bohm_effect|lang=zh-CN|style=Feynman) (Aharonov-Bohm effect) 的直接结果，该效应是量子物理学最深刻的结论之一，它指出带电粒子的相位会受到[电磁势](@keyword=electromagnetic_potentials|lang=zh-CN|style=Feynman)的影响，即使在场本身为零的区域也是如此。两条路径之间的[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)最终与所包围的磁通量成正比。

让我们像最早理解这个器件的物理学家那样，追溯其逻辑 [@problem_id:2990728]。通过每个结 $j=1,2$ 的电流遵循**约瑟夫森[电流-相位关系](@keyword=current_phase_relation|lang=zh-CN|style=Feynman)**，$I_j = I_{c0} \sin(\delta_j)$，其中 $I_{c0}$ 是单个结能承载的最大电流，$\delta_j$ 是其两端的量子相位差。总电流就是 $I = I_1 + I_2$。磁通量 $\Phi$ 通过**[磁通量量子化](@keyword=quantized_flux|lang=zh-CN|style=Feynman)条件**将两个[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)锁定在一起：$\delta_2 - \delta_1 = 2\pi \frac{\Phi}{\Phi_0}$，其中 $\Phi_0$ 是一个[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)。

当我们用一点三角函数知识将这些部分组合在一起时，我们得到了一个惊人优雅的结果，即整个器件所能承载的最大超导电流为：

$$
I_{crit, SQUID}(\Phi_{ext}) = 2 I_{c0} \left| \cos\left(\frac{\pi \Phi_{ext}}{\Phi_0}\right) \right|
$$

这个方程是直流 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的灵魂 [@problem_id:1806351]。它告诉我们，总[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)并非恒定不变，而是随磁通量[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。当磁通量为零（或 $\Phi_0$ 的整数倍）时，余弦项为 1，我们得到最大相长干涉：器件能承载两倍于单个结的电流。但当磁通量恰好是这个[基本单位](@keyword=fundamental_units|lang=zh-CN|style=Feynman)的一半时，余弦项为零，[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)消失——完美的相消干涉！两条路径相互抵消了。

### 磁学的量子标尺

这种干涉的模式将我们引向故事中最关键的元素：**[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子** $\Phi_0$。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)每次在[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)增加一个确切的量 $\Phi_0$ 时，都会重复其优美的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。这个值并非任意的，它由自然界的基本常数铸就：

$$
\Phi_0 = \frac{h}{2e} \approx 2.07 \times 10^{-15} \ \text{Wb}
$$

在这里，$h$ 是普朗克常数，[量子理论](@keyword=quantum_theory|lang=zh-CN|style=Feynman)的基石，而 $e$ 是单个电子的元[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。请注意分母中的因子 $2e$。这不是笔误；它是一个直接且不可否认的证据，证明了引起超导的载流子确实是电子对 [@problem_id:1806334]。如果是单个电子作为载流子，[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)周期将会是现在的两倍。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的运行本身就是对库珀对存在的一个宏观测量与证实。

这种周期性将 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 变成了一把用于测量[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的、精度惊人的标尺。其响应的每一次[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)都对应于这把量子标尺上的一个“刻度”，一个大小为 $\Phi_0$ 的刻度。通过简单地计算这些[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，我们就可以测量[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的变化，其精度与宇宙的[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)紧密相连。

### 读取量子信号

我们得到了这个奇妙的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)，但我们如何观察它呢？我们无法直接测量[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)，而是测量电压。关键在于给 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 施加一个恒定的**[偏置电流](@keyword=bias_current|lang=zh-CN|style=Feynman)** $I_{bias}$。由此产生了两种主要策略。

一种方法是将[偏置电流](@keyword=bias_current|lang=zh-CN|style=Feynman)设定在[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)的最小值（$0$）和最大值（$2I_{c0}$）之间，例如，$I_{bias} = \frac{3}{2}I_{c0}$ [@problem_id:1806316]。当外部磁通量缓慢变化时，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman) $I_{crit,SQUID}$ 会上下[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。每当 $I_{crit,SQUID}$ 降到我们固定的 $I_{bias}$ 以下时，SQUID 就无法再维持[零电阻](@keyword=zero_resistance|lang=zh-CN|style=Feynman)状态。它会突然“开启”并产生一个电压。当 $I_{crit,SQUID}$ 再次升到 $I_{bias}$ 以上时，电压消失。随着磁通量的扫过，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 会“一开一关”地闪烁，提供一种类似数字式的对磁通量子的计数。

一种更常用且实用的方法是用一个始终略**大于**其最大可能[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)的电流 $I_{bias}$ 来偏置 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) ($I_{bias} > 2I_{c0}$)。在这种模式下，SQUID 始终处于有阻状态，其两端总有一个电压。然而，这个电压不是恒定的。电压的大小取决于“过剩”电流有多少——即[偏置电流](@keyword=bias_current|lang=zh-CN|style=Feynman)与[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)之间的差值。当 $I_{crit,SQUID}$ 随着磁通量[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)时，SQUID 两端的电压也随之[同步](@keyword=entrainment|lang=zh-CN|style=Feynman)[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman) [@problem_id:1806336]。结果是一条平滑的、周期性的电压-磁通曲线（$V$-$\Phi$ 曲线）。峰峰值电压摆幅 $\Delta V = V_{max} - V_{min}$ 就是我们测量的信号。这个信号是对底层量子干涉的忠实模拟再现。

### 追求极致灵敏度

SQUID 以其灵敏度而闻名。这从何而来？仅仅看到[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)是不够的；要探测到磁通量无限小的变化，我们需要输出电压对那个微小的磁通量变化做出尽可能大的响应。换言之，我们需要 $V$-$\Phi$ 曲线的斜率尽可能陡峭。

这个斜率被称为**传输函数**，$V_{\Phi} = \frac{dV}{d\Phi_{ext}}$ [@problem_id:1806312]。观察周期性的 $V$-$\Phi$ 曲线，我们可以看到在波峰和波谷处（电压最大或最小处），斜率为零。曲线在波峰和波谷之间的中点处最陡。为了达到最高灵敏度，SQUID 在这个最大斜率点上运行。复杂的电子设备被用于一个**[磁通锁定环](@keyword=flux_locked_loop|lang=zh-CN|style=Feynman)**中，以创建一个[反馈系统](@keyword=feedback_systems|lang=zh-CN|style=Feynman)。如果外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)试图使 SQUID 偏离这个最佳偏置点，反馈电路会产生一个反向磁通，以将其完美地保持在原位。这个反馈磁通的大小就是对所探测的外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的精确测量。正是这种量子干涉与巧妙的电子反馈相结合，使得 SQUID 能够测量比地球[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)弱十亿倍的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。

### 来自现实世界的注记

到目前为止，我们的旅程一直处于一个理想化的世界中。真实的 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 具有不完美性，这增加了引人入胜的复杂性。

如果两个约瑟夫森结并非完全相同，比如 $I_{c1} \neq I_{c2}$ 会怎样？干涉仍然会发生，但这就像一个略微跑调的和弦。[相消干涉](@keyword=destructive_interference|lang=zh-CN|style=Feynman)不再完美。总[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)在最小值点不再降至零。相反，[调制](@keyword=modulation|lang=zh-CN|style=Feynman)深度——最大和最小[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)之差——会减小。一个优美的结论表明，[调制](@keyword=modulation|lang=zh-CN|style=Feynman)深度恰好是两个结中**较弱**的那个结的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)的两倍，即 $\Delta I_c = 2 \min(I_{c1}, I_{c2})$ [@problem_id:1806349]。为了获得最佳性能，制造者必须不遗余力地使两个结尽可能相同。

此外，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 环路中循环的电流本身也会产生一个小的磁通量。这个“屏蔽”磁通通常与外部磁通量方向相反。如果环路的[自感](@keyword=self_inductance|lang=zh-CN|style=Feynman) $L$ 足够大，这个效应会变得很显著。这种行为由一个称为**屏蔽参数**的[无量纲数](@keyword=dimensionless_numbers|lang=zh-CN|style=Feynman) $\beta_L = 2LI_{c0}/\Phi_0$ 决定。如果 $\beta_L$ 变得过大（通常指 $\beta_L > 1$），SQUID 对外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的响应就会变得具有迟滞性——内部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)会依赖于所施加场的*历史* [@problem_id:83067]。这为实际器件设计增加了另一层必须管理的复杂性。

这些现实世界的细节并没有减损 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的美感。相反，它们丰富了这个故事，展示了对基本量子原理的深刻理解如何使我们不仅能解释，而且能工程化并掌握这些非凡的设备，将一种量子奇趣转变为科学最强大的工具之一。