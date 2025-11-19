## 引言
在多体量子物理中，[格林函数](@entry_id:147802)是连接微观理论与[宏观可观测量](@entry_id:751601)的核心工具，但对于复杂的相互作用系统，其计算极具挑战性。[格林函数](@entry_id:147802)的运动方程（Equation-of-motion, EOM）方法为此提供了一条强大而灵活的途径，它将复杂的动力学问题巧妙地转化为一个代数方程体系，从而系统性地揭示系统的[元激发](@entry_id:140859)谱。本文旨在全面解析这一关键方法。

我们将分三个层次展开讨论。首先，在“原理与机制”一章中，我们将建立[运动方程](@entry_id:170720)的基本框架，探讨其如何精确求解简单模型，以及如何通过[解耦近似](@entry_id:144820)（如Hubbard-I近似）处理强关联系统。其次，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将探索该方法在凝聚态物理、[量子输运](@entry_id:138932)和[量子化学](@entry_id:140193)等领域的广泛应用，展示其解决实际物理问题的强大能力。最后，“动手实践”部分将通过具体问题引导读者巩固所学。通过本文的学习，读者将掌握[运动方程法](@entry_id:147861)的精髓，并理解其在现代科学研究中的重要作用。

## 原理与机制

在上一章中，我们介绍了[格林函数](@entry_id:147802)作为研究多体系统[量子动力学](@entry_id:138183)和谱性质的强大工具。本章将深入探讨计算[格林函数](@entry_id:147802)的一种核心方法——[运动方程法](@entry_id:147861)（Equation-of-motion, EOM）。该方法通过分析算符在[海森堡绘景](@entry_id:141162)下的时间演化，建立起一系列关于[格林函数](@entry_id:147802)的代数方程，从而为求解系统的激发谱和响应函数提供了一条系统性的途径。我们将从该方法的基本原理出发，通过一系列从简至繁的物理模型，阐明其在不同情况下的应用机制，包括精确求解、近似处理以及与[戴森方程](@entry_id:146246)和[自能](@entry_id:145608)等核心概念的联系。

### [运动方程法](@entry_id:147861)的基本框架

让我们从[推迟格林函数](@entry_id:139183)的定义开始。对于两个算符 $A$ 和 $B$，其[推迟格林函数](@entry_id:139183)在时间域和频率域中的定义分别为：
$$
G_{AB}^R(t-t') = -i\Theta(t-t') \langle [A(t), B(t')]_{\eta} \rangle
$$
$$
G_{AB}^R(\omega) = \langle\langle A; B \rangle\rangle_\omega = \int_{-\infty}^{\infty} G_{AB}^R(t) e^{i\omega t} dt
$$
其中，$\Theta(t-t')$ 是赫维赛德阶跃函数，保证了因果性。$\langle \dots \rangle$ 表示在系统[基态](@entry_id:150928)或[热力学](@entry_id:141121)系综上的平均。$[A, B]_{\eta} = AB - \eta BA$ 是（反）对易子，对于[玻色子](@entry_id:138266)（或类[玻色子](@entry_id:138266)算符）$\eta = 1$，对于[费米子](@entry_id:146235)（或类[费米子算符](@entry_id:149120)）$\eta = -1$。[格林函数](@entry_id:147802)的物理意义在于其谱函数 $A_{AB}(\omega)$，它描述了系统的[元激发](@entry_id:140859)。谱函数与[推迟格林函数](@entry_id:139183)的虚部直接相关 [@problem_id:2983430] [@problem_id:809524]：
$$
A_{AB}(\omega) = -\frac{1}{\pi} \text{Im} G_{AB}^R(\omega)
$$
[谱函数](@entry_id:147628)的峰位对应于[元激发](@entry_id:140859)的能量，峰高则与其[谱权重](@entry_id:144751)（或强度）相关。

[运动方程法](@entry_id:147861)的出发点是海森堡方程 $i\hbar \frac{d A(t)}{dt} = [A(t), H]$。通过对 $G_{AB}^R(t-t')$ 对时间 $t$ 求导，并进行[傅里叶变换](@entry_id:142120)，我们可以得到其在频率域中的**[运动方程](@entry_id:170720)**（EOM）：
$$
\hbar\omega \langle\langle A; B \rangle\rangle_\omega = \langle [A, B]_\eta \rangle + \langle\langle [A, H]; B \rangle\rangle_\omega
$$
这个方程是我们后续所有分析的基石。方程的左边是[格林函数](@entry_id:147802)乘以能量 $\hbar\omega$。右边第一项是一个不含时间的（等时）对易或[反对易关系](@entry_id:153815)的系综平均，通常是一个常数，称为**非齐次项**。第二项则是一个新的、更高阶的格林函数，其形式为 $\langle\langle [A, H]; B \rangle\rangle_\omega$。

这里的核心挑战在于，对易子 $[A, H]$ 通常会产生比 $A$ 更复杂的算符。例如，如果 $A$ 是一个单粒子算符，而[哈密顿量](@entry_id:172864) $H$ 包含[相互作用项](@entry_id:637283)（如四[费米子](@entry_id:146235)项），那么 $[A, H]$ 将会包含三粒子算符。对这个新的三粒子[格林函数](@entry_id:147802)再次使用[运动方程](@entry_id:170720)，又会产生五粒子格林函数，如此循环往复，形成一个无限的**方程层级**（hierarchy of equations）。[运动方程法](@entry_id:147861)的精髓就在于如何根据具体的物理问题和所关心的[能量尺度](@entry_id:196201)，对这个方程层级进行合理的**截断**（truncation）或**解耦**（decoupling），从而得到一个封闭的代数方程组，进而求解出格林函数。

### [精确可解模型](@entry_id:142243)：二次型[哈密顿量](@entry_id:172864)

最简单的情况是当系统的[哈密顿量](@entry_id:172864)是算符的二次型时。在这种情况下，算符与[哈密顿量](@entry_id:172864)的对易子 $[A, H]$ 将是原始算符的线性组合。这意味着方程层级在第一步之后便自动封闭，我们可以得到一个有限维的[线性方程组](@entry_id:148943)，从而精确地求解格林函数。

#### 杂化能带系统

一个典型的例子是描述两个不同自由度（如[光子](@entry_id:145192)和激子，或[传导电子](@entry_id:145260)和局域f电子）之间线性耦合的模型。考虑一个由腔[光子](@entry_id:145192)（算符 $a$）和量子阱[激子](@entry_id:147299)（算符 $b$）构成的[激子](@entry_id:147299)-极化激元系统，其[哈密顿量](@entry_id:172864)为 [@problem_id:1132455]：
$$
H = \hbar\omega_c a^\dagger a + \hbar\omega_x b^\dagger b + \hbar g (a^\dagger b + b^\dagger a)
$$
这里 $\omega_c$ 和 $\omega_x$ 分别是[光子](@entry_id:145192)和[激子](@entry_id:147299)的频率， $g$ 是[耦合强度](@entry_id:275517)。我们想要求解[光子](@entry_id:145192)格林函数 $G_{aa}(\omega) = \langle\langle a; a^\dagger \rangle\rangle_\omega$。

根据[运动方程](@entry_id:170720)，我们有：
$$
\hbar\omega G_{aa}(\omega) = \langle [a, a^\dagger] \rangle + \langle\langle [a, H]; a^\dagger \rangle\rangle_\omega
$$
计算对易子 $[a, a^\dagger] = 1$ 和 $[a, H] = \hbar\omega_c a + \hbar g b$，代入后得到第一个方程：
$$
(\omega - \omega_c) G_{aa}(\omega) = \frac{1}{\hbar} + g G_{ba}(\omega)
$$
其中 $G_{ba}(\omega) = \langle\langle b; a^\dagger \rangle\rangle_\omega$ 是一个新的“杂化”格林函数。我们继续为 $G_{ba}(\omega)$ 写出运动方程：
$$
\hbar\omega G_{ba}(\omega) = \langle [b, a^\dagger] \rangle + \langle\langle [b, H]; a^\dagger \rangle\rangle_\omega
$$
计算对易子 $[b, a^\dagger] = 0$ 和 $[b, H] = \hbar\omega_x b + \hbar g a$，代入后得到第二个方程：
$$
(\omega - \omega_x) G_{ba}(\omega) = g G_{aa}(\omega)
$$
现在我们得到了一个关于 $G_{aa}(\omega)$ 和 $G_{ba}(\omega)$ 的封闭[线性方程组](@entry_id:148943)。求解这个[方程组](@entry_id:193238)，可得：
$$
G_{aa}(\omega) = \frac{\omega - \omega_x}{\hbar[(\omega - \omega_c)(\omega - \omega_x) - g^2]}
$$
格林[函数的极点](@entry_id:189069)给出了体系的[元激发](@entry_id:140859)能量，即极化激元的色散关系。这些能量是分母为零的解：
$$
(\omega - \omega_c)(\omega - \omega_x) - g^2 = 0
$$
解得两个[极化激元](@entry_id:142951)分支的能量为 $\omega_{\pm} = \frac{\omega_c + \omega_x}{2} \pm \frac{1}{2}\sqrt{(\omega_c - \omega_x)^2 + 4g^2}$。在[共振条件](@entry_id:754285)（零失谐）$\omega_c = \omega_x$ 下，能级劈裂为 $\omega_{\pm} = \omega_c \pm g$，能量差 $\Delta E = 2\hbar g$ 被称为**拉比劈裂**（Rabi splitting）。这种由于模式杂化导致的能级劈裂是这类耦合系统的普遍特征。

完全相同的数学结构也出现在其他重要的物理模型中，例如描述[重费米子材料](@entry_id:146546)的**周期[安德森模型](@entry_id:140681)**（Periodic Anderson Model）[@problem_id:1132393] 和描述原子与单模光场相互作用的**[杰恩斯-卡明斯模型](@entry_id:142868)**（Jaynes-Cummings Model）[@problem_id:1132429]，展示了[运动方程法](@entry_id:147861)在处理杂化问题上的普适性。

#### 超导与[南部-戈尔科夫格林函数](@entry_id:145547)

另一个重要的精确可解范例是BCS平均场理论下的[超导体](@entry_id:191025)。[超导体](@entry_id:191025)的特殊之处在于其[基态](@entry_id:150928)是电子对的[相干叠加](@entry_id:170209)，这意味着诸如 $\langle c_{\mathbf{k}\uparrow} c_{-\mathbf{k}\downarrow} \rangle$ 这样的“反常”期待值不为零。为了处理这种情况，我们必须将电子的产生和湮灭算符放在同等地位上。这自然地引出了**南部-戈尔科夫（Nambu-Gorkov）形式**。

我们定义一个四分量的[南部旋量](@entry_id:145326) $\Psi_{\mathbf{k}}^\dagger = (c_{\mathbf{k}\uparrow}^\dagger, c_{\mathbf{k}\downarrow}^\dagger, c_{-\mathbf{k}\uparrow}, c_{-\mathbf{k}\downarrow})$，并构建一个 $4\times4$ 的矩阵格林函数 $\hat{G}(\mathbf{k}, \omega) = \langle\langle \Psi_{\mathbf{k}}; \Psi_{\mathbf{k}}^\dagger \rangle\rangle_\omega$。其运动方程可以紧凑地写为：
$$
(\omega\mathbf{1} - \mathcal{H}_{\text{BdG}}(\mathbf{k})) \hat{G}(\mathbf{k}, \omega) = \mathbf{1}
$$
其中 $\mathcal{H}_{\text{BdG}}(\mathbf{k})$ 是**博戈留波夫-德热纳（Bogoliubov-de Gennes, BdG）[哈密顿量](@entry_id:172864)矩阵**。因此，体系的[准粒子激发](@entry_id:138475)能谱就是 BdG 矩阵的[本征值](@entry_id:154894)。

作为一个例子，考虑一个处于塞曼场中的s波[超导体](@entry_id:191025) [@problem_id:1132432]。其 BdG [哈密顿量](@entry_id:172864)为：
$$
\mathcal{H}_{\mathbf{k}} = \begin{pmatrix} \xi_{\mathbf{k}}-h & 0 & 0 & \Delta \\ 0 & \xi_{\mathbf{k}}+h & -\Delta & 0 \\ 0 & -\Delta & -\xi_{\mathbf{k}}+h & 0 \\ \Delta & 0 & 0 & -\xi_{\mathbf{k}}-h \end{pmatrix}
$$
其中 $\xi_{\mathbf{k}}$ 是正常态电子[色散](@entry_id:263750)，$\Delta$ 是[超导能隙](@entry_id:145058)， $h$ 是塞曼能量。这个 $4\times4$ 矩阵可以分解为两个不耦合的 $2\times2$ 块。求解其[本征值](@entry_id:154894)，我们得到四支[准粒子](@entry_id:136584)能带：$E = \pm h \pm \sqrt{\xi_{\mathbf{k}}^2 + \Delta^2}$。这清晰地展示了在塞曼场作用下，原本简并的BCS[准粒子](@entry_id:136584)谱 $E = \pm\sqrt{\xi_{\mathbf{k}}^2 + \Delta^2}$ 发生了劈裂。

### 相互作用系统的近似方法

对于包含相互作用的[哈密顿量](@entry_id:172864)，运动方程层级不再自动封闭，我们必须引入近似来截断它。选择何种[近似方案](@entry_id:267451)，取决于我们希望保留哪些关键的物理过程。

#### 平均场与哈特里-福克[解耦](@entry_id:637294)

最简单的近似是**平均场近似**。其核心思想是，当一个算符出现在一个高阶格林函数中时，如果它的涨落效应不重要，我们就可以用它的平均值来代替它。

考虑一个由[传导电子](@entry_id:145260)和[局域磁矩](@entry_id:138106)构成的**自旋-[费米子](@entry_id:146235)模型** [@problem_id:1132422]，其[相互作用哈密顿量](@entry_id:181720)为 $H_{int} = -J \sum_i \mathbf{s}_i \cdot \mathbf{S}_i$。电子[格林函数](@entry_id:147802)的运动方程中会出现一个高阶项 $\langle\langle c_{i\alpha} S_i^\gamma; c_{j\beta}^\dagger \rangle\rangle$。在铁磁背景下，[局域磁矩](@entry_id:138106) $\mathbf{S}_i$ 有一个很大的平均值 $\langle \mathbf{S}_i \rangle = S \hat{\mathbf{z}}$，而其涨落相对较小。因此，我们可以进行如下解耦：
$$
\langle\langle c_{i\alpha} S_i^z; c_{j\beta}^\dagger \rangle\rangle \approx \langle S_i^z \rangle \langle\langle c_{i\alpha}; c_{j\beta}^\dagger \rangle\rangle = S \langle\langle c_{i\alpha}; c_{j\beta}^\dagger \rangle\rangle
$$
通过这种方式，高阶[格林函数](@entry_id:147802)被约化为低阶[格林函数](@entry_id:147802)，方程层级得以封闭。对于自旋-[费米子](@entry_id:146235)模型，这个近似直接导致了一个自旋相关的自能 $\Sigma_\sigma = - J S \sigma/2$（其中 $\sigma = \pm 1$），它使电子能带发生劈裂，解释了巨磁阻等现象。

一个更普适的表述是**[哈特里-福克](@entry_id:142303)（Hartree-Fock）[解耦](@entry_id:637294)** [@problem_id:1132394]。对于一个四[费米子算符](@entry_id:149120)，其[解耦](@entry_id:637294)规则为：
$$
\langle\langle c_a^\dagger c_b c_c; c_d^\dagger \rangle\rangle \approx \langle c_a^\dagger c_b \rangle \langle\langle c_c; c_d^\dagger \rangle\rangle - \langle c_a^\dagger c_c \rangle \langle\langle c_b; c_d^\dagger \rangle\rangle
$$
这里，我们用所有可能的两点关联函数的乘积来近似四点关联函数。这种方法本质上是将相互作用效应平均化，转化为一个有效的单粒子问题。

#### Hubbard-I 近似：抓住原子物理

平均场理论在处理[弱相互作用](@entry_id:157579)时很有效，但对于强[关联电子系统](@entry_id:144460)（如库仑排斥 $U$ 远大于[电子跃迁](@entry_id:152949)能 $t$ 的情况），它则会失效。强关联系统的关键物理在于局域的、原子的行为。**Hubbard-I 近似**（也称原子近似）正是为了抓住这一核心物理而设计的。

我们以**哈伯德模型**为例，其[哈密顿量](@entry_id:172864)为 $H = \sum_{ij,\sigma} t_{ij} c_{i\sigma}^\dagger c_{j\sigma} + U \sum_i n_{i\uparrow} n_{i\downarrow}$。
[单粒子格林函数](@entry_id:140400) $G_{ij\sigma}(\omega) = \langle\langle c_{i\sigma}; c_{j\sigma}^\dagger \rangle\rangle_\omega$ 的运动方程为：
$$
(\omega + \mu) G_{ij\sigma}(\omega) = \delta_{ij} + \sum_m t_{im} G_{mj\sigma}(\omega) + U \langle\langle n_{i\bar{\sigma}} c_{i\sigma}; c_{j\sigma}^\dagger \rangle\rangle_\omega
$$
[相互作用项](@entry_id:637283)产生了一个高阶[格林函数](@entry_id:147802) $\Gamma_{ij\sigma}(\omega) = \langle\langle n_{i\bar{\sigma}} c_{i\sigma}; c_{j\sigma}^\dagger \rangle\rangle_\omega$。我们继续为 $\Gamma_{ij\sigma}$ 写[运动方程](@entry_id:170720)，会发现其动能项 $[n_{i\bar{\sigma}} c_{i\sigma}, H_{kin}]$ 会产生更复杂的[非局域关联](@entry_id:180194)项。

Hubbard-I 近似的核心在于对**第二个[运动方程](@entry_id:170720)**中的动能项进行[解耦](@entry_id:637294) [@problem_id:2861966]：
$$
\langle\langle n_{i\bar{\sigma}} c_{m\sigma}; c_{j\sigma}^\dagger \rangle\rangle_\omega \approx \langle n_{i\bar{\sigma}} \rangle \langle\langle c_{m\sigma}; c_{j\sigma}^\dagger \rangle\rangle_\omega = p G_{mj\sigma}(\omega)
$$
其中 $p = \langle n_{i\bar{\sigma}} \rangle$ 是反向自旋电子的平均占据数。这个[解耦](@entry_id:637294)的物理意义是，当一个电子在[晶格](@entry_id:196752)中运动时，它感受到的其他格点上的电子关联被平均化了。但与平均场不同的是，它精确地保留了电子在同一个格点上与另一个电子的相互作用。

在最简单的**原子极限**（$t_{ij}=0$）下 [@problem_id:809524]，该近似是精确的。求解得到的格林函数为：
$$
G_\sigma(\omega) = \frac{1-p}{\omega-\mu} + \frac{p}{\omega-\mu-U}
$$
其谱函数由两个 $\delta$ 峰构成，分别位于 $\omega=\mu$ 和 $\omega=\mu+U$。这两个能量对应于向一个格点添加电子所需的能量：如果该格点原先没有反向自旋电子，则能量为 $\mu$；如果已经有了一个，则由于库仑排斥，能量变为 $\mu+U$。

当考虑[晶格](@entry_id:196752)上的跃迁（$t_{ij} \neq 0$）时，求解上述封闭的[方程组](@entry_id:193238)会得到一个更复杂的格林函数，其分母是关于 $\omega$ 的二次多项式。这导致了两个极点，对应于两支[色散能](@entry_id:261481)带 [@problem_id:2861966]。这两条能带被称为**下哈伯德带（LHB）**和**上哈伯德带（UHB）**。Hubbard-I 近似成功地描述了由于强[库仑排斥](@entry_id:181876)导致的单条能带分裂为两条（LHB 和 UHB）这一[强关联物理](@entry_id:273328)的核心现象，其间的能量差约为 $U$。

#### 其他[解耦](@entry_id:637294)方案

[运动方程法](@entry_id:147861)的应用非常广泛，不同的物理系统需要不同的[解耦](@entry_id:637294)策略。
例如，在研究自旋系统的[集体激发](@entry_id:145026)（[磁振子](@entry_id:139809)）时，我们可以为自旋[升降算符](@entry_id:197899)的[格林函数](@entry_id:147802) $\langle\langle S_l^+; S_m^- \rangle\rangle_\omega$ 建立运动方程。对于**[海森堡模型](@entry_id:139958)**，这会产生形如 $\langle\langle S_i^z S_j^+; S_m^- \rangle\rangle_\omega$ 的项。**泰亚布利科夫（Tyablikov）解耦**（也称随机相近似，RPA）将其近似为 $\langle S_i^z \rangle \langle\langle S_j^+; S_m^- \rangle\rangle_\omega$，从而可以求解出磁振子的色散关系 [@problem_id:1132437]。

对于描述[高温超导体](@entry_id:156354)的**[t-J模型](@entry_id:143161)**，由于其[希尔伯特空间](@entry_id:261193)被限制在不允许双重占据的[子空间](@entry_id:150286)内，运动方程和解耦方案变得更为复杂，需要特别处理投影算符和自旋-空穴关联 [@problem_id:1132409]。

### [自能](@entry_id:145608)与[戴森方程](@entry_id:146246)

[运动方程法](@entry_id:147861)得到的结果最终可以被整理成一个统一而深刻的形式——**[戴森方程](@entry_id:146246)**。[戴森方程](@entry_id:146246)将相互作用系统的完整格林函数 $G$ 与[无相互作用系统](@entry_id:143064)的格林函数 $G_0$ 以及描述所有相互作用效应的**[自能](@entry_id:145608)**（self-energy）$\Sigma$联系起来：
$$
G(\mathbf{k}, \omega) = G_0(\mathbf{k}, \omega) + G_0(\mathbf{k}, \omega) \Sigma(\mathbf{k}, \omega) G(\mathbf{k}, \omega)
$$
或者更简洁的逆形式：
$$
G^{-1}(\mathbf{k}, \omega) = G_0^{-1}(\mathbf{k}, \omega) - \Sigma(\mathbf{k}, \omega)
$$
其中 $G_0^{-1}(\mathbf{k}, \omega) = \omega - \epsilon_{\mathbf{k}}$ （能量单位为 $\hbar=1$）。通过[运动方程法](@entry_id:147861)求解出的[格林函数](@entry_id:147802)，我们可以反过来识别出在该近似下的[自能](@entry_id:145608)。例如，在 Hubbard-I 近似下，自能是一个只依赖于频率 $\omega$ 而不依赖于动量 $\mathbf{k}$ 的量。

[自能](@entry_id:145608) $\Sigma(\mathbf{k}, \omega)$ 是一个极其重要的物理量，它包含了相互作用对单粒子性质的所有影响 [@problem_id:3019507] [@problem_id:2983430]。自能通常是一个复函数，其实部和虚部分别有明确的物理意义：
- **[自能](@entry_id:145608)的实部 $\text{Re}\,\Sigma^R(\mathbf{k}, \omega)$**：导致[准粒子能量](@entry_id:173936)的**[重整化](@entry_id:143501)**。也就是说，一个在相互作用“云”中运动的电子，其有效能量（或色散关系）会偏离裸电子的能量 $\epsilon_{\mathbf{k}}$。
- **自能的虚部 $\text{Im}\,\Sigma^R(\mathbf{k}, \omega)$**：描述了[准粒子](@entry_id:136584)的**[散射率](@entry_id:143589)**，它与[准粒子](@entry_id:136584)的**寿命** $\tau$ 成反比，即 $\tau_{\mathbf{k}} \propto 1 / |\text{Im}\,\Sigma^R(\mathbf{k}, E_{\mathbf{k}})|$。一个非零的虚部意味着[准粒子](@entry_id:136584)不再是体系的严格[本征态](@entry_id:149904)，它会通过散射衰变成其他激发，因此具有有限的寿命。

像 Hubbard-I 这样的简单[解耦](@entry_id:637294)方案，通常得到的[自能](@entry_id:145608)是纯实的（在能带内部），这意味着它们能描述能带的重整化，但无法描述[准粒子](@entry_id:136584)的有限寿命。要获得有限寿命，需要更高阶的[解耦](@entry_id:637294)方案，它们能保留产生粒子衰变和散射的物理过程。例如，在[费米液体理论](@entry_id:144069)中，更精确的计算表明，在[费米面](@entry_id:137798)附近，[自能](@entry_id:145608)虚部满足 $\text{Im}\,\Sigma^R(\omega, T) \propto -[\omega^2 + (\pi T)^2]$，这正是费米液体[准粒子](@entry_id:136584)具有长寿命的根源 [@problem_id:3019507]。

### 拓展话题

[运动方程法](@entry_id:147861)不仅限于上述平衡态和理想[晶格](@entry_id:196752)系统，它还可以推广到更复杂的情形。

#### [无序系统](@entry_id:145417)：[相干势近似](@entry_id:140539)

对于含有杂质或无序的合金，体系不再具有[平移不变性](@entry_id:195885)。**[相干势近似](@entry_id:140539)**（Coherent Potential Approximation, CPA）是一种强大的平均场理论，用于计算无序体系的平均[格林函数](@entry_id:147802) [@problem_id:1132406]。其思想是，用一个均匀的、待定的、能量依赖的有效势（或[自能](@entry_id:145608)）$\Sigma(E)$ 来替代原来的无规[随机势](@entry_id:144028)，构成一个“有效媒介”。$\Sigma(E)$ 的值通过一个自洽条件来确定：将一个真实的杂质原子嵌入到这个有效媒介中，要求这个杂质产生的平均散射[T矩阵](@entry_id:145367)为零。这保证了有效媒介在“平均”意义上等效于真实[无序系统](@entry_id:145417)。通过求解这个[自洽方程](@entry_id:155949)，我们可以得到体系的平均态密度，研究能带分裂、杂质带形成等现象。

#### 非平衡系统：Keldysh形式

当系统处于外场驱动下的[非平衡稳态](@entry_id:141783)时（例如，加上偏压的[量子输运](@entry_id:138932)体系），仅有[推迟格林函数](@entry_id:139183)不足以描述体系的全部性质。特别是，粒子的占据数[分布](@entry_id:182848)不再是简单的费米-狄拉克或[玻色-爱因斯坦分布](@entry_id:145257)。**Keldysh[非平衡格林函数](@entry_id:201883)**形式为此而生 [@problem_id:1132414]。它引入了更多的格林函数分量，如“小”格林函数 $G^<(\omega)$（它与粒子占据谱密度直接相关）和“大”格林函数 $G^>(\omega)$（与空穴占据谱密度相关）。对这些矩阵形式的格林函数应用[运动方程法](@entry_id:147861)，可以求解非平衡态下的粒子数、电流等物理量。

综上所述，[运动方程法](@entry_id:147861)为研究[多体系统](@entry_id:144006)的单粒子谱性质提供了一个直观且灵活的框架。无论是对于可以精确求解的简单模型，还是需要精巧近似才能处理的复杂相互作用问题，该方法都能引导我们抓住核心物理，获得对系统激发行为的深刻洞察。