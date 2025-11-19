## 引言
在[微分几何](@entry_id:145818)与理论物理的研究中，我们常常需要描述和计算在弯曲空间或复杂[坐标系](@entry_id:156346)下的物理量。虽然[坐标基](@entry_id:270149)底提供了一种自然的方式，但它们往往与空间的内在几何结构不匹配，导致计算异常繁琐。为了克服这一局限性，数学家[Élie Cartan](@entry_id:263871)发展出一种更为强大和优雅的工具——**[活动标架法](@entry_id:175562) (method of moving frames)**，其核心便是**[标架场](@entry_id:160577) (frame fields)** 与**[余标架场](@entry_id:183575) (coframe fields)** 的概念。这种方法允许我们为[流形](@entry_id:153038)上的每一点选择一个最适合问题本身的[局部基](@entry_id:151573)底，从而将复杂的[微分几何](@entry_id:145818)问题转化为更直观的代数运算。

本文旨在系统地引导您掌握[活动标架法](@entry_id:175562)的理论与实践。我们将从基本原理出发，解决在任意基底下如何表示和计算张量的问题，最终揭示这一方法在计算[空间曲率](@entry_id:755140)等深刻[几何不变量](@entry_id:178611)时的惊人效率。
- 在**“原理和机制”**一章中，您将学习[标架场](@entry_id:160577)与[余标架场](@entry_id:183575)的定义、对偶性，以及如何利用它们计算张量分量。本章的重点是嘉当的两个[结构方程](@entry_id:274644)，它们是计算联络和曲率的基石。
- 随后的**“应用与交叉学科联系”**一章将展示这些工具的实际威力，通过来自广义相对论、运动学、甚至[李群](@entry_id:137659)理论的实例，说明如何选择恰当的标架来揭示物理和几何问题的本质。
- 最后，在**“动手实践”**部分，您将通过解决具体问题来巩固所学知识，将抽象的理论转化为扎实的计算技能。

通过学习本文，您将能够超越[坐标系](@entry_id:156346)的束缚，获得一个分析和理解几何与物理世界的全新视角。让我们从[标架场](@entry_id:160577)的基本定义开始，踏上这段探索之旅。

## 原理和机制

在[张量分析](@entry_id:161423)中，我们经常使用与特定[坐标系](@entry_id:156346)相关联的基底。例如，在[笛卡尔坐标](@entry_id:167698) $(x, y, z)$ 中，我们使用[基向量](@entry_id:199546) $\{\partial_x, \partial_y, \partial_z\}$ 和对偶基1-形式 $\{dx, dy, dz\}$。然而，将我们的分析局限于[坐标基](@entry_id:270149)底有时会带来不便，甚至在概念上有所限制。一个更通用、更强大的方法是引入**[标架场](@entry_id:160577) (frame fields)** 和**[余标架场](@entry_id:183575) (coframe fields)** 的概念。标架是在[流形](@entry_id:153038)的每个点上为[切空间](@entry_id:199137)选择的一个（通常是非坐标的）基底。这种方法，通常被称为**[活动标架法](@entry_id:175562) (method of moving frames)**，为研究[流形](@entry_id:153038)的几何性质（如联络和曲率）提供了一个极其优雅和高效的计算框架。

本章将系统地阐述[标架场](@entry_id:160577)和[余标架场](@entry_id:183575)的原理，并探讨它们在几何计算中的核心机制。

### [标架场](@entry_id:160577)与[余标架场](@entry_id:183575)：定义与对偶性

在 $n$ 维[流形](@entry_id:153038)上，一个**[标架场](@entry_id:160577)**是在[流形](@entry_id:153038)的一个开集上定义的一组 $n$ 个线性无关的向量场 $\{e_1, e_2, \dots, e_n\}$。在每一点 $p$，向量 $\{e_1(p), \dots, e_n(p)\}$ 构成了该点切空间 $T_p M$ 的一个基底。与之相对应，一个**[余标架场](@entry_id:183575)**是一组 $n$ 个线性无关的[1-形式](@entry_id:270392)场 $\{\theta^1, \theta^2, \dots, \theta^n\}$，在每一点 $p$ 构成了[余切空间](@entry_id:270516) $T_p^* M$ 的一个基底。

[标架场](@entry_id:160577)和[余标架场](@entry_id:183575)之间最重要的关系是**对偶性**。一个[余标架场](@entry_id:183575) $\{\theta^a\}$ 被称为[标架场](@entry_id:160577) $\{e_b\}$ 的**对偶**，如果它们满足以下关系：
$$
\theta^a(e_b) = \delta^a_b
$$
其中 $\delta^a_b$ 是克罗内克 δ 符号，当 $a=b$ 时为1，否则为0。这个关系意味着 $\theta^a$ 这个1-形式的作用是“提取”一个向量在 $e_a$ 方向上的分量。

与依赖于特定[坐标系](@entry_id:156346)的[坐标基](@entry_id:270149)底 $(\{\partial_i\}, \{dx^i\})$ 不同，[标架场](@entry_id:160577)可以根据问题的几何或物理特性进行自由选择。这为简化计算提供了极大的灵活性。

要从一个给定的[标架场](@entry_id:160577) $\{e_a\}$ 构建其对偶[余标架场](@entry_id:183575) $\{\theta^b\}$，我们通常先将标架向量用某个已知的[坐标基](@entry_id:270149)底 $\{\partial_i\}$ 表示出来，$e_a = E_a^i \partial_i$。然后，我们将待求的对偶1-形式也用对偶[坐标基](@entry_id:270149)底 $\{dx^j\}$ 表示，$\theta^b = \Theta^b_j dx^j$。通过应用对偶性条件，我们可以解出系数 $\Theta^b_j$。

例如，考虑二维欧几里得平面 $\mathbb{R}^2$，其标准坐标为 $(x, y)$。[坐标基](@entry_id:270149)底为 $\{\partial_x, \partial_y\}$。我们定义一个新的[标架场](@entry_id:160577) [@problem_id:1512323]：
$$
e_1 = \partial_x
$$
$$
e_2 = \partial_x + \partial_y
$$
为了找到其对偶[余标架](@entry_id:637284) $\{\theta^1, \theta^2\}$，我们设 $\theta^1 = A dx + B dy$ 和 $\theta^2 = C dx + D dy$。然后应用对偶性条件：
$$
\theta^1(e_1) = (A dx + B dy)(\partial_x) = A \cdot dx(\partial_x) + B \cdot dy(\partial_x) = A \cdot 1 + B \cdot 0 = 1 \implies A=1
$$
$$
\theta^1(e_2) = (A dx + B dy)(\partial_x + \partial_y) = A(1) + B(1) = A+B = 0 \implies B=-1
$$
因此，$\theta^1 = dx - dy$。同样地，对于 $\theta^2$：
$$
\theta^2(e_1) = (C dx + D dy)(\partial_x) = C = 0
$$
$$
\theta^2(e_2) = (C dx + D dy)(\partial_x + \partial_y) = C+D = 1 \implies D=1
$$
所以，$\theta^2 = dy$。这样，我们就找到了与给定[标架场](@entry_id:160577)对偶的[余标架场](@entry_id:183575)。

### 标架中的张量分量

一旦我们有了一对对偶的标架和[余标架](@entry_id:637284) $\{e_a\}$ 和 $\{\theta^a\}$，任何向量场 $V$ 和1-形式场 $\omega$ 都可以用它们作为基底进行分解：
$$
V = V^a e_a
$$
$$
\omega = \omega_a \theta^a
$$
（这里我们使用爱因斯坦求和约定，对重复的上下指标求和）。分量 $V^a$ 和 $\omega_a$ 可以通过与对偶基底配对来得到：
$$
V^a = \theta^a(V)
$$
$$
\omega_a = \omega(e_a)
$$
这一性质极大地简化了分量的计算。

让我们继续使用之前的例子 [@problem_id:1512258]。假设有一个向量场 $V = y \partial_x + x \partial_y$ 和一个[1-形式](@entry_id:270392)场 $\omega = x dx + y dy$。我们希望找到它们在标架 $\{e_1, e_2\}$ 和[余标架](@entry_id:637284) $\{\theta^1, \theta^2\}$ 中的分量 $(\tilde{V}^1, \tilde{V}^2)$ 和 $(\tilde{\omega}_1, \tilde{\omega}_2)$。

对于向量场 $V$，我们可以直接利用已知的对偶基底进行投影：
$$
\tilde{V}^1 = \theta^1(V) = (dx-dy)(y \partial_x + x \partial_y) = y \cdot dx(\partial_x) - x \cdot dy(\partial_y) = y-x
$$
$$
\tilde{V}^2 = \theta^2(V) = dy(y \partial_x + x \partial_y) = x \cdot dy(\partial_y) = x
$$
所以 $V = (y-x) e_1 + x e_2$。

对于1-形式场 $\omega$，我们将其作用在标架向量上：
$$
\tilde{\omega}_1 = \omega(e_1) = (x dx + y dy)(\partial_x) = x \cdot dx(\partial_x) = x
$$
$$
\tilde{\omega}_2 = \omega(e_2) = (x dx + y dy)(\partial_x + \partial_y) = x \cdot dx(\partial_x) + y \cdot dy(\partial_y) = x+y
$$
所以 $\omega = x \theta^1 + (x+y) \theta^2$。

这个过程可以推广到更高阶的张量。例如，一个度规张量 $g$ 在标架 $\{e_a\}$ 中的分量被定义为：
$$
g_{ab} = g(e_a, e_b)
$$
这在处理非正交标架时尤为重要。考虑一个由线元 $ds^2 = (dx)^{2} + 2\sinh(x) dx dy + \cosh^{2}(x) (dy)^{2}$ 定义的黎曼度规，以及一个非正交标架 [@problem_id:1512302]：
$$
e_1 = 3\partial_x
$$
$$
e_2 = \partial_x - \partial_y
$$
在[坐标基](@entry_id:270149)底中，度规分量为 $g_{xx}=1$, $g_{xy}=\sinh(x)$, $g_{yy}=\cosh^2(x)$。我们可以利用度规的双线性性质计算其在标架 $\{e_1, e_2\}$ 中的分量：
$$
g_{11} = g(3\partial_x, 3\partial_x) = 9 g(\partial_x, \partial_x) = 9 g_{xx} = 9
$$
$$
g_{12} = g(3\partial_x, \partial_x - \partial_y) = 3 g(\partial_x, \partial_x) - 3 g(\partial_x, \partial_y) = 3g_{xx} - 3g_{xy} = 3(1 - \sinh(x))
$$
$$
g_{22} = g(\partial_x - \partial_y, \partial_x - \partial_y) = g_{xx} - 2g_{xy} + g_{yy} = 1 - 2\sinh(x) + \cosh^2(x)
$$
我们可以看到，即使在一个平坦空间中（如果度规是欧几里得的），选择一个非正交的标架也会导致度规矩阵出现非对角元素。

### 正交[标架场](@entry_id:160577)

在[黎曼几何](@entry_id:160508)和物理学中，一个特别有用和重要的选择是**正交[标架场](@entry_id:160577) (orthonormal frame field)**。这是一个[标架场](@entry_id:160577) $\{e_a\}$，其向量在每一点都相互正交且长度为单位1。对于一个黎曼度规 $g$，这意味着：
$$
g(e_a, e_b) = \delta_{ab}
$$
在洛伦兹几何（如[狭义相对论](@entry_id:275552)）中，正交条件被推广为：
$$
g(e_a, e_b) = \eta_{ab}
$$
其中 $\eta_{ab}$ 是[闵可夫斯基度规](@entry_id:154660)的矩阵形式，通常为 $\text{diag}(-1, 1, 1, 1)$。在这种情况下，范数为-1的向量称为**类时 (timelike)** 向量，范数为+1的向量称为**类空 (spacelike)** 向量，范数为0的向量称为**类光 (null)** 向量。

正交标架的最大优势在于，[度规张量](@entry_id:160222)在其中的分量是常数（$\delta_{ab}$ 或 $\eta_{ab}$）。这使得张量分量的计算大大简化，许多微分几何的运算变成了类似欧几里得空间中的代数运算。

给定一个度规，我们通常可以通过类似于革兰-施密特[正交化](@entry_id:149208)的过程来构建一个正交[标架场](@entry_id:160577)。例如，考虑由[线元](@entry_id:196833) $ds^2 = dx^2 + (1+x^2)dy^2$ 定义的度规 [@problem_id:1512271]。[坐标基](@entry_id:270149)矢 $\partial_x$ 和 $\partial_y$ 是正交的（因为没有 $dx dy$ 交叉项），但它们的长度不是单位1。
$$
g(\partial_x, \partial_x) = 1
$$
$$
g(\partial_y, \partial_y) = 1+x^2
$$
为了构建一个正交标架 $\{e_1, e_2\}$，我们可以取 $e_1 = \partial_x$，因为它已经是单位向量。然后，我们需要将 $\partial_y$ [标准化](@entry_id:637219)：
$$
e_2 = \frac{1}{\sqrt{g(\partial_y, \partial_y)}} \partial_y = \frac{1}{\sqrt{1+x^2}} \partial_y
$$
这个标架 $\{e_1, e_2\}$ 现在是正交的，即 $g(e_a, e_b) = \delta_{ab}$。

在洛伦兹几何中，验证一个标架是否正交的过程是相似的，但需要注意符号 [@problem_id:1512294]。在二维[闵可夫斯基时空](@entry_id:156421) $ds^2 = -dt^2+dx^2$ 中，考虑标架：
$$
E_1 = \sinh(\alpha x) \partial_t + \cosh(\alpha x) \partial_x
$$
$$
E_2 = \cosh(\alpha x) \partial_t + \sinh(\alpha x) \partial_x
$$
其度规分量为 $g_{tt}=-1, g_{xx}=1, g_{tx}=0$。我们计算[内积](@entry_id:158127)：
$$
g(E_1, E_1) = \sinh^2(\alpha x) g(\partial_t, \partial_t) + \cosh^2(\alpha x) g(\partial_x, \partial_x) = -\sinh^2(\alpha x) + \cosh^2(\alpha x) = 1
$$
$$
g(E_2, E_2) = \cosh^2(\alpha x) g(\partial_t, \partial_t) + \sinh^2(\alpha x) g(\partial_x, \partial_x) = -\cosh^2(\alpha x) + \sinh^2(\alpha x) = -1
$$
$$
g(E_1, E_2) = \sinh(\alpha x)\cosh(\alpha x) g(\partial_t, \partial_t) + \cosh(\alpha x)\sinh(\alpha x) g(\partial_x, \partial_x) = -\sinh(\alpha x)\cosh(\alpha x) + \cosh(\alpha x)\sinh(\alpha x) = 0
$$
因此，$\{E_1, E_2\}$ 是一个正交标架，其中 $E_1$ 是类空的，$E_2$ 是类时的。

正交标架的计算优势在求值[1-形式](@entry_id:270392)对向量的作用时表现得淋漓尽致。考虑一个物理场景，其中速度场 $V$ 和[力场](@entry_id:147325)（表示为[1-形式](@entry_id:270392) $\alpha$）都用正交标架和[余标架](@entry_id:637284)表示 [@problem_id:1512256]。例如，在极坐标中，$e_{\hat{r}} = \partial_r$ 和 $e_{\hat{\theta}} = \frac{1}{r} \partial_\theta$ 构成一个正交标架。其对偶[余标架](@entry_id:637284)为 $\theta^{\hat{r}} = dr$ 和 $\theta^{\hat{\theta}} = r d\theta$。如果 $V = V^{\hat{r}} e_{\hat{r}} + V^{\hat{\theta}} e_{\hat{\theta}}$ 且 $\alpha = \alpha_{\hat{r}} \theta^{\hat{r}} + \alpha_{\hat{\theta}} \theta^{\hat{\theta}}$，那么力所做的功（功率）$\alpha(V)$ 的计算就非常简单：
$$
\alpha(V) = (\alpha_{\hat{r}} \theta^{\hat{r}} + \alpha_{\hat{\theta}} \theta^{\hat{\theta}})(V^{\hat{r}} e_{\hat{r}} + V^{\hat{\theta}} e_{\hat{\theta}}) = \alpha_{\hat{r}} V^{\hat{r}} + \alpha_{\hat{\theta}} V^{\hat{\theta}}
$$
这只是分量的[点积](@entry_id:149019)，因为 $\theta^{\hat{a}}(e_{\hat{b}}) = \delta^{\hat{a}}_{\hat{b}}$。

### [结构函数](@entry_id:161908)与[李括号](@entry_id:636461)

一个普遍的[标架场](@entry_id:160577) $\{e_a\}$ 与[坐标基](@entry_id:270149)底 $\{\partial_i\}$ 的一个根本区别是，标架向量场一般是“不可积”的。这意味着不存在一个[坐标系](@entry_id:156346) $(y^1, \dots, y^n)$ 使得 $e_a = \partial / \partial y^a$。衡量这种不可积性的工具是**[李括号](@entry_id:636461) (Lie bracket)**。两个向量场 $V$ 和 $W$ 的李括号 $[V, W]$ 本身也是一个向量场。对于[坐标基](@entry_id:270149)矢，我们总是有 $[\partial_i, \partial_j] = 0$，因为[偏导数](@entry_id:146280)可以交换次序。然而，对于一般的标架向量，[李括号](@entry_id:636461)通常非零。

这个[李括号](@entry_id:636461)的结果可以再次在标架基底中展开，定义了**[结构函数](@entry_id:161908) (structure functions)** $C^c_{ab}(x)$：
$$
[e_a, e_b] = C^c_{ab}(x) e_c
$$
[结构函数](@entry_id:161908)（也称为[结构常数](@entry_id:157960)，尽管它们通常是坐标的函数）捕获了[标架场](@entry_id:160577)内在的“扭曲”或“非交换性”。如果所有的[结构函数](@entry_id:161908)都为零，那么根据[弗罗贝尼乌斯定理](@entry_id:181858)，这个[标架场](@entry_id:160577)是可积的，即它是一个（至少是局部的）[坐标基](@entry_id:270149)底。

例如，考虑[标架场](@entry_id:160577) $e_1 = x \partial_x - y \partial_y$ 和 $e_2 = y \partial_x + x \partial_y$ [@problem_id:1512289]。我们可以计算它们的李括号 $[e_1, e_2]$。向量场 $V = V^i \partial_i$ 和 $W = W^j \partial_j$ 的[李括号](@entry_id:636461)的第 $k$ 个分量是 $[V,W]^k = V^i \partial_i W^k - W^i \partial_i V^k$。计算得到：
$$
[e_1, e_2] = (-2y) \partial_x + (2x) \partial_y
$$
然后，我们需要将这个结果表示为 $e_1$ 和 $e_2$ 的[线性组合](@entry_id:154743)来找到[结构函数](@entry_id:161908)：
$$
(-2y) \partial_x + (2x) \partial_y = C^1_{12} (x \partial_x - y \partial_y) + C^2_{12} (y \partial_x + x \partial_y)
$$
通过在 $(x,y)$ 处求解这个[线性方程组](@entry_id:148943)，我们得到 $C^1_{12}(x,y) = -\frac{4xy}{x^2+y^2}$ 和 $C^2_{12}(x,y) = \frac{2(x^2-y^2)}{x^2+y^2}$。这些非零的[结构函数](@entry_id:161908)证实了该[标架场](@entry_id:160577)不是一个[坐标基](@entry_id:270149)底。

在[余标架](@entry_id:637284)的语言中，同样的信息被包含在1-形式的外微分中。它与[结构函数](@entry_id:161908)的关系由**[嘉当第一结构方程](@entry_id:186381) (Cartan's first structure equation)** 的一个简化版本给出：
$$
d\theta^c = -\frac{1}{2} C^c_{ab} \theta^a \wedge \theta^b
$$
这个方程表明，[余标架场](@entry_id:183575)的外微分可以完全由这些[1-形式](@entry_id:270392)本身和[结构函数](@entry_id:161908)来表示。例如，对于[余标架](@entry_id:637284) $\theta^1 = \exp(z) dx - y dz, \theta^2 = \exp(z) dy, \theta^3 = dz$ [@problem_id:1512260]，我们可以计算 $d\theta^1$：
$$
d\theta^1 = d(\exp(z) dx) - d(y dz) = (\exp(z) dz \wedge dx) - (dy \wedge dz)
$$
然后将 $dx, dy, dz$ 用 $\{\theta^a\}$ 表示回来，我们发现 $d\theta^1 = -\theta^1 \wedge \theta^3 - \exp(-z) \theta^2 \wedge \theta^3$。通过与 $d\theta^1 = C^1_{12}\theta^1\wedge\theta^2 + C^1_{13}\theta^1\wedge\theta^3 + C^1_{23}\theta^2\wedge\theta^3$（利用[反对称性](@entry_id:261893) $C^1_{ab} = -C^1_{ba}$）进行比较，我们可以读出[结构函数](@entry_id:161908)，例如 $C^1_{23} = -\exp(-z)$。

### [嘉当结构方程](@entry_id:162100)：[联络与曲率](@entry_id:158520)

[活动标架法](@entry_id:175562)的真正威力在于它提供了一种计算联络和曲率的系统方法。这是通过嘉当的两个[结构方程](@entry_id:274644)实现的。

#### 第一[结构方程](@entry_id:274644)与[联络1-形式](@entry_id:275839)

为了描述标架向量如何从一点变化到另一点，我们引入**[联络1-形式](@entry_id:275839) (connection 1-forms)** $\omega^a{}_b$。这些1-形式编码了关于[协变导数](@entry_id:152476)的信息。[嘉当第一结构方程](@entry_id:186381)将[余标架](@entry_id:637284)的[外微分](@entry_id:161900)与[联络1-形式](@entry_id:275839)联系起来。对于一个无挠（torsion-free）联络，如黎曼几何中的[列维-奇维塔联络](@entry_id:161107)，方程为：
$$
d\theta^a + \omega^a{}_b \wedge \theta^b = 0
$$
这个方程是一个核心方程：它允许我们通过求解一个[代数方程](@entry_id:272665)组来确定[联络1-形式](@entry_id:275839)。给定一个[余标架场](@entry_id:183575) $\{\theta^a\}$，我们计算它的[外微分](@entry_id:161900) $d\theta^a$，然后找到一组 $\omega^a{}_b$ 使得上述方程成立。

对于一个正交标架，[度规兼容性](@entry_id:265910)条件（即协变导数作用于度规为零）施加了一个重要的约束：[联络1-形式](@entry_id:275839)矩阵 $(\omega_{ab})$ 是反对称的，其中 $\omega_{ab} = \eta_{ac}\omega^c{}_b$。这意味着 $\omega_{ab} = -\omega_{ba}$。在黎曼情况下（$\eta_{ab} = \delta_{ab}$），这简化为 $\omega^a{}_b = -\omega^b{}_a$。这大大减少了需要求解的独立分量的数量。

让我们看一个具体的计算 [@problem_id:1512274]。在一个[二维流形](@entry_id:188198)上，给定一个正交[余标架](@entry_id:637284) $\theta^1 = du$ 和 $\theta^2 = u \, dv$。由于是二维正交标架，反对称性意味着 $\omega^1{}_1 = \omega^2{}_2 = 0$ 且 $\omega^2{}_1 = -\omega^1{}_2$。我们只需要求解一个独立的[联络1-形式](@entry_id:275839) $\omega^1{}_2$。
[结构方程](@entry_id:274644)为：
1.  对于 $a=1$: $d\theta^1 + \omega^1{}_2 \wedge \theta^2 = 0$
2.  对于 $a=2$: $d\theta^2 + \omega^2{}_1 \wedge \theta^1 = 0 \implies d\theta^2 - \omega^1{}_2 \wedge \theta^1 = 0$

首先，计算外微分：$d\theta^1 = d(du) = 0$，$d\theta^2 = d(u \, dv) = du \wedge dv$。
从方程1，$0 + \omega^1{}_2 \wedge (u \, dv) = 0$。这表明 $\omega^1{}_2$ 不能有 $du$ 分量，否则楔积将不为零。因此 $\omega^1{}_2$ 必须正比于 $dv$，我们设 $\omega^1{}_2 = f(u,v) \, dv$。

现在代入方程2：$du \wedge dv - (f \, dv) \wedge du = 0$。利用 $dv \wedge du = -du \wedge dv$，这变成 $(1+f) du \wedge dv = 0$。因此 $f=-1$。我们得出结论：
$$
\omega^1{}_2 = -dv
$$
这个例子完美地展示了[活动标架法](@entry_id:175562)的威力：通过纯粹的代数和外微分运算，我们就确定了空间的联络。

#### 第二[结构方程](@entry_id:274644)与[曲率2-形式](@entry_id:187677)

一旦我们知道了联络，下一步就是计算曲率。曲率描述了沿无穷小闭环平行移动一个向量时所产生的变化，它度量了空间的内在弯曲程度。在[活动标架](@entry_id:175562)的语言中，曲率由**[曲率2-形式](@entry_id:187677) (curvature 2-forms)** $\Omega^a{}_b$ 描述。它们由**[嘉当第二结构方程](@entry_id:196278)**定义：
$$
\Omega^a{}_b = d\omega^a{}_b + \omega^a{}_c \wedge \omega^c{}_b
$$
这个方程的结构与物理学中的杨-米尔斯场强公式非常相似，它表明曲率是联络的“场强”。

让我们完成之前的计算，并找出曲率 [@problem_id:1512285]。假设在一个[二维流形](@entry_id:188198)上，我们有一个正交[余标架](@entry_id:637284) $\theta^1=du, \theta^2 = \exp(-u^2/2) dv$，并且通过求解第一[结构方程](@entry_id:274644)我们已经得到了唯一的非零独立[联络1-形式](@entry_id:275839) $\omega^1{}_2 = u \exp(-u^2/2) dv$。
在二维情况下，第二[结构方程](@entry_id:274644)简化为：
$$
\Omega^1{}_2 = d\omega^1{}_2 + \omega^1{}_1 \wedge \omega^1{}_2 + \omega^1{}_2 \wedge \omega^2{}_2
$$
由于正交性，对角项为零，所以 $\Omega^1{}_2 = d\omega^1{}_2$。我们只需计算 $\omega^1{}_2$ 的[外微分](@entry_id:161900)：
$$
d\omega^1{}_2 = d(u \exp(-u^2/2) dv) = \frac{d}{du}(u \exp(-u^2/2)) du \wedge dv
$$
$$
= (1 \cdot \exp(-u^2/2) + u \cdot (-u \exp(-u^2/2))) du \wedge dv
$$
$$
= (1 - u^2) \exp(-u^2/2) du \wedge dv
$$
所以，$\Omega^1{}_2 = (1 - u^2) \exp(-u^2/2) du \wedge dv$。

[曲率2-形式](@entry_id:187677)的一个美妙之处在于它可以与[流形](@entry_id:153038)的[面积元](@entry_id:263205)联系起来。在这个例子中，[面积元](@entry_id:263205)是 $\theta^1 \wedge \theta^2 = du \wedge (\exp(-u^2/2) dv) = \exp(-u^2/2) du \wedge dv$。将我们的结果与[面积元](@entry_id:263205)进行比较：
$$
\Omega^1{}_2 = (1-u^2) (\exp(-u^2/2) du \wedge dv) = (1-u^2) \theta^1 \wedge \theta^2
$$
在二维黎曼几何中，[曲率2-形式](@entry_id:187677)与[高斯曲率](@entry_id:149725) $K$ 的关系是 $\Omega^1{}_2 = K \, \theta^1 \wedge \theta^2$。因此，我们直接读出高斯曲率为：
$$
K(u,v) = 1 - u^2
$$
这个结果展示了[嘉当结构方程](@entry_id:162100)的终极力量：它们提供了一个直接而系统的算法，从一个选择的（通常是正交的）[标架场](@entry_id:160577)出发，通过外微分和代数运算，便可计算出空间的联络和曲率这些最深刻的[几何不变量](@entry_id:178611)。