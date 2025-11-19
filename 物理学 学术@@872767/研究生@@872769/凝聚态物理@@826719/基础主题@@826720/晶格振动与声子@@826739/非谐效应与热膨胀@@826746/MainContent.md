## 引言
材料受热时尺寸发生变化，即热膨胀，是自然界中最普遍的物理现象之一。然而，在微观原子尺度上，这种看似简单的行为背后隐藏着深刻的[晶格动力学](@entry_id:145448)原理。理解热膨胀的起源不仅是[固态物理学](@entry_id:142261)的基础课题，对于在极端温度环境下工作的[材料设计](@entry_id:160450)与工程应用也至关重要。

经典的[晶格振动](@entry_id:140970)理论始于谐振近似，该模型虽然成功解释了比热等性质，却在[热膨胀](@entry_id:137427)问题上遇到了根本困难，因为它预测晶体的尺寸不随温度改变。这一矛盾揭示了，要真正理解[热膨胀](@entry_id:137427)，我们必须超越理想化的[谐振子](@entry_id:155622)图像，深入探究原子间相互作用的真实本质——[非谐性](@entry_id:137191)。

本文旨在系统性地解析非谐效应与热膨胀之间的联系。在第一章“原理与机制”中，我们将从谐振近似的局限性出发，阐明[非谐势](@entry_id:141227)能项如何导致热膨胀，并建立以[准谐近似](@entry_id:181809)和[格林艾森参数](@entry_id:143264)为核心的理论框架。第二章“应用与跨学科交叉”将展示这一理论如何应用于解释各向异性膨胀、[负热膨胀](@entry_id:265079)（NTE）等复杂现象，并探讨其与[材料化学](@entry_id:150195)、磁学等领域的交叉。最后，在“动手实践”部分，读者将有机会通过具体的计算问题，将理论知识应用于实践，加深对非谐效应物理内涵的理解。

## 原理与机制

在上一章中，我们介绍了热膨胀现象及其在科学和工程中的重要性。我们认识到，从微观角度理解材料为何会随着温度升高而膨胀，是固态物理学的一个核心问题。本章将深入探讨这一现象背后的基本原理和微观机制。我们将从理想化的谐振近似模型出发，揭示其局限性，然后引入非谐效应，并建立一个能够定量描述热膨胀的理论框架。

### 谐振近似及其局限性

在晶体[动力学理论](@entry_id:136901)中，一个最基本的模型是**谐振近似 (harmonic approximation)**。该模型假设[晶格](@entry_id:196752)中的每个原子都围绕其平衡位置做微小[振动](@entry_id:267781)。在这种情况下，我们可以将晶体的总势能 $U$ 按原子位移 $u$ 进行[泰勒展开](@entry_id:145057)。令 $u_{i\alpha}$ 表示第 $i$ 个原子在 $\alpha$ 方向上偏离其[平衡位置](@entry_id:272392)的位移，势能可以写为：

$U = U_0 + \sum_{i\alpha} \left. \frac{\partial U}{\partial u_{i\alpha}} \right|_0 u_{i\alpha} + \frac{1}{2!} \sum_{i\alpha, j\beta} \left. \frac{\partial^2 U}{\partial u_{i\alpha} \partial u_{j\beta}} \right|_0 u_{i\alpha} u_{j\beta} + \dots$

其中，$U_0$ 是晶体在所有原子都处于平衡位置时的[基态能量](@entry_id:263704)。在平衡状态下，作用在每个原子上的[净力](@entry_id:163825)为零，即 $F_{i\alpha} = - \partial U / \partial u_{i\alpha} = 0$，因此展开式中的线性项为零。谐振近似的核心思想是忽略所有三阶及更高阶的项，只保留到二阶项：

$U_{\text{harm}} = U_0 + \frac{1}{2} \sum_{i\alpha,j\beta} \Phi_{i\alpha,j\beta} u_{i\alpha} u_{j\beta}$

这里的 $\Phi_{i\alpha,j\beta} = \left. \partial^2 U / (\partial u_{i\alpha} \partial u_{j\beta}) \right|_0$ 是**[谐波](@entry_id:181533)力常数张量**。在这个近似下，原子的[运动方程](@entry_id:170720)是线性的，整个[晶格](@entry_id:196752)的复杂[振动](@entry_id:267781)可以被解耦为一系列独立的简正模式，即**[声子](@entry_id:140728) (phonons)**。每个[声子](@entry_id:140728)都像一个独立的[谐振子](@entry_id:155622)，它们之间没有相互作用。

然而，谐振近似有一个根本性的局限：它无法解释[热膨胀](@entry_id:137427)。在[谐波](@entry_id:181533)[势能](@entry_id:748988) $U_{\text{harm}}$ 中，[势阱](@entry_id:151413)是完全对称的抛物线形。无论振动能量（即温度）多高，原子在其[振动](@entry_id:267781)周期内向外偏离和向内偏离的概率是完全相同的。因此，其平均位移始终为零，$\langle u_{i\alpha} \rangle_T = 0$。这意味着晶体的平均尺寸不随温度变化。因此，要解释[热膨胀](@entry_id:137427)，我们必须超越谐振近似，考虑[势能](@entry_id:748988)中的**非谐效应 (anharmonicity)**。

### 非谐效应的起源：高阶势能项

非谐效应来源于原子间相互作用势的真实形态，它并非完美的抛物线。为了描述这种效应，我们需要在[势能展开](@entry_id:274986)式中包含更高阶的项 [@problem_id:2969969]。

$U \approx U_0 + \frac{1}{2!}\sum_{ij\alpha\beta}\Phi_{ij}^{\alpha\beta}u_{i\alpha} u_{j\beta}+\frac{1}{3!}\sum_{ijk\alpha\beta\gamma}\Psi_{ijk}^{\alpha\beta\gamma}u_{i\alpha} u_{j\beta} u_{k\gamma}+\frac{1}{4!}\sum_{ijkl\alpha\beta\gamma\delta}\Xi_{ijkl}^{\alpha\beta\gamma\delta}u_{i\alpha} u_{j\beta} u_{k\gamma} u_{l\delta}$

其中，$\Psi$ 和 $\Xi$ 分别是三阶（立方）和四阶（四次）非谐[力常数](@entry_id:156420)张量。这些高阶项破坏了[势阱](@entry_id:151413)的完美对称性，并引入了[声子](@entry_id:140728)之间的相互作用。

#### 立方非谐项与热膨胀

**立方项** $\Psi$ 是导致[热膨胀](@entry_id:137427)的最主要原因。该项对位移 $u$ 是奇次幂，使得势能井相对于平衡位置不对称。通常情况下，对于原子间距增大（膨胀）的方向，势能曲线比原子间距减小（压缩）的方向更为平缓。当原子因热能而[振动](@entry_id:267781)时，它会更容易向势能更平缓的一侧运动，导致其时间平均位置偏离原来的[平衡点](@entry_id:272705)，产生一个净的位移。宏观上，这表现为[晶格](@entry_id:196752)的膨胀。因此，从微扰论的角度看，正是立方非谐项 $\Psi$ 在最低阶上导致了非零的平均位移 $\langle u \rangle_T$，从而产生了热膨胀 [@problem_id:2969969]。

此外，立方项还描述了**三[声子](@entry_id:140728)相互作用**过程。在[二次量子化](@entry_id:137766)表述中，位移算符 $\hat{u}$ 是[声子](@entry_id:140728)产生和湮灭算符的线性组合。因此，包含 $\hat{u}^3$ 的[哈密顿量](@entry_id:172864) $\hat{H}^{(3)}$ 会包含诸如 $\hat{a}^\dagger \hat{a} \hat{a}$（一个[声子](@entry_id:140728)衰变为两个）和 $\hat{a}^\dagger \hat{a}^\dagger \hat{a}$（两个[声子](@entry_id:140728)合并为一个）等项。这些过程导致[声子](@entry_id:140728)数不守恒，并赋予[声子](@entry_id:140728)有限的寿命。

[晶格](@entry_id:196752)的周期性对这些相互作用施加了严格的[动量守恒](@entry_id:149964)选择定则。一个涉及三个[声子](@entry_id:140728)（波矢为 $\mathbf{q}_1, \mathbf{q}_2, \mathbf{q}_3$）的相互作用，其总[晶体动量](@entry_id:136369)必须守恒，或相差一个倒易点阵矢量 $\mathbf{G}$：

$\mathbf{q}_1 + \mathbf{q}_2 + \mathbf{q}_3 = \mathbf{G}$

当 $\mathbf{G} = \mathbf{0}$ 时，该过程称为**正常过程 (Normal process)**，它保持了[声子气](@entry_id:147597)体的[总动量](@entry_id:173071)。当 $\mathbf{G} \neq \mathbf{0}$ 时，该过程称为**[乌姆克拉普过程](@entry_id:145784) (Umklapp process)**，[声子气](@entry_id:147597)体的部分动量会转移给整个[晶格](@entry_id:196752)。虽然[乌姆克拉普过程](@entry_id:145784)对于产生热阻至关重要，但正常过程和[乌姆克拉普过程](@entry_id:145784)都源于同一个三阶非谐项，因此它们都对[声子频率](@entry_id:753407)的[温度依赖性](@entry_id:147684)以及热膨胀有贡献 [@problem_id:2969977]。

#### 四次非谐项的作用

**四次项** $\Xi$ 对位移 $u$ 是偶次幂，因此它本身不会破坏[势阱](@entry_id:151413)的对称性，也不会在最低阶上引起[热膨胀](@entry_id:137427)。它的主要作用是使[势阱](@entry_id:151413)的“硬度”或曲率随[振动](@entry_id:267781)振幅而变化。这导致了[声子频率](@entry_id:753407)的温度依赖性（频率重整化）和**四[声子](@entry_id:140728)相互作用**过程。在[一阶微扰理论](@entry_id:153242)中，[声子](@entry_id:140728)能量的移动由 $\langle n | \hat{H}_{\text{anharm}} | n \rangle$ 给出。由于立方项是[奇函数](@entry_id:173259)，其对角元为零，因此它只在二阶微扰中对频率产生影响。而四次项的对角元不为零，因此它是在一阶微扰中导致[声子频率](@entry_id:753407)随温度变化的主要原因 [@problem_id:2969969]。

### [准谐近似](@entry_id:181809)：一种有效的非谐理论

直接处理包含高阶项的[微扰理论](@entry_id:138766)在计算上非常复杂。为了更实用、更直观地处理[热膨胀](@entry_id:137427)问题，物理学家们发展了**[准谐近似](@entry_id:181809) (Quasi-Harmonic Approximation, QHA)**。

QHA的核心思想是，在**任意固定的[晶格](@entry_id:196752)体积 $V$**下，我们仍然认为晶格振动是[谐波](@entry_id:181533)的，即[声子](@entry_id:140728)之间不直接相互作用。但是，我们承认[声子](@entry_id:140728)的频率 $\omega_{\mathbf{q}\nu}$ 本身是体积 $V$ 的函数，即 $\omega_{\mathbf{q}\nu} = \omega_{\mathbf{q}\nu}(V)$ [@problem_id:2969950]。这种体积依赖性有效地将非谐效应纳入了模型。当温度升高，晶体试图膨胀时，体积的变化会引起[声子频率](@entry_id:753407)的变化，进而改变系统的自由能。晶体最终会稳定在使总[自由能最小化](@entry_id:183270)的新体积上。

在这种近似下，晶体的[振动](@entry_id:267781)[亥姆霍兹自由能](@entry_id:136442) $F_{\text{vib}}$ 可以写成所有[声子模式](@entry_id:201212)自由能的总和：

$F_{\text{vib}}(T,V)=\sum_{\mathbf{q}\nu}\left(\frac{\hbar\omega_{\mathbf{q}\nu}(V)}{2}+k_B T \ln\left[1-e^{-\hbar\omega_{\mathbf{q}\nu}(V)/k_B T}\right]\right)$

第一项是零点能，第二项是[热激发](@entry_id:275697)贡献的能量。正是由于 $\omega_{\mathbf{q}\nu}(V)$ 对体积的依赖性，才使得 $F_{\text{vib}}$ 对体积的导数不为零，从而产生了一个依赖于温度的**[振动](@entry_id:267781)热压力 (vibrational thermal pressure)** $p_{\text{vib}} = -(\partial F_{\text{vib}} / \partial V)_T$，这个压力驱动着晶体的[热膨胀](@entry_id:137427) [@problem_id:2969950]。

### [格林艾森参数](@entry_id:143264)：连接微观与宏观的桥梁

在[准谐近似](@entry_id:181809)框架中，描述[声子频率](@entry_id:753407)对体积变化的敏感度的关键物理量是无量纲的**模式[格林艾森参数](@entry_id:143264) (mode Grüneisen parameter)** $\gamma_{\mathbf{q}\nu}$：

$\gamma_{\mathbf{q}\nu} \equiv -\frac{\partial \ln \omega_{\mathbf{q}\nu}}{\partial \ln V} = -\frac{V}{\omega_{\mathbf{q}\nu}}\frac{\partial \omega_{\mathbf{q}\nu}}{\partial V}$

这个参数是连接微观[声子](@entry_id:140728)行为和宏观热力学性质的桥梁。一个正的 $\gamma_{\mathbf{q}\nu}$ 意味着当晶体[体积膨胀](@entry_id:144241)时，该模式的频率会降低（[声子](@entry_id:140728)软化）；反之，一个负的 $\gamma_{\mathbf{q}\nu}$ 意味着频率会升高（[声子](@entry_id:140728)[硬化](@entry_id:177483)）。

利用[格林艾森参数](@entry_id:143264)的定义，我们可以推导出[振动](@entry_id:267781)[热压力](@entry_id:202761) $p_{\text{vib}}$ 的一个重要表达式。通过对自由能求导，可以证明 [@problem_id:2969999]：

$p_{\text{vib}}(T,V) = \frac{1}{V}\sum_{\mathbf{q}\nu} \gamma_{\mathbf{q}\nu} U_{\mathbf{q}\nu}(T,V)$

其中 $U_{\mathbf{q}\nu}(T,V)$ 是模式 $(\mathbf{q},\nu)$ 的平均热振动能量。这个关系清晰地表明，每个[声子模式](@entry_id:201212)对[热压力](@entry_id:202761)的贡献，正比于其自身的能量和它的[格林艾森参数](@entry_id:143264)。

为了获得一个宏观的[热力学](@entry_id:141121)关系，我们定义一个**[热力学](@entry_id:141121)[格林艾森参数](@entry_id:143264)** $\gamma(T)$，它是所有模式[格林艾森参数](@entry_id:143264)以各自对热容的贡献 $C_{V,\mathbf{q}\nu}$ 为权重的加权平均：

$\gamma(T) = \frac{\sum_{\mathbf{q}\nu} \gamma_{\mathbf{q}\nu} C_{V,\mathbf{q}\nu}(T)}{\sum_{\mathbf{q}\nu} C_{V,\mathbf{q}\nu}(T)} = \frac{\sum_{\mathbf{q}\nu} \gamma_{\mathbf{q}\nu} C_{V,\mathbf{q}\nu}(T)}{C_V(T)}$

从[热力学](@entry_id:141121)基本定义出发，可以严格推导出体热膨胀系数 $\alpha_V \equiv \frac{1}{V}(\frac{\partial V}{\partial T})_p$、[定容热容](@entry_id:147536) $C_V$、等温体弹模量 $B \equiv -V(\frac{\partial p}{\partial V})_T$ 和[热力学](@entry_id:141121)[格林艾森参数](@entry_id:143264) $\gamma$ 之间的关系，这被称为**[格林艾森关系](@entry_id:261138)式** [@problem_id:2969996] [@problem_id:2969999]：

$\alpha_V = \frac{\gamma C_V}{B V}$

这个公式是理解热膨胀现象的核心。它告诉我们，一个材料的[热膨胀系数](@entry_id:150685)正比于它的[热容](@entry_id:137594)和[格林艾森参数](@entry_id:143264)，反比于它的体弹模量。也就是说，一个更容易储存热量（$C_V$ 大）、[声子频率](@entry_id:753407)对体积更敏感（$\gamma$ 大）、并且更容易被压缩（$B$ 小）的材料，其[热膨胀系数](@entry_id:150685)会更大。

### [热膨胀](@entry_id:137427)的温度依赖性

[格林艾森关系](@entry_id:261138)式 $\alpha_V = \gamma C_V / (B V)$ 使得我们可以通过分析热容 $C_V(T)$ 的行为来预测[热膨胀系数](@entry_id:150685) $\alpha_V(T)$ 的温度依赖性，因为在许多材料中，$\gamma$ 和 $B$ 对温度的依赖性相对较弱。

#### 高温和低温极限

在**高温极限**下 ($T \gg \Theta_D$，其中 $\Theta_D$ 是[德拜温度](@entry_id:140328)），根据[杜隆-珀蒂定律](@entry_id:191078)，[晶格热容](@entry_id:141837)趋于一个常数 $C_V \rightarrow 3Nk_B$，其中 $N$ 是原胞数目。因此，热膨胀系数也趋于一个饱和值 [@problem_id:2969986]：

$\alpha_{\infty} = \lim_{T \to \infty} \alpha_V(T) = \frac{3N\gamma k_B}{BV}$

在**低温极限**下 ($T \ll \Theta_D$)，根据[德拜模型](@entry_id:141712)，[晶格热容](@entry_id:141837)遵循著名的 $T^3$ 定律，即 $C_V \propto T^3$。相应地，[热膨胀系数](@entry_id:150685)也表现出相同的[温度依赖性](@entry_id:147684) [@problem_id:2969988]：

$\alpha_V(T) \propto T^3$

将[德拜模型](@entry_id:141712)的 $C_V$ 表达式代入，可以得到低温下 $\alpha_V(T)$ 的完整表达式。例如，对于各向同性固体，其[线膨胀](@entry_id:143725)系数 $\alpha_L = \alpha_V/3$ 在低温下为 $\alpha_L(T) = \frac{2\pi^2 k_B^4}{15 \hbar^3 v_s^3} \frac{\gamma}{B} T^3$ 的形式（此处 $v_s$ 为平均声速）[@problem_id:2969988]。

#### [声子频率](@entry_id:753407)的温度漂移

[准谐近似](@entry_id:181809)还预言了一个重要的可观测效应：在恒定压力下，[声子频率](@entry_id:753407)会随温度而改变。这种改变是[晶格](@entry_id:196752)体积热膨胀或收缩的直接结果。利用[链式法则](@entry_id:190743)，我们可以推导出在恒压下频率随温度的变化率 [@problem_id:2969976]：

$(\frac{\partial \omega_{\mathbf{q}\nu}}{\partial T})_{p} = (\frac{\partial \omega_{\mathbf{q}\nu}}{\partial V})_{T} (\frac{\partial V}{\partial T})_{p}$

利用 $\gamma_{\mathbf{q}\nu}$ 和 $\alpha_V$ 的定义，上式可以写为：

$(\frac{\partial \omega_{\mathbf{q}\nu}}{\partial T})_{p} = -\omega_{\mathbf{q}\nu} \gamma_{\mathbf{q}\nu} \alpha_V$

对于大多数材料，$\alpha_V > 0$ 且 $\gamma_{\mathbf{q}\nu} > 0$，这意味着 $(\partial \omega / \partial T)_p  0$，即[声子频率](@entry_id:753407)会随着温度升高而降低，这种现象称为**[声子](@entry_id:140728)软化 (phonon softening)**。例如，在一个典型的[立方晶体](@entry_id:198932)中，如果一个[光学声子](@entry_id:136993)模式在 $300\,\mathrm{K}$ 时的频率为 $5.2\,\mathrm{THz}$，其模式[格林艾森参数](@entry_id:143264) $\gamma=1.6$，材料的[线膨胀](@entry_id:143725)系数为 $2.1 \times 10^{-5}\,\mathrm{K}^{-1}$（体膨胀系数约为 $6.3 \times 10^{-5}\,\mathrm{K}^{-1}$），那么该[声子频率](@entry_id:753407)随温度的变化率约为 $-1.75 \times 10^{-4}\,\mathrm{THz/K}$，这是一个可以通过拉曼[光谱](@entry_id:185632)或[非弹性中子散射](@entry_id:140691)实验测量的数值 [@problem_id:2969976]。

### 特殊现象与前沿课题

基于上述理论框架，我们现在可以解释一些更为复杂和反常的热膨胀行为。

#### [负热膨胀](@entry_id:265079) (NTE)

虽然大多数材料热胀冷缩，但有些材料在一定温度范围内却表现出**[负热膨胀](@entry_id:265079) (Negative Thermal Expansion, NTE)**，即随着温度升高体积反而收缩 ($\alpha_V  0$)。

[格林艾森关系](@entry_id:261138)式 $\alpha_V = \frac{1}{VB} \sum_{\mathbf{q}\nu} \gamma_{\mathbf{q}\nu} C_{V, \mathbf{q}\nu}(T)$ 为我们提供了理解NTE的钥匙。由于 $V$, $B$ 和 $C_{V, \mathbf{q}\nu}$ 总是正的，NTE现象的发生要求加权平均的[格林艾森参数](@entry_id:143264)为负。这表明，材料中必须存在足够多且对[热容](@entry_id:137594)贡献足够大的、具有**负[格林艾森参数](@entry_id:143264)** ($\gamma_{\mathbf{q}\nu}  0$) 的[声子模式](@entry_id:201212)。

$\gamma_{\mathbf{q}\nu}  0$ 意味着 $\partial\omega_{\mathbf{q}\nu}/\partial V > 0$，即这些模式的频率随体积膨胀而升高。这类模式在一些具有特定结构的材料中很常见，例如由刚性[多面体](@entry_id:637910)（如 $\mathrm{SiO_4}$ 四面体或 $\mathrm{ZrO_6}$ 八面体）通过柔性[化学键](@entry_id:138216)（如角共享的氧原子）连接而成的框架结构材料。在这些材料中，存在低频的横向[振动](@entry_id:267781)模式，被称为**[刚性单元模式](@entry_id:141600) (Rigid Unit Modes, RUMs)**。这些模式对应于刚性[多面体](@entry_id:637910)单元的整体摆动或转动，而化学键的弯曲提供了恢复力。当[晶格](@entry_id:196752)膨胀时，这些柔性连接被拉直，使得抵抗刚性单元摆动的恢复力变大，从而导致这些RUMs的频率升高。

当温度升高时，这些低频的RUMs模式被热激发，它们的负 $\gamma_{\mathbf{q}\nu}$ 产生了负的[热压力](@entry_id:202761)，即一种使[晶格](@entry_id:196752)向内收缩的“拉力”。如果这种收缩效应超过了其他具有正 $\gamma_{\mathbf{q}\nu}$ 的常规伸缩[振动](@entry_id:267781)模式所产生的膨胀效应，材料的净体积就会收缩，从而表现出NTE [@problem_id:2969955]。需要强调的是，NTE是一个源于[量子统计](@entry_id:143815)的效应，只要相关的低频模式被热激发（即其[热容](@entry_id:137594) $C_{V, \mathbf{q}\nu}$ 变得显著），NTE就可以发生，通常在远低于经典极限的低温区即可观测到。同时，材料的力学稳定性（$B>0$）是存在稳定NTE行为的前提，而非阻碍 [@problem_id:2969955]。

#### [热膨胀系数](@entry_id:150685)的变号行为

更有趣的是，某些材料的热膨胀系数 $\alpha(T)$ 会随温度变化而改变符号。这通常发生在材料中同时存在贡献相反的[声子模式](@entry_id:201212)的情况下。

我们可以用一个简单的双爱因斯坦模型来说明这一现象 [@problem_id:2969983]。假设一个晶体的[声子谱](@entry_id:753408)由两类模式构成：
1.  一组低频模式（如 $\hbar\omega_1/k_B = 50\,\mathrm{K}$），它们是NTE的主要来源，具有负的[格林艾森参数](@entry_id:143264)（如 $\gamma_1 = -2.0$）。
2.  一组[高频模式](@entry_id:750297)（如 $\hbar\omega_2/k_B = 200\,\mathrm{K}$），它们是常规的伸缩[振动](@entry_id:267781)，具有正的[格林艾森参数](@entry_id:143264)（如 $\gamma_2 = +1.0$）。

根据 $\alpha_V(T) \propto \sum_i g_i \gamma_i C_{V,i}(T)$（$g_i$ 是模式简并度），$\alpha(T)$ 的符号由两项竞争决定：一项是 $g_1 \gamma_1 C_{V,1}(T)$（负贡献），另一项是 $g_2 \gamma_2 C_{V,2}(T)$（正贡献）。

*   **在极低温度下** ($T \ll 50\,\mathrm{K}$)，只有低频模式 $\omega_1$ 能被有效激发，其[热容](@entry_id:137594) $C_{V,1}(T)$ 远大于[高频模式](@entry_id:750297)的[热容](@entry_id:137594) $C_{V,2}(T)$（后者被指数抑制）。因此，负贡献项占主导，$\alpha(T)$ 为负，材料表现出NTE。
*   **随着温度升高**，[高频模式](@entry_id:750297) $\omega_2$ 开始被激发，其[热容](@entry_id:137594) $C_{V,2}(T)$ 迅速增长。正贡献项 $g_2 \gamma_2 C_{V,2}(T)$ 的权重越来越大。
*   **在某个临界温度 $T_c$**，正负贡献恰好相互抵消，使得 $\alpha(T_c) = 0$。
*   **当温度高于 $T_c$**，正贡献项最终超过负贡献项，$\alpha(T)$ 变为正值，材料转为正常的正[热膨胀](@entry_id:137427)行为。
*   **在高温极限下**，所有模式的热容都趋于经典值 $k_B$，$\alpha(T)$ 的符号由简并度加权的[格林艾森参数](@entry_id:143264)之和 $g_1\gamma_1 + g_2\gamma_2$ 决定。在我们的例子中，如果 $g_1=3, g_2=9$，那么总和为 $3(-2.0) + 9(+1.0) = +3.0$，为正值，与高温下 $\alpha(T)>0$ 的结论一致 [@problem_id:2969983]。

这种由不同[声子模式](@entry_id:201212)之间竞争所导致的复杂热膨胀行为，凸显了[准谐近似](@entry_id:181809)理论在解释和预测材料热物理性质方面的强大能力。