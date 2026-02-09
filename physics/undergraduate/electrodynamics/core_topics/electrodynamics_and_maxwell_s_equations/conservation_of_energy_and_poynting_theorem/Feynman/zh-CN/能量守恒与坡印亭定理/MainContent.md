## 引言
[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)是[物理学](@keyword=physics|lang=zh-CN|style=Feynman)中最基本的原则之一，但当应用于电和磁时，一个深刻的问题便浮现出来：能量究竟存在于何处？当我们为手机充电或打开一盏灯时，能量是如何从电源精确地传输到我们的设备中的？传统的[电路理论](@keyword=circuit_theory|lang=zh-CN|style=Feynman)对此语焉不详，使我们对于能量的旅程只有一个模糊的直觉。

本文旨在填补这一知识空白。我们将首先揭示一个革命性的概念：能量并非存在于导线中的[电子](@keyword=electrons|lang=zh-CN|style=Feynman)里，而是储存在[周围](@keyword=entourages|lang=zh-CN|style=Feynman)空间无形的[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)与[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman)之中。接着，我们将学习如何利用[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman)来追踪能量在空间中的流动，看到能量如何以出人意料的方式进入[电阻](@keyword=electrical_resistance|lang=zh-CN|style=Feynman)[发热](@keyword=fever|lang=zh-CN|style=Feynman)，或以[电磁波](@keyword=electromagnetic_waves|lang=zh-CN|style=Feynman)的形式穿越真空。最终，我们会探索这一定理在[电路](@keyword=electrical_networks|lang=zh-CN|style=Feynman)、[光学](@keyword=physics_of_light|lang=zh-CN|style=Feynman)、[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)乃至[相对论](@keyword=theory_of_relativity|lang=zh-CN|style=Feynman)等多个领域的惊人应用，从而构建一幅关于[电磁能](@keyword=electromagnetic_energy|lang=zh-CN|style=Feynman)量的完整而统一的图景。

让我们从最基本的问题开始，深入探索电磁世界的能量原理与机制。

## 原理与机制

在[物理学](@keyword=physics|lang=zh-CN|style=Feynman)中，最强大、最深刻的定律往往是[守恒定律](@keyword=conservation_laws|lang=zh-CN|style=Feynman)。[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)或许是其中最著名的一个。我们从孩提时代就知道，能量不能被创造，也不会被消灭，它只能从一种形式转化为另一种形式。当一颗球下落时，它的势能转化为[动能](@keyword=kinetic_energy|lang=zh-CN|style=Feynman)。当你点燃一根火柴，[化学能](@keyword=chemical_potential_energy|lang=zh-CN|style=Feynman)转化为光和热。这个法则是我们理解世界的基石。

但是，当我们将目光投向[电与磁](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)的奇妙[世界时](@keyword=universal_time|lang=zh-CN|style=Feynman)，一个棘手的问题浮现出来：能量究竟“居住”在哪里？当你给一个[电容器充电](@keyword=capacitor_charging|lang=zh-CN|style=Feynman)时，电池做的功去了哪里？当你启动一个电磁铁，[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)从零增加到稳定值，克服了[反电动势](@keyword=back_emf_2|lang=zh-CN|style=Feynman)，这部分能量又存储在何方？答案并不在导[线或](@keyword=wired_or|lang=zh-CN|style=Feynman)金属板上。答案是如此革命性，以至于它永远地改变了我们对“空间”本身的看法：能量，就存在于[电场和磁场](@keyword=electric_and_magnetic_fields|lang=zh-CN|style=Feynman)之中，存在于我们曾以为“空无一物”的空间里。

### 能量的宝库：静态场

让我们从最简单的情景开始思考。想象一下，我们要“建造”一个带电体，比如一个均匀带电的球壳 [@problem_id:1572750]。为此，我们必须从无穷远处，一点一点地搬运[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)，并将它们固定在球壳表面。由于同种[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)相互排斥，每搬运一小份[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)，我们都必须对抗已经存在[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)的排斥力做功。这个过程就像是压缩一根弹簧。我们做的功并没有消失，而是以势能的形式储存了起来。

但是，这个[能量储存](@keyword=energy_storage|lang=zh-CN|style=Feynman)在哪里？在[经典力学](@keyword=classical_mechanics|lang=zh-CN|style=Feynman)中，我们会说[能量储存](@keyword=energy_storage|lang=zh-CN|style=Feynman)在[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)的“构型”中。但电磁理论提供了一个更深刻、更具物理实在性的图像：[能量储存](@keyword=energy_storage|lang=zh-CN|style=Feynman)在[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)[周围](@keyword=entourages|lang=zh-CN|style=Feynman)空间中[弥散](@keyword=dispersion|lang=zh-CN|style=Feynman)的[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)里。球壳[周围](@keyword=entourages|lang=zh-CN|style=Feynman)的空间因为[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)的存在而“绷紧”了，就像张紧的弓。[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)强度越大的地方，能量的“[密度](@keyword=density|lang=zh-CN|style=Feynman)”也越高。具体来说，[电场中的能量密度](@keyword=energy_density_in_electric_fields|lang=zh-CN|style=Feynman) $u_E$ 由一个简洁优美的公式描述：

$$
u_E = \frac{1}{2} \epsilon_0 E^2
$$

其中 $E$ 是[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)强度的大小，$\epsilon_0$ 是[真空介电常数](@keyword=vacuum_permittivity|lang=zh-CN|style=Feynman)。这意味着，只要有[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)存在，空间就不再是空的，而是充满了能量！我们为“建造”球壳所做的全部功，都可以通过对整个空间的[电场能量密度](@keyword=electric_field_energy_density|lang=zh-CN|style=Feynman)进行积分而精确地找回来。

[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman)同样也是一个能量的宝库。考虑一个长长的[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)，当我们接通电源，试图在其中建立[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)时，变化的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)会产生一个“反抗”[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)增加的[反电动势](@keyword=back_emf_2|lang=zh-CN|style=Feynman) [@problem_id:1572747]。电源必须做功来对抗这种“[惯性](@keyword=inertia|lang=zh-CN|style=Feynman)”。这部分功去了哪里？它被用来在[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)内部建立起[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman)，并以[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman)能的形式储存起来。这个过程好比让一个沉重的[飞轮](@keyword=flywheel|lang=zh-CN|style=Feynman)[转动](@keyword=rotational_motion|lang=zh-CN|style=Feynman)起来，你需要持续用力，而你付出的能量则转化为了[飞轮](@keyword=flywheel|lang=zh-CN|style=Feynman)的[转动动能](@keyword=rotational_kinetic_energy|lang=zh-CN|style=Feynman)。[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman)的[能量密度](@keyword=energy_density|lang=zh-CN|style=Feynman) $u_B$ 也有一个与[电场能量密度](@keyword=electric_field_energy_density|lang=zh-CN|style=Feynman)形式上非常相似的表达式：

$$
u_B = \frac{1}{2\mu_0} B^2
$$

在这里，$B$ 是[磁感应强度](@keyword=magnetic_flux_density|lang=zh-CN|style=Feynman)的大小，$\mu_0$ 是[真空磁导率](@keyword=vacuum_permeability|lang=zh-CN|style=Feynman)。

至此，我们已经发现了大自然储藏[电磁能](@keyword=electromagnetic_energy|lang=zh-CN|style=Feynman)量的两个“储蓄账户”：[电场和磁场](@keyword=electric_and_magnetic_fields|lang=zh-CN|style=Feynman)。在静电和静磁的情况下，这两个账户里的“存款”是固定[不变的](@keyword=invariant|lang=zh-CN|style=Feynman)。但当世界开始运动和变化，能量便开始了它的奇妙旅程。

### 能量之流：[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman)

当一盏灯泡[发光](@keyword=luminescence|lang=zh-CN|style=Feynman)时，能量从遥远的[发电](@keyword=power_generation|lang=zh-CN|style=Feynman)厂，通过输电线，最终转化为灯丝中的光和热。这个过程我们习以为常，但能量究竟是如何“旅行”的呢？它是在导线里随着[电子](@keyword=electrons|lang=zh-CN|style=Feynman)一起流动吗？

让我们来看一个经典而又有些违反直觉的例子：一根通有稳定[直流](@keyword=rectilinear_flow|lang=zh-CN|style=Feynman)电的普通[电阻](@keyword=electrical_resistance|lang=zh-CN|style=Feynman)丝 [@problem_id:1572724]。[电阻](@keyword=electrical_resistance|lang=zh-CN|style=Feynman)丝会[发热](@keyword=fever|lang=zh-CN|style=Feynman)，这被称为[焦耳热](@keyword=joule_heating|lang=zh-CN|style=Feynman)。根据[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)，必然有能量源源不断地供给[电阻](@keyword=electrical_resistance|lang=zh-CN|style=Feynman)丝。这能量来自何方，又是如何进入[电阻](@keyword=electrical_resistance|lang=zh-CN|style=Feynman)丝的？几乎所有人都会猜测，能量是通过[电子](@keyword=electrons|lang=zh-CN|style=Feynman)的[碰撞](@keyword=collision|lang=zh-CN|style=Feynman)，沿着导线从电源“流”过来的。然而，麦克斯韦的电磁理论却描绘了一幅截然不同、也远为壮丽的图景。

在一个通有稳定[电流](@keyword=electric_current|lang=zh-CN|style=Feynman) $I$ 的长直导线中，电源在导线内部和[周围](@keyword=entourages|lang=zh-CN|style=Feynman)建立了一个沿导线方向的[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman) $\vec{E}$。同时，[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)还在导线[周围](@keyword=entourages|lang=zh-CN|style=Feynman)产生了一个[环形](@keyword=annulus|lang=zh-CN|style=Feynman)的[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman) $\vec{B}$。[物理学](@keyword=physics|lang=zh-CN|style=Feynman)家约翰·亨利·坡印亭 (John Henry Poynting) 发现，[电磁场](@keyword=electromagnetic_fields|lang=zh-CN|style=Feynman)的[能量流](@keyword=energy_flow|lang=zh-CN|style=Feynman)可以用一个矢量来描述，这个矢量后来被称为[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman) $\vec{S}$：

$$
\vec{S} = \frac{1}{\mu_0} (\vec{E} \times \vec{B})
$$

这个矢量不仅有大小，还有方向，它精确地告诉我们能量在空间中流动的方向[和速率](@keyword=sum_rate|lang=zh-CN|style=Feynman)（单位时间穿过单位面积的能量）。现在，让我们把这个公式应用到我们的[电阻](@keyword=electrical_resistance|lang=zh-CN|style=Feynman)丝上。[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman) $\vec{E}$ 沿着导线方向，而[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman) $\vec{B}$ 在导线表面是环绕着导线的。根据向量叉乘的[右手定则](@keyword=right_hand_rule|lang=zh-CN|style=Feynman)，你会惊奇地发现，[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman) $\vec{S}$ 既不指向电源方向，也不指向[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)方向，而是从导线**外部**的空间，**垂直指向**导线内部！

这是一个多么令人震惊的结论！用来加热[电阻](@keyword=electrical_resistance|lang=zh-CN|style=Feynman)丝的能量，并非沿着导线流动，而是从环绕着导线的空间中，通过[电磁场](@keyword=electromagnetic_fields|lang=zh-CN|style=Feynman)，径直地“注入”到导线中。电池或[发电机](@keyword=electric_generators|lang=zh-CN|style=Feynman)的作用，是在[周围](@keyword=entourages|lang=zh-CN|style=Feynman)空间中建立起特定的[电场和磁场](@keyword=electric_and_magnetic_fields|lang=zh-CN|style=Feynman)，而正是这些场，将能量精准地投送到了需要它的地方。

这个过程可以用一个更加精确的“局部预[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)则”来描述 [@problem_id:1572719]。对于这个稳恒系统，[坡印亭定理](@keyword=poynting_s_theorem|lang=zh-CN|style=Feynman)的[微分形式](@keyword=differential_forms|lang=zh-CN|style=Feynman)可以简化为：

$$
\nabla \cdot \vec{S} = - \vec{J} \cdot \vec{E}
$$

这里的 $\nabla \cdot \vec{S}$ 是[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman)的[散度](@keyword=nabla_dot_v|lang=zh-CN|style=Feynman)，它衡量的是在一个极小的体积内，能量是净流出（[散度](@keyword=nabla_dot_v|lang=zh-CN|style=Feynman)为正）还是净流入（[散度](@keyword=nabla_dot_v|lang=zh-CN|style=Feynman)为负）。而 $\vec{J} \cdot \vec{E}$ 恰好是[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)对[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)做功的[功率密度](@keyword=power_density|lang=zh-CN|style=Feynman)，也就是单位体积内转化为[热能](@keyword=thermal_energy|lang=zh-CN|style=Feynman)的速率。这个方程告诉我们，在一个微小的[体积元](@keyword=volume_element|lang=zh-CN|style=Feynman)内，[电磁场能量](@keyword=electromagnetic_field_energy|lang=zh-CN|style=Feynman)的净流入率，精确地等于该[体积元](@keyword=volume_element|lang=zh-CN|style=Feynman)内转化为[热能](@keyword=thermal_energy|lang=zh-CN|style=Feynman)的速率。能量的账本，在空间的每一点上，都是完美[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)的。

### 完整图景：动态与辐射

现在，让我们把所有的部分都拼合起来。如果[电场和磁场](@keyword=electric_and_magnetic_fields|lang=zh-CN|style=Feynman)本身随时间变化，那么储存在它们之中的[能量密度](@keyword=energy_density|lang=zh-CN|style=Feynman) $u = u_E + u_B$ 也会变化。此时，完整的[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)定律——[坡印亭定理](@keyword=poynting_s_theorem|lang=zh-CN|style=Feynman)——登场了：

$$
\frac{\partial u}{\partial t} + \nabla \cdot \vec{S} = - \vec{J} \cdot \vec{E}
$$

这个方程的含义是如此清晰而深刻。它告诉我们，在一个微小的空间体积里：

（单位时间内[能量[密](@keyword=energy_density|lang=zh-CN|style=Feynman)度](@article_id:301277)的**增加**）+（单位时间内从该体积**流出**的净能量）= -（单位时间内场对[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)**做功**的[功率密度](@keyword=power_density|lang=zh-CN|style=Feynman)）

换句话说，一个区域[内能](@keyword=internal_energy|lang=zh-CN|style=Feynman)量的增加，要么是因为有能量从别处流进来，要么是因为场从[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)那里“拿走”了能量（比如在[加速电荷](@keyword=accelerating_charges|lang=zh-CN|style=Feynman)时）。这正是能量的[连续性方程](@keyword=continuity_equation|lang=zh-CN|style=Feynman)，它保证了能量不会在任何地方凭空出现或消失。

让我们看一个没有[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)（$\vec{J}=0$）的例子：[驻波](@keyword=standing_waves|lang=zh-CN|style=Feynman) [@problem_id:1624534]。[驻波](@keyword=standing_waves|lang=zh-CN|style=Feynman)由两列相向传播的波[叠加](@keyword=superposition|lang=zh-CN|style=Feynman)而成，能量在空间中并没有净的流动，而是在局部“晃荡”。在某些点（波腹），能量在纯[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)能和纯[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman)能之间来回[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。在这些点之间，[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman) $\vec{S}$ 指示着能量在一个[振荡周期](@keyword=period_of_oscillation|lang=zh-CN|style=Feynman)内来回“奔流”。此时，方程变为 $\nabla \cdot \vec{S} = - \frac{\partial u}{\partial t}$。[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman)的[散度](@keyword=nabla_dot_v|lang=zh-CN|style=Feynman)不为零，意味着在一个地方[能量密度](@keyword=energy_density|lang=zh-CN|style=Feynman)正在减少（$\partial u / \partial t < 0$），而在另一个邻近的地方[能量密度](@keyword=energy_density|lang=zh-CN|style=Feynman)正在增加（$\partial u / \partial t > 0$）。能量就这样在空间中此消彼长地“晃荡”，但总量保持守恒。

而当我们谈论从太阳传到地球的光，或从手机基站发出的信号时，我们谈论的是行进的[电磁波](@keyword=electromagnetic_waves|lang=zh-CN|style=Feynman)。对于在真空中传播的平面[电磁波](@keyword=electromagnetic_waves|lang=zh-CN|style=Feynman)，有一个非常和谐的性质：在任何时刻，任何地点，[储存在电场中的能量](@keyword=energy_stored_in_electric_field|lang=zh-CN|style=Feynman)[密度](@keyword=density|lang=zh-CN|style=Feynman)和[储存在磁场中的能量](@keyword=energy_stored_in_magnetic_field|lang=zh-CN|style=Feynman)[密度](@keyword=density|lang=zh-CN|style=Feynman)总是精确相等的 [@problem_id:1790312]！能量在[电与磁](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)之间实现了完美的均分。此时，[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman) $\vec{S}$ 稳定地指向[波的传播](@keyword=wave_propagation|lang=zh-CN|style=Feynman)方向，它的大小就是我们所说的光的强度或[辐射通量](@keyword=radiative_flux|lang=zh-CN|style=Feynman)。正是这股来自太阳的[能量流](@keyword=energy_flow|lang=zh-CN|style=Feynman)，温暖了地球，驱动了生命，甚至可以推动未来的“光帆”飞船。

### 一个奇特的案例：循环的[能量流](@keyword=energy_flow|lang=zh-CN|style=Feynman)

最后，让我们思考一个能加深我们理解的“佯谬”。想象一个静止的[点电荷](@keyword=point_charges|lang=zh-CN|style=Feynman)，旁边放着一根通有稳定[直流](@keyword=rectilinear_flow|lang=zh-CN|style=Feynman)电的长直导线 [@problem_id:1572713]。[点电荷](@keyword=point_charges|lang=zh-CN|style=Feynman)产生一个辐射状的[静电场](@keyword=electrostatic_field|lang=zh-CN|style=Feynman) $\vec{E}$，导[线电流](@keyword=line_current|lang=zh-CN|style=Feynman)产生一个[环形](@keyword=annulus|lang=zh-CN|style=Feynman)的[静磁场](@keyword=static_magnetic_fields|lang=zh-CN|style=Feynman) $\vec{B}$。这里的[电场和磁场](@keyword=electric_and_magnetic_fields|lang=zh-CN|style=Feynman)都是静态的，不随时间变化。

现在我们计算[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman) $\vec{S} = \frac{1}{\mu_0}(\vec{E} \times \vec{B})$。我们会发现，$\vec{S}$ 并不为零！它在空间中形成了一个围绕导线循[环流](@keyword=fluid_circulation|lang=zh-CN|style=Feynman)动的[能量流](@keyword=energy_flow|lang=zh-CN|style=Feynman)。这是否意味着有能量在不停地运动？

答案是肯定的，但这里的“运动”更像是一个封闭的漩涡。如果我们去计算这个[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman)的[散度](@keyword=nabla_dot_v|lang=zh-CN|style=Feynman)，我们会发现 $\nabla \cdot \vec{S} = 0$。这意味着，虽然能量在“流动”，但它既没有源头，也没有汇合点。流入任何一个区域的能量都精确地等于流出的能量。因此，没有任何净的[能量转移](@keyword=energy_transfer|lang=zh-CN|style=Feynman)发生，系统中的[总能量](@keyword=total_energy|lang=zh-CN|style=Feynman)[分布](@keyword=generalized_functions|lang=zh-CN|style=Feynman)保持恒定。这个例子绝妙地提醒我们，[坡印亭矢量](@keyword=poynting_vector|lang=zh-CN|style=Feynman) $\vec{S}$ 本身代表的是“[能流](@keyword=energy_flux|lang=zh-CN|style=Feynman)[密度](@keyword=density|lang=zh-CN|style=Feynman)”，而真正导致能量储量变化的是它的**[散度](@keyword=nabla_dot_v|lang=zh-CN|style=Feynman)** $\nabla \cdot \vec{S}$。一个非零的 $\vec{S}$ 并不一定意味着发生了什么“了不得”的事情。

从将能量看作是[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)的属性，到理解能量是[弥散](@keyword=dispersion|lang=zh-CN|style=Feynman)在场中的一种实在；从静态的能量“宝库”，到动态的能量“流动”，[坡印亭定理](@keyword=poynting_s_theorem|lang=zh-CN|style=Feynman)为我们提供了追踪电磁世界中每一分能量的精确账本。它不仅仅是一个复杂的数学公式，更是[麦克斯韦理论](@keyword=maxwell_s_theory|lang=zh-CN|style=Feynman)内在和谐与统一的辉煌证明，是[物理学](@keyword=physics|lang=zh-CN|style=Feynman)中最美的篇章之一。

