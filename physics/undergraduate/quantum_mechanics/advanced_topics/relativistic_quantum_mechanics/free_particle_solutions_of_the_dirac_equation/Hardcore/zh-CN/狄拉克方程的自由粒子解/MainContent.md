## 引言
狄拉克方程是量子力学发展史上的一个里程碑，它首次成功地将狭义相对论与量子理论融合，为描述电子等自旋-1/2的费米子提供了坚实的理论框架。然而，方程本身所蕴含的深刻物理内涵，远不止于形式上的协变性。理解其最基本的解——自由粒子解，是揭开反物质之谜、阐明自旋的相对论起源以及构建现代量子场论的关键一步。本文旨在系统性地剖析狄拉克方程的自由粒子解，填补从基本方程到其物理现象和应用的知识鸿沟，引领读者深入探索相对论量子世界的奇妙景观。

在接下来的内容中，你将学习到：
- **原理与机制**：我们将从狄拉克方程本身出发，推导其平面波解，重点分析正能态与负能态的出现。通过探讨静止系和运动系中的解，我们将揭示反物质（狄拉克海）的理论起源，并阐明手征性、螺旋性等关键概念及其与粒子质量的关系。
- **应用与跨学科联系**：本章将展示自由粒子解如何作为构建物理可观测量（如守恒流）的基础，并预言了“颤动”等独特的相对论效应。我们将探讨这些解在粒子物理、原子物理中的应用，并说明其如何成为量子场论中进行散射计算的强大工具。
- **动手实践**：通过一系列精心设计的计算练习，你将有机会亲手验证狄拉克矩阵的代数性质，并探索手征性与螺旋性在不同物理极限下的具体表现，从而巩固理论知识，提升解决实际问题的能力。

让我们开始进入狄拉克方程优雅而强大的世界。

## 原理与机制

在上一章中，我们介绍了狄拉克方程的提出背景及其作为描述自旋为 $1/2$ 的相对论性粒子的基本框架。本章我们将深入探讨该方程的自由粒子解，揭示其内在结构、物理诠释以及深刻的对称性。我们将从最基本的原理出发，系统地构建这些解，并阐明它们所蕴含的革命性概念，如反物质的存在和手征性的物理意义。

### 狄拉克算符与相对论能量-动量关系

自由粒子的狄拉克方程以其简洁而深刻的形式出现（在自然单位制 $\hbar=c=1$ 中）：
$$
(i\gamma^\mu \partial_\mu - m)\psi(x) = 0
$$
其中 $\psi(x)$ 是四分量狄拉克旋量场，$\gamma^\mu$ 是满足克利福德代数 $\{\gamma^\mu, \gamma^\nu\} = 2g^{\mu\nu}I_4$ 的 $4 \times 4$ 矩阵，$g^{\mu\nu}$ 是闵可夫斯基度规（我们采用 $(+,-,-,-)$ 号差）。这个方程的一个核心特征是，它是一阶偏微分方程，这与非相对论的薛定谔方程类似，但其解必须同时满足狭义相对论的基本要求。

为了验证这一点，我们可以探究狄拉克算符与描述标量场的相对论性克莱因-戈登方程算符之间的联系。克莱因-戈登方程 $(\partial^\mu\partial_\mu + m^2)\phi=0$ 体现了相对论能量-动量关系 $E^2 = p^2 + m^2$。狄拉克通过寻找该关系的一个“平方根”而受到了启发。我们可以通过将一个类狄拉克算符与其“共轭”算符相乘来重现这个过程。

考虑一个广义的狄拉克算符 $\mathcal{D}_- = i\alpha\gamma^\mu \partial_\mu - \beta m$，以及其伴随算符 $\mathcal{D}_+ = i\alpha\gamma^\mu \partial_\mu + \beta m$，其中 $\alpha$ 和 $\beta$ 是实常数。它们的乘积作用在一个旋量场上时，会发生什么呢？
$$
\mathcal{D}_+ \mathcal{D}_- = (i\alpha\gamma^\mu \partial_\mu + \beta m)(i\alpha\gamma^\nu \partial_\nu - \beta m)
$$
展开此表达式，由于常数矩阵与偏导数可交换，交叉项 $(i\alpha\gamma^\mu \partial_\mu)(-\beta m) + (\beta m)(i\alpha\gamma^\nu \partial_\nu)$ 会相互抵消。剩下的项为：
$$
\mathcal{D}_+ \mathcal{D}_- = (i\alpha)^2 (\gamma^\mu \gamma^\nu \partial_\mu \partial_\nu) - (\beta m)^2 = -\alpha^2 \gamma^\mu \gamma^\nu \partial_\mu \partial_\nu - \beta^2 m^2
$$
由于导数算符 $\partial_\mu$ 和 $\partial_\nu$ 可交换，我们可以利用 $\gamma$ 矩阵的代数性质。将 $\gamma^\mu \gamma^\nu$ 分解为其对称和反对称部分：$\gamma^\mu \gamma^\nu = \frac{1}{2}(\gamma^\mu \gamma^\nu + \gamma^\nu \gamma^\mu) + \frac{1}{2}(\gamma^\mu \gamma^\nu - \gamma^\nu \gamma^\mu)$。由于 $\partial_\mu \partial_\nu$ 对指标 $\mu,\nu$ 是对称的，只有对称部分（即反对易子）会留下非零贡献：
$$
\gamma^\mu \gamma^\nu \partial_\mu \partial_\nu = \frac{1}{2}\{\gamma^\mu, \gamma^\nu\} \partial_\mu \partial_\nu = \frac{1}{2}(2g^{\mu\nu}) \partial_\mu \partial_\nu = g^{\mu\nu}\partial_\mu \partial_\nu = \partial^\mu \partial_\mu
$$
这里的 $\partial^\mu \partial_\mu$ 正是达朗贝尔算符。因此，我们得到：
$$
\mathcal{D}_+ \mathcal{D}_- = -\alpha^2 \partial^\mu \partial_\mu - \beta^2 m^2 = -\alpha^2(\partial^\mu \partial_\mu + \frac{\beta^2}{\alpha^2} m^2)
$$
这个结果表明，狄拉克算符的平方确实与克莱因-戈登算符成正比 [@problem_id:2095192]。对于标准的狄拉克方程，$\alpha = \beta = 1$，此时 $(i\gamma^\mu \partial_\mu + m)(i\gamma^\mu \partial_\mu - m) = -(\partial^\mu\partial_\mu + m^2)$。这意味着狄拉克方程的任何解 $\psi$ 的每一个分量都自动成为克莱因-戈登方程的解。这保证了狄拉克粒子严格遵守相对论的能量-动量关系。

### 自由粒子的平面波解

为了求解自由粒子的狄拉克方程，我们采用平面波 ansatz，这是解决具有时空平移不变性问题的标准方法。我们将解写成：
$$
\psi(x) = \omega(p, \epsilon) \exp(-i \epsilon p \cdot x)
$$
这里，$p^\mu = (E, \vec{p})$ 是粒子的四维动量，其中 $E = \sqrt{|\vec{p}|^2 + m^2}$ 是正能量解。$\omega(p, \epsilon)$ 是一个依赖于动量 $p$ 的四分量常数旋量。参数 $\epsilon$ 用于统一处理粒子和反粒子：$\epsilon=+1$ 对应正能解，此时旋量记为 $u(p)$；$\epsilon=-1$ 对应负能解，旋量记为 $v(p)$。

将此 ansatz 代入狄拉克方程 $(i\gamma^\mu \partial_\mu - m)\psi = 0$，导数算符作用在指数上：
$$
\partial_\mu \psi(x) = -i\epsilon p_\mu \psi(x)
$$
其中 $p_\mu = g_{\mu\nu}p^\nu = (E, -\vec{p})$。代入后，微分方程转化为一个纯代数方程 [@problem_id:2095169]：
$$
(i\gamma^\mu (-i\epsilon p_\mu) - m) \omega(p, \epsilon) = 0 \implies (\epsilon \gamma^\mu p_\mu - m)\omega(p, \epsilon) = 0
$$
这个方程通常被称为动量空间中的狄拉克方程。它是一个关于旋量 $\omega$ 的齐次线性方程组，其系数矩阵依赖于粒子的动量。

#### 静止系中的解与反粒子

求解上述代数方程最简单的情形是粒子处于静止系，即三维动量 $\vec{p} = 0$。此时，四维动量为 $p^\mu=(m, \vec{0})$，因此 $p_\mu=(m, \vec{0})$。动量空间狄拉克方程简化为：
$$
(\gamma^0 E - m)\psi = 0
$$
其中 $E$ 是静止能量。在狄拉克-泡利表象下，$\gamma^0 = \begin{pmatrix} I  0 \\ 0  -I \end{pmatrix}$，其中 $I$ 是 $2 \times 2$ 单位矩阵。将旋量 $\psi$ 分解为两个二分量旋量（旋量-旋量）$\phi$ 和 $\chi$，即 $\psi = \begin{pmatrix} \phi \\ \chi \end{pmatrix}$，方程变为：
$$
\begin{pmatrix} E \cdot I - m \cdot I  0 \\ 0  -E \cdot I - m \cdot I \end{pmatrix} \begin{pmatrix} \phi \\ \chi \end{pmatrix} = 0
$$
这给出了两个解耦的方程组：
1.  $(E - m)\phi = 0$
2.  $-(E + m)\chi = 0$

为了得到非零解，我们有两种可能 [@problem_id:2095231]：
- **正能解**: 必须有 $E = +m$ (在 $c=1$ 单位下)。此时，第二个方程变为 $-2m\chi = 0$，意味着 $\chi$ 必须为零。而 $\phi$ 可以是任意的二分量旋量。我们可以选择一组标准基，例如自旋向上 $\chi_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 和自旋向下 $\chi_2 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$。这给出了两个线性无关的正能解：
  $$
  \psi^{(1)} = \begin{pmatrix} \chi_1 \\ 0 \end{pmatrix}, \quad \psi^{(2)} = \begin{pmatrix} \chi_2 \\ 0 \end{pmatrix} \quad \text{对应能量 } E = +m
  $$

- **负能解**: 必须有 $E = -m$。此时，第一个方程变为 $-2m\phi = 0$，意味着 $\phi$ 必须为零。而 $\chi$ 可以是任意的。同样选择一组基，我们得到两个线性无关的负能解：
  $$
  \psi^{(3)} = \begin{pmatrix} 0 \\ \chi_1 \end{pmatrix}, \quad \psi^{(4)} = \begin{pmatrix} 0 \\ \chi_2 \end{pmatrix} \quad \text{对应能量 } E = -m
  $$

因此，对于静止的自由粒子，狄拉克方程预言了四种状态：两种具有正能量（粒子），对应自旋向上和向下；两种具有负能量（反粒子），也对应自旋向上和向下。负能解的出现是相对论量子力学的一个不可避免的推论，它带来了巨大的理论挑战和机遇。

#### 负能态与狄拉克海

负能量态的存在似乎意味着系统不稳定：一个正能量的电子可以通过辐射光子而跃迁到能量更低的负能态，乃至无限深的能级，这将导致所有物质在瞬间湮灭。为了解决这个灾难，狄拉克提出了一个大胆的假设，即**狄拉克海**理论。

他假设，物理上的真空并非真正的“空”，而是所有负能量态都已经被电子填满的状态。根据泡利不相容原理，每个量子态只能容纳一个费米子，因此一个处于正能量态的电子无法跃迁到已经被占据的负能海中。这样，真空就变得稳定了。

这个看似奇特的图像却做出了惊人的预言。如果一个能量足够大的光子（$\gamma$）与真空相互作用，它可以将一个负能海中的电子激发到一个正能量态。这个被激发的电子就成为我们可观测到的普通电子。同时，它在负能海中留下了一个“空穴”。这个空穴相对于填满的负能海而言，表现得像一个具有正电荷（因为缺少了负电荷）和正能量（因为它需要能量来“填补”这个空穴）的粒子。这个空穴就是电子的**反粒子**——正电子。

这个过程被称为**电子对产生**（pair production）。从能量守恒的角度看，要将一个电子从能量谱的顶端（最高负能级 $-mc^2$）提升到能量谱的底端（最低正能级 $+mc^2$），光子必须提供的最小能量等于这两个能级之间的能量差 [@problem_id:2095229]：
$$
\Delta E_{\text{min}} = (+mc^2) - (-mc^2) = 2mc^2
$$
对于电子，其静止质量 $m_e \approx 9.109 \times 10^{-31}$ kg，对应的静止能量 $m_e c^2 \approx 0.511$ MeV。因此，产生一对正负电子所需的最小能量约为 $1.022$ MeV。这一预言在1932年由 Carl Anderson 在宇宙射线实验中发现正电子而得到证实，这是理论物理学史上最辉煌的成就之一。

### 运动粒子的解

现在我们转向更一般的情况，即粒子具有非零动量 $\vec{p}$。动量空间狄拉克方程 $(\gamma^\mu p_\mu - m)\omega = 0$ 展开为块矩阵形式为 [@problem_id:2095169]：
$$
\begin{pmatrix} (E-m)I  -\vec{\sigma}\cdot\vec{p} \\ \vec{\sigma}\cdot\vec{p}  (-E-m)I \end{pmatrix} \begin{pmatrix} \phi \\ \chi \end{pmatrix} = 0
$$
这对应于两个耦合的方程：
$$
(E-m)\phi = (\vec{\sigma}\cdot\vec{p})\chi
$$
$$
(\vec{\sigma}\cdot\vec{p})\phi = (E+m)\chi
$$
从第二个方程，我们可以直接得到上下旋量分量之间的关系：
$$
\chi = \frac{\vec{\sigma}\cdot\vec{p}}{E+m} \phi
$$

#### 非相对论极限

这个关系式在非相对论极限下具有清晰的物理意义。在非相对论极限中，动能远小于静止能量，即 $|\vec{p}| \ll m$。此时，总能量 $E = \sqrt{|\vec{p}|^2 + m^2} \approx m + \frac{|\vec{p}|^2}{2m}$。因此，$E+m \approx 2m$。代入上述关系式，我们得到 [@problem_id:2095222]：
$$
\chi \approx \frac{\vec{\sigma}\cdot\vec{p}}{2m} \phi
$$
由于 $|\vec{p}|/m \approx v$ (速度)，$\chi$ 的大小相对于 $\phi$ 大约是 $v/c$ 的量级（恢复 $c$ 后）。因此，在低速情况下，下半部分的旋量 $\chi$ 是一个“小分量”，而上半部分的 $\phi$ 是“大分量”。这解释了为何在非相对论量子力学中，我们只需要一个二分量波函数（泡利旋量）就足以描述自旋。狄拉克理论在低能极限下自然地回归到了我们所熟悉的薛定谔-泡利理论。

#### 解的洛伦兹协变性

求解运动粒子的旋量，除了直接解代数方程，还有一个更具物理洞察力的方法：通过洛伦兹变换从静止解得到。狄拉克旋量在洛伦兹变换 $\Lambda$ 下的变换规则为 $\psi'(x') = S(\Lambda)\psi(x)$，其中 $x'=\Lambda x$，$S(\Lambda)$ 是洛伦兹群在旋量空间上的 $4 \times 4$ 表示矩阵。

对于一个沿 z 轴的助推（boost），其速度为 $v$，对应的 $S(\Lambda_z)$ 算符可以表示为：
$$
S(\Lambda_z) = \exp\left(\frac{\zeta}{2} \alpha_z\right)
$$
其中 $\zeta = \text{arctanh}(v)$ 是快度，$v=p_z/E$，而 $\alpha_z = \gamma^0 \gamma^z$。利用 $(\alpha_z)^2=I_4$ 的性质，指数函数可以展开为：
$$
S(\Lambda_z) = \cosh(\zeta/2) I_4 + \sinh(\zeta/2) \alpha_z
$$
现在，我们可以将此助推作用于一个静止的正能自旋向上态 $u_\uparrow(0)$ 上，以获得动量为 $p_z$ 的相应状态 $u_\uparrow(p_z)$ [@problem_id:2095172]。静止态（未归一化）为 $u_\uparrow(0) = \begin{pmatrix} 1 \\ 0 \\ 0 \\ 0 \end{pmatrix} = \begin{pmatrix} \chi_\uparrow \\ 0 \end{pmatrix}$。
经过一系列代数运算，并利用快度与能量、动量之间的关系式 $\cosh(\zeta/2) = \sqrt{\frac{E+m}{2m}}$ 和 $\sinh(\zeta/2) = \frac{p_z}{\sqrt{2m(E+m)}}$，我们可以得到助推后的旋量：
$$
u_\uparrow(p_z) = S(\Lambda_z) u_\uparrow(0) \propto \begin{pmatrix} \sqrt{E+m} \chi_\uparrow \\ \frac{p_z}{\sqrt{E+m}} \chi_\uparrow \end{pmatrix} = \begin{pmatrix} \sqrt{E+m} \\ 0 \\ \frac{p_z}{\sqrt{E+m}} \\ 0 \end{pmatrix}
$$
这个结果精确地展示了洛伦兹变换如何混合旋量的上下分量。在静止时纯粹是“大分量”的态，在运动时获得了“小分量”，其幅度与动量成正比，这与我们之前的分析完全一致。

### 协变流与洛伦兹不变量

为了从旋量解中构造可观测的物理量，如概率密度或流密度，我们需要构建在洛伦兹变换下具有确定变换性质的量（即协变张量）。在非相对论量子力学中，概率密度是 $\psi^\dagger \psi$。然而，在相对论框架下，$\psi^\dagger \psi$ 并不是一个洛伦兹标量，因为它在洛伦兹助推下会发生改变（由于时间膨胀效应）。

#### 狄拉克伴随旋量与伴随方程

正确的构造方式需要引入**狄拉克伴随旋量**（Dirac adjoint spinor），定义为：
$$
\bar{\psi} = \psi^\dagger \gamma^0
$$
这个定义并非随意选择，它恰好能保证我们构造出的双线性型具有良好的洛伦兹变换性质。要理解这一点，我们首先需要推导 $\bar{\psi}$ 所满足的方程。从狄拉克方程 $i\gamma^\mu \partial_\mu \psi - m\psi = 0$ 开始，取其厄米共轭：
$$
(i\gamma^\mu \partial_\mu \psi)^\dagger - (m\psi)^\dagger = 0 \implies -i(\partial_\mu \psi^\dagger)(\gamma^\mu)^\dagger - m\psi^\dagger = 0
$$
利用 $\gamma$ 矩阵的性质 $(\gamma^\mu)^\dagger = \gamma^0 \gamma^\mu \gamma^0$，方程变为：
$$
-i(\partial_\mu \psi^\dagger)\gamma^0 \gamma^\mu \gamma^0 - m\psi^\dagger = 0
$$
在方程右边乘以一个 $\gamma^0$，并利用 $(\gamma^0)^2=I$，我们得到：
$$
-i(\partial_\mu \psi^\dagger)\gamma^0 \gamma^\mu - m\psi^\dagger \gamma^0 = 0
$$
注意到 $\partial_\mu \bar{\psi} = (\partial_\mu \psi^\dagger)\gamma^0$，而 $m\bar{\psi} = m\psi^\dagger\gamma^0$，上式最终可以写成**伴随狄拉克方程** [@problem_id:2095178]：
$$
i(\partial_\mu \bar{\psi})\gamma^\mu + m\bar{\psi} = 0
$$
注意导数算符现在作用在 $\bar{\psi}$ 的左侧。

#### 标量密度：一个洛伦兹不变量

伴随旋量的美妙之处在于它的洛伦兹变换性质。如果 $\psi' = S(\Lambda)\psi$，那么 $\bar{\psi}'$ 的变换为：
$$
\bar{\psi}' = (\psi')^\dagger \gamma^0 = (S(\Lambda)\psi)^\dagger \gamma^0 = \psi^\dagger S(\Lambda)^\dagger \gamma^0
$$
利用关键关系 $S(\Lambda)^\dagger \gamma^0 = \gamma^0 S(\Lambda)^{-1}$（这是 $S(\Lambda)$ 作为洛伦兹群表示的一个基本性质），我们得到：
$$
\bar{\psi}' = \psi^\dagger \gamma^0 S(\Lambda)^{-1} = \bar{\psi} S(\Lambda)^{-1}
$$
现在，我们可以考察由 $\bar{\psi}$ 和 $\psi$ 构成的最简单的双线性型——**标量密度** $\bar{\psi}\psi$。在洛伦兹变换下，它变为 [@problem_id:2095219]：
$$
\bar{\psi}'\psi' = (\bar{\psi} S(\Lambda)^{-1}) (S(\Lambda)\psi) = \bar{\psi} (S(\Lambda)^{-1} S(\Lambda)) \psi = \bar{\psi}\psi
$$
这个结果表明，$\bar{\psi}\psi$ 是一个**洛伦兹标量**，即它在所有惯性系中都具有相同的值。这使其成为构建洛伦兹不变的拉格朗日量（如质量项 $m\bar{\psi}\psi$）的理想选择。同样，我们还可以构造一个四维矢量流 $j^\mu = \bar{\psi}\gamma^\mu\psi$，可以证明它是一个守恒的洛伦兹四维矢量，其零分量 $j^0 = \bar{\psi}\gamma^0\psi = \psi^\dagger\psi$ 正是概率密度。

### 手征性、螺旋性与质量

除了自旋，狄拉克粒子还具有另一个与“手性”相关的内在属性，称为**手征性**（Chirality）。

#### 手征性算符 $\gamma^5$

手征性由**手征性算符** $\gamma^5$ 来描述，它被定义为四个 $\gamma$ 矩阵的乘积：
$$
\gamma^5 = i\gamma^0\gamma^1\gamma^2\gamma^3
$$
这个算符具有两个至关重要的代数性质：
1.  它的平方是单位矩阵：$(\gamma^5)^2 = I_4$。这意味着它的本征值只能是 $\pm 1$。本征值为 $+1$ 的态被称为**右手征**态，本征值为 $-1$ 的态被称为**左手征**态。
2.  它与所有的 $\gamma^\mu$ 矩阵**反对易**（anticommute）[@problem_id:2095197]：
    $$
    \{\gamma^5, \gamma^\mu\} = \gamma^5\gamma^\mu + \gamma^\mu\gamma^5 = 0 \quad (\text{for } \mu=0,1,2,3)
    $$
这个反对易关系是理解手征性物理意义的关键。

#### 质量与手征性守恒破缺

一个物理量是否守恒，取决于其对应的算符是否与哈密顿量对易。自由狄拉克粒子的哈密顿量为 $H = \vec{\alpha} \cdot \vec{p} + \beta m = (\gamma^0 \vec{\gamma}) \cdot \vec{p} + \gamma^0 m$。我们来计算 $H$ 与 $\gamma^5$ 的对易子：
$$
[H, \gamma^5] = [\gamma^0 \vec{\gamma} \cdot \vec{p} + \gamma^0 m, \gamma^5]
$$
对于动能项，由于 $\gamma^5$ 与 $\gamma^0$ 和 $\gamma^k$ 都反对易，所以它与它们的乘积 $\gamma^0\gamma^k$ 是对易的。因此 $[\gamma^0 \vec{\gamma} \cdot \vec{p}, \gamma^5] = 0$。
然而，对于质量项，情况就不同了：
$$
[\gamma^0 m, \gamma^5] = m(\gamma^0\gamma^5 - \gamma^5\gamma^0) = m(\gamma^0\gamma^5 - (-\gamma^0\gamma^5)) = 2m\gamma^0\gamma^5 \neq 0
$$
这意味着 $[H, \gamma^5] \neq 0$ 只要质量 $m \neq 0$。这个结论至关重要：**对于有质量的粒子，手征性不守恒。**

我们可以通过一个具体的例子来生动地理解这一点。考虑一个静止的电子（$m>0, \vec{p}=0$），其哈密顿量简化为 $H=m\gamma^0$。假设在 $t=0$ 时刻，我们将电子制备在一个右手征态 $\psi(0)$，即 $\gamma^5\psi(0) = +\psi(0)$。随后的时间演化为 $\psi(t) = e^{-iHt}\psi(0) = e^{-imt\gamma^0}\psi(0)$。
利用 $(\gamma^0)^2=I$，我们可以展开指数函数：
$$
\psi(t) = [\cos(mt) \cdot I - i\sin(mt) \cdot \gamma^0] \psi(0)
$$
现在，我们想知道在 $t$ 时刻，测量到粒子处于左手征态的概率是多少。左手征态的投影算符是 $P_L = \frac{1}{2}(I - \gamma^5)$。作用在 $\psi(t)$ 上：
$$
P_L \psi(t) = \frac{1}{2}(I - \gamma^5)[\cos(mt)\psi(0) - i\sin(mt)\gamma^0\psi(0)]
$$
由于 $\gamma^5\psi(0)=\psi(0)$ 且 $\gamma^5\gamma^0\psi(0) = -\gamma^0\gamma^5\psi(0) = -\gamma^0\psi(0)$，我们得到：
$$
P_L \psi(t) = \frac{1}{2}[\cos(mt)\psi(0) - i\sin(mt)\gamma^0\psi(0) - \cos(mt)\psi(0) - i\sin(mt)\gamma^0\psi(0)] = -i\sin(mt)\gamma^0\psi(0)
$$
因此，找到左手征电子的概率幅的模平方为：
$$
\text{Prob}(L, t) = \| P_L \psi(t) \|^2 = \sin^2(mt) \|\gamma^0\psi(0)\|^2 = \sin^2(mt)
$$
这个结果 [@problem_id:2095237] 惊人地清晰：一个初始的纯右手征态会随着时间振荡，周期性地转变为左手征态，其振荡频率由粒子的质量决定。这生动地表明，手征性不是一个好的量子数，因为有质量粒子的能量本征态（$H$的本征态）并不是手征性的本征态。

与之相对的，**螺旋性**（Helicity）被定义为自旋在动量方向上的投影，其算符为 $\vec{\Sigma} \cdot \hat{p}$ (其中 $\vec{\Sigma}$ 是 $4\times 4$ 的自旋算符)。对于自由粒子，动量守恒，自旋也守恒，因此螺旋性是守恒的。对于有质量的粒子，手征性和螺旋性是两个不同的概念。然而，在 $m=0$ 的极限下，$[H, \gamma^5] = 0$，手征性变为守恒量，并且可以证明此时它与螺旋性是等价的。这一事实在标准模型中描述中微子等近无质量粒子时扮演着核心角色。