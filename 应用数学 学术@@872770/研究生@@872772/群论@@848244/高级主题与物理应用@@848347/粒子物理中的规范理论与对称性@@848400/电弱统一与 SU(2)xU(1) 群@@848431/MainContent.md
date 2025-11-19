## 引言
[电弱统一](@entry_id:159671)理论是粒子物理学标准模型的基石之一，它将看似截然不同的电磁相互作用与弱相互作用统一在了一个优美的数学框架之下。这一理论的建立是20世纪物理学最伟大的成就之一，它不仅深刻地改变了我们对基本粒子及其相互作用的理解，还为解释宇宙中物质[质量的起源](@entry_id:161752)提供了关键线索。然而，一个核心的谜题在于：为何传递电磁力的[光子](@entry_id:145192)是无质量的，而传递弱相互作用的[W和Z玻色子](@entry_id:152878)却非常重？这个知识上的鸿沟正是[电弱统一](@entry_id:159671)理论旨在解决的关键问题。

本文将带领读者系统地探索[电弱统一](@entry_id:159671)理论的内在逻辑与强大威力。我们将从第一部分“原理与机制”入手，深入剖析 $SU(2)_L \times U(1)_Y$ [规范群](@entry_id:144761)的结构，并详细阐述[希格斯机制](@entry_id:144416)如何通过[自发对称性破缺](@entry_id:140964)为[规范玻色子](@entry_id:200257)和[费米子](@entry_id:146235)赋予质量。接着，在“应用与跨学科连接”部分，我们将展示这一理论框架如何转化为可检验的物理预测，从[粒子衰变](@entry_id:159938)到[高能散射](@entry_id:151941)过程，并探讨其在宇宙学和新物理探索中的重要作用。最后，通过“动手实践”环节，你将有机会亲自应用这些概念，推导关键的物理关系，从而将抽象的理论知识转化为具体的物理洞察。通过这一系列的学习，你将对现代[粒子物理学](@entry_id:145253)的核心支柱之一建立起一个坚实而深入的理解。

## 原理与机制

在对[电弱相互作用](@entry_id:194122)的基本对称性有了初步了解之后，本章将深入探讨其内在的原理与机制。我们将系统地阐述标准模型中 $SU(2)_L \times U(1)_Y$ 规范理论的核心要素，从[费米子](@entry_id:146235)的表示和[量子数](@entry_id:145558)分配，到通过[希格斯机制](@entry_id:144416)实现的[自发对称性破缺](@entry_id:140964)，直至最终导出可观测的物理粒子——[光子](@entry_id:145192)、$W$ 和 $Z$ [玻色子](@entry_id:138266)以及[费米子](@entry_id:146235)——的质量。本章旨在构建一个严谨且自洽的理论框架，揭示[电弱统一](@entry_id:159671)理论的深刻内涵。

### 电弱规范群：$SU(2)_L \times U(1)_Y$

[电弱理论](@entry_id:137910)的基石是规范[对称群](@entry_id:146083) $SU(2)_L \times U(1)_Y$。这个[群结构](@entry_id:146855)精妙地编码了[弱相互作用](@entry_id:157579)和电磁相互作用的统一描述。其中，$SU(2)_L$ 是一个非阿贝尔群，代表**[弱同位旋](@entry_id:158166)**对称性，下标 $L$ 表示它仅作用于左手性的[费米子](@entry_id:146235)。$U(1)_Y$ 是一个阿贝尔群，代表**[弱超荷](@entry_id:149263)**对称性。

#### [费米子表示](@entry_id:152283)与[量子数](@entry_id:145558)

[电弱理论](@entry_id:137910)的一个关键特征是其**手征性**（chirality）。这意味着理论对左手和右手[费米子](@entry_id:146235)的处理方式是不同的。具体而言，所有左手[费米子](@entry_id:146235)都被组织成 $SU(2)_L$ 的**二重态**（doublets），它们是弱相互作用的参与者。而所有右手[费米子](@entry_id:146235)都是 $SU(2)_L$ 的**单重态**（singlets），它们不参与[弱相互作用](@entry_id:157579)。

与这些对称性相关联的[守恒荷](@entry_id:145660)是**[弱同位旋](@entry_id:158166)** $\vec{T}$（其分量为 $T^1, T^2, T^3$）和**[弱超荷](@entry_id:149263)** $Y$。对于一个二重态，总同位旋量子数为 $T=1/2$，其两个分量的 $T^3$ [特征值](@entry_id:154894)分别为 $+1/2$ 和 $-1/2$。对于单重态，则有 $T=T^3=0$。

这些量子数与我们更熟悉的[电荷](@entry_id:275494) $Q$ 之间通过**电弱[盖尔曼-西岛关系](@entry_id:189488)**（electroweak Gell-Mann–Nishijima formula）联系在一起：
$$Q = T^3 + \frac{Y}{2}$$
此处的[电荷](@entry_id:275494) $Q$ 以[基本电荷](@entry_id:272261) $e$ 为单位。这个关系是构建粒子谱和理解其电弱属性的中心法则。

一个至关重要的原则是，$SU(2)_L$ [规范变换](@entry_id:176521)只混合二重态内部的成员，而不会改变它们的整体属性。由于 $SU(2)_L$ 的生成元与 $U(1)_Y$ 的生成元是对易的，这意味着同一个 $SU(2)_L$ 多重态中的所有粒子都必须具有**完全相同的[弱超荷](@entry_id:149263)** $Y$。我们可以利用这一原则来确定[费米子](@entry_id:146235)[多重态](@entry_id:195830)的[弱超荷](@entry_id:149263)。

作为一个具体的例子，我们来考虑第一代左手夸克，它们构成一个[弱同位旋](@entry_id:158166)二重态 [@problem_id:671285]：
$$Q_L = \begin{pmatrix} u_L \\ d_L \end{pmatrix}$$
其中 $u_L$ 和 $d_L$ 分别是左手上夸克和左手下夸克。作为 $T=1/2$ 多重态的成员，它们的第三同位旋分量分别为 $T^3(u_L) = +1/2$ 和 $T^3(d_L) = -1/2$。实验上已知上夸克和下夸克的[电荷](@entry_id:275494)分别为 $Q_u = +2/3$ 和 $Q_d = -1/3$。

我们可以利用 $u_L$ 的属性来计算该二重态的[弱超荷](@entry_id:149263) $Y_{Q_L}$。根据[盖尔曼-西岛关系](@entry_id:189488)，我们有：
$$Y_{Q_L} = 2(Q_{u_L} - T^3(u_L)) = 2\left(\frac{2}{3} - \frac{1}{2}\right) = 2\left(\frac{1}{6}\right) = \frac{1}{3}$$
为了验证理论的自洽性，我们也可以用 $d_L$ 的属性进行计算：
$$Y_{Q_L} = 2(Q_{d_L} - T^3(d_L)) = 2\left(-\frac{1}{3} - \left(-\frac{1}{2}\right)\right) = 2\left(\frac{1}{6}\right) = \frac{1}{3}$$
两种计算得到相同的结果，这证实了理论的一致性，并确定了左手夸克二重态的[弱超荷](@entry_id:149263)为 $Y = 1/3$。通过类似的方法，我们可以系统地确定标准模型中所有[费米子](@entry_id:146235)多重态的[弱超荷](@entry_id:149263)。

### [自发对称性破缺](@entry_id:140964)：[希格斯机制](@entry_id:144416)

尽管 $SU(2)_L \times U(1)_Y$ 对称性优美地统一了电磁和[弱相互作用](@entry_id:157579)，但它也预言了四个无质量的规范玻色子，这与实验观测到的短程、有质量的 $W$ 和 $Z$ [玻色子](@entry_id:138266)相矛盾。解决方案在于**自发对称性破缺**（Spontaneous Symmetry Breaking, SSB），其在粒子物理中的实现被称为**希格斯机制**（Higgs mechanism）。

#### 标量势与[真空期望值](@entry_id:146340)

希格斯机制的核心是引入一个新的标量场，即[希格斯场](@entry_id:160081) $\Phi$。在标准模型中，$\Phi$ 是一个[复标量](@entry_id:272141)**二重态**，其[弱同位旋](@entry_id:158166)为 $T=1/2$，[弱超荷](@entry_id:149263)为 $Y=1$。
$$\Phi = \begin{pmatrix} \phi^+ \\ \phi^0 \end{pmatrix}$$
其中 $\phi^+$ 和 $\phi^0$ 是[复标量场](@entry_id:159799)。该场的动力学由一个规范不变的[标量势](@entry_id:276177) $V(\Phi)$ 决定，其最一般的可重整化形式为：
$$V(\Phi) = \mu^2 (\Phi^\dagger \Phi) + \lambda (\Phi^\dagger \Phi)^2$$
为了实现[自发对称性破缺](@entry_id:140964)，势的参数需要满足 $\lambda > 0$ 以保证势函数在场值很大时是下方有界的，以及 $\mu^2  0$。当 $\mu^2  0$ 时，势的最小值（即真空态）不再位于 $\Phi=0$ 处，而是出现在一个非零的场值上。通过最小化势函数 $V(\Phi)$，我们发现其最小值位于满足以下条件的场组态上：
$$\Phi^\dagger \Phi = -\frac{\mu^2}{2\lambda} \equiv \frac{v^2}{2}$$
这里的 $v = \sqrt{-\mu^2/\lambda}$ 是一个具有[质量量纲](@entry_id:160525)的常数，被称为希格斯场的**[真空期望值](@entry_id:146340)**（Vacuum Expectation Value, VEV）。这个非零的 VEV 渗透在整个时空中，构成了我们宇宙的“电弱真空”。

值得注意的是，[真空期望值](@entry_id:146340) $v$ 的具体表达式依赖于势函数 $V(\Phi)$ 的形式。例如，在一个假想的、包含更高维度算符的[超越标准模型](@entry_id:161067)（BSM）理论中，势函数可能更加复杂 [@problem_id:671233]。考虑这样一个势：
$$V(\Phi) = \mu^2 (\Phi^\dagger \Phi) + \lambda (\Phi^\dagger \Phi)^2 + \frac{\kappa}{M^2} (\Phi^\dagger \Phi)^3$$
若参数满足 $\mu^2 > 0$, $\lambda  0$ 且 $\kappa > 0$ 并且 $\lambda^2 > 3\kappa\mu^2/M^2$，我们同样可以找到一个非平庸的真空。通过求解 $\frac{dV}{d(\Phi^\dagger\Phi)}=0$，可以找到势的极值点。在进行[稳定性分析](@entry_id:144077)后（即要求[二阶导数](@entry_id:144508)为正），可以确定真正的最小值，从而得到 VEV $v$ 的表达式。这一过程表明，VEV 的存在和大小是由[标量场](@entry_id:151443)的自身[相互作用参数](@entry_id:750714)决定的。

#### 电弱真空的性质

[希格斯场](@entry_id:160081)在无穷多个[能量简并](@entry_id:203091)的真空态中选择了**一个**特定的方向。由于规范对称性，我们可以通过一次 $SU(2)_L$ 旋转，将[真空期望值](@entry_id:146340)选定在只有一个实数分量非零的形式，而不会丧失一般性：
$$\langle \Phi \rangle = \frac{1}{\sqrt{2}} \begin{pmatrix} 0 \\ v \end{pmatrix}$$
这个特定的 VEV 破坏了 $SU(2)_L \times U(1)_Y$ [对称群](@entry_id:146083)，但并非完全破坏。我们可以通过考察规范[群的生成元](@entry_id:137215)作用于[真空期望值](@entry_id:146340)的效果来判断哪些对称性被破坏了。一个生成元 $G$ 被称为是**破缺的**，如果它作用在真空上时，真空态发生了改变，即 $G \langle \Phi \rangle \neq 0$。反之，如果 $G \langle \Phi \rangle = 0$，则该生成元对应的对称性是**未破缺的**或**剩余的**。

$SU(2)_L$ 的生成元是 $T^a = \sigma_a/2$（$\sigma_a$ 是[泡利矩阵](@entry_id:139493)），$U(1)_Y$ 的生成元是 $Y/2$。让我们将它们作用于 $\langle\Phi\rangle$：
- $T^1 \langle\Phi\rangle = \frac{1}{2}\begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix} \frac{1}{\sqrt{2}}\begin{pmatrix} 0 \\ v \end{pmatrix} = \frac{1}{2\sqrt{2}}\begin{pmatrix} v \\ 0 \end{pmatrix} \neq 0$
- $T^2 \langle\Phi\rangle = \frac{1}{2}\begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} \frac{1}{\sqrt{2}}\begin{pmatrix} 0 \\ v \end{pmatrix} = \frac{1}{2\sqrt{2}}\begin{pmatrix} -iv \\ 0 \end{pmatrix} \neq 0$
- $T^3 \langle\Phi\rangle = \frac{1}{2}\begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix} \frac{1}{\sqrt{2}}\begin{pmatrix} 0 \\ v \end{pmatrix} = \frac{1}{2\sqrt{2}}\begin{pmatrix} 0 \\ -v \end{pmatrix} \neq 0$
- $\frac{Y}{2} \langle\Phi\rangle = \frac{1}{2}(1) \langle\Phi\rangle = \frac{1}{2\sqrt{2}}\begin{pmatrix} 0 \\ v \end{pmatrix} \neq 0$ (因为希格斯二重态的 $Y=1$)

显然，$T^1, T^2, T^3$ 和 $Y$ 这四个生成元都被 VEV 所破缺。然而，我们可以寻找一个它们的[线性组合](@entry_id:154743)，它能够保持真空不变。考虑[电荷](@entry_id:275494)算符 $Q = T^3 + Y/2$：
$$Q \langle\Phi\rangle = \left( T^3 + \frac{Y}{2} \right) \langle\Phi\rangle = T^3 \langle\Phi\rangle + \frac{Y}{2} \langle\Phi\rangle = \frac{1}{\sqrt{2}} \begin{pmatrix} 0 \\ -v/2 \end{pmatrix} + \frac{1}{\sqrt{2}} \begin{pmatrix} 0 \\ v/2 \end{pmatrix} = 0$$
[真空期望值](@entry_id:146340)被[电荷](@entry_id:275494)算符 $Q$ 所湮灭！这意味着尽管 $SU(2)_L \times U(1)_Y$ 对称性被破坏了，但由 $Q$ 生成的 $U(1)_{EM}$ 对称性仍然是完好的。这就是我们熟知的电磁规范对称性。真空本身是电中性的，因此对应的规范玻色子——[光子](@entry_id:145192)——将保持无质量。

这个原理是如此根本，以至于它可以用来检验任何包含[希格斯机制](@entry_id:144416)的理论。例如，在一个包含标准希格斯二重态 $\phi$ 和一个额外 $SU(2)_L$ 单重态标量 $\chi$ 的假想模型中，如果两个场都获得了非零 VEV $\langle\phi\rangle$ 和 $\langle\chi\rangle$，那么未破缺的电[磁对称性](@entry_id:186579)生成元 $Q_{em}$ 必须同时湮灭这两个 VEV [@problem_id:671200]。由于 $\chi$ 是 $SU(2)_L$ [单重态](@entry_id:154728)，所以 $T^3 \langle\chi\rangle = 0$。因此，条件 $Q_{em} \langle\chi\rangle = (T^3+Y/2)\langle\chi\rangle = (Y_\chi/2)\langle\chi\rangle=0$ 必然要求该单重态的[弱超荷](@entry_id:149263) $Y_\chi=0$。这强有力地展示了真空的对称性如何约束了理论中粒子的基本属性。

### 源于希格斯动能项的质量

[规范玻色子](@entry_id:200257)的质量并非凭空产生，而是源于它们与充满时空的希格斯 VEV 的相互作用。这些相互作用项隐藏在[希格斯场](@entry_id:160081)的动能项 $\mathcal{L}_{\text{kin}} = (D_\mu \Phi)^\dagger (D^\mu \Phi)$ 中。

#### [协变导数](@entry_id:152476)与[规范玻色子质量](@entry_id:147712)

协变导数 $D_\mu$ 确保了动能项在 $SU(2)_L \times U(1)_Y$ [规范变换](@entry_id:176521)下的[不变性](@entry_id:140168)。对于希格斯二重态，其[协变导数](@entry_id:152476)为：
$$D_\mu = \partial_\mu - i g \frac{\sigma^a}{2} W_\mu^a - i g' \frac{Y}{2} B_\mu$$
其中 $g$ 和 $g'$ 分别是 $SU(2)_L$ 和 $U(1)_Y$ 的规范[耦合常数](@entry_id:747980)，$W_\mu^a$ ($a=1,2,3$) 和 $B_\mu$ 是对应的规范场。

当我们将[希格斯场](@entry_id:160081)替换为其[真空期望值](@entry_id:146340) $\Phi \to \langle\Phi\rangle$ 时，偏导数项 $\partial_\mu \langle\Phi\rangle$ 为零（因为 VEV 是时空常数），动能项变为：
$$\mathcal{L}_{\text{mass}} = \left| \left( - i g \frac{\sigma^a}{2} W_\mu^a - i g' \frac{Y}{2} B_\mu \right) \langle\Phi\rangle \right|^2$$
展开这个表达式，我们就会得到关于[规范场](@entry_id:159627) $W_\mu^a$ 和 $B_\mu$ 的二次型。在[拉格朗日量](@entry_id:174593)中，任何场 $\mathcal{F}$ 的形如 $\frac{1}{2} m^2 \mathcal{F}^2$ 的项都对应于质量项，其中 $m$ 就是该场的质量。因此，上式正是[规范玻色子质量](@entry_id:147712)的来源。

#### 带电规范玻色子：$W^\pm$ 的质量

我们首先考察与带[电荷](@entry_id:275494)的弱相互作用相关的 $W^1_\mu$ 和 $W^2_\mu$ 场。它们的相互作用项来自 $\frac{\sigma^1}{2}W^1_\mu$ 和 $\frac{\sigma^2}{2}W^2_\mu$。将它们作用在 VEV 上：
$$g\left(\frac{\sigma^1}{2} W^1_\mu + \frac{\sigma^2}{2} W^2_\mu\right) \langle\Phi\rangle = \frac{g}{2\sqrt{2}} \begin{pmatrix} W^1_\mu - i W^2_\mu \\ 0 \end{pmatrix} v$$
将此项代入质量[拉格朗日量](@entry_id:174593) $\mathcal{L}_{\text{mass}}$ 并取模平方，得到：
$$\mathcal{L}_{\text{mass}} \supset \frac{g^2 v^2}{8} |W^1_\mu - i W^2_\mu|^2 = \frac{g^2 v^2}{8} (W^1_\mu - i W^2_\mu)(W^{1\mu} + i W^{2\mu})$$
物理上可观测的带电规范玻色子是 $W^1_\mu$ 和 $W^2_\mu$ 的线性组合，即 $W^\pm_\mu = \frac{1}{\sqrt{2}}(W^1_\mu \mp i W^2_\mu)$。利用此定义，上述质量项可以写为：
$$\mathcal{L}_{\text{mass}} \supset \frac{g^2 v^2}{4} W^+_\mu W^{-\mu}$$
将此与标准的质量项 $M_W^2 W^+_\mu W^{-\mu}$ 对比，我们直接读出 $W$ [玻色子](@entry_id:138266)的质量平方 [@problem_id:671283]：
$$M_W^2 = \frac{g^2 v^2}{4} \implies M_W = \frac{gv}{2}$$
这优美地将 $W$ [玻色子](@entry_id:138266)的质量与 $SU(2)_L$ 耦合常数 $g$ 和[电弱对称性破缺](@entry_id:161363)能标 $v$ 联系起来。

#### 中性规范玻色子：[光子](@entry_id:145192)与 $Z$ [玻色子](@entry_id:138266)

对于中性[规范场](@entry_id:159627) $W^3_\mu$ 和 $B_\mu$，情况更为有趣。它们的作用项为：
$$\left(g \frac{\sigma^3}{2} W^3_\mu + g' \frac{Y}{2} B_\mu\right) \langle\Phi\rangle = \left(g \frac{\sigma^3}{2} W^3_\mu + g' \frac{1}{2} B_\mu\right) \frac{1}{\sqrt{2}}\begin{pmatrix} 0 \\ v \end{pmatrix} = \frac{-v}{2\sqrt{2}} (g W^3_\mu - g' B_\mu) \begin{pmatrix} 0 \\ 1 \end{pmatrix}$$
将此项代入质量拉格朗日量，得到：
$$\mathcal{L}_{\text{mass}} \supset \frac{v^2}{8} (g W^3_\mu - g' B_\mu)^2 = \frac{1}{2} \begin{pmatrix} W^3_\mu  B_\mu \end{pmatrix} \frac{v^2}{4} \begin{pmatrix} g^2  -gg' \\ -gg'  g'^2 \end{pmatrix} \begin{pmatrix} W^{3\mu} \\ B^{\mu} \end{pmatrix}$$
这揭示了 $W^3_\mu$ 和 $B_\mu$ 场的质量平方矩阵 $\mathcal{M}^2$ [@problem_id:671306]：
$$\mathcal{M}^2 = \frac{v^2}{4} \begin{pmatrix} g^2  -gg' \\ -gg'  g'^2 \end{pmatrix}$$
由于存在非对角项（$-gg'$），$W^3_\mu$ 和 $B_\mu$ 并不是具有确定质量的物理粒子，它们会相互混合。物理上的质量本征态是使该[矩阵对角化](@entry_id:138930)的[线性组合](@entry_id:154743)。

对角化 $\mathcal{M}^2$ 会得到两个[本征值](@entry_id:154894)。其中一个[本征值](@entry_id:154894)为零，对应的[本征态](@entry_id:149904)就是无质量的**[光子](@entry_id:145192)**场 $A_\mu$。另一个非零[本征值](@entry_id:154894)则对应有质量的**$Z$ [玻色子](@entry_id:138266)**场 $Z_\mu$。

我们可以通过一个更物理的方法来识别[光子](@entry_id:145192)场 [@problem_id:671139]。[光子](@entry_id:145192)是未破缺的 $U(1)_{EM}$ 对称性的规范玻色子，因此它不能与希格斯 VEV 耦合。将 $W^3_\mu$ 和 $B_\mu$ 写成物理场 $A_\mu$ 和 $Z_\mu$ 的旋转：
$$W^3_\mu = A_\mu \sin\theta_W + Z_\mu \cos\theta_W$$
$$B_\mu = A_\mu \cos\theta_W - Z_\mu \sin\theta_W$$
其中 $\theta_W$ 是**[弱混合角](@entry_id:190680)**（Weinberg angle）。将此代入中性[玻色子](@entry_id:138266)与 VEV 的耦合项 $(g W^3_\mu - g' B_\mu)$ 中，并要求 $A_\mu$ 的系数为零：
$$g \sin\theta_W - g' \cos\theta_W = 0 \implies \tan\theta_W = \frac{g'}{g}$$
这个关系定义了[弱混合角](@entry_id:190680)。利用三角关系，我们可以反解出 $A_\mu$：
$$A_\mu = W^3_\mu \sin\theta_W + B_\mu \cos\theta_W = \frac{g' W^3_\mu + g B_\mu}{\sqrt{g^2+g'^2}}$$
这正是[光子](@entry_id:145192)场与原始[规范场](@entry_id:159627)的混合方式。

$Z$ [玻色子](@entry_id:138266)场是与 $A_\mu$ 正交的组合。其质量平方就是 $\mathcal{M}^2$ 的非零[本征值](@entry_id:154894)：
$$\det(\mathcal{M}^2 - M^2 I) = 0 \implies M^2_Z = \text{Tr}(\mathcal{M}^2) = \frac{v^2}{4}(g^2 + g'^2)$$
因此，$Z$ [玻色子](@entry_id:138266)的质量为：
$$M_Z = \frac{v}{2}\sqrt{g^2+g'^2} = \frac{gv}{2\cos\theta_W} = \frac{M_W}{\cos\theta_W}$$
这个关系 $M_W = M_Z \cos\theta_W$ 是[电弱统一](@entry_id:159671)理论的一个核心预言，已在实验上得到高度精确的验证。

#### $\rho$ 参数：希格斯结构的探针

标准模型[希格斯机制](@entry_id:144416)的一个深刻结果是关于 $W$ 和 $Z$ [玻色子](@entry_id:138266)质量的特定比率。为了量化这一点，物理学家定义了**$\rho$ 参数**：
$$\rho = \frac{M_W^2}{M_Z^2 \cos^2\theta_W}$$
利用我们上面导出的质量表达式和 $\cos^2\theta_W = g^2/(g^2+g'^2)$，我们可以计算在标准模型中的[树图](@entry_id:276372)层面 $\rho$ 值 [@problem_id:671157]：
$$\rho = \frac{g^2v^2/4}{\left(\frac{v^2}{4}(g^2+g'^2)\right) \left(\frac{g^2}{g^2+g'^2}\right)} = 1$$
$\rho=1$ 这个结果并非偶然，它根植于希格斯场是 $SU(2)_L$ 二重态这一事实。这种结构在希格斯势中导致了一种额外的全局对称性，即** custodial symmetry**，它保护了 $W$ 和 $Z$ 质量之间的关系。如果希格斯场具有不同的 $SU(2)_L$ 表示（例如[三重态](@entry_id:156705)），$\rho$ 的[树图](@entry_id:276372)值就会偏离 1。因此，实验上测得 $\rho \approx 1$ 是标准模型希格斯机制的有力证据。即使在包含多个希格斯二重态的模型中（例如2HDM），只要势函数满足 custodial symmetry，这个关系在[树图](@entry_id:276372)层面依然成立 [@problem_id:671301]。

### [费米子质量](@entry_id:155586)的产生：汤川相互作用

希格斯机制不仅为规范玻色子提供质量，也为[费米子](@entry_id:146235)（[夸克和轻子](@entry_id:753951)）提供了质量。由于[电弱理论](@entry_id:137910)的手征性，形如 $m \bar{\psi}_L \psi_R$ 的直接质量项会破坏 $SU(2)_L$ 规范对称性，因此是被禁止的。

[费米子质量](@entry_id:155586)是通过**汤川相互作用**（Yukawa interaction）产生的，这是[费米子](@entry_id:146235)与希格斯场的一种规范不变的相互作用。以一个泛化的上类型夸克 $u$ 为例，其汤川[拉格朗日量](@entry_id:174593)为：
$$\mathcal{L}_Y = -y_u (\bar{Q}_L \tilde{\Phi} u_R) + \text{h.c.}$$
其中 $Q_L = (u_L, d_L)^T$ 是左手夸克二重态，$u_R$ 是右手夸克[单重态](@entry_id:154728)，$y_u$ 是[汤川耦合](@entry_id:154951)常数。$\tilde{\Phi} = i\sigma_2 \Phi^*$ 是所谓的**共轭希格斯二重态**。引入 $\tilde{\Phi}$ 是必要的，因为它与 $\Phi$ 变换方式不同，可以与 $\bar{Q}_L$ 和 $u_R$ 结合构成一个 $SU(2)_L \times U(1)_Y$ 的标量（[不变量](@entry_id:148850)）。

[自发对称性破缺](@entry_id:140964)后，我们将 $\Phi$ 替换为它的 VEV $\langle\Phi\rangle$，那么 $\tilde{\Phi}$ 也相应地获得 VEV $\langle\tilde{\Phi}\rangle = (v/\sqrt{2}, 0)^T$。汤川拉格朗日量变为：
$$\mathcal{L}_{\text{mass}} = -y_u \left( (\bar{u}_L, \bar{d}_L) \frac{1}{\sqrt{2}} \begin{pmatrix} v \\ 0 \end{pmatrix} u_R \right) + \text{h.c.} = -\frac{y_u v}{\sqrt{2}} (\bar{u}_L u_R + \bar{u}_R u_L) = -\frac{y_u v}{\sqrt{2}} \bar{u}u$$
这正是一个标准的质量项。因此，上类型夸克的质量为 $m_u = y_u v / \sqrt{2}$。[费米子](@entry_id:146235)的[质量等级](@entry_id:151601)差异，本质上源于它们各自[汤川耦合](@entry_id:154951)常数 $y_f$ 的巨大差异。

这一机制也可以推广到更复杂的希格斯扇区。例如，在所谓的二型双希格斯二重态模型（Type-II 2HDM）中，存在两个希格斯二重态 $\Phi_u$ 和 $\Phi_d$，它们分别赋予上类型和下类型夸克质量 [@problem_id:671230]。顶夸克的汤川拉格朗日量写作 $\mathcal{L}_{Yukawa_t} = -y_t (\bar{Q}_L \tilde{\Phi}_u t_R + \text{h.c.})$。两个 VEV 的大小关系通常用一个混合角 $\beta$ 来[参数化](@entry_id:272587)，即 $v_u = v \sin\beta$ 和 $v_d = v \cos\beta$，其中 $v^2 = v_u^2+v_d^2$。在这种情况下，顶夸克的质量就变为：
$$m_t = \frac{y_t v_u}{\sqrt{2}} = \frac{y_t v \sin\beta}{\sqrt{2}}$$
这表明，在更广阔的理论框架中，[费米子](@entry_id:146235)的质量不仅依赖于其[汤川耦合](@entry_id:154951)，还可能与希格斯扇区的内部结构（如此处的 $\sin\beta$）有关。

综上所述，[电弱统一](@entry_id:159671)理论通过 $SU(2)_L \times U(1)_Y$ [规范对称性](@entry_id:136438)和[希格斯机制](@entry_id:144416)，不仅成功地统一了电磁与弱相互作用，还提供了一个深刻的、基于对称性原理的质量起源模型，其预言与实验观测取得了惊人的一致。