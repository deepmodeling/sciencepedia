## 引言
在量子多体物理的宏伟画卷中，“非对角长程序” (Off-diagonal Long-range Order, [ODLRO](@entry_id:159759)) 是理解物质如何从微观粒子的集合跃迁为展现宏观量子行为（如超流性与超导电性）的核心概念。它为我们提供了一种普适的语言，来描述系统中相隔遥远的粒子如何能“步调一致”，形成一个单一的、相干的[量子态](@entry_id:146142)。然而，从这一直观图像到其严谨的物理内涵，再到其在不同物理系统中的多样化表现，存在着巨大的知识深度。本文旨在系统性地填补这一鸿沟，为读者提供一个关于[ODLRO](@entry_id:159759)的全面而深入的理论图景。

为实现这一目标，我们将分三个章节展开论述。首先，在“**原理与机制**”一章中，我们将深入[ODLRO](@entry_id:159759)的理论核心，从其在[单体约化密度矩阵](@entry_id:160331)中的严格定义出发，阐明彭罗斯-翁萨格判据，并探讨热涨落、[量子涨落](@entry_id:154889)和无序等因素如何削弱甚至摧毁长程序。接着，在“**应用与跨学科连接**”一章中，我们将展示[ODLRO](@entry_id:159759)作为一个强大工具的广泛适用性，考察其在玻色-爱因斯坦凝聚、超导、[量子光学](@entry_id:140582)乃至高能物理等前沿领域中的具体体现和深刻影响。最后，通过“**动手实践**”部分提供的计算问题，读者将有机会亲手应用所学知识，将抽象的理论概念转化为具体的物理洞察。通过这一结构化的学习路径，读者将全面掌握[ODLRO](@entry_id:159759)的精髓，并理解其为何是现代量子物理不可或缺的基石。

## 原理与机制

本章旨在深入阐述非对角长程序（Off-diagonal Long-range Order, [ODLRO](@entry_id:159759)）的核心原理与物理机制。作为上一章“引言”的延续，我们将直接进入该概念的技术性定义，并系统地探讨其在不同量子系统中的表现形式、影响因素以及被破坏的机制。

### [单体约化密度矩阵](@entry_id:160331)与彭罗斯-翁萨格判据

在[多体量子系统](@entry_id:161678)中，描述[粒子统计](@entry_id:145640)[分布](@entry_id:182848)和[相干性](@entry_id:268953)的最基本工具之一是**[单体约化密度矩阵](@entry_id:160331) (one-body reduced density matrix, [1-RDM](@entry_id:183172))**。对于一个包含 $N$ 个[全同粒子](@entry_id:142755)的归一化多体态 $|\Psi\rangle$，其 [1-RDM](@entry_id:183172) 定义为：
$$
\rho_1(\mathbf{r}, \mathbf{r}') = \langle\Psi| \hat{\Psi}^\dagger(\mathbf{r}') \hat{\Psi}(\mathbf{r}) |\Psi\rangle
$$
其中 $\hat{\Psi}(\mathbf{r})$ 和 $\hat{\Psi}^\dagger(\mathbf{r}')$ 分别是在位置 $\mathbf{r}$ 湮灭一个粒子和在位置 $\mathbf{r}'$ 产生一个粒子的[场算符](@entry_id:140269)。因此，$\rho_1(\mathbf{r}, \mathbf{r}')$ 的物理意义可以理解为：在系统中于 $\mathbf{r}$ 处移除一个粒子，并于 $\mathbf{r}'$ 处重新置入一个粒子后，系统回到初始状态的量子力学几率幅。对角元 $\rho_1(\mathbf{r}, \mathbf{r}) = \langle\Psi| \hat{\Psi}^\dagger(\mathbf{r}) \hat{\Psi}(\mathbf{r}) |\Psi\rangle$ 就是在位置 $\mathbf{r}$ 的粒子数密度 $n(\mathbf{r})$。

[1-RDM](@entry_id:183172) 是一个[厄米算符](@entry_id:153410)，其[本征值](@entry_id:154894) $\{\lambda_k\}$ 均非负，代表了其对应[本征函数](@entry_id:154705)——即**自然[轨道](@entry_id:137151) (natural orbitals)** $\phi_k(\mathbf{r})$ ——上的平均粒子占据数。所有[本征值](@entry_id:154894)之和等于系统中的总粒子数，即 $\sum_k \lambda_k = N$。

1956年，Oliver Penrose 和 Lars Onsager 提出了一个判定[玻色-爱因斯坦凝聚](@entry_id:144849) (Bose-Einstein Condensation, BEC) 是否存在的普适性判据，该判据不依赖于系统是否存在相互作用。**彭罗斯-翁萨格判据**指出，如果 [1-RDM](@entry_id:183172) 的某个[本征值](@entry_id:154894) $\lambda_0$ 是宏观量级的，即与总粒子数 $N$ 成正比（$\lambda_0 \sim O(N)$），而所有其他[本征值](@entry_id:154894) $\lambda_{k\neq0}$ 都是 $O(1)$ 的小量，那么系统就存在[玻色-爱因斯坦凝聚](@entry_id:144849)。这个宏观占据的[本征值](@entry_id:154894) $\lambda_0$ 就被认为是凝聚体中的粒子数。这种单个[量子态](@entry_id:146142)被宏观数量粒子占据的现象，正是非对角长程序的标志。

为了深刻理解量子统计性在 [ODLRO](@entry_id:159759) 中的决定性作用，我们可以对比两个理想化的系统 [@problem_id:1256256]。考虑一个体积为 $V=L^3$ 的三维立方盒子，其中包含 $N$ 个粒子。

1.  **系统A：无相互作用[玻色子](@entry_id:138266)气体[基态](@entry_id:150928)。** 根据[玻色-爱因斯坦统计](@entry_id:139965)，所有 $N$ 个[玻色子](@entry_id:138266)在[基态](@entry_id:150928)时都会占据能量最低的单粒子态，即动量为零的[平面波](@entry_id:189798)[轨道](@entry_id:137151) $\phi_0(\mathbf{r}) = 1/\sqrt{V}$。此时，[1-RDM](@entry_id:183172) 为 $\rho_1^{(A)}(\mathbf{r}, \mathbf{r}') = N \phi_0(\mathbf{r}) \phi_0^*(\mathbf{r}') = N/V$。这个 [1-RDM](@entry_id:183172) 只有一个非零[本征值](@entry_id:154894)，其对应的自然[轨道](@entry_id:137151)就是 $\phi_0(\mathbf{r})$，该[本征值](@entry_id:154894) $\lambda_{\text{max}}^{(A)} = N$。

2.  **系统B：无相互作用的自旋极化[费米子](@entry_id:146235)气体[基态](@entry_id:150928)。** 根据[泡利不相容原理](@entry_id:141850)，每个单粒子[量子态](@entry_id:146142)最多只能容纳一个[费米子](@entry_id:146235)。因此，[基态](@entry_id:150928)是通过从最低能量开始，依次填充[动量空间](@entry_id:148936)中的各个平面波态，直至[费米面](@entry_id:137798) $|k| \le k_F$ 为止。这意味着所有被占据的自然[轨道](@entry_id:137151)（即这些平面波态）的占据数都恰好为 1。因此，[1-RDM](@entry_id:183172) 的最大[本征值](@entry_id:154894) $\lambda_{\text{max}}^{(B)} = 1$。

这两个系统的最大[本征值](@entry_id:154894)之比为 $\lambda_{\text{max}}^{(A)} / \lambda_{\text{max}}^{(B)} = N$。这个巨大的差异清晰地表明，只有[玻色子](@entry_id:138266)系统才能满足彭罗斯-翁萨格判据，形成凝聚。[费米子](@entry_id:146235)系统由于[泡利不相容原理](@entry_id:141850)的限制，其任何一个自然[轨道](@entry_id:137151)的占据数都不可能成为宏观量。

这个判据同样适用于具有内禀自由度的系统。例如，在一个自旋为1的BEC中，如果系统处于极化态（polar state），其[宏观波函数](@entry_id:143853)可以写为 $\mathbf{\Psi}(\mathbf{r}) = \sqrt{n_0(\mathbf{r})} \hat{\zeta}_{polar}$，其中 $\hat{\zeta}_{polar} = (0, 1, 0)^T$ 是一个描述所有粒子都处于 $m_s=0$ [自旋态](@entry_id:149436)的[旋量](@entry_id:158054)。通过求解其 [1-RDM](@entry_id:183172) 的本征方程，可以发现其最大的（也是唯一的）[本征值](@entry_id:154894)为凝聚体中的总粒子数 $N_0 = \int d^3\mathbf{r} \, n_0(\mathbf{r})$ [@problem_id:1256168]。这表明 [ODLRO](@entry_id:159759) 的概念可以自然地推广到包含自旋等内禀自由度的复杂凝聚体中。

### [ODLRO](@entry_id:159759)、关联函数与凝聚体分数

[1-RDM](@entry_id:183172) 的宏观[本征值](@entry_id:154894)与其[矩阵元](@entry_id:186505)在长程行为上的表现密切相关。如果 $\rho_1$ 有一个宏观[本征值](@entry_id:154894) $\lambda_0$，对应的自然[轨道](@entry_id:137151)为 $\phi_0(\mathbf{r})$，那么 [1-RDM](@entry_id:183172) 可以写作：
$$
\rho_1(\mathbf{r}, \mathbf{r}') = \lambda_0 \phi_0(\mathbf{r}) \phi_0^*(\mathbf{r}') + \sum_{k \neq 0} \lambda_k \phi_k(\mathbf{r}) \phi_k^*(\mathbf{r}')
$$
其中第二项是所有非凝聚模式的贡献。通常情况下，这些模式之间的相干性是短程的，因此当两点间距 $|\mathbf{r}-\mathbf{r}'|$ 趋于无穷大时，第二项的贡献会趋于零。于是，我们得到了 [ODLRO](@entry_id:159759) 的等价定义，即 [1-RDM](@entry_id:183172) 在大间距下的渐进行为：
$$
\lim_{|\mathbf{r}-\mathbf{r}'| \to \infty} \rho_1(\mathbf{r}, \mathbf{r}') = \lambda_0 \phi_0(\mathbf{r}) \phi_0^*(\mathbf{r}')
$$
在均匀系统中，$\phi_0(\mathbf{r})$ 是一个常数，因此 $\rho_1$ 趋于一个非零常数 $n_0$，这个 $n_0$ 就是**凝聚体密度**。这个非零的渐近值意味着，即使在宏观尺度上分离的两个点，移除和置入一个粒子的过程仍然保持着固定的相位关系，这正是“[长程序](@entry_id:155156)”的体现。

在处理有相互作用的系统时，精确定义“凝聚体中的粒子数”需要更加谨慎。存在两种常用的定义 [@problem_id:1256189]：
1.  **基于 [ODLRO](@entry_id:159759) 的定义 ($N_0^{(\rho)}$)**：根据长程关联，凝聚体粒子数定义为 $N_0^{(\rho)} = V \lim_{|\mathbf{r}-\mathbf{r}'|\to\infty} \rho_1(\mathbf{r}, \mathbf{r}')$。在[U(1)对称性](@entry_id:154785)破缺的图像下，[场算符](@entry_id:140269)具有非零的[期望值](@entry_id:153208) $\langle \hat{\Psi}(\mathbf{r}) \rangle = \sqrt{N_c/V}$，其中 $N_c$ 是相干部分的粒子数。由于涨落关联 $\langle \delta\hat{\Psi}^\dagger(\mathbf{r}) \delta\hat{\Psi}(\mathbf{r}') \rangle$ 是短程的，长程极限下的 $\rho_1$ 就由[场算符](@entry_id:140269)的[期望值](@entry_id:153208)乘积给出，即 $\lim \rho_1 = |\langle \hat{\Psi} \rangle|^2 = N_c/V$。因此，$N_0^{(\rho)} = N_c$。
2.  **基于动量分布的定义 ($N_0^{(n)}$)**：凝聚体粒子数被定义为占据零动量单粒子态的总粒子数，即 $N_0^{(n)} = \langle \hat{a}_0^\dagger \hat{a}_0 \rangle$，其中 $\hat{a}_0$ 是零动量模式的[湮灭算符](@entry_id:165390)。

这两个定义在无相互作用的理想 BEC 中是等价的。但在相互作用系统中，粒子间的碰撞会将一部分粒子“踢”出相干的凝聚体，但这些粒子仍可能占据零动量态。将[场算符](@entry_id:140269)分解为平均场和涨落部分 $\hat{\Psi} = \langle \hat{\Psi} \rangle + \delta\hat{\Psi}$，零[动量算符](@entry_id:151743)也相应分解为 $\hat{a}_0 = \langle \hat{a}_0 \rangle + \delta\hat{a}_0$。于是，$N_0^{(n)} = \langle \hat{a}_0^\dagger \hat{a}_0 \rangle = |\langle \hat{a}_0 \rangle|^2 + \langle \delta\hat{a}_0^\dagger \delta\hat{a}_0 \rangle = N_c + N_{dep,0}$，其中 $N_{dep,0}$ 是因相互作用而“损耗”但仍占据零动量模式的粒子数。因此，这两个定义的比值为 $\mathcal{R} = N_0^{(\rho)} / N_0^{(n)} = N_c / (N_c + N_{dep,0})$。这个结果表明，Penrose-Onsager 判据所定义的凝聚体分数仅包含相干部分，而[动量分布](@entry_id:162113)法则包含了所有零动量粒子。

[ODLRO](@entry_id:159759) 的存在也深刻地影响了高阶关联函数。对于一个具有 [ODLRO](@entry_id:159759) 的系统，其高阶[约化密度矩阵](@entry_id:146315)在长程极限下会因子化为低阶密度矩阵的乘积。以纯 BEC 为例 [@problem_id:1256273]，其二体[约化密度矩阵](@entry_id:146315) $\rho_2(\mathbf{r}_1, \mathbf{r}_2; \mathbf{r}'_1, \mathbf{r}'_2) = \langle \hat{\Psi}^\dagger(\mathbf{r}'_1) \hat{\Psi}^\dagger(\mathbf{r}'_2) \hat{\Psi}(\mathbf{r}_2) \hat{\Psi}(\mathbf{r}_1) \rangle$ 与两个[单体密度矩阵](@entry_id:161726)乘积的比值在[热力学极限](@entry_id:143061)下趋于1。对于有限粒子数 $N$ 的系统，这个比值为 $(N-1)/N$。这意味着在宏观尺度上，粒子间的关联消失，它们的行为变得独立，这正是凝聚体经典场描述的基石。

### 凝聚体的碎裂

彭罗斯-翁萨格判据所描述的简单 BEC，即只有一个自然[轨道](@entry_id:137151)被宏观占据，并非凝聚的唯一形式。在某些情况下，系统可能出现**凝聚体碎裂 (fragmented condensate)** 的现象，即 [1-RDM](@entry_id:183172) 有多个宏观量级的[本征值](@entry_id:154894)。

考虑一个包含 $N$ 个[玻色子](@entry_id:138266)（$N$为奇数）的系统，它们可以占据两个正交的单粒子模式 $\phi_1$ 和 $\phi_2$。如果系统的状态是这两个模式宏观占据数的叠加态，例如：
$$
|\Psi\rangle = \frac{1}{\sqrt{2}} \left( \left|\frac{N+1}{2}, \frac{N-1}{2}\right\rangle + \left|\frac{N-1}{2}, \frac{N+1}{2}\right\rangle \right)
$$
在这种状态下，没有一个单一模式被所有粒子占据。通过计算 [1-RDM](@entry_id:183172) 在 $\{\phi_1, \phi_2\}$ [基矢](@entry_id:199546)下的矩阵表示 $(\rho_1)_{ij} = \langle \Psi | a_i^\dagger a_j | \Psi \rangle$，可以发现其对角元（即每个模式的平均占据数）均为 $N/2$，而非对角元（模式间的相干项）为 $(N+1)/4$ [@problem_id:1256166]。求解该 $2 \times 2$ 矩阵的[本征值](@entry_id:154894)，我们得到两个宏观量级的[本征值](@entry_id:154894)：
$$
\lambda_{\pm} = \frac{N}{2} \pm \frac{N+1}{4}
$$
最大的[本征值](@entry_id:154894)为 $\lambda_{\text{max}} = (3N+1)/4$。另一个[本征值](@entry_id:154894) $\lambda_{-} = (N-1)/4$ 同样是 $O(N)$ 的。这表明系统虽然是凝聚的（存在宏观占据的自然[轨道](@entry_id:137151)），但它碎裂成了两个部分，凝聚没有发生在单一的[量子态](@entry_id:146142)上。这种情况在多组分 BEC 或受限几何中的系统中可能出现。

### [ODLRO](@entry_id:159759) 的破坏：[热涨落](@entry_id:143642)与[量子涨落](@entry_id:154889)

完美的 [ODLRO](@entry_id:159759) 是一种理想化的零温、三维系统的[基态](@entry_id:150928)特性。在更现实的条件下，热涨落和[量子涨落](@entry_id:154889)会削弱甚至完全破坏[长程序](@entry_id:155156)。

#### [热涨落](@entry_id:143642)与[准粒子激发](@entry_id:138475)
在有限温度 $T>0$ 时，热能会激发系统中的[元激发](@entry_id:140859)（或称[准粒子](@entry_id:136584)），这些[准粒子](@entry_id:136584)占据了原本属于凝聚体的粒子数，导致**热损耗 (thermal depletion)**。在[弱相互作用](@entry_id:157579)的三维[玻色气体](@entry_id:155364)中，这些低能[元激发](@entry_id:140859)是[声子模式](@entry_id:201212)的玻戈留波夫[准粒子](@entry_id:136584) [@problem_id:1256224]。在低温极限下 ($k_B T \ll \mu$，其中 $\mu \approx gn$ 是化学势，$g$ 是相互作用强度，$n$ 是粒子密度)，体系中由[热涨落](@entry_id:143642)激发的[准粒子](@entry_id:136584)（非凝聚原子）密度 $n_{th}$ 主要来自长波长的[声子模式](@entry_id:201212)。通过对所有动量模式的热占据数进行积分，可以得到其正比于温度的三次方：
$$
n_{th} = \frac{\zeta(3)}{2\pi^2} \left(\frac{k_B T}{\hbar c_s}\right)^3
$$
其中 $\zeta(3) \approx 1.202$ 是[黎曼zeta函数](@entry_id:161915)的值，$m$ 是[粒子质量](@entry_id:156313)，$c_s = \sqrt{gn/m}$ 是声速。热损耗的存在意味着凝聚体分数随温度升高而减小，[ODLRO](@entry_id:159759) 被削弱。当温度升高到[临界温度](@entry_id:146683) $T_c$ 时，凝聚体完全消失，[ODLRO](@entry_id:159759) 随之不复存在。

#### 低维度系统中的[准长程序](@entry_id:145141)
在低维度（一维和二维）系统中，涨落的影响变得更为剧烈，甚至可以在根本上改变[长程序](@entry_id:155156)的性质。

根据**[Mermin-Wagner定理](@entry_id:142609)**，在二维系统中，[连续对称性](@entry_id:137257)无法在有限温度下自发破缺。这意味着二维[玻色子](@entry_id:138266)系统在任何 $T>0$ 的情况下都不存在真正的 [ODLRO](@entry_id:159759)。然而，在低于 Berezinskii-Kosterlitz-Thouless (BKT) [相变](@entry_id:147324)温度时，系统会进入一种被称为**[准长程序](@entry_id:145141) (quasi-long-range order)** 的特殊状态。在这种状态下，关联函数不再像三维系统中那样趋于一个常数，而是随着距离 $r$ 的增加，以代数形式（[幂律](@entry_id:143404)）缓慢衰减：
$$
\rho_1(r) \sim r^{-\eta(T)}
$$
这个[幂律衰减](@entry_id:262227)的根源在于长波长的相位涨落。将玻色[场算符](@entry_id:140269)近似为 $\hat{\psi}(\mathbf{r}) \approx \sqrt{\rho_0} e^{i\hat{\theta}(\mathbf{r})}$，[1-RDM](@entry_id:183172) 的行为由相位关联函数 $\langle (\hat{\theta}(\mathbf{r}) - \hat{\theta}(0))^2 \rangle$ 决定。在二维有限温度下，该关联函数随距离对数增长，$\langle (\Delta\theta)^2 \rangle \propto \ln(r)$，这直接导致了 $\rho_1(r)$ 的[幂律衰减](@entry_id:262227) [@problem_id:1256182]。衰减指数 $\eta(T)$ 与温度和系统的[超流密度](@entry_id:142018) $\rho_s$ 直接相关：
$$
\eta(T) = \frac{m k_B T}{2\pi \hbar^2 \rho_s}
$$
这种代数衰减的关联意味着系统仍然具有高度的[相干性](@entry_id:268953)，足以支持超流，但并非严格意义上的长程序。

在一维系统中，量子涨落的作用甚至更为强大，以至于在**零温下**就足以摧毁真正的 [ODLRO](@entry_id:159759)。一维相互作用[玻色子](@entry_id:138266)系统的低能物理普适地由**[朝永-拉廷格液体](@entry_id:139351) (Tomonaga-Luttinger liquid, TLL)** 理论描述。与二维情况类似，其 [1-RDM](@entry_id:183172) 也表现为[幂律衰减](@entry_id:262227) [@problem_id:1256223]。通过[玻色化](@entry_id:139728)方法，可以计算出相[位场](@entry_id:143025)的[量子关联函数](@entry_id:143185)，并由此得到 [1-RDM](@entry_id:183172) 的衰减指数 $\eta$：
$$
\rho_1(r) \sim r^{-\eta}, \quad \eta = \frac{1}{2K}
$$
这里的 $K$ 是无量纲的**拉廷格参数**，它衡量了相互作用的强度（$K \to \infty$ 对应无相互作用[玻色子](@entry_id:138266)，$K=1$ 对应强排斥的 Tonks-Girardeau 气体）。这个结果表明，只要存在相互作用（$K \neq \infty$），[一维玻色子](@entry_id:136376)系统在零温下也只有[准长程序](@entry_id:145141)。

### [费米子](@entry_id:146235)超流与对关联
单个[费米子](@entry_id:146235)无法形成凝聚，但它们可以通过吸引相互作用配对形成“[库珀对](@entry_id:143370)”，这些[复合玻色子](@entry_id:160765)可以经历[玻色-爱因斯坦凝聚](@entry_id:144849)，从而形成超流或超导。在这种情况下，[ODLRO](@entry_id:159759) 体现在**对关联函数 (pair correlation function)** 中，而非单粒子关联函数。

对于一个由自旋向上 ($\uparrow$) 和向下 ($\downarrow$) 的[费米子](@entry_id:146235)组成的 BCS 超流体，其序参量是**反常对关联函数** $F(\mathbf{r}_1, \mathbf{r}_2) = \langle \psi_\uparrow(\mathbf{r}_1) \psi_\downarrow(\mathbf{r}_2) \rangle$。在[对称性破缺](@entry_id:158994)的平均场理论中，人们通常赋予这个量一个非零的[期望值](@entry_id:153208) $\Delta/g$，其中 $\Delta$ 是[能隙](@entry_id:191975)。然而，需要注意的是，在严格的粒子数守恒理论中，任何湮灭（或产生）奇数个[费米子](@entry_id:146235)的算符的[期望值](@entry_id:153208)都为零。因此，$\langle \psi_\uparrow(\mathbf{r}) \psi_\downarrow(\mathbf{r}') \rangle$ 这一关联函数，作为[动量空间](@entry_id:148936)中[BCS相干因子](@entry_id:142994)乘积 $u_k v_k$ 的[傅里叶变换](@entry_id:142120)，根据[黎曼-勒贝格引理](@entry_id:140988)，在 $|\mathbf{r}-\mathbf{r}'| \to \infty$ 时必然趋于零 [@problem_id:1256271]。

真正的 [ODLRO](@entry_id:159759) 体现在四点关联函数，即二体[约化密度矩阵](@entry_id:146315)的特定部分：
$$
G_2(\mathbf{r}_1, \mathbf{r}_2; \mathbf{r}'_1, \mathbf{r}'_2) = \langle \psi_\uparrow^\dagger(\mathbf{r}'_1) \psi_\downarrow^\dagger(\mathbf{r}'_2) \psi_\downarrow(\mathbf{r}_2) \psi_\uparrow(\mathbf{r}_1) \rangle
$$
在长程极限下，它因子化为对[波函数](@entry_id:147440)的乘积：$G_2 \to F^*(\mathbf{r}'_1, \mathbf{r}'_2) F(\mathbf{r}_1, \mathbf{r}_2)$。这表示一个在 $(\mathbf{r}_1, \mathbf{r}_2)$ 处湮灭的[库珀对](@entry_id:143370)和一个在遥远的 $(\mathbf{r}'_1, \mathbf{r}'_2)$ 处产生的[库珀对](@entry_id:143370)之间存在着固定的相位关系，这正是[费米子](@entry_id:146235)超流中的 [ODLRO](@entry_id:159759)。

对关联的[准长程序](@entry_id:145141)也可以在其他系统中出现。例如，在一维吸引相互作用的[玻色子](@entry_id:138266)气体中，粒子倾向于形成[紧束缚](@entry_id:142573)的分子对。这些分子对本身可以被看作是硬核[玻色子](@entry_id:138266)，形成一个具有[准长程序](@entry_id:145141)的 Tonks-Girardeau 气体。因此，原始[玻色子](@entry_id:138266)系统的局域对关联函数 $\mathcal{G}_p(x) = \langle \hat{\psi}^\dagger(x)\hat{\psi}^\dagger(x) \hat{\psi}(0)\hat{\psi}(0) \rangle$ 会展现出与分子对的 [1-RDM](@entry_id:183172) 相同的[幂律衰减](@entry_id:262227)行为 [@problem_id:1256137]，表现为一种对的准 [ODLRO](@entry_id:159759)。

### 无序的作用：玻色玻璃相

除了热涨落和量子涨落，静态的**无序 (disorder)**，如[随机势](@entry_id:144028)场，也能够有效地破坏 [ODLRO](@entry_id:159759)。与驱动系统趋向均匀的涨落不同，无序势场倾向于将粒子“钉扎”在[势能](@entry_id:748988)的低洼处，从而破坏相位的长程[相干性](@entry_id:268953)。

在一维相互作用[玻色子](@entry_id:138266)系统中，弱无序的存在会使系统从超流的拉廷格液体相转变为一个被称为**玻色玻璃 (Bose glass)** 的新物相。这是一个零温下的可压缩、无超流性的绝缘相。在玻色玻璃相中，[长程序](@entry_id:155156)被完全破坏，单粒子关联函数呈指数衰减：
$$
\rho_1(r) \sim \exp(-r/L_\phi)
$$
这里的 $L_\phi$ 被称为**拉金长度 (Larkin length)**，它表征了相位关联丢失的[特征长度尺度](@entry_id:266383)。其物理意义是，无序势导致的相位随机起伏在拉金长度的距离上累积到大约为 1 的程度，从而彻底破坏了[相位相干性](@entry_id:142586)。通过最小化系统的总能量（包含无序势的耦合），可以推导出拉金长度与无序强度 $D$、声速 $v_s$ 和拉廷格参数 $K$ 的关系 [@problem_id:1256202]：
$$
L_\phi = \frac{\hbar^2 v_s^2}{D K^2}
$$
这个结果表明，无序越强（$D$ 越大）或系统越“软”（$K$ 越大，即排斥越弱），相位就越容易被钉扎，相干长度 $L_\phi$ 就越短。玻色玻璃相的存在，展示了无序作为一种与涨落截然不同的机制，如何从根本上摧毁 [ODLRO](@entry_id:159759)，导致局域化和超流性的丧失。