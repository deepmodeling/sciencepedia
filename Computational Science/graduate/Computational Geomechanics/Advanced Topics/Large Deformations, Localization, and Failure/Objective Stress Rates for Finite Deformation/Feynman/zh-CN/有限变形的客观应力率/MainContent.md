## 引言
在[连续介质力学](@entry_id:155125)中，如何准确描述一个正在经历大变形和大转动的物体其内部应力的真实变化，是一个根本性的挑战。当我们观察一个旋转的物体时，即使其内部没有发生任何实际的拉伸或压缩，其[应力张量](@entry_id:148973)在固定[坐标系](@entry_id:156346)中的分量也在不断变化。标准的应力时间导数无法区分这种由[刚体转动](@entry_id:191086)引起的“表观”变化和由真实[材料变形](@entry_id:169356)引起的“内在”变化，这导致了一个严重的知识鸿沟：直接使用这种“被污染”的导数来构建[本构关系](@entry_id:186508)，会引发诸如在纯旋转中无中生有地创造能量等违背基本物理定律的悖论。

本文旨在系统性地解决这一难题，为读者构建一个关于[客观应力率](@entry_id:199282)的完整知识框架。我们将分三步深入探索：
*   **原理与机制**：我们将首先揭示物质框架无关性原理的深刻内涵，并以此为基石，学习如何通过共旋思想构造出如Jaumann率和[Green-Naghdi率](@entry_id:190839)等不同的[客观应力率](@entry_id:199282)。
*   **应用与[交叉](@entry_id:147634)学科联系**：接着，我们将把这些理论置于实际工程和科学问题的背景下，探讨不同[客观率](@entry_id:198692)的选择如何影响计算力学模拟和岩土灾害预测的结果，并分析其引发的著名悖论。
*   **动手实践**：最后，通过一系列精心设计的计算练习，您将有机会亲手验证客观性的重要性，并体会不恰当的模型选择所带来的非物理后果。

让我们首先进入第一章，从最基本的物理原理出发，理解为何需要以及如何构造一个“客观”的应力变化度量。

## 原理与机制

在物理学中，最深刻的洞见往往源于最简单的思想实验。想象一个绕着中心轴匀速旋转的飞轮。现在，让我们聚焦于[飞轮](@entry_id:195849)上的一个[质点](@entry_id:186768)。从物理直觉上来说，这个质点仅仅在做刚体旋转，它没有被拉伸、挤压或扭曲。因此，它内部的“真实”应力状态理应保持不变。然而，如果我们是一位站在地面上的静止观察者，我们会看到这个质点的位置在不断变化，描述其应力状态的张量（比如柯西应力张量 $\boldsymbol{\sigma}$）的分量也在一个固定的[坐标系](@entry_id:156346)中不停地改变。

这便引出了一个核心的困境：我们如何区分材料内部真实的[物理变化](@entry_id:136242)（例如由变形引起的应力增加）和仅仅由于观察者或者物体自身的旋转而带来的表观变化？我们日常使用的标准时间导数，$\dot{\boldsymbol{\sigma}}$，即柯西[应力张量](@entry_id:148973)的物质导数，恰恰混合了这两种效应。它所衡量的，是在一个固定的空间[坐标系](@entry_id:156346)中应力分量的变化率。这种“被污染”的度量方式会带来严重的物理问题。

### 观察者的困境：为何应力变化不简单

让我们把这个问题推向极致。假设我们错误地使用这个朴素的[物质导数](@entry_id:172646) $\dot{\boldsymbol{\sigma}}$ 来构建一个能量耗散的表达式，比如一个假设的“能量速率” $\dot{w} = \boldsymbol{\sigma} : \mathbb{A} : \dot{\boldsymbol{\sigma}}$，其中 $\mathbb{A}$ 是某个材料属性张量。现在，让一个物体经历一个纯粹的刚体旋转，比如转一整圈回到初始姿态，期间没有任何变形发生。由于是纯旋转，变形率张量 $\mathbf{D}$ 始终为零，因此真实的[机械功率](@entry_id:163535) $\boldsymbol{\sigma}:\mathbf{D}$ 也始终为零，整个过程不应有任何能量的净产生或消耗。

然而，如果我们用那个错误的能量速率表达式进行积分，我们会震惊地发现，在一个完整的旋转周期后，竟然产生了非零的净“功”！这意味着，仅仅通过改变观察视角或者让物体旋转，我们就能无中生有地创造能量，这显然违背了最基本的[热力学第一定律](@entry_id:146485)。这个悖论是一个清晰的警告：柯西[应力张量](@entry_id:148973)的物质导数 $\dot{\boldsymbol{\sigma}}$ 本身不是一个“客观”的物理量，我们不能用它来构建描述材料真实响应的[本构方程](@entry_id:138559)。

### 物质框架无关性原理

这个困境的解决方案，植根于一个深刻的物理原理，即**物质框架无关性 (Principle of Material Frame Indifference, MFI)**，有时也称为[客观性原理](@entry_id:185412)。它的核心思想是：物理定律的形式不应依赖于观察者。无论观察者是静止的，还是在做匀速运动，抑或是在做任意的刚体运动（旋转加平移），他们所观察到的物理现象，其内在规律应当是相同的。

在数学上，我们将一个观察者的变换描述为一个叠加的[刚体运动](@entry_id:193355)：$\mathbf{x}^*(t) = \mathbf{Q}(t)\mathbf{x}(t) + \mathbf{c}(t)$。这里，$\mathbf{x}$ 和 $\mathbf{x}^*$ 分别是同一个物[质点](@entry_id:186768)在旧、新观察者[坐标系](@entry_id:156346)中的位置，$\mathbf{Q}(t)$ 是一个时间依赖的正交旋转矩阵 ($\mathbf{Q}^T\mathbf{Q}=\mathbf{I}, \det\mathbf{Q}=1$)，$\mathbf{c}(t)$ 是一个平移向量。

根据这个原理，一个物理量是否“客观”，取决于它在观察者变换下的 transformation law。例如，柯西应力张量 $\boldsymbol{\sigma}$ 是一个客观的[二阶张量](@entry_id:199780)，因为它遵循标准的[张量变换法则](@entry_id:185176)：$\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$。这个变换只涉及旋转 $\mathbf{Q}$，忠实地反映了张量本身在空间中的旋转。

然而，当我们考察速度梯度 $\mathbf{L} = \nabla\mathbf{v}$ 时，情况就变得复杂了。它的变换规律是 $\mathbf{L}^* = \mathbf{Q}\mathbf{L}\mathbf{Q}^T + \boldsymbol{\Omega}$，其中 $\boldsymbol{\Omega} = \dot{\mathbf{Q}}\mathbf{Q}^T$ 是描述新观察者[参考系](@entry_id:169232)自身旋转快慢的[自旋张量](@entry_id:187346)。多出来的这一项 $\boldsymbol{\Omega}$ 表明，[速度梯度](@entry_id:261686) $\mathbf{L}$ 不是一个客观张量，它的值受到了观察者自身运动状态的“污染”。

我们的目标是构造一个应力“率”，它必须是一个客观的张量。也就是说，它的变换规律必须像 $\boldsymbol{\sigma}$ 一样纯粹，只涉及旋转 $\mathbf{Q}$，而不能有恼人的 $\boldsymbol{\Omega}$ 项。而我们已经看到，$\dot{\boldsymbol{\sigma}}$ 并不满足这个要求。因此，我们需要寻找一种新的“求导”方式。

### 构造[客观率](@entry_id:198692)：共旋思想

如何修正 $\dot{\boldsymbol{\sigma}}$ 呢？问题的根源在于，$\dot{\boldsymbol{\sigma}}$ 是在固定的空间[坐标系](@entry_id:156346)中度量变化。但材料本身在变形和运动的过程中，其内部的[晶格](@entry_id:196752)或[分子结构](@entry_id:140109)也在不断地旋转。一个更物理的度量方式，应该是去测量一个“附着”在材料上、并随之一起旋转的观察者所看到的应力变化率。这就是**共旋 (corotational)** 思想的精髓。

为了实现这一点，我们可以从 $\dot{\boldsymbol{\sigma}}$ 中减去（或者说“修正掉”）由于材料旋转引起的表观变化。一个普遍的[共旋率](@entry_id:183217)形式可以写成：
$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Xi}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Xi}
$$
这里，$\boldsymbol{\Xi}$ 是一个反对称的**[自旋张量](@entry_id:187346)**（spin tensor），它代表了我们所选择的、用于“抵消”旋转的参考框架的[瞬时角速度](@entry_id:171936)。这个表达式的右边两项 $\boldsymbol{\Xi}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{\Xi}$ （有时也写作 $-\boldsymbol{\sigma}\boldsymbol{\Xi} + \boldsymbol{\Xi}\boldsymbol{\sigma}$，取决于符号约定）精确地描述了当一个张量 $\boldsymbol{\sigma}$ 处于一个以[角速度](@entry_id:192539) $\boldsymbol{\Xi}$ 旋转的[参考系](@entry_id:169232)中时，其在固定[坐标系](@entry_id:156346)下的表观变化率。因此，$\dot{\boldsymbol{\sigma}}$ 减去这一项，剩下的就是“纯粹”的、在共旋[参考系](@entry_id:169232)中测得的变化率 $\overset{\circ}{\boldsymbol{\sigma}}$。

这种构造的优美之处在于，它完美地解决了我们最初的困境。考虑一个纯刚体旋转，此时材料没有发生任何变形，即变形率张量 $\mathbf{D}=0$。一个合理的本构模型（例如 $\overset{\circ}{\boldsymbol{\sigma}} = f(\mathbf{D})$）应该预测应力率 $\overset{\circ}{\boldsymbol{\sigma}}$ 为零。而对于纯旋转，我们可以证明柯西应力的变化率恰好是 $\dot{\boldsymbol{\sigma}} = \boldsymbol{\Xi}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{\Xi}$（如果我们选择的 $\boldsymbol{\Xi}$ 恰好是物体旋转的角速度）。代入[共旋率](@entry_id:183217)的定义，我们立刻得到 $\overset{\circ}{\boldsymbol{\sigma}} = (\boldsymbol{\Xi}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{\Xi}) - (\boldsymbol{\Xi}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{\Xi}) = \mathbf{0}$。这表明，所有基于这种形式定义的[客观率](@entry_id:198692)，都能够正确地判断出：在纯旋转过程中，材料的“内在”应力没有发生任何改变。

### 自旋的“动物园”：Jaumann、Green-Naghdi及其他

至此，我们找到了构造[客观率](@entry_id:198692)的通用“配方”。但问题也随之而来：我们应该选择哪个[自旋张量](@entry_id:187346) $\boldsymbol{\Xi}$ 来代表材料的旋转呢？对这个问题的不同回答，催生了一整个“动物园”的[客观率](@entry_id:198692)定义，其中最著名的有几种：

*   **Jaumann率 (或 Zaremba-Jaumann率)**: 这是最直观的选择。[速度梯度张量](@entry_id:270928) $\mathbf{L}$ 可以唯一地分解为一个对称部分 $\mathbf{D}$（变形率张量）和一个反对称部分 $\mathbf{W}$（涡度或[自旋张量](@entry_id:187346)），即 $\mathbf{L} = \mathbf{D} + \mathbf{W}$。$\mathbf{W}$ 描述了流体微团或材料点的瞬时平均转速。选择 $\boldsymbol{\Xi} = \mathbf{W}$，我们就得到了Jaumann率：
    $$
    \overset{\circ}{\boldsymbol{\sigma}}_J = \dot{\boldsymbol{\sigma}} - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W}
    $$

*   **[Green-Naghdi率](@entry_id:190839)**: 另一个更深刻的思路是，材料的真实“旋转”应该由其变形梯度 $\mathbf{F}$ 的旋转部分来定义。通过**极分解**，我们可以将任何变形梯度唯一地分解为一个旋转 $\mathbf{R}$ 和一个纯拉伸 $\mathbf{U}$，即 $\mathbf{F} = \mathbf{R}\mathbf{U}$。这里的 $\mathbf{R}$ 代表了材料纤维从初始构型到当前构型的净旋转。这个旋转的[角速度](@entry_id:192539)由[自旋张量](@entry_id:187346) $\boldsymbol{\Omega} = \dot{\mathbf{R}}\mathbf{R}^T$ 给出。选择 $\boldsymbol{\Xi} = \boldsymbol{\Omega}$，就得到了[Green-Naghdi率](@entry_id:190839)：
    $$
    \overset{\circ}{\boldsymbol{\sigma}}_{GN} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}
    $$

那么，Jaumann率和[Green-Naghdi率](@entry_id:190839)是一回事吗？换句话说，$\mathbf{W}$ 和 $\boldsymbol{\Omega}$ 是同一个东西吗？答案是否定的。通过一番推导，我们可以揭示它们之间的精确关系：$\mathbf{W} = \boldsymbol{\Omega} + \mathrm{skw}(\mathbf{R}(\dot{\mathbf{U}}\mathbf{U}^{-1})\mathbf{R}^T)$，其中 $\mathrm{skw}(\cdot)$ 表示取反对称部分。这表明， continuum spin $\mathbf{W}$ 不仅包含了材料的整体旋转 $\boldsymbol{\Omega}$，还包含了由拉伸演化（$\dot{\mathbf{U}}$）的非共轴性引起的额外自旋。只有当拉伸的[主方向](@entry_id:276187)不发生旋转时（即拉伸是共轴的），两者才会相等。

此外，还有**[Truesdell率](@entry_id:181014)**等其他定义，它们通常与更深层次的[能量守恒](@entry_id:140514)和超[弹性理论](@entry_id:184142)相关联，我们稍后会探讨这一点。

### 后果与警示：简单剪切悖论

既然存在不同的[客观率](@entry_id:198692)定义，那么选择哪一个会对结果产生影响吗？答案是肯定的，而且影响可能非常显著，有时甚至会产生与物理直觉相悖的结果。最经典的例子就是**简单剪切悖论**。

简单剪切是岩土力学中一个非常重要的变形模式，例如模拟断层带的错动。我们考虑一个简单的 hypoelastic 材料模型，其本构关系为 $\overset{\circ}{\boldsymbol{\sigma}}_J = 2G\mathbf{D}$，其中 $G$ 是[剪切模量](@entry_id:167228)。这是一个看似非常合理的线性模型，它将[客观应力率](@entry_id:199282)与变形率线性关联起来。

然而，当我们使用Jaumann率并求解材料在持续简单剪切下的应力响应时，会得到一个惊人的结果：[剪切应力](@entry_id:137139) $\sigma_{12}$ 并非随剪切应变 $\gamma$ [线性增长](@entry_id:157553)，而是呈现出正弦函数关系 $\sigma_{12} = G\sin(\gamma)$。这意味着，当剪切应变持续增大时，材料的抵抗能力（剪应力）会达到一个峰值，然后开始下降，甚至在应变为 $\pi$ 的倍数时变为零，之后又重新增强，如此循环往复。这显然是不符合物理实际的——一块被持续剪切的材料不应该表现出这种[振荡](@entry_id:267781)性的软化和硬化行为。

这个悖论揭示了Jaumann率的一个内在缺陷：它所使用的涡度张量 $\mathbf{W}$ 在简单剪切这种包含大量内禀旋转的变形中，会“过度矫正”应力率，从而导致了这种非物理的[振荡](@entry_id:267781)。相比之下，小应变理论预测的[线性关系](@entry_id:267880) $\sigma_{12} \approx G\gamma$ 只在 $\gamma$ 很小时才与Jaumann率的结果吻合。两者之间的归一化误差为 $\frac{\sin(\gamma)}{\gamma} - 1$，这清晰地量化了Jaumann率在大[剪切变形](@entry_id:170920)下的谬误。

### 从连续到离散：增量客观性

在现代[计算力学](@entry_id:174464)中，我们是在计算机上通过一系列离散的时间步来求解这些复杂的[非线性](@entry_id:637147)问题的。这意味着，我们在理论上坚持的[客观性原理](@entry_id:185412)，必须在数值算法的层面得到贯彻。一个数值积分方案如果不能保持客观性，那么它就会在计算中引入虚假的应力，就像我们最初讨论的那个能量悖论一样。

这个要求被称为**增量客观性 (incremental objectivity)**。它规定，一个将状态从时间步 $t_n$ 更新到 $t_{n+1}$ 的算法 $\boldsymbol{\sigma}_{n+1} = \mathcal{A}(\boldsymbol{\sigma}_n, \mathbf{F}_n, \mathbf{F}_{n+1})$ 必须满足以下条件：如果将算法的所有输入量（[初始应力](@entry_id:750652)、初始和最终的变形梯度）都根据一个任意的叠加刚体运动 $\mathbf{Q}(t)$ 进行变换，那么算法的输出（最终应力）也必须精确地等于未变换输出经过相应[旋转变换](@entry_id:200017)后的结果。

更具体地，算法必须满足通勤关系：
$$
\mathcal{A}(\mathbf{Q}_n\boldsymbol{\sigma}_n\mathbf{Q}_n^T, \mathbf{Q}_n\mathbf{F}_n, \mathbf{Q}_{n+1}\mathbf{F}_{n+1}) = \mathbf{Q}_{n+1}\mathcal{A}(\boldsymbol{\sigma}_n, \mathbf{F}_n, \mathbf{F}_{n+1})\mathbf{Q}_{n+1}^T
$$
这里需要特别注意，输入应力 $\boldsymbol{\sigma}_n$ 是用初始时刻的旋转 $\mathbf{Q}_n$ 来变换的，而输出应力 $\boldsymbol{\sigma}_{n+1}$ 则是用终止时刻的旋转 $\mathbf{Q}_{n+1}$ 来变换的。这个细节至关重要。

增量客观性有一个立竿见影的推论：对于一个纯粹的旋转增量（即 $\mathbf{F}_{n+1} = \mathbf{R}_{\Delta}\mathbf{F}_n$），算法必须精确地返回[初始应力](@entry_id:750652)经过该旋转后的结果，即 $\boldsymbol{\sigma}_{n+1} = \mathbf{R}_{\Delta}\boldsymbol{\sigma}_n\mathbf{R}_{\Delta}^T$。任何不能满足这个条件的算法，都会在纯旋转中产生虚假的应力，是不可靠的。

### 更深的联系：功率、能量与[超弹性](@entry_id:159356)

到目前为止，我们主要从[运动学](@entry_id:173318)的角度讨论了客观性。但还有一个更深层次的、基于[热力学](@entry_id:141121)的视角，它揭示了为什么某些[客观率](@entry_id:198692)比其他[客观率](@entry_id:198692)更为“自然”。这个视角的核心是**功率共轭 (power conjugacy)**。

我们知道，单位体积的[应力功率](@entry_id:182907)（即应力做功的速率）在当前构型下由 $\boldsymbol{\sigma} : \mathbf{D}$ 给出。这说明柯西应力 $\boldsymbol{\sigma}$ 和变形率 $\mathbf{D}$ 是一对功率共轭的量。然而，在建立材料模型时，我们常常更关心单位**参考**体积（即变形前的体积）储存的能量。由于体积在变形过程中会发生变化（$dv = J dV$，其中 $J=\det\mathbf{F}$ 是体积变化率），单位参考体积的功率应该是：
$$
P_V = J (\boldsymbol{\sigma} : \mathbf{D}) = (J\boldsymbol{\sigma}) : \mathbf{D}
$$
这启发我们定义一个新的[应力量度](@entry_id:198799)——**[Kirchhoff应力](@entry_id:751039)** $\boldsymbol{\tau} = J\boldsymbol{\sigma}$。上面的表达式告诉我们，[Kirchhoff应力](@entry_id:751039) $\boldsymbol{\tau}$ 和变形率 $\mathbf{D}$ 才是基于参考构型的“天然”功率共轭对。

这个看似简单的换元，对于构建与**超弹性 (hyperelasticity)**（即应力可以从一个[应变能函数](@entry_id:178435)导出）相容的本构模型至关重要。在超[弹性理论](@entry_id:184142)中，我们通常从一个定义在参考构型上的能量函数出发。为了将这样的理论推广到率形式，我们需要一个与参考构型能量密切相关的应力率。

通过一系列推导可以证明，与参考构型中的[第二Piola-Kirchhoff应力](@entry_id:173163)率 $\dot{\mathbf{S}}$ 直接对应的空间应力率，正是[Kirchhoff应力](@entry_id:751039)的**上随体率 (upper-convected rate)**，有时也被宽泛地称为[Truesdell率](@entry_id:181014)。因此，将 $\boldsymbol{\tau}$ 与[Truesdell率](@entry_id:181014)（或上随体率）配对，构建形如 $\overset{\circ}{\boldsymbol{\tau}} = \mathbb{C} : \mathbf{D}$ 的[本构模型](@entry_id:174726)，能够确保即使对于可压缩材料，其[能量守恒](@entry_id:140514)关系也得到完美的保持。相比之下，其他配对方式，比如将柯西应力 $\boldsymbol{\sigma}$ 与其上随体率配对，会因为忽略了体积变化 $J$ 的影响而破坏这种能量上的一致性。

这最终将我们从纯粹的[运动学](@entry_id:173318)修正，带到了力学与[热力学](@entry_id:141121)和谐统一的更高层面。选择一个“好”的[客观应力率](@entry_id:199282)，不仅仅是为了让方程在旋转下看起来正确，更是为了确保我们的模型能够忠实地反映能量的流动与转化这一宇宙的基本法则。