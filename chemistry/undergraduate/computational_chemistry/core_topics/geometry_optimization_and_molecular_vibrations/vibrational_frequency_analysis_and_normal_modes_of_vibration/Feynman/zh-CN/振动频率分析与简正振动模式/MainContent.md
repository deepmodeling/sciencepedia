## 引言
分子并不仅仅是教科书上静态的球棍模型，而是永不停歇、进行着复杂内部运动的动态实体。理解这些微观尺度下的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，是揭开物质结构、[化学反应性](@keyword=chemical_reactivity|lang=zh-CN|style=Feynman)和[能量转换](@keyword=energy_conversion|lang=zh-CN|style=Feynman)奥秘的钥匙。然而，这些看似混沌的原子运动背后隐藏着怎样的物理规律？我们又如何从理论上预测和解释实验中观测到的[振动光谱](@keyword=vibrational_spectra|lang=zh-CN|style=Feynman)？本文旨在系统地回答这些问题。在第一章“原理与机制”中，我们将从最简单的[谐振子模型](@keyword=harmonic_oscillator_model|lang=zh-CN|style=Feynman)出发，逐步深入到描述真实分子的[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式理论，探讨质量加权赫森矩阵、[零点振动能](@keyword=zero_point_vibrational_energy|lang=zh-CN|style=Feynman)等核心概念。随后，在第二章“应用与跨学科连接”中，我们将见证这一理论如何化身为化学家的“分子听诊器”，在物质鉴定、反应机理研究、[生物大分子](@keyword=biological_macromolecules|lang=zh-CN|style=Feynman)分析乃至[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)等广阔领域中发挥其强大的威力。现在，让我们一同开始这场探索分子交响乐的旅程。

## 原理与机制

在上一章中，我们将分子描绘成在微观尺度下不断[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)的实体。现在，让我们像物理学家一样，卷起袖子，深入探索这些[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)背后的原理。我们将发现，[分子振动](@keyword=molecular_vibrations|lang=zh-CN|style=Feynman)的世界就像一首宏伟的交响乐，遵循着优美而深刻的物理定律。我们的旅程将从最简单的音符开始，逐步揭示整个乐团的复杂和谐。

### 分子的交响乐：一个音乐的比喻

想象一个分子，比如水分子（$H_2O$），不是一个静态的米老鼠形状的积木，而是一件由三个小球（原子）通过弹簧（[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)）连接而成的乐器。如果你“敲击”它一下（例如，通过吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)），它就会开始[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。但它不会随意地乱晃。就像一把吉他被拨动时会发出特定的音高一样，分子也只会以一组特定的、离散的频率[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。这些频率就是分子的“振动光谱”，是它独一无二的指纹。我们的任务，就是去理解如何预测和解释这些指纹。

### 理想化的音符：谐振子

物理学中最强大的思想之一就是从简化的模型开始。我们能想象到的最简单的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)系统就是一个连接在弹簧上的小球——这便是“谐振子”。当小球偏离其平衡位置时，弹簧会施加一个把它[拉回](@keyword=pullback|lang=zh-CN|style=Feynman)来的力，这个力的大小与偏离的距离成正比。这种关系可以用一个抛物线形的[势能图](@keyword=potential_energy_diagrams|lang=zh-CN|style=Feynman)来描述：势能井的底部是平衡位置，井壁越陡峭，代表弹簧越“硬”，[振动频率](@keyword=vibrational_frequency|lang=zh-CN|style=Feynman)也就越高。

这个简单的模型告诉我们，[振动频率](@keyword=vibrational_frequency|lang=zh-CN|style=Feynman) $\omega$（角频率，单位是 $\mathrm{rad/s}$）由两个因素决定：弹簧的劲度系数 $k$（代表[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的强度）和物体的质量 $m$。它们的关系可以优美地写成：

$ \omega = \sqrt{\frac{k}{m}} $

这个公式充满了直觉：键越强（$k$ 越大），[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)越快；原子越重（$m$ 越大），[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)越慢。

在[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)实验中，科学家们更喜欢用一个叫“[波数](@keyword=wavenumber|lang=zh-CN|style=Feynman)”（$\tilde{\nu}$）的单位，单位是 $\mathrm{cm^{-1}}$（厘米的倒数）。它代表每厘米长度内包含的波的数目。它与[角频率](@keyword=break_frequency|lang=zh-CN|style=Feynman) $\omega$ 的关系很简单，只需要通过光速 $c$ 转换一下即可 [@problem_id:2466920]：

$ \omega = 2\pi c \tilde{\nu} $

这就像是用不同的语言描述同一个音高。理论计算常用 $\omega$，而实验测量常用 $\tilde{\nu}$。

### 寻找真正的和声：[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式与质量的角色

一个真实的分子远比单个谐振子复杂。它是由多个原子通过多根[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)连接而成的耦合系统。想象一下，一个由许多小球和弹簧组成的[复杂网络](@keyword=complex_networks|lang=zh-CN|style=Feynman)。如果你拉动其中一个小球，[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)会迅速传遍整个网络，运动将是混乱且复杂的。

然而，在这个看似混沌的运动中，隐藏着一种深刻的秩序。任何复杂的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，都可以被分解为一组更简单的、独立的“基本[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)模式”的叠加。这些基本模式被称为**[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式**（Normal Modes）。在每一个[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式中，分子中的**所有原子都以相同的频率、[同步](@keyword=entrainment|lang=zh-CN|style=Feynman)地**（同相或反相）进行和谐的周期性运动。它们是分子这件乐器能够奏出的最纯粹的“音符”。

那么，我们如何找到这些神秘的[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式呢？这正是[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)的核心任务之一。我们首先需要描述分子在任何几何构型下的势能，这被称为[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)（Potential Energy Surface, PES）。在分子的稳定结构（[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)的一个极小值点）附近，这个复杂的[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)可以被近似为一个高维的抛物面。描述这个[抛物面](@keyword=paraboloid|lang=zh-CN|style=Feynman)曲率的，是一个叫做**赫森矩阵**（Hessian Matrix）的数学对象。它的每个元素都是势能对两个原子坐标的[二阶偏导数](@keyword=second_partial_derivatives|lang=zh-CN|style=Feynman)，本质上就是我们前面提到的“劲度系数” $k$ 的推广 [@problem_id:2466884]。

你可能会想，我们只要找到这个赫森矩阵的本征矢量（eigenvectors），不就能得到[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式了吗？不完全是。这里的关键在于，原子不仅有“连接”，还有“质量”。一个氢原子和一个碳原子的运动方式显然是不同的。直接分析这个“电子”赫森矩阵，我们得到的只是[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)本身最陡和最缓的方向，但这并不代表真实的、可解耦的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)模式。除非，一个奇迹发生——分子中所有原子的质量都完全相同 [@problem_id:2466884]。

大自然巧妙地指引我们解决了这个问题。为了同时正确处理“弹簧的硬度”（势能）和“小球的重量”（动能），我们必须使用**质量加权的赫森矩阵**。这个操作在数学上相当于给每个原子的坐标都乘以其质量的平方根。这就像是在一个不公平的拔河比赛中，给体重较轻的选手更多的“权重”，使得比赛变得公平。当我们在经过质量加权后的新[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)里分析[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)时，动能和势能神奇地同时被对角化了。这意味着我们找到了真正独立的、[解耦](@keyword=disentanglement|lang=zh-CN|style=Feynman)的运动模式——[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式！

质量加权赫森矩阵的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)直接给出了[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式频率的平方（$\omega^2$），而它的本征矢量则精确地描绘了每个[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式中原子的运动方向和幅度 [@problem_id:2466884]。

[同位素取代](@keyword=isotopic_substitution|lang=zh-CN|style=Feynman)效应完美地印证了这个模型的正确性 [@problem_id:2466903]。比如，将水分子（$H_2O$）中的一个氢（$H$）换成其更重的同位素氘（$D$），形成半重水（$HDO$）。根据玻恩-奥本海默近似，电子的运动只关心原子核的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)和位置，而不关心其质量。因此，[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的“弹簧硬度”——即电子赫森矩阵——是完全不变的。但是，由于其中一个原子的质量改变了，质量加权的赫森矩阵必然会改变。结果是，我们计算出的振动频率和模式都会发生变化。这正是在红外光谱实验中观察到的现象！这深刻地揭示了，分子的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)是势能（电子结构）和动能（原子质量）共同谱写的交响曲。

### 消除“噪音”：分离纯粹的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)

一个分子在空间中不仅会[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，它还会作为一个整体平移（飞来飞去）和转动（滚来滚去）。这些运动显然不是我们关心的内部[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。一个[非线性分子](@keyword=non_linear_molecules|lang=zh-CN|style=Feynman)（比如水）总共有 $3N$ 个运动自由度（其中 $N$ 是原子数），其中 3 个是平动，3 个是转动。这些运动在[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)上不会引起能量变化，因此它们对应的“[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)”频率为零。

在进行[振动分析](@keyword=vibrational_analysis|lang=zh-CN|style=Feynman)时，我们必须想办法将这 6 个“无聊”的运动从 $3N$ 个总自由度中剔除，剩下的 $3N-6$ 个才是真正的内部[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。要做到这一点，我们需要一个特殊的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)，在这个[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)里，分子既不平移也不转动。这听起来容易，但对于一个正在[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)的、变形的物体来说，定义“不转动”是相当棘手的。

这个巧妙的解决方案就是**埃卡特框架**（Eckart frame）[@problem_id:2466902]。你可以把它想象成一个高超的摄像师，任务是拍摄一个正在跳舞同时又在舞台上移动和旋转的舞者。为了只捕捉舞者身体的内部动作（比如手臂的摆动），摄像师必须持续地移动和旋转摄像机，使得舞者的躯干在画面中始终保持静止和朝向不变。埃卡特框架就是这样一个“聪明的摄像机”，它通过一系列精巧的数学条件，确保了在描述[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)时，分子的整体转动和[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)在最大程度上被分离开来。

在计算上，这意味着我们需要通过一个称为“投影”的线性代数操作，将赫森矩阵中与平动和转动相关的部分“投影”掉，只留下纯粹的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)部分进行分析 [@problem_id:2466964]。这样，我们就能得到一个干净的、包含 $3N-6$ 个非零频率的振动光谱。

### 量子的[颤动](@keyword=trembling_motion|lang=zh-CN|style=Feynman)：一个永不静止的世界

到目前为止，我们的讨论大多是基于经典力学的。但原子和分子是量子世界的居民，它们的行为必须用量子力学来描述。量子力学为[分子振动](@keyword=molecular_vibrations|lang=zh-CN|style=Feynman)带来了两个惊人的特性。

首先，振动能量是量子化的。一个谐振子的能量不能取任意值，只能是一份一份的，其能量水平为 $E_n = \hbar\omega(n + 1/2)$，其中 $n$ 是[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman)（$0, 1, 2, ...$），$\hbar$ 是[约化普朗克常数](@keyword=reduced_planck_constant|lang=zh-CN|style=Feynman)。

其次，也是最奇特的，一个量子谐振子的最低能量（当 $n=0$ 时）并不是零，而是 $E_0 = \frac{1}{2}\hbar\omega$。这意味着，即使在绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)（$T=0$ K），分子也永远无法完全静止在势能井的底部。它必须永远地“颤动”。这种不可消除的、最低限度的振动能量被称为**[零点振动能](@keyword=zero_point_vibrational_energy|lang=zh-CN|style=Feynman)**（Zero-Point Vibrational Energy, ZPVE）。

为什么会这样？这源于量子力学最核心的原理之一——海森堡不确定性原理 [@problem_id:2466967]。这个原理指出，我们无法同时精确地知道一个粒子的位置和动量。如果一个分子完全静止在势能井的底部，那么它的位置（平衡位置）和动量（零）就都被精确地确定了，这恰恰是量子力学所禁止的。为了“遵守”[不确定性原理](@keyword=uncertainty_principle|lang=zh-CN|style=Feynman)，分子必须通过永不停歇的零点[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，来维持其位置和动量的不确定性。因此，ZPVE 是一个深刻的量子现象，它告诉我们，微观世界是一个永不静止的世界。分子的总 ZPVE 就是其所有 $3N-6$ 个[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)模式的[零点能](@keyword=zero_point_energy|lang=zh-CN|style=Feynman)量之和：

$ E_{ZPVE} = \sum_{i=1}^{3N-6} \frac{1}{2}\hbar\omega_i $

因为对于一个稳定的分子，所有的 $\omega_i$ 都是正实数，所以 ZPVE 永远是一个正值。

### 解读[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)乐谱：频率告诉我们什么

现在我们有了强大的理论工具，可以从计算中得到一组振动频率。这些数字就像一张乐谱，记录了分子的身份和状态信息。

#### 识别稳定结构：一首和谐的交响曲

在[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)中，我们常常需要寻找分子的稳定构型，这对应于[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)上的一个极小值点。但优化算法可能会把我们带到一个“假”的极小值点，比如一个平坦的“山肩”。如何确认我们找到的是一个真正的、四面八方都是上坡的“山谷”呢？

[振动频率分析](@keyword=vibrational_frequency_analysis|lang=zh-CN|style=Feynman)提供了一个决定性的判据 [@problem_id:2466905]。在一个真正的极小值点，任何方向的微小偏离都会导致能量上升。这意味着[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)在所有方向上的曲率都必须是正的。反映到计算结果上，就是质量加权赫森矩阵的所有 $3N-6$ 个[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)模式的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)都必须是正数。因为 $\omega = \sqrt{\lambda}$，所以这意味着一个稳定结构的所有[振动频率](@keyword=vibrational_frequency|lang=zh-CN|style=Feynman)都必须是**正实数**。如果计算结果显示有 $3N-6$ 个正实数频率（以及 6 个接近零的平动/转动频率），我们就可以满怀信心地宣布：“我们找到了一个真正的稳定结构！”

#### 识别[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)的关隘：一个不稳定的渐强音

更有趣的是，如果计算结果中出现了一个**虚数频率**，这通常不是计算错误，而是一个激动人心的发现！

一个虚数频率（例如 $\omega = i\nu$，其中 $\nu$ 是实数）意味着赫森矩阵的一个[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)是负数（$\lambda = \omega^2 = -\nu^2 < 0$）。负的曲率意味着什么？这意味着我们找到的不是一个山谷，而是一个**[鞍点](@keyword=saddle_point|lang=zh-CN|style=Feynman)**——在一个方向是能量的最高点（像山脊），而在所有其他方向是能量的最低点。这正是[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)中连接反应物和产物的“[过渡态](@keyword=activated_complex|lang=zh-CN|style=Feynman)”的精确数学定义！

那个唯一的虚数频率所对应的[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式，就是沿着反应坐标的运动——它描绘了分子如何扭曲、拉伸，最终“翻过”能垒，完成化学转变。这个虚数频率的大小也蕴含着丰富的信息 [@problem_id:2466891]。想象两个不同反应的能垒，一个“尖锐”，另一个“平缓”。“尖锐”的能垒意味着在过渡态顶点的曲率[绝对值](@keyword=absolute_value|lang=zh-CN|style=Feynman)很大，这将导致一个数值很大的虚频；而“平缓”的能垒则对应着较小的虚频。因此，虚频的大小直接告诉我们[反应能垒](@keyword=reaction_barriers|lang=zh-CN|style=Feynman)的“形状”。

### 当和谐被打破：[模式混合](@keyword=mode_mixing|lang=zh-CN|style=Feynman)与[非谐性](@keyword=anharmonicity|lang=zh-CN|style=Feynman)

我们之前描述的[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式是优美、独立的。但在真实的分子中，情况会变得更加复杂和有趣。

#### [振动](@keyword=oscillation|lang=zh-CN|style=Feynman)间的“对话”：[模式混合](@keyword=mode_mixing|lang=zh-CN|style=Feynman)

设想在丙二醛（malonaldehyde）分子中，有一个 C=O 双键的伸缩[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)和一个 C-C-H 键的弯曲[振动](@keyword=oscillation|lang=zh-CN|style=Feynman) [@problem_id:2466942]。如果它们的“自然”频率（没有考虑耦合时的频率）恰好比较接近，并且它们的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)方式具有相同的对称性，那么它们就不能再被看作是独立的了。它们会发生“混合”，就像两个频率相近的音叉会产生共鸣一样。

这种现象，有时被称为[费米共振](@keyword=fermi_resonance|lang=zh-CN|style=Feynman)，其结果是，我们最终观测到的不再是纯粹的 C=O 伸缩或纯粹的 C-C-H 弯曲。相反，我们得到两个新的、混合的[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式。一个模式是“大部分C=O伸缩，混合了少量C-C-H弯曲”，另一个模式则是“大部分C-C-H弯曲，混合了少量C=O伸缩”。

这种混合还会导致一个称为“[能级排斥](@keyword=level_repulsion|lang=zh-CN|style=Feynman)”的现象：两个模式的能量会相互推开，原本高频的模式频率会变得更高，而原本低频的模式频率会变得更低。更有趣的是“强度借贷”：通常，C=O 伸缩[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)在[红外光谱](@keyword=ir_spectrum|lang=zh-CN|style=Feynman)中非常强，而 C-C-H 弯曲则较弱。发生混合后，弱的弯曲[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)会从强的伸缩[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)那里“借”来一些强度，从而在光谱中变得比预期更明显。

通过[同位素取代](@keyword=isotopic_substitution|lang=zh-CN|style=Feynman)（例如，将 H 换成 D），我们可以人为地改变 C-C-D 弯曲的频率，使其远离 C=O 伸缩频率。这会大大减小它们之间的混合程度，使得各自的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)模式和[光谱强度](@keyword=spectral_intensity|lang=zh-CN|style=Feynman)都“回归”到更纯粹的状态。这种可控的实验变化为[模式混合](@keyword=mode_mixing|lang=zh-CN|style=Feynman)理论提供了强有力的证据。

#### 当弹簧断裂时：非谐性的世界

我们整个讨论的基础是[谐振子模型](@keyword=harmonic_oscillator_model|lang=zh-CN|style=Feynman)——一个永远不会断裂的完美弹簧。但真实的[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)更像是会疲劳、最终会断裂的弹簧。当[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)幅度很大时，势能就不再是完美的抛物线了，这种偏离被称为**非谐性**。

对于像氩气[双原子分子](@keyword=diatomic_molecules|lang=zh-CN|style=Feynman)（$Ar_2$）这样由微弱的范德华力维系的体系，[非谐性](@keyword=anharmonicity|lang=zh-CN|style=Feynman)的影响尤为显著 [@problem_id:2466910]。它的势能井非常浅，只能容纳少数几个束缚的振动能级。[谐振子模型](@keyword=harmonic_oscillator_model|lang=zh-CN|style=Feynman)在这里会犯下几个严重的错误：
1.  它错误地预测了存在无限多个等间距的能级，而实际上 $Ar_2$ 振动能量稍高就会解离成两个独立的氩原子。
2.  它用势能井底部的曲率来定义唯一的频率 $\omega$，但这完全无法描述在势能井较宽、较平坦区域的大幅度[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。
3.  在计算分子的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)性质（如[振动配分函数](@keyword=vibrational_partition_function|lang=zh-CN|style=Feynman)）时，谐振子模型会因为包含了这些“幽灵”高能级而导致严重高估。

这提醒我们，任何模型都有其适用范围。谐振子模型为我们理解[分子振动](@keyword=molecular_vibrations|lang=zh-CN|style=Feynman)提供了一个美妙而强大的框架，但要真正精确地描述现实世界，我们必须认识到它的局限，并在必要时引入更复杂的非谐性修正。

至此，我们已经穿越了[分子振动](@keyword=molecular_vibrations|lang=zh-CN|style=Feynman)的核心地带，从经典的弹簧小球到量子的不确定性，从和谐的[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式到复杂的[模式混合](@keyword=mode_mixing|lang=zh-CN|style=Feynman)。我们发现，一张看似简单的振动光谱，实则是分子内部结构、成键性质、质量分布和[量子效应](@keyword=quantum_effects|lang=zh-CN|style=Feynman)共同谱写的一部错综复杂而又无比和谐的交响乐。