## 引言
在探索[拓扑空间](@entry_id:155056)的奥秘时，我们不仅关注其宏大的全局构造，也同样着迷于其精细的局部特征。一个空间在某一点附近究竟是平滑如[欧几里得空间](@entry_id:138052)，还是隐藏着复杂的“[奇点](@entry_id:137764)”？要回答这个问题，我们需要一个能够超越直观感觉的严谨数学工具。[局部同调](@entry_id:160439)群应运而生，它为我们提供了一副“代数显微镜”，能够精确捕捉并量化一个点周围的拓扑结构，从而解决了如何从代数层面分析空间局部行为的难题。

本文将系统地介绍[局部同调](@entry_id:160439)群这一概念。在“原理与机制”一章中，我们将从其[相对同调](@entry_id:159348)的定义出发，学习[切除定理](@entry_id:159397)如何确保其“局部性”，并掌握如何利用长正合序列计算[流形](@entry_id:153038)[内点](@entry_id:270386)、[边界点](@entry_id:176493)以及基本[奇点](@entry_id:137764)的[局部同调](@entry_id:160439)。随后，在“应用与跨学科联系”一章中，我们将展示该工具的强大威力，看它如何被应用于探测和分类[代数几何](@entry_id:156300)与[奇点理论](@entry_id:160612)中的复杂[奇点](@entry_id:137764)，并揭示其与空间[可定向性](@entry_id:149777)等全局性质的深刻联系。最后，通过“动手实践”部分的精选习题，您将有机会亲手计算不同类型[奇点](@entry_id:137764)的[局部同调](@entry_id:160439)，将理论知识转化为解决问题的实际能力。

## 原理与机制

在拓扑学中，我们常常不仅关心一个空间的全局属性，也对其局部结构抱有浓厚的兴趣。一个空间在某一点附近“看起来像什么”？它是平滑的，还是存在某种[奇点](@entry_id:137764)？[局部同调](@entry_id:160439)群 (local homology groups) 为我们提供了一个强大的代数工具，以严谨的方式探究和回答这些问题。它通过分析一个点被“移除”时空间的[拓扑变化](@entry_id:136654)，来捕捉该点周围的几何与拓扑信息。

### [局部同调](@entry_id:160439)群的定义与基本性质

为了研究[拓扑空间](@entry_id:155056) $X$ 在某一点 $x$ 处的局部性质，一个自然的想法是考察包含 $x$ 的任意小邻域。然而，这样做缺乏一个规范的代数[不变量](@entry_id:148850)。[局部同调](@entry_id:160439)群通过[相对同调](@entry_id:159348)巧妙地解决了这个问题。

**[局部同调](@entry_id:160439)群**被定义为[相对同调群](@entry_id:159711) $H_n(X, X \setminus \{x\})$。这个定义乍看之下有些抽象，但其思想非常直观：我们考虑的是 $X$ 中的 $n$ 维链，但我们“忽略”那些完全位于 $X \setminus \{x\}$ 中的链。一个相对 $n$-圈 (relative $n$-cycle) 是一个 $n$ 维链 $\sigma$，其边界 $\partial \sigma$ 不在 $x$ 处，而是位于[子空间](@entry_id:150286) $X \setminus \{x\}$ 中。因此，这个同调群关注的正是那些“围绕”或“包含”点 $x$ 的链。

理解[局部同调](@entry_id:160439)群的关键工具是与空间对 $(X, X \setminus \{x\})$ 相关联的同调长正合序列。这个序列将[子空间](@entry_id:150286) $X \setminus \{x\}$ 的同调群、整体空间 $X$ 的同调群，以及我们所关注的[局部同调](@entry_id:160439)群联系在一起。

记 $i: X \setminus \{x\} \hookrightarrow X$ 为包含映射，$j: (X, \emptyset) \hookrightarrow (X, X \setminus \{x\})$ 为空间对的包含映射。它们在同调上诱导的同态分别为 $i_*$ 和 $j_*$。[连接同态](@entry_id:160713) $\partial$ 则将维度降低1。该长正合序列的一个片段具有如下形式 [@problem_id:1661094]：
$$
\dots \to H_n(X \setminus \{x\}) \xrightarrow{i_*} H_n(X) \xrightarrow{j_*} H_n(X, X \setminus \{x\}) \xrightarrow{\partial} H_{n-1}(X \setminus \{x\}) \to \dots
$$
这个序列是所有[局部同调](@entry_id:160439)计算的理论基石。它表明，[局部同调](@entry_id:160439)群 $H_n(X, X \setminus \{x\})$ 在某种程度上衡量了从 $H_n(X \setminus \{x\})$ 到 $H_n(X)$ 的映射 $i_*$ 与从 $H_{n-1}(X \setminus \{x\})$ 到 $H_{n-1}(X)$ 的映射之间的“差异”。

### [切除定理](@entry_id:159397)：聚焦于局部

[局部同调](@entry_id:160439)群的定义 $H_n(X, X \setminus \{x\})$ 似乎依赖于整个空间 $X$。然而，我们希望它是一个真正“局部”的性质，即只依赖于 $x$ 点附近的一个小邻域。这正是**[切除定理](@entry_id:159397) (Excision Theorem)** 发挥作用的地方。

[切除定理](@entry_id:159397)保证，如果我们取 $x$ 的任意一个[开邻域](@entry_id:268496) $U$，那么包含映射 $(U, U \setminus \{x\}) \hookrightarrow (X, X \setminus \{x\})$ 会诱导一个同构：
$$
H_n(U, U \setminus \{x\}) \cong H_n(X, X \setminus \{x\})
$$
这个同构的意义极为深远。它意味着，要计算一个点 $x$ 的[局部同调](@entry_id:160439)群，我们无需考虑整个复杂的空间 $X$，只需切除 $X \setminus U$ 这一部分，聚焦于 $x$ 的任何一个足够小的邻域 $U$ 即可。这正式确立了 $H_n(X, X \setminus \{x\})$ 作为“局部”[不变量](@entry_id:148850)的地位。

这一性质的一个优雅体现是在研究[覆盖映射](@entry_id:169347)时。若 $p: \tilde{X} \to X$ 是一个[覆盖映射](@entry_id:169347)，由于[覆盖映射](@entry_id:169347)是局部同胚，对于 $\tilde{X}$ 中的任意点 $\tilde{x}$ 及其像 $x = p(\tilde{x})$，存在 $\tilde{x}$ 的一个邻域 $V$ 和 $x$ 的一个邻域 $U$，使得 $p$ 限制在 $V$ 上是到 $U$ 的一个[同胚](@entry_id:146933)。结合[切除定理](@entry_id:159397)，这直接导出一个重要结论：由[覆盖映射](@entry_id:169347)诱导的同态 $p_*: H_n(\tilde{X}, \tilde{X} \setminus \{\tilde{x}\}) \to H_n(X, X \setminus \{x\})$ 对所有 $n \ge 0$ 都是一个同构 [@problem_id:1661091]。换言之，[局部同调](@entry_id:160439)在[覆盖映射](@entry_id:169347)下是不变的，这再次强调了它的纯粹局部性。

### [流形](@entry_id:153038)的同调特征

应用上述工具，我们首先考察一类最重要且行为良好的空间：[流形](@entry_id:153038)。

#### [流形](@entry_id:153038)[内点](@entry_id:270386)

考虑一个 $n$ 维[拓扑流形](@entry_id:271368) $M$ 和它的一个**[内点](@entry_id:270386)** $x$。根据[流形](@entry_id:153038)的定义，$x$ 存在一个[开邻域](@entry_id:268496) $U$ [同胚](@entry_id:146933)于[欧几里得空间](@entry_id:138052) $\mathbb{R}^n$。利用[切除定理](@entry_id:159397)，我们可以将计算简化到这个邻域中：
$$
H_k(M, M \setminus \{x\}) \cong H_k(U, U \setminus \{x\}) \cong H_k(\mathbb{R}^n, \mathbb{R}^n \setminus \{0\})
$$
这里我们不妨设[同胚](@entry_id:146933)将 $x$ 映为 $\mathbb{R}^n$ 的原点 $0$。为计算 $H_k(\mathbb{R}^n, \mathbb{R}^n \setminus \{0\})$，我们再次使用[切除定理](@entry_id:159397)，将问题简化到一个以原点为中心的[闭球](@entry_id:157850) $D^n$ 上，得到 $H_k(D^n, D^n \setminus \{0\})$。现在，我们考察空间对 $(D^n, D^n \setminus \{0\})$ 的[长正合序列](@entry_id:153438)：
$$
\dots \to H_k(D^n) \to H_k(D^n, D^n \setminus \{0\}) \xrightarrow{\partial} H_{k-1}(D^n \setminus \{0\}) \to H_{k-1}(D^n) \to \dots
$$
由于 $D^n$是可缩的，对所有 $j \ge 1$，其同调群 $H_j(D^n)$ 均为平凡群 $\{0\}$。因此，对于 $k \ge 2$，上述序列简化为 $0 \to H_k(D^n, D^n \setminus \{0\}) \to H_{k-1}(D^n \setminus \{0\}) \to 0$，这意味着 $H_k(D^n, D^n \setminus \{0\}) \cong H_{k-1}(D^n \setminus \{0\})$。对于 $k=1$ 的情况，我们得到 $H_1(D^n, D^n \setminus \{0\}) \cong \tilde{H}_0(D^n \setminus \{0\})$，其中 $\tilde{H}$ 表示简约同调。

空间 $D^n \setminus \{0\}$ 可以[形变收缩](@entry_id:148036)到球面 $S^{n-1}$ 上。因此，$H_{k-1}(D^n \setminus \{0\}) \cong H_{k-1}(S^{n-1})$。综合以上同构，我们得到了一个核心结果 [@problem_id:1661100]：
$$
H_k(\mathbb{R}^n, \mathbb{R}^n \setminus \{0\}) \cong \tilde{H}_{k-1}(S^{n-1})
$$
球面 $S^{n-1}$ 的简约同调群我们是熟知的：当 $k-1 = n-1$ (即 $k=n$) 且 $n \ge 1$ 时，$\tilde{H}_{n-1}(S^{n-1}) \cong \mathbb{Z}$；在其他维度 $k-1 \ge 0$ 时，均为[平凡群](@entry_id:151996)。

于是我们得出结论：对于一个 $n$ 维[流形](@entry_id:153038) $M$ 的任意[内点](@entry_id:270386) $x$，其[局部同调](@entry_id:160439)群为 [@problem_id:1661090] [@problem_id:1661147]：
$$
H_k(M, M \setminus \{x\}) \cong \begin{cases} \mathbb{Z}  & \text{if } k=n \\ \{0\} & \text{if } k \ne n \end{cases}
$$
这个非平凡的群 $H_n(M, M \setminus \{x\}) \cong \mathbb{Z}$ 具有深刻的几何意义。它的一个**生成元**可以被形象地理解为一个奇异 $n$-单纯形 $\sigma: \Delta^n \to M$，其像的内部包含点 $x$，而其边界 $\partial\sigma$ 则完全落在 $M \setminus \{x\}$ 中 [@problem_id:1664675]。这个生成元本质上代表了 $x$ 点附近的一个“体积元”。为这个同构于 $\mathbb{Z}$ 的群选择一个生成元（即选择 $+1$ 或 $-1$），就等价于在点 $x$ 处为[流形](@entry_id:153038)赋予了一个**[局部定向](@entry_id:264384) (local orientation)**。

#### [流形](@entry_id:153038)[边界点](@entry_id:176493)

现在，如果点 $x$ 位于一个[带边流形](@entry_id:159788) $M$ 的**边界** $\partial M$ 上，情况又会如何？此时，$x$ 的一个邻域同胚于一个[半空间](@entry_id:634770) $\mathbb{R}^n_+ = \{y \in \mathbb{R}^n \mid y_n \ge 0\}$，且 $x$ 对应于边界[超平面](@entry_id:268044) $y_n=0$ 上的点（例如原点）。通过与[内点](@entry_id:270386)情况完全相同的逻辑（切除和[同伦](@entry_id:139266)），计算归结为 $H_n(\mathbb{R}^n_+, \mathbb{R}^n_+ \setminus \{0\})$ [@problem_id:1661339]。

然而，挖去原点的半空间 $\mathbb{R}^n_+ \setminus \{0\}$ 是可缩的（它可以[形变收缩](@entry_id:148036)到其边界上的一个点）。因此，它的所有简约同调群均为[平凡群](@entry_id:151996)。根据 $H_n(\mathbb{R}^n_+, \mathbb{R}^n_+ \setminus \{0\}) \cong \tilde{H}_{n-1}(\mathbb{R}^n_+ \setminus \{0\})$ 的关系，我们立即得到：
$$
H_n(M, M \setminus \{x\}) \cong \{0\} \quad \text{for } x \in \partial M
$$
这个结果与[内点](@entry_id:270386)的情况形成了鲜明对比。因此，最高维度的[局部同调](@entry_id:160439)群为我们提供了一个纯粹的代数判据，用以区分[流形](@entry_id:153038)的[内点](@entry_id:270386)（同调群为 $\mathbb{Z}$）和[边界点](@entry_id:176493)（同调群为 $\{0\}$）。

### 超越[流形](@entry_id:153038)：分析[奇点](@entry_id:137764)

[局部同调](@entry_id:160439)群的真正威力在于分析那些不是[流形](@entry_id:153038)点的**[奇点](@entry_id:137764) (singularities)**。在这些点上，[局部同调](@entry_id:160439)群的行为将偏离[流形](@entry_id:153038)的模式，并揭示出[奇点](@entry_id:137764)独特的几何结构。

#### [局部连通性](@entry_id:152613)与低维同调

[局部同调](@entry_id:160439)的低维群，特别是 $H_1$ 和 $H_0$，可以探测一个点附近的连通性。考虑长正合序列的末尾部分：
$$
H_1(X, X \setminus \{x\}) \xrightarrow{\partial} H_0(X \setminus \{x\}) \xrightarrow{i_*} H_0(X) \to H_0(X, X \setminus \{x\}) \to 0
$$
如果 $x$ 的一个邻域是[路径连通](@entry_id:148704)的，那么通过[切除定理](@entry_id:159397)，我们可以假设 $H_0(X) \cong \mathbb{Z}$ 且 $H_0(X, X \setminus \{x\}) = 0$。序列变为一个短[正合序列](@entry_id:151503)，并导出同构：
$$
H_1(X, X \setminus \{x\}) \cong \ker(i_*: H_0(X \setminus \{x\}) \to H_0(X)) \cong \tilde{H}_0(X \setminus \{x\})
$$
$H_0(X \setminus \{x\})$ 是由 $X \setminus \{x\}$ 的[路径分支](@entry_id:155468)生成的自由阿贝尔群。$\tilde{H}_0(X \setminus \{x\})$ 的秩等于[路径分支](@entry_id:155468)数减一。因此，$H_1(X, X \setminus \{x\})$ 的秩精确地告诉我们，在挖掉点 $x$ 之后，空间“分裂”成了多少个新的连通部分。

一个典型的例子是考虑 $\mathbb{R}^2$ 中过原点的三条不同直线组成的联集 $X$。原点 $x_0=(0,0)$ 是一个[奇点](@entry_id:137764)。取 $x_0$ 的一个小的开圆盘邻域 $U$ 与 $X$ 相交的部分。$U$ 本身是[路径连通](@entry_id:148704)的，但 $U \setminus \{x_0\}$ 则由6个分离的线段组成。因此，$H_0(U \setminus \{x_0\}) \cong \mathbb{Z}^6$。根据上述同构，$H_1(X, X \setminus \{x_0\}) \cong \tilde{H}_0(U \setminus \{x_0\}) \cong \mathbb{Z}^5$ [@problem_id:1661140]。这个秩为5的群，与[流形](@entry_id:153038)点处秩为0的 $H_1$ 形成鲜明对比，清晰地指出了该点的“分支”奇异性。

#### [锥奇点](@entry_id:264048)

一类重要的[奇点](@entry_id:137764)是**锥点 (cone point)**。给定一个拓扑空间 $Y$，其上的锥 $CY$ 是将 $Y \times [0,1]$ 中的顶端 $Y \times \{1\}$ 捏成一个点 $v$ 所得到的空间。这个顶点 $v$ 就是一个典型的[奇点](@entry_id:137764)。

锥 $CY$ 本身是可缩的，因此其所有高阶同调群为零。$CY \setminus \{v\}$ 则同伦等价于底空间 $Y$。利用与之前相同的[长正合序列](@entry_id:153438)论证，可以得出一个非常优美的通式 [@problem_id:1661106]：
$$
H_k(CY, CY \setminus \{v\}) \cong \tilde{H}_{k-1}(Y) \quad \text{for all } k \ge 1
$$
并且 $H_0(CY, CY \setminus \{v\}) = 0$。这个公式揭示了一个深刻的联系：锥点处的[局部同调](@entry_id:160439)完全由底空间 $Y$ 的同调性质所决定。[奇点](@entry_id:137764) $v$ 的局部结构“编码”了整个空间 $Y$ 的拓扑信息。

例如，若底空间 $Y$ 是两个圆 $S^1 \sqcup S^1$ 的不交并，那么在锥点 $v$ 处的[局部同调](@entry_id:160439)群为：
- $H_1(CY, CY \setminus \{v\}) \cong \tilde{H}_0(S^1 \sqcup S^1) \cong \mathbb{Z}$
- $H_2(CY, CY \setminus \{v\}) \cong H_1(S^1 \sqcup S^1) \cong \mathbb{Z} \oplus \mathbb{Z}$
- 当 $k \ge 3$ 时，$H_k(CY, CY \setminus \{v\}) \cong H_{k-1}(S^1 \sqcup S^1) = 0$
这一组同调群 $(0, \mathbb{Z}, \mathbb{Z}\oplus\mathbb{Z}, 0, \dots)$ 显然不是任何维度[流形](@entry_id:153038)点的标志，它准确地反映了锥点下的几何构造。

#### [商空间](@entry_id:274314)[奇点](@entry_id:137764)

[局部同调](@entry_id:160439)在分析由群作用产生的[商空间](@entry_id:274314)[奇点](@entry_id:137764)（也称为**[轨道](@entry_id:137151)[流形奇点](@entry_id:161285)，orbifold singularities**）时也同样有效。考虑一个有限群 $G$ 作用在一个空间 $X$ 上。如果一个点 $x \in X$ 是作用的一个[不动点](@entry_id:156394)，那么它在[商空间](@entry_id:274314) $X/G$ 中的像通常是一个[奇点](@entry_id:137764)。

一个经典的例子是群 $G = \mathbb{Z}_2 = \{\pm 1\}$ 通过[数乘](@entry_id:155971)作用于 $\mathbb{R}^k$ ($k \ge 2$)。原点 $x_0=0$ 是唯一的[不动点](@entry_id:156394)。[商空间](@entry_id:274314) $X/G = \mathbb{R}^k/\mathbb{Z}_2$ 在原点的像 $\bar{x}_0$ 处有一个[奇点](@entry_id:137764)。不难发现，这个[商空间](@entry_id:274314)[同胚](@entry_id:146933)于[实射影空间](@entry_id:149094) $\mathbb{R}P^{k-1}$ 上的锥 $C(\mathbb{R}P^{k-1})$ [@problem_id:1661112]。

利用锥的公式，我们可以立即计算出这个[奇点](@entry_id:137764)的[局部同调](@entry_id:160439)：
$$
H_k(X/G, X/G \setminus \{\bar{x}_0\}) \cong \tilde{H}_{k-1}(\mathbb{R}P^{k-1})
$$
[实射影空间](@entry_id:149094)的整系数同调是与维度奇偶性密切相关的。例如，$\tilde{H}_{k-1}(\mathbb{R}P^{k-1}; \mathbb{Z})$ 在 $k-1$ 为奇数（即 $k$ 为偶数）时同构于 $\mathbb{Z}$，而在 $k-1$ 为偶数时为[平凡群](@entry_id:151996)或 $\mathbb{Z}_2$。因此，这个[奇点](@entry_id:137764)的 $k$ 维[局部同调](@entry_id:160439)群的秩（自由部分的阶）在 $k$ 为偶数时为1，在 $k$ 为奇数时为0。这揭示了这类商空间[奇点](@entry_id:137764)一种依赖于维度的微妙结构，而这种结构正是通过[局部同调](@entry_id:160439)群被精确地捕捉到的。

综上所述，[局部同调](@entry_id:160439)群从一个简单的[相对同调](@entry_id:159348)定义出发，借助[切除定理](@entry_id:159397)和长正合序列，发展成为一个能够区分[流形](@entry_id:153038)[内点](@entry_id:270386)、边界点，并能精细刻画各类[奇点](@entry_id:137764)几何结构的强大代数[不变量](@entry_id:148850)。