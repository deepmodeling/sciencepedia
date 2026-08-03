## 引言
在微分几何与理论物理的研究中，我们经常需要在流形的每一点上选择一组基向量来描述几何和物理量。虽然源于局部坐标系的坐标基底直观易懂，但在处理具有内在对称性（如李群）或复杂几何结构（如广义相对论中的弯曲时空）的系统时，它们往往显得笨拙。非坐标基（Noncoordinate Bases），也称为标架场（Frame Fields），为此提供了一个更强大、更灵活的分析框架。它突破了坐标网格的限制，允许我们选择在代数或物理上最自然的基底，从而极大地简化计算并揭示更深层次的结构。

本文旨在系统性地介绍非坐标基的核心思想与实用技术。在“原理与机制”一章中，我们将建立其数学基础，定义李括号与结构函数，并探讨如何在任意基底下进行微积分。接着，在“应用与交叉学科联系”中，我们将展示这些工具如何在黎曼几何、广义相对论和李群理论等领域大放异彩。最后，通过“动手实践”部分，读者将有机会亲手计算，将理论知识转化为解决具体问题的能力。

## 原理与机制

在微分几何中，我们研究的对象是光滑流形，而描述流形上局部几何与物理性质的基本工具是向量场和张量场。为了进行具体的计算，我们通常需要在每一点的切空间中选取一个基底。最自然的选择似乎是源于局部坐标系的 **坐标基底 (coordinate basis)**。然而，在许多理论与应用的情境下，特别是处理具有对称性的几何结构（如李群）或在物理学（如广义相对论）中，**非坐标基底 (noncoordinate bases)**，也称为 **标架场 (frame fields)** 或 **非完整基底 (anholonomic bases)**，提供了更为强大和简洁的分析框架。本章将深入探讨非坐标基底的定义、核心性质及其在几何计算中的关键作用。

### 非坐标基底的定义与核心特征

我们首先回顾坐标基底。给定流形 $M$ 上的一个局部坐标图 $(U, x^1, \dots, x^n)$，它自然地在每一点 $p \in U$ 的切空间 $T_pM$ 中定义了一组基向量 $\{\partial_1, \dots, \partial_n\}$，其中 $\partial_i = \frac{\partial}{\partial x^i}$。这组基底的一个根本性质是其任意两个基向量的 **李括号 (Lie bracket)** 恒为零：
$$
[\partial_i, \partial_j] = \partial_i \partial_j - \partial_j \partial_i = 0
$$
这反映了二阶偏导数的可交换性。这个性质在几何上意味着沿着一个坐标方向移动一小段，再沿着另一个坐标方向移动，其最终位置与交换移动顺序的结果相同，形成一个无穷小的坐标矩形。

与此相对，一个 **非坐标基底** 或 **标架** 是在流形的一个开集上定义的任意一组光滑向量场 $\{e_1, \dots, e_n\}$，它们在每一点都线性无关，从而构成该点切空间的一个基底。其最关键的特征在于，这些基向量场之间的李括号通常 **不为零**：
$$
[e_i, e_j] \neq 0
$$
这种非对易性是“非坐标”或“非完整”的本质体现。它意味着沿着这些基向量方向的无穷小位移通常无法“闭合”成一个矩形。从Frobenius定理的角度看，一组向量场的李括号如果能全部用这组向量场自身线性表示，那么这组向量场积分得到的叶状结构是否能成为一个坐标系的网格，取决于它们的李括号是否为零。李括号不为零，意味着不存在一个坐标系，使得这些基向量恰好是该坐标系的偏导数向量场。

### 不同基底下的表示

一旦我们选定了一个标架 $\{e_a\}$，流形上的任何张量场都可以用这个标架及其对偶标架来表示。这种表示的转换是理解非坐标基底应用的第一步。

#### 向量场与对偶1-形式的基底变换

任何一个向量场 $V$ 都可以表示为标架 $\{e_a\}$ 的线性组合，其系数是光滑函数 $c^a(x)$：
$$
V = c^a(x) e_a
$$
这里的求和约定适用于标架的索引。例如，我们可以在一个非坐标基底中展开一个坐标基向量。考虑在 $\mathbb{R}^3$ 上定义的一个标架 [@problem_id:999536]：
$$
\begin{aligned}
e_1 = \partial_y + z\partial_x \\
e_2 = \partial_z + x\partial_y \\
e_3 = \partial_x + y\partial_z
\end{aligned}
$$
若要将坐标基向量 $\partial_y$ 表示为 $e_a$ 的线性组合 $\partial_y = c^1 e_1 + c^2 e_2 + c^3 e_3$，我们只需将 $e_a$ 的表达式代入，并比较 $\partial_x, \partial_y, \partial_z$ 的系数。这会导出一个关于函数 $c^a(x, y, z)$ 的线性方程组。通过求解这个代数系统，我们可以得到每个分量，例如 $c^2 = \frac{yz}{1 + xyz}$。这个过程展示了在不同基底之间转换向量场分量的基本代数方法。

与向量基底 $\{e_a\}$ 相伴的是其 **对偶基底 (dual basis)**，也称为 **余标架 (coframe)** $\{\theta^a\}$。这是一组1-形式场，由对偶关系定义：
$$
\theta^a(e_b) = \delta^a_b
$$
其中 $\delta^a_b$ 是克罗内克 delta。要找到余标架的具体表达式，我们可以将其在坐标基底的对偶基 $\{dx^i\}$ 中展开，$\theta^a = f^a_i dx^i$，然后利用上述对偶关系来确定系数函数 $f^a_i$。

作为一个例子 [@problem_id:999546]，考虑 $\mathbb{R}^3$ 上的标架 $e_1 = \partial_x + \partial_y$, $e_2 = \partial_y + \partial_z$, $e_3 = \partial_z + \partial_x$。为了求出 $\theta^1$，我们设 $\theta^1 = a\,dx + b\,dy + c\,dz$。通过施加条件 $\theta^1(e_1)=1$, $\theta^1(e_2)=0$ 和 $\theta^1(e_3)=0$，我们得到一个关于系数 $a, b, c$ 的线性方程组。求解后可得 $\theta^1 = \frac{1}{2}dx + \frac{1}{2}dy - \frac{1}{2}dz$。这种方法是系统性的，可以推广到任意标架。

#### 度量张量的表示

张量的分量同样依赖于所选的基底。度量张量 $g$ 在标架 $\{e_a\}$ 中的分量由内积 $g_{ab} = g(e_a, e_b)$ 给出。即使在欧几里得空间，其标准度量在笛卡尔坐标基底 $\{\partial_i\}$ 下的分量是单位矩阵 $(\delta_{ij})$，但在一个非坐标基底中，其分量 $g_{ab}$ 可能会变得非常不平凡。

例如，在 $\mathbb{R}^3$ 的欧几里得度量下，考虑标架 [@problem_id:999626]：
$$
e_1 = \partial_x + y\partial_z, \quad e_2 = \partial_y + z\partial_x, \quad e_3 = \partial_z + x\partial_y
$$
由于笛卡尔基底是标准正交的，即 $g(\partial_i, \partial_j) = \delta_{ij}$，我们可以利用度量的双线性性质来计算新基底下的分量。例如，分量 $g_{12}$ 的计算如下：
$$
\begin{aligned}
g_{12} = g(e_1, e_2) \\
= g(\partial_x + y\partial_z, \partial_y + z\partial_x) \\
= g(\partial_x, \partial_y) + z g(\partial_x, \partial_x) + y g(\partial_z, \partial_y) + yz g(\partial_z, \partial_x) \\
= 0 + z \cdot 1 + y \cdot 0 + yz \cdot 0 = z
\end{aligned}
$$
这个结果 $g_{12} = z$ 表明，新度量矩阵的非对角元可以是非零的，并且可以是坐标的函数。这意味着标架 $\{e_a\}$ 既不是正交的，也不是标准化的。在广义相对论中，物理学家经常选择适应特定时空对称性或观测者运动状态的标架（例如，自由落体观测者的局部惯性标架），在这些标架下，尽管时空是弯曲的，度量张量在某一点上可以取闵可夫斯基形式 $g_{ab} = \eta_{ab}$。然而，这仅仅是在一点成立，其导数通常不为零，这体现为非零的联络系数。

### 标架的代数：李括号与结构函数

非坐标基底的非对易性由李括号 $[e_i, e_j]$ 完全刻画。由于 $\{e_k\}$ 构成一个基底，两个基向量的李括号（其本身也是一个向量场）必然可以再次按这个基底展开：
$$
[e_i, e_j] = C^k_{ij}(x) e_k
$$
这里的系数 $C^k_{ij}(x)$ 被称为 **结构函数 (structure functions)** 或 **结构系数 (structure coefficients)**。这些函数封装了标架的“扭曲”或“非完整”程度。如果所有 $C^k_{ij}$ 都恒为零，那么该标架（至少在局部上）就是一个坐标基底。

#### 结构函数的计算

在坐标基底 $\{\partial_\mu\}$ 下，两个向量场 $X = X^\mu \partial_\mu$ 和 $Y = Y^\nu \partial_\nu$ 的李括号可以表示为：
$$
[X, Y] = \sum_\sigma \left( \sum_\mu X^\mu \frac{\partial Y^\sigma}{\partial x^\mu} - Y^\mu \frac{\partial X^\sigma}{\partial x^\mu} \right) \partial_\sigma
$$
或更简洁地写作 $[X, Y]^\sigma = X(Y^\sigma) - Y(X^\sigma)$。我们可以利用这个公式来计算标架向量之间的李括号，然后将其结果重新用标架 $\{e_k\}$ 表示，从而读出结构函数。

考虑一个简单的例子 [@problem_id:999508]。在 $\mathbb{R}^2$ 上，令 $e_1 = \partial_x$，$e_2 = x\partial_x + \partial_y$。它们的李括号为：
$$
[e_1, e_2] = [\partial_x, x\partial_x + \partial_y] = [\partial_x, x\partial_x] + [\partial_x, \partial_y] = (\partial_x(x))\partial_x + x[\partial_x, \partial_x] + 0 = \partial_x
$$
由于 $e_1 = \partial_x$，我们得到 $[e_1, e_2] = e_1$。与 $[e_1, e_2] = C^k_{12} e_k$ 比较，我们得到 $C^1_{12} = 1$ 和 $C^2_{12} = 0$。

结构函数可以是常数，也可以是坐标的函数。例如，对于在 $\mathbb{R}^3$ 中的一个更复杂的标架 [@problem_id:999575]，计算 $[e_1, e_2]$ 后得到一个向量场 $-2\alpha \partial_z$。为了找到结构函数 $C^k_{12}$，我们需要将 $\partial_z$ 用 $\{e_1, e_2, e_3\}$ 表示出来，这又回到了基底变换的问题。完成这个变换后，我们就可以直接读出 $C^k_{12}$ 的表达式，它们可能是 $x,y,z$ 的函数。

一个特别富有启发性的例子是极坐标下的正交标架 [@problem_id:999563]。在 $\mathbb{R}^2 \setminus \{0\}$ 上，坐标基底是 $\{\partial_r, \partial_\phi\}$。一个更自然的单位正交标架是 $E_r = \partial_r$ 和 $E_\phi = \frac{1}{r}\partial_\phi$。它们的李括号是：
$$
[E_r, E_\phi] = [\partial_r, \frac{1}{r}\partial_\phi] = \partial_r(\frac{1}{r})\partial_\phi + \frac{1}{r}[\partial_r, \partial_\phi] = -\frac{1}{r^2}\partial_\phi = -\frac{1}{r} E_\phi
$$
这个非零的结果表明，即使是一个正交标架，如果它不是由一个坐标系直接产生，它也通常是一个非坐标基底。

### 非坐标基底下的微积分

在曲面上进行微积分的核心工具是 **协变导数 (covariant derivative)** $\nabla$。对于坐标基底，协变导数的计算由克里斯托费尔符号 (Christoffel symbols) $\Gamma^k_{ij}$ 给出：$\nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k$。那么，在非坐标基底中，我们如何定义和计算协变导数呢？

#### 联络系数

类似于坐标基底的情况，我们在标架 $\{e_i\}$ 中定义 **联络系数 (connection coefficients)** $\Gamma^k_{ij}$ (有时也称为 **里奇旋转系数 (Ricci rotation coefficients)**) 如下：
$$
\nabla_{e_i} e_j = \Gamma^k_{ij} e_k
$$
这些系数 $\Gamma^k_{ij}$ 描述了基向量场 $e_j$ 沿着另一个基向量场 $e_i$ 方向的无穷小变化。**一个至关重要的概念是：即使在平坦空间（如欧几里得空间，其曲率为零）中，只要使用的不是笛卡尔坐标基底，联络系数通常也不为零。**

让我们通过一个例子来阐明这一点 [@problem_id:999651]。考虑平坦的 $\mathbb{R}^2$ 和标架 $e_1 = \partial_x$, $e_2 = x\partial_x + \partial_y$。在平坦空间中使用笛卡尔坐标，对向量场 $Y = Y^x \partial_x + Y^y \partial_y$ 求协变导数 $\nabla_X Y$ 等同于对其分量求方向导数：$\nabla_X Y = (X(Y^x))\partial_x + (X(Y^y))\partial_y$。我们来计算 $\nabla_{e_2} e_2$：
$$
\begin{aligned}
\nabla_{e_2} e_2 = \nabla_{x\partial_x + \partial_y} (x\partial_x + \partial_y) \\
= ( (x\partial_x + \partial_y)(x) ) \partial_x + ( (x\partial_x + \partial_y)(1) ) \partial_y \\
= (x \cdot 1 + 0) \partial_x + (0) \partial_y \\
= x \partial_x = x e_1
\end{aligned}
$$
将结果与定义式 $\nabla_{e_2} e_2 = \Gamma^k_{22} e_k = \Gamma^1_{22} e_1 + \Gamma^2_{22} e_2$ 相比较，我们立即得到 $\Gamma^1_{22} = x$ 和 $\Gamma^2_{22} = 0$。这个非零的联络系数 $\Gamma^1_{22}=x$ 并非来自空间的弯曲，而是完全源于基向量 $e_2$ 自身随位置 $x$ 的变化。

#### 挠率与Koszul公式

联络与李括号之间存在深刻的联系。这种联系通过 **挠率张量 (torsion tensor)** $T$ 来体现，其定义为：
$$
T(X, Y) = \nabla_X Y - \nabla_Y X - [X, Y]
$$
在任意标架 $\{e_i\}$ 中，其分量为：
$$
T^k_{ij} = \Gamma^k_{ij} - \Gamma^k_{ji} - C^k_{ij}
$$
对于黎曼几何中标准的 **Levi-Civita联络**，其定义要求挠率为零，即 $T=0$。在这种情况下，我们得到一个至关重要的关系：
$$
\Gamma^k_{ij} - \Gamma^k_{ji} = C^k_{ij}
$$
这意味着结构函数恰好是Levi-Civita联络系数的反对称部分。这揭示了结构函数的几何意义：它们度量了沿着两个基向量方向的平行移动路径所形成四边形的“不闭合”程度。

此外，对于一个度量兼容的联络（如Levi-Civita联络），联络系数、度量分量和结构函数三者可以通过 **Koszul公式** 联系起来。在标架 $\{e_i\}$ 中，该公式的一种形式为：
$$
2 g(\nabla_{e_i} e_j, e_k) = e_i(g_{jk}) + e_j(g_{ik}) - e_k(g_{ij}) - g_{jm}C^m_{ik} - g_{im}C^m_{jk} + g_{km}C^m_{ij}
$$
这个公式在理论上极为重要，因为它表明，一旦我们知道了度量在标架中的分量 $g_{ij}$ 和标架的结构函数 $C^k_{ij}$，Levi-Civita联络就被唯一确定了。公式中的 $g([e_i, e_j], e_k) = g(C^m_{ij}e_m, e_k) = C^m_{ij}g_{mk}$ 等项直接体现了标架的非对易性对几何联络的贡献 [@problem_id:999508]。

### 进阶主题与应用

非坐标基底的概念在现代微分几何与理论物理中扮演着核心角色。

#### Cartan结构方程

除了通过李括号的定义来计算结构函数，Élie Cartan 发展了一套基于微分形式的等价而 souvent 更为优雅的方法。**Cartan第一结构方程** 将余标架1-形式的外微分与结构函数联系起来：
$$
d\theta^k = - \frac{1}{2} C^k_{ij} \theta^i \wedge \theta^j
$$
这个方程提供了一种计算结构函数的替代途径：首先计算出对偶基底 $\{\theta^k\}$，然后计算它们的外微分 $d\theta^k$，最后将结果与 $\theta^i \wedge \theta^j$ 进行比较，即可读出 $C^k_{ij}$。例如，在 [@problem_id:999697] 的设定中，通过计算李括号我们得到 $[e_1, e_3] = e_2$，这意味着 $C^2_{13}=1$。我们也可以通过计算 $d\theta^2$ 并找到其在基底 $\theta^1 \wedge \theta^3$ 上的分量来验证这一结果。

#### 李群上的左不变标架

非坐标基底的一个 canonical 应用场景是 **李群 (Lie groups)**。一个李群 $G$ 的李代数 $\mathfrak{g}$ 是其单位元处的切空间 $T_eG$。$\mathfrak{g}$ 中的任意一个向量 $v$ 都可以通过群的左乘操作唯一地扩展成 $G$ 上的一个 **左不变向量场 (left-invariant vector field)**。选取李代数的一组基底，我们就可以得到整个李群上的一个左不变标架 $\{e_a\}$。

对于这样的标架，一个美妙的事实是其结构函数是 **常数**，即 $C^k_{ij}$ 不依赖于群上的点。这些常数被称为李代数 $\mathfrak{g}$ 的 **结构常数 (structure constants)**。例如，对于 $SU(2)$ 群，其李代数 $\mathfrak{su}(2)$ 的结构常数可以由Levi-Civita符号给出：$C^k_{ab} = \epsilon_{abk}$ [@problem_id:999511]。

在李群上，我们可以定义具有附加性质的联络。例如，一个联络可能不是无挠的。如果我们在Levi-Civita联络 $\nabla$ 的基础上增加一个张量场 $K$，定义新的联络 $\tilde{\nabla}_X Y = \nabla_X Y + K(X,Y)$，那么新联络的挠率 $\tilde{T}$ 就由 $K$ 的反对称部分决定：$\tilde{T}^k_{ij} = K^k_{ij} - K^k_{ji}$。这种构造在爱因斯坦-嘉当引力理论和一些规范场论中非常重要，它们允许时空具有挠率，而挠率与物质的自旋密度相关联 [@problem_id:999511]。

同样，李代数的 Killing 型 $K_{ij} = C^l_{ik} C^k_{jl}$ 是一个重要的不变量，它反映了李代数的结构。它的计算完全依赖于结构常数 [@problem_id:999560]。

综上所述，非坐标基底或标架场是超越了特定坐标系限制的强大工具。它们通过结构函数将基底的非对易性代数化，通过联络系数将微积分推广到任意基底，并最终通过Cartan方程和在李群上的应用，展现了微分几何深邃的代数-几何对偶性。掌握非坐标基底是深入理解广义相对论、规范场论以及现代几何学不可或缺的一步。