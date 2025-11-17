## 引言
在现代几何学中，[复流形](@entry_id:159076)以其丰富的解析结构和与代数几何的深刻联系占据着核心地位。然而，从一个光滑实[流形](@entry_id:153038)的角度来看，我们如何判断它是否能够被赋予一个[复结构](@entry_id:269128)呢？这一问题引出了**近复结构**的概念——一个定义在[切丛](@entry_id:161294)上的简单代数条件 $J^2 = -\mathrm{Id}$。这个定义虽然简单，却引出了一个根本性的几何问题：一个抽象的近复结构在何种条件下才能真正“积分”成一个具有全纯坐标图卡的[复流形](@entry_id:159076)？这便是可积性问题，也是本文旨在解决的知识鸿沟。

为系统地回答这一问题，本文将分为三个部分。在“**原理与机制**”一章中，我们将奠定理论基石，从近[复结构](@entry_id:269128)的代数定义出发，引入衡量[可积性](@entry_id:142415)障碍的尼氏张量，并阐述深刻的[Newlander-Nirenberg定理](@entry_id:158862)。接着，在“**应用与交叉联系**”一章中，我们将展示这一理论的深远影响，探讨[可积性](@entry_id:142415)如何区分[复几何](@entry_id:159080)与[辛几何](@entry_id:160783)，并揭示其在[代数几何](@entry_id:156300)、[伪全纯曲线](@entry_id:201654)理论乃至Twistor理论中的关键作用。最后，“**动手实践**”部分将通过具体计算，帮助读者将抽象理论内化为扎实的技能。

通过这一系列的学习，读者将不仅掌握近复结构的核心理论，更能体会到它如何成为连接[微分几何](@entry_id:145818)、复分析与数学物理等多个领域的桥梁。现在，让我们从第一章开始，深入探索近复结构的内在原理与机制。

## 原理与机制

本章旨在深入探讨近复结构的内在原理与核心机制。我们将从其基本代数定义出发，逐步引入其在切丛上的几何分解，并最终聚焦于[可积性](@entry_id:142415)这一核心问题。我们将阐明近[复结构](@entry_id:269128)何时能够“局部地”等同于一个真正的[复流形](@entry_id:159076)结构，并介绍用以衡量这一点的关键工具——尼氏张量。通过著名的[Newlander-Nirenberg定理](@entry_id:158862)，我们将揭示[可积性](@entry_id:142415)的几个等价刻画，并展示其在[微分几何](@entry_id:145818)与[复分析](@entry_id:167282)中的深远意义。最后，我们将探讨近复结构与[黎曼度量](@entry_id:754359)的相互作用，最终引出对几乎厄米[流形](@entry_id:153038)进行精细分类的Gray-Hervella纲领。

### 近[复结构](@entry_id:269128)的代数定义与典范例子

一个光滑偶数维[流形](@entry_id:153038) $M^{2n}$ 上的**近[复结构](@entry_id:269128) (almost complex structure)** 是一个光滑的 $(1,1)$-型[张量场](@entry_id:190170) $J \in \Gamma(\mathrm{End}(TM))$，它在每一点 $p \in M$ 的切空间 $T_pM$ 上都定义了一个线性变换 $J_p: T_pM \to T_pM$，并满足如下代数关系：
$$
J^2 = -\mathrm{Id}
$$
其中 $\mathrm{Id}$ 是切丛上的[恒等变换](@entry_id:264671)。这个简单的代数条件蕴含了丰富的几何内容。首先，它要求 $J$ 的[特征值](@entry_id:154894)必须是 $\pm i$，由于 $J$ 是一个作用在实[向量空间](@entry_id:151108)上的实线性算子，这意味着[流形](@entry_id:153038)的维数必须是偶数。

理解一个抽象定义最好的方式，莫过于研究其最核心的例子。考虑 $2n$ 维欧氏空间 $\mathbb{R}^{2n}$，其上的标准坐标为 $(x_1, y_1, \dots, x_n, y_n)$。我们可以通过 $z_j = x_j + i y_j$ 将其与复空间 $\mathbb{C}^n$ 等同起来。在这个空间上，我们可以定义一个**标准近复结构** $J_0$，其作用在坐标切向量上定义为：
$$
J_0\left(\frac{\partial}{\partial x_j}\right) = \frac{\partial}{\partial y_j}, \quad J_0\left(\frac{\partial}{\partial y_j}\right) = -\frac{\partial}{\partial x_j}
$$
对于任意 $j=1, \dots, n$。这在几何上对应于将每个 $(x_j, y_j)$ 平面逆时针旋转 $\frac{\pi}{2}$。我们可以直接验证 $J_0$ 确实是一个近[复结构](@entry_id:269128) [@problem_id:2968633]：
$$
J_0^2\left(\frac{\partial}{\partial x_j}\right) = J_0\left(\frac{\partial}{\partial y_j}\right) = -\frac{\partial}{\partial x_j}
$$
$$
J_0^2\left(\frac{\partial}{\partial y_j}\right) = J_0\left(-\frac{\partial}{\partial x_j}\right) = -J_0\left(\frac{\partial}{\partial x_j}\right) = -\frac{\partial}{\partial y_j}
$$
由于 $J_0^2$ 在所有[基向量](@entry_id:199546)上的作用都是乘以 $-1$，故 $J_0^2 = -\mathrm{Id}$。

从线性代数的角度看，在基底 $\{\frac{\partial}{\partial x_1}, \frac{\partial}{\partial y_1}, \dots, \frac{\partial}{\partial x_n}, \frac{\partial}{\partial y_n}\}$ 下，$J_0$ 的[矩阵表示](@entry_id:146025)是一个由 $n$ 个 $2 \times 2$ 块组成的[块对角矩阵](@entry_id:145530)：
$$
[J_0] = \begin{pmatrix} A  0  \dots  0 \\ 0  A  \dots  0 \\ \vdots  \vdots  \ddots  \vdots \\ 0  0  \dots  A \end{pmatrix}, \quad \text{其中 } A = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}
$$
因此，$J_0$ 的[特征多项式](@entry_id:150909)是单个块的[特征多项式](@entry_id:150909)的 $n$ 次方。单个块的[特征多项式](@entry_id:150909)为 $\det(A - \lambda I_2) = \lambda^2+1$。所以，$J_0$ 的[特征多项式](@entry_id:150909)为 $p_{J_0}(\lambda) = (\lambda^2+1)^n$ [@problem_id:2968633]。这再次确认了其[特征值](@entry_id:154894)只能是 $\pm i$。

### [复化](@entry_id:260775)切丛与类型分解

为了更深入地[分析算子](@entry_id:746429) $J$，一个强大的工具是**[复化](@entry_id:260775) (complexification)**。我们将实[切丛](@entry_id:161294) $TM$ [张量积](@entry_id:140694) $\mathbb{C}$，得到[复化](@entry_id:260775)切丛 $T_\mathbb{C}M = TM \otimes_{\mathbb{R}} \mathbb{C}$。$J$ 可以自然地拓展为 $T_\mathbb{C}M$ 上的一个复[线性算子](@entry_id:149003)，我们仍记为 $J$。在这个[复向量丛](@entry_id:276223)上，$J$ 就可以被[对角化](@entry_id:147016)了。其[特征值](@entry_id:154894)为 $i$ 和 $-i$ 的特征[子空间](@entry_id:150286)分别记为 $T^{1,0}M$ 和 $T^{0,1}M$。

于是，[复化](@entry_id:260775)[切丛](@entry_id:161294)可以分解为两个子丛的直和 [@problem_id:2979132]：
$$
T_\mathbb{C}M = T^{1,0}M \oplus T^{0,1}M
$$
其中，$T^{1,0}M = \{X - iJX \mid X \in TM\}$ 是对应于[特征值](@entry_id:154894) $i$ 的特征丛，而 $T^{0,1}M = \{X + iJX \mid X \in TM\}$ 是对应于[特征值](@entry_id:154894) $-i$ 的特征丛。任何一个复切向量场 $Z \in \Gamma(T_\mathbb{C}M)$ 都可以唯一地分解为它的 $(1,0)$-[部分和](@entry_id:162077) $(0,1)$-部分。这个分解可以通过两个投影算子来实现 [@problem_id:2979132]：
$$
P^{1,0} = \frac{1}{2}(\mathrm{Id} - iJ), \quad P^{0,1} = \frac{1}{2}(\mathrm{Id} + iJ)
$$
这两个算子是幂等的 ($P^2=P$)，并且它们的像分别是 $T^{1,0}M$ 和 $T^{0,1}M$。

值得强调的是，**任何近复结构**，无论是否“好”，都允许我们进行这样的分解。这个分解的存在性仅仅依赖于 $J^2 = -\mathrm{Id}$ 这个代数条件 [@problem_id:2979132]。近[复结构](@entry_id:269128)的几何性质，特别是可积性，将取决于这两个子丛的性质，而非它们的存在性本身。

这个分解也自然地延伸到[余切丛](@entry_id:185138)和[微分形式](@entry_id:146747)上。复值[1-形式](@entry_id:270392)的空间 $\Lambda^1_\mathbb{C}M$ 分解为 $\Lambda^{1,0}M \oplus \Lambda^{0,1}M$，其中 $\Lambda^{1,0}M$ 中的形式在 $T^{0,1}M$ 的向量上取值为零，反之亦然。更高阶的[微分形式](@entry_id:146747)丛 $\Lambda^k_\mathbb{C}M$ 则可以进行更精细的**双次分解 (bigrading)**：
$$
\Lambda^k_\mathbb{C}M = \bigoplus_{p+q=k} \Lambda^{p,q}M
$$
其中 $\Lambda^{p,q}M$ 是由 $p$ 个 $(1,0)$-形式和 $q$ 个 $(0,1)$-形式的[楔积](@entry_id:147029)张成的空间。

为了更具体地理解 $(1,0)$-形式的含义，我们可以考虑一个局部地适应 $J$ 的 $g$-标准正交实[标架场](@entry_id:160577) $\{e_1, \dots, e_{2n}\}$，使得 $Je_k = e_{k+n}$。设其对偶[余标架](@entry_id:637284)为 $\{\theta^1, \dots, \theta^{2n}\}$。我们可以构造一组复值1-形式 $\alpha^k = \theta^k + i \theta^{k+n}$。通过直接计算可以验证，对于任意[切向量](@entry_id:265494) $v$，都有 $\alpha^k(Jv) = i\alpha^k(v)$ [@problem_id:2968626]。这正是 $\alpha^k$ 属于 $\Lambda^{1,0}M$ 的定义，因为它在 $J$ 的作用下表现得就像乘以 $i$。

### [可积性](@entry_id:142415)与尼氏张量

现在我们来探讨本章的核心问题：一个抽象定义的近[复结构](@entry_id:269128) $J$ 在何种条件下才能真正地成为一个“复结构”？换言之，我们什么时候可以找到一个局部的复坐标图卡 $\{z^1, \dots, z^n\}$，使得 $J$ 的作用恰好是标准结构 $J_0$ 的作用，即“乘以 $i$”？满足此条件的近[复结构](@entry_id:269128)被称为**可积的 (integrable)**。

可积性的关键在于 $J$ 与[流形](@entry_id:153038)上另一个內蕴的几何结构——[李括号](@entry_id:636461)——的相容性。李括号 $[X, Y]$ 衡量了沿着向量场 $X$ 和 $Y$ 的流的交换顺序的差异，是一个纯粹的微分几何概念。如果 $J$ 是可积的，那么它应该与李括号以一种和谐的方式共存。这种相容性的“失败”程度，由**尼氏张量 (Nijenhuis tensor)** $N_J$ 来衡量，其定义为 [@problem_id:3025479]：
$$
N_J(X, Y) = [JX, JY] - J[JX, Y] - J[X, JY] - [X, Y]
$$
对于任意向量场 $X, Y \in \Gamma(TM)$。注意，在定义中我们已经利用了 $J^2 = -\mathrm{Id}$ 来替换了传统定义中的 $J^2[X,Y]$ 项。

尼氏张量是一个张量，意味着它在每一点的值仅依赖于该点 $X$ 和 $Y$ 的值，而与其延拓方式无关。它本质上衡量了 $J$ 与李括号运算交换的失败程度。如果 $J$ 与[李括号](@entry_id:636461)可交换，我们期望 $[JX,JY]$ 等于 $J[X,Y]$ 的某种形式，而尼氏张量正是刻画了它们之间的差异。

对于 $\mathbb{R}^{2n}$ 上的标准结构 $J_0$，由于坐标[向量场的李括号](@entry_id:193400)恒为零（例如 $[\frac{\partial}{\partial x_j}, \frac{\partial}{\partial y_k}]=0$），我们可以直接计算出 $N_{J_0}(X, Y)$ 在所有[坐标基](@entry_id:270149)向量对上都为零。由于其张量性，这表明 $N_{J_0} \equiv 0$ [@problem_id:2968633]。这证实了一个我们早已知道的事实：$J_0$ 是可积的，因为它本身就是由复[坐标系](@entry_id:156346) $(z_1, \dots, z_n)$ 定义的。

### [Newlander-Nirenberg定理](@entry_id:158862)

尼氏张量的真正威力在于，它的消失不仅是[可积性](@entry_id:142415)的必要条件，而且是充分条件。这便是深刻的**[Newlander-Nirenberg定理](@entry_id:158862)**。

**定理 (Newlander-Nirenberg):** 设 $M$ 是一个 $C^2$ 类[光滑流形](@entry_id:160799)，其上带有一个 $C^1$ 类的近[复结构](@entry_id:269128) $J$。那么，$J$ 是可积的（即，在每一点附近都存在 $C^2$ 类的局部复坐标图卡，使得 $J$ 在此坐标下为标准结构 $J_0$）当且仅当其尼氏张量恒为零，即 $N_J \equiv 0$。

该定理为[可积性](@entry_id:142415)提供了一系列等价的刻画 [@problem_id:3025479] [@problem_id:3034880]：
1.  **代数条件:** $N_J \equiv 0$。
2.  **几何条件 ([分布](@entry_id:182848)的对合性):** 子丛 $T^{1,0}M$（以及 $T^{0,1}M$）在[李括号](@entry_id:636461)下是**对合的 (involutive)**。也就是说，任意两个 $(1,0)$-型[向量场的李括号](@entry_id:193400)仍然是 $(1,0)$-型的：
    $$
    \forall X, Y \in \Gamma(T^{1,0}M), \quad [X, Y] \in \Gamma(T^{1,0}M)
    $$
3.  **分析条件 ([局部坐标](@entry_id:181200)的存在性):** 在每一点附近，都存在一组局部[复值函数](@entry_id:196054) $z^1, \dots, z^n$，它们构成了局部坐标系，并且满足所谓的Cauchy-Riemann方程 $\bar{\partial}_J z^k = 0$。

对合性条件是[Frobenius定理](@entry_id:181858)的复版本。它保证了对合的[分布](@entry_id:182848) $T^{1,0}M$ 是可积的，即存在一个[叶状结构](@entry_id:160209)，其叶片在局部由满足 $W(f)=0$ 的函数 $f$ 定义，其中 $W$ 是 $T^{0,1}M$ 中的任意向量场。这些函数正是我们所寻找的局部全纯坐标。

当一个近复结构是可积的，并且我们找到了相应的全纯[坐标系](@entry_id:156346) $\{z^\alpha\}$ 时，几何结构会变得异常简洁。在此[坐标系](@entry_id:156346)下，$(1,0)$-型和 $(0,1)$-型的[基向量](@entry_id:199546)场可以简单地写成 $Z_\alpha = \frac{\partial}{\partial z^\alpha}$ 和 $\bar{Z}_\alpha = \frac{\partial}{\partial \overline{z}^\alpha}$。由于[偏导数](@entry_id:146280)的[可交换性](@entry_id:263314)，这些[基向量](@entry_id:199546)场之间的李括号全部为零 [@problem_id:2968607]：
$$
[Z_\alpha, Z_\beta] = 0, \quad [\bar{Z}_\alpha, \bar{Z}_\beta] = 0, \quad [Z_\alpha, \bar{Z}_\beta] = 0
$$
这完美地体现了对合性条件，并且实际上是一个更强的“局部可交换”条件。

反之，如果一个近复结构是不可积的，那么它的 $T^{0,1}M$ (或 $T^{1,0}M$) [分布](@entry_id:182848)就不是对合的。我们可以构造一个具体的例子来感受这一点。在 $\mathbb{R}^4$ 上，考虑由以下两个向量场局部张成的 $(0,1)$-空间 [@problem_id:2968610]：
$$
X^{0,1} = \frac{\partial}{\partial \bar{z}}, \quad Y^{0,1} = \frac{\partial}{\partial \bar{w}} + \bar{z}\frac{\partial}{\partial z}
$$
直接计算它们的[李括号](@entry_id:636461)可以得到：
$$
[X^{0,1}, Y^{0,1}] = \left[ \frac{\partial}{\partial \bar{z}}, \frac{\partial}{\partial \bar{w}} + \bar{z}\frac{\partial}{\partial z} \right] = \left[ \frac{\partial}{\partial \bar{z}}, \frac{\partial}{\partial \bar{w}} \right] + \left( \frac{\partial\bar{z}}{\partial \bar{z}} \right) \frac{\partial}{\partial z} + \bar{z} \left[ \frac{\partial}{\partial \bar{z}}, \frac{\partial}{\partial z} \right] = \frac{\partial}{\partial z}
$$
得到的结果 $\frac{\partial}{\partial z}$ 是一个纯粹的 $(1,0)$-型向量场。这意味着两个 $(0,1)$-型[向量场的李括号](@entry_id:193400)“泄露”到了 $(1,0)$-空间中，因此该[分布](@entry_id:182848)不是对合的，对应的近[复结构](@entry_id:269128)也不是可积的。这个非零的 $(1,0)$-部分正是尼氏张量的一个分量。

### [可积性](@entry_id:142415)的其他视角

除了尼氏张量，我们还可以从其他角度来理解[可积性](@entry_id:142415)。

#### 李导数视角

可积性与李导数 $\mathcal{L}_X J$ 密切相关。通过对尼氏张量的定义进行代数变形，我们可以得到一个优美的恒等式，它将 $N_J$ 与 $J$ 的[李导数](@entry_id:171745)联系起来 [@problem_id:3000542]：
$$
N_J(X,Y) = (\mathcal{L}_{JX} J)(Y) - J\big((\mathcal{L}_X J)(Y)\big)
$$
根据[Newlander-Nirenberg定理](@entry_id:158862)，$J$ 可积当且仅当 $N_J \equiv 0$。因此，上述恒等式给出了可积性的一个新判据：$J$ 是可积的，当且仅当对于所有向量场 $X$，以下算子等式成立：
$$
\mathcal{L}_{JX} J = J \circ \mathcal{L}_X J
$$
这个判据在某些代数推导中非常有用。需要注意的是，可积性并不意味着 $\mathcal{L}_X J = 0$ 对所有 $X$ 成立。$\mathcal{L}_X J = 0$ 的向量场被称为**全纯向量场**或 $J$ 的无穷小[自同构](@entry_id:155390)，一般的[复流形](@entry_id:159076)上并非所有向量场都是全纯的。

#### [外微分](@entry_id:161900)视角与[Dolbeault复形](@entry_id:181288)

[可积性](@entry_id:142415)最深刻的影响之一，是它决定了外微分算子 $d$ 在 $(p,q)$-形式分解下的行为。

对于一个任意的近复结构，外[微分算子](@entry_id:140145) $d$ 作用在一个 $(p,q)$-形式上时，其结果的类型可能会很复杂。然而，当且仅当 $J$ 是可积的 ($N_J \equiv 0$)，外微分算子 $d$ 会干净地分裂为两部分 [@problem_id:3034880]：
$$
d = \partial + \bar{\partial}
$$
其中 $\partial$ 是一个将 $(p,q)$-形式映为 $(p+1,q)$-形式的算子（称为**Dolbeault算子**），而 $\bar{\partial}$ 是一个将 $(p,q)$-形式映为 $(p,q+1)$-形式的算子（称为**共轭Dolbeault算子**）。

由基本的[外代数](@entry_id:201164)恒等式 $d^2 = d \circ d = 0$，我们可以推导出：
$$
0 = d^2 = (\partial + \bar{\partial})^2 = \partial^2 + (\partial\bar{\partial} + \bar{\partial}\partial) + \bar{\partial}^2
$$
由于这三个部分分别映到不同类型的形式空间中，它们必须各自为零。因此，在可[积流形](@entry_id:270208)上我们有：
$$
\partial^2 = 0, \quad \bar{\partial}^2 = 0, \quad \partial\bar{\partial} = -\bar{\partial}\partial
$$
条件 $\bar{\partial}^2 = 0$ 意味着我们可以将 $(\Lambda^{p,\bullet}(M), \bar{\partial})$ 视为一个上[链复形](@entry_id:150246)，即所谓的**[Dolbeault复形](@entry_id:181288)**。这个复形的上同调群 $H^{p,q}_{\bar{\partial}}(M)$，即**[Dolbeault上同调](@entry_id:203257)群**，是复流形上最重要的[不变量](@entry_id:148850)之一，它携带了[流形](@entry_id:153038)丰富的全纯结构信息。这一切都源于尼氏张量的消失。

### [度量兼容性](@entry_id:265910)：从厄米到凯勒

当[流形](@entry_id:153038)上不仅有近复结构 $J$，还有一个与之**兼容 (compatible)** 的黎曼度量 $g$ 时，我们就得到了一个**几乎厄米[流形](@entry_id:153038) (almost Hermitian manifold)**。兼容性意味着 $g(JX, JY) = g(X,Y)$ 对所有向量场 $X, Y$ 成立。这个条件等价于说 $J$ 对于度量 $g$ 而言是一个[等距变换](@entry_id:150881)。

在几乎厄米[流形](@entry_id:153038)上，我们可以定义一个重要的[2-形式](@entry_id:188008)，称为**[基本2-形式](@entry_id:183276) (fundamental 2-form)** $\omega$：
$$
\omega(X,Y) = g(JX,Y)
$$
这个形式是反对称的，并且是一个 $(1,1)$-形式。

兼容度量的存在也使得 $(1,0)$-型和 $(0,1)$-型[子空间](@entry_id:150286)在某种意义下是“正交”的。具体来说，如果我们定义切丛上的[厄米度量](@entry_id:202337) $h(U,V) = g_{\mathbb{C}}(U, \overline{V})$，其中 $g_{\mathbb{C}}$ 是 $g$ 的复[双线性](@entry_id:146819)延拓，$\overline{V}$ 是对 $V$ 的共轭，那么 $T^{1,0}M$ 和 $T^{0,1}M$ 关于 $h$ 是正交的 [@problem_id:2979132]。更有趣的是，对于任何两个 $(1,0)$-向量 $U, W$，我们有 $g_{\mathbb{C}}(U,W) = g_{\mathbb{C}}(JU,JW) = g_{\mathbb{C}}(iU, iW) = -g_{\mathbb{C}}(U,W)$，这意味着 $g_{\mathbb{C}}(U,W)=0$。也就是说，$T^{1,0}M$（以及 $T^{0,1}M$）是关于 $g_{\mathbb{C}}$ 的**迷向[子空间](@entry_id:150286) (isotropic subspace)**。

当一个几乎厄米[流形](@entry_id:153038)的近复结构 $J$ 是可积的（即 $N_J=0$），它就被称为**厄米[流形](@entry_id:153038) (Hermitian manifold)**。在厄米[流形](@entry_id:153038)中，最重要的一类是**[凯勒流形](@entry_id:161192) (Kähler manifold)**。一个[凯勒流形](@entry_id:161192)是一个厄米[流形](@entry_id:153038)，其[基本2-形式](@entry_id:183276) $\omega$ 是闭的，即 $d\omega = 0$。

[凯勒条件](@entry_id:637291) $d\omega = 0$ 是一个非常强的条件，它有许多等价的刻画。其中最重要的一条是：一个厄米[流形](@entry_id:153038)是[凯勒流形](@entry_id:161192)，当且仅当其[黎曼度量](@entry_id:754359) $g$ 的Levi-Civita联络 $\nabla$ 与 $J$ 可交换，即 $\nabla J = 0$ [@problem_id:2979132]。这意味着 $\nabla$ 在平行移动向量时保持了复结构。这也进一步意味着 $\nabla$ 保持了 $(p,q)$-分解，即将 $(p,q)$-型张量场沿任意方向的协变导数仍然是 $(p,q)$-型的。

[凯勒几何](@entry_id:160314)的优美之处在于它融合了[黎曼几何](@entry_id:160508)、[复几何](@entry_id:159080)和[辛几何](@entry_id:160783)。例如，在[凯勒流形](@entry_id:161192)上，[Hodge拉普拉斯算子](@entry_id:183923)之间存在着深刻的关系 $\Delta_d = 2\Delta_{\partial} = 2\Delta_{\bar{\partial}}$ [@problem_id:3034880]，这极大地简化了[Hodge理论](@entry_id:161814)的研究。

### 概览：Gray-Hervella分类

最后，我们介绍一个统一的框架，用于系统地理解从一般的几乎厄米结构到特殊的凯勒结构之间的各种可能性。这就是**Gray-Hervella分类**。

这个分类的出发点是**內蕴挠率 (intrinsic torsion)** $\nabla J$。在一个几乎厄米[流形](@entry_id:153038)上，$\nabla J$ 衡量了Levi-Civita联络保持复结构的失败程度。[凯勒流形](@entry_id:161192)的定义就是 $\nabla J=0$。对于非凯勒流形，$\nabla J$ 是一个非零的[张量场](@entry_id:190170)。

Gray和Hervella发现，所有可能的內蕴挠率构成的空间，在[酉群](@entry_id:138602) $U(n)$ 的表示下，可以不可约地分解为四个[子空间](@entry_id:150286)的总和：
$$
\mathcal{T} \cong W_1 \oplus W_2 \oplus W_3 \oplus W_4
$$
一个几乎厄米[流形](@entry_id:153038)属于16个Gray-Hervella类别中的某一类，取决于它的[挠率张量](@entry_id:204137) $\nabla J$ 落在哪个[子空间](@entry_id:150286)或[子空间之和](@entry_id:180324)中。这四个[基本类](@entry_id:158335)别各自对应着重要的几何性质 [@problem_id:2968591]：
*   **$W_1 \oplus W_2$**: 对应于**非可积** ($N_J \neq 0$) 的结构。
*   **$W_3 \oplus W_4$**: 对应于**可积**（即厄米，$N_J = 0$）的结构。

这四个基本类别可以更精细地描述：
*   **$W_1$ (近凯勒类, Nearly Kähler):** 挠率满足 $(\nabla_X J)X = 0$。其 $d\omega$ 是一个非零的 $(3,0)+(0,3)$-型3-形式。
*   **$W_2$ (近乎凯勒类, Almost Kähler):** 挠率的特点是 $d\omega=0$，但结构不可积 ($N_J \neq 0$)。
*   **$W_4$ (局部共形凯勒类, Locally Conformally Kähler):** 挠率由一个1-形式（Lee形式 $\theta$）完全决定，使得 $d\omega = \theta \wedge \omega$。这是可积的一类。
*   **$W_3$ (平衡厄米类, Balanced Hermitian):** 对应于 $N_J=0$ 且Lee形式 $\theta=0$ 的结构。其 $d\omega$ 是一个非零的、原始的 $(2,1)+(1,2)$-型3-形式。

在这个框架下，**凯勒流形**是挠率完全消失的[流形](@entry_id:153038)，即其挠率在所有四个[子空间](@entry_id:150286)中的分量都为零。Gray-Hervella分类为我们提供了一张精细的地图，清晰地标示了从最一般的几乎厄米结构到高度对称的凯勒结构之间的所有路径和中间站，完美地总结了本章探讨的各种原理和机制。