## 引言
在连续介质力学中，如何精确描述一个物体在经历复杂运动和变形时其内部物理量（如应力）的变化率，是一个根本性的问题。想象一片在[湍流](@article_id:318989)中翻滚的叶子，它既在伸展和弯曲，又在平移和旋转。如果我们使用的“变化率”无法区分真实的内在变形与外部的刚体旋转，那么我们建立的任何材料本构关系——描述应力如何响应应变的物理定律——都将是不可靠的，因为它会因观察者的运动状态而异。这种对观察者无关性的追求，即[客观性原理](@article_id:356369)，是构建可靠物理模型的基石。

本文旨在解决这一难题。我们将揭示为何最直观的[物质时间导数](@article_id:369934)在旋转参照系下会失效，[并系](@article_id:342721)统地探索如何修正它或用更根本的几何概念来取代它。通过接下来的章节，我们将奠定[客观性原理](@article_id:356369)的基础，并介绍共旋[导数](@article_id:318324)（如[Jaumann率](@article_id:364795)）和共移[导数](@article_id:318324)（如[Truesdell率](@article_id:360406)）这两种核心思想。我们还将看到这些理论工具如何在[流变学](@article_id:299119)、塑性力学和计算模拟等领域中发挥关键作用，并讨论不同[客观率](@article_id:377475)选择所带来的实际后果。

## 原理与机制

想象一下，你正试图描述一片在龙卷风中翻滚的叶子的形变。这片叶子不仅在伸展、弯曲甚至撕裂——这是它“真正”的内在变化——它同时还在空间中高速移动和旋转。我们如何才能从这团杂乱的运动中，精确地分离出那部分“真正”的形变速率呢？如果我们连如何测量一个量的“真实”变化率都搞不清楚，那物理学的大厦又将建立在怎样的沙滩之上？

这正是[连续介质力学](@article_id:315536)中一个极其深刻而优美的问题的核心。我们想要建立描述材料响应的本构关系，例如应力如何随应变而变化。这就需要我们计算应力这样的物理量的时间变化率。但问题是，我们测量的对象本身就在一个流动的、旋转的介质中。一个静止的观察者看到的，将是物体平动、转动和本征形变混合在一起的复杂景象。我们的任务，便是成为一名足够聪明的物理学家，设计出一把能滤掉所有“虚假”运动伪影的手术刀，直抵变化的本质。

### [客观性原理](@article_id:356369)：为所有观察者制定的规则

在寻找这把手术刀之前，我们必须先定下一条基本的游戏规则。物理学家称之为**物质框架无关性原理 (Principle of Material Frame-Indifference)**，或简称为**[客观性原理](@article_id:356369) (Principle of Objectivity)**。

这个原理的立意非常简单：物理定律和材料的本构行为不应依赖于观察者。想象有两个观察者：一位静静地站在地面上，另一位则在一个旋转的旋转木马上。对于他们来说，描述空间位置的坐标是不同的。如果地面观察者看到一个点在位置 $\boldsymbol{x}$，那么旋转木马上的观察者会看到它在另一个位置 $\boldsymbol{x}^\ast(t) = \boldsymbol{Q}(t)\boldsymbol{x}(t) + \boldsymbol{c}(t)$，其中 $\boldsymbol{Q}(t)$ 是一个旋转矩阵，描述了旋转木马的姿态，而 $\boldsymbol{c}(t)$ 则是其中心的平移。

尽管他们的观测视角不同，但他们测量的物理实在——比如材料内部的应力，它代表了原子间的真实作用力——必须是同一回事。它不能因为你的头晕目眩而改变。

那么，像应力这样的[张量](@article_id:321604)，在不同的观察者看来，其分量应该如何换算呢？一个矢量（比如力）会通过旋转矩阵进行变换：$\boldsymbol{f}^\ast = \boldsymbol{Q}\boldsymbol{f}$。那么一个二阶张量（比如[应力张量](@article_id:309392) $\boldsymbol{\sigma}$）呢？它是一个作用于矢量以产生另一个矢量的线性算子。为了确保像功率（$\boldsymbol{f} \cdot \boldsymbol{v}$）或[应力功率](@article_id:362231)（$\boldsymbol{\sigma}:\boldsymbol{D}$）这样的标量物理量在所有观察者看来都一样，我们可以推断出二阶[空间张量](@article_id:365009)，如[柯西应力](@article_id:348185) $\boldsymbol{\sigma}$，必须遵循如下的变换法则 [@problem_id:2666493]：
$$
\boldsymbol{T}^\ast(\boldsymbol{x}^\ast, t) = \boldsymbol{Q}(t) \boldsymbol{T}(\boldsymbol{x}, t) \boldsymbol{Q}^T(t)
$$
这个简单的公式是我们的基石。任何一个我们想要认真对待的[空间张量](@article_id:365009)，都必须遵守这个变换规则。

现在，我们寻找的“客观”时间变化率 $\mathcal{D}[\boldsymbol{T}]$ 也就有了一个明确的目标：它计算出的结果本身也必须是一个客观的[张量](@article_id:321604)。也就是说，它必须满足 [@problem_id:2666493]：
$$
\mathcal{D}[\boldsymbol{T}]^\ast = \boldsymbol{Q} \mathcal{D}[\boldsymbol{T}] \boldsymbol{Q}^T
$$
这个条件确保了我们所说的“变化率”本身也是一种不依赖于观察者旋转状态的物理实在。

### 最直接的尝试及其失败

最简单的时间[导数](@article_id:318324)是什么？当然是跟随一个物质点一起运动时所看到的变化率，我们称之为**[物质导数](@article_id:369934)**，记作 $\dot{\boldsymbol{T}}$。它已经考虑了物[质点](@article_id:365946)的平移，但它是否正确处理了旋转呢？

让我们来看一个具体的思想实验 [@problem_id:658176]。想象一种非常简单的流体[稳态](@article_id:326048)[剪切流](@article_id:330521)动，在固定的实验室[坐标系](@article_id:316753)中，速度场不随时间变化，因此应变率张量 $\boldsymbol{D}$ 也是一个常数。对于实验室里的观察者来说，既然一切都是[稳态](@article_id:326048)的，那么[应变率张量](@article_id:324365)的时间变化率自然是零，即 $\dot{\boldsymbol{D}} = \mathbf{0}$。

现在，让我们的朋友坐上一个绕着$z$轴匀速旋转的转盘来观察这个流动。对他而言，即使流场本身是[稳态](@article_id:326048)的，他也会看到[应变率张量](@article_id:324365)的各个分量在嗡嗡地变化，这仅仅是因为他的坐标轴在不停地旋转！

我们可以通过直接计算来验证这一点。对客观[张量](@article_id:321604)的变换法则 $ \boldsymbol{T}^\ast = \boldsymbol{Q} \boldsymbol{T} \boldsymbol{Q}^T $ 两边求[物质导数](@article_id:369934)，利用乘法法则，我们会得到一个令人不安的结果 [@problem_id:2666493]：
$$
\dot{\boldsymbol{T}}^\ast = \boldsymbol{Q} \dot{\boldsymbol{T}} \boldsymbol{Q}^T + \boldsymbol{\Omega} \boldsymbol{T}^\ast - \boldsymbol{T}^\ast \boldsymbol{\Omega}
$$
其中 $\boldsymbol{\Omega} := \dot{\boldsymbol{Q}}\boldsymbol{Q}^T$ 是描述观察者参照系旋转快慢的[自旋张量](@article_id:366504)。

看！物质导数 $\dot{\boldsymbol{T}}$ 并不客观！它的变换不仅仅是简单的 $ \boldsymbol{Q}(\cdot)\boldsymbol{Q}^T $，还多了两个讨厌的附加项 $\boldsymbol{\Omega} \boldsymbol{T}^\ast - \boldsymbol{T}^\ast \boldsymbol{\Omega}$。这些附加项，就是旋转木马上的朋友看到的“虚假”变化，是纯粹由参照系旋转产生的幻影。我们天真的第一次尝试失败了，但这次失败也为我们指明了前进的方向。

### “共旋”思想：与材料共舞

失败乃成功之母。上面公式中的“错误项” $\boldsymbol{\Omega} \boldsymbol{T}^\ast - \boldsymbol{T}^\ast \boldsymbol{\Omega}$ 正是修正我们[导数](@article_id:318324)的关键。既然物质导数包含了虚假的旋转效应，那我们何不把它减掉呢？

这就引出了**共旋[导数](@article_id:318324) (Corotational Rate)** 的核心思想。让我们定义一种新的[导数](@article_id:318324) $\overset{\diamond}{\boldsymbol{T}}$，它等于[物质导数](@article_id:369934)减去那个虚假的旋转部分 [@problem_id:2666477]：
$$
\overset{\diamond}{\boldsymbol{T}} = \dot{\boldsymbol{T}} - (\boldsymbol{\Omega} \boldsymbol{T} - \boldsymbol{T} \boldsymbol{\Omega}) = \dot{\boldsymbol{T}} - \boldsymbol{\Omega} \boldsymbol{T} + \boldsymbol{T} \boldsymbol{\Omega}
$$
这里的 $\boldsymbol{\Omega}$ 是一个我们选择的、用以描述材料“如何旋转”的[自旋张量](@article_id:366504)。

这个定义具有绝妙的几何意义 [@problem_id:2666477]。它代表了一个“附着”在材料上，并以自旋 $\boldsymbol{\Omega}$ 同步旋转的观察者所测得的[张量](@article_id:321604)变化率。想象一下，如果一个[张量](@article_id:321604)本身没有任何内在变化，只是随着材料在做刚性旋转，那么它的[物质导数](@article_id:369934)恰好是 $\dot{\boldsymbol{T}} = \boldsymbol{\Omega}\boldsymbol{T} - \boldsymbol{T}\boldsymbol{\Omega}$。在这种情况下，它的共旋[导数](@article_id:318324) $\overset{\diamond}{\boldsymbol{T}}$ 就精确地等于零！我们的新[导数](@article_id:318324)成功地“看穿”了刚体旋转的伪装，报告说“没有本质变化发生”。这正是我们想要的！

为了让这个共旋[导数](@article_id:318324)成为一个真正客观的[导数](@article_id:318324)，我们选择的[自旋张量](@article_id:366504) $\boldsymbol{\Omega}$ 本身也必须满足一个特定的变换法则：当观察者改变时，它必须变换为 $\boldsymbol{\Omega}^\ast = \boldsymbol{Q}\boldsymbol{\Omega}\boldsymbol{Q}^T + \dot{\boldsymbol{Q}}\boldsymbol{Q}^T$ [@problem_id:2666477]。这个条件保证了我们减去的“旋转效应”不多不少，正好能抵消观察者变换带来的虚假效应。

现在，问题变成了：我们应该选择哪个 $\boldsymbol{\Omega}$ 来代表材料的旋转呢？对这个问题的不同回答，便催生了客观[导数](@article_id:318324)这个“动物园”里的各种奇异“物种”。

### 自旋的动物园：不同的旋转方式

1.  **Jaumann 率**: 最直接的想法是，材料的旋转就应该是速度梯度 $\boldsymbol{L} = \nabla\boldsymbol{v}$ 的反对称部分，即[涡量张量](@article_id:368705) $\boldsymbol{W}$。它描述了物质微元自身的瞬时旋转角速度。将 $\boldsymbol{\Omega} = \boldsymbol{W}$ 代入共旋[导数](@article_id:318324)的公式，我们便得到了著名的 **Jaumann 率**。这好比是让我们的测量[坐标系](@article_id:316753)与材料中的一粒微尘同步旋转 [@problem_id:2666477]。

2.  **Green-Naghdi 率**: 一个更深刻的想法来自于对变形本身的分解。任何变形梯度 $\boldsymbol{F}$ 都可以唯一地分解为一个纯拉伸（由对称张量 $\boldsymbol{U}$ 描述）和一个纯刚体旋转（由[旋转张量](@article_id:370993) $\boldsymbol{R}$ 描述），即 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$（这被称为[极分解](@article_id:375742)）。或许，我们应该跟随这个代表了材料“姿态”的宏观旋转 $\boldsymbol{R}$？取 $\boldsymbol{\Omega}_{GN}=\dot{\boldsymbol{R}}\boldsymbol{R}^T$ 作为我们的自旋，就得到了 **Green-Naghdi 率** [@problem_id:2666476]。这相当于在一个与材料整体方向保持一致的框架内测量变化。

这两种自旋——微元的自旋 $\boldsymbol{W}$ 和材料姿态的自旋 $\boldsymbol{\Omega}_{GN}$——通常并不相同。它们仅在一种特殊情况下才相等：当材料的[主拉伸](@article_id:373569)方向在变形过程中保持不变时 [@problem_id:2666494]。例如，对于一个均匀的球形膨胀，所有方向都是[主方向](@article_id:339880)，且不发生旋转，此时两者相等。但在像剪切这样的变形中，[主拉伸](@article_id:373569)方向会不断旋转，这两种自旋就会分道扬镳。这微妙的差异告诉我们，定义材料的“旋转”并非只有一种方式。

### 另一种哲学：共移[导数](@article_id:318324)与Lie导数

除了通过“减去旋转”来修正物质导数，还有一种更根本、更优雅的哲学。那就是构造一种“天生就客观”的[导数](@article_id:318324)。这引领我们走向**共移[导数](@article_id:318324) (Convected Derivative)** 和一个在几何学中至高无上的概念——**Lie [导数](@article_id:318324)**。

Lie [导数](@article_id:318324)，记作 $\mathcal{L}_{\boldsymbol{v}}\boldsymbol{T}$，是描述一个张量场 $\boldsymbol{T}$ 沿着一个[矢量场](@article_id:322515)（在这里是[速度场](@article_id:335158) $\boldsymbol{v}$）流动时的“内在”变化率。它的定义方式极具启发性 [@problem_id:2666508]：想象一下，我们把一个物[质点](@article_id:365946)在未来某个瞬时 $t+\varepsilon$ 的[张量](@article_id:321604)值，“[拉回](@article_id:321220)”到它在当前时刻 $t$ 的位置上，然后再与当前时刻的[张量](@article_id:321604)值进行比较。这个“[拉回](@article_id:321220)”操作是沿着物质流动的几何路径进行的，因此整个定义过程完全不依赖于外部[坐标系](@article_id:316753)，是纯粹几何的。

因为 Lie [导数](@article_id:318324)的定义是内在的、几何的，所以它自然就是客观的 [@problem_id:2666508]。当我们把它写成在特定[坐标系](@article_id:316753)下的分量形式时，就得到了不同的共移[导数](@article_id:318324)。例如，**上[随体导数](@article_id:369934) (Upper Convected Rate)** 的表达式就是：
$$
\overset{\triangledown}{\boldsymbol{A}} = \dot{\boldsymbol{A}} - \boldsymbol{L}\boldsymbol{A} - \boldsymbol{A}\boldsymbol{L}^T
$$
这个[导数](@article_id:318324)有一个非常漂亮的性质。考虑[左柯西-格林张量](@article_id:365366) $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^T$，它本身就是对材料当前变形状态的一种度量。如果我们计算它的上[随体导数](@article_id:369934)，会得到一个惊人的简单结果：$\overset{\triangledown}{\boldsymbol{B}} = \mathbf{0}$ [@problem_id:2666504]。这再合理不过了！上[随体导数](@article_id:369934)是在一个与材料同步变形（拉伸和旋转）的[坐标系](@article_id:316753)里进行测量，而 $\boldsymbol{B}$ 本身就代表了这种变形。在一个与自己[完全同步](@article_id:331409)的参照系里，自己当然看起来是“静止”的。

### 终极统一：[Truesdell率](@article_id:360406)的物理根源

Lie [导数](@article_id:318324)这块“哲人石”不仅统一了共移[导数](@article_id:318324)，还为另一个看起来极其复杂的 **Truesdell 率**提供了水晶般清晰的物理解释。

在[连续介质力学](@article_id:315536)中，除了[柯西应力](@article_id:348185) $\boldsymbol{\sigma}$（单位**当前**面积上的力），我们还经常使用一个与之相关的量——基尔霍夫应力 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$，其中 $J$ 是体积变化率。$\boldsymbol{\tau}$ 可以被看作是某种意义上与初始构型相关的“加权”应力。

由于基尔霍夫应力 $\boldsymbol{\tau}$ 的物理性质，它的 Lie [导数](@article_id:318324) $\mathcal{L}_{\boldsymbol{v}}\boldsymbol{\tau}$ 是一个非常自然且客观的变化率。那么，[柯西应力](@article_id:348185) $\boldsymbol{\sigma}$ 的一个自然[客观率](@article_id:377475)定义不就有了吗？我们只需将 $\boldsymbol{\tau}$ 的[客观率](@article_id:377475)“转换”回去即可 [@problem_id:2666508]：
$$
\overset{\triangle}{\boldsymbol{\sigma}} = J^{-1} \mathcal{L}_{\boldsymbol{v}}\boldsymbol{\tau}
$$
这正是 Truesdell 率的几何定义！现在让我们打开这个“黑箱”。利用 $\mathcal{L}_{\boldsymbol{v}}\boldsymbol{\tau} = \dot{\boldsymbol{\tau}} - \boldsymbol{L}\boldsymbol{\tau} - \boldsymbol{\tau}\boldsymbol{L}^T$ 和 $\dot{\boldsymbol{\tau}} = \dot{J}\boldsymbol{\sigma} + J\dot{\boldsymbol{\sigma}}$，再结合质量守恒给出的关系式 $\dot{J} = J(\mathrm{tr}\,\boldsymbol{L})$（体积变化率等于[速度梯度](@article_id:325397)的迹），经过一番推导，我们就得到了 Truesdell 率的完整表达式 [@problem_id:2666484]：
$$
\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^T + (\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}
$$
那个曾经看似多余的、破坏了公式对称美的项 $(\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}$，现在终于露出了它的真面目！它根本不是凭空添加的，而是源于[柯西应力](@article_id:348185) $\boldsymbol{\sigma}$ 和基尔霍夫应力 $\boldsymbol{\tau}$ 之间的关系 $J$。因为[柯西应力](@article_id:348185)是定义在**当前**变形后的面积上的，而这个面积会随着体积的变化而变化，所以当我们计算它的变化率时，必须要把这个体积效应考虑进去。这正是 $(\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}$ 这一项所做的修正。抽象的数学形式背后，是坚实的物理实在。

### 结语：选择的意义

最后，值得澄清的是，我们讨论的**物质框架无关性**是关于**材料本构律**的假设，它要求[本构方程](@article_id:299007)在任意（包括加速和旋转的）观察者看来形式不变。而另一个大家熟知的**[伽利略不变性](@article_id:303965)**则是针对**牛顿运动定律**本身的要求，它只涉及在相互匀速直线运动的[惯性系](@article_id:339197)之间保持形式不变 [@problem_id:2666514]。[客观性原理](@article_id:356369)是一个更强的、施加于材料“性格”之上的约束。

那么，面对动物园里如此多的[客观率](@article_id:377475)，我们该如何选择？在小应变但大转动的情况下，许多共旋率的预言在数值上非常接近，差别只在高阶小量 [@problem_id:2666516]。但在大应变下，选择就变得至关重要。例如，基于 Jaumann 率的简单[弹塑性](@article_id:372155)模型在纯剪切下会给出不符合物理实际的[振荡](@article_id:331484)应力。而某些率，如对数率，其背后有一个真正的能量函数（即它满足**[超弹性](@article_id:319760)**），这使得它在描述弹性行为时具有更坚实的物理基础 [@problem_id:2666516]。

从一个简单的“龙卷风中的叶子”问题出发，我们踏上了一段寻找“真实”变化率的旅程。从最朴素的客观性要求，到共旋与共移两种思想的交锋，最终在 Lie 导[数的几何](@article_id:371956)框架下得以统一。我们看到，每一种[客观率](@article_id:377475)都是对同一个核心问题的不同解答，它们之间的差异反映了我们对“与材料一起运动”这一概念的不同理解。这不仅仅是一场数学游戏，更是物理学家和工程师为了更精确地描述我们这个复杂而动态的世界所做出的不懈努力。