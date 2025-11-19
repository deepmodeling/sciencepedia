## 引言
[李群](@entry_id:137659)作为[光滑流形](@entry_id:160799)与群结构的完美融合，在现代数学和物理学中扮演着核心角色。然而，要深入理解其丰富的几何内涵，我们必须拥有一套能够利用其内在对称性的强大工具。一个核心的挑战在于，如何将[流形](@entry_id:153038)上每一点的局部几何信息与群的整体[代数结构](@entry_id:137052)联系起来，从而将复杂的[非线性](@entry_id:637147)问题转化为更易于处理的代数问题。

本文正是为了解决这一问题，系统地介绍了[左不变向量场](@entry_id:637116)与[微分形式](@entry_id:146747)这一关键概念。这些对象利用[李群](@entry_id:137659)的左移对称性，构筑了一座连接[流形](@entry_id:153038)几何与[李代数](@entry_id:137954)代数的桥梁。通过学习本文，您将理解这种联系是如何建立的，以及它为何如此强大。

在“**原理与机制**”一章中，我们将从左移映射出发，严格定义[左不变向量场](@entry_id:637116)和[微分形式](@entry_id:146747)，并揭示它们如何由单位元处的信息（即李代数）完全确定。我们将探讨[李括号](@entry_id:636461)的[代数结构](@entry_id:137052)如何自然地出现在向量场上，并介绍核心的[Maurer-Cartan形式](@entry_id:196759)及其[结构方程](@entry_id:274644)。

随后，在“**应用与跨学科联系**”一章中，我们将展示这些理论工具的威力，看它们如何简化黎曼几何中的曲率计算，如何帮助我们理解紧[李群的[拓](@entry_id:191016)扑性质](@entry_id:141605)，以及如何在物理学和控制论中找到具体的应用。

最后，“**动手实践**”部分将通过一系列引导性问题，帮助您在具体的[李群](@entry_id:137659)（如[海森堡群](@entry_id:144785)和[SO(3)](@entry_id:138200)）上巩固所学知识，将抽象理论转化为坚实的计算能力。

## 原理与机制

在上一章介绍[李群](@entry_id:137659)作为光滑流形与群结构的融合之后，本章将深入探讨其微分几何的核心工具：[左不变向量场](@entry_id:637116)与微分形式。这些对象利用李[群的对称性](@entry_id:136707)，将[流形](@entry_id:153038)上每一点的[切空间](@entry_id:199137)与[单位元处的切空间](@entry_id:266468)（即[李代数](@entry_id:137954)）联系起来，从而将复杂的[全局分析](@entry_id:188294)问题转化为[李代数](@entry_id:137954)上的线性代数问题。本章将系统阐述这些工具的定义、性质及其在几何学中的深刻应用。

### 左移及其[微分](@entry_id:158718)

[李群](@entry_id:137659) $G$ 的群结构允许我们定义作用于其自身的标准变换。对任意固定的群元素 $g \in G$，**左移 (left translation)** 映射 $L_g: G \to G$ 定义为 $L_g(h) = gh$。由于[李群](@entry_id:137659)的乘法运算 $(g, h) \mapsto gh$ 被公理化地要求为[光滑映射](@entry_id:203730)，因此对于每一个固定的 $g$，映射 $L_g$ 都是一个[光滑映射](@entry_id:203730)。

更进一步，左移映射不仅仅是光滑的，它还是一个**微分同胚 (diffeomorphism)**。这意味着它是一个[双射](@entry_id:138092)，并且其自身和它的逆映射都是光滑的。要验证这一点，我们只需找到它的逆映射。对于任何 $k \in G$，方程 $gh=k$ 有唯一解 $h = g^{-1}k$。因此，$L_g$ 是[双射](@entry_id:138092)，其逆映射为 $(L_g)^{-1}(k) = g^{-1}k$。这个逆映射正是由 $g^{-1}$ 定义的左移，即 $(L_g)^{-1} = L_{g^{-1}}$。因为[李群](@entry_id:137659)的求逆运算 $g \mapsto g^{-1}$ 也是光滑的，所以 $L_{g^{-1}}$ 同样是一个[光滑映射](@entry_id:203730)。综上所述，$L_g$ 对任意 $g \in G$ 都是一个[微分同胚](@entry_id:147249) [@problem_id:3055547]。

作为[光滑映射](@entry_id:203730)，我们可以考察其在任意一点 $h \in G$ 的**[微分](@entry_id:158718) (differential)**（或称**[推前映射](@entry_id:160933) (pushforward)**），记为 $d(L_g)_h$ 或 $(L_g)_*$。这是一个从切空间 $T_h G$ 到 $T_{gh} G$ 的[线性同构](@entry_id:270529)。要理解这个[微分](@entry_id:158718)如何作用于一个切向量 $v \in T_hG$，我们可以通过光滑曲线来具象化切向量。设 $v$ 是通过点 $h$ 的一条光滑曲线 $\gamma: (-\varepsilon, \varepsilon) \to G$ 在 $t=0$ 时的速度向量，即 $\gamma(0)=h$ 且 $v = \frac{d}{dt}|_{t=0} \gamma(t)$。根据[微分](@entry_id:158718)的定义，向量 $d(L_g)_h(v)$ 就是复合曲线 $L_g \circ \gamma$ 在 $t=0$ 时的速度向量。该复合曲线的路径为 $t \mapsto L_g(\gamma(t)) = g\gamma(t)$。因此，[微分](@entry_id:158718)的作用可以明确地写为：
$$
d(L_g)_h(v) = \left.\frac{d}{dt}\right|_{t=0} \big(g\,\gamma(t)\big)
$$
这个表达式的几何意义是，$d(L_g)_h$ 将点 $h$ 处的一个速度向量，通过群乘法“平移”到了点 $gh$ 处的一个新的速度向量 [@problem_id:3055519]。由于 $L_g$ 是一个[微分同胚](@entry_id:147249)，它的[微分](@entry_id:158718) $d(L_g)_h$ 是一个[线性同构](@entry_id:270529)。这意味着它保留了[切空间](@entry_id:199137)的完整结构，是可逆的。利用[链式法则](@entry_id:190743)，我们可以确定其逆[映射的微分](@entry_id:269524)。因为 $(L_g)^{-1} \circ L_g = \text{id}_G$（$G$上的[恒等映射](@entry_id:634191)），对其[微分](@entry_id:158718)有 $d((L_g)^{-1})_{gh} \circ d(L_g)_h = \text{id}_{T_h G}$。这表明 $d((L_g)^{-1})_{gh}$ 正是 $d(L_g)_h$ 的逆线性映射，即：
$$
d\big((L_g)^{-1}\big)_{gh} = \big(d(L_g)_h\big)^{-1}
$$
结合 $(L_g)^{-1} = L_{g^{-1}}$，我们得到一个重要关系：$d(L_{g^{-1}})_{gh} = (d(L_g)_h)^{-1}$ [@problem_id:3055547]。

### [左不变向量场](@entry_id:637116)：通往[李代数](@entry_id:137954)的桥梁

[流形上的向量](@entry_id:160178)场是在每一点附加上一个[切向量](@entry_id:265494)的光滑指派。在李群上，我们可以利用左移的对称性来定义一类特殊的向量场。一个光滑向量场 $X$ (即一个映射 $g \mapsto X_g \in T_g G$) 被称为**左不变的 (left-invariant)**，如果它在所有左移的推前作用下保持不变。这意味着对任意 $g \in G$，我们有 $(L_g)_*X = X$。这个等式在逐点的意义上展开，即对任意 $g, h \in G$，下式成立 [@problem_id:3031944] [@problem_id:3055544]：
$$
d(L_g)_h(X_h) = X_{gh}
$$
这个定义揭示了一个深刻的性质：一个[左不变向量场](@entry_id:637116)由它在群中**任何一点**的值完全决定。特别地，它由在单位元 $e$ 处的值 $X_e \in T_eG$ 唯一确定。如果我们知道 $X_e$，那么在任意点 $g \in G$ 的向量值可以通过上式（令 $h=e$）得到：
$$
X_g = d(L_g)_e(X_e)
$$
反之，对于李代数 $\mathfrak{g} = T_eG$ 中的任意一个向量 $v \in \mathfrak{g}$，我们都可以通过上述公式定义一个遍布整个[李群](@entry_id:137659)的向量场 $\tilde{v}$：
$$
\tilde{v}(g) := d(L_g)_e(v)
$$
可以验证，这样构造出的向量场 $\tilde{v}$ 确实是左不变的。因此，在李代数 $\mathfrak{g}$ 与所有[左不变向量场](@entry_id:637116)的空间 $\mathfrak{X}_L(G)$ 之间存在一个一一对应关系。这个对应关系是一个[线性同构](@entry_id:270529)：将[左不变向量场](@entry_id:637116) $X$ 映射到其在单位元的值 $X_e$ 的映射 $\varphi: \mathfrak{X}_L(G) \to \mathfrak{g}$ 是一个[线性同构](@entry_id:270529) [@problem_id:3031944]。

这个抽象的构造在[矩阵李群](@entry_id:145968)中变得非常直观。例如，考虑 $G = \mathrm{GL}(n, \mathbb{R})$，其[李代数](@entry_id:137954) $\mathfrak{g} = T_I G$ 可以等同于所有 $n \times n$ 实矩阵的空间 $M(n, \mathbb{R})$。对于一个切向量 $V \in T_H G$（其中 $H \in G$ 是一个可逆矩阵），左移 $L_G(H) = GH$ 的[微分](@entry_id:158718)作用简化为矩阵乘法：$d(L_G)_H(V) = GV$。因此，由 $A = X_e \in \mathfrak{g}$ 决定的[左不变向量场](@entry_id:637116) $X$ 在任意矩阵 $H \in G$ 处的值就是 $X_H = d(L_H)_e(A) = HA$。

例如，在 $G = \mathrm{GL}(2, \mathbb{R})$上，设有两个[左不变向量场](@entry_id:637116) $X$ 和 $Y$，它们在[单位矩阵](@entry_id:156724) $I$ 处的值分别为 $X_e = \begin{pmatrix} 1  2 \\ 0  3 \end{pmatrix}$ 和 $Y_e = \begin{pmatrix} -1  0 \\ 4  2 \end{pmatrix}$。它们的线性组合 $Z = 3X - 2Y$ 也是一个[左不变向量场](@entry_id:637116)，其在单位元的值为 $Z_e = 3X_e - 2Y_e$。要计算 $Z$ 在任意一点 $g \in G$ 的值 $Z_g$，我们只需用 $g$ 左乘 $Z_e$ 即可。例如，在点 $g = \begin{pmatrix} 5  1 \\ 1  2 \end{pmatrix}$，我们有：
$$
Z_g = g Z_e = g(3X_e - 2Y_e) = \begin{pmatrix} 5  1 \\ 1  2 \end{pmatrix} \left( 3\begin{pmatrix} 1  2 \\ 0  3 \end{pmatrix} - 2\begin{pmatrix} -1  0 \\ 4  2 \end{pmatrix} \right) = \begin{pmatrix} 17  35 \\ -11  16 \end{pmatrix}
$$
这个例子清晰地展示了[左不变向量场](@entry_id:637116)空间 $\mathfrak{X}_L(G)$ 作为一个[向量空间](@entry_id:151108)的结构，以及它与[李代数](@entry_id:137954) $\mathfrak{g}$ 之间的密切联系 [@problem_id:1649964]。

### 左不变[向量场的李代数](@entry_id:194363)

向量场的一个核心运算是**[李括号](@entry_id:636461) (Lie bracket)** $[X,Y]$，它描述了沿着一个向量场的流如何改变另一个向量场。一个重要的事实是，两个左不变[向量场的李括号](@entry_id:193400)仍然是左不变的。这源于李括号在[微分同胚](@entry_id:147249)下的自然性。对于任何左移 $L_g$，我们有：
$$
(L_g)_*[X, Y] = [(L_g)_*X, (L_g)_*Y]
$$
因为 $X$ 和 $Y$ 是左不变的，所以 $(L_g)_*X = X$ 且 $(L_g)_*Y = Y$。代入上式得到：
$$
(L_g)_*[X, Y] = [X, Y]
$$
这恰恰证明了 $[X,Y]$ 也是左不变的。因此，[左不变向量场](@entry_id:637116)的空间 $\mathfrak{X}_L(G)$ 在[李括号](@entry_id:636461)运算下是封闭的，构成了一个李代数 [@problem_id:3031944]。

这一发现至关重要，因为它允许我们将 $\mathfrak{X}_L(G)$ 的李[代数结构](@entry_id:137052)通过之前建立的[线性同构](@entry_id:270529) $\varphi: X \mapsto X_e$ “传送”回 $T_eG = \mathfrak{g}$。我们可以**定义** $\mathfrak{g}$上的李括号如下：对于任意 $u, v \in \mathfrak{g}$，令 $\tilde{u}$ 和 $\tilde{v}$ 为它们各自唯一的左不变扩展，则定义：
$$
[u, v]_\mathfrak{g} := [\tilde{u}, \tilde{v}]_e
$$
这个定义将[李群](@entry_id:137659)的切空间 $\mathfrak{g}$ 赋予了一个李[代数结构](@entry_id:137052)，而这个结构完全由[流形](@entry_id:153038)上[向量场的李括号](@entry_id:193400)所决定。通过这个定义，映射 $\varphi: \mathfrak{X}_L(G) \to \mathfrak{g}$ 成为了一个**李代数同构**。正是这种同构关系，使得我们可以通过研究有限维李代数 $\mathfrak{g}$ 的代数性质来理解整个[李群](@entry_id:137659) $G$ 的几何和拓扑性质 [@problem_id:3031944]。

### 右[不变性](@entry_id:140168)与双不变性

与左移相对应，我们也可以定义**右移 (right translation)** $R_g: G \to G$ 为 $R_g(h) = hg$。类似地，一个向量场 $Y$ 被称为**右不变的 (right-invariant)** 如果对所有 $g,h \in G$ 都有 $d(R_g)_h(Y_h) = Y_{hg}$。

在[非交换群](@entry_id:141904)中，左不变和右不变通常是截然不同的性质。对于[矩阵李群](@entry_id:145968)，由 $A \in \mathfrak{g}$ 生成的向量场 $X_h = hA$ 是左不变的，而 $Y_h = Ah$ 是右不变的。一个向量场 $X_h = hA$ 是右不变的当且仅当对所有 $g, h \in G$ 都有 $(hA)g = (hg)A$，这等价于 $Ag=gA$ 对所有 $g \in G$ 成立。这通常是不满足的，除非 $A$ 属于李[群的中心](@entry_id:141952)。例如，在 $\mathrm{GL}(2, \mathbb{R})$ 中，选择 $A = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}$，则向量场 $X_h = hA$ 是左不变的，但不是右不变的 [@problem_id:3055544]。

一个同时是左不变和右不变的向量场被称为**双不变的 (bi-invariant)**。一个[左不变向量场](@entry_id:637116) $X$（对应于 $v=X_e \in \mathfrak{g}$）是双不变的，当且仅当它在所有右移下也不变。这等价于其在单位元的值 $v$ 在群的伴随作用下不变，即对所有 $g \in G$ 都有 $\mathrm{Ad}(g)(v) = v$。在[李代数](@entry_id:137954)的层面上，这等价于 $v$ 位于 $\mathfrak{g}$ 的中心，即对所有 $w \in \mathfrak{g}$ 都有 $[v, w] = 0$ [@problem_id:3055544]。

还有一个有趣的联系是，由右不变向量场诱导的李[代数结构](@entry_id:137052)与由[左不变向量场](@entry_id:637116)诱导的结构仅相差一个负号。也就是说，如果 $[u,v]_L$ 是通常定义的（由左不变场诱导的）李括号，$[u,v]_R$ 是由右不变场诱导的[李括号](@entry_id:636461)，那么 $[u,v]_R = -[u,v]_L$ [@problem_id:3031944]。

### [左不变微分形式](@entry_id:203779)与 Maurer-Cartan 形式

向量场的对偶概念是[微分1-形式](@entry_id:265626)。一个1-形式 $\alpha$ 被称为**左不变的 (left-invariant)**，如果它在所有左移的**[拉回](@entry_id:160816) (pullback)** 作用下保持不变，即对任意 $g \in G$，有 $(L_g)^*\alpha = \alpha$。与向量场类似，一个左不变1-形式也由其在单位元处的值 $\alpha_e \in \mathfrak{g}^*$ 唯一确定。

在所有[左不变形式](@entry_id:203779)中，有一个扮演着核心角色的对象，它是一个取值于李代数 $\mathfrak{g}$ 本身的[1-形式](@entry_id:270392)，称为**Maurer-Cartan 形式 (Maurer-Cartan form)**，记为 $\omega$。它在每一点 $g \in G$ 的定义为：
$$
\omega_g := d(L_{g^{-1}})_g : T_g G \to T_e G = \mathfrak{g}
$$
这个定义看起来有些抽象，但其几何意义非常清晰。$\omega_g$ 是一个线性映射，它将点 $g$ 处的任意一个[切向量](@entry_id:265494) $v \in T_gG$，“搬运”回单位元 $e$ 处的[切空间](@entry_id:199137) $\mathfrak{g}$。如果 $v$ 是曲线 $c(t)$ 在 $c(0)=g$ 时的速度向量 $c'(0)$，那么 $\omega_g(v)$ 就是被左移 $L_{g^{-1}}$ 作用后的新曲线 $t \mapsto g^{-1}c(t)$ 在 $t=0$ 时的速度向量 [@problem_id:3055525]。由于 $d(L_{g^{-1}})_g$ 是一个[线性同构](@entry_id:270529)，$\omega_g$ 为我们提供了一个典范的、不依赖于任何[坐标系](@entry_id:156346)或度量的[线性同构](@entry_id:270529) $T_gG \cong \mathfrak{g}$。

Maurer-Cartan 形式自身就是左不变的，即 $(L_h)^*\omega = \omega$ 对所有 $h \in G$ 成立。此外，它与[左不变向量场](@entry_id:637116)之间存在一种优美的对偶关系。如果 $\tilde{X}$ 是由 $X \in \mathfrak{g}$ 生成的[左不变向量场](@entry_id:637116)，那么将 $\omega$ 作用于 $\tilde{X}$ 上，我们得到一个常值函数，其值就是 $X$：
$$
\omega_g(\tilde{X}_g) = d(L_{g^{-1}})_g (d(L_g)_e X) = d(L_{g^{-1}} \circ L_g)_e (X) = d(\text{id})_e(X) = X
$$
这表明 $\omega$ 就像一个“万能钥匙”，可以将任何在点 $g$ 的[左不变向量场](@entry_id:637116)“解码”回其在李代数中的原始元素 [@problem_id:3055525]。

### Maurer-Cartan 方程

Maurer-Cartan 形式最深刻的性质体现在它所满足的[结构方程](@entry_id:274644)中。这个方程被称为 **Maurer-Cartan 方程**：
$$
d\omega + \frac{1}{2}[\omega, \omega] = 0
$$
这里的 $d$ 是外微分算子，而 $[\omega, \omega]$ 是一个结合了[楔积](@entry_id:147029)和[李代数](@entry_id:137954)括号的运算，具体定义为 $[\omega, \omega](U, V) = 2[\omega(U), \omega(V)]_\mathfrak{g}$，其中 $U, V$ 是任意两个向量场。这个方程封装了李群的全部局部几何信息，将李代数的[代数结构](@entry_id:137052)（[李括号](@entry_id:636461)）与[流形](@entry_id:153038)的[微分](@entry_id:158718)结构（[外微分](@entry_id:161900)）联系在一起 [@problem_id:3055525]。

此方程也可以用[李代数](@entry_id:137954)的基和[结构常数](@entry_id:157960)来表示。设 $\{E_i\}$ 是 $\mathfrak{g}$ 的一组基，$[E_i, E_j] = \sum_k c^k_{ij} E_k$，其中 $c^k_{ij}$ 是**[结构常数](@entry_id:157960)**。设 $\{\omega^i\}$ 是对偶的左不变[1-形式](@entry_id:270392)构成的基底，即 $\omega^i(\tilde{E}_j) = \delta^i_j$。可以证明，左不变[向量场的[李括](@entry_id:193400)号](@entry_id:636461)与李代数的[李括号](@entry_id:636461)完全对应：$[\tilde{E}_i, \tilde{E}_j] = \sum_k c^k_{ij} \tilde{E}_k$。利用[外微分](@entry_id:161900)的公式 $d\alpha(X,Y) = X(\alpha(Y)) - Y(\alpha(X)) - \alpha([X,Y])$，我们可以计算 $d\omega^k(\tilde{E}_i, \tilde{E}_j)$。由于 $\omega^k(\tilde{E}_j) = \delta^k_j$ 是常数，前两项为零，于是：
$$
d\omega^k(\tilde{E}_i, \tilde{E}_j) = -\omega^k([\tilde{E}_i, \tilde{E}_j]) = -\omega^k\left(\sum_l c^l_{ij} \tilde{E}_l\right) = -\sum_l c^l_{ij} \delta^k_l = -c^k_{ij}
$$
这给出了[Maurer-Cartan方程](@entry_id:637430)的坐标形式 [@problem_id:3055520]。

对于[矩阵李群](@entry_id:145968)，Maurer-Cartan 形式和方程有更为具体的表达。如果我们将[李群](@entry_id:137659)元素视为[矩阵函数](@entry_id:180392) $g$，那么 $dg$ 是一个矩阵，其元素是[1-形式](@entry_id:270392)。Maurer-Cartan 形式可以简洁地写成矩阵乘积 $\omega = g^{-1}dg$。[Maurer-Cartan方程](@entry_id:637430) $d\omega + \omega \wedge \omega = 0$ 就可以通过[矩阵微积分](@entry_id:181100)直接验证。关键一步是利用 $g g^{-1} = I$ 对其求外微分，得到 $d(g^{-1}) = -g^{-1}(dg)g^{-1}$。然后利用外微分的[莱布尼茨法则](@entry_id:157949) $d(AB) = dA \wedge B + (-1)^p A \wedge dB$（其中 $A$ 是 $p$-形式矩阵），我们有：
$$
d\omega = d(g^{-1}dg) = d(g^{-1}) \wedge dg + g^{-1} \wedge d(dg) = (-g^{-1}(dg)g^{-1}) \wedge dg
$$
由于 $d(dg)=0$。另一方面，$\omega \wedge \omega = (g^{-1}dg) \wedge (g^{-1}dg)$。经过计算可以证明，这两项正好相加为零，从而验证了 $d\omega + \omega \wedge \omega = 0$ [@problem_id:3055551]。

### 几何应用：不变度量与体积形式

左[不变性](@entry_id:140168)的概念在[黎曼几何](@entry_id:160508)中极为有用，它允许我们在整个李群上构造具有高度对称性的几何结构。

#### [左不变度量](@entry_id:637439)

我们可以在李代数 $\mathfrak{g} = T_eG$ 上任意指定一个[内积](@entry_id:158127)（欧氏度量）$\langle \cdot, \cdot \rangle_e$。然后，我们可以利用左移将这个[内积](@entry_id:158127)“传播”到整个群上，定义一个**左不变[黎曼度量](@entry_id:754359)** $\langle \cdot, \cdot \rangle$。其在任意一点 $g$ 的定义为：
$$
\langle u, v \rangle_g := \langle d(L_{g^{-1}})_g(u), d(L_{g^{-1}})_g(v) \rangle_e
$$
其中 $u, v \in T_gG$。根据这个定义，所有的左移 $L_h$ 都自动成为度量下的[等距同构](@entry_id:273188)。

这个构造有一个美妙的推论：任何 $\mathfrak{g}$ 中的一个[标准正交基](@entry_id:147779) $\{e_1, \dots, e_n\}$，通过左不变扩展 $E_i(g) = d(L_g)_e(e_i)$，会生成一个全局的**[标准正交标架](@entry_id:189702)场** $\{E_1, \dots, E_n\}$。也就是说，在每一点 $g \in G$，向量 $\{E_1(g), \dots, E_n(g)\}$ 都构成 $T_gG$ 的一个[标准正交基](@entry_id:147779)。这极大地简化了在李群上进行几何计算的复杂性 [@problem_id:3055533]。

#### 双不变[体积形式](@entry_id:203000)与[幺模群](@entry_id:202571)

与度量相关的是[体积形式](@entry_id:203000)。一个 $n$ 维李群总存在一个无处为零的左不变 $n$-形式 $\omega$，它被称为**左不变[体积形式](@entry_id:203000)**。一个自然的问题是：这个左不变的体积形式何时也是右不变的，从而成为一个**双不变体积形式**？这样的形式在积分理论中至关重要，因为它对应于群上的一个双[不变测度](@entry_id:202044)（[哈尔测度](@entry_id:142417)）。

答案与[李代数](@entry_id:137954)的伴随表示有关。对于任意 $X \in \mathfrak{g}$，可以计算左不变[体积形式](@entry_id:203000) $\omega$ 沿着[左不变向量场](@entry_id:637116) $X^L$ 的李导数，结果为：
$$
L_{X^L} \omega = - \mathrm{tr}(\mathrm{ad}_X) \omega
$$
其中 $\mathrm{ad}_X: \mathfrak{g} \to \mathfrak{g}$ 是伴随映射 $\mathrm{ad}_X(Y) = [X,Y]$，$\mathrm{tr}(\mathrm{ad}_X)$ 是这个线性映射的迹。

另一方面，$\omega$ 的右不变性等价于 $L_{X^L} \omega = 0$ 对所有 $X \in \mathfrak{g}$ 成立。因此，一个左不变[体积形式](@entry_id:203000)是双不变的，当且仅当对所有 $X \in \mathfrak{g}$，都有 $\mathrm{tr}(\mathrm{ad}_X)=0$。满足这个条件的[李群](@entry_id:137659)被称为**[幺模群](@entry_id:202571) (unimodular group)** [@problem_id:3055518]。

如果一个[李群](@entry_id:137659)不是幺模的，即存在某个 $X$ 使得 $\mathrm{tr}(\mathrm{ad}_X) \neq 0$，那么任何左不变[体积形式](@entry_id:203000)都不可能是右不变的。由于任意两个左不变体积形式只相差一个常数倍，这意味着该群上不存在任何双不变[体积形式](@entry_id:203000) [@problem_id:3055518]。许多重要的[李群](@entry_id:137659)都是幺模的，例如[交换群](@entry_id:145145)、[紧李群](@entry_id:146703)（如 $SO(n)$）和半单[李群](@entry_id:137659)（如 $SL(n, \mathbb{R})$），但并非所有李群都如此。这为[李群](@entry_id:137659)的分类提供了一个重要的代数判据。