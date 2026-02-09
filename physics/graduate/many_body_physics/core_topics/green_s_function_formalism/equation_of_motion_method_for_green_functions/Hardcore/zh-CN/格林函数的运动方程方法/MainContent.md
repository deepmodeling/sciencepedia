## 引言
在多体量子物理中，格林函数是连接微观理论与宏观可观测量的核心工具，但对于复杂的相互作用系统，其计算极具挑战性。格林函数的运动方程（Equation-of-motion, EOM）方法为此提供了一条强大而灵活的途径，它将复杂的动力学问题巧妙地转化为一个代数方程体系，从而系统性地揭示系统的元激发谱。本文旨在全面解析这一关键方法。

我们将分三个层次展开讨论。首先，在“原理与机制”一章中，我们将建立运动方程的基本框架，探讨其如何精确求解简单模型，以及如何通过解耦近似（如Hubbard-I近似）处理强关联系统。其次，在“应用与交叉学科联系”一章中，我们将探索该方法在凝聚态物理、量子输运和量子化学等领域的广泛应用，展示其解决实际物理问题的强大能力。最后，“动手实践”部分将通过具体问题引导读者巩固所学。通过本文的学习，读者将掌握运动方程法的精髓，并理解其在现代科学研究中的重要作用。

## 原理与机制

在上一章中，我们介绍了格林函数作为研究多体系统量子动力学和谱性质的强大工具。本章将深入探讨计算格林函数的一种核心方法——运动方程法（Equation-of-motion, EOM）。该方法通过分析算符在海森堡绘景下的时间演化，建立起一系列关于格林函数的代数方程，从而为求解系统的激发谱和响应函数提供了一条系统性的途径。我们将从该方法的基本原理出发，通过一系列从简至繁的物理模型，阐明其在不同情况下的应用机制，包括精确求解、近似处理以及与戴森方程和自能等核心概念的联系。

### 运动方程法的基本框架

让我们从推迟格林函数的定义开始。对于两个算符 $A$ 和 $B$，其推迟格林函数在时间域和频率域中的定义分别为：
$$
G_{AB}^R(t-t') = -i\Theta(t-t') \langle [A(t), B(t')]_{\eta} \rangle
$$
$$
G_{AB}^R(\omega) = \langle\langle A; B \rangle\rangle_\omega = \int_{-\infty}^{\infty} G_{AB}^R(t) e^{i\omega t} dt
$$
其中，$\Theta(t-t')$ 是赫维赛德阶跃函数，保证了因果性。$\langle \dots \rangle$ 表示在系统基态或热力学系综上的平均。$[A, B]_{\eta} = AB - \eta BA$ 是（反）对易子，对于玻色子（或类玻色子算符）$\eta = 1$，对于费米子（或类费米子算符）$\eta = -1$。格林函数的物理意义在于其谱函数 $A_{AB}(\omega)$，它描述了系统的元激发。谱函数与推迟格林函数的虚部直接相关 [@problem_id:2983430] [@problem_id:809524]：
$$
A_{AB}(\omega) = -\frac{1}{\pi} \text{Im} G_{AB}^R(\omega)
$$
谱函数的峰位对应于元激发的能量，峰高则与其谱权重（或强度）相关。

运动方程法的出发点是海森堡方程 $i\hbar \frac{d A(t)}{dt} = [A(t), H]$。通过对 $G_{AB}^R(t-t')$ 对时间 $t$ 求导，并进行傅里叶变换，我们可以得到其在频率域中的**运动方程**（EOM）：
$$
\hbar\omega \langle\langle A; B \rangle\rangle_\omega = \langle [A, B]_\eta \rangle + \langle\langle [A, H]; B \rangle\rangle_\omega
$$
这个方程是我们后续所有分析的基石。方程的左边是格林函数乘以能量 $\hbar\omega$。右边第一项是一个不含时间的（等时）对易或反对易关系的系综平均，通常是一个常数，称为**非齐次项**。第二项则是一个新的、更高阶的格林函数，其形式为 $\langle\langle [A, H]; B \rangle\rangle_\omega$。

这里的核心挑战在于，对易子 $[A, H]$ 通常会产生比 $A$ 更复杂的算符。例如，如果 $A$ 是一个单粒子算符，而哈密顿量 $H$ 包含相互作用项（如四费米子项），那么 $[A, H]$ 将会包含三粒子算符。对这个新的三粒子格林函数再次使用运动方程，又会产生五粒子格林函数，如此循环往复，形成一个无限的**方程层级**（hierarchy of equations）。运动方程法的精髓就在于如何根据具体的物理问题和所关心的能量尺度，对这个方程层级进行合理的**截断**（truncation）或**解耦**（decoupling），从而得到一个封闭的代数方程组，进而求解出格林函数。

### 精确可解模型：二次型哈密顿量

最简单的情况是当系统的哈密顿量是算符的二次型时。在这种情况下，算符与哈密顿量的对易子 $[A, H]$ 将是原始算符的线性组合。这意味着方程层级在第一步之后便自动封闭，我们可以得到一个有限维的线性方程组，从而精确地求解格林函数。

#### 杂化能带系统

一个典型的例子是描述两个不同自由度（如光子和激子，或传导电子和局域f电子）之间线性耦合的模型。考虑一个由腔光子（算符 $a$）和量子阱激子（算符 $b$）构成的激子-极化激元系统，其哈密顿量为 [@problem_id:1132455]：
$$
H = \hbar\omega_c a^\dagger a + \hbar\omega_x b^\dagger b + \hbar g (a^\dagger b + b^\dagger a)
$$
这里 $\omega_c$ 和 $\omega_x$ 分别是光子和激子的频率， $g$ 是耦合强度。我们想要求解光子格林函数 $G_{aa}(\omega) = \langle\langle a; a^\dagger \rangle\rangle_\omega$。

根据运动方程，我们有：
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
现在我们得到了一个关于 $G_{aa}(\omega)$ 和 $G_{ba}(\omega)$ 的封闭线性方程组。求解这个方程组，可得：
$$
G_{aa}(\omega) = \frac{\omega - \omega_x}{\hbar[(\omega - \omega_c)(\omega - \omega_x) - g^2]}
$$
格林函数的极点给出了体系的元激发能量，即极化激元的色散关系。这些能量是分母为零的解：
$$
(\omega - \omega_c)(\omega - \omega_x) - g^2 = 0
$$
解得两个极化激元分支的能量为 $\omega_{\pm} = \frac{\omega_c + \omega_x}{2} \pm \frac{1}{2}\sqrt{(\omega_c - \omega_x)^2 + 4g^2}$。在共振条件（零失谐）$\omega_c = \omega_x$ 下，能级劈裂为 $\omega_{\pm} = \omega_c \pm g$，能量差 $\Delta E = 2\hbar g$ 被称为**拉比劈裂**（Rabi splitting）。这种由于模式杂化导致的能级劈裂是这类耦合系统的普遍特征。

完全相同的数学结构也出现在其他重要的物理模型中，例如描述重费米子材料的**周期安德森模型**（Periodic Anderson Model）[@problem_id:1132393] 和描述原子与单模光场相互作用的**杰恩斯-卡明斯模型**（Jaynes-Cummings Model）[@problem_id:1132429]，展示了运动方程法在处理杂化问题上的普适性。

#### 超导与南部-戈尔科夫格林函数

另一个重要的精确可解范例是BCS平均场理论下的超导体。超导体的特殊之处在于其基态是电子对的相干叠加，这意味着诸如 $\langle c_{\mathbf{k}\uparrow} c_{-\mathbf{k}\downarrow} \rangle$ 这样的“反常”期待值不为零。为了处理这种情况，我们必须将电子的产生和湮灭算符放在同等地位上。这自然地引出了**南部-戈尔科夫（Nambu-Gorkov）形式**。

我们定义一个四分量的南部旋量 $\Psi_{\mathbf{k}}^\dagger = (c_{\mathbf{k}\uparrow}^\dagger, c_{\mathbf{k}\downarrow}^\dagger, c_{-\mathbf{k}\uparrow}, c_{-\mathbf{k}\downarrow})$，并构建一个 $4\times4$ 的矩阵格林函数 $\hat{G}(\mathbf{k}, \omega) = \langle\langle \Psi_{\mathbf{k}}; \Psi_{\mathbf{k}}^\dagger \rangle\rangle_\omega$。其运动方程可以紧凑地写为：
$$
(\omega\mathbf{1} - \mathcal{H}_{\text{BdG}}(\mathbf{k})) \hat{G}(\mathbf{k}, \omega) = \mathbf{1}
$$
其中 $\mathcal{H}_{\text{BdG}}(\mathbf{k})$ 是**博戈留波夫-德热纳（Bogoliubov-de Gennes, BdG）哈密顿量矩阵**。因此，体系的准粒子激发能谱就是 BdG 矩阵的本征值。

作为一个例子，考虑一个处于塞曼场中的s波超导体 [@problem_id:1132432]。其 BdG 哈密顿量为：
$$
\mathcal{H}_{\mathbf{k}} = \begin{pmatrix} \xi_{\mathbf{k}}-h & 0 & 0 & \Delta \\ 0 & \xi_{\mathbf{k}}+h & -\Delta & 0 \\ 0 & -\Delta & -\xi_{\mathbf{k}}+h & 0 \\ \Delta & 0 & 0 & -\xi_{\mathbf{k}}-h \end{pmatrix}
$$
其中 $\xi_{\mathbf{k}}$ 是正常态电子色散，$\Delta$ 是超导能隙， $h$ 是塞曼能量。这个 $4\times4$ 矩阵可以分解为两个不耦合的 $2\times2$ 块。求解其本征值，我们得到四支准粒子能带：$E = \pm h \pm \sqrt{\xi_{\mathbf{k}}^2 + \Delta^2}$。这清晰地展示了在塞曼场作用下，原本简并的BCS准粒子谱 $E = \pm\sqrt{\xi_{\mathbf{k}}^2 + \Delta^2}$ 发生了劈裂。

### 相互作用系统的近似方法

对于包含相互作用的哈密顿量，运动方程层级不再自动封闭，我们必须引入近似来截断它。选择何种近似方案，取决于我们希望保留哪些关键的物理过程。

#### 平均场与哈特里-福克解耦

最简单的近似是**平均场近似**。其核心思想是，当一个算符出现在一个高阶格林函数中时，如果它的涨落效应不重要，我们就可以用它的平均值来代替它。

考虑一个由传导电子和局域磁矩构成的**自旋-费米子模型** [@problem_id:1132422]，其相互作用哈密顿量为 $H_{int} = -J \sum_i \mathbf{s}_i \cdot \mathbf{S}_i$。电子格林函数的运动方程中会出现一个高阶项 $\langle\langle c_{i\alpha} S_i^\gamma; c_{j\beta}^\dagger \rangle\rangle$。在铁磁背景下，局域磁矩 $\mathbf{S}_i$ 有一个很大的平均值 $\langle \mathbf{S}_i \rangle = S \hat{\mathbf{z}}$，而其涨落相对较小。因此，我们可以进行如下解耦：
$$
\langle\langle c_{i\alpha} S_i^z; c_{j\beta}^\dagger \rangle\rangle \approx \langle S_i^z \rangle \langle\langle c_{i\alpha}; c_{j\beta}^\dagger \rangle\rangle = S \langle\langle c_{i\alpha}; c_{j\beta}^\dagger \rangle\rangle
$$
通过这种方式，高阶格林函数被约化为低阶格林函数，方程层级得以封闭。对于自旋-费米子模型，这个近似直接导致了一个自旋相关的自能 $\Sigma_\sigma = - J S \sigma/2$（其中 $\sigma = \pm 1$），它使电子能带发生劈裂，解释了巨磁阻等现象。

一个更普适的表述是**哈特里-福克（Hartree-Fock）解耦** [@problem_id:1132394]。对于一个四费米子算符，其解耦规则为：
$$
\langle\langle c_a^\dagger c_b c_c; c_d^\dagger \rangle\rangle \approx \langle c_a^\dagger c_b \rangle \langle\langle c_c; c_d^\dagger \rangle\rangle - \langle c_a^\dagger c_c \rangle \langle\langle c_b; c_d^\dagger \rangle\rangle
$$
这里，我们用所有可能的两点关联函数的乘积来近似四点关联函数。这种方法本质上是将相互作用效应平均化，转化为一个有效的单粒子问题。

#### Hubbard-I 近似：抓住原子物理

平均场理论在处理弱相互作用时很有效，但对于强关联电子系统（如库仑排斥 $U$ 远大于电子跃迁能 $t$ 的情况），它则会失效。强关联系统的关键物理在于局域的、原子的行为。**Hubbard-I 近似**（也称原子近似）正是为了抓住这一核心物理而设计的。

我们以**哈伯德模型**为例，其哈密顿量为 $H = \sum_{ij,\sigma} t_{ij} c_{i\sigma}^\dagger c_{j\sigma} + U \sum_i n_{i\uparrow} n_{i\downarrow}$。
单粒子格林函数 $G_{ij\sigma}(\omega) = \langle\langle c_{i\sigma}; c_{j\sigma}^\dagger \rangle\rangle_\omega$ 的运动方程为：
$$
(\omega + \mu) G_{ij\sigma}(\omega) = \delta_{ij} + \sum_m t_{im} G_{mj\sigma}(\omega) + U \langle\langle n_{i\bar{\sigma}} c_{i\sigma}; c_{j\sigma}^\dagger \rangle\rangle_\omega
$$
相互作用项产生了一个高阶格林函数 $\Gamma_{ij\sigma}(\omega) = \langle\langle n_{i\bar{\sigma}} c_{i\sigma}; c_{j\sigma}^\dagger \rangle\rangle_\omega$。我们继续为 $\Gamma_{ij\sigma}$ 写运动方程，会发现其动能项 $[n_{i\bar{\sigma}} c_{i\sigma}, H_{kin}]$ 会产生更复杂的非局域关联项。

Hubbard-I 近似的核心在于对**第二个运动方程**中的动能项进行解耦 [@problem_id:2861966]：
$$
\langle\langle n_{i\bar{\sigma}} c_{m\sigma}; c_{j\sigma}^\dagger \rangle\rangle_\omega \approx \langle n_{i\bar{\sigma}} \rangle \langle\langle c_{m\sigma}; c_{j\sigma}^\dagger \rangle\rangle_\omega = p G_{mj\sigma}(\omega)
$$
其中 $p = \langle n_{i\bar{\sigma}} \rangle$ 是反向自旋电子的平均占据数。这个解耦的物理意义是，当一个电子在晶格中运动时，它感受到的其他格点上的电子关联被平均化了。但与平均场不同的是，它精确地保留了电子在同一个格点上与另一个电子的相互作用。

在最简单的**原子极限**（$t_{ij}=0$）下 [@problem_id:809524]，该近似是精确的。求解得到的格林函数为：
$$
G_\sigma(\omega) = \frac{1-p}{\omega-\mu} + \frac{p}{\omega-\mu-U}
$$
其谱函数由两个 $\delta$ 峰构成，分别位于 $\omega=\mu$ 和 $\omega=\mu+U$。这两个能量对应于向一个格点添加电子所需的能量：如果该格点原先没有反向自旋电子，则能量为 $\mu$；如果已经有了一个，则由于库仑排斥，能量变为 $\mu+U$。

当考虑晶格上的跃迁（$t_{ij} \neq 0$）时，求解上述封闭的方程组会得到一个更复杂的格林函数，其分母是关于 $\omega$ 的二次多项式。这导致了两个极点，对应于两支色散能带 [@problem_id:2861966]。这两条能带被称为**下哈伯德带（LHB）**和**上哈伯德带（UHB）**。Hubbard-I 近似成功地描述了由于强库仑排斥导致的单条能带分裂为两条（LHB 和 UHB）这一强关联物理的核心现象，其间的能量差约为 $U$。

#### 其他解耦方案

运动方程法的应用非常广泛，不同的物理系统需要不同的解耦策略。
例如，在研究自旋系统的集体激发（磁振子）时，我们可以为自旋升降算符的格林函数 $\langle\langle S_l^+; S_m^- \rangle\rangle_\omega$ 建立运动方程。对于**海森堡模型**，这会产生形如 $\langle\langle S_i^z S_j^+; S_m^- \rangle\rangle_\omega$ 的项。**泰亚布利科夫（Tyablikov）解耦**（也称随机相近似，RPA）将其近似为 $\langle S_i^z \rangle \langle\langle S_j^+; S_m^- \rangle\rangle_\omega$，从而可以求解出磁振子的色散关系 [@problem_id:1132437]。

对于描述高温超导体的**t-J模型**，由于其希尔伯特空间被限制在不允许双重占据的子空间内，运动方程和解耦方案变得更为复杂，需要特别处理投影算符和自旋-空穴关联 [@problem_id:1132409]。

### 自能与戴森方程

运动方程法得到的结果最终可以被整理成一个统一而深刻的形式——**戴森方程**。戴森方程将相互作用系统的完整格林函数 $G$ 与无相互作用系统的格林函数 $G_0$ 以及描述所有相互作用效应的**自能**（self-energy）$\Sigma$联系起来：
$$
G(\mathbf{k}, \omega) = G_0(\mathbf{k}, \omega) + G_0(\mathbf{k}, \omega) \Sigma(\mathbf{k}, \omega) G(\mathbf{k}, \omega)
$$
或者更简洁的逆形式：
$$
G^{-1}(\mathbf{k}, \omega) = G_0^{-1}(\mathbf{k}, \omega) - \Sigma(\mathbf{k}, \omega)
$$
其中 $G_0^{-1}(\mathbf{k}, \omega) = \omega - \epsilon_{\mathbf{k}}$ （能量单位为 $\hbar=1$）。通过运动方程法求解出的格林函数，我们可以反过来识别出在该近似下的自能。例如，在 Hubbard-I 近似下，自能是一个只依赖于频率 $\omega$ 而不依赖于动量 $\mathbf{k}$ 的量。

自能 $\Sigma(\mathbf{k}, \omega)$ 是一个极其重要的物理量，它包含了相互作用对单粒子性质的所有影响 [@problem_id:3019507] [@problem_id:2983430]。自能通常是一个复函数，其实部和虚部分别有明确的物理意义：
- **自能的实部 $\text{Re}\,\Sigma^R(\mathbf{k}, \omega)$**：导致准粒子能量的**重整化**。也就是说，一个在相互作用“云”中运动的电子，其有效能量（或色散关系）会偏离裸电子的能量 $\epsilon_{\mathbf{k}}$。
- **自能的虚部 $\text{Im}\,\Sigma^R(\mathbf{k}, \omega)$**：描述了准粒子的**散射率**，它与准粒子的**寿命** $\tau$ 成反比，即 $\tau_{\mathbf{k}} \propto 1 / |\text{Im}\,\Sigma^R(\mathbf{k}, E_{\mathbf{k}})|$。一个非零的虚部意味着准粒子不再是体系的严格本征态，它会通过散射衰变成其他激发，因此具有有限的寿命。

像 Hubbard-I 这样的简单解耦方案，通常得到的自能是纯实的（在能带内部），这意味着它们能描述能带的重整化，但无法描述准粒子的有限寿命。要获得有限寿命，需要更高阶的解耦方案，它们能保留产生粒子衰变和散射的物理过程。例如，在费米液体理论中，更精确的计算表明，在费米面附近，自能虚部满足 $\text{Im}\,\Sigma^R(\omega, T) \propto -[\omega^2 + (\pi T)^2]$，这正是费米液体准粒子具有长寿命的根源 [@problem_id:3019507]。

### 拓展话题

运动方程法不仅限于上述平衡态和理想晶格系统，它还可以推广到更复杂的情形。

#### 无序系统：相干势近似

对于含有杂质或无序的合金，体系不再具有平移不变性。**相干势近似**（Coherent Potential Approximation, CPA）是一种强大的平均场理论，用于计算无序体系的平均格林函数 [@problem_id:1132406]。其思想是，用一个均匀的、待定的、能量依赖的有效势（或自能）$\Sigma(E)$ 来替代原来的无规随机势，构成一个“有效媒介”。$\Sigma(E)$ 的值通过一个自洽条件来确定：将一个真实的杂质原子嵌入到这个有效媒介中，要求这个杂质产生的平均散射T矩阵为零。这保证了有效媒介在“平均”意义上等效于真实无序系统。通过求解这个自洽方程，我们可以得到体系的平均态密度，研究能带分裂、杂质带形成等现象。

#### 非平衡系统：Keldysh形式

当系统处于外场驱动下的非平衡稳态时（例如，加上偏压的量子输运体系），仅有推迟格林函数不足以描述体系的全部性质。特别是，粒子的占据数分布不再是简单的费米-狄拉克或玻色-爱因斯坦分布。**Keldysh非平衡格林函数**形式为此而生 [@problem_id:1132414]。它引入了更多的格林函数分量，如“小”格林函数 $G^<(\omega)$（它与粒子占据谱密度直接相关）和“大”格林函数 $G^>(\omega)$（与空穴占据谱密度相关）。对这些矩阵形式的格林函数应用运动方程法，可以求解非平衡态下的粒子数、电流等物理量。

综上所述，运动方程法为研究多体系统的单粒子谱性质提供了一个直观且灵活的框架。无论是对于可以精确求解的简单模型，还是需要精巧近似才能处理的复杂相互作用问题，该方法都能引导我们抓住核心物理，获得对系统激发行为的深刻洞察。