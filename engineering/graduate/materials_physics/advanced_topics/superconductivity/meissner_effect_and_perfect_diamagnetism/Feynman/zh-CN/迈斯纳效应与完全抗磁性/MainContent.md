## 引言
提到超导，我们脑海中浮现的第一个画面往往是[零电阻](@keyword=zero_resistance|lang=zh-CN|style=Feynman)带来的、电流永不损耗的奇迹。然而，这一特性虽已足够令人惊叹，却并非超导现象的全貌。真正将[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)与理论上的“[完美导体](@keyword=perfect_conductor|lang=zh-CN|style=Feynman)”划清界限、揭示其深层物理本质的，是它与[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)之间一种更为独特和主动的相互作用。这种被称为“完美抗磁性”的现象，不仅是超导研究的基石，更是一座连接量子力学、[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)乃至宇宙学奥秘的桥梁。

本文旨在深入剖析这一核心特征——[迈斯纳效应](@keyword=the_meissner_effect|lang=zh-CN|style=Feynman)。我们将不再满足于零电阻的表面现象，而是要解答一个更根本的问题：是什么让[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)成为一种独特的量子物相？为了回答这个问题，本文将分为三个核心部分。首先，我们将通过思想实验和能量分析，揭示迈斯纳效应的原理与机制，探索从伦敦唯象理论到金兹堡-朗道[宏观量子态](@keyword=macroscopic_quantum_state|lang=zh-CN|style=Feynman)的层层深入的理解。接着，我们将跨越学科边界，探索这一效应在磁悬浮、[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)、天体物理探测乃至粒子物理中的广泛应用与深刻启示。最后，通过具体的计算练习，读者将有机会亲手应用这些理论，加深对超导世界量子规则的掌握。让我们一同启程，探索隐藏在绝对零度附近的物理学之美。

## 原理与机制

我们对[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的第一印象往往是它那不可思议的零电阻特性。想象一根由[超导材料](@keyword=superconducting_materials|lang=zh-CN|style=Feynman)制成的电线，一旦电流开始流动，它就可以永远、永远地流下去，没有任何能量损失。这本身已经足够神奇，但超导世界的真正瑰宝，那个将它与我们想象中的“[完美导体](@keyword=perfect_conductor|lang=zh-CN|style=Feynman)”彻底区分开来的核心特征，却隐藏在它与[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的奇特互动之中。

### 超导，不只是“完美导电”

让我们来做一个思想实验，一个能够揭示超导灵魂的实验。想象我们有两个外观完全相同的圆柱体样品，一个是理论上存在的“理想导体”，它的电阻为完美的零，但仅此而已；另一个则是真正的“[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)”。我们准备用两种不同的方式来探索它们的内心世界。[@problem_id:2840823] [@problem_id:3009512]

第一种方式叫作“[零场冷却](@keyword=zero_field_cooled|lang=zh-CN|style=Feynman)”（Zero-Field-Cooled, ZFC）。我们先把两个样品冷却到它们的“神奇”温度（[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的临界温度 $T_c$）以下，此时它们都处于[零电阻](@keyword=zero_resistance|lang=zh-CN|style=Feynman)状态。然后，我们在外部施加一个均匀的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。结果会怎样？两个样品表现得一模一样：它们内部都会产生[表面电流](@keyword=surface_current|lang=zh-CN|style=Feynman)，形成一个与外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)完全相反的内部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，从而将外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)完美地抵挡在外。它们内部的[磁感应强度](@keyword=magnetic_flux_density|lang=zh-CN|style=Feynman) $B_{\text{in}}$ 将保持为零。这似乎并不意外，法拉第电磁感应定律告诉我们，当[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)变化时，导体会产生[感应电流](@keyword=induced_current|lang=zh-CN|style=Feynman)来抵抗这种变化。对于一个电阻为零的导体，这种抵抗是完美的。

但真正的魔法发生在第二种方式中，我们称之为“场致冷却”（Field-Cooled, FC）。这次，我们先施加一个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，让磁力线穿透两个还处于“正常”状态的样品。所以，在冷却之前，它们内部的[磁感应强度](@keyword=magnetic_flux_density|lang=zh-CN|style=Feynman) $B_{\text{in}}$ 大约等于外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $\mu_0 H_0$。现在，我们保持[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)不变，开始给它们降温。

对于理想导体，当温度降至其电阻变为零的那一刻，它内部的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)会发生什么？根据电磁感应定律，只有当[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)发生 *变化* 时，才会产生[感应电流](@keyword=induced_current|lang=zh-CN|style=Feynman)。在我们的实验中，外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)是恒定的，所以没有任何变化去“命令”理想导体做些什么。结果是，之前已经存在于它内部的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)就被“冻结”或“捕获”在了那里。它的内部将保持着 $B_{\text{in}} \approx \mu_0 H_0$。理想导体的状态，取决于你如何到达那里——它的行为是历史依赖的。

而[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)则完全不同。当它在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中被冷却，跨过临界温度 $T_c$ 的那一刹那，惊人的事情发生了：它开始主动地、自发地将内部的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)“驱逐”出去！就好像这个材料突然对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)产生了洁癖，无法容忍任何磁力线存在于它的体内。最终，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部的[磁感应强度](@keyword=magnetic_flux_density|lang=zh-CN|style=Feynman)也会变为零，$B_{\text{in}} = 0$。这个主动驱逐[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，而不管[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)是何时施加的现象，就是著名的 **迈斯纳-奥克森菲尔德效应（Meissner-Ochsenfeld effect）**。

这个简单的思想实验揭示了一个深刻的真理：超导态并非仅仅是完美导电性所导致的动态结果，它是一个独特的、由[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)决定的 **[平衡态](@keyword=equilibrium_states|lang=zh-CN|style=Feynman)**。无论你走哪条路——先冷却再加场，还是先加场再冷却——只要最终的温度和[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)条件相同，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)总是会到达同一个终点：内部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)为零。这标志着超导是一种全新的物质相，就像水会结成冰一样，是一种由能量决定的、根本性的转变。

### 能量的游戏：为何要排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)？

为什么[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)会如此“费力”地去排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)？毕竟，将[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)从一个空间中排除出去是需要消耗能量的。想象一下，你试图用手推开两个相互吸引的磁铁，这需要做功。一个系统通常会自发地向能量更低的状态演化，那么[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的能量“收益”在哪里呢？[@problem_id:2840873]

这里的关键在于理解[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)中的 **吉布斯自由能（Gibbs free energy）**。当一个系统处于恒定的温度和外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中时，它最稳定的状态就是[吉布斯自由能](@keyword=gibbs_free_energy|lang=zh-CN|style=Feynman)最低的状态。让我们来算一算[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)和普通导体在[磁场中的能量](@keyword=energy_in_magnetic_field|lang=zh-CN|style=Feynman)账单。

一个材料排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，会使它的吉布斯自由能增加，增加的这部分能量密度为 $\frac{1}{2}\mu_0 H_a^2$，其中 $H_a$ 是外部施加的磁场强度。这笔“开销”正是排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)本身所需付出的能量代价。如果只有这笔开销，任何材料都不会自发地排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。[@problem_id:2840873]

但[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的秘密武器在于，当电子配对形成所谓的“库珀对（Cooper pairs）”进入超导态时，系统会释放出一部分能量，我们称之为 **[凝聚能](@keyword=condensation_energy|lang=zh-CN|style=Feynman)（condensation energy）**。这就像是电子们从混乱的单身状态进入了有序的配对生活，整体系统的能量降低了。这部分能量“收益”的密度可以表示为 $-\frac{1}{2}\mu_0 H_c^2(T)$，其中 $H_c(T)$ 就是我们之前提到的 **[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)[临界场](@keyword=critical_fields|lang=zh-CN|style=Feynman)**，它的大小与温度有关。

现在，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的“决策”就变得清晰了。它需要比较排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的“开销”和成为超导态的“收益”。两者之差的能量密度为：
$$ \Delta g = g_s(H_a, T) - g_n(H_a, T) = \frac{1}{2}\mu_0 H_a^2 - \frac{1}{2}\mu_0 H_c^2(T) $$
只要收益大于开销，即 $H_a < H_c(T)$ 时，总能量变化 $\Delta g$ 是负的，系统就会自发地选择进入排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的超导态。一旦外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)强大到 $H_a > H_c(T)$，排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的代价就过于高昂，超导态就会被破坏，材料恢复为普通的正常态。

这个简单的[能量平衡](@keyword=energy_balance|lang=zh-CN|style=Feynman)关系，巧妙地将宏观的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)临界场 $H_c$ 与微观的量子物理联系了起来。根据巴丁-库珀-施里弗（Bardeen-Cooper-Schrieffer, BCS）理论，[凝聚能](@keyword=condensation_energy|lang=zh-CN|style=Feynman)的来源是电子之间通过晶格振动（[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）作为媒介产生的吸引力，它打开了一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta_0$。[凝聚能](@keyword=condensation_energy|lang=zh-CN|style=Feynman)密度可以表示为 $U_0 = \frac{1}{2}N(0)\Delta_0^2$，其中 $N(0)$ 是费米能级处的[电子态密度](@keyword=electronic_density_of_states|lang=zh-CN|style=Feynman)。[@problem_id:2840878] 这意味着，我们可以从测量的宏观临界场 $B_c(0) = \mu_0 H_c(0)$，反推出微观世界里那个至关重要的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)大小：
$$ B_c(0) = \Delta_0 \sqrt{\mu_0 N(0)} $$
宏观与微观，通过如此简洁的公式统一起来，这正是物理学之美的体现。

### [磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)衰减的法则：[伦敦穿透深度](@keyword=london_penetration_depth|lang=zh-CN|style=Feynman)

迈斯纳效应告诉我们[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)被“驱逐”，但这个过程是怎样发生的呢？[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)是在材料表面戛然而止，还是以某种方式逐渐消失的？伦敦兄弟（Fritz and Heinz London）提出的唯象理论为我们描绘了一幅更精细的图景。[@problem_id:2840850]

他们提出的[伦敦方程](@keyword=london_equations|lang=zh-CN|style=Feynman)，本质上描述了超导电子（超流体）对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的一种“刚性”响应。当这些方程与麦克斯韦方程组结合时，我们得到了一个描述[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部[磁感应强度](@keyword=magnetic_flux_density|lang=zh-CN|style=Feynman) $\mathbf{B}$ 的美妙方程：
$$ \nabla^2 \mathbf{B} = \frac{1}{\lambda_L^2} \mathbf{B} $$
这个方程的解告诉我们，[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)并非在表面被突兀地切断，而是以指数形式衰减[渗透](@keyword=permeation|lang=zh-CN|style=Feynman)进[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部。对于一个半无限大的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，其表面的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)为 $B_0$，那么在深入表面距离为 $x$ 的地方，磁场强度为：
$$ B(x) = B_0 \exp\left(-\frac{x}{\lambda_L}\right) $$
这里的 $\lambda_L$ 就是一个至关重要的[特征长度](@keyword=characteristic_length|lang=zh-CN|style=Feynman)，被称为 **[伦敦穿透深度](@keyword=london_penetration_depth|lang=zh-CN|style=Feynman)（London penetration depth）**。它定义了[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)能“侵入”[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的典型距离。在比 $\lambda_L$ 深得多的区域，[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)几乎为零，迈斯纳效应得以体现。

更有趣的是，这个[穿透深度](@keyword=penetration_depth|lang=zh-CN|style=Feynman)不是一成不变的。它与超导电子的密度 $n_s$ 直接相关：$\lambda_L^2 \propto 1/n_s$。根据简单的“二流体模型”，我们可以想象[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中的电子分为“超流”和“正常”两部分。在绝对零度时，所有电子都是超流电子，$n_s$ 最大，$\lambda_L$ 最短。随着温度升高并接近临界温度 $T_c$，越来越多的超流电子“融化”成正常电子，$n_s$ 减小，因此 $\lambda_L$ 变长。这意味着，越热的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，其抵御[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的能力就越弱，[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)能[渗透](@keyword=permeation|lang=zh-CN|style=Feynman)得越深。[@problem_id:233458] 这就给了我们一幅动态的画面：超导性不是一个开关，而是一个随着温度变化的渐变过程。

### [宏观量子态](@keyword=macroscopic_quantum_state|lang=zh-CN|style=Feynman)的舞蹈：相位、涨落与量子化

我们迄今为止的讨论，虽然威力强大，但仍停留在唯象层面。[迈斯纳效应](@keyword=the_meissner_effect|lang=zh-CN|style=Feynman)的根源，植根于一个更深邃的现实：超导态是一个 **[宏观量子态](@keyword=macroscopic_quantum_state|lang=zh-CN|style=Feynman)**。金兹堡-朗道（Ginzburg-Landau, GL）理论让我们得以一窥这个奇妙世界的堂奥。

GL理论引入了一个“[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)” $\psi(\mathbf{r}) = |\psi(\mathbf{r})| e^{i\phi(\mathbf{r})}$，你可以把它想象成整个[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的“集体[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)”。其中，振幅的平方 $|\psi|^2$ 正比于超导电子的密度 $n_s$，而 $\phi(\mathbf{r})$ 则是它的相位。

在这个框架下，迈斯纳效应有了一种惊人的解释：在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部，[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)的载体——[光子](@keyword=photon|lang=zh-CN|style=Feynman)——似乎获得了“质量”。这导致它无法长距离传播，只能在 $\lambda_L$ 的尺度上指数衰减。这个机制与粒子物理中赋予基本粒子质量的[希格斯机制](@keyword=higgs_mechanism|lang=zh-CN|style=Feynman)惊人地相似，再次展现了不同物理学分支之间深刻的内在统一性。[@problem_id:2840849]

而[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的相位 $\phi$，更是引出了一系列纯粹的量子奇观。我们知道，任何一个[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)都必须是单值的，这意味着，如果你绕着一个环路走一圈再回到起点，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的相位变化必须是 $2\pi$ 的整数倍。对于一个中空的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)，这个简单的要求导致了石破天惊的结论：穿过环孔的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi_B$ 必须是量子化的！
$$ \Phi_B = n \frac{h}{q_s} $$
其中 $n$ 是整数，$h$ 是普朗克常数，$q_s$ 是超导载流子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。实验物理学家通过测量这个磁通量的最小单位——[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman) $\Phi_0$——发现它的值是 $h/(2e)$，而不是 $h/e$！[@problem_id:2840849] 这个“2”是无可辩驳的证据，证明了超导电流是由[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为 $2e$ 的物体——即库珀电子对——承载的。一个宏观的量子效应（[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)）直接揭示了微观世界的配对秘密。

### [超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的两种“性格”：I类与II类

有了[凝聚能](@keyword=condensation_energy|lang=zh-CN|style=Feynman)、[穿透深度](@keyword=penetration_depth|lang=zh-CN|style=Feynman)和[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)的概念，我们发现真实世界中的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)并非铁板一块，它们展现出至少两种截然不同的“性格”，这取决于两个内在长度尺度的竞争。[@problem_id:2840802]

第一个是[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)穿透深度 $\lambda$，我们已经很熟悉了。
第二个是 **相干长度（coherence length）** $\xi$。它描述了超导[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman) $|\psi|$ 发生显著变化所需的最小空间尺度，可以理解为库珀对的“尺寸”或者说超导态的“刚度”。

这两个长度的比例，定义了关键的 **[金兹堡-朗道参数](@keyword=ginzburg_landau_parameter|lang=zh-CN|style=Feynman)** $\kappa = \lambda/\xi$。这个参数决定了在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)和正常导体之间的[界面能量](@keyword=interfacial_energy|lang=zh-CN|style=Feynman)是正是负。

- **I类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman) ($\kappa < 1/\sqrt{2}$)**：在这种材料中，相干长度 $\xi$ 比[穿透深度](@keyword=penetration_depth|lang=zh-CN|style=Feynman) $\lambda$ 要长。这意味着超导态“恢复”得很慢，而[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)衰减得很快。这导致正常/超导界面的能量为正。因为系统不喜欢花费能量来制造界面，所以I类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)倾向于将界面面积减至最小。它的行为非常“纯粹”：在低于[临界场](@keyword=critical_fields|lang=zh-CN|style=Feynman) $H_c$ 时，它处于完美的迈斯纳态，完全排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)；一旦超过 $H_c$，它就干脆地完全转变为正常态。它的磁化强度 $M$ 会从 $-H_c$ 突变为0。[@problem_id:2840895]

- **II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman) ($\kappa > 1/\sqrt{2}$)**：这里的情况正好相反，$\lambda$ 比 $\xi$ 长。这使得界面能为负，也就是说，系统反倒“乐于”制造正常/超导界面！这种奇特的性质导致了一种全新的状态——**[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)（mixed state）**。当外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)超过一个较低的[临界场](@keyword=critical_fields|lang=zh-CN|style=Feynman) $H_{c1}$ 时，II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)不再完全排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，而是允许[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)以“磁通涡旋”的形式穿透进来。每个涡旋的中心是一个半径约为 $\xi$ 的正常态“核”，它携带一个[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman) $\Phi_0$。这种状态在能量上比完全排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)或完全变为正常态都更有利。随着[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)继续增强，越来越多的涡旋挤进材料，直到在更高的一个[上临界场](@keyword=upper_critical_field|lang=zh-CN|style=Feynman) $H_{c2}$ 时，所有涡旋的核连成一片，整个材料才最终变为正常态。因此，II类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的磁化曲线要复杂得多：在 $H_{c1}$ 之前是完美的迈斯纳态 ($M=-H$)，之后磁化强度的[绝对值](@keyword=absolute_value|lang=zh-CN|style=Feynman)逐渐减小，连续地趋近于零。[@problem_id:2840895]

我们今天发现的大多数[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，包括所有的高温超导体，都属于II类。正是这种形成磁通涡旋的能力，使得它们能够在极强的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)下依然保持超导特性，这也是它们在[核磁共振](@keyword=nuclear_magnetic_resonance|lang=zh-CN|style=Feynman)（MRI）、[粒子加速器](@keyword=particle_accelerators|lang=zh-CN|style=Feynman)等强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)应用中不可或缺的原因。

### 超越伦敦模型：非定域性的涟漪

最后，让我们像真正的物理学家那样，审视一下我们模型的局限性。伦敦理论假设电流在某一点的响应只取决于同一点的[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)，这是一个“定域”模型。然而，我们知道[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)本身就有一定的空间尺寸，即[相干长度](@keyword=healing_length|lang=zh-CN|style=Feynman) $\xi_0$。因此，更精确的描述（由Pippard首先提出）应该考虑到这一点：在某一点的电流，实际上取决于其周围 $\xi_0$ 范围内所有点的[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)的平均效果。这被称为 **非定域（nonlocal）** 响应。[@problem_id:2840838]

这种非定域性意味着，对于那些空间变化波长比 $\xi_0$ 短的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)分量，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的屏蔽效果会变差。这会修正纯指数衰减的简单图像，使得靠近表面的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)分布变得更加复杂。

从一个简单的“完美导电+迈斯纳效应”的图像出发，我们经过了能量、唯象理论、[宏观量子态](@keyword=macroscopic_quantum_state|lang=zh-CN|style=Feynman)和材料分类的旅程，最后来到了非定域性的前沿。每一步，我们的理解都更加深刻和精细。这正是科学的魅力所在：它不是一套僵化的教条，而是一个不断演进、自我完善的探索过程，引领我们一步步接近自然的真相。