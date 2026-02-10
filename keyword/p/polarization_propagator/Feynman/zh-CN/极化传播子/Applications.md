## 应用与跨学科联系

在上一章中，我们熟悉了[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman) $\Pi(q, \omega)$。我们视其为一个数学对象，一个“响应函数”，它告诉我们当受到一个在空间（$q$）和时间（$\omega$）上变化的电势的扰动时，电子海洋的密度如何变化。现在，我们将离开其定义的庄严殿堂，进入广阔的现实世界。我们的任务是观察这个传播子的实际作用。我希望，你会被这个单一概念所阐明的现象之广度所震惊。这仿佛我们被赋予了一副神奇的透镜，通过它，我们能突然理解为何金属会发光，为何某些晶体会自发扭曲，以及是什么力将分子凝聚成液体。[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)不仅仅是一个抽象的公式；它是开启对物质世界深刻而统一理解的钥匙。

### 材料的反击：屏蔽与[介电响应](@keyword=dielectric_response|lang=zh-CN|style=Feynman)

让我们从电子海洋最直观的行为开始。想象一下，你将一个单一的正[测试电荷](@keyword=test_charge|lang=zh-CN|style=Feynman)放入金属内部。会发生什么？作为带负电的粒子，可移动的电子会被它吸引。它们会蜂拥至这个“入侵者”周围，形成一团负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)云，部分抵消掉这个正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的电场。从远处看，原来的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)显得更弱了，也就是被“屏蔽”了。这就是材料的反击，通过自我[重排](@keyword=derangement|lang=zh-CN|style=Feynman)来最小化干扰。

我们如何精确地描述这种效应？这正是我们的[传播子](@keyword=propagators|lang=zh-CN|style=Feynman)首次隆重登场的地方。一种材料的屏蔽能力由其介电函数 $\epsilon(q)$ 来表征。它告诉我们，与我们施加的*外部*电势相比，材料内部感受到的*总*电势被减小了多少。而一个非凡的结果是，静态[介电函数](@keyword=dielectric_function|lang=zh-CN|style=Feynman)直接由静态[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman) $\Pi(q)$ 给出！在所谓的[随机相近似](@keyword=random_phase_approximation_(rpa)|lang=zh-CN|style=Feynman)中，这个关系异常简洁：

$$
\epsilon(q) = 1 - v(q)\Pi(q)
$$

其中 $v(q)$ 只是电子间[库仑排斥](@keyword=coulomb_repulsion|lang=zh-CN|style=Feynman)作用的傅里叶变换[@problem_id:3014998]。请看这个方程。它告诉了我们一切。整个系统的响应 $\epsilon(q)$ 由两部分决定：其组分之间的基本相互作用 $v(q)$，以及电子密度重新排布的内在能力 $\Pi(q)$。如果你知道[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)，你就知道材料将如何屏蔽任何静态[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。

但为什么电子能够以这种方式响应呢？这种屏蔽的微观起源是什么？答案深藏于电子的量子本性之中，并且是[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)的深刻推论之一。要理解这一点，我们必须从[第一性原理](@keyword=ab_initio|lang=zh-CN|style=Feynman)出发计算[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)本身。当我们对一个零温下的简单[电子气](@keyword=electron_gas|lang=zh-CN|style=Feynman)（一种称为胶状模型的模型）进行此计算时，我们得到了一个著名的结果，称为[Lindhard函数](@keyword=lindhard_function|lang=zh-CN|style=Feynman)[@problem_id:2989231]。计算过程有些复杂，但它所描绘的物理图像却异常清晰。屏蔽响应几乎完全来自于“费米海”顶端的电子——那些能量最高的电子。为什么？因为它们是唯一附近有空闲能级可以跃迁的电子。一个深处于[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)内部的电子无法对微小的扰动做出响应，因为所有相邻的态都已被占据。因此，材料的屏蔽能力是费米面——即占据态与未占据态之间的边界——存在的直接结果。

### 材料的歌与舞：[集体激发](@keyword=collective_excitations|lang=zh-CN|style=Feynman)与光学性质

屏蔽是一种被动的响应。但电子海洋能否做出更主动的行为？它能否维持自身的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，就像一块石头投入池塘后水面所产生的涟漪？答案是肯定的，这些集体之舞被称为等离激元。

再次想象我们关于介电函数的方程 $\epsilon(q, \omega)$。当[介电函数](@keyword=dielectric_function|lang=zh-CN|style=Feynman)趋于零，即 $\epsilon(q, \omega) = 0$ 时，等离激元就发生了[@problem_id:1169166]。[介电函数](@keyword=dielectric_function|lang=zh-CN|style=Feynman)为零意味着，即使在*外部*电势为零的情况下，材料内部仍然可能存在有限的*总*电势！这意味着系统可以维持一个[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的内部电场——从而维持其自身电荷密度的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)——而无需任何外部驱动力。整个电子气这种自持的、集体的“晃动”就是[等离激元](@keyword=plasmons|lang=zh-CN|style=Feynman)。它是一种真正的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，一种[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)，具有由等离子体频率 $\omega_p$ 给出的明确能量。金属的光泽正是这些等离激元的直接视觉标志，它们在可见光谱范围内高效地反射光线。

当我们改变这场舞蹈上演的舞台时，故事变得更加有趣。如果我们将电子限制在一个平坦的二维平面上会发生什么？基本规则是相同的：等离激元仍然出现在 $\epsilon(q, \omega)$ 为零的地方。但是，由于库仑相互作用在二维空间中有所不同，[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)的行为也不同，于是出现了一种新的舞蹈。二维[等离激元](@keyword=plasmons|lang=zh-CN|style=Feynman)在长波长下不再具有几乎恒定的能量，而是呈现出一种奇特的[色散关系](@keyword=dispersion_relations|lang=zh-CN|style=Feynman) $\omega_p(q) \propto \sqrt{q}$ [@problem_id:68923]。这难道不奇妙吗？仅仅通过改变世界的维度，我们就改变了其集体激发的基本特性。这就是[传播子](@keyword=propagators|lang=zh-CN|style=Feynman)形式体系所能提供的深刻、结构性的洞察。

这种与光和[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的联系是普遍的。[光导率](@keyword=optical_conductivity|lang=zh-CN|style=Feynman) $\sigma(\omega)$ 衡量的是对[时变电场](@keyword=time_varying_electric_field|lang=zh-CN|style=Feynman)（如光）响应时电流的流动情况，它也与[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)直接相关[@problem_id:1176923]。通过分析 $\Pi(q, \omega)$ 的长波长极限，我们可以推导出金属对光的基本响应，这一结果将微观量子世界与我们日常观察到的宏观光学性质联系起来。

### 材料形成键合：从分子到[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)

到目前为止，我们讨论的都是无限大的晶体。但物质的组成单元——原子和分子呢？同样的逻辑也适用。一个分子的电子云在电场中发生形变的能力称为其[极化率](@keyword=polarizability|lang=zh-CN|style=Feynman) $\alpha$。这正是体积[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)在分子中的对应物。它可以用一个非常相似的理论框架来计算，将响应与分子特定的占据和未占据轨道联系起来[@problem_id:215885]。

在这里，我们遇到了最美丽、最令人惊讶的应用之一。我们都知道，即使是像氦或氩这样的中性、非极性原子也可以被液化。这意味着它们之间必定存在一种吸引力。这种力的来源是什么？它就是[伦敦色散力](@keyword=london_dispersion_forces|lang=zh-CN|style=Feynman)，一种[范德华相互作用](@keyword=van_der_waals_interactions|lang=zh-CN|style=Feynman)。而这种力，究竟是什么呢？它是两个相邻原子的[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)之间的对话！

可以这样想：原子A的电子云在不断地进行微小的[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)。在任何一个瞬间，它都可能有一个微弱的、瞬时的偶极矩。这个转瞬即逝的偶极子会产生一个电场，被原子B感受到。由其自身极化率描述的原子B的电子云对这个电场作出响应，产生一个感生偶极。B中的这个感生偶极接着与A中原来的瞬时[偶极相互作用](@keyword=dipole_interaction|lang=zh-CN|style=Feynman)。令人惊奇的结果是，这种相互作用在所有可能的[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)上取平均后，总是表现为吸引力！描述这种力的Casimir-Polder积分公式，涉及到对两个分子的[极化率](@keyword=polarizability|lang=zh-CN|style=Feynman) $\boldsymbol{\alpha}_A(i\omega)$ 和 $\boldsymbol{\alpha}_B(i\omega)$ 的乘积在虚频上的积分[@problem_id:2928566]。正是描述每个分子内部嗡嗡作响和[抖动](@keyword=dither|lang=zh-CN|style=Feynman)的[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)，产生了这种普遍存在的、将世界大部分物质凝聚在一起的温和力量。

### 涌现：新粒子与新[物相](@keyword=phases_of_matter|lang=zh-CN|style=Feynman)

我们现在来到了最深刻、也最引人注目的应用。在这里，[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)不仅描述了材料的性质；它还预测了全新现象的涌现——新的粒子，乃至新的物相。

在绝缘体中，能量足够的光可以将一个电子从填满的[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)激发到空的导带中，留下一个带正电的“空穴”。电子和空穴通过[库仑力](@keyword=coulomb_force|lang=zh-CN|style=Feynman)相互吸引。但它们是否可能形成一个稳定的束缚对，就像一个生活在晶体内部的微型氢原子？这将是一种新粒子——[激子](@keyword=excitons|lang=zh-CN|style=Feynman)。答案可以通过求解我们[响应理论](@keyword=response_theory|lang=zh-CN|style=Feynman)的一个更高级版本——Bethe-Salpeter方程来找到，该方程建立在[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)框架之上。人们发现，吸引性的电子-空穴相互作用确实可以产生能量*低于*材料主要吸收阈的分立[束缚态](@keyword=bound_states|lang=zh-CN|style=Feynman)[@problem_id:2929382]。这些[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)内的态就是激子，它们在[光吸收](@keyword=optical_absorption|lang=zh-CN|style=Feynman)谱中表现为尖锐的峰。[传播子](@keyword=propagators|lang=zh-CN|style=Feynman)揭示了晶体[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)谱中一个隐藏的结构层次。

或许最惊人的预测来自于考察电子与其所处的原子核[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)之间的相互作用。原子并非一个刚性的、静态的背景；它们可以[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。这些[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)被量子化为[声子](@keyword=phonons|lang=zh-CN|style=Feynman)。电子的响应会影响[声子](@keyword=phonons|lang=zh-CN|style=Feynman)吗？当然会！电子[极化[传播](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)子](@article_id:313582) $\Pi(q)$ 对[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的“[自能](@keyword=self_energy|lang=zh-CN|style=Feynman)”有贡献。现在，如果[电子结构](@keyword=electronic_structure|lang=zh-CN|style=Feynman)很特殊呢？在一些材料中，特别是低维材料，[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)可能具有大面积的、平行的部分。这被称为“[费米面嵌套](@keyword=fermi_surface_nesting|lang=zh-CN|style=Feynman)”。对于一个连接这些平坦区域的波矢 $\mathbf{Q}$，[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman) $\Pi(\mathbf{Q}, 0)$ 会变得非常大。在[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上有大量的电子可以被具有这个特定[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman)的微扰轻易激发。

这种巨大的电子响应对[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)产生了戏剧性的影响。$\Pi(\mathbf{Q}, 0)$ 的巨大负值可以导致在该特定[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman) $\mathbf{Q}$ 处的[重整化](@keyword=renormalization|lang=zh-CN|style=Feynman)后的[声子](@keyword=phonons|lang=zh-CN|style=Feynman)频率软化，一直降到零[@problem_id:2818799]。一个零频率的[声子](@keyword=phonons|lang=zh-CN|style=Feynman)不再是[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)；它是[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的一种永久性的静态畸变，波长为 $2\pi/|\mathbf{Q}|$。整个晶体自发地屈曲并重组成一个新的、更复杂的结构，称为电荷密度波（CDW）。在这里，[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)扮演了不稳定的预兆角色，预测了系统自身的电子响应将驱动一次[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，进入一个全新的物相。

从宁静的屏蔽行为到[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的戏剧性坍塌，[极化传播子](@keyword=polarization_propagator|lang=zh-CN|style=Feynman)一直是我们的向导。这单一的概念能够将金属、分子、光和[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)编织成一幅连贯的织锦，这有力地证明了物理学的统一性。它向我们展示了，在多相互作用粒子的世界里，整体不仅不同于其各部分之和——它还可以是惊人地、美妙地、且不可预测地更加丰富。