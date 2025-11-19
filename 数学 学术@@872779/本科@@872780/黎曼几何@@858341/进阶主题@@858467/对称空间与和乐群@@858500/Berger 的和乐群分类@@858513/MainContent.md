## 引言
在[黎曼几何](@entry_id:160508)的宏伟画卷中，[和乐群](@entry_id:191471)（holonomy group）是一个衡量[流形](@entry_id:153038)局部几何“扭曲”程度的根本工具。它通过平行输运的概念，捕捉了一个向量沿闭合路径移动后所发生的转动，从而揭示了空间内在的曲率信息。一个自然而深刻的问题随之产生：对于一个黎曼流形，其和乐群可能有哪些？这个问题引向了20世纪微分几何最辉煌的成就之一——[Berger分类](@entry_id:198491)定理。该定理惊人地指出，在排除了可分解和高度对称的特殊情况后，不可约的黎曼流形所允许的和乐群种类极为有限，每一种都对应着一种独特的、高度结构化的几何世界。

本文旨在系统性地介绍[Berger分类](@entry_id:198491)及其深远意义。在第一章“原理与机制”中，我们将建立[平行输运](@entry_id:160671)与[和乐群](@entry_id:191471)的严格定义，探讨黎曼度量与曲率如何通过[Ambrose-Singer定理](@entry_id:198517)强力约束[和乐群](@entry_id:191471)，并最终引出[Berger分类](@entry_id:198491)列表。第二章“应用与跨学科联系”将展示该分类的威力，通过探索Calabi-Yau流形、例外和乐群等[特殊几何](@entry_id:194564)，揭示其与Einstein方程、标定几何、[旋量](@entry_id:158054)分析乃至弦理论的紧密联系。最后，在第三章“动手实践”中，读者将通过具体的计算示例，亲身体验从平坦空间到乘[积流形](@entry_id:270208)的不同[和乐](@entry_id:137051)行为，从而巩固理论知识。通过这一旅程，我们将看到[Berger分类](@entry_id:198491)不仅是对称性的深刻体现，更是连接纯粹数学与理论物理的坚实桥梁。

## 原理与机制

在理解了和乐群作为描述[黎曼流形](@entry_id:261160)局部几何“扭曲”程度的工具之后，本章将深入探讨其背后的基本原理与核心机制。我们将从一般的线性联络出发，逐步引入[黎曼度量](@entry_id:754359)的约束，并最终揭示曲率如何决定和乐群，以及特殊的几何结构如何将其约束到 Berger 分类所给出的一个非常短的列表中。

### [和乐群](@entry_id:191471)的基本概念

我们将首先建立平行输运和和乐群的严格定义，这些是后续讨论的基石。

#### 平行输运

考虑一个光滑连通[流形](@entry_id:153038) $M$ 及其上的一个线性联络 $\nabla$。对于 $M$ 中任意一条分段光滑的曲线 $\gamma: [0, 1] \to M$，沿 $\gamma$ 的一个向量场 $V(t)$ 如果满足协变常微分方程 $\nabla_{\dot{\gamma}(t)}V(t) = 0$，则称其为 **$\nabla$-平行的**。基于[线性常微分方程](@entry_id:276013)[解的存在唯一性](@entry_id:177406)定理，对于任意给定的初始向量 $v \in T_{\gamma(0)}M$，都存在唯一的沿 $\gamma$ 的[平行向量场](@entry_id:636129) $V(t)$ 满足 $V(0)=v$。

这使我们能够定义一个从起点[切空间](@entry_id:199137)到终点切空间的映射，即**平行输运**（**parallel transport**）。该映射记为 $P_{\gamma}: T_{\gamma(0)}M \to T_{\gamma(1)}M$，定义为 $P_{\gamma}(v) = V(1)$。由于协变[微分的线性](@entry_id:161574)性质，这个映射是线性的。此外，沿着反向路径 $\gamma^{-1}$ 的平行输运恰好是 $P_{\gamma}$ 的逆映射，因此 $P_{\gamma}$ 是一个[线性同构](@entry_id:270529)。值得强调的是，[平行输运](@entry_id:160671)映射 $P_{\gamma}$ 完全由联络 $\nabla$ 决定；改变联络通常会改变平行输运的结果 [@problem_id:3038228]。

#### [和乐群](@entry_id:191471)与限定[和乐群](@entry_id:191471)

当曲线 $\gamma$ 是一条始点和终点重合的环路（loop）时，即 $\gamma(0) = \gamma(1) = p$，平行输运 $P_{\gamma}$ 就成为[切空间](@entry_id:199137) $T_pM$ 上的一个自同构。在点 $p$ 的**和乐群**（**holonomy group**），记为 $\mathrm{Hol}_p(\nabla)$，定义为所有沿以 $p$ 为基点的分段光滑环路 $\gamma$ 的[平行输运](@entry_id:160671)映射 $P_{\gamma}$ 所构成的集合。

不难验证 $\mathrm{Hol}_p(\nabla)$ 构成一个群。首先，沿常值环路（$\gamma(t) = p$）的[平行输运](@entry_id:160671)是[恒等映射](@entry_id:634191)，因此单位元属于该集合。其次，两个环路 $\gamma_1$ 和 $\gamma_2$ 的复合环路 $\gamma_1 * \gamma_2$ 对应的[平行输运](@entry_id:160671)是 $P_{\gamma_2} \circ P_{\gamma_1}$，保证了运算的封闭性。最后，任一环路 $\gamma$ 的逆环路 $\gamma^{-1}$ 对应的[平行输运](@entry_id:160671)是 $P_{\gamma}^{-1}$，确保了每个元素都有逆。因此，$\mathrm{Hol}_p(\nabla)$ 是[切空间](@entry_id:199137) $T_pM$ 上[一般线性群](@entry_id:141275) $\mathrm{GL}(T_pM)$ 的一个[子群](@entry_id:146164) [@problem_id:3038228]。

一个更精细的概念是**限定[和乐群](@entry_id:191471)**（**restricted holonomy group**），记为 $\mathrm{Hol}_p^0(\nabla)$。它是由沿那些在 $M$ 中可缩（contractible）的环路的[平行输运](@entry_id:160671)生成的[子群](@entry_id:146164)。这个[子群](@entry_id:146164)在[和乐群](@entry_id:191471)的结构中扮演着核心角色：可以证明，当 $M$ 连通时，$\mathrm{Hol}_p^0(\nabla)$ 恰好是 $\mathrm{Hol}_p(\nabla)$ 作为[李群](@entry_id:137659)的单位连通分支。同时，它也是 $\mathrm{Hol}_p(\nabla)$ 的一个[正规子群](@entry_id:147397) [@problem_id:3038228] [@problem_id:3038231]。

#### 和乐群与[流形](@entry_id:153038)拓扑

和乐群不仅反映了联络的几何性质，还与[流形的拓扑](@entry_id:267834)结构密切相关。首先，在连通[流形](@entry_id:153038) $M$ 中，不同点 $p$ 和 $q$ 的[和乐群](@entry_id:191471)是共轭的。具体而言，若 $\sigma$ 是一条从 $p$ 到 $q$ 的路径，则有 $\mathrm{Hol}_q(\nabla) = P_{\sigma} \circ \mathrm{Hol}_p(\nabla) \circ P_{\sigma}^{-1}$。这意味着不同点的和乐群作为抽象群是同构的，因此我们常不加区分地谈论[流形](@entry_id:153038)的“和乐群”。

更深刻的联系体现在和乐群与[基本群](@entry_id:146111) $\pi_1(M,p)$ 的关系上。存在一个自然的、满的[群同态](@entry_id:140603) $\Phi: \pi_1(M,p) \to \mathrm{Hol}_p(\nabla) / \mathrm{Hol}_p^0(\nabla)$，它将环路的[同伦类](@entry_id:149365) $[\gamma]$ 映射到 $P_{\gamma}$ 所在的陪集 [@problem_id:2968911]。这个[同态的核](@entry_id:145895)由那些[平行输运](@entry_id:160671)落在限定[和乐群](@entry_id:191471)中的[同伦类](@entry_id:149365)构成。这个映射一般不是同构。例如，在一个标准的[平坦环面](@entry_id:261129)上，$\pi_1(T^2)$ 是非平凡的，但其[和乐群](@entry_id:191471)是平凡的 [@problem_id:3038228]。

这个关系引出了[万有覆盖](@entry_id:151142)（universal cover）在和乐群理论中的重要作用。设 $\pi: \widetilde{M} \to M$ 是 $M$ 的[万有覆盖](@entry_id:151142)。由于 $\widetilde{M}$ 是单连通的，其上任意环路都是可缩的，因此其[和乐群](@entry_id:191471) $\mathrm{Hol}_{\tilde{p}}(\tilde{\nabla})$ 与其限定[和乐群](@entry_id:191471)相等。可以证明，这个群通过[微分](@entry_id:158718)映射 $d\pi_{\tilde{p}}$ 的[共轭作用](@entry_id:143328)，与基[流形](@entry_id:153038) $M$ 的限定和乐群 $\mathrm{Hol}_p^0(\nabla)$ 同构。即 $\mathrm{Hol}_{\tilde{p}}(\tilde{\nabla}) \cong \mathrm{Hol}_p^0(\nabla)$ [@problem_id:2968911]。这使得我们可以通过研究单连通[流形](@entry_id:153038)的和乐群来理解一般[流形](@entry_id:153038)的限定和乐群。如果 $M$ 本身是单连通的，那么它的和乐群就是连通的，即 $\mathrm{Hol}_p(\nabla) = \mathrm{Hol}_p^0(\nabla)$ [@problem_id:2968911]。

### [黎曼和](@entry_id:137667)乐群的约束

到目前为止，我们的讨论适用于任何线性联络。然而，黎曼几何的核心是与度量 $g$ 兼容的 Levi-Civita 联络 $\nabla$。这个联络的特殊性质——无挠（torsion-free）和度量相容（metric-compatible）——对[和乐群](@entry_id:191471)施加了强大的约束。

#### 度量相容性的影响

Levi-Civita 联络的定义性特征是它保持度量不变，即 $\nabla g = 0$。这一性质的直接后果是，沿任意曲线的平行输运保持向量间的[内积](@entry_id:158127)不变。具体来说，如果 $V(t)$ 和 $W(t)$ 是沿曲线 $\gamma$ 的两个[平行向量场](@entry_id:636129)，那么它们[内积](@entry_id:158127)的导数为：
$$
\frac{d}{dt} g(V(t), W(t)) = g(\nabla_{\dot{\gamma}}V, W) + g(V, \nabla_{\dot{\gamma}}W) = g(0, W) + g(V, 0) = 0
$$
这意味着[内积](@entry_id:158127) $g(V(t), W(t))$ 沿曲线是一个常数。对于一条以 $p$ 为基点的环路 $\gamma$，这意味着对任意 $v, w \in T_pM$，都有 $g_p(v, w) = g_p(P_{\gamma}(v), P_{\gamma}(w))$。这正是说 $P_{\gamma}$ 是 $T_pM$ 上的一个[正交变换](@entry_id:155650)。因此，黎曼流形的[和乐群](@entry_id:191471) $\mathrm{Hol}_p(g)$ 必然是[正交群](@entry_id:152531) $\mathrm{O}(T_pM, g_p)$ 的一个[子群](@entry_id:146164) [@problem_id:3038259] [@problem_id:3038231]。这是一个至关重要的约束，将[和乐群](@entry_id:191471)从[一般线性群](@entry_id:141275) $\mathrm{GL}(n, \mathbb{R})$ 压缩到了更小的[正交群](@entry_id:152531) $\mathrm{O}(n)$ 中。

如果[流形](@entry_id:153038) $M$ 是可定向的，这意味着存在一个整体定义的、与度量兼容的体积形式 $\mathrm{vol}_g$。Levi-Civita 联络同样保持体积形式不变，即 $\nabla \mathrm{vol}_g = 0$。这意味着沿任何环路的平行输运 $P_{\gamma}$ 保持定向，其[行列式](@entry_id:142978)必须为 $+1$。因此，对于可定向的黎曼流形，其和乐群 $\mathrm{Hol}_p(g)$ 进一步被限制在[特殊正交群](@entry_id:146418) $\mathrm{SO}(T_pM, g_p)$ 内。即使[流形](@entry_id:153038)不可定向，其限定和乐群 $\mathrm{Hol}_p^0(g)$ 由于是连通的，也必然是 $\mathrm{SO}(T_pM, g_p)$ 的[子群](@entry_id:146164) [@problem_id:3038259] [@problem_id:3038231]。

需要注意的是，这些强有力的约束来自于度量相容性，而非无挠性。允许有挠的度量联络（即 $\nabla g = 0$ 但挠率 $T \neq 0$）会极大地扩展可能的和乐群，事实上，$\mathrm{SO}(n)$ 的任何连通李[子群](@entry_id:146164)都可以实现为某个有挠度量联络的[和乐群](@entry_id:191471)。这反过来凸显了 Levi-Civita 联络的无挠性在[限制和乐群](@entry_id:637133)可能性方面所起的关键作用，为 Berger 的分类铺平了道路 [@problem_id:3038231]。

#### 曲率的角色：Ambrose-Singer 定理

和乐群的几何意义在于它量化了[平行输运的路径依赖性](@entry_id:204826)。直观上，当一个向量沿一个无穷小环路平行移动一周后，它与初始向量的偏差是由该环路所包围区域的曲率决定的。这一思想被 **Ambrose-Singer 定理**（**Ambrose-Singer Theorem**）精确化。

该定理指出，[和乐群](@entry_id:191471) $\mathrm{Hol}_p(g)$ 的李代数 $\mathfrak{hol}_p(g)$，即所谓的**[和乐李代数](@entry_id:188537)**（**holonomy Lie algebra**），是由[流形](@entry_id:153038)上所有点的[曲率算子](@entry_id:198006)经过[平行输运](@entry_id:160671)“[拉回](@entry_id:160816)”到点 $p$ 后生成的。更准确地说，$\mathfrak{hol}_p(g)$ 是由形如 $P_{\gamma}^{-1} \circ R_x(u, v) \circ P_{\gamma}$ 的所有算子生成的最小[李代数](@entry_id:137954)，其中 $x$ 是[流形](@entry_id:153038)上的任意点，$u, v \in T_xM$，而 $\gamma$ 是一条从 $p$ 到 $x$ 的路径 [@problem_id:3038244]。

Ambrose-Singer 定理揭示了[和乐](@entry_id:137051)与曲率之间的深刻联系。它告诉我们，[和乐群](@entry_id:191471)完全由[流形](@entry_id:153038)的曲率结构所决定。一个直接的推论是，如果一个黎曼流形的黎曼曲率张量在所有点上都为零（即 $R \equiv 0$），那么其[和乐李代数](@entry_id:188537)必然为 $\{0\}$。这意味着其限定和乐群是平凡群 $\{\mathrm{Id}\}$ [@problem_id:3038244] [@problem_id:3038228]。

反之，仅仅在一点 $p$ 的曲率为零（$R_p=0$）并不意味着和乐群是平凡的。只要[流形](@entry_id:153038)在其他地方是弯曲的，通过一条进入弯曲区域的环路，我们仍然可以在 $p$ 点获得非平凡的和乐变换。只有在一种特殊情况下，即**[局部对称空间](@entry_id:637873)**（**locally symmetric space**，其[曲率张量](@entry_id:181383)是平行的，$\nabla R = 0$），[和乐李代数](@entry_id:188537)才完全由单一点 $p$ 的[曲率张量](@entry_id:181383) $\{R_p(u,v) \mid u,v \in T_pM\}$ 生成 [@problem_id:3038244]。

### 结构约化原理

我们已经看到，Levi-Civita 联络本身将和乐群从 $\mathrm{GL}(n)$ 约化到了 $\mathrm{SO}(n)$。Berger 分类的核心思想是，某些特殊的几何结构会进一步将[和乐群](@entry_id:191471)约化到 $\mathrm{SO}(n)$ 的更小[子群](@entry_id:146164)中。这种约化现象有两个主要来源：几何上的可分解性和代数上的[不变张量](@entry_id:203823)。

#### 不可约性和 de Rham 分解定理

[和乐群](@entry_id:191471) $\mathrm{Hol}_p(g)$ 在[切空间](@entry_id:199137) $T_pM$ 上的作用构成了一个表示，称为**[和乐](@entry_id:137051)表示**（**holonomy representation**）。这个表示可能是**可约的**（**reducible**）或**不可约的**（**irreducible**）。根据线性代数的定义，一个表示是不可约的，当且仅当不存在非平凡的（即非 $\{0\}$ 且非全空间）不变子空间 [@problem_id:3038232]。

如果[和乐](@entry_id:137051)表示是可约的，假设 $E_p \subset T_pM$ 是一个非平凡的不变子空间，那么这个[子空间](@entry_id:150286)可以在整个[流形](@entry_id:153038)上被“平行地”推广。通过将 $E_p$ 沿所有路径进行[平行输运](@entry_id:160671)，可以定义一个良定义的、光滑的[分布](@entry_id:182848) $E \subset TM$。这个[分布](@entry_id:182848)是**平行的**（**parallel**），意味着对于 $E$ 的任意[截面](@entry_id:154995) $Y$ 和任意向量场 $X$，协变导数 $\nabla_X Y$ 仍然是 $E$ 的一个[截面](@entry_id:154995)。

由于 Levi-Civita 联络保持度量， $E_p$ 的正交补 $E_p^{\perp}$ 也是一个不变子空间。因此，我们同样可以得到一个平行的正交补[分布](@entry_id:182848) $E^{\perp}$。这两个平行的[分布](@entry_id:182848)都是**对合的**（**involutive**），即它们的[截面](@entry_id:154995)的[李括号](@entry_id:636461)仍然是该[分布](@entry_id:182848)的[截面](@entry_id:154995)。根据 Frobenius 定理，它们都是可积的，并且其[积分流形](@entry_id:270062)是**[全测地的](@entry_id:183906)**（**totally geodesic**）。

这一系列推导的最终结果是 **de Rham 分解定理**（**de Rham Decomposition Theorem**）的局部形式：如果一个黎曼流形的和乐表示是可约的，那么这个[流形](@entry_id:153038)在局部上[等距同构](@entry_id:273188)于一个黎曼乘[积流形](@entry_id:270208) [@problem_id:3038232]。这意味着具有可约[和乐群](@entry_id:191471)的[流形](@entry_id:153038)可以被分解为具有不可约和乐群的更低维[流形](@entry_id:153038)的乘积。因此，为了对一般的和乐群进行分类，我们首先应该研究那些不可约的情况。这正是 Berger 分类中“不可约”假设的来源。

#### 平行张量场与[稳定子群](@entry_id:137216)

除了导致几何分解的可约性之外，另一种更精细的约化机制源于平行[张量场](@entry_id:190170)。基本原理是：如果[流形](@entry_id:153038) $(M,g)$ 上存在一个非平凡的平行[张量场](@entry_id:190170) $\varphi$（即 $\nabla \varphi = 0$），那么沿任何环路的[平行输运](@entry_id:160671)都必须保持该张量在基点 $p$ 的值 $\varphi_p$ 不变。

这意味着和乐群 $\mathrm{Hol}_p(g)$ 必须是 $\varphi_p$ 在 $\mathrm{SO}(T_pM)$ 中的**[稳定子群](@entry_id:137216)**（**stabilizer subgroup**）的[子群](@entry_id:146164)：
$$
\mathrm{Hol}_p(g) \subseteq \mathrm{Stab}_{\mathrm{SO}(n)}(\varphi_p) = \{ A \in \mathrm{SO}(n) \mid A(\varphi_p) = \varphi_p \}
$$
这里 $A(\varphi_p)$ 表示群元素 $A$ 对张量 $\varphi_p$ 的自然作用 [@problem_id:2968963] [@problem_id:3038250]。

这个原理是理解 Berger 分类的关键。任何使得[和乐群](@entry_id:191471)发生约化的[特殊几何](@entry_id:194564)结构，最终都可以归结为存在一个或多个被和乐群保持不变的代数对象。例如，考虑一个非零的平行 $k$-形式 $\varphi$（$1 \le k \le n-1$）。根据 $\mathrm{SO}(n)$ 的表示论，除了 $k=0$（标量）和 $k=n$（[体积形式](@entry_id:203000)）之外，任何非零的 $k$-形式在 $\mathrm{SO}(n)$ 的作用下都不是不变的。这意味着其[稳定子群](@entry_id:137216) $\mathrm{Stab}_{\mathrm{SO}(n)}(\varphi_p)$ 必然是 $\mathrm{SO}(n)$ 的一个[真子群](@entry_id:141915)。因此，存在一个非平凡的平行 $k$-形式（$1 \le k \le n-1$）会迫使[和乐群](@entry_id:191471)被约化到一个更小的[子群](@entry_id:146164)中 [@problem_id:2968963]。

### Berger 分类定理

综合以上所有原理——[黎曼度量](@entry_id:754359)的约束、曲率的决定性作用、不可约性假设以及平行张量导致的约化——Marcel Berger 在 20 世纪 50 年代对一类重要的黎曼流形的[和乐群](@entry_id:191471)进行了完全分类。

#### 定理的假设

Berger 的分类定理适用于满足以下条件的黎曼流形 $(M,g)$：
1.  **单连通**（**Simply connected**）：如前所述，这确保了[和乐群](@entry_id:191471)是连通的，即 $\mathrm{Hol}_p(g) = \mathrm{Hol}_p^0(g)$ [@problem_id:2968911]。
2.  **不可约**（**Irreducible**）：这意味着和乐表示是不可约的，从而排除了那些可以分解为乘积的[流形](@entry_id:153038) [@problem_id:3038232]。
3.  **非局部对称**（**Not locally symmetric**）：这排除了[曲率张量](@entry_id:181383)平行的空间（$\nabla R=0$）。[局部对称空间](@entry_id:637873)自身构成了一大类重要的几何对象，其和乐群（即其[齐性空间](@entry_id:271488)表示 $G/H$ 中的[迷向子群](@entry_id:200360) $H$）有其自身的、更庞大的分类，由 [Élie Cartan](@entry_id:263871) 完成。例如，格拉斯曼[流形](@entry_id:153038) $Gr_p(\mathbb{R}^{p+q}) = SO(p+q)/(SO(p) \times SO(q))$ 的和乐群是 $SO(p) \times SO(q)$，这个群并不在 Berger 的列表中。将这些空间排除，使得 Berger 的分类关注于更“一般”的弯曲[流形](@entry_id:153038) [@problem_id:3038252]。

#### Berger 列表：可能的[和乐群](@entry_id:191471)

Berger 证明，在上述假设下，[黎曼流形](@entry_id:261160)的和乐群（作为 $\mathrm{SO}(n)$ 的[子群](@entry_id:146164)）只有以下几种可能。每一种可能性都对应着一种特殊的几何结构，通常由一个或多个平行张量来刻画。

- **一般情况：**
    - $\mathbf{SO(n)}$：这是 $n$ 维可定向黎曼流形最一般（generic）的和乐群，对应于不存在除度量 $g$ 和[体积形式](@entry_id:203000)外的任何额外平行张量的情况 [@problem_id:3049801]。

- **Kähler 几何系列：**
    - $\mathbf{U(n)}$：[流形](@entry_id:153038)维数为 $2n$。这对应于 **Kähler [流形](@entry_id:153038)**。其几何结构由一个与度量兼容的平行[殆复结构](@entry_id:159849) $J$（即 $\nabla J=0$）定义。$U(n)$ 是 $\mathrm{SO}(2n)$ 中与 $J$ 交换的所有变换构成的[子群](@entry_id:146164) [@problem_id:3049801] [@problem_id:3038250]。
    - $\mathbf{SU(n)}$：[流形](@entry_id:153038)维数为 $2n$。这对应于 **Calabi-Yau [流形](@entry_id:153038)**（或更广义的具有特殊酉和乐群的[流形](@entry_id:153038)）。在 Kähler [流形](@entry_id:153038)的基础上，还存在一个平行的复体积形式 $\Omega$。具有这种和乐群的[流形](@entry_id:153038)是**[里奇平坦](@entry_id:159097)**（**Ricci-flat**）的 [@problem_id:3049801] [@problem_id:3038250]。

- **[四元数](@entry_id:147023) Kähler 几何系列：**
    - $\mathbf{Sp(n)}$：[流形](@entry_id:153038)维数为 $4n$。这对应于 **Hyperkähler [流形](@entry_id:153038)**。其几何特征是存在三个平行的、满足[四元数代数](@entry_id:196348)关系的[殆复结构](@entry_id:159849) $I, J, K$。这类[流形](@entry_id:153038)也是[里奇平坦](@entry_id:159097)的 [@problem_id:3049801] [@problem_id:3038250]。
    - $\mathbf{Sp(n) \cdot Sp(1)}$：[流形](@entry_id:153038)维数为 $4n$。这对应于**四元数-Kähler [流形](@entry_id:153038)**（**quaternionic-Kähler manifold**）。与 Hyperkähler 不同，它不要求单个的 $I, J, K$ 平行，而是要求它们张成的三维子丛在[平行输运](@entry_id:160671)下保持不变。这类[流形](@entry_id:153038)是**爱因斯坦[流形](@entry_id:153038)**（**Einstein manifold**），但不一定是[里奇平坦](@entry_id:159097)的 [@problem_id:3049801] [@problem_id:3038250]。

- **特殊情况（Exceptional Holonomy）：**
    - $\mathbf{G_2}$：[流形](@entry_id:153038)维数为 $7$。其几何由一个特定的平行 3-形式（称为稳定 3-形式）定义。具有 $G_2$ 和乐群的[流形](@entry_id:153038)是[里奇平坦](@entry_id:159097)的 [@problem_id:3049801] [@problem_id:3038250]。
    - $\mathbf{Spin(7)}$：[流形](@entry_id:153038)维数为 $8$。其几何由一个特定的平行 4-形式（称为 Cayley 形式）定义。具有 $\mathrm{Spin}(7)$ 和乐群的[流形](@entry_id:153038)也是[里奇平坦](@entry_id:159097)的 [@problem_id:3049801] [@problem_id:3038250]。

#### 总结与展望

Berger 的分类定理是一个里程碑式的成就。它揭示了在看似无穷的可能性中，[黎曼几何](@entry_id:160508)的内在约束（通过 Levi-Civita 联络和曲率体现）只允许极少数几种基本的、不可约的几何结构存在。这个简短的列表不仅在纯粹数学中具有深刻的意义，而且在理论物理，特别是[弦理论](@entry_id:145688)和 M 理论中，找到了令人惊奇的应用，其中具有[特殊和乐群](@entry_id:158889)（如 $SU(n)$, $G_2$, $\mathrm{Spin}(7)$）的[里奇平坦流形](@entry_id:636329)为时空[紧化](@entry_id:150518)提供了理想的候选模型。对这些[特殊几何](@entry_id:194564)的研究至今仍然是[微分几何](@entry_id:145818)中最活跃和富有成果的领域之一。