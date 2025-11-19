## 引言
理解分子如何与光相互作用是现代化学、物理和[材料科学](@entry_id:152226)的核心。[电子激发](@entry_id:190531)态是这一相互作用的中心舞台，其性质决定了吸收光谱、光化学反应和光电转换效率等关键现象。然而，精确地从第一性原理计算这些[激发态](@entry_id:261453)的能量和性质是一项巨大的理论挑战，它要求我们求解复杂的多体薛定谔方程。为了在计算效率和精度之间取得平衡，发展可靠的近似方法至关重要。

在众多[激发态计算](@entry_id:749156)方法中，基于[格林函数](@entry_id:147802)理论的[代数图解构造](@entry_id:181010)（Algebraic Diagrammatic Construction, [ADC](@entry_id:186514)）方法脱颖而出。它提供了一个严谨、系统可改进且物理图像清晰的理论框架，用于计算[电子激发](@entry_id:190531)和相关过程。本文旨在为读者提供一个关于ADC方法的全面指南，它不仅阐述了其深刻的理论基础，也展示了其在解决实际科学问题中的强大能力。

为实现这一目标，本文将分为三个核心章节。在“原理与机制”一章中，我们将深入探讨ADC的理论基石，从[极化传播子](@entry_id:201288)和[戴森方程](@entry_id:146246)出发，剖析其“代数”、“图解”和“构造”的内涵，并建立ADC(n)的微扰层次。随后，“应用与跨学科[交叉](@entry_id:147634)”一章将通过一系列丰富的实例，展示ADC如何应用于模拟各类[光谱](@entry_id:185632)、处理具有挑战性的电子结构以及与其他理论相结合以包含更复杂的物理效应。最后，“动手实践”部分将提供一系列精心设计的计算练习，帮助读者巩固理论知识，并将其付诸实践。通过这一系列的学习，读者将能够全面掌握ADC方法，并将其作为强大的工具应用于自己的研究领域。

## 原理与机制

本章旨在阐述用于[极化传播子](@entry_id:201288)的[代数图解构造](@entry_id:181010) (Algebraic Diagrammatic Construction, [ADC](@entry_id:186514)) 方法背后的核心原理与机制。我们将从[线性响应理论](@entry_id:145737)中的[极化传播子](@entry_id:201288)出发，建立其与实验[可观测量](@entry_id:267133)（如吸收光谱）的联系。随后，我们将引入戴森式方程 (Dyson-like equation)，它为近似求解传播子提供了严谨的理论框架。在此基础上，我们将系统地剖析[ADC](@entry_id:186514)方法名称中“代数”、“图解”和“构造”三个部分的物理内涵，并详细介绍[ADC](@entry_id:186514)(n)方法的层次结构，重点阐述[ADC](@entry_id:186514)(1)和ADC(2)的构成。最后，我们会将ADC方法与时间相关的[Hartree-Fock](@entry_id:142303) (TDHF) 等其他主流方法进行比较，并讨论其关键的理论性质，如稳定性和[尺度一致性](@entry_id:199161)。

### [极化传播子](@entry_id:201288)：从物理响应到[谱表示](@entry_id:153219)

在[多体量子理论](@entry_id:202614)中，[传播子](@entry_id:139558)或格林函数是描述系统对微扰响应的核心工具。对于[电子激发](@entry_id:190531)过程，我们最关心的是系统如何响应一个含时的[电磁场](@entry_id:265881)，这由**[极化传播子](@entry_id:201288)** (polarization propagator) 来描述。为了精确地建立理论与实验的联系，我们需要区分两种密切相关但定义不同的传播子。

首先是**推迟响应函数** (retarded response function)，在零温下，对于一个厄米[单体](@entry_id:136559)算符 $\hat{\mu}$（例如[电偶极矩](@entry_id:178520)算符），其定义为：
$$
\chi^{\mathrm{R}}(t) = -i \theta(t) \langle \Psi_0 | [\hat{\mu}(t), \hat{\mu}(0)] | \Psi_0 \rangle
$$
其中 $|\Psi_0\rangle$ 是系统的精确[基态](@entry_id:150928)，$\hat{\mu}(t) = e^{i \hat{H} t} \hat{\mu} e^{-i \hat{H} t}$ 是[海森堡绘景](@entry_id:141162)下的算符，$\theta(t)$ 是亥维赛德[阶跃函数](@entry_id:159192)。由于 $\theta(t)$ 因子的存在，$\chi^{\mathrm{R}}(t)$ 对于 $t \lt 0$ 恒为零，这体现了物理上的**因果性** (causality)——响应不会发生在扰动之前。在[频域](@entry_id:160070)中，推迟响应函数的虚部与单[光子](@entry_id:145192)[吸收光谱](@entry_id:144611)直接相关，是理论计算需要最终获得的关键物理量。

然而，在[多体微扰理论](@entry_id:168555)的图解方法中，更自然出现的是**含时序的（或称因果的）[极化传播子](@entry_id:201288)** (time-ordered or causal polarization propagator)：
$$
P^{\mathrm{T}}(t) = -i \langle \Psi_0 | \mathcal{T}\, \hat{\mu}(t) \hat{\mu}(0) | \Psi_0 \rangle
$$
其中 $\mathcal{T}$ 是戴森 (Dyson) 的含时序算符，它将算符按时间先后顺序[排列](@entry_id:136432)。

这两种传播子的核心价值在于它们的**[谱表示](@entry_id:153219)** (spectral representation) 或称**勒曼表示** (Lehmann representation)，它将[传播子](@entry_id:139558)与系统的本征态联系起来。通过在算符之间插入[哈密顿量](@entry_id:172864) $\hat{H}$ 的完备本征态 $\{|n\rangle\}$，并进行[傅里叶变换](@entry_id:142120)，我们可以得到它们在[频域](@entry_id:160070) $\omega$ 中的表达式 [@problem_id:2873811]。对于推迟响应函数 $\chi^{\mathrm{R}}(\omega)$，其[谱表示](@entry_id:153219)为：
$$
\chi^{\mathrm{R}}(\omega) = \sum_{n \neq 0} |\mu_{0n}|^2 \left[ \frac{1}{\omega - \Omega_{n0} + i\eta} - \frac{1}{\omega + \Omega_{n0} + i\eta} \right]
$$
而对于含时序传播子 $P^{\mathrm{T}}(\omega)$，其[谱表示](@entry_id:153219)为：
$$
P^{\mathrm{T}}(\omega) = \sum_{n \neq 0} |\mu_{0n}|^2 \left[ \frac{1}{\omega - \Omega_{n0} + i\eta} - \frac{1}{\omega + \Omega_{n0} - i\eta} \right]
$$
在这里，$\Omega_{n0} = E_n - E_0$ 是从[基态](@entry_id:150928)到[激发态](@entry_id:261453) $|n\rangle$ 的精确**[激发能](@entry_id:190368)**，$\mu_{0n} = \langle 0 | \hat{\mu} | n \rangle$ 是**跃迁矩**，$\eta$ 是一个趋于零的正无穷小量。

通过比较这两个[谱表示](@entry_id:153219)，我们可以发现它们在复[频域](@entry_id:160070)平面上的解析结构有显著不同。$\chi^{\mathrm{R}}(\omega)$ 的所有极点（位于 $\Omega_{n0} - i\eta$ 和 $-\Omega_{n0} - i\eta$）都位于复平面的下半部分，这是其因果性的直接数学体现。相反，$P^{\mathrm{T}}(\omega)$ 的极点则[分布](@entry_id:182848)在复平面的上下两侧（位于 $\Omega_{n0} - i\eta$ 和 $-\Omega_{n0} + i\eta$）。正是由于 $\chi^{\mathrm{R}}(\omega)$ 在上半复平面的[解析性](@entry_id:140716)，其在实轴上的实部和虚部通过**[克拉默斯-克勒尼希关系](@entry_id:140966)** (Kramers-Kronig relations) 相互关联 [@problem_id:2873811]。

尽管解析结构不同，但在实轴上，它们的虚部之间存在一个至关重要的简单关系。利用索霍茨基-普列梅利定理 ($\lim_{\eta \to 0^+} \frac{1}{x \pm i\eta} = \mathcal{P}\frac{1}{x} \mp i\pi \delta(x)$)，可以证明：
$$
\mathrm{Im}\,\chi^{\mathrm{R}}(\omega) = \operatorname{sgn}(\omega)\,\mathrm{Im}\,P^{\mathrm{T}}(\omega)
$$
其中 $\operatorname{sgn}(\omega)$ 是[符号函数](@entry_id:167507)。这个关系意味着，只要我们能计算出理论上更自然的含时序传播子 $P^{\mathrm{T}}(\omega)$，我们就可以直接获得物理上可观测的推迟响应函数 $\chi^{\mathrm{R}}(\omega)$ 的虚部，从而得到吸收光谱。[ADC](@entry_id:186514)方法的核心任务正是近似计算 $P^{\mathrm{T}}(\omega)$。

### [戴森方程](@entry_id:146246)与不可约极化部分

直接计算含时序传播子 $P^{\mathrm{T}}(\omega)$ 仍然非常困难，因为它包含了无穷多类的相互作用过程。[多体理论](@entry_id:169452)通过引入一个更基本的构成单元——**不可约极化部分** (irreducible polarization part) $\Pi(\omega)$，来简化此问题。

我们可以从两个角度理解 $P(\omega)$ 和 $\Pi(\omega)$ 的区别 [@problem_id:2873814]。在[线性响应](@entry_id:146180)的物理图像中，$P(\omega)$ 将系统的感生密度响应 $\delta n(\omega)$ 与**外部微扰势** $\delta v_{\mathrm{ext}}(\omega)$ 联系起来，即 $\delta n = P \delta v_{\mathrm{ext}}$。而 $\Pi(\omega)$ 则将密度响应与**总有效势** $\delta v_{\mathrm{tot}}(\omega)$ 联系起来，$\delta v_{\mathrm{tot}}$ 是外部势与由感生密度自身产生的感生势之和。在图解语言中，$\Pi(\omega)$ 被定义为所有无法通过切断一条[库仑相互作用](@entry_id:747947)线 $v$ 而分成两个独立部分的图的总和，因此被称为“不可约”。而 $P(\omega)$ 则包含了所有可约和不可约的图。

这两个量通过一个精确的**戴森式方程**联系在一起：
$$
P(\omega) = \Pi(\omega) + \Pi(\omega) \, v \, P(\omega)
$$
其中 $v$ 是裸[库仑相互作用](@entry_id:747947)算符。这个方程可以形式上求解为 $P = (1 - \Pi v)^{-1} \Pi$。这个方程的结构至关重要：它将复杂的全[传播子](@entry_id:139558) $P(\omega)$ 分解为一个更简单的“种子”部分 $\Pi(\omega)$ 和一个通过库仑相互作用 $v$ 进行的迭代“传播”过程。这意味着，如果我们能找到一个对不可约部分 $\Pi(\omega)$ 的良好近似，我们就可以通过[戴森方程](@entry_id:146246)（代数上）[重求和](@entry_id:275405)，从而得到一个包含了无穷阶微扰效应的、非微扰的全传播子 $P(\omega)$ 的近似。这正是[ADC](@entry_id:186514)以及许多其他现代多体方法的基本策略。

### [代数图解构造](@entry_id:181010) (ADC) 的核心思想

ADC方法为系统地近似[极化传播子](@entry_id:201288)提供了一个强大而严谨的框架。其名称中的三个词——“代数”、“图解”和“构造”——精确地概括了该方法的核心步骤。

**“图解” (Diagrammatic)**：[ADC](@entry_id:186514)方法的理论基础是[多体微扰理论](@entry_id:168555) (Many-Body Perturbation Theory, MBPT)。它采用Møller-Plesset (MP) 分配方案，将系统的[哈密顿量](@entry_id:172864)分为一个零阶的[福克算符](@entry_id:139887) (Fock operator) $\hat{F}$ 和一个微扰项——涨落势 (fluctuation potential) $\hat{W}$。利用维克定理 (Wick's theorem) 和基于[Hartree-Fock](@entry_id:142303) (HF) [基态](@entry_id:150928)的正常序，可以将[极化传播子](@entry_id:201288)展开成关于 $\hat{W}$ 的[微扰级数](@entry_id:266790)，这个级数中的每一项都可以用一个费曼图来表示 [@problem_id:2873786]。

**“构造” (Construction)**：ADC的精髓在于它不直接截断全传播子 $P(\omega)$ 的[微扰级数](@entry_id:266790)，因为这样做会破坏其固有的极点结构。相反，[ADC](@entry_id:186514)方法选择对更基本的**不可约**部分 $\Pi(\omega)$（或与之密切相关的自能部分）进行系统性的微扰截断 [@problem_id:2873855]。一个$n$阶的[ADC](@entry_id:186514)方案，即**ADC(n)**，其核心就是将不可约部分的[微扰展开](@entry_id:159275)式截断到$n$阶，即 $\Pi(\omega) \approx \Pi^{(n)}(\omega) = \sum_{k=1}^{n} \Pi^{[k]}(\omega)$。然后，利用这个近似的不可约部分，通过某种方式“求解”[戴森方程](@entry_id:146246)，从而“构造”出全[传播子](@entry_id:139558)的一个非微扰近似。

**“Algebraic” (代数)**：这是[ADC](@entry_id:186514)方法最具特色的一步。传统方法中，使用近似的 $\Pi^{(n)}(\omega)$ 求解[戴森方程](@entry_id:146246)仍会得到一个复杂的、依赖于频率 $\omega$ 的方程。ADC方法通过引入**中间态表示** (Intermediate State Representation, ISR) 将此问题巧妙地转化为一个与频率无关的、标准的**[厄米矩阵](@entry_id:155147)本征值问题** [@problem_id:2873834]。

ISR的[基矢](@entry_id:199546)是通过将粒子-空穴 (particle-hole) 激发算符作用在（关联的）[基态](@entry_id:150928)上生成的。例如，$1p1h$ 中间态形如 $\hat{N}(\hat{a}_a^\dagger \hat{a}_i)|\Psi_0\rangle$，$2p2h$ 中间态形如 $\hat{N}(\hat{a}_a^\dagger \hat{a}_b^\dagger \hat{a}_j \hat{a}_i)|\Psi_0\rangle$，等等（其中 $\hat{N}$ 表示正常序）。至关重要的是，ADC方法通过一个正交化过程（如[对称正交化](@entry_id:167626)）将这些通常非正交的[基矢](@entry_id:199546)转化为一组**标准正交基** $\{|\widetilde{\Psi}_I\rangle\}$，满足 $\langle \widetilde{\Psi}_I | \widetilde{\Psi}_J \rangle = \delta_{IJ}$。在此[基矢](@entry_id:199546)下，[传播子](@entry_id:139558)问题最终可以表示为一个[厄米矩阵](@entry_id:155147)的[本征值方程](@entry_id:192306)：
$$
\mathbf{M}\mathbf{Y}_K = \Omega_K \mathbf{Y}_K
$$
其中 $\mathbf{M}$ 是**ADC矩阵**（或称有效哈密顿量矩阵），其[矩阵元](@entry_id:186505)为 $M_{IJ} = \langle \widetilde{\Psi}_I | (\hat{H} - E_0) | \widetilde{\Psi}_J \rangle$。这个矩阵的[本征值](@entry_id:154894) $\Omega_K$ 直接给出了系统的[激发能](@entry_id:190368)，而本征矢量 $\mathbf{Y}_K$ 则包含了跃迁强度的信息。通过这种代数构造，ADC将一个动态的（频率依赖的）响应问题转化为了一个静态的（与频率无关的）[矩阵对角化](@entry_id:138930)问题，这不仅大大简化了计算，也保证了计算出的激发能始终为实数。

### ADC(n) 方法的层次结构

[ADC](@entry_id:186514)方法提供了一个系统的、可逐步改进的近似层次，称为ADC(n)方案。阶数$n$越高，包含的电子相关效应越精确，计算成本也越高。

#### [ADC](@entry_id:186514)(1): 与 CIS 和 TDA 的联系

[ADC](@entry_id:186514)(1)是[ADC](@entry_id:186514)层次结构中最简单的一级。根据[ADC](@entry_id:186514)的构造规则，ADC(1)的有效哈密顿量矩阵 $\mathbf{M}$ 的矩阵元需要精确到微扰的一阶。在仅包含 $1p1h$ 激发的中间态空间中，这意味着 [@problem_id:2873831]：
*   对角元 $M_{ia,ia}$ 包含零阶的[轨道](@entry_id:137151)能差 $(\epsilon_a - \epsilon_i)$ 和[一阶修正](@entry_id:155896)（对于此对角元为零）。
*   非对角元 $M_{ia,jb}$ 由一阶微扰，即涨落势 $\hat{W}$ 的矩阵元 $\langle \Phi_i^a | \hat{W} | \Phi_j^b \rangle$ 给出，这对应于两个电子的[相互作用积分](@entry_id:167594)。

将这些组合起来，[ADC](@entry_id:186514)(1)的久期矩阵恰好与**[单激发组态相互作用](@entry_id:174866)** (Configuration Interaction Singles, CIS) 方法的[哈密顿量](@entry_id:172864)矩阵完全相同。对于闭壳层体系，CIS又等价于对TDHF方程进行**[Tamm-Dancoff近似](@entry_id:178323)** (TDA)。因此，ADC(1)在激发能和跃迁强度方面与CIS/TDA是完全等价的。

这一结果的深层原因与**[布里渊定理](@entry_id:166170)** (Brillouin's theorem) 有关 [@problem_id:2873858]。该定理指出，对于一个正则HF参考态 $|\Phi_0\rangle$，完整的[哈密顿量](@entry_id:172864)在[基态](@entry_id:150928)和任意单[激发态](@entry_id:261453) $|\Phi_i^a\rangle$ 之间的矩阵元为零，即 $\langle \Phi_0 | \hat{H} | \Phi_i^a \rangle = 0$。这意味着涨落势的一阶耦合项 $\langle \Phi_0 | \hat{W} | \Phi_i^a \rangle$ 也为零。这保证了在最低阶的非平庸近似中，[激发态](@entry_id:261453)空间与HF[基态](@entry_id:150928)是[解耦](@entry_id:637294)的，可以将问题完全限制在 $1p1h$ 空间内解决，从而得到了CIS/TDA形式的理论。

#### [ADC](@entry_id:186514)(2): 引入双激发组态

[ADC](@entry_id:186514)(1)/CIS/TDA完全忽略了[激发态](@entry_id:261453)中的动态电子相关效应。为了系统地改进描述，ADC(2)方法将中间态空间扩展到包含 $1p1h$ 和 $2p2h$ 组态。根据[ADC](@entry_id:186514)(n)的构造规则，ADC(2)的久期矩阵 $\mathbf{M}$ 的各个块需要满足特定的微扰阶数精度 [@problem_id:2873786] [@problem_id:2873818]：
*   **$1p1h \leftrightarrow 1p1h$ 块**：其[矩阵元](@entry_id:186505)通过与 $2p2h$ 态的耦合，被有效地修正到[二阶精度](@entry_id:137876)。
*   **$1p1h \leftrightarrow 2p2h$ 块**：此耦合块由涨落势 $\hat{W}$ 直接连接，因此其[矩阵元](@entry_id:186505)在一阶是精确的。
*   **$2p2h \leftrightarrow 2p2h$ 块**：在“严格”[ADC](@entry_id:186514)(2)方案中，此块仅需零阶精度，即对角元为零阶的[轨道](@entry_id:137151)能之和 $(\epsilon_a+\epsilon_b-\epsilon_i-\epsilon_j)$，非对角元为零。

ADC(2)的关键进步在于包含了 $1p1h$ 和 $2p2h$ 态之间的耦合 [@problem_id:2873818]。在图解语言中，这对应于一个 $1p1h$ 态通过一次 $\hat{W}$ 相互作用散射成一个虚的 $2p2h$ 态，然后再通过一次 $\hat{W}$ 相互作用散射回一个 $1p1h$ 态的过程。这个 $1p1h \to 2p2h \to 1p1h$ 的过程对 $1p1h$ 态的能量给出了一个[二阶修正](@entry_id:199233)。因此，[ADC](@entry_id:186514)(2)是捕获了超越CIS/TDA的最低阶相关效应的ADC方法 [@problem_id:2873858]。

此外，由于ADC(2)的久期矩阵中明确包含了 $2p2h$ 空间，其本征谱中自然会出现以 $2p2h$ 组态为主导的[本征态](@entry_id:149904)。这些态对应于**[双激发态](@entry_id:187815)**，尽管在严格ADC(2)中它们的激发能仅有零阶精度，但这使得ADC(2)原则上能够描述TDHF/CIS等单激发方法完全无法处理的双激发过程 [@problem_id:2873818]。

#### ADC(n)的系统一致性

[ADC](@entry_id:186514)(n)方案的一个核心优点是其**系统一致性** (systematic consistency) [@problem_id:2873855]。对于主要由单[粒子-空穴激发](@entry_id:137289)构成的[激发态](@entry_id:261453)（通常是[光谱](@entry_id:185632)中较强的跃迁），ADC(n)方法计算出的激发能（即传播子的[极点位置](@entry_id:271565)）与精确的MBPT展开结果在微扰的$n$阶上是一致的。同时，相应的跃迁强度（与[传播子](@entry_id:139558)的留数相关）在$n-1$阶上是一致的。这一特性保证了ADC(n)是一个层次清晰、可系统改进的理论体系，用户可以通过选择不同的阶数$n$来平衡计算精度和成本。

### 与其他方法的比较及理论性质

#### ADC与TDHF/RPA：非厄米问题与不稳定性

计算[激发光谱](@entry_id:139562)最常用的方法之一是时间相关的[Hartree-Fock](@entry_id:142303) (TDHF) 理论，它等价于**[随机相位近似](@entry_id:754035)** (Random Phase Approximation, RPA)。TDHF/RPA的控制方程，即**[卡西达方程](@entry_id:183031)** (Casida equation)，可以写成一个广义本征值问题 [@problem_id:2873787]：
$$
\begin{pmatrix} \mathbf{A}  \mathbf{B} \\ \mathbf{B}^*  \mathbf{A}^* \end{pmatrix}
\begin{pmatrix} X \\ Y \end{pmatrix}
= \omega
\begin{pmatrix} \mathbf{1}  \mathbf{0} \\ \mathbf{0}  -\mathbf{1} \end{pmatrix}
\begin{pmatrix} X \\ Y \end{pmatrix}
$$
由于右侧度规矩阵 $(\begin{smallmatrix} \mathbf{1}  \mathbf{0} \\ \mathbf{0}  -\mathbf{1} \end{smallmatrix})$ 的不定性，这是一个**非厄米**的[本征值问题](@entry_id:142153)。当底层的HF参考态不稳定时（即违反Thouless稳定性条件），该方程可能产生复数[本征值](@entry_id:154894) $\omega$，对应于虚假的激发或[基态](@entry_id:150928)的衰变。

与此形成鲜明对比的是，[ADC](@entry_id:186514)方法通过其代数构造，在任何阶数下都产生一个标准的**厄米[本征值问题](@entry_id:142153)** $\mathbf{M}\mathbf{Y} = \Omega \mathbf{Y}$。[厄米矩阵](@entry_id:155147)的[本征值](@entry_id:154894)保证为实数。因此，[ADC](@entry_id:186514)方法在结构上避免了RPA中可能出现的非厄米不稳定性问题，使其成为一个更加稳健的计算方案。ADC的厄米化是一个深刻的理论构造，而非像TDA那样简单地丢弃$\mathbf{B}$矩阵。这种构造可以被理解为将具有不定性度规的精确传播子[代数结构](@entry_id:137052)，通过一个[合同变换](@entry_id:154837)，映射到一个具有正定度规（标准正交基）的中间态表示中，从而根除了不稳定的可能性 [@problem_id:2873787]。

#### [ADC](@entry_id:186514)的[尺度一致性](@entry_id:199161)

在[量子化学](@entry_id:140193)中，一个高质量的近似方法应具备**[尺度一致性](@entry_id:199161)** (size-consistency)。对于激发能这一[内含性质](@entry_id:181209) (intensive property)，[尺度一致性](@entry_id:199161)意味着对于一个由两个无限远、无相互作用的子系统 $A$ 和 $B$ 组成的超分子，其[激发能](@entry_id:190368)谱应该是子系统 $A$ 和 $B$ 各自激发能谱的简单并集。

[ADC](@entry_id:186514)(n)方法在任意阶数$n$下都严格满足[激发能](@entry_id:190368)的[尺度一致性](@entry_id:199161) [@problem_id:2873824]。其根本原因在于[ADC](@entry_id:186514)是基于**连通图** (connected diagrams) 的[微扰展开](@entry_id:159275)。对于无相互作用的子系统，不存在可以连接两个子系统的相互作用线，因此任何一个[连通图](@entry_id:264785)都必须完[全局域](@entry_id:196542)在某一个子系统上。这导致超分子的ADC[有效哈密顿量](@entry_id:748813)矩阵 $\mathbf{M}$ 在局域化的中间态[基矢](@entry_id:199546)下呈现出完美的[块对角结构](@entry_id:746869)：
$$
\mathbf{M}_{A \oplus B} = \begin{pmatrix} \mathbf{M}_A  \mathbf{0} \\ \mathbf{0}  \mathbf{M}_B \end{pmatrix}
$$
对角化这个矩阵自然会得到两个子系统谱的并集。同样，跃迁强度这样的[广延性质](@entry_id:145410) (extensive property) 也会正确地相加，即具备**[尺度广延性](@entry_id:144932)** (size-extensivity)。

值得注意的是，尽管[ADC](@entry_id:186514)理论上是尺度一致的，但在实际的超分子计算中，为了保证这一性质，必须采取特定的策略。如果使用标准的[正则分子轨道](@entry_id:197442)，不同子系统之间偶然的[轨道能级](@entry_id:151753)简并会导致[轨道混合](@entry_id:188404)，从而人为地引入非物理的子系统间耦合，破坏[尺度一致性](@entry_id:199161)。正确的做法是使用能够保持子系统独立性的[轨道](@entry_id:137151)[基矢](@entry_id:199546)，例如局域化分子[轨道](@entry_id:137151)或由各子系统[正则轨道](@entry_id:183413)直接拼接而成的块[正则轨道](@entry_id:183413) [@problem_id:2873824]。