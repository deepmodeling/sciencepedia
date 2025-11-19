## 引言
多晶体材料的性能，从金属的强度到[半导体](@entry_id:141536)的电学特性，都深刻地受到其内部微观结构的影响。其中，晶体织构——即构成材料的无数晶粒的[择优取向](@entry_id:190900)[分布](@entry_id:182848)——是决定其宏观各向异性行为的核心因素。然而，一个根本性的挑战在于，我们如何建立从单个晶粒的微观变形到整个材料宏观响应的可靠联系？这篇文章旨在系统性地解决这一问题，深入探讨塑性变形过程中织构演化的完整图景。

在本文中，我们将踏上一段跨越尺度的理论旅程。首先，在“原理与机制”章节中，我们将奠定理论基石，学习如何用[取向分布函数](@entry_id:191240)（ODF）精确描述织构，并揭示晶体滑移如何通过复杂的[运动学](@entry_id:173318)关系驱动[晶格](@entry_id:196752)旋转，进而改变织构。接着，在“应用与跨学科联系”章节中，我们将看到这些理论如何解释和预测真实的材料现象，从[金属成形](@entry_id:188560)中的各向异性到先进功能材料的可靠性。最后，“动手实践”部分将提供具体的计算练习，帮助您巩固对取向差、[极图](@entry_id:260961)和泰勒因子等关键概念的理解。

让我们首先进入第一章，深入剖析驱动织构演化的基本原理与物理机制。

## 原理与机制

在理解多晶体材料的宏观力学行为时，一个核心挑战在于如何描述和预测其内部微观结构在变形过程中的演化。晶体织构，即构成材料的众多晶粒的取向[分布](@entry_id:182848)，是决定[材料各向异性](@entry_id:204117)属性的关键因素。本章旨在深入阐述描述、驱动并控制织构演化的基本原理与物理机制。我们将从织构的数学描述出发，继而探讨塑性变形的微观根源，建立[晶格](@entry_id:196752)旋转与微观滑移之间的[运动学](@entry_id:173318)关联，并最终将这些概念整合为描述织构演化过程的宏观理论框架。

### 织构的定量描述：[取向分布函数](@entry_id:191240)

描述织构最完整的方式是使用**[取向分布函数](@entry_id:191240) (Orientation Distribution Function, ODF)**，通常记为 $f(g)$。这里的 $g$ 是一个数学对象，代表单个晶粒的取向。具体而言，$g$ 是一个属于**[三维特殊正交群](@entry_id:138200)** $\mathrm{SO}(3)$ 的[旋转矩阵](@entry_id:140302)，它将晶体[坐标系](@entry_id:156346)下的矢量映射到样品（或实验室）[坐标系](@entry_id:156346)下。

从更严格的数学角度来看，ODF $f(g)$ 是一个定义在群 $\mathrm{SO}(3)$ 上的[概率密度函数](@entry_id:140610) [@problem_id:2693628]。要理解“密度”，我们需要一个参照体积。在 $\mathrm{SO}(3)$ 这个弯曲的取向空间中，其“均匀体积元”由所谓的**[哈尔测度](@entry_id:142417) (Haar measure)** $d\mu(g)$ 给出。我们将此测度归一化，使得整个取向空间的总“体积”为 $\mu(\mathrm{SO}(3))=1$。这样，$f(g)d\mu(g)$ 就代表了晶粒取向落在 $g$ 附近一个无穷小邻域内的体积分数。ODF具有两个基本属性：

1.  **非负性**: 作为[概率密度](@entry_id:175496)，$f(g) \ge 0$ 几乎在所有取向上成立。
2.  **归一化**: 所有晶粒的[体积分数](@entry_id:756566)之和必须为1，这意味着ODF在整个取向空间上的积分为1：
    $$ \int_{\mathrm{SO}(3)} f(g)\,d\mu(g) = 1 $$

对于一个完全没有织构、所有取向完全随机[分布](@entry_id:182848)的材料，其ODF为常数 $f(g)=1$。任何偏离1的值都表示存在某种[择优取向](@entry_id:190900)。

材料的对称性对ODF的形式施加了重要约束 [@problem_id:2693628]。
- **晶体对称性**: 晶体本身具有对称性，例如面心立方(FCC)晶体具有立方对称性。这意味着物理上无法区分通过对称操作 $s$ (属于晶体[对称群](@entry_id:146083) $S$) 相关联的两个取向 $g$ 和 $gs$。因此，ODF必须满足**右不变性**: $f(g) = f(gs)$ 对所有 $s \in S$ 成立。
- **样品对称性**: 材料的加工过程（如轧制、拉伸）可能赋予样品宏观上的对称性。例如，轧制板材通常具有[正交对](@entry_id:164779)称性。如果样品在宏观操作 $h$ (属于样品对称群 $H$) 下保持不变，那么取向 $g$ 和 $hg$ 对应的物理状态就是等价的。因此，ODF必须满足**左不变性**: $f(g) = f(hg)$ 对所有 $h \in H$ 成立。

虽然ODF提供了织构的完整信息，但它无法直接通过实验测量。实验中更易获取的是**[极图](@entry_id:260961) (Pole Figure)**，记为 $P_h(\hat{n})$。[极图](@entry_id:260961)描述的是某个特定的[晶向](@entry_id:137393)族（例如，FCC晶体中的 $\{100\}$ [法线](@entry_id:167651)方向）在样品[坐标系](@entry_id:156346)中的[空间分布](@entry_id:188271)密度 [@problem_id:2693606]。

ODF与[极图](@entry_id:260961)之间的关系是一个**第一类[Fredholm积分方程](@entry_id:277002)**。给定一个[晶体学](@entry_id:140656)方向 $\hat{h}$（以晶体[坐标系](@entry_id:156346)中的单位矢量表示），一个取向为 $g$ 的晶粒会将其映射到样品[坐标系](@entry_id:156346)中的方向 $\hat{n} = g\hat{h}$。为了构建完整的[极图](@entry_id:260961)，我们必须考虑以下几点：
1.  **[晶体对称性](@entry_id:198772)**：必须对所有[晶体学](@entry_id:140656)上等效的方向 $t \in \mathcal{S}_h$ (其中 $\mathcal{S}_h$ 是由晶体对称群作用于 $\hat{h}$ 生成的等效方向集合) 进行求和。该集合的大小，即**[多重性](@entry_id:136466)因子 (multiplicity factor)** $M_h$，代表了该[晶向](@entry_id:137393)族的等效方向数目。
2.  **弗里德尔定律 (Friedel's Law)**：标准的X射线衍射实验无法区分方向 $\hat{n}$ 和其反方向 $-\hat{n}$。因此，测得的极[图密度](@entry_id:268958)是这两个方向真实密度的平均值。
3.  **归一化**：为了便于比较，[极图](@entry_id:260961)通常被归一化，使其在单位球面上的积分为特定值，例如，[球平均](@entry_id:165984)值为1 [@problem_id:2693579]。

综合以上因素，[极图](@entry_id:260961) $P_h(\hat{n})$ 可以通过对ODF $f(g)$ 进行积分得到：
$$
P_h(\hat{n}) = \frac{1}{2 M_h} \int_{\mathrm{SO}(3)} f(g) \sum_{t \in \mathcal{S}_h} \left[ \delta(\hat{n} - gt) + \delta(\hat{n} + gt) \right] dg
$$
其中 $\delta(\cdot)$ 是定义在单位球面上的狄拉克δ函数，它保证了只有当晶粒取向 $g$ 恰好将某个等效[晶向](@entry_id:137393) $t$ 映射到 $\hat{n}$ 或 $-\hat{n}$ 时，该晶粒才会对[极图](@entry_id:260961)在该点有贡献。这个方程是[织构分析](@entry_id:202600)的基石，它将不可测量的ODF与可测量的[极图](@entry_id:260961)联系起来，使得从实验数据反演ODF成为可能。

### 塑性变形的物理机制：晶体滑移

织构的演化主要由塑性变形驱动。在晶体材料中，塑性变形的主要微观机制是**晶体滑移 (crystallographic slip)**。滑移是指晶体的一部分相对于另一部分在特定的**滑移面 (slip plane)**上沿着特定的**滑移方向 (slip direction)**发生剪切运动。一个滑移面法线 $\boldsymbol{n}_s$ 和一个滑移方向 $\boldsymbol{m}_s$ (满足 $\boldsymbol{m}_s \cdot \boldsymbol{n}_s = 0$)共同定义了一个**[滑移系](@entry_id:136401) (slip system)** $s$。

驱动滑移的力是**分切剪应力 (resolved shear stress, RSS)**，记为 $\tau_s$。它是在[滑移面](@entry_id:158709)上作用于滑移方向的剪应力分量。给定晶粒承受的柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$，[滑移面](@entry_id:158709)上的牵[引力](@entry_id:175476)矢量为 $\boldsymbol{t} = \boldsymbol{\sigma} \cdot \boldsymbol{n}_s$。将此牵[引力](@entry_id:175476)投影到滑移方向上，即可得到分切剪应力 [@problem_id:2693637]：
$$
\tau_s = \boldsymbol{m}_s \cdot (\boldsymbol{\sigma} \cdot \boldsymbol{n}_s)
$$
这个表达式也可以通过引入**施密特张量 (Schmid tensor)** $P_s$ 以更紧凑的形式书写。施密特张量定义为滑移方向和[滑移面](@entry_id:158709)法线的对称组合：
$$
\boldsymbol{P}_s = \frac{1}{2}(\boldsymbol{m}_s \otimes \boldsymbol{n}_s + \boldsymbol{n}_s \otimes \boldsymbol{m}_s)
$$
利用张量[双点积](@entry_id:748648)的性质，分切剪应力可以表示为：
$$
\tau_s = \boldsymbol{\sigma} : \boldsymbol{P}_s
$$
施密特张量是**对称**且**无迹**的（$\mathrm{tr}(\boldsymbol{P}_s) = \boldsymbol{m}_s \cdot \boldsymbol{n}_s = 0$）。这一无迹特性揭示了一个深刻的物理事实：只有[应力张量](@entry_id:148973)的**偏量部分** $\mathrm{dev}\,\boldsymbol{\sigma} = \boldsymbol{\sigma} - \frac{1}{3}(\mathrm{tr}\,\boldsymbol{\sigma}) \boldsymbol{I}$ 才能驱动滑移，而**静水压力**部分 $(\mathrm{tr}\,\boldsymbol{\sigma}) \boldsymbol{I}$ 对分切剪应力没有贡献。这意味着在经典滑移理论中，[晶体塑性](@entry_id:141273)是压力无关的 [@problem_id:2693637]。

滑移何时发生以及速率如何，由材料的**[本构定律](@entry_id:178936) (constitutive law)** 决定。
- **率无关塑性 (Rate-Independent Plasticity)**：最简单的模型是**施密特定律 (Schmid's Law)**，它假设滑移只在分切剪应力的大小达到一个临界的阈值，即**临界分切剪应力 (critical resolved shear stress, CRSS)** $\tau_c$ 时才会发生。即当 $|\tau_s| = \tau_c$ 时，[滑移系](@entry_id:136401)被激活。根据热力学第二定律，[塑性耗散](@entry_id:201273)必须为非负，即 $\tau_s \dot{\gamma}_s \ge 0$，其中 $\dot{\gamma}_s$ 是滑移速率。这意味着滑移的方向总是与分切剪应力的方向一致 [@problem_id:2693637]。

- **率相关塑性 (Rate-Dependent Plasticity)**：在更实际的情况下，滑移速率与应力水平有关。一个广泛使用的模型是**[粘塑性](@entry_id:165397)[幂律](@entry_id:143404) (viscoplastic power law)** [@problem_id:2693615]：
$$
\dot{\gamma}_s = \dot{\gamma}_0 \left| \frac{\tau_s}{g} \right|^{1/m} \mathrm{sign}(\tau_s)
$$
其中，$\dot{\gamma}_0$ 是一个参考剪切速率，$g$ 是[滑移系](@entry_id:136401)的当前强度（或阻力），而 $m$ 是**率敏感性指数 (rate sensitivity exponent)**。这个指数 $m$ 对织构演化的速度和模式有着至关重要的影响：
  - 当 $m \to 0$ 时，指数 $1/m \to \infty$。这意味着滑移速率对微小的应力变化极其敏感。只要 $|\tau_s|$ 稍低于 $g$，$\dot{\gamma}_s$ 就几乎为零；一旦 $|\tau_s|$ 达到 $g$，滑移速率可以变得非常大。这有效地恢复了率无关的施密特定律。在这种情况下，变形会高度集中在那些取向最有利（即施密特因子最高）的少数[滑移系](@entry_id:136401)上，导致[晶格](@entry_id:196752)发生剧烈旋转，从而形成尖锐的织构。
  - 当 $m \to 1$ 时，滑移速率与分切剪应力成线性关系，$\dot{\gamma}_s \propto \tau_s$。这类似于牛顿流体的行为。在这种情况下，几乎所有的[滑移系](@entry_id:136401)都会有不同程度的活动，即使是那些分切剪应力较小的[滑移系](@entry_id:136401)。变形[分布](@entry_id:182848)在众多[滑移系](@entry_id:136401)上，导致[晶格](@entry_id:196752)旋转较为平缓，形成的织构也相对较弱。

### [晶格](@entry_id:196752)旋转的[运动学](@entry_id:173318)

我们已经知道滑移是塑性变形的来源，但滑移是如何导致[晶格](@entry_id:196752)旋转的呢？这需要通过有限变形运动学来建立联系。

核心概念是**变形梯度的[乘法分解](@entry_id:199514) (multiplicative decomposition of the deformation gradient)** [@problem_id:2693583]。变形梯度 $\boldsymbol{F}$ 描述了从材料初始构型到当前构型的完整映射。在[晶体塑性理论](@entry_id:180579)中，$\boldsymbol{F}$ 被分解为两部分：
$$
\boldsymbol{F} = \boldsymbol{F}_e \boldsymbol{F}_p
$$
- $\boldsymbol{F}_p$ 是**塑性变形梯度**，它代表了由晶体滑移引起的材料重排。这个过程在概念上发生在一个虚拟的、无应力的**[中间构型](@entry_id:193000) (intermediate configuration)**中。关键在于，$\boldsymbol{F}_p$ 描述的纯滑移过程本身并**不**旋转[晶格](@entry_id:196752)。[中间构型](@entry_id:193000)中的[晶格](@entry_id:196752)取向与初始构型中的相同。
- $\boldsymbol{F}_e$ 是**弹性变形梯度**，它将材料从无应力的[中间构型](@entry_id:193000)映射到最终的、承受应力的当前构型。$\boldsymbol{F}_e$ 包含了两个部分：[晶格](@entry_id:196752)的弹性拉伸和[晶格](@entry_id:196752)的**刚体旋转**。

织构演化正是由这个[晶格](@entry_id:196752)的刚体旋转所驱动的。为了从 $\boldsymbol{F}_e$ 中分离出旋转部分，我们使用**极分解 (polar decomposition)**：
$$
\boldsymbol{F}_e = \boldsymbol{R}_e \boldsymbol{U}_e \quad \text{或} \quad \boldsymbol{F}_e = \boldsymbol{V}_e \boldsymbol{R}_e
$$
其中 $\boldsymbol{U}_e$ 和 $\boldsymbol{V}_e$ 分别是右和左弹性[拉伸张量](@entry_id:193200)，而 $\boldsymbol{R}_e$ 是一个正交旋转矩阵。这个 $\boldsymbol{R}_e$ 精确地描述了从初始状态到当前状态[晶格](@entry_id:196752)的净旋转，它代表了晶粒取向的改变。

在分析织构演化的速率时，我们更关心旋转的速率，即**[晶格自旋](@entry_id:198780) (lattice spin)**，记为 $\boldsymbol{W}^e = \dot{\boldsymbol{R}}_e \boldsymbol{R}_e^T$。通过对变形梯度分解进行速率形式的分析，可以推导出[晶格自旋](@entry_id:198780)与总变形及塑性变形之间的关键运动学关系。[速度梯度](@entry_id:261686) $\boldsymbol{L} = \dot{\boldsymbol{F}}\boldsymbol{F}^{-1}$ 可以分解为对称的**应变率张量 (rate of deformation tensor)** $\boldsymbol{D}$ 和反对称的**[自旋张量](@entry_id:187346) (spin tensor)** $\boldsymbol{W}$。假设[弹性应变](@entry_id:189634)很小，我们得到一个至关重要的关系 [@problem_id:2693567] [@problem_id:2693605]：
$$
\boldsymbol{W}^e \approx \boldsymbol{W} - \boldsymbol{W}^p
$$
这个方程表明，**[晶格自旋](@entry_id:198780)**近似等于**[总自旋](@entry_id:153335)**减去**塑性自旋**。[总自旋](@entry_id:153335) $\boldsymbol{W}$ 由外部施加的变形（边界条件）决定，而塑性自旋 $\boldsymbol{W}^p$ 是由晶体内部的滑移活动产生的。塑性[速度梯度](@entry_id:261686) $\boldsymbol{L}^p$ 是所有[滑移系](@entry_id:136401)贡献的总和：
$$
\boldsymbol{L}^p = \sum_s \dot{\gamma}_s \boldsymbol{m}_s \otimes \boldsymbol{n}_s
$$
塑性自旋 $\boldsymbol{W}^p$ 是 $\boldsymbol{L}^p$ 的反对称部分 [@problem_id:2693622]：
$$
\boldsymbol{W}^p = \mathrm{skw}(\boldsymbol{L}^p) = \frac{1}{2}(\boldsymbol{L}^p - \boldsymbol{L}^{pT}) = \sum_s \frac{\dot{\gamma}_s}{2} (\boldsymbol{m}_s \otimes \boldsymbol{n}_s - \boldsymbol{n}_s \otimes \boldsymbol{m}_s)
$$
这个封闭的框架完美地阐释了织构演化的机制：外部变形施加了[总自旋](@entry_id:153335) $\boldsymbol{W}$；应力驱动的滑移产生了塑性自旋 $\boldsymbol{W}^p$；二者的差值 $\boldsymbol{W}^e$ 导致了[晶格](@entry_id:196752)的旋转，从而改变了晶粒的取向，并最终演化了宏观织构。由于[滑移系](@entry_id:136401) $(\boldsymbol{m}_s, \boldsymbol{n}_s)$ 是固定在晶体上的，因此塑性自旋 $\boldsymbol{W}^p$ 的具体值取决于晶粒的当前取向，这就是为什么不同取向的晶粒会经历不同旋转的原因。

### 多晶体模型与织构演化

将单晶体的物理机制应用于由亿万晶粒组成的多晶体材料，需要引入**[多晶体](@entry_id:139228)模型 (polycrystal model)**。这些模型的目的在于处理晶粒间的相互作用，即如何在满足宏观变形的同时，协调每个晶粒的局部变形，并满足力学平衡。两个经典的极端模型是[泰勒模型](@entry_id:203285)和萨克斯模型。

#### [泰勒模型](@entry_id:203285) (Taylor Model)

**[泰勒模型](@entry_id:203285)**是一个基于**应变均匀**假设的模型 [@problem_id:2693567]。它假定每个晶粒内的[速度梯度](@entry_id:261686) $\boldsymbol{L}^{(g)}$ 都与宏观[速度梯度](@entry_id:261686) $\bar{\boldsymbol{L}}$ 完全相同。
- **假设**: $\boldsymbol{L}^{(g)} = \bar{\boldsymbol{L}}$ 对所有晶粒 $g$ 成立。
- **推论**: 这直接意味着每个晶粒的[应变率张量](@entry_id:266108) $\boldsymbol{D}^{(g)}$ 都等于宏观[应变率张量](@entry_id:266108) $\bar{\boldsymbol{D}}$。为了满足这个严苛的运动学约束，每个晶粒通常需要激活至少5个独立的[滑移系](@entry_id:136401)（对于FCC晶体）。
- **后果**: 这种“刚性”约束使得模型预测的[材料硬度](@entry_id:160499)偏高，通常被视为[材料强度](@entry_id:158701)的**上限**。由于每个晶粒都被迫变形，即使是取向不利的“硬”晶粒也必须通过多重滑移来适应变形，这导致了剧烈的[晶格](@entry_id:196752)旋转。因此，[泰勒模型](@entry_id:203285)通常预测出比实验观察更为尖锐的织构。该模型满足了运动学相容性，但牺牲了晶界处的应力平衡。
- **[晶格](@entry_id:196752)旋转计算**: 在[泰勒模型](@entry_id:203285)下，[晶格自旋](@entry_id:198780)的计算非常直接。由于 $\boldsymbol{W}^{(g)} = \bar{\boldsymbol{W}}$，[晶格自旋](@entry_id:198780)为 $\boldsymbol{W}^{e(g)} \approx \bar{\boldsymbol{W}} - \boldsymbol{W}^{p(g)}$。通过[求解方程组](@entry_id:152624) $\boldsymbol{D}^{p(g)} = \bar{\boldsymbol{D}}$ 得到各[滑移系](@entry_id:136401)的滑移速率 $\dot{\gamma}_s^{(g)}$，然后计算出塑性自旋 $\boldsymbol{W}^{p(g)}$，即可确定该取向晶粒的旋转速率 [@problem_id:2693605]。

#### 萨克斯模型 (Sachs Model)

与[泰勒模型](@entry_id:203285)相反，**萨克斯模型**基于**应力均匀**的假设 [@problem_id:2693604]。
- **假设**: $\boldsymbol{\sigma}^{(g)} = \bar{\boldsymbol{\sigma}}$ 对所有晶粒 $g$ 成立。
- **推论**: 在这个模型中，每个晶粒都承受相同的应力。根据施密特定律，只有那些分切剪应力最大的滑移系（通常只有一或两个）会被激活。取向有利的“软”晶粒会发生大量滑移，而“硬”晶粒则几乎不变形。
- **后果**: 该模型预测的[材料硬度](@entry_id:160499)偏低，被视为强度的**下限**。由于应变在晶粒间极不均匀，该模型严重违反了晶界处的**运动学相容性**（即晶粒间可能出现孔洞或重叠），但它满足了应[力平衡](@entry_id:267186)。在织构演化方面，由于只有部分“软”晶粒发生显著旋转，而大量“硬”晶粒保持不动，萨克斯模型预测的织构演化速度较慢，形成的织构也比[泰勒模型](@entry_id:203285)弱得多。

[泰勒模型](@entry_id:203285)和萨克斯模型分别代表了多晶体行为的两个理论极限（上界和下界），为理解更复杂的自洽模型等高级理论提供了重要的概念基础。

### 织构演化的宏观描述

前面讨论的都是单个晶粒的行为或其简单平均。为了描述整个织构，即ODF的演化，我们需要一个能够追踪取向空间中[概率密度](@entry_id:175496)流动的宏观方程。

这个方程就是**ODF[输运方程](@entry_id:756133)**，也称**[刘维尔方程](@entry_id:156422) (Liouville equation)** [@problem_id:2693580]。它本质上是在取向空间中的一个[连续性方程](@entry_id:195013)，表达了概率守恒：
$$
\frac{\partial f(g,t)}{\partial t} + \nabla_g \cdot (f(g,t) \dot{g}(g,t)) = 0
$$
这里：
- $\frac{\partial f}{\partial t}$ 是ODF在固定取向 $g$ 处的[局部时](@entry_id:194383)间变化率。
- $\dot{g}(g,t)$ 是取向空间中的“速度场”，它代表了取向为 $g$ 的晶粒的旋转角速度。这个速度场是由前述[晶体塑性](@entry_id:141273)模型计算出的[晶格自旋](@entry_id:198780) $\boldsymbol{W}^e$ 决定的。
- $\nabla_g \cdot$ 是在 $\mathrm{SO}(3)$ [流形上的散度](@entry_id:196026)算子。
- $\nabla_g \cdot (f\dot{g})$ 这一项代表了由于[晶格](@entry_id:196752)旋[转导](@entry_id:139819)致的[概率密度](@entry_id:175496)流的散度，即净流出率。

这个方程优雅地将[单晶塑性](@entry_id:754915)理论与宏观织构统计描述联系在一起。通过求解给定初始织构 $f(g,0)$ 和变形历史所产生的速度场 $\dot{g}(g,t)$ 下的这个[偏微分方程](@entry_id:141332)，原则上可以预测织构在任何时刻的状态。

此外，这个框架是可扩展的，可以包含除滑移之外的其他变形机制，例如**形变孪生 (deformation twinning)** [@problem_id:2693630]。孪生是一种导致[晶格](@entry_id:196752)部分区域发生瞬时、离散的大角度转动的机制。一个取向为 $g$ 的母体晶粒可以通过孪生变体 $v$ 突变为一个新的取向 $Q_v g$。这种离散的“跳跃”过程可以在ODF输运方程中通过添加**源项和汇项**来描述：
$$
\frac{\partial f}{\partial t} + \nabla_g \cdot (f \dot{g}) = \sum_v \left[ \text{源项}(g) - \text{汇项}(g) \right]
$$
- **汇项**描述了在取向 $g$ 处的晶粒由于发生孪生而“消失”的速率，它正比于 $f(g,t)$。
- **源项**描述了其他取向的晶粒（例如 $Q_v^{-1}g$）通过孪生转变为取向 $g$ 而“产生”的速率，它正比于 $f(Q_v^{-1}g, t)$。

经过这样的修正，ODF[输运方程](@entry_id:756133)就成为了一个能够同时处理连续（滑移）和离散（孪生）[演化机制](@entry_id:196221)的强大工具，为精确预测复杂加载路径下的织构演化提供了坚实的理论基础。