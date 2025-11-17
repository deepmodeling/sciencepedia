## 引言
[密度泛函理论](@entry_id:139027)（DFT）是当代计算材料科学、[量子化学](@entry_id:140193)和凝聚态物理中最为重要和应用最广泛的工具之一。它在原子尺度上连接了电子结构与宏观物质性质，使得我们能够从第一性原理出发，预测和理解材料的力学、电子、磁学及化学性质。然而，对于多电子体系，直接求解薛定谔方程在计算上是不可行的。DFT通过将问题巧妙地重新表述为依赖于更简单的电子密度函数，为这一挑战提供了优雅而强大的解决方案，但其核心的交换关联泛函的精确形式未知，构成了理论与实践之间的关键知识鸿沟。

本文旨在系统性地引导读者深入理解DFT的精髓。我们将首先在“原理与机制”一章中，详细拆解其理论基础和核心的[Kohn-Sham方法](@entry_id:263733)。接着，在“应用与交叉学科联系”一章中，我们将展示DFT如何在材料物理、化学等领域解决实际问题，揭示其强大的预测能力与内在局限。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识转化为解决问题的实践技能。

## 原理与机制

本章旨在深入探讨[密度泛函理论](@entry_id:139027) (Density Functional Theory, DFT) 的核心原理与关键机制。我们将从其坚实的理论基础出发，逐步解析将这一理论付诸实践的 Kohn-Sham 方法，并探讨目前广泛应用的交换关联泛函近似。此外，我们还将审视标准 DFT 近似所面临的挑战，如[自相互作用](@entry_id:201333)错误和对[长程相互作用](@entry_id:140725)的描述不善，并介绍为克服这些局限性而发展的先进方法，包括 [DFT+U](@entry_id:142114) 和[色散](@entry_id:263750)修正。最后，本章将内容延伸至固体计算的实际技术考量以及 DFT 框架在有限温度和电子激发态领域的扩展。

### DFT 的基本定理：Hohenberg-Kohn 定理

[密度泛函理论](@entry_id:139027)的理论基石由 Hohenberg-Kohn (HK) 定理奠定，这两个定理从根本上重塑了我们对多电子体系[量子态](@entry_id:146142)的理解。它们将体系的[基态](@entry_id:150928)性质与电子密度——一个仅依赖于三个空间坐标的函数——直接关联起来，而非依赖于极其复杂的、包含所有电子坐标的[多体波函数](@entry_id:203043)。

第一个 HK 定理是一个[存在性定理](@entry_id:261096)。它断言，对于一个由外部势 $v(\mathbf{r})$ 所描述的非简并[基态](@entry_id:150928)体系，其[基态](@entry_id:150928)电子密度 $n_0(\mathbf{r})$ 唯一地确定了该外部势（相差一个无关紧要的常数）。由于外部势 $v(\mathbf{r})$ 与[哈密顿算符](@entry_id:144286)之间存在一一对应关系（对于给定的电子数 $N$），这意味着基[态密度](@entry_id:147894) $n_0(\mathbf{r})$ 唯一地确定了体系的完整[哈密顿量](@entry_id:172864)，并因此确定了体系的所有性质，包括[基态](@entry_id:150928)[波函数](@entry_id:147440)和总能量。

这一定理的深刻含义在于，体系的[基态](@entry_id:150928)总能量可以表示为电子密度的泛函：
$E[n] = F[n] + \int v(\mathbf{r})n(\mathbf{r}) d^3\mathbf{r}$

其中，$F[n]$ 是一个**[普适泛函](@entry_id:140176)**，它仅依赖于电子密度 $n(\mathbf{r})$，而与具体的外部势 $v(\mathbf{r})$ 无关。这个[普适泛函](@entry_id:140176)包含了电子的动能 $T[n]$ 以及[电子-电子相互作用](@entry_id:139900)能 $V_{ee}[n]$。不幸的是，尽管我们知道 $F[n]$ 存在，但它的精确形式对于多电子体系是未知的。

第二个 HK 定理引入了[变分原理](@entry_id:198028)。它指出，对于一个给定的外部势 $v(\mathbf{r})$，正确的[基态能量](@entry_id:263704) $E_0$ 是通过在所有满足条件的密度（$N$-representable densities）中最小化总能量泛函 $E[n]$ 得到的。即：
$E_0 = \min_{n} E[n] = \min_{n} \left( F[n] + \int v(\mathbf{r})n(\mathbf{r}) d^3\mathbf{r} \right)$

任何试验密度 $n'(\mathbf{r})$（不等于基[态密度](@entry_id:147894) $n_0(\mathbf{r})$）代入能量泛函，所得到的能量 $E[n']$ 必定高于或等于真实的基态能量 $E_0$。

我们可以通过一个单电子体系的简化模型来具体理解这些概念 [@problem_id:2813508]。考虑一个在一维谐振子势 $v(x) = \frac{1}{2}\omega^2 x^2$ 中的单个电子。对于单电子体系，不存在[电子-电子相互作用](@entry_id:139900)，因此[普适泛函](@entry_id:140176) $F[n]$仅包含动能项 $T[n]$。其总[能量泛函](@entry_id:170311)为 $E[n] = T[n] + \int v(x)n(x) dx$。对于一个实数、非负的[基态](@entry_id:150928)[轨道](@entry_id:137151)，[波函数](@entry_id:147440) $\psi(x)$ 与密度 $n(x)$ 的关系为 $\psi(x) = \sqrt{n(x)}$。利用这一关系，我们可以将标准的动能[期望值](@entry_id:153208) $T[\psi] = \frac{1}{2} \int (\frac{d\psi}{dx})^2 dx$（采用[原子单位](@entry_id:166762)）精确地重写为密度的泛函：
$T[n] = \frac{1}{8} \int_{-\infty}^{\infty} \frac{(n'(x))^2}{n(x)} dx$
这个表达式被称为 **von Weizsäcker 动能泛函**，它对任何单电子体系都是精确的。因此，该谐振子模型的精确总能量泛函为：
$E[n] = \frac{1}{8} \int_{-\infty}^{\infty} \frac{(n'(x))^2}{n(x)} dx + \frac{1}{2}\omega^2 \int_{-\infty}^{\infty} x^2 n(x) dx$

根据第二个 HK 定理，我们可以通过在一个试验密度族 $n_\alpha(x)$ 中最小化 $E[n]$ 来获得[基态能量](@entry_id:263704)的上限。例如，使用一个归一化的[高斯密度](@entry_id:199706)族 $n_{\alpha}(x) = \sqrt{\frac{\alpha}{\pi}}\exp(-\alpha x^2)$，通过计算上述积分并将能量 $E(\alpha)$ 对参数 $\alpha$ 求极小值，我们可以找到最佳近似。对于这个特定的例子，由于[高斯函数](@entry_id:261394)是[谐振子](@entry_id:155622)的精确[基态](@entry_id:150928)解，这个过程最终能够精确地得到[基态能量](@entry_id:263704) $E_0 = \omega/2$ [@problem_id:2813508]。这个例子清晰地展示了 HK 定理的变分原理如何通过密度泛函进行操作。

### Kohn-Sham 方法：从相互作用体系到非相互作用体系的映射

尽管 HK 定理在理论上极为优雅，但[普适泛函](@entry_id:140176) $F[n]$ 的未知形式，特别是其中复杂的动能项 $T[n]$，使其难以直接应用。Kohn-Sham (KS) 方法通过一个巧妙的构想解决了这一难题。其核心思想是，引入一个**虚构的非相互作用电子体系**，该体系的基态密度与我们感兴趣的真实相互作用体系的基態密度完全相同。

对于非相互作用体系，动能可以精确地写成其单粒子[轨道](@entry_id:137151) $\psi_i$ 的函数：
$T_s[n] = \sum_{i=1}^{N} \int \psi_i^*(\mathbf{r}) \left( -\frac{1}{2}\nabla^2 \right) \psi_i(\mathbf{r}) d^3\mathbf{r}$
其中，电子密度由这些 KS [轨道](@entry_id:137151)给出：$n(\mathbf{r}) = \sum_{i=1}^{N} |\psi_i(\mathbf{r})|^2$。

有了这个精确的非相互作用动能 $T_s[n]$，我们可以将真实体系的[普适泛函](@entry_id:140176) $F[n]$ 重新划分为三个部分：
$F[n] = T_s[n] + E_H[n] + E_{xc}[n]$

1.  **$T_s[n]$**：非相互作用电子体系的动能。这是真实体系动能的主要部分。
2.  **$E_H[n]$**：**Hartree 能量**，即电子密度[分布](@entry_id:182848)的经典静电自排斥能。
    $E_H[n] = \frac{1}{2} \int \int \frac{n(\mathbf{r})n(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} d^3\mathbf{r} d^3\mathbf{r}'$
3.  **$E_{xc}[n]$**：**交换关联 (exchange-correlation, xc) 能量**。这是一个“万能”项，它包含了所有剩余的复杂量子效应，包括：
    *   真实动能与非相互作用动能之差 ($T[n] - T_s[n]$)。
    *   超出经典 Hartree 排斥的所有非经典[电子-电子相互作用](@entry_id:139900)（即交换效应和关联效应）。

至此，真实相互作用体系的总能量泛函变为：
$E[n] = T_s[n] + E_H[n] + E_{xc}[n] + \int v_{ext}(\mathbf{r})n(\mathbf{r}) d^3\mathbf{r}$

对这个能量泛函关于 KS [轨道](@entry_id:137151) $\psi_i^*$ 应用[变分原理](@entry_id:198028)，同时保持其正交归一性，便可导出一组类似于单电子 Schrödinger 方程的方程，即 **Kohn-Sham 方程**：
$\left( -\frac{1}{2}\nabla^2 + v_{eff}(\mathbf{r}) \right) \psi_i(\mathbf{r}) = \varepsilon_i \psi_i(\mathbf{r})$

这里的**[有效势](@entry_id:142581)** $v_{eff}(\mathbf{r})$ 对所有电子都是相同的，它由四部分组成：
$v_{eff}(\mathbf{r}) = v_{ext}(\mathbf{r}) + v_H(\mathbf{r}) + v_{xc}(\mathbf{r})$

其中，$v_{ext}(\mathbf{r})$ 是外部势（例如[原子核](@entry_id:167902)的吸引势），$v_H(\mathbf{r}) = \int \frac{n(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} d^3\mathbf{r}'$ 是 Hartree 势，而**交换关联势** $v_{xc}(\mathbf{r})$ 是交换关联能量 $E_{xc}[n]$ 对密度的**泛函导数**：
$v_{xc}(\mathbf{r}) = \frac{\delta E_{xc}[n]}{\delta n(\mathbf{r})}$

KS 方法的流程是自洽的：从一个初始的密度猜测 $n(\mathbf{r})$ 出发，计算出 $v_{eff}(\mathbf{r})$，然后求解 KS 方程得到一组新的 KS [轨道](@entry_id:137151) $\psi_i$，再由这些[轨道](@entry_id:137151)构造出新的密度。这个过程不断迭代，直到密度收敛为止。

### 交换关联泛函的近似：“Jacob之梯”

KS 方法的 brilliance 在于它将求解[多体问题](@entry_id:138087)的困难（寻找精确的 $T[n]$）转化为了另一个同样困难但更易于近似的问题：寻找精确的 $E_{xc}[n]$。DFT 的发展很大程度上就是构造越来越精确的交换关联泛函的历史。这些近似通常被比喻为“Jacob之梯”，每一级都比前一级更复杂、更精确，但计算成本也更高。

#### 第一级：局域密度近似 (LDA)

**局域密度近似 (Local Density Approximation, [LDA](@entry_id:138982))** 是最简单也是最早的近似。它的核心思想是假设在空间中的每一点 $\mathbf{r}$，非[均匀电子气](@entry_id:163911)的交换关联能量密度 $\varepsilon_{xc}(n(\mathbf{r}))$ 与具有相同密度的**[均匀电子气](@entry_id:163911) (homogeneous electron gas, HEG)** 的交换关联能量密度相同。HEG 是一个理想化的模型，其电子密度处处恒定，其 $\varepsilon_{xc}^{HEG}(n)$ 可以通过[量子蒙特卡洛](@entry_id:144383)等方法精确计算。

因此，LDA 的总交换关联能为：
$E_{xc}^{LDA}[n] = \int n(\mathbf{r}) \varepsilon_{xc}^{HEG}(n(\mathbf{r})) d^3\mathbf{r}$

我们可以更具体地考察仅包含交换部分的 LDA（有时称为 Slater exchange） [@problem_id:2813517]。对于自旋非极化的 HEG，其交换能密度为 $\varepsilon_x(n) = C_x n^{4/3}$，其中 $C_x = -\frac{3}{4}(\frac{3}{\pi})^{1/3}$ 是一个[普适常数](@entry_id:165600)。于是，[LDA](@entry_id:138982) [交换能](@entry_id:137069)泛函为：
$E_x^{LDA}[n] = \int C_x n(\mathbf{r})^{4/3} d^3\mathbf{r}$

相应的[交换势](@entry_id:749153) $v_x(n)$ 是能量密度对密度的普通导数：
$v_x^{LDA}(n(\mathbf{r})) = \frac{d\varepsilon_x(n)}{dn}\Big|_{n=n(\mathbf{r})} = \frac{4}{3} C_x n(\mathbf{r})^{1/3}$

LDA 在描述[键长](@entry_id:144592)、[振动频率](@entry_id:199185)等方面出人意料地成功，尤其是在电子密度变化缓慢的体系中。然而，它系统性地高估了结合能，并低估了[能隙](@entry_id:191975)。

#### 第二级：[广义梯度近似 (GGA)](@entry_id:140295)

为了超越 LDA 的局域性限制，**[广义梯度近似](@entry_id:274118) (Generalized Gradient Approximations, GGA)** 被提出。GGA 不仅考虑了某一点的电子密度 $n(\mathbf{r})$，还考虑了该点密度的**梯度** $|\nabla n(\mathbf{r})|$，从而 incorporating 了关于密度变化快慢的信息。

GGA 泛函的一般形式为：
$E_{xc}^{GGA}[n] = \int f(n(\mathbf{r}), |\nabla n(\mathbf{r})|) d^3\mathbf{r}$

其中 $f$ 是一个精心设计的函数。与 LDA 不同，GGA 的交换关联势需要通过泛函导数的一般形式（Euler-Lagrange方程）来计算。对于一个依赖于 $n$ 和 $\nabla n$ 的能量密度 $e_{xc}(n, \nabla n)$，其泛函导数为 [@problem_id:2813511]：
$v_{xc}(\mathbf{r}) = \frac{\partial e_{xc}}{\partial n} - \nabla \cdot \left( \frac{\partial e_{xc}}{\partial \nabla n} \right)$

例如，考虑一个假想的半局域泛函模型 $E_{xc}[n] = \int [-C_x n^{4/3} + \beta \frac{|\nabla n|^2}{n}] d^3\mathbf{r}$。第一项是 LDA 交换项，第二项是梯度修正项。通过应用上述泛函导数公式，可以推导出对应的 $v_{xc}(\mathbf{r})$ 表达式。这个过程展示了如何从一个给定的 GGA [能量泛函](@entry_id:170311)解析地推导出其[势函数](@entry_id:176105) [@problem_id:2813511]。流行的 GGA 泛函（如 PBE, BLYP）通过满足已知的交换关联泛函的精确约束来构造，显著改善了对[结合能](@entry_id:143405)、[表面能](@entry_id:161228)和分子几何的描述。

### 标准近似的挑战与修正

尽管 LDA 和 GGA 取得了巨大成功，但它们在处理某些物理现象时仍存在系统性的缺陷。理解这些缺陷对于高级应用至关重要。

#### 自相互作用错误 (SIE)

一个理想的交换关联泛函应该能确保一个电子不会与自身发生相互作用。在精确的理论中，一个单电子体系的 Hartree 能量（电子与其自身密度场的[静电能](@entry_id:267406)）应该被[交换能](@entry_id:137069)量完全抵消。即对于单电子密度 $n_{1e}$，$E_H[n_{1e}] + E_x[n_{1e}] = 0$。

然而，LDA 和 GGA 等近似泛函并不满足这个条件。它们会产生一个虚假的、非零的**自相互作用能 (self-interaction energy, SIE)**。我们可以通过一个氢原子（或[类氢离子](@entry_id:174450)，[电荷](@entry_id:275494)为 Z）的例子来量化这一错误 [@problem_id:2813500]。对于一个 1s 电子，密度为 $n(\mathbf{r}) = (Z^3/\pi)\exp(-2Zr)$。我们可以精确计算其 Hartree 能量 $E_H[n]$ 和 LSDA 交换能 $E_x^{LSDA}[n]$。计算结果表明，$E_H[n] = \frac{5}{16}Z$，而 $E_x^{LSDA}[n]$ 是一个与 $Z$ 成正比的负值。它们的和 $E_{SIE} = E_H[n] + E_x^{LSDA}[n]$ 并不为零，这个残余的能量就是自相互作用错误。

SIE 的一个重要后果是**离域错误**。由于电子能感受到一部分自身产生的[排斥势](@entry_id:185622)，它倾向于将自己的[波函数](@entry_id:147440)“摊开”以降低能量，导致电子态过于[离域](@entry_id:183327)。这在描述含 $d$ 或 $f$ 电子的[强关联材料](@entry_id:198946)（如过渡金属氧化物）时尤其成问题，往往导致错误的金属性预测。

#### [强关联体系](@entry_id:145791)与 [DFT+U](@entry_id:142114)

为了修正 LDA/GGA 对[强关联体系](@entry_id:145791)的描述失败，**[DFT+U](@entry_id:142114)** 方法被引入。它是一种在标准 DFT 计算之上附加一个 Hubbard-like on-site 修正项的 pragmatic 方法。这个修正项专门作用于局域化的原子轨道[子空间](@entry_id:150286)（如 $d$ 或 $f$ [轨道](@entry_id:137151)）。

该修正能量的设计遵循几个原则：它必须在局域基的幺正变换下保持[旋转不变性](@entry_id:137644)，并且只惩罚分数占据的[轨道](@entry_id:137151)。一个满足这些条件的简单而有效的形式是 Dudarev 提出的 [@problem_id:2813509]：
$E_U = \frac{U_{eff}}{2} \sum_{\sigma \in \{\uparrow, \downarrow\}} \left[ \mathrm{Tr}(\mathbf{n}^\sigma) - \mathrm{Tr}((\mathbf{n}^\sigma)^2) \right]$

其中，$U_{eff}$ 是有效的 on-site 相互作用参数，$\mathbf{n}^\sigma$ 是在局域[轨道](@entry_id:137151)基上投影得到的自旋为 $\sigma$ 的占据数矩阵。$\mathrm{Tr}(\mathbf{n}^\sigma)$ 是该自旋通道的总占据数。$\mathrm{Tr}((\mathbf{n}^\sigma)^2)$ 可以看作占据数的“純度”度量。当[轨道](@entry_id:137151)被整数占据（0 或 1）时，$\mathbf{n}^\sigma$ 是一个[幂等矩阵](@entry_id:188272)（$(\mathbf{n}^\sigma)^2 = \mathbf{n}^\sigma$），此时 $\mathrm{Tr}(\mathbf{n}^\sigma) = \mathrm{Tr}((\mathbf{n}^\sigma)^2)$，修正能 $E_U$ 为零。当[轨道](@entry_id:137151)被分数占据时，$\mathrm{Tr}(\mathbf{n}^\sigma) > \mathrm{Tr}((\mathbf{n}^\sigma)^2)$，修正能为一个正值，从而惩罚了由 SIE 导致的非物理性分数占据，促使电子态更加局域化。这个方法的[旋转不变性](@entry_id:137644)可以通过矩阵[迹的循环性质](@entry_id:153103)得到证明 [@problem_id:2813509]。

#### 范德华斯 (van der Waals) 相互作用

另一个重大挑战是描述分子间或层状材料间的长程**范德华斯 (van der Waals, vdW) 色散力**。这些力源于瞬时[偶极-偶极相互作用](@entry_id:144039)，是一种非局域的电子关联效应。由于 LDA 和 GGA 的构造依赖于局域或半局域的密度信息，它们本质上无法捕捉这种长程物理。

从更根本的[绝热连接涨落-耗散定理](@entry_id:192440) (Adiabatic Connection Fluctuation-Dissipation Theorem, ACFDT) 出发，可以推导出两个相距为 $R$ 的可极化片段 A 和 B 之间的[色散能](@entry_id:261481)渐近形式为 $E_{disp} \approx -C_6/R^6$ [@problem_id:2813503]。其中，$C_6$ 系数由两个片段在[虚频](@entry_id:165180)轴上的频率依赖偶极极化率 $\alpha(i\omega)$ 决定：
$C_6 = \frac{3}{\pi} \int_0^\infty d\omega \alpha_A(i\omega) \alpha_B(i\omega)$

使用简单的 Drude [振子](@entry_id:271549)模型 $\alpha(i\omega) = \frac{\alpha_0}{1+(\omega/\omega_0)^2}$ 来近似[极化率](@entry_id:143513)，可以解析地得到 $C_6$ 系数。这揭示了[色散力](@entry_id:153203)与材料的动态响应特性之间的深刻联系。实用的[色散](@entry_id:263750)修正常常采用经验性方法，将形如 $-f(R)C_6/R^6$ 的成对原子间[相互作用项](@entry_id:637283)添加到 DFT 总能量中。其中 $f(R)$ 是一个**阻尼函数**，例如 Tang-Toennies 阻尼函数，用于在短程范围内消除 $-C_6/R^6$ 项的非物理性奇异行为，确保其只在长程起作用 [@problem_id:2813503]。

### 固体计算中的实践问题

将 DFT 应用于周期性晶体时，需要考虑一些特定的技术细节。

#### 布里渊区取样与涂抹

根据 Bloch 定理，晶体中电子的[波函数](@entry_id:147440)是扩展的 Bloch 波，由[晶格动量](@entry_id:143609)（或[波矢](@entry_id:178620)）$k$ 标记。总能量等性质需要通过在[倒易空间](@entry_id:754151)的第一**[布里渊区](@entry_id:142395) (Brillouin zone, BZ)** 内对所有占据态进行积分来获得。在数值计算中，这个连续积分被一个在 BZ 内的离散 $k$ 点网格上的求和所替代 [@problem_id:2813505]。

对于绝缘体和[半导体](@entry_id:141536)，价带被完全占据，导带完全为空，因此用有限的 $k$ 点网格进行求和通常收敛得很快。然而，对于金属，[费米能级](@entry_id:143215)横穿一个或多个能带，导致占据数在[费米面](@entry_id:137798)上有一个 sharp 的阶跃。用稀疏的 $k$ 点网格来近似这个不连续的阶跃函数会导致数值不稳定和缓慢的收敛。

为了解决这个问题，引入了**涂抹 (smearing)** 技术。它通过一个光滑的函数（如 Fermi-Dirac [分布](@entry_id:182848)或[高斯函数](@entry_id:261394)）来近似 $T=0$ K 时的阶跃占据函数。例如，Fermi-Dirac 占据函数为：
$f(\varepsilon, \mu, T) = \frac{1}{1 + \exp\left(\frac{\varepsilon - \mu}{k_B T}\right)}$
这里的温度 $T$ 通常被视为一个数值参数（涂抹宽度 $\sigma$），而非真实的物理温度。对于给定的电子数，化学势 $\mu$ 必须通过求解粒子数守恒方程来确定。涂抹技术极大地提高了金属体系总能量计算的收敛速度 [@problem_id:2813505]。

#### [基组](@entry_id:160309)与 Pulay 力

在实际计算中，Kohn-Sham [轨道](@entry_id:137151)需要在一个有限的**[基组](@entry_id:160309)**中展开。常用的[基组](@entry_id:160309)包括[平面波](@entry_id:189798)和局域[原子轨道](@entry_id:140819)（如高斯型或数值[原子轨道](@entry_id:140819)）。当使用随原子移动的局域[原子轨道](@entry_id:140819)[基组](@entry_id:160309)时，会产生一个微妙但重要的效应。

当计算[原子核](@entry_id:167902)上的力以进行[几何优化](@entry_id:151817)或分子动力学模拟时，总能量对[原子核](@entry_id:167902)坐标 $R$ 的导数不仅包含哈密顿矩阵 $H$ 的显式依赖（Hellmann-Feynman 力），还包含因[基函数](@entry_id:170178)本身依赖于原子位置而产生的额外项。这个额外项被称为 **Pulay 力**或 Pulay 修正 [@problem_id:2813514]。

对于一个非正交的、依赖于原子位置的[基组](@entry_id:160309)，其[重叠矩阵](@entry_id:268881) $S$ 不再是[单位矩阵](@entry_id:156724)且依赖于 $R$。通过对总能量表达式 $\varepsilon = c^T H c$（在 $c^T S c = 1$ 的[归一化条件](@entry_id:156486)下）求导，可以推导出总力为：
$F = -\frac{d\varepsilon}{dR} = -c^T\left(\frac{\partial H}{\partial R}\right)c + \varepsilon c^T\left(\frac{\partial S}{\partial R}\right)c$

第一项是 Hellmann-Feynman 力，而第二项就是 Pulay 力。它与[基组](@entry_id:160309)的不完备性有关，因为在一个完备的[基组](@entry_id:160309)中，[波函数](@entry_id:147440)的任何变化都可以由系数 $c$ 的变化来完全描述。忽略 Pulay 力会导致错误的力和不正确的平衡几何。

### DFT 框架的扩展

DFT 的基本思想还可以扩展到描述[基态](@entry_id:150928)之外的物理情景。

#### 有限温 DFT

Mermin 在 1965 年将 HK 定理推广到有限温度 $T>0$ 的场景。其核心思想是将变分原理应用于 grand canonical potential $\Omega = E - TS - \mu N$，而不是总能量 $E$。在这种框架下，KS 体系的粒子占据数遵循**Fermi-Dirac [分布](@entry_id:182848)** [@problem_id:2813504]。该[分布](@entry_id:182848)可以通过最大化 von Neumann 熵 $S = -k_B \sum_i [f_i \ln f_i + (1-f_i)\ln(1-f_i)]$，同时保持[平均粒子数](@entry_id:151202)和平均能量不变，通过 Lagrange [乘子法](@entry_id:170637)推导得出。有限温 DFT 对于研究材料在真实工作条件下的[相变](@entry_id:147324)、热力学性质等至关重要。

#### [激发态](@entry_id:261453)与 TDDFT

原则上，DFT 是一个基態理论。然而，通过**时变密度泛函理论 (Time-Dependent DFT, TDDFT)**，我们可以研究体系对时变外场的响应，从而获取电子激发态的信息。TDDFT 的基础是 Runge-Gross 定理，它将时变密度与时变外场[一一对应](@entry_id:143935)起来。

在[线性响应理论](@entry_id:145737)的框架下，可以推导出计算体系[激发能](@entry_id:190368)的方程。在一个称为**Tamm-Dancoff 近似 (TDA)** 的常用简化中，激发能 $\Omega$ 可以通过求解一个厄米矩阵的[本征值问题](@entry_id:142153)得到 [@problem_id:2813506]：
$\mathbf{H} \mathbf{F} = \Omega \mathbf{F}$

其中，$\mathbf{H}$ 矩阵由两部分构成：一个[对角矩阵](@entry_id:637782)，其元素是 KS 体系的单粒子-空穴跃迁能 $\omega_q = \varepsilon_a - \varepsilon_i$（$\varepsilon_a$ 为非占据[轨道能量](@entry_id:158481)，$\varepsilon_i$ 为占据轨道能量）；以及一个[耦合矩阵](@entry_id:191757) $K$，它描述了不同粒子-空穴对之间的相互作用，由 Hartree 和 xc 内核的[矩阵元](@entry_id:186505)构成。
$H_{qq'} = \omega_q \delta_{qq'} + K_{qq'}$

求解这个[本征值问题](@entry_id:142153)，得到的[本征值](@entry_id:154894) $\Omega$ 即为体系的中性电子激发能，这使得 DFT 能够被广泛用于计算[吸收光谱](@entry_id:144611)、光电子能谱等实验可观测的量。