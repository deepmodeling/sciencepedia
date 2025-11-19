## 引言
量子力学的公设构成了我们理解和预测原子与分子尺度下物质行为的理论基石。对于物理科学领域的学习者而言，这些抽象的数学原理——从希尔伯特空间到自伴算符——不仅是理论考试的重点，更是连接量子世界与宏观物理和化学现象（如分子结构、化学反应性和[光谱](@entry_id:185632)特征）的桥梁。然而，许多学习者常常感到困惑，难以将这些高度形式化的公设与化学直觉和实际应用联系起来。本文旨在弥合这一鸿沟，系统性地梳理量子力学的核心公设，并阐明其背后的物理意义和化学推论。

本文将分为三个核心章节。在“**原理与机制**”中，我们将严谨地建立量子力学的公理化体系，详细探讨[量子态](@entry_id:146142)、可观测量、测量过程、[时间演化](@entry_id:153943)以及复合系统的数学描述。随后，在“**应用与[交叉](@entry_id:147634)学科联系**”中，我们将展示这些公设如何具体地应用于解释化学成键、分子[光谱](@entry_id:185632)、电子相关等关键化学概念，并揭示其与物理学、计算科学等领域的深刻联系。最后，在“**动手实践**”部分，读者将通过解决具体问题，将理论知识转化为可操作的计算技能。通过这一结构化的学习路径，本文旨在帮助读者不仅“知道”量子力学的公设是什么，更能深刻“理解”它们为何如此，以及如何运用它们来解决真实的化学问题。

## 原理与机制

本章旨在系统性地阐述非[相对论量子力学](@entry_id:148643)的基本原理，这些原理共同构成了我们理解和预测分子尺度下物质行为的理论基石。我们将从[量子态](@entry_id:146142)的数学描述开始，深入探讨[可观测量](@entry_id:267133)的表示、测量过程的概率性本质及其后果，最后讨论系统的动力学演化以及[多粒子系统](@entry_id:192694)的组合规则。本章的论述将以严谨的数学形式展开，同时始终与物理操作和化学应用保持紧密联系。

### 量子系统的状态

#### 1.1 状态假设：[希尔伯特空间](@entry_id:261193)与态矢量

量子力学的第一个基本假设是，一个孤立量子系统的[纯态](@entry_id:141688)（pure state）由一个复（complex）可分（separable）希尔伯特空间（Hilbert space）$\mathcal{H}$ 中的单位矢量（unit vector）$|\psi\rangle$ 来描述。这一假设虽然抽象，但其每一个限定词——“希尔伯特”、“复”、“可分”——都深植于物理现实和数学一致性的要求之中。

[希尔伯特空间](@entry_id:261193)是一个配备了[内积](@entry_id:158127)的完备[向量空间](@entry_id:151108)。**完备性（completeness）** 是一个至关重要的拓扑性质，它要求空间中任何柯西序列（Cauchy sequence）都收敛于空间内的一点。从操作层面看，实验室中的态制备过程往往是一个理想化的极限过程。例如，我们可能通过一系列越来越精确的步骤来制备一个目标态。这一系列近似的制备过程在数学上对应于一列态矢量 $\{\psi_n\}_{n\in\mathbb{N}}$。如果这个制备过程在操作上是收敛的——即对于任何有界[可观测量](@entry_id:267133)，其测量概率和[期望值](@entry_id:153208)的序列都趋于稳定（形成柯西序列）——那么我们理应要求这个极限过程所指向的目标态本身也是理论所允许的一个有效态。这在数学上就要求态矢量的柯西序列必须收敛到[希尔伯特空间](@entry_id:261193) $\mathcal{H}$ 内的一个矢量。因此，完备性保证了理论的封闭性：物理上可实现的理想化极限过程总能对应到模型内的一个确切状态，而不会“泄漏”到空间之外 [@problem_id:2916810]。

**可分性（separability）** 要求希尔伯特空间拥有一个可数的[稠密子集](@entry_id:264458)，这等价于存在一个可数的标准正交基。这一要求与物理测量的可操作性直接相关。任何物理实验都由有限或至多可数个步骤构成。为了完全确定一个[量子态](@entry_id:146142) $|\psi\rangle = \sum_k c_k |e_k\rangle$，我们原则上需要确定其在一个[可数基](@entry_id:155278) $\{|e_k\rangle\}$ 上的所有分量 $c_k$。这可以通过可数次测量来实现。如果空间是不可分的，它将需要一个不可数的基，这意味着确定一个态需要不可数个独立参数，这在物理上是无法操作的。此外，[量子化学](@entry_id:140193)中研究的典型系统，如包含有限个[原子核](@entry_id:167902)和电子的分子，其[位形空间](@entry_id:149531)是有限维[流形](@entry_id:153038) $\mathbb{R}^{3N}$，所对应的函数空间，如$L^2(\mathbb{R}^{3N})$，本身就是可分的。因此，[可分性](@entry_id:143854)假设不仅是数学上的便利，更是对我们所研究的物理系统性质的直接抽象 [@problem_id:2916810]。

#### 1.2 射线假设：[全局相位](@entry_id:147947)与相对相位

虽然我们用单位矢量 $|\psi\rangle$ 表示状态，但更精确地说，一个物理状态对应于希尔伯特空间中的一条**射线（ray）**，即形如 $\{\lambda |\psi\rangle : \lambda \in \mathbb{C} \setminus \{0\}\}$ 的一维[子空间](@entry_id:150286)。当我们限制使用归一化矢量时，这意味着所有通过乘以一个相位因子 $e^{i\alpha}$（其中 $\alpha$ 为实数）而相互关联的矢量，如 $|\psi\rangle$ 和 $e^{i\alpha}|\psi\rangle$，描述的是完全相同的物理状态。这个 $e^{i\alpha}$ 被称为**[全局相位](@entry_id:147947)（global phase）**。

[全局相位](@entry_id:147947)的不[可观测性](@entry_id:152062)是量子力学的一个基本推论。任何可观测量（如测量概率或[期望值](@entry_id:153208)）的计算都涉及到形如 $\langle\phi|\hat{O}|\psi\rangle$ 的表达式的模平方或其[线性组合](@entry_id:154743)。在[全局相位](@entry_id:147947)变换 $|\psi\rangle \to |\psi'\rangle = e^{i\alpha}|\psi\rangle$ 下，概率 $P' = |\langle\chi|\psi'\rangle|^2 = |e^{i\alpha}\langle\chi|\psi\rangle|^2 = |\langle\chi|\psi\rangle|^2 = P$ 保持不变。类似地，[期望值](@entry_id:153208) $\langle A \rangle' = \langle\psi'|A|\psi'\rangle = \langle e^{i\alpha}\psi|A|e^{i\alpha}\psi\rangle = \langle\psi|A|\psi\rangle = \langle A \rangle$ 也保持不变。因此，[全局相位](@entry_id:147947)没有任何可观测的物理效应 [@problem_id:2916806]。

然而，**相对相位（relative phase）**则具有深刻的物理意义。考虑一个由两个[正交基](@entry_id:264024)态 $|g\rangle$ 和 $|e\rangle$ 张成的二维电子流形中的一个叠加态：
$$
|\psi\rangle = \cos\theta |g\rangle + e^{i\phi}\sin\theta |e\rangle
$$
这里的 $\phi$ 就是[基态](@entry_id:150928) $|g\rangle$ 和 $|e\rangle$ 之间的[相对相位](@entry_id:148120)。与[全局相位](@entry_id:147947)不同，[相对相位](@entry_id:148120)是可测量的，并且是[量子干涉](@entry_id:139127)现象的根源。例如，考虑在一个新的基 $\{|+\rangle, |-\rangle\}$ 中进行测量，其中 $|+\rangle = (|g\rangle+|e\rangle)/\sqrt{2}$。测量得到结果 “+” 的概率为：
$$
P_+ = |\langle+|\psi\rangle|^2 = \left| \frac{1}{\sqrt{2}}(\langle g|+\langle e|) (\cos\theta |g\rangle + e^{i\phi}\sin\theta |e\rangle) \right|^2 = \frac{1}{2}|\cos\theta + e^{i\phi}\sin\theta|^2
$$
展开计算可得：
$$
P_+(\theta, \phi) = \frac{1}{2}(1 + \sin(2\theta)\cos\phi)
$$
这个概率明确地依赖于相对相位 $\phi$。通过改变 $\phi$（例如，在[分子动力学](@entry_id:147283)中通过[激光](@entry_id:194225)场控制），我们可以观察到概率 $P_+$ 的[振荡](@entry_id:267781)，这就是量子干涉条纹。因此，[相对相位](@entry_id:148120)是状态的一个关键物理属性 [@problem_id:2916806]。

#### 1.3 [密度算符](@entry_id:138151)：[纯态](@entry_id:141688)与[混合态](@entry_id:141568)

态矢量描述的是对系统有最大可能了解的**[纯态](@entry_id:141688)（pure state）**。然而，在很多实际情况中，我们对系统的知识是不完备的，例如，系统可能是通过某个[随机过程](@entry_id:159502)制备的，或者它是某个更[大系统](@entry_id:166848)的一部分。在这种情况下，系统的状态由一个更普适的数学对象——**[密度算符](@entry_id:138151)（density operator）** $\rho$ 来描述。

一个算符 $\rho$ 是合法的[密度算符](@entry_id:138151)，当且仅当它满足以下三个条件 [@problem_id:2916819]：
1.  **[厄米性](@entry_id:141899)（Hermiticity）**: $\rho = \rho^\dagger$。这保证了测量概率是实数。
2.  **单位迹（Unit Trace）**: $\mathrm{Tr}(\rho) = 1$。这保证了总概率为1。
3.  **正半定性（Positive Semidefiniteness）**: $\rho \ge 0$，即其所有[本征值](@entry_id:154894)均非负。这保证了任何测量结果的概率都是非负的。

如果一个系统以概率 $p_k$ 处于纯态 $|\psi_k\rangle$，那么这个**系综（ensemble）**的状态由[密度算符](@entry_id:138151) $\rho = \sum_k p_k |\psi_k\rangle\langle\psi_k|$ 描述。这是一个**[混合态](@entry_id:141568)（mixed state）**。一个[纯态](@entry_id:141688) $|\psi\rangle$ 也可以用[密度算符](@entry_id:138151)表示，即 $\rho = |\psi\rangle\langle\psi|$。

区分[纯态](@entry_id:141688)和混合态的一个重要指标是**纯度（purity）**，定义为 $\mathrm{Tr}(\rho^2)$。
-   对于一个[纯态](@entry_id:141688) $\rho = |\psi\rangle\langle\psi|$，我们有 $\rho^2 = (|\psi\rangle\langle\psi|)(|\psi\rangle\langle\psi|) = |\psi\rangle\langle\psi| = \rho$。因此，$\mathrm{Tr}(\rho^2) = \mathrm{Tr}(\rho) = 1$。
-   对于一个[混合态](@entry_id:141568)，可以证明 $\mathrm{Tr}(\rho^2)  1$。其最小值为 $1/d$，其中 $d$ 是[希尔伯特空间](@entry_id:261193)的维度，这个最小值由**[最大混合态](@entry_id:137775)** $\rho = I/d$ 取得，其中 $I$ 是单位算符 [@problem_id:2916819]。

例如，算符 $$\rho_1 = \frac{1}{2}\begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix}$$ （在其二维支持空间内）的迹为1，[本征值](@entry_id:154894)为 $\{1, 0\}$，是[纯态](@entry_id:141688) $|\psi\rangle = \frac{1}{\sqrt{2}}(|e_1\rangle+|e_2\rangle)$ 的[密度算符](@entry_id:138151)，其纯度为 $\mathrm{Tr}(\rho_1^2)=1$。而算符 $$\rho_2 = \frac{1}{2}\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}$$ 的迹为1，[本征值](@entry_id:154894)为 $\{\frac{1}{2}, \frac{1}{2}\}$，是一个[混合态](@entry_id:141568)，其纯度为 $\mathrm{Tr}(\rho_2^2) = (\frac{1}{2})^2 + (\frac{1}{2})^2 = \frac{1}{2}  1$ [@problem_id:2916819]。

所有[密度算符](@entry_id:138151)构成的集合形成一个**[凸集](@entry_id:155617)（convex set）**。这意味着，如果 $\rho_1$ 和 $\rho_2$ 是两个有效的[量子态](@entry_id:146142)，那么它们的任意凸组合 $\rho = p\rho_1 + (1-p)\rho_2$（其中 $0 \le p \le 1$）也代表一个有效的[量子态](@entry_id:146142)。这与将两个系综以概率 $p$ 和 $1-p$ 混合的物理操作相对应。[纯态](@entry_id:141688)是该[凸集](@entry_id:155617)的**极点（extremal points）**。值得注意的是，该凸集的[边界点](@entry_id:176493)不仅包含纯态，还包含所有非满秩的混合态 [@problem_id:2916819]。

### 可观测量与测量

#### 2.1 可观测量假设：自伴算符

量子力学假设，每一个物理可观测量（observable），如能量、动量或偶极矩，都由一个厄米算符（Hermitian operator）表示。更准确地说，对于可能具有连续谱的无界算符（unbounded operator），这个算符必须是**自伴的（self-adjoint）**。

对称性（symmetry）与自伴性（self-adjointness）之间存在微妙但关键的区别。一个算符 $A$ 若在其定义域 $\mathcal{D}(A)$ 内满足 $\langle \psi, A\phi\rangle=\langle A\psi,\phi\rangle$，则称其为对称的。而自伴算符不仅要求对称，还要求其定义域与其伴随算符的定义域相同，即 $\mathcal{D}(A) = \mathcal{D}(A^\dagger)$。

为何必须要求自伴性？其核心原因在于**谱定理（Spectral Theorem）**。只有自伴算符才能保证存在一个唯一的、定义在实轴 $\mathbb{R}$ 上的**投影值测量（Projection-Valued Measure, PVM）** $\{E(B)\}$。这个 PVM 将[实轴](@entry_id:148276)的每个（波莱尔）[子集](@entry_id:261956) $B$ 映射到一个投影算符 $E(B)$，它构成了后续所有测量假设的数学基础。一个仅仅对称但非自伴的算符，其谱可能不是实数，也无法保证存在这样一个结构良好的[谱分解](@entry_id:173707) [@problem_id:2916811]。

此外，自伴性对于描述动力学也至关重要。如后文将述，系统的[幺正时间演化](@entry_id:192535)由[哈密顿算符](@entry_id:144286) $H$ 生成。**[斯通定理](@entry_id:262301)（Stone's Theorem）**表明，一个良定义的、保持概率守恒的[幺正演化](@entry_id:145020)群的存在，当且仅当其生成元 $H$ 是自伴的。因此，自伴性是[量子理论](@entry_id:145435)在测量和动力学两方面保持一致性的根本要求 [@problem_id:2916811]。在数学上，一个对称算符是否拥有[自伴扩张](@entry_id:264525)，可以通过其**亏损指标（deficiency indices）**来判断。只有当亏损指标相等时，才存在[自伴扩张](@entry_id:264525)。例如，在半直线 $(0, \infty)$ 上定义的[动量算符](@entry_id:151743) $p = -i\hbar\frac{d}{dx}$（其定义域为[紧支集](@entry_id:276214)[光滑函数](@entry_id:267124)）就是一个对称但非自伴的算符，它没有任何[自伴扩张](@entry_id:264525)，因此不能代表一个定义在半直线上的[物理可观测量](@entry_id:154692) [@problem_id:2916811]。

#### 2.2 测量假设与玻恩规则

当测量一个处于状态 $\rho$ 的系统上的[可观测量](@entry_id:267133) $A$ 时，测量结果的[概率分布](@entry_id:146404)由**玻恩规则（Born rule）**给出。如果 $A$ 拥有[离散谱](@entry_id:150970)，其[谱分解](@entry_id:173707)为 $A = \sum_a a P_a$，其中 $a$ 是[本征值](@entry_id:154894)，$P_a$ 是对应于[本征值](@entry_id:154894) $a$ 的[本征空间](@entry_id:147356)的投影算符。测量得到结果 $a$ 的概率是：
$$
p(a) = \mathrm{Tr}(\rho P_a)
$$
对于纯态 $\rho=|\psi\rangle\langle\psi|$，这简化为 $p(a) = \langle\psi|P_a|\psi\rangle$。如果[本征值](@entry_id:154894) $a$ 是非简并的，对应本征矢量 $|a\rangle$，则 $P_a = |a\rangle\langle a|$，概率为 $p(a) = |\langle a|\psi\rangle|^2$。

对于具有[连续谱](@entry_id:155477)的可观测量，如位置算符 $X$，其结果用[概率密度](@entry_id:175496)描述。粒子在位置 $x$ 附近被发现的[概率密度](@entry_id:175496)为 $p(x) = |\psi(x)|^2$，其中 $\psi(x) = \langle x|\psi\rangle$ 是位置表象中的[波函数](@entry_id:147440)。在区间 $\Delta$ 内发现粒子的概率是 $P(x \in \Delta) = \int_\Delta |\psi(x)|^2 dx$ [@problem_id:2916818]。

一个深刻的问题是：为什么概率是振幅的**模平方**，而不是其他函数？这一二次依赖关系并非随意选择，而是源于对[概率测度](@entry_id:190821)的更基本公理的要求。**[格里森定理](@entry_id:146674)（Gleason's theorem）**表明，在维度大于2的[希尔伯特空间](@entry_id:261193)中，任何在[投影算符](@entry_id:154142)上定义的、满足非负性、归一化和[可数可加性](@entry_id:186580)的非关联（non-contextual）[概率测度](@entry_id:190821)，必然可以表示为 $p(P) = \mathrm{Tr}(\rho P)$ 的形式，其中 $\rho$ 是一个唯一的[密度算符](@entry_id:138151)。对于纯态 $\rho=|\psi\rangle\langle\psi|$，这直接导出了玻恩规则 $p(P) = \langle\psi|P|\psi\rangle$。因此，概率的二次形式是量子力学逻辑结构的必然结果，而非一个独立的附加假设 [@problem_id:2916818]。

#### 2.3 统计诠释：[期望值](@entry_id:153208)与矩

玻恩规则不仅给出单个结果的概率，还决定了测量结果的整个统计分布。一个可观测量 $A$ 的**[期望值](@entry_id:153208)（expectation value）**，即大量相同制备的系统上进行单次测量所得结果的平均值，由下式给出：
$$
\langle A \rangle = \mathrm{Tr}(\rho A)
$$
对于纯态，则为 $\langle A \rangle = \langle\psi|A|\psi\rangle$。

更一般地，所有矩都可以从[谱测度](@entry_id:201693) $\mu_{A,\rho}(\Delta) = \mathrm{Tr}(\rho P_A(\Delta))$ 导出。第 $n$ 个矩是 $\langle A^n \rangle = \int_{\mathbb{R}} \lambda^n d\mu_{A,\rho}(\lambda)$。特别地，**[方差](@entry_id:200758)（variance）** $\Delta^2 A$ 描述了测量结果围绕[期望值](@entry_id:153208)的离散程度：
$$
\Delta^2 A = \langle (A - \langle A \rangle I)^2 \rangle = \langle A^2 \rangle - \langle A \rangle^2
$$
在使用这些公式时，必须注意无界算符的定义域问题。例如，[期望值](@entry_id:153208) $\langle\psi|A|\psi\rangle$ 和[方差](@entry_id:200758)的表达式只有在 $|\psi\rangle$ 属于相应算符（$A$ 或 $A^2$）的定义域时才有意义。一个态的[方差](@entry_id:200758)是有限的，当且仅当该态矢量位于算符 $A$ 的定义域内，即 $\int_{\mathbb{R}} \lambda^2 d\mu_{A,\psi}(\lambda)  \infty$。如果此条件不满足，则[方差](@entry_id:200758)为无穷大，表示测量结果的[分布](@entry_id:182848)非常离散 [@problem_id:2916815]。

最后，必须将量子[期望值](@entry_id:153208)与统计学中的样本平均值区分开。量子[期望值](@entry_id:153208)是在一个**系综**上定义的理论量，即对无限多个以相同方式制备的独立系统各进行一次测量，其结果的平均值。它不等于对**单个**量子系统进行连续多次测量得到的平均值，因为（除非特殊情况）测量会改变系统状态，导致后续测量的结果不再是[独立同分布](@entry_id:169067)的 [@problem_id:2916815]。

#### 2.4 投影假设：测量后的状态更新

测量不仅揭示了信息，它还通常会改变系统的状态。**投影假设（projection postulate）**描述了这种状态变化。对于一次理想的、可重复的**投影测量**（也称为冯·诺依曼测量），如果测量[可观测量](@entry_id:267133) $A$ 得到了结果 $a$，那么系统的状态会发生“塌缩”。

-   **非简并情况**：如果初态是 $|\psi\rangle$，测量得到非简并[本征值](@entry_id:154894) $a$（对应本征矢量 $|a\rangle$），那么测量后的状态就是 $|a\rangle$。
-   **简并情况**：这是一个更普遍和现实的场景。如果测量得到简并[本征值](@entry_id:154894) $a$，其对应的[本征空间](@entry_id:147356)由投影算符 $P_a$ 描述，那么状态的更新遵循**吕德斯规则（Lüders' rule）**。如果初态是 $\rho$，测量后的状态 $\rho_a$ 为：
    $$
    \rho \mapsto \rho_a = \frac{P_a \rho P_a}{\mathrm{Tr}(\rho P_a)}
    $$
    这个过程将状态投影到被测量的本征[子空间](@entry_id:150286)上。值得注意的是，这个更新规则保留了[密度算符](@entry_id:138151)在**该[子空间](@entry_id:150286)内部**的相干性。例如，如果初态是一个在 $a$ [子空间](@entry_id:150286)内不同[基矢](@entry_id:199546)量之间的叠加态，这个叠加关系在测量后会被保持，只是被重新归一化 [@problem_id:2916831]。

如果测量完成但结果未被读取（**非选择性测量**），则最终状态是所有可能结果的加权平均，即一个统计混合：
$$
\rho \mapsto \rho' = \sum_a p(a) \rho_a = \sum_a \mathrm{Tr}(\rho P_a) \frac{P_a \rho P_a}{\mathrm{Tr}(\rho P_a)} = \sum_a P_a \rho P_a
$$
这个过程会破坏不同本征[子空间](@entry_id:150286)之间的[相干性](@entry_id:268953)（即[密度算符](@entry_id:138151)矩阵中对应于不同[本征值](@entry_id:154894)的块间元素变为零），是**退相干（decoherence）**的一个基本模型 [@problem_id:2916831]。

#### 2.5 [广义测量](@entry_id:154280)：[POVM](@entry_id:138770)

投影测量是一个理想化的模型。更普适的测量框架是**正算符值测量（Positive Operator-Valued Measure, [POVM](@entry_id:138770)）**。一个[POVM](@entry_id:138770)由一系列正半定算符 $\{E_i\}$（称为“效应”）定义，它们满足[完备性关系](@entry_id:139077) $\sum_i E_i = I$。测量得到结果 $i$ 的概率为：
$$
p(i) = \mathrm{Tr}(\rho E_i)
$$
[POVM](@entry_id:138770)是PVM的推广。PVM是[POVM](@entry_id:138770)的一个特例，其中效应算符 $E_i$ 恰好是相互正交的[投影算符](@entry_id:154142) $P_i$。与PVM相比，[POVM](@entry_id:138770)具有更广泛的适用性：
-   **非正交效应**：[POVM](@entry_id:138770)的效应算符 $E_i$ 不需要相互正交，甚至不需要相互对易。例如，一个[量子比特](@entry_id:137928)（二维系统）上的PVM最多只能有两个结果，而一个[POVM](@entry_id:138770)可以有任意多个结果 [@problem_id:2916795]。
-   **非锐利测量**：[POVM](@entry_id:138770)通常描述的是“非锐利”（unsharp）或“模糊”（fuzzy）的测量，它们不具备PVM那种理想的[可重复性](@entry_id:194541)。
-   **子系统测量**：根据**[奈马克扩张定理](@entry_id:153668)（Naimark's Dilation Theorem）**，任何在系统 $\mathcal{H}$ 上的[POVM](@entry_id:138770)都可以被视为在一个更大的希尔伯特空间 $\mathcal{H} \otimes \mathcal{H}_A$（其中 $\mathcal{H}_A$ 是一个[辅助系统](@entry_id:142219)或“探针”）上的PVM，然后再将结果限制回原系统。这表明[POVM](@entry_id:138770)是描述[开放系统](@entry_id:147845)或与环境相互作用的系统上测量的自然语言 [@problem_id:2916795]。

### 动力学与复合系统

#### 3.1 [时间演化假设](@entry_id:155210)

孤立量子系统的时间演化由**薛定谔方程（Schrödinger equation）**描述。对于态矢量 $|\psi(t)\rangle$，其[微分形式](@entry_id:146747)为：
$$
i\hbar \frac{d}{dt}|\psi(t)\rangle = H|\psi(t)\rangle
$$
其中 $H$ 是系统的[哈密顿算符](@entry_id:144286)（Hamiltonian），即总能量的可观测量。由于能量是[物理可观测量](@entry_id:154692)，[哈密顿算符](@entry_id:144286) $H$ 必须是一个自伴算符。

正如之前所讨论的，对于无界[哈密顿算符](@entry_id:144286)（这在[量子化学](@entry_id:140193)中是常态），自伴性是至关重要的。**[斯通定理](@entry_id:262301)**保证了自伴的[哈密顿算符](@entry_id:144286) $H$ 能够生成一个唯一的、强连续的单参数幺正群 $U(t)$。这个幺正算符 $U(t) = \exp(-iHt/\hbar)$ 被称为[时间演化算符](@entry_id:196774)。它将任意初始状态 $|\psi_0\rangle$ 演化到时间 $t$ 时的状态：
$$
|\psi(t)\rangle = U(t)|\psi_0\rangle = e^{-iHt/\hbar}|\psi_0\rangle
$$
[幺正性](@entry_id:138773)（$U^\dagger(t)U(t) = I$）保证了态矢量的范数在[演化过程](@entry_id:175749)中守恒，即概率守恒。对于初始态在 $H$ 定义域内的情况，即 $|\psi_0\rangle \in \mathcal{D}(H)$，上述积分形式的解等价于微分形式的薛定谔方程。但对于任意初始态，演化由 $U(t)$ 给出，即使其可能不满足[微分方程](@entry_id:264184)的强形式 [@problem_id:2916821]。在[量子化学](@entry_id:140193)中，对于固定[原子核](@entry_id:167902)的分子电子[哈密顿算符](@entry_id:144286)，**卡托-雷利希定理（Kato-Rellich theorem）**等强大工具可以用来证明其在合适的定义域上是自伴的，从而保证了分子系统存在一个良定义的[幺正时间演化](@entry_id:192535) [@problem_id:2916821]。

#### 3.2 复合系统假设：[张量积](@entry_id:140694)与纠缠

当我们将多个子系统组合成一个复合系统时，其[状态空间](@entry_id:177074)由各子系统的希尔伯特空间的**[张量积](@entry_id:140694)（tensor product）**构成。例如，对于两个系统 $A$ 和 $B$，其复合系统的希尔伯特空间为 $\mathcal{H}_{AB} = \mathcal{H}_A \otimes \mathcal{H}_B$。

复合系统的状态可以分为两大类：**[可分态](@entry_id:142281)（separable states）**和**[纠缠态](@entry_id:152310)（entangled states）**。
-   一个纯态是**可分的**，当且仅当它可以写成两个子系统[纯态](@entry_id:141688)的张量积：$|\Psi\rangle = |\psi_A\rangle \otimes |\psi_B\rangle$。这意味着两个子系统具有独立的、确定的状态。
-   一个混合态是**可分的**，如果它可以被写成可分[纯态](@entry_id:141688)的统计混合，即 $\rho_{AB} = \sum_k p_k \rho_A^{(k)} \otimes \rho_B^{(k)}$。这代表的状态可以通过经典通信和局域操作（Local Operations and Classical Communication, LOCC）来制备。
-   任何不是[可分态](@entry_id:142281)的状态都被称为**纠缠态**。纠缠是量子力学独有的特性，它表示子系统之间存在非经典的关联，即使它们在空间上相距遥远。

对于一个[纯态](@entry_id:141688) $|\Psi\rangle$，其是否纠缠可以通过**[施密特分解](@entry_id:145934)（Schmidt decomposition）**来判断。如果其[施密特秩](@entry_id:154893)（Schmidt rank）大于1（即分解式中有多于一项），则该态是纠缠的。这等价于其任一子系统的[约化密度算符](@entry_id:190449) $\rho_A = \mathrm{Tr}_B(|\Psi\rangle\langle\Psi|)$ 的秩大于1 [@problem_id:2916792]。

需要注意的是，纠缠态的混合不一定产生纠缠态。例如，两个[贝尔态](@entry_id:140749) $|\Phi^\pm\rangle = (|00\rangle \pm |11\rangle)/\sqrt{2}$ 都是最大[纠缠态](@entry_id:152310)，但它们的等权重混合产生了一个[可分态](@entry_id:142281)：
$$
\rho_{AB} = \frac{1}{2}|\Phi^+\rangle\langle\Phi^+| + \frac{1}{2}|\Phi^-\rangle\langle\Phi^-| = \frac{1}{2}|00\rangle\langle 00| + \frac{1}{2}|11\rangle\langle 11|
$$
这个例子清楚地表明，纠缠态集合本身不是一个[凸集](@entry_id:155617) [@problem_id:2916792]。

#### 3.3 [全同粒子](@entry_id:142755)假设：对称性与[超选择定则](@entry_id:203866)

描述包含多个**全同粒子（identical particles）**的系统时，必须引入最后一个关键假设：**对称化假设（symmetrization postulate）**。该假设源于粒子不可区分的物理原理：任何交换两个全同粒子的操作都不会改变任何物理可观测量的值。

数学上，这意味着任何物理可观测量 $\hat{A}$ 必须与实现粒子[置换](@entry_id:136432)的幺正算符 $\hat{U}(\pi)$ 对易，即 $[\hat{A}, \hat{U}(\pi)] = \mathbf{0}$。根据[舒尔引理](@entry_id:136779)（Schur's Lemma），这个条件的一个深刻后果是，任何[物理可观测量](@entry_id:154692)都不能连接属于对称群 $S_N$ 的不等价不可约表示（irreps）的希尔伯特[子空间](@entry_id:150286)。换句话说，这些[子空间](@entry_id:150286)是相互隔离的**超选择扇区（superselection sectors）** [@problem_id:2916841]。

在三维空间中，对称群 $S_N$ 只有两种一维[不可约表示](@entry_id:263310)：
1.  **[平凡表示](@entry_id:141357)**（Trivial Representation）：$\hat{U}(\pi)|\Psi\rangle = +|\Psi\rangle$。属于这个扇区的粒子被称为**[玻色子](@entry_id:138266)（bosons）**，其多粒子[波函数](@entry_id:147440)在任意两个[粒子交换](@entry_id:154910)下是对称的。
2.  **符号表示**（Sign Representation）：$\hat{U}(\pi)|\Psi\rangle = \mathrm{sgn}(\pi)|\Psi\rangle$。属于这个扇区的粒子被称为**[费米子](@entry_id:146235)（fermions）**，其[波函数](@entry_id:147440)在交换下是反对称的。

[超选择定则](@entry_id:203866)意味着，一个由[玻色子](@entry_id:138266)态和[费米子](@entry_id:146235)态构成的[相干叠加](@entry_id:170209) $\alpha|\Psi_B\rangle + \beta|\Psi_F\rangle$ 虽然在数学上是[希尔伯特空间](@entry_id:261193)中一个合法的矢量，但在物理上是无法实现的，因为没有任何物理操作（由对称的[哈密顿量](@entry_id:172864)驱动）可以创造或探测其间的相对相位。其物理表现与一个经典统计[混合态](@entry_id:141568) $p_B|\Psi_B\rangle\langle\Psi_B| + p_F|\Psi_F\rangle\langle\Psi_F|$ 完全相同 [@problem_id:2916841]。

这个原理有直接的化学后果。例如，在氢分子 H$_2$ 中，两个质子是[费米子](@entry_id:146235)。其总核[波函数](@entry_id:147440)必须是反对称的。这导致了核[自旋态](@entry_id:149436)（对称的“[正氢](@entry_id:150894)”三线态与反对称的“[仲氢](@entry_id:753096)”[单线态](@entry_id:154728)）与核[转动态](@entry_id:158866)（只能取特定的奇数或偶数量子数）之间的严格耦合。由于[电磁跃迁](@entry_id:748891)几乎不能改变核自旋态，[正氢和仲氢](@entry_id:260889)表现为两种几乎不相互转化的独立物种，各自拥有不同的[光谱](@entry_id:185632)，这是[超选择定则](@entry_id:203866)在[分子光谱学](@entry_id:148164)中的一个直接体现 [@problem_id:2916841]。

值得一提的是，在二维系统中，交换的拓扑结构更为丰富，由[辫群](@entry_id:142941)（braid group）描述，这允许存在更广泛的[粒子统计](@entry_id:145640)类型，即**任意子（anyons）**，它们在交换下获得一个任意的相位因子，而不仅仅是 $\pm 1$ [@problem_id:2916841]。