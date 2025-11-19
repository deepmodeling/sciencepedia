## 引言
在[量子信息处理](@entry_id:158111)中，任何量子系统都不可避免地与环境相互作用，导致信息失真或丢失。为了构建可靠的[量子技术](@entry_id:142946)，我们必须精确量化这些噪声过程（即“量子信道”）对信息的影响。本文旨在系统性地建立一个框架，用以衡量量子信道在多大程度上能够保持信息，填补从直观概念到严格[信息论极限](@entry_id:750636)之间的认知鸿沟。在接下来的内容中，读者将首先学习用于量化信息保持度的核心**原理与机制**，包括保真度、[信道容量](@entry_id:143699)等基本度量。随后，我们将探索这些理论工具在[量子计算](@entry_id:142712)、凝聚态物理乃至[黑洞物理学](@entry_id:160472)中的广泛**应用与跨学科交叉**，展示其强大的解释力。最后，通过一系列**动手实践**问题，读者将有机会应用所学知识解决具体问题。让我们首先深入探讨衡量信道性能的各项基本原理。

## 原理与机制

在量子世界中，任何系统都不可避免地与周围环境发生相互作用。这种相互作用，通常被称为噪声，会导致量子信息的丢失或失真。为了设计、分析和优化[量子计算](@entry_id:142712)机、量子通信网络等量子技术，我们必须能够精确地量化和理解这些噪声过程对信息的影响。本章将系统地介绍一系列核心原理与机制，用以衡量[量子信道](@entry_id:145403)（即描述噪声过程的数学模型）在多大程度上能够保持信息。我们将从直观的保真度概念入手，逐步深入到更强大的数学工具和信息论度量，最终探讨信息传输的根本极限。

### 保真度：衡量状态相似性

衡量信道性能最直观的方法，是比较输入信道的[量子态](@entry_id:146142)与输出态的“相似”程度。在量子力学中，这种相似性由**保真度 (fidelity)** 来量化。对于两个[量子态](@entry_id:146142)，由[密度矩阵](@entry_id:139892) $\rho$ 和 $\sigma$ 描述，它们之间的保真度定义为 $F(\rho, \sigma) = \left(\text{Tr}\sqrt{\sqrt{\rho}\sigma\sqrt{\rho}}\right)^2$。当其中一个态是[纯态](@entry_id:141688) $|\psi\rangle$ 时（即 $\rho = |\psi\rangle\langle\psi|$），定义简化为 $F(|\psi\rangle, \sigma) = \langle\psi|\sigma|\psi\rangle$。保真度取值在 $0$ 和 $1$ 之间，当两个态完全相同时为 $1$，当它们正交时为 $0$。

#### 平均保真度

一个信道 $\mathcal{E}$ 的性能不应只取决于它对某个特定输入态的作用，而应反映其对所有可能输入态的平均影响。因此，我们引入**平均保真度 (average fidelity)** $F_{avg}(\mathcal{E})$ 的概念，它是在所有可能的纯输入态 $|\psi\rangle$ 上对保真度 $\langle\psi|\mathcal{E}(|\psi\rangle\langle\psi|)| \psi\rangle$ 进行的均匀平均。对于单个[量子比特](@entry_id:137928)，这个平均是在[布洛赫球面](@entry_id:138823)上对所有纯态进行积分：

$$
F_{avg}(\mathcal{E}) = \int \langle\psi|\mathcal{E}(|\psi\rangle\langle\psi|)|\psi\rangle\, d\psi
$$

其中积分是关于归一化的[哈尔测度](@entry_id:142417)进行的。

为了理解其具体应用，我们可以考察一个常见的[噪声模型](@entry_id:752540)——**各向异性退极化信道 (anisotropic depolarizing channel)** [@problem_id:92431]。该信道以概率 $p_x, p_y, p_z$ 分别对[量子比特](@entry_id:137928)施加泡利 $X, Y, Z$ 错误，以概率 $1 - p_x - p_y - p_z$ 保持其状态不变。其作用形式为：

$$
\mathcal{E}_{aniso}(\rho) = (1 - p_x - p_y - p_z)\rho + p_x X\rho X + p_y Y\rho Y + p_z Z\rho Z
$$

通过在[布洛赫球面](@entry_id:138823)上进行积分，可以计算出该信道的平均保真度为：

$$
F_{avg}(\mathcal{E}_{aniso}) = 1 - \frac{2}{3}(p_x + p_y + p_z)
$$

这个结果直观地表明，总的错误概率 $p_{total} = p_x + p_y + p_z$ 越大，平均保真度就越低。系数 $\frac{2}{3}$ 的出现源于在三维空间中对[泡利算符](@entry_id:144061)[期望值](@entry_id:153208)的平方进行平均的结果。

对于一类被称为**幺正信道 (unital channels)** 的特殊信道，即满足 $\mathcal{E}(I) = I$ 的信道（其中 $I$ 是单位算符），平均保真度的计算可以被大大简化。例如，**[相位阻尼](@entry_id:147888)信道 (phase damping channel)** 就是一个幺正信道 [@problem_id:60896]。该信道描述了[量子相干性](@entry_id:143031)的损失而没有能量的交换，其对[密度矩阵](@entry_id:139892) $\rho = \begin{pmatrix} \rho_{00} & \rho_{01} \\ \rho_{10} & \rho_{11} \end{pmatrix}$ 的作用是 $\mathcal{E}_\gamma(\rho) = \begin{pmatrix} \rho_{00} & (1-\gamma)\rho_{01} \\ (1-\gamma)\rho_{10} & \rho_{11} \end{pmatrix}$，其中 $\gamma$ 是阻尼参数。对于单比特幺正信道，平均保真度可以通过一个简洁的公式计算：

$$
F_{avg}(\mathcal{E}) = \frac{1}{2} + \frac{1}{12} \sum_{k \in \{x,y,z\}} \text{Tr}[\sigma_k \mathcal{E}(\sigma_k)]
$$

利用这个公式，我们可以求得[相位阻尼](@entry_id:147888)信道的平均保真度为 $F_{avg}(\mathcal{E}_\gamma) = 1 - \frac{\gamma}{3}$。这个结果表明，与退极化信道不同，[相位阻尼](@entry_id:147888)信道只影响相干项（即非对角元），因此其对平均保真度的影响方式也不同。

#### [纠缠保真度](@entry_id:138783)

在[量子计算](@entry_id:142712)和[量子通信](@entry_id:138989)中，我们关心的不仅仅是单个[量子态](@entry_id:146142)的保持，更重要的是保持[量子态](@entry_id:146142)之间的**纠缠 (entanglement)**。纠缠是[量子信息处理](@entry_id:158111)的核心资源。因此，一个更符合应用场景的性能指标是**[纠缠保真度](@entry_id:138783) (entanglement fidelity)** $F_e(\mathcal{E})$。

其定义过程如下：首先，在待测系统 $A$ 和一个隔离的[参考系](@entry_id:169232)统 $R$ 之间制备一个最大[纠缠态](@entry_id:152310)，如[贝尔态](@entry_id:140749) $|\Psi^+\rangle_{AR} = \frac{1}{\sqrt{d}} \sum_{i=0}^{d-1} |i\rangle_A \otimes |i\rangle_R$。然后，让信道 $\mathcal{E}$ 只作用于系统 $A$，[参考系](@entry_id:169232)统 $R$ 保持不变。[纠缠保真度](@entry_id:138783)就是初始的[纠缠态](@entry_id:152310)与经过信道作用后的末态之间的保真度。

$$
F_e(\mathcal{E}) = \langle\Psi^+|_{AR} \, (\mathcal{E}_A \otimes \mathcal{I}_R)(|\Psi^+\rangle\langle\Psi^+|_{AR}) \, |\Psi^+\rangle_{AR}
$$

[纠缠保真度](@entry_id:138783)衡量了一个信道保持与外部系统纠缠关系的能力，这对于评估[量子门](@entry_id:143510)和量子算法的性能至关重要。

让我们考虑一个**退相干信道 (dephasing channel)** [@problem_id:92458]，其作用为 $\mathcal{E}(\rho) = (1-p) \rho + p Z \rho Z$。这个信道以概率 $p$ 施加一个 $Z$ 错误。通过计算，我们发现其[纠缠保真度](@entry_id:138783)为 $F_e(\mathcal{E}) = 1-p$。这个结果非常直观：[纠缠保真度](@entry_id:138783)恰好等于状态不发生[退相干](@entry_id:145157)错误的概率。

我们可以将此推广到更一般的**泡利信道 (Pauli channel)** [@problem_id:92571]，其作用为 $\mathcal{E}(\rho) = p_I \rho + p_X X \rho X + p_Y Y \rho Y + p_Z Z \rho Z$，其中 $p_I = 1 - p_X - p_Y - p_Z$ 是无错误发生的概率。可以证明，其[纠缠保真度](@entry_id:138783)为 $F_e(\mathcal{E}) = p_I = 1 - p_X - p_Y - p_Z$。这再次印证了一个清晰的物理图像：[纠缠保真度](@entry_id:138783)就是信道“什么都不做”（即施加单位算符）的概率。

#### 保真度的统计涨落

平均保真度给出了信道性能的一个总体评估，但它掩盖了一个重要的细节：信道对不同输入态的影响可能不是均匀的。例如，**幅度阻尼信道 (amplitude damping channel)** 模拟的是粒子从[激发态](@entry_id:261453) $|1\rangle$ 到[基态](@entry_id:150928) $|0\rangle$ 的自发辐射过程。它对 $|0\rangle$ 态没有影响，但会使 $|1\rangle$ 态衰变。显然，它对[布洛赫球面](@entry_id:138823)“南极”附近的状态影响更大。

为了量化这种不均匀性，我们可以考察保真度的统计涨落，例如定义一个**保真度弥散 (Fidelity Dispersion)**，即保真度在所有纯输入态上的[方差](@entry_id:200758) $V_F(\mathcal{E}) = \langle F(\psi)^2 \rangle - \langle F(\psi) \rangle^2$ [@problem_id:92417]。对于幅度阻尼信道，可以计算出其保真度弥散是一个关于衰变概率 $\gamma$ 的非零函数。这证实了该信道对不同输入态的作用确实存在差异，而一个完全均匀的信道（如退极化信道）其保真度弥散为零。

### 可区分性与[信息回流](@entry_id:146865)

除了衡量状态的相似性，我们还关心信道如何影响我们区分不同[量子态](@entry_id:146142)的能力。这在量子通信中尤为重要，因为信息编码在可区分的状态上。

#### [迹距离](@entry_id:142668)

两个[量子态](@entry_id:146142) $\rho$ 和 $\sigma$ 的**可区分性 (distinguishability)** 由**[迹距离](@entry_id:142668) (trace distance)** 来量化，定义为：

$$
D(\rho, \sigma) = \frac{1}{2} \text{Tr}|\rho - \sigma| = \frac{1}{2} \text{Tr}\sqrt{(\rho - \sigma)^\dagger (\rho - \sigma)}
$$

[迹距离](@entry_id:142668)的取值范围也是 $[0, 1]$。$D=0$ 意味着两个态完全相同，无法区分；$D=1$ 意味着它们是正交的，可以完美地区分。其重要的操作含义是，通过一次测量能够区分 $\rho$ 和 $\sigma$ 的最大成功概率为 $\frac{1}{2}(1 + D(\rho, \sigma))$。

噪声信道通常会降低不同状态之间的[迹距离](@entry_id:142668)，从而使信息更难被读取。例如，考虑用[基态](@entry_id:150928) $|0\rangle$ 和[激发态](@entry_id:261453) $|1\rangle$ 来编码经典比特 '0' 和 '1'。这两个初始状态是正交的，[迹距离](@entry_id:142668)为 $1$。当它们通过一个衰变概率为 $\gamma$ 的幅度阻尼信道 $\mathcal{E}$ 后，输出态变为 $\mathcal{E}(|0\rangle\langle0|)$ 和 $\mathcal{E}(|1\rangle\langle1|)$。通过计算可以发现，它们之间的[迹距离](@entry_id:142668)变为了 $D(\mathcal{E}(\rho_0), \mathcal{E}(\rho_1)) = 1 - \gamma$ [@problem_id:92425]。这意味着，随着衰变概率 $\gamma$ 的增加，区分这两个编码状态的能力随之下降，当 $\gamma=1$ 时，无论输入是 $|0\rangle$ 还是 $|1\rangle$，输出都是 $|0\rangle\langle0|$，[迹距离](@entry_id:142668)为 $0$，信息完全丢失。

#### [非马尔可夫动力学](@entry_id:142796)与[信息回流](@entry_id:146865)

在许多简单的模型中，[系统与环境](@entry_id:142270)的相互作用被假设为**马尔可夫的 (Markovian)**，这意味着环境没有“记忆”，信息只能单向地从系统流向环境。在这种情况下，任何两个状态之间的[迹距离](@entry_id:142668)只会随时间单调不增。

然而，在更真实的物理系统中，环境可能具有复杂的内部结构和动力学，导致它能够“记住”过去与系统的相互作用。这种**非马尔可夫 (non-Markovian)** 效应可以导致信息从环境**回流 (backflow)** 到系统。这种[信息回流](@entry_id:146865)的一个标志性特征就是，两个状态之间的[迹距离](@entry_id:142668)在[演化过程](@entry_id:175749)中会短暂地增加，意味着它们在某个时间段内变得比之前更容易区分。

一个可以展示这种现象的典型模型是，一个[量子比特](@entry_id:137928)与一个经典**[随机电报噪声](@entry_id:269610) (random telegraph noise)** 环境耦合 [@problem_id:92476]。在这种模型的强耦合区域，可以观察到两个初始正交态（例如 $|\psi_1\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$ 和 $|\psi_2\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$）之间的[迹距离](@entry_id:142668)随时间[振荡](@entry_id:267781)衰减。[迹距离](@entry_id:142668)的每次增加都对应着一次[信息回流](@entry_id:146865)。通过分析[迹距离](@entry_id:142668)对时间的导数，我们可以精确地计算出[信息回流](@entry_id:146865)首次开始的时刻 $t_{backflow}$，这个时刻是耦合强度 $b$ 和噪声切换率 $\gamma$ 的函数。这一现象挑战了信息总是单向丢失的简单观念，并开启了利用[环境记忆](@entry_id:136908)来对抗退相干的研究方向。

### 信道的数学表示与性质

为了更深入地分析信道，我们需要一个更强大的数学框架。**Choi-Jamiołkowski 同构**提供了一个关键工具，它将一个作用于状态的动态过程（信道）映射为一个静态的[量子态](@entry_id:146142)。

#### Choi-Jamiołkowski 同构

该同构将一个作用于 $d$ 维系统的信道 $\mathcal{E}$ 映射到一个定义在 $d \times d$ 维复合系统上的**Choi 矩阵** $J(\mathcal{E})$：

$$
J(\mathcal{E}) = (I \otimes \mathcal{E})(|\Phi^+\rangle\langle\Phi^+|)
$$

其中 $I$ 是一个 $d$ 维[辅助系统](@entry_id:142219)上的单位映射，$|\Phi^+\rangle = \frac{1}{\sqrt{d}} \sum_{i=0}^{d-1} |i\rangle \otimes |i\rangle$ 是一个最大纠缠态。这个映射的美妙之处在于，信道 $\mathcal{E}$ 的所有性质都完全编码在其对应的 Choi 矩阵 $J(\mathcal{E})$ 中。研究一个动态的映射被转化为了研究一个静态的[密度矩阵](@entry_id:139892)。

#### [完全正性](@entry_id:149274)

一个[线性映射](@entry_id:185132)要成为一个物理上合法的量子信道，它必须是**完全正的 (completely positive)**。这意味着，即使该映射只作用于一个更大纠缠系统的一部分，整个系统的状态也必须保持为合法的（即正半定的）[密度矩阵](@entry_id:139892)。Choi-Jamiołkowski 同构给出了一个简单的判据：一个映射 $\mathcal{E}$ 是完全正的，当且仅当其 Choi 矩阵 $J(\mathcal{E})$ 是一个正半定矩阵。

我们可以利用这个判据来确定一个给定的[参数化](@entry_id:272587)线性映射在何种条件下是物理合法的。例如，考虑一个由单位映射 $\mathcal{I}(\rho) = \rho$ 和归约映射 $\mathcal{R}(\rho) = \operatorname{Tr}(\rho)I_d - \rho$ 线性组合而成的映射 $\mathcal{E}_p(\rho) = (1-p) \mathcal{I}(\rho) + p \mathcal{R}(\rho)$ [@problem_id:92507]。通过计算其 Choi 矩阵的[特征值](@entry_id:154894)，并要求所有[特征值](@entry_id:154894)非负，我们可以推导出参数 $p$ 必须满足 $p \le d/(2d-1)$。为了让这个映射对于任意维度 $d$ 的系统都是完全正的，$p$ 必须满足所有这些不等式，即 $p \le \inf_{d\ge2} \frac{d}{2d-1} = \frac{1}{2}$。

#### 信道纯度

Choi 矩阵的纯度 $\text{Tr}[J(\mathcal{E})^2]$ 可以被用作一个衡量信道“噪声程度”的指标，我们称之为**信道纯度**。对于一个无噪声的[幺正演化](@entry_id:145020) $\mathcal{E}(\rho) = U\rho U^\dagger$，其 Choi 矩阵是一个纯态，纯度为 $1$。而对于一个有噪声的信道，其 Choi 矩阵是一个混态，纯度小于 $1$。例如，对于参数为 $\lambda$ 的[相位阻尼](@entry_id:147888)信道，其信道纯度可以计算为 $1 - \lambda + \lambda^2/2$ [@problem_id:92427]，它随着噪声参数 $\lambda$ 的增加而减小。

#### 纠缠破坏信道

一类特别“嘈杂”的信道被称为**纠缠破坏 (entanglement-breaking, EB) 信道**。顾名思义，无论输入态 $\rho_{AB}$ 具有多么复杂的纠缠结构，只要信道作用于其中一个子系统（例如 $A$），输出态 $(\mathcal{E}_A \otimes I_B)(\rho_{AB})$ 一定会变成一个**可分离态 (separable state)**，即没有任何纠缠。

关于 EB 信道有一个基本定理：一个信道 $\mathcal{E}$ 是纠缠破坏的，当且仅当其 Choi 矩阵 $J(\mathcal{E})$ 是一个可分离态。这个定理将判断信道的动态性质转化为了判断一个静态的 Choi 矩阵是否可分离。

对于两个[量子比特](@entry_id:137928)的系统，一个强大的可分离性判据是 **Peres-Horodecki 判据 (PPT 判据)**，它指出一个态是可分离的当且仅当其**[部分转置](@entry_id:136776) (partial transpose)** 后仍然是正半定的。结合这两个工具，我们可以精确地确定一个信道何时是纠缠破坏的。

例如，考虑一个其 Choi 矩阵由 $J_p \propto p |\Phi^{+}\rangle\langle\Phi^{+}| + (1-p) (|01\rangle\langle01|+|10\rangle\langle10|)$ 给出的信道族 [@problem_id:92453]。通过计算其[部分转置](@entry_id:136776)矩阵的[特征值](@entry_id:154894)并要求它们非负，我们发现该信道是纠缠破坏的条件是 $p \le 2/3$。同样的技术也可以应用于更物理的模型，如**广义幅度阻尼信道 (generalized amplitude damping channel)**，从而将纠缠破坏的条件与[热噪声](@entry_id:139193)布居数 $N$ 和衰变概率 $\gamma$ 联系起来 [@problem_id:92395]。

对于具有高度对称性的信道，例如 **SU(d)协变信道**，其分析可以被大大简化 [@problem_id:92411]。这类信道的 Choi 矩阵可以写成对称[子空间](@entry_id:150286)投影仪 $P_S$ 和反对称[子空间](@entry_id:150286)投影仪 $P_A$ 的[线性组合](@entry_id:154743) $C_\Phi = \lambda_S P_S + \lambda_A P_A$。通过分析其[部分转置](@entry_id:136776)的谱，可以推导出纠缠破坏的条件仅仅取决于两个[特征值](@entry_id:154894)的比率 $R = \lambda_A / \lambda_S$，即 $R \le 1/(d-1)$。

### 信道容量：信息传输的极限

最终，我们希望知道通过一个给定的噪声信道，到底能够可靠地传输多少信息。这个问题的答案由信道的**容量 (capacity)** 给出。我们需要区分两种不同类型的信息：经典信息和[量子信息](@entry_id:137721)。

#### 经典容量

**经典容量 (Classical capacity)** $C(\mathcal{N})$ 指的是一个[量子信道](@entry_id:145403) $\mathcal{N}$ 每使用一次能够可靠传输的经典比特数的最大值。**Holevo-Schumacher-Westmoreland (HSW) 定理** 给出了其数学表达式。该定理指出，经典容量等于在所有可能的输入态系综 $\{q_i, \rho_i\}$ 上可以获得的最大**Holevo 信息 (Holevo information)** $\chi$。

Holevo 信息 $\chi(\{q_i, \sigma_i\}) = S(\sum_i q_i \sigma_i) - \sum_i q_i S(\sigma_i)$，量化了一个[量子态](@entry_id:146142)系综 $\{q_i, \sigma_i\}$ 中可被提取的经典[信息量](@entry_id:272315)。其中 $S(\cdot)$ 是冯诺依曼熵。

例如，对于一个三维（qutrit）的**替换信道**，它以概率 $p$ 将任意输入态替换为固定的 $|2\rangle\langle2|$ 态，以概率 $1-p$ 保持不变 [@problem_id:92512]。直觉上，任何编码在 $|2\rangle$ 态上的信息都会丢失。因此，最优的编码策略是在与 $|2\rangle$ 正交的[子空间](@entry_id:150286)中进行。通过选择输入态为 $|0\rangle$ 和 $|1\rangle$ 并计算相应的 Holevo 信息，我们发现其经典容量恰好为 $C(\mathcal{N}) = 1-p$。

另一个例子涉及[连续变量系统](@entry_id:144293)，比如用相干态 $|\alpha\rangle$ 和 $|-\alpha\rangle$ 编码信息，并通过一个纯损耗信道传输 [@problem_id:92553]。尽管输入是[纯态](@entry_id:141688)，经过信道后平均态是混态，其熵（即 Holevo 信息）给出了可获取的[信息量](@entry_id:272315)上界。

#### [量子容量](@entry_id:144186)

**[量子容量](@entry_id:144186) (Quantum capacity)** $Q(\mathcal{E})$ 指的是一个量子信道 $\mathcal{E}$ 每使用一次能够可靠传输的[量子比特](@entry_id:137928)数（qubits）的最大值。这是构建[容错量子计算机](@entry_id:141244)和[量子互联网](@entry_id:143445)的核心指标。

[量子容量](@entry_id:144186)的计算与一个关键量——**[相干信息](@entry_id:147583) (coherent information)** $I_c(\rho, \mathcal{E})$——密切相关。对于给定的输入态 $\rho$，[相干信息](@entry_id:147583)定义为：

$$
I_c(\rho, \mathcal{E}) = S(\mathcal{E}(\rho)) - S_{ex}(\rho, \mathcal{E})
$$

这里的 $S(\mathcal{E}(\rho))$ 是输出态的熵，而 $S_{ex}$ 是**交换熵 (exchange entropy)**，它等于[系统与环境](@entry_id:142270)相互作用后环境状态的熵。因此，[相干信息](@entry_id:147583)可以被理解为“进入系统的信息”（由输出熵体现）减去“泄漏到环境的信息”（由环境熵体现）的净差额。如果[相干信息](@entry_id:147583)为正，说明信息在系统中得到了净保留，有可能通过纠错码恢复。

[量子容量](@entry_id:144186)最终由正则化的[相干信息](@entry_id:147583)给出：$Q(\mathcal{E}) = \lim_{n\to\infty} \frac{1}{n} \max_{\rho_n} I_c(\rho_n, \mathcal{E}^{\otimes n})$。

计算[相干信息](@entry_id:147583)通常需要计算环境的最终状态，这可能很复杂。例如，对于一个输入为对[角态](@entry_id:145477)的[退相干](@entry_id:145157)信道，我们需要显式地构造环境态矩阵并计算其冯诺依曼熵 [@problem_id:92551]。在某些情况下，[相干信息](@entry_id:147583)可能为零，即使输入态是纯态。例如，对于幅度阻尼信道，当输入为 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)$ 时，其[相干信息](@entry_id:147583)恒为零 [@problem_id:92435]，表明对于此特定输入，没有任何[量子信息](@entry_id:137721)可以被可靠地传输。

一个理解[相干信息](@entry_id:147583)的强大视角来自于**互补信道 (complementary channel)**。任何量子信道 $\mathcal{E}$ 描述了信息从系统到系统的演化，其互补信道 $\mathcal{E}^c$ 则描述了同样过程中信息从系统到环境的演化。一个深刻的结论是，交换熵 $S_{ex}(\rho, \mathcal{E})$ 正是互补信道输出态的熵 $S(\mathcal{E}^c(\rho))$。这使得[相干信息](@entry_id:147583)可以被重写为 $I_c(\rho, \mathcal{E}) = S(\mathcal{E}(\rho)) - S(\mathcal{E}^c(\rho))$。这个形式清晰地揭示了量子信息保持是系统最终状态的熵与环境最终状态的熵之间的竞争。例如，我们可以通过计算互补信道作用于[最大混合态](@entry_id:137775)的输出来计算[相干信息](@entry_id:147583) [@problem_id:92398]。一个具体的例子是，[系统与环境](@entry_id:142270)发生[受控非门](@entry_id:180955)（CNOT）相互作用，这可以看作一个互补信道的过程，导致环境最终处于一个[混合态](@entry_id:141568)，其纯度降低 [@problem_id:92402]。

#### 强逆转换指数

[量子容量](@entry_id:144186) $Q(\mathcal{E})$ 划定了一个清晰的界限。当传输速率 $R  Q(\mathcal{E})$ 时，存在可以使错误率任意小的编码方案。但当速率 $R  Q(\mathcal{E})$ 时，会发生什么？**强逆转换定理 (strong converse theorem)** 指出，此时传输的错误概率不仅不会趋于零，反而会随着信道使用次数 $n$ 的增加而指数地趋于 $1$。

这个[指数收敛](@entry_id:142080)的速度由**强逆转换指数** $\xi_Q(R, \mathcal{E})$ 描述。对于一类被称为**反可降解 (antidegradable)** 的信道（这类信道的[量子容量](@entry_id:144186)为零），其强逆转换指数具有一个非常简洁的形式。例如，当衰减概率 $\gamma  1/2$ 时，幅度阻尼信道就是反可降解的。对于任何超出其容量（即 $R0$）的传输尝试，其强逆转换指数为 $\xi_Q(R, \mathcal{E}_\gamma) = R/2$ [@problem_id:92508]。这个结果为超高速率量子通信的失败模式提供了定量的刻画，在[量子信息论](@entry_id:141608)的编码理论中具有重要意义。