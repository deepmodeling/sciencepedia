## 引言
在研究复[半单李代数](@entry_id:190073)的结构时，基底的选择至关重要。尽管任何基底都能描述其代数运算，但其[结构常数](@entry_id:157960)通常是任意的复数，这限制了[李理论](@entry_id:148240)在复数域之外的应用。为了克服这一障碍，数学家 Claude Chevalley 提出了一种精妙的构造，即谢瓦莱基（Chevalley basis），它旨在寻找一个“理想”的基底，使得所有[结构常数](@entry_id:157960)均为整数。这一追求不仅在代数上极为优美，更开辟了将[李理论](@entry_id:148240)推广到任意域的道路。

本文系统地探讨了谢瓦莱基的理论与实践。读者将首先在“原理与机制”一章中学习其严谨的定义、构造方法以及由整[结构常数](@entry_id:157960)带来的深刻代数性质。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示谢瓦莱基如何成为连接[李代数表示论](@entry_id:190569)、数论、[算术几何](@entry_id:189136)乃至[理论物理学](@entry_id:154070)的关键桥梁。最后，通过“动手实践”中的具体问题，读者将有机会亲手应用这些概念，巩固对这一强大工具的理解。

## 原理与机制

继引言之后，本章深入探讨谢瓦莱基（Chevalley basis）的[构造原理](@entry_id:141667)、[代数结构](@entry_id:137052)及其内在机制。我们将从复[半单李代数](@entry_id:190073)出发，系统地阐述谢瓦莱基的定义，揭示其[结构常数](@entry_id:157960)为整数这一核心特性，并展示该基底如何在不同表示和[代数结构](@entry_id:137052)中发挥其基础性作用。

### 谢瓦莱基的定义：对整性的追求

对于一个复[半单李代数](@entry_id:190073) $\mathfrak{g}$，其基本结构由卡丹分解（Cartan decomposition）给出：$\mathfrak{g} = \mathfrak{h} \oplus \bigoplus_{\alpha \in \Phi} \mathfrak{g}_\alpha$，其中 $\mathfrak{h}$ 是卡丹子代数，$\Phi$ 是根系，$\mathfrak{g}_\alpha$ 是对应于根 $\alpha$ 的一维根空间。虽然任何一组[基向量](@entry_id:199546)都可以用来描述 $\mathfrak{g}$ 的李括号运算，但其[结构常数](@entry_id:157960) $[X, Y] = \sum_i c_i Z_i$ 通常是任意的复数。谢瓦莱构造的核心目标，是为 $\mathfrak{g}$ 寻找一个“理想的”基底，使得所有[结构常数](@entry_id:157960)均为整数。这个看似纯粹的代数追求，最终为在任意域上构造李群的类似物（即谢瓦莱群）铺平了道路。

一个谢瓦莱基由两部分组成：一组构成卡丹子代数 $\mathfrak{h}$ 基底的元素，以及为根系 $\Phi$ 中每个根 $\alpha$ 选取的一个根向量 $e_\alpha$。

#### 卡丹子代数的基底：[余根](@entry_id:193338)

谢瓦莱基并非为卡丹子代数 $\mathfrak{h}$ 选取任意基底，而是选择了一组具有深刻代数意义的元素，称为**[余根](@entry_id:193338) (coroots)**。对于根空间 $\mathfrak{h}^*$ 上的任意一个根 $\alpha$，其对应的**对偶根 (dual root)** 或[余根](@entry_id:193338)定义为 $\alpha^\vee = \frac{2\alpha}{(\alpha, \alpha)}$，其中 $(\cdot, \cdot)$ 是由[基灵型](@entry_id:161046)（Killing form）诱导的[内积](@entry_id:158127)。

谢瓦莱基在 $\mathfrak{h}$ 中选取的基底是与单根 $\alpha_1, \dots, \alpha_r$ 对应的**单[余根](@entry_id:193338) (simple coroots)** $\{h_1, \dots, h_r\}$，其中 $h_i$ 定义为 $h_{\alpha_i}$。这些单[余根](@entry_id:193338)由它们与单根的作用唯一确定：
$$
\alpha_j(h_i) = \langle \alpha_j, \alpha_i^\vee \rangle = \frac{2(\alpha_j, \alpha_i)}{(\alpha_i, \alpha_i)} = A_{ji}
$$
这里的 $A_{ji}$ 是卡丹矩阵的元素。这个关系式是寻找[余根](@entry_id:193338)具体形式的关键。

例如，考虑[李代数](@entry_id:137954) $\mathfrak{sl}_3(\mathbb{C})$，即所有迹为零的 $3 \times 3$ [复矩阵](@entry_id:190650)构成的代数。其卡丹子代数 $\mathfrak{h}$ 是[对角矩阵](@entry_id:637782)的[子空间](@entry_id:150286)。若单根为 $\alpha_1 = L_1 - L_2$ 和 $\alpha_2 = L_2 - L_3$，其中 $L_i$ 是取[对角矩阵](@entry_id:637782)第 $i$ 个对角元的分量函数，我们可以确定单[余根](@entry_id:193338) $H_{\alpha_1}$（此处记为 $h_1$）。设 $h_1 = \text{diag}(a, b, c)$ 且 $a+b+c=0$。根据定义，它必须满足：
$$
\alpha_1(h_1) = (L_1 - L_2)(h_1) = a - b = A_{11} = 2
$$
$$
\alpha_2(h_1) = (L_2 - L_3)(h_1) = b - c = A_{21} = -1
$$
解这个线性方程组，可得 $a=1, b=-1, c=0$。因此，在 $\mathfrak{sl}_3(\mathbb{C})$ 的标准表示下，单[余根](@entry_id:193338) $h_1$ 的矩阵形式为 $h_1 = \text{diag}(1, -1, 0)$ [@problem_id:800051]。

一个重要的性质是，任意根 $\alpha$ 的[余根](@entry_id:193338) $h_\alpha$ 总是单[余根](@entry_id:193338)的整系数[线性组合](@entry_id:154743)。例如，对于 $\mathfrak{a}_2 \cong \mathfrak{sl}_3(\mathbb{C})$，其[正根](@entry_id:199264)为 $\alpha_1, \alpha_2, \alpha_1+\alpha_2$。可以证明，与根 $\alpha_1+\alpha_2$ 相关联的[余根](@entry_id:193338) $h_{\alpha_1+\alpha_2}$ 恰好是两个单[余根](@entry_id:193338)之和：$h_{\alpha_1+\alpha_2} = h_1 + h_2$ [@problem_id:800089]。这个性质源于[李代数](@entry_id:137954)的[雅可比恒等式](@entry_id:140480)，并体现了[余根](@entry_id:193338)系与根系之间的深刻对偶关系。

#### 根向量的选取

对于根系 $\Phi$ 中的每一个根 $\alpha$，我们从一维根空间 $\mathfrak{g}_\alpha$ 中选取一个非[零向量](@entry_id:156189) $e_\alpha$。这些根向量的选择并非任意，它们必须满足特定的[归一化条件](@entry_id:156486)，以确保[结构常数](@entry_id:157960)的整性。这些条件构成了谢瓦莱[交换关系](@entry_id:136780)的核心。

### 谢瓦莱[交换关系](@entry_id:136780)

一个基底 $\{h_i\}_{i=1}^r \cup \{e_\alpha\}_{\alpha \in \Phi}$ 构成谢瓦莱基，当且仅当它满足以下[交换关系](@entry_id:136780)：

1.  **卡丹子代数的[交换性](@entry_id:140240)**:
    $$[h_i, h_j] = 0$$
    这表明卡丹子代数是阿贝尔的。

2.  **卡丹子代数对根向量的作用**:
    $$[h_i, e_\alpha] = \langle \alpha, \alpha_i^\vee \rangle e_\alpha = A_{\alpha i} e_\alpha$$
    其中 $A_{\alpha i}$ 是根 $\alpha$ 在单根基下的坐标与卡丹矩阵的组合。这表明 $e_\alpha$ 是 $h_i$ 的[特征向量](@entry_id:151813)，[特征值](@entry_id:154894)为整数 $\langle \alpha, \alpha_i^\vee \rangle$。

3.  **$\mathfrak{sl}_2$-三元组的构成**:
    $$[e_\alpha, e_{-\alpha}] = h_\alpha$$
    这个关系是至关重要的[归一化条件](@entry_id:156486)。它将[正根](@entry_id:199264)向量、负根向量与相应的[余根](@entry_id:193338)联系在一起，形成一个同构于 $\mathfrak{sl}_2$ 的子代数。

4.  **根向量之间的交换子**:
    $$[e_\alpha, e_\beta] = N_{\alpha, \beta} e_{\alpha+\beta} \quad (\text{若 } \alpha+\beta \in \Phi)$$
    如果 $\alpha+\beta$ 不是根且不为零，则[交换子](@entry_id:158878)为零。谢瓦莱证明，通过恰当选择 $e_\alpha$ 的标度，可以使得所有的**[结构常数](@entry_id:157960)** $N_{\alpha, \beta}$ 均为**整数**。

这些整数 $N_{\alpha, \beta}$ 的符号依赖于具体的构造约定，但它们的[绝对值](@entry_id:147688)由根系的几何结构唯一确定。

### 基底的构造与[结构常数](@entry_id:157960)的确定

谢瓦莱基的构造是一个系统性的过程，通常从单根对应的元素开始，逐步生成整个基底。

首先，为单根 $\alpha_i$ 选取根向量 $e_{\alpha_i}$。在许多标准表示中，这些向量有非常自然的选择。例如，在 $\mathfrak{sl}_n(\mathbb{C})$ 的定义表示中，单根 $\alpha_i = \epsilon_i - \epsilon_{i+1}$ 对应的根向量 $e_{\alpha_i}$ 可以选择为[基本矩阵](@entry_id:275638) $E_{i, i+1}$（即在 $(i, i+1)$ 位置为1，其余位置为0的矩阵）。

接下来，非单[正根](@entry_id:199264)的根向量通过**塞尔构造 (Serre's construction)** 生成。如果一个[正根](@entry_id:199264) $\gamma$ 可以写成两个[正根](@entry_id:199264) $\alpha$ 和 $\beta$ 的和，那么其根向量 $e_\gamma$ 可以通过计算交换子 $[e_\alpha, e_\beta]$ 得到（可能需要一个[归一化常数](@entry_id:752675)）。例如，在 $\mathfrak{sl}_4(\mathbb{C})$ 中，根 $\alpha_1+\alpha_2$ 的根向量 $e_{\alpha_1+\alpha_2}$ 可定义为 $[e_{\alpha_1}, e_{\alpha_2}]$。若取 $e_{\alpha_1} = E_{12}$ 和 $e_{\alpha_2} = E_{23}$，则
$$
e_{\alpha_1+\alpha_2} = [E_{12}, E_{23}] = E_{12}E_{23} - E_{23}E_{12} = E_{13} - 0 = E_{13}
$$
这清晰地展示了如何从简单的构造块生成更复杂的元素 [@problem_id:799978]。

值得注意的是，根向量的选择存在一定的自由度。我们可以对每个 $e_\alpha$ 乘以一个标量，只要保持 $[e_\alpha, e_{-\alpha}] = h_\alpha$ 的关系即可。不同的初始选择会影响其他根向量的表达式和[结构常数](@entry_id:157960)的具体数值，但不会改变它们的整性。例如，在 $\mathfrak{sl}_3(\mathbb{C})$ 中，如果我们做出非标准的初始选择，如 $e_{\alpha_1} = -E_{12}$ 和 $e_{\alpha_2} = iE_{23}$，并通过 $N_{\alpha_1, \alpha_2}=1$ 的约定来构造，我们依然可以推导出所有其他[基向量](@entry_id:199546)及其交换关系，并最终得到一个自洽的、[结构常数](@entry_id:157960)为整数的基底 [@problem_id:800018]。

#### [结构常数](@entry_id:157960)的计算

[结构常数](@entry_id:157960) $N_{\alpha, \beta}$ 的大小可以通过一个优美的组合公式确定。对于任意两个根 $\alpha, \beta$，所有形如 $\beta+k\alpha$（$k$为整数）的根构成一个所谓的**$\alpha$-根链 (root string)**。假设此根链为 $\{\beta - p\alpha, \dots, \beta+q\alpha\}$，其中 $p,q$ 是非负整数。那么，[结构常数](@entry_id:157960)的[绝对值](@entry_id:147688)由下式给出：
$$
|N_{\alpha, \beta}| = p+1
$$
这个公式揭示了[结构常数](@entry_id:157960)的代数值与[根系](@entry_id:198970)的几何形态之间的深刻联系。

例如，对于[例外李代数](@entry_id:202996) $\mathfrak{g}_2$，其单根为短根 $\alpha_1$ 和长根 $\alpha_2$。我们来计算 $N_{\alpha_1, \alpha_1+\alpha_2}$。这里，$\alpha=\alpha_1$，$\beta=\alpha_1+\alpha_2$。我们需要考察通过 $\beta$ 的 $\alpha$-根链。
- $\beta - 0\alpha = \alpha_1+\alpha_2$，是根。
- $\beta - 1\alpha = \alpha_2$，是根。
- $\beta - 2\alpha = \alpha_2 - \alpha_1$，不是根。
因此，最大整数 $p$ 使得 $\beta - p\alpha$ 是根的值为 $p=1$。根据公式，我们得到 $|N_{\alpha_1, \alpha_1+\alpha_2}| = p+1=2$ [@problem_id:799938]。至于它的符号，则取决于具体的符号约定（例如，可以规定当 $\alpha, \beta$ 均为[正根](@entry_id:199264)时 $N_{\alpha, \beta}>0$）。

### 结构性质与对称性

谢瓦莱基的优美之处不仅在于其整性，还在于它所揭示的[李代数](@entry_id:137954)的内在对称性。

#### 谢瓦莱反[自同构](@entry_id:155390)

存在一个重要的线性映射 $\sigma: \mathfrak{g} \to \mathfrak{g}$，称为**谢瓦莱反自同构 (Chevalley antiautomorphism)**，其定义如下：
$$
\sigma(h_i) = -h_i \quad \text{for all } i
$$
$$
\sigma(e_\alpha) = -e_{-\alpha} \quad \text{for all } \alpha \in \Phi
$$
这个映射是一个**反[自同构](@entry_id:155390)**，意味着它反转[李括号](@entry_id:636461)的顺序：$\sigma([X, Y]) = [\sigma(Y), \sigma(X)]$。这一性质为[结构常数](@entry_id:157960)之间建立了一系列关系。例如，应用 $\sigma$ 于交换关系 $[e_\alpha, e_\beta] = N_{\alpha, \beta}e_{\alpha+\beta}$，我们得到：
$$
\sigma([e_\alpha, e_\beta]) = \sigma(N_{\alpha, \beta}e_{\alpha+\beta}) = N_{\alpha, \beta}\sigma(e_{\alpha+\beta}) = -N_{\alpha, \beta}e_{-(\alpha+\beta)}
$$
另一方面，
$$
[\sigma(e_\beta), \sigma(e_\alpha)] = [-e_{-\beta}, -e_{-\alpha}] = [e_{-\beta}, e_{-\alpha}] = N_{-\beta, -\alpha}e_{-(\alpha+\beta)}
$$
比较两式可得一个重要的对称关系：$N_{-\beta, -\alpha} = -N_{\alpha, \beta}$ [@problem_id:799896]。

#### [基灵型](@entry_id:161046)的不变性

李代数的[基灵型](@entry_id:161046) $K(X, Y) = \text{tr}(\text{ad}(X)\text{ad}(Y))$ 具有**不变性 (invariance)**，即 $K([X, Y], Z) = K(X, [Y, Z])$。这一性质是探索[结构常数](@entry_id:157960)之间关系的又一强大工具。

通过[不变性](@entry_id:140168)可以证明，对于谢瓦莱基的元素，[基灵型](@entry_id:161046)满足 $K(e_\alpha, e_\beta) = 0$ 除非 $\beta = -\alpha$。对于 $e_\alpha$ 和 $e_{-\alpha}$ 对，可以推导出其[基灵型](@entry_id:161046)的值与根长直接相关：
$$
K(e_\alpha, e_{-\alpha}) = \frac{2}{(\alpha, \alpha)}
$$
这里的[内积](@entry_id:158127) $(\cdot, \cdot)$ 是在 $\mathfrak{h}^*$ 上诱导的[内积](@entry_id:158127)。这个公式表明，根向量对的“长度”（由[基灵型](@entry_id:161046)衡量）与根本身的长度成反比。

在处理具有不同长度根的非单带（non-simply-laced）李代数（如 $\mathfrak{f}_4, \mathfrak{g}_2$）时，这一关系尤为重要。通常约定将[内积](@entry_id:158127)归一化，使得长根 $\alpha$ 的平方长度为 $(\alpha, \alpha)=2$。例如，在 $\mathfrak{f}_4$ 代数中，根长的平方比为2:1。若 $\alpha$ 是长根，$\beta$ 是短根，则 $(\alpha, \alpha)=2$ 且 $(\beta, \beta)=1$。根据上述公式，我们有：
$$
K(e_\alpha, e_{-\alpha}) = \frac{2}{2} = 1
$$
$$
K(e_\beta, e_{-\beta}) = \frac{2}{1} = 2
$$
因此，它们[基灵型](@entry_id:161046)值的比值为 $\frac{K(e_\alpha, e_{-\alpha})}{K(e_\beta, e_{-\beta})} = \frac{1}{2}$ [@problem_id:800072]。这揭示了谢瓦莱基的几何性质如何反映在代数的度量结构中。

此外，[基灵型](@entry_id:161046)的不变性还能用来推导不同[结构常数](@entry_id:157960)之间的关系。例如，在 $\mathfrak{a}_2$ 中，通过考察 $K([e_{-\alpha_1}, e_{\alpha_1+\alpha_2}], e_{-\alpha_2})$ 并利用[不变性](@entry_id:140168)，可以证明 $N_{-\alpha_1, \alpha_1+\alpha_2} = N_{\alpha_1+\alpha_2, -\alpha_2}$ [@problem_id:799963]。

### 谢瓦莱格与任意域上的群

谢瓦莱基最深远的应用在于它使得我们能够“离开”复数域 $\mathbb{C}$。由于谢瓦莱基的所有[结构常数](@entry_id:157960)都是整数，我们可以考虑由这些[基向量](@entry_id:199546)在[整数环](@entry_id:181003) $\mathbb{Z}$ 上生成的自由 $\mathbb{Z}$-模：
$$
\mathfrak{g}_\mathbb{Z} = \bigoplus_{i=1}^r \mathbb{Z}h_i \oplus \bigoplus_{\alpha \in \Phi} \mathbb{Z}e_\alpha
$$
这个 $\mathbb{Z}$-模被称为**谢瓦莱格 (Chevalley lattice)**。由于[结构常数](@entry_id:157960)是整数，李括号运算在 $\mathfrak{g}_\mathbb{Z}$ 上是封闭的，使其成为一个定义在整数环 $\mathbb{Z}$ 上的李代数。

一旦我们有了在 $\mathbb{Z}$ 上的[李代数](@entry_id:137954)，我们就可以通过[张量积](@entry_id:140694)运算，在任何[交换环](@entry_id:148261) $k$ 上定义一个李代数：
$$
\mathfrak{g}_k = \mathfrak{g}_\mathbb{Z} \otimes_\mathbb{Z} k
$$
特别地，如果 $k$ 是一个域，例如[有限域](@entry_id:142106) $\mathbb{F}_p$，我们就得到了一个在特征 $p$ 域上的李代数 $\mathfrak{g}_{\mathbb{F}_p}$。这本质上就是将所有整数[结构常数](@entry_id:157960)模 $p$ 来进行计算。

这个过程可能会导致[代数结构](@entry_id:137052)发生微妙的变化。例如，在李代数 $\mathfrak{f}_4$ 中，存在[结构常数](@entry_id:157960)满足 $|N_{\alpha, \beta}|=2$。这意味着在[整数环](@entry_id:181003) $\mathbb{Z}$ 上，$[e_\alpha, e_\beta] = \pm 2 e_{\alpha+\beta}$。当我们转到特征为2的域 $\mathbb{F}_2$ 上时，这个[结构常数](@entry_id:157960)变为 $2 \equiv 0 \pmod 2$。因此，在[李代数](@entry_id:137954) $\mathfrak{g}_{\mathbb{F}_2}$ 中，原本非零的[交换子](@entry_id:158878) $[e_\alpha, e_\beta]$ 可能会变为零。

这种从[复李代数](@entry_id:204650)出发，通过谢瓦莱基和整数格，最终在任意域（特别是有限域）上构造代数对象的方法，是通向**谢瓦莱群 (Chevalley groups)** 的桥梁。这些群是复李群在任意域上的[完美模拟](@entry_id:753337)，构成了[有限单群分类](@entry_id:138125)理论的基石，也是[现代代数学](@entry_id:171265)和数论研究的核心对象。