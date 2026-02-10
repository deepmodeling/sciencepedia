## 引言
在已建立的物理学世界中，电子等粒子被认为是基本且不可分割的。然而，在某些材料的量子荒野中，这条规则似乎被打破，揭示出一些颠覆传统描述（如 Landau 的[费米液体理论](@keyword=fermi_liquid_theory|lang=zh-CN|style=Feynman)）的[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)。本文深入探讨了**[涌现规范理论](@keyword=emergent_gauge_theory|lang=zh-CN|style=Feynman)**这一引人入胜的领域，它是一个强大的框架，用于解决一个深刻的谜题：当粒子看似分崩离析时会发生什么？我们将探究强相互作用如何导致[电子分数化](@keyword=electron_fractionalization|lang=zh-CN|style=Feynman)为新的实体（即部分子），以及这种分裂行为如何催生出支配其世界的全新力。

第一章“原理与机制”将剖析该理论的核心思想。我们将踏上[部分子](@keyword=partons|lang=zh-CN|style=Feynman)构造的旅程，发现[涌现规范场](@keyword=emergent_gauge_fields|lang=zh-CN|style=Feynman)的起源，并见证部分子禁闭与自由之间的激烈斗争。随后，“应用与跨学科联系”一章将展示这些概念的惊人影响力，揭示它们如何解释量子自旋液体、禁戒[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)等谜团，并为革命性的拓扑量子计算机提供蓝图。准备好进入材料内部的隐藏景观，在这里，基本规则被彻底改写。

## 原理与机制

想象一下，你手中握着一个电子。据我们所知，它是一种基本的、不可分割的粒子。它有确定的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)和确定的自旋，这两个属性与其身份融为一体。但如果我们玩个游戏会怎样？如果我们接受一个看似荒谬的概念——认为电子可以由更小的部分组成——又会如何？这不仅仅是异想天开；它是理解一些有史以来最奇异、最深刻的物质状态的狂野而奇妙的起点。这段旅程将带领我们穿越材料内部新的、隐藏的景观，在那儿，粒子分崩离析，无形的力从虚无中涌现，主宰着它们的命运。

### 粒子的分裂：[部分子](@keyword=partons|lang=zh-CN|style=Feynman)构造

让我们从反抗既定教条的行为开始。我们将提出，代表自旋为 $\sigma$ 的电子的数学对象——电子算符 $c_{\sigma}$，可以被“分数化”。我们可以将其写成两个新的、假设的粒子或**[部分子](@keyword=partons|lang=zh-CN|style=Feynman)**的乘积：一个我们称之为**[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)** ($f_{\sigma}$) 的中性、携带自旋的[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)，以及一个我们称之为**荷子** ($h$) 的无自旋、携带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)。一种简单的写法是 $c_{i\sigma} = h_i^\dagger f_{i\sigma}$，其中 $i$ 标记了[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中的一个格点 [@problem_id:3020589]。

乍一看，这似乎只是一个数学技巧，一次变量替换。但它有一个直接而惊人的物理含义。如果一个电子是自旋子和荷子的复合物，那么这些组分或许可以独立存在。想象一下向材料中注入一个电子。它可能不会作为一个单一实体行进，而是瞬间分解为一个带走其自旋的自旋子和一个带走其[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的荷子。如果这两个[部分子](@keyword=partons|lang=zh-CN|style=Feynman)随后以不同速度行进，电子的自旋和[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)就在空间上分离了。这一非凡现象被称为**[自旋-电荷分离](@keyword=spin_charge_separation|lang=zh-CN|style=Feynman)**。这不是幻想；它是一维相互作用电子系统（即所谓的 Tomonaga-Luttinger 液体）中已确立的低能现实 [@problem_id:3017361]。在这些系统中，你永远找不到传统的类[电子激发](@keyword=electronic_promotion|lang=zh-CN|style=Feynman)，只能找到其分离的自旋和[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)组分。Landau 的[费米液体理论](@keyword=fermi_liquid_theory|lang=zh-CN|style=Feynman)所熟悉的那个世界——其中“[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)”只是穿着一层相互作用外衣的电子——完全崩溃了。

### 自由的代价：[涌现规范场](@keyword=emergent_gauge_fields|lang=zh-CN|style=Feynman)

这个 $c = h^\dagger f$ 的数学戏法带来了一个深刻且不可避免的后果。这种分解并非唯一。例如，我们可以将[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)场乘以一个相位 $\exp(i\theta)$，荷子场也乘以该相位 $\exp(i\theta)$，它们的组合将保持不变：$(e^{-i\theta} h^\dagger) (e^{i\theta} f) = h^\dagger f = c$。这种内部描述可以旋转而不改变物理电子的模糊性，是一种**规范冗余**。

自然以其无穷的智慧，并不会忽略这样的冗余。它将这些冗余提升到核心地位。相位 $\theta$ 不仅仅是一个数学产物；它变成了一个新的、在整个系统中弥漫的涨落场——一个**[涌现规范场](@keyword=emergent_gauge_fields|lang=zh-CN|style=Feynman)**，我们称之为 $a_{\mu}$。这个场是一种新的自然力，完全诞生于我们强相互作用系统的约束之中。例如，[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)不再是自由的；它现在在这种新的涌现力下携带了+1的“荷” [@problem_id:1143333]。

这个场的起源非常具体。单占据约束——即在这些模型中同一个格点上不能有两个电子的规则——是由[规范场](@keyword=gauge_fields|lang=zh-CN|style=Feynman)的时间分量 $a_0$ 来强制执行的，$a_0$ 的作用类似于一个针对规范荷的涨落化学势。空间分量 $a_i$ 则源于[部分子](@keyword=partons|lang=zh-CN|style=Feynman)在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上从一个格点跃迁到另一个格点时跃迁项的相位 [@problem_id:3013820]。因此，一个起初用于处理[强相互作用](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)的巧妙记账技巧，最终揭示了一个支配着我们分数化粒子命运的、隐藏的动力学[力场](@keyword=force_field|lang=zh-CN|style=Feynman)。

### 伟大的拉锯战：禁闭与[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)

一旦[涌现规范场](@keyword=emergent_gauge_fields|lang=zh-CN|style=Feynman)诞生，一出大戏便拉开帷幕。它在[部分子](@keyword=partons|lang=zh-CN|style=Feynman)之间传递一种力，试图将它们[拉回](@keyword=pullback|lang=zh-CN|style=Feynman)到一起。如果这种力非常强且长程，它的作用就像一根无法挣断的橡皮筋，[部分子](@keyword=partons|lang=zh-CN|style=Feynman)分得越开，力就越强。这被称为**禁闭**。在禁闭相中，[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)和荷子永远无法真正自由；它们被永久地束缚成一个类电子的物体。分数化的梦想就此破灭。

如果这种力能够被减弱或“屏蔽”，[部分子](@keyword=partons|lang=zh-CN|style=Feynman)就能摆脱彼此的束缚并自由漫游。这就是**[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)**，一种真正奇异的量子物质状态。我们系统的命运——禁闭还是[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)——就悬于这场伟大的拉锯战之上。

禁闭的拥护者是[涌现规范场](@keyword=emergent_gauge_fields|lang=zh-CN|style=Feynman)的一个微妙属性：它的**紧致性**。与我们真空中的[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)不同，这个涌现场是周期性的，就像一个从 $0$ 到 $2\pi$ 变化的角。这种紧致性允许[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中出现称为**[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)**（在2+1维中称为[瞬子](@keyword=instantons|lang=zh-CN|style=Feynman)）的[拓扑缺陷](@keyword=topological_defects|lang=zh-CN|style=Feynman)。你可以将它们想象为涌现[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子被创造或湮灭的瞬息时刻。正如伟大的物理学家 Alexander Polyakov 所展示的，如果这些[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)大量增殖并在材料中形成密集的“气体”，它们会创造一个无序的环境，不可避免地导致禁闭[@problem_id:3012645]。

但也有为[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)而战的英雄。[部分子](@keyword=partons|lang=zh-CN|style=Feynman)自身就可以成为自己的救星。一片由低能、“[无能](@keyword=anergy|lang=zh-CN|style=Feynman)隙”部分子（例如形成[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)或[狄拉克锥](@keyword=dirac_cones|lang=zh-CN|style=Feynman)的那些）组成的密集海洋，在屏蔽磁单极子方面非常有效。这些物[质粒](@keyword=plasmid|lang=zh-CN|style=Feynman)子的集体舞蹈抑制了[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)的隧穿事件，有效地将它们从低能世界中驱逐出去，为[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)相铺平了道路。此外，底层[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的基本对称性有时会禁止最危险的、低[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)出现，从而为[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)提供了额外的优势 [@problem_id:3012645]。

这场战斗对世界的维度也极其敏感。在三维系统中，即使没有物质，纯粹的紧致[规范理论](@keyword=gauge_theory|lang=zh-CN|style=Feynman)天然就是[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)的——这种状态被称为库仑相。磁单极子是具有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的、能量成本高昂的激发，在低温下很少出现。然而，在二维中，纯理论*总是*禁闭的。这使得像高温[铜氧化物超导体](@keyword=cuprate_superconductors|lang=zh-CN|style=Feynman)这样的二维材料成为一个引人入胜且困难重重的战场，而三维[重费米子材料](@keyword=heavy_fermion_materials|lang=zh-CN|style=Feynman)则被认为是承载稳定、[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman) $U(1)$ 分数化相的更有希望的候选者 [@problem_id:3011637]。

### 逃离陷阱：[希格斯机制](@keyword=higgs_mechanism|lang=zh-CN|style=Feynman)与 $\mathbb{Z}_2$ 液体

还有另一条通往自由的更微妙的路径：**Anderson-Higgs 机制**。如果作为[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)的荷子决定发生玻色-爱因斯坦凝聚，形成[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)，会怎么样？这个由带电粒子组成的凝聚体提供了一种介质，使涌现[光子](@keyword=photon|lang=zh-CN|style=Feynman)深陷其中。规范玻色子实际上“吃掉”了凝聚体中的一个低能模式并变得有质量。一个有质量的力载子只能传递[短程力](@keyword=short_range_forces|lang=zh-CN|style=Feynman)。而[短程力](@keyword=short_range_forces|lang=zh-CN|style=Feynman)无法禁闭相距遥远的[部分子](@keyword=partons|lang=zh-CN|style=Feynman)！

在许多理论模型中，凝聚的不是单个部分子，而是它们的配对。例如，自旋子可能形成单重态对 $\Delta_{ij} = \langle f_{i\uparrow} f_{j\downarrow} - f_{i\downarrow} f_{j\uparrow} \rangle$，然后发生凝聚 [@problem_id:3012625]。由于这个配对由两个[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)组成，它携带的规范荷为 2。当这个荷为 2 的场凝聚时，它并不会完全消除规范场。相反，它将连续的 $U(1)$ [规范对称性](@keyword=gauge_symmetry|lang=zh-CN|style=Feynman)破缺为一个更简单的离散 $\mathbb{Z}_2$ 对称性——在该对称性下，规范变换只能将场乘以 $+1$ 或 $-1$。

由此产生的状态是一种**$\mathbb{Z}_2$[自旋液体](@keyword=spin_liquids|lang=zh-CN|style=Feynman)**，这是一个具有非凡性质的物质[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)相。它的激发是有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)和另一种称为**维桑子** (vison) 的有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)粒子。维桑子是一个 $\mathbb{Z}_2$ 磁通量点，是原始 $U(1)$ 磁单极子的残余。这些粒子表现出奇异的“互统计”性质。如果你让一个自旋子绕着一个维桑子走一个闭合环路，它的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)会获得一个负号：$\exp(i\pi) = -1$ [@problem_id:3013902] [@problem_id:1143238]。这种交换特性是量子编织的一种形式，也是构建内禀[容错](@keyword=fault_tolerance|lang=zh-CN|style=Feynman)拓扑量子计算机方案的基础。

### 没有战争的世界：静态[规范场](@keyword=gauge_fields|lang=zh-CN|style=Feynman)与 Kitaev 模型

[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)粒子的宇宙是否总是充满了动力学力的戏剧性和禁闭的威胁？完全不是。著名的 Kitaev 蜂巢模型提供了一个惊人的反例 [@problem_id:3019920]。在这个精确可解模型中，[自旋分数化](@keyword=fractionalization_of_spin|lang=zh-CN|style=Feynman)为两种 Majorana [费米子](@keyword=fermion|lang=zh-CN|style=Feynman)。其中一组 Majorana [费米子](@keyword=fermion|lang=zh-CN|style=Feynman)形成一个 $\mathbb{Z}_2$ 规范场，但有一个关键区别：这个[规范场](@keyword=gauge_fields|lang=zh-CN|style=Feynman)是完全**静态的**。它的构型在时间上被冻结，形成一个恒定的背景景观，另一组 Majorana“物质”粒子在其中运动。

由于[规范场](@keyword=gauge_fields|lang=zh-CN|style=Feynman)不是动态的，也就没有携带力的粒子可供交换。禁闭本质上是一种动力学现象，因此在本构造中根本不存在。物[质粒](@keyword=plasmid|lang=zh-CN|style=Feynman)子默认就是[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)的。这提供了一个优雅的量子自旋液体范例，其中存在规范结构，但禁闭与[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)之间那场熟悉的拉锯战被完全规避了。

### 实验室中的回响：观测[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)

如果这个由部分子和涌现力组成的理论世界不能与实验联系起来，那它就只是一个神话。那么，我们如何才能看到这些效应呢？最清晰的印记出现在我们直接探测电子的时候。

在正常金属中，如果我们用光电发射技术踢出一个电子，我们会在测得的谱函数 $A(k, \omega)$ 中看到一个尖峰。这个峰对应于一个定义明确、长寿命的类电子[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，其强度由一个数 $Z > 0$ 来衡量。在具有[自旋-电荷分离](@keyword=spin_charge_separation|lang=zh-CN|style=Feynman)的[一维系统](@keyword=one_dimensional_systems|lang=zh-CN|style=Feynman)中，电子实际上已经溶解了。踢出它会产生一团由分离的自旋子和荷子激发组成的混乱混合物，而不是一个单一的尖峰。[谱函数](@keyword=spectral_function|lang=zh-CN|style=Feynman)只显示出宽泛的、连续的特征，[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)强度消失为零：$Z=0$ [@problem_id:3020589]。

在二维或三维系统中，观测到 $Z=0$ 将是存在分数化的[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)态的“确凿证据”。相反，如果我们发现自己处于一个部分子存在但又被重新禁闭成类电子态（也许是通过希格斯机制）的相中，我们会[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)尖锐的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)峰重新出现（$Z > 0$），这标志着电子的“重构” [@problem_id:3020589]。在像[铜氧化物](@keyword=cuprates|lang=zh-CN|style=Feynman)这样的复杂材料中，现实可能更为微妙，[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)可能是一种短暂现象，只在高能量或短距离下稳定，而在最大尺度上，禁闭不可避免地会占据主导。这种**中间尺度**[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)的图景产生了极其复杂的实验信号，物理学家们仍在努力解开这些谜团 [@problem_id:2828363]。在我们的实验室中寻找分数化世界的回响，持续推动着现代物理学的前沿。