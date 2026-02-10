## 引言
在广袤的材料世界中，大多数材料被清晰地归类为阻碍电子流动的绝缘体，或让电子自由传导的金属。然而，在这两个极端之间，存在着一个引人入胜的中间世界：[半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)。在这些材料中，主导电子行为的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)以独特且具有拓扑意义的方式接触，创造出一种新的[量子物态](@keyword=quantum_state_of_matter|lang=zh-CN|style=Feynman)。其中最令人着迷的当属歪尔半金属。这些晶体如同一个凝聚态物质的宇宙，其中涌现出近一个世纪前在[高能物理学](@keyword=particle_physics|lang=zh-CN|style=Feynman)中被理论预言、但从未被作为基本粒子观测到的[无质量粒子](@keyword=massless_particles|lang=zh-CN|style=Feynman)。

本文将探讨围绕这一奇异[物态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)的基本问题：这些材料是如何形成的？它们的决定性特征是什么？为什么它们能够激发跨学科物理学家的想象力？我们将探索一个奇妙的世界：在这里，晶体的内部几何结构孕育出行为如同没有质量的粒子；在这里，被称为[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)的超凡电子高速公路横跨材料表面；在这里，曾一度局限于[宇宙学理论](@keyword=cosmology_theories|lang=zh-CN|style=Feynman)的现象，如今可以在实验室的工作台上被测量。

为了引导我们的探索，本文分为两个主要部分。在第一章 **原理与机制** 中，我们将深入歪尔[半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)的理论核心，揭示它们如何从对称性破缺中诞生，并剖析定义它们的歪尔点的结构。在第二章 **应用与跨学科联系** 中，我们将连接理论与现实，讨论证明它们存在的实验特征、它们所催生的新奇电子与光学效应，以及它们与[粒子物理学](@keyword=particle_physics|lang=zh-CN|style=Feynman)乃至更广阔领域的深刻联系。

## 原理与机制

想象你是一位物理学家，但你凝视的不是星空，而是晶体的核心。你看到的世界并非由原子整齐[排列](@keyword=permutation|lang=zh-CN|style=Feynman)的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)构成，而是一个隐藏的能量景观宇宙，一片决定电子如何漫游的丘陵与山谷。在我们所熟知的大多数材料中，比如绝缘体，存在着一片广阔的禁区——[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，它将电子安然栖息的低能山谷（价带）与它们为导电而攀登的高能山丘（导带）分离开来。在金属中，这些区域重叠，电子形成一片汪洋大海，可以自由徜徉。

但是，大自然以其无穷的创造力，塑造出一些材料，在其中这些能量景观以最奇特、最美妙的方式接触。这些就是半金属，而这些接触点的几何形状定义了它们的本质。

### 晶体的电子动物园

思考两个表面可以接触的方式。它们可以沿一条线相遇，也可以只在一个点上接触。晶体内部的电子[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)也能做到同样的事情。有时，[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)和导带在抽象的动量空间中沿着一个连续的一维环或线相遇。我们称这种材料为**[节线半金属](@keyword=nodal_line_semimetals|lang=zh-CN|style=Feynman)**。

然而，更常见的情况是，[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)仅在离散、孤立的点上接触。这些“节点”是导带世界与[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)世界之间的门户，它们主要有两种类型。如果[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)遵循某些[基本对称性](@keyword=fundamental_symmetries|lang=zh-CN|style=Feynman)——即当时间倒流（**[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)**，$T$）和当观察其关于某点的镜像（**空间[反演对称性](@keyword=inversion_symmetry|lang=zh-CN|style=Feynman)**，$P$）时，其物理规律保持不变——这些接触点可以形成四重简并。这意味着四个不同的电子态在动量空间中的这一个点上共享相同的能量。我们称之为一个**狄拉克点**，这种材料则为**[狄拉克半金属](@keyword=dirac_semimetals|lang=zh-CN|style=Feynman)**，例如众所周知的砷化镉（$\text{Cd}_3\text{As}_2$）和铋化钠（$\text{Na}_3\text{Bi}$）[@problem_id:1827864]。

但如果我们打破这些神圣的对称性之一，会发生什么？如果材料由于磁性或缺少[对称中心](@keyword=center_of_inversion|lang=zh-CN|style=Feynman)，不再同时遵守 $T$ 和 $P$ 对称性，又会怎样？四重简并裂解了。[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)分裂成一对更基本、更稳固的实体：**歪尔点**。每个歪尔点是一个简单的二重简并，即只有两个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)接触的地方。这里就是**歪尔半金属**的核心地带 [@problem_id:1827877]。

### 歪尔点的诞生：一个关于[对称性破缺](@keyword=symmetry_breaking|lang=zh-CN|style=Feynman)的故事

[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)与歪尔点之间的关系是现代物理学中最优雅的故事之一。你可以把一个狄拉克点想象成两个具有相反特性或**手性**的歪尔点，在[时间反演](@keyword=time_reversal_2|lang=zh-CN|style=Feynman)和空间反演对称性的共同作用下，被迫叠加在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)的同一点上。

要创造一个歪尔半金属，你必须扮演一个微观雕塑家的角色，打破这个对称性的牢笼。你有两个选择。你可以引入磁性来打破[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)，这就像为电子设定了一个不同的“时间之矢”。或者，你可以使用一种天然缺少对称中心的晶体，比如砷化钽（TaAs）家族的晶体，从而打破空间[反演对称性](@keyword=inversion_symmetry|lang=zh-CN|style=Feynman) [@problem_id:1827864]。任何一种操作都像松开了一个门闩。两个歪尔点最终获得自由，在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中相互滑离。一个[狄拉克半金属](@keyword=dirac_semimetals|lang=zh-CN|style=Feynman)就转变成了一个歪尔半金属 [@problem_id:1827852]。

这不仅仅是理论上的奇想。人们可以想象，取一种普通绝缘体并施加压力。当你挤压它时，价带和导带之间的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)可能会缩小。如果你调节得恰到好处，在某个[临界压力](@keyword=critical_pressure|lang=zh-CN|style=Feynman) $P_c$ 下，[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)会闭合为零。在这一刻，[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)接触了。如果你再稍微用力挤压，[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)可能会[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)并重新打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，但此时材料的拓扑性质已经变得不同。正是在这个转变点，或者在合适的材料中稍微超过这个点，成对的歪尔点就可以从真空中诞生，这是一个量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)进入新物态的直接标志 [@problem_id:1827844]。

### 剖析歪尔点：固体中的[无质量粒子](@keyword=massless_particles|lang=zh-CN|style=Feynman)

那么，一个歪尔点究竟有何特别之处？如果我们放大其中一个点，会发现[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)形成了一个完美的、陡峭的圆锥。电子的能量与其偏离节点的动量呈线性关系：$E = \pm \hbar v_F |\boldsymbol{k}|$。这是一个惊人的发现，因为这恰恰是[无质量粒子](@keyword=massless_particles|lang=zh-CN|style=Feynman)（如[光子](@keyword=photon|lang=zh-CN|style=Feynman)）的能量-动量关系！当然，电子本身并非无质量。但是它们在晶体内部的集体行为——即**[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)**——表现得如同无质量的相对论性粒子，特别是歪尔[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)。这些[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)最初在高能物理学中被理论预言，但从未被观测到是基本粒子。歪尔半金属就是一个晶体中的宇宙，让这些难以捉摸的实体得以呈现。

这种[线性色散关系](@keyword=linear_dispersion_relation|lang=zh-CN|style=Feynman)带来了深刻且违反直觉的后果。在普通金属中，费米面——被占据电子态的边界——是一个大的二维表面。但在一个理想的、未掺杂的歪尔[半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)中，[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)恰好位于圆锥的顶点。此时，“[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)”缩小为一组零维的点！[@problem_id:1827861]。这意味着**[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)**——可用的电子“停车位”数量——在费米能级处为零，并随着能量偏离节点而按 $E^2$ 增长 [@problem_id:1827820]。

这就提出了一个绝妙的难题。如果在[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)处没有可用的态，这种材料如何能够导电呢？答案在于方程的另一部分：速度。线性[色散](@keyword=frequency_dispersion|lang=zh-CN|style=Feynman)意味着这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的群速度 $v_g = \partial E / \partial(\hbar k)$ 是一个很大的常数 $v_F$，与能量无关。因此，尽管在节点处几乎没有载流子，但它们以非常高且固定的速度移动。这种高迁移率足以弥补态的缺失，即使在绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)下也能产生一个有限的、非零的最小电导率 [@problem_id:1827828]。这是稀缺性与效率之间一种美妙的平衡。

有趣的是，大自然还有进一步的转折。歪尔锥并非总是完美竖直的。如果它们因晶体的特性而被强烈倾斜，甚至可能翻倒。在这种情况下，我们称之为**第二类歪尔[半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)**，节点能量处的费米面不再是一个点，而是一对接触的电子和空穴口袋。其基本拓扑性质是相同的，但对外场的响应却截然不同 [@problem_id:1827824]。

### 不可分割的纽带：拓扑与[表面态](@keyword=surface_states|lang=zh-CN|style=Feynman)的保证

或许，歪尔半金属最惊人的特征不在于其体态，而在于其表面。每个歪尔点在动量空间中都像一个称为**[贝里曲率](@keyword=berry_curvature|lang=zh-CN|style=Feynman)**的量的源或汇。我们为每个点赋予一个“手性”，即**手性荷**（$\chi = \pm 1$），它是一种[拓扑荷](@keyword=topological_charge|lang=zh-CN|style=Feynman)。就像你不能在没有南极的情况下拥有一个磁北极一样，你也不能创造或摧毁单个歪尔点。它们受到[拓扑保护](@keyword=topological_protection|lang=zh-CN|style=Feynman)，必须总是成对出现或湮灭，且手性相反。

材料体态的这种深刻[拓扑性质](@keyword=topological_property|lang=zh-CN|style=Feynman)为其表面带来了一个不可违背的承诺。这就是著名的**[体-边对应](@keyword=bulk_edge_correspondence|lang=zh-CN|style=Feynman)**。三维体态中这些分离的歪尔点的存在，必然要求在二维表面上存在奇特的电子态。这些不是普通的表面态。当你绘制出它们的图像时，你找不到普通二维金属那种闭合的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)环路。相反，你会发现奇异的、开放的电子态线，称为**[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)**。这些弧是电子的超凡高速公路，连接着体歪尔点在表面上相反手性的投影。

想象你有两种材料，一种是歪尔[半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)（A），另一种是平庸[半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)（B）。在 B 的表面，你看到一个正常的、闭合的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)环路。在 A 的表面，你看到这些奇怪的、不连续的[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)。现在，如果你试图污染表面，比如说在上面沉积一层薄的绝缘层，会发生什么？对于材料 B，脆弱的表面态很容易被破坏；[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)打开，导电环路消失。但对于材料 A，即歪尔半金属，奇迹发生了：[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)依然存在！它们的形状可能会稍有改变，但无法被移除。它们受到[拓扑保护](@keyword=topological_protection|lang=zh-CN|style=Feynman)，是隐藏在体态中歪尔点的直接而稳固的体现。只要体态仍然是歪尔[半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)，它们就必须存在 [@problem_id:1827857]。

### 晶体中宇宙的回响

这种奇异性并不仅限于表面。歪尔[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)的手性导致了一些似乎借鉴自高能物理领域的现象。其中最奇特的一个是**[手性反常](@keyword=axial_anomaly|lang=zh-CN|style=Feynman)**。理论预测，在平行的[电场和磁场](@keyword=electric_and_magnetic_fields|lang=zh-CN|style=Feynman)作用下，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)应该会从一个歪尔节点周围的态被“泵”到其相反手性伙伴节点周围的态。

虽然直接测量这种流动具有挑战性，但其效应是可以被观察到的。当向歪尔[半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)施加强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)时，电子态会重组为量子化的**朗道能级**。但对于歪尔[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)，一个特殊的“零”[朗道能级](@keyword=landau_levels|lang=zh-CN|style=Feynman)会出现。在这个能级上，电子实际上被限制在只能沿着[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)方向[一维运动](@keyword=one_dimensional_motion|lang=zh-CN|style=Feynman)。一个三维材料实际上变成了一大束一维[量子线](@keyword=quantum_wires|lang=zh-CN|style=Feynman)！这种独特的一维手性运动会导致独特的实验特征，例如，对材料比热的贡献与温度的三次方成正比（$C_V \propto T^3$），这是由节点附近的[线性色散关系](@keyword=linear_dispersion_relation|lang=zh-CN|style=Feynman)决定的 [@problem_id:1827858]。

从对称性破缺和[无质量粒子](@keyword=massless_particles|lang=zh-CN|style=Feynman)，到受拓扑保护的表面高速公路和宇宙反常现象，歪尔半金属的原理与机制揭示了一个丰富、相互关联的世界。它们向我们展示，看似平静的晶体内部，可以承载宇宙本身所有的基本之美与奇异。