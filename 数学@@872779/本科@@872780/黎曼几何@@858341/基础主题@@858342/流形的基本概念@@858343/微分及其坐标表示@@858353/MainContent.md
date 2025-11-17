## 引言
在[多变量微积分](@entry_id:147547)中，我们习惯于通过偏导数来理解函数的局部变化。然而，当我们将研究对象从平直的[欧氏空间](@entry_id:138052)推广到弯曲的光滑流形时，我们如何才能以一种内蕴的、不依赖于特定[坐标系](@entry_id:156346)的方式来描述这种变化呢？这正是[微分几何](@entry_id:145818)的核心问题之一，而“[微分](@entry_id:158718)”这一概念为我们提供了强有力的解答。[微分](@entry_id:158718)不仅是经典导数的自然推广，更是一个深刻的几何对象，它构成了分析[流形](@entry_id:153038)上函数、映射乃至整个几何结构的基础。

本文旨在系统地阐述[微分](@entry_id:158718)及其在[坐标系](@entry_id:156346)下的表示。我们将克服仅仅依赖偏导数向量的直观想法，建立一个在任何[光滑流形](@entry_id:160799)上都行之有效的严谨框架。通过阅读本文，您将理解[微分](@entry_id:158718)的代数本质，并学会如何在不同[坐标系](@entry_id:156346)（包括正交标架）中灵活地进行计算。

文章将分为三个核心部分。在“原理与机制”一章中，我们将从[微分](@entry_id:158718)作为余[切向量](@entry_id:265494)的内在定义出发，推导其坐标表达式，并探讨黎曼度量如何引入[梯度向量](@entry_id:141180)场这一对偶概念。接着，在“应用与跨学科联系”一章中，我们将展示[微分](@entry_id:158718)在坐标变换、几何量定义以及全局性质分析中的广泛应用，并揭示其在物理学、数据科学等前沿领域的深刻影响。最后，“动手实践”部分将提供一系列精心设计的问题，帮助您将理论知识转化为解决具体问题的能力。让我们首先深入探讨[微分](@entry_id:158718)的根本原理与机制。

## 原理与机制

继引言之后，本章将深入探讨[微分几何](@entry_id:145818)的核心工具——[微分](@entry_id:158718)及其在[坐标系](@entry_id:156346)下的表示。我们将从[光滑函数](@entry_id:267124)[微分](@entry_id:158718)的内在定义出发，逐步引入黎曼度量的作用，并最终将概念推广至[流形间的映射](@entry_id:158221)。

### 光滑[函数的[微](@entry_id:274991)分](@entry_id:158718)

在[光滑流形](@entry_id:160799)的框架下，一个函数在一点的“变化率”被精确地捕捉为一个代数对象，即它的[微分](@entry_id:158718)。这个对象是一个余[切向量](@entry_id:265494)，其定义完全独立于任何度量结构。

#### 将[微分](@entry_id:158718)定义为余[切向量](@entry_id:265494)

考虑一个 $n$ 维[光滑流形](@entry_id:160799) $M$。在任意一点 $p \in M$，其**[切空间](@entry_id:199137)** $T_pM$ 可以被严谨地定义为在点 $p$ 的**导子**（derivation）所构成的[向量空间](@entry_id:151108)。一个导子 $v$ 是一个作用于[流形](@entry_id:153038)上所有光滑函数 $f \in C^\infty(M)$ 的[线性映射](@entry_id:185132) $v: C^\infty(M) \to \mathbb{R}$，且满足[莱布尼茨法则](@entry_id:157949)（Leibniz rule）：对于任意 $f, g \in C^\infty(M)$，有 $v(fg) = f(p)v(g) + g(p)v(f)$。这个定义将[切向量](@entry_id:265494)的几何直觉（方向导数算子）提炼为其代数本质。

基于此，一个光滑函数 $f: M \to \mathbb{R}$ 在点 $p$ 的**[微分](@entry_id:158718)**（differential），记作 $df_p$，被定义为 $T_pM$ 上的一个线性泛函。也就是说，$df_p$ 是一个将切向量映射到实数的线性映射。其具体作用方式为：对于任意[切向量](@entry_id:265494) $v \in T_pM$，
$$
df_p(v) = v(f)
$$
这个定义表明，$df_p$ 的作用就是让切向量 $v$ （作为一个导子）作用在函数 $f$ 上。由定义可知，$df_p$ 是 $T_pM$ 的对偶空间 $T_p^*M$ 中的一个元素。这个[对偶空间](@entry_id:146945)被称为**[余切空间](@entry_id:270516)**（cotangent space）。因此，$df_p$ 是一个在点 $p$ 的**余切向量**（covector），也称为一个 $1$-**形式**（1-form）在点 $p$ 的值。

至关重要的是，[微分](@entry_id:158718) $df$ 的定义仅依赖于[流形](@entry_id:153038)的[光滑结构](@entry_id:159394)（它允许我们谈论[光滑函数](@entry_id:267124)和导子），而完全不依赖于任何黎曼度量或联络。它是一个比距离或角度更基本的内蕴几何对象 [@problem_id:3071956] [@problem_id:3043926]。

#### [切向量](@entry_id:265494)与[微分](@entry_id:158718)的坐标表示

为了进行具体计算，我们通常在[局部坐标](@entry_id:181200)图 $(U, (x^1, \dots, x^n))$ 中工作。这样一个[坐标图](@entry_id:156506)为[切空间](@entry_id:199137)和[余切空间](@entry_id:270516)提供了自然的基。

在点 $p \in U$，与坐标 $x^i$ 相关联的**坐标切向量** $\left.\frac{\partial}{\partial x^i}\right|_p$（常简记为 $\partial_i|_p$）被定义为一个导子，其作用于任意[光滑函数](@entry_id:267124) $f$ 的方式为取 $f$ 在该[坐标系](@entry_id:156346)下表示的[偏导数](@entry_id:146280)：
$$
\left.\frac{\partial}{\partial x^i}\right|_p(f) = \frac{\partial (f \circ x^{-1})}{\partial x^i}(x(p))
$$
可以验证，这样定义的 $\partial_i|_p$ 确实满足线性和[莱布尼茨法则](@entry_id:157949)，因此是 $T_pM$ 中的一个有效元素。更进一步，可以证明集合 $\{\partial_i|_p\}_{i=1}^n$ 构成了 $T_pM$ 的一个基，称为**坐标标架**（coordinate frame）[@problem_id:3043926]。

相应地，[余切空间](@entry_id:270516) $T_p^*M$ 拥有一个**对偶基**，由各个坐标函数 $x^i$ 的[微分](@entry_id:158718) $\{dx^i|_p\}_{i=1}^n$ 构成。根据[微分](@entry_id:158718)的定义，$dx^i|_p$ 作用于一个切向量 $v$ 的结果是 $v(x^i)$。当我们将其作用于[基向量](@entry_id:199546) $\partial_j|_p$ 时，我们得到：
$$
dx^i|_p(\partial_j|_p) = \partial_j|_p(x^i) = \frac{\partial x^i}{\partial x^j} = \delta^i_j
$$
其中 $\delta^i_j$ 是克罗内克（Kronecker）符号。这个关系式 $dx^i(\partial_j) = \delta^i_j$ 正是这两组基互为对偶的定义 [@problem_id:3043930] [@problem_id:3043926]。

现在，我们可以导出任意[光滑函数](@entry_id:267124) $f$ 的[微分](@entry_id:158718) $df$ 的坐标表达式。由于 $df_p$ 是一个余[切向量](@entry_id:265494)，它可以被写作对偶基的线性组合：
$$
df_p = \sum_{i=1}^n c_i \, dx^i|_p
$$
为了确定系数 $c_j$，我们将上式作用于[基向量](@entry_id:199546) $\partial_j|_p$：
$$
df_p(\partial_j|_p) = \left(\sum_{i=1}^n c_i \, dx^i|_p\right)(\partial_j|_p) = \sum_{i=1}^n c_i \, \delta^i_j = c_j
$$
另一方面，根据 $df_p$ 的定义，$df_p(\partial_j|_p) = \partial_j|_p(f) = \frac{\partial f}{\partial x^j}(p)$。比较两式可知，系数 $c_j$ 正是函数 $f$ 对坐标 $x^j$ 的偏导数。因此，我们得到了[微分](@entry_id:158718) $df$ 的核心坐标表达式：
$$
df = \frac{\partial f}{\partial x^i} dx^i
$$
这里我们采用了爱因斯坦求和约定，即对重复出现的上下指标自动求和。这个表达式表明，函数 $f$ 的偏导数 $\frac{\partial f}{\partial x^i}$ 正是其[微分](@entry_id:158718) $1$-形式 $df$ 在[坐标基](@entry_id:270149) $\{dx^i\}$下的分量 [@problem_id:3071956]。

**例：** 考虑二维[欧氏空间](@entry_id:138052) $\mathbb{R}^2$ 作为光滑流形，使用标准坐标 $(x,y)$。设[光滑函数](@entry_id:267124)为 $f(x,y) = x^2y$。其偏导数为：
$$
\frac{\partial f}{\partial x} = 2xy, \quad \frac{\partial f}{\partial y} = x^2
$$
因此，其[微分](@entry_id:158718) $df$ 的坐标表达式为：
$$
df = 2xy\,dx + x^2\,dy
$$
现在，让我们将这个 $1$-形式作用在一个具体的[切向量](@entry_id:265494)上，例如 $X = 2\partial_x - \partial_y$。根据定义 $df(X) = X(f)$：
$$
df(X) = (2\partial_x - \partial_y)(x^2y) = 2\partial_x(x^2y) - \partial_y(x^2y) = 2(2xy) - (x^2) = 4xy - x^2
$$
这个结果是一个标量（函数），与我们预期的一致 [@problem_id:3043928]。

#### 几何解释与性质

[坐标基](@entry_id:270149)向量 $\partial_i|_p$ 和对偶[基向量](@entry_id:199546) $dx^i|_p$ 具有清晰的几何意义。
- $\partial_i|_p(f)$ 的值是在点 $p$ 沿着第 $i$ 个坐标曲线方向上函数 $f$ 的**[方向导数](@entry_id:189133)** [@problem_id:3043930]。
- $dx^i|_p(v)$ 的作用是从任意一个[切向量](@entry_id:265494) $v = \sum_j v^j \partial_j|_p$ 中**提取其第 $i$ 个分量** $v^i$。即 $dx^i(v) = v^i$ [@problem_id:3043930]。

一个重要的性质是关于[微分](@entry_id:158718)何时为零。点 $p$ 的一个**[临界点](@entry_id:144653)**（critical point）是指 $df_p = 0$ 的点。这是一个内蕴的、与[坐标系](@entry_id:156346)无关的陈述，它意味着 $df_p$ 是[余切空间](@entry_id:270516)中的[零向量](@entry_id:156189)。根据线性代数的基本原理，一个向量是零向量，当且仅当它在某个（因此是任意）基下的所有分量都为零。由于 $df_p$ 在[坐标基](@entry_id:270149) $\{dx^i|_p\}$ 下的分量是偏导数 $\{\partial_i f(p)\}$，因此我们得出结论：
$$
df_p = 0 \iff \frac{\partial f}{\partial x^i}(p) = 0 \quad \text{for all } i=1, \dots, n
$$
这个[等价关系](@entry_id:138275)在任何一个[局部坐标](@entry_id:181200)图中都成立。如果在一套[坐标系](@entry_id:156346)中所有偏导数都为零，那么通过[坐标变换](@entry_id:172727)的[雅可比法](@entry_id:147508)则，在任何其他[坐标系](@entry_id:156346)中它们也必然都为零。因此，“$df_p$ 是否为零”这个问题的答案不依赖于[坐标系](@entry_id:156346)的选择 [@problem_id:3043927]。

### [黎曼度量](@entry_id:754359)的作用：梯度与范数

到目前为止，我们的讨论完全处于[光滑流形](@entry_id:160799)的范畴。引入**黎曼度量**（Riemannian metric）$g$ 会赋予[流形](@entry_id:153038)更丰富的几何结构，特别是它允许我们定义向量的长度和向量间的角度。度量 $g$ 为每个切空间 $T_pM$ 指定了一个[内积](@entry_id:158127) $g_p(\cdot, \cdot)$。

#### 梯度向量场

有了度量，我们就可以在切向量场和 $1$-形式场之间建立一个重要的对应关系。对于一个[光滑函数](@entry_id:267124) $f$，其**梯度**（gradient） $\nabla f$ 是一个**向量场**，其定义依赖于度量 $g$。$\nabla f$ 是唯一满足下述条件的向量场：对于任意向量场 $X$，
$$
g(\nabla f, X) = df(X)
$$
这个定义将 $1$-形式 $df$ 和向量场 $\nabla f$ 通过度量 $g$ 对偶起来。请注意 $df$ 和 $\nabla f$ 的根本区别：$df$ 是一个余[切向量](@entry_id:265494)场（$1$-形式场），其定义不依赖于度量；而 $\nabla f$ 是一个切向量场，它的定义从根本上就与度量 $g$ 绑定在一起。改变度量通常会改变[梯度向量](@entry_id:141180)场，即使函数 $f$ 和[微分](@entry_id:158718) $df$ 保持不变 [@problem_id:3043937]。

#### [音乐同构](@entry_id:199976)：降号(♭)与升号(♯)

上述 $df$ 与 $\nabla f$ 之间的关系是**[音乐同构](@entry_id:199976)**（musical isomorphisms）的一个实例。这些是由度量 $g$ 诱导的在[切空间](@entry_id:199137) $T_pM$ 和[余切空间](@entry_id:270516) $T_p^*M$ 之间的[典范同构](@entry_id:202335)。

- **降号(Flat)** 映射 $\flat: T_pM \to T_p^*M$，将一个[切向量](@entry_id:265494) $v$ 变为一个余切向量 $v^\flat$，其定义为：对于所有 $w \in T_pM$，$v^\flat(w) = g(v,w)$。这通常被称为“降低指标”。

- **升号(Sharp)** 映射 $\sharp: T_p^*M \to T_pM$，是 $\flat$ 的逆映射，将一个余切向量 $\alpha$ 变为一个[切向量](@entry_id:265494) $\alpha^\sharp$，其定义为：对于所有 $w \in T_pM$，$g(\alpha^\sharp, w) = \alpha(w)$。这被称为“升高指标”。

利用这些记号，梯度向量场可以被简洁地表示为[微分](@entry_id:158718)的“升号”：
$$
\nabla f = (df)^\sharp
$$
在[局部坐标](@entry_id:181200) $\{x^i\}$ 中，设度量张量的分量为 $g_{ij} = g(\partial_i, \partial_j)$，其[逆矩阵](@entry_id:140380)的分量为 $g^{ij}$ (满足 $g^{ik}g_{kj} = \delta^i_j$)。[音乐同构](@entry_id:199976)的坐标表达式可以推导如下：
- 对于 $v = v^i \partial_i$，其降号 $v^\flat$ 的分量 $(v^\flat)_j$ 为 $v^\flat(\partial_j) = g(v, \partial_j) = g(v^i\partial_i, \partial_j) = v^i g_{ij}$。因此 $v^\flat = (g_{ij}v^i)dx^j$。
- 对于 $\alpha = \alpha_j dx^j$，其升号 $\alpha^\sharp = (\alpha^\sharp)^i \partial_i$ 的分量 $(\alpha^\sharp)^i$ 满足 $g_{ki}(\alpha^\sharp)^i = g(\alpha^\sharp, \partial_k) = \alpha(\partial_k) = \alpha_k$。两边乘以 $g^{jk}$ 得到 $(\alpha^\sharp)^j = g^{jk}\alpha_k$。因此 $\alpha^\sharp = (g^{ij}\alpha_j)\partial_i$。

将此应用于梯度，由于 $df = (\partial_j f)dx^j$，我们得到梯度的坐标表达式：
$$
\nabla f = (g^{ij} \partial_j f) \partial_i
$$
这个表达式明确地显示了梯度对逆度量分量 $g^{ij}$ 的依赖性 [@problem_id:3043946] [@problem_id:3043937]。

**例：** 在 $\mathbb{R}^2$ 上考虑函数 $f(x,y) = x^2+y$。其[微分](@entry_id:158718)恒为 $df = 2x\,dx + dy$。现在我们考察两个不同的度量：
1.  标准欧氏度量 $g_1 = dx^2 + dy^2$。其矩阵为 $G_1 = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}$，[逆矩阵](@entry_id:140380) $G_1^{-1}$ 也是单位阵。此时 $g_1^{xx}=1, g_1^{xy}=0, g_1^{yy}=1$。梯度为：
    $$
    \nabla^{g_1} f = (g_1^{xx}\partial_x f + g_1^{xy}\partial_y f)\partial_x + (g_1^{yx}\partial_x f + g_1^{yy}\partial_y f)\partial_y = (1 \cdot 2x + 0 \cdot 1)\partial_x + (0 \cdot 2x + 1 \cdot 1)\partial_y = 2x\,\partial_x + \partial_y
    $$
2.  一个不同的度量 $g_2 = 4\,dx^2 + dy^2$。其矩阵为 $G_2 = \begin{pmatrix} 4  0 \\ 0  1 \end{pmatrix}$，逆矩阵 $G_2^{-1} = \begin{pmatrix} 1/4  0 \\ 0  1 \end{pmatrix}$。此时 $g_2^{xx}=1/4, g_2^{xy}=0, g_2^{yy}=1$。梯度变为：
    $$
    \nabla^{g_2} f = (\frac{1}{4} \cdot 2x + 0 \cdot 1)\partial_x + (0 \cdot 2x + 1 \cdot 1)\partial_y = \frac{x}{2}\,\partial_x + \partial_y
    $$
这个例子清晰地表明，改变度量从 $g_1$ 到 $g_2$ 并不改变[微分](@entry_id:158718) $df$，但显著地改变了梯度向量场 $\nabla f$ [@problem_id:3043937]。

#### [微分](@entry_id:158718)的范数

黎曼度量 $g$ 不仅在切空间 $T_pM$ 上定义了[内积](@entry_id:158127)，也通过其逆 $g^{-1}$ 在[余切空间](@entry_id:270516) $T_p^*M$ 上诱导了一个[内积](@entry_id:158127)。对于两个 $1$-形式 $\alpha, \beta$，它们的[内积](@entry_id:158127)定义为 $g^*(\alpha, \beta) = g(\alpha^\sharp, \beta^\sharp)$。在[坐标系](@entry_id:156346)中，这等于 $g^{ij}\alpha_i \beta_j$。

[微分](@entry_id:158718) $df$ 的**平方范数**（squared norm），记为 $|df|^2$，就是 $df$ 与自身的[内积](@entry_id:158127)：
$$
|df|^2 = g^*(df, df) = g^{ij}(\partial_i f)(\partial_j f)
$$
这个量是一个标量函数，它在每一点度量了函数 $f$ "变化得有多快"。计算它需要用到逆度量张量 $g^{ij}$ [@problem_id:3043953]。

### 正交标架：一个优美的视角

尽管坐标标架 $\{ \partial_i \}$ 在理论推导中很方便，但在实际计算中，特别是当度量 $g_{ij}$ 不是[单位矩阵](@entry_id:156724)时，它们可能会很繁琐。一个更优雅且计算上更简便的选择是使用**局部正交标架**（local orthonormal frame）。

#### 在正交标架中的表达式

一个局部正交标架是一个向量场基 $\{e_i\}_{i=1}^n$，满足 $g(e_i, e_j) = \delta_{ij}$。其对偶[余标架](@entry_id:637284)（dual coframe）是 $\{ \omega^i \}_{i=1}^n$，满足 $\omega^i(e_j) = \delta^i_j$。

在这样的标架下，任何向量场 $V$ 和 $1$-形式 $\alpha$ 的展开式都非常简洁：
- $V = \sum_i g(V, e_i) e_i$
- $\alpha = \sum_i \alpha(e_i) \omega^i$

将这两个通用公式应用于 $\nabla f$ 和 $df$：
- $df$ 的分量是 $df(e_i)$，根据[微分](@entry_id:158718)的定义，这等于 $e_i(f)$。因此：
  $$
  df = \sum_{i=1}^n e_i(f) \, \omega^i
  $$
- $\nabla f$ 的分量是 $g(\nabla f, e_i)$。根据梯度的定义，这等于 $df(e_i)$，也就是 $e_i(f)$。因此：
  $$
  \nabla f = \sum_{i=1}^n e_i(f) \, e_i
  $$
这两个表达式 [@problem_id:3043929] 异常简洁且富有启发性。它们表明，在正交标架下，[微分](@entry_id:158718) $df$ 和梯度 $\nabla f$ 具有**完全相同的分量**，即函数 $f$ 沿着各个[正交基](@entry_id:264024)向量方向的[方向导数](@entry_id:189133)。$df$ 是用这些分量和对偶[余标架](@entry_id:637284) $\{ \omega^i \}$ 组合成的 $1$-形式，而 $\nabla f$ 是用同样的分量和原始标架 $\{ e_i \}$ 组合成的向量场。

#### 范数的再探讨

使用正交标架的表达式，计算[微分](@entry_id:158718)的范数也变得极为简单。由于[余标架](@entry_id:637284) $\{ \omega^i \}$ 是对偶于正交标架 $\{ e_i \}$ 的，它自身在由 $g^*$ 诱导的[内积](@entry_id:158127)下也是一个正交基，即 $g^*(\omega^i, \omega^j) = \delta^{ij}$。因此，$df$ 的平方范数就是其分量的平方和：
$$
|df|^2 = g^*\left(\sum_i e_i(f)\omega^i, \sum_j e_j(f)\omega^j\right) = \sum_{i,j} e_i(f)e_j(f)g^*(\omega^i, \omega^j) = \sum_{i=1}^n (e_i(f))^2
$$
这个公式 $|df|^2 = \sum_i (e_i(f))^2$ 将一个复杂的、依赖于逆度量矩阵的计算，转化为一个简单的平方和。这突显了在处理[黎曼几何](@entry_id:160508)中的具体计算时，寻找一个正交标架的巨大威力 [@problem_id:3043953]。

### 推广：[流形](@entry_id:153038)间[映射的微分](@entry_id:269524)

目前我们只考虑了值域为 $\mathbb{R}$ 的函数 $f: M \to \mathbb{R}$。这个概念可以自然地推广到两个光滑流形之间的映射 $f: M \to N$。

设 $M$ 是 $m$ 维[流形](@entry_id:153038)， $N$ 是 $n$ 维[流形](@entry_id:153038)。一个映射 $f: M \to N$ 被称为**光滑的**（smooth），如果它在[局部坐标](@entry_id:181200)中的表示是光滑的。具体来说，对于 $M$ 中每一点 $p$，都存在 $p$ 的一个[坐标图](@entry_id:156506) $(U, \varphi)$ 和 $f(p)$ 的一个[坐标图](@entry_id:156506) $(V, \psi)$，使得 $f(U) \subseteq V$，并且复合映射 $\psi \circ f \circ \varphi^{-1}$ 是一个从 $\mathbb{R}^m$ 的开集到 $\mathbb{R}^n$ 的开集的[光滑映射](@entry_id:203730)（在标准微积分的意义下） [@problem_id:3044968]。

对于这样一个[光滑映射](@entry_id:203730) $f$，它在点 $p \in M$ 的**[微分](@entry_id:158718)**（或称**[前推](@entry_id:158718)**，pushforward）是一个[线性映射](@entry_id:185132)，记为 $df_p: T_pM \to T_{f(p)}N$。它的作用是将 $M$ 中过点 $p$ 的曲线的[切向量](@entry_id:265494)，映射为 $N$ 中对应的像曲线的[切向量](@entry_id:265494)。如果 $\gamma(t)$ 是 $M$ 中一条满足 $\gamma(0)=p$ 的光滑曲线，其在 $p$ 点的切向量为 $\gamma'(0)$，那么 $df_p$ 将这个向量映射到复合曲线 $f \circ \gamma$ 在 $f(p)$ 点的切向量 $(f \circ \gamma)'(0)$ [@problem_id:3044968]：
$$
df_p(\gamma'(0)) = (f \circ \gamma)'(0)
$$
在[局部坐标](@entry_id:181200)中，这个线性映射 $df_p$ 可以用一个矩阵来表示。设 $x=(x^1, \dots, x^m)$ 是 $p$ 附近的[局部坐标](@entry_id:181200)， $y=(y^1, \dots, y^n)$ 是 $f(p)$ 附近的[局部坐标](@entry_id:181200)。映射 $f$ 在这些坐标下表示为 $y = F(x)$。那么，相对于切空间的[坐标基](@entry_id:270149) $\{\partial/\partial x^i\}$ 和 $\{\partial/\partial y^j\}$，[线性映射](@entry_id:185132) $df_p$ 的矩阵就是函数 $F$ 在点 $\varphi(p)$ 的**[雅可比矩阵](@entry_id:264467)**（Jacobian matrix）[@problem_id:3044968]：
$$
[df_p]^j_i = \frac{\partial F^j}{\partial x^i}
$$
这个 $n \times m$ 矩阵捕捉了映射 $f$ 在一点附近的线性近似。它的秩在几何中至关重要，引出了**[浸入](@entry_id:161534)**（immersion，即 $df_p$ 处处[单射](@entry_id:183792)）和**淹没**（submersion，即 $df_p$ 处处满射）等概念。一个既是单射浸入又是到其像的[同胚](@entry_id:146933)的映射被称为**嵌入**（embedding）。[惠特尼嵌入定理](@entry_id:161137)（Whitney Embedding Theorem）是[微分拓扑](@entry_id:157662)的一个基石，它保证了任何 $n$ 维[光滑流形](@entry_id:160799)都可以被光滑地嵌入到 $2n$ 维的[欧氏空间](@entry_id:138052) $\mathbb{R}^{2n}$ 中，这显示了研究[流形](@entry_id:153038)间映射及其[微分](@entry_id:158718)的深远意义 [@problem_id:3044968]。