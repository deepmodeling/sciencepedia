## 引言
自由[狄拉克场的量子化](@entry_id:155126)是现代物理学的基石，它为描述电子等自旋1/2[费米子](@entry_id:146235)提供了相对论性的量子框架。尽管经典狄拉克理论在描述单粒子行为上取得了成功，但它无法解释粒子的创生与湮灭，也未能为[多粒子系统](@entry_id:192694)提供一个自洽的理论基础。为了填补这一空白，必须将[经典场论](@entry_id:149475)提升到量子层面，即进行“[二次量子化](@entry_id:137766)”。本文旨在系统性地引导读者完成这一过程，并理解其深远的物理意义。在接下来的章节中，我们将首先在“原理与机制”中，详细构建量子化的核心数学结构，包括[场算符](@entry_id:140269)、[反对易关系](@entry_id:153815)和[Fock空间](@entry_id:143624)；接着，在“应用与跨学科连接”中，我们将探索这一理论所带来的深刻物理推论，如反物质的预言、[自旋统计定理](@entry_id:147864)，以及它如何连接粒子物理、凝聚态物质乃至[引力](@entry_id:175476)理论等前沿领域；最后，通过“动手实践”，读者将有机会通过具体计算来巩固所学知识。现在，让我们从构建这一强大理论的基本原理与机制开始。

## 原理与机制

在上一章节中，我们介绍了自由[狄拉克场](@entry_id:156753)的经典理论，它为描述自旋为 $1/2$ 的[费米子](@entry_id:146235)（如电子）提供了相对论性的框架。然而，为了解释粒子的创生与湮灭等量子现象，并为[多粒子系统](@entry_id:192694)奠定基础，我们必须将该场论进行量子化。本章旨在系统阐述自由[狄拉克场](@entry_id:156753)量子化的核心原理与关键机制。我们将从构建[场算符](@entry_id:140269)入手，通过[正则反对易关系](@entry_id:146961)引入[粒子统计](@entry_id:145640)，并最终展示这一理论如何描述基本粒子的动力学、对称性及其与真空的相互作用。

### [狄拉克场](@entry_id:156753)算符及其模态展开

量子化过程的第一步是将经典的[狄拉克旋量](@entry_id:181944)场 $\psi(x)$ 及其共轭场 $\bar{\psi}(x)$ 提升为算符。这些[场算符](@entry_id:140269)是时空的函数，作用于一个[希尔伯特空间](@entry_id:261193)（即[Fock空间](@entry_id:143624)）中的[量子态](@entry_id:146142)。作为自由场的算符，$\psi(x)$ 必须满足自由[狄拉克方程](@entry_id:147922) $(i\gamma^\mu\partial_\mu - m)\psi(x) = 0$。这个[线性偏微分方程](@entry_id:172517)的通解可以表示为平面[波的叠加](@entry_id:166456)。在[量子理论](@entry_id:145435)中，叠加的系数不再是经典数，而是算符。

因此，[狄拉克场](@entry_id:156753)算符 $\psi(x)$ 可以进行如下的模态展开：
$$
\psi(x) = \int \frac{d^3p}{(2\pi)^3\sqrt{2E_{\mathbf{p}}}} \sum_{s} \left( a^s_{\mathbf{p}} u^s(\mathbf{p}) e^{-ip \cdot x} + b^{s\dagger}_{\mathbf{p}} v^s(\mathbf{p}) e^{ip \cdot x} \right)
$$
其中 $p^\mu = (E_{\mathbf{p}}, \mathbf{p})$ 是[四维动量](@entry_id:272346)，满足[在壳条件](@entry_id:189200) $p^2 = E_{\mathbf{p}}^2 - |\mathbf{p}|^2 = m^2$，即 $E_{\mathbf{p}} = \sqrt{|\mathbf{p}|^2 + m^2}$。$s$ 是自旋标签，通常取值为 $1, 2$ 或 $\uparrow, \downarrow$。

这个展开式中的各个组成部分具有明确的物理意义：
- $u^s(\mathbf{p})$ 和 $v^s(\mathbf{p})$ 是[狄拉克旋量](@entry_id:181944)，它们是自由狄拉克方程在动量空间中的正频和负频解，分别对应于粒子和反粒子。它们满足[完备性关系](@entry_id:139077)：$\sum_s u^s(\mathbf{p})\bar{u}^s(\mathbf{p}) = \not p + m$ 和 $\sum_s v^s(\mathbf{p})\bar{v}^s(\mathbf{p}) = \not p - m$，其中 $\not p = p_\mu \gamma^\mu$。
- $a^s_{\mathbf{p}}$ 和 $b^s_{\mathbf{p}}$ 是**[湮灭算符](@entry_id:165390)**。$a^s_{\mathbf{p}}$ 湮灭一个动量为 $\mathbf{p}$、自旋为 $s$ 的粒子（例如电子），而 $b^s_{\mathbf{p}}$ 湮灭一个动量为 $\mathbf{p}$、自旋为 $s$ 的反粒子（例如[正电子](@entry_id:149367)）。
- $a^{s\dagger}_{\mathbf{p}}$ 和 $b^{s\dagger}_{\mathbf{p}}$ 是**创生算符**，它们分别是 $a^s_{\mathbf{p}}$ 和 $b^s_{\mathbf{p}}$ 的[厄米共轭](@entry_id:191215)。$a^{s\dagger}_{\mathbf{p}}$ 创生一个粒子，而 $b^{s\dagger}_{\mathbf{p}}$ 创生一个反粒子。

这个展开式将场论的连续自由度（场在每一点的取值）与粒子力学的离散自由度（粒子的动量和自旋）联系起来。

### [正则反对易关系](@entry_id:146961) (CARs)

[玻色子](@entry_id:138266)场（如[电磁场](@entry_id:265881)或[克莱因-戈登场](@entry_id:152627)）的量子化是通过[正则对易关系](@entry_id:185041)来实现的。然而，描述[费米子](@entry_id:146235)的[狄拉克场](@entry_id:156753)必须服从[泡利不相容原理](@entry_id:141850)，即两个全同[费米子](@entry_id:146235)不能占据同一个[量子态](@entry_id:146142)。为了在场论中实现这一原理，我们必须对创生和湮灭算符施加**[正则反对易关系](@entry_id:146961)**（Canonical Anticommutation Relations, CARs）。令 $\{A, B\} = AB + BA$ 表示[反对易子](@entry_id:139754)，则CARs为：
$$
\{a^r_{\mathbf{p}}, a^{s\dagger}_{\mathbf{q}}\} = (2\pi)^3 \delta^{rs} \delta^{(3)}(\mathbf{p}-\mathbf{q})
$$
$$
\{b^r_{\mathbf{p}}, b^{s\dagger}_{\mathbf{q}}\} = (2\pi)^3 \delta^{rs} \delta^{(3)}(\mathbf{p}-\mathbf{q})
$$
所有其他[反对易子](@entry_id:139754)，例如 $\{a^r_{\mathbf{p}}, a^s_{\mathbf{q}}\}$、$\{b^r_{\mathbf{p}}, b^s_{\mathbf{q}}\}$、$\{a^r_{\mathbf{p}}, b^s_{\mathbf{q}}\}$ 和 $\{a^r_{\mathbf{p}}, b^{s\dagger}_{\mathbf{q}}\}$，均为零。

这些关系是量子化的核心。例如，$(a^{s\dagger}_{\mathbf{p}})^2 = \frac{1}{2}\{a^{s\dagger}_{\mathbf{p}}, a^{s\dagger}_{\mathbf{p}}\} = 0$ 这一事实直接表明，我们无法在同一动量和自旋态上创生两个粒子，这正是[泡利不相容原理](@entry_id:141850)的体现。

基于这些算符，我们可以构建出描述任意数量粒子和反粒子的[量子态](@entry_id:146142)的 **Fock 空间**。这个空间的基石是**真空态** $|0\rangle$，它被定义为不包含任何粒子或反粒子的状态，因此被所有[湮灭算符](@entry_id:165390)湮灭：
$$
a^s_{\mathbf{p}} |0\rangle = 0 \quad \text{and} \quad b^s_{\mathbf{p}} |0\rangle = 0 \quad \text{for all } \mathbf{p}, s
$$

### 粒子态与[可观测量](@entry_id:267133)

在[Fock空间](@entry_id:143624)中，我们可以通过创生算符作用于真空态来构建粒子态。例如，一个具有确定动量 $\mathbf{p}$ 和自旋 $s$ 的单电子态 $|p, s\rangle$ 可以定义为：
$$
|p, s\rangle = \sqrt{2E_{\mathbf{p}}} a_{\mathbf{p}}^{s\dagger} |0\rangle
$$
因子 $\sqrt{2E_{\mathbf{p}}}$ 是为了确保态的洛伦兹协变归一化。类似地，单[正电子](@entry_id:149367)态由 $b^{s\dagger}_{\mathbf{p}}|0\rangle$ 创生。

这些态是[物理可观测量](@entry_id:154692)的本征态，例如能量、动量和[电荷](@entry_id:275494)。自由[狄拉克场](@entry_id:156753)的[哈密顿量](@entry_id:172864) $H$ 和[电荷](@entry_id:275494)算符 $Q$ 可以用创生和湮灭算符表示。然而，直接从拉格朗日量推导出的算符会包含一个无限大的[真空能](@entry_id:155067)贡献。为了解决这个问题，我们采用**[正规排序](@entry_id:145434)**（normal ordering）的办法，记作 $:\mathcal{O}:$。其规则是重新[排列](@entry_id:136432)算符串，使得所有创生算符都位于所有[湮灭算符](@entry_id:165390)的左侧，并且由于[费米子](@entry_id:146235)的特性，每次[交换算符](@entry_id:156554)位置时要引入一个负号。

[正规排序](@entry_id:145434)后的[哈密顿量](@entry_id:172864) $H$ 和[电荷](@entry_id:275494)算符 $Q$（假设电子[电荷](@entry_id:275494)为 $-e$）为：
$$
H = \int \frac{d^3p}{(2\pi)^3} \sum_{s} E_{\mathbf{p}} \left( a^{s\dagger}_{\mathbf{p}} a^s_{\mathbf{p}} + b^{s\dagger}_{\mathbf{p}} b^s_{\mathbf{p}} \right)
$$
$$
Q = -e \int \frac{d^3p}{(2\pi)^3} \sum_{s} \left( a^{s\dagger}_{\mathbf{p}} a^s_{\mathbf{p}} - b^{s\dagger}_{\mathbf{p}} b^s_{\mathbf{p}} \right)
$$
$a^{s\dagger}_{\mathbf{p}} a^s_{\mathbf{p}}$ 和 $b^{s\dagger}_{\mathbf{p}} b^s_{\mathbf{p}}$ 分别是粒子和反粒子的**数算符**。从表达式可以看出，每个粒子（或反粒子）都为其所在态的总能量贡献 $E_{\mathbf{p}}$。[哈密顿量](@entry_id:172864)的这种形式清晰地展示了场的激发即为粒子，每个粒子都携带一份能量量子。

通过这些表达式，我们可以验证粒子态的物理属性。例如，一个动量为 $\mathbf{q}$、自旋为 $s$ 的单正电子态 $|\Psi\rangle = d^\dagger_s(\mathbf{q})|0\rangle$（此处为了与问题符号一致，我们用 $d^\dagger$ 表示[正电子](@entry_id:149367)创生算符）是[哈密顿量](@entry_id:172864)的本征态，其[能量本征值](@entry_id:144381)为 $E_\mathbf{q} = \sqrt{|\mathbf{q}|^2+m^2}$。我们也可以考察一个[复合算符](@entry_id:152160) $\mathcal{A} = H + \frac{\lambda m}{e} Q$ 作用在该态上，利用[反对易关系](@entry_id:153815)可以精确地计算出其[本征值](@entry_id:154894)，从而验证理论的[自洽性](@entry_id:160889) [@problem_id:358850]。

同样，[电荷](@entry_id:275494)算符 $Q$ 也揭示了粒子和反粒子的[电荷](@entry_id:275494)属性。作用在单电子态上，$Q|p,s\rangle = -e|p,s\rangle$；作用在单[正电子](@entry_id:149367)态上，$Q|p,s\rangle_{positron} = +e|p,s\rangle_{positron}$。这表明 $a^\dagger$ 创生的粒[子带](@entry_id:154462)[电荷](@entry_id:275494) $-e$，而 $b^\dagger$ 创生的粒子（反粒子）带[电荷](@entry_id:275494) $+e$。算符的[代数结构](@entry_id:137052)直接反映了物理性质。例如，可以计算[电荷](@entry_id:275494)算符 $Q$ 与一个经[电荷共轭](@entry_id:158278)变换后的电子创生算符 $C a^\dagger_{\mathbf{k},r} C^{-1} = b^\dagger_{\mathbf{k},r}$ 的对易子，结果表明 $[Q, b^\dagger_{\mathbf{k},r}] = e b^\dagger_{\mathbf{k},r}$，这精确地说明了 $b^\dagger_{\mathbf{k},r}$ 所创生的态的[电荷](@entry_id:275494)为 $+e$ [@problem_id:358739]。

### 场关联函数与传播子

[场算符](@entry_id:140269)本身不是[物理可观测量](@entry_id:154692)，但它们的关联函数（correlation functions）是。这些函数描述了在不同时空点创生和湮灭粒子的振幅，并与[散射截面](@entry_id:140322)等[可观测量](@entry_id:267133)直接相关。

最基本的构件是[场算符](@entry_id:140269)与粒子态之间的[矩阵元](@entry_id:186505)。例如，计算 $\langle 0 | \psi_\alpha(x) | p, s \rangle$ 相当于问：“在时空点 $x$ 湮灭一个粒子，而在无穷远的过去创生了一个动量为 $p$、自旋为 $s$ 的粒子，这个过程的振幅是多少？” 通过代入[场算符](@entry_id:140269)的模态展开，并利用 $a_{\mathbf{k}}^r |p, s\rangle$ 和 $\langle 0| a_{\mathbf{k}}^r$ 的性质，可以得到：
$$
\langle 0 | \psi_\alpha(x) | p, s \rangle = u^s_\alpha(\mathbf{p}) e^{-ip \cdot x}
$$
这个结果表明，[场算符](@entry_id:140269) $\psi(x)$ 的作用是从真空中“提取”出一个平面波粒子[波函数](@entry_id:147440) [@problem_id:358720]。

更重要的物理量是两点关联函数，也称为**[Wightman函数](@entry_id:190021)**。例如，正频[Wightman函数](@entry_id:190021)定义为 $S^+_{\alpha\beta}(x-y) = \langle 0 | \psi_\alpha(x) \bar{\psi}_\beta(y) | 0 \rangle$。这个量可以被诠释为在 $y$ 处创生一个粒子-反粒子对，然后在 $x$ 处将其湮灭的[真空期望值](@entry_id:146340)。通过将[场算符](@entry_id:140269)展开并利用CARs，我们可以计算出：
$$
S^+_{\alpha\beta}(x-y) = \int \frac{d^3p}{(2\pi)^3 2E_{\mathbf{p}}} (\not p + m)_{\alpha\beta} e^{-ip \cdot (x-y)}
$$
这个表达式可以进一步写成 $(i\not\partial_x + m)_{\alpha\beta} i\Delta_+(x-y)$，其中 $\Delta_+(x-y)$ 是标量场的[Wightman函数](@entry_id:190021)。对于等时空间隔 $x-y = (0, \mathbf{r})$，这个积分对于有质量场会涉及到[第二类修正贝塞尔函数](@entry_id:201421) $K_1(m|\mathbf{r}|)$ [@problem_id:358929]。

在[量子场论](@entry_id:138177)中，一个核心的概念是**传播子**（propagator），它描述了一个粒子从一点传播到另一点的振幅。对于[费米子](@entry_id:146235)场，其[传播子](@entry_id:139558)与[场算符](@entry_id:140269)的[反对易子](@entry_id:139754)密切相关。我们可以计算**不等时[反对易子](@entry_id:139754)** $\{\psi_\alpha(x), \bar{\psi}_\beta(y)\}$。这个计算结合了粒子 ($a, a^\dagger$) 和反粒子 ($b, b^\dagger$) 的贡献：
$$
\{\psi_\alpha(x), \bar{\psi}_\beta(y)\} = \int \frac{d^3p}{(2\pi)^3 2E_{\mathbf{p}}} \left[ (\not p + m)_{\alpha\beta} e^{-ip \cdot (x-y)} + (\not p - m)_{\alpha\beta} e^{ip \cdot (x-y)} \right]
$$
这个量通常记作 $iS(x-y)$。它的一个至关重要的性质是，它是狄拉克方程的格林函数。我们可以通过将狄拉克算符 $(i\gamma^\mu \partial_\mu^x - m)$ 作用于它来验证这一点。由于 $p^\mu$ 满足[在壳条件](@entry_id:189200) $p^2=m^2$，即 $\not p \not p = m^2$，我们可以证明 $(i\not\partial_x - m)(\not p + m)e^{-ip\cdot(x-y)} = (\not p - m)(\not p+m)e^{-ip\cdot(x-y)}=(p^2-m^2)e^{-ip\cdot(x-y)}=0$。对另一项的计算也得出类似结果。这表明，对于 $x \neq y$，该[反对易子](@entry_id:139754)满足自由[狄拉克方程](@entry_id:147922)，这正是[格林函数](@entry_id:147802)所要求的性质 [@problem_id:358749]。更完整的分析表明 $(i\not\partial_x - m) S(x-y) = \delta^{(4)}(x-y)$。

在等时情况下，$t_x=t_y=t$，[反对易关系](@entry_id:153815)简化为：
$$
\{\psi_\alpha(t, \mathbf{x}), \psi_\beta^\dagger(t, \mathbf{y})\} = \delta_{\alpha\beta}\delta^{(3)}(\mathbf{x}-\mathbf{y})
$$
这被称为等时[反对易关系](@entry_id:153815)，是[正则量子化](@entry_id:148501)的一个基本出发点。

### 对称性、流与[量子反常](@entry_id:146580)

[经典场论](@entry_id:149475)中的对称性通过诺特定理导致[守恒流](@entry_id:148966)。在量子理论中，这些对称性由作用在[Fock空间](@entry_id:143624)上的幺正算符实现，而[守恒流](@entry_id:148966)也相应地成为算符。

- **U(1)矢量对称性与[电荷守恒](@entry_id:264158)**: 全局U(1)变换 $\psi \to e^{-i\theta}\psi$ 对应于[电荷守恒](@entry_id:264158)。[守恒流](@entry_id:148966)算符为 $j^\mu(x) = -e :\bar{\psi}(x)\gamma^\mu\psi(x):$。其零分量 $j^0$ 的空间积分就是我们之前定义的[电荷](@entry_id:275494)算符 $Q = \int d^3x j^0(x)$。

- **手征对称性与轴矢流**: 对于**无质量** ($m=0$) 的[狄拉克场](@entry_id:156753)，拉格朗日量还具有额外的手征对称性 $\psi \to e^{i\alpha\gamma_5}\psi$。对应的诺特流是轴矢流 $J_5^\mu = \bar{\psi}\gamma^\mu\gamma_5\psi$。这个对称性在物理上与粒子的螺旋度（helicity）密切相关。螺旋度是自旋在动量方向上的投影。对于无质量[费米子](@entry_id:146235)，螺旋度是一个洛伦兹不变量。我们可以计算轴矢荷[密度算符](@entry_id:138151) $:J_5^0(x):$ 在一个确定螺旋度的单粒子态 $|k, h'\rangle$ 中的[期望值](@entry_id:153208)，结果表明该[期望值](@entry_id:153208)正比于粒子的螺旋度 [@problem_id:358736]。这揭示了轴矢荷与螺旋度之间的深刻联系。

然而，量子化过程有时会破坏经典的对称性，这一现象称为**[量子反常](@entry_id:146580)**（quantum anomaly）。一个著名的例子发生在[(1+1)维](@entry_id:153451)时空中。经典无质量[电动力学](@entry_id:158759)中的矢量流 $j^\mu$ 和轴矢流 $j_5^\mu$ 都是守恒的。但在量子理论中，由于算符在同一点的乘积需要正规化，导致流算符的[对易关系](@entry_id:136780)出现经典理论中不存在的项。例如，[电荷密度](@entry_id:144672) $j^0$ 和空间流 $j^1$ 的等时对易子的[真空期望值](@entry_id:146340)并非为零，而是包含一个所谓的**[施温格项](@entry_id:158784)**（Schwinger term）[@problem_id:358746]：
$$
\langle 0 | [j^0(t,x), j^1(t,y)] | 0 \rangle = \frac{i}{\pi} \partial_x \delta(x-y)
$$
这个非零结果是一个纯粹的量子效应，它在[量子霍尔效应](@entry_id:136283)和现代凝聚态物理中扮演着重要角色。

### 动力学与真空效应

在[海森堡绘景](@entry_id:141162)中，[量子态](@entry_id:146142)是固定的，而算符随[时间演化](@entry_id:153943)。[场算符](@entry_id:140269)的演化由[海森堡运动方程](@entry_id:140445) $i\partial_t \psi(t, \mathbf{x}) = [\psi(t, \mathbf{x}), H]$ 决定。通过求解这个方程，我们可以将任意时刻的[场算符](@entry_id:140269)用初始时刻 ($t=0$) 的[场算符](@entry_id:140269)来表示。例如，在动量空间中，$\tilde{\psi}(\mathbf{p}, t) = e^{-i H_D(\mathbf{p}) t} \tilde{\psi}(\mathbf{p}, 0)$，其中 $H_D(\mathbf{p})$ 是[动量空间](@entry_id:148936)中的狄拉克[哈密顿量](@entry_id:172864)矩阵。通过对[矩阵指数](@entry_id:139347) $e^{-i H_D t}$ 进行计算，我们可以得到场分量随时间的详细[振荡](@entry_id:267781)行为，这种[振荡](@entry_id:267781)混合了不同的手征分量，其频率由能量 $E_{\mathbf{p}}$ 和质量 $m$ 共同决定 [@problem_id:358922]。

最后，我们回到真空本身。尽管我们通过[正规排序](@entry_id:145434)移除了[哈密顿量](@entry_id:172864)中的无限大常数，但真空的物理性质远非平凡。真空可以被看作是充满虚粒子对的海洋，这些虚粒子可以与外场或边界条件相互作用，产生可观测的物理效应（如[卡西米尔效应](@entry_id:148651)）。

如果我们不采用[正规排序](@entry_id:145434)，而是通过引入一个动量截断 $\Lambda$ 来正规化[真空能](@entry_id:155067)量密度的[发散积分](@entry_id:140797)，可以更深入地研究真空的结构。自由[狄拉克场](@entry_id:156753)的[真空能](@entry_id:155067)量密度为：
$$
\mathcal{E}_{vac} = -2 \int \frac{d^3p}{(2\pi)^3} E_{\mathbf{p}} = -2 \int \frac{d^3p}{(2\pi)^3} \sqrt{|\mathbf{p}|^2 + m^2}
$$
（负号来源于[费米子](@entry_id:146235)真空的贡献）。这个积分在 $|\mathbf{p}| \to \infty$ 时是[紫外发散](@entry_id:183379)的。通过引入动量截断 $| \mathbf{p} | \le \Lambda$ 并对结果进行大 $\Lambda$ 展开，我们得到：
$$
\mathcal{E}_{vac}(\Lambda, m) = c_4 \Lambda^4 + c_2 m^2 \Lambda^2 + c_L m^4 \ln\left(\frac{\Lambda}{m}\right) + c_F m^4 + \mathcal{O}\left(\frac{m^6}{\Lambda^2}\right)
$$
这里的各项都有其物理解释。$\Lambda^4$ 和 $\Lambda^2$ 项是发散项，可以在重整化过程中被吸收。对数发散项 $m^4 \ln(\Lambda/m)$ 反映了标度变化下的理论行为。而最有趣的是有限的 $m^4$ 项，它的系数 $c_F$ 是一个可以通过精确计算确定的、与理论具体细节相关的非平凡数值 [@problem_id:358944]。这个有限部分贡献了宇宙学常数，构成了现代物理学中的一个重大谜题。这一分析表明，我们所说的“真空”具有丰富的内在结构，其能量响应是[量子场论](@entry_id:138177)的一个深刻且可计算的预言。