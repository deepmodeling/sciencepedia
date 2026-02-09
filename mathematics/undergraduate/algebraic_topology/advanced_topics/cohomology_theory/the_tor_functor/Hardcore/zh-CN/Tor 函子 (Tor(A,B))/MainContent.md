## 引言
在现代数学的宏伟蓝图中，同调代数扮演着至关重要的角色，它为不同数学分支提供了统一的语言和强大的计算工具。在这一领域中，Tor函子是一个基础而深刻的概念，它源于对张量积函子性质的探索。我们知道，张量积在处理代数结构时非常有用，但它并非完全“完美”——它只保持了序列的右正合性。这自然引出了一个核心问题：我们如何量化和理解张量积函子在保持单射性上的“失败”？Tor函子正是为了回答这一问题而生。

本文将带领读者深入探索Tor函子的世界。我们将从最基本的层面出发，逐步揭示其定义、性质和强大的应用。通过以下三个章节的系统学习，你将能够：

- 在**“原理与机制”**一章中，你将掌握Tor函子的形式化定义，学会如何通过自由分解来计算它，并理解其与长正合序列、挠子群以及平坦模等核心概念的内在联系。
- 在**“应用与跨学科联系”**一章中，你将见证Tor函子的威力，看它如何作为代数拓扑中泛系数定理和Künneth定理的基石，并如何跨越学科界限，在交换代数、群论甚至量子信息论中发挥关键作用。
- 最后，在**“动手实践”**部分，你将通过一系列精心设计的练习，将理论知识转化为实际的计算技能，从而真正巩固对Tor函子的理解。

让我们一同开启这段旅程，去发现Tor函子如何将抽象的代数结构与具体的数学问题巧妙地联系起来。

## 原理与机制

继前一章介绍张量积与同调的基本概念之后，本章将深入探讨一个核心的代数工具——**Tor函子**。Tor函子是张量积函子右正合性质的自然延伸，它为我们提供了一种精确度量张量积在何种程度上不保持短正合序列的方法。在代数拓扑中，Tor函子是万有系数定理和Künneth定理等关键理论的基石，它深刻地揭示了不同系数群的同调群之间的内在联系。

### Tor函子的定义

我们从Tor函子的构造开始。考虑一个交换环 $R$ 以及两个 $R$-模 $A$ 和 $B$。我们知道，对一个短正合序列 $0 \to M' \to M \to M'' \to 0$，施加函子 $- \otimes_R B$ 会得到一个右正合序列：
$$ M' \otimes_R B \to M \otimes_R B \to M'' \otimes_R B \to 0 $$
然而，最左边的映射 $M' \otimes_R B \to M \otimes_R B$ 通常不是单射。Tor函子 $\text{Tor}_n^R(A, B)$ 正是为了弥补这一“缺陷”而生的“导出函子”。

计算 $\text{Tor}_n^R(A, B)$ 的标准步骤如下：

1.  选取 $A$ 的一个**射影分解**（或自由分解）。在我们的主要研究领域，即整数环 $\mathbb{Z}$ 上的模（阿贝尔群）中，我们通常选取一个**自由分解**。这是一个由自由 $R$-模构成的长正合序列：
    $$ \dots \xrightarrow{d_3} F_2 \xrightarrow{d_2} F_1 \xrightarrow{d_1} F_0 \xrightarrow{\epsilon} A \to 0 $$
    其中每个 $F_i$ 都是自由 $R$-模。

2.  将函子 $- \otimes_R B$ 应用于上述分解（去掉 $A$ 项），得到一个链复形 $F_\bullet \otimes_R B$：
    $$ \dots \xrightarrow{d_3 \otimes \text{id}} F_2 \otimes_R B \xrightarrow{d_2 \otimes \text{id}} F_1 \otimes_R B \xrightarrow{d_1 \otimes \text{id}} F_0 \otimes_R B \to 0 $$
    注意，由于张量积函子并非左正合，这个新序列通常不再是正合的。

3.  第 $n$ 个 **Tor群** 被定义为这个链复形的第 $n$ 个同调群：
    $$ \text{Tor}_n^R(A, B) = H_n(F_\bullet \otimes_R B) = \frac{\ker(d_n \otimes \text{id})}{\text{im}(d_{n+1} \otimes \text{id})} $$

根据这个定义，$\text{Tor}_0^R(A, B)$ 正是我们熟悉的张量积 $A \otimes_R B$。本章的重点将是 $n \ge 1$ 的高阶Tor群，特别是 $\text{Tor}_1^R(A, B)$。

### $\mathbb{Z}$上的Tor函子

当我们把环 $R$ 特定为整数环 $\mathbb{Z}$ 时，模便是阿贝尔群，自由模便是自由阿贝尔群。此时，Tor函子的性质得到极大的简化。一个关于主理想整环（PID）上模的深刻结果是，任何自由阿贝尔群的子群仍然是自由阿贝尔群。这一事实导致了一个重要的推论：对于任意一个阿贝尔群 $A$，我们都可以构造一个长度为1的自由分解。

具体来说，我们可以选取一个满同态 $\epsilon: F_0 \to A$，其中 $F_0$ 是一个自由阿贝尔群（例如，由 $A$ 的所有元素作为生成元构成的自由群）。其核 $\ker(\epsilon)$ 作为 $F_0$ 的子群，也必然是自由的。令 $F_1 = \ker(\epsilon)$，我们就得到了一个短正合序列，也是 $A$ 的一个自由分解：
$$ 0 \to F_1 \xrightarrow{d_1} F_0 \xrightarrow{\epsilon} A \to 0 $$
我们可以将此分解视为一个无穷分解，其中对所有 $n \ge 2$，都有 $F_n = 0$。

当我们用这个分解来计算Tor群时，相应的链复形在 $n \ge 2$ 的位置上都是零。因此，其同调群也必然是零。这揭示了一个基本事实：对于任意两个阿贝尔群 $A$ 和 $B$ 以及所有整数 $n \ge 2$，总有：
$$ \text{Tor}_n^{\mathbb{Z}}(A, B) = \{0\} $$
因此，在阿贝尔群的范畴中，我们只需要关注 $\text{Tor}_1^{\mathbb{Z}}$，它捕捉了所有关于张量积非正合性的信息 [@problem_id:1690182]。为了简洁，我们后续将 $\text{Tor}_n^{\mathbb{Z}}(A, B)$ 简记为 $\text{Tor}_n(A, B)$。

### Tor长正合序列

Tor函子最有力的工具之一是它与短正合序列的相互作用。对于任意一个阿贝尔群的短正合序列 $0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0$ 和任意一个阿贝尔群 $G$，存在一个自然的长正合序列：
$$ \dots \to \text{Tor}_1(A, G) \to \text{Tor}_1(B, G) \to \text{Tor}_1(C, G) \xrightarrow{\partial} A \otimes G \xrightarrow{f \otimes \text{id}} B \otimes G \xrightarrow{g \otimes \text{id}} C \otimes G \to 0 $$
这里的 $\partial$ 称为**连接同态**。这个序列将不同群的Tor群和张量积联系在一起，是进行计算和理论推导的枢纽。

这个长正合序列的威力体现在它能区分不同类型的短正合序列。例如，考虑短正合序列 (I): $0 \to \mathbb{Z} \to \mathbb{Z} \oplus \mathbb{Z} \to \mathbb{Z} \to 0$。序列中的所有群都是自由阿贝尔群。自由群的一个重要特性是它们是**平坦**的，这意味着与它们作张量积是一个正合函子。用Tor函子的语言来说，一个模 $M$是平坦的，当且仅当对所有模 $N$，$\text{Tor}_1(M, N) = \{0\}$。由于序列 (I) 中的 $A, B, C$ 都是自由群，它们都是平坦的。因此，对应的长正合序列中的所有 $\text{Tor}_1$ 项均为零，这使得连接同态 $\partial_1$ 的定义域为零，其像自然也为零。序列的张量积部分 $A \otimes G \to B \otimes G \to C \otimes G \to 0$ 自身就是正合的 [@problem_id:1690186]。

相比之下，考虑序列 (II): $0 \to \mathbb{Z} \xrightarrow{\times 4} \mathbb{Z} \to \mathbb{Z}_4 \to 0$。这里的商群 $\mathbb{Z}_4$ 含有挠元。对应的长正合序列为：
$$ \text{Tor}_1(\mathbb{Z}, G) \to \text{Tor}_1(\mathbb{Z}_4, G) \xrightarrow{\partial_2} \mathbb{Z} \otimes G \xrightarrow{\times 4} \mathbb{Z} \otimes G \to \dots $$
由于 $\mathbb{Z}$ 是自由的，$\text{Tor}_1(\mathbb{Z}, G) = \{0\}$。因此，连接同态 $\partial_2$ 是一个单射。它的像 $\text{Im}(\partial_2)$ 同构于 $\text{Tor}_1(\mathbb{Z}_4, G)$，并且等于后续映射 $\times 4: G \to G$ 的核。这表明，当序列中出现挠群时，$\text{Tor}_1$ 通常是非平凡的，它精确地度量了张量积序列在左端“断裂”的程度 [@problem_id:1690186]。

我们可以通过一个具体的例子来理解连接同态 $\partial$ 的工作机制。考虑短正合序列 $0 \to \mathbb{Z} \xrightarrow{\times 12} \mathbb{Z} \to \mathbb{Z}_{12} \to 0$ 和群 $G=\mathbb{Z}_{18}$。长正合序列给出了连接同态 $\partial: \text{Tor}_1(\mathbb{Z}_{12}, \mathbb{Z}_{18}) \to \mathbb{Z} \otimes \mathbb{Z}_{18}$。通过计算可知 $\text{Tor}_1(\mathbb{Z}_{12}, \mathbb{Z}_{18}) \cong \mathbb{Z}_6$。为了计算连接同态 $\partial$ 的作用，我们遵循“图表追逐”的程序：将 $\mathbb{Z}_6$ 的一个生成元（在某个链复形中的代表元）提升到上一层，施加微分，然后利用正合性找到其原像。经过计算，我们发现 $\partial$ 将这个生成元映到 $\mathbb{Z} \otimes \mathbb{Z}_{18} \cong \mathbb{Z}_{18}$ 中一个阶为6的元素（例如 $3$）[@problem_id:1690175]。这个例子生动地展示了连接同态如何将高维的同调信息“连接”到低维的序列中。

### $\text{Tor}_1^{\mathbb{Z}}$ 的计算与解释

#### 对称性

尽管Tor函子的定义在两个变量 $A$ 和 $B$ 上看起来不对称（因为它依赖于对 $A$ 的分解），但一个深刻的定理指出，结果与分解的选择无关，并且函子本身是同构意义下对称的：
$$ \text{Tor}_n(A, B) \cong \text{Tor}_n(B, A) $$
我们可以通过一个核心例子来验证这一事实。让我们计算 $\text{Tor}_1(\mathbb{Z}_n, \mathbb{Z}_m)$。

首先，我们取 $\mathbb{Z}_n$ 的标准自由分解 $0 \to \mathbb{Z} \xrightarrow{\cdot n} \mathbb{Z} \to \mathbb{Z}_n \to 0$。与 $\mathbb{Z}_m$ 作张量积，我们得到链复形 $\mathbb{Z} \otimes \mathbb{Z}_m \xrightarrow{\cdot n \otimes \text{id}} \mathbb{Z} \otimes \mathbb{Z}_m$。利用同构 $\mathbb{Z} \otimes \mathbb{Z}_m \cong \mathbb{Z}_m$，这个链复形等价于 $\mathbb{Z}_m \xrightarrow{\cdot n} \mathbb{Z}_m$。$\text{Tor}_1(\mathbb{Z}_n, \mathbb{Z}_m)$ 就是这个映射的核。一个元素 $\bar{x} \in \mathbb{Z}_m$ 在核中当且仅当 $nx \equiv 0 \pmod m$。这个子群是循环群，其阶数为 $\gcd(n, m)$。

反过来，如果我们分解 $\mathbb{Z}_m$ 并与 $\mathbb{Z}_n$ 作张量积，我们会计算映射 $\mathbb{Z}_n \xrightarrow{\cdot m} \mathbb{Z}_n$ 的核，其阶数同样是 $\gcd(m, n)$。因此，两种计算方法都导向了相同的结果 [@problem_id:1690179] [@problem_id:1690178]：
$$ \text{Tor}_1(\mathbb{Z}_n, \mathbb{Z}_m) \cong \mathbb{Z}_{\gcd(n, m)} $$

#### Tor函子与挠子群

上述计算提供了一个至关重要的解释。如果我们取 $A = \mathbb{Z}_n$，那么对于任意阿贝尔群 $G$，我们有：
$$ \text{Tor}_1(\mathbb{Z}_n, G) \cong \ker(G \xrightarrow{\cdot n} G) = \{g \in G \mid ng = 0\} $$
这正是 $G$ 的 **$n$-挠子群**，通常记作 $G[n]$ [@problem_id:1690189]。这个结果为 $\text{Tor}_1$ 提供了具体的含义：$\text{Tor}_1(\mathbb{Z}_n, -)$ 是一个从阿贝尔群范畴到自身的函子，它精确地挑出了每个群中被 $n$ 消灭的元素。

这一观察可以推广。事实上，$\text{Tor}_1(A, B)$ 总是与 $A$ 和 $B$ 中的挠元紧密相关。一个普适的结论是：对任意阿贝尔群 $A$ 和 $B$，$\text{Tor}_1(A, B)$ **必定是一个挠群**，即其中每个元素都有有限的阶。

要理解这一点，我们首先注意到 $\text{Tor}_1(A, B) \cong \text{Tor}_1(A, t(B))$，其中 $t(B)$ 是 $B$ 的挠子群。这是因为商群 $B/t(B)$ 是无挠的，而在 $\mathbb{Z}$-模的范畴中，无挠等价于平坦，所以 $\text{Tor}_1(A, B/t(B))=\{0\}$。因此，我们只需证明 $\text{Tor}_1(A, t(B))$ 是挠群。考虑 $A$ 的自由分解 $0 \to F_1 \to F_0 \to A \to 0$。$\text{Tor}_1(A, t(B))$ 是 $\ker(F_1 \otimes t(B) \to F_0 \otimes t(B))$。任取该核中的一个元素 $z = \sum_k f_k \otimes b_k$，其中 $f_k \in F_1, b_k \in t(B)$。由于 $t(B)$ 是挠群，存在一个正整数 $N$ 使得对所有的 $k$ 都有 $N b_k = 0$。那么：
$$ N z = \sum_k f_k \otimes (N b_k) = \sum_k f_k \otimes 0 = 0 $$
这意味着 $z$ 的同调类 $[z]$ 在 $\text{Tor}_1(A, t(B))$ 中的阶是有限的（整除 $N$）。因此，该群是挠群 [@problem_id:1690169]。

#### Tor函子与平坦模

刚刚我们提到了**平坦模**的概念。一个 $\mathbb{Z}$-模（阿贝尔群）$B$ 是平坦的，当且仅当函子 $- \otimes_{\mathbb{Z}} B$ 是正合的。根据长正合序列理论，这等价于对所有阿贝尔群 $A$，都有 $\text{Tor}_1(A, B) = \{0\}$。

我们已经知道自由阿贝尔群是平坦的。一个更微妙的例子是**有理数群** $\mathbb{Q}$。$\mathbb{Q}$ 是一个无挠群，但它不是自由的。然而，$\mathbb{Q}$ 是平坦的。要理解这一点，我们可以考虑 $\text{Tor}_1(\mathbb{Q}, B)$。利用对称性，这同构于 $\text{Tor}_1(B, \mathbb{Q})$。根据定义，这是 $\ker(F_1 \otimes \mathbb{Q} \to F_0 \otimes \mathbb{Q})$，其中 $0 \to F_1 \to F_0 \to B \to 0$ 是 $B$ 的自由分解。关键在于，对于任何非零整数 $n$，乘 $n$ 的映射 $ \cdot n: \mathbb{Q} \to \mathbb{Q}$ 是一个同构（其逆是乘 $1/n$）。这意味着张量积函子 $- \otimes \mathbb{Q}$ 保持了单射性，从而使 $\text{Tor}_1(B, \mathbb{Q})$ 为零。因此，对于任意阿贝尔群 $B$（例如 $B=\mathbb{Z}_{13}$），我们有：
$$ \text{Tor}_1(\mathbb{Q}, B) = \{0\} $$
这说明 $\mathbb{Q}$ 是平坦的。一般地，所有**可除群**（divisible group）都是平坦的。[@problem_id:1690149]

#### Tor函子的可加性与应用

Tor函子具有**可加性**，即它与直和交换：
$$ \text{Tor}_1(\bigoplus_i A_i, B) \cong \bigoplus_i \text{Tor}_1(A_i, B) \quad \text{且} \quad \text{Tor}_1(A, \bigoplus_j B_j) \cong \bigoplus_j \text{Tor}_1(A, B_j) $$
这个性质在计算中非常有用。例如，要计算有限阿贝尔群 $A = \mathbb{Z}_{10} \oplus \mathbb{Z}_{15}$ 与模 $\mathbb{Q}/\mathbb{Z}$ 的Tor群，我们可以利用可加性：
$$ \text{Tor}_1(\mathbb{Z}_{10} \oplus \mathbb{Z}_{15}, \mathbb{Q}/\mathbb{Z}) \cong \text{Tor}_1(\mathbb{Z}_{10}, \mathbb{Q}/\mathbb{Z}) \oplus \text{Tor}_1(\mathbb{Z}_{15}, \mathbb{Q}/\mathbb{Z}) $$
对于每一项，我们使用公式 $\text{Tor}_1(\mathbb{Z}_n, G) \cong G[n]$。$\mathbb{Q}/\mathbb{Z}$ 的 $n$-挠子群 $(\mathbb{Q}/\mathbb{Z})[n]$ 正是同构于 $\mathbb{Z}_n$ 的循环群（由 $1/n + \mathbb{Z}$ 生成）。因此：
$$ \text{Tor}_1(\mathbb{Z}_n, \mathbb{Q}/\mathbb{Z}) \cong \mathbb{Z}_n $$
综合起来，我们得到了一个优美的结果：
$$ \text{Tor}_1(\mathbb{Z}_{10} \oplus \mathbb{Z}_{15}, \mathbb{Q}/\mathbb{Z}) \cong \mathbb{Z}_{10} \oplus \mathbb{Z}_{15} $$
这个结论可以推广到任意有限阿贝尔群 $A$：$\text{Tor}_1(A, \mathbb{Q}/\mathbb{Z}) \cong A$ [@problem_id:1690155]。这个同构在庞特里亚金对偶理论中扮演着重要角色。

### Tor函子的模结构

最后，值得一提的是，$\text{Tor}_1^R(A, B)$ 不仅仅是一个抽象的阿贝尔群，它还自然地继承了 $R$-模结构。当 $R$ 是交换环时，对 $r \in R$，其在 $\text{Tor}_1^R(A, B)$ 上的作用，是由它在 $B$ 上的乘法映射 $b \mapsto rb$ 所诱导的链映射在同调层面上产生的。

在 $R=\mathbb{Z}$ 的情况下，这意味着 $\text{Tor}_1(A, B)$ 的阿贝尔群结构是我们之前所讨论的。然而，这个观点在更广的语境下是有益的。例如，考虑 $\text{Tor}_1(\mathbb{Z}_{28}, \mathbb{Z}_{42}) \cong \mathbb{Z}_{14}$ [@problem_id:1690184]。我们知道这是一个14阶循环群。一个整数 $k \in \mathbb{Z}$ 在这个群上的作用就是数乘。例如，如果 $u$ 是生成元，则 $25 \cdot u$ 就是将 $u$ 自身加25次。由于群的阶是14，这个作用等价于 $ (25 \pmod{14}) \cdot u = 11 \cdot u$。这个例子清晰地表明，从模结构的角度来理解，可以为Tor群的内部运算提供一个更代数的框架。

总结而言，Tor函子，特别是 $\text{Tor}_1^{\mathbb{Z}}$，是一个强大而具体的多功能工具。它不仅量化了张量积的非正合性，还揭示了群的挠结构，并为我们提供了计算和联系不同代数对象的系统方法。这些原理和机制将在后续章节中应用于拓扑学，成为我们理解空间同调结构的关键。