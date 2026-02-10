## 应用与跨学科联系

在我们之前的讨论中，我们遇到了量子力学中最微妙和深刻的思想之一：阿哈罗诺夫-玻姆效应。我们了解到，一个电子，或任何带电粒子，其[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)可以被一个它从未接触过的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)所改变。粒子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)“感受”到矢量势 $\mathbf{A}$，即使在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $\mathbf{B} = \nabla \times \mathbf{A}$ 为零的区域。这或许看似一个哲学上的奇谈，一个供人琢磨的巧妙悖论。但自然界很少如此含蓄。一个如此基本的原理绝非只是派对上的小把戏；它是一把钥匙，能解开一系列广泛的现象，是一根线索，将看似迥异的科学领域编织在一起。

在本章中，我们将踏上一段旅程，去看看这把钥匙适合哪里。我们将看到阿哈罗诺夫-玻姆效应如何成为物理学家实验室中的实用工具，成为窥探材料量子世界的“显微镜”。然后，我们将拓宽视野，发现这种效应并非[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)所独有，而是一个普适概念——几何相位——的优美范例，它出现在晶[体力](@keyword=body_forces|lang=zh-CN|style=Feynman)学乃至拓扑材料的奇异世界中。最后，我们将目光投向宇宙本身，探问阿哈罗诺夫-玻姆效应就力的基本性质以及[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身的结构，教给了我们什么。

### 作为介观探针的 AB 效应

让我们首先深入到微观世界，进入“介观”物理学的领域。这个领域探索的是那些尺寸如此之小，以至于介于大块材料的经典世界和单个原子的量子世界之间的器件。在这些微观电路中，量子相干性至关重要，而阿哈罗诺夫-玻姆效应是其最强大的工具之一。

#### 量子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)计

[阿哈罗诺夫-玻姆相](@keyword=aharonov_bohm_phase|lang=zh-CN|style=Feynman)移 $\Delta\phi$ 与粒子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $q$ 及所环绕的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi$ 成正比：$\Delta\phi = q\Phi/\hbar$。这个简单的关系带来一个惊人的结果：如果我们能测量已知磁通量下的[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)，我们就能精确地确定粒子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)！阿哈罗诺夫-玻姆效应就是一个量子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)计。

这不仅仅是一个思想实验。当[超导理论](@keyword=superconductivity_theory|lang=zh-CN|style=Feynman)首次被提出时，它预测导致电阻完全消失的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载体不是单个电子，而是它们的束缚对，称为“库珀对”，带有 $-2e$ 的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。如何才能证明这一点呢？阿哈罗诺夫-玻姆效应提供了答案。通过制造一个微小的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)，并在其中心穿过[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)，物理学家观察到，环的量子特性以一个磁通量周期重复，而这个周期恰好是单个电子预期周期的一半。这就是确凿的证据：要获得相同的[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)量为两倍的粒子只需要一半的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) [@problem_id:1789075]。量子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)计读出了“-2e”，为该理论提供了惊人的证实。

故事变得更加奇特。在[分数量子霍尔效应](@keyword=fractional_quantum_hall_effect|lang=zh-CN|style=Feynman)的奇异领域，二维电子气在巨大[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)下可以凝聚成一种新的[量子流体](@keyword=quantum_fluids|lang=zh-CN|style=Feynman)。这种流体中的激发——即携带电流的“[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)”——被预测具有[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)的电子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，例如 $e/3$ 或 $e/5$。分数电荷的想法似乎与我们所知的一切都背道而驰。然而，阿哈罗诺夫-玻姆干涉测量法再次伸出援手。与库珀对测量类似的实验发现了[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)，表明这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)确实是分数的 [@problem_id:1141649]。AB 效应让我们能够直接见证这些奇异的[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)粒子的出现，它们既非[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)也非[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)，而是另一种全新的东西：任意子。

#### 倾听金属的量子私语

那么普通金属呢？如果我们用像金或铜这样的普通非超导金属制作一个微小的环，[阿哈罗诺夫-玻姆效应](@keyword=aharonov_bohm_effect|lang=zh-CN|style=Feynman)是否也起作用？绝对是的。在低温下，一个电子在环绕整个环行进时可以保持其[量子相干性](@keyword=quantum_coherence|lang=zh-CN|style=Feynman)。穿过[环中心](@keyword=center_of_a_ring|lang=zh-CN|style=Feynman)的磁通量会改变电子的允许能级。一个令人难以置信的结果是**[持续电流](@keyword=persistent_currents|lang=zh-CN|style=Feynman)**的存在：一个稳定的直流电流在*没有任何外加电压*的情况下环绕着[圆环](@keyword=annulus|lang=zh-CN|style=Feynman)流动！这个电流是[阿哈罗诺夫-玻姆相](@keyword=aharonov_bohm_phase|lang=zh-CN|style=Feynman)位的直接、宏观的体现，是量子私语变得可闻 [@problem_id:2968742]。这个电流量很小，但它的存在证明了物质中量子波持久的相干性。

如果我们更仔细地观察这种环的[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)随磁通量变化的情况，我们会发现一曲丰富的干涉交响乐。在[基本周期](@keyword=fundamental_period|lang=zh-CN|style=Feynman)为 $\Phi_0 = h/e$ 的阿哈罗诺夫-玻姆[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)之上，常常出现另一组周期为 $h/2e$ 的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。这些[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)源于一种不同的干涉——电子路径与其精确的[时间反演](@keyword=time_reversal_2|lang=zh-CN|style=Feynman)伙伴之间的干涉。[量子输运](@keyword=quantum_transport|lang=zh-CN|style=Feynman)的世界是一个繁忙的地方，其他物理效应可以有选择地干扰这首交响乐的某些部分。例如，[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)与其运动之间的相互作用（自旋-轨道耦合）可以像一个选择性阻尼器一样。在具有强自旋-轨道效应的材料中，$h/2e$ [振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)被强烈抑制，而基本的 $h/e$ 阿哈罗诺夫-玻姆[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)则保持稳健，这提供了一种强有力的方法来解开不同的[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)路径 [@problem_id:2968750]。

### [几何相位](@keyword=geometric_phase|lang=zh-CN|style=Feynman)的统一性

到目前为止，我们的例子都与[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)有关。但现代物理学最美妙的方面之一是认识到阿哈罗诺夫-玻姆效应只是一个更深层次原理——**几何相位**——最著名的例子。一个量子粒子可以仅仅因为其所取路径的几何形状而获得[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)，这不仅限于真实空间，也存在于更抽象的参数空间中。

#### 物质与力学中的类似现象

想象一个[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，一个完美有序的原子阵列。现在，引入一个缺陷——一个刃[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)，这就像在晶体中插入了一个额外的半原子面。这个缺陷会产生一个长程应变场。这种机械[应变能](@keyword=strain_energy|lang=zh-CN|style=Feynman)否以类似于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的方式影响电子？令人惊讶的是，是的。该应变场在数学上可以被一个“有效”或“赝”[规范势](@keyword=gauge_potential|lang=zh-CN|style=Feynman)所描述，这与磁矢量势 $\mathbf{A}$ 完全类似。一个电子绕着[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)线沿闭合路径行进时，会获得一个相移，即一种“弹性的”[阿哈罗诺夫-玻姆效应](@keyword=aharonov_bohm_effect|lang=zh-CN|style=Feynman)！磁通量的角色由柏格斯矢量扮演，这是一个拓扑上表征[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)的量 [@problem_id:175592]。描述[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)的相同数学语言再次出现，用以描述固体中缺陷的量子力学。这是物理学统一性的绝佳体现。

这个概念在现代[拓扑材料](@keyword=topological_materials|lang=zh-CN|style=Feynman)的研究中大放 okunice彩。思考一下石墨烯，一个由碳原子[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成[蜂窝晶格](@keyword=honeycomb_lattice|lang=zh-CN|style=Feynman)的单层薄片。[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)中的电子有一个称为“[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)”的特殊属性，它不与它们的内禀自旋相关，而是与它们位于蜂窝结构中两个碳亚[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中的哪一个有关。这个[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)被锁定在电子的运动方向上。如果一个电子沿着弯曲路径行进，它的[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)被迫旋转，在此过程中，它获得一个称为[贝里相位](@keyword=berry_s_phase|lang=zh-CN|style=Feynman)的[几何相位](@keyword=geometric_phase|lang=zh-CN|style=Feynman)。在[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)环中，这导致了一个额外的、内在的 $\pi$ [相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)，它被加到通常的磁[阿哈罗诺夫-玻姆相](@keyword=aharonov_bohm_phase|lang=zh-CN|style=Feynman)位之上。其结果是显著的：整个干涉图样移动了半个周期。[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)的极大值变成了极小值，反之亦然 [@problem_id:2968747]。这告诉我们，总相位是多种影响的组合——外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)几何与材料本身的内部[量子几何](@keyword=quantum_geometry|lang=zh-CN|style=Feynman)。

这种遍历一个环路可以赋予一个内禀相位的思想也处于[粒子统计](@keyword=particle_statistics|lang=zh-CN|style=Feynman)的核心。正如我们所提到的，任意子在相互编织时会获得一个统计相位。这个相位纯粹是几何的。如果一个任意子被迫绕一个不可收缩的环路行进，比如圆柱体的周长，它会仅仅因为其世界的拓扑结构而获得一个统计相位。如果同时还有一个磁通量穿过该圆柱体，那么获得的总相位就是磁[阿哈罗诺夫-玻姆相](@keyword=aharonov_bohm_phase|lang=zh-CN|style=Feynman)位和这个内禀统计相位的简单相加 [@problem_id:108895]。

### 宇宙与“如果”式思考

我们所揭示的原理是如此基本，以至于它们超越了实验室甚至地球。它们为我们理解自然界的基本力和宇宙结构提供了信息。

#### 为何[电磁力](@keyword=electromagnetic_forces|lang=zh-CN|style=Feynman)是长程力？

让我们来问一个经典的 Feynman 式的“如果”问题。阿哈罗诺夫-玻姆效应最纯粹的形式是拓扑的：相移只取决于包围的磁通量，而不取决于路径的形状或其与场区的距离。这直接关系到电磁力是[长程力](@keyword=long_range_forces|lang=zh-CN|style=Feynman)的事实，而这又是因为其载力粒子——[光子](@keyword=photon|lang=zh-CN|style=Feynman)——是无质量的。但如果[光子](@keyword=photon|lang=zh-CN|style=Feynman)有微小的质量呢？

[有质量光子](@keyword=massive_photon|lang=zh-CN|style=Feynman)的物理学由 Proca 电动力学描述。在这个假设的宇宙中，来自[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)的矢量势将不会延伸至无穷远；它会随距离呈指数衰减。阿哈罗诺夫-玻姆效应仍然会存在，但它将不再是拓扑的。[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)将依赖于电子路径的半径，随着路径远离[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)而变得越来越弱 [@problem_id:43768]。通过思考这个另类现实，我们对自己所处的世界有了更深的理解：阿哈罗诺夫-玻姆效应优美、长程、拓扑的性质，是[光子](@keyword=photon|lang=zh-CN|style=Feynman)无质量和[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)基本[规范对称性](@keyword=gauge_symmetry|lang=zh-CN|style=Feynman)的直接体现。在一个完美展示 AB 效应[非局域性](@keyword=non_locality|lang=zh-CN|style=Feynman)的例子中，如果圆柱体由[超导材料](@keyword=superconducting_materials|lang=zh-CN|style=Feynman)制成，它可以完美地将其内部与外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)屏蔽开来。在这种情况下，没有磁通量被包围，穿过孔洞的电子完全不会获得相移，无论外部场有多强 [@problem_id:70079]。该效应是全有或全无的。

#### 引力的回响

我们以一个最宏大的问题来结束我们的旅程：是否存在引力版本的[阿哈罗诺夫-玻姆效应](@keyword=aharonov_bohm_effect|lang=zh-CN|style=Feynman)？根据 Einstein 的广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)，答案是肯定的。一个大质量、旋转的物体，比如行星或恒星，不仅仅是[弯曲时空](@keyword=curved_spacetime|lang=zh-CN|style=Feynman)；它还会“拖拽”[时空](@keyword=space_time|lang=zh-CN|style=Feynman)随之旋转。这种效应，称为参考系拖拽，是“引力磁学”的一种表现。对这种拖拽的数学描述涉及到一个行为与矢量势完全相同的时空度规分量。

想象一个粒子在一个旋转物体周围的闭合环路中行进，该区域的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)是平坦的（没有引力“场”）。然而，由于全局的参考系拖拽效应，该粒子仍会获得一个[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)。这种“引力磁[阿哈罗诺夫-玻姆效应](@keyword=aharonov_bohm_effect|lang=zh-CN|style=Feynman)”已被预测用于假设的物体，如旋转的宇宙弦 [@problem_id:989322]，并且原则上，对于任何旋转质量体都是一个真实存在的效应。

从电子实验室的微小电路到宇宙的旋转结构，阿哈罗诺夫-玻姆效应揭示了一个基本真理。世界不只是由局域发生的事情——作用于一点的力——所支配。它也由全局的、拓扑的性质所支配。它由一种深刻的几何织物编织而成，这种织物只有通过量子相位的透镜才能被看见。电子从一个它无法触及的场中听到的奇异私语，回响在整个物理学中，通过学习倾听它，我们以一种更丰富、更统一的方式理解了宇宙。