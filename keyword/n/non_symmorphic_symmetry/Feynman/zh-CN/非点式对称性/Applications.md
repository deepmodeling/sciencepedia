## 应用与跨学科联系

在上一章中，我们剖析了[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)的奇特而美丽的本质——那些将旋转或反射与“被禁止的”分数平移相结合的特殊晶体学规则。我们看到，它们不仅仅是晶体分类中的奇闻异事，而是强制固体中波状态之间产生惊人联系的基本规则。现在，我们提出物理学家最喜欢问的问题：*那又怎样？* 我们在哪里能看到这些规则在起作用？我们能用它们做什么？

本章是一段旅程，探讨迈出那并非完整一步所带来的后果。我们将看到这个简单的几何思想如何让我们在实验室中寻找这些对称性，如何为[从头设计](@keyword=de_novo_design|lang=zh-CN|style=Feynman)奇特新材料提供工具包，如何对量子物质的集体行为施加深远的约束，并最终揭示晶体世界与纯数学抽象领域之间令人惊叹的联系。

### 使不可见者可见：实验特征

我们如何能确定深藏在低温[恒温器](@keyword=thermostats|lang=zh-CN|style=Feynman)内的晶体，确实拥有一种涉及其[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)分数平移的对称性呢？我们无法看到原子移动，但我们可以看到它们的舞蹈对生活在它们中间的电子所产生的影响。其中一个最强大的工具就是角分辨光电子能谱，或称 ARPES。在 [ARPES](@keyword=arpes|lang=zh-CN|style=Feynman) 实验中，我们用高能[光子](@keyword=photon|lang=zh-CN|style=Feynman)照射材料，将电子敲出。通过测量这些被逐出电子的能量和角度，我们可以重构电子能带结构——即晶体内部电子的“交通规则”。

现在，想象一个具有非点式[滑移面](@keyword=slip_planes|lang=zh-CN|style=Feynman)的晶体。正如我们所学到的，这种对称性强制某些电子[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)在[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)边界处变得简并——即接触。但它做的还不止这些。在这样一个接触点，两个简并的电子态相对于滑移操作的镜面反射部分具有相反的宇称。一个态是“偶宇称”，另一个是“[奇宇称](@keyword=odd_parity|lang=zh-CN|style=Feynman)”。

ARPES 实验通常可以设置成只对其中一种宇称敏感。当我们观察这对[简并态](@keyword=degenerate_states|lang=zh-CN|style=Feynman)时会发生什么？我们会看到一个非凡的现象：其中一个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)清晰可见，而与其简并的伙伴则完全消失。就好像一对同卵双胞胎中有一个是鬼影。这种现象，被称为**[系统性消光](@keyword=systematic_extinctions|lang=zh-CN|style=Feynman)**，是底层[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)的一个直接而明确的指纹 [@problem_id:1760853]。我们不仅仅是在推断对称性；我们正在亲眼看到其“选择定则”在起作用，这是来自晶体[量子力学波函数](@keyword=quantum_mechanics_wavefunctions|lang=zh-CN|style=Feynman)的一个明确信息。

这个原理不仅限于电子。任何在晶体中传播的类波激发都必须遵守其对称性规则。在像硅这样我们熟悉的材料中（它以[金刚石结构](@keyword=diamond_structure|lang=zh-CN|style=Feynman)结晶），晶格振动本身——即[声子](@keyword=phonons|lang=zh-CN|style=Feynman)——就受一个[非点式空间群](@keyword=nonsymmorphic_space_groups|lang=zh-CN|style=Feynman)的支配。在布里渊区的某些高[对称点](@keyword=point_of_symmetry|lang=zh-CN|style=Feynman)，[声子](@keyword=phonons|lang=zh-CN|style=Feynman)分支被迫成对地“粘在一起”，展现出仅靠更简单的点式对称性无法预测的简并性 [@problem_id:1163768]。通过用中子而非[光子散射](@keyword=photon_scattering|lang=zh-CN|style=Feynman)晶体，物理学家可以绘制出这些[声子](@keyword=phonons|lang=zh-CN|style=Feynman)[能带图](@keyword=energy_band_diagram|lang=zh-CN|style=Feynman)，并再次看到简并的标志性迹象，从而证实了我们这个时代最重要材料之一的非点式特性。

### 不可能的艺术：构筑奇异物质

也许[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)最激动人心的应用在于新兴的拓扑材料领域。在这里，这些对称性从一个待发现的被动属性，转变为一个主动的设计原则——成为电子设计师工具箱中一个强大的工具，用以构筑几十年前无法想象的具有特定性质的材料。[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)使我们能够创造并保护奇特的电子物态。

#### 锚定现实：狄拉克与韦尔半金属

在某些材料中，电子的行为不像我们在入门物理学中学到的缓慢、笨重的粒子，而更像无质量的[相对论性粒子](@keyword=relativistic_particle|lang=zh-CN|style=Feynman)，以恒定速度飞驰，并遵循[保罗·狄拉克](@keyword=paul_dirac|lang=zh-CN|style=Feynman)著名方程的一个版本。能带结构中发生这种情况的地方被称为[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)——导带和价带的四重简并[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)点。

有几种方法可以创造和保护这样的点。一种方法涉及[时间反演](@keyword=time_reversal_2|lang=zh-CN|style=Feynman)和反演对称性的组合。但这种保护方式有些灵活；随着材料参数的调整，狄拉克点可以在高对称线上四处移动。[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)提供了另一种更刚性的保护。它们具有非凡的能力，可以强制狄拉克点出现，并将其**钉在**布里渊区边界上的特定高对称位置 [@problem_id:1827841]。这就像一条规则说“两条路必须在这条高速公路的某处[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)”，而另一条规则说“它们必须*恰好*在州界线处[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)”之间的区别。

其根本原因是一段优美的量子代数。例如，一个螺旋轴是旋转 $2\pi/n$ 角后再进行分数平移。当你对一个 $180^\circ$ 螺旋（$n=2$）应用这个操作两次时，你会得到一个完整的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)平移，但由于电子的自旋，会带上一个关键的负号。这导致[对称算符](@keyword=symmetric_operators|lang=zh-CN|style=Feynman) $\hat{S}_z$ 的一个代数规则，恰好在[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)边界看起来像是 $\hat{S}_z^2 = -1$。这与时间反演算符所遵循的代数相同，它保证了每个能级都必须至少是二重简并的。当与其他对称性（如反演）结合时，这可以强制产生一个稳健的四重简并——一个[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)——它无法从其高对称位置移动 [@problem_id:2870335]。[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)本身合力为其电子创造了一个受保护的、涌现的[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)性宇宙。

#### 从点到线：[节线半金属](@keyword=nodal_line_semimetals|lang=zh-CN|style=Feynman)

大自然不必止步于创造简并点。如果[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)不仅仅在一个点上接触，而是沿着一整条线接触，形成一个“节线”或环呢？处于这种材料中的电子将拥有一整个连续的态，在这些态上它们的行为如同无质量粒子。[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)是创造这种结构的主要机制。

一个常见的方案包含两个要素：[能带反转](@keyword=band_inversion|lang=zh-CN|style=Feynman)和不同的对称性标记。想象有两个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)，由于晶体的化学性质，当我们从[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)中心移动到边缘时，它们想要交换位置。现在，如果这些[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)被“标记”上不同的滑移对称性[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)，它们就不能简单地混合并相互推开（这个过程称为杂化）。就像在不同轨道上的两列火车，它们注定要[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)。滑移对称性保护了这个[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)。因为这种保护存在于[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)的一个连续区域内，所以单点的[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)延伸成一条[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)线——一个节线 [@problem_id:2806771]。在一些简单的模型中，非点式平移迫使哈密顿量中耦合[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的部分具有一种奇特的动量依赖性，比如 $\cos(k_y/2)$。这样的项在数学上*保证*在 $k_y = \pi$ 时为零——也就是恰好在布リ渊区边界处——从而精确地在对称性指定的位置刻画出[节线](@keyword=nodal_lines|lang=zh-CN|style=Feynman) [@problem_id:3007320]。

#### 晶体沙漏

[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)在视觉上最令人惊叹的后果，可以说就是“沙漏[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)”。这种现象源于[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)与所有自旋 $1/2$ 电子都遵循的时间反演对称性之间的精妙相互作用。

让我们用一个类比。把高对称点上的电子态想象成成对的舞者，由[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)（一个[克拉默斯对](@keyword=kramers_pair|lang=zh-CN|style=Feynman)）联系在一起。滑移对称性为每个舞者分配一个名牌（一个[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)）。这里的诀窍是：由于分数平移的存在，这些名牌的性质随着我们在[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)中移动而改变。

在布里渊区中心（$\Gamma$ 点），滑移对称性的规则要求一个[克拉默斯对](@keyword=kramers_pair|lang=zh-CN|style=Feynman)中的两个舞者拥有*相反*的名牌，比如 $+1$ 和 $-1$。但在布里渊区边缘（$X$ 点），同样的规则要求它们拥有*相同*的名牌，比如 $+i$ 和 $+i$。现在，假设一个在 $\Gamma$ 点以 $+1$ 名牌开始的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)必须连接到 $X$ 点的一个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。它必须连接到一个拥有 $+i$ 名牌的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。它在 $\Gamma$ 点的克拉默斯伙伴，带着 $-1$ 的名牌，必须连接到 $X$ 点一个拥有 $-i$ 名牌的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。这对伙伴被迫分开并连接到不同的态！为了使[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)保持其连续性，它们必须在中间某处[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)。这种强制的伙伴交换和随后的[能带交叉](@keyword=band_crossing|lang=zh-CN|style=Feynman)创造了一种独特的[色散](@keyword=frequency_dispersion|lang=zh-CN|style=Feynman)形状，看起来就像一个沙漏。这不是偶然；这是[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)不可避免的后果。一个只有简单镜面对称、缺乏分数平移的晶体，其名牌没有这样的规则变化，因此也没有强制的沙漏[交叉](@keyword=decussation|lang=zh-CN|style=Feynman) [@problem_id:3007255]。沙漏[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)或许是“一步一转”的对称性对量子世界施加深刻连通性的最优雅证明。

### 超越单粒子：约束集体行为

到目前为止，我们都集中在能带结构所描述的单个电子（或[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）的行为上。但[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)也对量子系统的集体、多体行为施加了强大的约束。

考虑一个由具有[半整数自旋](@keyword=half_integer_spin|lang=zh-CN|style=Feynman)的原子组成的磁体。根据一个被称为 Lieb-Schultz-Mattis (LSM) 定理的强大定理，这样的系统在某些一般条件下，不能稳定在一个简单、平庸、有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。它的构造决定了它不能是平庸的。当一个非点式滑移对称性被加入其中时，这个定理变得更具规定性。系统不仅必须是奇特的和无能隙的，而且[无能](@keyword=anergy|lang=zh-CN|style=Feynman)隙的激发被钉在了布里渊区的特定角落，例如 $(\pi/a, \pi/a)$ 点 [@problem_id:1165095]。晶体几何深入到复杂的量子[多体相互作用](@keyword=many_body_interaction|lang=zh-CN|style=Feynman)世界，并指定了有趣的行为必须发生在哪里。这为寻找像[量子自旋液体](@keyword=quantum_spin_liquids|lang=zh-CN|style=Feynman)这样的奇特物相提供了强大的指导原则，这些[物相](@keyword=phases_of_matter|lang=zh-CN|style=Feynman)可能成为未来[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的基础。

### 通往抽象数学的桥梁：[群上同调](@keyword=group_cohomology|lang=zh-CN|style=Feynman)的语言

在最深的层次上，点式和[非点式空间群](@keyword=nonsymmorphic_space_groups|lang=zh-CN|style=Feynman)之间的区别不仅仅是物理上的，更是一个深刻的数学区别，将[晶体学](@keyword=crystallography|lang=zh-CN|style=Feynman)与群论的抽象领域联系起来。

一个空间群 $G$ 可以被看作是由两个更小的群构建而成的：平移群 $T$（无限的步进[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)）和点群 $P$（围绕一个点的旋转和反射集合）。一个点式群是组合它们的最简单方式，称为半直积。这就像拥有一组都共享一个共同原点的[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性。

然而，一个[非点式群](@keyword=nonsymmorphic_groups|lang=zh-CN|style=Feynman)代表了一种更“扭曲”或“纠缠”的方式来组合平移和点群操作。没有一个单一的点在所有的旋转和反射下都保持不变。用来分类所有可能扭曲两个群的方式的数学工具被称为**[群上同调](@keyword=group_cohomology|lang=zh-CN|style=Feynman)**。对于给定的[晶格和](@keyword=lattice_sums|lang=zh-CN|style=Feynman)点群，所有不同空间群的集合由“[第二上同调群](@keyword=second_cohomology_group|lang=zh-CN|style=Feynman)”分类，记为 $H^2(P, T)$。

在这种语言中，点式空间群对应于这个上同调群的平庸、无趣的元素——“零”元素。所有[非点式群](@keyword=nonsymmorphic_groups|lang=zh-CN|style=Feynman)则对应于非零、非平庸的元素 [@problem_id:780329]。例如，对于[点群](@keyword=point_groups|lang=zh-CN|style=Feynman) $D_6$（六边形的对称性），相关的[上同调群](@keyword=cohomology_groups|lang=zh-CN|style=Feynman)是[循环群](@keyword=cyclic_groups|lang=zh-CN|style=Feynman) $\mathbb{Z}_6$，它有六个元素：$\{0, 1, 2, 3, 4, 5\}$。这意味着有六种根本不同的方式来构建具有这种对称性的[空间群](@keyword=space_groups|lang=zh-CN|style=Feynman)。'0' 元素对应于点式群 $P622$。五个非零元素对应于包含螺旋轴的五个[非点式群](@keyword=nonsymmorphic_groups|lang=zh-CN|style=Feynman)，如 $P6_122$、$P6_222$ 等等。[空间群](@keyword=space_groups|lang=zh-CN|style=Feynman) $P6_k22$ 直接对应于 $\mathbb{Z}_6$ 中的元素 $k$。这提供了一个极其深刻而优雅的分类，揭示了支撑[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)多样性的隐藏数学骨架。

始于对晶体图样的简单观察，最终与现[代数学](@keyword=algebra|lang=zh-CN|style=Feynman)的一些优美结构相联系。从 [ARPES](@keyword=arpes|lang=zh-CN|style=Feynman) 测量中一个缺失的斑点到[群扩张](@keyword=group_extensions|lang=zh-CN|style=Feynman)的分类，[非点式对称性](@keyword=nonsymmorphic_symmetry|lang=zh-CN|style=Feynman)的旅程一次又一次地揭示了科学思想中非凡且常常出人意料的统一性。