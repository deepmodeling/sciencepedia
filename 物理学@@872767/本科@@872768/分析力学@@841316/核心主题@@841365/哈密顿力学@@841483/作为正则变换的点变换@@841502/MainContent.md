## 引言
在哈密顿力学的宏伟框架中，[正则变换](@entry_id:178165)扮演着核心角色，它允许我们在保持物理定律形式不变的前提下，灵活地选择最适宜的[坐标系](@entry_id:156346)来描述系统。然而，广义的[正则变换](@entry_id:178165)可能显得抽象，它们混合了坐标与动量，有时难以直观把握。本文聚焦于一类特别直观且功能强大的[正则变换](@entry_id:178165)——**[点变换](@entry_id:171852)**。

[点变换](@entry_id:171852)的本质是对系统[位形空间](@entry_id:149531)的重新参数化，例如从[笛卡尔坐标](@entry_id:167698)切换到极坐标。但其核心挑战在于：仅仅改变坐标是不够的，我们必须以一种精确的方式构造出新的[共轭动量](@entry_id:172203)，才能确保整个相空间变换是“正则”的，从而保持[哈密顿方程](@entry_id:156213)的优美结构。本文旨在填补从直观的坐标更换到严格的[正则变换](@entry_id:178165)之间的理论与实践鸿沟。

在接下来的内容中，我们将系统地探索[点变换](@entry_id:171852)的世界。第一章“**原理与机制**”将深入探讨[点变换](@entry_id:171852)的定义，并介绍两种核心的构造方法：利用泊松括号的不变性和使用生成函数。第二章“**应用与[交叉](@entry_id:147634)学科联系**”将通过丰富的实例展示[点变换](@entry_id:171852)如何作为一种强大的工具，用于简化[哈密顿量](@entry_id:172864)、解耦[多体系统](@entry_id:144006)，甚至揭示不同物理问题间的深刻联系。最后，第三章“**动手实践**”提供了一系列练习，帮助您将理论知识转化为解决问题的实际技能。

让我们首先从[点变换](@entry_id:171852)最基本的原理和机制开始。

## 原理与机制

在哈密顿力学中，[正则变换](@entry_id:178165)是一类特殊的相空间坐标变换，它保持[哈密顿方程](@entry_id:156213)的形式不变。在这类变换中，有一族特别重要且直观的变换，称为**[点变换](@entry_id:171852)** (point transformations)。与广义[正则变换](@entry_id:178165)不同，[点变换](@entry_id:171852)仅仅重新描述了系统的位形空间，而不涉及动量。本章将深入探讨[点变换](@entry_id:171852)的原理、构造方法及其深刻的物理内涵。

### [点变换](@entry_id:171852)的定义

一个**[点变换](@entry_id:171852)**是一种[坐标变换](@entry_id:172727)，其中新的[广义坐标](@entry_id:156576) $Q_i$ 仅是旧的[广义坐标](@entry_id:156576) $q_j$ 和时间 $t$ 的函数。其数学形式为：
$$ Q_i = Q_i(q_1, q_2, \dots, q_n, t) $$
如果变换不显含时间，则称为定常[点变换](@entry_id:171852)，$Q_i = Q_i(q_1, q_2, \dots, q_n)$。

这种变换的直观意义在于，它仅仅是对系统位形空间的一种重新标记或参数化。例如，描述一个平面内运动的[质点](@entry_id:186768)，我们可以用笛卡尔坐标 $(x, y)$，也可以用极坐标 $(r, \theta)$。从 $(x, y)$ 到 $(r, \theta)$ 的变换就是一个典型的[点变换](@entry_id:171852)，因为新的坐标仅依赖于旧的坐标。[点变换](@entry_id:171852)的挑战与核心在于：为了使整个相空间变换 $(q, p) \to (Q, P)$ 是正则的，新的[广义动量](@entry_id:165699) $P_i$ 必须以一种精确的方式依赖于旧的坐标 $(q_j, p_j)$。

### [点变换](@entry_id:171852)的[正则性条件](@entry_id:166962)

要确定与给定[点变换](@entry_id:171852) $Q_i(q_j)$ 相配的新动量 $P_i$，从而构成一个完整的[正则变换](@entry_id:178165)，我们有两种主要的方法：利用泊松括号的不变性，或通过构造[生成函数](@entry_id:146702)。

#### 泊松括号[不变性](@entry_id:140168)

[正则变换](@entry_id:178165)的一个根本性质是它保持基本泊松括号的[代数结构](@entry_id:137052)不变。对于任意一对[正则坐标](@entry_id:175654) $(q_k, p_k)$ 和 $(Q_k, P_k)$，必须满足以下关系：
$$ \{Q_i, Q_j\}_{q,p} = 0, \quad \{P_i, P_j\}_{q,p} = 0, \quad \{Q_i, P_j\}_{q,p} = \delta_{ij} $$
其中 $\delta_{ij}$ 是克罗内克符号。对于[点变换](@entry_id:171852) $Q_i = Q_i(q)$，由于新坐标不依赖于旧动量 $p_j$，第一个条件 $\{Q_i, Q_j\}_{q,p} = 0$ 自动满足。我们的任务是利用 $\{Q_i, P_j\}_{q,p} = \delta_{ij}$ 来确定 $P_j$ 的形式。

**一维情形**

对于只有一个自由度的系统，[点变换](@entry_id:171852)为 $Q=Q(q)$。正则条件简化为 $\{Q, P\}_{q,p} = 1$。根据泊松括号的定义：
$$ \{Q, P\}_{q,p} = \frac{\partial Q}{\partial q}\frac{\partial P}{\partial p} - \frac{\partial Q}{\partial p}\frac{\partial P}{\partial q} = 1 $$
由于 $Q$ 仅是 $q$ 的函数，$\frac{\partial Q}{\partial p} = 0$，上述方程简化为一个[一阶偏微分方程](@entry_id:178306)：
$$ \frac{dQ}{dq} \frac{\partial P}{\partial p} = 1 $$
只要 $\frac{dQ}{dq} \neq 0$，我们就可以解出 $\frac{\partial P}{\partial p} = \left(\frac{dQ}{dq}\right)^{-1}$。对 $p$ 积分，我们得到新动量 $P$ 的一般形式：
$$ P(q, p) = \frac{p}{\frac{dQ}{dq}} + f(q) $$
其中 $f(q)$ 是一个任意的关于 $q$ 的函数。在没有其他约束的情况下，我们通常选择最简洁的形式，即令 $f(q)=0$。因此，我们得到了一个至关重要的规则：
$$ P = \frac{p}{Q'(q)} $$

让我们通过几个例子来理解这个规则。

考虑一个简单的**标度变换** $Q = \lambda q$，其中 $\lambda$ 是一个非零常数 [@problem_id:2071943]。这里，$Q'(q) = \lambda$。根据我们的规则，新动量最简洁的形式为：
$$ P = \frac{p}{\lambda} $$
我们可以验证这个结果：$\{Q, P\}_{q,p} = \{\lambda q, p/\lambda\}_{q,p} = \frac{\partial(\lambda q)}{\partial q}\frac{\partial(p/\lambda)}{\partial p} - \frac{\partial(\lambda q)}{\partial p}\frac{\partial(p/\lambda)}{\partial q} = (\lambda)(\frac{1}{\lambda}) - 0 = 1$。这证实了变换是正则的。

另一个更有趣的例子是**[对数变换](@entry_id:267035)** $Q = \ln(q)$ (其中 $q > 0$) [@problem_id:2071963]。这里，$Q'(q) = 1/q$。因此，新动量为：
$$ P = \frac{p}{1/q} = qp $$
这个变换在处理某些与距离的对数相关的[中心力问题](@entry_id:178836)时非常有用。

**多维情形**

对于具有 $n$ 个自由度的系统，[点变换](@entry_id:171852)为 $Q_i = Q_i(q_1, \dots, q_n)$。动量之间的关系可以通过更普适的辛[形式[不变](@entry_id:275482)性](@entry_id:140168)导出，其结果是：
$$ p_k = \sum_{i=1}^{n} P_i \frac{\partial Q_i}{\partial q_k} $$
这个表达式将旧动量 $p_k$ 表示为新动量 $P_i$ 的[线性组合](@entry_id:154743)，系数是变换的[偏导数](@entry_id:146280)。为了更清晰地表达，我们引入坐标变换的**雅可比矩阵** (Jacobian matrix) $\mathbf{J}$，其[矩阵元](@entry_id:186505)定义为 $J_{ik} = \frac{\partial Q_i}{\partial q_k}$。这样，上述求和可以写成矩阵形式。注意到求和是对 $i$ 进行的，这对应于矩阵乘法的 $P_i (J^T)_{ik}$，其中 $\mathbf{J}^T$ 是 $\mathbf{J}$ 的转置矩阵。因此，我们可以简洁地写成：
$$ \mathbf{p} = \mathbf{J}^T \mathbf{P} $$
这里 $\mathbf{p}$ 和 $\mathbf{P}$ 是由各自的分量组成的列向量。如果雅可比矩阵 $\mathbf{J}$ 是可逆的（这意味着 $\det(\mathbf{J}) \neq 0$），那么 $\mathbf{J}^T$ 也是可逆的。我们可以解出新动量向量 $\mathbf{P}$ [@problem_id:2071931]：
$$ \mathbf{P} = (\mathbf{J}^T)^{-1} \mathbf{p} $$
这个强大的公式给出了任何可逆[点变换](@entry_id:171852)所对应的新动量的普适表达式。

例如，考虑一个二维平面上的[点变换](@entry_id:171852) [@problem_id:2071926]，从笛卡尔坐标 $(x, y)$ 变为新坐标 $(Q_1, Q_2)$：
$$ Q_1 = xy, \quad Q_2 = \frac{1}{2}(x^2 - y^2) $$
令旧坐标为 $q_1=x, q_2=y$。雅可比矩阵 $\mathbf{J}$ 为：
$$ \mathbf{J} = \begin{pmatrix} \frac{\partial Q_1}{\partial x} & \frac{\partial Q_1}{\partial y} \\ \frac{\partial Q_2}{\partial x} & \frac{\partial Q_2}{\partial y} \end{pmatrix} = \begin{pmatrix} y & x \\ x & -y \end{pmatrix} $$
其转置矩阵为 $\mathbf{J}^T = \mathbf{J}$，因为 $\mathbf{J}$ 是对称的。要找到新动量 $(P_1, P_2)$，我们需要计算 $(\mathbf{J}^T)^{-1}$。首先计算[行列式](@entry_id:142978)：
$$ \det(\mathbf{J}^T) = -y^2 - x^2 = -(x^2+y^2) $$
然后求逆：
$$ (\mathbf{J}^T)^{-1} = \frac{1}{-(x^2+y^2)} \begin{pmatrix} -y & -x \\ -x & y \end{pmatrix} = \frac{1}{x^2+y^2} \begin{pmatrix} y & x \\ x & -y \end{pmatrix} $$
最后，我们应用公式 $\mathbf{P} = (\mathbf{J}^T)^{-1} \mathbf{p}$：
$$ \begin{pmatrix} P_1 \\ P_2 \end{pmatrix} = \frac{1}{x^2+y^2} \begin{pmatrix} y & x \\ x & -y \end{pmatrix} \begin{pmatrix} p_x \\ p_y \end{pmatrix} = \frac{1}{x^2+y^2} \begin{pmatrix} y p_x + x p_y \\ x p_x - y p_y \end{pmatrix} $$
这就给出了新动量 $P_1$ 和 $P_2$ 关于旧相空间变量的完整表达式。

#### 使用[生成函数](@entry_id:146702)

构造[正则变换](@entry_id:178165)的另一种系统性方法是使用生成函数。对于[点变换](@entry_id:171852)，**第二类[生成函数](@entry_id:146702)** $F_2(\mathbf{q}, \mathbf{P}, t)$ 特别方便。变换方程由以下关系给出：
$$ Q_i = \frac{\partial F_2}{\partial P_i}, \quad p_i = \frac{\partial F_2}{\partial q_i} $$
考虑一种特殊形式的第二类生成函数，它对新动量 $\mathbf{P}$ 是线性的：
$$ F_2(\mathbf{q}, \mathbf{P}) = \sum_{j=1}^{n} g_j(\mathbf{q}) P_j $$
其中 $g_j$ 是旧坐标的任意函数。应用变换方程，我们得到新坐标：
$$ Q_i = \frac{\partial F_2}{\partial P_i} = \frac{\partial}{\partial P_i} \left( \sum_{j=1}^{n} g_j(\mathbf{q}) P_j \right) = g_i(\mathbf{q}) $$
这表明 $Q_i$ 确实只依赖于旧坐标 $q_j$，因此这种形式的 $F_2$ **总是**生成一个[点变换](@entry_id:171852)。同时，旧动量由下式给出：
$$ p_i = \frac{\partial F_2}{\partial q_i} = \sum_{j=1}^{n} P_j \frac{\partial g_j(\mathbf{q})}{\partial q_i} $$
由于我们已经证明了 $Q_j = g_j(\mathbf{q})$，这个关系可以重写为 $p_i = \sum_{j=1}^{n} P_j \frac{\partial Q_j}{\partial q_i}$，这与我们从泊松括号方法中得到的多维动量关系完全一致。

因此，任何一个定常[点变换](@entry_id:171852) $Q_i=Q_i(\mathbf{q})$ 都可以由一个形式为 $F_2(\mathbf{q}, \mathbf{P}) = \sum_j Q_j(\mathbf{q}) P_j$ 的第二类生成函数生成。

例如，让我们为一维平移变换 $Q = q + \delta_0$（其中 $\delta_0$ 是常数）找到[生成函数](@entry_id:146702) [@problem_id:2071929]。我们需要的 $F_2(q, P)$ 必须满足 $Q = \frac{\partial F_2}{\partial P} = q + \delta_0$。对 $P$ 积分得到：
$$ F_2(q, P) = (q + \delta_0)P + f(q) $$
其中 $f(q)$ 是积分“常数”。旧动量为 $p = \frac{\partial F_2}{\partial q} = P + f'(q)$。对于一个纯粹的坐标平移，我们期望动量不变，即 $p=P$。这就要求 $f'(q)=0$，即 $f(q)$ 为常数。选择最简单的形式（令常数为零），我们得到[生成函数](@entry_id:146702)：
$$ F_2(q, P) = (q + \delta_0)P $$

再比如，考虑形式为 $F_2(q, P) = \alpha q^n P$ 的[生成函数](@entry_id:146702) [@problem_id:2071960]。它生成的变换是：
$$ Q = \frac{\partial F_2}{\partial P} = \alpha q^n $$
$$ p = \frac{\partial F_2}{\partial q} = \alpha n q^{n-1} P $$
从第二个方程解出 $P$，我们得到 $P = p / (\alpha n q^{n-1})$。注意到 $Q'(q) = \alpha n q^{n-1}$，这再次验证了我们之前导出的公式 $P=p/Q'(q)$。

### [点变换](@entry_id:171852)的性质与推论

[点变换](@entry_id:171852)作为一类基础的[正则变换](@entry_id:178165)，具有一些重要的普适性质，这些性质揭示了哈密顿力学框架的深刻结构。

#### 相空间[体积守恒](@entry_id:276587)

所有[正则变换](@entry_id:178165)的一个标志性特征是它们保持相空间的体积不变，这一性质是[刘维尔定理](@entry_id:191167)的体现。在数学上，这意味着从旧坐标 $(q, p)$ 到新坐标 $(Q, P)$ 的完整相空间变换的雅可比行列式恒等于1。
$$ \det\left(\frac{\partial(Q_1, \dots, Q_n, P_1, \dots, P_n)}{\partial(q_1, \dots, q_n, p_1, \dots, p_n)}\right) = 1 $$
对于一维[点变换](@entry_id:171852) $Q=Q(q), P=p/Q'(q)$，我们可以显式地计算这个[雅可比行列式](@entry_id:137120) [@problem_id:2071957]：
$$ J = \det \begin{pmatrix} \frac{\partial Q}{\partial q} & \frac{\partial Q}{\partial p} \\ \frac{\partial P}{\partial q} & \frac{\partial P}{\partial p} \end{pmatrix} = \det \begin{pmatrix} Q'(q) & 0 \\ \frac{\partial}{\partial q}(p/Q'(q)) & 1/Q'(q) \end{pmatrix} $$
计算[行列式](@entry_id:142978)：
$$ J = Q'(q) \cdot \frac{1}{Q'(q)} - 0 \cdot \frac{\partial P}{\partial q} = 1 $$
这个结果表明，无论[点变换](@entry_id:171852)的具体形式如何，只要它是正则的，它就必然是保面积的。例如，对于标度变换 $Q = \lambda q, P = p/\lambda$，相空间的一个小矩形 $dq dp$ 被拉伸了 $\lambda$ 倍的 $q$ 轴，同时在 $p$ 轴上被压缩了 $1/\lambda$ 倍，总面积 $dQ dP = (\lambda dq)(dp/\lambda) = dq dp$ 保持不变。

#### [变换的复合](@entry_id:149828)

正则[点变换](@entry_id:171852)具有群的性质，即两个正则[点变换](@entry_id:171852)的相继作用，其结果仍然是一个正则[点变换](@entry_id:171852)。假设我们有两个一维变换 [@problem_id:2071927]：
1.  从 $(q, p_q)$ 到 $(Q, P_Q)$：$Q = f(q)$
2.  从 $(Q, P_Q)$ 到 $(R, P_R)$：$R = g(Q)$

这两个变换都是正则的，所以我们有：
$$ P_Q = \frac{p_q}{f'(q)} \quad \text{和} \quad P_R = \frac{P_Q}{g'(Q)} $$
将第一个式子代入第二个，得到最终动量 $P_R$ 与初始动量 $p_q$ 的关系：
$$ P_R = \frac{1}{g'(Q)} \left( \frac{p_q}{f'(q)} \right) = \frac{p_q}{f'(q)g'(Q)} $$
由于 $Q=f(q)$，我们可以将 $g'(Q)$ 写成 $g'(f(q))$。因此：
$$ P_R = \frac{p_q}{f'(q) g'(f(q))} $$
现在考虑复合变换 $R = g(f(q))$。根据[链式法则](@entry_id:190743)，其导数为 $dR/dq = g'(f(q))f'(q)$。因此，我们发现 $P_R = p_q / (dR/dq)$。这表明复合变换 $q \to R$ 及其导出的动量变换 $p_q \to P_R$ 同样遵循正则[点变换](@entry_id:171852)的基本规则。

#### 物理可观测量的不变性

物理定律不应依赖于我们选择的[坐标系](@entry_id:156346)。在哈密顿形式中，这一原理表现为**泊松括号在[正则变换](@entry_id:178165)下的[形式不变性](@entry_id:275482)**。对于任意两个物理量（即相空间函数）$A$ 和 $B$，它们的[泊松括号](@entry_id:151133)在变换前后保持不变：
$$ \{A, B\}_{q,p} = \{A, B\}_{Q,P} $$
这一性质保证了物理系统的[代数结构](@entry_id:137052)，如守恒律和对称性，在不同[正则坐标](@entry_id:175654)系下具有相同的数学表达。

一个深刻的例子是[角动量代数](@entry_id:178952)。在三维空间中，一个粒子的角动量分量 $L_x, L_y, L_z$ 在笛卡尔坐标系下满足著名的[泊松括号](@entry_id:151133)关系 $\{L_i, L_j\} = \epsilon_{ijk}L_k$。现在，我们进行一个从笛卡尔坐标 $(x,y,z)$ 到球坐标 $(r, \theta, \phi)$ 的[点变换](@entry_id:171852) [@problem_id:2071938]。这是一个标准的[点变换](@entry_id:171852)，我们可以导出新旧动量之间的关系，并将角动量分量用新的相空间变量 $(r, \theta, \phi, p_r, p_\theta, p_\phi)$ 表示。经过推导，可以得到：
$$ L_x = -p_{\theta}\sin\phi - p_{\phi}\cot\theta\cos\phi $$
$$ L_y = p_{\theta}\cos\phi - p_{\phi}\cot\theta\sin\phi $$
$$ L_z = p_{\phi} $$
现在，让我们在**球坐标**的相空间中直接计算[泊松括号](@entry_id:151133) $\{L_y, L_z\}$。
$$ \{L_y, L_z\}_{(r,\theta,\phi), (p_r, p_\theta, p_\phi)} = \{L_y, p_\phi\} = \frac{\partial L_y}{\partial \phi}\frac{\partial p_\phi}{\partial p_\phi} - \frac{\partial L_y}{\partial p_\phi}\frac{\partial p_\phi}{\partial \phi} = \frac{\partial L_y}{\partial \phi} $$
对 $L_y$ 的表达式求关于 $\phi$ 的[偏导数](@entry_id:146280)：
$$ \frac{\partial L_y}{\partial \phi} = \frac{\partial}{\partial \phi}(p_{\theta}\cos\phi - p_{\phi}\cot\theta\sin\phi) = -p_{\theta}\sin\phi - p_{\phi}\cot\theta\cos\phi $$
我们发现，这个结果恰好是在球坐标下 $L_x$ 的表达式。因此，我们验证了 $\{L_y, L_z\} = L_x$ 在坐标变换后依然成立。这强有力地证明了哈密顿形式的内在一致性和[坐标无关性](@entry_id:159715)。

#### 变换的[奇点](@entry_id:137764)

[点变换](@entry_id:171852)的正则性依赖于关系 $P=p/Q'(q)$（一维情形）或 $\mathbf{P} = (\mathbf{J}^T)^{-1} \mathbf{p}$（多维情形）的良好定义。一个潜在的问题出现在当分母为零时，即在一维情况下 $Q'(q)=0$，或在多维情况下雅可比矩阵 $\mathbf{J}$ 奇异（$\det(\mathbf{J})=0$）时。这些点被称为变换的**[奇点](@entry_id:137764)** (singularities)。

在[奇点](@entry_id:137764)处，坐标变换不是局部[一一对应](@entry_id:143935)的。例如，考虑一个粒子在圆周上运动，其位置由角度 $q$ 描述。我们引入新坐标 $Q = R\cos(q)$ [@problem_id:2071976]。这实际上是将圆周运动投影到直径上。[变换的导数](@entry_id:164838)是 $dQ/dq = -R\sin(q)$。在 $q=0$ 和 $q=\pi$ 处，该导数为零。这意味着在 $Q=+R$ ($q=0$) 和 $Q=-R$ ($q=\pi$) 这两个投影的端点，变换是奇异的。

让我们分析当粒子以恒定正动量 $p=p_0$ 运动，其位置平滑地经过 $q=\pi$ 时，新动量 $P$ 的行为：
$$ P(q) = \frac{p_0}{-R\sin(q)} $$
当 $q$ 从略小于 $\pi$ 的值（例如 $\pi-\epsilon$）趋近于 $\pi$ 时，$\sin(q) \approx \sin(\pi-\epsilon) = \sin(\epsilon)$ 是一个很小的正数。因此，$P(q) \to -\infty$。
当 $q$ 从略大于 $\pi$ 的值（例如 $\pi+\epsilon$）经过 $\pi$ 时，$\sin(q) \approx \sin(\pi+\epsilon) = -\sin(\epsilon)$ 是一个很小的负数。因此，$P(q) \to +\infty$。

这意味着，当[粒子平滑](@entry_id:753218)地通过圆周上的 $\pi$ 点时，新动量 $P$ 会经历一次从负无穷到正无穷的**不连续跳变**。这揭示了一个重要的教训：一个在物理上看似无害的[坐标变换](@entry_id:172727)，可能会在某些点引入非物理的奇异行为，使得该[坐标系](@entry_id:156346)不适用于描述跨越这些[奇点](@entry_id:137764)的动力学过程。因此，在选择[坐标系](@entry_id:156346)时，分析其雅可比行列式并识别[奇点](@entry_id:137764)是至关重要的一步。