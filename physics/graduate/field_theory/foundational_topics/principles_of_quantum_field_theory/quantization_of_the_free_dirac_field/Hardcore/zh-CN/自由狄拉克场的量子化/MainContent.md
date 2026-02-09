## 引言
自由狄拉克场的量子化是现代物理学的基石，它为描述电子等自旋1/2费米子提供了相对论性的量子框架。尽管经典狄拉克理论在描述单粒子行为上取得了成功，但它无法解释粒子的创生与湮灭，也未能为多粒子系统提供一个自洽的理论基础。为了填补这一空白，必须将经典场论提升到量子层面，即进行“二次量子化”。本文旨在系统性地引导读者完成这一过程，并理解其深远的物理意义。在接下来的章节中，我们将首先在“原理与机制”中，详细构建量子化的核心数学结构，包括场算符、反对易关系和Fock空间；接着，在“应用与跨学科连接”中，我们将探索这一理论所带来的深刻物理推论，如反物质的预言、自旋统计定理，以及它如何连接粒子物理、凝聚态物质乃至引力理论等前沿领域；最后，通过“动手实践”，读者将有机会通过具体计算来巩固所学知识。现在，让我们从构建这一强大理论的基本原理与机制开始。

## 原理与机制

在上一章节中，我们介绍了自由狄拉克场的经典理论，它为描述自旋为 $1/2$ 的费米子（如电子）提供了相对论性的框架。然而，为了解释粒子的创生与湮灭等量子现象，并为多粒子系统奠定基础，我们必须将该场论进行量子化。本章旨在系统阐述自由狄拉克场量子化的核心原理与关键机制。我们将从构建场算符入手，通过正则反对易关系引入粒子统计，并最终展示这一理论如何描述基本粒子的动力学、对称性及其与真空的相互作用。

### 狄拉克场算符及其模态展开

量子化过程的第一步是将经典的狄拉克旋量场 $\psi(x)$ 及其共轭场 $\bar{\psi}(x)$ 提升为算符。这些场算符是时空的函数，作用于一个希尔伯特空间（即Fock空间）中的量子态。作为自由场的算符，$\psi(x)$ 必须满足自由狄拉克方程 $(i\gamma^\mu\partial_\mu - m)\psi(x) = 0$。这个线性偏微分方程的通解可以表示为平面波的叠加。在量子理论中，叠加的系数不再是经典数，而是算符。

因此，狄拉克场算符 $\psi(x)$ 可以进行如下的模态展开：
$$
\psi(x) = \int \frac{d^3p}{(2\pi)^3\sqrt{2E_{\mathbf{p}}}} \sum_{s} \left( a^s_{\mathbf{p}} u^s(\mathbf{p}) e^{-ip \cdot x} + b^{s\dagger}_{\mathbf{p}} v^s(\mathbf{p}) e^{ip \cdot x} \right)
$$
其中 $p^\mu = (E_{\mathbf{p}}, \mathbf{p})$ 是四维动量，满足在壳条件 $p^2 = E_{\mathbf{p}}^2 - |\mathbf{p}|^2 = m^2$，即 $E_{\mathbf{p}} = \sqrt{|\mathbf{p}|^2 + m^2}$。$s$ 是自旋标签，通常取值为 $1, 2$ 或 $\uparrow, \downarrow$。

这个展开式中的各个组成部分具有明确的物理意义：
- $u^s(\mathbf{p})$ 和 $v^s(\mathbf{p})$ 是狄拉克旋量，它们是自由狄拉克方程在动量空间中的正频和负频解，分别对应于粒子和反粒子。它们满足完备性关系：$\sum_s u^s(\mathbf{p})\bar{u}^s(\mathbf{p}) = \not p + m$ 和 $\sum_s v^s(\mathbf{p})\bar{v}^s(\mathbf{p}) = \not p - m$，其中 $\not p = p_\mu \gamma^\mu$。
- $a^s_{\mathbf{p}}$ 和 $b^s_{\mathbf{p}}$ 是**湮灭算符**。$a^s_{\mathbf{p}}$ 湮灭一个动量为 $\mathbf{p}$、自旋为 $s$ 的粒子（例如电子），而 $b^s_{\mathbf{p}}$ 湮灭一个动量为 $\mathbf{p}$、自旋为 $s$ 的反粒子（例如正电子）。
- $a^{s\dagger}_{\mathbf{p}}$ 和 $b^{s\dagger}_{\mathbf{p}}$ 是**创生算符**，它们分别是 $a^s_{\mathbf{p}}$ 和 $b^s_{\mathbf{p}}$ 的厄米共轭。$a^{s\dagger}_{\mathbf{p}}$ 创生一个粒子，而 $b^{s\dagger}_{\mathbf{p}}$ 创生一个反粒子。

这个展开式将场论的连续自由度（场在每一点的取值）与粒子力学的离散自由度（粒子的动量和自旋）联系起来。

### 正则反对易关系 (CARs)

玻色子场（如电磁场或克莱因-戈登场）的量子化是通过正则对易关系来实现的。然而，描述费米子的狄拉克场必须服从泡利不相容原理，即两个全同费米子不能占据同一个量子态。为了在场论中实现这一原理，我们必须对创生和湮灭算符施加**正则反对易关系**（Canonical Anticommutation Relations, CARs）。令 $\{A, B\} = AB + BA$ 表示反对易子，则CARs为：
$$
\{a^r_{\mathbf{p}}, a^{s\dagger}_{\mathbf{q}}\} = (2\pi)^3 \delta^{rs} \delta^{(3)}(\mathbf{p}-\mathbf{q})
$$
$$
\{b^r_{\mathbf{p}}, b^{s\dagger}_{\mathbf{q}}\} = (2\pi)^3 \delta^{rs} \delta^{(3)}(\mathbf{p}-\mathbf{q})
$$
所有其他反对易子，例如 $\{a^r_{\mathbf{p}}, a^s_{\mathbf{q}}\}$、$\{b^r_{\mathbf{p}}, b^s_{\mathbf{q}}\}$、$\{a^r_{\mathbf{p}}, b^s_{\mathbf{q}}\}$ 和 $\{a^r_{\mathbf{p}}, b^{s\dagger}_{\mathbf{q}}\}$，均为零。

这些关系是量子化的核心。例如，$(a^{s\dagger}_{\mathbf{p}})^2 = \frac{1}{2}\{a^{s\dagger}_{\mathbf{p}}, a^{s\dagger}_{\mathbf{p}}\} = 0$ 这一事实直接表明，我们无法在同一动量和自旋态上创生两个粒子，这正是泡利不相容原理的体现。

基于这些算符，我们可以构建出描述任意数量粒子和反粒子的量子态的 **Fock 空间**。这个空间的基石是**真空态** $|0\rangle$，它被定义为不包含任何粒子或反粒子的状态，因此被所有湮灭算符湮灭：
$$
a^s_{\mathbf{p}} |0\rangle = 0 \quad \text{and} \quad b^s_{\mathbf{p}} |0\rangle = 0 \quad \text{for all } \mathbf{p}, s
$$

### 粒子态与可观测量

在Fock空间中，我们可以通过创生算符作用于真空态来构建粒子态。例如，一个具有确定动量 $\mathbf{p}$ 和自旋 $s$ 的单电子态 $|p, s\rangle$ 可以定义为：
$$
|p, s\rangle = \sqrt{2E_{\mathbf{p}}} a_{\mathbf{p}}^{s\dagger} |0\rangle
$$
因子 $\sqrt{2E_{\mathbf{p}}}$ 是为了确保态的洛伦兹协变归一化。类似地，单正电子态由 $b^{s\dagger}_{\mathbf{p}}|0\rangle$ 创生。

这些态是物理可观测量的本征态，例如能量、动量和电荷。自由狄拉克场的哈密顿量 $H$ 和电荷算符 $Q$ 可以用创生和湮灭算符表示。然而，直接从拉格朗日量推导出的算符会包含一个无限大的真空能贡献。为了解决这个问题，我们采用**正规排序**（normal ordering）的办法，记作 $:\mathcal{O}:$。其规则是重新排列算符串，使得所有创生算符都位于所有湮灭算符的左侧，并且由于费米子的特性，每次交换算符位置时要引入一个负号。

正规排序后的哈密顿量 $H$ 和电荷算符 $Q$（假设电子电荷为 $-e$）为：
$$
H = \int \frac{d^3p}{(2\pi)^3} \sum_{s} E_{\mathbf{p}} \left( a^{s\dagger}_{\mathbf{p}} a^s_{\mathbf{p}} + b^{s\dagger}_{\mathbf{p}} b^s_{\mathbf{p}} \right)
$$
$$
Q = -e \int \frac{d^3p}{(2\pi)^3} \sum_{s} \left( a^{s\dagger}_{\mathbf{p}} a^s_{\mathbf{p}} - b^{s\dagger}_{\mathbf{p}} b^s_{\mathbf{p}} \right)
$$
$a^{s\dagger}_{\mathbf{p}} a^s_{\mathbf{p}}$ 和 $b^{s\dagger}_{\mathbf{p}} b^s_{\mathbf{p}}$ 分别是粒子和反粒子的**数算符**。从表达式可以看出，每个粒子（或反粒子）都为其所在态的总能量贡献 $E_{\mathbf{p}}$。哈密顿量的这种形式清晰地展示了场的激发即为粒子，每个粒子都携带一份能量量子。

通过这些表达式，我们可以验证粒子态的物理属性。例如，一个动量为 $\mathbf{q}$、自旋为 $s$ 的单正电子态 $|\Psi\rangle = d^\dagger_s(\mathbf{q})|0\rangle$（此处为了与问题符号一致，我们用 $d^\dagger$ 表示正电子创生算符）是哈密顿量的本征态，其能量本征值为 $E_\mathbf{q} = \sqrt{|\mathbf{q}|^2+m^2}$。我们也可以考察一个复合算符 $\mathcal{A} = H + \frac{\lambda m}{e} Q$ 作用在该态上，利用反对易关系可以精确地计算出其本征值，从而验证理论的自洽性 [@problem_id:358850]。

同样，电荷算符 $Q$ 也揭示了粒子和反粒子的电荷属性。作用在单电子态上，$Q|p,s\rangle = -e|p,s\rangle$；作用在单正电子态上，$Q|p,s\rangle_{positron} = +e|p,s\rangle_{positron}$。这表明 $a^\dagger$ 创生的粒子带电荷 $-e$，而 $b^\dagger$ 创生的粒子（反粒子）带电荷 $+e$。算符的代数结构直接反映了物理性质。例如，可以计算电荷算符 $Q$ 与一个经电荷共轭变换后的电子创生算符 $C a^\dagger_{\mathbf{k},r} C^{-1} = b^\dagger_{\mathbf{k},r}$ 的对易子，结果表明 $[Q, b^\dagger_{\mathbf{k},r}] = e b^\dagger_{\mathbf{k},r}$，这精确地说明了 $b^\dagger_{\mathbf{k},r}$ 所创生的态的电荷为 $+e$ [@problem_id:358739]。

### 场关联函数与传播子

场算符本身不是物理可观测量，但它们的关联函数（correlation functions）是。这些函数描述了在不同时空点创生和湮灭粒子的振幅，并与散射截面等可观测量直接相关。

最基本的构件是场算符与粒子态之间的矩阵元。例如，计算 $\langle 0 | \psi_\alpha(x) | p, s \rangle$ 相当于问：“在时空点 $x$ 湮灭一个粒子，而在无穷远的过去创生了一个动量为 $p$、自旋为 $s$ 的粒子，这个过程的振幅是多少？” 通过代入场算符的模态展开，并利用 $a_{\mathbf{k}}^r |p, s\rangle$ 和 $\langle 0| a_{\mathbf{k}}^r$ 的性质，可以得到：
$$
\langle 0 | \psi_\alpha(x) | p, s \rangle = u^s_\alpha(\mathbf{p}) e^{-ip \cdot x}
$$
这个结果表明，场算符 $\psi(x)$ 的作用是从真空中“提取”出一个平面波粒子波函数 [@problem_id:358720]。

更重要的物理量是两点关联函数，也称为**Wightman函数**。例如，正频Wightman函数定义为 $S^+_{\alpha\beta}(x-y) = \langle 0 | \psi_\alpha(x) \bar{\psi}_\beta(y) | 0 \rangle$。这个量可以被诠释为在 $y$ 处创生一个粒子-反粒子对，然后在 $x$ 处将其湮灭的真空期望值。通过将场算符展开并利用CARs，我们可以计算出：
$$
S^+_{\alpha\beta}(x-y) = \int \frac{d^3p}{(2\pi)^3 2E_{\mathbf{p}}} (\not p + m)_{\alpha\beta} e^{-ip \cdot (x-y)}
$$
这个表达式可以进一步写成 $(i\not\partial_x + m)_{\alpha\beta} i\Delta_+(x-y)$，其中 $\Delta_+(x-y)$ 是标量场的Wightman函数。对于等时空间隔 $x-y = (0, \mathbf{r})$，这个积分对于有质量场会涉及到第二类修正贝塞尔函数 $K_1(m|\mathbf{r}|)$ [@problem_id:358929]。

在量子场论中，一个核心的概念是**传播子**（propagator），它描述了一个粒子从一点传播到另一点的振幅。对于费米子场，其传播子与场算符的反对易子密切相关。我们可以计算**不等时反对易子** $\{\psi_\alpha(x), \bar{\psi}_\beta(y)\}$。这个计算结合了粒子 ($a, a^\dagger$) 和反粒子 ($b, b^\dagger$) 的贡献：
$$
\{\psi_\alpha(x), \bar{\psi}_\beta(y)\} = \int \frac{d^3p}{(2\pi)^3 2E_{\mathbf{p}}} \left[ (\not p + m)_{\alpha\beta} e^{-ip \cdot (x-y)} + (\not p - m)_{\alpha\beta} e^{ip \cdot (x-y)} \right]
$$
这个量通常记作 $iS(x-y)$。它的一个至关重要的性质是，它是狄拉克方程的格林函数。我们可以通过将狄拉克算符 $(i\gamma^\mu \partial_\mu^x - m)$ 作用于它来验证这一点。由于 $p^\mu$ 满足在壳条件 $p^2=m^2$，即 $\not p \not p = m^2$，我们可以证明 $(i\not\partial_x - m)(\not p + m)e^{-ip\cdot(x-y)} = (\not p - m)(\not p+m)e^{-ip\cdot(x-y)}=(p^2-m^2)e^{-ip\cdot(x-y)}=0$。对另一项的计算也得出类似结果。这表明，对于 $x \neq y$，该反对易子满足自由狄拉克方程，这正是格林函数所要求的性质 [@problem_id:358749]。更完整的分析表明 $(i\not\partial_x - m) S(x-y) = \delta^{(4)}(x-y)$。

在等时情况下，$t_x=t_y=t$，反对易关系简化为：
$$
\{\psi_\alpha(t, \mathbf{x}), \psi_\beta^\dagger(t, \mathbf{y})\} = \delta_{\alpha\beta}\delta^{(3)}(\mathbf{x}-\mathbf{y})
$$
这被称为等时反对易关系，是正则量子化的一个基本出发点。

### 对称性、流与量子反常

经典场论中的对称性通过诺特定理导致守恒流。在量子理论中，这些对称性由作用在Fock空间上的幺正算符实现，而守恒流也相应地成为算符。

- **U(1)矢量对称性与电荷守恒**: 全局U(1)变换 $\psi \to e^{-i\theta}\psi$ 对应于电荷守恒。守恒流算符为 $j^\mu(x) = -e :\bar{\psi}(x)\gamma^\mu\psi(x):$。其零分量 $j^0$ 的空间积分就是我们之前定义的电荷算符 $Q = \int d^3x j^0(x)$。

- **手征对称性与轴矢流**: 对于**无质量** ($m=0$) 的狄拉克场，拉格朗日量还具有额外的手征对称性 $\psi \to e^{i\alpha\gamma_5}\psi$。对应的诺特流是轴矢流 $J_5^\mu = \bar{\psi}\gamma^\mu\gamma_5\psi$。这个对称性在物理上与粒子的螺旋度（helicity）密切相关。螺旋度是自旋在动量方向上的投影。对于无质量费米子，螺旋度是一个洛伦兹不变量。我们可以计算轴矢荷密度算符 $:J_5^0(x):$ 在一个确定螺旋度的单粒子态 $|k, h'\rangle$ 中的期望值，结果表明该期望值正比于粒子的螺旋度 [@problem_id:358736]。这揭示了轴矢荷与螺旋度之间的深刻联系。

然而，量子化过程有时会破坏经典的对称性，这一现象称为**量子反常**（quantum anomaly）。一个著名的例子发生在(1+1)维时空中。经典无质量电动力学中的矢量流 $j^\mu$ 和轴矢流 $j_5^\mu$ 都是守恒的。但在量子理论中，由于算符在同一点的乘积需要正规化，导致流算符的对易关系出现经典理论中不存在的项。例如，电荷密度 $j^0$ 和空间流 $j^1$ 的等时对易子的真空期望值并非为零，而是包含一个所谓的**施温格项**（Schwinger term）[@problem_id:358746]：
$$
\langle 0 | [j^0(t,x), j^1(t,y)] | 0 \rangle = \frac{i}{\pi} \partial_x \delta(x-y)
$$
这个非零结果是一个纯粹的量子效应，它在量子霍尔效应和现代凝聚态物理中扮演着重要角色。

### 动力学与真空效应

在海森堡绘景中，量子态是固定的，而算符随时间演化。场算符的演化由海森堡运动方程 $i\partial_t \psi(t, \mathbf{x}) = [\psi(t, \mathbf{x}), H]$ 决定。通过求解这个方程，我们可以将任意时刻的场算符用初始时刻 ($t=0$) 的场算符来表示。例如，在动量空间中，$\tilde{\psi}(\mathbf{p}, t) = e^{-i H_D(\mathbf{p}) t} \tilde{\psi}(\mathbf{p}, 0)$，其中 $H_D(\mathbf{p})$ 是动量空间中的狄拉克哈密顿量矩阵。通过对矩阵指数 $e^{-i H_D t}$ 进行计算，我们可以得到场分量随时间的详细振荡行为，这种振荡混合了不同的手征分量，其频率由能量 $E_{\mathbf{p}}$ 和质量 $m$ 共同决定 [@problem_id:358922]。

最后，我们回到真空本身。尽管我们通过正规排序移除了哈密顿量中的无限大常数，但真空的物理性质远非平凡。真空可以被看作是充满虚粒子对的海洋，这些虚粒子可以与外场或边界条件相互作用，产生可观测的物理效应（如卡西米尔效应）。

如果我们不采用正规排序，而是通过引入一个动量截断 $\Lambda$ 来正规化真空能量密度的发散积分，可以更深入地研究真空的结构。自由狄拉克场的真空能量密度为：
$$
\mathcal{E}_{vac} = -2 \int \frac{d^3p}{(2\pi)^3} E_{\mathbf{p}} = -2 \int \frac{d^3p}{(2\pi)^3} \sqrt{|\mathbf{p}|^2 + m^2}
$$
（负号来源于费米子真空的贡献）。这个积分在 $|\mathbf{p}| \to \infty$ 时是紫外发散的。通过引入动量截断 $| \mathbf{p} | \le \Lambda$ 并对结果进行大 $\Lambda$ 展开，我们得到：
$$
\mathcal{E}_{vac}(\Lambda, m) = c_4 \Lambda^4 + c_2 m^2 \Lambda^2 + c_L m^4 \ln\left(\frac{\Lambda}{m}\right) + c_F m^4 + \mathcal{O}\left(\frac{m^6}{\Lambda^2}\right)
$$
这里的各项都有其物理解释。$\Lambda^4$ 和 $\Lambda^2$ 项是发散项，可以在重整化过程中被吸收。对数发散项 $m^4 \ln(\Lambda/m)$ 反映了标度变化下的理论行为。而最有趣的是有限的 $m^4$ 项，它的系数 $c_F$ 是一个可以通过精确计算确定的、与理论具体细节相关的非平凡数值 [@problem_id:358944]。这个有限部分贡献了宇宙学常数，构成了现代物理学中的一个重大谜题。这一分析表明，我们所说的“真空”具有丰富的内在结构，其能量响应是量子场论的一个深刻且可计算的预言。