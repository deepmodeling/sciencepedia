## 引言
能够“记忆”其形状的材料处于智能材料技术的前沿。大多数人熟悉的是单向[形状记忆效应](@keyword=shape_memory_effect|lang=zh-CN|style=Feynman)：一种变形的合金在加热后能够迅速恢复其原始形态。但如果一种材料能做到更多呢？如果它可以被教会记忆两种不同的形状——一个用于低温，一个用于高温——并在两者之间自主循环，又会怎样？这种非凡的能力，被称为[双向形状记忆效应](@keyword=two_way_shape_memory_effect|lang=zh-CN|style=Feynman)，将一块简单的金属转变为一个可编程的固态引擎。本文深入探讨了这一先进现象背后的科学，旨在回答核心问题：一个“第二记忆”是如何被印刻进材料的[微观结构](@keyword=microstructure|lang=zh-CN|style=Feynman)中的。在接下来的章节中，我们将首先探讨基本的“原理与机理”，剖析[热弹性](@keyword=thermoelasticity|lang=zh-CN|style=Feynman)[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)以及通过训练产生的内应力场的作用。随后，“应用与跨学科联系”章节将展示这种效应如何被用来创造创新的执行器和智能设备，以及其核心原理如何延伸到其他类型的材料中。

## 原理与机理

所以，我们拥有这些能够“记忆”形状的非凡材料。当它们处于低温状态时，你使其变形，然后像魔术一样，它们在加热后会恢复到原始形态。这就是单向[形状记忆效应](@keyword=shape_memory_effect|lang=zh-CN|style=Feynman)，本身就是一个引人入胜的技巧。但故事远不止于此。我们能否教会一种[材料记忆](@keyword=material_memory|lang=zh-CN|style=Feynman)*两种*不同的形状——一个用于高温，一个用于低温——并让它自行在两者之间切换？答案是肯定的，而理解其原理将揭示支配材料世界的物理学更深层的奥秘。要做到这一点，我们首先需要了解这场戏剧上演的舞台：[热弹性](@keyword=thermoelasticity|lang=zh-CN|style=Feynman)[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)。

### 一个可逆的世界：[热弹性](@keyword=thermoelasticity|lang=zh-CN|style=Feynman)[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)

想象一支纪律严明的军乐队，[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成一个完美的对称网格。这就是我们的材料在高温下的状态，一个称为**奥氏体**的相。它有序、坚固，这是它偏好的“母相”形状。现在，当温度降低时，乐队不仅仅是打冷颤，而是进行重组。它分解成更小、协同的小组，每个小组都以特定的方式倾斜或剪切。这种新的、对称性较低、更复杂的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)是低温相，称为**[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)**。

从[奥氏体](@keyword=austenite|lang=zh-CN|style=Feynman)到[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)的这种变化是一种**[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)**。在你可能熟悉的大多数材料中，比如水结成冰或铁的锻造，这种[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)在原子尺度上通常是混乱的。想象一下铁匠将烧红的剑浸入水中淬火。钢中向[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)的转变是剧烈且不可逆的。它会产生一堆微观缺陷——主要是永久性[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)——将新结构锁定。试图通过简单地加热钢来逆转这一过程，并不能恢复原始的奥氏体晶体；你最终只是将钢[回火](@keyword=tempering|lang=zh-CN|style=Feynman)成不同的结构。

[形状记忆合金](@keyword=shape_memory_alloys|lang=zh-CN|style=Feynman)则不同。它们的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，如物理学家所说，是**[热弹性](@keyword=thermoelasticity|lang=zh-CN|style=Feynman)**的。从[奥氏体](@keyword=austenite|lang=zh-CN|style=Feynman)“网格”到马氏体“小组”的变化是通过一种协同的、无[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)的剪切发生的。原子的邻域被重新[排列](@keyword=permutation|lang=zh-CN|style=Feynman)，但原子并未四处移动。更重要的是，这种[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)的应变不是通过产生大量[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)来适应的，而是通过形成高度有序、可移动的不同[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)取向（或称**变体**）之间的界面。这些被称为**[孪晶界](@keyword=twin_boundary|lang=zh-CN|style=Feynman)**。因为没有造成永久性损伤，这个过程在[晶体学](@keyword=crystallography|lang=zh-CN|style=Feynman)上是可逆的。当你加热时，马氏体变体可以沿着完全相同的路径转化回去，完美地恢复原始的[奥氏体](@keyword=austenite|lang=zh-CN|style=Feynman)结构。

这个[可逆过程](@keyword=reversible_processes|lang=zh-CN|style=Feynman)由四个关键[温度控制](@keyword=temperature_control|lang=zh-CN|style=Feynman)：
*   在冷却时，[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)在**马氏体开始温度（$M_s$）**时开始，并在**[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)完成温度（$M_f$）**时完成。
*   在加热时，逆[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)在**[奥氏体](@keyword=austenite|lang=zh-CN|style=Feynman)开始温度（$A_s$）**时开始，并在**奥氏体完成温度（$A_f$）**时结束。

这种可逆的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)是实现形状记忆的根本引擎。

### 单行道

让我们跟踪一根标准的、“未经训练”的[形状记忆合金](@keyword=shape_memory_alloys|lang=zh-CN|style=Feynman)丝，观察其在一个循环中的基本单向效应。

1.  **从高温开始：** 我们从一根温度高于$A_f$的直丝开始。它处于稳定、无应力的奥氏体相。其应变为零。

2.  **冷却：** 我们将金属丝冷却到低于$M_f$的温度。它完全转变为[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)。但等等——金属丝仍然是直的！为什么？因为马氏体以多种自协调的变体形式生成。对于每一个向某个方向剪切的小区域，附近都有另一个向相反方向剪切的区域进行补偿。从外部看，所有这些微观剪切都相互抵消，宏观形状没有改变。其结构就像一副完美洗过的扑克牌；它包含了所有变体，但顺序杂乱无章。

3.  **低温变形：** 现在，当它处于低温的[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)状态时，我们把它弯成一个“U”形。这是关键一步。弯曲过程出奇地容易，因为我们并不是在通常意义上对金属进行永久性变形。相反，我们只是提供一个小小的推力，促使一些马氏体变体以牺牲其他变体为代价而生长。我们正在对材料进行**去孪生**——说服这些变体以一种适应新形状的方式重新[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。这就像把我们那副洗乱的牌整理好，让所有的牌都朝向同一个方向。一旦我们移除弯曲力，金属丝就保持在这个“U”形。

4.  **加热：** 我们轻轻加热金属丝。当其温度越过$A_s$并向$A_f$升高时，奇迹发生了。材料变回[奥氏体](@keyword=austenite|lang=zh-CN|style=Feynman)。由于奥氏体相只有一个“记忆”的构型——即最初的直线形状——金属丝迅速恢复其母相形状，完全抹去了“U”形。

如果我们再次冷却它，它仍然保持直线。它已经忘记了“U”形。它只记得它在高温时的母相形状。这就是**单向[形状记忆效应](@keyword=shape_memory_effect|lang=zh-CN|style=Feynman)**的本质。

### 训练新记忆：双向效应的秘密

这一切都非常巧妙，但我们的目标是创造一种在冷却时能自发呈现“U”形的材料，无需任何外力。我们需要它既能记住高温形状，也能记住低温形状。为此，我们必须对材料进行“训练”。

训练过程在原理上出奇地简单：我们只需一遍又一遍地重复单向循环。我们冷却金属丝，机械地将其变形为所需的低温形状（“U”形），然后加热以恢复高温形状（直线）。经过许多这样的循环后，材料内部发生了深刻的变化。现在，当我们冷却这根直的、无应力的金属丝时，它会自发地弯曲成“U”形。加热后，它又会变直。它学会了第二种记忆。这就是**[双向形状记忆效应](@keyword=two_way_shape_memory_effect|lang=zh-CN|style=Feynman)（TWSME）**。

这种训练做了什么？它在材料的[微观结构](@keyword=microstructure|lang=zh-CN|style=Feynman)中刻下了一幅微妙、无形的应力图景。每次我们使[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)变形时，我们不只是重新定向[孪晶界](@keyword=twin_boundary|lang=zh-CN|style=Feynman)。我们还创造了少量稳定的缺陷，比如有序的[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)网络，或者微小的、被困住的特定[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)变体岛，这些变体在加热时不会转变回去。每一次训练循环，这些缺陷结构都会被建立和加强。它们不会消失。

它们共同创造了一个永久的、内建的**内应力场**。可以把它想象成一种隐藏的偏向，是我们用于弯曲的力量的幽灵，如今被冻结在材料的构造中。

### 看不见的手：[内应力](@keyword=internal_stress|lang=zh-CN|style=Feynman)场的物理学

这个内应力场是整个双向效应的关键。自然是经济的；过程会遵循能量最低的路径。当经过训练的金属丝冷却并开始转变为马氏体时，它有许多变体选择。但现在，[内应力](@keyword=internal_stress|lang=zh-CN|style=Feynman)场提供了一只“引导之手”。

转变为与该内应力场方向一致的马氏体变体在能量上更有利。[内应力](@keyword=internal_stress|lang=zh-CN|style=Feynman)在该变[体应变](@keyword=volumetric_dilatation|lang=zh-CN|style=Feynman)上所做的功，一个形如$\boldsymbol{\sigma}_{\mathrm{int}}:\boldsymbol{\epsilon}^{\mathrm{tr}}$的项，降低了其总吉布斯自由能。因为这是一条更容易的路径，这些“受偏好”的变体优先形成，而其他变体的形成则受到抑制。由于所有这些优先形成的变体都以相同的方式[排列](@keyword=permutation|lang=zh-CN|style=Feynman)——即我们在训练期间强迫它们[排列](@keyword=permutation|lang=zh-CN|style=Feynman)的方式——它们各自的微观剪切会累加起来。结果如何？一个自发的宏观形状变化。金属丝自行弯曲。

这种[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)偏好有一个优美且可测量的后果。因为内应力辅助了[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，受偏好的变体可以在比通常情况下稍高的温度开始形成。这些变体的[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)开始温度$M_s$实际上被提高了。例如，仅50 MPa的拉伸[内应力](@keyword=internal_stress|lang=zh-CN|style=Feynman)就可以使局部$M_s$提高超过5 K，从而使这些变体在冷却过程中抢占先机。

真正奇妙的是这一切是如何联系起来的。我们可以基于这个想法建立一个物理模型。对于一种典型的材料，要产生约1.2%的自发双向应变，我们需要约20 MPa的内偏应力。这是一个合理的数字吗？我们可以转向微观结构，计算我们[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)从我们知道在训练期间产生的[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)阵列和残余[马氏体](@keyword=martensite|lang=zh-CN|style=Feynman)中得到的应力。惊人的是，这些数字几乎完全吻合。我们的理论所要求的应力，恰好是真实的物理[微观结构](@keyword=microstructure|lang=zh-CN|style=Feynman)所能提供的应力。这是一个强有力的证明，表明我们的图景是正确的。[双向形状记忆效应](@keyword=two_way_shape_memory_effect|lang=zh-CN|style=Feynman)不是魔术；它是一个微妙的、由训练精心雕琢的内部应力图景的宏观表现。