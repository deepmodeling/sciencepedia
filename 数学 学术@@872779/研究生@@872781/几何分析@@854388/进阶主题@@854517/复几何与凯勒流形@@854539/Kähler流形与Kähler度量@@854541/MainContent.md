## 引言
在现代微分几何的宏伟版图中，凯勒流形占据着一个核心且光辉的位置。它不仅是[黎曼几何](@entry_id:160508)、[复几何](@entry_id:159080)与[辛几何](@entry_id:160783)三大领域的完美交汇点，更是连接[代数几何](@entry_id:156300)、拓扑学乃至理论物理的坚实桥梁。凯勒流形的优美结构与刚性特征，使其成为研究几何、拓扑与分析之间深层联系的理想舞台。其核心魅力在于，一个看似简单的附加条件——凯勒形式的闭合性——便能衍生出极其丰富和深刻的几何与拓扑性质。

本文旨在系统性地探索凯勒流形的理论世界。我们将着手解决的核心问题是：凯勒结构是如何将不同几何分支的语言统一起来的？它如何简化几何分析中的计算，并引出寻找“典范”度量的现代理论？这些[典范度量](@entry_id:266957)又如何在其他数学领域和物理学中产生深远影响？

为回答这些问题，本文将分为三个章节。在“原理与机制”中，我们将从[复结构](@entry_id:269128)的基础出发，详细阐述[凯勒流形](@entry_id:161192)的定义、多种等价刻画及其对曲率和拓扑的直接影响，并介绍里程碑式的[卡拉比猜想](@entry_id:180885)。随后，在“应用与跨学科联系”一章，我们将通过具体的范例，如[复射影空间](@entry_id:268402)和 Calabi-Yau [流形](@entry_id:153038)，展示[凯勒几何](@entry_id:160314)如何在代数几何、[稳定性理论](@entry_id:149957)和[弦理论](@entry_id:145688)等领域中发挥关键作用。最后，“实践练习”部分将提供一系列计算问题，帮助读者巩固理论知识，将抽象概念转化为具体的分析能力。通过这段旅程，您将深入理解[凯勒几何](@entry_id:160314)的内在和谐及其作为现代数学中心支柱之一的重要地位。

## 原理与机制

在本章中，我们将深入探讨凯勒流形的核心几何原理。我们将从复结构的基本概念出发，逐步引入度量，并最终阐明定义凯勒流形的多个等价条件。这些条件揭示了[黎曼几何](@entry_id:160508)、[复几何](@entry_id:159080)与[辛几何](@entry_id:160783)之间深刻的内在联系。此外，我们将探讨[凯勒几何](@entry_id:160314)如何简化曲率的计算，并引出寻找“典范”度量的现代理论，即[卡拉比猜想](@entry_id:180885)及其解。最后，我们将展示凯勒结构如何对[流形的拓扑](@entry_id:267834)施加强大的约束。

### 从殆[复流形](@entry_id:159076)到复流形

[几何分析](@entry_id:157700)中的许多研究对象都具有复结构。一个光滑实[流形](@entry_id:153038) $M$（维度为 $2n$）上的**[殆复结构](@entry_id:159849) (almost complex structure)** 是一个光滑的张量场 $J$，它在每个切空间 $T_pM$ 上都表现为一个[线性映射](@entry_id:185132) $J_p: T_pM \to T_pM$，且满足 $J^2 = -\mathrm{Id}$，其中 $\mathrm{Id}$ 是[恒等映射](@entry_id:634191)。

这个简单的代数条件 $J^2 = -\mathrm{Id}$ 具有深远的意义。它允许我们将切丛 $TM$ [复化](@entry_id:260775)，得到 $T_{\mathbb{C}}M = TM \otimes_{\mathbb{R}} \mathbb{C}$。$J$ 的作用可以线性延拓到 $T_{\mathbb{C}}M$ 上，其[特征值](@entry_id:154894)必然为 $\mathrm{i}$ 和 $-\mathrm{i}$。这导致了[切丛](@entry_id:161294)的一个基本分解：
$$
T_{\mathbb{C}}M = T^{1,0}M \oplus T^{0,1}M
$$
其中 $T^{1,0}M$ 是对应于[特征值](@entry_id:154894) $\mathrm{i}$ 的特征子丛，其[截面](@entry_id:154995)称为 **(1,0) 型向量场**；$T^{0,1}M$ 则是对应于[特征值](@entry_id:154894) $-\mathrm{i}$ 的特征子丛，其[截面](@entry_id:154995)称为 **(0,1) 型向量场**。对偶地，[复化](@entry_id:260775)的[余切丛](@entry_id:185138)也分解为 $\Lambda^{1,0}M \oplus \Lambda^{0,1}M$，其[截面](@entry_id:154995)分别为 **(1,0) 型**和 **(0,1) 型**[微分形式](@entry_id:146747)。由此，任意 $k$-次微分形式的空间 $\Lambda^k(M)$ 也相应地分解为 $(p,q)$ 型形式的空间 $\Lambda^{p,q}(M)$，其中 $p+q=k$ [@problem_id:3031491]。

例如，在标准空间 $\mathbb{C}^n$ 上，我们有实坐标 $(x^1, y^1, \dots, x^n, y^n)$ 和复坐标 $z^k = x^k + \mathrm{i}y^k$。标准[复结构](@entry_id:269128) $J_0$ 的作用是 $J_0(\frac{\partial}{\partial x^k}) = \frac{\partial}{\partial y^k}$ 和 $J_0(\frac{\partial}{\partial y^k}) = -\frac{\partial}{\partial x^k}$。在这种情况下，(1,0) 型向量场由 $\frac{\partial}{\partial z^k} = \frac{1}{2}(\frac{\partial}{\partial x^k} - \mathrm{i}\frac{\partial}{\partial y^k})$ 张成，而 (1,0) 型 1-形式则由 $dz^k = dx^k + \mathrm{i}dy^k$ 张成 [@problem_id:3031491]。

然而，并非所有[殆复结构](@entry_id:159849)都等同于我们所熟知的复分析中的复结构。一个[殆复结构](@entry_id:159849)被称为**可积的 (integrable)**，如果[流形](@entry_id:153038) $M$ 局部上可以找到一组**全纯坐标 (holomorphic coordinates)** $(z^1, \dots, z^n)$，使得 $J$ 在这些坐标下就是标准[复结构](@entry_id:269128)。一个装配了可积[殆复结构](@entry_id:159849)的[流形](@entry_id:153038)被称为**[复流形](@entry_id:159076) (complex manifold)**。

[可积性](@entry_id:142415)的几何障碍由**[奈恩黑斯张量](@entry_id:159184) (Nijenhuis tensor)** $N_J$ 给出，其定义为：
$$
N_J(X,Y) = [JX, JY] - J[JX, Y] - J[X, JY] - [X,Y]
$$
其中 $X, Y$ 是任意向量场，$[ \cdot, \cdot ]$ 是李括号。**[纽兰德-尼伦伯格定理](@entry_id:158862) (Newlander-Nirenberg theorem)** 指出，一个[殆复结构](@entry_id:159849) $J$ 是可积的当且仅当其[奈恩黑斯张量](@entry_id:159184)恒为零，即 $N_J \equiv 0$。对于 $\mathbb{C}^n$ 上的标准[坐标系](@entry_id:156346)，由于坐标[向量场的[李括](@entry_id:193400)号](@entry_id:636461)均为零，我们可以直接验证其[奈恩黑斯张量](@entry_id:159184)为零，这再次确认了 $\mathbb{C}^n$ 是一个[复流形](@entry_id:159076) [@problem_id:3031491]。

### 引入度量：埃尔米特与凯勒结构

为了进行更深入的[几何分析](@entry_id:157700)，我们需要在复流形上引入度量结构。一个在复流形 $(M, J)$ 上的黎曼度量 $g$ 如果与复结构 $J$ **相容 (compatible)**，即满足
$$
g(JX, JY) = g(X,Y)
$$
对所有向量场 $X, Y$ 成立，则称 $g$ 为一个**[埃尔米特度量](@entry_id:202337) (Hermitian metric)**。此时，三元组 $(M, J, g)$ 构成一个**埃尔米特[流形](@entry_id:153038) (Hermitian manifold)**。任何[复流形](@entry_id:159076)上都存在[埃尔米特度量](@entry_id:202337)。

给定一个[埃尔米特度量](@entry_id:202337)，我们可以定义一个与之关联的[2-形式](@entry_id:188008)，称为**[基本2-形式](@entry_id:183276) (fundamental 2-form)** 或**凯勒形式 (Kähler form)**，其定义为：
$$
\omega(X,Y) = g(JX, Y)
$$
通过 $J^2 = -\mathrm{Id}$ 和 $g$ 的对称性及 $J$-[不变性](@entry_id:140168)，可以证明 $\omega$ 是一个实的、反对称的2-形式 [@problem_id:3034906]。此外，由于 $g$ 的非退化性，$\omega$ 也是非退化的。在局部全纯坐标 $\{z^k\}$ 下，$\omega$ 的表达式为
$$
\omega = \frac{\mathrm{i}}{2} \sum_{j,k=1}^n g_{j\bar{k}} dz^j \wedge d\bar{z}^k
$$
其中 $g_{j\bar{k}} = g(\frac{\partial}{\partial z^j}, \frac{\partial}{\partial \bar{z}^k})$。这表明 $\omega$ 是一个实的 **(1,1)-型形式**。

埃尔米特[流形](@entry_id:153038)的世界非常广阔，但其中一类特殊的[流形](@entry_id:153038)——[凯勒流形](@entry_id:161192)——因其优美的性质而成为几何分析的中心舞台。

一个埃尔米特[流形](@entry_id:153038) $(M, J, g)$ 如果其[基本2-形式](@entry_id:183276) $\omega$ 是**闭的 (closed)**，即 $d\omega = 0$，则被称为**[凯勒流形](@entry_id:161192) (Kähler manifold)**，度量 $g$ 称为**凯勒度量 (Kähler metric)** [@problem_id:3034906]。

这个看似简单的附加条件 $d\omega=0$ 融合了黎曼、复和辛三种几何结构。一个[凯勒流形](@entry_id:161192) $(M, J, g)$ 同时是：
1.  一个[黎曼流形](@entry_id:261160) $(M, g)$。
2.  一个复流形 $(M, J)$。
3.  一个[辛流形](@entry_id:161608) $(M, \omega)$，因为 $\omega$ 是一个闭的、非退化的2-形式。

这三种结构通过相容性条件 $g(JX,JY)=g(X,Y)$ 和 $\omega(X,Y)=g(JX,Y)$ 完美地结合在一起。

值得注意的是，并非所有[复流形](@entry_id:159076)都能成为[凯勒流形](@entry_id:161192)。存在一些拓扑障碍。例如，在一个紧致[凯勒流形](@entry_id:161192)上，凯勒形式 $\omega$ 的上同调类 $[\omega] \in H^2(M, \mathbb{R})$ 是非平凡的。因此，如果一个紧致复流形的第二个贝蒂数 $b_2(M) = \dim H^2(M, \mathbb{R})$ 为零，它就不可能承认任何凯勒度量。**霍普夫[流形](@entry_id:153038) (Hopf manifold)** 就是一个典型的例子。对于 $n \ge 2$，它同胚于 $S^{2n-1} \times S^1$，其 $H^2(H, \mathbb{R}) = 0$，因此它虽然是[复流形](@entry_id:159076)且可以拥有[埃尔米特度量](@entry_id:202337)，但绝不可能是凯勒流形 [@problem_id:2988843]。另一个更深刻的拓扑障碍来自[霍奇理论](@entry_id:161814)：在紧致[凯勒流形](@entry_id:161192)上，第一个贝蒂数 $b_1(M)$ 必须是偶数。**小平-瑟斯顿[流形](@entry_id:153038) (Kodaira-Thurston manifold)** 是一个紧致[辛流形](@entry_id:161608)，其 $b_1=3$，因此它不能被赋予凯勒结构 [@problem_id:3031483]。

### [凯勒流形](@entry_id:161192)的等价刻画

[凯勒条件](@entry_id:637291) $d\omega=0$ 有多种等价的表述，它们从不同侧面揭示了[凯勒几何](@entry_id:160314)的内在机制。

#### 几何条件：J 的平行性

凯勒流形最核心的几何特性是复结构 $J$ 与度量 $g$ 的 Levi-Civita 联络 $\nabla$ 的完美协调。一个埃尔米特[流形](@entry_id:153038) $(M, J, g)$ 是凯勒流形，当且仅当
$$
\nabla J = 0
$$
这意味着复结构张量 $J$ 在由度量 $g$ 决定的平行移动下是不变的。这个条件揭示了[凯勒几何](@entry_id:160314)的刚性：度量结构和复结构不是简单地并存，而是通过典范联络紧密地锁在一起 [@problem_id:3034906] [@problem_id:2979176]。

这一等价性的证明依赖于两个基本恒等式。对于任意殆埃尔米特[流形](@entry_id:153038)，我们有：
$$
d\omega(X,Y,Z) = \sum_{\text{cyc}} g((\nabla_X J)Y, Z)
$$
以及[奈恩黑斯张量](@entry_id:159184)与 $\nabla J$ 的关系式。从第一个恒等式立刻可以看出，如果 $\nabla J=0$，那么 $d\omega=0$。反之，若 $d\omega=0$ 且 $N_J=0$（即在[复流形](@entry_id:159076)上），可以证明 $\nabla J$ 必须为零 [@problem_id:2979176]。

#### 坐标条件：[凯勒势](@entry_id:154750)

在局部上，[凯勒条件](@entry_id:637291)极大地简化了度量的描述。一个[埃尔米特度量](@entry_id:202337)是凯勒度量，当且仅当在任意一[点的邻域](@entry_id:144055)内，存在一个实值函数 $\varphi$，称为**[凯勒势](@entry_id:154750) (Kähler potential)**，使得度量张量的分量可以表示为：
$$
g_{j\bar{k}} = \frac{\partial^2 \varphi}{\partial z^j \partial \bar{z}^k}
$$
此时，凯勒形式 $\omega$ 相应地成为 $\omega = \mathrm{i}\partial\bar{\partial}\varphi$。由于外微分算子 $d$ 可以分解为 $d=\partial+\bar{\partial}$，且 $\partial^2 = \bar{\partial}^2 = \partial\bar{\partial}+\bar{\partial}\partial = 0$，我们立即看到 $d\omega = \mathrm{i}(\partial+\bar{\partial})\partial\bar{\partial}\varphi = 0$，自动满足了[凯勒条件](@entry_id:637291)。反之，如果 $d\omega=0$，著名的 $\partial\bar{\partial}$-引理保证了在局部上这样的势函数 $\varphi$ 总是存在的 [@problem_id:2979199]。[凯勒势](@entry_id:154750)的存在性是[凯勒几何](@entry_id:160314)中进行显式计算和构造度量的强大工具。

#### 代数条件：和乐群

[流形](@entry_id:153038)的曲率信息被编码在**和乐群 (holonomy group)** $\mathrm{Hol}(g)$ 中，它由沿闭合环路平行移动[切向量](@entry_id:265494)所产生的[线性变换](@entry_id:149133)构成。对于一个 $2n$ 维黎曼流形，其和乐群一般是 $\mathrm{SO}(2n)$ 的一个[子群](@entry_id:146164)。
[凯勒条件](@entry_id:637291) $\nabla J = 0$ 意味着平行移动与 $J$ 的作用可交换。这等价于说，[和乐群](@entry_id:191471)的元素都保持 $J$ 不变。保持标准黎曼度量和标准[复结构](@entry_id:269128)的[线性变换](@entry_id:149133)群正是[酉群](@entry_id:138602) $\mathrm{U}(n)$。因此，一个埃尔米特[流形](@entry_id:153038)是[凯勒流形](@entry_id:161192)，当且仅当其和乐群被包含在[酉群](@entry_id:138602) $\mathrm{U}(n)$ 中：
$$
\mathrm{Hol}(g) \subset \mathrm{U}(n) \subset \mathrm{SO}(2n)
$$
这个条件将局部的[微分](@entry_id:158718)条件 ($\nabla J = 0$) 与一个全局的、纯代数的性质联系起来 [@problem_id:2979199]。

#### 联络条件：陈联络与Levi-Civita

在埃尔米特[流形](@entry_id:153038)上，除了 Levi-Civita 联络 $\nabla^{\mathrm{LC}}$（其特点是无挠且保度量），还有另一个重要的联络，即**陈联络 (Chern connection)** $\nabla^{\mathrm{Ch}}$。它是唯一满足保度量、保[复结构](@entry_id:269128)（即 $\nabla^{\mathrm{Ch}}g=0, \nabla^{\mathrm{Ch}}J=0$）且其[挠率张量](@entry_id:204137)为 (1,1)-型的联络。
对于一个[凯勒流形](@entry_id:161192)，由于 $\nabla^{\mathrm{LC}}$ 满足 $\nabla^{\mathrm{LC}}g=0$ 和 $\nabla^{\mathrm{LC}}J=0$，且其挠率为零（自然是 (1,1)-型），根据陈联络的唯一性，我们必然有 $\nabla^{\mathrm{LC}} = \nabla^{\mathrm{Ch}}$。反之，如果 $\nabla^{\mathrm{LC}} = \nabla^{\mathrm{Ch}}$，由于后者保 $J$，前者也必须保 $J$，从而[流形](@entry_id:153038)是凯勒的。因此，一个埃尔米特[流形](@entry_id:153038)是凯勒流形，当且仅当其 Levi-Civita 联络与陈联络重合，或者等价地说，其陈联络是[无挠的](@entry_id:161664) [@problem_id:2979199] [@problem_id:2979176]。

### 凯勒流形上的[局部坐标](@entry_id:181200)与曲率

[凯勒条件](@entry_id:637291)的诸多等价形式，尤其是 $\nabla J=0$，极大地简化了曲率的计算。在全纯[坐标系](@entry_id:156346)下，联络的 Christoffel 符号具有简洁的结构。利用 Koszul 公式和[凯勒条件](@entry_id:637291)，我们可以推导出：
$$
\Gamma^k_{ij} = g^{k\bar{m}} \frac{\partial g_{j\bar{m}}}{\partial z^i}, \quad \Gamma^k_{i\bar{j}} = 0
$$
以及它们的共轭。其中 $\Gamma^k_{i\bar{j}}=0$ 和 $\Gamma^{\bar{k}}_{ij}=0$ 的事实尤为重要，它表明 Levi-Civita 联络分别保持了 $T^{1,0}M$ 和 $T^{0,1}M$ 子丛，即[协变微分](@entry_id:263981)不会混合 $(1,0)$ 和 $(0,1)$ 型向量 [@problem_id:3031513]。

对于曲率，最重要的[不变量](@entry_id:148850)之一是**[里奇曲率](@entry_id:162038) (Ricci curvature)**。在凯勒流形上，[里奇曲率](@entry_id:162038)可以被封装在一个实的、闭的 (1,1)-型形式中，称为**[里奇形式](@entry_id:183612) (Ricci form)** $\rho$。其局部表达式与度量[矩阵的行列式](@entry_id:148198)直接相关：
$$
R_{j\bar{k}} = -\frac{\partial^2}{\partial z^j \partial \bar{z}^k} \log(\det(g_{m\bar{n}}))
$$
[里奇形式](@entry_id:183612)则为 $\rho = \mathrm{i} \sum_{j,k} R_{j\bar{k}} dz^j \wedge d\bar{z}^k$。一个深刻的结果是，[里奇形式](@entry_id:183612)的[上同调类](@entry_id:263961)由[流形的拓扑](@entry_id:267834)决定。具体来说，它代表了[第一陈类](@entry_id:201400) $c_1(M)$ 的 $2\pi$ 倍：
$$
[\rho] = 2\pi c_1(M) \in H^2(M, \mathbb{R})
$$
[里奇形式](@entry_id:183612)的闭性 $d\rho=0$ 是这个[上同调](@entry_id:160558)论断的基础，并且可以通过上述局部表达式直接验证 [@problem_id:906297]。

### [典范度量](@entry_id:266957)与[卡拉比猜想](@entry_id:180885)

[几何分析](@entry_id:157700)的一个中心目标是在给定的[流形](@entry_id:153038)上寻找具有特殊性质的“[典范度量](@entry_id:266957)”，例如具有常曲率的度量。在[凯勒几何](@entry_id:160314)中，最自然的一类[典范度量](@entry_id:266957)是**[凯勒-爱因斯坦度量](@entry_id:270601) (Kähler-Einstein metrics)**，它满足 $\rho = \lambda \omega$，其中 $\lambda$ 是一个实常数。

这引出了一个基本问题：给定一个紧致凯勒流形 $M$ 和一个凯勒类 $[\omega_0]$（即由闭的、正的 (1,1)-型形式构成的上同调类），我们能否在该凯勒类中找到一个凯勒度量，使其[里奇曲率](@entry_id:162038)等于某个预先给定的形式？

**[卡拉比猜想](@entry_id:180885) (Calabi Conjecture)** 对此给出了肯定的回答。该猜想由丘成桐 (Shing-Tung Yau) 在1978年证明，其内容如下：
**定理 (Yau, 1978):** 设 $M$ 为紧致凯勒流形，$[\omega_0]$ 为其上的一个凯勒类。对任意代表 $2\pi c_1(M)$ 的实的、闭的 (1,1)-型形式 $\rho$，在 $[\omega_0]$ 中存在唯一一个凯勒度量 $\omega$，使得其[里奇形式](@entry_id:183612)恰好为 $\rho$，即 $\mathrm{Ric}(\omega) = \rho$ [@problem_id:2982230]。

这个纯粹的几何存在性和唯一性问题，被丘成桐转化为一个高度[非线性](@entry_id:637147)的二阶[椭圆偏微分方程](@entry_id:178258)——**复 Monge-Ampère 方程**。寻找满足 $\mathrm{Ric}(\omega_\varphi) = \rho$ 的度量 $\omega_\varphi = \omega_0 + \mathrm{i}\partial\bar{\partial}\varphi$ 的问题，等价于求解关于未知势函数 $\varphi$ 的方程：
$$
(\omega_0 + \mathrm{i}\partial\bar{\partial}\varphi)^n = e^{f+c} \omega_0^n
$$
其中函数 $f$ 由 $\mathrm{Ric}(\omega_0) - \rho = \mathrm{i}\partial\bar{\partial}f$ 确定，常数 $c$ 由体积[归一化条件](@entry_id:156486)决定 [@problem_id:3031487]。丘成桐通过建立该方程解的[先验估计](@entry_id:186098)，成功证明了解的存在性。

[卡拉比猜想](@entry_id:180885)最著名的推论是关于[第一陈类](@entry_id:201400)为零的[流形](@entry_id:153038)。若 $c_1(M)=0$，我们可以取 $\rho=0$。丘成桐的定理保证了在每个凯勒类中，都存在一个唯一的**[里奇平坦](@entry_id:159097) (Ricci-flat)** 的凯勒度量。这些度量被称为**卡拉比-丘度量 (Calabi-Yau metrics)**，拥有 $\mathrm{SU}(n)$ 和乐群，它们在弦理论和[数学物理](@entry_id:265403)中扮演着至关重要的角色。

### [凯勒几何](@entry_id:160314)与拓扑：Lefschetz 定理

[凯勒流形](@entry_id:161192)的刚性结构对其拓扑施加了极强的限制。这些限制的根源在于一系列被称为**凯勒恒等式 (Kähler identities)** 的代数关系，它们联系了外微分算子 $d, \partial, \bar{\partial}$，它们的伴随算子，以及与凯勒形式 $\omega$ 相关的**Lefschetz 算子** $L(\eta) = \omega \wedge \eta$ 及其伴随算子 $\Lambda$ [@problem_id:3034906]。

这些恒等式的一个直接后果是紧致凯勒流形上的[霍奇理论](@entry_id:161814)，它不仅导致了上同调群的[霍奇分解](@entry_id:160332) $H^k(M, \mathbb{C}) = \bigoplus_{p+q=k} H^{p,q}(M)$，还揭示了[霍奇数](@entry_id:161605) $h^{p,q} = \dim H^{p,q}(M)$ 的对称性，如 $h^{p,q} = h^{q,p}$。这立刻导出 $b_1 = h^{1,0} + h^{0,1} = 2h^{1,0}$ 必须是偶数，为我们之前提到的拓扑障碍提供了理论依据 [@problem_id:3031483]。

[凯勒几何](@entry_id:160314)对拓扑最惊人的影响体现在**硬 Lefschetz 定理 (Hard Lefschetz Theorem)** 中。该定理断言，在 $n$ 维紧致凯勒流形上，对于 $k \le n$，由 Lefschetz 算子幂次诱导的映射
$$
L^{n-k}: H^k(M, \mathbb{R}) \to H^{2n-k}(M, \mathbb{R})
$$
是一个同构。

[复射影空间](@entry_id:268402) $\mathbb{CP}^n$ 及其上的 Fubini-Study 度量是检验这些思想的理想范例。$\mathbb{CP}^n$ 的[上同调环](@entry_id:160158)由一个2-次[上同调类](@entry_id:263961) $\alpha=[\omega]$ 生成，即 $H^\bullet(\mathbb{CP}^n; \mathbb{R}) \cong \mathbb{R}[\alpha]/\langle\alpha^{n+1}\rangle$。其[贝蒂数](@entry_id:153109)仅在偶数维非零。在这种情况下，硬 Lefschetz 映射 $L^{n-2k}: H^{2k} \to H^{2n-2k}$ 的作用是将基底元素 $\alpha^k$ 映射到 $\alpha^{n-k}$，这显然是一个同构 [@problem_id:3031509]。这个例子完美地展示了凯勒结构如何通过 Lefschetz 算子在[流形](@entry_id:153038)的上同调群之间建立起深刻的对称性。