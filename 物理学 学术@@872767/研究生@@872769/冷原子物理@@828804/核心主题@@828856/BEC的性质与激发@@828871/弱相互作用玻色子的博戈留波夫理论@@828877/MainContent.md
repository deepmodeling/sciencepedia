## 引言
玻色-爱因斯坦凝聚（Bose-Einstein Condensation, BEC）的实现开启了[量子多体物理学](@entry_id:141705)的新纪元。然而，[理想玻色气体](@entry_id:150722)的[简单图](@entry_id:274882)像忽略了原子间的相互作用，而正是这些相互作用催生了[超流性](@entry_id:159036)、[量子损耗](@entry_id:139939)等一系列深刻的物理现象。如何超越平均场理论，从微观层面精确描述一个[弱相互作用](@entry_id:157579)的[玻色子](@entry_id:138266)系统，是理解这些现象的关键。

博戈留波夫理论（Bogoliubov theory）为此提供了一个强大而优美的理论框架。它通过巧妙的数学变换，将一个复杂的[多体问题](@entry_id:138087)简化为一组无相互作用的[元激发](@entry_id:140859)——[准粒子](@entry_id:136584)，从而深刻揭示了系统的[基态](@entry_id:150928)结构和动力学行为。

本文将系统地引导读者掌握博戈留波夫理论的核心。在“原理与机制”一章中，我们将深入探讨理论的基本假设、[哈密顿量](@entry_id:172864)的对角化过程，以及由此得到的激发谱和[基态](@entry_id:150928)性质。随后的“应用与跨学科联系”一章将展示该理论如何解释真实世界的实验现象，并揭示其与凝聚态物理、[量子光学](@entry_id:140582)等领域的深刻联系。最后，通过“动手实践”部分提供的计算问题，读者将有机会亲手应用理论，巩固对关键概念的理解。

## 原理与机制

在理解了[相互作用玻色气体](@entry_id:160184)在低温下的基本物理图像，特别是玻色-爱因斯坦凝聚（Bose-Einstein Condensation, BEC）的概念之后，我们现在深入探讨描述这类系统的核心理论工具——博戈留波夫理论（Bogoliubov theory）。这一理论为我们提供了一个处理[弱相互作用玻色子](@entry_id:160415)多体问题的有效方法，揭示了系统的[基态](@entry_id:150928)性质和[元激发](@entry_id:140859)谱，这些都是非相互作用理论无法企及的。本章将系统地阐述博戈留波夫理论的基本原理、核心机制及其导出的一系列重要物理预测。

### 博戈留波夫近似：[哈密顿量](@entry_id:172864)的线性化

我们考虑一个由质量为 $m$ 的[玻色子](@entry_id:138266)组成的均匀气体，粒子间通过一个弱排斥的短程接触势 $U(\mathbf{r}) = g\delta(\mathbf{r})$（其中 $g > 0$）相互作用。系统的[哈密顿量](@entry_id:172864)在[二次量子化](@entry_id:137766)形式下为：
$$
\hat{H} = \sum_{\mathbf{k}} \epsilon_k \hat{a}_\mathbf{k}^\dagger \hat{a}_\mathbf{k} + \frac{g}{2V} \sum_{\mathbf{k}, \mathbf{p}, \mathbf{q}} \hat{a}_{\mathbf{p}+\mathbf{q}}^\dagger \hat{a}_{\mathbf{k}-\mathbf{q}}^\dagger \hat{a}_\mathbf{k} \hat{a}_\mathbf{p}
$$
其中 $\hat{a}_\mathbf{k}^\dagger$ 和 $\hat{a}_\mathbf{k}$ 分别是动量为 $\hbar\mathbf{k}$ 的粒子的产生和[湮灭算符](@entry_id:165390)，$\epsilon_k = \frac{\hbar^2 k^2}{2m}$ 是单粒子动能，$V$ 是系统体积。

由于相互作用项的存在，这个[哈密顿量](@entry_id:172864)无法精确对角化。博戈留波夫理论的出发点是一个关键的物理近似。在低温下，由于玻色-爱因斯坦凝聚，动量为零的[基态](@entry_id:150928)被宏观数量的粒子 $N_0$ 占据。因此，$\hat{a}_0^\dagger$ 和 $\hat{a}_0$ 的算符性质不再重要，它们的行为更像一个经典复数（c-number）。**博戈留波夫近似**（Bogoliubov approximation）正是将这两个算符替换为经典数：
$$
\hat{a}_0, \hat{a}_0^\dagger \to \sqrt{N_0}
$$
这里我们忽略了凝聚体相位的起伏，并将其设为实数。对于弱[相互作用气体](@entry_id:144962)，凝聚体的损耗很小，因此我们可以进一步近似 $N_0 \approx N$，其中 $N$ 是总粒子数。

将此近似代入[哈密顿量](@entry_id:172864)，并只保留非凝聚体算符（$\mathbf{k} \neq 0$）的至多二次项，我们可以得到描述激发模的有效哈密顿量。相互作用项中，最重要的贡献来自于一个或两个粒子在凝聚体中，而另外的粒子处于[激发态](@entry_id:261453)。经过系统的展开和整理，主要贡献项包括：
1.  凝聚体自身的平均场能量。
2.  激发粒子与凝聚体相互作用的项。

最终，描述[激发态](@entry_id:261453)的二次[哈密顿量](@entry_id:172864)可以写作 [@problem_id:1231315]：
$$
\hat{H}' = \sum_{\mathbf{k} \neq 0} \left[ (\epsilon_k + gn) \hat{a}_\mathbf{k}^\dagger \hat{a}_\mathbf{k} + \frac{gn}{2} (\hat{a}_\mathbf{k}^\dagger \hat{a}_{-\mathbf{k}}^\dagger + \hat{a}_\mathbf{k} \hat{a}_{-\mathbf{k}}) \right]
$$
这里，$n = N/V$ 是总粒子密度。第一项 $(\epsilon_k + gn) \hat{a}_\mathbf{k}^\dagger \hat{a}_\mathbf{k}$ 描述了激发粒子在凝聚体平均场中的能量，其中 $gn$ 是平均场能移。第二项 $\frac{gn}{2} (\hat{a}_\mathbf{k}^\dagger \hat{a}_{-\mathbf{k}}^\dagger + \hat{a}_\mathbf{k} \hat{a}_{-\mathbf{k}})$ 则是所谓的**反常项**（anomalous terms），它描述了从凝聚体中产生一对动量相反的粒子 ($\hat{a}_\mathbf{k}^\dagger \hat{a}_{-\mathbf{k}}^\dagger$) 或将这样一对粒子湮灭回凝聚体 ($\hat{a}_\mathbf{k} \hat{a}_{-\mathbf{k}}$) 的过程。正是这些反常项的存在，使得[哈密顿量](@entry_id:172864)不是对角的，也暗示了系统的真实[基态](@entry_id:150928)并非简单的粒子真空。

### [对角化](@entry_id:147016)：博戈留波夫变换与[准粒子](@entry_id:136584)

为了对角化[哈密顿量](@entry_id:172864) $\hat{H}'$，我们需要引入一种新的变换，即**博戈留波夫变换**（Bogoliubov transformation）。这个变换定义了一组新的算符 $\beta_\mathbf{k}$ 和 $\beta_\mathbf{k}^\dagger$，它们是原有粒子算符的[线性组合](@entry_id:154743)：
$$
\hat{a}_\mathbf{k} = u_k \beta_\mathbf{k} - v_k \beta_{-\mathbf{k}}^\dagger \\
\hat{a}_\mathbf{k}^\dagger = u_k \beta_\mathbf{k}^\dagger - v_k \beta_{-\mathbf{k}}
$$
其中，系数 $u_k$ 和 $v_k$ 是依赖于动量大小 $k=|\mathbf{k}|$ 的实数。我们希望新的算符 $\beta_\mathbf{k}$ 和 $\beta_\mathbf{k}^\dagger$ 描述的是系统中表现良好的[元激发](@entry_id:140859)，即**[准粒子](@entry_id:136584)**（quasiparticles）。这些[准粒子](@entry_id:136584)应当仍然是[玻色子](@entry_id:138266)，这意味着它们的算符必须满足标准的[玻色子](@entry_id:138266)[对易关系](@entry_id:136780)：
$$
[\beta_\mathbf{k}, \beta_{\mathbf{k}'}^\dagger] = \delta_{\mathbf{k},\mathbf{k}'}, \quad [\beta_\mathbf{k}, \beta_{\mathbf{k}'}] = 0, \quad [\beta_\mathbf{k}^\dagger, \beta_{\mathbf{k}'}^\dagger] = 0
$$
将变换式代入[对易关系](@entry_id:136780) $[\hat{a}_\mathbf{k}, \hat{a}_\mathbf{k}^\dagger] = 1$，我们得到：
$$
[u_k \beta_\mathbf{k} - v_k \beta_{-\mathbf{k}}^\dagger, u_k \beta_\mathbf{k}^\dagger - v_k \beta_{-\mathbf{k}}] = u_k^2 [\beta_\mathbf{k}, \beta_\mathbf{k}^\dagger] - v_k^2 [\beta_{-\mathbf{k}}^\dagger, \beta_{-\mathbf{k}}] = u_k^2 - (-v_k^2) = u_k^2 - v_k^2
$$
为了保持对易关系不变，即 $[\hat{a}_\mathbf{k}, \hat{a}_\mathbf{k}^\dagger]=1$，我们必须要求系数满足[归一化条件](@entry_id:156486)：
$$
u_k^2 - v_k^2 = 1
$$
这个条件保证了博戈留波夫变换是一种**[正则变换](@entry_id:178165)**（canonical transformation）。它本质上是一种广义的旋转，混合了产生和[湮灭算符](@entry_id:165390)。任何满足 $|c_1|^2 - |c_2|^2 = 1$ 的变换 $\Gamma_k = c_1 \beta_k + c_2 \beta_{-k}^\dagger$ 都会保持[玻色子](@entry_id:138266)[代数结构](@entry_id:137052) [@problem_id:1231317]。

将变换代入[哈密顿量](@entry_id:172864) $\hat{H}'$，并选择合适的 $u_k$ 和 $v_k$ 使得所有非对角项（如 $\beta_\mathbf{k}\beta_{-\mathbf{k}}$ 和 $\beta_\mathbf{k}^\dagger\beta_{-\mathbf{k}}^\dagger$）的系数为零。这一过程最终给出了 $u_k$ 和 $v_k$ 的表达式：
$$
u_k^2 = \frac{\epsilon_k + gn + E_k}{2E_k}, \quad v_k^2 = \frac{\epsilon_k + gn - E_k}{2E_k}
$$
以及[对角化](@entry_id:147016)后的[哈密顿量](@entry_id:172864)：
$$
\hat{H}' = E_{GS} + \sum_{\mathbf{k} \neq 0} E_k \beta_\mathbf{k}^\dagger \beta_\mathbf{k}
$$
这里的 $E_k$ 就是[准粒子](@entry_id:136584)的能量，即[元激发](@entry_id:140859)谱。$E_{GS}$ 是系统的[基态能量](@entry_id:263704)，包含了平均场能量和所有[准粒子](@entry_id:136584)模的[零点能](@entry_id:142176)之和。

### 博戈留波夫谱：[元激发](@entry_id:140859)

通过上述对角化过程，我们得到了著名的**博戈留波夫色散关系**（Bogoliubov dispersion relation）：
$$
E_k = \sqrt{(\epsilon_k + gn)^2 - (gn)^2} = \sqrt{\epsilon_k (\epsilon_k + 2gn)}
$$
这个[色散关系](@entry_id:140395)揭示了弱[相互作用[玻色气](@entry_id:160184)体](@entry_id:155364)中[元激发](@entry_id:140859)的深刻物理内涵。我们可以分析其在两个极限下的行为：

1.  **长波（低动量）极限** ($k \to 0$): 当 $\epsilon_k \ll gn$ 时，我们可以展开平方根，得到：
    $$
    E_k \approx \sqrt{2gn\epsilon_k} = \sqrt{2gn \frac{\hbar^2 k^2}{2m}} = \hbar k \sqrt{\frac{gn}{m}} \equiv \hbar c k
    $$
    这是一种线性的、[声子](@entry_id:140728)般的[色散关系](@entry_id:140395)。它表明系统的长波激发是**[声子](@entry_id:140728)**（phonons），其传播速度为 $c = \sqrt{gn/m}$。这个速度就是系统中的**声速**。[线性色散关系](@entry_id:266313)是超流体的一个标志性特征。

2.  **短波（高动量）极限** ($k \to \infty$): 当 $\epsilon_k \gg gn$ 时，[色散关系](@entry_id:140395)渐进于：
    $$
    E_k \approx \sqrt{\epsilon_k^2} = \epsilon_k = \frac{\hbar^2 k^2}{2m}
    $$
    这恢复了[自由粒子](@entry_id:148748)的二次[色散关系](@entry_id:140395)。这表明，高能激发（波长远小于平均粒子间距）的行为就像单个的、不受集体效应影响的粒子。

因此，博戈留波夫理论优美地统一了集体[声子](@entry_id:140728)激发和单粒子激发这两种图像。

### 博戈留波夫[基态](@entry_id:150928)的性质

对角化后的[哈密顿量](@entry_id:172864)描述了一套无相互作用的[准粒子](@entry_id:136584)。系统的**[基态](@entry_id:150928)** $|G\rangle$ 自然就是这些[准粒子](@entry_id:136584)的真空态，即对于所有 $\mathbf{k} \neq 0$：
$$
\beta_\mathbf{k} |G\rangle = 0
$$
然而，这个[准粒子](@entry_id:136584)真空态与原初的粒子真空态（即所有粒子都在凝聚体中）截然不同。我们可以通过计算[基态](@entry_id:150928)中[激发态](@entry_id:261453)粒子数来揭示这一点。[基态](@entry_id:150928)中动量为 $\mathbf{k}$ 的粒子数密度为：
$$
\langle G| \hat{a}_\mathbf{k}^\dagger \hat{a}_\mathbf{k} |G\rangle = \langle G| (u_k \beta_\mathbf{k}^\dagger - v_k \beta_{-\mathbf{k}}) (u_k \beta_\mathbf{k} - v_k \beta_{-\mathbf{k}}^\dagger) |G\rangle
$$
利用 $\beta_\mathbf{k} |G\rangle = 0$ 和 $\langle G| \beta_\mathbf{k}^\dagger = 0$，上式中唯一不为零的项是包含 $\beta_{-\mathbf{k}} \beta_{-\mathbf{k}}^\dagger$ 的项，其[期望值](@entry_id:153208)为1。因此我们得到：
$$
\langle G| \hat{a}_\mathbf{k}^\dagger \hat{a}_\mathbf{k} |G\rangle = v_k^2 \langle G| \beta_{-\mathbf{k}} \beta_{-\mathbf{k}}^\dagger |G\rangle = v_k^2
$$
由于 $v_k^2 > 0$，这表明即使在绝对零度的[基态](@entry_id:150928)下，由于相互作用，仍然有一部分粒子被散射出凝聚体，占据了 $\mathbf{k} \neq 0$ 的动量态。这一现象被称为**[量子损耗](@entry_id:139939)**（quantum depletion）。总的损耗粒子密度 $n'$ 为：
$$
n' = \frac{1}{V} \sum_{\mathbf{k} \neq 0} \langle \hat{a}_\mathbf{k}^\dagger \hat{a}_\mathbf{k} \rangle = \int \frac{d^d k}{(2\pi)^d} v_k^2
$$
其中 $d$ 是空间维度。例如，在二维情况下，可以计算出损耗分数 $n'/n$ 是一个与密度无关的常数，仅由[相互作用强度](@entry_id:192243)决定 [@problem_id:1231292]：
$$
\frac{n'}{n} = \frac{mg}{4\pi\hbar^2}
$$

另一个揭示[基态](@entry_id:150928)结构的有趣物理量是**反常对关联函数**（anomalous pair correlator）$\langle G| \hat{a}_\mathbf{k} \hat{a}_{-\mathbf{k}} |G\rangle$。在无相互作用的[基态](@entry_id:150928)中，此值为零。但在博戈留波夫[基态](@entry_id:150928)中 [@problem_id:1231315]：
$$
\langle G| \hat{a}_\mathbf{k} \hat{a}_{-\mathbf{k}} |G\rangle = \langle G| (u_k \beta_\mathbf{k} - v_k \beta_{-\mathbf{k}}^\dagger) (u_k \beta_{-\mathbf{k}} - v_k \beta_{\mathbf{k}}^\dagger) |G\rangle = -u_k v_k
$$
这个非零值表明，相互作用[基态](@entry_id:150928)中存在着动量完全相反的粒子对的相干叠加。这类似于[量子光学](@entry_id:140582)中的“[压缩真空态](@entry_id:195785)”，它包含了成[对产生](@entry_id:154125)的[光子](@entry_id:145192)。

### 物理预言与应用

博戈留波夫理论不仅提供了一个定性的物理图像，还能做出定量的预测。

#### [基态能量](@entry_id:263704)修正

系统的[基态能量](@entry_id:263704) $E_{GS}$ 是凝聚体的平均场能加上所有[准粒子](@entry_id:136584)模的[零点能](@entry_id:142176)之和。零点能贡献为 $\Delta E = \frac{1}{2} \sum_{\mathbf{k} \neq 0} (E_k - \epsilon_k - gn)$。这个求和在紫外（大 $k$）区域是发散的，需要通过正规化手段处理，即用真实的[散射长度](@entry_id:142881) $a_s$ 替换耦合常数 $g$。在三维空间中，这一计算最终导出了著名的 **Lee-Huang-Yang (LHY) 修正** [@problem_id:1231379]，它给出了超越平均场理论的第一个[能量修正](@entry_id:198270)项。以[单粒子能量](@entry_id:160812)表示，修正项为：
$$
\frac{\Delta E}{N} = \frac{256\sqrt{\pi}\hbar^2}{15m} a_s^{5/2} n^{3/2}
$$
其中 $g$ 已被 $g = 4\pi\hbar^2 a_s / m$ 替换。这个结果是稀薄[玻色气体](@entry_id:155364)理论的里程碑，与实验高度吻合。

我们也可以通过计算[基态能量](@entry_id:263704)来得到[热力学](@entry_id:141121)量，如化学势 $\mu = \partial E_g / \partial N$。在一维系统中，可以精确计算出量子涨落对化学势的修正 [@problem_id:1231296]。平均场化学势为 $\mu_{MF} = gn$，而考虑了[零点能](@entry_id:142176)之后的修正是：
$$
\delta\mu = \mu - \mu_{MF} = -\frac{\sqrt{m}g^{3/2}n^{1/2}}{2\pi\hbar}
$$
这表明[量子涨落](@entry_id:154889)倾向于降低系统的化学势。

#### [动态结构因子](@entry_id:143433)

系统的响应函数也可以在博戈留波夫理论框架下计算。**[动态结构因子](@entry_id:143433)** $S(\mathbf{k}, \omega)$ 描述了系统在受到一个动量为 $\hbar\mathbf{k}$、能量为 $\hbar\omega$ 的微扰时的响应强度。在零温下，博戈留波夫理论预言：
$$
S(\mathbf{k}, \omega) = \frac{\epsilon_k}{E_k} \delta(\omega - E_k/\hbar)
$$
这表明，系统只能通过创造一个能量为 $E_k$ 的单一[准粒子](@entry_id:136584)来吸收能量和动量。这个结果虽然是近似的，但它满足一些严格的理论约束，比如 **[f-求和规则](@entry_id:147775)**（f-sum rule）。该规则要求 $S(\mathbf{k}, \omega)$ 的一阶频率矩等于粒子的动能。我们可以验证：
$$
M_1(\mathbf{k}) = \int_0^\infty d\omega \, \omega S(\mathbf{k}, \omega) = \int_0^\infty d\omega \, \omega \frac{\epsilon_k}{E_k} \delta(\omega - E_k/\hbar) = \frac{E_k}{\hbar} \frac{\epsilon_k}{E_k} = \frac{\epsilon_k}{\hbar} = \frac{\hbar k^2}{2m}
$$
这与 [f-求和规则](@entry_id:147775)完全一致，显示了理论的内在[自洽性](@entry_id:160889) [@problem_id:1231275]。

#### 有限温效应

在有限温度 $T>0$ 时，[准粒子](@entry_id:136584)会根据[玻色-爱因斯坦分布](@entry_id:145257)被[热激发](@entry_id:275697)，其布居数为 $n_B(E_k) = (\exp(E_k/k_B T) - 1)^{-1}$。这些[热激发](@entry_id:275697)的[准粒子](@entry_id:136584)会导致凝聚体粒子数的进一步减少，称为**热损耗**（thermal depletion）。总的非凝聚粒子密度 $n'$ 由[量子损耗](@entry_id:139939)和热损耗两部分构成。在低温极限 $k_B T \ll gn$下，只有低能的[声子](@entry_id:140728)模被显著激发。此时，热损耗密度 $n'_T(T)$ 的主导行为是 [@problem_id:1394]：
$$
n'_{T}(T) \approx \int \frac{d^3k}{(2\pi)^3} \frac{\epsilon_k+gn_0}{E_k} n_B(E_k) \approx \frac{m^{3/2}k_B^2T^2}{12\hbar^3(gn_0)^{1/2}}
$$
结果表明，在低温下，热损耗密度随温度的平方 $T^2$ 增长，这与[声子](@entry_id:140728)激发的特性直接相关。

### [玻色气体](@entry_id:155364)中的不稳定性

博戈留波夫理论不仅能描述稳定体系，还能预测系统何时会变得不稳定。

#### 吸引相互作用与塌缩

如果[玻色子](@entry_id:138266)之间的相互作用是吸引的（$g = -|g|  0$），博戈留波夫谱变为：
$$
E_k = \sqrt{\epsilon_k (\epsilon_k - 2|g|n_0)}
$$
当动量较小，满足 $\epsilon_k  2|g|n_0$ 时，平方根内的表达式为负，导致[激发能](@entry_id:190368) $E_k$ 成为纯虚数。设 $E_k = i\hbar\Gamma_k$，则某个模式的布居数会随时间[指数增长](@entry_id:141869) $\propto \exp(2\Gamma_k t)$。这标志着系统存在**动力学不稳定性**（dynamical instability）。物理上，这意味着均匀的凝聚体不是一个稳定的[基态](@entry_id:150928)，任何微小的[密度涨落](@entry_id:143540)都会被放大，最终导致系统向更高密度的区域**塌缩**（collapse）。通过计算可以找到[不稳定性增长率](@entry_id:265537) $\Gamma_k$ 的最大值，它发生在 $\epsilon_k = |g|n_0$ 处 [@problem_id:1313]：
$$
\Gamma_{max} = \frac{|g|n_0}{\hbar}
$$
这个增长率决定了塌缩过程的初始时间尺度。

#### 流动[超流体](@entry_id:180718)与[临界速度](@entry_id:161155)

超流性的一个关键特征是无耗散的流动，但这只在流速低于某个**临界速度**（critical velocity）时才成立。博戈留波夫理论可以用来确定这个速度。考虑一个以速度 $\mathbf{v}_s$ 运动的凝聚体，其激发谱可以通过伽利略变换得到。然而，一个更严格的判据来自于考察系统[哈密顿量](@entry_id:172864)的正定性。在流动的[参考系](@entry_id:169232)中，二次[哈密顿量](@entry_id:172864)可以写成一个矩阵形式。当流速 $v_s$ 超过某个阈值时，该矩阵不再是正定的，意味着系统的能量不再有下界，从而导致动力学不稳定性，激发数会指数增长。

通过分析这个[哈密顿量](@entry_id:172864)矩阵的[本征值](@entry_id:154894)，可以发现，不稳定性首先出现在 $v_s$ 超过声速 $c$ 时 [@problem_id:1231335]。因此，动力学不稳定性给出的[临界速度](@entry_id:161155)为：
$$
v_c = \sqrt{\frac{gn_s}{m}} = c
$$
这个结果（$v_c=c$）是[超流体](@entry_id:180718)理论中的一个基本结论，它将宏观的[临界流动](@entry_id:275258)行为与微观的[元激发](@entry_id:140859)谱（声速）直接联系起来。

### 理论的范围与局限

博戈留波夫理论无疑是成功的，它正确预测了弱[相互作用[玻色气](@entry_id:160184)体](@entry_id:155364)的[声子](@entry_id:140728)激发、[量子损耗](@entry_id:139939)、LHY[能量修正](@entry_id:198270)和超流[临界速度](@entry_id:161155)等一系列核心物理现象。然而，它的基础——博戈留波夫近似——本身破坏了粒子数守恒。凝聚体被当作一个无限大的粒子蓄水池，可以随意取走或添加粒子。

更精致的、保持粒子数守恒的理论（如[Popov理论](@entry_id:162175)）也存在。有趣的是，通过对比可以发现，这些理论得到的[元激发](@entry_id:140859)谱与标准博戈留波夫谱在形式上非常接近。例如，一个Popov类型的[哈密顿量](@entry_id:172864)给出的[色散关系](@entry_id:140395)为 $\omega_P(\mathbf{k}) = \sqrt{(\epsilon_{\mathbf{k}}+g n)^2-(g n_0)^2}$。可以证明，这个[色散关系](@entry_id:140395)要与标准的博戈留波夫[色散](@entry_id:263750) $\omega_B(\mathbf{k}) = \sqrt{\epsilon_{\mathbf{k}}(\epsilon_{\mathbf{k}} + 2gn_0)}$ 完[全等](@entry_id:273198)同，当且仅当损耗密度 $n' = n - n_0 = 0$ [@problem_id:1231278]。这说明，只要相互作用是弱的，[量子损耗](@entry_id:139939)很小（$n_0 \approx n$），那么不守恒的博戈留波夫近似就是一个非常好的近似。

最后必须强调，博戈留波夫理论是一个**[弱耦合](@entry_id:140994)理论**。它适用于稀薄气体，其中参数 $na_s^3 \ll 1$ (在3D中)。对于[强相互作用](@entry_id:159198)系统，或者在低维（如一维和二维）系统中长波涨落极其重要的情况下，该理论会失效，需要更复杂的理论工具来处理。尽管如此，它仍然是所有现代[超冷原子气体](@entry_id:143830)理论的基石和出发点。