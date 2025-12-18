## 引言
理解将质子和中子束缚成[原子核](@entry_id:167902)的[核力](@entry_id:143248)，是核物理学的中心任务。尽管传统的唯象[核势](@entry_id:752727)模型在拟合实验数据方面取得了成功，但它们缺乏与底层理论——量子色动力学（QCD）的直接联系，也无法系统性地改进或先验地评估理论不确定性。为了弥补这一鸿沟，手征[有效场论](@entry_id:145328)（Chiral Effective Field Theory, $\chi$EFT）应运而生，它已成为从第一性原理出发理解核相互作用的现代标准理论框架。

本篇文章将系统地介绍手征[有效场论](@entry_id:145328)。在**“原理与机制”**一章中，我们将深入探讨该理论的基石——[有效场论](@entry_id:145328)思想、手征对称性及其破缺，并展示如何依据[幂次计数](@entry_id:158814)规则一步步构建[核力势](@entry_id:752706)。接下来，在**“应用与交叉学科联系”**一章中，我们将展示如何运用手征核力解决从头计算核结构、解释[核物质](@entry_id:158311)饱和之谜以及理解[中子星物态方程](@entry_id:161744)等前沿问题，并揭示其与粒子物理、天体物理等领域的深刻联系。最后，**“动手实践”**部分提供了一系列计算练习，旨在帮助读者将理论知识转化为解决具体物理问题的实践能力。

## 原理与机制

在上一章对[核力](@entry_id:143248)的历史背景和现象学描述进行介绍之后，本章将深入探讨描述核相互作用的现代理论框架——手征有效场论（Chiral Effective Field Theory, $\chi$EFT）。我们将从有效场论的基本原理出发，系统地阐述手征对称性如何支配[核力](@entry_id:143248)的结构，并展示如何一步步构建可系统性改进的[核力](@entry_id:143248)。本章的目标是揭示该理论的内在逻辑和机制，为后续章节中复杂的计算和应用奠定坚实的理论基础。

### [有效场论](@entry_id:145328)的核心原理

[有效场论](@entry_id:145328)（EFT）是一种强大的理论工具，它允许我们在不了解高能（或短程）物理细节的情况下，对低能（或长程）物理现象进行精确和系统的描述。其核心思想在于**标度分离（scale separation）**。

#### 标度分离与[幂次计数](@entry_id:158814)

在核物理中，我们关心的典型能动量标度 $Q$（例如，实验室能量 $E_{\mathrm{lab}} \lesssim 100\,\mathrm{MeV}$ 时的[核子](@entry_id:158389)动量 $Q \sim 200\,\mathrm{MeV}$）远小于一个被称为**破缺标度（breakdown scale）**的高[能标](@entry_id:196201)度 $\Lambda_\chi$。对于[核力](@entry_id:143248)而言，这个破缺标度由[量子色动力学](@entry_id:143869)（QCD）的**手征[对称性破缺](@entry_id:158994)（chiral symmetry breaking）**所决定，其数值约为 $\Lambda_\chi \sim 1\,\mathrm{GeV}$。

既然存在清晰的标度分离 $Q \ll \Lambda_\chi$，我们便可以构建一个只包含低能自由度（在这里是[核子](@entry_id:158389)和π介子）的[有效理论](@entry_id:155490)。所有高能自由度（如 $\rho$ 介子、$\Delta$ 共振或更深层次的夸克和胶子）的效应，都被系统地“积分掉（integrated out）”。这些高能物理的效应并不会完全消失，而是被编码到有效拉格朗日量中一系列局域算符的系数里，这些系数被称为**[低能常数](@entry_id:751501)（Low-Energy Constants, LECs）**。

EFT的系统性体现在其**[幂次计数](@entry_id:158814)（power counting）**规则上。任何一个可观测的物理量 $\mathcal{O}$ 都可以被展开成小参数 $Q/\Lambda_\chi$ 的[幂级数](@entry_id:146836)：
$$
\mathcal{O} = \sum_{\nu=0}^{\infty} c_\nu \left(\frac{Q}{\Lambda_\chi}\right)^\nu
$$
其中系数 $c_\nu$ 由理论的动力学和对称性决定。在实际计算中，我们总是在某个有限的阶 $\nu=N$ 处**截断（truncate）**这个级数。这样做的结果是，计算必然会带有一个**[截断误差](@entry_id:140949)（truncation error）**，这个误差的大小由被忽略的领头项决定，即 $\mathcal{O}((Q/\Lambda_\chi)^{N+1})$。

这一特性赋予了EFT**系统性可改进（systematically improvable）**的能力。如果我们想提高理论预言的精度，只需将计算推进到下一阶即可。同时，它还提供了一种先验地[估计理论](@entry_id:268624)不确定性的方法。这与传统的**唯象[核势](@entry_id:752727)（phenomenological potentials）**（如Argonne V18或CD-Bonn模型）形成了鲜明对比。[唯象模型](@entry_id:273816)虽然能够精确地拟合数据，但其形式主要基于物理直觉和数学便利性，缺乏一个可控的展开参数。因此，它们无法提供先验的误差估计，也没有系统性的阶梯来逐步提升理论的精度和一致性 。

#### 对称性与[重整化](@entry_id:143501)[不变性](@entry_id:140168)

EFT的另一个基石是**对称性（symmetries）**。有效拉格朗日量必须包含所有与基础理论（QCD）的对称性（及其破缺模式）相容的相互作用项。正是对称性极大地限制了拉格朗日量的形式，并为[幂次计数](@entry_id:158814)提供了组织原则。对于[核力](@entry_id:143248)，最重要的对称性就是QCD的（近似的）手征对称性。

在进行具体计算时，尤其是涉及到圈图的计算，我们常常会遇到[紫外发散](@entry_id:183379)。为了处理这些发散，需要引入一个**正则化（regularization）**方案，通常伴随着一个**截断动量（cutoff momentum）** $\Lambda$。这个截断动量是一个人为引入的、没有物理意义的参数，它必须处在低能和高能标度之间，即 $Q \lt \Lambda \lt \Lambda_\chi$。

一个自洽的EFT必须满足**[重整化群](@entry_id:147717)[不变性](@entry_id:140168)（Renormalization Group, RG, invariance）**：在经过正确的重整化之后，物理可观测量对截断动量 $\Lambda$ 的选择应不敏感，其剩余的依赖性必须与[截断误差](@entry_id:140949)同阶，即 $\mathcal{O}((Q/\Lambda_\chi)^{N+1})$。这个特性至关重要，它保证了理论的预言能力。在实践中，通过在某个“合理”窗口内（例如 $\Lambda \in [400, 600]\,\mathrm{MeV}$）改变 $\Lambda$ 的值，我们可以考察理论预言的变化，从而得到对[截断误差](@entry_id:140949)大小的可靠估计。这为量化理论不确定性提供了一条非常有力的途径，而这也是[唯象模型](@entry_id:273816)普遍缺乏的 。

### 手征对称性及其破缺

手征[有效场论](@entry_id:145328)的“手征”二字，源于其构建所依赖的核心对称性——QCD的手征对称性。

#### QCD的手征对称性

考虑只有上（u）和下（d）两种夸克的QCD（即双味夸克QCD）。在夸克质量为零（$m_u = m_d = 0$）的理想极限下，[QCD拉格朗日量](@entry_id:158089)具有一个全局的**手征对称性** $SU(2)_L \times SU(2)_R$。这个对称性源于左手和右手夸克场（$q_L$ 和 $q_R$）可以进行独立的 $SU(2)$ 转动：
$$
q_L \rightarrow U_L q_L, \quad q_R \rightarrow U_R q_R
$$
其中 $U_L \in SU(2)_L$，$U_R \in SU(2)_R$。这个对称性与**同位旋（isospin）**对称性不同。[同位旋对称性](@entry_id:146063)是当 $U_L = U_R = V$ 时的[子群](@entry_id:146164)，它同时、同等地转动左手和右手夸克，因此被称为**矢量（vector）**对称性 $SU(2)_V$。而手征对称性还包含了**轴矢量（axial）**变换，即 $U_L = U_R^\dagger$ 的情况，这种变换不等同地作用于左右手场 。

#### 自发与明显[对称性破缺](@entry_id:158994)

尽管手征对称性是理想[拉格朗日量](@entry_id:174593)的性质，但QCD的真空态却不具备这个对称性。实验和[格点QCD](@entry_id:143754)计算都证实了非零的**[夸克凝聚](@entry_id:148353)（quark condensate）** $\langle \bar{q}q \rangle = \langle \bar{u}u + \bar{d}d \rangle \neq 0$ 的存在。由于 $\bar{q}q = \bar{q}_L q_R + \bar{q}_R q_L$，这个凝聚项连接了左右手部分，因此它在独立的左右手转动下不是不变的。然而，它在矢量变换（$U_L=U_R$）下保持不变。

这种拉格朗日量具有对称性而真空态不具有的现象，被称为**自发对称性破缺（Spontaneous Symmetry Breaking, SSB）**。其破缺模式为：
$$
SU(2)_L \times SU(2)_R \rightarrow SU(2)_V
$$
根据**[戈德斯通定理](@entry_id:142874)（Goldstone's theorem）**，每一个被自发破缺的连续全局对称性生成元，都对应着一个零质量的无自旋粒子，即**戈德斯通玻色子（Goldstone boson）**。$SU(2)_L \times SU(2)_R$ 共有 $3+3=6$ 个生成元，而未破缺的[子群](@entry_id:146164) $SU(2)_V$ 有3个生成元，因此有 $6-3=3$ 个破缺的生成元。这导致了3个无质量的[戈德斯通玻色子](@entry_id:156185)的出现，它们在物理上被识别为三种[π介子](@entry_id:147923)（$\pi^+, \pi^0, \pi^-$），并构成一个同位旋三重态 。

在现实世界中，夸克质量并非严格为零。这个微小但非零的质量项（$\mathcal{L}_{\text{mass}} = -m_u\bar{u}u - m_d\bar{d}d$）在拉格朗日量中**明显地（explicitly）**破坏了手征对称性。结果，[π介子](@entry_id:147923)不再是严格无质量的[戈德斯通玻色子](@entry_id:156185)，而是获得了与其质量相关的微小质量，成为**膺[戈德斯通玻色子](@entry_id:156185)（pseudo-Goldstone bosons）**。π介子的质量平方近似正比于夸克质量之和，$m_\pi^2 \propto (m_u+m_d)$。在$\chi$EFT的[幂次计数](@entry_id:158814)中，[π介子](@entry_id:147923)的质量 $m_\pi$ 与典型的低能动量 $p$ 被视为同一量级，即 $p \sim m_\pi \sim Q$ 。

因此，π介子在$\chi$EFT中扮演着双重角色：它们是理论中明确包含的、最轻的**动力学自由度（dynamical degrees of freedom）**，其交换主导了[核力](@entry_id:143248)的长程部分；同时，它们的质量本身也作为一个小的展开标度，参与到[幂次计数](@entry_id:158814)中。

### 构建手征拉格朗日量

$\chi$EFT的[拉格朗日量](@entry_id:174593)是根据手征对称性及其破缺模式，按照[幂次计数](@entry_id:158814)系统构建的。其自由度是[π介子](@entry_id:147923)和[核子](@entry_id:158389)。

#### 重子手征微扰理论

一个技术上的挑战是如何将质量很大的[核子](@entry_id:158389)（$m_N \approx 940\,\mathrm{MeV}$）纳入一个低能展开中。[核子](@entry_id:158389)质量 $m_N$ 并非一个小量，它甚至接近破缺标度 $\Lambda_\chi$。如果在相对论性的拉格朗日量中直接处理，[核子](@entry_id:158389)[传播子](@entry_id:139558) $i/(\gamma \cdot p - m_N)$ 中的大质量 $m_N$ 会破坏简单的[幂次计数](@entry_id:158814)规则。

为了解决这个问题，**重子手征微扰理论（Heavy-Baryon Chiral Perturbation Theory, HBChPT）**被发展出来。其核心思想是将[核子](@entry_id:158389)的[四动量](@entry_id:264378) $p^\mu$ 分解为一个沿固定类时四速度 $v^\mu$（满足 $v^\mu v_\mu = 1$）的大分量和一个小的剩余动量 $k^\mu$：
$$
p^\mu = m_N v^\mu + k^\mu, \quad k^\mu \sim Q
$$
同时，[核子](@entry_id:158389)场 $\Psi(x)$ 也被分解为一个“轻”的（低频）分量 $N_v(x)$ 和一个“重”的（高频）分量 $H_v(x)$。通过将重的分量 $H_v(x)$ 积分掉，我们得到一个只包含轻分量 $N_v$ 的有效拉格朗日量。在这个形式下，[核子](@entry_id:158389)传播子变为 $i/(v \cdot k)$，它的大小正比于 $1/Q$，从而恢复了系统的[幂次计数](@entry_id:158814)。

这种方法的代价是牺牲了**明显[洛伦兹不变性](@entry_id:155152)（manifest Lorentz invariance）**，因为拉格朗日量中显式地出现了固定的速度矢量 $v^\mu$。尽管如此，最终计算出的物理可观测量仍然是洛伦兹不变的。这个框架在过去几十年中取得了巨大成功。近年来，一些新的**相对论性方案（relativistic formulations）**（如红外正则化等）也被发展出来，它们可以在保持明显[洛伦兹不变性](@entry_id:155152)的同时恢复[幂次计数](@entry_id:158814)。这些不同方案之间的差异主要体现在对 $1/m_N$ 修正项的处理上，在 $m_N \to \infty$ 的[静态极限](@entry_id:262480)下它们给出相同的结果 。

#### 领头阶πN相互作用

在HBChPT框架下，领头阶（Leading Order, LO）的π介子-[核子](@entry_id:158389)（$\pi N$）相互作用[拉格朗日量](@entry_id:174593) $\mathcal{L}_{\pi N}^{(1)}$ 是手征阶 $\mathcal{O}(Q)$ 的，其形式为：
$$
\hat{\mathcal{L}}_{\pi N}^{(1)} = \bar{N}_v (i v \cdot D) N_v + g_A \bar{N}_v S_v^\mu u_\mu N_v
$$
这里，$D_\mu$ 是手征[协变导数](@entry_id:152476)，$u_\mu$ 是由π介子场构建的、在手征变换下[协变](@entry_id:634097)的[轴矢量](@entry_id:196296)流，它包含一个导数，因此算作 $\mathcal{O}(Q)$。$S_v^\mu$ 是[协变](@entry_id:634097)[自旋算符](@entry_id:155419)，在[核子](@entry_id:158389)静止参考系中（$v^\mu=(1, \vec{0})$），它简化为 $(0, \frac{1}{2}\vec{\sigma})$，其中 $\vec{\sigma}$ 是泡利矩阵。

系数 $g_A$ 是**轴矢量[耦合常数](@entry_id:747980)（axial coupling constant）**，它是πN体系的一个关键[低能常数](@entry_id:751501)。它被定义为零动量转移下[核子](@entry_id:158389)轴矢量形状因子 $G_A(q^2)$ 的值，即 $g_A = G_A(0) \approx 1.27$。另一个重要的[低能常数](@entry_id:751501)是**[π介子衰变](@entry_id:149070)常数（pion decay constant）** $F_\pi \approx 92.4\,\mathrm{MeV}$，它出现在 $u_\mu$ 的定义中，并设定了手征[微扰理论](@entry_id:138766)的基本标度  。这个[拉格朗日量](@entry_id:174593)是推导核力的出发点。

### 从拉格朗日量推导[核力](@entry_id:143248)

有了有效的拉格朗日量，我们就可以着手计算[核子](@entry_id:158389)之间的相互作用势。Weinberg提出的方案至今仍是主流方法。

#### Weinberg方案：势与动力学

Weinberg建议将**[核势](@entry_id:752727) $V$** 定义为所有**两[核子](@entry_id:158389)不可约（two-nucleon irreducible）**图的总和。不可约图是指那些在切断任意两条[核子](@entry_id:158389)线后仍然保持连通的[费曼图](@entry_id:144373)。而**两[核子](@entry_id:158389)可约（reducible）**图，例如两个单π交换（One-Pion Exchange, OPE）相继发生的图，则不包含在势 $V$ 的定义中。

这些可约图的贡献是通过求解**Lippmann-Schwinger (LS) 方程**来非微扰地产生的：
$$
T = V + V G_0 T
$$
这里 $T$ 是完整的[散射振幅](@entry_id:155369)，$G_0$ 是自由[核子](@entry_id:158389)的[传播子](@entry_id:139558)。将LS方程展开，$T = V + V G_0 V + V G_0 V G_0 V + \dots$，这个级数自动地[对势](@entry_id:753090) $V$ 进行了无限次迭代，从而包含了所有可约图的贡献。这个方法巧妙地将定义势（一个理论构造）和求解动力学（一个量子力学问题）分离开来 。

#### 领头阶 (LO, $\mathcal{O}(Q^0)$) 核力

在领头阶，[核势](@entry_id:752727) $V_{\text{LO}}$ 由两部分组成：长程的单π[交换势](@entry_id:749153)和短程的[接触相互作用](@entry_id:150822)。

**1. 单π[交换势](@entry_id:749153) (OPE)**

通过计算由 $\mathcal{L}_{\pi N}^{(1)}$ 产生的、交换一个π介子的树级图，我们可以导出OPE势。在动量空间中，其结果为 ：
$$
V_{1\pi}(\boldsymbol{q}) = - \frac{g_A^2}{4F_\pi^2} \frac{(\boldsymbol{\sigma}_1 \cdot \boldsymbol{q}) (\boldsymbol{\sigma}_2 \cdot \boldsymbol{q})}{\boldsymbol{q}^2 + m_\pi^2} (\boldsymbol{\tau}_1 \cdot \boldsymbol{\tau}_2)
$$
其中 $\boldsymbol{q}$ 是动量转移，$\boldsymbol{\sigma}_i$ 和 $\boldsymbol{\tau}_i$ 分别是[核子](@entry_id:158389) $i$ 的自旋和[同位旋](@entry_id:199830)[泡利矩阵](@entry_id:139493)。这个势可以进一步分解为**[中心力](@entry_id:267832)（central force）**和**[张量力](@entry_id:161961)（tensor force）**部分：
$$
V_{1\pi}(\boldsymbol{q}) = (\boldsymbol{\tau}_1 \cdot \boldsymbol{\tau}_2) \left[ V_C(|\boldsymbol{q}|) (\boldsymbol{\sigma}_1 \cdot \boldsymbol{\sigma}_2) + V_T(|\boldsymbol{q}|) S_{12}(\hat{\boldsymbol{q}}) \right]
$$
其中 $S_{12}(\hat{\boldsymbol{q}}) = 3(\boldsymbol{\sigma}_1 \cdot \hat{\boldsymbol{q}})(\boldsymbol{\sigma}_2 \cdot \hat{\boldsymbol{q}}) - \boldsymbol{\sigma}_1 \cdot \boldsymbol{\sigma}_2$ 是[张量算符](@entry_id:203590)。推导表明，在领头阶静态近似下，[中心势](@entry_id:148563)和张量势的动量空间函数形式恰好相关 ：
$$
V_C(|\boldsymbol{q}|) = V_T(|\boldsymbol{q}|) = -\frac{g_A^2}{12 F_\pi^2} \frac{|\boldsymbol{q}|^2}{|\boldsymbol{q}|^2 + m_\pi^2}
$$
OPE势，特别是其[张量力](@entry_id:161961)部分，是[核力](@entry_id:143248)的关键特征，它解释了[氘核](@entry_id:161402)的[电四极矩](@entry_id:157483)等重要现象。

**2. [接触相互作用](@entry_id:150822) (Contact Interactions)**

除了由[π介子交换](@entry_id:162149)产生的长程力，还有源于被积分掉的高能物理的[短程力](@entry_id:142823)。在EFT中，这些力被模型化为**[接触相互作用](@entry_id:150822)**，即只在两个[核子](@entry_id:158389)位置相同时才起作用的零程势。在[动量空间](@entry_id:148936)中，它们表现为动量的多项式。

在领头阶（$\mathcal{O}(Q^0)$），根据所有对称性（宇称、[时间反演](@entry_id:182076)、伽利略[不变性](@entry_id:140168)等）要求，只允许存在两个独立的、与动量无关的接触项：
$$
V_{\text{contact}}^{(0)} = C_S + C_T (\boldsymbol{\sigma}_1 \cdot \boldsymbol{\sigma}_2)
$$
这两个算符足以描述[S波散射](@entry_id:155985)中的物理。它们的系数 $C_S$ 和 $C_T$ 是两个必须通过拟合实验数据（如[散射长度](@entry_id:142881)）来确定的[低能常数](@entry_id:751501) 。

因此，领头阶[核势](@entry_id:752727)为 $V_{\text{LO}} = V_{1\pi} + V_{\text{contact}}^{(0)}$。

#### 高阶修正与核力层级

$\chi$EFT的威力在于它可以系统地包含更高阶的修正。

**次领头阶 (NLO, $\mathcal{O}(Q^2)$)**

在NLO，[核势](@entry_id:752727)会收到两类新的贡献：
- **两π交换 (TPE) 势**: 这些是源于交换两个[π介子](@entry_id:147923)的一[圈图](@entry_id:149287)（如盒子图、交叉盒子图等）。在NLO，这些[圈图](@entry_id:149287)上的所有顶点都来自领头阶的πN[拉格朗日量](@entry_id:174593)。计算这些圈图会得到一些标准的圈函数，如 $L(q)$ 和 $A(q)$ 。
- **高阶接触项**: 在 $\mathcal{O}(Q^2)$ 阶，会出现7个新的、依赖于动量平方的接触算符，包括[中心力](@entry_id:267832)、自旋-自旋力、**自旋-[轨道](@entry_id:137151)（spin-orbit）**力和[张量力](@entry_id:161961)的[新形式](@entry_id:199611)。这些算符的系数是7个新的[低能常数](@entry_id:751501) 。

**次次领头阶 (N2LO, $\mathcal{O}(Q^3)$)**

进入N2LO后，理论变得更加丰富：
- **更复杂的TPE势**: 此时的TPE圈图会包含一个来自次领头阶πN[拉格朗日量](@entry_id:174593) $\mathcal{L}_{\pi N}^{(2)}$ 的顶点。这些顶点的强度由LEC $c_1, c_3, c_4$ 等决定 。
- **[三体力](@entry_id:159489) (3NF)**: 这是$\chi$EFT的一个里程碑式的预言。在N2LO，首次出现了不可约的**[三核子力](@entry_id:755955)（Three-Nucleon Force, 3NF）**。这说明[三体力](@entry_id:159489)并非一个附加的现象，而是与两体力在同一个手征对称性框架下内在一致地、在特定阶次上必然出现的物理效应。省略[三体力](@entry_id:159489)来进行N2LO或更高阶的计算，将破坏理论的系统性和一致性  。

这个从LO到NLO再到N2LO的逐级演进，清晰地展示了$\chi$EFT中的**[核力](@entry_id:143248)层级（hierarchy of nuclear forces）**：在每个阶次，都有特定形式的两[体力](@entry_id:174230)或[多体力](@entry_id:146826)出现，其重要性由[幂次计数](@entry_id:158814)规则先天地决定。

### 实践与前沿课题

将$\chi$EFT应用于实际计算，会涉及一些更深入的技术和概念。

#### [低能常数](@entry_id:751501)与自然性

$\chi$EFT的拉格朗日量中包含了大量的[低能常数](@entry_id:751501)（LECs），如πN耦合的 $c_i, \bar{d}_i$ 和NN接触项的 $C, D$ 等。这些常数编码了高能物理的细节，理论本身无法预言它们的值，必须通[过拟合](@entry_id:139093)低能实验数据（如πN[散射相移](@entry_id:138129)、NN[散射相移](@entry_id:138129)等）来确定 。

一个重要的指导原则是**自然性（naturalness）**或**朴素[量纲分析](@entry_id:140259)（Naive Dimensional Analysis, NDA）**。该原则假设，在将LECs写成无量纲形式后，其数值应该为 $\mathcal{O}(1)$。例如，一个[质量量纲](@entry_id:160525)为 $[C]=-k$ 的LEC，其无量纲形式为 $C\Lambda_\chi^k$，我们期望 $|C\Lambda_\chi^k| \sim 1$。这个原则为LECs的大小提供了[先验估计](@entry_id:186098)。

有时，拟合出的LEC会显著大于1，但这并不一定意味着自然性失效。一个典型的例子是LEC $c_3$。当理论中不显式包含 $\Delta(1232)$ 共振态时，它的效应会被吸收到LECs中。由于 $\Delta$ 的[激发能](@entry_id:190368)相对较低，它会对某些LEC（特别是 $c_3, c_4$）产生很大的增强效应，导致 $|c_3|\Lambda_\chi \sim 3-5$。因为这种增强的物理来源是明确的（即所谓的**共振饱和（resonance saturation）**），所以它被认为是与自然性概念相容的 。

#### 重整化、正则化与[幂次计数](@entry_id:158814)方案

如前所述，用LS方程迭代求解[核势](@entry_id:752727)（特别是奇异的[张量力](@entry_id:161961)）会产生发散。因此，必须[对势](@entry_id:753090)进行**正则化**。常用的[正则化方法](@entry_id:150559)有两类：

1.  **非局域[动量空间正则化](@entry_id:752132)**: 对动量空间的势核乘以一个因子，如 $V_\Lambda(\boldsymbol{p}', \boldsymbol{p}) = f_\Lambda(p') V(\boldsymbol{p}', \boldsymbol{p}) f_\Lambda(p)$，其中 $f_\Lambda(p) = \exp[-(p/\Lambda)^{2n}]$ 是一个在 $p > \Lambda$ 时迅速衰减的函数。这种正则化方式保持了伽利略[不变性](@entry_id:140168)，并且不破坏算符基底的Fierz重排[不变性](@entry_id:140168) 。

2.  **局域坐标空间正则化**: 在坐标空间中[对势](@entry_id:753090)乘以一个在 $r \to 0$ 时趋于零的函数，如 $V_{R_0}(\boldsymbol{r}) = f_{R_0}(r)V(\boldsymbol{r})$。这种方法虽然在物理上很直观（在短程抑制相互作用），但在动量空间中对应于一个复杂的卷积运算。这会破坏有限截断下算符基底的Fierz重排[不变性](@entry_id:140168)，引入依赖于[正则化方案](@entry_id:159370)的赝物理效应 。

对势的非微扰处理也引发了关于[幂次计数](@entry_id:158814)的争论。Weinberg计数方案在重整化方面存在问题，这促使了替代方案的发展，如Kaplan, Savage和Wise提出的**KSW方案**。KSW方案对[π介子交换](@entry_id:162149)进行微扰处理，从而在某些[散射道](@entry_id:152994)中实现了更好的重整化性质。然而，该方案在处理奇异[张量力](@entry_id:161961)主导的道中会失效。尽管存在这些理论上的微妙之处，经过修正的Weinberg计数方案仍然是当前核结构和反应计算中最广泛使用的方法 。

#### 不确定性量化

最后，任何基于EFT的预言都必须伴随着可靠的[误差估计](@entry_id:141578)。$\chi$EFT的理论不确定性主要有两个来源：一个是拟合LECs时实验数据带来的**[统计误差](@entry_id:755391)（statistical error）**，另一个是理论本身因有限阶截断而产生的**系统性[截断误差](@entry_id:140949)（systematic truncation error）**。

近年来，**贝叶斯统计（Bayesian statistics）**方法被广泛用于量化[截断误差](@entry_id:140949)。其核心思想是将EFT展开式 $X(Q) = \sum c_n Q^n$ 中所有未知系数 $c_n$ 都视为[随机变量](@entry_id:195330)。基于自然性假设，可以为这些系数设定一个层级先验分布，例如，假定它们独立地来自一个均值为零、[方差](@entry_id:200758)为 $\bar{c}^2$ 的高斯分布，其中超参数 $\bar{c}$ 本身也具有一个先验分布。

在这个框架下，[截断误差](@entry_id:140949) $\Delta_N(Q) = \sum_{n=N+1}^\infty c_n Q^n$ 就成了一个**高斯过程（Gaussian Process）**。这个过程的一个重要特征是，在不同动量点 $Q_i$ 和 $Q_j$ 的截断误差是**相关的（correlated）**，其协[方差](@entry_id:200758)可以从系数的[先验分布](@entry_id:141376)中导出：
$$
\mathrm{Cov}(\Delta_N(Q_i), \Delta_N(Q_j)) = \bar{c}^2 \frac{(Q_i Q_j)^{N+1}}{1 - Q_i Q_j}
$$
最终，一个物理量的总预言不确定性由两部分[协方差矩阵](@entry_id:139155)相加构成：一部分是来自实验测量、通常是对角的统计[误差协[方](@entry_id:194780)差](@entry_id:200758)；另一部分是来自理论截断、通常是非对角和相关的系统[误差协方差](@entry_id:194780)。这种方法清晰地区分了两种误差来源，并为$\chi$EFT的预言提供了严谨和稳健的[置信区间](@entry_id:142297) 。