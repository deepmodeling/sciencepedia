## 引言
在量子物理的宏伟殿堂中，理论工具的优雅与实用性同等重要。费曼-海尔曼定理正是这样一颗璀璨的明珠，它以一种惊人的简洁性，在系统的能量与内部物理量的[期望值](@entry_id:153208)之间架起了一座桥梁。然而，对于许多学习者和研究者而言，计算物理量的[期望值](@entry_id:153208)往往意味着求解复杂的[波函数](@entry_id:147440)并进行繁琐的积分，这一过程不仅耗时，有时甚至在解析上无法实现。本文旨在系统地揭示费曼-海尔曼定理如何巧妙地绕过这一障碍，为我们提供一种更直接、更具物理洞察力的计算途径。

在接下来的内容中，我们将分三个章节深入探索该定理。首先，在“原理与机制”一章中，我们将详细推导该定理，并阐明其核心思想——如何通过对[哈密顿量](@entry_id:172864)中的参数求导，来直接获得算符的[期望值](@entry_id:153208)。接着，在“应用与跨学科联系”一章，我们将展示该定理在原子物理、凝聚态物理、[量子化学](@entry_id:140193)乃至粒子物理等多个前沿领域的广泛应用，彰显其强大的普适性。最后，通过“动手实践”部分，读者将有机会亲手运用该定理解决具体的物理问题，从而巩固理解并体会其精妙之处。让我们一同开启这段探索之旅，领略量子世界中的深刻和谐。

## 原理与机制

在本章中，我们将深入探讨费曼-海尔曼（Feynman-Hellmann）定理的原理、机制及其在量子物理各个分支中的广泛应用。该定理是量子力学中一个极为强大而优美的工具，它在系统的[能量本征值](@entry_id:144381)与[哈密顿量](@entry_id:172864)中其他算符的[期望值](@entry_id:153208)之间建立了一座桥梁。通过巧妙地选择[哈密顿量](@entry_id:172864)中的参数，该定理使我们能够以一种非凡的、有时甚至是反直觉的方式，计算出那些通常需要复杂积分才能得到的物理量的[期望值](@entry_id:153208)。

### 费曼-海尔曼定理：基本原理

费曼-海尔曼定理指出，对于一个依赖于某个连续参数 $\lambda$ 的[哈密顿量](@entry_id:172864) $H(\lambda)$，其[能量本征值](@entry_id:144381) $E_n(\lambda)$ 对该参数的导数，等于[哈密顿量](@entry_id:172864)对该参数的偏导数在相应归一化本征态 $|\psi_n(\lambda)\rangle$ 下的[期望值](@entry_id:153208)。其数学表达式为：

$$
\frac{\partial E_n(\lambda)}{\partial \lambda} = \left\langle \psi_n(\lambda) \left| \frac{\partial H(\lambda)}{\partial \lambda} \right| \psi_n(\lambda) \right\rangle
$$

这个定理的证明异常简洁。我们从能量的[期望值](@entry_id:153208)表达式出发：$E_n(\lambda) = \langle \psi_n(\lambda) | H(\lambda) | \psi_n(\lambda) \rangle$。利用乘积法则对 $\lambda$ 求导，我们得到：

$$
\frac{\partial E_n}{\partial \lambda} = \left( \frac{\partial \langle \psi_n |}{\partial \lambda} \right) H | \psi_n \rangle + \langle \psi_n | \left( \frac{\partial H}{\partial \lambda} \right) | \psi_n \rangle + \langle \psi_n | H \left( \frac{\partial | \psi_n \rangle}{\partial \lambda} \right)
$$

利用定态薛定谔方程 $H|\psi_n\rangle = E_n|\psi_n\rangle$ 及其[厄米共轭](@entry_id:191215) $\langle\psi_n|H = E_n\langle\psi_n|$，上式可以改写为：

$$
\frac{\partial E_n}{\partial \lambda} = E_n \frac{\partial \langle \psi_n |}{\partial \lambda} | \psi_n \rangle + \left\langle \frac{\partial H}{\partial \lambda} \right\rangle + E_n \langle \psi_n | \frac{\partial | \psi_n \rangle}{\partial \lambda}
$$

$$
\frac{\partial E_n}{\partial \lambda} = E_n \frac{\partial}{\partial \lambda} \langle \psi_n | \psi_n \rangle + \left\langle \frac{\partial H}{\partial \lambda} \right\rangle
$$

由于本征态是归一化的，即 $\langle \psi_n | \psi_n \rangle = 1$，其对任何参数的导数均为零。因此，我们立即得到定理的最终形式。

该定理的精髓在于，它将一个[宏观可观测量](@entry_id:751601)（能量 $E_n$）的变化率与一个微观算符（$\partial H / \partial \lambda$）的[期望值](@entry_id:153208)直接联系起来。参数 $\lambda$ 的选择具有极大的灵活性，它可以是耦合常数、[粒子质量](@entry_id:156313)、外场强度，甚至是系统几何尺寸等任何可以连续变化的量。正是这种通用性，赋予了费曼-海尔曼定理强大的生命力。

### 在计算[期望值](@entry_id:153208)中的应用

费曼-海尔曼定理最直接的应用之一，就是计算各种物理量的[期望值](@entry_id:153208)，从而避免了求解复杂的[波函数](@entry_id:147440)和进行[多维积分](@entry_id:184252)。

#### 势能分量的计算

一个典型的例子是考虑一个质量为 $m$ 的粒子在一维吸引型狄拉克 $\delta$ 势 $V(x) = -g \delta(x)$ 中运动，其中 $g > 0$ 是势的强度。已知该体系的[基态能量](@entry_id:263704)为 $E = -\frac{m g^2}{2 \hbar^2}$。我们希望计算[势能](@entry_id:748988)的[期望值](@entry_id:153208) $\langle V \rangle$。若直接计算，我们需要先求解[波函数](@entry_id:147440)，然后计算积分 $\langle V \rangle = \int \psi^*(x) (-g\delta(x)) \psi(x) dx$。然而，通过费曼-海尔曼定理，我们可以选择势强度 $g$ 作为参数 $\lambda$。[哈密顿量](@entry_id:172864) $H = -\frac{\hbar^2}{2m} \frac{d^2}{dx^2} - g \delta(x)$ 对 $g$ 的偏导数为 $\frac{\partial H}{\partial g} = -\delta(x)$。根据定理：

$$
\frac{\partial E}{\partial g} = \left\langle \frac{\partial H}{\partial g} \right\rangle = \langle -\delta(x) \rangle = -\langle \delta(x) \rangle
$$

计算能量对 $g$ 的导数：$\frac{\partial E}{\partial g} = -\frac{m g}{\hbar^2}$。因此，$\langle \delta(x) \rangle = \frac{m g}{\hbar^2}$。[势能](@entry_id:748988)的[期望值](@entry_id:153208)为 $\langle V \rangle = \langle -g \delta(x) \rangle = -g \langle \delta(x) \rangle$，代入即可得到 $\langle V \rangle = -\frac{m g^2}{\hbar^2}$ [@problem_id:1094064]。值得注意的是，这个结果等于 $2E$，这是该体系[维里定理](@entry_id:146441)的一个体现，我们将在后面详细讨论。

该方法的威力在处理更复杂的势时同样显著。例如，对于高斯[势阱](@entry_id:151413) $V(x) = -V_0 \exp(-x^2/a^2)$，即使我们只知道一个近似的[基态能量](@entry_id:263704)表达式，如在深阱极限下的 $E_g(V_0) \approx -V_0 + \hbar \sqrt{\frac{V_0}{2ma^2}}$，我们依然可以计算 $\langle \exp(-x^2/a^2) \rangle$。选择势深 $V_0$ 作为参数，我们有 $\frac{\partial H}{\partial V_0} = -\exp(-x^2/a^2)$。因此，$\langle \exp(-x^2/a^2) \rangle = -\frac{dE_g}{dV_0}$。通过对近似能量求导，我们就能得到该算符[期望值](@entry_id:153208)的近似值 [@problem_id:1093947]。这种将定理应用于近似能量表达式（例如来自微扰论或变分法的结果）的策略，在多体物理和[量子化学](@entry_id:140193)中非常实用 [@problem_id:1093992]。

#### 动能与类维里关系

除了[势能](@entry_id:748988)，我们也可以通过巧妙选择参数来计算动能。考虑一个一维[无限深方势阱](@entry_id:136391)，宽度为 $L$，[基态能量](@entry_id:263704)为 $E_1 = \frac{\pi^2 \hbar^2}{2m L^2}$。为了求动能 $T = \frac{p^2}{2m}$ 的[期望值](@entry_id:153208)，我们可以将[哈密顿量](@entry_id:172864)中的质量 $m$ [参数化](@entry_id:272587)。一个聪明的选择是令 $\lambda = 1/m$。[哈密顿量](@entry_id:172864)变为 $H = \frac{\lambda p^2}{2} + V(x)$，能量表达式为 $E_1(\lambda) = \frac{\pi^2 \hbar^2}{2L^2} \lambda$。[哈密顿量](@entry_id:172864)对 $\lambda$ 的导数是 $\frac{\partial H}{\partial \lambda} = \frac{p^2}{2}$。根据定理：

$$
\left\langle \frac{p^2}{2} \right\rangle = \frac{\partial E_1}{\partial \lambda} = \frac{\pi^2 \hbar^2}{2L^2}
$$

而动能[期望值](@entry_id:153208) $\langle T \rangle = \left\langle \frac{p^2}{2m} \right\rangle = \lambda \left\langle \frac{p^2}{2} \right\rangle = \frac{1}{m} \left( \frac{\pi^2 \hbar^2}{2L^2} \right) = \frac{\pi^2 \hbar^2}{2mL^2}$，恰好等于总能量 $E_1$ [@problem_id:1094068]。这当然是意料之中的，因为在[势阱](@entry_id:151413)内部势能为零。

更有趣的应用出现在动能和势能都非零的情况。对于一维谐振子，其[哈密顿量](@entry_id:172864)为 $H = \frac{p^2}{2m} + \frac{1}{2} m \omega^2 x^2$，[基态能量](@entry_id:263704) $E_0 = \frac{1}{2}\hbar\omega$。同样取 $\lambda = 1/m$，[哈密顿量](@entry_id:172864)写作 $H(\lambda) = \frac{\lambda p^2}{2} + \frac{\omega^2 x^2}{2\lambda}$。关键在于，能量 $E_0$ 不依赖于 $\lambda$（即不依赖于质量 $m$）。因此，$\frac{\partial E_0}{\partial \lambda} = 0$。应用定理：

$$
0 = \left\langle \frac{\partial H}{\partial \lambda} \right\rangle = \left\langle \frac{p^2}{2} - \frac{\omega^2 x^2}{2\lambda^2} \right\rangle
$$

这意味着 $\langle \frac{p^2}{2} \rangle = \frac{\omega^2}{2\lambda^2} \langle x^2 \rangle$。将 $\lambda = 1/m$ 代回，我们得到 $\langle \frac{p^2}{2} \rangle = \frac{m^2 \omega^2}{2} \langle x^2 \rangle$。这实际上表明动能[期望值](@entry_id:153208)与[势能](@entry_id:748988)[期望值](@entry_id:153208)相等，即 $\langle T \rangle = \langle V \rangle$，这是谐振子的[维里定理](@entry_id:146441) [@problem_id:1093975]。同样的方法也适用于氢原子，通过对约化质量 $\mu$ [微分](@entry_id:158718)，可以证明 $\langle T \rangle = -E$，这也是库仑势下维里定理的一个特例 [@problem_id:1094084]。

### 与力和压强的联系：[广义力](@entry_id:169699)

当[哈密顿量](@entry_id:172864)中的参数是描述系统几何边界的变量时，费曼-海尔曼定理便与力、压强等宏观概念直接关联起来。在经典力学中，力是势能对位移的负梯度。在量子力学中，这个概念被推广为：与某个[广义坐标](@entry_id:156576) $\lambda$ 共轭的[广义力](@entry_id:169699) $F_\lambda$ 是系统总能量对该坐标的负导数，即 $F_\lambda = -\frac{\partial E}{\partial \lambda}$。

一个直观的例子是计算粒子对容器壁的力。考虑一个三维矩形无限深势阱，其边长为 $L_x, L_y, L_z$。基态能量为 $E_0 = \frac{\pi^2 \hbar^2}{2m} \left( \frac{1}{L_x^2} + \frac{1}{L_y^2} + \frac{1}{L_z^2} \right)$。粒子对位于 $x=L_x$ 的壁施加的力 $F_x$ 可以通过将 $L_x$ 视为参数来计算：

$$
F_x = -\frac{\partial E_0}{\partial L_x} = -\frac{\pi^2 \hbar^2}{2m} \frac{\partial}{\partial L_x} \left( L_x^{-2} \right) = \frac{\pi^2 \hbar^2}{m L_x^3}
$$

这提供了一个从第一性原理计算量子力学力的范例 [@problem_id:1094170]。类似地，我们可以计算粒子对容器壁的压强。对于一个边长为 $L$ 的立方体[势阱](@entry_id:151413)，体积 $V=L^3$，压强的[热力学](@entry_id:141121)定义是 $P = -\frac{\partial E}{\partial V}$。通过将[基态能量](@entry_id:263704) $E_0 = \frac{3\pi^2 \hbar^2}{2mL^2}$ 表示为体积 $V$ 的函数 $E_0(V) = \frac{3\pi^2 \hbar^2}{2m} V^{-2/3}$，我们可以直接求导得到[基态](@entry_id:150928)压强 [@problem_id:1093954]。这个概念可以推广到任意形状的边界，例如二维圆形[势阱](@entry_id:151413)中的压强 [@problem_id:1093949]。

该定理在分子物理和[量子化学](@entry_id:140193)中有着基石般的重要性。在[玻恩-奥本海默近似](@entry_id:146252)下，[原子核](@entry_id:167902)的位置被视为固定参数，我们求解电子的薛定谔方程。总能量 $E$ 是电子能量 $E_{el}$ 和核间经典[静电排斥](@entry_id:162128)能 $V_{NN}$ 之和。作用在某个[原子核](@entry_id:167902) $\alpha$ 上的量子力学力定义为 $\mathbf{F}_\alpha^{QM} = -\nabla_{\mathbf{R}_\alpha} E$。费曼和海尔曼独立证明，这个力完全等同于一个经典图像下的静电力：即其他所有[原子核](@entry_id:167902)对[原子核](@entry_id:167902) $\alpha$ 的库仑排斥力，加上由电子[波函数](@entry_id:147440)决定的静态电子云[电荷密度](@entry_id:144672) $\rho_e(\mathbf{r})$ 对[原子核](@entry_id:167902) $\alpha$ 的库仑吸[引力](@entry_id:175476)之和。

$$
\mathbf{F}_\alpha^{QM} = -\nabla_{\mathbf{R}_\alpha} (E_{el} + V_{NN}) = -\langle \Psi_{el} | \nabla_{\mathbf{R}_\alpha} H_{el} | \Psi_{el} \rangle - \nabla_{\mathbf{R}_\alpha} V_{NN}
$$

其中，$\langle \Psi_{el} | \nabla_{\mathbf{R}_\alpha} H_{el} | \Psi_{el} \rangle$ 正是电子云对[原子核](@entry_id:167902) $\alpha$ 的作用力。这个结果（即现在的费曼-海尔曼定理）意义非凡，因为它将抽象的量子力学能量梯度与直观的经典静电力图像联系起来，极大地简化了[分子动力学模拟](@entry_id:160737)中力的计算 [@problem_id:1094063]。

### 对外场的响应：[磁化率](@entry_id:138219)与[极化率](@entry_id:143513)

当参数 $\lambda$ 是外场（如[电场](@entry_id:194326)或[磁场](@entry_id:153296)）的强度时，费曼-海尔曼定理描述了系统如何响应这些外场，其[能量导数](@entry_id:170468)对应于各种磁化率或[极化率](@entry_id:143513)。

考虑一个带电[谐振子](@entry_id:155622)在外加[匀强电场](@entry_id:264305) $\mathcal{E}$ 中的情况，[哈密顿量](@entry_id:172864)为 $H = \frac{p^2}{2m} + \frac{1}{2}m\omega^2 x^2 - q\mathcal{E}x$。我们希望计算体系的感生电偶极矩，它与 $\langle x \rangle$ 成正比。选择[电场](@entry_id:194326)强度 $\mathcal{E}$ 作为参数，我们有 $\frac{\partial H}{\partial \mathcal{E}} = -qx$。因此，定理给出：

$$
\langle qx \rangle = -\frac{\partial E_0}{\partial \mathcal{E}}
$$

通过对[哈密顿量](@entry_id:172864)进行配方，可以得到基态能量 $E_0(\mathcal{E}) = \frac{1}{2}\hbar\omega - \frac{q^2 \mathcal{E}^2}{2m\omega^2}$。对其求导便可得到 $\langle qx \rangle$ [@problem_id:1094030]。

一个更经典的例子是氢原子在弱[电场](@entry_id:194326)中的[斯塔克效应](@entry_id:146306)。[哈密顿量](@entry_id:172864)的微扰项为 $H' = -p_z \mathcal{E}$，其中 $p_z = -ez$ 是 z 方向的[电偶极矩](@entry_id:178520)算符。根据微扰论，[基态能量](@entry_id:263704)在[二阶修正](@entry_id:199233)下变为 $E_g(\mathcal{E}) = E_g^{(0)} - \frac{1}{2}\alpha \mathcal{E}^2$，其中 $\alpha$ 是静态极化率（对于氢原子，$\alpha = \frac{9}{2}(4\pi\epsilon_0) a_0^3$）。应用费曼-海尔曼定理，感生[电偶极矩](@entry_id:178520)的[期望值](@entry_id:153208)为：

$$
\langle p_z \rangle = \left\langle -\frac{\partial H}{\partial \mathcal{E}} \right\rangle = -\frac{\partial E_g}{\partial \mathcal{E}} = - \frac{\partial}{\partial \mathcal{E}} \left( E_g^{(0)} - \frac{1}{2}\alpha \mathcal{E}^2 \right) = \alpha \mathcal{E}
$$

这个结果清晰地表明，[极化率](@entry_id:143513) $\alpha$ 是感生偶极矩与外场的比例系数，并且可以通过能量对场的二阶响应来定义 [@problem_id:1094094]。同样的技术也适用于计算其他体系（如二维[量子转子](@entry_id:753948)）的感生电偶极矩 [@problem_id:1094148]。

这个思想可以进一步推广。能量对参数的[二阶导数](@entry_id:144508)通常定义了物理学中的各种响应函数或“刚度”。例如，在凝聚态物理中，[超流密度](@entry_id:142018) $\rho_s$ 可以通过计算系统基态能量对施加在边界上的一个微小相位扭曲 $\theta$ 的[二阶导数](@entry_id:144508)来定义，即 $\rho_s \propto \frac{d^2 E_0}{d\theta^2}$ [@problem_id:1094143]。

### [量子维里定理](@entry_id:176645)：通过[标度变换](@entry_id:166413)建立的深层联系

前面我们已经多次遇到维里定理的特例。实际上，[维里定理](@entry_id:146441)本身可以通过一种与费曼-海尔曼定理思想类似的[标度论证](@entry_id:273307)方法导出。这个方法不仅优雅，而且揭示了动能和[势能](@entry_id:748988)[期望值](@entry_id:153208)之间的深刻普适关系。

考虑一个粒子在[中心势](@entry_id:148563) $V(r) = C r^n$ 中运动，其定态[波函数](@entry_id:147440)为 $\psi(\mathbf{r})$。我们可以构造一个依赖于标度参数 $\lambda$ 的试探波函数族 $\psi_\lambda(\mathbf{r}) = \lambda^{3/2} \psi(\lambda\mathbf{r})$（因子 $\lambda^{3/2}$ 确保归一化）。对于这个试探态，能量的[期望值](@entry_id:153208)为 $E(\lambda) = \langle \psi_\lambda | H | \psi_\lambda \rangle$。通过变量代换可以证明：

$$
E(\lambda) = \lambda^2 \langle T \rangle + \lambda^{-n} \langle V \rangle
$$

其中 $\langle T \rangle$ 和 $\langle V \rangle$ 是在真实本征态（即 $\lambda=1$ 的态）下的[期望值](@entry_id:153208)。根据变分原理，由于 $\psi(\mathbf{r})$ 是真实的[本征态](@entry_id:149904)，能量 $E(\lambda)$ 在 $\lambda=1$ 处必须取极小值。因此，$\frac{dE(\lambda)}{d\lambda}\Big|_{\lambda=1} = 0$。计算导数并令 $\lambda=1$：

$$
\frac{dE}{d\lambda}\Big|_{\lambda=1} = [2\lambda \langle T \rangle - n\lambda^{-n-1} \langle V \rangle]_{\lambda=1} = 2\langle T \rangle - n\langle V \rangle = 0
$$

这就导出了[幂律势](@entry_id:149253)下的[量子维里定理](@entry_id:176645)：$2\langle T \rangle = n\langle V \rangle$ [@problem_id:1094192]。

这个定理具有很好的线性叠加性。如果势是多个[幂律势](@entry_id:149253)的组合，例如 $V(x) = \lambda_2 x^2 + \lambda_4 x^4$，那么[维里定理](@entry_id:146441)也相应地叠加，即 $2\langle T \rangle = 2\langle V_2 \rangle + 4\langle V_4 \rangle$ [@problem_id:1094149]。对于包含吸引和排斥项的势，如 $V(r) = \lambda_1 r^{-1} + \lambda_2 r^2$，同样有 $2\langle T \rangle = -1 \cdot \langle V_1 \rangle + 2 \cdot \langle V_2 \rangle$ [@problem_id:1093989]。这个关系更普适的形式是 $2\langle T \rangle = \langle \mathbf{r} \cdot \nabla V \rangle$。

需要注意的是，维里定理的推导依赖于动能和势能算符在坐标标度变换下的特定行为。如果[哈密顿量](@entry_id:172864)中包含不依赖于坐标或动量（或以不同方式依赖）的项，例如自旋-轨道耦合项 $\lambda \mathbf{L}\cdot\mathbf{S}$，由于它在坐标[标度变换](@entry_id:166413)下不变，因此它不会出现在最终的维里关系中。标准[维里定理](@entry_id:146441)在这种情况下依然成立 [@problem_id:1094006]。

最后，我们可以将费曼-海尔曼定理与[量纲分析](@entry_id:140259)结合，来反过来验证[维里定理](@entry_id:146441)。对于一个势为 $V(r) = \lambda r^\nu$ 的体系，通过量纲分析可以确定[能量本征值](@entry_id:144381) $E$ 必须具有 $E \propto (\hbar^2/m)^{\nu/(\nu+2)} \lambda^{2/(\nu+2)}$ 的形式。然后，通过对 $\lambda$ 应用费曼-海尔曼定理，可以求出 $\langle V \rangle = \frac{2}{\nu+2}E$，进而求出 $\langle T \rangle = \frac{\nu}{\nu+2}E$。从这两个表达式可以立即验证 $2\langle T \rangle = \nu \langle V \rangle$ 成立 [@problem_id:1094118]。

### 对[统计力](@entry_id:194984)学的推广

费曼-海尔曼定理的原理可以无缝推广到有限温度的系综中。在这种情况下，我们关注的是体系的亥姆霍兹自由能 $F = -k_B T \ln Z$，其中 $Z = \text{Tr}(e^{-\beta H})$ 是[配分函数](@entry_id:193625)，$\beta = 1/(k_B T)$。

如果[哈密顿量](@entry_id:172864)依赖于参数 $\lambda$，那么自由能对 $\lambda$ 的导数为：

$$
\frac{\partial F}{\partial \lambda} = -k_B T \frac{1}{Z} \frac{\partial Z}{\partial \lambda} = -k_B T \frac{1}{Z} \text{Tr}\left( \frac{\partial}{\partial \lambda} e^{-\beta H} \right)
$$

使用算符指数的导数公式并考虑到迹的循环[不变性](@entry_id:140168)，可以证明：

$$
\frac{\partial F}{\partial \lambda} = \frac{1}{Z} \text{Tr}\left( e^{-\beta H} \frac{\partial H}{\partial \lambda} \right) = \left\langle \frac{\partial H}{\partial \lambda} \right\rangle_T
$$

这里的 $\langle \dots \rangle_T$ 表示在温度 $T$ 下的正则系综平均。这个结果是费曼-海尔曼定理在[统计力](@entry_id:194984)学中的直接对应。

一个简单的例子是考虑一个能级为 $E_1=0$ 和 $E_2=\Delta$ 的[二能级系统](@entry_id:138452)。其[哈密顿量](@entry_id:172864)可以写成 $H = \Delta |2\rangle\langle 2|$。我们想计算其[热力学平均](@entry_id:755909)能量 $\langle H \rangle$。选择能级分裂 $\Delta$ 作为参数 $\lambda$，则 $\frac{\partial H}{\partial \Delta} = |2\rangle\langle 2|$。根据推广的定理，$\frac{\partial F}{\partial \Delta} = \langle |2\rangle\langle 2| \rangle_T = p_2$，即粒子处于[激发态](@entry_id:261453)的概率。系统的[平均能量](@entry_id:145892)为 $\langle H \rangle = 0 \cdot p_1 + \Delta \cdot p_2 = \Delta p_2$。因此，$\langle H \rangle = \Delta \frac{\partial F}{\partial \Delta}$。通过计算[配分函数](@entry_id:193625) $Z = 1 + e^{-\beta \Delta}$ 和自由能 $F = -k_B T \ln(1+e^{-\beta\Delta})$，并对其求导，我们可以轻易地得到系统的[平均能量](@entry_id:145892) $\langle H \rangle = \frac{\Delta}{e^{\Delta / (k_B T)} + 1}$ [@problem_id:1094138]。