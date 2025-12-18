## 引言
在原子尺度上理解物质如何响应外部刺激（如光照或高能粒子撞击）是现代科学的核心挑战之一。这些过程的核心是电子与[原子核](@entry_id:167902)在飞秒（$10^{-15}$秒）时间尺度上的复杂耦合动力学。[含时密度泛函理论](@entry_id:200019)（Time-Dependent Density Functional Theory, TDDFT）作为一种强大的第一性原理计算方法，为直接模拟这些超快非平衡过程提供了坚实的理论框架。然而，从其深刻的理论基础到多样化的实际应用，TDDFT涉及广泛而复杂的概念，对于初学者而言，构建一个清晰、连贯的知识体系颇具挑战。

本文旨在弥合这一知识鸿沟，为研究生水平的学习者提供一份关于动力学TDDFT的结构化指南。我们将系统地从理论根基出发，逐步过渡到前沿应用和动手实践。读者将跟随本文的脉络，全面掌握TDDFT的来龙去脉：

第一章，“原理与机制”，将深入剖析TDDFT的理论核心。我们将从含时[科恩-沈方法](@entry_id:263733)出发，阐明如何将一个棘手的[多体问题](@entry_id:138087)转化为可解的单粒子问题，并详细介绍[实时传播](@entry_id:199067)与线性响应这两种主流计算[范式](@entry_id:161181)，最后将聚焦于该理论最关键的近似——[绝热近似](@entry_id:143074)及其局限性。

第二章，“应用与跨学科交叉”，将展示TDDFT作为一个通用工具，如何在化学、物理和[材料科学](@entry_id:152226)等领域大放异彩。通过具体案例，我们将探索其在模拟[光化学反应](@entry_id:184924)、[辐射损伤](@entry_id:160098)、超快磁学等前沿问题中的强大能力。

最后，在“动手实践”部分，我们将理论付诸实践。通过一系列精心设计的编程问题，读者将亲手实现TDDFT模拟的关键环节，从而巩固理论知识，并获得解决实际研究问题的宝贵技能。

## 原理与机制

本章旨在深入探讨[含时密度泛函理论](@entry_id:200019)（Time-Dependent Density Functional Theory, TDDFT）用于模拟动力学的核心原理和基本机制。我们将从该理论的基石——含时科恩-沈（Kohn-Sham, KS）方法出发，逐步解析其在实际计算中的两种主要应用形式：[实时传播](@entry_id:199067)（real-time propagation）和[线性响应](@entry_id:146180)（linear response）。在此过程中，我们将阐述如何求解含时[科恩-沈方程](@entry_id:143968)、如何将电子动力学与[原子核](@entry_id:167902)运动耦合，以及如何从理论计算中提取可观测量，如电子激发[光谱](@entry_id:185632)。最后，我们将重点剖析当前 TDDFT 方法中应用最广的[绝热近似](@entry_id:143074)（adiabatic approximation）及其局限性，特别是在描述[电荷转移](@entry_id:155270)等关键[化学物理](@entry_id:199585)过程中的挑战与前沿进展。

### 含时[科恩-沈方法](@entry_id:263733)：从多体到[单体](@entry_id:136559)

[含时密度泛函理论](@entry_id:200019)的中心思想，是通过一个巧妙的理论构建，将一个含相互作用的、极其复杂的真实多电子体系的动力学问题，精确地映射到一个虚拟的、无相互作用的辅助体系上。这个虚拟体系被称为 **含时科恩-沈（time-dependent Kohn-Sham, TDKS）体系**。这一映射的精髓在于，尽管科恩-沈体系中的“电子”是无相互作用的，但其演化被精心设计，以使其 **电子密度** $n(\mathbf{r},t)$ 在任意时刻、任意空间点都与真实的、含相互作用的体系完全一致。这一映射的可能性由 **Runge-Gross 定理** 提供了严格的理论保证。

理解 TDDFT 的关键在于区分两种核心[势场](@entry_id:143025)：**外势** $v_{\mathrm{ext}}(\mathbf{r},t)$ 和 **科恩-沈有效势** $v_{\mathrm{KS}}(\mathbf{r},t)$ 。

**外势** $v_{\mathrm{ext}}(\mathbf{r},t)$ 是物理上真实存在的势场。它描述了电子体系与外部环境的相互作用。在分子体系中，这主要包括电子与[原子核](@entry_id:167902)之间的静电吸引势。如果体系还受到外加[电磁场](@entry_id:265881)（如激光脉冲）的作用，该场的势也会作为外势的一部分。简而言之，$v_{\mathrm{ext}}(\mathbf{r},t)$ 是所有源于电子系统之外的势的总和。

**科恩-沈有效势** $v_{\mathrm{KS}}(\mathbf{r},t)$ 则是一个理论构造出的、作用于虚拟的无相互作用电子的有效势。它的目的是迫使这个无相互作用体系的密度演化与真实体系保持一致。根据其定义，科恩-沈有效势可以精确地分解为三个部分：

$v_{\mathrm{KS}}(\mathbf{r},t) = v_{\mathrm{ext}}(\mathbf{r},t) + v_{\mathrm{H}}[n](\mathbf{r},t) + v_{\mathrm{xc}}[n;\Psi_0,\Phi_0](\mathbf{r},t)$

其中：
1.  $v_{\mathrm{ext}}(\mathbf{r},t)$ 与物理体系中的外势完全相同。
2.  **哈特里（Hartree）势** $v_{\mathrm{H}}[n](\mathbf{r},t)$ 是一个依赖于密度 $n(\mathbf{r},t)$ 的泛函，它描述了电子之间经典的、平均化的库仑排斥作用。其表达式为：
    $v_{\mathrm{H}}[n](\mathbf{r},t) = \int \mathrm{d}^3r' \frac{n(\mathbf{r}',t)}{|\mathbf{r}-\mathbf{r}'|}$
3.  **交换-相关（exchange-correlation, xc）势** $v_{\mathrm{xc}}$ 是 TDDFT 的核心，也是其所有复杂性的集中体现。它包含了所有超越经典平均场（哈特里）描述的量子[多体效应](@entry_id:173569)。这包括电子的[泡利不相容原理](@entry_id:141850)所导致的交换作用，以及电子运动因库仑排斥而相互回避所产生的相关作用。原则上，$v_{\mathrm{xc}}$ 是电子密度 $n$ 的一个复杂泛函，并且可能依赖于体系的初始状态（$\Psi_0$ 和 $\Phi_0$）以及密度的历史演化（即“[记忆效应](@entry_id:266709)”）。

总结而言，$v_{\mathrm{ext}}$ 是物理输入，而 $v_{\mathrm{KS}}$ 是一个巧妙构造的工具，它通过包含 $v_{\mathrm{H}}$ 和 $v_{\mathrm{xc}}$，将真实体系中复杂的[电子-电子相互作用](@entry_id:139900)“内化”为一个附加的单粒子[势场](@entry_id:143025)。这样，求解含时多体薛定谔方程这一几乎不可能的任务，就转化为了求解一组耦合的单粒子方程——**含时[科恩-沈方程](@entry_id:143968)**：

$i\hbar \frac{\partial}{\partial t} \psi_k(\mathbf{r},t) = \left[ -\frac{\hbar^2}{2m_e}\nabla^2 + v_{\mathrm{KS}}(\mathbf{r},t) \right] \psi_k(\mathbf{r},t)$

其中 $\psi_k(\mathbf{r},t)$ 是第 $k$ 个[科恩-沈轨道](@entry_id:171979)，体系的总密度由这些[轨道](@entry_id:137151)构建：$n(\mathbf{r},t) = \sum_k f_k |\psi_k(\mathbf{r},t)|^2$（$f_k$ 为[轨道](@entry_id:137151)占据数）。由于 $v_{\mathrm{KS}}$ 依赖于密度 $n$，而 $n$ 又依赖于[科恩-沈轨道](@entry_id:171979) $\psi_k$，这组方程是自洽的、[非线性](@entry_id:637147)的。

虽然 Runge-Gross 定理保证了精确的 $v_{\mathrm{xc}}$ 存在，但其确切形式是未知的。因此，TDDFT 的所有实际应用都依赖于对 $v_{\mathrm{xc}}$ 的近似。这一近似的优劣直接决定了 TDDFT 计算的准确性。从另一个角度看，如果已知一个体系在某个外势下演化出的精确密度 $n(\mathbf{r},t)$，原则上可以通过“[逆向工程](@entry_id:754334)”反推出产生该密度所需的精确[科恩-沈势](@entry_id:169598) $v_{\mathrm{s}}(x,t)$ 。这进一步强调了密度与势之间深刻的内在联系，是 TDDFT 理论的基石。

### 实时动力学模拟

#### 求解含时[科恩-沈方程](@entry_id:143968)

实时 TDDFT 的核心任务是直接求解含时[科恩-沈方程](@entry_id:143968)，以获得体系密度随时间的演化。这是一个[初值问题](@entry_id:144620)：给定初始时刻 $t=0$ 的[科恩-沈轨道](@entry_id:171979)，我们需要在数值上积分这组[偏微分方程](@entry_id:141332)。

形式上，从时间 $t$ 到 $t+\Delta t$ 的演化由一个[时间演化算符](@entry_id:196774) $\hat{U}(t+\Delta t, t)$ 描述：

$\psi_k(t+\Delta t) = \hat{U}(t+\Delta t, t) \psi_k(t) = \mathcal{T} \exp\left(-\frac{i}{\hbar} \int_t^{t+\Delta t} \hat{H}_{\mathrm{KS}}(t') dt'\right) \psi_k(t)$

其中 $\hat{H}_{\mathrm{KS}}(t) = \hat{T} + \hat{V}_{\mathrm{KS}}(t)$ 是科恩-沈[哈密顿算符](@entry_id:144286)（$\hat{T}$ 是[动能算符](@entry_id:265633)，$\hat{V}_{\mathrm{KS}}$ 是乘势算符），$\mathcal{T}$ 是[时间排序算符](@entry_id:148044)。由于 $\hat{H}_{\mathrm{KS}}(t)$ 在不同时刻通常不对易，直接计算此指数算符非常困难。因此，必须采用[数值积分](@entry_id:136578)算法。

选择合适的[积分算法](@entry_id:192581)至关重要。一个看似简单的选择是**[前向欧拉法](@entry_id:141238)（forward Euler method）**，但它存在致命缺陷 。前向欧拉法的[演化算符](@entry_id:182628)近似为 $\hat{U}_{\mathrm{FE}} \approx \hat{I} - i \Delta t \hat{H}_{\mathrm{KS}}/\hbar$，它不是一个幺正算符。这意味着在演化过程中，波[函数的范数](@entry_id:275551)（即总粒子数）不守恒，通常会指数式地增长，导致模拟发散。

为了保证物理上的正确性（粒子数守恒），[数值积分器](@entry_id:752799)必须是**幺正的（unitary）**。一个广泛使用且性能优越的方法是**分裂算符（split-operator）法**。该方法利用 Baker-Campbell-Hausdorff (BCH) 公式，将[哈密顿量](@entry_id:172864)分解为动能部分 $\hat{T}$ 和[势能](@entry_id:748988)部分 $\hat{V}_{\mathrm{KS}}$。由于 $[\hat{T}, \hat{V}_{\mathrm{KS}}] \neq 0$，它们的指数不能简单地相乘。但对于一个小的 时间步长 $\Delta t$，可以使用对称的 **Strang 分裂**：

$\exp\left(-\frac{i}{\hbar} (\hat{T}+\hat{V}_{\mathrm{KS}}) \Delta t\right) \approx \exp\left(-\frac{i}{2\hbar} \hat{V}_{\mathrm{KS}} \Delta t\right) \exp\left(-\frac{i}{\hbar} \hat{T} \Delta t\right) \exp\left(-\frac{i}{2\hbar} \hat{V}_{\mathrm{KS}} \Delta t\right) + \mathcal{O}(\Delta t^3)$

这种二阶分裂方法所构造的近似[演化算符](@entry_id:182628)是幺正的，并且具有**时间反演对称性**。这意味着它能精确地保持波[函数范数](@entry_id:165870)，并具有良好的[长期稳定性](@entry_id:146123)。

在实际实现中，[分裂算符法](@entry_id:140717)的效率极高 。[对势能](@entry_id:203104)算符指数的应用只是在实空间（$x$-space）对[波函数](@entry_id:147440)进行逐点乘上一个相位因子。而对[动能算符](@entry_id:265633)指数的应用，则利用**[傅里叶变换](@entry_id:142120)（Fourier Transform）**。在动量空间（$k$-space）中，[动能算符](@entry_id:265633) $\hat{T} = \hat{p}^2/(2m_e)$ 变成了一个简单的乘法算符 $\hbar^2 k^2/(2m_e)$。因此，动能演化步骤可以通过以下流程高效完成：
1.  将[波函数](@entry_id:147440)从实空间快速傅里叶变换（FFT）到动量空间。
2.  在[动量空间](@entry_id:148936)中，乘以动能对应的相位因子。
3.  通过逆 FFT 将结果变换回[实空间](@entry_id:754128)。

这种结合了分裂算符和谱方法（FFT）的策略，是实时 TDDFT 模拟中最常用和最可靠的技术之一。

#### 耦合电子-原子[核动力学](@entry_id:752701)：Ehrenfest 方法

在分子和材料中，电子的运动与[原子核](@entry_id:167902)的运动是紧密耦合的。一个常见的处理这种耦合动力学的方法是 **Ehrenfest 方法**。该方法将[原子核](@entry_id:167902)视为经典粒子，其运动遵循[牛顿第二定律](@entry_id:274217)，而作用在[原子核](@entry_id:167902)上的力则由量子化的电子系统提供。

具体来说，在 Ehrenfest-TDDFT 框架下，[原子核](@entry_id:167902)在时刻 $t$ 受到的力 $\mathbf{F}_I$ 是通过计算电子系统在该时刻的总能量对[原子核](@entry_id:167902)位置 $\mathbf{R}_I$ 的[期望值](@entry_id:153208)的负梯度得到的。这导致了一组耦合的运动方程 ：

1.  **电子**：[科恩-沈轨道](@entry_id:171979)按含时[科恩-沈方程](@entry_id:143968)演化，其中 $v_{\mathrm{ext}}$ 包含随[原子核](@entry_id:167902)运动而变化的电子-核吸引势。
    $i\hbar\frac{\partial}{\partial t}|\psi_k(t)\rangle = \hat{H}_{\mathrm{KS}}[n(t); \{\mathbf{R}_I(t)\}] |\psi_k(t)\rangle$

2.  **[原子核](@entry_id:167902)**：[原子核](@entry_id:167902)按牛顿定律运动，受力等于总能量对[原子核](@entry_id:167902)位置的梯度。
    $M_I \ddot{\mathbf{R}}_I(t) = \mathbf{F}_I(t) = -\nabla_I E_{\mathrm{nn}} - \langle \Psi(t) | \nabla_I \hat{H}_{e} | \Psi(t) \rangle$

在实践中，力 $\mathbf{F}_I$ 的计算需要特别小心。当使用随[原子核](@entry_id:167902)移动的[基组](@entry_id:160309)（例如，原子中心[基函数](@entry_id:170178)）来展开[科恩-沈轨道](@entry_id:171979)时，仅仅计算[哈密顿量](@entry_id:172864)[期望值](@entry_id:153208)的梯度（即 Hellmann-Feynman 力）是不够的。[基函数](@entry_id:170178)本身对[原子核](@entry_id:167902)位置的依赖性也会对总能量产生贡献。这一额外的力项被称为 **Pulay 力** 或不[完备基组](@entry_id:200333)修正。在含时框架下，对[原子核](@entry_id:167902) $I$ 的总力表达式为 ：

$\mathbf{F}_I(t) = -\nabla_I E_{\mathrm{nn}} \underbrace{- \sum_k f_k \langle \psi_k(t) | \nabla_I \hat{H}_{\mathrm{KS}}(t) | \psi_k(t) \rangle}_{\text{Hellmann-Feynman Force}} \underbrace{+ 2 \operatorname{Re} \sum_k f_k \langle \nabla_I \psi_k(t) | \hat{H}_{\mathrm{KS}}(t) - i\hbar \frac{\partial}{\partial t} | \psi_k(t) \rangle}_{\text{Time-Dependent Pulay Force}}$

这里的 Pulay 力项修正了因[基组](@entry_id:160309)不完备而导致的[能量不守恒](@entry_id:276143)问题，确保了在[数值模拟](@entry_id:137087)中总能量的稳定。Ehrenfest 方法是一种平均场近似，它假设[原子核](@entry_id:167902)只感受到电子的平均效应，这在描述某些非绝热过程（如通过[锥形交叉点](@entry_id:202598)的超快弛豫）时存在局限性，但在许多场景下，它为研究光激发后的超快电子-核耦合动力学提供了一个计算上可行的、有价值的工具。

### [电子激发](@entry_id:190531)与[光谱](@entry_id:185632)：[线性响应](@entry_id:146180) TDDFT

除了模拟实时动力学，TDDFT 的另一个主要应用是计算[电子激发](@entry_id:190531)能和[光谱](@entry_id:185632)，这通常通过**[线性响应理论](@entry_id:145737)（linear-response TDDFT, LR-TDDFT）** 实现。其基本思想是研究体系在受到一个微弱、含时扰动（如光场）时，其密度如何响应。

#### 响应函数与因果性

体系的[线性响应](@entry_id:146180)由**响应函数**（或称响应核）$\chi$ 来描述。例如，诱导密度变化 $n_1(t)$ 与微弱外势 $v_1(t)$ 之间的关系可以写成一个卷积：

$n_1(t) = \int_{-\infty}^{\infty} \chi^{\mathrm{ret}}(t-t') v_1(t') dt'$

其中 $\chi^{\mathrm{ret}}(t)$ 是**推迟响应核**。物理上的**因果性（causality）**要求响应不能发生在扰动之前，即对于 $t  0$，$\chi^{\mathrm{ret}}(t) = 0$。在[频域](@entry_id:160070)中，因果性表现为响应函数 $\chi^{\mathrm{ret}}(\omega)$ 在[复频率](@entry_id:266400)平面的上半平面是解析的（即没有极点）。这导致了连接其实部和虚部的 **[Kramers-Kronig 关系](@entry_id:140966)** 。一个典型的、满足因果性的[响应函数](@entry_id:142629)模型具有在下半平面中的极点，例如 ：

$\chi^{\mathrm{ret}}(\omega) = \frac{A}{\omega-\omega_{0}+i\gamma} - \frac{A}{\omega+\omega_{0}+i\gamma}$

对其进行傅里葉逆变换，可以得到时域中的响应核 $\chi^{\mathrm{ret}}(t) = -2A \exp(-\gamma t) \sin(\omega_0 t) \Theta(t)$，其中 $\Theta(t)$ 是 Heaviside 阶跃函数。这清晰地展示了一个有阻尼（衰减率 $\gamma$）、有共振频率（$\omega_0$）的体系，其响应在 $t=0$ 之后才出现，符合因果律。

#### 计算[激发能](@entry_id:190368)：[频域](@entry_id:160070)与时域方法

体系的**[电子激发](@entry_id:190531)能**对应于其[响应函数](@entry_id:142629)的**极点**。在这些频率下，体系即使没有外界扰动也能维持自身密度[振荡](@entry_id:267781)。TDDFT 提供两种主流方法来计算这些极点。

1.  **[频域](@entry_id:160070)方法（Casida 方程）**：
    在[线性响应理论](@entry_id:145737)中，相互作用体系的[响应函数](@entry_id:142629) $\chi$ 与科恩-沈体系的[响应函数](@entry_id:142629) $\chi_s$ 通过一个戴森（Dyson）式的方程联系起来。求解这个方程的极点问题，最终可以转化为一个矩阵[本征值问题](@entry_id:142153)，即著名的 **Casida 方程**。
    
    为了抓住其物理本质，我们可以考虑一个仅涉及一对占据[轨道](@entry_id:137151) $i$ 和空[轨道](@entry_id:137151) $a$ 的简化模型 。在这种情况下，相互作用体系的[激发能](@entry_id:190368) $\Omega$ 与[科恩-沈轨道](@entry_id:171979)能级差 $\Delta_{ia} = \epsilon_a - \epsilon_i$ 的关系可以简化为：

    $\Omega^2 = \Delta_{ia}^2 + 4 \Delta_{ia} K_{ia,ia}$

    这里的 **[耦合矩阵](@entry_id:191757)元** $K_{ia,ia}$ 包含了哈特里和交换-相关内核的贡献，它描述了[电子-空穴对](@entry_id:142506)之间的有效相互作用。这个简单的公式揭示了一个核心物理图像：TDDFT 中的[电子激发](@entry_id:190531)不仅仅是简单的单粒子跃迁，而是科恩-沈跃迁（由 $\Delta_{ia}$ 体现）与电子-空穴相互作用（由 $K_{ia,ia}$ 体现）耦合的结果。

2.  **时域方法（delta-kick）**：
    [激发光谱](@entry_id:139562)也可以通过实时 TDDFT 模拟获得 。一个有效的方法是 **delta-kick** 技术。在 $t=0$ 时刻，对体系施加一个瞬时（$\delta$ 函数形式）的[电场](@entry_id:194326)脉冲。在长度规范下，这等效于在 $t=0$ 时刻给每个[科恩-沈轨道](@entry_id:171979)乘以一个与空间位置相关的相位因子，例如 $\exp(i\kappa r_j)$，其中 $\kappa$ 是“踢”的强度，$r_j$ 是位置算符的分量。
    
    这个瞬时“踢”将体系的[基态](@entry_id:150928)制备成一个包含所有可能的[激发态](@entry_id:261453)的非定态叠加态。之后，在没有外场的情况下，让体系自由演化。在演化过程中，体系的偶极矩 $\boldsymbol{\mu}(t)$ 会发生[振荡](@entry_id:267781)，其振荡频率就对应于体系的各个[激发能](@entry_id:190368)。
    
    通过记录 $\boldsymbol{\mu}(t)$ 随时间的演化，并对其进行傅里葉变换，就可以得到[频域](@entry_id:160070)中的偶极响应。体系的频率依赖**极化率** $\alpha(\omega)$ 可以直接从[诱导偶极矩](@entry_id:262417)的傅里葉变换中得到：
    
    $\alpha_{ij}(\omega) = \frac{1}{\kappa} \int_0^\infty \Delta\mu_i(t) e^{i\omega t} dt$
    
    $\alpha(\omega)$ 的峰位就对应于体系的[吸收光谱](@entry_id:144611)。这种时域方法与[频域](@entry_id:160070)的 Casida 方法在理论上是等价的，为计算[激发光谱](@entry_id:139562)提供了另一种强大而直观的途径。

### 挑战与前沿：[绝热近似](@entry_id:143074)及其失败

TDDFT 在实际应用中最广泛的近似是 **[绝热近似](@entry_id:143074)（Adiabatic Approximation）**。该近似假设在任意时刻 $t$，交换-相关势 $v_{\mathrm{xc}}[n](\mathbf{r},t)$ 只依赖于该时刻的密度 $n(\mathbf{r},t)$，而与其历史演化无关。这相当于使用了[基态](@entry_id:150928) DFT 中的交换-相关势泛函，只是将其应用于含时的密度。

虽然[绝热近似](@entry_id:143074)在描述许多局域价电子激发方面取得了巨大成功，但它在处理某些关键物理过程时存在严重的系统性失败，尤其是在**长程电荷转移（long-range charge-transfer, CT）** 过程中。

#### [电荷转移激发](@entry_id:174772)能的低估

考虑一个由电子给体（D）和受体（A）组成、相距较远的分子复合物。其最低的 CT 激发是从 D 的 HOMO 到 A 的 LUMO。在 $R \to \infty$ 的极限下，正确的 CT 激发能应该趋近于 $I_D - A_A - 1/R$（[原子单位](@entry_id:166762)），其中 $I_D$ 是 D 的电离能，$A_A$ 是 A 的[电子亲和能](@entry_id:147520)，$-1/R$ 项是分离后的正负离子间的库仑吸引能。

然而，使用绝热的（半）局域泛函（如 [LDA](@entry_id:138982) 或 GGA）的 TDDFT 计算会严重低估这个能量 。其根源在于，当 D 和 A 相距很远时，HOMO 和 LUMO 的空间交叠几乎为零。这导致了[耦合矩阵](@entry_id:191757)元 $K_{HL,HL}$ 中的库仑项 $(HL|HL)$ 和交换-相关项都趋于零。结果，CT 激发能被错误地预测为[科恩-沈轨道](@entry_id:171979)能级差 $\Delta_{HL} = \epsilon_L - \epsilon_H$，这个值远低于正确的能量。

为了修正这个问题，**[范围分离杂化泛函](@entry_id:184447)（range-separated hybrid functionals）** 被引入。这类泛函通过引入一部分非局域的[精确交换](@entry_id:178558)（Hartree-Fock exchange），特别是用于描述长程相互作用。这部分[精确交换](@entry_id:178558)能够正确地恢复电子-空穴之间的长程 $-1/R$ 吸引作用。使用包含比例为 $\alpha$ 的长程[精确交换](@entry_id:178558)的泛函，CT [激发能](@entry_id:190368)的渐进行为被修正为 $E_{\mathrm{CT}}(R) \approx I_D - A_A - \alpha/R$，大大改善了对 CT 激发的描述 。

#### 动力学中的[电荷](@entry_id:275494)分离问题

[绝热近似](@entry_id:143074)的失败在实时动力学模拟中表现得更为深刻。考虑一个光激发后从给体到受体的[电荷](@entry_id:275494)分离过程 。在精确的理论中，当一个整数[电荷](@entry_id:275494)（例如一个电子）完全从 D 转移到 A 之后，体系应该稳定在 $D^+A^-$ 状态。为了阻止电子“流回”或在两者之间形成不物理的分数[电荷](@entry_id:275494)态（如 $D^{+\delta}A^{-\delta}$），精确的交换-相关势 $v_{\mathrm{xc}}$ 必须在 D 和 A 之间的空间区域形成一个**势垒阶跃（potential step）**。

这个势垒阶跃是**能量[导数[不连续](@entry_id:136336)性](@entry_id:144108)（derivative discontinuity）** 在动力学中的体现。它是 $v_{\mathrm{xc}}$ 的一种高度非局域和**非绝热（non-adiabatic）**或**记忆依赖（memory-dependent）**的效应。势垒的高度和形成时机依赖于体系的电荷转移历史。

然而，任何[绝热近似](@entry_id:143074)，由于其定义上的“[无记忆性](@entry_id:201790)”，都无法产生这种动态形成的势垒阶跃。其后果是：
1.  在模拟中，[电荷转移](@entry_id:155270)过程不受控制，往往导致体系弛豫到一个具有非整数[电荷分布](@entry_id:144400)的、不物理的最终状态。
2.  体系的偶极矩随时间的演化被高估。
3.  fragment 上的布居数 $N_A(t)$ 会平滑地演化，而精确的动力学应该在电荷转移完成时（$N_A(t)$ 接近整数）表现出行为的急剧变化（如斜率的突变） 。

克服[绝热近似](@entry_id:143074)的失败是 TDDFT 理论发展的最前沿。发展具有[记忆效应](@entry_id:266709)的交换-相关泛函，或者转向更普适的理论框架如含时流密度泛函理论（TDCDFT），是解决这些挑战的有希望的方向  。这些前沿理论旨在从第一性原理出发，正确地描述[超快化学](@entry_id:173375)物理过程中复杂的非局域、非绝热量子效应。