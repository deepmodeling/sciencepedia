## 引言
狄拉克方程是现代物理学的基石之一，它首次成功地将量子力学与狭义相对论相结合，为描述电子等自旋$1/2$的费米子提供了坚实的理论框架。这一方程不仅精确地解释了电子的许多性质，还带来了诸如内禀自旋和反物质等革命性的预言，深刻地改变了我们对物质世界的理解。然而，理解狄拉克方程的全部威力，始于剖析其最基本的情形：自由粒子的解。这些解虽然理想化，却蕴含着理论的全部核心物理，并构成了处理更复杂相互作用问题的出发点。本文旨在系统地梳理和阐释狄拉克方程的自由粒子解，填补从抽象方程到具体物理图像之间的知识鸿沟。

本文将引导读者深入探索自由粒子解的奥秘。在“原理和机制”一章中，我们将从狄拉克方程的结构出发，推导静止和运动粒子的解，并揭示负能量态、反物质、内禀自旋和洛伦兹协变性等深刻的物理原理。接着，在“应用与跨学科联系”一章中，我们将展示这些基础解如何作为强大的工具，应用于量子场论的散射计算、强子物理的口袋模型，并启发了对马约拉纳费米子等前沿概念的探索。最后，“动手实践”部分将提供具体的计算问题，帮助读者将理论知识转化为解决实际问题的能力。通过这一系列的学习，读者将对相对论性量子力学的基础有更坚固和深入的理解。

## 原理和机制

在前一章中，我们介绍了狄拉克方程的起源及其作为相对论性量子力学基本方程的重要性。本章将深入探讨其核心内容：自由粒子解的结构、性质及其物理诠释。我们将从最简单的情形出发，逐步构建出描述具有任意动量的自旋$1/2$粒子的完整解决方案，并揭示这些解所蕴含的深刻物理原理，如内禀自旋、负能量态、反物质的存在以及洛伦兹协变性等。

### 狄拉克方程与相对论能量-动量关系

狄拉克方程的标准协变形式为：

$$
(i\hbar\gamma^\mu \partial_\mu - mc)\psi(x) = 0
$$

其中，$\psi(x)$ 是一个四分量旋量场，$\gamma^\mu$ 是四个 $4 \times 4$ 的狄拉克矩阵，$\partial_\mu = \frac{\partial}{\partial x^\mu}$ 是四维梯度算符。在自然单位制中（$\hbar = c = 1$），方程简化为 $(i\gamma^\mu \partial_\mu - m)\psi = 0$。

该方程的一个核心特征是它对时空坐标是一阶线性的，这与非相对论的薛定谔方程相似，但与二阶的克莱因-戈登方程不同。狄拉克最初的动机正是要构建一个满足相对论协变性的一阶波动方程。为了验证狄拉克方程确实符合相对论的能量-动量关系 $E^2 = p^2c^2 + m^2c^4$，我们可以考察将狄拉克算符作用两次的效果。

考虑算符 $(i\gamma^\nu \partial_\nu + m)$ 作用在狄拉克方程上：

$$
(i\gamma^\nu \partial_\nu + m)(i\gamma^\mu \partial_\mu - m)\psi = 0
$$

展开左侧，我们得到：

$$
( (i\gamma^\nu \partial_\nu)(i\gamma^\mu \partial_\mu) - m^2 )\psi = (-\gamma^\nu\gamma^\mu \partial_\nu\partial_\mu - m^2)\psi = 0
$$

注意到交叉项 $(i\gamma^\nu \partial_\nu)(-m)$ 和 $(m)(i\gamma^\mu \partial_\mu)$ 由于 $\gamma^\mu$ 和 $m$ 是常数而相互抵消。这里的关键在于处理 $\gamma^\nu\gamma^\mu$ 这一项。我们可以将其分解为对称和反对称部分：

$$
\gamma^\nu\gamma^\mu = \frac{1}{2}(\gamma^\nu\gamma^\mu + \gamma^\mu\gamma^\nu) + \frac{1}{2}(\gamma^\nu\gamma^\mu - \gamma^\mu\gamma^\nu) = \frac{1}{2}\{\gamma^\nu, \gamma^\mu\} + \frac{1}{2}[\gamma^\nu, \gamma^\mu]
$$

由于偏导数可以交换顺序（$\partial_\nu\partial_\mu = \partial_\mu\partial_\nu$），当与 $\partial_\nu\partial_\mu$ 相乘时，只有对称部分（反对易子）有贡献。根据定义 $\gamma$ 矩阵满足的**克利福德代数**关系 $\{\gamma^\mu, \gamma^\nu\} = 2\eta^{\mu\nu}I_4$，其中 $\eta^{\mu\nu}$ 是闵可夫斯基度规张量（我们采用 $(+,-,-,-)$ 符号），我们有：

$$
\gamma^\nu\gamma^\mu \partial_\nu\partial_\mu = \frac{1}{2}\{\gamma^\nu, \gamma^\mu\} \partial_\nu\partial_\mu = \frac{1}{2}(2\eta^{\mu\nu})\partial_\mu\partial_\nu = \eta^{\mu\nu}\partial_\mu\partial_\nu = \partial^\mu\partial_\mu \equiv \Box
$$

其中 $\Box$ 是达朗贝尔算符。因此，狄拉克方程的“平方”形式还原为：

$$
(-\Box - m^2)\psi = 0 \quad \Rightarrow \quad (\Box + m^2)\psi = 0
$$

这正是克莱因-戈登方程。这表明狄拉克旋量的每个分量都自动满足相对论的能量-动量关系，证实了狄拉克方程的相对论自洽性 [@problem_id:2095192]。正是 $\gamma$ 矩阵的代数结构，而非其具体表示，保证了这一根本性质。

### 静止粒子的解与负能量态

理解自由粒子解最简单的方法是从粒子静止的参考系开始。在这种情况下，粒子的三维动量 $\vec{p} = 0$。动量空间中的狄拉克方程 $(\gamma^\mu p_\mu - m)\psi = 0$ 变得格外简单。此时四维动量为 $p^\mu = (E, \vec{0})$，方程简化为：

$$
(\gamma^0 E - m)\psi = 0
$$

为了求解这个矩阵方程，我们需要选择一个 $\gamma$ 矩阵的具体表示。在标准的狄拉克-泡利表示中：

$$
\gamma^0 = \begin{pmatrix} I  0 \\ 0  -I \end{pmatrix}, \quad \gamma^k = \begin{pmatrix} 0  \sigma_k \\ -\sigma_k  0 \end{pmatrix}
$$

其中 $I$ 是 $2 \times 2$ 单位矩阵，$\sigma_k$ 是泡利矩阵。将四分量旋量 $\psi$ 分解为两个二分量旋量（旋量-旋量） $u_A$ 和 $u_B$：

$$
\psi = \begin{pmatrix} u_A \\ u_B \end{pmatrix}
$$

代入静止时的狄拉克方程，我们得到：

$$
\begin{pmatrix} E \cdot I - m \cdot I  0 \\ 0  -E \cdot I - m \cdot I \end{pmatrix} \begin{pmatrix} u_A \\ u_B \end{pmatrix} = \begin{pmatrix} (E-m)u_A \\ -(E+m)u_B \end{pmatrix} = 0
$$

这个矩阵方程分解为两个独立的方程：
1.  $(E-m)u_A = 0$
2.  $(E+m)u_B = 0$

要得到非零解，必须满足以下两种情况之一：
- **情况 1：正能量解**
  $E = m$（在标准单位中为 $mc^2$）。此时，为了满足第二个方程，必须有 $u_B = 0$。而 $u_A$ 可以是任意的二分量旋量。我们可以选择一组标准正交基，例如自旋向上 $\chi_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 和自旋向下 $\chi_2 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$。这给出了两个线性无关的正能量解。

- **情况 2：负能量解**
  $E = -m$（在标准单位中为 $-mc^2$）。此时，第一个方程要求 $u_A = 0$。而 $u_B$ 可以是任意的二分量旋量。同样选择 $\chi_1$ 和 $\chi_2$作为基，我们得到两个线性无关的负能量解。

综上所述，对于一个静止的自由粒子，狄拉克方程存在四个线性无关的解 [@problem_id:2095231]：
- **正能量解 ($E = mc^2$)**:
  $$
  \psi^{(1)} = \begin{pmatrix} \chi_1 \\ 0 \end{pmatrix}, \quad \psi^{(2)} = \begin{pmatrix} \chi_2 \\ 0 \end{pmatrix}
  $$
- **负能量解 ($E = -mc^2$)**:
  $$
  \psi^{(3)} = \begin{pmatrix} 0 \\ \chi_1 \end{pmatrix}, \quad \psi^{(4)} = \begin{pmatrix} 0 \\ \chi_2 \end{pmatrix}
  $$

负能量解的出现是狄拉克方程一个不可避免的推论，并曾一度引发理论上的困惑。狄拉克提出了一个革命性的诠释，即所谓的**狄拉克海**。他假设真空并非空无一物，而是所有负能量态都已被电子填满。根据泡利不相容原理，一个正能量电子无法跃迁到这些已被占据的负能量态。然而，如果一个高能光子（能量至少为 $2mc^2$）将一个负能量海中的电子激发到正能量态，这个电子就成为一个可观测的普通电子。同时，负能量海中留下的“空穴”表现为一个具有相同质量但电荷相反的粒子——反粒子（正电子）。

这个模型预言了从负能量态连续谱的顶端（$-mc^2$）到正能量态连续谱的底端（$+mc^2$）之间存在一个能隙。这个能隙的大小为 $\Delta E = (+mc^2) - (-mc^2) = 2mc^2$。对于电子而言，其静止质量 $m_e \approx 9.11 \times 10^{-31}$ kg，这个能隙大约是 $1.02$ MeV [@problem_id:2095229]。这恰好是电子-正电子对产生的阈值能量，为狄拉克的反物质预言提供了强有力的理论支持。

### 运动粒子的解

现在我们来构建描述具有非零动量 $\vec{p}$ 的自由粒子的解。有两种等价的方法可以实现这一点：直接代数求解或通过洛伦兹变换。

#### 代数方法

我们再次从动量空间方程 $(\gamma^\mu p_\mu - m)u(p) = 0$ 出发，其中 $p^\mu = (E, \vec{p})$ 且 $E = \sqrt{|\vec{p}|^2 + m^2}$。在狄拉克-泡利表示中，$\gamma^\mu p_\mu$ 算符可以写成块矩阵形式：

$$
\gamma^\mu p_\mu = \gamma^0 p_0 + \gamma^k p_k = \gamma^0 E - \vec{\gamma} \cdot \vec{p} = \begin{pmatrix} E \cdot I  -\vec{\sigma}\cdot\vec{p} \\ \vec{\sigma}\cdot\vec{p}  -E \cdot I \end{pmatrix}
$$

将 $u(p) = \begin{pmatrix} u_A \\ u_B \end{pmatrix}$ 代入，狄拉克方程变为：

$$
\begin{pmatrix} E \cdot I - m \cdot I  -\vec{\sigma}\cdot\vec{p} \\ \vec{\sigma}\cdot\vec{p}  -E \cdot I - m \cdot I \end{pmatrix} \begin{pmatrix} u_A \\ u_B \end{pmatrix} = 0
$$

这给出了两个耦合的二分量旋量方程：
1.  $(E-m)u_A - (\vec{\sigma}\cdot\vec{p})u_B = 0$
2.  $(\vec{\sigma}\cdot\vec{p})u_A - (E+m)u_B = 0$

对于正能量解，$E+m \neq 0$，我们可以从第二个方程解出 $u_B$：

$$
u_B = \frac{\vec{\sigma}\cdot\vec{p}}{E+m} u_A
$$

这个关系式表明，对于一个运动的粒子，其旋量的下半部分 ($u_B$) 由上半部分 ($u_A$) 和粒子的动量唯一确定 [@problem_id:2095185]。上半部分 $u_A$ 依然代表了粒子的自旋自由度。因此，对于一个给定的动量 $\vec{p}$，我们有两个线性无关的正能量解，对应于 $u_A$ 取为自旋向上和自旋向下的二分量旋量。

#### 洛伦兹变换方法

一个更深刻且更体现协变性的方法，是通过洛伦兹变换从静止解中构造出运动解。狄拉克方程是洛伦兹协变的，这意味着在不同惯性系下观察到的旋量场之间通过一个特定的变换矩阵 $S(\Lambda)$ 相关联：$\psi'(x') = S(\Lambda)\psi(x)$，其中 $x'=\Lambda x$。

对于一个从静止系到动量为 $\vec{p}$ 的参考系的纯提升（boost），变换算符 $S(\Lambda)$ 可以表示为：

$$
S(\Lambda) = \exp\left(-\frac{1}{2}\omega_{\mu\nu}S^{\mu\nu}\right)
$$

其中 $S^{\mu\nu} = \frac{i}{4}[\gamma^\mu, \gamma^\nu]$ 是洛伦兹群的生成元，$\omega_{\mu\nu}$ 是变换参数。对于一个沿 $z$ 轴方向，速度为 $v=p_z/E$ 的提升，这可以简化为 $S(\Lambda_z) = \exp(\frac{\zeta}{2}\alpha_z)$，其中 $\zeta = \text{arctanh}(p_z/E)$ 是快度，$\alpha_z = \gamma^0\gamma^z$ [@problem_id:2095172]。

利用 $(\alpha_z)^2 = I$ 的性质，指数函数可以展开为：

$$
S(\Lambda_z) = \cosh(\zeta/2) \cdot I + \sinh(\zeta/2) \cdot \alpha_z
$$

将这个算符作用于静止时的自旋向上解 $u_\uparrow(0)$，并利用与能量和动量相关的双曲函数恒等式，如 $\cosh(\zeta/2) = \sqrt{(E+m)/2m}$ 和 $\sinh(\zeta/2) = p_z / \sqrt{2m(E+m)}$，我们可以精确地导出运动粒子的旋量形式。例如，对于一个沿 $z$ 轴运动的自旋向上粒子，其旋量为 [@problem_id:2095172]：

$$
u_\uparrow(p_z) = \begin{pmatrix} \sqrt{E+m} \cdot \chi_\uparrow \\ \frac{p_z}{\sqrt{E+m}} \cdot \chi_\uparrow \end{pmatrix} = \begin{pmatrix} \sqrt{E+m} \\ 0 \\ \frac{p_z}{\sqrt{E+m}} \\ 0 \end{pmatrix}
$$

这与代数方法得到的结果完全一致，并突出了狄拉克解在洛伦兹变换下的优雅结构。

最终，我们可以写出四组标准化的平面波解：两组正能量解 $u^{(s)}(p)$ 和两组负能量解 $v^{(s)}(p)$，它们构成了自由狄拉克方程解的完备集。

### 解的性质与物理诠释

#### 洛伦兹协变性与标量密度

物理定律不应依赖于观察者的惯性参考系。在狄拉克理论中，这意味着由旋量构造的可观测量必须具有明确的洛伦兹变换性质。一个基本的构造是**标量密度** $\bar{\psi}\psi$。

首先，我们定义**狄拉克伴随旋量**为 $\bar{\psi} = \psi^\dagger \gamma^0$。在洛伦兹变换下，旋量 $\psi$ 变为 $\psi' = S(\Lambda)\psi$。可以证明，伴随旋量的变换规律是：

$$
\bar{\psi}' = (\psi')^\dagger \gamma^0 = (S(\Lambda)\psi)^\dagger \gamma^0 = \psi^\dagger S(\Lambda)^\dagger \gamma^0
$$

利用 $\gamma$ 矩阵代数中的一个重要恒等式 $S(\Lambda)^{-1} = \gamma^0 S(\Lambda)^\dagger \gamma^0$，我们可以得到：

$$
\bar{\psi}' = \psi^\dagger \gamma^0 (\gamma^0 S(\Lambda)^\dagger \gamma^0) = \bar{\psi} S(\Lambda)^{-1}
$$

现在我们来考察标量密度 $\bar{\psi}\psi$ 在变换下的行为：

$$
\bar{\psi}'\psi' = (\bar{\psi}S(\Lambda)^{-1})(S(\Lambda)\psi) = \bar{\psi}(S(\Lambda)^{-1}S(\Lambda))\psi = \bar{\psi}\psi
$$

这个结果表明，$\bar{\psi}\psi$ 是一个**洛伦兹标量**——它的值在所有惯性系中都是相同的 [@problem_id:2095219]。类似地，我们还可以构造其他协变对象，如协变流 $j^\mu = \bar{\psi}\gamma^\mu\psi$（一个四维矢量）等，它们是构建相互作用理论的基础。

#### 内禀自旋与角动量守恒

在非相对论量子力学中，轨道角动量 $\vec{L} = \vec{r} \times \vec{p}$ 对于中心势场是守恒的。然而，在狄拉克理论中，即使对于自由粒子，情况也并非如此。自由粒子的狄拉克哈密顿量为 $H_D = c\vec{\alpha} \cdot \vec{p} + \beta m c^2$。一个算符所对应的物理量是否守恒，取决于该算符是否与哈密顿量对易。

我们可以计算 $\vec{L}$ 与 $H_D$ 的对易子：

$$
[H_D, \vec{L}] = [c\vec{\alpha} \cdot \vec{p}, \vec{r} \times \vec{p}] = c\vec{\alpha} \cdot [\vec{p}, \vec{r} \times \vec{p}]
$$

利用算符对易关系，可以算出 $[H_D, \vec{L}] = i\hbar c (\vec{\alpha} \times \vec{p})$ [@problem_id:179498]。这个结果不为零，表明轨道角动量本身并不守恒。

然而，如果我们引入一个纯粹作用于旋量内部空间的算符，即**自旋算符** $\vec{S} = \frac{\hbar}{2}\vec{\Sigma}$，其中 $\vec{\Sigma} = \begin{pmatrix} \vec{\sigma}  0 \\ 0  \vec{\sigma} \end{pmatrix}$，并计算它与哈密顿量的对易子，会发现 $[H_D, \vec{S}] = -i\hbar c (\vec{\alpha} \times \vec{p})$。

惊人的是，$[H_D, \vec{L}]$ 和 $[H_D, \vec{S}]$ 两者之和恰好为零。这意味着总角动量 $\vec{J} = \vec{L} + \vec{S}$ 是守恒的：

$$
[H_D, \vec{J}] = [H_D, \vec{L} + \vec{S}] = 0
$$

这深刻地揭示了狄拉克方程自动包含了粒子的内禀角动量，即自旋。狄拉克粒子是一个内禀的自旋$1/2$粒子，其轨道运动和自旋之间存在耦合，只有两者的总和才是守恒量。

#### 手征性与螺旋性

**手征性**（Chirality）是与狄拉克旋量左右对称性相关的一个重要概念，由手征性算符 $\gamma^5 = i\gamma^0\gamma^1\gamma^2\gamma^3$ 来描述。$\gamma^5$ 的本征值为 $\pm 1$，分别对应右手和左手手征态。

一个物理量是否守恒，取决于其算符是否与哈密顿量对易。对于有质量的粒子，手征性不是一个守恒量。我们可以计算 $[H_D, \gamma^5]$：

$$
[H_D, \gamma^5] = [\vec{\alpha} \cdot \vec{p} + \beta m, \gamma^5]
$$

利用 $\gamma^5$ 与所有 $\gamma^\mu$ 反对易的性质（$\{\gamma^\mu, \gamma^5\}=0$），可以证明 $[\vec{\alpha}, \gamma^5]=0$ 但 $[\beta, \gamma^5] = 2\beta\gamma^5$。因此：

$$
[H_D, \gamma^5] = 2m\beta\gamma^5
$$

这个结果不为零，只要粒子质量 $m \neq 0$ [@problem_id:179470]。这意味着一个初始为纯右手征的粒子，在演化过程中会逐渐混合进左手征的分量。只有在无质量的极限下（$m=0$），手征性才守恒。在手征表示（Weyl representation）下，$\gamma^5$ 是对角的，质量项 $m\beta = m\gamma^0$ 显式地耦合了左右手征分量 [@problem_id:179463]，从而直观地解释了手征性不守恒的原因。

需要将手征性与**螺旋性**（Helicity）区分开。螺旋性是自旋在动量方向上的投影，由算符 $\vec{S} \cdot \vec{p} / |\vec{p}|$ 描述。对于有质量的粒子，可以通过洛伦兹变换到比粒子运动更快的参考系来改变动量方向，从而改变螺旋性。因此，螺旋性不是洛伦兹不变量。只有对于以光速运动的无质量粒子，螺旋性才是一个洛伦兹不变量，并与手征性等同。

### 对称性与粒子-反粒子诠释

#### 电荷共轭

狄拉克海的图像暗示了粒子和反粒子之间的深刻对称性。这种对称性在数学上通过**电荷共轭**（Charge Conjugation）变换 $C$ 来体现。电荷共轭的目的是将描述带电荷 $q$ 粒子的波动方程，转换为描述带电荷 $-q$ 粒子的方程。

对于自由粒子，电荷共轭变换将一个粒子解与一个反粒子解联系起来。该变换定义为：
$$
\psi_c(x) = i\gamma^2 \psi^*(x)
$$
其中 $\psi^*(x)$ 是 $\psi(x)$ 的复共轭。我们来考察这个变换对一个正能量平面波解 $\psi_p(x) = u(p) e^{-ip\cdot x/\hbar}$ 的作用。经过一系列计算，可以发现变换后的波函数 $\psi_c(x)$ 的时空依赖性变为 $e^{+ip\cdot x/\hbar}$ [@problem_id:2095225]。

$$
e^{+ip\cdot x/\hbar} = e^{+i(Et - \vec{p}\cdot\vec{x})/\hbar} = e^{-i(-E t - (-\vec{p})\cdot\vec{x})/\hbar} = e^{-i(-p)\cdot x/\hbar}
$$

这意味着，如果 $\psi_p(x)$ 描述一个四维动量为 $p^\mu = (E, \vec{p})$ 的粒子态，那么 $\psi_c(x)$ 就对应一个四维动量为 $-p^\mu = (-E, -\vec{p})$ 的态。一个具有正能量 $E$ 的粒子解，通过电荷共轭变换，变成了一个具有负能量 $-E$ 和反向动量 $-\vec{p}$ 的解。

这正是反粒子诠释的关键：一个能量为 $-E$、动量为 $-\vec{p}$ 的负能量粒子解，在物理上被重新诠释为描述一个能量为 $+E$、动量为 $+\vec{p}$ 的**反粒子**。因此，负能量解 $v(p)$ 实际上描述的是具有物理动量 $p$ 和能量 $E$ 的反粒子。电荷共轭对称性是粒子物理标准模型的一个基石。

#### Zitterbewegung (颤动)

狄拉克方程的单粒子诠释并非没有困难。一个著名的例子就是所谓的**Zitterbewegung**（德语，意为“颤动”）。这种现象源于正能量解和负能量解的叠加。

考虑一个处于静止状态的粒子，其初始波函数是正能量自旋向上态 $u_1(0)$ 和负能量自旋向上态 $v_1(0)$ 的等量叠加 [@problem_id:179469]：

$$
|\psi(0)\rangle = \frac{1}{\sqrt{2}}(u_1(0) + v_1(0))
$$

随时间演化，该态变为：

$$
|\psi(t)\rangle = \frac{1}{\sqrt{2}}(u_1(0)e^{-imc^2t/\hbar} + v_1(0)e^{+imc^2t/\hbar})
$$

现在我们计算速度算符 $\hat{v}_z = c\alpha_z$ 的期望值。由于 $\alpha_z$ 算符只连接上下分量（即正负能量解），对角项 $\langle u_1|\alpha_z|u_1\rangle$ 和 $\langle v_1|\alpha_z|v_1\rangle$ 均为零。非对角项（交叉项）则不为零，并导致：

$$
\langle \hat{v}_z \rangle(t) \propto \cos\left(\frac{2mc^2}{\hbar}t\right)
$$

速度期望值以一个极高的角频率 $\Omega = 2mc^2/\hbar$ 振荡。对于电子，这个频率约为 $1.6 \times 10^{21}$ Hz。这种超快的虚拟振荡，其振幅约为康普顿波长 $\hbar/mc$，被视为电子与狄拉克海中的虚正电子-电子对相互作用的结果。它揭示了在极小的时间和空间尺度上，严格的单粒子图像开始失效，量子场论的多体图像变得必要。

本章我们系统地剖析了自由狄拉克方程的解，从静止到运动，从其代数结构到其物理内涵。这些解不仅成功地描述了自旋$1/2$粒子的行为，还预言了反物质的存在，并为量子场论的建立奠定了坚实的基础。