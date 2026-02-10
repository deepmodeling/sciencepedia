## 引言
在广阔的材料世界中，一些最引人入胜、最具技术前景的材料被归类为“强关联系统”。在这些材料中，电子不再能被视为独立的粒子；它们之间的相互排斥作用占据主导地位，导致了一系列传统理论无法解释的奇异行为。这种复杂性的核心是磁性，它源于[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)之间错综复杂的舞蹈。理解这些系统中[磁性的起源](@keyword=origins_of_magnetism|lang=zh-CN|style=Feynman)至关重要，因为它掌握着解锁从高温超导电性到新奇[量子物态](@keyword=quantum_state_of_matter|lang=zh-CN|style=Feynman)等现象的关键。本文旨在解决一个基本问题：强相互作用是如何调控材料的集体磁性的？这是一个简单的模型无法解决的难题。

本文将引导您穿越这个复杂但有益的课题。首先，在“原理与机制”部分，我们将探讨基本概念，对比局域化的原子磁矩和[离域](@keyword=delocalization|lang=zh-CN|style=Feynman)的巡游电子这两个世界。我们将揭示原子自旋赖以[排列](@keyword=permutation|lang=zh-CN|style=Feynman)的多种沟通渠道——交换相互作用。我们还将审视那些因竞争性[量子效应](@keyword=quantum_effects|lang=zh-CN|style=Feynman)而产生奇异物质状态（如[重费米液体](@keyword=heavy_fermi_liquid|lang=zh-CN|style=Feynman)）的战场。随后，“应用与跨学科联系”部分将把这些理论与现实联系起来。我们将看到实验物理学家如何探测这些隐藏的磁性世界，电子的双重性如何在真实材料中体现，以及磁性如何与超导及其他电子特性紧密相连。让我们从深入探讨支配这场量子力学大戏的原理开始。

## 原理与机制

现在我们已经对迷人的[强关联材料](@keyword=strongly_correlated_materials|lang=zh-CN|style=Feynman)世界有了初步了解，让我们揭开其层层面纱，看看使其运转的齿轮与杠杆。为什么有些材料会成为强磁体，而另一些则顽固地保持非磁性？这个故事，正如物理学中常有的那样，始于电子。但这并非一个简单的故事，因为电子是一个出了名的“精神分裂”角色，有时表现得像一个微小的、局域化的旋转陀螺，有时又像一个弥散的、游荡的波。这两种特性之间的较量，正是固体中磁性的核心所在。

### 两种磁体之说：局域与巡游

想象一下在城市中漫步。在某些社区，居民们足不出户，每人都被限制在自己的房子里。而在另一些社区，街道上则挤满了自由流动的人群。固体中电子的世界与此非常相似。这种根本差异催生了两种截然不同的磁性图景。

首先是**局域磁矩**图景。在这里，负责产生磁性的电子被紧[紧束缚](@keyword=binding_constraints|lang=zh-CN|style=Feynman)在它们的母原子上。这种情况最著名地出现在含有内层电子壳层未填满的元素的材料中，例如过渡金属（铁、镍）的$3d$壳层，或[稀土元素](@keyword=rare_earth_elements_2|lang=zh-CN|style=Feynman)（钆、镨）埋藏更深的$4f$壳层。原子核的强大电吸引力以及同一原子上其他电子的排斥力——我们称之为**[在位库仑排斥](@keyword=on_site_coulomb_repulsion|lang=zh-CN|style=Feynman)**，或简称$U$——共同作用，将这些电子锁定在原位。每个原子都成了它自己的微小磁性王国。

在这些原子王国中，一套被称为**Hund定则**的严格规则支配着电子的排布方式。可以把它想象成一种原子[社会等级](@keyword=dominance_hierarchy|lang=zh-CN|style=Feynman)制度。首先，电子会占据不同的轨道，且自旋方向相同，以使[总自旋](@keyword=total_spin|lang=zh-CN|style=Feynman)$S$最大化。然后，它们会重新排布以使总轨道角动量$L$最大化。例如，对于一个具有$4f^2$[电子构型](@keyword=electron_configurations|lang=zh-CN|style=Feynman)的特定[稀土离子](@keyword=rare_earth_ions|lang=zh-CN|style=Feynman)，这些规则决定了其[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的[总自旋](@keyword=total_spin|lang=zh-CN|style=Feynman)为$S=1$、总轨道角动量为$L=5$。在这些较重的原子中，自旋和[轨道运动](@keyword=orbital_motion|lang=zh-CN|style=Feynman)强耦合在一起，形成一个单一、明确的总角动量$J$。对于$4f^2$这种情况（壳层填充未过半），结果是$J = |L-S| = 4$。[@problem_id:2980074]

这赋予了原子一个稳定且可测量的磁矩。在[稀土离子](@keyword=rare_earth_ions|lang=zh-CN|style=Feynman)中，$4f$电子被外层电子壳层很好地屏蔽，其轨道运动基本不受影响，使它们几乎成为局域磁矩的理想范例。相比之下，对于$3d$[过渡金属](@keyword=transition_metals|lang=zh-CN|style=Feynman)，$d$轨道位于原子的“外部”，并与周围晶体的电场发生强烈相互作用，这种效应通常会“淬灭”或冻结轨道角动量，使得磁矩几乎完全来自电子自旋。

在轨道的另一边，我们发现了**[巡游磁性](@keyword=itinerant_magnetism|lang=zh-CN|style=Feynman)**。在这里，电子不局限于任何单个原子，而是[离域](@keyword=delocalization|lang=zh-CN|style=Feynman)的，形成一个遍布整个晶体的广阔“电子海”。这些是在金属中[传导电流](@keyword=conduction_current|lang=zh-CN|style=Feynman)的电子。一个均匀的电子海如何能变得有磁性？这是通过一种集体共谋实现的。物理学家Edmund Stoner提出了一个极其简单的想法：想象一下将电子海分成两个群体，自旋向上和自旋向下。强迫一些电子翻转自旋会消耗动能，因为它们必须移动到更高能量的状态以避免踩到其他电子（Pauli不相容原理的结果）。然而，自旋相同的电子会自然地相互避开，这减少了它们之间的库仑排斥。如果这种排斥能的减少超过了动能的代价，系统就会发现自发产生磁矩是有利的，从而从一片巡游电子海中创造出铁磁体。

这场竞争被[在位库仑排斥](@keyword=on_site_coulomb_repulsion|lang=zh-CN|style=Feynman)$U$和**带宽**$W$之间的对抗完美地捕捉到，后者代表了电子通过在原子间跃迁可以节省的动能。
*   当$U$远大于$W$（$U \gg W$）时，电子被困在各自的原子上。我们处于局域极限，此时的磁性最好由这些局域自旋之间的相互作用来描述，这种情况被**[Heisenberg模型](@keyword=heisenberg_model|lang=zh-CN|style=Feynman)**所捕捉。许多绝缘氧化物就是这种情况。[@problem_id:2479417]
*   当$W$大于或与$U$相当（$W \gtrsim U$）时，电子可以自由漫游。我们处于巡游极限，磁性是[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)电子的集体不稳定性，由**[Stoner模型](@keyword=stoner_model|lang=zh-CN|style=Feynman)**描述。金属铁磁体如铁和镍就是这种情况。[@problem_id:2479417]

因此，第一个宏大原理是：固体中的磁性源于两种原型之一——一组明确的[原子磁矩](@keyword=atomic_magnetic_moments|lang=zh-CN|style=Feynman)，或一片游荡电子海的集体不稳定性。关键的仲裁者是库仑排斥与动能之比，$U/W$。

### 与邻共语：磁交换之舞

拥有磁矩，无论是局域的还是巡游的，都只是故事的一半。它们如何相互沟通以建立集体有序，例如铁磁体中的一致[排列](@keyword=permutation|lang=zh-CN|style=Feynman)或[反铁磁体](@keyword=antiferromagnets|lang=zh-CN|style=Feynman)中的交替模式？这种沟通被称为**交换相互作用**。

对于绝缘体中的[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)，原子之间通常相距太远，其电子云无法直接重叠。它们需要一个中间人。在许多氧化物中，这个角色由位于磁性金属离子之间的氧原子扮演。这种间接相互作用被称为**[超交换作用](@keyword=superexchange_interaction|lang=zh-CN|style=Feynman)**。这种交换的规则非常微妙，并精确地依赖于几何结构，正如**Goodenough-Kanamori规则**所阐述的那样。

考虑一条直线[排列](@keyword=permutation|lang=zh-CN|style=Feynman)的原子，金属-氧-金属，键角为$180^\circ$。一个金属原子上的电子要影响其邻居，它必须通过氧原子进行一次“虚”跃迁。量子力学的Pauli不相容原理规定，如果两个金属离子的自旋相反，这次虚跃迁的可能性要大得多。结果是产生了一种强大的推动力，促使自旋形成交替的上-下-上-下模式：**[反铁磁性](@keyword=anti_ferromagnetism|lang=zh-CN|style=Feynman)**[@problem_id:3012237]。这有点像两个人试图通过一扇旋转门握手；只有当他们朝相反方向移动时才能顺利进行。

但如果将几何结构改为$90^\circ$键角，主要路径就被阻塞了。现在，一个更微妙的、更高阶的过程可能占据主导。在某些情况下，这可以改变相互作用的符号，从而倾向于自旋的平行[排列](@keyword=permutation|lang=zh-CN|style=Feynman)：**铁磁性**[@problem_id:3012237]。这里的精妙之处在于，键角这个看似微不足道的细节，可以完全改变一种材料的磁性！

如果材料含有混合价态的原子，例如一个同时包含$\mathrm{Mn}^{3+}$和$\mathrm{Mn}^{4+}$离子的链，情况就变得更加复杂了。现在，一个电子实际上可以从$\mathrm{Mn}^{3+}$位点*真实地*跃迁到$\mathrm{Mn}^{4+}$位点。如果两个锰位点上巨大的、局域化的“核心”自旋指向同一方向，这种跃迁会容易得多得多。为什么？因为接受原子的Hund定则——到达的电子希望其自旋与已有的自旋平行。为了最大限度地实现[离域](@keyword=delocalization|lang=zh-CN|style=Feynman)并降低其动能，电子有效地迫使所有核心自旋[铁磁性](@keyword=ferromagnetism|lang=zh-CN|style=Feynman)地[排列](@keyword=permutation|lang=zh-CN|style=Feynman)起来。这种强大的机制被称为**[双交换作用](@keyword=double_exchange|lang=zh-CN|style=Feynman)**[@problem_id:3012237]。

为了真正理解这些绝缘体，我们甚至必须区分两种类型。在**[Mott-Hubbard绝缘体](@keyword=mott_hubbard_insulator|lang=zh-CN|style=Feynman)**中，电子运动的主要障碍是金属位点上的巨大排斥能$U$。而在**电荷转移绝缘体**中，从氧配体上拉走一个电子（耗能$\Delta$）实际上比将两个电子放在同一个金属原子上更容易。这看似一个学术细节，但却至关重要。例如，高温超导体就是通过掺杂[电荷转移](@keyword=charge_transfer|lang=zh-CN|style=Feynman)绝缘[体制](@keyword=body_plans|lang=zh-CN|style=Feynman)成的，其中配对的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子是主要生活在氧原子上而不是铜原子上的空穴。[@problem_id:2987319]

### 动荡的结合：电子海中的[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)

我们已经看到了两种极端情况：拥有[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)的绝缘体和拥有巡游电子的金属。但在迷人的中间地带，当我们有一个由明确的[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)（比如来自$f$-电子）组成的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)[浸没](@keyword=submersions|lang=zh-CN|style=Feynman)在一片巡游[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)的海洋中时，会发生什么呢？这就是**[重费米子](@keyword=heavy_fermion|lang=zh-CN|style=Feynman)**材料的领域，也是一个充满竞争趋势的战场。

一方面，导电电子可以充当长距离的信使，将一个局域磁矩的[自旋取向](@keyword=spin_alignment|lang=zh-CN|style=Feynman)信息传递给另一个。这种[间接交换](@keyword=indirect_exchange|lang=zh-CN|style=Feynman)被称为**[RKKY相互作用](@keyword=rkky_interaction|lang=zh-CN|style=Feynman)**。它试图将[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)锁定在一个长程磁有序中，通常是反铁磁有序。这种有序趋势的强度与局域电子和巡游电子之间耦合的平方成正比，我们称之为$J_K^2$。

另一方面是一种没有经典类比的纯粹量子力学效应：**Kondo效应**。在高温下，局域磁矩表现得独立。但随着温度降低，导电电子海发动了一场无声的叛乱。它们“围攻”每一个[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)，屏蔽其自旋，直到它被有效地中和，形成一个非磁性的“单态”。这种屏蔽趋势的特征[能标](@keyword=energy_scales|lang=zh-CN|style=Feynman)是[Kondo温度](@keyword=kondo_temperature|lang=zh-CN|style=Feynman)$T_K$，它随耦合$J_K$呈[指数增长](@keyword=exponential_growth|lang=zh-CN|style=Feynman)，并试图破坏[RKKY相互作用](@keyword=rkky_interaction|lang=zh-CN|style=Feynman)正试图建立的磁性。

物理学家Don Doniach绘制了一张简单但深刻的相图，描绘了这场战争的结果[@problem_id:3018877]。
*   当耦合$J_K$较弱时，RKKY获胜。随着材料冷却，它在[Néel温度](@keyword=néel_temperature|lang=zh-CN|style=Feynman)$T_N$下进入磁有序态。
*   当耦合$J_K$较强时，Kondo效应获胜。[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)被“溶解”到导电电子海中。系统避免了磁有序，而是在低温下转变为一种奇异的新物质状态：**[重费米液体](@keyword=heavy_fermi_liquid|lang=zh-CN|style=Feynman)**。

[重费米液体](@keyword=heavy_fermi_liquid|lang=zh-CN|style=Feynman)究竟是什么？它是一种金属，但在其中电子的表现好像它们获得了巨大的质量，有时高达自由电子质量的1000倍！这些“重”电子，或称[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，是原始导电电子和现已溶解的$f$-电子磁矩的复合物。实验上，这种“重”是显而易见的。比热的电子贡献，由系数$\gamma$量化，变得巨大。电阻率在高温下因与未屏蔽磁矩的散射而上升后，在低温下随着相干重态的形成而急剧下降[@problem_id:2833094] [@problem_id:2843765]。这些不是你日常所见的金属；它们是强关联能够引发深刻转变的明证。

### 前沿：为何简单图像会失效

假装物理学家已经完全搞清楚了这一切，那将是一种误导。事实上，强关联领域是一个前沿阵地，我们许多最简单、最可信的理论工具在这里都会失效。这种失效本身就具有深刻的启发性。

以[巡游铁磁性](@keyword=itinerant_ferromagnetism|lang=zh-CN|style=Feynman)的[Stoner模型](@keyword=stoner_model|lang=zh-CN|style=Feynman)为例。其简单的判据，$I N(E_F) > 1$（其中$I$是[相互作用强度](@keyword=interaction_strength|lang=zh-CN|style=Feynman)，$N(E_F)$是[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)的[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)），对于强铁磁体通常有效。然而，对于处于磁性边缘的材料，像[密度泛函理论](@keyword=density_functional_theory|lang=zh-CN|style=Feynman)（DFT）这样建立在类似平均场精神上的标准计算方法，常常会发出错误的警报。它们预测存在磁性，而实验上却没有发现[@problem_id:2997268]。原因是这些静态的、平均场理论忽略了**[自旋涨落](@keyword=spin_fluctuations|lang=zh-CN|style=Feynman)**。可以把它想象成即将结冰的液体；它充满了不断形成和融化的微观冰晶。在近磁性金属中，自旋不断形成短暂的、局域的磁性斑块（称为**顺磁振子**），这些斑块平均后为零。这些涨落是系统的真实物理，它们作为一种强大的无序力量，抑制了更简单理论所预测的[长程有序](@keyword=long_range_order|lang=zh-CN|style=Feynman)。

当我们考虑强关联的[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)模型——**[Hubbard模型](@keyword=hubbard_model|lang=zh-CN|style=Feynman)**时，这个挑战更加明显。一种看似简单的弱[耦合方法](@keyword=coupling_method|lang=zh-CN|style=Feynman)，即[随机相近似](@keyword=random_phase_approximation_(rpa)|lang=zh-CN|style=Feynman)（RPA），在这里惨败。它无法在不引入[对称性破缺](@keyword=symmetry_breaking|lang=zh-CN|style=Feynman)的情况下描述Mott绝缘体的有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)绝缘态。它完全忽略了[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)的出现及其在高温下的特征性Curie-Weiss磁化率。在二维情况下，它甚至错误地预测在有限温度下存在磁有序，这违反了一个被称为**[Mermin-Wagner定理](@keyword=mermin_wagner_theorem|lang=zh-CN|style=Feynman)**的严格数学结果[@problem_id:3019504]。

这些失败教会了我们一个至关重要的教训：在强关联的世界里，你无法将单个粒子的行为与整体的集体行为清晰地分离开。粒子的属性（如其质量）由其与群体的相互作用决定，而群体的响应又由粒子的属性决定。万物皆与其他万物耦合。为了取得进展，我们需要复杂的理论框架，如**[动力学平均场理论](@keyword=dynamical_mean_field_theory|lang=zh-CN|style=Feynman)（DMFT）**，它正是为解决这种自洽反馈循环而设计的[@problem_id:3019504] [@problem_id:2997268]。因此，深入磁性核心的旅程，也是一次通往理论物理前沿的旅程，在那里，众多相互作用电子的美丽而复杂的舞蹈，继续挑战并激励着我们。