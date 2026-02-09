## 引言
在现代数学与物理学中，对称性的研究占据着核心地位，而半单李代数是描述连续对称性最强大的数学语言。要深入理解这些代数的结构及其表示，仅仅依靠抽象的代数运算是远远不够的。我们需要一个更直观、更具几何性的视角来揭示其内在的秩序与美感。

这正是“权空间” (weight space) 与“权格” (weight lattice) 理论的用武之地。它们将抽象的代数问题转化为一个欧几里得空间中的几何与拓扑问题，解决了如何系统地分类和构造李代数表示这一核心难题。通过将表示的“权”视为空间中的点，复杂的表示结构便化为清晰的几何图案。

本文将带领读者踏上探索这片几何疆域的旅程。在第一章“原理与机制”中，我们将奠定理论基础，详细介绍权空间的几何结构、根与权这两套坐标系，以及作为对称性核心的外尔群。随后，在第二章“应用与跨学科联系”中，我们将见证这些抽象概念如何在粒子物理学的标准模型、凝聚态物理的晶体结构计算乃至概率论中发挥惊人的作用。最后，通过第三章“动手实践”，读者将有机会亲手运用这些工具解决具体问题，从而将理论知识内化为强大的分析能力。

让我们首先进入“原理与机制”部分，深入探索权空间的核心原理，揭示其作为李代数表示论基石的几何与代数机制。

## 原理与机制

在对半单李代数及其表示进行深入研究时，其几何结构提供了强有力的工具和深刻的见解。继引言之后，本章将深入探讨权空间 (weight space) 的核心原理与机制。我们将权空间视为一个具有确定几何结构的欧几里得空间，并研究其内部的两种基本格——根格 (root lattice) 和权格 (weight lattice)。理解这些结构及其相互关系，是掌握李代数表示论的关键。

### 权空间的几何结构

对于一个秩为 $r$ 的半单李代数 $\mathfrak{g}$，其权空间是嘉当子代数 $\mathfrak{h}$ 的对偶空间 $\mathfrak{h}^*$。这个空间并非仅仅是一个抽象的向量空间，它被赋予了一个源自基灵型 (Killing form) 的确定内积 $(\cdot, \cdot)$，从而成为一个欧几里得空间。这使得我们能够讨论权与根的长度、它们之间的夹角等几何概念。

在权空间 $\mathfrak{h}^*$ 中，有两组特别重要的基向量，它们是理解代数结构的基础：

1.  **单根 (Simple Roots)**: 一组 $r$ 个线性无关的向量 $\{\alpha_1, \dots, \alpha_r\}$，记作 $\Pi$。它们是构成整个根系 $\Phi$ 的基本单元。任何根 $\beta \in \Phi$ 都可以表示为单根的整系数线性组合，且系数同为非负或同为非正。

2.  **基本权 (Fundamental Weights)**: 另一组 $r$ 个线性无关的向量 $\{\omega_1, \dots, \omega_r\}$。它们与单根之间通过一个关键的**对偶关系**联系起来。为了陈述这个关系，我们首先引入**余根 (coroot)** 的概念。对于任意根 $\alpha$，其对应的余根 $\alpha^\vee$ 定义为 $\alpha^\vee = \frac{2\alpha}{(\alpha, \alpha)}$。基本权 $\omega_i$ 的定义正是通过它们与单余根 (simple coroots) $\alpha_j^\vee$ 的配对来实现的：
    $$
    \langle \omega_i, \alpha_j^\vee \rangle \equiv \frac{2(\omega_i, \alpha_j)}{(\alpha_j, \alpha_j)} = \delta_{ij}
    $$
    其中 $\delta_{ij}$ 是克罗内克符号。这个定义表明，基本权构成了对偶于单余根基 $\{\alpha_1^\vee, \dots, \alpha_r^\vee\}$ 的一组基。

这两组基之间的转换关系由**嘉当矩阵 (Cartan matrix)** $A$ 编码。嘉当矩阵的元素定义为：
$$
A_{ij} = \langle \alpha_i, \alpha_j^\vee \rangle = \frac{2(\alpha_i, \alpha_j)}{(\alpha_j, \alpha_j)}
$$
嘉当矩阵不仅编码了单根之间的几何关系（如相对长度和夹角），也成为了连接根与权这两个世界的关键桥梁。

### 基之间的转换：嘉当矩阵的角色

嘉当矩阵最直接的应用之一，就是在单根基 $\{\alpha_i\}$ 和基本权基 $\{\omega_i\}$ 之间进行坐标变换。例如，我们可以将任意一个单根表示为基本权的线性组合。

假设我们想将单根 $\alpha_k$ 写作 $\alpha_k = \sum_{j=1}^r c_j \omega_j$。为了确定系数 $c_j$，我们可以利用基本权的对偶性。将上式与单余根 $\alpha_l^\vee$ 做配对（即应用 $\langle \cdot, \alpha_l^\vee \rangle$）：
$$
\langle \alpha_k, \alpha_l^\vee \rangle = \left\langle \sum_{j=1}^r c_j \omega_j, \alpha_l^\vee \right\rangle = \sum_{j=1}^r c_j \langle \omega_j, \alpha_l^\vee \rangle = \sum_{j=1}^r c_j \delta_{jl} = c_l
$$
根据嘉当矩阵的定义，我们有 $A_{kl} = \langle \alpha_k, \alpha_l^\vee \rangle$。因此，我们得到 $c_l = A_{kl}$。这意味着单根 $\alpha_k$ 在基本权基下的坐标恰好是嘉当矩阵的第 $k$ **行**的元素。即：
$$
\alpha_k = \sum_{j=1}^r A_{kj} \omega_j
$$
这个关系在一些应用中非常直接 [@problem_id:842108]。

让我们以 $A_3$ 型李代数 $\mathfrak{sl}_4(\mathbb{C})$ 为例 [@problem_id:842108]。其嘉当矩阵为：
$$
A = \begin{pmatrix} 2  & -1  & 0 \\ -1  & 2  & -1 \\ 0  & -1  & 2 \end{pmatrix}
$$
根据上述关系，我们可以直接读出单根 $\alpha_2$ 在基本权基 $\{\omega_1, \omega_2, \omega_3\}$ 下的表达式。其系数就是嘉当矩阵的第二行 $(-1, 2, -1)$。因此，我们有：
$$
\alpha_2 = -\omega_1 + 2\omega_2 - \omega_3
$$
这个简单的例子展示了嘉当矩阵作为“翻译词典”的强大功能。反过来，将基本权表示为单根的线性组合则需要嘉当矩阵的逆矩阵 $A^{-1}$，这一关系我们将在后续讨论格结构时再次遇到。

### 权空间中的几何计算

权空间的欧几里得结构允许我们进行各种几何计算，这对于理解表示的结构至关重要。

例如，我们可以计算不同基本权之间的夹角。考虑 $A_3$ 型李代数 $\mathfrak{sl}_4(\mathbb{C})$，我们可以将权空间 $\mathfrak{h}^*$ 嵌入到四维空间 $\mathbb{R}^4$ 中，并使用标准正交基 $\{\epsilon_1, \epsilon_2, \epsilon_3, \epsilon_4\}$ 进行描述，但需满足约束 $\sum h_i = 0$。在此框架下，基本权可以被具体表示出来 [@problem_id:842236]：
$$
\omega_1 = \frac{3}{4}\epsilon_1 - \frac{1}{4}\epsilon_2 - \frac{1}{4}\epsilon_3 - \frac{1}{4}\epsilon_4
$$
$$
\omega_2 = \frac{1}{2}\epsilon_1 + \frac{1}{2}\epsilon_2 - \frac{1}{2}\epsilon_3 - \frac{1}{2}\epsilon_4
$$
利用标准内积 $(\epsilon_i, \epsilon_j) = \delta_{ij}$，我们可以计算 $\omega_1$ 和 $\omega_2$ 的内积及各自的范数平方：
$$
(\omega_1, \omega_2) = \frac{3}{8} - \frac{1}{8} - \frac{1}{8} + \frac{1}{8} = \frac{1}{2}
$$
$$
(\omega_1, \omega_1) = \left(\frac{3}{4}\right)^2 + 3 \left(-\frac{1}{4}\right)^2 = \frac{9}{16} + \frac{3}{16} = \frac{12}{16} = \frac{3}{4}
$$
$$
(\omega_2, \omega_2) = 4 \left(\frac{1}{2}\right)^2 = 1
$$
因此，它们之间夹角 $\theta$ 的余弦值为：
$$
\cos\theta = \frac{(\omega_1, \omega_2)}{\sqrt{(\omega_1, \omega_1)(\omega_2, \omega_2)}} = \frac{1/2}{\sqrt{3/4 \cdot 1}} = \frac{1}{\sqrt{3}}
$$
这个计算具体地展示了权空间的几何性质。

更一般地，基本权之间的内积矩阵 $M_{ij} = (\omega_i, \omega_j)$ 与嘉当矩阵的逆密切相关。对于根长均一的单连通 (simply-laced) 代数（如 A, D, E 型），若规范化使得 $(\alpha_i, \alpha_j) = A_{ij}$，则有 $M = \frac{1}{2}A^{-1}$。对于更一般的情况，关系会更复杂，但通过计算嘉当矩阵的逆，总能得到这些内积 [@problem_id:842127]。

以 $D_5$ 型李代数 $\mathfrak{so}_{10}$ 为例，其所有单根的长度平方均为 $2$。在这种情况下，可以证明内积 $(\omega_i, \omega_j)$ 就等于逆嘉当矩阵的元素 $(A^{-1})_{ij}$。要计算向量 $\lambda = \omega_2 - \omega_4$ 的范数平方 $||\lambda||^2$，我们需要计算 $(\omega_2, \omega_2)$, $(\omega_4, \omega_4)$ 和 $(\omega_2, \omega_4)$。这对应于计算 $A^{-1}$ 的 $(2,2)$, $(4,4)$ 和 $(2,4)$ 元。对于 $D_5$ 的嘉当矩阵，可以算出 $\det(A)=4$，并通过计算伴随矩阵的相关元素得到：
$$
(\omega_2, \omega_2) = (A^{-1})_{22} = \frac{C_{22}}{\det A} = \frac{8}{4} = 2
$$
$$
(\omega_4, \omega_4) = (A^{-1})_{44} = \frac{C_{44}}{\det A} = \frac{5}{4}
$$
$$
(\omega_2, \omega_4) = (A^{-1})_{24} = \frac{C_{42}}{\det A} = \frac{4}{4} = 1
$$
于是，
$$
||\lambda||^2 = ||\omega_2 - \omega_4||^2 = (\omega_2, \omega_2) - 2(\omega_2, \omega_4) + (\omega_4, \omega_4) = 2 - 2(1) + \frac{5}{4} = \frac{5}{4}
$$
有时，一个特定的根向量可能恰好等于一个基本权。例如，在 $C_3$ 型李代数 $\mathfrak{sp}_6$ 中，可以证明其最高短根 $\beta_s$ 正好是第二个基本权 $\omega_2$ [@problem_id:842132]。这揭示了根与权之间深刻而具体的联系。

### 瓦尔群的作用：权空间中的对称性

根系 $\Phi$ 具有高度的对称性，这些对称性由**瓦尔群 (Weyl group)** $W$ 描述。瓦尔群是由对应于每个单根 $\alpha_i$ 的反射 $s_i \equiv s_{\alpha_i}$ 生成的有限群。反射 $s_\alpha$ 是关于通过原点且正交于 $\alpha$ 的超平面的镜面反射。它在权空间 $\mathfrak{h}^*$ 上的作用由以下公式给出：
$$
s_\alpha(\lambda) = \lambda - \langle \lambda, \alpha^\vee \rangle \alpha
$$
其中 $\langle \lambda, \alpha^\vee \rangle = \frac{2(\lambda, \alpha)}{(\alpha, \alpha)}$ 是一个整数，表示权 $\lambda$ 相对于根 $\alpha$ 的动力学坐标。

当我们将这个作用应用于基本权时，计算会因为对偶关系 $\langle \omega_i, \alpha_j^\vee \rangle = \delta_{ij}$ 而大大简化。例如，让我们计算在 $C_3$ 型李代数 $\mathfrak{sp}_6$ 中，反射 $s_{\alpha_2}$ 作用于基本权 $\omega_2$ 的结果 [@problem_id:842238]。
$$
s_{\alpha_2}(\omega_2) = \omega_2 - \langle \omega_2, \alpha_2^\vee \rangle \alpha_2 = \omega_2 - (1) \cdot \alpha_2 = \omega_2 - \alpha_2
$$
为了得到最终结果在基本权基下的表示，我们需要将 $\alpha_2$ 替换为其在 $\omega$ 基下的表达式。对于 $C_3$，其嘉当矩阵为 $A = \begin{pmatrix} 2  & -1  & 0 \\ -1  & 2  & -2 \\ 0  & -1  & 2 \end{pmatrix}$。根据我们之前的结论，$\alpha_2$ 的系数由嘉当矩阵的第二行给出，即 $\alpha_2 = -\omega_1 + 2\omega_2 - 2\omega_3$。代入可得：
$$
s_{\alpha_2}(\omega_2) = \omega_2 - (-\omega_1 + 2\omega_2 - 2\omega_3) = \omega_1 - \omega_2 + 2\omega_3
$$
瓦尔群的元素是这些简单反射的乘积。例如，我们可以计算复合元素 $w = s_1 s_2 s_1$ 作用在 $A_3$ 的权 $\omega_2$ 上的结果 [@problem_id:842268]。这类计算可以通过在方便的基（如 $\epsilon_i$ 基）中进行向量运算，然后将结果转换回 $\omega$ 基来完成。计算表明 $s_1 s_2 s_1(\omega_2) = -\omega_1 + \omega_3$。

### 瓦尔群轨道与稳定子

瓦尔群作用于一个给定的权 $\lambda$，会生成一个离散的点集，称为 $\lambda$ 的**瓦尔群轨道 (Weyl group orbit)**，记为 $W(\lambda) = \{w(\lambda) \mid w \in W\}$。轨道中所有权在几何上是等价的，并且在表示论中扮演着不可或缺的角色（例如，一个不可约表示中的所有权构成若干个瓦尔群轨道的并集）。

一个轨道的元素数量可以通过**轨道-稳定子定理**计算。稳定子 $W_\lambda$ 是瓦尔群中保持 $\lambda$ 不变的元素的集合，即 $W_\lambda = \{w \in W \mid w(\lambda) = \lambda\}$。该定理指出：
$$
|W(\lambda)| = \frac{|W|}{|W_\lambda|}
$$
这里的挑战在于确定稳定子群 $W_\lambda$ 的大小。一个重要的结论是，$W_\lambda$ 本身也是一个（通常较小的）瓦尔群，它由那些保持 $\lambda$ 不变的简单反射 $s_j$ 生成。反射 $s_j$ 保持 $\lambda$ 不变的条件是 $\lambda$ 位于其反射超平面上，即 $(\lambda, \alpha_j) = 0$，等价于 $\langle \lambda, \alpha_j^\vee \rangle = 0$。

我们可以通过一个精美的例子来说明这一点：计算 $A_3$ 型李代数中 $\omega_2$ 的轨道大小 [@problem_id:842159]。
1.  首先，$A_3$ 的瓦尔群是置换群 $S_4$，其阶为 $|W| = 4! = 24$。
2.  接下来确定稳定子 $W_{\omega_2}$。我们需要找到所有满足 $\langle \omega_2, \alpha_j^\vee \rangle = 0$ 的下标 $j$。根据对偶关系，$\langle \omega_2, \alpha_j^\vee \rangle = \delta_{2j}$。因此，当 $j=1, 3$ 时该条件成立，而当 $j=2$ 时不成立。
3.  这意味着稳定子 $W_{\omega_2}$ 是由 $s_1$ 和 $s_3$ 生成的。在 $A_3$ 的邓金图（Dynkin diagram）$\circ_1 - \circ_2 - \circ_3$ 中，这相当于“移除”与 $\omega_2$ 非正交的节点 $2$。剩下的图由两个不相连的节点 $1$ 和 $3$ 组成，它对应于 $A_1 \times A_1$ 型李代数。
4.  因此，$W_{\omega_2}$ 同构于 $W(A_1) \times W(A_1)$。由于 $W(A_1) \cong S_2$ 的阶为 $2$，我们得到 $|W_{\omega_2}| = 2 \times 2 = 4$。
5.  最后，应用轨道-稳定子定理：
    $$
    |W(\omega_2)| = \frac{24}{4} = 6
    $$
这个结果不仅展示了计算方法，也揭示了邓金图、稳定子和子代数之间的深刻联系。

### 格的结构：根格与权格

最后，我们来关注权空间中的两个核心离散结构：根格与权格。

- **根格 (Root Lattice)** $Q$：所有单根的整系数线性组合构成的格。$Q = \bigoplus_{i=1}^r \mathbb{Z}\alpha_i$。
- **权格 (Weight Lattice)** $P$：所有基本权的整系数线性组合构成的格。$P = \bigoplus_{i=1}^r \mathbb{Z}\omega_i$。等价地，权格是所有与任意单余根配对都得到整数的向量 $\lambda \in \mathfrak{h}^*$ 的集合。

从关系式 $\alpha_k = \sum_j A_{kj} \omega_j$ 和嘉当矩阵元素 $A_{kj}$ 均为整数可知，每个单根都是基本权的整系数线性组合。这立即推导出根格是权格的一个子格，即 $Q \subseteq P$。

这个包含关系不是平凡的，商群 $P/Q$ 是一个有限阿贝尔群，它揭示了代数和相关李群的深刻拓扑信息。这个群被称为代数的**基本群 (fundamental group)**，它同构于对应单连通李群 $G_{sc}$ 的中心 $Z(G_{sc})$，也同构于伴随李群 $G_{ad}$ 的基本群 $\pi_1(G_{ad})$。

该商群的阶，即 $Q$ 在 $P$ 中的指标 $[P:Q]$，可以通过一个优美的公式计算：
$$
[P:Q] = |P/Q| = |\det(A)|
$$
其中 $A$ 是嘉当矩阵。例如，对于 $B_3$ 型李代数 $\mathfrak{so}_7$ [@problem_id:842121]，其嘉当矩阵为：
$$
A = \begin{pmatrix} 2  & -1  & 0 \\ -1  & 2  & -1 \\ 0  & -2  & 2 \end{pmatrix}
$$
其行列式为 $\det(A) = 2$。因此，对于 $\mathfrak{so}_7$, $[P:Q]=2$，$P/Q \cong \mathbb{Z}_2$。

商群的阶只是第一步，其群结构本身也至关重要。例如，对于 $D_n$ 型李代数，其嘉当矩阵的[行列式](@entry_id:142978) $|\det(A)|=4$。但 $P/Q$ 的结构依赖于 $n$ 的奇偶性 [@problem_id:842262]：
$$
P/Q \cong \begin{cases} \mathbb{Z}_4  &\text{if } n \text{ is odd} \\ \mathbb{Z}_2 \times \mathbb{Z}_2  &\text{if } n \text{ is even} \end{cases}
$$
因此对于 $D_6$ 型的 $\mathfrak{so}(12)$ ($n=6$ 为偶数)，$P/Q \cong \mathbb{Z}_2 \times \mathbb{Z}_2$。这个群有 $4$ 个元素，其中 $3$ 个是非平凡元素。

一个实际的应用是判断一个给定的权 $\Lambda$ 是否属于根格 $Q$。一个不可约表示 $L(\Lambda)$ 的所有权都属于根格的充要条件是其最高权 $\Lambda \in Q$。要判断这一点，我们需要将 $\Lambda = \sum m_i \omega_i$ 转换到单根基下。这需要使用嘉当矩阵的逆 $A^{-1}$，因为 $\omega_i = \sum_j (A^{-1})_{ij} \alpha_j$。代入得：
$$
\Lambda = \sum_i m_i \left( \sum_j (A^{-1})_{ij} \alpha_j \right) = \sum_j \left( \sum_i m_i (A^{-1})_{ij} \right) \alpha_j
$$
$\Lambda$ 属于根格 $Q$ 的条件是上式中 $\alpha_j$ 的系数对所有 $j$ 都是整数。

考虑 $D_4$ 型李代数 $\mathfrak{so}_8$ 的一个表示，其最高权为 $\Lambda(k) = (k^2-4)\omega_1 + 2k\omega_2 + 5\omega_3 + k\omega_4$ [@problem_id:842234]。我们需要找到最小的正整数 $k$，使得 $\Lambda(k) \in Q$ 且为优势权。首先计算 $D_4$ 的逆嘉当矩阵：
$$
A^{-1} = \frac{1}{2}\begin{pmatrix} 2  & 2  & 1  & 1 \\ 2  & 4  & 2  & 2 \\ 1  & 2  & 2  & 1 \\ 1  & 2  & 1  & 2 \end{pmatrix}
$$
$\Lambda(k)$ 在 $\alpha$ 基下的系数是通过将系数向量 $(m_1, m_2, m_3, m_4) = (k^2-4, 2k, 5, k)$ 与 $A^{-1}$ 的列相乘得到。例如，$\alpha_1$ 的系数为 $(k^2-4)\cdot 1 + (2k)\cdot 1 + 5\cdot(1/2) + k\cdot(1/2) = k^2 + 2.5k - 1.5$。经过计算，要求所有系数为整数的条件最终归结为 $k$ 必须是奇数。同时，作为最高权，系数 $m_i$ 必须非负，即 $k^2-4 \ge 0 \Rightarrow k \ge 2$。满足这两个条件的最小正整数是 $k=3$。

通过这些例子，我们看到权空间、根格、权格和瓦尔群这些抽象概念如何交织在一起，构成了一幅精美的几何与代数画卷，为理解李代数表示论提供了坚实的基础。