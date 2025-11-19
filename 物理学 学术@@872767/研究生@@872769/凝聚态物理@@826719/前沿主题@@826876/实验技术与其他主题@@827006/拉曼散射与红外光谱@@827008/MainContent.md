## 引言
[拉曼散射](@entry_id:141474)与红外[光谱](@entry_id:185632)是研究物质内部微观动力学的两种最基本、最强大的[光谱学](@entry_id:141940)工具。它们通过探测[分子振动](@entry_id:140827)和[晶格振动](@entry_id:140970)（[声子](@entry_id:140728)），为我们提供了洞悉物质化学结构、[晶体对称性](@entry_id:198772)、电子态以及[多体相互作用](@entry_id:751663)的独特窗口。尽管这些技术在化学、物理和[材料科学](@entry_id:152226)等领域得到了广泛应用，但要从复杂的谱图中准确提取深刻的物理和化学信息，需要对它们背后的核心原理有扎实的理解。本文旨在弥合实验观测与理论基础之间的鸿沟，系统性地阐述这两种[光谱](@entry_id:185632)技术的内在机制及其在前沿研究中的应用。

本文将通过三个章节层层递进，带领读者从基本原理走向前沿应用。在**“原理与机制”**一章中，我们将从光与物质相互作用的[守恒定律](@entry_id:269268)出发，深入探讨[声子](@entry_id:140728)的概念、决定谱学活性的[对称性选择定则](@entry_id:156619)，并介绍共振效应、[电子-声子耦合](@entry_id:139197)等高级多体物理现象。接下来的**“应用与[交叉](@entry_id:147634)学科联系”**一章将展示这些原理如何转化为强大的分析工具，通过一系列实例说明[光谱学](@entry_id:141940)在化学结构分析、材料[相变](@entry_id:147324)研究、[缺陷表征](@entry_id:203907)以及低维体系探索中的关键作用。最后，在**“动手实践”**部分，读者将有机会通过具体的理论计算问题，巩固对[声子](@entry_id:140728)[对称性分析](@entry_id:174795)和偏振选择定则的理解，将理论知识转化为解决实际问题的能力。通过本章的学习，您将能够为后续的[光谱](@entry_id:185632)解析与科学探索奠定坚实的理论基础。

## 原理与机制

本章旨在深入阐述[拉曼散射](@entry_id:141474)与红外[吸收[光谱](@entry_id:164865)学](@entry_id:141940)的核心物理原理与机制。我们将从基本的[守恒定律](@entry_id:269268)和相互作用模型出发，逐步深入到[对称性分析](@entry_id:174795)、[多体效应](@entry_id:173569)以及共振现象等高级主题。这些内容构成了理解和应用这些[光谱](@entry_id:185632)技术来探测[凝聚态物质](@entry_id:747660)中[元激发](@entry_id:140859)（如[声子](@entry_id:140728)）的理论基础。

### 基本过程与[守恒定律](@entry_id:269268)

光与晶体等介质相互作用时，绝大部分[光子](@entry_id:145192)会发生**弹性散射**，即散射[光子](@entry_id:145192)的能量与入射[光子能量](@entry_id:139314)相同。这一过程被称为**瑞利散射（Rayleigh scattering）**。然而，一小部分[光子](@entry_id:145192)会与介质的内部激发（例如[晶格振动](@entry_id:140970)）交换能量，发生**[非弹性散射](@entry_id:138624)**。当散射过程涉及[声子](@entry_id:140728)时，该过程被称为**拉曼散射（Raman scattering）**。

这些散射过程严格遵守能量和[晶体动量守恒](@entry_id:145588)定律。[@problem_id:3013331] 假设一个频率为 $\omega_i$、[波矢](@entry_id:178620)为 $\mathbf{k}_i$ 的入射[光子](@entry_id:145192)与[晶格](@entry_id:196752)相互作用，产生一个频率为 $\omega_s$、[波矢](@entry_id:178620)为 $\mathbf{k}_s$ 的散射[光子](@entry_id:145192)，同时激发或湮灭一个频率为 $\Omega_{\nu}(\mathbf{q})$、晶体动量为 $\mathbf{q}$ 的[声子](@entry_id:140728)（其中 $\nu$ 为[声子支](@entry_id:189965)的索引）。

[能量守恒](@entry_id:140514)要求：
$$ \hbar\omega_s = \hbar\omega_i \pm \hbar\Omega_{\nu}(\mathbf{q}) $$
其中，负号对应于创造一个[声子](@entry_id:140728)的**斯托克斯（Stokes）散射**过程，此时散射光子能量降低；正号对应于湮灭一个已存在[声子](@entry_id:140728)的**反斯托克斯（anti-Stokes）散射**过程，此时散射[光子能量](@entry_id:139314)增加。

[晶体动量守恒](@entry_id:145588)要求：
$$ \mathbf{k}_i = \mathbf{k}_s + \mathbf{q} + \mathbf{G} $$
其中 $\mathbf{G}$ 是一个[倒格矢](@entry_id:263351)。对于[晶格](@entry_id:196752)整体不参与动量交换的正常过程（Normal process），我们取 $\mathbf{G} = \mathbf{0}$，因此[声子](@entry_id:140728)波矢由[光子](@entry_id:145192)[波矢](@entry_id:178620)的改变决定：$\mathbf{q} = \mathbf{k}_i - \mathbf{k}_s$。

这一动量守恒关系带来了一个至关重要的结论：**一阶拉曼[光谱](@entry_id:185632)和[红外吸收](@entry_id:188893)主要探测布里渊区中心的[声子](@entry_id:140728)**。[@problem_id:3013311] 这一结论源于一个简单的尺度比较。可见光或近红外光在介质中的波长 $\lambda$ 通常在数百纳米量级（例如 $500 \, \text{nm}$），对应的[光子](@entry_id:145192)[波矢](@entry_id:178620)大小 $|k| = 2\pi/\lambda$ 约为 $10^7 \, \text{m}^{-1}$。而晶体的晶格常数 $a$ 通常在零点几纳米量级（例如 $0.5 \, \text{nm}$），其[第一布里渊区](@entry_id:269110)的尺度由 $\pi/a$ 决定，约为 $10^{10} \, \text{m}^{-1}$。显然，[光子](@entry_id:145192)[波矢](@entry_id:178620)的量级远小于[布里渊区](@entry_id:142395)的尺寸（$|k| \ll \pi/a$）。由于拉曼过程中交换的动量 $|\mathbf{q}| = |\mathbf{k}_i - \mathbf{k}_s| \le |\mathbf{k}_i| + |\mathbf{k}_s|$，因此被探测的[声子](@entry_id:140728)[波矢](@entry_id:178620) $\mathbf{q}$ 必须非常接近布里渊区的中心，即 $\mathbf{q} \approx \mathbf{0}$。

与拉曼散射（一种双[光子散射](@entry_id:194085)过程）不同，**[红外吸收](@entry_id:188893)（Infrared absorption）**是一种单[光子](@entry_id:145192)吸收过程。在此过程中，一个频率为 $\omega_i$ 的红外[光子](@entry_id:145192)被[晶格](@entry_id:196752)吸收，并创造一个[声子](@entry_id:140728)。[能量和动量守恒](@entry_id:193044)的表达式为 $\hbar\omega_i = \hbar\Omega_{\nu}(\mathbf{q})$ 和 $\mathbf{k}_i = \mathbf{q}$。由于能够激发[声子](@entry_id:140728)的红外[光子](@entry_id:145192)波长更长，其[波矢](@entry_id:178620) $|\mathbf{k}_i|$ 更小，因此[红外吸收](@entry_id:188893)同样只探测 $\mathbf{q} \approx \mathbf{0}$ 的[声子](@entry_id:140728)。

### [晶格振动](@entry_id:140970)：[声子](@entry_id:140728)

晶体中原子的周期性[排列](@entry_id:136432)使得它们的集体[振动](@entry_id:267781)可以被描述为一系列[简正模](@entry_id:139640)式，这些模式的量子化形式即为**[声子](@entry_id:140728)（phonons）**。对于一个含有 $p$ 个原子的原胞的晶体，在每个波矢 $\mathbf{q}$ 处存在 $3p$ 个[声子模式](@entry_id:201212)（支）。这些[声子支](@entry_id:189965)根据其在长波极限（$\mathbf{q} \to \mathbf{0}$）下的行为可分为两类：**[声学声子](@entry_id:141298)（acoustic phonons）**和**[光学声子](@entry_id:136993)（optical phonons）**。[@problem_id:3013346]

**[声学声子](@entry_id:141298)**：任何晶体都存在三支[声学声子](@entry_id:141298)。它们的频率在 $\mathbf{q} \to \mathbf{0}$ 时趋于零，即 $\omega(\mathbf{q}) \to 0$。在 $\mathbf{q}$ 点附近，其色散关系是线性的，$\omega \approx v_s |\mathbf{q}|$，其中 $v_s$ 是声速。这种模式对应于[原胞](@entry_id:159354)内所有原子近乎同相的集体[平移运动](@entry_id:187700)，宏观上表现为晶体中的[弹性波](@entry_id:196203)或声波。

**光学声子**：其余的 $3p-3$ 支[声子](@entry_id:140728)是光学声子。它们存在的条件是[原胞](@entry_id:159354)内[原子数](@entry_id:746561) $p > 1$。与[声学声子](@entry_id:141298)不同，光学声子在 $\mathbf{q} \to \mathbf{0}$ 时的频率趋于一个非零的常数，$\omega(\mathbf{0}) \neq 0$。其[振动](@entry_id:267781)模式对应于[原胞](@entry_id:159354)内原子之间的[相对运动](@entry_id:169798)（反相运动），而[原胞](@entry_id:159354)的质心保持不动。如果这些[相对运动](@entry_id:169798)的原子带有[有效电荷](@entry_id:748807)，[振动](@entry_id:267781)就会产生一个[振荡](@entry_id:267781)的[电偶极矩](@entry_id:178520)，从而能与[电磁场](@entry_id:265881)发生强烈的相互作用。

基于前一节 $\mathbf{q} \approx \mathbf{0}$ 的选择定则，我们可以得出结论：一阶拉曼散射和[红外吸收](@entry_id:188893)[光谱](@entry_id:185632)是研究**布里渊区中心（$\mathbf{q}=\mathbf{0}$）[光学声子](@entry_id:136993)**的有力工具。

### 相互作用机制与选择定则

一种[光学声子](@entry_id:136993)模式是否能被红外或拉曼[光谱](@entry_id:185632)探测到，取决于该[振动](@entry_id:267781)模式能否与光场发生有效的耦合。这两种技术的耦合机制截然不同，从而导致了它们各自独特的**选择定则（selection rules）**。

#### 经典图像：[洛伦兹振子模型](@entry_id:274156)

我们可以将一个光学声子模式经典地看作一个[阻尼谐振子](@entry_id:276848)（[洛伦兹振子模型](@entry_id:274156)）。[@problem_id:3013336] 在此图像下：

- **[红外活性](@entry_id:267987)（IR activity）**：当[声子](@entry_id:140728)[振动能](@entry_id:157909)引起晶体宏观**[电偶极矩](@entry_id:178520) $\boldsymbol{\mu}$** 发生变化时，该模式就是[红外活性](@entry_id:267987)的。光场的[电场](@entry_id:194326)可以直接驱动这个[振荡](@entry_id:267781)的偶极矩，当光频与[声子频率](@entry_id:753407)共振时，发生强烈的能量吸收。这个条件的数学表述是，[声子](@entry_id:140728)[简正坐标](@entry_id:143194) $Q$ 对[电偶极矩](@entry_id:178520)的导数不为零，即 $\frac{d\boldsymbol{\mu}}{dQ} \neq 0$。

- **[拉曼活性](@entry_id:264824)（Raman activity）**：[拉曼活性](@entry_id:264824)源于[声子](@entry_id:140728)[振动](@entry_id:267781)对材料**[电子极化率](@entry_id:144809)张量 $\boldsymbol{\alpha}$** 的调制。入射光的[电场](@entry_id:194326) $\mathbf{E}$ 在材料中感生出一个偶极矩 $\mathbf{p} = \boldsymbol{\alpha} \mathbf{E}$。如果[极化率](@entry_id:143513)本身是[声子](@entry_id:140728)坐标 $Q(t) = Q_0 \cos(\Omega t)$ 的函数，我们可以将其展开：$\boldsymbol{\alpha}(Q) \approx \boldsymbol{\alpha}_0 + \left(\frac{\partial \boldsymbol{\alpha}}{\partial Q}\right) Q(t)$。感生偶极矩将包含一个新项：
$$ \mathbf{p}_{\text{Raman}}(t) = \left(\frac{\partial \boldsymbol{\alpha}}{\partial Q}\right) Q_0 \cos(\Omega t) \mathbf{E}_0 \cos(\omega_i t) = \frac{1}{2} \left(\frac{\partial \boldsymbol{\alpha}}{\partial Q}\right) Q_0 \mathbf{E}_0 [\cos((\omega_i-\Omega)t) + \cos((\omega_i+\Omega)t)] $$
这个[振荡](@entry_id:267781)的偶极矩会辐射出频率为 $\omega_i \pm \Omega$ 的斯托克斯和反斯托克斯光。因此，拉曼活性的条件是极化率对[声子](@entry_id:140728)坐标的导数不为零，即 $\frac{\partial \boldsymbol{\alpha}}{\partial Q} \neq 0$。这个导数张量 $\mathbf{R}_{ij} = \left.\frac{\partial \alpha_{ij}}{\partial Q}\right|_{Q=0}$ 被定义为**拉曼张量（Raman tensor）**，它量化了[声子](@entry_id:140728)对[极化率](@entry_id:143513)的调制效率，是决定[拉曼散射](@entry_id:141474)强度的核心物理量。[@problem_id:3013337]

#### 量[子图](@entry_id:273342)像：[谐振子](@entry_id:155622)与跃迁选择定则

在量子力学中，[声子模式](@entry_id:201212)被描述为一个[量子谐振子](@entry_id:140678)，其能级为 $E_v = \hbar\Omega(v+1/2)$。[声子](@entry_id:140728)坐标 $Q$ 变为算符 $\hat{Q}$，它只连接相邻的能级。因此，对于任何与 $\hat{Q}$ [线性相关](@entry_id:185830)的算符，其跃迁[选择定则](@entry_id:140784)均为 $\Delta v = \pm 1$。[@problem_id:3013336]

- 对于[红外吸收](@entry_id:188893)，跃迁概率正比于 $|\langle v_f | \hat{\boldsymbol{\mu}} | v_i \rangle|^2 \propto |\frac{d\boldsymbol{\mu}}{dQ}|^2 |\langle v_f | \hat{Q} | v_i \rangle|^2$。这要求 $\frac{d\boldsymbol{\mu}}{dQ} \neq 0$ 且 $\Delta v = v_f - v_i = \pm 1$。
- 对于[拉曼散射](@entry_id:141474)，跃迁概率正比于 $|\langle v_f | \hat{\boldsymbol{\alpha}} | v_i \rangle|^2 \propto |\frac{\partial\boldsymbol{\alpha}}{\partial Q}|^2 |\langle v_f | \hat{Q} | v_i \rangle|^2$。这要求 $\frac{\partial\boldsymbol{\alpha}}{\partial Q} \neq 0$ 且 $\Delta v = \pm 1$。

[斯托克斯散射](@entry_id:159214)对应于跃迁 $v \to v+1$，而[反斯托克斯散射](@entry_id:271867)对应于跃迁 $v \to v-1$。在热平衡温度 $T$ 下，[声子](@entry_id:140728)布居在不同能级的概率遵循玻尔兹曼分布。反斯托克斯过程的发生需要晶体初始处于[激发态](@entry_id:261453)（如 $v=1$），而斯托克斯过程可以从[基态](@entry_id:150928)（$v=0$）开始。因此，[反斯托克斯线](@entry_id:746484)的强度远弱于[斯托克斯线](@entry_id:199316)，它们的强度比近似为：
$$ \frac{I_{\text{AS}}}{I_{\text{S}}} \approx \frac{P(v=1)}{P(v=0)} = \exp\left(-\frac{\hbar\Omega}{k_B T}\right) $$
这种强度不对称性是量子统计的直接体现，纯粹的经典[洛伦兹模型](@entry_id:144803)无法解释。[@problem_id:3013336]

### 对称性及其推论

晶体的对称性对[光谱选择定则](@entry_id:139860)施加了极其严格的约束。其中最著名的推论之一是针对具有反演对称性（[中心对称](@entry_id:144242)）晶体的**[互斥](@entry_id:752349)定则（rule of mutual exclusion）**。

在[中心对称](@entry_id:144242)晶体中，每一个 $\mathbf{q}=\mathbf{0}$ 的[声子模式](@entry_id:201212)都具有确定的**宇称（parity）**：在空间反演操作（$\mathbf{r} \to -\mathbf{r}$）下，其[简正坐标](@entry_id:143194) $Q$ 要么不变（偶宇称，gerade, g），要么变号（奇宇称，ungerade, u）。

相互作用算符也具有确定的宇称：[@problem_id:3013307]
- **电偶极矩算符 $\hat{\boldsymbol{\mu}}$** 是一个[极性矢量](@entry_id:184542)，具有**奇宇称** (ungerade)。
- **[极化率张量](@entry_id:191938)算符 $\hat{\boldsymbol{\alpha}}$** 是一个[二阶张量](@entry_id:199780)，具有**偶宇称** (gerade)。

根据量子力学，一个跃迁过程被允许的条件是其跃迁矩阵元的被积函数必须是全对称的（即偶宇称）。对于[基态](@entry_id:150928)到第一[激发态](@entry_id:261453)的跃迁，这意味着：
- **红外活性**：跃迁矩阵元为 $\langle \psi_1 | \hat{\boldsymbol{\mu}} | \psi_0 \rangle$。为使整体为偶宇称，[声子](@entry_id:140728)[波函数](@entry_id:147440) $\psi_1$ 的宇称必须与 $\hat{\boldsymbol{\mu}}$ 的宇称相同，即**[奇宇称](@entry_id:147965)**。因此，只有**奇宇称 (ungerade) 的[声子模式](@entry_id:201212)才是红外活性的**。
- **拉曼活性**：跃迁[矩阵元](@entry_id:186505)为 $\langle \psi_1 | \hat{\boldsymbol{\alpha}} | \psi_0 \rangle$。为使整体为偶宇称，$\psi_1$ 的宇称必须与 $\hat{\boldsymbol{\alpha}}$ 的宇称相同，即**偶宇称**。因此，只有**偶宇称 (gerade) 的[声子模式](@entry_id:201212)才是拉曼活性的**。

由此可得互斥定则：**在[中心对称](@entry_id:144242)晶体中，一个[声子模式](@entry_id:201212)不能同时既是[红外活性](@entry_id:267987)的又是[拉曼活性](@entry_id:264824)的**。[@problem_id:3013307] [@problem_id:3013336] 这个强大的定则是判断晶体是否具有反演对称中心的重要依据。

此外，拉曼张量 $\mathbf{R}_{ij}$ 的具体形式（哪些分量非零）由[声子模式](@entry_id:201212)的对称性（[不可约表示](@entry_id:263310)）和晶体的[点群对称性](@entry_id:141230)共同决定。这导致了**偏振选择定则**，即拉曼散射强度依赖于入射光和散射[光的偏振](@entry_id:262080)方向，通过分析偏振可以确定[声子模式](@entry_id:201212)的对称性。[@problem_id:3013337]

### 高级主题与[多体效应](@entry_id:173569)

#### 极性晶体中的[LO-TO劈裂](@entry_id:138758)

在离子性较强的极性晶体（如 GaAs, NaCl）中，$\mathbf{q} \approx \mathbf{0}$ 的光学声子会进一步区分为**横光学（TO）**和**纵光学（LO）**模式，且它们的频率会发生劈裂（$\omega_{\text{LO}} > \omega_{\text{TO}}$）。[@problem_id:3013332]

这种劈裂源于长程[库仑相互作用](@entry_id:747947)在长波极限下的[宏观电场](@entry_id:196409)效应：
- **TO 模式**：原子[振动](@entry_id:267781)方向垂直于[波矢](@entry_id:178620) $\mathbf{q}$。这导致[宏观极化](@entry_id:141855)强度 $\mathbf{P}$ 也垂直于 $\mathbf{q}$。根据电动力学，$\nabla \cdot \mathbf{P} = i\mathbf{q} \cdot \mathbf{P} = 0$，因此不会产生宏观纵向[电场](@entry_id:194326)。其频率 $\omega_{\text{TO}}$ 主要由短程作用力决定。
- **LO 模式**：原子[振动](@entry_id:267781)方向平行于[波矢](@entry_id:178620) $\mathbf{q}$。这导致 $\mathbf{P} \parallel \mathbf{q}$，从而产生一个不为零的极化散度 $\nabla \cdot \mathbf{P} \neq 0$。这个极化散度如同束缚[电荷](@entry_id:275494)，会诱导出一个宏观的纵向[电场](@entry_id:194326) $\mathbf{E}$。这个[宏观电场](@entry_id:196409)对离子施加了一个额外的恢复力，使得[晶格](@entry_id:196752)“更硬”，从而将 LO 模式的频率 $\omega_{\text{LO}}$ 提升到 $\omega_{\text{TO}}$ 之上。

劈裂的大小与材料的离子性密切相关，后者由**[玻恩有效电荷](@entry_id:144855)（Born effective charge）$Z^*$** 量化。$Z^*$ 越大，表示原子位移产生的极化强度越大，从而 LO 模式中感生的[宏观电场](@entry_id:196409)越强，恢复力也越大，最终导致更大的 LO-TO 劈裂。

由于光是横波，其[电场](@entry_id:194326)矢量垂直于传播方向 $\mathbf{k}$。在[红外吸收](@entry_id:188893)中，$\mathbf{q}=\mathbf{k}$，因此光场只能与同样是横向的 TO [声子模式](@entry_id:201212)直接耦合，而不能直接激发 LO [声子](@entry_id:140728)。[@problem_id:3013311]

#### [共振拉曼散射](@entry_id:184891)与荧光

[拉曼散射](@entry_id:141474)的强度并非一成不变，它强烈依赖于入射光子能量 $\hbar\omega_L$。描述这一现象需要超越经典[极化率](@entry_id:143513)模型，采用完整的量子力学**Kramers-Heisenberg-Dirac (KHD)** 微扰公式。该公式表明散射振幅依赖于一系列包含能量差的“能量分母”。[@problem_id:3013335]

- **非[共振拉曼散射](@entry_id:184891)**：当 $\hbar\omega_L$ 远小于材料的任何电子跃迁能（如[带隙](@entry_id:191975) $E_g$）时，能量分母很大且对频率不敏感。此时 KHD 公式可以近似简化为之前讨论的、与频率无关的拉曼张量模型，即**普拉切克（Placzek）近似**。此过程中的中间电子态是“虚的”，相互作用时间极短（飞秒量级）。[@problem_id:3013334]

- **[共振拉曼散射](@entry_id:184891) (RRS)**：当 $\hbar\omega_L$ 调谐到接近某个真实的电子态能量（如激子能级 $E_X$）时，某个能量分母趋近于零，导致[散射截面](@entry_id:140322)发生几个[数量级](@entry_id:264888)的巨大增强。此时，分母中的虚部（与电子态的[退相干时间](@entry_id:154396) $T_2$ 相关）使其保持有限。尽管 RRS 过程通过一个真实的电子能级进行，但它仍然是一个单一的、相干的量子过程，其[特征时间尺度](@entry_id:276738)由电子态的相干寿命 $T_2$（通常为几十飞秒）决定，而并非真实的粒子布居。[@problem_id:3013334]

- **与荧光的区别**：必须将 RRS 与**荧光（fluorescence）**严格区分。荧光是一个非相干的两步过程：(1) [光子](@entry_id:145192)被吸收，真实地在材料中产生一个长寿命（由辐射和[非辐射复合](@entry_id:267336)寿命 $\tau_X$ 决定，通常为纳秒量级）的[激发态](@entry_id:261453)粒子布居；(2) 这个布居的粒子在失去与入射光的相位记忆后，再自发辐射出[光子](@entry_id:145192)。因此，RRS 的出射[光子能量](@entry_id:139314)严格跟进入射光（$\omega_s = \omega_L \pm \Omega$），而荧光的发射能量固定在电子能级附近，与入射光能量无关（只要 $\hbar\omega_L \ge E_X$）。两者的时间尺度也截然不同（飞秒 vs. 纳秒）。[@problem_id:3013334]

#### [电子-声子耦合](@entry_id:139197)与[声子](@entry_id:140728)自能

在导体或[半导体](@entry_id:141536)中，[声子](@entry_id:140728)可以与电子（或空穴）发生相互作用。这种**[电子-声子耦合](@entry_id:139197)**会深刻地影响[声子](@entry_id:140728)的性质，并通过拉曼[光谱](@entry_id:185632)表现出来。[多体理论](@entry_id:169452)提供了一个描述此效应的强大框架，即**[声子](@entry_id:140728)[自能](@entry_id:145608)（phonon self-energy）$\Pi(\omega)$**。[@problem_id:3013330]

[声子](@entry_id:140728)自能是一个复数函数 $\Pi(\omega) = \text{Re}\Pi(\omega) + i\text{Im}\Pi(\omega)$，它修正了“裸”[声子](@entry_id:140728)的[传播子](@entry_id:139558)。
- **实部 $\text{Re}\Pi(\omega)$** 导致[声子频率](@entry_id:753407)的**重整化（renormalization）**，即观测到的[声子频率](@entry_id:753407)会从未受扰动的频率 $\Omega_0$ 发生移动。
- **虚部 $\text{Im}\Pi(\omega)$** 描述了[声子](@entry_id:140728)通过衰变成[电子-空穴对](@entry_id:142506)等过程而获得的有限寿命，从而导致[声子](@entry_id:140728)拉曼峰的**展宽**。

因果律要求自能的实部和虚部通过 **Kramers-Kronig (KK) 关系**相互关联。这意味着由[电子-声子耦合](@entry_id:139197)引起的任何频率移动都必然伴随着相应的[线宽](@entry_id:199028)变化，反之亦然。[@problem_id:3013330]

当一个分立的[声子模式](@entry_id:201212)的能量恰好落在一个连续的[电子激发](@entry_id:190531)谱（如[金属中的电子](@entry_id:138687)-空穴对[连续谱](@entry_id:155477)）之内时，两种散射途径会发生量子干涉。这不再产生对称的洛伦兹峰形，而是导致一种特征性的非对称线型，称为**[法诺共振](@entry_id:145500)（Fano resonance）**。[@problem_id:3013335] 拉曼[光谱](@entry_id:185632)中的[法诺线型](@entry_id:160361)是[电子-声子耦合](@entry_id:139197)存在的一个明确证据。