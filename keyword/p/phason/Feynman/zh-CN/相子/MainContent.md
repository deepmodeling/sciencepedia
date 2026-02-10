## 引言
在人们所熟知的[完美晶体](@keyword=perfect_crystal|lang=zh-CN|style=Feynman)世界里，原子[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成简单的重复[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。这些原子的集体摆动和[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)产生了称为[声子](@keyword=phonons|lang=zh-CN|style=Feynman)（即声音的粒子）的激发。但自然界中许多最引人入胜的材料，从准晶到具有电荷密度波的体系，都颠覆了这种简单的周期性有序。它们的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)是一种复杂、不重复的图案。这就引出了一个根本性问题：除了简单的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，这些复杂结构还能承载哪些其他基本激发？

答案在于一种非凡且往往难以捉摸的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)：**[相子](@keyword=phasons|lang=zh-CN|style=Feynman)**。[相子](@keyword=phasons|lang=zh-CN|style=Feynman)并非原子围绕其平均位置的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，而是底层图案本身的集体“滑动”或[重排](@keyword=derangement|lang=zh-CN|style=Feynman)。它代表了有序结构相位的细微变化。理解这一独特的自由度是揭开非周期物质秘密的关键。本文旨在探索[相子](@keyword=phasons|lang=zh-CN|style=Feynman)的世界。首先，**原理与机制**一章将深入探讨其理论基础，解释什么是[相子](@keyword=phasons|lang=zh-CN|style=Feynman)，支配其运动的物理学原理，以及它们如何从密度波到高维准晶模型等体系中涌现。随后，**应用与跨学科联系**一章将揭示这些理论概念如何在现实世界中体现，从在实验中留下明确的印记，到决定材料独特的力学和热学性质。

## 原理与机制

想象一下，你正凝视着一个完全静止的湖面。若你向湖中投下一颗石子，便会激起阵阵涟漪。[完美晶体](@keyword=perfect_crystal|lang=zh-CN|style=Feynman)中的原子就像那静止的湖水——一个完全有序、重复的图案。扰动产生的涟漪就是我们所说的**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**，即[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)，它是原子围绕其固定位置的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。这是一个我们熟悉且优美的故事。但如果水的“静止”状态并非平坦的呢？如果湖面在其最自然、能量最低的状态下，本就是一片由冻结波浪构成的景观，一个由波峰和波谷组成的完美规则、重复的图案呢？材料世界充满了这样的奇观，从**[电荷密度波](@keyword=charge_density_waves|lang=zh-CN|style=Feynman) (CDWs)** 和**[自旋密度波](@keyword=spin_density_wave_2|lang=zh-CN|style=Feynman) (SDWs)** 到**准晶**宏伟壮丽、不重复的图案。在这些体系中，存在着一种新型的涟漪，它不是原子位置的涟漪，而是图案本身的涟漪。这便是**[相子](@keyword=phasons|lang=zh-CN|style=Feynman)**的故事。

### 两种摆动的故事：振幅与相位

让我们从一个简单的波开始，就像你在数学课上画的那种：$A \cos(kx + \phi)$。这个波由两个关键属性定义：它的振幅 $A$（波峰有多高），以及它的相位 $\phi$（决定了波峰的位置）。现在，如果这个波代表了一种材料的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)——比如说，一个SDW中电子自旋的密度——那么它的低能激发，即“波上的摆动”，也将分为两种基本类型。

首先，你可以想象振幅的涨落，让波峰变得稍高或稍低。这就像一股能量脉冲，使整个波形“呼吸”。这类激发被称为**振幅子**。改变振幅通常需要耗费相当大的能量，因为它扰乱了最初形成该波的精妙平衡。因此，振幅子激发通常有一个能量“[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)”——你需要一个最小的能量块才能创造一个。

但是相位呢？想象一下，我们物理地抓住这个波，在不改变其形状或高度的情况下前后滑动它。这就是相位的变化，即 $\phi$ 的变化。如果我们的冻结波的波长相对于其下的原子间距是一个随机的无理数——我们称这种状态为**非公度**——那么波峰和波谷就没有偏好的固定位置。滑动整个波根本不会改变系统的总能量！这种滑动的自由是一种[连续对称性](@keyword=continuous_symmetry|lang=zh-CN|style=Feynman)，而物理学中一个深刻的原理，即**[戈德斯通定理](@keyword=goldstone_s_theorem|lang=zh-CN|style=Feynman)**，告诉我们，每当一个[连续对称性](@keyword=continuous_symmetry|lang=zh-CN|style=Feynman)被自发破缺时，必然存在一个无能隙、零能量的激发。这种激发，这种集体的滑动运动，就是**[相子](@keyword=phasons|lang=zh-CN|style=Feynman)**。

### 运动中的[相子](@keyword=phasons|lang=zh-CN|style=Feynman)：波、涟漪与动量

整个图案的均匀滑动仅仅是个开始。真正的乐趣始于相移并非处处相同。想象一下，相位 $\phi$ 现在依赖于位置，即 $\phi(x)$。空间变化的相位意味着局部波长在改变。相位变化快的地方，波被压缩；变化慢的地方，波被拉伸。因此，[相子](@keyword=phasons|lang=zh-CN|style=Feynman)是底层调制*相位*中传播的涟漪。

这种涟漪是如何移动的呢？让我们构建一个非常简单的画面。想象一串由微小弹簧连接的原子链。现在，假设一个外力已将它们[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成一个正[弦图](@keyword=chordal_graphs|lang=zh-CN|style=Feynman)案，一个静态的、非公度的结构波。如果我们制造一个小的、局部的相移——一个“[相子](@keyword=phasons|lang=zh-CN|style=Feynman)涟漪”——原子必须移动，拉伸和压缩它们之间的弹簧。这些被拉伸的弹簧会拉动它们的邻居，邻居再拉动它们的邻居，于是相位涟漪便沿着链传播下去。令人惊奇的是，详细的计算表明，这个[相子](@keyword=phasons|lang=zh-CN|style=Feynman)波以速度 $v_p = a\sqrt{C/m}$ 移动，其中 $a$ 是原子间距， $C$ 是[弹簧常数](@keyword=spring_constant|lang=zh-CN|style=Feynman)， $m$ 是原子质量。这与链中的声速完全相同！所以，在这个简单的视角下，[相子](@keyword=phasons|lang=zh-CN|style=Feynman)的行为很像[声子](@keyword=phonons|lang=zh-CN|style=Feynman)，一种声学波，但它代表的是结构*[重排](@keyword=derangement|lang=zh-CN|style=Feynman)*的传播，而非简单的[密度涨落](@keyword=density_fluctuations|lang=zh-CN|style=Feynman)。

就像[声子](@keyword=phonons|lang=zh-CN|style=Feynman)被量子化为声的粒子一样，[相子](@keyword=phasons|lang=zh-CN|style=Feynman)也可以被量子化为[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。一个波矢为 $q$ 的[相子](@keyword=phasons|lang=zh-CN|style=Feynman)携带一份精确的[晶体动量](@keyword=crystal_momentum|lang=zh-CN|style=Feynman) $p = \hbar q$ 和能量 $E = \hbar\omega(q)$。能量与动量之间的关系，即**色散关系** $\omega(q)$，包含了其动力学的秘密。虽然在长波长下它通常是线性的（$\omega \propto q$），但更复杂的模型显示它可能更加复杂，反映了其中错综复杂的相互作用力。

### 窥探高维：准晶中的[相子](@keyword=phasons|lang=zh-CN|style=Feynman)

[相子](@keyword=phasons|lang=zh-CN|style=Feynman)的概念在**准晶**的世界中找到了其最深刻、也 arguably 最优美的表达。这些材料的原子[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成完全有序却不重复的图案，很像彭罗斯铺砖。事物如何能做到有序却非周期性？物理学家发现，答案在于用更多维度来思考。

想象一个位于高维空间中的完美、简单、周期的晶体——对于一个三维二十面体准晶，这是一个六维超[立方晶格](@keyword=cubic_lattices|lang=zh-CN|style=Feynman)。我们的三维宇宙只是穿过这个[超晶格](@keyword=superlattices|lang=zh-CN|style=Feynman)的一个“切片”。我们看到的原子是六维晶体中恰好非常靠近我们三维切片的格点。这些原子在我们的三维切片*内部*的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)是我们熟悉的[声子](@keyword=phonons|lang=zh-CN|style=Feynman)。但如果我们摆动切片本身，让它在高维空间中来回移动呢？靠近切片的六维格点会改变，导致我们三维世界中的一些原子消失，而另一些原子在附近出现。这对应于原子“跃迁”到新的稳定位置，[重排](@keyword=derangement|lang=zh-CN|style=Feynman)了局域的拼贴图案。这种运动，这种在隐藏的、“垂直”维度中的位移，就是准晶中的[相子](@keyword=phasons|lang=zh-CN|style=Feynman)。

这个优雅的图像带来了强有力的推论。它告诉我们，一个**[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)**——材料中的一种[线缺陷](@keyword=line_defects|lang=zh-CN|style=Feynman)——不再仅仅是一个简单的原子面缺失。在高维视角下，一个[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)由一个“伯格斯矢量”来表征，该矢量是超晶格的一个[晶格矢量](@keyword=lattice_vectors|lang=zh-CN|style=Feynman)。这个矢量在我们的物理空间中有一个分量（[声子](@keyword=phonons|lang=zh-CN|style=Feynman)部分，$\mathbf{b}^{\parallel}$）和一个在垂直空间的分量（[相子](@keyword=phasons|lang=zh-CN|style=Feynman)部分，$\mathbf{b}^{\perp}$）。这意味着你可以拥有一个“纯[相子](@keyword=phasons|lang=zh-CN|style=Feynman)[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)”，这是一种没有长程原子位移的缺陷，但它代表了拼贴规则中的一个根本性错误，是几何图案本身的一道疤痕。

### 为[相子](@keyword=phasons|lang=zh-CN|style=Feynman)刹车：[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)、钉扎与扩散

在我们理想的、非公度的世界里，[相子](@keyword=phasons|lang=zh-CN|style=Feynman)是一种[无能](@keyword=anergy|lang=zh-CN|style=Feynman)隙、自由滑动的模式。然而，现实往往更混乱也更有趣。滑动的自由可以被剥夺。

一种方式是通过**锁定[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)**。如果[调制](@keyword=modulation|lang=zh-CN|style=Feynman)的波长非常接近底层原子[晶格间距](@keyword=lattice_spacing|lang=zh-CN|style=Feynman)的一个简单分数（例如，4倍间距），系统可能会发现，稍微拉伸或压缩其波以“锁定”并变得完全**公度**在能量上更为有利。当这种情况发生时，滑动对称性被破坏。现在波有特殊的、低能量的位置可以停留。试图将其从能量最低点滑开需要能量，这可以由一个“锁定”势，如 $-V\cos(4\phi)$ 来描述。这个势能就像一个回复力，赋予[相子](@keyword=phasons|lang=zh-CN|style=Feynman)有限的质量，并在其[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)中打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。

即使在真正非公度的体系中，杂质、缺陷或原子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)固有的离散性也可以充当“钉扎中心”，牵制住波，阻止其自由滑动。这种**钉扎**也提供了一个[回复力](@keyword=restoring_force|lang=zh-CN|style=Feynman)，并打开了一个[相子](@keyword=phasons|lang=zh-CN|style=Feynman)[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。

此外，在许多真实材料中，特别是准晶中，[相子](@keyword=phasons|lang=zh-CN|style=Feynman)根本不像清晰的波那样传播。相互作用导致它们的运动被严重阻尼。[相子](@keyword=phasons|lang=zh-CN|style=Feynman)激发不会像钟声一样鸣响，而是会缓慢而迟滞地弛豫回平衡状态。这被称为**[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)**或**[过阻尼](@keyword=overdamping|lang=zh-CN|style=Feynman)**动力学。[相子](@keyword=phasons|lang=zh-CN|style=Feynman)的运动更像是在搅拌糖蜜，而不是掀起波浪。这是[相子](@keyword=phasons|lang=zh-CN|style=Feynman)如此难以被直接观测的主要原因之一——它们不能有效地将能量从一处传递到另一处。

### [相子](@keyword=phasons|lang=zh-CN|style=Feynman)的重要性

那么，我们为什么要在意这些难以捉摸的激发呢？[相子](@keyword=phasons|lang=zh-CN|style=Feynman)不仅仅是理论上的奇珍；它们对于一大类材料的存在和性质至关重要。

首先，它们决定了这些结构的**稳定性**。在低维度（一维或二维）中，[无能](@keyword=anergy|lang=zh-CN|style=Feynman)隙[相子](@keyword=phasons|lang=zh-CN|style=Feynman)的热涨落会变得非常大，以至于它们可以完全摧毁准晶或[密度波](@keyword=density_wave|lang=zh-CN|style=Feynman)的长程序，实际上“熔化”了该图案。二维准晶在有限温度下的存在之所以是一个微妙的问题，正是因为这些强大的[相子](@keyword=phasons|lang=zh-CN|style=Feynman)涨落。

其次，它们留下了供实验学家寻找的独特印记。虽然传播的[相子](@keyword=phasons|lang=zh-CN|style=Feynman)很难看到，但与静态或缓慢[相子](@keyword=phasons|lang=zh-CN|style=Feynman)相关的*应变*却并非如此。[相子](@keyword=phasons|lang=zh-CN|style=Feynman)应变对应于摆动高维切片，它会导致用于识别准晶的尖锐衍射点（布拉格峰）以一种非常特征性的方式移动或展宽。这是证明它们存在的主要证据之一。

最后，[相子](@keyword=phasons|lang=zh-CN|style=Feynman)几乎影响着这些材料的每一种物理性质。人们认为，准晶中[相子](@keyword=phasons|lang=zh-CN|style=Feynman)的缓慢、[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)运动是其导热性异常低的主要原因。原子通过[相子](@keyword=phasons|lang=zh-CN|style=Feynman)翻转进行[重排](@keyword=derangement|lang=zh-CN|style=Feynman)的能力促成了它们独特的力学性质，比如它们在应力下的形变方式。从输运到[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)，[相子](@keyword=phasons|lang=zh-CN|style=Feynman)无声而缓慢的舞蹈正扮演着至关重要的角色，编织着[非周期有序](@keyword=aperiodic_order|lang=zh-CN|style=Feynman)这幅复杂而美丽的织锦。