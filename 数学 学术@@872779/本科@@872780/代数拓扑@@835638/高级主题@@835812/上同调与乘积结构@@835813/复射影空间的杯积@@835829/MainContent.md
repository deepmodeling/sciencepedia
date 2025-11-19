## 引言
[复射影空间](@entry_id:268402)（$\mathbb{C}P^n$）是几何与拓扑学中的核心研究对象之一。我们已经知道其上同调群在结构上极为简洁，仅在偶数维非零。然而，这一认识仅仅停留在[加法群](@entry_id:151801)的层面，未能揭示其全部的威力。[上同调理论](@entry_id:270863)的真正精髓在于其丰富的乘法结构——**[杯积](@entry_id:159554)（cup product）**，它将分立的上同调群整合为一个统一的代数实体：[上同调环](@entry_id:160158)。这个环结构不仅是一个优美的理论构造，更是连接[抽象代数](@entry_id:145216)与具体几何问题的关键桥梁，解决了仅凭[上同调群](@entry_id:142450)无法解答的深刻问题。

本文旨在系统地阐述[复射影空间](@entry_id:268402)的[杯积](@entry_id:159554)结构及其应用。在**“原理与机制”**一章中，我们将深入剖析 $\mathbb{C}P^n$ [上同调环](@entry_id:160158)的[代数结构](@entry_id:137052)——一个[截断多项式环](@entry_id:266249)，并从胞腔分解和[几何相交](@entry_id:159175)两个角度揭示其拓扑根源。接着，在**“应用与跨学科联系”**一章中，我们将展示这一结构如何作为强大的[不变量](@entry_id:148850)，在拓扑学、代数几何、微分几何乃至现代物理学中解决实际问题，例如约束连续映射、计算[子流形](@entry_id:159439)交点和确定特征类。最后，通过**“动手实践”**部分的精选习题，读者将有机会亲手运用所学知识，将理论内化为解决问题的能力。通过这一系列的学习，你将深刻理解[杯积](@entry_id:159554)如何将 $\mathbb{C}P^n$ 的上同调从一组孤立的群提升为一个蕴含着深刻几何信息的强大代数工具。

## 原理与机制

$n$ 维[复射影空间](@entry_id:268402) $\mathbb{C}P^n$ 的整系数[上同调群](@entry_id:142450)具有非常简洁的结构：仅在偶数维非零。具体而言，对于 $0 \le k \le n$，其上同调群 $H^{2k}(\mathbb{C}P^n; \mathbb{Z}) \cong \mathbb{Z}$，而在所有其他维度上均为零。然而，这一描述仅仅是作为分次[阿贝尔群的结构](@entry_id:140745)。[上同调理论](@entry_id:270863)的真正威力在于其附加的乘法结构——**[杯积](@entry_id:159554) (cup product)**，它将分次上同调群 $H^*(\mathbb{C}P^n; \mathbb{Z}) = \bigoplus_{k=0}^{2n} H^k(\mathbb{C}P^n; \mathbb{Z})$ 提升为一个**分次环 (graded ring)**。本章旨在深入探讨这一环结构的原理、机制及其深刻的几何与拓扑应用。

### [复射影空间](@entry_id:268402)的[上同调环](@entry_id:160158)

[复射影空间](@entry_id:268402)[上同调环](@entry_id:160158)的结构是代数拓扑中的一个经典结果。它可以通过一个极为优美的代数模型来描述。

**定理：** $n$ 维[复射影空间](@entry_id:268402) $\mathbb{C}P^n$ 的整系数[上同调环](@entry_id:160158) $H^*(\mathbb{C}P^n; \mathbb{Z})$ 同构于一个[截断多项式环](@entry_id:266249)：
$$ H^*(\mathbb{C}P^n; \mathbb{Z}) \cong \frac{\mathbb{Z}[x]}{\langle x^{n+1} \rangle} $$
其中 $x$ 是一个次数为 2 的未定元，对应于 $H^2(\mathbb{C}P^n; \mathbb{Z})$ 的一个生成元。

这个同构关系意味着，$\mathbb{C}P^n$ 的[上同调环](@entry_id:160158)在代数上等价于一个单变量 $x$ 的整系数[多项式环](@entry_id:152854)，但附加了一个关系式 $x^{n+1}=0$。这表明任何高于 $n$ 次的 $x$ 的幂次都为零。这个[环的结构](@entry_id:150907)分层如下：
- **0次[上同调群](@entry_id:142450)** $H^0(\mathbb{C}P^n; \mathbb{Z})$ 对应于环中的常数项，由 $1$ 生成。根据分次环的定义，乘法单位元必须是 0 次元素，因为它与任何元素 $a$ 的乘积 $1 \cup a$ 必须保持 $a$ 的次数不变。因此，$H^0(\mathbb{C}P^n; \mathbb{Z})$ 的生成元正是这个环的乘法单位元 [@problem_id:1645299]。

- **2k次上同调群** $H^{2k}(\mathbb{C}P^n; \mathbb{Z})$ (对于 $1 \le k \le n$) 对应于环中 $2k$ 次的元素，由 $x^k$ 生成。这意味着，如果我们记 $H^2(\mathbb{C}P^n; \mathbb{Z})$ 的生成元为 $\alpha$，那么 $H^{2k}(\mathbb{C}P^n; \mathbb{Z})$ 的生成元就是 $\alpha$ 与自身的 $k$ 次杯积，记作 $\alpha^k = \alpha \cup \dots \cup \alpha$。

- **截断关系** $x^{n+1}=0$ 意味着 $\alpha^{n+1}=0$。这与 $H^{2(n+1)}(\mathbb{C}P^n; \mathbb{Z}) = 0$ 的事实相符，因为 $\mathbb{C}P^n$ 的实维数为 $2n$。

让我们以[复射影平面](@entry_id:262661) $\mathbb{C}P^2$ ($n=2$) 为例来具体理解这个结构。其[上同调环](@entry_id:160158)为 $H^*(\mathbb{C}P^2; \mathbb{Z}) \cong \mathbb{Z}[x]/\langle x^3 \rangle$。设 $\alpha$ 是 $H^2(\mathbb{C}P^2; \mathbb{Z})$ 的一个生成元。根据[环同构](@entry_id:147982)，$\alpha$ 对应于 $x$。那么，杯积 $\alpha \cup \alpha = \alpha^2$ 就对应于多项式环中的 $x^2$。由于 $x^2$ 是 $\mathbb{Z}[x]/\langle x^3 \rangle$ 中 4 次部分的生成元，因此 $\alpha^2$ 必然是 $H^4(\mathbb{C}P^2; \mathbb{Z})$ 的一个生成元。它不为零，因为截断关系是 $\alpha^3=0$ 而不是 $\alpha^2=0$ [@problem_id:1645278]。

在这个代数框架下，上同调类的计算变得像多项式运算一样直观。例如，考虑 $H^*(\mathbb{C}P^2; \mathbb{Z})$ 中的两个元素 $A = 3 \cdot 1 + 2 \cdot \alpha$ 和 $B = 5 \cdot 1 - 4 \cdot \alpha$。它们的[杯积](@entry_id:159554) $A \cup B$ 可以通过[分配律](@entry_id:144084)计算得出 [@problem_id:1645312]：
$$ A \cup B = (3 \cdot 1 + 2 \cdot \alpha) \cup (5 \cdot 1 - 4 \cdot \alpha) $$
$$ = 15 \cdot (1 \cup 1) - 12 \cdot (1 \cup \alpha) + 10 \cdot (\alpha \cup 1) - 8 \cdot (\alpha \cup \alpha) $$
$$ = 15 \cdot 1 - 12 \cdot \alpha + 10 \cdot \alpha - 8 \cdot \alpha^2 $$
$$ = 15 \cdot 1 - 2 \cdot \alpha - 8 \cdot \alpha^2 $$
最终的结果是一个[上同调类](@entry_id:263961)，其在 $H^0$, $H^2$, $H^4$ 中的分量系数分别为 $15, -2, -8$。

### 杯积的一般性质：[双线性](@entry_id:146819)与[分次交换性](@entry_id:161347)

[杯积](@entry_id:159554)运算 $\cup: H^p(X; R) \times H^q(X; R) \to H^{p+q}(X; R)$ 具有两个基本性质：

1.  **双线性 (Bilinearity):** [杯积](@entry_id:159554)对于加法是可分配的，且与系数环 $R$ 的[标量乘法](@entry_id:155971)兼容。我们在上面的计算中已经不自觉地使用了这一性质。例如，对 $u=5\gamma_1 \in H^2(\mathbb{C}P^4; \mathbb{Z})$ 和 $v=7\gamma_2 \in H^4(\mathbb{C}P^4; \mathbb{Z})$，它们的[杯积](@entry_id:159554)是 $(5\gamma_1) \cup (7\gamma_2) = 35 (\gamma_1 \cup \gamma_2)$ [@problem_id:1645295]。

2.  **[分次交换性](@entry_id:161347) (Graded-Commutativity):** 对于任意两个上同调类 $a \in H^p(X; R)$ 和 $b \in H^q(X; R)$，它们的交换遵循以下规则：
    $$ a \cup b = (-1)^{pq} (b \cup a) $$
    符号 $(-1)^{pq}$ 取决于两个类次数的乘积。这意味着，如果 $p$ 或 $q$ 中至少有一个是偶数，那么 $a \cup b = b \cup a$，两者是普通交换的。只有当 $p$ 和 $q$ 都是奇数时，才会出现[反交换关系](@entry_id:153815) $a \cup b = - (b \cup a)$。

对于[复射影空间](@entry_id:268402) $\mathbb{C}P^n$，所有非零[上同调群](@entry_id:142450)都出现在偶数维。因此，任意两个非零齐次[上同调类](@entry_id:263961)的次数都是偶数。设 $a \in H^{2k}(\mathbb{C}P^n; \mathbb{Z})$ 和 $b \in H^{2l}(\mathbb{C}P^n; \mathbb{Z})$，它们的次数分别为 $2k$ 和 $2l$。根据分次交换律，符号因子是 $(-1)^{(2k)(2l)} = (-1)^{4kl} = 1$。因此，$H^*(\mathbb{C}P^n; \mathbb{Z})$ 是一个**严格交换**的环。

为了更好地理解[分次交换性](@entry_id:161347)的重要性，我们可以考察一个包含奇数次上同调类的空间，例如 $X = \mathbb{C}P^2 \times T^2$，其中 $T^2$ 是[二维环面](@entry_id:265991)。根据**[Künneth定理](@entry_id:274959)**，其[上同调环](@entry_id:160158)为 $H^*(X; \mathbb{Z}) \cong H^*(\mathbb{C}P^2; \mathbb{Z}) \otimes_{\mathbb{Z}} H^*(T^2; \mathbb{Z})$。我们知道 $H^*(\mathbb{C}P^2; \mathbb{Z}) \cong \mathbb{Z}[\alpha]/\langle \alpha^3 \rangle$ (其中 $\deg(\alpha)=2$)，$H^*(T^2; \mathbb{Z})$ 是由两个 1 次生成元 $\beta_1, \beta_2$ 生成的[外代数](@entry_id:201164) $\Lambda_{\mathbb{Z}}[\beta_1, \beta_2]$。在积空间中，混合杯积的计算规则是 $(a_1 \otimes b_1) \cup (a_2 \otimes b_2) = (-1)^{(\deg b_1)(\deg a_2)} (a_1 \cup a_2) \otimes (b_1 \cup b_2)$。
考虑 $\alpha \in H^2(X)$ 和 $\beta_1 \in H^1(X)$ 的[杯积](@entry_id:159554)。由于 $\deg(\alpha)=2$ 是偶数，我们有 $\alpha \cup \beta_1 = (-1)^{2 \cdot 1} \beta_1 \cup \alpha = \beta_1 \cup \alpha$。然而，对于两个奇数次的类 $\beta_1, \beta_2$，我们有 $\beta_1 \cup \beta_2 = (-1)^{1 \cdot 1} \beta_2 \cup \beta_1 = - \beta_2 \cup \beta_1$ [@problem_id:1645289]。这个例子凸显了 $\mathbb{C}P^n$ [上同调环](@entry_id:160158)的交换性是其特殊[代数结构](@entry_id:137052)的结果。

当我们将多个 $\mathbb{C}P^n$ 空间相乘时，例如 $X = \mathbb{C}P^3 \times \mathbb{C}P^4$，其[上同调环](@entry_id:160158)由[Künneth定理](@entry_id:274959)给出。由于所有生成元 $x \in H^2(\mathbb{C}P^3)$ 和 $y \in H^2(\mathbb{C}P^4)$ 都是偶数次，混合[杯积](@entry_id:159554)的符号因子总是 1。计算可以像普通的多项式乘法一样进行，只需注意各[自环](@entry_id:274670)中的截断关系 ($x^4=0, y^5=0$) [@problem_id:1645270]。

### [代数结构](@entry_id:137052)的拓扑根源

这个优美的[代数结构](@entry_id:137052)并非凭空而来，它深深植根于 $\mathbb{C}P^n$ 的拓扑构造之中。

#### [胞腔上同调](@entry_id:268465)视角

$\mathbb{C}P^n$ 有一个非常特殊的**胞腔分解 (cell decomposition)**：在每个偶数维度 $0, 2, \dots, 2n$ 上都恰好有一个胞腔，而在奇数维度上没有胞腔。我们记 $2k$ 维的胞腔为 $e_{2k}$。

由此产生的[胞腔链复形](@entry_id:160435) $C_*(\mathbb{C}P^n; \mathbb{Z})$ 在偶数维上是 $\mathbb{Z}$，奇数维上是 $0$。一个关键事实是，这个[链复形](@entry_id:150246)的所有**[边界映射](@entry_id:151165) (boundary maps)** 都为零。这意味着对偶的**上[链复形](@entry_id:150246) (cochain complex)** $C^*(\mathbb{C}P^n; \mathbb{Z})$ 的所有**上[边界映射](@entry_id:151165) (coboundary maps)** 也都是零。因此，[上同调群](@entry_id:142450) $H^{2k}(\mathbb{C}P^n; \mathbb{Z})$ 直接同构于上链群 $C^{2k}(\mathbb{C}P^n; \mathbb{Z})$。设 $e_{2k}^*$ 是 $C^{2k}$ 中对偶于 $e_{2k}$ 的基底（即 $e_{2k}^*(e_{2j}) = \delta_{kj}$），那么它的上同调类 $[e_{2k}^*]$ 就是 $H^{2k}(\mathbb{C}P^n; \mathbb{Z})$ 的生成元。

杯积结构源于对角映射 $\Delta: \mathbb{C}P^n \to \mathbb{C}P^n \times \mathbb{C}P^n$ 在链层面上的近似 $\Delta_*: C_*(\mathbb{C}P^n) \to C_*(\mathbb{C}P^n) \otimes C_*(\mathbb{C}P^n)$。对于 $\mathbb{C}P^n$ 的标准胞腔结构，这个映射有如下公式：
$$ \Delta_*(e_{2m}) = \sum_{i=0}^{m} e_{2i} \otimes e_{2(m-i)} $$
根据上链层面[杯积](@entry_id:159554)的定义，我们可以计算基底上链的[杯积](@entry_id:159554)。例如，对于 $e_{2k}^*$ 和 $e_{2l}^*$，它们在 $e_{2m}$ 上的值为：
$$ (e_{2k}^* \cup e_{2l}^*)(e_{2m}) = \langle e_{2k}^* \otimes e_{2l}^*, \Delta_*(e_{2m}) \rangle = \sum_{i=0}^{m} e_{2k}^*(e_{2i}) \cdot e_{2l}^*(e_{2(m-i)}) $$
$$ = \sum_{i=0}^{m} \delta_{ki} \cdot \delta_{l, m-i} $$
这个和只有在 $i=k$ 且 $m-i=l$（即 $m=k+l$）时才非零，此时其值为 1。因此，我们得到 $e_{2k}^* \cup e_{2l}^* = e_{2(k+l)}^*$。在传递到[上同调](@entry_id:160558)层面后，这意味着如果我们记 $\gamma_j = [e_{2j}^*]$，那么我们就有环关系 $\gamma_k \cup \gamma_l = \gamma_{k+l}$ [@problem_id:1645295]。这精确地复现了[多项式环](@entry_id:152854)的[乘法规则](@entry_id:197368) $x^k \cdot x^l = x^{k+l}$，从而为代数同构提供了具体的拓扑机制。

#### 几何解释：[庞加莱对偶](@entry_id:161676)与[相交理论](@entry_id:157884)

[上同调环](@entry_id:160158)的结构还有一个深刻的几何解释，这通过**[庞加莱对偶](@entry_id:161676) (Poincaré Duality)** 实现。对于一个紧致、可定向的 $d$ 维[流形](@entry_id:153038) $M$，[庞加莱对偶](@entry_id:161676)建立了 $H^k(M)$ 和 $H_{d-k}(M)$ 之间的同构。更重要的是，[上同调](@entry_id:160558)中的杯积运算对偶于同调中[子流形](@entry_id:159439)的**横截相交 (transverse intersection)**。

$\mathbb{C}P^n$ 是一个实维数为 $2n$ 的紧致、[可定向流形](@entry_id:276936)。
- $H^2(\mathbb{C}P^n; \mathbb{Z})$ 的生成元 $\alpha$ 是一个实[余维数](@entry_id:273141)为 2 的[子流形](@entry_id:159439)的对偶类。这个子流形正是一个**超平面 (hyperplane)**，即 $\mathbb{C}P^n$ 中一个线性嵌入的 $\mathbb{C}P^{n-1}$。
- 杯积 $\alpha \cup \alpha = \alpha^2 \in H^4(\mathbb{C}P^n; \mathbb{Z})$ 对偶于两个（通过微小扰动使其横截的）超平面的交。在 $\mathbb{C}P^2$ 中，两个不同的复直线（即超平面）相交于唯一点。因此，$\alpha^2$ 的几何意义是一个**点 (point)** 的对偶类 [@problem_id:1645261]。
- 依此类推，$\alpha^k \in H^{2k}(\mathbb{C}P^n; \mathbb{Z})$ 对偶于 $k$ 个一般位置的超平面的交。这个交集本身是一个复[余维数](@entry_id:273141)为 $k$ 的[线性子空间](@entry_id:151815)，即一个 $\mathbb{C}P^{n-k}$。
- 最终，$\alpha^n \in H^{2n}(\mathbb{C}P^n; \mathbb{Z})$ 对偶于 $n$ 个超平面的交，即一个 $\mathbb{C}P^0$，也就是一个点。这与 $H^{2n}(\mathbb{C}P^n; \mathbb{Z})$ 由点的对偶类生成的事实相符。
- 而代数关系 $\alpha^{n+1}=0$ 则对应于一个清晰的几何事实：在 $\mathbb{C}P^n$ 中，$n+1$ 个处于一般位置的[超平面](@entry_id:268044)的交集是**空集**。

这种代数与几何之间的优美对应，是代数拓扑强大威力的集中体现。

### [上同调环](@entry_id:160158)的应用

[上同调环](@entry_id:160158)不仅是一个漂亮的理论构造，更是一个强大的工具，可以用来解决具体的拓扑问题。

#### 区分拓扑空间

[上同调环](@entry_id:160158)是一个比上同调群更精细的**[同伦不变量](@entry_id:151920) (homotopy invariant)**。如果两个空间是同伦等价的，那么它们的[上同调环](@entry_id:160158)必须同构。这为我们提供了一种强有力的方法来区分[拓扑空间](@entry_id:155056)。

例如，考虑空间 $X = \mathbb{C}P^2$ 和空间 $Y = S^2 \vee S^4$（一个2维球面和一个4维球面的[楔和](@entry_id:270607)）。它们的[上同调群](@entry_id:142450)是相同的：
$$ H^k(X; \mathbb{Z}) \cong H^k(Y; \mathbb{Z}) \cong \begin{cases} \mathbb{Z}  \text{ if } k=0, 2, 4 \\ 0  \text{ otherwise} \end{cases} $$
然而，它们的环结构截然不同。对于 $X = \mathbb{C}P^2$，我们知道若 $\alpha$ 是 $H^2$ 的生成元，则 $\alpha^2 \neq 0$。但对于 $Y = S^2 \vee S^4$，可以让 $\beta$ 是 $H^2(Y)$ 的生成元，可以证明其杯积 $\beta^2=0$。由于它们的[上同调环](@entry_id:160158)在乘法结构上不同构，$\mathbb{C}P^2$ 和 $S^2 \vee S^4$ 就不可能是[同伦等价](@entry_id:150816)的 [@problem_id:1645296]。

#### 约束连续映射

[上同调](@entry_id:160558)的**[函子性](@entry_id:150069) (functoriality)** 意味着，任何一个连续映射 $f: X \to Y$ 都会诱导一个**[环同态](@entry_id:153804) (ring homomorphism)** $f^*: H^*(Y; R) \to H^*(X; R)$。这个代数约束可以用来证明某些[连续映射](@entry_id:153855)是不存在的。

一个经典的例子是证明不存在从 $\mathbb{C}P^n$ 到其[子空间](@entry_id:150286) $\mathbb{C}P^{n-1}$ 的**收缩映射 (retraction)**。收缩映射 $r: \mathbb{C}P^n \to \mathbb{C}P^{n-1}$ 是一个连续映射，其在[子空间](@entry_id:150286) $\mathbb{C}P^{n-1}$ 上的限制是[恒等映射](@entry_id:634191)。如果存在这样的 $r$，令 $i: \mathbb{C}P^{n-1} \hookrightarrow \mathbb{C}P^n$ 为标准包含映射，则我们有 $r \circ i = \text{id}_{\mathbb{C}P^{n-1}}$。

在应用上同调[函子](@entry_id:150427)后，我们得到一个[环同态](@entry_id:153804)的复合关系 $i^* \circ r^* = \text{id}^* = \text{id}$。
令 $H^*(\mathbb{C}P^n; \mathbb{Z}) \cong \mathbb{Z}[x]/\langle x^{n+1} \rangle$ 和 $H^*(\mathbb{C}P^{n-1}; \mathbb{Z}) \cong \mathbb{Z}[y]/\langle y^n \rangle$。已知包含映射诱导的同态 $i^*$ 将 $x$ 映为 $y$，即 $i^*(x)=y$。

现在考虑 $y \in H^2(\mathbb{C}P^{n-1})$。由于 $i^* \circ r^*$ 是 $H^*(\mathbb{C}P^{n-1})$ 上的恒等映射，它必须将 $y$ 映为自身。同时，由于 $r^*$ 是一个[环同态](@entry_id:153804)，它必须将 $y$ 映为 $H^2(\mathbb{C}P^n)$ 中的某个元素，我们称之为 $r^*(y)$。因为 $i^*(r^*(y)) = y$ 且 $i^*(x)=y$，可以推断 $r^*(y)$ 必须是 $x$（或 $-x$，不影响结论）。

现在我们利用环结构。在 $H^*(\mathbb{C}P^{n-1})$ 中，我们有关系式 $y^n=0$。将[环同态](@entry_id:153804) $r^*$ 应用于此等式，我们得到 $r^*(y^n)=r^*(0)=0$。另一方面，利用 $r^*$ 的[环同态](@entry_id:153804)性质，我们有 $r^*(y^n) = (r^*(y))^n = x^n$。
这就导出了一个矛盾：$x^n = 0$。然而，在 $H^*(\mathbb{C}P^n)$ 中，$x^n$ 是顶维上同调群 $H^{2n}(\mathbb{C}P^n; \mathbb{Z})$ 的非零生成元。这个矛盾证明了最初假设的收缩映射 $r$ 不可能存在 [@problem_id:1645313]。

### 推广至无穷维：$\mathbb{C}P^\infty$ 的情形

作为本章的结尾，我们自然会问：如果维数 $n$ 趋于无穷，会发生什么？无穷维[复射影空间](@entry_id:268402) $\mathbb{C}P^\infty$ 可以看作是包含序列 $\mathbb{C}P^1 \hookrightarrow \mathbb{C}P^2 \hookrightarrow \dots$ 的**直极限 (direct limit)**。

它的[上同调环](@entry_id:160158) $H^*(\mathbb{C}P^\infty; \mathbb{Z})$ 同样由一个 2 次的生成元 $\beta$ 生成。然而，这一次不再有截断。其[上同调环](@entry_id:160158)是一个完整的**多项式环**：
$$ H^*(\mathbb{C}P^\infty; \mathbb{Z}) \cong \mathbb{Z}[\beta] $$
这意味着，对于任意正整数 $k$，$\beta^k$ 都是一个非零元素，并且它生成了 $H^{2k}(\mathbb{C}P^\infty; \mathbb{Z}) \cong \mathbb{Z}$。

这个结论可以通过[函子性](@entry_id:150069)来优雅地证明。对于任意 $n$，包含映射 $i_n: \mathbb{C}P^n \to \mathbb{C}P^\infty$ 诱导[环同态](@entry_id:153804) $i_n^*: H^*(\mathbb{C}P^\infty; \mathbb{Z}) \to H^*(\mathbb{C}P^n; \mathbb{Z})$。这个同态将 $\beta$ 映为 $\mathbb{C}P^n$ [上同调环](@entry_id:160158)的生成元 $x_n$。
现在，假设在 $H^*(\mathbb{C}P^\infty; \mathbb{Z})$ 中存在 $\beta^k=0$ 对于某个正整数 $k$ 成立。那么对于任意 $n \ge k$，我们应用 $i_n^*$：
$$ i_n^*(\beta^k) = (i_n^*(\beta))^k = x_n^k = 0 $$
但这与我们在 $H^*(\mathbb{C}P^n; \mathbb{Z})$ 中的知识相矛盾，因为当 $n \ge k$ 时，$x_n^k$ 是 $H^{2k}(\mathbb{C}P^n; \mathbb{Z})$ 的非零生成元。因此，$\beta^k$ 对于任何 $k$ 都不能为零 [@problem_id:1645275]。$\mathbb{C}P^\infty$ 的[上同调环](@entry_id:160158)没有了维度限制，从而呈现为一个未截断的[多项式代数](@entry_id:263635)，它在代数拓扑和几何中扮演着基础性的角色，例如作为万有 $U(1)$ 丛的[分类空间](@entry_id:148422)。