## 引言
对[材料力学](@entry_id:201885)行为的精确描述，不仅需要考虑其弹性变形和塑性流动，还必须能够预测其性能如何因内部损伤的累积而逐渐退化，直至最终失效。传统的[弹塑性](@entry_id:193198)理论虽然能够描述材料的屈服和硬化，但无法解释刚度下降、[应力软化](@entry_id:176824)以及断裂萌生等现象，这构成了工程实践中的一个关键知识缺口。为了填补这一空白，必须建立一个能够统一描述材料从加载到失效全过程的本构框架，这便是损伤与[弹塑性](@entry_id:193198)耦合理论的核心使命。

本文旨在系统性地介绍这一高级理论。在接下来的章节中，我们将首先深入探讨其背后的[热力学](@entry_id:141121)**原理与机制**，建立严格的数学框架。随后，我们将考察该理论在[延性断裂](@entry_id:161045)、[疲劳分析](@entry_id:191624)和[计算力学](@entry_id:174464)等领域的广泛**应用与[交叉](@entry_id:147634)学科联系**。最后，通过一系列**动手实践**，您将有机会将理论知识转化为解决实际问题的计算技能，从而全面掌握这一强大的分析工具。

## 原理与机制

本章深入探讨了在[连续介质力学](@entry_id:155125)框架内，将材料损伤与弹性和塑性行为耦合的内在原理与核心机制。在前一章介绍性讨论的基础上，我们将构建一个基于不[可逆过程](@entry_id:276625)[热力学](@entry_id:141121)的严谨数学框架。这一框架不仅能够描述[材料刚度](@entry_id:158390)的退化，还能捕捉[损伤与塑性](@entry_id:203986)变形之间复杂的相互作用。我们将从基本的[热力学势](@entry_id:140516)函数出发，系统地推导出[本构关系](@entry_id:186508)、内变量的演化规律，并最终将理论延伸至有限应变领域。

### [热力学](@entry_id:141121)基础与内变量

建立一个自洽的[弹塑性](@entry_id:193198)损伤模型的基石是不可逆过程[热力学](@entry_id:141121)。其核心思想在于，材料的当前状态不仅由外部[可观测量](@entry_id:267133)（如应变）决定，还由一组描述其内部微观结构状态的**[内状态变量](@entry_id:750754)**（internal state variables）决定。对于耦合了损伤的[弹塑性](@entry_id:193198)材料，这些内变量通常包括塑性[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}^{p}$、描述[加工硬化](@entry_id:160669)的内变量（如累积塑性应变 $\kappa$），以及描述材料微观缺陷累积的[损伤变量](@entry_id:197066)（我们暂且用一个通用符号 $\boldsymbol{\xi}$ 代表）。

该理论框架的出发点是**亥姆霍兹自由能密度**（Helmholtz free energy density）$\psi$，它是一个[状态函数](@entry_id:137683)，其变量包括[可观测量](@entry_id:267133)（如总应变 $\boldsymbol{\varepsilon}$）和所有内变量。对于小应变问题，总应变通常可以加法分解为弹性部分 $\boldsymbol{\varepsilon}^{e}$ 和塑性部分 $\boldsymbol{\varepsilon}^{p}$，即 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{e} + \boldsymbol{\varepsilon}^{p}$。亥姆霍兹自由能 $\psi$ 则通常被假定为弹性应变和内变量的函数：$\psi = \psi(\boldsymbol{\varepsilon}^{e}, \boldsymbol{\xi})$。

根据热力学第二定律的局部形式，即 **Clausius-Duhem 不等式**，对于[等温过程](@entry_id:143096)，内能[耗散率](@entry_id:748577)必须非负。通过 **Coleman-Noll 程序**，我们可以从这一基本不等式中推导出材料的[本构关系](@entry_id:186508)。该程序指出，为了确保不等式对任意允许的[热力学过程](@entry_id:141636)均成立，那些可以被外部任意控制的变量（如总应变率 $\dot{\boldsymbol{\varepsilon}}$）的系数必须为零。这直接给出了[应力-应变关系](@entry_id:274093)。以 $\psi(\boldsymbol{\varepsilon}, \boldsymbol{\varepsilon}^{p}, D, \kappa)$ 为例，其中 $D$ 是[标量损伤变量](@entry_id:196275)，$\kappa$ 是[硬化](@entry_id:177483)变量，[耗散不等式](@entry_id:188634)写作 $\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0$。通过[链式法则](@entry_id:190743)展开 $\dot{\psi}$ 并重排，可得：
$$
\left(\boldsymbol{\sigma} - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}\right):\dot{\boldsymbol{\varepsilon}} - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^{p}}:\dot{\boldsymbol{\varepsilon}}^{p} - \frac{\partial \psi}{\partial D}\dot{D} - \frac{\partial \psi}{\partial \kappa}\dot{\kappa} \ge 0
$$
由于 $\dot{\boldsymbol{\varepsilon}}$ 是任意的，其系数必须为零，从而得到柯西应力 $\boldsymbol{\sigma}$ 的[状态方程](@entry_id:274378)：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$
余下的不等式，即**折减[耗散不等式](@entry_id:188634)**（reduced dissipation inequality），则约束了内变量的演化：
$$
\mathcal{D}_{int} = -\frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^{p}}:\dot{\boldsymbol{\varepsilon}}^{p} - \frac{\partial \psi}{\partial D}\dot{D} - \frac{\partial \psi}{\partial \kappa}\dot{\kappa} \ge 0
$$
这揭示了一个深刻的原理：每个内变量的演化（如 $\dot{\boldsymbol{\varepsilon}}^{p}$, $\dot{D}$, $\dot{\kappa}$）都由其共轭的**[热力学力](@entry_id:161907)**（thermodynamic force）驱动。这些力通过亥姆霍兹自由能对相应的内变量求[偏导数](@entry_id:146280)来定义。例如，与塑性应变 $\boldsymbol{\varepsilon}^{p}$、损伤 $D$ 和硬化 $\kappa$ 共轭的力（根据具体定义约定，可能包含负号）分别是 $\boldsymbol{X}$、$\boldsymbol{Y}$ 和 $\boldsymbol{R}$。

考虑一个具体的自由能形式 ：
$$
\psi(\boldsymbol{\varepsilon},\boldsymbol{\varepsilon}^{p},D,\kappa) = \frac{1}{2}(1-D)(\boldsymbol{\varepsilon}-\boldsymbol{\varepsilon}^{p}):\mathbb{C}:(\boldsymbol{\varepsilon}-\boldsymbol{\varepsilon}^{p}) + \phi(\kappa)
$$
其中 $\mathbb{C}$ 是初始[弹性刚度张量](@entry_id:170728)，$\phi(\kappa)$ 是[硬化](@entry_id:177483)势能。我们可以推导出与内变量 $\{D, \boldsymbol{\varepsilon}^{p}, \kappa\}$ 共轭的[热力学力](@entry_id:161907)。与[损伤演化](@entry_id:184965)共轭的力，即**[能量释放率](@entry_id:158357)**（energy release rate），通常定义为 $Y = -\partial \psi / \partial D$。与塑性应变和[硬化](@entry_id:177483)相关的力则为 $X = \partial \psi / \partial \boldsymbol{\varepsilon}^{p}$ 和 $R = \partial \psi / \partial \kappa$。计算这些[偏导数](@entry_id:146280)，我们得到：
$$
Y = \frac{1}{2}(\boldsymbol{\varepsilon}^{e}):\mathbb{C}:(\boldsymbol{\varepsilon}^{e})
$$
$$
X = -(1-D)\mathbb{C}:\boldsymbol{\varepsilon}^{e} = -\boldsymbol{\sigma}
$$
$$
R = \phi'(\kappa)
$$
这些[热力学力](@entry_id:161907)是构建[演化方程](@entry_id:268137)（即流动法则和损伤增长法则）的基础。重要的是，这些力的张量阶数与其共轭的内变量的阶数相匹配：标量内变量（$D, \kappa$）对应标量力（$Y, R$），而[二阶张量](@entry_id:199780)内变量（$\boldsymbol{\varepsilon}^{p}$）对应二阶张量力（$\boldsymbol{X}$）。

### 损伤的数学表述

[损伤变量](@entry_id:197066) $\boldsymbol{\xi}$ 的选择对模型的物理意义和[适用范围](@entry_id:636189)至关重要。不同的数学表示形式适用于描述不同类型的微观缺陷结构和由此产生的宏观各向异性行为 。

最简单的损伤表示是**[标量损伤变量](@entry_id:196275)**（scalar damage variable） $D$。它通常被定义在区间 $[0, 1)$ 内，其中 $D=0$ 代表无损的原始材料，而 $D \to 1$ 则表示材料完全丧失承载能力。标量损伤模型假设材料退化是**各向同性**的，即刚度在所有方向上均匀下降。这在物理上对应于材料内部微孔洞的均匀形核与等轴生长，常见于[延性](@entry_id:160108)金属在单调拉伸下的损伤模式。然而，由于其各向同性的本质，标量损伤无法描述由定向微裂纹引起的刚度各向异性损失，例如在[复合材料](@entry_id:139856)层合板或冷轧金属中观察到的现象。

为了描述具有一个优选方向的损伤，例如平行于某一特定平面的微裂纹族，我们可以引入**矢量[损伤变量](@entry_id:197066)**（vectorial damage variable）$\boldsymbol{a}$。这个矢量通常代表了损伤的主要方向（例如裂纹平面的法向）。这种表示能够描述**横观各向同性**（transverse isotropy）的[刚度退化](@entry_id:202277)，即材料在垂直于 $\boldsymbol{a}$ 的平面内表现为各向同性，但在平行于 $\boldsymbol{a}$ 的方向上具有不同的性质。然而，仅用一个矢量不足以完全表征具有多个独立损伤方向的材料，如具有两组正交裂纹的交叉层合板，这种材料表现出**[正交各向异性](@entry_id:196967)**（orthotropy）。

对于更普遍的[各向异性损伤](@entry_id:199086)，最常用的表示方法是**二阶对称[张量[损伤变](@entry_id:195924)量](@entry_id:197066)**（second-order symmetric tensor damage variable）$\boldsymbol{D}$。通过[谱分解](@entry_id:173707)，该张量可以写作 $\boldsymbol{D} = \sum_{i=1}^{3} d_{i} \boldsymbol{e}_{i} \otimes \boldsymbol{e}_{i}$，其中 $d_i$ 是沿三个相互正交的[主方向](@entry_id:276187) $\boldsymbol{e}_i$ 的主损伤值。这种表示方法能够自然地描述沿不同方向的不同程度的[刚度退化](@entry_id:202277)，使其成为模拟具有多个裂纹系统（如[交叉](@entry_id:147634)层合板）或由加工过程引起的织构（如冷轧金属）的材料的理想选择。

### 与弹性的耦合：[应变等效](@entry_id:186173)与能量等效

将[损伤变量](@entry_id:197066)引入[本构模型](@entry_id:174726)的核心问题是：它如何影响材料的弹性响应？[连续介质损伤力学](@entry_id:177438)为此提供了几个核心假设，其中最著名的是**[应变等效假设](@entry_id:199394)**（Hypothesis of Strain Equivalence）。

该假设由 Lemaitre 提出，其核心思想是：一个受损材料的[本构方程](@entry_id:138559)，在形式上与一个未受损材料的[本构方程](@entry_id:138559)相同，只要将名义柯西应力 $\boldsymbol{\sigma}$ 替换为一个**[有效应力](@entry_id:198048)**（effective stress）$\boldsymbol{\tilde{\sigma}}$。[有效应力](@entry_id:198048)被诠释为作用在材料“有效”或“未受损”承载[截面](@entry_id:154995)上的真实应力。对于各向同性标量损伤 $D$，有效应力张量与名义[应力张量](@entry_id:148973)之间的关系非常直观：
$$
\boldsymbol{\tilde{\sigma}} = \frac{\boldsymbol{\sigma}}{1-D}
$$
基于这个定义，我们可以从热力学势出发，严格推导出受损材料的[应力-应变关系](@entry_id:274093) 。未受损材料的[本构关系](@entry_id:186508)是 $\boldsymbol{\sigma}_{\text{virgin}} = \mathbb{C}_0 : \boldsymbol{\varepsilon}^e$，其中 $\mathbb{C}_0$ 是初始[刚度张量](@entry_id:176588)。根据[应变等效假设](@entry_id:199394)，[有效应力](@entry_id:198048) $\boldsymbol{\tilde{\sigma}}$ 应该遵循这个未受损的定律，即 $\boldsymbol{\tilde{\sigma}} = \mathbb{C}_0 : \boldsymbol{\varepsilon}^e$。将这个定义与有效应力和名义应力的关系式联立，我们立即得到受损材料的[本构关系](@entry_id:186508)：
$$
\boldsymbol{\sigma} = (1-D)\boldsymbol{\tilde{\sigma}} = (1-D) \mathbb{C}_0 : \boldsymbol{\varepsilon}^e
$$
这表明，受损材料的[切线刚度](@entry_id:166213)张量为 $\mathbb{C}(D) = (1-D)\mathbb{C}_0$。对于初始各向同性的材料，这意味着其杨氏模量 $E$ 和剪切模量 $G$ 都被均匀地折减为 $E(D)=(1-D)E_0$ 和 $G(D)=(1-D)G_0$。

另一个重要的概念是**能量等效假设**（Hypothesis of Energy Equivalence）。其一种常见的、基于[热力学](@entry_id:141121)的表述是，受损材料的亥姆霍兹自由能密度 $\psi$ 是未受损能量密度 $\psi_0$ 被损伤因子所折减的形式：
$$
\psi(\boldsymbol{\varepsilon}^{e}, D) = (1-D)\psi_0(\boldsymbol{\varepsilon}^{e}) = (1-D)\left(\frac{1}{2}\boldsymbol{\varepsilon}^{e} : \mathbb{C}_0 : \boldsymbol{\varepsilon}^{e}\right)
$$
通过对应力进行定义 $\boldsymbol{\sigma} = \partial \psi / \partial \boldsymbol{\varepsilon}^{e}$，我们得到 $\boldsymbol{\sigma} = (1-D)\mathbb{C}_0:\boldsymbol{\varepsilon}^e$。有趣的是，对于简单的各向同性标量损伤，[应变等效假设](@entry_id:199394)和能量等效假设得出了完全相同的宏观[本构关系](@entry_id:186508) 。

然而，这两种假设的等价性在更复杂的情况下会失效。例如，在处理诸如混凝土或岩石等材料中观察到的**单边效应**（unilateral effect）——即微裂纹在受压时闭合，刚度恢复——时，两种假设的推广方式有所不同。能量等效假设通常通过将[应变张量分解](@entry_id:184653)为拉伸部分 $\boldsymbol{\varepsilon}^+$ 和压缩部分 $\boldsymbol{\varepsilon}^-$，并只让损伤影响与拉伸相关的能量项来实现，例如 $\psi = (1-D)\psi_0(\boldsymbol{\varepsilon}^+) + \psi_0(\boldsymbol{\varepsilon}^-)$。这种方法可以自然地导出依赖于加载状态（拉伸或压缩）的[切线刚度](@entry_id:166213)，而无需引入更高阶的损伤张量。

### 与塑性的融合：屈服、[硬化](@entry_id:177483)与软化

将[损伤与塑性](@entry_id:203986)耦合是描述[材料失效](@entry_id:160997)前完整力学行为的关键。核心思想是将[塑性流动法则](@entry_id:189597)建立在[有效应力](@entry_id:198048)空间中。物理上，这是因为塑性滑移等微观机制发生在材料的未损伤部分。因此，[屈服函数](@entry_id:167970)通常被写成[有效应力](@entry_id:198048) $\boldsymbol{\tilde{\sigma}}$ 和硬化变量的函数，例如，对于 von Mises 屈服准则：
$$
f(\boldsymbol{\tilde{\sigma}}, \kappa) = \sqrt{\frac{3}{2}\text{dev}(\boldsymbol{\tilde{\sigma}}):\text{dev}(\boldsymbol{\tilde{\sigma}})} - \sigma_y(\kappa) \le 0
$$
其中 $\sigma_y(\kappa)$ 是当前[屈服应力](@entry_id:274513)。将 $\boldsymbol{\tilde{\sigma}} = \boldsymbol{\sigma} / (1-D)$ 代入，[屈服函数](@entry_id:167970)在名义[应力空间](@entry_id:199156)中变为：
$$
f(\boldsymbol{\sigma}, \kappa, D) = \frac{1}{1-D} \sqrt{\frac{3}{2}\text{dev}(\boldsymbol{\sigma}):\text{dev}(\boldsymbol{\sigma})} - \sigma_y(\kappa) \le 0
$$
这表明，随着损伤 $D$ 的累积，材料在名义应力空间中的弹性域会收缩，即材料会“软化”。

材料的宏观响应于是体现为**塑性[硬化](@entry_id:177483)**（由 $\kappa$ 增长引起）和**损伤软化**（由 $D$ 增长引起）之间的竞争。这种竞争决定了材料的整体应力-应变曲线是表现为净[硬化](@entry_id:177483)（斜率为正）还是净软化（斜率为负）。

我们可以通过一个一维[弹塑性](@entry_id:193198)损伤模型来精确地分析这种竞争 。考虑一个[屈服应力](@entry_id:274513)为 $\sigma_y(D,\kappa) = (1-D)\sigma_{y0} + H\kappa$ 的模型，其中 $\sigma_{y0}$ 是初始[屈服应力](@entry_id:274513)， $H$ 是线性[硬化](@entry_id:177483)模量。假设损伤随累积塑性应变 $\kappa$ 演化，即 $D=D(\kappa)$。通过推导一致性[切线](@entry_id:268870)模量 $E_t = d\sigma/d\varepsilon$，可以发现宏观软化（$E_t  0$）的条件为：
$$
H  \sigma_{y0} \frac{dD}{d\kappa}
$$
这个不等式清晰地量化了硬化与软化之间的竞争：左侧的 $H$ 代表材料因塑性变形而强化的能力，右侧的 $\sigma_{y0} D'(\kappa)$ 代表材料因损伤累积而弱化的速率。当损伤软化效应超过塑性硬化效应时，材料的宏观响应便进入软化阶段，最终导致失效。

此外，损伤和塑性之间的耦合还可以通过其他方式体现。例如，损伤的累积不仅会降低弹性刚度，还可能削弱材料的**硬化能力**。这可以通过让[硬化](@entry_id:177483)模量本身成为损伤的函数来建模 。例如，假设与[硬化](@entry_id:177483)变量 $\kappa$ 相关的储能部分为 $\psi_h(\kappa, D) = \frac{1}{2}H(D)\kappa^2$。如果采用最简单的线性退化形式 $H(D) = (1-D)H_0$，其中 $H_0$ 是初始硬化模量，那么共轭的硬化力为：
$$
R = \frac{\partial \psi_h}{\partial \kappa} = H(D)\kappa = (1-D)H_0\kappa
$$
在这种模型中，损伤的增长会同时降低材料的刚度和其抵抗进一步塑性变形的能力，从而加速软化过程。

### [损伤演化](@entry_id:184965)规律

一个完整的模型必须规定[损伤变量](@entry_id:197066)如何随加载历史演化。与塑性理论中的流动法则类似，[损伤演化](@entry_id:184965)也通常通过一个**损伤势函数**（damage potential）或加载函数 $\phi(Y, D)$ 来定义。该函数依赖于损伤的驱动力——能量释放率 $Y$——以及当前的损伤状态 $D$。

对于率无关的[损伤演化](@entry_id:184965)，其数学结构通常由一组 **[Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)**给出 。假设加载函数为 $\phi(Y,D) = Y - R(D) \le 0$，其中 $R(D)$ 是一个表征材料抵抗损伤能力的**损伤阻抗函数**（damage resistance function），它随 $D$ 单调递增。KKT 条件包括：
1.  **容许性条件**: $\phi(Y,D) \le 0$ (状态点必须在损伤弹性域内或其边界上)
2.  **不[可逆性](@entry_id:143146)条件**: $\dot{\lambda}_d \ge 0$ ([损伤演化](@entry_id:184965)是不可逆的，其中 $\dot{\lambda}_d$ 是损伤一致性乘子)
3.  **互补性条件**: $\phi(Y,D) \dot{\lambda}_d = 0$ (只有当状态点位于损伤[屈服面](@entry_id:175331)上时，损伤才能增长)

当损伤处于活动演化状态时（$\dot{D} > 0$），必然有 $\dot{\lambda}_d > 0$ 和 $\phi(Y,D)=0$。为了维持这种状态，加载函数的时间变化率也必须为零，这被称为**[一致性条件](@entry_id:637057)**（consistency condition）：
$$
\dot{\phi} = \frac{\partial \phi}{\partial Y}\dot{Y} + \frac{\partial \phi}{\partial D}\dot{D} = 0
$$
对于上述加载函数，我们有 $\partial \phi/\partial Y=1$ 和 $\partial \phi/\partial D = -R'(D)$。如果再引入一个关联损伤流动法则 $\dot{D} = \dot{\lambda}_d (\partial\phi/\partial Y) = \dot{\lambda}_d$，则[一致性条件](@entry_id:637057)变为 $\dot{Y} - R'(D)\dot{D} = 0$。将 $\dot{D}=\dot{\lambda}_d$ 代入，即可解出损伤乘子：
$$
\dot{\lambda}_d = \frac{\dot{Y}}{R'(D)}
$$
这个方程构成了[损伤演化](@entry_id:184965)的核心。它表明，损伤增长的速率（由 $\dot{\lambda}_d$ 代表）正比于其驱动力 $Y$ 的增长率，而反比于材料当前的损伤阻抗增长率 $R'(D)$。

### 有限应变框架下的表述

将[损伤与塑性](@entry_id:203986)理论推广到**有限应变**（finite strains）领域需要更严谨的[运动学](@entry_id:173318)和[热力学](@entry_id:141121)表述，以确保模型的**客观性**（objectivity）或称**物质[坐标无关性](@entry_id:159715)**（material frame-indifference）。

在[有限应变塑性](@entry_id:185352)中，变形梯度 $\boldsymbol{F}$ 通常被[乘法分解](@entry_id:199514)为弹性部分 $\boldsymbol{F}^e$ 和塑性部分 $\boldsymbol{F}^p$：
$$
\boldsymbol{F} = \boldsymbol{F}^e \boldsymbol{F}^p
$$
这种分解引入了一个虚拟的、无应力的**[中间构型](@entry_id:193000)**（intermediate configuration）。为了满足客观性，亥姆霍兹自由能 $\psi$ 必须是客观张量的函数。一个正确的选择是弹性[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}^e = (\boldsymbol{F}^e)^T \boldsymbol{F}^e$ 。因此，一个考虑了弹性、塑性硬化和损伤的、形式恰当的自由能可以写为：
$$
\psi(\boldsymbol{C}^e, \kappa, D) = (1-D)\hat{\psi}_e(\boldsymbol{C}^e) + \psi_p(\kappa)
$$
其中 $\hat{\psi}_e$ 是未受损的弹性[储能函数](@entry_id:197811)。

在此时，应力张量和共轭力的推导变得更为复杂，涉及到在不同构型（参考构型、[中间构型](@entry_id:193000)、当前构型）之间的张量映射（**push-forward** 和 **pull-back**）。例如，第二 Piola-Kirchhoff 应力张量 $\boldsymbol{S}$ (定义在参考构型) 与其在[中间构型](@entry_id:193000)中的对应物 $\boldsymbol{S}^e = 2 \partial\psi/\partial\boldsymbol{C}^e$ 通过 $\boldsymbol{F}^p$ 关联。

在此框架下推导出的折减[耗散不等式](@entry_id:188634)，其形式非常优雅 。[塑性耗散](@entry_id:201273)部分可以表示为[中间构型](@entry_id:193000)中的 **Mandel 应力** $\boldsymbol{M} = \boldsymbol{C}^e\boldsymbol{S}^e$ 与塑性速度梯度 $\boldsymbol{L}^p = \dot{\boldsymbol{F}}^p(\boldsymbol{F}^p)^{-1}$ 的[点积](@entry_id:149019)。最终，总耗散 $\mathcal{D}$ 可以分解为塑性、[硬化](@entry_id:177483)和损伤各自的贡献：
$$
\mathcal{D} = (\boldsymbol{M}:\boldsymbol{L}^p - R\dot{\alpha}) + Y\dot{D} \ge 0
$$
其中 $R=-\partial\psi/\partial\alpha$ 是硬化力。对于一个具体的 von Mises 型屈服准则和率无关的损伤准则，在同时发生[塑性流动](@entry_id:201346)和损伤增长的条件下，总耗散可以被精确地计算出来。例如，在一个特定的模型中，总耗散可以简化为：
$$
\mathcal{D} = (1-D)\sigma_{y0}\dot{\gamma} + Y_c\dot{D}
$$
其中 $\dot{\gamma}$ 是[塑性流动](@entry_id:201346)乘子，$\sigma_{y0}$ 是初始[屈服应力](@entry_id:274513)，$Y_c$ 是[损伤演化](@entry_id:184965)阈值。这个结果优美地展示了总[能量耗散](@entry_id:147406)是如何由两个独立的物理过程——塑性变形和[损伤演化](@entry_id:184965)——共同贡献的，即使在复杂的[有限应变运动学](@entry_id:168563)框架下，这种清晰的物理图像依然得以保持。