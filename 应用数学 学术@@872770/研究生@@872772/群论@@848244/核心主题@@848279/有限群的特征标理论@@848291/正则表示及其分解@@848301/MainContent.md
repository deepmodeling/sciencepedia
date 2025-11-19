## 引言
[正则表示](@entry_id:137028)是有限群表示理论中最基本也最深刻的构造之一。它不仅仅是众多表示中的一个例子，而是内蕴地包含了群的全部对称性信息。理解[正则表示](@entry_id:137028)是掌握群的[代数结构](@entry_id:137052)与其[线性表示](@entry_id:139970)之间内在联系的关键。一个核心问题是：我们如何能够系统地理解一个群的所有可能表示？[正则表示](@entry_id:137028)通过提供一个“万能”的表示，完美地解答了这个问题。它如同一个完整的宝库，包含了群的所有不可约表示作为其基本组成部分，等待我们去分解和发掘。

本文将引导你全面探索[正则表示](@entry_id:137028)的理论与实践。在第一章“原则与机理”中，我们将从[群代数](@entry_id:145139)出发，精确构造[正则表示](@entry_id:137028)，推导其特征标，并证明其核心的分解定理及其重要推论。随后的“应用与[交叉](@entry_id:147634)学科联系”章节将展示这一理论如何应用于从[代数结构](@entry_id:137052)分析到物理学和[调和分析](@entry_id:198768)的广泛领域。最后，通过“动手实践”部分，你将有机会通过具体计算来巩固和加深对这些抽象概念的理解。

## 原则与机理

在本章中，我们将深入探讨[有限群](@entry_id:139710)表示理论的核心构造之一：**[正则表示](@entry_id:137028) (regular representation)**。继引言章节之后，我们将直接进入其定义、基本性质、分解定理以及其在群[代数结构](@entry_id:137052)和[调和分析](@entry_id:198768)中的深刻应用。[正则表示](@entry_id:137028)不仅是构建表示理论的基石，它还内蕴地包含了群的所有不可约表示的信息，揭示了群的[代数结构](@entry_id:137052)与其表示之间的精妙联系。

### [群代数](@entry_id:145139)与[正则表示](@entry_id:137028)的构造

为了精确定义[正则表示](@entry_id:137028)，我们首先需要引入**[群代数](@entry_id:145139) (group algebra)** 的概念。给定一个有限群 $G$ 和一个域 $F$（在本节的讨论中，我们主要关注复数域 $\mathbb{C}$），[群代数](@entry_id:145139) $F[G]$（或 $\mathbb{C}[G]$）是一个以 $G$ 的所有元素为基的 $F$-[向量空间](@entry_id:151108)。因此，$F[G]$ 中的任意元素 $v$ 都可以唯一地写成一个形式线性组合：
$$
v = \sum_{g \in G} a_g g, \quad a_g \in F
$$
这个[向量空间](@entry_id:151108)的维数等于群的阶 $|G|$。通过将群 $G$ 中的乘法运算线性地拓展到整个空间，即
$$
\left( \sum_{g \in G} a_g g \right) \left( \sum_{h \in G} b_h h \right) = \sum_{g, h \in G} (a_g b_h) (gh)
$$
$F[G]$ 便具备了[代数结构](@entry_id:137052)。

现在，我们可以让群 $G$ 作用在其自身的[群代数](@entry_id:145139) $\mathbb{C}[G]$ 上。最自然的作用方式是**[左乘作用](@entry_id:140679)**：对于任意 $g' \in G$ 和任意向量 $v = \sum_{g \in G} a_g g \in \mathbb{C}[G]$，定义：
$$
g' \cdot v = g' \left( \sum_{g \in G} a_g g \right) = \sum_{g \in G} a_g (g'g)
$$
由于群的乘法满足[结合律](@entry_id:151180)，这个作用是一个线性变换，并且构成了一个[群同态](@entry_id:140603) $\rho: G \to \text{GL}(\mathbb{C}[G])$。这个由[左乘作用](@entry_id:140679)在[群代数](@entry_id:145139)上诱导的表示被称为 $G$ 的**[左正则表示](@entry_id:146345) (left regular representation)**，我们记为 $\rho_{\text{reg}}$。从[模论](@entry_id:139410)的观点看，这相当于将 $\mathbb{C}[G]$ 视为其自身的左模。

### [正则表示的特征标](@entry_id:137278)

表示的**特征标 (character)** 是研究其结构的关键工具。对于[正则表示](@entry_id:137028) $\rho_{\text{reg}}$，其特征标 $\chi_{\text{reg}}(g) = \text{Tr}(\rho_{\text{reg}}(g))$ 具有一个极其简洁而优美的形式。为了计算它，我们在 $\mathbb{C}[G]$ 中选取群元素 $\{h\}_{h \in G}$ 作为一组基。对于任意 $g' \in G$，$\rho_{\text{reg}}(g')$ 的作用是将[基向量](@entry_id:199546) $h$ 变换为 $g'h$。因此，表示矩阵 $[\rho_{\text{reg}}(g')]_{k,h}$ 在这个基下的[矩阵元](@entry_id:186505)为：
$$
[\rho_{\text{reg}}(g')]_{k,h} = \begin{cases} 1   \text{if } k = g'h \\ 0   \text{otherwise} \end{cases}
$$
特征标是[矩阵的迹](@entry_id:139694)，即对角元之和：
$$
\chi_{\text{reg}}(g') = \sum_{h \in G} [\rho_{\text{reg}}(g')]_{h,h}
$$
对角元非零，当且仅当 $h = g'h$。

我们分两种情况讨论 [@problem_id:2920925]：
1.  当 $g' = e$（单位元）时，条件 $h = eh$ 对所有 $h \in G$ 均成立。因此，矩阵的对角线上有 $|G|$ 个 1，其余为 0。所以，$\chi_{\text{reg}}(e) = |G|$。这表明[正则表示](@entry_id:137028)的维数等于[群的阶](@entry_id:137115)。

2.  当 $g' \neq e$ 时，方程 $h = g'h$ 在群中没有解（否则两边同乘 $h^{-1}$ 会得到 $e = g'$，与假设矛盾）。因此，所有对角元都为 0，从而 $\chi_{\text{reg}}(g') = 0$。

综上所述，[正则表示的特征标](@entry_id:137278)为：
$$
\chi_{\text{reg}}(g) = \begin{cases} |G|   \text{if } g=e \\ 0   \text{if } g \neq e \end{cases}
$$
这个简单的性质是[正则表示](@entry_id:137028)理论的基石，许多深刻的结论都由此导出。

### [正则表示的分解](@entry_id:146409)定理

有限群在复数域上的任何表示都可以分解为不可约表示 (irreducible representations, or irreps) 的直和。[正则表示的分解](@entry_id:146409)揭示了它与所有[不可约表示](@entry_id:263310)之间的内在联系。

**定理 ([正则表示分解](@entry_id:193264)定理):** 任何[有限群](@entry_id:139710) $G$ 的[左正则表示](@entry_id:146345) $\rho_{\text{reg}}$ 分解为 $G$ 的所有不等价[不可约表示](@entry_id:263310)的直和，其中每个[不可约表示](@entry_id:263310) $\rho_i$ 出现的次数（即**重数, multiplicity** $m_i$）等于其自身的维数 $d_i$。
$$
\rho_{\text{reg}} \cong \bigoplus_{i=1}^{k} m_i \rho_i = \bigoplus_{i=1}^{k} d_i \rho_i
$$
其中 $\{ \rho_i \}_{i=1}^k$ 是 $G$ 的所有不等价[不可约表示](@entry_id:263310)的完备集。

**证明:** 设 $\chi_i$ 是不可约表示 $\rho_i$ 的特征标。根据表示理论的基本公式，$\rho_i$ 在 $\rho_{\text{reg}}$ 中的[重数](@entry_id:136466) $m_i$ 可以通过[特征标的内积](@entry_id:137615)计算：
$$
m_i = \langle \chi_{\text{reg}}, \chi_i \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_{\text{reg}}(g) \overline{\chi_i(g)}
$$
利用我们刚刚导出的 $\chi_{\text{reg}}$ 的性质，这个求和中只有 $g=e$ 的项非零：
$$
m_i = \frac{1}{|G|} \left( \chi_{\text{reg}}(e) \overline{\chi_i(e)} + \sum_{g \neq e} 0 \cdot \overline{\chi_i(g)} \right) = \frac{1}{|G|} (|G| \cdot \overline{\chi_i(e)}) = \overline{\chi_i(e)}
$$
由于表示的维数 $d_i = \chi_i(e)$ 是一个正整数，所以 $\overline{\chi_i(e)} = \chi_i(e) = d_i$。因此，[重数](@entry_id:136466) $m_i$ 恰好等于 $\rho_i$ 的维数 $d_i$ [@problem_id:1611972] [@problem_id:2920925]。证毕。

### 分解定理的重要推论

[正则表示的分解](@entry_id:146409)定理是[表示论](@entry_id:137998)的中心结果之一，它有几个至关重要的推论。

**1. [正则表示](@entry_id:137028)的可约性**

对于任何阶数 $|G|  1$ 的非[平凡群](@entry_id:151996)，其[正则表示](@entry_id:137028)**必定是可约的 (reducible)**。我们可以通过计算其[特征标的内积](@entry_id:137615)范数平方来证明这一点 [@problem_id:1646205]。一个表示是不可约的当且仅当 $\langle \chi, \chi \rangle = 1$。
$$
\langle \chi_{\text{reg}}, \chi_{\text{reg}} \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_{\text{reg}}(g) \overline{\chi_{\text{reg}}(g)} = \frac{1}{|G|} (\chi_{\text{reg}}(e))^2 = \frac{1}{|G|} |G|^2 = |G|
$$
因为 $|G|  1$，所以 $\langle \chi_{\text{reg}}, \chi_{\text{reg}} \rangle  1$，这表明 $\rho_{\text{reg}}$ 是可约的。这也与分解定理一致：如果存在维数大于1的[不可约表示](@entry_id:263310)，或存在多于一个[不可约表示](@entry_id:263310)，那么分解后的表示显然是可约的。

**2. [维数平方和](@entry_id:142213)公式**

这个著名的公式直接从[正则表示的特征标](@entry_id:137278)分解中得出。根据分解定理，我们有特征标的等式：
$$
\chi_{\text{reg}}(g) = \sum_{i=1}^{k} d_i \chi_i(g)
$$
我们令 $g=e$ 来计算这个等式在单位元处的值。我们知道 $\chi_{\text{reg}}(e) = |G|$ 且 $\chi_i(e) = d_i$。代入得到：
$$
|G| = \sum_{i=1}^{k} d_i \cdot d_i = \sum_{i=1}^{k} d_i^2
$$
这个公式——**所有不等价[不可约表示](@entry_id:263310)的[维数平方和](@entry_id:142213)等于[群的阶](@entry_id:137115)**——是表示论中的一个基本恒等式，对于确定群的不可约表示维数至关重要 [@problem_id:2920925]。

**3. 一个具体的例子：$D_5$ 群**

让我们以正五边形的对称群——10阶[二面体群](@entry_id:143875) $D_5$ 为例来说明这些原理 [@problem_id:1611972]。
*   首先，我们需要知道 $D_5$ 有多少个不等价的不可约表示。这个数目等于群的[共轭类](@entry_id:143916)数目。对于 $D_5$，有4个[共轭类](@entry_id:143916)：$\{e\}$, $\{r, r^4\}$, $\{r^2, r^3\}$ 以及包含5个反射的类。因此，$D_5$ 有4个不可约表示，我们记为 $\rho_1, \rho_2, \rho_3, \rho_4$。
*   其次，我们利用[维数平方和](@entry_id:142213)公式确定它们的维数 $d_i$：$d_1^2 + d_2^2 + d_3^2 + d_4^2 = |D_5| = 10$。
*   [一维表示](@entry_id:136509)的数目等于[群的阿贝尔化](@entry_id:144001)（abelianization）$G/[G,G]$ 的阶。对于 $D_5$，其[换位子群](@entry_id:141128)为 $[D_5,D_5]=\langle r \rangle$，因此阿贝尔化 $D_5/[D_5,D_5]$ 的阶为 2，同构于 $\mathbb{Z}_2$，所以有两个[一维表示](@entry_id:136509)。不妨设 $d_1=1, d_2=1$。
*   代入平方和公式，我们得到 $1^2 + 1^2 + d_3^2 + d_4^2 = 10$，即 $d_3^2 + d_4^2 = 8$。满足这个条件的唯一正整数解是 $d_3=2, d_4=2$。
*   因此，$D_5$ 的4个不可约表示的维数分别为 $1, 1, 2, 2$。
*   根据[正则表示的分解](@entry_id:146409)定理，$\rho_{\text{reg}}$ 中每个[不可约表示的重数](@entry_id:141777)等于其维数。所以，$D_5$ 的[正则表示分解](@entry_id:193264)为：
    $$
    \rho_{\text{reg}} \cong \rho_1 \oplus \rho_2 \oplus 2\rho_3 \oplus 2\rho_4
    $$
    这清晰地展示了[正则表示](@entry_id:137028)是如何“包含”群的所有[基本对称性](@entry_id:161256)的。

### [群代数](@entry_id:145139)的[代数结构](@entry_id:137052)

[正则表示的分解](@entry_id:146409)不仅是[表示的分解](@entry_id:147581)，它还深刻地反映了[群代数](@entry_id:145139) $\mathbb{C}[G]$ 本身的[代数结构](@entry_id:137052)。根据[马施克定理](@entry_id:142097) (Maschke's Theorem)，只要[域的特征](@entry_id:154386)不整除[群的阶](@entry_id:137115)（对于 $\mathbb{C}$，特征为0，此条件总满足），[群代数](@entry_id:145139) $\mathbb{C}[G]$ 就是一个**[半单代数](@entry_id:139931) (semisimple algebra)**。

根据**Wedderburn-Artin 定理**，任何[半单代数](@entry_id:139931)都同构于一系列单代数 (simple algebras) 的直和。对于在[代数闭域](@entry_id:151836) $\mathbb{C}$ 上的[群代数](@entry_id:145139)，这些单代数就是[矩阵代数](@entry_id:153824)。具体来说：
$$
\mathbb{C}[G] \cong \bigoplus_{i=1}^{k} M_{d_i}(\mathbb{C})
$$
其中 $k$ 是不等价[不可约表示](@entry_id:263310)的数目，$d_i$ 是第 $i$ 个[不可约表示](@entry_id:263310)的维数，$M_{d_i}(\mathbb{C})$是 $\mathbb{C}$ 上的 $d_i \times d_i$ 矩阵代数。

这个代数同构与[正则表示的分解](@entry_id:146409)是同一现象的两个侧面。$\mathbb{C}[G]$ 的每个单代数分量 $M_{d_i}(\mathbb{C})$ 恰好对应一个[不可约表示](@entry_id:263310) $\rho_i$。[正则表示的分解](@entry_id:146409)，$\rho_{\text{reg}} \cong \bigoplus_i d_i \rho_i$，实际上是 $\mathbb{C}[G]$ 作为左 $G$-模的分解。每个 $M_{d_i}(\mathbb{C})$ 作为左 $G$-模，本身可以分解为 $d_i$ 个同构于 $\rho_i$ 的不可约子[模的[直](@entry_id:156308)和](@entry_id:156782)。

[群代数](@entry_id:145139)的**中心 (center)** $Z(\mathbb{C}[G])$ 也与此结构密切相关。$Z(\mathbb{C}[G])$ 的维数等于单代数分量的数目，也就是[不可约表示](@entry_id:263310)的数目，也即群的共轭类数目 [@problem_id:1611959]。例如，对于[四元数群](@entry_id:147721) $Q_8$，它有5个共轭类，因此有5个不可约表示。其[群代数](@entry_id:145139)的中心 $Z(\mathbb{C}[Q_8])$ 是一个5维[向量空间](@entry_id:151108)，并且 $\mathbb{C}[Q_8]$ 的Wedderburn分解包含5个单代数分量。

### 群上的[调和分析](@entry_id:198768)

[正则表示](@entry_id:137028)的理论框架可以被视为在[有限群](@entry_id:139710)上发展**[调和分析](@entry_id:198768) (harmonic analysis)** 或**傅里叶分析 (Fourier analysis)** 的基础。在这个视角下，[群代数](@entry_id:145139) $\mathbb{C}[G]$ 中的元素 $f = \sum a_g g$ 被看作是定义在群 $G$ 上的[复值函数](@entry_id:196054)。

*   不可约表示 $\rho_i$ 扮演了经典傅里叶分析中“基本频率”（如 $e^{inx}$）的角色。
*   一个函数 $f$ 的**[傅里叶变换](@entry_id:142120) (Fourier transform)** 被定义为它在每个[不可约表示](@entry_id:263310)下的像，即一组矩阵：
    $$
    \hat{f}(\rho_i) = \sum_{g \in G} a_g \rho_i(g) \in M_{d_i}(\mathbb{C})
    $$
*   [正则表示的分解](@entry_id:146409)定理[实质](@entry_id:149406)上说明，任何定义在群上的函数都可以被分解为这些“基本频率”的[线性组合](@entry_id:154743)。

这个类比中最核心的恒等式之一是**Plancherel 恒等式**，它相当于经典傅里叶理论中的 Parseval 定理。它将函数在“时域”（即群本身）的范数与它在“[频域](@entry_id:160070)”（即表示空间）的范数联系起来。在 $\mathbb{C}[G]$ 上定义[内积](@entry_id:158127) $\langle f, h \rangle = \sum_g a_g \overline{b_g}$，Plancherel 恒等式表述为：
$$
\sum_{g \in G} |a_g|^2 = \frac{1}{|G|} \sum_{i=1}^{k} d_i \text{Tr}(\hat{f}(\rho_i) \hat{f}(\rho_i)^\dagger)
$$
其中 $\hat{f}(\rho_i)^\dagger$ 是矩阵 $\hat{f}(\rho_i)$ 的共轭转置。这个恒等式可以被看作是“[能量守恒](@entry_id:140514)”：函数在群元素基下的能量（左侧）等于其在所有不可约表示分量上的能量之和（右侧）[@problem_id:823843]。

与此密切相关的是**中心本原[幂等元](@entry_id:153117) (central primitive idempotents)** $e_i$。每个不可约表示 $\rho_i$ 都对应一个中心元 $e_i = \frac{d_i}{|G|} \sum_g \chi_i(g^{-1}) g$。这个元素在[傅里叶变换](@entry_id:142120)下的像极为简单：$\hat{e_i}(\rho_j) = \delta_{ij} I_{d_i}$（其中 $I$ 是[单位矩阵](@entry_id:156724)）。在代数上，$e_i$ 是一个投影算子，它将 $\mathbb{C}[G]$ 投影到与 $\rho_i$ 相关的[子空间](@entry_id:150286)上（即 $d_i \rho_i$ 所在的同构型分量）。这个[子空间](@entry_id:150286)的维数是 $d_i^2$。可以证明，由 $e_i$ 定义的左乘[投影算子](@entry_id:154142) $P_i=L_{e_i}$ 的[Hilbert-Schmidt范数](@entry_id:265114)的平方恰好是这个[子空间](@entry_id:150286)的维数，即 $\|P_i\|_{HS}^2 = d_i^2$ [@problem_id:823893]。

### 向有理数域的推广

到目前为止，我们的讨论都集中在[复数域](@entry_id:153768) $\mathbb{C}$ 上。然而，将域从 $\mathbb{C}$ 替换为其他域，如有理[数域](@entry_id:155558) $\mathbb{Q}$，会引入新的复杂性和更丰富的结构。

对于有理[群代数](@entry_id:145139) $\mathbb{Q}[G]$，它仍然是半单的，因此[Wedderburn-Artin定理](@entry_id:197655)依然适用：
$$
\mathbb{Q}[G] \cong \bigoplus_{i=1}^{k} A_i
$$
其中每个 $A_i$ 是一个单代数。但与 $\mathbb{C}[G]$ 的情况不同，这里的单代数 $A_i$ 不再是 $\mathbb{Q}$ 上的[矩阵代数](@entry_id:153824)，而是 $M_{n_i}(D_i)$ 的形式，其中 $D_i$ 是一个包含 $\mathbb{Q}$ 的有限维**[除环](@entry_id:149568) (division algebra)**。

这里的关键问题是，如何确定单分量的数目 $k$ 以及它们的结构 $M_{n_i}(D_i)$？
1.  **单分量的数目:** $k$ 等于复不可约特征标的 **$\mathbb{Q}$-Galois 共轭类** 的数目。如果一个复特征标 $\chi$ 的所有值都在 $\mathbb{Q}$ 中，它自己就构成一个类。如果 $\chi$ 的值在某个[数域](@entry_id:155558) $\mathbb{Q}(\chi)$ 中，那么所有通过 Galois 群 $\text{Gal}(\mathbb{Q}(\chi)/\mathbb{Q})$ 的作用可以从 $\chi$ 得到的特征标都属于同一个共轭类。例如，对于 $D_7$ 群，它有5个复不可约特征标。其中两个是一维的，取值于 $\mathbb{Q}$，它们各自形成一个 $\mathbb{Q}$-Galois [共轭类](@entry_id:143916)。另外三个是二维的，它们的特征标值是相互共轭的无理数，因此它们共同构成一个[共轭类](@entry_id:143916)。所以，$\mathbb{Q}[D_7]$ 的Wedderburn分解中有 $2+1=3$ 个单代数分量 [@problem_id:823879]。

2.  **单分量的结构:** 确定每个 $M_{n_i}(D_i)$ 的具体结构更为复杂，涉及到**舒尔指数 (Schur index)** 的概念。对于一个 $\mathbb{Q}$-Galois 共轭类，它对应 $\mathbb{Q}[G]$ 中的一个单分量 $A_i$。这个分量的中心是特征标域 $\mathbb{Q}(\chi)$。[除环](@entry_id:149568) $D_i$ 可能是一个[非交换](@entry_id:136599)的代数。一个经典的例子是[四元数群](@entry_id:147721) $Q_8$。它的5个复特征标都取有理数值，但它们并不都对应 $\mathbb{Q}$ 上的[矩阵代数](@entry_id:153824)。分析表明，$\mathbb{Q}[Q_8]$ 的分解是：
    $$
    \mathbb{Q}[Q_8] \cong \mathbb{Q} \oplus \mathbb{Q} \oplus \mathbb{Q} \oplus \mathbb{Q} \oplus \mathbb{H}
    $$
    其中四个分量是 $\mathbb{Q}$ 本身（对应四个[一维表示](@entry_id:136509)），而第五个分量是 Hamilton [四元数代数](@entry_id:196348) $\mathbb{H}$，这是一个在 $\mathbb{Q}$ 上的4维非交换[除环](@entry_id:149568)（对应那个二维[不可约表示](@entry_id:263310)）。因此，出现在这个分解中的[除环](@entry_id:149568)的维数之和为 $1+1+1+1+4=8$ [@problem_id:823916]。

这个推广展示了[正则表示](@entry_id:137028)和[群代数](@entry_id:145139)理论的深度，揭示了群的结构、[表示论](@entry_id:137998)和数论之间深刻的相互作用。从[正则表示](@entry_id:137028)的基本分解出发，我们最终触及了代数数论和[非交换代数](@entry_id:141756)的前沿领域。