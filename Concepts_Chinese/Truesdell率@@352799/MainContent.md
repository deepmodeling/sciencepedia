## 引言
在研究材料如何变形（从橡皮筋的拉伸到地壳板块的流动）时，我们面临一个根本性的挑战：如何以一种独立于观察者的方式来描述物理定律？无论我们是在静止的实验室里观察，还是在旋转的航天器上观察，自然法则都不应改变。这个“材料框架无关性”原理是[连续介质力学](@article_id:315536)的基石，然而，当我们试图测量应力如何随时间变化时，它却带来了一个重大问题。最直观的度量方法——应力的物质时间导数——未能通过这一检验，因为其数值受到了观察者自身旋转的“污染”。

本文旨在通过探索[客观应力率](@article_id:378041)的概念来填补这一关键的知识空白。[客观应力率](@article_id:378041)是为提供一种真实的、与观察者无关的应力变化度量而设计的数学工具。本文将重点介绍其中一种最强大且最具物理洞察力的工具：[Truesdell率](@article_id:360406)。通过两个章节，您将对这一基本概念有深入的了解。
- **原理与机制**一章将揭示“观察者问题”，介绍[Jaumann率](@article_id:364795)等较为简单的[客观率](@article_id:377475)，然后推导[Truesdell率](@article_id:360406)，并强调其独特的结构和物理意义。
- **应用与跨学科联系**一章将展示[Truesdell率](@article_id:360406)在[预测建模](@article_id:345714)中的实际优势、其在现代计算模拟中的基础作用，以及其在固[体力](@article_id:353281)学之外领域（如[非牛顿流体](@article_id:306022)研究）中的相关性。

## 原理与机制
想象一下，您正坐在一架快速旋转的旋转木马上，试图描述您刚刚倒入咖啡中的奶油那优雅的漩涡。对您来说，奶油似乎被某种神秘的力量向外推，其路径以一种令人困惑的方式弯曲。然而，一个站在地面上的人看到的景象要简单得多：奶油只是随着旋转的咖啡一起移动，并缓慢地混合进去。支配这种流体的基本物理学——其粘度、密度以及它如何抵抗搅拌——并没有改变。唯一改变的是您，即观察者。自然法则的书写方式必须保证，对于您和地面上的人来说，它们看起来是相同的。这个强大的思想被称为**材料框架无关性原理**（principle of material frame-indifference），或简称为**客观性**（objectivity）。在材料世界中，这不仅仅是一种哲学上的偏好，而是对任何物理定律的严格要求。[@problem_id:2550539]

### 观察者问题：旋转的宇宙

当我们研究材料如何变形时——例如钢梁在荷载下弯曲、聚合物被拉伸或地壳板块移动——我们需要写下[本构定律](@article_id:357811)，将材料内部的力（**应力**）与其变形速率（**[应变率](@article_id:331700)**）联系起来。我们希望了解应力如何随时间变化。描述应力 $\boldsymbol{\sigma}$ 变化最显而易见的方法就是简单地对其求时间[导数](@article_id:318324)，我们记作 $\dot{\boldsymbol{\sigma}}$。这就是我们所说的**物质时间导数**；它告诉我们一个微小的材料质点在移动和变形时其应力是如何变化的。

但在这里，我们遇到了旋转木马问题。事实证明，这个简单直观的[导数](@article_id:318324)并非客观的。如果您（观察者）在材料变形时决定旋转您的[参考系](@article_id:345789)，您测量的 $\dot{\boldsymbol{\sigma}}$ 将与静止观察者测量的不同。您自身的旋转“污染”了测量结果。在数学上，如果一个新观察者相对于旧观察者以自旋 $\boldsymbol{\Omega}$ 旋转，则新的时间[导数](@article_id:318324) $\dot{\boldsymbol{\sigma}}^\ast$ 与旧的[导数](@article_id:318324)关系如下：

$$
\dot{\boldsymbol{\sigma}}^{\ast} = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}
$$

其中 $\boldsymbol{Q}$ 是关联两个[参考系](@article_id:345789)的[旋转张量](@article_id:370993)。一个客观的量应该简单地变换为 $\boldsymbol{A}^\ast = \boldsymbol{Q}\boldsymbol{A}\boldsymbol{Q}^{\mathsf{T}}$。多出来的两项 $\boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}$ 就是问题所在。它们是观察者自旋造成的假象，而非材料应力状态的真实物理变化。基于 $\dot{\boldsymbol{\sigma}}$ 建立的[本构定律](@article_id:357811)会根据科学家选择如何旋转而预测出不同的[材料行为](@article_id:321825)——这显然是荒谬的。[@problem_id:2905931]

### 随动修正：驯服自旋

我们如何解决这个问题呢？关键在于定义一个对观察者自旋“免疫”的、“更聪明”的[导数](@article_id:318324)。其思想是在一个与材料本身一同旋转的[坐标系](@article_id:316753)中测量应力的变化率。这被称为**随动[坐标系](@article_id:316753)**（corotational frame）。通过这样做，我们可以抵消非客观的旋转效应。

实现这一目标最著名的方法之一是**Zaremba–[Jaumann率](@article_id:364795)**（或简称[Jaumann率](@article_id:364795)）。我们取[物质时间导数](@article_id:369934) $\dot{\boldsymbol{\sigma}}$，并根据材料自身的旋转速率添加修正项。材料的旋转速率由**[自旋张量](@article_id:366504)** $\boldsymbol{W}$ 描述。[自旋张量](@article_id:366504) $\boldsymbol{W}$ 是[速度梯度](@article_id:325397) $\boldsymbol{L}$ 的反对称部分。其定义为：

$$
\overset{\mathrm{J}}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$

这里的奥妙在于，[自旋张量](@article_id:366504) $\boldsymbol{W}$ 的变换方式恰好能够抵消掉来自观察者旋转的讨厌的 $\boldsymbol{\Omega}$ 项。因此，[Jaumann率](@article_id:364795) $\overset{\mathrm{J}}{\boldsymbol{\sigma}}$ 是**客观的**。我们可以用它来建立[本构定律](@article_id:357811)，并确信我们的物理预测不会因为我们碰巧在旋转木马上而改变。[Jaumann率](@article_id:364795)只是众多可能的[客观率](@article_id:377475)之一；其他率，如**Green–Naghdi率**，使用不同的方法度量材料的自旋，但同样能实现客观性的目标。[@problem_id:2905949] [@problem_id:2886962]

### 两种应力的故事：揭示[Truesdell率](@article_id:360406)

那么，我们大功告成了吗？我们已经有了[客观率](@article_id:377475)。为什么还需要别的呢？这时，现代连续介质力学的奠基人之一Clifford Truesdell的深刻见解就发挥了作用。他认为变形不仅仅是旋转，还包括拉伸以及重要的体积变化。

**[Cauchy应力](@article_id:348185)** $\boldsymbol{\sigma}$ 被定义为单位*当前*面积上的力。当材料被压缩或拉伸时，其体积和密度会发生变化。这意味着力所分布的那个面积本身就在变化。一个真正全面的应力率难道不应该考虑这种效应吗？

为了构建这样一个率，我们可以使用一个巧妙的概念工具。让我们定义一个不同的[应力度量](@article_id:377578)，即**Kirchhoff应力** $\boldsymbol{\tau}$，其定义为：

$$
\boldsymbol{\tau} = J\boldsymbol{\sigma}
$$

其中 $J$ 是一个材料微元当前体积与其初始体积之比。您可以将Kirchhoff应力看作是[Cauchy应力](@article_id:348185)的一个“体积加权”版本。

现在，在连续介质力学中，一个非常自然的[客观率](@article_id:377475)是**Oldroyd上随体导数**，它对任意[张量](@article_id:321604) $\boldsymbol{A}$ 定义为 $\boldsymbol{A}^{\nabla} = \dot{\boldsymbol{A}} - \boldsymbol{L}\boldsymbol{A} - \boldsymbol{A}\boldsymbol{L}^{\mathsf{T}}$。它考虑了由完整的**速度梯度** $\boldsymbol{L}$（包括拉伸 $\boldsymbol{D}$ 和自旋 $\boldsymbol{W}$）引起的变化。让我们将这个稳健的率应用于我们的Kirchhoff应力 $\boldsymbol{\tau}$。

**[Cauchy应力](@article_id:348185)的[Truesdell率](@article_id:360406)**，记作 $\overset{\mathrm{T}}{\boldsymbol{\sigma}}$，被定义为与Kirchhoff应力的Oldroyd率相一致的比率，并按体积变化 $J$ 进行缩放。也就是说，我们要求：

$$
J\,\overset{\mathrm{T}}{\boldsymbol{\sigma}} = \boldsymbol{\tau}^{\nabla} = \dot{\boldsymbol{\tau}} - \boldsymbol{L}\boldsymbol{\tau} - \boldsymbol{\tau}\boldsymbol{L}^{\mathsf{T}}
$$

这看起来可能只是一个数学定义，但它是一个深刻的物理陈述。我们通过将[Cauchy应力](@article_id:348185)的“正确”率与一个已经和体积变化相关联的[应力度量](@article_id:377578)率联系起来，来定义它。现在，我们可以揭示[Truesdell率](@article_id:360406)了。我们将 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 代入，并使用运动学恒等式 $\dot{J} = J\,\mathrm{tr}(\boldsymbol{L})$（它表明体积变化率与速度梯度的迹相关）。经过一些微积分运算后，$J$ 项被消去，我们得到了一个优美而富有启发性的表达式 [@problem_id:2666484] [@problem_id:2609664]：

$$
\overset{\mathrm{T}}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^{\mathsf{T}} + (\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}
$$

这就是[Truesdell率](@article_id:360406)。前三项是 $\boldsymbol{\sigma}$ 的Oldroyd率。最后一项 $(\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}$ 是关键的补充。它直接源于体积比 $J$ 的时间[导数](@article_id:318324)。由于 $\mathrm{tr}\,\boldsymbol{L}$ 代表材料的[体积膨胀](@article_id:304671)率，这一项明确地解释了材料密度的变化如何影响应力。对于纯粹的膨胀运动，即材料在不改变形状的情况下均匀膨胀或收缩，该项起着核心作用。[@problem_id:2609664]

### 区别何在？拉伸与自旋

我们现在有了两种[客观率](@article_id:377475)：[Jaumann率](@article_id:364795)和[Truesdell率](@article_id:360406)。它们之间的根本区别是什么？我们可以通过简单地将两者相减来找出答案。在使用分解式 $\boldsymbol{L} = \boldsymbol{D}+\boldsymbol{W}$（其中 $\boldsymbol{D}$ 是对称的变形率[张量](@article_id:321604)，或称[拉伸张量](@article_id:372157)）后，数学运算揭示了一个非常清晰的结果：

$$
\overset{\mathrm{T}}{\boldsymbol{\sigma}} - \overset{\mathrm{J}}{\boldsymbol{\sigma}} = (\mathrm{tr}\,\boldsymbol{D})\boldsymbol{\sigma} - (\boldsymbol{D}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{D})
$$

注意这里缺少了什么：[自旋张量](@article_id:366504) $\boldsymbol{W}$。这两个率之间的全部差异仅取决于运动的**拉伸**部分 $\boldsymbol{D}$ 和应力状态 $\boldsymbol{\sigma}$。[@problem_id:2666095] [@problem_id:2666501]

这告诉了我们一切。[Jaumann率](@article_id:364795)是一个最小化的修正；它只考虑了材料的自旋。而[Truesdell率](@article_id:360406)做得更多：它同时考虑了自旋*和*拉伸。只有当材料没有变形（$\boldsymbol{D}=\boldsymbol{0}$）或者当拉伸和应力满足特殊条件 $(\mathrm{tr}\,\boldsymbol{D})\boldsymbol{\sigma} = \boldsymbol{D}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{D}$ 时，这两个率才是相同的。在所有其他情况下，它们会给出不同的答案，反映了它们不同的物理基础。

### 更深层的意义：形状与尺寸的耦合

谜题的最后一块揭示了最深刻的物理后果。任何应力状态都可以分解为两部分：一个表示压力并与体积（尺寸）变化相关的**球形**（或静水压）部分 $p\boldsymbol{I}$，以及一个与剪切和形状变化相关的**偏应力**部分 $\boldsymbol{s}$。所以，$\boldsymbol{\sigma} = p\boldsymbol{I} + \boldsymbol{s}$。

当我们将[Jaumann率](@article_id:364795)应用于这个分解后的应力时，我们发现它将这两部分整齐地分开了。球形部分的变化率只取决于 $\dot{p}$，而[偏应力](@article_id:342743)部分的变化率只取决于 $\dot{\boldsymbol{s}}$ 和 $\boldsymbol{s}$。它们之间没有相互影响。

然而，[Truesdell率](@article_id:360406)则不同。由于其定义包含了[拉伸张量](@article_id:372157) $\boldsymbol{D}$，它**耦合**了球形响应和[偏应力](@article_id:342743)响应。压力的变化率可能会受到偏应力 $\boldsymbol{s}$ 的影响，而[偏应力](@article_id:342743)部分的变化率也受到压力 $p$ 的影响。例如，在一个简[单剪切](@article_id:359902)流中（这是一种纯粹的形状改变运动），[Truesdell率](@article_id:360406)和[Jaumann率](@article_id:364795)的[偏应力](@article_id:342743)率部分之间的差异可能直接取决于材料中的压力 $p$。[@problem_id:2666515]

这种耦合并非数学上的巧合，它反映了一种潜在的物理现实。对于许多材料来说，压缩它们（增加压力）会使其变得更硬，更能抵抗剪切。[Truesdell率](@article_id:360406)提供了一个自然的框架来捕捉这种行为。选择[Jaumann率](@article_id:364795)、[Truesdell率](@article_id:360406)还是其他[客观率](@article_id:377475)，不仅仅是品味问题；这是一个本构选择，它内含了关于材料本身基本行为的不同假设。从旋转的咖啡杯到[张量微积分](@article_id:321827)中这些微妙的差别，这段旅程揭示了物理学的一个核心原则：寻求一种独立于观察者的对自然的描述，往往会引导我们对被观察事物本身有更深刻的理解。