## 引言
[哈密顿力学](@entry_id:146202)是继牛顿力学和[拉格朗日力学](@entry_id:147054)之后，对经典力学的又一次深刻重构。它不仅提供了一套求解力学问题的强大数学工具，更以其优美的对称性和深刻的物理内涵，成为连接经典物理与现代物理（如量子力学和[统计力](@entry_id:194984)学）的基石。与关注力和加速度的牛顿[范式](@entry_id:161181)或依赖于[广义坐标](@entry_id:156576)和速度的拉格朗日[范式](@entry_id:161181)不同，[哈密顿力学](@entry_id:146202)将我们的视角转移到了一个更为抽象和强大的“相空间”中，在这里，系统的状态由[广义坐标](@entry_id:156576)和与之共轭的[广义动量](@entry_id:165699)共同描述。

尽管对于简单问题，不同力学形式或许殊途同归，但哈密顿力学在处理复杂系统、揭示[守恒定律](@entry_id:269268)的本质以及理论推广方面展现出无与伦比的优势。本文旨在系统性地介绍[哈密顿运动方程](@entry_id:176972)的核心思想与应用。我们将填补从“知道”[拉格朗日方程](@entry_id:175419)到“理解”哈密顿形式之间存在的知识鸿沟，并展示后者为何是[理论物理学](@entry_id:154070)家的必备语言。

为了实现这一目标，本文将分为三个核心部分。在“**原理与机制**”一章中，我们将深入探讨[哈密顿力学](@entry_id:146202)的数学基础，从勒让德变换与[哈密顿量](@entry_id:172864)的构建，到哈密顿方程的建立、[泊松括号](@entry_id:151133)的引入以及[守恒定律](@entry_id:269268)的深刻内涵。接着，在“**应用与跨学科联系**”一章中，我们将展示哈密顿力学如何被应用于分析精密机械、电磁现象、天体[轨道](@entry_id:137151)，并揭示其如何成为通往混沌理论、[统计力](@entry_id:194984)学和量子力学的桥梁。最后，在“**动手实践**”部分，你将通过解决具体问题来巩固所学知识，将抽象的理论应用于实际的计算之中。

## 原理与机制

在上一章中，我们已经了解了哈密顿力学的基本出发点及其在物理学中的重要地位。本章将深入探讨[哈密顿力学](@entry_id:146202)的核心原理与关键机制，从[哈密顿量](@entry_id:172864)的构建、[哈密顿运动方程](@entry_id:176972)的建立，到[守恒定律](@entry_id:269268)的深刻内涵以及相空间的几何结构。我们将通过一系列具体的物理系统，系统地揭示这一理论框架的数学之美与物理洞察力。

### [从拉格朗日到哈密顿](@entry_id:164887)：勒让德变换与[哈密顿量](@entry_id:172864)

[分析力学](@entry_id:166738)的发展始于[拉格朗日形式](@entry_id:145697)。在[拉格朗日力学](@entry_id:147054)中，一个具有 $N$ 个自由度的物理系统的状态由一组[广义坐标](@entry_id:156576) $q_i$ 及其对应的[广义速度](@entry_id:178456) $\dot{q}_i$ 完全确定，其中 $i=1, 2, ..., N$。系统的动力学行为则蕴含在[拉格朗日量](@entry_id:174593) $L(q_i, \dot{q}_i, t)$ 之中，它通常定义为动能 $T$ 与势能 $V$ 之差，即 $L = T - V$。

[哈密顿力学](@entry_id:146202)提供了一种不同的视角。它将描述系统状态的基本变量从[广义坐标](@entry_id:156576)与[广义速度](@entry_id:178456) $(q_i, \dot{q}_i)$ 的组合，转变为[广义坐标](@entry_id:156576)与**[广义动量](@entry_id:165699)** $(q_i, p_i)$ 的组合。这个新的描述空间被称为**相空间** (phase space)。从速度到动量的转变并非任意的，而是通过一个严谨的数学工具——**[勒让德变换](@entry_id:146727)** (Legendre transformation) 来实现的。

首先，我们定义与[广义坐标](@entry_id:156576) $q_i$ 共轭的[广义动量](@entry_id:165699) $p_i$：

$$
p_i = \frac{\partial L(q_i, \dot{q}_i, t)}{\partial \dot{q}_i}
$$

这个定义建立了[广义速度](@entry_id:178456)与[广义动量](@entry_id:165699)之间的联系。在理想情况下，我们可以反解出 $\dot{q}_i$ 作为 $q_i, p_i$ 和 $t$ 的函数。接着，系统的**[哈密顿量](@entry_id:172864)** (Hamiltonian) $H$ 被定义为[拉格朗日量](@entry_id:174593) $L$ 关于[广义速度](@entry_id:178456) $\dot{q}_i$ 的[勒让德变换](@entry_id:146727)：

$$
H(q_i, p_i, t) = \sum_{i=1}^{N} p_i \dot{q}_i - L(q_i, \dot{q}_i, t)
$$

在执行变换时，我们必须用[广义动量](@entry_id:165699) $p_i$ 替换掉表达式中所有的[广义速度](@entry_id:178456) $\dot{q}_i$，从而确保最终的[哈密顿量](@entry_id:172864)是相空间坐标 $(q_i, p_i)$ 和时间 $t$ 的函数。

为了具体说明这一过程，我们来构建一个在均匀[引力场](@entry_id:169425)和[电场](@entry_id:194326)中运动的单摆的[哈密顿量](@entry_id:172864) [@problem_id:2195255]。设想一个质量为 $m$、带[电荷](@entry_id:275494)为 $q$ 的质点悬挂在长度为 $l$ 的轻杆一端，在竖直平面内摆动。系统受到竖直向下的均匀[引力场](@entry_id:169425)（[重力加速度](@entry_id:173411)为 $g$）和水平方向的均匀[电场](@entry_id:194326)（场强为 $E$）。我们选取摆角 $\theta$（与竖直向下的轴的夹角）作为[广义坐标](@entry_id:156576)。

首先，写出系统的动能 $T$ 和[势能](@entry_id:748988) $V$。[质点](@entry_id:186768)的速度大小为 $l\dot{\theta}$，因此动能为 $T = \frac{1}{2}m(l\dot{\theta})^2 = \frac{1}{2}ml^2\dot{\theta}^2$。若以悬挂点为原点，竖直向下为 $y$ 轴，水平向[电场](@entry_id:194326)方向为 $x$ 轴，则[质点](@entry_id:186768)位置为 $x = l\sin\theta, y = l\cos\theta$。[引力势能](@entry_id:269038)为 $V_g = -mgy = -mgl\cos\theta$，[电势能](@entry_id:260623)为 $V_e = -qEx = -qEl\sin\theta$。总[势能](@entry_id:748988)为 $V(\theta) = -mgl\cos\theta - qEl\sin\theta$。

拉格朗日量为 $L = T - V$：

$$
L(\theta, \dot{\theta}) = \frac{1}{2}ml^2\dot{\theta}^2 + mgl\cos\theta + qEl\sin\theta
$$

接下来，计算共轭于 $\theta$ 的[广义动量](@entry_id:165699) $p_\theta$：

$$
p_\theta = \frac{\partial L}{\partial \dot{\theta}} = ml^2\dot{\theta}
$$

由此我们可以反解出 $\dot{\theta} = \frac{p_\theta}{ml^2}$。现在，我们应用[勒让德变换](@entry_id:146727)来构建[哈密顿量](@entry_id:172864) $H$：

$$
H(\theta, p_\theta) = p_\theta \dot{\theta} - L = p_\theta \left(\frac{p_\theta}{ml^2}\right) - \left[ \frac{1}{2}ml^2\left(\frac{p_\theta}{ml^2}\right)^2 + mgl\cos\theta + qEl\sin\theta \right]
$$

化简后得到：

$$
H(\theta, p_\theta) = \frac{p_\theta^2}{ml^2} - \frac{p_\theta^2}{2ml^2} - mgl\cos\theta - qEl\sin\theta = \frac{p_\theta^2}{2ml^2} - mgl\cos\theta - qEl\sin\theta
$$

我们成功地将系统的描述从 $( \theta, \dot{\theta} )$ 空间转换到了 $( \theta, p_\theta )$ 相空间，并得到了[哈密顿量](@entry_id:172864) $H$。对于许多保守系统，其中坐标变换不显含时间，[哈密顿量](@entry_id:172864)恰好等于系统的总能量 $T+V$。在此例中，动能 $T = \frac{1}{2}ml^2\dot{\theta}^2 = \frac{p_\theta^2}{2ml^2}$，势能 $V$ 的定义是 $V = -mgl\cos\theta - qEl\sin\theta$，所以 $H = T+V$ 并不成立，而是 $H=T-V_{orig}$，其中 $V_{orig}$是[势能](@entry_id:748988)的通常定义。更准确地说，[拉格朗日量](@entry_id:174593)定义为$L=T-V$，而这里的$V$是$-mgl\cos\theta - qEl\sin\theta$。因此[哈密顿量](@entry_id:172864)为$H=\frac{p_\theta^2}{2ml^2} + V(\theta) = \frac{p_\theta^2}{2ml^2} - mgl\cos\theta - qEl\sin\theta$。此处原文的表述 $H=T+V$ 成立是有歧义的。应修正为：在此例中，动能 $T = \frac{1}{2}ml^2\dot{\theta}^2 = \frac{p_\theta^2}{2ml^2}$，而势能 $V = -mgl\cos\theta - qEl\sin\theta$。因此[哈密顿量](@entry_id:172864) $H = \frac{p_\theta^2}{2ml^2} + V$ 成立。

### [哈密顿方程](@entry_id:156213)：相空间的动力学

一旦我们拥有了[哈密顿量](@entry_id:172864) $H(q_i, p_i, t)$，系统的动力学演化就由一组优美对称的[一阶微分方程](@entry_id:173139)——**[哈密顿方程](@entry_id:156213)** (Hamilton's equations)——所支配：

$$
\dot{q}_i = \frac{\partial H}{\partial p_i}, \quad \dot{p}_i = - \frac{\partial H}{\partial q_i}
$$

这组方程描述了相空间中一个点 $(q_i(t), p_i(t))$ 如何随时间流逝。每个点的轨迹代表了系统的一种可能的演化历史。这组方程的对称性是[哈密顿力学](@entry_id:146202)的标志性特征之一：一个坐标的时间变化率由[哈密顿量](@entry_id:172864)对相应动量的偏导数给出，而一个动量的时间变化率则由[哈密顿量](@entry_id:172864)对相应坐标的[偏导数](@entry_id:146280)的负值给出。

让我们考察一个在一维[非谐势](@entry_id:141227) $V(x) = \alpha x^4$（其中 $\alpha > 0$）中运动的粒子 [@problem_id:2195217]。这个模型可以简化描述光学镊子中微球的运动。该系统的[哈密顿量](@entry_id:172864)为动能与[势能](@entry_id:748988)之和：

$$
H(x, p) = \frac{p^2}{2m} + \alpha x^4
$$

应用[哈密顿方程](@entry_id:156213)，我们可以立即得到相空间坐标 $(x, p)$ 的时间演化方程：

$$
\dot{x} = \frac{\partial H}{\partial p} = \frac{\partial}{\partial p}\left(\frac{p^2}{2m} + \alpha x^4\right) = \frac{p}{m}
$$

$$
\dot{p} = - \frac{\partial H}{\partial x} = - \frac{\partial}{\partial x}\left(\frac{p^2}{2m} + \alpha x^4\right) = -4\alpha x^3
$$

我们得到了一组耦合的[一阶微分方程](@entry_id:173139) $(\dot{x}, \dot{p}) = (\frac{p}{m}, -4\alpha x^3)$。这组方程完全决定了系统的运动。第一个方程 $\dot{x} = p/m$ 只是重申了我们熟悉的动量定义 $p=m\dot{x}$。第二个方程 $\dot{p} = -4\alpha x^3$ 则是[牛顿第二定律](@entry_id:274217)的体现，因为力 $F = -\frac{dV}{dx} = -4\alpha x^3$，而 $\dot{p}$ 正是动量的时间变化率。这表明，[哈密顿方程](@entry_id:156213)与我们已知的物理定律是完全自洽的。

### [哈密顿量](@entry_id:172864)与[能量守恒](@entry_id:140514)

[守恒定律](@entry_id:269268)在物理学中占据核心地位。[哈密顿力学](@entry_id:146202)为理解[守恒量](@entry_id:150267)，特别是[能量守恒](@entry_id:140514)，提供了深刻的见解。一个自然的问题是：在何种条件下，[哈密顿量](@entry_id:172864) $H$ 本身是一个[守恒量](@entry_id:150267)，即不随时间变化？

为了回答这个问题，我们来计算[哈密顿量](@entry_id:172864) $H(q_i, p_i, t)$ 的全时间导数 $\frac{dH}{dt}$。根据[多元函数](@entry_id:145643)的[链式法则](@entry_id:190743)：

$$
\frac{dH}{dt} = \sum_{i=1}^{N} \left( \frac{\partial H}{\partial q_i}\dot{q}_i + \frac{\partial H}{\partial p_i}\dot{p}_i \right) + \frac{\partial H}{\partial t}
$$

现在，我们可以将[哈密顿方程](@entry_id:156213) $\dot{q}_i = \partial H / \partial p_i$ 和 $\dot{p}_i = - \partial H / \partial q_i$ 代入上式：

$$
\frac{dH}{dt} = \sum_{i=1}^{N} \left( \frac{\partial H}{\partial q_i}\left(\frac{\partial H}{\partial p_i}\right) + \frac{\partial H}{\partial p_i}\left(-\frac{\partial H}{\partial q_i}\right) \right) + \frac{\partial H}{\partial t} = \sum_{i=1}^{N} \left( \frac{\partial H}{\partial q_i}\frac{\partial H}{\partial p_i} - \frac{\partial H}{\partial p_i}\frac{\partial H}{\partial q_i} \right) + \frac{\partial H}{\partial t}
$$

括号内的项相互抵消，我们得到了一个极为简洁且重要的结果：

$$
\frac{dH}{dt} = \frac{\partial H}{\partial t}
$$

这个方程告诉我们，[哈密顿量](@entry_id:172864) $H$ 的总时间变化率等于它对时间的偏导数。因此，**[哈密顿量](@entry_id:172864) $H$ 是一个守恒量（即 $\frac{dH}{dt} = 0$）的充分必要条件是[哈密顿量](@entry_id:172864)本身不显含时间（即 $\frac{\partial H}{\partial t} = 0$）**。

进一步地，通过对哈密顿定义的分析可以证明 $\frac{\partial H}{\partial t} = -\frac{\partial L}{\partial t}$ [@problem_id:2195201]。因此，[哈密顿量守恒](@entry_id:164570)的条件等价于[拉格朗日量](@entry_id:174593) $L$ 不显含时间。对于大多数物理系统，这个条件对应于系统的总[能量守恒](@entry_id:140514)。

当[哈密顿量](@entry_id:172864)显含时间时，它通常不再守恒。例如，考虑一个受时间依赖的谐振子势阱约束的粒子，其[哈密顿量](@entry_id:172864)为 $H(q, p, t) = \frac{p^2}{2m} + \frac{1}{2}m\omega(t)^2 q^2$ [@problem_id:1247199]。由于角频率 $\omega(t)$ 随时间变化，[哈密顿量](@entry_id:172864)显含时间。其能量变化率为：

$$
\frac{dH}{dt} = \frac{\partial H}{\partial t} = \frac{\partial}{\partial t}\left(\frac{1}{2}m\omega(t)^2 q^2\right) = m\omega(t)\dot{\omega}(t)q^2
$$

这表明系统的能量不再守恒，其变化率与外部参数 $\omega(t)$ 的变化方式直接相关。

### 泊松括号与[守恒定律](@entry_id:269268)

哈密顿力学引入了一个强大的数学工具——**[泊松括号](@entry_id:151133)** (Poisson bracket)，它极大地简化了[守恒定律](@entry_id:269268)的表述和物理量的演化分析。对于任意两个相空间函数 $A(q_i, p_i, t)$ 和 $B(q_i, p_i, t)$，它们的泊松括号定义为：

$$
\{A, B\} = \sum_{i=1}^{N} \left( \frac{\partial A}{\partial q_i}\frac{\partial B}{\partial p_i} - \frac{\partial A}{\partial p_i}\frac{\partial B}{\partial q_i} \right)
$$

利用泊松括号，哈密顿方程可以被写成更紧凑的形式。例如，$\dot{q}_i = \{q_i, H\}$ 和 $\dot{p}_i = \{p_i, H\}$。更一般地，任何一个不显含时间的相空间函数 $A(q,p)$ 的[时间演化](@entry_id:153943)都可以由它与[哈密顿量](@entry_id:172864)的泊松括号给出：

$$
\frac{dA}{dt} = \{A, H\}
$$

如果函数 $A$ 还显含时间，则其全时间导数为 $\frac{dA}{dt} = \{A, H\} + \frac{\partial A}{\partial t}$。从这个关系可以立刻看出，**一个不显含时间的物理量 $A$ 是守恒的，当且仅当它与系统[哈密顿量](@entry_id:172864)的[泊松括号](@entry_id:151133)为零，即 $\{A, H\} = 0$**。这个结论是[哈密顿力学](@entry_id:146202)中[诺特定理](@entry_id:145690)（[对称性与守恒](@entry_id:154858)定律的对应关系）的直接体现。

一个简单的例子是**[循环坐标](@entry_id:166220)** (cyclic coordinate)。如果某个[广义坐标](@entry_id:156576) $q_k$ 没有在[哈密顿量](@entry_id:172864)中出现（即 $\partial H / \partial q_k = 0$），我们称其为[循环坐标](@entry_id:166220)。根据[哈密顿方程](@entry_id:156213)，其[共轭动量](@entry_id:172203)的时间变化率为 $\dot{p}_k = - \partial H / \partial q_k = 0$。这意味着 $p_k$ 是一个守恒量。用泊松括号的语言来说，$\{p_k, H\} = \sum_i (\frac{\partial p_k}{\partial q_i}\frac{\partial H}{\partial p_i} - \frac{\partial p_k}{\partial p_i}\frac{\partial H}{\partial q_i}) = -\frac{\partial H}{\partial q_k} = 0$，因此 $p_k$ 守恒。例如，在均匀[引力场](@entry_id:169425)中运动的抛射体，其[哈密顿量](@entry_id:172864)为 $H = \frac{p_x^2 + p_y^2}{2m} + mgy$ [@problem_id:2195203]。坐标 $x$ 未在 $H$ 中出现，因此 $x$ 是[循环坐标](@entry_id:166220)，其[共轭动量](@entry_id:172203) $p_x$ 守恒，这对应于水平方向[动量守恒](@entry_id:149964)。

[泊松括号](@entry_id:151133)在分析角动量守恒等更复杂的对称性时威力尽显。角动量矢量 $\mathbf{L} = \mathbf{r} \times \mathbf{p}$ 的第 $x$ 分量为 $L_x = y p_z - z p_y$。它对时间的导数即为力矩的 $x$ 分量 $\tau_x$，可以用泊松括号计算：$\dot{L}_x = \{L_x, H\}$。如果一个粒子在[中心势](@entry_id:148563) $V(r)$ 中运动，其中 $r = |\mathbf{r}|$，其[哈密顿量](@entry_id:172864) $H = \frac{\mathbf{p}^2}{2m} + V(r)$ 具有旋转对称性。可以证明，在这种情况下，$\{\mathbf{L}, H\} = 0$，这意味着角动量矢量的所有分量都守恒。如果势场包含一个非[中心力](@entry_id:267832)部分，例如 $V_{nc} = \frac{p_0 z}{r^3}$，那么对称性被破坏，角动量不再守恒 [@problem_id:1247242]。计算表明 $\{L_x, H\} = \{L_x, V_{nc}\} = -\frac{p_0 y}{r^3}$，这正是在该势场中作用在粒子上的力矩的 $x$ 分量。

### 相空间流与[刘维尔定理](@entry_id:191167)

哈密顿方程不仅描述了单个系统状态点在相空间中的轨迹，还支配着一个由大量初始状态构成的“云”（系综）的整体演化。一个深刻且优美的结果是**刘维尔定理** (Liouville's theorem)，它指出，在[哈密顿系统](@entry_id:143533)[演化过程](@entry_id:175749)中，相空间中任意一块区域的体积是保持不变的。换句话说，相空间的“流体”是不可压缩的。

我们可以通过一个具体的例子来直观理解这个定理。考虑一个一维简谐振子，其[哈密顿量](@entry_id:172864)为 $H = \frac{p^2}{2m} + \frac{1}{2}m\omega^2q^2$。其[运动方程](@entry_id:170720)的解为：

$$
q(t) = q_0\cos(\omega t) + \frac{p_0}{m\omega}\sin(\omega t)
$$
$$
p(t) = p_0\cos(\omega t) - m\omega q_0\sin(\omega t)
$$

其中 $(q_0, p_0)$ 是初始时刻 $t=0$ 的相空间坐标。这个[演化过程](@entry_id:175749)是一个从 $(q_0, p_0)$到 $(q(t), p(t))$ 的[线性变换](@entry_id:149133)。我们可以考察这个变换如何改变一个微小的相空间面积元。一个初始位于 $[q_0, q_0+\delta q]$ 和 $[p_0, p_0+\delta p]$ 的矩形区域，其面积为 $\delta q \delta p$。经过时间 $t$ 后，这个矩形会变成一个平行四边形，其面积由变换的[雅可比行列式](@entry_id:137120)决定 [@problem_id:2195239]。该变换的[雅可比矩阵](@entry_id:264467) $J(t)$ 为：

$$
J(t) = \begin{pmatrix} \frac{\partial q(t)}{\partial q_0} & \frac{\partial q(t)}{\partial p_0} \\ \frac{\partial p(t)}{\partial q_0} & \frac{\partial p(t)}{\partial p_0} \end{pmatrix} = \begin{pmatrix} \cos(\omega t) & \frac{1}{m\omega}\sin(\omega t) \\ -m\omega\sin(\omega t) & \cos(\omega t) \end{pmatrix}
$$

其[行列式](@entry_id:142978)为：

$$
\det J(t) = \cos^2(\omega t) - \left(\frac{1}{m\omega}\sin(\omega t)\right)(-m\omega\sin(\omega t)) = \cos^2(\omega t) + \sin^2(\omega t) = 1
$$

由于[雅可比行列式](@entry_id:137120)恒等于 1，任何初始区域的面积在演化过程中都保持不变。初始的矩形可能会被拉伸和剪切，但其总面积 $\delta q \delta p$ 始终如一。这正是刘维尔定理在二维相空间中的体现。这个定理是[统计力](@entry_id:194984)学的基石，因为它保证了相空间中概率密度的守恒。

### [正则变换](@entry_id:178165)与[哈密顿-雅可比理论](@entry_id:165642)

[哈密顿力学](@entry_id:146202)的一个强大之处在于其形式在某类特殊的坐标变换下保持不变。这种变换被称为**[正则变换](@entry_id:178165)** (canonical transformation)，它将一组[正则坐标](@entry_id:175654) $(q, p)$ 变换为一组新的[正则坐标](@entry_id:175654) $(Q, P)$，而[运动方程](@entry_id:170720)在新坐标下仍然保持哈密顿形式 $\dot{Q} = \partial K/\partial P, \dot{P} = -\partial K/\partial Q$，其中 $K(Q, P, t)$ 是新的[哈密顿量](@entry_id:172864)。

检验一个变换是否为[正则变换](@entry_id:178165)的一种方法是计算**基本[泊松括号](@entry_id:151133)**。一个从 $(q, p)$ 到 $(Q(q,p), P(q,p))$ 的变换是正则的，条件是 $\{Q, P\}_{qp} = 1$（同时 $\{Q, Q\}_{qp} = 0$ 和 $\{P, P\}_{qp} = 0$）。例如，考虑变换 $Q = q^2, P = p/(2q)$ [@problem_id:1247111]。我们可以计算其泊松括号：

$$
\{Q, P\}_{qp} = \frac{\partial Q}{\partial q}\frac{\partial P}{\partial p} - \frac{\partial Q}{\partial p}\frac{\partial P}{\partial q} = (2q)\left(\frac{1}{2q}\right) - (0)\left(-\frac{p}{2q^2}\right) = 1
$$

由于结果为 1，这个变换是正则的。

[正则变换](@entry_id:178165)的目的是为了简化问题。最理想的情况是找到一个变换，使得新的[哈密顿量](@entry_id:172864) $K$ 变得非常简单，例如只依赖于新的动量 $P$，甚至为零。如果能做到这一点，新的运动方程将变得平凡可解。寻找这种理想变换的系统性方法导向了**[哈密顿-雅可比理论](@entry_id:165642)** (Hamilton-Jacobi theory)。

该理论的核心是求解[哈密顿-雅可比方程](@entry_id:145701)，这是一个关于所谓**生成函数** $S$ 的[一阶偏微分方程](@entry_id:178306)。这个[生成函数](@entry_id:146702)定义了从旧坐标到新坐标的[正则变换](@entry_id:178165)。例如，对于一个在势 $V(q) = C/q^2$ 中运动的粒子，其[哈密顿量](@entry_id:172864)为 $H(q,p) = \frac{p^2}{2m} + \frac{C}{q^2}$ [@problem_id:1247190]。我们可以尝试寻找一个[正则变换](@entry_id:178165)，使得新的[哈密顿量](@entry_id:172864)就是新的动量，即 $K=P$。[哈密顿-雅可比方程](@entry_id:145701)此时变为：

$$
H\left(q, \frac{\partial S}{\partial q}\right) = P \quad \Rightarrow \quad \frac{1}{2m}\left(\frac{\partial S}{\partial q}\right)^2 + \frac{C}{q^2} = P
$$

通过求解这个方程得到[生成函数](@entry_id:146702) $S(q,P)$，我们就能找到新旧坐标之间的关系，例如新坐标 $Q = \partial S/\partial P$。这个过程虽然在数学上更具挑战性，但它为求解复杂的力学问题提供了一条强大的路径，并构成了经典力学与量子力学之间的重要桥梁。