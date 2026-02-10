## 引言
从[喷气发动机](@keyword=jet_engine|lang=zh-CN|style=Feynman)强劲的尾气到室内空气的轻柔循环，[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)是自然界和技术中一种无处不在且功能强大的现象。与有序、可预测的层流射流不同，[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)的特点是混沌运动和非凡的混合能力。这种能力使其在无数应用中不可或缺，但同时也给试图预测和控制其行为的物理学家和工程师带来了巨大挑战。本文旨在通过揭示[湍流圆形射流](@keyword=turbulent_round_jets|lang=zh-CN|style=Feynman)的物理奥秘来应对这一挑战。第一章“原理与机制”将深入探讨[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)、卷吸和[自相似性](@keyword=self_similarity|lang=zh-CN|style=Feynman)的核心概念，解释支配这些射流如何扩展和速度衰减的普适定律。在此基础上，第二章“应用与跨学科联系”将探讨这些原理在化学工程、传热学到[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)等不同领域的实际影响，展示[流体动力学](@keyword=hydrodynamics|lang=zh-CN|style=Feynman)的基础知识如何转化为现实世界的创新。

## 原理与机制

想象一下，你站在一个平静的湖边打水漂。一瞬间，一股细而光滑的水流射向空中，几乎没有扰动水面就落了回去。现在，想象一根强力消防水龙带向同一个湖中喷射洪流。它不只是推开水；它猛烈地搅动湖水，形成一个混乱、扩张的泡沫水锥，向四面八方[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)。前者类似于**层流射流**，有序且可预测。后者则是**[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)**，一种混乱的产物，也是混合的奇迹。这两者之间深层次的区别是什么？又是什么优美而普适的定律在支配这种混乱呢？

### 混合的引擎：[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)与卷吸

[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)的决定性特征是其与周围流体惊人的混合能力。如果你将一股乙二醇以低速射入一个装有相同流体的水箱中，你会形成一股层流射流。它的边界是光滑的，它会像一根针一样穿透水箱，混合得很少。它缓慢扩展的角度将严重依赖于其速度和尺寸——具体来说，它与**雷诺数**成反比，[雷诺数](@keyword=reynolds_number|lang=zh-CN|style=Feynman)是衡量流动惯性与其粘性相对大小的指标。增加速度，[层流](@keyword=laminar_flow|lang=zh-CN|style=Feynman)射流相对于其动量实际上会变得*更细*。

但[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)的行为完全不同。一旦雷诺数足够高，流动就会发生戏剧性的转变。射流的边界变得不稳定，并爆发出一连串旋转的涡团。这股[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)的扩展角突然变成一个近似常数，完全独立于[雷诺数](@keyword=reynolds_number|lang=zh-CN|style=Feynman)[@problem_id:1768121]。一旦形成，一股[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)将以大致相同的角度扩展，无论其出口速度是10米/秒还是100米/秒。这种稳健的、恒定角度的扩展是[充分发展湍流](@keyword=developed_turbulence|lang=zh-CN|style=Feynman)的标志，也是它在从喷气发动机到工业混合器等各种应用中如此有效的秘诀。

这种变革性的[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)从何而来？它并非源于喷嘴本身，而是源于射流与其周围环境的相互作用。与管道中由壁面摩擦产生的[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)不同，射流是一种“自由”[剪切流](@keyword=shear_flow|lang=zh-CN|style=Feynman)。[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)诞生于射流边缘不稳定的[剪切层](@keyword=shear_layer|lang=zh-CN|style=Feynman)，那里来自射流的[高速流](@keyword=high_speed_flow|lang=zh-CN|style=Feynman)体与静止的环境流体发生摩擦。这种强烈的速度差是滋生不稳定的温床，它会催生出作为[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)过程核心的大涡团[@problem_id:1766427]。这些涡团反过来又做了一件了不起的事：它们主动伸出手，抓住静止的流体团块，将它们拉入射流的主体。这个过程被称为**卷吸**。射流实际上吞噬了它周围的流体，导致其质量和体积在向下游传播时不断增长。这种卷吸并非一个被动过程；它正是驱动射流扩展的引擎。

### 射流的遗忘特性：自相似性与[普适标度律](@keyword=universal_scaling_laws|lang=zh-CN|style=Feynman)

物理学中最深刻、最美丽的思想之一是，复杂系统在适当的条件下，可以忘记其起源的混乱细节，并稳定到一个简单、普适的状态。[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)就是这方面的一个完美例子。在离其产生点几十个直径远的地方，射流进入一个“[远场](@keyword=far_zone|lang=zh-CN|style=Feynman)”区域，在那里它达到了**自相似**状态。

在这种状态下，射流已经忘记了它是来自圆形喷嘴、锐边孔还是其他某种复杂的孔口。它也忘记了它在出口处的具体速度分布。它唯一“记住”的是它在开始时获得的总推力——它的初始**动量通量** $J$。这是动量注入系统的速率，由于没有外力作用于射流（在静止环境中），这个量是守恒的。

自相似性在视觉上意味着什么？它意味着射流[横截面](@keyword=cross_section|lang=zh-CN|style=Feynman)上的速度分布形状总是一样的，通常是一条[钟形曲线](@keyword=bell_curve|lang=zh-CN|style=Feynman)。当你向下游移动时，这个分布的形状不会改变；它只是变得更宽、更矮。射流的宽度 $b$ 增加，其在中心线上的最大速度（$u_{cl}$）衰减。

它是如何衰减的？我们可以通过一个非常简单的量纲分析论证来解决这个问题[@problem_id:1768139]。在远场中，中心线速度 $u_{cl}$ 可能依赖于哪些物理量？它不能依赖于喷嘴直径，因为射流已经忘记了它。它不能依赖于粘度，因为涡团的混沌混合完全压倒了分子摩擦的温和效应。唯一重要的是初始推力（[动量通量](@keyword=momentum_flux|lang=zh-CN|style=Feynman) $J$，单位为力或 $[M L T^{-2}]$）、流体密度（$\rho$，单位为 $[M L^{-3}]$）以及你离源头的距离（$x$，单位为 $[L]$）。你如何组合这三个量来得到一个速度（$[L T^{-1}]$）？唯一可能的组合是：

$$ u_{cl} \propto \sqrt{\frac{J}{\rho}} \frac{1}{x} $$

这是一个了不起的结果！[湍流圆形射流](@keyword=turbulent_round_jets|lang=zh-CN|style=Feynman)的中心线速度必须与其源头距离成反比衰减。距离加倍，速度减半。这个简单的 $1/x$ 衰减定律是所有此类射流的一个普适特征。这种标度律背后的物理原因是动量通量的守恒[@problem_id:563954]。总动量通量与 $\rho u^2 A$ 成正比，其中 $A$ 是射流的横截面积。由于射流的宽度随距离线性增长（$b \propto x$），其面积随距离的平方增长（$A \propto x^2$）。为了使[动量通量](@keyword=momentum_flux|lang=zh-CN|style=Feynman) $J \propto \rho u_{cl}^2 x^2$ 保持恒定，中心线速度必须按 $u_{cl} \propto 1/x$ 的比例变化。这两种效应完美地平衡了。

这个标度律具有实际意义，有时甚至是反直觉的。它告诉我们，射流在[远场](@keyword=far_zone|lang=zh-CN|style=Feynman)的强度取决于其初始动量通量，而不仅仅是其速度或[质量流](@keyword=mass_flow|lang=zh-CN|style=Feynman)率。考虑两个质量流率相同的射流。一个从光滑、设计精良的[喷嘴流](@keyword=nozzle_flow|lang=zh-CN|style=Feynman)出。另一个从同样直径的锐边孔口流出。由于一种称为“缩流”（vena contracta）的流体现象，从孔口流出的射流在出口后会收缩到一个更小的直径。为了通过这个更小的面积维持相同的质量流，其速度必须更高。这使得孔口射流具有更高的初始[动量通量](@keyword=momentum_flux|lang=zh-CN|style=Feynman)（$\rho A U^2$）。因此，在远下游，来自简单的锐边孔的射流实际上会比来自精美喷嘴的射流具有*更高*的中心线速度[@problem_id:1768128]！同样，如果你将射流的[动量通量](@keyword=momentum_flux|lang=zh-CN|style=Feynman)加倍，你会将其远场中心线速度增加一个因子 $\sqrt{2}$，即大约41%[@problem_id:1768120]。

### 回顾：[虚拟原点](@keyword=virtual_origin|lang=zh-CN|style=Feynman)

当然，自然界比我们简单的 $1/x$ 定律要微妙一些。这个定律是一个[渐近线](@keyword=asymptotes|lang=zh-CN|style=Feynman)——是对射流在无限远处行为的完美描述。在喷嘴附近，即“[近场](@keyword=near_field|lang=zh-CN|style=Feynman)”区域，射流仍在组织自身。来自喷嘴的初始均匀“顶帽形”速度剖面需要演变成[自相似](@keyword=self_similar|lang=zh-CN|style=Feynman)区域特有的钟形。这个发展过程需要一段距离。

为了解决这个问题，科学家们使用了一个巧妙的数学修正：**[虚拟原点](@keyword=virtual_origin|lang=zh-CN|style=Feynman)** $x_0$ [@problem_id:1768097]。我们不说速度与 $1/x$ 成正比，其中 $x$ 是与实际喷嘴的距离，而是说它与 $1/(x-x_0)$ 成正比。[虚拟原点](@keyword=virtual_origin|lang=zh-CN|style=Feynman)是一个虚构的点，通常位于物理喷嘴下游稍远处，完全发展的自相似射流*似乎*是从这一点起源的。这就像考虑到跑步者需要几步才能达到全速；[虚拟原点](@keyword=virtual_origin|lang=zh-CN|style=Feynman)是理想化的、恒定加速度比赛必须开始的点，以便与跑步者在赛道更远处的位​​置和速度相匹配。通过测量下游两个点的速度，人们可以向后推算找到这个[虚拟原点](@keyword=virtual_origin|lang=zh-CN|style=Feynman)的位置，并创建一个能够更广泛地准确描述射流速度衰减的模型。

### 射流如何成长：扩展、卷吸与[涡粘性](@keyword=eddy_viscosity|lang=zh-CN|style=Feynman)

我们已经看到射流会扩展并卷吸流体，并且我们已将其与速度的衰减联系起来。但是我们能让这种联系更精确吗？确实可以。射流的线性扩展（$b(x) = kx$，其中 $k$ 是扩展率）及其对质量的卷吸是同一枚硬币的两面。一项优美的分析表明，**卷吸系数** $\alpha$（量化射流吞噬环境流体的能力）与**扩展率** $k$ 成正比[@problem_id:660370]。这证实了我们的直觉：扩展更快的射流之所以如此，正是因为它卷吸了更多的流体。

这种扩展和混合的微观机制是什么？是[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)涡团。这些旋转的涡旋充当了高效的[动量输运](@keyword=momentum_transport|lang=zh-CN|style=Feynman)者。在射流高速核心中形成的涡团可以向外移动，携带其高动量并将其传递给边缘较慢的流体。反之，来自慢速边缘的涡团可能被卷入核心。这种混沌的动量交换远比层流中有序的[分子扩散](@keyword=molecular_diffusion|lang=zh-CN|style=Feynman)有效得多。

为了对此进行建模，我们可以使用 Ludwig Prandtl 引入的一个概念，即**[混合长度假说](@keyword=mixing_length_hypothesis|lang=zh-CN|style=Feynman)**。其思想是将所有这些[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)搅动的效果量化为一个**[涡粘性](@keyword=eddy_viscosity|lang=zh-CN|style=Feynman)** $\nu_t$ [@problem_id:593977]。可以把它看作是由[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)自身产生的有效粘性。分子粘性仅取决于流体的性质，而[涡粘性](@keyword=eddy_viscosity|lang=zh-CN|style=Feynman)则取决于流动本身——在[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)更强烈的地方它更大。对于射流来说，[涡粘性](@keyword=eddy_viscosity|lang=zh-CN|style=Feynman)与当地的中心线速度和当地的射流宽度成正比。这表明，随着射流变得更宽、更慢，其有效的“混合能力”也会相应改变。这种[涡粘性](@keyword=eddy_viscosity|lang=zh-CN|style=Feynman)通常比流体的分子粘性大数千倍，这正是[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)与其层流对应[物相](@keyword=phases_of_matter|lang=zh-CN|style=Feynman)比混合得如此剧烈的原因。

### 简化的局限：一个关于两种射流的难题

自相似性和[动量守恒](@keyword=conservation_of_momentum|lang=zh-CN|style=Feynman)的原理为我们理解[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)提供了一个强大而优雅的框架。但是[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)嫉妒地守护着它最深的秘密。即使是我们最先进的工具也可能在其复杂性面前显得无力。

一个经典的例子是“圆形射流/平面射流反常”现象[@problem_id:1766483]。工程师们经常使用计算模型，如标准的 **$k-\epsilon$ 模型**，来预测[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)。该模型使用一组通过大量实验校准的“普适”常数来预测[湍动能](@keyword=turbulent_kinetic_energy|lang=zh-CN|style=Feynman)（$k$）及其耗散率（$\epsilon$）等量。对于许多流动，它的效果非常好。然而，当应用于[自由射流](@keyword=free_jet|lang=zh-CN|style=Feynman)时，它就出错了。该模型正确地预测了平面射流（来自长而薄的缝隙）的扩展速度应该比圆形射流（来自圆形孔）快。但它算错了扩展率的*比值*。实验表明圆形射流的扩展速度约为平面射流的79%，而模型使用其标准常数预测该比率约为115%。

这种差异虽然看似很小，却凸显了一个深刻的真理：[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)的结构可能以不易被“普适”模型捕捉的方式依赖于流动的几何形状。它提醒我们，虽然我们发现了支配[湍流射流](@keyword=turbulent_jet|lang=zh-CN|style=Feynman)宏观行为的优美而强大的原理，但[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)复杂的内部运作仍然是[经典物理学](@keyword=classical_physics|lang=zh-CN|style=Feynman)中一个伟大的未解之谜。发现之旅，就像射流本身一样，不断向前，将已知与未知混合在一起。