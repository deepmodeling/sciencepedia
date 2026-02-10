## 应用与跨学科联系

在上一章中，我们进行了一次奇妙的数学炼金术。我们将熟悉的、永远前行的坐标——时间 $t$，大胆地旋转到[复平面](@keyword=complex_plane|lang=zh-CN|style=Feynman)中，用一个虚构的对应物 $\tau$ 取代了它。曾经描述无尽量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的薛定谔方程，转变成了类似于扩散方程的东西，描述着衰减与沉降。你可能会倾向于认为这不过是一个形式上的技巧，一种巧妙的计算便利。在某种程度上，你是对的！但这是一个后果如此深远的技巧，一把能打开如此多扇隐藏之门的钥匙，以至于沿着它的路径前行，就如同进行一次现代物理学的盛大巡礼。它揭示了量子世界、热学理论、乃至引力本质之间惊人的、隐秘的统一。那么，让我们踏上这段旅程，看看这个“虚构”的时间[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)我们走多远。

### 终极冷却系统：寻找[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)

[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)最直接、最直观的应用，或许是它作为一种“[量子冷却](@keyword=quantum_cooling|lang=zh-CN|style=Feynman)”机制的角色。想象你拨动一根吉他弦。在实时中，它以其基频音和许多更高音调、能量更高的谐波的丰富组合进行[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。现在，想象一个过程，它能选择性地比低能量[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)更快地抑制高能量[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。那些狂乱的、高频的摆动会几乎瞬间消失，留下纯净、深沉的[基频](@keyword=fundamental_frequency|lang=zh-CN|style=Feynman)音回响。

这正是[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)对量子系统所做的事情。任何任意的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)都可以被看作是许多能量本征态的叠加，就像吉他的声音是谐[波的叠加](@keyword=wave_superposition|lang=zh-CN|style=Feynman)一样。通过算符 $\exp(-\hat{H}\tau/\hbar)$ 在虚时中演化这个态，会相对于低能量分量指数级地抑制[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的高能量分量。随着虚时 $\tau$ 的推移，系统通过摆脱其[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)而“冷却”，不可逆转地弛豫到其最低能量的构型：[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。

这不仅仅是一个漂亮的类比；它是[计算物理学](@keyword=computational_physics|lang=zh-CN|style=Feynman)和化学中一个强大而实用的工具。当面对一个复杂的分子或一种新颖的材料时，首要且最重要的问题之一是：它最稳定的构型是什么？找到这个[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)对于理解[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)、[反应速率](@keyword=reaction_rates|lang=zh-CN|style=Feynman)和[材料性质](@keyword=material_properties|lang=zh-CN|style=Feynman)至关重要。[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)提供了一个优雅的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)来找到它。科学家们可以从对系统[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的任何合理猜测开始，在模拟中重复应用[虚时传播](@keyword=imaginary_time_propagation|lang=zh-CN|style=Feynman)子，然后观察它如何收敛到真正的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，有效地过滤掉所有其他可能性。

这个曾经属于经典超级计算机领域的想法，现在正被应用于下一代硬件：[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机。在一个激动人心的新方法中，诸如量子[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)（QITE）之类的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)直接操纵[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，以在量子处理器上模拟这种冷却过程。这种混合量子-经典方法有望为寻找那些即使是我们最好的经典机器也无法处理的复杂系统的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)提供一种新途径，可能彻底改变药物发现和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)。

### 驯服无穷大：量子[场论](@keyword=field_theory|lang=zh-CN|style=Feynman)的工具

当我们从单个粒子的量子力学转向量子场论（QFT）的狂野[世界时](@keyword=universal_time|lang=zh-CN|style=Feynman)，挑战急剧升级。QFT描述了基本粒子如何被创造和湮灭，其计算常常涉及对在真空中瞬间出现又消失的“虚”粒子的贡献求和。这些贡献以对所有可能动量的可怕积分的形式出现，并且它们因发散到无穷大而臭名昭著。

在普通（闵可夫斯基）[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中，这些积分的景观是险恶的，充满了与实粒子产生相对应的数学极点，使得计算成为一场技术噩梦。正是在这里，我们那个被称为**威克转动**的虚时技巧创造了一个小小的奇迹。通过将四动量的能量分量解析延拓到[复平面](@keyword=complex_plane|lang=zh-CN|style=Feynman)，$k^0 \to i k_E^4$，我们有效地旋转了计算的几何结构。[闵可夫斯基时空](@keyword=minkowski_spacetime|lang=zh-CN|style=Feynman)的复杂、[双曲几何](@keyword=hyperbolic_geometry|lang=zh-CN|style=Feynman)被转变为一个简单、行为良好的四维欧几里得空间。

这一举动产生了巨大的影响。曾经可怕的[振荡函数](@keyword=oscillating_functions|lang=zh-CN|style=Feynman)积分变成了指数衰减函数的积分，后者在计算上要稳定得多，也更容易处理。突然之间，描述粒子间基本相互作用的令人生畏的[圈图计算](@keyword=loop_calculation|lang=zh-CN|style=Feynman)变得易于处理。这项技术不仅仅是为了让数学变得更容易；它为处理出现的无穷大提供了一个数学上健全且定义良好的框架，这个过程物理学家称之为[正则化](@keyword=regularization|lang=zh-CN|style=Feynman)。威克转动是现代[理论物理学](@keyword=theoretical_physics|lang=zh-CN|style=Feynman)家工具箱中一个标准且不可或缺的工具。它的威力是如此普遍，以至于从[粒子物理学](@keyword=particle_physics|lang=zh-CN|style=Feynman)的标准模型一直延伸到[弦理论](@keyword=string_theory|lang=zh-CN|style=Feynman)的前沿，在[弦理论](@keyword=string_theory|lang=zh-CN|style=Feynman)中，同样的想法被用来理解振动弦在其二维“世界面”上的量子行为。

### 从时间到温度：[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的联系

现在我们到达了问题的核心，数学技巧在这里揭示了自己是一个深刻的物理原理。让我们再看看[虚时演化](@keyword=imaginary_time_evolution|lang=zh-CN|style=Feynman)算符 $\exp(-\hat{H}\tau/\hbar)$。它看起来熟悉吗？应该很熟悉！它在形式上与整个[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学中最重要的表达式——玻尔兹曼因子 $\exp(-\hat{H}/(k_B T))$——完全相同。这个因子决定了一个物理系统在与温度为 $T$ 的热浴处于[热平衡](@keyword=thermal_balance|lang=zh-CN|style=Feynman)时，处于特定能量状态的概率。

这并非巧合。这是一个深刻等价的标志：**一个在虚时中周期性演化的量子系统（周期为 $\beta$），在数学上与一个处于[热平衡](@keyword=thermal_balance|lang=zh-CN|style=Feynman)、温度为 $T$ 的[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学系统是无法区分的，其周期与温度由著名的关系式给出：**
$$
\beta = \frac{\hbar}{k_B T}
$$
这一惊人的联系意味着，整个量子[路径积分](@keyword=path_integration|lang=zh-CN|style=Feynman)的形式可以被重新用于研究[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)。最初由 Feynman 构想，用于对粒子从一点移动到另一点的所有可能[历史求和](@keyword=sum_over_histories|lang=zh-CN|style=Feynman)的路径积分，可以被重新解释。如果我们将路径限制在虚时中以周期 $\beta$ 呈周期性，路径积分就不再计算[量子跃迁振幅](@keyword=quantum_transition_amplitudes|lang=zh-CN|style=Feynman)。相反，它计算的是相应温度 $T$ 下[热力学系统](@keyword=thermodynamic_systems|lang=zh-CN|style=Feynman)的**配分函数**。

[配分函数](@keyword=sum_over_states_2|lang=zh-CN|style=Feynman)是[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的圣杯；从它出发，可以推导出系统的所有[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)性质：它的自由能、熵、压强和[比热](@keyword=specific_heat|lang=zh-CN|style=Feynman)。这座桥梁让我们能够探究，例如，一个粒子[热浴](@keyword=heat_bath|lang=zh-CN|style=Feynman)的存在如何影响其他粒子的性质，比如它们的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)。这不仅仅是一个学术问题；它对于理解早期宇宙灼热状态下或重离子对撞机内部的物质状态至关重要。量子[动力学与[热力](@keyword=kinetics_vs_thermodynamics|lang=zh-CN|style=Feynman)学](@article_id:359663)之间的桥梁，正是用虚时构建的。

### 引力、几何与[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)：盎鲁效应与[霍金效应](@keyword=hawking_effect|lang=zh-CN|style=Feynman)

这段旅程在最壮观、最出人意料的景观中达到高潮：量子理论与广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的交汇处。让我们首先考虑一个观察者，他正在均[匀加速](@keyword=uniform_acceleration|lang=zh-CN|style=Feynman)地穿过一个惯性（或自由漂浮）观察者所谓的真空。根据爱因斯坦的理论，这个[加速观察者](@keyword=accelerating_observer|lang=zh-CN|style=Feynman)的时空几何由 Rindler 度规描述。如果我们对这个度规进行我们现在熟悉的威克转动，一个奇特的特征出现了。由此产生的欧几里得空间看起来几乎像一个平面，但在观察者的原点处有一个“尖锐”的缺陷——一个[锥形奇点](@keyword=cone_singularity|lang=zh-CN|style=Feynman)。

为了使几何平滑且规则，正如我们相信[时空结构](@keyword=spacetime_structure|lang=zh-CN|style=Feynman)必须是的那样，我们被迫要求虚时坐标是周期性的。事实证明，所需的周期是由观察者的加速度 $\alpha$ 决定的。而我们刚刚学到了周期性虚时意味着什么？一个温度！这导出了一个惊人的结论，即**盎鲁效应**：一个加速的观察者感知的不是空无一物的空间。他们发现自己沉浸在一个由粒子组成的温暖浴场中，其温度与他们的加速度成正比。当你加速穿过真空时，真空本身会变热！

这个发现虽然听起来很奇怪，但却是通往一个关于[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)本质的更伟大启示的关键垫脚石。在[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的[事件视界](@keyword=event_horizon|lang=zh-CN|style=Feynman)附近，时空结构被拉伸得如此之剧烈，以至于对于一个被固定在那里的静止观察者来说，其几何与[加速观察者](@keyword=accelerating_observer|lang=zh-CN|style=Feynman)的 Rindler 几何非常相似。沿着这条思路，物理学家 Stephen Hawking 提出了一个问题：如果将威克转动应用于[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的 Schwarzschild 度规会发生什么？

答案是相同的。为了避免[事件视界](@keyword=event_horizon|lang=zh-CN|style=Feynman)处几何中的[锥形奇点](@keyword=cone_singularity|lang=zh-CN|style=Feynman)，虚时坐标*必须*被视为周期性的。这个必需的周期 $\beta = 8 \pi G M / c^3$，当用我们的时间-温度关系转换回来时，意味着[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)具有一个特定的、非零的温度。这就是**霍金辐射**这一深刻发现的起源。长期以来被认为是终极宇宙监狱、任何东西都无法逃脱的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)，实际上是[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)物体。它们发出微弱的热量，并在天文尺度的时间里缓慢地辐射掉它们的质量。这一美丽的见解，统一了广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)、[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)和量子力学，都源于一个简单的要求：[时空](@keyword=space_time|lang=zh-CN|style=Feynman)在旋转到虚时后，其几何必须是行为良好的。

### 结论

于是我们的旅程结束了。我们从一个看似数学障眼法的东西开始——将时间侧转。但这一个奇特的步骤却带领我们走遍了四方。它作为一种冷却系统，帮助我们找到物质的最低能量状态，无论是在我们的计算机里，还是在未来的量子芯片上。它驯服了量子[场论](@keyword=field_theory|lang=zh-CN|style=Feynman)中狂野的积分，使我们能够计算基本粒子的性质。然后，它揭示了其真实身份，即连接量子世界与热学及温度科学的万能钥匙。最后，在[弯曲时空](@keyword=curved_spacetime|lang=zh-CN|style=Feynman)的领域，它为加速的观察者点燃了真空中的火焰，并为[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的事件视界披上了一层热辉。

虚时的故事是自然法则内在联系的一个美丽例证。它表明，有时最“不真实”的概念可以引导我们走向关于物理世界最深刻的真理。它证明了一个事实：在物理学中，对数学优雅性和一致性的追求，常常引导我们发现宇宙最深邃的秘密。