## 引言
在现代物理学的宏伟画卷中，旋量（spinor）占据着一个核心且独特的地位。它们是描述宇宙基本物[质粒](@entry_id:263777)子——如电子、夸克等[费米子](@entry_id:146235)——所不可或缺的数学语言。将量子力学中[内禀角动量](@entry_id:189727)（自旋）的概念与爱因斯坦[狭义相对论](@entry_id:275552)的[洛伦兹变换](@entry_id:176827)框架相融合，是二十世纪初理论物理面临的一大挑战。[旋量](@entry_id:158054)理论的诞生，正是为了填补这一知识鸿沟，它提供了一个自洽且优美的框架，精确地刻画了自旋-1/2粒子在相对论性时空中的行为。

本文将系统地引导读者深入[闵可夫斯基时空](@entry_id:156421)中的[旋量](@entry_id:158054)世界。我们将分三部分展开：在“原理与机制”一章中，我们将从[旋量](@entry_id:158054)的代数根基——[洛伦兹群](@entry_id:139964)与 $SL(2, \mathbb{C})$ 群的深刻联系入手，逐步建立起外尔旋量和[狄拉克旋量](@entry_id:181944)的概念，并深入剖析支配其动力学的狄拉克方程。接下来，在“应用与跨学科联系”一章中，我们将探索旋量理论的巨大威力，展示其如何在[量子场论](@entry_id:138177)、广义相对论、原子物理乃至[超对称](@entry_id:155777)等前沿领域中扮演关键角色。最后，“动手实践”部分将提供一系列具体问题，帮助读者巩固理论知识并将其付诸实践。

现在，让我们首先进入该理论的数学与物理核心，从其根本原理与机制开始探索。

## 原理与机制

本章旨在深入探讨[闵可夫斯基时空](@entry_id:156421)中[旋量](@entry_id:158054)（spinor）的根本原理与核心机制。在之前的介绍性章节之后，我们将直接进入该理论的数学与物理细节。我们将从旋量的代数基础——[洛伦兹群](@entry_id:139964)与[特殊线性群](@entry_id:139538) $SL(2, \mathbb{C})$ 之间的深刻联系——开始，逐步构建起描述相对论性自旋-1/2粒子的完整框架。

### 代[数基](@entry_id:634389)础：$SL(2, \mathbb{C})$ 与[洛伦兹群](@entry_id:139964)

[闵可夫斯基时空](@entry_id:156421)中旋量理论的基石，是[洛伦兹群](@entry_id:139964)与 $2 \times 2$ [复矩阵](@entry_id:190650)群之间的一个惊人同构关系。具体而言，正常异时[洛伦兹群](@entry_id:139964) $SO^+(1,3)$（即保持时空方向和空间取向的[洛伦兹变换](@entry_id:176827)群）与[特殊线性群](@entry_id:139538) **$SL(2, \mathbb{C})$**（[行列式](@entry_id:142978)为1的 $2 \times 2$ [复矩阵](@entry_id:190650)群）密切相关。

这种联系可以通过将任意一个四维矢量 $x^\mu = (x^0, x^1, x^2, x^3)$ 与一个 $2 \times 2$ 的厄米矩阵（Hermitian matrix）$X$ 联系起来而建立。该映射定义为：
$$
X = x^\mu \sigma_\mu \equiv x^0 \sigma_0 + x^1 \sigma_1 + x^2 \sigma_2 + x^3 \sigma_3
$$
其中，$\sigma_0$ 是 $2 \times 2$ 的[单位矩阵](@entry_id:156724) $I_2$，而 $\sigma_k$ (k=1,2,3) 是著名的 **泡利矩阵 (Pauli matrices)**：
$$
\sigma_0 = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}, \quad \sigma_1 = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \quad \sigma_2 = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \quad \sigma_3 = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}
$$
将[四维矢量](@entry_id:275085)的分量代入，我们得到矩阵 $X$ 的具体形式：
$$
X = \begin{pmatrix} x^0+x^3 & x^1-ix^2 \\ x^1+ix^2 & x^0-x^3 \end{pmatrix}
$$
这个矩阵 $X$ 有一个至关重要的性质：它的[行列式](@entry_id:142978)等于[闵可夫斯基时空](@entry_id:156421)中[四维矢量](@entry_id:275085)长度的平方，即[时空间隔](@entry_id:154935)：
$$
\det(X) = (x^0+x^3)(x^0-x^3) - (x^1-ix^2)(x^1+ix^2) = (x^0)^2 - (x^3)^2 - ((x^1)^2 + (x^2)^2) = \eta_{\mu\nu} x^\mu x^\nu
$$
这里 $\eta_{\mu\nu}$ 是[闵可夫斯基度规](@entry_id:154660)，其符号规定为 $(+1, -1, -1, -1)$。

现在，我们考虑一个任意的 $SL(2, \mathbb{C})$ 矩阵 $M$ 对 $X$ 的作用。这个作用通过一个 **[合同变换](@entry_id:154837) (congruence transformation)** 来定义：
$$
X' = M X M^\dagger
$$
其中 $M^\dagger$ 是 $M$ 的[厄米共轭](@entry_id:191215)（即[转置](@entry_id:142115)共轭）。由于 $M$ 是 $SL(2, \mathbb{C})$ 的元素，$\det(M) = 1$，且 $\det(M^\dagger) = \overline{\det(M)} = 1$。因此，变换后矩阵的行列式保持不变：
$$
\det(X') = \det(M) \det(X) \det(M^\dagger) = \det(X)
$$
这意味着变换 $x^\mu \to x'^\mu$ 保持了[时空间隔](@entry_id:154935)不变，这正是 **洛伦兹变换 (Lorentz transformation)** 的定义。此外，由于 $X$ 是厄米的，可以证明 $X'$ 也是厄米的。因此，$X'$ 同样可以被写成一个新的四维矢量 $x'^\mu$ 的[线性组合](@entry_id:154743)形式 $X' = x'^\mu \sigma_\mu$。这样，我们便建立了从 $SL(2, \mathbb{C})$ 矩阵到[洛伦兹变换](@entry_id:176827) $\Lambda$ 的映射关系 $x'^\mu = \Lambda^\mu_{\ \nu} x^\nu$。这个映射是一个“二对一”的映射（[群同态](@entry_id:140603)），因为矩阵 $M$ 和 $-M$ 对应同一个[洛伦兹变换](@entry_id:176827)。因此，$SL(2, \mathbb{C})$ 被称为[洛伦兹群](@entry_id:139964) $SO^+(1,3)$ 的 **双重[覆盖群](@entry_id:161571) (double cover)**。

那些在 $SL(2, \mathbb{C})$ 表示下进行变换的二维复矢量，被称为 **外尔旋量 (Weyl spinors)**，它们是构成相对论性量子力学中更复杂的[狄拉克旋量](@entry_id:181944)的基本单元。

我们可以通过一个具体的例子来演示如何从 $SL(2, \mathbb{C})$ 变换中提取洛伦兹变换矩阵的分量 [@problem_id:1028170]。从 $X' = \begin{pmatrix} x'^0+x'^3 & x'^1-ix'^2 \\ x'^1+ix'^2 & x'^0-x'^3 \end{pmatrix}$ 中，我们可以反解出 $x'^\mu$ 的分量，例如 $x'^1 = \frac{1}{2}(X'_{12} + X'_{21})$。如果我们只关心由 $x^2=1$（其他分量为0）变换得到的结果，那么 $X = \sigma_2$，而变换后的 $x'^1$ 分量就是 $\Lambda^1_{\ 2}$。考虑 $SL(2, \mathbb{C})$ 矩阵 $M = \begin{pmatrix} 1+i & 2 \\ i & \frac{3+i}{2} \end{pmatrix}$，我们可以计算出 $X' = M \sigma_2 M^\dagger$ 的 $(1,2)$ 元素为 $X'_{12} = 3-2i$。由于 $X'$ 是[厄米矩阵](@entry_id:155147)，我们有 $X'_{21} = \overline{X'_{12}} = 3+2i$。因此，对应的[洛伦兹变换](@entry_id:176827)分量为 $\Lambda^1_{\ 2} = x'^1 = \frac{1}{2}(X'_{12} + X'_{21}) = \text{Re}(X'_{12}) + \text{Re}(X'_{21}) = 3$。

### 生成元与无穷小变换

研究李群的性质，最有效的方法之一是分析其李代数，即群的 **生成元 (generators)**。洛伦兹[群的生成元](@entry_id:137215)包括三个空间转动生成元 $J_i$ 和三个[洛伦兹助推](@entry_id:201972)（boost）生成元 $K_i$。在 $SL(2, \mathbb{C})$ 的框架下，这些生成元与泡利矩阵直接相关。一个由旋转矢量 $\boldsymbol{\theta}$ 描述的纯旋转 $R(\boldsymbol{\theta})$ 和一个由快度矢量 $\boldsymbol{\zeta}$ 描述的纯助推 $B(\boldsymbol{\zeta})$ 可以表示为：
$$
R(\boldsymbol{\theta}) = \exp\left(-\frac{i}{2}\boldsymbol{\theta} \cdot \boldsymbol{\sigma}\right), \quad B(\boldsymbol{\zeta}) = \exp\left(-\frac{1}{2}\boldsymbol{\zeta} \cdot \boldsymbol{\sigma}\right)
$$
可以看出，旋转的生成元是反厄米的（例如 $i\sigma_k$），而助推的生成元是厄米的（例如 $\sigma_k$）。

我们可以通过研究无穷小变换来精确确定生成元的形式 [@problem_id:1028264]。考虑一个沿 $x^1$ 方向的无穷小助推，其快度为 $\eta$。对应的 $SL(2, \mathbb{C})$ 矩阵 $A$ 和洛伦兹矩阵 $\Lambda$ 可以近似为：
$$
A \approx I_2 + \eta K_1, \quad \Lambda^\mu_{\ \nu} \approx \delta^\mu_\nu - \eta(\delta^\mu_0 \delta^1_\nu + \delta^\mu_1 \delta^0_\nu)
$$
将它们代入基本关系式 $A \sigma^\mu A^\dagger = \Lambda^\mu_{\ \nu} \sigma^\nu$ 并保留 $\eta$ 的一阶项，我们得到生成元 $K_1$ 必须满足的[代数方程](@entry_id:272665)：
$$
K_1 \sigma^\mu + \sigma^\mu K_1^\dagger = -(\delta^\mu_0 \sigma^1 + \delta^\mu_1 \sigma^0)
$$
通过对 $\mu=0, 1, 2, 3$ 分别求解，并利用 $K_1$ 是无迹的（因为 $A$ 的[行列式](@entry_id:142978)为1），我们可以唯一确定 $K_1 = -\frac{1}{2}\sigma_1$。类似地，可以得到所有助推生成元为 $K_i = -\frac{1}{2}\sigma_i$，而转动生成元为 $J_i = -\frac{i}{2}\sigma_i$。

$SL(2, \mathbb{C})$ 形式主义的一个深刻结论是，两个非共线的[洛伦兹助推](@entry_id:201972)的合并不等价于一个单一的助推，而是产生一个助推和一个空间旋转。这种现象被称为 **维格纳转动 (Wigner rotation)** 或 **[托马斯进动](@entry_id:273356) (Thomas precession)** [@problem_id:1028161]。考虑两个连续的无穷小助推 $B(\delta\boldsymbol{\zeta}_1)$ 和 $B(\delta\boldsymbol{\zeta}_2)$，其复合变换为 $A_{comp} = B(\delta\boldsymbol{\zeta}_2)B(\delta\boldsymbol{\zeta}_1)$。利用 Baker-Campbell-Hausdorff (BCH) 公式 $\exp(Y)\exp(X) \approx \exp(X + Y + \frac{1}{2}[Y,X])$，我们可以分析复合[变换的生成元](@entry_id:172031)。设 $X = -\frac{1}{2}\delta\boldsymbol{\zeta}_1 \cdot \boldsymbol{\sigma}$ 和 $Y = -\frac{1}{2}\delta\boldsymbol{\zeta}_2 \cdot \boldsymbol{\sigma}$，它们的对易子为：
$$
[Y,X] = \frac{1}{4}[\delta\boldsymbol{\zeta}_2 \cdot \boldsymbol{\sigma}, \delta\boldsymbol{\zeta}_1 \cdot \boldsymbol{\sigma}] = \frac{i}{2}(\delta\boldsymbol{\zeta}_2 \times \delta\boldsymbol{\zeta}_1) \cdot \boldsymbol{\sigma}
$$
因此，复合[变换的生成元](@entry_id:172031) $G_{comp}$ 包含一个厄米部分（对应总的助推 $\delta\boldsymbol{\zeta}_1 + \delta\boldsymbol{\zeta}_2$）和一个反厄米部分。后者正比于 $i(\delta\boldsymbol{\zeta}_1 \times \delta\boldsymbol{\zeta}_2) \cdot \boldsymbol{\sigma}$，这对应一个[无穷小旋转](@entry_id:166635)，其旋转矢量为：
$$
\delta\boldsymbol{\theta}_W = \frac{1}{2}(\delta\boldsymbol{\zeta}_1 \times \delta\boldsymbol{\zeta}_2)
$$
这个结果精确地量化了维格纳转动效应，它在原子物理和粒子物理中具有重要的物理后果。

### [狄拉克旋量](@entry_id:181944)与[狄拉克方程](@entry_id:147922)

尽管外尔旋量在描述[无质量粒子](@entry_id:263424)时非常有用，但为了构建一个能够描述有质量的自旋-1/2粒子（如电子）且在空间反演下具有良好性质的理论，我们需要引入四分量的 **[狄拉克旋量](@entry_id:181944) (Dirac spinor)** $\psi$。一个[狄拉克旋量](@entry_id:181944)可以被看作是由一个左手外尔[旋量](@entry_id:158054) $\psi_L$ 和一个右手外尔旋量 $\psi_R$ 组合而成的：
$$
\psi = \begin{pmatrix} \psi_L \\ \psi_R \end{pmatrix}
$$
在洛伦兹变换下，$\psi_L$ 和 $\psi_R$ 分别根据 $SL(2, \mathbb{C})$ 的 $(1/2, 0)$ 和 $(0, 1/2)$ 表示进行变换。

处理[狄拉克旋量](@entry_id:181944)的核心工具是 **伽马矩阵 (gamma matrices)** $\gamma^\mu$ ($\mu=0,1,2,3$)。这些是四个 $4 \times 4$ [复矩阵](@entry_id:190650)，它们定义于满足 **[克利福德代数](@entry_id:137625) (Clifford algebra)** 的[反对易关系](@entry_id:153815)：
$$
\{\gamma^\mu, \gamma^\nu\} = \gamma^\mu \gamma^\nu + \gamma^\nu \gamma^\mu = 2\eta^{\mu\nu} I_4
$$
其中 $I_4$ 是 $4 \times 4$ 单位矩阵。这个代数关系是相对论性量子力学的基石。

自由、有质量的自旋-1/2粒子的动力学由 **狄拉克方程 (Dirac equation)** 描述：
$$
(i\hbar\gamma^\mu\partial_\mu - mc)\psi = 0
$$
在自然单位制（$\hbar=c=1$）下，方程简化为 $(i\gamma^\mu\partial_\mu - m)\psi = 0$。

一个深刻的结论是，任何满足狄拉克方程的旋量场 $\psi$ 自动满足 **[克莱因-戈登方程](@entry_id:153831) (Klein-Gordon equation)** $(\partial^\mu\partial_\mu + m^2)\psi = 0$ [@problem_id:1028178]。这表明狄拉克方程不仅描述了粒子的自旋，还正确地包含了相对论性的能量-动量关系。我们可以通过直接作用狄拉克算符来证明这一点。考虑算符 $\mathcal{L} = (i\gamma^\nu\partial_\nu + m) (i\gamma^\mu\partial_\mu - m)$。展开此表达式：
$$
\mathcal{L} = -\gamma^\nu\gamma^\mu\partial_\nu\partial_\mu - m^2
$$
利用导数的[可交换性](@entry_id:263314) $\partial_\nu\partial_\mu = \partial_\mu\partial_\nu$，我们可以将乘积 $\gamma^\nu\gamma^\mu$ 对称化：
$$
\gamma^\nu\gamma^\mu\partial_\nu\partial_\mu = \frac{1}{2}(\gamma^\nu\gamma^\mu + \gamma^\mu\gamma^\nu)\partial_\nu\partial_\mu = \frac{1}{2}\{\gamma^\nu, \gamma^\mu\}\partial_\nu\partial_\mu
$$
代入[克利福德代数](@entry_id:137625)关系 $\{\gamma^\nu, \gamma^\mu\} = 2\eta^{\nu\mu}I_4$，上式变为：
$$
\eta^{\nu\mu}\partial_\nu\partial_\mu I_4 = \partial^\mu\partial_\mu I_4
$$
因此，我们得到一个算符恒等式：
$$
\mathcal{L} = -(\partial^\mu\partial_\mu + m^2)I_4
$$
当 $(i\gamma^\mu\partial_\mu - m)\psi = 0$ 时，显然有 $\mathcal{L}\psi = 0$，这就意味着 $(\partial^\mu\partial_\mu + m^2)\psi = 0$。

### 狄拉克[场的[洛伦兹变](@entry_id:267980)换](@entry_id:176827)

[狄拉克旋量](@entry_id:181944)场在洛伦兹变换 $x'^\mu = \Lambda^\mu_{\ \nu} x^\nu$ 下的变换规则是 $\Psi'(x') = S(\Lambda)\Psi(x)$，其中 $S(\Lambda)$ 是一个 $4 \times 4$ 的矩阵，构成了[洛伦兹群](@entry_id:139964)的[旋量表示](@entry_id:141362)。对于一个无穷小洛伦兹变换 $\Lambda^\mu_{\ \nu} \approx \delta^\mu_\nu + \omega^\mu_{\ \nu}$，[变换矩阵](@entry_id:151616) $S(\Lambda)$ 可以写为 $S(\Lambda) \approx I_4 - \frac{i}{2}\omega_{\mu\nu}S^{\mu\nu}$。这里的 $S^{\mu\nu}$ 是[洛伦兹群](@entry_id:139964)在[狄拉克旋量](@entry_id:181944)表示下的生成元，由伽马矩阵构造而成：
$$
S^{\mu\nu} = \frac{i}{4}[\gamma^\mu, \gamma^\nu]
$$
这些生成元自身的代数关系构成了[洛伦兹代数](@entry_id:186411)。

在特定的伽马矩阵表示下，生成元的结构变得非常清晰。例如，在 **手性表示 (chiral representation)** 或外尔表示中，伽马矩阵具有分块形式：
$$
\gamma^0 = \begin{pmatrix} 0 & I_2 \\ I_2 & 0 \end{pmatrix}, \quad \gamma^i = \begin{pmatrix} 0 & \sigma^i \\ -\sigma^i & 0 \end{pmatrix}
$$
在这种表示下，空间转动的生成元 $S^{ij}$ 呈块[对角形式](@entry_id:264850)。例如，我们可以计算 $xy$ 平面内的转动生成元 $S^{12}$ [@problem_id:1028216]：
$$
S^{12} = \frac{i}{4}[\gamma^1, \gamma^2]
$$
利用伽马矩阵的分块形式，我们有：
$$
[\gamma^1, \gamma^2] = \gamma^1\gamma^2 - \gamma^2\gamma^1 = \begin{pmatrix} 0 & \sigma^1 \\ -\sigma^1 & 0 \end{pmatrix}\begin{pmatrix} 0 & \sigma^2 \\ -\sigma^2 & 0 \end{pmatrix} - (1 \leftrightarrow 2) = \begin{pmatrix} -[\sigma^1, \sigma^2] & 0 \\ 0 & -[\sigma^1, \sigma^2] \end{pmatrix}
$$
利用泡利矩阵的[对易关系](@entry_id:136780) $[\sigma^1, \sigma^2] = 2i\sigma^3$，我们发现：
$$
S^{12} = \frac{i}{4}\begin{pmatrix} -2i\sigma^3 & 0 \\ 0 & -2i\sigma^3 \end{pmatrix} = \frac{1}{2}\begin{pmatrix} \sigma^3 & 0 \\ 0 & \sigma^3 \end{pmatrix}
$$
这清楚地表明，在手性基下，空间旋转不会混合左手和右手外尔旋量，并且其作用在每个外尔[旋量](@entry_id:158054)上的生成元正是我们之前遇到的 $SL(2, \mathbb{C})$ 转动生成元 $\sigma_3/2$。

伽马矩阵本身在[洛伦兹变换](@entry_id:176827)下的行为也至关重要。可以证明，它们像一个四维矢量一样变换：$S(\Lambda)^{-1}\gamma^\rho S(\Lambda) = \Lambda^\rho_{\ \sigma} \gamma^\sigma$。这个关系可以通过计算生成元与伽马矩阵的对易子来验证 [@problem_id:1028176]。这个基本的[对易关系](@entry_id:136780)是：
$$
[S^{\mu\nu}, \gamma^\rho] = i(\eta^{\nu\rho}\gamma^\mu - \eta^{\mu\rho}\gamma^\nu)
$$
这个恒等式确保了[狄拉克方程](@entry_id:147922)在形式上是洛伦兹[协变](@entry_id:634097)的。

### 物理态与[可观测量](@entry_id:267133)

理论的最终目的是描述物理粒子。[狄拉克方程](@entry_id:147922)的[平面波解](@entry_id:195230)代表了具有确定四维动量 $p^\mu$ 的粒子。在动量空间中，狄拉克方程变为一个[代数方程](@entry_id:272665) $(\gamma^\mu p_\mu - m)u(p) = 0$，其中 $u(p)$ 是一个四分量[动量空间](@entry_id:148936)[旋量](@entry_id:158054)。

我们可以通过为旋量的一部分分量（例如，在粒子静止系中对应自旋向上或向下的分量）设定初值来构造一组完备的解基 [@problem_id:1028244]。例如，在 **狄拉克-泡利表示** ($\gamma^0$ 对角化) 中，正能量解的形式为：
$$
u(p) = \sqrt{E+m} \begin{pmatrix} \chi \\ \frac{\vec{\sigma}\cdot\vec{p}}{E+m} \chi \end{pmatrix}
$$
其中 $E = \sqrt{|\vec{p}|^2 + m^2}$，$u = \begin{pmatrix} u_A \\ u_B \end{pmatrix}$，而 $\chi$ 是一个二维泡利[旋量](@entry_id:158054)，如 $\chi_+ = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$（自旋向上）或 $\chi_- = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$（自旋向下）。

这些解在[洛伦兹变换](@entry_id:176827)下的行为由矩阵 $S(\Lambda)$ 决定。例如，一个初始静止的自旋向下粒子，在经历一次[洛伦兹助推](@entry_id:201972)后，其[旋量](@entry_id:158054)的各个分量会发生混合 [@problem_id:1028213]。这个过程清晰地展示了自旋和动量是如何在相对论框架下纠缠在一起的。

为了从旋量场中提取可测量的物理量，我们构造了 **旋量双线性型 (spinor bilinears)**。这些是由 $\psi$ 和其 **狄拉克伴随 (Dirac adjoint)** $\bar{\psi} = \psi^\dagger \gamma^0$ 构成的特定组合。最重要的几个双线性型及其洛伦兹变换性质如下：
- $\bar{\psi}\psi$: 标量 (Scalar)
- $\bar{\psi}\gamma^\mu\psi$: 矢量 (Vector)
- $\bar{\psi}\sigma^{\mu\nu}\psi$: 张量 (Tensor)
- $\bar{\psi}\gamma^5\psi$: [赝标量](@entry_id:196696) (Pseudoscalar)
- $\bar{\psi}\gamma^5\gamma^\mu\psi$: 赝矢量 (Axial vector)

其中 $\gamma^5 = i\gamma^0\gamma^1\gamma^2\gamma^3$，而 $\sigma^{\mu\nu} = \frac{i}{2}[\gamma^\mu, \gamma^\nu]$。

这些[双线性](@entry_id:146819)型的变换性质保证了由它们构建的物理方程是洛伦兹[协变](@entry_id:634097)的。例如，[标量密度](@entry_id:161438) $\bar{\psi}\psi$ 在洛伦兹变换下是不变的，即 $\bar{\psi'}\psi' = \bar{\psi}\psi$。我们可以通过一个直接的计算来验证这一点 [@problem_id:1028125]。考虑一个初始的静止自旋向上态 $\Psi = (1, 0, 0, 0)^T$，其[标量密度](@entry_id:161438) $\bar{\Psi}\Psi = 1$。对其施加一个任意方向的[洛伦兹助推](@entry_id:201972)，得到变换后的旋量 $\Psi' = S(\Lambda)\Psi$。利用助推算符 $S(\Lambda)$ 的具体形式和 $\bar{\Psi'} = (S(\Lambda)\Psi)^\dagger \gamma^0 = \Psi^\dagger S(\Lambda)^\dagger \gamma^0$ 的关系，可以证明 $S(\Lambda)^\dagger \gamma^0 = \gamma^0 S(\Lambda)^{-1}$。于是：
$$
\bar{\Psi'}\Psi' = \Psi^\dagger \gamma^0 S(\Lambda)^{-1} S(\Lambda) \Psi = \Psi^\dagger \gamma^0 \Psi = \bar{\Psi}\Psi
$$
这证实了 $\bar{\psi}\psi$ 作为一个[洛伦兹标量](@entry_id:275319)的性质，它是构建[拉格朗日量](@entry_id:174593)中质量项的基础。

最后，理论还可以引入更具约束性的旋量类型，如 **[马约拉纳旋量](@entry_id:193020) (Majorana spinors)**，它们满足自身是其[电荷共轭](@entry_id:158278)的条件 $\chi = C \bar{\chi}^T$。这个条件对由[马约拉纳旋量](@entry_id:193020)构成的[双线性](@entry_id:146819)型施加了强烈的对称性约束 [@problem_id:1028207]。一个双线性型 $\bar{\chi}\Gamma\chi$ 是否恒为零，取决于矩阵 $M = C^\dagger\gamma^0\Gamma$ 的对称性。对于张量流 $J^{\mu\nu} = \bar{\chi}\sigma^{\mu\nu}\chi$，可以证明，其纯空间分量（如 $J^{12}, J^{23}, J^{13}$）由于对应的 $M$ 矩阵是反对称的而恒为零。相反，时空混合分量（如 $J^{01}, J^{02}, J^{03}$）对应的 $M$ 矩阵是对称的，因此这些分量通常不为零。这揭示了基本粒子的内在属性如何深刻地影响其可观测的相互作用形式。