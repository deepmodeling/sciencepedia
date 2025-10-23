## 引言
我们如何描述一个物体的运动？虽然我们可以轻易地追踪其在空间中的路径，但当物体本身改变形状时，一个更深层次的问题就出现了。我们如何将简单的旋转或平移（即刚体运动）与导致材料拉伸和扭曲的真实变形区分开来？发展一种不被观察视角所迷惑的数学语言，是力学中的一个根本挑战。一个正确的变形描述必须独立于观察者自身的运动，这一原则确保了我们的物理定律具有普适性。

本文探讨了[刚体运动](@article_id:329499)运动学的核心概念及其在定义变形中的深远作用。在第一章“原理与机制”中，我们将为这项任务构建数学框架。我们将介绍变形梯度，发现为何某些应变度量优于其他度量，并将关键的客观性概念形式化。在这一理论基础之后，第二章“应用与跨学科联系”将展示这些原理如何不仅仅是抽象概念，而是现代科学和工程中的重要工具，从验证物理定律到构建从桥梁到分子等万物的可靠计算模拟。

## 原理与机制

在我们理解世界的旅程中，我们通常从简单地观察事物运动开始。但对物理学家而言，描述本身是不够的；我们寻求的是其潜在的原理，即支配混乱运动的优雅规则。我们如何建立一种语言来讨论固体的扭转、拉伸和翻滚？更深刻的是，我们如何能确定我们的描述捕捉到了变形的真实物理现实，而不仅仅是我们自己特定的观察视角？这正是我们故事的真正起点——寻求一种既强大又真实的运动描述。

### 运动的特性：变形梯度

让我们想象一块黏土。在使其变形之前，我们可以用其位置矢量（我们称之为 $\boldsymbol{X}$）来标记黏土中的每一个微小粒子，这处在**参考构型**中。这就像在黏土上绘制一个完美的、未变形的坐标网格。现在，我们挤压并扭转它。原来位于 $\boldsymbol{X}$ 的粒子现在处在一个新位置 $\boldsymbol{x}$，这处在**当前构型**中。这个运动是一个映射，$\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$，它告诉我们每个粒子去了哪里。

但这个映射告诉我们的是整个物体的命运。如果我们想知道局部，就在某一个点周围，发生了什么呢？考虑一个无穷小的矢量，就像在我们的参考网格上画的一个箭头，我们称之为 $d\boldsymbol{X}$。变形后，这个小箭头变成了一个新的矢量 $d\boldsymbol{x}$——很可能指向一个新的方向并具有新的长度。原始箭头和新箭头之间的关系是关键。对于一个平滑的运动，这种关系是线性的，并由一个强大而单一的实体所捕捉：**变形梯度** $\boldsymbol{F}$。

$$d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$$

变形梯度 $\boldsymbol{F} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}}$ 是一个[张量](@article_id:321604)，在我们故事中扮演主角 [@problem_id:2705809]。它是一个局部的“放大镜”，告诉我们关于材料在某一点上变化的一切信息。它包含了关于局部拉伸和[局部旋转](@article_id:353495)的所有信息。如果你想象在参考构型中有一个无穷小的材料立方体，$\boldsymbol{F}$ 就是将其转换为在当前构型中它所变成的无穷小平行六面体的算子。为避免物质相互穿透，这个映射必须是可逆的，这意味着 $\boldsymbol{F}$ 的[行列式](@article_id:303413)（称为**[雅可比行列式](@article_id:365483)** $J=\det\boldsymbol{F}$）必须为正。这个[雅可比行列式](@article_id:365483)告诉我们体积如何变化，因为 $dV = J dV_{0}$。

我们可以通过想象一个由刚性旋转和一些附加位移组合而成的运动来感受这一点。如果运动由 $\boldsymbol{x} = \boldsymbol{R}\boldsymbol{X} + \boldsymbol{u}(\boldsymbol{X})$ 给出，其中 $\boldsymbol{R}$ 是一个常数旋转矩阵，$\boldsymbol{u}(\boldsymbol{X})$ 是一个[位移场](@article_id:301917)，那么变形梯度就是 $\boldsymbol{F} = \boldsymbol{R} + \nabla\boldsymbol{u}$ [@problem_id:2681452]。这似乎暗示了旋转和变形之间存在一种清晰的加性分离。但自然界的故事要微妙一些，而且正如我们将看到的，要优雅得多。

### 刚性旋转下的应变[不变性](@article_id:300612)：设计真实的变形度量

我们所说的“真实变形”是什么意思？从物理角度看，变形是导致材料产生应力的原因。如果你拿一根钢梁并弯曲它，它会产生[内应力](@article_id:369929)。但如果你只是在空中旋转同一根钢梁而不弯曲它，则不会出现新的应力。刚体运动——纯粹的平移或旋转——本身并不构成变形。因此，任何真实的应变度量都*必须*完全“无视”刚体运动。

让我们来检验这个想法。考虑一个只经历刚性旋转的物体，其运动由 $\boldsymbol{x} = \boldsymbol{R}\boldsymbol{X}$ 描述，其中 $\boldsymbol{R}$ 是一个[旋转张量](@article_id:370993) [@problem_id:2558937]。对于这个运动，变形梯度就是 $\boldsymbol{F} = \boldsymbol{R}$。我们如何从 $\boldsymbol{F}$ 构建一个忽略这种旋转的量？

让我们不看矢量的变化，而是看其长度的平方的变化——这是一个不依赖于方向的标量。我们无穷小矢量 $d\boldsymbol{X}$ 的长度平方是 $d\boldsymbol{X} \cdot d\boldsymbol{X} = d\boldsymbol{X}^{\mathsf{T}} d\boldsymbol{X}$。变形后，其新的长度平方是 $d\boldsymbol{x} \cdot d\boldsymbol{x} = d\boldsymbol{x}^{\mathsf{T}} d\boldsymbol{x}$。代入我们的基本关系 $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$，我们得到：

$$
d\boldsymbol{x}^{\mathsf{T}} d\boldsymbol{x} = (\boldsymbol{F} d\boldsymbol{X})^{\mathsf{T}} (\boldsymbol{F} d\boldsymbol{X}) = d\boldsymbol{X}^{\mathsf{T}} (\boldsymbol{F}^{\mathsf{T}} \boldsymbol{F}) d\boldsymbol{X}
$$

看看我们发现了什么！长度平方的变化完全由中间的[张量](@article_id:321604) $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$ 所控制。这就是著名的**右 Cauchy-Green 变形[张量](@article_id:321604)**。现在，让我们看看它在纯旋转情况下告诉我们什么。当 $\boldsymbol{F} = \boldsymbol{R}$ 时，我们得到 $\boldsymbol{C} = \boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}$。由于 $\boldsymbol{R}$ 是一个[旋转张量](@article_id:370993)，它的转置是它的逆，所以 $\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R} = \boldsymbol{I}$，即单位[张量](@article_id:321604)。

这意味着对于纯旋转，$\boldsymbol{C} = \boldsymbol{I}$，新的长度平方是 $d\boldsymbol{X}^{\mathsf{T}}\boldsymbol{I} d\boldsymbol{X} = d\boldsymbol{X}^{\mathsf{T}} d\boldsymbol{X}$。长度根本没有改变！[张量](@article_id:321604) $\boldsymbol{C}$ 成功地滤除了刚性旋转，告诉我们没有发生拉伸。这是一个优美的结果。

由此，我们可以定义**Green-Lagrange [应变张量](@article_id:372284)**为 $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})$。这个[张量](@article_id:321604)直接度量长度平方的变化。对于我们的纯旋转，$\boldsymbol{E} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{I}) = \boldsymbol{0}$ [@problem_id:2558937]。我们已经找到了我们真实的应变度量——一个当且仅当局部运动是纯刚性旋转时才为零的量。

### [客观性原理](@article_id:356369)：物理学不偏不倚

我们的物理描述必须对[刚性运动](@article_id:349714)不敏感，这一思想实际上是物理学的一个深刻原理，称为**[物质标架无关性原理](@article_id:356369)**，或**客观性**。这是关于物理现实本质的论断：自然法则不能依赖于观察者的位置或旋转运动 [@problem_id:2658054]。如果我在实验室长凳上研究橡胶的特性，而你在一个旋转的旋转木马上研究*完全相同的这块橡胶*，我们必须推导出相同的材料定律。你旋转的视角不能神奇地改变橡胶的刚度。

我们可以通过一个思想实验将其形式化。假设我们有一个运动 $\boldsymbol{x}(\boldsymbol{X},t)$。第二个观察者相对于第一个观察者在旋转和平移，他将看到物[质点](@article_id:365946)在不同的位置 $\boldsymbol{x}^{\star}(t) = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}(t)$，其中 $\boldsymbol{c}(t)$ 是平移，$\boldsymbol{Q}(t)$ 是一个随时间变化的旋转 [@problem_id:2653167]。那些具有独立于观察者的物理现实的量被称为**客观的**。

我们的[运动学](@article_id:323309)[张量](@article_id:321604)在这种变换下表现如何？
- 一个标量，要成为客观的，必须是不变的：$s^{\star} = s$。
- 一个在未变形体上定义的物质（或参考）[张量](@article_id:321604)，也必须是不变的：$\boldsymbol{S}^{\star} = \boldsymbol{S}$。
- 一个在当前的、运动的标架中定义的[空间张量](@article_id:365009)，必须简单地随观察者标架旋转：$\boldsymbol{T}^{\star} = \boldsymbol{Q}\boldsymbol{T}\boldsymbol{Q}^{\mathsf{T}}$。

让我们检查一下我们的关键量 [@problem_id:2658054] [@problem_id:2705809]。
新的变形梯度变为 $\boldsymbol{F}^{\star} = \boldsymbol{Q}\boldsymbol{F}$。它不是不变的，所以 $\boldsymbol{F}$ 不是一个客观的物质[张量](@article_id:321604)。它内在地包含了关于观察者视角的信息。
但是[右 Cauchy-Green 张量](@article_id:353212)呢？
$$
\boldsymbol{C}^{\star} = (\boldsymbol{F}^{\star})^{\mathsf{T}}\boldsymbol{F}^{\star} = (\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{I}\boldsymbol{F} = \boldsymbol{C}
$$
它是不变的！$\boldsymbol{C}$（以及由此衍生的 $\boldsymbol{E}$）是一个**客观物质[张量](@article_id:321604)**。这为我们使用它作为应变度量提供了最深刻的理由。它捕捉了材料状态的物理现实，与观察者无关。这就是为什么任何物理定律，比如材料的储存能函数 $\psi$，必须只通过像 $\boldsymbol{C}$ 这样的客观组合来依赖于变形梯度 $\boldsymbol{F}$，即 $\psi(\boldsymbol{F}) = \hat{\psi}(\boldsymbol{C})$ [@problem_id:2653167]。一块材料的能量不能仅仅因为我们决定围绕它旋转而改变！

### 动态图像：率、自旋与伪应力

到目前为止，我们只看了变形的一个快照。但是动态过程，即运动的影片呢？这里我们需要讨论“率”。自然的起点是**[速度梯度](@article_id:325397)** $\boldsymbol{L} = \nabla\boldsymbol{v}$，它描述了空间中各点粒子速度的变化。这个[张量](@article_id:321604)可以清晰地分解为其对称和反对称部分：

- $\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^{\mathsf{T}})$，**变形率[张量](@article_id:321604)**，描述瞬时拉伸率。
- $\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^{\mathsf{T}})$，**[自旋张量](@article_id:366504)**，描述瞬时旋转率（[涡量](@article_id:303185)）。

现在我们必须问我们那个关键问题：这些率是客观的吗？我们应用我们叠加的[刚体运动](@article_id:329499)，发现[速度梯度](@article_id:325397)变换为 $\boldsymbol{L}^{\star} = \boldsymbol{Q}\boldsymbol{L}\boldsymbol{Q}^{\mathsf{T}} + \dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}}$ [@problem_id:2905934]。那个额外的项 $\dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}}$ 是观察者[参考系](@article_id:345789)的[角速度](@article_id:323935)！这意味着 $\boldsymbol{L}$ 不是客观的——它的值取决于观察者旋转的速度。[自旋张量](@article_id:366504) $\boldsymbol{W}$ 也是如此。

但请看变形率 $\boldsymbol{D}$ 发生了什么。因为观察者的自旋项 $\dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}}$ 是反对称的，当我们取对称部分得到 $\boldsymbol{D}^{\star}$ 时，这些来自 $\boldsymbol{L}^{\star}$ 及其转置的额外项完美地抵消了！结果是 $\boldsymbol{D}^{\star} = \boldsymbol{Q}\boldsymbol{D}\boldsymbol{Q}^{\mathsf{T}}$。变形率 $\boldsymbol{D}$ 的变换方式与一个客观[空间张量](@article_id:365009)应有的方式完全一致 [@problem_id:2658054] [@problem_id:2905934]。它是一个真实的、客观的拉伸率度量。

这不仅仅是一个数学上的奇趣；它具有至关重要的实际意义。许多先进的材料模型，特别是用于流体或经历快速过程的金属的模型，被表述为*应力变化率*与变形率之间的关系：$\stackrel{\circ}{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$。为了使这个物理定律是客观的，如果 $\boldsymbol{D}$ 是客观的，那么应力率 $\stackrel{\circ}{\boldsymbol{\sigma}}$ 也必须是客观的。

这里的重磅消息是：你在微积分中学到的普通时间[导数](@article_id:318324) $\dot{\boldsymbol{\sigma}}$ 并*不*是客观的。在 constitutive law 中使用它是产生物理谬误的根源。

让我们用一个简单的、毁灭性的例子来看看为什么会这样 [@problem_id:2609668]。想象一根已经承受一定拉力 $\sigma_{0}$ 的杆，我们只是以恒定的角速度旋转它。没有新的拉伸发生，所以变形率 $\boldsymbol{D}$ 处处为零。一个不正确的、非客观的定律，如 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$，会预测 $\dot{\boldsymbol{\sigma}} = \boldsymbol{0}$。这意味着在固定的[实验室参考系](@article_id:346288)中看到的应力张量保持不变。但这在物理上是荒谬的！杆中的拉力是一个与材料绑定的物理实体；拉力的方向*必须*随杆一起旋转。错误的定律预测应力保持指向，比如说，水平方向，而杆在其下方旋转。这就产生了一种没有物理基础的“伪应力”。这个误差的量级不小；在旋转角度为 $\theta_f$ 后，应力误差的 Frobenius 范数为 $\sqrt{2}\sigma_{0}|\sin(\theta_{f})|$，这甚至可能比实际应力还要大！

为了解决这个问题，我们必须使用一个**[客观应力率](@article_id:378041)**。这些是巧妙构造的[导数](@article_id:318324)（如**Jaumann 率**或**Green-Naghdi 率**），它们实质上是在一个与材料共旋的[参考系](@article_id:345789)中计算时间[导数](@article_id:318324)，从而移除了由纯自旋引起的非客观部分 [@problem_id:2607442]。在我们那个 $\boldsymbol{D}=\boldsymbol{0}$ 的旋转杆例子中，任何有效的[客观应力率](@article_id:378041)都会正确地得出零，这表明没有由变形产生新的应力 [@problem_id:2666113]。

在工程软件（如有限元法）中不使用[客观率](@article_id:377475)将是灾难性的。当一个部件经受大旋转时，即使实际应变很小，程序也会预测应力从无到有地出现。想象一下，用一个连旋转的基本物理都搞错的程序来设计一个旋转的涡轮叶片或汽车悬架部件 [@problem_id:2607442]。

因此，我们从一个如何描述运动的简单问题开始的旅程，一直被一个深刻的对称性原理——客观性所引导。这个原理迫使我们发现了真实的、与观察者无关的应变（$\boldsymbol{C}$、$\boldsymbol{E}$）和应变率（$\boldsymbol{D}$）的度量，并揭示了以尊重物理定律基本统一性的方式描述变化是何等微妙而又至关重要。