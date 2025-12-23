## 引言
在固体力学领域，如何准确预测和模拟材料中裂纹的萌生与扩展，一直是核心的挑战之一。传统的[连续介质力学](@entry_id:155125)依赖于[偏微分方程](@entry_id:141332)，当[位移场](@entry_id:141476)出现不连续（即裂纹）时，其空间导数变得无定义，导致模型在数学上失效。[近场动力学](@entry_id:191791)（Peridynamics）作为一种革命性的[非局部理论](@entry_id:752667)，通过从根本上改变力学相互作用的描述方式，为这一难题提供了优雅的解决方案。它摒弃了空间导数的概念，转而假设物[质点](@entry_id:186768)与其有限邻域内的所有点都存在直接的相互作用，从而使得描述不连续现象成为可能。

本文旨在系统地阐述[近场动力学](@entry_id:191791)理论及其在[不连续性建模](@entry_id:165486)中的应用。通过本文的学习，您将掌握一种强大的计算工具，用以解决传统方法难以处理的复杂断裂问题。
*   在“**原理与机制**”一章中，我们将深入其核心的积分运动方程，剖析键断裂如何引发裂纹的自发涌现，并辨析键基与态基等不同本构模型的特点与联系。
*   随后，在“**应用与跨学科交叉**”一章中，我们将展示该理论如何从[断裂力学](@entry_id:141480)的前沿应用，扩展到热、流、化等多物理场耦合问题，以及在地球科学和[多尺度建模](@entry_id:154964)中的强大潜力。
*   最后，在“**动手实践**”部分，我们提供了一系列精心设计的计算练习，旨在帮助您将理论知识转化为解决实际问题的能力，加深对数值稳定性、[能量守恒](@entry_id:140514)和表面效应等关键概念的理解。

让我们首先进入第一章，探索[近场动力学](@entry_id:191791)赖以建立的数学原理与物理机制。

## 原理与机制

在上一章中，我们介绍了[近场动力学](@entry_id:191791)（Peridynamics）作为一种非局部[连续介质力学](@entry_id:155125)理论的背景和动机。本章我们将深入探讨其核心的数学原理和物理机制。我们将从其独特的运动方程出发，阐明它如何从根本上改变我们对[材料变形](@entry_id:169356)和断裂的建模方式。我们将详细剖析不同的[近场动力学](@entry_id:191791)[本构模型](@entry_id:174726)，并建立它们与经典理论之间的联系，最终探讨一些高级应用中出现的关键问题。

### [近场动力学](@entry_id:191791)运动方程：非局部相互作用的数学表达

经典[连续介质力学](@entry_id:155125)（Classical Continuum Mechanics, CCM）的基石是[偏微分方程](@entry_id:141332)，它假设物[质点](@entry_id:186768)只与其无限邻近的点发生直接相互作用。这种局部性假设在处理[不连续性](@entry_id:144108)（如裂纹）时会遇到根本性困难，因为[位移场](@entry_id:141476)的空间导数在不连续处是未定义的。

[近场动力学](@entry_id:191791)通过一个核心思想绕开了这一限制：它用一个积分方程取代了经典的[偏微分方程](@entry_id:141332)。该理论假设，在一个被称为**视域（horizon）**的有限邻域 $\mathcal{H}_{\boldsymbol{x}}$ 内，材料点 $\boldsymbol{x}$ 与其邻域内的所有点 $\boldsymbol{x}'$ 都存在直接的、非局部的相互作用。这些相互作用力，即**“键”（bonds）**，的总和决定了点 $\boldsymbol{x}$ 的运动。

根据牛顿第二定律，一个物[质点](@entry_id:186768) $\boldsymbol{x}$ 的[运动方程](@entry_id:170720)可以写作：
$$
\rho(\boldsymbol{x})\ddot{\boldsymbol{u}}(\boldsymbol{x},t) = \int_{\mathcal{H}_{\boldsymbol{x}}} \boldsymbol{f}\big(\boldsymbol{u}(\boldsymbol{x}',t)-\boldsymbol{u}(\boldsymbol{x},t), \boldsymbol{x}'-\boldsymbol{x}\big)\,\mathrm{d}V_{\boldsymbol{x}'} + \boldsymbol{b}(\boldsymbol{x},t)
$$
其中：
- $\rho(\boldsymbol{x})$ 是在参考构型中的质量密度。
- $\boldsymbol{u}(\boldsymbol{x},t)$ 是[位移矢量场](@entry_id:196067)。
- $\ddot{\boldsymbol{u}}(\boldsymbol{x},t)$ 是[局部加速度](@entry_id:272847)。
- $\boldsymbol{b}(\boldsymbol{x},t)$ 是外部体积力密度（如重力）。
- 积分项代表了在点 $\boldsymbol{x}$ 处所有内部相互作用力的合力密度。

这个方程的核心是**成对力函数（pairwise force function）** $\boldsymbol{f}$。它描述了位于 $\boldsymbol{x}'$ 的物质点对位于 $\boldsymbol{x}$ 的物[质点](@entry_id:186768)施加的力密度。至关重要的是，该函数仅依赖于两点之间的**相对位移** $\boldsymbol{\eta} = \boldsymbol{u}(\boldsymbol{x}',t)-\boldsymbol{u}(\boldsymbol{x},t)$ 和它们的**初始相对位置** $\boldsymbol{\xi} = \boldsymbol{x}'-\boldsymbol{x}$ 。这种对相对位移的依赖性确保了模型在刚体平移下的伽利略不变性，这是任何物理上合理的力学理论都必须满足的基本要求。

视域 $\mathcal{H}_{\boldsymbol{x}}$ 通常是一个以 $\boldsymbol{x}$ 为中心、半径为 $\delta$ 的球形区域。这个半径 $\delta$ 被称为**视域尺寸（horizon size）**，它是一个内禀的长度[尺度参数](@entry_id:268705)，定义了非局部相互作用的范围。对于任何固定的 $\delta > 0$，[近场动力学](@entry_id:191791)模型都是非局部的，因为点 $\boldsymbol{x}$ 的响应取决于其有限邻域内的位移场，而不仅仅是其无限邻近的导数 。

### 不连续性的自然表达：积分算子的力量

[近场动力学](@entry_id:191791)[运动方程](@entry_id:170720)最深刻的意义在于它处理不连续性的方式。经典运动方程包含应力[张量的散度](@entry_id:191736) $\nabla \cdot \boldsymbol{\sigma}$，而应力又依赖于[位移梯度](@entry_id:165352) $\nabla \boldsymbol{u}$。当[位移场](@entry_id:141476) $\boldsymbol{u}$ 存在跳跃不连续（即裂纹）时，其梯度在数学上会变成一个没有经典函数值的狄拉克$\delta$[分布](@entry_id:182848)，使得经典方程在该处失效。

相比之下，[近场动力学](@entry_id:191791)方程中的积分算子仅涉及位移值的差，而非其导数。为了使积分有意义，我们对位移场 $\boldsymbol{u}$ 的正则性要求远低于可微性。从[测度论](@entry_id:139744)的角度来看，只要 $\boldsymbol{u}$ 是可测的，且 $\boldsymbol{f}$ 在 $\mathcal{H}_{\boldsymbol{x}}$ 上是可积的，该积分就是良定义的。在三维空间中，一个裂纹面是一个二维表面，其[勒贝格测度](@entry_id:139781)（Lebesgue measure）为零。这意味着即使位移场 $\boldsymbol{u}$ 跨越裂纹面是不连续的，这个不连续的集合在积分域中的“体积”为零，因此不会影响积分的值。积分值由被积函数在“[几乎处处](@entry_id:146631)”的值决定。

因此，[近场动力学](@entry_id:191791)方程天然地**容纳（admit）**了位移[不连续性](@entry_id:144108)，而无需像[有限元法](@entry_id:749389)（FEM）那样引入特殊的[裂纹尖端单元](@entry_id:748033)，或像[扩展有限元法](@entry_id:162867)（XFEM）那样引入额外的浓缩函数。裂纹的形成和扩展成为模型内在演化的自然结果，而不是需要外部算法追踪的人为设定 。

### [断裂建模](@entry_id:752065)：裂纹的自发涌现

[近场动力学](@entry_id:191791)中材料的失效和断裂是通过**“键断裂”（bond breaking）**来建模的。这个概念直观且强大。

我们定义一个标量**键伸长率（bond stretch）** $s$，它度量了连接点 $\boldsymbol{x}$ 和 $\boldsymbol{x}'$ 的键的相对变形程度。当某个键的伸长率 $s$ 超过一个材料固有的临界值 $s_c$ 时，这个键就发生不可逆的断裂。在数学上，这意味着该键的成对力函数 $\boldsymbol{f}$ 将永久地被设置为零 。

在这个框架下，一条**裂纹并非一个预先定义的几何实体，而是一个“涌现”的现象**。它是在加载过程中，由一系列断裂的键所构成的区域。当一个区域内足够多的键断裂后，它们便无法再传递拉力。如果所有跨越某个假想[曲面](@entry_id:267450)的键都断裂了，那么这个[曲面](@entry_id:267450)两侧的物[质点](@entry_id:186768)之间就不再有任何力学耦合。这自然就形成了一个宏观的裂纹，其表面是无牵[引力](@entry_id:175476)的 。

我们可以将材料的非局部相互作用网络想象成一个**图（graph）**，其中材料点是顶点，完好的键是边。材料损伤的演化过程就对应于图中边的移除，从而改变了图的拓扑结构。当一个“切割集”（cut set）的边被移除，将[图分割](@entry_id:152532)成两个或多个不连通的[子图](@entry_id:273342)时，一个宏观裂纹就形成了。这种分离允许[位移场](@entry_id:141476)在切割面上产生跳跃，从而定义了裂纹面 。

这种自发的裂纹形成机制是[近场动力学](@entry_id:191791)最引人注目的优点之一，它能够自主预测复杂的[断裂模式](@entry_id:165801)，如[裂纹分叉](@entry_id:193371)、弯曲和聚合，而无需任何关于裂纹路径的先验假设。视域尺寸 $\delta$ 在此过程中扮演了关键角色，它不仅定义了相互作用的范围，还充当了一个正则化参数。在经典[断裂力学](@entry_id:141480)中，裂纹尖端存在[应力奇异性](@entry_id:166362)。而在[近场动力学](@entry_id:191791)中，由于力的计算是基于视域内的平均效应，这种奇异性被自然地抹平了。可以证明，由[近场动力学](@entry_id:191791)正则化产生的“过程区”尺寸与视域尺寸 $\delta$ 成正比，这为这个理论参数赋予了清晰的物理意义 。

### 本构模型：从键力到材料响应

成[对力](@entry_id:159909)函数 $\boldsymbol{f}$ 的具体形式定义了材料的本构行为。[近场动力学](@entry_id:191791)理论提供了不同层次的[本构模型](@entry_id:174726)。

#### 键基[近场动力学](@entry_id:191791) (Bond-Based Peridynamics)

最简单和最早期的模型是**键基（bond-based）**模型。在**线性微弹性（linear microelastic）**键基模型中，成对力被假定为**[中心力](@entry_id:267832)（central force）**，即力的方向始终沿着连接两点的键的方向 $\boldsymbol{e} = \boldsymbol{\xi}/|\boldsymbol{\xi}|$。其大小与键伸长率 $s$ 成正比 ：
$$
\boldsymbol{f}(\boldsymbol{\eta}, \boldsymbol{\xi}) = c(|\boldsymbol{\xi}|) s \boldsymbol{e}
$$
这里，$c(|\boldsymbol{\xi}|)$ 是一个**微观模量函数（micromodulus function）**，它描述了键的刚度，并且仅依赖于键的初始长度 $|\boldsymbol{\xi}|$。对于小变形，键伸长率定义为 $s = (\boldsymbol{\eta} \cdot \boldsymbol{e}) / |\boldsymbol{\xi}|$。

这个简单的模型具有一些优良的特性。由于成对力是中心力且满足作用力与反作用力定律（即 $\boldsymbol{f}(\boldsymbol{\eta}, \boldsymbol{\xi}) = -\boldsymbol{f}(-\boldsymbol{\eta}, -\boldsymbol{\xi})$），它自动满足[线动量](@entry_id:174467)和[角动量守恒](@entry_id:156798)，无需施加额外的本构约束。此外，存在一个微观[弹性势能](@entry_id:168893)，其对应于每个键的[应变能](@entry_id:162699)。对于上述[线性模型](@entry_id:178302)，总[应变能密度](@entry_id:200085)可以表示为邻域内所有键[应变能](@entry_id:162699)的积分 ：
$$
W(\boldsymbol{x},t) = \frac{1}{2}\int_{\mathcal{H}_{\boldsymbol{x}}} \frac{1}{2} c(|\boldsymbol{\xi}|) s^2 |\boldsymbol{\xi}| \,\mathrm{d}V_{\boldsymbol{x}'}
$$
然而，键基模型的中心力假设也带来了严重的局限性。在与经典弹性理论进行等效时，会发现该模型预测的泊松比 $\nu$ 是一个固定的值。对于三维各向同性材料，这个值被限制为 $\nu = 1/4$  。这意味着键[基模](@entry_id:165201)型无法描述具有其他泊松比值的材料，例如橡胶（$\nu \approx 0.5$）或多孔材料。

#### 态基[近场动力学](@entry_id:191791) (State-Based Peridynamics)

为了克服键基模型的局限性，**态基（state-based）**[近场动力学](@entry_id:191791)被提出。其核心思想是，作用在某个键上的力不再仅仅取决于该键自身的变形，而是依赖于该点视域内**所有键的集体变形状态**。

在态基模型中，我们引入**力态（force state）** $\underline{\mathbf{T}}$ 和**变形态（deformation state）** $\underline{\mathbf{Y}}$ 的概念 。变形态 $\underline{\mathbf{Y}}$ 是一个将邻域中每个键向量 $\boldsymbol{\xi}$ 映射到其在当前构型中对应向量 $\boldsymbol{y}(\boldsymbol{x}+\boldsymbol{\xi},t)-\boldsymbol{y}(\boldsymbol{x},t)$ 的算子。力态 $\underline{\mathbf{T}}$ 则是一个将每个键 $\boldsymbol{\xi}$ 映射到一个力密度向量 $\underline{\mathbf{T}}\langle\boldsymbol{\xi}\rangle$ 的算子。本构关系现在是力态和变形态之间的关系：$\underline{\mathbf{T}} = \mathcal{F}(\underline{\mathbf{Y}})$。

这种更通用的框架允许键力是非中心的，即 $\underline{\mathbf{T}}\langle\boldsymbol{\xi}\rangle$ 的方向可以不平行于 $\boldsymbol{\xi}$。这打破了键基模型的内在约束，使得态[基模](@entry_id:165201)型能够准确地再现任意[各向同性材料](@entry_id:170678)（即任意[泊松比](@entry_id:158876)）以及[各向异性材料](@entry_id:184874)的行为。然而，由于力不再是中心力，角动量守恒不再自动满足，必须作为一个额外的本构约束施加在力态上，通常形式为 $\int_{\mathcal{H}_{\boldsymbol{x}}} \boldsymbol{\xi} \times \underline{\mathbf{T}}\langle\boldsymbol{\xi}\rangle \, \mathrm{d}V_{\boldsymbol{\xi}} = \boldsymbol{0}$ 。

态[基模](@entry_id:165201)型分为**普通（ordinary）**和**非普通（non-ordinary）**两类。普通态基模型要求成[对力](@entry_id:159909)仍然满足作用力与[反作用](@entry_id:203910)力定律的强形式，而非普通模型则放宽了这一要求，为建模更复杂的材料（如考虑表面张力的流体）提供了更大的灵活性。

### 连接经典理论：校准与对应原理

一个力学理论的有效性不仅取决于其内部的自洽性，还取决于它与已被广泛验证的经典理论之间的联系。[近场动力学](@entry_id:191791)通过**局部极限（local limit）**和**本构[对应原理](@entry_id:155778)（constitutive correspondence）**与经典连续介质力学建立了坚实的桥梁。

#### 局部极限 ($\delta \to 0$)

当视域尺寸 $\delta$ 趋向于零时，[非局部模型](@entry_id:175315)在什么条件下会收敛到局部模型？对于一个足够光滑的[位移场](@entry_id:141476) $\boldsymbol{u}$，我们可以对其在点 $\boldsymbol{x}$ 处进行泰勒展开。将展开式代入[近场动力学](@entry_id:191791)[积分算子](@entry_id:262332)，我们可以研究其极限行为 。

研究表明，为了使[近场动力学](@entry_id:191791)算子收敛到经典的二阶微分算子（即应力散度），微观模量函数 $c(|\boldsymbol{\xi}|)$ 必须满足某些**[矩条件](@entry_id:136365)（moment conditions）** 。首先，函数 $c(|\boldsymbol{\xi}|)$ 必须是关于 $\boldsymbol{\xi}$ 的[偶函数](@entry_id:163605)，这保证了所有奇数阶矩（如一阶矩）由于对称性而消失，从而消除了非物理的一阶梯度项。其次，其关于空间测度的二阶矩必须是有限且非零的。这个条件保证了在 $\delta \to 0$ 的极限下，[积分算子](@entry_id:262332)能产生一个有限且非平凡的二阶[微分算子](@entry_id:140145)，其形式与经典弹性力学中的Navier算子一致。当然，这种收敛性只在光滑场中成立；在不连续处，局部极限是无定义的 。

#### 参数校准

为了使[近场动力学](@entry_id:191791)模型具有预测能力，其微观参数必须与材料的宏观属性（如[弹性模量](@entry_id:198862)和[断裂韧性](@entry_id:157609)）相关联。这种关联可以通过能量等效来建立。

例如，考虑一个处于均匀静水压力下的键基[近场动力学](@entry_id:191791)材料。通过计算该变形状态下的总[应变能密度](@entry_id:200085)，并将其与经典弹性理论中的[应变能密度](@entry_id:200085) $W_{CL} = \frac{1}{2}K\theta^2$（其中 $K$ 是体积模量，$\theta$ 是[体积应变](@entry_id:267252)）进行比较，我们可以推导出体积模量 $K$ 与微观模量 $c(r)$ 之间的精确关系 ：
$$
K = \frac{2\pi}{3} \int_{0}^{\delta} c(r) r^4 \,\mathrm{d}r
$$
同样，我们可以将断裂过程中的[能量耗散](@entry_id:147406)与宏观的**断裂能（fracture energy）** $G_c$ 联系起来。通过计算断开一个单位面积裂纹所穿过的所有键所需的总能量，并将其等同于 $G_c$，我们可以得到临界键伸长率 $s_c$ 与 $G_c$ 和 $c(r)$ 之间的关系 ：
$$
s_c = \sqrt{\frac{2 G_c}{\pi \int_0^\delta c(r) r^4 dr}}
$$
这些关系式使得我们能够通过实验测量的宏观材料常数来校准[近场动力学](@entry_id:191791)模型中的微观参数。

#### 本构对应原理

在态基模型中，**本构[对应原理](@entry_id:155778)（correspondence principle）**提供了一种更直接、更强大的方法来利用经典的本构关系 。其核心思想是，尽管[位移梯度](@entry_id:165352)在裂纹处无定义，我们仍然可以在每个点 $\boldsymbol{x}$ 的视域内，通过一个[加权最小二乘法](@entry_id:177517)来计算一个“最佳拟合”的**非局部变形梯度** $\mathbf{F}(\boldsymbol{x})$。
$$
\mathbf{F}(\boldsymbol{x}) = \left( \int_{\mathcal{H}_{\boldsymbol{x}}} \omega(|\boldsymbol{\xi}|) \, \underline{\mathbf{Y}}\langle \boldsymbol{\xi} \rangle \otimes \boldsymbol{\xi} \, dV' \right) \mathbf{K}^{-1}(\boldsymbol{x})
$$
其中，$\omega(|\boldsymbol{\xi}|)$ 是一个[影响函数](@entry_id:168646)，而 $\mathbf{K}(\boldsymbol{x})$ 是一个被称为**形状张量（shape tensor）**的几何量，它只依赖于邻域的初始构型：
$$
\mathbf{K}(\boldsymbol{x}) = \int_{\mathcal{H}_{\boldsymbol{x}}} \omega(|\boldsymbol{\xi}|) \, \boldsymbol{\xi} \otimes \boldsymbol{\xi} \, dV'
$$
一旦获得了非局部变形梯度 $\mathbf{F}(\boldsymbol{x})$，我们就可以像在经典力学中一样计算应变张量 $\boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$（对于[大变形](@entry_id:167243)）或 $\boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{F}+\mathbf{F}^T) - \mathbf{I}$（对于小变形）。然后，我们可以直接使用任何经典的[本构定律](@entry_id:178936)（例如，[胡克定律](@entry_id:149682) $\boldsymbol{\sigma} = \mathbf{C}:\boldsymbol{\varepsilon}$）来计算应力。最后，这个应力被用来构造[近场动力学](@entry_id:191791)力态 $\underline{\mathbf{T}}$。

这种方法的优越性在于，它允许我们将数十年积累的经典本构模型知识直接应用于[近场动力学](@entry_id:191791)框架，同时保留了该框架处理[不连续性](@entry_id:144108)的能力。

### 高级主题：[体积锁定](@entry_id:172606)与稳定化

尽管[对应模](@entry_id:200367)型非常强大，但在处理某些特定问题时，尤其是在数值实现中，也会面临挑战。一个典型的问题是**[体积锁定](@entry_id:172606)（volumetric locking）**，它发生在模拟**[近不可压缩材料](@entry_id:752388)**（即泊松比 $\nu$ 接近 $0.5$）时。

在[近不可压缩](@entry_id:752387)极限下，体积模量 $K$ (或拉梅参数 $\lambda$) 趋于无穷大，对体积变形产生极大的“惩罚”。在[数值离散化](@entry_id:752782)中，即使在理论上应为零体积应变的变形模式（如纯剪切）下，由于离散误差（特别是在边界附近），也可能产生微小的、非物理的寄生[体积应变](@entry_id:267252)。标准[对应模](@entry_id:200367)型会忠实地将这些寄生应变转化为巨大的能量和应力，导致整个系统表现出远超其实际刚度的虚假刚度，即“锁定”现象。

为了解决这个问题，研究者们发展了多种稳定化技术，其思想借鉴自[有限元法](@entry_id:749389) 。
- **B-bar类方法**：这种方法将局部计算的体积应变替换为一个在更大范围（甚至全局）内平均的体积应变。由于寄生体积应变通常是正负交错的，平均过程可以显著地将它们抵消，从而减轻锁定。
- **[偏应变](@entry_id:201263)-体积应变分离（Deviatoric-Volumetric Split）**：这种方法将[应变能](@entry_id:162699)分解为形状改变部分（[偏应变](@entry_id:201263)能）和体积改变部分（体积应变能）。然后，只对更“软”的[偏应变](@entry_id:201263)部分使用标准模型，而对“硬”的体积部分采用经过特殊处理的、不易锁定的形式。一种极端的形式是**非普通态基[偏应变](@entry_id:201263)模型**，它在某些情况下完全忽略体积能，从而完全避免[体积锁定](@entry_id:172606)。

这些高级技术展示了[近场动力学](@entry_id:191791)作为一个活跃的研究领域，其理论和数值方法仍在不断发展和完善，以应对各种复杂的材料行为和物理现象。