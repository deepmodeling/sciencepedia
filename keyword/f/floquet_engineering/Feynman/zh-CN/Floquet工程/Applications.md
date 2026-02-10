## 应用与跨学科联系

既然我们已经熟悉了[Floquet工程](@keyword=floquet_engineering|lang=zh-CN|style=Feynman)的基本原理，你可能会问：“这一切都非常优雅，但它究竟有何*用处*？”这是一个合理的问题。对物理学家来说，发现一个新原理，一种看待世界的新方式，本身往往就是一种回报。但一个强大思想的真正美妙之处，常常在其应用的万花筒中展现出来——它连接看似毫不相干的领域，让我们不仅能理解世界，更能开始塑造世界。

如果说静态哈密顿量是一块由自然雕刻的大理石，那么[Floquet工程](@keyword=floquet_engineering|lang=zh-CN|style=Feynman)就是一种新型的凿子。它是一种动态的、有节奏的工具，让我们能够动态地重塑物质。我们不再局限于自然提供的形状；我们可以使用光和其他周期性场来雕刻出新的功能、新的几何结构，甚至是原本不可能存在的全新物质相。让我们参观一下这个作坊，看看我们能建造出哪些奇妙的东西。

### 塑造运动与相互作用

在最基本的层面上，我们可以利用[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)来掌控量子运动的规则本身。想象一下[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中的粒子，像地铁线路上的乘客一样从一个格点跳到另一个格点。在静态世界里，格点之间的“隧穿”概率是材料的固定属性。但如果我们能来回摇晃[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)呢？通过仔细选择这种摇晃的频率和振幅，我们可以实现一些非凡的事情：我们可以有效地把隧穿*关闭*。这不仅仅是减少它；我们可以精确地把它调到零！这种效应，被称为**[相干隧穿](@keyword=coherent_tunneling|lang=zh-CN|style=Feynman)销毁**，是驱动周期内[时间平均](@keyword=time_averaging|lang=zh-CN|style=Feynman)的美妙结果。跳跃概率最终由一个称为[贝塞尔函数](@keyword=bessel_function|lang=zh-CN|style=Feynman)的数学函数所支配，该函数在特定的驱动强度下有零点。通过将我们的“摇晃旋钮”调到这些零点之一，我们可以将粒子完全冻结在原地，这种现象称为动力学局域化[@problem_id:2972557]。

当然，我们能关闭的，也能开启。考虑相反的情况：倾斜[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上的粒子，就像楼梯上的球。由倾斜产生的相邻格点间的能量差阻止它们跳跃。它们被卡住了。现在，我们施加驱动。如果驱动量子的能量$\hbar\omega$与楼梯的能量阶梯相匹配，驱动就能提供粒子攀登到下一个格点所需的精确“一脚”。这种**[光子辅助隧穿](@keyword=photon_assisted_tunneling|lang=zh-CN|style=Feynman)**在原本没有运动的地方恢复了运动，用光的力量将绝缘体变成了导体[@problem_id:2972557]。

这种控制超越了[单粒子运动](@keyword=single_particle_motion|lang=zh-CN|style=Feynman)，延伸到[多体系统](@keyword=many_body_systems|lang=zh-CN|style=Feynman)的复杂舞蹈中。在[超冷原子](@keyword=ultracold_atoms|lang=zh-CN|style=Feynman)的世界里，物理学家已经可以调节原子间相互作用的强度。[Floquet工程](@keyword=floquet_engineering|lang=zh-CN|style=Feynman)增加了另一层控制，使我们能够动态地修改这些相互作用。更微妙的是，我们可以设计出让复杂的、由相互作用驱动的过程成为主要输运形式的情景。在某些绝缘态下，单个粒子是固定的，但同一格点上的一对粒子——一个“双占据子”（doublon）——可以一起移动。通过使用驱动来抑制[单粒子运动](@keyword=single_particle_motion|lang=zh-CN|style=Feynman)，我们可以分离并研究这些奇异的双占据子[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的动力学，从而让我们进入一个更丰富的多体物理世界[@problem_id:41598]。

### 打造新材料与新几何

有了这些工具，我们能够超越简单地调整现有属性，可以创造出具有全新特性的材料。其中最惊人的例子之一是创造**[人工规范场](@keyword=synthetic_gauge_fields|lang=zh-CN|style=Feynman)**。中性原子，顾名思义，不受[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)影响。这很遗憾，因为带电粒子在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中的物理，比如量子霍尔效应，是整个物理学中最丰富的领域之一。

[Floquet工程](@keyword=floquet_engineering|lang=zh-CN|style=Feynman)提供了一种极其巧妙的变通方法。通过对光晶格中的原子施加精心编排的驱动序列，我们可以使从一个格点到下一个格点的“跳跃”振幅成为一个*复数*。这为什么重要？因为这个复数的相位作用于中性粒子的方式，与一个带电粒子从磁矢量势中拾取的[Aharonov-Bohm相](@keyword=aharonov_bohm_phase|lang=zh-CN|style=Feynman)位的作用方式完全相同。这些原子的行为*就好像*它们在巨大的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中运动，尽管现场连一块磁铁都没有[@problem_id:1233203]。我们欺骗了原子，让它们以为自己带电，从而为在纯净、高度可控的原子系统中实现和探索量子霍尔物理打开了大门。

也许这种方法最著名的成就是创造了**[Floquet拓扑绝缘体](@keyword=floquet_topological_insulators|lang=zh-CN|style=Feynman)**。石墨烯是一种神奇的材料，一层碳原子薄片，其中电子表现得像无质量的[相对论性粒子](@keyword=relativistic_particle|lang=zh-CN|style=Feynman)。但它是一种半金属，而不是真正的绝缘体。如果我们能打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，让电子获得质量，仅仅通过打开一束光呢？

通过用[圆偏振](@keyword=circular_polarization|lang=zh-CN|style=Feynman)激光照射石墨烯，我们恰好做到了这一点。光的旋转电场“搅动”电子，在高频极限下，涌现出的[有效哈密顿量](@keyword=effective_hamiltonian|lang=zh-CN|style=Feynman)包含了一个新项——一个看起来完全像质量的项。我们动态地在一个以前[无能](@keyword=anergy|lang=zh-CN|style=Feynman)隙的材料中产生了一个质量[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)[@problem_id:1097445]。这不仅仅是一个理论技巧；这种光诱导的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)改变了材料的基本电子拓扑结构。而且它有真实的、可测量的后果。例如，这种“Floquet[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)”在低温下的[电子热容](@keyword=electronic_heat_capacity|lang=zh-CN|style=Feynman)将显示出指数级的抑制，这是我们用光设计的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的清晰[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)印记[@problem_id:118019]。我们[实质](@keyword=parenchyma|lang=zh-CN|style=Feynman)上发明了一种只有在光照下才存在的新材料。

### 从[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)到[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机

[Floquet工程](@keyword=floquet_engineering|lang=zh-CN|style=Feynman)的力量远远超出了凝聚态和原子物理的范畴，延伸到了化学和计算机科学等领域。

在化学中，一个光诱导反应的命运常常在一个“[锥形交叉](@keyword=conical_intersections|lang=zh-CN|style=Feynman)点”上决定——这是两个电子态的[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)相遇的点，为分子从一个态切换到另一个态创造了一个漏斗。量子力学的一个基本规则，即[von Neumann-Wigner定理](@keyword=von_neumann_wigner_theorem|lang=zh-CN|style=Feynman)，指出要发生这种简并，至少需要两个独立的核坐标。这意味着一个简单的[双原子分子](@keyword=diatomic_molecules|lang=zh-CN|style=Feynman)，只有一个[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)坐标（[键长](@keyword=bond_length|lang=zh-CN|style=Feynman)$R$），不能有自然的[锥形交叉](@keyword=conical_intersections|lang=zh-CN|style=Feynman)。

但是，当我们将这个[双原子分子](@keyword=diatomic_molecules|lang=zh-CN|style=Feynman)置于强激光场中时会发生什么？一个新的坐标加入了进来：分子轴与场偏振之间的角度$\theta$。[缀饰态](@keyword=dressed_states|lang=zh-CN|style=Feynman)[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)现在存在于一个二维空间($R$, $\theta$)中。突然间，真正的简并成为可能！通过调节激光并找到合适的取向，我们可以在原本不存在的地方创造一个**[光致锥形交叉](@keyword=light_induced_conical_intersection|lang=zh-CN|style=Feynman)（LICI）**[@problem_id:2765932]。这对[光化学](@keyword=photochemistry|lang=zh-CN|style=Feynman)来说是一场革命，使我们能够用激光开辟新的[反应途径](@keyword=reaction_pathways|lang=zh-CN|style=Feynman)，并以前所未有的控制力引导化学动力学。

这种精妙控制的主题在构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的探索中得到了终[极体](@keyword=polar_bodies|lang=zh-CN|style=Feynman)现。其中一个巨大的挑战是[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，即[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的构件，非常脆弱。它们容易受到噪声和来自相邻比特的不必要“串扰”的影响——这是一种会破坏计算的寄生相互作用。在这里，[Floquet工程](@keyword=floquet_engineering|lang=zh-CN|style=Feynman)提供了一个极其优雅的解决方案。可以设计一种复杂的微波脉冲，同时完成两个任务：它执行所需的逻辑操作（一个双[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)门），同时生成一个有效场（一个[AC斯塔克位移](@keyword=light_shift|lang=zh-CN|style=Feynman)），该场被精确地调整以抵消不希望的寄生相互作用[@problem_id:70618]。这是量子工程的典范——不仅用驱动来计算，而且在计算发生的同时主动保护它。

### 奇异前沿：新的物质相

到目前为止，我们讨论了使用驱动来修改系统或以新的方式模仿静态现象。但最激动人心的前沿是[Floquet工程](@keyword=floquet_engineering|lang=zh-CN|style=Feynman)让我们能够创造出*没有静态类似物*的物质相——本质上是动态的组织形式。

其中一个例子是**反常[Floquet拓扑绝缘体](@keyword=floquet_topological_insulators|lang=zh-CN|style=Feynman)**。像它的静态表亲一样，它在其边界拥有稳健的导电态。但这些态可以具有在[静态系统](@keyword=static_systems|lang=zh-CN|style=Feynman)中不可能存在的[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)，例如$\varepsilon = \pi\hbar/T$，正好位于允许的[准能量](@keyword=quasi_energy|lang=zh-CN|style=Feynman)区的边缘。这个“$\pi$-模”中的本征态有一个奇特的性质：经过一个驱动周期$T$后，它的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)会带一个负号回来。它只在*两个*周期后才回到原始状态[@problem_id:1275963]。它以推动它的力的频率的一半[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)！

这种周期加倍的响应是另一个更奇异想法的关键标志：**[离散时间晶体](@keyword=discrete_time_crystals|lang=zh-CN|style=Feynman)（DTC）**。一个普通的晶体，比如钻石，是一种自发地打破连续*空间*-平移对称性的物质状态。原子们[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成一个周期性[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，尽管物理定律本身是处处相同的。一个[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)，在一个优美的类比中，是一个自发地打破离散*时间*-[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)的多体系统。当受到周期为$T$的[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)时，系统的响应不是周期$T$，而是更长的周期，$2T$，$3T$等等，并且对于任何一般的初始状态都稳健地如此。

很长一段时间里，人们不清楚这样的状态是否可以实现。但是通过结合[周期性驱动](@keyword=periodic_driving|lang=zh-CN|style=Feynman)、[多体相互作用](@keyword=many_body_interaction|lang=zh-CN|style=Feynman)和无序（以防止系统简单地升温）这些要素，这些相已经在实验室中被创造出来。在这些新思想最惊人的综合中，可以构建一个同时是[Floquet拓扑绝缘体](@keyword=floquet_topological_insulators|lang=zh-CN|style=Feynman)和[离散时间晶体](@keyword=discrete_time_crystals|lang=zh-CN|style=Feynman)的单一系统。在这样的系统中，边缘的拓扑$\pi$-模正是承载[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)序的物体，它们的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)以一种稳健的、周期加倍的节奏[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)[@problem_id:3021745]。

正是在这里，我们看到了[Floquet工程](@keyword=floquet_engineering|lang=zh-CN|style=Feynman)的全部力量和美妙。它不仅仅是一个工具，而是一个新的[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)。它赋予我们能力，将绝缘体变成导体，将半金属变成拓扑材料，并用光锻造出[人工磁场](@keyword=synthetic_magnetic_fields|lang=zh-CN|style=Feynman)。它深化了我们控制[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)和构建更稳健[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的能力。最后，它开启了通往像[时间晶体](@keyword=time_crystals|lang=zh-CN|style=Feynman)这样全新的、动态的物质相的大门，挑战了我们对序和平衡的根本观念。Floquet驱动的节奏性节拍是一种新型物理学的脉搏，而我们才刚刚开始探索它[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)我们进入的世界。