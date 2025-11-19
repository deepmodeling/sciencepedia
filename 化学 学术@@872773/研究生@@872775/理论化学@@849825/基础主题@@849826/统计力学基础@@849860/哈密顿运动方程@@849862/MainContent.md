## 引言
在经典力学的宏伟殿堂中，[哈密顿力学](@entry_id:146202)不仅是牛顿力学和[拉格朗日力学](@entry_id:147054)的自然延伸，更是一次深刻的理论[升华](@entry_id:139006)。它通过引入相空间的概念，将力学系统的描述提升到了一个前所未有的对称与优雅的高度。相较于在[位形空间](@entry_id:149531)中处理[二阶微分方程](@entry_id:269365)的[拉格朗日力学](@entry_id:147054)，哈密顿形式主义以其对称的一阶[运动方程](@entry_id:170720)和强大的[代数结构](@entry_id:137052)，揭示了物理学中更为根本的联系，解决了从[经典轨道](@entry_id:177335)到量子现象的理论鸿沟问题。本文旨在系统地引导读者穿越哈密顿力学的壮丽景观。在接下来的章节中，我们将首先深入“原理与机制”，从勒让德变换到[泊松括号](@entry_id:151133)，为您构建坚实的理论基础。随后，在“应用与跨学科联系”一章中，我们将见证这些原理如何在分子动力学、混沌理论、相对论乃至[量子场论](@entry_id:138177)中大放异彩。最后，通过“动手实践”部分，您将有机会亲手应用所学知识，解决具体的物理问题。让我们从哈密顿力学的核心——它的基本原理与机制——开始我们的探索之旅。

## 原理与机制

继前一章介绍之后，我们现在深入探讨[哈密顿力学](@entry_id:146202)的核心原理与机制。本章将系统地阐述从[拉格朗日表述](@entry_id:188652)到[哈密顿表述](@entry_id:276227)的过渡，推导[哈密顿运动方程](@entry_id:176972)，并引入[泊松括号](@entry_id:151133)这一强大工具来理解动力学和守恒律。此外，我们将探讨[正则变换](@entry_id:178165)的深刻含义，并最终触及连接经典力学与量子力学的桥梁，以及处理[约束系统](@entry_id:164587)的先进技术。

### 从[拉格朗日形式](@entry_id:145697)到哈密顿形式

[拉格朗日力学](@entry_id:147054)以[广义坐标](@entry_id:156576) $q$ 和[广义速度](@entry_id:178456) $\dot{q}$ 为变量，在系统的**位形空间**中描述运动。然而，为了获得一个更对称、更深刻地揭示物理学基本结构的理论框架，我们转向哈密顿力学。[哈密顿力学](@entry_id:146202)的舞台是**相空间**，这是一个维度为 $2N$ 的空间，由 $N$ 个[广义坐标](@entry_id:156576) $q_i$ 和它们对应的 $N$ 个**[正则动量](@entry_id:155151)**（或称[共轭动量](@entry_id:172203)）$p_i$ 共同张成。

[正则动量](@entry_id:155151) $p_i$ 通过[拉格朗日量](@entry_id:174593) $L(q, \dot{q}, t)$ 定义，具体为拉格朗日量对[广义速度](@entry_id:178456)的[偏导数](@entry_id:146280)：

$$
p_i \equiv \frac{\partial L}{\partial \dot{q}_i}
$$

这个定义是至关重要的。值得注意的是，[正则动量](@entry_id:155151)不一定等同于我们通常所说的力学动量（即质量乘以速度）。一个典型的例子是[电磁场](@entry_id:265881)中运动的[带电粒子](@entry_id:160311) [@problem_id:2776245]。对于一个质量为 $m$、[电荷](@entry_id:275494)为 $e$ 的粒子，在由[标量势](@entry_id:276177) $\phi(\mathbf{r})$ 和矢量势 $\mathbf{A}(\mathbf{r})$ 描述的[电磁场](@entry_id:265881)中运动，其拉格朗日量为：

$$
L(\mathbf{r}, \dot{\mathbf{r}}) = \frac{1}{2}m\dot{\mathbf{r}}^2 + e\dot{\mathbf{r}} \cdot \mathbf{A}(\mathbf{r}) - e\phi(\mathbf{r})
$$

对应的[正则动量](@entry_id:155151) $\mathbf{p}$ 为：

$$
\mathbf{p} = \frac{\partial L}{\partial \dot{\mathbf{r}}} = m\dot{\mathbf{r}} + e\mathbf{A}(\mathbf{r})
$$

显然，这个[正则动量](@entry_id:155151) $\mathbf{p}$ 与力学动量 $m\dot{\mathbf{r}}$ 是不同的，它包含了由矢量势 $\mathbf{A}$ 贡献的一项。这种区别在哈密顿形式中具有根本性的意义。

从拉格朗日量到[哈密顿量](@entry_id:172864)的转换是通过**[勒让德变换](@entry_id:146727)** (Legendre Transformation) 完成的。[哈密顿量](@entry_id:172864) $H$ 被定义为：

$$
H(q, p, t) = \sum_{i=1}^{N} p_i \dot{q}_i - L(q, \dot{q}, t)
$$

为了使[哈密顿量](@entry_id:172864)成为坐标 $q$ 和[正则动量](@entry_id:155151) $p$ 的函数，我们必须利用 $p_i$ 的定义式来消去 $\dot{q}_i$。对于一个在保守势 $U(q)$ 中运动的简单系统，[拉格朗日量](@entry_id:174593)通常是 $L = T - U$，其中动能 $T = \frac{1}{2}m\dot{q}^2$。此时，$p = m\dot{q}$，$\dot{q} = p/m$。[哈密顿量](@entry_id:172864)变为：

$$
H = p\dot{q} - (\frac{1}{2}m\dot{q}^2 - U(q)) = p(\frac{p}{m}) - (\frac{1}{2}m(\frac{p}{m})^2 - U(q)) = \frac{p^2}{2m} + U(q)
$$

在这种简单情况下，$H = T + U$，即系统的总能量。例如，考虑一个被三维[谐振子势](@entry_id:750179) $U(x, y, z) = \frac{1}{2}k(x^2 + y^2 + z^2)$ 束缚的粒子 [@problem_id:2195246]。其动能为 $T = \frac{1}{2m}(p_x^2 + p_y^2 + p_z^2)$，因此[哈密顿量](@entry_id:172864)为：

$$
H(x, y, z, p_x, p_y, p_z) = \frac{p_x^2 + p_y^2 + p_z^2}{2m} + \frac{1}{2}k(x^2 + y^2 + z^2)
$$

对于前面提到的电[磁场中的[带电粒](@entry_id:262149)子](@entry_id:160311)，我们需要将 $\dot{\mathbf{r}} = \frac{1}{m}(\mathbf{p} - e\mathbf{A})$ 代入。我们会发现[哈密顿量](@entry_id:172864) $H = \frac{1}{2}m\dot{\mathbf{r}}^2 + e\phi$，这仍然是系统的总能量（动能加[势能](@entry_id:748988)）。将其用正则变量写出，得到：

$$
H(\mathbf{r}, \mathbf{p}) = \frac{1}{2m}(\mathbf{p} - e\mathbf{A}(\mathbf{r}))^2 + e\phi(\mathbf{r})
$$

这个形式是理论化学中描述[原子核](@entry_id:167902)在[电磁场](@entry_id:265881)中运动的基础。

### [哈密顿运动方程](@entry_id:176972)

一旦我们得到了[哈密顿量](@entry_id:172864) $H(q, p, t)$，系统的动力学就由一组[一阶微分方程](@entry_id:173139)——**哈密顿方程**——完全确定。这些方程可以通过计算[哈密顿量](@entry_id:172864)的[全微分](@entry_id:171747)并与[拉格朗日方程](@entry_id:175419)相比较来推导。结果是一组优美对称的方程：

$$
\dot{q}_i = \frac{\partial H}{\partial p_i}
$$

$$
\dot{p}_i = - \frac{\partial H}{\partial q_i}
$$

这 $2N$ 个[一阶微分方程](@entry_id:173139)描述了系统状态点在相空间中的演化轨迹。它们构成了一个一阶系统，与[拉格朗日力学](@entry_id:147054)中的 $N$ 个二阶方程形成对比。这种一阶形式在理论分析和[数值模拟](@entry_id:137087)中都具有显著优势。

让我们将这些方程应用于之前的三维谐振子模型 [@problem_id:2195246]。[哈密顿量](@entry_id:172864)为 $H = \frac{1}{2m}(p_x^2+p_y^2+p_z^2) + \frac{1}{2}k(x^2+y^2+z^2)$。六个哈密顿方程是：

$$
\dot{x} = \frac{\partial H}{\partial p_x} = \frac{p_x}{m}, \quad \dot{y} = \frac{\partial H}{\partial p_y} = \frac{p_y}{m}, \quad \dot{z} = \frac{\partial H}{\partial p_z} = \frac{p_z}{m}
$$

$$
\dot{p}_x = -\frac{\partial H}{\partial x} = -kx, \quad \dot{p}_y = -\frac{\partial H}{\partial y} = -ky, \quad \dot{p}_z = -\frac{\partial H}{\partial z} = -kz
$$

第一组方程重申了[正则动量](@entry_id:155151)与速度的关系（在此例中 $p_x = m\dot{x}$）。第二组方程 $\dot{p}_i = - \partial U / \partial q_i$ [实质](@entry_id:149406)上是牛顿第二定律 $F = \dot{p}$。

更有说服力的是，将[哈密顿方程](@entry_id:156213)应用于电[磁场中的[带电粒](@entry_id:262149)子](@entry_id:160311) [@problem_id:2776245]。使用[哈密顿量](@entry_id:172864) $H = \frac{1}{2m}(\mathbf{p} - e\mathbf{A})^2 + e\phi$，第一个方程 $\dot{\mathbf{r}} = \partial H / \partial \mathbf{p}$ 给出了 $\dot{\mathbf{r}} = \frac{1}{m}(\mathbf{p} - e\mathbf{A})$，这与[正则动量](@entry_id:155151)的定义一致。第二个方程 $\dot{\mathbf{p}} = - \partial H / \partial \mathbf{r}$ 经过一番向量分析计算后，可以证明它最终等价于[洛伦兹力定律](@entry_id:270735)：

$$
m\ddot{\mathbf{r}} = e(\mathbf{E} + \dot{\mathbf{r}} \times \mathbf{B})
$$

其中[电场](@entry_id:194326) $\mathbf{E} = -\nabla\phi$ 和[磁场](@entry_id:153296) $\mathbf{B} = \nabla \times \mathbf{A}$。这个结果有力地证明了哈密顿形式的正确性和普适性。例如，在均匀[磁场](@entry_id:153296) $\mathbf{B}=B\hat{\mathbf{z}}$ 且无[电场](@entry_id:194326)的特殊情况下，该方程可以解出粒子做圆周运动，其回旋角频率为 $\omega_c = eB/m$ [@problem_id:2776245]。

### [泊松括号](@entry_id:151133)与[可观测量](@entry_id:267133)动力学

哈密顿力学的真正威力在于它提供了一种描述任意物理量（可观测量）如何随[时间演化](@entry_id:153943)的通用语言。一个[可观测量](@entry_id:267133)是相空间变量和时间的函数 $A(q, p, t)$。它的[全时间导数](@entry_id:172646)为：

$$
\frac{dA}{dt} = \sum_{i=1}^{N} \left( \frac{\partial A}{\partial q_i}\dot{q}_i + \frac{\partial A}{\partial p_i}\dot{p}_i \right) + \frac{\partial A}{\partial t}
$$

将哈密顿方程 $\dot{q}_i = \partial H / \partial p_i$ 和 $\dot{p}_i = - \partial H / \partial q_i$ 代入上式，我们得到：

$$
\frac{dA}{dt} = \sum_{i=1}^{N} \left( \frac{\partial A}{\partial q_i}\frac{\partial H}{\partial p_i} - \frac{\partial A}{\partial p_i}\frac{\partial H}{\partial q_i} \right) + \frac{\partial A}{\partial t}
$$

这个表达式促使我们定义一个全新的运算，即**泊松括号** (Poisson Bracket) [@problem_id:2776239]。对于任意两个相空间函数 $A(q, p)$ 和 $B(q, p)$，它们的[泊松括号](@entry_id:151133)定义为：

$$
\{A, B\} \equiv \sum_{i=1}^{N} \left( \frac{\partial A}{\partial q_i}\frac{\partial B}{\partial p_i} - \frac{\partial A}{\partial p_i}\frac{\partial B}{\partial q_i} \right)
$$

利用这个定义，任意可观测量的[演化方程](@entry_id:268137)可以被优雅地写成：

$$
\frac{dA}{dt} = \{A, H\} + \frac{\partial A}{\partial t}
$$

这个方程是哈密顿力学的核心方程之一。它表明，一个可观测量的时间演化由它与系统[哈密顿量](@entry_id:172864)的泊松括号以及它的显式时间依赖性共同决定。哈密顿方程本身是这个通用规则的特例，例如 $\dot{q}_i = \{q_i, H\}$ 和 $\dot{p}_i = \{p_i, H\}$。

泊松括号具有一系列重要的代数性质，这些性质使其成为描述[经典动力学](@entry_id:177360)结构的基础 [@problem_id:2776239]：
1.  **[反对称性](@entry_id:261893)**: $\{A, B\} = -\{B, A\}$。
2.  **[双线性](@entry_id:146819)**: 对两个变量都是线性的。
3.  **雅可比恒等式**: $\{A, \{B, C\}\} + \{B, \{C, A\}\} + \{C, \{A, B\}\} = 0$。
4.  **莱布尼兹法则 (导数性质)**: $\{A, BC\} = \{A, B\}C + B\{A, C\}$。

这些性质赋予了相空间上的可观测量集合一个**泊松代数**的结构，这在更高等的理论中是至关重要的。

基本的[正则坐标](@entry_id:175654)和动量之间的泊松括号关系尤其简单和基本：

$$
\{q_i, q_j\} = 0, \quad \{p_i, p_j\} = 0, \quad \{q_i, p_j\} = \delta_{ij}
$$

其中 $\delta_{ij}$ 是克罗内克符号。这些**基本[泊松括号](@entry_id:151133)**构成了整个代数的基础。

### 对称性、守恒律与诺特定理

泊松括号为我们提供了一个直接判断物理量是否守恒的有力工具。一个不显式依赖于时间的可观测量 $A$ 是守恒的（即是一个运动常数），当且仅当它的[全时间导数](@entry_id:172646)为零。根据演化方程 $\frac{dA}{dt} = \{A, H\}$，这意味着守恒的条件是：

$$
\{A, H\} = 0
$$

换句话说，一个不显含时间的可观测量是守恒的，当且仅当它与[哈密顿量](@entry_id:172864)的泊松括号为零。

[能量守恒](@entry_id:140514)是一个直接的应用。[哈密顿量](@entry_id:172864)本身的[时间演化](@entry_id:153943)为 $\frac{dH}{dt} = \{H, H\} + \frac{\partial H}{\partial t}$。由于[泊松括号](@entry_id:151133)的[反对称性](@entry_id:261893)，$\{H, H\} = 0$。因此：

$$
\frac{dH}{dt} = \frac{\partial H}{\partial t}
$$

这个结果与从[拉格朗日形式](@entry_id:145697)推导出的 $\frac{dH}{dt} = -\frac{\partial L}{\partial t}$ [@problem_id:2195201] 完全一致。它表明，如果[哈密顿量](@entry_id:172864)（或[拉格朗日量](@entry_id:174593)）不显式依赖于时间，则[哈密顿量](@entry_id:172864) $H$（通常是总能量）是守恒的。

这个框架优雅地统一了[对称性与守恒律](@entry_id:160300)，这正是**诺特定理**在哈密顿形式下的体现 [@problem_id:2776266]。一个连续对称性可以被一个生成元函数 $G(q, p, t)$ 所描述。如果[哈密顿量](@entry_id:172864)在该对称性变换下保持不变，那么可以证明这意味着 $\{H, G\}=0$。根据可观测量[演化方程](@entry_id:268137) $\frac{dG}{dt} = \{G, H\} + \frac{\partial G}{\partial t}$，并利用 $\{G, H\} = -\{H, G\} = 0$，我们得到 $\frac{dG}{dt} = \frac{\partial G}{\partial t}$。因此，如果生成元 $G$ 本身不显式依赖于时间（即 $\frac{\partial G}{\partial t}=0$），则 $\frac{dG}{dt}=0$，$G$ 就是一个守恒量。

**结论：如果系统[哈密顿量](@entry_id:172864)在一个由不显含时间的函数 $G$ 生成的连续变换下保持不变，则 $G$ 是一个守恒量。**

[角动量守恒](@entry_id:156798)就是一个绝佳的例子。对于一个在[中心势](@entry_id:148563) $V(r)$ 中运动的粒子，$H = \frac{\mathbf{p}^2}{2m} + V(r)$。可以证明，角动量的任意分量，例如 $L_z = xp_y - yp_x$，都与[哈密顿量](@entry_id:172864)有零泊松括号，即 $\{L_z, H\} = 0$。因此，角动量是守恒的。反之，如果[势场](@entry_id:143025)不是中心对称的，例如增加一个非中心项 $V_{nc}(\mathbf{r})$ [@problem_id:1247242]，那么泊松括号 $\{L_i, H\} = \{L_i, V_{nc}\}$ 通常不为零。这个非零值恰好等于作用在粒子上的力矩的分量，即 $\frac{dL_i}{dt} = \{L_i, H\}$，这精确地再现了角动量定理。

### [正则变换](@entry_id:178165)与[辛几何](@entry_id:160783)

[哈密顿力学](@entry_id:146202)的一个核心概念是**[正则变换](@entry_id:178165)** (Canonical Transformation)。这是一种相空间的坐标变换 $(q, p) \to (Q, P)$，它保持[哈密顿运动方程](@entry_id:176972)的形式不变。也就是说，在新的[坐标系](@entry_id:156346) $(Q, P)$ 中，存在一个新的[哈密顿量](@entry_id:172864) $K(Q, P, t)$，使得[运动方程](@entry_id:170720)仍然是：

$$
\dot{Q}_i = \frac{\partial K}{\partial P_i}, \quad \dot{P}_i = - \frac{\partial K}{\partial Q_i}
$$

一个变换是正则的，当且仅当它保持基本[泊松括号](@entry_id:151133)的结构 [@problem_id:2776272]。即新坐标必须满足：

$$
\{Q_i, Q_j\}_{q,p} = 0, \quad \{P_i, P_j\}_{q,p} = 0, \quad \{Q_i, P_j\}_{q,p} = \delta_{ij}
$$

其中下标 $_{q,p}$ 表示[泊松括号](@entry_id:151133)是关于旧坐标 $(q, p)$ 计算的。

**[无穷小正则变换](@entry_id:164301) (ICT)** 提供了一个更深刻的视角。任何一个相空间函数 $G(q, p, t)$ 都可以被看作一个[无穷小正则变换](@entry_id:164301)的**生成元**。在这个变换下，任意可观测量 $F$ 的变化由[泊松括号](@entry_id:151133)给出：

$$
\delta F = \epsilon \{F, G\}
$$

其中 $\epsilon$ 是一个无穷小参数。特别地，坐标和动量的变换为 $\delta q_i = \epsilon \{q_i, G\} = \epsilon \frac{\partial G}{\partial p_i}$ 和 $\delta p_i = \epsilon \{p_i, G\} = -\epsilon \frac{\partial G}{\partial q_i}$ [@problem_id:2776272]。从这个角度看，[时间演化](@entry_id:153943)本身可以被视为一个由[哈密顿量](@entry_id:172864) $H$ 生成的连续[正则变换](@entry_id:178165)。

如果生成元 $G$ 显式依赖于时间，为了保持[哈密顿方程](@entry_id:156213)的形式，旧的[哈密顿量](@entry_id:172864) $H$ 和新的[哈密顿量](@entry_id:172864) $K$ 之间的关系会略有调整，其一阶关系为 $K = H + \epsilon \frac{\partial G}{\partial t}$ [@problem_id:2776272]。

[正则变换](@entry_id:178165)的概念可以用更现代的[微分几何](@entry_id:145818)语言来表述，这揭示了哈密顿力学的**[辛几何](@entry_id:160783)** (Symplectic Geometry) 本质 [@problem_id:2776159]。相空间并非一个普通的空间，它内在地配备了一个称为**辛[2-形式](@entry_id:188008)** (symplectic 2-form) 的几何对象 $\omega$。在[正则坐标](@entry_id:175654)下，它具有[标准形式](@entry_id:153058)：

$$
\omega = \sum_{i=1}^{n} dq_i \wedge dp_i
$$

其中 $\wedge$ 是[外代数](@entry_id:201164)中的[楔积](@entry_id:147029)。这个[2-形式](@entry_id:188008)是反对称的，并且是非退化的。哈密顿方程可以被内蕴地写成 $i_{X_H}\omega = dH$，其中 $X_H$ 是[哈密顿向量场](@entry_id:270696)，dH是[哈密顿量](@entry_id:172864)的外微分。

从这个几何观点看，[正则变换](@entry_id:178165)（现在更精确地称为**辛[同胚](@entry_id:146933)**，symplectomorphism）是一个映射 $\phi: (q,p) \mapsto (Q,P)$，它保持辛形式不变。用**[拉回](@entry_id:160816)** (pullback) 运算 $\phi^*$ 来表示，这个条件就是：

$$
\phi^*\omega = \omega
$$

这个定义比基于泊松括号的定义更为基本和几何化，它表明[哈密顿动力学](@entry_id:156273)的本质是保持相空间的辛结构。

### 高等主题与应用

#### 通往量子力学之路

[哈密顿力学](@entry_id:146202)，特别是[泊松括号](@entry_id:151133)的[代数结构](@entry_id:137052)，为通向量子力学提供了最直接的路径。P.A.M. Dirac 在量子力学的发展中注意到，经典力学中的泊松括号和[量子力学中的算符](@entry_id:262952)对易子之间存在惊人的相似性 [@problem_id:2776274]。这导致了**[正则量子化](@entry_id:148501)**的基本思想：将经典[可观测量](@entry_id:267133)提升为希尔伯特空间中的算符，并用对易子来替换泊松括号，其对应关系为：

$$
\{A, B\} \longleftrightarrow \frac{1}{i\hbar} [\hat{A}, \hat{B}]
$$

其中 $[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A}$ 是[量子对易子](@entry_id:194337)，$\hbar$ 是[约化普朗克常数](@entry_id:275910)。经典[演化方程](@entry_id:268137) $\frac{dA}{dt} = \{A, H\}$ 直接对应于量子力学中的海森堡方程 $\frac{d\hat{A}}{dt} = \frac{1}{i\hbar}[\hat{A}, \hat{H}]$。

这种对应关系并非在所有情况下都精确成立。著名的 **Groenewold–van Hove 定理**表明，不存在一个能将所有经典多项式可观测量及其泊松[代数结构](@entry_id:137052)完美映射到[量子算符](@entry_id:137703)及其对易子代数的量子化方案 [@problem_id:2776274, B选项]。

然而，在**半经典极限** ($\hbar \to 0$) 下，这种对应关系是成立的。更精确的联系由**维格纳-外尔 (Wigner-Weyl) 相空间表述**给出。在此框架下，[量子对易子](@entry_id:194337)对应于**莫亚尔括号 (Moyal bracket)**，它在 $\hbar$ 的[幂级数展开](@entry_id:273325)中，其领头项恰好是[泊松括号](@entry_id:151133) [@problem_id:2776274, A选项]。

$$
\{A, H\}_{MB} = \{A, H\}_{PB} + \mathcal{O}(\hbar^2)
$$

一个重要的例外是，当[哈密顿量](@entry_id:172864)至多是[正则坐标](@entry_id:175654)和动量的二次多项式时（例如谐振子，或在[均匀电磁场](@entry_id:263197)中的粒子），莫亚尔括号与泊松括号完全相等。在这种情况下，量子海森堡方程与经典[哈密顿方程](@entry_id:156213)的形式完全一致 [@problem_id:2776274, D选项]。对于一般的[非谐势](@entry_id:141227)，不同算符排序方案的选择会影响 $\mathcal{O}(\hbar^2)$ 的修正项，从而影响定量的[半经典动力学](@entry_id:140913)计算结果 [@problem_id:2776274, E选项]。

#### [约束哈密顿系统](@entry_id:169165)

在[分子模拟](@entry_id:182701)等实际应用中，系统常常受到约束，例如[化学键](@entry_id:138216)长度固定（刚性键）或分子被视为刚体。这些约束在哈密顿形式中需要特殊处理。Dirac 发展了一套处理[约束系统](@entry_id:164587)的完整理论。

约束被分为**[第一类约束](@entry_id:168143)**和**[第二类约束](@entry_id:175584)**。对于具有[第二类约束](@entry_id:175584) $\phi_a(q,p)=0$ 的系统，其特征是约束的泊松括号矩阵 $C_{ab} \equiv \{\phi_a, \phi_b\}$ 是可逆的 [@problem_id:2776282]。在这种情况下，标准的泊松括号不再适用，必须被**[狄拉克括号](@entry_id:178441) (Dirac Bracket)**所取代：

$$
\{A, B\}_D \equiv \{A, B\} - \sum_{a,b} \{A, \phi_a\} (C^{-1})_{ab} \{\phi_b, B\}
$$

[狄拉克括号](@entry_id:178441)的关键性质是，任何[可观测量](@entry_id:267133)与约束的[狄拉克括号](@entry_id:178441)都恒为零，即 $\{F, \phi_a\}_D = 0$。这使得我们可以在理论中将约束作为强等式（而非仅在运动轨迹上成立的弱等式）来使用，从而无需引入拉格朗日乘子。系统的动力学演化由新的括号给出：

$$
\frac{dA}{dt} = \{A, H\}_D
$$

这个方法对于正确地处理如[刚性转子](@entry_id:156317)等约束分子系统的[经典动力学](@entry_id:177360)至关重要，并且也是对这类系统进行量子化的正确起点 [@problem_id:2776274, F选项]。