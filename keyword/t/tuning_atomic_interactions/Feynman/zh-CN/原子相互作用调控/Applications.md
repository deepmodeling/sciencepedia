## 应用与学科[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)

现在我们已经探索了调控原子相互作用背后的奇妙机制，你可能会问一个非常合理的问题：“那又怎样？” 拥有一个能控制原子间感受的旋钮固然是一项了不起的物理学壮举，但我们能用它来*做*什么呢？事实证明，这不仅仅是物理学家的玩具。这种控制是一把钥匙，它能开启新的世界，改变我们探测宇宙最深层规则、构建前所未有精度的技术、甚至构造全新计算形式的能力。我们已经从原子舞蹈的被动观察者，变成了它的编舞者。

### 塑造新物态：[BCS-BEC渡越](@keyword=bcs_bec_crossover|lang=zh-CN|style=Feynman)

或许，我们新获得控制能力最深远的应用，是创造和研究新奇物相的能力。在固态物理世界里，我们有两种著名的“超”行为。一种是玻色-爱因斯坦凝聚（BEC），其中一团[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)气体被冷却到接近绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)时，会坍缩成一个单一的、巨大的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。另一种是巴丁-库珀-施里弗（BCS）[超导理论](@keyword=superconductivity_theory|lang=zh-CN|style=Feynman)，它解释了金属中的电子如何配对并无阻力地流动。这些电子作为[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)，本不应形成BEC。但通过形成“库珀对”，它们的行为就像[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)，进入一个集体的[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)状态。

几十年来，这两种现象——BEC和BCS——被视为相关但又截然不同。BEC中的对（如双原子分子）是紧密束缚的，像一对紧贴着跳舞的舞伴，小而明确。而BCS超流体中的[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)则是弥散的、松散关联的实体，对中的两个粒子相隔的距离远大于电子间的平均间距。它们更像是宏大舞池中的舞者，与一个遥远的舞伴弱相关，但同属于一个巨大的[集体运动](@keyword=collective_motion|lang=zh-CN|style=Feynman)。

一个问题挥之不去：能否将一种状态连续地转变为另一种？利用超冷原子，答案是响亮的“是”。通过使用费什巴赫共振，我们可以取一团[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)原子气体，并调控它们之间的吸引力。当吸引力较弱时（对应于负的散射长度 $a$），原子形成大的、重叠的库珀对，这是BCS超流体的完美模拟。当我们转动旋钮——在共振点附近调节[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)——吸引力变得更强。散射长度 $a$ 变得很大，然后变为正值。[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)越拉越近，直到它们形成紧密束缚的[双原子分子](@keyword=diatomic_molecules|lang=zh-CN|style=Feynman)。这些分子作为[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)，随后可以形成[玻色-爱因斯坦凝聚](@keyword=bose_einstein_condensation|lang=zh-CN|style=Feynman)。

我们可以亲眼看着系统从一个BCS类的弱束缚对状态平滑地演化到一个紧束缚分子的BEC状态 ([@problem_id:2093375])。这个“[BCS-BEC渡越](@keyword=bcs_bec_crossover|lang=zh-CN|style=Feynman)”是物理学统一性的一个壮观证明，表明这两种看似不同的超流体现象只是同一底层量子现实的两个面孔，通过一个简单的调控参数连接起来。在实验室中拥有这个系统，使我们能够研究渡越正中间神秘的“幺正”区，这里的相互作用强度达到了量子力学所允许的极限，这个区域对于理解中子星和[早期宇宙](@keyword=early_universe|lang=zh-CN|style=Feynman)的[夸克-胶子等离子体](@keyword=quark_gluon_plasma|lang=zh-CN|style=Feynman)至关重要，并且极难进行理论计算。

### [量子工程](@keyword=quantum_engineering|lang=zh-CN|style=Feynman)师的工具箱：精度与控制

除了创造新世界，调控相互作用也是完善我们已有世界的重要工具。它使我们能够消除不希望的效应，并设计具有特定、理想性质的材料。

#### 完善时间

以原子钟为例，这是有史以来最精确的计时设备。它的工作原理是测量两个原子能级 $|1\rangle$ 和 $|2\rangle$ 之间量子跃迁的频率。一个理想的[原子钟](@keyword=atomic_clocks|lang=zh-CN|style=Feynman)应该测量单个孤立原子的跃迁。但实际上，我们使用的是一团原子，这些原子在不断地、尽管是轻微地相互碰撞。

每次碰撞都会轻微地改变参与原子的能级。这种“碰撞频移”引入了一个系统误差，导致时钟以一个略有不同且依赖于原子气体密度的速率滴答作响。这是一个微小的效应，但在追求极致精度的过程中，它是一个主要的难题。处于态 $|1\rangle$ 的原子所受的能量位移取决于它与处于态 $|1\rangle$ 的其他原子（由散射长度 $a_{11}$ 决定）和处于态 $|2\rangle$ 的其他原子（由 $a_{12}$ 决定）的相互作用。类似的规则也适用于处于态 $|2\rangle$ 的原子。最终的频移结果被证明与两个时钟态[散射长度](@keyword=scattering_length|lang=zh-CN|style=Feynman)的差异成正比，即一个类似 $(a_{22} - a_{11})$ 的项 ([@problem_id:1194913], [@problem_id:2016634])。

这就是我们神奇旋钮发挥作用的地方。利用费什巴赫共振，我们可以调控散射长度！想象一下，如果我们能调节[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，使得 $a_{11}$ 恰好等于 $a_{22}$。在这种情况下，碰撞频移将完全消失。原子仍然在碰撞，但从时钟跃迁的角度来看，两个态中的相互作用被完美地平衡了，误差也随之消失。这项技术现在已成为世界上最好的[原子钟](@keyword=atomic_clocks|lang=zh-CN|style=Feynman)的标准操作程序，推动着精确测量的边界。

#### 用光作画

改变能级的能力也让我们能够控制[量子气体](@keyword=quantum_gases|lang=zh-CN|style=Feynman)与光的相互作用。任何[材料的光学性质](@keyword=optical_properties_of_materials|lang=zh-CN|style=Feynman)——它的颜色、透明度、[折射率](@keyword=refractive_index|lang=zh-CN|style=Feynman)——都取决于其组成原子如何响应[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的电场。当光的频率接近原子共振时，这种响应最强。

由于原子间的相互作用会改变能级，它们也同样会改变共振频率。这意味着[超冷气体](@keyword=ultracold_gases|lang=zh-CN|style=Feynman)的光学性质变得依赖于我们设定的[相互作用强度](@keyword=interaction_strength|lang=zh-CN|style=Feynman)。描述光波进入介质时弯曲程度的[折射率](@keyword=refractive_index|lang=zh-CN|style=Feynman) $n$，不再是一个固定的常数，而是变成了原子密度和相互作用参数的函数 ([@problem_id:1039656])。通过调控相互作用，我们简直可以调控气体的[折射率](@keyword=refractive_index|lang=zh-CN|style=Feynman)。

一个更引人注目的例子是[电磁感应透明](@keyword=electromagnetically_induced_transparency|lang=zh-CN|style=Feynman)（EIT）。这是一种量子干涉技巧，人们可以用一束“控制”激光使一团原本不透明的原子云对一束特定频率的“探测”激光变得完全透明。实现这种透明的条件取决于原子两个[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)之间的精确能量差。在[玻色-爱因斯坦凝聚](@keyword=bose_einstein_condensation|lang=zh-CN|style=Feynman)体中，这些能级受到[平均场相互作用](@keyword=mean_field_interaction|lang=zh-CN|style=Feynman)的移动。处于态 $|1\rangle$ 的原子感受到其所有处于态 $|1\rangle$ 的邻居的存在，而一个处于态 $|2\rangle$ 的杂质原子则以不同的方式感受到这些邻居。结果是，透明条件发生了一个位移，其大小与密度 $n$ 和[散射长度](@keyword=scattering_length|lang=zh-CN|style=Feynman)之差 $(a_{12} - a_{11})$ 成正比 ([@problem_id:1989876])。因此，通过调控我们的费什巴赫共振，我们可以移动透明窗口的位置，有效地创造出一个仅由冷气体和光构成的可调谐[光学滤波](@keyword=optical_filtering|lang=zh-CN|style=Feynman)器。

### 新前沿：构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机

或许，可[调相](@keyword=phase_modulation|lang=zh-CN|style=Feynman)互作用最激动人心和最具未来感的应用是在[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)领域。[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的构建单元是[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，或称qubit，一个关键要求是能够使两个qubit以受控的方式相互作用，以执行逻辑门。

在这里，一类新的原子登上了舞台：里德堡原子。这些是电子被激发到非常高能级的原子。它们体积极其巨大——比普通原子大数千倍——并且由于其尺寸，它们具有极强且长程的相互作用。如果我们之前讨论的[短程相互作用](@keyword=short_range_interactions|lang=zh-CN|style=Feynman)像是原子间的碰撞，那么里德堡相互作用更像是可以在数微米范围内感知的强大[力场](@keyword=force_field|lang=zh-CN|style=Feynman)。这种相互作用的强度通常随原子间距离 $R$ 的增加而以 $1/R^6$ 的规律衰减。

这导致了一个被称为**里德堡阻塞**的关键效应。想象两个原子彼此靠近。我们用一束激光照射它们，该激光被调谐以将它们从[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|g\rangle$ 激发到里德堡态 $|r\rangle$。如果我们成功地将第一个原子激发到 $|r\rangle$ 态，它巨大的相互作用场会改变第二个原子的里德堡态能量。此时，激光对于第二个原子来说不再处于共振状态，因此它无法被激发。第一个原子有效地“阻塞”了第二个原子的激发。这是一个天然的条件[逻辑门](@keyword=logic_gates|lang=zh-CN|style=Feynman)：你可以激发原子2，*当且仅当*原子1处于[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。

这种阻塞效应不仅仅是一个理论构想，它可以被直接观察到。例如，在一种称为[奥特勒-汤斯分裂](@keyword=autler_townes_splitting|lang=zh-CN|style=Feynman)的光谱技术中，一束强激光“缀饰”一个[原子跃迁](@keyword=atomic_transitions|lang=zh-CN|style=Feynman)，将单个吸收峰分裂成一个双峰。这个双峰的间距取决于激光的性质。如果我们在测量一个原子的同时，其附近的另一个原子处于里德堡态，[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)移 $C_6/R^6$ 会叠加到激光失谐上，直接改变观测到的双峰分裂情况 ([@problem_id:2039367])。我们简直可以“看到”相互作用在起作用。

这种阻塞机制是许多[中性原子量子计算机](@keyword=neutral_atom_quantum_computer|lang=zh-CN|style=Feynman)中执行双[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)门的基础。更先进的方案则利用我们更精细地调控相互作用的能力。通过使用多束激光来“缀饰”[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)态，使其带有一点里德堡特性，我们可以设计出非常特定的相互作用形式，例如，在创造一种[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的类[磁耦合](@keyword=magnetic_coupling|lang=zh-CN|style=Feynman) ($J_{xy}$) 的同时，将另一种不希望的耦合 ($J_z$) 调谐到恰好为零 ([@problem_id:103964])。我们甚至可以设计复杂的多原子门，其中一个中心原子充当“媒介”，其激光参数被精确调谐，以在两个相邻的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)原子之间产生一个条件相移 ([@problem_id:1265030])。这是控制的终极体现：编排一场复杂的多原子舞蹈，以执行量子算法中的一个特定步骤。

从基础科学到技术前沿，调控原子相互作用是一条贯穿始终的主线。它有力地证明了我们对量子力学的深刻理解如何赋予了我们在最根本的层面上改造世界的空前能力。