## 引言
薛定谔方程是现代物理学的基石，它支配着非相对论量子系统的动态演化。掌握[量子动力学](@entry_id:138183)——即理解该方程的解——对于深入探索物理学、化学、[材料科学](@entry_id:152226)及其他众多科学领域至关重要。然而，尽管基础方程形式简洁，但其在复杂真实系统中的应用却揭示了大量深刻而富有挑战性的物理现象，从固态材料的电子特性到受外部驱动的非[平衡态](@entry_id:168134)行为，不一而足。本文旨在系统性地梳理量子动力学的核心理论，并展示其如何弥合基本原理与前沿交叉应用之间的鸿沟。

为实现这一目标，本文分为三个循序渐进的章节。第一章“原理与机制”将奠定坚实的理论基础，深入探讨[量子态](@entry_id:146142)的数学描述、[物理可观测量](@entry_id:154692)的算符表示，以及在各种[哈密顿量](@entry_id:172864)（含时、不含时、周期性）下的演化规律。第二章“应用与[交叉](@entry_id:147634)学科联系”将视野拓宽至多个前沿领域，通过实例展示量子动力学如何被用于解释[凝聚态物质](@entry_id:747660)的电子结构、外场中的奇特量子效应、介观器件的输运特性，乃至现代拓拓物理和宇宙学中的深刻概念。最后，在“动手实践”部分，读者将有机会通过解决具体问题，将理论知识转化为实践技能。通过这一结构化的学习路径，我们旨在为读者构建一个关于薛定谔方程与量子动力学的全面而深入的知识体系。

## 原理与机制

本章旨在深入探讨支配量子动力学的基本原理与核心机制。我们将从[量子态](@entry_id:146142)的数学描述出发，系统地阐述其在薛定谔方程下的[时间演化](@entry_id:153943)规律，并进一步探讨粒子在各种势场（如[电磁场](@entry_id:265881)、[周期势](@entry_id:140652)、局域缺陷等）中的行为。这些内容构成了理解和模拟材料中量子现象的理论基石。

### [量子态](@entry_id:146142)与可观测量：数学基础

在量子力学中，一个系统的状态由其所在希尔伯特空间 $\mathcal{H}$ 中的元素来描述。然而，这种描述并非一一对应，其中蕴含着深刻的结构。

#### 纯态与混合态

一个孤立量子系统若处于一个信息最完备的状态，则称其处于一个 **[纯态](@entry_id:141688) (pure state)**。从数学上讲，一个[纯态](@entry_id:141688)并非由[希尔伯特空间](@entry_id:261193)中一个唯一的非[零矢量](@entry_id:155273) $|\psi\rangle$ 来表示，而是由该矢量所生成的整个 **射线 (ray)** 来表示。一条射线是包含了所有与 $|\psi\rangle$ 共线的非[零矢量](@entry_id:155273)的[等价类](@entry_id:156032)，即 $[\psi] = \{c|\psi\rangle : c \in \mathbb{C} \setminus \{0\}\}$。这意味着，将代表一个[纯态](@entry_id:141688)的矢量乘以任何非零[复标量](@entry_id:272141) $c$（例如，一个[全局相位](@entry_id:147947)因子 $e^{i\alpha}$），所描述的物理状态是完全相同的。所有[可观测量](@entry_id:267133)的计算，例如[期望值](@entry_id:153208) $\langle A \rangle = \frac{\langle\psi|A|\psi\rangle}{\langle\psi|\psi\rangle}$，在这种变换下都保持不变，因为因子 $|c|^2$ 会在分子分母中抵消。因此，在实际计算中，我们通常选取射线中归一化的矢量（即 $\langle\psi|\psi\rangle=1$）作为该纯态的代表，但必须牢记，任何相差一个[全局相位](@entry_id:147947)的归一化矢量描述的都是同一个物理状态 [@problem_id:2857741]。

然而，在许多现实情况下，我们可能无法获得关于系统的完备信息，或者[系统与环境](@entry_id:142270)存在相互作用。此时，系统可能以一定的概率 $p_k$ 处于不同的纯态 $|\psi_k\rangle$ 之一。这种统计性的不确定性导致了 **混合态 (mixed state)** 的概念。混合态不能由单一的态矢量描述，而是必须通过 **[密度算符](@entry_id:138151) (density operator)** 或密度矩阵 $\rho$ 来刻画。[密度算符](@entry_id:138151)定义为这些纯态[投影算符](@entry_id:154142)的系综平均：
$$
\rho = \sum_k p_k |\psi_k\rangle\langle\psi_k|
$$
其中 $p_k \ge 0$ 且 $\sum_k p_k = 1$。一个算符要成为合法的[密度算符](@entry_id:138151)，必须满足三个基本性质：(1) 它是厄米算符（$\rho = \rho^\dagger$）；(2) 它是半正定的（$\langle\phi|\rho|\phi\rangle \ge 0$ 对任意 $|\phi\rangle$ 成立）；(3) 它的迹为1（$\mathrm{Tr}(\rho) = 1$）。[纯态](@entry_id:141688)可以看作是[混合态](@entry_id:141568)的一个特例，其[密度算符](@entry_id:138151)是一个秩为1的投影算符 $\rho = |\psi\rangle\langle\psi|$。对于一个[混合态](@entry_id:141568)，任何物理可观测量 $A$ 的[期望值](@entry_id:153208)为 $\langle A \rangle = \mathrm{Tr}(\rho A)$。一个至关重要的概念是，同一个[密度算符](@entry_id:138151) $\rho$ 可能有无穷多种不同的系综分解方式，但所有这些分解在操作上是不可区分的，因为它们对任何可观测量的预测结果都完全相同 [@problem_id:2857741]。

#### 对称算符与自伴算符

在量子力学中，物理可观测量由 **自伴算符 (self-adjoint operator)** 描述。这是一个比[厄米性](@entry_id:141899)（或对称性）更强的数学要求，其区别根植于算符的定义域。一个在稠密定义域 $\mathcal{D}(A)$ 上定义的线性算符 $A$ 被称为 **对称的 (symmetric)**，如果对于所有 $\psi, \phi \in \mathcal{D}(A)$，都有 $\langle \psi, A\phi \rangle = \langle A\psi, \phi \rangle$。它的伴随算符 $A^\dagger$ 的定义域 $\mathcal{D}(A^\dagger)$ 包含所有满足 $\langle \psi, A\phi \rangle = \langle \chi, \phi \rangle$ 对所有 $\phi \in \mathcal{D}(A)$ 都成立的 $\psi$，此时定义 $A^\dagger\psi = \chi$。一个算符是 **自伴的**，当且仅当它不仅是对称的，而且其定义域与其伴随算符的定义域完全相同，即 $A=A^\dagger$ 且 $\mathcal{D}(A) = \mathcal{D}(A^\dagger)$。

这个区别并非无足轻重，它对算符是否能成为一个合法的[哈密顿量](@entry_id:172864)或[可观测量](@entry_id:267133)至关重要。以一维半无限空间 $\mathcal{H} = L^2(0, \infty)$ 上的动量算符 $P = -i\hbar \frac{d}{dx}$ 为例 [@problem_id:2857763]。通过分部积分可知，对于任意 $\psi, \phi \in H^1(0, \infty)$（一阶索伯列夫空间，函数及其导数均平方可积），我们有 $\langle \psi, P\phi \rangle = \langle P\psi, \phi \rangle + i\hbar\overline{\psi(0)}\phi(0)$。
- 如果我们选择一个定义域为 $\mathcal{D}(P) = \{\psi \in H^1(0, \infty) : \psi(0)=0\}$，边界项因为 $\phi(0)=0$ 而消失，所以算符 $P$ 是对称的。但它的伴随算符的定义域是整个 $H^1(0, \infty)$，因为对于任何 $\psi \in H^1(0, \infty)$，边界项 $i\hbar\overline{\psi(0)}\phi(0)$ 总是为零，无需对 $\psi(0)$ 施加任何限制。由于 $\mathcal{D}(P) \neq \mathcal{D}(P^\dagger)$，该算符不是自伴的。
- 根据冯·诺伊曼的定理，一个对称算符是否存在[自伴扩张](@entry_id:264525)，取决于其[亏指数](@entry_id:266905) $(n_+, n_-)$ 是否相等。对于半无限空间上的[动量算符](@entry_id:151743)，可以证明其[亏指数](@entry_id:266905)为 $(1, 0)$，因此它不接受任何[自伴扩张](@entry_id:264525) [@problem_id:2857763]。这意味着在一维半无限空间中，不存在一个与动量相对应的、严格意义上的自伴[可观测量](@entry_id:267133)。这种微妙之处在处理具有边界或[奇点](@entry_id:137764)的系统时尤为关键，例如在为点缺陷建模时 [@problem_id:2857765]。

#### 玻恩法则

量子测量的概率性本质由 **玻恩法则 (Born rule)** 所描述。对于一个由投影算符集合 $\{P_i\}$（满足完备性 $\sum_i P_i = I$ 和正交性 $P_i P_j = \delta_{ij} P_i$）描述的投影测量，获得结果 $i$ 的概率 $p(i)$ 取决于系统的状态。
- 如果系统处于纯态 $|\psi\rangle$（已归一化），概率为 $p(i) = \langle\psi|P_i|\psi\rangle$。如果 $P_i$ 是一个秩为1的投影算符 $P_i = |\phi_i\rangle\langle\phi_i|$，则概率为 $p(i) = \langle\psi|\phi_i\rangle\langle\phi_i|\psi\rangle = |\langle\phi_i|\psi\rangle|^2$。一个常见的错误是忽略此处的平方 [@problem_id:2857741]。
- 如果系统处于混合态 $\rho$，则概率由更普适的公式给出：$p(i) = \mathrm{Tr}(\rho P_i)$。这个公式统一了两种情况，因为对于纯态 $\rho=|\psi\rangle\langle\psi|$，$\mathrm{Tr}(|\psi\rangle\langle\psi|P_i) = \langle\psi|P_i|\psi\rangle$ [@problem_id:2857741]。

例如，考虑一个由 **[最大混合态](@entry_id:137775)** $\rho = \frac{1}{2}I$ 描述的[二能级系统](@entry_id:138452)（[量子比特](@entry_id:137928)）。在任何一组正交基上进行投影测量，得到任意一个特定结果的概率总是 $\frac{1}{2}$。例如，对于 $|+\rangle = (|0\rangle+|1\rangle)/\sqrt{2}$，其[投影算符](@entry_id:154142)为 $P_+ = |+\rangle\langle+|$，概率为 $p(+) = \mathrm{Tr}(\frac{1}{2}I P_+) = \frac{1}{2}\mathrm{Tr}(P_+) = \frac{1}{2}$，因为任何秩为1的投影算符的迹都是1 [@problem_id:2857741]。

### 动力学演化：薛定谔方程

[量子态](@entry_id:146142)的动力学由 **时变薛定谔方程 (Time-Dependent Schrödinger Equation, TDSE)** 描述：
$$
i\hbar \frac{\partial}{\partial t} |\psi(t)\rangle = H(t) |\psi(t)\rangle
$$
其中 $H(t)$ 是系统的[哈密顿算符](@entry_id:144286)。

#### [哈密顿量](@entry_id:172864)不含时的情况

当[哈密顿量](@entry_id:172864) $H$ 不依赖于时间时，薛定谔方程的解具有特别简洁的形式。在这种情况下，存在一类特殊的解，称为 **定态 (stationary states)**。它们是[哈密顿量](@entry_id:172864)的[本征态](@entry_id:149904)，满足本征方程 $H|\phi_n\rangle = E_n|\phi_n\rangle$，其中 $E_n$ 是本征能量。一个定态的时间演化极其简单：$|\psi_n(t)\rangle = e^{-iE_n t/\hbar}|\phi_n\rangle$。它的[概率密度](@entry_id:175496) $|\psi_n(x,t)|^2 = |\phi_n(x)|^2$ 不随时间改变，并且任何不含时的[可观测量](@entry_id:267133) $A$ 的[期望值](@entry_id:153208) $\langle A \rangle_t = \langle\psi_n(t)|A|\psi_n(t)\rangle = \langle\phi_n|A|\phi_n\rangle$ 也是恒定的 [@problem_id:2857776]。

一个普遍的[量子态](@entry_id:146142) $|\psi(0)\rangle$ 通常可以写成这些定[态的叠加](@entry_id:273993)：$|\psi(0)\rangle = \sum_n c_n |\phi_n\rangle$。其后续演化由下式给出：
$$
|\psi(t)\rangle = \sum_n c_n e^{-iE_n t/\hbar} |\phi_n\rangle
$$
如果这个叠加态包含具有不同能量 $E_n \neq E_m$ 的分量，那么它就不再是定态。不同分量之间的[相对相位](@entry_id:148120) $e^{-i(E_n-E_m)t/\hbar}$ 会随[时间演化](@entry_id:153943)，导致干涉项的出现。这使得概率密度和[可观测量](@entry_id:267133)的[期望值](@entry_id:153208)通常会随时间[振荡](@entry_id:267781)。例如，一个初始态为 $(|\phi_1\rangle + |\phi_3\rangle)/\sqrt{2}$，其中 $E_1 \neq E_3$，其[概率密度](@entry_id:175496)将包含以角频率 $\omega = (E_3-E_1)/\hbar$ [振荡](@entry_id:267781)的项 [@problem_id:2857776]。

一个特殊情况是 **简并 (degeneracy)**，即多个[线性无关](@entry_id:148207)的本征态对应同一个本征能量。例如，如果 $H|\phi_1\rangle = E_1|\phi_1\rangle$ 且 $H|\phi_2\rangle = E_1|\phi_2\rangle$，那么它们的任意线性组合 $|\psi_b\rangle = c_1|\phi_1\rangle + c_2|\phi_2\rangle$ 也是能量为 $E_1$ 的本征态，因此也是一个[定态](@entry_id:137260) [@problem_id:2857776]。

当一个微扰 $W$ 作用于系统，使得原有的简并被解除时，有趣的动力学现象便会发生。假设在微扰作用下，原来的简并[本征态](@entry_id:149904) $|\phi_1\rangle, |\phi_2\rangle$ 分裂成两个新的、能量分别为 $E_1 \pm \delta$ 的本征态 $|\chi_\pm\rangle = (|\phi_1\rangle \pm |\phi_2\rangle)/\sqrt{2}$。如果系统初始处于 $|\psi(0)\rangle = |\phi_1\rangle = (|\chi_+\rangle + |\chi_-\rangle)/\sqrt{2}$，它就不再是新[哈密顿量](@entry_id:172864) $H' = H+W$ 的定态。它的演化将是 $|\psi(t)\rangle = (e^{-iE_+t/\hbar}|\chi_+\rangle + e^{-iE_-t/\hbar}|\chi_-\rangle)/\sqrt{2}$。概率密度 $|\psi(x,t)|^2$ 将包含一个干涉项，此项以角频率 $\omega = (E_+-E_-)/\hbar = 2\delta/\hbar$ [振荡](@entry_id:267781)。这种现象被称为 **[量子拍](@entry_id:155286) (quantum beats)**，是[简并解除](@entry_id:190366)后[相干叠加](@entry_id:170209)的直接后果 [@problem_id:2857776]。

#### [哈密顿量](@entry_id:172864)含时的情况：[弗洛凯理论](@entry_id:146392)

当[哈密顿量](@entry_id:172864)是时间周期性的，即 $H(t+T)=H(t)$，例如在周期性[激光](@entry_id:194225)场驱动的材料中，系统的动力学由 **[弗洛凯理论](@entry_id:146392) (Floquet theory)** 描述。其核心思想类似于固体物理中的[布洛赫定理](@entry_id:137461)，但应用于时间域。

[弗洛凯定理](@entry_id:175204)指出，对于周期[哈密顿量](@entry_id:172864)，薛定谔方程存在一组特解，形式为：
$$
|\psi_\alpha(t)\rangle = e^{-i\varepsilon_\alpha t/\hbar} |u_\alpha(t)\rangle
$$
其中 $|u_\alpha(t)\rangle$ 是与[哈密顿量](@entry_id:172864)具有相同周期的“弗洛凯模”，即 $|u_\alpha(t+T)\rangle = |u_\alpha(t)\rangle$。能量 $\varepsilon_\alpha$ 被称为 **[准能量](@entry_id:147199) (quasienergy)**。

为了理解这一点，我们定义 **频闪[演化算符](@entry_id:182628) (stroboscopic evolution operator)**，即演化一个周期 $T$ 的算符 $\hat{U}(T) \equiv \hat{U}(T,0)$。由于[哈密顿量](@entry_id:172864)的[厄米性](@entry_id:141899)，$\hat{U}(T)$ 是一个幺正算符，其[本征值](@entry_id:154894)必定位于复平面的单位圆上，可以写成 $e^{-i\varepsilon_\alpha T/\hbar}$ 的形式。这一定义直接导出了[准能量](@entry_id:147199) $\varepsilon_\alpha$ 的模糊性：由于 $e^{-i2\pi m}=1$（$m$为整数），[准能量](@entry_id:147199)仅在模 $\hbar\Omega = 2\pi\hbar/T$ 的意义下是确定的 [@problem_id:2857731]。

将弗洛凯解的形式代入演化过程，可以发现弗洛凯模的初态 $|u_\alpha(0)\rangle$ 正是频闪[演化算符](@entry_id:182628) $\hat{U}(T)$ 的本征态。由于 $\hat{U}(T)$ 是幺正的，我们可以形式上写出 $\hat{U}(T) = e^{-iH_F T/\hbar}$，从而定义一个不含时的 **[有效哈密顿量](@entry_id:748813) (effective Hamiltonian)** $H_F$。它的[本征值](@entry_id:154894)就是[准能量](@entry_id:147199) $\varepsilon_\alpha$。然而，由于[准能量](@entry_id:147199)的模糊性，$H_F$ 并非唯一。

完整的演化过程可以分解为一个由 $H_F$ 主导的平滑演化和一个周期性的“快速”[振荡](@entry_id:267781)，后者被称为 **微运动 (micromotion)**。这可以表示为[演化算符](@entry_id:182628)的分解：$\hat{U}(t,0) = \hat{P}(t)e^{-iH_F t/\hbar}$，其中 $\hat{P}(t)$ 是一个周期为 $T$ 的幺正算符，满足 $\hat{P}(0)=I$。在频闪观测的时刻 $t=nT$（$n$为整数），由于 $\hat{P}(nT)=\hat{P}(0)=I$，微运动的影响消失了，系统的演化完全由[有效哈密顿量](@entry_id:748813)决定：$\hat{U}(nT,0) = (e^{-iH_F T/\hbar})^n = (\hat{U}(T))^n$ [@problem_id:2857731]。

### 与场和势的相互作用

材料中电子的动力学行为很大程度上取决于它与内部[周期势](@entry_id:140652)以及外部场的相互作用。

#### [最小耦合](@entry_id:148226)与[规范不变性](@entry_id:137857)

当一个[电荷](@entry_id:275494)为 $q$ 的粒子在由标势 $\phi(\mathbf{r},t)$ 和[矢势](@entry_id:153642) $\mathbf{A}(\mathbf{r},t)$ 描述的[电磁场](@entry_id:265881)中运动时，其量子力学描述通过 **[最小耦合](@entry_id:148226) (minimal coupling)** 规则引入。该规则要求将[哈密顿量](@entry_id:172864)中的动量算符 $\hat{\mathbf{p}}$ 替换为[正则动量](@entry_id:155151) $\hat{\mathbf{p}} - q\mathbf{A}$。因此，对于一个在额外[势场](@entry_id:143025) $V(\mathbf{r})$ 中运动的粒子，其[哈密顿量](@entry_id:172864)为：
$$
\hat{H} = \frac{1}{2m}(\hat{\mathbf{p}} - q\mathbf{A})^2 + q\phi + V(\mathbf{r})
$$
[电磁势](@entry_id:266145)的选取存在自由度，即 **[规范变换](@entry_id:176521) (gauge transformation)**。一组新的势 $(\mathbf{A}', \phi')$ 与原势 $(\mathbf{A}, \phi)$ 如果描述的是完全相同的[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$，那么它们在物理上是等效的。这种变换由任意一个标量函数 $\chi(\mathbf{r},t)$ 产生：
$$
\mathbf{A} \to \mathbf{A}' = \mathbf{A} + \nabla\chi, \quad \phi \to \phi' = \phi - \frac{\partial\chi}{\partial t}
$$
物理学的基本要求是，物理定律的形式在[规范变换](@entry_id:176521)下应当保持不变，这即是 **[规范不变性](@entry_id:137857) (gauge invariance)** 原理。为了使薛定谔方程在这种变换下保持形式不变（协变），[波函数](@entry_id:147440) $\psi$ 必须同时经历一个相应的局域相位变换：
$$
\psi \to \psi' = e^{iq\chi/\hbar} \psi
$$
可以严格证明，在这一整套变换下，薛定谔方程 $i\hbar \frac{\partial \psi'}{\partial t} = \hat{H}'\psi'$ 与原方程具有完全相同的形式。更重要的是，所有物理可观测量，如概率密度 $|\psi'|^2 = |\psi|^2$ 和[概率流密度](@entry_id:152013) $\mathbf{j}' = \mathbf{j}$，都保持不变 [@problem_id:2857758]。这一深刻的对称性是现代物理学，包括标准模型，的基石之一。

#### 周期势中的动力学：[布洛赫振荡](@entry_id:138656)

在晶体中，电子在周期性[晶格](@entry_id:196752)势 $V(x)=V(x+a)$ 中运动。其[本征态](@entry_id:149904)是[布洛赫态](@entry_id:147552) $\psi_{nk}(x) = e^{ikx}u_{nk}(x)$，能量为 $\varepsilon_n(k)$，形成[能带结构](@entry_id:139379)。当一个恒定的外[电场](@entry_id:194326) $E$ 施加于晶体时，电子的行为会出乎经典直觉。

在单能带和[绝热近似](@entry_id:143074)下，电子的动力学可以用[半经典运动方程](@entry_id:138500)来描述。晶体动量 $k$ 的变化率由外力 $F_{ext} = -eE$ 决定：
$$
\hbar \frac{dk}{dt} = -eE
$$
积分可得 $k(t) = k(0) - \frac{eE}{\hbar}t$。[晶体动量](@entry_id:136369)随时间[线性增长](@entry_id:157553)。电子的群速度（即其期望速度）由能带的[色散关系](@entry_id:140395)决定：$\langle v \rangle = \frac{1}{\hbar}\frac{\partial \varepsilon_n(k)}{\partial k}$。将 $k(t)$ 代入，我们得到 $\langle v(t) \rangle = \frac{1}{\hbar}\frac{\partial \varepsilon_n}{\partial k}\big|_{k=k(t)}$。

关键在于，能带能量 $\varepsilon_n(k)$ 是 $k$ 的[周期函数](@entry_id:139337)，周期为[倒格矢](@entry_id:263351)的大小 $G = 2\pi/a$。因此，电子的速度 $\langle v(k) \rangle$ 也是 $k$ 的[周期函数](@entry_id:139337)。随着 $k(t)$ 线性地扫过整个[布里渊区](@entry_id:142395)，电子的速度先增加，在布里渊区边界附近由于有效质量变为负值而减小，甚至反向，然后周而复始。这种在[实空间](@entry_id:754128)中的周期性往复运动被称为 **[布洛赫振荡](@entry_id:138656) (Bloch oscillations)**。其周期 $T_B$ 是晶体动量改变一个[倒格矢](@entry_id:263351)所需的时间：
$$
\frac{eE}{\hbar}T_B = \frac{2\pi}{a} \implies T_B = \frac{2\pi\hbar}{eEa}
$$
这种纯粹的量子现象表明，在[理想晶体](@entry_id:138314)中，恒定[电场](@entry_id:194326)并不能产生持续的直流电流，而是导致电子在局域范围内[振荡](@entry_id:267781) [@problem_id:2857749]。

### [量子散射](@entry_id:147453)与束缚态

当电子与[晶格](@entry_id:196752)中的局域缺陷（如杂质、空位）相互作用时，其[波函数](@entry_id:147440)会发生散射或被束缚在缺陷周围。

#### [散射理论](@entry_id:143476)与[玻恩近似](@entry_id:138141)

散射问题旨在描述一个入射粒子（通常假定为平面波 $e^{i\mathbf{k}\cdot\mathbf{r}}$）与一个局域势 $V(\mathbf{r})$ 相互作用后的状态。薛定谔方程 $(-\frac{\hbar^2}{2m}\nabla^2+V)\psi = E\psi$ 可以改写为非齐次的亥姆霍兹方程：$(\nabla^2+k^2)\psi = \frac{2m}{\hbar^2}V\psi$，其中 $E=\frac{\hbar^2k^2}{2m}$。

利用格林函数方法，这个[微分方程](@entry_id:264184)可以转化为一个等价的积分方程，即 **[李普曼-施温格方程](@entry_id:142814) (Lippmann-Schwinger equation)**：
$$
\psi^{(+)}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} - \frac{m}{2\pi\hbar^2} \int d^3r' \frac{e^{ik|\mathbf{r}-\mathbf{r}'|}}{|\mathbf{r}-\mathbf{r}'|} V(\mathbf{r}')\psi^{(+)}(\mathbf{r}')
$$
这里的上标 $(+)$ 表示我们选择了满足向外[球面波](@entry_id:200471)边界条件的[格林函数](@entry_id:147802)。在远离散射中心的区域（$r\to\infty$），[波函数](@entry_id:147440)具有渐进行为 $\psi^{(+)}(\mathbf{r}) \to e^{i\mathbf{k}\cdot\mathbf{r}} + f(\mathbf{k}', \mathbf{k})\frac{e^{ikr}}{r}$，其中 $\mathbf{k}'=k\hat{\mathbf{r}}$ 是散射方向的波矢。系数 $f(\mathbf{k}',\mathbf{k})$ 被定义为 **[散射振幅](@entry_id:155369) (scattering amplitude)**，它的模方 $|f|^2$ 给出了[微分散射截面](@entry_id:172304)。

当[势场](@entry_id:143025) $V$ 较弱时，可以在[李普曼-施温格方程](@entry_id:142814)中进行迭代求解。**[一阶玻恩近似](@entry_id:201729) (First Born approximation)** 是将积分内的未知[波函数](@entry_id:147440) $\psi^{(+)}(\mathbf{r}')$ 用未受扰的入射波 $e^{i\mathbf{k}\cdot\mathbf{r}'}$ 代替。这给出散射振幅的表达式：
$$
f^{(1)}(\mathbf{k}', \mathbf{k}) = -\frac{m}{2\pi\hbar^2} \int d^3r' e^{-i(\mathbf{k}'-\mathbf{k})\cdot\mathbf{r}'} V(\mathbf{r}') = -\frac{m}{2\pi\hbar^2} \tilde{V}(\mathbf{q})
$$
其中 $\mathbf{q} = \mathbf{k}'-\mathbf{k}$ 是动量转移，$\tilde{V}(\mathbf{q})$ 是[势的傅里叶变换](@entry_id:149425)。这揭示了一个深刻的联系：在弱势极限下，[散射振幅](@entry_id:155369)正比于势在动量转移下的傅里叶分量 [@problem_id:2857750]。

例如，对于[半导体](@entry_id:141536)中的[杂质散射](@entry_id:267814)，其势场可以近似为 **[屏蔽库仑势](@entry_id:151053)（Yukawa势）** $V(r) = \frac{Ze^2}{4\pi\varepsilon} \frac{e^{-\kappa r}}{r}$。通过计算其[傅里叶变换](@entry_id:142120)，可以得到[一阶玻恩近似](@entry_id:201729)下的散射振幅：
$$
f^{(1)}(\theta) = -\frac{m^* Ze^2}{2\pi\varepsilon\hbar^2(\kappa^2 + q^2)} = -\frac{m^* Ze^2}{2\pi\varepsilon\hbar^2(\kappa^2 + 4k^2\sin^2(\theta/2))}
$$
其中 $\theta$ 是[散射角](@entry_id:171822)，$q=2k\sin(\theta/2)$ 是动量转移的大小，$\kappa$ 是屏蔽波数，$m^*$ 是电子的有效质量 [@problem_id:2857750]。

#### 束缚态：伯曼-施温格原理

对于吸引势 $V(r) \le 0$，除了[散射态](@entry_id:150968)（$E>0$），还可能存在 **束缚态 (bound states)**，即能量为负（$E0$）的、空间局域的定态解。确定给定[势场](@entry_id:143025)能支持多少个束缚态是一个核心问题。

**伯曼-施温格原理 (Birman-Schwinger principle)** 提供了一个强有力的数学工具。它指出，能量 $E=-\varepsilon$（$\varepsilon>0$）是[哈密顿量](@entry_id:172864) $H=H_0+V$ 的一个[本征值](@entry_id:154894)，当且仅当 1 是算符 $K_\varepsilon = \sqrt{|V|}(H_0+\varepsilon)^{-1}\sqrt{|V|}$ 的一个[本征值](@entry_id:154894)。其中 $H_0$ 是自由[哈密顿量](@entry_id:172864)，而 $|V|=-V$。

由于算符 $K_\varepsilon$ 随 $\varepsilon$ 的增加而单调减小，一个能量为 $E0$ 的束缚态存在，当且仅当 $K_0 = \lim_{\varepsilon\to 0^+} K_\varepsilon$ 算符至少有一个大于1的[本征值](@entry_id:154894)。因此，总的束缚态数目 $N$ 等于算符 $K_0$ 大于1的[本征值](@entry_id:154894)的个数。这可以进一步被放缩，得到一个[上界](@entry_id:274738)：
$$
N \le \sum_j \mu_j(0)^2 = \|K_0\|_{\mathrm{HS}}^2
$$
这里的 $\|K_0\|_{\mathrm{HS}}^2$ 是 $K_0$ 算符的[希尔伯特-施密特范数](@entry_id:265114)的平方，可以通过对其积分核的模方进行积分来计算。