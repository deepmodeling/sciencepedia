## 引言

在现代数学的宏伟版图中，[上同调群](@entry_id:142450)（Cohomology Groups, $H^n$）是基石性的[不变量](@entry_id:148850)，它为我们理解[拓扑空间](@entry_id:155056)的深层结构提供了一套极其强大的代数语言。与我们所熟知的、直观捕捉空间“孔洞”数量的同调论相比，上同调提供了一个对偶的、但结构上更为丰富的视角。其真正的威力在于其自然的乘法结构——[杯积](@entry_id:159554)，这使得一系列[上同调群](@entry_id:142450)融合成一个代[数环](@entry_id:636822)，从而能够编码远超简单计数“孔洞”的复杂几何信息。然而，正是这种抽象性和丰富的[代数结构](@entry_id:137052)，使得计算和理解上同调成为许多学习者面临的挑战。

本文旨在系统性地梳理[上同调](@entry_id:160558)的核心理论与应用，填补从抽象定义到实际计算与应用的认知鸿沟。我们将带领读者穿越[上同调](@entry_id:160558)的理论森林，掌握其精髓，并见证它如何在不同学科中大放异彩。

- 在“**原理与机制**”一章中，我们将从[德拉姆上同调](@entry_id:158673)的具体实例出发，建立上同调的基本直觉。随后，我们将系统介绍一系列强大的计算工具，包括泛系数定理、[Mayer-Vietoris序列](@entry_id:161286)和[Künneth公式](@entry_id:158001)，并深入剖析[上同调理论](@entry_id:270863)的灵魂——杯积结构及其深刻的几何意义。
- 接着，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将展示[上同调](@entry_id:160558)如何作为一种通用语言，通过特征类、层[上同调](@entry_id:160558)、伽罗瓦上同调等形式，在[微分几何](@entry_id:145818)、[代数几何](@entry_id:156300)、低维拓扑、物理学乃至数论等前沿领域中解决关键问题。
- 最后，通过“**动手实践**”部分，读者将有机会运用所学知识，解决一系列精心设计的计算问题，从而将理论知识内化为实际操作的能力。

通过本次学习，你将不仅掌握上同调群的计算方法，更将深刻理解其作为连接拓扑、几何与代数的桥梁所扮演的关键角色。

## 原理与机制

本章将深入探讨[上同调群](@entry_id:142450)的内在原理与核心机制。[上同调](@entry_id:160558)不仅是[拓扑空间](@entry_id:155056)的一系列[不变量](@entry_id:148850)，其丰富的[代数结构](@entry_id:137052)和强大的计算工具，使其成为现代几何学与拓扑学中不可或缺的支柱。我们将从上同调的基本属性出发，系统地介绍其主要计算方法，并着重阐述其核心结构——杯积（cup product）及其深刻的几何意义。

### [上同调群](@entry_id:142450)的基本概念

[上同调群](@entry_id:142450)从根本上捕捉了[拓扑空间](@entry_id:155056)的“孔洞”信息，但其视角与同调论相反。以[微分](@entry_id:158718)[流形](@entry_id:153038)上的 **[德拉姆上同调](@entry_id:158673)（de Rham cohomology）** 为例，其定义优雅地揭示了这一思想。对于一个光滑流形 $M$，其 $k$ 阶[德拉姆上同调](@entry_id:158673)群 $H_{dR}^k(M)$ 定义为商空间：
$$
H_{dR}^k(M) = \frac{Z^k(M)}{B^k(M)}
$$
其中，$Z^k(M)$ 是所有 **闭 $k$-形式**（closed $k$-forms）构成的[向量空间](@entry_id:151108)，即外微分 $d\omega = 0$ 的 $k$-形式 $\omega$；而 $B^k(M)$ 是所有 **恰当 $k$-形式**（exact $k$-forms）构成的[子空间](@entry_id:150286)，即存在一个 $(k-1)$-形式 $\eta$ 使得 $\omega = d\eta$ 的 $k$-形式。[庞加莱引理](@entry_id:160150)告诉我们，在[可缩空间](@entry_id:153541)（如欧氏空间 $\mathbb{R}^n$）上，任何[闭形式](@entry_id:272960)都是恰当的，因此其所有高阶上同调群均为零。这意味着[上同调群](@entry_id:142450)的非平凡性直接反映了空间的“[拓扑复杂度](@entry_id:261170)”。

[上同调](@entry_id:160558)的一个至关重要的特性是其 **[同伦不变性](@entry_id:150428)（homotopy invariance）**。如果两个空间具有相同的[同伦型](@entry_id:148015)，那么它们的上同调群是同构的。这使得我们能够通过将复杂空间简化为其[同伦等价](@entry_id:150816)的简单模型来计算其[上同调群](@entry_id:142450)。

一个典型的例子是计算从[二维球面](@entry_id:269890) $S^2$ 上移除三个不同点后所得[流形](@entry_id:153038) $M$ 的一阶[德拉姆上同调](@entry_id:158673)群 $\dim H_{dR}^1(M)$。直接在 $M$ 上处理微分形式会相当繁琐。然而，我们可以利用[同伦不变性](@entry_id:150428)来简化问题。通过球极投影，挖掉一个点的球面 $S^2 \setminus \{p_1\}$ [同胚](@entry_id:146933)于平面 $\mathbb{R}^2$。因此，挖掉三个点的球面 $M = S^2 \setminus \{p_1, p_2, p_3\}$ 就同胚于挖掉两个点的平面 $\mathbb{R}^2 \setminus \{q_1, q_2\}$。这个空间可以[形变收缩](@entry_id:148036)（homotopy equivalent）到两个圆的[楔和](@entry_id:270607)（wedge sum），记作 $S^1 \vee S^1$。由于 $H_{dR}^1(S^1) \cong \mathbb{R}$，并且一阶上同调群在[楔和](@entry_id:270607)下具有可加性，我们立即得到 $\dim H_{dR}^1(M) = \dim H_{dR}^1(S^1 \vee S^1) = 2$ [@problem_id:928028]。这个例子清晰地展示了，上同调所捕捉的是空间最根本的拓扑骨架，而非其具体的[几何实现](@entry_id:265700)。

### 上同调的计算工具

尽管定义清晰，但直接从定义出发计算上同调群往往是困难的。幸运的是，代数拓扑学发展了一套强大的计算工具箱。

#### 泛系数定理

**泛系数定理（Universal Coefficient Theorem, UCT）** 是连接上同调与同调的桥梁。同调群 $H_n(X; \mathbb{Z})$ 通常更易于通过胞腔分解等方法计算。UCT 表明，我们可以从积分同调[群代数](@entry_id:145139)地推导出任意系数群 $G$ 下的上同调群 $H^n(X; G)$。其核心是一个分裂的短[正合序列](@entry_id:151503)：
$$
0 \to \text{Ext}_{\mathbb{Z}}^1(H_{n-1}(X; \mathbb{Z}), G) \to H^n(X; G) \to \text{Hom}_{\mathbb{Z}}(H_n(X; \mathbb{Z}), G) \to 0
$$
这个序列的分裂意味着[上同调群](@entry_id:142450)可以分解为两个部分的直和：
$$
H^n(X; G) \cong \text{Ext}_{\mathbb{Z}}^1(H_{n-1}(X; \mathbb{Z}), G) \oplus \text{Hom}_{\mathbb{Z}}(H_n(X; \mathbb{Z}), G)
$$
这里，**Hom 函子** $\text{Hom}_{\mathbb{Z}}(H_n, G)$ 捕捉了由 $H_n$ 中的自由部分贡献的上同调部分。而 **Ext 函子** $\text{Ext}_{\mathbb{Z}}^1(H_{n-1}, G)$ 则完全由 $H_{n-1}$ 中的挠率部分（torsion）决定，它揭示了[上同调群](@entry_id:142450)中更为微妙的挠率结构。

考虑一个三维 **[透镜空间](@entry_id:274705)（Lens Space）** $L(p,q)$ 的例子。已知其积分同调群为 $H_1(L(p,q); \mathbb{Z}) \cong \mathbb{Z}/p\mathbb{Z}$ 和 $H_2(L(p,q); \mathbb{Z}) = 0$。我们来计算其二阶积分上同调群 $H^2(L(7,3); \mathbb{Z})$。根据 UCT，我们有：
$$
H^2(L(7,3); \mathbb{Z}) \cong \text{Ext}_{\mathbb{Z}}^1(H_1(L(7,3); \mathbb{Z}), \mathbb{Z}) \oplus \text{Hom}_{\mathbb{Z}}(H_2(L(7,3); \mathbb{Z}), \mathbb{Z})
$$
由于 $H_2(L(7,3); \mathbb{Z}) = 0$，右侧的 Hom 项为零。关键在于 Ext 项。利用 Ext [函子](@entry_id:150427)的性质 $\text{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/m\mathbb{Z}, \mathbb{Z}) \cong \mathbb{Z}/m\mathbb{Z}$，我们得到：
$$
\text{Ext}_{\mathbb{Z}}^1(H_1(L(7,3); \mathbb{Z}), \mathbb{Z}) \cong \text{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/7\mathbb{Z}, \mathbb{Z}) \cong \mathbb{Z}/7\mathbb{Z}
$$
因此，$H^2(L(7,3); \mathbb{Z}) \cong \mathbb{Z}/7\mathbb{Z}$，这是一个7阶的[循环群](@entry_id:138668) [@problem_id:928024]。这个结果表明，空间中一阶同调的挠率，通过 UCT 转化为高一阶的[上同调](@entry_id:160558)挠率。

#### Mayer-Vietoris 序列

**Mayer-Vietoris 序列（Mayer-Vietoris Sequence）** 是一种“分而治之”的强大工具。如果一个空间 $X$ 可以分解为两个（通常更简单的）[子空间](@entry_id:150286) $U$ 和 $V$ 的并，$X = U \cup V$，该序列就将 $U$, $V$, $U \cap V$ 和 $X$ 的[上同调群](@entry_id:142450)联系在一个[长正合序列](@entry_id:153438)中：
$$
\cdots \to H^n(X) \to H^n(U) \oplus H^n(V) \to H^n(U \cap V) \xrightarrow{\delta^*} H^{n+1}(X) \to \cdots
$$
其中，**[连接同态](@entry_id:160713)（connecting homomorphism）** $\delta^*$ 是关键，它将低维[上同调](@entry_id:160558)的信息“传递”到高一维。

我们以 **克莱因瓶（Klein bottle）** $K$ 为例来计算其二阶积分[上同调群](@entry_id:142450) $|H^2(K; \mathbb{Z})|$。[克莱因瓶](@entry_id:149661)可以看作是两个 **[莫比乌斯带](@entry_id:152389)（Möbius strip）** $U$ 和 $V$ 沿着它们共同的边界圆 $B \cong S^1$ 粘合而成。因此 $K = U \cup V$ 且 $U \cap V = B$。由于[莫比乌斯带](@entry_id:152389)[同伦](@entry_id:139266)于一个圆 $S^1$，我们有 $H^1(U) \cong H^1(V) \cong H^1(B) \cong \mathbb{Z}$，且它们的高于一阶的[上同调群](@entry_id:142450)均为零。将这些信息代入 Mayer-Vietoris 序列的相关部分：
$$
H^1(U) \oplus H^1(V) \xrightarrow{\psi^*} H^1(B) \xrightarrow{\delta^*} H^2(K) \to H^2(U) \oplus H^2(V)
$$
由于 $H^2(U) = H^2(V) = 0$，序列简化为 $H^2(K) \cong \text{coker}(\psi^*) = H^1(B) / \text{Im}(\psi^*)$。通过分析对偶的同调映射，可以确定映射 $\psi^*$ 的像是 $H^1(B)$ 中的[子群](@entry_id:146164) $2\mathbb{Z}$。因此，我们最终得到：
$$
H^2(K; \mathbb{Z}) \cong \mathbb{Z} / 2\mathbb{Z}
$$
这是一个2阶循环群 [@problem_id:928092]。

#### Künneth 定理

**Künneth 定理（Künneth Formula）** 用于计算积空间 $Y \times Z$ 的[上同调](@entry_id:160558)。对于域系数，它给出了一个简单的[环同构](@entry_id:147982)。但对于更一般的整数系数，其形式更为复杂，同样包含一个[分裂短正合序列](@entry_id:159775)，导致如下同构：
$$
H^n(Y \times Z; \mathbb{Z}) \cong \left( \bigoplus_{p+q=n} H^p(Y) \otimes H^q(Z) \right) \oplus \left( \bigoplus_{p+q=n+1} \mathrm{Tor}_1^{\mathbb{Z}}(H^p(Y), H^q(Z)) \right)
$$
其中 $\otimes$ 是张量积，**Tor [函子](@entry_id:150427)** $\mathrm{Tor}_1^{\mathbb{Z}}$ 捕捉了由因[子空间](@entry_id:150286)中的挠率相互作用产生的新的挠率。

例如，计算 $X = \mathbb{R}P^4 \times \mathbb{R}P^4$ 的五阶积分上同调群 $H^5(X; \mathbb{Z})$。[实射影空间](@entry_id:149094) $\mathbb{R}P^4$ 的非零积分上同调群为 $H^0 \cong \mathbb{Z}$, $H^2 \cong \mathbb{Z}_2$, $H^4 \cong \mathbb{Z}_2$。
对于 $H^5(X; \mathbb{Z})$ 的计算：
1.  **张量积部分** ($p+q=5$): 由于 $\mathbb{R}P^4$ 的奇数阶[上同调群](@entry_id:142450)为零，任何满足 $p+q=5$ 的配对 $(H^p, H^q)$ 中至少有一个为零，因此 $\bigoplus_{p+q=5} H^p \otimes H^q = 0$。
2.  **Tor 部分** ($p+q=6$): 我们需要考虑 $\mathrm{Tor}_1^{\mathbb{Z}}(H^p(\mathbb{R}P^4), H^q(\mathbb{R}P^4))$。Tor 函子在其中一个参数为[自由群](@entry_id:151249)（如 $\mathbb{Z}$）时为零。因此，非零贡献仅来自 $(p,q) = (2,4)$ 和 $(4,2)$。利用性质 $\mathrm{Tor}_1^{\mathbb{Z}}(\mathbb{Z}_m, \mathbb{Z}_n) \cong \mathbb{Z}_{\text{gcd}(m,n)}$，我们有 $\mathrm{Tor}_1^{\mathbb{Z}}(\mathbb{Z}_2, \mathbb{Z}_2) \cong \mathbb{Z}_2$。
    因此，Tor 部分的总贡献是 $\mathbb{Z}_2 \oplus \mathbb{Z}_2$。

结合两部分，我们得到 $H^5(\mathbb{R}P^4 \times \mathbb{R}P^4; \mathbb{Z}) \cong \mathbb{Z}_2 \oplus \mathbb{Z}_2$，其阶数为 4 [@problem_id:928147]。

#### [相对上同调](@entry_id:272456)与长正合序列

**[相对上同调](@entry_id:272456)群（Relative Cohomology Groups）** $H^n(X, A)$ 研究的是空间 $X$ 相对于其[子空间](@entry_id:150286) $A$ 的[拓扑性质](@entry_id:141605)。它们在处理[带边流形](@entry_id:159788)或研究空间的局部性质时非常有用。这些群与绝对[上同调群](@entry_id:142450)通过一个 **长正合序列（Long Exact Sequence of a Pair）** 联系起来：
$$
\cdots \to H^{n-1}(A) \xrightarrow{\delta^*} H^n(X,A) \to H^n(X) \xrightarrow{i^*} H^n(A) \to \cdots
$$
这里 $i^*$ 是由包含映射 $i: A \hookrightarrow X$ 诱导的限制映射。

考虑一个从环面上挖去一个小开圆盘得到的空间 $X$ (一个“带孔环面”)，其边界为 $A \cong S^1$。我们想计算二阶[相对上同调](@entry_id:272456)群的秩 $\text{rank}(H^2(X, A; \mathbb{Z}))$。空间 $X$ [同伦](@entry_id:139266)于 $S^1 \vee S^1$。我们有 $H^1(X) \cong \mathbb{Z} \oplus \mathbb{Z}$， $H^1(A) \cong \mathbb{Z}$，以及 $H^2(X) = 0$。将这些代入长正合序列中：
$$
\cdots \to H^1(X) \xrightarrow{i^*} H^1(A) \xrightarrow{\delta^*} H^2(X,A) \to H^2(X) \to \cdots
$$
序列的相关部分简化为：
$$
\mathbb{Z} \oplus \mathbb{Z} \xrightarrow{i^*} \mathbb{Z} \xrightarrow{\delta^*} H^2(X,A) \to 0
$$
可以证明，对于这种情况，限制映射 $i^*$ 是零同态。根据正合性，$\text{Im}(i^*) = \text{Ker}(\delta^*) = 0$，这意味着 $\delta^*$ 是一个单射。同时，由于序列在 $H^2(X,A)$ 处终止于零，$\delta^*$ 也是一个满射。因此，$\delta^*$ 是一个同构，我们得到 $H^2(X, A; \mathbb{Z}) \cong H^1(A; \mathbb{Z}) \cong \mathbb{Z}$。所以其秩为 1 [@problem_id:928042]。

### [上同调环](@entry_id:160158)结构：杯积

[上同调群](@entry_id:142450)的真正威力并不仅仅在于它们是可计算的[阿贝尔群](@entry_id:150284)，更在于它们之间存在一个自然的乘法结构——**杯积（cup product）**。杯积是一个[双线性映射](@entry_id:186502)：
$$
\cup: H^p(X; R) \times H^q(X; R) \to H^{p+q}(X; R)
$$
它将 $p$-[上同调类](@entry_id:263961)和 $q$-上同调类相乘，得到一个 $(p+q)$-[上同调类](@entry_id:263961)。这个运算赋予了所有上[同调群的直和](@entry_id:263088) $H^*(X; R) = \bigoplus_n H^n(X; R)$ 一个 **分次环（graded ring）** 的结构，称为 **[上同调环](@entry_id:160158)（cohomology ring）**。

[杯积](@entry_id:159554)满足[结合律](@entry_id:151180)和含幺律，并且具有 **[分次交换性](@entry_id:161347)（graded-commutativity）**：对于 $\alpha \in H^p(X)$ 和 $\beta \in H^q(X)$，有
$$
\alpha \cup \beta = (-1)^{pq} \beta \cup \alpha
$$
这意味着奇数次的类在交换时会引入一个负号，而当系[数环](@entry_id:636822)是 $\mathbb{Z}_2$ 时，杯积总是交换的。

#### 环结构的计算

在一个[上同调环](@entry_id:160158)中进行计算，本质上是在给定的生成元和关系下进行代数运算。例如，克莱因瓶 $K$ 的模2[上同调环](@entry_id:160158) $H^*(K; \mathbb{Z}_2)$，其一阶部分 $H^1(K; \mathbb{Z}_2)$ 由基 $\{u, v\}$ 生成，且满足关系 $u \cup u = v \cup v$ 和 $u \cup v = 0$。二阶部分的生成元为 $w = u \cup u$。要计算 $(u+v) \cup v$，我们利用[杯积](@entry_id:159554)的双线性：
$$
(u+v) \cup v = u \cup v + v \cup v
$$
代入给定的关系，我们得到：
$$
(u+v) \cup v = 0 + v \cup v = v \cup v = u \cup u = w
$$
因此，$(u+v) \cup v = 1 \cdot w$ [@problem_id:928027]。这个简单的计算展示了[上同调环](@entry_id:160158)的代数威力。

#### 几何解释：[相交形式](@entry_id:161075)

[杯积](@entry_id:159554)最深刻的意义在于其与[几何相交](@entry_id:159175)的联系。对于一个 $n$ 维的闭合、[可定向流形](@entry_id:276936) $M$，**[庞加莱对偶](@entry_id:161676)（Poincaré Duality）** 定理断言 $H^k(M)$ 与 $H_{n-k}(M)$ 之间存在一个自然同构。在这个框架下，杯积具有清晰的几何解释。

考虑一个 $2k$ 维的闭合[可定向流形](@entry_id:276936) $M$。我们可以在其中间维数的[上同调群](@entry_id:142450) $H^k(M; \mathbb{Z})$ 上定义一个对称[双线性](@entry_id:146819)配对，称为 **[相交形式](@entry_id:161075)（intersection form）**：
$$
Q_M: H^k(M; \mathbb{Z}) \times H^k(M; \mathbb{Z}) \to \mathbb{Z}
$$
$$
Q_M(\alpha, \beta) = \langle \alpha \cup \beta, [M] \rangle
$$
其中 $[M] \in H_{2k}(M; \mathbb{Z})$ 是[流形](@entry_id:153038)的基本同调类，$\langle \cdot, \cdot \rangle$ 表示[上同调类](@entry_id:263961)在同调类上的求值。[庞加莱对偶](@entry_id:161676)表明，[上同调类](@entry_id:263961) $\alpha, \beta$ 分别对应于 $k$ 维的子流形 $A, B$。在理想情况下（横截相交），$\alpha \cup \beta$ 对应于 $A$ 和 $B$ 的交集，而 $Q_M(\alpha, \beta)$ 则计算了这些交点的带符号计数。

这个形式是一个强大的[拓扑不变量](@entry_id:138526)。例如，在[四维流形](@entry_id:274951)的研究中，[相交形式](@entry_id:161075) $Q_M$ 在 $H^2(M; \mathbb{Z})$ 上的性质（如其[行列式](@entry_id:142978)、符号差等）几乎完全决定了[流形](@entry_id:153038)的[同伦型](@entry_id:148015)。

让我们计算 $M = (S^2 \times S^2) \# \mathbb{C}P^2$ 的[相交形式](@entry_id:161075)的[行列式](@entry_id:142978)，其中 $\#$ 表示 **[连通和](@entry_id:263574)（connected sum）**。
1.  对于 $S^2 \times S^2$，其 $H^2$ 由两个生成元 $\alpha, \beta$ 生成，它们分别是两个 $S^2$ 因子的[基本类](@entry_id:158335)的对偶。它们的杯积关系为 $\alpha \cup \alpha = 0, \beta \cup \beta = 0, \alpha \cup \beta = [\text{point}]$。对应的[相交矩阵](@entry_id:271171)为 $\begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$，[行列式](@entry_id:142978)为 $-1$。
2.  对于[复射影平面](@entry_id:262661) $\mathbb{C}P^2$，其 $H^2$ 由一个生成元 $x$ 生成，满足 $x \cup x$ 是 $H^4$ 的生成元。因此[相交矩阵](@entry_id:271171)为 $[1]$，[行列式](@entry_id:142978)为 $1$。
3.  [连通和](@entry_id:263574)的[相交形式](@entry_id:161075)是各个部分[相交形式](@entry_id:161075)的[直和](@entry_id:156782)。因此，$M$ 的[相交矩阵](@entry_id:271171)是上述两个矩阵的直和，其[行列式](@entry_id:142978)为 $(-1) \times 1 = -1$ [@problem_id:928130]。

[杯积](@entry_id:159554)的非退化性也是一个关键性质。对于一个闭合[可定向流形](@entry_id:276936)，$H^*(M)$ 上的杯积配对是 **非退化的（non-degenerate）**。例如，对于一个亏格为 $g$ 的闭合[可定向曲面](@entry_id:271413) $M_g$，其一阶[上同调群](@entry_id:142450) $H^1(M_g; \mathbb{R})$ 的维数为 $2g$。杯积 $\cup: H^1 \times H^1 \to H^2 \cong \mathbb{R}$ 在 $H^1$ 上定义了一个非退化的反[对称双线性形式](@entry_id:148281)，即一个 **[辛形式](@entry_id:165896)（symplectic form）**。这意味着对于任何非零的 $\omega \in H^1(M_g)$, [线性映射](@entry_id:185132) $L_\omega(\eta) = \omega \cup \eta$ 不会是零映射。由于 $H^2(M_g)$ 是一维的，这个映射的像必然是整个 $H^2(M_g)$，因此其维数为1 [@problem_id:928039]。

#### 积空间中的[杯积](@entry_id:159554)

对于[积空间](@entry_id:151693) $X \times Y$，其[上同调环](@entry_id:160158)可以通过 **Künneth 定理** 从因[子空间](@entry_id:150286)的环 $H^*(X)$ 和 $H^*(Y)$ 构造。这引入了 **叉积（cross product）**：
$$
\times: H^p(X) \times H^q(Y) \to H^{p+q}(X \times Y)
$$
积空间 $X \times Y$ 的[上同调环](@entry_id:160158)是 $H^*(X) \otimes H^*(Y)$。设 $p_1: X \times Y \to X$ 和 $p_2: X \times Y \to Y$ 是[投影映射](@entry_id:153398)。对于 $\alpha \in H^*(X)$ 和 $\beta \in H^*(Y)$，我们有 $p_1^*(\alpha) \cup p_2^*(\beta) = \alpha \times \beta$。这是一个连接[杯积](@entry_id:159554)和[叉积](@entry_id:156672)的基本关系。

考虑[流形](@entry_id:153038) $M = \mathbb{R}P^3 \times \mathbb{R}P^3$ 上的模2[上同调](@entry_id:160558)。设 $a$ 是 $H^1(\mathbb{R}P^3; \mathbb{Z}_2)$ 的生成元，定义 $x=p_1^*(a) \in H^1(M)$ 和 $y=p_2^*(a) \in H^1(M)$。我们要计算 $\langle x^3 \cup y^3, [M] \rangle$。
利用[叉积](@entry_id:156672)的语言，$x = a \times 1$，$y = 1 \times a$。由于系数是 $\mathbb{Z}_2$，[杯积](@entry_id:159554)与[叉积](@entry_id:156672)的[交换规则](@entry_id:184421)变得简单：$(\alpha_1 \times \beta_1) \cup (\alpha_2 \times \beta_2) = (\alpha_1 \cup \alpha_2) \times (\beta_1 \cup \beta_2)$。
因此，$x^3 = (a \times 1)^3 = a^3 \times 1$，$y^3 = (1 \times a)^3 = 1 \times a^3$。
它们的[杯积](@entry_id:159554)是 $x^3 \cup y^3 = (a^3 \times 1) \cup (1 \times a^3) = a^3 \times a^3$。
最后，在基本同调类 $[M] = [\mathbb{R}P^3] \times [\mathbb{R}P^3]$ 上求值：
$$
\langle a^3 \times a^3, [\mathbb{R}P^3] \times [\mathbb{R}P^3] \rangle = \langle a^3, [\mathbb{R}P^3] \rangle \cdot \langle a^3, [\mathbb{R}P^3] \rangle
$$
由于 $\mathbb{R}P^3$ 的顶阶上同调类在其[基本类](@entry_id:158335)上的求值为1，即 $\langle a^3, [\mathbb{R}P^3] \rangle = 1$，最终结果为 $1 \cdot 1 = 1$ [@problem_id:927995]。

### 系数间的关系：Bockstein 同态

上同调群强烈依赖于所选的系数群 $G$。改变系数群可以揭示空间的不同拓扑特性。**Bockstein 同态（Bockstein homomorphism）** 是研究不同系数群之间关系的核心工具。

任何系数群的短[正合序列](@entry_id:151503)，如 $0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0$，都会诱导一个[上同调](@entry_id:160558)的长正合序列：
$$
\cdots \to H^n(X; A) \xrightarrow{f_*} H^n(X; B) \xrightarrow{g_*} H^n(X; C) \xrightarrow{\beta} H^{n+1}(X; A) \to \cdots
$$
这里的[连接同态](@entry_id:160713) $\beta$ 就是 Bockstein 同态。它衡量了一个 $C$-[上同调类](@entry_id:263961)在多大程度上“不是”一个 $B$-上同调类的像。

最常见的例子来自系数序列 $0 \to \mathbb{Z} \xrightarrow{\times m} \mathbb{Z} \to \mathbb{Z}_m \to 0$。这给出了连接积分[上同调](@entry_id:160558)和模 $m$ 上同调的 Bockstein 同态 $\beta: H^n(X; \mathbb{Z}_m) \to H^{n+1}(X; \mathbb{Z})$。这个同态的非平凡性往往能探测到积分上同调中的 $m$-挠率。

以[克莱因瓶](@entry_id:149661) $K$ 为例，考虑 $m=2$ 的情况。我们想计算 Bockstein $\beta: H^1(K; \mathbb{Z}_2) \to H^2(K; \mathbb{Z})$ 的像的阶。相关的[长正合序列](@entry_id:153438)片段是：
$$
H^1(K; \mathbb{Z}) \xrightarrow{\rho} H^1(K; \mathbb{Z}_2) \xrightarrow{\beta} H^2(K; \mathbb{Z}) \xrightarrow{\times 2} H^2(K; \mathbb{Z})
$$
通过 UCT 或其他方法，我们可以计算出 $H^1(K; \mathbb{Z}) \cong \mathbb{Z}$，$H^1(K; \mathbb{Z}_2) \cong \mathbb{Z}_2 \oplus \mathbb{Z}_2$，以及 $H^2(K; \mathbb{Z}) \cong \mathbb{Z}_2$。
1.  映射 $\rho$ 是模2约化映射，它的像 $\text{Im}(\rho)$ 是 $H^1(K; \mathbb{Z}_2)$ 中的一个 $\mathbb{Z}_2$ [子群](@entry_id:146164)。
2.  根据正合性，$\text{Im}(\beta) = \text{Ker}(\times 2: H^2(K; \mathbb{Z}) \to H^2(K; \mathbb{Z}))$。
3.  由于 $H^2(K; \mathbb{Z}) \cong \mathbb{Z}_2$，在其上乘以2的映射是零映射。因此，$\text{Ker}(\times 2) = H^2(K; \mathbb{Z}) \cong \mathbb{Z}_2$。
所以，$\text{Im}(\beta) \cong \mathbb{Z}_2$，其阶数为 2 [@problem_id:928001]。这表明 $H^1(K; \mathbb{Z}_2)$ 中有一个元素（具体来说，是那个不来自积分上同调的元素），其 Bockstein 是 $H^2(K; \mathbb{Z})$ 中的非零[挠元](@entry_id:148301)。

总而言之，上同调论提供了一个多层次的框架来剖析拓扑空间。从基本的群[不变量](@entry_id:148850)，到Mayer-Vietoris和Künneth等强大的计算引擎，再到赋予其代数生命的杯积结构及其深刻的几何内涵，最后到通过[Bockstein同态](@entry_id:272275)联系不同系数下的视图，这些原理和机制共同构成了现代拓扑学和几何学研究的基石。