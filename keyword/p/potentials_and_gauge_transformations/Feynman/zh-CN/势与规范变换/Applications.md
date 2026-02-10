## 应用与跨学科联系

在我们完成了对[势和规范变换](@keyword=potentials_and_gauge_transformations|lang=zh-CN|style=Feynman)原理的探索之后，你可能会产生一种奇妙的感觉。我们已经确定，势 $V$ 和 $\vec{A}$ 并非唯一定义；存在一种“自由度”，可以用一种特定的方式改变它们，而不改变我们能实际测量的物理电场和磁场。乍一看，这似乎是一个数学上的麻烦，是我们描述中的一种冗余，需要设法消除。但在物理学中，我们学会了对这类“麻烦”保持警惕。它们往往不是缺陷，而是特性——是指向世界更深层、更优美结构的线索。[规范自由度](@keyword=gauge_freedom|lang=zh-CN|style=Feynman)的故事也许是这方面最深刻的例子。事实证明，这个原理不是一个待修正的麻烦，而是一把金钥匙，它解锁了我们对自然界每一种基本力的理解。

### 选择工具的实用艺术

让我们从经典[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)中规范自由度最实际的应用开始。如果势不是唯一的，我们应该使用哪一个呢？答案是：用那个能让我们最省事的！进行[规范变换](@keyword=gauge_transformations|lang=zh-CN|style=Feynman)的自由就是为特定工作选择工具的自由。

想象一个静止在空间中的点电荷。我们知道它会产生一个简单的库仑电场。我们可以用一个简单的标势 $V$ 和一个处处为零的[矢势](@keyword=vector_potential|lang=zh-CN|style=Feynman) $\vec{A}$ 来描述它。但我们可以自由地进行一次规范变换——即使是一次看起来非常奇怪、依赖于时间和空间的变换——从而得到一个新的 $V'$ 和一个新的、非零的 $\vec{A}'$。如果我们接着用这些新的、更复杂的势来计算电场，变换产生的额外项会巧妙地完全抵消，使我们得到与开始时完全相同的库仑场 [@problem_id:1583173]。物理规律顽固地保持不变，理应如此。

这种自由成为一种强大的实用工具。考虑描述一个均匀[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，就像在螺线管内部或[粒子加速器](@keyword=particle_accelerators|lang=zh-CN|style=Feynman)中使用的那种。描述这个场没有唯一的“正确”矢势。一种选择是*朗道规范*，它对于具有[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)的问题特别方便，比如一个电子在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中直线运动。另一种选择是*对称规范*，它更适合具有旋转对称性的问题，比如一个电子绕[中心点](@keyword=medoid|lang=zh-CN|style=Feynman)[轨道运动](@keyword=orbital_motion|lang=zh-CN|style=Feynman)。通过进行规范变换，我们可以随心所欲地在这些描述之间切换，从一种数学语言转换到另一种，以最好地适应我们问题的几何形状，而描述的却是完全相同的物理[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) [@problem_id:1202126] [@problem_id:1825509]。同样的原理也适用于描述[电磁波](@keyword=electromagnetic_waves|lang=zh-CN|style=Feynman)。我们总可以进行一次规范变换，以确保我们的[矢势](@keyword=vector_potential|lang=zh-CN|style=Feynman)在波传播方向上没有分量，从而简化对光及其偏振的描述 [@problem_id:1583168]。

### 量子飞跃：当势变为物理实体

很长一段时间里，故事就是这样：势是方便的数学工具，但场才是物理上真实的东西。然后量子力学出现了，故事变得有趣得多。在量子世界里，粒子由[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)描述，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)不仅有振幅，还有相位。而正是在这个相位中，矢势的幽灵复活了。

关键的联系是一个称为*[最小耦合](@keyword=minimal_coupling|lang=zh-CN|style=Feynman)*的原理。它规定了像电子这样的带电粒子应如何响应[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)。当我们写下带电粒子的薛定谔方程时，我们发现，为了在对势 $(\vec{A}, V)$进行规范变换后保持方程形式不变，我们*被迫*要同时变换粒子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman) $\psi$。这种变换是其局域相位的改变，一个直接依赖于我们用于势的规范函数 $\chi$ 的扭转。量子力学的一致性要求[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)的规范自由度必须与[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)的相位自由度联系在一起 [@problem_id:2857758] [@problem_id:2095525]。

这种联系带来了一个惊人的物理后果，即阿哈罗诺夫-玻姆效应所展示的。想象一个细长的[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)，[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)完全限制在其中。在[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)外部，[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $\vec{B}$ 为零。现在，我们让电子沿着螺线管两侧的路径发射，但从不进入其中，然后让它们重新组合以观察[干涉图样](@keyword=interference_pattern|lang=zh-CN|style=Feynman)。经典地看，由于电子从未穿过[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，它们应该不受任何力，其路径也不应受影响。但事实并非如此！[干涉图样](@keyword=interference_pattern|lang=zh-CN|style=Feynman)发生了移动，就好像螺线管仍在影响电子一样。

这怎么可能呢？虽然[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)外的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $\vec{B}$ 为零，但[矢势](@keyword=vector_potential|lang=zh-CN|style=Feynman) $\vec{A}$ 并不为零。当电子行进时，其量子相位会累积一个与 $\vec{A}$ 沿其路径的[线积分](@keyword=line_integrals|lang=zh-CN|style=Feynman)成正比的相移。因为 $\vec{A}$ 环绕着螺线管，所以左右两侧路径累积了不同的相移。这种[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)在最终的[干涉图样](@keyword=interference_pattern|lang=zh-CN|style=Feynman)中是物理上可观测的。这证明了，在量子力学中，带电粒子可以被势在[力场](@keyword=force_field|lang=zh-CN|style=Feynman)为零的区域所影响。“数学工具”具有了直接的、可测量的后果。[矢势](@keyword=vector_potential|lang=zh-CN|style=Feynman)围绕闭合回路的[线积分](@keyword=line_integrals|lang=zh-CN|style=Feynman)（与包围的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)有关）成为一个量子粒子可以“看到”的物理量 [@problem_id:609871]。

### 宏伟设计：作为组织原则的[规范理论](@keyword=gauge_theory|lang=zh-CN|style=Feynman)

这种对称性（规范不变性）与力（电磁力）之间的深刻联系，原来是一个普适的模板。20世纪后的物理学在很多方面就是将这个模板应用于越来越广泛领域的故事。

**凝聚态物质：[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的秘密**

在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的奇异世界里，电子结合成[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)，并凝聚成一个跨越整个材料的单一、巨大的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。这个宏观量子客体有其自身的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)，或称为*序参量* $\psi$。由于库珀对的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为 $2e$，这个序参量必须遵守规范不变性的规则。辉煌地描述了超导现象的[金兹堡-朗道理论](@keyword=ginzburg_landau_theory|lang=zh-CN|style=Feynman)，从根本上说就是一个规范理论。

在该理论中，[局域规范对称性](@keyword=local_gauge_symmetry|lang=zh-CN|style=Feynman)的自发破缺导致了[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)一些最著名的性质。在真空中无质量的[光子](@keyword=photon|lang=zh-CN|style=Feynman)，在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部获得了质量。这就是[安德森-希格斯机制](@keyword=anderson_higgs_mechanism|lang=zh-CN|style=Feynman)的核心。有质量的[光子](@keyword=photon|lang=zh-CN|style=Feynman)介导[短程力](@keyword=short_range_forces|lang=zh-CN|style=Feynman)，这解释了为什么[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)会被排出[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)——即[迈斯纳效应](@keyword=the_meissner_effect|lang=zh-CN|style=Feynman)。此外，要求[宏观波函数](@keyword=macroscopic_wavefunction|lang=zh-CN|style=Feynman)在围绕[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)中的孔洞一周后必须是单值的，这迫使陷于孔洞中的磁通量以 $\Phi_0 = h/2e$ 为单位量子化。分母中的因子 $2e$ 是对[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的直接测量，证实了微观理论。这些非凡的[宏观量子现象](@keyword=macroscopic_quantum_phenomena|lang=zh-CN|style=Feynman)都是系统潜在的规范对称性的直接后果 [@problem_id:2992433]。

**[粒子物理学](@keyword=particle_physics|lang=zh-CN|style=Feynman)：[标准模型](@keyword=standard_model|lang=zh-CN|style=Feynman)**

[规范理论](@keyword=gauge_theory|lang=zh-CN|style=Feynman)的胜利是[粒子物理学](@keyword=particle_physics|lang=zh-CN|style=Feynman)标准模型。物理学家们想：如果[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)的简单相位旋转——在一个称为U(1)的一维“内空间”中的旋转——不是唯一的可能性呢？如果基本粒子拥有更复杂的内空间，而物理定律在这些更高维空间中的旋转下保持不变呢？

这个想法是关键。通过要求支配夸克的定律在三维“色空间”（一种称为SU(3)的对称性）中的局域旋转下保持不变，你被迫引入一个新的[力场](@keyword=force_field|lang=zh-CN|style=Feynman)来维持这种[不变性](@keyword=invariance|lang=zh-CN|style=Feynman)。这个[力场](@keyword=force_field|lang=zh-CN|style=Feynman)就是胶子场，它介导强核力。通过要求在二维“[弱同位旋](@keyword=weak_isospin|lang=zh-CN|style=Feynman)空间”（SU(2)）中的旋转下不变，你必须引入[W和Z玻色子](@keyword=w_and_z_bosons|lang=zh-CN|style=Feynman)，它们介导[弱核力](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)。在这种非阿贝尔（或[杨-米尔斯](@keyword=yang_mills|lang=zh-CN|style=Feynman)）理论中，力的载体本身也带有它们所介导的力荷，导致了比[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)更丰富、更复杂的动力学 [@problem_id:718072]。在这种图景下，自然界基本力的存在本身就是[局域规范对称性](@keyword=local_gauge_symmetry|lang=zh-CN|style=Feynman)的要求。你不是手动把力放进去的；对称性原理为你生成了它们。

**引力与宇宙学：[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的规范**

引力也可以是一种规范理论吗？答案是响亮的“是”，而且是以一种优美类似的方式。在广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中，基本的对称性是在广义坐标变换下的不变性——即可以用你喜欢的任何[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)来描述[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的自由。在更深的层次上，[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的每一点也存在一个局域对称性：选择你的局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)，即你对“上”、“下”、“左”、“右”的局域定义的自由。这就是局域[洛伦兹不变性](@keyword=lorentz_invariance|lang=zh-CN|style=Feynman)原理。

正如使薛定谔方程在局域[相位移](@keyword=phase_shift|lang=zh-CN|style=Feynman)动下保持不变需要引入矢势 $A_\mu$ 一样，使旋量（如电子）的狄拉克方程在[弯曲时空](@keyword=curved_spacetime|lang=zh-CN|style=Feynman)中[局域洛伦兹变换](@keyword=local_lorentz_transformations|lang=zh-CN|style=Feynman)下保持不变，也需要引入一个新的联络场。这个场就是*[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)* $\Omega_\mu$。它的作用与[电磁势](@keyword=electromagnetic_potentials|lang=zh-CN|style=Feynman)完全类似：它是一个[规范势](@keyword=gauge_potential|lang=zh-CN|style=Feynman)，告诉[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)在[弯曲时空](@keyword=curved_spacetime|lang=zh-CN|style=Feynman)几何中从一点移动到另一点时如何定向 [@problem_id:1876058]。用这种语言来说，引力是[洛伦兹群](@keyword=lorentz_group|lang=zh-CN|style=Feynman)的[规范理论](@keyword=gauge_theory|lang=zh-CN|style=Feynman)。

这一观点甚至延伸到对整个宇宙的研究。当我们研究[早期宇宙](@keyword=early_universe|lang=zh-CN|style=Feynman)中那些成长为我们今天所见的星系的微小扰动时，我们面临一个规范问题。我们计算出的引力势或密度涨落等数值，都依赖于我们用来描述它们的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)。这与[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)中的势完全类似。为了做出真实的、物理的预测——比如宇宙微波背景辐射的温度图样——宇宙学家们必须构建特殊的“规范不变”量，这些量独立于坐标选择，从而确保他们的预测是关于宇宙本身的，而不是他们覆盖在宇宙之上的数学网格 [@problem_id:1488428]。

最初在[麦克斯韦方程组](@keyword=maxwell_s_equations|lang=zh-CN|style=Feynman)中的一个奇特之处，如今已成为现代物理学的核心组织原则。它决定了相互作用的形式，揭示了现实的量子本性，解释了奇异材料的行为，并为塑造我们宇宙在各种尺度上的力提供了蓝图。[规范对称性](@keyword=gauge_symmetry|lang=zh-CN|style=Feynman)是宇宙所遵循的沉默而优雅的规则。