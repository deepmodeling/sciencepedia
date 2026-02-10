## 引言
在物理学领域，很少有现象能像[超流性](@keyword=superfluidity|lang=zh-CN|style=Feynman)一样，在人类尺度上如此生动地展示量子世界的奇异规则。这种非凡的[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)最著名的例子是在接近绝对零度的液氦中观察到的，它能无任何摩擦或黏度地流动，完全违背了日常直觉。但是，一个原子集合体是如何自发地决定作为一个单一、完美协调的实体来行动的？是什么样的基本原理支配着这种奇特的转变？在宇宙的其他地方，这些规则是否也同样适用？本文将开启一段揭开这一量子奇迹神秘面纱的旅程。

我们将在“原理与机制”一节中，首先绘制出氦的独特相图，揭示其向超[流态](@keyword=flow_regimes|lang=zh-CN|style=Feynman)转变的本质。我们将探讨[玻色-爱因斯坦凝聚](@keyword=bose_einstein_condensation|lang=zh-CN|style=Feynman)的微观奥秘，以及解释[量子化涡旋](@keyword=quantized_vortices|lang=zh-CN|style=Feynman)和[无摩擦流动](@keyword=frictionless_flow|lang=zh-CN|style=Feynman)等现象的强大[双流体模型](@keyword=two_fluid_model|lang=zh-CN|style=Feynman)。随后，“应用与跨学科联系”一节将拓宽我们的视野，揭示[超流性](@keyword=superfluidity|lang=zh-CN|style=Feynman)的概念并不仅限于实验室的杜瓦瓶中。我们将看到，这些思想如何为凝聚态系统、[中子星](@keyword=neutron_stars|lang=zh-CN|style=Feynman)内部的奇异物理学提供关键见解，甚至为真空的基本结构提供深刻的类比，从而展示这场优美的量子之舞的深远影响。

## 原理与机制

要真正理解一种新现象，我们必须首先绘制出它的“疆域图”。对于像[液氦](@keyword=liquid_helium|lang=zh-CN|style=Feynman)这样的物质，这张图就是它的**相图**——一个告诉我们在任意温度和压力下它将处于何种状态（气态、液态或固态）的图表。但氦的[相图](@keyword=phase_portraits|lang=zh-CN|style=Feynman)与众不同，这是我们进入一个由奇异新规则支配的世界的第一个线索。

### 通往量子世界的路线图：[相图](@keyword=phase_portraits|lang=zh-CN|style=Feynman)

让我们开启一段旅程。想象我们有一个装有氦气的容器，然后开始给它降温。如果我们将压力保持在很低的水平，比如大约 $4.5 \text{ kPa}$（约大气压的4%），就会发生一些奇特的事情。当我们从温暖的 $6 \text{ K}$ 经过冷凝点继续降温时，气体并没有变成普通的液体，而是直接[凝结](@keyword=coagulation|lang=zh-CN|style=Feynman)成超[流态](@keyword=flow_regimes|lang=zh-CN|style=Feynman)，即**氦-II** [@problem_id:1997198]。它完全绕过了成为“正常”液体的阶段。

现在，让我们尝试另一条路径。假设我们将氦气加压到 $20 \text{ atm}$，并从温和的 $10 \text{ K}$ 开始冷却。在这个远高于氦[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)（$2.24 \text{ atm}$ 和 $5.2 \text{ K}$）的压力下，气体和液体之间的区别已经消失了。我们进入了**超临界流体**的领域。当我们冷却它时，它不会突然[凝结](@keyword=coagulation|lang=zh-CN|style=Feynman)，而是平滑连续地变得更稠密、更像液体，转变为称为**氦-I**的正常液相。但我们的旅程尚未结束。当我们继续冷却，经过一个非常特定的温度（在此压力下约为 $1.9 \text{ K}$）时，液体会经历另一次更微妙的转变。它变成了氦-II，即[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman) [@problem_id:1868644]。

这两段旅程揭示了[氦相图](@keyword=helium_phase_diagram|lang=zh-CN|style=Feynman)的一个关键特征：一条分隔正常液体（氦-I）和超流液体（氦-II）的界线。这条边界被称为**[λ线](@keyword=lambda_line|lang=zh-CN|style=Feynman)**。再注意一个非同寻常之处：在这张图上，在日常压力下，固、液、气三相没有交汇点。氦是唯一一种无论多冷，在其自身蒸气压下都不会凝固的元素。你必须用超过 $25 \text{ atm}$ 的压力挤压它，才能迫使其固化。这种对[凝固](@keyword=coagulation|lang=zh-CN|style=Feynman)的“抗拒”是我们得到的第一个重要暗示：量子力学正在宏观尺度上发挥作用。

### 一种别样的转变：[λ点](@keyword=lambda_point|lang=zh-CN|style=Feynman)

水沸腾时，需要在固定温度下持续输入能量——即[潜热](@keyword=latent_heat|lang=zh-CN|style=Feynman)——才能从液体转变为蒸汽。这是一种经典的**一级相变**，一个剧烈而明显的变化。而从正常氦-I到[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)-II的转变则完全不同。

如果你观察一个正在冷却的液氦容器，你会看到它剧烈地沸腾。然后，当它穿过[λ线](@keyword=lambda_line|lang=zh-CN|style=Feynman)时，沸腾会突然、诡异地停止。液体变得完全静止。没有气泡，没有骚动。这是因为这个转变没有**[潜热](@keyword=latent_heat|lang=zh-CN|style=Feynman)**。变化是连续的。

然而，如果你去测量液体储存热量的能力——即它的**[比热](@keyword=specific_heat|lang=zh-CN|style=Feynman)**——你会看到一个非凡的现象。当温度接近转变点时，比热急剧上升，形成一个尖锐的峰，形状酷似希腊字母λ（$\lambda$），该转变也因此得名。

这种行为——没有潜热，同时比热出现[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)——告诉物理学家，超流[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)是一种**[二级相变](@keyword=second_order_transition|lang=zh-CN|style=Feynman)** [@problem_id:1994351]。这是物质本身一种更微妙、更深刻的[重排](@keyword=derangement|lang=zh-CN|style=Feynman)。系统不仅仅像沸水那样改变密度，而是在改变其基本对称性。就好像一群随意走动的人群，在没有任何指令的情况下，突然开始以完美的统一步调齐步前进。

### 量子奥秘：[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)的交响乐

那么，这种奇怪行为背后的微观奥秘是什么？答案在于氦原子本身的量子身份。宇宙将所有粒子分为两大家族：**[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)**和**[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)**。[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)，如电子和[氦-3](@keyword=helium_3|lang=zh-CN|style=Feynman)原子，是“不合群的个人主义者”。它们受**[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)**的支配，该原理禁止任意两个[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)占据相同的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。它们坚持要有自己的空间。

而[氦-4](@keyword=helium_4|lang=zh-CN|style=Feynman)原子则是**[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)**。[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)是“社交性的”。它们不仅可以共享同一[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，而且*更倾向于*这样做。当你冷却一团[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)气体时，它们的量子性变得更加显著。当达到一个临界温度时，大部分原子会突然放弃其个体身份，集体跌落到可用的单一最低能量[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)中。这种集体“沉陷”被称为**玻色-爱因斯坦凝聚 (BEC)**。这些原子开始作为一个单一的、巨大的“[超原子](@keyword=superatoms|lang=zh-CN|style=Feynman)”行动，由一个单一、相干的[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)来描述。

这是否就是超流性背后的机制呢？让我们来验证一下。如果我们将液氦建模为一个简单的、无相互作用的[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)气体，并计算BEC应该发生的温度，我们得到的值约为 $3.14 \text{ K}$ [@problem_id:1356426]。而实际的转变发生在 $2.17 \text{ K}$。考虑到我们的模型完全忽略了稠密液体中原子间的[强相互作用](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)，这个结果已经惊人地接近了！这种一致性有力地表明，[玻色-爱因斯坦凝聚](@keyword=bose_einstein_condensation|lang=zh-CN|style=Feynman)确实是氦-4中[超流性](@keyword=superfluidity|lang=zh-CN|style=Feynman)的根本驱动力。预测温度与实际温度之间的差异，只是一个现实的提醒：[氦原子](@keyword=helium_atom|lang=zh-CN|style=Feynman)并[非理想气体](@keyword=non_ideal_gases|lang=zh-CN|style=Feynman)；它们会相互推挤和作用，从而略微改变了凝聚的条件。

这也优雅地解释了为什么由[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)构成的[液氦-3](@keyword=liquid_helium_3|lang=zh-CN|style=Feynman)行为如此不同。它的原子被禁止以同样的方式凝聚。要使[氦-3](@keyword=helium_3|lang=zh-CN|style=Feynman)成为[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)，[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)原子必须首先配对（其方式类似于[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中的电子）形成[复合玻色子](@keyword=composite_bosons|lang=zh-CN|style=Feynman)，这是一个更为精细的过程，只在低上千倍的温度下才会发生 [@problem_id:1994399]。

### 一体双流：量子行为的模型

我们如何描述一种部分是凝聚体、部分是无序原子的物质？杰出的**[双流体模型](@keyword=two_fluid_model|lang=zh-CN|style=Feynman)**设想氦-II的行为*仿佛*是两种相互[渗透](@keyword=permeation|lang=zh-CN|style=Feynman)的液体的混合物：

1.  **超流体组分**，由所有处于集体[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的原子组成。这种流体黏度为零，并且值得注意的是，其熵也为零。它是最纯粹、最有序形式的量子力学。
2.  **正常流体组分**，由其余处于[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)（称为“[声子](@keyword=phonons|lang=zh-CN|style=Feynman)”和“[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)”的[热激发](@keyword=thermal_excitation|lang=zh-CN|style=Feynman)）的原子组成。这种流体的行为像普通液体，具有黏度并携带系统的所有热量。

这是一个关键点：它们不是两种可以用过滤器分离的化学上不同的物质。[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)始终是由相同的氦-4原子构成的纯元素 [@problem_id:1983830]。[双流体模型](@keyword=two_fluid_model|lang=zh-CN|style=Feynman)是一个强大的理论工具，一种将有序的、量子相干的行为（[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)）与无序的、热学的行为（正常流体）分离开来的方法。在绝对零度下，液体将是100%的[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)。随着温度向[λ点](@keyword=lambda_point|lang=zh-CN|style=Feynman)升高，正常流体组分的比例以牺牲[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)组分为代价而增加，直到在 $T_\lambda$ 时，整个流体都变为“正常”流体。

一种更严谨的描述方式是通过**序参量**，这是一个在无序相（氦-I）中为零、在有序相（氦-II）中非零的数学量。对于[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)，序参量是一个**宏观复数[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)**，通常写作 $\Psi(\vec{r}) = \sqrt{n_s(\vec{r})} \exp(i\theta(\vec{r}))$。这个函数的大小 $\sqrt{n_s}$ 告诉我们[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)组分的密度，而它的相位 $\theta(\vec{r})$ 则掌握着其许多最奇异性质的秘密 [@problem_id:1958176]。在[λ点](@keyword=lambda_point|lang=zh-CN|style=Feynman)以下，这个[宏观波函数](@keyword=macroscopic_wavefunction|lang=zh-CN|style=Feynman)的自发出现代表了物理学中一个深刻的概念：**自发对称性破缺**。

### “超”的标志：[无摩擦流动](@keyword=frictionless_flow|lang=zh-CN|style=Feynman)与量子漩涡

有了这个理论框架，我们终于可以理解超流体的标志性行为了。

**零黏度：** 为什么超流体可以无摩擦地流动？物理学家Lev Landau提出了一个绝妙的论证。想象一个物体在流体中运动。要使其感受到阻力，它必须能够通过在流体中产生一个激发——比如一个微小的[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)那样的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)——来耗散能量。然而，根据严格的能量和动量守恒定律，这只有在物体运动速度超过某个**[临界速度](@keyword=critical_velocity|lang=zh-CN|style=Feynman)**时才可能发生。低于这个速度，根本无法产生激发。这在能量上和运动学上都是被禁止的。因此，没有能量损失的机制，物体运动时完全没有阻力 [@problem_id:1893291]。临界速度由流体的[元激发](@keyword=elementary_excitations|lang=zh-CN|style=Feynman)决定，并由著名的[朗道判据](@keyword=landau_criterion|lang=zh-CN|style=Feynman)给出：$v_c = \min_{p>0}(\epsilon(p)/p)$，其中 $\epsilon(p)$ 是动量为 $p$ 的激发的能量。

**[量子化涡旋](@keyword=quantized_vortices|lang=zh-CN|style=Feynman)：** 如果你试着旋转一桶普通的水，整桶水会一起旋转。但如果你试着旋转一桶[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)，它最初会保持完全静止。当你转得更快时，流体最终会“屈服”，但方式却异想天开。它会产生一系列微小、相同的漩涡，称为**[量子化涡旋](@keyword=quantized_vortices|lang=zh-CN|style=Feynman)**。每个涡旋都是一个流体在其中环流的微观龙卷风。宏观量子波函数 $\Psi$ 必须是单值的这一要求，意味着围绕任何此类涡旋的环流不能是任意值；它必须是某个基本常数——**[环流量子](@keyword=quantum_of_circulation|lang=zh-CN|style=Feynman)** $\kappa = h/m$ 的整数倍，其中 $h$ 是普朗克常数， $m$ 是单个氦原子的质量 [@problem_id:1994383]。这是量子力学支配大块流体行为的一个惊人证明。整个流体的旋转是通过不断增加这些相同的、量子化的漩涡来实现的。

**[第二声](@keyword=second_sound|lang=zh-CN|style=Feynman)：** 或许对[双流体模型](@keyword=two_fluid_model|lang=zh-CN|style=Feynman)最引人注目的证实是**第二声**的存在。普通声音，或称“[第一声](@keyword=first_sound|lang=zh-CN|style=Feynman)”，是压力和密度的波，其中正常组分和超流组分同相运动。但如果这两个组分*反相*运动会怎样？想象一下，超流组分（零熵）向一个方向运动，而正常组分（携带所有熵）向另一个方向运动，使得总密度保持不变。这将产生一种波，其中热量来回晃动，却没有相应的压力波。这将是一种[温度波](@keyword=temperature_wave|lang=zh-CN|style=Feynman)。这正是“[第二声](@keyword=second_sound|lang=zh-CN|style=Feynman)”的本质 [@problem_id:1994370]。它的实验发现是对双流体图像的巨大成功验证。

最后，[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)的[量子相干性](@keyword=quantum_coherence|lang=zh-CN|style=Feynman)并非无限。它有一个[特征长度尺度](@keyword=characteristic_length_scales|lang=zh-CN|style=Feynman)，即**恢复长度** $\xi(T)$，这是超流体从像边界壁这样的扰动中“恢复”过来的距离。这个长度在接近[相变温度](@keyword=phase_transition_temperature_(tm)|lang=zh-CN|style=Feynman)时会变得无限大。如果你将氦限制在比这个恢复长度更窄的通道中，你实际上可以抑制超[流态](@keyword=flow_regimes|lang=zh-CN|style=Feynman)，从而降低[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)发生的温度 [@problem_id:1994398]。即使是容器的形状也能改变超流体的量子现实。

从其奇特的[相图](@keyword=phase_portraits|lang=zh-CN|style=Feynman)到量子漩涡，超流性揭示了一个量子规则主导的世界，这些通常隐藏在原子领域的规则走上了中心舞台，上演了一场美丽而奇异的宏观大戏。