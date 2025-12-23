## 引言
[原子核](@entry_id:167902)作为一个复杂的[量子多体系统](@entry_id:141221)，展现出丰富的集体运动模式，例如[巨共振](@entry_id:159268)和超流现象。虽然[唯象模型](@entry_id:273816)能够有效描述这些集体行为，但从微观[核子](@entry_id:158389)相互作用出发，建立一个能够统一解释单粒子自由度和集体自由度之间耦合的理论框架，始终是核结构物理的核心挑战。[准粒子](@entry_id:136584)随机相近似 (Quasiparticle Random-Phase Approximation, QRPA) 正是应对这一挑战的基石理论之一，它为理解[原子核](@entry_id:167902)的[集体激发](@entry_id:145026)提供了强大而自洽的微观描述。本文旨在系统地阐述 QRPA 理论及其应用，填补从静态平均场认识到动态集体响应之间的知识鸿沟。

为实现这一目标，本文将分为三个部分。首先，在“原理与机制”一章中，我们将从时间相关的 [Hartree-Fock-Bogoliubov](@entry_id:750190) (TDHFB) 理论出发，详细推导 QRPA 方程，阐明其核心概念如准[玻色子](@entry_id:138266)近似、[基态关联](@entry_id:186115)和[自洽性](@entry_id:160889)的重要性。接着，在“应用与跨学科连接”一章中，我们将展示 QRPA 在解决具体物理问题中的威力，涵盖[原子核](@entry_id:167902)的电[磁激发](@entry_id:161593)、β衰变、[双贝塔衰变](@entry_id:160841)等关键领域，并探讨其在核天体物理中的关键作用以及与计算科学等其他学科的深刻联系。最后，“动手实践”部分将通过具体的计算任务，帮助读者动手实践，将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将全面掌握 QRPA 这一现代[核物理](@entry_id:136661)研究中的核心工具。

## 原理与机制

本章深入探讨[准粒子](@entry_id:136584)随机相近似 (Quasiparticle Random-Phase Approximation, QRPA) 的核心原理与机制。我们将从其作为时间相关的 [Hartree-Fock-Bogoliubov](@entry_id:750190) (TDHFB) 理论的[线性响应](@entry_id:146180)极限出发，构建其完整的理论框架。本章假定读者已经熟悉静态的 [Hartree-Fock-Bogoliubov (HFB)](@entry_id:750191) 方法，包括 Bogoliubov 变换和[准粒子](@entry_id:136584)真空的概念。我们将系统地推导 QRPA 方程，阐明其关键组成部分的物理意义，并讨论其在核结构物理中的重要应用和验证方法。

### 从时间相关的 HFB 到 QRPA

核系统中的[集体激发](@entry_id:145026)可以被理解为对 HFB [基态](@entry_id:150928)的微小[振动](@entry_id:267781)。描述这种动态演化的理论是**时间相关的 [Hartree-Fock-Bogoliubov](@entry_id:750190) (TDHFB) 理论**。在该理论中，系统的状态由广义[密度矩阵](@entry_id:139892) $\mathcal{R}(t)$ 描述，其演化遵循一个类似于量子力学中密度矩阵演化的方程。

在 Nambu-Gorkov 表象中，广义密度矩阵 $\mathcal{R}$ 和广义[平均场[哈密顿](@entry_id:751814)量](@entry_id:172864) $\mathcal{H}$ 具有特定的块结构。对于一个粒子数不守恒的超流系统，一个标准的表示是 ：
$$
\mathcal{R} = \begin{pmatrix}
\rho & \kappa \\
-\kappa^{*} & \mathbb{1}-\rho^{*}
\end{pmatrix}, \qquad
\mathcal{H} = \begin{pmatrix}
h[\rho]-\lambda & \Delta[\kappa] \\
-\Delta^{*}[\kappa] & -(h[\rho]-\lambda)^{*}
\end{pmatrix}
$$
这里，$\rho_{ij} = \langle c_{j}^{\dagger}c_{i} \rangle$ 是**正常[密度矩阵](@entry_id:139892)**，$\kappa_{ij} = \langle c_{j}c_{i} \rangle$ 是**配对张量**或反常密度，$h$ 是粒子-空穴平均场，$\Delta$ 是配对场，$\lambda$ 是为了约束[平均粒子数](@entry_id:151202)而引入的化学势。$\mathcal{R}$ 矩阵是一个厄米的[投影算符](@entry_id:154142)，满足 $\mathcal{R}^2 = \mathcal{R}$ 和 $\mathcal{R}^\dagger = \mathcal{R}$。

当系统受到一个弱的、时间相关的一体外场 $\mathcal{F}(t)$ 扰动时，其在 Nambu 空间中的形式为 $\mathcal{F}(t) = \begin{pmatrix} f(t) & 0 \\ 0 & -f^{*}(t) \end{pmatrix}$。系统的演化由 TDHFB 方程描述：
$$
\mathrm{i}\hbar \frac{d\mathcal{R}(t)}{dt} = \left[ \mathcal{H}[\mathcal{R}(t)]+\mathcal{F}(t), \mathcal{R}(t) \right]
$$
这个方程是[非线性](@entry_id:637147)的，因为自洽的平均场 $\mathcal{H}[\mathcal{R}(t)]$ 本身就是瞬时密度 $\mathcal{R}(t)$ 的函数。

**QRPA** 正是该方程在静态 HFB [基态](@entry_id:150928)解 $(\mathcal{R}_0, \mathcal{H}_0)$ 附近的小振幅极限。静态解满足 $[ \mathcal{H}_0, \mathcal{R}_0 ] = 0$。我们考虑微小的偏离：
$$
\mathcal{R}(t) = \mathcal{R}_{0}+\delta\mathcal{R}(t), \qquad \mathcal{H}(t) = \mathcal{H}_{0}+\delta\mathcal{H}(t)+\mathcal{F}(t)
$$
其中，**感应场** (induced field) $\delta\mathcal{H}(t)$ 是对密度变化 $\delta\mathcal{R}(t)$ 的[线性响应](@entry_id:146180)，$\delta\mathcal{H}(t)$ 与 $\delta\mathcal{R}(t)$ 呈线性关系。将这些展开式代入 TDHFB 方程并保留到一阶小量，我们得到**线性化的 TDHFB 方程** ：
$$
\mathrm{i}\hbar \frac{d\,\delta\mathcal{R}}{dt} = \left[ \mathcal{H}_{0}, \delta\mathcal{R} \right] + \left[ \delta\mathcal{H} + \mathcal{F}(t), \mathcal{R}_{0} \right]
$$
这个方程描述了系统对外场的[线性响应](@entry_id:146180)。对于自由[振荡](@entry_id:267781)（即 $\mathcal{F}(t)=0$），并假设[振动](@entry_id:267781)具有谐波形式 $\delta\mathcal{R}(t) = \delta\mathcal{R}(\omega) e^{-\mathrm{i}\omega t} + \text{h.c.}$，该方程就转化为一个本征值问题，即 QRPA 方程。

### QRPA [本征值问题](@entry_id:142153)

在对角化静态 HFB [哈密顿量](@entry_id:172864) $\mathcal{H}_0$ 的[准粒子](@entry_id:136584)基中，上述[线性响应](@entry_id:146180)方程可以写成一个著名的矩阵形式。在这个基中，[响应矩阵](@entry_id:754302) $\delta\mathcal{R}$ 的非对角块对应于产生两个[准粒子](@entry_id:136584)（前行振幅 $X$）和湮灭两个[准粒子](@entry_id:136584)（后行振幅 $Y$）。最终的 **QRPA 本征方程** 为一个广义厄米[本征问题](@entry_id:748835) ：
$$
\begin{pmatrix} A & B \\ B^{*} & A^{*} \end{pmatrix} \begin{pmatrix} X \\ Y \end{pmatrix}
= \omega \begin{pmatrix} \mathbb{1} & 0 \\ 0 & -\mathbb{1} \end{pmatrix} \begin{pmatrix} X \\ Y \end{pmatrix}
$$
其中，$\omega$ 是[激发态](@entry_id:261453)的能量（[声子](@entry_id:140728)能量）。

矩阵 $A$ 和 $B$ 分别被称为 **QRPA 矩阵**。
*   矩阵 $A$ 包含了未受扰动的两[准粒子能量](@entry_id:173936)（在其对角元上），以及前行散射的[剩余相互作用](@entry_id:159129)，即两[准粒子](@entry_id:136584)态之间的跃迁。
*   矩阵 $B$ 包含了后行散射的[剩余相互作用](@entry_id:159129)，它耦合了产生两个[准粒子](@entry_id:136584)和湮灭两个[准粒子](@entry_id:136584)的过程。$B$ 矩阵的存在是 RPA/QRPA 理论区别于较简单的 Tamm-Dancoff 近似 (TDA/QTDA) 的关键特征，它描述了[基态](@entry_id:150928)中已经存在的关联（[基态关联](@entry_id:186115)）。

为了确保理论的[自洽性](@entry_id:160889)，即[激发态](@entry_id:261453)的描述与[基态](@entry_id:150928)的描述源于同一个[能量泛函](@entry_id:170311)，QRPA 矩阵 $A$ 和 $B$ 必须由用于导出 HFB [基态](@entry_id:150928)的能量泛函 $E[\mathcal{R}]$ 的二阶泛函导数给出。具体来说，它们是在[准粒子](@entry_id:136584)基中能量 $E$ 的 Hessian 矩阵的相应块 ：
$$
A_{\mu\nu,\mu'\nu'} = (E_{\mu}+E_{\nu})\delta_{\mu\mu'}\delta_{\nu\nu'} + \left. \frac{\delta^{2}E}{\delta\mathcal{R}^{02}_{\nu\mu} \delta\mathcal{R}^{20}_{\mu'\nu'}} \right|_{\mathcal{R}^{0}}
$$
$$
B_{\mu\nu,\mu'\nu'} = \left. \frac{\delta^{2}E}{\delta\mathcal{R}^{02}_{\nu\mu} \delta\mathcal{R}^{02}_{\mu'\nu'}} \right|_{\mathcal{R}^{0}}
$$
这里，$E_\mu$ 是[准粒子能量](@entry_id:173936)，$\delta\mathcal{R}^{20}$ 和 $\delta\mathcal{R}^{02}$ 分别是对应于产生和湮灭一对[准粒子](@entry_id:136584)的广义密度变化。由于从粒[子基](@entry_id:151637)到[准粒子](@entry_id:136584)基的 Bogoliubov 变换混合了粒子和空穴态，这意味着 $A$ 和 $B$ 矩阵都同时接收来自**粒子-空穴** ($\delta^2 E / \delta\rho\delta\rho$) 和**粒子-粒子** ($\delta^2 E / \delta\kappa^*\delta\kappa$) 相互作用通道的贡献。

当使用如 Skyrme 或 Gogny 等依赖于密度的[能量密度泛函](@entry_id:161351) (EDF) 时，计算[二阶导数](@entry_id:144508)必须格外小心。能量泛函中的[耦合常数](@entry_id:747980)本身可能就是密度的函数，例如 $C[\rho(\mathbf{r})]$。根据泛函求导的链式法则，求[二阶导数](@entry_id:144508)时会产生额外的项，这些项被称为**重排项** (rearrangement terms) 。例如，$\delta C/\delta\rho$ 这样的导数项。这些项对于保持理论的完全[自洽性](@entry_id:160889)至关重要。

### 准[玻色子](@entry_id:138266)近似与 QRPA [声子](@entry_id:140728)

QRPA 的一个核心概念是**准[玻色子](@entry_id:138266)近似** (Quasiboson Approximation, QBA)。虽然[准粒子](@entry_id:136584)是[费米子](@entry_id:146235)，但 QRPA 将两[准粒子](@entry_id:136584)对的[产生算符](@entry_id:191512) $A_{ab}^{\dagger} = \alpha_{a}^{\dagger}\alpha_{b}^{\dagger}$ 和湮灭算符 $A_{ab} = \alpha_{b}\alpha_{a}$ 近似地视为[玻色子](@entry_id:138266)算符。

这种近似的根据在于，这些[费米子](@entry_id:146235)对算符的对易子在 HFB 真空态 $\lvert \Phi \rangle$（定义为 $\alpha_i \lvert \Phi \rangle = 0$）中的[期望值](@entry_id:153208)，恰好与[玻色子](@entry_id:138266)对易关系的形式一致 ：
$$
\langle \Phi \lvert [A_{ab}, A_{cd}^{\dagger}] \rvert \Phi \rangle = \delta_{ac}\delta_{bd} - \delta_{ad}\delta_{bc}
$$
QBA 就是用这个[期望值](@entry_id:153208)（一个 c-数）来代替[算符对易子](@entry_id:152475)本身。对该近似的偏离来自于对易子中包含的 $\alpha^\dagger\alpha$ 这样的两[准粒子](@entry_id:136584)算符项，它们破坏了完美的[玻色子](@entry_id:138266)代数。然而，这些修正项的效应在高集体性的[激发态](@entry_id:261453)中会变小。一个高度集体化的 **QRPA [声子](@entry_id:140728)** (phonon) 是大量（例如 $\Omega$ 个）两[准粒子](@entry_id:136584)组态的[相干叠加](@entry_id:170209)。在这种情况下，[泡利阻塞](@entry_id:160083)效应的修正项的量级大约为 $\mathcal{O}(1/\Omega)$，因此当集体性很强（$\Omega$ 很大）时，QBA 成为一个非常好的近似 。

在 QBA 框架下，一个 QRPA [声子](@entry_id:140728)的[产生算符](@entry_id:191512) $Q_\nu^\dagger$ 可以写成：
$$
Q_{\nu}^{\dagger} = \sum_{k} \left( X_{k}^{\nu} B_{k}^{\dagger} - Y_{k}^{\nu} B_{k} \right)
$$
其中 $B_k^\dagger$ 和 $B_k$ 是归一化的两[准粒子](@entry_id:136584)对的产生和湮灭算符，它们（近似地）满足[玻色子](@entry_id:138266)[对易关系](@entry_id:136780) $[B_k, B_{k'}^\dagger] \approx \delta_{kk'}$。$X_k^\nu$ 和 $Y_k^\nu$ 分别是前行和后行振幅，它们是 QRPA 本征方程的解。要求[声子](@entry_id:140728)算符自身也满足[玻色子](@entry_id:138266)[对易关系](@entry_id:136780) $[Q_\nu, Q_{\nu'}^\dagger] = \delta_{\nu\nu'}$，可以导出 QRPA 振幅的**[归一化条件](@entry_id:156486)** ：
$$
\sum_{k} \left( |X_{k}^{\nu}|^2 - |Y_{k}^{\nu}|^2 \right) = 1
$$
注意这个[归一化条件](@entry_id:156486)与通常的[向量归一化](@entry_id:149602)不同，它是一个“伪归一化”，反映了 QRPA 度规的非平庸结构。

我们可以通过一个具体的例子来理解 QRPA [本征向量](@entry_id:151813)的结构和集体性。假设一个 QRPA 计算给出了一个激发模式的（未归一化的）振幅，如 $X = (0.52, 0.34, \dots)$ 和 $Y = (0.10, 0.06, \dots)$。首先，我们可以计算 $\sum_k (X_k^2 - Y_k^2)$ 来检查其是否满足[归一化条件](@entry_id:156486)。如果不满足，可以通过一个标度因子进行重新归一化。其次，我们可以计算该模式的**[逆参与率](@entry_id:191299)** (Inverse Participation Ratio, IPR) 来衡量其**集体性**。IPR 的定义为 $\text{IPR} = \sum_k p_k^2$，其中 $p_k = (|X_k|^2 + |Y_k|^2) / \sum_j (|X_j|^2 + |Y_j|^2)$ 是第 $k$ 个组态的归一化权重 。IPR 的值介于 $1/N$（最大集体性，所有组态贡献均等）和 1（纯两[准粒子](@entry_id:136584)态）之间。

### 物理诠释与应用

QRPA 不仅是一个计算工具，它还提供了深刻的物理洞察力，并与其他理论和基本原理紧密相连。

#### HFB [基态](@entry_id:150928)的稳定性

QRPA 谱与 HFB [基态](@entry_id:150928)的稳定性直接相关。HFB 方程只保证了[能量泛函](@entry_id:170311)的一阶导数为零，即找到了一个极值点。要确定这个极值点是否是一个稳定的局域极小点，我们需要考察能量的二阶变分，即 Hessian 矩阵。QRPA 方程的求解本质上就是对这个 Hessian 矩阵的对角化。因此，HFB [基态](@entry_id:150928)是稳定的，当且仅当所有的 QRPA 本征能量 $\omega_\nu$ 都是实数。如果出现任何一个**虚数频率**（即 $\omega^2  0$），则表明 HFB [基态](@entry_id:150928)是不稳定的，系统会自发地演化到一个能量更低的形变状态 。

#### 赝模与[对称性恢复](@entry_id:181474)

根据 **Nambu-Goldstone 定理**，当一个[连续对称性](@entry_id:137257)被自发破缺时，谱中必须出现一个零能的 Nambu-Goldstone [玻色子](@entry_id:138266)。在 HFB+QRPA 框架中，尽管底层的能量泛函（或[哈密顿量](@entry_id:172864)）具有某些对称性，但 HFB [基态](@entry_id:150928)可能会破坏这些对称性。例如：
*   HFB [基态](@entry_id:150928)破坏了与粒子数守恒相关的**全局[规范对称性](@entry_id:136438) U(1)**。
*   HFB [基态](@entry_id:150928)通过将[原子核](@entry_id:167902)局域在空间某处而破坏了**平移对称性**。

在一个完全自洽的 QRPA 计算中（即[基态](@entry_id:150928)和[剩余相互作用](@entry_id:159129)源于同一个[能量泛函](@entry_id:170311)，并包含了所有重排项），这些破缺的对称性会导致谱中出现能量严格为零的**赝模** (spurious modes)。这些赝模的[产生算符](@entry_id:191512)对应于破缺对称性的生成元，例如[粒子数算符](@entry_id:153568) $\hat{N}$ 和总[动量算符](@entry_id:151743) $\hat{\mathbf{P}}$。这些[零能模](@entry_id:172472)与所有物理[激发态](@entry_id:261453)正交，必须从物理谱中分离出去。因此，检查这些赝模是否精确地位于零能，是验证 QRPA 计算自洽性的一个强有力的判据 。

#### 求和规则

**求和规则** (Sum Rules) 为验证 QRPA 计算的质量提供了模型无关的严格约束。对于一个任意的一体算符 $\hat{F}$，其最重要的两个求和规则是**非能量加权求和规则 (NEWSR)** 和**能量加权求和规则 (EWSR)**。它们可以被精确地表示为只依赖于[基态](@entry_id:150928)性质的表达式 ：
*   $m_0(\hat{F}) = \sum_\nu |\langle \nu | \hat{F} | 0 \rangle|^2 = \langle 0 | \hat{F}^\dagger \hat{F} | 0 \rangle - |\langle 0 | \hat{F} | 0 \rangle|^2$
*   $m_1(\hat{F}) = \sum_\nu E_\nu |\langle \nu | \hat{F} | 0 \rangle|^2 = \frac{1}{2} \langle 0 | [\hat{F}^\dagger, [\hat{H}, \hat{F}]] | 0 \rangle$

在 QRPA 计算中，只有当计算是完全自洽的（包括重排项）并且使用的组态空间足够大时，这些求和规则才会被满足。因此，通过比较 QRPA 谱计算出的 $m_0, m_1$ 的值与从[基态](@entry_id:150928)性质计算出的精确值，可以全面检验计算的[自洽性](@entry_id:160889)、模型空间的完备性以及赝模的分离情况。这与 Thouless 定理和 Goldstone 定理的要求是一致的。

#### QRPA 的不同类型

QRPA 理论可以应用于不同类型的激发。
*   在没有[配对关联](@entry_id:158315)的极限下（即配对场 $\Delta \to 0$），HFB 理论退化为 Hartree-Fock (HF) 理论。相应地，[准粒子](@entry_id:136584)退化为粒子或空穴。此时，两[准粒子](@entry_id:136584)组态退化为[粒子-空穴组态](@entry_id:753191)，而 **QRPA 也自然地退化为标准的粒子-空穴随机相近似 (RPA)**。在这种极限下，与粒子数对称性破缺相关的 Nambu-Goldstone 模也会消失 。
*   根据所涉及的[核子](@entry_id:158389)种类，QRPA 可分为两种主要类型 ：
    1.  **同类粒子 QRPA (lpQRPA)**：描述不改变质子数和中子数的激发，例如[巨共振](@entry_id:159268)。其[声子](@entry_id:140728)由质子-质子 ($pp$) 或中子-中子 ($nn$) 两[准粒子](@entry_id:136584)对构成，因此总的[同位旋](@entry_id:199830)第三分量 $\Delta T_z=0$。
    2.  **质子-中子 QRPA ([pnQRPA](@entry_id:753535))**：描述连接[原子核](@entry_id:167902)与其邻居核的**[电荷交换](@entry_id:186361)激发**，例如 $\beta$ 衰变和[中微子散射](@entry_id:158589)。其[声子](@entry_id:140728)由质子-中子 ($pn$) 两[准粒子](@entry_id:136584)对的相干叠加构成，其[同位旋](@entry_id:199830)第三分量改变 $\Delta T_z = \pm 1$。驱动这类激发的算符是[同位旋](@entry_id:199830)[升降算符](@entry_id:197899) $\hat{\tau}_\pm$，它们在[准粒子](@entry_id:136584)基中的表示包含了耦合质子和中子[准粒子](@entry_id:136584)的项，如 $\alpha^\dagger_p \alpha_n$ 和 $\alpha^\dagger_p \alpha^\dagger_{\bar{n}}$。

综上所述，QRPA 提供了一个强大而灵活的框架，用于研究[原子核](@entry_id:167902)的集体激发。它的成功依赖于对 HFB [基态](@entry_id:150928)的精确描述、理论的完全[自洽性](@entry_id:160889)（特别是对重排项的处理），以及对赝模和求和规则等基本物理原理的严格遵守。