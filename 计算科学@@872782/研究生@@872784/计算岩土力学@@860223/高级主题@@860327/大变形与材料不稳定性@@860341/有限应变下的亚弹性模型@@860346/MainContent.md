## 引言
在大规模变形的岩土工程问题中，如滑坡动力学、地基失稳和结构-土体相互作用，精确描述材料的力学行为至关重要。许多[地质材料](@entry_id:749838)表现出复杂的[非线性响应](@entry_id:188175)，其刚度随应力状态而变化。[亚弹性模型](@entry_id:184632)为描述这类材料提供了一个增量式的本构框架，直接关联了应力率和变形率。然而，在[有限应变理论](@entry_id:176941)中，一个核心挑战随之出现：标准的应力时间导数并非客观量，它会随观察者的[刚体转动](@entry_id:191086)而改变，导致物理上不一致的预测。因此，如何构建一个满足[材料标架无关性](@entry_id:177919)原理的本构关系，是[亚弹性](@entry_id:204371)建模必须解决的知识缺口。

本文旨在系统性地阐述[大应变](@entry_id:751152)[亚弹性](@entry_id:204371)建模的理论与实践。通过学习本文，读者将能够掌握解决上述挑战的核心方法。在“原理与机制”章节中，我们将建立有限变形的[运动学](@entry_id:173318)框架，并阐明为何必须引入[客观应力率](@entry_id:199282)，同时剖析几种关键[客观率](@entry_id:198692)的定义与物理意义。接下来的“应用与交叉学科联系”章节将展示[亚弹性模型](@entry_id:184632)如何被扩展和应用于解决实际的岩土工程问题，包括参数化、多物理场耦合以及在计算力学中面临的挑战。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识转化为解决问题的能力。

## 原理与机制

本章深入探讨[大应变](@entry_id:751152)[亚弹性](@entry_id:204371)建模的理论基础和核心机制。我们将从有限变形运动学的基本定义出发，建立描述变形、转动和应力的严谨框架。随后，我们将引入[亚弹性](@entry_id:204371)[本构关系](@entry_id:186508)的核心概念，即[客观应力率](@entry_id:199282)，并详细阐述其在确保材料响应的客观性方面不可或缺的作用。最后，我们将剖析几种关键的[客观率](@entry_id:198692)，并揭示[亚弹性模型](@entry_id:184632)固有的理论缺陷，为后续章节中更先进的本构理论奠定基础。

### 有限变形运动学

在[有限应变理论](@entry_id:176941)中，精确描述一个连续体从其初始（参考）构型到当前（空间）构型的运动是所有分析的起点。

#### 变形梯度与速度梯度

一个[质点](@entry_id:186768)在参考构型中的位置由向量 $\boldsymbol{X}$ 表示，在当前构型中的位置由 $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$ 表示。描述这种局部变形的核心工具是 **变形梯度 (deformation gradient)** $\boldsymbol{F}$，其定义为：
$$
\boldsymbol{F} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}}
$$
变形梯度 $\boldsymbol{F}$ 包含了关于局部拉伸、压缩和旋转的全部信息。为了描述变形的速率，我们引入 **[空间速度梯度](@entry_id:187198) (spatial velocity gradient)** $\boldsymbol{L}$，它由[空间速度](@entry_id:190294)场 $\boldsymbol{v}(\boldsymbol{x}, t)$ 的梯度给出：
$$
\boldsymbol{L} = \nabla \boldsymbol{v} = \frac{\partial \boldsymbol{v}}{\partial \boldsymbol{x}}
$$
$\boldsymbol{L}$ 与 $\boldsymbol{F}$ 的[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{F}}$ 之间存在一个基本关系：$\boldsymbol{L} = \dot{\boldsymbol{F}} \boldsymbol{F}^{-1}$。

#### 变形率与自旋

速度梯度 $\boldsymbol{L}$ 本身可以被分解为其对称[部分和](@entry_id:162077)反对称部分，这两部分具有截然不同的物理意义 [@problem_id:3530881]。

对称部分被称为 **变形率张量 (rate-of-deformation tensor)** 或伸长张量，用 $\boldsymbol{d}$ 表示：
$$
\boldsymbol{d} = \mathrm{sym}(\boldsymbol{L}) = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^{\mathrm{T}})
$$
$\boldsymbol{d}$ 描述了材料单元体真实的形状变化速率，包括沿不同方向的拉伸或压缩（由其对角分量表示）和剪切角的变化（由其非对角分量表示）。值得注意的是，[体积应变率](@entry_id:272471)完全由 $\boldsymbol{d}$ 的迹（trace）决定，即 $\mathrm{tr}(\boldsymbol{d})$，它等于 $\mathrm{tr}(\boldsymbol{L})$，因为[反对称张量](@entry_id:199349)的迹恒为零。

反对称部分被称为 **[自旋张量](@entry_id:187346) (spin tensor)** 或[涡量张量](@entry_id:189621)，用 $\boldsymbol{w}$ 表示：
$$
\boldsymbol{w} = \mathrm{skew}(\boldsymbol{L}) = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^{\mathrm{T}})
$$
$\boldsymbol{w}$ 描述了材料单元体的瞬时[刚体转动](@entry_id:191086)速率。一个至关重要的概念是，这种[刚体转动](@entry_id:191086)本身并不引起材料的内应力变化，也不做功。[应力功率](@entry_id:182907)（单位体积的内功率）由 $\boldsymbol{\sigma} : \boldsymbol{L}$ 给出。由于柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是对称的，而 $\boldsymbol{w}$ 是反对称的，它们的[双点积](@entry_id:748648)恒为零，即 $\boldsymbol{\sigma} : \boldsymbol{w} = 0$。因此，[应力功率](@entry_id:182907)完全由变形率决定：
$$
P = \boldsymbol{\sigma} : \boldsymbol{L} = \boldsymbol{\sigma} : (\boldsymbol{d} + \boldsymbol{w}) = \boldsymbol{\sigma} : \boldsymbol{d}
$$
这清晰地表明，只有引起形状变化的变形率 $\boldsymbol{d}$ 才与应力做功相关，而自旋 $\boldsymbol{w}$ 则不贡献机械功 [@problem_id:3530881]。

#### [有限应变度量](@entry_id:185716)

当变形不再微小时，有多种方式可以度量应变。

**[格林-拉格朗日应变](@entry_id:170427) (Green-Lagrange strain)** $\boldsymbol{E}$ 是一种在参考构型中定义的[应变度量](@entry_id:755495)，它通过[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C} = \boldsymbol{F}^{\mathrm{T}}\boldsymbol{F}$ 定义：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})
$$
与之对应，**[阿尔曼西应变](@entry_id:191140) (Almansi strain)** $\boldsymbol{e}$ 是一种在当前构型中定义的[应变度量](@entry_id:755495)，通过[左柯西-格林张量](@entry_id:186163) $\boldsymbol{b} = \boldsymbol{F}\boldsymbol{F}^{\mathrm{T}}$ 的逆来定义：
$$
\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{b}^{-1})
$$
为了更深入地理解变形，我们可以使用 **极分解 (polar decomposition)** 将 $\boldsymbol{F}$ 分解为一个纯旋转 $\boldsymbol{R}$ 和一个纯拉伸 $\boldsymbol{U}$（或 $\boldsymbol{V}$）：
$$
\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U} = \boldsymbol{V}\boldsymbol{R}
$$
其中 $\boldsymbol{U}$ 是右[拉伸张量](@entry_id:193200)，$\boldsymbol{V}$ 是左[拉伸张量](@entry_id:193200)，$\boldsymbol{R}$ 是一个正常正交张量，代表了材料的[刚体转动](@entry_id:191086)部分。

基于这种分解，可以定义 **[亨基应变](@entry_id:191329) (Hencky strain)** 或[对数应变](@entry_id:751438) $\boldsymbol{E}_{H}$：
$$
\boldsymbol{E}_{H} = \ln(\boldsymbol{U})
$$
其中 $\ln(\cdot)$ 表示主[矩阵对数](@entry_id:169041)。[亨基应变](@entry_id:191329)的一个优越特性是，对于一系列共轴的拉伸变形（即各步变形的主方向相同），总的[亨基应变](@entry_id:191329)等于各步应变之和。而[格林-拉格朗日应变](@entry_id:170427)和[阿尔曼西应变](@entry_id:191140)则不具备这种可加性 [@problem_id:3530905]。

### 应力度量与[功共轭](@entry_id:194957)

在有限应变框架下，单一的应力概念已不足以满足所有需求。我们需要引入多种应力度量，它们分别与特定的构型和[应变度量](@entry_id:755495)相关联 [@problem_id:3530946]。

#### 多种应力度量

- **柯西应力 (Cauchy stress)** $\boldsymbol{\sigma}$：这是物理上“真实”的应力，定义为当前构型中的作用力除以当前构型的面积。它是对称的，并且在[欧拉描述](@entry_id:264722)（空间描述）中使用。

- **[第一皮奥拉-基尔霍夫应力](@entry_id:163971) (First Piola-Kirchhoff stress, PK1)** $\boldsymbol{P}$：这是一种名义应力，它将当前构型中的力与参考构型中的面积相关联。$\boldsymbol{P}$ 通常是非对称的。

- **[第二皮奥拉-基尔霍夫应力](@entry_id:173163) (Second Piola-Kirchhoff stress, PK2)** $\boldsymbol{S}$：这是一种完全拉格朗日（物质）的应力度量，它将力向量和面积向量都映射回参考构型。$\boldsymbol{S}$ 是对称的。

- **[基尔霍夫应力](@entry_id:751039) (Kirchhoff stress)** $\boldsymbol{\tau}$：它是柯西应力的一个缩放版本，$\boldsymbol{\tau} = J\boldsymbol{\sigma}$，其中 $J = \det(\boldsymbol{F})$ 是变形梯度的[雅可比行列式](@entry_id:137120)。引入它的主要目的是为了简化功率表达式。

#### 转换关系

这些应力度量之间存在精确的转换关系，这些关系可以通过力的平衡和 Nanson 公式（$n \, da = J \boldsymbol{F}^{-\mathrm{T}} N \, dA$）推导出来 [@problem_id:3530946]：
$$
\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-\mathrm{T}} = \boldsymbol{\tau} \boldsymbol{F}^{-\mathrm{T}}
$$
$$
\boldsymbol{S} = \boldsymbol{F}^{-1} \boldsymbol{P} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-\mathrm{T}} = \boldsymbol{F}^{-1} \boldsymbol{\tau} \boldsymbol{F}^{-\mathrm{T}}
$$
从这些关系可以导出在物质和空间描述之间转换[应力张量](@entry_id:148973)的 **推前 (push-forward)** 和 **[拉回](@entry_id:160816) (pull-back)** 操作。例如，对称的 PK2 应力 $\boldsymbol{S}$ 可以被推前到空间构型，得到对称的[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}$：
$$
\boldsymbol{\tau} = \boldsymbol{F} \boldsymbol{S} \boldsymbol{F}^{\mathrm{T}} \quad (\text{Push-forward})
$$
反之，[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}$ 可以被[拉回](@entry_id:160816)到参考构型，得到 PK2 应力 $\boldsymbol{S}$：
$$
\boldsymbol{S} = \boldsymbol{F}^{-1} \boldsymbol{\tau} \boldsymbol{F}^{-\mathrm{T}} \quad (\text{Pull-back})
$$

#### [功共轭](@entry_id:194957)概念

为了确保[热力学一致性](@entry_id:138886)，本构模型中的应力和应变（或[应变率](@entry_id:154778)）必须是 **[功共轭](@entry_id:194957) (work-conjugate)** 的，这意味着它们的[双点积](@entry_id:748648)给出了单位体积的功率。通过分析内部功率的等价性，我们可以确定几对重要的[功共轭](@entry_id:194957)对 [@problem_id:3530947, @problem_id:3530946]：
$$
p_V = \boldsymbol{S} : \dot{\boldsymbol{E}} = \boldsymbol{P} : \dot{\boldsymbol{F}} = \boldsymbol{\tau} : \boldsymbol{d} = J (\boldsymbol{\sigma} : \boldsymbol{d})
$$
其中 $p_V$ 是单位参考体积的功率。这个恒等式揭示了以下[功共轭](@entry_id:194957)关系：
- 在物质描述中，PK2 应力 $\boldsymbol{S}$ 与[格林-拉格朗日应变](@entry_id:170427)率 $\dot{\boldsymbol{E}}$ 共轭。
- 在空间描述中，[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}$ 与变形率张量 $\boldsymbol{d}$ 共轭。
- 此外，对于[各向同性材料](@entry_id:170678)，[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}$ 也与[亨基应变](@entry_id:191329)的一种速率形式[功共轭](@entry_id:194957)，这使得[对数应变](@entry_id:751438)在超弹性模型中特别有用 [@problem_id:3530905]。

### [亚弹性](@entry_id:204371)本构框架

[亚弹性模型](@entry_id:184632)直接构建了应力率和变形率之间的关系，这是一种增量或速率形式的本构理论。

#### 率形式的本构律

一个典型的各向同性线[亚弹性模型](@entry_id:184632)的通用形式为 [@problem_id:3530923]：
$$
\overset{\circ}{\boldsymbol{\sigma}} = 2\mu\boldsymbol{d} + \lambda\mathrm{tr}(\boldsymbol{d})\boldsymbol{I}
$$
其中 $\lambda$ 和 $\mu$ 是材料参数（类似于拉梅参数），$\boldsymbol{I}$ 是单位张量，而 $\overset{\circ}{\boldsymbol{\sigma}}$ 是一个**客观的**应力率。对于岩土材料，这些模量通常是压力相关的，例如，[体积模量](@entry_id:160069) $K$ 和剪切模量 $G$ 可以表示为平均应力 $p$ 的函数，如 $K(p) = K_0 + \alpha p$ 和 $G(p) = G_0 + \beta p$ [@problem_id:3530880]。

#### 客观性问题

在构建[本构关系](@entry_id:186508)时，一个核心要求是它必须满足 **[材料标架无关性](@entry_id:177919) (Material Frame Indifference, MFI)** 原理，也称为[客观性原理](@entry_id:185412)。该原理指出，材料的本构响应不应依赖于观察者（或其[坐标系](@entry_id:156346)）的[刚体运动](@entry_id:193355)。

然而，柯西应力 $\boldsymbol{\sigma}$ 的标准[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ **不是**客观的 [@problem_id:3530923]。在一个叠加了[刚体转动](@entry_id:191086)的观察者看来，$\dot{\boldsymbol{\sigma}}$ 的变换规律很复杂，它不符合一个客观张量率的变换法则。这意味着，如果我们错误地使用 $\dot{\boldsymbol{\sigma}}$ 来构建本构律，例如 $\dot{\boldsymbol{\sigma}} = f(\boldsymbol{d}, \boldsymbol{\sigma})$，那么两个以不同角速度旋转的观察者将会推断出不同的材料属性，这在物理上是荒谬的。

解决方案是使用 **[客观应力率](@entry_id:199282) (objective stress rates)**。这些特殊定义的应力率被精确地构造出来，以消除由于材料的[刚体转动](@entry_id:191086)（由[自旋张量](@entry_id:187346) $\boldsymbol{w}$ 体现）而引起的柯西应力分量的变化，从而只保留由真实变形（由变形率张量 $\boldsymbol{d}$ 体现）引起的应力变化部分 [@problem_id:3530881]。

一个直接的推论是，对于任何纯[刚体运动](@entry_id:193355)（其中 $\boldsymbol{d}=0$），任何客观的[亚弹性模型](@entry_id:184632)都必须预测[客观应力率](@entry_id:199282)为零，即 $\overset{\circ}{\boldsymbol{\sigma}} = \boldsymbol{0}$。这确保了材料在无变形的纯旋转下不会产生虚假的内应力 [@problem_id:3530881, @problem_id:3530923]。

### 关键的[客观应力率](@entry_id:199282)及其性质

多种[客观应力率](@entry_id:199282)已被提出，它们本质上反映了选择不同旋转参照系来衡量应力变化。

#### 协同转动率 (Corotational Rates)

协同转动率背后的思想是，在一个与材料一同旋转的“协同转动”[坐标系](@entry_id:156346)中去观察[应力张量](@entry_id:148973)。在该[坐标系](@entry_id:156346)中观察到的应力变化率自然是客观的。

##### [Jaumann 率](@entry_id:185572)

**[Jaumann 率](@entry_id:185572)**（或 Zaremba-Jaumann率）是最著名的协同转动率之一。它通过使用连续体的[自旋张量](@entry_id:187346) $\boldsymbol{w}$ 来校正[物质时间导数](@entry_id:190892)，定义为 [@problem_id:3530941]：
$$
\boldsymbol{\sigma}^{\nabla} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\boldsymbol{w} - \boldsymbol{w}\boldsymbol{\sigma}
$$
这里的[自旋张量](@entry_id:187346) $\boldsymbol{w} = \mathrm{skew}(\boldsymbol{L})$ 代表了材料单元体本身的瞬时转速。

##### Green-Naghdi 率

**Green-Naghdi (GN) 率**是另一种重要的协同转动率。它使用的“协同转动”是由极分解 $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$ 中的[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 所定义的。GN 率使用极分解旋转的自旋 $\boldsymbol{\Omega}_{R} = \dot{\boldsymbol{R}}\boldsymbol{R}^{\mathrm{T}}$ 来定义 [@problem_id:3530897]：
$$
\boldsymbol{\sigma}^{\triangledown} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}_{R}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}_{R}
$$
GN 率有一个非常直观的物理解释：它是在旋转坐标系中观察到的应力张量 $\tilde{\boldsymbol{\sigma}} = \boldsymbol{R}^{\mathrm{T}}\boldsymbol{\sigma}\boldsymbol{R}$ 的普通时间导数，然后再转换回空间[坐标系](@entry_id:156346) [@problem_id:3530897]。

在一般变形中，连续体自旋 $\boldsymbol{w}$ 和极分解自旋 $\boldsymbol{\Omega}_{R}$ 并**不**相同。一个经典的例子是平面简单剪切，其变形梯度为 $\boldsymbol{F} = \begin{pmatrix} 1  \gamma \\ 0  1 \end{pmatrix}$。在这种情况下，可以推导出 $\boldsymbol{w}$ 是一个常数矩阵，而 $\boldsymbol{\Omega}_{R}$ 则随着剪切应变 $\gamma$ 的增加而变化 [@problem_id:3530891]。$\boldsymbol{w}$ 和 $\boldsymbol{\Omega}_{R}$ 之间的差异仅在 $\boldsymbol{U}$ 和 $\dot{\boldsymbol{U}}$ 可交换时才消失 [@problem_id:3530897]。因此，使用 [Jaumann 率](@entry_id:185572)和 GN 率的[亚弹性模型](@entry_id:184632)通常会预测出不同的应力响应 [@problem_id:3530923]。

#### Truesdell 率

**Truesdell 率** $\overset{\triangle}{\boldsymbol{\sigma}}$ 属于另一类被称为[对流](@entry_id:141806)率（convected rates）的[客观率](@entry_id:198692)。它的定义较为复杂：
$$
\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^{\mathrm{T}} + \mathrm{tr}(\boldsymbol{d})\boldsymbol{\sigma}
$$
尽管形式复杂，但 Truesdell 率具有一个独特的、理论上非常重要的性质：它为物质描述和空间描述之间提供了一个直接的桥梁。一个在物质构型中以 PK2 应力率 $\dot{\boldsymbol{S}}$ 和[格林-拉格朗日应变](@entry_id:170427)率 $\dot{\boldsymbol{E}}$ 写出的[本构关系](@entry_id:186508) $\dot{\boldsymbol{S}} = \mathbb{C} : \dot{\boldsymbol{E}}$，可以被精确地、无附加项地转换为一个在空间构型中以 Truesdell 率和变形率张量 $\boldsymbol{d}$ 写出的关系 $\overset{\triangle}{\boldsymbol{\sigma}} = \boldsymbol{c} : \boldsymbol{d}$。其中，空间[弹性张量](@entry_id:170728) $\boldsymbol{c}$ 是物质[弹性张量](@entry_id:170728) $\mathbb{C}$ 的推前形式。而 [Jaumann 率](@entry_id:185572)等其他协同转动率则不具备这种简洁的映射关系 [@problem_id:3530947]。

### [亚弹性模型](@entry_id:184632)的缺陷与病态行为

尽管[亚弹性模型](@entry_id:184632)在概念上相对简单，并且在小应变增量计算中仍有应用，但它们存在严重的理论缺陷，这些缺陷在有限应变下会表现为非物理的病态行为。

#### 不[可积性](@entry_id:142415)与路径依赖

[亚弹性模型](@entry_id:184632)的主要理论缺陷是它们通常是 **不可积的 (non-integrable)**。这意味着应力通常不能从一个应变势能函数（即[应变能密度函数](@entry_id:755490)）中导出。这类模型不属于更具物理基础的[超弹性](@entry_id:159356)（hyperelastic）模型范畴。

一个直接的后果是 **路径依赖 (path dependence)**。对于一个[亚弹性](@entry_id:204371)材料，其最终应力状态不仅取决于最终的变形状态，还取决于达到该状态所经历的变形路径。我们可以通过一个计算实验来清晰地展示这一点 [@problem_id:3530880]：考虑一个初始受压的土样，我们对其施加两种不同的变形序列。(A) 先施加一个简单剪切，再施加一个单轴压缩；(B) 先施加同样的单轴压缩，再施加同样的简单剪切。由于变形的有限性和非交换性，这两个序列的最终变形状态不同，更重要的是，即使它们能达到相同的最终变形状态，计算结果也会显示最终的柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}_{\mathrm{final}}^{A}$ 和 $\boldsymbol{\sigma}_{\mathrm{final}}^{B}$ 是不同的。这表明，对于[亚弹性](@entry_id:204371)材料，变形历史至关重要，这与弹性材料的行为（应力仅由当前变形决定）形成鲜明对比。

#### 简单剪切中的虚假振荡

[亚弹性模型](@entry_id:184632)最著名的病态行为之一是在[大应变](@entry_id:751152)简单剪切下的虚假应力[振荡](@entry_id:267781)。考虑一个以恒定剪切率 $\dot{\gamma}$ 进行的简单剪切流动。如果使用基于 [Jaumann 率](@entry_id:185572)的[亚弹性模型](@entry_id:184632)来预测应力响应，结果会出乎意料 [@problem_id:3530929]。

初始时，剪应力 $\sigma_{12}$ 会随[剪应变](@entry_id:175241) $\gamma$ 的增加而增加，这符合物理直觉。然而，当[剪应变](@entry_id:175241)达到一定程度时，剪应力会达到一个峰值，然后开始减小，甚至变为负值，随后在零值附近[振荡](@entry_id:267781)。同时，[法向应力](@entry_id:260622)分量 $\sigma_{11}$ 和 $\sigma_{22}$ 也会表现出类似的[振荡](@entry_id:267781)行为。这种预测与实验中观察到的单调或渐进饱和的应力响应完全不符。这种非物理行为的根源在于，[Jaumann 率](@entry_id:185572)使用的协同转动框架（由 $\boldsymbol{w}$ 定义）在简单剪切中会“过度旋转”，导致应力张量在固定的空间[坐标系](@entry_id:156346)中来回摆动 [@problem_id:3530929]。

这些理论和实践上的缺陷凸显了[亚弹性模型](@entry_id:184632)在模拟[大应变](@entry_id:751152)问题时的局限性，并推动了基于超弹性理论的更稳健的[本构模型](@entry_id:174726)的发展。然而，对[亚弹性](@entry_id:204371)原理的理解对于掌握有限变形力学的历史发展和理解现代计算方法中的一些数值技术仍然至关重要。