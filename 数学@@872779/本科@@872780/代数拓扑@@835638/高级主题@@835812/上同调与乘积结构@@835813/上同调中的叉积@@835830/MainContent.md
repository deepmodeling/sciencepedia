## 引言
在代数拓扑中，一个核心任务是开发能够揭示[拓扑空间](@entry_id:155056)内在结构的[不变量](@entry_id:148850)。当我们通过[笛卡尔积](@entry_id:154642)构造更复杂的空间（如从圆周 $S^1$ 构造环面 $T^2 = S^1 \times S^1$）时，一个自然而关键的问题随之产生：我们能否从因[子空间](@entry_id:150286) $X$ 和 $Y$ 的[上同调](@entry_id:160558)信息中，推导出[积空间](@entry_id:151693) $X \times Y$ 的上同调？这个知识缺口正是本文要探讨的核心，而解答这一问题的关键工具便是上同调中的**叉积 (cross product)**。

本文将系统地引导你掌握这一强大工具。在“**原理与机制**”一章中，我们将深入其定义，探索其关键的代数性质，并揭示它如何作为更广为人知的[杯积](@entry_id:159554)的结构基础。接下来，在“**应用与交叉学科联系**”一章，我们将展示叉积的威力，看它如何通过[Künneth定理](@entry_id:274959)精确计算出复杂[积空间的上同调](@entry_id:266890)环，并如何与微分几何、向量丛理论等领域产生共鸣。最后，通过“**动手实践**”中的具体计算问题，你将有机会亲自运用这些理论，将抽象概念转化为坚实的解题能力。

现在，让我们从最基本的问题出发，开始探索叉积的原理及其背后的深刻机制。

## 原理与机制

在本章中，我们将深入探讨[上同调理论](@entry_id:270863)中的一个核心构造：**叉积 (cross product)**。继引言之后，我们将系统地阐述叉积的原理、关键性质及其在计算[拓扑空间的积](@entry_id:152598)空间[上同调环](@entry_id:160158)结构中的核心作用。叉积不仅是连接不同空间上同调的桥梁，也是理解杯积等其他重要[代数结构](@entry_id:137052)的基石。

### 动机与定义

一个自然而然的问题是：两个[拓扑空间](@entry_id:155056) $X$ 和 $Y$ 的[积空间](@entry_id:151693) $X \times Y$ 的[上同调群](@entry_id:142450)与 $X$ 和 $Y$ 各自的[上同调群](@entry_id:142450)之间有何关系？[叉积](@entry_id:156672)正是为了回答这个问题而引入的。它是一个[双线性映射](@entry_id:186502)，将来自两个因[子空间](@entry_id:150286)的上同调类结合起来，生成[积空间](@entry_id:151693)中的一个上同调类。

形式上，设 $R$ 是一个[交换环](@entry_id:148261)，对于任意非负整数 $p$ 和 $q$，[上同调叉积](@entry_id:261629)是如下映射：
$$
\times: H^p(X; R) \times H^q(Y; R) \to H^{p+q}(X \times Y; R)
$$
这个映射在同调层面上是良定义的，这意味着它将上循环配对映为上循环，并将包含上边缘的配对映为上边缘。这可以通过在 **上链 (cochain)** 层面定义叉积来精确验证。对于一个 $p$-上链 $\phi \in C^p(X; R)$ 和一个 $q$-上链 $\psi \in C^q(Y; R)$，它们的叉积 $\phi \times \psi$ 是一个 $(p+q)$-上链，其上边缘算子 $\delta$ 满足一个关键的**[莱布尼茨法则](@entry_id:157949) (Leibniz rule)**：
$$
\delta(\phi \times \psi) = (\delta\phi) \times \psi + (-1)^p \phi \times (\delta\psi)
$$
这个公式揭示了[叉积](@entry_id:156672)与上边缘算子之间的深刻联系。如果 $\phi$ 和 $\psi$ 都是**上循环 (cocycle)**（即 $\delta\phi=0$ 且 $\delta\psi=0$），那么它们的[叉积](@entry_id:156672)的上边缘也是零，$\delta(\phi \times \psi) = 0$，因此 $\phi \times \psi$ 也是一个上循环。

更重要的是，如果其中一个上链是**上边缘 (coboundary)**，例如 $\phi = \delta c$ 对于某个 $(p-1)$-上链 $c$ 成立，而 $\psi$ 是一个上循环，那么它们的[叉积](@entry_id:156672)就是一个上边缘。我们可以直接验证这一点 [@problem_id:1679013]：
$$
\delta((-1)^{p-1} c \times \psi) = (-1)^{p-1} \left( (\delta c) \times \psi + (-1)^{p-1} c \times (\delta\psi) \right) = (\delta c) \times \psi + c \times 0 = \phi \times \psi
$$
这意味着由 $\phi = \delta c$ 和 $\psi$ 构成的[叉积](@entry_id:156672) $\phi \times \psi$ 在上同调中代表零类。这个性质保证了叉积在商掉上边缘后，能够诱导出从 $H^p(X; R) \times H^q(Y; R)$ 到 $H^{p+q}(X \times Y; R)$ 的一个[良定义映射](@entry_id:136264)。在某些情况下，例如当 $c \in C^0(X;\mathbb{Z})$ 且 $v \in C^1(Y;\mathbb{Z})$ 是一个上循环时，若 $u = \delta c$，则 $\delta(c \times v) = (\delta c) \times v + (-1)^0 c \times (\delta v) = u \times v$，这提供了一个具体的例子 [@problem_id:1679013]。

### 作为杯积基础的[叉积](@entry_id:156672)

令人惊讶的是，空间 $X$ 上的“内蕴”[代数结构](@entry_id:137052)——**[杯积](@entry_id:159554) (cup product)** $\cup$，可以被看作是“外在”的叉积的一种特殊情况。这揭示了[叉积](@entry_id:156672)更为基础的地位。

这个联系是通过**对角映射 (diagonal map)** $\Delta: X \to X \times X$ 建立的，其定义为 $\Delta(x) = (x,x)$。对于任意两个[上同调类](@entry_id:263961) $\alpha \in H^p(X; R)$ 和 $\beta \in H^q(X; R)$，它们的杯积可以定义为它们在 $X \times X$ 中的叉积 $\alpha \times \beta$ 沿着对角线[拉回](@entry_id:160816)到 $X$ 的结果：
$$
\alpha \cup \beta = \Delta^*(\alpha \times \beta)
$$
其中 $\Delta^*$ 是对角映射 $\Delta$ 在[上同调](@entry_id:160558)上诱导的[拉回](@entry_id:160816)映射。这个定义不仅优雅，而且使得[杯积](@entry_id:159554)的许多重要性质可以从叉积的相应性质中推导出来。

一个典型的例子是杯积的**[分次交换性](@entry_id:161347) (graded-commutativity)**。考虑**交换映射 (swap map)** $T: X \times X \to X \times X$，定义为 $T(x_1, x_2) = (x_2, x_1)$。在同调层面上，这个映射诱导的[拉回](@entry_id:160816) $T^*$ 对[叉积](@entry_id:156672)的作用是引入一个符号 [@problem_id:1679005]：
$$
T^*(\beta \times \alpha) = (-1)^{pq} (\alpha \times \beta)
$$
其中 $p = \deg(\alpha)$ 和 $q = \deg(\beta)$。这个性质可以直接从上链[叉积](@entry_id:156672)的组合定义（即Eilenberg-MacLane公式）中严格证明。现在，我们观察到对角映射和交换映射的复合满足 $T \circ \Delta = \Delta$，因为 $T(\Delta(x)) = T(x,x) = (x,x) = \Delta(x)$。根据[拉回](@entry_id:160816)映射的[逆变性](@entry_id:192290)，我们有 $\Delta^* = (T \circ \Delta)^* = \Delta^* \circ T^*$。利用这个关系，我们可以推导出[杯积](@entry_id:159554)的分次交换律 [@problem_id:1678959]：
$$
\beta \cup \alpha = \Delta^*(\beta \times \alpha) = \Delta^*(T^*(\beta \times \alpha)) = \Delta^*((-1)^{pq}(\alpha \times \beta)) = (-1)^{pq} \Delta^*(\alpha \times \beta) = (-1)^{pq} (\alpha \cup \beta)
$$
这就证明了 $\alpha \cup \beta = (-1)^{pq}(\beta \cup \alpha)$。

在计算层面，这种联系也同样存在。使用单纯复形或[CW复形](@entry_id:150589)时，对角映射在链层面有一个组合的近似，称为**对角逼近 (diagonal approximation)** $d: C_n(X) \to \bigoplus_{i+j=n} C_i(X) \otimes C_j(X)$。上链的杯积 $u \cup v$ 就可以定义为上链[叉积](@entry_id:156672) $u \times v$ 在对角逼近诱导的[拉回](@entry_id:160816) $d^*$下的值，即 $u \cup v = d^*(u \times v)$。例如，在一个2-单形 $\sigma=[v_0, v_1, v_2]$ 上，对角逼近为 $d(\sigma) = [v_0]\otimes[v_0,v_1,v_2] + [v_0,v_1]\otimes[v_1,v_2] + [v_0,v_1,v_2]\otimes[v_2]$。如果我们有两个1-上链 $u$ 和 $v$，那么 2-上链 $u \cup v$ 在 $\sigma$ 上的值就是 $(u \times v)(d(\sigma))$。由于 $u \times v$ 只在 $C_1(X) \otimes C_1(X)$ 部分非零，我们得到 $(u \cup v)(\sigma) = u([v_0, v_1])v([v_1, v_2])$ [@problem_id:1678973]。这为杯积的计算提供了一个具体而强大的工具。

### 基本代数性质

除了作为[杯积](@entry_id:159554)的基础，[叉积](@entry_id:156672)本身也拥有一套丰富的代数性质，这些性质对于计算[积空间的上同调](@entry_id:266890)至关重要。

#### 结合律
[叉积](@entry_id:156672)是**结合的 (associative)**。在自然同胚 $(X \times Y) \times Z \cong X \times (Y \times Z)$ 下，对于上同调类 $\alpha \in H^*(X)$, $\beta \in H^*(Y)$, $\gamma \in H^*(Z)$，我们有：
$$
(\alpha \times \beta) \times \gamma = \alpha \times (\beta \times \gamma)
$$
我们可以通过一个具体的例子来验证这一点。考虑3-维环面 $T^3 = S^1 \times S^1 \times S^1$。设 $\alpha_i \in H^1(S^1_i; \mathbb{Z})$ 是第 $i$ 个圆周的[上同调](@entry_id:160558)生成元。$H^3(T^3; \mathbb{Z})$ 的生成元 $\delta$ 可以通过在积CW结构的基本3-胞腔 $e_1 \times e_2 \times e_3$ 上求值为1来定义。我们可以计算 $(\alpha_1 \times \alpha_2) \times \alpha_3$ 在这个胞腔上的值： $((\alpha_1 \times \alpha_2) \times \alpha_3)((e_1 \times e_2) \times e_3) = (\alpha_1 \times \alpha_2)(e_1 \times e_2) \cdot \alpha_3(e_3) = \alpha_1(e_1)\alpha_2(e_2)\alpha_3(e_3) = 1 \cdot 1 \cdot 1 = 1$。同样地，$\alpha_1 \times (\alpha_2 \times \alpha_3)$ 的求值也为1。因此，在同调层面上 $(\alpha_1 \times \alpha_2) \times \alpha_3 = \delta = \alpha_1 \times (\alpha_2 \times \alpha_3)$ [@problem_id:1678976]。

#### 单位元与投影
$H^0(X; R)$ 中的乘法单位元 $1_X$ 在[叉积](@entry_id:156672)中扮演着特殊角色。考虑从[积空间](@entry_id:151693)到各个因子的**[投影映射](@entry_id:153398) (projection maps)** $p_X: X \times Y \to X$ 和 $p_Y: X \times Y \to Y$。它们诱导的[拉回](@entry_id:160816)映射与[叉积](@entry_id:156672)有如下基本关系：
$$
p_X^*(\alpha) = \alpha \times 1_Y \quad \text{for } \alpha \in H^*(X; R)
$$
$$
p_Y^*(\beta) = 1_X \times \beta \quad \text{for } \beta \in H^*(Y; R)
$$
这意味着从一个因[子空间](@entry_id:150286)[拉回](@entry_id:160816)的上同调类，可以简单地表示为该类与另一个空间的0次[上同调](@entry_id:160558)单位元的[叉积](@entry_id:156672)。这些形如 $\alpha \times 1_Y$ 和 $1_X \times \beta$ 的类是构成[积空间](@entry_id:151693)[上同调](@entry_id:160558)的基本元素。

#### 与[杯积](@entry_id:159554)的相互作用
在[积空间](@entry_id:151693) $X \times Y$ 上，杯积和[叉积](@entry_id:156672)遵循一个重要的**混合乘法公式**。对于任意[上同调类](@entry_id:263961) $\alpha_1 \in H^{p_1}(X)$, $\beta_1 \in H^{q_1}(Y)$, $\alpha_2 \in H^{p_2}(X)$, $\beta_2 \in H^{q_2}(Y)$，它们在 $X \times Y$ 中的杯积可以表示为：
$$
(\alpha_1 \times \beta_1) \cup (\alpha_2 \times \beta_2) = (-1)^{q_1 p_2} (\alpha_1 \cup \alpha_2) \times (\beta_1 \cup \beta_2)
$$
这个公式是进行具体计算的强大工具。符号 $(-1)^{q_1 p_2}$ 源于在概念上将 $\beta_1$ 和 $\alpha_2$ 交换位置。

让我们看一个经典应用。考虑2-维环面 $T^2 = S^1 \times S^1$。设 $\gamma \in H^1(S^1; \mathbb{Z})$ 是其生成元，$1 \in H^0(S^1; \mathbb{Z})$ 是单位元。$H^1(T^2; \mathbb{Z})$ 的一组基可以由 $a = \gamma \times 1$ 和 $b = 1 \times \gamma$ 给出。利用上述公式，我们可以计算它们的杯积 [@problem_id:1678968]：
$$
a \cup b = (\gamma \times 1) \cup (1 \times \gamma)
$$
这里 $p_1=1, q_1=0, p_2=0, q_2=1$，所以符号因子是 $(-1)^{0 \cdot 0} = 1$。因此：
$$
a \cup b = (\gamma \cup 1) \times (1 \cup \gamma) = \gamma \times \gamma
$$
$\gamma \times \gamma$ 正是 $H^2(T^2; \mathbb{Z})$ 的生成元。这个计算揭示了环面熟悉的[上同调环](@entry_id:160158)结构 $H^*(T^2; \mathbb{Z}) \cong \Lambda[a,b]$ （由 $a, b$ 生成的[外代数](@entry_id:201164)）。

在更复杂的例子中，这个公式同样有效。考虑空间 $M = T^2 \times \mathbb{CP}^2$，并设 $\alpha, \beta$ 是 $H^1(T^2)$ 的生成元，$u$ 是 $H^2(\mathbb{CP}^2)$ 的生成元。积空间中的两个类 $A = p_X^*(3\alpha - 5\beta) + p_Y^*(2u)$ 和 $B = p_X^*(\alpha \cup \beta) + p_Y^*(7u^2)$。我们可以将它们用[叉积](@entry_id:156672)表示为 $A = (3\alpha - 5\beta)\times 1 + 1 \times (2u)$ 和 $B = (\alpha\cup\beta)\times 1 + 1 \times (7u^2)$。要计算 $A \cup B$ 的5次分量，我们只需考虑能产生5次项的乘积，即 $A$ 的1次分量和 $B$ 的4次分量的杯积 [@problem_id:1678990]：
$$
[A \cup B]_{\deg 5} = ((3\alpha - 5\beta)\times 1) \cup (1 \times (7u^2))
$$
应用混合乘法公式，这里 $p_1=1, q_1=0, p_2=0, q_2=4$，符号为 $(-1)^{0 \cdot 0}=1$。
$$
[A \cup B]_{\deg 5} = ((3\alpha - 5\beta)\cup 1) \times (1 \cup (7u^2)) = (3\alpha - 5\beta) \times (7u^2) = 21(\alpha \times u^2) - 35(\beta \times u^2)
$$
这精确地确定了结果在 $H^5(M; \mathbb{Z})$ 基底下的系数。

### 几何行为与[Künneth定理](@entry_id:274959)

#### 在[子空间](@entry_id:150286)上的限制
[叉积的几何意义](@entry_id:264380)也可以通过它在积空间的[子空间](@entry_id:150286)上的行为来理解。一个重要的[子空间](@entry_id:150286)是**[楔和](@entry_id:270607) (wedge sum)** $X \vee Y$，它可以嵌入到积空间 $X \times Y$ 中，作为[子空间](@entry_id:150286) $X \times \{y_0\} \cup \{x_0\} \times Y$，其中 $x_0, y_0$ 是基点。

考虑一个叉积类 $\alpha \times \beta \in H^{p+q}(X \times Y)$ 在 $X \vee Y$ 上的限制。
- 当限制到 $X \times \{y_0\}$ 时，这个类变为 $\alpha \cup c_{y_0}^*(\beta)$，其中 $c_{y_0}: X \to Y$ 是常值映射。如果 $\beta$ 的次数 $q \gt 0$，那么它在常值映射下的[拉回](@entry_id:160816)为零，所以限制为零。
- 类似地，当限制到 $\{x_0\} \times Y$ 时，如果 $\alpha$ 的次数 $p \gt 0$，限制也为零。
因此，如果 $p, q > 0$，那么 $\alpha \times \beta$ 在整个 $X \vee Y$ 上的限制为零。

然而，形如 $\alpha \times 1_Y$ 或 $1_X \times \beta$ 的类表现不同。例如，考虑 $X=Y=S^1$，设 $u, v$ 分别是两个圆周的 $H^1$ 生成元。$H^1(X \vee Y)$ 的元素可以由它在两个圆周上的限制 $(au, bv)$ 唯一确定。考虑积空间 $X \times Y$ 中的类 $\omega = 7(u \times 1_Y) + 3(1_X \times v)$。它在 $X \vee Y$ 上的[拉回](@entry_id:160816) $i^*(\omega)$，当限制到第一个 $S^1$ 时，得到 $7u$；当限制到第二个 $S^1$ 时，得到 $3v$。因此，[拉回](@entry_id:160816)类对应于 $(7u, 3v)$ [@problem_id:1678998]。

#### [Künneth定理](@entry_id:274959)
[叉积](@entry_id:156672)是理解**[Künneth定理](@entry_id:274959)**的关键，该定理精确描述了[积空间的上同调](@entry_id:266890)。[Künneth定理](@entry_id:274959)断言，在一定条件下，[积空间的上同调](@entry_id:266890)可以通过其因[子空间](@entry_id:150286)的[上同调](@entry_id:160558)的[张量积](@entry_id:140694)来计算。[叉积](@entry_id:156672)提供了从张量积到[积空间](@entry_id:151693)[上同调](@entry_id:160558)的自然映射：
$$
\mu: \bigoplus_{p+q=n} H^p(X; R) \otimes_R H^q(Y; R) \to H^n(X \times Y; R)
$$
定义为 $\mu(\sum \alpha_i \otimes \beta_i) = \sum \alpha_i \times \beta_i$。

如果系数环 $R$ 是一个域，或者所有 $H^k(X; \mathbb{Z})$ 都是自由阿贝尔群（在使用整数系数时），那么映射 $\mu$ 是一个同构。此时，$H^*(X \times Y; R) \cong H^*(X; R) \otimes_R H^*(Y; R)$ 作为分次 $R$-模。

然而，在更一般的情况下，情况会变得复杂。
首先，映射 $\mu$ 的像可能不包含所有类型的元素。积空间中的一个上同调类不一定能写成单个“纯”叉积 $\alpha \times \beta$ 的形式，但它可以是这类项的和。例如，在 $\mathbb{C}P^1 \times \mathbb{C}P^1$ 中，设 $u, v$ 分别是从第一和第二因子[拉回](@entry_id:160816)的 $H^2$ 生成元。类 $\gamma = u+v \in H^2(\mathbb{C}P^1 \times \mathbb{C}P^1; \mathbb{Z})$ 就不是一个纯叉积。我们可以通过计算它的[杯积](@entry_id:159554)平方来验证这一点：$\gamma^2 = (u+v)^2 = u^2+2uv+v^2$。由于在 $H^*(\mathbb{C}P^1)$ 中 $x^2=0$，我们有 $u^2=0, v^2=0$，所以 $\gamma^2 = 2uv$。因为 $uv = u \times v$ 是 $H^4$ 的生成元，$\gamma^2 \neq 0$。而任何纯[叉积](@entry_id:156672)形式的2次类（例如 $x \times 1$ 或 $1 \times x$）的平方都为零。因此 $\gamma$ 不可能是纯[叉积](@entry_id:156672) [@problem_id:1679016]。

其次，当使用整数系数 $\mathbb{Z}$ 时，如果因[子空间](@entry_id:150286)的[上同调群](@entry_id:142450)包含**挠率 (torsion)**，[积空间的上同调](@entry_id:266890)可能会出现新的挠率部分，这部分不能由张量积捕获。完整的[Künneth定理](@entry_id:274959)表明存在一个短[正合序列](@entry_id:151503)：
$$
0 \to \bigoplus_{i+j=n} H^{i}(X) \otimes H^{j}(Y) \to H^{n}(X \times Y) \to \bigoplus_{i+j=n+1} \mathrm{Tor}(H^{i}(X), H^{j}(Y)) \to 0
$$
这里的 $\mathrm{Tor}(A,B)$ 是[环论](@entry_id:143825)中的**挠积[函子](@entry_id:150427) (Tor functor)**，它测量了张量积的非精确性。

例如，考虑实射影平面 $\mathbb{R}P^2$。其整数上同调为 $H^0(\mathbb{R}P^2;\mathbb{Z}) \cong \mathbb{Z}$, $H^2(\mathbb{R}P^2;\mathbb{Z}) \cong \mathbb{Z}_2$，其他次数为0。为了计算 $H^2(\mathbb{R}P^2 \times \mathbb{R}P^2; \mathbb{Z})$，我们应用Künneth序列 [@problem_id:1678988]：
- **[张量积](@entry_id:140694)部分 ($i+j=2$)**：$ (H^0 \otimes H^2) \oplus (H^1 \otimes H^1) \oplus (H^2 \otimes H^0) \cong (\mathbb{Z} \otimes \mathbb{Z}_2) \oplus (0 \otimes 0) \oplus (\mathbb{Z}_2 \otimes \mathbb{Z}) \cong \mathbb{Z}_2 \oplus \mathbb{Z}_2$。
- **Tor部分 ($i+j=3$)**：所有项如 $\mathrm{Tor}(H^1, H^2) = \mathrm{Tor}(0, \mathbb{Z}_2)=0$ 均为零。

因此，短[正合序列](@entry_id:151503)退化为 $0 \to \mathbb{Z}_2 \oplus \mathbb{Z}_2 \to H^2(\mathbb{R}P^2 \times \mathbb{R}P^2; \mathbb{Z}) \to 0$，这意味着 $H^2(\mathbb{R}P^2 \times \mathbb{R}P^2; \mathbb{Z}) \cong \mathbb{Z}_2 \oplus \mathbb{Z}_2$。这个结果清晰地表明，[积空间的上同调](@entry_id:266890)可以比因[子空间](@entry_id:150286)的[上同调](@entry_id:160558)之和更为丰富，而[叉积](@entry_id:156672)和[Künneth定理](@entry_id:274959)为我们提供了精确理解和计算这种结构的强大框架。