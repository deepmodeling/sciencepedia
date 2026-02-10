## 引言
[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的混沌、涡旋特性是物理学和工程学中最大的挑战之一。虽然基本的 Navier-Stokes 方程可以描述这种运动，但对于大多数实际应用而言，直接求解这些方程在计算上是不可行的。这就需要使用[湍流模型](@keyword=turbulent_flow_modeling|lang=zh-CN|style=Feynman)，这些模型旨在捕捉[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)对平均流的统计效应。核心问题在于如何[对流](@keyword=convection_current|lang=zh-CN|style=Feynman)场方程进行平均化后产生的[雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)项进行建模。为了近似这个项，存在不同的策略，从而产生了一系列复杂度和准确性各不相同的模型。

本文深入探讨了[单方程模型](@keyword=one_equation_models|lang=zh-CN|style=Feynman)，这类模型在保真度上相比更简单的代数方法有了关[键性](@keyword=bond_character|lang=zh-CN|style=Feynman)的提升。通过聚焦于这类模型，我们弥合了基于有根据的猜测与更复杂、计算量更大的方法之间的差距。您将了解到定义这些模型的概念性飞跃，以及它们是如何基于基本物理原理构建的。

第一章“原理与机制”将解构这些模型的工作方式。我们将考察涡[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)的概念、[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)物理量[输运方程](@keyword=transport_equation|lang=zh-CN|style=Feynman)的构建，以及根据物理定律对模型进行[标定](@keyword=calibration|lang=zh-CN|style=Feynman)的关键过程。第二章“应用与跨学科联系”将展示这些模型卓越的通用性，阐述它们在[航空航天工程](@keyword=aerospace_engineering|lang=zh-CN|style=Feynman)、[气象学](@keyword=meteorology|lang=zh-CN|style=Feynman)和[天体物理学](@keyword=astrophysics|lang=zh-CN|style=Feynman)等不同领域的应用，揭示其所描述物理现象的[普适性](@keyword=universality|lang=zh-CN|style=Feynman)。

## 原理与机制

想象一下，试图预测一片被卷入阵风中的树叶的路径。这简直是徒劳无功。空气以一种混乱、不可预测的方式旋转和翻滚。这就是[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)。现在，想象你正在设计一架大型喷气式飞机。你不能只是摊开双手说这太复杂了！你需要理解所有这些旋转和翻滚对飞机的*平均*影响。这正是[湍流建模](@keyword=turbulence_modeling|lang=zh-CN|style=Feynman)的核心挑战：驯服混沌，不是通过追踪每一个涡旋，而是通过捕捉其集体的、统计学的行为。

著名的 Navier-Stokes 方程，即[流体运动](@keyword=fluid_motion|lang=zh-CN|style=Feynman)的宏伟定律，如果你有足够强大的计算机和无限的时间，它完全能够描述每一个细微的涡旋。但我们两者都没有。所以，我们作弊。我们使用一种称为雷诺平均的数学技巧，通过对时间进行平均来平滑流场。问题是，这个过程留下了一个神秘的新项——**[雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)**，它代表了由[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)脉动自身输运的[动量](@keyword=momentum|lang=zh-CN|style=Feynman)。整个[湍流建模](@keyword=turbulence_modeling|lang=zh-CN|style=Feynman)的游戏归结为找到一种方法来近似这个项。

### [湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)的游戏

解决[雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)问题最简洁优美的思想之一是 **Boussinesq 假设**。它提出，平均而言，[湍流涡旋](@keyword=turbulent_eddies|lang=zh-CN|style=Feynman)的行为有点像气体中的分子，会产生一种“额外”的[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)。正如分子[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)源于分子的随机运动，这种新的**[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)**或**涡[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)** ($\nu_t$) 源于涡旋的搅动。这是一个极富直觉的飞跃！它表明，复杂的[雷诺应力张量](@keyword=reynolds_stress_tensor|lang=zh-CN|style=Feynman)可以直接与平均流的[应变率](@keyword=strain_rate|lang=zh-CN|style=Feynman)相关联，而 $\nu_t$ 则是比例常数。

突然之间，我们寻找六个未知应力分量的艰巨任务简化为寻找一个标量：$\nu_t$。但如何寻找呢？让我们来玩一个量纲游戏。[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)的量纲是长度的平方除以时间，或者说是一个[特征速度](@keyword=characteristic_speeds|lang=zh-CN|style=Feynman)尺度乘以一个[特征长度尺度](@keyword=characteristic_length_scales|lang=zh-CN|style=Feynman)。

$$
\nu_t \sim v' \ell
$$

在这里，$v'$ 代表[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)脉动的典型[速度](@keyword=velocity|lang=zh-CN|style=Feynman)，$\ell$ 代表最大的、含能涡旋的典型尺寸。每一种[湍流模型](@keyword=turbulent_flow_modeling|lang=zh-CN|style=Feynman)，无论以何种方式，都是为这两个尺度提供一个计算公式的尝试。

最简单的计算公式被称为**零方程模型**。它们是纯代数的，意味着它们利用平均流的局部属性（如与壁面的距离或[速度梯度](@keyword=velocity_gradient|lang=zh-CN|style=Feynman)）来猜测 $v'$ 和 $\ell$。它们计算[速度](@keyword=velocity|lang=zh-CN|style=Feynman)快，但没有记忆。它们对[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)是如何到达那里的，或者将要去向何方一无所知。它们只对空间和时间上某一点的流动条件做出反应。

### 伟大的飞跃：从猜测到输运

为了做得更好，我们需要给我们的模型一个记忆。[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)不是一个局部现象；它在一个地方产生，随流[场移](@keyword=field_shift|lang=zh-CN|style=Feynman)动，在另一个地方消亡。它有自己的历史。概念上的巨大飞跃是停止猜测其中一个[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)尺度，转而为其建立一个**[输运方程](@keyword=transport_equation|lang=zh-CN|style=Feynman)** [@problem_id:1766432]。这正是一个**[单方程模型](@keyword=one_equation_models|lang=zh-CN|style=Feynman)**的定义。

把它想象成一个像[湍动能](@keyword=turbulent_kinetic_energy|lang=zh-CN|style=Feynman) $k$（它为我们提供了[速度](@keyword=velocity|lang=zh-CN|style=Feynman)尺度 $v' \sim \sqrt{k}$）这样的物理量的财务预算。一个[输运方程](@keyword=transport_equation|lang=zh-CN|style=Feynman)表明，在一个微小流体元中 $k$ 的变化率等于其产生量、[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)量以及通过[对流](@keyword=convection_current|lang=zh-CN|style=Feynman)和[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)移入或移出量的总和。

$$
\frac{Dk}{Dt} = \text{产生项} - \text{耗散项} + \text{输运项}
$$

通过将这个额外的[微分方程](@keyword=differential_equations|lang=zh-CN|style=Feynman)与主流动方程一起求解，模型现在考虑了[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的历史。它知道它所看到的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)是在上游产生的，还是已经缓慢[衰减](@keyword=attenuation|lang=zh-CN|style=Feynman)了很长时间。长度尺度 $\ell$ 仍然由一个简单的代数公式提供，但现在我们正在求解[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)能量的生命历程。

### [单方程模型](@keyword=one_equation_models|lang=zh-CN|style=Feynman)的剖析

让我们来剖析一个著名且稳健的例子：**Spalart-Allmaras (SA) 模型**。它不求解[湍动能](@keyword=turbulent_kinetic_energy|lang=zh-CN|style=Feynman)，而是为一个巧妙的变量 $\tilde{\nu}$ 求解一个[输运方程](@keyword=transport_equation|lang=zh-CN|style=Feynman)，该变量与涡[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)直接相关。其原理完全相同。它的[输运方程](@keyword=transport_equation|lang=zh-CN|style=Feynman)是[源项](@keyword=source_term|lang=zh-CN|style=Feynman)和汇项的[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)。

**产生项：** [湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)在哪里诞生？它由平均流供给。当不同[速度](@keyword=velocity|lang=zh-CN|style=Feynman)的流体层相互滑过时（一种称为剪切的现象），流动变得不稳定并产生涡旋。创造这些涡旋的能量是从平均流的[动能](@keyword=kinetic_energy|lang=zh-CN|style=Feynman)中窃取的。因此，模型中的产生项必须与流场的平均应变或[涡量](@keyword=curl_of_velocity_field|lang=zh-CN|style=Feynman)成正比。在[湍流边界层](@keyword=turbulent_boundary_layer|lang=zh-CN|style=Feynman)中，这种产生是持续不断的，不断为混沌运动提供能量 [@problem_id:462770]。

**[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)项：** 如果[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)只被产生，流动将变得无限混沌。必须有东西来摧毁它。在固体壁面附近，会发生两件事：[无滑移条件](@keyword=no_slip_condition|lang=zh-CN|style=Feynman)迫使[速度](@keyword=velocity|lang=zh-CN|style=Feynman)为零，并且壁面本身物理上限制了涡旋的尺寸。[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)，作为[相对运动](@keyword=relative_motion|lang=zh-CN|style=Feynman)的克星，会抑制涡旋，将其[动能](@keyword=kinetic_energy|lang=zh-CN|style=Feynman)转化为热量。我们如何对此进行建模？

让我们运用一些物理推理。[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)的速率当然应该取决于有多少“东西”可以被[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)——即我们的变量 $\tilde{\nu}$。它还必须依赖于[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)过程的一个[特征时间尺度](@keyword=characteristic_timescale|lang=zh-CN|style=Feynman)。这个时间尺度是什么？在壁面附近，最重要的长度尺度是到壁面的距离 $d$。涡旋本身的[速度](@keyword=velocity|lang=zh-CN|style=Feynman)尺度可以与 $\tilde{\nu}$ 和 $d$ 相关联。将这些因素放在一起，一个漂亮的[量纲分析](@keyword=dimensionless_analysis|lang=zh-CN|style=Feynman)告诉我们，[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)时间尺度必须与 $d^2/\tilde{\nu}$ 成正比。那么，[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)*率*就与 $\tilde{\nu}$ 除以这个时间尺度成正比，从而得到一个形如 $(\tilde{\nu}/d)^2$ 的项 [@problem_id:578282]。这不是一个随意的猜测；这是由涡旋在表面附近消亡的物理过程所决定的形式。

### [校准](@keyword=calibration|lang=zh-CN|style=Feynman)音叉：依据[壁面律](@keyword=logarithmic_law_of_the_wall|lang=zh-CN|style=Feynman)进行[标定](@keyword=calibration|lang=zh-CN|style=Feynman)

所以我们有了一台机器，一个带有产生项和[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)项的[输运方程](@keyword=transport_equation|lang=zh-CN|style=Feynman)，其中点缀着一些像 $c_{b1}$ 和 $c_{w1}$ 这样的常数。我们如何设置这些参数？这些常数仅仅是随意的“凑合因子”吗？绝对不是。它们以制表匠般的精度进行[标定](@keyword=calibration|lang=zh-CN|style=Feynman)，根据[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)最可靠、最普适的特征进行调整。

最终的基准是**[壁面律](@keyword=logarithmic_law_of_the_wall|lang=zh-CN|style=Feynman)**。在[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)靠近壁面但又在黏糊糊的黏性子层之外的区域，出现了一个惊人简单的区域，称为对数层或“log-layer”。在这里，[速度剖面](@keyword=velocity_profile|lang=zh-CN|style=Feynman)遵循一个普适的对数形状，几十年的实验表明，涡[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)遵循一个简单的[线性关系](@keyword=linear_relationship|lang=zh-CN|style=Feynman)：

$$
\nu_t = \kappa u_\tau y
$$

其中 $u_\tau$ 是一个称为**[摩擦速度](@keyword=friction_velocity|lang=zh-CN|style=Feynman)**的[特征速度](@keyword=characteristic_speeds|lang=zh-CN|style=Feynman)，$y$ 是与壁面的距离，而 $\kappa$ 是**von Kármán 常数**，[湍流理论](@keyword=turbulence_theory|lang=zh-CN|style=Feynman)中的一个基本普适数（其值约为 $0.41$）。

在这个对数层中，流动达到一种近乎完美的**[局部平衡](@keyword=local_equilibrium|lang=zh-CN|style=Feynman)**状态：[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的产生几乎完全被其[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)所[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)。[对流](@keyword=convection_current|lang=zh-CN|style=Feynman)和[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)是次要的。通过采用我们的[单方程模型](@keyword=one_equation_models|lang=zh-CN|style=Feynman)并应用这个[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)条件（$P \approx D$），我们可以求解出它预测的涡[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman) [@problem_id:668680]。然后，我们要求模型的预测与现实相符。我们强制模型再现 $\nu_t = \kappa u_\tau y$ [@problem_id:669851]。

这种[标定](@keyword=calibration|lang=zh-CN|style=Feynman)行为是神奇的。它在方程中的抽象常数与对数律的基本物理原理之间建立了一个直接的联系。例如，通过强制这种一致性，我们可以推导出模型常数 $c_{b1}$、$c_{w1}$ 与 von Kármán 常数 $\kappa$ 之间的明确关系 [@problem_id:641328]。如果我们考虑完整的[输运方程](@keyword=transport_equation|lang=zh-CN|style=Feynman)，包括[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)项，我们可以推导出对模型系数更精确的约束 [@problem_id:659893]。模型不再是一个黑匣子；其内部结构从根本上与经过实验验证的真理联系在一起。我们甚至可以反向推导，证明该模型在这一区域等同于经典的[混合长度](@keyword=mixing_length|lang=zh-CN|style=Feynman)模型，揭示了不同层次[湍流理论](@keyword=turbulence_theory|lang=zh-CN|style=Feynman)之间的深层联系 [@problem_id:644258]。

### 了解边界：模型失足之处

尽管这些模型十分优雅，我们绝不能忘记它们是*模型*。它们所做的最重要的简化假设是 Boussinesq 假设本身：即[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)应力与平均[应变率](@keyword=strain_rate|lang=zh-CN|style=Feynman)成正比。这对于许多简单的[剪切流](@keyword=shear_flow|lang=zh-CN|style=Feynman)（如平板上的流动）来说效果出奇地好。但自然界比这要狡猾得多。

考虑一个沿着急弯流动的流场，就像河湾里的水流。[流线](@keyword=streamlines|lang=zh-CN|style=Feynman)是弯曲的。这种[曲率](@keyword=curvature|lang=zh-CN|style=Feynman)引入的[离心力](@keyword=centrifugal_force|lang=zh-CN|style=Feynman)既可以稳定[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)，也可以使其不稳定。在弯道的外侧（凸面），[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)受到抑制。在内侧（凹面），[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)得到增强。

像 Spalart-Allmaras 这样的标准[单方程模型](@keyword=one_equation_models|lang=zh-CN|style=Feynman)完全无法感知这种效应。它的产生项只看到局部的剪切，而看不到[流线](@keyword=streamlines|lang=zh-CN|style=Feynman)的[曲率](@keyword=curvature|lang=zh-CN|style=Feynman)。只要[速度剖面](@keyword=velocity_profile|lang=zh-CN|style=Feynman)相同，无论流动是直的还是弯的，它都会预测相同水平的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)。在具有强凸面[曲率](@keyword=curvature|lang=zh-CN|style=Feynman)的流动中，真实[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)被严重抑制，而该模型将严重高估涡[黏度](@keyword=viscosity|lang=zh-CN|style=Feynman)和[热传递](@keyword=heat_transfer|lang=zh-CN|style=Feynman)。这不是一个小错误；这是根植于模型核心假设的定性失败 [@problem_id:2447856]。更高级的模型，如[双方程模型](@keyword=two_equation_models|lang=zh-CN|style=Feynman)，可以对旋转和[曲率](@keyword=curvature|lang=zh-CN|style=Feynman)变得敏感，但这有力地提醒我们：永远要理解你所使用工具的假设。

### 优雅的转变：通往模拟涡旋之路

[单方程模型](@keyword=one_equation_models|lang=zh-CN|style=Feynman)的故事并没有因其局限性而结束。其稳健的[输运方程](@keyword=transport_equation|lang=zh-CN|style=Feynman)框架具有卓越的适应性。一种名为**[分离](@keyword=fractionation|lang=zh-CN|style=Feynman)涡模拟 (DES)** 的巧妙修改，将该模型转换为另一种用途。

回想一下，[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)项取决于到壁面的距离 $d$。DES 修改做了一个简单而深刻的改变：它用一个新的长度尺度 $\tilde{d}$ 替换了 $d$，这个新尺度是壁面距离和[计算网格](@keyword=computational_mesh|lang=zh-CN|style=Feynman)局部尺寸 $\Delta$ 的*最小值*。

$$
\tilde{d} = \min(d, C_{DES}\Delta)
$$

在壁面附近，$d$ 很小，所以 $\tilde{d} = d$，模型表现如常，模拟[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的平均效应。但在远离壁面的地方，我们可能使用足够精细的网格来解析大涡旋，此时 $\Delta$ 可能变得比 $d$ 小。在这种情况下，$\tilde{d} = C_{DES}\Delta$。[耗散](@keyword=dissipation|lang=zh-CN|style=Feynman)项现在依赖于网格尺寸。这一改变有效地关闭了模型作为统计替代品的角色，并将其转变为用于[大涡模拟 (LES)](@keyword=large_eddy_simulation_(les)|lang=zh-CN|style=Feynman) 的[亚格子尺度模型](@keyword=subgrid_scale_models|lang=zh-CN|style=Feynman)，LES 直接计算大涡旋，而只对小的、未解析的涡旋进行建模 [@problem_id:578298]。

这个简单而优雅的转换展示了其背后物理原理的力量和美感。通过理解主导[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的长度尺度的作用，我们可以调整一个单一的[输运方程](@keyword=transport_equation|lang=zh-CN|style=Feynman)来执行两种完全不同的任务，从而在统计建模和直接模拟之间架起一座桥梁。从一个简单的量纲论证到一个复杂的[混合模型](@keyword=mixture_models|lang=zh-CN|style=Feynman)，[单方程模型](@keyword=one_equation_models|lang=zh-CN|style=Feynman)的历程证明了物理直觉和数学优雅在我们探索[周围](@keyword=entourages|lang=zh-CN|style=Feynman)[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)世界中的强大力量。

