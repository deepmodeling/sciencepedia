## 引言
量子隐形传态是现代[量子信息科学](@entry_id:150091)中最具标志性和革命性的概念之一。它描绘了一幅看似科幻的图景：将一个粒子的[量子态](@entry_id:146142)——其完整的[量子信息](@entry_id:137721)——从一个地点瞬间传输到另一个地点，而无需物理上移动粒子本身。这一非凡过程的实现并非魔法，而是根植于量子力学的两个最深奥的特性：量子纠缠和量子测量。它不仅挑战了我们对信息和现实的经典直觉，也为[量子技术](@entry_id:142946)的未来发展铺平了道路。

然而，[量子态](@entry_id:146142)的脆弱性和[不可克隆定理](@entry_id:146200)构成了信息传输的根本障碍。我们如何能在不直接测量（从而破坏）一个未知[量子态](@entry_id:146142)的情况下，精确地在远处“重建”它？量子隐形传态协议正是为了解决这一核心难题而设计的。它巧妙地规避了直接复制的禁令，通过消耗预先共享的纠缠资源，将[量子信息](@entry_id:137721)“移动”而非“克隆”。

本文将系统地引导您深入量子隐形传态的世界。在“原理与机制”一章中，我们将详细拆解协议的每一步，揭示其背后的数学结构和物理原理，并探讨其对因果律和[不可克隆定理](@entry_id:146200)的遵从。接着，在“应用与跨学科连接”一章中，我们将视野拓宽，探索隐形传态如何成为构建[量子计算](@entry_id:142712)机、[量子互联网](@entry_id:143445)乃至连接凝聚态物理与宇宙学的强大桥梁。最后，“动手实践”部分将提供具体的计算问题，帮助您巩固对关键概念的理解。通过本次学习，您将领会到量子隐形传态为何不仅是一个精妙的协议，更是一个开启量子世界无限可能的关键钥匙。

## 原理与机制

量子隐形传态是[量子信息科学](@entry_id:150091)中的一项核心协议，它使得在不物理性地移动粒子本身的情况下，将一个[量子态](@entry_id:146142)从一个地点传输到另一个地点成为可能。这一过程依赖于量子力学的两个基本特征：量子纠缠和[量子测量](@entry_id:272490)。本章将深入探讨量子隐形传态的内在机制、基本原理，并探索其各种推广和应用。

### [量子比特](@entry_id:137928)隐形传态的核心机制

标准量子隐形传态协议旨在将一个任意的单[量子比特](@entry_id:137928)态 $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ 从发送方（通常称为 Alice）传输给接收方（Bob）。要实现这一点，需要三个关键要素：
1.  待传输的[量子比特](@entry_id:137928)，其状态为 $|\psi\rangle$。
2.  一个预先共享的量子通道，通常是一个处于最大[纠缠态](@entry_id:152310)（如贝尔态 $|\Phi^+\rangle$）的[量子比特](@entry_id:137928)对。
3.  一个经典通信通道，用于从 Alice 向 Bob 传输少量信息。

让我们将该协议分解为一系列精确的步骤。假设 Alice 拥有待传输的[量子比特](@entry_id:137928)（记为[量子比特](@entry_id:137928)1），以及[纠缠对](@entry_id:160576)中的一个[量子比特](@entry_id:137928)（记为[量子比特](@entry_id:137928)2）。Bob 则拥有纠缠对的另一个[量子比特](@entry_id:137928)（记为[量子比特](@entry_id:137928)3）。纠缠对处于贝尔态 $|\Phi^+\rangle_{23} = \frac{1}{\sqrt{2}}(|00\rangle_{23} + |11\rangle_{23})$。因此，整个[三量子比特](@entry_id:146257)系统的初始状态为：

$$
|\Psi_{\text{initial}}\rangle = |\psi\rangle_1 \otimes |\Phi^+\rangle_{23} = (\alpha|0\rangle_1 + \beta|1\rangle_1) \otimes \frac{1}{\sqrt{2}}(|00\rangle_{23} + |11\rangle_{23})
$$

展开后得到：

$$
|\Psi_{\text{initial}}\rangle = \frac{1}{\sqrt{2}}(\alpha|000\rangle_{123} + \alpha|011\rangle_{123} + \beta|100\rangle_{123} + \beta|111\rangle_{123})
$$

协议按以下步骤进行：

**第一步：Alice 的局域操作**

Alice 对她所拥有的两个[量子比特](@entry_id:137928)（1和2）执行一系列[量子门](@entry_id:143510)操作。首先，她施加一个**[受控非门](@entry_id:180955) (CNOT)**，其中[量子比特](@entry_id:137928)1为控制位，[量子比特](@entry_id:137928)2为目标位。CNOT 门的作用是，当控制位为 $|1\rangle$ 时，翻转目标位。作用在系统上，状态变为：

$$
|\Psi_{\text{after CNOT}}\rangle = \frac{1}{\sqrt{2}}(\alpha|000\rangle + \alpha|011\rangle + \beta|110\rangle + \beta|101\rangle)
$$

接着，Alice 对[量子比特](@entry_id:137928)1施加一个**哈达玛门 (Hadamard gate)**。哈达玛门将计算[基矢](@entry_id:199546)转换为叠加态：$H|0\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$ 和 $H|1\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$。施加此门后，系统的总状态演变为 [@problem_id:2113242]：

$$
|\Psi_{\text{final}}\rangle = \frac{1}{2} \big[ |00\rangle_{12}(\alpha|0\rangle_3 + \beta|1\rangle_3) + |01\rangle_{12}(\beta|0\rangle_3 + \alpha|1\rangle_3) + |10\rangle_{12}(\alpha|0\rangle_3 - \beta|1\rangle_3) + |11\rangle_{12}(\alpha|1\rangle_3 - \beta|0\rangle_3) \big]
$$

**第二步：贝尔基测量**

此时，Alice 对她的两个[量子比特](@entry_id:137928)（1和2）在计算基 $\lbrace|00\rangle, |01\rangle, |10\rangle, |11\rangle\rbrace$ 中进行测量。一个深刻的见解是，Alice 在第一步中施加的 CNOT 和哈达玛门序列，实际上构成了一个从贝尔基到计算基的变换。也就是说，如果将四个贝尔态 $|\Phi^\pm\rangle, |\Psi^\pm\rangle$ 输入这个电路，输出将分别是四个计算[基态](@entry_id:150928) $|00\rangle, |01\rangle, |10\rangle, |11\rangle$ [@problem_id:2113226]。因此，在 CNOT 和哈达玛门之后进行计算基测量，等效于直接对 Alice 的两个[量子比特](@entry_id:137928)进行**贝尔基测量**。

根据量子测量的投影假设，当 Alice 的测量得到四个可能结果（例如，“00”、“01”、“10”或“11”）之一时，整个系统的状态会坍缩到相应的项。重要的是，观察上式 $|\Psi_{\text{final}}\rangle$ 的结构：Alice 的每个测量结果都唯一地将 Bob 的[量子比特](@entry_id:137928)3投影到一个特定的状态。这四个可能的状态与原始状态 $|\psi\rangle$ 密切相关：

-   若 Alice 测得 $|00\rangle_{12}$，Bob 的[量子比特](@entry_id:137928)状态为 $(\alpha|0\rangle_3 + \beta|1\rangle_3) = I|\psi\rangle_3$。
-   若 Alice 测得 $|01\rangle_{12}$，Bob 的[量子比特](@entry_id:137928)状态为 $(\beta|0\rangle_3 + \alpha|1\rangle_3) = \sigma_x|\psi\rangle_3$。
-   若 Alice 测得 $|10\rangle_{12}$，Bob 的[量子比特](@entry_id:137928)状态为 $(\alpha|0\rangle_3 - \beta|1\rangle_3) = \sigma_z|\psi\rangle_3$。
-   若 Alice 测得 $|11\rangle_{12}$，Bob 的[量子比特](@entry_id:137928)状态为 $(\alpha|1\rangle_3 - \beta|0\rangle_3) = \sigma_x\sigma_z|\psi\rangle_3$。

其中 $\sigma_x$ 和 $\sigma_z$ 是泡利算符。

**第三步：经典通信与 Bob 的幺正修正**

Alice 将她的两比特经典测量结果通过经典通道发送给 Bob。Bob 根据收到的信息，对他他的[量子比特](@entry_id:137928)3施加一个相应的**幺正修正操作**。

-   收到 “00”：施加 $I$ (恒等操作)。
-   收到 “01”：施加 $\sigma_x$。
-   收到 “10”：施加 $\sigma_z$。
-   收到 “11”：施加 $\sigma_z\sigma_x$。

由于[泡利算符](@entry_id:144061)是自身的逆（$\sigma_i^2 = I$），并且 $(\sigma_z\sigma_x)^\dagger = \sigma_x^\dagger \sigma_z^\dagger = \sigma_x \sigma_z$，Bob 的操作精确地“撤销”了测量引入的变换。例如，如果 Alice 测得 "01"，Bob 的[量子比特](@entry_id:137928)处于 $\sigma_x|\psi\rangle_3$ 态。他施加 $\sigma_x$ 后，状态变为 $\sigma_x(\sigma_x|\psi\rangle_3) = \sigma_x^2|\psi\rangle_3 = |\psi\rangle_3$。无论 Alice 的测量结果如何，经过 Bob 的修正后，他的[量子比特](@entry_id:137928)最终都将处于原始状态 $|\psi\rangle$。至此，隐形传态完成。

### 基本原理与重要推论

#### 传输的是状态，而非物质

量子隐形传态这个术语可能会引起误解。协议传输的不是物理粒子本身，而是它的[量子态](@entry_id:146142)，即描述其所有量子属性的信息。在一个思想实验中 [@problem_id:2113274]，假设 Alice 想要传送的[光子](@entry_id:145192)A具有能量 $E_A$ 和[偏振态](@entry_id:175130) $|\psi\rangle$。她与 Bob 共享的[纠缠光子对](@entry_id:188235)（B和C）具有不同的能量 $E_B$。在协议结束后，Bob 的[光子](@entry_id:145192)C将拥有[偏振态](@entry_id:175130) $|\psi\rangle$，但它的能量仍然是 $E_B$。这是因为整个协议中的所有[量子操作](@entry_id:145906)（CNOT、哈达玛门、[泡利修正](@entry_id:142610)）都只作用于[量子比特](@entry_id:137928)的内部自由度（如偏振），而没有改变粒子的外部属性（如能量）。因此，是“状态”被销毁并异地重建，而非物质本身被传送。

#### 对因果律的遵从

量子纠缠的“瞬时”关联特性常常引发关于超光速通信的疑问。然而，量子隐形传态协议严格遵守因果律，不允许信息以超光速传播。关键在于经典通信信道的作用。

让我们考虑一种情况，在 Alice 完成[贝尔测量](@entry_id:136639)后，她发送给 Bob 的经典信息丢失了 [@problem_id:2113227]。Bob 知道测量已经发生，但对结果一无所知。从 Bob 的角度来看，他的[量子比特](@entry_id:137928)处于一个统计[混合态](@entry_id:141568)，即所有四种可能结果的等权重混合。我们可以用[密度矩阵](@entry_id:139892) $\rho_C$ 来描述 Bob 的[量子比特](@entry_id:137928)状态。在 Alice 测量之后，Bob 的[量子比特](@entry_id:137928)有 $\frac{1}{4}$ 的概率分别处于以下四个[纯态](@entry_id:141688)之一：$|\psi\rangle$, $\sigma_x|\psi\rangle$, $\sigma_z|\psi\rangle$, $\sigma_x\sigma_z|\psi\rangle$。其密度矩阵为：

$$
\rho_C = \frac{1}{4} \left( |\psi\rangle\langle\psi| + \sigma_x|\psi\rangle\langle\psi|\sigma_x + \sigma_z|\psi\rangle\langle\psi|\sigma_z + \sigma_x\sigma_z|\psi\rangle\langle\psi|\sigma_z\sigma_x \right)
$$

通过代数运算可以证明 [@problem_id:2113273]，这个密度矩阵等于：

$$
\rho_C = \frac{1}{2} I = \frac{1}{2} \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}
$$

这是一个**[最大混合态](@entry_id:137775)**。它不包含任何关于原始态 $|\psi\rangle$ 中系数 $\alpha$ 和 $\beta$ 的信息。无论 Bob 如何测量这个[量子比特](@entry_id:137928)，他得到 $|0\rangle$ 或 $|1\rangle$ 的概率都是 $\frac{1}{2}$。这意味着，没有 Alice 的经典信息，Bob 无法从他的[量子比特](@entry_id:137928)中提取任何关于 $|\psi\rangle$ 的有用信息。只有当经典信息（其传递速度受光速限制）到达后，Bob 才能进行正确的幺正操作，从而恢复出确定的状态 $|\psi\rangle$。因此，是纠缠和经典信息的结合才完成了状态的传输，二者缺一不可。

#### 对[不可克隆定理](@entry_id:146200)的遵从

[不可克隆定理](@entry_id:146200)是量子力学的一块基石，它指出不可能创造一个任意未知[量子态](@entry_id:146142)的精确、独立副本。量子隐形传态看似在 Bob 处“复制”了 Alice 的状态，但它并不违反此定理。原因在于，在创建 Bob 处副本的过程中，Alice 处的原始[量子态](@entry_id:146142)被不可逆地销毁了。

在协议的步骤分解中，Alice 的 CNOT 和哈达玛门操作都是幺正的，因而是可逆的。然而，在第二步中，Alice 对她的两个[量子比特](@entry_id:137928)进行了测量 [@problem_id:2113249]。[量子测量](@entry_id:272490)是一个不可逆的过程。一旦测量完成，Alice 的[量子比特](@entry_id:137928)1（携带原始态 $|\psi\rangle$）和[量子比特](@entry_id:137928)2就坍缩到了四个经典贝尔[基态](@entry_id:150928)之一。原始的叠加态 $|\psi\rangle$ 在 Alice 那里就不复存在了。因此，隐形传态不是“克隆”，而更像是“移动”：量子信息在一个地方消失，在另一个地方重现。

### 协议的推广与变体

#### 对纠缠资源的依赖性

量子隐形传态的成功严重依赖于共享纠缠的质量。

-   **纠缠的必要性**: 如果 Alice 和 Bob 共享的不是[纠缠态](@entry_id:152310)，而是像 $|+\rangle_B \otimes |+\rangle_C$ 这样的乘积态，隐形传态协议将完全失败 [@problem_id:2113289]。在这种情况下，无论 Alice 的测量结果是什么，Bob 的[量子比特](@entry_id:137928)总是处于与原始态 $|\psi\rangle$ 无关的状态 $|+\rangle_C$。对所有可能的输入态取平均，其平均保真度仅为 $\frac{1}{2}$，这相当于随机猜测，不比任何经典策略更好。这证明了纠缠是实现高保真度隐形传态的必要资源。

-   **不同[贝尔态](@entry_id:140749)资源**: 标准协议使用 $|\Phi^+\rangle$ 作为资源。如果使用其他[贝尔态](@entry_id:140749)，例如 $|\Psi^-\rangle_{BC} = \frac{1}{\sqrt{2}}(|01\rangle - |10\rangle)$，协议仍然可以工作，但 Bob 需要的修正算符集会改变 [@problem_id:2113298]。例如，当 Alice 测得 $|\Phi^+\rangle_{AB}$ 时，Bob 需要施加 $Y$ 算符来修正。这表明协议的内在逻辑结构保持不变，但具体的修正操作取决于所用纠缠资源的精确形式。

-   **非最大纠缠资源**: 协议也可以使用非最大纠缠的纯态，如 $| \psi_p \rangle = \sqrt{p}|00\rangle + \sqrt{1-p}|11\rangle$ (其中 $p \neq 1/2$)，或者更一般的形式如 $\frac{1}{\sqrt{2}}(|00\rangle + i|11\rangle)$ [@problem_id:2113234]。在这种情况下，隐形传态仍然可能，但 Bob 的修正操作通常会变得比简单的[泡利算符](@entry_id:144061)更复杂，并且保真度可能不再是完美的。一个量子信道何时会因为资源纠缠度不足而失去传输纠缠的能力（即成为“纠缠破缺”信道）？对于[纯态](@entry_id:141688)资源 $| \psi_p \rangle$，可以证明只有当纠缠完全消失时（即 $p=0$ 或 $p=1$），信道才会变成纠缠破缺的 [@problem_id:128203]。

#### 传输混合态与高维系统

-   **传输[混合态](@entry_id:141568)**: 隐形传态协议不仅能传输[纯态](@entry_id:141688)，也能完美地传输混合态。如果 Alice 的输入是一个由密度矩阵 $\rho_{in}$ 描述的混合态，那么在理想条件下，Bob 最终得到的输出态就是 $\rho_{out} = \rho_{in}$ [@problem_id:2113285]。这可以通过[密度矩阵](@entry_id:139892) formalism 进行直接计算，展示了协议的普适性。

-   **高维系统（Qutrit）隐形传态**: 隐形传态的原理可以推广到高于二维的量子系统。例如，对于一个[三能级系统](@entry_id:147049)（qutrit），其状态为 $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle + \gamma|2\rangle$。我们可以使用一对最大纠缠的 qutrit 对作为资源，并定义广义的贝尔基和广义的[泡利算符](@entry_id:144061) $X$ 和 $Z$（$X|j\rangle = |(j+1)\pmod 3\rangle$，$Z|j\rangle = \omega^j |j\rangle$，其中 $\omega = \exp(i 2\pi/3)$）。Alice 的测量将产生 9 种可能的结果（用两个三[进制](@entry_id:634389)数 $k,l$ 表示），Bob 则需要根据收到的 $(k,l)$ 施加 9 种修正算符 $U_{kl}$ 之一。可以推导出，这些修正算符由广义泡利算符构成，形式为 $U_{kl} = Z^k X^l$ [@problem_id:2113245]。

### 应用与高级课题

#### [纠缠交换](@entry_id:137925) (Entanglement Swapping)

[纠缠交换](@entry_id:137925)是量子隐形传态最重要和最巧妙的应用之一，它是构建量子中继和大型[量子网络](@entry_id:144522)的基础。其核心思想是“传输纠缠本身”。

设想一个场景 [@problem_id:2113292]，Alice 和 Bob 各自与中间人 Charlie 共享一个纠缠对。即 Alice (A) 与 Charlie (C1) 纠缠，Charlie (C2) 与 Bob (B) 纠缠。Alice 和 Bob 之间没有直接的相互作用。现在，如果 Charlie 对他拥有的两个[量子比特](@entry_id:137928) (C1, C2) 进行一次贝尔基测量，并将测量结果公布，那么 Alice 和 Bob 的[量子比特](@entry_id:137928) (A, B) 会瞬间坍缩到一个纠缠态上。

这个过程可以理解为：Charlie 实际上是将在 C1 上的纠缠关系“隐形传送”到了 B 上。更具体地说，如果初始纠缠对是 $|\Phi^+\rangle_{AC1}$ 和 $|\Phi^+\rangle_{C2B}$，当 Charlie 的测量结果为 $|\Psi^-\rangle_{C1C2}$ 时，Alice 和 Bob 之间的[量子比特](@entry_id:137928)将处于 $|\Psi^-\rangle_{AB}$ 态。实际上，Charlie 的四种[贝尔测量](@entry_id:136639)结果将分别对应 Alice 和 Bob 之间形成的四种贝尔态之一。通过经典通信，Alice 和 Bob 可以知道他们共享的是哪种[贝尔态](@entry_id:140749)，并可以通过局域操作将其转换为标准形式。这个过程也常被描述为“将一个纠缠对的一半进行隐形传态” [@problem_id:2113276]。

#### 噪声环境下的隐形传态

在实际应用中，纠缠资源总是会受到噪声的干扰。一个典型的[噪声模型](@entry_id:752540)是**韦尔纳态 (Werner state)**，它是一个最大纠缠态 $|\Phi^+\rangle$ 和一个[最大混合态](@entry_id:137775) $\frac{I \otimes I}{d^2}$ 的混合体，其形式为 $\rho_W = p |\Phi^+\rangle\langle\Phi^+| + (1-p) \frac{I \otimes I}{d^2}$，其中 $p$ 是混合概率或保真度，$d$ 是系统维度。

-   **平均保真度**: 使用韦尔纳态作为资源，隐形传态的质量会下降。对于一个 qutrit 系统（$d=3$），使用参数为 $p$ 的韦尔纳态进行隐形传态，其平均保真度 $\bar{F}$（对所有可能的纯输入态取平均）为 $\bar{F} = \frac{2p+1}{3}$ [@problem_id:128222]。当 $p=1$（理想资源）时，$\bar{F}=1$；当 $p=0$（完全无纠缠的噪声）时，$\bar{F}=1/3$，这正是在三维系统中随机猜测的保真度。

-   **[纠缠交换](@entry_id:137925)与噪声**: 当用于[纠缠交换](@entry_id:137925)的两个初始[纠缠对](@entry_id:160576)都是带有可见度 $V$ 的韦尔纳态时，交换成功后，新建立的[纠缠对](@entry_id:160576)的保真度会进一步下降。其最终态的保真度（相对于理想的 $|\Psi^-\rangle$ 态）为 $F = \frac{1+3V^2}{4}$ [@problem_id:723850]。这表明噪声在[量子网络](@entry_id:144522)中会逐级累积。

#### 门隐形传态与远程测量

隐形传态的概念可以从传输“数据”（[量子态](@entry_id:146142)）推广到传输“操作”（量子门）。

-   **门隐形传态 (Gate Teleportation)**: 我们可以利用隐形传态的框架来实现一个非局域的量子门。例如，要在 Alice 和 Bob 的两个[量子比特](@entry_id:137928)上实现一个受控-Z (CZ) 门，可以通过使用两个共享的[纠缠对](@entry_id:160576)，并结合 Alice 的局域操作、测量和经典通信来完成。这个过程的质量可以用**过程保真度**来衡量。如果使用的纠缠资源是两个可见度为 $p$ 的韦尔纳态，那么实现的 CZ 门的过程保真度为 $F_p = \frac{(3p+1)^2}{16}$ [@problem_id:723826]。

-   **远程测量 (Remote Measurement)**: 假设 Bob 有一个[量子比特](@entry_id:137928)需要用 Alice 实验室里的一个特殊测量设备（一个 [POVM](@entry_id:138770) $\lbrace M_k \rbrace$）来测量。他们可以通过隐形传态将 Bob 的[量子比特](@entry_id:137928)状态传送到 Alice 那里进行测量。如果这个过程中的经典信道有噪声（例如比特翻转错误概率为 $\epsilon$），那么从 Bob 的角度看，这个过程等效于对他的原始[量子比特](@entry_id:137928)进行了一个新的、被噪声扭曲的有效测量 $\lbrace M'_k \rbrace$。这个有效的 [POVM](@entry_id:138770) 算符可以被精确计算出来，它包含了原始算符 $M_k$ 以及被[泡利算符](@entry_id:144061)“扭曲”的项，其系数与噪声概率 $\epsilon$ 相关 [@problem_id:128208]：
    $$
    M'_k = (1-\epsilon)^2 M_k + \epsilon(1-\epsilon)(\sigma_x M_k \sigma_x + \sigma_z M_k \sigma_z) + \epsilon^2 \sigma_y M_k \sigma_y
    $$
    这个例子完美地展示了经典世界的噪声如何转化为[量子操作](@entry_id:145906)的特定[噪声模型](@entry_id:752540)。

-   **[纠缠的单配性](@entry_id:141408)**: 纠缠是一种独特的量子资源，具有“单配性” (monogamy) 的特点，即一个[量子比特](@entry_id:137928)无法同时与两个或多个其他[量子比特](@entry_id:137928)形成最大纠缠。隐形传态过程生动地展示了这一点。在一个涉及 Greenberger-Horne-Zeilinger (GHZ) 态 $|GHZ\rangle_{ABC} = \frac{1}{\sqrt{2}}(|000\rangle + |111\rangle)$ 的协议中 [@problem_id:128193]，如果 Alice 将她拥有的 A [量子比特](@entry_id:137928)的状态隐形传态给第四方 David，那么原来在 Bob 和 Charlie 之间的纠缠关系会完全消失。计算表明，协议结束后，Bob 和 Charlie 的联合状态是一个可分离的[混合态](@entry_id:141568)，它们之间的[对数负性](@entry_id:137607)为零。这表明 Alice 将其与 B、C 的纠缠关系“消耗”掉，以建立与 David 的纠缠关系。

综上所述，量子隐形传态不仅是一个精妙的协议，更是一个强大的理论工具，它深刻地揭示了量子信息、纠缠、测量和经典通信之间的复杂互动，并为[量子计算](@entry_id:142712)和[量子通信](@entry_id:138989)的广阔应用领域奠定了基础。