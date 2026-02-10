## 引言
在追求知识的道路上，无论是理解宇宙，还是设计坚固的结构，能够测量极其微小的变化都至关重要。[光学干涉测量法](@keyword=optical_interferometry|lang=zh-CN|style=Feynman)，即利用光波进行测量的科学，提供了这种精妙的灵敏度，但它也带来了一个重大挑战：正是这种能探测微小现象的灵敏度，也使其极易受到[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)和温度变化等环境噪声的影响。这一实际限制常常使最灵敏的[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)只能在高度隔离的实验室中使用。本文旨在探讨[共路干涉仪](@keyword=common_path_interferometer|lang=zh-CN|style=Feynman)这种优雅而强大的设计理念，来解决这一问题。这类仪器通过巧妙的设计，能够从噪声中分辨出信号。

在接下来的章节中，您将发现这一原理如何在多种强大的设备中得以实现。第一章“原理与机制”将解析核心概念，探讨像[Sagnac干涉仪](@keyword=sagnac_interferometer|lang=zh-CN|style=Feynman)和剪切[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)这样的基础装置如何抑制[共模噪声](@keyword=common_mode_noise|lang=zh-CN|style=Feynman)。随后，“应用与跨学科联系”一章将展示这种方法在工程、医学乃至量子物理前沿等不同领域所带来的变革性影响，揭示出贯穿精确测量领域的一条统一线索。

## 原理与机制

想象一下，有人让你画一个完美的圆。这很难！现在，再想象一下，让你用一支笔在第一个圆上再描一遍，但这支笔只在你第二次画的线偏离第一条线时才会留下痕迹。如果你完美地描绘了路径，纸上将空无一物。但任何轻微的颤抖，任何微小的偏离，都会立即显现出来。这便是**[共路干涉仪](@keyword=common_path_interferometer|lang=zh-CN|style=Feynman)**的核心理念。这是一种极其灵敏的设备，其灵敏并非源于其脆弱，而是因为它被设计用来忽略混乱，并凸显最微小、最有趣的差异。它通过将两束源自同一母体的光束，沿几乎完全相同的路径传播来实现这一点。正是这段共享的旅程赋予了[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)超凡的能力：对[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)和[温度波](@keyword=temperature_wave|lang=zh-CN|style=Feynman)动等常见外界干扰的强大免疫力，使其能够探测到极其细微的现象。

### 共享路径之美：[Sagnac干涉仪](@keyword=sagnac_interferometer|lang=zh-CN|style=Feynman)

最典型的[共路干涉仪](@keyword=common_path_interferometer|lang=zh-CN|style=Feynman)是**[Sagnac干涉仪](@keyword=sagnac_interferometer|lang=zh-CN|style=Feynman)**。在其最纯粹的形式中，一束光射向一个**[分束器](@keyword=beam_splitter|lang=zh-CN|style=Feynman)**——一种特殊的镜子，它能反射一半的光，并让另一半光通过。这样，光束被分成两个完全相同的“双胞胎”：一束沿闭合回路顺时针 (CW) 传播，另一束则沿完全相同的回路逆时针 (CCW) 传播。完成旅程后，它们回到同一个[分束器](@keyword=beam_splitter|lang=zh-CN|style=Feynman)并重新合束，射向一个探测器。

由于两束光都沿相同的物理路径传播，它们会经历相同的[颠簸](@keyword=thrashing|lang=zh-CN|style=Feynman)和摆动。如果一面镜子[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，它对两束光的影响是均等的。如果路径中的空气受[热膨胀](@keyword=thermal_expansion|lang=zh-CN|style=Feynman)，它对两束光的光程改变也是相同的。当光束重新合束时，这些**共模**扰动会相互抵消，从而产生一个异常稳定的信号。

但这种稳定性并非故事的终点，而恰恰是起点。真正的魔力发生在对称性被打破之时——即当某种因素以不同方式影响这两束[反向传播](@keyword=backpropagation|lang=zh-CN|style=Feynman)的光束时。此时，[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)便成为探测那种不对称性的极其灵敏的工具。

最著名的例子是**[Sagnac效应](@keyword=sagnac_effect|lang=zh-CN|style=Feynman)**。如果你旋转整个[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)回路，沿旋转方向传播的光束需要走稍远一点的距离才能追上离去的[分束器](@keyword=beam_splitter|lang=zh-CN|style=Feynman)，而逆着旋转方向传播的光束路径则稍短一些。这个与旋转速率成正比的微小[光程差](@keyword=optical_path_difference|lang=zh-CN|style=Feynman)，会在两束光之间产生一个[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)。这正是[光纤陀螺仪](@keyword=fiber_optic_gyroscope|lang=zh-CN|style=Feynman)的工作原理，它们是引导飞机、卫星和潜艇的惯性核心，使其无需任何外部参考即可导航。

我们也可以有意地在共路中放置物体来研究其特性。想象一下，我们采用一个由强度为 $I_0$ 的[非偏振光](@keyword=unpolarized_light|lang=zh-CN|style=Feynman)馈入的[Sagnac干涉仪](@keyword=sagnac_interferometer|lang=zh-CN|style=Feynman)，并在回路中插入一个简单的[线性偏振片](@keyword=linear_polarizer|lang=zh-CN|style=Feynman)[@problem_id:2249208]。顺时针和逆时针光束都必须穿过它。一个理想的[偏振片](@keyword=optical_polarizer|lang=zh-CN|style=Feynman)会丢弃所有与其偏振轴不符的光，对[非偏振光](@keyword=unpolarized_light|lang=zh-CN|style=Feynman)而言，这意味着它丢弃了一半的能量。穿过[偏振片](@keyword=optical_polarizer|lang=zh-CN|style=Feynman)后，两束光都变成了完全偏振的，强度为原来的一半。当这两束现已完全相同的光束重新合束时，它们可以以完美的对比度进行干涉。然而，由于一半的光从一开始就被丢弃了，探测器上最亮的条纹强度最多也只能达到 $I_0/2$。共路确保了该元件对两束光的影响是相同的，而物理定律则决定了其结果。

当我们探测[光与物质相互作用](@keyword=light_matter_interaction|lang=zh-CN|style=Feynman)的本质时，事情变得更加引人入胜。大多数光学元件是**互易的**：它们对光束的影响不依赖于光的传播方向。一面镜子从两边反射的方式是相同的。但有些材料是**非互易的**。例如，**[法拉第旋转器](@keyword=faraday_rotator|lang=zh-CN|style=Feynman)**利用[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)将[光的偏振](@keyword=light_polarization|lang=zh-CN|style=Feynman)方向旋转一个角度，比如 $+\theta$，而这个旋转与[光的传播](@keyword=light_propagation|lang=zh-CN|style=Feynman)方向无关。

让我们进行一个思想实验，将一个互易元件，如**[半波片](@keyword=half_wave_plate|lang=zh-CN|style=Feynman) (HWP)**，和一个非互易的[法拉第旋转器](@keyword=faraday_rotator|lang=zh-CN|style=Feynman) (FR) 都放入我们的Sagnac回路中[@problem_id:976776]。顺时针光束先通过FR，再通过HWP。逆时针光束则以相反的顺序遇到它们，先是HWP，然后是FR。对于互易的HWP，[反向传播](@keyword=backpropagation|lang=zh-CN|style=Feynman)等同于一个不同的数学变换（其矩阵的转置）。而对于非互易的FR，两个方向的变换是相同的。最终结果是，顺时针路径的总偏振变化与逆时针路径的不同。[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)成了一个区分互易和非互易效应的灵敏工具，这一原理被用于构建光学隔离器，这种器件像光的单行道一样工作。这种装置可以被精确控制，甚至可以在输入端使用非偏振光，通过回路中不对称的偏[振动力学](@keyword=vibrational_mechanics|lang=zh-CN|style=Feynman)，在输出端产生具有特定、可调[偏振度](@keyword=degree_of_polarization|lang=zh-CN|style=Feynman)的光[@problem_id:1025172]。

### 双重影像：剪切[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)

并非所有[共路干涉仪](@keyword=common_path_interferometer|lang=zh-CN|style=Feynman)都使用[反向传播](@keyword=backpropagation|lang=zh-CN|style=Feynman)的光束。另一类巧妙的设计是**剪切[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)**，它通过复制第一束光并将其轻微平移（即*剪切*）来产生第二束光。

想象一下，你透过一扇特殊的窗户看远处的风景，这扇窗户既显示正常景象，也显示一个向右平移了一英寸的透明副本。如果看一堵平坦无奇的墙，重叠部分会很无趣。但如果你看一道栅栏，你会看到一个复杂的重叠板条图案。这扇剪切窗户让你将场景中的每一点与其紧邻的点进行比较。

**横向剪切[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)**，例如**Jamin干涉仪**，正是对光[波前](@keyword=wavefront|lang=zh-CN|style=Feynman)做这样的操作。它接收一个入射波前，将其分束，然后与自身的横向平移版本重新合束。这是一个极其强大的诊断工具。如果入射波前是完美的平面——如同来自理想激光器——将其与平移后的副本干涉会产生一个均匀的场。但如果[波前](@keyword=wavefront|lang=zh-CN|style=Feynman)是畸变的，比如穿过[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)大气或不完美的透镜，干涉图样会立刻揭示出[波前](@keyword=wavefront|lang=zh-CN|style=Feynman)形状的*梯度*或斜率。这就像光波相位的地形图。

这项技术还为我们提供了一个直接观察光最基本属性之一的窗口：**[空间相干性](@keyword=spatial_coherence|lang=zh-CN|style=Feynman)**。[相干性](@keyword=coherence|lang=zh-CN|style=Feynman)要问的是：光波在空间中某一点的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)与另一点的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)有多大关联？来自遥远恒星的光以非常有序、相干的波前到达。而来自近处磨砂灯泡的光则是一团混乱的杂波。剪切[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)通过迫使一个波前与自身的平移版本发生干涉来直接测量这一点。

考虑用来自两个微小、相互非相干的点光源的光照射Jamin[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)，该干涉仪引入的剪切量为 $s$。这两个点光源位于很远的距离 $L$ 处，彼此相距为 $d$ [@problem_id:1036422]。这两个光源共同作用，如同一个略微扩展的光源。干涉仪产生的[干涉条纹](@keyword=interference_fringes|lang=zh-CN|style=Feynman)的可见度将取决于间距 $d$。随着 $d$ 的增加，可见度下降，直到在 $d = \lambda L / (2s)$ 时完全消失。此时，相距为剪切距离 $s$ 的两点处的光已变得完全不相关。[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)测量了光场的相干性，而这反过来又告诉我们光源的大小。这就是像[恒星干涉测量法](@keyword=stellar_interferometry|lang=zh-CN|style=Feynman)这类天文学技术的实用原理，用于测量那些因太遥远而无法被任何单个望远镜分辨的恒星的角直径。

应用不止于线性光学。让我们在其中一条剪切路径中放置一种特殊材料。这种材料表现出**[双光子吸收](@keyword=two_photon_absorption|lang=zh-CN|style=Feynman) (TPA)**，即[光强度](@keyword=light_intensity|lang=zh-CN|style=Feynman)越高，它对光的吸收越强[@problem_id:1036431]。现在，参考光束的强度是恒定的，但样品光束的强度会因其自身功率而减小。两个干涉光束之间的这种强度不平衡会降低[条纹可见度](@keyword=fringe_visibility|lang=zh-CN|style=Feynman)。输入激光越强，TPA效应越显著，可见度就越低。通过简单地测量[条纹可见度](@keyword=fringe_visibility|lang=zh-CN|style=Feynman)随输入激[光功率](@keyword=optical_power|lang=zh-CN|style=Feynman)的变化，我们就可以反推出该材料的非线性TPA系数 $\beta$，且精度很高。

### 极致精度：差分测量

共路设计理念在**差分测量**中达到了顶峰。这个想法简单而深刻。如果你想在一个不断晃动的秤上称一根羽毛的重量，你会非常困难。但如果你有两个相同的秤，把羽毛放在其中一个上，然后用放有羽毛的晃动秤的读数减去那个空的、同样晃动的秤的读数，晃动——即[共模噪声](@keyword=common_mode_noise|lang=zh-CN|style=Feynman)——就消失了，只剩下羽毛的重量。

这就是现代用作重力梯度仪的**[原子干涉仪](@keyword=atom_interferometer|lang=zh-CN|style=Feynman)**背后的原理[@problem_id:1167112]。这些设备是[Mach-Zehnder干涉仪](@keyword=mach_zehnder_interferometer|lang=zh-CN|style=Feynman)，但它们分裂和重组的是超冷原子的物质波，而非光波。原子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的相位对重力极其敏感。一个重[力梯度](@keyword=force_gradient|lang=zh-CN|style=Feynman)仪由两个这样的[原子干涉仪](@keyword=atom_interferometer|lang=zh-CN|style=Feynman)组成，一个垂直放置在另一个上方，相隔距离为 $L$。每个[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)都是一个共路设备，其相位会因当地的[重力加速度](@keyword=acceleration_due_to_gravity|lang=zh-CN|style=Feynman) $g$ 而发生偏移。

关键的测量不是任何一个[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)的相位，而是顶部和底部[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)之间的相位*差*，$\delta\Phi = \Delta\Phi_B - \Delta\Phi_A$。这个差分相位与**重[力梯度](@keyword=force_gradient|lang=zh-CN|style=Feynman)** $\Gamma$ 直接成正比，$\Gamma$ 是重力随高度变化的快慢（$g(z) = g_0 - \Gamma z$）。这是一项极其强大的技术。例如，用于操控原子的激光的任何漂移或频率啁啾对两个干涉仪来说都是共同效应，因此在相减过程中被完美抵消。这使得可以测量地球[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)的微小变化，可用于矿产勘探、寻找地下空洞或监测含水层。

当然，现实世界从不完美。如果整个装置，以及驱动[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)的激光束，与真正的垂直方向有一个微小的静态倾斜角 $\theta$ 会怎么样？这将导致激光的波矢量 $\mathbf{k}_{\text{eff}}$ 有一个微小的水平分量，而重力 $\mathbf{g}$ 是纯垂直的。每个[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)中的[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)取决于[点积](@keyword=dot_product|lang=zh-CN|style=Feynman) $\mathbf{k}_{\text{eff}} \cdot \mathbf{g}$，该值现在与 $\cos\theta$ 成正比。正如分析所示[@problem_id:1167112]，这个微小的倾斜在[差分](@keyword=differencing|lang=zh-CN|style=Feynman)测量中不会被抵消。它会引入一个与 $\theta^2$ 以及人们试图测量的重[力梯度](@keyword=force_gradient|lang=zh-CN|style=Feynman) $\Gamma$ 成比例的虚假信号。这不是失败，而是一个教训。它既展示了[差分](@keyword=differencing|lang=zh-CN|style=Feynman)共路方法在消除大量噪声源方面的巨大威力，也凸显了实验物理学家面临的持续挑战：当你将精度推向绝对极限时，必须理解并减弱那些浮现出来的更细微的[系统误差](@keyword=systematic_error|lang=zh-CN|style=Feynman)。从[陀螺仪](@keyword=gyroscope|lang=zh-CN|style=Feynman)到量子传感器，原理始终如一：让宇宙为你完成减法运算。