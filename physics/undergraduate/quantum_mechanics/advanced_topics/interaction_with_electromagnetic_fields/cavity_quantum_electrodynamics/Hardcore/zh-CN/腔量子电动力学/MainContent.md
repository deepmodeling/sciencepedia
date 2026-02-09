## 引言
腔量子电动力学（Cavity Quantum Electrodynamics, cQED）是研究单个原子与光学谐振腔中单个光子相互作用的前沿领域，它不仅为我们提供了一个在最基本层面上检验量子力学原理的理想平台，也构成了现代量子光学和量子信息科学的基石。理解和控制这种微观相互作用是开发量子计算机、安全量子通信和超高精度传感器的关键。然而，如何精确描述这种孤立量子系统中的光-物质耦合，并揭示其独特的量子动力学，构成了该领域的核心理论挑战。

本文旨在系统性地介绍腔QED的核心概念与前沿应用。在接下来的章节中，我们将踏上一段从基础理论到实际应用的探索之旅。在“原理与机制”一章中，我们将深入剖析描述原子-腔场相互作用的Jaynes-Cummings模型，揭示真空拉比振荡和缀饰态等迷人的量子现象。随后，在“应用与交叉学科联系”一章中，我们将展示这些基本原理如何转化为强大的技术，用于构建量子逻辑门、实现量子网络，并探讨其思想如何启发凝聚态物理与量子化学等领域的研究。最后，通过“动手实践”部分，读者将有机会通过解决具体问题来巩固所学知识。

## 原理与机制

继前一章对腔量子电动力学 (Cavity Quantum Electrodynamics, cQED) 的宏观介绍之后，本章将深入探讨其核心的物理原理与理论模型。我们将从描述一个二能级原子与单模光腔相互作用的基础哈密顿量出发，逐步建立起著名的 Jaynes-Cummings 模型。在此基础上，我们将揭示该系统独特的量子动力学行为，如真空拉比振荡，并引出缀饰态 (dressed states) 这一核心概念。最后，我们将讨论实现这些量子现象的关键条件，并将其与真实物理系统中的损耗机制联系起来。

### 原子-场相互作用与旋转波近似

在腔QED中，最基础的模型考虑一个二能级原子与一个高品质光学腔内的单个量子化电磁场模式之间的相互作用。我们将原子的基态和激发态分别记为 $|g\rangle$ 和 $|e\rangle$，其能量差为 $\hbar\omega_a$，其中 $\omega_a$ 是原子的跃迁频率。该单模光腔的共振频率为 $\omega_c$，腔内光子由湮灭算符 $\hat{a}$ 和产生算符 $\hat{a}^\dagger$ 描述。在没有相互作用的情况下，系统的自由哈密顿量是原子哈密顿量 $\hat{H}_A$ 与光腔哈密顿量 $\hat{H}_C$ 之和：

$$
\hat{H}_0 = \hat{H}_A + \hat{H}_C = \frac{1}{2}\hbar\omega_a\hat{\sigma}_z + \hbar\omega_c \left(\hat{a}^\dagger \hat{a} + \frac{1}{2}\right)
$$

其中，$\hat{\sigma}_z = |e\rangle\langle e| - |g\rangle\langle g|$ 是泡利z算符，描述了原子的布居数反转。原子与腔场之间的相互作用在电偶极近似下由相互作用哈密顿量 $\hat{H}_I$ 描述。该哈密顿量正比于原子偶极矩算符 $\hat{d} \propto (\hat{\sigma}_+ + \hat{\sigma}_-)$ 与腔内电场算符 $\hat{E} \propto (\hat{a} + \hat{a}^\dagger)$ 的乘积。这里，$\hat{\sigma}_+ = |e\rangle\langle g|$ 和 $\hat{\sigma}_- = |g\rangle\langle e|$ 分别是原子的上升和下降算符。因此，完整的相互作用哈密顿量可以写为 [@problem_id:2083511]：

$$
\hat{H}_I = \hbar g (\hat{\sigma}_+ + \hat{\sigma}_-)(\hat{a} + \hat{a}^\dagger)
$$

其中 $g$ 是描述原子与腔场之间相互作用强度的实数耦合常数。将上式展开，我们得到四个不同的项：

$$
\hat{H}_I = \hbar g (\hat{a}\hat{\sigma}_+ + \hat{a}^\dagger\hat{\sigma}_-) + \hbar g (\hat{a}^\dagger\hat{\sigma}_+ + \hat{a}\hat{\sigma}_-)
$$

这四项描述了四种不同的物理过程 [@problem_id:2083525]：
1.  $\hat{a}\hat{\sigma}_+$：原子吸收一个光子并从基态 $|g\rangle$ 跃迁到激发态 $|e\rangle$。
2.  $\hat{a}^\dagger\hat{\sigma}_-$：原子从激发态 $|e\rangle$ 跃迁到基态 $|g\rangle$ 并发射一个光子。
3.  $\hat{a}^\dagger\hat{\sigma}_+$：原子从基态 $|g\rangle$ 跃迁到激发态 $|e\rangle$ 的同时，腔内也**产生**一个光子。
4.  $\hat{a}\hat{\sigma}_-$：原子从激发态 $|e\rangle$ 跃迁到基态 $|g\rangle$ 的同时，腔内也**湮灭**一个光子。

在通常的实验条件下，原子跃迁频率 $\omega_a$ 与光腔频率 $\omega_c$ 非常接近（即近共振，$\omega_a \approx \omega_c$），并且耦合强度 $g$ 远小于这两个频率（即 $g \ll \omega_a, \omega_c$）。在这种情况下，我们可以应用**旋转波近似 (Rotating Wave Approximation, RWA)**。

为了理解 RWA 的物理依据，我们可以变换到相对于自由哈密顿量 $\hat{H}_0$ 的相互作用绘景中。在此绘景中，各项的时间演化因子分别为：$\hat{a}\hat{\sigma}_+ \rightarrow \hat{a}\hat{\sigma}_+ \exp(-i(\omega_c - \omega_a)t)$，$\hat{a}^\dagger\hat{\sigma}_- \rightarrow \hat{a}^\dagger\hat{\sigma}_- \exp(i(\omega_c - \omega_a)t)$，$\hat{a}^\dagger\hat{\sigma}_+ \rightarrow \hat{a}^\dagger\hat{\sigma}_+ \exp(i(\omega_c + \omega_a)t)$，以及 $\hat{a}\hat{\sigma}_- \rightarrow \hat{a}\hat{\sigma}_- \exp(-i(\omega_c + \omega_a)t)$。

在近共振条件下，前两项（称为“共转项”）的振荡频率 $\pm(\omega_c - \omega_a)$ 非常小。这意味着它们描述的过程——原子与腔场之间交换一个能量子——是近似能量守恒的，可以有效地发生。相比之下，后两项（称为**反转项 (counter-rotating terms)**, $\hat{H}_{CR} = \hbar g (\hat{a}^\dagger\hat{\sigma}_+ + \hat{a}\hat{\sigma}_-)$）的振荡频率 $\pm(\omega_c + \omega_a)$ 非常大。这些项对应于严重违反能量守恒的过程（同时产生或湮灭原子和光子的激发）。在系统演化的特征时间尺度（如 $1/g$）上，这些高速振荡项的贡献会迅速平均为零，因此可以被忽略 [@problem_id:2083525]。值得注意的是，尽管在动力学演化中可以忽略反转项，但对于某些特定的纠缠态，它们仍然可以有非零的期望值，这揭示了RWA作为一种近似的本质 [@problem_id:2083511]。

忽略了反转项之后，我们得到了腔QED中最为重要的模型之一——**Jaynes-Cummings (JC) 哈密顿量**：

$$
\hat{H}_{\text{JC}} = \frac{1}{2}\hbar\omega_a\hat{\sigma}_z + \hbar\omega_c \hat{a}^\dagger \hat{a} + \hbar g (\hat{a}\hat{\sigma}_+ + \hat{a}^\dagger\hat{\sigma}_-)
$$

为简化讨论，我们通常将零点能项 $\frac{1}{2}\hbar\omega_c$ 省略，因为它仅导致整体能量的平移。

### Jaynes-Cummings 模型：一个守恒律及其推论

Jaynes-Cummings 模型一个极为重要的特性是它内蕴一个守恒律。让我们定义一个算符 $\hat{N}$，它代表系统的**总激发数**，即腔内光子数与原子激发之和：

$$
\hat{N} = \hat{a}^\dagger\hat{a} + |e\rangle\langle e| = \hat{a}^\dagger\hat{a} + \frac{1}{2}(\hat{\sigma}_z + I)
$$

其中 $I$ 是单位算符。我们可以证明这个总激发数算符与 JC 哈密顿量是对易的，即 $[\hat{H}_{\text{JC}}, \hat{N}] = 0$ [@problem_id:2083516]。自由哈密顿量的部分显然与 $\hat{N}$ 对易。对于相互作用项，我们可以计算：
$$
[\hat{a}\hat{\sigma}_+ + \hat{a}^\dagger\hat{\sigma}_-, \hat{a}^\dagger\hat{a} + |e\rangle\langle e|] = [\hat{a}\hat{\sigma}_+, \hat{a}^\dagger\hat{a}] + [\hat{a}^\dagger\hat{\sigma}_-, \hat{a}^\dagger\hat{a}] + [\hat{a}\hat{\sigma}_+, |e\rangle\langle e|] + [\hat{a}^\dagger\hat{\sigma}_-, |e\rangle\langle e|]
$$
利用算符的对易关系，可以证明上式右边的各项恰好相互抵消，最终得到 $[\hat{H}_{\text{JC}}, \hat{N}] = 0$。

根据量子力学基本原理，这意味着总激发数 $\hat{N}$ 是一个守恒量。这个守恒律的物理含义是，在 RWA 下，原子与腔场之间只能交换激发，而不能凭空创造或湮灭总的激发。例如，当一个光子被原子吸收时（光子数减1），原子必须从基态跃迁到激发态（原子激发数加1），从而保持总激发数不变。

这个守恒律极大地简化了对系统动力学的分析。它意味着哈密顿量 $\hat{H}_{\text{JC}}$ 在以总激发数 $\hat{N}$ 的本征态为基矢的表象中是块对角的。除了系统基态 $|g, 0\rangle$（总激发数为0）是唯一的之外，所有其他态都成对出现。对于任意整数 $n \ge 0$，态矢 $|e, n\rangle$（原子在激发态，腔内有 $n$ 个光子）和 $|g, n+1\rangle$（原子在基态，腔内有 $n+1$ 个光子）具有相同的总激发数 $N = n+1$。因此，系统的动力学演化被限制在一系列独立的二维子空间内，每个子空间由一对“裸态” (bare states) $\{|e, n\rangle, |g, n+1\rangle\}$ 张成。

### 缀饰态与真空拉比振荡

守恒律的存在使我们能够精确求解 JC 模型的动力学。让我们首先考虑最简单也是最引人入胜的情形：$N=1$ 的子空间，它由态矢 $|e, 0\rangle$ 和 $|g, 1\rangle$ 张成。假设系统初始处于 $|e, 0\rangle$ 状态，即一个激发态原子与一个处于真空状态的腔场。

在共振条件下（$\omega_a = \omega_c$），这两个态是简并的。相互作用哈密顿量 $\hat{H}_{int} = \hbar g (\hat{a}\hat{\sigma}_+ + \hat{a}^\dagger\hat{\sigma}_-)$ 将这两个态耦合起来：
$$
\hat{H}_{int}|e, 0\rangle = \hbar g |g, 1\rangle
$$
$$
\hat{H}_{int}|g, 1\rangle = \hbar g |e, 0\rangle
$$
求解含时薛定谔方程 $i\hbar \frac{d}{dt}|\psi(t)\rangle = \hat{H}|\psi(t)\rangle$，可以得到系统的状态随时间的演化。若初态为 $|\psi(0)\rangle = |e, 0\rangle$，则在任意时刻 $t$，系统状态为：
$$
|\psi(t)\rangle = \cos(gt)|e, 0\rangle - i\sin(gt)|g, 1\rangle
$$
从中可以看出，找到原子处于激发态的概率为 $P_e(t) = |\langle e, 0|\psi(t)\rangle|^2 = \cos^2(gt)$ [@problem_id:2083499]。这意味着系统的能量在原子和腔场之间以频率 $2g$ 周期性地来回交换。一个激发态原子会发射一个光子到腔中而回到基态，随后又会重新吸收这个光子回到激发态。这种原子与**真空**腔场之间的相干能量交换被称为**真空拉比振荡 (vacuum Rabi oscillation)**。它是腔QED的一个标志性量子效应，表明了真空并非“空无一物”，而是具有可与之发生相互作用的涨落。

在任意一个由 $\{|e, n\rangle, |g, n+1\rangle\}$ 张成的子空间中，相互作用哈密顿量都会混合这两个裸态，形成新的能量本征态。这些新的本征态被称为**缀饰态 (dressed states)**，因为它们可以被看作是被光子“云”所“缀饰”的原子态。对于给定的总激发数 $N=n+1$，在共振条件下，哈密顿量在该子空间中的矩阵形式为：
$$
H_n = \hbar\omega_c\left(n+\frac{1}{2}\right) \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + \hbar g \sqrt{n+1} \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}
$$
通过对角化，我们得到两个缀饰态本征矢及其对应的本征能量：
$$
|n, +\rangle = \frac{1}{\sqrt{2}} (|e, n\rangle + |g, n+1\rangle) \quad \text{with energy} \quad E_{n,+} = \hbar\omega_c\left(n+\frac{1}{2}\right) + \hbar g \sqrt{n+1}
$$
$$
|n, -\rangle = \frac{1}{\sqrt{2}} (|e, n\rangle - |g, n+1\rangle) \quad \text{with energy} \quad E_{n,-} = \hbar\omega_c\left(n+\frac{1}{2}\right) - \hbar g \sqrt{n+1}
$$
(请注意，缀饰态的具体形式可能因哈密顿量表示的约定而有一个相位因子，例如 $\frac{1}{\sqrt{2}}(|e,n\rangle \pm i |g,n+1\rangle)$，但这不影响其物理实质 [@problem_id:2083497])。

缀饰态是原子-腔场复合系统的真实定态，代表了光与物质的深度混合。一个处于缀饰态的系统，其性质（如相互作用能）是恒定的。例如，对于态 $|\Psi\rangle = \frac{1}{\sqrt{2}} (|e, n\rangle - |g, n+1\rangle)$，其相互作用能的期望值为 $\langle\Psi|\hat{H}_{int}|\Psi\rangle = -\hbar g \sqrt{n+1}$，这是一个不随时间改变的确定值，再次印证了缀饰态的定态特性 [@problem_id:2083546]。

### Jaynes-Cummings 阶梯：量子化的能谱

缀饰态的能量表达式 $E_{n, \pm}$ 揭示了原子-腔场系统的能谱结构，这一结构被称为**Jaynes-Cummings 阶梯**。对于每一个激发数 $n$（$n=0, 1, 2, \dots$），原本简并的能级 $|e, n\rangle$ 和 $|g, n+1\rangle$ 分裂成一个能量差为 $2\hbar g \sqrt{n+1}$ 的双重态，这被称为**拉比分裂 (Rabi splitting)**。

这个能谱最引人注目的特征是分裂大小对 $\sqrt{n+1}$ 的依赖性。这与经典物理的预测截然不同。如果将腔场看作经典电磁场，拉比分裂将正比于电场振幅，即正比于 $\sqrt{n}$。而 JC 模型预测的分裂大小正比于 $\sqrt{n+1}$，这种差异在 $n=0$ 时最为显著：即使腔内没有光子（真空场），也存在一个大小为 $2\hbar g$ 的**真空拉比分裂**。

能级间距的非线性（即对 $\sqrt{n+1}$ 的依赖）是 JC 阶梯的另一个关键量子特征。这与量子谐振子的等间距能谱形成鲜明对比。由于这种**非谐性 (anharmonicity)**，从一个双重态到相邻双重态的跃迁频率是依赖于 $n$ 的。例如，从 $n=1$ 的能级跃迁到 $n=2$ 的能级，两个可能的跃迁（$|1, -\rangle \to |2, -\rangle$ 和 $|1, +\rangle \to |2, +\rangle$）的频率是不同的 [@problem_id:2083522]。这种非谐性是至关重要的，因为它允许我们选择性地寻址特定的跃迁，这是将腔QED系统用作量子比特进行量子计算的基础。

### 真实系统：相干耦合与退相干

到目前为止，我们的讨论都基于理想的 Jaynes-Cummings 模型，它是一个封闭的、无损耗的系统。然而，在真实的物理系统中，原子-腔场系统不可避免地与外部环境发生相互作用，导致能量耗散和量子相干性的损失（即**退相干**）。

主要有两种损耗机制 [@problem_id:2083524]：
1.  **原子自发辐射 (Atomic Spontaneous Emission)**：激发态原子可以通过与腔模以外的其他环境电磁模式相互作用而衰变，这个过程的速率由 $\gamma$ 表征。
2.  **腔场衰减 (Cavity Decay)**：由于腔镜不完美（例如具有有限的透射率），腔内的光子会以速率 $\kappa$ 泄漏到外部环境中。

为了能观测到如真空拉比振荡这样的相干量子效应，原子与腔场之间交换能量的速率必须远快于能量因任何一种机制而丢失的速率。这就引出了**强耦合机制 (strong coupling regime)** 的判据：

$$
g \gg \kappa, \gamma
$$

当满足这个条件时，系统可以在退相干破坏其量子态之前，完成多次相干的能量交换周期。在实验上，强耦合的一个明确标志是在腔的透射谱中观测到真空拉比分裂。当一个弱探测激光扫过腔共振频率时，如果系统处于强耦合区，透射谱会从单个洛伦兹峰分裂成两个峰。更精确的理论分析表明，能够分辨出这两个峰的条件为 $g > |\kappa-\gamma|/4$，而峰之间的频率间隔由 $2\sqrt{g^2 - (\kappa-\gamma)^2/16}$ 给出 [@problem_id:2083514]。

与强耦合相对的是**弱耦合机制 (weak coupling regime)**，即 $g \ll \kappa, \gamma$。在此区域，相干振荡被过阻尼，原子激发态在有机会将能量还给原子之前就已经通过自发辐射或腔衰减而丢失了。尽管如此，弱耦合机制下腔的存在依然能显著影响原子的辐射特性，这一现象被称为**珀塞尔效应 (Purcell effect)**。

根据费米黄金定则，原子的自发辐射率正比于其跃迁频率处真空电磁模式的局域态密度 (LDOS)。一个高品质因数 $Q$、小模式体积 $V$ 的谐振腔，能极大地增强其共振频率附近的 LDOS。因此，将一个原子置于这样一个腔中，可以使其向腔模的自发辐射率 $\gamma_{\text{cavity}}$ 相对于其在自由空间中的辐射率 $\gamma_0$ 大幅增强。这个增强的倍数被称为珀塞尔因子。在共振情况下，这一比率可以表示为 [@problem_id:2083528]：
$$
\frac{\gamma_{\text{cavity}}}{\gamma_0} \propto \frac{Q}{V}
$$
珀塞尔效应是实现高效单光子源的关键技术，它能迫使原子优先将能量发射到我们需要的特定腔模中，从而实现对单光子产生过程的确定性控制。

综上所述，腔量子电动力学的丰富物理内涵根植于原子与单模光场之间最基本的相互作用。通过旋转波近似，我们得到了 Jaynes-Cummings 模型，它预言了缀饰态、真空拉比振荡和非谐的 Jaynes-Cummings 阶梯等纯粹的量子现象。这些现象的实验观测依赖于系统是否处于强耦合机制，而与之相对的弱耦合机制则引出了同样重要的珀塞尔效应。这些基本原理构成了现代量子光学和量子信息科学的基石。