## 引言
热与机械力之间的关系是几乎所有物理科学和工程领域中的一个关键考量。我们凭直觉知道材料受热会膨胀，但这个简单的事实背后隐藏着复杂的现实：为什么受热的铁轨会以毁灭性的力量屈曲，而另一个物体却能无害地膨胀？答案在于超越肤浅的理解，去掌握温度、变形和内应力之间错综复杂的相互作用。这一知识鸿沟由连续介质力学的一项基本原理所填补：杜哈梅-诺依曼定律。本文将对这一优美的理论进行全面探索。第一部分**“原理与机制”**将解构该定律本身，解释应变如何分解为热分量和弹性分量，以及这一概念如何植根于[热力学](@article_id:359663)。随后，**“应用与跨学科联系”**部分将展示该定律深远的实际影响，说明它如何被用于解决工程学、[材料科学](@article_id:312640)和[地球物理学](@article_id:307757)中的实际问题。

## 原理与机制

想象一条长而直的铁轨在夏日的阳光下暴晒。每一段钢轨，如果任其自然，都会变长一些。现在，如果我们把这些钢轨首尾相连地焊接在一起，不留任何缝隙，会发生什么？当太阳炙烤时，钢轨仍然*想要*膨胀，但相邻的钢轨却不允许它们这样做。这种内部的斗争，一种强大的生长欲望被不可移动的约束所挫败，催生了巨大的力。钢轨可能会屈曲成一条引人注目的蛇形曲线，这是我们称之为**热应力**现象的壮观而危险的展示。

要理解这一点，我们需要超越“热使物[体膨胀](@article_id:298146)”这一简单观念，去揭示温度、形状和力之间美妙的相互作用。由 Jean-Marie Duhamel 和 Franz Ernst Neumann 在19世纪提出的关键思想，是力学中最优雅的理念之一：我们必须分解应变。

### 膨胀的欲望与被压缩的抗拒

将材料形状的任何变化——拉伸、挤压、扭转——都看作是一种**应变**。杜哈梅-诺依曼定律告诉我们，我们观察到的总应变（可以用[张量](@article_id:321604) $\boldsymbol{\varepsilon}$ 表示）实际上是两个不同部分的总和：

$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{e} + \boldsymbol{\varepsilon}^{th}
$$

在这里，$\boldsymbol{\varepsilon}^{th}$ 是**[热应变](@article_id:366887)**。这是材料仅仅因为其温度发生变化而*想要*经历的应变。它是材料自然、无应力的膨胀或收缩的欲望。如果你让铁轨在阳光下自由膨胀，其全部观察到的应变就纯粹是[热应变](@article_id:366887)。

另一部分，$\boldsymbol{\varepsilon}^{e}$，是**[弹性应变](@article_id:368718)**。这是与内力相关的应变——由于材料被推或拉而发生的拉伸、挤压和剪切。至关重要的是，*只有*这部分弹性应变才会产生应力。

这种简单的分解功能极其强大。它告诉我们，如果一个材料可以完全按照其温度所指示的那样自由变形，那么[弹性应变](@article_id:368718) $\boldsymbol{\varepsilon}^{e}$ 为零，因此应力 $\boldsymbol{\sigma}$ 也为零。应力不是由加热引起的，而是由*约束*加热想要引起的膨胀所造成的。

这就引出了问题的核心。应力与[弹性应变](@article_id:368718)之间的关系由广义**[胡克定律](@article_id:310101)**所支配，我们可以写成 $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}^{e}$，其中 $\mathbb{C}$ 是材料的[刚度张量](@article_id:355554)。通过将我们的[应变分解](@article_id:365209)式重新[排列](@article_id:296886)为 $\boldsymbol{\varepsilon}^{e} = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{th}$，我们便得到了**杜哈梅-诺依曼定律**：

$$
\boldsymbol{\sigma} = \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{th})
$$

这个方程是[热弹性力学](@article_id:318851)的基础。它优雅地指出，应力是材料对其被迫进入的总变形 ($\boldsymbol{\varepsilon}$) 与其因温度而自然采取的变形 ($\boldsymbol{\varepsilon}^{th}$) 之间差异的弹性响应 [@problem_id:2898282] [@problem_id:2615069]。

### 描述膨胀：从简单标量到优雅[张量](@article_id:321604)

那么我们如何量化这种“膨胀的欲望”呢？对于在所有方向上都相同的简单材料——我们称之为**各向同性**材料——答案很简单。[热应变](@article_id:366887)在每个方向上都是相同的。我们可以用一个单一的标量数 $\alpha$，即我们熟悉的**线性热膨胀系数**来描述它。它的单位就是温度的倒数，比如 $\mathrm{K}^{-1}$ [@problem_id:2615069]。对于温度变化 $\Delta T$，任何方向上的[热应变](@article_id:366887)就是 $\alpha \Delta T$。

总体积变化与此相关但又有所不同。如果一个小立方体沿其三个轴的每一个轴都膨胀了 $\alpha \Delta T$，其体积变化近似为 $3\alpha \Delta T$。这就给出了线性膨胀系数 $\alpha$ 和体积[热膨胀系数](@article_id:304072) $\beta$ 之间的关系，对于[各向同性材料](@article_id:349861)，$\beta = 3\alpha$ [@problem_id:2928399] [@problem_id:2625928]。

但是，对于在所有方向上不尽相同的材料呢？一块木头横纹的膨胀远大于顺纹。一个石英单晶有其自身优选的膨胀方向。对于这些**各向异性**材料，单个标量 $\alpha$ 是不够的。我们需要一个更复杂的工具：**热膨胀系数[张量](@article_id:321604)** $\boldsymbol{\alpha}$（其分量为 $\alpha_{ij}$）。[热应变](@article_id:366887)则由 $\boldsymbol{\varepsilon}^{th} = \boldsymbol{\alpha} \Delta T$ 给出 [@problem_id:2615069]。

这个[张量](@article_id:321604)作为材料的一种属性，必须尊重材料的[内禀对称性](@article_id:347970)。这是一个深刻的思想，被称为诺依曼原理。
- 对于像木材这样的**[正交各向异性](@article_id:375808)**材料，它有三个相互垂直的对称面，当坐标轴与这些[对称轴](@article_id:356247)对齐时，其热膨胀[张量](@article_id:321604)是对角的。这意味着它有三个不同的主膨胀系数，但仅靠加热不会引起剪切 [@problem_id:2615069]。
- 对于像碳纤维复合材料或六方晶体这样的**横观各向同性**材料，它关于一个[轴对称](@article_id:352431)，只有两个独立的系数：沿该轴的膨胀系数 ($\alpha_{\parallel}$) 和在垂直于该轴的平面内的膨胀系数 ($\alpha_{\perp}$) [@problem_id:2615069] [@problem_id:2625928]。
- 对于**立方**晶体，其对称性非常高，以至于[张量](@article_id:321604)必须是各向同性的——它必须是单位[张量](@article_id:321604)的标量倍，这使我们回到单个系数 $\alpha$ 的情况 [@problem_id:2625928]。

这个[张量](@article_id:321604) $\boldsymbol{\alpha}$ 总是对称的 ($\alpha_{ij} = \alpha_{ji}$)，因为它所产生的应变张量必须是对称的。当我们旋转我们的观察[坐标系](@article_id:316753)时，它的分量会以一种精确的方式进行变换，其[主值](@article_id:368662)代表了最大和最小的膨胀系数 [@problem_id:2625928]。它是描述热膨胀[方向性](@article_id:329799)的[完美数](@article_id:641274)学对象。

### 热应力的诞生：当欲望撞上壁垒

现在我们可以回到我们的铁轨问题上。让我们将其建模为一个简单的各向同性杆。当它被加热 $\Delta T$ 但被牢固地固定住以至于完全不能膨胀时，会发生什么？这是**完全约束**的情况，意味着总应变为零：$\boldsymbol{\varepsilon} = \boldsymbol{0}$。

让我们将此代入杜哈梅-诺依曼定律：
$$
\boldsymbol{\sigma} = \mathbb{C} : (\boldsymbol{0} - \boldsymbol{\varepsilon}^{th}) = - \mathbb{C} : (\boldsymbol{\alpha} \Delta T)
$$
材料仍然有其[热膨胀](@article_id:297878)的欲望 ($\boldsymbol{\varepsilon}^{th} = \alpha \Delta T \boldsymbol{I}$)，但由于总应变为零，[弹性应变](@article_id:368718)必须为 $\boldsymbol{\varepsilon}^{e} = \boldsymbol{0} - \boldsymbol{\varepsilon}^{th} = -\alpha \Delta T \boldsymbol{I}$。材料在所有方向上都受到弹性压缩，就好像它被一个越来越紧的虎钳夹住一样。这种压缩性[弹性应变](@article_id:368718)产生了应力。

对于[各向同性材料](@article_id:349861)，在进行[张量](@article_id:321604)数学运算后，出现了一个优美而简单的结果 [@problem_id:2898282] [@problem_id:2701587]。产生的应力是纯[静水压力](@article_id:302068)：
$$
\boldsymbol{\sigma} = -3K\alpha\Delta T \boldsymbol{I}
$$
这里，$\boldsymbol{I}$ 是单位[张量](@article_id:321604)，$K$ 是**[体积模量](@article_id:320473)**，它衡量材料抵[抗体](@article_id:307222)积变化的能力。这个方程揭示性极强。它告诉我们，产生的压应力与温升 ($\Delta T$)、材料的膨胀欲望 ($\alpha$) 及其抗压缩的顽固性 ($K$) 成正比 [@problem_id:2925011]。这就是为什么像钢这样具有高体积模量的材料，当其[热膨胀](@article_id:297878)受阻时，能够产生巨大的应力。

### 问题的[热力学](@article_id:359663)核心

杜哈梅-诺依曼定律不仅仅是一个巧妙的猜测；它深深植根于热力学定律。[热弹性](@article_id:318851)材料的行为可以由一个单一的热力学势——**[亥姆霍兹自由能](@article_id:296896)** $\psi(\boldsymbol{\varepsilon}, T)$ 完全描述。这个函数代表在给定应变和温度下可用于做功的能量。

应力和熵就是这个势的[导数](@article_id:318324)：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} \quad \text{and} \quad s = -\frac{\partial \psi}{\partial T}
$$
通过假设一个合适的二次形式的 $\psi$ 来解释弹性能及其与温度的耦合，人们可以从第一性原理推导出整个杜哈梅-诺依曼框架 [@problem_id:2925011] [@problem_id:2625928]。

这种[热力学](@article_id:359663)观点揭示了更深层次的联系。例如，你是否曾想过为什么一种物质的[比热](@article_id:297374)可以有不同的值？我们有定[压比](@article_id:298149)热 ($c_p$) 和定容比热 ($c_v$)。对于固体也存在类似的区分：定应力[热容](@article_id:340019) ($c_{\boldsymbol{\sigma}}$) 和定应变[热容](@article_id:340019) ($c_{\boldsymbol{\varepsilon}}$)。

想象一下加热一个固体。如果应力保持恒定（例如，零应力，自由膨胀），你增加的所有热量都用于提高其温度。但如果应变保持恒定（完全约束情况），材料就不能膨胀。当你增加热量时，你不仅在提高它的温度，还在以[热应力](@article_id:360016)的形式累积弹性应变能。你的一部分热能被储存为机械势能！这意味着你需要增加更多的热量才能达到相同的温升。因此，$c_{\boldsymbol{\sigma}}$ 总是大于 $c_{\boldsymbol{\varepsilon}}$。这个差异并非任意的；它可以直接从[亥姆霍兹自由能](@article_id:296896)中推导出来，对于各向同性固体，它由一个极其紧凑的公式给出 [@problem_id:2924972]：
$$
c_{\boldsymbol{\sigma}} - c_{\boldsymbol{\varepsilon}} = 9\alpha^2 K T
$$
这个优美的结果将[热容](@article_id:340019)的差异与控制[热应力](@article_id:360016)的完全相同的参数直接联系起来：膨胀系数 ($\alpha$)、体积模量 ($K$) 和绝对温度 ($T$)。这是力学与[热力学](@article_id:359663)深刻统一的明证。

### 双向互动：热与变形的完整舞蹈

我们的旅程展示了温度如何影响物体的机械状态。但反过来是否也成立呢？变形会影响温度吗？当然会。这被称为**[热弹性耦合](@article_id:362753)**。当你快速压缩气体时，它会升温。同样的事情也发生在固体中，尽管效果通常小得多。快速膨胀会导致轻微的冷却。

这种[双向耦合](@article_id:357690)意味着，在最一般的情况下，力学问题和热学问题是不可分割的。一个[热弹性](@article_id:318851)体的完整描述涉及两个耦合方程 [@problem_id:2701601]：
1.  **[力学平衡](@article_id:309249)方程：** $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \rho \ddot{\boldsymbol{u}}$，其中应力 $\boldsymbol{\sigma}$ 取决于温度。
2.  **热传导方程：** $\rho c \dot{T} = \nabla \cdot (\boldsymbol{k} \nabla T) - 3K\alpha T_0 \text{tr}(\dot{\boldsymbol{\varepsilon}}) + r$，其中包括一个与[体积应变率](@article_id:336168) $\text{tr}(\dot{\boldsymbol{\varepsilon}})$ 成正比的热源/汇项。

项 $-3K\alpha T_0 \text{tr}(\dot{\boldsymbol{\varepsilon}})$ 就是[热弹性耦合](@article_id:362753)项。它在数学上捕捉到了变化的体积就像一个热源或热汇这一事实。

在许[多工](@article_id:329938)程情况下，这个耦合项与[热方程](@article_id:304863)中的其他项相比很小。这使得一个重大的简化成为可能，即所谓的**[非耦合热弹性力学](@article_id:374628)** [@problem_id:2928430]。在这种方法中，我们直接从[热方程](@article_id:304863)中去掉耦合项。这“[解耦](@article_id:641586)”了问题：
1.  首先，我们求解标准的[热传导方程](@article_id:373663) $\rho c \dot{T} = \nabla \cdot (\boldsymbol{k} \nabla T) + r$，以找出物体中各处的温度场 $T(\boldsymbol{x}, t)$。
2.  然后，我们将这个温度场作为已知输入代入力学问题，并使用杜哈梅-诺依曼定律求解位移和应力。

这条单行道——即温度影响力学，但力学不影响温度——对于大多数准静态问题来说是一个极好的近似。它构成了工程师分析从发动机部件到微电子芯片等各种事物中热应力的基础，而所有这些都始于将应变分为两部分的简单而优雅的思想：一部分源于热，另一部分源于力 [@problem_id:2692164]。