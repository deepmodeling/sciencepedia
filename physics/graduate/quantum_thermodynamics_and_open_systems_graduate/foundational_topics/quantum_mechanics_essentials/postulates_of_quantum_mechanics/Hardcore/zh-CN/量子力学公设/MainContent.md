## 引言
量子力学是二十世纪最伟大的[科学革命](@entry_id:919172)之一，它从根本上重塑了我们对物理实在的理解，并为现代技术（从激光到晶体管再到量子计算）奠定了理论基石。与经典物理的直观确定性不同，微观世界遵循一套奇异而深刻的规则。这些规则并非零散的发现，而是可以从一个严谨、自洽的公理化体系——量子力学的基本公设——中逻辑地推导出来。这些公设为描述量子现象提供了统一的数学语言，解决了经典理论无法解释的原子稳定性、[黑体辐射](@entry_id:137223)等难题。

本文旨在系统地剖析这些核心公设，揭示它们如何共同构筑起整个[量子理论](@entry_id:145435)的宏伟大厦。在“原理与机制”一章中，我们将深入探讨量子态的数学表示、可观测量的本质、测量的概率性以及系统的动力学演化。随后，在“应用与跨学科连接”一章中，我们将展示这些抽象的公设如何在量子化学、量子热力学和量子信息等前沿领域中转化为强大的预测和分析工具。最后，“动手实践”部分将提供一系列精心设计的问题，帮助您将理论知识应用于具体计算，从而巩固对这些基本原理的掌握。通过本次学习，您将对量子世界的运作方式建立起一个坚实而深刻的理解。

## 原理与机制

量子力学的理论框架建立在一系列基本公设之上。这些公设不仅为量子现象提供了数学语言，也深刻地塑造了我们对物理实在的理解。本章旨在系统地阐述这些核心原理与机制，从量子态的描述、可观测量的本质，到测量过程与系统演化，最终延伸至复合系统与对称性的深刻内涵。我们将以一种严谨且内在逻辑一致的方式，揭示这些公设如何共同构建起整个量子理论的大厦。

### 量子系统的状态

描述一个物理系统的第一步是定义其“状态”。在量子力学中，状态的概念远比经典力学中的位置与动量更为抽象和丰富。

#### 纯态、[希尔伯特空间](@entry_id:261193)与[叠加原理](@entry_id:144649)

量子力学的第一个基本公设断言，一个孤立量子系统的所有可能**纯态 (pure states)** 都与一个复数、可分离的**希尔伯特空间 (Hilbert space)** $\mathcal{H}$ 中的“射线”一一对应。一条**射线 (ray)** 是指由一个非[零矢量](@entry_id:155273) $| \psi \rangle \in \mathcal{H}$ 生成的[等价类](@entry_id:156032)，其中包含了所有与 $| \psi \rangle$ 相差一个非零复数标量乘子的矢量，即 $\{c|\psi\rangle : c \in \mathbb{C} \setminus \{0\}\}$。

这一表述的物理含义是，两个矢量 $| \psi \rangle$ 和 $| \phi \rangle = c | \psi \rangle$ (其中 $c \neq 0$) 代表的是同一个物理状态。为何如此？答案在于所有物理预测的计算方式。例如，一个[可观测量](@entry_id:267133) $A$ 在状态 $| \psi \rangle$ 中的[期望值](@entry_id:150961)由下式给出：
$$
\langle A \rangle = \frac{\langle\psi|A|\psi\rangle}{\langle\psi|\psi\rangle}
$$
若我们将 $| \psi \rangle$ 替换为 $| \phi \rangle = c | \psi \rangle$，[期望值](@entry_id:150961)变为：
$$
\langle A \rangle_{\phi} = \frac{\langle c\psi|A|c\psi\rangle}{\langle c\psi|c\psi\rangle} = \frac{c^*c\langle\psi|A|\psi\rangle}{c^*c\langle\psi|\psi\rangle} = \frac{|c|^2\langle\psi|A|\psi\rangle}{|c|^2\langle\psi|\psi\rangle} = \frac{\langle\psi|A|\psi\rangle}{\langle\psi|\psi\rangle} = \langle A \rangle_{\psi}
$$
由于 $c \neq 0$，因子 $|c|^2$ 可以从分子和分母中约去，使得[期望值](@entry_id:150961)保持不变。同样的道理适用于所有通过玻恩定则计算的概率。因此，所有可观测的物理量都对这种[标量乘法](@entry_id:155971)不敏感。

习惯上，我们通常选择归一化的矢量来代表一个[纯态](@entry_id:141688)，即满足 $\langle\psi|\psi\rangle = 1$ 的矢量。在这种约定下，描述同一纯态的两个归一化矢量 $| \psi \rangle$ 和 $| \phi \rangle$ 之间的关系简化为 $| \phi \rangle = e^{i\theta} | \psi \rangle$，其中 $e^{i\theta}$ 是一个相位因子，$\theta \in \mathbb{R}$。这个相位 $e^{i\theta}$ 被称为**[全局相位](@entry_id:147947) (global phase)**。[全局相位](@entry_id:147947)的不可观测性是量子力学的一个基本特征 。

希尔伯特空间的线性矢量空间结构直接导出了量子力学中最具革命性的概念之一：**叠加原理 (superposition principle)**。如果 $| \psi_1 \rangle$ 和 $| \psi_2 \rangle$ 是系统可能存在的两个状态，那么它们的任意[线性组合](@entry_id:154743) $| \psi \rangle = c_1 | \psi_1 \rangle + c_2 | \psi_2 \rangle$ (其中 $c_1, c_2$ 是复数，且整体归一化后) 也代表了一个系统可能存在的、物理上截然不同的状态。这种新状态并非经典意义上系统“部分处于” $| \psi_1 \rangle$ 状态、“部分处于” $| \psi_2 \rangle$ 状态的混合，而是一种全新的量子实在。

#### 混合态与[密度算符](@entry_id:138151)

[纯态](@entry_id:141688)描述的是我们对系统拥有最大可能信息的理想情况。然而，在许多现实场景中，例如当系统与环境发生纠缠，或者当我们对系统的制备过程只有统计性知识时，我们需要一个更普适的描述方式。这就是**[密度算符](@entry_id:138151) (density operator)**，或称[密度矩阵](@entry_id:139892) $\rho$。

第二个公设推广了状态的概念：一个量子系统的状态由[希尔伯特空间](@entry_id:261193) $\mathcal{H}$ 上的一个**[密度算符](@entry_id:138151)** $\rho$ 来描述。密度算符是满足以下三个条件的算符：
1.  **[厄米性](@entry_id:141899) (Hermiticity)**: $\rho = \rho^{\dagger}$
2.  **正半定性 (Positive semi-definiteness)**: $\langle \phi | \rho | \phi \rangle \ge 0$ 对所有 $|\phi\rangle \in \mathcal{H}$ 成立。
3.  **归一化 (Normalization)**: $\mathrm{Tr}(\rho) = 1$

纯态是密度算符 formalism 的一个特例。对于一个由归一化矢量 $|\psi\rangle$ 描述的[纯态](@entry_id:141688)，其[密度算符](@entry_id:138151)是一个秩为1的投影算符：$\rho = |\psi\rangle\langle\psi|$。使用[密度算符](@entry_id:138151)的好处之一在于，它自然地消除了[全局相位](@entry_id:147947)的不确定性，因为 $|e^{i\theta}\psi\rangle\langle e^{i\theta}\psi| = |\psi\rangle\langle\psi|$ 。

如果一个系统不能被描述为一个[纯态](@entry_id:141688)，则称其处于**混合态 (mixed state)**。一个混合态可以看作是多个纯态 $\rho_i = |\psi_i\rangle\langle\psi_i|$ 的统计系综，其密度算符为 $\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i|$，其中 $p_i$ 是制备出[纯态](@entry_id:141688) $|\psi_i\rangle$ 的经典概率，满足 $p_i \ge 0$ 和 $\sum_i p_i = 1$。根据[谱定理](@entry_id:136620)，任何[密度算符](@entry_id:138151)都可以写成这种形式，其中 $|\psi_i\rangle$ 是其本征矢量。

区分[纯态](@entry_id:141688)和混合态的一个重要指标是**纯度 (purity)**，定义为 $\mathcal{P} = \mathrm{Tr}(\rho^2)$。
- 对于[纯态](@entry_id:141688) $\rho = |\psi\rangle\langle\psi|$，我们有 $\rho^2 = (|\psi\rangle\langle\psi|)(|\psi\rangle\langle\psi|) = |\psi\rangle\langle\psi| = \rho$。因此，$\mathrm{Tr}(\rho^2) = \mathrm{Tr}(\rho) = 1$。
- 对于[混合态](@entry_id:141568)，其纯度总是小于1。

在一个维度为 $d$ 的有限维希尔伯特空间中，纯度有一个明确的范围：$\frac{1}{d} \le \mathrm{Tr}(\rho^2) \le 1$。纯度达到上界 $1$ 当且仅当该状态是纯态。纯度达到下界 $\frac{1}{d}$ 当且仅当该状态是**[最大混合态](@entry_id:137775) (maximally mixed state)** $\rho = \frac{I}{d}$，它代表了我们对系统信息最无知的状态 。

必须强调**[相干叠加](@entry_id:170209) (coherent superposition)** 与**统计混合 (statistical mixture)** 的根本区别 。考虑一个二维系统（量子比特），基态为 $|0\rangle$ 和 $|1\rangle$。
- 一个[相干叠加](@entry_id:170209)态，例如 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$，其[密度矩阵](@entry_id:139892)为 $\rho_{sup} = |+\rangle\langle+| = \frac{1}{2}\begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix}$。
- 一个统计[混合态](@entry_id:141568)，以 $50\%$ 的概率处于 $|0\rangle$， $50\%$ 的概率处于 $|1\rangle$，其[密度矩阵](@entry_id:139892)为 $\rho_{mix} = \frac{1}{2}|0\rangle\langle0| + \frac{1}{2}|1\rangle\langle1| = \frac{1}{2}\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}$。

$\rho_{sup}$ 中的非对角元素（$\rho_{01}, \rho_{10}$）被称为**相干项 (coherences)**，它们是[量子干涉](@entry_id:139127)效应的来源。例如，测量[泡利算符](@entry_id:144061) $\sigma_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$ 的[期望值](@entry_id:150961)：
- 对于叠加态：$\langle\sigma_x\rangle_{sup} = \mathrm{Tr}(\rho_{sup} \sigma_x) = 1$。
- 对于[混合态](@entry_id:141568)：$\langle\sigma_x\rangle_{mix} = \mathrm{Tr}(\rho_{mix} \sigma_x) = 0$。
这个显著的差异表明，叠加态和混合态是截然不同的物理状态，尽管它们在 $\{|0\rangle, |1\rangle\}$ 基上的布居数（对角元素）完全相同。在布洛赫球的几何图像中，所有[纯态](@entry_id:141688)都位于球面，而混合态则位于球内。上述的 $|+\rangle$ 态位于球面上，而 $\rho_{mix}$ 则位于球心。

### 可观测量与测量

量子态本身是不可直接观测的。我们通过测量物理量（[可观测量](@entry_id:267133)）来获取关于系统的信息。

#### 作为自伴算符的可观测量

第三个公设是关于可观测量的数学表示。它规定：每一个物理**[可观测量](@entry_id:267133) (observable)**都对应于希尔伯特空间 $\mathcal{H}$ 上的一个**自伴算符 (self-adjoint operator)**。

对于有限维[希尔伯特空间](@entry_id:261193)，自伴算符与我们更熟悉的[厄米矩阵](@entry_id:155147)是等价的。然而，在[无穷维空间](@entry_id:141268)中（例如描述一个粒子的位置或动量），这个区分至关重要。一个算符 $A$ 是对称的（或厄米的），如果对于其定义域 $\mathcal{D}(A)$ 内的所有 $|\psi\rangle, |\phi\rangle$，都有 $\langle\psi|A|\phi\rangle = \langle A\psi|\phi\rangle$。一个算符是自伴的，如果它不仅是对称的，而且其定义域与其伴随算符 $A^\dagger$ 的定义域相同，即 $A=A^\dagger$ 且 $\mathcal{D}(A) = \mathcal{D}(A^\dagger)$。

为何要求自伴性而非仅仅对称性？ 原因在于，只有自伴算符才能保证拥有完备的、定义在[实数轴](@entry_id:147286) $\mathbb{R}$ 上的[谱理论](@entry_id:275351)。**[谱定理](@entry_id:136620) (spectral theorem)** 是这一公设的数学核心，它断言任何自伴算符 $A$ 都可以表示为一个谱积分：
$$
A = \int_{-\infty}^{\infty} a \, dE_A(a)
$$
这里的 $E_A$ 是一个**投影值测量 (Projection-Valued Measure, PVM)**。它为[实数轴](@entry_id:147286)上的每一个（Borel）子集 $\Delta \subseteq \mathbb{R}$ 指定一个[投影算符](@entry_id:154142) $E_A(\Delta)$。这个[谱分解](@entry_id:173707)确保了以下两点：
1.  **实数谱**：测量的结果必须是实数，这与自伴算符的谱必定是实数集相符。
2.  **完备的概率理论**：PVM $E_A$ 允许我们为任何可能的测量结果区间 $\Delta$ 计算概率，而不仅仅是单个的本征值。一个仅仅对称但非自伴的算符可能没有这样的[谱分解](@entry_id:173707)，从而无法为所有可能的测量结果赋予一致的概率解释。

#### 玻恩定则与测量统计

第四个公设，即**[玻恩定则](@entry_id:154470) (Born rule)**，将状态和[可观测量](@entry_id:267133)联系起来，给出了测量的[统计预测](@entry_id:168738)。其最普遍的形式是：
当测量由自伴算符 $A$ 代表的可观测量时，若系统处于状态 $\rho$，则测量结果落在实数集 $\Delta$ 内的概率为：
$$
\mathbb{P}(\Delta) = \mathrm{Tr}(\rho E_A(\Delta))
$$
其中 $E_A(\Delta)$ 是与 $A$ 对应的 PVM。如果 $A$ 具有[离散谱](@entry_id:150970) $\{a_i\}$，且对应的本征投影为 $\{\Pi_i\}$，则测量结果为 $a_i$ 的概率简化为更常见的形式：
$$
p(a_i) = \mathrm{Tr}(\rho \Pi_i)
$$
对于[纯态](@entry_id:141688) $\rho=|\psi\rangle\langle\psi|$，这进一步简化为 $p(a_i) = \langle\psi|\Pi_i|\psi\rangle$。

可观测量的[期望值](@entry_id:150961)则可以从谱积分中得到：
$$
\langle A \rangle = \mathrm{Tr}(\rho A) = \mathrm{Tr}\left(\rho \int a \, dE_A(a)\right) = \int a \, \mathrm{Tr}(\rho \, dE_A(a))
$$
这个表达式只有在[积分收敛](@entry_id:139742)时才有意义，这对于无界算符（如能量、位置）是一个重要的考虑 。

#### [广义测量](@entry_id:154280) (POVM)

投影测量是一种理想化的模型。在更现实的场景中，尤其是在开放量子系统和[量子信息处理](@entry_id:158111)中，测量过程本身可能更加复杂。例如，一个测量可能通过让系统与一个辅助系统（称为探针或 ancilla）相互作用，然后对探针进行投影测量来实现。

这种更一般化的测量框架由**正算符值测量 (Positive Operator-Valued Measure, POVM)** 描述 。一个 POVM 是希尔伯特空间 $\mathcal{H}$ 上的一组算符 $\{M_i\}$，它们满足：
1.  **正性**: 每个 $M_i$ 都是正半定算符，$M_i \ge 0$。
2.  **完备性**: 所有算符之和为单位算符，$\sum_i M_i = I$。

对于一个由 [POVM](@entry_id:138770) $\{M_i\}$ 描述的测量，获得结果 $i$ 的概率由[广义玻恩](@entry_id:182759)定则给出：
$$
p_i = \mathrm{Tr}(\rho M_i)
$$
[POVM](@entry_id:138770) 的元素 $M_i$ 不必是相互正交的投影算符，这使其比 PVM 更具[一般性](@entry_id:161765)。事实上，任何 PVM 都是 [POVM](@entry_id:138770) 的一个特例。POVM 的 formalism 至关重要，因为它描述了所有数学上一致且物理上可实现的[量子测量](@entry_id:272490)。例如，当一个系统经历一个由 CPTP 映射 $\Lambda$ 描述的噪声过程，然后对其进行一个由 PVM $\{E_A(\Delta)\}$ 定义的投影测量时，对初始状态 $\rho$ 而言，整个过程等效于一个由 [POVM](@entry_id:138770) $\{\Lambda^*(E_A(\Delta))\}$ 描述的[广义测量](@entry_id:154280) 。

#### [测量后状态](@entry_id:148034)

测量不仅揭示了信息，通常还会改变系统的状态。这就是所谓的“波包塌缩”。对于一个选择性的理想投影测量，如果我们获得了对应于本征值 $a$ 的结果，那么系统的后验状态由**吕德斯定则 (Lüders' rule)** 给出 ：
$$
\rho \mapsto \rho'_a = \frac{\Pi_a \rho \Pi_a}{\mathrm{Tr}(\rho \Pi_a)}
$$
其中 $\Pi_a$ 是对应于结果 $a$ 的[投影算符](@entry_id:154142)。分母 $\mathrm{Tr}(\rho \Pi_a)$ 正是获得结果 $a$ 的概率，确保了新的密度算符 $\rho'_a$ 是归一化的。

这个规则可以从更基本的原理推导出来，如测量的[可重复性](@entry_id:194541)（即刻[重复测量](@entry_id:896842)会以概率1得到相同结果）和一个“最小扰动”原则：测量不应不必要地扰动与被测 observable 相容（即对易）的其他[可观测量](@entry_id:267133)的值。吕德斯定则优于早期冯·诺依曼的投影假设，尤其是在处理简并本征值时，因为它保留了简并子空间内的相[干性](@entry_id:900268)，体现了更少的扰动。

### 动力学

量子系统的状态如何随时间演化？动力学公设对此给出了回答，并区分了孤立（封闭）系统和与环境相互作用的（开放）系统。

#### [封闭系统](@entry_id:139565)的演化

第五个公设描述了**封闭量子系统 (closed quantum system)** 的动力学。它指出，一个[封闭系统](@entry_id:139565)的时间演化是由一个**幺正变换 (unitary transformation)** 描述的。具体来说，从时间 $t_1$ 到 $t_2$ 的状态演化由一个幺正算符 $U(t_2, t_1)$ 实现：
$$
|\psi(t_2)\rangle = U(t_2, t_1) |\psi(t_1)\rangle \quad \text{或} \quad \rho(t_2) = U(t_2, t_1) \rho(t_1) U(t_2, t_1)^\dagger
$$
对于时间无关的[哈密顿量](@entry_id:144286) $H$ 的系统，演化是时齐的，即 $U(t_2, t_1)$ 只依赖于时间间隔 $t = t_2 - t_1$。从可逆性、时齐性和连续性等物理原则出发，可以证明[演化算符](@entry_id:182628)族 $\{U(t)\}$ 构成一个**强连续单参数幺正群** 。

**[斯通定理](@entry_id:262301) (Stone's theorem)** 在此起到了关键作用。它保证了对于每一个这样的幺正群，都存在一个唯一的自伴算符 $H$（称为[群的生成元](@entry_id:137215)），使得：
$$
U(t) = \exp\left(-\frac{iHt}{\hbar}\right)
$$
这个生成元 $H$ 就是系统的**哈密顿算符 (Hamiltonian)**。[幺正演化](@entry_id:145020)的微分形式就是著名的**薛定谔方程 (Schrödinger equation)**：
$$
i\hbar \frac{d}{dt}|\psi(t)\rangle = H|\psi(t)\rangle
$$
对于密度算符，其[演化方程](@entry_id:268137)称为**刘维尔-[冯·诺依曼方程](@entry_id:153472) (Liouville-von Neumann equation)**：
$$
i\hbar \frac{d\rho}{dt} = [H, \rho]
$$
为了确保物理上合理的[哈密顿量](@entry_id:144286)能够生成一个合法的[幺正演化](@entry_id:145020)，证明其自伴性是至关重要的一步。例如，对于包含库仑相互作用的分子[哈密顿量](@entry_id:144286)，可以通过**Kato-Rellich 定理**等数学工具来严格证明其自伴性，从而保证了其生成的动力学是良定义的 。

#### [开放系统](@entry_id:147845)的演化

现实世界中的量子系统很少是完全孤立的。它们不可避免地与周围的广阔**环境 (environment)** 相互作用，成为**开放量子系统 (open quantum system)**。这种相互作用导致了退相干、弛豫和耗散等非幺正现象。

在**[马尔可夫近似](@entry_id:1127636) (Markovian approximation)** 下，我们假设环境很大且关联时间很短，以至于它没有“记忆”，系统在任意时刻的演化只依赖于当前状态。在这种情况下，系统的动力学由一个**[量子动力学半群](@entry_id:1130394) (quantum dynamical semigroup)** 描述。这是一个满足[半群性质](@entry_id:271012) $\mathcal{T}_{t+s} = \mathcal{T}_t \circ \mathcal{T}_s$ (对 $t,s \ge 0$) 的**完全正定保迹 (Completely Positive Trace-Preserving, CPTP)** 映射族 $\{\mathcal{T}_t\}_{t \ge 0}$ 。

与幺正群类似，这样的[半群](@entry_id:153860)也有一个生成元，通常记为 $\mathcal{L}$，称为**[刘维尔超算符](@entry_id:1127322) (Liouvillian super-operator)**。系统的密度算符演化遵循一个**主方程 (master equation)**：
$$
\frac{d\rho}{dt} = \mathcal{L}(\rho)
$$
Gorini、Kossakowski、Sudarshan 和 Lindblad证明，任何生成 CPTP [半群](@entry_id:153860)的[刘维尔算符](@entry_id:201034) $\mathcal{L}$ 都必须具有以下一般形式，即 **GKSL 方程**或**[林德布拉德方程](@entry_id:147719) (Lindblad equation)**:
$$
\mathcal{L}(\rho) = -i[H, \rho] + \sum_k \gamma_k \left( L_k \rho L_k^\dagger - \frac{1}{2} \{L_k^\dagger L_k, \rho\} \right)
$$
其中：
- $H$ 是一个[厄米算符](@entry_id:153410)，代表系统的幺正演化部分（可能包含环境引起的能量重整化）。
- $\{L_k\}$ 是一组**林德布拉德算符 (Lindblad operators)** 或**[量子跃迁算符](@entry_id:187493) (quantum jump operators)**，描述了系统与环境之间的各种不[可逆过程](@entry_id:276625)。
- $\gamma_k \ge 0$ 是这些过程发生的速率。
- $\{A, B\} = AB + BA$ 是[反对易子](@entry_id:139754)。
第一项是刘维尔-[冯·诺依曼方程](@entry_id:153472)，描述相干演化。第二项是耗散项，描述[退相干](@entry_id:145157)、弛豫等过程。这个方程是研究[量子热力学](@entry_id:140152)、[量子光学](@entry_id:140582)和量子信息中耗散过程的基石。

### 复合系统与对称性

最后，我们需要公设来处理由多个部分组成的系统，以及对称性在量子力学中的体现。

#### [张量积](@entry_id:140694)公设与纠缠

第六个公设是关于**复合系统 (composite system)** 的。如果一个系统由两个子系统 A 和 B 组成，其希尔伯特空间分别为 $\mathcal{H}_A$ 和 $\mathcal{H}_B$，那么复合系统的希尔伯特空间是这两个空间的**[张量积](@entry_id:140694) (tensor product)**：
$$
\mathcal{H}_{AB} = \mathcal{H}_A \otimes \mathcal{H}_B
$$
如果系统 A 处于态 $|a\rangle \in \mathcal{H}_A$，系统 B 处于态 $|b\rangle \in \mathcal{H}_B$，那么复合系统的态是**积态 (product state)** $|a\rangle \otimes |b\rangle$。然而，复合系统的绝大多数态都无法写成这种简单的乘积形式。这些不能写成积态的[纯态](@entry_id:141688)被称为**[纠缠态](@entry_id:152310) (entangled states)**。

一个典型的例子是[贝尔态](@entry_id:140749) $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|0\rangle_A \otimes |0\rangle_B + |1\rangle_A \otimes |1\rangle_B)$。在这个态中，任何对子系统 A 的测量结果都与对子系统 B 的测量结果完美关联，但每个子系统本身并没有确定的状态。如果我们只关心子系统 A，它的状态需要通过对复合系统密度矩阵 $\rho_{AB} = |\Phi^+\rangle\langle\Phi^+|$ 做**[偏迹](@entry_id:146482) (partial trace)** 运算得到：$\rho_A = \mathrm{Tr}_B(\rho_{AB}) = \frac{1}{2}I_A$。这是一个[最大混合态](@entry_id:137775)，说明我们对子系统 A 的状态一无所知，尽管我们对整个复合系统的状态拥有完全的信息。

**[施密特分解](@entry_id:145934) (Schmidt decomposition)** 是分析二体纯态纠缠的有力工具 。它表明，任何二体纯态 $|\psi\rangle \in \mathcal{H}_A \otimes \mathcal{H}_B$ 都可以写成如下形式：
$$
|\psi\rangle = \sum_{k=1}^r \sqrt{\lambda_k} |u_k\rangle_A \otimes |v_k\rangle_B
$$
其中 $\{|u_k\rangle_A\}$ 和 $\{|v_k\rangle_B\}$ 分别是 $\mathcal{H}_A$ 和 $\mathcal{H}_B$ 中的一组[标准正交基](@entry_id:147779)，$\sqrt{\lambda_k}$ 是正实数，称为[施密特系数](@entry_id:137823)，满足 $\sum_k \lambda_k = 1$。
-   **[施密特秩](@entry_id:154893) (Schmidt rank)** $r$ 是求和中的项数。一个态是积态当且仅当其[施密特秩](@entry_id:154893) $r=1$。如果 $r>1$，该态就是[纠缠态](@entry_id:152310)。
-   [施密特系数](@entry_id:137823)的平方 $\lambda_k$ 恰好是[约化密度算符](@entry_id:190449) $\rho_A$ 和 $\rho_B$ 的非零本征值。
-   **[纠缠熵](@entry_id:140818) (entropy of entanglement)** 定义为[约化密度算符](@entry_id:190449)的[冯·诺依曼熵](@entry_id:143216) $S(\rho_A) = -\sum_k \lambda_k \ln \lambda_k$。它量化了两个子系统之间的纠缠程度。对于积态，$S(\rho_A)=0$。
纠缠是量子力学最深刻的特征之一，它在量子计算、[量子通信](@entry_id:138989)和[量子密码学](@entry_id:144827)中扮演着核心角色。

#### [全同粒子](@entry_id:142755)的[对称化公设](@entry_id:148962)

第七个公设涉及**[全同粒子](@entry_id:142755) (identical particles)**。它规定，由多个[全同粒子](@entry_id:142755)组成的系统的状态矢量在交换任意两个粒子的坐标（包括空间和自旋）时必须保持对称或反对称。
-   对于**玻色子 (bosons)** (如光子、胶子)，交换粒子后状态矢量不变（**对称**）。
-   对于**[费米子](@entry_id:146235) (fermions)** (如电子、夸克)，交换粒子后状态矢量反号（**反对称**）。

这个**[对称化公设](@entry_id:148962) (symmetrization postulate)** 有着深远的物理后果。对于[费米子](@entry_id:146235)系统，如[多电子原子](@entry_id:157716)或分子，[反对称性](@entry_id:261893)要求直接导出了**泡利不相容原理 (Pauli exclusion principle)**：两个费米子不能占据同一个单粒子量子态。

例如，考虑一个双电子系统 。其总[波函数](@entry_id:201714) $\Psi(\mathbf{x}_1, \mathbf{x}_2)$ 必须满足 $\Psi(\mathbf{x}_2, \mathbf{x}_1) = -\Psi(\mathbf{x}_1, \mathbf{x}_2)$。通常，[波函数](@entry_id:201714)可以分解为空间[部分和](@entry_id:162077)自旋部分的乘积。为了使总[波函数](@entry_id:201714)反对称，必须满足以下两种组合之一：
1.  空间部分反对称 $\times$ 自旋部分对称（自旋[三重态](@entry_id:156705)）。
2.  空间部分对称 $\times$ 自旋部分反对称（[自旋单重态](@entry_id:153133)）。

如果两个电子占据同一个空间轨道 $\phi_a(\mathbf{r})$，其空间[波函数](@entry_id:201714) $\phi_a(\mathbf{r}_1)\phi_a(\mathbf{r}_2)$ 必然是对称的。因此，它们的自旋部分必须是反对称的（[单重态](@entry_id:154728)），即 $\frac{1}{\sqrt{2}}(\alpha(1)\beta(2) - \beta(1)\alpha(2))$。这就是为何同一个原子轨道最多只能容纳两个自旋相反的电子的原因。

#### [超选择定则](@entry_id:203866)

对称性在量子力学中扮演着核心角色，而**[超选择定则](@entry_id:203866) (superselection rules)** 是其一个深刻体现 。设想存在一个守恒的“荷” $Q$，其对应的算符 $\hat{Q}$与系统所有**可观测**的物理量 $\hat{A}$ 都对易，即 $[\hat{A}, \hat{Q}] = 0$ for all $\hat{A} \in \mathcal{A}_{obs}$。

这个条件意味着，任何物理操作（由 $\mathcal{A}_{obs}$ 中的算符描述）都不能改变系统的荷 $Q$。[希尔伯特空间](@entry_id:261193)因此可以分解为 $\hat{Q}$ 的不同本征值 $q$ 所对应的子空间（扇区）的[直和](@entry_id:156782)：$\mathcal{H} = \bigoplus_q \mathcal{H}_q$。这些子空间 $\mathcal{H}_q$ 就是**超选择扇区 (superselection sectors)**。

其关键后果是：
- 任何可观测算符 $\hat{A}$ 都不能连接不同的扇区，即对于 $|\psi_q\rangle \in \mathcal{H}_q$ 和 $|\psi_{q'}\rangle \in \mathcal{H}_{q'}$，若 $q \neq q'$，则矩阵元 $\langle \psi_{q'}|\hat{A}|\psi_q\rangle = 0$。
- 因此，我们无法通过任何物理测量来区分一个处于不同扇区态的[相干叠加](@entry_id:170209) $|\psi\rangle = c_1|\psi_q\rangle + c_2|\psi_{q'}\rangle$ 和一个处于这些态的经典统计混合 $\rho = |c_1|^2|\psi_q\rangle\langle\psi_q| + |c_2|^2|\psi_{q'}\rangle\langle\psi_{q'}|$。
- 这意味着，不同超选择扇区之间的**[相对相位](@entry_id:148120) (relative phase)** 是不可观测的。我们不能制备或验证一个具有确定[相对相位](@entry_id:148120)的、跨扇区的叠加态。

例如，电荷就是一个超选择荷。我们无法制备一个电子和一个质子的[相干叠加](@entry_id:170209)态。[超选择定则](@entry_id:203866)限制了叠加原理的普适性，它将整个[希尔伯特空间划分](@entry_id:202324)为一个个独立的“世界”，物理过程只能在每个世界内部发生，而不能在世界之间建立相[干性](@entry_id:900268)。这与[全局相位](@entry_id:147947)的不可观测性是两个不同的概念：[全局相位](@entry_id:147947)是[量子态表示](@entry_id:146523)的内在冗余，而[相对相位](@entry_id:148120)的不[可观测性](@entry_id:152062)则是由于物理定律限制了我们的操作能力。

综上所述，量子力学的公设构成了一个严密而自洽的逻辑体系，它不仅成功地解释了微观世界的各种奇异现象，也为[量子技术](@entry_id:142946)的发展提供了坚实的理论基础。