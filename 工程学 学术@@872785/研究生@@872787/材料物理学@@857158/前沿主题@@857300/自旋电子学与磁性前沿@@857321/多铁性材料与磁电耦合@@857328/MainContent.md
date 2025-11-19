## 引言
在凝聚态物理与[材料科学](@entry_id:152226)的前沿，[多铁性](@entry_id:147052)（multiferroics）材料因其在单一相中同时展现出铁电、铁磁（或反铁磁）等多种铁序而备受瞩目。这些材料的核心魅力在于不同序参量之间的耦合，特别是电极化与磁化之间的[磁电耦合](@entry_id:140576)效应。这种耦合效应预示着通过[电场](@entry_id:194326)控制磁性（反之亦然）的可能性，为开发超越传统摩尔定律的下一代低[功耗](@entry_id:264815)、高密度信息存储和逻辑器件开辟了革命性的道路。然而，[铁电性](@entry_id:144234)与磁性在微观层面上的“相互排斥”使得天然的[多铁体](@entry_id:147052)十分稀有，其背后的物理机制也异常复杂，这构成了该领域的核心科学挑战与知识空白。

本文旨在系统性地梳理[多铁性](@entry_id:147052)与[磁电耦合](@entry_id:140576)的核心知识体系。读者将通过本文的学习，建立一个从基本原理到前沿应用的完整认知框架。
*   在**“原理与机制”**一章中，我们将深入探讨[多铁性](@entry_id:147052)存在的对称性先决条件，运用朗道唯象理论描述序参量之间的耦合，并剖析催生不同类型[多铁性](@entry_id:147052)的微观物理起源。
*   随后的**“应用与交叉学科关联”**一章将展示这些基本原理如何转化为实际的技术应用，重点介绍其在自旋电子学、高灵敏传感器以及新奇量子物态探索等交叉学科领域中的巨大潜力。
*   最后，**“动手实践”**部分将提供一系列计算练习，引导读者运用所学理论解决具体问题，加深对[磁电耦合](@entry_id:140576)动力学等核心概念的理解。

## 原理与机制

### 基本定义与对称性原理

[多铁性材料](@entry_id:158643)，根据其定义，是在单一相中同时表现出至少两种主要铁序（ferroic order）的材料，例如铁电性与[磁有序](@entry_id:143206) [@problem_id:2502312]。理解这些现象的原理，必须首先从其[序参量](@entry_id:144819)（order parameter）的对称性入手。

[铁电性](@entry_id:144234)的序参量是自发极化强度 $\mathbf{P}$。作为一个[极性矢量](@entry_id:184542)，$\mathbf{P}$ 在空间反演操作（spatial inversion, $\mathcal{I}$）下反号（$\mathcal{I}(\mathbf{P}) = -\mathbf{P}$），而在时间反演操作（time reversal, $\mathcal{T}$）下不变（$\mathcal{T}(\mathbf{P}) = \mathbf{P}$）。因此，任何材料要实现非零的[自发极化](@entry_id:141025)（$\langle \mathbf{P} \rangle \neq \mathbf{0}$），其[晶体结构](@entry_id:140373)必须破缺空间反演对称性，即结构本身是[非中心对称](@entry_id:157488)的。

[磁有序](@entry_id:143206)的[序参量](@entry_id:144819)则更为多样。对于铁磁体（ferromagnet），序参量是[净磁化强度](@entry_id:752443) $\mathbf{M}$。作为一个[轴矢量](@entry_id:196296)（axial vector），$\mathbf{M}$ 在空间反演下不变（$\mathcal{I}(\mathbf{M}) = \mathbf{M}$），但在时间反演下反号（$\mathcal{T}(\mathbf{M}) = -\mathbf{M}$）。对于更常见的反铁磁体（antiferromagnet），其[净磁化强度](@entry_id:752443) $\langle \mathbf{M} \rangle$ 可能为零。在这种情况下，需要引入[交错磁化](@entry_id:194295)强度 $\mathbf{L}$ 作为序参量。例如，对于一个双子[晶格](@entry_id:196752)反铁磁体，$\mathbf{L}$ 定义为两个子[晶格](@entry_id:196752)磁化强度之差 $\mathbf{L} = \mathbf{M}_{A} - \mathbf{M}_{B}$。与 $\mathbf{M}$ 类似，$\mathbf{L}$ 在时间反演下也反号（$\mathcal{T}(\mathbf{L}) = -\mathbf{L}$），因此非零的 $\langle \mathbf{M} \rangle$ 或 $\langle \mathbf{L} \rangle$ 都标志着时间反演对称性的破缺 [@problem_id:2502312]。

由此可见，[多铁体](@entry_id:147052)若要同时具备铁电性和磁有序，一个根本性的对称性要求是，其有序相必须同时破缺空间[反演对称性](@entry_id:269948)（以允许 $\mathbf{P} \neq \mathbf{0}$）和时间反演对称性（以允许磁有序存在）。此外，一个重要的实际条件是，该材料必须是良好的电绝缘体。在导体中，自由移动的载流子会迅速屏蔽任何内部的静电场，从而中和宏观的[自发极化](@entry_id:141025)，使其无法稳定存在或被测量 [@problem_id:2502312]。

### [磁电效应](@entry_id:137842)：耦合与共存

仅仅在同一材料中观测到铁电性和磁有序的共存，并不足以称其为真正意义上的磁电[多铁体](@entry_id:147052)。关键在于这两种序之间是否存在**耦合**（coupling）。这种耦合的明确标志是，一种序的状态可以通过施加与另一种序共轭的场来调控。

从[热力学](@entry_id:141121)角度看，[磁电耦合](@entry_id:140576)最精确的操作性定义是系统自由能对[电场和磁场](@entry_id:261347)存在非零的混合[二阶偏导数](@entry_id:635213) [@problem_id:2502308]。考虑一个[吉布斯自由能](@entry_id:146774)密度 $G(T, \mathbf{E}, \mathbf{H})$，极化强度 $\mathbf{P}$ 和磁化强度 $\mathbf{M}$ 可由其对共轭场的[偏导数](@entry_id:146280)定义：
$P_{i} \equiv -\left.\frac{\partial G}{\partial E_{i}}\right|_{T,H}$
$M_{i} \equiv -\left.\frac{\partial G}{\partial H_{i}}\right|_{T,E}$

[磁电耦合](@entry_id:140576)的存在意味着[电场](@entry_id:194326)可以诱导磁化，[磁场](@entry_id:153296)可以诱导极化。在[线性响应](@entry_id:146180)范围内，这表现为非零的[交叉](@entry_id:147634)[磁化率](@entry_id:138219)，这些磁化率构成了**线性磁电张量** $\alpha_{ij}$。根据麦克斯韦关系（[混合偏导数](@entry_id:139334)的等价性），我们有：
$\alpha_{ij} \equiv \left.\frac{\partial P_{i}}{\partial H_{j}}\right|_{T,E} = \left.\frac{\partial M_{j}}{\partial E_{i}}\right|_{T,H} = -\left.\frac{\partial^{2}G}{\partial E_{i}\,\partial H_{j}}\right|_{T}$
这种关系被称为互易条件（reciprocity condition）。如果一个材料中所有这些[混合偏导数](@entry_id:139334)都为零，那么即使铁电性与磁性共存，它们也是相互独立的，不存在[磁电效应](@entry_id:137842) [@problem_id:2502308]。

基于此，我们可以写出线性磁[电介质](@entry_id:147163)的[本构关系](@entry_id:186508)。从一个包含交叉项的自由能密度 $\Phi(E_i, H_i) = \Phi_0 - \frac{1}{2}\epsilon_{ij} E_i E_j - \frac{1}{2}\chi_{ij} H_i H_j - \alpha_{ij} E_i H_j$ 出发，通过求导可以得到 [@problem_id:2502343]：
$P_i = \epsilon_{ij} E_j + \alpha_{ij} H_j$
$M_i = \chi_{ij} H_j + \alpha_{ji} E_j$
这里，$\epsilon_{ij}$ 和 $\chi_{ij}$ 分别是电容率和[磁化率张量](@entry_id:751635)。在无耗散的[平衡态](@entry_id:168134)下，[热力学](@entry_id:141121)互易性要求 $\alpha_{ij} = \alpha_{ji}$。

线性磁电张量 $\alpha_{ij}$ 存在的对称性要求极为严格。我们可以通过分析自由能中的交叉耦合项 $F_{ME} = -\alpha_{ij} E_i H_j$ 在对称操作下的变换来理解这一点。
*   在空间反演 $\mathcal{I}$ 下：$E_i \to -E_i$ ([极性矢量](@entry_id:184542))，$H_j \to H_j$ ([轴矢量](@entry_id:196296))。因此，$F_{ME} \to -F_{ME}$。若要 $F_{ME}$ 不变，则必须有 $F_{ME}=0$，即 $\alpha_{ij}=0$。
*   在[时间反演](@entry_id:182076) $\mathcal{T}$ 下：$E_i \to E_i$ (T-偶)，$H_j \to -H_j$ (T-奇)。因此，$F_{ME} \to -F_{ME}$。同样，若要 $F_{ME}$ 不变，则 $\alpha_{ij}=0$。

结论是，[线性磁电效应](@entry_id:204105)只有在材料的磁点群同时破缺空间反演 $\mathcal{I}$ 和时间反演 $\mathcal{T}$ 对称性的情况下才被允许 [@problem_id:2843293] [@problem_id:2502312]。一个有趣且重要的特例是，即使 $\mathcal{I}$ 和 $\mathcal{T}$ 都被单独破缺，它们的乘积 $\mathcal{I}\mathcal{T}$ 仍可能是一个[对称操作](@entry_id:143398)。在这种情况下，[线性磁电效应](@entry_id:204105)仍然是允许的，因为 $F_{ME}$ 在 $\mathcal{I}\mathcal{T}$ 操作下不变（$E_i \to -E_i, H_j \to -H_j$，故 $F_{ME} \to F_{ME}$）。典型的例子是反铁磁体 $\mathrm{Cr}_2\mathrm{O}_3$，它是第一个被实验证实存在[线性磁电效应](@entry_id:204105)的材料 [@problem_id:2843293]。

### 唯象理论：[朗道自由能](@entry_id:146600)模型

[朗道理论](@entry_id:138967)为描述[多铁体](@entry_id:147052)中的[相变](@entry_id:147324)和序参量耦合提供了强大的唯象框架。对于一个单轴[多铁体](@entry_id:147052)，其自由能密度 $F$ 可以展开为极化 $P$ 和磁化 $M$ 的[幂级数](@entry_id:146836) [@problem_id:2843267]：
$$F(P,M)=\frac{a}{2}P^2+\frac{b}{4}P^4+\frac{c}{2}M^2+\frac{d}{4}M^4+\gamma P^2 M^2 - E P - H M$$
其中 $a, b, c, d, \gamma$ 是与材料相关的系数，$E$ 和 $H$ 是外场。

各项系数的存在与否受到对称性的严格约束。在一个具有[中心对称](@entry_id:144242)和时间反演对称性的高温母相中，自由能必须在 $\mathcal{I}$ 和 $\mathcal{T}$ 操作下保持不变。由于 $P$ 在 $\mathcal{I}$ 下是奇的，而 $M$ 在 $\mathcal{T}$ 下是奇的，任何包含奇数次幂 $P$ 或 $M$ 的项（如 $P$, $P^3$, $M$, $M^3$, $PM$ 等）在[零场](@entry_id:199169)下都是被对称性禁止的。例如，[双线性](@entry_id:146819)耦合项 $PM$ 在 $\mathcal{I}$ 和 $\mathcal{T}$ 下都会变号，因此被禁止。然而，双二次耦合项 $\gamma P^2 M^2$ 是允许的，因为它同时是 $\mathcal{I}$-偶和 $\mathcal{T}$-偶的。这个耦合项是描述许多[多铁体](@entry_id:147052)中极化与磁化相互作用的最简单形式 [@problem_id:2843267]。

如果母相本身就是[非中心对称](@entry_id:157488)的（破缺 $\mathcal{I}$），但保持[时间反演对称性](@entry_id:138094)（$\mathcal{T}$ 守恒），那么对 $P$ 的幂次不再有偶数限制。在这种情况下，$PM$ 项仍然因为破坏 $\mathcal{T}$ 对称性而被禁止，但诸如 $PM^2$ 这样的项则成为对称性允许的最低阶[磁电耦合](@entry_id:140576)项 [@problem_id:2843267]。

这个 $\gamma P^2 M^2$ 耦合项带来了重要的物理后果。首先，为了保证系统在大的 $|P|$ 和 $|M|$ 下的热力学稳定性，自由能必须有下界，这要求高次项系数满足 $b>0$, $d>0$ 和 $bd > 4\gamma^2$ [@problem_id:2843267]。其次，它导致了[铁电相变](@entry_id:185454)和[磁相变](@entry_id:139255)的相互影响。例如，在一个[磁有序](@entry_id:143206)相（$M \neq 0$）中，与 $P^2$ 相关的自由能项变为 $(\frac{a}{2} + \gamma M^2)P^2$。这意味着[磁有序](@entry_id:143206)的出现会改变[铁电相变](@entry_id:185454)的有效二次项系数，从而移动[铁电转变](@entry_id:185454)温度 $T_{FE}$。根据 $\gamma$ 的符号，磁有序的出现可以促进（$\gamma  0$）或抑制（$\gamma > 0$）铁电性的形成 [@problem_id:2843267]。

### [多铁体](@entry_id:147052)材料的微观起源与分类

#### 第一类与第二类[多铁体](@entry_id:147052)

根据[铁电性](@entry_id:144234)和磁有序的起源以及它们之间的关系，[多铁体](@entry_id:147052)通常被分为两大类 [@problem_id:2502362]。

**第一类 (Type-I) [多铁体](@entry_id:147052)**：在这类材料中，[铁电性](@entry_id:144234)和磁有序源于不同的物理机制，并且通常在截然不同的温度下出现。铁电性通常源于强大的[结构不稳定性](@entry_id:264972)，例如离子位移，其能量尺度在电子伏特（eV）级别，因此[铁电转变](@entry_id:185454)温度 $T_{FE}$ 非常高（常远高于室温）。而[磁有序](@entry_id:143206)源于较弱的磁交换作用，能量尺度在毫[电子伏特](@entry_id:144194)（meV）级别，因此磁转变温度 $T_N$ 或 $T_C$ 通常远低于 $T_{FE}$。由于铁电性的驱动力与磁性无关，这类材料的自发极化强度 $P$ 通常很大（可达 $1 \sim 100 \, \mu\mathrm{C}/\mathrm{cm}^2$）。这类材料中的[磁电耦合](@entry_id:140576)是一种次级效应，通常较弱。典型的例子是[铁酸铋](@entry_id:160561) $\mathrm{BiFeO}_3$，其 $T_{FE} \approx 1100 \, \mathrm{K}$，$T_N \approx 640 \, \mathrm{K}$，室温下具有高达 $60 \sim 100 \, \mu\mathrm{C}/\mathrm{cm}^2$ 的[极化强度](@entry_id:188176)。

**第二类 (Type-II) [多铁体](@entry_id:147052)**：在这类材料中，[铁电性](@entry_id:144234)本身就是由特定的磁有序所诱导的。换言之，是[磁有序](@entry_id:143206)的形成破坏了空间反演对称性，从而产生了电极化。由于极化源于相对微弱的磁相互作用（如[自旋-轨道耦合](@entry_id:143520)），其大小通常很小（典型值为 $10^{-3} \sim 1 \, \mu\mathrm{C}/\mathrm{cm}^2$）。更重要的是，铁电性完全依附于磁有序，因此[铁电转变](@entry_id:185454)与磁转变发生在同一温度，即 $T_{FE} = T_N$。这些转变温度通常很低（远低于室温）。然而，由于铁电性和磁性源于同一机制，它们之间的[磁电耦合](@entry_id:140576)非常强。典型的例子是锰酸铽 $\mathrm{TbMnO}_3$，在其低于约 $28 \, \mathrm{K}$ 的[摆线](@entry_id:172297)状[磁有序](@entry_id:143206)相中，会诱导出约 $0.1 \, \mu\mathrm{C}/\mathrm{cm}^2$ 的电极化。

#### 第一类[多铁性](@entry_id:147052)的机制：$d^0$ 规则及其规避

传统[铁电体](@entry_id:138549)（如 $\mathrm{BaTiO}_3$）和[磁性材料](@entry_id:137953)的[化学成分](@entry_id:138867)要求似乎是相互排斥的，这解释了为什么[多铁体](@entry_id:147052)如此稀有。在[钙钛矿氧化物](@entry_id:192992) $ABO_3$ 中，铁电性通常由 B 位阳离子的极性偏心位移引起。这种位移的驱动力源于所谓的**二阶[姜-泰勒效应](@entry_id:136867)（Second-Order Jahn-Teller, SOJT）**。它涉及到已占据的氧 $2p$ [轨道](@entry_id:137151)与名义上空的过渡金属 $d$ [轨道](@entry_id:137151)之间的共价杂化。为了使这种杂化有效，B 位阳离子的 $d$ [轨道](@entry_id:137151)必须是空的，即具有 $d^0$ 电子构型（如 $\mathrm{Ti}^{4+}$）。然而，磁性（特别是来源于 B 位阳离子的磁性）恰恰要求 $d$ [轨道](@entry_id:137151)被部分填充以拥有未配对电子。这个矛盾被称为“$d^0$ vs $d^n$”问题，它解释了为什么 B 位驱动的铁电性和磁性在同一材料中难以共存 [@problem_id:2502350]。

实现第一类[多铁体](@entry_id:147052)的一条有效途径是规避这一矛盾，即**将铁电性和[磁性的起源](@entry_id:158161)在[晶格](@entry_id:196752)中进行[解耦](@entry_id:637294)**。一种成功的策略是，让铁电性由 A 位阳离子驱动，而磁性由 B 位阳离子提供。例如，在 $\mathrm{BiFeO}_3$ 中，铁电性主要源于 A 位 $\mathrm{Bi}^{3+}$ 离子的 $6s^2$ 孤对电子的立体化学活性，这种活性导致了强烈的极性畸变。这并不对 B 位离子的电子构型提出 $d^0$ 要求。因此，B 位可以被磁性的 $\mathrm{Fe}^{3+}$（$d^5$ 构型）离子占据，从而实现[铁电性](@entry_id:144234)和磁性的共存 [@problem_id:2502350]。

#### 本征、非本征与杂化[非本征铁电性](@entry_id:143468)

根据极化 $P$ 在[相变](@entry_id:147324)中的角色，铁电性可以被更精细地划分为不同类型，这对于理解[多铁体](@entry_id:147052)的设计至关重要 [@problem_id:2502349]。

*   **本征[铁电性](@entry_id:144234) (Proper ferroelectricity)**：极化 $P$ 本身就是驱动[相变](@entry_id:147324)的主要序参量。这意味着一个极性的晶格振动模式（[软模](@entry_id:143177)）在转变温度 $T_c$ 处失稳并“冻结”在[晶格](@entry_id:196752)中。上面提到的 $d^0$ 偏心机制和孤对电子机制都属于本征[铁电性](@entry_id:144234)，如 $\mathrm{BaTiO_3}$ 和 $\mathrm{BiFeO_3}$ [@problem_id:2502349]。这是第一类[多铁体](@entry_id:147052)中最常见的情形 [@problem_id:2502288]。

*   **[非本征铁电性](@entry_id:143468) (Improper ferroelectricity)**：极化 $P$ 是一个次级序参量，它是由一个非极性的主要[序参量](@entry_id:144819)（如结构畸变或磁有序）通过对称性允许的耦合诱导产生的。
    *   **几何[非本征铁电性](@entry_id:143468)**：一个例子是六方锰矿（如 $\mathrm{YMnO}_3$）。其主要[序参量](@entry_id:144819)是 $\mathrm{MnO}_5$ 双锥层的非极性翘曲和三聚化畸变。这种几何畸变本身破坏了反演对称性，从而诱导了一个次级的电极化 [@problem_id:2502288] [@problem_id:2502349]。
    *   **磁致[非本征铁电性](@entry_id:143468)**：这是第二类[多铁体](@entry_id:147052)的定义。主要序参量是[磁有序](@entry_id:143206)，例如在 $\mathrm{TbMnO}_3$ 中的[摆线](@entry_id:172297)磁序通过逆DM机制诱导出电极化 [@problem_id:2502349]。

*   **杂化[非本征铁电性](@entry_id:143468) (Hybrid improper ferroelectricity)**：这是[非本征铁电性](@entry_id:143468)的一个特殊子类。其中，极化 $P$ 是由两个或多个不同的非极性结构序参量（如八面体旋转模式）的乘积耦合产生的。单独的任何一个模式都不会破坏[反演对称性](@entry_id:269948)，但它们的组合可以。这种机制常见于层状[钙钛矿](@entry_id:186025)中，例如通过两种不同类型的[八面体倾转](@entry_id:161131)模式的组合来诱导铁电性 [@problem_id:2502349]。

#### 第二类[多铁性](@entry_id:147052)的机制：磁致极化

在第二类[多铁体](@entry_id:147052)中，特定的磁结构是打破空间反演对称性并产生电极化的根源。其微观机制主要有两种 [@problem_id:2502355]。

1.  **交换伸缩 (Exchange Striction)**：该机制源于磁交换作用强度 $J_{ij}$ 对原子间距的依赖性，即磁-弹耦合。在某些磁结构中，为了最小化总能量，[晶格](@entry_id:196752)会发生畸变，从而在两个自旋 $\mathbf{S}_i$ 和 $\mathbf{S}_j$ 之间产生一个与自旋[标量积](@entry_id:138996) $\mathbf{S}_i \cdot \mathbf{S}_j$ 相关的局域极性位移。例如，对于一个沿 $\hat{\mathbf{x}}$ 方向的共线 $\uparrow\uparrow\downarrow\downarrow$ 反铁磁序，如果相邻化学键不等价（例如，具有不同的磁弹[耦合系数](@entry_id:273384) $\lambda_A$ 和 $\lambda_B$），那么铁磁键（$\mathbf{S}_i \cdot \mathbf{S}_j > 0$）和反铁磁键（$\mathbf{S}_i \cdot \mathbf{S}_j  0$）上的伸缩效应将无法抵消，从而导致一个沿链方向的净电极化，其大小正比于 $(\lambda_A - \lambda_B)$。

2.  **逆 Dzyaloshinskii-Moriya 相互作用 (Inverse DM) / 自旋流机制**：该机制是[自旋-轨道耦合](@entry_id:143520)在非共线[磁结构](@entry_id:201216)中的体现，由 Katsura, Nagaosa 和 Balatsky (KNB) 提出。它指出，两个非共线自旋 $\mathbf{S}_i$ 和 $\mathbf{S}_j$ 可以通过它们之间的连接矢量 $\mathbf{e}_{ij}$ 产生一个局域[电偶极矩](@entry_id:178520) $\mathbf{p}_{ij}$：
    $$\mathbf{p}_{ij} \propto \mathbf{e}_{ij} \times (\mathbf{S}_i \times \mathbf{S}_j)$$
    [宏观极化](@entry_id:141855) $\mathbf{P}$ 是所有这些局域[电偶极矩](@entry_id:178520)的矢量和。这个表达式的对称性是正确的：$\mathbf{S}_i \times \mathbf{S}_j$ 是一个 T-偶的[轴矢量](@entry_id:196296)，它与[极性矢量](@entry_id:184542) $\mathbf{e}_{ij}$ 的叉乘结果是一个 T-偶的[极性矢量](@entry_id:184542)，与 $\mathbf{P}$ 的对称性一致。
    该机制的关键要求是**非共线自旋**，因为共线自旋的叉乘为零。它能很好地解释螺旋[磁序](@entry_id:161845)中产生的电极化。例如：
    *   对于一个**[摆线](@entry_id:172297) (cycloid)** 螺旋（自旋在包含传播矢量 $\mathbf{k}$ 的平面内旋转），例如 $\mathbf{k} \parallel \hat{\mathbf{x}}$ 且自旋在 $\hat{\mathbf{x}}-\hat{\mathbf{y}}$ 平面内旋转，$\mathbf{S}_i \times \mathbf{S}_j$ 指向 $\hat{\mathbf{z}}$ 方向，因此 $\mathbf{P} \propto \hat{\mathbf{x}} \times \hat{\mathbf{z}} \propto -\hat{\mathbf{y}}$。
    *   对于一个**螺旋 (proper screw/helical)** 螺旋（自旋在垂直于 $\mathbf{k}$ 的平面内旋转），例如 $\mathbf{k} \parallel \hat{\mathbf{x}}$ 且自旋在 $\hat{\mathbf{y}}-\hat{\mathbf{z}}$ 平面内旋转，$\mathbf{S}_i \times \mathbf{S}_j$ 指向 $\hat{\mathbf{x}}$ 方向，因此 $\mathbf{P} \propto \hat{\mathbf{x}} \times \hat{\mathbf{x}} = \mathbf{0}$。
    这表明，只有特定类型的非共线磁序才能通过该机制产生电极化。值得注意的是，无论是交换伸缩还是自旋流机制，都不要求系统具有[净磁化强度](@entry_id:752443)，它们在净磁矩为零的反铁磁体中同样有效 [@problem_id:2502355]。