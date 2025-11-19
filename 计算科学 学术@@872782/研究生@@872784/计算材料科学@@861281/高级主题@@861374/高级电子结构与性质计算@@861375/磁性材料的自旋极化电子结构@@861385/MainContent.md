## 引言
磁性材料是现代科技的基石，从[数据存储](@entry_id:141659)到能源转换，其应用无处不在。要从根本上理解并设计这些材料的性能，我们必须深入其微观世界，探索由电子[自旋不平衡](@entry_id:160115)所决定的“[自旋极化电子结构](@entry_id:755226)”。[第一性原理计算](@entry_id:198754)，特别是基于密度泛函理论（DFT）的方法，已成为连接量子力学与宏观磁性的最强大桥梁，然而，从基础理论到精确预测真实材料的复杂磁性行为，仍存在着理论和方法上的挑战，例如如何处理强关联效应和相对论效应。

本文旨在系统性地梳理这一核心领域。在“原理与机制”一章中，我们将从[自旋密度泛函理论](@entry_id:755223)出发，逐步建立起描述磁性的理论框架，并探讨处理[强关联体系](@entry_id:145791)与[非共线磁性](@entry_id:181233)的高级方法。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论如何应用于预测磁各向异性、自旋电子学性质和[磁光效应](@entry_id:262395)等实际问题，彰显其在[材料科学](@entry_id:152226)和凝聚态物理中的广泛影响力。最后，“动手实践”部分将提供一系列计算练习，帮助您将理论知识转化为解决实际问题的能力，从而真正掌握[磁性材料](@entry_id:137953)的计算研究。

## 原理与机制

在“引言”章节中，我们概述了磁性材料在科学和技术中的重要性，并介绍了[自旋极化电子结构](@entry_id:755226)计算作为理解和预测其性质的核心工具。本章将深入探讨这些计算背后的基本原理和核心机制。我们将从[自旋密度泛函理论](@entry_id:755223)的基础出发，逐步建立描述磁性体系的科恩-沈（Kohn-Sham）方程，探讨交换关联泛函的关键作用，并阐明治愈标准 DFT 近似缺陷的方法。最后，我们将讨论超越简单共线磁性的更高级理论，并探索如何将[第一性原理计算](@entry_id:198754)结果与描述[磁相](@entry_id:161372)互作用的有效模型[哈密顿量](@entry_id:172864)联系起来。

### [自旋密度泛函理论](@entry_id:755223)的基础

标准的[密度泛函理论](@entry_id:139027)（DFT）建立在霍恩伯格-科恩（Hohenberg-Kohn）定理之上，该定理证明了非简并[基态](@entry_id:150928)下，系统的所有性质都唯一地由其粒子[数密度](@entry_id:268986) $n(\mathbf{r})$ 决定。然而，对于[磁性材料](@entry_id:137953)，电子的自旋是至关重要的自由度。电荷密度 $n(\mathbf{r})$ 本身不足以完全描述一个自旋极化的系统。例如，一个铁磁体和一个顺磁体在没有外[磁场](@entry_id:153296)时可以具有非常相似的电荷密度[分布](@entry_id:182848)，但它们的磁性却截然不同。

为了解决这个问题，DFT被推广为**[自旋密度泛函理论](@entry_id:755223)（Spin-Density Functional Theory, SDFT）**。SDFT的基本变量不再是单一的标量场 $n(\mathbf{r})$，而是一个包含四个分量的集合：总粒子数密度 $n(\mathbf{r})$ 和三维的**自旋磁化密度（spin magnetization density）**矢量 $\mathbf{m}(\mathbf{r})$。从更基本的角度看，这些量可以被定义为一个 $2 \times 2$ 的[自旋密度](@entry_id:267742)矩阵 $n_{\alpha\beta}(\mathbf{r})$ 的分量。

在一个非相对论性的多电子系统中，我们可以利用[二次量子化](@entry_id:137766)的[场算符](@entry_id:140269) $\hat{\psi}_\alpha(\mathbf{r})$ 来形式化地定义这些核心变量，其中 $\alpha \in \{\uparrow, \downarrow\}$ 表示电子的[自旋投影](@entry_id:184359)。该算符在位置 $\mathbf{r}$ 湮灭一个自旋为 $\alpha$ 的电子。系统的[基态](@entry_id:150928)性质由[相关算符](@entry_id:152528)的[基态](@entry_id:150928)[期望值](@entry_id:153208)给出。

**粒子数密度（particle-number density）** $n(\mathbf{r})$ 是粒子数[密度算符](@entry_id:138151) $\hat{n}(\mathbf{r}) = \sum_{\alpha} \hat{\psi}^\dagger_\alpha(\mathbf{r}) \hat{\psi}_\alpha(\mathbf{r})$ 的[期望值](@entry_id:153208)：
$$
n(\mathbf{r}) = \langle \hat{n}(\mathbf{r}) \rangle = \sum_{\alpha} \langle \hat{\psi}^\dagger_\alpha(\mathbf{r}) \hat{\psi}_\alpha(\mathbf{r}) \rangle
$$
这可以被看作是自旋向上和自旋向下电子密度的总和，$n(\mathbf{r}) = n_\uparrow(\mathbf{r}) + n_\downarrow(\mathbf{r})$。

**自旋磁化密度（spin magnetization density）** $\mathbf{m}(\mathbf{r})$ 的定义则与系统如何与外[磁场](@entry_id:153296) $\mathbf{B}_{\mathrm{ext}}(\mathbf{r})$ 相互作用紧密相关。塞曼（Zeeman）相互作用能的形式为 $E_Z = \int d^3r\, \mathbf{B}_{\mathrm{ext}}(\mathbf{r}) \cdot \mathbf{m}(\mathbf{r})$。同时，从量子力学角度看，该能量是塞曼[哈密顿量](@entry_id:172864) $H_Z = -\int d^3r\, \hat{\boldsymbol{\mu}}(\mathbf{r}) \cdot \mathbf{B}_{\mathrm{ext}}(\mathbf{r})$ 的[期望值](@entry_id:153208)。其中，$\hat{\boldsymbol{\mu}}(\mathbf{r})$ 是[自旋磁矩](@entry_id:272337)[密度算符](@entry_id:138151)，它与[自旋密度](@entry_id:267742)算符 $\hat{\mathbf{s}}(\mathbf{r})$ 相关：$\hat{\boldsymbol{\mu}}(\mathbf{r}) = - \frac{g_s \mu_B}{\hbar} \hat{\mathbf{s}}(\mathbf{r})$。这里，$g_s \approx 2$ 是电子的自旋[g因子](@entry_id:153442)，$\mu_B$ 是[玻尔磁子](@entry_id:151037)。

通过比较这两种能量表达式，我们确定 $\mathbf{m}(\mathbf{r}) = -\langle \hat{\boldsymbol{\mu}}(\mathbf{r}) \rangle$。代入算符的定义，并利用[自旋密度](@entry_id:267742)算符 $\hat{\mathbf{s}}(\mathbf{r}) = \frac{\hbar}{2} \sum_{\alpha\beta} \hat{\psi}^\dagger_\alpha(\mathbf{r}) \boldsymbol{\sigma}_{\alpha\beta} \hat{\psi}_\beta(\mathbf{r})$（其中 $\boldsymbol{\sigma}$ 是泡利矩阵矢量），我们可以推导出 $\mathbf{m}(\mathbf{r})$ 的微观表达式：
$$
\mathbf{m}(\mathbf{r}) = \mu_B \sum_{\alpha\beta} \langle \hat{\psi}^\dagger_\alpha(\mathbf{r}) \hat{\psi}_\beta(\mathbf{r}) \rangle \boldsymbol{\sigma}_{\beta\alpha}
$$
这里我们引入了[自旋密度](@entry_id:267742)矩阵 $n_{\alpha\beta}(\mathbf{r}) = \langle \hat{\psi}^\dagger_\beta(\mathbf{r}) \hat{\psi}_\alpha(\mathbf{r}) \rangle$。利用这个矩阵，$n(\mathbf{r})$ 是其对角元素之和（迹），而 $\mathbf{m}(\mathbf{r})$ 则由其所有分量（对角和非对角）决定。

在许多情况下，比如简单的铁磁体或反铁磁体，我们可以假设所有局域自旋都沿着一个共同的全局轴（例如 $z$ 轴）对齐或反对齐。这就是**共线磁性（collinear magnetism）**近似。在这种情况下，自旋密度矩阵是对角的，非对角项 $n_{\uparrow\downarrow}(\mathbf{r})$ 和 $n_{\downarrow\uparrow}(\mathbf{r})$ 为零。磁化密度矢量也简化为一个[标量场](@entry_id:151443)乘以一个单位矢量 $\hat{\mathbf{e}}$：
$$
\mathbf{m}(\mathbf{r}) = \mu_B [n_\uparrow(\mathbf{r}) - n_\downarrow(\mathbf{r})] \hat{\mathbf{e}}
$$
因此，在共线近似下，SDFT的两个基本变量是两个独立的标量场：自旋向上密度 $n_\uparrow(\mathbf{r})$ 和自旋向下密度 $n_\downarrow(\mathbf{r})$。这与仅使用单一变量 $n(\mathbf{r})$ 的电荷密度泛函理论形成了鲜明对比，后者无法内在地描述自旋极化或磁有序现象。

### 共线磁性的[科恩-沈方程](@entry_id:143968)

SDFT的霍恩伯格-科恩-沈（Hohenberg-Kohn-Sham）框架旨在将一个相互作用的[自旋极化](@entry_id:164038)电子系统映射到一个更容易处理的、具有相同基态密度 $n_\uparrow(\mathbf{r})$ 和 $n_\downarrow(\mathbf{r})$ 的无相互作用[辅助系统](@entry_id:142219)。这个[辅助系统](@entry_id:142219)由一组单粒子薛定谔方程——即科恩-沈（Kohn-Sham, KS）方程——来描述。

在共线磁性近似下，自旋向上和自旋向下的电子是解耦的。这意味着我们可以为每个自旋通道（$\sigma \in \{\uparrow, \downarrow\}$）分别写下一个独立的KS方程。在[原子单位](@entry_id:166762)制（$\hbar = m_e = e = 4\pi\epsilon_0 = 1$）中，这些方程的形式如下：
$$
\left[-\frac{1}{2}\nabla^2 + v_{s,\sigma}(\mathbf{r})\right]\varphi_{i\sigma}(\mathbf{r}) = \varepsilon_{i\sigma}\varphi_{i\sigma}(\mathbf{r})
$$
这里，$\varphi_{i\sigma}(\mathbf{r})$ 是第 $i$ 个KS[轨道](@entry_id:137151)，其自旋为 $\sigma$，对应的本征能量为 $\varepsilon_{i\sigma}$。方程的核心是**自旋依赖的[有效势](@entry_id:142581)（spin-dependent effective potential）** $v_{s,\sigma}(\mathbf{r})$，它由三部分组成：
$$
v_{s,\sigma}(\mathbf{r}) = v(\mathbf{r}) + v_H(\mathbf{r}) + v_{xc,\sigma}(\mathbf{r})
$$

1.  **外势（External Potential） $v(\mathbf{r})$**：这是由[原子核](@entry_id:167902)和任何外部施加的[标量场](@entry_id:151443)（如[电场](@entry_id:194326)）产生的势。它与电子的[电荷](@entry_id:275494)耦合，因此对自旋向上和向下的电子是相同的。

2.  **哈特里势（Hartree Potential） $v_H(\mathbf{r})$**：这是由总电子密度 $n(\mathbf{r}) = n_\uparrow(\mathbf{r}) + n_\downarrow(\mathbf{r})$ 产生的经典静电势（平均场）。它通过泊松方程 $\nabla^2 v_H(\mathbf{r}) = -4\pi n(\mathbf{r})$ 确定，同样不依赖于自旋。

3.  **交换关联势（Exchange-Correlation Potential） $v_{xc,\sigma}(\mathbf{r})$**：这是SDFT的核心，包含了所有非经典的、多体的量子效应。至关重要的是，这个势是**自旋依赖的**。它形式上定义为交换关联[能量泛函](@entry_id:170311) $E_{xc}[n_\uparrow, n_\downarrow]$ 对相应自旋密度的泛函导数：
    $$
    v_{xc,\sigma}(\mathbf{r}) = \frac{\delta E_{xc}[n_\uparrow, n_\downarrow]}{\delta n_\sigma(\mathbf{r})}
    $$
    由于 $E_{xc}$ 本身依赖于 $n_\uparrow$ 和 $n_\downarrow$ 的相互关系，其对 $n_\uparrow$ 和 $n_\downarrow$ 的导数通常是不同的，即 $v_{xc,\uparrow}(\mathbf{r}) \neq v_{xc,\downarrow}(\mathbf{r})$。正是这种差异导致了自旋向上和向下电子感受到的[有效势](@entry_id:142581)不同，从而驱动了体系的[自旋极化](@entry_id:164038)。

一旦求解KS方程得到[轨道](@entry_id:137151) $\varphi_{i\sigma}$ 和[本征值](@entry_id:154894) $\varepsilon_{i\sigma}$，就可以根据[费米-狄拉克分布](@entry_id:138909)（在零温下为[阶梯函数](@entry_id:159192)）确定占据数 $f_{i\sigma}$，并反过来构建出[自旋密度](@entry_id:267742)：
$$
n_\sigma(\mathbf{r}) = \sum_i f_{i\sigma} |\varphi_{i\sigma}(\mathbf{r})|^2
$$
由于有效势 $v_{s,\sigma}$ 依赖于密度 $n_\sigma$，而密度又依赖于KS[轨道](@entry_id:137151)，这个过程必须迭代进行，直到势、[轨道](@entry_id:137151)和密度达到自洽。

### 磁性体系的交换关联泛函

KS-DFT的预测能力完全取决于交换关联（XC）[能量泛函](@entry_id:170311) $E_{xc}[n_\uparrow, n_\downarrow]$ 的准确性。与非磁性体系一样，对 $E_{xc}$ 的近似构成了一个被称为“[雅各布天梯](@entry_id:139901)”（Jacob's Ladder）的层次结构，每一级都引入更复杂的成分来提高精度。

- **局域[自旋密度](@entry_id:267742)近似（Local Spin Density Approximation, LSDA）**：这是最简单的一级近似。它假设在空间中的每一点 $\mathbf{r}$，XC能量密度只依赖于该点的[自旋密度](@entry_id:267742)值 $n_\uparrow(\mathbf{r})$ 和 $n_\downarrow(\mathbf{r})$。其函数形式取自具有相同常[数密度](@entry_id:268986)的[均匀电子气](@entry_id:163911)（HEG）的精确解。
    $$
    E_{xc}^{\text{LSDA}}[n_\uparrow, n_\downarrow] = \int d^3r\, n(\mathbf{r}) \varepsilon_{xc}^{\text{HEG}}(n_\uparrow(\mathbf{r}), n_\downarrow(\mathbf{r}))
    $$

- **[广义梯度近似](@entry_id:274118)（Generalized Gradient Approximation, GGA）**：为了超越LSDA的局域性，GGA在能量密度中额外引入了自旋密度的梯度 $\nabla n_\uparrow(\mathbf{r})$ 和 $\nabla n_\downarrow(\mathbf{r})$。这使得泛函能够感知电子密度的不均匀性，从而在描述原子、分子和固体时通常能提供比LSDA更高的准确性。

- **元[广义梯度近似](@entry_id:274118)（[meta-GGA](@entry_id:191648)）**：[meta-GGA](@entry_id:191648)在GGA的基础上更进一步，引入了与KS[轨道](@entry_id:137151)相关的半局域信息。最常见的成分是自旋分辨的动能密度：
    $$
    \tau_\sigma(\mathbf{r}) = \frac{1}{2} \sum_i^{\text{occ}} |\nabla \varphi_{i\sigma}(\mathbf{r})|^2
    $$
    $\tau_\sigma$ 能够区分不同类型的[化学键](@entry_id:138216)，并能满足更多已知的XC泛函精确约束，从而有望获得更高的精度。

为了更深入地理解交换作用的本质，一个重要的精确关系是**[交换能](@entry_id:137069)的自旋[标度关系](@entry_id:273705)（spin-scaling relation for exchange energy）**。交换作用源于[泡利不相容原理](@entry_id:141850)，它只发生在自旋相同的电子之间。因此，一个自旋极化体系的总[交换能](@entry_id:137069) $E_x[n_\uparrow, n_\downarrow]$ 应该是纯自旋向上电子云的[交换能](@entry_id:137069)与纯自旋向下电子云的[交换能](@entry_id:137069)之和。这个物理图像可以被精确地表述为以下关系：
$$
E_x[n_\uparrow, n_\downarrow] = \frac{1}{2} \left\{ E_x[2n_\uparrow] + E_x[2n_\downarrow] \right\}
$$
这里 $E_x[n]$ 指的是一个总密度为 $n$ 的无自旋极化体系（即 $n_\uparrow = n_\downarrow = n/2$）的[交换能](@entry_id:137069)泛函。这个关系式是所有XC泛函的交换部分都应满足的严格约束。值得注意的是，由于关联作用包含不同自旋电子间的相互作用，这个简单的标度关系并不适用于关联能 $E_c$ 或总的交换关联能 $E_{xc}$。

为了具体感受交换作用如何驱动磁性，我们可以考虑[均匀电子气](@entry_id:163911)模型。在哈特里-福克（[Hartree-Fock](@entry_id:142303)）近似下，可以精确推导出[交换能](@entry_id:137069)密度。对于一个总密度为 $n$、[自旋极化](@entry_id:164038)度为 $\zeta = (n_\uparrow - n_\downarrow)/n$ 的系统，其每个电子的平均交换能 $\epsilon_x$ 为：
$$
\epsilon_x(\zeta) = -\frac{3}{8\pi} (3\pi^2 n)^{1/3} \left[ (1+\zeta)^{4/3} + (1-\zeta)^{4/3} \right]
$$
通过分析这个表达式，我们可以比较两种极限情况：
- **顺磁态（paramagnetic state, $\zeta=0$）**: $\epsilon_x(0) = -\frac{3}{4\pi} (3\pi^2 n)^{1/3}$。
- **铁磁态（ferromagnetic state, $\zeta=1$）**: $\epsilon_x(1) = -2^{1/3} \frac{3}{4\pi} (3\pi^2 n)^{1/3} = 2^{1/3} \epsilon_x(0)$。
由于 $\epsilon_x(0)$ 是负值且 $2^{1/3} \approx 1.26 > 1$，我们发现 $\epsilon_x(1)  \epsilon_x(0)$。这意味着，仅考虑交换作用，完全[自旋极化](@entry_id:164038)的铁磁态比无极化的顺磁态能量更低。这个能量差为自发磁性的出现提供了基本的驱动力。然而，形成自旋极化需要将电子从一个自旋通道移动到另一个，这会增加系统的动能。一个稳定的铁磁态能否形成，取决于交换能的降低是否足以克服动能的增加。

### 巡游电子铁磁性的[斯通纳模型](@entry_id:137633)

上述交换能与动能之间的竞争，在巡游电子（itinerant electron）磁性的**[斯通纳模型](@entry_id:137633)（Stoner model）**中得到了简洁的阐述。该模型将金属中的[铁磁性](@entry_id:137256)视为[顺磁性](@entry_id:139883)费米液体在零温下的自发不稳定性。

[斯通纳模型](@entry_id:137633)的核心思想是，当一个[顺磁性](@entry_id:139883)金属发生微小的[自旋极化](@entry_id:164038)时，总能量会发生变化。能量变化包含两部分：一部分是动能的增加，另一部分是交换能的降低。
- **动能代价**：为了产生净磁矩，需要将一些电子从费米能级以下的某个自旋通道（例如，自旋向下）移动到费米能级以上的另一个自旋通道（自旋向上）。这个过程显然会增加系统的总动能。对于微小的磁化，$M$，动能代价近似为二次的，即 $\Delta E_{\text{kin}} \propto M^2 / N(E_F)$，其中 $N(E_F)$ 是[费米能级](@entry_id:143215)处的单自旋态密度。态密度越大，意味着在[费米能级](@entry_id:143215)附近有越多的态可供占据，从而以较小的能量代价实现电子的重新布局，即动能代价越小。
- **[交换能](@entry_id:137069)收益**：如前所述，自旋极化降低了[交换能](@entry_id:137069)。在[斯通纳模型](@entry_id:137633)中，这种效应被参数化为一个正比于磁化平方的能量收益，$\Delta E_{\text{xc}} \propto -I M^2$，其中 $I$ 是**斯通纳参数**，它反映了材料中交换关联相互作用的强度。

一个顺磁态的金属是否会自发地转变为铁磁态，取决于总能量变化 $\Delta E = \Delta E_{\text{kin}} + \Delta E_{\text{xc}}$ 的符号。当[交换能](@entry_id:137069)收益超过动能代价时，系统将通过[自发磁化](@entry_id:154730)来降低总能量。这个不稳定性发生的临界条件被称为**[斯通纳判据](@entry_id:145415)（Stoner criterion）**：
$$
I N(E_F) > 1
$$
这个简单而不失深刻的判据揭示了巡游电子[铁磁性](@entry_id:137256)的两个关键要素：
1.  **强的交换相互作用（大的 $I$）**：这由材料的内在化学成分和成键性质决定。在DFT的框架内，斯通纳参数 $I$ 可以被微观地解释为交换关联势的自旋劈裂 $\Delta V_{xc} = V_{xc}^\uparrow - V_{xc}^\downarrow$ 随磁化密度 $m = n_\uparrow - n_\downarrow$ 的初始变化率，$I \approx \partial \Delta V_{xc} / \partial m|_{m=0}$。
2.  **高的[费米能级态密度](@entry_id:204201)（大的 $N(E_F)$）**：这由材料的能带结构决定。通常，具有窄而尖锐的d带或f带穿过费米能级的金属（如Fe, Co, Ni等过渡金属，以及一些[重费米子体系](@entry_id:140736)）更容易满足[斯通纳判据](@entry_id:145415)。例如，对于一个简单的抛物线能带，[态密度](@entry_id:147894)与[有效质量](@entry_id:142879) $m^*$ 成正比，$N(E_F) \propto m^*$。因此，具有较大有效质量的电子（“重”电子）更容易驱动磁性。

### 超越标准DFT：[强关联体系](@entry_id:145791)与[DFT+U方法](@entry_id:748357)

尽管LSDA和GGA在描述许多金属和[半导体](@entry_id:141536)的电子结构方面取得了巨大成功，但它们在处理一类重要材料——**[强关联电子体系](@entry_id:183796)（strongly correlated electron systems）**——时常常会系统性地失败。这类材料的典型代表是含有部分填充的 $d$ 或 $f$ [电子壳层](@entry_id:270981)的过渡金属氧化物和稀土化合物。

标准DFT近似的主要缺陷在于**[自相互作用误差](@entry_id:139981)（self-interaction error, SIE）**。在一个精确的理论中，一个电子不应与它自身产生的势发生相互作用。然而，在LSDA和GGA中，哈特里项包含了一个电子与其自身平均电荷密度的 spurious 相互作用，而交换关联项只不完全地抵消了这一伪相互作用。对于巡游性较强的 $s$ 和 $p$ 电子，这个误差影响较小。但对于局域性很强的 $d$ 和 $f$ 电子，SIE变得非常严重。它会过度地使这些局域[轨道](@entry_id:137151)“[离域](@entry_id:183327)化”，即错误地倾向于形成分数占据的能带，而不是物理上正确的整数占据的局域态。

这种错误的离域化描述导致了两个典型的失败：
1.  **[能隙](@entry_id:191975)低估**：许多[强关联材料](@entry_id:198946)在实验上是具有大[带隙](@entry_id:191975)的绝缘体（所谓的莫特绝缘体或[电荷转移绝缘体](@entry_id:137636)），但LSDA/GGA计算常常错误地预测它们是金属或[带隙](@entry_id:191975)过小的[半导体](@entry_id:141536)。
2.  **磁矩低估**：[离域](@entry_id:183327)化倾向削弱了电子的局域特性，导致计算出的局域磁矩（原子位点上的净自旋）远小于实验值。

为了修正这一缺陷，**[DFT+U方法](@entry_id:748357)**被引入。这是一种混合方案，它在标准DFT计算的基础上，对选定的局域[轨道](@entry_id:137151)[子空间](@entry_id:150286)（如过渡金属的d轨道）额外施加一个源于哈伯德（Hubbard）模型的修正项。总能量泛函变为：
$$
E_{\text{DFT}+U} = E_{\text{DFT}} + E_U - E_{\text{DC}}
$$
- $E_U$ 是哈伯德修正项，它对局域[轨道](@entry_id:137151)引入了强烈的**[在位库仑排斥](@entry_id:269911)（on-site Coulomb repulsion）**。这个能量项惩罚了分数占据，使得总能量关于[轨道](@entry_id:137151)占据数的函数是凸的，从而驱动局域电子占据数趋向于整数，促进电子的局域化。
- $E_{\text{DC}}$ 是**双重计数（double-counting）**修正项，它用于减去已经由标准DFT部分（LSDA/GGA）近似包含的平均库仑相互作用，以避免重复计算。

[DFT+U方法](@entry_id:748357)通过以下机制改善了对[强关联体系](@entry_id:145791)的描述：
- **增强[自旋极化](@entry_id:164038)**：在自旋极化计算中，由于多数和少数自旋通道的占据数不同，哈伯德 $U$ 修正会产生一个强烈的、依赖于自旋和[轨道](@entry_id:137151)的势。这个势会显著增大多数和少数[自旋态](@entry_id:149436)之间的能量劈裂，从而稳定一个具有更大局域磁矩的[基态](@entry_id:150928)。
- **打开[能隙](@entry_id:191975)**：通过将占据的 $d$ 轨道能量向更低处推，未占据的 $d$ 轨道能量向更高处推，[DFT+U](@entry_id:142114)可以成功地打开一个[能隙](@entry_id:191975)。如果[能隙形成](@entry_id:265171)于占据的 $d$ 带（下哈伯德带）和未占据的 $d$ 带（上哈伯德带）之间，则称为**莫特-哈伯德（Mott-Hubbard）[能隙](@entry_id:191975)**。在许多氧化物中，氧的 $p$ 带能量位于金属的上下哈伯德带之间。在这种情况下，[DFT+U](@entry_id:142114)可能打开一个介于占据的氧 $p$ 带和未占据的金属 $d$ 带之间的[能隙](@entry_id:191975)，这被称为**电荷转移（charge-transfer）[能隙](@entry_id:191975)**。

### 超越共线磁性：[非共线磁性](@entry_id:181233)与自旋-轨道耦合

到目前为止，我们的讨论主要局限于磁矩处处平行的共线磁性。然而，自然界中存在大量磁序更为复杂的**[非共线磁性](@entry_id:181233)（noncollinear magnetism）**材料，例如螺旋磁体、自旋螺旋、[斯格明子](@entry_id:141088)（skyrmions）等。此外，即使在共线磁体中，要理解磁各向异性等现象，也必须考虑相对论效应。

处理这些复杂情况要求我们回到SDFT更普遍的形式，并引入相对论修正。这导致理论框架的两个关键推广：必须使用**双分量[旋量](@entry_id:158054)（two-component spinor）**的KS[轨道](@entry_id:137151)，并且有效势必须是一个**$2\times2$矩阵**。

这一推广的必要性可以从两个角度理解：

1.  **从SDFT的变分结构出发**：在非共线情况下，磁化密度 $\mathbf{m}(\mathbf{r})$ 是一个在空间中方向可以任意变化的矢量场。根据SDFT的变分原理，交换关联势是[能量泛函](@entry_id:170311)对密度变量的导数。对矢量场 $\mathbf{m}(\mathbf{r})$ 求导会产生一个矢量场——**交换关联[磁场](@entry_id:153296) $\mathbf{B}_{xc}(\mathbf{r})$**。这个内禀的[有效磁场](@entry_id:139861)会像外[磁场](@entry_id:153296)一样，通过塞曼项的形式与电子自旋耦合。因此，总的有效KS[哈密顿量](@entry_id:172864)中包含一项 $\mu_B \boldsymbol{\sigma} \cdot \mathbf{B}_{\text{eff}}(\mathbf{r})$，其中 $\mathbf{B}_{\text{eff}}$ 包含了外部场、[轨道](@entry_id:137151)场以及交换关联场。由于[泡利矩阵](@entry_id:139493) $\boldsymbol{\sigma}$ 的存在，这个[哈密顿量](@entry_id:172864)是一个 $2\times2$ 矩阵，其[本征态](@entry_id:149904)自然是双分量[旋量](@entry_id:158054)。

2.  **从[相对论量子力学](@entry_id:148643)出发**：描述电子的真正基本方程是[狄拉克方程](@entry_id:147922)。在非相对论极限下（对 $1/c^2$ 展开），可以得到泡利[哈密顿量](@entry_id:172864)。除了动能和势能项，这个[哈密顿量](@entry_id:172864)还包含了几个关键的相对论修正项。其中最重要的是**[自旋-轨道耦合](@entry_id:143520)（Spin-Orbit Coupling, SOC）**项：
    $$
    H_{\text{SO}} = \frac{\hbar}{4m^2c^2} (\nabla V \times \mathbf{p}) \cdot \boldsymbol{\sigma}
    $$
    其中 $V(\mathbf{r})$ 是晶体势，$\mathbf{p}$ 是动量算符。这个算符直接耦合了电子的自旋（$\boldsymbol{\sigma}$）和它在[晶格](@entry_id:196752)[电场](@entry_id:194326)（由 $\nabla V$ 体现）中的轨道运动（$\mathbf{p}$）。由于 $\boldsymbol{\sigma}$ 的存在，SOC是一个内在的 $2\times2$ 矩阵算符，它作用在双分量旋量[波函数](@entry_id:147440)上。

SOC的存在对电子结构有深远的影响：
- **自旋混合**：SOC[哈密顿量](@entry_id:172864)包含 $\sigma_x$ 和 $\sigma_y$ 项，它们在自旋向上/向下[基矢](@entry_id:199546)中是非对角的。这意味着自旋不再是一个[好量子数](@entry_id:262514)，KS[本征态](@entry_id:149904)会成为自旋向上和向下态的混合态。
- **避免交叉**：当两个具有不同自旋特性的能带在没有SOC时发生交叉，SOC的非对角项通常会打开一个[能隙](@entry_id:191975)，形成所谓的**避免交叉（avoided crossing）**。
- **动量依赖的自旋劈裂**：在缺乏空间[反演对称性](@entry_id:269948)的体系中（例如[晶体表面](@entry_id:195760)或某些[非中心对称晶体](@entry_id:162159)），SOC可以导致能带的自旋劈裂，即使在没有外[磁场](@entry_id:153296)或磁有序的情况下也是如此。一个著名的例子是在表面产生的**[拉什巴效应](@entry_id:140786)（Rashba effect）**，其[哈密顿量](@entry_id:172864)形式为 $H_R \propto (\mathbf{k} \times \boldsymbol{\sigma}) \cdot \hat{\mathbf{n}}$，导致能带沿特定动量方向发生劈裂。
- **[磁晶各向异性](@entry_id:144488)（Magnetocrystalline Anisotropy）**：SOC将[电子自旋](@entry_id:137016)耦合到[晶格](@entry_id:196752)（通过势场 $V$），这意味着系统的总能量会依赖于磁化方向相对于[晶格](@entry_id:196752)轴的方向。这种能量差异就是[磁晶各向异性](@entry_id:144488)，它是永磁材料[矫顽力](@entry_id:159399)的微观来源。

### 从第一性原理到模型[哈密顿量](@entry_id:172864)：[海森堡模型](@entry_id:139958)的映射

尽管DFT计算能够提供关于磁性材料[电子结构](@entry_id:145158)的详尽信息，但它们通常局限于零温下的特定磁构型，且计算成本高昂。为了研究有限温度下的[磁相变](@entry_id:139255)、[磁激发](@entry_id:161593)（如[磁振子](@entry_id:139809)）或大尺度[磁织构](@entry_id:751636)，物理学家们常常采用更简单的有效自旋模型，其中最著名的就是**[海森堡模型](@entry_id:139958)（Heisenberg model）**。

其经典形式的[哈密顿量](@entry_id:172864)为：
$$
H = - \sum_{i \neq j} J_{ij} \mathbf{S}_i \cdot \mathbf{S}_j
$$
这里，$\mathbf{S}_i$ 是位于[晶格](@entry_id:196752)格点 $i$ 上的经典自旋矢量（通常假定为单位矢量），$J_{ij}$ 是格点 $i$ 和 $j$ 之间的**[交换相互作用](@entry_id:140006)参数**。如果 $J_{ij} > 0$，则铁磁[排列](@entry_id:136432)（自旋平行）能量更低；如果 $J_{ij}  0$，则反铁磁[排列](@entry_id:136432)（自旋反平行）能量更低。

一个关键的挑战是如何从[第一性原理计算](@entry_id:198754)中为特定材料确定这些交换参数 $J_{ij}$。一种广泛使用的方法是能量映射法。其基本思想是，通过DFT计算一系列不同磁构型（如铁磁、不同类型的反铁磁、自旋螺旋等）的总能量，然后将这些能量值拟合到[海森堡模型](@entry_id:139958)的能量表达式中，从而解出 $J_{ij}$。

例如，对于一个只有最近邻相互作用 $J_1$ 的简[立方晶格](@entry_id:148452)（最近邻数 $z_1=6$），铁磁态（FM）和奈尔型反铁磁态（AFM）的能量（每个原子）分别为：
- $E_{\text{FM}} = E_0 - 3J_1 S^2$
- $E_{\text{AFM}} = E_0 + 3J_1 S^2$
其中 $E_0$ 是一个与构型无关的能量常数 (如果 $S=1$ 则 $S^2$ 可省略)。因此，我们可以通过计算这两种构型的DFT能量差来提取 $J_1$：
$$
J_1 S^2 = \frac{E_{\text{AFM}} - E_{\text{FM}}}{6}
$$
我们可以通过计算第三种构型（例如一个特定的自旋螺旋）的能量来检验这个模型的有效性。如果仅包含最近邻相互作用的[海森堡模型](@entry_id:139958)预测的能量与DFT直接计算的能量不符，这通常表明存在不可忽略的更远邻相互作用（$J_2, J_3, \dots$）或更复杂的非海森堡相互作用。

将第一性原理的巡游电[子图](@entry_id:273342)像映射到局域矩的[海森堡模型](@entry_id:139958)，依赖于一系列重要假设，这些假设的失效是该映射方法的主要误差来源：
- **刚性自旋近似**：[海森堡模型](@entry_id:139958)假设每个格点上的自旋矩大小是固定的。然而，在巡游磁体中，局域磁矩的大小（纵向涨落）可以随其取向和周围环境而变化。忽略这种**纵向涨落**（或幅度软化）在弱铁磁体中尤其成问题，因为它会高估维持非共线构型所需的能量，从而导致对 $J_{ij}$ 的高估。
- **[绝热近似](@entry_id:143074)**：该映射假设自旋的运动非常缓慢，以至于电子总能保持在其瞬时[基态](@entry_id:150928)。
- **非海森堡相互作用**：真实的相互作用可能比简单的[双线性](@entry_id:146819)标积 $\mathbf{S}_i \cdot \mathbf{S}_j$ 更复杂。例如，**双二次交换（biquadratic exchange）** $(\mathbf{S}_i \cdot \mathbf{S}_j)^2$ 和多自旋相互作用在某些具有特殊[费米面](@entry_id:137798)特征（如嵌套）或[近简并](@entry_id:172107)能带的体系中可能变得很重要。
- **计算方法的近似**：提取 $J_{ij}$ 的具体方法本身也包含近似。例如，基于**磁力[微扰理论](@entry_id:138766)（Magnetic Force Theorem）**的方法依赖于非自洽的能带能量差，这在靠近[斯通纳不稳定性](@entry_id:157501)时可能引入显著误差。
- **自旋-轨道耦合**：忽略SOC会遗漏各向异性交换作用，如反对称的**贾洛申斯基-莫里亚相互作用（Dzyaloshinskii-Moriya interaction）**，它对稳定非共线手性磁结构至关重要。此外，SOC也会对各向同性的 $J_{ij}$ 值本身产生修正。

尽管存在这些限制，从DFT到[海森堡模型](@entry_id:139958)的映射仍然是连接微观电子结构和宏观磁现象的强大而不可或缺的工具，前提是研究者对其[适用范围](@entry_id:636189)和潜在的误差来源有清晰的认识。