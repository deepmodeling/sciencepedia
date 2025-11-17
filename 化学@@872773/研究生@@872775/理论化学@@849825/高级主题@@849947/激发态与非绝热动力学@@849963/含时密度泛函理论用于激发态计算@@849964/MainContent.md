## 引言
理解物质如何与光相互作用，是现代科学的核心议题之一，它驱动着光化学、[光伏材料](@entry_id:161573)、生物成像和光遗传学等众多前沿领域的发展。这些过程的本质，是分子或材料在吸收光子能量后，从[基态](@entry_id:150928)跃迁至[电子激发](@entry_id:190531)态，并由此引发一系列复杂的物理和[化学变化](@entry_id:144473)。从第一性原理出发，描述这些动态过程需要求解[含时薛定谔方程](@entry_id:137898)，但这对于绝大多数真实体系而言，其计算复杂度是难以承受的。因此，发展精确且高效的理论方法来研究电子激发态，成为了理论与计算化学领域的一项重大挑战。

[含时密度泛函理论](@entry_id:200019)（Time-Dependent Density Functional Theory, TDDFT）正是在这样的背景下应运而生，并迅速成为研究分子和材料[激发态](@entry_id:261453)性质最广泛使用的工具之一。与基[态密度](@entry_id:147894)泛函理论（DFT）一脉相承，TDDFT的巧妙之处在于它同样绕开了求解复杂的[多体波函数](@entry_id:203043)，而是将体系的电子密度作为基本变量。它不仅在理论上证明了含时密度包含了系统的全部信息，更重要的是提供了一个在计算上可行的框架，将求解激发能谱的问题转化为一个类似于标准[量子化学](@entry_id:140193)计算的[本征值问题](@entry_id:142153)。

本文旨在为读者提供一份关于TDDFT用于[激发态计算](@entry_id:749156)的全面指南。我们将从理论的基石出发，逐步深入到其应用和前沿挑战。在接下来的章节中，我们将首先在“原理与机制”中深入探讨其理论根基（[龙格-格罗斯定理](@entry_id:272222)）和核心计算机制（含时[科恩-沈方程](@entry_id:143968)与[卡西达方程](@entry_id:183031)）；然后，我们将在“应用与交叉学科联系”中展示其在化学、物理、[材料科学](@entry_id:152226)等多个领域的广泛应用，揭示其如何帮助我们理解复杂体系的光学和[光化学](@entry_id:140933)行为；最后，在“动手实践”部分，通过一系列精心设计的练习，读者将有机会亲手实践并巩固所学的关键概念。

## 原理与机制

在理解了时间相关[密度泛函理论](@entry_id:139027) (Time-Dependent Density Functional Theory, TDDFT) 的基本目标之后，我们现在深入探讨其赖以建立的理论原理和使其在实践中得以应用的计算机制。本章将从根本的定理出发，构建起从抽象理论到具体计算方程的桥梁，并最终审视当前主流近似方法的优势与局限性。

### 基础理论：使用密度的“权利”

任何一种基于电子密度的理论，其合法性的根基都在于证明电子密度这一看似简单的三维[标量场](@entry_id:151443)，确实包含了求解[多体系统](@entry_id:144006)性质所需的全部信息。对于[基态](@entry_id:150928)问题，霍亨伯格-科恩 (Hohenberg-Kohn) 定理扮演了这一角色。对于含时系统，与之对应的基石是 **龙格-格罗斯 (Runge-Gross) 定理**。

[龙格-格罗斯定理](@entry_id:272222)指出，对于一个给定的多电子系统，其初始[多体波函数](@entry_id:203043) $\Psi_0$ 在 $t_0$ 时刻是固定的。如果系统在两个不同的含时外势 $v(\mathbf{r},t)$ 和 $v'(\mathbf{r},t)$ 下演化，并且这两个势的差不仅仅是一个纯粹依赖于时间的函数（即 $v(\mathbf{r},t) - v'(\mathbf{r},t) \neq -c(t)$），那么它们所产生的含时电子密度 $n(\mathbf{r},t)$ 和 $n'(\mathbf{r},t)$ 也必然不同。反之，如果两个势产生的密度相同，那么这两个势最多只相差一个纯粹依赖于时间的函数 $c(t)$。

这个定理建立了一个至关重要的**一一对应关系**：在给定初始状态 $\Psi_0$ 的前提下，含时电子密度 $n(\mathbf{r},t)$ 与外势 $v(\mathbf{r},t)$（在一个仅与时间相关的函数 $c(t)$ 的规范自由度内）是唯一对应的。这意味着，密度 $n(\mathbf{r},t)$ 的演化历史唯一地决定了驱动这一演化的外势。既然系统的[哈密顿量](@entry_id:172864)由外势唯一确定（除了固定的动能和电子间相互作用），那么原则上，所有关于系统演化的信息都可以从含时密度中提取出来。

值得注意的是，[龙格-格罗斯定理](@entry_id:272222)的原始证明依赖于一些关键假设。其中最重要的是要求外势在初始时刻 $t_0$ 附近是**时间解析的**（即可以在 $(t-t_0)$ 中进行[泰勒展开](@entry_id:145057)）。此外，证明过程还利用了[分部积分](@entry_id:136350)，这要求密度和流密度在空间边界处（例如，在无穷远处快速衰减或满足[周期性边界条件](@entry_id:147809)）表现良好，以确保边界项为零。[龙格-格罗斯定理](@entry_id:272222)赋予了我们使用密度作为基本变量来描述量子系统动力学的“权利”，为TDDFT的整个理论框架奠定了坚实的基础。

### 时间相关的科恩-沈 (TDKS) 系统：一个实用的映射

尽管[龙格-格罗斯定理](@entry_id:272222)保证了原理上的可能性，但它并未直接提供一种计算含时密度的方法。与[基态](@entry_id:150928)DFT类似，TDDFT引入了一个巧妙的[辅助系统](@entry_id:142219)——**时间相关的科恩-沈 (Time-Dependent Kohn-Sham, TDKS) 系统**。这是一个虚构的、由无相互作用的电子组成的系统，但它被精心设计，使其在[演化过程](@entry_id:175749)中能够精确地再现真实相互作用系统的含时电子密度 $n(\mathbf{r},t)$。

这个无相互作用的系统中的每个电子（或称[科恩-沈轨道](@entry_id:171979) $\phi_i(\mathbf{r},t)$）都遵循一个单粒子[含时薛定谔方程](@entry_id:137898)，即 **TDKS 方程**（使用[原子单位](@entry_id:166762)）：
$$
\mathrm{i}\frac{\partial}{\partial t} \phi_i(\mathbf{r},t) = \left[ -\frac{1}{2}\nabla^2 + v_{s}(\mathbf{r},t) \right] \phi_i(\mathbf{r},t)
$$
这里的关键在于有效的**[科恩-沈势](@entry_id:169598)** $v_s(\mathbf{r},t)$。为了使这个虚构系统能够再现真实的密度，即满足约束条件 $n(\mathbf{r},t) = \sum_i f_i |\phi_i(\mathbf{r},t)|^2$（其中 $f_i$ 是[轨道](@entry_id:137151)占据数），$v_s$ 必须包含真实系统的所有复杂[多体效应](@entry_id:173569)。它通常被分解为三个部分：
$$
v_s(\mathbf{r},t) = v_{\text{ext}}(\mathbf{r},t) + v_{\text{H}}(\mathbf{r},t) + v_{\text{xc}}(\mathbf{r},t)
$$

1.  $v_{\text{ext}}(\mathbf{r},t)$ 是作用于真实系统的**外部势**（例如，[原子核](@entry_id:167902)的吸引势）。
2.  $v_{\text{H}}(\mathbf{r},t)$ 是经典的**哈特里 (Hartree) 势**，它描述了电子与整个电子云平均[电荷分布](@entry_id:144400)之间的静电相互作用：
    $$
    v_{\text{H}}[n](\mathbf{r},t) = \int \frac{n(\mathbf{r}',t)}{|\mathbf{r}-\mathbf{r}'|} \mathrm{d}\mathbf{r}'
    $$
3.  $v_{\text{xc}}(\mathbf{r},t)$ 是**交换关联 (exchange-correlation, xc) 势**。这是一个核心的、也是理论中最复杂的部分。它被定义为囊括所有剩余[多体效应](@entry_id:173569)的“万能”项，包括真实系统与无相互作用KS系统之间动能的差异，以及所有非经典的交换和关联效应。

精确的交换关联势 $v_{\text{xc}}$ 具有两个至关重要的特性。首先，它具有**[记忆效应](@entry_id:266709) (memory)**，即在时刻 $t$ 的 $v_{\text{xc}}(\mathbf{r},t)$ 不仅依赖于同一时刻的密度 $n(\mathbf{r},t)$，还依赖于所有过去时刻 $t' \lt t$ 的密度历史。其次，它还具有**初始状态依赖性**，即 $v_{\text{xc}}$ 的具体泛函形式依赖于真实相互作用系统的初始态 $\Psi_0$ 和所选的KS系统的初始态 $\Phi_0$。因此，精确的交换关联势应被写为 $v_{\text{xc}}[n, \Psi_0, \Phi_0](\mathbf{r},t)$。TDKS方案的伟大之处在于，它将寻找复杂的[多体波函数](@entry_id:203043) $\Psi(t)$ 的问题，转化为寻找一个有效的单粒子势 $v_s(\mathbf{r},t)$ 的问题，而这个势的核心未知部分就是 $v_{\text{xc}}$。

### [线性响应理论](@entry_id:145737)：探测量子激发

TDDFT的一个主要应用是计算电子激发能和相关的[光谱](@entry_id:185632)性质。这通常是在**[线性响应理论](@entry_id:145737) (linear-response theory)** 的框架下完成的。其基本思想是，当一个系统受到一个微弱的、含时的外部微扰（例如，[电磁场](@entry_id:265881)）时，其密度的响应在微扰强度上是线性的。

描述这种响应的关键物理量是**密度-密度[响应函数](@entry_id:142629)** $\chi(\mathbf{r}, \mathbf{r}', t-t')$。它定义为在 $\mathbf{r}'$ 和 $t'$ 处施加的微扰势 $\delta v_{\text{ext}}(\mathbf{r}',t')$ 引起在 $\mathbf{r}$ 和 $t$ 处密度变化的比例系数，即泛函导数：
$$
\chi(\mathbf{r}, \mathbf{r}', t-t') = \left. \frac{\delta n(\mathbf{r},t)}{\delta v_{\text{ext}}(\mathbf{r}',t')} \right|_{\delta v_{\text{ext}} \to 0}
$$
因此，总的密度响应可以表示为对微扰的卷积：
$$
\delta n(\mathbf{r},t) = \int \mathrm{d}\mathbf{r}' \int \mathrm{d}t' \, \chi(\mathbf{r}, \mathbf{r}', t-t') \, \delta v_{\text{ext}}(\mathbf{r}',t')
$$

物理上的**因果性 (causality)** 原理要求，效应不能先于原因发生。这意味着在时刻 $t$ 的密度响应不能依赖于未来时刻 $t' > t$ 的微扰。这一基本原理对响应函数施加了严格的数学约束：$\chi(\mathbf{r}, \mathbf{r}', t-t') = 0$ 只要 $t  < t'$。满足这一条件的[响应函数](@entry_id:142629)被称为**推迟响应函数 (retarded response function)**。在频率域中，因果性表现为一个同样深刻的性质：[响应函数](@entry_id:142629) $\chi(\omega)$ 在[复频率](@entry_id:266400)平面的上半平面（$\text{Im}\,\omega > 0$）是解析的。这一[解析性](@entry_id:140716)直接导致了其真实[部分和](@entry_id:162077)虚幻部分通过**克拉默-克若尼关系 (Kramers–Kronig relations)**相互关联。

在TDDFT的框架下，我们可以推导出一个联系真实相互作用[系统响应](@entry_id:264152)函数 $\chi$ 和KS[无相互作用系统](@entry_id:143064)响应函数 $\chi_s$ 的方程，通常称为**戴森式方程 (Dyson-like equation)**：
$$
\chi(\omega) = \chi_s(\omega) + \chi_s(\omega) \left[ v_c + f_{\text{xc}}(\omega) \right] \chi(\omega)
$$
其中 $v_c$ 是库仑核（即哈特里相互作用的核），而 $f_{\text{xc}}(\omega)$ 是交换关联核，即 $v_{\text{xc}}$ 对密度 $n$ 的泛函导数。这个方程的物理意义是，真实系统的响应等于KS系统的响应，再加上一个由KS[系统响应](@entry_id:264152)引起的密度变化，通过哈特里和交换关联相互作用，反过来修正[有效势](@entry_id:142581)，并再次产生响应的[无穷级数](@entry_id:143366)之和。

电子激发对应于系统固有的、即使在没有外部驱动场的情况下也能持续存在的密度[振荡](@entry_id:267781)模式。这些模式的频率，即**激发能** $\Omega$，对应于响应函数 $\chi(\omega)$ 的**极点 (poles)**。从戴森式方程的形式可以看出，$\chi(\omega)$ 的极点出现在使得 $(1 - \chi_s(\omega)K(\omega))^{-1}$ 发散的频率处，其中 $K(\omega) = v_c + f_{\text{xc}}(\omega)$。这等价于求解以下方程：
$$
\det[\mathbf{1} - \boldsymbol{\chi}_s(\omega)\mathbf{K}(\omega)] = 0
$$
这里我们已经将算符方程投影到一个有限[基组](@entry_id:160309)上，得到了矩阵形式。这个方程是现代TDDFT计算[激发能](@entry_id:190368)的核心。

### [绝热近似](@entry_id:143074)与[卡西达方程](@entry_id:183031)：TDDFT的主力方法

精确的交换关联核 $f_{\text{xc}}(\omega)$ 具有复杂的频率依赖性，这源于精确 $v_{\text{xc}}$ 的[记忆效应](@entry_id:266709)。在绝大多数实际计算中，一个根本性的简化被采用，即**[绝热近似](@entry_id:143074) (adiabatic approximation)**。

[绝热近似](@entry_id:143074)假设交换关联势完全没有记忆效应，即在时刻 $t$ 的 $v_{\text{xc}}$ 只依赖于同一时刻的密度 $n(\mathbf{r}, t)$。更具体地说，它用对应于瞬时密度 $n(\mathbf{r},t)$ 的那个[基态](@entry_id:150928)交换关联势来近似真实的含时势：
$$
v_{\text{xc}}[n](\mathbf{r},t) \approx v_{\text{xc}}^{\text{A}}[n](\mathbf{r},t) \equiv v_{\text{xc}}^{\text{gs}}[n(\cdot,t)](\mathbf{r})
$$
其中 $v_{\text{xc}}^{\text{gs}}[n] = \delta E_{\text{xc}}^{\text{gs}}[n] / \delta n$ 是由[基态](@entry_id:150928)交换关联能量泛函 $E_{\text{xc}}^{\text{gs}}$ 定义的[基态](@entry_id:150928)势。这一近似的直接后果是，交换关联核变得与频率无关，并且在时域中是局域的：
$$
f_{\text{xc}}^{\text{A}}(\mathbf{r},\mathbf{r}',t-t') = \delta(t-t') \, \left.\frac{\delta v_{\text{xc}}^{\text{gs}}[n](\mathbf{r})}{\delta n(\mathbf{r}')}\right|_{n=n_{0}}
$$
其中 $\delta(t-t')$ 是[狄拉克δ函数](@entry_id:153299)。

在[绝热近似](@entry_id:143074)下，之前寻找响应函数极点的方程可以被重新表述为一个矩阵本征值问题，这被称为**[卡西达方程](@entry_id:183031) (Casida's equations)**。在由KS占据[轨道](@entry_id:137151) $i, j$ 到空[轨道](@entry_id:137151) $a, b$ 的单粒子跃迁构成的[基组](@entry_id:160309)中，该方程具有以下形式：
$$
\begin{pmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B}^* & \mathbf{A}^* \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix} = \omega \begin{pmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & -\mathbf{1} \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix}
$$
其中，$\omega$ 是激发能，向量 $\mathbf{X}$ 和 $\mathbf{Y}$ 分别包含了激发（占据→空）和退激发（空→占据）的组态幅度。矩阵 $\mathbf{A}$ 和 $\mathbf{B}$ 的元素由KS[轨道能级](@entry_id:151753)差和耦合核积分给出。对于一个自旋受限的闭壳层体系，其[矩阵元](@entry_id:186505)可针对**[单重态](@entry_id:154728) (singlet)** 和**三重态 (triplet)** 激发进行自旋匹配：
$$
A_{ia,jb} = \delta_{ij}\delta_{ab}(\epsilon_a - \epsilon_i) + K_{ia,jb}
$$
$$
B_{ia,jb} = K_{ia,bj}
$$
其中[耦合矩阵](@entry_id:191757) $K_{ia,jb}$ 对[单重态和三重态](@entry_id:148894)有不同的形式。以常见的积分为例，$(pq|rs) \equiv \iint \phi_p(\mathbf r)\phi_q(\mathbf r) \frac{1}{|\mathbf r-\mathbf r'|} \phi_r(\mathbf r')\phi_s(\mathbf r') d\mathbf r d\mathbf r'$，我们有：
*   **单重态 ($S$)**: $K_{ia,jb}^{S} = 2\,(ia|jb) + (ia|f_{\text{xc}}^{\uparrow\uparrow} + f_{\text{xc}}^{\uparrow\downarrow}|jb)$
*   **[三重态](@entry_id:156705) ($T$)**: $K_{ia,jb}^{T} = (ia|f_{\text{xc}}^{\uparrow\uparrow} - f_{\text{xc}}^{\uparrow\downarrow}|jb)$

请注意，单重态的哈特里项 $(ia|jb)$ 前有一个因子 $2$，这是由于自旋整合的结果，而[三重态](@entry_id:156705)的哈特里项则因抵消而消失。

为了进一步简化计算，尤其是在早期的TDDFT应用中，**塔姆-丹可夫近似 (Tamm-Dancoff approximation, TDA)** 被广泛使用。TDA的本质是忽略激发与退激发组态之间的耦合，即令 $\mathbf{B}=\mathbf{0}$。在此近似下，[卡西达方程](@entry_id:183031)简化为一个标准的厄米[本征值问题](@entry_id:142153)：
$$
\mathbf{A}\mathbf{X} = \omega \mathbf{X}
$$
这种忽略在物理上可以被认为是退激发振幅 $\mathbf{Y}$ 远小于激发振幅 $\mathbf{X}$。当[耦合矩阵](@entry_id:191757) $\mathbf{B}$ 的元素相对于典型的[轨道能级](@entry_id:151753)差较小时，这种近似是合理的，这通常发生在具有较大[HOMO-LUMO能隙](@entry_id:139325)的体系中。

### [光谱](@entry_id:185632)性质：计算[可观测量](@entry_id:267133)

求解[卡西达方程](@entry_id:183031)不仅能得到[激发能](@entry_id:190368) $\omega_S$，还能得到对应的本征矢 $(\mathbf{X}_S, \mathbf{Y}_S)$。这些本征矢包含了描述[激发态](@entry_id:261453)的宝贵信息，并允许我们计算跃迁相关的[可观测量](@entry_id:267133)。其中最重要的一个量是**[振子强度](@entry_id:147221) (oscillator strength)** $f_S$，它衡量了从[基态](@entry_id:150928)到[激发态](@entry_id:261453) $S$ 的光吸收跃迁的强度。

在长度规范下，对于一个单重态激发，其无量纲振子强度由下式给出：
$$
f_S = \frac{2}{3} \omega_S \sum_{\alpha=x,y,z} \left| \langle 0 | \hat{r}_{\alpha} | S \rangle \right|^2
$$
其中 $\langle 0 | \hat{r}_{\alpha} | S \rangle$ 是从[基态](@entry_id:150928)到[激发态](@entry_id:261453)的跃迁偶极矩。在TDDFT中，这个跃迁偶极矩可以通过卡西达本征矢和单电子偶极积分计算得出。定义一个跃迁偶极向量 $\mathbf{D}_{\alpha}$，其分量为 $(\mathbf{D}_{\alpha})_{ia} = \langle \phi_i | \hat{r}_{\alpha} | \phi_a \rangle$，则跃迁偶极矩由下式给出：
$$
\langle 0 | \hat{r}_{\alpha} | S \rangle_{\text{TDDFT}} = \mathbf{D}_{\alpha}^{\top} (\mathbf{X}_S + \mathbf{Y}_S)
$$
因此，[振子强度](@entry_id:147221)的最终计算公式为：
$$
f_S = \frac{2}{3} \omega_S \sum_{\alpha=x,y,z} \left| \mathbf{D}_{\alpha}^{\top} (\mathbf{X}_S + \mathbf{Y}_S) \right|^2
$$
这个公式是在本征矢满足辛[归一化条件](@entry_id:156486) $\mathbf{X}_S^{\top}\mathbf{X}_S - \mathbf{Y}_S^{\top}\mathbf{Y}_S = 1$ 的情况下成立的。通过计算一系列激发的能量和振子强度，我们就可以模拟出分子的[电子吸收光谱](@entry_id:269577)。

### 已知缺陷与现代解决方案：TDDFT的前沿

尽管绝热TDDFT取得了巨大成功，但它并非万能药。理解其固有的局限性对于正确应用该理论和推动其发展至关重要。以下是两个最著名的“病症”。

#### 电荷转移与里德堡激发

当使用标准的半局域（如[LDA](@entry_id:138982), GGA）或杂化泛函时，绝热TDDFT在描述两类特定激发时会遭遇系统性失败：**长程[电荷转移](@entry_id:155270) (long-range charge-transfer, CT) 激发**和**里德堡 (Rydberg) 激发**。

*   **[电荷转移激发](@entry_id:174772)**：考虑一个由相距很远的给体（D）和受体（A）组成的复合物。一个CT激发对应于电子从D的[轨道](@entry_id:137151)移动到A的[轨道](@entry_id:137151)。在D和A的[轨道空间](@entry_id:148658)重叠可以忽略的极限下，绝热的、空间局域的交换关联核 $f_{\text{xc}}$ 的[矩阵元](@entry_id:186505)在CT跃迁密度之间会趋于零。这导致TDDFT计算出的CT激发能错误地退化为KS[轨道能级](@entry_id:151753)差 $\epsilon_A - \epsilon_D$，严重低估了真实的激发能。更重要的是，它完全丢失了分离后正负离子对之间应有的 $-1/R$ 库仑吸引能。
*   **里德堡激发**：里德堡激发是指电子被激发到离[原子核](@entry_id:167902)非常远的、高度弥散的[轨道](@entry_id:137151)。这些[轨道](@entry_id:137151)的行为由势场的长程性质决定。对于一个中性分子，一个远离的电子应该感受到一个净+1的点电荷，即势应该以 $-1/r$ 的形式衰减。然而，标准半局域泛函的交换关联势部分衰减过快（通常是指数形式），这会抵消掉正确的长程行为。结果是，[基态](@entry_id:150928)KS势无法支持一个正确的、无穷的里德堡能级序列。因此，TDDFT计算要么完全丢失这些激发，要么给出严重不准确的能量。

解决这些问题是TDDFT发展的一个主要驱动力。**[范围分离泛函](@entry_id:199148) (range-separated functionals)** 和**渐近校正势 (asymptotically corrected potentials)** 等现代方法通过在泛函中引入部分[精确交换](@entry_id:178558)并修正其长程行为，已经能够显著改善甚至解决这些问题。

#### 双重激发

另一个根本性的限制是，绝热TDDFT无法描述**双重激发 (double excitations)** 或更一般的多重激发。在精确的理论中，一个主要由两个电子同时被激发的组态构成的多体态，只要它与[基态](@entry_id:150928)之间存在非零的跃迁密度（通常通过关联效应混合入的单激发组分实现），就会在响应函数中表现为一个极点。

然而，绝热TDDFT的数学结构——一个在单粒子-单空穴（$1p1h$）跃迁空间内的本征值问题——从根本上限制了它只能产生与 $1p1h$ 组态数一样多的[激发态](@entry_id:261453)。它所描述的[激发态](@entry_id:261453)都是 $1p1h$ 组态的[线性组合](@entry_id:154743)。一个频率无关的核 $f_{\text{xc}}^{\text{A}}$ 无法在这个框架内创造出新的、对应于双重激发的极点。

原则上，要捕获双重激发，必须超越[绝热近似](@entry_id:143074)，引入一个**频率相关的交换关联核** $f_{\text{xc}}(\omega)$。一个具有自身极点结构的 $f_{\text{xc}}(\omega)$ 可以将这些新的极点引入到总的响应函数 $\chi(\omega)$ 中，从而在[光谱](@entry_id:185632)中产生对应于双重激发的[共振峰](@entry_id:271281)。开发实用且准确的含频核是TDDFT理论研究的一个活跃前沿。

总之，TDDFT提供了一个强大且计算成本相对低廉的框架来研究[电子激发](@entry_id:190531)。其核心机制在于通过TDKS系统和[线性响应理论](@entry_id:145737)，将复杂的多体问题转化为一个有效的单粒子问题。然而，用户必须清醒地认识到[绝热近似](@entry_id:143074)带来的系统性限制，并根据所研究的问题选择合适的泛函或更高级的方法。