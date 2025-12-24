## 引言
将[热力学定律](@entry_id:202285)从宏观世界延伸至微观量子领域，是现代物理学的一项核心挑战。特别是对于与环境持续[交换能](@entry_id:137069)量和信息的[开放量子系统](@entry_id:138632)，经典热力学第一定律需要被重新审视和构建。其核心难题在于，当量子相干性与环境诱导的耗散过程共存时，我们应如何清晰且一致地定义“功”与“热”这两个基本概念？本文旨在系统性地解决这一知识鸿沟，为理解开放量子系统中的能量转换提供一个坚实的理论基础。

本文将引导读者分三步深入探索这一主题。在第一章“原理与机制”中，我们将建立[量子热](@entry_id:1130400)与功的标准定义，剖析其背后的物理机制，并探讨在不同物理情境下（如强耦合与[非马尔可夫动力学](@entry_id:142796)）这些定义的适用性与微妙之处。随后的第二章“应用与交叉学科联系”将展示这些基本原理的强大应用价值，从量子热机的设计到[量子输运](@entry_id:138932)中的热电现象，再到信息与能量在[量子麦克斯韦妖](@entry_id:1130406)等思想实验中的深刻联系。最后，在“动手实践”部分，通过具体的计算练习，读者将有机会亲手应用这些理论，将抽象的方程转化为对物理过程的直观理解。通过这一结构化的学习路径，我们将揭示开放量子系统的第一定律是如何成为连接量子物理、凝聚态物理与信息科学等多个学科的桥梁。

## 原理与机制

在对[开放量子系统](@entry_id:138632)的研究中，将宏观[热力学定律](@entry_id:202285)（特别是第一定律）推广到量子领域是一项核心任务。与经典[热力学](@entry_id:172368)不同，量子系统可以存在于[能量本征态](@entry_id:152154)的[相干叠加](@entry_id:170209)态中，并且其与环境的相互作用可以诱导复杂的非幺正动力学。本章旨在系统地阐述开放量子系统中的能量、功和热的定义，并探讨这些定义背后的物理机制、微妙之处及其在不同物理情境下的应用。

### [开放量子系统](@entry_id:138632)中的第一定律

经典[热力学第一定律](@entry_id:146485)指出，一个[封闭系统](@entry_id:139565)内能的变化量等于外界对系统做的功与系统吸收的热量之和。对于一个与环境相互作用的[开放量子系统](@entry_id:138632)，其总能量（系统+环境）是守恒的，但系统本身的能量可以与环境进行交换。我们将系统的**内能 (internal energy)** 定义为其哈密顿量 $H_S(t)$ 在系统状态 $\rho_S(t)$下的[期望值](@entry_id:150961)：

$$
U(t) = \mathrm{Tr}[\rho_S(t) H_S(t)]
$$

内能随时间的变化率可以通过对上式求导得到：

$$
\frac{dU(t)}{dt} = \mathrm{Tr}\left[\frac{d\rho_S(t)}{dt} H_S(t)\right] + \mathrm{Tr}\left[\rho_S(t) \frac{dH_S(t)}{dt}\right]
$$

这个表达式自然地将内能的变化分解为两个物理来源。第一个来源与系统状态 $\rho_S(t)$ 的改变有关，而第二个来源与系统哈密顿量 $H_S(t)$ 本身的显式时间依赖性有关。这启发了[量子热力学](@entry_id:140152)中对**功 (work)** 和 **热 (heat)** 的标准定义，这一框架通常归功于 Alicki：

1.  **功率 (Power, $\dot{W}$)**：定义为由于外部控制参数（例如变化的电磁场）导致[哈密顿量](@entry_id:144286)显式随时间变化而引起的内能变化率。这代表了外界对系统做功的速率。

    $$
    \dot{W}(t) = \mathrm{Tr}\left[\rho_S(t) \frac{dH_S(t)}{dt}\right]
    $$

2.  **热流率 (Heat Rate, $\dot{Q}$)**：定义为由于系统状态随时间演化（通常由与环境的相互作用引起）而导致的内能变化率。这代表了系统与环境之间的能量交换。

    $$
    \dot{Q}(t) = \mathrm{Tr}\left[H_S(t) \frac{d\rho_S(t)}{dt}\right]
    $$

根据这些定义，[开放量子系统](@entry_id:138632)的**第一定律 (First Law)** 可以写作 $\dot{U}(t) = \dot{W}(t) + \dot{Q}(t)$。

为了具体理解这些定义，我们考虑一个被驱动的[二能级系统](@entry_id:138452)（量子比特），其哈密顿量为 $H_S(t) = \frac{\omega}{2}\sigma_z + \Omega(t)\sigma_x$，其中 $\omega$ 是固定的跃迁频率，$\Omega(t)$ 是一个随时间变化的驱动强度。我们可以用[布洛赫矢量](@entry_id:144181) $(r_x, r_y, r_z)$ 来表示其状态 $\rho_S(t) = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma})$。

首先计算功率 $\dot{W}(t)$。哈密顿量的时间导数是 $\dot{H}_S(t) = \dot{\Omega}(t)\sigma_x$。因此，功率为：

$$
\dot{W}(t) = \mathrm{Tr}[\rho_S(t) \dot{H}_S(t)] = \mathrm{Tr}\left[\frac{1}{2}(I + r_x\sigma_x + r_y\sigma_y + r_z\sigma_z) \dot{\Omega}(t)\sigma_x\right]
$$

利用[泡利矩阵](@entry_id:139493)的[迹恒等式](@entry_id:188149)（例如 $\mathrm{Tr}[\sigma_i]=0$ 和 $\mathrm{Tr}[\sigma_i\sigma_j]=2\delta_{ij}$），我们发现只有含 $\sigma_x^2$ 的项对迹有贡献，得到：

$$
\dot{W}(t) = \dot{\Omega}(t) r_x(t)
$$

这个结果直观地表明，功率正比于[哈密顿量](@entry_id:144286)变化的速度 $\dot{\Omega}(t)$ 和系统在驱动方向上的响应 $r_x(t)$。

接下来，我们计算热流率 $\dot{Q}(t)$。状态的导数是 $\dot{\rho}_S(t) = \frac{1}{2}(\dot{r}_x\sigma_x + \dot{r}_y\sigma_y + \dot{r}_z\sigma_z)$。热流率为：

$$
\dot{Q}(t) = \mathrm{Tr}[H_S(t) \dot{\rho}_S(t)] = \mathrm{Tr}\left[\left(\frac{\omega}{2}\sigma_z + \Omega(t)\sigma_x\right) \frac{1}{2}(\dot{r}_x\sigma_x + \dot{r}_y\sigma_y + \dot{r}_z\sigma_z)\right]
$$

再次使用[迹恒等式](@entry_id:188149)，我们得到：

$$
\dot{Q}(t) = \frac{\omega}{2}\dot{r}_z(t) + \Omega(t)\dot{r}_x(t)
$$

这个表达式表明，热流与[布洛赫矢量](@entry_id:144181)分量的时间导数有关，反映了系统状态本身因与环境相互作用而发生的变化。

### 热的物理诠释与定义的一致性

将热流率的定义与描述[开放系统](@entry_id:147845)演化的 Gorini-Kossakowski-Sudarshan-Lindblad (GKLS) 主方程 $\dot{\rho}_S = -i[H_S, \rho_S] + \mathcal{L}(\rho_S)$ 相结合，可以得到更深刻的物理图像。这里 $\mathcal{L}$ 是**耗散子 (dissipator)**，描述了与环境相互作用引起的非幺正动力学。热流率可以写作：

$$
\dot{Q}(t) = \mathrm{Tr}[H_S (\mathcal{L}(\rho_S) - i[H_S, \rho_S])] = \mathrm{Tr}[H_S \mathcal{L}(\rho_S)]
$$

最后一个等式成立是因为 $\mathrm{Tr}[H_S [H_S, \rho_S]] = 0$（利用迹的循环[不变性](@entry_id:140168)）。这个结果至关重要：它表明热流完全是由动力学中的耗散部分（即与环境的相互作用）产生的，而[幺正演化](@entry_id:145020)部分不产生热。

#### 热与瞬时能量本征基中的布居数变化

为了获得最清晰的物理图像，我们在 $H_S(t)$ 的**瞬时能量本征基 (instantaneous energy eigenbasis, IEB)** $\{|\varepsilon_n(t)\rangle\}$ 中展开热流率的表达式。在此基底下，$H_S(t)$ 是对角的，$H_S(t) = \sum_n \varepsilon_n(t) |\varepsilon_n(t)\rangle\langle\varepsilon_n(t)|$。热流率变为：

$$
\dot{Q}(t) = \mathrm{Tr}[H_S \mathcal{L}(\rho_S)] = \sum_n \langle\varepsilon_n(t)| H_S \mathcal{L}(\rho_S) |\varepsilon_n(t)\rangle = \sum_n \varepsilon_n(t) \langle\varepsilon_n(t)| \mathcal{L}(\rho_S) |\varepsilon_n(t)\rangle
$$

这个表达式揭示了热的核心物理意义：**热是[能量本征态](@entry_id:152154)布居数因耗散而发生的变化率与相应能量的加权和**。$\langle\varepsilon_n(t)| \mathcal{L}(\rho_S) |\varepsilon_n(t)\rangle$ 正是耗散子 $\mathcal{L}$ 引起的能级 $n$ 布居数的变化率。

然而，这种清晰的对应关系仅在瞬时能量本征基中成立。如果在其他基底下错误地将热等同于布居数变化，就会得出错误的结论。例如，考虑一个由哈密顿量 $H(t) = \frac{\hbar \omega}{2}[\cos\theta(t)\sigma_z + \sin\theta(t)\sigma_x]$ 驱动的量子比特，它经历一个沿 $\sigma_z$ 轴的[纯退相干](@entry_id:204036)过程 $\mathcal{D}_z[\rho] = \frac{\gamma}{2}(\sigma_z\rho\sigma_z - \rho)$。在 $\sigma_z$ 的本征基 $\{|0\rangle, |1\rangle\}$ 中，这个耗散子只衰减非对角元（相[干性](@entry_id:900268)），而布居数保持不变，即 $\langle 0|\mathcal{D}_z[\rho]|0\rangle = \langle 1|\mathcal{D}_z[\rho]|1\rangle = 0$。如果错误地在这个基底下计算热，将得到零。然而，真正的热流率是 $\dot{Q}(t) = \mathrm{Tr}[H(t)\mathcal{D}_z[\rho]] = -\gamma\hbar\omega\sin\theta(t)\mathrm{Re}\{\rho_{01}\}$，当[驱动项](@entry_id:165986)存在时（$\sin\theta(t)\neq 0$），它通常不为零。这是因为驱动使得能量本征基与[退相干](@entry_id:145157)基底不一致，退相干过程可以在能量本征基中诱发布居数的变化，从而产生热交换。

#### [热力学一致性](@entry_id:138886)：[平衡态](@entry_id:270364)与零热流

一个自洽的[热力学](@entry_id:172368)理论必须符合基本的[热力学定律](@entry_id:202285)，如第零定律。该定律意味着，当系统与单一[热库](@entry_id:143608)[达到热平衡](@entry_id:1132996)时，它们之间不应有净热流。我们可以通过一个具体的模型来验证我们的定义。考虑一个与温度为 $\beta^{-1}$ 的热库耦合的[量子谐振子](@entry_id:140678)，其哈密顿量为 $H_S = \omega a^\dagger a$。在弱耦合近似下，其动力学由一个 GKLS 方程描述，其中包含粒子数下降（速率 $\Gamma_\downarrow$）和上升（速率 $\Gamma_\uparrow$）过程。这些速率满足 Kubo-Martin-Schwinger (KMS) 详细平衡条件：$\Gamma_\uparrow / \Gamma_\downarrow = \exp(-\beta\omega)$。

系统的[平均粒子数](@entry_id:151202) $n(t) = \langle a^\dagger a \rangle(t)$ 的变化率为 $\dot{n}(t) = \Gamma_\uparrow (n(t)+1) - \Gamma_\downarrow n(t)$。由于没有外部驱动，$\dot{W}=0$，因此热流率为 $\dot{Q}(t) = \dot{U}(t) = \omega \dot{n}(t)$。当系统达到**[稳态](@entry_id:139253) (steady state)** 时，$\dot{n}(t) \to 0$，这意味着[稳态热流](@entry_id:264790) $J_Q^{(ss)} = \lim_{t\to\infty} \dot{Q}(t) = 0$。这与第零定律的预期完全一致。此时，系统的[稳态](@entry_id:139253)粒子数 $n_{ss} = \frac{\Gamma_\uparrow}{\Gamma_\downarrow - \Gamma_\uparrow} = \frac{1}{\exp(\beta\omega)-1}$，这正是[玻色-爱因斯坦分布](@entry_id:145257)，表明系统已经与[热库](@entry_id:143608)达到了[热平衡](@entry_id:157986)。

这种一致性并非总是能得到保证，尤其是在使用近似的主方程模型时。例如，对于一个由两个相互作用的子系统构成的系统，每个子系统都与自己的独立[热库](@entry_id:143608)耦合，研究者面临一个建模选择：是构建一个“**局域 (local)**”主方程，其中每个耗散子只作用于其对应的裸子系统；还是构建一个“**全局 (global)**”主方程，其中耗散子作用于整个耦合系统的能量本征模式。研究表明，即使所有热库温度相同，局域主方程也可能错误地预测出一个非零的[稳态热流](@entry_id:264790)在子系统之间循环。这种非物理的“虚假热流”违反了[热力学第零定律](@entry_id:147511)。相比之下，全局主方程能正确预测系统将弛豫到与热库温度相符的全局吉布斯态，并且所有[稳态热流](@entry_id:264790)均为零，从而保证了热力学一致性。

### 第一定律分解中的微妙之处

尽管功和热的定义在形式上很清晰，但在具体应用中存在一些微妙之处，这些问题源于如何界定“系统”的边界以及如何解释动力学的不同部分。

#### [规范自由度](@entry_id:160491)：[兰姆位移](@entry_id:148944)[哈密顿量](@entry_id:144286)

在从微观模型推导 [GKLS 主方程](@entry_id:1125650)时，除了耗散子 $\mathcal{L}$，通常还会出现一个由环境诱导的[哈密顿量](@entry_id:144286)修正项，称为**[兰姆位移](@entry_id:148944)[哈密顿量](@entry_id:144286) (Lamb-shift Hamiltonian)**, $H_{LS}$。完整的主方程形式为 $\dot{\rho}_S = -i[H_S + H_{LS}, \rho_S] + \mathcal{L}(\rho_S)$。这带来了一个定义上的模糊性：我们应该将系统的[哈密顿量](@entry_id:144286)视为裸哈密顿量 $H_S$，还是包含[兰姆位移](@entry_id:148944)的[有效哈密顿量](@entry_id:748813) $\tilde{H}_S = H_S + H_{LS}$？

这个选择会影响功和热的分解。如果内能定义为 $U = \mathrm{Tr}[\rho_S H_S]$，那么功和热为 $\dot{W} = \mathrm{Tr}[\rho_S \dot{H}_S]$ 和 $\dot{Q} = \mathrm{Tr}[\dot{\rho}_S H_S]$。如果内能被重新定义为 $\tilde{U} = \mathrm{Tr}[\rho_S \tilde{H}_S]$，那么新的功和热将是 $\dot{\tilde{W}} = \mathrm{Tr}[\rho_S \dot{\tilde{H}}_S]$ 和 $\dot{\tilde{Q}} = \mathrm{Tr}[\dot{\rho}_S \tilde{H}_S]$。

一般而言，这两种分解的数值是不同的。功的变化量为 $\Delta\dot{W} = \mathrm{Tr}[\rho_S \dot{H}_{LS}]$，热的变化量为 $\Delta\dot{Q} = \mathrm{Tr}[\dot{\rho}_S H_{LS}]$。功和热的分解在这种“规范”选择下是依赖的。只有在一系列严格条件下，这种分解才是唯一的。这些条件包括：$H_{LS}$ 本身不随时间变化（$\partial_t H_{LS} = 0$），$H_{LS}$ 与 $H_S$ 对易（$[H_S, H_{LS}]=0$），以及 $H_{LS}$ 是耗散子 $\mathcal{L}$ 的零模式（$\mathcal{L}^*(H_{LS})=0$）。在实际物理系统中，这些条件并不总能满足，这凸显了在诠释功和热时需要格外小心。

#### 来自参考系变换的虚假热

另一个可能导致混淆的来源是对参考系变换的错误处理。假设一个实验者在一个随时间幺正演化的[旋转参考系](@entry_id:174154)中观察系统，其状态为 $\rho'(t) = U^\dagger(t)\rho(t)U(t)$。如果他/她错误地将实验室参考系下的哈密顿量 $H_0$ 与[旋转参考系](@entry_id:174154)中的状态导数 $\dot{\rho}'(t)$ 结合来计算热流，即 $\dot{Q}_{\mathrm{wrong}}(t) = \mathrm{Tr}[H_0 \dot{\rho}'(t)]$，那么就会出现问题。

$\dot{\rho}'(t)$ 不仅包含了因与环境相互作用而产生的非幺正变化，还包含了因参考系自身旋转而产生的纯幺正变化。具体来说，$\dot{\rho}'(t) = U^\dagger(\dot{\rho} - i[K, \rho])U$，其中 $K=i\dot{U}U^\dagger$ 是幺正[变换的生成元](@entry_id:172031)。这个额外的幺正项 $-i[K, \rho]$ 会在 $\dot{Q}_{\mathrm{wrong}}$ 的计算中产生一个非零的贡献，即使系统是孤立的。这个贡献是“虚假的”，因为它不代表与[热库](@entry_id:143608)的真实能量交换，而仅仅是参考系运动的产物。例如，对于一个具有初始相[干性](@entry_id:900268)的量子比特，在绕 $\sigma_y$ 轴旋转的参考系中，这种错误的计算会产生一个与旋转速率 $\dot{\theta}(0)$ 和初始相[干性](@entry_id:900268) $m_x(0)$ 成正比的虚假[熵产生](@entry_id:141771)率项，可能导致瞬时的“第二定律违背”。这强调了功和热的定义必须基于物理上清晰的能量交换过程，而不是任意的数学分解。

### 超越[弱耦合](@entry_id:1127454)与马尔可夫近似

标准的 GKLS 框架建立在[弱耦合](@entry_id:1127454)和马尔可夫（无记忆）近似之上。当这些条件不满足时，我们需要更广义的理论。

#### 强耦合与平均力[哈密顿量](@entry_id:144286)

当[系统与环境](@entry_id:142270)的相互作用不可忽略时（**强耦合 (strong coupling)** 区域），系统的[有效能](@entry_id:139794)量结构会因相互作用而发生显著改变。此时，使用裸[哈密顿量](@entry_id:144286) $H_S$ 来定义内能变得不恰当。正确的做法是引入**平均力[哈密顿量](@entry_id:144286) (Hamiltonian of Mean Force)**, $H^*(\beta, \lambda)$。

这个算符的定义源于[平衡态](@entry_id:270364)统计力学。对于一个给定的总哈密顿量 $H(\lambda) = H_S(\lambda) + H_B + H_{SB}$，系统的约化[平衡态](@entry_id:270364) $\rho_S^\beta(\lambda) = \mathrm{Tr}_B[e^{-\beta H(\lambda)}/Z_{SB}]$ 可以被表示为一个由 $H^*$ 生成的有效吉布斯态：

$$
\rho_S^\beta(\lambda) = \frac{e^{-\beta H^*(\beta, \lambda)}}{Z_S^*}
$$

由此可以解出 $H^*$ 的[标准形式](@entry_id:153058)：

$$
H^*(\beta, \lambda) = -\beta^{-1}\ln\left(\frac{\mathrm{Tr}_B[e^{-\beta (H_S(\lambda)+H_B+H_{SB})}]}{\mathrm{Tr}_B[e^{-\beta H_B}]}\right)
$$

这个定义是非微扰的，它精确地包含了所有阶的[系统-环境相互作用](@entry_id:202993)对系统[有效能](@entry_id:139794)级的影响。在强耦合[热力学](@entry_id:172368)中，系统的内能应定义为 $U(t) = \mathrm{Tr}_S[\rho_S(t) H^*(\beta, \lambda_t)]$。相应地，功和热的分解也基于 $H^*$ 进行：$\delta W = \mathrm{Tr}_S[\rho_S dH^*]$ 和 $\delta Q = \mathrm{Tr}_S[H^* d\rho_S]$。这种方法为将[热力学](@entry_id:172368)推广到强耦合领域提供了坚实的基础。

#### [非马尔可夫动力学](@entry_id:142796)与能量回流

当环境具有结构化的谱密度或[系统与环境](@entry_id:142270)的相互作用很强时，环境的“[记忆效应](@entry_id:266709)”会变得显著，导致**非马尔可夫 (non-Markovian)** 动力学。在这种情况下，描述系统演化的主方程中的[耗散率](@entry_id:748577)（例如 $\gamma(t)$）可能会在某些时间间隔内变为负值。

一个负的[耗散率](@entry_id:748577)具有深刻的物理意义。回到我们对一个经历[振幅阻尼](@entry_id:146861)的[二能级系统](@entry_id:138452)的分析，其热流率为 $\dot{Q}(t) = -\hbar\omega_0 \gamma(t) p_e(t)$，其中 $p_e(t)$ 是激发态布居数。当 $\gamma(t) > 0$ 时，$\dot{Q}(t)  0$，系统能量流向环境，这是通常的耗散过程。然而，当 $\gamma(t)  0$ 时，$\dot{Q}(t) > 0$，这意味着能量从环境流回系统。这种现象被称为**能量回流 (energy backflow)**。它是[非马尔可夫动力学](@entry_id:142796)的一个关键标志，表明信息和能量在系统与环境之间可以双向流动，而不是像马尔可夫过程中那样单向地从系统流失到环境。

### 高级主题与不同视角

#### 热、相[干性](@entry_id:900268)与[可提取功](@entry_id:1124640)

在某些过程中，系统的[能量本征态](@entry_id:152154)布居数可能保持不变，导致传统意义上的热交换为零。但这并不意味着没有发生[热力学](@entry_id:172368)上重要的变化。一个典型的例子是[纯退相干](@entry_id:204036)过程，它只破坏能量本征基中的相[干性](@entry_id:900268)。

考虑一个处于[相干叠加](@entry_id:170209)态的量子系统，其内能 $U$ 可以被进一步分解为两部分：**被动能量 (passive energy)** $U_{\mathrm{pass}}$ 和 **遍历熵/[可提取功](@entry_id:1124640) (ergotropy)** $\mathcal{W}$。被动能量是指通过幺正变换无法从系统中提取的能量，对应于一个与原状态具有相同本征值但能量-布居数排序最优化的“被动状态”的能量。遍历熵/[可提取功](@entry_id:1124640)则是内能中超出被动能量的部分，即 $\mathcal{W} = U - U_{\mathrm{pass}}$，它存储在相[干性](@entry_id:900268)中，代表了可以通过循环幺正过程提取的[最大功](@entry_id:143924)。

在一个[纯退相干](@entry_id:204036)过程中，系统的[能量本征态](@entry_id:152154)布居数不变，因此内能 $U$ 和传统热流 $\dot{Q}_{\mathrm{trad}}$ 均为零。然而，[退相干](@entry_id:145157)过程会破坏相[干性](@entry_id:900268)，从而导致遍历熵/[可提取功](@entry_id:1124640) $\mathcal{W}$ 减少。由于总内能不变，减少的遍历熵/[可提取功](@entry_id:1124640)必须转化为被动能量的增加，即 $\dot{\mathcal{W}}(t) = -\dot{U}_{\mathrm{pass}}(t)  0$。这个被动能量的增加可以被看作是一种“[耗散功](@entry_id:748576)”，即原本可以做功的有序能量（相[干性](@entry_id:900268)）因与环境相互作用而退化为无序的、不可提取的能量。这为理解热与信息之间的深刻联系提供了一个新的视角。

#### 随机第一定律：轨迹视角

[GKLS 主方程](@entry_id:1125650)描述的是大量相同系统组成的系综的平均行为。然而，通过所谓的“展开 (unraveling)”，我们可以将主方程的动力学分解为单个量子系统的**[随机轨迹](@entry_id:755474) (stochastic trajectories)**。在量子跳跃图像中，单个系统的演化由两部分组成：在两次跳跃之间，系统状态在有效非厄米哈密顿量的作用下连续演化；在某些随机时刻，系统经历瞬时的“**量子跳跃 (quantum jump)**”。

这个[轨迹图](@entry_id:756083)像为[热力学第一定律](@entry_id:146485)提供了一个更为微观的诠释。在一个[随机轨迹](@entry_id:755474)上，无穷小时间内的内能变化 $\delta U_{\mathrm{trj}}$ 同样可以分解为功和热。

*   **随机功 ($\delta W_{\mathrm{trj}}$)**：功的来源与系综层面相同，即[哈密顿量](@entry_id:144286)的显式时间依赖性。在两次跳跃之间的连续演化过程中，外界持续对系统做功，$\delta W_{\mathrm{trj}} = \langle\psi(t)|\dot{H}(t)|\psi(t)\rangle dt$。

*   **随机热 ($\delta Q_{\mathrm{trj}}$)**：热的交换则与量子跳跃事件直接关联。在两次跳跃之间的连续演化过程中，没有与热库的实际能量交换，因此 $\delta Q_{\mathrm{trj}} = 0$。当一次量子跳跃发生时，例如从能级 $|g\rangle$ 跃迁到 $|e\rangle$，系统从热库吸收了一个能量量子 $\hbar\omega(t_j)$，此时 $\delta Q_{\mathrm{trj}} = +\hbar\omega(t_j)$。反之，当系统从 $|e\rangle$ 跃迁到 $|g\rangle$ 时，它向热库释放一个能量量子，$\delta Q_{\mathrm{trj}} = -\hbar\omega(t_j)$。

这种定义满足了所有一致性要求：它在轨迹层面保证了能量守恒；它将热与微观的能量量子交换事件联系起来；对所有可能的轨迹进行系综平均后，可以精确地恢复由主方程导出的平均热流率。这个**随机第一定律 (stochastic first law)** 揭示了[量子热](@entry_id:1130400)交换的离散和随机本性，为理解和控制单个量子系统中的能量流动提供了强大的理论工具。