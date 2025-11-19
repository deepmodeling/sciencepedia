## 引言
在计算岩土力学及其他处理大变形问题的工程与科学领域，准确描述材料的应力演化是建立可靠数值模型的基石。当材料经历显著的旋转和变形时，一个核心的挑战随之出现：如何定义一个在物理上具有意义的应力变化率？简单地使用应力的标准时间导数会导致模型预测结果依赖于观察者的[参考系](@entry_id:169232)，从而产生旋转物体即可凭空产生应力等违背物理现实的谬论。这一根本性的知识鸿沟，即如何构建独立于观察者刚体运动的[本构关系](@entry_id:186508)，正是本文旨在解决的核心问题。

为应对此挑战，本文将系统性地引导读者深入有限变形理论的核心——[客观应力率](@entry_id:199282)。通过三个循序渐进的章节，你将全面掌握这一关键概念：

在“原理与机制”一章中，我们将奠定理论基础，从材料[坐标无关性](@entry_id:159715)原理出发，揭示为何需要[客观率](@entry_id:198692)，并详细拆解Jaumann率、[Green-Naghdi率](@entry_id:190839)等主流[客观率](@entry_id:198692)的构建机制与运动学内涵。

接着，在“应用与跨学科连接”一章，我们将理论付诸实践，探讨[客观率](@entry_id:198692)的选择如何在计算岩[土力学](@entry_id:180264)、地球物理学等领域的[弹塑性分析](@entry_id:181788)、[滑坡模拟](@entry_id:751129)和[液化](@entry_id:184829)预测中产生深远影响，并揭示不同率形式的局限性与数值伪影。

最后，“动手实践”部分提供了一系列精心设计的计算练习，旨在让你通过编程实践，亲手验证[客观性原理](@entry_id:185412)、复现非物理效应，从而将抽象的理论转化为牢固的工程直觉和计算技能。

通过本文的学习，你将不仅理解[客观应力率](@entry_id:199282)的数学形式，更能洞悉其背后的物理精髓，并有能力在未来的研究与工程实践中，做出明智的[本构模型](@entry_id:174726)选择。

## 原理与机制

在[大变形分析](@entry_id:163435)中，描述应力如何随材料变形和运动而演化是计算岩[土力学](@entry_id:180264)的一个核心挑战。简单地使用柯西应力（Cauchy stress）张量对时间的[物质导数](@entry_id:172646)（material time derivative）来构建本构关系，将导致物理上不合理的模型，因为这种导数并非客观的（objective）。也就是说，它的值依赖于观察者的[参考系](@entry_id:169232)。本章旨在深入阐述确保本构关系在任意刚体运动下保持形式不变的基本原理——材料[坐标无关性](@entry_id:159715)（Material Frame Indifference），并系统地介绍和比较为满足此原理而设计的各种[客观应力率](@entry_id:199282)（objective stress rates）的构建机制、物理含义及其在计算实践中的应用与局限。

### 材料[坐标无关性](@entry_id:159715)原理

材料[坐标无关性](@entry_id:159715)原理（Principle of Material Frame Indifference, MFI），亦称[客观性原理](@entry_id:185412)（principle of objectivity），是一条普适的物理约束，要求材料的[本构方程](@entry_id:138559)——即联系应力与变形（或变形率）的关系式——必须独立于观察者。换言之，无论观察者自身如何进行刚体运动（平移和旋转），其描述的材料物理响应应保持一致。

为了精确地表述这一原理，我们考虑两个观察者。一个在固定的“背景”[参考系](@entry_id:169232)中，另一个在相对于背景系进行时变刚体运动的[参考系](@entry_id:169232)中。在任意时刻 $t$，一个物[质点](@entry_id:186768)在背景系中的空间位置为 $\mathbf{x}$，而在运动系中的位置为 $\mathbf{x}^*$。这两个位置之间的关系可以通过一个时变的[旋转张量](@entry_id:191990) $\mathbf{Q}(t)$（满足 $\mathbf{Q}^T\mathbf{Q}=\mathbf{I}$ 和 $\det\mathbf{Q}=1$）和一个平移向量 $\mathbf{c}(t)$ 来描述：
$$
\mathbf{x}^*(t) = \mathbf{Q}(t)\mathbf{x}(t) + \mathbf{c}(t)
$$
这种变换被称为叠加刚体运动（superposed rigid-body motion）。

MFI原理要求，所有描述材料内在响应的物理量必须是客观的。对于标量，客观性意味着其值在两个[参考系](@entry_id:169232)中不变。对于矢量和张量，客观性则要求它们根据其张量阶数进行相应的[旋转变换](@entry_id:200017)。例如，柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是一个二阶[空间张量](@entry_id:185799)，其客观性要求它的变换规律如下：
$$
\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T
$$
这个变换关系可以从柯西牵引公式（Cauchy's traction formula）$\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ 推导得出。在叠加[刚体运动](@entry_id:193355)下，物理上的真实[牵引矢量](@entry_id:189429) $\mathbf{t}$ 和[单位法向量](@entry_id:178851) $\mathbf{n}$ 都会随观察者旋转，即 $\mathbf{t}^* = \mathbf{Q}\mathbf{t}$ 和 $\mathbf{n}^* = \mathbf{Q}\mathbf{n}$。因此，在运动系中，$\mathbf{t}^* = \boldsymbol{\sigma}^*\mathbf{n}^*$，即 $\mathbf{Q}\mathbf{t} = \boldsymbol{\sigma}^*(\mathbf{Q}\mathbf{n})$。将 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ 代入，得到 $\mathbf{Q}\boldsymbol{\sigma}\mathbf{n} = \boldsymbol{\sigma}^*\mathbf{Q}\mathbf{n}$。由于此式对任意[法向量](@entry_id:264185) $\mathbf{n}$ 都成立，我们便得到了 $\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$ [@problem_id:3546920]。

然而，并非所有在连续介质力学中有用的量都是客观的。一个至关重要的反例是[空间速度梯度](@entry_id:187198)张量 $\mathbf{L} = \nabla \mathbf{v}$。在叠加刚体运动下，物质点的[速度变换](@entry_id:265594)为：
$$
\mathbf{v}^* = \frac{d\mathbf{x}^*}{dt} = \dot{\mathbf{Q}}\mathbf{x} + \mathbf{Q}\mathbf{v} + \dot{\mathbf{c}}
$$
对 $\mathbf{x}^*$ 求梯度可得 $\mathbf{L}^* = \nabla_{\mathbf{x}^*} \mathbf{v}^*$。利用链式法则和 $\mathbf{x} = \mathbf{Q}^T(\mathbf{x}^* - \mathbf{c})$，我们推导出 $\mathbf{L}$ 的变换规律为：
$$
\mathbf{L}^* = \mathbf{Q}\mathbf{L}\mathbf{Q}^T + \dot{\mathbf{Q}}\mathbf{Q}^T
$$
我们定义观察者自旋（observer spin）为 $\boldsymbol{\Omega}(t) = \dot{\mathbf{Q}}(t)\mathbf{Q}^T(t)$。由于 $\mathbf{Q}\mathbf{Q}^T=\mathbf{I}$，对其求导可知 $\dot{\mathbf{Q}}\mathbf{Q}^T + \mathbf{Q}\dot{\mathbf{Q}}^T = \mathbf{0}$，这意味着 $\boldsymbol{\Omega}$ 是一个[反对称张量](@entry_id:199349)（$\boldsymbol{\Omega}^T = -\boldsymbol{\Omega}$）。因此，$\mathbf{L}$ 的变换式写作：
$$
\mathbf{L}^* = \mathbf{Q}\mathbf{L}\mathbf{Q}^T + \boldsymbol{\Omega}
$$
由于存在额外的 $\boldsymbol{\Omega}$ 项，速度梯度 $\mathbf{L}$ 及其[物质时间导数](@entry_id:190892)都不是客观张量。更重要的是，柯西应力的标准[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ 也不是客观的。对其变换关系 $\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$ 求时间导数，我们得到：
$$
\dot{\boldsymbol{\sigma}}^* = \dot{\mathbf{Q}}\boldsymbol{\sigma}\mathbf{Q}^T + \mathbf{Q}\dot{\boldsymbol{\sigma}}\mathbf{Q}^T + \mathbf{Q}\boldsymbol{\sigma}\dot{\mathbf{Q}}^T = \boldsymbol{\Omega}(\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T) + \mathbf{Q}\dot{\boldsymbol{\sigma}}\mathbf{Q}^T + (\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T)\boldsymbol{\Omega}^T = \boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega} + \mathbf{Q}\dot{\boldsymbol{\sigma}}\mathbf{Q}^T
$$
这表明 $\dot{\boldsymbol{\sigma}}$ 的变换除了标准的张量旋转外，还包含了与观察者自旋 $\boldsymbol{\Omega}$ 相关的附加项。因此，任何直接关联 $\dot{\boldsymbol{\sigma}}$ 与变形率（如 $\mathbf{D}$）的[本构方程](@entry_id:138559)，例如 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{D}$，都将违反 MFI 原理，因为方程的形式会随观察者的改变而改变。

### 构建[客观应力率](@entry_id:199282)

为了克服 $\dot{\boldsymbol{\sigma}}$ 的非客观性，我们需要构建一个在物理上更有意义的应力率，它能够正确地在叠加刚体运动下进行[张量变换](@entry_id:183453)。这个修正后的应力率被称为 **[客观应力率](@entry_id:199282)** 或 **同转（corotational）应力率**。其核心思想是，在计算应力变化率时，减去由材料局部旋转引起的应力变化部分。

一个通用的同转应力率 $\overset{\circ}{\boldsymbol{\sigma}}$ 可以定义为：
$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Xi}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Xi}
$$
其中，$\boldsymbol{\Xi}$ 是一个与材料运动相关的、由观察者选择的反对称 **[自旋张量](@entry_id:187346)**（spin tensor）。这些修正项 $\boldsymbol{\Xi}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{\Xi}$ 的作用正是为了抵消在 $\dot{\boldsymbol{\sigma}}^*$ 变换式中出现的非客观项 $\boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega}$。如果选取的[自旋张量](@entry_id:187346) $\boldsymbol{\Xi}$ 自身变换规律为 $\boldsymbol{\Xi}^* = \mathbf{Q}\boldsymbol{\Xi}\mathbf{Q}^T + \boldsymbol{\Omega}$，那么可以证明，以此定义的 $\overset{\circ}{\boldsymbol{\sigma}}$ 是一个客观张量，即满足 $\overset{\circ}{\boldsymbol{\sigma}}^* = \mathbf{Q}\overset{\circ}{\boldsymbol{\sigma}}\mathbf{Q}^T$。

问题的关键在于，如何定义这个代表材料“旋转”的[自旋张量](@entry_id:187346) $\boldsymbol{\Xi}$？不同的选择导致了不同的[客观应力率](@entry_id:199282)定义，每种定义都有其独特的[运动学](@entry_id:173318)解释和在本构模型中的不同表现。在讨论具体的[客观率](@entry_id:198692)之前，我们必须先明确定义它们所依赖的关键[运动学](@entry_id:173318)张量。

### 关键[运动学](@entry_id:173318)张量：构建模块

描述材料局部运动的主要工具是[空间速度梯度](@entry_id:187198) $\mathbf{L}$。这个张量可以唯一地分解为一个对称部分和一个反对称部分：
$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$
其中：
- **变形率张量（rate-of-deformation tensor）** $\mathbf{D}$ 是 $\mathbf{L}$ 的对称部分：
  $$
  \mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)
  $$
  $\mathbf{D}$ 描述了材料微元的拉伸和[剪切变形](@entry_id:170920)速率，它是一个客观张量。
- **[自旋张量](@entry_id:187346)（spin tensor）**或**[涡量张量](@entry_id:189621)（vorticity tensor）** $\mathbf{W}$ 是 $\mathbf{L}$ 的反对称部分：
  $$
  \mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)
  $$
  $\mathbf{W}$ 描述了材料微元的平均瞬时转动速率。它不是一个客观张量，其变换规律与 $\mathbf{L}$ 相同，即 $\mathbf{W}^* = \mathbf{Q}\mathbf{W}\mathbf{Q}^T + \boldsymbol{\Omega}$。

为了具体理解这些张量的计算，我们考虑一个同时包含均匀拉伸和简单剪切的平面应变运动[@problem_id:3546925]。该运动由以下映射描述：
$$
\mathbf{x} = \varphi(\mathbf{X},t) =
\begin{pmatrix}
a(t)[X_1 + \gamma(t)X_2] \\
a(t)X_2 \\
a(t)X_3
\end{pmatrix}
$$
其中 $a(t)$ 是时变拉伸因子，$\gamma(t)$ 是时变剪切应变。通过[运动学](@entry_id:173318)基本关系 $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$，其中 $\mathbf{F} = \partial\mathbf{x}/\partial\mathbf{X}$ 是变形梯度，我们可以推导出该运动对应的[空间速度梯度](@entry_id:187198)为：
$$
\mathbf{L} = \begin{pmatrix}
\frac{\dot{a}}{a}  \dot{\gamma}  0 \\
0  \frac{\dot{a}}{a}  0 \\
0  0  \frac{\dot{a}}{a}
\end{pmatrix}
$$
进而，变形率张量和[自旋张量](@entry_id:187346)分别为：
$$
\mathbf{D} = \begin{pmatrix}
\frac{\dot{a}}{a}  \frac{\dot{\gamma}}{2}  0 \\
\frac{\dot{\gamma}}{2}  \frac{\dot{a}}{a}  0 \\
0  0  \frac{\dot{a}}{a}
\end{pmatrix}, \quad
\mathbf{W} = \begin{pmatrix}
0  \frac{\dot{\gamma}}{2}  0 \\
-\frac{\dot{\gamma}}{2}  0  0 \\
0  0  0
\end{pmatrix}
$$
这个例子清晰地展示了如何从一个给定的运动历程中分解出驱动应力演化的变形率 $\mathbf{D}$ 和用于构建[客观率](@entry_id:198692)的自旋 $\mathbf{W}$。

### [客观率](@entry_id:198692)的选择：运动学基础与比较

有了[运动学](@entry_id:173318)张量的定义，我们现在可以介绍几种在[计算力学](@entry_id:174464)中广泛使用的[客观应力率](@entry_id:199282)。

#### Jaumann-Zaremba 率
最直接和历史上最常见的选择是使用连续介质的[自旋张量](@entry_id:187346) $\mathbf{W}$ 作为同转框架的自旋，即令 $\boldsymbol{\Xi} = \mathbf{W}$。这样定义的[客观率](@entry_id:198692)被称为 **Jaumann-Zaremba 率** 或简称 **[Jaumann 率](@entry_id:185572)** ($\overset{J}{\boldsymbol{\sigma}}$)：
$$
\overset{J}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W}
$$
[Jaumann 率](@entry_id:185572)的优点是其定义简单，直接依赖于可从速度场计算的 $\mathbf{W}$。

#### Green-Naghdi 率
另一种选择是基于变形梯度的极分解（polar decomposition）$\mathbf{F} = \mathbf{R}\mathbf{U}$。在这里，$\mathbf{U}$ 是对称的正定右[拉伸张量](@entry_id:193200)，描述了纯变形；$\mathbf{R}$ 是正交[旋转张量](@entry_id:191990)，描述了材料微元的纯刚体旋转。我们可以定义一个与这个材料旋转直接关联的自旋，称为 **极分解自旋**（polar spin）或 **Green-Naghdi 自旋** $\boldsymbol{\Omega}$：
$$
\boldsymbol{\Omega} = \dot{\mathbf{R}}\mathbf{R}^T
$$
使用这个自旋，我们得到 **Green-Naghdi 率** ($\overset{GN}{\boldsymbol{\sigma}}$)：
$$
\overset{GN}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}
$$
Green-Naghdi 率在概念上似乎更“物理”，因为它试图跟随材料纤维的真实旋转 $\mathbf{R}$。

#### [Jaumann 率](@entry_id:185572)与 Green-Naghdi 率的比较
一个关键问题是：这两个（以及其他）[客观率](@entry_id:198692)是否等价？答案是否定的。通过对 $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$ 代入极分解并进行推导，可以得到 $\mathbf{W}$ 和 $\boldsymbol{\Omega}$ 之间的精确关系[@problem_id:3546961]：
$$
\mathbf{W} = \boldsymbol{\Omega} + \mathrm{skw}\left(\mathbf{R}(\dot{\mathbf{U}}\mathbf{U}^{-1})\mathbf{R}^T\right)
$$
其中 $\mathrm{skw}(\cdot)$ 表示取[张量的反对称部分](@entry_id:193562)。这个关系式表明，连续介质自旋 $\mathbf{W}$ 与材料旋转率 $\boldsymbol{\Omega}$ 通常是不同的。它们的差值与拉伸率 $\dot{\mathbf{U}}$ 和当前拉伸状态 $\mathbf{U}$ 有关。只有在特定条件下，例如当拉伸率张量 $\dot{\mathbf{U}}$ 的主方向与[拉伸张量](@entry_id:193200) $\mathbf{U}$ 的[主方向](@entry_id:276187)始终保持一致时（即共轴演化），二者才会相等。在一般的变形路径下，$\mathbf{W} \neq \boldsymbol{\Omega}$，因此 [Jaumann 率](@entry_id:185572)和 Green-Naghdi 率给出的应力演化是不同的。

#### Truesdell 率
另一个重要的[客观率](@entry_id:198692)是 **Truesdell 率**。它与[上随体导数](@entry_id:756365)（upper-convected derivative）密切相关，通常与[Kirchhoff应力](@entry_id:751039) $\boldsymbol{\tau}=J\boldsymbol{\sigma}$（其中 $J=\det\mathbf{F}$）配对使用。其定义较为复杂，但对于与超弹性（hyperelasticity）理论建立联系至关重要，我们将在后续章节深入探讨。

### [本构模型](@entry_id:174726)及其物理后果

在岩土力学等领域，一种常见的[本构模型](@entry_id:174726)是 ** hypoelasticity（次弹性）** 模型，其一般形式为：
$$
\overset{\circ}{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{D}
$$
其中 $\mathbb{C}$ 是四阶弹性模量张量。这个模型将[客观应力率](@entry_id:199282)与变形率张量线性关联起来。然而，模型的预测结果会显著依赖于所选择的[客观率](@entry_id:198692) $\overset{\circ}{\boldsymbol{\sigma}}$。

#### 基本要求：刚体旋转试验

任何一个有效的[客观率](@entry_id:198692)，其首要的、也是最基本的检验标准是：在纯刚体旋转下，材料不应产生任何应力。对于一个纯刚体旋转，变形梯度为 $\mathbf{F}(t) = \mathbf{R}(t)$，其中 $\mathbf{R}(t)$ 是一个旋转矩阵。在这种情况下，变形率张量 $\mathbf{D}$ 恒为零。根据次弹性本构律，$\overset{\circ}{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{0} = \mathbf{0}$。这意味着[客观应力率](@entry_id:199282)必须为零。

我们可以验证，所有主流的[客观率](@entry_id:198692)都满足这个要求。例如，对于纯刚体旋转，$\mathbf{L} = \dot{\mathbf{R}}\mathbf{R}^T$，它是一个[反对称张量](@entry_id:199349)，因此 $\mathbf{W} = \mathbf{L}$。同时，根据定义 $\boldsymbol{\Omega} = \dot{\mathbf{R}}\mathbf{R}^T$，所以 $\mathbf{W}=\boldsymbol{\Omega}$。应力的实际演化是 $\boldsymbol{\sigma}(t) = \mathbf{R}(t)\boldsymbol{\sigma}(0)\mathbf{R}(t)^T$，对其求导可得 $\dot{\boldsymbol{\sigma}} = \mathbf{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{W}$。代入Jaumann率的定义：
$$
\overset{J}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W} = (\mathbf{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{W}) - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W} = \mathbf{0}
$$
同理，[Green-Naghdi率](@entry_id:190839)和[Truesdell率](@entry_id:181014)在该情况下也都为零[@problem_id:3546956]。这证实了[客观率](@entry_id:198692)成功地将物理变形（由 $\mathbf{D}$ 度量）与纯粹的旋转分离开来。

#### 病态行为：简单剪切试验

然而，通过刚体旋转试验并不能说明一个[客观率](@entry_id:198692)在所有情况下都是“好的”。一个经典的例子是简单剪切试验。考虑一个初始无应力的次弹性材料，在恒定剪切速率下进行简单剪切运动。其[运动学](@entry_id:173318)特征是变形率 $\mathbf{D}$ 和自旋 $\mathbf{W}$ 均为非零常数。

如果我们使用 [Jaumann 率](@entry_id:185572)构建本构模型 $\overset{J}{\boldsymbol{\sigma}} = 2G\mathbf{D}$（$G$ 为[剪切模量](@entry_id:167228)），通过求解该微分方程组，可以得到[剪切应力](@entry_id:137139) $\sigma_{12}$ 随剪切应变 $\gamma$ 的[演化关系](@entry_id:175708)[@problem_id:3546926] [@problem_id:3546987]：
$$
\sigma_{12}(\gamma) = G \sin(\gamma)
$$
这个结果在物理上是相当不合理的。它预测，随着剪切应变的单调增加，剪切应力会发生[振荡](@entry_id:267781)，甚至在 $\gamma > \pi/2$ 时出现[应力软化](@entry_id:176824)，这与大多数材料在单调剪切下的实验观察相悖。这种[振荡](@entry_id:267781)行为是 [Jaumann 率](@entry_id:185572)模型的一个著名缺陷，它源于 $\mathbf{W}$ 所描述的转动与材料纤维的真实转动在简单剪切中的差异。相对于小应变理论的[线性预测](@entry_id:180569) $\sigma_{12}^{\mathrm{bench}} = G\gamma$，使用 [Jaumann 率](@entry_id:185572)引入的归一化误差为：
$$
E(\gamma) = \frac{\sigma_{12}(\gamma) - \sigma_{12}^{\mathrm{bench}}(\gamma)}{\sigma_{12}^{\mathrm{bench}}(\gamma)} = \frac{\sin(\gamma)}{\gamma} - 1
$$
这个误差随着 $\gamma$ 的增大而变得显著，警示我们在[大应变](@entry_id:751152)剪切问题中必须谨慎选择[客观率](@entry_id:198692)。

#### 客观性的重要性：能量视角

如果有人质疑客观性的必要性，认为它只是数学上的繁琐要求，那么一个基于[能量守恒](@entry_id:140514)的 Gedankenexperiment（思想实验）可以提供最有力的回答。假设我们错误地使用非客观的[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ 来构建一个“能量”表达式。考虑一个初始有[主应力](@entry_id:176761) $\sigma_1 \neq \sigma_2$ 的样本，让它经历一个从 $\theta=0$到$\theta=2\pi$的完整纯刚体旋转周期。

在这个过程中，由于是纯旋转，变形率 $\mathbf{D}=\mathbf{0}$，因此真实的[机械功率](@entry_id:163535)密度 $\sigma:D$ 始终为零，总功当然也为零。然而，如果我们错误地使用一个与 $\dot{\boldsymbol{\sigma}}$ 相关的能量率表达式，例如 $\dot{w}_{\mathrm{err}} = \boldsymbol{\sigma} : \mathbb{A} : \dot{\boldsymbol{\sigma}}$（其中 $\mathbb{A}$ 是某个固定的[四阶张量](@entry_id:181350)），并对整个周期积分，我们会发现总功可能不为零[@problem_id:3546982]。例如，在特定选择的 $\mathbb{A}$ 下，可以计算出总功为：
$$
W_{\mathrm{err}} = \int_0^T \dot{w}_{\mathrm{err}}(t) dt = \pi\alpha(\sigma_1 - \sigma_2)^2
$$
这个非零的结果意味着，仅仅通过旋转物体，我们就能无中生有地创造或消耗能量，这严重违反了[热力学第一定律](@entry_id:146485)。这个悖论的根源在于 $\dot{\boldsymbol{\sigma}}$ 的非客观性。因此，客观性不是一个可有可无的数学选项，而是确保物理定律（如[能量守恒](@entry_id:140514)）在所有[参考系](@entry_id:169232)中都成立的根本要求。

### 高等议题与计算考量

除了上述基本原理和机制外，高级应用和计算实现中还需考虑更多细节。

#### 对称性保持

[角动量守恒](@entry_id:156798)要求柯西应力张量必须是对称的。一个合理的[本构模型](@entry_id:174726)应能保证，如果[初始应力](@entry_id:750652)是对称的，那么在后续的演化中它也应保持对称。对于次弹性模型 $\overset{\circ}{\boldsymbol{\sigma}} = \mathbf{S}$（其中 $\mathbf{S}$ 是对称的），我们可以考察应力张量反对称部分的演化。可以证明，如果 $\boldsymbol{\sigma}$ 在某一时刻是对称的，其反对称部分的产生率由下式决定[@problem_id:3546951]：
$$
\mathrm{skw}(\dot{\boldsymbol{\sigma}}) = \boldsymbol{\Xi}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{\Xi}
$$
因此，要使应力始终保持对称，必须满足条件 $[\boldsymbol{\Xi}, \boldsymbol{\sigma}] \equiv \boldsymbol{\Xi}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{\Xi} = \mathbf{0}$，即应力张量必须与所选的[自旋张量](@entry_id:187346)对易。对于Jaumann率，条件是 $[\mathbf{W}, \boldsymbol{\sigma}]=\mathbf{0}$；对于[Green-Naghdi率](@entry_id:190839)，则是 $[\boldsymbol{\Omega}, \boldsymbol{\sigma}]=\mathbf{0}$。在一般变形中，这个条件通常不被满足（除非应力是静水的，$\boldsymbol{\sigma}=p\mathbf{I}$），这意味着这些[客观率](@entry_id:198692)可能会人为地产生微小的[非对称应力](@entry_id:191550)。在数值计算中，通常会在每个时间步后强制将应力张量对称化。

#### 功率共轭与超弹性一致性

选择“最佳”[客观率](@entry_id:198692)的一个更深层次的准则是其与能量原理的内在联系。在[连续介质力学](@entry_id:155125)中，单位体积的[应力功率](@entry_id:182907)有两个常用定义：单位当前体积的功率 $P_v = \boldsymbol{\sigma}:\mathbf{D}$，以及单位参考体积的功率 $P_V = J(\boldsymbol{\sigma}:\mathbf{D}) = (J\boldsymbol{\sigma}):\mathbf{D}$。定义[Kirchhoff应力](@entry_id:751039) $\boldsymbol{\tau} = J\boldsymbol{\sigma}$，则 $P_V = \boldsymbol{\tau}:\mathbf{D}$。

这个关系表明，在以参考构型为基础的能量理论（如[超弹性](@entry_id:159356)）中，[Kirchhoff应力](@entry_id:751039) $\boldsymbol{\tau}$ 与变形率 $\mathbf{D}$ 是自然**功率共轭**（power-conjugate）的。一个源于参考构型中[应变能函数](@entry_id:178435) $\Psi_0$ 的[超弹性](@entry_id:159356)模型，其能量变化率 $\dot{\Psi}_0$ 必须等于 $P_V$。从这个框架出发，可以严格推导出，与参考构型中的[第二Piola-Kirchhoff应力](@entry_id:173163)率 $\dot{\mathbf{S}}$ 相对应的空间应力率，正是[Kirchhoff应力](@entry_id:751039)的[上随体导数](@entry_id:756365) $\boldsymbol{\tau}^\nabla = \dot{\boldsymbol{\tau}} - \mathbf{L}\boldsymbol{\tau} - \boldsymbol{\tau}\mathbf{L}^T$。这个率通常被称为[Kirchhoff应力](@entry_id:751039)的[Truesdell率](@entry_id:181014)。因此，对于可压缩材料，配对 $(\boldsymbol{\tau}, \boldsymbol{\tau}^\nabla)$ 来构建[本构模型](@entry_id:174726)，在能量上比配对 $(\boldsymbol{\sigma}, \boldsymbol{\sigma}^\nabla)$ 更为自然和一致[@problem_id:3546988]。后者忽略了体积变化对能量的贡献，破坏了与超弹性理论的直接联系。

#### 数值方法中的增量客观性

最后，将连续的本构理论转化为离散的[数值算法](@entry_id:752770)时，[客观性原理](@entry_id:185412)必须在每个时间增量步上得到保证，这被称为 **增量客观性**（incremental objectivity）。一个数值更新算法可以表示为：
$$
\boldsymbol{\sigma}_{n+1} = \mathcal{A}(\boldsymbol{\sigma}_n, \mathbf{F}_n, \mathbf{F}_{n+1}, \Delta t)
$$
增量客观性要求，对于任意施加在时间步 $[t_n, t_{n+1}]$ 上的刚体运动 $\mathbf{Q}(t)$，算法必须满足以下条件[@problem_id:3546950]：
$$
\mathcal{A}(\mathbf{Q}_n\boldsymbol{\sigma}_n\mathbf{Q}_n^T, \mathbf{Q}_n\mathbf{F}_n, \mathbf{Q}_{n+1}\mathbf{F}_{n+1}, \Delta t) = \mathbf{Q}_{n+1} \mathcal{A}(\boldsymbol{\sigma}_n, \mathbf{F}_n, \mathbf{F}_{n+1}, \Delta t) \mathbf{Q}_{n+1}^T
$$
简而言之，用旋转后的输入运行算法，得到的结果应等于原结果经过相应旋转后的张量。这条规则的直接推论是，对于一个纯旋转增量（即增量变形梯度 $\mathbf{F}_\Delta = \mathbf{F}_{n+1}\mathbf{F}_n^{-1}$ 本身就是一个旋转矩阵 $\mathbf{R}_\Delta$），算法必须精确地返回：
$$
\boldsymbol{\sigma}_{n+1} = \mathbf{R}_\Delta \boldsymbol{\sigma}_n \mathbf{R}_\Delta^T
$$
这是检验[应力更新算法](@entry_id:181937)是否正确实现的关键标准，确保了数值解不会因[刚体转动](@entry_id:191086)而产生虚假的应力或能量。