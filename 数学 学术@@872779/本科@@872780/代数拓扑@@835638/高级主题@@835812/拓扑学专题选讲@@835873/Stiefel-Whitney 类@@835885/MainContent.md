## 引言
施蒂费尔-惠特尼类（Stiefel-Whitney classes）是代数拓扑学中用于研究实向量丛的基石。它们是一系列强大的代数[不变量](@entry_id:148850)，能够将向量丛复杂的拓扑结构，如扭曲和整体性质，转化为可以在[上同调环](@entry_id:160158)中进行计算的代数对象。这一理论的深远意义在于，它为[微分几何](@entry_id:145818)和拓扑学中的许多核心问题——例如一个[流形](@entry_id:153038)是否可定向、能否浸入高维空间、或是否允许定义[旋量](@entry_id:158054)场——提供了精确的判别标准。本文旨在为读者构建一个关于施蒂费尔-惠特尼类的完整知识框架，弥合抽象定义与具体应用之间的鸿沟。

在接下来的内容中，我们将分步探索这一迷人的领域。在“原理与机制”一章，我们将从公理化定义出发，建立施蒂费尔-惠特尼类的理论基础，并介绍如[惠特尼和公式](@entry_id:271148)与[分裂原理](@entry_id:158035)等核心计算工具。随后，“应用与跨学科联系”一章将展示这些抽象工具的威力，揭示它们如何判定[流形的可定向性](@entry_id:158057)、[自旋结构](@entry_id:161662)，解决浸入与嵌入问题，甚至在理论物理的前沿中扮演关键角色。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者巩固所学知识，将理论应用于具体的拓扑计算中。

## 原理与机制

Stiefel-Whitney 类为研究实向量丛提供了一套强有力的代数[不变量](@entry_id:148850)。这些[不变量](@entry_id:148850)是定义在向量丛底空间上的[上同调类](@entry_id:263961)，其系数取自[二元域](@entry_id:267286) $\mathbb{Z}/2\mathbb{Z}$。它们以一种深刻的方式捕捉了向量丛的扭曲结构。本章将系统地阐述 Stiefel-Whitney 类的公理化定义、核心性质以及它们在几何与拓扑中的关键应用。

### 公理化基础

Stiefel-Whitney 类的现代处理方式是公理化的，这意味着我们首先规定它们必须遵守的一套基本法则。从这些法则出发，我们可以推导出它们所有的性质，并证明它们的存在性和唯一性。对于定义在拓扑空间 $X$ 上的任意一个实向量丛 $\xi$，其 Stiefel-Whitney 类是一系列[上同调类](@entry_id:263961) $w_i(\xi) \in H^i(X; \mathbb{Z}/2\mathbb{Z})$，其中 $i=0, 1, 2, \dots$。将这些类合并为一个形式和，我们得到**总 Stiefel-Whitney 类 (total Stiefel-Whitney class)**：
$$
w(\xi) = \sum_{i \ge 0} w_i(\xi) = w_0(\xi) + w_1(\xi) + w_2(\xi) + \dots
$$
这是一个位于总[上同调环](@entry_id:160158) $H^*(X; \mathbb{Z}/2\mathbb{Z})$ 中的元素。这些类由以下四个基本公理所唯一确定。

#### 1. 第零类与正规化公理 (Normalization Axiom)
对于任意非空、[路径连通空间](@entry_id:152443) $X$ 上的任意实向量叢 $\xi$, 其第零阶 Stiefel-Whitney 类 $w_0(\xi)$ 是上同调群 $H^0(X; \mathbb{Z}/2\mathbb{Z})$ 中的单位元。

这是一个基础性的规定，确保了理论的一致性。假设一个向量丛 $\xi$ 存在一个“稳定逆” $\eta$，使得它们的 Whitney 和 $\xi \oplus \eta$ 是一个平凡丛 $\epsilon^k$。利用 Whitney 和公式（见下文）$w(\xi \oplus \eta) = w(\xi) \smile w(\eta)$ 和平凡丛公理 $w(\epsilon^k)=1$，我们得到 $w(\xi) \smile w(\eta) = 1$。考察这个等式在零次[上同调](@entry_id:160558)的部分，我们有 $w_0(\xi) \smile w_0(\eta) = 1$。由于 $X$ 是[路径连通](@entry_id:148704)的，$H^0(X; \mathbb{Z}/2\mathbb{Z}) \cong \mathbb{Z}/2\mathbb{Z}=\{0, 1\}$，其中的杯积就是域中的乘法。在 $\mathbb{Z}/2\mathbb{Z}$ 中，乘积为 1 的唯一可能是两个因子都为 1。因此，我们必须有 $w_0(\xi)=1$。[@problem_id:1675397]

#### 2. 维数公理 (Dimension Axiom)
如果向量丛 $\xi$ 的秩（即纤维的维数）为 $k$，那么对于所有 $i > k$，其 Stiefel-Whitney 类 $w_i(\xi)$ 均为零。

这个公理是自然的，它意味着向量丛的拓扑复杂性受其纤维维数的限制。因此，一个秩为 $k$ 的丛 $\xi$ 的总 Stiefel-Whitney 类实际上是一个有限和：
$$
w(\xi) = 1 + w_1(\xi) + \dots + w_k(\xi)
$$

#### 3. Whitney 和公式 (Whitney Sum Formula)
对于定义在同一底空间 $X$ 上的任意两个向量丛 $\xi$ 和 $\eta$，它们的 Whitney 和 $\xi \oplus \eta$ 的总 Stiefel-Whitney 类等于它们各自总 Stiefel-Whitney 类的杯积：
$$
w(\xi \oplus \eta) = w(\xi) \smile w(\eta)
$$
这是最具计算威力的公理之一。它将向量丛的[直和](@entry_id:156782)操作转化为[上同调环](@entry_id:160158)中的乘法。例如，考虑一个 2 秩向量丛 $\xi$ 和一个 3 秩向量丛 $\eta$。它们的 Whitney 和 $\zeta = \xi \oplus \eta$ 是一个 5 秩丛。我们可以计算 $\zeta$ 的 Stiefel-Whitney 类。根据维数公理，我们有 $w(\xi) = 1 + w_1(\xi) + w_2(\xi)$ 和 $w(\eta) = 1 + w_1(\eta) + w_2(\eta) + w_3(\eta)$。根据 Whitney 和公式：
$$
w(\zeta) = (1 + w_1(\xi) + w_2(\xi)) \smile (1 + w_1(\eta) + w_2(\eta) + w_3(\eta))
$$
要找到 $\zeta$ 的第四个 Stiefel-Whitney 类 $w_4(\zeta)$，我们需要展开这个乘积，并收集所有次数为 4 的项（一个形如 $w_i(\xi) \smile w_j(\eta)$ 的项的次数是 $i+j$）。符合条件的项是 $w_1(\xi) \smile w_3(\eta)$ (次数 $1+3=4$) 和 $w_2(\xi) \smile w_2(\eta)$ (次数 $2+2=4$)。因此，我们得到：
$$
w_4(\zeta) = w_1(\xi) \smile w_3(\eta) + w_2(\xi) \smile w_2(\eta)
$$
这个例子 [@problem_id:1675390] 展示了如何系统地利用公理进行计算。

#### 4. 自然性公理 (Naturality Axiom)
如果 $f: Y \to X$ 是一个[连续映射](@entry_id:153855)，$\xi$ 是 $X$ 上的一个向量丛，那么 $Y$ 上的[拉回丛](@entry_id:159346) $f^*\xi$ 的总 Stiefel-Whitney 类是 $\xi$ 的总 Stiefel-Whitney 类通过 $f$ 诱导的[上同调](@entry_id:160558)映射 $f^*$ 的像：
$$
w(f^*\xi) = f^*(w(\xi))
$$
换言之，$w_i(f^*\xi) = f^*(w_i(\xi))$ 对所有 $i$ 成立。自然性公理确保了 Stiefel-Whitney 类在空间之间的映射下表现良好，是“拓扑不变量”这一说法的精确表述。

例如，考虑从[实射影平面](@entry_id:150364) $\mathbb{R}P^2$到 $\mathbb{R}P^5$ 的标准包含映射 $i: \mathbb{R}P^2 \hookrightarrow \mathbb{R}P^5$。$\mathbb{R}P^n$ 的[上同调环](@entry_id:160158)为 $H^*(\mathbb{R}P^n; \mathbb{Z}/2\mathbb{Z}) \cong (\mathbb{Z}/2\mathbb{Z})[x_n] / (x_n^{n+1})$，其中 $x_n$ 是 1 次生成元。映射 $i$ 诱导的[环同态](@entry_id:153804) $i^*$ 将 $x_5$ 映为 $x_2$。设 $\gamma_1^5$ 为 $\mathbb{R}P^5$ 上的典范线丛，其总 Stiefel-Whitney 类为 $w(\gamma_1^5) = 1+x_5$。现在考虑 $\mathbb{R}P^5$ 上的 2 秩丛 $\eta = \gamma_1^5 \oplus \gamma_1^5$。利用 Whitney 和公式，我们有 $w(\eta) = (1+x_5)^2 = 1+2x_5+x_5^2=1+x_5^2$ (因为系数在 $\mathbb{Z}/2\mathbb{Z}$ 中)。我们想计算[拉回丛](@entry_id:159346) $i^*\eta$ 的第二 Stiefel-Whitney 类 $w_2(i^*\eta)$。根据自然性公理：
$$
w(i^*\eta) = i^*(w(\eta)) = i^*(1+x_5^2) = i^*(1) + i^*(x_5^2) = 1 + (i^*(x_5))^2 = 1 + x_2^2
$$
由此可知，$w_2(i^*\eta) = x_2^2 \in H^2(\mathbb{R}P^2; \mathbb{Z}/2\mathbb{Z})$。[@problem_id:1675361]

这些公理中的最后一块拼图是为最简单的非平凡丛——线丛——指定一个基准。这通常通过考察万有线丛 (universal line bundle) 来完成。万有线丛 $\gamma^1$ 定义在无限维[实射影空间](@entry_id:149094) $\mathbb{R}P^\infty$上，其关键性质是任何空间 $X$ 上的任何线丛都可以通过一个分类映射 $f:X \to \mathbb{R}P^\infty$ 从 $\gamma^1$ [拉回](@entry_id:160816)得到。公理规定 $w_1(\gamma^1)$ 是 $H^1(\mathbb{R}P^\infty; \mathbb{Z}/2\mathbb{Z})$ 的非零生成元。对于一个具体的例子，如 $\mathbb{R}P^1$ 上的 tautological line bundle，其分类映射就是包含映射 $\mathbb{R}P^1 \hookrightarrow \mathbb{R}P^\infty$。$H^1(\mathbb{R}P^1; \mathbb{Z}/2\mathbb{Z})$ 的生成元是 $\alpha$，那么该线丛的第一 Stiefel-Whitney 类就是 $\alpha$。[@problem_id:1675403]

### [分裂原理](@entry_id:158035)：理论的基石

公理化方法虽然简洁有效，但可能会让人觉得像空中楼阁。这些公理，特别是 Whitney 和公式，为何是“正确”的？**[分裂原理](@entry_id:158035) (Splitting Principle)** 为此提供了坚实的理论基础。它断言：

> 对于任意底空间 $B$ 上的任意秩为 $n$ 的实向量丛 $E$，存在一个[辅助空间](@entry_id:638067) $B'$ 和一个[连续映射](@entry_id:153855) $p: B' \to B$，使得：
> 1.  [拉回丛](@entry_id:159346) $p^*E$ 同构于 $n$ 个线丛的 Whitney 和：$p^*E \cong L_1 \oplus L_2 \oplus \dots \oplus L_n$。
> 2.  由 $p$ 诱导的[上同调环](@entry_id:160158)同态 $p^*: H^*(B; \mathbb{Z}/2\mathbb{Z}) \to H^*(B'; \mathbb{Z}/2\mathbb{Z})$ 是一个[单射](@entry_id:183792)（即 injective map）。

[分裂原理](@entry_id:158035)的精髓在于，它允许我们将关于任意向量丛的证明问题，转化为一个更容易处理的、关于线丛直和的问题。这是因为线丛的 Stiefel-Whitney 类非常简单：一个线丛 $L$ 的总 Stiefel-Whitney 类就是 $w(L) = 1 + w_1(L)$。

让我们看看[分裂原理](@entry_id:158035)如何用于证明 Whitney 和公式 $w(E \oplus F) = w(E) \smile w(F)$。根据[分裂原理](@entry_id:158035)，我们可以找到一个映射 $p: B' \to B$，使得 $p^*E$ 和 $p^*F$ 都分裂为线丛之和，并且 $p^*$ 是单射。由于 $p^*$ 是[单射](@entry_id:183792)，要证明 $w(E \oplus F) = w(E) \smile w(F)$，我们只需证明 $p^*(w(E \oplus F)) = p^*(w(E) \smile w(F))$。

利用自然性公理，等式左边变为 $w(p^*(E \oplus F)) = w(p^*E \oplus p^*F)$。等式右边变为 $p^*(w(E)) \smile p^*(w(F)) = w(p^*E) \smile w(p^*F)$。于是，我们只需在空间 $B'$ 上证明 $w(p^*E \oplus p^*F) = w(p^*E) \smile w(p^*F)$。但在 $B'$ 上，$p^*E$ 和 $p^*F$ 都已分裂为线丛之和，对线丛之和，Whitney 和公式可以通过基本代数直接验证。因此，等式在 $B'$ 上成立。由于 $p^*$ 是单射，等式在原始空间 $B$ 上也必须成立。

所以，[分裂原理](@entry_id:158035)的 conceptual function 是将一般性问题简化到可直接验证的特例（线丛），然后利用 $p^*$ 的[单射性](@entry_id:147722)将结果推广回一般情况。[@problem_id:1675393]

### 核心应用：从几何到示性类

Stiefel-Whitney 类的真正威力在于它们能够“探测”并量化向量丛的几何与拓扑性质。特别是，当应用于[流形](@entry_id:153038)的切丛时，它们揭示了[流形](@entry_id:153038)本身的深刻属性。

#### [可定向性](@entry_id:149777)与第一 Stiefel-Whitney 类 ($w_1$)

一个光滑流形最基本的几何性质之一是其**[可定向性](@entry_id:149777) (orientability)**。直观上，一个[曲面](@entry_id:267450)是可定向的，如果我们可以为它定义一致的“内”和“外”，或者说，在[曲面](@entry_id:267450)上移动的观察者不会发现自己的左右手方向发生了颠倒。著名的莫比乌斯带和[克莱因瓶](@entry_id:149661)就是不可定向的例子。

这个几何概念与第一 Stiefel-Whitney 类之间有着精准的代数联系：
> 一个光滑连通[流形](@entry_id:153038) $M$ 是可定向的，当且仅当其切丛的第一 Stiefel-Whitney 类为零，即 $w_1(TM) = 0$。

因此，$w_1(TM) \in H^1(M; \mathbb{Z}/2\mathbb{Z})$ 可以被视为[流形](@entry_id:153038) $M$ **[可定向性](@entry_id:149777)的障碍 (obstruction to orientability)**。如果它非零，[流形](@entry_id:153038)就不可定向。

根据这个定理，我们可以立即判断一些常见[流形的可定向性](@entry_id:158057) [@problem_id:1675405]：
-   **球面 $S^n$ 和环面 $T^n$**：这些都是标准的[可定向流形](@entry_id:276936)。我们可以一致地为它们定义定向（例如，球面上的外[法向量](@entry_id:264185)）。因此，必然有 $w_1(TS^n) = 0$ 和 $w_1(TT^n) = 0$。
-   **欧氏空间 $\mathbb{R}^n$**：其切丛是平凡的 $T\mathbb{R}^n \cong \mathbb{R}^n \times \mathbb{R}^n$。平凡丛的所有 Stiefel-Whitney 类（除了 $w_0$）都为零，所以 $w_1(T\mathbb{R}^n)=0$，$\mathbb{R}^n$ 是可定向的。
-   **[克莱因瓶](@entry_id:149661) (Klein bottle) $K$ 和[实射影平面](@entry_id:150364) $\mathbb{R}P^2$**：这两个是经典的[不可定向曲面](@entry_id:276231)。因此，它们的[切丛](@entry_id:161294)的第一 Stiefel-Whitney 类必然非零：$w_1(TK) \neq 0$ [@problem_id:1675380] 和 $w_1(T\mathbb{R}P^2) \neq 0$。

#### Spin 结构与第二 Stiefel-Whitney 类 ($w_2$)

在更深入的几何和物理学（如[弦理论](@entry_id:145688)和[量子场论](@entry_id:138177)）中，一个比可定向更精细的结构——**Spin 结构**——扮演着核心角色。一个[流形](@entry_id:153038)如果拥有 Spin 结构，我们称之为 **Spin [流形](@entry_id:153038) (Spin manifold)**。粗略地说，[可定向流形](@entry_id:276936)允许我们一致地定义旋转，而 Spin [流形](@entry_id:153038)则允许我们一致地定义这些旋转的“平方根”。

Spin 结构的存在性也由一个 Stiefel-Whitney 类来判定。首先，一个[流形](@entry_id:153038)必须是可定向的才可能拥有 Spin 结构。对于[可定向流形](@entry_id:276936)，判据如下：
> 一个光滑、可定向的[流形](@entry_id:153038) $M$ 存在 Spin 结构，当且仅当其[切丛](@entry_id:161294)的第二 Stiefel-Whitney 类为零，即 $w_2(TM) = 0$。

因此，$w_2(TM) \in H^2(M; \mathbb{Z}/2\mathbb{Z})$ 是在可定向条件下**存在 Spin 结构的障碍**。

让我们以[复射影空间](@entry_id:268402) $\mathbb{C}P^n$ 为例。这是一个实维度为 $2n$ 的光滑[可定向流形](@entry_id:276936)。其[上同调环](@entry_id:160158)为 $H^*(\mathbb{C}P^n; \mathbb{Z}/2\mathbb{Z}) \cong (\mathbb{Z}/2\mathbb{Z})[a]/(a^{n+1})$，其中 $a$ 是 $H^2$ 的生成元。一个重要的已知事实是其切丛的总 Stiefel-Whitney 类为 $w(T\mathbb{C}P^n) = (1+a)^{n+1}$。利用[二项式定理](@entry_id:276665)，我们展开它：
$$
w(T\mathbb{C}P^n) = \sum_{k=0}^{n+1} \binom{n+1}{k} a^k = 1 + \binom{n+1}{1}a + \binom{n+1}{2}a^2 + \dots
$$
$w_2(T\mathbb{C}P^n)$ 是上同调次数为 2 的部分。由于 $a$ 的次数是 2，这对应于 $k=1$ 的项。所以，$w_2(T\mathbb{C}P^n) = \binom{n+1}{1} a \pmod 2 = (n+1)a \pmod 2$。这个类为零的条件是系数 $(n+1)$ 在模 2 意义下为零，即 $n+1$ 是偶数，或者说 $n$ 是奇数。

因此，$\mathbb{C}P^n$ 存在[自旋结构](@entry_id:161662)当且仅当 $n$ 是奇数。例如，$\mathbb{C}P^1, \mathbb{C}P^3, \mathbb{C}P^5, \mathbb{C}P^7$ 是[自旋流形](@entry_id:200931)，而 $\mathbb{C}P^2, \mathbb{C}P^4, \mathbb{C}P^6$ 不是。[@problem_id:1675379]

#### 向量场与最高 Stiefel-Whitney 类 ($w_k$)

另一个基本的拓扑问题是关于向量丛**[截面](@entry_id:154995) (section)** 的存在性。对于[流形](@entry_id:153038)的[切丛](@entry_id:161294) $TM$ 而言，一个[截面](@entry_id:154995)就是一个向量场。一个特别有趣的问题是：一个[流形](@entry_id:153038)上是否存在一个**处处非零的向量场 (nowhere-zero vector field)**？

最高 Stiefel-Whitney 类为此提供了一个强大的障碍。对于一个秩为 $k$ 的实向量丛 $\xi$：
> 如果 $\xi$ 存在一个处处非零的[截面](@entry_id:154995)，那么它的最高 Stiefel-Whitney 类必须为零，即 $w_k(\xi) = 0$。

其 converse 不一定成立，但这个单向的结论已经非常有用。如果 $w_k(\xi) \neq 0$，我们就可以断定 $\xi$ 不存在处处非零的[截面](@entry_id:154995)。

以 4 维[实射影空间](@entry_id:149094) $\mathbb{R}P^4$ 的[切丛](@entry_id:161294) $T\mathbb{R}P^4$ 为例。这是一个秩为 4 的向量丛。我们已知 $H^*(\mathbb{R}P^n; \mathbb{Z}/2\mathbb{Z}) \cong (\mathbb{Z}/2\mathbb{Z})[a]/(a^{n+1})$ 和 $w(T\mathbb{R}P^n) = (1+a)^{n+1}$。对于 $n=4$：
$$
w(T\mathbb{R}P^4) = (1+a)^5 = 1 + 5a + 10a^2 + 10a^3 + 5a^4 + a^5
$$
在 $\mathbb{Z}/2\mathbb{Z}$ 系数下，并注意到 $a^5=0$，$10 \equiv 0 \pmod 2$，$5 \equiv 1 \pmod 2$，上式简化为：
$$
w(T\mathbb{R}P^4) = 1 + a + a^4
$$
由此可知，最高 Stiefel-Whitney 类为 $w_4(T\mathbb{R}P^4) = a^4$。因为 $a^4$ 在 $H^4(\mathbb{R}P^4; \mathbb{Z}/2\mathbb{Z})$ 中是非零元素，所以 $w_4(T\mathbb{R}P^4) \neq 0$。根据上述[障碍理论](@entry_id:161880)，我们立刻得出结论：$\mathbb{R}P^4$ 上不存在处处非零的[切向量](@entry_id:265494)场。[@problem_id:1675395]

### 深度[不变量](@entry_id:148850)：[Stiefel-Whitney 数](@entry_id:262572)与[配边理论](@entry_id:161998)

Stiefel-Whitney 类不仅可以单独使用，它们的组合也蕴含着深刻的拓扑信息。对于一个 $n$ 维闭[流形](@entry_id:153038)（即紧致无边）$M$，我们可以将次数总和为 $n$ 的 Stiefel-Whitney 类的杯积，作用在[流形](@entry_id:153038)的 $\mathbb{Z}/2\mathbb{Z}$ **基本闭类 (fundamental class)** $[M] \in H_n(M; \mathbb{Z}/2\mathbb{Z})$ 上。这个求值结果是一个 $\mathbb{Z}/2\mathbb{Z}$ 中的数（0 或 1），称为**[Stiefel-Whitney 数](@entry_id:262572) (Stiefel-Whitney number)**。

例如，对于任意分区 $n = i_1 + i_2 + \dots + i_k$，我们都可以构造一个 [Stiefel-Whitney 数](@entry_id:262572)：
$$
\langle w_{i_1}(TM) \smile w_{i_2}(TM) \smile \dots \smile w_{i_k}(TM), [M] \rangle \in \mathbb{Z}/2\mathbb{Z}
$$
其中 $\langle \cdot, \cdot \rangle$ 表示上同调类在同调类上的求值（Kronecker 配对）。

一个特别重要的 [Stiefel-Whitney 数](@entry_id:262572)是最高 Stiefel-Whitney 类本身对应的数 $\langle w_n(TM), [M] \rangle$。一个深刻的定理（有时称为 Wu 公式）指出，这个数等于[流形](@entry_id:153038) $M$ 的**[欧拉示性数](@entry_id:152513) (Euler characteristic)** $\chi(M)$ 模 2 的值：
$$
\langle w_n(TM), [M] \rangle = \chi(M) \pmod 2
$$
例如，对于 $\mathbb{R}P^2$，我们有 $w(T\mathbb{R}P^2) = 1+a+a^2$，所以 $w_2(T\mathbb{R}P^2) = a^2$。其 [Stiefel-Whitney 数](@entry_id:262572)为 $\langle a^2, [\mathbb{R}P^2] \rangle = 1$。这与 $\mathbb{R}P^2$ 的[欧拉示性数](@entry_id:152513) $\chi(\mathbb{R}P^2)=1$ 模 2 相吻合。[@problem_id:1675407]

[Stiefel-Whitney 数](@entry_id:262572)的终极应用之一是在 René Thom 的**[配边理论](@entry_id:161998) (cobordism theory)** 中。一个核心问题是：一个给定的 $n$ 维闭[流形](@entry_id:153038) $M$ 是否是某个 $(n+1)$ 维紧致流形 $W$ 的边界（即 $M = \partial W$）？如果是，我们称 $M$ 是一个**零配边 (null-cobordant)** 或**边界[流形](@entry_id:153038) (boundary manifold)**。

Thom 的革命性定理给出了一个完全代数的判据：
> 一个光滑闭 $n$-[流形](@entry_id:153038) $M$ 是一个边界[流形](@entry_id:153038)，当且仅当其所有的 [Stiefel-Whitney 数](@entry_id:262572)都为零。

这个定理将一个纯粹的几何构造问题（寻找一个“填充”[流形](@entry_id:153038) $W$）转化为了一个有限的代数计算。只要我们能找到任何一个非零的 [Stiefel-Whitney 数](@entry_id:262572)，就可以断定该[流形](@entry_id:153038)不是边界。

让我们用这个定理来检验一些[实射影空间](@entry_id:149094) [@problem_id:1675362]：
-   **$\mathbb{R}P^2$**：这是一个 2 维[流形](@entry_id:153038)。我们已经看到它的 [Stiefel-Whitney 数](@entry_id:262572) $\langle w_2(T\mathbb{R}P^2), [\mathbb{R}P^2] \rangle = \langle a^2, [\mathbb{R}P^2] \rangle = 1$。因为存在非零的 [Stiefel-Whitney 数](@entry_id:262572)，所以 $\mathbb{R}P^2$ 不是边界。
-   **$\mathbb{R}P^4$**：这是一个 4 维[流形](@entry_id:153038)。我们之前计算过 $w(T\mathbb{R}P^4)=1+a+a^4$。一个 4 次的 [Stiefel-Whitney 数](@entry_id:262572)是 $\langle w_4(T\mathbb{R}P^4), [\mathbb{R}P^4] \rangle = \langle a^4, [\mathbb{R}P^4] \rangle = 1$。因此，$\mathbb{R}P^4$ 也不是边界。
-   **$\mathbb{R}P^3$**：这是一个 3 维[流形](@entry_id:153038)。它的总 Stiefel-Whitney 类是 $w(T\mathbb{R}P^3) = (1+a)^4 = 1+4a+6a^2+4a^3+a^4$。在 $\mathbb{Z}/2\mathbb{Z}$ 系数下，这变为 $w(T\mathbb{R}P^3) = 1+a^4$。但在 $H^*(\mathbb{R}P^3; \mathbb{Z}/2\mathbb{Z}) \cong (\mathbb{Z}/2\mathbb{Z})[a]/(a^4)$ 中，$a^4=0$。所以 $w(T\mathbb{R}P^3) = 1$！这意味着所有 $i>0$ 的 Stiefel-Whitney 类 $w_i(T\mathbb{R}P^3)$ 都为零。因此，$\mathbb{R}P^3$ 的所有 [Stiefel-Whitney 数](@entry_id:262572)必然都是零。根据 Thom 的定理，$\mathbb{R}P^3$ 是一个边界[流形](@entry_id:153038)。（事实上，$\mathbb{R}P^3$ 是 4 维[复射影空间](@entry_id:268402) $\mathbb{C}P^2$ 中一个超曲面的边界。）

通过这些例子，我们看到 Stiefel-Whitney 类如何从一套抽象的公理出发，构建起一座连接代数拓扑与微分几何的桥梁，为我们理[解空间](@entry_id:200470)的深层结构提供了精准而有力的工具。