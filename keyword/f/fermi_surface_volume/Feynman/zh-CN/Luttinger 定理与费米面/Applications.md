## 应用与跨学科联系

既然我们已经掌握了[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)背后的原理和 Luttinger 定理的深刻论断，你可能会想把它当作一个美丽但或许抽象的理论物理学成果存档。事实远非如此。这个定理不是博物馆的展品；它是一匹任劳任怨的驮马，一把能解锁材料世界中各种惊人现象的万能钥匙。它是我们的向导，我们的会计师，确保无论金属中的电子相互作用变得多么奇异或复杂，粒子的基本计数都得到遵守。让我们踏上一段旅程，看看这个简单的计数规则如何让我们能够表征、预测，甚至发现物质的秘密。

### 基本普查：从电子数到金属特性

我们这个新工具最直接的应用就是一次简单的普查。如果你告诉我一种简单金属有多少价电子，我就能告诉你它的[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)体积。对于一种[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)近似球形的简单金属，这意味着我们可以仅凭其电子密度计算出它的尺寸，比如[费米波矢](@keyword=fermi_wavevector|lang=zh-CN|style=Feynman) $k_F$ [@problem_id:2810712]。想一想：单个原子的一个属性——它愿意共享的电子数量——决定了数以万亿计的电子在固体中运动的宏观集体属性。

但我们怎么知道我们是对的呢？毕竟，物理学是一门实验科学。最优雅的验证之一来自一种称为[德哈斯-范阿尔芬效应](@keyword=dhva_effect|lang=zh-CN|style=Feynman)的现象。当我们将金属置于低温下的强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中时，我们发现其磁性会随着我们改变磁场强度而以一种奇特、周期性的方式[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。事实证明，这些[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的频率与[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)的[横截面](@keyword=cross_section|lang=zh-CN|style=Feynman)积成正比。我们通过这些实验测量的频率，与我们仅仅通过数电子预测出的尺寸惊人地精确匹配，这是[量子理论](@keyword=quantum_theory|lang=zh-CN|style=Feynman)的辉煌胜利。这位宇宙会计师，Luttinger 定理，其账目完美无误 [@problem_id:2812607]。

### 超越球体：真实材料的丰富织锦

当然，世界很少像一个完美的球体那么简单。晶体中的原子[排列](@keyword=permutation|lang=zh-CN|style=Feynman)在一个周期性[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中，这种重[复结构](@keyword=complex_structure|lang=zh-CN|style=Feynman)在空间结构上施加了自己的“纹理”。电子在某些方向上移动比其他方向更容易。这种各向异性将[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)从一个简单的球体扭曲成各种美丽而复杂的形状。

想象一种像一叠煎饼一样构建的材料，电子可以在煎饼层内轻松穿梭，但很难在层与层之间跳跃。它的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)可能看起来像一个圆柱体，或者可能是一张波浪状的、起伏的薄片 [@problem_id:1766265]。在更奇特的材料中，比如最近发现的[节线半金属](@keyword=nodal_line_semimetals|lang=zh-CN|style=Feynman)，费米面可以呈现出环形——一个漂浮在动量空间中的甜甜圈 [@problem_id:2810795]。然而，尽管如此复杂，我们的定理依然坚挺。*形状*可能被[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)扭曲，但这些表面所包围的总*体积*仍然顽固地由电子数固定。

在许多现代材料中，特别是像[高温超导体](@keyword=high_temperature_superconductors|lang=zh-CN|style=Feynman)这样的研究前沿材料，情况更为复杂。布里渊区中不仅仅只有一个[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)，而是有几个不同的“口袋”共存。一些口袋是“电子型”的，另一些是“空穴型”的，代表电子的缺失。在这里，Luttinger 定理变成了一个详细的记账规则。[实验物理学](@keyword=experimental_physics|lang=zh-CN|style=Feynman)家使用[角分辨光电子能谱](@keyword=arpes|lang=zh-CN|style=Feynman)（[ARPES](@keyword=arpes|lang=zh-CN|style=Feynman)）等技术，可以绘制出这些口袋并测量它们的体积。然后他们可以检查[电子口袋](@keyword=electron_pockets|lang=zh-CN|style=Feynman)的体积是否与空穴口袋的体积平衡。一个完美平衡的材料被称为“[电荷补偿](@keyword=charge_compensation|lang=zh-CN|style=Feynman)”材料。了解像[铁基超导体](@keyword=iron_based_superconductors|lang=zh-CN|style=Feynman)这样的材料是补偿的，还是有轻微的电子或空穴过剩，是理解其电子特性及其超导倾向的关键线索 [@problem_id:2831483]。

### 相互作用的魔力：当电子穿上“外衣”

到目前为止，我们已经看到 Luttinger 定理对容器的形状漠不关心。现在我们迎来一个更深刻的发现：对于绝大多数材料来说，它也对电子之间汹涌、复杂的相互作用漠不关心。

想象一个房间里有一群人。你可以数出他们的人数。现在，如果他们开始互动，配对跳舞，形成交谈圈，或者相互碰撞呢？情况变得复杂，但只要没有人进出，人数是不变的。Luttinger 定理就是这个道理的量子版本。在哈伯德模型（一个电子相互作用的基本蓝图）中，我们可以“调大”电子间的排斥。随着我们这样做，电子变得越来越迟缓。它们不再像[自由粒子](@keyword=the_free_particle|lang=zh-CN|style=Feynman)那样行为，而是像“[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)”，穿着一层自身相互作用的云，这使得它们重得多。人们可能天真地认为这会改变[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)。但它不会。[费米面体积](@keyword=fermi_surface_volume|lang=zh-CN|style=Feynman)保持绝对恒定，是一个[拓扑不变量](@keyword=topological_invariants|lang=zh-CN|style=Feynman)，即使我们增加相互作用强度也是如此。它坚守阵地，直到相互作用变得如此之强，以至于系统经历灾难性的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，电子戛然而止，形成莫特绝缘体。在那一点上，金属态本身就不存在了 [@problem_id:2974469]。

这种稳固性导致了凝聚态物理中最壮观的现象之一，这发现在被称为“重费米子”体系的材料中。这些材料通常含有像 Cerium 或 Ytterbium 这样的元素，它们有两种电子：普通的、可移动的[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)，以及像微小局部磁体一样行为的、紧密束缚的“$f$”电子。在高温下，只有[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)形成[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)。[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)是“小”的，只计算了这些电子。

但当我们冷却材料时，一个量子力学奇迹发生了。[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)海开始与[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)发生相干相互作用。每个局域磁矩都被[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)“屏蔽”，形成一个复杂的、纠缠的多体态。在这个新的低温状态下，曾经局域化的 $f$ 电子被吸收到集体中。它们成为巡游流体的一部分。结果是戏剧性的：费米面突然改变其尺寸。它变得“大”，因为现在 Luttinger 定理必须计算*原始*[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)和*新动员起来的* $f$ 电子 [@problem_id:3018914]。这不是一个微小的变化；这是电子[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的根本性转变，是费米体积的一次不连续跳跃，可以直接观察为材料电子性质的改变 [@problem_id:56906]。

### 前沿：探索[量子物质](@keyword=quantum_matter|lang=zh-CN|style=Feynman)的侦探工具

这种揭示[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子“真实”数量的能力，使得[费米面体积](@keyword=fermi_surface_volume|lang=zh-CN|style=Feynman)成为物理学前沿不可或缺的工具。考虑一个重费米子金属在绝对零度下通过施加压力等方式被调控跨越一个量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)。在一边，它是一个具有[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)的顺磁性金属。在另一边，它是一个[反铁磁体](@keyword=antiferromagnets|lang=zh-CN|style=Feynman)。它是如何到达那里的？

可能存在两种相互竞争的理论。一种理论是[自旋密度波](@keyword=spin_density_wave_2|lang=zh-CN|style=Feynman)（SDW）转变，它提出[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)保持完整，只是被新的磁周期性重构和打开[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。另一种理论是“近藤破坏”（KB）转变，它提出了一个更为激进的观点：$f$ 电子突然放弃集体，恢复为[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)，导致费米面从大崩溃到小。

我们如何决定？我们使用 Luttinger 定理作为我们的向导。我们进行对[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)尺寸敏感的实验。[霍尔系数](@keyword=hall_coefficient|lang=zh-CN|style=Feynman)——一个衡量[载流子密度](@keyword=charge_carrier_density|lang=zh-CN|style=Feynman)的指标——在转变点是平滑演变还是突然跳跃？量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的频率是连续变化还是不连续变化？通过回答这些问题，我们可以区分这两种情景，并揭示[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)的基本性质 [@problem_id:2833047]。

故事甚至还没有结束。还有关于更奇异物质状态的理论提议，即所谓的“分数化”液体，其中电子本身可能分裂成携带其自旋和[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的组成部分。在这样一个奇异的世界里，我们熟悉的 Luttinger 定理版本将会失效。但它的失效方式非常具体，测得的费米体积与预期电子数的偏差本身将成为这种新的、拓扑有序的[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)的确凿证据 [@problem_id:2812607]。

从一个直观的计数法则到一个用于诊断[量子临界性](@keyword=quantum_criticality|lang=zh-CN|style=Feynman)和拓扑序的工具，[费米面体积](@keyword=fermi_surface_volume|lang=zh-CN|style=Feynman)的概念是贯穿凝聚态物理学核心的一条金线。它以惊人的清晰度和力量向我们展示了最基本的守恒定律如何与量子力学的丰富性合谋，共同编排了电子世界宏伟而美丽的交响乐。