## 引言
在量子电动力学（QED）的理论构建中，选择一个合适的规范是处理[电磁场](@entry_id:265881)内在自由度的关键一步，这直接影响到理论的物理图像和计算的复杂度。在众多规范选择中，[库仑规范](@entry_id:273044)（或称横向规范）以其独特的物理直观性而著称。它解决了如何在量子框架下清晰地区分静态[电荷](@entry_id:275494)间的瞬时库仑力与动态[电磁辐射](@entry_id:152916)（[光子](@entry_id:145192)）的问题，弥合了经典直觉与[量子场论](@entry_id:138177)形式体系之间的鸿沟。

本文将系统地引导读者深入理解这一强大的理论工具。在“原理与机制”一章中，我们将详细推导[库仑规范](@entry_id:273044)下的[哈密顿量](@entry_id:172864)，揭示其如何将相互作用分解为瞬时[库仑势](@entry_id:154276)和[横向场](@entry_id:266489)耦合，并探讨场的量子化过程。接下来的“应用与跨学科联系”一章将展示该理论在原子物理、[量子化学](@entry_id:140193)及凝聚态物理等前沿领域的具体应用，从[兰姆位移](@entry_id:148944)到[超导现象](@entry_id:142943)，彰显其广泛的解释力。最后，“动手实践”部分提供了一系列计算练习，帮助读者将理论知识转化为解决实际问题的能力。

## 原理与机制

在量子电动力学（QED）的研究中，选择特定的规范是处理理论中内在自由度的关键步骤。[库仑规范](@entry_id:273044)，也称为横向规范或辐射规范，因其能清晰地分离物理自由度而备受青睐。本章旨在深入阐述在[库仑规范](@entry_id:273044)下进行QED[正则量子化](@entry_id:148501)的核心原理与机制。与 manifestly covariant 的方法（如 Gupta-Bleuler 量子化）不同，[库仑规范](@entry_id:273044)牺牲了表观上的[洛伦兹协变性](@entry_id:161987)，但换来了物理图像的直观性：它将[带电粒子](@entry_id:160311)间的相互作用明确地分解为瞬时、非局域的[库仑相互作用](@entry_id:747947)和由[横向光子](@entry_id:197405)传播的[横向场](@entry_id:266489)相互作用。这种处理方式在量子光学和原子分子物理等领域中尤其有效，因为它直接对应于我们对静态[电力](@entry_id:262356)和辐射的物理直觉。

### 正则形式与[规范固定](@entry_id:142821)

我们从一个由 $N$ 个非相对论性[带电粒子](@entry_id:160311)与[电磁场](@entry_id:265881)相互作用的系统的经典[拉格朗日量](@entry_id:174593)出发。系统的[总拉格朗日量](@entry_id:756063) $L$ 是粒子动能与场及相互作用部分的总和：
$$
L = \sum_{i=1}^N \frac{1}{2} m_i |\dot{\mathbf{r}}_i|^2 + \int d^3x \, \mathcal{L}_{\text{field+int}}
$$
其中场与相互作用的拉格朗日密度 $\mathcal{L}_{\text{field+int}}$ 为：
$$
\mathcal{L}_{\text{field+int}} = \frac{\epsilon_0}{2} \left( \mathbf{E}^2 - c^2 \mathbf{B}^2 \right) + \mathbf{j} \cdot \mathbf{A} - \rho \phi
$$
[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$ 通过标量势 $\phi$ 和矢量势 $\mathbf{A}$ 定义：$\mathbf{E} = -\nabla\phi - \dot{\mathbf{A}}$，$\mathbf{B} = \nabla \times \mathbf{A}$。[电荷密度](@entry_id:144672) $\rho$ 和[电流密度](@entry_id:190690) $\mathbf{j}$ 由点[粒子产生](@entry_id:158755)。

[电磁势](@entry_id:266145) $(\phi, \mathbf{A})$ 存在[规范自由度](@entry_id:160491)，使得我们需要选择一个特定的规范来消除冗余。**[库仑规范](@entry_id:273044)** (Coulomb gauge) 通过施加以下条件来实现这一点：
$$
\nabla \cdot \mathbf{A} = 0
$$
这个条件深刻地影响了场的动力学。在高斯定律 $\nabla \cdot \mathbf{E} = \rho / \epsilon_0$ 中代入 $\mathbf{E} = -\nabla\phi - \dot{\mathbf{A}}$，我们得到：
$$
-\nabla^2\phi - \nabla \cdot \dot{\mathbf{A}} = \rho / \epsilon_0
$$
由于 $\nabla \cdot \mathbf{A} = 0$，我们可以交换时间和空间导数的顺序，得到 $\nabla \cdot \dot{\mathbf{A}} = \frac{d}{dt}(\nabla \cdot \mathbf{A}) = 0$。因此，[高斯定律](@entry_id:141493)简化为一个[泊松方程](@entry_id:143763)：
$$
\nabla^2 \phi(\mathbf{x}, t) = -\frac{\rho(\mathbf{x}, t)}{\epsilon_0}
$$
这个方程的解是瞬时的，它将标量势 $\phi$ 在时刻 $t$ 完全由同一时刻 $t$ 的电荷分布 $\rho$ 决定：
$$
\phi(\mathbf{x}, t) = \int d^3\mathbf{z} \, \frac{\rho(\mathbf{z}, t)}{4\pi\epsilon_0|\mathbf{x}-\mathbf{z}|}
$$
这意味着在[库仑规范](@entry_id:273044)中，**标量势 $\phi$ (或在相对论记法中的 $A_0$) 不再是一个独立的动力学自由度**。它被[电荷分布](@entry_id:144400)“束缚”住了，成为物质场的一个非局域函数。这种非动力学特性体现为 $A_0$ 算符与旋量场 $\psi$ 之间的非平庸的等时对易关系 [@problem_id:717173]。具体来说，通过求解上述泊松方程并将 $\rho = e\psi^\dagger\psi$ 代入，可以推导出：
$$
[A_0(\mathbf{x}, t), \psi(\mathbf{y}, t)] = -\frac{e}{4\pi\epsilon_0|\mathbf{x}-\mathbf{y}|} \psi(\mathbf{y}, t)
$$
这个非零且非局域的对易子明确显示了 $A_0$ 作为依赖于物质场的算符的地位。

### [库仑规范](@entry_id:273044)[哈密顿量](@entry_id:172864)

为了进行量子化，我们通过勒让德变换从[拉格朗日量](@entry_id:174593)构造[哈密顿量](@entry_id:172864)。这一过程将揭示[库仑规范](@entry_id:273044)的核心物理图像 [@problem_id:717131]。

首先，我们确定[正则动量](@entry_id:155151)。对于粒子，其[正则动量](@entry_id:155151) $\mathbf{p}_i$ 是：
$$
\mathbf{p}_i = \frac{\partial L}{\partial \dot{\mathbf{r}}_i} = m_i\dot{\mathbf{r}}_i + q_i\mathbf{A}(\mathbf{r}_i, t)
$$
由于[规范条件](@entry_id:749730) $\nabla \cdot \mathbf{A} = 0$，矢量势 $\mathbf{A}$ 完全是横向的，我们记为 $\mathbf{A}_T$。因此，$\mathbf{p}_i = m_i\dot{\mathbf{r}}_i + q_i\mathbf{A}_T(\mathbf{r}_i)$。

对于场，只有横向矢量势 $\mathbf{A}_T$ 是动力学变量。其[共轭动量](@entry_id:172203)场 $\mathbf{\Pi}_T$ 为：
$$
\mathbf{\Pi}_T(\mathbf{x}) = \frac{\delta L}{\delta \dot{\mathbf{A}}_T(\mathbf{x})} = \epsilon_0 (-\nabla\phi - \dot{\mathbf{A}}_T) = -\epsilon_0 \mathbf{E}(\mathbf{x})
$$
一个关键的步骤是利用[亥姆霍兹分解](@entry_id:181767)将任意矢量场（此处为 $\mathbf{E}$）分解为无旋的纵向部分 ($\mathbf{E}_L$) 和无散的横向部分 ($\mathbf{E}_T$)。我们有 $\mathbf{E}_L = -\nabla\phi$ 和 $\mathbf{E}_T = -\dot{\mathbf{A}}_T$。因此，[共轭动量](@entry_id:172203)场就是横向[电场](@entry_id:194326)（乘以 $-\epsilon_0$）：$\mathbf{\Pi}_T = -\epsilon_0 \mathbf{E}_T$。

现在，我们构造[哈密顿量](@entry_id:172864) $H = \sum_i \mathbf{p}_i \cdot \dot{\mathbf{r}}_i + \int d^3x \, \mathbf{\Pi}_T \cdot \dot{\mathbf{A}}_T - L$。经过一系列代数运算，并将场的能量 $\frac{\epsilon_0}{2}\int d^3x \, \mathbf{E}^2$ 分解为纵向和横向部分 $\frac{\epsilon_0}{2}\int (\mathbf{E}_L^2 + \mathbf{E}_T^2) d^3x$，我们会发现纵向[电场](@entry_id:194326)的能量项可以被精确地改写为所有[电荷](@entry_id:275494)对之间的瞬时[库仑势能](@entry_id:263842)：
$$
U_C = \frac{\epsilon_0}{2} \int d^3x \, \mathbf{E}_L^2 = \frac{1}{2} \int d^3x \, \rho(\mathbf{x}) \phi(\mathbf{x}) = \frac{1}{8\pi\epsilon_0} \sum_{i \neq j} \frac{q_i q_j}{|\mathbf{r}_i - \mathbf{r}_j|}
$$
这里我们忽略了点电荷的无限[自能](@entry_id:145608)项（$i=j$ 的情况）。

最终，系统的总[哈密顿量](@entry_id:172864)呈现出三个物理意义清晰的部分 [@problem_id:717131]：
$$
H = \sum_{i=1}^N \frac{1}{2m_i} \left( \mathbf{p}_i - q_i\mathbf{A}_T(\mathbf{r}_i) \right)^2 + \frac{1}{8\pi\epsilon_0} \sum_{i \neq j} \frac{q_i q_j}{|\mathbf{r}_i - \mathbf{r}_j|} + \int d^3x \left[ \frac{\mathbf{\Pi}_T^2}{2\epsilon_0} + \frac{\epsilon_0 c^2}{2} (\nabla \times \mathbf{A}_T)^2 \right]
$$
这三个部分分别是：
1.  **物质与[横向场](@entry_id:266489)的相互作用**：第一项代表了粒子的动能以及它们通过[最小耦合](@entry_id:148226)（minimal coupling）与**横向矢量势** $\mathbf{A}_T$ 的相互作用。
2.  **[瞬时库仑相互作用](@entry_id:196309)**：第二项是粒子间瞬时、非延迟的[库仑势能](@entry_id:263842)。这是从纵向[电场](@entry_id:194326)中产生的，是[库仑规范](@entry_id:273044)最显著的特征。
3.  **自由横向辐射场**：第三项是[自由电磁场的哈密顿量](@entry_id:182976)，但它只包含横向分量。$\frac{\mathbf{\Pi}_T^2}{2\epsilon_0} = \frac{\epsilon_0 \mathbf{E}_T^2}{2}$ 是横向[电场](@entry_id:194326)的能量，$\frac{\epsilon_0 c^2}{2}(\nabla \times \mathbf{A}_T)^2 = \frac{1}{2\mu_0}\mathbf{B}^2$ 是[磁场](@entry_id:153296)的能量。

这个[哈密顿量](@entry_id:172864)完美地体现了[库仑规范](@entry_id:273044)的物理图像：[静电相互作用](@entry_id:166363)被瞬时处理，而所有与辐射和[延迟效应](@entry_id:199612)相关的动力学都包含在[横向场](@entry_id:266489)中。

### [横向场](@entry_id:266489)的量子化

[哈密顿量](@entry_id:172864)的第三部分描述了一个自由的横向[电磁场](@entry_id:265881)。它的量子化过程是QED的核心内容之一。我们将横向矢量势 $\mathbf{A}_T$ 和其[共轭动量](@entry_id:172203) $\mathbf{\Pi}_T$ 展开为一系列独立的[谐振子](@entry_id:155622)模式。对于每一个波矢 $\mathbf{k}$，存在两个相互正交的**横向[极化矢量](@entry_id:269389)** $\boldsymbol{\epsilon}_{\lambda}(\mathbf{k})$（$\lambda=1,2$），它们满足 $\mathbf{k} \cdot \boldsymbol{\epsilon}_{\lambda}(\mathbf{k}) = 0$。

场的算符可以展开为[光子](@entry_id:145192)的产生 ($a_{\mathbf{k}, \lambda}^\dagger$) 和湮灭 ($a_{\mathbf{k}, \lambda}$) 算符：
$$
\mathbf{A}_T(\mathbf{r}) = \sum_{\mathbf{k},\lambda} \sqrt{\frac{\hbar}{2\epsilon_0 V \omega_k}} \left( \boldsymbol{\epsilon}_{\mathbf{k},\lambda} a_{\mathbf{k},\lambda} e^{i\mathbf{k}\cdot\mathbf{r}} + \boldsymbol{\epsilon}_{\mathbf{k},\lambda}^* a_{\mathbf{k},\lambda}^\dagger e^{-i\mathbf{k}\cdot\mathbf{r}} \right)
$$
其中 $\omega_k = c|\mathbf{k}|$ 是模式的[角频率](@entry_id:261565)，$V$ 是量子化体积。这些算符满足[玻色子](@entry_id:138266)[对易关系](@entry_id:136780)：$[a_{\mathbf{k}, \lambda}, a_{\mathbf{k}', \lambda'}^\dagger] = \delta_{\mathbf{k}\mathbf{k}'}\delta_{\lambda\lambda'}$。

将此展开代入自由[辐射场](@entry_id:164265)[哈密顿量](@entry_id:172864)，它就变成了对所有模式的[谐振子](@entry_id:155622)[哈密顿量](@entry_id:172864)的求和：
$$
H_{rad} = \sum_{\mathbf{k}, \lambda} \hbar \omega_{\mathbf{k}} \left( a_{\mathbf{k}, \lambda}^\dagger a_{\mathbf{k}, \lambda} + \frac{1}{2} \right)
$$
这一形式表明，自由横向[电磁场](@entry_id:265881)被量子化为一组无穷多的[谐振子](@entry_id:155622)，每个谐振子对应一个特定动量和极化的**[光子](@entry_id:145192)**。

量子场的态由[福克空间](@entry_id:143624) (Fock space) 描述。真空态 $|0\rangle$ 是没有任何[光子](@entry_id:145192)的态，满足 $a_{\mathbf{k}, \lambda}|0\rangle = 0$。通过在真空上作用[产生算符](@entry_id:191512)，我们可以构建多[光子](@entry_id:145192)态。例如，一个具有确定[波矢](@entry_id:178620) $\mathbf{k}_0$ 和极化 $\lambda_0$ 的单[光子](@entry_id:145192)态是 $| \psi_{\mathbf{k}_0, \lambda_0} \rangle = a_{\mathbf{k}_0, \lambda_0}^\dagger |0\rangle$。

这个单[光子](@entry_id:145192)态是 $H_{rad}$ 的本征态。它的能量可以通过计算它与真空态的能量差 $\Delta E$ 来确定 [@problem_id:717275]。真空态的能量是所有模式的[零点能](@entry_id:142176)之和，$E_{vac} = \sum_{\mathbf{k}, \lambda} \frac{1}{2} \hbar \omega_{\mathbf{k}}$。而单[光子](@entry_id:145192)态的能量为 $E_{\psi} = \hbar \omega_{\mathbf{k}_0} + E_{vac}$。因此，一个[光子](@entry_id:145192)的能量（相对于真空）是：
$$
\Delta E = E_{\psi} - E_{vac} = \hbar \omega_{\mathbf{k}_0} = \hbar c |\mathbf{k}_0|
$$
这证实了[普朗克-爱因斯坦关系](@entry_id:147416)，并将[光子](@entry_id:145192)确立为携带一份能量 $\hbar \omega$ 和动量 $\hbar \mathbf{k}$ 的场的量子。

### [希尔伯特空间](@entry_id:261193)与物理态条件

在[库仑规范](@entry_id:273044)中，[希尔伯特空间](@entry_id:261193)只包含物质场和**[横向光子](@entry_id:197405)**的态。纵向[光子](@entry_id:145192)和标量[光子](@entry_id:145192)并不作为独立的自由度出现。这一点可以通过构造一个形式上的“纵向[光子](@entry_id:145192)态”并证明其模方为零来严格说明 [@problem_id:717123]。如果我们用矢量势算符的纵向分量作用于真空，即 $|\Psi_L(\mathbf{q})\rangle = (\hat{\mathbf{q}} \cdot \mathbf{A}^{(-)}(\mathbf{q})) |0\rangle$，其中 $\mathbf{A}^{(-)}$ 是 $\mathbf{A}_T$ 的[产生算符](@entry_id:191512)部分，我们会发现 $\langle \Psi_L | \Psi_L \rangle = 0$。这是因为[极化矢量](@entry_id:269389)求和的[完备性关系](@entry_id:139077) $\sum_{\lambda=1,2} (\mathbf{e}_{\mathbf{q},\lambda})_i (\mathbf{e}_{\mathbf{q},\lambda})_j = \delta_{ij} - \hat{q}_i \hat{q}_j$ 导致了 $\sum_{\lambda} |\hat{\mathbf{q}} \cdot \mathbf{e}_{\mathbf{q},\lambda}|^2 = 0$。一个模为零的态在希尔伯特空间中等同于[零矢量](@entry_id:155273)，因此它不代表任何物理粒子。

尽管我们已经通过[哈密顿量](@entry_id:172864)的形式消除了非动力学自由度，但在更形式的[正则量子化](@entry_id:148501)框架中，高斯定律作为一个约束条件仍然扮演着重要角色。在[量子理论](@entry_id:145435)中，它要求物理态 $|\Psi_{phys}\rangle$ 必须满足约束算符的湮灭条件。在没有源的情况下，一个较弱的条件（类似于 Gupta-Bleuler 条件）是物理态必须被[电场散度](@entry_id:261010)的正频部分湮灭：
$$
\nabla \cdot \hat{\mathbf{E}}^{+}(\mathbf{x}) |\Psi_{phys}\rangle = 0
$$
幸运的是，在[库仑规范](@entry_id:273044)中，这个条件是自动满足的。横向[电场算符](@entry_id:196320) $\hat{\mathbf{E}}_T$ 的展开式只包含横向[极化矢量](@entry_id:269389) $\boldsymbol{\epsilon}_{\lambda}(\mathbf{k})$。由于 $\mathbf{k} \cdot \boldsymbol{\epsilon}_{\lambda}(\mathbf{k}) = 0$，当我们计算[电场散度](@entry_id:261010)时，每一项都会包含一个因子 $\mathbf{k} \cdot \boldsymbol{\epsilon}_{\lambda}(\mathbf{k})$，从而导致整个表达式恒等于零 [@problem_id:717100]。
$$
\nabla \cdot \hat{\mathbf{E}}^{+}(\mathbf{x}) = 0 \quad (\text{算符恒等式})
$$
这意味着在[库仑规范](@entry_id:273044)的[福克空间](@entry_id:143624)中构建的任何态（例如真空态、单[光子](@entry_id:145192)态、多[光子](@entry_id:145192)态等）都自动是物理态。这大大简化了态空间的结构，是[库仑规范](@entry_id:273044)的一个主要优点。

### 对称性与[自洽性](@entry_id:160889)检验

一个有效的[量子场论](@entry_id:138177)必须遵守基本的物理原理，如对称性和守恒律。

**电荷守恒**：总[电荷](@entry_id:275494)算符 $Q = \int d^3x \, \rho(\mathbf{x})$ 是一个[守恒量](@entry_id:150267)，这意味着它必须与总[哈密顿量](@entry_id:172864) $H$ 对易。通过逐项检查 $Q$ 与 $H$ 的各个部分的对易子，可以验证 $[Q, H] = 0$ [@problem_id:717209]。$H_{matter}$ 和 $H_{Coulomb}$ 的构造都涉及到电荷密度的 bilinear 形式 $\psi^\dagger\psi$，它们自然与总荷算符 $Q$ ([费米子](@entry_id:146235)数算符) 对易。而 $H_{em}$ 和 $H_{transverse}$ 中的[场算符](@entry_id:140269)与[费米子](@entry_id:146235)[场算符](@entry_id:140269)在等时是对易的。因此，整个[哈密顿量](@entry_id:172864)保持电荷守恒。

**[规范不变性](@entry_id:137857)与约束**：从更深刻的层面看，[高斯定律](@entry_id:141493) $G(\mathbf{x}) = \nabla \cdot \mathbf{\Pi}(\mathbf{x}) - \rho(\mathbf{x}) \approx 0$ 是一个一级约束，它生成了不随时间变化的[规范变换](@entry_id:176521) [@problem_id:717246]。为了理论的自洽性，物理态[子空间](@entry_id:150286)必须在时间演化下保持稳定，这意味着约束本身必须是守恒的。也就是说，$[G(\mathbf{x}), H_C]$ 在作用于物理态时必须为零，其中 $H_C$ 是引入[辅助场](@entry_id:155519)之前的正则[哈密顿量](@entry_id:172864)。事实上，可以证明 $[G(\mathbf{x}), H_C]=0$ 在整个希尔伯特空间上都成立。这个[对易关系](@entry_id:136780)源于一个精妙的抵消。具体而言，对易子 $[ \nabla \cdot \mathbf{\Pi}(\mathbf{x}), H_C]$ 的计算结果是 $i\hbar \nabla \cdot \mathbf{j}(\mathbf{x})$ [@problem_id:717144]。因此，为了使总的对易子为零，我们必须有：
$$
[\rho(\mathbf{x}), H_C] + i\hbar \nabla \cdot \mathbf{j}(\mathbf{x}) = 0
$$
这正是量子化的[电荷连续性](@entry_id:747292)方程 $\dot{\rho} + \nabla \cdot \mathbf{j} = 0$ 的算符形式。这表明，高斯定律的守恒性与[电荷守恒](@entry_id:264158)这一基本物理定律是内在统一的。

**[洛伦兹协变性](@entry_id:161987)**：[库仑规范](@entry_id:273044)最受诟病的一点是它破坏了表观的[洛伦兹协变性](@entry_id:161987)。[瞬时库仑相互作用](@entry_id:196309)项显然不是协变的。然而，这只是理论表象的问题。完整的QED理论是洛伦兹[协变](@entry_id:634097)的，这意味着物理的[可观测量](@entry_id:267133)（如散射截面）的计算结果与[参考系](@entry_id:169232)无关。这可以通过验证[庞加莱代数](@entry_id:161072)的生成元满足正确的[对易关系](@entry_id:136780)来证明。例如，两个 boost 生成元 $K_i$ 和 $K_j$ 的对易子应该与[角动量生成元](@entry_id:149542) $J_k$ 相关。尽管在[库仑规范](@entry_id:273044)中 $K_i = \int d^3x \, x_i T^{00}(\mathbf{x})$ 因包含非局域的[库仑能](@entry_id:161936)量密度而变得极其复杂，但经过繁复的计算，仍然可以证明它们满足正确的[洛伦兹代数](@entry_id:186411)关系，例如 $[K_i, K_j] = -i\epsilon_{ijk} J_k$ [@problem_id:717222]。这确保了尽管表述方式不协变，理论的物理内涵仍然是与狭义相对论完全相容的。我们也可以从路径积分的角度来理解，通[过积分](@entry_id:753033)掉非动力学的 $A_0$ 场，可以得到一个只包含物质场和横向规范场的[有效作用量](@entry_id:145780)，这个过程虽然不透明地保持洛伦兹对称性，但最终的[S矩阵](@entry_id:137017)元与协变规范下的结果是一致的 [@problem_id:717137]。

综上所述，[库仑规范](@entry_id:273044)下的QED提供了一个物理上非常直观的量子化方案。它以清晰的方式隔离出系统的动力学自由度（物[质粒](@entry_id:263777)子和[横向光子](@entry_id:197405)），并将[静电相互作用](@entry_id:166363)作为瞬时力来处理。尽管它在处理相对论性问题时显得较为笨拙，但其清晰的物理图像和简洁的[希尔伯特空间](@entry_id:261193)结构使其在许多应用中成为不可或缺的强大工具。