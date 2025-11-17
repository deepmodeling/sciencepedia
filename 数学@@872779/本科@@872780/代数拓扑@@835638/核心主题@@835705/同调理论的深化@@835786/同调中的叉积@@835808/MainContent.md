## 引言
在代数拓扑的研究中，一个核心任务是通过代数[不变量](@entry_id:148850)来理解和区分拓扑空间。当我们面对由简单空间（如 $X$ 和 $Y$）构成的[积空间](@entry_id:151693) $X \times Y$ 时，一个自然而深刻的问题随之产生：我们如何从 $X$ 和 $Y$ 的同调群信息，推导出[积空间](@entry_id:151693) $X \times Y$ 的同调群？简单地将同调群相加或相乘并不能完全捕捉其复杂的拓扑结构。同调叉积正是为了填补这一知识鸿沟而引入的强大工具，它提供了一种系统性的方法来“编织”因[子空间](@entry_id:150286)的同调类，从而生成[积空间](@entry_id:151693)的同调类。

本文将引导读者全面探索同调叉积的理论与实践。在第一部分“原理与机制”中，我们将从链复合物的张量积出发，揭示叉积的构造基础及其核心的代数法则。接着，在第二部分“应用与跨学科联系”中，我们将展示叉积如何被用于计算具体空间的同调群、理解[流形](@entry_id:153038)的几何结构，并建立与[不动点理论](@entry_id:157862)、[H-空间](@entry_id:262905)等高等论题的联系。最后，“动手实践”部分将提供一系列练习，帮助读者将理论知识转化为解决问题的实际能力。现在，让我们首先深入其构造的核心，探究叉积的原理与机制。

## 原理与机制

继上一章介绍积空间的基本[拓扑性质](@entry_id:141605)之后，本章将深入探讨代数拓扑中一个核心的构造工具——**同调叉积 (cross product in homology)**。这一工具为我们提供了从单个空间的同调群信息来构造其[积空间](@entry_id:151693)同调群元素的基本途径。理解[叉积](@entry_id:156672)的原理与机制，不仅是计算[积空间](@entry_id:151693)同调群的关键，更是揭示同调与[上同调](@entry_id:160558)之间深刻对偶性，以及理解更广泛的[代数结构](@entry_id:137052)（如[Künneth公式](@entry_id:158001)）的基石。

### 链层面的叉积：构造的基础

从最直观的角度看，如果我们有一个$p$维的对象（例如，一个$p$-单纯形或$p$-胞腔）位于空间$X$中，以及一个$q$维的对象位于空间$Y$中，那么它们在[积空间](@entry_id:151693)$X \times Y$中的[笛卡尔积](@entry_id:154642)自然地形成一个$(p+q)$维的对象。同调的[叉积](@entry_id:156672)正是对这一几何直观的代数刻画。它首先定义在链复合物的层面上。

#### [胞腔同调](@entry_id:264549)中的叉积

当空间$X$和$Y$具有[CW复形](@entry_id:150589)结构时，其[积空间](@entry_id:151693)$X \times Y$也自然地继承了一个[CW复形](@entry_id:150589)结构。$X \times Y$的$k$-胞腔是由$X$的$p$-胞腔$e^p$和$Y$的$q$-胞腔$e^q$的积$e^p \times e^q$（其中$p+q=k$）构成的。这启发我们将$X \times Y$的胞腔链复合物$C_*(X \times Y)$等同于$X$和$Y$各自胞腔链复合物的**张量积 (tensor product)**，即 $C_*(X \times Y) \cong C_*(X) \otimes C_*(Y)$。

在这一代数框架下，最核心的机制是[积空间](@entry_id:151693)中[边界算子](@entry_id:160216)$\partial$的行为。对于一个由$p$-胞腔$a \in C_p(X)$和$q$-胞腔$b \in C_q(Y)$构成的积胞腔$a \otimes b \in C_{p+q}(X \times Y)$，其边界由以下**分级[莱布尼茨法则](@entry_id:157949) (graded Leibniz rule)** 给出：
$$ \partial(a \otimes b) = (\partial a) \otimes b + (-1)^p a \otimes (\partial b) $$
这里的$(-1)^p$符号因子源于将$b$的边界“穿过”$p$维对象$a$时产生的符号。这个公式是所有叉积计算的出发点。

让我们通过一个具体的例子来理解这个法则的应用。考虑[实射影平面](@entry_id:150364)$\mathbb{R}P^2$，它有一个标准的CW结构，在0、1、2维各有一个胞腔，记为$e^0, e^1, e^2$。其（整系数）胞腔链复合物的[边界映射](@entry_id:151165)由$\partial e^2 = 2e^1$和$\partial e^1 = 0$给出。现在我们考察[积空间](@entry_id:151693)$X = \mathbb{R}P^2 \times \mathbb{R}P^2$。为了区分，我们将第一个$\mathbb{R}P^2$的胞腔记为$c^0, c^1, c^2$，第二个记为$d^0, d^1, d^2$。我们来计算$X$中唯一的4维胞腔$c^2 \times d^2$（代数上记为$c^2 \otimes d^2$）的边界[@problem_id:1679271]。
根据[莱布尼茨法则](@entry_id:157949)，其中$a=c^2$的维数$p=2$：
$$ \partial(c^2 \otimes d^2) = (\partial c^2) \otimes d^2 + (-1)^2 c^2 \otimes (\partial d^2) $$
我们已知 $\partial c^2 = 2c^1$ 和 $\partial d^2 = 2d^1$，代入上式得到：
$$ \partial(c^2 \otimes d^2) = (2c^1) \otimes d^2 + c^2 \otimes (2d^1) = 2(c^1 \otimes d^2) + 2(c^2 \otimes d^1) $$
这个结果是一个3-链，它由$X$的两个3-胞腔$c^1 \times d^2$和$c^2 \times d^1$线性组合而成。

#### [奇异同调](@entry_id:158380)中的[叉积](@entry_id:156672)

对于一般的[拓扑空间](@entry_id:155056)，我们使用[奇异同调](@entry_id:158380)。若$\sigma: \Delta^p \to X$是一个奇异$p$-单纯形，$\tau: \Delta^q \to Y$是一个奇异$q$-单纯形，它们的[叉积](@entry_id:156672)$\sigma \times \tau$是一个奇异$(p+q)$-链，而不是单个的[奇异单纯形](@entry_id:265569)。它通过一种标准方式（[Alexander-Whitney映射](@entry_id:275009)）将积单纯形$\Delta^p \times \Delta^q$剖分成一系列$(p+q)$-单纯形来定义。尽管其具体构造较为繁琐，但其边界同样遵循上述[莱布尼茨法则](@entry_id:157949)。

一个简单的例子足以说明其要点[@problem_id:1679263]。考虑一个1-单纯形$\sigma: \Delta^1 \to X$和一个0-单纯形$\tau: \Delta^0 \to Y$（即一个点$y \in Y$）。它们的[叉积](@entry_id:156672)可以被定义为一个1-单纯形$\sigma \times \tau: \Delta^1 \to X \times Y$，映射为$u \mapsto (\sigma(u), y)$。我们来计算其边界。根据[莱布尼茨法则](@entry_id:157949)（$p=1$）：
$$ \partial(\sigma \times \tau) = (\partial \sigma) \times \tau + (-1)^1 \sigma \times (\partial \tau) $$
由于$\tau$是0-单纯形，它的边界$\partial \tau = 0$。因此，公式简化为：
$$ \partial(\sigma \times \tau) = (\partial \sigma) \times \tau $$
若$\partial \sigma = P_{\sigma(v_1)} - P_{\sigma(v_0)}$，其中$P_z$是映射到点$z$的0-单纯形，那么$(\partial \sigma) \times \tau = (P_{\sigma(v_1)} - P_{\sigma(v_0)}) \times \tau = P_{\sigma(v_1)} \times \tau - P_{\sigma(v_0)} \times \tau = P_{(\sigma(v_1), y)} - P_{(\sigma(v_0), y)}$。这与直接计算1-单纯形$\sigma \times \tau$的边界所得结果完全一致，验证了[莱布尼茨法则](@entry_id:157949)的自洽性。

### 同调层面的诱导积

链层面的[叉积](@entry_id:156672)之所以重要，是因为它能自然地“下降”到同调层面，定义一个同调类之间的乘积。

设$\alpha \in H_p(X)$和$\beta \in H_q(Y)$是两个同调类。我们可以选取它们的代表闭链，即$a \in C_p(X)$使得$[a]=\alpha$（即$\partial a = 0$），以及$b \in C_q(Y)$使得$[b]=\beta$（即$\partial b = 0$）。现在我们考察它们的链层叉积$a \otimes b$。它的边界是：
$$ \partial(a \otimes b) = (\partial a) \otimes b + (-1)^p a \otimes (\partial b) = 0 \otimes b + (-1)^p a \otimes 0 = 0 $$
这意味着两个闭链的[叉积](@entry_id:156672)仍然是一个闭链，因此它定义了一个[积空间](@entry_id:151693)中的同调类$[a \otimes b] \in H_{p+q}(X \times Y)$。进一步可以证明，这个同调类不依赖于代表闭链$a$和$b$的选取。这样，我们就得到了一个良定义的**同调叉积**映射：
$$ \times: H_p(X; G) \times H_q(Y; G) \to H_{p+q}(X \times Y; G) $$

这个在同调层面上定义的乘积具有一系列优良的代数性质，使其成为一个强大的理论工具。

#### 基本代数性质

1.  **[双线性性](@entry_id:146819) (Bilinearity)**：[叉积](@entry_id:156672)对于每一个变量都是线性的。例如，对于整数$n$和同调类$\alpha, \beta$，有$n(\alpha \times \beta) = (n\alpha) \times \beta = \alpha \times (n\beta)$。这个看似简单的性质有一个直接的推论：如果$\beta$是一个挠类（torsion class），即存在非零整数$n$使得$n\beta = 0$，那么对于任何同调类$\alpha$，它们的叉积$\alpha \times \beta$也必然是一个挠类[@problem_id:1679233]。这是因为$n(\alpha \times \beta) = \alpha \times (n\beta) = \alpha \times 0 = 0$。

2.  **自然性 (Naturality)**：叉积与连续映射的[诱导同态](@entry_id:266478)相容。对于[连续映射](@entry_id:153855)$f: X \to X'$和$g: Y \to Y'$，以及同调类$\alpha \in H_p(X)$和$\beta \in H_q(Y)$，我们有：
    $$ (f \times g)_*(\alpha \times \beta) = f_*(\alpha) \times g_*(\beta) $$
    其中$f \times g: X \times Y \to X' \times Y'$是积映射。这个性质表明，先做叉积再通过映射$f \times g$推向前，等价于先将各个因子推向前再做[叉积](@entry_id:156672)。
    例如，若$f: X \to X$和$g: Y \to Y$分别是使得$f_*(\alpha) = k\alpha$和$g_*(\beta) = l\beta$的自映射（$k,l$为整数），那么积映射$F=f \times g$作用在叉积类$\gamma = \alpha \times \beta$上的效果是[@problem_id:1679259]：
    $$ F_*(\gamma) = F_*(\alpha \times \beta) = f_*(\alpha) \times g_*(\beta) = (k\alpha) \times (l\beta) = kl(\alpha \times \beta) = kl\gamma $$
    这表明[叉积](@entry_id:156672)类的“[特征值](@entry_id:154894)”是因子类“[特征值](@entry_id:154894)”的乘积。

3.  **分级交换性 (Graded Commutativity)**：交换$X$和$Y$的次序不是无代价的。令$T: X \times Y \to Y \times X$是交换坐标的映射，$T(x,y)=(y,x)$。它在同调上诱导的映射满足：
    $$ T_*(\alpha \times \beta) = (-1)^{pq} (\beta \times \alpha) $$
    其中$p = \deg \alpha$，$q = \deg \beta$。符号$(-1)^{pq}$是Koszul符号规则的体现。
    举例来说，考虑$S^1$的1维生成元$\alpha \in H_1(S^1)$和$S^2$的2维生成元$\beta \in H_2(S^2)$[@problem_id:1679278]。这里$p=1, q=2$，因此$pq=2$是偶数。交换映射$T: S^1 \times S^2 \to S^2 \times S^1$作用在[叉积](@entry_id:156672)类$\alpha \times \beta$上，我们得到：
    $$ T_*(\alpha \times \beta) = (-1)^{1 \cdot 2} (\beta \times \alpha) = (+1) (\beta \times \alpha) = \beta \times \alpha $$
    这意味着在这种情况下，交换坐标的同态将$\alpha \times \beta$映射到$\beta \times \alpha$而不改变符号。

4.  **[结合性](@entry_id:147258) (Associativity)**：对于三个空间$X, Y, Z$中的同调类$\alpha, \beta, \gamma$，在自然的[同胚](@entry_id:146933)$(X \times Y) \times Z \cong X \times (Y \times Z)$下，我们有$(\alpha \times \beta) \times \gamma = \alpha \times (\beta \times \gamma)$。[结合性](@entry_id:147258)与[交换性](@entry_id:140240)一起，可以用来计算任意因子[置换](@entry_id:136432)所产生的符号。例如，一个三因子的[循环置换](@entry_id:272913)$(1,2,3) \to (2,3,1)$可以分解为两次相邻[对换](@entry_id:142115)：$(1,2,3) \to (1,3,2) \to (2,3,1)$。如果$\alpha_i \in H_1(X_i)$，那么$\alpha_1 \times \alpha_2 \times \alpha_3$在[置换](@entry_id:136432)下变为$\alpha_2 \times \alpha_3 \times \alpha_1$时，符号变化为$(-1)^{1 \cdot 1}(-1)^{1 \cdot (1+1)} = (-1)(+1) = -1$。[@problem_id:1679255]

### 进阶应用与关联

叉积的真正威力体现在它与其他拓扑不变量和构造的深刻联系中。

#### [相对同调](@entry_id:159348)与长正合列

[叉积](@entry_id:156672)可以推广到[相对同调群](@entry_id:159711)。对于空间偶$(X, A)$和$(Y, B)$，叉积是一个映射：
$$ \times: H_p(X, A) \times H_q(Y, B) \to H_{p+q}(X \times Y, A \times Y \cup X \times B) $$
这个相对版本的叉积与[相对同调](@entry_id:159348)的长正合列中的**[连接同态](@entry_id:160713) (connecting homomorphism)** $\partial_*$ 优美地结合在一起，同样遵循一个[莱布尼茨法则](@entry_id:157949)：
$$ \partial_*(\mu \times \nu) = (\partial_* \mu) \times \nu + (-1)^{\deg \mu} \mu \times (\partial_* \nu) $$
这里$\mu \in H_p(X,A)$，$\nu \in H_q(Y,B)$。

这个性质是计算嵌入在更大空间中的[子空间](@entry_id:150286)偶同调的有力工具。例如，考虑空间偶$(D^2 \times S^1, S^1 \times S^1)$，即实心环柄及其边界环面。令$\iota_2$是$H_2(D^2, S^1)$的生成元，$\sigma_1$是$H_1(S^1)$的生成元，并约定[连接同态](@entry_id:160713)$\partial_*(\iota_2) = \sigma_1 \in H_1(S^1)$。我们想计算$\gamma = \iota_2 \times \sigma_1 \in H_3(D^2 \times S^1, S^1 \times S^1)$在[连接同态](@entry_id:160713)$\partial_*: H_3(D^2 \times S^1, S^1 \times S^1) \to H_2(S^1 \times S^1)$下的像[@problem_id:1679237][@problem_id:1679280]。
应用上述[莱布尼茨法则](@entry_id:157949)（注意$\sigma_1 \in H_1(S^1, \emptyset)$，所以对它的[连接同态](@entry_id:160713)为零）：
$$ \partial_*(\iota_2 \times \sigma_1) = (\partial_* \iota_2) \times \sigma_1 + (-1)^2 \iota_2 \times (\partial_* \sigma_1) = \sigma_1 \times \sigma_1 + \iota_2 \times 0 = \sigma_1 \times \sigma_1 $$
我们知道$H_2(S^1 \times S^1) \cong \mathbb{Z}$的生成元正是$\tau = \sigma_1 \times \sigma_1$。因此$\partial_*(\gamma) = \tau$。更进一步，由于空间$D^2 \times S^1$与$S^1$同伦等价，其3维同调群为0。长正合列片段 $H_3(D^2 \times S^1) \to H_3(D^2 \times S^1, S^1 \times S^1) \xrightarrow{\partial_*} H_2(S^1 \times S^1) \to H_2(D^2 \times S^1)$ 简化为 $0 \to \mathbb{Z} \xrightarrow{\partial_*} \mathbb{Z} \to 0$。这表明$\partial_*$是一个同构。因此，$\gamma=\iota_2 \times \sigma_1$一定是$H_3(D^2 \times S^1, S^1 \times S^1)$的生成元（或其负元）。

#### 与上同调杯积的对偶关系

同调[叉积](@entry_id:156672)与上同调中的**[杯积](@entry_id:159554) (cup product)** $\smile$ 之间存在深刻的对偶关系。这种关系通过**对角映射 (diagonal map)** $\Delta: X \to X \times X$（定义为$\Delta(x) = (x,x)$）来建立。令$\phi \in H^p(X), \psi \in H^q(X)$为上同调类，$\alpha \in H_{p+q}(X)$为同调类。它们之间的关系由以下基本恒等式给出：
$$ \langle \phi \smile \psi, \alpha \rangle = \langle \phi \times \psi, \Delta_*(\alpha) \rangle $$
这里左边的$\langle \cdot, \cdot \rangle$是上同调类与同调类之间的求值配对（Kronecker积），右边的$\phi \times \psi$是[上同调](@entry_id:160558)的外积（external product），$\Delta_*(\alpha)$是$\alpha$在对角映射下的像。

这个恒等式非常强大。例如，考虑2维环面$T^2$，其$H_1(T^2)$有一组基$\{a, b\}$，$H_2(T^2)$的生成元为$\mu$。$H^1(T^2)$有对偶基$\{a^*, b^*\}$，满足$\langle a^*, a \rangle = 1, \langle a^*, b \rangle = 0$等。假设定向使得$\langle a^* \smile b^*, \mu \rangle = 1$。我们想确定$\Delta_*(\mu)$在$H_2(T^2 \times T^2)$的基$\{a \times b, b \times a, \dots\}$中的展开式系数[@problem_id:1679269]。设$\Delta_*(\mu) = c_1(a \times b) + c_2(b \times a) + \dots$。
利用上述恒等式，我们有：
$$ 1 = \langle a^* \smile b^*, \mu \rangle = \langle a^* \times b^*, \Delta_*(\mu) \rangle $$
将$\Delta_*(\mu)$的展开式代入，并利用外积的求值法则$\langle \phi' \times \psi', c'_k \times c'_l \rangle = (-1)^{\deg(\psi')\deg(c'_k)} \langle \phi', c'_k \rangle \langle \psi', c'_l \rangle$，我们可以逐项计算。对于$a^* \times b^*$，只有与$a \times b$的配对不为零：
$$ \langle a^* \times b^*, a \times b \rangle = (-1)^{1 \cdot 1} \langle a^*, a \rangle \langle b^*, b \rangle = (-1)(1)(1) = -1 $$
与其他基元的配对均为零。因此，
$$ 1 = \langle a^* \times b^*, \Delta_*(\mu) \rangle = c_1 \cdot \langle a^* \times b^*, a \times b \rangle = c_1 \cdot (-1) $$
由此解得$c_1 = -1$。这清晰地展示了如何利用[叉积](@entry_id:156672)与杯积的对偶性来计算对角映射在同调上的复杂作用。

#### [Künneth公式](@entry_id:158001)与挠积

最后，[叉积](@entry_id:156672)是著名的**[Künneth公式](@entry_id:158001)**的核心。该公式描述了[积空间](@entry_id:151693)$X \times Y$的同调群与因[子空间](@entry_id:150286)$X, Y$同调群的关系。在最简单的情况下（例如，当系数域是域，或当其中一个空间的[整同调](@entry_id:276347)群是自由的），[Künneth公式](@entry_id:158001)表明[叉积](@entry_id:156672)诱导了一个同构：
$$ \bigoplus_{p+q=k} H_p(X) \otimes H_q(Y) \xrightarrow{\cong} H_k(X \times Y) $$
这意味着$H_k(X \times Y)$中的每一个同调类都可以表示为形如$\sum_i \alpha_i \times \beta_i$的叉积和。

然而，在处理整系数同调时，情况变得更加复杂。完整的[Künneth定理](@entry_id:274959)包含一个额外的项，称为**挠积 (torsion product)**，记为$\text{Tor}$：
$$ H_k(X \times Y; \mathbb{Z}) \cong \left( \bigoplus_{p+q=k} H_p(X) \otimes H_q(Y) \right) \oplus \left( \bigoplus_{p+q=k-1} \text{Tor}(H_p(X), H_q(Y)) \right) $$
这意味着$H_k(X \times Y)$中可能存在无法表示为因[子空间](@entry_id:150286)同调类之[叉积](@entry_id:156672)的元素。这些元素正是由$\text{Tor}$项产生的。

一个经典的例子是$X = \mathbb{R}P^2 \times \mathbb{R}P^2$的3维[整同调](@entry_id:276347)群$H_3(X; \mathbb{Z})$ [@problem_id:1679239]。我们已知$H_0(\mathbb{R}P^2) \cong \mathbb{Z}$, $H_1(\mathbb{R}P^2) \cong \mathbb{Z}_2$, $H_2(\mathbb{R}P^2) \cong 0$。因此，在$H_3(X)$中，来自$H_p \otimes H_q$项（其中$p+q=3$）的贡献均为0。然而，来自$\text{Tor}$项的贡献不为零：$\text{Tor}(H_1(\mathbb{R}P^2), H_1(\mathbb{R}P^2)) = \text{Tor}(\mathbb{Z}_2, \mathbb{Z}_2) \cong \mathbb{Z}_2$。因此[Künneth公式](@entry_id:158001)预言$H_3(\mathbb{R}P^2 \times \mathbb{R}P^2) \cong \mathbb{Z}_2$。

这个2阶挠类的代表闭链是什么？它不能是$\alpha \times \beta$的形式。回顾胞腔链的计算，其中$\partial e^1=0$且$\partial e^2=2e^1$。令$e^k_1$和$e^k_2$分别为两个$\mathbb{R}P^2$因子的胞腔链生成元。一个3-链$z = A(e^2_1 \otimes e^1_2) + B(e^1_1 \otimes e^2_2)$的边界是$\partial z = A \cdot \partial(e^2_1 \otimes e^1_2) + B \cdot \partial(e^1_1 \otimes e^2_2) = A(2e^1_1 \otimes e^1_2) + B(-2e^1_1 \otimes e^1_2) = 2(A-B)(e^1_1 \otimes e^1_2)$。因此，$z$是闭链当且仅当$A=B$。取$A=B=1$，得到闭链$z = e^2_1 \otimes e^1_2 + e^1_1 \otimes e^2_2$。同时，4-胞腔的边界是$\partial(e^2_1 \otimes e^2_2) = (\partial e^2_1) \otimes e^2_2 + e^2_1 \otimes (\partial e^2_2) = (2e^1_1) \otimes e^2_2 + e^2_1 \otimes (2e^1_2) = 2(e^1_1 \otimes e^2_2 + e^2_1 \otimes e^1_2) = 2z$。
这意味着$z$本身不是边界，但$2z$是边界。因此，$z$在同调群中代表一个2阶元素，它正是$H_3(\mathbb{R}P^2 \times \mathbb{R}P^2)$的生成元。这个例子完美地说明了，积空间的同调可以比其因[子空间](@entry_id:150286)同调类的简单乘积更为丰富，而叉积理论正是理解这种丰富性的关键所在。