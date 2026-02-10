## 应用与跨学科联系

在我们之前的讨论中，我们找到了一种极其简单的方法来描述固体如何变形。我们抛弃了所有复杂的非线性项，得到了微[应变[张](@keyword=strain_tensor|lang=zh-CN|style=Feynman)量](@article_id:321604) $\boldsymbol{\varepsilon}$。该[张量](@keyword=tensor|lang=zh-CN|style=Feynman)将局部变形与材料[质点](@keyword=point_mass|lang=zh-CN|style=Feynman)的位移线性地联系起来，但前提是必须满足一个关键条件：变形必须*小*。这不仅意味着微小的拉伸或压缩，也意味着微小的转动。

一个合理的问题是：这样一个限制性强的小工具有什么用？现实世界中充满了各种大尺度、复杂的弯曲、扭转和运动。我们的“[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)”仅仅是物理学家的一个巧妙花招，一个只存在于黑板上的概念吗？答案是响亮的*“不”*，我们将在本章探讨这一点。事实证明，这个简单的概念是所有工程和物理科学中最强大、影响最深远的概念之一。它是我们构建世界（从桥梁、飞机到设计它们的[计算机模拟](@keyword=computer_simulation|lang=zh-CN|style=Feynman)）的基石，甚至让我们能够窥探物质的原子核心。让我们开始探索它广阔而惊人的领域。

### 工程师的工具箱：设计我们周围的世界

看看任何宏伟的结构——摩天大楼、悬索桥、飞机机翼。它在风、重力和成千上万种其他力的作用下屹立不倒。工程师们是如何充满信心地设计出这些东西的？很大程度上，这要归功于[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)理论的推论。

考虑一根简单的梁，这是[结构工程](@keyword=structural_engineering|lang=zh-CN|style=Feynman)中最基本的构件。当你在上面施加载荷时，它会弯曲。顶面受压，底面受拉。在中间某处，必定有一条既不压缩也不拉伸的线：中性轴。梁的厚度方向上的应变分布是怎样的？有人可能会猜测这是一个复杂的事情，取决于材料的属性——无论是钢、木材还是混凝土。但美妙的事实是，并非如此。

如果我们做出一个简单而优雅的假设，这也是[梁理论](@keyword=beam_theory|lang=zh-CN|style=Feynman)的基石——即梁的[横截面](@keyword=cross_section|lang=zh-CN|style=Feynman)在弯曲前是平的，弯曲后仍然保持平的——一个纯粹由变形几何学得出的非凡结果便应运而生。在距离梁中性轴为 $y$ 处，[轴向应变](@keyword=axial_strain|lang=zh-CN|style=Feynman) $\varepsilon_x$ 由一个极为简单的线性关系给出：

$$
\varepsilon_x(y) = -\kappa y
$$

其中 $\kappa$ 是弯曲梁的曲率。就是这样。这种线性应变分布纯粹是[运动学](@keyword=kinematics|lang=zh-CN|style=Feynman)的结果。它与材料的性质无关！由这种应变产生的应力当然会依赖于材料。钢抵抗这种应变的能力比橡胶强得多。但是变形本身的模式保持不变。令人惊讶的是，即使梁的部分区域开始发生永久变形——即所谓的塑性——这种线性应变剖面仍然成立。只要[总曲率](@keyword=total_curvature|lang=zh-CN|style=Feynman)没有极端到违反“小变形”几何假设，[横截面](@keyword=cross_section|lang=zh-CN|style=Feynman)上的应变就固执地保持线性。这个单一、简单的结果是现代世界几乎所有承重结构设计的出发点。

### 数字孪生：在现实发生前进行模拟

在过去，要测试汽车或飞机的新设计，你必须把它造出来。如果失败了，你还得再造一个。今天，我们在计算机内部构建虚拟原型——“数字孪生”——并对其施加模拟的力。这场革命是由一种称为**[有限元法 (FEM)](@keyword=finite_element_method_(fem)|lang=zh-CN|style=Feynman)** 的技术实现的，而其核心正是微应变[张量](@keyword=tensor|lang=zh-CN|style=Feynman)。

[有限元法](@keyword=finite_element_method|lang=zh-CN|style=Feynman)的思想是，将一个复杂的形状分解成大量简单的小形状或“单元”，就像马赛克一样。然后将物理定律应用于每个微小的单元。但是我们如何以计算机能理解的方式来表述这些定律呢？我们使用物理学中一个深刻的概念，称为**[虚功原理](@keyword=principle_of_virtual_work|lang=zh-CN|style=Feynman)**。

想象一个处于完美平衡状态的结构。如果你给它一个微小的、物理上可能但假想的“虚”推动，所有力——外力和内力——所做的总功必须为零。内功，即材料内部应力所做的功，是通过将应力乘以*虚应变*在物体体积上积分来计算的。而这个虚应变是什么？它正是由我们的[虚位移](@keyword=virtual_displacement|lang=zh-CN|style=Feynman)场产生的[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)，$\delta\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \delta\mathbf{u} + (\nabla \delta\mathbf{u})^T)$。

所以，我们简单的应变度量是让计算机能够检查复杂结构平衡状态的关键要素。每当你看到一个彩色的工程模拟图，显示新机器零件中的应力分布时，你看到的都是用[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)数学绘制的画面。

### 线性的局限：一句警示

至此，你可能认为我们的小[张量](@keyword=tensor|lang=zh-CN|style=Feynman)无所不能。但一个好的科学家，就像一个好的工匠，知道他们工具的局限性。[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)理论的力量来自其假设，而正是通过理解这些假设，我们才能真正掌握它。关键的假设是[位移梯度](@keyword=displacement_gradient|lang=zh-CN|style=Feynman) $\nabla\mathbf{u}$ 很小。这意味着两件事：应变很小，*并且*转动很小。

如果转动变大，即使应变保持很小，会发生什么？

拿一把薄塑料尺或钢卷尺。你可以轻易地将它弯成一个大弧形，甚至一个完整的圆。挠度是巨大的，尺上各段的转动也绝不小。然而，材料本身几乎没有拉伸。真实的应变非常微小。如果你试图将[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)理论应用于这个问题，你会得到一个荒谬的答案。它会预测尺子仅仅因为被旋转就经历了压缩应变，这在物理上是荒谬的。纯[刚体转动](@keyword=rigid_body_rotation_2|lang=zh-CN|style=Feynman)应该产生零应变。[Green-Lagrange应变张量](@keyword=green_lagrange_strain_tensor|lang=zh-CN|style=Feynman)，我们上一章提到的那个更复杂的非线性朋友，能正确地给出零应变。而微[应变[张](@keyword=strain_tensor|lang=zh-CN|style=Feynman)量](@article_id:321604)则不能。

线性理论的这种失效不仅仅是一个数学上的奇特现象；它对后处理有限元软件的结果具有深远的实际意义。如果工程师对一个涉及大转动的问题（比如一个非常柔性结构的弯曲）使用标准的线性模拟，软件将计算出虚假的、非物理的应力。这是粗心大意者常掉入的典型陷阱。它教给我们一个至关重要的教训：“小应变”的世界与“小[位移梯度](@keyword=displacement_gradient|lang=zh-CN|style=Feynman)”的世界并不相同。对于涉及大转动的问题，我们必须放弃我们简单的线性运动学，进入**[几何非线性](@keyword=geometric_nonlinearity|lang=zh-CN|style=Feynman)**的领域，在那里我们有选择地重新引入一些我们曾愉快丢弃的二次项。

### 材料交响曲：从聚合物到金属

到目前为止，我们大多将固体想象成简单的弹性弹簧。但材料世界远比这更丰富、更复杂。在这里，微应V变也为描述它们的行为提供了基本语言。

考虑**粘弹性**材料，如聚合物、生物组织，甚至[地质时间尺度](@keyword=geologic_timescale|lang=zh-CN|style=Feynman)上的地幔。它们的响应取决于时间。拉一根橡皮筋，它会弹回，但拉一块彩色橡皮泥，它会流动。[线性粘弹性](@keyword=linear_viscoelasticity|lang=zh-CN|style=Feynman)理论通过将当前应力视为对整个应变*历史*的响应来捕捉这一点。这个被称为**[Boltzmann叠加原理](@keyword=boltzmann_superposition_principle|lang=zh-CN|style=Feynman)**的杰出洞见，是将时间 $t$ 的应力表示为在所有过去时间 $\tau$ 上应变率的积分。该积分由一个材料函数——松弛模量——加权，该函数描述了过去应变的记忆如何随时间“消退”。这个优雅而强大的理论是现代聚合物科学的基础，它完全是在[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)的框架内建立的。

$$
\sigma(t)=\int_{0}^{t} E(t-\tau)\,\frac{d\varepsilon(\tau)}{d\tau}\,d\tau
$$

那么对于可以永久变形的材料，比如一块金属，又该如何处理？当你弯曲一个回形针时，它不会完全弹回。这就是**塑性**。为了描述这一点，我们必须区分变形中可恢复的（弹性）[部分和](@keyword=partial_sums|lang=zh-CN|style=Feynman)永久的（塑性）部分。在小应变的世界里，这是通过一个极其简单的技巧完成的：我们只需假设总[应变张量](@keyword=strain_tensor|lang=zh-CN|style=Feynman)可以分解为两部分相加：

$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{e} + \boldsymbol{\varepsilon}^{p}
$$

这里，$\boldsymbol{\varepsilon}^e$ 是卸载后会消失的弹性应变，而 $\boldsymbol{\varepsilon}^p$ 是会保留下来的塑性应变。这种“加和分解”是整个小应变塑性领域的概念起点，该理论使我们能够模拟从金属锻造过程到极端载荷下结构安全分析的一切。

### 地球呼吸与晶体歌唱：隐藏的世界

[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)的[影响范围](@keyword=range_of_influence|lang=zh-CN|style=Feynman)延伸到了初看起来与力学关系不大的领域。

当一栋重型建筑建在湿粘土上时，地基会随时间沉降。当从砂岩中开采石油时，岩石会压实。这个过程称为**固结**，它由固体地球与其孔隙中流体之间微妙的相互作用所控制。当固体骨架被压缩时，孔隙流体（通常是水）的压力上升。这种高压流体慢慢渗出，使得骨架能够进一步压实。

是什么将固体力学与流体流动联系起来的？是固体骨架体积的变化率，它由微应变[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的迹给出，$\varepsilon_v = \text{tr}(\boldsymbol{\varepsilon})$。固体体积变化率 $\dot{\varepsilon}_v$ 决定了流体被挤出的速率。因此，我们简单的应变张量在岩[土力学](@keyword=soil_mechanics|lang=zh-CN|style=Feynman)和油藏工程中扮演着关键角色，帮助我们预测地面沉降和管理自然资源。

也许最令人惊叹的应用来自固态物理学领域。我们如何能确定我们计算的这些应变是真实的？我们能*看见*它们吗？答案是肯定的，通过**[X射线衍射 (XRD)](@keyword=x_ray_diffraction_(xrd)|lang=zh-CN|style=Feynman)**。晶体是原子整齐、重复的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。这种周期性结构对[X射线](@keyword=x_ray|lang=zh-CN|style=Feynman)来说就像一个[衍射光栅](@keyword=diffraction_grating|lang=zh-CN|style=Feynman)。衍射光束的图案是晶体“倒易晶格”的图谱，它是其实际空间原子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的傅里叶变换。

现在，如果我们对晶体施加一个小的应变 $\boldsymbol{\varepsilon}$ 会发生什么？实际空间的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)会变形。作为一个直接的数学结果，倒易晶格也会以一种精确可预测的方式变形。未变形晶体中的一个[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)向量 $\mathbf{G}$ 在应变晶体中会变成一个新的向量 $\mathbf{G}'$，[一阶近似](@keyword=first_order_approximation|lang=zh-CN|style=Feynman)下由下式给出：

$$
\mathbf{G}' \approx (\mathbf{I} - \boldsymbol{\varepsilon}) \mathbf{G}
$$

因为衍射斑点的位置是由这些倒易向量决定的，所以晶体上的应变会导致斑点在探测器上的位置*移动*。通过测量这种移动，物理学家和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)家可以反向推导出晶体内部的微应变[张量](@keyword=tensor|lang=zh-CN|style=Feynman)，其精度极高。这项技术使我们能够测量焊接接头中的[残余应力](@keyword=residual_stress|lang=zh-CN|style=Feynman)，观察微观缺陷周围的应变场，并探测新材料的基本力学性能。它是通向原子尺度力学世界的一扇直接窗口，所有这一切都是通过[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)的镜头来解读的。

从桥梁和梁的可见世界，到晶体中原子无形的舞蹈，[微应变](@keyword=microstrain|lang=zh-CN|style=Feynman)的概念证明了它是一个不可或缺的工具。它印证了物理学家的信条：找到一个好的近似，理解它的局限，它将为你解锁一个充满洞见的宇宙。