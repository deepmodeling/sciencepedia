## 引言
守恒定律，作为描述质量、动量和能量在物理系统中如何保持不变的基本法则，构成了整个[连续介质力学](@entry_id:155125)，尤其是流体动力学的理论基石。对于航空航天领域的研究生而言，深刻理解这些定律的积分与[微分形式](@entry_id:146747)不仅是理论要求，更是准确分析和模拟高速[可压缩流](@entry_id:747589)动（如飞行器周围的激波和喷气发动机内的复杂流动）的先决条件。然而，一个核心的挑战在于：当流场中出现激波等不连续现象时，经典的[微分形式守恒律](@entry_id:166470)便不再适用，这给理论分析和[数值模拟](@entry_id:146043)带来了巨大的困难。

本文旨在系统性地解决这一问题。我们将带领读者深入探索[积分守恒律](@entry_id:202878)与[微分](@entry_id:158422)守恒律之间的深刻联系与本质区别。在“原理与机制”一章中，我们将从最基本的物理公理出发，推导这两种数学表述，并阐明为何积分形式在处理不连续解时更为根本，同时介绍[弱解](@entry_id:161732)、[Rankine-Hugoniot跳跃条件](@entry_id:139267)和[熵条件](@entry_id:166346)等关键概念。随后，在“应用与跨学科联系”一章中，我们将展示这些理论如何在[航空航天工程](@entry_id:268503)、[计算流体动力学](@entry_id:142614)（CFD）数值格式设计以及[交通流](@entry_id:165354)、[环境科学](@entry_id:187998)等多个交叉学科中发挥其强大的指导作用。最后，通过“动手实践”部分提供的精选练习，读者将有机会亲手应用这些原理，将理论知识转化为解决实际问题的能力。通过这一系列的学习，您将建立起对守恒定律的完整而深入的认识。

## 原理与机制

在本章中，我们将深入探讨构成[计算流体动力学](@entry_id:142614)（CFD）理论基石的积分形式与[微分形式守恒律](@entry_id:166470)。我们将从最基本的物理原理出发，建立起这两套表述之间的数学联系，并阐明为何这种联系在处理包含激波等不连续性的复杂航空航天流动问题时至关重要。此外，我们还将探讨这些原理如何直接指导我们构建能够准确捕捉物理现象的鲁棒数值格式。

### [积分守恒律](@entry_id:202878)与[微分](@entry_id:158422)守恒律的等价性与范畴

物理守恒律，例如质量、动量和能量守恒，其最普适的表述是基于一个有限大小的控制体（control volume）。考虑一个任意的[标量密度](@entry_id:161438) $\phi(\mathbf{x},t)$（例如单位体积的质量或能量），其在空间中的输运由一个通量矢量 $\mathbf{F}(\mathbf{x},t)$ 描述，同时还可能存在一个单位体积的源项 $S(\mathbf{x},t)$（例如化学反应产生的质量或外部热源）。对于一个固定的控制体 $\Omega$，其边界为 $\partial\Omega$，向外的[单位法向量](@entry_id:178851)为 $\mathbf{n}$，守恒原理断言：

控制体内 $\phi$ 总量的变化率，等于流出边界的净通量，加上体积内源项的总和。

这个物理陈述的数学表达即为**积分形式守恒律**：

$$
\frac{\partial}{\partial t}\int_{\Omega}\phi\,dV + \int_{\partial\Omega}\mathbf{F}\cdot\mathbf{n}\,dA = \int_{\Omega}S\,dV
$$

在此方程中，$\int_{\partial\Omega}\mathbf{F}\cdot\mathbf{n}\,dA$ 精确地代表了通过固定边界 $\partial\Omega$ 的 $\phi$ 的净流出率，它包含了所有输运机制（如对流和扩散）。而 $\int_{\Omega}S\,dV$ 则是整个控制体内 $\phi$ 的总生成率。

为了从这个宏观的、基于控制体的描述过渡到一个局部的、点态的描述，我们需要引入一些关于流动变量平滑性的假设。如果我们假定场变量 $\phi$、$\mathbf{F}$ 和 $S$ 是足够光滑的（例如，至少是 $C^1$ 连续的），我们就可以将时间导数移入积分号内，并应用**高斯散度定理**（Gauss's divergence theorem）将面积分转化为体积分：

$$
\int_{\Omega}\frac{\partial \phi}{\partial t}\,dV + \int_{\Omega}\nabla\cdot\mathbf{F}\,dV = \int_{\Omega}S\,dV
$$

将所有项合并到一个[体积分](@entry_id:171119)下，我们得到：

$$
\int_{\Omega}\left(\frac{\partial \phi}{\partial t} + \nabla\cdot\mathbf{F} - S\right)\,dV = 0
$$

这个[积分方程](@entry_id:138643)的美妙之处在于，[积分守恒律](@entry_id:202878)的原始公理要求它对**任意**形状和大小的控制体 $\Omega$ 都成立。如果一个连续函数在[任意子](@entry_id:143753)区域上的积分都为零，那么这个函数本身必然处处为零。这个强大的论证，被称为**变分法基本引理**（fundamental lemma of the calculus of variations）的变体，允许我们移除积分号，得到一个在空间每一点都必须满足的方程，这便是**[微分形式守恒律](@entry_id:166470)**：

$$
\frac{\partial \phi}{\partial t} + \nabla\cdot\mathbf{F} = S
$$

在这个局部方程中，$\nabla\cdot\mathbf{F}$ 的物理意义是通量的**散度**，它描述了在一个无穷小体积周围，[通量矢量](@entry_id:273577)场的汇聚或发散程度，从而决定了该点 $\phi$ 值的瞬时增加或减少。

因此，积分形式与[微分形式守恒律](@entry_id:166470)的等价性，是建立在一系列关键假设之上的  ：
1.  **普适性**：积分定律必须对所有（足够规则的）控制体成立。
2.  **平滑性**：场变量 $\phi$ 和 $\mathbf{F}$ 必须足够光滑，以保证时间导数与积分可以交换，且空间导数（即散度）存在，从而[高斯散度定理](@entry_id:188065)可以应用。对于经典推导，通常要求 $C^1$ 连续性。在更现代的[偏微分方程理论](@entry_id:189232)中，这些条件被放宽到[索博列夫空间](@entry_id:141995)（Sobolev spaces）的框架下，例如要求 $\mathbf{F} \in H(\mathrm{div}; \Omega)$，即 $\mathbf{F}$ 及其散度均在 $L^2$ 空间中。
3.  **几何规则性**：控制体的边界 $\partial\Omega$ 需要足够规则（例如，分片 $C^1$ 或更弱的 Lipschitz 边界），以确保高斯散度定理成立。

### [可压缩流](@entry_id:747589)动的守恒变量

在将上述通用框架应用于[可压缩流体](@entry_id:164617)动力学时，一个核心问题是：我们应该选择哪些变量作为守恒密度 $\phi$？答案并非任意，而是由物理定律的内在结构决定的。对于可压缩的牛顿流体，基本[守恒量](@entry_id:161475)是质量、动量和总能量。为了使它们的控制方程能够写成[散度形式](@entry_id:748608)（divergence form），我们必须选择一组特定的**守恒变量**。这个[守恒变量](@entry_id:747720)矢量 $\mathbf{q}$ 定义为：

$$
\mathbf{q} = \begin{bmatrix} \rho \\ \rho\mathbf{u} \\ \rho E \end{bmatrix}
$$

其中 $\rho$ 是流体密度，$\mathbf{u}$ 是[速度矢量](@entry_id:269648)，而 $E$ 是单位质量的总能量，定义为 $E = e + \frac{1}{2}\|\mathbf{u}\|^2$，即内能与动能之和 。

选择这组变量的根本原因在于，只有对于它们，质量、动量和总能量的[输运方程](@entry_id:174281)才能被精确地写成守恒形式 $\partial_t \mathbf{q} + \nabla \cdot \mathbf{F} = \mathbf{S}$，其中 $\mathbf{F}$ 是一个仅依赖于 $\mathbf{q}$（及其梯度，在[粘性流](@entry_id:136330)中）的通量张量。例如：
-   **[质量守恒](@entry_id:204015)**：$\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0$。这里 $q=\rho$，通量为 $\mathbf{F}=\rho\mathbf{u}$。
-   **[动量守恒](@entry_id:149964)**：$\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \otimes \mathbf{u} + p\mathbf{I} - \boldsymbol{\tau}) = \rho \mathbf{f}$。这里 $q=\rho\mathbf{u}$，通量包含了对流项、压力项和粘性应力项。
-   **总能量守恒**：$\frac{\partial (\rho E)}{\partial t} + \nabla \cdot ((\rho E + p)\mathbf{u} - \boldsymbol{\tau} \cdot \mathbf{u} + \mathbf{q}_{h}) = \rho \mathbf{f} \cdot \mathbf{u} + \dot{q}$。这里 $q=\rho E$，通量包含了能量的对流、压力功、[粘性耗散](@entry_id:143708)功和[热传导](@entry_id:143509)。

这种[守恒形式](@entry_id:1122899)是至关重要的。因为它保证了当我们对任意控制体进行积分时，通过应用散度定理，体内总量的变化仅取决于通过边界的通量和显式的源项。这直接对应于物理守恒的原始定义 。

特别值得注意的是总能量的使用。如果我们试图为内能 $\rho e$ 写一个[守恒方程](@entry_id:1122898)，我们会发现方程中会出现诸如 $-p(\nabla \cdot \mathbf{u})$ 这样的项，它代[表压力](@entry_id:147760)做功，但不能被写成某个通量的散度。然而，当我们考虑动能方程时，会出现一个对应的项 $-\mathbf{u} \cdot \nabla p$。令人惊奇的是，这两项之和 $-p(\nabla\cdot\mathbf{u}) - \mathbf{u}\cdot\nabla p = -\nabla\cdot(p\mathbf{u})$，恰好是一个完整的散度项！因此，通过将内能和动能打包成总能量 $E$，那些“非守恒”的源项神奇地组合成了一个守恒的通量项。这就是为什么必须使用 $\rho E$ 而不是 $\rho e$ 作为守恒变量，以获得一个纯粹的[守恒形式方程](@entry_id:1122915) 。

与守恒变量 $\mathbf{q}$ 相对的是**[原始变量](@entry_id:753733)**（primitive variables），通常指 $[\rho, \mathbf{u}, p]^T$。用[原始变量](@entry_id:753733)写出的方程包含非守恒乘积项（如对流项 $(\mathbf{u} \cdot \nabla)\mathbf{u}$），它们不具备[散度结构](@entry_id:748609)。虽然在数学上是等价的（对于光滑解），但在数值离散和处理不连续解时，这种差异会产生深刻的后果。

### 不连续解：[弱解](@entry_id:161732)与跳跃条件

在高速[可压缩流](@entry_id:747589)中，如航空航天应用中常见的激波和接触间断，流场是**不连续**的。在这些[不连续面](@entry_id:180188)上，经典导数不存在，[微分形式](@entry_id:146747)的守恒律失去了意义。然而，流体依然遵守基本的物理守恒。这表明，积分形式的守恒律是更基本、更普适的表述。

当解不光滑时，我们引入**[弱解](@entry_id:161732)**（weak solution）的概念。一个函数 $u$ 被称为守恒律 $\partial_t u + \partial_x f(u) = 0$ 的[弱解](@entry_id:161732)，如果对于所有光滑且具有[紧支集](@entry_id:276214)的“[检验函数](@entry_id:166589)” $\varphi(x,t)$，以下积分等式成立 ：
$$
\int_0^\infty \int_{\mathbb{R}} \left( u \, \partial_t \varphi + f(u) \, \partial_x \varphi \right) \, dx \, dt + \int_{\mathbb{R}} u_0(x) \, \varphi(x,0) \, dx = 0
$$
这个定义是通过将原[偏微分](@entry_id:194612)方程乘以检验函数并进行分部积分得到的，巧妙地将导数从可能不存在的解 $u$ 转移到了无限光滑的检验函数 $\varphi$ 上。重要的是，这个[弱形式](@entry_id:142897)的定义与“对所有控制体 $[a,b]$ 和时间区间 $[t_1, t_2]$ [积分守恒律](@entry_id:202878)都成立”是等价的 。

那么，在不连续面上，守恒律体现为什么形式呢？它不再是一个[偏微分](@entry_id:194612)方程，而是一个代数关系，称为**跳跃条件**（jump condition）或**Rankine–Hugoniot条件**。我们可以通过对一个跨越间断面的、无限薄的“药盒”（pillbox）控制体应用[积分守恒律](@entry_id:202878)来推导它 。

考虑一个以法向速度 $V_n$ 运动的间断面 $\Sigma(t)$，其法向量为 $\mathbf{n}$。当“药盒”的厚度趋于零时，[体积分](@entry_id:171119)的变化率项和面积分的通量项都与“药盒”的底面积成正比。二者必须相互平衡。时间导数项变为 $-V_n \llbracket \phi \rrbracket$，表示[间断面](@entry_id:180188)扫过单位面积时，由于 $\phi$ 的跳跃 $\llbracket \phi \rrbracket = \phi_{+} - \phi_{-}$ 导致的量的变化。通量项则变为法向通量的跳跃 $\llbracket \mathbf{F} \cdot \mathbf{n} \rrbracket$。两[相平衡](@entry_id:136822)得到普适的[Rankine-Hugoniot条件](@entry_id:181986)：

$$
V_n \llbracket \phi \rrbracket = \llbracket \mathbf{F} \cdot \mathbf{n} \rrbracket
$$

或者写成更紧凑的形式 $\llbracket \mathbf{F}\cdot \mathbf{n} - \phi V_n \rrbracket = 0$，这表明相对于运动[间断面](@entry_id:180188)自身的通量是连续的 。这个[代数方程](@entry_id:272665)代替了[微分](@entry_id:158422)方程，成为了在[间断面](@entry_id:180188)上必须满足的守恒定律。对于[可压缩欧拉方程](@entry_id:747588)组，这意味着质量、动量和总能量的法向通量跳跃与它们各自密度的跳跃和激波速度相关联。

### 物理[可实现性](@entry_id:193701)：熵条件

[Rankine-Hugoniot条件](@entry_id:181986)本身是纯代数的，它可能会允许多个数学上可能的解。例如，它既允许压力增加的压缩激波，也允许压力减小的膨胀激波。然而，物理世界的经验和[热力学](@entry_id:172368)第二定律告诉我们，[孤立系统](@entry_id:159201)中的[自发过程](@entry_id:137544)总是朝着熵增加的方向进行。激波是一个高度不可逆的耗散过程，因此流体穿越激波时，其熵必须增加（或在极限情况下保持不变）。膨胀激波会导致熵减少，因此是不符合物理规律的 。

这个物理约束被称为**[熵条件](@entry_id:166346)**（entropy condition）。它作为附加准则，用于从[Rankine-Hugoniot条件](@entry_id:181986)的多个解中筛选出唯一符合物理现实的解。数学上，这一原则被表述为一个**[熵不等式](@entry_id:184404)**。对于一个凸的熵函数 $\eta(\mathbf{q})$（例如，对于理想气体，可以选择 $\eta = -\rho s$，其中 $s$ 是比熵），物理上可实现的[弱解](@entry_id:161732)必须满足：

$$
\partial_{t}\eta(\mathbf{q}) + \nabla \cdot \mathbf{q}_{\eta}(\mathbf{q}) \le 0
$$

其中 $\mathbf{q}_{\eta}$ 是对应的熵通量。这个不等式需要在分布意义上成立。这个条件的严格数学 justification 来自于**[消失粘性法](@entry_id:177856)**（vanishing viscosity method）：人们证明，当[Navier-Stokes](@entry_id:276387)方程中的粘性和热导系数趋于零时，其解会收敛到[欧拉方程](@entry_id:177914)的[弱解](@entry_id:161732)，而这个[弱解](@entry_id:161732)恰好满足上述[熵不等式](@entry_id:184404) 。因此，[积分守恒律](@entry_id:202878)本身不足以保证[解的唯一性](@entry_id:143619)；必须辅以[熵条件](@entry_id:166346)才能构成一个适定的问题。

### 从连续到离散：[数值守恒](@entry_id:175179)性

守恒律的理论对于构建可靠的[CFD方法](@entry_id:747237)具有决定性的指导意义。**[有限体积法](@entry_id:141374)**（Finite Volume Method, FVM）是这一思想最直接的体现。FVM直接离散积分形式的守恒律：

$$
\frac{d}{dt}\int_{V_i}\mathbf{q}\,dV + \int_{\partial V_i} \mathbf{F}(\mathbf{q})\cdot \mathbf{n}\,dA = \mathbf{0}
$$

对于网格单元 $V_i$，其 cell-averaged [守恒量](@entry_id:161475) $\mathbf{q}_i$ 的变化率由通过其所有面 $f \in \partial V_i$ 的数值通量之和决定：

$$
|V_i|\frac{d\mathbf{q}_i}{dt} = -\sum_{f \in \partial V_i} \hat{\mathbf{F}}_f |S_f|
$$

一个数值格式要做到**守恒**，关键在于其对界面通量的处理。对于任意一个内部界面 $f$，它被两个相邻的单元 $i$ 和 $j$ 共享。从单元 $i$ 的角度看，流出界面的通量为 $\hat{\mathbf{F}}_{ij}$；从单元 $j$ 的角度看，流入的通量为 $\hat{\mathbf{F}}_{ji}$。一个**守恒的数值格式**必须保证，对于同一个界面，一个单元计算的流出量精确等于相邻单元计算的流入量 。在实践中，这意味着为每个界面计算一个**单一的、唯一的通量值** $\hat{\mathbf{F}}_f$，然后将这个值加到其中一个单元的残差上，同时从另一个单元的残差中减去它。

这种设计保证了当我们将所有单元的方程加起来时，所有内部界面的通量贡献会像“伸缩求和”（telescoping sum）一样精确抵消。因此，整个计算域内[守恒量](@entry_id:161475)的总变化，仅取决于通过域边界的通量，完美地模拟了宏观物理守恒。

这一特性对于正确捕捉激波至关重要。著名的**[Lax-Wendroff定理](@entry_id:751184)**指出，如果一个[守恒格式](@entry_id:747714)的数值解收敛，那么它必然收敛到一个真实的[弱解](@entry_id:161732)。这意味着，只要格式是守恒的，它就能自动满足正确的[Rankine-Hugoniot跳跃条件](@entry_id:139267)，从而得到正确的激[波速](@entry_id:186208)度和强度，而与网格是否对齐激波无关 。相反，采用[非守恒形式](@entry_id:1128837)（如基于[原始变量](@entry_id:753733)的有限差分法）的格式，由于离散[乘法法则](@entry_id:144424)的误差，无法保证通量的精确抵消，即使解看起来稳定并收敛，也可能收敛到一个违反[Rankine-Hugoniot条件](@entry_id:181986)的[伪解](@entry_id:275285)，导致激波位置和强度的严重错误。

### 高级主题与推广

#### [移动控制体](@entry_id:265261)与ALE方法

在许多航空航天问题中，例如机翼[颤振](@entry_id:749473)或弹射物分离，计算域的边界会随时间运动。此时，我们需要使用**任意拉格朗日-欧拉**（Arbitrary Lagrangian-Eulerian, ALE）方法。其理论基础是适用于移动和变形控制体 $\mathcal{V}(t)$ 的**雷诺输运定理**（Reynolds Transport Theorem, RTT）。当控制体边界以速度 $\mathbf{w}$ 运动时，$\mathcal{V}(t)$ 内 $\phi$ 总量的变化率由两部分构成：一部分是由于场 $\phi$ 自身的非定常变化，另一部分是由于边界运动扫过流体而引起的通量。

将物理守恒律 $\partial_t \phi + \nabla\cdot(\phi\mathbf{u}) = 0$（这里以对流通量为例）与RTT结合，可以得到ALE框架下的[积分守恒律](@entry_id:202878) ：

$$
\frac{d}{dt}\int_{\mathcal{V}(t)} \phi\, dV + \int_{\partial\mathcal{V}(t)} \phi\,(\mathbf{u}-\mathbf{w})\cdot\mathbf{n}\, dA = 0
$$

这里的关键在于，跨越移动边界的有效通量，是由流体相对于边界的运动速度 $(\mathbf{u}-\mathbf{w})$ 决定的。这个形式是ALE有限体积格式的出发点。

#### [离散守恒](@entry_id:1123819)的精妙之处

即使在连续层面代数等价的方程形式，在离散后也可能表现出截然不同的性质。以[不可压缩流](@entry_id:140301)动的动量方程中的[非线性](@entry_id:637147)对流项为例，它可以写成多种形式：
-   **守恒形式**: $\nabla \cdot (\mathbf{u} \otimes \mathbf{u})$
-   **平流形式**: $(\mathbf{u} \cdot \nabla) \mathbf{u}$
-   **斜对称形式**: $\frac{1}{2} [\nabla \cdot (\mathbf{u} \otimes \mathbf{u}) + (\mathbf{u} \cdot \nabla) \mathbf{u}]$

在连续且不可压缩（$\nabla \cdot \mathbf{u} = 0$）的条件下，这三者完[全等](@entry_id:273198)价。然而，当使用中心差分等满足[分部求和](@entry_id:755630)（summation-by-parts）性质的离散算子时，它们的离散性质迥异 。可以证明，只有**斜对称形式**才能在离散层面精确地 conserving 动能，即其对离散动能变化率的贡献为零。[守恒形式](@entry_id:1122899)和平流形式都会因为混淆误差（aliasing error）而产生虚假的动能生成或耗散。在需要精确捕捉能量级联过程的[湍流模拟](@entry_id:1133511)等应用中，选择这种[动能守恒](@entry_id:177660)的离散格式至关重要，它能显著增强数值格式的长期稳定性和物理保真度。这揭示了在从连续到离散的转化过程中，深刻理解守恒律的离散对应物是何等重要。