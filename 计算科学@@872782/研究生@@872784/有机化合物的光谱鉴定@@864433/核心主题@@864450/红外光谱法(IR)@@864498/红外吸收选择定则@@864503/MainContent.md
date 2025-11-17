## 引言
红外(IR)[光谱](@entry_id:185632)是鉴定分子结构和探测化学环境最强大的工具之一。然而，要从一张复杂的谱图中提取有价值的信息，我们不能仅仅满足于经验性的[官能团](@entry_id:139479)频率对应，而必须深入理解其背后的基本物理规律——[红外吸收](@entry_id:188893)选择定则。这些定则决定了在一个分子的众多[振动](@entry_id:267781)模式中，哪些能够吸收红外辐射并产生可观测的谱峰，而哪些则在[光谱](@entry_id:185632)中“沉默”。本文旨在填补从经验观察到深刻物理理解之间的鸿沟，系统性地阐明这些定则的来源、表现形式及其在复杂化学体系中的应用。

通过本文的学习，您将不仅掌握判断一个[振动](@entry_id:267781)模式是否具有[红外活性](@entry_id:267987)的核心判据，还能理解光[谱强度](@entry_id:176230)的来源、[泛音](@entry_id:177516)和合频等“禁戒”跃迁出现的原因，以及对称性是如何支配分子[光谱](@entry_id:185632)的。文章将分为三个章节逐步展开：
*   **原理与机制** 将深入探讨选择定则的量子力学基础，从跃迁偶极矩出发，推导[偶极矩变化](@entry_id:748447)的核心要求，并解释非谐性、对称性以及[振转耦合](@entry_id:163823)如何影响[光谱](@entry_id:185632)。
*   **应用与交叉学科联系** 将展示这些基本原理如何在实际中大放异彩，通过实例说明如何利用选择定则（及其“破缺”）来鉴定[分子对称性](@entry_id:202199)、探测[表面吸附](@entry_id:268937)物种的取向，以及它如何与[材料科学](@entry_id:152226)、生物物理学等领域[交叉](@entry_id:147634)。
*   **动手实践** 将通过一系列计算问题，引导您将理论知识应用于具体情境，从计算双原子分子的[谱线](@entry_id:193408)位置到预测[多原子分子](@entry_id:268323)的[光谱](@entry_id:185632)活性，巩固并深化您的理解。

让我们首先进入第一章，从根本上探索[红外吸收](@entry_id:188893)的物理原理与机制。

## 原理与机制

### 红外[吸收的量子力学](@entry_id:169728)基础

红外[光谱](@entry_id:185632)的核心在于分子与电磁辐射的相互作用。在[电偶极近似](@entry_id:150449)下，这种相互作用由一个微扰[哈密顿算符](@entry_id:144286) $\hat{H}'(t)=-\hat{\boldsymbol{\mu}}\cdot \mathbf{E}(t)$ 描述，其中 $\hat{\boldsymbol{\mu}}$ 是分子的电偶极矩算符，$\mathbf{E}(t)$ 是电磁辐射随时间变化的[电场](@entry_id:194326)。根据[含时微扰理论](@entry_id:141200)，从一个初始振动能态 $\psi_i$ 跃迁到一个末态 $\psi_f$ 的概率正比于**跃迁偶极矩** (transition dipole moment) $\boldsymbol{\mu}_{fi}$ 的模平方，其定义为：

$$
\boldsymbol{\mu}_{fi} = \langle \psi_f | \hat{\boldsymbol{\mu}} | \psi_i \rangle = \int \psi_f^* \hat{\boldsymbol{\mu}} \psi_i d\tau
$$

一个跃迁是否“允许”发生，即其在[光谱](@entry_id:185632)中是否具有可观测的强度，根本上取决于这个积分是否为零。如果 $\boldsymbol{\mu}_{fi} = \mathbf{0}$，则该跃迁是**禁戒**的；反之，如果 $\boldsymbol{\mu}_{fi} \neq \mathbf{0}$，则该跃迁是**允许**的。

在玻恩-奥本海默近似 (Born-Oppenheimer approximation) 下，我们可以将分子的总波[函数近似](@entry_id:141329)地分离为电子[波函数](@entry_id:147440)和核（[振动](@entry_id:267781)与转动）[波函数](@entry_id:147440)的乘积。对于红外[光谱](@entry_id:185632)中研究的纯[振动跃迁](@entry_id:167069)，我们关注的是在同一电[子基](@entry_id:151637)态内，[振动](@entry_id:267781)量子数发生变化的能级跃迁。

### 基本[选择定则](@entry_id:140784)：偶极矩的变化

为了评估跃迁偶极矩，我们需要了解[分子偶极矩](@entry_id:152656) $\boldsymbol{\mu}$ 如何随[原子核](@entry_id:167902)的位移而变化。我们可以将偶极矩 $\boldsymbol{\mu}$ 沿着一个特定的简正[振动](@entry_id:267781)坐标 $Q$（描述一种集体原子运动模式）在[平衡位置](@entry_id:272392) ($Q=0$) 附近进行泰勒级数展开 [@problem_id:3723178]：

$$
\boldsymbol{\mu}(Q) = \boldsymbol{\mu}_0 + \left(\frac{\partial \boldsymbol{\mu}}{\partial Q}\right)_0 Q + \frac{1}{2}\left(\frac{\partial^2 \boldsymbol{\mu}}{\partial Q^2}\right)_0 Q^2 + \cdots
$$

其中，$\boldsymbol{\mu}_0 = \boldsymbol{\mu}(0)$ 是分子在平衡构型下的**[永久偶极矩](@entry_id:163961)** (permanent dipole moment)，而 $(\frac{\partial \boldsymbol{\mu}}{\partial Q})_0$ 是偶极矩随[简正坐标](@entry_id:143194)的[一阶导数](@entry_id:749425)，评估于平衡位置，通常被称为**动态偶极矩** (dynamic dipole moment)。

将此展开式代入跃迁偶极矩的积分表达式中，并考虑一个从初态 $|v_i\rangle$ 到末态 $|v_f\rangle$ 的[振动跃迁](@entry_id:167069)：

$$
\boldsymbol{\mu}_{fi} = \left\langle v_f \left| \boldsymbol{\mu}_0 + \left(\frac{\partial \boldsymbol{\mu}}{\partial Q}\right)_0 Q + \cdots \right| v_i \right\rangle = \boldsymbol{\mu}_0 \langle v_f | v_i \rangle + \left(\frac{\partial \boldsymbol{\mu}}{\partial Q}\right)_0 \langle v_f | Q | v_i \rangle + \cdots
$$

我们逐项分析此表达式：

1.  **永久偶极矩项**：由于[谐振子](@entry_id:155622)[波函数](@entry_id:147440)是正交归一的，即 $\langle v_f | v_i \rangle = \delta_{v_f v_i}$（克罗内克-德尔塔函数），第一项 $\boldsymbol{\mu}_0 \langle v_f | v_i \rangle$ 仅在 $v_f = v_i$ 时非零。这种情况不涉及能级跃迁，因此**[永久偶极矩](@entry_id:163961)的存在本身并不能引起[振动](@entry_id:267781)吸收**。一个分子即便没有永久偶极矩（即 $\boldsymbol{\mu}_0 = \mathbf{0}$），也可能具有[红外活性](@entry_id:267987)。

2.  **[一阶导数](@entry_id:749425)项**：第二项 $(\frac{\partial \boldsymbol{\mu}}{\partial Q})_0 \langle v_f | Q | v_i \rangle$ 是决定[基频](@entry_id:268182)[振动](@entry_id:267781)吸收的关键。要使此项非零，必须同时满足两个条件：
    *   **总体[选择定则](@entry_id:140784) (Gross Selection Rule)**：动态偶极矩必须非零，即 $(\frac{\partial \boldsymbol{\mu}}{\partial Q})_0 \neq \mathbf{0}$。这是[红外吸收](@entry_id:188893)最核心的物理判据：**一个[振动](@entry_id:267781)模式要具有红外活性，该[振动](@entry_id:267781)必须引起分子总偶极矩的净变化**。
    *   **特定选择定则 (Specific Selection Rule)**：积分 $\langle v_f | Q | v_i \rangle$ 必须非零。在[谐振子模型](@entry_id:178080)下，此积分仅在 $v_f = v_i \pm 1$ 时非零。

因此，对于基频跃迁（$v=0 \to v=1$），[红外吸收](@entry_id:188893)的强度 $I$ 正比于跃迁偶极矩的模平方，即：

$$
I \propto |\boldsymbol{\mu}_{fi}|^2 \propto \left| \left(\frac{\partial \boldsymbol{\mu}}{\partial Q}\right)_0 \right|^2 = \sum_{i=x,y,z} \left( \frac{\partial \mu_i}{\partial Q} \right)_0^2
$$

这个关系明确指出，[红外吸收](@entry_id:188893)的强度取决于[振动](@entry_id:267781)过程中[偶极矩变化](@entry_id:748447)的**幅度**，而非分子静态偶极矩的大小 [@problem_id:3723221]。例如，一个分子可能具有较大的永久偶极矩，但某个[振动](@entry_id:267781)模式若几乎不改变偶极矩，其[红外吸收](@entry_id:188893)峰就会很弱。反之，如二氧化碳 ($\text{CO}_2$) 这样没有永久偶极矩的分子，其反对称伸缩[振动](@entry_id:267781)会产生一个[振荡](@entry_id:267781)的偶极矩，因此具有非常强的[红外吸收](@entry_id:188893)。

设想一个分子具有两个[简正模](@entry_id:139640)式 $\alpha$ 和 $\beta$。模式 $\alpha$ 的偶极矩导数分量为 $(\frac{\partial \mu_x}{\partial Q_\alpha})_0 = 0.30$ D，$(\frac{\partial \mu_z}{\partial Q_\alpha})_0 = -0.40$ D；模式 $\beta$ 的偶极矩导数分量为 $(\frac{\partial \mu_x}{\partial Q_\beta})_0 = 0.10$ D，$(\frac{\partial \mu_y}{\partial Q_\beta})_0 = 0.10$ D，$(\frac{\partial \mu_z}{\partial Q_\beta})_0 = 0.10$ D。尽管模式 $\beta$ 在三个方向上都有[偶极矩变化](@entry_id:748447)，但其总强度 $I_\beta \propto (0.1^2 + 0.1^2 + 0.1^2) = 0.03$ D$^2$。而模式 $\alpha$ 的总强度 $I_\alpha \propto (0.3^2 + (-0.4)^2) = 0.09 + 0.16 = 0.25$ D$^2$。因此，模式 $\alpha$ 的[红外吸收](@entry_id:188893)强度预计将远大于模式 $\beta$ [@problem_id:3723221]。

### 超越双谐近似：[非谐性](@entry_id:137191)

在最简单的**双谐近似**（即谐振子势能和线性偶极矩函数）下，唯一允许的红外跃迁是 $\Delta v = \pm 1$。然而，实验[光谱](@entry_id:185632)中经常观测到**[泛音](@entry_id:177516)** (overtones, $\Delta v = \pm 2, \pm 3, \dots$) 和**合频** (combination bands, $\Delta v_i = 1, \Delta v_j = 1$) 等“禁戒”跃迁。这些现象的出现源于**[非谐性](@entry_id:137191)** (anharmonicity)，它分为两种 [@problem_id:3723195] [@problem_id:3723211]。

#### [电非谐性](@entry_id:188082) (Electrical Anharmonicity)

[电非谐性](@entry_id:188082)是指分子的偶极矩函数 $\boldsymbol{\mu}(Q)$ 不是严格线性的，即在泰勒展开式中，二次或更高阶的导数项不可忽略。

$$
\boldsymbol{\mu}(Q) = \boldsymbol{\mu}_0 + \left(\frac{\partial \boldsymbol{\mu}}{\partial Q}\right)_0 Q + \frac{1}{2}\left(\frac{\partial^2 \boldsymbol{\mu}}{\partial Q^2}\right)_0 Q^2 + \frac{1}{3!}\left(\frac{\partial^3 \boldsymbol{\mu}}{\partial Q^3}\right)_0 Q^3 + \cdots
$$

即使在[谐振子势](@entry_id:750179)能模型下（即[振动](@entry_id:267781)[波函数](@entry_id:147440)是标准的[谐振子](@entry_id:155622)函数），这些高阶项也能导致[泛音跃迁](@entry_id:268098)。例如，二次项 $(\frac{\partial^2 \boldsymbol{\mu}}{\partial Q^2})_0 Q^2$ 会使跃迁偶极矩积分 $\langle v_f | Q^2 | v_i \rangle$ 变为非零，而谐振子的 $Q^2$ 算符遵循 $\Delta v = 0, \pm 2$ 的选择定则。因此，[电非谐性](@entry_id:188082)直接为一阶泛音（$\Delta v = \pm 2$）提供了强度。同理，三次项 $Q^3$ 遵循 $\Delta v = \pm 1, \pm 3$ 的选择定则，从而使二阶[泛音](@entry_id:177516)（$\Delta v = \pm 3$）得以出现 [@problem_id:3723195]。

对于[多原子分子](@entry_id:268323)，偶极矩对多个[简正坐标](@entry_id:143194)的依赖性可能包含[交叉](@entry_id:147634)项，例如 $\beta_{ij} Q_i Q_j$。这样的[交叉](@entry_id:147634)项是合频带（例如，从[基态](@entry_id:150928) $|v_i=0, v_j=0\rangle$ 到 $|v_i=1, v_j=1\rangle$）变得允许的原因之一，因为[跃迁积分](@entry_id:147296) $\langle 1,1 | \beta_{ij} Q_i Q_j | 0,0 \rangle = \beta_{ij} \langle 1 | Q_i | 0 \rangle \langle 1 | Q_j | 0 \rangle$ 的两个子积分都非零 [@problem_id:3723195]。

#### 力学[非谐性](@entry_id:137191) (Mechanical Anharmonicity)

力学[非谐性](@entry_id:137191)是指分子的[振动](@entry_id:267781)势能函数 $V(Q)$ 不是一个完美的二次抛物线，而是包含 $Q^3$、$Q^4$ 等高阶项。

$$
V(Q) = \frac{1}{2}k Q^2 + a Q^3 + b Q^4 + \cdots
$$

力学非谐性主要带来两个后果：

1.  **能级不等间距**：[振动能级](@entry_id:193001)不再是等间距的，而是随着量子数 $v$ 的增加，能级间隔通常会变小。这意味着[泛音带](@entry_id:173945)的频率通常会略小于基频带频率的整数倍（例如，$\nu_{0 \to 2}  2\nu_{0 \to 1}$）。因此，观测到的[泛音带](@entry_id:173945)的精确位置主要是力学[非谐性](@entry_id:137191)的体现 [@problem_id:3723195]。

2.  **[波函数](@entry_id:147440)混合**：真实的[振动](@entry_id:267781)[波函数](@entry_id:147440)不再是纯粹的谐振子本征函数，而是谐振子函数的[线性组合](@entry_id:154743)。例如，真实的[基态](@entry_id:150928)[波函数](@entry_id:147440) $\psi'_0$ 可能含有少量 $\psi_1, \psi_2, \dots$ 的成分。这种[波函数](@entry_id:147440)的混合“破坏”了严格的 $\Delta v = \pm 1$ [选择定则](@entry_id:140784)。即使偶极矩函数是严格线性的（$\boldsymbol{\mu}(Q) \propto Q$），由于[波函数](@entry_id:147440)的混合，[跃迁积分](@entry_id:147296) $\langle \psi'_{v+2} | Q | \psi'_v \rangle$ 也可能非零，从而赋予[泛音跃迁](@entry_id:268098)一定的强度 [@problem_id:3723211]。

#### [热谱带](@entry_id:750382) (Hot Bands)

在室温下，如果一个分子的[振动频率](@entry_id:199185)足够低（通常低于约 $600 \text{ cm}^{-1}$），那么根据[玻尔兹曼分布](@entry_id:142765)，有不可忽略比例的分子会处于第一[振动](@entry_id:267781)[激发态](@entry_id:261453) ($v=1$) 或更高能级。从这些已处于[激发态](@entry_id:261453)的分子出发的跃迁被称为**[热谱带](@entry_id:750382)** (hot bands)。

在谐振子和线性偶极矩近似下，[热谱带](@entry_id:750382)同样遵循 $\Delta v = \pm 1$ 的选择定则。因此，一个常见的[热谱带](@entry_id:750382)是 $v=1 \to v=2$ 的跃迁。由于力学[非谐性](@entry_id:137191)的影响，这个跃迁的能量通常略小于基频跃迁（$v=0 \to v=1$），因此[热谱带](@entry_id:750382)通常出现在[基频](@entry_id:268182)峰的低频侧。其强度与初始能级 $v$ 的布居数成正比，该布居数由玻尔兹曼因子 $\exp(-E_v/k_B T)$ 决定，因此其强度随温度升高而显著增加 [@problem_id:3723198]。

### 对称性与[选择定则](@entry_id:140784)

对于[多原子分子](@entry_id:268323)，群论提供了一种无需计算积分就能判断[振动](@entry_id:267781)模式是否具有[红外活性](@entry_id:267987)的强大工具。

#### 对称性判据

一个[振动](@entry_id:267781)模式的[红外活性](@entry_id:267987)与其对称性密切相关。跃迁偶极矩 $\boldsymbol{\mu}_{fi} = \langle \psi_f | \hat{\boldsymbol{\mu}} | \psi_i \rangle$ 是一个积分，只有当被积函数 $\psi_f^* \hat{\boldsymbol{\mu}} \psi_i$ 在分子所属[点群](@entry_id:142456)的所有[对称操作](@entry_id:143398)下保持不变（即属于全对称表示）时，积分才可能非零。

对于基频跃迁，初态 $\psi_i = \psi_0$ 是[振动](@entry_id:267781)[基态](@entry_id:150928)，其[波函数](@entry_id:147440)总是全对称的（例如，在 $D_{2h}$ [点群](@entry_id:142456)中属于 $A_g$ 表示）。末态 $\psi_f = \psi_1$ 的对称性与该[简正模](@entry_id:139640)式 $Q$ 的对称性相同。偶极矩算符 $\hat{\boldsymbol{\mu}}$ 是一个矢量，其分量 $\mu_x, \mu_y, \mu_z$ 的对称性分别与笛卡尔坐标 $x, y, z$ 相同。

因此，[选择定则](@entry_id:140784)简化为：**一个[振动](@entry_id:267781)模式是[红外活性](@entry_id:267987)的，当且仅当其所属的[不可约表示](@entry_id:263310)与笛卡尔坐标 $x$, $y$, 或 $z$ 之一的[不可约表示](@entry_id:263310)相同** [@problem_id:3723204]。

例如，考虑一个属于 $D_{2h}$ 点群的分子。在该[点群](@entry_id:142456)的[特征标表](@entry_id:146676)中，$x, y, z$ 分别属于 $B_{3u}, B_{2u}, B_{1u}$ 表示。如果该分子的一个[振动](@entry_id:267781)模式 $\nu_b$ 的对称性为 $B_{1u}$，则它与 $z$ 坐标具有相同的对称性，因此 $\nu_b$ 是[红外活性](@entry_id:267987)的，其跃迁是 $z$ 偏振的。另一个模式 $\nu_d$ 的对称性为 $B_{3u}$，与 $x$ 坐标相同，因此也是红外活性的（$x$ 偏振）。而对称性为 $A_g$（全对称）或 $B_{2g}$ 的模式则不与任何[笛卡尔坐标](@entry_id:167698)同属一个表示，因此它们是红外非活性的 [@problem_id:3723204]。

#### [互斥](@entry_id:752349)原理 (The Mutual Exclusion Principle)

对于具有**[反演中心](@entry_id:141957)**（即中心对称）的分子（例如[点群](@entry_id:142456)为 $D_{2h}, D_{\infty h}, O_h$ 的分子），[红外活性](@entry_id:267987)和拉曼活性之间存在一个重要的关系，称为**互斥原理** [@problem_id:3723220]。

在中心对称[点群](@entry_id:142456)中，所有[不可约表示](@entry_id:263310)都可以根据其在反演操作 $\hat{i}$ 下的行为分为**偶宇称** (gerade, $g$，对称) 或**奇宇称** (ungerade, $u$，反对称)。
*   电偶极矩算符 $\boldsymbol{\mu}$ 是一个矢量，在反演操作下会改变符号，因此它总是属于 $u$ 对称性。
*   拉曼散射的算符是[极化率张量](@entry_id:191938) $\boldsymbol{\alpha}$，其分量与二次函数 ($x^2, xy$ 等) 具有相同的变换性质，在反演操作下保持不变，因此它总是属于 $g$ 对称性。

根据对称性判据，一个[振动](@entry_id:267781)模式要具有[红外活性](@entry_id:267987)，其对称性必须是 $u$。而一个[振动](@entry_id:267781)模式要具有[拉曼活性](@entry_id:264824)，其对称性必须是 $g$。由于一个模式的对称性不可能同时既是 $g$ 又是 $u$，因此：

**对于[中心对称分子](@entry_id:166437)，一个[振动](@entry_id:267781)模式或者是[红外活性](@entry_id:267987)的，或者是[拉曼活性](@entry_id:264824)的，但绝不能同时是两者。**

这个原理是判断分子是否具有对称中心的有力证据。如果一个分子的[红外光谱和拉曼光谱](@entry_id:261105)中出现了相同频率的谱带，那么该分子几乎可以肯定不具有[反演中心](@entry_id:141957)。需要注意的是，如果分子对称性因[同位素取代](@entry_id:174631)（如 $^{16}$O=C=$^{16}$O 变为 $^{16}$O=C=$^{18}$O）或处于凝聚相环境中而被破坏，[互斥](@entry_id:752349)原理可能不再严格成立 [@problem_id:3723220]。

### 振转[光谱选择定则](@entry_id:139860)

在气相中，分子的[振动](@entry_id:267781)和转动是耦合的，[红外吸收](@entry_id:188893)实际上是[振转跃迁](@entry_id:181881)，导致谱带呈现出由许多分立[谱线](@entry_id:193408)组成的[精细结构](@entry_id:140861)。

#### [线性分子](@entry_id:166760)

对于线性分子（如 HCl, CO, CO$_2$），其振转能级可以近似为[刚性转子](@entry_id:156317)和[简谐振子](@entry_id:145764)的组合。其[选择定则](@entry_id:140784)为 [@problem_id:3723210]：
*   **[振动选择定则](@entry_id:175545)**: $\Delta v = \pm 1$ （对于基频）
*   **[转动选择定则](@entry_id:167711)**:
    *   对于**平行谱带**（跃迁偶极矩平行于分子轴，如 $\Sigma \to \Sigma$ 跃迁），$\Delta J = \pm 1$。
    *   对于**垂直谱带**（跃迁偶极矩垂直于分子轴，如 $\Sigma \to \Pi$ 跃迁），$\Delta J = 0, \pm 1$。

$\Delta J = +1, -1, 0$ 的跃迁分别构成谱图中的 **R 支**、**P 支** 和 **Q 支**。对于[异核双原子分子](@entry_id:145325)或线性分子的伸缩[振动](@entry_id:267781)，跃迁偶极矩通常是平行的。由于对称性限制（宇称必须改变），$\Delta J = 0$ 的跃迁是禁戒的。因此，这类分子的红外[光谱](@entry_id:185632)通常只包含 P 支和 R 支，在谱带中心（[带隙](@entry_id:191975)）没有 Q 支。即使考虑到[非谐性](@entry_id:137191)（允许[泛音带](@entry_id:173945)出现），对于平行谱带，$\Delta J = \pm 1$ 的[转动选择定则](@entry_id:167711)依然成立，Q 支仍然是禁戒的 [@problem_id:3723210]。

#### [对称陀螺分子](@entry_id:189173)

对于[对称陀螺分子](@entry_id:189173)（例如 $CH_3Cl$），其转动状态由两个[量子数](@entry_id:145558) $J$ 和 $K$ 描述。其[选择定则](@entry_id:140784)取决于跃迁偶极矩的方向 [@problem_id:3723199]：
*   **[振动选择定则](@entry_id:175545)**: $\Delta v = \pm 1$
*   **[转动选择定则](@entry_id:167711)**:
    *   **平行谱带**（跃迁偶极矩平行于主[对称轴](@entry_id:177299)）：$\Delta K = 0$, $\Delta J = 0, \pm 1$ (当 $K \neq 0$ 时) 或 $\Delta J = \pm 1$ (当 $K=0$ 时)。这类谱带通常具有明显的 P, Q, R 支结构。
    *   **垂直谱带**（跃迁偶极矩垂直于主对称轴）：$\Delta K = \pm 1$, $\Delta J = 0, \pm 1$。这类谱带的结构更为复杂，通常由一系列以 Q 支为主的子谱带叠加而成。

### 高阶效应：电四极矩跃迁

在标准处理中，我们通常只考虑电[偶极相互作用](@entry_id:193339)。然而，[光与物质的相互作用](@entry_id:268903)[哈密顿量](@entry_id:172864)是一个多极展开，更高阶的项包括[电四极矩](@entry_id:157483)、[磁偶极矩](@entry_id:158175)等。在某些情况下，一个根据电偶极选择定则完全禁戒的跃迁，可能通过这些高阶机制获得微弱的强度。

电四极矩 ($Q_{ij}$) 与[电场](@entry_id:194326)**梯度** ($\nabla \mathbf{E}$) 耦合。其贡献相对于[电偶极跃迁](@entry_id:149662)的强度可以通过量级分析来估计 [@problem_id:3723215]。
*   [电偶极跃迁](@entry_id:149662)振幅 $\propto |\boldsymbol{\mu}| |\mathbf{E}| \sim (ea) |\mathbf{E}|$
*   [电四极矩](@entry_id:157483)跃迁振幅 $\propto |Q| |\nabla \mathbf{E}| \sim (ea^2) |\nabla \mathbf{E}|$
其中 $a$ 是[分子尺寸](@entry_id:752128)，$e$ 是元[电荷](@entry_id:275494)。

在常规的**[远场](@entry_id:269288)**红外[光谱](@entry_id:185632)中，[电场梯度](@entry_id:268185) $|\nabla \mathbf{E}| \sim k |\mathbf{E}| = (2\pi/\lambda)|\mathbf{E}|$, 其中 $\lambda$ 是光的波长。因此，强度比为：

$$
\frac{I_{EQ}}{I_{ED}} \sim \left(\frac{ea^2 \cdot k|\mathbf{E}|}{ea \cdot |\mathbf{E}|}\right)^2 = (ka)^2 = \left(\frac{2\pi a}{\lambda}\right)^2
$$

对于一个中红外波段的典型值，$\lambda = 10 \text{ } \mu\text{m} = 10^{-5} \text{ m}$，分子尺寸 $a = 1 \text{ \AA} = 10^{-10} \text{ m}$，这个比率约为 $(6.28 \times 10^{-5})^2 \approx 4 \times 10^{-9}$。这是一个极小的值，远低于常规[光谱仪](@entry_id:193181)的检测极限，因此在远场[光谱](@entry_id:185632)中，[电四极矩](@entry_id:157483)跃迁通常可以忽略。

然而，在现代**[近场](@entry_id:269780)**[光谱](@entry_id:185632)技术中（如针尖增强红外[光谱](@entry_id:185632)，TEIRA），样品被置于一个[纳米结构](@entry_id:148157)的强局域场中。此时，[电场梯度](@entry_id:268185)不再由波长决定，而是由纳米结构的尺寸 $L$ 决定，即 $|\nabla \mathbf{E}| \sim |\mathbf{E}|/L$。强度比变为：

$$
\frac{I_{EQ}}{I_{ED}} \sim \left(\frac{a}{L}\right)^2
$$

如果使用一个尺寸为 $L=10 \text{ nm}$ 的针尖，这个比率将变为 $(10^{-10}/10^{-8})^2 = 10^{-4}$。这个值远大于之前的远场估计，并且完全可能被现代仪器检测到。因此，近场技术为观测和利用这些原本“禁戒”的高阶跃迁提供了新的途径 [@problem_id:3723215]。