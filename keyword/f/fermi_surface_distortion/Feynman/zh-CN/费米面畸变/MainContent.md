## 引言
在凝聚态物理的世界里，[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)的概念是理解金属行为的基石。在最简单的形式下，它是[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中一个完美的球面，在绝对零度下分隔了占据电子态与未占据电子态。然而，这一理想化的图像仅适用于无相互作用的电子。一个根本性的问题随之产生：当考虑到电子之间强大的[静电排斥](@keyword=electrostatic_repulsion|lang=zh-CN|style=Feynman)时，这个原始的球形表面会发生什么？这些相互作用如何重塑电子系统的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)？

本文深入探讨了[费米面畸变](@keyword=fermi_surface_distortion|lang=zh-CN|style=Feynman)这一引人入胜的现象，这是一个由相互作用驱动电子系统自发破缺对称性的过程。它通过[朗道费米液体理论](@keyword=landau_fermi_liquid_theory|lang=zh-CN|style=Feynman)的优雅框架来探索这一过程的物理学。第一章**“原理与机制”**将介绍[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的概念和[朗道参数](@keyword=landau_parameters|lang=zh-CN|style=Feynman)的语言，推导出著名的波梅兰丘克[稳定性判据](@keyword=stability_criteria|lang=zh-CN|style=Feynman)。它将解释吸引性相互作用如何导致不稳定性以及新的、畸变的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（如[向列相](@keyword=nematic_phase|lang=zh-CN|style=Feynman)费米流体）的出现。在这一理论基础之后，第二章**“应用与跨学科联系”**将连接理论与现实。它将展示这些畸变如何在实验中被观察到，并讨论它们对材料的力学性质、非常规超导以及量子临界系统和[莫尔材料](@keyword=moiré_materials|lang=zh-CN|style=Feynman)的奇异物理产生的深远影响。通过从抽象原理到具体后果的旅程，我们将揭示费米面的形状如何不仅仅是一种被动属性，而是在定义丰富量子[物相](@keyword=phases_of_matter|lang=zh-CN|style=Feynman)过程中的一个积极参与者。

## 原理与机制

想象一片在无星之夜下完全静止、冰冷的海洋。这是我们的起点：一堆在绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)下的电子，表现得像一片宁静的**费米海**。在这种状态下，所有可用的低能级都被填满，直至一个称为**[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)** $\epsilon_F$ 的清晰能量边界。在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中，这个边界形成一个完美的球面——**费米面**。球面内的每一点代表一个被填充的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，球面外的每一点都是空的。然而，这个优美而简单的图像描述的是无相互作用的电子。真实世界要有趣得多。作为带电粒子，电子之间相互猛烈排斥。当我们开启这些相互作用时，我们宁静的[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)会发生什么？

苏联物理学家 Lev Landau 的天才之处在于，他意识到即使在这种相互作用的混乱中，某种有序的表象依然存在。他提出，电子在与群体的相互作用中被“缀饰”，其行为如同他称之为**[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)**的新实体。想象一个人穿过拥挤的人群；他不仅仅是他自己，而是一个更迟缓的实体，推开别人，同时也被别人推。这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)仍然形成一个[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)，但它们的“社会性”相互作用深刻地改变了系统的集体行为。这就是**[朗道费米液体理论](@keyword=landau_fermi_liquid_theory|lang=zh-CN|style=Feynman)**的世界。

### 相互作用的语言：[朗道参数](@keyword=landau_parameters|lang=zh-CN|style=Feynman)

我们如何才能描述无数电子之间错综复杂的相互作用网络呢？我们无法追踪每一次推挤。取而代之，Landau 设计了一种绝妙的简化方法。他专注于两个[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)在最重要位置——[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上——的相互作用。他提出，一个[准粒子能量](@keyword=quasiparticle_energies|lang=zh-CN|style=Feynman)的变化取决于所有其他[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的状态。这种依赖关系的强度由一个主函数——**朗道相互作用函数** $f_{\sigma\sigma'}(\hat{\mathbf{p}}\cdot\hat{\mathbf{p}}')$ 所描述。

这个函数告诉我们，一个动量为 $\mathbf{p}$、自旋为 $\sigma$ 的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的能量，如何受到另一个动量为 $\mathbf{p}'$、自旋为 $\sigma'$ 的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)存在的影响。对于一个各向同性的系统，这种相互作用只取决于两个动量之间的夹角 $\theta = \arccos(\hat{\mathbf{p}}\cdot\hat{\mathbf{p}}')$ 以及它们的相对[自旋取向](@keyword=spin_alignment|lang=zh-CN|style=Feynman)。

为了理解这一点，我们可以分解这种相互作用，就像一个和弦由基本音符构成一样。首先，我们将其分为两个“通道”：一个与[自旋取向](@keyword=spin_alignment|lang=zh-CN|style=Feynman)无关的**自旋对称**部分 ($f^s$)，和一个依赖于自旋取向的**自旋反对称**部分 ($f^a$)。你可以将对称部分视为控制类[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)属性（[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)如何响应密度变化），而反对称部分则控制类自旋属性（它们如何响应磁化）。

接下来，我们将这些函数中的每一个都展开为**[勒让德多项式](@keyword=legendre_polynomials|lang=zh-CN|style=Feynman)** $P_l(\cos\theta)$ 的级数。这是一个精妙的数学技巧，它将任何角度依赖性分解为由整数 $l=0, 1, 2, ...$ 索引的纯“谐波”之和：
$$
f^{s,a}(\cos\theta) = \sum_{l=0}^{\infty} f_{l}^{s,a} P_{l}(\cos\theta)
$$
每个系数 $f_l^s$ 或 $f_l^a$ 告诉我们特定角形状下相互作用的强度。
*   $l=0$ 对应于均匀、各向同性的相互作用——就像一种普遍的吸引或排斥背景嗡嗡声。
*   $l=1$ 代表[偶极相互作用](@keyword=dipole_interaction|lang=zh-CN|style=Feynman)——偏好于在一个方向上的相互作用。
*   $l=2$ 是四极相互作用——比如粒子更喜欢与它们前面和后面的粒子相互作用，而不是与侧面的粒子相互作用。

最后，为了使它们具有普适性，我们通过乘以[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)处的态密度 $N(0)$ 来定义无量纲的**[朗道参数](@keyword=landau_parameters|lang=zh-CN|style=Feynman)** $F_l^s$ 和 $F_l^a$。这些参数，$F_0^s, F_1^s, F_2^s, ...$ 和 $F_0^a, F_1^a, ...$，是我们用来描述相互作用[费米液体](@keyword=fermi_liquid|lang=zh-CN|style=Feynman)的基本语言 [@problem_id:2995962] [@problem_id:1161198]。它们是决定我们的[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)是保持一个平静的球面，还是扭曲成某种新的、奇异形状的关键数字。

### 一场拉锯战：动能与相互作用能

那么，是什么决定了[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)的形状呢？这是一场两大基本力量之间的宏大拉锯战：**动能**和**[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)**。

1.  **动能：** 这是运动的能量。为了最小化动能，系统希望首先填充能量最低的态。在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中，这意味着填充一个紧凑的、完美的球体。任何偏离球形的形状——比方说，将一些粒子在一个方向上推向更高的动量，同时从另一个方向拉入一些粒子——都不可避免地会提高总动能。动能是球形形状的坚定捍卫者；它代表了任何形变的“代价”。

2.  **[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)：** 这就是事情变得有趣的地方。由我们的[朗道参数](@keyword=landau_parameters|lang=zh-CN|style=Feynman)所描述的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)之间的相互作用，既可能在费米面变形时提高能量，也可能降低能量。如果相互作用对于某个特定的形状（例如，四极形状）是强吸引的，系统可能会通过扭曲成该形状来*获得*能量。

费米面的命运悬于这场拉锯战的平衡之中。球形[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)只有在任何可能的形变所付出的动能代价超过任何可能从相互作用中获得的能量增益时才是稳定的 [@problem_id:2995985]。

### [临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)：波梅兰丘克[稳定性判据](@keyword=stability_criteria|lang=zh-CN|style=Feynman)

值得注意的是，这场复杂的战斗可以被提炼成一组优美而简单的条件。对于每一种可能的畸变形状，由谐波数 $l$ 和自旋通道（$s$ 或 $a$）定义，[费米液体](@keyword=fermi_liquid|lang=zh-CN|style=Feynman)的稳定性由一个单一的表达式决定。在给定通道中，微小畸变所引起的能量变化 $\delta E$ 正比于：
$$
\delta E \propto \left( 1 + \frac{F_l^{s,a}}{2l+1} \right)
$$
让我们来解读这个优雅的公式。'1' 代表动能代价——它总是正的，总是抵抗畸变。项 $\frac{F_l^{s,a}}{2l+1}$ 代表该特定畸变形状的[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)增益或损失。只有当总能量变化对于*任何*类型的形变都是正的，系统才是稳定的。这意味着括号中的表达式对于对称和反对称通道中的*所有* $l \geq 0$ 都必须为正。这就给了我们著名的**波梅兰丘克[稳定性判据](@keyword=stability_criteria|lang=zh-CN|style=Feynman)** [@problem_id:3013217] [@problem_id:2995985]：
$$
1 + \frac{F_l^s}{2l+1} > 0 \quad \text{以及} \quad 1 + \frac{F_l^a}{2l+1} > 0 \quad \text{对于所有 } l
$$
只要其中一个条件被违反，能量代价就会变为负值。系统发现自发变形在能量上是有利的。球形[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)变得不稳定，并坍缩成一个新的、畸变的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。这种[自发对称性破缺](@keyword=spontaneous_symmetry_breaking|lang=zh-CN|style=Feynman)被称为**[波梅兰丘克不稳定性](@keyword=pomeranchuk_instability|lang=zh-CN|style=Feynman)**。这种不稳定性不是在相互作用 $F_l$ 大且为正（排斥）时发生，而是在它变得足够大且为*负*（吸引），足以压倒动能对球形的偏好时发生 [@problem_id:3013217]。

### 形态展览：不稳定性的后果

当[波梅兰丘克不稳定性](@keyword=pomeranchuk_instability|lang=zh-CN|style=Feynman)发生时，[费米液体](@keyword=fermi_liquid|lang=zh-CN|style=Feynman)经历一次[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，进入一种新的物质状态，其性质由变得不稳定的特定通道（$l$ 和[自旋对称性](@keyword=spin_symmetry|lang=zh-CN|style=Feynman)）决定。

#### 可压缩的液体与自发磁体 ($l=0$)

让我们从最简单的情况开始，$l=0$，即均匀畸变。
*   **[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)通道 ($s$)：** 稳定性条件是 $1 + F_0^s > 0$。量 $(1+F_0^s)$ 与系统的**压缩率** $\kappa$ 直接相关，它衡量当你按压液体时其体积变化了多少 [@problem_id:3016239]。正的压缩率意味着当你挤压液体时，它会反抗。当 $F_0^s$ 从上方接近 $-1$ 时，压缩率发散至无穷大。液体变得无限“松软”。如果 $F_0^s$ 越过 $-1$，压缩率变为负值。挤压它会导致它进一步坍缩！这标志着向相分离的不稳定性——液体自发地分离成高密度和低密度的“水坑”。

*   **自旋通道 ($a$)：** 条件是 $1 + F_0^a > 0$。该通道决定了系统对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的响应。当 $F_0^a$ 接近 $-1$ 时，[磁化率](@keyword=susceptibility|lang=zh-CN|style=Feynman)发散。系统对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)变得极其敏感。如果 $F_0^a$ 越过 $-1$，即使没有外加[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，系统也可以通过自发地对齐准[粒子自旋](@keyword=particle_spin|lang=zh-CN|style=Feynman)来降低其能量。它变成了一个**巡游铁磁体**。这正是在更广泛的[费米液体理论](@keyword=fermi_liquid_theory|lang=zh-CN|style=Feynman)框架内优雅地重新出现的著名斯通纳铁磁性判据 [@problem_id:2995962]。

#### 向列相流体：当球体变为[椭球体](@keyword=ellipsoid|lang=zh-CN|style=Feynman) ($l=2$)

$l=2$ 的情况是“[费米面畸变](@keyword=fermi_surface_distortion|lang=zh-CN|style=Feynman)”思想真正生动体现的地方。这个通道对应于四极形变。稳定性条件是 $1 + \frac{F_2^s}{5} > 0$。[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)发生在[朗道参数](@keyword=landau_parameters|lang=zh-CN|style=Feynman)达到一个特定的负值时：
$$
F_2^s = -5
$$
如果这个通道中的相互作用变得比这个阈值更具吸引性（例如，$F_2^s = -5.1$），球形费米面就会变得不稳定 [@problem_id:87989] [@problem_id:1112362]。会发生什么呢？系统自发地破坏了转动对称性。费米面从一个完美的球体变形为一个类[椭球体](@keyword=ellipsoid|lang=zh-CN|style=Feynman)的形状。这个新状态被称为**[向列相](@keyword=nematic_phase|lang=zh-CN|style=Feynman)费米流体**。

这个名字来自于与液晶的类比。[向列相液晶](@keyword=nematic_liquid_crystals|lang=zh-CN|style=Feynman)的分子沿着一个共同的方向[排列](@keyword=permutation|lang=zh-CN|style=Feynman)，破坏了转动对称性，但它们仍然可以自由流动，保持了平移对称性。类似地，我们的向列相费米流体在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中有一个优选方向，但[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)并未被锁定在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中。

我们甚至可以写出不稳定发生后新的、畸变的费米面是什么样子。如果原始的球形[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)半径为 $k_{F0}$，那么新的、依赖于角度的半径 $k_F(\theta)$ 由下式给出 [@problem_id:56925]：
$$
k_F(\theta) \approx k_{F0} \left(1 + \frac{\Delta}{2 \epsilon_F} \cos(2\theta)\right)
$$
这里，$\Delta$ 是一个衡量畸变强度的小能量参数。$\cos(2\theta)$ 项是四极形状的数学特征——它在两个相反的方向（例如，在 $\theta=0$ 和 $\theta=\pi$）拉伸表面，并在垂直方向（在 $\theta=\pi/2$ 和 $\theta=3\pi/2$）挤压它。我们抽象的稳定性条件催生了电子量子世界的一个具体、有形的新几何形态。

关于奇特的 $l=1$ 情况的一个简要说明：人们可能也[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)在这里发生不稳定性。然而，在一个具有[伽利略不变性](@keyword=galilean_invariance|lang=zh-CN|style=Feynman)的系统（如自由空间中的电子）中，$l=1$ 的畸变仅仅对应于在动量空间中移动整个费米球。这等同于让整个液体运动起来——这是[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)的改变，而不是破坏[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)对称性的真正[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)不稳定性 [@problem_id:3013217]。

### [相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)之声：模式软化

系统是如何从物理上从一个稳定的球体过渡到一个不稳定的球体呢？向[波梅兰丘克不稳定性](@keyword=pomeranchuk_instability|lang=zh-CN|style=Feynman)的趋近不仅仅是一个静态事件；它具有戏剧性的动态后果。

在[无碰撞区](@keyword=collisionless_regime|lang=zh-CN|style=Feynman)，费米液体可以支持称为**[零声](@keyword=zero_sound|lang=zh-CN|style=Feynman)**的独特[集体振荡](@keyword=collective_oscillations|lang=zh-CN|style=Feynman)。这些是费米面上的畸变传播波，一种[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)的沙沙声。对于每个角[谐波](@keyword=harmonic_waves|lang=zh-CN|style=Feynman) $l$，都有一个相应的[零声](@keyword=zero_sound|lang=zh-CN|style=Feynman)模式。这种波的速度由费米液体抵抗该特定形状畸变的“刚度”决定。

而什么决定了刚度？正是我们的稳定性因子 $(1 + \frac{F_l^s}{2l+1})$！[零声](@keyword=zero_sound|lang=zh-CN|style=Feynman)速度的平方与这个因子成正比。

现在，想象一下我们可以调整材料中的相互作用，将 $F_l^s$ 越来越接近临界值 $-(2l+1)$。当我们这样做时，液体的刚度接近于零。因此，相应[零声](@keyword=zero_sound|lang=zh-CN|style=Feynman)波的速度减慢，其频率对于任何给定的波长都变得越来越低。这种现象称为**模式软化**。在精确的[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，频率一直下降到零。[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)冻结成一个静态的、永久的形变 [@problem_id:2995994]。

如果我们越过[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，刚度变为负值。波频率的平方变为负值，意味着频率本身变成了一个虚数。在波的语言中，虚频率意味着[指数增长](@keyword=exponential_growth|lang=zh-CN|style=Feynman)。任何微小的、具有正确形状的随机涨落现在都将在时间上指数级增长，不可阻挡地将系统推入其新的、畸变的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。

这个故事由能量中的高阶项来完成。畸变不会无限增长。一个新的稳定力（一个与畸变平方成正比的项，如朗道展开中的 $\beta u^4$）最终会介入，阻止失控的增长。然后，系统在一个小的但有限的畸变下达到新的平衡，从而降低了其总能量 [@problem_id:2995935]。[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)变得寂静无声，正是新世界诞生的预兆。