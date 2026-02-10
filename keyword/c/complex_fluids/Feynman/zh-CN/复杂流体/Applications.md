## 应用与跨学科联系

在了解了区分复杂流体丰富世界与其简单[牛顿流体](@keyword=newtonian_fluids|lang=zh-CN|style=Feynman)同类的基本原理之后，我们可能会倾向于将剪切变稀、[粘弹性](@keyword=viscoelasticity|lang=zh-CN|style=Feynman)、屈服应力等概念视为优雅但或许深奥的奇观。事实远非如此。实际上，我们被这些非凡的材料所包围，并由它们构成。它们独特的行为并非不便的复杂性；它们正是自然界和工程师们巧妙利用以使生命成为可能、技术得以运转的特性。现在，让我们漫步于这片引人入胜的景象之中，看看我们学到的原理是如何成为理解从我们心脏的跳动到驱动我们世界的科技创造等一系列现象的关键。

### 生命的机器：我们的身体即复杂流体

自然是最初的流变学大师。早在任何物理学家写下粘度方程之前，进化就已经在为优化功能而调整[生物流](@keyword=biological_flows|lang=zh-CN|style=Feynman)体的流动特性。我们自己的身体就是一个活生生的复杂流体动力学博物馆。

思考一下生命的河流：我们的血液。它不是像水一样的简单流体。它是由可变形[红细胞](@keyword=red_blood_cells|lang=zh-CN|style=Feynman)组成的稠密悬浮液，这赋予了它一种被称为剪切变稀的奇妙特性。在我们主动脉这些宽阔、快速流动的高速公路上，剪切速率很高。[红细胞变形](@keyword=red_blood_cell_deformation|lang=zh-CN|style=Feynman)并与流动方向对齐，就像顺着急流漂流的木头，血液的[有效粘度](@keyword=effective_viscosity|lang=zh-CN|style=Feynman)下降，使其能够出人意料地轻松流动。但在我们毛细血管那些狭窄、缓慢移动的小巷里，剪切速率很低，红细胞可以形成称为“叠连体”的瞬时堆叠结构。这赋予血液更高的[有效粘度](@keyword=effective_viscosity|lang=zh-CN|style=Feynman)，有助于调节压力和与周围组织的交换。这种剪切变稀的特性是自然工程的杰作，确保了在大尺度上的高效运输和在小尺度上的有效功能。要真正捕捉这一点，我们不仅要考虑粘度，还要考虑流体的内部“记忆”——这些[微观结构形成](@keyword=microstructure_formation|lang=zh-CN|style=Feynman)或破裂所需的时间。这可以通过一个结构松弛时间 $\lambda$ 来量化。通过将这个时间与流动的时间尺度进行比较，使用一个称为[德博拉数](@keyword=deborah_number|lang=zh-CN|style=Feynman)的[无量纲群](@keyword=dimensionless_groups|lang=zh-CN|style=Feynman)，我们可以预测血液会更像简单液体还是结构化的复杂液体[@problem_id:4160498]。

结构与流动之间的这种舞蹈并不仅限于我们的[循环系统](@keyword=circulatory_system|lang=zh-CN|style=Feynman)。它对于我们如何进食至关重要。对于有[吞咽困难](@keyword=dysphagia|lang=zh-CN|style=Feynman)（一种称为 dysphagia 的病症）的患者来说，像水这样的稀薄液体可能很危险。它们流动得太快，可能在吞咽的保护性反射启动前进入气道。解决方案是什么？我们求助于复杂流体科学。通过添加特殊的增稠剂，我们将简单的液体转变为剪切变稀的流体。当增稠液体含在口中时，它处于非常低的剪切状态，因此粘度很高。它表现得很“稠”，作为一个有[内聚力](@keyword=cohesive_forces|lang=zh-CN|style=Feynman)的食团保持在一起，并抵抗过早[溢出](@keyword=overflow|lang=zh-CN|style=Feynman)。但在吞咽时强大、高剪切的作用下，其粘度急剧下降。它在需要时变得“稀”，使其能够轻松、安全地通过咽部。这种双重特性——静止时稠，运动时稀——正是为那些肌肉控制减弱或延迟的人使吞咽更安全、更高效所需要的[@problem_id:4785825]。

复杂流体的影响甚至延伸到生命的最初阶段。精子细胞到卵母细胞的旅程并非在简单的水中游泳，而是在宫颈粘液中进行的一次英勇航行，这是一种经典的[粘弹性流体](@keyword=viscoelastic_fluids|lang=zh-CN|style=Feynman)。这种由[生物聚合物](@keyword=biopolymers|lang=zh-CN|style=Feynman)组成的复杂网络，既表现出剪切变稀的特性，也表现出弹性特性。精子尾部的摆动产生高的局部剪切速率，这使其紧邻区域的粘液“变稀”，开辟出一条阻力较低的路径。与此同时，流体的弹性——其储存和释放能量的能力——与游泳运动相互作用。根据[鞭毛](@keyword=flagella|lang=zh-CN|style=Feynman)摆动的具体情况，这种弹性响应既可能阻碍推进，也可能在某些情况下甚至有助于推进。理解游泳者运动与流体复杂响应之间这种错综复杂的相互作用，对于理解生育能力和设计仿生微型机器人至关重要。为了正确地对此建模，我们需要复杂的[本构定律](@keyword=constitutive_laws|lang=zh-CN|style=Feynman)，如 [Giesekus 模型](@keyword=giesekus_model|lang=zh-CN|style=Feynman)，它既能捕捉剪切变稀的粘度，也能捕捉在更简单的模型中不存在的弹性法向应力[@problem_id:2660070]。

最后，我们用复杂流体来治愈自己。当你使用药用眼药水时，你通常依赖[流变学](@keyword=rheology|lang=zh-CN|style=Feynman)来确保药物起作用。简单的、像水一样的溶液会在眨眼和引流的瞬间被清除出眼睛。为了克服这一点，许多现代眼科制剂是凝胶、乳液或悬浮液。例如，凝胶具有高粘度，能显著减缓其从眼球表面的清除速度，增加“[停留时间](@keyword=sojourn_time|lang=zh-CN|style=Feynman)”，让药物有更多时间被吸收。许多凝胶也是剪切变稀的，因此虽然它们在眨眼之间能保持原位，但眨眼本身的高剪切作用使它们能舒适地铺开，而不会感觉过于粘稠。乳液和软膏提供了一个半固体或油性相，作为[亲脂性药物](@keyword=lipophilic_drugs|lang=zh-CN|style=Feynman)的储库，随时间缓慢释放它们。在所有这些情况下，我们都是有意地从简单流体转向复杂流体，以控制输运并提高[生物利用度](@keyword=bioavailability|lang=zh-CN|style=Feynman)，这是物理化学在药理学中的一个优美应用[@problem_id:4729951]。

### 用“智能”胶状物进行工程设计

自然界通过进化发现的，工程师们通过才智学会了。控制复杂流体的流动是无数工业过程的核心。

以制造驱动我们手机和汽车的[锂离子电池](@keyword=lithium_ion_batteries|lang=zh-CN|style=Feynman)为例。一个关键步骤是将一层薄而均匀的“电极浆料”涂覆到金属箔上。这种浆料是一种复杂流体——一种由活性颗粒、[导电添加剂](@keyword=conductive_additive|lang=zh-CN|style=Feynman)和粘合剂组成的稠密悬浮液。其[流变学](@keyword=rheology|lang=zh-CN|style=Feynman)是非牛顿行为的交响曲。它具有**[屈服应力](@keyword=yield_stress|lang=zh-CN|style=Feynman)**，意味着在施加一定的最小力之前它不会流动；这对于稳定性极好，因为它能防止涂层下垂或破裂成细流。它是**剪切变稀**的，因此可以在高处理速度下轻松泵送和铺展。而且它通常是**触[变性](@keyword=denaturation|lang=zh-CN|style=Feynman)**的，意味着其粘度取决于剪切历史；它在加工时变稀，但静置时会恢复其结构。此外，它还可能是**粘弹性**的，储存的弹性能量如果管理不当，可能在浆料离开涂覆设备时引起诸如拉丝或出口溶胀等缺陷。成功制造电池关键取决于调整这些流变特性[@problem_id:3927870]。

流变学在[热能工程](@keyword=thermal_engineering|lang=zh-CN|style=Feynman)中的影响同样深远。想象一下，你需要通过加热的管道泵送一种[非牛顿流体](@keyword=non_newtonian_fluid|lang=zh-CN|style=Feynman)——比如聚合物熔体或像番茄酱这样的食品——来对其进行加热或冷却。[牛顿流体](@keyword=newtonian_fluids|lang=zh-CN|style=Feynman)会形成抛物线形的速度分布。但剪切变稀的流体则会形成一个更平钝、更像“栓流”的剖面，因为在剪切最高的地方（靠近管壁）粘度更低。这种改变了的速度剖面完全改变了传热的游戏规则。由于流体核心部分移动得更均匀，且速度梯度集中在管壁附近，热量沿管道平流输送和从管壁扩散进来的方式都不同了。为牛顿流体开发的标准工程[传热关联式](@keyword=heat_transfer_correlations|lang=zh-CN|style=Feynman)完全失效。为了正确设计[换热器](@keyword=heat_exchanger|lang=zh-CN|style=Feynman)，工程师必须考虑流体的幂律指数或其他流变参数，这些参数决定了[速度剖面](@keyword=velocity_profile|lang=zh-CN|style=Feynman)的形状，并因此决定了热发展长度[@problem_id:2530618] [@problem_id:2494521]。

这种重写规则的必要性也延伸到了更大尺度的流动中。许多关键过程涉及复杂流体在[多孔介质](@keyword=porous_media|lang=zh-CN|style=Feynman)中的流动——想想使用聚合物溶液进行强化采油、污染物在土壤中的扩散、过滤浆料，甚至是生物流体在组织中的流动。描述多孔介质中缓慢流动的经典法则是[达西定律](@keyword=darcy_s_law|lang=zh-CN|style=Feynman)（Darcy's Law），该定律指出流速与压力梯度成正比。但该定律建立在牛顿流体粘度恒定的假设之上。当将剪切变稀的[聚合物溶液](@keyword=polymer_solutions|lang=zh-CN|style=Feynman)注入油藏时，其[有效粘度](@keyword=effective_viscosity|lang=zh-CN|style=Feynman)取决于它被强制通过曲折孔隙空间的速度。岩石的简单渗透率不再是一个常数；它变成了一个取决于流速的表观渗透率。为了对此进行建模，经典的 Darcy 和 [Brinkman 方程](@keyword=brinkman_equation|lang=zh-CN|style=Feynman)必须被推广，纳入一个依赖于剪切速率的粘度。这使我们能够预测如何使用这些“智能”流体更有效地从多孔岩石中驱替石油，这是一个具有巨大经济和技术重要性的问题[@problem_id:4088041]。

### 数字孪生：模拟复杂性

在现代世界中，我们常常寻求使用计算机模拟来理解和设计系统。但我们如何教计算机理解复杂流体的奇妙特性呢？这一挑战推动了计算科学的边界。

如果你想模拟剪切变稀流体在表面上的流动——例如，涂有非牛顿除冰液的飞机机翼——你不能使用与空气或水相同的假设。流体的粘度不是恒定的。在表面附近，即边界层的高剪切区域，粘度将远低于远离表面的地方。这会产生深远的影响：对于剪切变稀的流体，边界层更薄，壁面[速度梯度](@keyword=velocity_gradient|lang=zh-CN|style=Feynman)比[牛顿流体](@keyword=newtonian_fluids|lang=zh-CN|style=Feynman)的情况更陡峭。为了使[计算流体动力学](@keyword=computational_fluid_dynamics|lang=zh-CN|style=Feynman)（CFD）模拟准确，其网格——即求解方程的点阵——必须在壁面附近更密集，以捕捉这些陡峭的梯度。相反，对于[剪切增稠](@keyword=shear_thickening_2|lang=zh-CN|style=Feynman)的流体，边界层会更厚，较粗的网格可能就足够了。如果在模拟的设计阶段就没有考虑到流体的[流变性](@keyword=fluxionality|lang=zh-CN|style=Feynman)，就会导致对诸如阻力和传热等关键量的错误预测[@problem_id:3938588]。

最终的挑战在于模拟[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)。水中的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)已经是[经典物理学](@keyword=classical_physics|lang=zh-CN|style=Feynman)的一大未解难题。但复杂流体中的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)则是另一回事。流体的内部微观结构——聚合物链、悬浮颗粒——直接与[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)涡旋相互作用。在许多剪切变稀的流体中，长链聚合物可以伸展并像微小的橡皮筋一样作用，从而显著抑制小尺度涡旋并减少[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)阻力。这是一个具有重大实际意义的现象，但它意味着我们标准的湍流模型，如 $k-\varepsilon$ 模型，必须被修改。模型参数不能再是普适常数，而必须成为局部流体[流变学](@keyword=rheology|lang=zh-CN|style=Feynman)的函数，以解释变化的[表观粘度](@keyword=apparent_viscosity|lang=zh-CN|style=Feynman)及其对[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)能量产生和耗散的影响[@problem_id:3384774]。

### 统一的视角

从我们血管中的生命之血到我们技术的制造和世界的模拟，复杂流体的印记无处不在。乍一看，这些应用可能似乎毫无关联——医生治疗病人，工程师设计电池，物理学家模拟[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)。然而，在表面之下，它们都由相同的基本原理所统一。它们都是关于微观结构与宏观流动、记忆与耗散、材料在受力时的响应方式的故事。进入复杂流体世界的旅程，是一次深入塑造我们世界的材料核心的旅程，它提醒我们物理学在解释我们周围看似迥异的现象时所具有的美丽而统一的力量。