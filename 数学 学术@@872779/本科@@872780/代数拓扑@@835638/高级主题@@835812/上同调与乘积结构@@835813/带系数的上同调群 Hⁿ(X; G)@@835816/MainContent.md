## 引言
在代数拓扑的宏伟版图上，[上同调理论](@entry_id:270863)以其深刻的洞察力和强大的计算能力，成为继同调论之后又一核心支柱。它不仅是同调论的“对偶”镜像，更通过引入可变的系数群和丰富的[代数结构](@entry_id:137052)（如上积），为我们提供了更加精细和强大的工具来探测拓扑空间的内在性质。许多仅用同调群无法区分的空间或无法解决的几何问题，在上同调的视角下迎刃而解。

本文旨在系统地引导读者深入[带系数上同调](@entry_id:160573)群的世界。我们将分三步展开：首先，在“原理与机制”一章中，我们将从上[链复形](@entry_id:150246)出发，建立[上同调群](@entry_id:142450)的形式化定义，并详细阐述泛系数定理和长正合序列这两个连接同调与上同调、以及不同系数上同调之间的关键桥梁。接着，在“应用与跨学科联系”一章，我们将见证理论的力量，学习如何利用[上同调环](@entry_id:160158)结构区分[拓扑空间](@entry_id:155056)，理解其在[流形](@entry_id:153038)对偶性中的核心作用，并探索其作为示性类和阻碍理论的基础。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者巩固所学知识并将其付诸实践。

让我们从构建[上同调理论](@entry_id:270863)的基石开始，一同探索其精妙的原理与机制。

## 原理与机制

继前一章对上同调基本思想的介绍之后，本章将深入探讨其形式化定义和核心机制。我们将引入系数群的概念，这极大地扩展了[上同调理论](@entry_id:270863)的范畴和威力。通过研究上[链复形](@entry_id:150246)、泛系数定理以及系数变化所产生的[长正合序列](@entry_id:153438)，我们将揭示[上同调群](@entry_id:142450)丰富的[代数结构](@entry_id:137052)，并阐明其与同调群之间的深刻对偶关系。

### 上[链复形](@entry_id:150246)：定义与基本性质

[上同调](@entry_id:160558)的计算框架始于 **上[链复形](@entry_id:150246) (cochain complex)**。与同调理论中的链群（由[奇异单纯形](@entry_id:265569)生成的自由阿贝尔群）相对，上链群则由定义在这些单纯形上的函数构成。

给定一个[拓扑空间](@entry_id:155056) $X$ 和一个[阿贝尔群](@entry_id:150284) $G$（称为 **系数群 (coefficient group)**），一个 **$n$-上链 ($n$-cochain)** 是一个函数 $\phi: S_n(X) \to G$，其中 $S_n(X)$ 是 $X$ 中所有奇异 $n$-单纯形的集合。所有 $n$-上链的集合构成一个阿贝尔群，记为 $C^n(X; G)$，其群运算由 $G$ 中的运算逐点定义。

与[链复形](@entry_id:150246)中的[边界算子](@entry_id:160216) $\partial$ 类似，我们在上链群之间定义 **上[边界算子](@entry_id:160216) (coboundary operator)** $\delta^n: C^n(X; G) \to C^{n+1}(X; G)$。对于一个 $n$-上链 $\phi$ 和一个奇异 $(n+1)$-单纯形 $\sigma: \Delta^{n+1} \to X$，$\delta^n \phi$ 的定义如下：
$$ (\delta^n \phi)(\sigma) = \phi(\partial_{n+1} \sigma) $$
其中 $\partial_{n+1}$ 是标准的[边界算子](@entry_id:160216)，$\phi$ 的作用线性地延拓到链群 $C_{n}(X)$ 上。

[上同调理论](@entry_id:270863)的一个基石是性质 $\delta \circ \delta = 0$。这个性质保证了 $\text{im}(\delta^{n-1}) \subseteq \ker(\delta^n)$，从而使得[商群](@entry_id:145113) $H^n(X; G) = \ker(\delta^n) / \text{im}(\delta^{n-1})$ 的定义是良定的。这个商群就是 $X$ 的 **$n$ 阶[上同调群](@entry_id:142450) (n-th cohomology group)**。

一个关键问题是：为什么系数群 $G$ 必须是[阿贝尔群](@entry_id:150284)？[@problem_id:1640941] 这个问题揭示了背后的代[数基](@entry_id:634389)础。让我们考虑如果 $G$ 是一个[非阿贝尔群](@entry_id:141904)（乘法记法），上[边界算子](@entry_id:160216)会如何定义。一种自然的推广是使用交错积：
$$ (\delta \phi)(\sigma) = \prod_{i=0}^{k+1} \phi(\sigma_i)^{(-1)^i} = \phi(\sigma_0) \cdot \phi(\sigma_1)^{-1} \cdot \phi(\sigma_2) \cdot \ldots $$
其中 $\sigma_i$ 是 $\sigma$ 的第 $i$ 个面。当我们计算 $\delta^2 \phi$ 时，会得到一个双重乘积。对一个 $(k+2)$-单纯形 $\sigma$ 求值，我们有：
$$ (\delta^2 \phi)(\sigma) = \prod_{j=0}^{k+2} \left[ (\delta \phi)(\sigma_j) \right]^{(-1)^j} = \prod_{j=0}^{k+2} \left[ \prod_{i=0}^{k+1} \phi((\sigma_j)_i)^{(-1)^i} \right]^{(-1)^j} $$
问题出现在下一步。为了重组乘积中的项以利用单纯恒等式 $(\sigma_j)_i = (\sigma_i)_{j-1}$ (对于 $i \lt j$) 来进行对消，我们需要交换乘积的顺序。例如，将指数 $(-1)^j$ 分配到内部乘积中：
$$ \left( A_0 \cdot A_1 \cdot \ldots \cdot A_{k+1} \right)^{-1} $$
在[非阿贝尔群](@entry_id:141904)中，上式等于 $A_{k+1}^{-1} \cdot \ldots \cdot A_1^{-1} \cdot A_0^{-1}$，乘积的顺序被颠倒了。然而，若要推导 $\delta^2 = 0$，则需要能够自由地交换各项的顺序，例如将 $\phi((\sigma_j)_i)$ 和 $\phi((\sigma_k)_l)$ 交换位置。这恰恰要求 $G$ 中的运算是可交换的，即 $G$ 必须是一个阿贝尔群。如果 $G$ 是[阿贝尔群](@entry_id:150284)（加法记法），那么所有运算都是可交换的，对消过程可以顺利进行，最终得到 $\delta^2 \phi = 0$。因此，系数群的阿贝尔性是[上同调理论](@entry_id:270863)能够成立的根本代数保证。

### 基本[上同调群](@entry_id:142450)：诠释与计算

[上同调群](@entry_id:142450)的定义虽然抽象，但在低阶时具有非常直观的几何和拓扑意义。

#### 零阶[上同调群](@entry_id:142450) $H^0(X; G)$

我们从最简单的零阶[上同调群](@entry_id:142450) $H^0(X; G)$ 开始。根据定义，$H^0(X; G) = \ker(\delta^0) / \text{im}(\delta^{-1})$。按照约定，$C^{-1}(X; G)=0$，所以 $\text{im}(\delta^{-1}) = 0$，因此 $H^0(X; G) \cong \ker(\delta^0)$。

一个 0-上链 $\phi \in C^0(X; G)$ 是一个从 0-单纯形（即 $X$ 中的点）到 $G$ 的函数。因此，我们可以将 $\phi$ 视为一个函数 $\phi: X \to G$。

上[边界算子](@entry_id:160216) $\delta^0: C^0(X; G) \to C^1(X; G)$ 作用于一个 1-单纯形 $\sigma: \Delta^1 \to X$ 上，其结果为：
$$ (\delta^0 \phi)(\sigma) = \phi(\partial_1 \sigma) = \phi(\sigma(v_1)) - \phi(\sigma(v_0)) $$
其中 $v_1$ 和 $v_0$ 是 $\Delta^1$ 的两个端点。因此，$\phi$ 是一个 **0-上循环 (0-cocycle)**（即 $\phi \in \ker(\delta^0)$）当且仅当对于任意连接点 $x_0$ 和 $x_1$ 的路径（可以视为 1-单纯形），都有 $\phi(x_1) - \phi(x_0) = 0$，即 $\phi(x_1) = \phi(x_0)$。

[@problem_id:1640928] 这意味着，一个 0-上循环在 $X$ 的每个[路径连通分支](@entry_id:275432)上都必须是一个常值函数。如果 $X$ 本身是[路径连通](@entry_id:148704)的，那么任何一个 0-上循环在整个空间 $X$上都是常数。这样的常值函数由其在 $G$ 中的唯一值确定。因此，0-上循环的群 $\ker(\delta^0)$ 与系数群 $G$ 同构。所以，对于一个非空、路径连通的空间 $X$，我们有：
$$ H^0(X; G) \cong G $$

如果 $X$ 不是路径连通的，而是由一系列[路径连通分支](@entry_id:275432) $X_i$ 构成，$X = \bigsqcup_i X_i$，那么一个 0-上循环就是在每个分支 $X_i$ 上取一个常数值 $g_i \in G$。因此，0-上循环的[群同构](@entry_id:147371)于各个系数[群的直积](@entry_id:143585)（对于有限个分支，直积与[直和](@entry_id:156782)相同）。例如，[@problem_id:1640936] 考虑一个由 $n$ 个离散点构成的空间 $X = \{p_1, \ldots, p_n\}$。每个点都是一个[路径连通分支](@entry_id:275432)。因此，
$$ H^0(X; G) \cong \bigoplus_{i=1}^n H^0(\{p_i\}; G) \cong \bigoplus_{i=1}^n G $$
对于 $k \ge 1$，一个点的 $k$-维同调群为零，因此其 $k$-维上同调群也为零。于是对于这 $n$ 个点的空间，$H^k(X; G) = 0$ 对所有 $k \ge 1$ 成立。

#### 一阶上同调群的几何直观

一阶[上同调群](@entry_id:142450) $H^1(X; G)$ 捕捉了空间中“环路”的某种对偶信息。我们可以通过单纯复形来获得更具体的几何图像。[@problem_id:1640944] 考虑一个三角剖分后的圆 $S^1$，由四个顶点 $\{v_0, v_1, v_2, v_3\}$ 和四条有向边 $\{e_0, e_1, e_2, e_3\}$ 构成一个闭环。一个实系数的 1-上链 $\phi$ 就是给每条边 $e_i$ 赋予一个实数值 $\phi(e_i)$。

一个 1-上链 $\psi$ 如果是一个 **上边界 (coboundary)**，意味着存在一个 0-上链 $f$（即在每个顶点上的赋值 $f(v_i) \in \mathbb{R}$），使得 $\psi = \delta f$。具体来说，在边 $e_i = [v_i, v_{i+1}]$ 上，$(\delta f)(e_i) = f(v_{i+1}) - f(v_i)$。这可以看作是某种形式的“梯度”。

一个 1-上链 $\phi$ 是一个 **上循环 (cocycle)**，如果 $\delta \phi = 0$。对于这个圆的剖分，唯一的 2-单纯形不存在，所以所有 1-上链都是上循环。$H^1(S^1; \mathbb{R})$ 描述了那些不是上边界的上循环。

在给定的例子 [@problem_id:1640944] 中，一个 1-上链 $\phi$ 可以被分解为一个上边界部分 $\delta f$ 和一个“调和”部分 $\alpha$。调和部分 $\alpha$ 的特征是在构成基本环路的所有边上取相同的值 $c$。这个常数 $c$ 捕捉了上链 $\phi$ 无法被“梯度” $\delta f$ 解释的部分。为了找到这个值，我们可以对 $\phi(e_i) = f(v_{i+1}) - f(v_i) + c$ 这四个方程求和。左边是 $\sum_i \phi(e_i)$，右边的 $f$ 项会形成伸缩和而抵消（$\sum (f(v_{i+1}) - f(v_i)) = 0$），剩下 $4c$。因此，
$$ c = \frac{1}{4} \sum_{i=0}^3 \phi(e_i) $$
这个值 $c$ 正是上同调类 $[\phi] \in H^1(S^1; \mathbb{R})$ 的一种表示。它衡量了当沿着整个[环路积分](@entry_id:164828)时 $\phi$ 值的“净增量”，这部分增量无法通过调整顶点处的“势能” $f(v_i)$ 来消除。

### 泛系数定理：连接同调与上同调

[上同调群](@entry_id:142450) $H^n(X; G)$ 与同调群 $H_n(X; \mathbb{Z})$ 之间存在着深刻的联系，这一联系由 **泛系数定理 (Universal Coefficient Theorem, UCT)** 精确描述。该定理指出，对于任意[拓扑空间](@entry_id:155056) $X$ 和任意[阿贝尔系数](@entry_id:269558)群 $G$，存在一个对每个 $n \ge 0$ 都成立的短[正合序列](@entry_id:151503)：
$$ 0 \to \text{Ext}(H_{n-1}(X; \mathbb{Z}), G) \to H^n(X; G) \to \text{Hom}(H_n(X; \mathbb{Z}), G) \to 0 $$
而且这个序列是分裂的，这意味着[上同调群](@entry_id:142450)可以表示为两部分的[直和](@entry_id:156782)：
$$ H^n(X; G) \cong \text{Ext}(H_{n-1}(X; \mathbb{Z}), G) \oplus \text{Hom}(H_n(X; \mathbb{Z}), G) $$
这里的 $\text{Hom}(A, B)$ 是从群 $A$ 到 $B$ 的所有同态构成的群，而 $\text{Ext}(A, B)$ 是一个来自同调代数的函子，称为 **Ext [函子](@entry_id:150427)**。直观上，$\text{Hom}(H_n(X; \mathbb{Z}), G)$ 部分代表了 $H^n$ 中由 $H_n$ 的“自由部分”贡献的部分，而 $\text{Ext}(H_{n-1}(X; \mathbb{Z}), G)$ 部分则捕捉了由 $H_{n-1}$ 的“挠部分”（即有限阶元素）引起的效应。

#### 整数系数的情形

当系数群 $G = \mathbb{Z}$ 时，UCT 提供了一个计算整数[上同调](@entry_id:160558)的强大工具。我们需要一些基本的 Ext 和 Hom 群的性质：
*   $\text{Hom}(\mathbb{Z}, \mathbb{Z}) \cong \mathbb{Z}$
*   $\text{Hom}(\mathbb{Z}_m, \mathbb{Z}) = 0$ (因为 $\mathbb{Z}$ 中没有非零的[挠元](@entry_id:148301))
*   $\text{Ext}(\mathbb{Z}, \mathbb{Z}) = 0$
*   $\text{Ext}(\mathbb{Z}_m, \mathbb{Z}) \cong \mathbb{Z}_m$

让我们以[实射影平面](@entry_id:150364) $\mathbb{R}P^2$ 为例 [@problem_id:1640963]。已知其整系数同调群为：
$H_0(\mathbb{R}P^2; \mathbb{Z}) \cong \mathbb{Z}$, $H_1(\mathbb{R}P^2; \mathbb{Z}) \cong \mathbb{Z}_2$, $H_n(\mathbb{R}P^2; \mathbb{Z}) = 0$ for $n \ge 2$.

利用 UCT 计算其整系数[上同调群](@entry_id:142450) $H^n(\mathbb{R}P^2; \mathbb{Z})$：
*   **n = 0**: $H^0(\mathbb{R}P^2; \mathbb{Z}) \cong \text{Ext}(H_{-1}, \mathbb{Z}) \oplus \text{Hom}(H_0, \mathbb{Z}) \cong 0 \oplus \text{Hom}(\mathbb{Z}, \mathbb{Z}) \cong \mathbb{Z}$.
*   **n = 1**: $H^1(\mathbb{R}P^2; \mathbb{Z}) \cong \text{Ext}(H_0, \mathbb{Z}) \oplus \text{Hom}(H_1, \mathbb{Z}) \cong \text{Ext}(\mathbb{Z}, \mathbb{Z}) \oplus \text{Hom}(\mathbb{Z}_2, \mathbb{Z}) \cong 0 \oplus 0 = 0$.
*   **n = 2**: $H^2(\mathbb{R}P^2; \mathbb{Z}) \cong \text{Ext}(H_1, \mathbb{Z}) \oplus \text{Hom}(H_2, \mathbb{Z}) \cong \text{Ext}(\mathbb{Z}_2, \mathbb{Z}) \oplus \text{Hom}(0, \mathbb{Z}) \cong \mathbb{Z}_2 \oplus 0 \cong \mathbb{Z}_2$.
*   **n > 2**: $H_n$ 和 $H_{n-1}$ 均为零，因此 $H^n$ 也为零。

我们看到，$H_1$ 中的挠部分 $\mathbb{Z}_2$ “转移”到了 $H^2$ 中，这是 UCT 的一个典型体现。

#### 域系数的情形

当系数群 $G$ 是一个 **[可除群](@entry_id:154489) (divisible group)** 时（例如，任何域，如 $\mathbb{Q}, \mathbb{R}, \mathbb{C}$），UCT 的形式会极大简化。一个关键的代数事实是，如果 $G$ 是可除的，那么对于任何阿贝尔群 $A$，$\text{Ext}(A, G) = 0$。
在这种情况下，UCT 中的短[正合序列](@entry_id:151503)退化为：
$$ H^n(X; G) \cong \text{Hom}(H_n(X; \mathbb{Z}), G) $$

这告诉我们，当系数是一个域（比如有理数 $\mathbb{Q}$）时，上同调群就是同调群的[对偶向量空间](@entry_id:193439)。

考虑计算 $H^k(X; \mathbb{Q})$ [@problem_id:1640937]。首先，我们将整系数同调[群分解](@entry_id:146162)为自由部分和挠部分：$H_k(X; \mathbb{Z}) \cong \mathbb{Z}^{r_k} \oplus T_k$，其中 $r_k$ 是 $k$ 阶[贝蒂数](@entry_id:153109) (Betti number)，$T_k$ 是[挠子群](@entry_id:139454)。
$$ H^k(X; \mathbb{Q}) \cong \text{Hom}(\mathbb{Z}^{r_k} \oplus T_k, \mathbb{Q}) \cong \text{Hom}(\mathbb{Z}^{r_k}, \mathbb{Q}) \oplus \text{Hom}(T_k, \mathbb{Q}) $$
由于 $\mathbb{Q}$ 中没有非零的[挠元](@entry_id:148301)，任何从一个[挠群](@entry_id:144787) $T_k$ 到 $\mathbb{Q}$ 的同态都必然是零同态，即 $\text{Hom}(T_k, \mathbb{Q}) = 0$。而 $\text{Hom}(\mathbb{Z}^{r_k}, \mathbb{Q}) \cong \mathbb{Q}^{r_k}$。因此，
$$ H^k(X; \mathbb{Q}) \cong \mathbb{Q}^{r_k} $$
这意味着 $k$ 阶有理[上同调群](@entry_id:142450)的维数等于 $k$ 阶整系数同调群的秩（即 $k$ 阶[贝蒂数](@entry_id:153109)）。换言之，**有理上同调“无视”同调群中的所有挠信息**。

例如，对于一个同调群为 $H_2(X; \mathbb{Z}) \cong \mathbb{Z}^3 \oplus \mathbb{Z}_2 \oplus \mathbb{Z}_4$ 的空间，其秩为 $r_2=3$，因此其二阶有理上同调群的维数为 $d_2 = \dim_{\mathbb{Q}} H^2(X; \mathbb{Q}) = 3$ [@problem_id:1640937]。这个原理在结合其他工具（如 Künneth 定理）时也同样适用。例如在计算 $H^3(\mathbb{R}P^2 \times \mathbb{R}P^3; \mathbb{Q})$ 时 [@problem_id:1640948]，我们首先计算出 $H^k(\mathbb{R}P^2; \mathbb{Q})$ 和 $H^k(\mathbb{R}P^3; \mathbb{Q})$ 的维数，然后利用 Künneth 定理（在域系数下形式最简单）将它们组合起来。

### [函子性](@entry_id:150069)与对偶性

上同调群和[诱导同态](@entry_id:266478)构成了从[拓扑空间](@entry_id:155056)范畴到[阿贝尔群](@entry_id:150284)范畴的一个 **[逆变函子](@entry_id:155027) (contravariant functor)**。这意味着一个连续映射 $f: X \to Y$ 不仅诱导了同调群之间的[前推](@entry_id:158718)同态 $f_*: H_n(X) \to H_n(Y)$，还诱导了[上同调群](@entry_id:142450)之间的 **[拉回](@entry_id:160816)同态 (pullback homomorphism)** $f^*: H^n(Y; G) \to H^n(X; G)$。注意箭头的方向是反转的。

#### [诱导同态](@entry_id:266478)的同构

UCT 的自然性保证了同调与上同调之间的紧密联系也体现在[诱导同态](@entry_id:266478)上。一个非常强大的结论是：如果一个[连续映射](@entry_id:153855) $f: X \to Y$ 诱导了所有阶数上整系数同调群的同构，即 $f_*: H_n(X; \mathbb{Z}) \xrightarrow{\cong} H_n(Y; \mathbb{Z})$ 对所有 $n$ 成立，那么它也诱导了以 *任何* [阿贝尔群](@entry_id:150284) $G$ 为系数的上同调群的同构 $f^*: H^n(Y; G) \xrightarrow{\cong} H^n(X; G)$ [@problem_id:1640945]。

这个结论的证明优雅地运用了 **[五引理](@entry_id:263766) (Five Lemma)**。由于 $f_*$ 是同构，它所诱导的 $\text{Hom}$ 和 $\text{Ext}$ 函子层面的映射也都是同构。将这些同构映射置于 UCT 导出的[交换图](@entry_id:747516)表中：
$$
\begin{array}{ccccccc}
\text{Ext}(H_{n-1}(Y), G)  \to  H^{n}(Y; G)  \to  \text{Hom}(H_{n}(Y), G) \\
\downarrow \cong   \downarrow f^{*}   \downarrow \cong \\
\text{Ext}(H_{n-1}(X), G)  \to  H^{n}(X; G)  \to  \text{Hom}(H_{n}(X), G)
\end{array}
$$
由于左右两边的纵向箭头都是同构，根据[五引理](@entry_id:263766)，中间的箭头 $f^*$ 也必须是同构。这个结论（有时被称为上同调的 Whitehead 定理）非常有用，因为它允许我们从关于最基本的 $\mathbb{Z}$ 系数同调的信息，推断出关于所有其他系数[上同调](@entry_id:160558)的行为。

#### Kronecker 配对

[上同调](@entry_id:160558)与同调之间的对偶性可以通过 **Kronecker 配对 (Kronecker pairing)** 来具体化。这是一个[双线性映射](@entry_id:186502)：
$$ \langle \cdot, \cdot \rangle: H^n(X; G) \times H_n(X; \mathbb{Z}) \to G $$
定义为 $\langle [\phi], [c] \rangle = \phi(c)$，其中 $\phi$ 是一个 $n$-上循环， $c$ 是一个 $n$-循环。这个配对是良定义的，因为如果 $\phi$ 是一个上边界 $\delta\psi$，或者 $c$ 是一个边界 $\partial d$，其值为零。

这个配对的一个重要性质是其 **自然性**。对于一个[连续映射](@entry_id:153855) $f: X \to Y$，以下关系成立：
$$ \langle f^*(\omega), c \rangle = \langle \omega, f_*(c) \rangle $$
其中 $\omega \in H^n(Y; G)$，$c \in H_n(X; \mathbb{Z})$。这表明[拉回](@entry_id:160816) $f^*$ 是[前推](@entry_id:158718) $f_*$ 在配对下的 **伴随映射 (adjoint map)**。

[@problem_id:1640953] 我们可以利用这个性质进行具体的计算。例如，设 $i: A \hookrightarrow X$ 是一个[子空间](@entry_id:150286)的包含映射。我们想知道 $X$ 中的一个上同调类 $\omega \in H^n(X; G)$ 被限制到[子空间](@entry_id:150286) $A$ 上是什么，即计算 $i^*(\omega) \in H^n(A; G)$。根据自然性，我们只需知道 $A$ 中的同调类在 $X$ 中的像 $i_*(c)$ 是什么即可。如果 $\omega = c_1 \alpha^* + c_2 \beta^*$ 是环面 $T^2$ 上的一个 1-[上同调类](@entry_id:263961)，而 $A$ 是环面上一个由同调类 $p[\alpha] + q[\beta]$ 代表的圈，那么 $\omega$ 限制在 $A$ 上的类 $i^*(\omega) = k\gamma^*$ (其中 $\gamma^*$ 是 $A$ 上 $H^1$ 的基) 的系数 $k$ 可以通过配对计算：
$$ k = \langle k\gamma^*, [\gamma] \rangle = \langle i^*(\omega), [\gamma] \rangle = \langle \omega, i_*([\gamma]) \rangle = \langle c_1 \alpha^* + c_2 \beta^*, p[\alpha] + q[\beta] \rangle = c_1 p + c_2 q $$
这个结果清晰地展示了同调与上同调之间深刻的对偶结构。

### 系数[长正合序列](@entry_id:153438)

[上同调理论](@entry_id:270863)的另一个强大工具来自于系数群的 **[长正合序列](@entry_id:153438) (long exact sequence)**。任何一个关于系数群的短[正合序列](@entry_id:151503)
$$ 0 \to A \xrightarrow{\alpha} B \xrightarrow{\beta} C \to 0 $$
都会在任何空间 $X$ 上诱导一个[上同调](@entry_id:160558)的长正合序列：
$$ \cdots \to H^n(X; A) \xrightarrow{\alpha_*} H^n(X; B) \xrightarrow{\beta_*} H^n(X; C) \xrightarrow{\delta} H^{n+1}(X; A) \to \cdots $$
其中 $\alpha_*$ 和 $\beta_*$ 是由系数映射诱导的显然映射，而 **[连接同态](@entry_id:160713) (connecting homomorphism)** $\delta$ 是一个新出现的、非平凡的映射，它将阶数提升了 1。这个映射 $\delta$ 通常被称为 **Bockstein 同态**。

一个经典的应用源于短[正合序列](@entry_id:151503) $0 \to \mathbb{Z} \xrightarrow{\cdot p} \mathbb{Z} \to \mathbb{Z}_p \to 0$，其中 $p$ 是一个整数（通常是素数）。这条序列将整系数[上同调](@entry_id:160558)与模 $p$ 上同调联系起来。

[@problem_id:1661653] 让我们再次以 $\mathbb{R}P^2$ 为例，并考虑 $p=2$ 的情形。短[正合序列](@entry_id:151503)是：
$$ 0 \to \mathbb{Z} \xrightarrow{\cdot 2} \mathbb{Z} \xrightarrow{\pi} \mathbb{Z}_2 \to 0 $$
它诱导的长正合序列中包含这样一段：
$$ \cdots \to H^1(X; \mathbb{Z}) \xrightarrow{(\cdot 2)_*} H^1(X; \mathbb{Z}) \xrightarrow{\pi_*} H^1(X; \mathbb{Z}_2) \xrightarrow{\delta} H^2(X; \mathbb{Z}) \to \cdots $$
我们已知 $H^1(\mathbb{R}P^2; \mathbb{Z}) = 0$ 且 $H^1(\mathbb{R}P^2; \mathbb{Z}_2) \cong \mathbb{Z}_2$。将这些信息代入序列，得到：
$$ \cdots \to 0 \xrightarrow{\pi_*} H^1(\mathbb{R}P^2; \mathbb{Z}_2) \xrightarrow{\delta} H^2(\mathbb{R}P^2; \mathbb{Z}) \to \cdots $$
根据[正合序列](@entry_id:151503)的定义，在 $H^1(X; \mathbb{Z}_2)$ 处，$\ker(\delta) = \text{im}(\pi_*)$。由于 $\pi_*$ 的定义域是零群，它的像也是零，因此 $\ker(\delta) = 0$。这说明 Bockstein 同态 $\delta: H^1(\mathbb{R}P^2; \mathbb{Z}_2) \to H^2(\mathbb{R}P^2; \mathbb{Z})$ 是一个单射。

由于 $H^1(\mathbb{R}P^2; \mathbb{Z}_2) \cong \mathbb{Z}_2$ 且 $H^2(\mathbb{R}P^2; \mathbb{Z}) \cong \mathbb{Z}_2$，一个从 $\mathbb{Z}_2$到 $\mathbb{Z}_2$的单射必然是同构。因此，Bockstein 同态 $\delta$ 将 $H^1(\mathbb{R}P^2; \mathbb{Z}_2)$ 中的非零元映为 $H^2(\mathbb{R}P^2; \mathbb{Z})$ 中的非零元。

这个例子完美地展示了[长正合序列](@entry_id:153438)如何揭示不同系数上同调群之间的代数关系，Bockstein 同态在其中扮演了关键的桥梁角色。通过操纵这些代数工具，我们可以从已知的信息中推导出新的、非平凡的拓扑结论。