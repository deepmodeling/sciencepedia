## 引言
在[计算固体力学](@entry_id:169583)的广阔领域中，对结构和材料行为的精确预测是工程设计与科学探索的核心。线性分析，尽管简洁高效，但其基本假设——响应与载荷成正比——在面对现实世界中众多复杂现象时显得力不从心。当结构经历大位移、材料发生屈服或物体间发生接触时，系统行为便进入了[非线性](@entry_id:637147)的范畴。准确捕捉这些行为对于保证结构安全、优化产品性能以及推动科学创新至关重要。然而，[非线性](@entry_id:637147)行为的来源多样且机理复杂，构成了一道知识鸿沟，需要系统性的梳理与理解。

本文旨在填补这一鸿沟，为读者提供一个关于[计算固体力学](@entry_id:169583)中[非线性](@entry_id:637147)来源的全面指南。我们将系统地剖析三大[非线性](@entry_id:637147)根源，引领读者逐步深入这一核心主题。在“原理与机制”一章中，我们将奠定理论基石，详细阐述几何、材料及[接触非线性](@entry_id:747785)的基本物理原理和数学表述。随后的“应用与跨学科联系”一章将理论付诸实践，通过一系列工程与科学案例，展示这些[非线性](@entry_id:637147)概念如何被用于解决从结构失稳到生物力学等前沿问题。最后，在“动手实践”一章中，读者将有机会通过具体的计算练习，巩固并应用所学知识。通过这一结构化的学习路径，本文将帮助你构建起从理论基础到高级应用的完整[非线性](@entry_id:637147)分析知识体系。

## 原理与机制

在[计算固体力学](@entry_id:169583)中，[非线性](@entry_id:637147)行为源于[系统响应](@entry_id:264152)与所施加的载荷或位移之间不再成正比。这种不成比例性可能由多种物理现象引起，通常分为三大类：[几何非线性](@entry_id:169896)、[材料非线性](@entry_id:162855)以及[接触非线性](@entry_id:747785)。本章将深入探讨这三种[非线性](@entry_id:637147)来源的根本原理及其在力学模型中的数学表述。

### [几何非线性](@entry_id:169896)：大变形[运动学](@entry_id:173318)

[几何非线性](@entry_id:169896)源于当结构发生显著的位移和转动时，平衡方程必须在变形后的构型上建立，并且[应变-位移关系](@entry_id:173321)变得不再是线性的。

#### 基本运动学量

为了精确描述大变形，我们必须区分物体的两个构型：未变形的**参考构型**（或称[材料构型](@entry_id:183091)），记为 $\Omega_0$，以及变形后的**当前构型**（或称空间构型），记为 $\Omega$。物质点在参考构型中的位置用向量 $\boldsymbol{X}$ 表示，在当前构型中的位置用 $\boldsymbol{x}$ 表示。

连接这两个构型的核心是**变形映射** $\boldsymbol{\varphi}$，它将每个物[质点](@entry_id:186768)从其[参考位](@entry_id:754187)置映射到当前位置：$\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$。相应地，**位移向量**定义为 $\boldsymbol{u}(\boldsymbol{X}, t) = \boldsymbol{x} - \boldsymbol{X}$。

描述局部变形的关键物理量是**变形梯度** $\boldsymbol{F}$。它是一个[二阶张量](@entry_id:199780)，定义为变形映射对参考坐标的梯度：
$$
\boldsymbol{F} = \frac{\partial \boldsymbol{\varphi}}{\partial \boldsymbol{X}} = \nabla_{\boldsymbol{X}} \boldsymbol{\varphi}
$$
变形梯度建立了参考构型中一个无限小[线元](@entry_id:196833) $d\boldsymbol{X}$ 与其在当前构型中对应线元 $d\boldsymbol{x}$ 之间的关系：$d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$。利用位移的定义，$\boldsymbol{F}$ 也可以表示为 $\boldsymbol{F} = \boldsymbol{I} + \nabla_{\boldsymbol{X}}\boldsymbol{u}$，其中 $\boldsymbol{I}$ 是单位张量。

在线性[小变形理论](@entry_id:174991)中，我们使用[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla_{\boldsymbol{X}}\boldsymbol{u} + (\nabla_{\boldsymbol{X}}\boldsymbol{u})^{\mathsf{T}})$。然而，在大变形中，该定义不足以描述变形，因为它忽略了[位移梯度](@entry_id:165352)的二次项。为了[正确度](@entry_id:197374)量变形，我们考察[线元](@entry_id:196833)长度的平方的变化。在当前构型中，[线元](@entry_id:196833)长度的平方为：
$$
ds^2 = d\boldsymbol{x} \cdot d\boldsymbol{x} = (\boldsymbol{F} d\boldsymbol{X}) \cdot (\boldsymbol{F} d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}) d\boldsymbol{X}
$$
其中，张量 $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$ 被称为**右柯西-格林变形张量**。它是一个定义在参考构型上的[对称张量](@entry_id:148092)，用于度量物质线元的拉伸。$\boldsymbol{C}$ 的一个重要特性是它对于叠加在当前构型上的[刚体转动](@entry_id:191086)是客观的（或称标架无关的），这意味着它只度量纯变形，而滤除了[刚体转动](@entry_id:191086)的影响。

基于 $\boldsymbol{C}$，我们可以定义一个真正度量应变的张量，即**[格林-拉格朗日应变张量](@entry_id:187745)** $\boldsymbol{E}$：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I}) = \frac{1}{2}(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} - \boldsymbol{I})
$$
将 $\boldsymbol{F} = \boldsymbol{I} + \nabla_{\boldsymbol{X}}\boldsymbol{u}$ 代入，我们得到：
$$
\boldsymbol{E} = \frac{1}{2}((\nabla_{\boldsymbol{X}}\boldsymbol{u}) + (\nabla_{\boldsymbol{X}}\boldsymbol{u})^{\mathsf{T}} + (\nabla_{\boldsymbol{X}}\boldsymbol{u})^{\mathsf{T}}(\nabla_{\boldsymbol{X}}\boldsymbol{u}))
$$
这个表达式明确显示，[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ 是[位移梯度](@entry_id:165352)的**二次函数**。这个[非线性](@entry_id:637147)的[应变-位移关系](@entry_id:173321)正是**[几何非线性](@entry_id:169896)**的根本来源。当[位移梯度](@entry_id:165352)很小时，二次项可以忽略不计，此时 $\boldsymbol{E}$ 退化为线性应变张量 $\boldsymbol{\varepsilon}$ [@problem_id:3601252]。

#### [几何非线性](@entry_id:169896)的计算格式

在求解[非线性](@entry_id:637147)问题时，[平衡方程](@entry_id:172166)的弱形式（虚功原理）必须在某个构型上进行积分。这导致了两种主要的计算格式。

**总拉格朗日 (Total Lagrangian, TL) 格式**：在该格式中，所有的运动学和动力学量都被映射回固定的、未变形的参考构型 $\Omega_0$ 进行计算。积分和求导都是相对于参考坐标 $\boldsymbol{X}$ 进行的。其弱形式的[内虚功](@entry_id:172278)项表示为：
$$
\delta W_{\text{int}} = \int_{\Omega_0} \boldsymbol{S} : \delta\boldsymbol{E} \, d\Omega_0
$$
这里，$\boldsymbol{S}$ 是**第二类皮奥拉-基尔霍夫 (Second Piola-Kirchhoff, PK2) 应力张量**，它与[格林-拉格朗日应变张量](@entry_id:187745) $\boldsymbol{E}$ 在能量上共轭。$\boldsymbol{S}$ 是一个定义在参考构型上的对称张量，与柯西应力 $\boldsymbol{\sigma}$ 的关系为 $\boldsymbol{S} = J \boldsymbol{F}^{-1}\boldsymbol{\sigma}\boldsymbol{F}^{-\mathsf{T}}$，其中 $J = \det(\boldsymbol{F})$。由于积分域固定，TL格式在处理固体力学问题时非常方便。

**更新拉格朗日 (Updated Lagrangian, UL) 格式**：与TL格式相反，UL格式在每个时间步或荷载步的当前构型 $\Omega_t$ 上建立和求解平衡方程。积分和求导都是相对于当前坐标 $\boldsymbol{x}$ 进行的。其[内虚功](@entry_id:172278)项为：
$$
\delta W_{\text{int}} = \int_{\Omega_t} \boldsymbol{\sigma} : \boldsymbol{d} \, d\Omega_t
$$
这里，$\boldsymbol{\sigma}$ 是**柯西 (Cauchy) [应力张量](@entry_id:148973)**（即真实应力），它与**变形率张量** $\boldsymbol{d}$（速度梯度的对称部分）在能量上共轭。由于当前构型是不断变化的，UL格式在处理大流动或涉及接触的算法时可能更具优势，但需要在每个增量步更新几何信息 [@problem_id:3601315]。

#### 物理表现：[结构屈曲](@entry_id:171177)

[几何非线性](@entry_id:169896)最经典的物理表现之一是细长结构的**[屈曲](@entry_id:162815)**（buckling）。考虑一个两端铰接的细长压杆（[欧拉-伯努利梁](@entry_id:749104)），受到轴向压力 $P$。在线性理论中，只要 $P$ 不足以使[材料屈服](@entry_id:751736)，压杆将保持直线状态。然而，当压力达到某个临界值时，即使材料仍处于弹性范围内，压杆也会突然发生侧向弯曲。

这种现象可以用[能量法](@entry_id:183021)来解释。系统的总[势能](@entry_id:748988) $\Pi$ 由两部分组成：一部分是弯曲产生的**应变能** $U$，另一部分是外力 $P$ 所做的功的负值，即**外力势能** $W$。对于横向位移为 $w(x)$ 的梁：
$$
\Pi[w] = U + W = \frac{1}{2} \int_{0}^{L} EI (w''(x))^2 \, dx - \frac{1}{2} \int_{0}^{L} P (w'(x))^2 \, dx
$$
其中，第一项是[弯曲应变能](@entry_id:203595)，与曲率的平方成正比。第二项是外力[势能](@entry_id:748988)，它来源于轴向缩短，而这个缩短量可以通过对 $(w')^2$ 积分得到，这正是[几何非线性](@entry_id:169896)的体现。

一个平衡状态是稳定的，当且仅当总[势能](@entry_id:748988)在该状态的二阶变分 $\delta^2\Pi$ 是正定的。对于压杆的直线平衡状态（$w=0$），其二阶变分与总势能表达式形式相同：
$$
\delta^2\Pi[w, w] = \int_{0}^{L} \left( EI(w''(x))^2 - P(w'(x))^2 \right) dx
$$
当 $P$ 较小时，积分项中的 $EI(w'')^2$ 起主导作用，$\delta^2\Pi > 0$，直线状态是稳定的。随着 $P$ 的增加，负的“[几何刚度](@entry_id:172820)”项 $-P(w')^2$ 的影响越来越大。当 $P$ 达到**[临界屈曲载荷](@entry_id:202664)** $P_{\text{cr}}$ 时，存在一个非平凡的位移形函数 $w(x)$ 使得 $\delta^2\Pi = 0$。这意味着系统的刚度阵（[切线刚度](@entry_id:166213)）失去了正定性，结构发生了失稳。求解这个[变分问题](@entry_id:756445)可以得到一个特征值问题 $EI w^{(4)} + P w'' = 0$，其最低的[特征值](@entry_id:154894)即为临界载荷 $P_{\text{cr}} = \frac{\pi^2 EI}{L^2}$，对应的[特征函数](@entry_id:186820) $w(x) = \sin(\frac{\pi x}{L})$ 为屈曲模态 [@problem_id:3601322]。

### [材料非线性](@entry_id:162855)：超越胡克定律

[材料非线性](@entry_id:162855)描述的是材料的[应力-应变关系](@entry_id:274093)本身是[非线性](@entry_id:637147)的，这种关系可能依赖于加载历史、加载速率或温度等因素。

#### 率无关塑性理论框架

塑性是金属等材料中一种典型的[材料非线性](@entry_id:162855)行为，其特征是存在不可恢复的永久变形。小应变率无关塑性理论的经典框架基于以下几个核心概念：

1.  **[应变分解](@entry_id:186005)**：总应变张量 $\boldsymbol{\varepsilon}$ 可以加性分解为弹性的、可恢复的部分 $\boldsymbol{\varepsilon}^{\mathrm{e}}$ 和塑性的、不可恢复的部分 $\boldsymbol{\varepsilon}^{\mathrm{p}}$：$\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{\mathrm{e}} + \boldsymbol{\varepsilon}^{\mathrm{p}}$。

2.  **弹性定律**：应力 $\boldsymbol{\sigma}$ 完全由[弹性应变](@entry_id:189634) $\boldsymbol{\varepsilon}^{\mathrm{e}}$ 决定，通常遵循胡克定律 $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}^{\mathrm{e}}$。能量储存在弹性变形中，亥姆霍兹自由能 $\psi$ 是弹性应变和内变量的函数 $\psi(\boldsymbol{\varepsilon}^{\mathrm{e}}, \alpha)$。应力可从自由能导出：$\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^{\mathrm{e}}}$。

3.  **[屈服准则](@entry_id:193897)**：材料在应力空间中存在一个弹性域。该域的边界由**[屈服函数](@entry_id:167970)** $f(\boldsymbol{\sigma}, \alpha) = 0$ 定义，其中 $\alpha$ 是一组描述材料历史（如加工硬化）的内变量。当 $f  0$ 时，材料处于弹性状态；当 $f = 0$ 时，材料可能发生塑性流动。$f > 0$ 的状态是不允许的。

4.  **[流动法则](@entry_id:177163)**：当达到屈服条件时，塑性应变率 $\dot{\boldsymbol{\varepsilon}}^{\mathrm{p}}$ 的方向由[流动法则](@entry_id:177163)确定。对于金属，通常采用**[相关联流动法则](@entry_id:163391)**，即塑性应变率的方向与屈服面在应力空间的法线方向一致：
    $$
    \dot{\boldsymbol{\varepsilon}}^{\mathrm{p}} = \lambda \frac{\partial f}{\partial \boldsymbol{\sigma}}
    $$
    其中 $\lambda \ge 0$ 是**塑性乘子**，它度量[塑性流动](@entry_id:201346)的速率。

5.  **硬化法则**：硬化法则描述了内变量 $\alpha$ 如何随塑性变形而演化，从而导致[屈服面](@entry_id:175331)的扩大（[硬化](@entry_id:177483)）或移动。例如，$\dot{\alpha} = \lambda h(\boldsymbol{\sigma}, \alpha)$。

这些关系与一组被称为**[Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)**的加载/卸载条件相结合：$f \le 0$, $\lambda \ge 0$, $\lambda f = 0$。这些条件优雅地概括了材料的行为：只有当应力状态在屈服面上时（$f=0$），才可能发生[塑性流动](@entry_id:201346)（$\lambda > 0$）。如果在屈服面上，应力状态要继续保持在[屈服面](@entry_id:175331)上（除非卸载），这要求 $\dot{f}=0$，即**一致性条件**，该条件用于确定塑性乘子 $\lambda$ 的大小 [@problem_id:3601318]。

#### 黏弹性：时间依赖的材料响应

黏弹性是另一类重要的[材料非线性](@entry_id:162855)，其特点是材料响应依赖于加载速率。例如，聚合物在快速加载时表现得更硬，在慢速加载或恒定载荷下会发生蠕变。

在有限变形框架下，一个[广义Maxwell模型](@entry_id:169862)可以用来描述这种行为。其总应力可以看作是一个处于平衡状态的弹性弹簧（描述长期响应）与若干个Maxwell单元（一个弹簧和一个黏壶[串联](@entry_id:141009)，描述松弛过程）并联的结果。此时，总的[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}$ 可以分解为平衡部分 $\boldsymbol{\tau}_{\text{eq}}$ 和代表每个Maxwell单元的非平衡部分 $\boldsymbol{A}_k$ 的和：
$$
\boldsymbol{\tau} = \boldsymbol{\tau}_{\text{eq}} + \sum_{k=1}^{n} \boldsymbol{A}_k
$$
平衡应力 $\boldsymbol{\tau}_{\text{eq}}$ 通常由一个[超弹性](@entry_id:159356)模型（如Neo-Hookean模型）描述，它是当前变形（如 $\boldsymbol{B}$ 或 $J$）的函数。非平衡应力 $\boldsymbol{A}_k$ 被视为内部[状态变量](@entry_id:138790)，它们的[演化方程](@entry_id:268137)描述了材料的松弛行为。一个[热力学](@entry_id:141121)上容许的[演化方程](@entry_id:268137)（如上随体[Maxwell模型](@entry_id:157958)）通常具有以下形式：
$$
\overset{\triangledown}{\boldsymbol{A}_k} + \frac{1}{\theta_k}\boldsymbol{A}_k = 2G_k \text{dev}(\boldsymbol{d})
$$
其中 $\overset{\triangledown}{\boldsymbol{A}_k}$ 是 $\boldsymbol{A}_k$ 的一个[客观率](@entry_id:198692)，$\theta_k$ 和 $G_k$ 分别是第 $k$ 个单元的松弛时间和剪切模量，$\boldsymbol{d}$ 是变形率张量。这个方程表明，内部应力会以松弛时间 $\theta_k$ 衰减，同时由当前的变形率驱动产生 [@problem_id:3601262]。

#### 材料失稳：软化与局部化

在某些材料中，如混凝土、岩土或某些金属，在达到峰值应力后，材料的承载能力会随着应变的增加而下降，这种现象称为**[应变软化](@entry_id:755491)**。这是一个极端的[材料非线性](@entry_id:162855)形式，它会导致**材料失稳**。

从数学上看，材料失稳与控制[方程组](@entry_id:193238)**椭圆性的丧失**有关。在准静态问题中，当增量形式的本构关系（[切线](@entry_id:268870)模量 $\mathbb{C}^{\text{alg}}$）不再满足强椭圆性条件时，就会发生失稳。强椭圆性条件要求对于任意非[零向量](@entry_id:156189) $\boldsymbol{a}$ 和 $\boldsymbol{n}$，下式恒成立：$a_i n_j \mathbb{C}^{\text{alg}}_{ijkl} a_k n_l > 0$。

一个更实用的判据是检查**[声学张量](@entry_id:200089)** $\mathbb{Q}(\boldsymbol{n})$ 的正定性，其定义为 $\mathbb{Q}_{ik}(\boldsymbol{n}) = n_j \mathbb{C}^{\text{alg}}_{ijkl} n_l$。[声学张量](@entry_id:200089)的[特征值](@entry_id:154894)与沿方向 $\boldsymbol{n}$ 传播的平面波波速的平方成正比。当某个方向 $\boldsymbol{n}$ 的[声学张量](@entry_id:200089)的最小特征值变为零或负值时，强椭圆性丧失。这意味着沿该方向的[波速](@entry_id:186208)为虚数，扰动无法传播，变形会倾向于集中在一个无限薄的带内，即**[应变局部化](@entry_id:176973)**（如剪切带）。

对于二维各向同性材料，[声学张量](@entry_id:200089)的[特征值](@entry_id:154894)不依赖于方向 $\boldsymbol{n}$，它们等于剪切模量 $\mu$ 和[平面应变](@entry_id:167046)[纵波](@entry_id:172335)模量 $\lambda+2\mu$。因此，失稳发生的条件是 $\mu \le 0$ 或 $\lambda+2\mu \le 0$。在数值计算中检测到这种情况时，需要采用**正则化**技术，例如，通过微小地增加 $\mu$ 来恢复椭圆性，以避免网格依赖和数值发散 [@problem_id:3601340]。

### 几何与[材料非线性](@entry_id:162855)的相互作用

当[大变形](@entry_id:167243)和[材料非线性](@entry_id:162855)同时存在时，二者的耦合会带来新的挑战，尤其是在如何客观地描述材料本构关系方面。

#### 率形式本构与[客观应力率](@entry_id:199282)

许多材料模型（如塑性和黏弹性）自然地以率形式给出，即应力率与[应变率](@entry_id:154778)之间存在关系。然而，在有限转动下，普通的柯西应力材料时间导数 $\dot{\boldsymbol{\sigma}}$ 并不是一个客观的量。在一个与材料一同刚性转动的观察者看来，即使材料没有变形，$\dot{\boldsymbol{\sigma}}$ 也不会为零。具体来说，在叠加了一个具有自旋 $\boldsymbol{\Omega}$ 的[刚体转动](@entry_id:191086)后，新的应力率 $\dot{\boldsymbol{\sigma}}^*$ 与旧的应力率 $\dot{\boldsymbol{\sigma}}$ 的关系为：
$$
\dot{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega}
$$
其中 $\boldsymbol{Q}$ 是转动张量。额外的项 $\boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega}$ 表明 $\dot{\boldsymbol{\sigma}}$ 不满足[张量变换法则](@entry_id:185176)，因而不是客观的 [@problem_id:3601294]。

为了在有限变形框架下使用率形式的本构，必须采用**[客观应力率](@entry_id:199282)**。[客观率](@entry_id:198692)通过从材料导数中减去由[刚体转动](@entry_id:191086)引起的部分来构造。一个常见的选择是**Jaumann率**（或称余旋率），它使用材料[自旋张量](@entry_id:187346) $\boldsymbol{W}$（[速度梯度](@entry_id:261686)的反对称部分）来修正：
$$
\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$
可以证明，Jaumann率是客观的，即 $(\overset{\triangle}{\boldsymbol{\sigma}})^* = \boldsymbol{Q}\overset{\triangle}{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}}$。

#### [伪弹性](@entry_id:159612)模型的警示：非物理[振荡](@entry_id:267781)

虽然使用[客观率](@entry_id:198692)是必要的，但这并非万无一失。一个著名的例子是基于Jaumann率的**[伪弹性](@entry_id:159612) (hypoelastic)** 模型，其[本构关系](@entry_id:186508)为 $\overset{\triangle}{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{d}$。考虑一个简单的剪切变形，[速度场](@entry_id:271461)为 $\boldsymbol{v} = (\dot{\gamma}x_2, 0, 0)$。对于这个变形，变形率 $\boldsymbol{d}$ 和自旋 $\boldsymbol{W}$ 都是常数。将[伪弹性](@entry_id:159612)定律代入Jaumann率的定义，可以得到一个关于应力分量的[常微分方程组](@entry_id:266774)。求解这个[方程组](@entry_id:193238)会发现，在持续的单向剪切下，[剪切应力](@entry_id:137139) $\sigma_{12}$ 和[正应力](@entry_id:260622) $\sigma_{11}, \sigma_{22}$ 都会随应变 $\gamma = \dot{\gamma}t$ 呈正弦或余弦[振荡](@entry_id:267781)。例如，$\sigma_{12}(t) = G \sin(\dot{\gamma}t)$。这显然是非物理的，因为真实的弹性材料在单向剪切下应力应单调增加。这个例子警示我们，仅仅保证客观性不足以构建一个物理上合理的有限变形材料模型，更根本的方法是基于[亥姆霍兹自由能](@entry_id:136442)的超弹性框架 [@problem_id:3601330]。

### [接触非线性](@entry_id:747785)：变化的边界条件

[接触非线性](@entry_id:747785)源于两个或多个物体之间相互作用时产生的边界条件的急剧变化。接触区域、接触状态（分离、滑动或粘着）以及[接触力](@entry_id:165079)都是未知的，并且随着变形的进行而改变。

#### 单边约束与[互补条件](@entry_id:747558)

最简单的接触形式是无摩擦的**单边约束 (unilateral constraint)**。考虑一个弹性体与一个刚性障碍物之间的接触。其物理行为可以用一组简单的条件来描述：
1.  **不可穿透条件**：物体不能穿透障碍物。如果用法向[间隙函数](@entry_id:164997) $g_n$ 来表示物体表面与障碍物之间的距离（$g_n \ge 0$ 表示无穿透），则该条件为 $g_n \ge 0$。
2.  **非粘着条件**：[接触力](@entry_id:165079)只能是压力，不能是拉力。如果用法向接触压力 $p_n$ 表示（$p_n \ge 0$ 表示压力），则该条件为 $p_n \ge 0$。
3.  **互补性**：这两个条件是互补的。如果存在间隙（$g_n > 0$），则[接触力](@entry_id:165079)必须为零（$p_n = 0$）。反之，如果存在接触压力（$p_n > 0$），则间隙必须为零（$g_n = 0$）。

这三个条件可以优雅地合并为一个**[互补条件](@entry_id:747558)**：
$$
g_n \ge 0, \quad p_n \ge 0, \quad g_n p_n = 0
$$
这种 "要么-要么" 的性质是接触问题的核心[非线性](@entry_id:637147)来源 [@problem_id:3601260]。

#### [接触约束](@entry_id:171598)的计算方法

将这种基于不等式的[互补条件](@entry_id:747558)纳入[有限元法](@entry_id:749389)的弱形式平衡方程中，有几种主流方法。

**精确方法**：这些方法旨在精确满足[互补条件](@entry_id:747558)。
*   **[拉格朗日乘子法](@entry_id:176596)**：将法向接触压力 $p_n$（或记为 $\lambda_n$）作为一个独立的未知场（拉格朗日乘子）引入。系统的求解变量包括位移场和这个乘子场。[弱形式](@entry_id:142897)中会增加一个约束项 $\int_{\Gamma_c} \lambda_n \delta g_n \, d\Gamma$，其中 $\delta g_n$ 是法向间隙的变分。这形成了一个[鞍点问题](@entry_id:174221)，需要特殊的求解器。
*   **[变分不等式](@entry_id:172788)**：不引入新的变量，而是将不可穿透条件 $g_n \ge 0$ 直接施加在位移场的容许空间上，使其成为一个凸集 $K$。[平衡问题](@entry_id:636409)不再是在整个空间中寻找[势能](@entry_id:748988)的驻点（[变分方程](@entry_id:635018)），而是在凸集 $K$ 上寻找[势能](@entry_id:748988)的最小值（**[变分不等式](@entry_id:172788)**）。这两种方法在数学上是等价的 [@problem_id:3601260]。

**近似方法**：这些方法通过修正模型来近似满足接触条件，通常在计算上更简单。
*   **[罚函数法](@entry_id:636090)**：这是最流行的方法之一。其思想是将[接触约束](@entry_id:171598)视为一个带有很大刚度的弹簧。在总势能中增加一个**罚能项**，例如 $\frac{1}{2}\varepsilon \langle -g_n \rangle_+^2$，其中 $\varepsilon$ 是一个大的正数，称为**罚参数**，$\langle \cdot \rangle_+$ 表示取正部。这个能量项只在发生穿透（$g_n  0$）时才被激活，并且穿透越深，能量越大。这等效于引入一个与[穿透深度](@entry_id:136478)成正比的接触压力 $p_n = \varepsilon \langle -g_n \rangle_+$。

罚参数 $\varepsilon$ 的选择是一个权衡：它必须足够大以减小穿透误差，但过大会导致[刚度矩阵](@entry_id:178659)病态，难以求解。一个好的做法是让[罚刚度](@entry_id:753321)与接触单元的物理刚度相匹配，例如，$\varepsilon \sim E/h$，其中 $E$ 是材料的弹性模量，$h$ 是网格尺寸。在这种选择下，由罚方法引入的穿透误差通常与[有限元法](@entry_id:749389)本身的[离散化误差](@entry_id:748522)在同一个量级（例如，$\mathcal{O}(h)$）[@problem_id:3601328]。