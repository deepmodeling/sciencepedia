## 引言
在[多体物理学](@entry_id:144526)领域，理解包含大量[相互作用费米子](@entry_id:160994)（如金属中的电子、[液氦-3](@entry_id:147785)原子或[中子星](@entry_id:147259)内的中子）的系统是核心挑战之一。直接求解此类系统的薛定谔方程几乎是不可能的，这构成了一个巨大的知识鸿沟。[朗道费米液体理论](@entry_id:151062)正是在这一背景下应运而生，它提供了一个极其强大且普适的唯象框架，用以描述这些复杂系统在低温下的低能物理行为，而无需深入了解微观相互作用的全部细节。其核心思想在于，系统的低能激发谱与无相互作用的费米气体惊人地相似，只不过基本激发单元不再是裸粒子，而是被相互作用“[重整化](@entry_id:143501)”了的“[准粒子](@entry_id:136584)”。

本文将带领读者系统地穿越费米液体理论的宏伟景观。在第一章“原理与机制”中，我们将深入探讨[准粒子](@entry_id:136584)的概念、其数学描述（[格林函数](@entry_id:147802)方法）以及描述[准粒子](@entry_id:136584)间相互作用的朗道能量泛函，揭示理论的根基。随后的第二章“应用与跨学科联系”将展示该理论的强大威力，阐明它如何解释从[凝聚态物质](@entry_id:747660)到[核物理](@entry_id:136661)和天体物理等不同领域中的宏观现象。最后，在“动手实践”部分，我们提供了一系列精心设计的问题，旨在通过计算和分析，帮助读者将抽象的理论概念转化为具体的物理洞察。通过这趟旅程，您将掌握现代[多体物理学](@entry_id:144526)中不可或缺的基石之一。

## 原理与机制

本章旨在深入探讨费米液体理论的核心原理与基本机制。在前一章介绍[费米液体](@entry_id:142392)理论的背景和动机之后，我们将系统地阐述[准粒子](@entry_id:136584)的概念、它们的性质以及它们之间的相互作用。我们将从微观的[格林函数](@entry_id:147802)图像和唯象的Landau能量泛函两个角度出发，揭示这一理论如何精确地描述[相互作用费米子](@entry_id:160994)系统的低能物理。此外，我们还将探讨该理论如何预测宏观[热力学](@entry_id:141121)与[输运性质](@entry_id:203130)，并最终讨论其适用范围的边界，即[费米液体](@entry_id:142392)理论在某些物理情境下如何失效。

### [准粒子](@entry_id:136584)的概念：从微观图像到唯象理论

相互作用的[多体系统](@entry_id:144006)是凝聚态物理的核心挑战之一。即使只考虑两体相互作用，其复杂性也通常使得精确求解薛定谔方程变得不可能。[Landau费米液体理论](@entry_id:151062)的卓越之处在于，它提出了一种巧妙的解决思路：尽管系统的[基态](@entry_id:150928)和高能[激发态](@entry_id:261453)可能极其复杂，但其低能激发谱却可能具有与无[相互作用费米气体](@entry_id:160307)相似的结构。其基本激发单元不再是裸露的[费米子](@entry_id:146235)，而是“[准粒子](@entry_id:136584)”（quasiparticle）。

[准粒子](@entry_id:136584)是一个携带与原始[费米子](@entry_id:146235)相同[量子数](@entry_id:145558)（如[电荷](@entry_id:275494)、自旋、动量）的[元激发](@entry_id:140859)，但其性质（如能量、质量）因与周围粒子云的相互作用而被“重整化”（renormalized）。可以将其想象成一个在人群中移动的人：他/她的运动不仅取决于自身，还受到周围人群排斥和牵引的影响，使其有效惯性增大。类似地，一个[准粒子](@entry_id:136584)是一个裸[费米子](@entry_id:146235)及其周围[粒子-空穴激发](@entry_id:137289)云共同构成的复合体。

#### [准粒子](@entry_id:136584)的基石：绝热连续性与[Luttinger定理](@entry_id:143497)

[准粒子](@entry_id:136584)概念的合法性依赖于一个深刻的假设，即**绝热连续性**（adiabatic continuity）。该原理 [@problem_id:2999007] 断言，对于一个正常的金属态，我们可以通过将[相互作用强度](@entry_id:192243) $\lambda$ 从零“绝热地”（即缓慢且不引起[相变](@entry_id:147324)）开启到其完全强度，从而将无[相互作用费米气体](@entry_id:160307)的[基态](@entry_id:150928)和低能[激发态](@entry_id:261453)连续地演化为相互作用系统的相应状态。在这个过程中，低能[激发态](@entry_id:261453)之间不会发生[能级穿越](@entry_id:152596)。

这意味着，[无相互作用系统](@entry_id:143064)中的一个单粒子（或单空穴）激发，在相互作用开启后，会平滑地演变为一个携带相同量子数的、长寿命的[准粒子](@entry_id:136584)（或准空穴）激发。这种一一对应关系是费米液体理论的根基，它允许我们用[无相互作用系统](@entry_id:143064)的[量子数](@entry_id:145558)来标记和描述相互作用系统的低能激发。

这一图像的稳定性得到了 **Luttinger 定理** [@problem_id:2998980] 的有力支持。该定理是一个严格的非微扰结论，它指出，只要系统保持为正常的[费米液体](@entry_id:142392)态（没有发生[对称性破缺](@entry_id:158994)），其[费米面](@entry_id:137798)的体积 $\mathcal{V}_F$ 完全由粒子[数密度](@entry_id:268986) $n$ 决定，而与相互作用的细节无关。对于自旋为 $1/2$ 的[费米子](@entry_id:146235)，其关系为：
$$
n = \frac{2}{(2\pi)^d} \mathcal{V}_F
$$
其中 $d$ 是空间维度。Luttinger 定理的证明依赖于[单粒子格林函数](@entry_id:140400)的解析性质和守恒律，特别是所谓的Luttinger-[Ward恒等式](@entry_id:147000)。该定理保证了即使在[强相互作用](@entry_id:159198)下，“费米面”这个几何概念依然稳固且具有明确的物理意义，它所包围的[动量空间](@entry_id:148936)体积与[自由费米子](@entry_id:140103)情形下完全相同。

#### [准粒子](@entry_id:136584)的性质：格林函数方法

绝热连续性的假设可以在格林函数的形式化语言中得到精确的数学表述。单粒子[推迟格林函数](@entry_id:139183) $G^R(\mathbf{p}, \omega)$ 描述了在系统中加入一个动量为 $\mathbf{p}$ 的粒子后，以能量 $\omega$ 将其找回的几率幅。它由[戴森方程](@entry_id:146246)（Dyson equation）定义：
$$
G^R(\mathbf{p}, \omega) = \frac{1}{\omega - \epsilon^0_{\mathbf{p}} - \Sigma^R(\mathbf{p}, \omega)}
$$
其中 $\epsilon^0_{\mathbf{p}}$ 是裸粒子的[色散关系](@entry_id:140395)，而**自能**（self-energy）$\Sigma^R(\mathbf{p}, \omega)$ 则包含了所有相互作用的复杂效应。

一个长寿命的粒子状激发对应于格林函数在[复频率](@entry_id:266400)平面上靠近[实轴](@entry_id:148276)的一个极点。对于[费米液体](@entry_id:142392)中的[准粒子](@entry_id:136584)，其性质就由这个极点周围格林函数的行为决定。在极点附近，[格林函数](@entry_id:147802)可以近似写为 [@problem_id:2999059] [@problem_id:2998987]：
$$
G^R(\mathbf{p}, \omega) \approx \frac{Z_{\mathbf{p}}}{\omega - (\epsilon_{\mathbf{p}}-\mu) + i\Gamma_{\mathbf{p}}/2}
$$
其中 $\mu$ 是化学势。这个表达式揭示了[准粒子](@entry_id:136584)的三个关键属性：

1.  **[准粒子能量](@entry_id:173936) $\epsilon_{\mathbf{p}}$**：极点的实部定义了[准粒子](@entry_id:136584)的能量。它由方程 $\epsilon_{\mathbf{p}} - \epsilon^0_{\mathbf{p}} - \text{Re}\,\Sigma^R(\mathbf{p}, \epsilon_{\mathbf{p}}-\mu) = 0$ 隐式定义。相互作用通过自能的实部 $\text{Re}\,\Sigma^R$ 来重整化裸粒子的能量。在[费米面](@entry_id:137798)附近，我们可以线性化色散关系 $\epsilon_{\mathbf{p}} \approx \mu + v_F^* (|\mathbf{p}| - p_F)$，其中 $p_F$ 是[费米动量](@entry_id:147114)。这定义了[准粒子](@entry_id:136584)的费米速度 $v_F^*$ 和**有效质量** $m^*$ ($v_F^* = p_F/m^*$)。相互作用通常导致 $m^* \neq m$，其中 $m$ 是裸[粒子质量](@entry_id:156313) [@problem_id:2999059]。

2.  **[准粒子寿命](@entry_id:145453) $\tau_{\mathbf{p}} = 1/\Gamma_{\mathbf{p}}$**：极点的虚部 $\Gamma_{\mathbf{p}}$ 描述了[准粒子](@entry_id:136584)的衰变率，即寿命的倒数。它与[自能](@entry_id:145608)的虚部直接相关：$\Gamma_{\mathbf{p}} = -2Z_{\mathbf{p}} \text{Im}\,\Sigma^R(\mathbf{p}, \epsilon_{\mathbf{p}}-\mu)$。一个关键的结论是，由于[泡利不相容原理](@entry_id:141850)对散射末态相空间的严格限制，靠近[费米面](@entry_id:137798)的[准粒子](@entry_id:136584)的[衰变率](@entry_id:156530)会迅速趋于零。对于三维系统，其标度行为为 [@problem_id:2999049]：
    $$
    \Gamma_{\mathbf{p}} \propto (\epsilon_{\mathbf{p}} - \mu)^2
    $$
    这个二次方的衰减是[费米液体](@entry_id:142392)稳定性的核心。它保证了当[准粒子能量](@entry_id:173936) $\epsilon_{\mathbf{p}}$ 趋近于化学势 $\mu$ 时，其能量不确定度 $\Gamma_{\mathbf{p}}$ 比其激发能 $|\epsilon_{\mathbf{p}}-\mu|$更快地趋于零。即 $\Gamma_{\mathbf{p}}/|\epsilon_{\mathbf{p}}-\mu| \to 0$。这正是[准粒子](@entry_id:136584)概念之所以良好的根本原因：它们在费米面附近变得越来越“像”一个真正的粒子 [@problem_id:2999059]。我们可以通过一个具体的例子来理解这一点。假设自能虚部为 $\text{Im}\,\Sigma^R(\omega) = -\alpha(\omega-\mu)^2$，其中 $\alpha$ 是一个正常数。对于一个能量为 $E_k = \mu + \delta E$ 的[准粒子](@entry_id:136584)，其寿命 $\tau$ 可以计算为 [@problem_id:1136184]：
    $$
    \frac{1}{\tau} = -2Z\,\text{Im}\,\Sigma^R(E_k) = -2Z[-\alpha(E_k - \mu)^2] = 2\alpha Z (\delta E)^2
    $$
    因此，$\tau = \frac{1}{2\alpha Z (\delta E)^2}$。当 $\delta E \to 0$ 时，寿命 $\tau \to \infty$。

3.  **[准粒子权重](@entry_id:140100) $Z_{\mathbf{p}}$**：极点的留数（residue） $Z_{\mathbf{p}}$，也称为[准粒子权重](@entry_id:140100)，取值在 $0 \lt Z_{\mathbf{p}} \le 1$ 之间 ($Z=1$ 对应无相互作用情况)。它有深刻的物理意义 [@problem_id:2999059] [@problem_id:2998987]：
    *   从形式上，它由自能的频率依赖性决定：$Z_{\mathbf{p}} = \left( 1 - \frac{\partial \text{Re}\,\Sigma^R(\mathbf{p}, \omega)}{\partial \omega} \right)^{-1}_{\omega=\epsilon_{\mathbf{p}}-\mu}$。
    *   从谱函数 $A(\mathbf{p},\omega) = -2\text{Im}\,G^R(\mathbf{p},\omega)$ 的角度看，$Z_{\mathbf{p}}$ 是[准粒子](@entry_id:136584)相干峰（coherent peak）所占的[谱权重](@entry_id:144751)，而 $1-Z_{\mathbf{p}}$ 的权重则[分布](@entry_id:182848)在更宽的非相干背景（incoherent background）中，后者代表了更复杂的多体激发。
    *   从[多体波函数](@entry_id:203043)的角度看，$Z_{\mathbf{p}}$ 是将一个裸粒子加入系统所形成的态 $c^\dagger_{\mathbf{p}}|\Psi_0^N\rangle$ 与真实的 $(N+1)$ [粒子系统](@entry_id:180557)单[准粒子](@entry_id:136584)本征态 $|\Psi_{\mathbf{p}}^{N+1}\rangle$ 之间交叠的平方，即 $Z_{\mathbf{p}} = |\langle \Psi_{\mathbf{p}}^{N+1} | c_{\mathbf{p}}^{\dagger} | \Psi_0^N \rangle|^2$。
    *   从可观测量的角度看，$Z_{\mathbf{p}_F}$（在费米面上的权重）等于零温下系统动量分布函数 $n(\mathbf{p})=\langle c^\dagger_{\mathbf{p}} c_{\mathbf{p}} \rangle$ 在[费米面](@entry_id:137798) $p_F$ 处的不连续跳变的大小。

只要 $Z_{\mathbf{p}_F} > 0$，[准粒子](@entry_id:136584)图像就成立，费米液体理论的根基就稳固。

### [准粒子](@entry_id:136584)间的相互作用：Landau[能量泛函](@entry_id:170311)

Landau 理论的另一面是其唯象方法，它直接从[准粒子](@entry_id:136584)的存在性出发，构建了一个描述系统低能行为的[有效理论](@entry_id:155490)。其核心思想是，系统的总能量可以看作是[准粒子](@entry_id:136584)占据数[分布](@entry_id:182848) $\{n_{\mathbf{p}\sigma}\}$ 的一个泛函 $E[\{n_{\mathbf{p}\sigma}\}]$。

对于一个偏离[基态](@entry_id:150928)[分布](@entry_id:182848) $n^0_{\mathbf{p}\sigma}$ 很小的[激发态](@entry_id:261453)，其占据数变化为 $\delta n_{\mathbf{p}\sigma} = n_{\mathbf{p}\sigma} - n^0_{\mathbf{p}\sigma}$。能量泛函对 $\delta n_{\mathbf{p}\sigma}$ 进行[泰勒展开](@entry_id:145057)，到二阶项为 [@problem_id:2999012]：
$$
\delta E = E - E_0 = \sum_{\mathbf{p}\sigma} \epsilon_{\mathbf{p}\sigma} \delta n_{\mathbf{p}\sigma} + \frac{1}{2V} \sum_{\mathbf{p}\sigma, \mathbf{p}'\sigma'} f_{\sigma\sigma'}(\mathbf{p}, \mathbf{p}') \delta n_{\mathbf{p}\sigma} \delta n_{\mathbf{p}'\sigma'}
$$
这里，$V$ 是系统体积。

*   线性项的系数 $\epsilon_{\mathbf{p}\sigma} = \frac{\delta E}{\delta n_{\mathbf{p}\sigma}}\Big|_{0}$ 正是[基态](@entry_id:150928)中[准粒子](@entry_id:136584)的能量，它对应于[格林函数](@entry_id:147802)方法中定义的[准粒子色散](@entry_id:161746)。
*   二次项的系数 $f_{\sigma\sigma'}(\mathbf{p}, \mathbf{p}') = V \frac{\delta^2 E}{\delta n_{\mathbf{p}\sigma} \delta n_{\mathbf{p}'\sigma'}}\Big|_{0}$ 被称为 **Landau 相互作用函数**。它描述了两个[准粒子](@entry_id:136584)之间的有效相互作用。物理上，它代表了由于一个[准粒子](@entry_id:136584)占据数的变化 $\delta n_{\mathbf{p}'\sigma'}$ 引起的另一个[准粒子能量](@entry_id:173936)的变化：
    $$
    \delta\epsilon_{\mathbf{p}\sigma} = \frac{1}{V} \sum_{\mathbf{p}'\sigma'} f_{\sigma\sigma'}(\mathbf{p}, \mathbf{p}') \delta n_{\mathbf{p}'\sigma'}
    $$
    $f$ 函数不是裸粒子间的相互作用势，而是一个高度[重整化](@entry_id:143501)的量，它描述了[准粒子](@entry_id:136584)之间的[前向散射振幅](@entry_id:154109)。

#### Landau相互作用函数与[Landau参数](@entry_id:144630)

对于一个各向同性、自旋旋转不变的系统，相互作用函数 $f_{\sigma\sigma'}(\mathbf{p}, \mathbf{p}')$ 仅依赖于费米面上两个动量 $\mathbf{p}$ 和 $\mathbf{p}'$ 之间的夹角 $\theta$ 以及它们的自旋构型。它可以被分解为**自旋对称** ($f^s$) 和**自旋反对称** ($f^a$) 两个通道 [@problem_id:2998983]：
$$
f^s(\theta) = \frac{1}{2} (f_{\uparrow\uparrow}(\theta) + f_{\uparrow\downarrow}(\theta))
$$
$$
f^a(\theta) = \frac{1}{2} (f_{\uparrow\uparrow}(\theta) - f_{\uparrow\downarrow}(\theta))
$$
$f^s$ 通道描述了与总密度（[电荷](@entry_id:275494)）扰动相关的相互作用，而 $f^a$ 通道描述了与自旋密度（磁化）扰动相关的相互作用。

为了便于应用，通常将这两个函数展开为勒让德多项式 $P_l(\cos\theta)$：
$$
f^{s,a}(\cos\theta) = \sum_{l=0}^\infty f_l^{s,a} P_l(\cos\theta)
$$
展开系数 $f_l^{s,a}$ 具有能量×体积的量纲。通过乘以[费米能级](@entry_id:143215)的单[自旋态](@entry_id:149436)密度 $N(0)$，可以得到一组无量纲的常数，即 **Landau 参数** $F_l^s$ 和 $F_l^a$：
$$
F_l^s = N(0) f_l^s, \quad F_l^a = N(0) f_l^a
$$
这些 Landau 参数是理论的核心，它们是描述特定费米液体性质的唯象参数，原则上可以从实验中测定，或从更微观的理论中计算。

### 宏观性质与集体行为

Landau 参数的巨大威力在于，它们直接决定了系统的各种宏观响应函数和热力学性质。

#### 热力学性质的[重整化](@entry_id:143501)

系统的许多宏观性质，如[有效质量](@entry_id:142879)、压缩性、磁化率，都因相互作用而从无[相互作用费米气体](@entry_id:160307)的取值上发生偏移。Landau 理论给出了这些[重整化](@entry_id:143501)与 Landau 参数之间的精确关系 [@problem_id:2999040]。

*   **[有效质量](@entry_id:142879) $m^*$**：对于一个伽利略不变的系统（如[液氦-3](@entry_id:147785)），[有效质量](@entry_id:142879)与 $F_1^s$ 参数有直接关系 [@problem_id:1136159] [@problem_id:1136104]：
    $$
    \frac{m^*}{m} = 1 + \frac{F_1^s}{3}
    $$
    这个关系源于对系统总动量流的守恒要求。一个[准粒子](@entry_id:136584)的运动会引起周围流体的“背流”（backflow），$F_1^s$ 正是描述了这种效应。

*   **[可压缩性](@entry_id:144559) $\kappa$**：[等温压缩率](@entry_id:140894)衡量系统抵抗密度变化的能力。它与 $l=0$ 的对称参数 $F_0^s$ 相关 [@problem_id:1136133]：
    $$
    \frac{\kappa}{\kappa_0} = \frac{m^*/m}{1+F_0^s}
    $$
    其中 $\kappa_0$ 是相同密度的无[相互作用费米气体](@entry_id:160307)的压缩率。一个排斥性相互作用（$F_0^s > 0$）会使液体更“硬”，降低其可压缩性。

*   **[自旋磁化率](@entry_id:141223) $\chi_s$**：泡利顺磁磁化率描述系统在外[磁场](@entry_id:153296)下的自旋极化趋势。它由 $l=0$ 的反对称参数 $F_0^a$ 决定 [@problem_id:1136105]：
    $$
    \frac{\chi_s}{\chi_{0}} = \frac{m^*/m}{1+F_0^a}
    $$
    其中 $\chi_0$ 是无相互作用时的泡利[磁化率](@entry_id:138219)。如果 $F_0^a$ 趋近于 $-1$，[磁化率](@entry_id:138219)会发散，这预示着系统趋向于[铁磁不稳定性](@entry_id:157649)，即所谓的 **[Stoner 不稳定性](@entry_id:157501)**。

#### [费米液体](@entry_id:142392)的稳定性

[费米液体](@entry_id:142392)作为一个[热力学](@entry_id:141121)稳定相，必须能抵抗各种自发形变。这些稳定性条件对 Landau 参数施加了严格的约束。例如，上面提到的[可压缩性](@entry_id:144559)和[磁化率](@entry_id:138219)必须为正，这要求：
$$
1+F_0^s > 0 \implies F_0^s > -1
$$
$$
1+F_0^a > 0 \implies F_0^a > -1
$$
违反第一个条件（$F_0^s \to -1$）意味着系统抵抗相分离的能力消失，会发生[一级相变](@entry_id:155013) [@problem_id:1136182]。违反第二个条件（$F_0^a \to -1$）则对应于[铁磁不稳定性](@entry_id:157649)。

除了这些均匀的形变，费米面本身也可能自发地偏离球形。这类不稳定性被称为 **Pomeranchuk 不稳定性**。对于一个具有角动量 $l \ge 1$ 的形变，稳定性条件要求 [@problem_id:1136122]：
$$
1 + \frac{F_l^s}{2l+1} > 0 \implies F_l^s > -(2l+1)
$$
$$
1 + \frac{F_l^a}{2l+1} > 0 \implies F_l^a > -(2l+1)
$$
例如，$l=2$ 的对称通道不稳定性（$F_2^s \to -5$）对应于费米面向四极形（nematic）的自发扭曲。这些条件展示了 Landau 理论如何内在地包含了对其自身有效性的判据。

### 動力學與響應理論

Landau 理论不仅能描述静态的热力学性质，还能通过一个半经典的动理学方程来描述系统的动态响应和[集体激发](@entry_id:145026)。

#### [Landau-Silin动理学方程](@entry_id:138539)

对于一个空间不均匀或随时间变化的系统，准[粒子[分布函](@entry_id:753202)数](@entry_id:145626) $n_{\mathbf{p}\sigma}(\mathbf{r}, t)$ 的演化由 **Landau-Silin 动理学方程** 描述 [@problem_id:2999041]：
$$
\frac{\partial n_{\mathbf{p}\sigma}}{\partial t} + \nabla_{\mathbf{p}}\varepsilon_{\mathbf{p}\sigma} \cdot \nabla_{\mathbf{r}} n_{\mathbf{p}\sigma} - \nabla_{\mathbf{r}}\varepsilon_{\mathbf{p}\sigma} \cdot \nabla_{\mathbf{p}} n_{\mathbf{p}\sigma} = I_{\text{coll}}[n]
$$
这个方程类似于经典的玻尔兹曼方程，但有本质区别：
1.  它描述的是[准粒子](@entry_id:136584)，而非裸粒子。
2.  [准粒子](@entry_id:136584)的能量 $\varepsilon_{\mathbf{p}\sigma}(\mathbf{r}, t)$ 不仅依赖于动量 $\mathbf{p}$ 和外部[势场](@entry_id:143025)，它本身还是[分布函数](@entry_id:145626) $n$ 的泛函，包含了来自其他[准粒子](@entry_id:136584)的[平均场相互作用](@entry_id:200557)。力项 $-\nabla_{\mathbf{r}}\varepsilon_{\mathbf{p}\sigma}$ 中包含了这一重要的平均场效应。
3.  $I_{\text{coll}}[n]$ 是描述[准粒子](@entry_id:136584)之间剩余散射的[碰撞积分](@entry_id:152100)项，它驱动系统趋向[局域平衡](@entry_id:156295)。

这个方程是研究费米液体中各种[输运现象](@entry_id:147655)（如[电导](@entry_id:177131)、[热导](@entry_id:189019)）和[集体模](@entry_id:137129)式（如[零声](@entry_id:142772)）的出发点。

#### 守恒律、[Ward恒等式](@entry_id:147000)与[顶点修正](@entry_id:146982)

在微观理论中计算[响应函数](@entry_id:142629)（如电导率）时，必须小心处理相互作用以保证物理守恒律（如[电荷守恒](@entry_id:264158)）得到满足。一个常见的近似是只考虑[自能修正](@entry_id:754667)的“泡图”（dressed bubble）计算，即使用完全格林函数 $G$ 但使用裸顶点。然而，这种近似通常会破坏守恒律 [@problem_id:2999023]。

正确的做法是确保自能 $\Sigma$ 和三点[顶点函数](@entry_id:145137) $\Gamma^\mu$ 的近似是一致的，满足所谓的**Ward-Takahashi 恒等式**。该恒等式是[规范不变性](@entry_id:137857)（电荷守恒）在[量子场论](@entry_id:138177)中的体现，它将[顶点函数](@entry_id:145137)与[格林函数](@entry_id:147802)联系起来：
$$
q_\mu \Gamma^\mu(p+q, p) = G^{-1}(p+q) - G^{-1}(p)
$$
这意味着，对[自能](@entry_id:145608)的任何近似都隐含着对**[顶点修正](@entry_id:146982)**（vertex corrections）的特定要求。只有包含了这些相容的[顶点修正](@entry_id:146982)，计算出的响应函数才能保证满足守恒律和相关的求和规则（如 $f$-sum rule）。

#### 伽利略不变性与[晶格](@entry_id:196752)效应

在伽利略不变的系统中（如[液氦-3](@entry_id:147785)），物理定律在一个惯性系到另一个的变换下不变。这导致了一个强大的[非重整化定理](@entry_id:156718)：系统的总电流与[总动量](@entry_id:173071)成正比，比例系数只含裸质量 $m$。这意味着，尽管[准粒子](@entry_id:136584)的有效质量 $m^*$ 被相互作用[重整化](@entry_id:143501)，但系统的[电荷输运](@entry_id:194535)响应（如电导率的[Drude权重](@entry_id:140162)）最终只依赖于裸质量 $m$ [@problem_id:2999023]。这种看似矛盾的结果得以实现，正是因为[顶点修正](@entry_id:146982)（在唯象语言中称为“背流”效应）的贡献恰好抵消了[自能修正](@entry_id:754667)中 $m^*$ 的效应 [@problem_id:1272843]。

然而，对于[晶格](@entry_id:196752)中的电子，伽利略[不变性](@entry_id:140168)被周期性势场打破。[晶格动量](@entry_id:143609)守恒只在模一个[倒格矢](@entry_id:263351)的意义下成立。因此，上述的[非重整化定理](@entry_id:156718)不再适用 [@problem_id:2998994]。在金属中：
*   [有效质量](@entry_id:142879)与 $F_1^s$ 之间的简单关系 $m^*/m = 1+F_1^s/3$ 不再成立。
*   电流响应变得复杂，它不仅依赖于带结构（裸[粒子速度](@entry_id:196946) $\nabla_{\mathbf{k}}\varepsilon_{\mathbf{k}}$），还受到复杂的、不再能简单由 $F_1^s$ 描述的[顶点修正](@entry_id:146982)的影响。
*   光学 $f$-sum rule 的形式也发生改变，它不再简单地与 $n/m$ 相关，而是与能带曲率的布里渊区平均有关 [@problem_id:2998994]。

这凸显了将[费米液体](@entry_id:142392)理论应用于真实固体材料时需要注意的 subtlety。

### 費米[液体理论](@entry_id:152493)的失效

尽管[费米液体](@entry_id:142392)理论在描述常规金属和[液氦-3](@entry_id:147785)方面取得了巨大成功，但它并非 universally applicable。它的基础——长寿命[准粒子](@entry_id:136584)的存在——在某些物理系统中会被破坏。

#### 一维系统：[Luttinger液体](@entry_id:140974)

在一维空间中，[泡利不相容原理](@entry_id:141850)的限制变得异常苛刻，使得低能粒子只能进行[前向散射](@entry_id:191808)。这种受限的运动学特性从根本上改变了系统的物理行为。相互作用的[费米子](@entry_id:146235)一维系统不再是[费米液体](@entry_id:142392)，而是被称为**Luttinger 液体** [@problem_id:2999049]。

Luttinger 液体与费米液体的关键区别在于：
*   **无[准粒子](@entry_id:136584)**：单粒子激发不再是良好定义的[元激发](@entry_id:140859)。[准粒子权重](@entry_id:140100) $Z$ 精确为零。这意味着将一个电子加入系统会立即引发强烈的集体响应，使其溶解在多体背景中。
*   **[自旋-电荷分离](@entry_id:142517)**：系统的低能激发是两种独立的集体模式：[电荷密度波](@entry_id:146282)和[自旋密度波](@entry_id:139011)。这两种模式以不同的速度传播。一个注入的电子会“分裂”成一个携带其[电荷](@entry_id:275494)的“[电荷](@entry_id:275494)子”（holon）和一个携带其自旋的“[自旋子](@entry_id:140415)”（spinon）。
*   **[幂律](@entry_id:143404)行为**：由于没有[准粒子](@entry_id:136584)，各种物理量（如谱函数、[隧穿态密度](@entry_id:145618)）在低能下表现出与相互作用相关的[幂律](@entry_id:143404)行为，而不是费米液体中的有限跳变或常数行为。

#### [量子临界点](@entry_id:144325)附近：非[费米液体](@entry_id:142392)

即使在二维或三维空间，费米液体理论也可能在零温[相变](@entry_id:147324)点——即**[量子临界点](@entry_id:144325)**（QCP）——附近失效 [@problem_id:2999019]。当通过调谐某个非温度参数（如压力、[磁场](@entry_id:153296)、掺杂）使系统趋近于一个连续的[量子相变](@entry_id:146027)时，序参量的量子涨落会变得长程且低频。

如果这些临界涨落与[费米面](@entry_id:137798)上的[粒子-空穴激发](@entry_id:137289)有效耦合，它们会成为一个极其有效的散射源，从而破坏[准粒子](@entry_id:136584)。例如，在二维铁磁或向列相（nematic）量子临界点附近，理论分析（Hertz-Millis理论）表明，临界涨落是[过阻尼](@entry_id:167953)的，其动力学标度指数为 $z=3$。与这些涨落的相互作用导致[电子自能](@entry_id:148523)具有奇异的频率依赖性：
$$
\Sigma(\omega) \propto \omega^{2/3}
$$
这导致[准粒子](@entry_id:136584)衰减率 $\Gamma(\omega) \propto \omega^{2/3}$。因此，比率 $\Gamma(\omega)/\omega \propto \omega^{-1/3}$ 在 $\omega \to 0$ 时发散，完全违反了[准粒子](@entry_id:136584)存在的条件。在这种**非费米液体**（non-Fermi liquid）中，输运和热力学性质也表现出与标准费米液体理论预测显著不同的奇异温度依赖性，这是现代凝聚态物理研究的一个核心前沿领域。