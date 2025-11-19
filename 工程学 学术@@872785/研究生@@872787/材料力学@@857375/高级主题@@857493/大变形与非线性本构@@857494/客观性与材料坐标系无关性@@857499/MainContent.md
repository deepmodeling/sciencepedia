## 引言
在[连续介质力学](@entry_id:155125)中，描述[材料力学](@entry_id:201885)行为的[本构关系](@entry_id:186508)是理论的基石。为了确保这些物理定律的普适性，一个不容置疑的基本公理是：物理定律必须独立于观测者。这意味着，无论观测者自身处于何种运动状态，材料的内在物理响应都应保持不变。这一核心思想被称为**物质[标架无关性原理](@entry_id:200995) (Principle of Material Frame Indifference, PMFI)**，或更简洁地称为**[客观性原理](@entry_id:185412) (Principle of Objectivity)**。它解决了如何确保我们描述的物理规律是物质的固有属性，而非观测视角的产物这一根本问题。

本文旨在对[客观性原理](@entry_id:185412)进行一次系统而深入的剖析。我们将从其数学基础出发，逐步揭示它[对力](@entry_id:159909)学理论的深远影响。

- 在“**原理与机制**”一章中，我们将建立观测者变换的数学框架，严格区分客观与非客观的物理量，并阐明该原理对本构函数形式的根本性约束。
- 接下来，在“**应用与跨学科交叉**”一章，我们将展示这一原理如何指导从弹性到塑性等各类材料模型的构建，并探讨其在[计算力学](@entry_id:174464)和基础物理学中的深远影响。
- 最后，“**动手实践**”部分将通过具体计算问题，让您亲身体验非客观模型如何导致物理谬误，从而巩固对理论的理解。

通过学习本文，您将能够掌握这一强大工具，从而在进行[材料建模](@entry_id:751724)和力学分析时，确保理论的自洽性与物理的真实性。

## 原理与机制

在连续介质力学中，[本构关系](@entry_id:186508)是描述材料物理行为的核心。一个基本公理是，这些物理定律必须独立于观测者。换言之，无论观测者如何运动，材料的内在响应（例如，特定变形状态下的应力）都应该是相同的。这一基本思想被称为**物质[标架无关性原理](@entry_id:200995) (Principle of Material Frame Indifference, PMFI)**，或简称为**[客观性原理](@entry_id:185412) (Principle of Objectivity)**。本章将系统地阐述该原理的数学框架、其对[运动学](@entry_id:173318)量和[本构方程](@entry_id:138559)的深刻影响，并澄清一些常见的混淆概念。

### 观测者与标架无关性的数学框架

在经典力学中，我们假设存在一个绝对的、全局的“背景”空间，通常是一个[欧几里得空间](@entry_id:138052)。一个**观测者**由一个用于度量该空间中点的位置和运动的参考标架来定义。不同的观测者可以相对于彼此进行[刚体运动](@entry_id:193355)。因此，一个“观测者变换”被数学模型化为一个依赖于时间的[刚体运动](@entry_id:193355)，它将一个观测者（例如，一个“静止”的实验室标架）测量的空间点 $\mathbf{x}$ 映射到另一个观测者（一个“运动”的标架）测量的点 $\mathbf{x}^*$。

这种变换在任意时刻 $t$ 都可以表示为：
$$ \mathbf{x}^* = \mathbf{Q}(t) \mathbf{x} + \mathbf{c}(t) $$
其中 $\mathbf{c}(t) \in \mathbb{R}^3$ 是一个依赖于时间的平移向量，而 $\mathbf{Q}(t)$ 是一个依赖于时间的正交张量。正交性，即 $\mathbf{Q}^T\mathbf{Q}=\mathbf{I}$（$\mathbf{I}$ 为单位张量），确保了点之间的距离在变换下保持不变。我们进一步要求 $\det(\mathbf{Q})=1$，这意味着变换保持了空间的定向（即，[右手坐标系](@entry_id:166669)仍然是[右手坐标系](@entry_id:166669)）。满足这些条件的张量 $\mathbf{Q}(t)$ 属于**[三维特殊正交群](@entry_id:138200)**，记为 $\mathrm{SO}(3)$。

这些保持定向的刚体运动构成了一个数学群，即**三维[特殊欧几里得群](@entry_id:139383)** $\mathrm{SE}(3)$。该群的元素是偶对 $(\mathbf{Q}, \mathbf{c})$，其中 $\mathbf{Q} \in \mathrm{SO}(3)$ 且 $\mathbf{c} \in \mathbb{R}^3$。群的复合运算，对应于连续进行两次观测者变换，其法则为：
$$ (\mathbf{Q}_2, \mathbf{c}_2) \cdot (\mathbf{Q}_1, \mathbf{c}_1) = (\mathbf{Q}_2 \mathbf{Q}_1, \mathbf{c}_2 + \mathbf{Q}_2 \mathbf{c}_1) $$
该群的单位元是 $(\mathbf{I}, \mathbf{0})$，它代表了没有运动的变换 [@problem_id:2906337]。值得注意的是，[牛顿力学](@entry_id:162125)框架下的一个基本假设是存在[绝对时间](@entry_id:265046)，所有观测者共享同一个时间，即 $t^*=t$。

### 客观场：标量、矢量和张量

物质[标架无关性原理](@entry_id:200995)要求物理量和描述它们之间关系的本构律不能依赖于观测者的选择。一个满足此要求的物理量被称为**客观的 (objective)** 或**标架无关的 (frame-indifferent)**。

对于一个在空间点 $(\mathbf{x}, t)$ 定义的物理场，其客观性要求该场在不同观测者标架下的值之间存在确定的关系。

一个**客观[标量场](@entry_id:151443)** $\phi(\mathbf{x}, t)$，例如密度或温度，其值在给定的物理点上不应随观测者而改变。这意味着在新标架中，在点 $\mathbf{x}^*$ 的值 $\phi^*$ 应该等于旧标架中对应物理点 $\mathbf{x}$ 的值 $\phi$：
$$ \phi^*(\mathbf{x}^*, t) = \phi(\mathbf{x}, t) $$
为了将 $\phi^*$ 表示为 $\mathbf{x}^*$ 的函数，我们需要将 $\mathbf{x}$ 用 $\mathbf{x}^*$ 表示。由 $\mathbf{x}^* = \mathbf{Q}(t) \mathbf{x} + \mathbf{c}(t)$ 可得 $\mathbf{x} = \mathbf{Q}(t)^T (\mathbf{x}^* - \mathbf{c}(t))$。因此，客观标量的完整变换法则是：
$$ \phi^*(\mathbf{x}^*, t) = \phi(\mathbf{Q}(t)^T (\mathbf{x}^* - \mathbf{c}(t)), t) $$
[@problem_id:2906337]

一个**客观矢量场** $\mathbf{a}(\mathbf{x}, t)$，例如作用在单位体积上的体力，其方向和大小的物理实在性不应改变，但其分量会随着观测者[坐标系](@entry_id:156346)的旋转而改变。如果 $\mathbf{a}$ 是旧标架中的矢量，$\mathbf{a}^*$ 是新标架中的矢量，它们通过[旋转张量](@entry_id:191990) $\mathbf{Q}(t)$ 联系起来：
$$ \mathbf{a}^*(\mathbf{x}^*, t) = \mathbf{Q}(t) \mathbf{a}(\mathbf{x}, t) $$
其中 $\mathbf{x}$ 和 $\mathbf{x}^*$ 依然由[坐标变换](@entry_id:172727)公式关联 [@problem_id:2906337] [@problem_id:2906326]。这个法则可以通过考虑连接两个空间点的矢量 $\mathbf{v} = \mathbf{x}_2 - \mathbf{x}_1$ 的变换来推导，平移项 $\mathbf{c}(t)$ 会被抵消。

一个**客观二阶张量场** $\mathbf{T}(\mathbf{x}, t)$，例如柯西应力张量 $\boldsymbol{\sigma}$，它将一个空间矢量（如[单位法向量](@entry_id:178851) $\mathbf{n}$）线性映射到另一个空间矢量（如[面力矢量](@entry_id:189429) $\mathbf{t}_{\mathbf{n}}$）。这个物理关系 $\mathbf{t}_{\mathbf{n}} = \mathbf{T}\mathbf{n}$ 必须在所有标架中都成立。在新标架中，我们有 $\mathbf{t}_{\mathbf{n}}^* = \mathbf{T}^*\mathbf{n}^*$。由于 $\mathbf{t}_{\mathbf{n}}$ 和 $\mathbf{n}$ 都是客观矢量，它们遵循 $\mathbf{t}_{\mathbf{n}}^* = \mathbf{Q}\mathbf{t}_{\mathbf{n}}$ 和 $\mathbf{n}^* = \mathbf{Q}\mathbf{n}$ 的变换法则。代入可得 $\mathbf{Q}\mathbf{t}_{\mathbf{n}} = \mathbf{T}^*(\mathbf{Q}\mathbf{n})$，即 $\mathbf{Q}(\mathbf{T}\mathbf{n}) = (\mathbf{T}^*\mathbf{Q})\mathbf{n}$。由于这对任意矢量 $\mathbf{n}$ 都成立，我们得到[张量变换法则](@entry_id:185176)：
$$ \mathbf{T}^*(\mathbf{x}^*, t) = \mathbf{Q}(t) \mathbf{T}(\mathbf{x}, t) \mathbf{Q}(t)^T $$
[@problem_id:2906337] [@problem_id:2906326]

在此，区分**客观性 (objectivity)** 和**[协变](@entry_id:634097)性 (covariance)** 至关重要。客观性是施加在**单个物理场**上的属性，规定了其在不同观测者下的测量值如何关联。而协变性是**整个物理定律或控制方程**的属性，它要求方程的数学形式在所有允许的观测者变换下保持不变。一个协变方程可能包含非客观的量（例如，牛顿第二定律 $\mathrm{div}\,\boldsymbol{\sigma} + \rho\mathbf{b} = \rho\mathbf{a}$ 包含非客观的加速度 $\mathbf{a}$），但方程中所有项的变换性质必须以一种能保持方程结构不变的方式组合在一起 [@problem_id:2906326]。

### 非客观的[运动学](@entry_id:173318)量

并非所有物理中常见的量都是客观的。事实上，许多基本的运动学量都依赖于观测者。

**[速度场](@entry_id:271461)** $\mathbf{v}$ 是一个典型的例子。物质点在旧标架中的轨迹为 $\mathbf{x}(t)$，其速度为 $\mathbf{v} = \dot{\mathbf{x}}(t)$。在新标架中，同一物质点的轨迹为 $\mathbf{x}^*(t) = \mathbf{Q}(t)\mathbf{x}(t) + \mathbf{c}(t)$。对时间求导，使用乘法法则，我们得到新标架中的速度 $\mathbf{v}^*$：
$$ \mathbf{v}^* = \dot{\mathbf{x}}^* = \dot{\mathbf{Q}}(t)\mathbf{x}(t) + \mathbf{Q}(t)\dot{\mathbf{x}}(t) + \dot{\mathbf{c}}(t) = \dot{\mathbf{Q}}\mathbf{x} + \mathbf{Q}\mathbf{v} + \dot{\mathbf{c}} $$
这个变换法则包含额外的项：$\dot{\mathbf{c}}$（观测者标架的平移速度）和 $\dot{\mathbf{Q}}\mathbf{x}$（由观测者标架的旋转引起的[相对速度](@entry_id:178060)）。这表明[速度场](@entry_id:271461) $\mathbf{v}$ 并非一个客观矢量 [@problem_id:2906337]。

**[空间速度梯度](@entry_id:187198)** $\mathbf{L} = \nabla\mathbf{v}$ 同样不是客观的。通过[链式法则](@entry_id:190743)对其变换法则进行推导，可以得到：
$$ \mathbf{L}^* = \mathbf{Q}\mathbf{L}\mathbf{Q}^T + \dot{\mathbf{Q}}\mathbf{Q}^T $$
我们定义**观测者[自旋张量](@entry_id:187346)** $\boldsymbol{\Omega}(t) := \dot{\mathbf{Q}}(t)\mathbf{Q}^T(t)$，这是一个[反对称张量](@entry_id:199349)，代表了运动标架相对于静止标架的[瞬时角速度](@entry_id:171936)。于是，$\mathbf{L}$ 的变换可以写成 [@problem_id:2906351]：
$$ \mathbf{L}^* = \mathbf{Q}\mathbf{L}\mathbf{Q}^T + \boldsymbol{\Omega} $$
附加项 $\boldsymbol{\Omega}$ 明确地显示了 $\mathbf{L}$ 对观测者旋转速率的依赖性，因此它不是一个客观张量。

然而，如果我们将 $\mathbf{L}$ 分解为其对称部分，即**变形率张量** $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)$，和其反对称部分，即**[自旋张量](@entry_id:187346)** $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$，我们会发现一个重要的结果。由于 $\boldsymbol{\Omega}$ 是反对称的，其对称部分为零。因此，$\mathbf{D}$ 的变换法则是：
$$ \mathbf{D}^* = \mathrm{sym}(\mathbf{L}^*) = \mathrm{sym}(\mathbf{Q}\mathbf{L}\mathbf{Q}^T + \boldsymbol{\Omega}) = \mathbf{Q}\,\mathrm{sym}(\mathbf{L})\,\mathbf{Q}^T = \mathbf{Q}\mathbf{D}\mathbf{Q}^T $$
这表明**变形率张量 $\mathbf{D}$ 是一个客观张量**。相反，[自旋张量](@entry_id:187346) $\mathbf{W}$ 却不是客观的：
$$ \mathbf{W}^* = \mathrm{skw}(\mathbf{L}^*) = \mathbf{Q}\mathbf{W}\mathbf{Q}^T + \boldsymbol{\Omega} $$
它包含了观测者的自旋。这个结果的物理意义是：物质的拉伸和[剪切变形](@entry_id:170920)速率是所有观测者都一致同意的物理实在，而物质的旋转速率则与观测者自身的旋转速率纠缠在一起，因而变得主观。同样，**涡量 (vorticity)** $\boldsymbol{\omega} = \nabla \times \mathbf{v}$，其大小是[自旋张量](@entry_id:187346) $\mathbf{W}$ 分量的两倍，因此也不是客观的 [@problem_id:2906328]。

### 对本构关系的物质[标架无关性原理](@entry_id:200995) (PMFI)

PMFI 的核心要义是：**[本构方程](@entry_id:138559)必须独立于观测者**。这意味着本构律只能通过客观的量来表达。

形式上，对于一个描述柯西应力 $\boldsymbol{\sigma}$ 的[本构关系](@entry_id:186508) $\boldsymbol{\sigma} = \hat{\boldsymbol{\sigma}}(\text{args})$，其中 "args" 代表一组运动学或[热力学变量](@entry_id:160587)，PMFI 要求函数形式 $\hat{\boldsymbol{\sigma}}$ 在所有观测者标架下都是相同的。结合应力张量的客观变换法则，我们得到对本构函数的约束条件 [@problem_id:2906327]：
$$ \hat{\boldsymbol{\sigma}}(\text{args}^*) = \mathbf{Q} \hat{\boldsymbol{\sigma}}(\text{args}) \mathbf{Q}^T $$
其中 $\text{args}^*$ 是在新标架下测得的变量。

这一原理具有深远的影响。例如，它直接排除了任何形如 $\boldsymbol{\sigma} = \mathcal{F}(\mathbf{L})$ 的本构关系。因为 $\mathbf{L}$ 不是客观的，它的变换包含任意的观测者自旋 $\boldsymbol{\Omega}$，而 $\boldsymbol{\sigma}$ 的变换却不包含。为了满足PMFI，函数 $\mathcal{F}$ 必须对 $\mathbf{L}$ 的反对称部分不敏感，这实际上意味着[本构关系](@entry_id:186508)只能依赖于变形率张量 $\mathbf{D}$，即 $\boldsymbol{\sigma} = \hat{\boldsymbol{\sigma}}(\mathbf{D}, \dots)$ [@problem_id:2906327]。

必须强调，**PMFI** 和**[材料对称性](@entry_id:190289)（如各向同性）**是两个完全不同的概念。PMFI 是一个普适的物理原理，适用于所有材料，它关注的是空间观测标架的变换。而各向同性是一种材料属性，描述的是材料响应在参考构形（材料自身）旋转下的[不变性](@entry_id:140168)。一个材料可以是各向异性的，但其本构律仍必须遵守PMFI。
例如，考虑一个[纤维增强复合材料](@entry_id:194995)，其本构律可能包含一个描述纤维方向的材料矢量 $\mathbf{a}_0$。一个形如 $\boldsymbol{\sigma} = \alpha \mathbf{F}\mathbf{A}_0\mathbf{F}^T$（其中 $\mathbf{A}_0 = \mathbf{a}_0 \otimes \mathbf{a}_0$ 是结构张量，$\mathbf{F}$ 是变形梯度）的定律是**各向异性**的，因为它明显依赖于材料的特定方向 $\mathbf{a}_0$。然而，它又是**客观的**，因为张量 $\mathbf{F}\mathbf{A}_0\mathbf{F}^T$ 是[材料张量](@entry_id:196294) $\mathbf{A}_0$ 到当前构形的客观映射（push-forward）。相反，一个形如 $\boldsymbol{\sigma} = k \mathbf{v} \otimes \mathbf{v}$ 的假想定律是**各向同性**的（不含任何优[选材](@entry_id:161179)料方向），但它**违反了PMFI**，因为它依赖于非客观的[速度场](@entry_id:271461) $\mathbf{v}$ [@problem_id:2906317]。

### 在材料（拉格朗日）和[有限应变表述](@entry_id:749399)中的客观性

[客观性原理](@entry_id:185412)同样适用于以参考构形为基准的[拉格朗日描述](@entry_id:264498)。

**[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 (First Piola-Kirchhoff stress, P)** 是一个连接参考构形和当前构形的“两点张量”。它与柯西应力 $\boldsymbol{\sigma}$ 的关系为 $\mathbf{P} = J\boldsymbol{\sigma}\mathbf{F}^{-T}$，其中 $J = \det(\mathbf{F})$。在观测者变换下，$\mathbf{P}$ 的变换法则是：
$$ \mathbf{P}^* = \mathbf{Q}\mathbf{P} $$
因为它没有像客观[二阶张量](@entry_id:199780)那样通过 $\mathbf{Q}^T$ 进行后乘变换，所以**[第一皮奥拉-基尔霍夫应力](@entry_id:163971) $\mathbf{P}$ 不是客观张量** [@problem_id:2906346]。

相比之下，某些完全在参考构形中定义的应变量是天然客观的。**右柯西-格林变形张量 (Right Cauchy-Green tensor)** $\mathbf{C} = \mathbf{F}^T\mathbf{F}$ 在观测者变换下的变换为 $\mathbf{C}^* = (\mathbf{Q}\mathbf{F})^T(\mathbf{Q}\mathbf{F}) = \mathbf{F}^T\mathbf{Q}^T\mathbf{Q}\mathbf{F} = \mathbf{F}^T\mathbf{F} = \mathbf{C}$。因此，**$\mathbf{C}$ 是客观的**。同理，**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain)** $\mathbf{E} = \frac{1}{2}(\mathbf{C}-\mathbf{I})$ 也是客观的 [@problem_id:2695201] [@problem_id:2906311]。

这一特性使得 $\mathbf{C}$ 和 $\mathbf{E}$ 成为构建有限变形[本构模型](@entry_id:174726)的理想选择。对于[超弹性材料](@entry_id:190241)，其[应变能密度函数](@entry_id:755490) $\Psi(\mathbf{F})$ 必须满足 PMFI，即 $\Psi(\mathbf{Q}\mathbf{F})=\Psi(\mathbf{F})$。如果我们将应变能表示为 $\mathbf{C}$ 的函数，$\Psi = \hat{\Psi}(\mathbf{C})$，或**右[拉伸张量](@entry_id:193200)** $\mathbf{U}=\sqrt{\mathbf{C}}$ 的函数，$\Psi = \tilde{\Psi}(\mathbf{U})$，那么客观性要求将自动满足，因为 $\mathbf{C}$ 和 $\mathbf{U}$ 本身就是客观的 [@problem_id:2695201]。

与此形成鲜明对比的是，在线性弹性理论中广泛使用的**线性化应变张量** $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T)$（其中 $\mathbf{u}$ 是[位移场](@entry_id:141476)）**不是客观的**。在叠加一个[刚体转动](@entry_id:191086) $\mathbf{Q}$ 后，即使没有真实变形（$\mathbf{u}=\mathbf{0}$），线性化应变也会产生一个虚假的应变 $\boldsymbol{\varepsilon}^* = \frac{1}{2}(\mathbf{Q}+\mathbf{Q}^T-2\mathbf{I})$。对于一个微小的转动角 $\theta$，这个虚假应变的大小约为 $O(\theta^2)$。在小应变（量级为 $\epsilon$）和小转动（量级为 $\theta$）并存的情况下，$\boldsymbol{\varepsilon}$ 的非客观误差项量级为 $O(\theta\epsilon) + O(\theta^2)$。因此，线性弹性理论的应用范畴被严格限制在**小应变且小转动**的工况下。通常，当转动和小[应变梯度](@entry_id:204192)有相同的量级，即 $\theta = O(\epsilon)$ 时，非客观误差为 $O(\epsilon^2)$，相对于线性理论保留的 $O(\epsilon)$ 项可以忽略不计 [@problem_id:2906311]。

### 时间导数的挑战：[客观应力率](@entry_id:199282)

在建立率无关塑性或[粘弹性](@entry_id:148045)等率型本构关系时，我们希望将应力的“变化率”与变形率张量 $\mathbf{D}$ 关联起来。一个自然的想法是使用柯西应力 $\boldsymbol{\sigma}$ 的材料时间导数 $\dot{\boldsymbol{\sigma}}$。然而，这又带来了一个新的客观性难题。

可以证明，**柯西应力的材料时间导数 $\dot{\boldsymbol{\sigma}}$ 不是一个客观张量**。在观测者变换下，$\dot{\boldsymbol{\sigma}}$ 的变换法则为：
$$ \dot{\boldsymbol{\sigma}}^* = \mathbf{Q}\dot{\boldsymbol{\sigma}}\mathbf{Q}^T + \dot{\mathbf{Q}}\boldsymbol{\sigma}\mathbf{Q}^T + \mathbf{Q}\boldsymbol{\sigma}\dot{\mathbf{Q}}^T $$
一个客观张量的时间导数，其变换结果应为 $\mathbf{Q}\dot{\boldsymbol{\sigma}}\mathbf{Q}^T$。多出来的两项 $\dot{\mathbf{Q}}\boldsymbol{\sigma}\mathbf{Q}^T + \mathbf{Q}\boldsymbol{\sigma}\dot{\mathbf{Q}}^T$ 是非客观误差。这个误差可以表示为观测者自旋 $\boldsymbol{\Omega} = \dot{\mathbf{Q}}\mathbf{Q}^T$ 与变换后应力 $\boldsymbol{\sigma}^*$ 的李括号：$\boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega}$。即使在原始标架中应力是恒定的（$\dot{\boldsymbol{\sigma}}=\mathbf{0}$），在一个旋转的观测者看来，应力也在变化，其变化率完全由观测者的旋转和当前的应力状态决定 [@problem_id:2906339]。

这个问题的存在，意味着我们不能直接在[本构关系](@entry_id:186508)中使用 $\dot{\boldsymbol{\sigma}}$。为了解决这个问题，力学家们构造了多种**[客观应力率](@entry_id:199282)**（或称**[共旋应力率](@entry_id:747894)**），例如 [Jaumann 率](@entry_id:185572)、Green-Naghdi 率或 Truesdell 率。这些应力率的定义都包含对材料时间导数 $\dot{\boldsymbol{\sigma}}$ 的修正项，以抵消由于[刚体转动](@entry_id:191086)引起的非客观部分，从而得到一个真正客观的率量，可以合法地用于构建率型[本构方程](@entry_id:138559)。对这些[客观率](@entry_id:198692)的深入探讨，是高级[材料建模](@entry_id:751724)理论的重要组成部分。