## 引言
[狄拉克场](@entry_id:156753)理论是现代物理学的基石之一，它首次成功地将量子力学与爱因斯坦的[狭义相对论](@entry_id:275552)无缝融合。在20世纪初，描述高速运动电子的理论存在着根本性的空白，非相对论的薛定谔方程无法解释电子的自旋等内在属性及其在相对论速度下的行为。[狄拉克方程](@entry_id:147922)的提出，不仅填补了这一空白，更以其深刻的数学优雅性和惊人的预测能力，揭示了自然界更深层次的对称性与结构，例如反物质的存在。本文旨在为读者提供一个关于经典[狄拉克场](@entry_id:156753)与[旋量](@entry_id:158054)的全面而深入的理解。

我们将分三个核心章节展开探索。在“原理与机制”中，我们将从拉格朗日和[哈密顿量](@entry_id:172864)形式出发，剖析[狄拉克场](@entry_id:156753)的基本动力学，深入研究其核心组成部分——伽马矩阵和旋量，并探讨其在[时空对称性](@entry_id:179029)下的变换规律。接着，在“应用与跨学科联系”中，我们将展示狄拉克理论如何超越其粒子物理的起源，成为凝聚态物理、广义相对论乃至纯数学等多个领域的强大分析工具。最后，通过一系列“动手实践”问题，读者将有机会亲手应用所学知识，解决具体的物理问题，从而将抽象的理论概念转化为扎实的计算技能。

## 原理与机制

本章旨在系统性地阐述经典[狄拉克场](@entry_id:156753)的核心原理与机制。我们将从[狄拉克场](@entry_id:156753)的拉格朗日和[哈密顿量](@entry_id:172864)形式出发，深入探讨其固有的旋量结构、不同的数学表示及其内在联系。在此基础上，我们将剖析[狄拉克场](@entry_id:156753)在[时空对称性](@entry_id:179029)（包括[洛伦兹变换](@entry_id:176827)和分立对称性）下的变换行为，并揭示由此产生的守恒律。最后，我们将探讨一些由狄拉克方程预测的独特物理现象以及超越标准[狄拉克费米子](@entry_id:161484)的特殊旋量类型。

### [狄拉克场](@entry_id:156753)的拉格朗日与[哈密顿量](@entry_id:172864)形式

描述一个质量为 $m$ 的自由[旋量](@entry_id:158054)场 $\psi(x)$ 的相对论性动力学，最简洁的出发点是其拉格朗日密度 $\mathcal{L}$。它必须是一个[洛伦兹标量](@entry_id:275319)，并能导出一阶的[运动方程](@entry_id:170720)。满足这些条件的标准形式是：
$$
\mathcal{L} = \bar{\psi} (\mathrm{i} \gamma^\mu \partial_\mu - m) \psi
$$
在此表达式中，$\psi(x)$ 是一个四分量复值旋量场，$\partial_\mu$ 是时空四维梯度算符。$\gamma^\mu$ 是四个 $4 \times 4$ 矩阵，被称为[狄拉克伽马矩阵](@entry_id:196236)，它们是狄拉克理论的代[数基](@entry_id:634389)石。它们满足反对易的[克利福德代数](@entry_id:137625)关系：
$$
\{ \gamma^\mu, \gamma^\nu \} = \gamma^\mu \gamma^\nu + \gamma^\nu \gamma^\mu = 2 g^{\mu\nu} I_4
$$
其中 $g^{\mu\nu}$ 是闵可夫斯基时空度规，我们采用 $(+,-,-,-)$ 的符号约定，$I_4$ 是 $4 \times 4$ [单位矩阵](@entry_id:156724)。符号 $\bar{\psi}$ 代表狄拉克伴随[旋量](@entry_id:158054)，定义为 $\bar{\psi} = \psi^\dagger \gamma^0$，其中 $\dagger$ 表示[厄米共轭](@entry_id:191215)。这个构造确保了 $\bar{\psi}\psi$ 是一个[洛伦兹标量](@entry_id:275319)。

从拉格朗日密度出发，我们可以通过标准的[勒让德变换](@entry_id:146727)构建理论的[哈密顿量密度](@entry_id:164562) $\mathcal{H}$。首先，我们定义与场分量 $\psi_\alpha$ 共轭的[正则动量](@entry_id:155151) $\Pi_\alpha$：
$$
\Pi_\alpha = \frac{\partial \mathcal{L}}{\partial(\partial_0 \psi_\alpha)}
$$
由于拉格朗日密度对 $\partial_0 \psi$ 是线性的，$\mathcal{L} = \mathrm{i} \psi^\dagger \gamma^0 \gamma^0 \partial_0 \psi + \dots = \mathrm{i} \psi^\dagger \partial_0 \psi + \dots$，我们得到 $\Pi = \mathrm{i} \psi^\dagger$。这是一个重要的特征：[狄拉克场](@entry_id:156753)的[正则动量](@entry_id:155151)与其场本身相关，而不是其时间导数。这表明狄拉克理论是一个[约束系统](@entry_id:164587)，其动力学是一阶的。

[哈密顿量密度](@entry_id:164562)由下式给出：
$$
\mathcal{H} = \Pi (\partial_0 \psi) - \mathcal{L}
$$
代入 $\Pi$ 和 $\mathcal{L}$ 的表达式，我们发现包含 $\partial_0 \psi$ 的项相互抵消：
$$
\mathcal{H} = (\mathrm{i} \psi^\dagger)(\partial_0 \psi) - \left( \mathrm{i} \bar{\psi} \gamma^0 \partial_0 \psi + \mathrm{i} \bar{\psi} \gamma^k \partial_k \psi - m \bar{\psi} \psi \right)
$$
$$
\mathcal{H} = \mathrm{i} \psi^\dagger \partial_0 \psi - \left( \mathrm{i} \psi^\dagger \partial_0 \psi + \mathrm{i} \psi^\dagger \gamma^0 \gamma^k \partial_k \psi - m \psi^\dagger \gamma^0 \psi \right)
$$
最终得到[哈密顿量密度](@entry_id:164562)：
$$
\mathcal{H} = -\mathrm{i} \psi^\dagger \gamma^0 \gamma^k \partial_k \psi + m \psi^\dagger \gamma^0 \psi = \bar{\psi} (-\mathrm{i} \gamma^k \partial_k + m) \psi
$$
这可以写成更紧凑的形式 $\mathcal{H} = \psi^\dagger H \psi$，其中 $H = \vec{\alpha} \cdot \vec{p} + \beta m$ 是单粒子狄拉克[哈密顿算符](@entry_id:144286)，$\vec{p} = -\mathrm{i}\vec{\nabla}$，且[狄拉克矩阵](@entry_id:155614) $\vec{\alpha}$ 和 $\beta$ 定义为 $\alpha^k = \gamma^0 \gamma^k$ 和 $\beta = \gamma^0$。

为了更具体地理解动能项的结构，我们可以考虑在手性（或外尔）表示下进行这一推导 [@problem_id:391020]。在该表示中，$\psi$ 分解为左手和右手外尔[旋量](@entry_id:158054) $\psi_L$ 和 $\psi_R$。[哈密顿量密度](@entry_id:164562)最终呈现为：
$$
\mathcal{H} = \mathrm{i} \psi_L^\dagger \sigma^k \partial_k \psi_L - \mathrm{i} \psi_R^\dagger \sigma^k \partial_k \psi_R + m (\psi_L^\dagger \psi_R + \psi_R^\dagger \psi_L)
$$
其中 $\sigma^k$ 是泡利矩阵。这一形式清晰地表明，动能项将左手和右手部分分开处理，而质量项则将它们耦合在一起。

### 伽马矩阵的表示

[克利福德代数](@entry_id:137625) $\{ \gamma^\mu, \gamma^\nu \} = 2 g^{\mu\nu} I_4$ 并没有唯一确定伽马矩阵的具体形式。任何一组通过[相似变换](@entry_id:152935) $\gamma'^\mu = S \gamma^\mu S^{-1}$ 相互关联的矩阵都同样有效，其中 $S$ 是一个可逆矩阵。不同的表示在处理特定问题时各有优势。

最常用的两种表示是 **狄拉克-泡利表示** 和 **手性（或外尔）表示**。

在 **狄拉克-泡利表示** 中，伽马矩阵具有块结构：
$$
\gamma^0_D = \begin{pmatrix} I_2  & 0 \\ 0 & -I_2 \end{pmatrix}, \quad \gamma^i_D = \begin{pmatrix} 0 & \sigma^i \\ -\sigma^i & 0 \end{pmatrix}
$$
这种表示的 $\gamma^0$ 是对角的，它将旋量的上下两个分量（大分量和小分量）与正负能量清晰地联系起来，因此在分析非相对论极限时特别有用。

在 **手性（或外尔）表示** 中，伽马矩阵则为：
$$
\gamma^0_C = \begin{pmatrix} 0 & I_2 \\ I_2 & 0 \end{pmatrix}, \quad \gamma^i_C = \begin{pmatrix} 0 & \sigma^i \\ -\sigma^i & 0 \end{pmatrix}
$$
注意，空间部分的伽马矩阵在两种表示中是相同的。手性表示的优势在于它使描述手性（粒子“手性”的内在属性）的算子 $\gamma^5$ 变成[对角形式](@entry_id:264850)，这在研究无质量粒子或与[手性对称性](@entry_id:141715)相关的现象时非常方便。

物理学不应依赖于我们选择的数学表示。因此，这两种表示之间必须存在一个确定的联系。我们可以找到一个[相似变换](@entry_id:152935)矩阵 $S$ 使得 $\gamma^\mu_C = S \gamma^\mu_D S^{-1}$ [@problem_id:390939]。通过比较两种表示中 $\gamma^0$ 的形式，并要求 $S$ 与 $\gamma^i_D$ 对易（因为 $\gamma^i_D = \gamma^i_C$），可以构建出这个矩阵。一个满足[幺正性](@entry_id:138773)、实数性和迹为正等条件的标准选择是：
$$
S = \frac{1}{\sqrt{2}} \begin{pmatrix} I_2 & -I_2 \\ I_2 & I_2 \end{pmatrix}
$$
理解不同表示之间的转换能力是[场论](@entry_id:155241)计算中的一项基本技能。

### [旋量](@entry_id:158054)及其组分

#### [平面波解](@entry_id:195230)
狄拉克方程的[平面波解](@entry_id:195230)构成了描述自由粒子的[基本模式](@entry_id:165201)。在[动量空间](@entry_id:148936)中，方程变为一个[代数方程](@entry_id:272665)：
$$
(\gamma^\mu p_\mu - m) u(p) = 0
$$
其中 $p^\mu = (E, \vec{p})$ 是粒子的[四维动量](@entry_id:272346)，满足[在壳条件](@entry_id:189200) $E = \sqrt{|\vec{p}|^2 + m^2}$，$u(p)$ 是一个四分量[狄拉克旋量](@entry_id:181944)。

在狄拉克-泡利表示中，我们可以将 $u(p)$ 分解为两个二分量[旋量](@entry_id:158054)，即上分量 $\phi$ 和下分量 $\chi$：$u(p) = \begin{pmatrix} \phi \\ \chi \end{pmatrix}$。代入狄拉克方程后，我们得到一个耦合的[方程组](@entry_id:193238)：
$$
(E - m)\phi - (\vec{\sigma} \cdot \vec{p})\chi = 0
$$
$$
(\vec{\sigma} \cdot \vec{p})\phi - (E + m)\chi = 0
$$
从第二个方程，我们可以解出下分量 $\chi$ 与上分量 $\phi$ 的关系 [@problem_id:390907]：
$$
\chi = \frac{\vec{\sigma} \cdot \vec{p}}{E + m} \phi
$$
这个关系揭示了深刻的物理内涵。在非相对论极限下，$|\vec{p}| \ll m$ 且 $E \approx m$，此时下分量 $\chi$ 相对于上分量 $\phi$ 非常小。$\phi$ 对应于粒子的“大分量”，而 $\chi$ 是“小分量”。这与薛定谔理论中的二分量泡利旋量相对应。然而，在超相对论极限下 ($E \gg m$)，下分量的大小变得与上分量相当，表明粒子的相对论性质变得至关重要。

#### 外尔旋量与手性
手性的概念是理解[狄拉克场](@entry_id:156753)的关键。它由第五个伽马矩阵 $\gamma^5$ 来定义：
$$
\gamma^5 = \mathrm{i}\gamma^0\gamma^1\gamma^2\gamma^3
$$
$\gamma^5$ 与所有四个常规伽马矩阵反对易，且 $(\gamma^5)^2 = I_4$。利用 $\gamma^5$，我们可以构造两个相互正交的投影算子：
$$
P_L = \frac{1 - \gamma^5}{2}, \quad P_R = \frac{1 + \gamma^5}{2}
$$
这两个算子可以将任何[狄拉克旋量](@entry_id:181944) $\psi$ 分解为左手部分 $\psi_L = P_L \psi$ 和右手部分 $\psi_R = P_R \psi$。顾名思义，$P_L$ 投影出左手手性态，而 $P_R$ 投影出右手手性态。

在手性表示中，这种分解变得尤为简洁，因为 $\gamma^5_C = \begin{pmatrix} -I_2 & 0 \\ 0 & I_2 \end{pmatrix}$ 是对角的。因此，一个[狄拉克旋量](@entry_id:181944)可以直接写成：
$$
\psi = \begin{pmatrix} \psi_L \\ \psi_R \end{pmatrix}
$$
在这种表示下，[狄拉克方程](@entry_id:147922)可以被重写为两个耦合的[一阶微分方程](@entry_id:173139) [@problem_id:390885]：
$$
\mathrm{i} \bar{\sigma}^\mu \partial_\mu \psi_L = m \psi_R
$$
$$
\mathrm{i} \sigma^\mu \partial_\mu \psi_R = m \psi_L
$$
其中 $\sigma^\mu = (I_2, \vec{\sigma})$ 和 $\bar{\sigma}^\mu = (I_2, -\vec{\sigma})$。这些方程清楚地显示，质量 $m$ 起到了耦合左手和右手旋量的作用。如果粒子是无质量的 ($m=0$)，这两个方程解耦，$\psi_L$ 和 $\psi_R$ 分别独立地满足外尔方程。

通过代数操作，我们可以[解耦](@entry_id:637294)这两个方程。例如，将第一个方程作用于第二个方程的左侧，可以得到一个只关于 $\psi_L$ 的二阶方程：
$$
(\partial^\mu \partial_\mu + m^2) \psi_L(x) = 0
$$
这正是[克莱因-戈登方程](@entry_id:153831)。同理，$\psi_R$ 也满足同样的方程。这表明，尽管狄拉克方程是一阶的，但它的每个分量都必须满足由[相对论能量](@entry_id:158443)-动量关系 $E^2 = p^2 + m^2$ 所决定的二阶[克莱因-戈登方程](@entry_id:153831) [@problem_id:390885]。

将[洛伦兹不变量](@entry_id:161821)（称为狄拉克复合算子）用外尔[旋量表示](@entry_id:141362)也非常有启发性。例如，标量 $\bar{\psi}\psi$ 和[赝标量](@entry_id:196696) $\bar{\psi}\gamma^5\psi$ 可以写为 [@problem_id:390806]：
$$
\bar{\psi}\psi = \psi_L^\dagger \psi_R + \psi_R^\dagger \psi_L
$$
$$
\bar{\psi}\gamma^5\psi = \psi_L^\dagger \psi_R - \psi_R^\dagger \psi_L
$$
这些表达式在构建超出标准模型的[粒子物理理论](@entry_id:200576)（如[四费米子相互作用](@entry_id:184227)理论）时至关重要。

### 对称性与变换

#### 洛伦兹变换与自旋
[狄拉克旋量](@entry_id:181944)在[洛伦兹变换](@entry_id:176827) $\Lambda$ 下的变换规则为 $\psi'(x') = S[\Lambda]\psi(x)$，其中 $x'=\Lambda x$。$S[\Lambda]$ 是旋量空间中[洛伦兹群的表示](@entry_id:181892)矩阵，可以由伽马矩阵的生成元 $J^{\mu\nu} = \frac{\mathrm{i}}{4}[\gamma^\mu, \gamma^\nu]$ 构建。对于沿 $z$ 轴的特定[快度](@entry_id:265131)为 $\zeta$ 的助推（boost），变换算子为：
$$
S(\zeta) = \exp\left(\frac{\zeta}{2}\gamma^0\gamma^3\right)
$$
粒子的自旋由泡利-鲁班斯基（Pauli-Lubanski）[赝矢量](@entry_id:196296) $S^\mu$ 来协变地描述。对于一个动量为 $p$、归一化为 $\bar{\psi}\psi=1$ 的粒子，其定义为 $S^\mu = -\frac{1}{2} \bar{\psi} \gamma^5 \gamma^\mu \psi$。一个有趣的练习是考察一个在静止系中沿 $x$ 轴极化的粒子，当它被沿 $z$ 轴助推后其自旋如何变化 [@problem_id:390971]。通过显式计算，可以发现尽管[旋量](@entry_id:158054)的所有四个分量都发生了复杂的变换，但其自旋矢量的 $x$ 分量 $S^1$ 仍然保持不变。这说明在没有外力矩的情况下，自旋的取向（相对于运动方向）在[洛伦兹变换](@entry_id:176827)下以一种非平凡的方式保持。

#### 分立对称性：宇称、[电荷共轭](@entry_id:158278)和[时间反演](@entry_id:182076)

除了连续的洛伦兹对称性，狄拉克理论还具有重要的分立对称性。

**宇称 (P):** [宇称变换](@entry_id:159187)反转空间坐标：$x=(t, \vec{x}) \to x_P=(t, -\vec{x})$。[狄拉克场](@entry_id:156753)在此变换下的行为是 $\Psi'(x) = P \Psi(x_P)$。在任何表示中，宇称算子 $P$ 都等于 $\gamma^0$。在手性表示中，$P = \gamma^0 = \begin{pmatrix} 0 & I \\ I & 0 \end{pmatrix}$。这意味着[宇称变换](@entry_id:159187)会交换左手和右手外尔旋量 [@problem_id:390946]：
$$
\psi_L(x) \to \psi_R(x_P), \quad \psi_R(x) \to \psi_L(x_P)
$$
这个性质对于确定场的复合量（如 $\bar{\psi}\psi$）在宇称下的变换属性至关重要。例如，一个量若在[宇称变换](@entry_id:159187)下不变，则称为标量；若获得一个负号，则称为[赝标量](@entry_id:196696)。

**[电荷共轭](@entry_id:158278) (C):** [电荷共轭](@entry_id:158278)操作将粒子与其反粒子联系起来。对于一个旋量场 $\psi$，其[电荷共轭](@entry_id:158278)场 $\psi^c$ 定义为 $\psi^c = C \bar{\psi}^T$。矩阵 $C$ 被定义为满足以下核心关系（在任何表示中都成立，仅相差一个相位）：
$$
C \gamma^\mu C^{-1} = -(\gamma^\mu)^T
$$
其中 $T$ 表示[矩阵转置](@entry_id:155858)。这个关系意味着，在伽马矩阵具有特定对称性的表象中， $C$ 与某些伽马矩阵对易，而与另一些[反对易](@entry_id:186708)。例如，在手性表示中，$\gamma^0$ 和 $\gamma^2$ 是对称的，而 $\gamma^1$ 和 $\gamma^3$ 是反对称的。因此，可以证明 $C$ 与 $\gamma^0, \gamma^2$ 对易，而与 $\gamma^1, \gamma^3$ 反对易 [@problem_id:390922]。这些条件，再加上幺正性和实数性等附加约束，可以唯一确定 $C$ 的形式。进一步可以验证 $C$ 满足如 $C^T = -C$ 和 $C^2 = -I_4$ 等重要性质。

**时间反演 (T):** [时间反演](@entry_id:182076)变换反转时间坐标，$t \to -t$。它是一个[反幺正算符](@entry_id:197532)，其对[旋量](@entry_id:158054)[波函数](@entry_id:147440)的作用定义为 $\psi^T(p) = T_K \psi^*(p)$，其中 $*$ 表示[复共轭](@entry_id:174690)。在狄拉克表示中，矩阵 $T_K$ 由 $T_K = \mathrm{i}\gamma^1\gamma^3$ 给出 [@problem_id:390883]。与P和C不同，T的反幺正性质使其在[量子场论](@entry_id:138177)中扮演着独特的角色。

#### 守恒律
根据诺特定理，[连续对称性](@entry_id:137257)对应于[守恒流](@entry_id:148966)和[守恒荷](@entry_id:145660)。狄拉克拉格朗日量具有全局U(1)相位不变性 $\psi \to e^{-\mathrm{i}\alpha}\psi$，这导致了一个守恒的矢量流 $J^\mu = \bar{\psi}\gamma^\mu\psi$，满足 $\partial_\mu J^\mu = 0$。$J^0 = \psi^\dagger\psi$ 是[概率密度](@entry_id:175496)，而 $Q = \int d^3x J^0$ 是守恒的[电荷](@entry_id:275494)（例如[电荷](@entry_id:275494)）。

另一个至关重要的[守恒量](@entry_id:150267)是[总角动量](@entry_id:155748)。对于在[中心势](@entry_id:148563) $V(r)$ 中运动的狄拉克粒子，其[哈密顿量](@entry_id:172864)为 $H = \vec{\alpha} \cdot \vec{p} + \beta m + V(r)I_4$。轨道角动量 $\vec{L} = \vec{x} \times \vec{p}$ 和[自旋角动量](@entry_id:149719) $\vec{S} = \frac{1}{2}\vec{\Sigma}$（其中 $\vec{\Sigma} = \begin{pmatrix} \vec{\sigma} & 0 \\ 0 & \vec{\sigma} \end{pmatrix}$）本身并不与[哈密顿量](@entry_id:172864)对易，即 $[H, \vec{L}] \neq 0$ 和 $[H, \vec{S}] \neq 0$。这意味着[轨道](@entry_id:137151)和[自旋角动量](@entry_id:149719)不是独立的[守恒量](@entry_id:150267)。然而，它们的和，即总角动量 $\vec{J} = \vec{L} + \vec{S}$，确实与[哈密顿量](@entry_id:172864)对易：$[H, \vec{J}] = 0$ [@problem_id:390938]。这揭示了狄拉克理论内在地包含了[自旋-轨道耦合](@entry_id:143520)，总角动量才是真正的[守恒量](@entry_id:150267)。

### 高级主题与物理现象

#### [颤动](@entry_id:142726) ([Zitterbewegung](@entry_id:142726))
狄拉克方程的一个惊人预测是自由粒子也会表现出一种称为“颤动”（Zitterbewegung）的快速[振荡运动](@entry_id:194817)。这种现象源于构成粒子波包的正能量和[负能量](@entry_id:161542)[平面波解](@entry_id:195230)之间的干涉。

速度算符由[海森堡运动方程](@entry_id:140445)定义为 $\hat{\vec{v}} = \frac{d\vec{x}}{dt} = \mathrm{i}[H, \vec{x}] = c\vec{\alpha}$。由于 $\alpha$ 矩阵的非对角性，速度算符的[本征值](@entry_id:154894)是 $\pm c$，这似乎与一个有质量粒子速度不能达到光速相矛盾。更重要的是，速度算符 $\vec{\alpha}$ 与[自由粒子](@entry_id:148748)[哈密顿量](@entry_id:172864) $H$ 不对易，这意味着速度不是一个守恒量。

我们可以通过计算一个特定状态的速度[期望值](@entry_id:153208)来观察这种现象。考虑一个由正能量和负能量静止系[本征态](@entry_id:149904)叠加而成的初始状态 [@problem_id:391027]。例如，一个初始态 $\Psi(0) = \frac{1}{2} (u_1 + \mathrm{i} u_2 - \mathrm{i} v_1 + v_2)$。计算其速度算符 $y$ 分量的[期望值](@entry_id:153208)随时间的变化，会得到：
$$
\langle \hat{v}_y \rangle(t) = c \sin\left( \frac{2 m c^2 t}{\hbar} \right)
$$
这个结果表明，即使粒子的[总动量](@entry_id:173071)为零，其瞬时速度的[期望值](@entry_id:153208)也在以一个极高的频率 $2mc^2/\hbar$ [振荡](@entry_id:267781)，振幅为光速 $c$。这个频率对应于正[负能量](@entry_id:161542)态之间的[能隙](@entry_id:191975)。这是一种纯粹的相对论量子效应，通常由于频率太高而难以直接观测。

#### [马约拉纳旋量](@entry_id:193020)
除了我们一直讨论的（复数）[狄拉克旋量](@entry_id:181944)外，理论上还可以存在一种特殊的（实数）旋量，称为[马约拉纳旋量](@entry_id:193020)。[马约拉纳旋量](@entry_id:193020) $\psi_M$ 的定义是它等于其自身的[电荷共轭](@entry_id:158278)：
$$
\psi_M = \psi_M^c = C \bar{\psi}_M^T
$$
这意味着[马约拉纳粒子](@entry_id:157721)是其自身的反粒子。

[马约拉纳旋量](@entry_id:193020)的一个根本性质是其守恒的U(1)矢量流 $J^\mu = \bar{\psi}\gamma^\mu\psi$ 恒为零。这可以利用旋量[双线性](@entry_id:146819)的[电荷共轭](@entry_id:158278)性质来证明。对于任意两个[狄拉克旋量](@entry_id:181944) $\psi_1$ 和 $\psi_2$，存在一个恒等式：$\bar{\psi}_1 \gamma^\mu \psi_2 = -\overline{(\psi_2^c)} \gamma^\mu (\psi_1^c)$。对于[马约拉纳旋量](@entry_id:193020)，我们有 $\psi_M = \psi_M^c$。将 $\psi_1$ 和 $\psi_2$ 都设为 $\psi_M$，该恒等式变为：
$$
J^\mu = \bar{\psi}_M \gamma^\mu \psi_M = - \overline{\psi_M} \gamma^\mu \psi_M = -J^\mu
$$
这意味着 $2J^\mu = 0$，因此 $J^\mu = 0$ [@problem_id:390927]。这个结果意义重大。它表明[马约拉纳费米子](@entry_id:137199)不能携带任何守恒的U(1)荷，如[电荷](@entry_id:275494)。这使它们与[狄拉克费米子](@entry_id:161484)（如电子）有着本质的区别，并使它们成为中微子和暗物质等[电中性](@entry_id:157680)粒子的候选者。