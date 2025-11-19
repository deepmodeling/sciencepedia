## 引言
在现代工程与科学研究中，准确预测材料在极端载荷下的行为是设计的关键，尤其是在涉及[大变形](@entry_id:167243)和[刚体转动](@entry_id:191086)的复杂场景中，例如金属成型、车辆碰撞或[生物组织力学](@entry_id:194951)。对于许多材料而言，其力学响应不仅取决于当前的变形状态，还依赖于变形的速率。为了描述这种[路径依赖](@entry_id:138606)和率相关的行为，[连续介质力学](@entry_id:155125)引入了率形式的[本构方程](@entry_id:138559)，它直接关联了应力的变化率与变形的速率。

然而，这一看似直接的方法隐藏着一个深刻的挑战：如何定义一个在物理上具有普遍有效性的“应力率”？我们面临的核心问题是**物质[坐标系](@entry_id:156346)无关性原理**（亦称[客观性原理](@entry_id:185412)），它要求物理定律必须对所有观察者（无论其如何平移或旋转）都具有相同的形式。令人意外的是，最直观的应力时间导数——[物质时间导数](@entry_id:190892)——并不满足这一基本原理，这意味着使用它会导致物理上荒谬的预测，例如在纯刚体旋转中产生虚假的应力。

为了解决这一根本性的知识鸿沟，本文系统地介绍了**客观应力率**的概念。我们将通过三个章节的深入探讨，带领读者全面掌握这一高级[固体力学](@entry_id:164042)中的核心主题。
- 在“**原理与机制**”中，我们将从物质[坐标系](@entry_id:156346)无关性原理出发，严格证明为何需要客观应力率，并详细阐述如何通过随动导数的思想构建出Jaumann率、[Green-Naghdi率](@entry_id:190839)等多种关键的[客观率](@entry_id:198692)。
- 在“**应用与跨学科连接**”中，我们将探讨这些理论在实际问题中的应用和后果，比较不同[客观率](@entry_id:198692)在[亚弹性](@entry_id:204371)、[弹塑性](@entry_id:193198)和有限元计算中所带来的不同预测结果，并揭示其与[流变学](@entry_id:138671)、[损伤力学](@entry_id:178377)等领域的深刻联系。
- 最后，在“**动手实践**”部分，通过一系列精心设计的计算练习，读者将有机会将理论知识转化为解决实际问题的能力。

通过本文的学习，你将不仅理解客观应力率的数学形式，更将洞悉其背后的物理思想，为进行高水平的[非线性力学](@entry_id:178303)分析和研究奠定坚实的基础。

## 原理与机制

在处理经历大变形和[刚体转动](@entry_id:191086)的材料时，建立能够准确描述应力演化的本构关系是[连续介质力学](@entry_id:155125)的核心挑战之一。当材料的响应速率依赖于变形速率时（例如在[弹塑性](@entry_id:193198)或粘弹性中），我们必须使用应力率。然而，并非任何时间导数都适用于此目的。[本构方程](@entry_id:138559)必须遵守一条基本物理原理——**物质[坐标系](@entry_id:156346)无关性原理**，也称**[客观性原理](@entry_id:185412)**。该原理要求物理定律的形式不应依赖于观察者。本章将深入探讨这一原理，阐明为何简单的[物质时间导数](@entry_id:190892)不满足该要求，并系统介绍为满足此原理而构建的各种**客观应力率**的原理和机制。

### 物质[坐标系](@entry_id:156346)无关性原理

物质[坐标系](@entry_id:156346)无关性原理（或称[客观性原理](@entry_id:185412)）指出，[本构方程](@entry_id:138559)——即描述材料行为的数学关系——必须在所有（[刚体运动](@entry_id:193355)的）观察者看来都具有相同的形式。想象两位观察者，一位处于静止的[实验室坐标系](@entry_id:166991)，另一位在相对于[实验室坐标系](@entry_id:166991)进行任意时变平移和旋转的[坐标系](@entry_id:156346)中。两位观察者测量的物理量（如速度或应力）的数值分量可能不同，但描述这些量之间关系的物理定律本身必须是相同的。

数学上，我们将两个观察者联系起来的变换称为**叠加[刚体运动](@entry_id:193355)**。如果一个质点在“静止”观察者[坐标系](@entry_id:156346)中的位置是 $\boldsymbol{x}$，那么在“运动”观察者[坐标系](@entry_id:156346)中的位置 $\boldsymbol{x}^{\ast}$ 由下式给出：
$$
\boldsymbol{x}^{\ast}(t) = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}(t)
$$
其中 $\boldsymbol{c}(t)$ 是一个时变平移向量，$\boldsymbol{Q}(t)$ 是一个时变**正常正交张量**（即 $\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q} = \boldsymbol{I}$ 且 $\det(\boldsymbol{Q})=1$），代表刚体旋转。

根据这一原理，不同类型的物理量在观察者变换下具有特定的变换规则。
- **客观标量**（如密度 $\rho$ 或温度 $T$）在变换下保持不变：$\rho^{\ast} = \rho$。
- **客观向量**（如力 $\boldsymbol{f}$）随观察者[坐标系](@entry_id:156346)旋转：$\boldsymbol{f}^{\ast} = \boldsymbol{Q}\boldsymbol{f}$。
- **客观[二阶张量](@entry_id:199780)**（如柯西应力 $\boldsymbol{\sigma}$）也随之旋转，其变换规则为：
$$
\boldsymbol{T}^{\ast} = \boldsymbol{Q}\boldsymbol{T}\boldsymbol{Q}^{\mathsf{T}}
$$
这个变换规则是客观张量的定义性特征 [@problem_id:2666106]。一个本构关系若要满足物质[坐标系](@entry_id:156346)无关性，其所涉及的所有张量都必须是客观的，并且其函数形式必须是**各向同性**的，这意味着函数形式本身不因[坐标系](@entry_id:156346)的旋转而改变 [@problem_id:2666103]。具体来说，对于一个形如 $\boldsymbol{\sigma} = \mathcal{H}(\boldsymbol{d})$ 的[本构关系](@entry_id:186508)，其中 $\boldsymbol{d}$ 是变形率张量，该原理要求对于任意正常的正交张量 $\boldsymbol{Q}$，函数 $\mathcal{H}$ 必须满足：
$$
\mathcal{H}(\boldsymbol{Q}\boldsymbol{d}\boldsymbol{Q}^{\mathsf{T}}) = \boldsymbol{Q}\mathcal{H}(\boldsymbol{d})\boldsymbol{Q}^{\mathsf{T}}
$$

### 率相关本构模型的挑战：[物质时间导数](@entry_id:190892)的非客观性

许多先进的材料模型，如 hypoelasticity（[亚弹性](@entry_id:204371)）和[弹塑性](@entry_id:193198)模型，都属于率相关[本构模型](@entry_id:174726)。这类模型描述了应力的“率”与变形的“率”之间的关系，通常形式为 $\overset{\circ}{\boldsymbol{\sigma}} = \mathcal{H}(\boldsymbol{D})$，其中 $\boldsymbol{D}$ 是变形率张量，$\overset{\circ}{\boldsymbol{\sigma}}$ 是某种应力率。

一个自然而然的问题是：我们是否可以使用最简单的应力率，即柯西应力 $\boldsymbol{\sigma}$ 的**[物质时间导数](@entry_id:190892)** $\dot{\boldsymbol{\sigma}}$？为了回答这个问题，我们必须检验 $\dot{\boldsymbol{\sigma}}$ 是否是一个客观张量，即它是否遵循 $\boldsymbol{T}^{\ast} = \boldsymbol{Q}\boldsymbol{T}\boldsymbol{Q}^{\mathsf{T}}$ 的变换规则。

我们从柯西应力张量的客观变换规则出发：
$$
\boldsymbol{\sigma}^{\ast} = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}
$$
对时间 $t$ 求[物质导数](@entry_id:172646)，并应用乘法法则，我们得到：
$$
\dot{\boldsymbol{\sigma}}^{\ast} = \frac{d}{dt}(\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}) = \dot{\boldsymbol{Q}}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{Q}\boldsymbol{\sigma}\dot{\boldsymbol{Q}}^{\mathsf{T}}
$$
为了更好地理解这个表达式，我们引入**观察者[自旋张量](@entry_id:187346)** $\boldsymbol{\Omega} = \dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}}$。由于 $\boldsymbol{Q}$ 是正交的，$\boldsymbol{\Omega}$ 是一个[斜对称张量](@entry_id:199349) ($\boldsymbol{\Omega}^{\mathsf{T}} = -\boldsymbol{\Omega}$)。利用 $\boldsymbol{Q}$ 的正交性和 $\boldsymbol{\Omega}$ 的定义，上式可以改写为：
$$
\dot{\boldsymbol{\sigma}}^{\ast} = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}
$$
这个结果至关重要 [@problem_id:2905931]。它表明 $\dot{\boldsymbol{\sigma}}^{\ast}$ 并不等于 $\boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}}$。多出来的两项 $\boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}$ 是由观察者自身的旋转速率 $\dot{\boldsymbol{Q}}$ 引起的。除非观察者没有旋转（$\boldsymbol{\Omega}=\boldsymbol{0}$）或者 $\boldsymbol{\Omega}$ 与 $\boldsymbol{\sigma}^{\ast}$ 可交换（通常不成立），否则 $\dot{\boldsymbol{\sigma}}$ 就不是一个客观张量。

使用非客观的 $\dot{\boldsymbol{\sigma}}$ 会导致物理上荒谬的预测。考虑一个处于[初始应力](@entry_id:750652)状态 $\boldsymbol{\sigma}_0$ 的物体只进行刚体旋转，不发生任何变形。在这种情况下，变形率张量 $\boldsymbol{D}$ 为零。如果采用一个（不正确的）[亚弹性](@entry_id:204371)本构模型 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$，该模型将预测 $\dot{\boldsymbol{\sigma}} = \boldsymbol{0}$，意味着在实验室坐标系中测量的应力分量将保持恒定。然而，从物理上看，材料内部的应力状态是随材料一同旋转的。因此，正确的[应力张量](@entry_id:148973)应该是 $\boldsymbol{\sigma}(t) = \boldsymbol{R}(t)\boldsymbol{\sigma}_0\boldsymbol{R}(t)^{\mathsf{T}}$，其中 $\boldsymbol{R}(t)$ 是描述材料旋转的[旋转张量](@entry_id:191990)。这个不正确的模型无法预测应力的旋转，从而在材料旋转时产生了虚假的、非物理的应力 [@problem_id:2666090]。

### [运动学](@entry_id:173318)张量的客观性

为了构建客观的应力率，我们首先需要系统地审视本构关系中常见的[运动学](@entry_id:173318)张量的客观性 [@problem_id:2905934]。

- **变形梯度** $\boldsymbol{F}$：定义为 $\boldsymbol{F} = \partial\boldsymbol{x}/\partial\boldsymbol{X}$，它将参考构型中的向量映射到当前构型。在叠加[刚体运动](@entry_id:193355)下，它的变换规则是 $\boldsymbol{F}^{\ast} = \boldsymbol{Q}\boldsymbol{F}$。这不符合客观二阶[空间张量](@entry_id:185799)的变换规则，因此 $\boldsymbol{F}$ 不是一个客观的[空间张量](@entry_id:185799)。它是一个“两点张量”。

- **[速度梯度](@entry_id:261686)** $\boldsymbol{L}$：定义为 $\boldsymbol{L} = \nabla\boldsymbol{v}$，其变换规则为 $\boldsymbol{L}^{\ast} = \boldsymbol{Q}\boldsymbol{L}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}$。由于存在附加项 $\boldsymbol{\Omega}$，速度梯度 $\boldsymbol{L}$ 不是客观的。

- **变形率张量** $\boldsymbol{D}$：作为速度梯度的对称部分，$\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^{\mathsf{T}})$。其变换规则为：
$$
\boldsymbol{D}^{\ast} = \boldsymbol{Q}\boldsymbol{D}\boldsymbol{Q}^{\mathsf{T}}
$$
附加的自旋项在对称化过程中被消除了。因此，**$\boldsymbol{D}$ 是一个客观张量**。这是它能够被广泛用于[本构方程](@entry_id:138559)右侧（作为“驱动力”）的根本原因。

- **[自旋张量](@entry_id:187346)** $\boldsymbol{W}$：作为[速度梯度](@entry_id:261686)的斜对称部分，$\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^{\mathsf{T}})$。其变换规则与 $\boldsymbol{L}$ 类似，但形式更为明确：
$$
\boldsymbol{W}^{\ast} = \boldsymbol{Q}\boldsymbol{W}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}
$$
$\boldsymbol{W}$ 显然不是客观的。然而，它的非客观性恰好与观察者自旋 $\boldsymbol{\Omega}$ 以一种简单的加和方式耦合。这一特性正是构建客观应力率的关键。

### 构建客观应力率：随动导数

我们已经看到，$\dot{\boldsymbol{\sigma}}$ 的非客观性源于附加项 $[\boldsymbol{\Omega}, \boldsymbol{\sigma}^{\ast}] = \boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}$。解决问题的思路是通过引入一个修正项来抵消这个非客观部分。这引出了**随动导数**（Corotational Derivative）的概念。

一个随动导数可以被理解为在一个随材料旋转的[坐标系](@entry_id:156346)中观察到的张量时间导数。其一般形式为：
$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\boldsymbol{\omega} - \boldsymbol{\omega}\boldsymbol{\sigma}
$$
其中 $\boldsymbol{\omega}$ 是一个被我们选择用来定义该导数的斜对称[自旋张量](@entry_id:187346)。

为了使这个新定义的应力率 $\overset{\circ}{\boldsymbol{\sigma}}$ 成为客观的，即满足 $\overset{\circ}{\boldsymbol{\sigma}}{}^{\ast} = \boldsymbol{Q}\overset{\circ}{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}}$，所选择的[自旋张量](@entry_id:187346) $\boldsymbol{\omega}$ 必须满足一个特定的变换规则。通过代数推导可以证明，这个条件是 [@problem_id:2666126] [@problem_id:2905949]：
$$
\boldsymbol{\omega}^{\ast} = \boldsymbol{Q}\boldsymbol{\omega}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}
$$
这个条件意味着，我们必须选择一个“非客观”的[自旋张量](@entry_id:187346) $\boldsymbol{\omega}$，其非客观部分正好能抵消掉 $\dot{\boldsymbol{\sigma}}$ 变换规则中的非客观项。幸运的是，我们在上一节中已经找到了这样的张量。

不同的客观应力率对应于对随动[坐标系](@entry_id:156346)自旋 $\boldsymbol{\omega}$ 的不同选择。以下是一些最常用的客观应力率：

- **[Jaumann 率](@entry_id:185572)**（或 Zaremba-[Jaumann 率](@entry_id:185572)）($\boldsymbol{\sigma}^{\nabla J}$):
这是最常见的选择之一，它选取材料自身的[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 作为随动自旋，即 $\boldsymbol{\omega} = \boldsymbol{W}$。我们已知 $\boldsymbol{W}$ 的变换规则是 $\boldsymbol{W}^{\ast} = \boldsymbol{Q}\boldsymbol{W}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}$，正好满足条件。因此，[Jaumann 率](@entry_id:185572)是客观的：
$$
\boldsymbol{\sigma}^{\nabla J} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\boldsymbol{W} - \boldsymbol{W}\boldsymbol{\sigma}
$$

- **Green-Naghdi 率** ($\boldsymbol{\sigma}^{\nabla G}$):
此率选择变形梯度极分解 $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$ 中[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 的自旋 $\boldsymbol{\omega}_{\mathrm{GN}} = \dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}}$ 作为随动自旋。可以证明，$\boldsymbol{\omega}_{\mathrm{GN}}$ 也满足变换规则 $\boldsymbol{\omega}_{\mathrm{GN}}^{\ast} = \boldsymbol{Q}\boldsymbol{\omega}_{\mathrm{GN}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}$，因此 Green-Naghdi 率也是客观的 [@problem_id:2905949]。
$$
\boldsymbol{\sigma}^{\nabla G} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\boldsymbol{\omega}_{\mathrm{GN}} - \boldsymbol{\omega}_{\mathrm{GN}}\boldsymbol{\sigma}
$$

- **Truesdell 率** ($\boldsymbol{\sigma}^{\nabla T}$):
Truesdell 率的结构与简单的随动导数不同，但它同样是客观的。其定义为：
$$
\boldsymbol{\sigma}^{\nabla T} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^{\mathsf{T}} + (\mathrm{tr}(\boldsymbol{D}))\boldsymbol{\sigma}
$$
通过直接的变换分析可以验证其客观性 [@problem_id:2905949]。

至此，我们已经构建了多种客观应力率。它们的一个共同优点是，对于仅经历刚体旋转而无变形的物体，所有这些客观应力率都为零 [@problem_id:2905958]。这解决了之前提到的使用 $\dot{\boldsymbol{\sigma}}$ 产生的悖论，并正确地反映了在这种情况下，应力状态只是被动地随材料旋转，其在随动[坐标系](@entry_id:156346)中的“变化率”为零。

### 不同客观应力率的物理意义

既然存在多种客观应力率，我们自然会问：选择哪一种有关系吗？答案是肯定的，不同的客观应力率在物理上代表了不同的假设，并会导致不同的应力预测，尤其是在复杂的加载路径下。

我们来比较一下 [Jaumann 率](@entry_id:185572)和 Green-Naghdi 率。它们之间的差异可以表示为 [@problem_id:2666116]：
$$
\boldsymbol{\sigma}^{\nabla G} - \boldsymbol{\sigma}^{\nabla J} = \boldsymbol{\sigma}(\boldsymbol{\omega}_{\mathrm{GN}} - \boldsymbol{W}) - (\boldsymbol{\omega}_{\mathrm{GN}} - \boldsymbol{W})\boldsymbol{\sigma}
$$
这个差异是应力张量 $\boldsymbol{\sigma}$ 与自旋差 $(\boldsymbol{\omega}_{\mathrm{GN}} - \boldsymbol{W})$ 的[交换子](@entry_id:158878)。一个关键的推论是，在应力的[主轴](@entry_id:172691)[坐标系](@entry_id:156346)中，这个差异张量是纯粹非对角的。这意味着，在一个形如 $\overset{\circ}{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$ 的[亚弹性模型](@entry_id:184632)中，使用 [Jaumann 率](@entry_id:185572)还是 Green-Naghdi 率，将得到完全相同的[主应力](@entry_id:176761)**大小**的演化率，但会预测出不同的[主应力](@entry_id:176761)**方向**的旋转率。

现在比较 [Jaumann 率](@entry_id:185572)和 Truesdell 率。它们之间的差异为 [@problem_id:2666095]：
$$
\boldsymbol{\sigma}^{\nabla T} - \boldsymbol{\sigma}^{\nabla J} = (\mathrm{tr}(\boldsymbol{D}))\boldsymbol{\sigma} - (\boldsymbol{D}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{D})
$$
这个差异依赖于变形率张量 $\boldsymbol{D}$ 和[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$。与前一个比较不同，这个差异张量通常具有非零的对角分量。因此，即使对于各向同性材料，在相同的变形率 $\boldsymbol{D}$ 下，使用这两种率也会导致主应力大小和方向的演化都出现差异。

总之，客观应力率的选择并非无足轻重，它本身就是[本构建模](@entry_id:183370)的一部分。不存在一个“绝对正确”的客观应力率。对于纯剪切等简单变形，许多率的预测结果相似；但在涉及大转动和非[比例加载](@entry_id:191744)的复杂路径下，不同率之间的差异会变得非常显著。因此，选择哪种客观应力率，应基于实验数据和所要描述的特定材料行为来决定。