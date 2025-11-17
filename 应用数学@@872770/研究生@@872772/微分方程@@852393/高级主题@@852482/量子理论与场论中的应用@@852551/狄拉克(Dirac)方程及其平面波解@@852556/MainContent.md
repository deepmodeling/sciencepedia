## 引言
狄拉克方程是[物理学史](@entry_id:168682)上的一座丰碑，它首次成功地将量子力学原理与[狭义相对论](@entry_id:275552)融合，为描述电子等自旋1/2[费米子](@entry_id:146235)的行为提供了坚实的理论框架。在其诞生之前，物理学面临着如何构建一个既满足[洛伦兹协变性](@entry_id:161987)又能解释电子内禀自旋的[量子理论](@entry_id:145435)的巨大挑战。[狄拉克方程](@entry_id:147922)的提出不仅完美解决了这一难题，还带来了诸如反物质预言等一系列深刻的物理洞见。

本文旨在系统性地剖析[狄拉克方程](@entry_id:147922)及其最重要的解——[平面波解](@entry_id:195230)。在“原理与机制”一章中，我们将深入其数学结构，从构建解的形式到探讨其[对称性与守恒](@entry_id:154858)量。随后的“应用与跨学科联系”一章将展示该理论如何从解释基本[粒子散射](@entry_id:152941)，延伸到描述[石墨烯](@entry_id:143512)等新奇材料的特性，并成为探索广义相对论与前沿理论的工具。最后，“动手实践”部分将提供具体的计算练习，帮助读者巩固理论知识并将其付诸实践。通过这三个层次的递进学习，读者将全面掌握狄拉克方程的核心思想，并理解其在现代物理学中持久且广泛的影响力。

## 原理与机制

继前一章对[狄拉克方程](@entry_id:147922)的介绍之后，本章将深入探讨其解的内在结构、物理诠释以及其所蕴含的[基本对称性](@entry_id:161256)。我们将从构建狄拉克方程的[平面波解](@entry_id:195230)出发，系统地阐释旋量的归一化、洛伦兹变换下的协变性、[守恒定律](@entry_id:269268)，并最终辨析手征性与螺旋性这两个核心概念。通过这些分析，我们将揭示狄拉克理论如何精确地描述相对论性自旋1/2粒子的行为。

### [狄拉克方程](@entry_id:147922)的[动量空间](@entry_id:148936)形式与[平面波解](@entry_id:195230)

[狄拉克方程](@entry_id:147922)在坐标空间中的形式为 $(i\gamma^\mu \partial_\mu - m)\psi(x) = 0$（采用自然单位制 $\hbar=c=1$）。对于一个[自由粒子](@entry_id:148748)，其[波函数](@entry_id:147440)可以自然地用平面波来描述。我们寻找形如 $\psi(x) = u(p) e^{-ip \cdot x}$ 的解，其中 $p^\mu = (E, \vec{p})$ 是粒子的[四维动量](@entry_id:272346)，满足[在壳条件](@entry_id:189200) $p^2 = p_\mu p^\mu = E^2 - |\vec{p}|^2 = m^2$。将此平面波形式代入[狄拉克方程](@entry_id:147922)，[微分](@entry_id:158718)算符 $\partial_\mu$ 作用在指数项上，得到 $-ip_\mu$。这使得方程简化为一个关于代数旋量 $u(p)$ 的[矩阵方程](@entry_id:203695)：

$(\gamma^\mu p_\mu - m)u(p) = 0$

这个方程被称为[动量空间](@entry_id:148936)中的[狄拉克方程](@entry_id:147922)。$u(p)$ 是一个四分量旋量，描述了给定动量下粒子的内禀自旋状态。为了求解这个方程，我们通常选择一个特定的伽马矩阵表示。在标准的狄拉克-泡利表示（Dirac-Pauli representation）中，伽马矩阵为：

$\gamma^0 = \begin{pmatrix} I  0 \\ 0  -I \end{pmatrix}, \quad \vec{\gamma} = \begin{pmatrix} 0  \vec{\sigma} \\ -\vec{\sigma}  0 \end{pmatrix}$

其中 $I$ 是 $2 \times 2$ [单位矩阵](@entry_id:156724)，$\vec{\sigma}$ 是泡利矩阵向量。将旋量 $u(p)$ 分解为两个二分量[旋量](@entry_id:158054)（通常称为上下分量） $u_A$ 和 $u_B$：

$u(p) = \begin{pmatrix} u_A \\ u_B \end{pmatrix}$

代入动量空间[狄拉克方程](@entry_id:147922) $(\gamma^0 E - \vec{\gamma} \cdot \vec{p} - m)u(p) = 0$，我们得到一组关于 $u_A$ 和 $u_B$ 的耦合方程：

$(E - m)u_A - (\vec{\sigma} \cdot \vec{p})u_B = 0$
$(\vec{\sigma} \cdot \vec{p})u_A - (E + m)u_B = 0$

从第二个方程，我们可以解出 $u_B$ 与 $u_A$ 的关系：

$u_B = \frac{\vec{\sigma} \cdot \vec{p}}{E+m} u_A$

这表明，对于一个正能量解（$E0$），下分量 $u_B$ 完全由上分量 $u_A$ 决定。因此，一个正能量的[狄拉克旋量](@entry_id:181944)可以写为：

$u(p) = N \begin{pmatrix} \chi \\ \frac{\vec{\sigma} \cdot \vec{p}}{E+m} \chi \end{pmatrix}$

其中 $\chi$ 是一个任意的二分量旋量， $N$ 是[归一化常数](@entry_id:752675)。通常，我们选择 $\chi$ 为自旋向上或向下的本征态，例如 $\chi_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 和 $\chi_2 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$。

这个解的结构揭示了一个重要的物理特性。在非相对论极限下，$|\vec{p}| \ll m$，此时 $E \approx m$。分母 $E+m \approx 2m$ 变得很大，而分子中的 $|\vec{p}|$ 很小，导致下分量 $u_B$ 的模相对于上分量 $u_A$ 非常小。这与非相对论的泡利理论相符，其中粒子状态由一个二分量旋量描述。然而，在超相对论极限下 ($|\vec{p}| \gg m$, $E \approx |\vec{p}|$)，下分量的大小变得与上分量相当。我们可以通过计算上下分量范数之比来量化这一点 [@problem_id:1153682]。对于一个正螺旋度（自旋平行于动量）的粒子，可以证明：

$\frac{\|u_A\|}{\|u_B\|} = \frac{E+m}{|\vec{p}|}$

这个比值在粒子静止时（$|\vec{p}| \to 0$）趋于无穷大，而在高能时趋于1，说明了下分量在相对论效应中扮演着至关重要的角色。

### 旋量的归一化与正交性

在[量子场论](@entry_id:138177)的计算中，拥有一个洛伦兹协变且标准化的[内积](@entry_id:158127)至关重要。对于[狄拉克旋量](@entry_id:181944)，简单的[厄米共轭](@entry_id:191215)[内积](@entry_id:158127) $u^\dagger u$ 并不是一个[洛伦兹标量](@entry_id:275319)（它在[洛伦兹变换](@entry_id:176827)下表现为[四维矢量](@entry_id:275085)的时间分量）。为了构造一个标量，我们引入 **狄拉克伴随**（Dirac adjoint）的定义：

$\bar{u}(p) = u^\dagger(p) \gamma^0$

利用狄拉克伴随，我们可以构造[洛伦兹标量](@entry_id:275319)积 $\bar{u}(p) u(p)$。对于我们之前导出的[平面波解](@entry_id:195230)，选取归一化常数 $N = \sqrt{E+m}$，正能量解可写作：

$u_s(p) = \sqrt{E+m} \begin{pmatrix} \chi_s \\ \frac{\vec{\sigma} \cdot \vec{p}}{E+m} \chi_s \end{pmatrix}$

其中 $s=1,2$ 代表两种自旋态，对应的 $\chi_s$ 满足 $\chi_r^\dagger \chi_s = \delta_{rs}$。

现在我们可以计算这个洛伦兹不变量积 $\bar{u}_r(p) u_s(p)$ [@problem_id:1153589]。计算过程如下：

$\bar{u}_r(p) u_s(p) = u_r^\dagger(p) \gamma^0 u_s(p)$

将 $u_r$ 和 $u_s$ 的分块形式代入，并利用 $\gamma^0 = \begin{pmatrix} I  0 \\ 0  -I \end{pmatrix}$，得到：

$\bar{u}_r u_s = (E+m) \left[ \chi_r^\dagger \chi_s - \chi_r^\dagger \left(\frac{\vec{\sigma} \cdot \vec{p}}{E+m}\right)^\dagger \left(\frac{\vec{\sigma} \cdot \vec{p}}{E+m}\right) \chi_s \right]$

由于 $(\vec{\sigma} \cdot \vec{p})^\dagger = \vec{\sigma} \cdot \vec{p}$ （因为[泡利矩阵](@entry_id:139493)是厄米的），我们得到：

$\bar{u}_r u_s = (E+m) \left[ \chi_r^\dagger \chi_s - \frac{\chi_r^\dagger (\vec{\sigma} \cdot \vec{p})^2 \chi_s}{(E+m)^2} \right]$

利用关键恒等式 $(\vec{\sigma} \cdot \vec{p})^2 = |\vec{p}|^2 I$ 和 $\chi_r^\dagger \chi_s = \delta_{rs}$，上式简化为：

$\bar{u}_r u_s = (E+m) \delta_{rs} \left[ 1 - \frac{|\vec{p}|^2}{(E+m)^2} \right] = \frac{(E+m)^2 - |\vec{p}|^2}{E+m} \delta_{rs}$

最后，利用[在壳条件](@entry_id:189200) $E^2 - |\vec{p}|^2 = m^2$，分子变为 $(E^2+2mE+m^2) - (E^2-m^2) = 2mE+2m^2 = 2m(E+m)$。于是我们得到最终的归一化关系：

$\bar{u}_r(p) u_s(p) = 2m \delta_{rs}$

类似地，可以导出负能量解 $v_s(p)$ 以及正负能量解之间的[正交关系](@entry_id:145540)，它们共同构成了[狄拉克旋量](@entry_id:181944)完备的归一化与[正交性条件](@entry_id:168905)，这在[散射截面](@entry_id:140322)等物理量的计算中是不可或缺的。

### 物理诠释：[概率流](@entry_id:150949)与粒子速度

狄拉克理论的一个早期困惑源于对速度算符的诠释。如果我们天真地将[哈密顿量](@entry_id:172864) $H_D = \vec{\alpha} \cdot \vec{p} + \beta m$ 与位置算符 $\vec{x}$ 的对易子作为速度算符 $\vec{v} = i[H_D, \vec{x}] = \vec{\alpha}$，我们会发现其[本征值](@entry_id:154894)是 $\pm 1$（在自然单位制中，即光速 $\pm c$）。这意味着对一个狄拉克粒子进行速度测量，结果总是光速，这显然与有质量粒子的物理事实相悖。

这个悖论的解决方案在于认识到，瞬时速度算符 $\vec{\alpha}$ 描述的是一种称为“颤动”（[Zitterbewegung](@entry_id:142726)）的快速[振荡运动](@entry_id:194817)，而不是粒子宏观的[传播速度](@entry_id:189384)。物理上更有意义的量是概率流的速度。狄拉克方程导出一个守恒的四维[概率流](@entry_id:150949) $j^\mu = (\rho, \vec{j}) = \bar{\psi}\gamma^\mu\psi$。其中，$\rho = \psi^\dagger \psi$ 是概率密度，$\vec{j} = \psi^\dagger \vec{\alpha} \psi$ 是[概率流密度](@entry_id:152013)。一个粒子的有效速度应被定义为[概率流密度](@entry_id:152013)与概率密度之比，即 $\vec{v}_{\text{eff}} = \vec{j}/\rho$。

让我们为一个[平面波解](@entry_id:195230) $\psi(x) = u(p)e^{-ip \cdot x}$ 计算这个比值 [@problem_id:1153494]。利用前面给出的正能量旋量形式 $u(p)$ (设 $c=1, \hbar=1$)：

首先计算[概率密度](@entry_id:175496) $\rho = u^\dagger u$：
$u^\dagger u = (E+m) \left( \chi^\dagger \chi + \chi^\dagger \frac{(\vec{\sigma}\cdot\vec{p})^2}{(E+m)^2} \chi \right) = (E+m) \left( 1 + \frac{|\vec{p}|^2}{(E+m)^2} \right) = \frac{(E+m)^2+|\vec{p}|^2}{E+m} = \frac{2E(E+m)}{E+m} = 2E$

然后计算[概率流密度](@entry_id:152013) $\vec{j} = u^\dagger \vec{\alpha} u$。利用 $\vec{\alpha} = \begin{pmatrix} 0  \vec{\sigma} \\ \vec{\sigma}  0 \end{pmatrix}$：
$u^\dagger \vec{\alpha} u = \sqrt{E+m} \begin{pmatrix} \chi^\dagger  \chi^\dagger \frac{\vec{\sigma}\cdot\vec{p}}{E+m} \end{pmatrix} \begin{pmatrix} 0  \vec{\sigma} \\ \vec{\sigma}  0 \end{pmatrix} \sqrt{E+m} \begin{pmatrix} \chi \\ \frac{\vec{\sigma}\cdot\vec{p}}{E+m}\chi \end{pmatrix}$
$= (E+m) \left( \chi^\dagger \frac{\vec{\sigma}(\vec{\sigma}\cdot\vec{p})}{E+m}\chi + \chi^\dagger \frac{(\vec{\sigma}\cdot\vec{p})\vec{\sigma}}{E+m}\chi \right)$
利用泡利矩阵的[反对易关系](@entry_id:153815)，其分量形式满足 $\sigma_k(\vec{\sigma}\cdot\vec{p}) + (\vec{\sigma}\cdot\vec{p})\sigma_k = 2p_k I$。因此，括号中的整个表达式化简为 $\frac{2\vec{p}}{E+m}$。于是：
$\vec{j} = (E+m) \frac{2\vec{p}}{E+m} = 2\vec{p}$

于是，有效速度为：
$\vec{v}_{\text{eff}} = \frac{\vec{j}}{\rho} = \frac{2\vec{p}}{2E} = \frac{\vec{p}}{E}$

这个结果正是狭义相对论中一个能量为 $E$、动量为 $\vec{p}$ 的粒子的经典速度。这完美地解决了速度算符[本征值](@entry_id:154894)的悖论，表明狄拉克理论在描述粒子整体运动方面与经典相对论是一致的。

### 相对论协变性与[洛伦兹变换](@entry_id:176827)

[狄拉克方程](@entry_id:147922)的一个核心要求是其形式在所有[惯性参考系](@entry_id:276742)中保持不变，即具有相对论[协变](@entry_id:634097)性。在洛伦兹变换 $x'^\mu = \Lambda^\mu{}_\nu x^\nu$ 下，[旋量](@entry_id:158054)场 $\psi(x)$ 并非保持不变，而是通过一个 $4 \times 4$ 矩阵 $S(\Lambda)$进行变换：

$\psi'(x') = S(\Lambda)\psi(x)$

为了使[狄拉克方程](@entry_id:147922) $(i\gamma^\mu \partial'_\mu - m)\psi'(x') = 0$ 与原方程形式相同，伽马矩阵必须满足如下变换关系：

$S(\Lambda)^{-1} \gamma^\mu S(\Lambda) = \Lambda^\mu{}_\nu \gamma^\nu$

这个关系是狄拉克理论[协变](@entry_id:634097)性的基石。我们可以通过一个具体的例子来验证它。考虑一个沿 z 轴的[洛伦兹助推](@entry_id:201972)（boost），其变换矩阵 $\Lambda^\mu{}_\nu$ 和对应的 $S(\Lambda)$ 具有特定形式。根据上述变换法则，变换后的伽马矩阵 $\tilde{\gamma}^\mu = S^{-1}\gamma^\mu S$ 可以直接用原伽马矩阵和变换参数（[快度](@entry_id:265131) $\eta$）表示 [@problem_id:1153618]：

$\tilde{\gamma}^0 = \Lambda^0{}_\nu \gamma^\nu = \cosh(\eta)\gamma^0 - \sinh(\eta)\gamma^3$
$\tilde{\gamma}^3 = \Lambda^3{}_\nu \gamma^\nu = -\sinh(\eta)\gamma^0 + \cosh(\eta)\gamma^3$

将这两式相加，可以得到一个简洁的关系：
$\tilde{\gamma}^0 + \tilde{\gamma}^3 = (\cosh\eta - \sinh\eta)(\gamma^0 + \gamma^3) = e^{-\eta}(\gamma^0 + \gamma^3)$

这种[协变](@entry_id:634097)性保证了由伽马矩阵和[旋量](@entry_id:158054)构造的物理量在不同[参考系](@entry_id:169232)下有明确的变换行为。例如，前面定义的[标量积](@entry_id:138996) $\bar{\psi}\psi$ 是一个[洛伦兹标量](@entry_id:275319)，即在任何[参考系](@entry_id:169232)下其值都不变。我们可以显式地证明这一点 [@problem_id:1153558]。

考虑一个静止的自旋向上粒子，其旋量为 $u^{(1)}(p_0)$，其中 $p_0=(m, \vec{0})$。其[标量积](@entry_id:138996)为 $\bar{u}^{(1)}(p_0)u^{(1)}(p_0) = 2m$。现在对该粒子施加一个[洛伦兹助推](@entry_id:201972)，使其获得动量 $\vec{p}$。新的旋量 $u(p)$ 由 $u(p) = S(\Lambda)u(p_0)$ 给出。通过显式计算变换后的[旋量](@entry_id:158054) $u(p)$，并计算其新的[标量积](@entry_id:138996) $\bar{u}(p)u(p) = (S(\Lambda)u(p_0))^\dagger \gamma^0 (S(\Lambda)u(p_0))$，可以证明：

$\bar{u}(p)u(p) = u(p_0)^\dagger S(\Lambda)^\dagger \gamma^0 S(\Lambda) u(p_0)$

利用 $S(\Lambda)^\dagger \gamma^0 = \gamma^0 S(\Lambda)^{-1}$ 的性质，上式变为 $u(p_0)^\dagger \gamma^0 S(\Lambda)^{-1} S(\Lambda) u(p_0) = \bar{u}(p_0)u(p_0)$。因此，我们证明了 $\bar{u}(p)u(p) = 2m$ 确实是一个洛伦兹不变量。

### [对称性与守恒](@entry_id:154858)量

在量子力学中，[对称性与守恒](@entry_id:154858)定律密切相关。如果一个物理量的算符与系统的[哈密顿量](@entry_id:172864)对易，那么这个物理量就是守恒的。

**[总角动量](@entry_id:155748)**

对于一个自由的狄拉克粒子，其[哈密顿量](@entry_id:172864)为 $H_D = \vec{\alpha} \cdot \vec{p} + \beta m$。我们可能会问，[轨道角动量](@entry_id:191303) $\vec{L} = \vec{r} \times \vec{p}$ 和[自旋角动量](@entry_id:149719) $\vec{S} = \frac{1}{2}\vec{\Sigma}$ 是否守恒？通过计算可以发现，$[H_D, \vec{L}] \neq 0$ 且 $[H_D, \vec{S}] \neq 0$。这意味着轨道角动量和自旋角动量本身都不是[守恒量](@entry_id:150267)。这反映了相对论中自旋与[轨道运动](@entry_id:162856)的耦合。

然而，它们的和，即总角动量 $\vec{J} = \vec{L} + \vec{S}$，却是守恒的。我们可以通过直接计算对易子 $[H_D, J_k]$ 来证明这一点 [@problem_id:1153633]。对易子可以分解为两部分：

$[H_D, J_k] = [ \vec{\alpha} \cdot \vec{p}, L_k ] + [ \vec{\alpha} \cdot \vec{p}, S_k ]$

利用算符的[对易关系](@entry_id:136780)，可以证明第一部分等于 $i(\vec{\alpha} \times \vec{p})_k$，而第二部分等于 $-i(\vec{\alpha} \times \vec{p})_k$。两者精确地相互抵消：

$[H_D, J_k] = i(\vec{\alpha} \times \vec{p})_k - i(\vec{\alpha} \times \vec{p})_k = 0$

这表明总角动量 $\vec{J}$ 的每一个分量都与自由狄拉克[哈密顿量](@entry_id:172864)对易，因此总角动量是守恒的。

**螺旋性**

螺旋性（Helicity）定义为自旋在动量方向上的投影。其算符为 $\hat{h} = \vec{S} \cdot \frac{\vec{p}}{|\vec{p}|}$。对于自由粒子，我们可以考察一个更简单的算符 $\vec{\Sigma} \cdot \vec{p}$ 是否与[哈密顿量](@entry_id:172864)对易 [@problem_id:1153465]。计算对易子 $[H_D, \vec{\Sigma} \cdot \vec{p}]$：

$[H_D, \vec{\Sigma}_i p_i] = [\alpha_j p_j, \Sigma_i p_i] = [\alpha_j, \Sigma_i] p_j p_i$

利用 $\alpha$ 矩阵和 $\Sigma$ 矩阵的对易关系 $[\alpha_j, \Sigma_i] = 2i \epsilon_{jik} \alpha_k$，上式变为 $2i \epsilon_{jik} \alpha_k p_j p_i$。由于 $p_j p_i$ 对指标 $i, j$ 是对称的，而[列维-奇维塔符号](@entry_id:193594) $\epsilon_{jik}$ 是反对称的，它们缩并求和后结果为零。因此：

$[H_D, \vec{\Sigma} \cdot \vec{p}] = 0$

这意味着螺旋性对于自由狄拉克粒子是一个守恒量，即粒子的[自旋投影](@entry_id:184359)到其运动方向上的值在运动过程中保持不变。

### 手征性、[螺旋性](@entry_id:157633)与[离散对称性](@entry_id:146994)

在狄拉克理论中，手征性（Chirality）和螺旋性是两个既相关又截然不同的重要概念。为了清晰地讨论手征性，我们通常采用外尔（Weyl）或手征表示（chiral representation）的伽马矩阵：

$\gamma^0 = \begin{pmatrix} 0  I \\ I  0 \end{pmatrix}, \quad \gamma^k = \begin{pmatrix} 0  \sigma^k \\ -\sigma^k  0 \end{pmatrix}, \quad \gamma^5 = i\gamma^0\gamma^1\gamma^2\gamma^3 = \begin{pmatrix} -I  0 \\ 0  I \end{pmatrix}$

手征性算符是 $\gamma^5$。它的[本征值](@entry_id:154894)为 $\pm 1$。[本征值](@entry_id:154894)为 $-1$ 的态称为左手（left-handed）手征态，[本征值](@entry_id:154894)为 $+1$ 的态称为右手（right-handed）手征态。任何[狄拉克旋量](@entry_id:181944) $u$ 都可以分解为左手和右手手征部分：$u = u_L + u_R$，其中 $u_L = P_L u$ 和 $u_R = P_R u$，投影算符为 $P_{L/R} = \frac{1}{2}(1 \mp \gamma^5)$。

对于一个 **无质量** 粒子（$m=0$），[狄拉克方程](@entry_id:147922)变为 $\gamma^\mu p_\mu u = 0$。在此情况下，可以证明[螺旋性](@entry_id:157633)算符与手征性算符 $\gamma^5$ 是等价的。也就是说，一个[无质量粒子](@entry_id:263424)的[螺旋性](@entry_id:157633)就是它的手征性。

然而，对于 **有质量** 的粒子（$m0$），情况则大不相同。[螺旋性](@entry_id:157633)依赖于[参考系](@entry_id:169232)（可以通过助推超过一个有质量的粒子，使其动量反向，从而改变其螺旋度），而手征性是一个洛伦兹不变量。一个具有确定螺旋性的有质量粒子态，通常是左手和右手手征态的混合。我们可以通过计算一个螺旋度本征态中手征性算符的[期望值](@entry_id:153208)来量化这一点 [@problem_id:1153476]。对于一个正能量、正螺旋度（螺旋度为 $+1/2$）的态，其手征性的[期望值](@entry_id:153208)为：

$\langle \gamma^5 \rangle = \frac{u^\dagger \gamma^5 u}{u^\dagger u} = \frac{|\vec{p}|}{E}$

由于对于有质量粒子 $|\vec{p}|  E$，这个[期望值](@entry_id:153208)总是在 $(-1, 1)$ 之间。这意味着该状态是左手和右手手征态的叠加。只有在超相对论极限下（$|\vec{p}| \to E$），$\langle \gamma^5 \rangle \to 1$，螺旋度[本征态](@entry_id:149904)才趋近于一个纯粹的手征态。

**[离散对称性](@entry_id:146994)**

*   **宇称（Parity, P）**: [宇称变换](@entry_id:159187)将空间坐标反演 $\vec{x} \to -\vec{x}$。它作用在[旋量](@entry_id:158054)场上为 $\psi_P(t, \vec{x}) = \gamma^0 \psi(t, -\vec{x})$。这个变换会使动量反向 $\vec{p} \to -\vec{p}$。对于一个具有确定螺旋度的态，[宇称变换](@entry_id:159187)会反转其螺旋度 [@problem_id:1153554]。例如，一个动量为 $\vec{p}$ 的正螺旋度态，在[宇称变换](@entry_id:159187)后会变成一个动量为 $-\vec{p}$ 的负螺旋度态。这是因为动量 $\vec{p}$ 是一个[极矢量](@entry_id:184542)，而自旋角动量 $\vec{S}$ 是一个轴矢量，它们的[点积](@entry_id:149019)（螺旋度）是一个[赝标量](@entry_id:196696)，在[宇称变换](@entry_id:159187)下改变符号。

*   **[电荷共轭](@entry_id:158278)（Charge Conjugation, C）**: [电荷共轭](@entry_id:158278)操作将粒子转变为其反粒子。它作用在[旋量](@entry_id:158054)场上为 $\psi_C(x) = C \bar{\psi}^T(x) = i\gamma^2 \psi^*(x)$。这个变换同样会反转粒子的螺旋度 [@problem_id:1153667]。如果一个正能量旋量 $u(\vec{p})$ 描述的是一个螺旋度为 $h$ 的粒子，那么其[电荷共轭](@entry_id:158278)[旋量](@entry_id:158054) $u_c(\vec{p}) = i\gamma^2 u^*(\vec{p})$ 将描述一个螺旋度为 $h' = -h$ 的反粒子。这一性质在[弱相互作用](@entry_id:157579)中具有极其重要的意义，因为[弱相互作用](@entry_id:157579)对不同螺旋度的粒子和反粒子的耦合方式是不同的。

通过对狄拉克方程[平面波解](@entry_id:195230)的深入分析，我们不仅掌握了描述相对论性[费米子](@entry_id:146235)的数学工具，还揭示了其背后深刻的物理原理和对称性结构，为进入[量子场论](@entry_id:138177)的更广阔领域奠定了坚实的基础。