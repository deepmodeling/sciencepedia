## 引言
在[物理学](@keyword=physics|lang=zh-CN|style=Feynman)的宏伟殿堂中，能量与[动量守恒](@keyword=momentum_conservation|lang=zh-CN|style=Feynman)是最为神圣的基石之一。在经典的[牛顿力学](@keyword=newtonian_mechanics|lang=zh-CN|style=Feynman)世界里，追踪这些[守恒量](@keyword=conserved_quantity|lang=zh-CN|style=Feynman)相对简单——只需将[孤立系统](@keyword=isolated_systems|lang=zh-CN|style=Feynman)中所有物体的能量与[动量](@keyword=momentum|lang=zh-CN|style=Feynman)相加即可。然而，随着[电磁场](@keyword=electromagnetic_fields|lang=zh-CN|style=Feynman)理论的诞生，[物理学](@keyword=physics|lang=zh-CN|style=Feynman)家们面临一个棘手的难题：能量和[动量](@keyword=momentum|lang=zh-CN|style=Feynman)似乎可以从物质中消失，融入看似空无一物的场中，使得传统的记账方式出现了漏洞。我们如何追踪这些“无形”的能量与[动量](@keyword=momentum|lang=zh-CN|style=Feynman)，并重建一个普适的[守恒定律](@keyword=conservation_laws|lang=zh-CN|style=Feynman)？

为了解决这一问题，[物理学](@keyword=physics|lang=zh-CN|style=Feynman)引入了一个更为强大和普适的工具——[应力-能量张量](@keyword=stress_energy_tensor|lang=zh-CN|style=Feynman)。本文将带领读者深入探索这一核心概念。在第一章中，我们将解码[应力-能量张量](@keyword=stress_energy_tensor|lang=zh-CN|style=Feynman)的结构，理解其如何作为一个“宇宙账本”精确记录能量与[动量](@keyword=momentum|lang=zh-CN|style=Feynman)的[分布](@keyword=generalized_functions|lang=zh-CN|style=Feynman)和流动，并揭示[守恒定律](@keyword=conservation_laws|lang=zh-CN|style=Feynman)与[时空对称性](@keyword=spacetime_symmetry|lang=zh-CN|style=Feynman)之间深刻的内在联系。随后的章节将展示这一理论工具的强大应用，解释它如何统一描述从尘埃到光，再到[真空能](@keyword=vacuum_energy|lang=zh-CN|style=Feynman)等万物的物理行为，并最终在[广义相对论](@keyword=general_relativity|lang=zh-CN|style=Feynman)中扮演[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)之源，与[时空几何](@keyword=spacetime_geometry|lang=zh-CN|style=Feynman)进行宏大的对话。通过本次学习，您将理解[能量-动量守恒](@keyword=energy_momentum_conservation_2|lang=zh-CN|style=Feynman)如何从一个简单的记账法则，[演变](@keyword=descent_with_modification|lang=zh-CN|style=Feynman)为支配宇宙运行的根本规律。

## 原理与机制

想象一下，[物理学](@keyword=physics|lang=zh-CN|style=Feynman)家就像是宇宙的会计师。他们最关心的问题之一，就是追踪宇宙中最宝贵的资产——能量和[动量](@keyword=momentum|lang=zh-CN|style=Feynman)。在牛顿的世界里，这很简单。你有一个球，它有质量和[速度](@keyword=velocity|lang=zh-CN|style=Feynman)，于是它就有[动能和动量](@keyword=kinetic_energy_and_momentum|lang=zh-CN|style=Feynman)。两个球[碰撞](@keyword=collision|lang=zh-CN|style=Feynman)，你只要把它们各自的能量和[动量](@keyword=momentum|lang=zh-CN|style=Feynman)加起来，就知道[碰撞](@keyword=collision|lang=zh-CN|style=Feynman)前后的总量是守恒的。

但是，当 [Michael Faraday](@keyword=michael_faraday|lang=zh-CN|style=Feynman) 和 James Clerk Maxwell 揭示了[电磁场](@keyword=electromagnetic_fields|lang=zh-CN|style=Feynman)的存在后，事情变得复杂起来。能量和[动量](@keyword=momentum|lang=zh-CN|style=Feynman)不再仅仅寄宿于小球那样的实体上，它们也可以[弥散](@keyword=dispersion|lang=zh-CN|style=Feynman)在看似空无一物的空间中，以场的形式存在。当一根天线发射无线电波时，能量和[动量](@keyword=momentum|lang=zh-CN|style=Feynman)就从天线里“流”了出去，散播到广阔的空间之中。我们的会计账本上突然出现了一个巨大的漏洞：能量和[动量](@keyword=momentum|lang=zh-CN|style=Feynman)可以凭空消失在场里！

为了堵上这个漏洞，[物理学](@keyword=physics|lang=zh-CN|style=Feynman)需要一个更强大的记账工具。这个工具不仅要能记录一个点上的能量有多少，还要能描述这些能量是如何流动的，甚至要能告诉我们场内部的“[张力](@keyword=tonicity|lang=zh-CN|style=Feynman)”或“压力”是什么样的。这个恢弘的工具，就是 **[应力-能量张量](@keyword=stress_energy_tensor|lang=zh-CN|style=Feynman) (Stress-Energy Tensor)**，我们用一个优雅的符号 $T^{\mu\nu}$ 来表示它。

### 宇宙的账本：解码 $T^{\mu\nu}$

不要被“[张量](@keyword=tensors|lang=zh-CN|style=Feynman)”这个词吓倒。现在，你可以把它想象成一个 4x4 的信息[矩阵](@keyword=matrix|lang=zh-CN|style=Feynman)，一个关于[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)中任意一点能量与[动量](@keyword=momentum|lang=zh-CN|style=Feynman)状况的“天气图”。这张图的每一个条目都蕴含着丰富的物理意义 [@problem_id:1818973]。

$$
T^{\mu\nu} = 
\begin{pmatrix}
T^{00} & T^{01} & T^{02} & T^{03} \\
T^{10} & T^{11} & T^{12} & T^{13} \\
T^{20} & T^{21} & T^{22} & T^{23} \\
T^{30} & T^{31} & T^{32} & T^{33} 
\end{pmatrix}
$$

- $T^{00}$ 是最直观的一项：**[能量密度](@keyword=energy_density|lang=zh-CN|style=Feynman)**。它告诉你，在一个特定的时间和地点，单位体积内“包含”了多少能量。这包括了物质的[静止质量](@keyword=rest_mass|lang=zh-CN|style=Feynman)能 ($E=mc^2$)、[动能](@keyword=kinetic_energy|lang=zh-CN|style=Feynman)以及场本身储存的能量。

- $T^{0i}$（例如 $T^{01}, T^{02}, T^{03}$）代表**[能量通量](@keyword=energy_flux|lang=zh-CN|style=Feynman)**，也就是能量的流动。$T^{01}$ 描述了能量在 $x$ 方向上流动的速率。如果一道光束沿着 $x$ 轴传播，那么它的 $T^{01}$ 分量就会是一个非零值。

- $T^{i0}$（例如 $T^{10}, T^{20}, T^{30}$）代表**[动量密度](@keyword=momentum_density|lang=zh-CN|style=Feynman)**。$T^{10}$ 告诉你，在单位体积内，有多少指向 $x$ 方向的[动量](@keyword=momentum|lang=zh-CN|style=Feynman)。

现在，奇妙的事情发生了。这个[矩阵](@keyword=matrix|lang=zh-CN|style=Feynman)是**[对称](@keyword=symmetry|lang=zh-CN|style=Feynman)**的，即 $T^{\mu\nu} = T^{\nu\mu}$。特别是，$T^{0i} = T^{i0}$。这可不是数学上的巧合，它揭示了一个深刻的物理联系：**能量的流动必然伴随着[动量](@keyword=momentum|lang=zh-CN|style=Feynman)的存在**。具体来说，它们之间有一个简单的关系：$\vec{g} = \vec{S}/c^2$，其中 $\vec{g}$ 是[动量密度](@keyword=momentum_density|lang=zh-CN|style=Feynman)，而 $\vec{S}$ 是[能量通量](@keyword=energy_flux|lang=zh-CN|style=Feynman)（即坡印廷矢量）。

让我们通过一个“[光子](@keyword=photons|lang=zh-CN|style=Feynman)火箭”的例子来感受一下这个关系的力量 [@problem_id:1819025]。假设一个火箭通过将燃料质量 $\Delta m$ 完全转化为一束完美准直的光来获得[推力](@keyword=thrust|lang=zh-CN|style=Feynman)。根据爱因斯坦的[质能方程](@keyword=e=mc^2|lang=zh-CN|style=Feynman)，这束光携带的能量是 $E = \Delta m c^2$。因为能量的流动就是[动量密度](@keyword=momentum_density|lang=zh-CN|style=Feynman)（乘以 $c^2$），这束光也必须携带[动量](@keyword=momentum|lang=zh-CN|style=Feynman)！它的[动量](@keyword=momentum|lang=zh-CN|style=Feynman)大小就是 $p = E/c = \Delta m c$。根据[动量守恒](@keyword=momentum_conservation|lang=zh-CN|style=Feynman)，火箭会获得一个反向的等大[动量](@keyword=momentum|lang=zh-CN|style=Feynman)，从而被推动。这个效应——[光压](@keyword=radiation_pressure|lang=zh-CN|style=Feynman)，正是驱动[太阳帆](@keyword=solar_sails|lang=zh-CN|style=Feynman)的原理，而它的根源，就藏在[应力-能量张量](@keyword=stress_energy_tensor|lang=zh-CN|style=Feynman)的[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)之中。

- $T^{ij}$（$i, j$ 均为 1, 2, 3）则描述了[动量](@keyword=momentum|lang=zh-CN|style=Feynman)的流动，这在宏观上表现为**压力 (pressure)** 和 **[剪应力](@keyword=shear_stress|lang=zh-CN|style=Feynman) (shear stress)**。想象一下完美的流体，比如一杯静止的水 [@problem_id:1819018]。它会从四面八方给你一个均等的压力 $p$，但不会有任何方向的“拖拽感”（[剪应力](@keyword=shear_stress|lang=zh-CN|style=Feynman)）。在这种情况下，[应力-能量张量](@keyword=stress_energy_tensor|lang=zh-CN|style=Feynman)的空间部分会是一个非常简洁的[对角矩阵](@keyword=diagonal_matrices|lang=zh-CN|style=Feynman)，$T^{11}=T^{22}=T^{33}=p$。而整个静止流体的[张量](@keyword=tensors|lang=zh-CN|style=Feynman)就是漂亮的 $\text{diag}(\rho, p, p, p)$，其中 $\rho$ 是包含了[静止质量](@keyword=rest_mass|lang=zh-CN|style=Feynman)的[能量密度](@keyword=energy_density|lang=zh-CN|style=Feynman)。

### 黄金法则：[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)的本地化表达

有了这个强大的账本 $T^{\mu\nu}$，我们终于可以写下[物理学](@keyword=physics|lang=zh-CN|style=Feynman)中最核心的定律之一：[能量-动量守恒](@keyword=energy_momentum_conservation_2|lang=zh-CN|style=Feynman)。在[相对论](@keyword=theory_of_relativity|lang=zh-CN|style=Feynman)的语言里，它被浓缩成一个极其简洁的方程：

$$
\partial_\mu T^{\mu\nu} = 0
$$

这里的 $\partial_\mu$ 是[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)四维[梯度](@keyword=gradient|lang=zh-CN|style=Feynman)，代表对时间和空间求导。这个方程实际上是四个独立的方程（因为 $\nu$ 可以取 0, 1, 2, 3），分别对应[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)和三个方向上的[动量守恒](@keyword=momentum_conservation|lang=zh-CN|style=Feynman)。

这个方程的深刻之处在于它是一个**局域 (local)** 定律。它不只是说宇宙的[总能量](@keyword=total_energy|lang=zh-CN|style=Feynman)不变，而是说能量不能在一个地方凭空消失，然后在另一个地方凭空出现。能量若要减少，必须是“流”走了。

让我们把 $\nu=0$ 的情况拆开看看，它对应着能量守aporation [@problem_id:1818986]。$\partial_\mu T^{\mu 0} = 0$ 展开后就是：

$$
\frac{\partial T^{00}}{\partial x^0} + \frac{\partial T^{10}}{\partial x^1} + \frac{\partial T^{20}}{\partial x^2} + \frac{\partial T^{30}}{\partial x^3} = 0
$$

回忆一下各个分量的含义，$T^{00}$ 是[能量密度](@keyword=energy_density|lang=zh-CN|style=Feynman) $\mathcal{E}$，$T^{i0}$ 是[动量密度](@keyword=momentum_density|lang=zh-CN|style=Feynman)（等于[能量通量](@keyword=energy_flux|lang=zh-CN|style=Feynman)除以 $c^2$），而 $x^0 = ct$。稍作整理，这个方程就变成了我们更熟悉的形式：

$$
\frac{\partial \mathcal{E}}{\partial t} + \vec{\nabla} \cdot \vec{S} = 0
$$

这正是经典的**[连续性方程](@keyword=continuity_equation|lang=zh-CN|style=Feynman)**！它说，一个区域内[能量[密](@keyword=energy_density|lang=zh-CN|style=Feynman)度](@article_id:301277)的变化率（$\partial \mathcal{E} / \partial t$），必须等于流出该区域的[能量通量](@keyword=energy_flux|lang=zh-CN|style=Feynman)的[散度](@keyword=nabla_dot_v|lang=zh-CN|style=Feynman)（$\vec{\nabla} \cdot \vec{S}$）。一滴墨水在水中[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)，任何一小块区域里墨水浓度的变化，都等于有多少墨水分子流进或流出这个区域的边界。能量-[动量](@keyword=momentum|lang=zh-CN|style=Feynman)的行为也是如此，它们像一种“流体”一样在[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)中流动。

如果一个系统是孤立的，意味着它与外界没有能量或[动量](@keyword=momentum|lang=zh-CN|style=Feynman)[交换](@keyword=crossing_over|lang=zh-CN|style=Feynman)，那么在包围它的遥远[边界面](@keyword=boundary_surface|lang=zh-CN|style=Feynman)上，所有的能量[动量](@keyword=momentum|lang=zh-CN|style=Feynman)流（即 $T^{i\nu}$）都为零。在这种情况下，上述[局域守恒定律](@keyword=local_conservation_law|lang=zh-CN|style=Feynman)通过数学上的[高斯定理](@keyword=divergence_theorem|lang=zh-CN|style=Feynman)，就能保证整个系统内部的[总能量](@keyword=total_energy|lang=zh-CN|style=Feynman)和[总动量](@keyword=total_linear_momentum|lang=zh-CN|style=Feynman)是一个不随时间改变的恒定值 [@problem_id:1819008]。

### 守恒的根源：[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)的[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)

我们不禁要问，为什么能量-[动量](@keyword=momentum|lang=zh-CN|style=Feynman)会如此严格地遵守 $\partial_\mu T^{\mu\nu} = 0$ 这个黄金法则呢？这背后是否隐藏着更深层的原因？

答案是肯定的，而且美得令人屏息。伟大的数学家 [Emmy Noether](@keyword=emmy_noether|lang=zh-CN|style=Feynman) 发现了一个惊人的联系：**物理系统的每一个[连续对称性](@keyword=continuous_symmetry|lang=zh-CN|style=Feynman)，都对应着一个[守恒定律](@keyword=conservation_laws|lang=zh-CN|style=Feynman)** [@problem_id:2090114]。

[能量-动量守恒](@keyword=energy_momentum_conservation_2|lang=zh-CN|style=Feynman)对应的[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)是什么呢？是**[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)的[平移不变性](@keyword=translational_invariance|lang=zh-CN|style=Feynman) (spacetime translational invariance)**。

- **空间[平移[不变](@keyword=translational_invariance|lang=zh-CN|style=Feynman)性](@article_id:300612)**：物理定律在这里和在月球上是一样的。你把整个实验装置平移到另一个地方，实验结果不会改变。这个[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)，通过 Noether 定理，直接导出了**[动量守恒](@keyword=momentum_conservation|lang=zh-CN|style=Feynman)**。

- **[时间平移不变性](@keyword=time_translation_invariance|lang=zh-CN|style=Feynman)**：物理定律在今天和在昨天是一样的。实验结果不依赖于你何时开始测量。这个[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)则导出了**[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)**。

[应力-能量张量](@keyword=stress_energy_tensor|lang=zh-CN|style=Feynman)的守恒律 $\partial_\mu T^{\mu\nu}=0$ 正是这两个[守恒定律](@keyword=conservation_laws|lang=zh-CN|style=Feynman)在[相对论](@keyword=theory_of_relativity|lang=zh-CN|style=Feynman)框架下的统一体。它源于我们宇宙最基本的一个特性：[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)的均匀性。宇宙没有“中心”，也没有“创世时刻”作为绝对的时间起点。正是这种完美的、朴素的[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)，成为了[能量-动量守恒](@keyword=energy_momentum_conservation_2|lang=zh-CN|style=Feynman)这块[物理学](@keyword=physics|lang=zh-CN|style=Feynman)基石的根基所在。

### 当[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)弯曲：[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)的介入

到目前为止，我们都假设[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)是平直的，就像一张平坦的纸。但爱因斯坦告诉我们，物质和能量会使[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)弯曲，这就是[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)的本质。在[弯曲时空](@keyword=curved_spacetime|lang=zh-CN|style=Feynman)中，之前那个简单的求导 $\partial_\mu$ 不再适用，我们必须用一个更复杂的“[协变导数](@keyword=covariant_derivative|lang=zh-CN|style=Feynman)” $\nabla_\mu$ 来代替它。[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)定律也随之升级为：

$$
\nabla_\mu T^{\mu\nu} = 0
$$

这个方程的含义发生了微妙但深刻的变化。它不再表示物质和（非[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)）场的能量[动量](@keyword=momentum|lang=zh-CN|style=Feynman)自身是守恒的。相反，它描述了**物质与[时空几何](@keyword=spacetime_geometry|lang=zh-CN|style=Feynman)之间能量和[动量](@keyword=momentum|lang=zh-CN|style=Feynman)的[交换](@keyword=crossing_over|lang=zh-CN|style=Feynman)**。这就好比一个在弯曲的坡面上[滚动](@keyword=physics_of_rolling|lang=zh-CN|style=Feynman)的小球，它的能量和[动量](@keyword=momentum|lang=zh-CN|style=Feynman)会因为与坡面的相互作用而改变。

这个方程成了爱因斯坦构建[广义相对论](@keyword=general_relativity|lang=zh-CN|style=Feynman)的关键线索 [@problem_id:1832892]。他想建立一个形如“几何 = 物质”的方程。既然“物质”这边由 $T^{\mu\nu}$ 描述，并且满足 $\nabla_\mu T^{\mu\nu} = 0$，那么“几何”那边也必须有一个[张量](@keyword=tensors|lang=zh-CN|style=Feynman) $G^{\mu\nu}$，它由[时空度规](@keyword=spacetime_metrics|lang=zh-CN|style=Feynman)（描述弯曲的量）构成，并且必须自动满足 $\nabla_\mu G^{\mu\nu} = 0$ 这个数学恒等式。幸运的是，这样的几何[张量](@keyword=tensors|lang=zh-CN|style=Feynman)确实存在，它就是大名鼎鼎的**[爱因斯坦张量](@keyword=einstein_tensor|lang=zh-CN|style=Feynman)**，它的这个性质是[黎曼几何](@keyword=riemannian_geometry|lang=zh-CN|style=Feynman)中一个被称为[比安基恒等式](@keyword=bianchi_identity|lang=zh-CN|style=Feynman) (Bianchi identities) 的必然结果。物理定律与数学结构在此处实现了完美的契合。

### [引力能](@keyword=gravitational_energy|lang=zh-CN|style=Feynman)的幽灵

现在，一个自然的问题浮出水面：既然物质的能量可以和[引力场](@keyword=gravitational_fields|lang=zh-CN|style=Feynman)（即[时空几何](@keyword=spacetime_geometry|lang=zh-CN|style=Feynman)）[交换](@keyword=crossing_over|lang=zh-CN|style=Feynman)，我们是否可以定义一个“[引力场](@keyword=gravitational_fields|lang=zh-CN|style=Feynman)的能量”，把它和物质的能量加在一起，得到一个新的、完全守恒的[总能量](@keyword=total_energy|lang=zh-CN|style=Feynman)呢？

答案出人意料：**不可以，至少在任何一个局域的点上是不可以的。**

这听起来很荒谬。[引力波](@keyword=gravitational_waves|lang=zh-CN|style=Feynman)（[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)的涟漪）明明可以携带能量，驱动探测器，为什么我们却不能在空间中指着一个点说“这里的[引力场](@keyword=gravitational_fields|lang=zh-CN|style=Feynman)能量是多少”呢？

原因就在于[广义相对论](@keyword=general_relativity|lang=zh-CN|style=Feynman)的另一个基石——**[等效原理](@keyword=equivalence_principle|lang=zh-CN|style=Feynman) (Equivalence Principle)** [@problem_id:1832837] [@problem_id:1818965]。该原理指出，在一个小的、自由下落的[参考系](@keyword=frames_of_reference|lang=zh-CN|style=Feynman)里（比如一个掉落的电梯或者绕地球飞行的空间站），[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)效应会局部消失。在那个[参考系](@keyword=frames_of_reference|lang=zh-CN|style=Feynman)里，任何仪器都测不到[引力场](@keyword=gravitational_fields|lang=zh-CN|style=Feynman)的存在。

设想一下，如果存在一个真正的、物理的“[引力场](@keyword=gravitational_fields|lang=zh-CN|style=Feynman)[能量密度](@keyword=energy_density|lang=zh-CN|style=Feynman)[张量](@keyword=tensors|lang=zh-CN|style=Feynman)”，那么在那个自由下落的电梯里，它测量出的值必然是零。然而，一个真正的[张量](@keyword=tensors|lang=zh-CN|style=Feynman)如果在一个[参考系](@keyword=frames_of_reference|lang=zh-CN|style=Feynman)中为零，它在任何其他[参考系](@keyword=frames_of_reference|lang=zh-CN|style=Feynman)中也必须为零。这意味着[引力场](@keyword=gravitational_fields|lang=zh-CN|style=Feynman)的能量在任何地方都得是零！这显然是错的。

这个矛盾的唯一出路是：**[引力场](@keyword=gravitational_fields|lang=zh-CN|style=Feynman)的能量是真实的，但它不是一个能够局域化的物理量**。你无法把它像罐头里的沙丁鱼一样塞进空间中的一小块体积里。任何试图描述[引力能](@keyword=gravitational_energy|lang=zh-CN|style=Feynman)量的数学对象（如兰道-栗弗席茨[赝张量](@keyword=pseudotensor|lang=zh-CN|style=Feynman)），都不可避免地依赖于你所选择的坐标系，它们不是真正的[张量](@keyword=tensors|lang=zh-CN|style=Feynman)，[物理学](@keyword=physics|lang=zh-CN|style=Feynman)家称之为“[赝张量](@keyword=pseudotensor|lang=zh-CN|style=Feynman)”。

这意味着，[引力场](@keyword=gravitational_fields|lang=zh-CN|style=Feynman)的能量是一种全局的、[弥散](@keyword=dispersion|lang=zh-CN|style=Feynman)在整个[时空几何](@keyword=spacetime_geometry|lang=zh-CN|style=Feynman)中的属性。你只有在一个足够大的、包含了整个物质系统和其产生的[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)弯曲的区域里谈论[总能量](@keyword=total_energy|lang=zh-CN|style=Feynman)，才是有意义的。在[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)的世界里，能量这个概念变得更加微妙、更加难以捉摸，它与[时空](@keyword=spacetime|lang=zh-CN|style=Feynman)的结构本身密不可分，像一个幽灵，你感受得到它的存在，却无法在任何一个点上将它捕获。这正是[广义相对论](@keyword=general_relativity|lang=zh-CN|style=Feynman)的深邃与魅力所在。

