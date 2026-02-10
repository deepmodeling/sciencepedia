## 应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系

我们花了一些时间来探索支配[复杂流体](@keyword=complex_fluids|lang=zh-CN|style=Feynman)流动的那些奇特而美妙的规则。你可能会留下的印象是，这些仅仅是实验室里的奇闻异事，有趣但与水、空气和简单机器的“真实”世界脱节。事实远非如此。在本章中，我们将踏上一段旅程，去看看这些[非线性流变学](@keyword=nonlinear_rheology|lang=zh-CN|style=Feynman)的原理并非例外，而是常态。它们是隐藏的建筑师，塑造着从我们身体的功能到我们星球冰盖宏伟而缓慢的舞蹈等各种现象。我们将发现一种惊人的统一性，看到同样的基本思想在工程师的工作室、生物学家的显微镜和地球物理学家的全[球模型](@keyword=spherical_model|lang=zh-CN|style=Feynman)中发挥作用。

### 工程一个“顽固”的世界

让我们从一些熟悉的事物开始。为什么油漆能粘在刷子上，却又能平滑地涂抹在墙上？为什么你必须拍打番茄酱瓶的底部才能让它流出来？答案是一种叫做**[屈服应力](@keyword=yield_stress|lang=zh-CN|style=Feynman)**的特性：这些材料在被足够用力推动之前表现得像固体，然后像液体一样流动。这种“顽固”不是需要克服的麻烦；而是一种需要被设计的特性。

考虑一下移动大量颗粒状物料的挑战——筒仓中的谷物、水泥粉或药片。如果这些物料像水一样，它们会毫不费力地从料斗中流出。但它们不会。它们会发生堵塞，在出口上方形成一个稳定的“拱”，阻止所有流动。通过将致密的颗粒状物料建模为**宾汉流体**——最简单的[屈服应力流体](@keyword=yield_stress_fluids|lang=zh-CN|style=Feynman)模型——工程师可以精确预测这种情况何时会发生。物料在中心形成一个类似固体的“[栓塞](@keyword=embolism|lang=zh-CN|style=Feynman)”，在外围屈服的、类似液体的层中滑动。只有当壁面处的重力应力大于物料的[屈服应力](@keyword=yield_stress|lang=zh-CN|style=Feynman) $\tau_y$ 时，才会发生流动。如果 $\tau_y \ge \rho g H$（其中 $H$ 是出口的一个特征尺寸），物料将形成一个稳定的拱，并拒绝流动，无论上面堆积了多少物料 [@problem_id:2381301]。理解这一点为工程师提供了设计不堵塞的料斗和筒仓的工具。

这种顽固性也会随着流动速率而改变。许多[复杂流体](@keyword=complex_fluids|lang=zh-CN|style=Feynman)，特别是那些含有长链聚合物或细胞悬浮液的流体，是**[剪切稀化](@keyword=shear_thinning|lang=zh-CN|style=Feynman)**的：你搅拌得越用力，它们就变得越稀（粘性越小）。这在生物技术中是一把双刃剑。想象一下你在运行一个大型发酵罐，以培养一种能生产抗生素的[丝状真菌](@keyword=filamentous_fungi|lang=zh-CN|style=Feynman)。随着真菌的生长，发酵液变成一种浓稠的[剪切稀化](@keyword=shear_thinning|lang=zh-CN|style=Feynman)悬浮液。当你试图用叶轮搅拌它时，会产生一个既有趣又有问题的情况。在高速旋转的叶轮叶片旁边，剪切速率很高，所以[表观粘度](@keyword=apparent_viscosity|lang=zh-CN|style=Feynman)很低。这会形成一个充分混合、类似水的流体“空穴”。但仅在不远处，剪切速率下降，[表观粘度](@keyword=apparent_viscosity|lang=zh-CN|style=Feynman)急剧上升。罐中其余部分变成了一个几乎停滞、高度粘稠的物质团，与空穴的物质交换非常缓慢。

这会带来灾难性的后果。全局[混合时间](@keyword=mixing_time|lang=zh-CN|style=Feynman) $\theta_m$ 急剧增加，因为营养物质需要很长时间才能到达停滞区的细胞。此外，吹入罐中的氧气被困住了。叶轮可能很擅长在其空穴内将气泡打成细雾，但这些气泡无法分散到粘稠、停滞的主体中。它们会聚集并直接穿过液面逸出，使大多数细胞缺氧。结果，与简单的牛顿流体相比，整体混合效率和至关重要的氧[传质系数](@keyword=mass_transfer_coefficient|lang=zh-CN|style=Feynman) $k_La$ 都急剧下降 [@problem_id:2501995]。你所[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的生长本身，却造成了进一步生长的流变学障碍——这是生物过程工程师面临的深刻挑战。

### 身体作为一种[复杂流体](@keyword=complex_fluids|lang=zh-CN|style=Feynman)

我们不必在工业大桶中寻找复杂的流体；我们自己就充满了它们。血液、粘液和滑液都是流变工程的杰作，经过数十亿年的进化精细调整。

血液远不止是带红色的水。它是一种可变形细胞的浓悬浮液，其流动特性对其功能至关重要。在动脉中高速流动时，[红细胞](@keyword=red_blood_cells|lang=zh-CN|style=Feynman)飞速前进，血液的行为或多或少像一种简单的牛顿流体。但在[微循环](@keyword=microcirculation|lang=zh-CN|style=Feynman)中流速较慢的部分，特别是在收集细胞返回心脏的毛细血管后微静脉中，情况变得有趣起来。在这些低剪切速率下，红细胞开始聚集在一起，形成聚合体，从而极大地增加了血液的[表观粘度](@keyword=apparent_viscosity|lang=zh-CN|style=Feynman)。血液是一种[剪切稀化流体](@keyword=shear_thinning_fluids|lang=zh-CN|style=Feynman)，并且据信也具有微小的屈服应力。

这具有深远的生理学后果。[循环系统](@keyword=circulatory_system|lang=zh-CN|style=Feynman)是一系列串联的阻力器，而娇嫩的毛细血管——所有氧气和营养物质交换发生的地方——内的压力由下游（微静脉，$R_v$）与上游（微动脉，$R_a$）的阻力之比决定。由于在低剪切的微静脉中，[表观粘度](@keyword=apparent_viscosity|lang=zh-CN|style=Feynman)及因此的阻力不成比例地增加，导致 $R_v/R_a$ 比值上升。根据[斯塔林方程](@keyword=starling_equation|lang=zh-CN|style=Feynman)，这会使毛细血管中的压力*升高*，将更多液体推入周围组织。因此，血液的非牛顿性质是调节我们体内液体平衡的直接因素 [@problem_id:2583416]。这种复杂性也带来了挑战：推断血管壁内皮细胞感受到的真实[剪切应力](@keyword=shear_stress|lang=zh-CN|style=Feynman)——这是血管健康的关键信号——并不直接。基于抛物线[速度剖面](@keyword=velocity_profile|lang=zh-CN|style=Feynman)或整体[粘度测量](@keyword=viscosity_measurement|lang=zh-CN|style=Feynman)的简单公式可能会产生误导，因为在壁面附近会形成无细胞血浆层，并且在低剪切速率下会出现平钝的、类似栓塞的流动剖面 [@problem_id:2583416]。

或许生物流变学中最优雅的例子之一是在[受精机制](@keyword=fertilization_mechanism|lang=zh-CN|style=Feynman)中找到的。宫颈粘液不是被动介质；它是一个主动的过滤器，一个旨在筛选出最具活力的精子的质量控制检查站。其特性完美地展示了[屈服应力](@keyword=yield_stress|lang=zh-CN|style=Feynman)和**粘弹性**——既像液体又像固体的能力。粘液是由[粘蛋白](@keyword=mucin|lang=zh-CN|style=Feynman)聚合物构成的网络。要通过，精子必须满足两个条件。首先，其游动必须产生足够的推进[剪切应力](@keyword=shear_stress|lang=zh-CN|style=Feynman) $\tau$，以局部破坏[聚合物网络](@keyword=polymer_networks|lang=zh-CN|style=Feynman)，即必须超过粘液的有效屈服应力 $\tau_y$。其次，精子鞭毛的摆动必须足够快，以超越聚合物链的弹性回缩。这由魏森伯格数 $Wi = \lambda \dot{\gamma}$ 来量化，其中 $\lambda$ 是流体的松弛时间，$\dot{\gamma}$ 是精子产生的剪切速率。如果 $Wi$ 远小于1，精子基本上是在糖浆中游泳；如果 $Wi$ 大于1，流体没有时间松弛，精子可以创造一个短暂的、类似液体的通道游过去。

这创造了一个双重考验。一个低活力的精子，产生低的剪切速率，在这两方面都失败了：其推进应力太弱，无法克服 $\tau_y$，其低摆动频率使其 $Wi$ 值低，这意味着它会被[弹性网络](@keyword=elastic_net|lang=zh-CN|style=Feynman)困住。然而，一个高动力的精子会产生高剪切速率。这使其能够超过[屈服应力](@keyword=yield_stress|lang=zh-CN|style=Feynman)*并*达到高魏森伯格数，导致粘液局部发生[剪切稀化](@keyword=shear_thinning|lang=zh-CN|style=Feynman)和屈服。粘液有效地在强大的游泳者面前“融化”，为其通过创造了一条低阻力的走廊 [@problem_id:2646467]。这是用[流变学](@keyword=rheology|lang=zh-CN|style=Feynman)语言书写的自然选择。

### 当事情升温时：反馈与不稳定性

流变学与其他物理学（如[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)和[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)）的相互作用可以导致更复杂和有趣的现象，包括[反馈回路](@keyword=feedback_loop|lang=zh-CN|style=Feynman)和不稳定性。

想象一下剪切一种非常粘稠的流体，比如挤出机中的[聚合物熔体](@keyword=polymer_melts|lang=zh-CN|style=Feynman)。你为使其流动所做的功会以热量的形式耗散，提高流体的温度。但对于大多数这类流体，粘度对温度高度敏感——稍微加热就可能导致粘度大幅下降。这创造了一个[反馈回路](@keyword=feedback_loop|lang=zh-CN|style=Feynman)：流动产生热量，热量降低粘度，较低的粘度可能会改变流动，从而改变热量的产生。这种耦合可能导致一种称为**多重[稳态](@keyword=steady_state_2|lang=zh-CN|style=Feynman)**的现象。对于完全相同的边界条件（例如，[库埃特流](@keyword=couette_flow|lang=zh-CN|style=Feynman)中移动板的速度），系统可以存在于几个不同稳定状态中的一个：一个“冷”的、高应力状态，或一个“热”的、低应力状态，其粘度要低得多。一个关键的无量纲数，它结合了粘度的温度敏感性（$\beta$）、[粘性耗散](@keyword=viscous_dissipation|lang=zh-CN|style=Feynman)和[热传导](@keyword=conduction_heat_transfer|lang=zh-CN|style=Feynman)，决定了这种[多重性](@keyword=multiplicity|lang=zh-CN|style=Feynman)是否可能。对于该参数的大值，系统的响应曲线呈S形，允许单个输入对应三种可能的解 [@problem_id:2494606]。这不仅仅是一个数学上的奇特现象；它对于工业[聚合物加工](@keyword=polymer_processing|lang=zh-CN|style=Feynman)至关重要，因为意外跳跃到“热失控”状态可能会毁坏产品或损坏设备。

[非线性流变学](@keyword=nonlinear_rheology|lang=zh-CN|style=Feynman)也改变了不稳定性的本质。在简单的牛顿流体世界中，不稳定性通常表现为一个明确的阈值——在某个临界值处，开关会翻转。考虑显示器中的[液晶](@keyword=liquid_crystals|lang=zh-CN|style=Feynman)，通过施加电压可以使其形成[对流](@keyword=convection|lang=zh-CN|style=Feynman)卷（威廉姆斯畴）。对于牛顿[液晶](@keyword=liquid_crystals|lang=zh-CN|style=Feynman)，这发生在非常特定的阈值电压 $V_{th}$。但如果[液晶](@keyword=liquid_crystals|lang=zh-CN|style=Feynman)表现为非牛顿[幂律流体](@keyword=power_law_fluid|lang=zh-CN|style=Feynman)，其中应力与剪切速率的关系为 $\tau \propto \dot{\gamma}^n$，阈值的性质就变了。不再有一个单一的[临界电压](@keyword=critical_voltage|lang=zh-CN|style=Feynman)。相反，触发不稳定性所需的电压变得依赖于初始不可避免的缺陷或涨落的大小。阈值变得“模糊”，遵循类似 $V_{th}^2 \propto \theta_0^{n-1}$ 的关系，其中 $\theta_0$ 是初始扰动的振幅 [@problem_id:84881]。简单的开/关开关被一个渐变的调光器所取代，这是非线性材料响应的直接后果。

当我们考虑[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)——终极的[流体不稳定性](@keyword=instability_in_fluids|lang=zh-CN|style=Feynman)时，这种复杂性进一步加深。用于预测[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)的[计算流体力学](@keyword=computational_fluid_dynamics|lang=zh-CN|style=Feynman)（CFD）模型，是为空气和水等流体开发的，对于非牛顿流体必须从根本上重新思考。当对控制方程进行平均时，流变学的非线性在*平均[粘性应力](@keyword=viscous_stress|lang=zh-CN|style=Feynman)*本身引入了新的、未封闭的相关项——这在牛顿流体中根本不存在 [@problem_id:2447850]。这也改变了物质被[湍流输运](@keyword=turbulent_transport|lang=zh-CN|style=Feynman)的方式。[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)的[动量输运](@keyword=momentum_transport|lang=zh-CN|style=Feynman)效率（[涡粘性](@keyword=eddy_viscosity|lang=zh-CN|style=Feynman)）和热输运效率（涡[热扩散率](@keyword=thermal_diffusivity|lang=zh-CN|style=Feynman)）不再以相同的方式耦合。对于[剪切稀化流体](@keyword=shear_thinning_fluids|lang=zh-CN|style=Feynman)，[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)增强了，但[动量输运](@keyword=momentum_transport|lang=zh-CN|style=Feynman)比[被动标量](@keyword=passive_scalar|lang=zh-CN|style=Feynman)的[热输运](@keyword=heat_transport|lang=zh-CN|style=Feynman)增强得更强。这意味着它们的比值，即[湍流普朗特数](@keyword=turbulent_prandtl_number|lang=zh-CN|style=Feynman) $Pr_t$，会随着流体的[流变性](@keyword=fluxionality|lang=zh-CN|style=Feynman)而改变 [@problem_id:2494591]。正确处理这一点对于准确模拟和设计无数工业过程至关重要。

### 行星尺度：冰的缓慢舞蹈

最后，让我们放大视野，看看[非线性流变学](@keyword=nonlinear_rheology|lang=zh-CN|style=Feynman)在行星尺度上的作用。冰川可能看起来是固体，但在长时标上，它是一种流体——一种非常缓慢、非常粘稠的非牛顿流体。冰川和冰盖的运动，是我们气候系统的一个关键组成部分，受其流变学支配。

冰川学中的一个关键问题是：冰川如何在其基岩上滑动？冰川的底部并不光滑；它是一个充满凸起和凹陷的地貌。冰通过两种相互竞争的机制越过这些障碍。对于小凸起，上游侧巨大的压力降低了冰的熔点，使其融化。水流绕过凸起到达低压的下游侧，并在那里重新冻结。这个过程称为**重融**（regelation）。对于大凸起，这个受传热限制的过程太慢了。相反，障碍物周围的高[应力集中](@keyword=stress_concentration|lang=zh-CN|style=Feynman)导致冰变形并[蠕变](@keyword=creep|lang=zh-CN|style=Feynman)过去，遵循一个非线性的[粘性流](@keyword=viscous_flows|lang=zh-CN|style=Feynman)动定律（格伦流动定律）。

Weertman 滑动定律的卓越洞见在于，冰川会自行调整以适应“控制性障碍物尺寸”——即提供*最大*阻力的基岩粗糙度的特定波长。这是因为重融对于小凸起（短波长）最有效，而蠕变对于大凸起（长波长）最有效。在这两者之间，存在一个最难克服的波长。这个最大阻力波长决定了总摩擦力，并且在给定冰川自重驱动应力的情况下，决定了总滑动速度 $u_b$ [@problem_id:458547]。这是一个[自然系统](@keyword=systema_naturae|lang=zh-CN|style=Feynman)在相互竞争的过程中寻找平衡的优美例子，而这个平衡完全由冰和水的材料属性所介导。

### 结论

我们的旅程已经完成。我们看到了同样的基本思想——[屈服应力](@keyword=yield_stress|lang=zh-CN|style=Feynman)、[剪切稀化](@keyword=shear_thinning|lang=zh-CN|style=Feynman)、[粘弹性](@keyword=viscoelasticity|lang=zh-CN|style=Feynman)和非线性[蠕变](@keyword=creep|lang=zh-CN|style=Feynman)——出现在各种惊人多样的背景中。从搅拌真菌悬浮液的棘手问题到我们组织中微妙的液体平衡，从游泳精子的生物物理考验到冰川的宏伟滑动，[非线性流变学](@keyword=nonlinear_rheology|lang=zh-CN|style=Feynman)的原理提供了一种统一的语言来描述世界上复杂材料如何响应力。它有力地提醒我们，在自然界中，复杂性不是缺陷，而是一种设计原则。通过理解它，我们不仅成为更好的工程师和科学家，而且对我们所栖居的这个错综复杂、相互关联的世界有了更深的欣赏。