## 引言
在物理学和几何学的探索中，一个基本原则是自然法则的表达形式不应依赖于我们碰巧选择的观测视角或[坐标系](@entry_id:156346)。在平直的欧几里得空间中，矢量和微积分的传统工具足以应对，然而，当我们将目光投向更广阔的领域——如广义相对论中由物质和能量决定的[弯曲时空](@entry_id:159822)，或现代微分几何中的抽象[流形](@entry_id:153038)时——这些经典工具便显得力不从心。普通导数在坐标变换下会产生不符合物理规律的“杂项”，这揭示了一个深刻的知识鸿沟：我们缺乏一种能够在弯曲空间上进行[一致性分析](@entry_id:189411)的普适数学语言。

为了填补这一鸿沟，数学家和物理学家发展出了张量场理论。张量场是矢量和标量概念的终极推广，它们是内蕴于[流形](@entry_id:153038)几何结构之中的对象，其定义从根本上保证了[坐标无关性](@entry_id:159715)。掌握张量场，就如同掌握了一门描述弯曲世界的通用语言，它使得我们能够精确地表述从时空曲率到物质行为的各种物理现象，而无需担心[坐标系](@entry_id:156346)选择所带来的含糊不清。

本文将引导您系统地学习这门强大的语言。在第一章**原理与机制**中，我们将从坐标变换的挑战出发，建立张量的严格定义，探索[张量代数](@entry_id:161671)的基本运算，并引入[协变导数](@entry_id:152476)和[李导数](@entry_id:171745)等关键的[微分](@entry_id:158718)工具。随后，在第二章**应用与跨学科联系**中，我们将看到这些理论如何在广义相对论、宇宙学、经典力学等多个领域大放异彩，成为连接抽象数学与物理现实的桥梁。最后，通过**动手实践**环节，您将有机会运用所学知识解决具体问题，从而加深理解并巩固技能。让我们开始这段探索之旅，揭开[流形](@entry_id:153038)上张量场的奥秘。

## 原理与机制

在上一章中，我们介绍了[光滑流形](@entry_id:160799)作为推广欧几里得空间概念的数学框架。[流形](@entry_id:153038)在局部上类似于[欧几里得空间](@entry_id:138052)，但其全局结构可能远为复杂。为了在这些弯曲的空间上描述物理定律和几何属性，我们需要发展一套新的数学语言，这套语言的核心就是张量场。物理定律的表达形式不应依赖于我们碰巧选择的特定[坐标系](@entry_id:156346)。张量正是为满足这一“[坐标无关性](@entry_id:159715)”或“协变性”原则而设计的数学对象。本章将深入探讨[张量场](@entry_id:190170)的核心原理与基本机制。

### 坐标变换与张量的必要性

我们从最简单的场——标量场开始。一个**[标量场](@entry_id:151443)** (scalar field) 是[流形](@entry_id:153038)上每个点赋予一个实数的函数，例如温度[分布](@entry_id:182848)或势能。考虑一个在二维平面 $\mathbb{R}^2$ 上的标量场，其在[笛卡尔坐标](@entry_id:167698) $(x,y)$ 下的表达式为 $f(x,y)$。如果我们切换到另一套[坐标系](@entry_id:156346)，比如极坐标 $(r, \theta)$，其中 $x = r \cos(\theta)$ 且 $y = r \sin(\theta)$，那么同一个物理点 $P$ 的坐标会改变，但标量场在该点的值必须保持不变。这意味着新的函数表达式 $\tilde{f}(r, \theta)$ 必须满足 $\tilde{f}(r, \theta) = f(x(r,\theta), y(r,\theta))$。例如，一个在[笛卡尔坐标](@entry_id:167698)下形式复杂的标量场 $f(x,y) = (x^2 - y^2)^2 + 4x^2y^2$，在代入极[坐标变换](@entry_id:172727)后，其表达式惊人地简化为 $\tilde{f}(r, \theta) = r^4$ ([@problem_id:1667573])。这阐明了一个核心思想：标量的值是内在的、几何的，而其函数表达式则依赖于[坐标系](@entry_id:156346)的选择。

接下来，我们考虑矢量场。一个**矢量场** (vector field) 在[流形](@entry_id:153038)的每一点指定一个切矢量。在[局部坐标系](@entry_id:751394) $(x^1, \dots, x^n)$ 中，一个切矢量 $V$ 可以写成分量的线性组合 $V = V^i \frac{\partial}{\partial x^i}$，其中 $\{\frac{\partial}{\partial x^i}\}$ 是[坐标基](@entry_id:270149)矢。如果切换到新的[坐标系](@entry_id:156346) $(x'^1, \dots, x'^n)$，根据[链式法则](@entry_id:190743)，[基矢](@entry_id:199546)的变换关系为 $\frac{\partial}{\partial x^i} = \frac{\partial x'^j}{\partial x^i} \frac{\partial}{\partial x'^j}$。为了使矢量 $V$ 本身保持不变，其分量必须以一种“反变”的方式进行变换：
$$
V'^j = \frac{\partial x'^j}{\partial x^i} V^i
$$
这种变换法则确保了 $V = V^i \frac{\partial}{\partial x^i} = V^i (\frac{\partial x'^j}{\partial x^i} \frac{\partial}{\partial x'^j}) = (\frac{\partial x'^j}{\partial x^i} V^i) \frac{\partial}{\partial x'^j} = V'^j \frac{\partial}{\partial x'^j}$，即矢量作为一个几何对象的独立性。遵循这种变换规则的矢量称为**逆变矢量** (contravariant vector)。

现在，一个自然的问题出现了：我们能否像在普通微积分中那样，通过对矢量场的分量求偏导数来分析其变化？让我们考察对象 $M^i_{\ j} = \frac{\partial V^i}{\partial x^j}$ 的变换性质。如果我们天真地假设它像一个张量那样变换，那么在新[坐标系](@entry_id:156346)中的分量 $M'^{k}_{\ l}$ 应该满足特定的[张量变换法则](@entry_id:185176)。然而，通过直接计算可以揭示一个深刻的问题。在新[坐标系](@entry_id:156346)中，我们有 $V'^k = \frac{\partial x'^k}{\partial x^i} V^i$。对这个表达式关于新坐标 $x'^l$求偏导，并应用链式法则和乘法法则：
$$
\frac{\partial V'^k}{\partial x'^l} = \frac{\partial}{\partial x'^l} \left( \frac{\partial x'^k}{\partial x^i} V^i \right) = \frac{\partial x^j}{\partial x'^l} \frac{\partial}{\partial x^j} \left( \frac{\partial x'^k}{\partial x^i} V^i \right) = \frac{\partial x^j}{\partial x'^l} \left( \frac{\partial^2 x'^k}{\partial x^j \partial x^i} V^i + \frac{\partial x'^k}{\partial x^i} \frac{\partial V^i}{\partial x^j} \right)
$$
整理后得到：
$$
\frac{\partial V'^k}{\partial x'^l} = \frac{\partial x'^k}{\partial x^i} \frac{\partial x^j}{\partial x'^l} \frac{\partial V^i}{\partial x^j} + \frac{\partial^2 x'^k}{\partial x^i \partial x^j} \frac{\partial x^j}{\partial x'^l} V^i
$$
这个结果表明，$\frac{\partial V'^k}{\partial x'^l}$ 不仅仅是旧分量 $\frac{\partial V^i}{\partial x^j}$ 的线性组合。它还包含一个额外的项，这个项与坐标变换的[二阶导数](@entry_id:144508)有关。这意味着对象 $\frac{\partial V^i}{\partial x^j}$ 的分量**不遵循[张量变换法则](@entry_id:185176)**，因此它不是一个张量。

一个具体的例子可以很好地说明这一点。在[二维流形](@entry_id:188198)上，考虑坐标变换 $x' = x^2, y' = y$ 和矢量场 $V^x = y, V^y = x$。如果我们假设偏导数矩阵 $M^i_j = \frac{\partial V^i}{\partial x^j}$ 按照 (1,1) 型张量的规则进行变换，我们会得到一个结果 $T^{x'}_{x'}$。然而，如果我们先将矢量场 $V$ 的分量变换到新[坐标系](@entry_id:156346)，得到 $V'^{x'}(x', y')$，然后再直接对新坐标求导，会得到另一个结果 $D^{x'}_{x'} = \frac{\partial V'^{x'}}{\partial x'}$。计算表明，这两个结果并不相等，它们的差值 $D^{x'}_{x'} - T^{x'}_{x'}$ 在一般情况下不为零 ([@problem_id:1856094])。这个“失败”是至关重要的，它揭示了在弯曲空间或任意[坐标系](@entry_id:156346)中，简单的偏导数不再具有良好的几何意义。为了修正这一点，我们需要引入一种新的导数——[协变导数](@entry_id:152476)，而这正是[张量分析](@entry_id:161423)的核心动机之一。

### 张量的严格定义

为了克服上述困难，我们需要一个不依赖于[坐标系](@entry_id:156346)的、更加根本的张量定义。

#### 从[多重线性映射](@entry_id:274221)的视角

现代[微分几何](@entry_id:145818)将张量定义为[切空间](@entry_id:199137)上的[多重线性映射](@entry_id:274221)。在[流形](@entry_id:153038) $M$ 的每一点 $p$，我们有一个**[切空间](@entry_id:199137)** (tangent space) $T_pM$，它是由所有在该点作用于光滑函数的“方向导数”或“导子”构成的矢量空间。在局部坐标系 $(x^1, \dots, x^n)$ 下，[切空间](@entry_id:199137) $T_pM$ 的一组自然基底由[偏导数](@entry_id:146280)算符 $\{\frac{\partial}{\partial x^1}|_p, \dots, \frac{\partial}{\partial x^n}|_p\}$ 构成。

与每个矢量空间 $V$ 相关联的是其**对偶空间** (dual space) $V^*$，它由 $V$ 上的所有线性实值函数构成。切空间 $T_pM$ 的对偶空间被称为**[余切空间](@entry_id:270516)** (cotangent space)，记作 $T_p^*M$。它的元素被称为**[余矢量](@entry_id:157727)** (covectors) 或**1-形式** (1-forms)。给定 $T_pM$ 的[坐标基](@entry_id:270149)底 $\{\partial_j = \frac{\partial}{\partial x^j}|_p\}$，存在一个唯一的对偶基底 $\{dx^1|_p, \dots, dx^n|_p\} \subset T_p^*M$，其定义满足关系 $dx^i(\partial_j) = \delta^i_j$，其中 $\delta^i_j$ 是克罗内克符号 ([@problem_id:2992321])。一个余矢量 $\omega \in T_p^*M$ 可以表示为 $\omega = \omega_i dx^i$。它的分量变换法则可以通过保持标量 $\omega(V) = \omega_i V^i$ 在[坐标变换](@entry_id:172727)下的不变性来导出，结果为：
$$
\omega'_j = \frac{\partial x^i}{\partial x'^j} \omega_i
$$
这种变换方式被称为**协变** (covariant)。值得注意的是，虽然 $T_pM$ 和 $T_p^*M$ 都是 $n$ 维矢量空间，因而彼此同构，但在[流形](@entry_id:153038)上并没有一个独立于额外结构（如度规）的“自然”或“典则”同构 ([@problem_id:2992321])。

基于此，我们可以给出张量的普适定义：在点 $p$ 的一个 **$(k,l)$ 型张量** (tensor of type $(k,l)$) $T$ 是一个[多重线性映射](@entry_id:274221)，它取 $k$ 个余矢量和 $l$ 个切矢量作为输入，并输出一个实数：
$$
T: \underbrace{T_p^*M \times \dots \times T_p^*M}_{k \text{ times}} \times \underbrace{T_pM \times \dots \times T_pM}_{l \text{ times}} \to \mathbb{R}
$$
根据这个定义：
- 一个 **(0,0) 型张量**是一个不接受任何矢量输入的映射，即一个标量。
- 一个 **(1,0) 型张量**是一个映射 $T: T_p^*M \to \mathbb{R}$。根据对偶空间的性质，这等价于 $T_pM$ 中的一个矢量。
- 一个 **(0,1) 型张量**是一个映射 $T: T_pM \to \mathbb{R}$，即 $T_p^*M$ 中的一个余矢量。
- 一个 **(0,2) 型张量** $T$ 是一个[双线性映射](@entry_id:186502) $T: T_pM \times T_pM \to \mathbb{R}$。它取两个矢量 $X, Y \in T_pM$ 并返回一个数 $T(X,Y)$。例如，一个在坐标 $(u,v)$ 下由[双线性形式](@entry_id:746794) $T_p(X, Y) = \exp(u) X^1 Y^1 - uv(X^1 Y^2 + X^2 Y^1) + \exp(-v) X^2 Y^2$ 定义的张量，就是一个具体的 (0,2) 型张量 ([@problem_id:1543252])。

将一个张量作用于[基矢](@entry_id:199546)和对偶[基矢](@entry_id:199546)，可以得到它的分量。例如，对于一个 $(1,2)$ 型张量 $T$，其分量为 $T^i_{jk} = T(dx^i, \partial_j, \partial_k)$。

#### 从分量变换的视角

这个抽象定义与更经典的、基于分量变换的定义是等价的。一个 $(k,l)$ 型张量可以由它在一组[坐标系](@entry_id:156346)中的分量 $T^{i_1 \dots i_k}_{j_1 \dots j_l}$ 来确定。当[坐标系](@entry_id:156346)从 $x$ 变换到 $x'$ 时，这些分量必须遵循以下变换法则：
$$
T'^{i'_1 \dots i'_k}_{j'_1 \dots j'_l} = \left( \frac{\partial x'^{i'_1}}{\partial x^{i_1}} \dots \frac{\partial x'^{i'_k}}{\partial x^{i_k}} \right) \left( \frac{\partial x^{j_1}}{\partial x'^{j'_1}} \dots \frac{\partial x^{j_l}}{\partial x'^{j'_l}} \right) T^{i_1 \dots i_k}_{j_1 \dots j_l}
$$
这里，每个[逆变](@entry_id:192290)指标（上标）都带有一个“正向”的雅可比矩阵因子 $\frac{\partial x'}{\partial x}$，而每个[协变](@entry_id:634097)指标（下标）都带有一个“逆向”的[雅可比矩阵](@entry_id:264467)因子 $\frac{\partial x}{\partial x'}$ ([@problem_id:2992321])。这个复杂的公式精确地保证了当我们用张量 $T$ 及其分量，去“吃掉”相应数量的[协变](@entry_id:634097)和逆变矢量的分量时，最终得到的结果是一个标量，其值与[坐标系](@entry_id:156346)无关。

将这两种观点结合起来，我们便获得了对张量的完整理解：它既是抽象的几何对象（[多重线性映射](@entry_id:274221)），又具有在不同[坐标系](@entry_id:156346)下表现良好、可供计算的分量。一个**张量场** (tensor field) 就是在[流形](@entry_id:153038) $M$ 的每一点 $p$ 都指定一个该点上的张量，并且其分量在任何[局部坐标系](@entry_id:751394)中都是[光滑函数](@entry_id:267124)。

### [张量代数](@entry_id:161671)：构建与操作[张量场](@entry_id:190170)

一旦定义了张量，我们就可以通过代数运算来组合和操纵它们。

#### [张量积](@entry_id:140694)

最基本的构建操作是**[张量积](@entry_id:140694)** (tensor product)，用符号 $\otimes$ 表示。它允许我们从低阶张量构建[高阶张量](@entry_id:200122)。例如，给定两个 [1-形式](@entry_id:270392)（(0,1)型张量）$\alpha$ 和 $\beta$，它们的张量积 $\alpha \otimes \beta$ 是一个 (0,2) 型张量，其定义为：
$$
(\alpha \otimes \beta)(V, W) = \alpha(V) \beta(W)
$$
其中 $V, W$ 是任意两个切矢量。在分量层面，如果 $\alpha = \alpha_i dx^i$ 和 $\beta = \beta_j dx^j$，那么 $T = \alpha \otimes \beta$ 的分量就是 $T_{ij} = \alpha_i \beta_j$。例如，在 $\mathbb{R}^3$ 中，[1-形式](@entry_id:270392) $\alpha = dz$ (分量为 $\alpha_z=1$, 其他为0) 和 $\beta = x\,dy$ (分量为 $\beta_y=x$, 其他为0) 的[张量积](@entry_id:140694) $T = \alpha \otimes \beta$ 是一个 (0,2) 型张量，其唯一非零分量是 $T_{zy} = \alpha_z \beta_y = x$ ([@problem_id:1667532])。

#### 缩并

与[张量积](@entry_id:140694)相反的操作是**缩并** (contraction)，它通过选取一个逆变指标和一个[协变](@entry_id:634097)指标，并将它们相加（遵循爱因斯坦求和约定）来降低张量的阶。这个操作的结果是一个新的、阶数减少了 (1,1) 的张量。

最常见的缩并例子是 (1,1) 型张量 $F$ 的**迹** (trace)。在[局部坐标](@entry_id:181200)中，其分量为 $F^i_j$，其迹定义为 $\text{tr}(F) = F^i_i = F^1_1 + F^2_2 + \dots + F^n_n$。迹是一个标量场，这意味着它的值在[坐标变换](@entry_id:172727)下是不变的。例如，如果一个 (1,1) 型张量在[笛卡尔坐标](@entry_id:167698) $(x,y)$ 下的迹为 $\text{tr}(F) = x^2 + xy$，我们可以通过坐标代换 $x = \frac{u+v}{2}, y = \frac{u-v}{2}$ 找到它在另一[坐标系](@entry_id:156346) $(u,v)$ 下的表达式，而无需重新计算[张量变换](@entry_id:183453) ([@problem_id:1543245])。

另一个基本的缩并是对一个 1-形式 $\omega$ 和一个矢量场 $X$ 进行配对。结果是一个标量场 $f(p) = \omega_p(X_p)$。在[局部坐标](@entry_id:181200)中，这表现为 $f = \omega_i X^i$。由于 $\omega$ 和 $X$ 都是光滑[张量场](@entry_id:190170)，它们的缩并结果也是一个光滑的标量场 ([@problem_id:2992321])。

#### 对称化操作

对于具有多个相同类型指标的张量，我们可以定义对称化和反对称化操作。一个 (0,2) 型张量 $T$ 的分量为 $T_{ij}$。它可以唯一地分解为一个**对称部分** (symmetric part) $S$ 和一个**斜对称（或反对称）部分** (skew-symmetric part) $A$：
$$
T_{ij} = S_{ij} + A_{ij}
$$
其中，
$$
S_{ij} = \frac{1}{2}(T_{ij} + T_{ji})
$$
$$
A_{ij} = \frac{1}{2}(T_{ij} - T_{ji})
$$
通过定义可知，$S$ 是对称的（$S_{ij} = S_{ji}$），而 $A$ 是斜对称的（$A_{ij} = -A_{ji}$）。这个分解在物理和几何中非常重要，例如，电磁场张量就是一个 (0,2) 型的[斜对称张量](@entry_id:199349)。对于一个给定的张量，例如在 $\mathbb{R}^2$ 中分量为 $T_{xy} = x^2+y$ 和 $T_{yx} = -x^2+y$ 的张量，我们可以直接应用这些公式计算其对称和斜对称部分的分量，如 $S_{xy}=y$ 和 $A_{xy}=x^2$ ([@problem_id:1667537])。

### 度规张量：赋予[流形](@entry_id:153038)几何结构

在所有[张量场](@entry_id:190170)中，有一类尤为重要，它赋予[流形](@entry_id:153038)以几何概念，如长度、角度和体积。这就是**[度规张量](@entry_id:160222)** (metric tensor)。

一个度规张量 $g$ 是一个光滑的、对称的、非退化的 (0,2) 型张量场。
- **对称性**意味着对于任意矢量场 $X, Y$，都有 $g(X, Y) = g(Y, X)$。
- **非退化性**意味着如果对于某个矢量 $X_p$，有 $g_p(X_p, Y_p) = 0$ 对所有矢量 $Y_p \in T_pM$ 都成立，那么必有 $X_p = 0$。这等价于说度规张量的分量矩阵 $[g_{ij}]$ 在任何[坐标系](@entry_id:156346)下都是可逆的。

根据 $g$ 的一个附加属性，我们将度规分为两类 ([@problem_id:2992334])：
1.  **黎曼度规 (Riemannian Metric):** 如果 $g$ 是正定的，即对于任意非[零矢量](@entry_id:155273)场 $X$，恒有 $g(X, X) > 0$，则称 $g$ 为黎曼度规。拥有黎曼度规的[流形](@entry_id:153038)称为[黎曼流形](@entry_id:261160)。这推广了欧几里得几何，允许我们定义弧长、角度和体积。在[黎曼流形](@entry_id:261160)的每个[切空间](@entry_id:199137) $T_pM$ 中，[单位球](@entry_id:142558)面 $\{v \in T_pM : g_p(v,v)=1\}$ 是一个紧集 ([@problem_id:2992334])。
2.  **伪黎曼度规 (Pseudo-Riemannian Metric):** 如果 $g$ 是非退化的但不定（即存在 $X$ 和 $Y$ 使得 $g(X,X) > 0$ 和 $g(Y,Y)  0$），则称 $g$ 为伪黎曼度规。最著名的例子是广义相对论中的[洛伦兹度规](@entry_id:184391)，其符号差为 $(+,-,-,-)$ 或 $(-,+,+,+)$。在[伪黎曼流形](@entry_id:184750)中，矢量可以根据其“长度”的平方的符号分为类时、类空和[类光矢量](@entry_id:155273)。这导致了因果结构等更为丰富的物理概念，但也意味着 $g(X,X)$ 的平方根不能直接用作定义距离函数，因为它可以为零或虚数 ([@problem_id:2992334])。

度规张量的一个关键作用是建立切空间 $T_pM$ 和其对偶空间 $T_p^*M$ 之间的联系。通过度规，我们可以定义所谓的“[音乐同构](@entry_id:199976)”：
- **[降指标](@entry_id:272166) (flat, $\flat$)**: 将一个矢量 $V$ 映射到一个 1-形式 $V^\flat$，定义为 $V^\flat(W) = g(V, W)$ 对所有矢量 $W$ 成立。在坐标中，这表现为 $(\alpha_V)_i = g_{ij}V^j$。
- **[升指标](@entry_id:265340) (sharp, $\sharp$)**: 将一个 1-形式 $\omega$ 映射到一个矢量 $\omega^\sharp$，定义为满足 $g(\omega^\sharp, W) = \omega(W)$ 对所有矢量 $W$ 成立的唯一矢量。在坐标中，这表现为 $(\omega^\sharp)^i = g^{ij}\omega_j$，其中 $g^{ij}$ 是度规矩阵 $g_{ij}$ 的[逆矩阵](@entry_id:140380)分量。

这些同构的存在性和光滑性正是度规非退化性的直接后果 ([@problem_id:2992334])。它们允许我们在[逆变和协变张量](@entry_id:197629)之间自由转换，是张量计算中不可或缺的工具。

### 张量场的[微分](@entry_id:158718)

我们回到本章开头提出的问题：如何在[流形](@entry_id:153038)上[微分](@entry_id:158718)[张量场](@entry_id:190170)？

#### 协变导数

我们已经看到，普通偏导数 $\partial_j V^i$ 不是张量。为了得到一个具有良好变换性质的导数，我们必须引入一个称为**[仿射联络](@entry_id:160152)** (affine connection) 的新结构。联络提供了一种“连接”邻近点切空间的方法，从而使得比较不同点的矢量成为可能。

一个[仿射联络](@entry_id:160152) $\nabla$ 在[局部坐标系](@entry_id:751394)中由一组称为**克里斯托费尔符号** (Christoffel symbols) 的系数 $\Gamma^k_{ij}$ 来描述。与偏导数算子本身类似，这些符号**不构成**一个张量的分量。它们的变换法则是：
$$
\bar{\Gamma}^k_{ij} = \frac{\partial \bar{x}^k}{\partial x^m} \frac{\partial x^p}{\partial \bar{x}^i} \frac{\partial x^q}{\partial \bar{x}^j} \Gamma^m_{pq} + \frac{\partial \bar{x}^k}{\partial x^m} \frac{\partial^2 x^m}{\partial \bar{x}^i \partial \bar{x}^j}
$$
注意这个变换法则中的第二个非齐次项，它与我们之[前推](@entry_id:158718)导 $\partial_j V^i$ 变换法则时遇到的“坏”项非常相似。事实上，它的形式正是为了“抵消”那个坏项而存在的 ([@problem_id:1543267])。

利用联络，我们定义**协变导数** (covariant derivative) $\nabla_j V^i$ 如下：
$$
\nabla_j V^i = \partial_j V^i + \Gamma^i_{jk} V^k
$$
可以证明，这个新定义的量 $\nabla V$ 确实是一个 (1,1) 型[张量场](@entry_id:190170)。[协变导数](@entry_id:152476)通过引入克里斯托费尔符号作为“修正项”，弥补了普通偏导数的缺陷，使其成为一个真正的几何运算。

对于任何黎曼或[伪黎曼流形](@entry_id:184750)，存在一个唯一满足以下两个条件的联络，称为**列维-奇维塔联络** (Levi-Civita connection) ([@problem_id:2992334])：
1.  **无挠 (Torsion-free):** $\Gamma^k_{ij} = \Gamma^k_{ji}$。
2.  **度规兼容 (Metric-compatible):** $\nabla_k g_{ij} = 0$。这意味着[度规张量](@entry_id:160222)在协变导数下“像常数一样”，矢量在平行移动时其长度和它们之间的角度保持不变。

#### 李导数

除了协变导数，还有另一种在[流形](@entry_id:153038)上[微分](@entry_id:158718)张量的重要方式，即**李导数** (Lie derivative)。与协变导数不同，[李导数](@entry_id:171745)的定义不依赖于任何额外的联络结构，它只依赖于[流形](@entry_id:153038)本身的[微分](@entry_id:158718)结构。

给定一个矢量场 $X$，它在[流形](@entry_id:153038)上生成一个“流”，即一系列点沿着 $X$ 的[积分曲线](@entry_id:161858)的移动。[张量场](@entry_id:190170) $T$ 沿 $X$ 的[李导数](@entry_id:171745) $\mathcal{L}_X T$ 衡量了 $T$ 在这个流的拖拽下的变化率。对于一个 (0,2) 型张量（如度规 $g$），其[李导数](@entry_id:171745)的分量由下式给出：
$$
(\mathcal{L}_X g)_{ij} = X^k \partial_k g_{ij} + g_{kj} \partial_i X^k + g_{ik} \partial_j X^k
$$
这个公式定义了一个新的 (0,2) 型张量，其计算完全基于给定的张量和矢量场的分量及其偏导数。例如，我们可以计算在一个具有非欧几里得度规 $g_{xx} = g_{yy} = y^{-2}$ 的平面上，度规沿矢量场 $X = y \partial_y$ 的李导数分量 $(\mathcal{L}_X g)_{xx}$，并发现它是一个非零的函数 ([@problem_id:1667566])。李导数在研究[流形](@entry_id:153038)的对称性（即寻找使度规不变的矢量场，即满足 $\mathcal{L}_X g = 0$ 的 Killing 矢量场）等方面起着核心作用。

总之，张量场为在弯曲空间中表述物理和几何提供了一套自洽且强大的语言。通过理解张量的定义（无论是作为[多重线性映射](@entry_id:274221)还是通过其变换法则）、掌握其代数运算（张量积、缩并）以及[微分](@entry_id:158718)工具（[协变导数](@entry_id:152476)、[李导数](@entry_id:171745)），我们便拥有了探索从[微分几何](@entry_id:145818)到广义相对论等众多现代科学领域的关键钥匙。