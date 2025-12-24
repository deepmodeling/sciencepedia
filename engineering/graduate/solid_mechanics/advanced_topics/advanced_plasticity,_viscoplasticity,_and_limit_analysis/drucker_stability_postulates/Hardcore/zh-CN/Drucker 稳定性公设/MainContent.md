## 引言
在固体力学领域，构建能够准确描述材料行为的本构模型至关重要。然而，一个数学上可行的模型如何能保证其在物理上是合理的？特别是在处理金属、土壤等材料的非弹性行为时，我们如何确保模型不会违反[能量守恒](@entry_id:140514)等基本物理定律，并能导出在数学上适定的边值问题？[Drucker稳定性公设](@entry_id:200080)为解决这一核心问题提供了一套强有力且影响深远的准则。它不仅是抽象的理论约束，更是连接材料微观耗散与宏观结构响应的桥梁，构成了现代塑性力学的基石。

本文旨在全面系统地阐述[Drucker稳定性公设](@entry_id:200080)。我们将从以下三个层面展开：
*   在“**原理与机制**”一章中，我们将深入探讨公设的基本陈述、深刻的[热力学](@entry_id:141121)背景，以及其在数学上如何导出[屈服面凸性](@entry_id:756808)、关联流动法则等关键推论，并解释其在保证[边值问题](@entry_id:193901)解唯一性中的作用。
*   在“**应用与跨学科联系**”一章中，我们将展示这些原理如何在更广泛的工程问题中发挥作用，包括其在结构[极限分析](@entry_id:188743)与安定理论中的核心地位，以及如何利用它来理解和预测非[关联材料](@entry_id:138171)和软化材料中的失稳与[应变局部化](@entry_id:176973)现象。
*   最后，在“**动手实践**”部分，通过一系列精心设计的算例，读者将有机会亲手验证和应用这些理论概念，从而将抽象的原理转化为解决实际问题的能力。

通过本次学习，你将建立起对[材料稳定性](@entry_id:183933)的深刻理解，并掌握评估和构建物理上合理的[本构模型](@entry_id:174726)的核心工具。

## 原理与机制

在非弹性[材料力学](@entry_id:201885)中，保证[本构模型](@entry_id:174726)的物理合理性和数学上的[适定性](@entry_id:148590)至关重要。[Drucker稳定性公设](@entry_id:200080)为此提供了一套强有力的准则。这些公设最初是为了确保准静态加载下[弹塑性](@entry_id:193198)边值问题[解的唯一性](@entry_id:143619)而提出的，但其内涵远不止于此，深刻地揭示了材料耗散行为的内在约束。本章将系统阐述[Drucker公设](@entry_id:180546)的基本原理、[热力学](@entry_id:141121)基础、数学推论及其应用。

### 基本公设的陈述

[Drucker公设](@entry_id:180546)是对材料在增量加载-卸载循环中的耗散行为施加的约束。对于速率无关的[弹塑性](@entry_id:193198)材料，这些公设可以方便地以率形式或增量形式表达。在小应变理论框架下，我们通常会遇到两种主要形式的公设。

第一种，也是最基本的形式，有时被称为**Drucker第一公设**或[最大塑性耗散](@entry_id:184825)公设。它要求在任何产生[塑性流动](@entry_id:201346)的过程中，应力在塑性应变增量上所做的功（即塑性功增量）必须是非负的。对于一个给定的应力状态 $\boldsymbol{\sigma}$，如果发生了塑性应变增量 $\delta\boldsymbol{\varepsilon}^p$，那么：

$$
\delta W^p = \boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon}^p \ge 0
$$

此处，$:$ 表示张量的[双点积](@entry_id:748648)。这个条件  的物理意义是，材料的塑性变形过程是一个耗散过程，它不会自发地对外做功。这个公设与一个包含原点的[凸屈服面](@entry_id:203690)和关联[流动法则](@entry_id:177163)紧密相关。

第二种形式，被称为**Drucker第二公设**或严格意义上的稳定性公设，对材料的硬化行为施加了更强的限制。它要求在任何引起塑性流动的加载增量中，应力增量 $\delta\boldsymbol{\sigma}$ 在相应的塑性应变增量 $\delta\boldsymbol{\varepsilon}^p$ 上所做的功必须是非负的：

$$
\delta\boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon}^p \ge 0
$$

这个条件也被称为**硬化公设**，因为它排除了[应变软化](@entry_id:755491)行为，即材料在塑性变形过程中抵抗力下降的现象。对于[理想塑性](@entry_id:753335)材料，该表达式取等号，即 $\delta\boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon}^p = 0$。

这两种公设共同构成了材料在Drucker意义上稳定的基础。它们不仅是抽象的数学约束，更有着深刻的物理和[热力学](@entry_id:141121)背景。

### [热力学](@entry_id:141121)基础与物理诠释

[Drucker公设](@entry_id:180546)的合理性根植于热力学第二定律，但它提出了比基本[热力学约束](@entry_id:755911)更严格的要求。对于[等温过程](@entry_id:143096)，局部形式的[Clausius-Duhem不等式](@entry_id:193424)（即[耗散不等式](@entry_id:188634)）要求力学[耗散率](@entry_id:748577) $\mathcal{D}$ 必须非负：

$$
\mathcal{D} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$

其中 $\boldsymbol{\sigma}$ 是柯西应力，$\dot{\boldsymbol{\varepsilon}}$ 是总应变率，$\dot{\psi}$ 是单位体积亥姆霍兹自由能（代表储存能）的变化率。对于一个标准的[弹塑性](@entry_id:193198)模型，总应变可以分解为弹性部分 $\boldsymbol{\varepsilon}^e$ 和塑性部分 $\boldsymbol{\varepsilon}^p$，即 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p$。如果我们假设自由能仅是弹性应变和一组内变量（如硬化参数）的函数 $\psi(\boldsymbol{\varepsilon}^e, \boldsymbol{\alpha})$，并且应力是自由能对[弹性应变](@entry_id:189634)的[偏导数](@entry_id:146280) $\boldsymbol{\sigma} = \partial\psi/\partial\boldsymbol{\varepsilon}^e$，那么[耗散不等式](@entry_id:188634)可以被简化 。

代入[应变率](@entry_id:154778)分解 $\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p$ 和自由能变化率 $\dot{\psi} = (\partial\psi/\partial\boldsymbol{\varepsilon}^e):\dot{\boldsymbol{\varepsilon}}^e + (\partial\psi/\partial\boldsymbol{\alpha})\cdot\dot{\boldsymbol{\alpha}} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^e + \dots$，我们发现总的力学耗散主要由[塑性流动](@entry_id:201346)贡献：

$$
\mathcal{D} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p - (\text{与硬化相关的能量储存率}) \ge 0
$$

在最简单的情况下（没有与[硬化](@entry_id:177483)相关的能量储存），热力学第二定律直接要求塑性功率非负，即 $\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p \ge 0$。这与Drucker第一公设完全一致。它表明，塑性变形是一个不可逆的能量耗散过程。

这一点的物理意义在于，材料是**被动**的。在一个封闭的加载-卸载循环中（即所有状态变量，包括应力、应变和内部变量，都回到初始值），对被动材料所做的净功必须是非负的，即 $W_{\mathcal{C}} = \oint \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon} \ge 0$。如果 $W_{\mathcal{C}}  0$，意味着材料在一个循环中向外界输出了净能量，这构成了一种[第二类永动机](@entry_id:139670)，是物理上不允许的 。[Drucker公设](@entry_id:180546)通过在微观增量层面施加约束，确保了这种宏观上的不可能性。

相比之下，对于纯弹性材料，其响应是保守的，应力是应变[势能的梯度](@entry_id:173126)，因此在任何闭合循环中做的净功恒为零，$W_{\mathcal{C}} = \oint \mathrm{d}\psi = 0$ 。另一方面，对于**[活性材料](@entry_id:139916)**（如[肌肉组织](@entry_id:145481)或某些[智能材料](@entry_id:196298)），它们内部有能量源（如化学能），可以在一个循环中对外做净功（$W_{\mathcal{C}}  0$）。这种行为不违反[热力学定律](@entry_id:202285)，因为它消耗了内部储存的非[机械能](@entry_id:162989)，但这显然超出了被动材料的范畴，[Drucker公设](@entry_id:180546)也就不再适用 。

因此，我们可以更形式化地区分**Drucker[材料稳定性](@entry_id:183933)**和**热力学稳定性**。热力学稳定性通常通过系统的某个全局状态函数（如Lyapunov函数）的演化来描述。例如，对于一个孤立的绝热系统，总熵 $S$ 永不减少（$\dot{S} \ge 0$）；对于等温[封闭系统](@entry_id:139565)，总[亥姆霍兹自由能](@entry_id:136442) $F$ 永不增加（$\dot{F} \le 0$）。而Drucker稳定性是一个更强的、施加在本构关系上的力学条件，它要求塑性功的非负性以及本构映射的单调性，以确保力学响应的稳定。仅仅满足[热力学第二定律](@entry_id:142732)（即 $\mathcal{D} \ge 0$）并不足以保证Drucker稳定性 。

### 数学推论：[屈服面](@entry_id:175331)几何与本构算子性质

[Drucker公设](@entry_id:180546)的强大之处在于它们导出了一系列深刻的数学结论，这些结论极大地塑造了现代塑性力学理论的结构。

#### [屈服面](@entry_id:175331)的凸性与流动法则

在塑性理论中，一个最经典也最重要的结果是，对于采用**关联[流动法则](@entry_id:177163)**的材料，[Drucker公设](@entry_id:180546)等价于**[屈服面](@entry_id:175331)（或弹性域）的凸性** 。关联流动法则是指塑性应变率的方向总是沿着[屈服面](@entry_id:175331)在当前应力点的外法线方向。

这个等价关系包含两个方面：
1.  **（关联流动 + [凸屈服面](@entry_id:203690)） $\implies$ [Drucker公设](@entry_id:180546)成立**：
    如果[屈服面](@entry_id:175331)是凸的，那么根据凸集理论，对于屈服面上任意一点 $\boldsymbol{\sigma}$，其外[法线](@entry_id:167651) $\boldsymbol{n}$ 与从该点指向集合内任意一点 $\boldsymbol{\sigma}^*$ 的向量的[内积](@entry_id:158127)非正，即 $(\boldsymbol{\sigma}^* - \boldsymbol{\sigma}) : \boldsymbol{n} \le 0$。如果流动法则是关联的，那么塑性[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p$ 与外[法线](@entry_id:167651) $\boldsymbol{n}$ 同向。考虑屈服面上的两个不同应力点 $\boldsymbol{\sigma}_1$ 和 $\boldsymbol{\sigma}_2$，我们可以证明 $(\boldsymbol{\sigma}_2 - \boldsymbol{\sigma}_1) : (\dot{\boldsymbol{\varepsilon}}^p_2 - \dot{\boldsymbol{\varepsilon}}^p_1) \ge 0$ 成立，这正是[Drucker公设](@entry_id:180546)的一种广义形式。

2.  **（关联流动 + [Drucker公设](@entry_id:180546)） $\implies$ 屈服面是凸的**：
    反过来，如果[Drucker公设](@entry_id:180546)成立，并且流动法则是关联的，我们可以证明[屈服面](@entry_id:175331)必须是凸的。证明的思路是，假设[屈服面](@entry_id:175331)非凸，我们总可以找到两个点，其连线的一部分在屈服面之外，并利用关联流动法则构造出一个违反[Drucker公设](@entry_id:180546)的加载路径。

这个等价关系为塑性本构的建立提供了坚实的理论基础，解释了为何在大多数工程模型中，我们都采用J2、Tresca、Mohr-Coulomb等凸的[屈服函数](@entry_id:167970)。

#### 本构算子的单调性与对称性

[Drucker公设](@entry_id:180546)也可以被重新表述为对增量本构算子性质的约束。假设存在一个算子 $\mathcal{T}$，它将应变增量 $\delta\boldsymbol{\varepsilon}$ 映射到应力增量 $\delta\boldsymbol{\sigma}$，即 $\delta\boldsymbol{\sigma} = \mathcal{T}(\delta\boldsymbol{\varepsilon})$。

[Drucker公设](@entry_id:180546)可以被证明等价于算子 $\mathcal{T}$ 的**[单调性](@entry_id:143760)** 。对于从同一状态出发的任意两个不同的应变增量 $\delta\boldsymbol{\varepsilon}_1$ 和 $\delta\boldsymbol{\varepsilon}_2$，以及它们对应的应力增量 $\delta\boldsymbol{\sigma}_1 = \mathcal{T}(\delta\boldsymbol{\varepsilon}_1)$ 和 $\delta\boldsymbol{\sigma}_2 = \mathcal{T}(\delta\boldsymbol{\varepsilon}_2)$，以下不等式成立：

$$
(\delta\boldsymbol{\sigma}_2 - \delta\boldsymbol{\sigma}_1) : (\delta\boldsymbol{\varepsilon}_2 - \delta\boldsymbol{\varepsilon}_1) \ge 0
$$

这个单调性条件在现代塑性理论中具有核心地位，它是证明[弹塑性](@entry_id:193198)[边值问题](@entry_id:193901)解的存在性和唯一性的关键。

此外，对于采用关联流动法则的材料，增量本构关系具有**主对称性**。如果增量本构关系是线性的，例如，$\delta\boldsymbol{\varepsilon} = \mathbb{S} : \delta\boldsymbol{\sigma}$，其中 $\mathbb{S}$ 是[切线](@entry_id:268870)柔度张量，则其主对称性（$\mathbb{S}_{ijkl} = \mathbb{S}_{klij}$）意味着[交叉](@entry_id:147634)功相等 ：

$$
\delta\boldsymbol{\sigma}_1 : \delta\boldsymbol{\varepsilon}_2 = \delta\boldsymbol{\sigma}_2 : \delta\boldsymbol{\varepsilon}_1
$$

这一性质是经典的[Betti互易定理](@entry_id:184528)在增量问题中的体现。

### 在[边值问题](@entry_id:193901)[适定性](@entry_id:148590)中的应用

[Drucker公设](@entry_id:180546)最重要的应用之一是为准静态[弹塑性](@entry_id:193198)边值问题解的**唯一性**提供保证。考虑一个增量步的[弱形式](@entry_id:142897)问题，我们需求解位移增量场 $\Delta\boldsymbol{u}$，使得对于所有[虚位移](@entry_id:168781)场 $\boldsymbol{w}$，以下[虚功](@entry_id:176403)方程成立：

$$
a(\Delta\boldsymbol{u}, \boldsymbol{w}) = \int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{w}) : \mathbb{C}_{\mathrm{ep}} : \boldsymbol{\varepsilon}(\Delta\boldsymbol{u}) \, \mathrm{d}V = \ell(\boldsymbol{w})
$$

其中，$\mathbb{C}_{\mathrm{ep}}$ 是[弹塑性](@entry_id:193198)[切线刚度](@entry_id:166213)算子，$\ell(\boldsymbol{w})$ 是外力[虚功](@entry_id:176403)项。[解的唯一性](@entry_id:143619)取决于[双线性](@entry_id:146819)形 $a(\cdot, \cdot)$ 的性质 。

证明唯一性的标准方法是假设存在两个不同的解 $\Delta\boldsymbol{u}^{(1)}$ 和 $\Delta\boldsymbol{u}^{(2)}$。它们的差 $\Delta\boldsymbol{u}^d = \Delta\boldsymbol{u}^{(1)} - \Delta\boldsymbol{u}^{(2)}$ 满足 $a(\Delta\boldsymbol{u}^d, \boldsymbol{w}) = 0$。若令[虚位移](@entry_id:168781)场 $\boldsymbol{w}$ 等于差值本身 $\Delta\boldsymbol{u}^d$，我们得到：

$$
a(\Delta\boldsymbol{u}^d, \Delta\boldsymbol{u}^d) = \int_{\Omega} \boldsymbol{\varepsilon}(\Delta\boldsymbol{u}^d) : \mathbb{C}_{\mathrm{ep}} : \boldsymbol{\varepsilon}(\Delta\boldsymbol{u}^d) \, \mathrm{d}V = 0
$$

要从上式得出 $\Delta\boldsymbol{u}^d = \boldsymbol{0}$（即解是唯一的），积分项必须是正定的。这需要满足两个条件：
1.  **对称性**：[弹塑性](@entry_id:193198)[切线](@entry_id:268870)算子 $\mathbb{C}_{\mathrm{ep}}$ 必须具有主对称性，即 $\mathbb{C}_{\mathrm{ep}_{ijkl}} = \mathbb{C}_{\mathrm{ep}_{klij}}$。这确保了[双线性](@entry_id:146819)形 $a(\cdot, \cdot)$ 是对称的。对于采用关联[流动法则](@entry_id:177163)的塑性模型，这个对称性是自然满足的。这种对称性是[Betti互易定理](@entry_id:184528)在增量问题中的体现。

2.  **正定性（或强制性）**：[切线](@entry_id:268870)算子 $\mathbb{C}_{\mathrm{ep}}$ 必须是正定的。Drucker第二公设（$\delta\boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon}^p \ge 0$）确保了这一点。严格的硬化（$H > 0$）使得 $\mathbb{C}_{\mathrm{ep}}$ 是严格正定的，从而保证了在[位移控制](@entry_id:748569)下[解的唯一性](@entry_id:143619)。对于[理想塑性](@entry_id:753335)（$H=0$），算子只是半正定的，唯一性可能会丧失。

因此，[Drucker公设](@entry_id:180546)（特别是第二公设）与关联[流动法则](@entry_id:177163)相结合，通过保证[弹塑性](@entry_id:193198)[切线](@entry_id:268870)算子的对称性和正定性，为增量[边值问题](@entry_id:193901)的[适定性](@entry_id:148590)提供了坚实的力学基础 。

### 有效性范围与有限应变推广

经典[Drucker公设](@entry_id:180546)的应用并非无条件的，理解其适用范围至关重要。

首先，这些公设是为**准静态**、**速率无关**的过程制定的。在动态问题中，惯性效应可能导致失稳（如[剪切带](@entry_id:183352)），即使材料本身满足[Drucker公设](@entry_id:180546)，[解的唯一性](@entry_id:143619)也无法保证 。

其次，公设严格排除了**[应变软化](@entry_id:755491)**行为。任何导致[切线](@entry_id:268870)模量丧失正定性的软化模型（$H0$）都将违反Drucker第二公设，并可能导致材料失稳和数值计算上的困难。

当推广到**有限应变**领域时，情况变得更加复杂，核心挑战在于确保所有物理量和本构关系满足**物质[坐标无关性](@entry_id:159715)（客观性）**原理。
-   小应变理论中的[应力功率](@entry_id:182907) $\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}$ 不是客观的。在有限应变下，必须使用客观的、能量共轭的变量对来定义功率。例如，单位当前体积的功率应为柯西应力 $\boldsymbol{\sigma}$ 与变形率张量 $\boldsymbol{d}$ 的[点积](@entry_id:149019)，$\mathcal{P} = \boldsymbol{\sigma}:\boldsymbol{d}$。相应地，[塑性耗散](@entry_id:201273)率则为 $\mathcal{D} = \boldsymbol{\sigma}:\boldsymbol{d}^p$ 。
-   [Drucker公设](@entry_id:180546)的不等式必须用这些客观的量来表述，例如 $\boldsymbol{\sigma}:\boldsymbol{d}^p \ge 0$，以确保其物理意义不依赖于观察者。
-   在有限应变率形式本构中，必须使用**[客观应力率](@entry_id:199282)**（如Jaumann率或[Green-Naghdi率](@entry_id:190839)）。[客观率](@entry_id:198692)的选择会影响具体的应力[演化计算](@entry_id:634852)路径，但它并不改变[Drucker公设](@entry_id:180546)的基本形式 $\boldsymbol{\sigma}:\boldsymbol{d}^p \ge 0$。这是因为[耗散不等式](@entry_id:188634)本身是基于[能量共轭对](@entry_id:748968)定义的，其客观性已经得到保证，而[客观应力率](@entry_id:199282)的选择是内在于弹性本构关系中的一个技术环节 , 。

综上所述，[Drucker公设](@entry_id:180546)为被动、非软化、速率无关材料的力学行为提供了一套严格而自洽的稳定性准则。它不仅深刻地揭示了塑性变形的耗散本质，还与屈服面的几何形状、流动法则、本构算子的数学性质以及宏观边值问题的[适定性](@entry_id:148590)紧密相连，构成了现代塑性力学理论的基石之一。