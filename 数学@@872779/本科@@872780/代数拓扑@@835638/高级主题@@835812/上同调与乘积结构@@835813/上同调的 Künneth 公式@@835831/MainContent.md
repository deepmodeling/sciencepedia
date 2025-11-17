## 引言
在代数拓扑学中，一个核心策略是通过分析空间的代数[不变量](@entry_id:148850)来理解其几何结构。当我们面对一个由简单空间通过笛卡尔积构造出的复杂空间 $X \times Y$ 时，一个自然而深刻的问题随之产生：我们能否利用已知的 $X$ 和 $Y$ 的上同调群 $H^*(X)$ 和 $H^*(Y)$，来系统地计算乘[积空间的上同调](@entry_id:266890)群 $H^*(X \times Y)$？这个知识上的缺口正是[Künneth公式](@entry_id:158001)所要填补的。[Künneth公式](@entry_id:158001)为这个问题提供了强有力的解答，它不仅是一个计算工具，更是连接不同空间拓扑性质的桥梁。

本文将带领读者全面掌握[上同调的Künneth公式](@entry_id:275804)。在“原理与机制”一章中，我们将从最简单的域系数情形入手，逐步过渡到包含挠子信息的、更为精细的整系数短[正合序列](@entry_id:151503)，并最终揭示其作为[上同调环](@entry_id:160158)同构的深层结构。随后的“应用与跨学科联系”章节将展示该公式的实际威力，从直接计算[拓扑不变量](@entry_id:138526)到在微分几何、[同伦论](@entry_id:150876)等领域中的关键作用。最后，“动手实践”部分提供了一系列精心设计的问题，帮助读者将理论知识转化为解决具体问题的能力。通过本章的学习，您将能够熟练运用[Künneth公式](@entry_id:158001)来分析和理解乘积空间的拓扑结构。

## 原理与机制

在理解了[上同调](@entry_id:160558)的基本概念之后，我们现在转向一个更高级但极其强大的工具：用于计算乘[积空间](@entry_id:151693)上同调的 **Künneth 公式**。拓扑学中一个常见的研究策略是将复杂的[空间分解](@entry_id:755142)为更简单的组成部分。如果一个空间可以表示为两个或多个更简单[空间的笛卡尔积](@entry_id:276174) $X \times Y$，我们自然会问：能否从 $X$ 和 $Y$ 的[上同调群](@entry_id:142450)来确定 $X \times Y$ 的[上同调群](@entry_id:142450)？Künneth 公式为这个问题提供了肯定的答案，但其具体形式的复杂性取决于我们使用的系[数环](@entry_id:636822)。本章将系统地阐述 Künneth 公式的不同形式，从最简单的情形开始，逐步揭示其内在机制的全部深度和威力。

### 最简单的情形：域系数上同调

当我们处理的系数是**域 (field)** $F$ 时，例如有理数域 $\mathbb{Q}$、[实数域](@entry_id:151347) $\mathbb{R}$ 或有限域 $\mathbb{Z}_p$（其中 $p$ 为素数），上同调群 $H^k(X; F)$ 成为域 $F$ 上的[向量空间](@entry_id:151108)。这种[代数结构](@entry_id:137052)的简化使得 Künneth 公式呈现出其最简洁、最直观的形式。

**Künneth 定理（域系数情形）**：设 $X$ 和 $Y$ 为[拓扑空间](@entry_id:155056)， $F$ 为一个域。若 $X$ 的上同调群 $H^k(X; F)$ 在每个维度 $k$ 上都是有限维的，则存在一个自然的同构：

$$
H^k(X \times Y; F) \cong \bigoplus_{i+j=k} \left( H^i(X; F) \otimes_F H^j(Y; F) \right)
$$

这里的 $\bigoplus$ 表示[向量空间](@entry_id:151108)的**[直和](@entry_id:156782) (direct sum)**，$\otimes_F$ 表示在域 $F$ 上的**[张量积](@entry_id:140694) (tensor product)**。对于[向量空间](@entry_id:151108)，$V \otimes_F W$ 的维度是两个空间维度的乘积，即 $\dim(V \otimes_F W) = (\dim V)(\dim W)$。因此，这个公式提供了一个直接的计算方法。

一个直接的推论是关于**[贝蒂数](@entry_id:153109) (Betti numbers)** 的。一个空间的第 $k$ 个贝蒂数 $b_k(X)$ 定义为 $H^k(X; \mathbb{Q})$ 的维数（通常在特征为零的域上是独立的）。取上述同构两边的维数，我们得到一个优雅的公式：

$$
b_k(X \times Y) = \sum_{i+j=k} b_i(X) b_j(Y)
$$

这个公式表明，乘[积空间](@entry_id:151693)的[贝蒂数](@entry_id:153109)可以通过其因[子空间](@entry_id:150286)贝蒂数的多项式卷积来计算。

**示例：环面与球面的乘积**
让我们通过一个具体的例子来理解这个公式的应用。考虑空间 $M = \mathbb{T}^3 \times S^4$，其中 $\mathbb{T}^3$ 是三维环面，$S^4$ 是四维球面。我们的目标是计算其第5个[贝蒂数](@entry_id:153109) $b_5(M)$ [@problem_id:1686239]。已知 $\mathbb{T}^n$ 的[贝蒂数](@entry_id:153109)为 $b_k(\mathbb{T}^n) = \binom{n}{k}$，而 $S^m$ 的[贝蒂数](@entry_id:153109)仅在 $b_0(S^m)$ 和 $b_m(S^m)$ 处为1，其余为0。
因此，我们有 $b_i(\mathbb{T}^3) = \binom{3}{i}$ 对 $i=0,1,2,3$ 成立，以及 $b_j(S^4)$ 仅在 $j=0,4$ 时为1。
应用公式：
$$
b_5(\mathbb{T}^3 \times S^4) = \sum_{i+j=5} b_i(\mathbb{T}^3) b_j(S^4)
$$
由于 $b_j(S^4)$ 的非零项很少，我们只需考虑 $j=0$ 和 $j=4$ 的情况。
当 $j=0$ 时，$i=5$，项为 $b_5(\mathbb{T}^3) b_0(S^4) = 0 \times 1 = 0$。
当 $j=4$ 时，$i=1$，项为 $b_1(\mathbb{T}^3) b_4(S^4) = \binom{3}{1} \times 1 = 3$。
所有其他项均为0。因此，$b_5(M) = 0 + 3 = 3$。

**示例：两个球面的乘积**
另一个经典例子是两个球面 $S^p \times S^q$ 的乘积（其中 $p, q > 0$）[@problem_id:1679007]。$H^k(S^n; \mathbb{Q})$ 仅在 $k=0$ 和 $k=n$ 时为 $\mathbb{Q}$，否则为0。因此， $H^k(S^p \times S^q; \mathbb{Q})$ 只有在 $k$ 能表示为 $i+j$（其中 $i \in \{0, p\}$, $j \in \{0, q\}$）时才可能非零。这意味着非零上同调群只可能出现在 $k \in \{0, p, q, p+q\}$ 这些维度上。
- $k=0$：仅由 $H^0(S^p) \otimes H^0(S^q)$ 贡献，维度为1。
- $k=p+q$：仅由 $H^p(S^p) \otimes H^q(S^q)$ 贡献，维度为1。
- $k=p$：由 $H^p(S^p) \otimes H^0(S^q)$ 贡献。如果 $p=q$，还会得到来自 $H^0(S^p) \otimes H^p(S^q)$ 的额外贡献。因此，当 $p \neq q$ 时， $d_p = \dim H^p(S^p \times S^q; \mathbb{Q}) = 1$；当 $p=q$ 时， $d_p = 2$。
- $k=q$：情况与 $k=p$ 类似。如果 $p \neq q$， $d_q=1$。如果 $p=q$，这个情况就与上面 $k=p$ 的情况重合了。

这个例子揭示了一个重要的现象：空间的对称性（如 $p=q$）会在其[上同调群](@entry_id:142450)的结构中留下印记。

**域系数的优势：消除挠子**
选择域作为系数的一个关键优势是它能“忽略”上同调群中的**挠子 (torsion)** 部分。例如，[克莱因瓶](@entry_id:149661) $K$ 的整系数上同调群为 $H^0(K;\mathbb{Z}) \cong \mathbb{Z}$, $H^1(K;\mathbb{Z}) \cong \mathbb{Z}$, $H^2(K;\mathbb{Z}) \cong \mathbb{Z}_2$。其中 $H^2$ 是一个[挠子群](@entry_id:139454)。如果我们想计算 $K \times K$ 的有理[上同调群](@entry_id:142450) $H^n(K \times K; \mathbb{Q})$，直接使用整系数[上同调](@entry_id:160558)会很复杂 [@problem_id:1686185]。然而，通过泛系数定理，我们可以先计算 $K$ 的有理[上同调](@entry_id:160558)。泛系数定理表明 $H^n(K; \mathbb{Q}) \cong \text{Hom}(H_n(K; \mathbb{Z}), \mathbb{Q})$，因为 $\mathbb{Q}$ 是一个[可除群](@entry_id:154489)，所以 Ext 项消失了。由于 $\text{Hom}(\mathbb{Z}_m, \mathbb{Q})=0$，这个过程有效地“杀死”了所有挠子信息，只保留了自由部分的信息。计算可得 $H^0(K;\mathbb{Q}) \cong \mathbb{Q}$, $H^1(K;\mathbb{Q}) \cong \mathbb{Q}$，而更高维的上同调为0。现在，我们可以轻松地应用 Künneth 公式来计算 $H^*(K \times K; \mathbb{Q})$ 的[贝蒂数](@entry_id:153109)，结果为 $b_0=1, b_1=2, b_2=1$，其余为0。这个例子生动地说明了，为了简化计算，策略性地选择域（尤其是特征为0的域，如 $\mathbb{Q}$）作为系数是多么有效。

### 完整图景：整系数 Künneth 公式

虽然域系数简化了计算，但它们也丢失了关于挠子的宝贵拓扑信息。为了捕捉完整的图像，我们必须使用[整数环](@entry_id:181003) $\mathbb{Z}$ 作为系数。这使得[代数结构](@entry_id:137052)变得更加复杂，因为我们现在处理的是一般的[阿贝尔群](@entry_id:150284)，而不是[向量空间](@entry_id:151108)。其结果是 Künneth 公式的一个更精细的版本，通常表述为一个**短[正合序列](@entry_id:151503) (short exact sequence)**。

**Künneth 定理（整系数情形）**：对任意拓扑空间 $X$ 和 $Y$，对每个维度 $n$，存在一个自然的短[正合序列](@entry_id:151503)：
$$
0 \to \bigoplus_{i+j=n} H^i(X; \mathbb{Z}) \otimes_{\mathbb{Z}} H^j(Y; \mathbb{Z}) \to H^n(X \times Y; \mathbb{Z}) \to \bigoplus_{i+j=n+1} \text{Tor}_1^{\mathbb{Z}}(H^i(X; \mathbb{Z}), H^j(Y; \mathbb{Z})) \to 0
$$

这个序列比域系数版本复杂得多。让我们分解它的组成部分：
1.  **张量积项** $\bigoplus_{i+j=n} H^i(X; \mathbb{Z}) \otimes_{\mathbb{Z}} H^j(Y; \mathbb{Z})$：这类似于域系数版本，但现在是阿贝尔群的[张量积](@entry_id:140694)。需要注意的是，即使 $A$ 和 $B$ 都是[挠子群](@entry_id:139454)，它们的张量积也可能非零，例如 $\mathbb{Z}_m \otimes \mathbb{Z}_n \cong \mathbb{Z}_{\gcd(m,n)}$。此外，[挠子群](@entry_id:139454)与[自由群](@entry_id:151249)的张量积也可以是[挠子群](@entry_id:139454)，例如 $\mathbb{Z}_m \otimes \mathbb{Z} \cong \mathbb{Z}_m$。

2.  **Tor 项** $\bigoplus_{i+j=n+1} \text{Tor}_1^{\mathbb{Z}}(H^i(X; \mathbb{Z}), H^j(Y; \mathbb{Z}))$：这是全新的部分。**Tor 函子** ($\text{Tor}$ 是 Torsion 的缩写) 是从同调代数中产生的一个工具，它精确地量化了[张量积](@entry_id:140694)[函子](@entry_id:150427)在处理短[正合序列](@entry_id:151503)时的“非正合性”。直观上，它捕捉了由因[子空间](@entry_id:150286)中的挠子相互作用而产生的新挠子。一个关键的计算法则是 $\text{Tor}_1^{\mathbb{Z}}(\mathbb{Z}_m, \mathbb{Z}_n) \cong \mathbb{Z}_{\gcd(m,n)}$。值得注意的是，如果 $A$ 或 $B$ 是自由阿贝尔群（即无挠子），则 $\text{Tor}_1^{\mathbb{Z}}(A, B) = 0$。

3.  **短[正合序列](@entry_id:151503)**：这个序列告诉我们 $H^n(X \times Y; \mathbb{Z})$ 包含了来自[张量积](@entry_id:140694)项的贡献，并且它本身是 Tor 项的一个“扩张”。在许多情况下（例如，如果 Tor 项是[自由群](@entry_id:151249)，这在这里不常见），这个序列会**分裂 (split)**，意味着 $H^n(X \times Y; \mathbb{Z})$ 同构于张量积项与 Tor 项的[直和](@entry_id:156782)。虽然这种分裂不是自然的，但对于计算群的结构来说已经足够了：
    $$
    H^n(X \times Y; \mathbb{Z}) \cong \left( \bigoplus_{i+j=n} H^i \otimes H^j \right) \oplus \left( \bigoplus_{i+j=n+1} \text{Tor}(H^i, H^j) \right)
    $$

**示例：挠子从何而来？**
乘积空间中的挠子可以有两个来源：继承自因[子空间](@entry_id:150286)的挠子（通过张量积项），或由挠子相互作用产生的新挠子（通过 Tor 项）。
考虑空间 $\mathbb{R}P^2 \times S^2$ [@problem_id:1686240]。我们有 $H^2(\mathbb{R}P^2; \mathbb{Z}) \cong \mathbb{Z}_2$ 和 $H^2(S^2; \mathbb{Z}) \cong \mathbb{Z}$。
-   计算 $H^2(\mathbb{R}P^2 \times S^2; \mathbb{Z})$：[张量积](@entry_id:140694)项为 $(H^0 \otimes H^2) \oplus (H^1 \otimes H^1) \oplus (H^2 \otimes H^0) \cong (\mathbb{Z} \otimes \mathbb{Z}) \oplus (0 \otimes 0) \oplus (\mathbb{Z}_2 \otimes \mathbb{Z}) \cong \mathbb{Z} \oplus \mathbb{Z}_2$。Tor 项则涉及 $i+j=3$ 的维数组合，由于 $H^1$ 或 $H^3$ 至少有一个为零，且 $\text{Tor}(\mathbb{Z}_2, \mathbb{Z})=0$，所以 Tor 项为零。因此 $H^2(\mathbb{R}P^2 \times S^2; \mathbb{Z}) \cong \mathbb{Z} \oplus \mathbb{Z}_2$。这里的 $\mathbb{Z}_2$ 挠子部分直接来自 $H^2(\mathbb{R}P^2)$。
-   计算 $H^4(\mathbb{R}P^2 \times S^2; \mathbb{Z})$：[张量积](@entry_id:140694)项为 $H^2(\mathbb{R}P^2) \otimes H^2(S^2) \cong \mathbb{Z}_2 \otimes \mathbb{Z} \cong \mathbb{Z}_2$。Tor 项为零。所以 $H^4(\mathbb{R}P^2 \times S^2; \mathbb{Z}) \cong \mathbb{Z}_2$。

**示例：Tor 项在行动**
为了看到 Tor 项如何产生新的挠子，我们必须选择因[子空间](@entry_id:150286)，使其挠子能在正确的维度上相互作用。一个绝佳的例子是两个三维**[透镜空间](@entry_id:274705) (Lens space)** 的乘积，如 $L(p,1) \times L(q,1)$，其中 $p,q$ 是素数 [@problem_id:1686243]。已知 $H^2(L(k,1);\mathbb{Z}) \cong \mathbb{Z}_k$。我们来计算 $H^3(L(p,1) \times L(q,1); \mathbb{Z})$ 的挠子[子群](@entry_id:146164)。
-   **[张量积](@entry_id:140694)部分** $\bigoplus_{i+j=3} H^i \otimes H^j$ 的贡献是 $(H^0 \otimes H^3) \oplus (H^3 \otimes H^0) \cong \mathbb{Z} \oplus \mathbb{Z}$，这是[无挠的](@entry_id:161664)。
-   **Tor 部分** $\bigoplus_{i+j=4} \text{Tor}(H^i, H^j)$ 的唯一可能非零项是 $\text{Tor}(H^2, H^2) = \text{Tor}(\mathbb{Z}_p, \mathbb{Z}_q)$。
因此，$H^3$ 的整个挠子[子群](@entry_id:146164)就是 $\text{Tor}(\mathbb{Z}_p, \mathbb{Z}_q) \cong \mathbb{Z}_{\gcd(p,q)}$。
现在考虑两种情况：
1.  如果 $p, q$ 是不同的素数，$\gcd(p,q)=1$，[挠子群](@entry_id:139454)为 $\mathbb{Z}_1 = \{0\}$，是平凡群。
2.  如果 $p=q$，$\gcd(p,p)=p$，[挠子群](@entry_id:139454)为 $\mathbb{Z}_p$。
这个例子戏剧性地展示了 Tor 项的本质：它检测并量化了不同因[子空间](@entry_id:150286)的挠子结构之间的“共振”。

我们还应注意到，这些看似抽象的公式构成了代数拓扑工具箱中一个自洽的系统。例如，人们可以先使用同调的 Künneth 公式计算 $H_*(\mathbb{R}P^2 \times S^1; \mathbb{Z})$，然后应用泛系数定理得到 $H^*(\mathbb{R}P^2 \times S^1; \mathbb{Z})$ [@problem_id:1686244]。其计算结果与直接应用[上同调](@entry_id:160558)的 Künneth 公式得到的结果完全一致，这验证了这些理论的内在和谐性。

### 环结构：上同调作为分次环

Künneth 公式最强大的版本揭示了乘积空间[上同调](@entry_id:160558)的**环结构 (ring structure)**，该结构由**杯积 (cup product)** $\cup$ 赋予。域系数的 Künneth 公式实际上是一个**分次代数 (graded algebra)** 的同构：

$$
H^*(X \times Y; F) \cong H^*(X; F) \otimes_F H^*(Y; F)
$$

这里的[乘法规则](@entry_id:197368)由**叉积 (cross product)** 定义。对于 $u \in H^i(X; F)$ 和 $v \in H^j(Y; F)$，它们的叉积 $u \times v \in H^{i+j}(X \times Y; F)$ 定义为 $u \times v = \pi_X^*(u) \cup \pi_Y^*(v)$，其中 $\pi_X$ 和 $\pi_Y$ 是到 $X$ 和 $Y$ 的投影。[张量积](@entry_id:140694)环的[乘法规则](@entry_id:197368)是 $(a \otimes b) \cdot (c \otimes d) = (-1)^{|b||c|} (a \cup c) \otimes (b \cup d)$，其中 $|b|$ 是 $b$ 的维度。

**示例：一个[外代数](@entry_id:201164)**
考虑空间 $S^1 \times S^3$ 的有理[上同调环](@entry_id:160158) [@problem_id:1686220]。我们知道 $H^*(S^1; \mathbb{Q})$ 是由一个1次生成元 $a$ 生成的[外代数](@entry_id:201164) $\Lambda_{\mathbb{Q}}(a) = \mathbb{Q}[a]/(a^2)$。类似地，$H^*(S^3; \mathbb{Q})$ 是由一个3次生成元 $b$ 生成的[外代数](@entry_id:201164) $\Lambda_{\mathbb{Q}}(b) = \mathbb{Q}[b]/(b^2)$。
因此，乘[积空间](@entry_id:151693)的环结构是：
$$
H^*(S^1 \times S^3; \mathbb{Q}) \cong H^*(S^1; \mathbb{Q}) \otimes_{\mathbb{Q}} H^*(S^3; \mathbb{Q}) \cong \Lambda_{\mathbb{Q}}(a) \otimes_{\mathbb{Q}} \Lambda_{\mathbb{Q}}(b) \cong \Lambda_{\mathbb{Q}}(a,b)
$$
这是一个由1次生成元 $a$ 和3次生成元 $b$ 生成的[外代数](@entry_id:201164)，其关系为 $a^2=0, b^2=0$ 和 $ab = -ba$。重要的是，乘积 $a \cup b$ 是 $H^4(S^1 \times S^3; \mathbb{Q})$ 中一个非零的元素，这表明并非所有正维数[上同调类](@entry_id:263961)的[杯积](@entry_id:159554)都为零。

对于整系数，当 Tor 项消失时（例如，当其中一个因[子空间](@entry_id:150286)的所有[上同调群](@entry_id:142450)都是自由阿贝尔群时），类似的[环同构](@entry_id:147982)也成立。

**示例：带挠子的整[上同调环](@entry_id:160158)**
考虑 $X = \mathbb{R}P^2 \times S^1$ 的整[上同调环](@entry_id:160158) [@problem_id:1686249]。$H^*(S^1; \mathbb{Z})$ 的所有群都是自由的（$\mathbb{Z}$ 或 0），所以 Künneth 短[正合序列](@entry_id:151503)中的所有 Tor 项都为零。这使得加性分裂成为一个[环同构](@entry_id:147982)：
$$
H^*(\mathbb{R}P^2 \times S^1; \mathbb{Z}) \cong H^*(\mathbb{R}P^2; \mathbb{Z}) \otimes_{\mathbb{Z}} H^*(S^1; \mathbb{Z})
$$
$H^*(\mathbb{R}P^2; \mathbb{Z})$ 由生成元 $w \in H^2$ 描述，关系为 $w^2=0$ 和 $2w=0$。$H^*(S^1; \mathbb{Z})$ 由生成元 $u \in H^1$ 描述，关系为 $u^2=0$。将它们张量起来，我们得到乘[积空间](@entry_id:151693)的环结构由两个生成元 $u$ (1次) 和 $w$ (2次) 及其关系决定：
$$
H^*(\mathbb{R}P^2 \times S^1; \mathbb{Z}) \cong \mathbb{Z}[u, w] / (u^2, w^2, 2w)
$$
这个简洁的表示法完美地捕捉了乘积空间的加性群结构和[乘性](@entry_id:187940)[杯积](@entry_id:159554)结构。

**逆向应用：分解环结构**
Künneth [环同构](@entry_id:147982)也可以被逆向使用。假设我们知道乘[积空间](@entry_id:151693) $X \times Y$ 的有理[上同调环](@entry_id:160158)，我们能推断出 $X$ 和 $Y$ 的[上同调环](@entry_id:160158)是什么样的吗？[@problem_id:1686242]
例如，如果 $H^*(X \times Y; \mathbb{Q}) \cong \Lambda_{\mathbb{Q}}(\alpha_1, \alpha_3, \alpha_5)$，一个由奇数次生成元构成的[外代数](@entry_id:201164)。通过分析代数的“不可分解元”空间，可以证明 $H^*(X; \mathbb{Q})$ 和 $H^*(Y; \mathbb{Q})$ 本身也必须是[外代数](@entry_id:201164)，并且它们的生成元集合构成了 $\{\alpha_1, \alpha_3, \alpha_5\}$ 的一个划分。因此，可能的情况包括 (忽略顺序)：
1.  $H^*(X; \mathbb{Q}) \cong \mathbb{Q}$ (平凡代数) 且 $H^*(Y; \mathbb{Q}) \cong \Lambda_{\mathbb{Q}}(\alpha_1, \alpha_3, \alpha_5)$。
2.  $H^*(X; \mathbb{Q}) \cong \Lambda_{\mathbb{Q}}(\alpha_1)$ 且 $H^*(Y; \mathbb{Q}) \cong \Lambda_{\mathbb{Q}}(\alpha_3, \alpha_5)$。
3.  $H^*(X; \mathbb{Q}) \cong \Lambda_{\mathbb{Q}}(\alpha_3)$ 且 $H^*(Y; \mathbb{Q}) \cong \Lambda_{\mathbb{Q}}(\alpha_1, \alpha_5)$。
4.  $H^*(X; \mathbb{Q}) \cong \Lambda_{\mathbb{Q}}(\alpha_5)$ 且 $H^*(Y; \mathbb{Q}) \cong \Lambda_{\mathbb{Q}}(\alpha_1, \alpha_3)$。
这展示了 Künneth 公式作为分析空间拓扑结构的一个深刻的结构性工具的威力。

### 适用范围与局限性

最后，至关重要的是要明确 Künneth 公式的适用边界。此公式是关于**拓扑积 (topological product)** $X \times Y$ 的一个定理。它**不**适用于更一般的**纤维丛 (fiber bundle)**。

一个纤维丛也是由一个“底空间” $B$ 和一个“纤维” $F$ 构建起来的，但其局部结构是 $U \times F$（其中 $U$ 是 $B$ 的一个开集），而全局结构可能是“扭曲的”。$X \times Y$ 是最简单的一种纤维丛，称为**平凡丛 (trivial bundle)**。

为了看清这一点，我们比较两个都是以 $S^2$ 为底、以 $S^1$ 为纤维的三维流形 [@problem_id:1686252]：
1.  **平凡丛**： $X_1 = S^2 \times S^1$。
2.  **非平凡丛**： $X_2 = T_1S^2$，即 $S^2$ 的单位切丛。这是一个[流形](@entry_id:153038)，它[同胚](@entry_id:146933)于三维[实射影空间](@entry_id:149094) $\mathbb{R}P^3$。

它们的 $\mathbb{Z}_2$ 系数[上同调环](@entry_id:160158)截然不同：
-   根据 Künneth 定理，$H^*(S^2 \times S^1; \mathbb{Z}_2) \cong H^*(S^2; \mathbb{Z}_2) \otimes H^*(S^1; \mathbb{Z}_2) \cong \mathbb{Z}_2[\alpha, \beta]/(\alpha^3, \beta^2)$，其中 $|\alpha|=2, |\beta|=1$。
-   而对于 $\mathbb{R}P^3$，其 $\mathbb{Z}_2$ [上同调环](@entry_id:160158)是熟知的结果：$H^*(\mathbb{R}P^3; \mathbb{Z}_2) \cong \mathbb{Z}_2[\gamma]/(\gamma^4)$，其中 $|\gamma|=1$。

这两个环的加性结构不同（例如，$X_1$ 的[贝蒂数](@entry_id:153109)序列是 1,1,1,1，而 $X_2$ 的是 1,1,1,1，但这是在 $\mathbb{Z}_2$ 系数下，他们的整系数上同调群不同），[乘性](@entry_id:187940)结构也完全不同。这清晰地表明，Künneth 公式不能应用于非平凡丛。处理一般[纤维丛](@entry_id:159565)的[上同调](@entry_id:160558)需要一个更强大、更精细的工具，即 **Leray-Serre [谱序列](@entry_id:158626) (Leray-Serre spectral sequence)**，这将是后续章节的主题。

总之，Künneth 公式是一座桥梁，它将简单空间的知识转化为对由它们构建的乘积空间的理解。通过调整系数并仔细处理 Tor 项和环结构，它为我们提供了一个强大而精确的计算框架，同时也界定了其自身应用的边界，为我们探索更广阔的拓扑世界指明了方向。