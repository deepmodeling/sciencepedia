## 应用与跨学科联系

在掌握了雷诺平均的数学核心之后，我们可能会倾向于将其视为一种巧妙但抽象的技巧。事实远非如此。这种将世界分为平均值和脉动值的简单行为，是所有科学和工程领域中最强大、最实用的工具之一。它使我们能够对极其复杂的系统提出合理的问题，并惊人地得到合理的答案。关键在于理解我们正在问的是哪种问题。

思考一下天气和气候的区别。“下周二下午3点巴黎会下雨吗？”这是一个天气问题。它要求了解大气的瞬时、混沌状态。“巴黎七月份的平均降雨量是多少？”这是一个气候问题。它要求的是一个长期的统计平均值，一个由地理、季节和大规模大气模式决定的系统稳定属性，而不是每一朵云在特定时刻的确切位置。

雷诺平均是我们用来研究[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)“气候”而非其“天气”的工具 [@problem_id:2447873]。雷诺平均纳维-斯托克斯（RANS）模拟为我们提供了[平均速度](@keyword=average_velocity|lang=zh-CN|style=Feynman)、平均压力、平均温度——也就是气候。它不会，也不能告诉我们每个小涡旋和[涡流](@keyword=vortex_flow|lang=zh-CN|style=Feynman)的确切、短暂状态。这是一个至关重要的区别。例如，如果我们想预测喷气发动机产生的噪音，我们问的是一个“天气”问题。声音由快速、时变的压力脉动承载。[RANS模型](@keyword=rans_models|lang=zh-CN|style=Feynman)正是对这些脉动进行平均，因此对这种宽带噪音是“充耳不闻”的。要“听到”它，我们需要其他工具，比如能够捕捉[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)天气的尺度解析模拟，或者使用RANS气候统计数据来推断可能产生的声音的复杂声学比拟方法 [@problem_id:3357774]。

但是，对于大量至关重要的问题，气候正是我们需要知道的。正是在这里，雷诺平均成为了工程师和科学家最信赖的伙伴。

### 工程师的工具箱：驯服[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)

想象一下，你正在设计一个飞机机翼、一辆赛车或风力涡轮机的叶片。你主要关心的不是每个微小涡旋在某个微秒的位置。你需要知道平均[升力](@keyword=lift_force|lang=zh-CN|style=Feynman)、平均阻力、结构上的[平均应力](@keyword=mean_stress|lang=zh-CN|style=Feynman)。你需要的是气候。

当我们对[纳维-斯托克斯方程](@keyword=navier_stokes_equations|lang=zh-CN|style=Feynman)进行雷诺平均时，一个奇妙的简化发生了：混沌的时间依赖性消失了。但它留下了一个幽灵：[雷诺应力张量](@keyword=reynolds_stress_tensor|lang=zh-CN|style=Feynman)，$-\rho\overline{u_i'u_j'}$。这一项告诉我们平均流受到[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的影响。它代表了由混沌脉动引起的动量净输运。对于三维流动，这个幽灵在我们的方程中引入了六个新的未知量，造成了著名的“封闭问题” [@problem_id:3392595]。我们的未知数多于方程数！

这就是[湍流建模](@keyword=turbulence_modeling|lang=zh-CN|style=Feynman)真正艺术的开始。整个领域都是一项创造性的工作，旨在通过寻找一种合理的方式，用已知的平均量来表达未知的[雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)，从而“封闭”方程。最简单也是最早期的思想之一是[混合长度模型](@keyword=mixing_length_model|lang=zh-CN|style=Feynman)，该模型提出[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)粘度$\nu_t$可以与局部[平均速度](@keyword=average_velocity|lang=zh-CN|style=Feynman)梯度相关联。在一个零方程模型中，我们可以提出一个类似$\nu_t = l_m^2 \sqrt{2 S_{ij} S_{ij}}$的关系式，其中$S_{ij}$是平均[应变率张量](@keyword=strain_rate_tensor_2|lang=zh-CN|style=Feynman)，$l_m$是我们根据几何形状（例如，距墙的距离）设定的一个“[混合长度](@keyword=mixing_length|lang=zh-CN|style=Feynman)”。突然之间，未知的应力就通过我们正在求解的平均速度以代数形式表达出来，[方程组](@keyword=simultaneous_equations|lang=zh-CN|style=Feynman)也就封闭了 [@problem_id:3392595]。诚然，这是一种近似，但却是一种非常有效的方法，为首次对[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)进行实际计算打开了大门。

当然，我们可以做得更好。真正的威力来自于更复杂的“[两方程模型](@keyword=two_equation_models|lang=zh-CN|style=Feynman)”，如著名的$k-\epsilon$和$k-\omega$模型。这些模型不只是猜测[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)粘度；它们求解两个额外的[输运方程](@keyword=transport_equations|lang=zh-CN|style=Feynman)来描述[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)自身的属性——通常是[湍动能](@keyword=turbulent_kinetic_energy|lang=zh-CN|style=Feynman)$k = \frac{1}{2}\overline{u_i'u_i'}$，以及一个代表[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)长度或时间尺度的变量，如其[耗散率](@keyword=dissipation_rate|lang=zh-CN|style=Feynman)$\epsilon$或比[耗散率](@keyword=dissipation_rate|lang=zh-CN|style=Feynman)$\omega$。例如，在标准的$k-\omega$模型中，[涡粘度](@keyword=eddy_viscosity|lang=zh-CN|style=Feynman)不再是预先设定的，而是通过关系式$\mu_t = \rho \frac{k}{\omega}$，由求解得到的场量$k$和$\omega$计算得出 [@problem_id:3382340]。这些模型是现代[计算流体力学](@keyword=computational_hydrodynamics|lang=zh-CN|style=Feynman)（CFD）的主力，每天都被用来设计从心脏瓣膜到[高超声速飞行](@keyword=hypersonic_flight|lang=zh-CN|style=Feynman)器的各种事物。

### 伟大的比拟：输运的统一性

雷诺平均框架最美妙的结果之一，或许是它揭示了自然界深刻的统一性。事实证明，[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)是一个不加选择的混合器。它不仅混合动量；它混合流体携带的任何东西——热量、化学物质、污染物、灰尘。而且其混合方式惊人地相似。

让我们将雷诺平均应用于热量[输运方程](@keyword=transport_equations|lang=zh-CN|style=Feynman)（能量方程）。正如我们发现了源于速度脉动相关性$\overline{u_i'u_j'}$的雷诺应力项一样，我们现在也发现了一个“[湍流热通量](@keyword=turbulent_heat_flux|lang=zh-CN|style=Feynman)”项$\overline{u_j'T'}$，它源于速度脉动和温度脉动$T'$之间的相关性 [@problem_id:2506722]。这一项代表了由翻腾的[涡流](@keyword=vortex_flow|lang=zh-CN|style=Feynman)引起的额外热量输运。

我们可以使用与处理[雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)完全相同的逻辑来模拟这个新项。我们提出一个[梯度扩散假说](@keyword=gradient_diffusion_hypothesis|lang=zh-CN|style=Feynman)：[湍流热通量](@keyword=turbulent_heat_flux|lang=zh-CN|style=Feynman)与平均温度的梯度成正比，即$\overline{u_j'T'} = -\alpha_t \frac{\partial \bar{T}}{\partial x_j}$，其中$\alpha_t$是[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)[热扩散率](@keyword=thermal_diffusivity|lang=zh-CN|style=Feynman)。[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)粘度与该[热扩散率](@keyword=thermal_diffusivity|lang=zh-CN|style=Feynman)之比是一个[无量纲数](@keyword=dimensionless_numbers|lang=zh-CN|style=Feynman)，称为[湍流普朗特数](@keyword=turbulent_prandtl_number|lang=zh-CN|style=Feynman)，$Pr_t = \nu_t / \alpha_t$。

现在，让我们对化学物质的输运（如空气中的污染物或海洋中的盐分）再做一次同样的操作。我们对物质浓度方程进行雷诺平均。一个新的项出现了：“[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)质量通量”$\overline{u_j'c'}$，其中$c'$是浓度的脉动。我们再次以同样的方式对其建模：$\overline{u_j'c'} = -D_t \frac{\partial \bar{C}}{\partial x_j}$，其中$D_t$是[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)[质量扩散](@keyword=mass_diffusion|lang=zh-CN|style=Feynman)率 [@problem_id:2484153]。我们再次构建一个无量纲比值，即[湍流施密特数](@keyword=turbulent_schmidt_number|lang=zh-CN|style=Feynman)，$Sc_t = \nu_t / D_t$。

你看到这个模式了吗？[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)中的动量、热量和[质量输运](@keyword=mass_transport|lang=zh-CN|style=Feynman)的物理过程都由相同的数学结构描述。这就是著名的雷诺比拟的核心。实验发现，对于许多流动， $Pr_t$ 和 $Sc_t$ 都接近于1。这意味着$\nu_t \approx \alpha_t \approx D_t$。换言之，[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)在混合动量、热量和质量方面的效率大致相同。这一深刻的洞见使我们能够仅仅通过了解[流体摩擦](@keyword=fluid_friction|lang=zh-CN|style=Feynman)，就能预测复杂系统中的[热量和质量传递](@keyword=heat_and_mass_transfer|lang=zh-CN|style=Feynman)速率——从冷却核反应堆到理解[生物反应器](@keyword=bioreactors|lang=zh-CN|style=Feynman)中营养物质的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)！

### 超越现有领域：调整平均方法

雷诺平均的哲学——分离已解析和未解析的尺度，并模拟后者的影响——是如此强大，以至于它已被改编用于分析科学中一些最复杂的系统。

#### 可压缩流与多[相混合](@keyword=phase_mixing|lang=zh-CN|style=Feynman)物

当流动速度非常高，接近或超过声速时，流体的密度不能再被视为常数。为了防止一连串令人困惑的新相关项出现在我们的方程中，我们可以使用一种略有不同的平均程序，称为[Favre平均](@keyword=favre_averaging|lang=zh-CN|style=Feynman)或质量加权平均 [@problem_id:629908]。这个巧妙的选择使最终的平均流方程看起来简洁而熟悉。然而，新的物理现象确实会出现。在高速流动中，像“压力-膨胀项”（描述[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)运动与内能之间的能量交换）和“膨胀耗散项”（湍[动能耗散](@keyword=kinetic_energy_dissipation|lang=zh-CN|style=Feynman)的额外途径）等项变得重要。这些效应是[可压缩性](@keyword=compressibility|lang=zh-CN|style=Feynman)的直接后果，必须被添加到我们的模型中，才能准确预测航空航天工程中的[超音速射流](@keyword=supersonic_jet|lang=zh-CN|style=Feynman)、激波和其他现象 [@problem_id:3382029]。

同样的应用精神也适用于包含多于一个相的流动，例如河流中的泥沙、空气中的雨滴或工业混合器中的粉末。通过[对流](@keyword=convection|lang=zh-CN|style=Feynman)体和颗粒之间的力应用雷诺平均，一个引人入胜的新项出现了：“[湍流弥散](@keyword=turbulent_dispersion|lang=zh-CN|style=Feynman)力”。该力源于颗粒浓度脉动与[流体速度](@keyword=fluid_velocity|lang=zh-CN|style=Feynman)脉动之间的相关性。它有一个清晰的物理意义：[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)倾向于将颗粒散开，将它们从平均浓度高的区域推向平均浓度低的区域。对这种力进行建模对于预测侵蚀、河流中的泥沙输运以及许多化学工程过程的效率至关重要 [@problem_id:570488]。

#### 宇宙涡流：[模拟宇宙](@keyword=simulating_the_universe|lang=zh-CN|style=Feynman)

雷诺平均哲学威力的最终证明来自一个与管道和飞机相去甚远的领域：[计算天体物理学](@keyword=computational_astrophysics|lang=zh-CN|style=Feynman)。在模拟整个星系的形成时，即使是最强大的超级计算机也无法解析每一颗恒星、每一片气体云，或[超大质量黑洞](@keyword=supermassive_black_holes|lang=zh-CN|style=Feynman)周围的微小区域。这些关键过程是“亚网格”的；它们比模拟能处理的最小体积还要小。

解决方案是什么？天体物理学家的做法与Osborne Reynolds完全相同。他们将已解析的模拟变量视为“平均流”，将所有未解析的物理过程视为“脉动”。然后，他们创建“[亚网格模型](@keyword=subgrid_models|lang=zh-CN|style=Feynman)”来表示这些未解析过程对星系尺度动力学的平均效应。例如，一个用于恒星形成的[亚网格模型](@keyword=subgrid_models|lang=zh-CN|style=Feynman)可能会在模拟单元格中已解析的气体密度超过某个阈值时，将气体转化为恒星粒子。一个用于[活动星系核](@keyword=active_galactic_nuclei|lang=zh-CN|style=Feynman)（AGN）反馈的[亚网格模型](@keyword=subgrid_models|lang=zh-CN|style=Feynman)可能会根据一个未解析的中心[黑洞吸积](@keyword=black_hole_accretion|lang=zh-CN|style=Feynman)模型，向周围[气体注入](@keyword=gas_puffing|lang=zh-CN|style=Feynman)一定量的热能。

这些[亚网格模型](@keyword=subgrid_models|lang=zh-CN|style=Feynman)本质上是雷诺平均的封闭项。它们是基于物理动机的[参数化](@keyword=parametrization|lang=zh-CN|style=Feynman)方法，用以描述未解析尺度对已解析尺度的影响 [@problem_id:3537578]。这是一个惊人的发现：用来计算船只阻力的智力框架，同样被用来模拟整个宇宙的演化。

### 了解平均值的力量与局限

雷诺平均为我们提供了[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)系统的“气候”。这种统计观点非常强大，使我们能够构建现代世界，并模拟像宇宙一样浩瀚的系统。通过牺牲混沌的“天气”，我们获得了一门关于平均值的、易于处理和具有预测性的科学。这证明了这样一个思想：即使在最复杂、最混沌的系统中，也常常存在简单、优雅且极其有用的潜在规律。Reynolds的天才之处在于给了我们看透它们的透镜。