## 引言
近年来，[扭转双层石墨烯](@entry_id:145647)（Twisted Bilayer Graphene, TBG）已成为凝聚态物理领域一颗璀璨的新星。当两层[石墨烯](@entry_id:143512)堆叠并以一个约为1.1度的微小“[魔角](@entry_id:138416)”相互扭转时，这个系统展现出了一系列出人意料的奇异物相，包括关联绝缘态和非常规超[导电性](@entry_id:137481)。这一发现彻底改变了我们对二维材料中电子行为的理解，揭示了仅通过几何调控就能开启[强关联物理](@entry_id:273328)世界的大门。然而，这些新奇现象背后的物理机制是什么？为何一个简单的转角能引发如此深刻的变革？本文旨在系统性地回答这些问题，为读者构建一个关于[魔角](@entry_id:138416)物理的完整知识框架。

本文将分为三个核心部分，引导读者逐步深入这个迷人的领域。在“**原理与机制**”一章中，我们将从单层[石墨烯](@entry_id:143512)的基础电子结构出发，构建描述扭转体系的Bistritzer-MacDonald[连续模](@entry_id:158807)型，并详细推导[魔角](@entry_id:138416)的出现以及平坦能带的形成机理，同时探讨[晶格](@entry_id:196752)弛豫与[能带拓扑](@entry_id:182035)等关键修正。接下来，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将探讨[平带物理](@entry_id:188459)如何催生出丰富的关联[物态](@entry_id:139436)，并展示[魔角石墨烯](@entry_id:140710)如何作为一个理想的平台，连接起非常规超导、拓扑物理和强[磁场](@entry_id:153296)物理等多个前沿研究方向。最后，通过“**动手实践**”部分提供的一系列计算问题，读者将有机会亲手应用所学理论，巩固对核心概念的理解。通过这一结构化的学习路径，我们将一同揭开[扭转双层石墨烯](@entry_id:145647)中蕴藏的深刻物理画卷。

## 原理与机制

本章旨在深入阐述[扭转双层石墨烯](@entry_id:145647)中奇异物理现象背后的基本原理和核心机制。我们将从构成材料的基础单元——单层石墨烯的[晶格](@entry_id:196752)与[电子结构](@entry_id:145158)出发，逐步构建起描述扭转体系的[连续模](@entry_id:158807)型，并最终揭示[魔角](@entry_id:138416)的出现及其相关的物理内涵。

### [石墨烯](@entry_id:143512)单层：[晶格](@entry_id:196752)与[电子结构](@entry_id:145158)回顾

理解[扭转双层石墨烯](@entry_id:145647)的前提是精确掌握单层石墨烯的结构。[石墨烯](@entry_id:143512)的碳原子[排列](@entry_id:136432)成一个二维蜂窝状[晶格](@entry_id:196752)。然而，[蜂窝晶格](@entry_id:188740)本身并非一个布拉维[晶格](@entry_id:196752)（Bravais lattice），因为它不满足[平移对称性](@entry_id:171614)下所有格点等价的条件。取而代之，它可以被精确地描述为一个带有双原子基元（two-atom basis）的三角布拉维[晶格](@entry_id:196752)。

具体来说，我们可以定义一组[原初格矢](@entry_id:270646)（primitive lattice vectors）$\boldsymbol{a}_{1}$ 和 $\boldsymbol{a}_{2}$ 来生成这个三角[晶格](@entry_id:196752)。一种常见的选择是：
$$
\boldsymbol{a}_{1}=\frac{a}{2}\,\hat{\boldsymbol{x}}+\frac{\sqrt{3}\,a}{2}\,\hat{\boldsymbol{y}}, \qquad
\boldsymbol{a}_{2}=-\frac{a}{2}\,\hat{\boldsymbol{x}}+\frac{\sqrt{3}\,a}{2}\,\hat{\boldsymbol{y}}
$$
其中 $a$ 是三角[晶格](@entry_id:196752)的[晶格常数](@entry_id:158935)。为了构成蜂窝结构，每个[原胞](@entry_id:159354)内必须包含两个不等价的碳原子，它们分别属于两个子[晶格](@entry_id:196752)，通常标记为 $A$ 和 $B$。若我们将 $A$ 子[晶格](@entry_id:196752)的一个原子置于[晶格](@entry_id:196752)原点 $\boldsymbol{\tau}_{A}=\boldsymbol{0}$，那么与其最近邻的 $B$ 子[晶格](@entry_id:196752)原子的位置可以由一个[基矢](@entry_id:199546) $\boldsymbol{\tau}_{B}$ 给出。一个形成规整蜂窝结构的正确选择是 $\boldsymbol{\tau}_{B} = (\boldsymbol{a}_{1}+\boldsymbol{a}_{2})/3$ [@problem_id:3022766]。

在动量空间中，[晶格](@entry_id:196752)的性质由其倒易晶格（reciprocal lattice）描述。倒易晶格的[原初格矢](@entry_id:270646) $\boldsymbol{b}_{1}$ 和 $\boldsymbol{b}_{2}$ 由关系 $\boldsymbol{a}_{i} \cdot \boldsymbol{b}_{j} = 2\pi\delta_{ij}$ 唯一确定。对于上述 $\boldsymbol{a}_{1}$ 和 $\boldsymbol{a}_{2}$ 的选择，相应的倒易格矢为：
$$
\boldsymbol{b}_{1}=\frac{2\pi}{a}\left(1, \frac{1}{\sqrt{3}}\right), \qquad \boldsymbol{b}_{2}=\frac{2\pi}{a}\left(-1, \frac{1}{\sqrt{3}}\right)
$$
[第一布里渊区](@entry_id:269110)（First Brillouin Zone, BZ）是[倒易晶格](@entry_id:136718)的[维格纳-赛兹原胞](@entry_id:137574)（Wigner-Seitz cell），对于[石墨烯](@entry_id:143512)而言，它是一个六边形。

[石墨烯](@entry_id:143512)最引人注目的电子学特性源于其在布里渊区六个顶角处的行为。这六个顶角实际上只对应两个不等价的高对称性点，分别标记为 $\boldsymbol{K}$ 和 $\boldsymbol{K}'$ 点，也称为[狄拉克点](@entry_id:276156)（Dirac points）。在这两个点附近，电子的能带呈现出线性能量-动量色散关系，其行为可由无质量的狄拉克方程有效描述。对于上述[晶格](@entry_id:196752)约定，沿 $k_x$ 轴的两个不等价的[狄拉克点](@entry_id:276156)可以被确定为 $\boldsymbol{K} = (\boldsymbol{b}_{1}-\boldsymbol{b}_{2})/3 = (4\pi/(3a), 0)$ 和 $\boldsymbol{K}'=-\boldsymbol{K}$ [@problem_id:3022766]。这两个不等价的谷（valley），即 $\boldsymbol{K}$ 谷和 $\boldsymbol{K}'$ 谷，构成了[石墨烯](@entry_id:143512)低能物理的自由度。

### 从堆叠到莫尔图案

当两层石墨烯堆叠在一起时，其物理性质强烈地依赖于层间的相对[排列](@entry_id:136432)方式，即堆叠序。最简单的高对称性堆叠方式包括 $AA$ 堆叠和 $AB$（伯纳尔）堆叠 [@problem_id:3022741]。
- **$AA$ 堆叠**：通过将第二层相对于第一层进行零位移（$\boldsymbol{\delta}=\boldsymbol{0}$）得到。在此构型中，顶层的 $A$($B$)原子精确地位于底层 $A$($B$)原子的正上方。这种结构保留了六重旋转对称性（$C_{6z}$）和空间反演对称性（$I$）。
- **$AB$ 堆叠**：通过将第二层相对于第一层平移一个最近邻矢量（例如，$\boldsymbol{\delta}=\boldsymbol{\tau}$，其中 $\boldsymbol{\tau}$ 是从 $A$ 位指向 $B$ 位的矢量）得到。此时，顶层的 $A$ 原子位于底层的 $B$ 原子之上，而顶层的 $B$ 原子则位于底层蜂窝六边形的中心。这种堆叠破坏了 $C_{6z}$ 对称性，但保留了三重[旋转对称](@entry_id:137077)性（$C_{3z}$）和空间[反演对称性](@entry_id:269948)。与之相关的 $BA$ 堆叠（$\boldsymbol{\delta}=-\boldsymbol{\tau}$）则与 $AB$ 堆叠通过 $C_{2z}$ 旋转等[对称操作](@entry_id:143398)相关联，具有相同的对称性和能量。

当两层石墨烯之间存在一个微小的转角 $\theta$ 时，情况变得更为复杂和有趣。两套周期性的[蜂窝晶格](@entry_id:188740)发生干涉，形成一个更大尺度的周期性图案，即**莫尔[超晶格](@entry_id:200197)**（moiré superlattice）。这个莫尔图案的周期性 $L_m$ 远大于石墨烯的原子晶格常数 $a$，且在小角度极限下与转角成反比，即 $L_m \approx a/\theta$（其中 $\theta$ 以弧度计）。

这种新的、长程的周期性同样反映在[动量空间](@entry_id:148936)中。莫尔[超晶格](@entry_id:200197)对应一个更小的**莫尔[布里渊区](@entry_id:142395)**（moiré Brillouin Zone, mBZ）。莫尔倒易晶格的格矢 $\boldsymbol{g}$ 可以被理解为两层石墨烯各自[倒易晶格矢量](@entry_id:263351)的差。假设我们将顶层和底层分别旋转 $+\theta/2$ 和 $-\theta/2$，那么它们各自的倒易格矢变为 $\boldsymbol{b}_i^{(1)} = \mathbf{R}(+\theta/2)\boldsymbol{b}_i$ 和 $\boldsymbol{b}_i^{(2)} = \mathbf{R}(-\theta/2)\boldsymbol{b}_i$。莫尔倒易晶格的[原初格矢](@entry_id:270646) $\boldsymbol{g}_i$ 可以由这些旋转后的格矢的最小非零差值给出，即 $\boldsymbol{g}_i = \boldsymbol{b}_i^{(1)} - \boldsymbol{b}_i^{(2)}$。

利用简单的几何关系，我们可以推导出莫尔倒易格矢的模长与单层倒易格矢模长的关系 [@problem_id:3022767]。两个大小相等、夹角为 $\theta$ 的矢量之差的模长为：
$$
|\boldsymbol{g}_i|^2 = |\boldsymbol{b}_i^{(1)}|^2 + |\boldsymbol{b}_i^{(2)}|^2 - 2 \boldsymbol{b}_i^{(1)} \cdot \boldsymbol{b}_i^{(2)} = 2|\boldsymbol{b}_i|^2 - 2|\boldsymbol{b}_i|^2\cos\theta = 4|\boldsymbol{b}_i|^2 \sin^2(\theta/2)
$$
因此，莫尔倒易晶格的特征尺度 $k_\theta = |\boldsymbol{g}_i|$ 与单层[倒易晶格](@entry_id:136718)尺度 $|\boldsymbol{b}_i|$ 的关系为：
$$
\frac{k_\theta}{|\boldsymbol{b}_i|} = 2\sin(\frac{\theta}{2})
$$
在小角度 $\theta \ll 1$ 的情况下，$\sin(\theta/2) \approx \theta/2$，所以 $k_\theta \approx |\boldsymbol{b}_i| \theta$。这定量地表明，随着真实空间莫尔周期 $L_m$ 的增大，[动量空间](@entry_id:148936)的莫尔布里渊区尺寸 $k_\theta$ 会相应缩小。

### Bistritzer-MacDonald [连续模](@entry_id:158807)型

为了描述[扭转双层石墨烯](@entry_id:145647)在小角度下的低能物理，Bistritzer和MacDonald提出了一个强大的**[连续模](@entry_id:158807)型**（continuum model）。该模型的核心思想是，由于莫尔周期 $L_m$ 远大于原子[晶格常数](@entry_id:158935) $a$，层间的耦合可以被视为一个在原子尺度上平滑、但在莫尔尺度上周期性变化的微扰。

**谷[解耦近似](@entry_id:144820)**

首先，一个关键的简化是**谷解耦**（valley decoupling）[@problem_id:3022785]。要将一个电子从 $\boldsymbol{K}$ 谷散射到 $\boldsymbol{K}'$ 谷，需要一个大小约为 $|\boldsymbol{K}-\boldsymbol{K}'| \sim 1/a$ 的动量转移。然而，莫尔[势场](@entry_id:143025)的主要傅里叶分量所提供的动量转移尺度为 $k_\theta \sim \theta/a$。在小角度极限下（例如 $\theta \ll 1$），$k_\theta \ll 1/a$。这意味着平滑的莫尔势场无法提供足够的动量来直接连接两个谷。因此，由莫尔[势场](@entry_id:143025)引起的[谷间散射](@entry_id:136281)被极大地抑制了，其振幅随 $a/L_m \sim \theta$ 的减小而快速衰减。这使得我们可以构建一个在谷指标上近似[块对角化](@entry_id:145518)的[哈密顿量](@entry_id:172864)，即分别独立地处理 $\boldsymbol{K}$ 谷和 $\boldsymbol{K}'$ 谷的物理。

**[哈密顿量](@entry_id:172864)的构建**

在一个固定的谷（例如 $\boldsymbol{K}$ 谷）内，[连续模](@entry_id:158807)型[哈密顿量](@entry_id:172864)可以写成一个 $4 \times 4$ 的矩阵形式，其[基矢](@entry_id:199546)为 $(\psi_{A1}, \psi_{B1}, \psi_{A2}, \psi_{B2})$，其中 $A/B$ 是子[晶格](@entry_id:196752)指标，$1/2$是层指标。该[哈密顿量](@entry_id:172864)具有如下块结构 [@problem_id:3022774]：
$$
H = \begin{pmatrix} h_{+\theta/2}(-i\nabla)  T(\boldsymbol{r}) \\ T^\dagger(\boldsymbol{r})  h_{-\theta/2}(-i\nabla) \end{pmatrix}
$$

- **层内[哈密顿量](@entry_id:172864) $h_{\pm\theta/2}$**：对角块描述了两个独立旋转的[石墨烯](@entry_id:143512)单层。每一层的低能激发都是围绕其[狄拉克点](@entry_id:276156)的[无质量狄拉克费米子](@entry_id:142256)。在一个固定的[全局坐标系](@entry_id:171029)中，将单层旋转角度 $\phi$ 等效于旋转其[动量算符](@entry_id:151743)。因此，对于旋转了 $\pm\theta/2$ 的两层，其[哈密顿量](@entry_id:172864)为：
$$
h_{\pm\theta/2}(-i\nabla) = -\hbar v_F \boldsymbol{\sigma} \cdot (R(\pm\theta/2)(-i\nabla))
$$
其中 $v_F$ 是单层[石墨烯](@entry_id:143512)的费米速度，$\boldsymbol{\sigma}=(\sigma_x, \sigma_y)$ 是作用于子[晶格](@entry_id:196752)空间的泡利矩阵，$R(\phi)$ 是[二维旋转矩阵](@entry_id:154975)。

- **层间隧穿[哈密顿量](@entry_id:172864) $T(\boldsymbol{r})$**：非对角块 $T(\boldsymbol{r})$ 描述了依赖于局域位置的层间[电子隧穿](@entry_id:180411)。由于它具有莫尔超晶格的周期性，可以被傅里叶展开为莫尔倒易格矢 $\boldsymbol{q}_j$ 的级数。只保留最低阶的三个傅里叶分量（对应最小的三个非零莫尔倒易格矢），隧穿项可以写为：
$$
T(\boldsymbol{r})=\sum_{j=1}^{3} T_j e^{i\boldsymbol{q}_j\cdot \boldsymbol{r}}
$$
其中 $\boldsymbol{q}_1, \boldsymbol{q}_2, \boldsymbol{q}_3$ 是由对称性关联的三个最小莫尔倒易格矢，满足 $\boldsymbol{q}_1+\boldsymbol{q}_2+\boldsymbol{q}_3=\boldsymbol{0}$。矩阵 $T_j$ 的形式由对称性决定，并由两个参数 $w_0$ 和 $w_1$ 描述。$w_0$ 描述了子[晶格](@entry_id:196752)守恒的隧穿（$A_1 \leftrightarrow A_2, B_1 \leftrightarrow B_2$），这在 $AA$ 堆叠区域占主导。$w_1$ 描述了子[晶格](@entry_id:196752)交换的隧穿（$A_1 \leftrightarrow B_2, B_1 \leftrightarrow A_2$），这在 $AB/BA$ 堆叠区域占主导。一个符合对称性要求的[标准形式](@entry_id:153058)为 [@problem_id:3022774]：
$$
T_1=\begin{pmatrix} w_0  w_1 \\ w_1  w_0 \end{pmatrix}, \quad T_2=\begin{pmatrix} w_0  w_1 e^{-i 2\pi/3} \\ w_1 e^{+i 2\pi/3}  w_0 \end{pmatrix}, \quad T_3=\begin{pmatrix} w_0  w_1 e^{+i 2\pi/3} \\ w_1 e^{-i 2\pi/3}  w_0 \end{pmatrix}
$$
这种形式确保了[哈密顿量](@entry_id:172864)具有莫尔[晶格](@entry_id:196752)的三重[旋转对称](@entry_id:137077)性。

**[动量空间](@entry_id:148936)图像**

在[动量空间](@entry_id:148936)中，层间隧穿项 $T(\boldsymbol{r})$ 起到了耦合不同动量态的作用。一个在第一层中、动量为 $\boldsymbol{k}$（相对于该层的[狄拉克点](@entry_id:276156)）的电子，可以通过隧穿跃迁到第二层，其动量变为 $\boldsymbol{k}+\boldsymbol{q}_j$（相对于第二层的[狄拉克点](@entry_id:276156)）。这种耦合过程可以无限进行下去，形成一个以莫尔倒易格矢 $\boldsymbol{q}_j$ 连接起来的无限动量格点网络。

为了实际计算，需要对这个无限的[动量空间](@entry_id:148936)进行截断。一个常用的截断方案是所谓的“第一星截断”（first-star truncation）。例如，考虑一个从第一层出发，经历一次到第二层的“[前向散射](@entry_id:191808)”，再经历一次回到第一层的“后向散射”的过程 [@problem_id:3022740]。初始态在第一层动量为 $\boldsymbol{k}$，一次[前向散射](@entry_id:191808)后到达第二层动量为 $\boldsymbol{k}+\boldsymbol{q}_j$，再经一次后向散射后回到第一层，动量变为 $(\boldsymbol{k}+\boldsymbol{q}_j) - \boldsymbol{q}_l$。相对于初始动量 $\boldsymbol{k}$，动量偏移为 $\boldsymbol{q}_j - \boldsymbol{q}_l$。所有这些由一次往返过程产生的动量偏移，连同零偏移本身，构成了一个有效的[基组](@entry_id:160309)。这个[基组](@entry_id:160309)包含了[零矢量](@entry_id:155273)和六个模长为 $\sqrt{3}|\boldsymbol{q}_j|$ 的矢量，总共包含7个动量态。这个有限的[基组](@entry_id:160309)构成了求解[连续模](@entry_id:158807)型[哈密顿量](@entry_id:172864)谱的最小现实模型的基础。

### [魔角](@entry_id:138416)的出现

Bistritzer-MacDonald模型最惊人的预言是，在特定的“[魔角](@entry_id:138416)”$\theta_m$下，系统低能区的有效费米速度会消失，导致能带变得异常平坦。

我们可以通过微扰论来理解这一现象。将层间耦合视为对层内狄拉克[哈密顿量](@entry_id:172864)的微扰。考虑一个在第一层[狄拉克点](@entry_id:276156)附近、动量为 $\boldsymbol{k}$ 的电子。它可以通过隧穿虚拟地跃迁到第二层，然后再跃迁回来。这个二阶微扰过程修正了电子自身的能量，从而重新归一化了其动能项。

有效哈密顿量的 $\boldsymbol{k}$-线性项可以写为 [@problem_id:3022793]：
$$
H_{\text{eff}}^{(1)}(\boldsymbol{k}) = -\hbar v_F (\boldsymbol{\sigma}\cdot\boldsymbol{k}) + \sum_{j=1}^3 T_j \frac{1}{-H_2(\boldsymbol{k}-\boldsymbol{q}_j)} T_j^\dagger \Big|_{\text{linear in }\boldsymbol{k}}
$$
在小 $\boldsymbol{k}$ 极限下，$| \boldsymbol{k}-\boldsymbol{q}_j | \approx k_\theta$，分母中的能量差近似为 $\hbar v_F k_\theta$。经过计算，$\boldsymbol{k}$-线性修正项与原始的动能项形式相同，但符号相反。这导致有效费米速度被重新归一化：
$$
v^*(\theta) = v_F \left( 1 - 3\alpha^2 \right)
$$
其中 $\alpha = \frac{w_1}{\hbar v_F k_\theta}$ 是一个无量纲的耦合常数，它代表了层间耦合能 $w_1$ 与莫尔尺度上的动能 $\hbar v_F k_\theta$ 之间的比值。这里的计算采用了手性极限（chiral limit, $w_0=0$）。

当括号内的项为零时，有效费米速度消失，即 $v^*(\theta_m)=0$。这个条件是：
$$
1 - 3\alpha^2 = 0 \implies \alpha = \frac{1}{\sqrt{3}}
$$
将 $\alpha$ 和 $k_\theta = 2 k_D \sin(\theta/2)$ 的定义代入，我们可以解出第一个[魔角](@entry_id:138416) $\theta_m$ 满足的条件 [@problem_id:3022793]：
$$
\sin(\theta_m/2) = \frac{\sqrt{3}w_1}{2\hbar v_F k_D}
$$
求解 $\theta_m$ 得到：
$$
\theta_m = 2\arcsin\left(\frac{\sqrt{3}w_1}{2\hbar v_F k_D}\right)
$$
在[魔角](@entry_id:138416)处，电子的动能被层间耦合效应有效“淬灭”，导致在[狄拉克点](@entry_id:276156)附近[形成能](@entry_id:142642)量几乎不随动量变化的平坦能带。正是这些平带使得电子间相互作用的效应被急剧放大，从而催生了诸如超导和关联绝缘态等[强关联物理](@entry_id:273328)现象。

### 超越理想化模型：带宽与拓扑

虽然上述理想化模型成功预言了[魔角](@entry_id:138416)和平带的出现，但要更精确地理解真实的物理系统，我们必须考虑一些更精细的效应。

#### [晶格](@entry_id:196752)弛豫的作用

真实的晶体并非刚性的。为了最小化总能量，原子会偏离其在理想莫尔图案中的位置，这一过程称为**[晶格](@entry_id:196752)弛豫**（lattice relaxation）[@problem_id:3022771]。总能量包含层内[弹性形变](@entry_id:161971)能和层间黏附能。由于 $AB/BA$ 堆叠的黏附能低于 $AA$ 堆叠，系统会自发地进行结构调整：在平面内，高能量的 $AA$ 堆叠区域会收缩，而低能量的 $AB/BA$ 堆叠区域会扩张；在垂直方向，为了进一步降低能量，$AA$ 区域的层间距会增大，而 $AB/BA$ 区域的层间距则保持紧密。

这种结构重构对[连续模](@entry_id:158807)型的参数 $w_0$ 和 $w_1$ 产生了显著的重新归一化。
- $w_0$ 主要由 $AA$ 区域的隧穿贡献。由于 $AA$ 区域面积收缩且层间距增大（层间隧穿随距离指数衰减），$w_0$ 的值被大大削弱。
- $w_1$ 主要由 $AB/BA$ 区域贡献。这些区域面积扩张且层间距保持紧密，因此 $w_1$ 的值相对保持不变或受影响较小。

最终结果是，在考虑了[晶格](@entry_id:196752)弛豫的更真实模型中，$w_0$ 远小于 $w_1$ ($w_0 \ll w_1$)。这一不等关系对于在[魔角](@entry_id:138416)附近形成孤立且带宽极窄的平带至关重要。

#### 为何平带不“平”

一个常见的误解是，在[魔角](@entry_id:138416)处 $v^*(\theta)=0$ 意味着能带是严格平坦的（即带宽为零）。然而，这是不正确的 [@problem_id:3022826]。群速度的定义是 $ \boldsymbol{v}(\boldsymbol{k}) = \frac{1}{\hbar}\nabla_{\boldsymbol{k}} E(\boldsymbol{k})$。$v^*(\theta_m)=0$ 仅仅意味着在莫尔布里渊区的[狄拉克点](@entry_id:276156)（高对称性点 $\boldsymbol{K}_{\mathrm{m}}$）处，[能带色散](@entry_id:138609) $E(\boldsymbol{k})$ 的一阶（线性）项消失了。

然而，$E(\boldsymbol{k})$ 在 $\boldsymbol{K}_{\mathrm{m}}$ 点附近的[泰勒展开](@entry_id:145057)式还包含更高阶的项：
$$
E(\boldsymbol{K}_{\mathrm{m}} + \boldsymbol{q}) \approx E(\boldsymbol{K}_{\mathrm{m}}) + c_2 |\boldsymbol{q}|^2 + c_3 f(\boldsymbol{q},\phi) + \dots
$$
即使线性项消失，由对称性所允许的二次项（决定能带曲率）和更高阶项（如三角翘曲 "trigonal warping"）通常仍然存在。这些高阶项的物理来源是电子与更高能量的“远程”能带之间的虚拟耦合，以及莫尔[势场](@entry_id:143025)中被忽略的高阶傅里叶分量。正是这些高阶项导致了能带在整个莫尔[布里渊区](@entry_id:142395)内仍然具有一定的[色散](@entry_id:263750)，从而产生一个有限的、非零的**剩余带宽**（residual bandwidth）。因此，[魔角](@entry_id:138416)处的能带是“准平坦”而非“绝对平坦”。

#### 平带的[脆弱拓扑](@entry_id:143829)

除了能量[色散](@entry_id:263750)，平带还具有非平庸的拓扑性质。[拓扑能带理论](@entry_id:141523)根据全局性质对能带进行分类，这种分类在没有关闭[能隙](@entry_id:191975)的情况下是稳固的。拓扑性质通常分为**稳定拓扑**（stable topology）和**[脆弱拓扑](@entry_id:143829)**（fragile topology）[@problem_id:3022769]。

- **稳定拓扑**由 K-理论描述，其拓扑不变量（如陈数）在与任意数目的“平庸”原子能带（trivial bands）耦合后依然保持不变。
- **[脆弱拓扑](@entry_id:143829)**则是一种更微妙的拓扑。它所描述的能带虽然在稳定分类下是平庸的（即其 K-理论[不变量](@entry_id:148850)为零），但自身却无法在保持对称性的前提下被形变为一组局域化的原子轨道（即无法被“瓦尼尔化”）。然而，这种拓扑“脆弱”之处在于，一旦与某些特定的平庸能带耦合，其[拓扑阻碍](@entry_id:634492)就会消失，整个系统就变得平庸了。

在单谷、单自旋的 Bistritzer-MacDonald 模型中，系统具有 $C_2\mathcal{T}$ 联合对称性（$C_2$为面内二重旋转，$\mathcal{T}$为[时间反演](@entry_id:182076)）。在此对称性保护下，平带的稳定拓扑不变量（陈数）被证明为零。然而，进一步的分析表明，这两条平带作为一个整体，具有一个非零的**[脆弱拓扑](@entry_id:143829)**[不变量](@entry_id:148850)，即[欧拉类](@entry_id:161259)（Euler class）不为零 [@problem_id:3022769]。这个非零的[欧拉类](@entry_id:161259)导致了一个瓦尼尔阻碍，意味着我们无法为这两条能带构造出满足所有对称性的局域化[瓦尼尔函数](@entry_id:145994)。这种拓扑性质既非平庸，也非稳定，是[脆弱拓扑](@entry_id:143829)的一个典型范例，它深刻地影响着[平带](@entry_id:139485)中的电子行为和相互作用的性质。