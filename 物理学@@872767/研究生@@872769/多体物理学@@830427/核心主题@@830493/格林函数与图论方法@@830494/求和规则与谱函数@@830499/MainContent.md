## 引言
在庞杂的多体量子世界中，粒子间的复杂相互作用催生了从超导到[夸克禁闭](@entry_id:143757)等一系列奇妙的物理现象。然而，这种复杂性也为理论描述和实验验证带来了巨大挑战。我们如何才能从微观的动力学细节中提炼出普适的规律？又如何检验我们构建的理论模型的有效性？[谱函数](@entry_id:147628)与求和规则正是应对这些核心问题的强大理论武器。它们共同构成了一座桥梁，一端连接着描述粒子激发的微观谱信息，另一端则连接着系统的[宏观可观测量](@entry_id:751601)和基本守恒律。

本文旨在系统性地介绍谱函数与求和规则的理论及其应用。读者将通过三个章节的学习，全面掌握这一核心概念：
*   **第一章：原理与机制**，我们将从量子力学的第一性原理出发，深入探讨[谱函数](@entry_id:147628)的定义、其与[格林函数](@entry_id:147802)的深刻联系，并推导出一系列作为精确约束而存在的求和规则。
*   **第二章：应用与跨学科联系**，我们将把视野拓宽到具体的物理问题中，展示求和规则如何在凝聚态物理、粒子物理和[核物理](@entry_id:136661)等前沿领域中，被用来解释实验现象、约束理论模型。
*   **第三章：动手实践**，通过一系列精心设计的计算问题，读者将有机会亲手应用所学知识，巩固对[谱函数](@entry_id:147628)和求和规则的理解，并体会它们在解决实际问题中的威力。

通过本文的学习，你将不仅理解谱函数与求和规则的数学形式，更将领会其作为物理学中深刻统一思想的精髓。

## 原理与机制

在本章中，我们将深入探讨[多体物理学](@entry_id:144526)中的两个核心概念：谱函数 (spectral function) 和求和规则 (sum rules)。谱函数是连接理论与实验的关键桥梁，它揭示了系统中单粒子激发的基本信息。而求和规则是源于量子力学基本原理的精确约束，为任何有效的理论或近似提供了严格的检验标准。我们将从基本定义出发，系统地构建这些概念，并通过一系列的应用展示它们的威力。

### [谱函数](@entry_id:147628)的基本性质

在[多体量子系统](@entry_id:161678)中，我们常常关心向系统中添加或移除一个粒子会发生什么。这些过程的概率和能量[分布](@entry_id:182848)被一个称为**单粒子谱函数** (single-particle spectral function) 的核心量所捕获，通常记为 $A(\mathbf{k}, \omega)$。此函数依赖于动量 $\mathbf{k}$ 和能量 $\omega$。

#### Lehmann 表示及其物理意义

[谱函数](@entry_id:147628)最直观的定义来自于其 **Lehmann 表示**。在零温下，对于一个包含 $N$ 个粒子的系统，其谱函数可以写作：
$$
A(\mathbf{k}, \omega) = \sum_m |\langle \Psi_m^{N+1} | c_{\mathbf{k}}^\dagger | \Psi_0^N \rangle|^2 \delta(\omega - (E_m^{N+1} - E_0^N)) + \sum_n |\langle \Psi_n^{N-1} | c_{\mathbf{k}} | \Psi_0^N \rangle|^2 \delta(\omega - (E_0^N - E_n^{N-1}))
$$
这里，$|\Psi_0^N\rangle$ 是 $N$ 粒子系统的[基态](@entry_id:150928)，能量为 $E_0^N$。$c_{\mathbf{k}}^\dagger$ 和 $c_{\mathbf{k}}$ 分别是在动量为 $\mathbf{k}$ 的模式上产生和湮灭一个粒子的算符。总和遍历 $(N+1)$ 和 $(N-1)$ [粒子系统](@entry_id:180557)的所有[本征态](@entry_id:149904) $|\Psi_m^{N+1}\rangle$ 和 $|\Psi_n^{N-1}\rangle$。

这个表达式有非常清晰的物理图像：
1.  **粒子部分 (Particle Part)**: 第一项对应于在动量为 $\mathbf{k}$ 的模式上向系统中添加一个粒子的过程。它只在 $\omega > \mu$ 时有贡献，其中 $\mu = E_0^{N+1} - E_0^N$ 是化学势。这部分的[谱函数](@entry_id:147628)可以通过**反光[电子能谱](@entry_id:160814) (Inverse Photoemission Spectroscopy, IPES)** 等实验技术探测。其中的 $\delta$ 函数确保了[能量守恒](@entry_id:140514)：我们注入的能量 $\omega$ 必须等于系统从 $N$ 粒[子基](@entry_id:151637)态跃迁到 $(N+1)$ 粒子某个[激发态](@entry_id:261453)所需的能量。

2.  **空穴部分 (Hole Part)**: 第二项对应于从系统中移除一个动量为 $\mathbf{k}$ 的粒子的过程。它只在 $\omega  \mu$ 时有贡献。这部分可以通过**光电子能谱 (Photoemission Spectroscopy, PES)** 探测。同样，$\delta$ 函数保证[能量守恒](@entry_id:140514)。

因此，[谱函数](@entry_id:147628) $A(\mathbf{k}, \omega)$ 完整地描述了单粒子激发的[能谱](@entry_id:181780)，即在给定的动量 $\mathbf{k}$ 下，以能量 $\omega$ 激发系统的可能性。

#### 与格林函数的关系

[谱函数](@entry_id:147628)与系统的**[单粒子格林函数](@entry_id:140400)** (Green's function) 密切相关，后者是研究多体系统动力学性质的强大数学工具。特别是，**[推迟格林函数](@entry_id:139183)** ([retarded Green's function](@entry_id:139183)) $G^R(\mathbf{k}, \omega)$ 与谱函数之间存在一个简单的关系：
$$
A(\mathbf{k}, \omega) = -\frac{1}{\pi} \text{Im}[G^R(\mathbf{k}, \omega)]
$$
这个关系至关重要，因为它将[谱函数](@entry_id:147628)这个直接的物理可观测量与[格林函数](@entry_id:147802)这个强大的理论计算工具联系起来。格林函数 $G^R(\mathbf{k}, z)$ 在[复频率](@entry_id:266400)平面 $z$ 的上半平面是解析的，这一性质是**因果律 (causality)** 的直接体现。正是这种解析性，引出了连接谱函数实部和虚部的 **[Kramers-Kronig 关系](@entry_id:140966)**，并成为许多求和规则的深刻根源。

### 零阶矩求和规则：概率守恒

最基本也最重要的求和规则是[谱函数](@entry_id:147628)的**零阶矩** (zeroth moment)，即[谱函数](@entry_id:147628)对所有频率的积分。这个积分代表了在给定动量 $\mathbf{k}$ 下，添加或移除一个粒子的总概率。

我们可以通过对 Lehmann 表示进行积分来直接推导这个规则 [@problem_id:1191298]。考虑一个[费米子](@entry_id:146235)系统，其产生和[湮灭算符](@entry_id:165390)满足[正则对易关系](@entry_id:185041) (Canonical Anticommutation Relations, CAR)：$\{c_{\mathbf{k}\sigma}, c_{\mathbf{k'}\sigma'}^\dagger\} = \delta_{\mathbf{k}, \mathbf{k'}} \delta_{\sigma, \sigma'}$。在零温下，谱函数的积分为：
$$
\int_{-\infty}^{\infty} d\omega \, A_{\sigma}(\mathbf{k}, \omega) = \int_{-\infty}^{\infty} d\omega \, \left[ \sum_{n} |\langle n | c_{\mathbf{k}\sigma}^\dagger | 0 \rangle|^2 \delta(\omega - E_n) + \sum_{n} |\langle n | c_{\mathbf{k}\sigma} | 0 \rangle|^2 \delta(\omega + E_n) \right]
$$
利用 $\delta$ 函数的性质，积分结果为：
$$
\sum_{n} |\langle n | c_{\mathbf{k}\sigma}^\dagger | 0 \rangle|^2 + \sum_{n} |\langle n | c_{\mathbf{k}\sigma} | 0 \rangle|^2 = \langle 0 | c_{\mathbf{k}\sigma} c_{\mathbf{k}\sigma}^\dagger | 0 \rangle + \langle 0 | c_{\mathbf{k}\sigma}^\dagger c_{\mathbf{k}\sigma} | 0 \rangle = \langle 0 | \{ c_{\mathbf{k}\sigma}, c_{\mathbf{k}\sigma}^\dagger \} | 0 \rangle
$$
这里我们利用了[完备性关系](@entry_id:139077) $\sum_n |n\rangle\langle n| = \hat{1}$。根据 CAR，$\{c_{\mathbf{k}\sigma}, c_{\mathbf{k}\sigma}^\dagger\} = 1$。因此，我们得到了一个极其普适的结果：
$$
\int_{-\infty}^{\infty} d\omega \, A_{\sigma}(\mathbf{k}, \omega) = \langle 0 | 1 | 0 \rangle = 1
$$
这个结果被称为**零阶矩求和规则**或**总权[重求和](@entry_id:275405)规则**。它表明，对于任何给定的动量和自旋，谱函数的总积分为 1。这个规则是粒子数守恒和量子力学基本对易关系的直接体现，它不依赖于系统[哈密顿量](@entry_id:172864)的具体形式，因此对任何相互作用强度都成立。

这个求和规则也可以从格林函数的[解析性](@entry_id:140716)质通过复变分析推导出来 [@problem_id:645386]。考虑一个任意归一化态 $|\phi\rangle$，其关联的[格林函数](@entry_id:147802) $g(z) = \langle\phi| (z-H)^{-1} |\phi\rangle$。由于[哈密顿量](@entry_id:172864) $H$ 是自伴的，$g(z)$ 在上半复平面解析。通过在[上半平面](@entry_id:199119)构造一个大的半圆形围道对 $g(z)$ 进行积分，并利用 $g(z) \sim 1/z$ 当 $|z| \to \infty$ 的行为，可以证明 $\int_{-\infty}^{\infty} \text{Im}[g(E+i0)] dE = -\pi$。结合谱函数的定义 $A(E) = - \frac{1}{\pi} \text{Im}[g(E+i0)]$，我们再次得到 $\int A(E) dE = 1$。这种推导方式突出了求和规则与因果律的深刻联系。

这个基本规则有广泛的应用。例如，在**[单杂质安德森模型](@entry_id:138488) (SIAM)** 中，描述磁性杂质的 d [轨道](@entry_id:137151)的[谱函数](@entry_id:147628) $A_d(\omega)$，即使在存在与[传导电子](@entry_id:145260)复杂的杂化和强[库仑相互作用](@entry_id:747947) $U$ 的情况下，其总积分权重（对两个[自旋求和](@entry_id:162099)后）也必须为 2 [@problem_id:1201361]。另一个例子是在 **BCS [超导体](@entry_id:191025)**理论中，基本激发是[电子和空穴](@entry_id:274534)的相干叠加，即**博戈留波夫[准粒子](@entry_id:136584)** (Bogoliubov quasiparticle)。尽管其构成复杂，但与一个[准粒子](@entry_id:136584)相关的总[谱权重](@entry_id:144751)仍然精确地为 1，这表明它是一个良定义的、[概率守恒](@entry_id:149166)的激发 [@problem_id:1201318]。

### [高阶矩](@entry_id:266936)求和规则与可观测量

除了总权重，谱函数的**矩** (moments) 也遵循严格的求和规则，它们将[谱函数](@entry_id:147628)的形状与系统的静态[可观测量](@entry_id:267133)联系起来。

#### 谱函数的分解与[动量分布](@entry_id:162113)

我们可以将总[谱权重](@entry_id:144751)分解为占据（空穴）和未占据（粒子）两部分。对[谱函数](@entry_id:147628)的空穴部分积分，可以直接得到该动量态的**[基态](@entry_id:150928)[动量分布](@entry_id:162113)函数** $n(\mathbf{k})$ [@problem_id:1201350]：
$$
\int_{-\infty}^{\mu} d\omega \, A(\mathbf{k}, \omega) = \langle \Psi_0^N | c_{\mathbf{k}}^\dagger c_{\mathbf{k}} | \Psi_0^N \rangle = n(\mathbf{k})
$$
这个关系极其有用，因为它意味着通过对光电子能谱信号在[费米面](@entry_id:137798)以下进行积分，可以直接测量出动量分布函数 $n(\mathbf{k})$。相应地，对粒子部分的积分给出 $1 - n(\mathbf{k})$，即在动量为 $\mathbf{k}$ 的态上添加一个粒子的概率。

#### 一阶矩与平均能量

[谱函数](@entry_id:147628)的**一阶矩** (first moment) 给出了[谱分布](@entry_id:158779)的平均能量。它与[哈密顿量](@entry_id:172864)直接相关：
$$
\int_{-\infty}^{\infty} d\omega \, \omega \, A_{\sigma}(\mathbf{k}, \omega) = \langle \{ [c_{\mathbf{k}\sigma}, H], c_{\mathbf{k}\sigma}^\dagger \} \rangle_0
$$
这里，$\langle \dots \rangle_0$ 表示在[基态](@entry_id:150928)中的[期望值](@entry_id:153208)。这个关系式将谱函数的[平均能量](@entry_id:145892)与算符 $c_{\mathbf{k}\sigma}$ 和[哈密顿量](@entry_id:172864) $H$ 之间的对易子联系起来。

让我们以 **Hubbard 模型**为例 [@problem_id:3016584] [@problem_id:1168707]。其[哈密顿量](@entry_id:172864)为 $H = \sum_{\mathbf{k},\sigma} (\epsilon_{\mathbf{k}} - \mu) c_{\mathbf{k}\sigma}^\dagger c_{\mathbf{k}\sigma} + U \sum_{i} n_{i\uparrow} n_{i\downarrow}$。通过计算对易子 $[c_{\mathbf{k}\sigma}, H]$，我们可以得到一阶矩的精确表达式：
$$
\int_{-\infty}^{\infty} d\omega \, \omega \, A_{\sigma}(\mathbf{k}, \omega) = \epsilon_{\mathbf{k}} - \mu + U \langle n_{-\sigma} \rangle
$$
其中 $\langle n_{-\sigma} \rangle$ 是系统中平均的相反自旋的电子密度。这个结果表明，相互作用 $U$ 将谱的中心能量从非相互作用值 $\epsilon_{\mathbf{k}} - \mu$ 移动了一个量 $U \langle n_{-\sigma} \rangle$。在半满的 Mott 绝缘体中，$\langle n_{-\sigma} \rangle = 1/2$，化学势 $\mu = U/2$，一阶矩为 $\epsilon_{\mathbf{k}}$。特别是在原子极限下 ($t=0$，$\epsilon_{\mathbf{k}}=0$)，移除一个电子的谱（下哈伯德带）的[平均能量](@entry_id:145892)为 $-U/2$ [@problem_id:1168707]。

更一般地，对于由某个算符 $\hat{A}$ 诱导的跃迁，其[振子强度求和规则](@entry_id:183363)通常与双对易子 $\langle k | [[\hat{A}, \hat{H}], \hat{A}] | k \rangle$ 的[期望值](@entry_id:153208)有关，这就是著名的**托马斯-赖歇-库恩 (Thomas-Reiche-Kuhn, TRK) 求和规则**的一般形式 [@problem_id:1201321]。

### 强关联系统中的求和规则

在强[关联电子系统](@entry_id:144460)中，由于强大的[库仑排斥](@entry_id:181876)，粒子不再是独立的。这种约束会改变底层的算符代数，从而修正求和规则。

一个典型的例子是 **t-J 模型**，它通过投影排除了双重占据的电子态来描述强关联系统。在这个受限的[希尔伯特空间](@entry_id:261193)中，电子算符 $c_{i\sigma}$ 被替换为投影算符 $\tilde{c}_{i\sigma} = c_{i\sigma}(1 - n_{i\bar{\sigma}})$。这导致了非正则的[对易关系](@entry_id:136780)：$\{\tilde{c}_{i\sigma}, \tilde{c}_{i\sigma}^\dagger\} = 1 - n_{i\bar{\sigma}}$。这个看似微小的改变对求和规则有深刻影响 [@problem_id:3020818]。对所有动量和[自旋求和](@entry_id:162099)，总积分[谱权重](@entry_id:144751)不再是 $2N$（$N$为格点数），而是：
$$
\sum_{\mathbf{k},\sigma} \int_{-\infty}^{\infty} d\omega \, A_{\mathbf{k}\sigma}(\omega) = \sum_{i,\sigma} \langle \{ \tilde{c}_{i\sigma}, \tilde{c}_{i\sigma}^\dagger \} \rangle = \sum_i \langle (1-n_{i\downarrow}) + (1-n_{i\uparrow}) \rangle = 2N - \langle N_e \rangle
$$
如果系统的平均电子密度为 $1-x$（$x$ 为空穴[掺杂浓度](@entry_id:272646)），则电子总数 $\langle N_e \rangle = N(1-x)$。因此，总[谱权重](@entry_id:144751)为 $2N - N(1-x) = N(1+x)$。相应地，移除电子（占据态）的总权重为 $\langle N_e \rangle = N(1-x)$，而添加电子（未占据态）的总权重为 $N(1+x) - N(1-x) = 2Nx$。

这些规则对于理解强关联现象，如**[谱权重转移](@entry_id:146476) (spectral weight transfer)**，至关重要。例如，在掺杂一个 Mott 绝缘体时，[谱权重](@entry_id:144751)会从高能量的哈伯德带转移到莫特[能隙](@entry_id:191975)内部，形成所谓的“[能隙](@entry_id:191975)内态”。利用求和规则可以精确地证明，这些新出现的[能隙](@entry_id:191975)内态的总[谱权重](@entry_id:144751)正比于[掺杂浓度](@entry_id:272646) $\delta$。在 $U \to \infty$ 的极限下，可以证明[能隙](@entry_id:191975)内态（来自向空格点添加电子）的总权重为 $2\delta$ [@problem_id:3006226]。

### [响应函数](@entry_id:142629)的求和规则

求和规则不仅适用于单粒子谱函数，也广泛应用于描述系统对外部微扰响应的**[线性响应函数](@entry_id:160418)** (linear response functions)，如电导率和[磁化率](@entry_id:138219)。这些求和规则同样源于因果律和基本对易关系。

#### [Kramers-Kronig 关系](@entry_id:140966)及其应用

任何因果[响应函数](@entry_id:142629) $\chi(\omega)$ 的[傅里叶变换](@entry_id:142120)在复频率上半平面都是解析的。这导致了其实部和虚部通过 Kramers-Kronig (KK) 关系相互关联。一个特别有用的 KK 关系是：
$$
\text{Re}[\chi(\omega=0)] = \frac{2}{\pi} \mathcal{P} \int_{0}^{\infty} d\omega' \frac{\text{Im}[\chi(\omega')]}{\omega'}
$$
这里 $\mathcal{P}$ 表示[柯西主值](@entry_id:192761)。这个关系意味着，一个系统的静态（零频率）响应可以通过对其动态（有限频率）响应的耗散部分（虚部）进行积分来确定。

例如，对于一个导电材料，其**逆[介电函数](@entry_id:136859)** $\epsilon^{-1}(\mathbf{q}, \omega)$ 在长波极限下 ($\mathbf{q} \to 0$) 必须满足**[完美屏蔽](@entry_id:146940) (perfect screening)** 条件，即 $\epsilon^{-1}(\mathbf{q}\to 0, \omega=0) = 0$。将此条件应用于 $\chi = \epsilon^{-1} - 1$ 的 KK 关系，可以导出一个重要的求和规则 [@problem_id:1201327]：
$$
\lim_{\mathbf{q}\to 0} \int_0^\infty \frac{d\omega}{\omega} \text{Im}[\epsilon^{-1}(\mathbf{q}, \omega)] = -\frac{\pi}{2}
$$
这被称为**[完美屏蔽](@entry_id:146940)求和规则**，它将[介电函数](@entry_id:136859)的动态行为与材料的基本[静电屏蔽](@entry_id:192260)能力联系起来。类似地，静态[磁化率](@entry_id:138219) $\chi(\mathbf{q}, 0)$ 也可以通过对[动态磁化率](@entry_id:139739)的虚部积分得到 [@problem_id:1201310]。

#### [f-求和规则](@entry_id:147775)及其[高阶矩](@entry_id:266936)

另一个著名的例子是**[光学电导率](@entry_id:139437)** $\sigma(\omega)$ 的求和规则。其耗散部分 $\text{Re}[\sigma(\omega)]$ 的积分与系统的载流子密度 $n$ 和质量 $m$ 直接相关：
$$
\int_0^\infty d\omega \, \text{Re}[\sigma(\omega)] = \frac{\pi n e^2}{2m}
$$
这被称为**[f-求和规则](@entry_id:147775)** (f-sum rule)，它是一个非微扰的精确结果。更高阶的频率矩也存在，并提供了关于谱形更精细的信息。例如，$\sigma(\omega)$ 的三阶矩与流算符时间导数的平方[期望值](@entry_id:153208)有关 [@problem_id:1201325]：
$$
\int_0^\infty d\omega \, \omega^3 \text{Re}[\sigma_{xx}(\omega)] = \frac{\pi}{2\hbar V} \langle \dot{J}_x^\dagger \dot{J}_x \rangle
$$
通过计算 $\dot{J}_x = \frac{i}{\hbar}[H, J_x]$，可以将这个积分与[哈密顿量](@entry_id:172864)的具体形式联系起来。

### 广阔的应用与现代背景

求和规则的概念远远超出了凝聚态物理的范畴，在[量子场论](@entry_id:138177)和现代物理前沿研究中也扮演着核心角色。

- **[规范场](@entry_id:159627)论**: 在量子色动力学 (QCD) 等[规范场](@entry_id:159627)论中，即使是描述非物理自由度（如时间规范中的纵向胶子）的[传播子](@entry_id:139558)，其谱函数也遵循由[正则对易关系](@entry_id:185041)导出的求和规则。然而，由于这些态不是物理渐进态，它们的谱密度不一定为正定，这揭示了规范理论的深刻结构 [@problem_id:323822]。在某些可解模型中，如 1+1 维的 **Schwinger 模型**，轴矢流反常可以表现为一个求和规则，其中流散度的谱函数完全由一个单一的、有质量的[玻色子](@entry_id:138266)态饱和 [@problem_id:1133960]。

- **非遍历系统**: 在**[多体局域化](@entry_id:147122) (MBL)** 等非遍历系统中，系统在长[时间演化](@entry_id:153943)后仍“记住”其初始状态。这种记忆体现在[可观测量](@entry_id:267133)的[时间平均](@entry_id:267915)值不为零。谱函数中的零频（弹性）峰的权重 $C_0$ 直接量化了这种时间不变的关联，并与描述非遍历性的[序参量](@entry_id:144819)（如无限时间不平衡量 $\mathcal{I}_\infty$）密切相关 [@problem_id:1201304]。

- **[近似理论](@entry_id:138536)的检验**: 在实践中，求和规则是检验近似理论和数值计算结果是否可靠的“试金石”。任何一个物理上合理的谱[函数近似](@entry_id:141329)形式，其低阶矩必须满足精确的求和规则。例如，如果我们将一个[准粒子](@entry_id:136584)峰近似为一个[洛伦兹函数](@entry_id:199503) $A^{\text{approx}}(\omega) = \frac{Z}{\pi} \frac{\Gamma}{(\omega-\Omega)^2 + \Gamma^2}$，那么零阶和一阶求和规则会立即固定其总权重 $Z$ 和峰位 $\Omega$ [@problem_id:2977718]。任何数值计算得到的谱函数，我们都可以通过计算其矩并与求和规则的精确值进行比较，来量化其“不一致性”，从而评估计算的准确性 [@problem_id:3016584]。

总之，谱函数是揭示多体系统单粒子激发本质的核心物理量，而求和规则则是从量子力学第一性原理出发的精确约束。它们共同构成了我们理解、描述和检验复杂量子系统行为的强大理论框架。