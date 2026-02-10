## 引言
自被发现以来，[铜氧化物](@keyword=cuprates|lang=zh-CN|style=Feynman)材料一直处于物理学的前沿，既带来了巨大的挑战，也提供了非凡的机遇。它们在前所未有的高温下展现超导电性的能力，打破了现有的理论[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)，并预示着一场技术革命。然而，支配这些材料的物理学极其复杂，其复杂性被浓缩在一个“[相图](@keyword=phase_portraits|lang=zh-CN|style=Feynman)”中，该相图描绘了它们在不同温度和载流子浓度下的行为。然而，这张图并非简单的[状态图](@keyword=state_diagram|lang=zh-CN|style=Feynman)表；它是一片由奇异物相构成的令人困惑的领域，包括备受瞩目的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)、磁有序绝缘体、一个神秘的“[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)”，以及一种行为与地球上任何物质都不同的“[奇异金属](@keyword=strange_metals|lang=zh-CN|style=Feynman)”。核心问题在于找到能为这种复杂性带来秩序并解释[高温超导](@keyword=high_temperature_superconductivity|lang=zh-CN|style=Feynman)机制的根本原理。

本文旨在作为穿越这片迷人领域的导览。通过将其分解为不同组成部分，并解释赋予它们意义的理论概念，本文旨在揭开[铜氧化物相图](@keyword=cuprate_phase_diagram|lang=zh-CN|style=Feynman)的神秘面纱。您将不仅了解到这些[物相](@keyword=phases_of_matter|lang=zh-CN|style=Feynman)是*什么*，还将理解它们*为何*会从[强相互作用](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)电子的量子力学舞蹈中涌现。这场旅程将从探索基本原理和机制开始，始于[铜氧平面](@keyword=cuo2_planes|lang=zh-CN|style=Feynman)的独特性质、其[电子结构](@keyword=electronic_structure|lang=zh-CN|style=Feynman)，以及其绝缘和磁性母体的起源。随后，我们将见证掺杂如何改变材料，催生出[超导穹顶](@keyword=superconducting_dome|lang=zh-CN|style=Feynman)和其他神秘的物相。接下来，文章将把焦点转向这些知识的应用和跨学科联系，展示相图如何成为实验科学家不可或缺的工具，并成为连接[材料设计](@keyword=materials_design|lang=zh-CN|style=Feynman)、[黑洞物理学](@keyword=black_hole_physics|lang=zh-CN|style=Feynman)等其他科学前沿领域的深刻桥梁。

## 原理与机制

既然我们已经对铜氧化物这片令人困惑的领域有了一瞥，现在让我们更深入地探索。我们的目标是理解其*原因*。为什么这些材料会以如此奇特而美妙的方式行事？如同任何一部伟大的戏剧，铜氧化物的故事在一个独特的舞台上展开，由一群遵循几条基本规则的相互作用的角色共同演绎。要欣赏这出戏剧，我们必须首先了解舞台和演员。

### [铜氧平面](@keyword=cuo2_planes|lang=zh-CN|style=Feynman)舞台：一个关于强关联的故事

所有有趣的事情都发生在一个近二维的铜氧原子平面上，即$\mathrm{CuO_2}$平面。如果您学过入门级的固态物理学，您可能会根据电子数量预测这些材料应该是金属。简单的计算表明，最高[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)是半满的，为电子移动和导电留下了充足的空间。但大自然给了我们一个惊喜：未掺杂的母体化合物，如$\mathrm{La_2CuO_4}$，并非金属，而是优良的绝缘体。

为什么？关键在于**强关联**。想象一下，铜位点是些小房间，而电子是极度反社会、彼此厌恶的居住者。将两个电子放在同一个铜位点上的能量代价，我们称之为参数$U_d$，是巨大的——远大于它们通过跳跃到相邻位点所能获得的能量，这个参数称为$t$。这就是**[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)**的本质：电子被“局域化”，不是被任何外部势垒困住，而是被它们之间的相互排斥作用困在各自的位点上。

但故事更为微妙。在[铜氧化物](@keyword=cuprates|lang=zh-CN|style=Feynman)中，氧原子扮演着至关重要的角色。事实证明，将一个电子从氧原子移动到铜原子的能量代价，一个称为电荷转移能$\Delta$的量，*小于*将两个电子放在同一铜位点上的代价$U_d$。这使得铜氧化物成为**电荷转移绝缘体**，而非简单的[莫特-哈伯德绝缘体](@keyword=mott_hubbard_insulator|lang=zh-CN|style=Feynman) [@problem_id:3009369]。这个看似微小的细节至关重要：它决定了当我们开始产生可移动的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)时，它们会倾向于驻留在氧原子上，而不是铜原子上。这为后续所有复杂的物理现象搭建了舞台。

### 母体态：一场[凝固](@keyword=coagulation|lang=zh-CN|style=Feynman)的磁性舞蹈

因此，在未掺杂的母体化合物中，我们有一个局域化的电子平面，每个铜位点上有一个电子。它们无法四处移动以导电。但它们是否无所事事？远非如此。虽然它们被困住了，但它们的[量子力学自旋](@keyword=quantum_mechanics_spin|lang=zh-CN|style=Feynman)仍然可以相互作用。一个铜位点上的电子可以进行一次到其邻居的“虚”跳跃——这是一种通常被巨大的排斥作用$U_d$所禁止的短暂[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)。然而，这种快速的访问和返回，使得两个相邻铜位点上的自旋能够相互感知。最终结果是一种被称为**[超交换](@keyword=superexchange|lang=zh-CN|style=Feynman)**的有效磁相互作用，其强度$J$正比于$\frac{t^2}{U_d}$ [@problem_id:1781835]。

这种[超交换相互作用](@keyword=superexchange_interaction|lang=zh-CN|style=Feynman)是反铁磁性的：它迫使每个电子的自旋指向与其所有邻居相反的方向。因此，未掺杂的$\mathrm{CuO_2}$平面的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)是一个完美的磁性棋盘格，一个**反铁磁**（AFM）态。这不仅仅是一个理论上的奇想；它是一种实在的、有序的物质相，存在于某个称为[奈尔温度](@keyword=néel_temperature|lang=zh-CN|style=Feynman)$T_N$的[临界温度](@keyword=critical_temperature|lang=zh-CN|style=Feynman)之下。这是一个具有优美、凝固的磁序的领域。

### 掺杂：搅动一池春水

现在，我们扮演变革者的角色。我们可以通过一种称为**掺杂**的过程来化学改变材料，从而从$\mathrm{CuO_2}$平面中移除电子，留下可移动的“空穴”。让我们用$p$表示这些空穴的浓度。

这些空穴去了哪里？正如我们所知，由于[铜氧化物](@keyword=cuprates|lang=zh-CN|style=Feynman)是电荷转移绝缘体，空穴在能量上更倾向于驻留在铜位点周围的氧原子上。氧原子上的空穴并不会孤立存在；它会与相邻铜原子的自旋形成一个强烈的量子力学束缚态。这个复合体，被称为**张-赖斯[单重态](@keyword=singlet_state|lang=zh-CN|style=Feynman)**，是掺杂铜氧化物中的基本载流子 [@problem_id:3009369]。

将这些可移动的空穴引入刚性的反铁磁棋盘格中，首要的后果是什么？它们会摧毁它。一个可移动的空穴，在追求退局域化以降低其动能的过程中，就像一个在完美棋盘上涂鸦的破坏者。空穴的运动不可避免地会扰乱自旋的整齐反向[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。起初，你可能会认为AFM序只是被稀释了，但实际机制要优雅得多。空穴的集体运动倾向于将[磁序](@keyword=magnetic_ordering|lang=zh-CN|style=Feynman)扭曲成螺旋状。随着空穴浓度$p$的增加，这个螺旋的波长$\lambda(p)$会缩短。为了使材料保持真正的长程三维[磁序](@keyword=magnetic_ordering|lang=zh-CN|style=Feynman)，不同的$\mathrm{CuO_2}$平面必须在磁性上相互锁定。但它们只能在一定距离内，即层间锁定长度$\ell_{\perp}$，维持这种步调一致。当掺杂引起的螺旋变得过紧——也就是说，当$\lambda(p)$变得比$\ell_{\perp}$短时——各层便无法再协调，三维AFM序随之瓦解 [@problem_id:2828399]。这种美妙的竞争长度尺度机制解释了为什么AFM相会如此突然地消失，仅在$p \approx 0.02$的微小空穴浓度下。

### 宏伟之旅：电子态地图

随着AFM序的瓦解，我们进入了一个广阔而神秘的新领域。完整的温度-掺杂（$T-p$）相图就是我们探索这个新世界的地图。让我们来一次巡游。

我们的地图有两个轴：纵轴是温度$T$，[横轴](@keyword=transverse_axis|lang=zh-CN|style=Feynman)是空穴掺杂$p$ [@problem_id:2994159]。在最左边（$p=0$），是我们已经讨论过的反铁磁绝缘体。当我们稍微增加$p$时，AFM相迅速退去。然后，奇迹出现了：**[超导穹顶](@keyword=superconducting_dome|lang=zh-CN|style=Feynman)**。但在到达那里之前，我们必须穿行于其上方的区域。这个区域被泛称为“正常态”，但它绝不正常。它包罗了各种奇异的行为。

至关重要的是要理解，这张地图上的线并非都是同一种类型 [@problem_id:3009326]。一些线，如AFM相的边界（$T_N$）和超导相的边界（$T_c$），标志着真正的**[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)**。跨越这些线就像水冻结成冰；系统的性质会突然改变，一种新的[对称性破缺](@keyword=symmetry_breaking|lang=zh-CN|style=Feynman)的序态出现。而其他线，最著名的是[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)线$T^\star$，被认为是**[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)**（crossover）。跨越一条[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)线更像是空气从潮湿逐渐变为干燥；行为会发生变化，但没有一个尖锐、奇异的转变点。

### [超导穹顶](@keyword=superconducting_dome|lang=zh-CN|style=Feynman)：精妙的平衡

这张地图上最著名的特征是存在高温超导的穹顶状区域。在大约$p \approx 0.05$的[掺杂浓度](@keyword=doping_concentration|lang=zh-CN|style=Feynman)下，材料在[临界温度](@keyword=critical_temperature|lang=zh-CN|style=Feynman)$T_c$以下开始超导。随着我们添加更多的空穴，$T_c$会升高，在“最佳掺杂”（$p \approx 0.16$）处达到最大值，然后再次下降，最终在$p \approx 0.27$附近消失。这种非单调的形状就是著名的**[超导穹顶](@keyword=superconducting_dome|lang=zh-CN|style=Feynman)**。

为什么是穹顶？最简单的直觉是，超导需要在两个因素之间达成妥协：可用于形成配对的载流子数量，以及将它们结合在一起的“胶水”的强度 [@problem_id:1781809]。在低掺杂时，你有很强的胶水但载流子不足。在重过掺杂区，你有大量的载流子，但胶水变弱了。最佳点介于两者之间。

但是，*什么*是胶水呢？一个主流理论，源于AFM相的邻近性，认为胶水是由**[自旋涨落](@keyword=spin_fluctuations|lang=zh-CN|style=Feynman)**——融化的磁序的颤动残余——构成的。当将掺杂从过掺杂一侧调谐至磁性**[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)**（QCP）时，这些涨落会增强，从而增强配对胶水并导致$T_c$上升。然而，一个美丽的悖论出现了：如果涨落变得过强过慢（正好在QCP附近），它们不仅会形成配对，还会散射它们，起到一种**破对**作用，从而抑制$T_c$。此外，胶水本身的特征能量也会崩溃。这种在增强的相互作用和崩溃的[能量尺度](@keyword=energy_scales|lang=zh-CN|style=Feynman)之间的自然竞争，优雅地产生了一个穹顶状的$T_c$ [@problem_id:3009301]。最高的$T_c$并非出现在QCP*处*，而是在距离它一个安全的位置。

### 巨大之谜：[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)与竞争序

或许我们地图上最深的谜团是**[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)**相，它笼罩在欠掺杂区（$p  0.16$）的[超导穹顶](@keyword=superconducting_dome|lang=zh-CN|style=Feynman)之上。在一个[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)温度$T^\star(p)$以下，这个温度在低掺杂时远高于$T_c(p)$，材料开始表现得非常奇怪。从光[电子能谱](@keyword=electron_energy_spectrum|lang=zh-CN|style=Feynman)（ARPES）到[核磁共振](@keyword=nuclear_magnetic_resonance|lang=zh-CN|style=Feynman)（NMR）的大量实验都发现证据表明，电子能谱中开始打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，抑制了低能态的可及性 [@problem_id:3011016] [@problem_id:3009380]。

这仿佛是电子已经开始配对，但没有实现真正超导所需的宏观长程[相位相干性](@keyword=phase_coherence|lang=zh-CN|style=Feynman)。想象一个巨大的舞厅里挤满了舞者。超导就好比所有舞伴在整个舞池中以完美、同步的步伐共舞。而[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)相则像是一种状态，舞者们已经找到了各自的舞伴，并开始在小团体中跳华尔兹，但这些团体之间尚未相互[同步](@keyword=entrainment|lang=zh-CN|style=Feynman)。系统在局部打开了[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，但缺乏展现[零电阻](@keyword=zero_resistance|lang=zh-CN|style=Feynman)的全局[相干性](@keyword=coherence|lang=zh-CN|style=Feynman)。

[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)区域并非一个等待超导出现的空荡荡的候车室；它是一个**竞争序**的战场。大自然在其复杂性中，探索着组织电子的其他方式。一种惊人的可能性是形成**[条纹相](@keyword=stripe_phase|lang=zh-CN|style=Feynman)** [@problem_id:2491220]。在这里，系统在空穴的运动需求和自旋的反铁磁序需求之间找到了一个复杂的折衷方案。空穴分离成一维的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)河流，流淌在近乎完美反铁磁性的背景中。这是电子[自组织](@keyword=self_organization|lang=zh-CN|style=Feynman)的一个卓越范例。

更奇异的可能性，即所谓的“隐藏序”，可能潜伏在[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)中。例如，测量偏振光旋转（[克尔效应](@keyword=kerr_effect|lang=zh-CN|style=Feynman)）的极其灵敏的实验已经发现了一种自发破缺[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)的相的证据，这与在一个晶体晶胞内存在[微观电流](@keyword=microscopic_current|lang=zh-CN|style=Feynman)环的理论提议相符 [@problem_id:3009378]。揭示[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)的真实性质及其与超导的关系，仍然是物理学中最大的未解之谜之一。

### 回归常态：过掺杂区的[费米液体](@keyword=fermi_liquid|lang=zh-CN|style=Feynman)

最后，如果我们继续推进，将体系掺杂到远超[超导穹顶](@keyword=superconducting_dome|lang=zh-CN|style=Feynman)的范围（$p > 0.27$），会发生什么？奇特性逐渐消退。[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)消失。在最佳掺杂附近的“[奇异金属](@keyword=strange_metals|lang=zh-CN|style=Feynman)”区域表现出与温度成奇特的线性关系的[电阻率](@keyword=electrical_resistivity|lang=zh-CN|style=Feynman)，最终过渡到正常金属所预期的常规$T^2$依赖关系。我们终于抵达了**费米液体**的熟悉领域。在这里，强关联已得到充分的屏蔽，电子，或者更准确地说，它们的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)化身，表现得如同教科书固态理论中行为良好、近乎独立的粒子 [@problem_id:2994159]。

穿越[铜氧化物相图](@keyword=cuprate_phase_diagram|lang=zh-CN|style=Feynman)的旅程，是一次穿越强关联量子物质奇迹的旅行。它始于[磁性绝缘体](@keyword=magnetic_insulators|lang=zh-CN|style=Feynman)的欺骗性简单，穿过竞争序、隐藏相和壮观的[超导穹顶](@keyword=superconducting_dome|lang=zh-CN|style=Feynman)的漩涡，最终抵达常规金属的平静彼岸。这张地图上的每一个特征都讲述了一个关于电子精妙而深刻的量子之舞的故事，一个我们才刚刚开始完全理解的舞蹈。