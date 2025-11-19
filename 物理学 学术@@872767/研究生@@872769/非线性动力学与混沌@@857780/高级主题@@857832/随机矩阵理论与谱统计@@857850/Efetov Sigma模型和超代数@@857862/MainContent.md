## 引言
叶费托夫西格玛模型（Efetov Sigma Model）是现代[凝聚态理论](@entry_id:141958)物理中一个极其强大且优雅的工具，专门用于解决包含无序的量子系统问题。在诸如介观金属、量子点和[拓扑材料](@entry_id:142123)等复杂系统中，直接求解包含随机杂质势的薛定谔方程几乎是不可能的。该模型的核心思想是绕过对系统微观细节的精确求解，通过对所有可能的无序构型进行平均，直接提取出那些不依赖于特定杂质排布的普适物理性质，如平均[电导](@entry_id:177131)、态[密度[关](@entry_id:157860)联和](@entry_id:269099)[量子干涉](@entry_id:139127)效应。它巧妙地解决了计算[无序平均](@entry_id:183213)[格林函数](@entry_id:147802)时遇到的分母问题，为探索无序世界的物理规律开辟了一条全新的道路。

本文旨在为读者提供一个关于叶费托夫西格玛模型的系统性介绍。我们将从其数学基础出发，逐步揭示其物理内涵和强大应用。在“原理与机制”一章中，我们将介绍超代数这一核心数学语言，并展示如何通过[无序平均](@entry_id:183213)和哈伯德-斯特拉托诺维奇变换，从一个微观[哈密顿量](@entry_id:172864)严格地推导出描述低能集体自由度的[非线性西格玛模型](@entry_id:190355)。随后，在“应用与跨学科连接”一章中，我们将把这一理论框架应用于多个前沿领域，包括[随机矩阵理论](@entry_id:142253)、介观[量子输运](@entry_id:138932)、电子相互作用效应以及拓扑材料，展示其如何解释[弱局域化](@entry_id:146052)、[普适电导涨落](@entry_id:139635)等关键物理现象。最后，在“动手实践”部分，我们提供了一系列练习，帮助读者巩固对超代数和模型构建的理解。通过这三部分的学习，读者将能够掌握叶费托夫西格玛模型的基本原理，并体会其作为连接微观世界与宏观普适性的桥梁所具有的深刻魅力。

## 原理与机制

本章旨在阐述支撑叶费托夫西格玛模型（Efetov Sigma Model）的核心原理与数学机制。我们将从超代数（superalgebra）的基本构件——格拉斯曼代数（Grassmann algebra）和超矩阵（supermatrix）——出发，逐步构建起一个功能强大的[场论](@entry_id:155241)框架。随后，我们将展示该框架如何从一个微观的无序[哈密顿量](@entry_id:172864)出发，通过[无序平均](@entry_id:183213)和哈伯德-斯特拉托诺维奇变换（Hubbard-Stratonovich transformation），自然地导出[非线性西格玛模型](@entry_id:190355)。最后，我们将探讨该模型的[鞍点](@entry_id:142576)[流形](@entry_id:153038)结构及其低能涨落，这些涨落描述了如[弱局域化](@entry_id:146052)等关键的物理输运现象。

### 代[数基](@entry_id:634389)础：超数与超矩阵

超对称方法的核心是一种将交换变量（[玻色子](@entry_id:138266)）和反交换变量（[费米子](@entry_id:146235)）统一处理的数学语言。这一语言的基础是超代数，它为描述[无序系统](@entry_id:145417)中的物理可观测量提供了精确的工具。

#### 格拉斯曼代数与[别列津积分](@entry_id:192484)

物理系统的[配分函数](@entry_id:193625)通常通过[泛函积分](@entry_id:268544)进行计算。对于包含[费米子](@entry_id:146235)的系统，积分变量不再是普通的复数或实数，而是所谓的**[格拉斯曼数](@entry_id:136855)（Grassmann numbers）**。这是一组满足[反交换关系](@entry_id:153815)的抽象数学对象。对于一对共轭的[格拉斯曼变量](@entry_id:199573) $\psi$ 和 $\bar{\psi}$，它们遵循以下代数规则：
$$
\psi^2 = 0, \quad \bar{\psi}^2 = 0, \quad \psi\bar{\psi} + \bar{\psi}\psi = 0
$$
这些规则的一个直接推论是，任何关于这些变量的函数 $f(\bar{\psi}, \psi)$ 必定是一个有限的多项式。例如，对于单对变量，函数最多是线性的：$f(\bar{\psi}, \psi) = c_0 + c_1\psi + c_2\bar{\psi} + c_3\bar{\psi}\psi$。

对[格拉斯曼变量](@entry_id:199573)的积分，即**[别列津积分](@entry_id:192484)（Berezin integration）**，由一套独特的规则定义，其本质上是一种[微分](@entry_id:158718)运算。基本规则为：
$$
\int d\psi = 0, \quad \int d\psi \, \psi = 1
$$
对于[多变量积分](@entry_id:139873)，我们采用迭代方式，并规[定积分](@entry_id:147612)测度 $d\bar{\psi} d\psi$ 的次序使得 $\int d\bar{\psi} d\psi \, (\psi \bar{\psi}) = 1$。注意到 $\psi\bar{\psi} = -\bar{\psi}\psi$，这意味着 $\int d\bar{\psi} d\psi \, (\bar{\psi}\psi) = -1$。

为了理解这些规则的实际应用，我们可以考虑一个仅包含单个[费米子](@entry_id:146235)能级的玩具模型。其作用量为 $S[\bar{\psi}, \psi] = a \bar{\psi} \psi$，其中 $a$ 是一个复数。[配分函数](@entry_id:193625) $Z$ 由高斯型[别列津积分](@entry_id:192484)给出。由于 $\bar{\psi}\psi$ 的平方为零（$(\bar{\psi}\psi)^2 = \bar{\psi}\psi\bar{\psi}\psi = -\bar{\psi}\bar{\psi}\psi\psi = 0$），[指数函数](@entry_id:161417)的[泰勒展开](@entry_id:145057)会截断：
$$
e^{-S} = e^{-a \bar{\psi} \psi} = 1 - a \bar{\psi} \psi
$$
利用[别列津积分](@entry_id:192484)规则，[配分函数](@entry_id:193625)的计算如下 [@problem_id:867467]：
$$
Z = \int d\bar{\psi} d\psi \, (1 - a \bar{\psi} \psi) = \int d\bar{\psi} d\psi \cdot 1 - a \int d\bar{\psi} d\psi \, (\bar{\psi} \psi) = 0 - a(-1) = a
$$
这个结果揭示了一个普遍的规律：对[费米子](@entry_id:146235)场进行[高斯积分](@entry_id:187139)得到的结果是作用量中二次项系数矩阵的**[行列式](@entry_id:142978)（determinant）**。在此例中，矩阵是一个 $1 \times 1$ 矩阵 $(a)$，其[行列式](@entry_id:142978)就是 $a$。

物理可观测量，如[格林函数](@entry_id:147802)，可以通过计算关联函数得到。例如，两点关联函数 $G = \langle \psi \bar{\psi} \rangle$ 的计算方式如下 [@problem_id:867467]：
$$
G = \frac{1}{Z} \int d\bar{\psi} d\psi \, (\psi \bar{\psi}) \, e^{-a \bar{\psi} \psi} = \frac{1}{a} \int d\bar{\psi} d\psi \, (\psi \bar{\psi}) (1 - a \bar{\psi} \psi)
$$
展开括号内的表达式，我们得到 $\psi \bar{\psi} - a \psi \bar{\psi} \bar{\psi} \psi$。由于 $\bar{\psi}^2=0$，第二项为零。因此：
$$
G = \frac{1}{a} \int d\bar{\psi} d\psi \, (\psi \bar{\psi}) = \frac{1}{a} \cdot 1 = \frac{1}{a}
$$
这恰好是作用量矩阵 $a$ 的逆。

这个结论可以推广到多变量情况。对于一组格拉斯曼场 $\psi = (\psi_1, ..., \psi_N)^T$ 和 $\bar{\psi} = (\bar{\psi}_1, ..., \bar{\psi}_N)^T$，以及一个可逆的 $N \times N$ 矩阵 $M$，普遍的高斯[别列津积分](@entry_id:192484)公式为：
$$
\int d\bar{\psi} d\psi \, \exp(-\bar{\psi}^T M \psi) = \det(M)
$$
其中 $d\bar{\psi} d\psi \equiv d\bar{\psi}_N ... d\bar{\psi}_1 d\psi_N ... d\psi_1$。包含源项的[生成泛函](@entry_id:152688)则为：
$$
Z[\bar{\eta}, \eta] = \int d\bar{\psi} d\psi \, \exp(-\bar{\psi}^T M \psi + \bar{\eta}^T \psi + \bar{\psi}^T \eta) = \det(M) \exp(\bar{\eta}^T M^{-1} \eta)
$$
其中 $\eta$ 和 $\bar{\eta}$ 是格拉斯曼源场。这个公式是计算任意关联函数的基础。通过对源场求导，我们可以得到任意 n 点关联函数。例如，两点关联函数为 $\langle \psi_i \bar{\psi}_j \rangle = (M^{-1})_{ji}$。对于高阶关联函数，可以使用**[威克定理](@entry_id:137086)（Wick's theorem）**将其分解为两点函数的乘积。例如，四点关联函数可以表示为 [@problem_id:867395]：
$$
\langle \psi_i \bar{\psi}_j \psi_k \bar{\psi}_l \rangle = \langle \psi_i \bar{\psi}_j \rangle \langle \psi_k \bar{\psi}_l \rangle - \langle \psi_i \bar{\psi}_l \rangle \langle \psi_k \bar{\psi}_j \rangle = (M^{-1})_{ji}(M^{-1})_{lk} - (M^{-1})_{li}(M^{-1})_{jk}
$$
这个表达式的形式是一个[行列式](@entry_id:142978)，这正是[费米子统计](@entry_id:148436)中[泡利不相容原理](@entry_id:141850)的体现。

#### [李超代数](@entry_id:187567)与超矩阵

将玻色场和费米场置于同一理论框架中的自然语言是**[李超代数](@entry_id:187567)（Lie superalgebra）**。一个[李超代数](@entry_id:187567) $\mathfrak{g}$ 是一个 $\mathbb{Z}_2$-分次[向量空间](@entry_id:151108)，即它可以分解为一个偶[子空间](@entry_id:150286) $\mathfrak{g}_0$（玻色部分）和一个奇[子空间](@entry_id:150286) $\mathfrak{g}_1$（费米部分）的直和：$\mathfrak{g} = \mathfrak{g}_0 \oplus \mathfrak{g}_1$。

在 Efetov 的方法中，最常遇到的[李超代数](@entry_id:187567)是 $\mathfrak{gl}(m|n)$，它可以表示为 $(m+n) \times (m+n)$ 的**超矩阵（supermatrices）**。一个超矩阵 $X$ 具有分块形式：
$$
X = \begin{pmatrix} A  B \\ C  D \end{pmatrix}
$$
其中 $A$ 是 $m \times m$ 矩阵，$D$ 是 $n \times n$ 矩阵，它们的[矩阵元](@entry_id:186505)是交换的（偶性，玻色型）。而 $B$ ($m \times n$) 和 $C$ ($n \times m$) 的矩阵元是[反交换的](@entry_id:262442)（奇性，费米型）。

对于超矩阵，一个至关重要的操作是**[超迹](@entry_id:183947)（supertrace）**，其定义为：
$$
\text{STr}(X) = \text{Tr}(A) - \text{Tr}(D)
$$
注意[费米子](@entry_id:146235)块 $D$ 的迹前面有一个关键的负号。这个负号确保了[超迹](@entry_id:183947)具有循环[不变性](@entry_id:140168)，即 $\text{STr}(XY) = \text{STr}(YX)$。我们可以通过一个 $\mathfrak{gl}(1|1)$ 的例子来验证这个性质。考虑两个一般的 $\mathfrak{gl}(1|1)$ 超矩阵 [@problem_id:867399]：
$$
X = \begin{pmatrix} a  \alpha \\ \beta  b \end{pmatrix}, \quad Y = \begin{pmatrix} c  \gamma \\ \delta  d \end{pmatrix}
$$
其中 $a, b, c, d$ 是偶性元素，$\alpha, \beta, \gamma, \delta$ 是奇性元素。它们乘积的[超迹](@entry_id:183947)为 $\text{STr}(XY) = (ac + \alpha\delta) - (\beta\gamma + bd)$ 和 $\text{STr}(YX) = (ca + \gamma\beta) - (\delta\alpha + db)$。两者之差为：
$$
\text{STr}(XY) - \text{STr}(YX) = (ac + \alpha\delta - \beta\gamma - bd) - (ca + \gamma\beta - \delta\alpha - db)
$$
利用代数规则（偶元互换通勤，奇偶元通勤，奇元互换反通勤：$ac=ca, bd=db, \alpha\delta = -\delta\alpha, \gamma\beta = -\beta\gamma$），上式变为：
$$
= \alpha\delta - \beta\gamma - \gamma\beta + \delta\alpha = \alpha\delta - \beta\gamma - (-\beta\gamma) + (-\alpha\delta) = \alpha\delta - \beta\gamma + \beta\gamma - \alpha\delta = 0
$$
因此，$\text{STr}([X,Y]) = \text{STr}(XY) - \text{STr}(YX) = 0$。这个循环属性是西格玛模型拉格朗日量具有良好对称性的保证。

[李超代数](@entry_id:187567)的结构由**[分次李括号](@entry_id:181952)（graded Lie bracket）**或**[超交换](@entry_id:142159)子（supercommutator）**定义：
$$
[X, Y] = XY - (-1)^{p(X)p(Y)} YX
$$
其中 $p(X)$ 是元素 $X$ 的奇偶性（偶为0，奇为1）。如果 $X, Y$ 中至少有一个是偶元素，它就退化为普通交换子 $[X,Y] = XY-YX$。如果两者都是奇元素，它就变成[反交换](@entry_id:186708)子 $\{X,Y\} = XY+YX$。

这个[代数结构](@entry_id:137052)由**[结构常数](@entry_id:157960)（structure constants）** $f_{AB}{}^C$ 刻画，它们定义了[基矢](@entry_id:199546) $T_A$ 之间的括号关系：$[T_A, T_B] = \sum_C f_{AB}{}^C T_C$。例如，计算两个奇性[基矢](@entry_id:199546)的超交换子可以得到一个偶性元素，从而确定相关的[结构常数](@entry_id:157960) [@problem_id:867445]。同时，这些括号运算必须满足**分次[雅可比恒等式](@entry_id:140480)（graded Jacobi identity）** [@problem_id:867394]，这是[李超代数](@entry_id:187567)的[自洽性](@entry_id:160889)要求。

### 叶费托夫西格玛模型：从无序到[场论](@entry_id:155241)

有了超代数的工具，我们现在可以构建描述无序电子系统的有效场论。其核心思想是对系统的格林函数（或其[生成泛函](@entry_id:152688)）在所有可能的无序构型上进行平均。

#### [无序平均](@entry_id:183213)与相互作用的出现

考虑一个由 $N \times N$ 随机[哈密顿量](@entry_id:172864) $H$ 描述的系统，其[矩阵元](@entry_id:186505)取自某个[概率分布](@entry_id:146404)，例如[高斯幺正系综 (GUE)](@entry_id:188014)，$P(H) \propto \exp(-\frac{N}{v^2} \text{Tr}(H^2))$。我们感兴趣的是诸如[态密度](@entry_id:147894)之类的平均物理量。这些量可以从平均后的[生成泛函](@entry_id:152688) $\langle Z \rangle_H$ 中得到。

在[超对称](@entry_id:155777)方法中，[生成泛函](@entry_id:152688)被表示为一个对超向量场 $\Psi_k = (\phi_k, \chi_k)^T$ 的[泛函积分](@entry_id:268544)，其中 $\phi_k$ 是复玻色场，$\chi_k$ 是[复格](@entry_id:170186)拉斯曼场。对[哈密顿量](@entry_id:172864) $H$ 进行高斯积分（即[无序平均](@entry_id:183213)）后，一个关键的现象发生了：原本在 $\Psi_k$ 场中是无相互作用的理论，现在出现了一个四场相互作用项。这个过程将不同的能级 $k$ 耦合在一起。平均后的[有效作用量](@entry_id:145780)形式如下 [@problem_id:867480]：
$$
S_{\text{eff}}[\bar{\Psi}, \Psi] \propto \sum_{k=1}^{N} \bar{\Psi}_k (E - H_0) \Psi_k + \frac{v^2}{N} \text{STr}\left( \left(\sum_{k=1}^N \Psi_k \bar{\Psi}_k\right)^2 \right)
$$
我们定义一个 $2 \times 2$ 的超矩阵 $Q = \sum_{k=1}^N \Psi_k \bar{\Psi}_k$。这个 $Q$ 矩阵混合了所有能级的信息。[无序平均](@entry_id:183213)产生的相互作用项就是 $\frac{v^2}{N} \text{STr}(Q^2)$。这个四次项使得理论难以精确求解。

#### 哈伯德-斯特拉托诺维奇变换

为了处理这个四次项，我们采用**哈伯德-斯特拉托诺维奇（Hubbard-Stratonovich, HS）变换**。这是一种标准的[场论](@entry_id:155241)技巧，通过引入一个辅助场来将四次项线性化。对于超矩阵的标量表达式 $\text{STr}(Q^2)$，我们可以引入一个辅助的 $2 \times 2$ 超矩阵场 $\mathcal{R}$ 来解耦该项。HS 变换的恒等式大致为：
$$
\exp\left(-\frac{v^2}{N} \text{STr}(Q^2)\right) \propto \int \mathcal{D}\mathcal{R} \, \exp\left(-\frac{N}{4v^2} \text{STr}(\mathcal{R}^2) + i \, \text{STr}(\mathcal{R}Q)\right)
$$
通过这个变换，关于 $\Psi$ 的作用量现在变成了线性的（通过 $\text{STr}(\mathcal{R}Q) = \sum_k \bar{\Psi}_k \mathcal{R} \Psi_k$）。这使得我们可以先对原始的 $\Psi$ 场进行积分。对 $\Psi$ 积分后，会得到一个关于 $\mathcal{R}$ 的[行列式](@entry_id:142978)，最终得到一个只依赖于[辅助场](@entry_id:155519) $\mathcal{R}$ 的[有效作用量](@entry_id:145780) $S[\mathcal{R}]$。这个新的场 $\mathcal{R}$ (或与其密切相关的场 $Q$) 就是**[非线性西格玛模型](@entry_id:190355)（nonlinear sigma model）**的基本场。这个过程的代价是，我们从一个对“快”变量 $\Psi$ 的简单积分，转换为了一个对“慢”的集体场 $\mathcal{R}$ 的复杂积分。这个新作用量的系数中包含了与 $\text{STr}(\mathcal{R}^2)$ 成正比的项，其系数为 $-\frac{N}{4v^2}$ [@problem_id:867480]，它将决定新[场论](@entry_id:155241)中涨落的“硬度”。

### 西格玛模型的结构与动力学

通过 HS 变换得到的[有效理论](@entry_id:155490) $S[Q]$ 是一个关于超矩阵场 $Q$ 的[场论](@entry_id:155241)。这个理论的普适性质由其对称性和低能激发谱决定。

#### [鞍点](@entry_id:142576)[流形](@entry_id:153038)

$Q$ 场的[有效作用量](@entry_id:145780)通常不是在单一的 $Q$ 值处取极值，而是在一个由满足特定约束条件的矩阵构成的连续[流形](@entry_id:153038)上取[极值](@entry_id:145933)。这个[流形](@entry_id:153038)被称为**[鞍点](@entry_id:142576)[流形](@entry_id:153038)（saddle-point manifold）**。在许多重要的物理情况下，这个约束条件是 $Q^2 = \mathbb{I}$，其中 $\mathbb{I}$ 是单位超矩阵。

这个[流形](@entry_id:153038)通常具有**[对称空间](@entry_id:181790)（symmetric space）**的结构，可以表示为一个李群 $G$ 与其[子群](@entry_id:146164) $H$ 的**[陪集空间](@entry_id:180459)（coset space）** $G/H$。这里的对称性破缺 $G \to H$ 是理解系统低能物理的关键。[流形](@entry_id:153038)的维度对应于破缺的生成元数量，这些生成[元激发](@entry_id:140859)出的[无质量模式](@entry_id:152801)被称为**[戈德斯通模](@entry_id:141982)式（Goldstone modes）**。

例如，在 replica formalism 中，对于[正交对](@entry_id:164779)称性（D类），[鞍点](@entry_id:142576)[流形](@entry_id:153038)是 $O(2N)/U(N)$，其中 $N$ 是副本数。此[流形](@entry_id:153038)的维度可以通过计算群的维度差得到 [@problem_id:867452]：
$$
\dim(O(2N)) = \frac{2N(2N-1)}{2} = 2N^2 - N
$$
$$
\dim(U(N)) = N^2
$$
因此，[戈德斯通模](@entry_id:141982)式的数量为 $\dim(M) = \dim(G) - \dim(H) = (2N^2 - N) - N^2 = N^2 - N = N(N-1)$。这些模式构成了系统的低能自由度。

[鞍点](@entry_id:142576)[流形](@entry_id:153038)上的一个点 $Q$ 可以通过对称群的元素[参数化](@entry_id:272587)。例如，对于幺正对称性（A类），$Q$ 可以表示为 $Q = U\Lambda U^{-1}$，其中 $\Lambda$ 是一个固定的对角超矩阵（如 $\text{diag}(1,-1)$），而 $U$ 是[对称群](@entry_id:146083) $G$（如 $U(1,1)$）中的元素。这种构造自动满足了 $Q^2 = \mathbb{I}$ 的约束，因为 $Q^2 = U\Lambda U^{-1} U\Lambda U^{-1} = U\Lambda^2 U^{-1} = U\mathbb{I}U^{-1} = \mathbb{I}$ [@problem_id:867460]。

#### 低能涨落：[扩散](@entry_id:141445)子与合作子

系统的普适输运性质由[鞍点](@entry_id:142576)[流形](@entry_id:153038)上的低能、长波长的涨落（[戈德斯通模](@entry_id:141982)式）决定。这些涨落对应于 $Q(\mathbf{r})$ 场的缓慢空间和时间变化。描述这些慢模式的[有效作用量](@entry_id:145780)通常可以展开为梯度的[幂级数](@entry_id:146836)。对于金属系统，[主导项](@entry_id:167418)是梯度的平方：
$$
S[Q] = \frac{\pi \nu}{8} \int d^d\mathbf{r} \, \text{STr} \left[ D (\nabla Q)^2 - 2i(\omega + i\delta) \Lambda Q \right]
$$
这里的 $D$ 是[扩散](@entry_id:141445)常数，$\nu$ 是[费米能级的态密度](@entry_id:161911)，$\omega$ 是频率。第一项是“动能项”，它抑制了场 $Q$ 的剧烈空间变化。第二项是“质量项”，它来自[格林函数](@entry_id:147802)中的能量和频率依赖，它会给涨落一个有效质量，抑制大的涨落。

为了研究这些涨落的传播，我们将 $Q$ 在其[鞍点](@entry_id:142576)值 $Q_0 = \Lambda$ 附近展开。这些涨落模式可以被分为不同的类型，其中最重要的是**[扩散](@entry_id:141445)子（diffusons）**和**合作子（cooperons）**。它们分别对应于粒子-空穴和粒子-粒子通道的[扩散](@entry_id:141445)传播。

以[扩散](@entry_id:141445)子为例，其动力学由 $Q$ 矩阵在“延迟-超前”（Retarded-Advanced）空间中的非对角块描述。将上述作用量对这些涨落场（记为 $W$）展开到二次，可以得到一个描述自由传播模式的二次型作用量。例如，在傅里叶空间中，[扩散](@entry_id:141445)子模式的二次作用量形式为 [@problem_id:867482]：
$$
S^{(2)} \propto \sum_{\mathbf{q}} \text{STr} \left[ (D\mathbf{q}^2 - i\omega) W_{ra}(-\mathbf{q}) W_{ar}(\mathbf{q}) \right]
$$
这个二次作用量允许我们直接读出涨落场的传播子，即它们的二点关联函数。对于[扩散](@entry_id:141445)子的玻色部分，其[传播子](@entry_id:139558)（**[扩散](@entry_id:141445)子[传播子](@entry_id:139558)**）为：
$$
P_D(\mathbf{q}, \omega) = \langle w_{ar}(\mathbf{q}) w_{ra}(-\mathbf{q}) \rangle \propto \frac{1}{D\mathbf{q}^2 - i\omega}
$$
这个传播子是整个无序[输运理论](@entry_id:143989)的基石。它的极点 $\omega = -iD\mathbf{q}^2$ 描述了[电子密度涨落](@entry_id:748910)的[扩散](@entry_id:141445)行为。量子干涉效应，如[弱局域化](@entry_id:146052)，可以通过计算这些模式的[圈图修正](@entry_id:150150)来得到。

#### 非平衡扩展：凯尔迪什形式

西格玛模型框架的强大之处在于它还可以推广到非平衡系统，这通常通过**凯尔迪什（Keldysh）形式**实现。在这种方法中，$Q$ 矩阵的维度加倍，以包含描述系统动力学和统计分布的信息。

在非平衡态下，一个核心问题是**涨落-耗散定理（Fluctuation-Dissipation Theorem, FDT）**的命运。FDT 是平衡态统计物理的标志，它将系统的线性响应（耗散）与系统在平衡态的涨落关联起来。在凯尔迪什西格玛模型中，FDT 的成立与否有一个清晰的代数判据：当且仅当[鞍点](@entry_id:142576)矩阵 $Q$ 与代表[平衡分布](@entry_id:263943)的矩阵 $\Lambda_{eq}$ 对易时，FDT 成立。

考虑一个两端连接着不同化学势 $\mu_L \neq \mu_R$ 的量子点。这是一个典型的非平衡系统。我们可以计算其[鞍点](@entry_id:142576)矩阵 $Q$ 和对应于某个参考[平衡态](@entry_id:168134)的矩阵 $\Lambda_{eq}$ 之间的[交换子](@entry_id:158878) $[Q, \Lambda_{eq}]$。直接的计算表明，当存在偏压时（$\mu_L \neq \mu_R$），这个交换子不为零 [@problem_id:867428]。其非零的 $(1,2)$ [矩阵元](@entry_id:186505)直接量化了系统偏离平衡的程度，以及 FDT 被破坏的程度。这清晰地展示了西格玛模型不仅能描述平衡态的普适性质，还能精确刻画非平衡系统中的[量子输运](@entry_id:138932)和统计物理。