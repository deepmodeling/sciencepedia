## 引言
李群，作为同时具备光滑流形与群结构的数学对象，在几何学与物理学中扮演着核心角色。赋予李群一个黎曼度量，便可在其上进行距离、角度和曲率的测量。然而，当度量与群的[代数结构](@entry_id:137052)相容，即在群乘法下保持不变时，其几何性质便会呈现出非凡的对称性与简洁性。这类特殊的度量被称为[双不变度量](@entry_id:184842)，它们是理解对称空间和建立几何与代数之间桥梁的关键。

尽管[双不变度量](@entry_id:184842)极为重要，但其存在性并非理所当然，其几何后果也并非显而易见。本文旨在系统性地解决这些问题：一个[李群](@entry_id:137659)在何种条件下才允许[双不变度量](@entry_id:184842)的存在？一旦存在，这些度量如何分类？它们又如何深刻地简化[流形](@entry_id:153038)的几何结构，并应用于其他数学和物理分支？

为解答这些问题，本文将分为三个部分。第一章，**原理与机制**，将从定义出发，建立[双不变度量](@entry_id:184842)与李代数上不变[内积](@entry_id:158127)的核心对应关系，并探讨其存在性、分类方法以及基本的几何性质。第二章，**应用与[交叉](@entry_id:147634)学科联系**，将通过具体的例子（如$SU(2)$）展示这些原理的强大威力，揭示[双不变度量](@entry_id:184842)如何在[测地线](@entry_id:269969)计算、曲率分析、[谱几何](@entry_id:186460)乃至规范场论中发挥作用。最后，在**动手实践**部分，读者将通过解决具体问题来巩固对[紧李群](@entry_id:146703)、非[紧李群](@entry_id:146703)以及[李群](@entry_id:137659)直积上[双不变度量](@entry_id:184842)理论的理解。

## 原理与机制

在本章中，我们将深入探讨[李群](@entry_id:137659)上的[双不变度量](@entry_id:184842)的基本原理与核心机制。[双不变度量](@entry_id:184842)在黎曼几何、[李理论](@entry_id:148240)和物理学中扮演着至关重要的角色，因为它们赋予了李群一种高度对称的几何结构。我们将从定义出发，建立[双不变度量](@entry_id:184842)与[李代数](@entry_id:137954)上特定代数性质之间的根本联系，然后探讨其存在性、分类方法，最后展示其深刻的几何与分析性质。

### 定义与基本对应关系

一个[李群](@entry_id:137659) $G$ 上的黎曼度量 $g$ 是在每个[切空间](@entry_id:199137) $T_pG$ 上光滑地指定一个[内积](@entry_id:158127) $g_p = \langle \cdot, \cdot \rangle_p$。李群的群结构允许我们定义特殊的度量，这些度量在群乘法的作用下保持不变。

对于任意 $h \in G$，左平移 $L_h: G \to G$ 定义为 $L_h(p) = hp$，右平移 $R_h: G \to G$ 定义为 $R_h(p) = ph$。这些都是微分同胚。一个黎曼度量 $g$ 被称为 **左不变的 (left-invariant)**，如果它在所有左平移下都保持不变。这意味着对于任意 $h \in G$，度量 $g$ 等于其在 $L_h$ 下的回拉 (pullback) $L_h^*g$。根据回拉的定义，这等价于对所有 $p \in G$ 和所有[切向量](@entry_id:265494) $X, Y \in T_pG$，满足：
$$
\langle X, Y \rangle_p = (L_h^*g)_p(X, Y) = \langle (dL_h)_p X, (dL_h)_p Y \rangle_{hp}
$$
同理，一个度量被称为 **右不变的 (right-invariant)**，如果它在所有右平移下保持不变，即对所有 $h \in G$ 满足 $g = R_h^*g$，或者说：
$$
\langle X, Y \rangle_p = (R_h^*g)_p(X, Y) = \langle (dR_h)_p X, (dR_h)_p Y \rangle_{ph}
$$
一个既是左不变又是右不变的黎曼度量，被称为 **[双不变度量](@entry_id:184842) (bi-invariant metric)** [@problem_id:2969097]。

[左不变度量](@entry_id:637439)有一个极其重要的性质：它们完全由其在单位元 $e$ 处的取值所决定。设 $\mathfrak{g} = T_eG$ 是 $G$ 的[李代数](@entry_id:137954)，任何 $\mathfrak{g}$ 上的一个[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle_e$ 都可以通过左平移唯一地扩展为 $G$ 上的一个[左不变度量](@entry_id:637439)。具体地，对于任意点 $p \in G$，我们可以通过将[切向量](@entry_id:265494)从 $T_pG$ “[拉回](@entry_id:160816)”到 $T_eG$ 来定义该点的[内积](@entry_id:158127)。这是通过左平移的[微分](@entry_id:158718) $(dL_{p^{-1}})_p: T_pG \to T_eG$ 实现的。因此，对于任意 $X, Y \in T_pG$，[左不变度量](@entry_id:637439)由下式定义 [@problem_id:2969097]：
$$
\langle X, Y \rangle_p := \langle (dL_{p^{-1}})_p X, (dL_{p^{-1}})_p Y \rangle_e
$$
这个构造建立了一个基本的[一一对应](@entry_id:143935)关系：$G$ 上的左不变[黎曼度量](@entry_id:754359)与 $\mathfrak{g}$ 上的[内积](@entry_id:158127)之间存在一一对应。

现在，核心问题变为：一个由 $\mathfrak{g}$ 上的[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle_e$ 生成的[左不变度量](@entry_id:637439)，在什么条件下也是右不变的，从而成为[双不变度量](@entry_id:184842)？

为了回答这个问题，我们只需检验右[不变性条件](@entry_id:171412)在单位元 $e$ 处是否成立即可，因为度量已经是左不变的。对于任意 $h \in G$，右[不变性](@entry_id:140168)要求 $(R_h^*g)_e = g_e$。对任意 $X, Y \in \mathfrak{g} = T_eG$，这意味着：
$$
\langle X, Y \rangle_e = (R_h^*g)_e(X, Y) = \langle (dR_h)_e X, (dR_h)_e Y \rangle_h
$$
现在，我们使用左[不变性](@entry_id:140168)将右侧在 $h$ 点的[内积](@entry_id:158127)转换回 $e$ 点：
$$
\langle (dR_h)_e X, (dR_h)_e Y \rangle_h = \langle (dL_{h^{-1}})_h ((dR_h)_e X), (dL_{h^{-1}})_h ((dR_h)_e Y) \rangle_e
$$
注意到复合映射 $L_{h^{-1}} \circ R_h$ 是共轭映射 $C_{h^{-1}}(p) = h^{-1}ph$。其在单位元 $e$ 处的[微分](@entry_id:158718)恰好是伴随表示 $\operatorname{Ad}_{h^{-1}}$。因此，上述等式变为：
$$
\langle X, Y \rangle_e = \langle \operatorname{Ad}_{h^{-1}}(X), \operatorname{Ad}_{h^{-1}}(Y) \rangle_e
$$
由于这个等式必须对所有 $h \in G$ 成立，而 $h \mapsto h^{-1}$ 是一个[双射](@entry_id:138092)，这等价于[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle_e$ 在伴随表示 $\operatorname{Ad}(G)$ 的作用下是不变的，即对于所有 $h \in G$ 和 $X, Y \in \mathfrak{g}$，有：
$$
\langle \operatorname{Ad}_h(X), \operatorname{Ad}_h(Y) \rangle_e = \langle X, Y \rangle_e
$$
这个结论是[双不变度量](@entry_id:184842)理论的基石 [@problem_id:2969108]。

对于一个连通[李群](@entry_id:137659) $G$，$\operatorname{Ad}(G)$-不变性等价于其无穷小形式，即 $\operatorname{ad}$-不变性。对上述 $\operatorname{Ad}$-[不变性条件](@entry_id:171412)关于 $h$ 在单位元处求导，可以得到对所有 $X, Y, Z \in \mathfrak{g}$ 成立的条件：
$$
\langle [Z, X], Y \rangle_e + \langle X, [Z, Y] \rangle_e = 0
$$
这个条件表明，对于任意 $Z \in \mathfrak{g}$，[线性算子](@entry_id:149003) $\operatorname{ad}_Z: \mathfrak{g} \to \mathfrak{g}$ （定义为 $\operatorname{ad}_Z(X) = [Z,X]$）是关于[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle_e$ 的一个 **斜[对称算子](@entry_id:272489) (skew-symmetric operator)** [@problem_id:2969097] [@problem_id:2982733]。

### 存在性条件

我们已经看到，[双不变度量](@entry_id:184842)的存在性等价于李代数 $\mathfrak{g}$ 上存在一个 $\operatorname{Ad}$-不变的[内积](@entry_id:158127)。那么，哪些李群满足这个条件呢？

对于 **[紧李群](@entry_id:146703) (compact Lie group)**，答案是肯定的。我们可以通过一个优美的 **平均化技巧 (averaging technique)** 来构造一个 $\operatorname{Ad}$-不变[内积](@entry_id:158127)。从 $\mathfrak{g}$ 上的任意一个[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle_0$ 出发，我们利用[紧群](@entry_id:146287)上存在的总测度为 1 的双不变 Haar 测度 $d\mu$ 来定义一个新的[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle$：
$$
\langle X, Y \rangle := \int_G \langle \operatorname{Ad}_g(X), \operatorname{Ad}_g(Y) \rangle_0 \, d\mu(g)
$$
这个积分是良定义的，因为被积函数在[紧空间](@entry_id:155073) $G$ 上是连续有界的。通过利用 Haar 测度的不变性，可以证明这个新的[内积](@entry_id:158127)确实是 $\operatorname{Ad}(G)$-不变的 [@problem_id:2969108]。因此，我们得出结论：**任何[紧李群](@entry_id:146703)都存在双不变[黎曼度量](@entry_id:754359)**。

然而，对于 **非[紧李群](@entry_id:146703) (non-compact Lie group)**，情况则完全不同。其 Haar 测度的总测度是无穷大的，即 $\mu(G) = \infty$。这导致上述平均化积分通常会发散。例如，如果 $\mathfrak{g}$ 有非平凡的中心，取中心元 $X \neq 0$，则 $\operatorname{Ad}_g(X)=X$ 对所有 $g$ 成立，那么 $\langle X, X \rangle$ 的积分显然为无穷大。任何试图通过截断或加权来强制收敛的方法，通常会破坏所需的 $\operatorname{Ad}$-不变性。因此，这个平均化方法对于非[紧李群](@entry_id:146703)是失效的 [@problem_id:2969106]。

[双不变度量](@entry_id:184842)存在的充要条件是一个纯代数条件。一个连通[李群](@entry_id:137659) $G$ 存在双不变黎曼度量，当且仅当其李代数 $\mathfrak{g}$ 是 **紧致型约化 (reductive of compact type)** 的。这意味着 $\mathfrak{g}$ 可以分解为一个紧致[半单李代数](@entry_id:190073)和一个[交换代数](@entry_id:149047)的[直和](@entry_id:156782)：$\mathfrak{g} = \mathfrak{s} \oplus \mathfrak{z}$，其中 $\mathfrak{s} = [\mathfrak{g}, \mathfrak{g}]$ 是紧致半单的，$\mathfrak{z}$ 是 $\mathfrak{g}$ 的中心。

一个重要的反例是三维 **[海森堡群](@entry_id:144785) (Heisenberg group)** $H_3$。其[李代数](@entry_id:137954) $\mathfrak{h}_3$ 由基 $\{X, Y, Z\}$ 张成，满足 $[X, Y] = Z$ 且 $Z$ 是中心元。算子 $\operatorname{ad}_X$ 和 $\operatorname{ad}_Y$ 都是非零的[幂零算子](@entry_id:148875)。一个非零的[幂零算子](@entry_id:148875)在任何[内积](@entry_id:158127)下都不可能是斜对称的（因为斜[对称算子](@entry_id:272489)是正规的，从而可对角化，而唯一可对角化的[幂零算子](@entry_id:148875)是零算子）。因此，$\mathfrak{h}_3$ 上不存在使所有 $\operatorname{ad}$ 算子都斜对称的[内积](@entry_id:158127)，故[海森堡群](@entry_id:144785) $H_3$ 不存在双不变[黎曼度量](@entry_id:754359) [@problem_id:2982733]。

### 结构与分类

对于存在[双不变度量](@entry_id:184842)的[李群](@entry_id:137659)（即其[李代数](@entry_id:137954) $\mathfrak{g}$ 是紧致型约化的），我们可以对其上的所有[双不变度量](@entry_id:184842)进行分类。设 $\mathfrak{g}$ 分解为其中心 $\mathfrak{z}$ 和一系列单理想 (simple ideals) $\mathfrak{g}_i$ 的[直和](@entry_id:156782)：
$$
\mathfrak{g} = \mathfrak{z} \oplus \mathfrak{g}_1 \oplus \cdots \oplus \mathfrak{g}_r
$$
任何一个 $\operatorname{Ad}(G)$-不变[内积](@entry_id:158127)都必须与这个[代数结构](@entry_id:137052)相容。利用 $\operatorname{ad}$-[不变性条件](@entry_id:171412)可以证明，这个[直和分解](@entry_id:263004)在任何[双不变度量](@entry_id:184842)下都是 **正交的 (orthogonal)** [@problem_id:2969107]。也就是说，对于 $i \neq j$，$\langle \mathfrak{g}_i, \mathfrak{g}_j \rangle = \{0\}$，并且 $\langle \mathfrak{z}, \mathfrak{g}_i \rangle = \{0\}$ 对所有 $i$ 成立。这个正交性可以从$\operatorname{ad}$-[不变性条件](@entry_id:171412)中推导出来。对于任意$X \in \mathfrak{g}_i, Y \in \mathfrak{g}_j$ ($i \neq j$)和$Z \in \mathfrak{g}_i$，有$[Z, Y]=0$。[不变性条件](@entry_id:171412) $\langle [Z,X], Y \rangle + \langle X, [Z,Y] \rangle = 0$ 简化为 $\langle [Z,X], Y \rangle=0$。由于这适用于所有$X,Z \in \mathfrak{g}_i$，因此 $\langle [\mathfrak{g}_i, \mathfrak{g}_i], \mathfrak{g}_j \rangle = \{0\}$。由于单理想是完美的（perfect），即 $[\mathfrak{g}_i, \mathfrak{g}_i] = \mathfrak{g}_i$，我们得到 $\langle \mathfrak{g}_i, \mathfrak{g}_j \rangle = \{0\}$ [@problem_id:2969094]。

因此，一个[双不变度量](@entry_id:184842)的[分类问题](@entry_id:637153)分解为在每个子代数上独立地进行分类：

1.  **在中心 $\mathfrak{z}$ 上**：伴随作用在中心上是平凡的，即 $\operatorname{Ad}_g(Z) = Z$ 对所有 $Z \in \mathfrak{z}$ 成立。这意味着任何定义在 $\mathfrak{z}$ 上的[内积](@entry_id:158127)都自动是 $\operatorname{Ad}(G)$-不变的。因此，$\mathfrak{z}$ 上的[双不变度量](@entry_id:184842)部分是任意的。如果 $\dim(\mathfrak{z}) = k$，那么这部分有 $k(k+1)/2$ 个自由参数 [@problem_id:2969102]。

2.  **在单理想 $\mathfrak{g}_i$ 上**：$\mathfrak{g}_i$ 上的伴随表示是不可约的。根据[舒尔引理](@entry_id:136779) (Schur's Lemma)，任何两个在[不可约表示](@entry_id:263310)空间上的[不变双线性形式](@entry_id:137662)必然成比例。$\mathfrak{g}_i$ 的 **[基灵型](@entry_id:161046) (Killing form)** $B_i(X,Y) = \mathrm{tr}(\operatorname{ad}_X \circ \operatorname{ad}_Y)$ 是一个自然存在的 $\operatorname{ad}$-不变[对称双线性形式](@entry_id:148281)。由于 $\mathfrak{g}_i$ 是紧致单代数，其[基灵型](@entry_id:161046)是负定的。因此，任何 $\mathfrak{g}_i$ 上的 $\operatorname{Ad}(G)$-不变[内积](@entry_id:158127)都必须是[基灵型](@entry_id:161046)的某个负的常数倍，即 $\langle \cdot, \cdot \rangle_i = -c_i B_i$，其中 $c_i$ 是一个正的常数 [@problem_id:2969102] [@problem_id:2969107]。

综上所述，一个紧致型约化[李代数](@entry_id:137954) $\mathfrak{g} = \mathfrak{z} \oplus \bigoplus_{i=1}^r \mathfrak{g}_i$ 上的[双不变度量](@entry_id:184842)由以下数据唯一确定：中心 $\mathfrak{z}$ 上的一个任意[内积](@entry_id:158127)，以及对应每个单理想 $\mathfrak{g}_i$ 的一个正标量 $c_i > 0$。因此，[双不变度量](@entry_id:184842)的模空间 (moduli space) 的维度是 $k(k+1)/2 + r$，其中 $k = \dim(\mathfrak{z})$，$r$ 是单理想的个数 [@problem_id:2969107]。

值得注意的是，虽然非[紧李群](@entry_id:146703)通常不存在双不变 *黎曼* 度量，但它们可能存在双不变的 **[伪黎曼度量](@entry_id:185204) (pseudo-Riemannian metric)**。一个典型的例子是 $G = SL(2, \mathbb{R})$，其[李代数](@entry_id:137954) $\mathfrak{sl}(2, \mathbb{R})$ 是非紧的单代数。它的[基灵型](@entry_id:161046)是非退化的，但符号差为 $(2,1)$（两个正[特征值](@entry_id:154894)，一个负[特征值](@entry_id:154894)）。这个[基灵型](@entry_id:161046)可以用来定义 $SL(2, \mathbb{R})$ 上一个双不变的洛伦兹度量 [@problem_id:2969105]。

### 几何性质与应用

[李群](@entry_id:137659)上的[双不变度量](@entry_id:184842)具有优美的几何性质，这使得它们成为研究对称空间的典范。

一个最基本的性质是，对于一个带有[双不变度量](@entry_id:184842)的李群，从单位元出发的 **[测地线](@entry_id:269969) (geodesics)** 恰好是 **[单参数子群](@entry_id:181957) (one-parameter subgroups)**，即形如 $\gamma(t) = \exp(tX)$ 的曲线，其中 $X \in \mathfrak{g}$。

这个事实有一个重要的推论。如果我们使用指数映射 $\exp: \mathfrak{g} \to G$ 在单位元附近建立[坐标系](@entry_id:156346)（称为指数坐标或[法坐标](@entry_id:143194)），那么这些直线型的[单参数子群](@entry_id:181957)在坐标中就是直线。[测地线方程](@entry_id:264349) $\nabla_{\dot{\gamma}}\dot{\gamma} = 0$ 在这些坐标下要求克氏符 (Christoffel symbols) $\Gamma^k_{ij}$ 满足 $\Gamma^k_{ij} v^i v^j = 0$ 对所有速度向量 $v$ 成立。这反过来证明了，在单位元处，克氏符必须为零，即 $\Gamma^k_{ij}(0) = 0$ [@problem_id:2969099]。这意味着在单位元附近，度量的泰勒展开中没有一次项，几何结构在局部看起来非常接近[欧几里得空间](@entry_id:138052)。

[双不变度量](@entry_id:184842)在[几何分析](@entry_id:157700)中也扮演着核心角色。一个黎曼流形上的 **[拉普拉斯-贝尔特拉米算子](@entry_id:267002) (Laplace-Beltrami operator)** $\Delta$ 是一个基本的二阶微分算子。对于一个具有[双不变度量](@entry_id:184842)的李群 $(G,g)$，这个几何算子与[李代数](@entry_id:137954)的一个纯代数对象——**[卡西米尔元](@entry_id:202375) (Casimir element)** $\Omega$——紧密相连。

给定一个 $\operatorname{Ad}$-不变[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle$ 和 $\mathfrak{g}$ 的一个对应的标准正交基 $\{X_i\}$，[卡西米尔元](@entry_id:202375)定义为[泛包络代数](@entry_id:188071) $U(\mathfrak{g})$ 中的元素 $\Omega = \sum_i X_i^2$。可以证明 $\Omega$ 位于 $U(\mathfrak{g})$ 的中心，并且不依赖于[标准正交基](@entry_id:147779)的选择。当我们将 $X_i$ 视为 $G$ 上的[左不变向量场](@entry_id:637116)时，$\{\tilde{X}_i\}$ 构成 $(G,g)$ 上的一个[标准正交标架](@entry_id:189702)场。[拉普拉斯算子](@entry_id:146319)可以表示为 $\Delta f = -\sum_i (\tilde{X}_i^2 f - (\nabla_{\tilde{X}_i}\tilde{X}_i)f)$。对于[双不变度量](@entry_id:184842)，可以证明其列维-奇维塔联络满足 $\nabla_{\tilde{X}}\tilde{Y} = \frac{1}{2}[\tilde{X}, \tilde{Y}]$，因此 $\nabla_{\tilde{X}_i}\tilde{X}_i = 0$。这使得拉普拉斯算子的表达式急剧简化为：
$$
\Delta f = -\sum_i \tilde{X}_i^2 f = -dL(\Omega)f
$$
其中 $dL(\Omega)$ 表示[卡西米尔元](@entry_id:202375)通过[左正则表示](@entry_id:146345)作用在函数上。这个等式 $\Delta = -dL(\Omega)$ 建立了几何（[拉普拉斯算子](@entry_id:146319)）与代数（[卡西米尔元](@entry_id:202375)）之间的深刻联系。由于度量也是右不变的，我们同样可以得到 $\Delta = -dR(\Omega)$，其中 $dR$ 是[右正则表示](@entry_id:145729) [@problem_id:2969104]。这个关系是[调和分析](@entry_id:198768)和[表示论](@entry_id:137998)在[李群](@entry_id:137659)上研究的出发点。