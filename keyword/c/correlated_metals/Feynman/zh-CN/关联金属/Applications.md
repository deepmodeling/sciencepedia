## 应用与跨学科联系

在我们之前的讨论中，我们穿越了关联金属这个奇异而美妙的世界。我们看到，当电子被挤在狭小的空间里时，那种简单、独立的电子图像是如何失效的，从而导致了新的现象：电子的质量变得巨大，另一些电子则被固定在原地形成莫特绝缘体，还有一套全新的规则支配着它们的集体之舞。

你可能会想：“这确实是个不错的理论游乐场，但这一切都是真的吗？我们能‘看到’这些‘重’电子吗？这些想法真的能帮助我们理解或制造任何东西吗？”答案是响亮的“是”。关联电子物理学并非一个孤立的好奇之物；它是一个关键的透镜，通过它我们可以理解大量真实世界的材料，也是一个强大的工具，连接着[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)和工业催化等不同领域。在本章中，我们将探讨我们如何知道这些想法是正确的，以及它们在哪些方面得到了应用。

### 实验学家的工具箱：揭开电[子群](@keyword=subgroup|lang=zh-CN|style=Feynman)体的面纱

你如何研究一群相互作用的电子？你不能只看其中一个；你必须探测它们的集体。物理学家们设计了巧妙的方法来做到这一点。他们对这些材料进行探针、光照、加热和磁化，并在系统的响应中，读出强关联的标志性特征。

#### 失踪的光之谜：为电子“称重”

想象一下用光照射一块简单的金属。自由移动的电子会在光的电场作用下[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)并重新辐射光线，这就是金属闪亮的原因。用物理学的语言来说，对极低频率光（如红外光）的响应由Drude模型描述，其强度由一个叫做[Drude权重](@keyword=drude_weight|lang=zh-CN|style=Feynman)的术语量化。对于简单金属，这个权重由电子数（$n$）和它们的普通质量决定。

现在，让我们在关联金属上做同样的实验。一件奇妙的事情发生了：相当一部分的[Drude权重](@keyword=drude_weight|lang=zh-CN|style=Feynman)*不见了*！材料在低频下的响应比你预期的要弱。那部分[谱权重](@keyword=spectral_weight|lang=zh-CN|style=Feynman)——那部分“光”——到哪里去了？守恒定律要求一个答案。事实证明，丢失的权重被转移到了更高的频率，通常在红外中段。这种高频吸收对应于将两个电子强行置于同一个原子上所需的巨大能量代价——即Hubbard $U$能量。我们实际上看到了[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)的影子，即对应于我们所谓的下[Hubbard带](@keyword=hubbard_bands|lang=zh-CN|style=Feynman)和上[Hubbard带](@keyword=hubbard_bands|lang=zh-CN|style=Feynman)之间跃迁的“非相干”激发 [@problem_id:2982968]。

这一现象为我们提供了一个强大的工具。*保留*在低频的[Drude权重](@keyword=drude_weight|lang=zh-CN|style=Feynman)部分，是[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)[留数](@keyword=residue|lang=zh-CN|style=Feynman)$Z$的直接量度，它量化了我们的重[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)中还剩下多少“类电子”的特性。此外，通过仔细地在一定频率范围内对[光电导](@keyword=photoconductivity|lang=zh-CN|style=Feynman)进行积分，我们可以利用一个称为*[f-求和规则](@keyword=f_sum_rule|lang=zh-CN|style=Feynman)*的基本关系，直接测量[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)$m^*$。这是我们能够“称量”一个电子，并确认它已经比其裸质量[重数](@keyword=multiplicity|lang=zh-CN|style=Feynman)百倍的最直接方法之一 [@problem_id:2825420]。这些基础的光学实验如此优美地揭示了[质量重整化](@keyword=mass_renormalization|lang=zh-CN|style=Feynman)和[谱权重转移](@keyword=spectral_weight_transfer|lang=zh-CN|style=Feynman)等核心理论概念，这是对整个图像的惊人证实。

#### [费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)不变的心跳

这是凝聚态物理学中最深刻、最美丽的真理之一。当你将金属置于强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中时，电子的能量被量子化成称为[朗道能级](@keyword=landau_levels|lang=zh-CN|style=Feynman)的离散能级。当你改变[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)时，这些能级会逐一穿过[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)，引起各种物理性质（如磁化强度）的微小、周期性[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。这种量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，被称为de Haas-van Alphen (dHvA) 效应，就像金属[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)有节奏的心跳。

这个心跳的频率与费米面的[截面](@keyword=cross_section_2|lang=zh-CN|style=Feynman)积成正比。现在，考虑一个强关联金属。相互作用很激烈，电子又重又迟缓，它们的行为极其复杂。你肯定会[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)费米面的形状和大小会发生剧烈改变，dHvA频率也随之改变。

但事实并非如此。在一个被称为**[Luttinger定理](@keyword=luttinger_s_theorem|lang=zh-CN|style=Feynman)**的深刻原理保护下的一个里程碑式结果中，[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)包围的体积是一个[不变量](@keyword=invariant|lang=zh-CN|style=Feynman)，它仅由系统中的电子数量决定，并且完全独立于它们相互作用的强度。相互作用可以极大地[重整化](@keyword=renormalization|lang=zh-CN|style=Feynman)[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)质量，这会减弱dHvA[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的*振幅*，但它们不能改变其*频率* [@problem_id:2812607]。这是一个类似拓扑的陈述：无论你如何搅动和推挤人群，房间里的人总数是固定的。在一个质量增强千倍的材料中通过dHvA[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)看到“正确”的[费米面体积](@keyword=fermi_surface_volume|lang=zh-CN|style=Feynman)，是Landau的[费米液体理论](@keyword=fermi_liquid_theory|lang=zh-CN|style=Feynman)即使在强相互作用极限下也成立的最深刻的验证之一。它还给了我们一个利器：当一种材料的量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)给出的频率与[电子计数](@keyword=electron_counting|lang=zh-CN|style=Feynman)*不*匹配时，我们就知道有更奇异的事情正在发生，比如电子分裂成了几个部分 [@problem_id:2812607]。

#### 迟滞性的热学与磁学指纹

再想想我们的重[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。它们移动缓慢，并且在能量上紧密地堆积在费米能级附近。这对金属的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)性质有着直接的影响。[电子比热](@keyword=electronic_specific_heat|lang=zh-CN|style=Feynman)——将电子气温度提高一度所需的能量——与[费米能级处的态密度](@keyword=density_of_states_at_the_fermi_level|lang=zh-CN|style=Feynman)成正比。由于大的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)$m^*$意味着大的[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)，关联金属表现出惊人的巨大[电子比热](@keyword=electronic_specific_heat|lang=zh-CN|style=Feynman)，通常比简单金属大数百倍。这是一个“重费米子”金属的经典标志，可以在低温实验室中检测到 [@problem_id:117993]。

磁化率也发生了类似的事情。泡利磁化率衡量的是电子自旋与外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)对齐的难易程度，它也与态密度成正比。在关联金属中，这种磁化率也被极大地增强了。当系统被调控得更接近[莫特相变](@keyword=mott_transition|lang=zh-CN|style=Feynman)时，[有效质量发散](@keyword=effective_mass_divergence|lang=zh-CN|style=Feynman)，[磁化率](@keyword=susceptibility|lang=zh-CN|style=Feynman)也随之发散，预示着向磁有序态的不稳定性 [@problem_id:174263]。这些热学和磁学测量为这些材料中存在一种新型电子态提供了最早的线索。

#### 用[X射线](@keyword=x_ray|lang=zh-CN|style=Feynman)进行原子解剖

到目前为止，我们讨论的探针——光学、dHvA、比热——测量的都是电子流体的集体、巡游性质。但如果我们想检验Hubbard模型的核心假设：电子是局域在单个原子上并感受到强烈的在位排斥力，该怎么办？为此，我们需要一个能够对单个原子进行“解剖”的工具。

高能[X射线](@keyword=x_ray|lang=zh-CN|style=Feynman)是实现这一点的完美工具。在[X射线光电子能谱](@keyword=x_ray_photoelectron_spectroscopy|lang=zh-CN|style=Feynman)（XPS）中，我们用足够能量的[X射线](@keyword=x_ray|lang=zh-CN|style=Feynman)将一个来自原子深层、紧密束缚的芯能级的电子打出。在原子核中突然产生的这个正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，会在价层的$d$或$f$电子中引起“摇动效应”。在简单金属中，这种响应会是一个单一、宽泛的特征。但在莫特绝缘体中，价电子处于明确的、类似原子的构型中。系统可以弛豫到几种不同的末态构型，每种构型都有不同的能量。结果，射出电子的[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)显示出一系列尖锐的“多重峰”。这种复杂的结构是原子局域化、量子力学状态的直接指纹，由在位排斥$U$和洪特耦合$J_H$所支配。这是最终的证实，即在深层次上，莫特绝缘体的行为更像是一组孤立的原子，而不是传统的固体 [@problem_id:3006179] [@problem_id:3006218]。

### 物理实验室之外：工作中的关联电子

关联电子物理学的思想并非局限于黑板或低温实验室。它们已成为[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)、化学及其他领域设计和理解技术不可或缺的工具。

#### 驯服代码：物理学家为化学家难题提供的解决方案

几十年来，[计算材料科学](@keyword=computational_materials_science|lang=zh-CN|style=Feynman)家和化学家面临着一个重大危机。他们从第一性原理模拟材料的主要工具——密度泛函理论（DFT）——对于像硅这样的简单材料取得了巨大成功。但对于一大类重要的[过渡金属氧化物](@keyword=transition_metal_oxides|lang=zh-CN|style=Feynman)——也就是我们现在认识到的关联材料——DFT却灾难性地失败了。它会预测作为透明绝缘体的氧化镍（NiO）应该是一种金属。

问题在于近似[DFT泛函](@keyword=dft_functionals|lang=zh-CN|style=Feynman)中一个隐蔽的“自相互作用误差”，它人为地偏爱电子铺展开来（[离域](@keyword=delocalization|lang=zh-CN|style=Feynman)化），而实际上它们应该是局域的。解决方案并非来自计算界，而是直接来自关联电子的凝聚态物理学。研究人员提出了一个绝妙的修正方案：在标准的DFT计算中增加一个有针对性的“惩罚”项，即一个Hubbard $U$，它只作用于局域的$d$轨道。这个DFT$+U$方法明确地惩罚非物理的[分数占据](@keyword=fractional_occupancy|lang=zh-CN|style=Feynman)，并迫使[电子局域化](@keyword=electron_localization|lang=zh-CN|style=Feynman)，从而正确地打开一个[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。这种直接从[多体理论](@keyword=many_body_theory|lang=zh-CN|style=Feynman)引入计算框架的方法，现在已经成为一个标准的、不可或缺的工具，每天被成千上万的研究人员用来设计从电池阴极到磁性材料和[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)的各种物质 [@problem_id:2460150]。

#### 炼金术士的秘密：预测化学反应性

现代科学的一大挑战是设计出完美的[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)——一种能够加速特定[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)的材料，例如，将有害的$\text{CO}_2$转化为有用的燃料。金属表面上的[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)是成键和断键的精巧舞蹈。[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)对反应物分子的“粘性”至关重要：如果太弱，分子不会结合；如果太强，它们会卡住而无法反应。

寻找“金发姑娘”[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)似乎是炼金术士的追求，一个反复试错的过程。但是，同样，一个来自固体物理学的深刻概念提供了关键。Jens Nørskov和他的同事们表明，许多分子在过渡金属表面上的结合能与一个单一、简单的参数——金属$d$电子态的能量加权平均值，即所谓的**$d$带中心**——有着极好的相关性。这个单一的数字，我们的理论告诉我们如何计算甚至调控它，决定了[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的强度。当$d$带中心向[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)移动时，与吸附物轨道的杂化增强，使得表面“更粘” [@problem_id:2472152]。这个框架彻底改变了催化领域，将其从一门玄学转变为一门预测科学，使我们能够在踏入实验室之前，就计算筛选成千上万种潜在的合金，以找到最佳[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)。

#### 前沿：[奇异金属](@keyword=strange_metals|lang=zh-CN|style=Feynman)、[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)与一场“拔河比赛”

关联金属的故事远未结束。事实上，它直接将我们引向了科学界一些最重大的未解之谜的门前，比如高温超导。许多展现这种奇异现象的材料，如[铜氧化物](@keyword=cuprates|lang=zh-CN|style=Feynman)和铁基氮族化物，都是掺杂的莫特绝缘体。它们的“正常”态，即超导出现前的状态，不是简单金属，而是一种“[奇异金属](@keyword=strange_metals|lang=zh-CN|style=Feynman)”，一种挑战我们[费米液体](@keyword=fermi_liquid|lang=zh-CN|style=Feynman)描述的状态。

理解这些材料需要超越我们最简单的模型。真实材料有多个$d$轨道，而迫使不同轨道中[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)对齐的洪特耦合$J_H$扮演着主角。例如，在许多[铁基超导体](@keyword=iron_based_superconductors|lang=zh-CN|style=Feynman)中，$U$和强$J_H$的结合导致了一种迷人的状态，称为“[洪特金属](@keyword=hund_s_metals|lang=zh-CN|style=Feynman)”。这是一种奇异的物质状态，它既是高度关联的，具有巨大的[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)，又保持金属性，强烈抵抗局域化的趋势。这种表现出精神分裂般特性的状态，即一些[电子局域化](@keyword=electron_localization|lang=zh-CN|style=Feynman)而另一些电子巡游（一种轨道选择性莫特相），现在被认为是这些材料中[高温超导](@keyword=high_temperature_superconductivity|lang=zh-CN|style=Feynman)诞生的母体 [@problem_id:3006218]。

最后，这种冲突与竞争的主题在[重费米子材料](@keyword=heavy_fermion_materials|lang=zh-CN|style=Feynman)中得到了完美的体现。在这些系统中，巨大的[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)天真地暗示着根据简单的[Stoner判据](@keyword=stoner_criterion|lang=zh-CN|style=Feynman)，它们都应该是铁磁体。然而，大多数都不是。它们陷入了一场巨大的斗争。一方面，[RKKY相互作用](@keyword=rkky_interaction|lang=zh-CN|style=Feynman)试图使局域磁矩发生磁性有序。另一方面，近藤效应试图完全淬灭这些磁矩，将它们吸收到一个集体的、非磁性的重[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)海洋中。材料的命运——无论是成为顺磁体、反铁磁体，还是甚至是[非常规超导体](@keyword=unconventional_superconductors|lang=zh-CN|style=Feynman)——都悬于这场拔河比赛的微妙平衡之中 [@problem_id:2997299]。正是在这些临界空间，在各种[竞争有序](@keyword=competing_orders|lang=zh-CN|style=Feynman)的[引爆点](@keyword=tipping_points|lang=zh-CN|style=Feynman)上，大自然常常揭示其最深刻、最美丽的秘密。

从解释实验数据到指导新技术的设计，关联电子物理学已成为现代科学版图中不可或缺的一部分，证明了基本思想照亮复杂世界的强大力量。