## 引言
在核物理研究的前沿，对远离稳定线核素，特别是具有弱束缚结构的原子核（如氘核和晕核）的探索，揭示了传统核反应模型所面临的挑战。这些原子核极易在与靶核的碰撞中发生破裂，其连续的破裂态（连续谱）与束缚的基态之间存在强烈的耦合，这种耦合效应是标准光学模型或扭曲波玻恩近似难以准确描述的。这便构成了一个关键的知识缺口：如何建立一个既能精确处理破裂效应，又能在计算上可行的理论框架。

连续谱离散化耦合通道（Continuum-Discretized Coupled-Channel, CDCC）方法正是为解决这一核心问题而发展的强大理论工具。它通过一种巧妙的离散化技巧，将无限维的连续谱问题转化为有限维的耦合方程组，从而为精确描述弱束缚核的反应动力学提供了可能。本文旨在系统性地介绍CDCC方法。在“原理与机制”一章中，我们将从三体散射问题的量子力学基础出发，详细阐述CDCC的数学构造、核心近似及其物理内涵。随后，在“应用与跨学科关联”一章中，我们将展示该方法如何被用于解决核物理和核天体物理中的前沿问题，并探讨其与计算科学等领域的深刻联系。最后，“实践练习”部分将通过具体的计算问题，引导读者亲身体验模型构建和结果分析的关键环节，从而真正掌握这一先进的计算方法。

## 原理与机制

在本章中，我们将深入探讨连续谱离散化耦合通道（Continuum-Discretized Coupled-Channel, CDCC）方法的核心原理与物理机制。CDCC方法是处理由弱束缚弹核（如氘核、锂-11等）引发的核反应的一种强大理论工具。我们将从建立三体散射问题的量子力学描述出发，系统地阐述CDCC方法如何将一个无穷维的复杂问题转化为一个在计算上可行的、有限维的耦合方程组。本章旨在揭示该方法背后的物理直觉、数学构造及其应用的有效性边界。

### 三体散射问题的哈密顿量

CDCC方法的出发点是将弹核-靶核散射视为一个非相对论性的三体量子力学问题。考虑一个由两个团簇（记为 $t$ 和 $b$）构成的复合弹核 $p$（$p=t+b$）与一个无内部结构的目标靶核 $T$ 发生散射。例如，在氘核（$d$）散射中，$t$ 和 $b$ 分别是质子（$p$）和中子（$n$）。设三个组分的质量分别为 $m_t$、$m_b$ 和 $m_T$，它们在实验室坐标系中的位置矢量分别为 $\mathbf{r}_t$、$\mathbf{r}_b$ 和 $\mathbf{r}_T$。系统的总哈密顿量由三者的动能与它们之间的对相互作用势能组成：

$$H_{\mathrm{lab}} = -\frac{\hbar^2}{2m_t}\nabla_{\mathbf{r}_t}^2 - \frac{\hbar^2}{2m_b}\nabla_{\mathbf{r}_b}^2 - \frac{\hbar^2}{2m_T}\nabla_{\mathbf{r}_T}^2 + V_{tb}(|\mathbf{r}_t - \mathbf{r}_b|) + V_{tT}(|\mathbf{r}_t - \mathbf{r}_T|) + V_{bT}(|\mathbf{r}_b - \mathbf{r}_T|)$$

为了描述散射过程，我们需要分离出整个系统质心（Center of Mass, CM）的平庸运动，专注于相对运动。这可以通过引入一套合适的雅可比（Jacobi）坐标来实现。对于弹核-靶核这样的划分，最自然的雅可比坐标选择是：
1.  弹核的内部相对坐标：$\mathbf{r} = \mathbf{r}_t - \mathbf{r}_b$
2.  弹核质心与靶核的相对坐标：$\mathbf{R} = \frac{m_t \mathbf{r}_t + m_b \mathbf{r}_b}{m_p} - \mathbf{r}_T$，其中 $m_p = m_t + m_b$ 是弹核的总质量。

在这套坐标系下，总动能算符可以完美地分离为三项，分别对应弹核内部相对运动、弹核-靶核相对运动以及三体系统总质心的运动。总质心运动的能量在散射过程中是守恒的，可以从哈密顿量中分离出去。描述散射动力学的相对运动哈密顿量 $H_{\mathrm{rel}}$ 因此可以写为：

$$H_{\mathrm{rel}} = T_{\mathbf{R}} + H_p + V_{PT}(\mathbf{R}, \mathbf{r})$$

其中，$T_{\mathbf{R}} = -\frac{\hbar^2}{2\mu_{pT}}\nabla_{\mathbf{R}}^2$ 是弹核-靶核相对运动的动能算符，$\mu_{pT} = \frac{m_p m_T}{m_p + m_T}$ 是该相对运动的约化质量。$H_p = -\frac{\hbar^2}{2\mu_{tb}}\nabla_{\mathbf{r}}^2 + V_{tb}(|\mathbf{r}|)$ 是弹核的内部哈密顿量，它描述了团簇 $t$ 和 $b$ 在其自身质心系中的运动，其中 $\mu_{tb} = \frac{m_t m_b}{m_p}$ 是弹核内部的约化质量。$H_p$ 的本征态构成了弹核的束缚态和连续谱（破裂）态。

最重要的部分是耦合势 $V_{PT}(\mathbf{R}, \mathbf{r})$，它代表了弹核的两个组分与靶核之间的相互作用总和，即 $V_{PT} = V_{tT} + V_{bT}$。为了在雅可比坐标中表达它，我们需要将团簇-靶核的距离 $|\mathbf{r}_{tT}|$ 和 $|\mathbf{r}_{bT}|$ 用 $\mathbf{R}$ 和 $\mathbf{r}$ 表示。经过简单的坐标变换，我们得到 [@problem_id:3552242]：

$$\mathbf{r}_{tT} = \mathbf{r}_t - \mathbf{r}_T = \mathbf{R} + \frac{m_b}{m_p}\mathbf{r}$$

$$\mathbf{r}_{bT} = \mathbf{r}_b - \mathbf{r}_T = \mathbf{R} - \frac{m_t}{m_p}\mathbf{r}$$

于是，完整的相对运动哈密顿量写作：

$$H_{\mathrm{rel}} = -\frac{\hbar^2}{2\mu_{pT}}\nabla_{\mathbf{R}}^2 + \left[ -\frac{\hbar^2}{2\mu_{tb}}\nabla_{\mathbf{r}}^2 + V_{tb}(|\mathbf{r}|) \right] + V_{tT}\left(\left|\mathbf{R} + \frac{m_b}{m_p}\mathbf{r}\right|\right) + V_{bT}\left(\left|\mathbf{R} - \frac{m_t}{m_p}\mathbf{r}\right|\right)$$

这个哈密顿量是CDCC方法的基础。其中，耦合项 $V_{tT}$ 和 $V_{bT}$ 的自变量同时依赖于 $\mathbf{R}$ 和 $\mathbf{r}$，这正是导致弹核内部运动与弹核-靶核相对运动之间发生耦合的根源。CDCC的核心任务，就是求解这个哈密顿量所描述的三体薛定谔方程 $H_{\mathrm{rel}} \Psi(\mathbf{R}, \mathbf{r}) = E \Psi(\mathbf{R}, \mathbf{r})$。

### 散射理论的语言：通道、S矩阵与渐进行为

为了求解散射问题，我们必须定义系统的**通道（channels）**。在散射理论中，一个通道对应于系统在渐近区域（即 $R=|\mathbf{R}| \to \infty$）的一个特定组态。在这个区域，相互作用势 $V_{PT}$ 趋于零（对于短程核力）或变为纯库仑势，系统可以分解为互不相互作用（或仅有库仑作用）的子系统。因此，一个通道 $\alpha$ 由一组守恒的量子数（如弹核的内禀态、相对轨道角动量等）来标记 [@problem_id:3552246]。

对于我们考虑的三体问题，通道可以由弹核的内部状态 $\phi_\alpha(\mathbf{r})$ 来定义，它是内部哈密顿量 $H_p$ 的本征态，满足 $H_p \phi_\alpha(\mathbf{r}) = \epsilon_\alpha \phi_\alpha(\mathbf{r})$。$\epsilon_\alpha$ 是弹核的内部能量。
- 如果 $\epsilon_\alpha < 0$，$\phi_\alpha$ 是一个束缚态（如氘核的基态）。
- 如果 $\epsilon_\alpha > 0$，$\phi_\alpha$ 是一个连续谱态，代表弹核已破裂成两个自由的团簇。

系统的总波函数 $\Psi(\mathbf{R}, \mathbf{r})$ 在渐近区域可以按通道展开。对于一个从初始通道 $\beta$（例如，弹核处于基态）开始的散射过程，其总波函数的渐进行为包含一个入射波部分和多个出射波部分：

$$\Psi_\beta^{(+)}(\mathbf{R}, \mathbf{r}) \xrightarrow{R\to\infty} \mathcal{I}_\beta(\mathbf{R})\phi_\beta(\mathbf{r}) + \sum_\alpha S_{\alpha\beta} \mathcal{O}_\alpha(\mathbf{R})\phi_\alpha(\mathbf{r})$$

这里，$\mathcal{I}_\beta$ 代表在初始通道 $\beta$ 中的入射球面波（或库仑波），$\mathcal{O}_\alpha$ 代表在末态通道 $\alpha$ 中的出射球面波（或库仑波）。连接入射和出射波幅度的复数系数 $S_{\alpha\beta}$ 构成了**散射矩阵（S-matrix）**。$S_{\alpha\beta}$ 的模方 $|S_{\alpha\beta}|^2$（乘以相应的相空间因子）给出了从初态 $\beta$ 跃迁到末态 $\alpha$ 的概率，因此S矩阵包含了关于散射过程的所有可观测量信息。

根据能量守恒，只有那些满足总能量 $E > \epsilon_\alpha$ 的通道才能在无穷远处被观测到，这些通道被称为**开放通道（open channels）**。对于那些 $E < \epsilon_\alpha$ 的通道，它们的相对运动动能为负，渐近波函数呈指数衰减，无法将粒子带到无穷远，这些通道被称为**闭合通道（closed channels）**。尽管闭合通道没有渐近的出射通量，但它们在相互作用区域内（$R$ 较小时）可以通过虚激发（virtual couplings）影响开放通道的动力学，从而改变开放通道之间的S矩阵元 [@problem_id:3552246]。

因此，求解散射问题的关键在于，为耦合方程设定正确的**渐近边界条件（asymptotic boundary conditions）**。对于一个从初态 $\alpha$ 入射的短程力散射问题，边界条件要求 [@problem_id:3552256]：
1.  在入射通道 $c=\alpha$ 中，解是入射波与出射波的叠加。
2.  在所有其他开放通道 $c \neq \alpha$ 中，解必须是纯出射波。
3.  在所有闭合通道中，解必须是指数衰减的。

数学上，对于开放通道，其径向波函数 $\chi_c(R)$ 的渐进行为由Hankel函数描述：

$$\chi_c(R) \xrightarrow{R\to\infty} \delta_{c\alpha}\,h^{(-)}_{L_\alpha}(k_\alpha R) + S_{c\alpha}\,h^{(+)}_{L_c}(k_c R)$$

其中 $h^{(-)}$ 和 $h^{(+)}$ 分别代表入射和出射球面波，$k_c = \sqrt{2\mu_{pT}(E-\epsilon_c)}/\hbar$ 是通道波数。对于闭合通道，其渐进行为是 $\chi_c(R) \propto \exp(-\kappa_c R)$，其中 $\kappa_c = \sqrt{2\mu_{pT}(\epsilon_c-E)}/\hbar$。如果存在长程库仑相互作用，则Hankel函数需被库仑波函数替代 [@problem_id:3552256]。

### CDCC方法的核心：连续谱的离散化

弹核的破裂态构成了一个能量连续的谱，这意味着存在无穷多个开放通道。直接处理无穷多个耦合通道在计算上是不可能的。CDCC方法的核心思想，就是用一个有限的、离散的、可对角化的（square-integrable, $L^2$）基来近似这个无穷的连续谱。这就是“连续谱离散化”的含义 [@problem_id:3552246]。

具体做法是，将弹核的内部连续谱按照动量 $k$ 或能量 $\epsilon = \hbar^2 k^2 / (2\mu_{tb})$ 分割成若干个区间，即“bins”。在每个bin内部，通过对真实的连续谱波函数进行加权平均，构造出一个 $L^2$ 的波包，这个波包就被当作一个新的、有效的离散态，称为**bin态**。

为了构造出物理意义明确且数值性能良好的bin态，必须精心选择叠加时的相位。一个朴素的平均会因为不同能量的波函数相位不一致而导致相消干涉，使得构造出的bin态振幅过小。一个成熟的方案是**平均相位法（average phase method）** [@problem_id:3552304]。真实散射态 $\phi_{\ell}(k,r)$ 在渐近区域的行为是 $\phi_{\ell}(k,r) \propto r^{-1} \sin(kr - \ell \pi/2 + \delta_{\ell}(k))$，其中 $\delta_{\ell}(k)$ 是散射相移。$k$ 的变化导致 $\delta_{\ell}(k)$ 变化，这是相位不一致的主要来源。因此，在构造bin态 $\phi_{\alpha}^{(\ell)}(r)$ 时，我们在积分中引入一个反向的相位因子 $e^{-i\delta_{\ell}(k)}$ 来抵消这个变化：

$$\phi_{\alpha}^{(\ell)}(r) = \mathcal{N}_{\alpha} \int_{k_{1}}^{k_{2}} \mathrm{d}k \, f_{\alpha}(k) \, e^{-i[\delta_{\ell}(k) - \bar{\delta}_{\alpha\ell}]} \, \phi_{\ell}(k,r)$$

其中 $[k_1, k_2]$ 定义了第 $\alpha$ 个bin，$f_\alpha(k)$ 是一个缓慢变化的权重函数，$\bar{\delta}_{\alpha\ell}$ 是该bin内的平均相移。这个操作使得被积函数中不同 $k$ 的分量在渐近区域的相位基本对齐，从而实现相长干涉，构造出具有显著空间振幅的bin态。

通过这种方式，无穷的连续谱被一个有限的集合（包含束缚态和所有bin态）所取代。总波函数 $\Psi(\mathbf{R}, \mathbf{r})$ 就可以在这个有限的离散基上展开：

$$\Psi(\mathbf{R}, \mathbf{r}) = \sum_{\alpha=0}^{N_{\text{model}}-1} \chi_{\alpha}(\mathbf{R}) \phi_{\alpha}(\mathbf{r})$$

其中 $\phi_0$ 是束缚基态，$\phi_{\alpha>0}$ 是代表连续谱的bin态。$\chi_{\alpha}(\mathbf{R})$ 是待求解的通道波函数。将此展开式代入三体薛定谔方程，并利用基函数 $\phi_\alpha$ 的正交性，就得到了一组有限数量的**耦合通道方程（coupled-channel equations）**。

### 耦合通道方程与耦合势

将波函数展开式代入薛定谔方程 $H_{\mathrm{rel}}\Psi = E\Psi$，并用 $\phi_\beta^*(\mathbf{r})$ 从左边积分，我们得到关于通道波函数 $\chi_\beta(\mathbf{R})$ 的方程组：

$$\left[ -\frac{\hbar^2}{2\mu_{pT}}\nabla_{\mathbf{R}}^2 + \epsilon_\beta - E \right] \chi_{\beta}(\mathbf{R}) + \sum_{\alpha} U_{\beta\alpha}(\mathbf{R}) \chi_{\alpha}(\mathbf{R}) = 0$$

这里的核心是**耦合势矩阵（coupling potential matrix）** $U_{\beta\alpha}(\mathbf{R})$，其定义为：

$$U_{\beta\alpha}(\mathbf{R}) = \int \phi_{\beta}^*(\mathbf{r}) \left[ V_{tT}\left(\left|\mathbf{R} + \frac{m_b}{m_p}\mathbf{r}\right|\right) + V_{bT}\left(\left|\mathbf{R} - \frac{m_t}{m_p}\mathbf{r}\right|\right) \right] \phi_{\alpha}(\mathbf{r}) d\mathbf{r}$$

耦合势 $U_{\beta\alpha}(\mathbf{R})$ 描述了由于弹核组分与靶核的相互作用，导致弹核从内部状态 $\alpha$ 跃迁到内部状态 $\beta$ 的过程。对角项 $U_{\alpha\alpha}(\mathbf{R})$ 描述了在通道 $\alpha$ 内的弹性散射，而非对角项 $U_{\beta\alpha}(\mathbf{R})$（$\beta \neq \alpha$）则驱动了非弹性散射和破裂过程。

在实际计算中，直接进行上述六维积分是困难的。通常采用**多极展开（multipole expansion）**来简化耦合势的计算，尤其是在外围区域（$r \ll R$）。我们将 $V_{tT}$ 和 $V_{bT}$ 对小位移 $\pm c \mathbf{r}$ 做泰勒展开。例如，对于一个标量场 $V(|\mathbf{R}+\mathbf{s}|)$，其展开式为：

$$V(|\mathbf{R}+\mathbf{s}|) \approx V(R) + (\mathbf{s} \cdot \hat{\mathbf{R}}) \frac{dV(R)}{dR} + \frac{1}{2} \sum_{i,j} s_i s_j \frac{\partial^2 V(R)}{\partial R_i \partial R_j} + \dots$$

将团簇-靶核相互作用代入并按内部坐标 $\mathbf{r}$ 的幂次和角动量秩 $\lambda$ 整理，就可以得到耦合势的多极分量 [@problem_id:3552314]。例如，最低阶的非平庸耦合项是电偶极（$\lambda=1$）和电四极（$\lambda=2$）跃迁。利用球谐函数加法定理，可以将耦合势分解为只依赖于 $\mathbf{R}$ 的径向部分和依赖于 $\mathbf{r}$ 与 $\mathbf{R}$ 角度的部分。例如，$\lambda=1$ 的耦合算符形式为：

$$V_{\lambda=1} \propto \left[ c_{t} \frac{d V_{tT}(R)}{dR} - c_{b} \frac{d V_{bT}(R)}{dR} \right] \sum_{\mu} Y_{1\mu}^*(\hat{\mathbf{R}}) (r Y_{1\mu}(\hat{\mathbf{r}}))$$

其中 $c_t = m_b/m_p$, $c_b=m_t/m_p$。这里的算符 $r Y_{1\mu}(\hat{\mathbf{r}})$ 是弹核内部的电偶极跃迁算符。通过计算这些内部算符在基态和bin态之间的矩阵元，我们就可以得到具体的耦合势形式。由于总哈密顿量的转动不变性，总角动量 $J$ 和宇称 $\pi$ 是守恒量。这使得庞大的耦合方程组可以按照不同的 $(J, \pi)$ 值分解成一系列独立的、规模小得多的块，极大地简化了计算 [@problem_id:3552263]。

### 破裂对弹性的影响：动力学极化势

CDCC方法不仅能计算破裂反应截面，还能极其精确地描述破裂道耦合对弹性散射的影响。这种影响可以通过引入**动力学极化势（Dynamic Polarization Potential, DPP）**的概念来深刻理解。

利用Feshbach的投影算符形式理论 [@problem_id:3552248]，我们可以将整个希尔伯特空间分为两部分：$P$ 空间和 $Q$ 空间。$P$ 空间由我们感兴趣的通道（通常是弹性通道，即弹核基态）构成，投影算符为 $P$。$Q$ 空间则包含所有其他通道（在这里是所有破裂bin态），投影算符为 $Q=1-P$。

始于薛定谔方程 $(E-H)\Psi = 0$，并将其投影到 $P$ 和 $Q$ 空间，得到一个方程组。通过形式上求解 $Q$ 空间的方程并代回到 $P$ 空间的方程中，我们可以得到一个只针对 $P$ 空间波函数 $\Psi_P = P\Psi$ 的有效单通道薛定谔方程：

$$[E - H_{PP} - H_{PQ}(E - H_{QQ} + i\epsilon)^{-1}H_{QP}] \Psi_P = 0$$

这里的有效哈密顿量包含了两部分：$H_{PP}$ 是在 $P$ 空间内的“裸”相互作用（对应于对角耦合势 $U_{00}$），而第二项 $\Delta U(E) = H_{PQ}(E - H_{QQ} + i\epsilon)^{-1}H_{QP}$ 就是DPP。DPP描述了所有通过虚激发进入 $Q$ 空间（破裂）、在其中传播、再退激发回到 $P$ 空间（弹性通道）的二级过程的总效应。

DPP具有两个至关重要的特性 [@problem_id:3552248]：
1.  **能量依赖性**：由于传播子 $(E - H_{QQ})^{-1}$ 的存在，DPP显式地依赖于散射能量 $E$。
2.  **非定域性**：在坐标表象中，DPP是一个积分算符。它在 $\mathbf{R}$ 点的作用依赖于波函数在所有其他点 $\mathbf{R}'$ 的值。其积分核的形式为 $\mathcal{K}(\mathbf{R}, \mathbf{R}'; E) \propto \sum_{\beta \in Q} U_{0\beta}(\mathbf{R}) G_{\beta}^{(+)}(\mathbf{R}, \mathbf{R}'; E) U_{\beta 0}(\mathbf{R}')$，其中 $G_{\beta}^{(+)}$ 是在破裂通道 $\beta$ 中的格林函数。这种非定域性的物理解释是：弹核在 $\mathbf{R}'$ 点发生虚破裂，破裂后的碎片传播到 $\mathbf{R}$ 点，然后再复合形成弹核。

这个非定域且能量依赖的DPP，加上裸势 $U_{00}$，共同构成了弹核感受到的总有效势。尽管DPP是如此复杂，但它的效应可以通过一个等效的**定域势（Equivalent Local Potential, ELP）**来近似，只要这个定域势能够在单通道计算中重现由完整CDCC计算得到的弹性散射可观测量（如相移、S矩阵元、微分截面等）。通过S矩阵反演等技术，可以从CDCC的计算结果中构造出这样的等效定域势，从而为理解和参数化破裂效应提供了一个直观的工具 [@problem_id:3552248]。

### 实际应用与有效性边界

作为一个数值方法，CDCC的计算结果的可靠性取决于其模型空间的完备性。因此，进行严格的**收敛性检验（convergence tests）**是任何CDCC研究中必不可少的一步 [@problem_id:3552253]。一个严谨的收敛方案通常包括：
1.  系统地、逐个地扩大模型空间参数，如增加弹核内部最大角动量 $l_{\max}$、最高连续谱能量 $E_{\max}$、每个分波的bin数量、耦合势多极展开的最高阶数 $\lambda_{\max}$ 以及总角动量 $L_{\max}$。
2.  在每一步扩大中，监控关键物理观测量（如弹性散射微分截面、相移）的稳定性。当进一步扩大模型空间不再引起可观测量的显著变化时，可以认为计算达到了收敛。
3.  检验结果对于离散化方案（如等能量间隔分bin与等动量间隔分bin）的不敏感性，是更高阶的验证手段 [@problem_id:3552253]。

模型空间的截断不可避免地导致部分反应通量的丢失。在一个完备的理论中，S矩阵是幺正的，总反应截面等于所有出射通道截面之和。在截断的CDCC空间内，计算出的S矩阵不再严格幺正，总通量会小于1。收敛的CDCC计算，其本质是使得被截断的模型空间之外的通量损失可以忽略不计。

尽管CDCC方法非常成功，但它并非万能的，其有效性有明确的边界。通过与“精确”的三体求解方法（如Faddeev/AGS方程）进行基准比较，可以清晰地揭示其局限性 [@problem_id:3552252]。CDCC方法可能变得不可靠或需要重大扩展的典型情景包括：
- **低能、库仑主导的反应**：在重靶上、接近库仑势垒的能量下，长程的库仑相互作用变得极为重要。这会导致耦合势衰减非常缓慢，需要极大的模型空间（非常高的角动量、极大的耦合半径）才能收敛，使得标准CDCC计算变得异常困难且对截断参数敏感 [@problem_id:3552284], [@problem_id:3552252]。
- **高能、相对论性反应**：当每个核子的能量达到数百MeV（如 $E/A \gtrsim 200 \text{ MeV}$），弹核速度接近光速，非相对论的薛定谔方程本身就失效了。必须采用包含相对论动力学的理论框架（如Eikonal-CDCC）来处理 [@problem_id:3552284]。
- **真实的“三体弹核”**：对于像 $^{6}\text{He}$（$\alpha+n+n$）这样的弹核，其本身就是三体系统。此时，整个散射问题是四体问题。标准的CDCC（基于三体模型）在结构上无法描述弹核内部复杂的三体关联和破裂模式，需要扩展到四体CDCC或使用专门为三体弹核设计的基 [@problem_id:3552284]。
- **重排/转移反应**：标准的CDCC方法只在入射通道的集团划分（如 $d+A \to p+n+A$）下展开波函数。它天生无法描述末态集团划分发生改变的反应，如转移反应 $(d,p)$（末态为 $p+(n+A)$）。因此，CDCC无法计算转移反应截面，这正是Faddeev/AGS等方法的优势所在 [@problem_id:3552252]。

总之，CDCC方法是解决弱束缚核反应问题的一个极其强大和灵活的工具。理解其基本原理、构造机制以及应用的局限性，是利用这一方法进行可靠的物理研究和预测的关键。