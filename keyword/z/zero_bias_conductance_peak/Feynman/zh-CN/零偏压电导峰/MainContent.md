## 引言
在超冷材料的量子世界中，[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)测量为我们提供了一扇窥探电子微观世界的窗口。对于[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，我们通常[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)在低能量处发现一个[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)为零的“谷”，这是[超导能隙](@keyword=superconducting_gap|lang=zh-CN|style=Feynman)的直接结果。然而，在特定条件下，一个令人费解的现象发生了：一个尖锐的[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)*峰*恰好出现在零偏压处。这个“[零偏压电导峰](@keyword=zero_bias_conductance_peak|lang=zh-CN|style=Feynman)”（ZBCP）完全颠覆了简单的预期，标志着非同寻常的量子力学效应正在发挥作用。

本文将揭开 ZBCP 的奥秘。我们将首先探讨该峰背后的“原理与机制”，重点关注[非常规超导体](@keyword=unconventional_superconductors|lang=zh-CN|style=Feynman)中优美的安德烈夫反射理论，并将其与其他可能的原因进行对比。随后，“应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系”一节将展示物理学家如何利用 ZBCP 这一强大工具来探测奇异[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的性质、寻找难以捉摸的马约拉纳费米子，以及诊断近藤效应中复杂的的[多体相互作用](@keyword=many_body_interaction|lang=zh-CN|style=Feynman)。我们的探索始于一个基本问题：在原本预期是空谷的地方，是什么物理过程能够创造出一座态的“山峰”？

## 原理与机制

那么，我们面临一个谜题。我们的引言已经暗示了一种奇异而优美的现象，称为**[零偏压电导峰](@keyword=zero_bias_conductance_peak|lang=zh-CN|style=Feynman) (ZBCP)**。要真正理解它为何如此引人注目，我们首先需要了解当我们探测[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的电子世界时，我们*[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)*看到什么。想象一下，你是一位物理学家，拥有一根极细的探针——[扫描隧道显微镜](@keyword=scanning_tunneling_microscope|lang=zh-CN|style=Feynman)——它可以在不同的外加电压下测量电子的流动，即**隧穿[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)**。在极低的温度下，这种[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)可以完美地映射出材料中可用的电子态，这一属性我们称之为**态密度 (DOS)**。

### 消失的态之谷

对于一个普通的，或称**常规的 s 波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)**，情况简单而优雅。在[临界温度](@keyword=critical_temperature|lang=zh-CN|style=Feynman)以下，电子配对形成**[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)**，在此过程中打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta$。这个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)就像能量景观中的一个禁区；任何单电子态都无法存在于其中。如果我们测量[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)，会发现对于任何满足 $|eV| < \Delta$ 的外加电压 $V$，[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)绝对为零。这是一个平坦、空旷的谷。只有当我们提供足够的能量来打破一个[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)，即在 $|eV| = \Delta$ 时，[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)才会突然飙升，在谷的边缘形成尖锐的“相干峰”。

但并非所有[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)都如此简单。例如，高温[铜氧化物](@keyword=cuprates|lang=zh-CN|style=Feynman)是**非常规的 d 波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)**。它们的特点是具有更复杂、各向异性的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。可以这样想：[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)不再是电子沿任何方向传播时都相同，而是取决于电子动量 $\mathbf{k}$ 的方向。至关重要的是，在一些特殊方向上，即所谓的**节点**，[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta(\mathbf{k})$ 会收缩至恰好为零。

现在，我们的隧穿实验能看到什么呢？由于实验通常是对所有方向进行平均，这些节点会产生深远的影响。不再有单一的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)需要克服。在任意低的能量，甚至低至零能量处，都存在着电子态。结果是，态密度在低能量处不再为零。相反，详细的计算告诉我们它随能量线性增长，$N_s(E) \propto |E|$。这意味着[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)不再是一个平底谷，而是一个完美的 V 形，在零偏压处下降到一个尖锐的最小值——但不是平坦的零点 [@problem_id:1821820] [@problem_id:2988201]。

而这正是谜题的核心所在。**“[零偏压电导峰](@keyword=zero_bias_conductance_peak|lang=zh-CN|style=Feynman)”**这个名字本身就告诉我们，在某些条件下，我们找到的不是一个谷（无论是平底的还是 V 形的），而是一座山——一个尖锐的[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)*峰*，恰好出现在我们预期是最小值的地方。这不是一个微小的效应，而是对我们简单预期的彻底颠覆。它告诉我们，表面正在发生一些新奇而非凡的事情。

### 魔镜与 π [相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)

我们故事的主角是一种被称为**安德烈夫反射**的现象。在正常金属和[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的界面处，一个能量小于[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta$ 的电子不能简单地进入[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。相反，它可以被反射为一个空穴——其类似反物质的对应物——同时一个[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)被注入[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。这不是普通的反射；这是一个转变过程，在这个过程中，超导序参量 $\Delta(\mathbf{k})$ 的相位会印刻在被反射的粒子上。

现在，让我们回到我们的 d 波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman) $\Delta(\mathbf{k})$ 不仅仅是一个数值大小；它还有一个符号（一个 $0$ 或 $\pi$ 的相位）。对于[铜氧化物](@keyword=cuprates|lang=zh-CN|style=Feynman)中常见的 $d_{x^2-y^2}$ 对称性，[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)沿晶体的 $x$ 和 $y$ 轴为正，沿对角线方向为负。

想象一下，我们沿着一个特定的对角线，即所谓的 **(110) 表面**切割晶体。这个表面就像一面魔镜 [@problem_id:2828354]。一个[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)从[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部以动量 $\mathbf{k}_{\text{in}}$ 接近表面。假设它行进的方向上[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta(\mathbf{k}_{\text{in}})$ 为正。当它从这个 (110) 表面镜面反射时，它的新动量 $\mathbf{k}_{\text{out}}$ 指向一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)为负的方向。也就是说，$\Delta(\mathbf{k}_{\text{out}}) = -\Delta(\mathbf{k}_{\text{in}})$。[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)在反射时，其感知到的世界发生了突然的符号反转——一个 $\pi$ 的完美[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)。

这个[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)是关键。一个在反射时获得 $\pi$ 相位的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)可以与自身发生相长干涉。这种相长干涉将[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)束缚在表面，形成一个特殊的、由[电子和空穴](@keyword=electrons_and_holes|lang=zh-CN|style=Feynman)完美叠加而成的态。这个过程的数学推导异常优美：唯一能满足这种完美的相长干涉条件的能量，恰好是零能量 [@problem_id:2988217] [@problem_id:2861941] [@problem_id:3012865]。

这就产生了一种被称为**零能安德烈夫束缚态 (ABS)** 的东西。而且因为这个条件对很大范围内的入射角都成立，而不仅仅是某一个角度，所以大量的态都聚集在这一个能级上。在某一能量处的大量态的累积，正是一个[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)峰。而在零能量处的态密度峰，也正是在我们的隧穿实验中测量到的[零偏压电导峰](@keyword=zero_bias_conductance_peak|lang=zh-CN|style=Feynman)。山峰出现在了山谷中，我们现在理解了它的“地质”成因：它是一座由态构成的“火山峰”，由[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)在符号改变的界面上反射并发生[相长干涉](@keyword=constructive_interference|lang=zh-CN|style=Feynman)而形成。

这个解释还给了我们一个至关重要的预测：ZBCP 应该对[表面取向](@keyword=surface_anchoring|lang=zh-CN|style=Feynman)高度敏感。如果我们换作沿 (100) 表面切割晶体，“魔镜”效应就会消失。反射不再引起[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的符号改变，[相长干涉](@keyword=constructive_interference|lang=zh-CN|style=Feynman)的条件无法满足，没有零能态形成，我们看到的会是通常的 V 形[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，而不是峰 [@problem_id:2828354]。这种取向依赖性已在实验中得到了精美的验证，让我们对这一图像充满信心。

### 检验峰的脆弱性

一个稳健的科学理论不仅能解释，还能预测。而最有趣的预测往往涉及试图打破这种现象。如果我们扰动这个完美的系统会发生什么？

首先，如果我们的“魔镜”不是完全光滑的呢？[表面粗糙度](@keyword=surface_roughness|lang=zh-CN|style=Feynman)和缺陷会引入散射，破坏[束缚态](@keyword=bound_states|lang=zh-CN|style=Feynman)所需的精细的[相位相干性](@keyword=phase_coherence|lang=zh-CN|style=Feynman)。这种“[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)”使得[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的寿命变为有限。在量子力学中，有限的寿命意味着态的能量不再是完美精确的。零能态会展宽成一个称为[洛伦兹分布](@keyword=lorentzian_distribution|lang=zh-CN|style=Feynman)的形态。结果是，ZBCP 变得更低更宽。人们发现峰的高度与[散射率](@keyword=scattering_rates|lang=zh-CN|style=Feynman) $\Gamma$ 成反比。表面越干净，峰就越高越尖 [@problem_id:3023157]。这一点也与我们在实验室中看到的相符。

其次，如果我们在平行于表面的方向施加一个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)会发生什么？众所周知，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)会排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，它通过在表面附近建立起屏蔽电流——一种[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的流动——来实现这一点。这种超流产生了一种[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)能感受到的“[以太风](@keyword=aether_wind|lang=zh-CN|style=Feynman)”。顺着风运动的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)会获得能量上的多普勒[蓝移](@keyword=blueshift|lang=zh-CN|style=Feynman)，而逆风运动的则会获得[红移](@keyword=redshift|lang=zh-CN|style=Feynman)。这对我们的零能态产生了显著的影响。原来包含两个方向运动的态的单个峰，会分裂成两个独立的峰，对称地分布在零偏压两侧，能量为 $\pm \delta E$。这个分裂的大小 $\delta E$ 与磁场强度成正比。观察到这种分裂，是安德烈夫束缚态图像的又一个有力证明 [@problem_id:3009552]。

### 另一个嫌疑犯：杂质的共振

在我们宣布结案之前，一个优秀的科学家必须考虑所有可能性。还有没有其他方法可以在零偏压处获得增强的[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)呢？事实证明是有的。

让我们回到 d 波能隙的性质。它的符号改变特性是关键。想象一下，我们在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)体材料内部放置一个单一的、强的、非磁性杂质原子。[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)可以在这个杂质上发生散射。由于[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)在[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上会改变符号，杂质可以轻易地将[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)从一个具有正[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的态散射到一个具有负[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的态。这种散射是“对破坏性的”，并且具有很强的破坏作用。事实上，一个强杂质可以像一个[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的共振腔，将一个态局域在它周围。就像表面一样，这种机制可以创造一个非常接近零能量的**共振态** [@problem_id:2988237]。

这带来了一个有趣的难题。如果我们在实验中看到了 ZBCP，它究竟是一个真正的表面安德烈夫态，还是由于我们测量位置恰好有一个表面杂质原子造成的？这是一个该领域中真实存在的争论，例如在研究[超导涡旋](@keyword=superconducting_vortices|lang=zh-CN|style=Feynman)核心内部的电子态时。我们如何扮演侦探，区分这两个“罪魁祸首”？

答案在于识别它们独特的“指纹” [@problem_id:3009585]：

-   **位置，位置，位置：** 安德烈夫[束缚态](@keyword=bound_states|lang=zh-CN|style=Feynman)是表面（或涡旋）的属性。如果涡旋移动，ABS 也会随之移动。而杂质态则被钉扎在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中的特定原子上。无论周围的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)发生什么变化，它都会待在原地。
-   **[空间分布](@keyword=spatial_distribution|lang=zh-CN|style=Feynman)特征：** 杂质共振具有一种典型的、高度结构化的、原子尺度的空间图案——通常是与晶轴对齐的“四叶草”形状。而[表面态](@keyword=surface_states|lang=zh-CN|style=Feynman)通常更平滑，其尺寸由[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的一个基本长度尺度——[相干长度](@keyword=healing_length|lang=zh-CN|style=Feynman) $\xi$ 决定，这个尺度通常远大于单个原子。
-   **剂量：** 表面态的数量由表面本身决定。但如果杂质是原因，那么向材料中故意添加更多杂质应该会增加我们观察到的 ZBCP 的数量。

通过设计实验来检验这些微妙但关键的差异，物理学家可以区分这些优美的现象。[零偏压电导峰](@keyword=zero_bias_conductance_peak|lang=zh-CN|style=Feynman)的故事完美地诠释了科学过程的运作：一个意外的观察引出了一个优美的理论解释，这又带来了一系列新的预测和对量子世界更深刻、更精确的理解。