## 引言
[威克定理](@entry_id:137086)是现代[量子场论](@entry_id:138177)的基石之一，尤其在[路径积分表述](@entry_id:145051)中，它扮演着将抽象的[泛函积分](@entry_id:268544)转化为具体物理计算的关键角色。从根本上说，[路径积分](@entry_id:156701)提供了一种优雅的方式来描述量子系统从一个状态到另一个状态的所有可能历史的总和。然而，若无系统性的计算工具，这个强大的形式框架将难以应用。[威克定理](@entry_id:137086)正是解决了这一难题，它为计算[量子场论](@entry_id:138177)中的核心物理量——关联函数——提供了一套强大的组合算法，从而架起了理论模型与实验[可观测量](@entry_id:267133)之间的桥梁。

本文旨在深入剖析[路径积分](@entry_id:156701)框架下的[威克定理](@entry_id:137086)，从其基本原理到前沿应用，为读者构建一个完整而深入的知识体系。我们将分三个章节展开探讨：
- **原理与机制**：我们将从[高斯积分](@entry_id:187139)出发，揭示[威克定理](@entry_id:137086)的数学本质，并详细阐述其在玻色场和引入[格拉斯曼数](@entry_id:136855)的费米场中的具体形式与微妙差异。
- **应用与跨学科联系**：我们将展示[威克定理](@entry_id:137086)作为微扰论“引擎”的强大威力，探索其在粒子物理散射计算、凝聚态物质的集体行为，乃至[弯曲时空量子场论](@entry_id:184500)等多个领域的广泛应用。
- **动手实践**：最后，通过一系列精心设计的计算问题，读者将有机会亲手应用所学知识，巩固对[威克定理](@entry_id:137086)及其应用的理解。

通过本篇的学习，您不仅将掌握一个核心的计算技术，更将深刻体会到物理学不同分支背后统一的数学结构和思想。让我们首先进入第一章，探究[威克定理](@entry_id:137086)的根本原理与机制。

## 原理与机制

在上一章中，我们介绍了路径积分作为一种强大的[量子场论](@entry_id:138177)形式化方法。它将量子力学中的跃迁振幅重新表述为对场的所有可能构型的[泛函积分](@entry_id:268544)。对于可解的理论，尤其是那些作用量是场的二次型的“自由”理论，路径积分提供了一套系统而优雅的计算方法，用于计算关联函数。本章的核心是探讨**[威克定理](@entry_id:137086) (Wick's Theorem)** 在[路径积分](@entry_id:156701)框架下的原理与机制。该定理是连接抽象的[泛函积分](@entry_id:268544)与可计算的物理观测量（如[散射振幅](@entry_id:155369)和[衰变率](@entry_id:156530)）之间的关键桥梁，尤其是在微扰论中扮演着不可或缺的角色。

### 理论基础：高斯[路径积分](@entry_id:156701)与场的收缩

从根本上说，自由场的[路径积分](@entry_id:156701)是高斯积分在无限维[函数空间](@entry_id:143478)上的推广。对于一个由 $n$ 个变量 $x_i$ 组成的系统，其[高斯积分](@entry_id:187139)为：
$$
\int d^n x \exp\left(-\frac{1}{2} \sum_{i,j} x_i A_{ij} x_j\right) = \sqrt{\frac{(2\pi)^n}{\det A}}
$$
其中 $A$ 是一个正定对称矩阵。在此背景下，一个变量（或算符）$\mathcal{O}(x)$ 的[期望值](@entry_id:153208)由归一化的积分给出：
$$
\langle \mathcal{O}(x) \rangle = \frac{\int d^n x \, \mathcal{O}(x) \exp\left(-\frac{1}{2} x^T A x\right)}{\int d^n x \exp\left(-\frac{1}{2} x^T A x\right)}
$$
高斯积分的一个关键性质是，任意多个变量[乘积的期望值](@entry_id:201037)可以完全由两点函数（即二次矩）确定。具体而言，$\langle x_i x_j \rangle = (A^{-1})_{ij}$。对于一个包含多个变量的乘积，其[期望值](@entry_id:153208)等于将这些变量两两配对，然后将每对的[期望值](@entry_id:153208)相乘，并对所有可能的配对方式求和。这就是[威克定理](@entry_id:137086)的雏形。

在[量子场论](@entry_id:138177)中，场 $\phi(x)$ 取代了[离散变量](@entry_id:263628) $x_i$，而作用量 $S[\phi]$ 中的二次型算符（如克莱因-戈登算符 $-(\Box + m^2)$）取代了矩阵 $A$。两点关联函数，即**传播子 (propagator)**，则对应于该算符的逆，即[格林函数](@entry_id:147802)。我们将这个基本的配对操作称为**收缩 (contraction)**。

### 玻色场的[威克定理](@entry_id:137086)

对于一个实标量场 $\phi(x)$，其自由理论的拉格朗日量通常具有 $\mathcal{L} = \frac{1}{2}(\partial_\mu \phi)^2 - \frac{1}{2}m^2\phi^2$ 的形式。[威克定理](@entry_id:137086)断言，[场算符](@entry_id:140269)的时间排序乘积的[真空期望值](@entry_id:146340)（VEV）等于所有可能的[场算符](@entry_id:140269)对之间收缩的乘积之和。

单个收缩被定义为两个场的时间排序乘积的[真空期望值](@entry_id:146340)，即**[费曼传播子](@entry_id:140690) (Feynman propagator)**：
$$
\text{收缩: } \langle 0 | T\{\phi(x) \phi(y)\} | 0 \rangle \equiv i\Delta_F(x-y)
$$
其中 $T$ 表示时间排序。[费曼传播子](@entry_id:140690)是克莱因-戈登算符的[格林函数](@entry_id:147802)，满足：
$$
(\Box_x + m^2) i\Delta_F(x-y) = -i \cdot i \delta^{(4)}(x-y) = \delta^{(4)}(x-y)
$$
（在闵可夫斯基时空，通常定义 $(\Box_x + m^2) \Delta_F(x-y) = -i\delta^{(4)}(x-y)$）。

以四点关联函数为例，[威克定理](@entry_id:137086)给出了一个清晰的组合图像：
$$
\langle 0 | T\{\phi(x_1)\phi(x_2)\phi(x_3)\phi(x_4)\} | 0 \rangle = \langle T\{\phi_1\phi_2\}\rangle \langle T\{\phi_3\phi_4\}\rangle + \langle T\{\phi_1\phi_3\}\rangle \langle T\{\phi_2\phi_4\}\rangle + \langle T\{\phi_1\phi_4\}\rangle \langle T\{\phi_2\phi_3\}\rangle
$$
这可以表示为：
$$
i^2 \Delta_F(x_1-x_2)\Delta_F(x_3-x_4) + i^2 \Delta_F(x_1-x_3)\Delta_F(x_2-x_4) + i^2 \Delta_F(x_1-x_4)\Delta_F(x_2-x_3)
$$
这个原理的普适性在于，它不依赖于作用量的具体形式，只要作用量是场的二次型即可。例如，考虑一个具有非标准动能项的 Lifshitz 标量场理论，其作用量为 $S[\phi] = \int d^4x \, \left( \frac{1}{2}(\partial_0 \phi)^2 - \frac{\kappa}{2} (\nabla^2 \phi)^2 \right)$ [@problem_id:449953]。尽管其[色散关系](@entry_id:140395) $\omega^2 = \kappa k^4$ 与标准的洛伦兹不变理论不同，但由于作用量仍然是 $\phi$ 的二次型，该理论是高斯理论。因此，一旦我们计算出其对应的（非标准的）[费曼传播子](@entry_id:140690) $D(x-y)$，四点函数仍然遵循上述三项配对规则，即 $D(x_1-x_2)D(x_3-x_4) + (\text{其他两个配对})$。

对于[复标量场](@entry_id:159799)，情况类似，但收缩只在场与其复共轭之间非零。即，唯一的非零收缩是 $\langle 0 | T\{ \phi(x) \phi^\dagger(y) \} | 0 \rangle = i\Delta_F(x-y)$，而 $\langle T\{\phi\phi\}\rangle$ 和 $\langle T\{\phi^\dagger\phi^\dagger\}\rangle$ 均为零。这源于理论的 $U(1)$ 对称性（[电荷守恒](@entry_id:264158)）。因此，对于四点函数 $\langle 0 | T\{ \phi(x_1) \phi^\dagger(x_2) \phi(x_3) \phi^\dagger(x_4) \} | 0 \rangle$，只有两种可能的完全收缩方式：
$$
\langle 0 | T\{ \phi_1 \phi^\dagger_2 \phi_3 \phi^\dagger_4 \} | 0 \rangle = \langle T\{\phi_1\phi^\dagger_2\}\rangle \langle T\{\phi_3\phi^\dagger_4\}\rangle + \langle T\{\phi_1\phi^\dagger_4\}\rangle \langle T\{\phi_3\phi^\dagger_2\}\rangle
$$
$$
= -\Delta_F(x_1-x_2)\Delta_F(x_3-x_4) - \Delta_F(x_1-x_4)\Delta_F(x_3-x_2)
$$
[威克定理](@entry_id:137086)的一个强大推论是，我们可以将[微分](@entry_id:158718)算符移出时间排序的[期望值](@entry_id:153208)。例如，在计算包含 $(\Box_x+m^2)\phi(x)$ 这样一项的关联函数时，我们可以先应用[威克定理](@entry_id:137086)计算不带[微分](@entry_id:158718)算符的关联函数，然后对其结果作用[微分](@entry_id:158718)算符。利用传播子是格林函数这一事实，这通常会使计算大大简化，并将[传播子](@entry_id:139558)转换为狄拉克 $\delta$ 函数，从而揭示出[接触相互作用](@entry_id:150822)的本质 [@problem_id:449917]。

### 费米场的[威克定理](@entry_id:137086)：反对易的角色

当处理[费米子](@entry_id:146235)场（如[狄拉克场](@entry_id:156753) $\psi$）时，[路径积分](@entry_id:156701)需要使用[反交换的](@entry_id:262442)[格拉斯曼数](@entry_id:136855)。这导致了[威克定理](@entry_id:137086)的一个关键修改：在将[费米子算符](@entry_id:149120)重新排序以形成收缩对时，每次交换两个[费米子算符](@entry_id:149120)的位置，都会引入一个负号。

对于[费米子](@entry_id:146235)，基本的收缩是[狄拉克场](@entry_id:156753)的[费曼传播子](@entry_id:140690)，它是一个 $4 \times 4$ 的矩阵：
$$
\text{收缩: } \langle 0 | T\{\psi_\alpha(x) \bar{\psi}_\beta(y)\} | 0 \rangle \equiv iS_{F, \alpha\beta}(x-y)
$$
其中 $\alpha, \beta$ 是旋量指数。$\langle T\{\psi\psi\}\rangle$ 和 $\langle T\{\bar{\psi}\bar{\psi}\}\rangle$ 均为零。

考虑一个四点函数 $\langle 0 | T\{ \eta_1 \bar{\eta}_2 \eta_3 \bar{\eta}_4 \} | 0 \rangle$，其中 $\eta, \bar{\eta}$ 是通用的[格拉斯曼变量](@entry_id:199573) [@problem_id:449938]。收缩必须在 $\eta$ 和 $\bar{\eta}$ 之间进行。其结果是所有可能配对的总和，但每个配对的符号取决于将算符重新[排列](@entry_id:136432)成该配对所需的[置换符号](@entry_id:153173)。对于 $\langle \eta_a \bar{\eta}_b \eta_c \bar{\eta}_d \rangle$，结果为：
$$
\langle \eta_a \bar{\eta}_b \rangle \langle \eta_c \bar{\eta}_d \rangle - \langle \eta_a \bar{\eta}_d \rangle \langle \eta_c \bar{\eta}_b \rangle
$$
这个负号至关重要，它反映了[费米-狄拉克统计](@entry_id:140706)的[泡利不相容原理](@entry_id:141850)。第一项对应直接配对，而第二项（带负号）来自[交叉](@entry_id:147634)配对，其符号源于形成该配对所需的算符交换。

在处理具有内部结构（如[旋量](@entry_id:158054)指数）的[狄拉克场](@entry_id:156753)时，收缩本身就更加复杂。例如，计算一个包含特定手性投影的四点函数，如 $G = \langle 0 | T\{ \bar{\psi}_R(x_1) \psi_L(x_2) \bar{\psi}_L(x_3) \psi_R(x_4) \} | 0 \rangle$ [@problem_id:449932]。根据[费米子](@entry_id:146235)[威克定理](@entry_id:137086)，这等于 $\langle \bar{\psi}_R(1)\psi_L(2) \rangle \langle \bar{\psi}_L(3)\psi_R(4) \rangle - \langle \bar{\psi}_R(1)\psi_R(4) \rangle \langle \bar{\psi}_L(3)\psi_L(2) \rangle$。
每一项收缩，例如 $\langle \bar{\psi}_R(x_1) \psi_L(x_2) \rangle = \langle \bar{\psi}(x_1) P_L \cdot P_L \psi(x_2) \rangle$，都涉及到在旋量空间中对传播子 $S_F(x_2-x_1)$ 和[手性投影算符](@entry_id:181205) $P_L, P_R$ 的乘积求迹 (Trace)。这揭示了[威克定理](@entry_id:137086)如何与场的内部对称性（如手性）相结合，最终的计算结果会受到这些对称性的强烈约束。例如，在有质量的理论中，手性混合项 $m\bar{\psi}\psi = m(\bar{\psi}_R\psi_L + \bar{\psi}_L\psi_R)$ 意味着只有混合手性的收缩才与质量 $m$ 成正比，而保持手性的收缩则与动量[微分](@entry_id:158718)算符相关。

### 高级应用与扩展

[威克定理](@entry_id:137086)的真正威力体现在它能够处理比自由场n点函数更复杂的情形。它是微扰[量子场论](@entry_id:138177)的计算引擎。

#### 在外源存在下的关联函数

考虑一个受到经典外源 $J(x)$ 影响的[标量场](@entry_id:151443)，其作用量为 $S[\phi, J] = S_0[\phi] + \int d^Dx J(x)\phi(x)$。这是一个仍然可以精确求解的高斯理论。通过完成配方，可以将场变量平移 $\phi(x) = \phi'(x) + \phi_{\text{cl}}(x)$，其中 $\phi_{\text{cl}}(x)$ 是满足经典[运动方程](@entry_id:170720) $(\Box+m^2)\phi_{\text{cl}}=J$ 的经典场解，而 $\phi'(x)$ 是量子涨落场。经典解由[传播子](@entry_id:139558)给出：$\phi_{\text{cl}}(x) = i \int d^Dy \Delta_F(x-y) J(y)$。

在此背景下，任何关联函数都可以分解为与经典场相关的部分和纯量子涨落的部分。例如，三点函数 $\langle T\{\phi(x_1)\phi(x_2)\phi(x_3)\}\rangle_J$ [@problem_id:449994] 的计算结果包含两类项：
1.  **连通项 (Connected parts)**：一个场被替换为经典解 $\phi_{\text{cl}}$，另外两个场通过传播子收缩。这会产生形如 $\phi_{\text{cl}}(x_1) \Delta_F(x_2-x_3)$ 的项（以及其[置换](@entry_id:136432)）。
2.  **非连通项 (Disconnected parts)**：所有三个场都被替换为经典解，产生 $\phi_{\text{cl}}(x_1)\phi_{\text{cl}}(x_2)\phi_{\text{cl}}(x_3)$。

这种分解是[量子场论](@entry_id:138177)中连通图和[非连通图](@entry_id:192455)概念的数学基础。物理上，[连通图](@entry_id:264785)描述了粒子之间不可分割的相互作用过程，而[非连通图](@entry_id:192455)则代表了多个独立过程的简单组合。

#### [复合算符](@entry_id:152160)与正规乘积

[威克定理](@entry_id:137086)同样适用于由基本场构成的**[复合算符](@entry_id:152160) (composite operators)**，如[标量密度](@entry_id:161438) $S(x) = \bar{\psi}(x)\psi(x)$ 或流 $J^\mu(x) = \bar{\psi}(x)\gamma^\mu\psi(x)$。计算[复合算符](@entry_id:152160)的关联函数时，我们首先将它们展开为基本场，然后应用[威克定理](@entry_id:137086)。

例如，计算 $\langle T\{S(z) J^\mu(0)\}\rangle$ [@problem_id:449983]，我们实际计算的是 $\langle T\{\bar{\psi}(z)\psi(z) \bar{\psi}(0)\gamma^\mu\psi(0)\}\rangle$。应用[费米子](@entry_id:146235)[威克定理](@entry_id:137086)，这会产生一个[收缩环](@entry_id:137366)，其表达式为 $- \text{Tr}[iS_F(z) \gamma^\mu iS_F(-z)]$。这个迹的计算结果可能为零，也可能不为零，这取决于所涉及的伽马矩阵的对称性。例如，对于自由[狄拉克场](@entry_id:156753)，这个特定的关联函数由于迹内的伽马矩阵个数为奇数而恒为零，这反映了理论的特定对称性。

在处理[复合算符](@entry_id:152160)时，**正规乘积 (normal ordering)** 的概念变得至关重要。正规乘积，记为 $:\mathcal{O}:$，旨在移除算符内部的自收缩（即真空“气泡”或“蝌蚪图”）。例如，对于[标量场](@entry_id:151443)，$: \phi^2(x) : \equiv \phi^2(x) - \langle \phi^2(x) \rangle$。这个定义减去了发散的[真空期望值](@entry_id:146340)，使得[复合算符](@entry_id:152160)具有良定义的物理意义。计算正规乘积算符的关联函数时，我们只考虑不同算符之间的场的收缩。例如，$\langle : \phi^2(x) : \, : \phi^2(y) : \rangle_c^{\text{conn}}$ 的计算表明，在应用[威克定理](@entry_id:137086)后，只有连接 $x$ 和 $y$ 的收缩被保留，最终结果为 $2(i\Delta_F(x-y))^2$ [@problem_id:449930]。

一个更高级的[复合算符](@entry_id:152160)是**顶点算符 (vertex operator)**，如在[二维共形场论](@entry_id:148817)中常见的 $:e^{i\alpha\phi(x)}:$ [@problem_id:449962]。这类算符的关联函数也可以通过[高斯积分](@entry_id:187139)的性质（本质上是[威克定理](@entry_id:137086)的推广）来计算，它们在弦论和凝聚态物理中描述了粒子的创生和湮灭。

#### 作为微扰论引擎的[威克定理](@entry_id:137086)

[威克定理](@entry_id:137086)最核心的应用是在处理**相互作用理论**时的[微扰展开](@entry_id:159275)。对于一个包含相互作用项 $S_{\text{int}}$（例如 $\frac{\lambda}{4!}\phi^4$）的理论，其[路径积分](@entry_id:156701)为：
$$
\langle \mathcal{O} \rangle = \frac{\int \mathcal{D}\phi \, \mathcal{O}[\phi] e^{-S_0[\phi]} e^{-S_{\text{int}}[\phi]}}{\int \mathcal{D}\phi \, e^{-S_0[\phi]} e^{-S_{\text{int}}[\phi]}}
$$
在微扰论中，我们将 $e^{-S_{\text{int}}}$ 按耦合常数（如 $\lambda$）的幂次展开：
$$
e^{-S_{\text{int}}} = 1 - S_{\text{int}} + \frac{1}{2!}S_{\text{int}}^2 - \dots
$$
然后，我们将这个级数代入路径积分。每一项都变成在**自由理论**（由 $S_0$ 定义）中计算一个包含多个[场算符](@entry_id:140269)[乘积的期望值](@entry_id:201037)。这正是[威克定理](@entry_id:137086)发挥作用的地方。

例如，要计算一个 $\phi^3$ 理论中标量场自能的一[圈图修正](@entry_id:150150) [@problem_id:449897]，我们需要计算传播子的[二阶修正](@entry_id:199233)。这涉及到在[路径积分](@entry_id:156701)中包含两个来自[微扰展开](@entry_id:159275)的相互作用顶点 $(\frac{g}{3!}\phi^3)^2$。因此，我们需要计算的项形如 $\langle T\{\phi(x)\phi(y) \int d^4z_1 \phi^3(z_1) \int d^4z_2 \phi^3(z_2)\}\rangle_0$。这个表达式中有8个[场算符](@entry_id:140269)，[威克定理](@entry_id:137086)告诉我们要将它们全部配对。这些配对的组合方式，在[费曼图](@entry_id:144373)语言中，精确地对应于连接点 $x$ 和 $y$ 的所有可能的一圈图。每一个图都对应于一个由传播子乘积构成的积分，[威克定理](@entry_id:137086)为我们提供了从[拉格朗日量](@entry_id:174593)直接写下这些[费曼规则](@entry_id:156797)的系统方法。

总之，[威克定理](@entry_id:137086)是一个强大而优雅的组合工具。它将自由[场论](@entry_id:155241)中复杂的n点关联函数的计算简化为基本二点函数（传播子）的组合问题。更重要的是，它构成了微扰[量子场论](@entry_id:138177)的基石，使得我们能够系统地计算由相互作用引起的量子修正，从而将理论预测与实验观测联系起来。