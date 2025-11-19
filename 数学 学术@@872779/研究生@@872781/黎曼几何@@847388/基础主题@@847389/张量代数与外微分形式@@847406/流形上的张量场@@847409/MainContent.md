## 引言
在探索从[行星轨道](@entry_id:179004)到宇宙膨胀等物理现象，或是在研究[曲面](@entry_id:267450)的纯粹几何形态时，我们不可避免地要从平直的[欧几里得空间](@entry_id:138052)进入更广阔的弯曲空间——即光滑流形的世界。然而，我们熟悉的矢量、梯度、导数等概念在这些弯曲空间中将如何定义？我们如何确保物理定律的表达形式不依赖于观察者选择的任意[坐标系](@entry_id:156346)？答案在于一个强大而普适的数学语言：[张量场](@entry_id:190170)。

本文旨在系统地揭开[流形](@entry_id:153038)上[张量场](@entry_id:190170)的面纱，填补从基础[流形理论](@entry_id:263722)到高级几何与物理应用的知识鸿沟。我们将阐明，张量并非仅仅是带有复杂指标的抽象符号，而是描述局部几何与物理性质的、内在的、不依赖于坐标的数学实体。

在接下来的章节中，你将踏上一段结构清晰的学习之旅。在**“原理与机制”**一章中，我们将建立张量场的坚实基础，从其作为[多重线性映射](@entry_id:274221)的精确定义，到其在[坐标系](@entry_id:156346)下的变换规则，并最终引入协变导数这一核心微积分工具。随后，在**“应用与跨学科联系”**一章，我们将展示这些抽象理论的巨大威力，看它们如何作为几何的基石描述距离与曲率，如何揭示[物理学中的对称性](@entry_id:144576)与守恒律，以及如何在广义相对论等前沿领域扮演不可或缺的角色。最后，通过**“动手实践”**中的一系列计算练习，你将有机会亲手应用所学知识，将理论转化为具体的计算技能，从而真正内化对张量场的理解。

## 原理与机制

本章旨在系统地阐述[流形](@entry_id:153038)上[张量场](@entry_id:190170)的核心原理与机制。在前一章引入了[光滑流形](@entry_id:160799)的基本概念之后，我们现在将注意力转向定义在这些[流形](@entry_id:153038)上的关键几何对象——张量。我们将从张量的代数定义出发，逐步探讨其坐标表示、基本运算，并最终深入研究[微分](@entry_id:158718)运算，这些构成了黎曼几何的基石。

### 张量的再审视：[多重线性映射](@entry_id:274221)的视角

在深入探讨[张量场](@entry_id:190170)之前，我们必须首先在[流形](@entry_id:153038)的每一点上精确地定义张量。给定一个光滑流形 $M$ 和其上一点 $p$，我们已经熟悉了该点的切空间 $T_pM$（一个[向量空间](@entry_id:151108)）和其对偶空间，即[余切空间](@entry_id:270516) $T_p^*M$。

一个在点 $p$ 的 **$(r,s)$ 型张量**（tensor of type $(r,s)$）最形式化的定义是张量积空间中的一个元素：
$$
T_p^{r,s} M \coloneqq \underbrace{T_p M \otimes \cdots \otimes T_p M}_{r \text{ 个}} \otimes \underbrace{T_p^* M \otimes \cdots \otimes T_p^* M}_{s \text{ 个}}
$$
其中 $\otimes$ 表示[向量空间](@entry_id:151108)之间的[张量积](@entry_id:140694)。这种定义虽然在代数上是精确的，但在几何和物理应用中，另一种等价的观点往往更为直观和实用。

通过[张量积的泛性质](@entry_id:150937)，可以证明上述张量空间与一个特定的[多重线性映射](@entry_id:274221)空间之间存在一个**[典范同构](@entry_id:202335)**（canonical isomorphism）。具体来说，一个 $(r,s)$ 型张量可以被等同地视为一个[多重线性映射](@entry_id:274221)，它以 $r$ 个余向量（covectors）和 $s$ 个切向量（tangent vectors）为输入，并返回一个实数 [@problem_id:2992324] [@problem_id:2992314]。即：
$$
T^{r,s}_{p}M \;\cong\; \operatorname{Mult}\big((T_{p}^{*}M)^{\times r} \times (T_{p}M)^{\times s}, \mathbb{R}\big)
$$
其中 $\operatorname{Mult}$ 代表[多重线性映射](@entry_id:274221)的空间。在这个视角下，一个张量 $T \in T^{r,s}_{p}M$ 是一个函数 $T(\omega^1, \dots, \omega^r, v_1, \dots, v_s)$，它在每一个参数上都是线性的。例如，一个 $(1,2)$ 型张量 $T$ 会接受一个余向量 $\omega$ 和两个向量 $v_1, v_2$，并给出一个实数 $T(\omega, v_1, v_2)$。这种将张量视为“输入[向量和余向量](@entry_id:181128)，输出标量”的机器的观点，是理解张量在坐标变换下行为的关键。

值得强调的是，切空间 $T_pM$ 和[余切空间](@entry_id:270516) $T_p^*M$ 虽然维度相同，但它们之间**不存在**一个独立于任何额外选择的[典范同构](@entry_id:202335) [@problem_id:2992321]。区分向量（[逆变张量](@entry_id:636697)）和余向量（[协变张量](@entry_id:634493)）是[张量分析](@entry_id:161423)的根本。只有在引入了诸如黎曼度规之类的附加结构后，我们才能在这两个空间之间建立一个特定的（但非唯一的）同构。

### [张量场](@entry_id:190170)及其坐标表示

现在，我们将逐点的张量概念扩展到整个[流形](@entry_id:153038)。一个 **$(r,s)$ 型[张量场](@entry_id:190170)**（tensor field of type $(r,s)$）是[流形](@entry_id:153038) $M$ 上的一个光滑剖切（smooth section），它为 $M$ 上的每一个点 $p$ 指定一个该点的 $(r,s)$ 型张量 $T_p$。我们将所有这些逐点的张量空间 $T^{r,s}_p M$ 的不交并集记为 $\mathrm{T}^{r,s}M$，这个集合本身具有一个光滑向量丛的结构，称为**[张量丛](@entry_id:203012)**（tensor bundle）[@problem_id:2992314]。一个张量场就是这个丛的一个光滑剖切。在微分几何中，除非特别说明，我们默认所有对象（包括[张量场](@entry_id:190170)）都是光滑的（$C^\infty$）。

为了进行具体计算，我们通常在[局部坐标](@entry_id:181200)卡 $(U, (x^1, \dots, x^n))$ 中工作。在此坐标卡中，[切空间](@entry_id:199137) $T_pM$ 有一组自然的基底，即[坐标向量](@entry_id:153319)场 $\left\{\partial_i \equiv \frac{\partial}{\partial x^i}\right\}$。相应地，[余切空间](@entry_id:270516) $T_p^*M$ 有其对偶基底 $\left\{\mathrm{d}x^j\right\}$，其定义满足**对偶关系** [@problem_id:2992321]：
$$
\mathrm{d}x^j\left(\frac{\partial}{\partial x^i}\right) = \delta^j_i
$$
其中 $\delta^j_i$ 是克罗内克（Kronecker）δ。

利用这些基底，任何一个 $(r,s)$ 型张量场 $T$ 可以在该[坐标卡](@entry_id:262338)覆盖的区域内被分解为：
$$
T = T^{i_1 \dots i_r}_{j_1 \dots j_s} \; \partial_{i_1} \otimes \cdots \otimes \partial_{i_r} \otimes \mathrm{d}x^{j_1} \otimes \cdots \otimes \mathrm{d}x^{j_s}
$$
其中 $T^{i_1 \dots i_r}_{j_1 \dots j_s}$ 是定义在 $U$ 上的光滑函数，称为 $T$ 在此[坐标系](@entry_id:156346)下的**分量**（components）。这里我们采用了爱因斯坦求和约定，即成对出现的同名上下指标表示对该指标从 $1$ 到 $n$ 求和。

张量之所以是几何对象，关键在于其分量在[坐标变换](@entry_id:172727)下的特定**变换法则**（transformation law）。考虑另一个交叠的[坐标系](@entry_id:156346) $(x'^1, \dots, x'^n)$。根据[链式法则](@entry_id:190743)，新旧[坐标基](@entry_id:270149)底之间的关系是：
$$
\partial'_{p} = \frac{\partial x^{i}}{\partial x'^{p}}\,\partial_{i} \quad \text{以及} \quad \mathrm{d}x'^{q} = \frac{\partial x'^{q}}{\partial x^{j}}\,\mathrm{d}x^{j}
$$
由于[张量场](@entry_id:190170) $T$ 本身是一个不依赖于[坐标系](@entry_id:156346)的几何实体，它在两个[坐标系](@entry_id:156346)下的表达式必须相等。这导出了其分量的变换法则。例如，对于一个 $(1,1)$ 型张量 $A = A^i_j \partial_i \otimes \mathrm{d}x^j = A'^p_q \partial'_p \otimes \mathrm{d}x'^q$，其分量变换法则为 [@problem_id:2992335]：
$$
A'^p_q = \frac{\partial x'^p}{\partial x^i} \frac{\partial x^j}{\partial x'^q} A^i_j
$$
一般地，对于一个 $(r,s)$ 型张量，每个逆变（上）指标的变换都乘以一个雅可比矩阵 $J = (\frac{\partial x'}{\partial x})$ 的因子，而每个[协变](@entry_id:634097)（下）指标的变换则乘以其[逆矩阵](@entry_id:140380) $J^{-1} = (\frac{\partial x}{\partial x'})$ 的因子 [@problem_id:2992321] [@problem_id:2992314]。

**例：$(0,2)$ 型张量的[坐标变换](@entry_id:172727)** [@problem_id:2992312]

考虑 $\mathbb{R}^2$ 上的一个 $(0,2)$ 型[张量场](@entry_id:190170) $T$，它在笛卡尔坐标 $(x,y)$ 下由下式给出：
$$
T=(2x^{2}+3xy)\,\mathrm{d}x\otimes \mathrm{d}x + (x^{2}-y^{2})\,(\mathrm{d}x\otimes \mathrm{d}y+\mathrm{d}y\otimes \mathrm{d}x) + (4xy+y^{2})\,\mathrm{d}y\otimes \mathrm{d}y
$$
我们希望计算其在极坐标 $(r, \theta)$ 下的分量 $T_{\theta\theta}$，其中 $x=r\cos\theta, y=r\sin\theta$。根据定义，$T_{\theta\theta} = T(\partial_\theta, \partial_\theta)$。首先，我们用链式法则将 $\partial_\theta$ 用笛卡尔基底表示：
$$
\partial_{\theta}=\frac{\partial x}{\partial \theta}\,\partial_{x}+\frac{\partial y}{\partial \theta}\,\partial_{y} = (-r\sin\theta)\partial_{x}+(r\cos\theta)\partial_{y}
$$
由于 $T$ 是双线性的，我们有：
$$
T(\partial_\theta, \partial_\theta) = T_{xx} \left(\frac{\partial x}{\partial \theta}\right)^2 + 2T_{xy} \left(\frac{\partial x}{\partial \theta}\right)\left(\frac{\partial y}{\partial \theta}\right) + T_{yy} \left(\frac{\partial y}{\partial \theta}\right)^2
$$
此公式本质上就是 $(0,2)$ 型张量的变换法则 $T'_{\alpha\beta} = \frac{\partial x^i}{\partial x'^\alpha} \frac{\partial x^j}{\partial x'^\beta} T_{ij}$ 的具体应用。
假设我们关注点 $(r, \theta) = (2, \pi/3)$。该点笛卡尔坐标为 $(x,y) = (1, \sqrt{3})$。
在该点，$\frac{\partial x}{\partial \theta} = -r\sin\theta = -2(\sqrt{3}/2) = -\sqrt{3}$，$\frac{\partial y}{\partial \theta} = r\cos\theta = 2(1/2) = 1$。
$T$ 在[笛卡尔坐标](@entry_id:167698)下的分量为：
$T_{xx} = 2(1)^2+3(1)(\sqrt{3}) = 2+3\sqrt{3}$
$T_{xy} = T_{yx} = 1^2 - (\sqrt{3})^2 = -2$
$T_{yy} = 4(1)(\sqrt{3}) + (\sqrt{3})^2 = 4\sqrt{3}+3$
代入变换公式，我们得到：
$$
T_{\theta\theta} = (2+3\sqrt{3})(-\sqrt{3})^2 + 2(-2)(-\sqrt{3})(1) + (4\sqrt{3}+3)(1)^2 = (6+9\sqrt{3}) + 4\sqrt{3} + (3+4\sqrt{3}) = 9 + 17\sqrt{3}
$$
这个计算具体地展示了张量分量如何依赖于[坐标系](@entry_id:156346)，以及它们之间如何通过雅可比矩阵相互关联。

最后，有一个优雅的、不依赖坐标的判别张量场光滑性的方法，即**张量光滑性判据**：一个剖切 $T: M \to \mathrm{T}^{r,s}M$ 是光滑的，当且仅当对于任意光滑的余向量场 $\omega^1, \dots, \omega^r$ 和任意光滑的向量场 $X_1, \dots, X_s$，标量函数 $p \mapsto T_p(\omega^1_p, \dots, X_{s,p})$ 是光滑的 [@problem_id:2992314] [@problem_id:2992321]。

### 张量场的基本运算

[张量代数](@entry_id:161671)的核心运算可以自然地推广到[张量场](@entry_id:190170)。

**[张量积](@entry_id:140694)（Tensor Product）**：两个张量场 $T_1$ 和 $T_2$ 的张量积 $(T_1 \otimes T_2)$ 是一个更高阶的张量场，其在每一点 $p$ 的值就是 $T_{1,p} \otimes T_{2,p}$。这是构造复杂张量场的基本方法。

**缩并（Contraction）**：缩并是一种降低张量阶数的操作，它将一个[逆变](@entry_id:192290)指标和一个协变指标“配对”并求和。最简单的例子是 $(1,1)$ 型张量 $A = A^i_j \partial_i \otimes \mathrm{d}x^j$ 的**迹**（trace）。其迹定义为 $\operatorname{tr}(A) = A^i_i$。一个至关重要的问题是：这个定义是否依赖于[坐标系](@entry_id:156346)？答案是不依赖。我们可以证明 $\operatorname{tr}(A)$ 是一个标量场，即在坐标变换下不变。利用前述 $A^i_j$ 的变换法则，我们有 [@problem_id:2992335]：
$$
A'^p_p = \frac{\partial x'^p}{\partial x^i} \frac{\partial x^j}{\partial x'^p} A^i_j = \left(\frac{\partial x^j}{\partial x'^p} \frac{\partial x'^p}{\partial x^i}\right) A^i_j = \frac{\partial x^j}{\partial x^i} A^i_j = \delta^j_i A^i_j = A^i_i
$$
这表明缩并是一个内在的、几何的运算。

**对称性（Symmetries）**：我们可以讨论张量在交换其协变指标或逆变指标时的行为。例如，一个 $(0,2)$ 型张量 $T$ 是**对称的**（symmetric）如果 $T(v_1, v_2) = T(v_2, v_1)$，或等价地 $T_{ij}=T_{ji}$；它是**反对称的**（antisymmetric）如果 $T(v_1, v_2) = -T(v_2, v_1)$，或 $T_{ij}=-T_{ji}$。特别地，一个全反对称的[协变张量](@entry_id:634493)场被称为**[微分形式](@entry_id:146747)**（differential form）。对于一个 $k$-形式 $\omega$，其反对称性意味着对于任意[置换](@entry_id:136432) $\sigma \in S_k$，有 $\omega(v_{\sigma(1)}, \dots, v_{\sigma(k)}) = \operatorname{sgn}(\sigma) \omega(v_1, \dots, v_k)$，这等价于当任意两个输入向量相同时，$\omega$ 的值为零 [@problem_id:2992324]。
然而，混合协变和逆变指标的对称性（例如，假设 $T^i_j = T^j_i$）在没有附加结构的情况下是**没有意义的**。这样的性质在[坐标变换](@entry_id:172727)下通常不被保持，因此它不是一个张量性质。要比较一个[逆变](@entry_id:192290)指标和一个[协变](@entry_id:634097)指标，我们需要一个在 $T_pM$ 和 $T_p^*M$ 之间的同构，而这正是[度规张量](@entry_id:160222)所提供的 [@problem_id:2992324]。

**[拉回](@entry_id:160816)（Pullback）**：给定一个[光滑映射](@entry_id:203730) $f: M \to N$ 和 $N$ 上的一个[协变张量](@entry_id:634493)场 $\beta$（例如一个 $1$-形式），我们可以定义 $M$ 上的一个新张量场，称为 $\beta$ 通过 $f$ 的**[拉回](@entry_id:160816)**，记作 $f^*\beta$。对于 $1$-形式，其定义为 [@problem_id:2992321]：
$$
(f^*\beta)_p(v) = \beta_{f(p)}(df_p(v)) \quad \text{for all } v \in T_pM
$$
其中 $df_p: T_pM \to T_{f(p)}N$ 是 $f$ 在 $p$ 点的[微分](@entry_id:158718)（或[前推](@entry_id:158718)）。几何上，这相当于将在 $N$ 上的测量（由 $\beta$ 给出）“[拉回](@entry_id:160816)”到 $M$ 上。

### 度规张量的角色

到目前为止，我们讨论的结构都是[流形](@entry_id:153038)固有的。现在我们引入一个对几何至关重要的附加结构。

一个**黎曼度规**（Riemannian metric）$g$ 是一个光滑的、对称的、正定的 $(0,2)$ 型[张量场](@entry_id:190170) [@problem_id:2992334]。
- **光滑**和**对称**意味着 $g$ 是一个光滑[张量场](@entry_id:190170)且在每个点 $p$ 都有 $g_p(v,w) = g_p(w,v)$。
- **正定**意味着对于任意非[零向量](@entry_id:156189) $v \in T_pM$，都有 $g_p(v,v) > 0$。

度规在每个[切空间](@entry_id:199137) $T_pM$ 上定义了一个[内积](@entry_id:158127)。这使得我们可以定义向量的**长度**（$\|v\| = \sqrt{g_p(v,v)}$）和两个向量之间的**夹角**。如果去掉[正定性](@entry_id:149643)，只要求 $g$ 在每个点上是**非退化**的（即若 $g_p(v,w)=0$ 对所有 $w$ 成立，则必有 $v=0$），我们就得到一个**伪黎曼度规**（pseudo-Riemannian metric），这是广义相对论的数学基础。

度规最重要的功能之一是它提供了切空间和[余切空间](@entry_id:270516)之间的**[音乐同构](@entry_id:199976)**（musical isomorphisms） [@problem_id:2992334]。
- **降号（flat）** 映射 $\flat: TM \to T^*M$ 将一个向量 $v$ 映射到一个余向量 $v^\flat$，定义为 $v^\flat(w) = g(v,w)$。
- **升号（sharp）** 映射 $\sharp: T^*M \to TM$ 是其逆映射，它将一个[余向量](@entry_id:157727) $\omega$ 映射到一个唯一的向量 $\omega^\sharp$，满足 $g(\omega^\sharp, w) = \omega(w)$ 对所有 $w$ 成立。

这些同构完全依赖于度规 $g$ 的选择 [@problem_id:2992321]。它们允许我们在[逆变和协变张量](@entry_id:197629)之间进行转换，也就是俗称的“[升降指标](@entry_id:161292)”。

**例：函数的梯度** [@problem_id:2992333]

度规的一个直接应用是定义光滑函数 $f: M \to \mathbb{R}$ 的**梯度**（gradient）。[函数的微分](@entry_id:274991) $\mathrm{d}f$ 是一个 $1$-形式（即 $(0,1)$ 型张量场）。梯度向量场 $\nabla f$（或 $\operatorname{grad}f$）被定义为 $\mathrm{d}f$ 在升号映射下的像：
$$
\nabla f \coloneqq (\mathrm{d}f)^\sharp
$$
根据定义，$\nabla f$ 是唯一满足下式的向量场：
$$
g(\nabla f, X) = \mathrm{d}f(X) = X(f)
$$
对任意向量场 $X$ 成立。要在[局部坐标](@entry_id:181200)中计算 $\nabla f$，我们写出 $\nabla f = (\nabla f)^i \partial_i$。则 $g(\nabla f, X) = g_{ij}(\nabla f)^i X^j$。而 $\mathrm{d}f(X) = (\partial_j f) X^j$。由于这对所有 $X$ 都成立，我们得到 $g_{ij}(\nabla f)^i = \partial_j f$。
令 $g^{ik}$ 为度规矩阵 $(g_{ij})$ 的逆矩阵的分量，我们解出梯度的分量为：
$$
(\nabla f)^k = g^{kj} \partial_j f
$$
这个公式清楚地显示了梯度依赖于度规。例如，在 $\mathbb{R}^2$ 上赋予度规 $g = (1+x^2)\mathrm{d}x^2 + xy(\mathrm{d}x\otimes \mathrm{d}y + \mathrm{d}y\otimes \mathrm{d}x) + (1+y^2)\mathrm{d}y^2$，函数 $f(x,y)=x^2 y+\sin(xy)$ 的梯度可以通过计算逆矩阵 $g^{ij}$ 和[偏导数](@entry_id:146280) $\partial_j f$ 并应用上述公式得到，这将得到一个相当复杂的表达式，与欧几里得空间中的梯度 $(\partial_x f, \partial_y f)$ 大相径庭。

### [张量场](@entry_id:190170)的[微分](@entry_id:158718)

[流形](@entry_id:153038)上[张量分析](@entry_id:161423)的核心挑战是如何对[张量场](@entry_id:190170)进行[微分](@entry_id:158718)。简单地对张量分量求[偏导数](@entry_id:146280)通常不会得到一个张量，因为这样得到的量在坐标变换下的行为不符合[张量变换法则](@entry_id:185176)。

**例：克里斯托费尔符号的非张量性** [@problem_id:1543267]
考虑一个联络（connection）$\nabla$，它定义了向量场如何相互[微分](@entry_id:158718)。在[局部坐标](@entry_id:181200)中，这由**[克里斯托费尔符号](@entry_id:159831)**（Christoffel symbols）$\Gamma^k_{ij}$ 描述，其定义为 $\nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k$。如果 $\Gamma^k_{ij}$ 是一个 $(1,2)$ 型张量的分量，那么在[坐标变换](@entry_id:172727)下，它应该遵循[张量变换法则](@entry_id:185176)。然而，直接计算表明其变换法则是：
$$
\bar{\Gamma}^k_{ij} = \frac{\partial \bar{x}^k}{\partial x^m} \frac{\partial x^p}{\partial \bar{x}^i} \frac{\partial x^q}{\partial \bar{x}^j} \Gamma^m_{pq} + \frac{\partial \bar{x}^k}{\partial x^m} \frac{\partial^2 x^m}{\partial \bar{x}^i \partial \bar{x}^j}
$$
这个额外的、涉及坐标[二阶偏导数](@entry_id:635213)的项表明 $\Gamma^k_{ij}$ **不是一个张量**。这也揭示了为什么分量的偏导数不是张量性的：它缺少一个用[克里斯托费尔符号](@entry_id:159831)来“修正”的项。这启发我们定义两种内在的、几何的[微分](@entry_id:158718)方式。

#### 李导数

**[李导数](@entry_id:171745)**（Lie derivative）$\mathcal{L}_X T$ 测量了张量场 $T$ 沿着向量场 $X$ 的流（flow）的无穷小变化。它是一种不依赖于任何附加结构（如度规或联络）的自然导数。
其基本性质包括：
- 对标量函数 $f$，$\mathcal{L}_X f = X(f)$。
- 对向量场 $Y$，$\mathcal{L}_X Y = [X,Y]$，即[李括号](@entry_id:636461)。
- 它对张量积满足[莱布尼茨法则](@entry_id:157949)。

利用这些性质，我们可以推导出[李导数](@entry_id:171745)作用于一个一般 $(r,s)$ 型张量 $T$ 的分量表达式 [@problem_id:2992300]：
$$
(\mathcal{L}_{X}T)^{i_{1}\cdots i_{r}}_{j_{1}\cdots j_{s}} = X^{k}\partial_{k}T^{i_{1}\cdots i_{r}}_{j_{1}\cdots j_{s}} - \sum_{p=1}^{r}T^{i_{1}\cdots \alpha \cdots i_{r}}_{j_{1}\cdots j_{s}}\partial_{\alpha}X^{i_{p}} + \sum_{q=1}^{s}T^{i_{1}\cdots i_{r}}_{j_{1}\cdots \beta \cdots j_{s}}\partial_{j_{q}}X^{\beta}
$$
第一项是沿 $X$ 的[方向导数](@entry_id:189133)。其余的项是“修正项”，它们解释了[坐标系](@entry_id:156346)本身如何被 $X$ 的流拖拽。

#### [协变导数](@entry_id:152476)

与李导数不同，**[协变导数](@entry_id:152476)**（covariant derivative）需要一个**[仿射联络](@entry_id:160152)**（affine connection）$\nabla$。在黎曼流形 $(M,g)$ 上，有一个唯一的、与度规 $g$ 兼容（$\nabla g = 0$）且无挠（torsion-free）的联络，称为**列维-奇维塔联络**（Levi-Civita connection）[@problem_id:2992334]。这是黎曼几何中的标准导数。

给定一个 $(r,s)$ 型张量场 $T$，其[协变导数](@entry_id:152476) $\nabla T$ 是一个 $(r, s+1)$ 型[张量场](@entry_id:190170)。其分量记为 $\nabla_k T^{i_1\dots}_{j_1\dots}$。这个新张量场在每一个槽中都是 $C^\infty(M)$-线性的 [@problem_id:2992336]。利用联络的定义和[莱布尼茨法则](@entry_id:157949)，可以推导出其分量表达式 [@problem_id:2992336]：
$$
(\nabla_{\ell}T)^{i_{1}\dots i_{r}}{}_{j_{1}\dots j_{s}} = \partial_{\ell} T^{i_{1}\dots i_{r}}{}_{j_{1}\dots j_{s}} + \sum_{p=1}^{r} \Gamma^{i_{p}}_{\ell k} T^{i_{1}\dots k \dots i_{r}}{}_{j_{1}\dots j_{s}} - \sum_{q=1}^{s} \Gamma^{k}_{\ell j_{q}} T^{i_{1}\dots i_{r}}{}_{j_{1}\dots k \dots j_{s}}
$$
这个公式是[张量微积分](@entry_id:161423)的核心。它表明，张量场的协变导数的分量，是其普通[偏导数](@entry_id:146280)加上一系列涉及[克里斯托费尔符号](@entry_id:159831)的修正项。正是这些修正项，确保了 $\nabla T$ 的分量在[坐标变换](@entry_id:172727)下表现为一个 $(r, s+1)$ 型张量。[协变导数](@entry_id:152476)推广了欧几里得空间中沿某方向的方向导数的概念，并允许我们讨论平行输运、[测地线](@entry_id:269969)和曲率等核心几何概念。

总之，张量场为描述[流形](@entry_id:153038)上的几何和物理量提供了统一的语言。它们的[代数结构](@entry_id:137052)通过[张量积](@entry_id:140694)和缩并来体现，而它们的分析性质则由[李导数](@entry_id:171745)和[协变导数](@entry_id:152476)来刻画。[度规张量](@entry_id:160222)的引入，通过建立切空间和[余切空间](@entry_id:270516)之间的联系并定义几何测量，极大地丰富了这一理论框架。