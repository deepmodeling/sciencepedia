## 应用与[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)学科联系

在前一章中，我们深入探讨了将强形式的[平衡方程](@keyword=equilibrium_equations|lang=zh-CN|style=Feynman)——这一描述自然法则的[微分](@keyword=pushforward|lang=zh-CN|style=Feynman)语言——转化为弱[形式的积分](@keyword=integration_of_forms|lang=zh-CN|style=Feynman)语言的精妙过程。我们发现，这一转化的核心正是虚功原理，一个看似抽象但功能强大的概念。现在，我们将踏上一段新的旅程，去探索这一原理如何从纸上的方程，化身为理解和改造我们脚下这片大地的有力工具。您将会看到，这单一、优美的思想，如同一把钥匙，开启了从预测建筑沉降到分析地震响应，乃至驾驭地下能源的无数扇门。这不仅仅是公式的应用，更是一场发现物理定律内在统一性与和谐之美的智力探险。

### 坚实地球：静力、动力与破坏

我们旅程的第一站，是看似沉寂却无时无刻不在承受和传递力量的固体地球。

#### 地基静力学之基石

一切[岩土工程设计](@keyword=geotechnical_design|lang=zh-CN|style=Feynman)都始于一个最基本的问题：大地如何承载其自身的重量？想象一座山，或是一栋即将拔地而起的摩天大楼下的土层。在任意深度，那里的土壤或岩石所承受的压力，正是其上方所有物质重量的总和。虚功原理为我们提供了一种极其普适的方法来描述这种平衡。通过对一个无限小的土体单元应用力的平衡（强形式），或者对整个土柱考虑一个假想的（虚）位移，我们都可以推导出其内部应力的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)。

例如，在一个具有不均匀密度 $\rho(x)$ 的土柱中，[虚功原理](@keyword=principle_of_virtual_work|lang=zh-CN|style=Feynman)告诉我们，对于任何[虚位移](@keyword=virtual_displacement|lang=zh-CN|style=Feynman)场 $\delta u(x)$，由内部应力 $\sigma(x)$ 所做的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)必须等于由重力（体力）和地表荷载（面积力）所做的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)。这个积分形式的平衡陈述，即[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)，不仅完美地包含了[微分形式](@keyword=differential_forms|lang=zh-CN|style=Feynman)的平衡方程 $\frac{d\sigma}{dx} = \rho(x)g$，而且自然地将地表的荷载条件也融入其中。通过求解这个简单的方程，我们就能精确计算出从地表到地球深处任意一点的应力状态，这是设计任何安全地基的第一步 [@problem_id:3565466]。

更有趣的是，当地表没有任何外加荷载时，我们称之为“自由表面”。在有限元等数值方法的弱形式框架下，我们无需对这些边界做任何特殊处理。弱形式的边界积分项因为牵[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)为零而自然消失。这正是虚功原理的优雅之处：一个在物理上显而易见的事实——没有外力就没有外力功——在数学上得到了完美的体现。这种边界条件被称为“自然边界条件”，它与必须强制施加的位移（本质）边界条件形成了鲜明对比 [@problem_id:3563197]。

#### 运动中的地球：动力学与地震

当然，地球并非总是静止的。地震[波的传播](@keyword=wave_propagation|lang=zh-CN|style=Feynman)、爆炸的冲击、打桩的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，都要求我们把视野从静力学扩展到动力学。这看似是一个巨大的跨越，但在虚功原理的框架下，这种延伸却异常自然。我们只需将原理从“[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)”升级为“[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)率”——即功率的平衡。

此时，除了[内力](@keyword=internal_forces|lang=zh-CN|style=Feynman)[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)率和外力[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)率之外，我们还需要考虑惯性力所做的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)率。根据[牛顿第二定律](@keyword=newton_s_second_law|lang=zh-CN|style=Feynman)，质量乘以加速度等效于一个力，即达朗贝尔力。因此，在[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)率平衡中加入[惯性力](@keyword=inertial_forces|lang=zh-CN|style=Feynman)项 $\int_{\Omega}\rho \ddot{\boldsymbol{u}}\cdot\delta \boldsymbol{u}\,d\Omega$ 和描述能量耗散的阻尼力项，我们就得到了动力学问题的完整[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)。这个看似简单的补充，让我们能够模拟地震荷载下土壤的响应，评估结构的抗震性能，这对于高烈度区的城市规划和生命线工程设计至关重要 [@problem_id:3565500]。

#### 当地球破碎：界面与失效

真实的岩土体充满了各种不连续性——岩石中的节理、土壤中的层理、活动的断层。这些界面是潜在的薄弱环节，它们的滑移或开启往往是灾难的起点，比如滑坡和工程失稳。

强形式方法在处理这些尖锐的[不连续面](@keyword=surface_of_discontinuity|lang=zh-CN|style=Feynman)时会遇到数学上的困难，而[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)则再次展现了其强大的包容性。我们可以将界面的行为，例如摩擦滑移，作为一个额外的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)项加入到总的[平衡方程](@keyword=equilibrium_equations|lang=zh-CN|style=Feynman)中。考虑一个倾斜的岩层，[上层](@keyword=superstratum|lang=zh-CN|style=Feynman)岩体有沿接触面滑动的趋势。接触面上的[摩擦力](@keyword=friction_force|lang=zh-CN|style=Feynman)阻止了这种滑动。根据[库仑摩擦定律](@keyword=coulomb_friction_law|lang=zh-CN|style=Feynman)，这个[摩擦力](@keyword=friction_force|lang=zh-CN|style=Feynman)的大小不能超过一个由正应力和摩擦系数决定的阈值 $|\tau| \le \mu \sigma_n$。

当驱动力（如重力分量）小于最大[摩擦力](@keyword=friction_force|lang=zh-CN|style=Feynman)时，界面“粘滞”不动。当驱动力达到阈值时，滑移发生。这种“[粘滞](@keyword=stiction|lang=zh-CN|style=Feynman)-滑移”转换是一个典型的[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)、非光滑问题。在虚功原理的框架下，我们可以通过一个变分“不等式”来描述它：界面上[摩擦力](@keyword=friction_force|lang=zh-CN|style=Feynman)所做的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)（或耗散的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)率）被纳入总的能量平衡中，而[摩擦力](@keyword=friction_force|lang=zh-CN|style=Feynman)的演化则遵循一个[能量耗散](@keyword=energy_dissipation|lang=zh-CN|style=Feynman)最大化或与之等价的法则。这使得我们能够分析边坡的稳定性，预测潜在的滑动面，并设计加固措施 [@problem_id:3565459]。

### 多孔地球：固体与流体的相互作用

深入地下来看，土壤和岩石并非完全密实，它们是充满了孔隙的骨架，孔隙中则充满了水、油或气体。这种固-液两相介质的特性，是岩土力学区别于一般[固体力学](@keyword=solid_mechanics|lang=zh-CN|style=Feynman)的核心，也催生了更多有趣的耦合现象。

#### 饱和土地：孔隙介质力学

当外部荷载施加到饱和土体上时，荷载将由固体骨架和孔隙流体共同承担。著名的[太沙基有效应力](@keyword=terzaghi_effective_stress|lang=zh-CN|style=Feynman)原理告诉我们，土体的变形和强度主要由“有效应力”——即总应力减去[孔隙水压力](@keyword=pore_water_pressure|lang=zh-CN|style=Feynman)——所控制。虚功原理完美地拥抱了这一思想。在弱形式的陈述中，总应力 $\boldsymbol{\sigma}$ 所做的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)可以被分解为[有效应力](@keyword=effective_stress|lang=zh-CN|style=Feynman) $\boldsymbol{\sigma}'$ 所做的功和[孔隙压力](@keyword=pore_pressure|lang=zh-CN|style=Feynman) $p$ 所做的功。

具体来说，内部[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)项 $\int_{\Omega} \boldsymbol{\sigma} : \delta\boldsymbol{\epsilon} \, d\Omega$ 被写为 $\int_{\Omega} (\boldsymbol{\sigma}' - \alpha p \boldsymbol{I}) : \delta\boldsymbol{\epsilon} \, d\Omega$，其中 $\delta\boldsymbol{\epsilon}$ 是虚应变张量，$\alpha$ 是[Biot系数](@keyword=biot_coefficient|lang=zh-CN|style=Feynman)。这一分解清晰地揭示了孔隙压力 $p$ 是如何通过对固体骨架施加一个各向同性的压[力场](@keyword=force_field|lang=zh-CN|style=Feynman)来影响其力学行为的 [@problem_id:3565473]。这为所有饱和土的力学分析提供了统一的变分基础。

#### 沉降与固结

这一耦合最经典的体现是建筑物的沉降。当我们在饱和的粘土地基上修建一座建筑时，建筑物的重量会立刻传递给下方的土体，导致[孔隙水压力](@keyword=pore_water_pressure|lang=zh-CN|style=Feynman)急剧升高。由于粘土的渗透性很低，水无法立即排出，初始阶段几乎全部荷载由水承担。随着时间的推移，高压的孔隙水会缓缓地向周围低压区渗透、排出，荷载便逐渐从水转移到土骨架上，土骨架被压缩，地表随之发生沉降。这个过程被称为“固结”。

描述[孔隙水压力](@keyword=pore_water_pressure|lang=zh-CN|style=Feynman)消散的方程是一个扩散方程，与[热传导方程](@keyword=heat_transfer_equation|lang=zh-CN|style=Feynman)非常相似。我们可以对这个流体[质量守恒](@keyword=mass_conservation|lang=zh-CN|style=Feynman)方程应用同样强大的“[加权余量法](@keyword=weighted_residual_methods|lang=zh-CN|style=Feynman)”（本质上是[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)思想的推广，有时称为“[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)率平衡”），乘以一个虚压[力场](@keyword=force_field|lang=zh-CN|style=Feynman) $w(x)$ 并在全域积分，从而得到固结问题的弱形式。这个[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)与力学平衡的弱形式联立，构成了描述固结过程的完整数学模型。通过求解这个模型，工程师可以预测建筑物在未来数十年内的沉降量和沉降速率，确保其长期安全 [@problem_id:3565481]。

#### [水力压裂](@keyword=hydraulic_fracturing|lang=zh-CN|style=Feynman)：改造地下世界

固-液耦合的威力也可以被主动利用，例如在能源开采领域。[水力压裂](@keyword=hydraulic_fracturing|lang=zh-CN|style=Feynman)技术通过向深部岩层中注入高压流体，人为地制造或扩大裂缝，从而提高石油、天然气或[地热能](@keyword=geothermal_energy|lang=zh-CN|style=Feynman)的开采效率。在这个过程中，[流体压力](@keyword=pressure_in_fluids|lang=zh-CN|style=Feynman) $p$ 在裂缝表面上做的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman) $\int_{\Gamma_f}p\,\delta w\,d\Gamma_f$ （其中 $w$ 是裂缝开度）成为了驱动裂缝扩展的关键外力。

与此同时，裂缝的张开是不可逆的——一旦张开，它就不能“愈合”回比之前更小的宽度。这种不可逆性再次将我们带入了[变分不等式](@keyword=variational_inequality|lang=zh-CN|style=Feynman)的领域。我们可以引入一个拉格朗日乘子 $\lambda$ 来强制执行这个 $w \ge w^{\text{prev}}$ 的约束。整个复杂的物理过程——岩石的弹性变形、流体在裂缝中的流动、压力对裂缝面的作用，以及裂缝扩展的不可逆性——都被统一在一个耦合的弱[形式系统](@keyword=formal_systems|lang=zh-CN|style=Feynman)之中。这使得对这一复杂工程活动的精确模拟和优化成为可能 [@problem_id:3565530]。

### 耦合的宇宙：拓展应用[视界](@keyword=apparent_horizon|lang=zh-CN|style=Feynman)

虚功原理的魅力在于其惊人的延展性。一旦掌握了其核心思想——通过与一个任意的“虚场”相乘并积分来将一个[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)转化为一个积分陈述——我们就可以将其应用到其他物理学领域，并构建出描述复杂多场耦合现象的宏伟框架。

#### 热-力耦合：炽热的地球

在许多地质工程问题中，温度扮演着至关重要的角色。[地热能](@keyword=geothermal_energy|lang=zh-CN|style=Feynman)源的开发、深层核废料的处置、冻土区的工程建设，都涉及到显著的温度变化。温度变化通[过热](@keyword=superheating|lang=zh-CN|style=Feynman)胀冷缩效应影响岩土体的应力[状态和](@keyword=sum_of_states|lang=zh-CN|style=Feynman)变形。

我们可以将热力学第一定律（[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)）也写成[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)，并将其与力学平衡的[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)联立。有趣的是，一个源自[热力学势](@keyword=thermodynamic_potentials|lang=zh-CN|style=Feynman)能（如亥姆霍兹自由能或内能）的[变分原理](@keyword=variational_principles|lang=zh-CN|style=Feynman)，能够自然地导出一个对称的耦合系统。这意味着温度场对位移场的影响（通过热应力）和位移场对温度场的影响（通过应变产生的热弹效应）在数学结构上是相互关联、彼此“镜像”的。这种深刻的对称性不仅使计算更加高效，更揭示了热与力之间内在的物理联系 [@problem_id:3565449]。

#### 超越塑性：时间的流逝

许多岩土材料，特别是粘土，表现出显著的时间依赖性。它们的变形不仅取决于当前的应力，还取决于加载的历史和速率。这种行为被称为“[粘塑性](@keyword=viscoplasticity|lang=zh-CN|style=Feynman)”。例如，一个粘土边坡在恒定的重力作用下，可能会在数年甚至数十年后才发生[蠕变](@keyword=thermal_creep|lang=zh-CN|style=Feynman)破坏。

为了描述这种现象，我们需要一个能够描述塑性[应变率](@keyword=strain_rate|lang=zh-CN|style=Feynman) $\dot{\gamma}$ 的演化定律，例如[Perzyna过应力模型](@keyword=perzyna_overstress_model|lang=zh-CN|style=Feynman)。这个模型说，[塑性流动](@keyword=plastic_flow|lang=zh-CN|style=Feynman)的速率正比于当前应力超出“静态”屈服应力的那一部分。我们可以将这个流动法则也纳入变分框架。除了力学上的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)，我们还可以定义一个“虚[耗散功率](@keyword=dissipated_power|lang=zh-CN|style=Feynman)”，$\int_{\Omega}\eta \, \dot{\gamma}\, \delta\gamma \, d\Omega$，它代表了[粘性流](@keyword=viscous_flows|lang=zh-CN|style=Feynman)动耗散能量的虚变化率。将这个耗散原理与力学平衡的[虚功原理](@keyword=principle_of_virtual_work|lang=zh-CN|style=Feynman)相结合，我们就能够建立起描述材料长期蠕变和[应力松弛](@keyword=stress_relaxation|lang=zh-CN|style=Feynman)行为的完整模型 [@problem_id:3565495]。

#### 万物理论的序曲：电-化-力耦合

在细颗粒的粘土中，物理过程的复杂性达到了顶峰。粘土颗粒表面通常带有负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，会吸引孔隙水中的阳离子，形成一个被称为“[双电层](@keyword=electrical_double_layer|lang=zh-CN|style=Feynman)”的微观结构。这个结构的存在，使得粘土的行为同时受到力学、水力、化学和[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)的多重控制。

例如，在土体两端施加一个[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)，会驱动水和离子发生定向迁移，这种现象被称为“[电渗](@keyword=electro_osmosis|lang=zh-CN|style=Feynman)”和“电泳”。这个过程可以被用来加固软土地基，或者从污染的土壤中提取[重金属污染](@keyword=heavy_metal_contamination|lang=zh-CN|style=Feynman)物（动电修复）。描述这一现象需要联立求解力学平衡、[流体流动](@keyword=fluid_flow|lang=zh-CN|style=Feynman)、[离子输运](@keyword=ionic_transport|lang=zh-CN|style=Feynman)（[Nernst-Planck方程](@keyword=nernst_planck_equation|lang=zh-CN|style=Feynman)）和[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)（Poisson方程）。每一个方程都可以通过虚功原理或其广义形式（[加权余量法](@keyword=weighted_residual_methods|lang=zh-CN|style=Feynman)）转化为[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)。甚至[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)本身产生的体力（[麦克斯韦应力](@keyword=maxwell_stress|lang=zh-CN|style=Feynman)）也可以被优雅地包含在力学[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)项 $\int_{\Omega}\boldsymbol{\sigma}^{e}:\delta\boldsymbol{\epsilon}\,d\Omega$ 中。尽管问题变得异常复杂，但底层的变分思想依然是统一的，它像一条金线，将这些看似无关的物理领域[串联](@keyword=catenation|lang=zh-CN|style=Feynman)在一起 [@problem_id:3565464]。

#### 土-结构相互作用

最后，让我们回到工程实践。在岩土工程中，我们几乎总是在处理结构物（如桩基、隧道衬砌、挡土墙）与周围土体的相互作用。这两部分的力学特性和变形模式截然不同，如何将它们有效地“粘合”在一起进行分析，是一个核心挑战。

[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)为此提供了完美的舞台。我们可以用适合描述杆、板、壳的[梁单元](@keyword=beam_elements|lang=zh-CN|style=Feynman)来模拟结构，用实体单元来模拟土壤。它们各自的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)表达式可以被简单地相加。而它们之间的连接——即位移协调和力的传递——则可以通过引入拉格朗日乘子在[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)中得到精确满足。例如，一个桩和土体在接触面上必须有相同的位移，这个约束可以通过一个额外的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)项 $\int_{\Gamma_{sb}} \boldsymbol{\lambda} \cdot (\boldsymbol{u}_{\text{soil}} - \boldsymbol{u}_{\text{beam}}) \, d\Gamma$ 来施加。在这里，拉格朗日乘子 $\boldsymbol{\lambda}$ 的物理意义正是接触面上的相互作用力 [@problem_id:3565485]。

### 超越局部：通往新理论的桥梁

到目前为止，我们讨论的模型都基于一个共同的假设——“局部性”，即一点的应力只取决于该点的应变。然而，在处理材料破坏，特别是裂缝的萌生和扩展时，这个假设遇到了挑战。裂缝的尖端是一个应力[奇异点](@keyword=exceptional_points|lang=zh-CN|style=Feynman)，这给基于[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)的强形式带来了麻烦。

#### [大变形](@keyword=large_deformations|lang=zh-CN|style=Feynman)与塑性

在模拟如滑坡这样的大规模破坏时，材料会经历剧烈的变形和流动。此时，我们需要在初始的、未变形的构型上建立平衡方程，以避免网格的过度畸变。[虚功原理](@keyword=principle_of_virtual_work|lang=zh-CN|style=Feynman)可以被优雅地写在初始构型上，只需将应力（柯西应力）和应变（小应变）替换为它们在初始构型上的对应量（第二类[Piola-Kirchhoff应力](@keyword=piola_kirchhoff_stress|lang=zh-CN|style=Feynman)和[格林-拉格朗日应变](@keyword=green_lagrange_strain|lang=zh-CN|style=Feynman)）。这种“拉格朗日”描述方式是所有现代[非线性有限元](@keyword=nonlinear_finite_elements|lang=zh-CN|style=Feynman)程序的核心，它允许我们追踪材料从微小变形到完全破坏的全过程 [@problem_id:3565451]。

#### [非局部力学](@keyword=nonlocal_mechanics|lang=zh-CN|style=Feynman)与[近场动力学](@keyword=peridynamics|lang=zh-CN|style=Feynman)

为了从根本上克服裂缝奇异性的问题，近年来“非局部”理论，如[近场动力学](@keyword=peridynamics|lang=zh-CN|style=Feynman)（Peridynamics），应运而生。它的核心思想是，物质点之间的相互作用力是远距离的，作用范围在一个被称为“[视界](@keyword=apparent_horizon|lang=zh-CN|style=Feynman)”的小邻域 $\mathcal{H}_x$ 内，而不是像经典理论那样只通过直接接触。其平衡方程是一个积分方程，而非[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)。

令人惊奇的是，经典理论与这种前沿理论之间也存在一座由[虚功原理](@keyword=principle_of_virtual_work|lang=zh-CN|style=Feynman)搭建的桥梁。我们可以定义一个非局部的[虚功](@keyword=virtual_work|lang=zh-CN|style=Feynman)表达式，$\int_{\Omega}\int_{\mathcal{H}_x}f(x,\xi)\cdot\delta u(x)\,d\xi\,dx$，其中 $f(x,\xi)$ 是物[质点](@keyword=point_mass|lang=zh-CN|style=Feynman)对之间的相互作用力。可以证明，当[视界](@keyword=apparent_horizon|lang=zh-CN|style=Feynman)半径 $\varepsilon$ 趋向于零时，在满足特定数学条件（[矩条件](@keyword=moment_conditions|lang=zh-CN|style=Feynman)）下，这个非局部的积分算子将收敛于经典的应力散度（即 $E u''$）。这意味着，经典的、局部的虚功原理，可以被看作是更普适的非局部原理在[视界](@keyword=apparent_horizon|lang=zh-CN|style=Feynman)消失时的极限情况 [@problem_id:3565506]。这一发现不仅深刻地揭示了我们经典理论的适用边界，也再次证明了变分原理作为物理学“[元语言](@keyword=metalanguage|lang=zh-CN|style=Feynman)”的强大生命力。

### 结语

从一块土的自重应力，到[多物理场耦合](@keyword=multiphysics_coupling|lang=zh-CN|style=Feynman)的复杂过程，再到连接经典与前沿理论的桥梁，我们看到，虚功原理和由它导出的弱形式，远不止是一种数学技巧。它是一种思想，一种世界观。它告诉我们，自然界纷繁复杂的现象背后，可能隐藏着一个极其简单和统一的平衡法则。对于工程师和科学家而言，掌握了这把钥匙，就拥有了以一种连贯而深刻的方式去理解和描述我们所生活的这个物理世界的力量。