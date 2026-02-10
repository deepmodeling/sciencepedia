## 引言
在物理学和工程学的研究中，我们通常从理想化的[稳态](@keyword=steady_state_2|lang=zh-CN|style=Feynman)开始，在[稳态](@keyword=steady_state_2|lang=zh-CN|style=Feynman)下，条件随时间保持不变。然而，现实世界本质上是动态的，由变化、信号和瞬变所定义。这个动态领域由[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)——即随时间变化的电流——所支配。理解这些现象不仅仅是一项学术活动，它对于掌握从[电磁波](@keyword=electromagnetic_waves|lang=zh-CN|style=Feynman)到我们身体机能等一切事物背后的原理至关重要。

本文旨在弥合稳恒电流的简单世界与复杂的、随时间变化的现实之间的鸿沟。它全面概述了[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)，引导读者了解其基本性质和深远影响。第一章“原理与机制”深入探讨了定义[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)的核心物理定律，包括电荷守恒、[连续性方程](@keyword=equation_of_continuity|lang=zh-CN|style=Feynman)以及麦克斯韦革命性的[位移电流](@keyword=displacement_current|lang=zh-CN|style=Feynman)补充。第二章“应用与跨学科联系”则探索这些原理如何在技术与自然界中体现，揭示了瞬态电流在电子学、[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)乃至构成生命的生物过程中的关键作用。

## 原理与机制

在我们理解世界的旅程中，我们通常从最简单的情形开始。我们想象水稳定地流过河流，空气平滑地掠过机翼，或电流均匀地穿过电线。这是一个“[稳态](@keyword=steady_state_2|lang=zh-CN|style=Feynman)”的世界，一个事物随时间保持不变的、平静且可预测的领域。但现实世界很少如此平静。它是一个充满变化、闪光与爆裂、信号与心跳的世界。这是一个由**[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)**支配的世界，理解它们就是理解自然本身的动力学。

### 不容违背的[电荷守恒](@keyword=charge_conservation|lang=zh-CN|style=Feynman)定律

让我们从一条基本到几乎可称之为宇宙会计账本的规则开始：你不能创造或消灭[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，只能移动它。在熟悉的简单电子电路世界里，这条原理有一个著名的名字：**[基尔霍夫电流定律](@keyword=kirchhoff_s_current_law|lang=zh-CN|style=Feynman) (KCL)**。它指出，在任何结点处，流入的总电流量必须精确等于流出的总电流量。

想象一个结点，两个电流 $I_1(t)$ 和 $I_2(t)$ 流入，第三个电流 $I_3(t)$ 流出。如果系统是“稳恒的”，即结点本身不能像一个微小的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)蓄水池那样储存[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，那么 KCL 在每个瞬间都成立：$I_1(t) + I_2(t) = I_3(t)$。很简单。流入的必须等于流出的。

但如果结点*可以*储存[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)呢？如果它不只是一个点，而是一个小[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)、一个分子或一个生物细胞呢？那么，这笔账就变得更有趣了。如果流入的电流多于流出的电流，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $Q$ 就会开始在结点处积聚。这个积聚的速率 $\frac{dQ}{dt}$ 就是净流入减去净流出。我们的方程变为：

$$
\frac{dQ}{dt} = I_{\text{in}} - I_{\text{out}} = I_1(t) + I_2(t) - I_3(t)
$$

这个简单的修正是通往整个非稳恒现象世界的大门。任何时候只要 $\frac{dQ}{dt}$ 不为零，我们处理的就是非稳恒情况。这可能发生在[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)电流如 $I_0 \sin(\omega t)$、斜坡电流如 $\alpha t$ 或衰减电流如 $\beta \exp(-t/\tau_c)$ 的情况下。一旦电流变得不平衡，某个地方的某个东西就在充电或放电。

这个想法可以更普遍地表达。与其考虑单个结点，不如考虑空间中的任何区域。[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的流动由**[电流密度](@keyword=current_density|lang=zh-CN|style=Feynman)矢量** $\vec{J}$ 描述，它告诉我们每一点上电流的大小和方向。[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的“堆积”由变化的**电荷密度** $\rho$ 描述。连接它们的记账规则是物理学中最优雅和最强大的表述之一，即**[连续性方程](@keyword=equation_of_continuity|lang=zh-CN|style=Feynman)**：

$$
\nabla \cdot \vec{J} + \frac{\partial \rho}{\partial t} = 0
$$

项 $\nabla \cdot \vec{J}$ 是[电流密度的散度](@keyword=divergence_of_current_density|lang=zh-CN|style=Feynman)。它衡量电流从一个点“散开”的程度，这恰好是[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)离开该点的速率。该方程表明，电流流出一个微小体积的速率（$\nabla \cdot \vec{J}$）必须与该体积内储存的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)减少的速率（$-\frac{\partial \rho}{\partial t}$）相平衡。[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)是守恒的，无论何时何地。

因此，**稳恒电流**是一种可以永远流动而不会导致任何[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)积聚或流失的电流。要实现这一点，电荷密度必须不随时间变化，因此 $\frac{\partial \rho}{\partial t} = 0$。[连续性方程](@keyword=equation_of_continuity|lang=zh-CN|style=Feynman)于是告诉我们任何稳恒电流的条件：$\nabla \cdot \vec{J} = 0$。电流的流线永远不能有起点或终点；它们必须形成闭合回路或延伸至无穷远。像 $\vec{J} = C(y\hat{x} - x\hat{y})$ 这样的电流密度描述了一种旋转的、涡旋状的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)流动。在任何一点，流入的电流都与流出的电流完美平衡，因此其散度为零，它可以代表一种完全稳恒但非均匀的电流。任何满足 $\nabla \cdot \vec{J} \neq 0$ 的电流，根据定义，都是[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)。

### 基石的裂缝：[安培定律](@keyword=ampere_s_law|lang=zh-CN|style=Feynman)的危机

这条看似简单的[电荷守恒](@keyword=charge_conservation|lang=zh-CN|style=Feynman)规则引发了[物理学史](@keyword=history_of_physics|lang=zh-CN|style=Feynman)上最伟大的思想飞跃之一。在19世纪中叶，电学和磁学的定律已接近完备。其中一条定律是安培定律，其原始形式指出[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)由电流产生：$\nabla \times \vec{B} = \mu_0 \vec{J}$。

问题就在这里。有一个数学恒等式表明，一个[旋度的散度](@keyword=divergence_of_a_curl|lang=zh-CN|style=Feynman)恒为零：$\nabla \cdot (\nabla \times \vec{B}) = 0$。如果我们将此应用于[安培定律](@keyword=ampere_s_law|lang=zh-CN|style=Feynman)，我们必然得出结论 $\nabla \cdot (\mu_0 \vec{J}) = 0$，这意味着对于该定律所描述的任何情况，$\nabla \cdot \vec{J}$ 都必须为零。

但是等等！我们刚刚确定，对于[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)，$\nabla \cdot \vec{J} = -\frac{\partial \rho}{\partial t}$，这*不*是零。这意味着，当时的[安培定律](@keyword=ampere_s_law|lang=zh-CN|style=Feynman)在逻辑上与[电荷守恒](@keyword=charge_conservation|lang=zh-CN|style=Feynman)定律在任何[电荷密度](@keyword=charge_density|lang=zh-CN|style=Feynman)随时间变化的情况下（例如给[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)充电）不一致！旧定律只适用于稳恒电流，即 $\frac{\partial \rho}{\partial t} = 0$ 的情况。

这正是 James Clerk Maxwell 解决的危机。他意识到缺少了某些东西。如果你在给一个[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)充电，电流会流过导线，但似乎在极板处停止了。那么，“信息”是如何穿过间隙以产生我们知道存在于那里的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的呢？Maxwell 提出，间隙中**变化的电场**本身就像一种电流，他称之为**位移电流**，$\vec{J}_D = \epsilon_0 \frac{\partial \vec{E}}{\partial t}$。

通过将这一项加入安培定律，他创建了完整的麦克斯韦-安培方程：
$$
\nabla \times \vec{B} = \mu_0 \left( \vec{J} + \epsilon_0 \frac{\partial \vec{E}}{\partial t} \right)
$$
这修正了一切。新的、广义的“电流”（$\vec{J} + \vec{J}_D$）现在始终是[无散度](@keyword=divergence_free|lang=zh-CN|style=Feynman)的，在所有情况下都满足电荷守恒。这不仅仅是一个补丁，而是一场革命。它揭示了变化的电场会产生[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，正如 Faraday 已经证明变化的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)会产生电场一样。这种美丽的对称性是电磁波——即光本身——的基础。对[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)的研究迫使我们认识到，光、电和磁都是一个统一整体的几个方面。

### 变化中的世界：感应与瞬态电流

既然我们有了正确的定律，就让我们看看它们的作用。[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)最引人注目的来源是**法拉第电磁感应定律**：穿过电路回路的磁通量变化会感应出[电动势 (EMF)](@keyword=electromotive_force_(emf)|lang=zh-CN|style=Feynman)，从而驱动电流。

$$
\mathcal{E} = - \frac{d\Phi_B}{dt}
$$

没有哪里比[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)更能完美地说明这一原理了。[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的电阻为零。如果你将一个[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)置于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中，然后试图改变该[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，法拉第定律就会生效。它会在环中感应出电流。因为电阻为零，这个[感应电流](@keyword=induced_current|lang=zh-CN|style=Feynman)会毫不费力地流动，增长到恰好能产生自身[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的强度，该[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)完美地抵消了外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的变化。结果是什么呢？穿过环的总[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)保持不变。如果你在一个普通环内部将[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)的电流增加到 $I_0$，*然后*使环变为超导状态，磁通量就被“锁定”了。如果你接着关闭[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)，一个**[持续电流](@keyword=persistent_currents|lang=zh-CN|style=Feynman)**将在环中永远流动，维持着初始的磁通量。这是一个非稳恒过程（变化的外部场）催生出一个新的稳恒电流。

在有电阻的普通导体世界中，情况不那么持久，但同样重要。当你拨动一个包含电感和电容的电路中的开关时，电流和电压不会瞬间达到它们的新值。电感器具有类似惯性的特性，反对电流的变化；而[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)则能够储存[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，这两种元件使得系统需要一段时间来调整。在这个调整期间，我们会得到**瞬态电流**。

这些瞬态由电路的电阻、电感和电容决定。例如，在一个有电感和电阻的电路中，[运动方程](@keyword=equations_of_motion|lang=zh-CN|style=Feynman)可以写成紧凑的矩阵形式：$\frac{d\vec{I}}{dt} = A\vec{I} + \vec{f}(t)$。关键的物理原理隐藏在矩阵 $A$ 中。该矩阵的元素单位是时间的倒数（$s^{-1}$），它们代表瞬态电流衰减或[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的特征速率。它们定义了时间常数（如 $\tau = L/R$），告诉我们电路有多“迟钝”。当系统从一个状态过渡到另一个状态时，这些瞬态电流负责耗散能量，通常以热量的形式。

当然，并非所有[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)都是会消失的瞬态电流。我们可以持续地驱动它们，最著名的形式是**交流电 (AC)**。如果我们让一个交流电，比如 $I(t) = I_0 \cos(\omega t)$，通过两条相邻的导线，它们之间的力也会随时间变化。如果电流同相，它们之间的力仍然是吸引力，但其大小会脉动，变化规律为 $\cos^2(\omega t)$。这种脉动力是无数设备（从电动机到扬声器）背后的原理。

### 电线之外：更广泛的电流家族

[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)的概念比我们目前所见的还要广泛。它延伸到任何[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)在运动的情况，即使它不是铜线中的电子流。

考虑金属电极和盐[水溶液](@keyword=aqueous_solutions|lang=zh-CN|style=Feynman)之间的界面，这是所有生物学和电化学的基础情景。表面会形成一个**[电化学双电层](@keyword=electrochemical_double_layer|lang=zh-CN|style=Feynman)**：溶液中的一层离子被吸引到带电的电极表面。这个结构的作用就像一个微型[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)。如果你改变电极上的电压，溶液中的离子必须物理移动来为这个[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)充电或放电。离子的这种移动是一种真实的电流，但实际上没有电子从电极跃入溶液中。这被称为**非[法拉第电流](@keyword=faradaic_current|lang=zh-CN|style=Feynman)**，或称电容性电流。它由我们熟悉的[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)方程描述，$I_{nf} = C_{dl} \frac{dV}{dt}$。神经冲动就是这样传播的——以离子穿过[细胞膜](@keyword=plasma_membrane|lang=zh-CN|style=Feynman)的波的形式，这是一种携带信息的[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)。

最后，让我们看看所有[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)中最基本的一种：噪声。放大看任何一个电阻器，即使它上面没有电压。电阻器中的原子因热能而晃动和[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。这种持续的搅动会推挤自由电子，使它们随机地舞动。在任何给定瞬间，纯粹由于偶然，向左移动的电子可能比向右的多，从而产生一个微小而短暂的电流脉冲。这就是**热噪声**，或称[约翰逊-奈奎斯特噪声](@keyword=johnson_nyquist_noise|lang=zh-CN|style=Feynman)。它就是终极的[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)：一种存在于任何温度高于绝对零度的导体中的、混乱随机的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)运动。虽然平均电流为零，但其均方根 (RMS) 值不为零，它为任何电子测量的灵敏度设定了一个基本限制。这种噪声是热力学第二定律的低语，在电子的舞蹈中上演。

从支配光本身的宏伟麦克斯韦定律，到[拨动开关](@keyword=toggle_switch|lang=zh-CN|style=Feynman)时的瞬时火花，再到我们大脑中形成思想的微妙离子转移，世界充满了[非稳恒电流](@keyword=non_steady_currents|lang=zh-CN|style=Feynman)。它们是变化的语言，行动的媒介，也是一个动态宇宙的根本构造。