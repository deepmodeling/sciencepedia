## 引言
在构建强大[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的探索中，选择基本构建单元——[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)——至关重要。在众多候选者中，由两个相互作用电子的自旋构成的单重态-[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)（S-T）[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，因其[可扩展性](@keyword=scalability|lang=zh-CN|style=Feynman)和全电学控制的潜力而脱颖而出。但是，如何利用两个自旋之间精巧的相对[排列](@keyword=permutation|lang=zh-CN|style=Feynman)来稳健地存储和处理信息呢？本文旨在揭开[单重态-三重态量子比特](@keyword=singlet_triplet_qubit|lang=zh-CN|style=Feynman)的神秘面纱，探讨在固态[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)环境中创建可控、相干的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)所面临的挑战。

我们的旅程始于第一节**“原理与机制”**，在该节中，我们将深入探讨赋予该[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)生命的量子力学。我们将探索两个电子如何被囚禁在被称为双[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)的[人造原子](@keyword=artificial_atoms|lang=zh-CN|style=Feynman)中，它们的集体自旋态如何形成逻辑上的“0”和“1”，以及用于操控和读出这些信息的巧妙技术。随后，**“应用与跨学科联系”**一节将拓宽我们的视野。我们将看到为何这种[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)架构对[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)如此富有前景，其核心原理如何在化学和超[精密测量](@keyword=precision_measurement|lang=zh-CN|style=Feynman)领域产生共鸣，以及它如何持续演进。通过这次探索，您将对[单重态-三重态量子比特](@keyword=singlet_triplet_qubit|lang=zh-CN|style=Feynman)获得全面的理解，从其基本物理原理到其深远影响。

## 原理与机制

好了，让我们深入实践吧。我们已经了解了由两个电子构成[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的概念，但它究竟是如何*工作*的呢？你如何与它对话，告诉它做什么，然后听取它的回答？这正是真正物理学的起点，一个关于量子之舞、巧妙工程以及与宇宙中嘈杂干扰持续斗争的有趣故事。

### [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的家：在硅中锻造的“原子”

首先，我们需要为我们的电子建造一个家。想象一块完美光滑、超洁净的[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)晶圆。通过在表面上使用微小、精心设计的电极，我们可以在[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)内部施加电压，从而创建一个定制的电[势景观](@keyword=potential_landscape|lang=zh-CN|style=Feynman)。可以把它想象成塑造一个微型鸡蛋盒。我们可以创建两个相邻的微小电势“水坑”，它们小到每个刚好能容纳一个电子。这种结构被称为**双[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)**（DQD）。

这些不仅仅是普通的水坑。它们非常小，以至于电子的量子性质凸显出来。电子不再是位于中心的微小球体；它们的存在由一个[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)来描述，即一团概率云，具有离散的能级。从这个意义上说，每个量子点都像一个定制设计的[人造原子](@keyword=artificial_atoms|lang=zh-CN|style=Feynman)。我们有两个这样的原子并排存在，通过调节门上的电压，我们可以控制一切：水坑的深度、其中的电子数量，以及最重要的是，它们之间山丘的高度，这决定了两个电子“交谈”的难易程度。

### 双自旋的故事：单重态与[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)

现在，我们在每个[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)中放置一个电子。每个电子都拥有一个称为**自旋**的基本量子属性，其作用类似于一个微型条形磁铁。它可以指向“上”($\lvert \uparrow \rangle$) 或 “下”($\lvert \downarrow \rangle$)。对于两个电子，我们就有两个自旋。它们如何组合呢？

直观地，你可能会想到四种可能性：$\lvert \uparrow \uparrow \rangle$、$\lvert \uparrow \downarrow \rangle$、$\lvert \downarrow \uparrow \rangle$ 和 $\lvert \downarrow \downarrow \rangle$。但量子力学有一种更优雅、也更有趣的组织方式。自然界倾向于使用具有确定总自旋的态。这两个自旋组合形成一个包含四个状态的家族：

1.  一个**[自旋单重态](@keyword=spin_singlet_state|lang=zh-CN|style=Feynman)** $|S\rangle$，[总自旋](@keyword=total_spin|lang=zh-CN|style=Feynman)为零：
    $$ |S\rangle = \frac{1}{\sqrt{2}} (\lvert\uparrow\downarrow\rangle - \lvert\downarrow\uparrow\rangle) $$
2.  一个包含三个**自旋[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)** $|T\rangle$ 的家族，[总自旋](@keyword=total_spin|lang=zh-CN|style=Feynman)为一：
    $$ \begin{aligned} |T_+\rangle &= \lvert\uparrow\uparrow\rangle \\ |T_0\rangle &= \frac{1}{\sqrt{2}} (\lvert\uparrow\downarrow\rangle + \lvert\downarrow\uparrow\rangle) \\ |T_-\rangle &= \lvert\downarrow\downarrow\rangle \end{aligned} $$

注意单重态中的那个奇怪的负号。这不仅仅是一个数学上的怪癖，它具有深远的意义。它意味着单重态的[自旋态](@keyword=spin_states|lang=zh-CN|style=Feynman)是*反对称*的——如果你交换两个电子，态的符号会反转。而[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)都是*对称*的——交换电子不会改变态。

我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，即**[单重态-三重态量子比特](@keyword=singlet_triplet_qubit|lang=zh-CN|style=Feynman)**，仅使用这四个态中的两个来定义：单重态 $|S\rangle$ 和中心[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman) $|T_0\rangle$。它们是我们的逻辑零和一。为什么是这两个？一个关键原因是，它们沿任何选定轴（$\hat{z}$）的总[自旋投影](@keyword=spin_projection|lang=zh-CN|style=Feynman)都为零。这使得它们对均匀[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的涨落具有内在的抵抗力，因为这种涨落会对 $|T_+\rangle$ 和 $|T_-\rangle$ 产生不同的影响。

这些[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)态是深度量子的。它们是**最大纠缠**的。这是什么意思？如果两个电子处于 $|S\rangle$ 态，这并非指电子1是上自旋而电子2是下自旋，或者反之。而是两种可能性同时存在。如果你测量电子1的自旋并发现它是“上”，你立即知道电子2*必须*是“下”。然而，在你测量之前，每个独立电子的自旋是完全不确定的。事实上，如果你对其中一个电子的状态求[偏迹](@keyword=partial_trace|lang=zh-CN|style=Feynman)，剩下那个电子的状态是完全随机的——50/50 的上自旋和下自旋[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)，就好像你刚刚抛了一枚硬币 [@problem_id:2115076]。这种完美的关联性与个体随机性的结合，正是纠缠奇特而强大的本质。

### 控制的艺术 I：交换相互作用之舞

那么我们有了[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)态。如何操纵它们呢？我们需要一种方法使[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)从 $|S\rangle$ 演化到 $|T_0\rangle$ 再返回，或者改变它们之间的[相对相位](@keyword=relative_phase|lang=zh-CN|style=Feynman)。实现这一目标的主要工具是一种美妙的量子力学效应，称为**[交换相互作用](@keyword=exchange_interaction|lang=zh-CN|style=Feynman)**。

它的起源是[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)和电子间静电[库仑排斥](@keyword=coulomb_repulsion|lang=zh-CN|style=Feynman)之间奇妙的相互作用。总[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)是空间部分和自旋部分的乘积。

-   对于**单重态**，自旋部分是反对称的。为了使总[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)反对称，空间部分必须是*对称*的。这意味着平均而言，电子倾向于靠得更近。
-   对于**三重态**，自旋部分是对称的。因此，空间部分必须是*反对称*的。这意味着平均而言，电子倾向于保持更远的距离。

由于电子相互排斥，它们相距较远的构型（[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)）比相距较近的构型（[单重态](@keyword=singlet_state|lang=zh-CN|style=Feynman)）具有更低的[库仑能](@keyword=coulomb_energy|lang=zh-CN|style=Feynman)量。这个能量差就是**交换能**。我们写出一个有效的[相互作用哈密顿量](@keyword=interaction_hamiltonian|lang=zh-CN|style=Feynman)来描述这一点：$H_{\mathrm{ex}} = J \mathbf{S}_1 \cdot \mathbf{S}_2$。

态 $|S\rangle$ 和 $|T_0\rangle$ 是该哈密顿量的[本征态](@keyword=eigenstates|lang=zh-CN|style=Feynman)，但能量不同：
$$ E_S = -\frac{3}{4}J\hbar^2 \quad \text{and} \quad E_{T_0} = +\frac{1}{4}J\hbar^2 $$
我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)态之间的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)就是 $E_{T_0} - E_S = J\hbar^2$。我们仅通过改变控制两个[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)之间势垒的门电压就可以调节这个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的强度参数 $J$。降低势垒会增加[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的重叠，从而增加 $J$。

现在，奇迹发生了。像 $|\psi\rangle = \frac{1}{\sqrt{2}}(|S\rangle + |T_0\rangle)$（也就是我们熟悉的老朋友 $|\uparrow\downarrow\rangle$）这样的态是一个叠加态。当我们开启[交换相互作用](@keyword=exchange_interaction|lang=zh-CN|style=Feynman)时，$|S\rangle$ 和 $|T_0\rangle$ 分量会随着时间以不同的能量依赖相位 $e^{-iEt/\hbar}$ 进行演化。它们之间会累积一个相对相位 $\phi(t) = (E_{T_0} - E_S)t/\hbar = J\hbar t$。这正是在[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的[布洛赫球面](@keyword=bloch_sphere|lang=zh-CN|style=Feynman)上绕 z 轴的旋转！通过对[交换相互作用](@keyword=exchange_interaction|lang=zh-CN|style=Feynman) $J$ 进行特定时长的脉冲操作，我们可以实现任何[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的 z 轴旋转 [@problem_id:2125700]。

### 控制的艺术 II：驾驭[梯度场](@keyword=gradient_fields|lang=zh-CN|style=Feynman)

Z 轴旋转很棒，但还不够。为了能到达布洛赫球面上的任意一点，我们需要能够绕第二个不同的轴进行旋转。这是通过一个涉及[非均匀磁场](@keyword=non_uniform_magnetic_fields|lang=zh-CN|style=Feynman)的巧妙技巧实现的 [@problem_id:3011866]。

假设我们施加一个在两个量子点上不完全相同的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。我们可以设置一个**[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)梯度**，使得点1上的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)比点2上的略强（例如，$B_1 = B_0 + \Delta B_z/2$ 和 $B_2 = B_0 - \Delta B_z/2$）。此时，塞曼[相互作用哈密顿量](@keyword=interaction_hamiltonian|lang=zh-CN|style=Feynman)中会有一个与场强差成正比的项，作用于自旋的差值：
$$ H_Z \propto \Delta B_z (S_{1z} - S_{2z}) $$
这个算符是关键。让我们看看它如何作用于我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)态：
$$ (S_{1z} - S_{2z}) |S\rangle = \hbar |T_0\rangle $$
$$ (S_{1z} - S_{2z}) |T_0\rangle = \hbar |S\rangle $$
它将一个[单重态](@keyword=singlet_state|lang=zh-CN|style=Feynman)翻转成一个三重态，又将一个[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)翻转成一个单重态！在逻辑基 $\{|S\rangle, |T_0\rangle\}$ 中，这个算符是一个泡利 $\sigma_x$ 矩阵。因此，一个恒定的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)梯度会驱动绕[布洛赫球面](@keyword=bloch_sphere|lang=zh-CN|style=Feynman) x 轴的旋转。

这样，我们就成功了。通过用门电压脉冲化[交换相互作用](@keyword=exchange_interaction|lang=zh-CN|style=Feynman)（用于 $\sigma_z$ 旋转）并施加一个静态[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)梯度（用于 $\sigma_x$ 旋转），我们可以执行任意的[单量子比特门](@keyword=single_qubit_gates|lang=zh-CN|style=Feynman)操作。我们实现了**普适的单[量子比特控制](@keyword=qubit_control|lang=zh-CN|style=Feynman)** [@problem_id:3011866]。

### 间谍与密语：读取[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的思想

在完成计算之后，我们需要读取答案。[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)是处于 $|S\rangle$ 态还是 $|T_0\rangle$ 态？我们不能直接“看”到自旋。取而代之，我们使用一种精妙的方法，称为**自旋到[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)转换**。我们将不可测量的自旋信息转换为可测量的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)信号。对于 S-T [量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，最常用的方法是**[泡利自旋阻塞](@keyword=pauli_spin_blockade|lang=zh-CN|style=Feynman)**（PSB）[@problem_id:3012031]。

这个间谍活动是这样进行的。我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)处于(1,1)[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)构型——每个[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)中有一个电子。然后，我们对门电压施加脉冲，使电子在能量上有利于从一个点隧穿到另一个点，以达到(0,2)构型。

-   如果[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)处于**[单重态](@keyword=singlet_state|lang=zh-CN|style=Feynman)** $|S(1,1)\rangle$，这个跃迁是允许的。两个电子可以愉快地聚集在同一个点中，形成[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|S(0,2)\rangle$。一个电子发生隧穿，双量子点的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)构型发生改变。
-   如果[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)处于**三重态** $|T_0(1,1)\rangle$，情况就不同了。[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)禁止两个具有对称[自旋态](@keyword=spin_states|lang=zh-CN|style=Feynman)（如所有三重态）的电子占据同一个最低能量的空间轨道。向 $|S(0,2)\rangle$ 的跃迁因自旋守恒而被禁止。电子被“阻塞”了；它们无法移动。

因此我们有了一个清晰的映射：单重态 $\rightarrow$ [电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)隧穿，三重态 $\rightarrow$ [电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)阻塞。为了检测这一点，我们在双[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)旁边放置一个极其灵敏的静电计，如一个**[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)接触**（QPC）。QPC的[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)对局域静电环境极其敏感。当一个电子从一个点隧穿到另一个点时，QPC会“看到”[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的变化，其[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)也会随之改变。通过监测QPC，我们可以推断出是否发生了隧穿事件，从而得知我们[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的初始自旋态。

### 世界中不可避免的噪声：退相干与泄漏

在一个完美的世界里，我们的故事到此就结束了。但现实世界是一个混乱、嘈杂的地方。我们精巧的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)不断受到其环境的干扰，导致两种主要的错误：退相移和泄漏。

**[退相](@keyword=dephasing|lang=zh-CN|style=Feynman)移**是相位信息的丢失。主要的控制旋钮，即交换能，对静电势呈指数依赖。不幸的是，[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)中充满了处于“陷阱”位点的杂散[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，这些[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)会随机跳跃。这会产生一个波动的电场，即**[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)噪声**。这意味着我们的[交换相互作用](@keyword=exchange_interaction|lang=zh-CN|style=Feynman)强度实际上是一个有噪声的、波动的量：$J(t) = J_0 + \delta J(t)$。这导致我们 z 轴旋转的速度随机波动，从而模糊了我们叠加态的相位。这被称为纯[退相](@keyword=dephasing|lang=zh-CN|style=Feynman)移。我们可以用不同的方式对这种噪声建模，例如，认为它来自单个离散的涨落源（**[随机电报噪声](@keyword=random_telegraph_noise|lang=zh-CN|style=Feynman)**）[@problem_id:118314] 或来自一个完整的涨落源浴（**奥恩斯坦-乌伦贝克噪声**）[@problem_id:118286]。这两种贡献加在一起，都会降低我们[量子操作](@keyword=quantum_operations|lang=zh-CN|style=Feynman)的最终**保真度**，保真度是衡量我们的最终态与我们意图创造的理想态有多接近的指标 [@problem_id:106566]。

**泄漏**是指[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)从其计算子空间 $\{|S\rangle, |T_0\rangle\}$ “逃逸”到其他态，如 $|T_+\rangle$ 或 $|T_-\rangle$。造成这种“背叛”的主要是两种物理机制 [@problem_id:3011885]：

1.  **[超精细相互作用](@keyword=hyperfine_interactions|lang=zh-CN|style=Feynman)：** [电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)并非独自存在。它们被[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中成千上万的原子核自旋（例如，镓和砷的原子核）所包围。这些原子[核自旋](@keyword=nuclear_spin|lang=zh-CN|style=Feynman)会产生一个微小、波动且不均匀的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，称为奥弗豪泽场（Overhauser field）。这个场在两点间的差异中，垂直于我们主外加[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的分量可以直接混合 $|S\rangle$ 和 $|T_\pm\rangle$ 态，导致泄漏。同样是这个相互作用，也可能打破“完美”的[泡利阻塞](@keyword=pauli_blocking|lang=zh-CN|style=Feynman)，允许[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)缓慢隧穿，产生微小的泄[漏电流](@keyword=leakage_current|lang=zh-CN|style=Feynman)，从而干扰我们的读出 [@problem_id:716146]。

2.  **[自旋轨道](@keyword=spin_orbitals|lang=zh-CN|style=Feynman)耦合：** 根据[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)，移动的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)在电场中会感受到一个等效[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。当我们的电子在[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)内运动时，它们与[晶体电场](@keyword=crystal_electric_field|lang=zh-CN|style=Feynman)的相互作用就会产生这样的效应。这种**自旋轨道耦合**为自旋翻转提供了另一个通道，可能会将我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)态与泄漏[态混合](@keyword=state_mixing|lang=zh-CN|style=Feynman)起来。

最后，即使是我们的读出过程也不是完美的。在我们等待[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)传感器获得读数的期间，电子的自旋可能会自发翻转并弛豫到其[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（一个 $T_1$ 错误）。或者，经典传感器本身可能噪声太大或速度太慢，无法可靠地检测到[单电子隧穿](@keyword=single_electron_tunneling|lang=zh-CN|style=Feynman)事件 [@problem_id:3012031]。

理解、建模并对抗这些噪声源是构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的巨大挑战和前沿阵地。源于量子力学和固态物理基本规则的[单重态-三重态量子比特](@keyword=singlet_triplet_qubit|lang=zh-CN|style=Feynman)，提供了一个迷人的舞台，在这片舞台上，为争取[量子相干性](@keyword=quantum_coherence|lang=zh-CN|style=Feynman)的战斗每天都在上演。