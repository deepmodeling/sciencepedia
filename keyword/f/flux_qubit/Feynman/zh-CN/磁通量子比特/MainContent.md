## 引言
构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的探索取决于一个单一的基本挑战：创造并控制一个可靠的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)（qubit）。虽然原子和[光子](@keyword=photon|lang=zh-CN|style=Feynman)是天然的候选者，但另一种强大的方法则源自超导电路的宏观世界。这些电路在冷却到接近绝对零度时，可以表现为单一的、相干的量子物体。这就提出了一个引人入胜的问题：我们如何利用超导性原理来设计一个可以存储和处理[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)的[两能级系统](@keyword=two_level_system|lang=zh-CN|style=Feynman)？

本文旨在揭示其中一个最杰出的答案：[磁通量子比特](@keyword=flux_qubit|lang=zh-CN|style=Feynman)。我们将探索一个简单的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)路，在奇异的量子力学定律支配下，如何被转变为一个精密且可控的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。您将了解到[持续电流](@keyword=persistent_currents|lang=zh-CN|style=Feynman)、[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)以及约瑟夫森结的独特性质如何相互作用，从而产生一个鲁棒的量子器件。

我们的旅程始于在 **原理与机制** 部分剖析其核心操作理论。在这里，我们将揭示[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)和[量子隧穿](@keyword=quantum_mechanical_tunneling|lang=zh-CN|style=Feynman)如何创造一个“[双势阱](@keyword=double_well_potential|lang=zh-CN|style=Feynman)”——一个其两个谷底构成了[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的‘0’和‘1’态的景观，以及一个简单的哈密顿量如何优雅地描述这个系统。在此之后，文章将在 **应用与跨学科联系** 中探讨该[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的实际用途和更广泛的意义。我们将研究物理学家如何与这些脆弱的量子系统“对话”并保护它们，并看到它们不仅作为计算单元，还作为探索现实本质的微型实验室如何发挥作用。

## 原理与机制

想象一下，你有一个理想导体，一种电阻绝对为零的物质。如果你将它塑造成一个环，并让电流开始流动，它会持续多久？在没有任何电阻耗散能量的情况下，电流应该永远流动——这就是**[持续电流](@keyword=persistent_currents|lang=zh-CN|style=Feynman)**。这不仅仅是幻想；它是超导性的现实，也是我们构建[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)之路上的第一块垫脚石。但是，一个简单的、永恒流动的电流只是一个经典的好奇现象。为了让它变得量子化，我们需要引入一些来自量子世界的美妙而微妙的成分。

### 环中之河：[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)定律

让我们继续讨论我们的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)。在量子领域，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中的载流子不是单个电子，而是它们的配对，称为**库珀对**。这些库珀对的行为就像一个单一、统一的[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)，无散射、无损耗地流动。现在，如果我们将环置于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中会发生什么？

正如吉他弦只能以形成[驻波](@keyword=standing_waves|lang=zh-CN|style=Feynman)的特定频率[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)一样，在环中循环流动的库珀对的量子波也必须满足一个特殊条件：在完成一整圈后，其相位必须回到起始值。这个“[相位相干性](@keyword=phase_coherence|lang=zh-CN|style=Feynman)”的简单要求带来了一个深刻的后果，大自然以不容置疑的刚性强制执行这一法则。它规定了穿过环的总[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)——来自任何外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的磁通量与[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)自身电流产生的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)之和——不能是任意值。它必须是基本常数**[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)** $\Phi_0 = h/(2e)$ 的整数倍。

这被称为**[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)**。环会采取一切必要措施来满足这个定律。想象一下，我们试图让系统陷入两难。我们施加一个精确调谐的外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi_{ext}$，它正好位于两个整数值之间，比如对于某个整数 $k$ 来说，$\Phi_{ext} = (k + 1/2)\Phi_0$ [@problem_id:1778085]。此时[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)陷入了困境。它不能无所作为；总[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)必须是 $\Phi_0$ 的整数倍。它通过产生自身的[持续电流](@keyword=persistent_currents|lang=zh-CN|style=Feynman) $I_s$ 来解决这个问题。这个电流产生自身的磁通量 $L I_s$（其中 $L$ 是环的[自感](@keyword=self_inductance|lang=zh-CN|style=Feynman)），它要么与外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)相加，要么相减，以达到最接近的“合法”值。

系统面临一个选择：要么感应出顺时针方向的电流，将总[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)推高到 $(k+1)\Phi_0$；要么感应出逆时针方向的电流，将[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)拉低到 $k\Phi_0$。由于起始点正好在中间，两种选择的能量代价完全相同。我们得到了两个能量相等的简并态，仅通过环流的方向来区分。这就是一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的雏形——两个不同且稳定的状态。我们可以称它们为 $|L\rangle$（代表左旋，即逆时针电流）和 $|R\rangle$（代表右旋，即顺时针电流）。

### 量子隧道：引入约瑟夫森结

一个简单的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)有点过于“经典”。这些状态非常稳固，但它们缺乏[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)所需的量子精妙性。将磁通量拉至整数值所需的电流通常很大，分隔 $|L\rangle$ 和 $|R\rangle$ 态的能垒也巨大。为了让事情更有趣，我们需要在我们的完美环中引入一个“弱连接”。

这个弱连接就是**[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)**，一个分隔两块[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的纳米级薄绝缘层。在经典物理中，没有电流能穿过这个间隙。但由于[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)是量子物体，它们可以**隧穿**通过这个势垒。已故的伟大物理学家 Brian Josephson 发现，隧穿过结的超导电流 $I$ 不是任意电流；它通过优美的公式 $I = I_c \sin(\phi)$ 与结两侧的量子[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman) $\phi$ 相关，其中 $I_c$ 是结的**[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)**，即它能支持的最大超导电流。

在我们的环中放置一个[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)从根本上改变了它的特性 [@problem_id:1812686]。这个结就像一个坚硬环上的铰链，使其更加灵活。[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)波的相位不再需要完美连续；它在穿过结时可以“滑移”。[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)规则现在被软化了。总[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)不再是严格量子化的，而是磁通量与结上[相位滑移](@keyword=phase_slips|lang=zh-CN|style=Feynman)之和必须被量子化。这导致了丰富的非线性行为。对于特定的外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)，我们可能会找到多个关于[持续电流](@keyword=persistent_currents|lang=zh-CN|style=Feynman)的稳定解，对应于系统平衡来自[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)和结的相位贡献的不同方式。

### 用磁通雕塑：[双势阱](@keyword=double_well_potential|lang=zh-CN|style=Feynman)

要理解[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的状态，我们必须从能量的角度思考。任何物理系统都会寻求其最低能量状态。我们的带结环的能量主要有两个组成部分：存储在环路中的磁能（$E_L = \frac{1}{2} L I^2$）和存储在结中的**[约瑟夫森能量](@keyword=josephson_energy|lang=zh-CN|style=Feynman)**（$E_J(\phi) = -E_{J0} \cos(\phi)$），其中 $E_{J0}$与结的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman) $I_c$ 成正比。结“偏好”其两端的[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)为零，以最小化其能量。

一个特别巧妙的设计，也是许多现实世界量子处理器的核心部件，是**三结[磁通量子比特](@keyword=flux_qubit|lang=zh-CN|style=Feynman)**。它由一个被三个结打断的环路组成，其中两个结相同，第三个结略小一些 [@problem_id:2832181]。这种构造为我们提供了精妙的控制能力。通过调节外部磁通量 $\Phi_{ext}$，我们可以雕塑系统的势能景观。

当我们将外部磁通量设置为恰好半个[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)，即 $\Phi_{ext} = \Phi_0/2$ 时，一个美丽的对称性出现了。势能作为环路中磁通量的函数，形成了一个完美的**[双势阱](@keyword=double_well_potential|lang=zh-CN|style=Feynman)**。一个[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)对应于一个具有顺时针持续环流的稳定态 $|R\rangle$，另一个对应于一个具有逆时针环流的同样稳定的态 $|L\rangle$。这两个态的能量完全相同。这个特殊的磁通值 $\Phi_{ext} = \Phi_0/2$ 被称为**简并点**或**甜点**。这两个[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)代表了我们潜在比特的经典“0”和“1”。

### 当世界碰撞：量子哈密顿量

到目前为止，我们有两个独立的[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)，两个独立的状态。但我们生活在一个量子世界。如果环路中的磁通量是一个量子变量，它就不必待在某一个[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)里。它可以隧穿过分隔两个最小值的能垒。这种量子隧穿是[磁通量子比特](@keyword=flux_qubit|lang=zh-CN|style=Feynman)的核心。

这种隧穿的可能性从根本上改变了故事。$|L\rangle$ 和 $|R\rangle$ 这两个状态不再是真正的能量本征态。真正的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)变成了两者的对称叠加，形式如 $(|L\rangle + |R\rangle)/\sqrt{2}$，而第一[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)则是反对称叠加，形式如 $(|L\rangle - |R\rangle)/\sqrt{2}$。由于隧穿，之前[能量简并](@keyword=energy_degeneracy|lang=zh-CN|style=Feynman)的两个状态现在被一个小的能量[差分](@keyword=differencing|lang=zh-CN|style=Feynman)开了，这个差被称为**隧穿分裂**或[能量间隙](@keyword=energy_gap|lang=zh-CN|style=Feynman)，用 $\Delta$ 表示。

这个间隙 $\Delta$ 的大小关键取决于[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)间能垒的高度和宽度 [@problem_id:1907785]。更高或更宽的能垒使得隧穿更不可能发生，导致 $\Delta$ 更小。这个隧穿过程是量子“[瞬子](@keyword=instantons|lang=zh-CN|style=Feynman)”的一个美丽例子，这是一条在经典物理中被禁止但在量子力学中被允许的路径。

我们现在可以用一个极其简单而强大的[有效哈密顿量](@keyword=effective_hamiltonian|lang=zh-CN|style=Feynman)来描述整个量子系统，这是一个决定其演化的矩阵。在我们电[流态](@keyword=flow_regimes|lang=zh-CN|style=Feynman)的[基矢](@keyword=basis_vector|lang=zh-CN|style=Feynman) $\{|L\rangle, |R\rangle\}$ 下，这个哈密顿量看起来是这样的 [@problem_id:468511]：

$$ \hat{H} = -\frac{1}{2} \begin{pmatrix} \varepsilon & \Delta \\ \Delta & -\varepsilon \end{pmatrix} = -\frac{1}{2} (\varepsilon \hat{\sigma}_z + \Delta \hat{\sigma}_x) $$

我们来解释一下这个公式。**泡利矩阵** $\hat{\sigma}_z$ 和 $\hat{\sigma}_x$ 只是描述[两能级系统](@keyword=two_level_system|lang=zh-CN|style=Feynman)的一种便捷的数学语言。
*   带有 $\hat{\sigma}_z$ 的项代表两个电[流态](@keyword=flow_regimes|lang=zh-CN|style=Feynman)之间的能量差。参数 $\varepsilon$ 是**能量偏置**，我们可以通过将外部[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi_{ext}$ 从甜点 $\Phi_0/2$ 调整开来直接控制它。当 $\varepsilon=0$ 时，我们处于甜点，两个[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)是平齐的。
*   带有 $\hat{\sigma}_x$ 的项代表两个状态之间的量子隧穿。这是混合 $|L\rangle$ 和 $|R\rangle$ 的“非对角”项。其强度由隧穿分裂 $\Delta$ 给出。

这个哈密顿量就是一切。它告诉我们[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的能级，以及当我们拨动控制旋钮时它们如何变化。

### 驾驭量子：控制与读出

如果你不能控制一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)并读取它的状态，那么它就没什么用。
*   **读出：** 我们[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的两个状态是由沿相反方向流动的电流定义的。这些电流产生微小但可测量的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。通过将我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)耦合到一个非常灵敏的磁力计（如[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)），我们可以测量这个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)并推断出[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的状态。我们测量的量与 $\hat{\sigma}_z$ 算符的[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)有关，它平均地告诉我们[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)态中“左旋电流”与“右旋电流”的成分各占多少 [@problem_id:468511]。

*   **控制：** 哈密顿量向我们展示了如何控制[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。我们可以通过向[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)环路发送小的磁通脉冲来按需改变 $\varepsilon$。想象一下，我们从处于甜点（$\varepsilon=0$）的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)开始。如果我们现在缓慢地改变磁通量，增加 $\varepsilon$，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)会温和地跟随，始终保持在可用的最低能量状态。这是一个**绝热**过程。但如果我们非常迅速地改变[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)，让 $\varepsilon$ 快速扫过能级最接近的“反[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)”点，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)就没有时间调整。它可以跃迁到[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)，这个过程被称为**郎道-齐纳跃迁** [@problem_id:2100258]。通过精确地定时和塑造这些磁通脉冲，我们可以将[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)从[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)驱动到[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)，或者创造任何我们想要的任意叠加态。这是执行[量子门](@keyword=quantum_computing_gates|lang=zh-CN|style=Feynman)的基础。

### 现实世界的干预：电感、缺陷与噪声

我们理想化的图景很美，但现实世界的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)必须应对一些额外的复杂性。
*   **[自感](@keyword=self_inductance|lang=zh-CN|style=Feynman)：** [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)环路中的[持续电流](@keyword=persistent_currents|lang=zh-CN|style=Feynman)会产生自己的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)。这个[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)[反作用](@keyword=backreaction|lang=zh-CN|style=Feynman)于[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)自身，部分屏蔽了我们施加的外部磁通量。这意味着[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)感受到的能量偏置 $\varepsilon$ 取决于[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)自身的状态！这种反馈效应有效地“修饰”了[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，降低了它对我们控制信号的敏感度 [@problem_id:139408]。这是工程师在精确控制[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)时必须考虑的微妙之处。

*   **制备缺陷：** 制造出三个完全相同的约瑟夫森结是不可能的。如果两个“相同”的较小结的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)略有不同会怎样？人们可能[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)这会使甜点偏离 $\Phi_{ext} = \Phi_0/2$ 的纯粹对称点。值得注意的是，由于三结设计的巧妙对称性，简并点在一阶近似下对这种小的不对称性是免疫的 [@problem_id:139309]。这种内在的鲁棒性是该设计如此受欢迎的原因之一。

*   **噪声：** [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)最大的敌人是来[自环](@keyword=self_loop|lang=zh-CN|style=Feynman)境的噪声，它会随机地翻转其状态或破坏其脆弱的量子叠加——这一过程称为**[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)**。甜点之所以“甜”，是因为在 $\Phi_{ext} = \Phi_0/2$ 处，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的能量对[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)的缓[慢波](@keyword=slow_waves|lang=zh-CN|style=Feynman)动是一阶不敏感的。这极大地增强了它的[相干性](@keyword=coherence|lang=zh-CN|style=Feynman)。然而，[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)并非完全免疫。它在二阶上仍然对磁通噪声敏感，并且仍然容易受到其他噪声源的影响，例如其结的[临界电流](@keyword=critical_current|lang=zh-CN|style=Feynman)的波动 [@problem_id:139365]。设计一个真正鲁棒的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机是一场对抗这些各种噪声通道的持续战斗，推动工程师创造更安静的环境和更具弹性的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)设计。

从一个遵循基本量子规则的简单线圈，我们构建了一个复杂、可控但又脆弱的量子物体。[磁通量子比特](@keyword=flux_qubit|lang=zh-CN|style=Feynman)证明了量子世界奇特而美丽的定律如何能够被驾驭、塑造并应用于计算的前沿。