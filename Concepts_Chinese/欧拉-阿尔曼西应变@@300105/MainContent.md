## 引言
当材料经历大变形时，例如将一根橡皮筋拉伸到其两倍长，我们如何精确地测量“应变”？适用于微小变化的简单工程公式开始失效，揭示了描述物理变形时更深层次的复杂性。这种差异标志着一个根本性的知识空白：测量大应变需要选择一个[参考系](@article_id:345789)，一个观察变形的视角。[连续介质力学](@article_id:315536)提供了一个严谨的框架来解决这个问题，它超越了简单的比率，转向更深刻的几何理解。

本文通过探索其核心概念之一：[欧拉-阿尔曼西应变张量](@article_id:373844)，来深入探讨这一框架。它通过呈现“现场记者”的视角——一种根植于材料当前变形状态的描述——来应对描述大规模变形的挑战。接下来的章节将引导您理解这一概念。在**原理与机制**中，我们将从第一性原理出发推导[欧拉-阿尔曼西应变](@article_id:366270)，并将其与其历史上的对应概念——[格林-拉格朗日应变](@article_id:349620)进行对比，揭示连接它们的优雅数学关系。之后，**应用与跨学科联系**将展示为什么这种空间视角在从[计算流体动力学](@article_id:303052)到生物力学等领域中是不可或缺的，阐明应变度量的理论选择如何产生深远的现实世界影响。

## 原理与机制

当我们拉伸一根橡皮筋时，它会变长。这是一个简单的概念，却为物理学中一个出乎意料地丰富而美丽的角落打开了大门。描述这种拉伸最直观的方式是工程师所称的**工程应变**：长度的变化量除以原始长度，即$(\text{新长度} - \text{原长度}) / (\text{原长度})$。如果将一根10厘米长的橡皮筋拉伸到11厘米，应变为 $(11 - 10) / 10 = 0.1$。这对于微小变化非常有效。但是当变化很大时，比如将橡皮筋拉伸到20厘米（应变为1.0）或将一块泡沫压扁到其一半大小（应变为-0.5）时，会发生什么呢？

当变形变大时，我们简单的定义开始失效。不同但同样合理的应变测量方法开始给出不同的答案。例如，我们可以使用**真应变**（也称对数应变），它通过累加整个过程中的所有无穷小拉伸得到，即$\ln(\text{新长度}/\text{原长度})$。对于那根从10厘米拉伸到11厘米的橡皮筋，真应变为 $\ln(1.1) \approx 0.0953$。这个值与0.1相近，但不完全相同。若将其拉伸到20厘米，工程应变为1.0，而真应变为 $\ln(2) \approx 0.693$。现在的差异就非常显著了！[@problem_id:2708309]

这种差异并不意味着一种度量是“对的”而另一种是“错的”。它是一个线索，表明背后有更深层次的东西在发生。它告诉我们，对于大变形，*测量*应变这一行为本身就需要选择一个视角。为了驾驭这个领域，连续介质力学提供了一个更稳健的框架，它不是建立在简单的长度比率上，而是建立在一个更基本、更几何化的思想上。

### 万物的尺度：长度平方的变化

想象一下，在拉伸橡皮筋之前，我们在上面画了一条微小的、长度几乎为零的线段。我们称其初始[向量表示](@article_id:345740)为 $d\boldsymbol{X}$，其初始长度的平方为 $dL^2 = d\boldsymbol{X} \cdot d\boldsymbol{X}$。现在，我们使橡皮筋变形。我们的小线段移动、拉伸并旋转到一个新的方位，我们称之为 $d\boldsymbol{x}$。它的新长度的平方是 $d\ell^2 = d\boldsymbol{x} \cdot d\boldsymbol{x}$。变形的基本度量，即应变的原始物理“素材”，就是这个长度平方的变化量： $d\ell^2 - dL^2$。

这个量是一个标量；它是一个纯数，不依赖于你如何看待它。所有现代应变理论都从这里开始。它们之间的差异源于一个简单的问题：我们如何将这个变化与物体的几何形状联系起来？答案实际上取决于你的视角。你是一位历史学家，将一切与过去作比较？还是一位现场记者，描述眼前的一切？

### 历史学家的视角：[格林-拉格朗日应变](@article_id:349620)

让我们采纳历史学家的视角。我们站在原始的、未变形的世界（**参考构型**）中，并参照它来描述所有变化。我们有初始线段 $d\boldsymbol{X}$，并且我们知道最终线段通过**变形梯度**[张量](@article_id:321604) $\boldsymbol{F}$ 与它相关联，即 $d\boldsymbol{x} = \boldsymbol{F}d\boldsymbol{X}$。[张量](@article_id:321604) $\boldsymbol{F}$ 就像一本局部字典，将向量从参考构型翻译到当前构型。

让我们仅使用参考构型的语言来写出我们的基本量，即长度平方的变化量：
$$
d\ell^2 - dL^2 = ( \boldsymbol{F}d\boldsymbol{X} ) \cdot ( \boldsymbol{F}d\boldsymbol{X} ) - d\boldsymbol{X} \cdot d\boldsymbol{X}
$$
使用[点积](@article_id:309438)的性质稍作整理可得：
$$
d\ell^2 - dL^2 = d\boldsymbol{X} \cdot (\boldsymbol{F}^T \boldsymbol{F} d\boldsymbol{X}) - d\boldsymbol{X} \cdot d\boldsymbol{X} = d\boldsymbol{X} \cdot [(\boldsymbol{F}^T \boldsymbol{F} - \boldsymbol{I})d\boldsymbol{X}]
$$
其中 $\boldsymbol{I}$ 是单位[张量](@article_id:321604)。

看括号里的项。它是一个新[张量](@article_id:321604) $\boldsymbol{F}^T \boldsymbol{F} - \boldsymbol{I}$，捕捉了整个变形。为了使其成为一个在小变形情况下与工程应变一致的正式应变度量，我们定义**[格林-拉格朗日应变张量](@article_id:366888)** $\boldsymbol{E}$ 为它的一半：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^T \boldsymbol{F} - \boldsymbol{I})
$$
于是，长度平方的变化量可以优雅地表示为 $2\,d\boldsymbol{X} \cdot \boldsymbol{E}\,d\boldsymbol{X}$ [@problem_id:2657136][@problem_id:2896798]。因为 $\boldsymbol{E}$ 是使用根植于初始未变形物体的向量和运算来定义的，所以它被称为**物质**或**拉格朗日**应变度量。这是历史学家对变形的记录。

### 现场记者的视角：[欧拉-阿尔曼西应变](@article_id:366270)

现在，让我们换个角色，成为一名置身于变形材料中的现场记者。我们现在处于最终的、变形后的世界（**当前构型**）。我们希望描述相同的物理变化 $d\ell^2 - dL^2$，但只使用*当前*的语言。我们现在的基本构件是最终的线段 $d\boldsymbol{x}$。

为此，我们需要用当前几何来表示*原始*长度 $dL^2$。我们只需反转我们的字典：$d\boldsymbol{X} = \boldsymbol{F}^{-1}d\boldsymbol{x}$。
$$
dL^2 = (\boldsymbol{F}^{-1}d\boldsymbol{x}) \cdot (\boldsymbol{F}^{-1}d\boldsymbol{x}) = d\boldsymbol{x} \cdot [\boldsymbol{F}^{-T}\boldsymbol{F}^{-1}d\boldsymbol{x}]
$$
现在我们从这个新视角来写长度平方的变化量：
$$
d\ell^2 - dL^2 = d\boldsymbol{x} \cdot d\boldsymbol{x} - d\boldsymbol{x} \cdot [\boldsymbol{F}^{-T}\boldsymbol{F}^{-1}d\boldsymbol{x}] = d\boldsymbol{x} \cdot [(\boldsymbol{I} - \boldsymbol{F}^{-T}\boldsymbol{F}^{-1})d\boldsymbol{x}]
$$
和之前一样，这启发了一个新的应变度量。我们定义**[欧拉-阿尔曼西应变张量](@article_id:373844)** $\boldsymbol{e}$ 为：
$$
\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{F}^{-T}\boldsymbol{F}^{-1})
$$
量 $\boldsymbol{F}\boldsymbol{F}^T$ 通常被称为[左柯西-格林张量](@article_id:365366) $\boldsymbol{b}$，所以它的逆是 $\boldsymbol{b}^{-1} = \boldsymbol{F}^{-T}\boldsymbol{F}^{-1}$。这给出了该定义最常见的形式：
$$
\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{b}^{-1})
$$
我们的长度平方变化量现在写为 $2\,d\boldsymbol{x} \cdot \boldsymbol{e}\,d\boldsymbol{x}$ [@problem_id:2640421]。这是一个**空间**或**欧拉**应变度量。它描述了应变在物体当前所占据的空间中*当下*的状态。

### 连接两个世界

历史学家（$\boldsymbol{E}$）和现场记者（$\boldsymbol{e}$）描述的是完全相同的物理事件 $d\ell^2 - dL^2$，只是视角不同。因此，他们的度量理应可以相互转换。因为它们都描述了相同的[二次型](@article_id:314990)，我们得到一个等式 [@problem_id:2695241]：
$$
d\boldsymbol{X} \cdot \boldsymbol{E}\,d\boldsymbol{X} = d\boldsymbol{x} \cdot \boldsymbol{e}\,d\boldsymbol{x}
$$
通过在右侧代入 $d\boldsymbol{x} = \boldsymbol{F}d\boldsymbol{X}$，我们可以将现场记者的测量带回到历史学家的世界：
$$
d\boldsymbol{X} \cdot \boldsymbol{E}\,d\boldsymbol{X} = (\boldsymbol{F}d\boldsymbol{X}) \cdot \boldsymbol{e}\,(\boldsymbol{F}d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{F}^T \boldsymbol{e} \boldsymbol{F}) d\boldsymbol{X}
$$
由于这对任何微小线段 $d\boldsymbol{X}$ 都必须成立，[张量](@article_id:321604)本身必须有如下关系：
$$
\boldsymbol{E} = \boldsymbol{F}^T \boldsymbol{e} \boldsymbol{F}
$$
这个优美的操作被称为**后拉（pull-back）**；它将[空间张量](@article_id:365009) $\boldsymbol{e}$ [拉回](@article_id:321220)到参考构型。我们同样可以轻易地反转这个关系，将物质[张量](@article_id:321604) $\boldsymbol{E}$ **前推（push-forward）**到当前构型 [@problem_id:2695241] [@problem_id:2709088]：
$$
\boldsymbol{e} = \boldsymbol{F}^{-T} \boldsymbol{E} \boldsymbol{F}^{-1}
$$
这些方程是有限应变的罗塞塔石碑，让我们能够在物质描述和空间描述之间无缝转换。它们表明 $\boldsymbol{E}$ 和 $\boldsymbol{e}$ 不是独立的实体，而是同一枚硬币的两面。这种深刻的联系甚至给出了它们的[主值](@article_id:368662)（沿[主拉伸](@article_id:373569)轴的应变）之间的直接代数关系，$\boldsymbol{E}$ 的[主值](@article_id:368662)为 $\epsilon$，$\boldsymbol{e}$ 的主值为 $\eta$：$\epsilon = \eta / (1-2\eta)$ [@problem_id:1551021]。

### 客观性检验：应变度量的荣誉勋章

一个真正的变形度量不应被无关紧要的运动所迷惑。如果我们拿起橡皮筋，只是移动或旋转它，而没有任何拉伸或剪切，那么应变必须为零。$\boldsymbol{E}$ 和 $\boldsymbol{e}$ 都完美地通过了这个检验：对于任何[刚体运动](@article_id:329499)，$\boldsymbol{F}$ 是一个纯旋转矩阵，这直接导致了 $\boldsymbol{E}=\boldsymbol{0}$ 和 $\boldsymbol{e}=\boldsymbol{0}$ [@problem_id:2922623]。

但还有一个更微妙的检验。如果我们先使物体变形，然后一个观察者从一个不同的角度（**叠加[刚体运动](@article_id:329499)**）来观察整个实验，会怎么样？物理过程没有改变，但观察者的[坐标系](@article_id:316753)改变了。一个有效的应变度量应该有合理的表现。在这里，$\boldsymbol{E}$ 和 $\boldsymbol{e}$ 的不同性质得以彰显。
[格林-拉格朗日应变](@article_id:349620) $\boldsymbol{E}$ 与物体固有的参考状态相关联，完全不受影响。外部观察者的旋转不会改变记录在材料内部的历史。新的应变 $\hat{\boldsymbol{E}}$ 与旧的应变 $\boldsymbol{E}$ 完全相同 [@problem_id:2922623]。
然而，[欧拉-阿尔曼西应变](@article_id:366270) $\boldsymbol{e}$ 存在于物理空间中。当观察者通过旋转矩阵 $\boldsymbol{Q}$ 旋转其视点时，[张量](@article_id:321604) $\boldsymbol{e}$ 会随物体一同旋转：$\hat{\boldsymbol{e}} = \boldsymbol{Q}\boldsymbol{e}\boldsymbol{Q}^T$ [@problem_id:2640421]。这个性质被称为**客观性**，正是这种可预测的变换使得这些[张量](@article_id:321604)具有物理意义。

### 加法的陷阱

让我们回到简单的[单轴拉伸](@article_id:367416)。如果我们将一根杆拉伸因子为 $a$，然后再拉伸因子为 $b$，总拉伸因子是 $ab$。我们能通过简单地将每一步的应变相加来得到总应变吗？让我们来验证一下。对于[格林-拉格朗日应变](@article_id:349620)，总应变为 $E_{total} = E_a + E_b + 2 E_a E_b$。对于[欧拉-阿尔曼西应变](@article_id:366270)，也存在类似的非可加关系。所以，答案是不能！[@problem_id:2640405]

这种非可加性直接源于其定义的二次性质（$\boldsymbol{F}^T\boldsymbol{F}$ 和 $\boldsymbol{b}^{-1}$）。当你组合变形时，你需要将 $\boldsymbol{F}$ [张量](@article_id:321604)相乘，而对这个乘积进行平方会产生[交叉](@article_id:315017)项，从而破坏了简单的加法。只有在变形非常小的情况下，这些[交叉](@article_id:315017)项才可以忽略不计，应变才近似可加 [@problem_id:2886611][@problem_id:2640405]。这是一个深刻的观点：一个对于单步变形在几何上和物理上都完美的应变度量，对于一系列变形在代数上可能并不方便。（在这种情况下，唯一*可加*的应变度量是对数[Hencky应变](@article_id:370352)，正是因为对数将乘积变成了和）。

### 我们为什么需要现场记者？

既然[格林-拉格朗日应变](@article_id:349620)通过追溯到一个不变的[参考系](@article_id:345789)而显得更“基础”，那么我们为什么还需要[欧拉-阿尔曼西应变](@article_id:366270)呢？答案在于我们研究现实世界的方式，特别是在[流体动力学](@article_id:319275)和计算工程等领域。

在许多问题中，我们没有一个方便的未变形状态可以追溯。想象一下在管道中流动的水；它的“原始”形状是什么？所有重要的是当前的流动状态。在这里，空间描述是唯一自然的选择。

即使在固体力学中，对于模拟车祸或金属锻造等复杂过程，我们也使用计算机分小的时间步来解决问题。在这种**更新[拉格朗日](@article_id:373322)（Updated Lagrangian）**提法中，一个时间步结束时的构型成为下一个微小变形增量的“参考”。要描述这个小步骤中的应变，最自然的方法是使用基于当前几何的空间度量——[欧拉-阿尔曼西应变](@article_id:366270)是一个完美的选择。对于微小的增量位移，增量[欧拉-阿尔曼西应变](@article_id:366270)会漂亮地简化为我们熟悉的[无穷小应变](@article_id:375995)，使其在计算上非常方便 [@problem_id:2709088]。它是*当下*的语言，而这正是在一步步构建未来时所需要的。