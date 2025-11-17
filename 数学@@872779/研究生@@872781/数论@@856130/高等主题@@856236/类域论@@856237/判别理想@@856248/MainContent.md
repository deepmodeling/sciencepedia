## 引言
[判别式理想](@entry_id:200833)是[代数数论](@entry_id:148067)中的一个基本[不变量](@entry_id:148850)，它深刻地揭示了数域扩张的内在算术结构。对于任何一个数域扩张，一个核心问题是如何量化其复杂性，特别是素理想在扩张中如何“分支”或“退化”，即[分歧](@entry_id:193119)现象。[判别式理想](@entry_id:200833)正是为了解决这一问题而生的强大工具，它将抽象的[代数结构](@entry_id:137052)与具体的算术行为联系起来。

本文将带领读者全面探索[判别式理想](@entry_id:200833)。在“原理与机制”一章中，我们将从格上的[双线性形式](@entry_id:746794)出发，建立[判别式](@entry_id:174614)的基本定义，并揭示其与迹形式、分歧理想和导子等核心概念的内在联系。随后的“应用与交叉联系”一章将展示[判别式](@entry_id:174614)在实践中的威力，阐述它如何作为[分歧](@entry_id:193119)的精确度量，在[类域论](@entry_id:155687)中扮演关键角色，并与[解析数论](@entry_id:158402)、[算术几何](@entry_id:189136)等领域产生深刻共鸣。最后，通过“动手实践”部分提供的具体计算问题，读者将有机会巩固所学理论知识。

现在，让我们从第一章开始，深入[判别式理想](@entry_id:200833)的理论核心，理解其基本原理与运作机制。

## 原理与机制

本章旨在深入探讨[代数数论](@entry_id:148067)中的一个核心[不变量](@entry_id:148850)——[判别式理想](@entry_id:200833)（the discriminant ideal）。我们将从其基本定义出发，系统地阐述其内在原理与关键机制。我们将看到，[判别式](@entry_id:174614)不仅是一个抽象的代数对象，它还深刻地编码了数域扩张中的分歧（ramification）信息，并与数域的其他重要[不变量](@entry_id:148850)，如分歧理想（the different ideal）和导子（the conductor），有着密不可分的关系。本章将从一般性的[代数结构](@entry_id:137052)入手，逐步聚焦于数域扩张，最终展示[判别式](@entry_id:174614)在具体计算和理论应用中的强大威力。

### 格的判别式与迹形式

在深入研究[数域的判别式](@entry_id:200799)之前，我们先在一个更具一般性的框架下建立核心概念。设 $K$ 是一个数域，其整数环为 $\mathcal{O}_K$（这是一个戴德金[整环](@entry_id:155321)）。令 $V$ 是一个 $n$ 维的 $K$-[向量空间](@entry_id:151108)，并设 $b: V \times V \to K$ 是一个[对称双线性形式](@entry_id:148281)。$V$ 中的一个**格 (lattice)** 是指一个满秩的、有限生成的 $\mathcal{O}_K$-[子模](@entry_id:148922)。如果一个格 $A$ 是一个自由 $\mathcal{O}_K$-模，我们可以取其一组 $\mathcal{O}_K$-基 $\{x_1, \dots, x_n\}$。

与这组基相关联，我们可以构造一个 Gram 矩阵，其元素由双线性形式 $b$ 给出：$G = (b(x_i, x_j))_{1 \le i,j \le n}$。这个[矩阵的行列式](@entry_id:148198) $d(x_1, \dots, x_n) = \det(G)$ 被称为该基的**判别式 (discriminant)**。

一个自然的问题是：[判别式](@entry_id:174614)在多大程度上依赖于基的选择？假设我们另取一组基 $\{y_1, \dots, y_n\}$，它与原基通过一个[基变换矩阵](@entry_id:184480) $C \in \text{GL}_n(\mathcal{O}_K)$ 联系，即 $y_i = \sum_{k} C_{ik} x_k$。通过[双线性形式](@entry_id:746794)的性质，可以推导出新基的 Gram 矩阵 $G'$ 与原矩阵 $G$ 的关系为 $G' = C G C^T$。取[行列式](@entry_id:142978)，我们得到：
$$ d(y_1, \dots, y_n) = \det(G') = \det(C) \det(G) \det(C^T) = (\det C)^2 d(x_1, \dots, x_n) $$
由于 $C$ 是 $\mathcal{O}_K$ 上的[可逆矩阵](@entry_id:171829)，其[行列式](@entry_id:142978) $\det C$ 必然是 $\mathcal{O}_K$ 中的一个单位元（unit）。因此，$(\det C)^2$ 也是一个单位元。这意味着，不同基的判别式之间仅相差一个单位元的平方。因此，由任意基的[判别式](@entry_id:174614)生成的 $\mathcal{O}_K$ 中的主理想是唯一确定的。这个理想被称为格 $A$ 关于[双线性形式](@entry_id:746794) $b$ 的**[判别式理想](@entry_id:200833) (discriminant ideal)**，记作 $\mathfrak{d}(A, b)$。

### 数域扩张的[判别式理想](@entry_id:200833)

现在，我们将上述[一般性](@entry_id:161765)框架应用于[代数数论](@entry_id:148067)的核心研究对象：数[域扩张](@entry_id:153187)。令 $L/K$ 为一个 $n$ 次[有限可分扩张](@entry_id:150910)。此时，[向量空间](@entry_id:151108) $V$ 就是 $L$，而最自然、最重要的[双线性形式](@entry_id:746794)是**迹形式 (trace form)**，定义为：
$$ T(x, y) = \text{Tr}_{L/K}(xy) \quad \text{for } x, y \in L $$
扩张 $L/K$ 的[可分性](@entry_id:143854)保证了迹形式是非退化的，这意味着对于任意非零的 $x \in L$，都存在 $y \in L$ 使得 $\text{Tr}_{L/K}(xy) \neq 0$。这一点至关重要，因为它确保了判别式不会恒为零 [@problem_id:3025775]。

我们考虑 $L$ 中的[整数环](@entry_id:181003) $\mathcal{O}_L$。它是一个秩为 $n$ 的 $\mathcal{O}_K$-模。在许多重要情况下（例如，当 $\mathcal{O}_K$ 是[主理想整环](@entry_id:152359)时，如 $K=\mathbb{Q}$），$\mathcal{O}_L$ 是一个自由 $\mathcal{O}_K$-模。此时，我们可以取其一组 $\mathcal{O}_K$-基 $\{e_1, \dots, e_n\}$，并根据迹形式计算[判别式](@entry_id:174614)，从而定义扩张 $L/K$ 的**[判别式理想](@entry_id:200833)** $\mathfrak{d}_{L/K}$：
$$ \mathfrak{d}_{L/K} = \langle \det(\text{Tr}_{L/K}(e_i e_j)) \rangle_{\mathcal{O}_K} $$
即使在 $\mathcal{O}_L$ 不是自由 $\mathcal{O}_K$-模的更一般情况下，我们也可以通过局部化的方法定义[判别式理想](@entry_id:200833)，它仍然是 $\mathcal{O}_K$ 中一个良定义的整理想。

一个特别重要且基础的情形是绝对扩张，即基域为 $K=\mathbb{Q}$。此时 $\mathcal{O}_K = \mathbb{Z}$，[判别式理想](@entry_id:200833)是 $\mathbb{Z}$ 中的一个[主理想](@entry_id:152760)，由一个唯一的整数 $d_L$ 生成（取决于符号约定，通常取正值）。这个整数 $d_L$ 被称为数域 $L$ 的**[判别式](@entry_id:174614) (discriminant)**。其[绝对值](@entry_id:147688) $|d_L|$ 称为**绝对[判别式](@entry_id:174614)** [@problem_id:3025781]。

### 阶的判别式

在[数域](@entry_id:155558) $L$ 中，除了其最大的[整数环](@entry_id:181003) $\mathcal{O}_L$（称为**极大阶 (maximal order)**）外，还存在其他被称为**阶 (order)** 的子环。一个 $L$ 中的阶 $A$ 是一个同时满足以下条件的子环：$A \subseteq \mathcal{O}_L$，且 $A$ 是一个秩为 $n=[L:\mathbb{Q}]$ 的自由 $\mathbb{Z}$-模。

阶的判别式定义方式与 $\mathcal{O}_L$ 完全相同，即选取其一组 $\mathbb{Z}$-基，并计算迹形式的 Gram 矩阵的行列式。阶的[判别式](@entry_id:174614)与极大阶的判别式之间存在一个非常优美的关系。设 $A \subset B$ 是 $L$ 中的两个阶，它们都是秩为 $n$ 的自由 $\mathbb{Z}$-模。由于 $A$ 是 $B$ 的[子模](@entry_id:148922)，我们可以选取 $B$ 的一组基 $\{\beta_1, \dots, \beta_n\}$ 和 $A$ 的一组基 $\{\alpha_1, \dots, \alpha_n\}$，它们之间通过一个整[系数矩阵](@entry_id:151473) $C$ 变换，$\alpha_i = \sum_j c_{ij} \beta_j$。加法群 $B/A$ 的阶，即**指数 (index)** $[B:A]$，等于 $|\det(C)|$。

利用上一节的判别式变换公式，我们立即得到：
$$ \text{disc}(A) = (\det C)^2 \text{disc}(B) = [B:A]^2 \text{disc}(B) $$
这个公式 [@problem_id:3025769] 是研究非极大阶[判别式](@entry_id:174614)的基础。特别地，对于任意阶 $A \subseteq \mathcal{O}_L$，我们有：
$$ \text{disc}(A) = [\mathcal{O}_L:A]^2 \text{disc}(\mathcal{O}_L) $$
这个关系表明，任何非极大阶的判别式都是极大阶判别式的一个倍数，其间的因子恰好是指数的平方。这意味着阶 $A$ 越“小”（即指数 $[\mathcal{O}_L:A]$ 越大），其判别式就越大。

在相对扩张 $L/K$ 的更一般情境下，该关系推广为理想的等式。对于 $\mathcal{O}_L$ 中的一个 $\mathcal{O}_K$-阶 $A$，我们有：
$$ \mathfrak{d}(A/\mathcal{O}_K) = [\mathcal{O}_L:A]_{\mathcal{O}_K}^2 \cdot \mathfrak{d}(\mathcal{O}_L/\mathcal{O}_K) $$
这里，$[\mathcal{O}_L:A]_{\mathcal{O}_K}$ 是一个推广了整数指数的**指数理想 (index ideal)**。这个理想可以通过 $\mathcal{O}_K$-模 $\mathcal{O}_L/A$ 的 **零阶 Fitting 理想 (zeroth Fitting ideal)** $\text{Fit}_0(\mathcal{O}_L/A)$ 来精确定义 [@problem_id:3025778]。

### 分歧理想及其与判别式的关系

[判别式理想](@entry_id:200833)的一个深刻意义在于它与另一个称为**[分歧](@entry_id:193119)理想 (different ideal)** 的[不变量](@entry_id:148850)之间的联系。为了定义分歧理想，我们首先引入 $\mathcal{O}_L$ 关于迹形式的[对偶格](@entry_id:150046)，称为**余分歧理想 (codifferent ideal)** 或逆[分歧](@entry_id:193119)理想：
$$ \mathfrak{D}_{L/K}^{-1} = \{ x \in L \mid \text{Tr}_{L/K}(x \mathcal{O}_L) \subseteq \mathcal{O}_K \} $$
可以证明，$\mathfrak{D}_{L/K}^{-1}$ 是 $L$ 中的一个分式理想，并且包含 $\mathcal{O}_L$。分歧理想 $\mathfrak{D}_{L/K}$ 就定义为 $\mathfrak{D}_{L/K}^{-1}$ 在分式理想群中的逆。由于 $\mathcal{O}_L \subseteq \mathfrak{D}_{L/K}^{-1}$，取逆后得到 $\mathfrak{D}_{L/K} \subseteq \mathcal{O}_L$，因此分歧理想是 $\mathcal{O}_L$ 的一个整理想。

[判别式理想](@entry_id:200833)和[分歧](@entry_id:193119)理想之间的基本关系由以下定理给出：
$$ \mathfrak{d}_{L/K} = N_{L/K}(\mathfrak{D}_{L/K}) $$
其中 $N_{L/K}$ 是从 $\mathcal{O}_L$ 的理想到 $\mathcal{O}_K$ 的理想的**范数映射 (norm map)**。这个**判别式-分歧公式**至关重要，因为它将一个定义在基域 $K$ 中的理想（判别式）与一个定义在扩张域 $L$ 中的理想（分歧理想）通过范数联系起来。

在绝对扩张 $K=\mathbb{Q}$ 的情况下，此公式具有一个清晰的数值解释。设 $d_L$ 为 $L$ 的判别式。公式变为 $(|d_L|)_{\mathbb{Z}} = N_{L/\mathbb{Q}}(\mathfrak{D}_{L/\mathbb{Q}})$。[理想的范数](@entry_id:155476)定义为 $N_{L/\mathbb{Q}}(\mathfrak{a}) = ([\mathcal{O}_L:\mathfrak{a}])_{\mathbb{Z}}$。因此，我们得到数值等式：
$$ |d_L| = [\mathcal{O}_L : \mathfrak{D}_{L/\mathbb{Q}}] $$
利用指数的对偶性 $[I^{-1}:\mathcal{O}_L] = [\mathcal{O}_L:I]$，我们还可以得到 $|d_L| = [\mathfrak{D}_{L/\mathbb{Q}}^{-1}:\mathcal{O}_L]$ [@problem_id:3025781]。这表明绝对[判别式](@entry_id:174614)精确地度量了[整数环](@entry_id:181003) $\mathcal{O}_L$ 在其[对偶格](@entry_id:150046)中的“稀疏”程度。

### 阶的导子

对于一个非极大阶 $A \subset \mathcal{O}_L$，还有一个称为**导子 (conductor)** 的重要理想，它捕捉了 $A$ 与 $\mathcal{O}_L$ 之间的差异。导子 $\mathfrak{f}(A)$ 定义为：
$$ \mathfrak{f}(A) = \{ x \in \mathcal{O}_L \mid x\mathcal{O}_L \subseteq A \} $$
根据定义，$\mathfrak{f}(A)$ 是 $\mathcal{O}_L$ 中包含在 $A$ 内部的最大的理想。它也可以被刻画为 $\mathcal{O}_L$-模 $\mathcal{O}_L/A$ 的**[零化子](@entry_id:155446) (annihilator)** [@problem_id:3025790]。

导子、指数和判别式之间存在着深刻的联系。一个关键的定理指出，对于[指数和](@entry_id:199860)导子范数，我们有等式 $[\mathcal{O}_L:A]^2 = N_{L/\mathbb{Q}}(\mathfrak{f}(A))$。将此关系与我们之前得到的公式 $\text{disc}(A) = [\mathcal{O}_L:A]^2 \text{disc}(\mathcal{O}_L)$ 相结合，可以得到[判别式](@entry_id:174614)与导子范数之间的直接关系：
$$ \text{disc}(A) = N_{L/\mathbb{Q}}(\mathfrak{f}(A)) \cdot \text{disc}(\mathcal{O}_L) $$
这个公式为我们提供了一个定性的理解：一个阶 $A$ 的判别式相对于[域判别式](@entry_id:198568) $\text{disc}(\mathcal{O}_L)$ 的“额外”部分，完全由其导子的范数所决定。导子“越大”（即其范数越大），意味着阶 $A$ 与极大阶 $\mathcal{O}_L$ 的差异越大，其判别式也相应地越大 [@problem_id:3025790]。

例如，在二次域中，任何阶都可以写成 $A = \mathbb{Z} + f\mathcal{O}_L = \mathbb{Z}[f\omega]$ 的形式，其中 $f \ge 1$ 是一个整数。此时，指数 $[\mathcal{O}_L:A] = f$，阶的导子是理想 $(f)\mathcal{O}_L$，于是我们有 $\text{disc}(A) = f^2 \text{disc}(\mathcal{O}_L)$ [@problem_id:3025790]。

### 分歧与判别式

[判别式理想](@entry_id:200833)最重要的作用是它精确地指出了哪些素理想在[域扩张](@entry_id:153187)中发生了**分歧 (ramification)**。一个由戴德金建立的基本定理断言：

**戴德金[判别式](@entry_id:174614)定理 (Dedekin[d'](@entry_id:189153)s Discriminant Theorem):** 基域 $\mathcal{O}_K$ 中的一个[素理想](@entry_id:154026) $\mathfrak{p}$ 在扩张 $L/K$ 中[分歧](@entry_id:193119)，当且仅当 $\mathfrak{p}$ 整除[判别式理想](@entry_id:200833) $\mathfrak{d}_{L/K}$。

换言之，[判别式理想](@entry_id:200833)的素因子恰好是所有在扩张中分歧的[素理想](@entry_id:154026)。这使得判别式成为研究算术性质的核心工具。

这种分歧现象的根源在于[分歧](@entry_id:193119)理想。一个扩张在 $\mathcal{O}_L$ 的[素理想](@entry_id:154026) $\mathfrak{P}$ 处分歧，当且仅当 $\mathfrak{P}$ 整除分歧理想 $\mathfrak{D}_{L/K}$。判别式-[分歧](@entry_id:193119)公式 $ \mathfrak{d}_{L/K} = N_{L/K}(\mathfrak{D}_{L/K}) $ 正是将这种发生在扩张域 $L$ 中的局部分歧信息（通过分歧理想）传递到基域 $K$ 中（通过[判别式理想](@entry_id:200833)）。

分歧的“剧烈”程度可以通过**[分歧](@entry_id:193119)群 (ramification groups)** 来量化。对于 $L/K$ 的一个伽罗瓦扩张，其伽罗瓦群为 $G$，在每个[素理想](@entry_id:154026) $\mathfrak{P}$ 上方都有一系列正规子群（[分歧](@entry_id:193119)群）$G_0 \supseteq G_1 \supseteq G_2 \supseteq \dots$。**[希尔伯特分歧公式](@entry_id:200135) (Hilbert's Different Formula)** 给出了分歧理想的 $\mathfrak{P}$-进赋值：
$$ v_{\mathfrak{P}}(\mathfrak{D}_{L/K}) = \sum_{i=0}^{\infty} (|G_i| - 1) $$
这个和是有限的，因为它对[分歧](@entry_id:193119)[群的阶](@entry_id:137115)数偏离 $1$ 的程度进行了累加 [@problem_id:3025782]。

在**驯分歧 (tame ramification)** 的情况下（即[分歧指数](@entry_id:186386) $e$ 与剩[余域](@entry_id:139336)特征 $p$ 互素），只有 $G_0$（[惯性群](@entry_id:200010)）非平凡，此时公式简化为 $v_{\mathfrak{P}}(\mathfrak{D}_{L/K}) = |G_0| - 1 = e-1$。在**[野分歧](@entry_id:149250) (wild ramification)** 的情况下（$p$ 整除 $e$），高阶[分歧](@entry_id:193119)群 $G_i (i \ge 1)$ 会有贡献，使得[分歧](@entry_id:193119)理想的指数变得更大。

### 计算方法与应用

理论的价值最终体现在其解决问题的能力上。我们现在探讨一些计算[判别式](@entry_id:174614)和运用其性质的关键方法。

#### [戴德金-库默尔定理](@entry_id:150157)

这是一个将多项式分解与[素理想分解](@entry_id:197179)联系起来的强大工具。设 $K=\mathbb{Q}(\theta)$，其中 $\theta$ 是整系数不[可约多项式](@entry_id:148759) $f(x)$ 的根。如果一个素数 $p$ 不整除指数 $[\mathcal{O}_K:\mathbb{Z}[\theta]]$，那么理想 $p\mathcal{O}_K$ 的分解方式与多项式 $f(x)$ 在模 $p$ 剩[余域](@entry_id:139336) $\mathbb{F}_p$ 上的分解方式完全一致。若 $\bar{f}(x) = \prod_i \bar{g}_i(x)^{e_i}$，则 $p\mathcal{O}_K = \prod_i \mathfrak{p}_i^{e_i}$，其中[分歧指数](@entry_id:186386)和剩余次数分别由 $e_i$ 和 $\deg(\bar{g}_i)$ 给出 [@problem_id:3025772]。

**示例 1 (驯[分歧](@entry_id:193119)):** 考虑 $f(x) = x^3 - x - 1$，其[判别式](@entry_id:174614) $\Delta(f) = -23$。由于 $-23$ 是无平方因子的，我们有 $\mathcal{O}_K = \mathbb{Z}[\theta]$ 且[域判别式](@entry_id:198568) $d_K = -23$。对于 $p=23$，$\bar{f}(x) \equiv (x-10)^2(x-3) \pmod{23}$。[戴德金-库默尔定理](@entry_id:150157)适用，表明 $23\mathcal{O}_K = \mathfrak{p}_{1}^2 \mathfrak{p}_{2}$，[分歧指数](@entry_id:186386)分别为 $e_1=2, e_2=1$，剩余次数均为 $1$。这是一个驯[分歧](@entry_id:193119)（$23 \nmid 2$）。利用驯分歧公式 $v_p(d_K) = \sum f_i(e_i - 1)$，我们得到 $v_{23}(d_K) = 1 \cdot (2-1) + 1 \cdot (1-1) = 1$，这与 $d_K=-23$ 的结果一致 [@problem_id:3025772]。

**示例 2 (驯[分歧](@entry_id:193119)与[野分歧](@entry_id:149250)):** 考虑 $K=\mathbb{Q}(\sqrt[3]{2})$，其由 $f(x)=x^3-2$ 定义。
- 在 $p=2$ 处，$\bar{f}(x) \equiv x^3 \pmod{2}$。由于整数环为 $\mathcal{O}_K=\mathbb{Z}[\sqrt[3]{2}]$，[戴德金-库默尔定理](@entry_id:150157)适用，故 $2\mathcal{O}_K = \mathfrak{p}_2^3$。[分歧指数](@entry_id:186386) $e=3$。由于 $p=2$ 不整除 $e=3$，这是驯分歧。分歧理想的指数为 $e-1=2$，故 $v_2(d_K) = f \cdot (e-1) = 1 \cdot 2 = 2$。
- 在 $p=3$ 处，情况更为复杂。虽然[戴德金-库默尔定理](@entry_id:150157)的简单应用（基于 $\bar{f}(x) \equiv x^3+1 \equiv (x+1)(x^2-x+1) \pmod{3}$）会错误地表明3不[分歧](@entry_id:193119)，但这是一个该定理条件不满足的典型例子。通过更深入的分析（例如使用[牛顿多边形](@entry_id:182301)），可以证明3实际上是[完全分歧的](@entry_id:189971)，$3\mathcal{O}_K = \mathfrak{p}_3^3$，[分歧指数](@entry_id:186386) $e=3$。由于 $p=3$ 整除 $e=3$，这是[野分歧](@entry_id:149250)。可以计算出[分歧](@entry_id:193119)理想的指数为 $v_{\mathfrak{p}_3}(\mathfrak{D}_{K/\mathbb{Q}}) = 3$。因此，$v_3(d_K) = f \cdot v_{\mathfrak{p}_3}(\mathfrak{D}) = 1 \cdot 3 = 3$。
综上，我们得到 $(v_2(d_K), v_3(d_K)) = (2, 3)$ [@problem_id:3025771]。

#### [判别式](@entry_id:174614)的[塔定律](@entry_id:150838)

对于一个[域塔](@entry_id:153606) $M/L/K$，[判别式理想](@entry_id:200833)满足一个传递性法则，称为**[塔定律](@entry_id:150838) (tower law)**：
$$ \mathfrak{d}_{M/K} = (N_{L/K}(\mathfrak{d}_{M/L})) \cdot (\mathfrak{d}_{L/K})^{[M:L]} $$
这个公式在理论和计算中都非常有用。例如，要验证其在 $M=\mathbb{Q}(\sqrt{5},\sqrt{13}) / L=\mathbb{Q}(\sqrt{5}) / \mathbb{Q}$ 中的成立，可以逐个素数比较该等式两边的 $p$-进赋值。这需要计算绝对判别式 $d_{M/\mathbb{Q}}=(65^2)$ 和 $d_{L/\mathbb{Q}}=5$，以及相对[判别式](@entry_id:174614) $\mathfrak{d}_{M/L}$（其分歧发生在 $13$ 上方），然后应用范数公式，最终验证等式在每个[分歧素数](@entry_id:183288) $p=5, 13$ 处都成立 [@problem_id:3025797]。

#### 导子-[判别式](@entry_id:174614)公式与[类域论](@entry_id:155687)

对于[阿贝尔扩张](@entry_id:152984)，判别式与[类域论](@entry_id:155687)中的核心概念——**导子 (conductor)** 建立了深刻的联系。一个[阿贝尔扩张](@entry_id:152984) $K/\mathbb{Q}$ 的**导子** $f_K$ 是使得 $K \subseteq \mathbb{Q}(\zeta_{f_K})$ 成立的最小正整数。**导子-[判别式](@entry_id:174614)公式**表明：
$$ |d_K| = \prod_{\chi \neq 1} f_{\chi} $$
其中乘积遍及 $K/\mathbb{Q}$ 的伽罗瓦群的所有非平凡特征 $\chi$，而 $f_{\chi}$ 是与 $\chi$ 关联的[狄利克雷特征](@entry_id:151586)的导子。

**示例 3:** 考虑 $m=13$ 次分圆域 $\mathbb{Q}(\zeta_{13})$ 中唯一的循环四次[子域](@entry_id:155812) $K$。其导子为 $13$。$K/\mathbb{Q}$ 的伽罗瓦群是 $4$ 阶循环群，有 $3$ 个非平凡特征。由于扩张的导子是 $13$，每个非平凡特征的导子也必定是 $13$。因此，$|d_K| = 13 \cdot 13 \cdot 13 = 13^3$。

更进一步，[类域论](@entry_id:155687)告诉我们，一个未[分歧](@entry_id:193119)的素数 $p$ 在 $K$ 中的分解行为由其[弗罗贝尼乌斯元](@entry_id:181102) (Frobenius element) $\text{Frob}_p$ 决定，而该元素又由 $p$ 模导子 $f_K$ 的[剩余类](@entry_id:185226)决定。在上述例子中，一个素数 $p \neq 13$ 在 $K$ 中完全分裂当且仅当 $p$ 模 $13$ 的[剩余类](@entry_id:185226)属于 $(\mathbb{Z}/13\mathbb{Z})^{\times}$ 中由伽罗瓦理论确定的指数为 $4$ 的[子群](@entry_id:146164)，即 $p$ 是模13的四次剩余。如果 $p$ 模 $13$ 的[剩余类](@entry_id:185226)是商[群的生成元](@entry_id:137215)，则 $p$ 保持为[惰性素数](@entry_id:196337)。这个例子完美地展示了判别式如何作为桥梁，将域的代数构造与素数的算术分解行为联系起来 [@problem_id:3025795]。