## 应用与跨学科联系

在前面的章节中，我们已经建立了[纤维化的长正合序列](@entry_id:161359)这一核心理论工具。现在，我们将注意力从抽象的理论框架转向其在各种数学和物理问题中的具体应用。本章旨在展示纤维化长正合序列不仅仅是一个理论构造，更是一个强大的计算和概念工具，它能够揭示看似无关的拓扑空间之间的深刻联系，并为计算重要的[拓扑不变量](@entry_id:138526)（如[同伦群](@entry_id:159885)）提供一种系统性的方法。我们将通过一系列精心挑选的例子，探索该序列在几何学、李群理论、[同伦论](@entry_id:150876)乃至理论物理等领域的广泛应用。

### 基本计算与结构推断

纤维化长正合序列最直接的应用之一是计算拓扑空间的[同伦群](@entry_id:159885)。通过将一个复杂的[空间分解](@entry_id:755142)为一个更简单的基空间和纤维，我们可以利用已知空间的[同伦群](@entry_id:159885)来推断未知空间的[同伦群](@entry_id:159885)。

#### 积空间的[同伦群](@entry_id:159885)

一个基础且重要的例子是积空间。考虑两个拓扑空间 $S^n$ 和 $S^m$ 的[笛卡尔积](@entry_id:154642) $S^n \times S^m$。我们可以构造一个投影纤维化 $p: S^n \times S^m \to S^n$，其定义为 $p(x, y) = x$。这个[纤维化](@entry_id:203334)的纤维恰好是 $S^m$。相应的[长正合序列](@entry_id:153438)片段为：
$$ \dots \to \pi_k(S^m) \xrightarrow{i_*} \pi_k(S^n \times S^m) \xrightarrow{p_*} \pi_k(S^n) \xrightarrow{\partial_k} \pi_{k-1}(S^m) \to \dots $$
这个纤维化的特殊之处在于它存在一个“[截面](@entry_id:154995)” (section)——一个连续映射 $s: S^n \to S^n \times S^m$，例如可以定义为 $s(x) = (x, y_0)$，其中 $y_0$ 是 $S^m$ 中的一个基点。这个[截面](@entry_id:154995)满足 $p \circ s = \operatorname{id}_{S^n}$。在同伦群的层面上，这意味着诱导的同态 $p_* \circ s_* = \operatorname{id}_{\pi_k(S^n)}$。因此，$p_*$ 是一个满射。根据正合性，[连接同态](@entry_id:160713) $\partial_k$ 的核（kernel）是 $p_*$ 的像（image），即整个 $\pi_k(S^n)$。由于 $\partial_k$ 的定义域是 $\pi_k(S^n)$，这迫使 $\partial_k$ 成为零同态。

因为 $\partial_k = 0$，[长正合序列](@entry_id:153438)在 $\pi_k(S^n \times S^m)$ 处断裂成一个短[正合序列](@entry_id:151503)：
$$ 0 \to \pi_k(S^m) \xrightarrow{i_*} \pi_k(S^n \times S^m) \xrightarrow{p_*} \pi_k(S^n) \to 0 $$
这个短[正合序列](@entry_id:151503)是可裂的（split），因为 $s_*$ 提供了一个从 $\pi_k(S^n)$ 到 $\pi_k(S^n \times S^m)$ 的[右逆](@entry_id:161498)。对于阿贝尔群（当 $k \ge 2$ 时）和满足特定条件的[非阿贝尔群](@entry_id:141904)（当 $k=1$ 时），这意味着中间的群是两边群的[直和](@entry_id:156782)。因此，我们得到了一个众所周知的结果：
$$ \pi_k(S^n \times S^m) \cong \pi_k(S^n) \oplus \pi_k(S^m) \quad (\text{for } k \ge 1) $$
这个例子完美地展示了[长正合序列](@entry_id:153438)如何与空间的几何结构（存在[截面](@entry_id:154995)）相互作用，从而得到关于其代数[不变量](@entry_id:148850)的精确信息。

#### Hopf [纤维化](@entry_id:203334)与[球面的同伦群](@entry_id:160393)

计算球面的高维同伦群是代数拓扑学中的一个核心挑战。Hopf 纤维化及其相关的长正合序列为此提供了第一个深刻的见解。考虑著名的 Hopf [纤维化](@entry_id:203334) $S^1 \to S^3 \to S^2$。

首先，我们可以利用这个序列来计算 $\pi_2(S^3)$。相关的[长正合序列](@entry_id:153438)片段是：
$$ \dots \to \pi_2(S^1) \to \pi_2(S^3) \to \pi_2(S^2) \xrightarrow{\partial} \pi_1(S^1) \to \pi_1(S^3) \to \dots $$
我们已知 $\pi_2(S^1) = 0$ 和 $\pi_1(S^3) = 0$。代入这些信息，序列变为：
$$ 0 \to \pi_2(S^3) \to \pi_2(S^2) \xrightarrow{\partial} \pi_1(S^1) \to 0 $$
这表明[连接同态](@entry_id:160713) $\partial$ 是一个满射。更进一步，如果我们知道 $\pi_2(S^2) \cong \mathbb{Z}$ 和 $\pi_1(S^1) \cong \mathbb{Z}$，序列就成为 $0 \to \pi_2(S^3) \to \mathbb{Z} \xrightarrow{\partial} \mathbb{Z} \to 0$。一个从 $\mathbb{Z}$ 到 $\mathbb{Z}$ 的满同态必然是同构。因此，$\partial$ 的核是平凡的。根据正合性，从 $\pi_2(S^3)$ 到 $\pi_2(S^2)$ 的映射的像等于 $\partial$ 的核，即平凡群 $\{0\}$。由于该映射也是单射（因为它前面的群是 $0$），这迫使 $\pi_2(S^3)$ 本身必须是平凡群。

这个看似简单的结果 $\pi_2(S^3) = 0$ 在历史上是令人惊讶的，它表明并非所有高维球面都有非平凡的二维[同伦](@entry_id:139266)。

同样是这个序列，它也揭示了更高维度的信息。让我们考察 $k=3$ 时的序列：
$$ \dots \to \pi_3(S^1) \to \pi_3(S^3) \to \pi_3(S^2) \xrightarrow{\partial} \pi_2(S^1) \to \dots $$
我们知道球面的高维同伦群性质，$\pi_n(S^1) = 0$ 对于所有 $n \ge 2$。因此 $\pi_3(S^1) = 0$ 和 $\pi_2(S^1) = 0$。序列简化为：
$$ 0 \to \pi_3(S^3) \to \pi_3(S^2) \to 0 $$
这立即意味着从 $\pi_3(S^3)$ 到 $\pi_3(S^2)$ 的映射是一个同构。由于已知 $\pi_3(S^3) \cong \mathbb{Z}$，我们立即推断出 $\pi_3(S^2) \cong \mathbb{Z}$。这是一个非凡的结果：一个从三维空间到二维空间的映射（Hopf 映射）竟然可以携带关于三维[同伦](@entry_id:139266)的非平凡信息。这表明 $S^2$ 的三维[同伦群](@entry_id:159885)是非平凡的，这与直觉相悖，并开启了[稳定同伦理论](@entry_id:272389)的研究。

深入探究这个序列的结构，我们可以分析[连接同态](@entry_id:160713) $\partial: \pi_2(S^2) \to \pi_1(S^1)$ 本身。考虑序列片段 $\pi_2(S^3) \to \pi_2(S^2) \xrightarrow{\partial} \pi_1(S^1) \to \pi_1(S^3)$。代入已知的同伦群 $\pi_2(S^3) = 0$, $\pi_1(S^3) = 0$, $\pi_2(S^2) \cong \mathbb{Z}$, $\pi_1(S^1) \cong \mathbb{Z}$，我们得到：
$$ 0 \to \mathbb{Z} \xrightarrow{\partial} \mathbb{Z} \to 0 $$
正合性在左边的 $\mathbb{Z}$ 处意味着 $\partial$ 是[单射](@entry_id:183792)（核为 $0$），在右边的 $\mathbb{Z}$ 处意味着 $\partial$ 是满射（像为 $\mathbb{Z}$）。因此，[连接同态](@entry_id:160713) $\partial$ 本身就是一个同构。这个事实不仅给出了群的结构，还揭示了Hopf[纤维化](@entry_id:203334)中不同维度[同伦群](@entry_id:159885)之间相互作用的精确代数方式。

### 在[李群](@entry_id:137659)与对称性中的应用

[李群](@entry_id:137659)是描述连续对称性的数学对象，在物理学和几何学中扮演着核心角色。它们的拓扑结构，特别是[同伦群](@entry_id:159885)，具有深刻的物理意义。纤维化[长正合序列](@entry_id:153438)是研究[李群](@entry_id:137659)[拓扑性质](@entry_id:141605)的有力工具。

一个典型的例子是[特殊正交群](@entry_id:146418) $SO(n)$，即 $n$ 维欧几里得空间中保持定向的旋转群。考虑映射 $p: SO(3) \to S^2$，它将一个旋转矩阵 $R$ 映到它作用于一个固定[单位向量](@entry_id:165907)（如北极点）的结果 $R\mathbf{v}$。这是一个[纤维化](@entry_id:203334)，其纤维是所有保持向量 $\mathbf{v}$ 不变的旋转，这个[稳定子群](@entry_id:137216)同构于 $SO(2)$，拓扑上即为圆周 $S^1$。因此，我们有[纤维化](@entry_id:203334) $SO(2) \to SO(3) \to S^2$。

为了计算 $SO(3)$ 的基本群 $\pi_1(SO(3))$，我们写下长正合序列的相关部分：
$$ \pi_2(SO(3)) \to \pi_2(S^2) \xrightarrow{\partial} \pi_1(SO(2)) \to \pi_1(SO(3)) \to \pi_1(S^2) $$
我们使用以下已知信息：$\pi_2(SO(3))=0$（这是一个非平凡的事实），$\pi_2(S^2) \cong \mathbb{Z}$，$\pi_1(SO(2)) \cong \pi_1(S^1) \cong \mathbb{Z}$，以及 $\pi_1(S^2)=0$。序列变为：
$$ 0 \to \mathbb{Z} \xrightarrow{\partial} \mathbb{Z} \to \pi_1(SO(3)) \to 0 $$
从这个序列我们可以看出，$\pi_1(SO(3))$ 同构于 $\mathbb{Z}/\operatorname{im}(\partial)$。这里的关键在于确定[连接同态](@entry_id:160713) $\partial$ 的像。一个更深入的分析表明（这超出了本章范围，但结果是标准的），$\partial$ 将 $\pi_2(S^2)$ 的生成元映为 $\pi_1(SO(2))$ 生成元的两倍。换句话说，$\partial$ 是一个乘以 $2$ 的映射。因此，它的像是 $2\mathbb{Z}$。于是我们得到了一个至关重要的计算结果：
$$ \pi_1(SO(3)) \cong \mathbb{Z}/2\mathbb{Z} \cong \mathbb{Z}_2 $$
这个结果表明，在旋转群 $SO(3)$ 中存在一种无法收缩为一点的回路，但走过两次后就可以收缩。这在量子力学中表现为自旋为 $1/2$ 粒子的存在，例如电子，它需要旋转 $720^\circ$（而不是 $360^\circ$）才能恢复到原始状态。

此外，长正合序列还能揭示[李群](@entry_id:137659)[同伦群](@entry_id:159885)的“稳定”行为。考虑由标准嵌入诱导的纤维化序列 $SO(n) \to SO(n+1) \to S^n$，对所有 $n \ge 2$ 均成立。对于任意固定的 $k \ge 1$，长正合序列的片段为：
$$ \pi_{k+1}(S^n) \to \pi_k(SO(n)) \to \pi_k(SO(n+1)) \to \pi_k(S^n) $$
代数拓扑的一个基本结论是，当维数 $i  j$ 时，[球面的同伦群](@entry_id:160393) $\pi_i(S^j)$ 是平凡的。因此，如果我们选择的 $n$ 足够大，使得 $k  n$ 和 $k+1  n$ 同时成立（即 $n > k+1$），那么序列两端的群 $\pi_k(S^n)$ 和 $\pi_{k+1}(S^n)$ 都将是平凡群。根据正合性，这迫使中间的映射成为一个同构：
$$ \pi_k(SO(n)) \cong \pi_k(SO(n+1)) \quad \text{for } n > k+1 $$
这意味着对于固定的维度 $k$，只要我们考虑的旋转群的维数 $n$ 足够大，其 $k$-阶[同伦群](@entry_id:159885)就不再变化，达到了一个稳定值。这个现象称为[同伦群](@entry_id:159885)的稳定性，是通向更深刻的[博特周期性](@entry_id:158449)（Bott periodicity）理论的第一步。

### 与[纤维丛](@entry_id:159565)、[示性类](@entry_id:160596)和几何学的联系

纤维化是比几何概念“[纤维丛](@entry_id:159565)”更宽泛的拓扑概念，但许多重要的[纤维丛](@entry_id:159565)都是[纤维化](@entry_id:203334)。因此，长正合序列在微分几何中也有着广泛的应用。

一个例子是[流形](@entry_id:153038)的单位[切丛](@entry_id:161294)。对于二维球面 $S^2$，其单位[切丛](@entry_id:161294) $T_1S^2$ 是所有附着在 $S^2$ 上每一点的单位长度[切向量](@entry_id:265494)的集合。存在一个自然的[投影映射](@entry_id:153398) $p: T_1S^2 \to S^2$，将每个切向量映到它的作用点。这是一个[纤维化](@entry_id:203334)，其在任意一点的纤维都是该点所有[单位切向量](@entry_id:262985)组成的圆周，即 $S^1$。因此我们有[纤维化](@entry_id:203334) $S^1 \to T_1S^2 \to S^2$。

为了计算 $T_1S^2$ 的基本群，我们考察长正合序列：
$$ \pi_2(T_1S^2) \to \pi_2(S^2) \xrightarrow{\partial} \pi_1(S^1) \to \pi_1(T_1S^2) \to \pi_1(S^2) $$
代入已知群 $\pi_2(S^2) \cong \mathbb{Z}$, $\pi_1(S^1) \cong \mathbb{Z}$, $\pi_1(S^2) = 0$，序列变为：
$$ \pi_2(T_1S^2) \to \mathbb{Z} \xrightarrow{\partial} \mathbb{Z} \to \pi_1(T_1S^2) \to 0 $$
一个深刻的几何结果（Gysin 序列理论的一部分）指出，对于[单位球](@entry_id:142558)面丛，[连接同态](@entry_id:160713) $\partial: \pi_2(B) \to \pi_1(F)$ 的行为由基空间 $B$ 的[欧拉示性数](@entry_id:152513) $\chi(B)$ 决定。在此例中，$\partial$ 是一个从 $\mathbb{Z}$ 到 $\mathbb{Z}$ 的映射，由乘以 $\chi(S^2)$ 给出。由于 $\chi(S^2)=2$，$\partial$ 就是乘以 $2$ 的映射。因此，$\operatorname{im}(\partial) = 2\mathbb{Z}$。根据正合性，我们得到：
$$ \pi_1(T_1S^2) \cong \mathbb{Z} / \operatorname{im}(\partial) \cong \mathbb{Z} / 2\mathbb{Z} \cong \mathbb{Z}_2 $$
这说明 $S^2$ 的单位[切丛](@entry_id:161294)的[基本群](@entry_id:146111)是二阶[循环群](@entry_id:138668)。这个空间与 $SO(3)$ 和三维[实射影空间](@entry_id:149094) $\mathbb{R}P^3$ 密切相关，它们都有相同的[基本群](@entry_id:146111) $\mathbb{Z}_2$。

[长正合序列](@entry_id:153438)的思想也可以推广到同调群。对于一个以圆周 $S^1$ 为基空间的[纤维化](@entry_id:203334)，存在一个称为王序列（Wang sequence）的[长正合序列](@entry_id:153438)。考虑[克莱因瓶](@entry_id:149661) $K$，它可以看作一个以 $S^1$ 为纤维，以 $S^1$ 为基空间的[纤维丛](@entry_id:159565)。这个丛是“扭曲”的，其扭曲程度由一个称为“单延”（[monodromy](@entry_id:174849)）的映射 $h: S^1 \to S^1$ 描述，这里 $h$ 是一个反射。相应的王序列（对于整系数同调群）片段为：
$$ \dots \to H_1(S^1) \xrightarrow{h_* - \operatorname{id}} H_1(S^1) \to H_1(K) \to H_0(S^1) \xrightarrow{h_* - \operatorname{id}} H_0(S^1) \to \dots $$
我们知道 $H_1(S^1) \cong \mathbb{Z}$，并且反射诱导的映射 $h_*$ 在 $H_1$ 上是乘以 $-1$。在 $H_0(S^1) \cong \mathbb{Z}$ 上，$h_*$ 是恒等映射（乘以 $1$）。因此，$h_* - \operatorname{id}$ 在 $H_1$ 上是乘以 $-2$，在 $H_0$ 上是零映射。序列变为：
$$ \mathbb{Z} \xrightarrow{\times(-2)} \mathbb{Z} \to H_1(K) \to \mathbb{Z} \xrightarrow{0} \mathbb{Z} $$
通过正合性分析，我们得到一个短[正合序列](@entry_id:151503) $0 \to \mathbb{Z}_2 \to H_1(K) \to \mathbb{Z} \to 0$。由于 $\mathbb{Z}$ 是自由[阿贝尔群](@entry_id:150284)，这个序列是可裂的，因此我们得出[克莱因瓶](@entry_id:149661)的[第一同调群](@entry_id:145318)：
$$ H_1(K) \cong \mathbb{Z} \oplus \mathbb{Z}_2 $$
这个例子展示了[长正合序列](@entry_id:153438)框架的普适性，它不仅适用于[同伦群](@entry_id:159885)，也适用于同调群，并能有效地处理由单延引起的扭曲结构。

### 在[同伦论](@entry_id:150876)中的核心应用

在[代数拓扑学](@entry_id:138192)的核心领域——[同伦论](@entry_id:150876)中，[纤维化](@entry_id:203334)及其[长正合序列](@entry_id:153438)是构建理论和进行计算的基石。

#### 示性空间与[群作用](@entry_id:268812)

对于一个（离散）群 $G$，可以构造一个称为其示性空间 $BG$ 的[拓扑空间](@entry_id:155056)。这个空间是通过一个称为泛 $G$-[主丛](@entry_id:160029)的[纤维化](@entry_id:203334) $G \to EG \to BG$ 来定义的。这里的总空间 $EG$ 是一个[可缩空间](@entry_id:153541)，意味着它所有的[同伦群](@entry_id:159885)都是平凡的。利用[长正合序列](@entry_id:153438)，我们可以轻松确定 $BG$ 的[基本群](@entry_id:146111)。序列的相关部分是：
$$ \dots \to \pi_1(EG) \to \pi_1(BG) \xrightarrow{\partial} \pi_0(G) \to \pi_0(EG) \to \dots $$
由于 $EG$ 是可缩的，$\pi_1(EG)=0$ 且 $\pi_0(EG)$ 是一个单点集。因为 $G$ 是离散的，$\pi_0(G)$ 就是 $G$ 本身的集合。序列简化为 $0 \to \pi_1(BG) \to G \to \{e\} \to \dots$，这表明 $\partial$ 是一个同构。因此我们得到一个基本结果：
$$ \pi_1(BG) \cong G $$
这个结果将一个纯代数对象（群 $G$）与一个拓扑对象（空间 $BG$）的基本群联系起来。示性空间理论在矢量丛分类等领域至关重要。例如，通过考察泛复线丛[纤维化](@entry_id:203334) $S^1 \to S^\infty \to \mathbb{C}P^\infty$（其中 $S^\infty$ 是可缩的无限维球面，而 $\mathbb{C}P^\infty$ 是 $U(1) \cong S^1$ 的示性空间），[长正合序列](@entry_id:153438)可以用来计算无限维[复射影空间](@entry_id:268402) $\mathbb{C}P^\infty$ 的低维同伦群，如 $\pi_1(\mathbb{C}P^\infty)=0$ 和 $\pi_2(\mathbb{C}P^\infty) \cong \mathbb{Z}$。

Borel 构造进一步推广了这一思想。对于一个群 $G$ 在空间 $X$ 上的[自由作用](@entry_id:268835)，存在一个纤维化 $X \to EG \times_G X \to BG$，其中 $EG \times_G X$ 是[商空间](@entry_id:274314) $X/G$ 的一个同伦等价模型。长正合序列可以用来计算[商空间](@entry_id:274314)的[同伦群](@entry_id:159885)。例如，考虑[透镜空间](@entry_id:274705) $L(m,1)$，它是由[循环群](@entry_id:138668) $\mathbb{Z}_m$ [自由作用](@entry_id:268835)于奇数维球面 $S^{2n-1}$ ($n>1$) 得到的商空间。相应的 Borel 纤维化为 $S^{2n-1} \to L(m,1) \to B\mathbb{Z}_m$。由于 $S^{2n-1}$ 是单连通的（$\pi_1=0$），并且 $\pi_1(B\mathbb{Z}_m) \cong \mathbb{Z}_m$，长正合序列立即给出：
$$ \pi_1(L(m,1)) \cong \pi_1(B\mathbb{Z}_m) \cong \mathbb{Z}_m $$
这提供了一种计算具有对称性的空间商的拓扑不变量的系统方法。

#### [环路空间](@entry_id:160867)

[环路空间](@entry_id:160867)是现代[同伦论](@entry_id:150876)和理论物理（特别是弦论）中的一个中心对象。给定一个基点空间 $X$，其自由[环路空间](@entry_id:160867) $LX$ 是所有从 $S^1$ 到 $X$ 的映射构成的空间。存在一个自然的求值[纤维化](@entry_id:203334)（evaluation fibration）$\Omega X \to LX \to X$，其中纤维 $\Omega X$ 是所有基于基点的环路构成的空间。这个[纤维化的长正合序列](@entry_id:161359)将 $X$ 的同伦群与 $LX$ 和 $\Omega X$ 的[同伦群](@entry_id:159885)联系起来。

结合[同伦论](@entry_id:150876)中的一个基本同构 $\pi_n(\Omega X) \cong \pi_{n+1}(X)$，长正合序列成为一个强大的计算工具。例如，考虑 $X = \mathbb{C}P^2$。[长正合序列](@entry_id:153438)的片段为 $\pi_2(\Omega X) \to \pi_2(LX) \to \pi_2(X) \to \pi_1(\Omega X) \to \dots$。利用上述同构，并代入 $\mathbb{C}P^2$ 的已知同伦群（$\pi_3(\mathbb{C}P^2)=0$, $\pi_2(\mathbb{C}P^2) \cong \mathbb{Z}$），我们可以推导出 $\pi_2(L(\mathbb{C}P^2)) \cong \pi_2(\mathbb{C}P^2) \cong \mathbb{Z}$。

更有趣的是，[环路空间](@entry_id:160867)构造本身是[函子性](@entry_id:150069)的。一个纤维化 $F \to E \to B$ 会诱导一个[环路空间](@entry_id:160867)的[纤维化](@entry_id:203334) $LF \to LE \to LB$。将此应用于 Hopf [纤维化](@entry_id:203334) $S^1 \to S^3 \to S^2$，我们得到一个纤维化 $LS^1 \to LS^3 \to LS^2$。通过分析其长正合序列，并利用已知的[环路空间](@entry_id:160867)同伦群，可以计算出 $\pi_2(LS^2)$。相关的短[正合序列](@entry_id:151503)是 $0 \to \mathbb{Z} \to \pi_2(LS^2) \to \mathbb{Z} \to 0$。由于 $\mathbb{Z}$ 是[自由群](@entry_id:151249)，序列可裂，我们得到 $\pi_2(LS^2) \cong \mathbb{Z} \oplus \mathbb{Z}$。这个计算在弦论等领域中具有重要意义，因为[环路空间](@entry_id:160867)是弦的位形空间。

#### 同伦分解与有理[同伦](@entry_id:139266)

长正合序列是同伦分解技术的基础，如 [Postnikov 塔](@entry_id:158954)。[Postnikov 塔](@entry_id:158954)将一个任意的 CW 复形 $X$ 分解为一系列更简单的空间 $X_n$ 的反向极限，其中每个 $X_n$ 通过一个纤维化 $K(\pi_n(X), n) \to X_n \to X_{n-1}$ 从前一步得到。这里的纤维是 Eilenberg-MacLane 空间。对这个[纤维化](@entry_id:203334)反复应用长正合序列，是理解空间如何由其[同伦群](@entry_id:159885)“组装”起来的关键。

最后，[长正合序列](@entry_id:153438)在有理[同伦](@entry_id:139266)理论中表现出惊人的简化。有理[同伦群](@entry_id:159885) $\pi_n(X, \mathbb{Q})$ 定义为 $\pi_n(X) \otimes_{\mathbb{Z}} \mathbb{Q}$。由于张量积[函子](@entry_id:150427) $\otimes \mathbb{Q}$ 是正合的，[纤维化的长正合序列](@entry_id:161359)在张量化后仍然是正合的。一个重要的推论是：如果一个纤维化 $F \to E \to B$ 的基空间 $B$ 是“有理可缩”的（即其所有同伦群都是有限群，从而有理[同伦群](@entry_id:159885)为零），那么其有理[同伦](@entry_id:139266)[长正合序列](@entry_id:153438)中的 $\pi_n(B, \mathbb{Q})$ 项全部为零。这立即导致一个同构：
$$ \pi_n(F, \mathbb{Q}) \cong \pi_n(E, \mathbb{Q}) \quad \text{for } n \ge 2 $$
这意味着从纤维到总空间的包含映射 $i: F \to E$ 是一个有理同伦等价。换句话说，在忽略所有挠（torsion）信息后，纤维和总空间在拓扑上是不可区分的。这为研究复杂空间的有理[同伦型](@entry_id:148015)提供了一种强大的简化策略。

总而言之，[纤维化的长正合序列](@entry_id:161359)是连接代数与拓扑的中心桥梁之一。它不仅是一个强大的计算引擎，更是一种深刻的思维方式，使我们能够通过分解和重组来理解复杂的拓扑结构，其影响遍及现代数学和物理的众多分支。