## 引言
是什么将[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)束缚在一起？这个致密而微小的质子和中[子集](@keyword=subset|lang=zh-CN|style=Feynman)合体，受制于一种复杂的力相互作用，难以轻易解释。为了揭开这个谜团，物理学家们发展出一个强有力的类比：将[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)视为一滴微小的液体。这个简单而深刻的概念，被称为液滴模型，构成了[贝特-魏茨泽克公式](@keyword=bethe_weizsäcker_formula|lang=zh-CN|style=Feynman)的基础，这是一个用于计算束缚[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)能量的[半经验方法](@keyword=semiempirical_methods|lang=zh-CN|style=Feynman)。本文将引导您了解核物理学中这一里程碑式的成就。在第一章“原理与机制”中，我们将逐一解构该公式，揭示每一项背后的物理意义。随后，在“应用与跨学科联系”中，我们将探索这个单一方程如何描绘核稳定性的图景，解释恒星的能量，并与天体物理学、化学等领域建立联系。

## 原理与机制

想象一下，你想要理解一个你看不见的东西，它的内部运作由我们日常经验中完全不同的力所主宰。这就是[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)所带来的挑战。它是一个微小、密度高得难以想象的质子和中子束。是什么将它束缚在一起？又是什么决定了它的稳定性，乃至它的存在本身？要回答这些问题，我们不从完整、极其复杂的[量子色动力学](@keyword=quantum_chromodynamics|lang=zh-CN|style=Feynman)理论入手。相反，我们采取物理学家们热衷的方式：我们做一个类比。我们从一幅图景开始。

### [原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)如液滴：一个奇特的类比

让我们想象[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)是一滴微小的液体。这听起来似乎是个奇怪的想法，但它出人意料地强大。一滴水是分子的集合，由短程的吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)维系在一起。它们拉动着自己最近的邻居，这种内聚力赋予了液滴完整性和其特有的球形形状——即在给定体积下使表面积最小化的形状。

[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)也是粒子的集合——质子和中子，统称为**[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)**。它们同样被一种短程的吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)维系在一起：**强核力**。这种力极其强大，但只在极小的距离内起作用，基本上只作用于一个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)与其紧邻的[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)之间。就像水分子一样，[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)们尽可能紧密地挤在一起，形成一种密度几乎恒定的“核液体”。这个简单而优美的类比，被称为**液滴模型**，是我们构建核物理学中最成功的公式之一的起点：**[贝特-魏茨泽克公式](@keyword=bethe_weizsäcker_formula|lang=zh-CN|style=Feynman)**，或称**[半经验质量公式](@keyword=semi_empirical_mass_formula|lang=zh-CN|style=Feynman)（SEMF）**。它是一个计算任何[原子核结合能](@keyword=nuclear_binding_energy|lang=zh-CN|style=Feynman)的配方，也就是将[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)维系在一起的能量。让我们一步步构建它。

### 逐项构建公式

**结合能**，用$B(A,Z)$表示，是将一个质量数为$A$（总[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)数）、原子序数为$Z$（质子数）的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)分解为其独立的质子和中子所需要提供的能量。[结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)越高，意味着[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)越稳定。我们的公式将是几项之和，每一项代表一种不同的物理效应。

#### 体积效应（体积能）

对结合能的主要贡献来自于[强核力](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)将每个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)拉向其邻居。因为这种力是“饱和的”——意味着每个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)只与其固定数量的最近邻相互作用——核液滴内部的每个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)贡献的结合能大致相同。因此，作为一阶近似，总[结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)应简单地与总[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)数$A$成正比。这就是我们的**体积项**：

$$ E_v = a_v A $$

在这里，$a_v$是一个正常数，一个经验系数，代表了理想化、无限“核物质”中每个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的结合能。这一项是[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的基础“胶水”，是它存在的主要原因。[@problem_id:2921679] [@problem_id:2919548]

#### “不愉快”的表面（表面能）

我们的体积项假设每个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)都被完全包围，但对于那些位于表面的[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)来说，情况并非如此。就像人群边缘的人一样，表面[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)相互作用的邻居更少。它比内部的[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)束缚得更松散。这降低了总结合能。这种效应必然与[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的表面积成正比。

如果我们假设核液体具有恒定密度，其体积与[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)数$A$成正比。球体的体积是$\frac{4}{3}\pi R^3$，所以半径$R$必须与$A^{1/3}$成正比。表面积$4\pi R^2$则必须与$(A^{1/3})^2 = A^{2/3}$成正比。这给了我们第二项，即**表面项**，它是一个负修正：

$$ E_s = -a_s A^{2/3} $$

系数$a_s$是另一个正常数。对于非常小的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)，很大一部分[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)位于表面，因此这一项非常重要。对于大的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)，体积项（$A$）主导了表面项（$A^{2/3}$），就像宏观的水滴一样。[@problem_id:1896937]

#### 质子间的“不和”（[库仑能](@keyword=coulomb_energy|lang=zh-CN|style=Feynman)）

到目前为止，我们只考虑了吸引性的强核力。但[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)中也包含质子，它们都带正电。正如你所知，同种[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)相互排斥。这种静电排斥力作用距离很长，每个质子都会推开其他所有质子。这与强核力相抗衡，降低了结合能。

一个均匀带电球体的势能与其总[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的平方成正比，并与其半径成反比，即$Q^2/R$。对于[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)，总[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)是$Q=Ze$（其中$e$是元[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)），半径$R \propto A^{1/3}$。因此，我们期望排斥能与$Z^2 / A^{1/3}$成正比。更仔细地计算所有不同质子对之间的相互作用，会得到一个因子$Z(Z-1)$而不是$Z^2$，因为质子不排斥自己。这给了我们**库仑项**：

$$ E_c = -a_c \frac{Z(Z-1)}{A^{1/3}} $$

系数$a_c$不仅仅是一个随机数；它可以根据静电学定律计算出来。它与元[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)和[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的基本尺寸参数直接相关。这在经验公式和基础物理学之间提供了一个美妙的联系。[@problem_id:398517]

与表面效应不同，[库仑排斥](@keyword=coulomb_repulsion|lang=zh-CN|style=Feynman)随着[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)变大而变得更具破坏性。随着$A$的增长，$Z$也趋于增长（在一段时间内大约为$A/2$）。[库仑排斥](@keyword=coulomb_repulsion|lang=zh-CN|style=Feynman)力，其尺度大致为$A^{5/3}$，最终增长速度超过了内聚的体积项（尺度为$A$）。质子之间的这种内部“不和”最终限制了稳定[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的大小，并为元素周期表画上了句号。[@problem_id:1896937]

### 量子修正：液滴变得“怪异”

经典的液滴模型是一幅强有力的图景，但[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)是量子粒子。它们是**[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)**，并遵循量子力学中奇特而美妙的规则。我们需要在公式中加入几个量子修正。

#### 不平衡的代价（[不对称能](@keyword=asymmetry_energy|lang=zh-CN|style=Feynman)）

想象你有两个盒子，一个放红球（质子），一个放蓝球（中子）。**[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)**指出，没有两个相同的[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)可以占据同一个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。这就像说你只能在盒子的每个“架子”上放一个球，而且这些架子处于不同的能量高度。要添加更多相同颜色的球，你必须将它们放在越来越高的架子上，从而增加总能量。

对于固定的总[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)数$A$，当质子和中子数量大致相等（$N \approx Z$）时，可以达到最低的总能量状态，此时质子和中子“盒子”被填充到相同的能级。如果你有很大的不平衡——比如说，中子比质子多得多——你将被迫把那些额外的中子放在非常高的能级上，这会耗费大量能量。这降低了整体结合能。这种能量惩罚被称为**[不对称能](@keyword=asymmetry_energy|lang=zh-CN|style=Feynman)**，它与中子超额数的平方$(N-Z)^2$成正比，与[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的体积$A$成反比。这给了我们第四项：

$$ E_a = -a_a \frac{(A-2Z)^2}{A} $$

在这里，我们使用了$N-Z = (A-Z)-Z = A-2Z$。这一项纯粹是量子力学的，它解释了为什么轻的稳定[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)有$N \approx Z$。在核的层面上，宇宙偏爱平衡。[@problem_id:2921679] [@problem_id:2948185]

#### “伙伴”系统（对能）

还有一个最后、微妙的量子效应。[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)有自旋，它们喜欢形成配对。一个质子会与另一个自旋相反的质子形成一个能量上有利的配对，一个中子也会与另一个中子这样做。这种“[伙伴系统](@keyword=buddy_system|lang=zh-CN|style=Feynman)”导致结合能略微增加。
*   如果一个[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)有偶数个质子和偶数个中子（**偶偶核**），所有的[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)都可以配对。这些[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)异常稳定。
*   如果它有奇数个质子和奇数个中子（**奇奇核**），将会有一个“孤独”的质子和一个“孤独”的中子。这些[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)通常不太稳定。
*   如果总[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)数$A$是奇数（**奇A核**），将会有一个未配对的[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)，但效应不那么显著。

我们添加一个小的**对能项**$\delta(A,Z)$来解释这一点。对于偶偶核，它是结合能的一个小奖励；对于奇奇核，它是一个惩罚；对于奇A核，它是零。随着[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)变大，这一项的大小会减小。[@problem_id:3568185]

### 综合应用：一个稳定性的公式

现在我们有了完整的[半经验质量公式](@keyword=semi_empirical_mass_formula|lang=zh-CN|style=Feynman)，用于计算[结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)$B(A,Z)$：

$$ B(A,Z) \approx a_v A - a_s A^{2/3} - a_c \frac{Z(Z-1)}{A^{1/3}} - a_a \frac{(A-2Z)^2}{A} + \delta(A,Z) $$

这个方程是物理直觉的胜利。它是“半经验的”，因为每一项的形式都来自一个物理模型（液滴模型、量子统计），但系数（$a_v, a_s, a_c, a_a$以及对能项的系数）是通过将公式与实验测量的核质量进行拟合来微调的。它将理论与实验融合成一个具有非凡预测能力的工具。[@problem_id:2921679] 我们可以用它做什么呢？

#### [稳定谷](@keyword=valley_of_stability|lang=zh-CN|style=Feynman)

对于任意给定的总[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)数$A$，质子和中子的最稳定组合是什么？我们可以通过将公式视为固定$A$下$Z$的函数，并找到使[结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)最大化的$Z$值来求解。当你进行数学计算时，你会发现当你改变$Z$时，[结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)描绘出一条开口向下的抛物线。这条抛物线的顶点$Z^{\star}$代表了该质量数下最稳定的质子数。[@problem_id:2919495] [@problem_id:2919499]

这在所有已知[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的图谱上定义了一个“[β稳定谷](@keyword=valley_of_beta_stability_2|lang=zh-CN|style=Feynman)”。
*   对于[轻核](@keyword=light_nuclei|lang=zh-CN|style=Feynman)，不对称项（$E_a$）是形状的主要驱动因素，因此最稳定的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)具有$Z \approx N \approx A/2$。
*   对于重核，库仑项（$E_c$）成为一个主要角色。为了最小化其排斥效应，[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)倾向于拥有更少的质子和更多的中子。因此，[稳定谷](@keyword=valley_of_stability|lang=zh-CN|style=Feynman)从$N=Z$线向富中子同位素方向弯曲。[@problem-id:2948185]

位于这个谷两侧的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)是不稳定的。它们会自发地进行β衰变，将一个中子变成一个质子，或反之，以便向谷底移动，达到一个更稳定的构型。我们的公式完美地解释了核存在的图景。

#### [结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)的峰值与恒星的秘密

也许该公式最深刻的预测来自于绘制**比结合能**（每个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的[结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)）$B/A$与[质量数](@keyword=mass_number|lang=zh-CN|style=Feynman)$A$的关系图。
*   对于[轻核](@keyword=light_nuclei|lang=zh-CN|style=Feynman)，$B/A$随$A$增加而增加。这是因为[表面积与体积之比](@keyword=surface_area_to_volume_ratio|lang=zh-CN|style=Feynman)较大，增加更多的[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)使[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)更像“块体”，减少了每个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的表面惩罚。
*   对于非常重的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)，$B/A$随$A$增加而减小。这是由于库仑排斥力的不断增加，最终开始压倒[强核力](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)的内聚力。

结果是一条先上升、达到峰值，然后缓慢下降的曲线。峰值出现在[质量数](@keyword=mass_number|lang=zh-CN|style=Feynman)$A \approx 56-62$附近，像铁（$^{56}\mathrm{Fe}$）和镍这样的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)是宇宙中束缚最紧密的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)之一。[@problem_id:3711739]

这条单一的曲线解释了恒星和核电站的能量来源。只要你能增加结合能，能量就会被释放。通过将[轻核](@keyword=light_nuclei|lang=zh-CN|style=Feynman)（如氢）聚变成更重的核（如氦），你沿着曲线的左侧向上攀升，释放出巨大的能量。这就是**聚变**，恒星的引擎。通过将非常重的核（如铀）分裂成更轻的碎片，你从曲线的右侧向峰值方向移动，同样释放能量。这就是**裂变**。整个核能的宇宙大戏都写在这条曲线的形状中，一个由我们公式中各项的推拉作用所决定的形状。

### 超越液滴模型：知识的前沿

液滴模型是最终的定论吗？当然不是。它是一个模型，而所有模型都有其局限性。它在描述[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的平滑、平均性质方面做得非常出色。但它无法解释某些细节。例如，观测到质子或中子数为“幻数”（2, 8, 20, 28, 50, 82, 126）的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)异常稳定，远超平滑公式的预测。

这些偏差被称为**壳层效应**，它们源于[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)详细的[量子壳层结构](@keyword=quantum_shell_structure|lang=zh-CN|style=Feynman)，类似于原子中的电子壳层。[半经验质量公式](@keyword=semi_empirical_mass_formula|lang=zh-CN|style=Feynman)为我们提供了完美的宏观基线，是这幅画的粗略笔触。现代核物理学家则利用这个基线，应用更先进的理论——甚至是复杂的机器学习算法——来预测叠加于其上的微观、[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的[壳层修正](@keyword=shell_correction|lang=zh-CN|style=Feynman)。[@problem_id:3568185] 通过研究公式的预测对其系数的微小变化的敏感性，科学家们还可以探究哪些物理效应对处于存在边缘的奇异[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)最为重要。[@problem_id:2921668]

始于一个简单的液滴类比的旅程，带我们穿越了[经典物理学](@keyword=classical_physics|lang=zh-CN|style=Feynman)和量子力学，解释了[物质的稳定性](@keyword=stability_of_matter|lang=zh-CN|style=Feynman)、太阳的能量，并将我们带到了现代研究的前沿。这是一个完美的例子，说明在科学中，一个简单、直观的想法，经过精心发展，可以揭示宇宙最深的秘密。

