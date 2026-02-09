## 引言
在量子电动力学（QED）的理论构建中，选择一个合适的规范是处理电磁场内在自由度的关键一步，这直接影响到理论的物理图像和计算的复杂度。在众多规范选择中，库仑规范（或称横向规范）以其独特的物理直观性而著称。它解决了如何在量子框架下清晰地区分静态电荷间的瞬时库仑力与动态电磁辐射（光子）的问题，弥合了经典直觉与量子场论形式体系之间的鸿沟。

本文将系统地引导读者深入理解这一强大的理论工具。在“原理与机制”一章中，我们将详细推导库仑规范下的哈密顿量，揭示其如何将相互作用分解为瞬时库仑势和横向场耦合，并探讨场的量子化过程。接下来的“应用与跨学科联系”一章将展示该理论在原子物理、量子化学及凝聚态物理等前沿领域的具体应用，从兰姆位移到超导现象，彰显其广泛的解释力。最后，“动手实践”部分提供了一系列计算练习，帮助读者将理论知识转化为解决实际问题的能力。

## 原理与机制

在量子电动力学（QED）的研究中，选择特定的规范是处理理论中内在自由度的关键步骤。库仑规范，也称为横向规范或辐射规范，因其能清晰地分离物理自由度而备受青睐。本章旨在深入阐述在库仑规范下进行QED正则量子化的核心原理与机制。与 manifestly covariant 的方法（如 Gupta-Bleuler 量子化）不同，库仑规范牺牲了表观上的洛伦兹协变性，但换来了物理图像的直观性：它将带电粒子间的相互作用明确地分解为瞬时、非局域的库仑相互作用和由横向光子传播的横向场相互作用。这种处理方式在量子光学和原子分子物理等领域中尤其有效，因为它直接对应于我们对静态电力和辐射的物理直觉。

### 正则形式与规范固定

我们从一个由 $N$ 个非相对论性带电粒子与电磁场相互作用的系统的经典拉格朗日量出发。系统的总拉格朗日量 $L$ 是粒子动能与场及相互作用部分的总和：
$$
L = \sum_{i=1}^N \frac{1}{2} m_i |\dot{\mathbf{r}}_i|^2 + \int d^3x \, \mathcal{L}_{\text{field+int}}
$$
其中场与相互作用的拉格朗日密度 $\mathcal{L}_{\text{field+int}}$ 为：
$$
\mathcal{L}_{\text{field+int}} = \frac{\epsilon_0}{2} \left( \mathbf{E}^2 - c^2 \mathbf{B}^2 \right) + \mathbf{j} \cdot \mathbf{A} - \rho \phi
$$
电场 $\mathbf{E}$ 和磁场 $\mathbf{B}$ 通过标量势 $\phi$ 和矢量势 $\mathbf{A}$ 定义：$\mathbf{E} = -\nabla\phi - \dot{\mathbf{A}}$，$\mathbf{B} = \nabla \times \mathbf{A}$。电荷密度 $\rho$ 和电流密度 $\mathbf{j}$ 由点粒子产生。

电磁势 $(\phi, \mathbf{A})$ 存在规范自由度，使得我们需要选择一个特定的规范来消除冗余。**库仑规范** (Coulomb gauge) 通过施加以下条件来实现这一点：
$$
\nabla \cdot \mathbf{A} = 0
$$
这个条件深刻地影响了场的动力学。在高斯定律 $\nabla \cdot \mathbf{E} = \rho / \epsilon_0$ 中代入 $\mathbf{E} = -\nabla\phi - \dot{\mathbf{A}}$，我们得到：
$$
-\nabla^2\phi - \nabla \cdot \dot{\mathbf{A}} = \rho / \epsilon_0
$$
由于 $\nabla \cdot \mathbf{A} = 0$，我们可以交换时间和空间导数的顺序，得到 $\nabla \cdot \dot{\mathbf{A}} = \frac{d}{dt}(\nabla \cdot \mathbf{A}) = 0$。因此，高斯定律简化为一个泊松方程：
$$
\nabla^2 \phi(\mathbf{x}, t) = -\frac{\rho(\mathbf{x}, t)}{\epsilon_0}
$$
这个方程的解是瞬时的，它将标量势 $\phi$ 在时刻 $t$ 完全由同一时刻 $t$ 的电荷分布 $\rho$ 决定：
$$
\phi(\mathbf{x}, t) = \int d^3\mathbf{z} \, \frac{\rho(\mathbf{z}, t)}{4\pi\epsilon_0|\mathbf{x}-\mathbf{z}|}
$$
这意味着在库仑规范中，**标量势 $\phi$ (或在相对论记法中的 $A_0$) 不再是一个独立的动力学自由度**。它被电荷分布“束缚”住了，成为物质场的一个非局域函数。这种非动力学特性体现为 $A_0$ 算符与旋量场 $\psi$ 之间的非平庸的等时对易关系 [@problem_id:717173]。具体来说，通过求解上述泊松方程并将 $\rho = e\psi^\dagger\psi$ 代入，可以推导出：
$$
[A_0(\mathbf{x}, t), \psi(\mathbf{y}, t)] = -\frac{e}{4\pi\epsilon_0|\mathbf{x}-\mathbf{y}|} \psi(\mathbf{y}, t)
$$
这个非零且非局域的对易子明确显示了 $A_0$ 作为依赖于物质场的算符的地位。

### 库仑规范哈密顿量

为了进行量子化，我们通过勒让德变换从拉格朗日量构造哈密顿量。这一过程将揭示库仑规范的核心物理图像 [@problem_id:717131]。

首先，我们确定正则动量。对于粒子，其正则动量 $\mathbf{p}_i$ 是：
$$
\mathbf{p}_i = \frac{\partial L}{\partial \dot{\mathbf{r}}_i} = m_i\dot{\mathbf{r}}_i + q_i\mathbf{A}(\mathbf{r}_i, t)
$$
由于规范条件 $\nabla \cdot \mathbf{A} = 0$，矢量势 $\mathbf{A}$ 完全是横向的，我们记为 $\mathbf{A}_T$。因此，$\mathbf{p}_i = m_i\dot{\mathbf{r}}_i + q_i\mathbf{A}_T(\mathbf{r}_i)$。

对于场，只有横向矢量势 $\mathbf{A}_T$ 是动力学变量。其共轭动量场 $\mathbf{\Pi}_T$ 为：
$$
\mathbf{\Pi}_T(\mathbf{x}) = \frac{\delta L}{\delta \dot{\mathbf{A}}_T(\mathbf{x})} = \epsilon_0 (-\nabla\phi - \dot{\mathbf{A}}_T) = -\epsilon_0 \mathbf{E}(\mathbf{x})
$$
一个关键的步骤是利用亥姆霍兹分解将任意矢量场（此处为 $\mathbf{E}$）分解为无旋的纵向部分 ($\mathbf{E}_L$) 和无散的横向部分 ($\mathbf{E}_T$)。我们有 $\mathbf{E}_L = -\nabla\phi$ 和 $\mathbf{E}_T = -\dot{\mathbf{A}}_T$。因此，共轭动量场就是横向电场（乘以 $-\epsilon_0$）：$\mathbf{\Pi}_T = -\epsilon_0 \mathbf{E}_T$。

现在，我们构造哈密顿量 $H = \sum_i \mathbf{p}_i \cdot \dot{\mathbf{r}}_i + \int d^3x \, \mathbf{\Pi}_T \cdot \dot{\mathbf{A}}_T - L$。经过一系列代数运算，并将场的能量 $\frac{\epsilon_0}{2}\int d^3x \, \mathbf{E}^2$ 分解为纵向和横向部分 $\frac{\epsilon_0}{2}\int (\mathbf{E}_L^2 + \mathbf{E}_T^2) d^3x$，我们会发现纵向电场的能量项可以被精确地改写为所有电荷对之间的瞬时库仑势能：
$$
U_C = \frac{\epsilon_0}{2} \int d^3x \, \mathbf{E}_L^2 = \frac{1}{2} \int d^3x \, \rho(\mathbf{x}) \phi(\mathbf{x}) = \frac{1}{8\pi\epsilon_0} \sum_{i \neq j} \frac{q_i q_j}{|\mathbf{r}_i - \mathbf{r}_j|}
$$
这里我们忽略了点电荷的无限自能项（$i=j$ 的情况）。

最终，系统的总哈密顿量呈现出三个物理意义清晰的部分 [@problem_id:717131]：
$$
H = \sum_{i=1}^N \frac{1}{2m_i} \left( \mathbf{p}_i - q_i\mathbf{A}_T(\mathbf{r}_i) \right)^2 + \frac{1}{8\pi\epsilon_0} \sum_{i \neq j} \frac{q_i q_j}{|\mathbf{r}_i - \mathbf{r}_j|} + \int d^3x \left[ \frac{\mathbf{\Pi}_T^2}{2\epsilon_0} + \frac{\epsilon_0 c^2}{2} (\nabla \times \mathbf{A}_T)^2 \right]
$$
这三个部分分别是：
1.  **物质与横向场的相互作用**：第一项代表了粒子的动能以及它们通过最小耦合（minimal coupling）与**横向矢量势** $\mathbf{A}_T$ 的相互作用。
2.  **瞬时库仑相互作用**：第二项是粒子间瞬时、非延迟的库仑势能。这是从纵向电场中产生的，是库仑规范最显著的特征。
3.  **自由横向辐射场**：第三项是自由电磁场的哈密顿量，但它只包含横向分量。$\frac{\mathbf{\Pi}_T^2}{2\epsilon_0} = \frac{\epsilon_0 \mathbf{E}_T^2}{2}$ 是横向电场的能量，$\frac{\epsilon_0 c^2}{2}(\nabla \times \mathbf{A}_T)^2 = \frac{1}{2\mu_0}\mathbf{B}^2$ 是磁场的能量。

这个哈密顿量完美地体现了库仑规范的物理图像：静电相互作用被瞬时处理，而所有与辐射和延迟效应相关的动力学都包含在横向场中。

### 横向场的量子化

哈密顿量的第三部分描述了一个自由的横向电磁场。它的量子化过程是QED的核心内容之一。我们将横向矢量势 $\mathbf{A}_T$ 和其共轭动量 $\mathbf{\Pi}_T$ 展开为一系列独立的谐振子模式。对于每一个波矢 $\mathbf{k}$，存在两个相互正交的**横向极化矢量** $\boldsymbol{\epsilon}_{\lambda}(\mathbf{k})$（$\lambda=1,2$），它们满足 $\mathbf{k} \cdot \boldsymbol{\epsilon}_{\lambda}(\mathbf{k}) = 0$。

场的算符可以展开为光子的产生 ($a_{\mathbf{k}, \lambda}^\dagger$) 和湮灭 ($a_{\mathbf{k}, \lambda}$) 算符：
$$
\mathbf{A}_T(\mathbf{r}) = \sum_{\mathbf{k},\lambda} \sqrt{\frac{\hbar}{2\epsilon_0 V \omega_k}} \left( \boldsymbol{\epsilon}_{\mathbf{k},\lambda} a_{\mathbf{k},\lambda} e^{i\mathbf{k}\cdot\mathbf{r}} + \boldsymbol{\epsilon}_{\mathbf{k},\lambda}^* a_{\mathbf{k},\lambda}^\dagger e^{-i\mathbf{k}\cdot\mathbf{r}} \right)
$$
其中 $\omega_k = c|\mathbf{k}|$ 是模式的角频率，$V$ 是量子化体积。这些算符满足玻色子对易关系：$[a_{\mathbf{k}, \lambda}, a_{\mathbf{k}', \lambda'}^\dagger] = \delta_{\mathbf{k}\mathbf{k}'}\delta_{\lambda\lambda'}$。

将此展开代入自由辐射场哈密顿量，它就变成了对所有模式的谐振子哈密顿量的求和：
$$
H_{rad} = \sum_{\mathbf{k}, \lambda} \hbar \omega_{\mathbf{k}} \left( a_{\mathbf{k}, \lambda}^\dagger a_{\mathbf{k}, \lambda} + \frac{1}{2} \right)
$$
这一形式表明，自由横向电磁场被量子化为一组无穷多的谐振子，每个谐振子对应一个特定动量和极化的**光子**。

量子场的态由福克空间 (Fock space) 描述。真空态 $|0\rangle$ 是没有任何光子的态，满足 $a_{\mathbf{k}, \lambda}|0\rangle = 0$。通过在真空上作用产生算符，我们可以构建多光子态。例如，一个具有确定波矢 $\mathbf{k}_0$ 和极化 $\lambda_0$ 的单光子态是 $| \psi_{\mathbf{k}_0, \lambda_0} \rangle = a_{\mathbf{k}_0, \lambda_0}^\dagger |0\rangle$。

这个单光子态是 $H_{rad}$ 的本征态。它的能量可以通过计算它与真空态的能量差 $\Delta E$ 来确定 [@problem_id:717275]。真空态的能量是所有模式的零点能之和，$E_{vac} = \sum_{\mathbf{k}, \lambda} \frac{1}{2} \hbar \omega_{\mathbf{k}}$。而单光子态的能量为 $E_{\psi} = \hbar \omega_{\mathbf{k}_0} + E_{vac}$。因此，一个光子的能量（相对于真空）是：
$$
\Delta E = E_{\psi} - E_{vac} = \hbar \omega_{\mathbf{k}_0} = \hbar c |\mathbf{k}_0|
$$
这证实了普朗克-爱因斯坦关系，并将光子确立为携带一份能量 $\hbar \omega$ 和动量 $\hbar \mathbf{k}$ 的场的量子。

### 希尔伯特空间与物理态条件

在库仑规范中，希尔伯特空间只包含物质场和**横向光子**的态。纵向光子和标量光子并不作为独立的自由度出现。这一点可以通过构造一个形式上的“纵向光子态”并证明其模方为零来严格说明 [@problem_id:717123]。如果我们用矢量势算符的纵向分量作用于真空，即 $|\Psi_L(\mathbf{q})\rangle = (\hat{\mathbf{q}} \cdot \mathbf{A}^{(-)}(\mathbf{q})) |0\rangle$，其中 $\mathbf{A}^{(-)}$ 是 $\mathbf{A}_T$ 的产生算符部分，我们会发现 $\langle \Psi_L | \Psi_L \rangle = 0$。这是因为极化矢量求和的完备性关系 $\sum_{\lambda=1,2} (\mathbf{e}_{\mathbf{q},\lambda})_i (\mathbf{e}_{\mathbf{q},\lambda})_j = \delta_{ij} - \hat{q}_i \hat{q}_j$ 导致了 $\sum_{\lambda} |\hat{\mathbf{q}} \cdot \mathbf{e}_{\mathbf{q},\lambda}|^2 = 0$。一个模为零的态在希尔伯特空间中等同于零矢量，因此它不代表任何物理粒子。

尽管我们已经通过哈密顿量的形式消除了非动力学自由度，但在更形式的正则量子化框架中，高斯定律作为一个约束条件仍然扮演着重要角色。在量子理论中，它要求物理态 $|\Psi_{phys}\rangle$ 必须满足约束算符的湮灭条件。在没有源的情况下，一个较弱的条件（类似于 Gupta-Bleuler 条件）是物理态必须被电场散度的正频部分湮灭：
$$
\nabla \cdot \hat{\mathbf{E}}^{+}(\mathbf{x}) |\Psi_{phys}\rangle = 0
$$
幸运的是，在库仑规范中，这个条件是自动满足的。横向电场算符 $\hat{\mathbf{E}}_T$ 的展开式只包含横向极化矢量 $\boldsymbol{\epsilon}_{\lambda}(\mathbf{k})$。由于 $\mathbf{k} \cdot \boldsymbol{\epsilon}_{\lambda}(\mathbf{k}) = 0$，当我们计算电场散度时，每一项都会包含一个因子 $\mathbf{k} \cdot \boldsymbol{\epsilon}_{\lambda}(\mathbf{k})$，从而导致整个表达式恒等于零 [@problem_id:717100]。
$$
\nabla \cdot \hat{\mathbf{E}}^{+}(\mathbf{x}) = 0 \quad (\text{算符恒等式})
$$
这意味着在库仑规范的福克空间中构建的任何态（例如真空态、单光子态、多光子态等）都自动是物理态。这大大简化了态空间的结构，是库仑规范的一个主要优点。

### 对称性与自洽性检验

一个有效的量子场论必须遵守基本的物理原理，如对称性和守恒律。

**电荷守恒**：总电荷算符 $Q = \int d^3x \, \rho(\mathbf{x})$ 是一个守恒量，这意味着它必须与总哈密顿量 $H$ 对易。通过逐项检查 $Q$ 与 $H$ 的各个部分的对易子，可以验证 $[Q, H] = 0$ [@problem_id:717209]。$H_{matter}$ 和 $H_{Coulomb}$ 的构造都涉及到电荷密度的 bilinear 形式 $\psi^\dagger\psi$，它们自然与总荷算符 $Q$ (费米子数算符) 对易。而 $H_{em}$ 和 $H_{transverse}$ 中的场算符与费米子场算符在等时是对易的。因此，整个哈密顿量保持电荷守恒。

**规范不变性与约束**：从更深刻的层面看，高斯定律 $G(\mathbf{x}) = \nabla \cdot \mathbf{\Pi}(\mathbf{x}) - \rho(\mathbf{x}) \approx 0$ 是一个一级约束，它生成了不随时间变化的规范变换 [@problem_id:717246]。为了理论的自洽性，物理态子空间必须在时间演化下保持稳定，这意味着约束本身必须是守恒的。也就是说，$[G(\mathbf{x}), H_C]$ 在作用于物理态时必须为零，其中 $H_C$ 是引入辅助场之前的正则哈密顿量。事实上，可以证明 $[G(\mathbf{x}), H_C]=0$ 在整个希尔伯特空间上都成立。这个对易关系源于一个精妙的抵消。具体而言，对易子 $[ \nabla \cdot \mathbf{\Pi}(\mathbf{x}), H_C]$ 的计算结果是 $i\hbar \nabla \cdot \mathbf{j}(\mathbf{x})$ [@problem_id:717144]。因此，为了使总的对易子为零，我们必须有：
$$
[\rho(\mathbf{x}), H_C] + i\hbar \nabla \cdot \mathbf{j}(\mathbf{x}) = 0
$$
这正是量子化的电荷连续性方程 $\dot{\rho} + \nabla \cdot \mathbf{j} = 0$ 的算符形式。这表明，高斯定律的守恒性与电荷守恒这一基本物理定律是内在统一的。

**洛伦兹协变性**：库仑规范最受诟病的一点是它破坏了表观的洛伦兹协变性。瞬时库仑相互作用项显然不是协变的。然而，这只是理论表象的问题。完整的QED理论是洛伦兹协变的，这意味着物理的可观测量（如散射截面）的计算结果与参考系无关。这可以通过验证庞加莱代数的生成元满足正确的对易关系来证明。例如，两个 boost 生成元 $K_i$ 和 $K_j$ 的对易子应该与角动量生成元 $J_k$ 相关。尽管在库仑规范中 $K_i = \int d^3x \, x_i T^{00}(\mathbf{x})$ 因包含非局域的库仑能量密度而变得极其复杂，但经过繁复的计算，仍然可以证明它们满足正确的洛伦兹代数关系，例如 $[K_i, K_j] = -i\epsilon_{ijk} J_k$ [@problem_id:717222]。这确保了尽管表述方式不协变，理论的物理内涵仍然是与狭义相对论完全相容的。我们也可以从路径积分的角度来理解，通过积分掉非动力学的 $A_0$ 场，可以得到一个只包含物质场和横向规范场的有效作用量，这个过程虽然不透明地保持洛伦兹对称性，但最终的S矩阵元与协变规范下的结果是一致的 [@problem_id:717137]。

综上所述，库仑规范下的QED提供了一个物理上非常直观的量子化方案。它以清晰的方式隔离出系统的动力学自由度（物质粒子和横向光子），并将静电相互作用作为瞬时力来处理。尽管它在处理相对论性问题时显得较为笨拙，但其清晰的物理图像和简洁的希尔伯特空间结构使其在许多应用中成为不可或缺的强大工具。