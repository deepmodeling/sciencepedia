## 引言
在量子力学与工程学的交汇处，存在着一种灵敏度无与伦比的设备：[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)（Superconducting Quantum Interference Device），简称 SQUID。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 能够探测到比人脑产生的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)弱数千倍的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，是科学界已知的最强大的磁力计。然而，赋予其这种非凡能力——植根于超导性和量子隧穿等奇特现象——的原理，似乎抽象且远离实际应用。本文旨在弥合这一差距，揭示 SQUID 操作的神秘面纱，并探讨其在整个科学领域的变革性影响。在第一章“原理与机制”中，我们将进入量子世界，了解[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)和[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)如何赋予 SQUID 如此高的灵敏度。随后，“应用与跨学科联系”一章将展示这个非凡的设备如何作为一种主要工具，在从[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)、化学到[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)前沿等领域中发挥作用，揭示定义我们世界的无形磁学印记。

## 原理与机制

想象一下，你有一个由[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)制成的完美圆环。[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)是一种材料，当冷却到某个临界温度以下时，会失去所有电阻。但它还会做一些更神奇的事情：它变成一个单一、巨大的量子物体。所有携带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的电子配对成所谓的**[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)**，这些[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)开始以完美的同一步调起舞，由一个贯穿整个环的单一、相干的量子波函数来描述。

现在，量子力学的一个基本规则是[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)必须是单值的。如果你沿着环绕行一周后回到起点，这个[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的值必须与初始值相同。这个看似简单的要求带来了一个深远的结果。在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)存在的情况下，这个[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的相会发生扭曲。为了让[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在绕行一圈后能够完美地与自身重合，穿过环孔的总磁通量——即[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的总量——不能是任意值。它必须是自然界一个[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)的整数倍：**磁通量子**，记作 $\Phi_0 = h/(2e)$，其中 $h$ 是普朗克常数，$2e$ 是一个库珀对的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。

这就是**[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)**，它是 SQUID 的灵魂。[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)就像给[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)穿上了一件小小的量子紧身衣，只允许[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)以离散、量子化的包形式存在。[@problem_id:2291082]

### 问题的核心：约瑟夫森结

一个完美的、未断裂的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)很有趣，但其真正的潜力在我们有意削弱它时才被释放出来。想象我们把这个环切开，插入一个非常薄的绝缘材料层。这个断点被称为**约瑟夫森结**。这是我们原本完美的超导电路中的一个“弱连接”。

你可能会认为这个断点会阻止电流流动。对于普通电子来说，确实如此。但[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)是量子力学对象。它们可以直接**隧穿**通过这个势垒，就好像它不存在一样。然而，这种隧穿[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)并非无条件的。其最大值取决于结两侧[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的量子相之差。电流与相位之间的这种关系是第一**[约瑟夫森效应](@keyword=josephson_effect|lang=zh-CN|style=Feynman)**，是 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 操作的基石。

[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 有两大类，根据结的数量来区分。**射频 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman)**（RF SQUID）在其环路中使用单个结，而我们将重点讨论的**直流 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman)**（DC [SQUID](@keyword=squid|lang=zh-CN|style=Feynman)）则在[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)上[并联](@keyword=parallel_connection|lang=zh-CN|style=Feynman)放置了两个[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)。[@problem_id:1806317]

### 从环路到干涉仪

为什么是两个结？因为两条路径允许**[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)**。这就是 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 中的“I”：[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)（Superconducting Quantum Interference Device）。当[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)接近[并联](@keyword=parallel_connection|lang=zh-CN|style=Feynman)的结时会分流，一部分通过每个结进行隧穿。这两支电流随后在另一侧重新组合。

就像[双缝实验](@keyword=double_slit_experiment|lang=zh-CN|style=Feynman)中的光波一样，这两个物质波可以发生相长干涉，导致总[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)很大，或者相消干涉，导致总[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)很小。决定这种干涉性质的是什么呢？是穿过环路的磁通量 $\Phi$。

磁通量控制着两条路径之间的相对[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)。结果是，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 在无电阻情况下能够承载的最大[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)，即**[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)**，是所施加[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的[周期函数](@keyword=periodic_functions|lang=zh-CN|style=Feynman)。这个美丽的干涉图样的数学形式惊人地简单：

$$ I_{\text{max}}(\Phi) = 2I_c \left| \cos\left(\frac{\pi \Phi}{\Phi_0}\right) \right| $$

这里，$I_c$ 是单个结的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)。请注意这个调制的周期：它就是磁通量子 $\Phi_0$。每当[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)变化一个 $\Phi_0$——一个约 $2.07 \times 10^{-15}$ 韦伯的微小磁通量——[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)就会经历一个完整的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)周期。这就是其传奇般灵敏度的来源。[@problem_id:2291082]

### 读取量子低语：[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 如何工作

我们有了一个其[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)对[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)极其敏感的设备。但我们如何读出它呢？我们不能直接测量[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)。相反，我们采取一种巧妙的方法。我们施加一个恒定的[直流偏置](@keyword=dc_biasing|lang=zh-CN|style=Feynman)电流 $I_{\text{bias}}$，这个电流被特意选择为略大于 SQUID 可能的最大[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)（$2I_c$）。

由于偏置电流总是大于无电阻状态下所能承载的电流，SQUID 被迫进入电阻态。设备两端出现一个电压 $V$。这个电压不是恒定的；它取决于偏置电流超出随磁通变化的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)的多少。随着[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi$ 的变化，$I_{\text{max}}(\Phi)$ 发生[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，因此电压 $V$ 也随之[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。

要将 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 用作磁力计，我们不直接测量磁通量，而是测量其两端的**电压**。磁通量的微小变化会引起可测量的电压变化。通过监测这个电压，我们可以检测到仅为单个[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)百万分之一的磁通量变化。这就是 SQUID 如何将量子干涉图样转换为宏观、可测量的信号。[@problem_id:1812683]

### 现实世界的干预：阻尼与屏蔽

当然，现实世界比我们简单的图景要复杂得多。两个关键的物理参数，通常用希腊字母贝塔（$\beta$）表示，决定了 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的实际性能。

首先，任何真实的约瑟夫森结都有电容。这个电容就像量子相位的惯性，使其不易改变。如果这个“惯性”太大，结就会变得**[欠阻尼](@keyword=underdamping|lang=zh-CN|style=Feynman)**。当偏置到电压态时，它在电流降低时不会平滑地返回到零电压态；由于其动量，它会“卡住”，只有在更低的电流下才返回。这种跳跃性的、滞回的行为对 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的操作来说是个麻烦。阻尼程度由 **Stewart-McCumber 参数** $\beta_C = \frac{2\pi I_c R^2 C}{\Phi_0}$ 捕捉。为确保平滑、无滞回的操作，设计者必须使 $\beta_C \lesssim 1$。最常见的方法是在每个结上并联一个微小的分流电阻，这会降低[有效电阻](@keyword=effective_resistance|lang=zh-CN|style=Feynman) $R$ 并提供一个“阻尼”[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的路径，使设备行为良好。[@problem_id:3018099]

其次，[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)本身不仅仅是一个几何路径；它有[自感](@keyword=self_inductance|lang=zh-CN|style=Feynman) $L$。这意味着环路中的任何环流都会产生其自身的磁通量。这种自生磁通量与外部施加的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)相反——这种现象被称为**屏蔽**。该效应的强度由**屏蔽参数** $\beta_L = 2 L I_c / \Phi_0$ 控制。如果 $\beta_L$ 太大（通常大于 1），SQUID 会主动抵抗你试图测量的磁通量。这会降低电压信号的调制深度，扭曲美丽的类余弦响应曲线，甚至可能引入其自身形式的滞回，从而严重降低磁力计的性能。因此，SQUID 的设计是一个精巧的平衡艺术，需要将 $\beta_C$ 和 $\beta_L$ 都保持在它们的最佳范围内。[@problem_id:2862988]

### 弱连接的艺术

到目前为止，我们谈论“[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)”时，仿佛它是一个单一、整体的东西。实际上，制造这些弱连接是[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的一项重大成就，它们有几种不同的类型。

- **SIS ([超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)-绝缘体-[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)) 结**，是经典的例子，其电流和相位之间具有优美的正弦关系。然而，它们的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)对绝缘体厚度呈指数级敏感，这使得它们在制造上难以获得高重现性。[@problem_id:3018016]
- **SNS ([超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)-正常金属-[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)) 结** 使用一层薄的正常、非超导金属作为弱连接。它们天然无滞回，因为正常金属起到了内置分流电阻的作用。然而，这个电阻本身是热噪声（约翰逊噪声）的来源，这会限制 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的最终灵敏度。它们的[电流-相位关系](@keyword=current_phase_relation|lang=zh-CN|style=Feynman)也明显非正弦。[@problem_id:3018016]
- 其他类型，如 **Dayem 桥**（超导薄膜上的一个简单窄颈）或**[纳米线](@keyword=nanowires|lang=zh-CN|style=Feynman)弱连接**，在某些方面更容易制造，但通常存在重现性差和其它噪声源的问题。[@problem_id:3018016]

结技术的选择是一项关键的工程决策，需要在[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的性能、噪声特性和制造的实际挑战之间进行权衡。

### 延伸探测：磁通变换器

[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 是一个对其环路处[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)极其敏感的探测器。但如果你想测量的样品——比如说，一种磁性[纳米材料](@keyword=nanomaterials|lang=zh-CN|style=Feynman)或人脑的微弱[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)——位于一定距离之外怎么办？你不能简单地把精密的 SQUID 直接放在任何东西上面。

解决方案是另一个优雅的超导电路：**磁通变换器**。它由一个闭合的超导线环和两个线圈组成。一个较大的**拾取线圈**（$L_p$）放置在待测样品附近。一个较小的**输入线圈**（$L_i$）放置在非常靠近 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 环路的位置，通过[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)与之耦合。

当样品的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)发生变化时，它会在拾取线圈中引起[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)变化。由于变换器是一个闭合的超导电路，磁通量必须守恒。为了抵消这种变化，导线中会感应出一个持续的[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)。这个相同的电流流过输入线圈，产生一个[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)，该磁通量被高效地“输送”到 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 环路中。通过仔细匹配线圈的电感，可以优化这种磁通量的传输，使 SQUID 能够作为一种超灵敏的远程磁性探测器。[@problem_id:1806360]

### 与微波共舞：Shapiro 台阶

[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 的物理学不止于此。如果除了[直流偏置](@keyword=dc_biasing|lang=zh-CN|style=Feynman)电流外，我们还用微波（射频电流）照射 [SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 会发生什么？产生直流电压的约瑟夫森[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，其频率可以锁定到所施加的射频驱动或其[谐波](@keyword=harmonic_waves|lang=zh-CN|style=Feynman)上。这种锁相现象表现为[电流-电压特性](@keyword=i_v_characteristics|lang=zh-CN|style=Feynman)中完全平坦的、量子化的电压台阶，称为 **Shapiro 台阶**。第 $n$ 阶台阶的电压由驱动频率 $f$ 精确决定：$V_n = n (h/2e) f$。

值得注意的是，SQUID 的[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)特性依然存在。这些 Shapiro 台阶的宽度受[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的调制，再次遵循相同的 $|\cos(\pi \Phi / \Phi_0)|$ 依赖关系。如果你将 SQUID 偏置在零电压台阶上并扫描磁通量，它将保持在零伏，直到你接近[半整数](@keyword=half_integers|lang=zh-CN|style=Feynman)[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)（$\Phi_0/2, 3\Phi_0/2, \dots$）。在这些点上，零电压台阶消失，[SQUID](@keyword=squid|lang=zh-CN|style=Feynman) 被迫跳到有限电压，从而在电压-磁通曲线中产生尖锐的峰值。这种交流和[直流约瑟夫森效应](@keyword=dc_josephson_effect|lang=zh-CN|style=Feynman)之间，与量子干涉交织在一起的非凡相互作用，不仅加深了我们对该设备的理解，也为计量学和射频探测等新应用打开了大门。[@problem_id:2863059]