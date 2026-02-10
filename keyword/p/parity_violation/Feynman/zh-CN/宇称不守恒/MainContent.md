## 引言
几个世纪以来，人们根深蒂固地认为自然法则是[左右对称](@keyword=bilateral_symmetry|lang=zh-CN|style=Feynman)的，对左和右没有偏好。这个被称为[宇称对称性](@keyword=parity_symmetry|lang=zh-CN|style=Feynman)的概念表明，任何物理过程的镜像也是一个完全有效的物理过程。这是一个直观而优美的想法，但在 20 世纪中叶，这面完美的镜子出现了裂痕。物理学家发现，宇宙的基本相互作用之一——[弱核力](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)——破坏了这种对称性，这意味着在亚原子层面，自然界确实能够区分左和右。

本文旨在探讨这种对称性破缺的深远影响。我们将探究这种不对称性的根本原因及其在物理世界中的表现形式。第一章“原理与机制”将剖析核心理论，解释弱相互作用如何引发[宇称不守恒](@keyword=parity_violation|lang=zh-CN|style=Feynman)，以及这种微弱的效应如何在重原子中被放大，从而使其能够被实验测量。接下来的“应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系”一章将揭示这一现象如何从一个科学奇观转变为一种强大而精确的工具，促成了横跨[粒子物理学](@keyword=particle_physics|lang=zh-CN|style=Feynman)、[核结构](@keyword=nuclear_structure|lang=zh-CN|style=Feynman)、化学乃至宇宙学等领域的发现。

## 原理与机制

想象一下观看一场完全弹性的台球碰撞的影片。现在，再想象观看这部影片的镜像。你能分辨出区别吗？当然不能。运动定律——至少是我们日常经历的那些支配引力和[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)的定律——是左右对称的。它们没有偏好的左手或右手。物理世界的这种深刻对称性被称为**宇称**。这是一个简单、直观的概念，即如果我们将整个实验在镜子中反映，或者等效地，将所有空间坐标通过原点反演（$\vec{r} \to -\vec{r}$），自然法则应当保持不变。在很长一段时间里，我们认为这种对称性是绝对的，是宇宙中一条神圣且不可打破的定律。

然而，在 20 世纪中叶，我们发现了这面镜子上的裂痕。

### 破碎的镜子：对称性如何丢失

一个物理系统如何会失去其[宇称对称性](@keyword=parity_symmetry|lang=zh-CN|style=Feynman)？有时，我们可以强迫它这样做。考虑一个漂浮在真空中的氢原子。它的行为由质子和电子之间的电磁力支配，这是一种完全对称的力。原子的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)具有确定的宇称；s 轨道是球对称的，具有偶宇称，而 p 轨道呈哑铃形，具有奇宇称。支配该原子的定律不对原子及其镜像加以区分。

现在，让我们将这个原子置于一个均匀的[静电场](@keyword=electrostatic_field|lang=zh-CN|style=Feynman) $\vec{E}$ 中。电场指向一个特定的方向。这个看似简单的行为从根本上改变了情况。原子与电场之间的相互作用由原子总能量（其哈密顿量）中的一项来描述，$H_{int} = -e\vec{r} \cdot \vec{E}$，其中 $\vec{r}$ 是电子的[位置矢量](@keyword=position_vectors|lang=zh-CN|style=Feynman)。当我们进行宇称操作，即“镜像反射”时，会发生什么？位置矢量反向，$\vec{r} \to -\vec{r}$。但定义我们实验[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)的外部电场保持不变。结果是[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)的符号反转：$H_{int} \to -H_{int}$。系统的总能量在镜像世界中不再与现实世界中的相同。电场的存在明确地破坏了[宇称对称性](@keyword=parity_symmetry|lang=zh-CN|style=Feynman) [@problem_id:1994123]。

这是一个优美而清晰的例子，但这是一种*外部*的对称性破缺。是我们强加给它的。真正令人震惊的发现是，自然界中存在一种基本相互作用，其核心本身就内建了这种不对称性。这种相互作用就是**[弱核力](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)**。

### 不对称性的构建者：[弱相互作用](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)

[弱相互作用](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)负责[放射性衰变](@keyword=radioactive_decay|lang=zh-CN|style=Feynman)，而且事实证明，它本质上是“左手的”。要理解其工作原理，我们需要窥探[粒子物理标准模型](@keyword=standard_model_particle_physics|lang=zh-CN|style=Feynman)的机制。造成[原子宇称不守恒](@keyword=atomic_parity_violation|lang=zh-CN|style=Feynman)的相互作用是**[弱中性流](@keyword=weak_neutral_current|lang=zh-CN|style=Feynman)**，由 $Z^0$ [玻色子](@keyword=boson|lang=zh-CN|style=Feynman)介导。这种相互作用可以被看作是电子与原子核内夸克之间的一种对话。

在物理学中，相互作用通常用“流”来描述。可以想象电子的流与核子的流相互作用。这些流中的每一个都包含两个部分：
1.  一个**矢量**部分（$V$），其行为像普通的力，在宇称反射下像标准矢量（例如，位置 $\vec{r}$）一样变换。
2.  一个**轴矢量**部分（$A$），与粒子的内禀自旋或“手性”有关，在宇称反射下像[轴矢量](@keyword=axial_vector|lang=zh-CN|style=Feynman)（例如，角动量 $\vec{L} = \vec{r} \times \vec{p}$）一样变换。

总相互作用是所有可能配对的总和：矢量电子与矢量[核子](@keyword=nucleons|lang=zh-CN|style=Feynman)（$V_e V_n$）、[轴矢量](@keyword=axial_vector|lang=zh-CN|style=Feynman)电子与[轴矢量](@keyword=axial_vector|lang=zh-CN|style=Feynman)核子（$A_e A_n$），以及关键的混合项 $V_e A_n$ 和 $A_e V_n$。

让我们看看这些项在镜像中会发生什么。在[宇称变换](@keyword=parity_transformation|lang=zh-CN|style=Feynman)下，矢量量的空间分量会改变符号，而轴矢量量的则不会。
-   对于 $V_e V_n$ 和 $A_e A_n$，两次符号反转（或没有反转）会相互抵消。相互作用在镜像中看起来是一样的。这些项是[宇称守恒](@keyword=parity_conservation|lang=zh-CN|style=Feynman)的。
-   然而，对于混合项 $V_e A_n$ 和 $A_e V_n$，乘积中只有一个部分会改变符号。整个相互作用在宇称反射下会改变符号 [@problem_id:2009302]。

在[宇称变换](@keyword=parity_transformation|lang=zh-CN|style=Feynman)下改变符号的相互作用被称为**[赝标量](@keyword=pseudoscalar|lang=zh-CN|style=Feynman)**。基本[电弱理论](@keyword=electroweak_theory|lang=zh-CN|style=Feynman)中这些 $V_e A_n$ 和 $A_e V_n$ 项的存在是[宇称不守恒](@keyword=parity_violation|lang=zh-CN|style=Feynman)的最终根源。宇宙，在弱相互作用的层面上，并非左右对称。它能够区分左和右。

### 世界的模糊：混合相反宇称的态

在原子内部存在[赝标量](@keyword=pseudoscalar|lang=zh-CN|style=Feynman)相互作用会带来什么物理后果？它会导致现实的模糊。具有确定宇称的态不再是原子的真实能量本征态。弱相互作用就像一只幻影之手，将电磁作用永远保持分离的[态混合](@keyword=state_mixing|lang=zh-CN|style=Feynman)在一起。

考虑氢原子著名的 $2s_{1/2}$ 和 $2p_{1/2}$ 态。它们的能量几乎相同，但宇称相反（s 态的 $l=0$ 是[偶宇称](@keyword=even_parity|lang=zh-CN|style=Feynman)，p 态的 $l=1$ 是[奇宇称](@keyword=odd_parity|lang=zh-CN|style=Feynman)）。在一个仅由[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)支配的世界里，处于 $2s_{1/2}$ 态的原子不可能自发地转变为 $2p_{1/2}$ 态。在某种意义上，它们是正交的世界。

然而，[宇称不守恒](@keyword=parity_violation|lang=zh-CN|style=Feynman)的哈密顿量 $H_{PV}$ 可以将它们联系起来。因为它是[赝标量](@keyword=pseudoscalar|lang=zh-CN|style=Feynman)，根据对称性，“矩阵元” $\langle 2p_{1/2} | H_{PV} | 2s_{1/2} \rangle$ 被允许为非零值 [@problem_id:1221707]。结果是，我们过去称为 $|s\rangle$ 的态实际上是一个[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)：
$$ |\tilde{s}\rangle \approx |s\rangle + \eta |p\rangle $$
而我们称为 $|p\rangle$ 的态现在是：
$$ |\tilde{p}\rangle \approx |p\rangle - \eta^* |s\rangle $$
其中 $\eta$ 是一个微小的混合系数。原子的态不再是纯粹的[偶宇称](@keyword=even_parity|lang=zh-CN|style=Feynman)或[奇宇称](@keyword=odd_parity|lang=zh-CN|style=Feynman)；它们现在是两者的[量子叠加](@keyword=quantum_superposition|lang=zh-CN|style=Feynman)。这种混合是[原子宇称不守恒](@keyword=atomic_parity_violation|lang=zh-CN|style=Feynman)的核心机制。这种混合的一个效应是，曾经被严格禁戒的跃迁现在可能发生。例如，电偶极（E1）跃迁要求宇称改变。从 $|s\rangle$ 态通过 E1 通道衰变到[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|g\rangle$（也是偶宇称）是不可能的。但对于[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman) $|\tilde{s}\rangle$，其微小的 $|p\rangle$ 成分可以通过快速的 E1 跃迁进行衰变，产生一个微小但可观测的“错误宇称”信号。

### 放大器：为何重原子是关键

这种混合效应小得惊人。在氢原子中，它如此微小以至于完全无法测量。那么科学家们是如何设法观察到它的呢？他们采用了一种巧妙的策略：在效应被放大的地方进行寻找。他们使用非常重的原子，如铯（$Z=55$）、铊（$Z=81$）或镱（$Z=70$）。[宇称不守恒](@keyword=parity_violation|lang=zh-CN|style=Feynman)效应的大小遵循一个著名的标度关系，称为 **$Z^3$ 定律**。该效应大致随[原子序数](@keyword=atomic_number|lang=zh-CN|style=Feynman)的立方增长！让我们来看看这个“放大共谋”为何会发生。

1.  **更多的相互作用粒子**：相互作用的强度与原子核的[弱荷](@keyword=weak_charge|lang=zh-CN|style=Feynman) $Q_W$ 成正比。在一个很好的近似下，这个[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)与中子数 $N$ 成正比，而中子数大致随 $Z$ 变化。更大的原子核拥有更大的[弱荷](@keyword=weak_charge|lang=zh-CN|style=Feynman)。

2.  **电子-核交叠与[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)效应**：[弱相互作用](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)是短程的，所以效应主要取决于电子在原子核附近的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)。在重原子中，巨大的核[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)将内层电子加速到[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)性速度。这种效应极大地压缩了电子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)，显著增加了电子在原子核处或其附近的[概率密度](@keyword=probability_density|lang=zh-CN|style=Feynman)。综合计算表明，这个[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)相关的[矩阵元](@keyword=matrix_elements|lang=zh-CN|style=Feynman)因子大致与 $Z^2$ 成正比。

当你将这两个主要因素——[弱荷](@keyword=weak_charge|lang=zh-CN|style=Feynman)（大致与 $Z$ 成正比）和[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)效应（大致与 $Z^2$ 成正比）——结合起来时，便得到了惊人的 $Z^3$ 标度关系 [@problem_id:2009318]。铯（$Z=55$）中的[宇称不守恒](@keyword=parity_violation|lang=zh-CN|style=Feynman)振幅比像锂（$Z=3$）这样的轻原子大数千倍 [@problem_id:2009272]。正是这种增强将该效应从理论上的好奇提升到了精确测量的领域。此外，根据[微扰理论](@keyword=perturbation_theory|lang=zh-CN|style=Feynman)，我们知道混合系数 $\eta$ 与[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)之间的能量差 $\Delta E$ 成反比 [@problem_id:2009248]。因此，物理学家们寻找那些恰好也具有[近简并](@keyword=near_degeneracy|lang=zh-CN|style=Feynman)相反宇称态的重原子，这种组合提供了可能的最大放大效果。

### 中子的秘密：探测原子核

让我们更仔细地看看[弱荷](@keyword=weak_charge|lang=zh-CN|style=Feynman) $Q_W$。[标准模型](@keyword=standard_model|lang=zh-CN|style=Feynman)给出了它的精确预测：
$$ Q_W = Z(1 - 4\sin^2\theta_W) - N $$
这里，$Z$ 是质子数，$N$ 是中子数，$\theta_W$ 是[温伯格角](@keyword=weak_mixing_angle|lang=zh-CN|style=Feynman)，一个自然界的基本常数，其实验值为 $\sin^2\theta_W \approx 0.231$。如果你代入这个数字，你会发现乘以质子数 $Z$ 的项是 $1 - 4(0.231) = 1 - 0.924 = 0.076$。这是一个非常小的数字！每个质子对[弱荷](@keyword=weak_charge|lang=zh-CN|style=Feynman)的贡献被抑制了超过 92%。相比之下，每个中子的贡献系数为 $-1$。

这得出了一个深刻的结论：原子核的[弱荷](@keyword=weak_charge|lang=zh-CN|style=Feynman)绝大部分由中子数决定 [@problem_id:2009321]。对于镱-174（$Z=70, N=104$），质子的总贡献大约是中子贡献的 $5\%$。这意味着[原子宇称不守恒](@keyword=atomic_parity_violation|lang=zh-CN|style=Feynman)实验不仅仅是对[标准模型](@keyword=standard_model|lang=zh-CN|style=Feynman)的检验；它们还是探测原子核内**中子分布**的绝佳探针。通过测量这些微小的原子效应，物理学家可以绘制出原子核内中子位置的图谱——即“[中子皮](@keyword=neutron_skin|lang=zh-CN|style=Feynman)”——从而提供传统主要观测质子的电磁探针难以获得的独特见解。

### 核内的一个扭转：环磁矩

故事并未就此结束。我们讨论的主要[宇称不守恒](@keyword=parity_violation|lang=zh-CN|style=Feynman)效应是整个原子核的集体效应，且与[核自旋](@keyword=nuclear_spin|lang=zh-CN|style=Feynman)无关。但还有第二个更微妙的机制在起作用。[弱相互作用](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)也作用于核子（质子和中子）*之间*。这种内部的[宇称不守恒](@keyword=parity_violation|lang=zh-CN|style=Feynman)可以将核内的弱流[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成一种奇特的、甜甜圈形（环形）的[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)。这种构型被称为**核环磁矩**。

这个环磁矩会与原子的电子产生其自身的[宇称不守恒](@keyword=parity_violation|lang=zh-CN|style=Feynman)相互作用。其定义特征是其强度与[核自旋](@keyword=nuclear_spin|lang=zh-CN|style=Feynman) $\vec{I}$ 成正比 [@problem_id:2009288]。与不依赖自旋的效应一样，它在[宇称变换](@keyword=parity_transformation|lang=zh-CN|style=Feynman)下是奇性的（破坏[镜像对称](@keyword=mirror_symmetry|lang=zh-CN|style=Feynman)性），但在时间反演下是偶性的（支配它的定律在时间正向和反向时相同）。通过比较同一元素不同同位素（它们具有不同的核自旋）中的[宇称不守恒](@keyword=parity_violation|lang=zh-CN|style=Feynman)测量结果，实验学家可以从环磁矩效应中分离出不依赖自旋的效应。这使他们能够打开另一扇窗，窥探[弱相互作用](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)的奇特、不对称世界，这一次是研究它在原子核内部的作用。