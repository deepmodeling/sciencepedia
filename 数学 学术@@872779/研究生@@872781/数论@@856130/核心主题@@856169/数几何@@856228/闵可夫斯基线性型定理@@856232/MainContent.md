## 引言
闵可夫斯基[线性形式](@entry_id:276136)定理是“数之几何”领域的奠基性成果，它在看似无关的几何学与数论之间架起了一座优雅的桥梁。该定理深刻地回答了一个核心的算术问题：在何种条件下，我们能保证一个由多个线性形式组成的不等式系统，必定拥有一个非零的整数解？这个问题的答案不仅具有理论上的美感，更在数学的多个分支中扮演着至关重要的角色。本文旨在系统性地剖析这一定理，带领读者穿越其理论的深度与应用的广度。

本文将分为三个核心部分。在“原理与机制”一章中，我们将从几何直观出发，探讨定理的两种等价表述，并揭示其证明如何巧妙地[借力](@entry_id:167067)于更为根本的[闵可夫斯基凸体定理](@entry_id:183895)，同时分析其成立的边界条件与核心假设。接下来的“应用与跨学科关联”一章将展示该定理的强大威力，看它如何成为解决代数数论中[类数](@entry_id:156164)有限性、[狄利克雷单位定理](@entry_id:155550)等经典问题的关键，并如何在[丢番图逼近](@entry_id:199334)和更广泛的科学领域中发挥作用。最后，“动手实践”部分将通过具体问题，帮助读者将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将全面掌握闵可夫斯基[线性形式](@entry_id:276136)定理的精髓及其深远影响。

## 原理与机制

本章旨在深入探讨闵可夫斯基[线性形式](@entry_id:276136)定理 (Minkowski's Linear Forms Theorem) 的核心原理与证明机制。我们将从几何直观出发，建立证明该定理所需的关键要素，并阐明其与更具普适性的[闵可夫斯基凸体定理](@entry_id:183895)之间的深刻联系。我们的探讨不仅会涵盖定理的标准证明，还将深入分析其成立的边界条件与关键假设，从而为读者提供一个全面而严谨的理论框架。

### 几何基础：两种等价的视角

理解闵可夫斯基线性形式定理的精髓，始于认识到该问题可以从两种等价的几何视角进行阐述。这两种视角虽然出发点不同，但最终殊途同归，共同揭示了问题背后统一的几何结构。

我们考虑一个由 $n$ 个变量构成的 $n$ 个实线性形式组成的系统：
$$
L_i(\mathbf{x}) = \sum_{j=1}^n a_{ij} x_j, \quad \text{其中 } i \in \{1, \ldots, n\}
$$
其中 $\mathbf{x} = (x_1, \ldots, x_n)^{\mathsf{T}} \in \mathbb{R}^n$ 是变量向量。这些线性形式的系数 $a_{ij}$ 可以构成一个 $n \times n$ 的实矩阵 $A = (a_{ij})$。根据矩阵与向量乘法的定义，这个[线性形式](@entry_id:276136)系统可以被简洁地表示为一个[线性映射](@entry_id:185132) $T_A: \mathbb{R}^n \to \mathbb{R}^n$，其定义为 $T_A(\mathbf{x}) = A\mathbf{x}$。该映射的第 $i$ 个分量恰好是第 $i$ 个[线性形式](@entry_id:276136)的值，即 $(A\mathbf{x})_i = L_i(\mathbf{x})$ [@problem_id:3017951]。

闵可夫斯基线性形式定理旨在寻找一个非零整数向量 $\mathbf{z} \in \mathbb{Z}^n \setminus \{\mathbf{0}\}$，使得其在所有[线性形式](@entry_id:276136)下的取值都受到特定正实数 $b_1, \ldots, b_n$ 的约束：
$$
|L_i(\mathbf{z})| \le b_i \quad \text{对所有 } i \in \{1, \ldots, n\}
$$
这组不等式定义了 $\mathbb{R}^n$ 空间中的一个区域。现在，我们来探讨描述这个问题的两种几何框架。

#### 视角一：固定的格点，变换的区域

第一种视角将我们的注意力集中在标准的整数格 $\mathbb{Z}^n$ 上。我们试图证明，在这个固定的、规则的格点结构中，存在一个非零格点落入了由上述不等式所定义的特定区域内。

我们定义这个区域为 $K$：
$$
K = \{\mathbf{x} \in \mathbb{R}^n : |L_i(\mathbf{x})| \le b_i \text{ 对所有 } i=1,\dots,n\}
$$
为了更好地理解 $K$ 的几何形状，我们引入一个在“目标空间”中更为简单的几何体：一个轴对齐的超长方体（或称为“盒子”）$B$：
$$
B = \{\mathbf{y} \in \mathbb{R}^n : |y_i| \le b_i \text{ 对所有 } i=1,\dots,n\}
$$
利用 $L(\mathbf{x}) = A\mathbf{x}$ 的关系，我们可以看到，一个点 $\mathbf{x}$ 属于集合 $K$ 的充要条件是它的像 $A\mathbf{x}$ 属于盒子 $B$。如果矩阵 $A$ 是可逆的，那么这种关系可以写成 $\mathbf{x} \in A^{-1}(B)$。因此，**集合 $K$ 是轴对齐的盒子 $B$ 在线性映射 $A^{-1}$下的[原像](@entry_id:150899) (preimage)** [@problem_id:3017985]。

盒子 $B$ 本身是一个**中心对称**的**[凸体](@entry_id:183909)**。所谓中心对称，是指如果 $\mathbf{y} \in B$，那么 $-\mathbf{y}$ 也必然在 $B$ 中。所谓[凸体](@entry_id:183909)，是指连接 $B$ 中任意两点的线段完全包含在 $B$ 中。由于线性变换保持[中心对称](@entry_id:144242)性和[凸性](@entry_id:138568)，作为 $B$ 的[原像](@entry_id:150899)，集合 $K$ 也必然是一个[中心对称](@entry_id:144242)的[凸体](@entry_id:183909)。几何上，盒子 $B$ 是一个特殊的平行[多面体](@entry_id:637910)（orthotope），而 $K$ 则是 $B$ 经过线性变换 $A^{-1}$ 后得到的像，因此 $K$ 是一个（通常是倾斜的）**平行多面体 (parallelotope)**。

在此视角下，[线性形式](@entry_id:276136)问题转化为：证明标准整数格 $\mathbb{Z}^n$ 中至少存在一个非零点，位于这个中心对称的凸平行多面体 $K$ 内部。

#### 视角二：变换的格点，固定的区域

第二种视角则转换了我们的[参考系](@entry_id:169232)。我们不再考察标准格 $\mathbb{Z}^n$ 与复杂区域 $K$ 的关系，而是考察一个经过变换的、可能“倾斜”的格点结构与简单区域 $B$ 的关系。

我们定义一个由矩阵 $A$ 生成的**格 (lattice)** $\Lambda$：
$$
\Lambda = A(\mathbb{Z}^n) = \{A\mathbf{x} : \mathbf{x} \in \mathbb{Z}^n\}
$$
这个格 $\Lambda$ 是 $\mathbb{R}^n$ 的一个离散[子群](@entry_id:146164)，由 $A$ 的列向量的所有整数[线性组合](@entry_id:154743)构成。由于 $A$ 是可逆的，$\Lambda$ 是一个**满秩格 (full-rank lattice)**。

寻找一个非零整数向量 $\mathbf{x} \in \mathbb{Z}^n \setminus \{\mathbf{0}\}$ 使得 $|L_i(\mathbf{x})| \le b_i$ 成立，等价于寻找一个向量 $\mathbf{y} = A\mathbf{x}$，它满足 $|y_i| \le b_i$。由于 $\mathbf{x}$ 是非零整数向量，$\mathbf{y} = A\mathbf{x}$ 便是格 $\Lambda$ 中的一个非零点。而条件 $|y_i| \le b_i$ 恰好意味着 $\mathbf{y}$ 位于我们之前定义的轴对齐盒子 $B$ 中 [@problem_id:3017953]。

因此，在此视角下，[线性形式](@entry_id:276136)问题转化为：证明由 $A$ 生成的格 $\Lambda$ 中至少存在一个非零点，位于这个简单的轴对齐盒子 $B$ 内部。

这两种视角通过一个[线性变换](@entry_id:149133) $A$ 相互关联，它们是同一枚硬币的两面，为我们从不同角度证明和理解定理提供了便利 [@problem_id:3017962]。

### 体积的角色与[行列式](@entry_id:142978)

无论采取哪种视角，问题的核心都在于比较一个区域的“大小”和一个格点的“稀疏程度”。在[欧氏空间](@entry_id:138052)中，区域的大小由其**[勒贝格测度](@entry_id:139781) (Lebesgue measure)**，即**体积 (volume)** 来衡量。而格点的稀疏程度，则由其**[协体积](@entry_id:186549) (covolume)** 来描述，即格的[基本域](@entry_id:201756)的体积。

首先，我们确定相关几何体的体积。
- **盒子 $B$ 的体积**: 轴对齐盒子 $B = \prod_{i=1}^n [-b_i, b_i]$ 的体积是其各边长度的乘积。第 $i$ 维的边长为 $2b_i$，因此：
  $$
  \operatorname{vol}(B) = \prod_{i=1}^n (2b_i) = 2^n \prod_{i=1}^n b_i
  $$

- **[行列式](@entry_id:142978)作为[体积缩放因子](@entry_id:158899)**: 线性代数的一个基本事实是，当一个[可测集](@entry_id:159173) $S \subset \mathbb{R}^n$ 经过一个由可逆矩阵 $M$ 定义的[线性变换](@entry_id:149133) $T(\mathbf{x}) = M\mathbf{x}$ 时，其体积会缩放一个因子，这个因子恰好是[矩阵行列式](@entry_id:194066)的[绝对值](@entry_id:147688)：
  $$
  \operatorname{vol}(T(S)) = |\det M| \operatorname{vol}(S)
  $$

- **格的[协体积](@entry_id:186549)**: 对于由[可逆矩阵](@entry_id:171829) $A$ 生成的格 $\Lambda = A(\mathbb{Z}^n)$，其[协体积](@entry_id:186549)（记为 $\det(\Lambda)$）等于 $A$ 的列向量所张成的基本平行[多面体](@entry_id:637910)的体积。根据[体积缩放](@entry_id:197908)原理，这个体积等于 $|\det A|$ 乘以标准格 $\mathbb{Z}^n$ 的[基本域](@entry_id:201756)（单位超立方体）的体积，即 1。因此：
  $$
  \det(\Lambda) = |\det A|
  $$

现在，我们可以计算在第一种视角下出现的倾斜平行[多面体](@entry_id:637910) $K$ 的体积。我们已经知道 $K = A^{-1}(B)$，这意味着 $A(K) = B$。应用[体积缩放](@entry_id:197908)公式：
$$
\operatorname{vol}(B) = \operatorname{vol}(A(K)) = |\det A| \operatorname{vol}(K)
$$
由于 $A$ 可逆，$\det A \neq 0$，我们可以解出 $\operatorname{vol}(K)$：
$$
\operatorname{vol}(K) = \frac{\operatorname{vol}(B)}{|\det A|} = \frac{2^n \prod_{i=1}^n b_i}{|\det A|}
$$
这个公式是连接[线性形式](@entry_id:276136)参数 ($b_i$)、矩阵 $A$ 的性质 ($|\det A|$) 以及关键几何体 $K$ 的体积之间的桥梁 [@problem_id:3017965] [@problem_id:3017951]。

### [闵可夫斯基凸体定理](@entry_id:183895)：证明的引擎

连接几何体的体积与格点存在性的强大工具，是数学家 Hermann Minkowski 提出的**第一[凸体](@entry_id:183909)定理 (First Convex Body Theorem)**。这个定理是数论几何的基石。

**闵可夫斯基第一[凸体](@entry_id:183909)定理 (MCBT)**：设 $K$ 是 $\mathbb{R}^n$ 中的一个[中心对称](@entry_id:144242)、凸的、可测的集合，$\Lambda$ 是 $\mathbb{R}^n$ 中的一个满秩格。如果 $K$ 的体积满足
$$
\operatorname{vol}(K) > 2^n \det(\Lambda)
$$
那么 $K$ 必定包含 $\Lambda$ 中至少一个非零格点。

这个定理直观上是合理的：如果一个区域“足够大”，而格点又“足够密”，那么这个区域必然会“捕捉”到至少一个非零格点。$2^n$ 这个因子的出现有着深刻的几何原因。

#### [凸性](@entry_id:138568)与[中心对称](@entry_id:144242)性的关键作用

在应用MCBT之前，我们必须理解其假设为何如此重要。为什么集合 $K$ 必须是中心对称且凸的？这与MCBT的经典证明方法紧密相关，该证明巧妙地运用了[鸽巢原理](@entry_id:268698) [@problem_id:3017942]。

证明的关键步骤是考虑集合 $\frac{1}{2}K = \{\frac{1}{2}\mathbf{x} : \mathbf{x} \in K\}$。如果 $\operatorname{vol}(K) > 2^n \det(\Lambda)$，那么 $\operatorname{vol}(\frac{1}{2}K) = \frac{1}{2^n}\operatorname{vol}(K) > \det(\Lambda)$。这意味着 $\frac{1}{2}K$ 的体积比格 $\Lambda$ 的一个[基本域](@entry_id:201756)还要大。根据布里希菲尔德引理（Blichfeldt's Lemma），可以断言，必然存在 $\frac{1}{2}K$ 中的两个不同的点 $\mathbf{y}_1, \mathbf{y}_2$，它们的差是一个非零的格向量，即 $\mathbf{v} = \mathbf{y}_1 - \mathbf{y}_2 \in \Lambda \setminus \{\mathbf{0}\}$。

接下来的问题是：这个非零格向量 $\mathbf{v}$ 是否位于原始集合 $K$ 中？这正是**[中心对称](@entry_id:144242)性**和**凸性**发挥作用的地方。
1.  由于 $\mathbf{y}_1, \mathbf{y}_2 \in \frac{1}{2}K$，根据定义，存在 $\mathbf{x}_1, \mathbf{x}_2 \in K$ 使得 $\mathbf{y}_1 = \frac{1}{2}\mathbf{x}_1$ 且 $\mathbf{y}_2 = \frac{1}{2}\mathbf{x}_2$。
2.  因为 $K$ 是**中心对称**的，$\mathbf{x}_2 \in K$ 意味着 $-\mathbf{x}_2 \in K$。
3.  现在我们知道 $\mathbf{x}_1$ 和 $-\mathbf{x}_2$ 都在 $K$ 中。因为 $K$ 是**凸**的，连接这两点的线段上的中点也必须在 $K$ 中。这个中点就是：
    $$
    \frac{1}{2}(\mathbf{x}_1 + (-\mathbf{x}_2)) = \frac{1}{2}(\mathbf{x}_1 - \mathbf{x}_2) = \mathbf{y}_1 - \mathbf{y}_2 = \mathbf{v}
    $$
4.  因此，我们证明了 $\mathbf{v} \in K$。

这个论证表明，正是[中心对称](@entry_id:144242)和凸性这两个属性共同保证了[差集](@entry_id:140904) $(\frac{1}{2}K) - (\frac{1}{2}K)$ 包含于 $K$ 内，从而使得由[鸽巢原理](@entry_id:268698)找到的格向量能够落在我们所期望的集合中。缺少任何一个条件，这个结论都无法保证。

### 综合证明：线性形式定理的推导

现在，我们万事俱备，可以将所有部件组装起来，从两种视角推导出闵可夫斯基线性形式定理。

#### 从视角一推导

- **问题设定**: 寻找 $\mathbf{x} \in \mathbb{Z}^n \setminus \{\mathbf{0}\}$ 使得 $\mathbf{x} \in K = A^{-1}(B)$。
- **应用MCBT**: 我们将MCBT应用于中心对称[凸体](@entry_id:183909) $K$ 和标准格 $\mathbb{Z}^n$。标准格的[协体积](@entry_id:186549) $\det(\mathbb{Z}^n)=1$。
- **体积条件**: MCBT 要求 $\operatorname{vol}(K) > 2^n \det(\mathbb{Z}^n) = 2^n$。
- **代入计算**: 我们已经计算出 $\operatorname{vol}(K) = \frac{2^n \prod_{i=1}^n b_i}{|\det A|}$。因此，条件变为：
  $$
  \frac{2^n \prod_{i=1}^n b_i}{|\det A|} > 2^n \implies \prod_{i=1}^n b_i > |\det A|
  $$
- **结论**: 如果 $\prod_{i=1}^n b_i > |\det A|$ 成立，那么MCBT保证存在一个非零整数向量 $\mathbf{x} \in K \cap (\mathbb{Z}^n \setminus \{\mathbf{0}\})$。根据 $K$ 的定义，这个向量 $\mathbf{x}$ 满足 $|L_i(\mathbf{x})| \le b_i$ 对所有 $i$ 成立。这正是[线性形式](@entry_id:276136)定理的结论 [@problem_id:3017963]。

#### 从视角二推导

- **问题设定**: 寻找 $\mathbf{y} \in \Lambda \setminus \{\mathbf{0}\}$ 使得 $\mathbf{y} \in B$，其中 $\Lambda = A(\mathbb{Z}^n)$。
- **应用MCBT**: 我们将MCBT应用于[中心对称](@entry_id:144242)[凸体](@entry_id:183909)（盒子）$B$ 和格 $\Lambda$。
- **体积条件**: MCBT 要求 $\operatorname{vol}(B) > 2^n \det(\Lambda)$。
- **代入计算**: 我们知道 $\operatorname{vol}(B) = 2^n \prod_{i=1}^n b_i$ 且 $\det(\Lambda) = |\det A|$。因此，条件变为：
  $$
  2^n \prod_{i=1}^n b_i > 2^n |\det A| \implies \prod_{i=1}^n b_i > |\det A|
  $$
- **结论**: 如果 $\prod_{i=1}^n b_i > |\det A|$ 成立，那么MCBT保证存在一个非零格点 $\mathbf{y} \in B \cap (\Lambda \setminus \{\mathbf{0}\})$。由于 $\mathbf{y} \in \Lambda$，它必然可以写成 $\mathbf{y} = A\mathbf{x}$ 的形式，其中 $\mathbf{x} \in \mathbb{Z}^n \setminus \{\mathbf{0}\}$。而 $\mathbf{y} \in B$ 意味着 $|(A\mathbf{x})_i| \le b_i$，即 $|L_i(\mathbf{x})| \le b_i$。这同样得到了[线性形式](@entry_id:276136)定理的结论 [@problem_id:3017967]。

两种视角的推导都指向同一个条件和同一个结论，这深刻地揭示了闵可夫斯基线性形式定理本质上是[闵可夫斯基凸体定理](@entry_id:183895)在平行多面体这一特定几何背景下的直接应用 [@problem_id:3017962]。

### 重要考量与精妙之处

一个严谨的理论不仅需要清晰的证明，还需要对定理的假设、边界情况和适用范围有透彻的理解。

#### 边界情况：严格与非严格不等式

在上述推导中，我们使用了MCBT的严格不等式形式 $\operatorname{vol}(K) > 2^n \det(\Lambda)$。这自然地导出了线性形式定理中的严格不等式 $\prod b_i > |\det A|$。然而，定理的最强形式实际上是非严格的。我们如何从一个基于严格不等式的工具得到一个包含等号的结论呢？

答案在于一个精巧的**极限论证 (limiting argument)** [@problem_id:3017982]。假设我们想证明在条件 $\prod b_i = |\det A|$ 下定理依然成立。在这种情况下，集合 $K$ 的体积恰好是 $2^n$，MCBT的严格形式不再适用。

我们可以构造一个稍微“膨胀”的[集合序列](@entry_id:184571)。对于任意 $\varepsilon > 0$，我们定义新的界限 $b_i' = (1+\varepsilon)b_i$。对于这组新的界限，我们有 $\prod b_i' = (1+\varepsilon)^n \prod b_i = (1+\varepsilon)^n |\det A| > |\det A|$。因此，对于每一个 $\varepsilon > 0$，都存在一个非零整数向量 $\mathbf{x}_\varepsilon$ 满足 $|L_i(\mathbf{x}_\varepsilon)| \le (1+\varepsilon)b_i$。

现在，我们让 $\varepsilon$ 趋向于 0，例如取一系列 $\varepsilon_k = 1/k$。我们会得到一个非零整数向量序列 $\{\mathbf{x}_k\}_{k=1}^\infty$。所有的这些向量都位于一个固定的有界区域内（例如，由 $\varepsilon=1$ 定义的区域）。由于整数格是离散的，一个有界区域内只能包含有限个整数点。因此，根据[鸽巢原理](@entry_id:268698)，这个无限的向量序列中必然有一个非[零向量](@entry_id:156189) $\mathbf{z}$ 出现了无限多次。

对于这个固定的向量 $\mathbf{z}$，不等式 $|L_i(\mathbf{z})| \le (1+1/k)b_i$ 对无限多个 $k$ 值成立。让 $k \to \infty$，我们便得到 $|L_i(\mathbf{z})| \le b_i$。这样，我们就为等式情况 $\prod b_i = |\det A|$ 找到了一个非零整数解。

因此，闵可夫斯基线性形式定理的完整陈述是：
> 若 $A \in \text{GL}_n(\mathbb{R})$ 且 $b_1, \ldots, b_n$ 为正实数，满足 $\prod_{i=1}^n b_i \ge |\det A|$，则存在一个非零整数向量 $\mathbf{z} \in \mathbb{Z}^n \setminus \{\mathbf{0}\}$，使得 $|L_i(\mathbf{z})| \le b_i$ 对所有 $i=1, \ldots, n$ 成立。

#### [可逆性](@entry_id:143146)的必要性

在整个讨论中，我们都假设矩阵 $A$ 是可逆的，即 $A \in \text{GL}_n(\mathbb{R})$ 或 $\det A \neq 0$。这个条件是至关重要的。如果 $A$ 是奇异的（或称退化的），即 $\det A = 0$，会发生什么？[@problem_id:3017984]

当 $\det A = 0$ 时，[线性映射](@entry_id:185132) $A$ 将 $\mathbb{R}^n$ 压缩到一个维数更低的[子空间](@entry_id:150286)中。其**核 (kernel)** $\ker(A) = \{\mathbf{x} \in \mathbb{R}^n : A\mathbf{x} = \mathbf{0}\}$ 是一个至少一维的[子空间](@entry_id:150286)。

在这种情况下，集合 $K = A^{-1}(B)$ 的结构会发生根本性改变。如果 $\mathbf{x}_0$ 是 $K$ 中的一个点（即 $A\mathbf{x}_0 \in B$），那么对于任意 $\mathbf{v} \in \ker(A)$，我们有 $A(\mathbf{x}_0 + \mathbf{v}) = A\mathbf{x}_0 + A\mathbf{v} = A\mathbf{x}_0 + \mathbf{0} \in B$。这意味着整个仿射[子空间](@entry_id:150286) $\mathbf{x}_0 + \ker(A)$ 都包含在 $K$ 中。因此，$K$ 成为了一个**无界集**，其 $n$ 维体积为无穷大。

此时，体积条件 $\operatorname{vol}(K) > 2^n$ 总是被满足，但它失去了任何约束力。体积与参数 $b_i$ 之间的定量关系 $\operatorname{vol}(K) = (2^n \prod b_i)/|\det A|$ 因分母为零而失效。因此，基于体积的论证完全崩溃了。实际上，当 $A$ 奇异时，定理的结论通常是不成立的。我们可以轻易构造出一个奇异的 $A$ 和一组 $b_i$，使得满足条件的非零整数向量不存在。

#### 充分而非必要条件

值得强调的是，闵可夫斯基线性形式定理给出的 $\prod b_i \ge |\det A|$ 是一个**充分条件**，而非必要条件。也就是说，即使这个条件不满足，仍然可能存在满足不等式的非零整数点。

例如，考虑 $n=2$，$A = I_2$（[单位矩阵](@entry_id:156724)），此时 $|\det A| = 1$。线性形式为 $L_1(\mathbf{x}) = x_1, L_2(\mathbf{x}) = x_2$。我们选择 $b_1=1, b_2=0.5$。这里 $\prod b_i = 0.5  1$，不满足定理的条件。然而，非零整数向量 $\mathbf{z}=(1,0)$ 显然满足 $|L_1(\mathbf{z})|=1 \le 1$ 和 $|L_2(\mathbf{z})|=0 \le 0.5$。这说明，当体积不足时，一个点“碰巧”落入区域的可能性依然存在 [@problem_id:3017951]。[闵可夫斯基定理](@entry_id:204587)的威力在于，它保证了当体积足够大时，这种“碰巧”会变成一种“必然”。

#### 不变性

最后，定理的一个优美特性是其在格的[基变换](@entry_id:189626)下的[不变性](@entry_id:140168)。如果我们将矩阵 $A$ 替换为 $AU$，其中 $U$ 是一个**[幺模矩阵](@entry_id:148345) (unimodular matrix)**（即 $U$ 是一个整数矩阵且 $\det U = \pm 1$），那么定理的适用性不会改变 [@problem_id:3017967]。这是因为：
1.  新的[行列式](@entry_id:142978)[绝对值](@entry_id:147688)不变：$|\det(AU)| = |\det A||\det U| = |\det A|$。
2.  新的格不变：$AU(\mathbb{Z}^n) = A(\mathbb{Z}^n) = \Lambda$，因为[幺模矩阵](@entry_id:148345) $U$ 是 $\mathbb{Z}^n$ 的一个[自同构](@entry_id:155390)。

由于定理的条件 $\prod b_i \ge |\det A|$ 和所考察的格 $\Lambda$ 都没有改变，其结论自然也保持不变。这表明闵可夫斯基线性形式定理本质上是关于格 $\Lambda$ 本身的几何性质，而不依赖于我们选择哪个矩阵 $A$ 来表示这个格。