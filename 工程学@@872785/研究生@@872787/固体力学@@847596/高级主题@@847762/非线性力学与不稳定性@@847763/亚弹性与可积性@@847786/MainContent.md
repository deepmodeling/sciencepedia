## 引言
在[固体力学](@entry_id:164042)中，精确描述材料如何响应外力是连接变形与受力的核心，这便是[本构关系](@entry_id:186508)的任务。理想情况下，我们希望建立[应力与应变](@entry_id:137374)的直接函数关系，即超弹性理论。然而，在处理复杂的加载历史或在[数值模拟](@entry_id:137087)的增量框架中，我们常采用一种替代方法：建立应力变化率与变形率之间的关系。这种以率形式定义的[本构模型](@entry_id:174726)被称为**[亚弹性](@entry_id:204371) (hypoelasticity)**。它的直观性使其在计算中看似方便，但其背后隐藏着深刻的理论挑战，即“可积性”问题，这直接关系到模型是否能代表一个真正的、[能量守恒](@entry_id:140514)的弹性体。本文旨在系统性地剖析亚[弹性理论](@entry_id:184142)，揭示其内在的矛盾及其对现代力学建模的深远影响。

本文将引导读者分三步深入理解[亚弹性](@entry_id:204371)及其相关概念。在“**原理与机制**”一章中，我们将建立[亚弹性模型](@entry_id:184632)的基本框架，探讨为满足材料[坐标系](@entry_id:156346)无关性而引入的[客观应力率](@entry_id:199282)，并聚焦于核心的可积性问题，揭示大多数[亚弹性模型](@entry_id:184632)为何在理论上存在缺陷，甚至会导致非物理的预测。接下来，在“**应用与交叉学科联系**”一章中，我们将探讨这些理论在[计算力学](@entry_id:174464)、[有限应变塑性](@entry_id:185352)、地球物理学等领域的具体体现，分析[亚弹性模型](@entry_id:184632)的局限性如何推动了更先进的[超弹性](@entry_id:159356)-塑性理论的发展。最后，通过“**动手实践**”部分提供的具体计算问题，读者将能够亲手验证[亚弹性模型](@entry_id:184632)的[路径依赖性](@entry_id:186326)和非物理行为，从而将抽象的理论概念转化为具体的力学直觉。

## 原理与机制

在连续介质力学中，本构关系描述了材料如何响应外部载荷，是连接[运动学](@entry_id:173318)与动力学的桥梁。对于弹性材料，最理想的描述是建立一个应力与应变的直接函数关系。然而，在处理复杂变形历史或在增量计算框架中，我们常常采用一种替代方法，即建立应力变化率与变形率之间的关系。这种以率形式定义的本构模型被称为**[亚弹性](@entry_id:204371) (hypoelasticity)**。本章将深入探讨[亚弹性模型](@entry_id:184632)的构建原理、其内在的理论挑战，以及这些挑战对材料行为预测的深刻影响。

### [亚弹性](@entry_id:204371)：[本构关系](@entry_id:186508)的率形式

与通过一个[势函数](@entry_id:176105)（如[应变能密度函数](@entry_id:755490) $\psi$）直接定义[应力-应变关系](@entry_id:274093)的**[超弹性](@entry_id:159356) (hyperelasticity)** 不同，[亚弹性模型](@entry_id:184632)假设应力的一个[客观率](@entry_id:198692)（用 $\stackrel{\diamond}{\boldsymbol{\sigma}}$ 表示）是当前应力状态 $\boldsymbol{\sigma}$ 和变形率张量 $\boldsymbol{d}$ 的函数。最简单的线性[亚弹性模型](@entry_id:184632)可以表示为：

$$
\stackrel{\diamond}{\boldsymbol{\sigma}} = \mathbb{C}(\boldsymbol{\sigma}):\boldsymbol{d}
$$

其中 $\boldsymbol{\sigma}$ 是柯西（Cauchy）应力张量，$\boldsymbol{d}$ 是变形率张量，定义为[速度梯度](@entry_id:261686) $\boldsymbol{l}$ 的对称部分，即 $\boldsymbol{d} = \frac{1}{2}(\boldsymbol{l} + \boldsymbol{l}^{\mathsf{T}})$。$\mathbb{C}$ 是一个[四阶张量](@entry_id:181350)，称为[切线](@entry_id:268870)模量张量。在最简单的情况下，$\mathbb{C}$ 是一个常数张量，例如对于[各向同性材料](@entry_id:170678)，其形式为 $\mathbb{C}:\boldsymbol{d} = \lambda \mathrm{tr}(\boldsymbol{d})\boldsymbol{I} + 2\mu\boldsymbol{d}$，其中 $\lambda$ 和 $\mu$ 是拉梅（Lamé）常数。[@problem_id:2647787] 这种率形式的定义在概念上很直观，因为它将应力的瞬时“响应”与变形的瞬时“速率”联系起来，这在数值模拟的增量步中尤其方便。

然而，这个定义的简洁性背后隐藏着深刻的复杂性，其核心在于符号 $\stackrel{\diamond}{(\cdot)}$，即“[客观应力率](@entry_id:199282)”。

### 材料[坐标系](@entry_id:156346)无关性原理与[客观应力率](@entry_id:199282)

[本构定律](@entry_id:178936)的一个基本要求是**材料[坐标系](@entry_id:156346)无关性原理 (principle of material frame indifference)**，也称为[客观性原理](@entry_id:185412)。该原理指出，本构关系在叠加一个任意的刚体运动（即不产生应变的平移和旋转）后必须保持形式不变。换言之，一个旋转的观察者和一个静止的观察者必须测量到相同的材料响应。

一个直接的推论是，[本构方程](@entry_id:138559)两边的张量必须以相同的方式对刚体旋转做出响应，即它们必须是**客观的 (objective)**。变形率张量 $\boldsymbol{d}$ 是一个客观张量。然而，柯西应力张量的标准[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ 却不是客观的。在叠加一个角速度为 $\boldsymbol{\Omega}$ 的刚体旋转后，$\dot{\boldsymbol{\sigma}}$ 的变换关系为：
$$
\dot{\boldsymbol{\sigma}}^{\ast} = \boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega} + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}}
$$
其中 $\boldsymbol{Q}$ 是[旋转张量](@entry_id:191990)，$\boldsymbol{\sigma}^*$ 是旋转后的应力。附加项的存在表明 $\dot{\boldsymbol{\sigma}}$ 的值取决于观察者的旋转状态，因此它不能直接用于本构关系中。[@problem_id:2647775]

为了满足客观性要求，我们必须使用一个**[客观应力率](@entry_id:199282)**。大多数[客观应力率](@entry_id:199282)都具有协运形式，它通过减去[应力张量](@entry_id:148973)随材料局部旋转而产生的变化部分来修正物质导数：
$$
\stackrel{\diamond}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}_{\sigma}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}_{\sigma}
$$
其中 $\boldsymbol{W}_{\sigma}$ 是一个与材料旋转相关的[自旋张量](@entry_id:187346)。不同的 $\boldsymbol{W}_{\sigma}$ 定义了不同的[客观率](@entry_id:198692)，常见的例子包括：

*   **Zaremba–[Jaumann 率](@entry_id:185572)** (或简称为 [Jaumann 率](@entry_id:185572)): 这种应力率使用速度梯度 $\boldsymbol{l}$ 的反对称部分，即[自旋张量](@entry_id:187346) $\boldsymbol{w} = \frac{1}{2}(\boldsymbol{l} - \boldsymbol{l}^{\mathsf{T}})$。即 $\boldsymbol{W}_{\sigma} = \boldsymbol{w}$。它代表了与材料当前变形速率相关的平均物质旋转。[@problem_id:2647772]

*   **Truesdell 率**: 此率与物质[坐标系](@entry_id:156346)下的应力度量（第二 Piola-Kirchhoff 应力）的[物质导数](@entry_id:172646)相关，其在空间[坐标系](@entry_id:156346)下的表达形式较为复杂，但也是一个有效的[客观率](@entry_id:198692)。[@problem_id:2647763]

*   **Green–Naghdi 率**: 此率使用极分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$ 中[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 的自旋，即 $\boldsymbol{W}_{\sigma} = \dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}}$。它度量了物质方向的真实旋转率。[@problem_id:2647773]

[客观性原理](@entry_id:185412)是如此根本，以至于任何有效的本构模型，无论是各向同性还是各向异性，都必须遵守。例如，如果试图构建一个应力依赖的各向异性模型，必须确保其各向异性方向由材料本身决定（例如，由一个嵌入材料的矢量 $\boldsymbol{a}$ 定义），而不是依赖于固定的空间[坐标系](@entry_id:156346)。一个依赖于固定空间方向（如 $\boldsymbol{e}_1$）的“朴素”模型会违反客观性，因为旋转后，材料的优先方向会改变，而模型的数学形式却不会相应地改变。正确的做法是使用材料结构张量（如 $\boldsymbol{A} = \boldsymbol{a} \otimes \boldsymbol{a}$）和[不变量](@entry_id:148850)（如 $\boldsymbol{\sigma}:\boldsymbol{A}$）来构建本构函数，从而确保其在任何旋转下都保持形式不变。[@problem_id:2647752]

### 可积性问题：[亚弹性](@entry_id:204371)等同于弹性吗？

既然我们已经建立了客观的[亚弹性模型](@entry_id:184632)，一个核心问题随之而来：如果我们将[亚弹性](@entry_id:204371)定律沿着一个变形路径进行积分，得到的[应力-应变关系](@entry_id:274093)是否与从一个[应变能势](@entry_id:755493)函数导出的[超弹性](@entry_id:159356)关系等价？这个问题被称为**可积性 (integrability)** 问题。

如果一个[亚弹性模型](@entry_id:184632)是可积的，那么它就描述了一个真正的弹性材料，其响应是路径无关的。这意味着，对于任何一个闭合的变形循环（即材料从一个状态出发，经过一系列变形后又回到初始状态），所做的净功必须为零：
$$
W_{cyc} = \oint \boldsymbol{\sigma}:\boldsymbol{d} \, dt = 0
$$
这个条件至关重要。如果在一个闭合循环中 $W_{cyc} \neq 0$，则意味着材料要么凭空产生了能量（$W_{cyc}  0$），要么耗散了能量（$W_{cyc} > 0$）。对于一个纯弹性、[等温过程](@entry_id:143096)，前者违反了[热力学第二定律](@entry_id:142732)（构成[第二类永动机](@entry_id:139670)），后者则意味着存在耗散，材料并非纯弹性。因此，不可积的[亚弹性模型](@entry_id:184632)无法严格地代表一个纯弹性体。[@problem_id:2647774]

我们可以通过两种方式来检验一个[亚弹性模型](@entry_id:184632)的[可积性](@entry_id:142415)：

1.  **直接循环积分**: 我们可以选择一个在应变空间中的闭合路径，然后沿此路径积分[本构方程](@entry_id:138559)，计算总功 $\oint \boldsymbol{\sigma}:\boldsymbol{d} \, dt$。例如，在一个由两个独立应变分量 $\varepsilon_{11}$ 和 $\varepsilon_{22}$ 构成的平面中，我们可以沿着一个矩形路径 $A \rightarrow B \rightarrow C \rightarrow D$ 进行积分。如果最终计算出的总功不为零，则证明该模型是不可积的，其响应是[路径依赖](@entry_id:138606)的。[@problem_id:2647757]

2.  **[路径依赖性](@entry_id:186326)检验**: 可积性的一个等价条件是，在任意两点之间的做功只取决于起点和终点，而与路径无关。在数学上，这与一个微分形式是否为[全微分](@entry_id:171747)（或称“[恰当微分](@entry_id:147306)”）的问题等价。一个检验方法是检查[混合偏导数的对称性](@entry_id:146941)。如果我们可以用两个参数 $s$ 和 $t$ 来[参数化](@entry_id:272587)变形历史，那么总功 $W(s,t)$ 是否路径无关，可以通过比较 $\frac{\partial^2 W}{\partial s \partial t}$ 和 $\frac{\partial^2 W}{\partial t \partial s}$ 来判断。如果它们不相等，则说明变形顺序会影响最终结果，即存在[路径依赖](@entry_id:138606)。[@problem_id:2647769]

令人惊讶的是，对于大多数常见的[客观率](@entry_id:198692)（如 [Jaumann 率](@entry_id:185572)和 Truesdell 率），即使采用最简单的常数模量 $\mathbb{C}$，得到的[亚弹性模型](@entry_id:184632)也是**不可积的**。

### 不可积性的后果：非物理的病态行为

[亚弹性模型](@entry_id:184632)的不[可积性](@entry_id:142415)并非一个纯粹的数学瑕疵，它会导致模型预测出与物理现实严重不符的“病态”行为。最经典的例子是**简单剪切 (simple shear)** 问题。

考虑一个材料块，其[速度场](@entry_id:271461)为 $v_1 = \dot{\gamma} y, v_2=v_3=0$，其中 $\dot{\gamma}$ 是恒定的剪切率。这是一个[等容变形](@entry_id:196451)，变形率 $\boldsymbol{d}$ 和[自旋张量](@entry_id:187346) $\boldsymbol{w}$ 都是常数。我们来考察使用 [Jaumann 率](@entry_id:185572)的线性[亚弹性模型](@entry_id:184632) $\stackrel{\diamond}{\boldsymbol{\sigma}} = 2G\boldsymbol{d}$ 的预测结果。

通[过积分](@entry_id:753033)这个[常微分方程组](@entry_id:266774)，可以得到应力随时间的演化。对于[剪切应力](@entry_id:137139) $\sigma_{12}$，模型预测其会随应变 $\gamma = \dot{\gamma}t$ 正弦[振荡](@entry_id:267781)：$\sigma_{12}(t) = G\sin(\dot{\gamma}t)$。更引人注目的是法向应力的行为。模型预测，在剪切方向上的[法向应力](@entry_id:260622) $\sigma_{11}$ 会出现一个非零的、并且随剪切应变持续[振荡](@entry_id:267781)的分量：[@problem_id:2647772]
$$
\sigma_{11}(t) = G(1 - \cos(\dot{\gamma}t))
$$
这个预测是完全非物理的。真实材料在简单剪切下，[法向应力](@entry_id:260622)（Poynting 效应）会发展并趋于一个稳定值，而绝不会无限[振荡](@entry_id:267781)。这种[振荡](@entry_id:267781)行为是 [Jaumann 率](@entry_id:185572)模型的一个著名缺陷，直接源于其不可积性。

更有甚者，如果我们换用另一个[客观率](@entry_id:198692)，例如 Truesdell 率，对同样的问题进行分析，会得到完全不同的预测。使用 Truesdell 率的模型预测，第一[法向应力差](@entry_id:191914) $N_1 = \sigma_{11} - \sigma_{22}$ 会随剪切应变 $\gamma$ 的平方单调增长，即 $N_1^{\mathrm{(Truesdell)}}(\gamma) = G\gamma^2$，而 [Jaumann 率](@entry_id:185572)的预测则是 $N_1^{\mathrm{(Jaumann)}}(\gamma) = 2G(1 - \cos(\gamma))$。[@problem_id:2647763]

这揭示了[亚弹性](@entry_id:204371)框架的根本困境：不仅大多数模型是不可积和非物理的，而且模型的预测结果严重依赖于所选择的[客观率](@entry_id:198692)，没有一个明确的先验准则来指导我们选择哪一个才是“正确”的。

### 一个特例：可积的对数率模型

在众多不可积的模型中，存在一个重要的特例。根据 Bernstein 的[可积性](@entry_id:142415)条件，如果一个[亚弹性模型](@entry_id:184632) $\stackrel{\diamond}{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{d}$ 要想是可积的，必须满足一个关键的[运动学](@entry_id:173318)和本构学的对应关系：所选用的[客观率](@entry_id:198692) $\stackrel{\diamond}{(\cdot)}$ 必须恰好是某个[应变张量](@entry_id:193332) $\boldsymbol{E}$ 的协运率（即满足 $\stackrel{\diamond}{\boldsymbol{E}} = \boldsymbol{d}$），并且模量张量 $\mathbb{C}$ 是某个[势函数](@entry_id:176105) $\psi(\boldsymbol{E})$ 的[二阶导数](@entry_id:144508)（Hessian 矩阵）。[@problem_id:2647787]

事实证明，存在这样一对“完美搭档”：**亨基（Hencky）应变**和**对数率 (logarithmic rate)**。

[亨基应变](@entry_id:191329)，又称[对数应变](@entry_id:751438)，定义为左柯西-格林伸长张量 $\boldsymbol{V}$ 的自然对数，即 $\boldsymbol{h} = \ln \boldsymbol{V}$。而对数率 $\stackrel{\ln}{\nabla}(\cdot)$ 则被唯一地定义为这样一个协运率，它使得[亨基应变](@entry_id:191329)的协运率恰好等于变形率张量 $\boldsymbol{d}$，即：
$$
\stackrel{\ln}{\nabla}\boldsymbol{h} = \boldsymbol{d}
$$
现在，如果我们采用对数率来构建[亚弹性](@entry_id:204371)定律：
$$
\stackrel{\ln}{\nabla}\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{d}
$$
利用对数率的定义，上式可以改写为：
$$
\stackrel{\ln}{\nabla}\boldsymbol{\sigma} = \mathbb{C}:(\stackrel{\ln}{\nabla}\boldsymbol{h})
$$
如果 $\mathbb{C}$ 是一个常数张量，这个方程可以在协运[坐标系](@entry_id:156346)下直接积分，得到一个线性的[应力-应变关系](@entry_id:274093)：
$$
\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{h}
$$
这个关系可以从一个二次形式的[应变能密度函数](@entry_id:755490) $\psi(\boldsymbol{h}) = \frac{1}{2}\boldsymbol{h}:(\mathbb{C}:\boldsymbol{h})$ 导出，因此，该模型是[超弹性](@entry_id:159356)的，并且是完全可积的。[@problem_id:2647775] 这种基于对数率和[亨基应变](@entry_id:191329)的模型，也被称为对数[弹塑性](@entry_id:193198)模型，它确保了在纯弹性变形下[能量守恒](@entry_id:140514)和[路径无关性](@entry_id:163750)。

在纯拉伸（即无刚体旋转）这种特殊运动下，我们可以更清晰地看到这一点。在这种情况下，可以证明对数率的自旋项为零，因此对数率退化为简单的[物质时间导数](@entry_id:190892) $\dot{(\cdot)}$。同时，运动学关系也简化为 $\boldsymbol{d} = \dot{\boldsymbol{h}}$。于是[本构方程](@entry_id:138559)变为 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\dot{\boldsymbol{h}}$，直接积分即可得到 $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{h}$，从而证明了其可积性并导出了应力与[亨基应变](@entry_id:191329)的[线性关系](@entry_id:267880)。[@problem_id:2647767]

### 总结与展望：[亚弹性](@entry_id:204371)在现代力学中的位置

通过本章的讨论，我们可以对[亚弹性](@entry_id:204371)形成一个清晰而审慎的认识。

*   [亚弹性](@entry_id:204371)是一种以率形式定义的[本构模型](@entry_id:174726)，其核心要求是使用[客观应力率](@entry_id:199282)以满足材料[坐标系](@entry_id:156346)无关性原理。
*   然而，大多数看似合理的[亚弹性模型](@entry_id:184632)（如使用 [Jaumann 率](@entry_id:185572)的模型）都是不可积的。这意味着它们不对应于一个储能[势函数](@entry_id:176105)，会导致在闭合变形循环中产生或耗散能量，这与纯弹性材料的物理行为相悖，并违反[热力学](@entry_id:141121)基本定律。
*   这种不可积性在具体问题中表现为非物理的病态预测，例如在简单剪切中出现无限[振荡](@entry_id:267781)的法向应力。
*   对数率与[亨基应变](@entry_id:191329)的组合是一个重要的例外，它构建了一个可积的[亚弹性模型](@entry_id:184632)，该模型等价于一个基于[亨基应变](@entry_id:191329)的超弹性模型。
*   值得注意的是，当应变非常小时，所有不同的[客观率](@entry_id:198692)都近似等于[物质时间导数](@entry_id:190892)，[亚弹性模型](@entry_id:184632)退化为经典的线性弹性理论，此时[可积性](@entry_id:142415)问题自然消失。因此，这些复杂性是[有限应变理论](@entry_id:176941)所特有的。[@problem_id:2647787]

尽管存在这些理论上的严重缺陷，[亚弹性](@entry_id:204371)框架在现代[计算力学](@entry_id:174464)中，特别是在**[弹塑性力学](@entry_id:193198)**中，仍然占有一席之地。在[弹塑性](@entry_id:193198)理论中，总变形被分解为弹性和塑性部分。在每一个小的增量步中，材料的弹性响应通常就是用[亚弹性模型](@entry_id:184632)来描述的。因为每个增量步的变形很小，由不可积性带来的[路径依赖](@entry_id:138606)误差通常也被控制在可接受的范围内。因此，理解[亚弹性](@entry_id:204371)的原理、局限性和病态行为，对于正确应用和解读这些高级[计算模型](@entry_id:152639)至关重要。