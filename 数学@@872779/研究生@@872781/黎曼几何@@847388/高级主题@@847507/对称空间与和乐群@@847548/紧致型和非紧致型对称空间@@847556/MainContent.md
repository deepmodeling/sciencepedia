## 引言
[黎曼对称空间](@entry_id:193796)在现代微分几何中占据着核心地位，它们既是具有完美对称性的几何典范，又是连接[李群论](@entry_id:204663)、拓扑学与分析学的关键桥梁。尽管许多基础几何对象，如[欧氏空间](@entry_id:138052)、球面和[双曲空间](@entry_id:268092)，都属于[对称空间](@entry_id:181790)，但缺乏一个统一的理论框架来理解它们共同的深层结构和性质，这构成了一个知识上的挑战。本文旨在填补这一空白，为读者提供一个关于[对称空间](@entry_id:181790)理论的系统性介绍。

本文将分为三个章节，引导读者逐步深入这一优美的领域。在“原理与机制”一章中，我们将建立对称空间的几何与代数基础，阐明其曲率特性，并介绍其核心的分类法——紧致型、非紧致型与欧氏型。接下来的“应用与[交叉](@entry_id:147634)学科联系”一章，将展示这些抽象理论如何应用于具体的几何问题，如曲率计算、子[流形分类](@entry_id:636935)，并揭示其在拓扑学、[谱理论](@entry_id:275351)和刚性现象中的深刻影响。最后，通过“动手实践”部分，读者将有机会运用所学知识，解决与[对称空间](@entry_id:181790)结构相关的具体计算问题，从而巩固和深化理解。

## 原理与机制

在介绍性章节对[黎曼对称空间](@entry_id:193796)的基本概念有了初步了解后，本章将深入探讨其内在的原理和结构性机制。我们将从其几何与代数定义出发，揭示其[曲率张量](@entry_id:181383)的核心性质，并阐明局部与全局对称性之间的关键区别。最后，我们将详细阐述[对称空间](@entry_id:181790)著名的三分法——紧致型、非紧致型和欧氏型，并通过典范对偶性和具体实例来揭示其深刻的内在联系和[精细结构](@entry_id:140861)。

### 基本定义：几何与代数视角

对称空间可以通过两种等价但视角不同的方式来定义：一种是直观的几何方法，通过点对称操作；另一种是更具结构性的代数方法，通过李群和李代数。

#### 几何定义：测地对称

从几何学的角度看，一个连通的黎曼流形 $(M,g)$ 被称为 **[黎曼对称空间](@entry_id:193796) (Riemannian symmetric space)**，如果[对流](@entry_id:141806)形上的每一点 $p \in M$，都存在一个全局的[等距同构](@entry_id:273188) $s_p: M \to M$，满足以下两个条件：
1.  $p$ 是 $s_p$ 的一个[不动点](@entry_id:156394)，即 $s_p(p) = p$。
2.  $s_p$ 在点 $p$ 的[微分](@entry_id:158718)是负单位映射，即 $(ds_p)_p = -\mathrm{Id}_{T_pM}$。

这个映射 $s_p$ 被称为在点 $p$ 的 **测地对称 (geodesic symmetry)**。第二个条件意味着对称操作会反转所有经过点 $p$ 的[测地线](@entry_id:269969)的方向。更精确地说，如果 $\gamma(t) = \exp_p(tv)$ 是一条经过 $p$ 的[测地线](@entry_id:269969)，其中 $v \in T_pM$，那么对称操作 $s_p$ 的作用就是将其映射到“反向”的[测地线](@entry_id:269969)上：

$$ s_p(\exp_p(v)) = \exp_p(-v) $$

此等式在指数映射有定义的范围内成立。这个性质直观地描绘了[流形](@entry_id:153038)在每一点附近如何“对称”地反射。[@problem_id:2991881]

最简单的例子是 $n$ 维欧氏空间 $(\mathbb{R}^n, g_{\mathrm{eucl}})$。对于任意点 $x \in \mathbb{R}^n$，我们可以定义一个点反射映射 $s_x(y) = 2x - y$。不难验证，$s_x$ 是一个保持欧氏距离的[等距同构](@entry_id:273188)，它固定了点 $x$，并且其[微分](@entry_id:158718)恒为 $-\mathrm{Id}$。因此，$\mathbb{R}^n$ 是一个[黎曼对称空间](@entry_id:193796)。[@problem_id:2991873] 其他基本例子还包括标[准球](@entry_id:169696)面 $S^n$ 和[双曲空间](@entry_id:268092) $\mathbb{H}^n$。

#### 代数定义：对称偶

[黎曼对称空间](@entry_id:193796)具有高度的齐性，这意味着它们总可以被表述为[齐性空间](@entry_id:271488)。具体而言，任何一个[黎曼对称空间](@entry_id:193796) $M$ 都可以表示为 $M \cong G/K$ 的形式，其中 $G$ 是 $M$ 的[等距同构](@entry_id:273188)群 $\mathrm{Isom}(M)$ 的单位[连通分支](@entry_id:141881)，而 $K$ 是某一点 $o \in M$ 的[迷向子群](@entry_id:200360) (isotropy subgroup)。这种[代数结构](@entry_id:137052)为我们提供了更强大的分析工具。

这个结构的核心是一个 **对合[自同构](@entry_id:155390) (involutive automorphism)** $\sigma: G \to G$，即一个满足 $\sigma^2 = \mathrm{id}$ 的李群自同构。[迷向子群](@entry_id:200360) $K$ 与 $\sigma$ 的[不动点](@entry_id:156394)集 $G^\sigma = \{g \in G : \sigma(g) = g\}$ 密切相关，通常 $K$ 是 $G^\sigma$ 的一个开[子群](@entry_id:146164)。这样的一对 $(G,K)$ 被称为一个 **对称偶 (symmetric pair)**。[@problem_id:2991870]

这个[自同构](@entry_id:155390)在[李代数](@entry_id:137954)层面引起了关键的分解。令 $\mathfrak{g}$ 和 $\mathfrak{k}$ 分别为 $G$ 和 $K$ 的李代数，$\sigma$ 在单位元处的[微分](@entry_id:158718) $d\sigma_e: \mathfrak{g} \to \mathfrak{g}$ 是一个[李代数](@entry_id:137954)[自同构](@entry_id:155390)，且其平方为单位映射。因此，$d\sigma_e$ 的[特征值](@entry_id:154894)只能是 $+1$ 和 $-1$。这导致了 $\mathfrak{g}$ 的一个[典范分解](@entry_id:634116)：

$$ \mathfrak{g} = \mathfrak{k} \oplus \mathfrak{p} $$

其中 $\mathfrak{k} = \{X \in \mathfrak{g} : d\sigma_e(X) = X\}$ 是 $+1$ 特征空间，而 $\mathfrak{p} = \{X \in \mathfrak{g} : d\sigma_e(X) = -X\}$ 是 $-1$ [特征空间](@entry_id:638014)。由于 $d\sigma_e$ 是一个李代数自同构，它保持[李括号](@entry_id:636461)运算，这导出了这三个[子空间](@entry_id:150286)之间标志性的 **括号关系**：

$$ [\mathfrak{k}, \mathfrak{k}] \subset \mathfrak{k}, \quad [\mathfrak{k}, \mathfrak{p}] \subset \mathfrak{p}, \quad [\mathfrak{p}, \mathfrak{p}] \subset \mathfrak{k} $$

第一个关系说明 $\mathfrak{k}$ 本身是一个李子代数，这与它是[子群](@entry_id:146164) $K$ 的[李代数](@entry_id:137954)的事实相符。第二个关系至关重要，它说明 $\mathfrak{p}$ 在 $K$ 的伴随作用下是不变的。第三个关系则是对称空间曲率性质的代数根源。[@problem_id:2991870]

#### [迷向表示](@entry_id:184529)与切空间

代数定义与几何定义通过切空间联系起来。在[齐性空间](@entry_id:271488) $M=G/K$ 的基点 $o=eK$ 处，[切空间](@entry_id:199137) $T_oM$ 可以被自然地等同于[商空间](@entry_id:274314) $\mathfrak{g}/\mathfrak{k}$。借助[典范分解](@entry_id:634116) $\mathfrak{g} = \mathfrak{k} \oplus \mathfrak{p}$，我们得到一个更具体的等同关系：

$$ T_oM \cong \mathfrak{p} $$

[迷向子群](@entry_id:200360) $K$ 作用在 $M$ 上并保持基点 $o$ 不动，因此它诱导了在切空间 $T_oM$ 上的一个[线性表示](@entry_id:139970)，称为 **[迷向表示](@entry_id:184529) (isotropy representation)** $\iota: K \to \mathrm{GL}(T_oM)$。利用上述等同关系 $T_oM \cong \mathfrak{p}$，我们可以精确地刻画这个表示。对于任意 $k \in K$ 和 $X \in \mathfrak{p}$，[迷向表示](@entry_id:184529)的作用等价于 $K$ 在 $\mathfrak{p}$ 上的伴随作用：

$$ \iota(k) \text{ 对应于 } \mathrm{Ad}(k)|_{\mathfrak{p}} $$

括号关系 $[\mathfrak{k}, \mathfrak{p}] \subset \mathfrak{p}$ 保证了 $\mathfrak{p}$ 确实是 $K$ 的伴随作用下的一个[不变子空间](@entry_id:152829)，即 $\mathrm{Ad}(k)X \in \mathfrak{p}$ 对所有 $k \in K, X \in \mathfrak{p}$ 成立。此外，对称空间上的 $G$-不变[黎曼度量](@entry_id:754359)在点 $o$ 诱导了 $\mathfrak{p}$ 上的一个 $\mathrm{Ad}(K)$-不变[内积](@entry_id:158127)。这意味着[迷向表示](@entry_id:184529)是一个正交表示，即 $\iota(K)$ 是[正交群](@entry_id:152531) $O(T_oM)$ 的一个[子群](@entry_id:146164)。[@problem_id:2991911] [@problem_id:2991870]

### 曲率与局部-全局之分

[对称空间](@entry_id:181790)的几何性质由其曲率张量 $R$ 主宰。一个深刻的结果是，对称性这一几何概念等价于一个简洁的解析条件。

#### 平行曲率张量: $\nabla R = 0$

[黎曼对称空间](@entry_id:193796)的一个根本性质是其曲率张量是 **协变常数 (covariantly constant)** 或平行的，即其[协变微分](@entry_id:263981)为零：

$$ \nabla R \equiv 0 $$

我们可以通过对称性定义来推导这个结论。由于 $s_p$ 是一个[等距同构](@entry_id:273188)，它保持曲率张量 $R$ 和[Levi-Civita联络](@entry_id:161107) $\nabla$ 不变。因此，它也保持 $\nabla R$ 不变。在点 $p$，利用 $s_p$ 的性质，我们有 $s_p(p)=p$ 和 $(ds_p)_p = -\mathrm{Id}$。将 $s_p$ 作用于张量 $\nabla R$ 在点 $p$ 的分量 $(\nabla_V R)(X,Y)Z$，我们得到：

$$ -(\nabla_V R)_p(X,Y)Z = (\nabla_{-V} R)_p(-X,-Y)(-Z) $$

利用张量的[多重线性](@entry_id:151506)性质，右侧等于 $(\nabla_V R)_p(X,Y)Z$。因此我们有 $-T=T$，其中 $T$ 是张量分量，这意味着 $T=0$。由于 $p,V,X,Y,Z$ 是任意的，我们必然有 $\nabla R \equiv 0$。[@problem_id:2991881]

反过来，$\nabla R=0$ 这个条件足以保证[流形](@entry_id:153038)是 **局部对称 (locally symmetric)** 的。这意味着在每一点 $p$ 的一个邻域内，测地对称 $s_p(\exp_p(v)) = \exp_p(-v)$ 是一个[局部等距](@entry_id:158618)同构。$\nabla R=0$ 保证了沿[测地线](@entry_id:269969)的平行移动能够保持曲率信息不变，这正是证明 $s_p$ 保持度量的关键。[@problem_id:2991905]

#### 局部对称与全局对称

局部对称（$\nabla R = 0$）并不自动保证全局对称。要将每一点的局部对称性 $s_p$ 提升为全局定义的[等距同构](@entry_id:273188)，[流形](@entry_id:153038)需要满足额外的拓扑和完备性条件。这一经典结果由 **Cartan-Ambrose-Hicks 定理** 给出：

> 一个连通、完备且单连通的局部对称[黎曼流形](@entry_id:261160)是一个（全局）[黎曼对称空间](@entry_id:193796)。

换言之，**完备性** 和 **[单连通性](@entry_id:189103)** 是将局部结构“粘贴”成全局结构所需的胶水。[@problem_id:2991881] [@problem_id:2991905]

缺乏这些条件会导致重要的反例。最典型的例子是紧致的双曲[曲面](@entry_id:267450)。考虑双曲平面 $\mathbb{H}^2$，这是一个单连通、完备的对称空间，其曲率为常数 $-1$。取其一个[无挠的](@entry_id:161664)、余紧的离散等距[子群](@entry_id:146164) $\Gamma$（一个[Fuchsian群](@entry_id:261064)），则商空间 $M = \Gamma \backslash \mathbb{H}^2$ 是一个亏格 $g \ge 2$ 的闭[曲面](@entry_id:267450)。由于[商映射](@entry_id:140877)是[局部等距](@entry_id:158618)， $M$ 继承了 $\mathbb{H}^2$ 的局部几何，因此其曲率也为常数 $-1$，这意味着 $\nabla R = 0$，$M$ 是一个[局部对称空间](@entry_id:637873)。然而，$M$ 并不是全局对称的。一个关键的阻碍是，一个具有[负曲率](@entry_id:159335)的[紧致流形](@entry_id:158804)的[等距同构](@entry_id:273188)群必定是有限群。而一个非平凡的全局[对称空间](@entry_id:181790)，由于其齐性，必然拥有一个维数大于零的李群作为其[等距同构](@entry_id:273188)群。因此，$M$ 上的局部测地对称无法扩展为[全局等距](@entry_id:184658)。[@problem_id:2991903]

相比之下，某些非单连通的[局部对称空间](@entry_id:637873)仍然可以是全局对称的。例如，[平坦环面](@entry_id:261129) $T^n = \mathbb{R}^n / \mathbb{Z}^n$ 和具有标准度量的[实射影空间](@entry_id:149094) $\mathbb{R}P^n = S^n / \{\pm \mathrm{Id}\}$ 都是全局对称空间。其原因是，其覆盖空间（分别是 $\mathbb{R}^n$ 和 $S^n$）上的测地对称可以完美地“下降”到[商空间](@entry_id:274314)上，因为它们与离散群 $\mathbb{Z}^n$ 和 $\{\pm \mathrm{Id}\}$ 的作用是相容的。[@problem_id:2991903]

### 三分法：紧致型、非紧致型与欧氏型

基于曲率性质和相关的李群结构，单连通的[黎曼对称空间](@entry_id:193796)可以被唯一地分解为三类基本构建块的乘积：欧氏型、紧致型和非紧致型。

#### 分类标准

假设 $(M,g)$ 是一个单连通、不可约（不能写成两个非平凡黎曼流形的乘积）的[对称空间](@entry_id:181790)。

*   **欧氏型 (Euclidean Type)**: 这类空间的曲率张量恒为零 ($R \equiv 0$)。唯一的例子就是[欧氏空间](@entry_id:138052) $\mathbb{R}^n$。其[等距同构](@entry_id:273188)群 $G = E(n) = O(n) \ltimes \mathbb{R}^n$ 的[李代数](@entry_id:137954) $\mathfrak{e}(n) = \mathfrak{o}(n) \ltimes \mathbb{R}^n$ 包含一个阿贝尔理想（平移部分），因此它不是半单的。作为对称偶，$M \cong G_0/K$ 其中 $G_0 = \mathrm{SO}(n) \ltimes \mathbb{R}^n$, $K=\mathrm{SO}(n)$。对应的[李代数分解](@entry_id:185623)为 $\mathfrak{g} = \mathfrak{so}(n) \oplus \mathbb{R}^n = \mathfrak{k} \oplus \mathfrak{p}$，其关键特征是 $[\mathfrak{p}, \mathfrak{p}] = 0$，这正是曲率为零的代数体现。[@problem_id:2991873]

*   **紧致型 (Compact Type)**: 这类空间作为[流形](@entry_id:153038)是紧致的。其等价特征包括：
    *   [截面曲率](@entry_id:159738)处处非负 ($K \ge 0$)。
    *   [等距同构](@entry_id:273188)群的单位[连通分支](@entry_id:141881) $G$ 是一个紧致半单[李群](@entry_id:137659)。
    *   $G$ 的李代数 $\mathfrak{g}$ 上的[基灵型](@entry_id:161046) (Killing form) $B$ 是负定的。
    在代数层面，$\mathfrak{g} = \mathfrak{k} \oplus \mathfrak{p}$ 的结构中，$\mathfrak{p}$ 上的 $\mathrm{Ad}(K)$-不变[内积](@entry_id:158127)可以由 $-B$ 的限制给出，因为 $-B$ 是正定的。[@problem_id:2991902] [@problem_id:2991870]

*   **非紧致型 (Noncompact Type)**: 这类空间作为[流形](@entry_id:153038)是非紧致的。其等价特征包括：
    *   [截面曲率](@entry_id:159738)处处非正 ($K \le 0$)。
    *   [等距同构](@entry_id:273188)群的单位[连通分支](@entry_id:141881) $G$ 是一个非紧致半单李群，且[迷向子群](@entry_id:200360) $K$ 是其[极大紧子群](@entry_id:203454)。
    *   [李代数](@entry_id:137954) $\mathfrak{g}$ 上的[基灵型](@entry_id:161046) $B$ 在 $\mathfrak{k}$ 上是负定的，在 $\mathfrak{p}$ 上是正定的。这种分解被称为 **[嘉当分解](@entry_id:182528) (Cartan decomposition)**。
    $\mathfrak{p}$ 上的 $\mathrm{Ad}(K)$-不变[内积](@entry_id:158127)可以直接由 $B$ 的限制给出。[@problem_id:2991902] [@problem_id:2991870]

值得注意的是，除非[流形](@entry_id:153038)的秩为1，否则紧致型空间的曲率通常只是非负（允许存在零曲率平面），而非处处严格为正。同样，非紧致型空间的曲率通常只是非正，而非处处严格为负。[@problem_id:2991902]

#### 紧致与非紧致的对偶性

紧致型和非紧致型[对称空间](@entry_id:181790)之间存在一种深刻的 **对偶性 (duality)**，称为 **嘉当对偶 (Cartan duality)**。从代数上讲，给定一个非紧致型[半单李代数](@entry_id:190073)及其[嘉当分解](@entry_id:182528) $\mathfrak{g} = \mathfrak{k} \oplus \mathfrak{p}$，我们可以构造其 **紧致对偶 (compact dual)** [李代数](@entry_id:137954)：

$$ \mathfrak{g}^* = \mathfrak{k} \oplus i\mathfrak{p} $$

这是一个紧致[李代数](@entry_id:137954)，而 $(\mathfrak{g}^*, \mathfrak{k})$ 构成了一个对应于紧致型[对称空间](@entry_id:181790)的对称偶。这个过程是可逆的。这种对偶性在几何层面表现为曲率符号的翻转。

**例1：[常曲率空间](@entry_id:161841)**
最基本的对偶例子是球面 $S^n$ 和双曲空间 $\mathbb{H}^n$。设 $S^n$ 的曲率为常数 $+k$ ($k>0$)，$\mathbb{H}^n$ 的曲率为 $-k$。它们分别是紧致型和非紧致型[对称空间](@entry_id:181790)的典范。
*   它们的[曲率张量](@entry_id:181383) $R$ 作为 (1,3)-张量，通过切空间的[等距同构](@entry_id:273188) $I: T_pS^n \to T_q\mathbb{H}^n$ 联系起来，满足 $I(R^{S^n}(X,Y)Z) = -R^{\mathbb{H}^n}(IX,IY)IZ$。
*   它们的[里奇张量](@entry_id:159336)满足 $\mathrm{Ric}^{S^n} = -\mathrm{Ric}^{\mathbb{H}^n}$。
*   它们的数量曲率也满足 $S_{S^n} = -S_{\mathbb{H}^n}$。
*   然而，作为 (0,4)-张量，它们的范数是相等的：$\|R^{S^n}\| = \|R^{\mathbb{H}^n}\|$，因为范数依赖于曲率的平方 $k^2$。[@problem_id:2991882]

**例2：一个非恒定曲率的对偶偶**
考虑非紧致对称空间 $M_{\mathrm{nc}} = SL(n,\mathbb{R})/SO(n)$。其[李代数分解](@entry_id:185623)为 $\mathfrak{sl}(n,\mathbb{R}) = \mathfrak{so}(n) \oplus \mathfrak{p}$，其中 $\mathfrak{p}$ 是所有迹为零的[实对称矩阵](@entry_id:192806)构成的空间。其截面曲率处处非正。

它的紧致[对偶空间](@entry_id:146945)是 $M_{\mathrm{c}} = SU(n)/SO(n)$。其李代数是 $\mathfrak{su}(n)$，可以被构造为 $\mathfrak{su}(n) = \mathfrak{so}(n) \oplus i\mathfrak{p}$。这里的 $i\mathfrak{p}$ 是所有迹为零的纯虚对称矩阵（即对称且反埃尔米特的矩阵）构成的空间。$SU(n)/SO(n)$ 的[截面曲率](@entry_id:159738)处处非负。

对偶性在曲率公式中清晰地体现出来。对称空间的[曲率张量](@entry_id:181383)在基点处可由[李括号](@entry_id:636461)计算：$R(X,Y)Z = -[[X,Y],Z]$，其中 $X,Y,Z \in \mathfrak{p}$。
*   对于 $M_{\mathrm{nc}}$，截面曲率 $K_{\mathrm{nc}}(X,Y) = -\langle [[X,Y],Y], X\rangle_{\mathfrak{p}} = -B_{\mathrm{nc}}([X,Y], [X,Y])$。由于 $[X,Y] \in \mathfrak{k}$ 且 $B_{\mathrm{nc}}$ 在 $\mathfrak{k}$ 上负定，故 $K_{\mathrm{nc}} \le 0$。
*   对于 $M_{\mathrm{c}}$，[截面曲率](@entry_id:159738) $K_{\mathrm{c}}(iX,iY) = -\langle [[iX,iY],iY], iX\rangle_{\mathfrak{p}^*} = -(-B_{\mathrm{c}}([[iX,iY],iY],iX))$。利用 $[iX,iY]_{\mathfrak{g}^*} = -[X,Y]_{\mathfrak{g}}$ 的事实，以及 $B_{\mathrm{c}}$ 在 $\mathfrak{k}$ 上负定，可以推导出 $K_{\mathrm{c}} \ge 0$。本质上，曲率符号的翻转源于[代数结构](@entry_id:137052)中 $i^2=-1$ 的出现以及度量范数的选择（在紧致情况下使用 $-B$）。[@problem_id:2991909]

#### 非紧致空间的[精细结构](@entry_id:140861)：[限制根系](@entry_id:193805)

非紧致型[对称空间](@entry_id:181790)具有更丰富的结构，可以通过 **[限制根系](@entry_id:193805) (restricted root system)** 来描述。这个理论类似于[半单李代数](@entry_id:190073)的根系理论，但适用于[对称空间](@entry_id:181790)的分解。

设 $\mathfrak{g}=\mathfrak{k}\oplus\mathfrak{p}$ 是一个非紧致型对称空间的[李代数分解](@entry_id:185623)。我们选取 $\mathfrak{p}$ 中的一个 **极大阿贝尔[子空间](@entry_id:150286)** $\mathfrak{a}$。由于 $\mathfrak{a}$ 中的所有元素相互交换，算子族 $\{\mathrm{ad}(H) : H \in \mathfrak{a}\}$ 是一个作用在 $\mathfrak{g}$ 上的可交换的线性算子族。进一步可以证明，它们都是可[对角化](@entry_id:147016)的。因此，$\mathfrak{g}$ 可以被分解为这个算子族的公共特征[子空间之和](@entry_id:180324)：

$$ \mathfrak{g} = \mathfrak{g}_0 \oplus \bigoplus_{\alpha \in \Sigma} \mathfrak{g}_\alpha $$

其中，对于每个[线性泛函](@entry_id:276136) $\alpha \in \mathfrak{a}^*$（称为 **限制根 (restricted root)**），对应的 **根空间** $\mathfrak{g}_\alpha$ 定义为：
$$ \mathfrak{g}_\alpha = \{X \in \mathfrak{g} : [H,X] = \alpha(H)X \text{ for all } H \in \mathfrak{a}\} $$
$\Sigma$ 是所有使得 $\mathfrak{g}_\alpha \neq \{0\}$ 的非零[线性泛函](@entry_id:276136) $\alpha$ 的集合。零根空间 $\mathfrak{g}_0$ 是 $\mathfrak{a}$ 在 $\mathfrak{g}$ 中的[中心化子](@entry_id:146604) $Z_{\mathfrak{g}}(\mathfrak{a})$。

这个分解具有优美的结构性质：
*   $[\mathfrak{g}_\alpha, \mathfrak{g}_\beta] \subset \mathfrak{g}_{\alpha+\beta}$。
*   嘉当对合 $\theta$ 将 $\mathfrak{g}_\alpha$ 映射到 $\mathfrak{g}_{-\alpha}$。
*   集合 $\Sigma$ 构成了一个（可能非约化的）[根系](@entry_id:198970)。

这个限制[根空间分解](@entry_id:185263)是理解非紧致[对称空间](@entry_id:181790)几何学（如[测地线](@entry_id:269969)的渐近行为、[散射理论](@entry_id:143476)）和[表示论](@entry_id:137998)的基石。[@problem_id:2991898]

最后，值得一提的是，对称空间中的[测地线](@entry_id:269969)具有特别简单的形式。通过基点 $o=eK$ 的所有[测地线](@entry_id:269969)都是形如 $\gamma(t) = \exp(tX) \cdot o$ 的[轨道](@entry_id:137151)，其中 $\exp$ 是李[群的指数](@entry_id:145655)映射，而向量 $X$ 必须取自[子空间](@entry_id:150286) $\mathfrak{p}$。反之，每一个 $X \in \mathfrak{p}$ 都对应着一条通过基点的[测地线](@entry_id:269969)。[@problem_id:2991870] 这再次凸显了[李代数分解](@entry_id:185623) $\mathfrak{g}=\mathfrak{k}\oplus\mathfrak{p}$ 在连接代数与几何中的核心作用。