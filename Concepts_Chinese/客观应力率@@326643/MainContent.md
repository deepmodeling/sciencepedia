## 引言
在研究材料如何变形时，当运动巨大且复杂时，会出现一个根本性的挑战。我们如何测量一个同时被拉伸和旋转的材料内部应力的真实变化？这个问题是连续介质力学的核心，并突显了简单化方法中的一个关键缺陷：应力变化的标准率并非独立于观察者的视角。这种未能遵循**[物质标架无关性原理](@article_id:356369)**的情况会导致物理上无意义的模型，尤其是在涉及大旋转的情景中。本文将直面这一问题。首先，在“原理与机制”一章中，我们将深入探讨客观性的概念，论证为何应力的简单时间[导数](@article_id:318324)会失效，并探索**共旋[导数](@article_id:318324)**或[客观应力率](@article_id:378041)这一精妙的解决方案。在这一理论基础之后，“应用与跨学科联系”一章将揭示为何这些概念不仅仅是学术性的，而且对计算工程的实践世界至关重要，影响着从有限元模拟的准确性到[结构稳定性](@article_id:308355)的预测等方方面面。

## 原理与机制

想象一下你正在搅拌一大锅又厚又冷的太妃糖。这很费力。太妃糖抵抗拉伸和变形——它处于**应力**状态。但它也随着你的勺子的圆周运动而被带动。如果你是一个漂浮在太妃糖中的微小观察者，你就会不停地旋转。从你旋转的视角来看，你将如何测量由太妃糖被拉伸引起的“真实”应力变化，以区别于由你自身旋转引起的表观变化？这个简单的问题将我们带入[连续介质力学](@article_id:315536)中最微妙和精妙的概念之一：对**[客观应力率](@article_id:378041)**的需求。

### 观察者问题：为何你的时间[导数](@article_id:318324)不是我的时间[导数](@article_id:318324)

物理学的核心在于一个优美的对称性原理：自然法则不应依赖于观察者。材料的内在本构行为——即它如何响应力而变形——无论是从静止的实验室观察，还是从旋转的木马上观察，都必须是相同的。这个思想被称为**[物质标架无关性原理](@article_id:356369)**，或称**客观性**。它要求我们的[本构方程](@article_id:299007)，即描述[材料行为](@article_id:321825)的数学法则，在观察者的任何刚体运动下都必须保持其形式不变 [@problem_id:2906321]。

让我们看看这对压力意味着什么。太妃糖内部的应力由一个称为[柯西应力张量](@article_id:326933)的数学对象 $\boldsymbol{\sigma}$ 来描述。如果一个新的观察者相对于你正在旋转，其旋转由一个[旋转张量](@article_id:370993) $\boldsymbol{Q}(t)$ 描述，那么他们将测量到一个不同的应力张量 $\boldsymbol{\sigma}^*$，其分量就是你的[张量](@article_id:321604)分量旋转后的结果：$\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T$。这完全合理；你们都在观察同一种物理应力状态，只是从不同的角度看而已。

当我们考虑应力如何随时间*变化*时，问题就来了。我们可能天真地认为应力变化率就是其时间[导数](@article_id:318324)，$\dot{\boldsymbol{\sigma}} = d\boldsymbol{\sigma}/dt$。但是这个率是“客观的”吗？让我们通过对变换法则求时间[导数](@article_id:318324)来检验一下：
$$ \dot{\boldsymbol{\sigma}}^* = \frac{d}{dt}(\boldsymbol{Q} \boldsymbol{\sigma} \boldsymbol{Q}^T) = \dot{\boldsymbol{Q}} \boldsymbol{\sigma} \boldsymbol{Q}^T + \boldsymbol{Q} \dot{\boldsymbol{\sigma}} \boldsymbol{Q}^T + \boldsymbol{Q} \boldsymbol{\sigma} \dot{\boldsymbol{Q}}^T $$
如果我们将观察者的自旋定义为[反对称张量](@article_id:370125) $\boldsymbol{\Omega} = \dot{\boldsymbol{Q}}\boldsymbol{Q}^T$，这个方程就变成 [@problem_id:2700483] [@problem_id:2691194]：
$$ \dot{\boldsymbol{\sigma}}^* = \boldsymbol{Q} \dot{\boldsymbol{\sigma}} \boldsymbol{Q}^T + \boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega} $$
看看那些多出来的项！新观察者看到的应力率 $\dot{\boldsymbol{\sigma}}^*$，并不仅仅是你的应力率的旋转版本 $\boldsymbol{Q} \dot{\boldsymbol{\sigma}} \boldsymbol{Q}^T$。它还包含了依赖于观察者自旋 $\boldsymbol{\Omega}$ 的附加部分。这意味着简单的物质时间导数 $\dot{\boldsymbol{\sigma}}$ 是**不客观的**。它将由变形引起的真实物理应力变化与由观察者旋转引起的虚假运动学变化混合在一起。在本构律中使用 $\dot{\boldsymbol{\sigma}}$ 就像试图用一把会随机收缩和旋转的尺子来测量植物的生长一样，得到的数字将毫无意义。

### 共旋思想：随材料一同转动

那么，我们如何解决这个问题呢？答案堪称神来之笔。如果问题在于旋转，那我们就把它减掉！我们需要发明一种新的[导数](@article_id:318324)，即**[客观应力率](@article_id:378041)**，它从一个与材料“同步前进”、每时每刻都与之共旋的观察者的角度来测量应力变化。这便是**共旋率**。

其中最直观的是 **Jaumann 应力率**。其思想是利用材料自身的[局部旋转](@article_id:353495)速率，即所谓的**[自旋张量](@article_id:366504)** $\boldsymbol{W}$，来定义共旋[参考系](@article_id:345789)。[自旋张量](@article_id:366504)就是[速度梯度](@article_id:325397) $\boldsymbol{L}$ 的反对称（或旋转）部分，即 $\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^T)$。于是，Jaumann 率被定义为 [@problem_id:2911179]：
$$ \overset{\nabla}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W} $$
我们添加的这些项，被称为[李括号](@article_id:640756)或交换子，正是为了精确地解释因材料旋转而引起的应力张量分量变化率的“修正项”。这是一项精美的数学工程。为了验证其有效性，让我们回到一个预应力体经历纯刚性旋转的测试案例。在这种情况下，没有变形，只有自旋，所以速度梯度就是 $\boldsymbol{L} = \boldsymbol{W}$。应力张量随物体进行物理旋转，这意味着其时间[导数](@article_id:318324)恰好是 $\dot{\boldsymbol{\sigma}} = \boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}$。将此代入 Jaumann 率的定义中，得到：
$$ \overset{\nabla}{\boldsymbol{\sigma}} = (\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}) - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W} = \boldsymbol{0} $$
它完美地奏效了！[客观率](@article_id:377475)为零，正确地告诉我们没有因变形产生新的应力——因为根本没有任何变形。应力只是被动地旋转了而已 [@problem_id:2911179] [@problem_id:2666516]。这符合我们的物理直觉和[客观性原理](@article_id:356369)。

### 率的“动物园”：并非所有旋转都生而平等

要是事情这么简单就好了。事实证明，“材料旋转”的概念并非唯一。它是速度场 $\boldsymbol{W}$ 的瞬时自旋吗？还是材料底层结构本身的旋转，由变形梯度[极分解](@article_id:375742)（$\boldsymbol{F} = \boldsymbol{RU}$）中的[旋转张量](@article_id:370993) $\boldsymbol{R}$ 来描述？对共旋[参考系](@article_id:345789)的不同选择，会产生一个由各种不同[客观率](@article_id:377475)组成的“动物园”。

除了 **Jaumann 率**，这个动物园里其他著名的成员还包括：
*   **[Green-Naghdi率](@article_id:369882)**，它使用材料[旋转张量](@article_id:370993) $\boldsymbol{R}$ 的自旋。许多人认为这种率与材料的实际方向在物理上联系更紧密 [@problem_id:2609660]。
*   **Truesdell 率**，它不完全是共旋的，而是通过将变化率与参考构形联系起来推导出来的。它的结构有根本性的不同 [@problem_id:2610336]。

对于非常小的变形，这些不同的率会给出几乎相同的结果。只有当大旋转与变形相结合时，差异才会变得显著 [@problem_id:2666516]。而且这些差异可能是巨大的！一个著名的例子是简[单剪切](@article_id:359902)运动中应力的预测。如果我们使用 Jaumann 率建立一个简单的基于率的（**[亚弹性](@article_id:382974)**）材料模型，它会预测剪应力随着剪切的增加而发生非物理性的[振荡](@article_id:331484)。然而，使用 Green-Naghdi 率的模型则会预测一个更为合理的、单调增加的应力。这表明，[客观率](@article_id:377475)的选择不仅仅是一场学术辩论；它对预测材料的行为具有真实、可测量的后果。[@problem_id:2609660] [@problem_id:2610336]。

### 更深层次的问题：[路径依赖性](@article_id:365518)与势能的探寻

这就引出了一个更深层次的问题。弹性的整个理念植根于能量的储存和释放，就像弹簧一样。当你拉伸一个真正的弹性材料，然后让它恢复原状时，所做的[净功](@article_id:374695)应该为零。你输入的能量被储存起来，然后又被释放出来。具有这种性质的材料被称为**超弹性**材料，其行为可以从一个称为**储能势** $\psi$ 的标量函数中推导出来。在这个优美的图景中，应力仅仅是势能对应变度量的[导数](@article_id:318324)（例如，$\boldsymbol{S} = 2 \frac{\partial \psi}{\partial \boldsymbol{C}}$，其中 $\boldsymbol{C}$ 是右 Cauchy-Green [应变张量](@article_id:372284)）。

关键的是，在超[弹性理论](@article_id:363424)中，你根本不需要[客观应力率](@article_id:378041)！通过将势能 $\psi$ 定义为客观应变张量（如 $\boldsymbol{C}$）的函数，客观性就自动得到了满足，因为 $\boldsymbol{C}$ 本身对观察者的旋转是不变的。任何时刻的应力完全由该时刻的变形决定，而不是由达到该状态所经过的路径决定。[@problem_id:2567310]。

那么，我们基于率的**[亚弹性](@article_id:382974)**模型（如 $\overset{\nabla}{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$）能否通过积分找到一个底层的能量势呢？所做的功是否与路径无关？对于大多数[客观率](@article_id:377475)的选择，包括流行的 Jaumann 率，惊人的答案是**否**。你可以让材料在一个闭合回路上变形（例如，一个简[单剪切](@article_id:359902)循环），会发现模型预测了能量的净产生或净消耗。[@problem_id:2872325]。这是因为“[应力功率](@article_id:362231)[一阶微分形式](@article_id:334092)”在数学上不是“恰当的”——它不能被写成一个势能函数的[全导数](@article_id:298038)。[@problem_id:2872325]。

然而，有一个漂亮的例外证明了这条规则。存在一种特殊的[客观率](@article_id:377475)，即**对数率**，当与一个恒定的[弹性张量](@article_id:349909)一起使用时，它是*可积的*。它对应于一个超弹性模型，其中能量是对数（或 Hencky）应变的二次函数。这揭示了运动学（率的选择）和[热力学](@article_id:359663)（势的存在性）之间深刻而微妙的统一。[@problem_id:2647787]。

从描述一锅被搅拌的太妃糖这个简单问题出发，我们的旅程带领我们穿越了客观性的基本原理、共旋率的巧妙发明以及在它们之间进行选择的实际后果。最终，它向我们展示了这些基于率的模型与更基础的、基于能量的超弹性框架之间的深刻联系。这证明了在物理学中，对一个看似简单的观察进行仔细而诚实的分析，可以如何展开成一个丰富而优美的理论结构，这个结构不仅在智力上令人满足，而且对我们世界的实际工程——从设计汽车轮胎到模拟生物组织的行为——都至关重要。[@problem_id:2691194] [@problem_id:2616473]。