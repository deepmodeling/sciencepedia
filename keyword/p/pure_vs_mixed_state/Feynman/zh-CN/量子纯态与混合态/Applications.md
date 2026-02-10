## 应用与跨学科联系：处于某种态中的宇宙

至今，我们已经探讨了将量子世界分为[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)和[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)两种描述的数学机制。纯态，即原始的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)或态矢量 $|\psi\rangle$，代表了知识的顶峰——关于一个量子系统所有可知的信息都包含其中。而[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)，由更繁琐的[密度算符](@keyword=density_operator|lang=zh-CN|style=Feynman) $\rho$ 描述，似乎代表了一种退步，一种对无知的承认。当我们面对一个[统计系综](@keyword=statistical_ensembles|lang=zh-CN|style=Feynman)，一个我们只知道系统处于若干纯态之一的概率的混乱集合时，我们便使用这种描述。

但这就是全部吗？这种区别仅仅是实验制备质量好坏的一个记账笔记吗？或者，它是否揭示了更深层次的东西，一些关于现实本身惊人本质的启示？你或许已经猜到，答案是响亮的“是”。探寻纯态和混合态应用的旅程，将我们从实验室工作台的实际操作，一直带到[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的事件视界。这是一个统一了不同科学领域的故事，揭示了这单一的区别是整个物理学中最强大、最具启发性的概念之一。

### 实验主义者的工具箱：量化量子领域的无知

让我们从实验室开始。如果一个理论家交给你一个本应产生特定[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的设备，你如何检查它是否正常工作？你不能简单地“看”一下态矢量。量子世界不会如此轻易地泄露它的秘密。相反，你必须通过测量来探询它。这个过程，被称为**[量子态层析](@keyword=quantum_state_tomography|lang=zh-CN|style=Feynman)**，是从实验数据中重建[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的艺术。

想象一下，这个系统是一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)的[基本单位](@keyword=fundamental_units|lang=zh-CN|style=Feynman)。它的状态可以被看作是在一个半径为1的球体（著名的[布洛赫球面](@keyword=bloch_sphere|lang=zh-CN|style=Feynman)）上或其内部的一个点。球面上的任何一点都对应一个[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)。球体*内部*的任何一点都代表一个混合态。位于正中心，坐标为 $(0,0,0)$ 的点，是[最大混合态](@keyword=maximally_mixed_state|lang=zh-CN|style=Feynman)——一种完全无知的状态，是所有可能性等概率的统计混合。

为了找出我们的态在哪里，我们对一个经相同方式制备的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)系综进行了大量测量。我们测量自旋沿三个正交轴——$x$, $y$, $z$——的平均值，即[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)。这些值 $\langle \sigma_x \rangle = a$, $\langle \sigma_y \rangle = b$ 和 $\langle \sigma_z \rangle = c$，给了我们态的[布洛赫矢量](@keyword=bloch_vector|lang=zh-CN|style=Feynman) $\mathbf{p} = (a, b, c)$ 的坐标。然后我们可以计算一个关键量，即*纯度* $\gamma = \mathrm{Tr}(\rho^2)$。对于单个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，这原来是我们测量值的一个简单而优雅的函数：$\gamma = \frac{1}{2}(1+a^2+b^2+c^2)$ [@problem_id:2110376]。如果我们测量的矢量长度的平方 $|\mathbf{p}|^2 = a^2+b^2+c^2$ 等于 1，那么 $\gamma=1$，我们的态就是纯态——它位于球面上。如果 $|\mathbf{p}| \lt 1$，那么 $\gamma \lt 1$，我们的态就是[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)，位于球体内部的某个位置。离中心的距离直接告诉我们态有多“纯”。

这不仅仅是[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)中的一个抽象练习。完全相同的原理也应用于[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)。在旨在利用电子自旋进行信息处理的[自旋电子学](@keyword=spintronics|lang=zh-CN|style=Feynman)领域中，穿过材料的电子的[自旋极化](@keyword=spin_polarization|lang=zh-CN|style=Feynman)程度，正是用同样的[布洛赫矢量](@keyword=bloch_vector|lang=zh-CN|style=Feynman)形式体系来描述的。[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)[态的纯度](@keyword=purity_of_a_state|lang=zh-CN|style=Feynman)是决定自旋电子器件效率的关键参数 [@problem_id:2525138]。这些概念如此普适，以至于一个源于量子信息理论的方程，在凝聚态物理学中找到了直接的用武之地。

这种“混合性”最初从何而来？它可以源于简单的、类似经典的不确定性。也许量子光学实验中的一个光源不稳定，一半时间产生真空态 $|0\rangle$，另一半时间产生[压缩真空态](@keyword=squeezed_vacuum_state|lang=zh-CN|style=Feynman) $|r\rangle$。由此产生的态是两者的非相干统计混合 [@problem_id:710800]。或者，在使用[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)研究的化学溶液中，不同的分子可能处于略有不同的局部电场或“微环境”中，导致我们必须用[密度算符](@keyword=density_operator|lang=zh-CN|style=Feynman)来描述的一个[统计系综](@keyword=statistical_ensembles|lang=zh-CN|style=Feynman) [@problem_id:2829838]。这种混合性本质上是对我们无法完美控制每一个变量的承认。但还有另一种更奇怪的混合性来源。

### 来自更大世界的混合态：纠缠之影

准备好进行一次概念上的飞跃。一个量子系统可以表现为[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)，即使没有任何经典不确定性，没有不稳定的设备，也没有任何[统计系综](@keyword=statistical_ensembles|lang=zh-CN|style=Feynman)。这种情况发生在我们正在观察的系统与另一个我们*没有*观察的系统**纠缠**在一起的时候。混合性源于纯粹的量子联系。

想象 Alice 和 Bob 共享一对处于一个完美定义的[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)中的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，比如著名的[单重态](@keyword=singlet_state|lang=zh-CN|style=Feynman) $|\psi^-\rangle = \frac{1}{\sqrt{2}}(|01\rangle - |10\rangle)$。整个系统被完全确定地了解。但如果 Alice 在她的实验室里孤立地尝试描述*她自己那个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)*的状态呢？她无法接触到 Bob 的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。为了找到她子系统的状态，她必须执行一个叫做[偏迹](@keyword=partial_trace|lang=zh-CN|style=Feynman)的数学操作——她必须对 Bob 未被观察的那一半的所有可能性进行平均。

结果是惊人的。她的单个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的状态是[最大混合态](@keyword=maximally_mixed_state|lang=zh-CN|style=Feynman)！其[布洛赫矢量](@keyword=bloch_vector|lang=zh-CN|style=Feynman)位于球体的中心，$\mathbf{p} = (0,0,0)$。她对整体的完美认知，已经消解为对局部的完全无知。这是一个深刻的真理：对于一个纠缠系统，子系统的状态通常是混合的 [@problem_id:112209]。子系统的纯度，实际上是它与世界其他部分纠缠程度的度量。一个纯的子系统意味着它根本没有纠缠（它处于一个乘积态），而一个最大混合子系统则意味着它是最大程度纠缠的。我们对子系统的“无知”是其与另一部分量子关联的直接后果。

这个想法有一个优美的几何体现。考虑 Werner 态，这是一个由一个纯[纠缠态](@keyword=entangled_state|lang=zh-CN|style=Feynman)和一个[最大混合态](@keyword=maximally_mixed_state|lang=zh-CN|style=Feynman)混合而成的态，由一个“可见度”参数 $p$ 控制 [@problem_id:504004]。当 $p=1$ 时，该态是纯[单重态](@keyword=singlet_state|lang=zh-CN|style=Feynman)。当 $p=0$ 时，它是最大混合噪声。对于中间值，它是一个部分纯的、纠缠的态。Alice 可以对她的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)进行测量，并根据她的选择和结果，“导引”Bob 的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)进入各种状态。她能将 Bob 的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)导引到的所有状态的集合，在布洛赫球面内部形成一个实心[椭球体](@keyword=ellipsoid|lang=zh-CN|style=Feynman)。这个“导引[椭球](@keyword=ellipsoid|lang=zh-CN|style=Feynman)”的体积是纠缠资源的直接度量。对于[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman) ($p=1$)，体积是最大的。随着态变得更加混合（$p$ 减小），[椭球](@keyword=ellipsoid|lang=zh-CN|style=Feynman)收缩。对于[最大混合态](@keyword=maximally_mixed_state|lang=zh-CN|style=Feynman) ($p=0$)，体积为零——Alice 失去了影响 Bob 状态的所有能力。纯度这个抽象概念变成了一个代表控制能力的可触及的几何体积。

### 宏[大统一](@keyword=grand_unification|lang=zh-CN|style=Feynman)：纯化与作为纯态的宇宙

我们已经看到，纠缠可以是混合性的一个来源。现在，让我们反过来问一个问题：*每一个*[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)是否都可以被理解为一个更大的、纯[纠缠态](@keyword=entangled_state|lang=zh-CN|style=Feynman)的一部分？令人难以置信的是，答案是肯定的。这就是**纯化**的概念，它为我们对世界的量子描述提供了一个深刻而强大的统一。

任何描述系统 S 的[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman) $\rho_S$ 都可以数学上表示为一个更大[希尔伯特空间](@keyword=hilbert_spaces|lang=zh-CN|style=Feynman)中纯态 $|\Psi\rangle$ 的[偏迹](@keyword=partial_trace|lang=zh-CN|style=Feynman)，这个大空间由我们的系统 S 和一个虚构的“辅助”系统 A 组成。换句话说，$\rho_S = \mathrm{Tr}_A(|\Psi\rangle\langle\Psi|)$。我们那个混乱的、统计性的[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)总是可以被看作是一个更大现实中一个干净、确定的[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)的一部分。混合性只是我们因对[辅助系统](@keyword=ancilla_system|lang=zh-CN|style=Feynman)“视而不见”而付出的代价。

这不仅仅是某种哲学上的空谈。它是一个具有巨大实用价值的工具。例如，在[理论化学](@keyword=theoretical_chemistry|lang=zh-CN|style=Feynman)中，科学家们希望模拟分子在有限温度下的动力学。处于热平衡的系统处于一个典型的混合态 $\rho \propto \exp(-\beta \hat{H})$。许多强大的计算方法，如多组态时间依赖 Hartree (MCTDH) 方法，是为处理纯态[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)而非密度矩阵而设计的。纯化技巧提供了解决方案：他们不是模拟 $f$ 模态分子的[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)，而是模拟一个扩大的 $2f$ 模态“系统+辅助”空间中的纯态。通过在这个更大的纯态上进行[时间演化](@keyword=time_evolution|lang=zh-CN|style=Feynman)，然后在最后追踪掉[辅助系统](@keyword=ancilla_system|lang=zh-CN|style=Feynman)，他们可以完美地恢复原始混合[热态](@keyword=thermal_states|lang=zh-CN|style=Feynman)的动力学 [@problem_id:2818023]。一个概念上的突破促成了一个计算上的突破。

这引出了一个令人叹为观止的提议。也许我们在现实世界中遇到的每一个[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)——来自退相干，来自[热噪声](@keyword=johnson_nyquist_noise|lang=zh-CN|style=Feynman)，来自任何“经典”无知的来源——最终都只是我们对一个大得多的、完美纯净的宇宙[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的有限视角的反映。

### 宇宙学联系：[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)与信息的本质

让我们将这个想法带到它最宏大的舞台：宇宙本身。理论物理学中最惊人的发现之一是，纯态和[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)之间的区别，是理解[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的核心。

根据[弯曲时空中的量子场论](@keyword=quantum_field_theory_in_curved_spacetime|lang=zh-CN|style=Feynman)，一个永恒[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)（Hartle-Hawking 态）附近的真空态是一个单一的、普适的[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)。关键在于，这个真空中充满了跨越[黑洞事件视界](@keyword=black_hole_event_horizon|lang=zh-CN|style=Feynman)纠缠在一起的[虚粒子](@keyword=virtual_particles|lang=zh-CN|style=Feynman)对。存在视界内部的[场模](@keyword=field_modes|lang=zh-CN|style=Feynman)式，它们永远与我们因果分离；也存在外部的场模式。

现在，考虑一个生活在[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)之外的观察者。她无法接触到内部的模式。就像 Alice 必须对 Bob 的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)进行追踪一样，我们的观察者必须对纠缠真空场的内部模式进行追踪。她会看到什么？对一个纯[纠缠态](@keyword=entangled_state|lang=zh-CN|style=Feynman)的一半进行[偏迹](@keyword=partial_trace|lang=zh-CN|style=Feynman)会产生一个[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)。在这个特殊而显著的案例中，外部观察者得到的最终状态是一个完美的**热[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)** [@problem_id:74142]。

这就是**霍金辐射**的起源。[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)似乎发出[热辐射](@keyword=thermal_radiation|lang=zh-CN|style=Feynman)，不是因为它在经典意义上是热的，而是因为时空结构本身就是由纠缠的量子场编织而成的，而[事件视界](@keyword=event_horizon|lang=zh-CN|style=Feynman)就像一道基本的帷幕，将部分现实对我们隐藏起来。[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的“热”是[量子纠缠](@keyword=quantum_entanglement|lang=zh-CN|style=Feynman)的一种体现。我们看到的辐射的混合性，是底层纠缠真空纯度的直接后果。我们用来分析实验室中一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的工具，如纯度和[纠缠度量](@keyword=entanglement_measures|lang=zh-CN|style=Feynman)，可以用来计算[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)性质。

### 一条贯穿现实的线索

我们的旅程结束了。我们从一个实际问题开始：我们如何判断一个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)是否被完美知晓？这引导我们了解了实验主义者的层析工具箱。然后我们发现了一个更深、更奇怪的无知来源：纠缠投下的量子阴影。这揭示了一个[态的纯度](@keyword=purity_of_a_state|lang=zh-CN|style=Feynman)与其提供的资源能力之间的优美对应关系。接着，我们用纯化的概念统一了这两种混合性的来源，提出如果我们能看到全局，那么每一个态都是纯的。最后，我们看到这个宏伟的想法在宇宙尺度上上演，解释了[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)神秘的光芒。

[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)与混合态之间的区别，起初似乎只是一个技术细节，但它已被证明是一条金线。它将量子信息、凝聚态物理学、计算化学和引力物理学编织在一起。这是一个量化我们的知识、衡量我们的资源并照亮物理宇宙最深层联系的概念。它告诉我们，我们所看到的这个混乱的、统计性的世界，或许仅仅是我们对于一个单一、浩瀚且完美纯净的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的有限视角。