## 引言
光与物质的相互作用是科学中最基本的过程之一，支撑着从宝石的颜色到激光器的工作原理的一切事物。在晶体这一完美有序的世界里，这种相互作用由一系列优雅的量子力学规则所支配。但是，为什么像砷化镓这样的某些晶体材料能明亮地发光，构成我们的LED，而作为现代电子学基础的硅却保持黑暗呢？答案不仅在于光的能量，更在于一个更微妙的[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman)：晶体动量。它对光与物质相互作用施加的明显限制，在物质世界中创造了一道“巨大鸿沟”，这一区别对技术产生了深远的影响。

本文将层层揭开这个迷人课题的面纱。我们将探索对称性和守恒性这些抽象原理如何转化为定义我们这个时代的材料的有形属性。在接下来的章节中，您将对固态物理这一关键领域获得深刻的理解。我们将从“原理与机制”一章开始，探索核心物理学，其中能量和[晶体动量守恒](@keyword=crystal_momentum_conservation|lang=zh-CN|style=Feynman)定律得以确立，并引出[直接带隙和间接带隙](@keyword=direct_and_indirect_bandgap|lang=zh-CN|style=Feynman)这一关键概念。然后，我们将在“应用与跨学科联系”一章中进入真实世界，看看物理学家和工程师如何利用、变通甚至打破这些规则，以创造从[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)和[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)显示器到[拓扑物质](@keyword=topological_matter|lang=zh-CN|style=Feynman)等奇异前沿领域的革命性技术。

## 原理与机制

### [对称性与守恒](@keyword=symmetry_and_conservation|lang=zh-CN|style=Feynman)之舞

想象一下，你正试图穿越一个广阔、种植完美的果园，那里的每一棵树都一模一样，并以重复的晶体模式[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。你的移动并非完全自由；它受制于你周围的周期性景观。从一棵树移动到下一排的相应树木，感觉与任何其他类似的移动都相同。这就是一个电子在[完美晶体](@keyword=perfect_crystal|lang=zh-CN|style=Feynman)中的世界。原子惊人规则的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)创造了一个周期性的电势，一个无限重复的山丘和山谷景观。

量子力学告诉我们，在这种周期性世界中的运动有一些美妙之处。穿行于此景观的电子并不像一个具有确定动量的简单粒子。相反，它的波状性质受到[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的调制。薛定谔方程的解，被称为**[布洛赫态](@keyword=bloch_states|lang=zh-CN|style=Feynman) (Bloch states)**，是与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)本身具有相同周期性的波。这些状态中的每一个都由一个特殊的量子数来标记，称为**晶体动量 (crystal momentum)**，用向量 $\hbar\mathbf{k}$ 表示。这与[自由粒子](@keyword=the_free_particle|lang=zh-CN|style=Feynman)在真空中的动量不同；它更像一本护照，描述了电子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在从一个晶胞移动到下一个[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)时如何演化。它是晶体[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)的直接结果。

正如自由空间中的动量守恒源于空间处处相同的对称性一样，晶体动量的守恒则源于[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)从一个晶胞到下一个晶胞都相同的特性。任何发生在这个完美晶体内的过程，例如电子与光的相互作用，都必须尊重这种潜在的对称性。相互作用前系统的总[晶体动量](@keyword=crystal_momentum|lang=zh-CN|style=Feynman)必须等于相互作用后的总晶体动量，至少在[相差](@keyword=phase_contrast|lang=zh-CN|style=Feynman)一个倒格矢的“跳跃”范围内是如此，而对于我们关心的过程，这个细节通常可以忽略。这一条优雅的原则是理解固体中大量光学现象的关键。[@problem_id:2982263] [@problem_id:2819440]

### [光子](@keyword=photon|lang=zh-CN|style=Feynman)的轻柔一推

现在，让我们用一束光照射我们的晶体。一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)，即光的量子，同时携带能量和动量。当一个处于较低[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)（价带）的电子吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)时，它可以获得足够的能量跃迁到更高的、空的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)（[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)）。这被称为**[带间跃迁](@keyword=interband_transitions|lang=zh-CN|style=Feynman) (interband transition)**。能量显然是守恒的：电子的最终能量是其初始能量加上[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量，$E_{photon} = \hbar\omega$。

但动量呢？[光子](@keyword=photon|lang=zh-CN|style=Feynman)也将其动量 $\hbar\mathbf{q}$ 传递给电子。[晶体动量守恒](@keyword=crystal_momentum_conservation|lang=zh-CN|style=Feynman)定律规定，电子的最终晶体动量 $\mathbf{k}_f$ 必须等于其初始[晶体动量](@keyword=crystal_momentum|lang=zh-CN|style=Feynman) $\mathbf{k}_i$ 加上[光子](@keyword=photon|lang=zh-CN|style=Feynman)的动量 $\mathbf{q}$。所以，$\mathbf{k}_f = \mathbf{k}_i + \mathbf{q}$。

然而，在这里我们遇到了尺度上的巨大不匹配。让我们看看数字。对于一个典型的晶体，晶格常数——原子间的距离——大约是几埃（$a \approx 0.5 \text{ nm}$）。所有可能晶体动量的“地图”，即布里渊区，其大小与此成反比，大约为 $2\pi/a$。对于可见光，波长要大得多，大约为 $\lambda \approx 500 \text{ nm}$。这个[光子](@keyword=photon|lang=zh-CN|style=Feynman)的动量是 $q = 2\pi/\lambda$。让我们比较一下两者：[光子动量](@keyword=photon_momentum|lang=zh-CN|style=Feynman)与晶体动量空间尺度的比率是 $q / (2\pi/a) = a/\lambda$。[@problem_id:2819487]

数值上，这大约是 $0.5 \text{ nm} / 500 \text{ nm} = 0.001$。这个微小的数字是问题的核心。[光子](@keyword=photon|lang=zh-CN|style=Feynman)给了电子巨大的能量冲击，但只给了它一个微小到几乎可以忽略不计的动量推动。[@problem_id:2982257] 在一个极好的近似下，我们可以认为[光子](@keyword=photon|lang=zh-CN|style=Feynman)的动量为零。守恒定律因此急剧简化为：
$$ \mathbf{k}_f \approx \mathbf{k}_i $$
这是[光学跃迁](@keyword=optical_transitions|lang=zh-CN|style=Feynman)的基本选择定则。它意味着当一个电子吸收[光子](@keyword=photon|lang=zh-CN|style=Feynman)时，它必须在能量-动量[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman)图上几乎垂直向上跳跃。这被称为**[垂直跃迁](@keyword=vertical_transitions|lang=zh-CN|style=Feynman) (vertical transition)**。[@problem_id:2451003]

### 巨大鸿沟：[直接带隙与间接带隙](@keyword=direct_vs_indirect_gap|lang=zh-CN|style=Feynman)

这个简单的规则 $\mathbf{k}_f \approx \mathbf{k}_i$ 产生了深远的影响，将几乎所有的[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)分成了两个截然不同的家族。

处于满价带中的电子自然会寻找能量最低的路径跃迁到空的导带。这条路径从价带的最高点，即**价带顶 (Valence Band Maximum, VBM)** 开始，结束于导带的最低点，即**导带底 (Conduction Band Minimum, CBM)**。它们之间的能量差就是材料的基本[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $E_g$。

**1. [直接带隙](@keyword=direct_bandgap|lang=zh-CN|style=Feynman)材料：** 在一些材料中，如砷化镓 (Gallium Arsenide, GaAs)，出现了一个奇妙的巧合。VBM和CBM在动量空间中完美对齐；它们都出现在相同的[晶体动量](@keyword=crystal_momentum|lang=zh-CN|style=Feynman) $\mathbf{k}$ 值处。具有这种性质的材料被称为具有**直接带隙 (direct band gap)**。对于一个位于VBM并希望跃迁到CBM的电子来说，这个跃迁很简单。它几乎不需要[动量变化](@keyword=change_in_momentum|lang=zh-CN|style=Feynman)，这个条件通过吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)就能完美满足。电子可以垂直向上跃迁，轻松地同时满足[能量和动量守恒](@keyword=conservation_of_energy_and_momentum|lang=zh-CN|style=Feynman)。这是一个高效的一阶量子过程。反之亦然：一个处于CBM的电子可以轻易地回落到VBM并辐射一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)。这就是为什么直接带隙材料是如此出色的发光体，并构成了我们的发光二极管 (LED) 和[激光二极管](@keyword=laser_diode|lang=zh-CN|style=Feynman)的基础。[@problem_id:1354778] [@problem_id:3002201]

**2. [间接带隙](@keyword=indirect_bandgap|lang=zh-CN|style=Feynman)材料：** 在其他材料中，如电子工业的主力军硅(Silicon, Si)和锗(Germanium, Ge)，情况则有所不同。VBM出现在一个 $\mathbf{k}$ 值处，而CBM则位于动量空间中一个完全不同的点。这种材料具有**间接带隙 (indirect band gap)**。现在电子面临一个两难的境地。为了进行能量最低的跃迁，它需要显著改变其能量*和*动量。但是[光子](@keyword=photon|lang=zh-CN|style=Feynman)只能提供能量；它无法提供大的[动量变化](@keyword=change_in_momentum|lang=zh-CN|style=Feynman)。从VBM的[垂直跃迁](@keyword=vertical_transitions|lang=zh-CN|style=Feynman)会把电子带到导带中一个高能量点，而不是最低点。直接跃迁到CBM因动量守恒而被禁止。从某种意义上说，电子被困住了。[辐射复合](@keyword=radiative_recombination|lang=zh-CN|style=Feynman)的可能性极低，这就是为什么当你在纯硅芯片上通过电流时它不会发光。[@problem_id:2484959]

### [声子](@keyword=phonons|lang=zh-CN|style=Feynman)来拯救

如果在间接带隙材料中禁止直接[光子](@keyword=photon|lang=zh-CN|style=Feynman)吸收，那么任何吸收是如何发生的呢？晶体并非一个完全静止和刚性的物体。它的原子处于持续的集体[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)中。量子力学告诉我们，这些晶格振动也是量子化的，晶格振动的一个量子被称为**[声子](@keyword=phonons|lang=zh-CN|style=Feynman) (phonon)**。

可以把[声子](@keyword=phonons|lang=zh-CN|style=Feynman)想象成一个声音的量子。虽然其能量通常很小（远小于[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量），但[声子](@keyword=phonons|lang=zh-CN|style=Feynman)可以携带大量的晶体动量，其范围可以跨越整个布里渊区。这正是电子所需要的。

为了在[间接带隙](@keyword=indirect_bandgap|lang=zh-CN|style=Feynman)材料中发生跃迁，电子必须参与一个更复杂的[三体](@keyword=trisomy|lang=zh-CN|style=Feynman)相互作用。它吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)以获得必要的能量，*并*同时吸收或发射一个[声子](@keyword=phonons|lang=zh-CN|style=Feynman)以获得必要的动量冲击。[@problem_id:1354778] 现在的守恒定律涉及所有三个参与者：
$$ \mathbf{k}_f = \mathbf{k}_i + \mathbf{q} \pm \mathbf{k}_{\text{phonon}} $$
由于[光子](@keyword=photon|lang=zh-CN|style=Feynman)的动量 $\mathbf{q}$ 可以忽略不计，[声子](@keyword=phonons|lang=zh-CN|style=Feynman)必须提供连接[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)和导带[极值](@keyword=extrema|lang=zh-CN|style=Feynman)点之间所需的动量：$\mathbf{k}_{\text{phonon}} \approx \pm(\mathbf{k}_c - \mathbf{k}_v)$。

这是一个[二阶过程](@keyword=second_order_process|lang=zh-CN|style=Feynman)——就像需要两件独立的事情同时发生——因此其发生的概率远低于直接的一阶[垂直跃迁](@keyword=vertical_transitions|lang=zh-CN|style=Feynman)。这解释了为什么间接材料在带边附近的光学吸收要弱得多。这也解释了为什么它们的[吸收光谱](@keyword=absorption_spectrum|lang=zh-CN|style=Feynman)有一个平缓的、依赖于温度的起始（因为可用[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的数量随温度升高而增加），通常在对应于[带隙能量](@keyword=bandgap_energy|lang=zh-CN|style=Feynman)加上或减去一个[声子](@keyword=phonons|lang=zh-CN|style=Feynman)能量的能量点上显示出特征性的“拐点”，这与[直接带隙](@keyword=direct_bandgap|lang=zh-CN|style=Feynman)材料尖锐、强烈的吸收边形成鲜明对比。[@problem_id:2955770] [@problem_id:2484959]

### 超越基础：自旋与束缚对

当我们更深入地观察时，[动量守恒](@keyword=conservation_of_momentum|lang=zh-CN|style=Feynman)原理提供了更丰富的理解。

**自旋的角色：** 到目前为止，我们忽略了电子的[内禀角动量](@keyword=intrinsic_angular_momentum|lang=zh-CN|style=Feynman)：它的自旋。在跃迁过程中，[光子](@keyword=photon|lang=zh-CN|style=Feynman)的电场会翻转电子的自旋吗？在最简单的图景中，答案是否定的。光的电场与电子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)及其[轨道运动](@keyword=orbital_motion|lang=zh-CN|style=Feynman)相互作用。自旋是一个纯粹的[量子磁性](@keyword=quantum_magnetism|lang=zh-CN|style=Feynman)属性。只要自旋和轨道运动是独立的，相互作用算符就不会作用于电子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的自旋部分。由于自旋向上和自旋向下态的正交性 ($\langle\uparrow|\downarrow\rangle=0$)，任何会翻转自旋的跃迁矩阵元都为零。[选择定则](@keyword=selection_rules|lang=zh-CN|style=Feynman)是 $\Delta S = 0$；自旋是守恒的。[@problem_id:3015268] 在许多真实材料中，自旋翻转*确实*会发生，但这是更微妙的**自旋轨道耦合 (spin-orbit coupling)**效应的结果，这是一种[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)现象，它将电子的自旋与其[轨道运动](@keyword=orbital_motion|lang=zh-CN|style=Feynman)纠缠在一起，为光-轨道相互作用影响自旋提供了一条途径。

**[激子](@keyword=excitons|lang=zh-CN|style=Feynman) (Exciton)：** 当[光子](@keyword=photon|lang=zh-CN|style=Feynman)将一个[电子激发](@keyword=electronic_promotion|lang=zh-CN|style=Feynman)到[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)时，它在价带中留下一个带正电的“空穴”。这个电子和空穴可以通过库仑力相互吸引，形成一个[束缚态](@keyword=bound_states|lang=zh-CN|style=Feynman)，就像一个在晶体内部的微型氢原子。这个[电子-空穴对](@keyword=electron_hole_pair|lang=zh-CN|style=Feynman)本身就是一个[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，被称为**激子 (exciton)**。这个新实体会改变我们的规则吗？值得注意的是，不会。作为一个整体，激子携带一个明确的[质心](@keyword=center_of_mass|lang=zh-CN|style=Feynman)晶体动量 $\mathbf{K}$。就像单个电子一样，[光子](@keyword=photon|lang=zh-CN|style=Feynman)只能创建或湮灭动量接近于零的激子：$\mathbf{K} \approx \mathbf{q} \approx \mathbf{0}$。

这引出了一个美妙而有力的结论。在[直接带隙](@keyword=direct_bandgap|lang=zh-CN|style=Feynman)材料中，能量最低的激子由一个处于相同 $\mathbf{k}$ 值的电子和空穴形成，所以它的[质心动量](@keyword=center_of_mass_momentum|lang=zh-CN|style=Feynman)为 $\mathbf{K} \approx \mathbf{0}$。这种“明”激子与光有强烈的相互作用。在[间接带隙](@keyword=indirect_bandgap|lang=zh-CN|style=Feynman)材料中，能量最低的激子由一个处于不同 $\mathbf{k}$ 点的电子和空穴形成，使其具有一个大的[质心动量](@keyword=center_of_mass_momentum|lang=zh-CN|style=Feynman) $\mathbf{K} \neq \mathbf{0}$。这种激子不能仅由光产生，也不能通过发射光来衰变。它是一个**动量[暗态](@keyword=dark_states|lang=zh-CN|style=Feynman) (momentum-dark)**[激子](@keyword=excitons|lang=zh-CN|style=Feynman)，一个隐藏的状态，只有在[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的帮助下才能参与光学过程。[@problem_id:2814838] [光子](@keyword=photon|lang=zh-CN|style=Feynman)轻柔推动的简单规则即使对于这些更复杂的复合粒子也同样适用，统一了我们对不同现象的理解。

最后，值得将这些**带间 (interband)** 跃迁与**带内 (intraband)** 过程进行对比，在带内过程中，电子被场加速但仍保持在单一[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)内。在[完美晶体](@keyword=perfect_crystal|lang=zh-CN|style=Feynman)中，来自光波的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)电场不能在[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)内引起净能量吸收；它只是使电子来回晃动。为了让电子在有限频率下吸收能量，它需要发生散射——与杂质、缺陷或[声子散射](@keyword=phonon_scattering|lang=zh-CN|style=Feynman)。这种散射破坏了完美的动量守恒，从而允许了吸收，这正是金属具有其特征性光学性质的原因，这些性质由[德鲁德模型](@keyword=drude_model|lang=zh-CN|style=Feynman) (Drude model) 描述。[@problem_id:2819440] 这再次突显了对称性和守恒定律在支配光与物质在晶体有序世界中丰富多样的相互作用方式中所扮演的核心角色。