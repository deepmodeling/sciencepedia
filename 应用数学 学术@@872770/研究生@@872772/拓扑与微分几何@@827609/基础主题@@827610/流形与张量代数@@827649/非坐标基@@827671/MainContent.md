## 引言
在微分几何与理论物理的研究中，我们经常需要在[流形](@entry_id:153038)的每一点上选择一组[基向量](@entry_id:199546)来描述几何和物理量。虽然源于局部坐标系的[坐标基](@entry_id:270149)底直观易懂，但在处理具有内在对称性（如[李群](@entry_id:137659)）或复杂几何结构（如广义相对论中的[弯曲时空](@entry_id:159822)）的系统时，它们往往显得笨拙。非[坐标基](@entry_id:270149)（Noncoordinate Bases），也称为[标架场](@entry_id:160577)（Frame Fields），为此提供了一个更强大、更灵活的分析框架。它突破了坐标网格的限制，允许我们选择在代数或物理上最自然的基底，从而极大地简化计算并揭示更深层次的结构。

本文旨在系统性地介绍非[坐标基](@entry_id:270149)的核心思想与实用技术。在“原理与机制”一章中，我们将建立其数学基础，定义[李括号](@entry_id:636461)与[结构函数](@entry_id:161908)，并探讨如何在任意基底下进行微积分。接着，在“应用与交叉学科联系”中，我们将展示这些工具如何在[黎曼几何](@entry_id:160508)、广义相对论和[李群](@entry_id:137659)理论等领域大放异彩。最后，通过“动手实践”部分，读者将有机会亲手计算，将理论知识转化为解决具体问题的能力。

## 原理与机制

在[微分几何](@entry_id:145818)中，我们研究的对象是光滑流形，而描述[流形](@entry_id:153038)上局部几何与物理性质的基本工具是向量场和[张量场](@entry_id:190170)。为了进行具体的计算，我们通常需要在每一点的切空间中选取一个基底。最自然的选择似乎是源于局部坐标系的 **[坐标基](@entry_id:270149)底 (coordinate basis)**。然而，在许多理论与应用的情境下，特别是处理具有对称性的几何结构（如[李群](@entry_id:137659)）或在物理学（如广义相对论）中，**非[坐标基](@entry_id:270149)底 (noncoordinate bases)**，也称为 **[标架场](@entry_id:160577) (frame fields)** 或 **[非完整基](@entry_id:161763)底 (anholonomic bases)**，提供了更为强大和简洁的分析框架。本章将深入探讨非[坐标基](@entry_id:270149)底的定义、核心性质及其在几何计算中的关键作用。

### 非[坐标基](@entry_id:270149)底的定义与核心特征

我们首先回顾[坐标基](@entry_id:270149)底。给定[流形](@entry_id:153038) $M$ 上的一个[局部坐标](@entry_id:181200)图 $(U, x^1, \dots, x^n)$，它自然地在每一点 $p \in U$ 的切空间 $T_pM$ 中定义了一组[基向量](@entry_id:199546) $\{\partial_1, \dots, \partial_n\}$，其中 $\partial_i = \frac{\partial}{\partial x^i}$。这组基底的一个根本性质是其任意两个[基向量](@entry_id:199546)的 **[李括号](@entry_id:636461) (Lie bracket)** 恒为零：
$$
[\partial_i, \partial_j] = \partial_i \partial_j - \partial_j \partial_i = 0
$$
这反映了[二阶偏导数](@entry_id:635213)的[可交换性](@entry_id:263314)。这个性质在几何上意味着沿着一个坐标方向移动一小段，再沿着另一个坐标方向移动，其最终位置与交换移动顺序的结果相同，形成一个无穷小的坐标矩形。

与此相对，一个 **非[坐标基](@entry_id:270149)底** 或 **标架** 是在[流形](@entry_id:153038)的一个开集上定义的任意一组光滑向量场 $\{e_1, \dots, e_n\}$，它们在每一点都[线性无关](@entry_id:148207)，从而构成该点切空间的一个基底。其最关键的特征在于，这些[基向量](@entry_id:199546)场之间的[李括号](@entry_id:636461)通常 **不为零**：
$$
[e_i, e_j] \neq 0
$$
这种[非对易性](@entry_id:153545)是“非坐标”或“非完整”的本质体现。它意味着沿着这些[基向量](@entry_id:199546)方向的[无穷小位移](@entry_id:202209)通常无法“闭合”成一个矩形。从[Frobenius定理](@entry_id:181858)的角度看，一组[向量场的李括号](@entry_id:193400)如果能全部用这组向量场自身[线性表示](@entry_id:139970)，那么这组向量场积分得到的[叶状结构](@entry_id:160209)是否能成为一个[坐标系](@entry_id:156346)的网格，取决于它们的[李括号](@entry_id:636461)是否为零。李括号不为零，意味着不存在一个[坐标系](@entry_id:156346)，使得这些[基向量](@entry_id:199546)恰好是该[坐标系](@entry_id:156346)的偏导数向量场。

### 不同基底下的表示

一旦我们选定了一个标架 $\{e_a\}$，[流形](@entry_id:153038)上的任何[张量场](@entry_id:190170)都可以用这个标架及其对偶标架来表示。这种表示的转换是理解非[坐标基](@entry_id:270149)底应用的第一步。

#### 向量场与对偶[1-形式](@entry_id:270392)的基底变换

任何一个向量场 $V$ 都可以表示为标架 $\{e_a\}$ 的[线性组合](@entry_id:154743)，其系数是[光滑函数](@entry_id:267124) $c^a(x)$：
$$
V = c^a(x) e_a
$$
这里的求和约定适用于标架的索引。例如，我们可以在一个非[坐标基](@entry_id:270149)底中展开一个[坐标基](@entry_id:270149)向量。考虑在 $\mathbb{R}^3$ 上定义的一个标架 [@problem_id:999536]：
$$
\begin{aligned}
e_1 = \partial_y + z\partial_x \\
e_2 = \partial_z + x\partial_y \\
e_3 = \partial_x + y\partial_z
\end{aligned}
$$
若要将[坐标基](@entry_id:270149)向量 $\partial_y$ 表示为 $e_a$ 的[线性组合](@entry_id:154743) $\partial_y = c^1 e_1 + c^2 e_2 + c^3 e_3$，我们只需将 $e_a$ 的表达式代入，并比较 $\partial_x, \partial_y, \partial_z$ 的系数。这会导出一个关于函数 $c^a(x, y, z)$ 的[线性方程组](@entry_id:148943)。通过求解这个代数系统，我们可以得到每个分量，例如 $c^2 = \frac{yz}{1 + xyz}$。这个过程展示了在不同基底之间转换向量场分量的基本代数方法。

与向量基底 $\{e_a\}$ 相伴的是其 **对偶基底 (dual basis)**，也称为 **[余标架](@entry_id:637284) (coframe)** $\{\theta^a\}$。这是一组[1-形式](@entry_id:270392)场，由对偶关系定义：
$$
\theta^a(e_b) = \delta^a_b
$$
其中 $\delta^a_b$ 是克罗内克 delta。要找到[余标架](@entry_id:637284)的具体表达式，我们可以将其在[坐标基](@entry_id:270149)底的对偶基 $\{dx^i\}$ 中展开，$\theta^a = f^a_i dx^i$，然后利用上述对偶关系来确定系数函数 $f^a_i$。

作为一个例子 [@problem_id:999546]，考虑 $\mathbb{R}^3$ 上的标架 $e_1 = \partial_x + \partial_y$, $e_2 = \partial_y + \partial_z$, $e_3 = \partial_z + \partial_x$。为了求出 $\theta^1$，我们设 $\theta^1 = a\,dx + b\,dy + c\,dz$。通过施加条件 $\theta^1(e_1)=1$, $\theta^1(e_2)=0$ 和 $\theta^1(e_3)=0$，我们得到一个关于系数 $a, b, c$ 的[线性方程组](@entry_id:148943)。求解后可得 $\theta^1 = \frac{1}{2}dx + \frac{1}{2}dy - \frac{1}{2}dz$。这种方法是系统性的，可以推广到任意标架。

#### 度量张量的表示

张量的分量同样依赖于所选的基底。度量张量 $g$ 在标架 $\{e_a\}$ 中的分量由[内积](@entry_id:158127) $g_{ab} = g(e_a, e_b)$ 给出。即使在欧几里得空间，其标准度量在[笛卡尔坐标](@entry_id:167698)基底 $\{\partial_i\}$ 下的分量是单位矩阵 $(\delta_{ij})$，但在一个非[坐标基](@entry_id:270149)底中，其分量 $g_{ab}$ 可能会变得非常不平凡。

例如，在 $\mathbb{R}^3$ 的[欧几里得度量](@entry_id:147197)下，考虑标架 [@problem_id:999626]：
$$
e_1 = \partial_x + y\partial_z, \quad e_2 = \partial_y + z\partial_x, \quad e_3 = \partial_z + x\partial_y
$$
由于笛卡尔基底是标准正交的，即 $g(\partial_i, \partial_j) = \delta_{ij}$，我们可以利用度量的[双线性性](@entry_id:146819)质来计算新基底下的分量。例如，分量 $g_{12}$ 的计算如下：
$$
\begin{aligned}
g_{12} = g(e_1, e_2) \\
= g(\partial_x + y\partial_z, \partial_y + z\partial_x) \\
= g(\partial_x, \partial_y) + z g(\partial_x, \partial_x) + y g(\partial_z, \partial_y) + yz g(\partial_z, \partial_x) \\
= 0 + z \cdot 1 + y \cdot 0 + yz \cdot 0 = z
\end{aligned}
$$
这个结果 $g_{12} = z$ 表明，新度量矩阵的非对角元可以是非零的，并且可以是坐标的函数。这意味着标架 $\{e_a\}$ 既不是正交的，也不是[标准化](@entry_id:637219)的。在广义相对论中，物理学家经常选择适应特定[时空对称性](@entry_id:179029)或观测者运动状态的标架（例如，自由落体观测者的局部惯性标架），在这些标架下，尽管时空是弯曲的，度量张量在某一点上可以取闵可夫斯基形式 $g_{ab} = \eta_{ab}$。然而，这仅仅是在一点成立，其导数通常不为零，这体现为非零的[联络系数](@entry_id:157618)。

### 标架的代数：[李括号](@entry_id:636461)与[结构函数](@entry_id:161908)

非[坐标基](@entry_id:270149)底的非对易性由李括号 $[e_i, e_j]$ 完全刻画。由于 $\{e_k\}$ 构成一个基底，两个[基向量](@entry_id:199546)的李括号（其本身也是一个向量场）必然可以再次按这个基底展开：
$$
[e_i, e_j] = C^k_{ij}(x) e_k
$$
这里的系数 $C^k_{ij}(x)$ 被称为 **[结构函数](@entry_id:161908) (structure functions)** 或 **结构系数 (structure coefficients)**。这些函数封装了标架的“扭曲”或“非完整”程度。如果所有 $C^k_{ij}$ 都恒为零，那么该标架（至少在局部上）就是一个[坐标基](@entry_id:270149)底。

#### [结构函数](@entry_id:161908)的计算

在[坐标基](@entry_id:270149)底 $\{\partial_\mu\}$ 下，两个向量场 $X = X^\mu \partial_\mu$ 和 $Y = Y^\nu \partial_\nu$ 的李括号可以表示为：
$$
[X, Y] = \sum_\sigma \left( \sum_\mu X^\mu \frac{\partial Y^\sigma}{\partial x^\mu} - Y^\mu \frac{\partial X^\sigma}{\partial x^\mu} \right) \partial_\sigma
$$
或更简洁地写作 $[X, Y]^\sigma = X(Y^\sigma) - Y(X^\sigma)$。我们可以利用这个公式来计算标架向量之间的[李括号](@entry_id:636461)，然后将其结果重新用标架 $\{e_k\}$ 表示，从而读出[结构函数](@entry_id:161908)。

考虑一个简单的例子 [@problem_id:999508]。在 $\mathbb{R}^2$ 上，令 $e_1 = \partial_x$，$e_2 = x\partial_x + \partial_y$。它们的[李括号](@entry_id:636461)为：
$$
[e_1, e_2] = [\partial_x, x\partial_x + \partial_y] = [\partial_x, x\partial_x] + [\partial_x, \partial_y] = (\partial_x(x))\partial_x + x[\partial_x, \partial_x] + 0 = \partial_x
$$
由于 $e_1 = \partial_x$，我们得到 $[e_1, e_2] = e_1$。与 $[e_1, e_2] = C^k_{12} e_k$ 比较，我们得到 $C^1_{12} = 1$ 和 $C^2_{12} = 0$。

[结构函数](@entry_id:161908)可以是常数，也可以是坐标的函数。例如，对于在 $\mathbb{R}^3$ 中的一个更复杂的标架 [@problem_id:999575]，计算 $[e_1, e_2]$ 后得到一个向量场 $-2\alpha \partial_z$。为了找到[结构函数](@entry_id:161908) $C^k_{12}$，我们需要将 $\partial_z$ 用 $\{e_1, e_2, e_3\}$ 表示出来，这又回到了基底变换的问题。完成这个变换后，我们就可以直接读出 $C^k_{12}$ 的表达式，它们可能是 $x,y,z$ 的函数。

一个特别富有启发性的例子是极坐标下的正交标架 [@problem_id:999563]。在 $\mathbb{R}^2 \setminus \{0\}$ 上，[坐标基](@entry_id:270149)底是 $\{\partial_r, \partial_\phi\}$。一个更自然的单位正交标架是 $E_r = \partial_r$ 和 $E_\phi = \frac{1}{r}\partial_\phi$。它们的[李括号](@entry_id:636461)是：
$$
[E_r, E_\phi] = [\partial_r, \frac{1}{r}\partial_\phi] = \partial_r(\frac{1}{r})\partial_\phi + \frac{1}{r}[\partial_r, \partial_\phi] = -\frac{1}{r^2}\partial_\phi = -\frac{1}{r} E_\phi
$$
这个非零的结果表明，即使是一个正交标架，如果它不是由一个[坐标系](@entry_id:156346)直接产生，它也通常是一个非[坐标基](@entry_id:270149)底。

### 非[坐标基](@entry_id:270149)底下的微积分

在[曲面](@entry_id:267450)上进行微积分的核心工具是 **协变导数 (covariant derivative)** $\nabla$。对于[坐标基](@entry_id:270149)底，协变导数的计算由[克里斯托费尔符号](@entry_id:159831) (Christoffel symbols) $\Gamma^k_{ij}$ 给出：$\nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k$。那么，在非[坐标基](@entry_id:270149)底中，我们如何定义和计算协变导数呢？

#### [联络系数](@entry_id:157618)

类似于[坐标基](@entry_id:270149)底的情况，我们在标架 $\{e_i\}$ 中定义 **[联络系数](@entry_id:157618) (connection coefficients)** $\Gamma^k_{ij}$ (有时也称为 **里奇旋转系数 (Ricci rotation coefficients)**) 如下：
$$
\nabla_{e_i} e_j = \Gamma^k_{ij} e_k
$$
这些系数 $\Gamma^k_{ij}$ 描述了[基向量](@entry_id:199546)场 $e_j$ 沿着另一个[基向量](@entry_id:199546)场 $e_i$ 方向的无穷小变化。**一个至关重要的概念是：即使在平坦空间（如[欧几里得空间](@entry_id:138052)，其曲率为零）中，只要使用的不是[笛卡尔坐标](@entry_id:167698)基底，[联络系数](@entry_id:157618)通常也不为零。**

让我们通过一个例子来阐明这一点 [@problem_id:999651]。考虑平坦的 $\mathbb{R}^2$ 和标架 $e_1 = \partial_x$, $e_2 = x\partial_x + \partial_y$。在平坦空间中使用笛卡尔坐标，对向量场 $Y = Y^x \partial_x + Y^y \partial_y$ 求协变导数 $\nabla_X Y$ 等同于对其分量求方向导数：$\nabla_X Y = (X(Y^x))\partial_x + (X(Y^y))\partial_y$。我们来计算 $\nabla_{e_2} e_2$：
$$
\begin{aligned}
\nabla_{e_2} e_2 = \nabla_{x\partial_x + \partial_y} (x\partial_x + \partial_y) \\
= ( (x\partial_x + \partial_y)(x) ) \partial_x + ( (x\partial_x + \partial_y)(1) ) \partial_y \\
= (x \cdot 1 + 0) \partial_x + (0) \partial_y \\
= x \partial_x = x e_1
\end{aligned}
$$
将结果与定义式 $\nabla_{e_2} e_2 = \Gamma^k_{22} e_k = \Gamma^1_{22} e_1 + \Gamma^2_{22} e_2$ 相比较，我们立即得到 $\Gamma^1_{22} = x$ 和 $\Gamma^2_{22} = 0$。这个非零的[联络系数](@entry_id:157618) $\Gamma^1_{22}=x$ 并非来自空间的弯曲，而是完全源于[基向量](@entry_id:199546) $e_2$ 自身随位置 $x$ 的变化。

#### 挠率与[Koszul公式](@entry_id:181356)

联络与李括号之间存在深刻的联系。这种联系通过 **[挠率张量](@entry_id:204137) (torsion tensor)** $T$ 来体现，其定义为：
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
这意味着[结构函数](@entry_id:161908)恰好是Levi-Civita联络系数的反对称部分。这揭示了[结构函数](@entry_id:161908)的几何意义：它们度量了沿着两个[基向量](@entry_id:199546)方向的平行移动路径所形成四边形的“不闭合”程度。

此外，对于一个度量兼容的联络（如Levi-Civita联络），[联络系数](@entry_id:157618)、度量分量和[结构函数](@entry_id:161908)三者可以通过 **[Koszul公式](@entry_id:181356)** 联系起来。在标架 $\{e_i\}$ 中，该公式的一种形式为：
$$
2 g(\nabla_{e_i} e_j, e_k) = e_i(g_{jk}) + e_j(g_{ik}) - e_k(g_{ij}) - g_{jm}C^m_{ik} - g_{im}C^m_{jk} + g_{km}C^m_{ij}
$$
这个公式在理论上极为重要，因为它表明，一旦我们知道了度量在标架中的分量 $g_{ij}$ 和标架的[结构函数](@entry_id:161908) $C^k_{ij}$，Levi-Civita联络就被唯一确定了。公式中的 $g([e_i, e_j], e_k) = g(C^m_{ij}e_m, e_k) = C^m_{ij}g_{mk}$ 等项直接体现了标架的非对易性对几何联络的贡献 [@problem_id:999508]。

### 进阶主题与应用

非[坐标基](@entry_id:270149)底的概念在现代[微分几何](@entry_id:145818)与理论物理中扮演着核心角色。

#### [Cartan结构方程](@entry_id:262185)

除了通过[李括号](@entry_id:636461)的定义来计算[结构函数](@entry_id:161908)，[Élie Cartan](@entry_id:263871) 发展了一套基于[微分形式](@entry_id:146747)的等价而 souvent 更为优雅的方法。**[Cartan第一结构方程](@entry_id:198919)** 将[余标架](@entry_id:637284)1-形式的外微分与[结构函数](@entry_id:161908)联系起来：
$$
d\theta^k = - \frac{1}{2} C^k_{ij} \theta^i \wedge \theta^j
$$
这个方程提供了一种计算[结构函数](@entry_id:161908)的[替代途径](@entry_id:182853)：首先计算出对偶基底 $\{\theta^k\}$，然后计算它们的外微分 $d\theta^k$，最后将结果与 $\theta^i \wedge \theta^j$ 进行比较，即可读出 $C^k_{ij}$。例如，在 [@problem_id:999697] 的设定中，通过计算[李括号](@entry_id:636461)我们得到 $[e_1, e_3] = e_2$，这意味着 $C^2_{13}=1$。我们也可以通过计算 $d\theta^2$ 并找到其在基底 $\theta^1 \wedge \theta^3$ 上的分量来验证这一结果。

#### 李群上的左不变标架

非[坐标基](@entry_id:270149)底的一个 canonical 应用场景是 **李群 (Lie groups)**。一个李群 $G$ 的[李代数](@entry_id:137954) $\mathfrak{g}$ 是其[单位元处的切空间](@entry_id:266468) $T_eG$。$\mathfrak{g}$ 中的任意一个向量 $v$ 都可以通过群的左乘操作唯一地扩展成 $G$ 上的一个 **[左不变向量场](@entry_id:637116) (left-invariant vector field)**。选取李代数的一组基底，我们就可以得到整个[李群](@entry_id:137659)上的一个左不变标架 $\{e_a\}$。

对于这样的标架，一个美妙的事实是其[结构函数](@entry_id:161908)是 **常数**，即 $C^k_{ij}$ 不依赖于群上的点。这些常数被称为李代数 $\mathfrak{g}$ 的 **[结构常数](@entry_id:157960) (structure constants)**。例如，对于 $SU(2)$ 群，其[李代数](@entry_id:137954) $\mathfrak{su}(2)$ 的[结构常数](@entry_id:157960)可以由[Levi-Civita符号](@entry_id:155382)给出：$C^k_{ab} = \epsilon_{abk}$ [@problem_id:999511]。

在李群上，我们可以定义具有附加性质的联络。例如，一个联络可能不是[无挠的](@entry_id:161664)。如果我们在[Levi-Civita联络](@entry_id:161107) $\nabla$ 的基础上增加一个张量场 $K$，定义新的联络 $\tilde{\nabla}_X Y = \nabla_X Y + K(X,Y)$，那么新[联络的挠率](@entry_id:192913) $\tilde{T}$ 就由 $K$ 的反对称部分决定：$\tilde{T}^k_{ij} = K^k_{ij} - K^k_{ji}$。这种构造在爱因斯坦-嘉当[引力](@entry_id:175476)理论和一些[规范场](@entry_id:159627)论中非常重要，它们允许时空具有挠率，而挠率与物质的[自旋密度](@entry_id:267742)相关联 [@problem_id:999511]。

同样，李代数的 Killing 型 $K_{ij} = C^l_{ik} C^k_{jl}$ 是一个重要的[不变量](@entry_id:148850)，它反映了李代数的结构。它的计算完全依赖于[结构常数](@entry_id:157960) [@problem_id:999560]。

综上所述，非[坐标基](@entry_id:270149)底或[标架场](@entry_id:160577)是超越了特定[坐标系](@entry_id:156346)限制的强大工具。它们通过[结构函数](@entry_id:161908)将基底的非对易性代数化，通过[联络系数](@entry_id:157618)将微积分推广到任意基底，并最终通过Cartan方程和在[李群](@entry_id:137659)上的应用，展现了微分几何深邃的代数-[几何对偶](@entry_id:204458)性。掌握非[坐标基](@entry_id:270149)底是深入理解广义相对论、规范场论以及现代几何学不可或缺的一步。