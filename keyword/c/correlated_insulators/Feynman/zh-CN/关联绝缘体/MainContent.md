## 引言
在材料世界中，[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)体和绝缘体之间的区别似乎是根本性的。简单的[能带理论](@keyword=electronic_band_theory|lang=zh-CN|style=Feynman)通过描述电子如何填充允许的能级（即[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)）来优雅地解释了这一点。当一个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)被完全填满，且与下一个空带之间存在较大的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)时，该材料就是[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)绝缘体；否则，它就是金属。然而，自然界偶尔会提出一些深刻的难题，挑战这些基本思想。某些材料，如氧化镍，根据能带理论本应是金属，实验上却被发现是优良的绝缘体。这种鲜明的矛盾揭示了我们最简单的图像中的一个关键缺陷，并将我们带入了关联绝缘体的奇异领域。

本文旨在解决一个根本问题：当电子间的相互作用，特别是它们彼此的排斥力，成为主导其行为的力量时，会发生什么？我们将探讨这种“电子关联”如何使[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子戛然而止，将一个本应是金属的材料转变为绝缘体。这段旅程将揭示一幅远超简单导电现象的丰富画卷，触及磁性、非常规超导以及全新的量子物质状态。

为了解开这个谜题，我们首先将深入探讨催生关联绝缘体的基本**原理与机制**。我们将探索[电子跃迁](@keyword=electronic_transitions|lang=zh-CN|style=Feynman)与排斥之间的斗争，介绍关键的哈伯德模型，并定义莫特绝缘体的结构，将其与其他类型的绝缘态进行对比。随后，我们将进入**应用与跨学科联系**的世界，揭示这些迷人的材料如何成为现代物理学中一些最激动人心的研究领域的核心，从[高温超导体](@keyword=high_temperature_superconductors|lang=zh-CN|style=Feynman)的奥秘到[莫尔材料](@keyword=moiré_materials|lang=zh-CN|style=Feynman)中人工构建的量子景观。

## 原理与机制

现在，你可能会想：“绝缘体有什么大不了的？有些东西导电，有些不导电。这是入门知识。” 对于某些类型的绝缘体，你说得没错。对于像硅或金刚石这样的材料，情况很简单，而且相当优雅。电子居住在一座秩序井然的公寓楼里——[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，其中允许的能级被分组成“楼层”，即**[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)**。**[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)绝缘体**就是一个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)被完全填满，并且与下一个完全空的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)之间存在一个巨大[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的情况。电子无处可去；它们所在楼层的每个“座位”都被占满，而跳到上面空楼层的能量成本太高。由简单[能带理论](@keyword=electronic_band_theory|lang=zh-CN|style=Feynman)所讲述的故事到此结束。

但大自然喜欢出难题。物理学家偶然发现了像氧化镍（NiO）这样的材料，它打破了这幅整洁的图景。根据我们可靠的能带理论——该理论将电子视为在晶体中滑行的独立波——NiO应该有一个部分填充的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。它应该是一种金属！这就像一个半满的停车场，有大量的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)供汽车移动。然而，实验上，NiO是一种极好的绝缘体 [@problem_id:1789857]。所有的汽车都卡在自己的位置上，拒绝移动。这不仅仅是一个小错误；这是我们最简单、最基本的固体理论的灾难性失败。这个矛盾告诉我们，我们忽略了一些至关重要的东西，这些东西把一个本应是金属的材料变成了一个顽固的绝缘体。这种新型的状态就是我们所说的**关联绝缘体**。

### 意志之战：跃迁与排斥

为了理解这种对常识的反叛，我们必须超越行为良好、独立电子的图景。我们必须承认，电子，说得温和点，是“反社会”的。它们带负电，并且相互排斥。在大多数金属中，电子移动得如此之快，并且分布得如此之广（[离域](@keyword=delocalization|lang=zh-CN|style=Feynman)），以至于这种排斥仅仅是一种背景噪音。但如果它们被迫挤在狭小的空间里呢？

想象一下一串原子链上的电子。有两种基本的冲动主宰着它们的生活。第一种是量子力学的探索冲动——从一个原子跳到它的邻居那里。这就是**动能**，我们可以用一个参数 $t$（代表“转移”或“跃迁”）来表示。这种跃迁使得电子能够[离域](@keyword=delocalization|lang=zh-CN|style=Feynman)并导电；它是驱动一个系统趋向于成为金属的冲动 [@problem_id:2454792]。

第二种冲动是纯粹的[静电排斥](@keyword=electrostatic_repulsion|lang=zh-CN|style=Feynman)。一个电子单独占据一个原子没有问题。但如果第二个电子试图跳到同一个原子上，就会产生剧烈的排斥。让两个电子处在同一个位置需要付出巨大的能量代价。我们称这个能量成本为**[在位库仑排斥](@keyword=on_site_coulomb_repulsion|lang=zh-CN|style=Feynman)**，或简称 $U$。这是阻碍移动、促进局域化的势能 [@problem_id:2454792]。

关联绝缘体的整个故事就是这两种力量之间的意志之战：离域的动能 $t$ 和局域化的排斥能 $U$。

当 $t$ 远大于 $U$ 时，电子移动的欲望轻易地克服了它们之间的相互厌恶。它们[离域](@keyword=delocalization|lang=zh-CN|style=Feynman)成宽的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)，你就得到了一个标准的金属（或者如果[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)恰好被填满，就是[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)绝缘体）。但当情况反转，$U$ 远大于 $t$ 时，戏剧性的事情发生了。排斥力赢了。

### 莫特绝缘体的剖析

在 $U \gg t$ 的区域，电子跳到已占据格点的能量代价变得令人望而却步。如果我们平均每个原子有一个电子（这种情况称为**半填充**），为了避免支付巨大的能量惩罚 $U$，每个电子实际上都被“困”在自己的原子上。这种由于强排斥作用导致电子停止移动的现象被称为**莫特局域化**，由此产生的状态是**[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)**。交通堵塞不是因为缺少[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)，而是因为司机们拒绝彼此相邻停车！

#### [莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)与哈伯德[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)

这种[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)局域化以一种新颖而有趣的方式重塑了[电子结构](@keyword=electronic_structure|lang=zh-CN|style=Feynman)。原来半填充的金属[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)被完全摧毁。取而代之的是，出现了两个新的、截然不同的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)，它们被一个巨大的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)隔开。这些被称为**哈伯德[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)** [@problem_id:2862019]。

*   **下哈伯德[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)**对应于每个原子都拥有其单个电子的状态。要移动一个电子（即产生电流），你必须将其从原子上移走，留下一个空穴。
*   **上哈伯德[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)**对应于高能状态，在这种状态下，你强行将第二个电子放到了一个已被占据的原子上，形成一个“双占据格点”或**双电子子**。

下哈伯德[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的顶部和上哈伯德[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的底部之间的能量差就是**[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)**。其大小约等于 $U$，即创建第一个双电子子-空穴对的能量成本。这不是由[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)周期性产生的单粒子[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)；它是一个源于[电子-电子排斥](@keyword=electron_electron_repulsion|lang=zh-CN|style=Feynman)的真正的**多体[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**。这就像是由 $U$ 设定的“入场费”，你必须支付这笔费用才能让[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子开始移动。

#### [电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)冻结，自旋自由

在这里，我们偶然发现了一个极其精妙的要点。在莫特绝缘体中，电子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)被锁定在原位。但每个局域化的电子仍然拥有一个内在属性：它的自旋。虽然电子不能相互“拜访”，它们的自旋仍然可以相互“交流”！[@problem_id:2862019]

如何实现呢？通过一个称为**[超交换](@keyword=superexchange|lang=zh-CN|style=Feynman)**的微妙量子力学过程。想象相邻原子上的两个电子，它们的自旋方向相反。存在一个微小而短暂的机会，一个电子会“虚拟”地跳到邻居的格点上（产生一个暂时的、高能量的双电子子），然后立刻跳回来。由于[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)，这种短暂的、被禁止的“旅行”只有在[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)相反时才可能发生。这次快速旅行的净效应是稍微降低了系统的能量。如果电子的自旋平行，这个虚拟跃迁过程就被禁止，它们的能量就不会降低。

这意味着系统在能量上偏爱相邻自旋反向[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。它在自旋之间发展出一种有效的[反铁磁耦合](@keyword=antiferromagnetic_coupling|lang=zh-CN|style=Feynman)，通过[微扰理论](@keyword=perturbation_theory|lang=zh-CN|style=Feynman)可以证明，其强度 $J$ 正比于 $\frac{t^2}{U}$ [@problem_id:2479456]。因此，[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)虽然是电的不良导体，但通常是一种充满活力的[磁性材料](@keyword=magnetic_materials|lang=zh-CN|style=Feynman)。[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)被冻结了，但自旋的世界却因低能激发（自旋波或[磁振子](@keyword=magnons|lang=zh-CN|style=Feynman)）而生机勃勃。

### 绝缘体现场指南

这种丰富的物理学为我们提供了清晰的标志，用以区分这些奇异的绝缘体和它们更平凡的表亲。

#### 莫特 vs. 斯莱特：鸡生蛋还是蛋生鸡？

正如我们刚才看到的，许多[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)是[反铁磁性](@keyword=anti_ferromagnetism|lang=zh-CN|style=Feynman)的。但有些材料成为绝缘体是*因为*它们是反铁磁性的。反铁磁有序可以将晶胞的大小加倍，这会折叠电子[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)并打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。这被称为**斯莱特绝缘体**。那么，究竟是哪种情况呢？材料是因其为磁体而绝缘（斯莱特），还是因其为底层的[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)而成为磁体？

关键的考验是温度。斯莱特[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)是磁序的直接后果。如果你将材料加热到其磁有序温度（**[奈尔温度](@keyword=néel_temperature|lang=zh-CN|style=Feynman)**，$T_N$）之上，磁性消失，斯莱特[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)也随之关闭。材料应该会变成金属。然而，在莫特绝缘体中，主[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的量级是 $U$，而磁性是尺度为 $J \sim t^2/U$ 的低能效应。由于 $U \gg t$，[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)远大于磁性的能标。因此，[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)在远高于其[奈尔温度](@keyword=néel_temperature|lang=zh-CN|style=Feynman)时仍然是稳定的绝缘体。[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)在非磁性的顺磁相中持续存在，是[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)的确凿证据 [@problem_id:3006254] [@problem_id:2454792]。

#### 莫特 vs. 安德森：相互作用 vs. 无序

还有另一种方式可以困住电子：**无序**。如果[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)不是完美的，而是含有高密度的缺陷和杂质，随机的[势场](@keyword=potential_field|lang=zh-CN|style=Feynman)会导致电子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)变得局域化。这是一种**[安德森绝缘体](@keyword=anderson_insulator|lang=zh-CN|style=Feynman)**。关键的区别在于机制：莫特局域化源于洁净晶体中电子-电子的*相互作用*，而[安德森局域化](@keyword=anderson_localization|lang=zh-CN|style=Feynman)源于电子-无序散射，即使没有相互作用也会发生。它们可以通过在低温下的导电方式来区分。[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)显示出**激活**输运，其电导率与 $\exp(-\Delta/T)$ 成比例，因为电子必须通过[热激发](@keyword=thermal_excitation|lang=zh-CN|style=Feynman)跨越硬[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $\Delta$。而[安德森绝缘体](@keyword=anderson_insulator|lang=zh-CN|style=Feynman)，其[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)中甚至可能没有硬[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，通过**变程跃迁**导电，这是一个电子在遥远的局域态之间隧穿的过程，其特征[电导率](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)与 $\exp[-(T_0/T)^{\alpha}]$ 成比例 [@problem_id:2800117]。

#### 真实世界：电荷转移绝缘体

哈伯德模型是一个优美的简化，但在像氧化物这样的真实材料中，氧原子（“配体”）扮演着至关重要的角色。在20世纪80年代，Zaanen、Sawatzky 和 Allen 意识到绝缘体可以被分类在一个更丰富的图表中。最低能量的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)激发可能不是将一个电子从一个金属原子跳到另一个金属原子（能量成本为 $U$），而是将一个电子从附近的氧原子转移到金属原子上。这个过程的能量成本被称为**电荷转移能**，$\Delta$ [@problem_id:2484978]。

这给了我们两类主要的关联绝缘体：
1.  **[莫特-哈伯德绝缘体](@keyword=mott_hubbard_insulator|lang=zh-CN|style=Feynman)**：当 $U < \Delta$ 时出现。[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)具有我们熟悉的 $d \rightarrow d$ 特征，其大小由 $U$ 决定。
2.  **电荷转移绝缘体**：当 $\Delta < U$ 时出现。最低能量的激发是从氧的 $p$ 轨道到金属的 $d$ 轨道。[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)具有 $p \rightarrow d$ 特征，其大小由 $\Delta$ 决定。

这个ZSA方案提供了一个更准确、更具预测性的框架来理解真实世界的材料，从[莫特-哈伯德绝缘体](@keyword=mott_hubbard_insulator|lang=zh-CN|style=Feynman)NiO到[电荷转移](@keyword=charge_transfer|lang=zh-CN|style=Feynman)绝缘体CuO——[高温超导体](@keyword=high_temperature_superconductors|lang=zh-CN|style=Feynman)的母体化合物。

### 一种更深层次的奇异性：打破基本规则

也许莫特绝缘体最深刻的方面是它们如何打破了金属物理学的一个基石原则：**[卢廷格定理](@keyword=luttinger_s_theorem|lang=zh-CN|style=Feynman)**。本质上，这个定理是一个“粒子计数”规则。它指出，对于任何正常金属，**[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)**——动量空间中分隔已占据态和未占据态的边界——的体积严格由电子总数决定 [@problem_id:1124473]。

一个半填充的莫特绝缘体具有很高的电子密度。如果它是一个金属，[卢廷格定理](@keyword=luttinger_s_theorem|lang=zh-CN|style=Feynman)将要求一个大的、明确的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)。但[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)*没有*[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)；它处处都有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)！它的[费米面体积](@keyword=fermi_surface_volume|lang=zh-CN|style=Feynman)为零。这是对[卢廷格定理](@keyword=luttinger_s_theorem|lang=zh-CN|style=Feynman)的一个直接而惊人的违反。

这告诉我们一些极其深刻的事情：[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)不仅仅是一个有奇怪[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的金属。它是一种全新的物质状态，不能从一个简单的非相互作用[电子气](@keyword=electron_gas|lang=zh-CN|style=Feynman)平滑地演变（或“[绝热连接](@keyword=adiabatic_connection|lang=zh-CN|style=Feynman)”）而来。它是**[非费米液体](@keyword=non_fermi_liquids|lang=zh-CN|style=Feynman)**的一个典型例子。更奇怪的是，对一个基本定理的这种违反并不要求系统打破其底层[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的任何对称性，如[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)。这种奇异性是强关联本身的一种内在的、涌现的属性 [@problem_id:1124473]。

### 驯服野兽：我们如何计算不可能

这种固有的“奇异性”使得关联绝缘体极难建模。材料物理学中的标准计算方法，如使用**[局域密度近似](@keyword=local_density_approximation|lang=zh-CN|style=Feynman)（LDA）**等简单近似的**[密度泛函理论](@keyword=density_functional_theory|lang=zh-CN|style=Feynman)（DFT）**，是建立在独立粒子或平均场图像之上的。它们非常擅长描述关联较弱的系统。但当面对[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)时，它们会灾难性地失败。因为它们不能正确处理强的在位排斥 $U$，所以它们倾向于过度[离域电子](@keyword=delocalized_electrons|lang=zh-CN|style=Feynman)。对像NiO这样的[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)进行LDA计算通常会——错误地——预测它是一种金属 [@problem_id:2088767]。

这种失败的根本原因是，这些简单的泛函“过于平滑”；它们缺少一个称为**[导数](@keyword=derivative|lang=zh-CN|style=Feynman)[不连续性](@keyword=discontinuity|lang=zh-CN|style=Feynman)**的特征，并且存在**[自相互作用误差](@keyword=self_interaction_error|lang=zh-CN|style=Feynman)**，即电子会虚假地与自身相互作用。为了解决这个问题，物理学家们开发了更复杂的方法。像**[DFT+U](@keyword=dft+u|lang=zh-CN|style=Feynman)**和**[杂化泛函](@keyword=hybrid_functionals|lang=zh-CN|style=Feynman)**这样的技术就是为了修正这个缺陷而设计的。它们通过为局域电子显式地加回一个类似哈伯德的 $U$ 惩罚，或者通过混合一部分精确的非局域交换来起作用，这有助于惩罚[自相互作用](@keyword=self_interaction|lang=zh-CN|style=Feynman) [@problem_id:2985479]。这些先进的方法已经取得了显著的成功，最终让理论家能够从[第一性原理计算](@keyword=ab_initio_calculations|lang=zh-CN|style=Feynman)这些[强关联材料](@keyword=strongly_correlated_materials|lang=zh-CN|style=Feynman)的性质，并与实验进行预测性的对话。

从一个简单的实验难题到关于[量子物质](@keyword=quantum_matter|lang=zh-CN|style=Feynman)本质和计算前沿的深刻问题，关联绝缘体的故事完美地展示了，努力解决一个简单的矛盾如何[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)领我们发现全新的物理大陆。