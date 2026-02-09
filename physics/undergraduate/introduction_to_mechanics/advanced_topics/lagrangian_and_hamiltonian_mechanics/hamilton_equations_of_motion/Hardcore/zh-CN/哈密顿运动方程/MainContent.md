## 引言
哈密顿力学是继牛顿力学和拉格朗日力学之后，对经典力学的又一次深刻重构。它不仅提供了一套求解力学问题的强大数学工具，更以其优美的对称性和深刻的物理内涵，成为连接经典物理与现代物理（如量子力学和统计力学）的基石。与关注力和加速度的牛顿范式或依赖于广义坐标和速度的拉格朗日范式不同，哈密顿力学将我们的视角转移到了一个更为抽象和强大的“相空间”中，在这里，系统的状态由广义坐标和与之共轭的广义动量共同描述。

尽管对于简单问题，不同力学形式或许殊途同归，但哈密顿力学在处理复杂系统、揭示守恒定律的本质以及理论推广方面展现出无与伦比的优势。本文旨在系统性地介绍哈密顿运动方程的核心思想与应用。我们将填补从“知道”拉格朗日方程到“理解”哈密顿形式之间存在的知识鸿沟，并展示后者为何是理论物理学家的必备语言。

为了实现这一目标，本文将分为三个核心部分。在“**原理与机制**”一章中，我们将深入探讨哈密顿力学的数学基础，从勒让德变换与哈密顿量的构建，到哈密顿方程的建立、泊松括号的引入以及守恒定律的深刻内涵。接着，在“**应用与跨学科联系**”一章中，我们将展示哈密顿力学如何被应用于分析精密机械、电磁现象、天体轨道，并揭示其如何成为通往混沌理论、统计力学和量子力学的桥梁。最后，在“**动手实践**”部分，你将通过解决具体问题来巩固所学知识，将抽象的理论应用于实际的计算之中。

## 原理与机制

在上一章中，我们已经了解了哈密顿力学的基本出发点及其在物理学中的重要地位。本章将深入探讨哈密顿力学的核心原理与关键机制，从哈密顿量的构建、哈密顿运动方程的建立，到守恒定律的深刻内涵以及相空间的几何结构。我们将通过一系列具体的物理系统，系统地揭示这一理论框架的数学之美与物理洞察力。

### 从拉格朗日到哈密顿：勒让德变换与哈密顿量

分析力学的发展始于拉格朗日形式。在拉格朗日力学中，一个具有 $N$ 个自由度的物理系统的状态由一组广义坐标 $q_i$ 及其对应的广义速度 $\dot{q}_i$ 完全确定，其中 $i=1, 2, ..., N$。系统的动力学行为则蕴含在拉格朗日量 $L(q_i, \dot{q}_i, t)$ 之中，它通常定义为动能 $T$ 与势能 $V$ 之差，即 $L = T - V$。

哈密顿力学提供了一种不同的视角。它将描述系统状态的基本变量从广义坐标与广义速度 $(q_i, \dot{q}_i)$ 的组合，转变为广义坐标与**广义动量** $(q_i, p_i)$ 的组合。这个新的描述空间被称为**相空间** (phase space)。从速度到动量的转变并非任意的，而是通过一个严谨的数学工具——**勒让德变换** (Legendre transformation) 来实现的。

首先，我们定义与广义坐标 $q_i$ 共轭的广义动量 $p_i$：

$$
p_i = \frac{\partial L(q_i, \dot{q}_i, t)}{\partial \dot{q}_i}
$$

这个定义建立了广义速度与广义动量之间的联系。在理想情况下，我们可以反解出 $\dot{q}_i$ 作为 $q_i, p_i$ 和 $t$ 的函数。接着，系统的**哈密顿量** (Hamiltonian) $H$ 被定义为拉格朗日量 $L$ 关于广义速度 $\dot{q}_i$ 的勒让德变换：

$$
H(q_i, p_i, t) = \sum_{i=1}^{N} p_i \dot{q}_i - L(q_i, \dot{q}_i, t)
$$

在执行变换时，我们必须用广义动量 $p_i$ 替换掉表达式中所有的广义速度 $\dot{q}_i$，从而确保最终的哈密顿量是相空间坐标 $(q_i, p_i)$ 和时间 $t$ 的函数。

为了具体说明这一过程，我们来构建一个在均匀引力场和电场中运动的单摆的哈密顿量 [@problem_id:2195255]。设想一个质量为 $m$、带电荷为 $q$ 的质点悬挂在长度为 $l$ 的轻杆一端，在竖直平面内摆动。系统受到竖直向下的均匀引力场（重力加速度为 $g$）和水平方向的均匀电场（场强为 $E$）。我们选取摆角 $\theta$（与竖直向下的轴的夹角）作为广义坐标。

首先，写出系统的动能 $T$ 和势能 $V$。质点的速度大小为 $l\dot{\theta}$，因此动能为 $T = \frac{1}{2}m(l\dot{\theta})^2 = \frac{1}{2}ml^2\dot{\theta}^2$。若以悬挂点为原点，竖直向下为 $y$ 轴，水平向电场方向为 $x$ 轴，则质点位置为 $x = l\sin\theta, y = l\cos\theta$。引力势能为 $V_g = -mgy = -mgl\cos\theta$，电势能为 $V_e = -qEx = -qEl\sin\theta$。总势能为 $V(\theta) = -mgl\cos\theta - qEl\sin\theta$。

拉格朗日量为 $L = T - V$：

$$
L(\theta, \dot{\theta}) = \frac{1}{2}ml^2\dot{\theta}^2 + mgl\cos\theta + qEl\sin\theta
$$

接下来，计算共轭于 $\theta$ 的广义动量 $p_\theta$：

$$
p_\theta = \frac{\partial L}{\partial \dot{\theta}} = ml^2\dot{\theta}
$$

由此我们可以反解出 $\dot{\theta} = \frac{p_\theta}{ml^2}$。现在，我们应用勒让德变换来构建哈密顿量 $H$：

$$
H(\theta, p_\theta) = p_\theta \dot{\theta} - L = p_\theta \left(\frac{p_\theta}{ml^2}\right) - \left[ \frac{1}{2}ml^2\left(\frac{p_\theta}{ml^2}\right)^2 + mgl\cos\theta + qEl\sin\theta \right]
$$

化简后得到：

$$
H(\theta, p_\theta) = \frac{p_\theta^2}{ml^2} - \frac{p_\theta^2}{2ml^2} - mgl\cos\theta - qEl\sin\theta = \frac{p_\theta^2}{2ml^2} - mgl\cos\theta - qEl\sin\theta
$$

我们成功地将系统的描述从 $( \theta, \dot{\theta} )$ 空间转换到了 $( \theta, p_\theta )$ 相空间，并得到了哈密顿量 $H$。对于许多保守系统，其中坐标变换不显含时间，哈密顿量恰好等于系统的总能量 $T+V$。在此例中，动能 $T = \frac{1}{2}ml^2\dot{\theta}^2 = \frac{p_\theta^2}{2ml^2}$，势能 $V$ 的定义是 $V = -mgl\cos\theta - qEl\sin\theta$，所以 $H = T+V$ 并不成立，而是 $H=T-V_{orig}$，其中 $V_{orig}$是势能的通常定义。更准确地说，拉格朗日量定义为$L=T-V$，而这里的$V$是$-mgl\cos\theta - qEl\sin\theta$。因此哈密顿量为$H=\frac{p_\theta^2}{2ml^2} + V(\theta) = \frac{p_\theta^2}{2ml^2} - mgl\cos\theta - qEl\sin\theta$。此处原文的表述 $H=T+V$ 成立是有歧义的。应修正为：在此例中，动能 $T = \frac{1}{2}ml^2\dot{\theta}^2 = \frac{p_\theta^2}{2ml^2}$，而势能 $V = -mgl\cos\theta - qEl\sin\theta$。因此哈密顿量 $H = \frac{p_\theta^2}{2ml^2} + V$ 成立。

### 哈密顿方程：相空间的动力学

一旦我们拥有了哈密顿量 $H(q_i, p_i, t)$，系统的动力学演化就由一组优美对称的一阶微分方程——**哈密顿方程** (Hamilton's equations)——所支配：

$$
\dot{q}_i = \frac{\partial H}{\partial p_i}, \quad \dot{p}_i = - \frac{\partial H}{\partial q_i}
$$

这组方程描述了相空间中一个点 $(q_i(t), p_i(t))$ 如何随时间流逝。每个点的轨迹代表了系统的一种可能的演化历史。这组方程的对称性是哈密顿力学的标志性特征之一：一个坐标的时间变化率由哈密顿量对相应动量的偏导数给出，而一个动量的时间变化率则由哈密顿量对相应坐标的偏导数的负值给出。

让我们考察一个在一维非谐势 $V(x) = \alpha x^4$（其中 $\alpha > 0$）中运动的粒子 [@problem_id:2195217]。这个模型可以简化描述光学镊子中微球的运动。该系统的哈密顿量为动能与势能之和：

$$
H(x, p) = \frac{p^2}{2m} + \alpha x^4
$$

应用哈密顿方程，我们可以立即得到相空间坐标 $(x, p)$ 的时间演化方程：

$$
\dot{x} = \frac{\partial H}{\partial p} = \frac{\partial}{\partial p}\left(\frac{p^2}{2m} + \alpha x^4\right) = \frac{p}{m}
$$

$$
\dot{p} = - \frac{\partial H}{\partial x} = - \frac{\partial}{\partial x}\left(\frac{p^2}{2m} + \alpha x^4\right) = -4\alpha x^3
$$

我们得到了一组耦合的一阶微分方程 $(\dot{x}, \dot{p}) = (\frac{p}{m}, -4\alpha x^3)$。这组方程完全决定了系统的运动。第一个方程 $\dot{x} = p/m$ 只是重申了我们熟悉的动量定义 $p=m\dot{x}$。第二个方程 $\dot{p} = -4\alpha x^3$ 则是牛顿第二定律的体现，因为力 $F = -\frac{dV}{dx} = -4\alpha x^3$，而 $\dot{p}$ 正是动量的时间变化率。这表明，哈密顿方程与我们已知的物理定律是完全自洽的。

### 哈密顿量与能量守恒

守恒定律在物理学中占据核心地位。哈密顿力学为理解守恒量，特别是能量守恒，提供了深刻的见解。一个自然的问题是：在何种条件下，哈密顿量 $H$ 本身是一个守恒量，即不随时间变化？

为了回答这个问题，我们来计算哈密顿量 $H(q_i, p_i, t)$ 的全时间导数 $\frac{dH}{dt}$。根据多元函数的链式法则：

$$
\frac{dH}{dt} = \sum_{i=1}^{N} \left( \frac{\partial H}{\partial q_i}\dot{q}_i + \frac{\partial H}{\partial p_i}\dot{p}_i \right) + \frac{\partial H}{\partial t}
$$

现在，我们可以将哈密顿方程 $\dot{q}_i = \partial H / \partial p_i$ 和 $\dot{p}_i = - \partial H / \partial q_i$ 代入上式：

$$
\frac{dH}{dt} = \sum_{i=1}^{N} \left( \frac{\partial H}{\partial q_i}\left(\frac{\partial H}{\partial p_i}\right) + \frac{\partial H}{\partial p_i}\left(-\frac{\partial H}{\partial q_i}\right) \right) + \frac{\partial H}{\partial t} = \sum_{i=1}^{N} \left( \frac{\partial H}{\partial q_i}\frac{\partial H}{\partial p_i} - \frac{\partial H}{\partial p_i}\frac{\partial H}{\partial q_i} \right) + \frac{\partial H}{\partial t}
$$

括号内的项相互抵消，我们得到了一个极为简洁且重要的结果：

$$
\frac{dH}{dt} = \frac{\partial H}{\partial t}
$$

这个方程告诉我们，哈密顿量 $H$ 的总时间变化率等于它对时间的偏导数。因此，**哈密顿量 $H$ 是一个守恒量（即 $\frac{dH}{dt} = 0$）的充分必要条件是哈密顿量本身不显含时间（即 $\frac{\partial H}{\partial t} = 0$）**。

进一步地，通过对哈密顿定义的分析可以证明 $\frac{\partial H}{\partial t} = -\frac{\partial L}{\partial t}$ [@problem_id:2195201]。因此，哈密顿量守恒的条件等价于拉格朗日量 $L$ 不显含时间。对于大多数物理系统，这个条件对应于系统的总能量守恒。

当哈密顿量显含时间时，它通常不再守恒。例如，考虑一个受时间依赖的谐振子势阱约束的粒子，其哈密顿量为 $H(q, p, t) = \frac{p^2}{2m} + \frac{1}{2}m\omega(t)^2 q^2$ [@problem_id:1247199]。由于角频率 $\omega(t)$ 随时间变化，哈密顿量显含时间。其能量变化率为：

$$
\frac{dH}{dt} = \frac{\partial H}{\partial t} = \frac{\partial}{\partial t}\left(\frac{1}{2}m\omega(t)^2 q^2\right) = m\omega(t)\dot{\omega}(t)q^2
$$

这表明系统的能量不再守恒，其变化率与外部参数 $\omega(t)$ 的变化方式直接相关。

### 泊松括号与守恒定律

哈密顿力学引入了一个强大的数学工具——**泊松括号** (Poisson bracket)，它极大地简化了守恒定律的表述和物理量的演化分析。对于任意两个相空间函数 $A(q_i, p_i, t)$ 和 $B(q_i, p_i, t)$，它们的泊松括号定义为：

$$
\{A, B\} = \sum_{i=1}^{N} \left( \frac{\partial A}{\partial q_i}\frac{\partial B}{\partial p_i} - \frac{\partial A}{\partial p_i}\frac{\partial B}{\partial q_i} \right)
$$

利用泊松括号，哈密顿方程可以被写成更紧凑的形式。例如，$\dot{q}_i = \{q_i, H\}$ 和 $\dot{p}_i = \{p_i, H\}$。更一般地，任何一个不显含时间的相空间函数 $A(q,p)$ 的时间演化都可以由它与哈密顿量的泊松括号给出：

$$
\frac{dA}{dt} = \{A, H\}
$$

如果函数 $A$ 还显含时间，则其全时间导数为 $\frac{dA}{dt} = \{A, H\} + \frac{\partial A}{\partial t}$。从这个关系可以立刻看出，**一个不显含时间的物理量 $A$ 是守恒的，当且仅当它与系统哈密顿量的泊松括号为零，即 $\{A, H\} = 0$**。这个结论是哈密顿力学中诺特定理（对称性与守恒定律的对应关系）的直接体现。

一个简单的例子是**循环坐标** (cyclic coordinate)。如果某个广义坐标 $q_k$ 没有在哈密顿量中出现（即 $\partial H / \partial q_k = 0$），我们称其为循环坐标。根据哈密顿方程，其共轭动量的时间变化率为 $\dot{p}_k = - \partial H / \partial q_k = 0$。这意味着 $p_k$ 是一个守恒量。用泊松括号的语言来说，$\{p_k, H\} = \sum_i (\frac{\partial p_k}{\partial q_i}\frac{\partial H}{\partial p_i} - \frac{\partial p_k}{\partial p_i}\frac{\partial H}{\partial q_i}) = -\frac{\partial H}{\partial q_k} = 0$，因此 $p_k$ 守恒。例如，在均匀引力场中运动的抛射体，其哈密顿量为 $H = \frac{p_x^2 + p_y^2}{2m} + mgy$ [@problem_id:2195203]。坐标 $x$ 未在 $H$ 中出现，因此 $x$ 是循环坐标，其共轭动量 $p_x$ 守恒，这对应于水平方向动量守恒。

泊松括号在分析角动量守恒等更复杂的对称性时威力尽显。角动量矢量 $\mathbf{L} = \mathbf{r} \times \mathbf{p}$ 的第 $x$ 分量为 $L_x = y p_z - z p_y$。它对时间的导数即为力矩的 $x$ 分量 $\tau_x$，可以用泊松括号计算：$\dot{L}_x = \{L_x, H\}$。如果一个粒子在中心势 $V(r)$ 中运动，其中 $r = |\mathbf{r}|$，其哈密顿量 $H = \frac{\mathbf{p}^2}{2m} + V(r)$ 具有旋转对称性。可以证明，在这种情况下，$\{\mathbf{L}, H\} = 0$，这意味着角动量矢量的所有分量都守恒。如果势场包含一个非中心力部分，例如 $V_{nc} = \frac{p_0 z}{r^3}$，那么对称性被破坏，角动量不再守恒 [@problem_id:1247242]。计算表明 $\{L_x, H\} = \{L_x, V_{nc}\} = -\frac{p_0 y}{r^3}$，这正是在该势场中作用在粒子上的力矩的 $x$ 分量。

### 相空间流与刘维尔定理

哈密顿方程不仅描述了单个系统状态点在相空间中的轨迹，还支配着一个由大量初始状态构成的“云”（系综）的整体演化。一个深刻且优美的结果是**刘维尔定理** (Liouville's theorem)，它指出，在哈密顿系统演化过程中，相空间中任意一块区域的体积是保持不变的。换句话说，相空间的“流体”是不可压缩的。

我们可以通过一个具体的例子来直观理解这个定理。考虑一个一维简谐振子，其哈密顿量为 $H = \frac{p^2}{2m} + \frac{1}{2}m\omega^2q^2$。其运动方程的解为：

$$
q(t) = q_0\cos(\omega t) + \frac{p_0}{m\omega}\sin(\omega t)
$$
$$
p(t) = p_0\cos(\omega t) - m\omega q_0\sin(\omega t)
$$

其中 $(q_0, p_0)$ 是初始时刻 $t=0$ 的相空间坐标。这个演化过程是一个从 $(q_0, p_0)$到 $(q(t), p(t))$ 的线性变换。我们可以考察这个变换如何改变一个微小的相空间面积元。一个初始位于 $[q_0, q_0+\delta q]$ 和 $[p_0, p_0+\delta p]$ 的矩形区域，其面积为 $\delta q \delta p$。经过时间 $t$ 后，这个矩形会变成一个平行四边形，其面积由变换的雅可比行列式决定 [@problem_id:2195239]。该变换的雅可比矩阵 $J(t)$ 为：

$$
J(t) = \begin{pmatrix} \frac{\partial q(t)}{\partial q_0} & \frac{\partial q(t)}{\partial p_0} \\ \frac{\partial p(t)}{\partial q_0} & \frac{\partial p(t)}{\partial p_0} \end{pmatrix} = \begin{pmatrix} \cos(\omega t) & \frac{1}{m\omega}\sin(\omega t) \\ -m\omega\sin(\omega t) & \cos(\omega t) \end{pmatrix}
$$

其行列式为：

$$
\det J(t) = \cos^2(\omega t) - \left(\frac{1}{m\omega}\sin(\omega t)\right)(-m\omega\sin(\omega t)) = \cos^2(\omega t) + \sin^2(\omega t) = 1
$$

由于雅可比行列式恒等于 1，任何初始区域的面积在演化过程中都保持不变。初始的矩形可能会被拉伸和剪切，但其总面积 $\delta q \delta p$ 始终如一。这正是刘维尔定理在二维相空间中的体现。这个定理是统计力学的基石，因为它保证了相空间中概率密度的守恒。

### 正则变换与哈密顿-雅可比理论

哈密顿力学的一个强大之处在于其形式在某类特殊的坐标变换下保持不变。这种变换被称为**正则变换** (canonical transformation)，它将一组正则坐标 $(q, p)$ 变换为一组新的正则坐标 $(Q, P)$，而运动方程在新坐标下仍然保持哈密顿形式 $\dot{Q} = \partial K/\partial P, \dot{P} = -\partial K/\partial Q$，其中 $K(Q, P, t)$ 是新的哈密顿量。

检验一个变换是否为正则变换的一种方法是计算**基本泊松括号**。一个从 $(q, p)$ 到 $(Q(q,p), P(q,p))$ 的变换是正则的，条件是 $\{Q, P\}_{qp} = 1$（同时 $\{Q, Q\}_{qp} = 0$ 和 $\{P, P\}_{qp} = 0$）。例如，考虑变换 $Q = q^2, P = p/(2q)$ [@problem_id:1247111]。我们可以计算其泊松括号：

$$
\{Q, P\}_{qp} = \frac{\partial Q}{\partial q}\frac{\partial P}{\partial p} - \frac{\partial Q}{\partial p}\frac{\partial P}{\partial q} = (2q)\left(\frac{1}{2q}\right) - (0)\left(-\frac{p}{2q^2}\right) = 1
$$

由于结果为 1，这个变换是正则的。

正则变换的目的是为了简化问题。最理想的情况是找到一个变换，使得新的哈密顿量 $K$ 变得非常简单，例如只依赖于新的动量 $P$，甚至为零。如果能做到这一点，新的运动方程将变得平凡可解。寻找这种理想变换的系统性方法导向了**哈密顿-雅可比理论** (Hamilton-Jacobi theory)。

该理论的核心是求解哈密顿-雅可比方程，这是一个关于所谓**生成函数** $S$ 的一阶偏微分方程。这个生成函数定义了从旧坐标到新坐标的正则变换。例如，对于一个在势 $V(q) = C/q^2$ 中运动的粒子，其哈密顿量为 $H(q,p) = \frac{p^2}{2m} + \frac{C}{q^2}$ [@problem_id:1247190]。我们可以尝试寻找一个正则变换，使得新的哈密顿量就是新的动量，即 $K=P$。哈密顿-雅可比方程此时变为：

$$
H\left(q, \frac{\partial S}{\partial q}\right) = P \quad \Rightarrow \quad \frac{1}{2m}\left(\frac{\partial S}{\partial q}\right)^2 + \frac{C}{q^2} = P
$$

通过求解这个方程得到生成函数 $S(q,P)$，我们就能找到新旧坐标之间的关系，例如新坐标 $Q = \partial S/\partial P$。这个过程虽然在数学上更具挑战性，但它为求解复杂的力学问题提供了一条强大的路径，并构成了经典力学与量子力学之间的重要桥梁。