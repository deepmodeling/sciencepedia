## 引言
在现代[连续介质力学](@entry_id:155125)中，描述[材料力学](@entry_id:201885)行为的本构关系是理论的基石。对于许多经历复杂变形过程的材料，如聚合物流体、金属和软组织，其响应往往通过率形式的[本构方程](@entry_id:138559)来描述，即应力率与变形率之间建立联系。这一方法引出了一个基础性问题：我们应该如何恰当地定义“应力率”？简单地采用跟随物[质点](@entry_id:186768)的[物质时间导数](@entry_id:190892)，会遇到一个深刻的理论困境——它无法满足物理定律必须独立于观察者的基本要求，即[客观性原理](@entry_id:185412)。

本文旨在系统性地解决这一知识鸿沟。我们将深入探讨为何[物质时间导数](@entry_id:190892)在描述[空间张量](@entry_id:185799)（如柯西应力）的变化时会失效，并阐明为何必须引入“客观时间导数”这一概念。通过本文的学习，您将掌握构建和区分不同客观时间导数的核心思想，并理解它们在现代[材料建模](@entry_id:751724)中的关键作用。

文章的结构将引导您逐步深入这一主题。在“原理与机制”一章中，我们将首先建立物质标架无关性的概念，并以此为基础，详细推导和比较多种主流的客观时间导数，如Jaumann率、[Green-Naghdi率](@entry_id:190839)和[Truesdell率](@entry_id:181014)。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论工具如何在[流变学](@entry_id:138671)、次[弹性理论](@entry_id:184142)和[有限应变塑性](@entry_id:185352)力学等前沿领域中发挥作用，揭示不同导数的选择如何导致对材料行为的不同预测。最后，“动手实践”部分将提供具体的计算练习，帮助您巩固对这些关键概念的理解。

## 原理与机制

在连续介质力学中，本构关系描述了材料如何响应变形或变形率，它将应力等动力学量与应变等[运动学](@entry_id:173318)量联系起来。许多先进的材料模型，特别是在塑性、[粘弹性](@entry_id:148045)以及[流体力学](@entry_id:136788)领域，都采用率形式（rate-form）的[本构方程](@entry_id:138559)，即应力率与变形率张量之间存在关系。这就提出了一个核心问题：我们应该使用哪种时间导数来描述应力的变化率？一个看似自然的选择是**[物质时间导数](@entry_id:190892)**（material time derivative），它描述了跟随一个物质点（[质点](@entry_id:186768)）的物理量的变化率。然而，我们将看到，在处理[空间张量](@entry_id:185799)（如柯西应力）时，[物质时间导数](@entry_id:190892)存在一个根本性的缺陷，这促使我们必须发展和使用**客观时间导数**（objective time derivatives）。

### [客观性原理](@entry_id:185412)（物质标架无关性）

为了理解[物质时间导数](@entry_id:190892)的问题所在，我们必须首先掌握**[客观性原理](@entry_id:185412)**（principle of objectivity），也称为**物质标架无关性**（material frame-indifference）。该原理断言，材料的本构响应（即其内在力学行为）不应依赖于观察者。换句话说，物理定律和本构关系在所有观察者看来都必须是相同的。

在数学上，我们将一个观察者建模为一个[刚性运动](@entry_id:170523)的参考标架。两个观察者之间的关系可以通过一个**叠加刚体运动**（superposed rigid body motion）来描述。假设一个观察者使用坐标 $\mathbf{x}$ 来描述一个物质点在时刻 $t$ 的空间位置，而另一个“加星”观察者使用坐标 $\mathbf{x}^{\ast}$。它们之间的关系可以表示为：
$$
\mathbf{x}^{\ast}(t) = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}(t)
$$
其中 $\mathbf{c}(t)$ 是一个时变平移向量，$\mathbf{Q}(t)$ 是一个时变**正常正交张量**（proper orthogonal tensor），满足 $\mathbf{Q}(t)\mathbf{Q}(t)^T = \mathbf{I}$ 且 $\det \mathbf{Q}(t) = 1$。这意味着 $\mathbf{Q}(t)$ 代表了一个纯旋转。这个变换保持了点之间的距离和手性，精确地描述了两个刚性标架之间的相对运动。

[客观性原理](@entry_id:185412)要求物理量在不同观察者标架下的表示遵循特定的变换法则。一个物理量如果遵循这样的法则，我们就称之为**客观的**（objective）。
*   **客观标量**（Objective scalars），如温度 $\theta$ 或密度 $\rho$，其值与观察者无关，即 $\theta^{\ast} = \theta$。
*   **客观向量**（Objective vectors），如力 $\mathbf{f}$，其分量随观察者标架的旋转而变换：$\mathbf{f}^{\ast} = \mathbf{Q}\mathbf{f}$。
*   **客观二阶[空间张量](@entry_id:185799)**（Objective second-order spatial tensors），如柯西应力张量 $\boldsymbol{\sigma}$，其变换法则是：
    $$
    \mathbf{T}^{\ast}(\mathbf{x}^{\ast}, t) = \mathbf{Q}(t) \mathbf{T}(\mathbf{x}, t) \mathbf{Q}(t)^T
    $$
    这个法则可以通过要求[标量不变量](@entry_id:193787)（如能量密度 $\mathbf{a} \cdot (\mathbf{T}\mathbf{b})$）在所有标架中保持不变来推导得出。

值得注意的是，[客观性原理](@entry_id:185412)（物质标架无关性）不同于**伽利略[不变性](@entry_id:140168)**（Galilean invariance）。伽利略[不变性](@entry_id:140168)要求力学基本定律（如[动量平衡](@entry_id:193575)方程）在所有*惯性*[参考系](@entry_id:169232)（即以恒定速度[相对运动](@entry_id:169798)的[参考系](@entry_id:169232)）中形式不变。而物质标架无关性则是一个更强的要求，它适用于任意（包括非惯性的、加速和旋转的）[参考系](@entry_id:169232)，并主要对*[本构方程](@entry_id:138559)*而非基本平衡定律施加约束。

### 时间导数的问题：非客观性

现在我们回到最初的问题：为什么[物质时间导数](@entry_id:190892) $\dot{\mathbf{T}}$ 不适用于率形式的[本构方程](@entry_id:138559)？答案是：**对于一个客观的[空间张量](@entry_id:185799) $\mathbf{T}$，其[物质时间导数](@entry_id:190892) $\dot{\mathbf{T}}$ 通常不是客观的。**

我们可以通过对其变换法则的直接计算来证明这一点。对变换关系 $\mathbf{T}^{\ast} = \mathbf{Q}\mathbf{T}\mathbf{Q}^T$ 两边关于时间求[物质导数](@entry_id:172646)，并应用[乘法法则](@entry_id:144424)，得到：
$$
\dot{\mathbf{T}}^{\ast} = \dot{\mathbf{Q}}\mathbf{T}\mathbf{Q}^T + \mathbf{Q}\dot{\mathbf{T}}\mathbf{Q}^T + \mathbf{Q}\mathbf{T}\dot{\mathbf{Q}}^T
$$
为了更好地理解这个表达式，我们引入叠加运动的**[自旋张量](@entry_id:187346)**（spin tensor） $\boldsymbol{\omega} = \dot{\mathbf{Q}}\mathbf{Q}^T$，它是一个[反对称张量](@entry_id:199349)。利用 $\mathbf{Q}^T\mathbf{Q}=\mathbf{I}$，我们有 $\mathbf{T} = \mathbf{Q}^T\mathbf{T}^{\ast}\mathbf{Q}$ 和 $\dot{\mathbf{Q}}^T = -\mathbf{Q}^T\boldsymbol{\omega}$。代入上式，经过整理可得：
$$
\dot{\mathbf{T}}^{\ast} = \mathbf{Q}\dot{\mathbf{T}}\mathbf{Q}^T + \boldsymbol{\omega}\mathbf{T}^{\ast} - \mathbf{T}^{\ast}\boldsymbol{\omega}
$$
如果[物质导数](@entry_id:172646)是客观的，其变换法则应为 $\dot{\mathbf{T}}^{\ast} = \mathbf{Q}\dot{\mathbf{T}}\mathbf{Q}^T$。然而，上式中多出了额外的项 $\boldsymbol{\omega}\mathbf{T}^{\ast} - \mathbf{T}^{\ast}\boldsymbol{\omega}$。这些项源于观察者标架自身的旋转（当 $\boldsymbol{\omega} \neq \mathbf{0}$ 时），它们“污染”了张量内在的、由[材料变形](@entry_id:169356)引起的真实变化率。因此，[物质时间导数](@entry_id:190892)依赖于观察者，不是一个客观的量。

一个具体的例子可以清晰地说明这个问题。考虑一个稳定的简单[剪切流](@entry_id:266817)，其[速度场](@entry_id:271461)为 $\mathbf{v} = (ky, 0, 0)$。对于一个固定的观察者，变形率张量 $\mathbf{D}$ 是一个常数张量，其[物质导数](@entry_id:172646)为零。但是，对于一个以角速度 $\omega$ 旋转的观察者来说，他所测量的变形率张量 $\mathbf{D}'$ 是时变的，其物质导数通常不为零。这意味着，即使在最简单的[稳态流](@entry_id:275664)动中，两个观察者对“变形率的变化率”也会有不同的测量结果，这使得物质导数无法用于建立普适的本构关系。

### 客观时间导数的定义与构造

为了建立客观的本构关系，我们需要构造一种新的时间导数，其结果本身就是一个客观张量。我们称这样一种算子 $\mathcal{D}[\cdot]$ 为**客观时间导数算子**。根据定义，如果 $\mathbf{T}$ 是一个客观张量，那么其客观时间导数 $\mathcal{D}[\mathbf{T}]$ 也必须是一个客观张量，即它必须满足以下变换法则：
$$
\mathcal{D}[\mathbf{T}]^{\ast} = \mathbf{Q} (\mathcal{D}[\mathbf{T}]) \mathbf{Q}^T
$$
构造[客观率](@entry_id:198692)的核心思想是从[物质导数](@entry_id:172646)中减去由观察者旋转引起的非客观项。这引出了几族不同的客观时间导数。

#### 协同旋转率（Corotational Rates）

协同旋转率的思想是，在一个与材料一同“协同旋转”的标架中去测量张量的变化率。因为这个浮动标架已经包含了旋转效应，所以在这个标架中计算的时间导数反映了张量“扣除”刚体旋转后的真实变化。

一般地，一个协同旋转率可以写成如下形式：
$$
\overset{\diamond}{\mathbf{T}} = \dot{\mathbf{T}} - \boldsymbol{\Omega}\mathbf{T} + \mathbf{T}\boldsymbol{\Omega}
$$
其中 $\boldsymbol{\Omega}$ 是一个反对称的**[自旋张量](@entry_id:187346)**，它代表了用于“抵消”旋转的协同旋转参考标架的[瞬时角速度](@entry_id:171936)。为了使这个率是客观的，所选的[自旋张量](@entry_id:187346) $\boldsymbol{\Omega}$ 必须满足一个特定的变换条件：
$$
\boldsymbol{\Omega}^{\ast} = \mathbf{Q}\boldsymbol{\Omega}\mathbf{Q}^T + \dot{\mathbf{Q}}\mathbf{Q}^T
$$
这个条件保证了在不同观察者看来，用于修正的自[旋量](@entry_id:158054)能够恰当地计入观察者之间的相对旋转 $\dot{\mathbf{Q}}\mathbf{Q}^T$。通过选择不同的、满足此条件的[自旋张量](@entry_id:187346) $\boldsymbol{\Omega}$，我们得到了一系列不同的协同旋转率。

*   **[Jaumann 率](@entry_id:185572)** (或 Zaremba-[Jaumann 率](@entry_id:185572)): 这是最经典的协同旋转率，它选择材料自身的**[自旋张量](@entry_id:187346)**（spin tensor）或**[涡量张量](@entry_id:189621)**（vorticity tensor）$\mathbf{W}$ 作为协同旋转的自旋。$\mathbf{W}$ 是[速度梯度](@entry_id:261686) $\mathbf{L} = \nabla \mathbf{v}$ 的反对称部分：$\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$。可以证明，$\mathbf{W}$ 恰好满足所需的变换法则，因此 [Jaumann 率](@entry_id:185572)是客观的。
    $$
    \mathbf{T}^{J} = \dot{\mathbf{T}} - \mathbf{W}\mathbf{T} + \mathbf{T}\mathbf{W}
    $$

*   **Green-Naghdi 率**: 该率选择另一个与[材料变形](@entry_id:169356)紧密相关的自旋。考虑变形梯度 $\mathbf{F}$ 的**极分解** $\mathbf{F} = \mathbf{R}\mathbf{U}$，其中 $\mathbf{R}$ 是一个[旋转张量](@entry_id:191990)，代表了物质微团体从参考构型到当前构型的纯旋转部分。Green-Naghdi 率就使用这个材料旋转的[角速度](@entry_id:192539) $\boldsymbol{\Omega}_{GN} = \dot{\mathbf{R}}\mathbf{R}^T$ 作为协同旋转的自旋。这个自旋同样满足客观性变换条件。
    $$
    \overset{\diamond}{\boldsymbol{\sigma}}_{GN} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}_{GN}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}_{GN}
    $$
    Green-Naghdi 率有一个优美的物理解释：它是在材料旋转标架中观察到的[应力张量](@entry_id:148973) $\boldsymbol{\sigma}_R = \mathbf{R}^T\boldsymbol{\sigma}\mathbf{R}$ 的[物质导数](@entry_id:172646)，然后再推回到当前的空间标架中。即：
    $$
    \overset{\diamond}{\boldsymbol{\sigma}}_{GN} = \mathbf{R} \left( \frac{d}{dt}(\mathbf{R}^T \boldsymbol{\sigma} \mathbf{R}) \right) \mathbf{R}^T
    $$

#### [对流](@entry_id:141806)率（Convected Rates）

另一族重要的[客观率](@entry_id:198692)是**[对流](@entry_id:141806)率**，它们源于在随材料变形而扭曲的[坐标系](@entry_id:156346)（即[对流](@entry_id:141806)[坐标系](@entry_id:156346)）中考察张量的变化。

*   **上随体率** (Upper Convected / Oldroyd-B Rate): 其定义为：
    $$
    \overset{\triangledown}{\mathbf{A}} = \dot{\mathbf{A}} - \mathbf{L}\mathbf{A} - \mathbf{A}\mathbf{L}^{T}
    $$
    可以证明，该率是客观的。上随体率有一个非常重要的特性：**左柯西-格林变形张量** $\mathbf{B} = \mathbf{F}\mathbf{F}^T$ 的上随体率恒为零，即 $\overset{\triangledown}{\mathbf{B}} = \mathbf{0}$。这表明张量 $\mathbf{B}$ 在随体[坐标系](@entry_id:156346)下是“守恒”的，这为上随体率提供了清晰的运动学解释。

*   **下随体率** (Lower Convected / Oldroyd-A Rate): 其定义为：
    $$
    \check{\mathbf{A}} = \dot{\mathbf{A}} + \mathbf{L}^{T}\mathbf{A} + \mathbf{A}\mathbf{L}
    $$
    该率同样是客观的。

*   **Truesdell 率**: Truesdell 率与上随体率密切相关，但它专门针对柯西应力 $\boldsymbol{\sigma}$ 定义，并且考虑了体积变化的影响。它通过**[基尔霍夫应力](@entry_id:751039)** (Kirchhoff stress) $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ (其中 $J = \det \mathbf{F}$ 是体积比) 的上随体率来定义。通过关系式 $\overset{\triangledown}{\boldsymbol{\tau}} = J \overset{\triangle}{\boldsymbol{\sigma}}$，可以推导出 Truesdell 率的表达式为：
    $$
    \overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \mathbf{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{L}^T + (\mathrm{tr}\,\mathbf{L})\boldsymbol{\sigma}
    $$
    与上随体率相比，Truesdell 率多出了一项 $(\mathrm{tr}\,\mathbf{L})\boldsymbol{\sigma}$。这一项的来源是 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 对时间求导时，雅可比行列式 $J$ 的变化率 $\dot{J}$，根据[质量守恒](@entry_id:204015)有 $\dot{J} = J (\mathrm{tr}\,\mathbf{L})$。因此，这一项是体积变化率（膨胀率）的直接体现，使得 Truesdell 率在可压缩流动问题中尤为重要。值得注意的是，Truesdell 率不属于协同旋转率的一般形式。

#### 几何观点：[李导数](@entry_id:171745)

从[微分几何](@entry_id:145818)的角度看，所有[客观率](@entry_id:198692)都可以被一个更基本的概念所统一，那就是**[李导数](@entry_id:171745)**（Lie Derivative）。一个[空间张量](@entry_id:185799)场 $\mathbf{T}$ 沿着[速度场](@entry_id:271461) $\mathbf{v}$ 的李导数 $\mathcal{L}_{\mathbf{v}}\mathbf{T}$，从根本上定义了该张量场沿物质流动的内在变化率，它通过将张量场“[拉回](@entry_id:160816)”到同一点进行比较来消除[坐标系](@entry_id:156346)效应。

[李导数](@entry_id:171745)的一个关键性质是它**天生就是客观的**。许多我们之前讨论的[客观率](@entry_id:198692)都可以用李导数来简洁地表示。例如，柯西应力的 Truesdell 率可以优雅地定义为：
$$
\overset{\triangle}{\boldsymbol{\sigma}} = J^{-1}\mathcal{L}_{\mathbf{v}}\boldsymbol{\tau}
$$
这个定义立即使其客观性变得显而易见，并揭示了其深层的几何意义。

### 各种率的比较与应用

既然我们定义了多种[客观率](@entry_id:198692)，一个自然的问题是：它们之间有何区别？我们应该选择哪一个？

*   **自旋的比较**: 不同的协同旋转率源于对“协同旋转”的不同理解，即选择了不同的[自旋张量](@entry_id:187346)。例如，[Jaumann 率](@entry_id:185572)使用的材料自旋 $\mathbf{W}$ 和 Green-Naghdi 率使用的极分解旋转率 $\boldsymbol{\Omega}_{GN}$ 通常并不相等。它们相等的充分必要条件是 $\mathbf{U}$ 和 $\dot{\mathbf{U}}$ 可交换，即 $[\dot{\mathbf{U}}, \mathbf{U}]=\mathbf{0}$。这在物理上意味着主拉伸方向在材料[坐标系](@entry_id:156346)下是固定的，没有发生旋转。一个均匀的各向同性拉伸满足此条件，而一个简单剪切流动则不满足。

*   **小应变、大转动情况**: 在许多工程问题（如[金属塑性](@entry_id:176585)、柔性结构）中，材料的[弹性应变](@entry_id:189634)很小，但整体结构可能经历大的[刚体转动](@entry_id:191086)。在这种情况下，可以证明，所有协同旋转率（如 Jaumann、Green-Naghdi 和对数率）的预测在应变的一阶小量上是彼此一致的，它们的差别只体现在二阶及更高阶的小量上。因此，在小应变理论的框架下，选择哪种协同旋转率通常影响不大。

*   **[可积性](@entry_id:142415)与超弹性**: 在构建弹性本构模型时，一个重要的物理要求是模型的**[可积性](@entry_id:142415)**（integrability），即可否从一个[应变能密度函数](@entry_id:755490)（stored-energy function）导出，即是否为**[超弹性](@entry_id:159356)**（hyperelastic）模型。一个不可积的（或称**[亚弹性](@entry_id:204371)**，hypoelastic）模型在应变的闭合循环中可能会预测出虚假的能量产生或耗散。
    *   一个著名的结果是，基于 [Jaumann 率](@entry_id:185572)或 Green-Naghdi 率的线性[亚弹性模型](@entry_id:184632)（即[客观率](@entry_id:198692)正比于变形率 $\mathbf{D}$）通常是不可积的。例如，在纯剪切的加载-卸载循环下，它们会预测非零的净功。
    *   相比之下，**对数率**（Logarithmic rate）在这种线性关系下是可积的，它能对应一个定义在[对数应变](@entry_id:751438)上的超弹性[势能函数](@entry_id:200753)。
    *   这个特性对于确保[大变形](@entry_id:167243)下弹性模型的物理真实性至关重要。

*   **刚体旋转检验**: 所有合理的[客观率](@entry_id:198692)都必须通过一个基本的“健全性检验”：在纯刚体旋转下，变形率 $\mathbf{D}=\mathbf{0}$，因此任何[客观应力率](@entry_id:199282)都应为零（$\overset{\diamond}{\boldsymbol{\sigma}}=\mathbf{0}$）。这意味着，应力张量本身只是随刚体一同旋转，而不产生任何虚假的应力增量。我们所讨论的所有[客观率](@entry_id:198692)——[Jaumann 率](@entry_id:185572)、Green-Naghdi 率、Truesdell 率等——都满足这一基本要求。

总之，客观时间导数是处理有限变形和旋转问题时，建立率形式本构关系的基石。虽然存在多种定义，但它们都旨在从测量到的总变化率中分离出由观察者或材料刚体旋转引起的表观变化，从而捕捉张量的内在变化。对不同[客观率](@entry_id:198692)的选择取决于具体的物理问题、所期望的精度以及对模型理论性质（如可积性）的要求。