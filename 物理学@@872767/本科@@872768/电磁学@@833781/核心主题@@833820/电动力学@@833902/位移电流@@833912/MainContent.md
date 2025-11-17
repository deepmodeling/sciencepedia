## 引言

在19世纪中叶，电磁学似乎已被划分为两个相对独立的领域：由[库仑定律](@entry_id:139360)和[高斯定律](@entry_id:141493)描述的[静电学](@entry_id:140489)，以及由[毕奥-萨伐尔定律](@entry_id:267294)和[安培环路定律](@entry_id:140092)描述的[静磁学](@entry_id:140120)。这些理论在处理静止[电荷](@entry_id:275494)和[稳恒电流](@entry_id:271551)时取得了巨大成功。然而，当物理学家试图将它们统一成一个能够描述动态过程（即随时间变化的电场和磁场）的普适理论时，一个深刻的内在矛盾便浮现出来：[安培环路定律](@entry_id:140092)与基本的电荷守恒定律在[非稳恒电流](@entry_id:268886)情况下发生了冲突。

本文的核心主题——[位移电流](@entry_id:190231)，正是James Clerk Maxwell为解决这一理论困境而提出的革命性概念。它不仅是一个巧妙的数学修正，更是一个深刻的物理洞见，揭示了变化的[电场](@entry_id:194326)同样可以作为[磁场](@entry_id:153296)的源。这一思想的引入，最终完成了电磁理论的统一，并直接导出了[电磁波](@entry_id:269629)存在的惊人预言，为我们理解光、无线电以及整个现代通信世界打开了大门。

为了系统地掌握这一关键概念，我们将分三个章节展开探讨：
*   在 **“原理与机制”** 中，我们将追溯位移电流的理论必然性，深入剖析其物理本质，并阐明它如何作为[磁场源](@entry_id:267241)解决了经典理论的矛盾。
*   在 **“应用与跨学科联系”** 中，我们将超越基础理论，通过[电容器](@entry_id:267364)、高频电子学、[材料科学](@entry_id:152226)、生物物理乃至广义相对论等领域的实例，展示[位移电流](@entry_id:190231)在科学与工程中的广泛应用和深远影响。
*   最后，在 **“动手实践”** 部分，我们将通过一系列精心设计的计算练习，帮助您将理论知识转化为解决实际问题的能力，从而巩固和深化对位移电流的理解。

## 原理与机制

在静电学和[静磁学](@entry_id:140120)中，安培环路定律将[稳恒电流](@entry_id:271551)与它所产生的[磁场](@entry_id:153296)联系起来。然而，当电场和磁场随时间变化时，这套理论框架便暴露出内在的矛盾。正是为了解决这一矛盾，James Clerk Maxwell 引入了一个革命性的概念——位移电流，它不仅完善了电磁理论，还预言了[电磁波](@entry_id:269629)的存在。本章将深入探讨位移电流的理论必然性、物理本质、及其作为[磁场源](@entry_id:267241)的机制。

### [安培定律](@entry_id:140092)在[时变场](@entry_id:180620)中的不自洽性

在19世纪，安培环路定律的微分形式被表述为 $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}$，其中 $\mathbf{B}$ 是[磁感应强度](@entry_id:144179)，$\mu_0$ 是[真空磁导率](@entry_id:186031)，$\mathbf{J}$ 是传导电流密度。这个定律在[稳恒电流](@entry_id:271551)（即[电流密度](@entry_id:190690)不随时间变化）的情况下非常成功。然而，当应用于[非稳恒电流](@entry_id:268886)的情景时，一个深刻的矛盾便显现出来。

这个矛盾源于它与另一个基本物理原理——电荷守恒定律——的冲突。电荷守恒定律的局域表达式，即[连续性方程](@entry_id:195013)，写作 $\nabla \cdot \mathbf{J} + \frac{\partial \rho}{\partial t} = 0$，其中 $\rho$ 是电荷密度。这个方程表明，任何从一个微小体积中流出的净电流，都必须等于该体积内[电荷](@entry_id:275494)量的减少率。

现在，让我们审视[安培定律](@entry_id:140092)的数学结构。一个基本的矢量恒等式是，任何旋度场的散度恒为零，即 $\nabla \cdot (\nabla \times \mathbf{A}) = 0$ 对于任意矢量场 $\mathbf{A}$ 都成立。将这个恒等式应用于安培定律的左侧，我们得到 $\nabla \cdot (\nabla \times \mathbf{B}) = 0$。这意味着，[安培定律](@entry_id:140092)的右侧也必须有为零的散度：$\mu_0 (\nabla \cdot \mathbf{J}) = 0$。因此，原始的安培定律隐含地要求 $\nabla \cdot \mathbf{J} = 0$。

这正是矛盾所在。根据连续性方程，$\nabla \cdot \mathbf{J} = - \frac{\partial \rho}{\partial t}$。因此，原始安培定律只在 $\frac{\partial \rho}{\partial t} = 0$ 的情况下才与[电荷守恒](@entry_id:264158)兼容，也就是在电荷密度不随时间变化的静电或[稳恒电流](@entry_id:271551)情况下。然而，在许多物理过程中，比如给[电容器充电](@entry_id:270179)时，[电荷](@entry_id:275494)在[电容器](@entry_id:267364)极板上积聚，$\rho$ 显然随时间变化，导致 $\frac{\partial \rho}{\partial t} \neq 0$ [@problem_id:1859410]。

我们可以通过一个思想实验来更直观地理解这个悖论 [@problem_id:1619362]。考虑一个正在充电的平行板电容器。我们取一个环绕着连接[电容器](@entry_id:267364)极板的导线的[安培环路](@entry_id:275261) $\mathcal{C}$。根据[安培定律的积分形式](@entry_id:270391) $\oint_{\mathcal{C}} \mathbf{B} \cdot d\mathbf{l} = \mu_0 I_{enc}$，[环路积分](@entry_id:164828)的值应该由穿过以该环路为边界的任意[曲面](@entry_id:267450) $\mathcal{S}$ 的电流 $I_{enc}$ 决定。
1.  如果我们选择一个简单的平面圆盘形[曲面](@entry_id:267450) $\mathcal{S}_1$，它被导线垂直穿过，那么穿过它的电流就是导线中的传导电流 $I$。
2.  然而，如果我们选择一个“袋状”[曲面](@entry_id:267450) $\mathcal{S}_2$，它也以环路 $\mathcal{C}$ 为边界，但它包裹住[电容器](@entry_id:267364)的一个极板，并从两极板之间的间隙穿过。由于没有[电荷](@entry_id:275494)载流子（传导电流）穿过[电容器](@entry_id:267364)两板间的真空或[电介质](@entry_id:147163)，穿过 $\mathcal{S}_2$ 的传导电流 $I_{enc}$ 为零。

对于同一个[安培环路](@entry_id:275261) $\mathcal{C}$，[磁场](@entry_id:153296)的[环路积分](@entry_id:164828) $\oint_{\mathcal{C}} \mathbf{B} \cdot d\mathbf{l}$ 必须是唯一的，但我们却根据所选[曲面](@entry_id:267450)的不同得出了两个矛盾的结果（$\mu_0 I$ 和 $0$）。这清楚地表明，原始的安培定律在处理时变问题时是不完备的。

### [麦克斯韦的修正](@entry_id:266656)：[位移电流](@entry_id:190231)

为了解决这一矛盾，Maxwell 提出，[安培定律](@entry_id:140092)需要增加一个修正项。他假设，变化的[电场](@entry_id:194326)本身就可以作为[磁场](@entry_id:153296)的源，就像[传导电流](@entry_id:265343)一样。这个新的[源项](@entry_id:269111)被称为 **位移电流 (displacement current)**。修正后的[安培-麦克斯韦定律](@entry_id:266368)的微分形式为：
$$
\nabla \times \mathbf{B} = \mu_0 (\mathbf{J} + \mathbf{J}_{d})
$$
其中 $\mathbf{J}_{d}$ 就是 **[位移电流](@entry_id:190231)密度 (displacement current density)**。

为了使这个修正后的定律与电荷守恒普遍兼容，我们必须确定 $\mathbf{J}_{d}$ 的形式。再次对上式两边取散度：
$$
\nabla \cdot (\nabla \times \mathbf{B}) = 0 = \mu_0 (\nabla \cdot \mathbf{J} + \nabla \cdot \mathbf{J}_{d})
$$
这要求 $\nabla \cdot \mathbf{J}_d = - \nabla \cdot \mathbf{J}$。结合连续性方程 $\nabla \cdot \mathbf{J} = - \frac{\partial \rho}{\partial t}$，我们得到一个关于位移电流密度的关键条件：
$$
\nabla \cdot \mathbf{J}_{d} = \frac{\partial \rho}{\partial t}
$$
这个关系表明，位移电流密度的“源”是[电荷密度](@entry_id:144672)的变化率。现在，我们需要将这个关系与[电场](@entry_id:194326)联系起来。高斯定律给出了[电场](@entry_id:194326)与[电荷密度](@entry_id:144672)的关系：$\nabla \cdot \mathbf{E} = \rho / \varepsilon_0$（在真空中）。对[高斯定律](@entry_id:141493)两边取时间[偏导数](@entry_id:146280)，得到：
$$
\nabla \cdot \left(\frac{\partial \mathbf{E}}{\partial t}\right) = \frac{1}{\varepsilon_0} \frac{\partial \rho}{\partial t} \quad \implies \quad \frac{\partial \rho}{\partial t} = \varepsilon_0 \nabla \cdot \left(\frac{\partial \mathbf{E}}{\partial t}\right)
$$
比较我们得到的两个关于 $\frac{\partial \rho}{\partial t}$ 的表达式，可以发现：
$$
\nabla \cdot \mathbf{J}_{d} = \nabla \cdot \left(\varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}\right)
$$
为了满足这个条件，最简洁、最自然的选择就是 [@problem_id:1859410]：
$$
\mathbf{J}_{d} = \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}
$$
将此定义代入，我们便得到了完整的 **[安培-麦克斯韦定律](@entry_id:266368)**：
$$
\nabla \times \mathbf{B} = \mu_0 \left(\mathbf{J} + \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}\right)
$$
在[电介质](@entry_id:147163)中，我们通常使用[电位移矢量](@entry_id:197092) $\mathbf{D} = \varepsilon \mathbf{E}$，其中 $\varepsilon$ 是介质的[介电常数](@entry_id:146714)。此时，位移电流密度的更普适定义是 $\mathbf{J}_d = \frac{\partial \mathbf{D}}{\partial t}$。

重要的是要强调，**位移电流不是真实[电荷](@entry_id:275494)的流动**。它是一个与 **[时变电场](@entry_id:197741)** 相关联的物理量，其在产生[磁场](@entry_id:153296)方面扮演着与真实[电荷](@entry_id:275494)流动（[传导电流](@entry_id:265343)）等效的角色。

### 位移电流的物理本质与电路的完备性

引入位移电流的概念后，我们可以重新审视充电[电容器](@entry_id:267364)的悖论。[安培-麦克斯韦定律](@entry_id:266368)的积分形式是：
$$
\oint_{\mathcal{C}} \mathbf{B} \cdot d\mathbf{l} = \mu_0 (I_{c,enc} + I_{d,enc})
$$
其中 $I_{c,enc} = \iint_{\mathcal{S}} \mathbf{J} \cdot d\mathbf{A}$ 是穿过[曲面](@entry_id:267450) $\mathcal{S}$ 的[传导电流](@entry_id:265343)，而 **总位移电流** $I_{d,enc}$ 定义为：
$$
I_{d,enc} = \iint_{\mathcal{S}} \mathbf{J}_d \cdot d\mathbf{A} = \iint_{\mathcal{S}} \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t} \cdot d\mathbf{A} = \varepsilon_0 \frac{d\Phi_E}{dt}
$$
这里 $\Phi_E = \iint_{\mathcal{S}} \mathbf{E} \cdot d\mathbf{A}$ 是穿过同一[曲面](@entry_id:267450)的[电通量](@entry_id:266049)。

现在，让我们回到[电容器](@entry_id:267364)的例子[@problem_id:1619362]：
1.  对于穿过导线的平面[曲面](@entry_id:267450) $\mathcal{S}_1$，[电场](@entry_id:194326)不随时间变化（假设导线外没有[时变电场](@entry_id:197741)），因此 $\frac{d\Phi_E}{dt} = 0$，而传导电流为 $I$。所以右侧为 $\mu_0 I$。
2.  对于穿过[电容器](@entry_id:267364)间隙的袋状[曲面](@entry_id:267450) $\mathcal{S}_2$，传导电流为零，但由于极板上[电荷](@entry_id:275494)的累积，两板间的[电场](@entry_id:194326) $\mathbf{E}$ 正在增强。这导致穿过 $\mathcal{S}_2$ 的[电通量](@entry_id:266049) $\Phi_E$ 随时间变化，从而产生一个非零的位移电流 $I_d = \varepsilon_0 \frac{d\Phi_E}{dt}$。可以证明，这个[位移电流](@entry_id:190231)的大小恰好等于导线中的传导电流 $I$。因此，对于 $\mathcal{S}_2$，定律的右侧也变为 $\mu_0 I_d = \mu_0 I$。

这样，无论我们选择哪个[曲面](@entry_id:267450)，[安培-麦克斯韦定律](@entry_id:266368)都给出了相同的结果，悖论得以解决。位移电流完美地“接续”了[传导电流](@entry_id:265343)，使得电流在某种意义上形成了一个完整的回路：传导电流在导线中流动，位移电流在[电容器](@entry_id:267364)的间隙中“流动”。

我们可以从一个更根本的层面来理解这种“电路的完备性”。定义 **总[电流密度](@entry_id:190690)** 为 $\mathbf{J}_{tot} = \mathbf{J} + \mathbf{J}_d = \mathbf{J} + \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}$。计算它的散度：
$$
\nabla \cdot \mathbf{J}_{tot} = \nabla \cdot \mathbf{J} + \nabla \cdot \left(\varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}\right)
$$
利用连续性方程 $\nabla \cdot \mathbf{J} = -\frac{\partial \rho}{\partial t}$ 和[高斯定律的微分形式](@entry_id:191832) $\rho = \varepsilon_0 \nabla \cdot \mathbf{E}$，上式变为：
$$
\nabla \cdot \mathbf{J}_{tot} = -\frac{\partial \rho}{\partial t} + \varepsilon_0 \frac{\partial}{\partial t}(\nabla \cdot \mathbf{E}) = -\frac{\partial \rho}{\partial t} + \frac{\partial \rho}{\partial t} = 0
$$
这表明，总[电流密度](@entry_id:190690) $\mathbf{J}_{tot}$ 是一个无散度的矢量场 [@problem_id:1825582]。根据[散度定理](@entry_id:143110)，穿过任何闭合[曲面](@entry_id:267450)的总电流通量恒为零。这意味着总电流（传导电流与位移电流之和）形成了连续不断的闭合流线。对于[电容器](@entry_id:267364)而言，流入一个极板的[传导电流](@entry_id:265343)，等于从该极板周围空间流出的位移电流 [@problem_id:1825582]。

需要注意的是，位移电流是由[电场](@entry_id:194326)的变化率产生的。如果[电场](@entry_id:194326)是静止的，即使它很强，[位移电流](@entry_id:190231)也为零。例如，对于一个被单个静止点电荷 $q$ 包围的任意闭合[曲面](@entry_id:267450)，穿过该[曲面](@entry_id:267450)的[电通量](@entry_id:266049) $\Phi_E = q/\varepsilon_0$ 是一个常数。因此，通过这个闭合[曲面](@entry_id:267450)的总位移电流为 $I_d = \varepsilon_0 \frac{d\Phi_E}{dt} = 0$ [@problem_id:1825546]。

### 作为[磁场源](@entry_id:267241)的位移电流

[安培-麦克斯韦定律](@entry_id:266368)指出，[时变电场](@entry_id:197741)（通过位移电流）和[传导电流](@entry_id:265343)一样，都是[磁场](@entry_id:153296)的源。让我们来计算由[位移电流](@entry_id:190231)产生的[磁场](@entry_id:153296)。以一个正在以恒定电流 $I$ 充电的圆形平行板电容器为例，其极板半径为 $R$。

假设两板间的[电场](@entry_id:194326) $\mathbf{E}$ 是均匀的。那么，流经整个[电容器](@entry_id:267364)间隙的总[位移电流](@entry_id:190231) $I_d$ 等于传导电流 $I$。这意味着 $\varepsilon_0 \frac{d(E \cdot \pi R^2)}{dt} = I$，所以[电场](@entry_id:194326)的变化率为 $\frac{dE}{dt} = \frac{I}{\varepsilon_0 \pi R^2}$。[位移电流](@entry_id:190231)密度在两板间是均匀的，大小为 $J_d = \varepsilon_0 \frac{dE}{dt} = \frac{I}{\pi R^2}$。

现在，我们可以在[电容器](@entry_id:267364)内部，于一个半径为 $r  R$ 的同轴圆形[安培环路](@entry_id:275261)上应用[安培-麦克斯韦定律](@entry_id:266368)。由于对称性，[磁场](@entry_id:153296) $\mathbf{B}$ 应该是指向[方位角](@entry_id:164011)方向的，并且在环路上大小恒定。环路内部没有[传导电流](@entry_id:265343)，只有位移电流。穿过这个半径为 $r$ 的圆盘的[位移电流](@entry_id:190231)为：
$$
I_{d,enc}(r) = J_d \times (\pi r^2) = \frac{I}{\pi R^2} \pi r^2 = I \frac{r^2}{R^2}
$$
这个结果本身就是一个重要的洞察：[位移电流](@entry_id:190231)是[分布](@entry_id:182848)在整个区域的 [@problem_id:1570488]。应用定律：
$$
\oint \mathbf{B} \cdot d\mathbf{l} = B(r) \cdot (2\pi r) = \mu_0 I_{d,enc}(r) = \mu_0 I \frac{r^2}{R^2}
$$
解出[磁场](@entry_id:153296)大小为：
$$
B(r) = \frac{\mu_0 I}{2\pi R^2} r
$$
这个结果表明，在充电[电容器](@entry_id:267364)的内部，[磁场](@entry_id:153296)从中心轴的零值开始线性增加，这与在具有均匀电流密度的导线内部的[磁场](@entry_id:153296)[分布](@entry_id:182848)形式完全相同。这雄辩地证明了[位移电流](@entry_id:190231)确实是[磁场](@entry_id:153296)的真实来源。

这一原理可以推广到更复杂的情况，例如当[电容器](@entry_id:267364)内部填充了非均匀的[电介质](@entry_id:147163)时 [@problem_id:1825572]。在这种情况下，使用更普适的[位移电流](@entry_id:190231)密度 $\mathbf{J}_d = \frac{\partial \mathbf{D}}{\partial t} = \frac{\partial (\varepsilon(r) \mathbf{E})}{\partial t}$，通[过积分](@entry_id:753033)计算出包围的[位移电流](@entry_id:190231)，同样可以求得感应出的[磁场](@entry_id:153296)。

位移电流的概念不仅限于[电容器](@entry_id:267364)。任何产生[时变电场](@entry_id:197741)的物理过程都会伴随着[位移电流](@entry_id:190231)。一个经典的例子是一个以恒定速度运动的[点电荷](@entry_id:263616) [@problem_id:1790066]。当这个[电荷](@entry_id:275494)飞过一个固定的线圈时，它产生的[电场](@entry_id:194326)在线圈所围面积上的通量会发生变化。这个变化的[电通量](@entry_id:266049) $\frac{d\Phi_E}{dt}$ 会产生一个瞬时的[位移电流](@entry_id:190231) $I_d = \varepsilon_0 \frac{d\Phi_E}{dt}$，这个位移电流又会在线圈周围感应出一个瞬时的[磁场](@entry_id:153296)。

### [位移电流](@entry_id:190231)与传导电流的相对重要性

在不同的物理条件下，[位移电流](@entry_id:190231)和[传导电流](@entry_id:265343)的相对重要性差异巨大。

在一个良导体（如铜线）中，即使是交流电，[位移电流](@entry_id:190231)通常也可以忽略不计。考虑一根承载频率为 $f = 60 \text{ Hz}$ 交流电的铜线。导线内的[电场](@entry_id:194326) $\mathbf{E}$ 随时间正弦变化。传导电流密度为 $\mathbf{J}_c = \sigma \mathbf{E}$，[位移电流](@entry_id:190231)密度为 $\mathbf{J}_d = \varepsilon \frac{\partial \mathbf{E}}{\partial t}$。对于正弦场，$\frac{\partial \mathbf{E}}{\partial t}$ 的幅值是 $\omega E_0 = 2\pi f E_0$。因此，两种电流密度的幅值之比为：
$$
\frac{|\mathbf{J}_{d, \text{max}}|}{|\mathbf{J}_{c, \text{max}}|} = \frac{\varepsilon \omega E_0}{\sigma E_0} = \frac{2\pi f \varepsilon}{\sigma}
$$
使用铜的电导率 $\sigma \approx 6 \times 10^7 \, (\Omega \cdot \text{m})^{-1}$ 和[介电常数](@entry_id:146714) $\varepsilon \approx \varepsilon_0 = 8.85 \times 10^{-12} \text{ F/m}$，我们得到这个比值约为 $5.6 \times 10^{-17}$ [@problem_id:1825521]。这是一个极小的数值，表明在低频下的良导体中，位移电流完全可以被忽略，[磁场](@entry_id:153296)几乎完全由[传导电流](@entry_id:265343)产生。

然而，在不良导体或[电介质](@entry_id:147163)中，以及在高频下，情况则大不相同。上述比值 $\frac{\varepsilon \omega}{\sigma}$ 是一个关键的[无量纲参数](@entry_id:169335)。我们可以定义一个 **[交叉](@entry_id:147634)频率 (crossover frequency)** $\omega_c = \sigma / \varepsilon$，在该频率下，位移电流的幅值等于[传导电流](@entry_id:265343)的幅值 [@problem_id:1613184]。
- 当驱动频率 $\omega \ll \omega_c$ 时，传导电流占主导地位，材料表现为导体。
- 当驱动频率 $\omega \gg \omega_c$ 时，位移电流占主导地位，材料表现为[电介质](@entry_id:147163)。

这个概念对于[高频电路设计](@entry_id:267137)、[微波工程](@entry_id:274335)以及[材料科学](@entry_id:152226)至关重要，它决定了材料在特定电磁频率下的响应是类导体的（耗散能量）还是类介质的（储存能量）。

### 能量考量

[位移电流](@entry_id:190231)的引入也与[电磁场](@entry_id:265881)的[能量守恒](@entry_id:140514)密切相关。外场对电流做功的[功率密度](@entry_id:194407)为 $\mathbf{E} \cdot \mathbf{J}_{tot}$。在没有传导电流的介质中，这简化为 $\mathbf{E} \cdot \mathbf{J}_d$。在标准的静态介质中（$\varepsilon$ 为常数），我们有：
$$
P_V = \mathbf{E} \cdot \mathbf{J}_d = \mathbf{E} \cdot \left(\varepsilon \frac{\partial \mathbf{E}}{\partial t}\right) = \frac{\varepsilon}{2} \frac{\partial}{\partial t}(\mathbf{E} \cdot \mathbf{E}) = \frac{\partial}{\partial t}\left(\frac{1}{2}\varepsilon E^2\right) = \frac{\partial u_E}{\partial t}
$$
其中 $u_E = \frac{1}{2} \mathbf{E} \cdot \mathbf{D}$ 是[电场能量密度](@entry_id:261497)。这个结果表明，在这种情况下，外场对位移电流做的功完全转化为储存的[电场能量](@entry_id:193072)的增加率。

然而，在一个更复杂的情况下，例如介质本身的性质随时间变化（即 $\varepsilon(t)$），能量的流动会变得更加微妙 [@problem_id:1825544]。此时，位移电流密度为 $\mathbf{J}_d = \frac{\partial}{\partial t}(\varepsilon(t) \mathbf{E}(t)) = \frac{d\varepsilon}{dt}\mathbf{E} + \varepsilon \frac{\partial \mathbf{E}}{\partial t}$。
[电场](@entry_id:194326)提供的[功率密度](@entry_id:194407)为：
$$
P_V = \mathbf{E} \cdot \mathbf{J}_d = \frac{d\varepsilon}{dt}E^2 + \varepsilon \mathbf{E} \cdot \frac{\partial \mathbf{E}}{\partial t}
$$
而[电场能量密度](@entry_id:261497) $u_E = \frac{1}{2} \varepsilon E^2$ 的变化率为：
$$
R_U = \frac{\partial u_E}{\partial t} = \frac{1}{2} \frac{d\varepsilon}{dt} E^2 + \varepsilon \mathbf{E} \cdot \frac{\partial \mathbf{E}}{\partial t}
$$
这两者之间的差值为：
$$
P_V - R_U = \frac{1}{2} \frac{d\varepsilon}{dt} E^2
$$
这个非零的差值意味着，当[介电常数](@entry_id:146714)随时间变化时，[电场](@entry_id:194326)做的功并不仅仅用于增加[电场能量](@entry_id:193072)。其中一部分能量被用于改变介质本身的状态。如果 $\frac{d\varepsilon}{dt} > 0$，则需要额外的能量来“构建”这种增强的介电性能；反之，如果介质的[极化能力](@entry_id:151274)减弱（$\frac{d\varepsilon}{dt}  0$），则能量会从介质释放回[电磁场](@entry_id:265881)。这揭示了场与物质之间能量交换的更深层次的机制。

总之，位移电流不仅是一个为满足理论自洽性而引入的数学工具，它更是一个深刻的物理实在。它代表了[时变电场](@entry_id:197741)作为[磁场源](@entry_id:267241)的能力，是理解[电磁波传播](@entry_id:272130)、高频电路行为以及场与物质相互作用的关键。没有位移电流，电磁学将停留在静态和准静态的领域，而一个包含光、无线电和所有电磁辐射的动态宇宙将无法被理论所描述。