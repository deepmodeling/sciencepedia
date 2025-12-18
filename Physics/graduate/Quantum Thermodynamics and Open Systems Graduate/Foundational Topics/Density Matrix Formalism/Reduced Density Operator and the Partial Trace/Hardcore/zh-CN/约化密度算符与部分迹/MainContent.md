## 引言
在广阔的量子宇宙中，任何我们感兴趣的系统都只是更大整体的一部分。然而，与经典世界不同，[量子纠缠](@entry_id:136576)以一种深刻的方式将子系统与其环境联系在一起，使得我们无法简单地忽略“外部世界”。那么，我们如何才能在数学上精确地描述一个开放量子子系统的状态，并预测其行为呢？这个根本性问题引出了[量子理论](@entry_id:145435)中一个至关重要的概念：**[约化密度算符](@entry_id:190449)**，以及获得它的核心数学操作——**[偏迹](@entry_id:146482)**。

本文旨在系统性地阐明[约化密度算符](@entry_id:190449)与[偏迹](@entry_id:146482)的理论与应用。我们将从第一章 **“原理与机制”** 开始，深入探讨为何需要这一工具，给出其严格的数学定义，并解析其作为完全正保迹(CPTP)映射的关键性质。接着，在第二章 **“应用与跨学科联系”** 中，我们将展示这一概念如何成为理解[退相干](@entry_id:145157)、[量化纠缠](@entry_id:144669)、构建[量子热力学](@entry_id:140152)乃至探测拓扑物态的基石，连接起物理、化学与信息科学等多个领域。最后，通过第三章 **“动手实践”** 中的精选练习，读者将有机会亲手计算[约化密度算符](@entry_id:190449)，并模拟其在开放[系统动力学](@entry_id:136288)中的演化，从而将理论知识转化为实践能力。

## 原理与机制

在量子力学中，当我们研究一个复合系统的子系统时，我们面临一个核心挑战：如何描述一个只构成宇宙一部分的量子系统？与经典力学中我们可以简单地忽略不感兴趣的自由度不同，[量子纠缠](@entry_id:136576)的存在使得子系统与其环境之间存在着非经典的关联。即使整个复合系统处于一个完全确定的纯态，其子系统也可能表现出统计不确定性。为了解决这个问题，我们需要一个数学工具，它必须能够（1）仅利用子系统的自由度来形式化描述；（2）准确预测在该子系统上进行任何可能测量的所有统计结果。这个工具就是**[约化密度算符](@entry_id:190449)（reduced density operator）**，而获得它的过程被称为**[偏迹](@entry_id:146482)（partial trace）**。本章将深入探讨[约化密度算符](@entry_id:190449)的原理、性质及其在开放量子系统理论中的核心作用。

### [约化密度算符](@entry_id:190449)的运算必要性与定义

考虑一个由我们感兴趣的系统 $S$ 和其环境 $E$ 组成的[复合量子系统](@entry_id:193313)。其总希尔伯特空间是[张量积](@entry_id:140694)空间 $\mathcal{H} = \mathcal{H}_S \otimes \mathcal{H}_E$。复合系统的状态由作用在 $\mathcal{H}$ 上的**[密度算符](@entry_id:138151)** $\rho_{SE}$ 描述。一个算符要成为密度算符，必须满足三个条件：它是正半定的（$\rho_{SE} \ge 0$），它的迹为1（$\mathrm{Tr}(\rho_{SE}) = 1$），并且是[厄米算符](@entry_id:153410)（$\rho_{SE} = \rho_{SE}^\dagger$）。

现在，假设一位实验者只能对子系统 $S$ 进行测量。在量子力学中，对 $S$ 的任意[可观测量](@entry_id:267133)都由一个作用在 $\mathcal{H}_S$ 上的[厄米算符](@entry_id:153410) $A_S$ 表示。要在复合系统中测量这个量，相应的算符应为 $A_S \otimes I_E$，其中 $I_E$ 是环境希尔伯特空间 $\mathcal{H}_E$ 上的恒等算符。根据玻恩法则，该测量的[期望值](@entry_id:150961)为：

$$
\langle A_S \rangle = \mathrm{Tr}_{SE}((A_S \otimes I_E) \rho_{SE})
$$

其中 $\mathrm{Tr}_{SE}$ 表示在整个复合空间 $\mathcal{H}_S \otimes \mathcal{H}_E$ 上取迹。

这个表达式虽然准确，但却依赖于完整的联合态 $\rho_{SE}$，这通常是难以获知或处理的。我们希望能找到一个只作用于 $\mathcal{H}_S$ 的算符，我们称之为 $\rho_S$，它能够完全等价地给出所有局域可观测量 $A_S$ 的[期望值](@entry_id:150961)。换言之，我们寻求一个满足以下条件的算符 $\rho_S$：

$$
\langle A_S \rangle = \mathrm{Tr}_S(A_S \rho_S)
$$

对所有作用于 $\mathcal{H}_S$ 的算符 $A_S$ 都成立。

结合这两个[期望值](@entry_id:150961)表达式，我们得到了 $\rho_S$ 的核心定义关系：

$$
\mathrm{Tr}_S(A_S \rho_S) = \mathrm{Tr}_{SE}((A_S \otimes I_E) \rho_{SE}) \quad \forall A_S \in \mathcal{L}(\mathcal{H}_S)
$$

其中 $\mathcal{L}(\mathcal{H}_S)$ 是 $\mathcal{H}_S$ 上所有线性算符构成的空间。

在有限维希尔伯特空间中，算符空间本身构成一个希尔伯特空间，其[内积](@entry_id:750660)（[希尔伯特-施密特内积](@entry_id:190429)）为 $\langle X, Y \rangle_{\mathrm{HS}} = \mathrm{Tr}(X^\dagger Y)$。这种[内积](@entry_id:750660)是非简并的，这意味着如果对所有 $X$，$\mathrm{Tr}(XY) = 0$ 都成立，那么必然有 $Y=0$。利用这一点，可以证明满足上述定义关系的算符 $\rho_S$ 不仅存在，而且是**唯一**的 。

更重要的是，这个唯一存在的算符 $\rho_S$ 本身就是一个合法的[密度算符](@entry_id:138151)。我们可以通过选择特定的 $A_S$ 来验证这一点：
1.  **单位迹**：选择 $A_S = I_S$（$\mathcal{H}_S$ 上的恒等算符）。定义关系式变为 $\mathrm{Tr}_S(I_S \rho_S) = \mathrm{Tr}_{SE}((I_S \otimes I_E) \rho_{SE})$。左边即为 $\mathrm{Tr}_S(\rho_S)$，右边是 $\mathrm{Tr}_{SE}(\rho_{SE})$，而已知后者为 $1$。因此，$\mathrm{Tr}_S(\rho_S) = 1$。
2.  **正半定性**：为了证明 $\rho_S \ge 0$，我们需要说明对 $\mathcal{H}_S$ 中的任意态 $|\psi\rangle$，都有 $\langle\psi|\rho_S|\psi\rangle \ge 0$。我们可以选择 $A_S = |\psi\rangle\langle\psi|$，这是一个[投影算符](@entry_id:154142)，因此是正半定的。代入定义关系式，左边为 $\mathrm{Tr}_S(|\psi\rangle\langle\psi| \rho_S) = \langle\psi|\rho_S|\psi\rangle$。右边为 $\mathrm{Tr}_{SE}((|\psi\rangle\langle\psi| \otimes I_E) \rho_{SE})$。由于 $|\psi\rangle\langle\psi|$ 和 $I_E$ 都是正定算符，它们的[张量积](@entry_id:140694) $(|\psi\rangle\langle\psi| \otimes I_E)$ 也是正定算符。两个正定算符的乘积的迹是非负的，因此右边 $\ge 0$。于是我们证明了 $\langle\psi|\rho_S|\psi\rangle \ge 0$，即 $\rho_S$ 是正半定的。

这一结论至关重要：无论联合态 $\rho_{SE}$ 是乘积态、[经典关联](@entry_id:136367)态还是[纠缠态](@entry_id:152310)，总存在一个唯一的、合法的[密度算符](@entry_id:138151) $\rho_S$ 能够完美再现所有局域测量的结果 。任何两个不同的联合态 $\rho_{SE}$ 和 $\sigma_{SE}$，只要它们产生相同的[约化密度算符](@entry_id:190449) $\rho_S = \sigma_S$，那么对于任何仅限于在子系统 $S$ 上（包括引入辅助系统进行测量）的操作，它们都是不可区分的 。因此，$\rho_S$ 是描述子系统 $S$ 的完备[状态表示](@entry_id:141201)。从环境 $E$ 中“迹出”（tracing out）自由度的过程，在数学上和操作上都是合理且必要的。

### [偏迹](@entry_id:146482)：定义与计算

将[联合态密度](@entry_id:143002)算符 $\rho_{SE}$ 映射到[约化密度算符](@entry_id:190449) $\rho_S$ 的数学操作被称为**[偏迹](@entry_id:146482)（partial trace）**，记作 $\mathrm{Tr}_E$。因此，我们可以简洁地写成：

$$
\rho_S = \mathrm{Tr}_E(\rho_{SE})
$$

这个映射是唯一的[线性映射](@entry_id:185132)，满足前面给出的定义关系式 。为了进行具体计算，我们可以引入基矢。设 $\{|i\rangle_S\}$ 和 $\{|\alpha\rangle_E\}$ 分别是 $\mathcal{H}_S$ 和 $\mathcal{H}_E$ 的一组[标准正交基](@entry_id:147779)。$\rho_S$ 的矩阵元可以通过以下方式计算：

$$
\langle i | \rho_S | j \rangle = \sum_{\alpha} \langle i, \alpha | \rho_{SE} | j, \alpha \rangle
$$

这里 $|i, \alpha\rangle$ 是 $|i\rangle_S \otimes |\alpha\rangle_E$ 的简写。这个公式的物理意义是：为了得到系统 $S$ 在态 $|i\rangle$ 和 $|j\rangle$ 之间的相[干性](@entry_id:900268)（矩阵元），我们需要将联合态中所有与环境态 $|\alpha\rangle$ “对角”的相应[矩阵元](@entry_id:186505)相加，即对环境的所有可能性进行求和。这个定义是独立于我们为环境选择的具体[基矢](@entry_id:199546)的 。

这个过程与经典概率论中的**[边缘化](@entry_id:264637)（marginalization）**有着深刻的类比。考虑一个具有联合概率分布 $p(s, e)$ 的经典系统。如果我们只对变量 $s$ 感兴趣，我们会通过对所有可能的 $e$ 求和来计算边缘概率分布：$p_S(s) = \sum_e p(s, e)$。如果一个量子态 $\rho_{SE}$ 恰好在某个乘积基 $\{|s, e\rangle\}$ 上是对角的，即 $\rho_{SE} = \sum_{s,e} p(s,e) |s,e\rangle\langle s,e|$，那么它的[约化密度算符](@entry_id:190449) $\rho_S$ 也会是对角的，其对角元恰好就是经典边缘概率 $\sum_e p(s,e)$ 。因此，[偏迹](@entry_id:146482)可以被视为量子世界中对我们不感兴趣或无法访问的自由度求和的推广。

在实际计算中，若密度算符 $\rho_{SE}$ 以一个 $(d_S d_E) \times (d_S d_E)$ 的矩阵形式给出（其中 $d_S, d_E$ 分别是 $\mathcal{H}_S, \mathcal{H}_E$ 的维度），[偏迹](@entry_id:146482)有非常直观的计算方法。假设矩阵索引遵循[行主序](@entry_id:634801)，即复合索引 $r = i \cdot d_E + \alpha$，$c = j \cdot d_E + \beta$。那么计算 $\rho_S$ 的 $(i,j)$ 元就等于对 $\rho_{SE}$ 的相应子块求迹 ：
1.  **[分块矩阵](@entry_id:148435)观点**：将 $\rho_{SE}$ 视为一个 $d_S \times d_S$ 的[分块矩阵](@entry_id:148435)，其中每个块 $B_{ij}$ 是一个 $d_E \times d_E$ 的子矩阵。$\rho_S$ 的第 $(i,j)$ 个矩阵元就是子块 $B_{ij}$ 的迹，即 $(\rho_S)_{ij} = \mathrm{Tr}(B_{ij}) = \sum_{\alpha} (B_{ij})_{\alpha\alpha}$。
2.  **张量重塑观点**：将该 $(d_S d_E) \times (d_S d_E)$ 矩阵重塑为一个[四阶张量](@entry_id:181350) $T_{i\alpha, j\beta}$。然后，通过对两个[环境指标](@entry_id:185137)求和并要求它们相等（即[张量缩并](@entry_id:193373)），可以得到 $\rho_S$ 的矩阵元：$(\rho_S)_{ij} = \sum_{\alpha} T_{i\alpha, j\alpha}$。

这两种方法在数学上是等价的，为从抽象定义到具体计算提供了桥梁 。

### 约化态与偏[迹映射](@entry_id:194370)的性质

#### 偏[迹映射](@entry_id:194370)的数学特性

作为从 $\mathcal{L}(\mathcal{H}_S \otimes \mathcal{H}_E)$ 到 $\mathcal{L}(\mathcal{H}_S)$ 的一个映射，[偏迹](@entry_id:146482) $\mathrm{Tr}_E$ 具有一系列关键的数学性质，这些性质保证了它在物理上的合理性。
- **线性（Linearity）**：$\mathrm{Tr}_E(aX + bY) = a\mathrm{Tr}_E(X) + b\mathrm{Tr}_E(Y)$。
- **保迹性（Trace-preserving）**：$\mathrm{Tr}_S(\mathrm{Tr}_E(X)) = \mathrm{Tr}_{SE}(X)$。这意味着如果 $\rho_{SE}$ 的迹为1，那么 $\rho_S$ 的迹也为1。
- **保持[厄米性](@entry_id:141899)（Hermiticity-preserving）**：如果 $X$ 是[厄米算符](@entry_id:153410)，那么 $\mathrm{Tr}_E(X)$ 也是[厄米算符](@entry_id:153410) 。
- **[完全正性](@entry_id:149274)（Completely Positive, CP）**：这个性质比简单的正性（即 $X \ge 0 \implies \mathrm{Tr}_E(X) \ge 0$）更强。它要求即使在偏[迹映射](@entry_id:194370)上附加一个任意维度的[辅助系统](@entry_id:142219)（即考虑映射 $\mathrm{Tr}_E \otimes I_A$），该扩展映射仍然保持正性。这确保了该操作在与任何未参与的旁观系统结合时仍然是物理上可能的。

综合来看，[偏迹](@entry_id:146482)是一个**完全正的保迹（Completely Positive and Trace-Preserving, CPTP）**映射 。CPTP 映射是描述[开放量子系统](@entry_id:138632)动力学的数学基石，而[偏迹](@entry_id:146482)是这类映射中最基本、最典型的例子。

值得注意的是，虽然正的输入保证了正的输出，但一个非正定的输入 $X$ 经过[偏迹](@entry_id:146482)后，其输出 $\mathrm{Tr}_E(X)$ 可能是正定的、非正定的，甚至是零算符。然而，其[逆否命题](@entry_id:265332)是成立的：如果 $\mathrm{Tr}_E(X)$ 具有负特征值，那么 $X$ 必然不是正半定的 。

#### 纯度、纠缠与熵

[约化密度算符](@entry_id:190449)的一个核心应用是量化和理解[量子纠缠](@entry_id:136576)。一个关键指标是**纯度（purity）**，定义为 $\mathcal{P}(\rho) = \mathrm{Tr}(\rho^2)$。
- 对于一个[纯态](@entry_id:141688) $\rho = |\psi\rangle\langle\psi|$，其纯度为 $\mathcal{P}(\rho)=1$。
- 对于一个混态，其纯度满足 $1/d \le \mathcal{P}(\rho)  1$，其中 $d$ 是希尔伯特空间的维度。纯度最小的值 $1/d$ 对应于**最大混态** $\rho = I/d$。
- 一个[密度算符](@entry_id:138151)代表[纯态](@entry_id:141688)的充要条件是其纯度为1 。

当一个复合系统 $S+E$ 处于纯态 $|\Psi\rangle$ 时，其子系统 $S$ 的状态 $\rho_S = \mathrm{Tr}_E(|\Psi\rangle\langle\Psi|)$ 的性质直接反映了 $S$ 与 $E$ 之间的纠缠。
让我们看一个典范性的例子：一个由两个量子比特组成的系统，处于[贝尔态](@entry_id:140749) $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$。这是一个最大纠缠[纯态](@entry_id:141688)。通过直接计算，我们可以求得子系统 $S$ 的[约化密度算符](@entry_id:190449) ：

$$
\rho_S = \mathrm{Tr}_E(|\Phi^+\rangle\langle\Phi^+|) = \frac{1}{2}|0\rangle\langle 0| + \frac{1}{2}|1\rangle\langle 1| = \frac{1}{2}I_S
$$

这是一个最大混态！这个结果揭示了一个深刻的量子现象：即使整个系统的信息是完全已知的（处于纯态），但由于纠缠，关于其任何一个局域子系统的信息可以是完全未知的。该子系统表现得像一个完全随机的[统计系综](@entry_id:149738)。这种从一个全局纯态中产生的混态是[量子纠缠](@entry_id:136576)的直接标志。

这个现象可以用**[冯·诺依曼熵](@entry_id:143216)（von Neumann entropy）**来量化，其定义为 $S(\rho) = -\mathrm{Tr}(\rho \ln \rho)$。它度量了我们对一个量子态的无知程度。对于[纯态](@entry_id:141688)，熵为零。对于上述[贝尔态](@entry_id:140749)的例子，$S(\rho_{SE})=0$，但 $S(\rho_S) = \ln 2$，是[两能级系统](@entry_id:196082)的[最大熵](@entry_id:156648)。这种由于纠缠而产生的熵被称为**[纠缠熵](@entry_id:140818)（entropy of entanglement）** 。

### [施密特分解](@entry_id:145934)与纠缠的量化

对于任意一个纯态 $|\Psi\rangle \in \mathcal{H}_S \otimes \mathcal{H}_E$，**[施密特分解](@entry_id:145934)定理（Schmidt decomposition theorem）**提供了一个强大的分析工具。该定理指出，总可以找到 $\mathcal{H}_S$ 的一组[标准正交基](@entry_id:147779) $\{|s_k\rangle\}$ 和 $\mathcal{H}_E$ 的一组[标准正交基](@entry_id:147779) $\{|e_k\rangle\}$，使得 $|\Psi\rangle$ 可以被写成如下形式：

$$
|\Psi\rangle = \sum_{k=1}^r \sqrt{p_k} |s_k\rangle \otimes |e_k\rangle
$$

其中 $p_k > 0$ 且 $\sum_k p_k = 1$。这些系数 $\sqrt{p_k}$ 被称为**[施密特系数](@entry_id:137823)**，而非零项的数目 $r$ 被称为**[施密特秩](@entry_id:154893)（Schmidt rank）**。

[施密特分解](@entry_id:145934)极大地简化了[约化密度算符](@entry_id:190449)的计算。对处于上述[施密特分解](@entry_id:145934)形式的 $|\Psi\rangle$ 取[偏迹](@entry_id:146482)，我们立即得到 $\rho_S$ 和 $\rho_E$ 的[谱分解](@entry_id:173707)：

$$
\rho_S = \sum_{k=1}^r p_k |s_k\rangle\langle s_k| \quad \text{and} \quad \rho_E = \sum_{k=1}^r p_k |e_k\rangle\langle e_k|
$$

这个结果带来了一系列重要的推论  ：
1.  对于任何纯的二体态，其两个子系统的[约化密度算符](@entry_id:190449) $\rho_S$ 和 $\rho_E$ 具有**完全相同的非零[特征值谱](@entry_id:1124216)** $\{p_k\}$。
2.  因此，它们的纯度相等 $\mathrm{Tr}(\rho_S^2) = \mathrm{Tr}(\rho_E^2) = \sum_k p_k^2$，[冯·诺依曼熵](@entry_id:143216)也相等 $S(\rho_S) = S(\rho_E)$。
3.  $\rho_S$ 的秩等于[施密特秩](@entry_id:154893) $r$。
4.  一个纯的二体态是**可分离的（separable）**（即可以写成乘积态 $|\Psi\rangle = |\phi_S\rangle \otimes |\phi_E\rangle$）的充要条件是其[施密特秩](@entry_id:154893)为 $1$。这等价于其[约化密度算符](@entry_id:190449) $\rho_S$ 是一个纯态（即 $\mathrm{rank}(\rho_S)=1$ 或 $\mathrm{Tr}(\rho_S^2)=1$）。

因此，[约化密度算符](@entry_id:190449)的谱性质为我们提供了一个直接的、可计算的[纠缠度量](@entry_id:139894)。[施密特秩](@entry_id:154893)大于 $1$ 意味着纠缠的存在，而特征值 $\{p_k\}$ 的分布则量化了纠缠的程度。一个接近均匀的分布（如最大[纠缠态](@entry_id:152310)）对应于高度混合的约化态和大量的[纠缠熵](@entry_id:140818)。

### 在[开放量子系统](@entry_id:138632)中的应用：动力学与[退相干](@entry_id:145157)

[偏迹](@entry_id:146482)在描述**开放量子系统（open quantum systems）**的动力学中扮演着核心角色。在这种情景下，系统 $S$ 与一个大的环境 $E$（如[热浴](@entry_id:137040)）相互作用。总的系统 $S+E$ 的演化是幺正的，由某个总[哈密顿量](@entry_id:144286) $H_{SE}$ 支配：$\rho_{SE}(t) = U(t)\rho_{SE}(0)U^\dagger(t)$，其中 $U(t) = \exp(-iH_{SE}t)$。然而，我们通常只对系统 $S$ 的动力学感兴趣，这可以通过在每一步都取[偏迹](@entry_id:146482)得到：

$$
\rho_S(t) = \mathrm{Tr}_E(\rho_{SE}(t)) = \mathrm{Tr}_E(U(t)\rho_{SE}(0)U^\dagger(t))
$$

如果系统和环境初始不相关，即 $\rho_{SE}(0) = \rho_S(0) \otimes \rho_E(0)$，那么从初始系统态 $\rho_S(0)$ 到时刻 $t$ 的系统态 $\rho_S(t)$ 的映射定义了一个**量子动力学映射（quantum dynamical map）** $\Lambda_t$。

这个过程的一个关键物理效应是**退相干（decoherence）**。退相干是指系统的量子相干性（由[密度矩阵](@entry_id:139892)的非对角元素表示）由于与环境的纠缠而逐渐消失的过程。考虑一个简单的模型 ，一个量子比特 $S$ 初始处于叠加态 $(|0\rangle+|1\rangle)/\sqrt{2}$，并与一个环境比特 $E$ 发生纯粹的去相位相互作用。演化后，系统 $S$ 的[约化密度矩阵](@entry_id:146315)的非对角元素会被一个依赖于时间的因子 $\gamma(t)$ 衰减。这个[衰减因子](@entry_id:1121239)的大小 $| \gamma(t) |$ 直接量化了相[干性](@entry_id:900268)的保持程度。

通过计算可以发现，随着相[干性](@entry_id:900268) $| \gamma(t) |$ 的减小，系统 $S$ 的[冯·诺依曼熵](@entry_id:143216) $S(\rho_S(t))$ 会相应地增加 。这描绘了一幅清晰的物理图像：系统 $S$ 最初拥有的量子信息（相[干性](@entry_id:900268)）通过与环境的相互作用“泄漏”到 $S-E$ 的关联中。从局域的 $S$ 视角来看，这种信息的丢失表现为熵的增加和态的混合化。

#### 高级主题：超越简单动力学

虽然上述基于初始不相关假设的模型非常有用，但更复杂的情况也时常出现。
- **初始关联**：如果系统与环境在演化开始时就存在关联，那么从 $\rho_S(0)$ 到 $\rho_S(t)$ 的映射就不再是唯一的，它会依赖于初始关联的具体形式。在这种情况下，一个普适的量子动力学映射 $\Lambda_t$ 可能根本不存在。某些理论上构造的初始关联甚至可以导致一个等效的动力学映射不是完全正的，这表明它不能被视为一个普适的物理过程 。例如，著名的转置映射（transpose map）就是这样一个非完全正的映射，它可以被形式化地构造出来，但不能代表一个物理上可实现的演化。

- **[非马尔可夫动力学](@entry_id:142796)与[CP可分性](@entry_id:137495)**：当环境具有“结构”（例如，有限的、或具有离散[能谱](@entry_id:181780)）时，从系统流失到环境中的信息可能会在稍后部分地“流回”到系统中，导致相[干性](@entry_id:900268)的短暂恢复（recoherence）。这种现象被称为**非马尔可夫效应**。一个标记马尔可夫（无记忆）动力学的数学标准是**[CP可分性](@entry_id:137495)（CP-divisibility）**。一个动力学映射族 $\{\Lambda_{t,0}\}$ 被称为CP可分的，如果对于任意 $t \ge s \ge 0$，总演化可以分解为 $\Lambda_{t,0} = \Lambda_{t,s} \circ \Lambda_{s,0}$，其中中间映射 $\Lambda_{t,s}$ 本身也是一个[CPTP映射](@entry_id:143017)。在发生[信息回流](@entry_id:146865)的[非马尔可夫过程](@entry_id:182857)中，可以发现存在某些时间间隔使得 $\Lambda_{t,s}$ 不是完全正的，从而破坏了[CP可分性](@entry_id:137495) 。这为我们从数学上精确定义和探测[量子动力学](@entry_id:138183)中的记忆效应提供了途径。

总之，[约化密度算符](@entry_id:190449)和[偏迹](@entry_id:146482)不仅是描述量子子系统的基本工具，也是探索[量子纠缠](@entry_id:136576)、退相干以及更复杂的非马尔可夫开放[系统动力学](@entry_id:136288)的理论基石。