## 引言
在探索弯曲空间的几何学时，曲率无疑是核心概念。传统上，我们通过繁复的[黎曼张量分量](@entry_id:188469)来描述它，但这种方法往往掩盖了其更深层次的结构。本文旨在填补这一认知空白，介绍一种由 [Élie Cartan](@entry_id:263871) 开创的更为优雅和强大的语言——微分形式——来理解曲率。这种方法不仅极大地简化了计算，更揭示了[曲率与拓扑](@entry_id:264903)学及现代物理学之间惊人而深刻的联系。在接下来的篇章中，我们将首先在“原理与机制”中深入探讨[联络形式](@entry_id:263247)、曲率形式以及[嘉当结构方程](@entry_id:162100)的基本理论。随后，我们将在“应用与跨学科联系”中展示这些工具在解决具体几何问题、连接局部与全局拓扑以及在广义相对论和[规范场](@entry_id:159627)论中的强大威力。最后，通过一系列精心设计的“动手实践”问题，你将有机会亲自运用这些知识，巩固并深化理解。

## 原理与机制

在[微分几何](@entry_id:145818)中，曲率是对几何对象偏离平坦（欧几里得）空间程度的度量。虽然可以通过黎曼曲率张量 $R^i_{jkl}$ 及其复杂的索引来研究曲率，但一种更深刻、更优雅的表述是由伟大的几何学家 [Élie Cartan](@entry_id:263871) 提出的，它使用了微分形式的语言。这种方法不仅简化了计算，而且揭示了[曲率与拓扑](@entry_id:264903)学和现代物理学（如[规范场](@entry_id:159627)论）之间深刻的内在联系。本章将系统地阐述[联络形式](@entry_id:263247)和曲率形式的原理，并通过 Cartan 的[结构方程](@entry_id:274644)来揭示其机制。

### 联络与挠率：第一[结构方程](@entry_id:274644)

为了在[流形](@entry_id:153038)上[微分](@entry_id:158718)矢量场，我们需要引入**联络**（connection）的概念。联络可以被看作是在[流形](@entry_id:153038)的不同点之间“连接”切空间的一种方式。在[活动标架](@entry_id:175562)（moving frame）的语言中，这一概念被优美地封装在**[联络1-形式](@entry_id:275839)**（connection 1-form）中。

考虑一个 $n$ 维[流形](@entry_id:153038)，在每一点的[切空间](@entry_id:199137)上，我们可以选取一组[基矢](@entry_id:199546) $\{e_i\}$。其对偶基底构成一组[1-形式](@entry_id:270392) $\{\theta^i\}$，称为**[余标架](@entry_id:637284)**（coframe）。这些[1-形式](@entry_id:270392)构成了该点[余切空间](@entry_id:270516)的基底。联络可以表示为一个矩阵值的[1-形式](@entry_id:270392) $\boldsymbol{\omega}$，其[矩阵元](@entry_id:186505)为 $\omega^i_j$。这些 $\omega^i_j$ 描述了[基矢](@entry_id:199546) $e_j$ 沿着某个方向移动时的无穷小变化如何分解到[基矢](@entry_id:199546) $e_i$ 上。

[联络1-形式](@entry_id:275839)与[余标架](@entry_id:637284)之间存在一个基本关系，即 **Cartan 第一[结构方程](@entry_id:274644)**：

$$
T^i = d\theta^i + \omega^i_j \wedge \theta^j
$$

在这里，$d$ 是[外微分](@entry_id:161900)算符，$\wedge$ 是外积（[楔积](@entry_id:147029)），并采用了爱因斯坦求和约定（对重复的上下指标 $j$ 求和）。$T^i$ 是一个[2-形式](@entry_id:188008)，称为**挠率2-形式**（torsion 2-form）。它度量了当你沿着两个不同方向的无穷小平行四边形移动时，[基矢](@entry_id:199546)所经历的旋转是否闭合。如果 $T^i = 0$ 对所有 $i$ 成立，我们称该联络是**无挠**的（torsion-free）。[黎曼几何](@entry_id:160508)中研究的**[列维-奇维塔联络](@entry_id:161107)**（Levi-Civita connection）就是一个重要的[无挠联络](@entry_id:181337)。

在[局部坐标系](@entry_id:751394) $\{x^i\}$ 中，最自然的[余标架](@entry_id:637284)是[坐标基](@entry_id:270149)[1-形式](@entry_id:270392) $dx^i$。在这种情况下，[联络1-形式](@entry_id:275839) $\omega^i_j$ 可以用**[克里斯托费尔符号](@entry_id:159831)**（Christoffel symbols） $\Gamma^i_{jk}$ 表示：

$$
\omega^i_j = \Gamma^i_{jk} dx^k
$$

将此代入第一[结构方程](@entry_id:274644)，并注意到[坐标基](@entry_id:270149)1-形式的外微分为零（$d(dx^i) = 0$），我们得到挠率的表达式：

$$
T^i = \omega^i_j \wedge dx^j = (\Gamma^i_{jk} dx^k) \wedge dx^j = \Gamma^i_{jk} dx^k \wedge dx^j
$$

我们可以将挠率2-形式展开为 $T^i = \frac{1}{2} T^i_{jk} dx^j \wedge dx^k$，其中 $T^i_{jk}$ 是[挠率张量](@entry_id:204137)的分量。通过反对称化上式右侧，我们得到 $T^i = \frac{1}{2} (\Gamma^i_{kj} - \Gamma^i_{jk}) dx^k \wedge dx^j$。比较系数可知：

$$
T^i_{jk} = \Gamma^i_{jk} - \Gamma^i_{kj}
$$

这个结果揭示了一个深刻的联系：联络是[无挠的](@entry_id:161664)（$T^i_{jk}=0$），当且仅当[克里斯托费尔符号](@entry_id:159831)的下指标是对称的（$\Gamma^i_{jk} = \Gamma^i_{kj}$）。因此，如果在一个[坐标系](@entry_id:156346)下发现克里斯托费尔符号的下指标不对称，那么这个联络必然具有非零的挠率 [@problem_id:1502850]。

### 曲率形式：第二[结构方程](@entry_id:274644)

联络描述了矢量场如何变化，而曲率则描述了联络本身如何“卷曲”。换言之，曲率是“变化的速率的变化率”。它量化了沿无穷小闭环[平行输运](@entry_id:160671)一个向量时，该向量与初始状态的差异。这个概念被 **Cartan 第二[结构方程](@entry_id:274644)** 精确地捕捉：

$$
\boldsymbol{\Omega} = d\boldsymbol{\omega} + \boldsymbol{\omega} \wedge \boldsymbol{\omega}
$$

这里，$\boldsymbol{\Omega}$ 是一个矩阵值的[2-形式](@entry_id:188008)，称为**[曲率2-形式](@entry_id:187677)**（curvature 2-form），其矩阵元为 $\Omega^i_j$。方程右边的第一项 $d\boldsymbol{\omega}$ 是我们可能从阿贝尔（交换）理论中预期的项。第二项 $\boldsymbol{\omega} \wedge \boldsymbol{\omega}$ 是一个矩阵乘积与[外积](@entry_id:147029)的结合，其存在是因为联络的矩阵值通常是不可交换的。正是这个“非阿贝尔”项，赋予了现代规范场论丰富的结构。

与挠率一样，[曲率2-形式](@entry_id:187677)的分量 $\Omega^i_j$ 与我们更熟悉的**黎曼曲率张量** $R^i_{jkl}$ 直接相关。在[余标架](@entry_id:637284) $\{\theta^i\}$ 中，它们的关系是：

$$
\Omega^i_j = \frac{1}{2} R^i_{jkl} \theta^k \wedge \theta^l
$$

这个方程是一个关键的“词典”，它在分量语言和[形式语言](@entry_id:265110)之间建立了转换。张量的所有对称性和反对称性都被巧妙地编码在2-形式 $\Omega^i_j$ 的[代数结构](@entry_id:137052)中。

### 计算曲率：一个范例

为了具体理解这些抽象的方程，让我们在一个经典的例子——半径为 $R$ 的[二维球面](@entry_id:269890) $S^2$ 上计算曲率形式。

球面的度规（[线元](@entry_id:196833)）在[球坐标](@entry_id:146054) $(\theta, \phi)$ 下为 $ds^2 = R^2 d\theta^2 + R^2 \sin^2\theta d\phi^2$。为了简化计算，我们引入一个局部**正交[余标架](@entry_id:637284)**（orthonormal coframe）：

$$
\theta^1 = R \, d\theta, \quad \theta^2 = R \sin\theta \, d\phi
$$

在这个基底下，度规简化为 $ds^2 = (\theta^1)^2 + (\theta^2)^2$。我们的目标是求出列维-奇维塔联络对应的曲率形式矩阵 $\boldsymbol{\Omega}$。

**第一步：利用第一[结构方程](@entry_id:274644)求[联络形式](@entry_id:263247) $\omega^i_j$**

[列维-奇维塔联络](@entry_id:161107)是[无挠的](@entry_id:161664) ($T^i=0$) 并且是度规相容的。无挠条件意味着第一[结构方程](@entry_id:274644)变为 $d\theta^i + \omega^i_j \wedge \theta^j = 0$。度规相容性在一个正交标架中意味着[联络形式](@entry_id:263247)矩阵是反对称的，即 $\omega_{ij} = -\omega_{ji}$。对于二维情况，这意味着 $\omega^1_1 = \omega^2_2 = 0$ 并且 $\omega^2_1 = -\omega^1_2$。

我们首先计算[余标架](@entry_id:637284)的外微分：
$d\theta^1 = d(R \, d\theta) = 0$
$d\theta^2 = d(R \sin\theta \, d\phi) = R \cos\theta \, d\theta \wedge d\phi$

为了用[余标架](@entry_id:637284)基底表示 $d\theta^2$，我们将 $d\theta$ 和 $d\phi$ 替换为 $\frac{\theta^1}{R}$ 和 $\frac{\theta^2}{R\sin\theta}$：
$d\theta^2 = R \cos\theta \left(\frac{\theta^1}{R}\right) \wedge \left(\frac{\theta^2}{R\sin\theta}\right) = \frac{\cot\theta}{R} \theta^1 \wedge \theta^2$

现在应用无挠条件：
对于 $i=1$： $d\theta^1 + \omega^1_2 \wedge \theta^2 = 0 \implies 0 + \omega^1_2 \wedge \theta^2 = 0$。
对于 $i=2$： $d\theta^2 + \omega^2_1 \wedge \theta^1 = 0 \implies \frac{\cot\theta}{R} \theta^1 \wedge \theta^2 - \omega^1_2 \wedge \theta^1 = 0$。

从第一个方程，我们可以看出 $\omega^1_2$ 必须是 $\theta^2$ 的某个倍数，设 $\omega^1_2 = f \theta^2$。代入第二个方程得到 $\frac{\cot\theta}{R} \theta^1 \wedge \theta^2 + f \theta^1 \wedge \theta^2 = 0$，这给出 $f = -\frac{\cot\theta}{R}$。因此，唯一的非零[联络形式](@entry_id:263247)分量是：

$$
\omega^1_2 = -\frac{\cot\theta}{R} \theta^2 \quad \text{和} \quad \omega^2_1 = - \omega^1_2 = \frac{\cot\theta}{R} \theta^2
$$

**第二步：利用第二[结构方程](@entry_id:274644)求曲率形式 $\Omega^i_j$**

现在我们应用第二[结构方程](@entry_id:274644) $\Omega^i_j = d\omega^i_j + \omega^i_k \wedge \omega^k_j$。
由于 $\omega^1_1 = \omega^2_2 = 0$，矩阵乘积项 $\boldsymbol{\omega} \wedge \boldsymbol{\omega}$ 为零。例如，$\Omega^1_2$ 的这一项是 $\omega^1_1 \wedge \omega^1_2 + \omega^1_2 \wedge \omega^2_2 = 0$。因此，曲率形式简化为 $\Omega^i_j = d\omega^i_j$。

我们来计算 $\Omega^1_2 = d\omega^1_2$：
$$
\Omega^1_2 = d\left(-\frac{\cot\theta}{R} \theta^2\right) = d\left(-\frac{\cot\theta}{R}\right) \wedge \theta^2 + \left(-\frac{\cot\theta}{R}\right) d\theta^2
$$
计算各项：
$d\left(-\frac{\cot\theta}{R}\right) = \frac{1}{R \sin^2\theta} d\theta = \frac{1}{R^2 \sin^2\theta} \theta^1$
代入之前求得的 $d\theta^2 = \frac{\cot\theta}{R} \theta^1 \wedge \theta^2$，我们得到：
$$
\Omega^1_2 = \left(\frac{1}{R^2 \sin^2\theta} \theta^1\right) \wedge \theta^2 - \frac{\cot\theta}{R} \left(\frac{\cot\theta}{R} \theta^1 \wedge \theta^2\right)
$$
$$
\Omega^1_2 = \left(\frac{1}{R^2 \sin^2\theta} - \frac{\cos^2\theta}{R^2 \sin^2\theta}\right) \theta^1 \wedge \theta^2 = \frac{1 - \cos^2\theta}{R^2 \sin^2\theta} \theta^1 \wedge \theta^2 = \frac{1}{R^2} \theta^1 \wedge \theta^2
$$

利用反对称性 $\Omega^2_1 = -\Omega^1_2$ 和 $\Omega^1_1 = \Omega^2_2 = 0$，我们最终得到曲率矩阵 [@problem_id:1502873]：

$$
\boldsymbol{\Omega} = \begin{pmatrix} 0  \frac{1}{R^2} \theta^1 \wedge \theta^2 \\ -\frac{1}{R^2} \theta^1 \wedge \theta^2  0 \end{pmatrix}
$$

这个结果非常优雅。它告诉我们，曲率形式 $\Omega^1_2$ 与面积元 $\theta^1 \wedge \theta^2$ 成正比，比例系数恰好是球面的高斯曲率 $K = 1/R^2$。这清晰地展示了曲率形式如何封装了[流形](@entry_id:153038)的内蕴几何信息。

### 曲率形式的性质与对称性

曲率形式不仅仅是一个计算工具，它还满足深刻的代数和[微分](@entry_id:158718)恒等式，这些恒等式反映了底层几何的结构。

#### [反对称性](@entry_id:261893)与[李代数](@entry_id:137954)
对于与度规相容的联络（如[列维-奇维塔联络](@entry_id:161107)），在一个正交标架中，[联络形式](@entry_id:263247)矩阵 $\boldsymbol{\omega}$ 是反对称的，即 $\omega_{ij} = g_{ik}\omega^k_j = -\omega_{ji}$。这意味着 $\boldsymbol{\omega}$ 的值取自于**[特殊正交群](@entry_id:146418)** $SO(n)$ 的**[李代数](@entry_id:137954)** $\mathfrak{so}(n)$，即反对称矩阵的集合。可以证明，这进一步导致曲率形式矩阵 $\boldsymbol{\Omega}$ 也取值于 $\mathfrak{so}(n)$，即 $\Omega_{ij} = -\Omega_{ji}$。这一性质在之后的讨论中至关重要。

#### [比安基恒等式](@entry_id:261685) (Bianchi Identities)

[曲率张量](@entry_id:181383)满足两个重要的恒等式，称为[比安基恒等式](@entry_id:261685)。在[形式语言](@entry_id:265110)中，它们变得异常简洁。

**[第一比安基恒等式](@entry_id:200081)**：对于[无挠联络](@entry_id:181337)，[黎曼张量分量](@entry_id:188469)满足 $R^i_{jkl} + R^i_{klj} + R^i_{ljk} = 0$。这个看似复杂的索引游戏，在形式语言中可以被证明等价于一个极其简单的表达式 [@problem_id:1502856]：

$$
\Omega^i_j \wedge \theta^j = 0
$$

这个方程通过将[曲率2-形式](@entry_id:187677)与[余标架](@entry_id:637284)[1-形式](@entry_id:270392)进行[楔积](@entry_id:147029)来实现，优雅地编码了张量的[循环对称性](@entry_id:193404)。

**[第二比安基恒等式](@entry_id:199705)**：这个恒等式是 Cartan [结构方程](@entry_id:274644)的一个直接推论。对第二[结构方程](@entry_id:274644) $\boldsymbol{\Omega} = d\boldsymbol{\omega} + \boldsymbol{\omega} \wedge \boldsymbol{\omega}$ 两边取[外微分](@entry_id:161900) $d$：

$$
d\boldsymbol{\Omega} = d(d\boldsymbol{\omega}) + d(\boldsymbol{\omega} \wedge \boldsymbol{\omega}) = 0 + d\boldsymbol{\omega} \wedge \boldsymbol{\omega} - \boldsymbol{\omega} \wedge d\boldsymbol{\omega}
$$

利用 $\boldsymbol{\Omega} = d\boldsymbol{\omega} + \boldsymbol{\omega} \wedge \boldsymbol{\omega}$ 可得 $d\boldsymbol{\omega} = \boldsymbol{\Omega} - \boldsymbol{\omega} \wedge \boldsymbol{\omega}$，代入上式：
$$
d\boldsymbol{\Omega} = (\boldsymbol{\Omega} - \boldsymbol{\omega} \wedge \boldsymbol{\omega}) \wedge \boldsymbol{\omega} - \boldsymbol{\omega} \wedge (\boldsymbol{\Omega} - \boldsymbol{\omega} \wedge \boldsymbol{\omega}) = \boldsymbol{\Omega} \wedge \boldsymbol{\omega} - \boldsymbol{\omega} \wedge \boldsymbol{\Omega}
$$
整理后得到：
$$
d\boldsymbol{\Omega} - (\boldsymbol{\omega} \wedge \boldsymbol{\Omega} - \boldsymbol{\Omega} \wedge \boldsymbol{\omega}) = 0 \quad \text{或} \quad d\boldsymbol{\Omega} + [\boldsymbol{\omega}, \boldsymbol{\Omega}] = 0
$$
其中 $[\boldsymbol{\omega}, \boldsymbol{\Omega}]$ 是矩阵的李括号。我们常定义**外共变导数** $D\boldsymbol{\Omega} = d\boldsymbol{\Omega} + [\boldsymbol{\omega}, \boldsymbol{\Omega}]$，于是[第二比安基恒等式](@entry_id:199705)可以简洁地写为 $D\boldsymbol{\Omega} = 0$。这个恒等式在[规范场](@entry_id:159627)论中至关重要，它意味着场强的“散度”为零，对应于源不存在时的麦克斯韦方程组。

### 曲率的几何与物理诠释

曲率形式的威力在于它能连接抽象的几何概念与具体的物理现象。

#### [和乐群](@entry_id:191471)与曲率
曲率的几何意义在于它生成了**和乐群**（holonomy group）。将在[流形](@entry_id:153038)上的一条闭合路径[平行输运](@entry_id:160671)一个切向量，该向量最终会相对于其初始状态发生一个旋转（或洛伦兹变换）。所有可能的闭环路径引起的这种变换构成一个[李群](@entry_id:137659)，即[和乐群](@entry_id:191471)。**Ambrose-Singer 定理**表明，和乐群的李代数恰好由所有**[曲率算子](@entry_id:198006)** $\Omega(X,Y)$ 在该点张成的代数生成，其中 $X, Y$ 是[切向量](@entry_id:265494)。换句话说，曲率告诉我们“在无穷小尺度上有哪些旋转是可能的”。

例如，考虑一个由[曲率2-形式](@entry_id:187677) $\Omega$ 在某点 $p$ 作用于不同[切向量](@entry_id:265494)对 $(\partial_1, \partial_2)$ 和 $(\partial_1, \partial_3)$ 所产生的两个矩阵 $A = \Omega(\partial_1, \partial_2)$ 和 $B = \Omega(\partial_1, \partial_3)$。这些矩阵本身是[和乐群](@entry_id:191471)[李代数](@entry_id:137954)的元素。它们的李括号 $[A, B] = AB - BA$ 同样也是李代数的元素，反映了[和乐群](@entry_id:191471)的非交换结构 [@problem_id:1502881]。

#### [积流形](@entry_id:270208)上的曲率
如果一个[流形](@entry_id:153038)是两个[子流形](@entry_id:159439) $M_1$ 和 $M_2$ 的**[积流形](@entry_id:270208)** $M = M_1 \times M_2$，并且其度规是两个子流形度规之和 $g = g_1 + g_2$，那么其列维-奇维塔联络和曲率也会相应地分解。[联络形式](@entry_id:263247)矩阵 $\boldsymbol{\omega}$ 和曲率形式矩阵 $\boldsymbol{\Omega}$ 都会呈现[块对角结构](@entry_id:746869)：

$$
\boldsymbol{\omega} = \begin{pmatrix} \boldsymbol{\omega}_1  0 \\ 0  \boldsymbol{\omega}_2 \end{pmatrix}, \quad \boldsymbol{\Omega} = \begin{pmatrix} \boldsymbol{\Omega}_1  0 \\ 0  \boldsymbol{\Omega}_2 \end{pmatrix}
$$

这意味着曲率不会“混合”来自不同[子流形](@entry_id:159439)的维度。一个仅在 $M_1$ 内部的平行输运闭环不会产生任何在 $M_2$ 方向上的旋转，反之亦然。这就是为什么在研究 $S^2 \times H^2$ 这样的[积流形](@entry_id:270208)时，混合了两个子流形坐标的曲率张量分量，如 $R^1_{234}$，必然为零的原因 [@problem_id:1502855]。

#### [规范场](@entry_id:159627)论中的曲率
曲率形式的框架可以从黎曼几何（其对称群为 $SO(n)$）自然地推广到处理更一般[李群](@entry_id:137659) $G$ 的**[主丛](@entry_id:160029)**（principal bundle）理论。这正是现代物理学中**非阿贝尔规范场论**的数学基础。

在这种推广中：
- **[联络1-形式](@entry_id:275839)** $\boldsymbol{\omega}$ 被称为**[规范势](@entry_id:188985)**（gauge potential），它是一个取值于李代数 $\mathfrak{g}$ 的[1-形式](@entry_id:270392)。
- **[曲率2-形式](@entry_id:187677)** $\boldsymbol{\Omega} = d\boldsymbol{\omega} + \boldsymbol{\omega} \wedge \boldsymbol{\omega}$ 被称为**场强**（field strength）。

一个**[规范变换](@entry_id:176521)**由一个时空到李群 $G$ 的映射 $g(x)$ 给出。在此变换下，[规范势](@entry_id:188985)的变换法则是：

$$
\boldsymbol{\omega}' = g^{-1}\boldsymbol{\omega} g + g^{-1}dg
$$

这是一个非齐次的变换。然而，场强（曲率）的变换法则却非常简洁。通过直接计算可以证明 [@problem_id:1502876]：

$$
\boldsymbol{\Omega}' = d\boldsymbol{\omega}' + \boldsymbol{\omega}' \wedge \boldsymbol{\omega}' = g^{-1}(d\boldsymbol{\omega} + \boldsymbol{\omega} \wedge \boldsymbol{\omega})g = g^{-1}\boldsymbol{\Omega} g
$$

这个结果至关重要：场强（曲率）在规范变换下不是不变的，而是**共变**（covariantly）的。这意味着物理定律若要规范不变，就必须以一种能适应这种变换的方式来构造。

### 从曲率形式到[不变量](@entry_id:148850)

尽管曲率本身依赖于标架或规范的选择，但我们可以从中构造出不依赖于这些选择的**[不变量](@entry_id:148850)**。这些[不变量](@entry_id:148850)既可以是局部的张量，也可以是全局的拓扑示性数。

#### [张量不变量](@entry_id:203254)：里奇张量
黎曼曲率张量 $R^i_{jkl}$ 的不同收缩会产生更简单的张量，它们在物理学（如广义相对论）中有重要应用。例如，**里奇张量**（Ricci tensor）定义为 $R_{ik} = R^j_{ijk}$。利用 $\Omega^i_j = \frac{1}{2} R^i_{jkl} \theta^k \wedge \theta^l$ 这个关系，我们可以从曲率形式中提取黎曼张量的分量，然后进行收缩得到[里奇张量](@entry_id:159336)的分量 [@problem_id:1502870]。这提供了一个从形式到分量并计算[物理可观测量](@entry_id:154692)（如爱因斯坦张量）的系统途径。

#### [拓扑不变量](@entry_id:138526)：[示性类](@entry_id:160596)
曲率形式最深刻的应用之一是构造[拓扑不变量](@entry_id:138526)。虽然 $\boldsymbol{\Omega}$ 本身在[规范变换](@entry_id:176521)下不是不变的，但某些由 $\boldsymbol{\Omega}$ 构造的多项式却是。利用迹 `tr` 的循环性质 $\text{tr}(ABC) = \text{tr}(BCA)$，我们可以看到：

$$
\text{tr}(\boldsymbol{\Omega}' \wedge \boldsymbol{\Omega}') = \text{tr}((g^{-1}\boldsymbol{\Omega} g) \wedge (g^{-1}\boldsymbol{\Omega} g)) = \text{tr}(g^{-1}(\boldsymbol{\Omega} \wedge \boldsymbol{\Omega})g) = \text{tr}(\boldsymbol{\Omega} \wedge \boldsymbol{\Omega})
$$

因此，像 $\text{tr}(\boldsymbol{\Omega} \wedge \boldsymbol{\Omega})$ 这样的4-形式是规范不变的。**陈-韦伊理论**（Chern-Weil theory）的一个核心结果是，这类形式不仅是规范不变的，而且还是**闭**的（closed），即它们的外微分为零。例如：

$$
d(\text{tr}(\boldsymbol{\Omega} \wedge \boldsymbol{\Omega})) = 0
$$

这个被称为**第一庞特里亚金形式**（first Pontryagin form）的4-形式是[闭形式](@entry_id:272960)。根据[德拉姆理论](@entry_id:160579)，闭形式定义了一个上同调类，这个[上同调类](@entry_id:263961)是一个**[拓扑不变量](@entry_id:138526)**，它只依赖于底[层流](@entry_id:149458)形或向量丛的全局拓扑结构，而不依赖于所选取的具体联络或度规。这些[不变量](@entry_id:148850)被称为**示性类**（characteristic classes）。

一个闭形式在局部总是**恰当**的（exact），即它可以写成另一个低阶形式的外微分。例如，$\text{tr}(\boldsymbol{\Omega} \wedge \boldsymbol{\Omega}) = dC_3$，其中 $C_3$ 是一个3-形式，被称为**陈-西蒙斯形式**（Chern-Simons form）。可以证明，为了满足这个关系，陈-西蒙斯形式必须具有 $C_3 = \text{tr}(\boldsymbol{\omega} \wedge d\boldsymbol{\omega}) + \frac{2}{3} \text{tr}(\boldsymbol{\omega} \wedge \boldsymbol{\omega} \wedge \boldsymbol{\omega})$ 的形式 [@problem_id:1502849]。

与此形成对比的是，对于一个与度规相容的联络，其曲率形式矩阵 $\boldsymbol{\Omega}$ 在正交标架中是反对称的。[反对称矩阵](@entry_id:155998)的迹为零。因此，$\text{tr}(\boldsymbol{\Omega})$ 这个[2-形式](@entry_id:188008)恒等于零 [@problem_id:1502852]。这再次凸显了像 $\text{tr}(\boldsymbol{\Omega} \wedge \boldsymbol{\Omega})$ 这样的高次迹在构造[不变量](@entry_id:148850)中的特殊地位。它们能够探测到曲率的非交换结构，并将其转化为深刻的全局拓扑信息。