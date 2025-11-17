## 引言
[庞加莱对偶定理](@entry_id:274166)是[代数拓扑学](@entry_id:138192)领域的一块核心基石，它以惊人的方式揭示了[流形](@entry_id:153038)（一类表现良好的拓扑空间）的两种基本代数[不变量](@entry_id:148850)——同调群与[上同调群](@entry_id:142450)——之间的深刻对偶关系。这一定理不仅是理论上的优美成果，更是理解[流形](@entry_id:153038)内在几何与拓扑结构的强大工具，它告诉我们，一个空间的低维“洞”的结构信息，竟能完美地反映在其高维“洞”的结构之中。

然而，在初次接触同调与上同调时，人们往往将它们视为各自独立的代数序列，它们之间的内在联系并不显而易见。本文旨在填补这一认知上的沟壑，系统性地阐明[庞加莱对偶定理](@entry_id:274166)是如何精确地刻画这种联系的。读者将通过本文学习到这一定理从基本原理到前沿应用的完整图景。

文章将分为三个部分展开。首先，在“原理和机制”一章中，我们将深入探讨定理的构造基础，从定义[可定向性](@entry_id:149777)与关键的“[基本类](@entry_id:158335)”开始，到阐释实现对偶的“[杯积](@entry_id:159554)”运算，并讨论定理在不同[流形](@entry_id:153038)（如不可定向或[带边流形](@entry_id:159788)）上的变体。接下来，在“应用与跨学科联系”一章中，我们将展示该定理的强大威力，看它如何约束[流形的拓扑](@entry_id:267834)[不变量](@entry_id:148850)（如[贝蒂数](@entry_id:153109)）、如何通过[相交理论](@entry_id:157884)提供几何直观，以及它如何在[微分几何](@entry_id:145818)、[代数几何](@entry_id:156300)乃至理论物理中扮演关键角色。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者将理论知识应用于具体计算，从而真正内化所学内容。

让我们首先进入定理的核心，探索其精妙的原理与机制。

## 原理和机制

[庞加莱对偶定理](@entry_id:274166)是[代数拓扑学](@entry_id:138192)的基石之一，它深刻地揭示了特定空间（即[流形](@entry_id:153038)）的同调群与上同调群之间的内在联系。本章旨在系统地阐述该定理的核心原理、关键机制及其在几何与拓扑研究中的深远影响。我们将从构建定理的基础——[基本类](@entry_id:158335)——开始，逐步揭示对偶同构的运作方式，并探讨其在可定向与不可定[流形](@entry_id:153038)以及[带边流形](@entry_id:159788)等不同情境下的表现形式。

### [基本类](@entry_id:158335)：从局部到整体

[庞加莱对偶定理](@entry_id:274166)的出发点是**[可定向性](@entry_id:149777)**的概念以及与之密切相关的**[基本类](@entry_id:158335) (fundamental class)**。为了理解这一点，我们首先需要考察[流形](@entry_id:153038)的局部拓扑结构。

对于一个 $n$ 维[流形](@entry_id:153038) $M$，其在任意一点 $x \in M$ 的**[局部定向](@entry_id:264384) (local orientation)** 被定义为[相对同调群](@entry_id:159711) $H_n(M, M \setminus \{x\})$ 的一个生成元。这个[群同构](@entry_id:147371)于整数群 $\mathbb{Z}$，因此在每个点我们都有两个选择，分别对应于 $+1$ 和 $-1$。一个全局的**定向 (orientation)** 是为[流形](@entry_id:153038)上每一点选择一个[局部定向](@entry_id:264384) $\mu_x \in H_n(M, M \setminus \{x\})$，并且这种选择是*连续的*或*一致的*。具体来说，对于每一点 $x$，都存在一个包含 $x$ 的[闭球](@entry_id:157850) $B \subset M$，以及 $H_n(M, M \setminus B)$ 的一个生成元 $\mu_B$，使得对于任意 $y \in B$，$\mu_y$ 都是 $\mu_B$ 在自然包含映射 $H_n(M, M \setminus B) \to H_n(M, M \setminus \{y\})$ 下的像。

有了这样一组一致的[局部定向](@entry_id:264384) $\{\mu_x\}_{x \in M}$，我们的目标是构造一个定义在整个[流形](@entry_id:153038)上的单一、全局的同调类，即**基本类** $[M] \in H_n(M)$。这个全局[基本类](@entry_id:158335)与[局部定向](@entry_id:264384)之间的关系是其核心定义：基本类 $[M]$ 是绝对同调群 $H_n(M)$ 中唯一的元素，其在对于每个点 $x \in M$ 的自然映射 $j_x: H_n(M) \to H_n(M, M \setminus \{x\})$ 下的像恰好是该点的[局部定向](@entry_id:264384) $\mu_x$。也就是说，对于所有 $x \in M$，都有 $j_x([M]) = \mu_x$。[@problem_id:1688559]

这个全局类的存在性依赖于[流形](@entry_id:153038)的紧致性，紧致性保证了我们可以用有限个“定向一致”的开集或[闭球](@entry_id:157850)覆盖整个[流形](@entry_id:153038)，并通过[迈耶-维托里斯序列](@entry_id:161286) (Mayer-Vietoris sequence) 等工具将这些局部的定向“黏合”成一个全局的 $n$-循环。而其唯一性则源于对偶 $(M, M \setminus \{x\})$ 的长正合序列，该序列表明映射 $j_x$ 是[单射](@entry_id:183792)。

那么，对于**不可定向 (non-orientable)** [流形](@entry_id:153038)，情况又如何呢？[不可定向性](@entry_id:155097)的本质在于无法在整个[流形](@entry_id:153038)上做出一致的[局部定向](@entry_id:264384)选择。任何尝试沿着[流形](@entry_id:153038)中的某条闭合路径（一个“方向反转环”）连续地传递[局部定向](@entry_id:264384)，最终都会导致回到起点时定向发生反转。这一拓扑特性直接导致了其顶维整系数同调群的结构。考虑一个闭合、连通的不可定向 $n$-[流形](@entry_id:153038) $M$ 上的任意一个整系数 $n$-循环 $c = \sum k_i \tau_i$，其中 $\tau_i$ 是构成[流形](@entry_id:153038)[三角剖分](@entry_id:272253)的 $n$-单形。循环条件 $\partial c = 0$ 要求在任意两个相邻单形 $\tau_i$ 和 $\tau_j$ 的公共 $(n-1)$-面上，它们的系数必须满足特定关系，即 $k_j = \pm k_i$。当沿着一个方向反转环传播这个系数关系时，我们会得到 $k_i = -k_i$，这在整数环 $\mathbb{Z}$ 中意味着 $k_i = 0$。由于[流形](@entry_id:153038)是连通的，这个结论会传递到所有系数上，迫使所有 $k_i$ 都为零。因此，对于一个闭合的[不可定向流形](@entry_id:160551) $M$，其唯一的整系数 $n$-循环是零循环，这导致其顶维[整同调](@entry_id:276347)群为平凡群，即 $H_n(M; \mathbb{Z}) = \{0\}$。[@problem_id:1688558] 这一结论从根本上说明了为何标准形式的[庞加莱对偶定理](@entry_id:274166)要求[流形](@entry_id:153038)是可定向的——因为在不可定向的情况下，对偶关系中至关重要的基本类 $[M] \in H_n(M; \mathbb{Z})$ 根本不存在（为零）。

### [庞加莱对偶](@entry_id:161676)同构

有了[基本类](@entry_id:158335)的概念，我们就可以陈述[庞加莱对偶定理](@entry_id:274166)的核心内容。

**定理 ([庞加莱对偶](@entry_id:161676))**：令 $M$ 为一个闭合、可定向的 $n$ 维[流形](@entry_id:153038)。对于任意系数群 $G$ 和任意整数 $0 \le k \le n$，**杯积 (cap product)** 运算诱导出一个同构：
$$
D: H^k(M; G) \stackrel{\cong}{\longrightarrow} H_{n-k}(M; G)
$$
该同构由 $D(\alpha) = [M] \cap \alpha$ 定义，其中 $[M] \in H_n(M; G)$ 是 $M$ 的基本类。

这个定理揭示了[流形](@entry_id:153038)的 $k$ 维[上同调群](@entry_id:142450)与 $(n-k)$ 维同调群之间存在着一种深刻的对偶关系。此处的关键是**杯积**运算，记作 $\cap$，它是一个[双线性映射](@entry_id:186502) $\cap: H_p(M; G) \times H^q(M; G) \to H_{p-q}(M; G)$。直观上，可以将其理解为在一个 $p$ 维链上“作用”一个 $q$ 维上链，通过在链的前 $q$ 个单形上求值，得到一个 $(p-q)$ 维的链。

对偶同构的一个基本且极具启发性的例子发生在 $k=0$ 时。对于一个连通[流形](@entry_id:153038) $M$，其零次上同调群 $H^0(M; \mathbb{Z}) \cong \mathbb{Z}$ 由[上同调环](@entry_id:160158)的乘法单位元 $1$ 生成。根据对偶同构的定义，这个单位元 $1$ 的对偶是什么呢？
$$
D(1) = [M] \cap 1
$$
杯积的一个基本性质是，与零次上同调单位元 $1$ 作[杯积](@entry_id:159554)不改变同调类。因此，我们有 $[M] \cap 1 = [M]$。这表明，[庞加莱对偶](@entry_id:161676)将[上同调](@entry_id:160558)中的乘法单位元映为同调中的基本类。[@problem_id:1688568] 这个优美的关系为整个[对偶理论](@entry_id:143133)提供了一个坚实的起点。

为了更具体地理解对偶同构的运作机制，让我们考察一个实例：[二维环面](@entry_id:265991) $M = T^2$。设其[第一同调群](@entry_id:145318) $H_1(T^2; \mathbb{R})$ 的基为 $[a], [b]$，分别代表环面的两个基本循环。其对偶基为 $H^1(T^2; \mathbb{R})$ 的基 $\alpha, \beta$，满足[克罗内克积](@entry_id:182766)关系 $\langle \alpha, [a] \rangle = 1, \langle \alpha, [b] \rangle = 0$ 等。[庞加莱对偶](@entry_id:161676)同构 $D: H^1(T^2; \mathbb{R}) \to H_1(T^2; \mathbb{R})$ 由 $D(\eta) = [T^2] \cap \eta$ 给出。为了计算一个具体的上同调类 $\gamma = 3\alpha - 5\beta$ 的对偶，我们可以利用一个至关重要的恒等式，它将杯积 (cup product) $\cup$、嘉积 (cap product) $\cap$ 和克罗内克积 (Kronecker pairing) $\langle \cdot, \cdot \rangle$ 联系在一起：
$$
\langle \zeta, [M] \cap \eta \rangle = \langle \zeta \cup \eta, [M] \rangle
$$
对于适当维数的同调类与[上同调类](@entry_id:263961)。设 $D(\gamma) = x[a] + y[b]$。我们可以通过与对偶基 $\alpha, \beta$ 配对来求解系数 $x, y$：
$$
x = \langle \alpha, D(\gamma) \rangle = \langle \alpha, [T^2] \cap \gamma \rangle = \langle \alpha \cup \gamma, [T^2] \rangle
$$
$$
y = \langle \beta, D(\gamma) \rangle = \langle \beta, [T^2] \cap \gamma \rangle = \langle \beta \cup \gamma, [T^2] \rangle
$$
利用[上同调环](@entry_id:160158)的[乘法规则](@entry_id:197368)（例如 $\alpha \cup \beta = - \beta \cup \alpha = \omega$，其中 $\omega$ 是 $H^2(T^2)$ 的生成元且 $\langle \omega, [T^2] \rangle = 1$），以及 $\gamma = 3\alpha - 5\beta$，我们可以计算出杯积：
$$
\alpha \cup \gamma = \alpha \cup (3\alpha - 5\beta) = 3(\alpha \cup \alpha) - 5(\alpha \cup \beta) = -5\omega
$$
$$
\beta \cup \gamma = \beta \cup (3\alpha - 5\beta) = 3(\beta \cup \alpha) - 5(\beta \cup \beta) = 3(-\omega) = -3\omega
$$
代入后得到 $x = \langle -5\omega, [T^2] \rangle = -5$ 和 $y = \langle -3\omega, [T^2] \rangle = -3$。因此，$\gamma = 3\alpha - 5\beta$ 的[庞加莱对偶](@entry_id:161676)是 $-5[a] - 3[b]$。[@problem_id:1688541] 这个计算过程清晰地展示了对偶同构是如何通过[上同调](@entry_id:160558)的[代数结构](@entry_id:137052)（[杯积](@entry_id:159554)）来确定的。

### 推论与解释

[庞加莱对偶](@entry_id:161676)不仅仅是一个抽象的同构，它带来了一系列深刻的几何与拓扑推论。

#### 贝蒂数的对称性与[欧拉示性数](@entry_id:152513)

当使用域（如 $\mathbb{Q}$ 或 $\mathbb{R}$）作为系数时，同调群与[上同调群](@entry_id:142450)都是[向量空间](@entry_id:151108)，它们的维数被称为**贝蒂数 (Betti numbers)**，$b_k(M) = \dim H_k(M; \mathbb{Q})$。根据[庞加莱对偶](@entry_id:161676)，$H_k(M)$ 与 $H_{n-k}(M)$ 同构，因此它们的维数必须相等。这意味着贝蒂数序列具有对称性：
$$
b_k(M) = b_{n-k}(M)
$$
这个简单的对称关系具有强大的预测能力。例如，考虑一个 6 维的闭合、连通、[可定向流形](@entry_id:276936) $M$，已知其贝蒂数为 $b_1(M)=2$, $b_2(M)=7$, $b_3(M)=10$。利用[贝蒂数](@entry_id:153109)的对称性，我们可以立即推断出其他的[贝蒂数](@entry_id:153109)：$b_0(M) = b_6(M) = 1$ (因为[流形](@entry_id:153038)连通)，$b_5(M) = b_1(M) = 2$，以及 $b_4(M) = b_2(M) = 7$。有了完整的贝蒂数序列，我们便可以计算[流形](@entry_id:153038)的**[欧拉示性数](@entry_id:152513) (Euler characteristic)** $\chi(M)$：
$$
\chi(M) = \sum_{k=0}^{6} (-1)^k b_k(M) = 1 - 2 + 7 - 10 + 7 - 2 + 1 = 2
$$
[@problem_id:1688575] 如果[流形](@entry_id:153038)的维数 $n$ 是奇数，贝蒂数的对称性 $\chi(M) = \sum (-1)^k b_k$ 会导致[欧拉示性数](@entry_id:152513)为零。

#### 对偶作为非退化配对

[庞加莱对偶](@entry_id:161676)的另一种重要表述形式是**非退化[双线性](@entry_id:146819)配对 (non-degenerate bilinear pairing)**。对于一个闭合可定向 $n$-[流形](@entry_id:153038)，在域系数下，我们可以定义一个配对：
$$
B: H^k(M) \times H^{n-k}(M) \to \mathbb{R}
$$
$$
B(\alpha, \beta) = \langle \alpha \cup \beta, [M] \rangle
$$
这里 $\langle \cdot, \cdot \rangle$ 可以理解为顶阶上同调类在[基本类](@entry_id:158335)上的求值（或“积分”）。[庞加莱对偶定理](@entry_id:274166)等价于声明这个配对是**非退化的**，即对于任意非零的 $\alpha \in H^k(M)$，都存在一个 $\beta \in H^{n-k}(M)$ 使得 $B(\alpha, \beta) \neq 0$。这个非退化配对建立了 $H^k(M)$ 与其对偶空间 $(H^{n-k}(M))^*$ 之间的同构。当 $k=n-k$（即 $k=n/2$）时，这在 $H^{n/2}(M)$ 上定义了一个非退化的[双线性形式](@entry_id:746794)，其性质（对称或反对称）取决于 $n/2$ 的奇偶性，这成为了研究[流形](@entry_id:153038)拓扑的一个重要[不变量](@entry_id:148850)。例如，在[二维环面](@entry_id:265991) $T^2$ 的例子中，$k=1, n=2$，配对 $B: H^1(T^2) \times H^1(T^2) \to \mathbb{R}$ 将 $H^1(T^2)$ 与其对偶空间 $(H^1(T^2))^*$ 等同起来。通过这个配对，我们可以找到 $H^1(T^2)$ 中与对偶基的某个元素（如 $\alpha^*$）相对应的上同调类，计算表明这个类是 $-\beta$。[@problem_id:1688584]

#### 几何解释：[相交理论](@entry_id:157884)

也许[庞加莱对偶](@entry_id:161676)最迷人的方面是它在代数与几何之间建立的桥梁。它将抽象的[上同调类](@entry_id:263961)与具体的几何对象——[子流形](@entry_id:159439)——联系起来。粗略地说，一个 $k$-上同调类的[庞加莱对偶](@entry_id:161676)是一个 $(n-k)$-维的子流形（或更一般的循环）。更进一步，[上同调环](@entry_id:160158)中的**[杯积](@entry_id:159554)**运算在几何上对应于这些对偶子流形的**横截相交 (transverse intersection)**。

具体而言，如果 $\alpha \in H^k(M)$ 和 $\beta \in H^{n-k}(M)$ 的对偶[子流形](@entry_id:159439)分别为 $A$ 和 $B$，那么它们的杯积在[基本类](@entry_id:158335)上的求值 $\langle \alpha \cup \beta, [M] \rangle$ 就等于 $A$ 和 $B$ 的**定向[相交数](@entry_id:161199) (oriented intersection number)**。

让我们再次回到[二维环面](@entry_id:265991) $T^2$ 的例子。设 $\gamma, \delta \in H^1(T^2; \mathbb{Z})$ 是两个上同调类，其[庞加莱对偶](@entry_id:161676)由一维[子流形](@entry_id:159439)（[闭合曲线](@entry_id:264519)） $C$ 和 $D$ 的同调类 $[C]$ 和 $[D]$ 代表。那么 $C$ 和 $D$ 的定向[相交数](@entry_id:161199) $I(C,D)$ 可以通过纯代数的方式计算：
$$
I(C,D) = \langle \gamma \cup \delta, [T^2] \rangle
$$
例如，若 $\gamma = 3\alpha - \beta$ 且 $\delta = 2\alpha + 5\beta$，利用[上同调环](@entry_id:160158)的[乘法规则](@entry_id:197368)，我们计算出 $\gamma \cup \delta = 17 [T^2]^*$，其中 $[T^2]^*$ 是 $H^2(T^2)$ 的生成元。因此，[相交数](@entry_id:161199)就是 $\langle 17 [T^2]^*, [T^2] \rangle = 17$。[@problem_id:1688561] 这一思想是现代几何拓扑的核心，它允许我们将几何问题（如计算曲线的[交点数](@entry_id:161199)）转化为代数问题（计算[上同调环](@entry_id:160158)中的乘积）。

#### 计算应用

除了理论上的深刻性，[庞加莱对偶](@entry_id:161676)也是一个强大的计算工具。它允许我们将一个可能很难计算的同调群的秩，转化为计算另一个可能更容易处理的[上同调群](@entry_id:142450)的秩。例如，要计算[流形](@entry_id:153038) $M = S^2 \times S^2 \times S^2 \times S^2$ 的四阶同调群 $H_4(M; \mathbb{Z})$ 的秩。这是一个 8 维的闭合[可定向流形](@entry_id:276936)。直接计算 $H_4(M)$ 可能很复杂，但利用[庞加莱对偶](@entry_id:161676)，我们知道：
$$
\text{rank}(H_4(M; \mathbb{Z})) = \text{rank}(H^{8-4}(M; \mathbb{Z})) = \text{rank}(H^4(M; \mathbb{Z}))
$$
现在问题转化为计算四阶上同调群的秩。利用适用于[积空间](@entry_id:151693)的 Künneth 公式，我们知道 $M$ 的[上同调环](@entry_id:160158)是四个 $S^2$ [上同调环](@entry_id:160158)的张量积。由于 $H^*(S^2; \mathbb{Z}) \cong \mathbb{Z}[\alpha]/(\alpha^2)$，其中 $\deg(\alpha)=2$，$H^*(M; \mathbb{Z})$ 就由四个二次的生成元 $\alpha_1, \alpha_2, \alpha_3, \alpha_4$ 生成。$H^4(M)$ 的基由形如 $\alpha_i \cup \alpha_j$ ($i  j$) 的元素构成。从四个生成元中选取两个不同者组合，其方式有 $\binom{4}{2} = 6$ 种。因此，$H^4(M; \mathbb{Z})$ 的秩为 6，从而 $H_4(M; \mathbb{Z})$ 的秩也为 6。[@problem_id:1688539]

### 推广与变体

标准的[庞加莱对偶定理](@entry_id:274166)适用于闭合、[可定向流形](@entry_id:276936)。然而，这个强大的思想可以推广到更广泛的情境中。

#### [带边流形](@entry_id:159788)：Lefschetz 对偶

当[流形](@entry_id:153038) $M$ 带有边界 $\partial M$ 时，标准的对偶关系不再成立，但一个修正的版本——**Lefschetz 对偶 (Lefschetz duality)**——依然有效。对于一个紧致、可定向的 $n$ 维[流形](@entry_id:153038) $M$，Lefschetz 对偶建立了绝对群和相对群之间的同构关系。它有两种主要形式：
$$
H_k(M, \partial M; G) \cong H^{n-k}(M; G)
$$
$$
H^k(M, \partial M; G) \cong H_{n-k}(M; G)
$$
这些同构依然由与[基本类](@entry_id:158335) $[M] \in H_n(M, \partial M; G)$ 作杯积或嘉积来诱导。这个基本类现在是一个[相对同调](@entry_id:159348)类。

作为一个应用，考虑实心环体 $M = S^1 \times D^2$。这是一个带边界 $\partial M = S^1 \times S^1$ 的 3 维[紧致可定向流形](@entry_id:157578)。我们想确定其二阶[相对同调群](@entry_id:159711) $H_2(M, \partial M; \mathbb{Z})$。根据 Lefschetz 对偶，我们有：
$$
H_2(M, \partial M; \mathbb{Z}) \cong H^{3-2}(M; \mathbb{Z}) = H^1(M; \mathbb{Z})
$$
由于实心环体 $M$ 与圆周 $S^1$ 是同伦等价的，它们的上同调群同构。我们知道 $H^1(S^1; \mathbb{Z}) \cong \mathbb{Z}$，因此 $H^1(M; \mathbb{Z}) \cong \mathbb{Z}$。结论是 $H_2(M, \partial M; \mathbb{Z}) \cong \mathbb{Z}$。[@problem_id:1688595]

#### [不可定向流形](@entry_id:160551)

我们已经看到，对于闭合[不可定向流形](@entry_id:160551) $M$，$H_n(M; \mathbb{Z}) = \{0\}$，因此[标准形式](@entry_id:153058)的[庞加莱对偶](@entry_id:161676)不成立。但是，对偶思想并未完全失效，只是需要调整。

最简单的调整是使用 $\mathbb{Z}_2$ 系数。任何[流形](@entry_id:153038)都是 $\mathbb{Z}_2$-可定向的，即在模 2 意义下可以定义一个基本类。因此，对于任意闭合 $n$-[流形](@entry_id:153038)（无论是否可定向），[庞加莱对偶](@entry_id:161676)在 $\mathbb{Z}_2$ 系数下总是成立的：
$$
H^k(M; \mathbb{Z}_2) \cong H_{n-k}(M; \mathbb{Z}_2)
$$
对于整系数，情况更为复杂。对偶同构的目标群需要被“扭曲”。具体来说，同构 $H^k(M; \mathbb{Z}) \cong H_{n-k}(M; \mathbb{Z}_{\omega_1})$ 成立，其中 $\mathbb{Z}_{\omega_1}$ 是一个**局部系数系统 (local coefficient system)** 或**扭曲系数 (twisted coefficients)**，其扭曲由[定向特征标](@entry_id:262012) $\omega_1: \pi_1(M) \to \{\pm 1\}$ 决定。

虽然扭曲系数的完整理论超出了本章的范围，但我们可以通过考察其推论来理解其影响。例如，对于著名的不可定向[二维流形](@entry_id:188198)——[克莱因瓶](@entry_id:149661) $K$——其同调群为 $H_0 \cong \mathbb{Z}$, $H_1 \cong \mathbb{Z} \oplus \mathbb{Z}_2$, $H_2 = 0$。[不可定向的](@entry_id:150510)[庞加莱对偶](@entry_id:161676)的一个结果是，第一[上同调群](@entry_id:142450) $H^1(K; \mathbb{Z})$ 与[第一同调群](@entry_id:145318)的自由部分 $H_1(K; \mathbb{Z}) / \text{Torsion}(H_1(K; \mathbb{Z}))$ 是同构的。我们可以分别计算这两者。利用泛系数定理，可以得到 $H^1(K; \mathbb{Z}) \cong \text{Hom}(H_1(K; \mathbb{Z}), \mathbb{Z}) \cong \text{Hom}(\mathbb{Z} \oplus \mathbb{Z}_2, \mathbb{Z}) \cong \mathbb{Z}$。另一方面，$H_1$ 的挠部分是 $\mathbb{Z}_2$，因此商群 $H_1(K; \mathbb{Z}) / \text{Torsion}(H_1(K; \mathbb{Z})) \cong (\mathbb{Z} \oplus \mathbb{Z}_2) / \mathbb{Z}_2 \cong \mathbb{Z}$。确实，两者都是 $\mathbb{Z}$，因此它们是同构的。[@problem_id:1688586] 这个例子具体地展示了在不可定向情况下，对偶关系是如何以一种更微妙的形式呈现的。