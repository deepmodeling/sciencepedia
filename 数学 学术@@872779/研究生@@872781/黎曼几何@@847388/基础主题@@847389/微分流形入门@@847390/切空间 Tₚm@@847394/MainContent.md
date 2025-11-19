## 引言
在微分几何的宏伟殿堂中，[切空间](@entry_id:199137)概念是支撑起整个大厦的基石。它允许我们将强大而直观的线性代数工具应用于局部弯曲的[光滑流形](@entry_id:160799)之上。尽管流形本身可能是[非线性](@entry_id:637147)的复杂对象，但在每一个点，我们都可以通过一个[向量空间](@entry_id:151108)——切空间——来对其进行最佳的线性近似。本文旨在系统性地揭示切空间的奥秘，解决从抽象定义到具体应用的过渡难题。

通过本文的学习，您将建立起对这一核心概念的坚实理解。我们将从第一性原理出发，逐步深入。在“原理与机制”一章中，我们将形式化地定义[切空间与余切空间](@entry_id:157598)，并探讨它们在[坐标变换](@entry_id:172727)下的内在行为，以及黎曼度量如何为它们赋予丰富的几何结构。接下来，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示[切空间](@entry_id:199137)作为线性化舞台的强大威力，看它如何连接[微分几何](@entry_id:145818)与分析学、物理学等多个领域。最后，通过“动手实践”部分，您将有机会通过解决具体问题，将理论知识转化为可操作的技能。让我们一同启程，探索[流形](@entry_id:153038)上这片至关重要的“局部平地”。

## 原理与机制

在介绍性章节之后，我们现在深入探讨[切空间](@entry_id:199137)及其相关构造的数学核心。本章将从第一性原理出发，系统地建立切空间、[余切空间](@entry_id:270516)的概念，并阐明它们在[坐标变换](@entry_id:172727)下的行为。我们还将探讨[黎曼度量](@entry_id:754359)如何提供一种关键的附加结构，从而连接这些看似分离的世界。我们的目标是不仅要理解这些对象的定义，更要掌握它们在[微分几何](@entry_id:145818)中的运作机制。

### 切空间：[流形](@entry_id:153038)的线性近似

思考一个光滑流形 $M$ 上的一个点 $p$。尽[管流](@entry_id:189531)形本身在局部上可能弯曲，但[微分几何](@entry_id:145818)的一个核心思想是在每个点 $p$ 附近用一个[线性空间](@entry_id:151108)来近似它。这个[线性空间](@entry_id:151108)就是**[切空间](@entry_id:199137)**，记为 $T_p M$。它是在点 $p$ [对流](@entry_id:141806)形 $M$ 进行的“线性化”或“[一阶近似](@entry_id:147559)”。我们可以通过几种等价的方式来形式化这个概念，其中最富代数性的定义是将其视为一个导[子空间](@entry_id:150286)。

一个在点 $p$ 的**切向量**（tangent vector）被定义为一个作用在 $M$ 上的光滑实值[函数代数](@entry_id:144602) $C^\infty(M)$ 上的映射 $v: C^\infty(M) \to \mathbb{R}$，它满足两个条件：
1.  **线性性**: 对任意常数 $a, b \in \mathbb{R}$ 和函数 $f, g \in C^\infty(M)$，有 $v(af+bg) = av(f) + bv(g)$。
2.  **莱布尼兹法则 (Leibniz Rule)**: 对任意函数 $f, g \in C^\infty(M)$，有 $v(fg) = f(p)v(g) + g(p)v(f)$。

满足这两个条件的映射 $v$ 被称为在点 $p$ 的一个**导子**（derivation）。莱布尼兹法则精确地捕捉了方向[导数的性质](@entry_id:141529)，它确保了[切向量](@entry_id:265494)只关心函数在点 $p$ 附近的局部行为。所有在点 $p$ 的导子的集合，通过自然的函数加法和[标量乘法](@entry_id:155971)，构成了一个实[向量空间](@entry_id:151108)，这个空间就是切空间 $T_p M$。

为了具体地把握[切空间](@entry_id:199137)，我们引入[局部坐标](@entry_id:181200)。设 $(U, \phi)$ 是包含 $p$ 的一个[局部坐标](@entry_id:181200)卡，其坐标函数为 $(x^1, \dots, x^n)$。在点 $p$，我们可以定义 $n$ 个特殊的导子，记为 $\left\{ \frac{\partial}{\partial x^1}\bigg|_p, \dots, \frac{\partial}{\partial x^n}\bigg|_p \right\}$。它们对任意[光滑函数](@entry_id:267124) $f \in C^\infty(M)$ 的作用方式定义为：
$$
\frac{\partial}{\partial x^i}\bigg|_p (f) := \frac{\partial (f \circ \phi^{-1})}{\partial x^i}(\phi(p))
$$
可以验证，这些映射确实满足线性和莱布尼兹法则，因此它们是 $T_p M$ 中的元素。更重要的是，可以证明这 $n$ 个向量构成了 $T_p M$ 的一组基。这组基被称为由[坐标系](@entry_id:156346) $(x^i)$ 诱导的**[坐标基](@entry_id:270149)**。

这一事实带来了一个至关重要的结论：在点 $p$ 的[切空间](@entry_id:199137)的维数等于[流形](@entry_id:153038)本身的维数。
$$
\dim(T_p M) = \dim(M)
$$
这个原理的应用非常广泛。例如，考虑一个在二维平面内运动的刚性哑铃。它的位形（configuration）可以由其质心坐标 $(x, y)$ 和其与固定轴的夹角 $\theta$ 唯一确定。所有可能的位形 $(x, y, \theta)$ 构成了一个三维流形 $M$。在任意一个位形 $p$ 处，系统所有可能的[瞬时速度](@entry_id:167797)（例如 $(\dot{x}, \dot{y}, \dot{\theta})$）张成了一个[向量空间](@entry_id:151108)，这个空间正是切空间 $T_p M$。由于[流形](@entry_id:153038)是三维的，因此该[切空间](@entry_id:199137)的维数也必然是 3 [@problem_id:1852967]。

### [余切空间](@entry_id:270516)：对偶视角

一旦我们理解了[切空间](@entry_id:199137)是一个[向量空间](@entry_id:151108)，线性代数中的[对偶理论](@entry_id:143133)便自然地进入了我们的视野。对于每个切空间 $T_p M$，都存在一个与之对应的**[对偶向量空间](@entry_id:193439)**（dual vector space），我们称之为在点 $p$ 的**[余切空间](@entry_id:270516)**（cotangent space），记为 $T_p^*M$。

根据定义，$T_p^*M$ 是所有从 $T_p M$ 到[实数域](@entry_id:151347) $\mathbb{R}$ 的[线性映射](@entry_id:185132)的集合。
$$
T_p^*M := \text{Hom}(T_p M, \mathbb{R})
$$
[余切空间](@entry_id:270516)中的元素被称为**余[切向量](@entry_id:265494)**（covector），或称在点 $p$ 的 **[1-形式](@entry_id:270392)**（1-form）。线性代数的一个基本定理告诉我们，任何[有限维向量空间](@entry_id:265491)的对偶空间都具有与原空间相同的维数。因此，我们有：
$$
\dim(T_p^*M) = \dim(T_p M) = \dim(M)
$$
例如，如果一个[流形](@entry_id:153038)的维数是 7，那么在任意一点的切空间 $T_p M$ 是一个 7 维[向量空间](@entry_id:151108)。其对偶空间，即所有从 $T_p M$ 到 $\mathbb{R}$ 的线性映射构成的空间，也必然是一个 7 维[向量空间](@entry_id:151108) [@problem_id:1635495]。

余切向量最自然、最重要的来源是[光滑函数](@entry_id:267124)的**[微分](@entry_id:158718)**（differential）。对于任意[光滑函数](@entry_id:267124) $f: M \to \mathbb{R}$，它在点 $p$ 的[微分](@entry_id:158718) $df_p$ 是一个余[切向量](@entry_id:265494)，其定义为其对任意切向量 $v_p \in T_p M$ 的作用：
$$
df_p(v_p) := v_p(f)
$$
这个定义完美地体现了对偶性：余[切向量](@entry_id:265494)“吞食”切向量并产生一个实数。$df_p(v_p)$ 的值表示函数 $f$ 沿着 $v_p$ 方向的一阶变化率。值得强调的是，[微分](@entry_id:158718) $df_p$ 只捕捉了函数 $f$ 在点 $p$ 的一阶（线性）行为，而不包含任何关于其二阶或更高阶行为（如曲率）的信息 [@problem_id:2994005]。

正如[切空间](@entry_id:199137)有[坐标基](@entry_id:270149)一样，[余切空间](@entry_id:270516)也有其对应的**对偶基**。给定[切空间](@entry_id:199137)的[坐标基](@entry_id:270149) $\{\partial_i|_p\}$（简记为 $\partial/\partial x^i|_p$），其对偶基由坐标函数本身的[微分](@entry_id:158718)构成，记为 $\{dx^1|_p, \dots, dx^n|_p\}$。它们被称为**坐标余基**。这两个基底之间的对偶关系通过以下基本等式体现：
$$
dx^i|_p \left( \frac{\partial}{\partial x^j}\bigg|_p \right) = \delta^i_j
$$
其中 $\delta^i_j$ 是克罗内克符号（Kronecker delta）。这个等式可以直接从[微分](@entry_id:158718)和导子的定义中推导出来 [@problem_id:2994035]：
$$
dx^i|_p \left( \frac{\partial}{\partial x^j}\bigg|_p \right) = \frac{\partial}{\partial x^j}\bigg|_p (x^i) = \frac{\partial x^i}{\partial x^j} = \delta^i_j
$$

有了基底，我们就可以用分量来表示任意的[向量和余向量](@entry_id:181128)。一个[切向量](@entry_id:265494) $v_p \in T_p M$ 可以写成 $v_p = \sum_i v^i \frac{\partial}{\partial x^i}\big|_p$，而一个余向量 $\omega_p \in T_p^*M$ 可以写成 $\omega_p = \sum_j \omega_j dx^j\big|_p$。它们之间的**自然配对**（natural pairing）$\omega_p(v_p)$ 可以通过分量轻松计算。利用线性和对偶基的关系，我们得到：
$$
\omega_p(v_p) = \left( \sum_j \omega_j dx^j\big|_p \right) \left( \sum_i v^i \frac{\partial}{\partial x^i}\bigg|_p \right) = \sum_{i,j} \omega_j v^i \left( dx^j\big|_p \left( \frac{\partial}{\partial x^i}\bigg|_p \right) \right) = \sum_{i,j} \omega_j v^i \delta^j_i = \sum_i \omega_i v^i
$$
这个结果——对应分量的乘[积之和](@entry_id:266697)——是[微分几何](@entry_id:145818)中进行具体计算的基石。例如，如果在一个[三维流形](@entry_id:193484)的[局部坐标](@entry_id:181200)中，我们有余向量 $\omega_p$ 的分量为 $(3, 5, -2)$，向量 $v_p$ 的分量为 $(2, -1, 4)$，那么它们的配对值为 $\omega_p(v_p) = (3)(2) + (5)(-1) + (-2)(4) = 6 - 5 - 8 = -7$ [@problem_id:2994035]。

### 变换、丛与场

到目前为止，我们只讨论了单一点上的结构。为了研究[流形](@entry_id:153038)的全局性质，我们需要将所有点上的[切空间](@entry_id:199137)和[余切空间](@entry_id:270516)“捆绑”在一起。所有[切空间](@entry_id:199137)的并集 $TM = \bigsqcup_{p \in M} T_p M$ 构成了**[切丛](@entry_id:161294)**（tangent bundle），而所有[余切空间](@entry_id:270516)的并集 $T^*M = \bigsqcup_{p \in M} T_p^*M$ 构成了**[余切丛](@entry_id:185138)**（cotangent bundle）。

一个**向量场**（vector field）是[切丛](@entry_id:161294)的一个光滑[截面](@entry_id:154995)，即一个[光滑映射](@entry_id:203730) $X: M \to TM$，它为[流形](@entry_id:153038)上的每一点 $p$ 指定一个[切向量](@entry_id:265494) $X_p \in T_p M$。类似地，一个**[1-形式](@entry_id:270392)**（1-form）是[余切丛](@entry_id:185138)的一个光滑[截面](@entry_id:154995) $\alpha: M \to T^*M$，它为每一点 $p$ 指定一个[余向量](@entry_id:157727) $\alpha_p \in T_p^*M$ [@problem_id:2994002]。当一个 1-形式 $\alpha$ 和一个向量场 $X$ 配对时，会产生一个光滑的实值函数 $p \mapsto \alpha_p(X_p)$。

[流形](@entry_id:153038)的一个基本特征是它被多个[局部坐标](@entry_id:181200)卡所覆盖。一个自然的问题是：当从一个[坐标系](@entry_id:156346)切换到另一个[坐标系](@entry_id:156346)时，[向量和余向量](@entry_id:181128)的分量会如何变化？答案揭示了它们深刻的几何本性。

考虑两个重叠的坐标卡 $(U, (x^i))$ 和 $(V, (y^j))$。坐标变换函数 $y = y(x)$ 是光滑的，并且其[雅可比矩阵](@entry_id:264467) $J$ 的元素为 $J^i{}_j = \frac{\partial y^i}{\partial x^j}$。使用[链式法则](@entry_id:190743)，我们可以找到两个[坐标基](@entry_id:270149)之间的关系：
$$
\frac{\partial}{\partial x^j} = \sum_i \frac{\partial y^i}{\partial x^j} \frac{\partial}{\partial y^i} = \sum_i J^i{}_j \frac{\partial}{\partial y^i}
$$
现在，假设一个切向量 $v$ 在 $x$-[坐标系](@entry_id:156346)下的分量为 $(v^j)$，在 $y$-[坐标系](@entry_id:156346)下的分量为 $(v'^i)$。为了保持向量 $v$ 本身的[几何不变性](@entry_id:637068)，即 $v = \sum_j v^j \frac{\partial}{\partial x^j} = \sum_i v'^i \frac{\partial}{\partial y^i}$，我们必须有：
$$
\sum_i v'^i \frac{\partial}{\partial y^i} = \sum_j v^j \left( \sum_i J^i{}_j \frac{\partial}{\partial y^i} \right) = \sum_i \left( \sum_j J^i{}_j v^j \right) \frac{\partial}{\partial y^i}
$$
比较 $\frac{\partial}{\partial y^i}$ 的系数，我们得到了向量分量的变换法则：
$$
v'^i = \sum_j \frac{\partial y^i}{\partial x^j} v^j \quad \text{或矩阵形式} \quad v' = J v
$$
这个变换法则被称为**逆变**（contravariant）法则。向量分量的[变换矩阵](@entry_id:151616)是雅可比矩阵 $J$ 本身。

对于余向量，情况则有所不同。再次使用[链式法则](@entry_id:190743)，我们得到余基的变换关系：
$$
dx^j = \sum_i \frac{\partial x^j}{\partial y^i} dy^i
$$
注意这里出现的是逆变换的[雅可比矩阵](@entry_id:264467) $(J^{-1})$ 的元素。然而，一种更直接的方法是考虑 $dy^i = \sum_j \frac{\partial y^i}{\partial x^j} dx^j = \sum_j J^i{}_j dx^j$。设一个[余向量](@entry_id:157727) $\omega$ 在 $x$-[坐标系](@entry_id:156346)下分量为 $(\omega_j)$，在 $y$-[坐标系](@entry_id:156346)下分量为 $(\omega'_i)$。那么 $\omega = \sum_j \omega_j dx^j = \sum_i \omega'_i dy^i$。代入 $dy^i$ 的表达式：
$$
\sum_j \omega_j dx^j = \sum_i \omega'_i \left( \sum_j J^i{}_j dx^j \right) = \sum_j \left( \sum_i \omega'_i J^i{}_j \right) dx^j
$$
比较 $dx^j$ 的系数，我们得到：
$$
\omega_j = \sum_i \omega'_i J^i{}_j \quad \text{或矩阵形式} \quad \omega = J^T \omega'
$$
解出 $\omega'$，我们得到余向量分量的变换法则：
$$
\omega' = (J^T)^{-1} \omega = (J^{-1})^T \omega
$$
这个变换法则被称为**共变**（covariant）法则。余向量分量的变换矩阵是雅可比矩阵的逆转置。这一关键区别是区分[向量和余向量](@entry_id:181128)的根本原因 [@problem_id:2994058]。尽管变换法则不同，但它们的配对值在坐标变换下是不变的：$\omega'^T v' = (\omega^T J^{-1}) (J v) = \omega^T v$。这证实了配对是一个内在的、与坐标无关的几何运算。

让我们通过一个具体的例子来理解这些变换。考虑单位球面 $S^2$，我们可以用两个球极投影[坐标卡](@entry_id:262338)来覆盖它。从北极投影的坐标为 $(u,v)$，从南极投影的坐标为 $(U,V)$。在两个[坐标卡](@entry_id:262338)的重叠区域，坐标变换函数为 $\tau(u,v) = (U,V) = \left(\frac{u}{u^2+v^2}, \frac{v}{u^2+v^2}\right)$。[切丛](@entry_id:161294)的**过渡函数**（transition function）就是这个变换的[雅可比矩阵](@entry_id:264467) $J=D\tau$。经过计算可得 [@problem_id:3004639]：
$$
J(u,v) = \begin{pmatrix} \frac{\partial U}{\partial u}  \frac{\partial U}{\partial v} \\ \frac{\partial V}{\partial u}  \frac{\partial V}{\partial v} \end{pmatrix} = \begin{pmatrix} \frac{v^2 - u^2}{(u^2 + v^2)^2}  \frac{-2uv}{(u^2 + v^2)^2} \\ \frac{-2uv}{(u^2 + v^2)^2}  \frac{u^2 - v^2}{(u^2 + v^2)^2} \end{pmatrix}
$$
这个矩阵的行列式为 $-\frac{1}{(u^2+v^2)^2}$，在定义域上恒不为零。这意味着在每一点，这个变换都是可逆的，矩阵属于[一般线性群](@entry_id:141275) $\mathrm{GL}(2, \mathbb{R})$。这确保了我们可以一致地在不同坐标卡之间粘合[切空间](@entry_id:199137)，从而形成一个光滑的[切丛](@entry_id:161294)。

### 几何结构的角色

我们已经看到[向量和余向量](@entry_id:181128)在[坐标变换](@entry_id:172727)下表现出不同的行为。这引出了一个深刻的问题：是否存在一种“自然的”或“典范的”方式来等同 $T_p M$ 和 $T_p^*M$？这里的“自然”意味着这种等同不依赖于任何任意的选择，比如[坐标系](@entry_id:156346)的选择。从纯代数的角度看，这意味着我们需要一个在[一般线性群](@entry_id:141275) $\mathrm{GL}(V)$ 作用下等变的同构 $\Phi: V \to V^*$。

答案是否定的。可以证明，任何这样的“自然”同构都必须对应一个在所有线性变换下都不变的[双线性形式](@entry_id:746794)。然而，除了零形式之外，唯一满足此条件的只有零形式，而零形式是退化的，无法给出同构。这个论证，特别是通过考虑简单的缩放变换，表明在没有额外结构的情况下，[向量空间](@entry_id:151108) $V$ 和其对偶空间 $V^*$ 之间不存在[典范同构](@entry_id:202335) [@problem_id:2994032]。

这正是**黎曼度量**（Riemannian metric）登场的地方。一个[黎曼度量](@entry_id:754359) $g$ 为[流形](@entry_id:153038) $M$ 上的每一点 $p$ 提供了一个切空间 $T_p M$ 上的**[内积](@entry_id:158127)**（即一个对称、正定的非退化双线性形式）$g_p$。正是这个度量 $g$ 提供了我们所需要的“额外结构”。

给定度量 $g$，我们可以定义两个互逆的同构，称为**[音乐同构](@entry_id:199976)**（musical isomorphisms）：
1.  **降号**（flat）映射 $\flat: T_p M \to T_p^* M$，它将一个向量 $v$ 映射到一个余向量 $v^\flat$，定义为 $v^\flat(w) = g_p(v, w)$ 对于所有 $w \in T_p M$。
2.  **升号**（sharp）映射 $\sharp: T_p^* M \to T_p M$，它是降号映射的逆。它将一个余向量 $\omega$ 映射到唯一一个满足 $g_p(\omega^\sharp, w) = \omega(w)$ 对所有 $w \in T_p M$ 成立的向量 $\omega^\sharp$。

这两个同构之所以重要，是因为它们在[向量和余向量](@entry_id:181128)之间建立了一座桥梁。然而，这座桥梁的建造依赖于度量 $g$ 这个“蓝图”。如果更换度量，那么这座桥梁也会随之改变 [@problem_id:2994005]。

例如，在 $\mathbb{R}^2$ 的原点，考虑余向量 $\omega = dx+dy$。如果使用标准的[欧几里得度量](@entry_id:147197) $g = dx^2 + dy^2$，其度量矩阵为单位阵 $I$，那么 $\omega^\sharp = \partial_x + \partial_y$。但如果使用另一个度量 $h$，其度量矩阵为 $\mathrm{diag}(2,1)$，那么通过求解 $H v = \omega$ 得到 $v=(\frac{1}{2},1)$，即相对于度量 $h$，$\omega^\sharp = \frac{1}{2}\partial_x + \partial_y$。这个简单的例子清晰地表明，[音乐同构](@entry_id:199976)是依赖于度量的 [@problem_id:2994041]。

在[局部坐标](@entry_id:181200)中，升号映射有一个方便的表达式。如果度量张量的分量为 $g_{ij}$，其逆矩阵的分量为 $g^{ij}$，那么[余向量](@entry_id:157727) $\omega = \omega_i dx^i$ 对应的向量 $\omega^\sharp = v^j \partial_j$ 的分量由下式给出：
$$
v^j = \sum_i g^{ji}(p) \omega_i
$$
这个公式在[黎曼几何](@entry_id:160508)的计算中无处不在 [@problem_id:2994041]。

有了[音乐同构](@entry_id:199976)，我们现在可以精确地定义函数的**梯度**（gradient）。一个[光滑函数](@entry_id:267124) $f$ 的梯度 $\nabla f$ 是一个向量场，它由 $f$ 的[微分](@entry_id:158718) $df$ 通过升号映射得到：
$$
\nabla f := (df)^\sharp
$$
换言之，梯度是唯一满足 $g(\nabla f, X) = df(X)$ 对所有向量场 $X$ 成立的向量场。这澄清了一个常见的误解：[微分](@entry_id:158718) $df$ 是一个[余向量](@entry_id:157727)场，而梯度 $\nabla f$ 是一个向量场。它们通过度量 $g$ 相互关联 [@problem_id:2994005]。

### 应用与进阶主题

#### 映射的[拉回](@entry_id:160816)

切空间和[余切空间](@entry_id:270516)的一个重要应用是描述[流形间的映射](@entry_id:158221)如何影响其上的几何对象。给定一个[光滑映射](@entry_id:203730) $F: M \to N$，它在点 $p$ 的**[微分](@entry_id:158718)**（或**[前推](@entry_id:158718)**）是一个线性映射 $dF_p: T_p M \to T_{F(p)} N$。这个映射描述了 $F$ 如何变换切向量。

对偶地，我们可以定义[余向量](@entry_id:157727)的**[拉回](@entry_id:160816)**（pullback）。给定 $N$ 上的一个余向量 $\alpha \in T_{F(p)}^* N$，它被 $F$ [拉回](@entry_id:160816)到 $M$ 上成为一个余向量 $(F^*\alpha)_p \in T_p^*M$。其定义如下：对于任意 $v \in T_p M$，
$$
(F^*\alpha)_p(v) := \alpha(dF_p(v))
$$
这个操作本质上是通过[前推](@entry_id:158718)映射 $dF_p$ 将 $v$ “推送”到 $N$ 上，然后再用 $\alpha$ 作用于其上。这是一种通过与 $F$ 的线性近似 $dF_p$ 进行预复合来“测量” $F$ 的方式 [@problem_id:2994005]。[拉回运算](@entry_id:753859)的一个重要性质是它与[外微分](@entry_id:161900)的[可交换性](@entry_id:263314)，例如，对于函数 $h: N \to \mathbb{R}$，我们有链式法则的优雅形式：$d(h \circ F) = F^*(dh)$ [@problem_id:2994005]。

#### [带边流形](@entry_id:159788)上的[切空间](@entry_id:199137)

最后，我们简要讨论一个特殊但重要的情形：[带边流形](@entry_id:159788)。令 $M$ 为一个 $n$ 维[带边流形](@entry_id:159788)，其边界为 $\partial M$。
当一个点 $p$ 位于边界 $\partial M$ 上时，[切空间](@entry_id:199137) $T_p M$ 的定义仍然有效，并且其维数**仍然是 $n$**。一个常见的误解是认为[边界点](@entry_id:176493)的[切空间维数](@entry_id:275897)会减少，但这混淆了[流形](@entry_id:153038) $M$ 的切空间 $T_p M$（$n$ 维）和边界[子流形](@entry_id:159439) $\partial M$ 的[切空间](@entry_id:199137) $T_p(\partial M)$（$n-1$ 维）。后者是前者的一个[子空间](@entry_id:150286)。

在边界点 $p$，我们可以区分指向[流形](@entry_id:153038)“内部”的向量。这些**内指向量**（inward-pointing vectors）的集合构成 $T_p M$ 中的一个闭[半空间](@entry_id:634770)，而不是一个[线性子空间](@entry_id:151815)。这个[半空间](@entry_id:634770)可以用两种等价的方式来描述 [@problem_id:3004653]：
1.  如果[流形](@entry_id:153038)由一个定义函数 $\rho$ 给出，即 $M = \{q \mid \rho(q) \ge 0\}$，那么内指向量集为 $\{v \in T_p M \mid d\rho_p(v) \ge 0\}$。其中 $T_p(\partial M)$ 恰好是 $d\rho_p$ 的核。
2.  如果[流形](@entry_id:153038)赋有黎曼度量 $g$，设 $\nu_p$ 是指向内部的[单位法向量](@entry_id:178851)，那么内指向量集为 $\{v \in T_p M \mid g_p(v, \nu_p) \ge 0\}$。

这些概念在研究涉及边界的物理理论（如广义相对论中的[视界](@entry_id:746488)）和[几何分析](@entry_id:157700)中的边值问题时至关重要。

本章通过建立切空间和[余切空间](@entry_id:270516)的基本原理与机制，为深入学习黎曼几何的更高级主题，如联络、曲率和积分理论，奠定了坚实的基础。