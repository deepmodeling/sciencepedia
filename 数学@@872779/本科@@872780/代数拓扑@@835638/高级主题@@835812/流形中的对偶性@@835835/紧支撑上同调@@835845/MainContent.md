## 引言
在代数拓扑的宏伟版图中，[上同调理论](@entry_id:270863)是探索空间内在结构的不二法门。然而，经典的[上同调理论](@entry_id:270863)，如[奇异上同调](@entry_id:271229)或[德拉姆上同调](@entry_id:158673)，在面对[非紧空间](@entry_id:273664)时会暴露出其局限性。例如，它无法区分不同维度的[欧几里得空间](@entry_id:138052)，并且代数[拓扑的基](@entry_id:148152)石之一——[庞加莱对偶定理](@entry_id:274166)——也仅限于[紧致流形](@entry_id:158804)。这些问题揭示了一个知识上的缺口：我们需要一种更为精细的拓扑不变量，它既能继承[上同调](@entry_id:160558)的强大[代数结构](@entry_id:137052)，又能敏锐地捕捉到[非紧空间](@entry_id:273664)的几何与渐近特性。

本文旨在系统地介绍**[紧支撑上同调](@entry_id:634085) (Cohomology with Compact Supports)**，这一为解决上述难题而生的优美理论。通过本文的学习，读者将能够理解标准上同调的不足之处，并掌握[紧支撑上同调](@entry_id:634085)的完整框架。第一章**“原理与机制”**将从基本定义出发，深入探讨[紧支撑](@entry_id:276214)上[链复形](@entry_id:150246)的构造、关键性质以及与标准上同调的联系。第二章**“应用与跨学科联系”**将展示该理论的强大威力，通过具体计算和实例，阐明其在推广[庞加莱对偶](@entry_id:161676)、解决[纽结理论](@entry_id:141161)问题以及连接[微分几何](@entry_id:145818)等领域中的核心作用。最后，第三章**“动手实践”**提供了一系列练习，帮助读者将理论知识转化为解决实际问题的能力。

现在，让我们首先进入理论的核心，探索[紧支撑上同调](@entry_id:634085)的**原理与机制**。

## 原理与机制

在研究[拓扑空间](@entry_id:155056)的代数[不变量](@entry_id:148850)时，[奇异上同调](@entry_id:271229)是一种极其强大的工具。然而，对于[非紧空间](@entry_id:273664)，标准[上同调理论](@entry_id:270863)有时无法捕捉到空间的某些重要几何特性。例如，[欧几里得空间](@entry_id:138052) $\mathbb{R}^n$ 在所有正维度上的[上同调群](@entry_id:142450)都是平凡的，这似乎与其作为 $n$ 维[流形](@entry_id:153038)的直观感受相悖。此外，代数拓扑中的一个基石性定理——[庞加莱对偶定理](@entry_id:274166)，在其经典表述中仅适用于[紧致可定向流形](@entry_id:157578)。这些局限性促使我们寻求一种更为精细的理论，它既能保留上同调的代数威力，又能更好地适应[非紧空间](@entry_id:273664)的拓扑结构。这种理论便是**[紧支撑上同调](@entry_id:634085) (Cohomology with Compact Supports)**。本章将深入探讨[紧支撑上同调](@entry_id:634085)的定义、基本原理、计算方法及其在[非紧流形](@entry_id:185981)对偶性中的核心作用。

### 为何需要新的[上同调理论](@entry_id:270863)？

我们首先探讨为何经典的[上同调理论](@entry_id:270863)在[非紧空间](@entry_id:273664)上会遇到困难。以[德拉姆上同调](@entry_id:158673) (de Rham cohomology) 为例，它是光滑流形上同调的一种具体实现。对于一个紧致、可定向的 $n$ 维[流形](@entry_id:153038) $M$，[庞加莱对偶定理](@entry_id:274166)断言，$k$ 次[上同调群](@entry_id:142450) $H^k(M)$ 与 $n-k$ 次上同调群 $H^{n-k}(M)$ 之间存在一个非退化的配对，从而导出它们之间的同构。这个配对通[过积分](@entry_id:753033)定义：对于 $[\omega] \in H^k(M)$ 和 $[\eta] \in H^{n-k}(M)$，配对值为：
$$
\langle [\omega], [\eta] \rangle = \int_M \omega \wedge \eta
$$
这个定义之所以成立，有两个关键前提。第一，由于 $M$ 是紧致的，光滑形式 $\omega$ 和 $\eta$ 的外积 $\omega \wedge \eta$ 在 $M$ 上的积分必然收敛。第二，这个配对在同调类上是良定义的。如果 $\omega$ 被一个恰当形式 $d\alpha$ 替换，那么根据斯托克斯定理，$\int_M (d\alpha) \wedge \eta = \int_M d(\alpha \wedge \eta) = \int_{\partial M} \alpha \wedge \eta$，而紧致无边[流形](@entry_id:153038) $M$ 的边界 $\partial M$ 为空集，所以积分为零。

然而，若将[流形](@entry_id:153038) $M$ 替换为非紧的[欧几里得空间](@entry_id:138052) $\mathbb{R}^n$，这两个前提都会失效。最根本的问题在于，对于任意的闭形式 $\omega$ 和 $\eta$，它们的[楔积](@entry_id:147029)在整个 $\mathbb{R}^n$ 上的积分 $\int_{\mathbb{R}^n} \omega \wedge \eta$ 不再保证收敛。因为积分区域是无限的，被积函数如果衰减得不够快，积分值就可能发散 [@problem_id:1529975]。这一根本性的收敛问题使得上述积分配对无法直接推广到[非紧空间](@entry_id:273664)，从而导致标准[庞加莱对偶定理](@entry_id:274166)的失效。正是为了克服这一障碍，我们需要对上同调的定义进行修正，引入“[紧支撑](@entry_id:276214)”这一概念。

### [紧支撑上同调](@entry_id:634085)的构造

[紧支撑上同调](@entry_id:634085)的核心思想是只考虑那些“在无穷远处为零”的上链。

#### [紧支撑](@entry_id:276214)上[链复形](@entry_id:150246)

对于一个拓扑空间 $X$，一个奇异 $k$-上链 $\phi \in C^k(X; G)$ 是一个从奇异 $k$-链群到系数[阿贝尔群](@entry_id:150284) $G$ 的同态。$\phi$ 的**支撑 (support)**，记作 $\text{supp}(\phi)$，被定义为 $X$ 中最小的[闭子集](@entry_id:155133) $A$，使得对于任何支撑完全包含在 $X \setminus A$ 中的奇异 $k$-链 $\sigma$，都有 $\phi(\sigma) = 0$。如果 $\text{supp}(\phi)$ 是 $X$ 中的一个紧[子集](@entry_id:261956)，我们称 $\phi$ 是一个**具有[紧支撑](@entry_id:276214)的上链 (cochain with compact support)**。

所有 $k$ 次[紧支撑](@entry_id:276214)上链构成的集合记为 $C_c^k(X; G)$。可以验证，它在逐[点加法](@entry_id:177138)下构成 $C^k(X; G)$ 的一个[子群](@entry_id:146164)。至关重要的一点是，标准的上边缘算子 $\delta: C^k(X; G) \to C^{k+1}(X; G)$ 将[紧支撑](@entry_id:276214)上[链映射](@entry_id:268209)到[紧支撑](@entry_id:276214)上链。也就是说，$\delta$ 可以被限制为 $C_c^*(X;G)$ 上的一个映射 $\delta: C_c^k(X; G) \to C_c^{k+1}(X; G)$。这是因为一个链的边界的支撑包含于该链的支撑之内，所以如果一个 $(k+1)$-链 $\sigma$ 的支撑位于 $\text{supp}(\phi)$ 之外，那么它的边界 $\partial \sigma$ 的支撑也位于 $\text{supp}(\phi)$ 之外，从而 $(\delta\phi)(\sigma) = \phi(\partial\sigma) = 0$。这表明 $\text{supp}(\delta\phi) \subseteq \text{supp}(\phi)$，因此如果 $\phi$ 的支撑是紧的，那么 $\delta\phi$ 的支撑也是紧的。

我们通过一个具体的例子来理解支撑和上边缘算子的相互作用 [@problem_id:1641331]。考虑 $X=\mathbb{R}^n$ ($n \ge 2$)，令 $D$ 为其中的闭单位球。定义一个 0-上链 $\phi \in C^0(\mathbb{R}^n; \mathbb{Z})$ 为 $D$ 的特征函数，即 $\phi(p)=1$ 如果 $p \in D$，否则 $\phi(p)=0$。$\phi$ 的支撑是 $D$，这是一个紧集，故 $\phi \in C_c^0(\mathbb{R}^n; \mathbb{Z})$。它的上边缘 $\delta\phi$ 是一个 1-上链。对于任意 1-单纯形 $\sigma: \Delta^1 \to \mathbb{R}^n$，我们有 $(\delta\phi)(\sigma) = \phi(\sigma(1)) - \phi(\sigma(0))$。这个值非零，当且仅当 $\sigma$ 的一个端点在 $D$ 内，另一个在 $D$ 外。这意味着任何穿过 $D$ 的边界 $S^{n-1}$ 的路径都会被 $\delta\phi$ “探测”到。可以证明，$\delta\phi$ 的支撑恰好是[单位球](@entry_id:142558)面 $S^{n-1}$。这个例子清晰地表明，即使上边缘算子可能改变上链的支撑，它仍将[紧支撑](@entry_id:276214)上链映为[紧支撑](@entry_id:276214)上链（这里 $D$ 和 $S^{n-1}$ 都是[紧集](@entry_id:147575)）。

由于 $\delta \circ \delta = 0$ 依然成立，我们便得到了一个[子复形](@entry_id:264130) $(C_c^*(X; G), \delta)$，称为**[紧支撑](@entry_id:276214)上[链复形](@entry_id:150246) (cochain complex with compact supports)**。该复形的上同调群定义为 $X$ 的**[紧支撑上同调](@entry_id:634085)群**，记作 $H_c^k(X; G)$。
$$
H_c^k(X; G) = Z_c^k(X; G) / B_c^k(X; G)
$$
其中 $Z_c^k(X; G)$ 是 $C_c^k(X; G)$ 中的闭上链（cocycles），而 $B_c^k(X; G) = \delta(C_c^{k-1}(X; G))$ 是 $C_c^{k-1}(X; G)$ 中元素的上边缘（coboundaries）。

值得注意的是，$B_c^k(X;G)$ ([紧支撑](@entry_id:276214)上链的上边缘) 与 $B^k(X;G) \cap C_c^k(X;G)$ (恰好具有[紧支撑](@entry_id:276214)的上边缘) 两者之间存在微妙的差别。一个上边缘可能自身是[紧支撑](@entry_id:276214)的，但它未必是某个[紧支撑](@entry_id:276214)上链的上边缘。这个问题 [@problem_id:1641346] 中的例子有助于我们思考。考虑 $\mathbb{R}$ 上的 1-上链 $\phi(\sigma) = \sigma(1)-\sigma(0)$。它是 0-上链 $f(x)=x$ 的上边缘，$\phi = \delta f$。然而，$f(x)=x$ 显然不具有[紧支撑](@entry_id:276214)。可以证明，不存在任何具有[紧支撑](@entry_id:276214)的 0-上链 $g$ 使得 $\phi = \delta g$。因为如果 $g$ 的支撑是紧的，那么在支撑之外 $g$ 恒为零。取 $a, b$ 在 $g$ 的支撑之外，则 $(\delta g)(\sigma) = g(b)-g(a) = 0-0=0$，但这与 $\phi(\sigma) = b-a \neq 0$ 矛盾。这个例子说明，要求上链本身具有[紧支撑](@entry_id:276214)是一个比要求其上边缘具有[紧支撑](@entry_id:276214)更强的条件，而这正是 $H_c^*$ 与 $H^*$ 产生差异的根源。

### 基本性质与计算

[紧支撑上同调](@entry_id:634085)与普通上同调之间有着密切的联系，尤其是在紧空间上。

#### 与普通上同调的关系

对于一个**紧空间** $X$，其上的任何上链都自动具有[紧支撑](@entry_id:276214)，因为 $X$ 本身就是一个紧集，可以作为任何上链支撑集的[上界](@entry_id:274738)。因此，$C_c^k(X; G) = C^k(X; G)$ 对所有 $k$ 成立。这意味着它们的[上同调群](@entry_id:142450)是同构的：
$$
H_c^k(X; G) \cong H^k(X; G) \quad (\text{当 } X \text{ 是紧空间时})
$$
另一种理解此同构的方式是通过[紧支撑上同调](@entry_id:634085)的另一个等价定义：**正向极限 (direct limit) 定义**。对于一个局部紧 Hausdorff 空间 $X$，
$$
H_c^k(X; G) = \varinjlim_{K} H^k(X, X \setminus K; G)
$$
这里的极限是在 $X$ 的所有紧[子集](@entry_id:261956) $K$构成的[有向集](@entry_id:155049)上取定的（按包含关系排序）。如果 $X$ 本身是紧的，那么 $K=X$ 是这个[有向集](@entry_id:155049)中的一个终极对象。根据正向极限的一般性质，极限同构于在终极对象处的值。因此，
$$
H_c^k(X; G) \cong H^k(X, X \setminus X; G) = H^k(X, \emptyset; G) \cong H^k(X; G)
$$
这个问题 [@problem_id:1641386] 就利用 $T^2$ 这个例子阐释了这一点，指明了对于[紧空间](@entry_id:155073)而言，这个正向极限的塌缩是两者同构最根本的原因。

#### 典范例子：[欧几里得空间](@entry_id:138052)

对于[非紧空间](@entry_id:273664)，[紧支撑上同调](@entry_id:634085)展现出其独特的性质。我们来计算 $H_c^k(\mathbb{R}^n; \mathbb{Z})$ [@problem_id:1641388]。利用正向极限的定义，我们可以用一族逐渐“填满”$\mathbb{R}^n$ 的紧集（例如半径为 $R$ 的[闭球](@entry_id:157850) $\overline{B}_R$）来[计算极限](@entry_id:138209)：
$$
H_c^k(\mathbb{R}^n; \mathbb{Z}) \cong \varinjlim_{R \to \infty} H^k(\mathbb{R}^n, \mathbb{R}^n \setminus \overline{B}_R; \mathbb{Z})
$$
根据[切除定理](@entry_id:159397) (Excision Theorem)，[相对上同调](@entry_id:272456)群 $H^k(\mathbb{R}^n, \mathbb{R}^n \setminus \overline{B}_R; \mathbb{Z})$ 同构于 $H^k(B_{R'}, B_{R'} \setminus \overline{B}_R; \mathbb{Z})$，其中 $R'>R$。后者又[形变收缩](@entry_id:148036)到 $H^k(\overline{B}_R, \partial \overline{B}_R; \mathbb{Z})$。利用对 $(\overline{B}_R, \partial \overline{B}_R)$ 的长正合列和 $\overline{B}_R$ 的[可缩性](@entry_id:154431)，可以算出：
$$
H^k(\overline{B}_R, \partial \overline{B}_R; \mathbb{Z}) \cong \tilde{H}^{k-1}(\partial \overline{B}_R; \mathbb{Z}) \cong \tilde{H}^{k-1}(S^{n-1}; \mathbb{Z})
$$
我们知道球面 $S^{n-1}$ 的[约化上同调](@entry_id:268050)群在 $k-1 = n-1$（即 $k=n$）时为 $\mathbb{Z}$，其他维度为 0。因此，
$$
H_c^k(\mathbb{R}^n; \mathbb{Z}) \cong \begin{cases} \mathbb{Z}  \text{if } k=n \\ 0  \text{if } k \neq n \end{cases}
$$
这个结果意义非凡：[紧支撑上同调](@entry_id:634085)成功地“探测”到了 $\mathbb{R}^n$ 的 $n$ 维特性，这与 $H^k(\mathbb{R}^n)$ 在 $k>0$ 时恒为零的平庸结果形成鲜明对比。

#### 与[单点紧化](@entry_id:153786)的联系

上述计算结果暗示了一个深刻的联系。一个局部紧 Hausdorff 空间 $X$ 的**[单点紧化](@entry_id:153786) (one-point compactification)** $X^+$ 是通过添加一个“[无穷远点](@entry_id:172513)”$\infty$ 得到的紧空间。对于 $X=\mathbb{R}^n$，其[单点紧化](@entry_id:153786) $X^+$ [同胚](@entry_id:146933)于球面 $S^n$。我们刚刚计算得到的 $H_c^k(\mathbb{R}^n)$ 恰好同构于 $S^n$ 的[约化上同调](@entry_id:268050) $\tilde{H}^k(S^n)$。这并非巧合，而是一个普适的定理：
$$
H_c^k(X; G) \cong \tilde{H}^k(X^+; G)
$$
这个同构为计算[紧支撑上同调](@entry_id:634085)提供了强大的武器，将[非紧空间](@entry_id:273664)的问题转化为了我们更熟悉的[紧空间](@entry_id:155073)（及其[上同调](@entry_id:160558)）的问题 [@problem_id:1641388]。

### [函子性](@entry_id:150069)与结构

如同任何[上同调理论](@entry_id:270863)，我们需要理解它在映射下的表现（[函子性](@entry_id:150069)）以及它所满足的[代数结构](@entry_id:137052)（如长正合列）。

#### [诱导同态](@entry_id:266478)与 proper 映射

普通[上同调](@entry_id:160558)是[逆变](@entry_id:192290)的函子：任何连续映射 $f: X \to Y$ 都诱导一个**[拉回](@entry_id:160816)同态 (pullback homomorphism)** $f^*: H^k(Y) \to H^k(X)$。对于[紧支撑上同调](@entry_id:634085)，情况更为微妙。一个[连续映射](@entry_id:153855) $f: X \to Y$ 要诱导一个定义良好的[拉回](@entry_id:160816)同态 $f^*: H_c^k(Y) \to H_c^k(X)$，需要满足一个额外的条件：$f$ 必须是 **proper 映射 (proper map)**。

一个连续映射 $f: X \to Y$ 被称为 **proper 映射**，如果 $Y$ 中任意紧[子集](@entry_id:261956) $K$ 的原像 $f^{-1}(K)$ 在 $X$ 中也是[紧集](@entry_id:147575)。这个条件保证了 $f$ 的[拉回](@entry_id:160816)操作 $f^*$ 会将 $Y$ 上的[紧支撑](@entry_id:276214)上链映为 $X$ 上的[紧支撑](@entry_id:276214)上链。若 $f$ 不是 proper 映射，一个 $Y$ 上的[紧支撑](@entry_id:276214)上链的[拉回](@entry_id:160816)就可能不再具有[紧支撑](@entry_id:276214)，从而 $f^*$ 无法在[紧支撑](@entry_id:276214)上[链复形](@entry_id:150246)的层面上被定义。

让我们看两个例子。
1.  **Proper 映射的例子** [@problem_id:1641375]: 考虑 $f: \mathbb{R} \to \mathbb{R}$，$f(x)=x^3-x$。由于 $\lim_{|x| \to \infty} |f(x)| = \infty$，任何 $\mathbb{R}$ 中的[有界集](@entry_id:157754)（因此是任何紧集）的[原像](@entry_id:150899)也必然是有界的。由于 $f$ 连续，[闭集](@entry_id:136446)[原像](@entry_id:150899)是[闭集](@entry_id:136446)。因此，紧集的[原像](@entry_id:150899)是闭合且有界的，故也是紧集。所以 $f$ 是一个 proper 映射，它诱导了良定义的同态 $f^*: H_c^k(\mathbb{R}) \to H_c^k(\mathbb{R})$。

2.  **非 Proper 映射的例子** [@problem_id:1641328]: 考虑[投影映射](@entry_id:153398) $p: \mathbb{R}^2 \to \mathbb{R}$，$p(x,y)=x$。取 $\mathbb{R}$ 中的紧集 $K=[0,1]$。它的[原像](@entry_id:150899) $p^{-1}(K) = [0,1] \times \mathbb{R}$ 是一个无限長的条带，在 $\mathbb{R}^2$ 中显然非紧。因此，$p$ 不是 proper 映射。这意味着不存在一个自然定义的[拉回](@entry_id:160816)同态 $p_c^*: H_c^k(\mathbb{R}) \to H_c^k(\mathbb{R}^2)$。即使我们知道 $H_c^1(\mathbb{R}) \cong \mathbb{Z}$ 而 $H_c^1(\mathbb{R}^2)=0$，也不能谈论一个从 $\mathbb{Z}$到 $0$ 的“诱导映射”，因为这个映射的构造从根本上就失败了。

#### 长正合列

与普通[上同调类](@entry_id:263961)似，[紧支撑上同调](@entry_id:634085)也满足重要的[正合序列](@entry_id:151503)性质。对于一个局部紧 Hausdorff 空间 $X$、一个开[子集](@entry_id:261956) $U$ 及其闭[补集](@entry_id:161099) $F = X \setminus U$，存在一个**长正合列**：
$$
\dots \to H_c^k(U) \to H_c^k(X) \to H_c^k(F) \to H_c^{k+1}(U) \to \dots
$$
注意，这里的 $H_c^k(F)$ 是有意义的，因为作为 $X$ 的[闭子集](@entry_id:155133)，$F$ 也是局部紧的。这个长正合列是计算未知空间[紧支撑上同调](@entry_id:634085)的有力工具。

例如，我们可以用它来计算 $Y = \mathbb{R} \setminus [0,1]$ 的[紧支撑](@entry_id:276214) Betti 数 [@problem_id:1641368]。令 $X=\mathbb{R}$，$U=Y$，以及 $F=[0,1]$。我们将已知信息代入长正合列：
-   $H_c^0(\mathbb{R})=0$, $H_c^1(\mathbb{R}) \cong \mathbb{Z}$，更高阶为 0。
-   $F=[0,1]$ 是[紧空间](@entry_id:155073)，所以 $H_c^k(F) \cong H^k(F)$。由于 $F$ 可缩，所以 $H_c^0(F) \cong \mathbb{Z}$，更高阶为 0。

正合列的相关部分为：
$$
\cdots \to H_c^0(\mathbb{R}) \to H_c^0([0,1]) \to H_c^1(Y) \to H_c^1(\mathbb{R}) \to H_c^1([0,1]) \to \cdots
$$
代入已知群，得到：
$$
\cdots \to 0 \to \mathbb{Z} \to H_c^1(Y) \to \mathbb{Z} \to 0 \to \cdots
$$
这导出一个短正合列 $0 \to \mathbb{Z} \to H_c^1(Y) \to \mathbb{Z} \to 0$。由此可知 $H_c^1(Y)$ 的秩为 $1+1=2$。另外，由于 $Y=(-\infty,0) \cup (1,\infty)$ 的两个连通分支都是非紧的，任何在其上的[紧支撑](@entry_id:276214) 0-上链（局部常值函数）必须为零，所以 $H_c^0(Y)=0$。因此，我们计算出 $h_c^0(Y)=0$ 和 $h_c^1(Y)=2$。

### [非紧流形](@entry_id:185981)的[庞加莱对偶](@entry_id:161676)

现在我们回到最初的动机：为[非紧流形](@entry_id:185981)建立[庞加莱对偶](@entry_id:161676)。[紧支撑上同调](@entry_id:634085)正是缺失的关键环节。

经典[庞加莱对偶](@entry_id:161676)的失败可以通过一个最简单的例子——实直线 $\mathbb{R}$——清晰地展示出来 [@problem_id:1666082]。作为一个 1-维[流形](@entry_id:153038)，如果对偶成立，我们期望 $H_0(\mathbb{R})$ 与 $H^{1-0}(\mathbb{R})=H^1(\mathbb{R})$ 同构。然而，$\mathbb{R}$ 是连通的，所以 $H_0(\mathbb{R}; \mathbb{Z}) \cong \mathbb{Z}$。但 $\mathbb{R}$ 也是可缩的，所以 $H^1(\mathbb{R}; \mathbb{Z})=0$。显然 $\mathbb{Z} \not\cong 0$，因此经典对偶不成立。

修正后的**[非紧流形](@entry_id:185981)[庞加莱对偶定理](@entry_id:274166)**阐明：对于一个可定向的 $n$ 维[流形](@entry_id:153038) $M$（不要求紧致），其同调群与[紧支撑上同调](@entry_id:634085)群之间存在如下同构：
$$
H_c^k(M; G) \cong H_{n-k}(M; G)
$$
让我们用 $\mathbb{R}$ 来检验这个新版本。我们期望 $H_c^1(\mathbb{R})$ 与 $H_{1-1}(\mathbb{R})=H_0(\mathbb{R})$ 同构。我们已经知道 $H_0(\mathbb{R}; \mathbb{Z}) \cong \mathbb{Z}$。根据前面关于[欧几里得空间](@entry_id:138052)的计算，$H_c^1(\mathbb{R}; \mathbb{Z}) \cong \mathbb{Z}$。两者确实同构！这个修正后的对偶关系完美地运作了 [@problem_id:1666082]。

这个定理不仅在理论上优美，在实践中也非常有用。例如，我们可以用它来计算一个亏格为 $g$ 的[曲面](@entry_id:267450) $S_g$ 去掉 $m$ 个点后得到的[非紧流形](@entry_id:185981) $X_{g,m}$ 的[紧支撑上同调](@entry_id:634085) [@problem_id:1664185]。根据[庞加莱对偶](@entry_id:161676)，$H_c^1(X_{g,m}; \mathbb{Z}) \cong H_{2-1}(X_{g,m}; \mathbb{Z}) = H_1(X_{g,m}; \mathbb{Z})$。我们可以通过计算欧拉示性数 $\chi(X_{g,m}) = \chi(S_g) - m = (2-2g) - m$ 来求出 $H_1$ 的秩。因为 $X_{g,m}$ 连通且非紧，所以 $b_0=1, b_2=0$。由[欧拉-庞加莱公式](@entry_id:274300) $\chi = b_0 - b_1 + b_2$，我们得到 $b_1 = b_0 - \chi = 1 - (2-2g-m) = 2g+m-1$。因此，$H_c^1(X_{g,m}; \mathbb{Z})$ 的秩就是 $2g+m-1$。

此外，还存在配对普通[上同调](@entry_id:160558)和[紧支撑上同调](@entry_id:634085)的另一版本对偶：$H^k(M)$ 与 $H_c^{n-k}(M)$ 互为[对偶向量空间](@entry_id:193439)。这正是对最初积分配对失效问题的完美解决方案：通过要求其中一个上同调类具有[紧支撑](@entry_id:276214)，保证了积分 $\int_M \omega \wedge \eta$ 的收敛性，从而恢复了对偶结构。

总之，[紧支撑上同调](@entry_id:634085)是代数拓扑中一个深刻而必要的概念。它不仅弥补了普通上同调在处理[非紧空间](@entry_id:273664)时的不足，还使得[庞加莱对偶](@entry_id:161676)这一美丽的对称性原理得以推广到更广阔的[流形](@entry_id:153038)世界中。