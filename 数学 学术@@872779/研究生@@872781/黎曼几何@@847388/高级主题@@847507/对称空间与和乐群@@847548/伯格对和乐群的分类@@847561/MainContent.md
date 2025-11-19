## 引言
在[黎曼几何](@entry_id:160508)中，和乐群（Holonomy Group）是连接[流形](@entry_id:153038)局部曲率与[全局几何](@entry_id:197506)及拓扑的根本性工具。它通过考察向量沿闭合路径平行移动后的变化，精确地量化了空间的弯曲方式。一个核心问题随之产生：哪些群可以作为[黎曼流形](@entry_id:261160)的[和乐群](@entry_id:191471)出现，它们又如何决定[流形](@entry_id:153038)的几何特性？对这一问题的深刻回答，最终形成了现代几何学的基石之一——贝尔杰分类（Berger Classification），它为不可约黎曼流形的和乐群提供了一份惊人地简洁的清单，并由此建立了一个理解和组织“[特殊几何](@entry_id:194564)”的强大框架。

本文旨在系统地阐述贝尔杰分类的理论基础及其深远影响。全文分为三个核心章节。
*   在第一章 **「原理与机制」** 中，我们将奠定理论基础，从平行移动和曲率出发定义和乐群，通过[安布罗斯-辛格定理](@entry_id:198517)揭示其与曲率的代数联系，并借助[de Rham分解定理](@entry_id:195682)将问题简化，最终引出贝尔杰的分类列表。
*   第二章 **「应用与[交叉](@entry_id:147634)学科联系」** 将展示该分类的强大威力，探索[特殊和乐群](@entry_id:158889)如何催生出[凯勒流形](@entry_id:161192)、[卡拉比-丘流形](@entry_id:159253)和G2[流形](@entry_id:153038)等关键几何结构，并阐明其在爱因斯坦度量、[代数几何](@entry_id:156300)和理论物理中的应用。
*   最后的 **「动手实践」** 章节将通过一系列具体问题，帮助读者在实践中巩固对这些抽象概念的理解。

通过这三个章节的引导，读者将深刻体会到，[和乐群](@entry_id:191471)这一看似纯粹的[代数结构](@entry_id:137052)，如何成为一把钥匙，解锁了黎曼几何乃至更广阔数学与物理领域的丰富世界。

## 原理与机制

在黎曼几何中，[联络与曲率](@entry_id:158520)是描述[流形](@entry_id:153038)局部几何性质的核心工具。然而，一个自然的问题是：[流形](@entry_id:153038)的局部几何信息在多大程度上决定了其全局结构？[和乐群](@entry_id:191471)（Holonomy Group）理论为此问题提供了深刻的回答。和乐群通过平行移动将[切空间](@entry_id:199137)中的向量沿闭合回路移动一周，从而捕捉了空间的弯曲程度。本章将系统地阐述[黎曼和](@entry_id:137667)乐群的基本原理与机制，揭示它如何成为连接局部曲率与[全局几何](@entry_id:197506)的桥梁，并最终引向贝尔杰（Berger）对和乐群的精妙分类。

### [和乐群](@entry_id:191471)：通过平行移动捕捉曲率

#### 定义与基本性质

让我们从平行移动的概念开始。在黎曼流形 $(M,g)$ 上，给定其上的列维-奇维塔（Levi-Civita）联络 $\nabla$，对于一条分段光滑的曲线 $\gamma: [0, 1] \to M$，一个沿 $\gamma$ 的向量场 $V(t)$ 如果满足[协变导数](@entry_id:152476)方程 $\nabla_{\dot{\gamma}(t)} V(t) = 0$，则称其为**[平行向量场](@entry_id:636129)**。对于任意起点 $p = \gamma(0)$ 处的切向量 $v \in T_p M$，存在唯一一个沿 $\gamma$ 的[平行向量场](@entry_id:636129) $V(t)$ 使得 $V(0) = v$。**平行移动**映射 $P_\gamma: T_{\gamma(0)}M \to T_{\gamma(1)}M$ 定义为 $P_\gamma(v) = V(1)$。这是一个[线性同构](@entry_id:270529)。

现在，我们特别关注那些起点和终点重合的曲线，即基点为 $p$ 的**回路**（loop）。对于任何一个基点为 $p$ 的分段光滑回路 $\sigma$，平行移动映射 $P_\sigma$ 是一个从 $T_p M$ 到自身的线性自同构，即 $P_\sigma \in \mathrm{GL}(T_p M)$。所有这些由 $p$ 点的所有可能回路生成的线性变换，在映射复合运算下构成一个群，这个群被称为在点 $p$ 的**和乐群**，记为 $\mathrm{Hol}_p(\nabla)$。它自然地是 $T_p M$ 上[一般线性群](@entry_id:141275) $\mathrm{GL}(T_p M)$ 的一个[子群](@entry_id:146164) [@problem_id:2968906]。

[黎曼和](@entry_id:137667)乐群有两个至关重要的性质，它们都源于列维-奇维塔联络的特殊性。

1.  **正交性**：列维-奇维塔联络是**度量相容的**（metric-compatible），即 $\nabla g = 0$。这意味着平行移动保持向量间的[内积](@entry_id:158127)。具体来说，对于沿回路 $\sigma$ 平行移动的任意两个向量 $u, v \in T_p M$，我们有 $g_p(P_\sigma(u), P_\sigma(v)) = g_p(u, v)$。这正是[正交变换](@entry_id:155650)的定义。因此，[和乐群](@entry_id:191471) $\mathrm{Hol}_p(g)$（我们用 $g$ 代替 $\nabla$ 以强调其对度量的依赖）必然是切空间 $(T_p M, g_p)$ 上[正交群](@entry_id:152531) $\mathrm{O}(T_p M)$ 的一个[子群](@entry_id:146164) [@problem_id:2968980]。

2.  **特殊正交性**：如果[流形](@entry_id:153038) $M$ 是**可定向的**（oriented），这意味着存在一个全局一致定义的体积形式 $\mathrm{vol}_g$。[列维-奇维塔联络](@entry_id:161107)的一个关键性质是它同样保持[体积形式](@entry_id:203000)不变，即 $\nabla (\mathrm{vol}_g) = 0$。因此，平行移动操作 $P_\sigma$ 必须保持在 $p$ 点的体积元不变。线性变换对[体积元](@entry_id:267802)的作用由其[行列式](@entry_id:142978)决定，保持[体积元](@entry_id:267802)不变意味着 $\det(P_\sigma) = 1$。结合正交性，这表明在可定向[黎曼流形](@entry_id:261160)上，[和乐群](@entry_id:191471)是[特殊正交群](@entry_id:146418) $\mathrm{SO}(T_p M)$ 的一个[子群](@entry_id:146164)，即 $\mathrm{Hol}_p(g) \subset \mathrm{SO}(n)$，其中 $n = \dim M$ [@problem_id:2968939]。其[李代数](@entry_id:137954) $\mathfrak{hol}_p(g)$ 因此是斜对称矩阵代数 $\mathfrak{so}(n)$ 的一个子代数。

#### [基点的无关性](@entry_id:273050)与[和乐群](@entry_id:191471)表示

和乐群的定义似乎依赖于基点 $p$ 的选择。然而，在连通[流形](@entry_id:153038)上，[和乐群](@entry_id:191471)的**[共轭类](@entry_id:143916)**是[独立于基点](@entry_id:273050)的。考虑[流形](@entry_id:153038)中任意两点 $p$ 和 $q$。由于[流形](@entry_id:153038)是连通的，存在一条从 $p$到 $q$ 的路径 $\gamma$。这条路径定义了一个平行移动同构 $P_\gamma: T_p M \to T_q M$。

对于 $\mathrm{Hol}_p(g)$ 中的任意元素 $h_p = P_\sigma$（其中 $\sigma$ 是一个在 $p$ 点的回路），我们可以构造一个在 $q$ 点的新回路 $\lambda = \gamma \cdot \sigma \cdot \gamma^{-1}$。沿此新回路的平行移动为 $P_\lambda = P_\gamma \circ P_\sigma \circ P_{\gamma^{-1}} = P_\gamma h_p P_\gamma^{-1}$。这表明 $P_\gamma \mathrm{Hol}_p(g) P_\gamma^{-1} \subseteq \mathrm{Hol}_q(g)$。反之亦然，我们可以证明 $\mathrm{Hol}_q(g) \subseteq P_\gamma \mathrm{Hol}_p(g) P_\gamma^{-1}$。因此，我们得到关系式 $\mathrm{Hol}_q(g) = P_\gamma \mathrm{Hol}_p(g) P_\gamma^{-1}$。这意味着不同点的和乐群在 $\mathrm{O}(n)$ 中是相互共轭的。虽然具体的同构 $P_\gamma$ 依赖于路径 $\gamma$，但群的抽象结构和其作为[矩阵群](@entry_id:137464)的共轭类在整个连通[流形](@entry_id:153038)上是不变的 [@problem_id:2968906]。

和乐群 $\mathrm{Hol}_p(g)$ 通过其在切空间 $T_p M$ 上的自然作用，定义了一个[线性表示](@entry_id:139970)，这被称为**和乐群表示**（holonomy representation）。这个表示的性质，例如它是否可约，蕴含了关于[流形](@entry_id:153038)几何结构的深刻信息 [@problem_id:2968956]。

### 拓扑的角色：[限制和乐群](@entry_id:637133)与[万有覆盖](@entry_id:151142)

#### [和乐群](@entry_id:191471)与[限制和乐群](@entry_id:637133)

[和乐群](@entry_id:191471)的定义包含了[流形](@entry_id:153038)上所有类型的回路，这使其不仅依赖于[流形](@entry_id:153038)的局部几何，也与[流形](@entry_id:153038)的全局拓扑性质（如“洞”的存在）有关。为了将几何效应与拓扑效应分离，我们引入**[限制和乐群](@entry_id:637133)**（restricted holonomy group）$\mathrm{Hol}_p^0(g)$。它定义为由所有**可缩回路**（contractible loops）在 $p$ 点产生的平行移动构成的[子群](@entry_id:146164) [@problem_id:2968956]。

一个基本事实是，[限制和乐群](@entry_id:637133) $\mathrm{Hol}_p^0(g)$ 正是[和乐群](@entry_id:191471) $\mathrm{Hol}_p(g)$ 作为李群的单位[连通分支](@entry_id:141881)。因此，$\mathrm{Hol}_p^0(g)$ 是 $\mathrm{Hol}_p(g)$ 的一个连通正规子群，[商群](@entry_id:145113) $\mathrm{Hol}_p(g) / \mathrm{Hol}_p^0(g)$ 是一个离散群。

这个商群与[流形](@entry_id:153038)的基本群 $\pi_1(M,p)$ 密切相关。存在一个自然、满的[群同态](@entry_id:140603) $\Phi: \pi_1(M,p) \to \mathrm{Hol}_p(g) / \mathrm{Hol}_p^0(g)$，它将一个回路的[同伦类](@entry_id:149365) $[\gamma]$ 映到由 $P_\gamma$ 代表的[陪集](@entry_id:147145) [@problem_id:2968911]。这个映射是良定义的，因为如果两个回路 $\gamma_1$ 和 $\gamma_2$ 是[同伦](@entry_id:139266)的，则复合回路 $\gamma_1 \cdot \gamma_2^{-1}$ 是可缩的，因此 $P_{\gamma_1 \cdot \gamma_2^{-1}} = P_{\gamma_1} \circ (P_{\gamma_2})^{-1} \in \mathrm{Hol}_p^0(g)$，这意味着 $P_{\gamma_1}$ 和 $P_{\gamma_2}$ 属于同一个陪集。

然而，需要强调的是，这个同态 $\Phi$ 通常**不是**一个同构。例如，对于标准的[平坦环面](@entry_id:261129) $T^n$，其[基本群](@entry_id:146111) $\pi_1(T^n,p) \cong \mathbb{Z}^n$ 非常大，但由于其曲率为零，平行移动与路径无关，任何回路的平行移动都是[恒等变换](@entry_id:264671)。因此其和乐群是平凡群 $\{\mathrm{Id}\}$，[商群](@entry_id:145113)也是平凡的。这表明非平凡的拓扑（非平凡的 $\pi_1$）不一定导致非平凡的[和乐群](@entry_id:191471)行为 [@problem_id:2968911]。

#### [万有覆盖](@entry_id:151142)与简化

处理[流形](@entry_id:153038)拓扑复杂性的一个标准方法是提升到其**[万有覆盖空间](@entry_id:154691)**（universal cover）。令 $\pi: \widetilde{M} \to M$ 为[万有覆盖](@entry_id:151142)映射，我们可以将度量 $g$ 提升为 $\widetilde{M}$ 上的度量 $\widetilde{g}$。由于 $\widetilde{M}$ 是单连通的，其上所有的回路都是可缩的。

这导致了一个关键的简化：$\widetilde{M}$ 的和乐群 $\mathrm{Hol}_{\widetilde{p}}(\widetilde{g})$（对于 $\pi(\widetilde{p})=p$）与 $M$ 的[限制和乐群](@entry_id:637133) $\mathrm{Hol}_p^0(g)$ 是同构的。这是因为 $\widetilde{M}$ 上的任意回路投影到 $M$ 上都是可缩回路，反之亦然。通过[微分](@entry_id:158718)映射 $d\pi_{\widetilde{p}}: T_{\widetilde{p}}\widetilde{M} \to T_p M$ 建立的切空间等同，平行移动算子也一一对应 [@problem_id:2968911]。

特别地，如果[流形](@entry_id:153038) $M$ 本身就是**单连通的**（simply connected），那么 $\pi_1(M,p)$ 是[平凡群](@entry_id:151996)。这意味着所有回路都是可缩的，因此 $\mathrm{Hol}_p(g) = \mathrm{Hol}_p^0(g)$。在这种情况下，和乐群本身就是一个连通[李群](@entry_id:137659)。这极大地简化了问题，并成为贝尔杰分类的一个核心假设 [@problem_id:2968911] [@problem_id:2968939]。

### 与曲率的联系：[安布罗斯-辛格定理](@entry_id:198517)

和乐群的概念似乎只与平行移动和回路有关，但它与黎曼曲率张量 $R$ 有着深刻的内在联系。直观上，曲率衡量了平行移动在无穷小尺度上的[路径依赖性](@entry_id:186326)。沿一个由向量 $X, Y$ 张成的无穷小平行四边形回路进行平行移动，一个向量 $V$ 的变化近似为 $-R(X,Y)V$。这暗示曲率张量应该“生成”和乐群。

这一直观想法被**[安布罗斯-辛格定理](@entry_id:198517)**（Ambrose-Singer Theorem）精确化。该定理指出，[和乐群](@entry_id:191471)的[李代数](@entry_id:137954) $\mathfrak{hol}_p(g)$ 是由所有[曲率算子](@entry_id:198006) $R_x(u,v)$（作用于 $T_x M$）沿着从 $p$ 到 $x$ 的所有路径 $\gamma$ 平行移回到 $T_p M$ 后生成的。即，
$$
\mathfrak{hol}_p(g) = \mathrm{span} \left\{ P_\gamma^{-1} R_x(u,v) P_\gamma \mid x \in M, u,v \in T_x M, \gamma \text{ is a path from } p \text{ to } x \right\}
$$
这个定理是连接[微分](@entry_id:158718)（曲率）和积分（和乐群）的关键环节 [@problem_id:2968956] [@problem_id:2968880]。

一个常见的误解是，$\mathfrak{hol}_p(g)$ 仅由在单一点 $p$ 的[曲率算子](@entry_id:198006) $\{R_p(u,v)\}$ 生成。这仅在一种特殊情况下成立，即当[流形](@entry_id:153038)是**[局部对称空间](@entry_id:637873)**（locally symmetric space）时，其[曲率张量](@entry_id:181383)是平行的（$\nabla R = 0$）[@problem_id:2968931]。对于一般的[黎曼流形](@entry_id:261160)，必须考虑所有点的曲率信息。

[安布罗斯-辛格定理](@entry_id:198517)本身对联络的要求非常宽泛，它适用于任何[切丛](@entry_id:161294)上的线性联络，不要求联络无挠（torsion-free）或度量相容。挠率 $T$ 的存在会改变曲率张量所满足的代数关系（如[比安基恒等式](@entry_id:261685)），从而间接影响和乐群代数，但它并不会作为独立的生成元加入到[和乐群](@entry_id:191471)代数中。贝尔杰分类之所以专注于[无挠的](@entry_id:161664)列维-奇维塔联络，是因为它在[黎曼几何](@entry_id:160508)的框架下是唯一且自然的选择 [@problem_id:2968879]。

### 和乐群的结构：分解与不可约性

#### de Rham 分解定理

[和乐群](@entry_id:191471)表示的性质反映了[流形](@entry_id:153038)的几何结构。一个关键问题是：和乐群表示是否**可约**（reducible）？一个表示是可约的，如果存在一个非平凡的真[子空间](@entry_id:150286) $V \subset T_p M$ 在所有[和乐群](@entry_id:191471)元素的作用下保持不变。

如果 $\mathrm{Hol}_p(g)$ 表示是可约的，那么[不变子空间](@entry_id:152829) $V$ 可以通过平行移动推广到整个[流形](@entry_id:153038)上，形成一个光滑的、平行的子丛 $E \subset TM$。其[正交补](@entry_id:149922) $E^\perp$ 同样也是一个平行子丛。

**de Rham 分解定理**（de Rham Decomposition Theorem）指出，对于一个单连通、完备的[黎曼流形](@entry_id:261160) $(M,g)$，其和乐群表示是可约的，当且仅当 $(M,g)$ 可以分解为一个黎曼乘[积流形](@entry_id:270208) $(M_1, g_1) \times \dots \times (M_k, g_k)$ [@problem_id:2968960] [@problem_id:2968914]。

这个分解的后果是显著的：乘[积流形](@entry_id:270208)的[和乐群](@entry_id:191471)是其因[子流形](@entry_id:159439)和乐[群的直积](@entry_id:143585)：
$$
\mathrm{Hol}_p(g) \cong \mathrm{Hol}_{p_1}(g_1) \times \dots \times \mathrm{Hol}_{p_k}(g_k)
$$
其中 $p=(p_1, \dots, p_k)$ 是基点。在李代数层面，这意味着 $\mathfrak{hol}_p(g) = \mathfrak{hol}_{p_1}(g_1) \oplus \dots \oplus \mathfrak{hol}_{p_k}(g_k)$。此外，每个因子 $M_i$ 的[和乐群](@entry_id:191471)表示是**不可约的**（irreducible），或者 $M_i$ 是一个平坦的欧氏空间（其[和乐群](@entry_id:191471)是平凡的）。

例如，考虑乘[积流形](@entry_id:270208) $S^2(a) \times S^3(b)$。其[和乐群](@entry_id:191471)代数是 $\mathfrak{hol}(S^2(a)) \oplus \mathfrak{hol}(S^3(b))$。我们知道 $S^2$ 的[和乐群](@entry_id:191471)是 $\mathrm{SO}(2)$，其代数 $\mathfrak{so}(2)$ 维数为1。$S^3$ 的[和乐群](@entry_id:191471)是 $\mathrm{SO}(3)$，其代数 $\mathfrak{so}(3)$ 维数为3。因此，$S^2(a) \times S^3(b)$ 的[和乐群](@entry_id:191471)代数维数是 $1+3=4$ [@problem_id:2968880]。

de Rham 分解定理的威力在于它将一般黎曼流形的和乐群[分类问题](@entry_id:637153)，简化为对那些具有不可约[和乐群](@entry_id:191471)表示的“基本构建块”的[分类问题](@entry_id:637153)。

### 贝尔杰分类：主要结果

基于上述所有原理，贝尔杰得以对[黎曼和](@entry_id:137667)乐群进行分类。其策略是：
1.  利用 de Rham 定理，将问题简化为**不可约**的[和乐群](@entry_id:191471)表示。
2.  利用[万有覆盖](@entry_id:151142)，将问题简化为**单连通**[流形](@entry_id:153038)，此时和乐群是连通的（$\mathrm{Hol} = \mathrm{Hol}^0$）。
3.  将问题进一步分为两类：[局部对称空间](@entry_id:637873)和非[局部对称空间](@entry_id:637873)。

#### [对称空间](@entry_id:181790)与非[对称空间](@entry_id:181790)

**[局部对称空间](@entry_id:637873)**是曲率张量平行的空间（$\nabla R = 0$）。卡丹（[Élie Cartan](@entry_id:263871)）已经对这些空间的[和乐群](@entry_id:191471)进行了完整分类。对于一个不可约的[黎曼对称空间](@entry_id:193796) $G/K$，其和乐群恰好是其在切空间上的**[迷向表示](@entry_id:184529)**（isotropy representation） [@problem_id:2968931]。

贝尔杰的工作集中在剩下的，也是更“一般”的一类：单连通、具有不可约[和乐群](@entry_id:191471)表示、且**非局部对称**的[黎曼流形](@entry_id:261160)。

#### 贝尔杰列表与[和乐群](@entry_id:191471)原理

通过对满足黎曼曲率张量代数对称性（特别是[第一比安基恒等式](@entry_id:200081)）的不可约子代数 $\mathfrak{h} \subset \mathfrak{so}(n)$ 进行穷举式的排除，贝尔杰证明，对于上述非对称情况，可能的[限制和乐群](@entry_id:637133)（或其[李代数](@entry_id:137954)）只能是以下列表中的一个 [@problem_id:2968980]：

| 和乐群 | [李代数](@entry_id:137954) | 作用空间 ($n = \dim M$) | 对应的几何结构 |
| :--- | :--- | :--- | :--- |
| $\mathrm{SO}(n)$ | $\mathfrak{so}(n)$ | $n \ge 2$ | 一般（无特殊结构） |
| $\mathrm{U}(m)$ | $\mathfrak{u}(m)$ | $n=2m, m \ge 2$ | 凯勒（Kähler）[流形](@entry_id:153038) |
| $\mathrm{SU}(m)$ | $\mathfrak{su}(m)$ | $n=2m, m \ge 2$ | 卡拉比-丘（Calabi-Yau）[流形](@entry_id:153038) |
| $\mathrm{Sp}(m)$ | $\mathfrak{sp}(m)$ | $n=4m, m \ge 1$ | 超凯勒（Hyperkähler）[流形](@entry_id:153038) |
| $\mathrm{Sp}(m)\cdot\mathrm{Sp}(1)$ | $\mathfrak{sp}(m)\oplus\mathfrak{sp}(1)$ | $n=4m, m \ge 2$ | 四元数凯勒（Quaternion-Kähler）[流形](@entry_id:153038)|
| $G_2$ | $\mathfrak{g}_2$ | $n=7$ | $G_2$ [流形](@entry_id:153038) |
| $\mathrm{Spin}(7)$ | $\mathfrak{spin}(7)$ | $n=8$ | $\mathrm{Spin}(7)$ [流形](@entry_id:153038) |

这个列表的深刻之处在于**和乐群原理**（Holonomy Principle）：一个张量场是平行的（即其[协变导数](@entry_id:152476)为零），当且仅当它在每一点都被[和乐群](@entry_id:191471)固定。

这意味着贝尔杰列表中的每一个“特殊”和乐群（即非 $\mathrm{SO}(n)$ 的群）的存在，等价于[流形](@entry_id:153038)上存在某种特殊的平行几何结构 [@problem_id:2968939]：
*   [和乐群](@entry_id:191471)为 $\mathrm{U}(m)$ 意味着存在一个平行的复结构 $J$。
*   [和乐群](@entry_id:191471)为 $\mathrm{SU}(m)$ 意味着存在一个平行的复结构 $J$ 和一个平行的复[体积形式](@entry_id:203000)（[流形](@entry_id:153038)是[里奇平坦](@entry_id:159097)的[凯勒流形](@entry_id:161192)）。
*   [和乐群](@entry_id:191471)为 $G_2$ 或 $\mathrm{Spin}(7)$ 意味着存在一个平行的特殊校准形式（calibration）。

$\mathrm{SO}(n)$ 是**一般情况**。对于一个“随机”选择的黎曼度量，没有任何理由期望它会恰好允许一个平行的复结构或其他特殊张量。因此，对于一个单连通[流形](@entry_id:153038)上的“一般”度量，其和乐群就是 $\mathrm{SO}(n)$ [@problem_id:2968939]。这澄清了一些误解，例如，拥有 $\mathrm{SO}(n)$ 和乐群并不要求[流形](@entry_id:153038)具有[常曲率](@entry_id:162122)；后者是一个非常强的条件，而前者是普遍情况。同样，在维度7，虽然存在具有 $G_2$ 和乐群的特殊[流形](@entry_id:153038)，但这并不妨碍也存在具有一般和乐群 $\mathrm{SO}(7)$ 的[流形](@entry_id:153038)。

总之，贝尔杰分类不仅提供了一个看似纯代数的列表，更重要的是，它为[黎曼流形](@entry_id:261160)的分类提供了一个强大的几何框架。通过和乐群，我们可以将[流形](@entry_id:153038)根据其所承载的平行几何结构进行分层，从最一般的 $\mathrm{SO}(n)$ [流形](@entry_id:153038)到具有丰富对称性的高度特殊的例[外流](@entry_id:274280)形。