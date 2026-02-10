## 应用与跨学科联系

在遍历了支配[湍流模拟](@keyword=turbulent_flow_modeling|lang=zh-CN|style=Feynman)世界的原理和机制之后，我们可能会感到某种满足。我们已经建立了一个强大的思想工具箱：能量从大涡到小涡的串级之舞，雷诺平均纳维-斯托克斯（RANS）、[大涡模拟（LES）](@keyword=large_eddy_simulation_(les)|lang=zh-CN|style=Feynman)和[直接数值模拟](@keyword=direct_numerical_simulation|lang=zh-CN|style=Feynman)（DNS）的不同理念，以及将它们联系在一起的基本方程。但这一切是为了什么？所有这些错综复杂的理论机器的意义何在？

答案，以及这门学科真正的美，不在于工具本身，而在于它们让我们能够看到和建造什么。[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)研究不是物理学家和数学家自娱自乐的游戏；它是一个普适的镜头，通过它我们可以理解世界，从我们呼吸的空气到我们看到的星星。它是一座桥梁，连接着最实际的工程挑战和最深奥的天体物理学问题。现在，让我们走过这座桥，探索它所揭示的一些景象。

### 从有序到混沌：三维的诞生

在很长一段时间里，我们对某些流体流动的印象是出人意料的有序和优雅。考虑水流过一个圆柱体。在恰当的速度下，圆柱体后的尾流会组织成一种惊人规则的漩涡图案，从顶部和底部交替脱落。这条“[卡门涡街](@keyword=kármán_vortex_street|lang=zh-CN|style=Feynman)”是[流体力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)的教科书范例，一种完美的周期性、二维华尔兹[@problem_id:3319554]。它很美，可以预测，对于一个局限于平面的世界来说，这就是全部的故事。

但我们的世界不是一个平面。如果我们把速度再提高一点会发生什么？一个真实的三维模拟揭示了一个戏剧性的转变。在二维图像中如此整齐的完美平行的涡辊，开始沿着它们的长度出现波纹和起伏。它们变得不稳定。流动虽然仍由主要的[涡脱](@keyword=vortex_shedding|lang=zh-CN|style=Feynman)落主导，但现在其上叠加了丰富的三维结构[@problem_id:2438883]。这种[二次不稳定性](@keyword=secondary_instability|lang=zh-CN|style=Feynman)打破了完美的展向相干性；作用在圆柱体上的力变得不那么规则。简单的华尔兹变成了一场复杂得多的混沌之舞。这不是模拟的失败；而是它最大的成功。它告诉我们，超过某一点，第三个维度不是一个可选项——它是必不可少的。自然坚持如此。从二维的幻想过渡到三维的现实，是为什么三维[湍流模拟](@keyword=turbulent_flow_modeling|lang=zh-CN|style=Feynman)不仅是一个工具，而且是必需品的第一个也是最根本的原因。

### 现实的代价

如果我们追求的是三维现实，就必须准备好付出代价。在模拟世界里，这个代价就是计算成本。想象一下进行一次[直接数值模拟](@keyword=direct_numerical_simulation|lang=zh-CN|style=Feynman)（DNS），我们解析每一个[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)运动，从最大的漩涡到能量最终耗散为热量的最小一缕。对于一个简单的三维盒子中的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)，捕捉所有尺度所需的网格点数随[雷诺数](@keyword=reynolds_number|lang=zh-CN|style=Feynman) $Re$ 爆炸性增长，其[标度关系](@keyword=scaling_relationships|lang=zh-CN|style=Feynman)大约为 $Re^{9/4}$。

这不仅仅是一个稍大的数字。一个假设的相同设置的二维模拟，遵循不同的物理串级，其网格点数仅以 $Re^1$ 增长。运行三维模拟与二维模拟相比的计算工作量——即总计算次数——其标度关系达到了惊人的 $Re^{3/2}$ [@problem_id:3340076]。对于一个中等高的[雷诺数](@keyword=reynolds_number|lang=zh-CN|style=Feynman) $10^4$，这意味着三维模拟的工作量是二维模拟的*一百万倍*！这一个严酷的[标度律](@keyword=scaling_laws|lang=zh-CN|style=Feynman)是[湍流模拟](@keyword=turbulent_flow_modeling|lang=zh-CN|style=Feynman)的守门人。它告诉我们，虽然DNS是最终的真理，但这是一个我们只能在相对简单的流动和低雷诺数下才能负担得起的真理。正是这种巨大的成本催生了整个模型体系，迫使我们发明了LES和RANS的巧妙折衷方案。

### 改造世界：驯服[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)之风

大多数工程问题——设计汽车、飞机或洁净空气城市——都发生在雷诺数远高于DNS所能及的范围。在这里，我们必须务实，运用我们的物理直觉，为正确的工作选择正确的工具。

考虑一辆乘用车的外空气动力学。流经车顶或引擎盖等长而光滑表面的流动相对规整。但是，围绕侧视镜、构成挡风玻璃框架的A柱，尤其是在车辆后方复杂的尾流中，流动是分离、再循环和三维[涡流](@keyword=vortex_flow|lang=zh-CN|style=Feynman)的混沌混合体。要在有限的计算预算下模拟这一切，不可能处处都解析靠近壁面的薄黏性子层。工程解决方案是一种“分区”方法：在行为良好、附着的流动区域使用计算成本低的“[壁面函数](@keyword=wall_functions|lang=zh-CN|style=Feynman)”，但在流动分离并产生阻力的关键区域，投入宝贵的网格点来完全解析[边界层](@keyword=boundary_layer|lang=zh-CN|style=Feynman)或使用增强模型[@problem_id:3390696]。这是由对底层物理的深刻理解所指导的折衷艺术。

对于像飞机着陆时的多段[翼型](@keyword=aerofoil|lang=zh-CN|style=Feynman)这样的东西，挑战被极大地放大了。这里的目标是产生最大[升力](@keyword=lift_force|lang=zh-CN|style=Feynman)，这是通过迫使空气通过主翼、前缘缝翼和后缘襟翼之间的狭窄间隙来实现的。从这些间隙流出的流动形成高度不稳定的剪切层，它们迅速转变为[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)，并理想地重新附着到下一个翼面上。捕捉这一物理过程——分离、转捩和再附着——对于预测[失速](@keyword=stall|lang=zh-CN|style=Feynman)和确保安全至关重要。这是一个简单的[RANS模型](@keyword=rans_models|lang=zh-CN|style=Feynman)常常失败的任务。最先进的解决方案是[混合RANS-LES](@keyword=hybrid_rans_les|lang=zh-CN|style=Feynman)方法，例如延迟分离涡模拟（DDES）。这种聪明的方法让模拟在附着[边界层](@keyword=boundary_layer|lang=zh-CN|style=Feynman)内以高效的RANS模式运行，但在关键物理现象发生的分离剪切层中，它会自动切换到更昂贵、能解析[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的LES模式[@problem_id:3331485]。这相当于一个外科医生只在精确的关注区域使用高倍显微镜。

[湍流模拟](@keyword=turbulent_flow_modeling|lang=zh-CN|style=Feynman)的影响超越了机器，延伸到我们的生活环境。想象一种污染物从一个密集城市的街道层面源头释放出来。风流经这些“城市峡谷”时是高度[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的。虽然[时间平均](@keyword=time_averaging|lang=zh-CN|style=Feynman)的[RANS模型](@keyword=rans_models|lang=zh-CN|style=Feynman)可能给出平均浓度的合理图像，但它完全忽略了[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)中最危险的方面：间歇性的大尺度涡，它们可以卷起大量污染物，并以集中的“团块”形式将其输送到行人的呼吸高度。预测这些高浓度事件的概率对于健康和安全评估至关重要。只有像LES这样能够明确捕捉这些驱动输运的大尺度非定常运动的时间解析方法，才能提供这一重要信息[@problem_id:2447849]。

### 自然之怒与宇宙画布

帮助我们设计更安静的汽车或更安全城市的相同原理，也让我们能够理解自然的巨大力量和宇宙的宏大动力学。

粉[雪崩](@keyword=avalanches|lang=zh-CN|style=Feynman)是一幅可怕的景象——一股由雪和空气组成的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)重力流从山坡上雷鸣般地冲下。其破坏力由其前部的大型、相干的滚动[叶状结构](@keyword=foliation|lang=zh-CN|style=Feynman)承载。[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman)的RANS模拟，由于其本质，会平均掉这些非定常结构，给出一个看起来平滑、温和的前缘，掩盖了现实。然而，LES模拟可以捕捉到这些致命的大尺度涡的诞生和演变，为灾害提供一个更忠实的画面[@problem_id:2447864]。在这里，三维模拟是理解并可能减轻自然灾害的工具。

将我们的目光从地球上移开，我们发现在最宏伟的画布上，[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)正在挥毫泼墨。像我们的太阳这样的恒星是巨大的[湍流对流](@keyword=turbulent_convection|lang=zh-CN|style=Feynman)等离子体球。虽然我们无法期望用DNS级别的保真度模拟整个恒星，但我们可以对[恒星对流](@keyword=stellar_convection|lang=zh-CN|style=Feynman)区内的一个小的等离子体“盒子”进行高度详细的三维模拟。从这样的模拟中，我们可以计算出[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的平均特性，例如“[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)压力”——由剧烈的[流体运动](@keyword=fluid_motion|lang=zh-CN|style=Feynman)提供的对抗[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)的额外支撑。然后，这个[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)压力可以作为一个更符合物理的项被纳入更简单的、一维的整个恒星模型中，从而更好地预测其结构、演化和寿命[@problem_id:349297]。这是一个[多尺度建模](@keyword=multiscale_modeling|lang=zh-CN|style=Feynman)的绝佳例子，我们最详细的模拟为我们最广阔的理论提供了信息。

宇宙不仅是[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的，而且常常是超音速的。在恒星之间广阔、寒冷的气体和尘埃云中，新恒星在此诞生，[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)将物质聚集在一起，而[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)则将其推开。这种由超新星爆炸和[恒星风](@keyword=stellar_winds|lang=zh-CN|style=Feynman)驱动的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)是高度可压缩和超音速的。在这里，我们熟悉的不可压缩流的柯尔莫哥洛夫[能量串级](@keyword=energy_cascade|lang=zh-CN|style=Feynman)，及其著名的 $E(k) \propto k^{-5/3}$ [能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)，让位给了另一种现实。流动由一张激波网主导。这些作为急剧间断的激波，从根本上改变了[能量串级](@keyword=energy_cascade|lang=zh-CN|style=Feynman)，导致了更陡峭的速度谱，接近 $E(k) \propto k^{-2}$。[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)基本“规则”的这种变化意味着，为地球上工程流动开发的[亚格子尺度模型](@keyword=sub_grid_scale_models|lang=zh-CN|style=Feynman)必须为宇宙中可压缩、激波主导的环境进行彻底的重新思考和调整[@problem_id:3537267]。

最后，我们转向人类最伟大的科学探索之一：驾驭核聚变的力量。在[托卡马克](@keyword=tokamaks|lang=zh-CN|style=Feynman)（tokamak）——一种设计用于约束比太阳核心更热的等离子体的甜甜圈形装置中，[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)是头号大敌。它无情地将热量从中心输送到边缘，就像在磁瓶上戳了个洞。理解和控制这种[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)至关重要。这不再是我们熟悉的水或空气的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)；它是一个令人眼花缭乱的等离子体微不稳定性动物园，有着诸如[离子温度](@keyword=ion_temperature|lang=zh-CN|style=Feynman)梯度（ITG）模和[捕获电子模](@keyword=trapped_electron_modes|lang=zh-CN|style=Feynman)（TEM）之类的名字，所有这些都在由梯度、碰撞和[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)几何结构决定的复杂舞蹈中相互作用。专门的模拟框架，如[回旋动理学](@keyword=gyrokinetics|lang=zh-CN|style=Feynman)，是我们解开这种多尺度混沌的主要工具，其中微小的、快速移动的电子尺度涡可以影响更大、更慢的离子尺度[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)[@problem_id:3701661]。在这里，三维模拟不仅仅是为了理解世界本来的样子；它是在我们构建未来世界的探索中不可或缺的指南。

从一个浸水的圆柱体到一颗恒星的心脏，从一辆汽车的尾流到一个聚变反应堆的核心，问题在本质上总是相同的：那壮丽、复杂而永无止境的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)之舞。通过模拟，我们终于学会了它的舞步。