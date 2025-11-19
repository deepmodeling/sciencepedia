## 引言
超导电性，即材料在低于某一[临界温度](@entry_id:146683)时电阻完全消失的[宏观量子现象](@entry_id:144018)，自发现以来一直吸引着物理学家的极大兴趣。然而，[零电阻](@entry_id:145222)的特性本身并不足以完全定义超导态，一个关键的谜题在于它与[理想导体](@entry_id:273420)的本质区别。一个电阻为零的“[完美导体](@entry_id:273420)”会俘获其内部的磁通量，而[超导体](@entry_id:191025)则会主动将[磁场](@entry_id:153296)排出体外——这便是迈斯纳效应。这一现象揭示了超导态是一个独特的、与历史路径无关的热力学平衡态，需要一套超越经典电磁学的理论来描述。

本文旨在系统性地介绍并应用弗里茨·伦敦 (Fritz London) 和海因茨·伦敦 (Heinz London) 兄弟提出的唯象电动力学理论，它为理解[超导体](@entry_id:191025)的电磁行为奠定了基石。通过阅读本章，你将深入学习：
-   **原理与机制**：我们将从迈斯纳效应出发，建立[伦敦方程](@entry_id:139502)，并探讨[伦敦穿透深度](@entry_id:143674)的概念，以及该局域理论的[适用范围](@entry_id:636189)和局限性。
-   **应用与交叉学科联系**：我们将展示如何运用伦敦理论来表征材料、理解[第二类超导体](@entry_id:143461)中的涡旋物理，并揭示其如何成为连接宏观测量与微观[配对机制](@entry_id:145844)的桥梁。
-   **动手实践**：通过一系列精心设计的计算问题，你将亲手应用[伦敦方程](@entry_id:139502)来解决超导[电动力学](@entry_id:158759)中的经典问题，从而巩固你的理解。

现在，让我们从区分[超导体](@entry_id:191025)与完美导体的根本差异开始，进入[伦敦电动力学](@entry_id:191745)的核心世界。

## 原理与机制

在引言章节中，我们已经了解了超[导电性](@entry_id:137481)的基本现象，即在临界温度以下电阻突然消失。然而，仅凭[零电阻](@entry_id:145222)这一点并不能完全捕捉到超导态的本质。本章将深入探讨描述[超导体](@entry_id:191025)内[电磁场](@entry_id:265881)行为的唯象理论——[伦敦电动力学](@entry_id:191745)，并阐明其背后的核心原理与机制。我们将从区分[超导体](@entry_id:191025)与理想完美导体出发，建立[伦敦方程](@entry_id:139502)，并探讨其在描述[磁场](@entry_id:153296)排斥、[表面电流](@entry_id:261791)以及理论局限性等方面的应用。

### [迈斯纳效应](@entry_id:273600)：超导电性的基本特征

一个自然的疑问是：一个电阻为零的导体（即**[完美导体](@entry_id:273420) (perfect conductor)**）与一个[超导体](@entry_id:191025)有何区别？乍看之下，两者似乎等价。然而，1933年，Walther Meissner 和 Robert Ochsenfeld 的一个关键实验揭示了两者之间深刻的差异。

考虑一个思想实验来阐明这一点。假设我们有两种材料：一种是假想的完美导体，其电导率 $\sigma \to \infty$；另一种是真实的[超导体](@entry_id:191025)。我们将这两种材料置于一个恒定的外[磁场](@entry_id:153296) $H_0$ 中，并将其从高于其[临界温度](@entry_id:146683) $T_c$ 的状态冷却到低于 $T_c$ 的状态。这个过程被称为**场致冷却 (field-cooling)** [@problem_id:3009512]。

对于完美导体，其电磁行为由[欧姆定律](@entry_id:276027) $\mathbf{J} = \sigma \mathbf{E}$ 和麦克斯韦方程组支配。在 $\sigma \to \infty$ 的极限下，为了维持有限的[电流密度](@entry_id:190690) $\mathbf{J}$，[导体内部的电场](@entry_id:262634) $\mathbf{E}$ 必须为零。根据法拉第[电磁感应](@entry_id:181154)定律 $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$，内部[电场](@entry_id:194326)为零意味着[磁感应强度](@entry_id:144179) $\mathbf{B}$ 的时间变化率为零，即 $\frac{\partial \mathbf{B}}{\partial t} = 0$。这个方程的含义是，一旦材料进入完美导电状态，其内部的[磁通量](@entry_id:268943)就会被“冻结”或“俘获”，无法再随时间改变。在场致冷却过程中，由于外部[磁场](@entry_id:153296)是恒定的，没有变化的[磁场](@entry_id:153296)来诱导电流，因此在材料转变为完美导体之前穿透其内部的[磁场](@entry_id:153296)将被完整地保留下来。最终，[完美导体](@entry_id:273420)内部的[磁感应强度](@entry_id:144179) $B_{\text{bulk}} \approx \mu_0 H_0$ [@problem_id:3001691] [@problem_id:2840809]。

然而，Meissner 和 Ochsenfeld 的实验表明，当[超导体](@entry_id:191025)在[磁场](@entry_id:153296)中被冷却至 $T_c$ 以下时，它会主动地将内部的磁通量排出体外，使得其内部深处的[磁感应强度](@entry_id:144179) $B_{\text{bulk}} \approx 0$。这种现象被称为**迈斯纳-奥克森菲尔德效应 (Meissner-Ochsenfeld effect)**，或简称为**迈斯纳效应**。

这种行为与[完美导体](@entry_id:273420)截然不同。更重要的是，无论[超导体](@entry_id:191025)是在冷却前还是冷却后被置于[磁场](@entry_id:153296)中（即所谓的“[零场冷却](@entry_id:148709)”），其最终的[平衡态](@entry_id:168134)都是内部[磁场](@entry_id:153296)为零。这表明超导态是一个独特的、与历史路径无关的**[热力学平衡](@entry_id:141660)态**，而不仅仅是一种动力学特性（如[零电阻](@entry_id:145222)）。完美[电导](@entry_id:177131)性所预言的[磁通](@entry_id:191239)俘获是一个依赖于历史的[非平衡现象](@entry_id:198484)，因此，它不足以描述超导电性。为了解释[迈斯纳效应](@entry_id:273600)，我们需要一套全新的电[动力学方程](@entry_id:751029)，它必须包含一个能够将电流与[静态磁场](@entry_id:195560)直接联系起来的本构关系 [@problem_id:2840809] [@problem_id:3001691]。

### [伦敦方程](@entry_id:139502)：唯象电[动力学理论](@entry_id:136901)

为了解释迈斯纳效应，Fritz London 和 Heinz London 兄弟在1935年提出了一个唯象理论。他们假设超导电流是由一种无散射、无耗散的**超流体 (superfluid)** 载流子（后来被理解为[库珀对](@entry_id:143370)）承载的。

#### [超流体](@entry_id:180718)模型与第一[伦敦方程](@entry_id:139502)

我们可以从一个简单的经典模型出发。考虑一个由密度为 $n_s$、[电荷](@entry_id:275494)为 $q$、质量为 $m$ 的无耗散载流子组成的带电[超流体](@entry_id:180718)。在[电场](@entry_id:194326) $\mathbf{E}$ 的作用下，每个载流子根据[牛顿第二定律](@entry_id:274217)进行加速：
$m \frac{d\mathbf{v}_s}{dt} = q\mathbf{E}$
其中 $\mathbf{v}_s$ 是[超流体](@entry_id:180718)的速度。超流[电流密度](@entry_id:190690)由 $\mathbf{J}_s = n_s q \mathbf{v}_s$ 给出。对其求时间导数，我们得到：
$\frac{\partial \mathbf{J}_s}{\partial t} = n_s q \frac{\partial \mathbf{v}_s}{\partial t} = \frac{n_s q^2}{m} \mathbf{E}$
这就是**第一[伦敦方程](@entry_id:139502)**。它描述了超流载流子在[电场](@entry_id:194326)中的无损加速行为。这个方程的一个直接推论是，在恒定的直流[电场](@entry_id:194326) $\mathbf{E}_0$ 作用下，超流电流将随时间线性增长 $\mathbf{J}_s(t) = (\frac{n_s q^2}{m} t) \mathbf{E}_0$，这意味着[直流电导率](@entry_id:273370)是无穷大的 [@problem_id:3001720]。在[频域](@entry_id:160070)中，这对应于[电导率](@entry_id:137481) $\sigma(\omega)$ 在零频处有一个狄拉克 $\delta$ 函数。

#### 第二[伦敦方程](@entry_id:139502)：[平衡态](@entry_id:168134)的公设

然而，仅有第一[伦敦方程](@entry_id:139502)是不够的。通过对其两边取旋度并结合法拉第定律 $\nabla \times \mathbf{E} = -\partial_t \mathbf{B}$，可以推导出：
$\frac{\partial}{\partial t} \left( \nabla \times \mathbf{J}_s + \frac{n_s q^2}{m} \mathbf{B} \right) = 0$
这表明量 $\nabla \times \mathbf{J}_s + \frac{n_s q^2}{m} \mathbf{B}$ 是一个不随时间变化的守恒量，其值由[初始条件](@entry_id:152863)决定。这恰恰是完美导体的行为，它会导致[磁通](@entry_id:191239)俘获，而不能解释与历史无关的迈斯纳效应 [@problem_id:2840809]。

为了获得迈斯纳效应，伦敦兄弟更进一步，**公设 (postulated)** 在[热力学平衡](@entry_id:141660)态下，这个[守恒量](@entry_id:150267)必须恒为零。这就得到了**第二[伦敦方程](@entry_id:139502)**：
$\nabla \times \mathbf{J}_s = -\frac{n_s q^2}{m} \mathbf{B}$
这个方程是一个描述[平衡态](@entry_id:168134)的全新本构关系，它直接将超流电流的卷曲与局域[磁场](@entry_id:153296)联系起来，正是解释迈斯纳效应所缺失的关键环节。注意，这个方程中的负号至关重要；如果符号为正，将导致[磁场](@entry_id:153296)在[超导体](@entry_id:191025)内部[振荡](@entry_id:267781)或增长，而不是被排斥 [@problem_id:2837249]。

#### 从[正则动量](@entry_id:155151)到第二[伦敦方程](@entry_id:139502)

第二[伦敦方程](@entry_id:139502)有一个更深刻的来源，它与超导态的宏观[量子相干性](@entry_id:143031)有关。在一个单连通的[超导体](@entry_id:191025)中，所有超流载流子共享一个[宏观波函数](@entry_id:143853)，其相位是单值的。这导致了载流子的**[正则动量](@entry_id:155151)** $\mathbf{p}_{\text{can}} = m\mathbf{v}_s + q\mathbf{A}$ 在平衡态下是无旋的，即 $\nabla \times \mathbf{p}_{\text{can}} = \mathbf{0}$，其中 $\mathbf{A}$ 是[磁矢量势](@entry_id:141246) [@problem_id:2837249]。
展开这个旋度，我们得到：
$m(\nabla \times \mathbf{v}_s) + q(\nabla \times \mathbf{A}) = \mathbf{0}$
由于 $\mathbf{B} = \nabla \times \mathbf{A}$，我们有 $m(\nabla \times \mathbf{v}_s) = -q\mathbf{B}$。再对[电流密度](@entry_id:190690)表达式 $\mathbf{J}_s = n_s q \mathbf{v}_s$ 两边取旋度（假设 $n_s$ 均匀），即可直接得到第二[伦敦方程](@entry_id:139502)：
$\nabla \times \mathbf{J}_s = n_s q (\nabla \times \mathbf{v}_s) = n_s q \left(-\frac{q}{m}\mathbf{B}\right) = -\frac{n_s q^2}{m} \mathbf{B}$
这种推导方式揭示了第二[伦敦方程](@entry_id:139502)是超导宏观量子性的直接体现。

### [磁场](@entry_id:153296)排斥与穿透深度

有了[伦敦方程](@entry_id:139502)，我们现在可以定量地描述迈斯纳效应。

#### [磁场](@entry_id:153296)的控制方程

在静态情况下，[安培定律](@entry_id:140092)为 $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}_s$，其中 $\mu_0$ 是[真空磁导率](@entry_id:186031)。对安培定律两边取旋度，并利用矢量恒等式 $\nabla \times (\nabla \times \mathbf{B}) = \nabla(\nabla \cdot \mathbf{B}) - \nabla^2 \mathbf{B}$ 以及麦克斯韦方程 $\nabla \cdot \mathbf{B} = 0$，我们得到：
$-\nabla^2 \mathbf{B} = \mu_0 (\nabla \times \mathbf{J}_s)$
将第二[伦敦方程](@entry_id:139502)代入上式：
$-\nabla^2 \mathbf{B} = \mu_0 \left( -\frac{n_s q^2}{m} \mathbf{B} \right)$
整理后得到描述[超导体](@entry_id:191025)内部[磁场](@entry_id:153296)的关键方程：
$\nabla^2 \mathbf{B} = \frac{\mu_0 n_s q^2}{m} \mathbf{B}$
这个方程表明，[磁场](@entry_id:153296) $\mathbf{B}$ 的[拉普拉斯算子](@entry_id:146319)正比于其自身。

#### [伦敦穿透深度](@entry_id:143674)

我们可以定义一个具有长度量纲的特征参数，即**[伦敦穿透深度](@entry_id:143674) (London penetration depth)** $\lambda_L$：
$\lambda_L^2 = \frac{m}{\mu_0 n_s q^2}$
于是，场方程可以写成更简洁的形式：
$\nabla^2 \mathbf{B} = \frac{1}{\lambda_L^2} \mathbf{B}$
[伦敦穿透深度](@entry_id:143674) $\lambda_L$ 是一个由材料参数（载流子密度 $n_s$、[有效质量](@entry_id:142879) $m$ 和[电荷](@entry_id:275494) $q$）决定的本征长度。它依赖于[真空磁导率](@entry_id:186031) $\mu_0$，而不依赖于[真空介电常数](@entry_id:204253) $\epsilon_0$，反映了超导屏蔽是一种磁效应 [@problem_id:2837249]。$\lambda_L$ 的物理意义是[磁场](@entry_id:153296)能够穿透到[超导体](@entry_id:191025)表面的特征深度。

#### 块体与薄膜几何中的场[分布](@entry_id:182848)

考虑一个占据半空间 $x>0$ 的[超导体](@entry_id:191025)，在 $x0$ 的真空区域施加一个平行于表面的均匀[磁场](@entry_id:153296) $B_0 \hat{\mathbf{z}}$。在这种一维几何下，方程简化为 $\frac{d^2 B_z}{dx^2} = \frac{1}{\lambda_L^2} B_z$。考虑到物理上合理的边界条件，即[磁场](@entry_id:153296)在[超导体](@entry_id:191025)深处 ($x \to \infty$) 不会发散，且在界面 $x=0$ 处切向分量连续，可以得到方程的解为 [@problem_id:2837249] [@problem_id:3001691]：
$B_z(x) = B_0 \exp(-x/\lambda_L)$
这个解完美地描述了迈斯纳效应：[磁场](@entry_id:153296)从[超导体](@entry_id:191025)表面开始呈指数衰减，在几个 $\lambda_L$ 的深度之外，[磁场](@entry_id:153296)几乎为零。这种指数衰减的场[分布](@entry_id:182848)是[超导体](@entry_id:191025)[自由能最小化](@entry_id:183270)的结果，它是在排斥[磁场](@entry_id:153296)产生的[磁场](@entry_id:153296)能与维持屏蔽电流所需的动能之间取得的一种平衡 [@problem_id:3001691]。

在更复杂的几何中，例如一个厚度为 $d$ 的薄膜，其一侧 ($x=0$) 施加[磁场](@entry_id:153296) $H_0$，另一侧 ($x=d$) 为无场真空，场[分布](@entry_id:182848)的解会更加复杂。通过求解方程并应用边界条件 $H_z(0) = H_0$ 和 $H_z(d) = 0$，可以得到内部的[磁场](@entry_id:153296)[分布](@entry_id:182848)为 [@problem_id:2837251]：
$H_z(x) = H_0 \frac{\sinh((d-x)/\lambda_L)}{\sinh(d/\lambda_L)}$
相应的，在受照面 $x=0$ 处的屏蔽电流密度大小为：
$|J_y(x=0)| = \frac{H_0}{\lambda_L} \coth\left(\frac{d}{\lambda_L}\right)$
当薄膜厚度 $d \gg \lambda_L$ 时，$\coth(d/\lambda_L) \to 1$，结果趋近于半无限大块体的情况。

### 伦敦理论的深入探讨

[伦敦方程](@entry_id:139502)虽然形式简洁，但其内涵丰富，并引出了一些更深入的概念。

#### 伦敦规范的便利性

在某些情况下，直接使用矢量势 $\mathbf{A}$ 而不是[磁场](@entry_id:153296) $\mathbf{B}$ 会更方便。通过对第一[伦敦方程](@entry_id:139502)进行时间积分，可以得到一个看似简单的关系 $\mathbf{J}_s = -\frac{n_s q^2}{m} \mathbf{A}$。然而，这个关系本身是**规范不守恒 (not gauge invariant)** 的，因为在[规范变换](@entry_id:176521) $\mathbf{A} \to \mathbf{A} + \nabla\chi$ 下，$\mathbf{A}$ 会改变，而[物理可观测量](@entry_id:154692) $\mathbf{J}_s$ 不应改变。

为了解决这个问题，可以选择一个特定的规范。**伦敦规范 (London gauge)**，定义为 $\nabla \cdot \mathbf{A} = 0$，是一个特别方便的选择。在这种规范下，$\mathbf{J}_s$ 与 $\mathbf{A}$ 的简单正比关系 $\mathbf{J}_s = -(\frac{n_s q^2}{m}) \mathbf{A}$ 得以成立，极大地简化了计算 [@problem_id:1818570]。然而，必须强调的是，物理上真正有意义且规范不变的是用场量 $\mathbf{E}$ 和 $\mathbf{B}$ 书写的[伦敦方程](@entry_id:139502) [@problem_id:2840809]。

#### 纵向与横向响应：等离激元与[磁屏蔽](@entry_id:192877)

伦敦理论的一个显著特点是它主要关注对横向[磁场](@entry_id:153296)的响应（屏蔽），而似乎忽略了对纵向[电场](@entry_id:194326)的响应。这背后的物理原因是深刻的 [@problem_id:3001717]。

带电超流体的纵向[集体激发](@entry_id:145026)模式与[电荷密度](@entry_id:144672)的[振荡](@entry_id:267781)相关。结合第一[伦敦方程](@entry_id:139502)、[电荷连续性](@entry_id:747292)方程 $\partial_t \rho + \nabla \cdot \mathbf{j} = 0$ 和高斯定律 $\nabla \cdot \mathbf{E} = \rho / \epsilon_0$，可以推导出[电荷密度](@entry_id:144672) $\rho$ 满足一个简谐[振动](@entry_id:267781)方程：
$\frac{\partial^2 \rho}{\partial t^2} + \omega_p^2 \rho = 0$
其中 $\omega_p^2 = \frac{n_s q^2}{m \epsilon_0}$ 是**等离激元频率 (plasma frequency)** 的平方。对于金属中的电子密度，$\hbar\omega_p$ 通常对应于数个[电子伏特](@entry_id:144194)的高能量（紫外波段）。因此，在低频电动力学（包括静态情况）中，这些高能量的纵向模式（[等离激元](@entry_id:146184)）无法被激发，可以近似认为[电荷密度](@entry_id:144672)始终为零。

相比之下，[横向模式](@entry_id:163265)与无散的[磁场](@entry_id:153296)（$\nabla \cdot \mathbf{B} = 0$）相关。第二[伦敦方程](@entry_id:139502)描述了对横向[磁场](@entry_id:153296)的[无能](@entry_id:201612)隙响应。即使是静态（$\omega=0$）的[磁场](@entry_id:153296)也会被屏蔽。因此，在低能区，[超导体的电磁响应](@entry_id:146891)由横向[磁屏蔽](@entry_id:192877)主导，而纵向[电荷](@entry_id:275494)[振荡](@entry_id:267781)则被“冻结”在高能区，这为伦敦理论集中处理磁响应提供了物理上的合理解释。

### 局域模型的局限性：[非局域电动力学](@entry_id:199532)

[伦敦电动力学](@entry_id:191745)是一个**局域 (local)** 理论，因为它假设在某一点 $\mathbf{r}$ 的电流密度 $\mathbf{J}_s(\mathbf{r})$ 只由该点处的场（如 $\mathbf{A}(\mathbf{r})$）决定。然而，根据BCS微观理论，超导载流子（[库珀对](@entry_id:143370)）具有有限的空间尺度，这个尺度由**[BCS相干长度](@entry_id:189204) (BCS coherence length)** $\xi_0$ 描述。

#### 相干长度与非局域性的起源

当[电磁场](@entry_id:265881)的空间变化尺度远大于[库珀对](@entry_id:143370)的尺寸 $\xi_0$ 时，局域近似是成立的。但是，如果场的空间变化尺度变得与 $\xi_0$ 相当或更小时，一个库珀对在其空间范围内会感受到变化的场，此时电流响应就不再是局域的。在 $\mathbf{r}$ 点的电流将依赖于其周围一个大小约为 $\xi_0$ 的邻域内的场的平均值。这种效应被称为**非局域性 (nonlocality)**。

在迈斯纳态中，场的特征变化尺度由穿透深度 $\lambda$ 决定。因此，当 $\xi_0 \gtrsim \lambda$ 时，局域的伦敦理论就会失效 [@problem_id:3023056]。这种情况下的[超导体](@entry_id:191025)被称为**Pippard[超导体](@entry_id:191025)**。

#### Pippard 理论与非局域响应核

非局域响应的一般形式在[实空间](@entry_id:754128)中是一个[卷积积分](@entry_id:155865)：
$\mathbf{J}(\mathbf{r}) = -\int d^3 r' \, \underline{\underline{K}}(\mathbf{r}-\mathbf{r}') \mathbf{A}(\mathbf{r}')$
其中 $\underline{\underline{K}}(\mathbf{r}-\mathbf{r}')$ 是一个响应核，其作用范围约为相干长度 $\xi_0$。在傅里叶空间中，这个关系简化为乘法：
$\mathbf{J}(\mathbf{q}) = -\underline{\underline{K}}(\mathbf{q}) \mathbf{A}(\mathbf{q})$
非局域性体现在响应核 $\underline{\underline{K}}(\mathbf{q})$ 对波矢 $\mathbf{q}$ 的依赖上。

*   当场变化缓慢时（$q \to 0$），$K(q)$ 趋于一个常数，恢复为伦敦理论。
*   当场变化迅速时（$q$ 增大），扩展尺寸为 $\xi_0$ 的库珀对无法有效跟随场的快速变化，其响应会被平均掉，导致响应核 $K(q)$ 的大小随 $q$ 的增大而减小 [@problem_id:3023056]。
*   规范不变性要求响应是横向的，即 $\mathbf{q} \cdot \mathbf{J}(\mathbf{q})=0$。这给响应核张量带来了约束，其形式必须为 $\underline{\underline{K}}_{ij}(\mathbf{q}) = K(q) (\delta_{ij} - \frac{q_i q_j}{q^2})$，这表明只有垂直于 $\mathbf{q}$ 的矢量势分量才会贡献电流 [@problem_id:3023056]。

非局域效应修正了穿透深度的概念。穿透深度也变得依赖于[波矢](@entry_id:178620) $q$。对 Pippard 核在小 $q$ 处展开，可以得到对[伦敦穿透深度](@entry_id:143674)的第一个非局域修正 [@problem_id:1096857]：
$\lambda(q) \approx \lambda_L \left(1 + \frac{\xi_0^2 q^2}{20}\right)$

#### [第一类与第二类超导体](@entry_id:198434)

描述非局域性强弱的关键[无量纲参数](@entry_id:169335)是[金兹堡-朗道参数](@entry_id:147113) $\kappa = \lambda/\xi$（其中 $\xi$ 是有效[相干长度](@entry_id:139128)）。
*   **[第一类超导体](@entry_id:142688)**：通常 $\kappa  1/\sqrt{2}$，意味着 $\xi > \lambda$。这类[超导体](@entry_id:191025)（特别是洁净样品）表现出强烈的非局域性（Pippard型），伦敦局域理论对其描述不佳。
*   **[第二类超导体](@entry_id:143461)**：$\kappa > 1/\sqrt{2}$，意味着 $\lambda > \xi$。在这类[超导体](@entry_id:191025)中，场的[穿透深度](@entry_id:136478)远大于库珀对的尺寸，因此局域的伦敦理论是一个非常好的近似 [@problem_id:3023056]。

### 杂质的作用：洁净极限与肮脏极限

真实材料中总存在杂质，它们通过散射电子来影响超[导电性](@entry_id:137481)。电子的**平均自由程 (mean free path)** $l$ 是描述[杂质散射](@entry_id:267814)强度的关键参数。

#### 有效相干长度

在存在杂质的情况下，[库珀对](@entry_id:143370)的相干性会受到破坏。有效[相干长度](@entry_id:139128) $\xi$ 由本征[BCS相干长度](@entry_id:189204) $\xi_0$ 和[平均自由程](@entry_id:139563) $l$ 共同决定，一个很好的近似是 $1/\xi \approx 1/\xi_0 + 1/l$。

*   **洁净极限 (Clean limit)**：当 $l \gg \xi_0$ 时，[杂质散射](@entry_id:267814)效应可以忽略，有效[相干长度](@entry_id:139128) $\xi \approx \xi_0$。这是非局域效应最显著的区域，因为[库珀对](@entry_id:143370)的尺寸最大 [@problem_id:2837254]。
*   **肮脏极限 (Dirty limit)**：当 $l \ll \xi_0$ 时，电子在形成相干配对的距离内会经历多次散射。这有效地将相干长度缩短为[平均自由程](@entry_id:139563)，即 $\xi \approx l$。

#### 肮脏极限下的局域性恢复与[穿透深度](@entry_id:136478)

一个看似矛盾但非常重要的结果是，在肮脏极限下，非局域效应反而被抑制了。由于有效[相干长度](@entry_id:139128) $\xi \approx l$ 变得很小，局域条件 $\xi \ll \lambda$ 更容易满足，从而使电动力学行为**恢复局域性** [@problem_id:2837254]。

然而，这种局域理论的穿透深度不同于理想的[伦敦穿透深度](@entry_id:143674) $\lambda_L$。在肮脏极限下，穿透深度会增加，其关系为：
$\lambda \approx \lambda_L \sqrt{\frac{\xi_0}{l}}$
这意味着增加杂质（减小 $l$）会使穿透深度变大，削弱了[超导体](@entry_id:191025)的[磁屏蔽](@entry_id:192877)能力。

在肮脏局域极限下，[超流体](@entry_id:180718)刚度（正比于 $1/\lambda^2$）与材料的正常态[电导率](@entry_id:137481) $\sigma_n$ 和零温[能隙](@entry_id:191975) $\Delta_0$ 之间存在一个优美的关系：$1/\lambda^2 \propto \sigma_n \Delta_0$ [@problem_id:2837254]。这个关系在实验上得到了验证，并为通过测量正常态性质来推断超导态参数提供了一条途径。

#### [安德森定理](@entry_id:139654)与杂质类型

需要区分不同类型的杂质。**[安德森定理](@entry_id:139654) (Anderson's theorem)** 指出，对于传统的 s-波[超导体](@entry_id:191025)，非磁性杂质不会改变其[热力学性质](@entry_id:146047)，如临界温度 $T_c$ 和[能隙](@entry_id:191975) $\Delta$。这是因为非磁性散射保持了[时间反演对称性](@entry_id:138094)，而这是[库珀配对](@entry_id:195218)所必需的。然而，磁性杂质会导致自旋翻转散射，破坏时间反演对称性，是一种强烈的**破对 (pair-breaking)** 机制。因此，磁性杂质会显著抑制 $T_c$、$\Delta_0$ 以及超流体密度 $n_s$，从而导致[超流体](@entry_id:180718)刚度 $1/\lambda^2$ 的迅速下降 [@problem_id:2837254]。

综上所述，[伦敦电动力学](@entry_id:191745)及其扩展为我们理解[超导体](@entry_id:191025)独特的电磁响应提供了坚实的理论框架。从[迈斯纳效应](@entry_id:273600)这一核心现象出发，我们构建了局域的[伦敦方程](@entry_id:139502)，并探讨了其在描述[磁场](@entry_id:153296)穿透、[表面电流](@entry_id:261791)以及不同响应模式方面的成功。同时，我们也认识到其局限性，并通过引入非局域性和杂质效应等概念，将其推广到更广泛、更真实的物理情境中。