## 引言
[德拉姆上同调](@entry_id:158673)是连接[微分几何](@entry_id:145818)与代数拓扑的桥梁，它通过微分形式来探究[流形](@entry_id:153038)的深刻[拓扑性质](@entry_id:141605)。然而，直接根据定义计算一个复杂[流形](@entry_id:153038)的上同调群往往是极其困难的。为了解决这一计算难题，数学家们发展了一系列强大的代数工具，其中，迈尔-维托里斯序列（Mayer-Vietoris Sequence）无疑是最为重要和实用的工具之一。它提供了一种“分而治之”的策略，允许我们将整个[流形](@entry_id:153038)上的计算[问题分解](@entry_id:272624)为在更简单的局部区域上的问题，然后通过一个精巧的代数框架将这些局部信息重新“粘合”起来，从而揭示全局的拓扑结构。

本文旨在为读者提供一个关于[德拉姆上同调](@entry_id:158673)中迈尔-维托里斯序列的全面而深入的指南。我们将从其代数根源出发，逐步揭示其工作原理，并通过丰富的实例展示其计算威力。文章分为三个核心部分：在“原理与机制”一章中，我们将深入剖析序列的构造基础，包括微分形式的短[正合序列](@entry_id:151503)、单位分解的应用以及关键的[连接同态](@entry_id:160713)。接着，在“应用与跨学科联系”一章，我们将展示如何利用该序列具体计算球面、环面及其他重要空间的[上同调群](@entry_id:142450)，并探讨其在物理学等领域的联系。最后，“实践练习”部分将提供一系列精心设计的问题，帮助读者巩固理论知识并将其付诸实践。通过本次学习，你将掌握一个分析[流形](@entry_id:153038)拓扑的强大方法论。

## 原理与机制

### 代数基础：[德拉姆复形](@entry_id:178752)的短[正合序列](@entry_id:151503)

迈尔-维托里斯序列是计算[流形](@entry_id:153038)上[德拉姆上同调](@entry_id:158673)群的强大工具，其威力源于一个深刻的[代数结构](@entry_id:137052)。理解这一结构是掌握其应用的关键。其核心思想是将整个[流形](@entry_id:153038)上的微分形式[问题分解](@entry_id:272624)为在两个开[子集](@entry_id:261956)及其交集上的局部问题。

设 $M$ 是一个光滑流形，并被两个开集 $U$ 和 $V$ 覆盖，即 $M = U \cup V$。对于任何光滑流形 $X$，其**[德拉姆复形](@entry_id:178752) (de Rham complex)** 是一个配对 $(\Omega^\bullet(X), d)$，其中 $\Omega^k(X)$ 是 $X$ 上光滑 $k$-[微分形式](@entry_id:146747)构成的[向量空间](@entry_id:151108)，而 $d: \Omega^k(X) \to \Omega^{k+1}(X)$ 是外微分算子。外[微分算子](@entry_id:140145)满足 $d \circ d = 0$（或简记为 $d^2 = 0$）。

一个 $k$-形式 $\omega$ 如果满足 $d\omega = 0$，则被称为**闭形式 (closed form)**。如果存在一个 $(k-1)$-形式 $\eta$ 使得 $\omega = d\eta$，则称 $\omega$ 为**恰当形式 (exact form)**。$d^2=0$ 这个性质直接导出一个重要结论：所有恰当形式都是闭形式。一个[流形](@entry_id:153038)的**$k$阶[德拉姆上同调](@entry_id:158673)群 (de Rham cohomology group)** $H^k_{\mathrm{dR}}(M)$，正是用于衡量“[闭形式](@entry_id:272960)在多大程度上不是恰当形式”的代数[不变量](@entry_id:148850)。其定义为[商空间](@entry_id:274314)：
$$ H^k_{\mathrm{dR}}(M) = \frac{\ker(d: \Omega^k(M) \to \Omega^{k+1}(M))}{\mathrm{im}(d: \Omega^{k-1}(M) \to \Omega^k(M))} = \frac{\text{闭 } k\text{-形式}}{\text{恰当 } k\text{-形式}} $$
因此，一个[闭形式](@entry_id:272960) $\omega$ 在 $H^k_{\mathrm{dR}}(M)$ 中代表的同调类 $[\omega]$ 等于零，当且仅当 $\omega$ 是一个恰当形式。

对于[开覆盖](@entry_id:140020) $M=U \cup V$，我们可以构造一个关联这些空间的[德拉姆复形](@entry_id:178752)的短序列：
$$ 0 \longrightarrow \Omega^\bullet(M) \xrightarrow{r} \Omega^\bullet(U) \oplus \Omega^\bullet(V) \xrightarrow{s} \Omega^\bullet(U \cap V) \longrightarrow 0 $$

让我们来剖析这个序列中的映射及其性质。

- **映射 $r$**：这是一个限制映射，定义为 $r(\omega) = (\omega|_U, \omega|_V)$。它将 $M$ 上的一个形式限制到 $U$ 和 $V$ 上，得到一对形式。这个映射是[单射](@entry_id:183792)（injective），因为如果一个光滑形式在一个[开覆盖](@entry_id:140020)的每个集合上都为零，那么它在整个[流形](@entry_id:153038)上必然为零。

- **映射 $s$**：这是一个差映射，定义为 $s(\alpha, \beta) = \alpha|_{U \cap V} - \beta|_{U \cap V}$。它取 $U$ 上的一个形式 $\alpha$ 和 $V$ 上的一个形式 $\beta$，并将它们在交集 $U \cap V$ 上的差作为结果。

这个序列被称为**短[正合序列](@entry_id:151503) (short exact sequence)**，意味着在每个位置，前一个映射的像集 (image) 都恰好等于后一个映射的核集 (kernel)。
- 在 $\Omega^\bullet(M)$ 处， $r$ 是单射，意味着其核为 $\{0\}$。
- 在 $\Omega^\bullet(U \cap V)$ 处，序列正合意味着 $s$ 是满射 (surjective)。
- 关键在于中间项 $\Omega^\bullet(U) \oplus \Omega^\bullet(V)$ 处的正合性，即 $\ker(s) = \mathrm{im}(r)$。

$\mathrm{im}(r) \subseteq \ker(s)$ 是显而易见的：任何来自全局形式 $\omega$ 的限制对 $(\omega|_U, \omega|_V)$，在交集上作差必然为零。真正深刻的是反向包含关系 $\ker(s) \subseteq \mathrm{im}(r)$，它被称为**微分形式的[粘合引理](@entry_id:151713) (gluing lemma for differential forms)**。它断言，如果 $U$ 上的形式 $\alpha$ 和 $V$ 上的形式 $\beta$ 在交集 $U \cap V$ 上相等（即 $(\alpha, \beta) \in \ker(s)$），那么必然存在一个定义在整个[流形](@entry_id:153038) $M$ 上的全局形式 $\omega$，使得 $\omega$ 限制在 $U$ 上是 $\alpha$，限制在 $V$ 上是 $\beta$。

这个粘合过程并非平凡，它的实现依赖于**[单位分解](@entry_id:150115) (partition of unity)** 的存在。对于一个[光滑流形](@entry_id:160799)（更准确地说，是仿紧致的[光滑流形](@entry_id:160799)，所有豪斯多夫第二可数的[流形](@entry_id:153038)都满足此条件），任何[开覆盖](@entry_id:140020)都存在一个从属于它的光滑[单位分解](@entry_id:150115)。对于覆盖 $\{U, V\}$，这意味着存在[光滑函数](@entry_id:267124) $\rho_U, \rho_V: M \to [0,1]$ 使得：
1. $\mathrm{supp}(\rho_U) \subset U$ 且 $\mathrm{supp}(\rho_V) \subset V$。
2. 对所有 $x \in M$，$\rho_U(x) + \rho_V(x) = 1$。

有了[单位分解](@entry_id:150115)，我们可以如下构造全局形式 $\omega$。首先，将 $\rho_U \beta$（定义在 $V$ 上）和 $\rho_V \alpha$（定义在 $U$ 上）通过在各自开集外延拓为零，得到 $M$ 上的光滑形式。然后定义：
$$ \omega = (\text{延拓的 }\rho_U \beta) + (\text{延拓的 }\rho_V \alpha) $$
一个更简洁（尽管不严谨）的写法是 $\omega = \rho_U \beta + \rho_V \alpha$。通过在 $U$ 和 $V$ 上分别验证，可以证明 $\omega|_U = \alpha$ 和 $\omega|_V = \beta$，从而证明了 $\ker(s) \subseteq \mathrm{im}(r)$。这个构造过程是迈尔-维托里斯序列理论的核心机制之一。同样，映射 $s$ 的满射性也通过[单位分解](@entry_id:150115)来证明。

### 迈尔-维托里斯[长正合序列](@entry_id:153438)

上述关于微分形式复形的短[正合序列](@entry_id:151503)，通过同调代数中的一个基本定理（通常称为[蛇引理](@entry_id:152840)或之字引理），可以“翻译”成一个关于[上同调群](@entry_id:142450)的**[长正合序列](@entry_id:153438) (long exact sequence)**。这个序列就是**迈尔-维托里斯序列**：
$$ \cdots \to H^k_{\mathrm{dR}}(M) \xrightarrow{r^*} H^k_{\mathrm{dR}}(U) \oplus H^k_{\mathrm{dR}}(V) \xrightarrow{s^*} H^k_{\mathrm{dR}}(U \cap V) \xrightarrow{\delta} H^{k+1}_{\mathrm{dR}}(M) \to \cdots $$
这个序列是无穷的，向左右两个方向无限延伸。序列中的每个映射都是由短[正合序列](@entry_id:151503)中的映射在同调层面上诱导而来。

- **映射 $r^*$**: 由限制映射 $r$ 诱导。它将一个全局同调类 $[\omega] \in H^k_{\mathrm{dR}}(M)$ 映射到由其在 $U$ 和 $V$ 上的限制所代表的同调类对 $([\omega|_U], [\omega|_V])$。

- **映射 $s^*$**: 由差映射 $s$ 诱导。它作用于一对同调类 $([\alpha], [\beta]) \in H^k_{\mathrm{dR}}(U) \oplus H^k_{\mathrm{dR}}(V)$，结果是它们在交集上的限制之差的同调类 $[\alpha|_{U \cap V} - \beta|_{U \cap V}]$。

- **映射 $\delta$**: 这是**[连接同态](@entry_id:160713) (connecting homomorphism)**，也是序列中最奇妙的部分。它将度数提升 1，把 $U \cap V$ 上的 $k$ 阶[上同调](@entry_id:160558)信息与 $M$ 上的 $(k+1)$ 阶上同调信息联系起来。

### [连接同态](@entry_id:160713) $\delta$

[连接同态](@entry_id:160713) $\delta$ 的构造是整个理论的精髓，它揭示了局部信息如何“粘合”成全局[拓扑性质](@entry_id:141605)。其构造过程可以概括为以下步骤，这是一个典型的“图追逐” (diagram chasing) 论证：

1.  **选取代表元**：从 $H^k_{\mathrm{dR}}(U \cap V)$ 中任取一个同调类 $[\eta]$，它由一个闭 $k$-形式 $\eta \in \Omega^k(U \cap V)$ 代表，即 $d\eta = 0$。

2.  **提升到 $U$ 和 $V$**：由于映射 $s: \Omega^k(U) \oplus \Omega^k(V) \to \Omega^k(U \cap V)$ 是满射，我们总能找到一对形式 $(\alpha, \beta)$（其中 $\alpha \in \Omega^k(U), \beta \in \Omega^k(V)$）使得 $s(\alpha, \beta) = \alpha|_{U \cap V} - \beta|_{U \cap V} = \eta$。这个提升过程不是唯一的，但可以使用[单位分解](@entry_id:150115) $\{\rho_U, \rho_V\}$ 给出一个标准的构造：可以取 $\alpha$ 为 $\rho_V \eta$ 在 $U$ 上的光滑延拓，$\beta$ 为 $-\rho_U \eta$ 在 $V$ 上的光滑延拓。

3.  **应用[外微分](@entry_id:161900)**：对 $(\alpha, \beta)$ 应用外[微分算子](@entry_id:140145) $d$，得到一对 $(k+1)$-形式 $(d\alpha, d\beta)$。由于 $d$ 与 $s$ 可交换，我们有 $s(d\alpha, d\beta) = d(s(\alpha, \beta)) = d\eta = 0$。这意味着 $(d\alpha, d\beta)$ 属于 $s$ 的核。

4.  **寻找全局原像**：根据短[正合序列](@entry_id:151503)在 $\Omega^{k+1}(U) \oplus \Omega^{k+1}(V)$ 处的正合性 ($\ker(s) = \mathrm{im}(r)$)，必然存在一个唯一的全局 $(k+1)$-形式 $\omega \in \Omega^{k+1}(M)$，使得 $r(\omega) = (d\alpha, d\beta)$。也就是说，这个全局形式 $\omega$ 满足 $\omega|_U = d\alpha$ 和 $\omega|_V = d\beta$。

5.  **定义 $\delta([\eta])$**：这个全局形式 $\omega$ 是闭形式（因为 $d\omega$ 在 $U$ 和 $V$ 上均为零），因此它代表了 $H^{k+1}_{\mathrm{dR}}(M)$ 中的一个同调类 $[\omega]$。我们定义 $\delta([\eta]) = [\omega]$。

尽管这个构造过程涉及[单位分解](@entry_id:150115)和提升形式的选择，但最终得到的[上同调类](@entry_id:263961) $[\omega]$ 被证明是唯一的，与所有中间选择无关。

使用在第2步中提到的标准提升，我们可以得到 $\delta$ 的一个具体公式。$\omega$ 在 $U$ 上的限制为 $d\alpha = d(\rho_V \eta) = d\rho_V \wedge \eta + \rho_V d\eta$。由于 $\eta$ 是闭形式，$d\eta = 0$，所以 $\omega|_U = d\rho_V \wedge \eta$。类似地，$\omega|_V = -d\rho_U \wedge \eta$。这两个表达式在交集 $U \cap V$ 上是相等的，因为 $\rho_U + \rho_V = 1$ 蕴含 $d\rho_U + d\rho_V = 0$。

### 诠释正合性：序列的力量

迈尔-维托里斯序列的“正合性”是其成为强大计算工具的根源。它在每个[上同调群](@entry_id:142450)处都提供了一个精确的代数关系，将局部信息与全局信息联系起来。

#### 在 $H^k_{\mathrm{dR}}(M)$ 处的正合性
序列的 $\cdots \to H^{k-1}_{\mathrm{dR}}(U \cap V) \xrightarrow{\delta} H^k_{\mathrm{dR}}(M) \xrightarrow{r^*} H^k_{\mathrm{dR}}(U) \oplus H^k_{\mathrm{dR}}(V) \to \cdots$ 部分意味着 $\ker(r^*) = \mathrm{im}(\delta)$。
这告诉我们：一个全局闭形式 $\omega$ 在 $U$ 和 $V$ 上的限制都是恰当形式（即 $[\omega|_U]=0$ 和 $[\omega|_V]=0$），当且仅当它的同调类 $[\omega]$ 来自于交集上的一个 $(k-1)$ 阶同调类经由 $\delta$ 的映射。
这揭示了一个深刻的道理：**局部可解性不等于全局可解性**。一个在 $U$ 和 $V$ 上都是恰当的闭形式 $\omega$，不一定在整个 $M$ 上是恰当的。它不是恰当形式的“阻碍”正存在于 $H^{k-1}_{\mathrm{dR}}(U \cap V)$ 中。如果 $H^{k-1}_{\mathrm{dR}}(U \cap V)=0$，那么这种阻碍就不存在，任何在 $U$ 和 $V$ 上都恰当的闭形式在 $M$ 上也一定是恰当的。一个经典的例子是在圆 $S^1$ 上，一个非恰当的闭[1-形式](@entry_id:270392)（如角度形式 $d\theta$）可以被限制在两个相互交叠的、同胚于实线段的开弧上，而在每个开弧上它都是恰当的。这里的阻碍来自于 $H^0_{\mathrm{dR}}(U \cap V) \cong \mathbb{R} \oplus \mathbb{R}$。

#### 在 $H^k_{\mathrm{dR}}(U) \oplus H^k_{\mathrm{dR}}(V)$ 处的正合性
序列的 $\cdots \to H^k_{\mathrm{dR}}(M) \xrightarrow{r^*} H^k_{\mathrm{dR}}(U) \oplus H^k_{\mathrm{dR}}(V) \xrightarrow{s^*} H^k_{\mathrm{dR}}(U \cap V) \to \cdots$ 部分意味着 $\ker(s^*) = \mathrm{im}(r^*)$。
这提供了**[上同调类](@entry_id:263961)的粘合条件**。一对同调类 $([\alpha], [\beta])$ 满足 $s^*([\alpha], [\beta])=0$，即 $[\alpha|_{U \cap V}] = [\beta|_{U \cap V}]$，当且仅当这对同调类是某个全局同调类 $[\omega] \in H^k_{\mathrm{dR}}(M)$ 的限制，即 $([\alpha], [\beta]) = ([\omega|_U], [\omega|_V])$。换言之，来自 $U$ 和 $V$ 的两个[上同调类](@entry_id:263961)，如果它们在交集上的“表现”一致，那么它们就可以被“粘合”成一个全局的[上同调类](@entry_id:263961)。

#### 在 $H^k_{\mathrm{dR}}(U \cap V)$ 处的正合性
序列的 $\cdots \to H^k_{\mathrm{dR}}(U) \oplus H^k_{\mathrm{dR}}(V) \xrightarrow{s^*} H^k_{\mathrm{dR}}(U \cap V) \xrightarrow{\delta} H^{k+1}_{\mathrm{dR}}(M) \to \cdots$ 部分意味着 $\ker(\delta) = \mathrm{im}(s^*)$。
这阐明了[连接同态](@entry_id:160713) $\delta$ 的作用。一个定义在交集上的同调类 $[\eta] \in H^k_{\mathrm{dR}}(U \cap V)$ 在 $\delta$ 映射下为零，当且仅当 $[\eta]$ 可以表示为 $U$ 上的一个同调类和 $V$ 上的一个同调类在交集上限制的差，即 $[\eta] = [\alpha|_{U \cap V}] - [\beta|_{U \cap V}]$。这为我们提供了一个判断交集上的一个类是否会产生非平凡的全局高阶上同调的判据。那些不能被分解为来自 $U$ 和 $V$ 的类的差的元素，正是通过 $\delta$ 映射贡献于 $H^{k+1}_{\mathrm{dR}}(M)$ 的非平凡元素。

### 自然性与应用

迈尔-维托里斯序列的一个极其重要的性质是其**自然性 (naturality)**。假设我们有两个[流形](@entry_id:153038) $M$ 和 $N$，它们各自有开覆盖 $M=U \cup V$ 和 $N=U' \cup V'$。如果有一个[光滑映射](@entry_id:203730) $f: M \to N$ 保持了这些覆盖结构，即 $f(U) \subseteq U'$ 且 $f(V) \subseteq V'$，那么这个映射 $f$ 会诱导两个[长正合序列](@entry_id:153438)之间的一系列[交换图](@entry_id:747516)，形成一个“阶梯”。

对于每一阶[上同调](@entry_id:160558)，由[拉回](@entry_id:160816)映射 $f^*$ 诱导的映射构成了这个阶梯的“梯级”。例如，我们有以下[交换图](@entry_id:747516)：
$$
\begin{CD}
H^k(U' \cap V') @>{\delta_N}>> H^{k+1}(N) \\
@A{(f|_{U' \cap V'})^*}AA @AA{f^*}A \\
H^k(U \cap V) @>{\delta_M}>> H^{k+1}(M)
\end{CD}
$$
这个图的[可交换性](@entry_id:263314)意味着 $f^* \circ \delta_N = \delta_M \circ (f|_{U' \cap V'})^*$。简而言之，通过 $\delta$ 映射再[拉回](@entry_id:160816)，与先[拉回](@entry_id:160816)再通过 $\delta$ 映射的结果是相同的（在同调意义上）。

这个性质与**[同伦不变性](@entry_id:150428) (homotopy invariance)** 相结合，构成了计算[上同调](@entry_id:160558)的强大策略。[德拉姆上同调](@entry_id:158673)的一个基本性质是，同伦等价的[流形](@entry_id:153038)具有同构的[上同调群](@entry_id:142450)。

让我们通过一个例子来展示这一切如何协同工作。考虑计算一个开圆环 $X = S^1 \times (0,1)$ 的[上同调](@entry_id:160558)。
1.  **利用[同伦不变性](@entry_id:150428)简化问题**：[圆环](@entry_id:163678) $X$ 可以光滑地强[形变收缩](@entry_id:148036)到其中心的圆周 $S^1 \times \{1/2\}$。这意味着 $X$ 和 $S^1$ 是[同伦等价](@entry_id:150816)的。因此，它们的[德拉姆上同调](@entry_id:158673)群是同构的。这个同构由[投影映射](@entry_id:153398) $p: X \to S^1$ 的[拉回](@entry_id:160816) $p^*: H^k_{\mathrm{dR}}(S^1) \to H^k_{\mathrm{dR}}(X)$ 实现。于是，计算 $H^k_{\mathrm{dR}}(X)$ 的问题就转化为了计算 $H^k_{\mathrm{dR}}(S^1)$。

2.  **利用迈尔-维托里斯序列计算 $H^k_{\mathrm{dR}}(S^1)$**：我们用两个相互交叠的开弧 $I_1$ 和 $I_2$ 来覆盖 $S^1$。每个开弧都是可收缩的（同胚于[开区间](@entry_id:157577)），因此它们的所有正阶[上同调群](@entry_id:142450)都为零：$H^{k\ge 1}_{\mathrm{dR}}(I_1)=H^{k\ge 1}_{\mathrm{dR}}(I_2)=0$。它们的交集 $I_1 \cap I_2$ 由两个不相交的开弧组成，因此 $H^0_{\mathrm{dR}}(I_1 \cap I_2) \cong \mathbb{R} \oplus \mathbb{R}$。

    考察 $S^1$ 的迈尔-维托里斯序列的一部分：
    $$ H^0_{\mathrm{dR}}(I_1) \oplus H^0_{\mathrm{dR}}(I_2) \xrightarrow{s^*} H^0_{\mathrm{dR}}(I_1 \cap I_2) \xrightarrow{\delta} H^1_{\mathrm{dR}}(S^1) \to H^1_{\mathrm{dR}}(I_1) \oplus H^1_{\mathrm{dR}}(I_2) $$
    由于 $H^1_{\mathrm{dR}}(I_1)=H^1_{\mathrm{dR}}(I_2)=0$，最右边的项为零。根据正合性，这意味着 $\delta$ 是满射。
    $H^0_{\mathrm{dR}}(I_1) \cong \mathbb{R}$ 和 $H^0_{\mathrm{dR}}(I_2) \cong \mathbb{R}$，所以 $H^0_{\mathrm{dR}}(I_1) \oplus H^0_{\mathrm{dR}}(I_2) \cong \mathbb{R}^2$。映射 $s^*$ 将一对常数 $(c_1, c_2)$ 映到在 $I_1 \cap I_2$ 上的限制之差 $c_1-c_2$。这个差在 $I_1 \cap I_2$ 的两个连通分支上都是相同的常数。因此，$\mathrm{im}(s^*)$ 对应于 $\mathbb{R} \oplus \mathbb{R}$ 中的对角线[子空间](@entry_id:150286) $\{(d,d) | d \in \mathbb{R}\}$。
    根据正合性，$\ker(\delta) = \mathrm{im}(s^*)$。因此，我们有同构：
    $$ H^1_{\mathrm{dR}}(S^1) \cong \frac{H^0_{\mathrm{dR}}(I_1 \cap I_2)}{\mathrm{im}(s^*)} \cong \frac{\mathbb{R} \oplus \mathbb{R}}{\{(d,d)\}} \cong \mathbb{R} $$
    我们不仅计算出 $H^1_{\mathrm{dR}}(S^1) \cong \mathbb{R}$，还找到了它的生成元。例如，由 $H^0_{\mathrm{dR}}(I_1 \cap I_2)$ 中由向量 $(1, -1)$ 代表的类（即在一个交集分支上取值为1，在另一个上取值为-1的函数），它不属于 $\ker(\delta)$，因此它在 $\delta$ 映射下的像 $\delta([1, -1])$ 是 $H^1_{\mathrm{dR}}(S^1)$ 的一个非零元素，即一个生成元。

3.  **整合结果**：我们已经知道 $p^*: H^1_{\mathrm{dR}}(S^1) \to H^1_{\mathrm{dR}}(X)$ 是一个同构。因此，$H^1_{\mathrm{dR}}(X) \cong \mathbb{R}$，其生成元就是 $S^1$ 的生成元在 $p^*$ 下的像。

自然性保证了这种分步计算的内在一致性。我们可以为[圆环](@entry_id:163678) $X$ 构造一个相应的覆盖 $U=p^{-1}(I_1)$ 和 $V=p^{-1}(I_2)$，并直接应用迈尔-维托里斯序列来计算 $H^1_{\mathrm{dR}}(X)$。自然性告诉我们，这两种方法（先计算 $S^1$ 再[拉回](@entry_id:160816)，或直接计算 $X$）会得到一致的结果。这展示了迈尔-维托里斯序列如何与其他基本工具无缝集成，共同构成[微分拓扑](@entry_id:157662)中强大的计算框架。