## 引言
在连续介质力学领域，最基本的任务之一是描述材料在变形时其内部应力状态如何演变。尽管这看似直接，但当材料在拉伸或压缩之外还经历大转动时，一个深刻的挑战便出现了。我们如何才能建立普适的、并且不依赖于我们观察者自身在空间中如何旋转的应力物理定律？

本文所要解决的核心问题是，简单直观的应力张量时间[导数](@article_id:318324)存在根本性缺陷。它将真实的材料响应与由刚体旋转引起的虚假效应混合在一起，从而导致所建立的定律不具有客观性。为解决此问题，人们提出了**[客观应力率](@article_id:378041)**的概念——这是一种“更智能”的[导数](@article_id:318324)，它提供了一种纯净的、无旋转影响的度量，用以衡量应力在材料自身[参考系](@article_id:345789)中的真实变化。

本文将引导您深入理解这一基本概念。在第一章**原理与机制**中，我们将探讨客观性的理论基础，通过类比来理解为何朴素的应力率会失效，并考察不同[客观率](@article_id:377475)（如 Jaumann 率和 Truesdell 率）的构造及其后果。随后，在**应用与跨学科联系**一章中，我们将看到这些理论思想如何在计算机模拟、[结构工程](@article_id:312686)乃至[复杂流体](@article_id:377207)研究中产生至关重要的现实影响。

## 原理与机制

想象一下，您正在尝试描述风。您有一个风向标，它是一只立于尖塔之上的华丽金鸡。风吹来时，金鸡随之转动。作为一名勤奋的科学家，您记下指针改变方向的速率。但这时，一个淘气的朋友走过来，开始旋转整个尖塔。现在，指针改变方向的速度快多了！如果您天真地记下这个新的、更快的速率，您就会错误地断定风发生了巨大变化。您的测量结果被仪器的旋转所污染。要找出风的*真实*变化，您必须足够聪明，从您的测量值中减去尖塔的旋转。

这正是我们在连续介质力学中描述材料应力变化时所面临的困境。简单的应力材料时间[导数](@article_id:318324) $\dot{\boldsymbol{\sigma}}$ 就像对旋转金鸡的朴素测量。它既看到了因材料实际被挤压和拉伸（变形）而产生的应力变化，也看到了仅仅因为材料本身在空间中旋转而发生的[应力分量](@article_id:373838)的“变化”。然而，一条物理定律不应依赖于我们决定让实验室旋转多快。它必须独立于观察者，这一原则我们称之为**材料[坐标系](@article_id:316753)无关性**或**客观性**。我们朴素的率 $\dot{\boldsymbol{\sigma}}$ 在这项检验中彻底失败了 [@problem_id:2911179] [@problem_id:2905949]。

### 旋转指针问题：将旋转与变形分离

让我们来看看这种“污染”为何会发生。假设一个[参考系](@article_id:345789)中的观察者看到的[应力张量](@article_id:309392)为 $\boldsymbol{\sigma}$。第二个观察者的[参考系](@article_id:345789)相对于第一个[参考系](@article_id:345789)以旋转 $\boldsymbol{Q}(t)$ 运动，他将看到一个不同的[应力张量](@article_id:309392) $\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}$。这只是[旋转坐标系](@article_id:349521)时[张量](@article_id:321604)分量变化的标准法则。

当我们问应力的*变化率*如何变化时，问题就出现了。利用[微分](@article_id:319122)的乘法法则，第二个观察者看到的变化率为：
$$ \dot{\boldsymbol{\sigma}}^* = \dot{\boldsymbol{Q}}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{Q}\boldsymbol{\sigma}\dot{\boldsymbol{Q}}^{\mathsf{T}} $$

如果我们将观察者[参考系](@article_id:345789)的自旋定义为[反对称张量](@article_id:370125) $\boldsymbol{\Omega} = \dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}}$，经过少量代数运算可以得到：
$$ \dot{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega} $$

瞧！变换后的变化率 $\dot{\boldsymbol{\sigma}}^*$ 并不仅仅是原始变化率的旋转版本 $\boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}}$。它多了两个额外的项 $\boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega}$，这两项依赖于观察者的自旋 $\boldsymbol{\Omega}$。这就是“旋转金鸡”问题的数学标记。像 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$（其中 $\mathbb{C}$ 是[弹性张量](@article_id:349909)，$\boldsymbol{D}$ 是变形率）这样的本构律不可能是自然界的基本定律，因为它的形式本身就依赖于观察者 [@problem_id:2691194]。

### 打造“客观”观察者：同转思想

我们该如何修正这个问题？我们必须发明一种“更智能”的应力率，一种清除了这些旋转效应的应力率。我们需要定义一种新的[导数](@article_id:318324)，我们称之为 $\stackrel{\circ}{\boldsymbol{\sigma}}$，它必须是真正**客观的**，这意味着它应该像一个真正的[张量](@article_id:321604)那样进行干净利落的变换：$\stackrel{\circ}{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\stackrel{\circ}{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}}$。

最直观的方法是在一个*随*材料一同旋转的[坐标系](@article_id:316753)中测量应力率。这就是**同转率**（corotational rate）的精髓。我们取朴素的应力率 $\dot{\boldsymbol{\sigma}}$，并加上一些修正项，这些修正项被设计用来精确抵消虚假的旋转部分。其一般形式如下：
$$ \stackrel{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\omega}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\omega} $$
此处，$\boldsymbol{\omega}$ 是一个精心选择的[反对称张量](@article_id:370125)，代表了我们对材料自旋速率的最佳猜测。

一个非常常见且自然的选择是使用[自旋张量](@article_id:366504) $\boldsymbol{W}$，它就是速度梯度 $\boldsymbol{L}$ 的反对称部分。这便催生了著名的 **Zaremba-Jaumann 率**（或简称 **Jaumann 率**）：
$$ \stackrel{\nabla}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W} $$
根据其构造，这个新的率是客观的。一个检验其有效性的绝佳测试是考虑一个只进行纯刚体旋转而没有任何变形的物体。在这种情况下，没有拉伸或挤压，因此 $\boldsymbol{D} = \mathbf{0}$。从物理上我们预期，“真实”的应力变化率应为零。对于纯刚体旋转，事实证明 $\dot{\boldsymbol{\sigma}} = \boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}$。将此代入 Jaumann 率的定义，得到 $\stackrel{\nabla}{\boldsymbol{\sigma}} = (\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}) - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W} = \mathbf{0}$。它完美地工作了！我们更智能的率正确地报告出，在材料自身的同转[坐标系](@article_id:316753)中，应力没有发生任何有意义的变化 [@problem_id:2911179]。这使得我们能够建立客观的本构律：$\stackrel{\nabla}{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$。

### 各种各样的率：是否存在唯一“真实”的定义？

但等等。[自旋张量](@article_id:366504) $\boldsymbol{W}$ 是 $\boldsymbol{\omega}$ 的唯一可能选择吗？当然不是！我们打开了一个充满可能性的潘多拉魔盒。物理学家和工程师们定义了五花八门的[客观率](@article_id:377475)，每一种都基于对材料自旋的不同定义。

例如，**Green-Naghdi 率** 使用了变形梯度[极分解](@article_id:375742)（$\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$）中[旋转张量](@article_id:370993) $\boldsymbol{R}$ 的自旋，它代表了材料“纤维”本身的旋转。另一个重要选择是 **Truesdell 率**，它不严格属于同转率，但它是通过考虑未变形参考构形中应力的变化率并将其映射到当前构形推导出来的。它的形式更为复杂：$\overset{\mathrm{T}}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^{\mathsf{T}} + (\text{tr}\boldsymbol{D})\boldsymbol{\sigma}$ [@problem_id:2872325]。

所有这些率（以及其他许多率！）都完全是客观的。它们都能正确处理叠加的[刚体运动](@article_id:329499)。但它们并不相同。如果我们将材料置于简[单剪切](@article_id:359902)之下，[自旋张量](@article_id:366504) $\boldsymbol{W}$ 与 Green-Naghdi 率中使用的材料纤维自旋 $\boldsymbol{\Omega}$ 是不同的 [@problem_id:2610336]。这就引出了一个引人入胜且至关重要的问题：如果我们使用不同的[客观率](@article_id:377475)来构建[本构模型](@article_id:353764)，我们会得到不同的物理预测吗？

### [振荡](@article_id:331484)应力的奇特案例

答案是响亮的“是”。[客观率](@article_id:377475)的选择不仅仅是数学上的细微差别，它具有深远的物理后果。为了说明这一点，让我们考虑一个著名的思想实验：一个弹性块承受大的、连续的简[单剪切](@article_id:359902)，就像一副扑克牌从顶部被推动一样 [@problem_id:2905969]。

我们使用一个简单的基于率的[本构模型](@article_id:353764)，称为**次弹性**（hypoelastic）模型，该模型表明[客观应力率](@article_id:378041)与变形率成正比：$\stackrel{\circ}{\boldsymbol{\sigma}} = 2G\,\boldsymbol{D}$，其中 $G$ 是剪切模量。

如果我们使用 **Truesdell 率**，我们会发现剪应力 $\sigma_{12}$ 随剪切量 $\gamma$ 线性增长：$\sigma_{12}^{T}(\gamma) = G\gamma$。这似乎是合理的：剪切越大，应力越大。

但如果我们使用 **Jaumann 率**，就会发生完全奇异的事情。[剪应力](@article_id:297590)并不会无限增长，而是会[振荡](@article_id:331484)：$\sigma_{12}^{J}(\gamma) = G\sin(\gamma)$！该模型预测，当您持续剪切材料时，应力会上升，然后下降，接着变为负值，如此循环。这非常反直觉，并且与大多数真实材料在大剪切下的行为不符。两种预测之间的差异 $\Delta \sigma_{12}(\gamma) = G(\gamma - \sin(\gamma))$ 随着剪切量的增大而变得巨大 [@problem_id:2905969]。

这个结果是一个警示信号。它告诉我们，这些简单的次弹性模型虽然是客观的，但并未捕捉到弹性的全貌。使用 Jaumann 率构建的模型表现出一种奇怪的**[路径依赖性](@article_id:365518)**。如果您将其剪切 $2\pi$ 的量，然后再反向剪切回到起点，最终应力为零，但您所做的功却不为零。您在一条闭合回路上莫名其妙地产生或损失了能量，而一个真正的弹性材料绝不应该出现这种情况 [@problem_id:2647787]。

### 更深层的联系：能量、[势函数](@article_id:332364)与魔法山

这把我们引向了最深邃的思想。描述弹性行为的黄金标准是**超弹性**。[超弹性材料](@article_id:369306)是指其应力状态可由一个**储能[势函数](@article_id:332364)** $\psi$ 导出的材料，该函数仅依赖于当前的变形状态。把它想象成一个完美的弹簧，其势能为 $\frac{1}{2}kx^2$。力是势的[导数](@article_id:318324)，$F = kx$，它只取决于当前的位置 $x$，而与如何到达该位置无关。从 $x_1$ 移动到 $x_2$ 再回到 $x_1$ 所做的功恒为零。这是一个[保守系统](@article_id:323146)。

变形过程所做的功可以被想象成在某个地形上的旅程。对于[超弹性材料](@article_id:369306)，这个地形就像真实世界中受重力作用的山脉。从一点爬到另一点所做的功只取决于高度的变化（势能），而与所走的具体路径无关。

然而，使用 Jaumann 率的次弹性模型就像一座“魔法山”。您可以沿一条闭合回路行走并回到起点，却发现自己获得或失去了能量。所做的功是路径依赖的。在数学上，我们称“[应力功率](@article_id:362231)一[范式](@article_id:329204)非恰当（not exact）” [@problem_id:2872325]。这意味着对于一般的次弹性模型，不存在一个底层的[储能函数](@article_id:353935) $\psi$。这就是为什么基于 Jaumann 率的模型被称为*次*弹性（*hypo*elastic，“次等”弹性），而非*超*弹性（*hyper*elastic，真正的弹性）。

是否存在既是次弹性又是超弹性的模型？是的，但仅在非常特殊的情况下。例如，使用一种称为“对数率”的特定率的模型，在数学上等价于一个其能量是对数（或 Hencky）应变的函数的[超弹性](@article_id:319760)模型 [@problem_id:2647787]。

这给了我们一个关键的洞见。如果一种材料是真正的弹性体，我们根本就不应该使用基于率的模型。我们应该定义一个[储能函数](@article_id:353935)，例如，定义为[右 Cauchy-Green 张量](@article_id:353212) $W(\boldsymbol{C})$ 的函数。这种**超弹性**中使用的方法从一开始就将客观性内建其中，因为[张量](@article_id:321604) $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$ 自动对叠加的旋转保持不变。由于应力是直接从当前变形计算得出，而不是通过对应力率进行积分，整个[客观应力率](@article_id:378041)的问题就变得没有必要了 [@problem_id:2567310]。[客观率](@article_id:377475)是用于*非弹性*世界的工具——例如塑性和[粘塑性](@article_id:344741)——在这些领域，材料的状态本质上依赖于所经历的路径。

### 何时可以安全地保持“天真”：来自无穷小山丘的视角

在讨论了这么多之后，您可能会想：如果朴素的率 $\dot{\boldsymbol{\sigma}}$ 如此错误，为什么每本入门工程教科书都在使用它？答案在于一个优美的量级分析 [@problem_id:2673815]。

回想一下，朴素的率被一个形如 $\boldsymbol{\omega}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{\omega}$ 的虚假旋转项所污染。让我们比较一下这个项的大小与来自物理应变的“真实”应力率的大小。

在**[无穷小应变](@article_id:375995)范围**内，所有应变和旋转都非常小（比如，量级为 $\epsilon \ll 1$），此时应力也很小（$\|\boldsymbol{\sigma}\| \sim \epsilon$），自旋速率也很小（$\|\boldsymbol{\omega}\| \sim \dot{\epsilon}$）。因此，虚假的旋转率的量级约为 $\sim \dot{\epsilon} \cdot \epsilon$。而由应变产生的物理率的量级约为 $\sim \dot{\epsilon}$。虚假项与物理项之比的量级为 $\epsilon$。由于 $\epsilon$ 非常小，旋转误差是一个可以忽略不计的高阶项！对于小变形，我们朴素的率是真实[客观率](@article_id:377475)的一个完美近似。

然而，在**有限应变范围**内，即使应变很小，旋转也可能很大。自旋速率 $\|\boldsymbol{\omega}\|$ 的量级可以为 1。现在，虚假的旋转率的量级约为 $\sim 1 \cdot \epsilon = \epsilon$。这与物理应力率的量级相同！误差不再可以忽略；它成了一个主导效应。

这是整个谜题的最后一块拼图。对于一根轻微弯曲的梁或一座承受交通荷载的桥梁，旋转是微小的，我们可以安全地使用简化的、应力率之间区别消失的小应变理论。但对于一个旋转的汽车轮胎、一块被冲压成复杂形状的金属板，或高分子聚合物的[湍流](@article_id:318989)，旋转是巨大的。在这些世界里，[客观应力率](@article_id:378041)的概念不是学术上的好奇心——它是编写任何有意义的物理定律的必要关键。