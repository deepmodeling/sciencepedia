## 引言
在固体力学宏伟的理论殿堂中，[虚功原理](@entry_id:138749)（Principle of Virtual Work）占据着基石般的核心地位。它并非仅仅是一种求解静定或[超静定结构](@entry_id:185344)的巧妙技巧，而是一种更为深刻和普适的平衡思想，以其优雅的积分形式统一了从简单梁杆到复杂连续介质的力学分析。然而，许多学习者对其理解往往停留在初等的应用层面，未能充分领会其作为现代[计算力学](@entry_id:174464)（尤其是[有限元法](@entry_id:749389)）理论支柱的根本作用，也未能洞悉其在处理[几何非线性](@entry_id:169896)、[材料非线性](@entry_id:162855)及多物理场耦合等前沿问题时所展现的强大生命力。

本篇文章旨在弥合这一认知鸿沟，引领读者进行一次从基本原理到前沿应用的深度探索。我们将超越公式的表面，揭示虚功原理背后严谨的数学结构与深刻的物理内涵。通过本文的学习，读者将能够清晰地理解该原理如何从一个经典力学概念，演变为驱动现代工程仿真的核心引擎。

为实现这一目标，本文将分为三个紧密相连的章节。第一章，**“原理与机制”**，将深入剖析[虚功原理](@entry_id:138749)的理论基础，严格定义[虚位移](@entry_id:168781)、内外[虚功](@entry_id:176403)，并借助泛函分析工具阐明其作为[平衡方程](@entry_id:172166)“弱形式”的数学本质。第二章，**“应用与[交叉](@entry_id:147634)学科联系”**，将展示该原理的强大实践价值，探讨它如何奠定有限元方法的根基，并如何被扩展以解决结构稳定性、大变形、[接触力学](@entry_id:177379)及[多物理场耦合](@entry_id:171389)等复杂问题。最后，在第三章**“动手实践”**中，我们将通过一系列精心设计的练习，帮助读者将抽象的理论知识转化为具体的分析与计算能力，从而真正掌握[虚功原理](@entry_id:138749)的精髓。

## 原理与机制

本章旨在深入探讨[可变形体](@entry_id:201887)[虚功原理](@entry_id:138749)的理论基础与核心机制。作为[固体力学](@entry_id:164042)中一个极为强大和普适的工具，虚功原理不仅为复杂结构的静力学和动力学问题提供了一个统一的分析框架，而且是[有限元法](@entry_id:749389)等现代计算力学方法的理论基石。我们将从其基本陈述出发，逐步揭示其在数学上的严谨性，并最终将其拓展至有限变形和更抽象的[泛函分析](@entry_id:146220)框架中。

### 虚功原理的基本陈述

在平衡状态下，作用于一个[可变形体](@entry_id:201887)的所有外力所做的[虚功](@entry_id:176403)等于其内部应力所做的[虚功](@entry_id:176403)。这一陈述便是**[虚功原理](@entry_id:138749)（Principle of Virtual Work, PVW）** 的核心思想。这里的“虚”字，指的是一个假想的、满足[运动学](@entry_id:173318)约束的、无穷小的位移场，我们称之为**[虚位移](@entry_id:168781) (virtual displacement)**，记为 $\delta \boldsymbol{u}$。该原理为我们提供了一种绕开局部[微分](@entry_id:158718)平衡方程，而从一个积分（或全局）视角来描述平衡状态的方法。

#### 外部[虚功](@entry_id:176403)

**外部[虚功](@entry_id:176403)** ($\delta W_{\text{ext}}$) 是所有**主动施加的**外力在[虚位移](@entry_id:168781)场 $\delta \boldsymbol{u}$ 上所做的功。对于一个占据区域 $\Omega$ 的物体，其外部载荷通常包括[体力](@entry_id:174230)（如重力、电磁力）和面力（如接触压力、风载荷）。

假设物体受到一个单位体积的体力 $\boldsymbol{b}(\boldsymbol{x})$ 的作用，并在其部分边界 $\Gamma_t$ 上受到一个单位面积的预设面力 $\bar{\boldsymbol{t}}(\boldsymbol{x})$ 的作用。那么，外部[虚功](@entry_id:176403)可以表示为这两个部分贡献的总和：
$$
\delta W_{\text{ext}} = \int_{\Omega} \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \delta \boldsymbol{u} \, \mathrm{d}A
$$
第一个积分项代表了[体力](@entry_id:174230)在整个物体体积上所做的[虚功](@entry_id:176403)。第二个积分项则代表了在所谓的**诺伊曼边界（Neumann boundary）** 或**面力边界** $\Gamma_t$ 上，预设面力所做的[虚功](@entry_id:176403)。值得注意的是，在物体的另一部分边界 $\Gamma_u$ 上，位移是预先设定的。这部分边界上的力是未知的约束反力，它们不是主动施加的外力，因此不包含在外部[虚功](@entry_id:176403)的表达式中。我们将在后文中看到，[虚功原理](@entry_id:138749)的表述巧妙地回避了对这些未知反力的计算。[@problem_id:2676312]

#### 内部[虚功](@entry_id:176403)

**内部[虚功](@entry_id:176403)** ($\delta W_{\text{int}}$) 是物体内部的应[力场](@entry_id:147325)在虚变形上所做的功。一个更精确的出发点是[应力功率](@entry_id:182907)，即[应力张量](@entry_id:148973)与速度梯度的缩并。对于一个[虚位移](@entry_id:168781)场 $\delta \boldsymbol{u}$，其对应的虚[位移梯度](@entry_id:165352)为 $\nabla \delta \boldsymbol{u}$。因此，内部[虚功](@entry_id:176403)可以初步定义为：
$$
\delta W_{\text{int}} = \int_{\Omega} \boldsymbol{\sigma} : \nabla\delta\boldsymbol{u} \, \mathrm{d}V
$$
其中 $\boldsymbol{\sigma}$ 是柯西应力张量（Cauchy stress tensor），`:` 代表张量的[双点积](@entry_id:748648)。

任何[二阶张量](@entry_id:199780)（如 $\nabla \delta \boldsymbol{u}$）都可以分解为一个对称[部分和](@entry_id:162077)一个反对称部分。在小应变理论中，其对称部分被称为**虚应变张量 (virtual strain tensor)** $\delta \boldsymbol{\varepsilon}$，而反对称部分被称为**虚转动张量 (virtual rotation tensor)** 或虚[自旋张量](@entry_id:187346) $\delta \boldsymbol{\omega}$。
$$
\nabla\delta\boldsymbol{u} = \boldsymbol{\varepsilon}(\delta \boldsymbol{u}) + \boldsymbol{\omega}(\delta \boldsymbol{u})
$$
其中，
$$
\boldsymbol{\varepsilon}(\delta \boldsymbol{u}) = \frac{1}{2} \left( \nabla \delta \boldsymbol{u} + (\nabla \delta \boldsymbol{u})^{\mathsf{T}} \right), \quad \boldsymbol{\omega}(\delta \boldsymbol{u}) = \frac{1}{2} \left( \nabla \delta \boldsymbol{u} - (\nabla \delta \boldsymbol{u})^{\mathsf{T}} \right)
$$
将此分解代入内部[虚功](@entry_id:176403)的表达式，我们得到：
$$
\delta W_{\text{int}} = \int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta \boldsymbol{u}) \, \mathrm{d}V + \int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\omega}(\delta \boldsymbol{u}) \, \mathrm{d}V
$$
对于经典的柯西连续介质，在没有体力偶矩的情况下，[角动量守恒](@entry_id:156798)定律要求柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。[张量代数](@entry_id:161671)的一个基本结论是，一个[对称张量](@entry_id:148092)与一个[反对称张量](@entry_id:199349)的[双点积](@entry_id:748648)恒为零。因此，$\boldsymbol{\sigma} : \boldsymbol{\omega}(\delta \boldsymbol{u}) = 0$ 在物体内的每一点都成立。这意味着虚转动（即材料微元的刚性转动）部分对内部[虚功](@entry_id:176403)没有贡献。

于是，对于经典连续介质，内部[虚功](@entry_id:176403)的表达式简化为：
$$
\delta W_{\text{int}} = \int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta \boldsymbol{u}) \, \mathrm{d}V
$$
这个结果揭示了一个深刻的物理联系：内部功仅由应力与应变（变形的度量）的共轭[对产生](@entry_id:154125)。正是柯西应力[张量的对称性](@entry_id:202126)，使得应变成为了与应力[功共轭](@entry_id:194957)的运动学量。值得一提的是，在一些更广义的连续介质理论中，例如**偶应力理论（couple-stress theory）**，应力张量可能不是对称的，其反对称部分会与材料的微观转动梯度（与 $\boldsymbol{\omega}$ 相关）做功。但在经典理论的范畴内，我们可以忽略这种复杂性。[@problem_id:2676278]

综上所述，[虚功原理](@entry_id:138749)的完整表述为：对于任意运动学容许的[虚位移](@entry_id:168781) $\delta \boldsymbol{u}$，一个处于平衡状态的物体都满足
$$
\int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta \boldsymbol{u}) \, \mathrm{d}V = \int_{\Omega} \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \delta \boldsymbol{u} \, \mathrm{d}A
$$

### [运动学](@entry_id:173318)容许性与函数空间

[虚功原理](@entry_id:138749)的表述中有一个关键限定词：“[运动学](@entry_id:173318)容许的（kinematically admissible）”。一个[虚位移](@entry_id:168781)场 $\delta \boldsymbol{u}$ 并非任意选取的函数，它必须满足特定的数学和物理要求。这些要求定义了**容许[虚位移](@entry_id:168781)空间**，也称为**检验函数空间（test function space）**。

首先，[虚位移](@entry_id:168781)必须与问题中给定的**本质边界条件（essential boundary conditions）** 相容。本质边界条件是直接施加在位移场 $\boldsymbol{u}$ 上的约束。例如，在边界的某一部分 $\Gamma_u$ 上，位移被指定为 $\boldsymbol{u} = \bar{\boldsymbol{u}}$。我们考虑一个受到扰动后的位移场 $\boldsymbol{u} + \delta \boldsymbol{u}$。为了使这个扰动后的场仍然是“[运动学](@entry_id:173318)容许”的，它必须继续满足相同的本质边界条件。因此，在 $\Gamma_u$ 上，我们必须有 $\boldsymbol{u} + \delta \boldsymbol{u} = \bar{\boldsymbol{u}}$。由于真实的[位移场](@entry_id:141476) $\boldsymbol{u}$ 已经满足 $\boldsymbol{u} = \bar{\boldsymbol{u}}$，这直接导出[虚位移](@entry_id:168781)场必须在 $\Gamma_u$ 上为零：
$$
\delta \boldsymbol{u} = \boldsymbol{0} \quad \text{on } \Gamma_u
$$
这个条件至关重要。从[变分学](@entry_id:197464)的角度看，真实的解 $\boldsymbol{u}$ 位于一个由本质边界条件定义的约束[流形](@entry_id:153038)上。容许的变分（即[虚位移](@entry_id:168781)）必须是该[流形](@entry_id:153038)的切向矢量。要求 $\delta \boldsymbol{u}$ 在本质边界上为零，正是确保了这一点。[@problem_id:2676379]

其次，[虚位移](@entry_id:168781)场必须具有足够的**[光滑性](@entry_id:634843)（regularity）**，以确保内部虚[功积分](@entry_id:181218) $\int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta \boldsymbol{u}) \, \mathrm{d}V$ 是有意义的。这个积分中包含了 $\delta \boldsymbol{u}$ 的[一阶导数](@entry_id:749425)（通过虚应变 $\boldsymbol{\varepsilon}(\delta \boldsymbol{u})$ 体现）。在现代数学框架下，为了使积分有定义且能应用强大的数学工具，我们通常要求积分项是平方可积的。这意味着虚应变 $\boldsymbol{\varepsilon}(\delta \boldsymbol{u})$ 的分量应该是 $L^2(\Omega)$ 函数。这就要求[虚位移](@entry_id:168781)场 $\delta \boldsymbol{u}$ 本身及其（广义）一阶导数都是平方可积的。

满足这个条件的函数所构成的空间，正是**[索博列夫空间](@entry_id:141995)（Sobolev space）** $H^1(\Omega)$。相比于要求函数连续可导的经典空间（如 $C^1(\Omega)$），$H^1(\Omega)$ 是一个更“弱”也更广泛的空间，它包含了例如有限元法中常用的分片多项式函数。因此，要求[虚位移](@entry_id:168781)场属于 $H^1(\Omega)^d$ (对于 $d$ 维空间) 是保证虚功原理[适定性](@entry_id:148590)的最弱标准要求。

综合以上两点，我们可以精确地定义容许[虚位移](@entry_id:168781)的空间 $\mathcal{V}$ (也称为检验空间)：
$$
\mathcal{V} = \{ \boldsymbol{v} \in [H^1(\Omega)]^d \mid \boldsymbol{v} = \boldsymbol{0} \text{ on } \Gamma_u \}
$$
这个空间包含了所有满足齐次本质边界条件的 $H^1$ 向量函数。索博列夫空间的[迹定理](@entry_id:203967)保证了在 $\Gamma_u$ 上施加边界条件是数学上严格的。[@problem_id:2676267]

### 从[弱形式](@entry_id:142897)到强形式：恢复局部方程

[虚功原理](@entry_id:138749)通常被称为平衡方程的**[弱形式](@entry_id:142897)（weak form）**，因为它是在积分意义上表述的。而我们熟悉的偏[微分形式](@entry_id:146747)的[平衡方程](@entry_id:172166) $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0}$ 则被称为**强形式（strong form）**。弱形式的一个巨大威力在于，它反过来也蕴含了强形式。我们可以通过[分部积分](@entry_id:136350)和**[变分法](@entry_id:163656)基本引理（Fundamental Lemma of the Calculus of Variations）** 来揭示这一点。

让我们从[虚功原理](@entry_id:138749)的方程出发：
$$
\int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta \boldsymbol{u}) \, \mathrm{d}V = \int_{\Omega} \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \delta \boldsymbol{u} \, \mathrm{d}A
$$
利用 $\boldsymbol{\sigma}$ 的对称性，我们有 $\boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta \boldsymbol{u}) = \boldsymbol{\sigma} : \nabla(\delta \boldsymbol{u})$。现在，对内部[虚功](@entry_id:176403)项使用分部积分（即[高斯散度定理](@entry_id:188065)的推广）：
$$
\int_{\Omega} \boldsymbol{\sigma} : \nabla(\delta \boldsymbol{u}) \, \mathrm{d}V = \int_{\partial \Omega} (\boldsymbol{\sigma} \boldsymbol{n}) \cdot \delta \boldsymbol{u} \, \mathrm{d}A - \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \cdot \delta \boldsymbol{u} \, \mathrm{d}V
$$
其中 $\boldsymbol{n}$ 是边界 $\partial \Omega$ 上的单位外法向向量。将此式代回[虚功原理](@entry_id:138749)，并整理所有项到等式一侧：
$$
\int_{\Omega} (-\nabla \cdot \boldsymbol{\sigma} - \boldsymbol{b}) \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\partial \Omega} (\boldsymbol{\sigma} \boldsymbol{n}) \cdot \delta \boldsymbol{u} \, \mathrm{d}A - \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \delta \boldsymbol{u} \, \mathrm{d}A = 0
$$
我们将边界积分 $\int_{\partial \Omega}$ 分解为在 $\Gamma_u$ 和 $\Gamma_t$ 上的积分。由于容许的[虚位移](@entry_id:168781) $\delta \boldsymbol{u}$ 在 $\Gamma_u$ 上为零，因此在 $\Gamma_u$ 上的积分为零。方程简化为：
$$
\int_{\Omega} (-\nabla \cdot \boldsymbol{\sigma} - \boldsymbol{b}) \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} (\boldsymbol{\sigma} \boldsymbol{n} - \bar{\boldsymbol{t}}) \cdot \delta \boldsymbol{u} \, \mathrm{d}A = 0
$$
这个方程必须对**所有**容许的[虚位移](@entry_id:168781) $\delta \boldsymbol{u}$ 成立。这就是[变分法](@entry_id:163656)基本引理发挥作用的地方。该引理指出，如果一个积分 $\int f \phi = 0$ 对一个足够丰富的检验函数集 $\{\phi\}$ 中的所有函数都成立，那么被积函数 $f$ 本身必然（[几乎处处](@entry_id:146631)）为零。

首先，我们考虑一类特殊的[虚位移](@entry_id:168781)，它们在整个边界 $\partial \Omega$ 上都为零（即具有[紧支集](@entry_id:276214)）。对于这类 $\delta \boldsymbol{u}$，上式中的边界积分项自动消失，只剩下体积积分。根据[变分法](@entry_id:163656)基本引理，这要求体积积分的被积函数为零：
$$
-\nabla \cdot \boldsymbol{\sigma} - \boldsymbol{b} = \boldsymbol{0} \quad \implies \quad \nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0} \quad \text{in } \Omega
$$
这正是我们所熟知的**[局部平衡](@entry_id:156295)方程（强形式）**。[@problem_id:2676305]

既然[局部平衡](@entry_id:156295)方程在 $\Omega$ 内成立，那么对于任意 $\delta \boldsymbol{u}$，体积积分项恒为零。于是，我们的方程进一步简化为：
$$
\int_{\Gamma_t} (\boldsymbol{\sigma} \boldsymbol{n} - \bar{\boldsymbol{t}}) \cdot \delta \boldsymbol{u} \, \mathrm{d}A = 0
$$
现在，这个等式必须对所有在 $\Gamma_u$ 上为零但在 $\Gamma_t$ 上任意的容许[虚位移](@entry_id:168781) $\delta \boldsymbol{u}$ 成立。再次应用[变分法](@entry_id:163656)基本引理（这次是在[曲面](@entry_id:267450) $\Gamma_t$ 上），我们得出结论：
$$
\boldsymbol{\sigma} \boldsymbol{n} - \bar{\boldsymbol{t}} = \boldsymbol{0} \quad \implies \quad \boldsymbol{\sigma} \boldsymbol{n} = \bar{\boldsymbol{t}} \quad \text{on } \Gamma_t
$$
这正是**自然边界条件（natural boundary condition）**。它表明，由内部应[力场](@entry_id:147325)计算出的边界上的面力 $\boldsymbol{\sigma}\boldsymbol{n}$，必须等于外部施加的预设面力 $\bar{\boldsymbol{t}}$。[@problem_id:2676331]

这个推导过程完美地展示了[虚功原理](@entry_id:138749)的深刻内涵：一个单一的[积分方程](@entry_id:138643)等价于一个[偏微分方程](@entry_id:141332)和一组边界条件。同时，它也揭示了应力[张量的对称性](@entry_id:202126)是不可从虚功原理本身推导的，它是一个独立的物理定律（[角动量守恒](@entry_id:156798)）的结果。[@problem_id:2676305]

### [本质边界条件与自然边界条件](@entry_id:146051)

通过上述推导，我们可以清晰地区分两类边界条件。

**[本质边界条件](@entry_id:173524)**（或称运动学边界条件、[狄利克雷边界条件](@entry_id:173524)）是那些直接施加在求解的基本变量（在位移法中即位移 $\boldsymbol{u}$）上的约束。例如，$\boldsymbol{u} = \bar{\boldsymbol{u}}$。在[变分形式](@entry_id:166033)中，这些条件必须被**预先**满足。这意味着求[解空间](@entry_id:200470)（trial space）中的函数必须满足这些条件，而检验空间（test space）中的函数必须满足其齐次形式（例如 $\delta \boldsymbol{u} = \boldsymbol{0}$）。

**自然边界条件**（或称动力学边界条件、[诺伊曼边界条件](@entry_id:142124)）是那些涉及到基本变量的导数（在[固体力学](@entry_id:164042)中通常与力或应力相关）的约束。例如，$\boldsymbol{\sigma} \boldsymbol{n} = \bar{\boldsymbol{t}}$。这些条件并**不**需要被求解函数或检验函数预先满足。相反，它们是作为[变分方程](@entry_id:635018)的**推论**而“自然”地出现的。

一个有趣且重要的例子是自由表面。如果在一段边界 $\Gamma_f$ 上没有施加任何边界条件，这意味着位移 $\boldsymbol{u}$ 在该处不受任何运动学约束。因此，[虚位移](@entry_id:168781) $\delta \boldsymbol{u}$ 在 $\Gamma_f$ 上是任意的。在弱形式推导的边界项 $\int_{\Gamma_f} (\boldsymbol{\sigma}\boldsymbol{n}) \cdot \delta \boldsymbol{u} \, dA$ 中，由于 $\delta \boldsymbol{u}$ 的任意性，必须有 $\boldsymbol{\sigma}\boldsymbol{n} = \boldsymbol{0}$。因此，“无指定条件”等价于一个零面力的自然边界条件。

另一个富有启发性的例子是刚性光滑接触。假设物体在边界 $\Gamma_c$ 上与一个刚性、光滑、无摩擦的表面接触。
- “刚性”和“接触”意味着物体不能侵入该表面。这限制了法向位移，例如 $\boldsymbol{u} \cdot \boldsymbol{n} \le 0$。这是一个关于位移的运动学约束，因此是**本质**的。对应的[虚位移](@entry_id:168781)必须满足 $\delta \boldsymbol{u} \cdot \boldsymbol{n} = 0$（假设维持接触）。
- “光滑无摩擦”意味着表面不能提供切向的阻力。这限制了[面力矢量](@entry_id:189429)的切向分量为零，即 $\boldsymbol{t} \cdot \boldsymbol{\tau} = 0$，其中 $\boldsymbol{\tau}$ 是切向向量。这是一个关于力的约束，它将作为**自然**边界条件从[变分原理](@entry_id:198028)中导出，因为切向的[虚位移](@entry_id:168781) $\delta \boldsymbol{u} \cdot \boldsymbol{\tau}$ 是任意的。

这种区分在梁和板壳理论中也同样适用。例如，对于[欧拉-伯努利梁](@entry_id:749104)，挠度 $w$ 和转角 $\theta=w'$ 是基本[运动学](@entry_id:173318)变量。指定挠度或转角是本质条件，而指定剪力 $V$ 或[弯矩](@entry_id:202968) $M$ 则是自然条件。[@problem_id:2923147]

### 有限变形理论的拓展

以上讨论主要局限于小应变理论。当物体经历大位移、大转动和[大应变](@entry_id:751152)时，我们需要采用**有限变形（finite deformation）** 理论。其核心思想——[虚功](@entry_id:176403)（或更准确地说是[虚功](@entry_id:176403)率）原理——依然成立，但必须谨慎选择相互匹配的[应力张量](@entry_id:148973)和[应变率张量](@entry_id:266108)。这些匹配的张量对被称为**[功共轭](@entry_id:194957)（work-conjugate）** 对。

在有限变形中，我们需要区分**参考构型（reference configuration）** $\Omega_0$（通常是未变形状态）和**当前构型（current configuration）** $\Omega(t)$。这导致了多种应力和[应变度量](@entry_id:755495)的定义。

1.  **当前构型描述 ([欧拉描述](@entry_id:264722))**:
    最自然的出发点是当前构型中的[功率密度](@entry_id:194407)。内部虚[功率密度](@entry_id:194407)是柯西应力 $\boldsymbol{\sigma}$ 与虚变形率张量 $\hat{\boldsymbol{d}}$ 的缩并。$\boldsymbol{\sigma}$ 是对称的真实应力，$\boldsymbol{d}$ 是变形率张量（[速度梯度](@entry_id:261686) $\boldsymbol{L}=\nabla\boldsymbol{v}$ 的对称部分）。这是第一对[功共轭](@entry_id:194957)量：$(\boldsymbol{\sigma}, \boldsymbol{d})$。
    内部[虚功](@entry_id:176403)率为：$\delta \mathcal{P}_{\text{int}} = \int_{\Omega(t)} \boldsymbol{\sigma} : \hat{\boldsymbol{d}} \, dv$

2.  **参考构型描述 ([拉格朗日描述](@entry_id:264498))**:
    通过坐标变换，我们可以将积分[拉回](@entry_id:160816)到不变的参考构型上。这引出了另外两对重要的[功共轭](@entry_id:194957)量：
    - **第一类Piola-Kirchhoff（PK1）应力** $\boldsymbol{P}$ 与 **变形梯度率** $\dot{\boldsymbol{F}}$。$\boldsymbol{P}$ 是一个非对称张量，它将参考构型中的面元力与当前构型的力联系起来。内部[虚功](@entry_id:176403)率等效地表示为：
      $$
      \delta \mathcal{P}_{\text{int}} = \int_{\Omega_0} \boldsymbol{P} : \widehat{\dot{\boldsymbol{F}}} \, dV
      $$
    - **第二类Piola-Kirchhoff（PK2）应力** $\boldsymbol{S}$ 与 **格林-拉格朗日（Green-Lagrange）[应变率](@entry_id:154778)** $\dot{\boldsymbol{E}}$。$\boldsymbol{S}$ 是一个对称的、纯粹从材料角度定义的[应力张量](@entry_id:148973)。它与同样是材料度量的[Green-Lagrange应变](@entry_id:170427) $E = \frac{1}{2}(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} - \boldsymbol{I})$ 的率共轭。内部[虚功](@entry_id:176403)率又可以等效地表示为：
      $$
      \delta \mathcal{P}_{\text{int}} = \int_{\Omega_0} \boldsymbol{S} : \widehat{\dot{\boldsymbol{E}}} \, dV
      $$
这三个等价的[虚功](@entry_id:176403)率表达式是有限变形力学的基础。[@problem_id:2676350]

选择正确的[功共轭](@entry_id:194957)对应力-应变对至关重要，因为它确保了能量表达式的**客观性（objectivity）**，即物理定律不应依赖于观察者的[参考系](@entry_id:169232)。错误地搭配非共轭的量会导致依赖于观察者旋转状态的、物理上无意义的结果。

例如，如果我们错误地将当前构型中的柯西应力 $\boldsymbol{\sigma}$ 与参考构型中的[格林-拉格朗日应变](@entry_id:170427) $\delta\boldsymbol{E}$ 搭配，构造一个“功”密度 $w^* = \boldsymbol{\sigma} : \delta\boldsymbol{E}$，这个量将不是客观的。考虑一个[初始应力](@entry_id:750652)为 $\boldsymbol{\sigma} = \mathrm{diag}(s_1, s_2, 0)$，虚应变为 $\delta\boldsymbol{E} = \mathrm{diag}(e_1, e_2, 0)$ 的状态。初始的“功”密度为 $w^* = s_1 e_1 + s_2 e_2$。如果观察者绕第三轴旋转一个角度 $\theta$，根据[张量变换法则](@entry_id:185176)，他观察到的柯西应力为 $\boldsymbol{\sigma}' = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}$，而[格林-拉格朗日应变](@entry_id:170427)作为[材料张量](@entry_id:196294)保持不变 $\delta\boldsymbol{E}'=\delta\boldsymbol{E}$。新的“功”密度将变为 $w^{*'} = \boldsymbol{\sigma}' : \delta\boldsymbol{E}$。计算表明，两者之差为：
$$
\Delta w = w^{*'} - w^* = (s_1 - s_2)(e_2 - e_1)\sin^2\theta
$$
只要 $s_1 \neq s_2$ 且 $e_1 \neq e_2$，这个差值就非零。例如，取 $s_1=100\,\text{MPa}$, $s_2=50\,\text{MPa}$, $e_1=0.02$, $e_2=0.01$，并旋转 $\theta=30^\circ$，差值将为 $\Delta w = -1.25 \times 10^5 \, \text{Pa}$。这表明 $w^*$ 的值依赖于观察者的旋转角 $\theta$，因此它不是一个客观的物理标量，这种非共轭的搭配是错误的。[@problem_id:2676304]

### 抽象[变分形式](@entry_id:166033)

最后，我们可以将[线性弹性](@entry_id:166983)体的虚功原理提炼成一个高度抽象但极其有用的数学形式，即**[变分问题](@entry_id:756445)（variational problem）**。这种形式是现代[偏微分方程理论](@entry_id:189232)和有限元分析的出发点。

回到小应变线性弹性问题。我们已经定义了检验空间 $\mathcal{V} = H^1_{\Gamma_u}(\Omega)^n$。真实位移解 $\boldsymbol{u}$ 属于一个[仿射空间](@entry_id:152906) $\boldsymbol{u} \in \bar{\boldsymbol{u}} + \mathcal{V}$，即它等于某个满足[非齐次边界条件](@entry_id:750645)的函数 $\bar{\boldsymbol{u}}$ 加上一个属于 $\mathcal{V}$ 的函数。

虚功原理的方程可以被重写为：求 $\boldsymbol{u} \in \bar{\boldsymbol{u}} + \mathcal{V}$，使得对于所有 $\boldsymbol{v} \in \mathcal{V}$，都有
$$
a(\boldsymbol{u}, \boldsymbol{v}) = \ell(\boldsymbol{v})
$$
这里：
- $a(\cdot, \cdot)$ 是一个**双线性形式（bilinear form）**，它代表了内部[虚功](@entry_id:176403)。对于[线性弹性](@entry_id:166983)体，它由下式定义：
  $$
  a(\boldsymbol{u}, \boldsymbol{v}) := \int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{u}) : \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, \mathrm{d}x
  $$
  其中 $\mathbb{C}$ 是[四阶弹性张量](@entry_id:188318)。这个[双线性形式](@entry_id:746794)是对称、连续且（在 $\mathcal{V}$ 上）**强制的（coercive）**，这些性质对于解的存在性和唯一性至关重要。

- $\ell(\cdot)$ 是一个**[线性泛函](@entry_id:276136)（linear functional）**，它代表了外部[虚功](@entry_id:176403)：
  $$
  \ell(\boldsymbol{v}) := \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, \mathrm{d}x + \langle \bar{\boldsymbol{t}}, \mathrm{tr}(\boldsymbol{v}) \rangle_{H^{-1/2}(\Gamma_t), H^{1/2}(\Gamma_t)}
  $$
  这里，面力项被严格地写作 $H^{-1/2}(\Gamma_t)$ 和 $H^{1/2}(\Gamma_t)$ 之间的对偶积，以适应更一般的载荷情况（例如点载荷）。这个[线性泛函](@entry_id:276136)在空间 $\mathcal{V}$ 上是连续（有界）的。

$a(\boldsymbol{u}, \boldsymbol{v}) = \ell(\boldsymbol{v})$ 的表述是[虚功原理](@entry_id:138749)最纯粹的数学形式。它将一个复杂的物理问题转化为一个定义在无穷维函数空间上的[抽象代数](@entry_id:145216)方程。以**[Lax-Milgram定理](@entry_id:137966)**为代表的泛函分析工具，能够直接作用于这种形式，为在适当条件下证明解的存在性、唯一性和稳定性提供了坚实的理论基础。这不仅加深了我们对物理原理的理解，也为开发可靠的数值求解方法（如有限元法）铺平了道路，因为[有限元法](@entry_id:749389)的本质就是在这个无穷维空间中寻找一个有限维[子空间](@entry_id:150286)来近似求解这个[变分问题](@entry_id:756445)。[@problem_id:2676354]