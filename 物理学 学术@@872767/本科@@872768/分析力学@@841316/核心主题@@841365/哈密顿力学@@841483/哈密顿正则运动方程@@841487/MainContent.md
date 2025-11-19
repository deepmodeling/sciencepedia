## 引言

经典力学，作为物理学最古老也最坚实的分支，拥有多种精妙的数学表述。在[拉格朗日力学](@entry_id:147054)之后，爱尔兰数学家William Rowan Hamilton提出了一种更为深刻和对称的理论框架——[哈密顿力学](@entry_id:146202)。它不仅为解决力学问题提供了另一种强大的工具，更重要的是，它揭示了物理定律背后优美的几何结构和普适原理，其影响深远，直至今日的量子力学和现代物理前沿。

本文旨在系统地介绍哈密顿力学的核心——**哈密顿正则[运动方程](@entry_id:170720)**。我们将从[拉格朗日力学](@entry_id:147054)出发，解决其二阶运动方程在理论分析上的一些不便，过渡到以[广义坐标](@entry_id:156576)和[广义动量](@entry_id:165699)为基本变量的一阶动力学体系。通过学习本文，您将能够掌握从构建[哈密顿量](@entry_id:172864)到求解正则方程的全过程，并理解其背后深刻的物理思想。

在接下来的内容中，我们将分三步深入探索：
*   **原理与机制** 章节将奠定理论基础，详细阐述从拉格朗日量到[哈密顿量](@entry_id:172864)的[勒让德变换](@entry_id:146727)，推导核心的[哈密顿正则方程](@entry_id:176897)，并引入相空间、[泊松括号](@entry_id:151133)及守恒律等关键概念。
*   **应用与跨学科联系** 章节将展示[哈密顿形式体系](@entry_id:148673)的强大威力，探讨其在[刚体动力学](@entry_id:142040)、[中心力问题](@entry_id:178836)、电磁学、相对论乃至[经典场论](@entry_id:149475)等众多领域的应用，揭示其作为一种统一物理语言的价值。
*   **动手实践** 章节将提供一系列精心设计的计算问题，引导您将理论知识应用于具体物理情境，从而巩固和深化对哈密顿力学的理解。

让我们一同开启这段探索之旅，领略[哈密顿力学](@entry_id:146202)那无与伦比的数学之美与物理洞察力。

## 原理与机制

在[拉格朗日力学](@entry_id:147054)中，系统的状态由[广义坐标](@entry_id:156576)及其时间导数（[广义速度](@entry_id:178456)）描述，动力学由二阶的[欧拉-拉格朗日方程](@entry_id:137827)决定。然而，存在一种等价但形式上更为对称和深刻的力学表述，即哈密顿力学。[哈密顿力学](@entry_id:146202)的核心是将系统的状态描述为[广义坐标](@entry_id:156576)和与之共轭的[广义动量](@entry_id:165699)的函数，其动力学演化由一组[一阶微分方程](@entry_id:173139)——[哈密顿正则方程](@entry_id:176897)——所支配。本章将详细阐述[哈密顿量](@entry_id:172864)的构建方法、正则方程的推导及其物理意义，并探讨其在守恒律、相[空间分析](@entry_id:183208)以及处理复杂系统中的应用。

### [从拉格朗日到哈密顿](@entry_id:164887)：勒让德变换

[哈密顿力学](@entry_id:146202)的出发点是对[拉格朗日形式](@entry_id:145697)体系的一次变量代换。在[拉格朗日力学](@entry_id:147054)中，拉格朗日量 $L$ 是[广义坐标](@entry_id:156576) $q_i$、[广义速度](@entry_id:178456) $\dot{q}_i$ 和时间 $t$ 的函数，即 $L(q, \dot{q}, t)$。哈密顿力学的目标是使用[广义坐标](@entry_id:156576) $q_i$ 和一个新变量——**[广义动量](@entry_id:165699) (generalized momentum)** $p_i$——来描述系统状态。

[广义动量](@entry_id:165699) $p_i$ 定义为拉格朗日量对[广义速度](@entry_id:178456)的[偏导数](@entry_id:146280)：
$$
p_i = \frac{\partial L}{\partial \dot{q}_i}
$$
这个定义将速度 $\dot{q}_i$ 与一个新的动力学变量 $p_i$ 联系起来。为了将理论的描述基础从 $(q, \dot{q})$ 空间完全转换到 $(q, p)$ 空间，我们需要引入一个新的函数，即**[哈密顿量](@entry_id:172864) (Hamiltonian)** $H$。这个转换通过**勒让德变换 (Legendre transformation)** 实现：
$$
H(q, p, t) = \sum_{i} p_i \dot{q}_i - L(q, \dot{q}, t)
$$
在执行此变换时，一个关键步骤是利用 $p_i$ 的定义式将所有的[广义速度](@entry_id:178456) $\dot{q}_i$ 都用[广义坐标](@entry_id:156576) $q_i$ 和[广义动量](@entry_id:165699) $p_i$ 表示出来，从而确保最终的[哈密顿量](@entry_id:172864)是 $q$、 $p$ 和 $t$ 的函数，即 $H(q, p, t)$。

让我们通过一个具体的物理系统来阐明这个过程。考虑一个质量为 $m$ 的质点，悬挂在一个劲度系数为 $k$ 的竖直弹簧下端，并在匀强重[力场](@entry_id:147325) $g$ 中运动。我们设定[广义坐标](@entry_id:156576) $z$ 为质点相对于弹簧自然长度处的竖直向下位移 [@problem_id:2055738]。系统的动能 $T$ 和势能 $V$ 分别为：
$$
T = \frac{1}{2}m\dot{z}^2
$$
$$
V(z) = \frac{1}{2}kz^2 - mgz
$$
系统的[拉格朗日量](@entry_id:174593) $L = T - V$ 为：
$$
L(z, \dot{z}) = \frac{1}{2}m\dot{z}^2 - \frac{1}{2}kz^2 + mgz
$$
根据定义，共轭于 $z$ 的[广义动量](@entry_id:165699) $p_z$ 是：
$$
p_z = \frac{\partial L}{\partial \dot{z}} = m\dot{z}
$$
现在，我们可以构造[哈密顿量](@entry_id:172864)。首先，我们将 $\dot{z}$ 用 $p_z$ 表示：$\dot{z} = p_z / m$。然后代入[勒让德变换](@entry_id:146727)的定义式：
$$
H(z, p_z) = p_z \dot{z} - L = p_z \left( \frac{p_z}{m} \right) - \left( \frac{1}{2}m\left(\frac{p_z}{m}\right)^2 - \frac{1}{2}kz^2 + mgz \right)
$$
$$
H(z, p_z) = \frac{p_z^2}{m} - \left( \frac{p_z^2}{2m} - \frac{1}{2}kz^2 + mgz \right) = \frac{p_z^2}{2m} + \frac{1}{2}kz^2 - mgz
$$
通过这个过程，我们成功地将系统的描述从 $(z, \dot{z})$ 空间转换到了 $(z, p_z)$ 空间，并得到了作为坐标和动量函数的[哈密顿量](@entry_id:172864) $H(z, p_z)$。

### [哈密顿正则方程](@entry_id:176897)

一旦获得了[哈密顿量](@entry_id:172864) $H(q, p, t)$，系统的动力学演化就由一组优美对称的[一阶微分方程](@entry_id:173139)——**[哈密顿正则方程](@entry_id:176897) (Hamilton's Canonical Equations)**——所描述：
$$
\dot{q}_i = \frac{\partial H}{\partial p_i}
$$
$$
\dot{p}_i = -\frac{\partial H}{\partial q_i}
$$
这组方程构成了[哈密顿力学](@entry_id:146202)的核心。与[拉格朗日方程](@entry_id:175419)的二阶形式不同，[哈密顿方程](@entry_id:156213)将一个具有 $N$ 个自由度的系统的 $N$ 个二阶微分方程，转化为了 $2N$ 个[一阶微分方程](@entry_id:173139)。这种形式在理论分析和数值计算中都具有显著优势。

方程 $\dot{q}_i = \partial H / \partial p_i$ 给出了[广义坐标](@entry_id:156576)随时间的变化率，它通常与[广义速度](@entry_id:178456)和动量之间的关系有关。方程 $\dot{p}_i = -\partial H / \partial q_i$ 描述了[广义动量](@entry_id:165699)随时间的变化率，其右侧 $-\partial H / \partial q_i$ 被称为**[广义力](@entry_id:169699) (generalized force)**。

例如，对于一个在一维四次势 $U(x) = \frac{1}{4}\beta x^4$ 中运动的粒子，其[哈密顿量](@entry_id:172864)为 $H = \frac{p^2}{2m} + \frac{1}{4}\beta x^4$ [@problem_id:2055701]。应用[哈密顿正则方程](@entry_id:176897)，我们得到：
$$
\dot{x} = \frac{\partial H}{\partial p} = \frac{p}{m}
$$
$$
\dot{p} = -\frac{\partial H}{\partial x} = -\beta x^3
$$
这里的 $\dot{p}$ 正好等于势能的负梯度，即作用在粒子上的力，这与[牛顿第二定律](@entry_id:274217) $\dot{p} = F$ 完全一致。哈密顿方程不仅可以用来求解系统的运动轨迹，还可以用来分析任意物理量 $Q(q, p, t)$ 的[时间演化](@entry_id:153943)。其时间导数由下式给出：
$$
\frac{dQ}{dt} = \frac{\partial Q}{\partial t} + \sum_i \left( \frac{\partial Q}{\partial q_i}\dot{q}_i + \frac{\partial Q}{\partial p_i}\dot{p}_i \right) = \frac{\partial Q}{\partial t} + \sum_i \left( \frac{\partial Q}{\partial q_i}\frac{\partial H}{\partial p_i} - \frac{\partial Q}{\partial p_i}\frac{\partial H}{\partial q_i} \right)
$$
上式括号中的部分被称为 $Q$ 和 $H$ 的**[泊松括号](@entry_id:151133) (Poisson bracket)**，记作 $\{Q, H\}$。

### [哈密顿量](@entry_id:172864)与能量

一个自然的问题是：[哈密顿量](@entry_id:172864) $H$ 与系统的总能量 $E = T + V$ 有什么关系？
对于一个保守系统，如果定义[广义坐标](@entry_id:156576)的变换不显含时间，那么[哈密顿量](@entry_id:172864)就等于系统的[总机械能](@entry_id:167353)。在前面的竖直弹簧[振子](@entry_id:271549)例子中 [@problem_id:2055738]，我们得到的[哈密顿量](@entry_id:172864) $H = \frac{p_z^2}{2m} + \frac{1}{2}kz^2 - mgz$ 正好是系统的动能 $\frac{p_z^2}{2m}$ 与[势能](@entry_id:748988) $V(z)$ 之和。

[哈密顿量](@entry_id:172864)的守恒性是另一个核心议题。对 $H(q, p, t)$ 求[全时间导数](@entry_id:172646)：
$$
\frac{dH}{dt} = \frac{\partial H}{\partial t} + \sum_i \left( \frac{\partial H}{\partial q_i}\dot{q}_i + \frac{\partial H}{\partial p_i}\dot{p}_i \right)
$$
将[哈密顿正则方程](@entry_id:176897)代入上式，我们发现括号内的和为零：
$$
\sum_i \left( \frac{\partial H}{\partial q_i}\frac{\partial H}{\partial p_i} + \frac{\partial H}{\partial p_i}\left(-\frac{\partial H}{\partial q_i}\right) \right) = 0
$$
因此，我们得到一个至关重要的结论：
$$
\frac{dH}{dt} = \frac{\partial H}{\partial t}
$$
这意味着，**如果[哈密顿量](@entry_id:172864)不显含时间（即 $\partial H / \partial t = 0$），那么[哈密顿量](@entry_id:172864)本身就是一个[守恒量](@entry_id:150267)**。对于上述保守系统，这意味着总能量是守恒的。

然而，当系统存在显式的时间依赖性时，情况就变得复杂。
考虑一个摆长随时间线性增加的单摆 $l(t) = l_0 + v_0 t$ [@problem_id:2055718]。其[哈密顿量](@entry_id:172864)可以被推导为：
$$
H(\theta, p_\theta, t) = \frac{p_\theta^2}{2m(l_0+v_0t)^2} - mg(l_0+v_0t)\cos\theta - \frac{1}{2}m v_0^2
$$
这个[哈密顿量](@entry_id:172864)显含时间 $t$，因此它不守恒。此外，由于坐标变换本身是含时的，这个[哈密顿量](@entry_id:172864)也不等于总能量 $T+V$。

另一个有趣的例子是质量随时间变化的粒子 $m(t)$ [@problem_id:2055700]。其[哈密顿量](@entry_id:172864)为 $H(x, p, t) = \frac{p^2}{2m(t)} + U(x)$。尽管它的形式是 $T+V$，但由于 $m(t)$ 的存在，它仍然显含时间，因此系统的[能量不守恒](@entry_id:276143)。尽管如此，[哈密顿正则方程](@entry_id:176897)的形式依然保持不变，体现了该框架的普适性：
$$
\dot{x} = \frac{\partial H}{\partial p} = \frac{p}{m(t)}
$$
$$
\dot{p} = -\frac{\partial H}{\partial x} = -\frac{dU}{dx}
$$
值得注意的是，$\dot{p}$ 等于外力，而不是[总动量](@entry_id:173071) $p=m(t)\dot{x}$ 的时间导数，这与[牛顿第二定律](@entry_id:274217)的原始形式 $F = \frac{d(m v)}{dt}$ 是一致的。

与此相对，如果质量是位置的函数，如 $m(x) = m_0 \exp(\alpha x)$ [@problem_id:2055713]，其[哈密顿量](@entry_id:172864)为 $H(x, p) = \frac{p^2}{2m(x)} + U(x)$。此时 $H$ 不显含时间，因此 $H$ 是守恒的。然而，从哈密顿方程推导出的加速度方程却包含一个与速度平方相关的“[伪力](@entry_id:169104)”项，这源于质量的空间变化：
$$
\ddot{x} = -\frac{1}{2}\frac{m'(x)}{m(x)}\dot{x}^2 - \frac{k}{m(x)}x
$$
这充分展示了[哈密顿形式体系](@entry_id:148673)在处理非标准问题时的严谨性和威力。

### 相空间与守恒律

哈密顿力学引入了一个极其重要的几何概念——**相空间 (phase space)**。一个具有 $N$ 个自由度的系统，其相空间是一个以 $N$ 个[广义坐标](@entry_id:156576) $q_i$ 和 $N$ 个[广义动量](@entry_id:165699) $p_i$ 为坐标轴的 $2N$ 维空间。系统的任意一个瞬时状态都对应于相空间中的一个点，而系统随时间的演化则对应于相空间中的一条轨迹。

一维[简谐振子](@entry_id:145764)是理解相空间的经典范例 [@problem_id:2055720]。其[哈密顿量](@entry_id:172864)为：
$$
H(q, p) = \frac{p^2}{2m} + \frac{1}{2}kq^2
$$
由于 $H$ 不显含时间，它是一个[守恒量](@entry_id:150267)，等于系统的总能量 $E$。因此，相空间中的运动轨迹必须满足方程 $H=E$：
$$
\frac{q^2}{(\sqrt{2E/k})^2} + \frac{p^2}{(\sqrt{2mE})^2} = 1
$$
这正是一个以原点为中心，[半长轴](@entry_id:164167)分别为 $\sqrt{2E/k}$ 和 $\sqrt{2mE}$ 的[椭圆方程](@entry_id:169190)。系统的状态点就在这个椭圆上周而复始地运动，直观地展示了[振动](@entry_id:267781)的周期性。

哈密顿力学还为理解守恒律提供了深刻的见解。如果一个[广义坐标](@entry_id:156576) $q_k$ 没有在[哈密顿量](@entry_id:172864)的表达式中出现（即 $\partial H / \partial q_k = 0$），那么这个坐标就被称为**[循环坐标](@entry_id:166220) (cyclic coordinate)**。根据[哈密顿方程](@entry_id:156213) $\dot{p}_k = -\partial H / \partial q_k$，我们立即得到 $\dot{p}_k = 0$，这意味着与[循环坐标](@entry_id:166220)共轭的[广义动量](@entry_id:165699) $p_k$ 是一个守恒量。

这一原理是诺特定理在哈密顿框架下的体现：对称性导致守恒律。坐标 $q_k$ 的缺失意味着[哈密顿量](@entry_id:172864)在该坐标方向上具有平移不变性（一种对称性），这导致了动量 $p_k$ 的守恒。

例如，在一个无摩擦的圆锥内表面运动的粒子，若用距离顶点的斜距 $r$ 和绕[对称轴](@entry_id:177299)的[方位角](@entry_id:164011) $\phi$ 作为[广义坐标](@entry_id:156576)，其[哈密顿量](@entry_id:172864)为 [@problem_id:2055761]：
$$
H = \frac{p_r^2}{2m} + \frac{p_\phi^2}{2m r^2 \sin^2\alpha} + mgr\cos\alpha
$$
由于坐标 $\phi$ 未在 $H$ 中出现（$\partial H / \partial \phi = 0$），$\phi$ 是一个[循环坐标](@entry_id:166220)。因此，其[共轭动量](@entry_id:172203) $p_\phi$ 是一个[守恒量](@entry_id:150267)，代表了系统绕竖直轴的角动量守恒。

同样，对于在三维空间中运动的[自由粒子](@entry_id:148748)，使用[球坐标](@entry_id:146054) $(r, \theta, \phi)$ 描述时，其[哈密顿量](@entry_id:172864)为 [@problem_id:2055746]：
$$
H = \frac{p_r^2}{2m} + \frac{p_\theta^2}{2mr^2} + \frac{p_\phi^2}{2mr^2\sin^2\theta}
$$
这里，$\phi$ 是一个[循环坐标](@entry_id:166220)，所以 $p_\phi$（z轴方向的角动量）守恒。然而，$\theta$ 出现在了[哈密顿量](@entry_id:172864)中，因此 $p_\theta$ 不守恒，其变化率由 $\dot{p}_\theta = -\partial H / \partial \theta$ 给出，物理上对应于“离心力”产生的力矩。

### 哈密顿力学的扩展

标准的[哈密顿形式体系](@entry_id:148673)主要用于描述保守系统。然而，通过适当的修改，它也可以处理更广泛的物理情境。

**[非保守系统](@entry_id:166237)**：对于存在如[摩擦力](@entry_id:171772)之类的[非保守力](@entry_id:163431) $F_{nc}$ 的系统，可以将其效应作为一个[广义力](@entry_id:169699) $Q_k$ 添加到正则方程中：
$$
\dot{q}_i = \frac{\partial H}{\partial p_i}
$$
$$
\dot{p}_i = -\frac{\partial H}{\partial q_i} + Q_i
$$
其中 $H$ 通常只包含系统的保守部分。例如，对于一个受[斯托克斯阻力](@entry_id:168107) $F_{drag} = -\gamma \dot{x}$ 影响的[阻尼振子](@entry_id:173004) [@problem_id:2055727]，系统的[哈密顿量](@entry_id:172864)（保守能量）的变化率可以计算为：
$$
\frac{dH}{dt} = \sum_i \frac{\partial H}{\partial p_i} Q_i = \frac{\partial H}{\partial p} Q_{drag} = \left(\frac{p}{m}\right)(-\gamma \dot{x}) = \left(\frac{p}{m}\right)\left(-\gamma \frac{p}{m}\right) = -\frac{\gamma p^2}{m^2}
$$
这个结果精确地描述了能量因阻力而耗散的速率，其值总是负的，表明能量在不断减少。

**[正则变换](@entry_id:178165)**：[哈密顿力学](@entry_id:146202)的一个强大之处在于**[正则变换](@entry_id:178165) (canonical transformation)** 理论。这是一种在相空间中进行的坐标变换 $(q, p) \to (Q, P)$，它能保持[哈密顿方程](@entry_id:156213)的形式不变。也就是说，在新坐标下，存在一个新的[哈密顿量](@entry_id:172864) $K(Q, P, t)$，使得运动方程为：
$$
\dot{Q}_i = \frac{\partial K}{\partial P_i}, \quad \dot{P}_i = -\frac{\partial K}{\partial Q_i}
$$
[正则变换](@entry_id:178165)的目的是通过巧妙地选择新坐标来简化问题。理想情况下，我们希望找到一组新坐标，使得新的[哈密顿量](@entry_id:172864) $K$ 尽可能简单，例如，让所有新坐标都成为[循环坐标](@entry_id:166220)。

这种变换可以通过所谓的**[生成函数](@entry_id:146702) (generating function)** 来实现。例如，对于[简谐振子](@entry_id:145764)，可以找到一个从 $(q, p)$ 到[作用量-角度变量](@entry_id:161141) $(Q, P)$ 的[正则变换](@entry_id:178165) [@problem_id:2055763]。这个变换由第一类[生成函数](@entry_id:146702) $F_1(q, Q)$ 产生，其形式为：
$$
F_1(q, Q) = \frac{m\omega}{2} q^2 \cot Q
$$
通过关系式 $p = \partial F_1 / \partial q$ 和 $P = -\partial F_1 / \partial Q$，这个生成函数可以导出旧变量和新变量之间的联系。在[作用量-角度变量](@entry_id:161141)下，[简谐振子](@entry_id:145764)的[哈密顿量](@entry_id:172864)变为 $K = \omega P$，这是一个非常简单的形式。新的正则方程为 $\dot{Q} = \omega$ 和 $\dot{P} = 0$，其解极其平凡：$P$ 是一个常数，而 $Q$ [线性增长](@entry_id:157553)。这揭示了[正则变换](@entry_id:178165)在求解复杂动力学问题中的巨大潜力。

综上所述，哈密顿力学不仅为经典力学提供了另一套求解工具，更重要的是，它通过相空间、正则方程和[正则变换](@entry_id:178165)等概念，揭示了动力学系统的深刻几何结构和对称性，为后续的[统计力](@entry_id:194984)学和量子力学的发展奠定了坚实的基础。