## 引言
材料在使用过程中，由于微裂纹、微孔洞的萌生与扩展，其力学性能会逐渐退化，这一过程被称为“损伤”。准确预测损伤的演化对于确保工程结构（从桥梁、飞机到电子元件）的安全性和可靠性至关重要。然而，传统的经验性方法往往缺乏严格的物理基础，难以推广到复杂的加载条件和新材料中。本文旨在介绍一个基于[连续介质力学](@entry_id:155125)和不[可逆过程](@entry_id:276625)[热力学](@entry_id:141121)的严谨框架，它将损伤视为一个内部[状态变量](@entry_id:138790)，从而为描述和预测材料退化行为提供了坚实的理论根基。

通过本文的学习，读者将深入理解[损伤力学](@entry_id:178377)的基本原理，并掌握如何构建与[热力学定律](@entry_id:202285)相容的本构模型。
- 在**“原理与机制”**一章中，我们将从损伤的物理定义出发，建立亥姆霍兹自由能与应力、损伤之间的关系，推导驱动[损伤演化](@entry_id:184965)的[热力学力](@entry_id:161907)，并构建控制损伤增长的演化法则。
- 随后的**“应用与跨学科联系”**一章将展示该框架的强大应用价值，探讨如何将其用于模拟[延性](@entry_id:160108)金属、准[脆性](@entry_id:198160)混凝土以及各向异性[复合材料](@entry_id:139856)的复杂行为，并讨论其在有限元分析和[断裂力学](@entry_id:141480)中的实现。
- 最后，**“动手实践”**部分将通过具体的计算练习，帮助读者将理论知识转化为解决实际问题的能力，例如推导损伤驱动力以及实现一个简单的[损伤-塑性耦合](@entry_id:193357)算法。

让我们首先进入第一章，系统地构建[损伤演化](@entry_id:184965)的热力学原理与机制。

## 原理与机制

本章旨在系统阐述[损伤演化](@entry_id:184965)的[热力学](@entry_id:141121)框架。我们将从[连续介质损伤力学](@entry_id:177438)的基本概念出发，建立一个与热力学定律相容的本构理论。我们将把损伤视为一个内部状态变量，并从[亥姆霍兹自由能](@entry_id:136442)势中导出其共轭的[热力学](@entry_id:141121)驱动力。随后，我们将构建损伤的演化法则，并探讨一些用于模拟材料复杂行为（如[拉压不对称性](@entry_id:201728)）的高级模型。本章的目标是为材料退化、塑性耦合及局部化等现象的建模提供坚实的理论基础。

### 损伤的物理概念与现象学描述

在宏观尺度上，材料的力学响应因微观缺陷（如微裂纹、微孔洞）的萌生与扩展而逐渐退化，这一过程被称为**损伤**。为了在连续介质力学的框架内描述这一现象，我们需要引入一个能够量化材料内部状态退化的场变量。

最直观的损伤定义源于 L.M. Kachanov 的思想，即损伤导致了材料有效承载面积的减少。考虑一个初始[横截面](@entry_id:154995)积为 $A_0$ 的杆件，在[单轴拉伸](@entry_id:188287)力 $F$ 的作用下，其内部产生了微观缺陷。我们可以将[横截面](@entry_id:154995)想象成由两部分组成：一部分是仍然能够传递应力的“完好”有效区域 $A_{\mathrm{eff}}$，另一部分是已失效的损伤区域 $A_d$，其中 $A_{\mathrm{eff}} + A_d = A_0$。

据此，我们可以定义一个无量纲的**[标量损伤变量](@entry_id:196275)** $d$，它表示已损伤面积占初始面积的比例：
$$
d = \frac{A_d}{A_0} = 1 - \frac{A_{\mathrm{eff}}}{A_0}
$$
对于一个全新的、无损的材料，$A_d = 0$，因此 $d=0$。当材料完全失效时，$A_d = A_0$，此时 $d=1$。因此，[损伤变量](@entry_id:197066) $d$ 的取值范围为 $[0, 1]$。

材料的响应并非由在整个名义[截面](@entry_id:154995)上平均的**名义应力** $\sigma = F/A_0$ 决定，而是由作用在实际承载区域上的“真实”应力决定。这个应力被称为**[有效应力](@entry_id:198048)** $\tilde{\sigma}$。假设在拉伸状态下，损伤区域（裂纹和孔洞）不传递拉力，则全部外力 $F$ 必须由[有效面积](@entry_id:197911) $A_{\mathrm{eff}}$ 来承担。因此，有效应力可以定义为：
$$
\tilde{\sigma} = \frac{F}{A_{\mathrm{eff}}}
$$
结合名义应力和[损伤变量](@entry_id:197066)的定义，我们可以推导出名义应力与有效应力之间的基本关系。由力平衡可知 $F = \sigma A_0 = \tilde{\sigma} A_{\mathrm{eff}}$。将 $A_{\mathrm{eff}} = A_0 (1-d)$ 代入，可得：
$$
\sigma A_0 = \tilde{\sigma} A_0 (1-d)
$$
由此得到：
$$
\tilde{\sigma} = \frac{\sigma}{1-d}
$$
这个关系式是[连续介质损伤力学](@entry_id:177438)的基石之一。值得注意的是，这个简洁的公式建立在一系列关键假设之上 [@problem_id:2924517]：
1.  **均匀性假设**：微观缺陷在[代表性体积元](@entry_id:164290)（Representative Volume Element, RVE）尺度上是统计[均匀分布](@entry_id:194597)的，使得[有效应力](@entry_id:198048)在承载区域上是均匀的。
2.  **损伤区域无应力**：在拉伸载荷下，损伤区域（如裂纹面）是自由的，不传递任何应力。
3.  **小应变假设**：材料的变形足够小，可以忽略[横截面](@entry_id:154995)积 $A_0$ 因泊松效应等引起的几何变化。
4.  **[尺度分离](@entry_id:270204)假设**：存在一个清晰的[尺度分离](@entry_id:270204)，即微观缺陷的尺寸远小于 RVE 的尺寸，而 RVE 的尺寸又远小于宏观结构的尺寸。

这一框架的核心思想是**等效性假设**，即受损材料的本构关系可以通过未受损材料的本构关系，但用有效应力替代名义应力来描述。

### [损伤的热力学框架](@entry_id:188411)：状态定律与耗散

为了确保损伤模型的物理真实性，其本构关系必须满足热力学定律。我们将采用基于内部变量的不[可逆过程](@entry_id:276625)[热力学](@entry_id:141121)框架来构建这些关系。对于[等温过程](@entry_id:143096)，[热力学第二定律](@entry_id:142732)要求系统的内禀耗散率 $\mathcal{D}$ 必须非负。

在小应变和等温条件下，局部形式的热力学第二定律（即 **Clausius–Duhem 不等式**）可以简化为机械[耗散不等式](@entry_id:188634) [@problem_id:2924540]：
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$
其中，$\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\boldsymbol{\varepsilon}$ 是[小应变张量](@entry_id:754968)，$\psi$ 是单位体积的**亥姆霍兹自由能**，上标点表示材料时间导数。[亥姆霍兹自由能](@entry_id:136442)是一个状态函数，对于一个可损伤的弹性材料，它依赖于当前的应变和损伤状态，即 $\psi = \psi(\boldsymbol{\varepsilon}, d)$。

利用[链式法则](@entry_id:190743)，$\psi$ 的时间导数为：
$$
\dot{\psi} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} : \dot{\boldsymbol{\varepsilon}} + \frac{\partial \psi}{\partial d} \dot{d}
$$
将此式代入[耗散不等式](@entry_id:188634)，我们得到：
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \left( \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} : \dot{\boldsymbol{\varepsilon}} + \frac{\partial \psi}{\partial d} \dot{d} \right) \ge 0
$$
整理后可得：
$$
\mathcal{D} = \left( \boldsymbol{\sigma} - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} \right) : \dot{\boldsymbol{\varepsilon}} - \frac{\partial \psi}{\partial d} \dot{d} \ge 0
$$
根据 **Coleman-Noll 程序**，此不等式必须对所有可能的、运动学上容许的过程（即任意的 $\dot{\boldsymbol{\varepsilon}}$）都成立。为了保证这一点，与 $\dot{\boldsymbol{\varepsilon}}$ 相乘的项必须为零 [@problem_id:2924515]。这给出了应力的**状态定律**：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$
这个关系表明，对于给定的损伤状态 $d$，应力可以从自由能势中通过对应变的求导得到，这是一种超弹性关系。

将应力状态定律代回，[耗散不等式](@entry_id:188634)简化为：
$$
\mathcal{D} = - \frac{\partial \psi}{\partial d} \dot{d} \ge 0
$$
这个不等式描述了由[损伤演化](@entry_id:184965)引起的[能量耗散](@entry_id:147406)。我们定义一个与[损伤变量](@entry_id:197066) $d$ 共轭的**[热力学力](@entry_id:161907)**，称为**[损伤能量释放率](@entry_id:195626)** $Y$：
$$
Y = - \frac{\partial \psi}{\partial d}
$$
$Y$ 代表了当损伤增加一个单位时，系统能量释放的速率，因此它是驱动[损伤演化](@entry_id:184965)的“力”。有了这个定义，[耗散不等式](@entry_id:188634)最终呈现为一个简洁而深刻的形式：
$$
\mathcal{D} = Y \dot{d} \ge 0
$$
由于损伤是一个不可逆过程（材料不会自发愈合），我们有 $\dot{d} \ge 0$。因此，为了满足[热力学第二定律](@entry_id:142732)，必须要求 $Y \ge 0$。

### 自由能势的构建

[热力学](@entry_id:141121)框架的建立为我们选择合适的[亥姆霍兹自由能](@entry_id:136442) $\psi(\boldsymbol{\varepsilon}, d)$ 提供了严格的准则。一个有效且一致的[自由能函数](@entry_id:749582)必须满足以下条件 [@problem_id:2924536]：

1.  **[热力学](@entry_id:141121)容许性**：对于所有可能的 $(\boldsymbol{\varepsilon}, d)$ 状态，其导出的[损伤能量释放率](@entry_id:195626) $Y = -\partial \psi / \partial d$ 必须非负。
2.  **无损状态**：当 $d=0$ 时，自由能必须退化为未受损材料的弹性应变能，即 $\psi(\boldsymbol{\varepsilon}, 0) = \psi_0(\boldsymbol{\varepsilon}) = \frac{1}{2} \boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon}$，其中 $\mathbb{C}_0$ 是初始[弹性张量](@entry_id:170728)。
3.  **完全损伤状态**：当 $d=1$ 时，材料完全失去承载能力，无法储存任何[弹性应变能](@entry_id:202243)，因此 $\psi(\boldsymbol{\varepsilon}, 1) = 0$。

一种常见的构建方式是将损伤效应通过一个退化函数 $g(d)$ 引入到未受损的自由能 $\psi_0$ 中。例如，以下两种形式在文献中很常见：

- **形式 A**: $\psi(\boldsymbol{\varepsilon}, d) = (1-d) \psi_0(\boldsymbol{\varepsilon})$
- **形式 B**: $\psi(\boldsymbol{\varepsilon}, d) = (1-d)^2 \psi_0(\boldsymbol{\varepsilon})$

我们来检验这两种形式。对于形式 A，[损伤能量释放率](@entry_id:195626)为 $Y = - \frac{\partial}{\partial d} [(1-d)\psi_0] = \psi_0(\boldsymbol{\varepsilon})$。由于[弹性应变能](@entry_id:202243) $\psi_0$ 总是非负的，因此 $Y \ge 0$ 恒成立。同时，当 $d=0$ 时 $\psi = \psi_0$，当 $d=1$ 时 $\psi=0$。因此，形式 A 是一个[热力学](@entry_id:141121)上容许的有效模型。

对于形式 B，能量释放率为 $Y = - \frac{\partial}{\partial d} [(1-d)^2 \psi_0] = 2(1-d)\psi_0(\boldsymbol{\varepsilon})$ [@problem_id:2924552]。由于 $d \in [0, 1]$，$(1-d) \ge 0$，因此 $Y \ge 0$ 也恒成立。该形式同样满足 $d=0$ 和 $d=1$ 时的边界条件。

这两种形式都与经典的**等效性假设**有关 [@problem_id:2924559]。
- **[应变等效](@entry_id:186173)性假设**：受损材料的[本构关系](@entry_id:186508)与未受损材料相同，但需将应力替换为有效应力。从 $\boldsymbol{\varepsilon} = \mathbb{S}_0 : \tilde{\boldsymbol{\sigma}} = \mathbb{S}_0 : (\boldsymbol{\sigma}/(1-d))$ 出发，可以推导出 $\boldsymbol{\sigma} = (1-d) \mathbb{C}_0 : \boldsymbol{\varepsilon}$。这对应于自由能 $\psi = (1-d)\psi_0(\boldsymbol{\varepsilon})$。
- **应力等效性假设**：受损材料的[本构关系](@entry_id:186508)与未受损材料相同，但需将应力替换为有效应力。从 $\tilde{\boldsymbol{\sigma}} = \mathbb{C}_0 : \boldsymbol{\varepsilon}$ 出发，即 $\boldsymbol{\sigma}/(1-d) = \mathbb{C}_0 : \boldsymbol{\varepsilon}$，同样可以推导出 $\boldsymbol{\sigma} = (1-d) \mathbb{C}_0 : \boldsymbol{\varepsilon}$。

有趣的是，在小应变线弹性框架下，这两种看似不同的假设导出了完全相同的[应力-应变关系](@entry_id:274093)和自由能形式。然而，它们的概念基础和在更复杂的模型（如[弹塑性](@entry_id:193198)损伤耦合）中的应用是不同的。例如，应力等效性假设在耦合塑性时非常方便，因为它允许在[有效应力](@entry_id:198048)空间中直接使用未受损材料的屈服准则。

### [损伤演化定律](@entry_id:184382)：率无关模型

确定了损伤的驱动力 $Y$ 之后，下一步是建立一个描述[损伤变量](@entry_id:197066) $d$ 如何随加载历史演化的**演化定律**。对于许多材料在准静态加载下的行为，可以采用**率无关**模型，这意味着演化不依赖于加载速率。

这种模型通常借鉴于率无关塑性理论的框架，其核心是引入一个**损伤准则**或**加载函数** $\phi$。该函数定义了在[热力学力](@entry_id:161907)空间中的一个弹性（或无损）区域。当状态点位于该区域内部时，损伤不发展；只有当状态点到达并试图穿出该区域边界时，损伤才会演化。

一个通用的损伤准则可以写成 $\phi(Y, \kappa) \le 0$，其中 $\kappa$ 是一个**历史变量**，用于描述损伤阈值的演化（即损伤硬化）。例如，$\kappa$ 可以是迄今为止材料所经历的最大[能量释放率](@entry_id:158357) [@problem_id:2924541]。

率无关的[损伤演化](@entry_id:184965)由一组被称为 **Kuhn-Tucker (KKT) [互补条件](@entry_id:747558)**的规则控制 [@problem_id:2924513]：
1.  **容许性条件**: $\phi(Y, \kappa) \le 0$
2.  **损伤不[可逆性](@entry_id:143146)**: $\dot{d} \ge 0$
3.  **[互补条件](@entry_id:747558)**: $\dot{d} \phi(Y, \kappa) = 0$

第三条[互补条件](@entry_id:747558)是关键：它表明，如果损伤正在演化（$\dot{d} > 0$），那么状态点必须位于损伤面上（$\phi = 0$）；反之，如果状态点严格位于弹性域内部（$\phi  0$），则损伤必须停止演化（$\dot{d} = 0$）。

当损伤处于活动状态时（$\phi=0$ 且 $\dot{d}>0$），状态点必须保持在损伤面上，这意味着 $\phi$ 的时间导数必须为零。这被称为**一致性条件**：
$$
\dot{\phi} = \frac{\partial \phi}{\partial Y} \dot{Y} + \frac{\partial \phi}{\partial \kappa} \dot{\kappa} = 0
$$
这个方程用于确定在加载过程中损伤和硬化变量的增量。

最后，损伤的增量方向由**关联[流动法则](@entry_id:177163)**给出，该法则假定损伤率的方向与损伤面在[热力学力](@entry_id:161907)空间中的法线方向一致：
$$
\dot{d} = \dot{\lambda} \frac{\partial \phi}{\partial Y}
$$
其中 $\dot{\lambda} \ge 0$ 是一个非负的**一致性参数**（或损伤乘子），其大小由一致性条件确定。

例如，对于一个简单的损伤准则 $\phi = Y - R(\kappa)$，其中 $R(\kappa)$ 是损伤抗力函数。关联流动法则给出 $\dot{d} = \dot{\lambda} \frac{\partial \phi}{\partial Y} = \dot{\lambda}$。这意味着损伤率直接等于一致性参数 [@problem_id:2924541]。

### [模型比较](@entry_id:266577)与高级主题

#### [损伤与塑性](@entry_id:203986)的比较

[热力学](@entry_id:141121)框架揭示了损伤和塑性这两种非弹性行为的深刻异同 [@problem_id:2895587]。

- **相似之处**：两者都可以被描述为由[热力学力](@entry_id:161907)驱动的内部变量的演化。率无关塑性和率无关损伤都采用加载函数、KKT 条件和一致性条件来控制其演化。
- **根本区别**：塑性是由于[位错运动](@entry_id:143448)等机制导致的**不可恢复的变形**，它改变了材料的形状但通常不改变其弹性刚度。在[应力-应变曲线](@entry_id:159459)上，塑性加载后的卸载路径与初始弹性加载路径平行。而损伤是材料完整性的**退化**，其宏观表现为**弹性刚度的降低**。因此，在损伤模型中，卸载路径的斜率会随着损伤的累积而减小。

简而言之，塑性是关于**永久应变** $\boldsymbol{\varepsilon}^p$ 的理论，而损伤是关于**[刚度退化](@entry_id:202277)** $\mathbb{C}(d)$ 的理论。

#### [拉压不对称性](@entry_id:201728)

简单的标量损伤模型，如 $\psi = (1-d)\psi_0(\boldsymbol{\varepsilon})$，存在一个严重的物理缺陷：它们预测材料在任何非零应变状态下都会产生损伤，包括纯静水压缩。然而，对于混凝土、[陶瓷](@entry_id:148626)、岩石等准[脆性](@entry_id:198160)材料，拉伸是损伤的主要驱动因素，而压缩通常不会引起（或以非常不同的方式引起）损伤。

为了解决这个问题，需要对模型进行修正，以区分拉伸和压缩状态的作用。一种行之有效的方法是对[弹性应变能](@entry_id:202243)进行**拉伸-压缩分解** [@problem_id:2924545]。其核心思想是将未受损的自由能 $\psi_0$ 分解为拉伸部分 $\psi_0^+$ 和压缩部分 $\psi_0^-$，即 $\psi_0 = \psi_0^+ + \psi_0^-$，然后只让损伤影响拉伸部分：
$$
\psi(\boldsymbol{\varepsilon}, d) = (1-d) \psi_0^+(\boldsymbol{\varepsilon}) + \psi_0^-(\boldsymbol{\varepsilon})
$$
这样，[损伤能量释放率](@entry_id:195626)变为 $Y = \psi_0^+(\boldsymbol{\varepsilon})$。在纯压缩状态下，$\psi_0^+(\boldsymbol{\varepsilon}) = 0$，因此 $Y=0$，损伤不会演化。

一个严谨且客观的分解方法是基于应变张量的**谱分解**。首先，计算[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 的[主应变](@entry_id:197797) $\varepsilon_i$ 和对应的[主方向](@entry_id:276187) $\boldsymbol{n}_i$。然后定义[应变张量](@entry_id:193332)的正部和负部：
$$
\boldsymbol{\varepsilon}^+ = \sum_{i=1}^{3} \langle \varepsilon_i \rangle_+ \boldsymbol{n}_i \otimes \boldsymbol{n}_i \quad , \quad \boldsymbol{\varepsilon}^- = \sum_{i=1}^{3} \langle \varepsilon_i \rangle_- \boldsymbol{n}_i \otimes \boldsymbol{n}_i
$$
其中 $\langle x \rangle_+ = \frac{1}{2}(x + |x|)$ 是正部分算子（Macaulay 括号），$\langle x \rangle_- = \frac{1}{2}(x - |x|)$ 是负部分算子。

基于此，可以将[各向同性线弹性](@entry_id:185899)自由能（以 Lamé 参数 $\lambda$ 和 $\mu$ 表示）分解为 [@problem_id:2924545]：
$$
\psi^{+}(\boldsymbol{\varepsilon}) = \frac{1}{2}\lambda \langle \mathrm{tr}(\boldsymbol{\varepsilon}) \rangle_+^2 + \mu \boldsymbol{\varepsilon}^+ : \boldsymbol{\varepsilon}^+
$$
$$
\psi^{-}(\boldsymbol{\varepsilon}) = \frac{1}{2}\lambda \langle \mathrm{tr}(\boldsymbol{\varepsilon}) \rangle_-^2 + \mu \boldsymbol{\varepsilon}^- : \boldsymbol{\varepsilon}^-
$$
这个分解保证了 $\psi_0 = \psi_0^+ + \psi_0^-$，并且在任何[主应变](@entry_id:197797)均为非正的压缩状态下，$\psi_0^+$ 都精确为零，从而正确地抑制了压缩状态下的[损伤演化](@entry_id:184965)。这种方法为模拟准[脆性](@entry_id:198160)材料的复杂行为提供了坚实的理论基础。