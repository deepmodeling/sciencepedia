## 引言
率相关[晶体塑性理论](@entry_id:180579)是连接微观[位错动力学](@entry_id:748548)与宏观[材料力学](@entry_id:201885)行为的关键桥梁，对于精确预测金属等晶体材料在不同[应变率](@entry_id:154778)和温度下的响应至关重要。传统的率无关塑性模型无法描述[蠕变](@entry_id:150410)、[应力松弛](@entry_id:159905)以及[应变率敏感性](@entry_id:188216)等时间依赖现象，从而在许多工程应用中暴露出其局限性。本文旨在系统性地填补这一认知空白，为读者构建一个完整而深入的率相关[晶体塑性理论](@entry_id:180579)知识体系。在接下来的内容中，我们将首先在“原理与机制”一章中，从晶体滑移的[运动学](@entry_id:173318)基础出发，建立有限变形框架下的本构关系与[硬化](@entry_id:177483)法则；随后，在“应用与跨学科交叉”一章中，我们将展示该理论如何用于模拟织构演化、[循环塑性](@entry_id:176411)等复杂现象，并探讨其与[热力学](@entry_id:141121)、计算科学等领域的交叉前沿；最后，通过“实践练习”部分，读者将有机会亲手推导和计算，将理论知识转化为解决实际问题的能力。

## 原理与机制

本章旨在阐述率相关[晶体塑性理论](@entry_id:180579)的基本原理与核心机制。在前一章介绍其背景和意义的基础上，我们将深入探讨描述[晶体塑性](@entry_id:141273)变形的[运动学](@entry_id:173318)和动力学框架，建立其[本构关系](@entry_id:186508)，并分析该理论在模拟各种材料现象中的重要作用。我们将从基本定义出发，逐步构建一个适用于有限变形的、[热力学一致的](@entry_id:755906)理论体系，并探讨其与率无关理论的本质区别及其在处理[应变局部化](@entry_id:176973)等复杂问题时的独特优势。

### 晶体滑移的运动学与动力学基础

晶体中的塑性变形主要通过[位错](@entry_id:157482)在特定晶面（滑移面）上沿特定[晶向](@entry_id:137393)（滑移方向）运动所产生的剪切（即滑移）来实现。每一对滑移方向与[滑移面](@entry_id:158709)共同构成一个**滑移系（slip system）**。

在小应变框架下，我们可以精确地建立宏观塑性应变与微观滑移之间的联系。一个滑移系 $\alpha$ 可以由位于[滑移面](@entry_id:158709)内的单位滑移方向矢量 $s^\alpha$ 和垂直于滑移面的单位法向矢量 $n^\alpha$ 来定义，两者相互正交，即 $s^\alpha \cdot n^\alpha = 0$。当该[滑移系](@entry_id:136401)上发生剪切率为 $\dot{\gamma}^\alpha$ 的滑移时，它对材料点[速度梯度张量](@entry_id:270928) $L$ 的塑性部分 $L^p$ 的贡献为简单剪切的形式：$L^p = \dot{\gamma}^\alpha (s^\alpha \otimes n^\alpha)$。考虑到所有活动滑移系的贡献，总的塑性速度梯度为它们的线性叠加：

$$
L^p = \sum_{\alpha} \dot{\gamma}^\alpha (s^\alpha \otimes n^\alpha)
$$

其中，“$\otimes$” 表示[并矢积](@entry_id:748716)。需要注意的是，$L^p$ 通常是一个非[对称张量](@entry_id:148092)。然而，在连续介质力学中，与应力做[功共轭](@entry_id:194957)的应变率张量必须是对称的。因此，我们将塑性[应变率张量](@entry_id:266108) $\dot{\varepsilon}^p$ 定义为 $L^p$ 的对称部分：

$$
\dot{\varepsilon}^p = \operatorname{sym}(L^p) = \frac{1}{2}(L^p + (L^p)^{\mathsf{T}}) = \sum_{\alpha} \dot{\gamma}^\alpha \frac{1}{2}(s^\alpha \otimes n^\alpha + n^\alpha \otimes s^\alpha)
$$

为了方便，我们定义一个与每个滑移系相关的**对称Schmid张量（symmetric Schmid tensor）** $m^\alpha$：

$$
m^\alpha = \operatorname{sym}(s^\alpha \otimes n^\alpha) = \frac{1}{2}(s^\alpha \otimes n^\alpha + n^\alpha \otimes s^\alpha)
$$

于是，塑性[应变率](@entry_id:154778)可以简洁地写为 $\dot{\varepsilon}^p = \sum_{\alpha} \dot{\gamma}^\alpha m^\alpha$。这个定义是构建[晶体塑性](@entry_id:141273)模型[运动学](@entry_id:173318)描述的核心 [@problem_id:2678637]。

Schmid张量具有一些重要的性质。首先，由于 $s^\alpha$ 和 $n^\alpha$ 正交，它的迹（trace）为零：

$$
\operatorname{tr}(m^\alpha) = \operatorname{tr}\left(\frac{1}{2}(s^\alpha \otimes n^\alpha + n^\alpha \otimes s^\alpha)\right) = \frac{1}{2}(s^\alpha \cdot n^\alpha + n^\alpha \cdot s^\alpha) = s^\alpha \cdot n^\alpha = 0
$$

迹为零的张量称为**[偏张量](@entry_id:185837)（deviatoric tensor）**。这反映了一个重要的物理事实：由[位错滑移](@entry_id:275474)引起的塑性变形在小应变下是保持体积不变的（isochoric），即它只引起形状改变，不引起体积变化。

接下来，我们建立驱动滑移的力与滑移率之间的关系。单位体积的塑性[功率耗散](@entry_id:264815) $P_{diss}$ 可以从两个角度计算：宏观上，它是柯西应力张量 $\sigma$ 与塑性[应变率张量](@entry_id:266108) $\dot{\varepsilon}^p$ 的[双点积](@entry_id:748648)；微观上，它是所有滑移系上分切应力 $\tau^\alpha$ 与相应滑移率 $\dot{\gamma}^\alpha$ 乘[积之和](@entry_id:266697)。基于[功共轭](@entry_id:194957)原理，两者必须相等：

$$
P_{diss} = \sigma : \dot{\varepsilon}^p = \sum_{\alpha} \tau^\alpha \dot{\gamma}^\alpha
$$

将 $\dot{\varepsilon}^p = \sum_{\alpha} \dot{\gamma}^\alpha m^\alpha$ 代入上式，我们得到：

$$
\sigma : \left(\sum_{\alpha} \dot{\gamma}^\alpha m^\alpha\right) = \sum_{\alpha} \dot{\gamma}^\alpha (\sigma : m^\alpha) = \sum_{\alpha} \tau^\alpha \dot{\gamma}^\alpha
$$

通过比较系数，我们可以明确**分[切应力](@entry_id:137139)（resolved shear stress）** $\tau^\alpha$ 的表达式，它是宏观应力 $\sigma$ 在滑移系 $\alpha$ 上的投影：

$$
\tau^\alpha = \sigma : m^\alpha
$$

这个关系是著名的**[Schmid定律](@entry_id:160968)**的核心，它表明，驱动特定[滑移系](@entry_id:136401)上塑性滑移的有效力，是作用在[滑移面](@entry_id:158709)上、沿着滑移方向的剪切应力分量。这个分切应力是连接宏观加载与微观滑移机制的关键物理量 [@problem_id:2678637]。

### 向有限变形的推广

当材料经历大变形时，小应变假设不再成立，旋转和应变之间的耦合变得不可忽略。此时，我们需要一个更为普适的[运动学](@entry_id:173318)框架。由Lee和Kröner等人发展的**变形梯度的[乘法分解](@entry_id:199514)（multiplicative decomposition of the deformation gradient）**为此提供了理论基础。

该理论引入了一个假想的**[中间构型](@entry_id:193000)（intermediate configuration）**。这个构型是通过“卸载”当前构型中的弹性变形（即[晶格](@entry_id:196752)的拉伸和旋转）得到的。在此构型中，[晶格](@entry_id:196752)是完美且无应力的，但由于塑性滑移的非协调性，它通常无法构成一个连续的物体。

总的变形梯度张量 $F$ 描述了从初始参考构型到当前构型的映射。[乘法分解](@entry_id:199514)将其分解为两部分：

$$
F = F^e F^p
$$

这里：
- $F^p$ 代表**塑性变形梯度**，它描述了从参考构型到[中间构型](@entry_id:193000)的映射。它完全由[晶格](@entry_id:196752)上的滑移累积而成，因此是“[晶格](@entry_id:196752)[不变量](@entry_id:148850)”，即[晶格](@entry_id:196752)本身在此过程中不发生畸变。[位错滑移](@entry_id:275474)本质上是保体积的剪切过程，故通常有 $\det(F^p) \approx 1$。由于[位错](@entry_id:157482)在材料中的[分布](@entry_id:182848)不均匀， $F^p$ 通常是一个**不协调（incompatible）**的场，即它不是某个连续位移场的梯度。
- $F^e$ 代表**弹性变形梯度**，它描述了从[中间构型](@entry_id:193000)到当前构型的映射。它包含了[晶格](@entry_id:196752)的弹性拉伸和刚体旋转。正是这部分变形储存了[弹性应变能](@entry_id:202243)，并最终决定了材料中的柯西应力。

这个分解的顺序至关重要：$F = F^e F^p$ 意味着塑性滑移（$F^p$）在逻辑上先发生，然后弹性变形（$F^e$）作用于这个已经发生塑性重排的结构之上 [@problem_id:2678635]。

小应变理论中的应变加法分解 $\varepsilon = \varepsilon^e + \varepsilon^p$ 实际上是[乘法分解](@entry_id:199514)在[位移梯度](@entry_id:165352)极小时的[一阶近似](@entry_id:147559)。当存在有限的[晶格](@entry_id:196752)旋转时，即使[弹性应变](@entry_id:189634)很小，加法分解也会失效，因为它无法正确处理塑性滑移与[晶格](@entry_id:196752)旋转之间的耦合，而这种耦合对于模拟织构演化等现象至关重要。

在有限变形框架下，分[切应力](@entry_id:137139)的定义也需要相应地修正，以保证[热力学一致性](@entry_id:138886)。通常，[亥姆霍兹自由能](@entry_id:136442) $\psi$ 被假设为仅依赖于弹性变形，例如通过弹性[右柯西-格林张量](@entry_id:174156) $C_e = (F^e)^{\mathsf{T}} F^e$ 来描述，即 $\psi = \psi(C_e)$。其共轭的应力度量是在[中间构型](@entry_id:193000)中定义的第二类Piola-Kirchhoff（PK2）应力 $S_e = 2 \partial\psi / \partial C_e$。

通过复杂的塑性[功耗](@entry_id:264815)散推导，可以证明分[切应力](@entry_id:137139) $\tau^\alpha$ 可以通过**[Mandel应力](@entry_id:191786)（Mandel stress）** $M = C_e S_e$ 来计算。[Mandel应力](@entry_id:191786)是一个在[中间构型](@entry_id:193000)中定义的、通常非对称的应力度量。分切应力是[Mandel应力](@entry_id:191786)在[中间构型](@entry_id:193000)中定义的Schmid张量 $G^\alpha = \operatorname{sym}(s_0^\alpha \otimes n_0^\alpha)$ 上的投影 [@problem_id:2678666]：

$$
\tau^\alpha = M : G^\alpha = (C_e S_e) : G^\alpha
$$

其中 $s_0^\alpha$ 和 $n_0^\alpha$ 是在[中间构型](@entry_id:193000)（即无应力[晶格](@entry_id:196752)）中定义的滑移方向和法向矢量。这个表达式是构建[热力学一致的](@entry_id:755906)有限变形[晶体塑性](@entry_id:141273)模型的关键动力学关系。

### 滑移的本构律：率相关性与[硬化](@entry_id:177483)

分[切应力](@entry_id:137139) $\tau^\alpha$ 提供了驱动力，但滑移率 $\dot{\gamma}^\alpha$ 具体如何响应该驱动力，则由材料的[本构关系](@entry_id:186508)（或称**流变律，flow rule**）决定。这正是“率相关”[晶体塑性](@entry_id:141273)的核心。

#### 率相关性的物理基础

在微观尺度上，滑移率 $\dot{\gamma}$ 与可动位错密度 $\rho_m$、柏氏矢量大小 $b$ 以及[位错](@entry_id:157482)的平均运动速度 $v$ 直接相关，这由**Orowan关系**给出：$\dot{\gamma} = \rho_m b v$。[位错](@entry_id:157482)的运动并非一帆风顺，它需要克服[晶格](@entry_id:196752)中的各种障碍，如Peierls-Nabarro势垒、杂质原子、森林[位错](@entry_id:157482)等。

在许多金属中，尤其是在中低温下，[位错](@entry_id:157482)克服这些短程障碍的过程是由**[热激活](@entry_id:201301)（thermal activation）**控制的。根据**过渡态理论（Transition State Theory）**，[位错](@entry_id:157482)成功跨越一个能量为 $\Delta G$ 的势垒的频率 $\nu$ 遵循阿伦尼乌斯（Arrhenius）关系：

$$
\nu = \nu_0 \exp\left(-\frac{\Delta G}{k_B T}\right)
$$

其中 $\nu_0$ 是尝试频率，$k_B$ 是玻尔兹曼常数，$T$ 是[绝对温度](@entry_id:144687)。外加的剪应力 $\tau$ 会帮助[位错](@entry_id:157482)克服势垒，从而降低有效激活能 $\Delta G$。在一个简单的线性（Eyring）模型中，$\Delta G(\tau) = \Delta F_0 - |\tau|V^*$，其中 $\Delta F_0$ 是零应力下的势垒高度，$V^*$ 是**激活体积（activation volume）**。将这些关系与[Orowan方程](@entry_id:272833)结合，可以推导出滑移率的表达式 [@problem_id:2875401]：

$$
\dot{\gamma} = \dot{\gamma}_0 \exp\left(-\frac{\Delta F_0 - |\tau|V^*}{k_B T}\right) \mathrm{sign}(\tau)
$$

其中 $\dot{\gamma}_0$ 是一个包含微观结构参数的参考应变率。这个方程明确地揭示了滑移率对温度 $T$ 和应力 $\tau$ 的指数依赖性，这是率相关行为的物理根源。更复杂的模型可以用更一般的非线性关系 $\Delta G(\tau)$ 来描述势垒的削弱效应。

#### 唯象流变律

尽管可以从物理原理出发，但在实际应用中，更常用的是形式简单且能有效捕捉实验现象的[唯象模型](@entry_id:273816)。其中最著名的是**[幂律](@entry_id:143404)（power-law）**[粘塑性](@entry_id:165397)模型。该模型将滑移率 $\dot{\gamma}^\alpha$ 与有效驱动应力联系起来：

$$
\dot{\gamma}^\alpha = \dot{\gamma}_0 \left| \frac{\tau^\alpha - \chi^\alpha}{g^\alpha} \right|^{1/m} \mathrm{sign}(\tau^\alpha - \chi^\alpha)
$$

这个方程引入了三个关键的材料参数和状态变量 [@problem_id:2678684]：
- $g^\alpha$：**滑移阻力（slip resistance）**或**临界分[切应力](@entry_id:137139)（Critical Resolved Shear Stress, CRSS）**。它代表了滑移系 $\alpha$ 上位错运动的瞬时固有阻力，是**[各向同性硬化](@entry_id:164486)（isotropic hardening）**的量度。
- $\chi^\alpha$：**[背应力](@entry_id:198105)（back stress）**。它代表了由[位错塞积](@entry_id:187511)等结构在材料内部产生的长程[内应力](@entry_id:193721)场，该应[力场](@entry_id:147325)会“抵抗”或“协助”外加应力。[背应力](@entry_id:198105)是**[运动硬化](@entry_id:172077)（kinematic hardening）**的量度，它能解释包申格效应（Bauschinger effect）。
- $m$：**率敏感指数（rate sensitivity exponent）**。它量化了滑移率对应力的敏感程度。$m$ 值越大，材料的率敏感性越低。在极限情况 $m \to 0^+$ 时，该[幂律](@entry_id:143404)关系趋向于一个率无关的阈值响应：只有当[有效应力](@entry_id:198048) $|\tau^\alpha - \chi^\alpha|$ 达到滑移阻力 $g^\alpha$ 时，滑移才会发生。

#### [硬化](@entry_id:177483)演化律

在塑性变形过程中，位错密度增加、[位错](@entry_id:157482)胞形成等[微观结构演化](@entry_id:142782)会导致材料的滑移阻力不断变化，这一现象称为**[硬化](@entry_id:177483)（hardening）**。因此，$g^\alpha$ 和 $\chi^\alpha$ 不是常数，而是随塑性应变累积而演化的内部[状态变量](@entry_id:138790)。描述它们[演化过程](@entry_id:175749)的方程称为**[硬化](@entry_id:177483)律（hardening law）**。

**[各向同性硬化](@entry_id:164486)**描述了屈服面的均匀扩张，即所有方向的滑移阻力都在增加。$g^\alpha$ 的演化不仅取决于本[滑移系](@entry_id:136401) $\alpha$ 上的滑移（**自[硬化](@entry_id:177483)，self-hardening**），还取决于其他滑移系 $\beta$ 上的滑移（**潜硬化，latent hardening**）。这是因为不同滑移系上的[位错](@entry_id:157482)会相互交割、缠结，形成所谓的“森林[位错](@entry_id:157482)”，阻碍彼此的运动。一个常用的[线性硬化模型](@entry_id:180941)为 [@problem_id:2628517]：

$$
\dot{g}^\alpha = \sum_{\beta} h_{\alpha\beta} |\dot{\gamma}^\beta|
$$

其中 $h_{\alpha\beta}$ 是**[硬化](@entry_id:177483)矩阵**。对角项 $h_{\alpha\alpha}$ 描述了自[硬化](@entry_id:177483)强度，而非对角项 $h_{\alpha\beta} (\beta \neq \alpha)$ 描述了由滑移系 $\beta$ 的活动对滑移系 $\alpha$ 造成的潜[硬化](@entry_id:177483)强度。$|\dot{\gamma}^\beta|$ 的[绝对值](@entry_id:147688)表明硬化是不可逆的，与滑移方向无关。

**[运动硬化](@entry_id:172077)**描述了[屈服面](@entry_id:175331)在[应力空间](@entry_id:199156)的平移，这与[背应力](@entry_id:198105) $\chi^\alpha$ 的演化相关。一个经典的[运动硬化](@entry_id:172077)模型是引入了**动态回复（dynamic recovery）**的[Armstrong-Frederick模型](@entry_id:192715) [@problem_id:2678643]：

$$
\dot{\chi}^\alpha = c \dot{\gamma}^\alpha - d |\dot{\gamma}^\alpha| \chi^\alpha
$$

其中 $c$ 和 $d$ 是材料常数。第一项 $c \dot{\gamma}^\alpha$ 是一个线性硬化项，它使背应力随塑性滑移而增长。第二项 $- d |\dot{\gamma}^\alpha| \chi^\alpha$ 是回复项，它使背应力趋向于一个饱和值，模拟了高温或[大应变](@entry_id:751152)下[位错](@entry_id:157482)通过攀移、[交滑移](@entry_id:195437)等机制重排和湮灭，从而使内[应力松弛](@entry_id:159905)的过程。在单向加载下，该模型预测[背应力](@entry_id:198105)将饱和于 $\chi_{sat} = c/d$。在反向加载时，已建立的正向背应力会显著降低反向屈服所需的应力，从而完美地解释了**包申格效应**。

### 率相关与率无关塑性理论的对比

为了更深刻地理解率相关模型的本质，有必要将其与传统的**率无关（rate-independent）**塑性理论进行对比。

率无关理论假设材料的响应不依赖于加载速率。其核心是一个明确的**屈服面（yield surface）**，它在[应力空间](@entry_id:199156)中定义了一个纯弹性区域。对于[晶体塑性](@entry_id:141273)，这通常由一组独立的屈服条件给出 [@problem_id:2628502]：

$$
\phi^\alpha = |\tau^\alpha| - g^\alpha \le 0, \quad \forall \alpha
$$

[塑性流动](@entry_id:201346)只有当应力状态位于屈服面上（即 $\phi^\alpha = 0$）时才可能发生。这由所谓的**Kuhn-Tucker[互补条件](@entry_id:747558)**来描述：存在非负的塑性乘子 $\lambda^\alpha \ge 0$（与滑移率大小相关），满足 $\lambda^\alpha \phi^\alpha = 0$。这意味着，要么 $\phi^\alpha  0$（应力在[屈服面](@entry_id:175331)内）且 $\lambda^\alpha=0$（无[塑性流动](@entry_id:201346)），要么 $\phi^\alpha = 0$（应力在屈服面上）且 $\lambda^\alpha \ge 0$（允许[塑性流动](@entry_id:201346)）。

在**关联塑性（associative plasticity）**中，塑性流动的“方向”垂直于屈服面。这可以更优雅地通过**耗散势（dissipation potential）** $D(\dot{\gamma})$ 来表述。对于上述屈服条件，耗散势为 $D(\dot{\gamma}) = \sum_\alpha g^\alpha |\dot{\gamma}^\alpha|$。真实的应力状态是使[塑性耗散](@entry_id:201273)功率最大化的状态，这等价于 $\tau^\alpha \in \partial_{\dot{\gamma}^\alpha} D$。

两者的核心区别在于：
1.  **屈服概念**：率无关模型有清晰的屈服界限，应力状态不能超越屈服面。率相关模型（如[幂律模型](@entry_id:272028)）没有绝对的[屈服点](@entry_id:188474)，任何非零应力都会导致非零的（尽管可能极小的）塑性滑移率。应力可以“[过冲](@entry_id:147201)”（overstress）到超过静态屈服强度 $g^\alpha$ 的水平，以驱动更高的滑移率。
2.  **时间尺度**：率无关模型的[本构方程](@entry_id:138559)在时间上是零阶齐次的，其响应与加载历史的速率无关。率相关模型的[本构方程](@entry_id:138559)中显式包含时间速率，因此其应力-应变响应依赖于加载快慢。

### 宏观行为与应用推论

将单晶的[本构模型](@entry_id:174726)应用于[多晶材料](@entry_id:158956)，并分析其宏观后果，是[晶体塑性理论](@entry_id:180579)的最终目标之一。

#### 多晶平均化方案

[多晶体](@entry_id:139228)由大量取向各异的晶粒组成。预测其整体力学行为需要采用某种**均匀化（homogenization）**或**平均化（averaging）**方法。两种经典的简化模型提供了行为的上下限估计 [@problem_id:2678649]：

- **Sachs模型**：基于**应力均匀假设**，即认为多晶体中每个晶粒内的应力状态都与宏观外加应力 $\Sigma$ 相同（$\sigma^{(g)} = \Sigma$）。在此假设下，每个晶粒根据自身取向和外加应力独立地发生变形。多晶体的总塑性[应变率](@entry_id:154778)是所有晶粒塑性应变率的体积分数加权平均。这是一个静态相容但[运动学](@entry_id:173318)不相容的模型。
$$
D^p_{agg} = \langle D^{p,(g)} \rangle = \sum_{g} f^{(g)} D^{p,(g)}(\Sigma)
$$

- **[Taylor模型](@entry_id:203285)**：基于**应变均匀假设**，即认为每个晶粒的塑性[应变率](@entry_id:154778)都与宏观塑性应变率 $D^p_{agg}$ 相同（$D^{p,(g)} = D^p_{agg}$）。为了满足这个苛刻的运动学约束，每个晶粒内部必须产生不同的应力状态 $\sigma^{(g)}$。宏观应力是这些晶粒应力的体积分数平均（$\Sigma = \langle \sigma^{(g)} \rangle$）。这是一个[运动学](@entry_id:173318)相容但静态不相容的模型。在[Taylor模型](@entry_id:203285)下，由宏观应力求宏观应变是一个需要求解复杂[非线性方程组](@entry_id:178110)的逆问题。

这些模型虽然简化，但为理解晶体取向（织构）对多晶体力学性能各向异性的影响提供了基础。

#### [应变局部化](@entry_id:176973)与率相关的正则化效应

在材料发生**[应变软化](@entry_id:755491)（strain softening）**（例如，$H  0$）的情况下，变形会倾向于集中在非常窄的区域内，形成**[剪切带](@entry_id:183352)（shear band）**，即**[应变局部化](@entry_id:176973)（strain localization）**。

对于率无关的软化材料，描述该过程的[偏微分方程组](@entry_id:172573)会失去椭圆性，导致数学上的**[不适定性](@entry_id:635673)（ill-posedness）**。这意味着，对于平面波扰动，其增长率会随着[波数](@entry_id:172452)的增大（波长的减小）而无限增大。在[数值模拟](@entry_id:137087)中，这表现为计算结果对网格尺寸的极端病态依赖：网格越细，[剪切带](@entry_id:183352)就越窄，应变峰值就越高，无法得到收敛的解。

而率相关性则为这一难题提供了天然的**正则化（regularization）**机制 [@problem_id:2678655]。在率相关模型中，驱动高应变率需要很高的应力。当变形试图在窄带内快速集中时，率相关性会产生一种类似于粘性的抵抗力，耗散能量并抑制局部化的无限增长。通过[线性稳定性分析](@entry_id:154985)可以证明，对于率相关模型（$m>0$），即使在软化情况下，扰动的增长率在短波极限下也是有界的。这使得初始[边值问题](@entry_id:193901)保持**[适定性](@entry_id:148590)（well-posed）**。因此，率相关性不仅是对材料物理行为的更真实描述，也为模拟[应变局部化](@entry_id:176973)等复杂失效模式提供了稳健的数学和计算框架。