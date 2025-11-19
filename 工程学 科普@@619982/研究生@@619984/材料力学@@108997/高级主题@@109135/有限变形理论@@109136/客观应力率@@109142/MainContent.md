## 引言

在描述材料如何响应外力时，连续介质力学旨在建立普适的物理定律，即[本构方程](@article_id:299007)。对于微小变形，[应力与应变](@article_id:297825)之间的关系相对简单。然而，当材料经历大变形与大转动时，例如高速旋转的涡轮叶片或被弯折的橡胶，一个根本性的难题浮出水面：我们该如何恰当地描述“应力随时间的变化率”？一个看似合理的定义可能在旋转的视角下变得毫无意义，从而违反物理学中最基本的“客观性”原理。

本文正是为了解决这一难题。我们将揭示为何最直观的应力时间[导数](@article_id:318324)在描述旋转物体时会产生悖论，并引入“[客观应力率](@article_id:378041)”这一关键概念作为修正方案。在接下来的内容中，我们将首先深入理解[客观性原理](@article_id:356369)的内涵，以及[Jaumann率](@article_id:364795)等不同[客观率](@article_id:377475)是如何被巧妙地构造出来的。随后，我们将探讨这些理论在工程实践中的深远影响，分析不当的模型选择如何在[计算机模拟](@article_id:306827)中导致灾难性的错误预测。最后，文章将介绍更为先进的超弹性框架，展示力学理论如何通过回归基本物理原理，为复杂问题提供优雅且计算高效的解决方案。本文将带领您开启一场从理论悖论到工程应用的探索之旅，揭示隐藏在变形与旋转背后的力学之美。

## 原理与机制

在物理学中，我们最激动人心的任务之一就是寻找描述宇宙运行方式的“定律”。这些定律通常以数学方程的形式出现，将一个量的变化率与另一个量联系起来。牛顿的第二定律，$\boldsymbol{F} = m\boldsymbol{a}$，就是一个完美的例子：它告诉我们，物体的[动量变化](@article_id:352966)率（由加速度 $\boldsymbol{a}$ 体现）与施加在它上面的力 $\boldsymbol{F}$ 成正比。在[材料科学](@article_id:312640)中，我们也在寻找类似的定律，用以描述材料在受力时如何响应。我们希望有一个方程，能够告诉我们材料内部应力（一种内部作用力）的变化率与材料如何变形之间的关系。

### 观察的艺术与物理定律的[不变性](@article_id:300612)

在深入探讨之前，让我们先来思考一个看似简单却至关重要的问题：物理定律应该依赖于我们如何观察它吗？想象一下，你正站在地面上观察一个旋转的陀螺。你的朋友更大胆一些，她跳上了另一个巨大的、与陀螺同步旋转的圆形平台。你们两人都会看到陀螺在运动，但你们的描述会截然不同。你看到陀螺上的一个点在做圆周运动，而你的朋友（在旋转的参照系里）可能会看到那个点是静止的！

尽管你们的观测记录大相径庭，但你们都必须同意一件事：陀螺的运动是由相同的物理定律支配的。陀螺不会因为你的朋友决定和它一起旋转就改变它的物理行为。这个深刻的原理被称为**物质参照系无关性（Material Frame Indifference, MFI）**，或者简称**客观性（Objectivity）**。它要求我们的物理定律（特别是描述[材料行为](@article_id:321825)的[本构方程](@article_id:299007)）必须对于所有做[刚性运动](@article_id:349714)的观察者都具有相同的形式 [@problem_id:2666103]。

在数学上，两个观察者的参照系可以通过一个[刚性运动](@article_id:349714)联系起来：$\boldsymbol{x}^{\ast}(t)=\boldsymbol{c}(t)+\boldsymbol{Q}(t)\boldsymbol{x}(t)$。这里，$\boldsymbol{x}$ 和 $\boldsymbol{x}^{\ast}$ 分别是同一个物理点在两个参照系中的位置，$\boldsymbol{c}(t)$ 是一个随时间变化的平移，而 $\boldsymbol{Q}(t)$ 是一个随时间变化的旋转矩阵。这个[旋转矩阵](@article_id:300745) $\boldsymbol{Q}(t)$ 将是我们故事的核心。

### 一个看似合理的定律与一个荒谬的悖论

好了，让我们回到寻找材料定律的任务上来。一个非常自然的想法是，材料内部应力 $\boldsymbol{\sigma}$ 的变化率应该与材料的变形速率成正比。材料的变形速率可以用一个叫做**[应变率张量](@article_id:324365)（rate-of-deformation tensor）$\boldsymbol{D}$** 的量来描述。直观地说，$\boldsymbol{D}$ 衡量了材料被拉伸或压缩的快慢；如果 $\boldsymbol{D}=\boldsymbol{0}$，说明材料没有发生形变，只是在做整体的[刚性运动](@article_id:349714)（平移或旋转）[@problem_id:2905934]。

那么，最简单的“变化率”是什么呢？自然是材料时间[导数](@article_id:318324)，我们记作 $\dot{\boldsymbol{\sigma}}$。于是，我们满怀希望地写下了一个看似非常合理的[本构方程](@article_id:299007)：
$$
\dot{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}
$$
这里，$\mathbb{C}$ 是一个[四阶张量](@article_id:360724)，代表材料的弹性属性。这个方程说的是：应力的变化率正比于[应变率](@article_id:331700)。听起来很不错，对吧？

现在，让我们用一个思想实验来检验这个定律，这个实验将揭示一个惊人的悖论。想象我们有一块已经被预先拉伸的橡胶（所以它内部存在一个初始应力 $\boldsymbol{\sigma}_0$）。现在，我们不去进一步拉伸或压缩它，只是让它绕着一个轴匀速旋转 [@problem_id:2666090]。

在这个过程中，因为没有额外的拉伸或压缩，应变率张量 $\boldsymbol{D}$ 始终为零。根据我们提出的定律 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$，我们得到 $\dot{\boldsymbol{\sigma}} = \boldsymbol{0}$。这意味着，对于一个站在地面上的静止观察者来说，这块旋转橡胶中的[应力张量](@article_id:309392)应该是一个恒定的量。也就是说，如果橡胶的拉伸方向最初指向东方，那么即使橡胶旋转了，这个“拉伸方向”在实验室[坐标系](@article_id:316753)中应该永远指向东方。

但这显然是荒谬的！物理直觉告诉我们，应力是材料内部的属性，它必须**随着材料一起旋转**。如果拉伸方向开始时是沿着材料的某个内嵌的纤维方向，那么当材料旋转时，那个纤维和它所承载的应力也必须一起旋转。然而，我们的“定律”却预测应力固定在空间中，不随材料旋转。理论与（思想）实验发生了尖锐的冲突！这意味着，我们最初的假设——使用简单的材料时间[导数](@article_id:318324) $\dot{\boldsymbol{\sigma}}$——是错误的。

### 诊断问题：时间[导数](@article_id:318324)的“背叛”

为什么 $\dot{\boldsymbol{\sigma}}$ 会“背叛”我们呢？问题出在它的定义上。材料时间[导数](@article_id:318324)测量的是一个量相对于一个**固定在空间中**的[坐标系](@article_id:316753)的变化率。当物体本身在旋转时，$\dot{\boldsymbol{\sigma}}$ 会把两件事混为一谈：一部分是由于材料真实变形引起的“物理”应力变化，另一部分是由于物体旋转导致的纯粹“几何”变化。我们的定律需要的是前者，但 $\dot{\boldsymbol{\sigma}}$ 却给了我们两者的混合物。

数学再一次清晰地揭示了问题的根源。如果我们检视 $\dot{\boldsymbol{\sigma}}$ 在不同观察者参照系下的变换关系，我们会发现它并不“客观” [@problem_id:2905931]。一个表现良好的、客观的物理量（比如应力 $\boldsymbol{\sigma}$ 或[应变率](@article_id:331700) $\boldsymbol{D}$）在从一个参照系变到另一个旋转的参照系时，应该遵循一个简单的旋转法则：$\boldsymbol{T}^{\ast} = \boldsymbol{Q}\boldsymbol{T}\boldsymbol{Q}^{\mathsf{T}}$ [@problem_id:2666106]。然而，材料时间[导数](@article_id:318324)的变换法则是：
$$
\dot{\boldsymbol{\sigma}}^{\ast} = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}
$$
这里，$\boldsymbol{\Omega} = \dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}}$ 是描述观察者自身旋转快慢的“观察者[自旋张量](@article_id:366504)”。那两个额外的、看起来很麻烦的项 $\boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}$，正是导致所有问题的“罪魁祸首”。它们的存在意味着 $\dot{\boldsymbol{\sigma}}$ 的值依赖于观察者自身的旋转状态，因此它不是一个客观的物理量，不能被用来构建一个普适的物理定律 [@problem_id:2905949]。

### 巧妙的修正：与材料共舞

既然 $\dot{\boldsymbol{\sigma}}$ 掺杂了旋转的“假象”，我们能否想办法把它剔除掉呢？这正是“[客观应力率](@article_id:378041)”概念的精髓。我们的目标是定义一个**新的**应力率，它能够忽略纯粹的刚体旋转，只反映由变形引起的[真实应力](@article_id:370022)变化。换句话说，我们需要一个从“与材料一同旋转”的视角来观察应力变化的[导数](@article_id:318324)。

让我们看看如何实现这个修正。首先，我们需要一个描述材料自身局部旋转快慢的量。这个量就是**[自旋张量](@article_id:366504)（spin tensor）$\boldsymbol{W}$**，它是速度梯度 $\boldsymbol{L}$ 的反对称部分 [@problem_id:2905934]。有趣的是，[自旋张量](@article_id:366504) $\boldsymbol{W}$ 本身也**不是**客观的！它的变换规律是 $\boldsymbol{W}^{\ast} = \boldsymbol{Q}\boldsymbol{W}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}$。

请注意！那个“罪魁祸首”——观察者自旋 $\boldsymbol{\Omega}$——又出现了！$\dot{\boldsymbol{\sigma}}$ 的非客观性和 $\boldsymbol{W}$ 的非客观性源于同一个“污染源” $\boldsymbol{\Omega}$。这带来了一个绝妙的想法：我们能否用一个“被污染”的量去修正另一个“被污染”的量，让它们的“污染”部分正好相互抵消？[@problem_id:2666126]

答案是肯定的。通过将材料时间[导数](@article_id:318324) $\dot{\boldsymbol{\sigma}}$ 与由[自旋张量](@article_id:366504) $\boldsymbol{W}$ 构成的修正项组合起来，我们可以构造一个新的应力率。最著名的例子就是**[Jaumann率](@article_id:364795)**，定义为：
$$
\boldsymbol{\sigma}^{\nabla J} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$
这后面的修正项 $\boldsymbol{\sigma}\boldsymbol{W} - \boldsymbol{W}\boldsymbol{\sigma}$（一个所谓的“李括号”或“交换子”）被精确地设计出来，用于抵消在[坐标系](@article_id:316753)变换时 $\dot{\boldsymbol{\sigma}}$ 中出现的多余旋转项。经过这个修正后，人们可以证明，[Jaumann率](@article_id:364795) $\boldsymbol{\sigma}^{\nabla J}$ 是一个真正的客观量，它的变换规律就是我们所[期望](@article_id:311378)的 $\left(\boldsymbol{\sigma}^{\nabla J}\right)^{\ast} = \boldsymbol{Q}\boldsymbol{\sigma}^{\nabla J}\boldsymbol{Q}^{\mathsf{T}}$ [@problem_id:2905949]。

### 悖论的解决与定律的新生

现在，让我们带着这个新工具回到那个“旋转橡胶”的悖论中。对于纯刚体旋转，我们之前计算出 $\dot{\boldsymbol{\sigma}} = \boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}$ [@problem_id:2905958]。现在我们来计算它的[Jaumann率](@article_id:364795)：
$$
\boldsymbol{\sigma}^{\nabla J} = \dot{\boldsymbol{\sigma}} - (\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}) = (\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}) - (\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}) = \boldsymbol{0}
$$
结果为零！这正是我们所[期望](@article_id:311378)的！对于一个只旋转而不变形的物体，[Jaumann率](@article_id:364795)正确地告诉我们“没有物理上的应力变化”。它成功地“看穿”了旋转的表象，抓住了物理的实质。这意味着，像 $\boldsymbol{\sigma}^{\nabla J} = \mathbb{C}:\boldsymbol{D}$ 这样的[本构方程](@article_id:299007)现在是一个物理上和数学上都站得住脚的定律了。

### 客观性的万花筒：不止一个答案

[Jaumann率](@article_id:364795)是唯一的解决方案吗？不是的。我们看到，解决问题的关键是找到一个合适的[自旋张量](@article_id:366504)（我们称其为 $\boldsymbol{\Lambda}$），用它来“校正”材料时间[导数](@article_id:318324)。[Jaumann率](@article_id:364795)选择了材料的[自旋张量](@article_id:366504) $\boldsymbol{W}$ 作为这个校正工具。但任何满足特定变换规律的[自旋张量](@article_id:366504) $\boldsymbol{\Lambda}$ 都可以胜任这个工作 [@problem_id:2666126]。

这开启了一个充满各种可能性的“[客观率](@article_id:377475)的万花筒”：

*   **[Green-Naghdi率](@article_id:369882)**：它使用的自旋来自于[材料变形](@article_id:348581)梯度 $\boldsymbol{F}$ 的极分解（$\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$）中的旋转部分 $\boldsymbol{R}$。这好比是跟随一套内嵌于材料内部的、不会被拉伸的坐标轴进行观察。

*   **[Truesdell率](@article_id:360406)**：这是另一种形式的[客观率](@article_id:377475)，它的定义方式不同，但同样满足客观性要求。

所有这些[客观率](@article_id:377475)（Jaumann、Green-Naghdi、Truesdell等）都有一个共同的优良品质：对于纯刚体旋转，它们的值都为零 [@problem_id:2905958]。这使得它们都成为构建[本构模型](@article_id:353764)的合格候选者 [@problem_id:2905949]。

那么，我们该如何选择呢？它们在物理上是等价的吗？答案是否定的。在简单的剪切变形等更复杂的运动下，使用不同的[客观率](@article_id:377475)会得到不同的应力预测。例如，[Jaumann率](@article_id:364795)和[Green-Naghdi率](@article_id:369882)的差别，主要体现在它们如何预测应力[主方向](@article_id:339880)的旋转，而对于应力主值自身的变化率，在一些简单模型中它们的预测是相同的 [@problem_id:2666116]。而[Jaumann率](@article_id:364795)和[Truesdell率](@article_id:360406)的差别则与应变率 $\boldsymbol{D}$ 直接相关 [@problem_id:2666095]。

选择“最好”的[客观率](@article_id:377475)取决于具体的材料和变形过程，这至今仍是连续介质力学中一个引人入胜且在持续研究的领域。从一个看似简单的“如何描述变化”的问题出发，我们经历了一场从悖论到修正、再到发现一个丰富理论体系的奇妙旅程。这恰恰展示了物理学的魅力：最深刻的洞见，往往隐藏在对最基本概念的不断审视之中。