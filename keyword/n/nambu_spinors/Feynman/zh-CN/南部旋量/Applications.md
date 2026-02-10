## 应用与跨学科联系

在上一章中，我们介绍了一个奇特的数学工具：[南部旋量](@keyword=nambu_spinors|lang=zh-CN|style=Feynman)。乍一看，它可能仅仅像一个巧妙的记账技巧，一种将电子[产生和湮灭算符](@keyword=creation_and_annihilation_operators|lang=zh-CN|style=Feynman)方便地分组，使一个纠缠的哈密顿量看起来整洁可解的方法。如果仅此而已，它将是一个有用但或许平淡无奇的工具。但在物理学中，一个真正好的技巧从来不*仅仅*是一个技巧。它是通往现实的新窗口。[南部旋量](@keyword=nambu_spinors|lang=zh-CN|style=Feynman)让我们看到的相互作用电子世界，不是由粒子及其缺失（空穴）构成的，而是由一种新的、幽灵般的实体构成的：Bogoliubov [准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，一个部分是粒子、部分是空穴的量子力学嵌合体。

本章是一次通过这扇新窗户看世界的旅程。我们将发现，这个奇特的视角并非学术上的好奇心，而是揭开现代科学中一些最深刻、最活跃研究领域现象秘密的关键。我们将看到它如何以惊人的清晰度解释了数十年来超导性的谜团，以及它现在如何成为新一代[量子技术](@keyword=quantum_technology|lang=zh-CN|style=Feynman)的设计蓝图。

### 看见[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)：超导性的标志

这种方法第一个也是最著名的成功在于传统[超导理论](@keyword=superconductivity_theory|lang=zh-CN|style=Feynman)。在 Bardeen-Cooper-Schrieffer (BCS) 理论之前，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的一个决定性属性——在临界温度以下电阻完全消失——是一个深刻的谜。BCS 哈密顿量的南部表示法直击问题的核心 ([@problem_id:1177474])。该形式论揭示，在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，费米能级附近的电子会结合成库珀对。要激发系统，你不能再仅仅轻推一个电子。相反，你必须打破一个库珀对，这需要一定的能量。这将产生两个 Bogoliubov [准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。完成此过程的最小能量就是著名的超导能隙，$\Delta$。

在南部语言中，这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)允许的能谱非常简单：$E_k = \sqrt{\xi_k^2 + |\Delta|^2}$，其中 $\xi_k$ 是电子相对于费米能级的能量。这个方程讲述了一个强有力的故事。对于一个远低于[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)（$\xi_k$ 是大的负数）的普通电子，[准粒子能量](@keyword=quasiparticle_energies|lang=zh-CN|style=Feynman) $E_k$ 就是 $|\xi_k|$，其行为像一个正常的空穴。远高于[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)时，它行为像一个正常的电子。但在 $\xi_k \approx 0$ 的费米能级附近的关键区域，一个大小为 $2|\Delta|$ 的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)打开了。在这个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)内不允许任何单粒子激发。

这不仅是理论预测；它也是一个可以通过惊人直接的方式观察到的实验事实。其中最强大的工具之一是[角分辨光电子能谱](@keyword=arpes|lang=zh-CN|style=Feynman)（ARPES）。你可以把 [ARPES](@keyword=arpes|lang=zh-CN|style=Feynman) 看作材料中电子的一种量子照相亭：你用高能[光子](@keyword=photon|lang=zh-CN|style=Feynman)照射样品，将电子敲出。通过测量这些射出电子的能量和动量，你可以重建电子在内部的能量-动量关系——即[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman)。

当对[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)进行 [ARPES](@keyword=arpes|lang=zh-CN|style=Feynman) 实验时，它揭示了对 Bogoliubov [准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)图像的壮观证实 ([@problem_id:2988266])。测量到的占据态的[色散关系](@keyword=dispersion_relations|lang=zh-CN|style=Feynman)不是一条简单的曲线，而是“向后弯曲”。动量小于[费米动量](@keyword=fermi_momentum|lang=zh-CN|style=Feynman) $k_F$ 的电子具有正速度，但当其动量增加超过 $k_F$ 时，其速度变为*负*，然后再转弯。这种“后弯”是[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)双重性质的独特指纹。南部-格林函数形式论精确预测了这种行为，甚至通过所谓的“[相干因子](@keyword=coherence_factors|lang=zh-CN|style=Feynman)” $u_k^2$ 和 $v_k^2$ 告诉我们 [ARPES](@keyword=arpes|lang=zh-CN|style=Feynman) 信号的强度，这些因子衡量了[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)中的电子和空穴成分。在这个实验中，抽象的[南部旋量](@keyword=nambu_spinors|lang=zh-CN|style=Feynman)及其混合[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)以壮观的方式得以呈现。

### 变成空穴的粒子：安德烈夫反射

[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中激发的粒子-空穴特性导致了在其边界处另一个奇异而美妙的现象。如果你试图从正常金属向[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)发送一个电子会发生什么？如果电子的能量 $E$ 小于[能隙能量](@keyword=bandgap_energy|lang=zh-CN|style=Feynman) $\Delta$ ，它似乎无处可去——[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部没有可用的态。

南部形式论给出了令人惊讶的答案：电子进入了，但只能通过从金属中抓取另一个电子并形成库珀对的方式进入。为了守恒[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，这个过程必须留下一个电子的亏损——换句话说，一个空穴。但这不仅仅是任何空穴。它是一个“[逆反射](@keyword=retroreflection|lang=zh-CN|style=Feynman)”的空穴，一个沿着入射电子所走的确切路径返回的空穴 ([@problem_id:2969727])。这个过程被称为安德烈夫反射。入射电子在界面处被转换成反射的空穴。

这不仅仅是一次简单的反射。从粒子到反粒子（空穴）的转换伴随着一个非常具体、依赖于能量的相移，由优美的公式 $\phi_A(E) = -\arccos(E/\Delta)$ 给出。这个相移并非次要细节；它是界面的一个基本属性，支配着由[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)制成的量子器件（如[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)和干涉仪）的行为。[南部旋量](@keyword=nambu_spinors|lang=zh-CN|style=Feynman)描述从一开始就平等地对待粒子和空穴，使得这个奇怪反射过程的起源看起来几乎是自然的。

### 寻找马约拉纳：在物质中设计拓扑

到目前为止，我们已经用[南部旋量](@keyword=nambu_spinors|lang=zh-CN|style=Feynman)出色地解释了观察到的现象。但其最大的力量可能在于其预测能力，作为创造全新[物态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)的设计工具。这将我们带到了物理学中最激动人心的前沿之一：寻找[马约拉纳费米子](@keyword=majorana_fermions|lang=zh-CN|style=Feynman)。

在基本[粒子物理学](@keyword=particle_physics|lang=zh-CN|style=Feynman)中，[马约拉纳费米子](@keyword=majorana_fermions|lang=zh-CN|style=Feynman)是其自身的[反粒子](@keyword=antiparticles|lang=zh-CN|style=Feynman)的粒子。虽然它们在[时空](@keyword=space_time|lang=zh-CN|style=Feynman)真空中的存在仍然是假设性的，但凝聚态物质的世界提供了一种类似的可能性。Bogoliubov [准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)是电子和空穴的叠加。如果我们能够设计一种情况，使得这种叠加是完美平衡的——一个恰好是半电子半空穴的状态呢？这样一个状态 $\gamma$ 将满足条件 $\gamma = \gamma^\dagger$，使其成为自身的[反粒子](@keyword=antiparticles|lang=zh-CN|style=Feynman)。这就是马约拉纳[零能模](@keyword=zero_energy_mode|lang=zh-CN|style=Feynman)（MZM）。

南部框架是阐述这一探索的完美语言。Alexei Kitaev 在一个惊人简单的“玩具模型”中奠定了蓝图 ([@problem_id:2869427])。想象一根一维的无自旋[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)线，其中配对发生在相邻位点之间（一种“p波”[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)）。用南部基底写出的该系统的 BdG 哈密顿量揭示了一些非凡的东西。通过简单地调整像化学势 $\mu$ 这样的参数，人们可以驱动系统经历一次从“平庸”绝缘态到“拓扑”超导态的量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)。

是什么让这个新相“拓扑”？它拥有一个非凡的性质：虽然线的体材料有一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，但其端点被迫承载一个能量恰好为零的态 ([@problem_id:1124308])。原因是对称性的一个美丽结果。[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的南部哈密顿量具有内在的[粒子-空穴对称性](@keyword=particle_hole_symmetry|lang=zh-CN|style=Feynman)，这决定了如果存在一个能量为 $E$ 的态，就必须存在一个能量为 $-E$ 的伙伴态。但是线端的态是独特的且空间孤立的；它没有伙伴。一个态成为自身伙伴的唯一方式是其能量是自身的负数：$E = -E$，这意味着 $E=0$。这就是马约拉纳[零能模](@keyword=zero_energy_mode|lang=zh-CN|style=Feynman)，一个被系统拓扑结构固定在零能量的态！

这个深刻的思想将凝聚态物理与量子[场论](@keyword=field_theory|lang=zh-CN|style=Feynman)的深奥概念联系起来。Kitaev 链在[拓扑相变](@keyword=topological_phase_transition|lang=zh-CN|style=Feynman)附近的 BdG 哈密顿量可以直接映射到一维狄拉克方程，即支配电子的[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)方程 ([@problem_id:3004011])。在这个映射中，化学势扮演了一个空间变化的“质量”的角色。线的末端是这个质量改变符号的[畴壁](@keyword=domain_walls|lang=zh-CN|style=Feynman)。Roman Jackiw 和 Claudio Rebbi 在 1976 年的一项著名定理指出，[狄拉克方程](@keyword=dirac_equation|lang=zh-CN|style=Feynman)中的这样一个质量[畴壁](@keyword=domain_walls|lang=zh-CN|style=Feynman)必须捕获一个单一、稳健的[零能模](@keyword=zero_energy_mode|lang=zh-CN|style=Feynman)。因此，一个来自粒子物理学的定理保证了超导线末端[马约拉纳模](@keyword=majorana_modes|lang=zh-CN|style=Feynman)的存在！

### 从玩具模型到实验室

Kitaev 模型很美，但无自旋的 p 波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)并非现成的。在这里，南部形式论的预测能力成为实验物理学家的实用指南。我们如何用常见材料*工程化*一个有效的 p 波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)？

目前，两个主要提议（均使用南部语言表述）指导着全球的实验努力。
- 一个想法是取一根具有强[自旋轨道](@keyword=spin_orbitals|lang=zh-CN|style=Feynman)耦合（一种将电子自旋与其运动联系起来的相互作用）的[半导体纳米线](@keyword=semiconductor_nanowire|lang=zh-CN|style=Feynman)，将其置于传统 s 波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的近邻，并施加一个强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) ([@problem_id:160597])。这个分析需要完整的四分量[南部旋量](@keyword=nambu_spinors|lang=zh-CN|style=Feynman)（包括自旋）。令人难以置信的是，由此产生的 BdG 哈密顿量表明，这种成分的组合有效地模仿了 Kitaev 链的物理特性，并预计在其末端承载马约拉纳[零能模](@keyword=zero_energy_mode|lang=zh-CN|style=Feynman)。
- 另一条路径始于一种不同的奇异材料，一种拓扑绝缘体，其边缘自然地承载着自旋和动量锁定在一起的“[螺旋性](@keyword=helicity|lang=zh-CN|style=Feynman)”电子。将这样的边缘与 s 波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)近邻接触，也被预测会产生一个拓扑超导态 ([@problem_id:3012535])。

这些想法不仅限于一维线。在二维[拓扑超导体](@keyword=topological_superconductors|lang=zh-CN|style=Feynman)中，马约拉纳[零能模](@keyword=zero_energy_mode|lang=zh-CN|style=Feynman)可以被困在材料内部形成的[量子涡旋](@keyword=quantum_vortices|lang=zh-CN|style=Feynman)中，就像飓风眼中的空气一样 ([@problem_id:1269179])。这些被困的模可以通过外部场来探测；例如，预测旋转整个系统会使马约拉纳的能量随角速度成比例移动，$E = -\hbar\Omega$。

这项全球研究的最终、诱人的目标是实现一个拓扑量子计算机。传统的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)（qubit）是一个脆弱的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，容易受到环境噪声的退相干影响。然而，一个[拓扑量子比特](@keyword=topological_qubit|lang=zh-CN|style=Feynman)将非局域地编码在一对[空间分离](@keyword=spatial_separation|lang=zh-CN|style=Feynman)的马约拉纳[零能模](@keyword=zero_energy_mode|lang=zh-CN|style=Feynman)中。信息将存储在它们的共享状态中，而不是任何局域属性中，使其本质上对局域干扰具有鲁棒性。在[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中编织这些[马约拉纳模](@keyword=majorana_modes|lang=zh-CN|style=Feynman)将执行[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)。

我们在本章中所走的旅程是非凡的。我们从一个数学上的便利——[南部旋量](@keyword=nambu_spinors|lang=zh-CN|style=Feynman)——开始。这引导我们到一个新的物理图像——Bogoliubov [准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。这个图像让我们以新的眼光看待[超导能隙](@keyword=superconducting_gap|lang=zh-CN|style=Feynman)和安德烈夫反射等熟悉的现象。最后，它已成为设计可能有一天为稳健[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机提供动力的新拓扑[物态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)的理论基石。这是一个有力的证明，说明找到描述世界的正确语言，反过来，可以赋予我们改变世界的力量。