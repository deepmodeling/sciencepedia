## 引言
对称空间，作为[黎曼几何](@entry_id:160508)与李群理论交汇处的璀璨明珠，拥有着异常丰富且高度对称的结构。然而，其底层的半单李群结构往往错综复杂，使得直接研究其几何与分析性质变得极具挑战性。为了系统地剖析这些空间，数学家们发展出了一套强有力的代数工具，其中[嘉当分解](@entry_id:182528)与[岩泽分解](@entry_id:200501)居于核心地位。本文旨在深入探讨这两种分解，揭示它们如何将一个复杂的[李群](@entry_id:137659)拆解为更易于理解的紧致、阿贝尔和幂零部分，并由此揭示对称空间的深层奥秘。

在接下来的内容中，我们将分三步展开：
首先，在“原理与机制”一章，我们将深入研究嘉当与[岩泽分解](@entry_id:200501)的代数根源，从李代数的嘉当对合与[根空间分解](@entry_id:185263)出发，理解它们如何生成[对称空间](@entry_id:181790)的[黎曼度量](@entry_id:754359)和[全局坐标系](@entry_id:171029)。
其次，在“应用与交叉学科联系”一章，我们将展示这些抽象分解在具体问题中的威力，探索它们如何用于描述[测地线](@entry_id:269969)、曲率、[渐近几何](@entry_id:635883)，以及它们在[调和分析](@entry_id:198768)、数论等领域的深刻应用。
最后，通过“动手实践”部分的精选习题，读者将有机会亲手计算和验证这些理论在具体例子中的表现，从而巩固和深化对这些核心概念的理解。

## 原理与机制

本章深入探讨了对称空间的代数与几何结构，重点介绍[嘉当分解](@entry_id:182528)与[岩泽分解](@entry_id:200501)。这些分解不仅为研究半单[李群](@entry_id:137659)提供了基本的结构定理，也为理解相关[黎曼对称空间](@entry_id:193796)的几何学（如曲率、[测地线](@entry_id:269969)和[坐标系](@entry_id:156346)）奠定了基础。我们将从李代数的[嘉当分解](@entry_id:182528)出发，逐步构建对称空间的黎曼度量，并探索其全局分解（如极分解、$KAK$ 分解和[岩泽分解](@entry_id:200501)）的几何意义。

### [嘉当分解](@entry_id:182528)

[嘉当分解](@entry_id:182528)是理解[半单李代数](@entry_id:190073)和相关对称空间结构的起点。它源于一种称为**嘉当对合**的特殊自同构。

设 $\mathfrak{g}$ 是一个实[半单李代数](@entry_id:190073)。$\mathfrak{g}$ 上的一个**嘉当对合**是一个[李代数](@entry_id:137954)自同构 $\theta: \mathfrak{g} \to \mathfrak{g}$，满足 $\theta^2 = \mathrm{Id}$，并且由它定义的[双线性形式](@entry_id:746794) $B_\theta(X, Y) = -B(X, \theta Y)$ 是正定的，其中 $B$ 是 $\mathfrak{g}$ 的[基灵型](@entry_id:161046)（Killing form）。

由于 $\theta$ 的平方是恒等映射，其[特征值](@entry_id:154894)只能是 $+1$ 和 $-1$。这导出了 $\mathfrak{g}$ 的一个[直和分解](@entry_id:263004)，即**[嘉当分解](@entry_id:182528)**：
$$ \mathfrak{g} = \mathfrak{k} \oplus \mathfrak{p} $$
其中 $\mathfrak{k} = \{X \in \mathfrak{g} \mid \theta(X) = X\}$ 是 $+1$ [特征空间](@entry_id:638014)，而 $\mathfrak{p} = \{X \in \mathfrak{g} \mid \theta(X) = -X\}$ 是 $-1$ [特征空间](@entry_id:638014)。

这个分解具有深刻的结构性质。首先，[基灵型](@entry_id:161046) $B$ 在这两个[子空间](@entry_id:150286)上表现出明确的定号性：对于非紧型[半单李代数](@entry_id:190073)（即其对应的李群非紧），$B$ 在 $\mathfrak{k}$ 上是负定的，在 $\mathfrak{p}$ 上是正定的。其次，这两个[子空间](@entry_id:150286)之间的[李括号](@entry_id:636461)遵循特定的规则：
$$ [\mathfrak{k}, \mathfrak{k}] \subseteq \mathfrak{k}, \quad [\mathfrak{k}, \mathfrak{p}] \subseteq \mathfrak{p}, \quad [\mathfrak{p}, \mathfrak{p}] \subseteq \mathfrak{k} $$
第一条关系表明 $\mathfrak{k}$ 是 $\mathfrak{g}$ 的一个子代数。第二条关系意味着 $\mathfrak{p}$ 在 $\mathfrak{k}$ 的伴随作用下是不变的，即 $\mathfrak{p}$ 是一个 $\mathfrak{k}$-模。第三条关系则揭示了 $\mathfrak{p}$ 中的元素如何相互作用以产生 $\mathfrak{k}$ 中的元素，这对理解对称空间的曲率至关重要。

### 从李代数到[对称空间](@entry_id:181790)

[嘉当分解](@entry_id:182528)的几何意义通过将其提升到[李群](@entry_id:137659)层面而变得清晰。设 $G$ 是一个具有李代数 $\mathfrak{g}$ 的连通半单[李群](@entry_id:137659)。

与李代数[子空间](@entry_id:150286) $\mathfrak{k}$ 对应，$G$ 中存在一个解析[子群](@entry_id:146164) $K$，其[李代数](@entry_id:137954)为 $\mathfrak{k}$。一个核心结论是，$K$ 是 $G$ 的一个**[极大紧子群](@entry_id:203454)**，并且任何两个[极大紧子群](@entry_id:203454)在 $G$ 中都是共轭的。这个结论的证明过程极具启发性 [@problem_id:2969862]：
首先，可以证明 $K$ 是紧的。由于 $\theta$ 的定义，[内积](@entry_id:158127) $\langle X, Y \rangle_\theta = -B(X, \theta Y)$ 在 $\mathfrak{g}$ 上是正定的。可以验证这个[内积](@entry_id:158127)在 $K$ 的伴随作用下是不变的，即 $\mathrm{Ad}(K)$ 是[正交群](@entry_id:152531) $O(\mathfrak{g}, \langle \cdot, \cdot \rangle_\theta)$ 的一个[子群](@entry_id:146164)。由于[正交群](@entry_id:152531)是紧的，其闭[子群](@entry_id:146164) $\mathrm{Ad}(K)$ 也是紧的。又因为 $G$ 的中心有限，从 $K$ 到 $\mathrm{Ad}(K)$ 的映射是一个有限叶覆盖，因此 $K$ 本身也是紧的。
其次，为了证明 $K$ 的极[大性](@entry_id:268856)，可以考虑 $G$ 中任意一个紧[子群](@entry_id:146164) $C$。通过在 $C$ 上对[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle_\theta$ 进行平均（使用[哈尔测度](@entry_id:142417)），可以构造一个新的 $\mathrm{Ad}(C)$-不变[内积](@entry_id:158127)。这个新[内积](@entry_id:158127)又定义了一个新的嘉当对合 $\theta'$，其对应的[极大紧子群](@entry_id:203454) $K'$ 包含了 $C$。由于所有嘉当对合都是通过[内自同构](@entry_id:142697)共轭的，所以 $K'$ 与 $K$ 共轭。这表明 $G$ 的任何紧[子群](@entry_id:146164)都包含于 $K$ 的某个[共轭子群](@entry_id:140560)中，从而确立了 $K$ 的极[大性](@entry_id:268856)以及它在共轭意义下的唯一性。

有了[极大紧子群](@entry_id:203454) $K$，我们便可以定义**[黎曼对称空间](@entry_id:193796)**（非紧型）为[商空间](@entry_id:274314) $M = G/K$。这是一个[齐性空间](@entry_id:271488)， $G$ 通过左平移作用于其上。为了赋予 $M$ 黎曼流形的结构，我们需要在其[切空间](@entry_id:199137)上定义一个 $G$-不变的[黎曼度量](@entry_id:754359)。这个过程完美地展示了[代数结构](@entry_id:137052)如何生成几何结构 [@problem_id:2969888]：
1.  **在原点定义[内积](@entry_id:158127)**：首先考虑基点 $o = eK \in M$ 的[切空间](@entry_id:199137) $T_o M$。这个[切空间](@entry_id:199137)可以自然地通过商[映射的[微](@entry_id:269524)分](@entry_id:158718)与[向量空间](@entry_id:151108) $\mathfrak{p}$ 等同，即 $T_o M \cong \mathfrak{g}/\mathfrak{k} \cong \mathfrak{p}$。我们在 $\mathfrak{p}$ 上定义一个[内积](@entry_id:158127)，利用[基灵型](@entry_id:161046) $B$ 在 $\mathfrak{p}$ 上的[正定性](@entry_id:149643)。对于任意 $X, Y \in \mathfrak{p}$，定义：
    $$ \langle X, Y \rangle_o := B(X, Y) $$
    由于 $B$ 在 $\mathfrak{p}$ 上是对称正定的，这是一个合法的[内积](@entry_id:158127)。

2.  **推广到整个空间**：为了在 $M$ 的任意点 $p = gK$ 定义度量，我们利用 $G$ 的[传递作用](@entry_id:154215)。对于任意切向量 $v, w \in T_{gK} M$，我们通过左平移 $L_{g^{-1}}$ 将它们[拉回](@entry_id:160816)到原点 $o$，然后在 $T_o M$ 中计算它们的[内积](@entry_id:158127)：
    $$ \langle v, w \rangle_{gK} := \langle d(L_{g^{-1}})v, d(L_{g^{-1}})w \rangle_o $$
    这个定义的自洽性（即不依赖于[陪集](@entry_id:147145)代表元 $g$ 的选取）依赖于[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle_o$ 的 $\mathrm{Ad}(K)$-[不变性](@entry_id:140168)。幸运的是，[基灵型](@entry_id:161046) $B$ 是 $\mathrm{Ad}(G)$-不变的，因此也是 $\mathrm{Ad}(K)$-不变的。同时，[子空间](@entry_id:150286) $\mathfrak{p}$ 也在 $\mathrm{Ad}(K)$ 的作用下保持不变。这两个事实保证了度量是良定义的。

3.  **$G$-不变性**：通过这种方式构造的度量，根据其定义，自然地在 $G$ 的左平移作用下保持不变，即 $G$ 的作用是等距作用。

此外，如果 $K$ 在 $\mathfrak{p}$ 上的伴随表示是不可约的（这种空间称为**迷向不可约的**），那么根据[舒尔引理](@entry_id:136779)（Schur's Lemma），$\mathfrak{p}$ 上任何 $\mathrm{Ad}(K)$-不变的[内积](@entry_id:158127)都必然是 $B|_{\mathfrak{p}}$ 的一个正常数倍。这意味着 $M=G/K$ 上的任何 $G$-不变黎曼度量在这种情况下本质上是唯一的（相差一个常数倍） [@problem_id:2969888]。

### 全局分解：从极分解到 $KAK$ 分解

代数层面的[嘉当分解](@entry_id:182528) $\mathfrak{g} = \mathfrak{k} \oplus \mathfrak{p}$ 对应着群层面上的**极分解**（或称[嘉当分解](@entry_id:182528)）：$G = K \exp(\mathfrak{p})$。这表示 $G$ 中的每个元素 $g$ 都可以唯一地写成一个紧部分 $k \in K$ 和一个“径向”部分 $p \in P = \exp(\mathfrak{p})$ 的乘积 $g=kp$。

这个抽象的分解在 $G = SL(n, \mathbb{R})$ 的例子中变得非常具体和直观 [@problem_id:2969898]。对于 $SL(n, \mathbb{R})$，标准的嘉当对合是 $\theta(X) = -X^\top$。
-   $+1$ [特征空间](@entry_id:638014) $\mathfrak{k}$ 是所有迹为零的[反对称矩阵](@entry_id:155998)，即 $\mathfrak{so}(n)$。对应的[极大紧子群](@entry_id:203454) $K$ 就是[特殊正交群](@entry_id:146418) $SO(n)$。
-   $-1$ [特征空间](@entry_id:638014) $\mathfrak{p}$ 是所有迹为零的对称矩阵。
-   集合 $P = \exp(\mathfrak{p})$ 恰好是所有[行列式](@entry_id:142978)为 $1$ 的正定对称矩阵。

因此，$SL(n, \mathbb{R})$ 的极分解 $G=KP$ 就是我们熟悉的[矩阵分解](@entry_id:139760)：任何一个[行列式](@entry_id:142978)为 $1$ 的实矩阵 $g$ 都可以唯一地分解为一个[旋转矩阵](@entry_id:140302) $k \in SO(n)$ 和一个[行列式](@entry_id:142978)为 $1$ 的正定[对称矩阵](@entry_id:143130) $p$ 的乘积。

进一步，我们可以对 $P$ 中的元素进行分解。这是一个比极分解更精细的结构，即 **$KAK$ 分解**。设 $\mathfrak{a}$ 是 $\mathfrak{p}$ 中的一个极大阿贝尔[子空间](@entry_id:150286)（即 $\mathfrak{a}$ 中的元素相互对易，且 $\mathfrak{a}$ 在此性质下是极大的），并令 $A = \exp(\mathfrak{a})$。$KAK$ 分解定理断言，每个 $g \in G$ 都可以写成 $g=k_1 a k_2$ 的形式，其中 $k_1, k_2 \in K$，$a \in A$。

再次以 $G=SL(n, \mathbb{R})$ 为例 [@problem_id:2969863]，我们可以选择 $\mathfrak{a}$ 为所有迹为零的对角矩阵。那么 $A$ 就是所有对角线上元素为正且乘积为 $1$ 的[对角矩阵](@entry_id:637782)。
这个 $KAK$ 分解与矩阵的**[奇异值分解 (SVD)](@entry_id:172448)** 密切相关。任何矩阵 $g \in SL(n, \mathbb{R})$ 都有 SVD 分解 $g=U\Sigma V^\top$，其中 $U, V \in SO(n)$，$\Sigma$ 是对角矩阵，其对角元（奇异值）为正。
-   $g$ 的极分解 $g=kp$ 中的因子 $p$ 与[奇异值](@entry_id:152907)直接相关：$p = \sqrt{g^\top g}$。通过 SVD，我们发现 $g^\top g = (U\Sigma V^\top)^\top (U\Sigma V^\top) = V \Sigma^2 V^\top$。因此，$p = V \Sigma V^\top$。这表明 $p$ 的[特征值](@entry_id:154894)就是 $g$ 的[奇异值](@entry_id:152907) [@problem_id:2969898]。
-   将 $p$ 对角化 $p=k_2^{-1} a k_2$ (其中 $k_2 \in SO(n)$, $a$ 是对角阵)，我们得到 $g = kp = k(k_2^{-1} a k_2) = (kk_2^{-1}) a k_2$。令 $k_1 = kk_2^{-1}$，这就得到了 $g=k_1 a k_2$ 的形式。这里的 $a$ 是一个[对角矩阵](@entry_id:637782)，其对角元正是 $g$ 的[奇异值](@entry_id:152907)。

$KAK$ 分解中的 $a$ 并非唯一。其不确定性由**外尔群 (Weyl Group)** $W = N_K(A)/Z_K(A)$ 描述，其中 $N_K(A)$ 和 $Z_K(A)$ 分别是 $A$ 在 $K$ 中的[正规化子](@entry_id:145708)和[中心化子](@entry_id:146604)。两个元素 $a, a' \in A$ 给出相同的双边陪集 $KaK = Ka'K$ 当且仅当它们位于同一个外尔群[轨道](@entry_id:137151)上 [@problem_id:2969844]。
对于 $SL(n, \mathbb{R})$，可以计算出 $N_K(\mathfrak{a})$ 是所有[行列式](@entry_id:142978)为 1 的符号[置换矩阵](@entry_id:136841)，而 $Z_K(\mathfrak{a})$ 是对角线上元素为 $\pm 1$ 且[行列式](@entry_id:142978)为 1 的[对角矩阵](@entry_id:637782)。其[商群](@entry_id:145113) $W$ 同构于 $n$ 次对称群 $S_n$ [@problem_id:2969846]。$S_n$ 的作用就是[置换](@entry_id:136432) $a$ 的对角元（即奇异值）。

为了获得唯一性，我们选择一个**正外尔室 (Positive Weyl Chamber)** $A^+$ 作为 $A$ 的一个基本区域。对于 $SL(n, \mathbb{R})$，一个通常的选择是 $A^+ = \{ \mathrm{diag}(a_1, \dots, a_n) \mid a_1 \ge a_2 \ge \dots \ge a_n > 0, \prod a_i = 1 \}$。$KAK$ 分解定理的精细形式是：每个 $g \in G$ 都可以分解为 $g = k_1 a k_2$，其中 $k_1, k_2 \in K$，且 $a \in A^+$ 是**唯一**的。这个唯一性是通过要求[奇异值](@entry_id:152907)按非增顺序[排列](@entry_id:136432)来实现的 [@problem_id:2969863] [@problem_id:2969844]。

### [岩泽分解](@entry_id:200501)及其代[数基](@entry_id:634389)础

[岩泽分解](@entry_id:200501)提供了另一种看待半单[李群](@entry_id:137659)全局结构的视角。它依赖于比[嘉当分解](@entry_id:182528)更精细的代数构造，即[根空间分解](@entry_id:185263)。

首先，我们引入[对称空间](@entry_id:181790)的**秩**的概念。几何上，一个[流形](@entry_id:153038)中的**平坦子流形**是一个曲率恒为零的测地完备子流形。对称空间 $M$ 的**秩** $r(M)$ 定义为 $M$ 中极大平坦子流形的维数。代数上，这个几何概念等价于极大阿贝尔[子空间](@entry_id:150286) $\mathfrak{a} \subset \mathfrak{p}$ 的维数，即 $r(M) = \dim(\mathfrak{a})$。这是因为 $M=G/K$ 中的平坦[子流形](@entry_id:159439)恰好对应于 $\mathfrak{p}$ 的阿贝尔[子空间](@entry_id:150286)，极大平坦[子流形](@entry_id:159439)则对应于 $\mathfrak{p}$ 的极大阿贝尔[子空间](@entry_id:150286) $\mathfrak{a}$ [@problem_id:2969857]。曲率公式 $K(X,Y) \propto -\|[X,Y]\|^2$ 清楚地表明，当且仅当 $X,Y$ 对易时，它们张成的平面的[截面曲率](@entry_id:159738)为零。

给定极大阿贝尔[子空间](@entry_id:150286) $\mathfrak{a} \subset \mathfrak{p}$，我们考察 $\mathrm{ad}(\mathfrak{a})$ 在 $\mathfrak{g}$ 上的作用。由于 $\mathfrak{a}$ 中所有元素对易，算子族 $\{\mathrm{ad}(H) \mid H \in \mathfrak{a}\}$ 是一个可交换的[对称算子](@entry_id:272489)族。根据谱定理，$\mathfrak{g}$ 可以分解为这些算子的公共特征[子空间](@entry_id:150286)（称为**根空间**）的[直和](@entry_id:156782) [@problem_id:2969868]：
$$ \mathfrak{g} = \mathfrak{g}_0 \oplus \bigoplus_{\alpha \in \Sigma} \mathfrak{g}_\alpha $$
这里，$\alpha \in \mathfrak{a}^* \setminus \{0\}$ 是一个非零[线性泛函](@entry_id:276136)，称为**限制根**，$\Sigma$ 是所有限制根的集合。根空间定义为：
$$ \mathfrak{g}_\alpha = \{ X \in \mathfrak{g} \mid [H, X] = \alpha(H)X \text{ for all } H \in \mathfrak{a} \} $$
而 $\mathfrak{g}_0$ 是 $\mathfrak{a}$ 在 $\mathfrak{g}$ 中的中心化子。可以证明 $\mathfrak{g}_0 = C_\mathfrak{k}(\mathfrak{a}) \oplus \mathfrak{a}$，并且[根系](@entry_id:198970) $\Sigma$ 张成了[对偶空间](@entry_id:146945) $\mathfrak{a}^*$。

通过选择一个[正根](@entry_id:199264)系 $\Sigma^+ \subset \Sigma$，我们可以定义一个[幂零李代数](@entry_id:192104) $\mathfrak{n} = \bigoplus_{\alpha \in \Sigma^+} \mathfrak{g}_\alpha$。这导出了李代数的**[岩泽分解](@entry_id:200501)**：
$$ \mathfrak{g} = \mathfrak{k} \oplus \mathfrak{a} \oplus \mathfrak{n} $$
这是一个[向量空间](@entry_id:151108)的[直和分解](@entry_id:263004)，但与[嘉当分解](@entry_id:182528)不同，$\mathfrak{a} \oplus \mathfrak{n}$ 通常不是 $\mathfrak{g}$ 的子代数。

在群的层面上，我们有相应的**[岩泽分解](@entry_id:200501)** $G=KAN$，其中 $A=\exp(\mathfrak{a})$，$N=\exp(\mathfrak{n})$。这个分解的一个关键特性是它的**唯一性**：每个 $g \in G$ 都可以**唯一地**写成 $g=kan$ 的形式，其中 $k \in K, a \in A, n \in N$。这种唯一性与 $KAK$ 分解中需要引入外尔群和外尔室来解决模糊性的情况形成对比。[岩泽分解](@entry_id:200501)本身依赖于[正根](@entry_id:199264)系的选择，但一旦选定，分解就是唯一的 [@problem_id:2969844]。

### 对偶性与解析延拓

对称空间理论中最深刻和优美的思想之一是紧致型与非紧致型空间之间的**对偶性**。

从一个[非紧型对称空间](@entry_id:636486)的李代数 $\mathfrak{g} = \mathfrak{k} \oplus \mathfrak{p}$ 出发，我们可以构造其**紧致对偶**李代数 [@problem_id:2969848]。这个构造在 $\mathfrak{g}$ 的[复化](@entry_id:260775) $\mathfrak{g}_{\mathbb{C}} = \mathfrak{g} \otimes \mathbb{C}$ 中进行。我们定义一个新的实子代数：
$$ \mathfrak{u} = \mathfrak{k} \oplus i\mathfrak{p} $$
其中 $i$ 是虚数单位。可以验证 $\mathfrak{u}$ 在李括号下是封闭的，因为 $[\mathfrak{k}, i\mathfrak{p}] \subset i\mathfrak{p}$ 和 $[i\mathfrak{p}, i\mathfrak{p}] = -[\mathfrak{p},\mathfrak{p}] \subset \mathfrak{k}$。更重要的是，$\mathfrak{g}$ 的[基灵型](@entry_id:161046) $B$ 在 $\mathfrak{p}$ 上是正定的，在 $i\mathfrak{p}$ 上则是负定的（因为 $B(iX, iY) = -B(X,Y)$）。由于 $B$ 在 $\mathfrak{k}$ 上本已是负定，它在整个 $\mathfrak{u}$ 上都是负定的。根据[嘉当判据](@entry_id:191878)，一个[半单李代数](@entry_id:190073)的[基灵型](@entry_id:161046)是负定的当且仅当其对应的[李群](@entry_id:137659)是紧的。因此，$\mathfrak{u}$ 是一个[紧致李群](@entry_id:146703) $U$ 的[李代数](@entry_id:137954)，而 $X_c = U/K$ 就是 $X=G/K$ 的紧致对偶对称空间。

这种对偶性不仅是代数上的，它在几何和分析上也有深远的影响。许多在[非紧空间](@entry_id:273664) $X$ 上的分析问题，可以通过到紧致[对偶空间](@entry_id:146945) $X_c$ 的**解析延拓**来解决。这个延拓的核心是通过映射 $H \mapsto iH$ 将 $\mathfrak{a}$ 与其在 $\mathfrak{u}$ 中的对偶伙伴 $i\mathfrak{a}$ 等同起来 [@problem_id:2969890]。

例如，考虑 $K$-不变函数上的[拉普拉斯-贝尔特拉米算子](@entry_id:267002) $\Delta$。其径向部分 $R$ 在 $\mathfrak{a}$ 上是一个二阶微分算子。对于[非紧空间](@entry_id:273664) $X$，其径向算子 $R_{\mathrm{nc}}$ 的一阶项系数包含 $\coth(\alpha(H))$ 这样的[双曲函数](@entry_id:165175)。对于紧致空间 $X_c$，其径向算子 $R_{\mathrm{c}}$ 的一阶项系数则包含 $\cot(\alpha(H))$ 这样的三角函数。这两个算子通过解析延拓联系在一起。若令 $C^*$ 表示由 $H \mapsto iH$ 引起的[拉回](@entry_id:160816)作用，则有算子恒等式：
$$ C^* R_{\mathrm{nc}} (C^*)^{-1} = -R_{\mathrm{c}} $$
这意味着，在[非紧空间](@entry_id:273664)上的[拉普拉斯算子](@entry_id:146319)，通过解析延拓到虚宗量，就（在差一个负号的意义下）变成了紧致[对偶空间](@entry_id:146945)上的[拉普拉斯算子](@entry_id:146319) [@problem_id:2969890]。

这种对偶性也体现在球函数（即 $K$-双不变的[拉普拉斯算子](@entry_id:146319)[特征函数](@entry_id:186820)）上。[非紧空间](@entry_id:273664) $X$ 上的球函数 $\varphi_\lambda$ 和[紧致空间](@entry_id:155073) $X_c$ 上的球函数 $\psi_\Lambda$ 可以通过类似的解析延拓关系联系起来。这种关系是[调和分析](@entry_id:198768)中一个强有力的工具。

最后，[对称空间](@entry_id:181790)的分解理论也与[调和分析](@entry_id:198768)中的一个核心结果——**Harish-Chandra 同构**——紧密相连。该同构建立了 $X$ 上所有 $G$-不变微分算子所构成的代数 $\mathbb{D}(X)$ 与 $\mathfrak{a}$ 上 $W$-[不变多项式](@entry_id:266937)代数 $S(\mathfrak{a})^W$ 之间的一个同构。这意味着 $\mathbb{D}(X)$ 的联合[特征值](@entry_id:154894)（谱）由外尔群 $W$ 在对偶空间 $\mathfrak{a}^*$ 上的[轨道](@entry_id:137151)来[参数化](@entry_id:272587)。这再次凸显了外尔群 $W$ 和外尔室 $A^+$ 在消[解模糊](@entry_id:271900)性、提供唯一[参数化](@entry_id:272587)方面所扮演的核心角色，无论是对于几何分解（$KAK$）还是对于[谱理论](@entry_id:275351) [@problem_id:2969844]。