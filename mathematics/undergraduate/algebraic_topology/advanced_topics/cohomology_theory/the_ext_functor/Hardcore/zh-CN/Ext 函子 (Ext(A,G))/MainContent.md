## 引言
在现代代数学与拓扑学的交汇处，存在着一系列强大的工具，它们使我们能够探索和量化代数对象的深层结构。其中，**Ext 函子** 扮演着至关重要的角色。作为 Hom 函子的自然延伸，Ext 函子不仅是同调代数的核心概念，更是一种能够揭示模的扩张、同态的阻碍以及拓扑空间内在属性的通用语言。

当我们应用 Hom 函子于一个短正合序列时，我们很快会发现它通常只保持了序列的一部分正合性，即它是“左正合”的。这种不完全性带来了一个根本性的问题：我们如何系统地理解和度量这种“正合性的缺失”？Ext 函子正是为了回答这一问题而生。它通过构造一系列的“导出函子”，将 Hom 函子的非正合性转化为可计算的代数不变量，即 Ext 群。

本文将带领你系统地学习 Ext 函子。在**“原理和机制”**一章中，我们将从其定义出发，通过投射分解构建 Ext 群，并揭示其与模扩张之间深刻的对应关系。在**“应用与跨学科联系”**一章中，我们将走出纯代数的范畴，探索 Ext 函子如何在代数拓扑（通过泛系数定理）和群上同调等领域大放异彩，展示其解决实际问题的强大能力。最后，在**“动手实践”**一章中，你将通过一系列精心设计的练习，将理论知识应用于具体计算，从而真正掌握这一重要工具。

## 原理和机制

在前一章中，我们介绍了同调代数的基本工具，如链复形、同调和正合序列。现在，我们将运用这些工具来构建和理解一个在代数学和拓扑学中都至关重要的对象：**Ext 函子**。`Ext` 函子是 `Hom` 函子的导函子，它精确地量化了 `Hom` 函子在保持序列正合性方面的“失败”程度，并揭示了模的扩张结构。

### Ext 函子的定义：一个同调方法

我们知道，对于一个环 $R$ 上的 $R$-模 $A$ 和 $B$，函子 $\text{Hom}_R(A, -)$ 和 $\text{Hom}_R(-, B)$ 通常只是**左正合**的。这意味着它们能将短正合序列的“左边部分”保持为正合，但通常不能将一个满同态（序列右侧的箭头）映为另一个满同态。`Ext` 函子正是为了弥补这一缺陷而生，它通过构造一个长正合序列来“修复”`Hom` 函子的非正合性。

#### 通过投射分解构建

定义 `Ext` 函子的标准方法是使用**投射分解**。对于任何一个左 $R$-模 $A$，它的一个投射分解是一个由投射模构成的长正合序列，形式如下：
$$ \dots \xrightarrow{d_3} P_2 \xrightarrow{d_2} P_1 \xrightarrow{d_1} P_0 \xrightarrow{\epsilon} A \to 0 $$
其中每个 $P_i$ 都是投射 $R$-模。这个序列在除 $A$ 之外的每个位置都是正合的。

为了计算 `Ext` 群 $\text{Ext}^n_R(A, B)$，我们执行以下三个步骤：

1.  **截断分解**：取 $A$ 的投射分解，并去掉模 $A$ 本身，我们得到一个链复形，通常记作 $P_\bullet$：
    $$ \dots \xrightarrow{d_3} P_2 \xrightarrow{d_2} P_1 \xrightarrow{d_1} P_0 \to 0 $$

2.  **应用 Hom 函子**：将逆变函子 $\text{Hom}_R(-, B)$ 应用于这个链复形。由于函子是逆变的，它会反转所有箭头的方向，从而产生一个**上链复形**：
    $$ 0 \to \text{Hom}_R(P_0, B) \xrightarrow{d_1^*} \text{Hom}_R(P_1, B) \xrightarrow{d_2^*} \text{Hom}_R(P_2, B) \to \dots $$
    这里的上微分算子 $d_n^*$ 是由原先的微分算子 $d_n$ 诱导的，其定义为 $d_n^*(\phi) = \phi \circ d_n$，其中 $\phi: P_{n-1} \to B$ 是一个同态。

3.  **计算上同调**：第 $n$ 个 `Ext` 群，记为 $\text{Ext}^n_R(A, B)$，被定义为这个上链复形的第 $n$ 个上同调群。具体来说：
    $$ \text{Ext}^n_R(A, B) = H^n(\text{Hom}_R(P_\bullet, B)) = \frac{\ker(d_{n+1}^*)}{\text{im}(d_n^*)} $$
    这里我们约定 $d_0^*$ 是从零群出发的零映射。

根据这个定义，$\text{Ext}^1_R(A, B)$ 的具体表达式为：
$$ \text{Ext}^1_R(A, B) = \frac{\ker(d_2^*)}{\text{im}(d_1^*)} $$
其中 $\ker(d_2^*)$ 的元素是从 $P_1$ 到 $B$ 的**上循环**（cocycles），而 $\text{im}(d_1^*)$ 的元素是**上边缘**（coboundaries）。

#### 第零个 Ext 群

一个好的推广应该包含原有的概念。让我们验证一下 $n=0$ 的情况。根据定义：
$$ \text{Ext}^0_R(A, B) = \frac{\ker(d_1^*)}{\text{im}(d_0^*)} = \ker(d_1^*) $$
因为 $\text{im}(d_0^*)$ 是零群。$\ker(d_1^*)$ 包含所有同态 $\phi \in \text{Hom}_R(P_0, B)$，使得 $d_1^*(\phi) = \phi \circ d_1 = 0$。

回顾投射分解的起始部分是正合序列 $P_1 \xrightarrow{d_1} P_0 \xrightarrow{\epsilon} A \to 0$。正合性意味着 $\text{im}(d_1) = \ker(\epsilon)$。因此，条件 $\phi \circ d_1 = 0$ 等价于 $\phi$ 在 $\ker(\epsilon)$ 上为零。根据万有性质（具体地，商模的万有性质），一个定义在 $P_0$ 上的同态 $\phi$ 在 $\ker(\epsilon)$ 上为零，当且仅当它可以通过商映射 $\epsilon$ 进行分解。也就是说，存在一个唯一的同态 $g: A \to B$ 使得 $\phi = g \circ \epsilon$。

这个分解建立了一个 $\ker(d_1^*)$ 与 $\text{Hom}_R(A, B)$ 之间的一一对应。这个对应关系是自然的，并且是一个群同构。因此，我们得到了一个基本结论：
$$ \text{Ext}^0_R(A, B) \cong \text{Hom}_R(A, B) $$
这表明 `Ext` 函子确实是 `Hom` 函子的一个自然延伸。

值得注意的是，我们也可以通过对第二个变量 $B$ 取**内射分解**，然后应用协变函子 $\text{Hom}_R(A, -)$ 来定义 `Ext` 群。一个被称为同调代数基本定理的深刻结果保证了这两种方法（以及其他方法）计算出的 `Ext` 群是同构的，这证明了 `Ext` 函子的内在性和稳健性。

### 基本性质与模的刻画

`Ext` 函子，特别是 $\text{Ext}^1$，为我们提供了一种强大的语言来刻画模的重要性质。

#### Ext 与投射模和内射模

投射模和内射模的定义本质上是关于同态的提升和扩张性质。这些性质可以被 `Ext` 函子的消失性完美地捕捉。

一个 $R$-模 $P$ 是**投射模**，当且仅当对于任何模 $M$，都有 $\text{Ext}^1_R(P, M) = 0$。这是因为如果 $P$ 是投射的，我们可以取一个极短的投射分解 $0 \to 0 \to P \xrightarrow{\text{id}} P \to 0$。应用 $\text{Hom}_R(-, M)$ 函子后得到的上链复形是平凡的，其上同调群（除了零阶）自然为零。反之，若 $\text{Ext}^1_R(P, M)=0$ 对所有 $M$ 成立，则表明函子 $\text{Hom}_R(P, -)$ 是正合的，这正是投射模的一个等价定义。

例如，考虑环 $R = \mathbb{Z}/4\mathbb{Z}$。$R$ 本身作为 $R$-模是自由的，因此是投射的。所以对于任何 $R$-模 $M$，我们必然有 $\text{Ext}^1_R(R, M) = 0$。这个性质并不依赖于 $M$ 的具体结构。

与此对偶地，一个 $R$-模 $I$ 是**内射模**，当且仅当对于任何模 $M$，都有 $\text{Ext}^1_R(M, I) = 0$。这个结论源于以下事实：$I$ 是内射的等价于逆变函子 $\text{Hom}_R(-, I)$ 是一个正合函子。一个函子是正合的，当且仅当它所有的（高阶）导函子都为零。由于 $\text{Ext}^n_R(-, I)$ 是 $\text{Hom}_R(-, I)$ 的右导函子，所以 $\text{Ext}^1_R(M, I)$ 对所有 $M$ 为零正是 $I$ 是内射模的标志。

因此，$\text{Ext}^1$ 可以被视为衡量一个模“非投射”或“非内射”程度的标尺。

### 核心诠释：Ext¹ 与模扩张

虽然 `Ext` 的定义看似抽象，但 $\text{Ext}^1$ 有一个非常具体和直观的解释：它对模的**扩张**进行分类。

一个形如 $0 \to A \to B \to C \to 0$ 的短正合序列被称为 **$C$ by $A$ 的一个扩张**（an extension of $C$ by $A$）。这意味着 $A$ 同构于 $B$ 的一个子模，并且 $C$ 同构于商模 $B/A$。

如果存在同态 $\beta: B_1 \to B_2$ 使得图表
$$
\begin{array}{ccccccccc}
0  \to  A  \xrightarrow{i_1}  B_1  \xrightarrow{p_1}  C  \to  0 \\
  \downarrow\text{id}_A   \downarrow\beta   \downarrow\text{id}_C   \\
0  \to  A  \xrightarrow{i_2}  B_2  \xrightarrow{p_2}  C  \to  0
\end{array}
$$
交换，我们就称两个扩张 $E_1$ 和 $E_2$ 是**等价的**。这样的 $\beta$ 必定是一个同构。

核心结论是：群 $\text{Ext}^1_R(C, A)$ 的元素与 $C$ by $A$ 的扩张的等价类之间存在一个一一对应关系。

#### 扩张的群结构：贝尔和 (Baer Sum)

更进一步，这个等价类的集合并非只是一个集合，它构成了一个阿贝尔群。群的加法运算被称为**贝尔和**。给定两个扩张 $[E_1]$ 和 $[E_2]$，它们的和 $[E_1] + [E_2]$ 通过一个包含“拉回”和“推出”的两步构造过程来定义。

这个群的**单位元**是什么？它正是**可裂项短正合序列** $0 \to A \to A \oplus C \to C \to 0$ 所代表的等价类。一个扩张是可裂的，意味着中间项 $B$ 同构于两端项的直和 $A \oplus C$。因此，$\text{Ext}^1_R(C, A) = 0$ 当且仅当所有 $C$ by $A$ 的扩张都是可裂的。这再次印证了 `Ext` 作为衡量“非正合性”或“不可裂性”的度量。

#### 从扩张到上循环

为了使这种对应关系更加具体，我们需要一个程序，能将一个给定的扩张映射到 $\text{Ext}^1_R(C, A)$ 中的一个元素。这个过程如下：

1.  取 $C$ 的一个投射分解，例如 $P_1 \xrightarrow{d_1} P_0 \xrightarrow{\epsilon} C \to 0$。
2.  考虑给定的扩张 $0 \to A \xrightarrow{i} B \xrightarrow{p} C \to 0$。
3.  由于 $P_0$ 是投射的而 $p$ 是满射，我们可以将映射 $\epsilon: P_0 \to C$ **提升**为一个映射 $s_0: P_0 \to B$，使得 $p \circ s_0 = \epsilon$。
4.  现在考察复合映射 $s_0 \circ d_1: P_1 \to B$。通过简单的图表追踪可以发现，这个映射的像落在 $\ker(p)$ 中，而根据正合性，$\ker(p) = \text{im}(i)$。
5.  由于 $i$ 是单射，存在一个唯一的映射 $\alpha: P_1 \to A$ 使得 $i \circ \alpha = s_0 \circ d_1$。
6.  可以证明这个 $\alpha$ 是一个 1-上循环，即 $\alpha \in \ker(d_2^*)$。它在上同调群 $\text{Ext}^1_R(C, A)$ 中所代表的类 $[\alpha]$ 就是对应于该扩张的元素。

例如，考虑阿贝尔群（即 $\mathbb{Z}$-模）的扩张 $0 \to \mathbb{Z}/4\mathbb{Z} \xrightarrow{i} \mathbb{Z}/24\mathbb{Z} \xrightarrow{p} \mathbb{Z}/6\mathbb{Z} \to 0$，其中 $i(k) = 6k$，$p$ 是模 6 的投影。取 $\mathbb{Z}/6\mathbb{Z}$ 的标准自由分解 $0 \to \mathbb{Z} \xrightarrow{\times 6} \mathbb{Z} \to \mathbb{Z}/6\mathbb{Z} \to 0$。通过上述步骤，可以计算出代表这个扩张的 1-上循环 $\alpha: \mathbb{Z} \to \mathbb{Z}/4\mathbb{Z}$ 满足 $\alpha(1) = 1 \in \mathbb{Z}/4\mathbb{Z}$。

#### 零元与上边缘

相应地，作为群单位元的可裂扩张，其对应的上循环必须是一个上边缘，即 `Ext` 群中的零元。

考虑可裂扩张 $0 \to A \xrightarrow{i} A \oplus C \xrightarrow{p} C \to 0$。如果我们按照上述流程计算其对应的上循环 $\alpha$，我们会发现这个 $\alpha$ 总能被写作 $\alpha = \phi \circ d_1 = d_1^*(\phi)$ 的形式，其中 $\phi$ 是一个从 $P_0$ 到 $A$ 的同态。这正是说 $\alpha$ 是一个上边缘，因此它在商群 $\ker(d_2^*)/\text{im}(d_1^*)$ 中代表零元。这个过程明确地将群论中的单位元（可裂扩张）与同调代数中的零元（上边缘）联系起来。

### Ext 的长正合序列

`Ext` 函子最有力的应用之一来自于它们自然形成的长正合序列。

给定任意一个短正合序列 $0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0$ 和另一个模 $G$，将逆变函子 $\text{Hom}_R(-, G)$ 应用于它，我们得到一个（通常不完整的）正合序列。`Ext` 函子可以将其“无缝”地延展成一个**长正合序列**：
$$
\begin{align*}
0  \to \text{Hom}_R(C, G) \xrightarrow{g^*} \text{Hom}_R(B, G) \xrightarrow{f^*} \text{Hom}_R(A, G) \\
 \xrightarrow{\delta} \text{Ext}^1_R(C, G) \to \text{Ext}^1_R(B, G) \to \text{Ext}^1_R(A, G) \\
 \xrightarrow{\delta} \text{Ext}^2_R(C, G) \to \dots
\end{align*}
$$
这个序列在理论和计算中都极为重要。

#### 连接同态 $\delta$

这个长序列的关键是**连接同态** $\delta: \text{Hom}_R(A, G) \to \text{Ext}^1_R(C, G)$。它将不同阶数的上同调群联系起来。$\delta$ 的构造是一个典型的“图表追踪”或“蛇形引理”的应用。

给定一个同态 $\phi \in \text{Hom}_R(A, G)$，我们通过以下方式构造 $\delta(\phi)$：
1.  取 $C$ 的投射分解 $P_1 \to P_0 \to C \to 0$。
2.  利用 $P_0$ 的投射性和 $g: B \to C$ 的满射性，存在一个提升 $\beta: P_0 \to B$ 使得 $g \circ \beta = \epsilon$。
3.  通过一系列的图表追踪，我们构造出一个 1-上循环 $\psi: P_1 \to G$。
4.  $\delta(\phi)$ 就被定义为这个上循环 $\psi$ 在 $\text{Ext}^1_R(C, G)$ 中所代表的类。

#### 应用：提升的阻碍

长正合序列的精妙之处在于它揭示了深刻的结构性信息。序列在 $\text{Hom}_R(A, G)$ 处的正合性意味着 $\text{im}(f^*) = \ker(\delta)$。

回忆一下，$f^*: \text{Hom}_R(B, G) \to \text{Hom}_R(A, G)$ 的定义是 $f^*(\psi) = \psi \circ f$。因此，一个同态 $\phi \in \text{Hom}_R(A, G)$ 位于 $\text{im}(f^*)$ 中，当且仅当存在一个 $\psi: B \to G$ 使得 $\phi = \psi \circ f$。这种情况我们称 $\phi$ 可以**提升**（或扩张）到 $B$。

于是，正合性条件 $\text{im}(f^*) = \ker(\delta)$ 告诉我们：
> 一个同态 $\phi: A \to G$ 可以被提升到 $B$，当且仅当 $\delta(\phi) = 0$。

换句话说，$\delta(\phi) \in \text{Ext}^1_R(C, G)$ 是 $\phi$ 无法被提升的**阻碍**。如果这个阻碍非零，提升就不可能。

一个经典的例子可以阐明这一点。考虑 $\mathbb{Z}$-模的短正合序列 $0 \to \mathbb{Z} \xrightarrow{\times 2} \mathbb{Z} \xrightarrow{\text{proj}} \mathbb{Z}/2\mathbb{Z} \to 0$。让 $G = \mathbb{Z}/2\mathbb{Z}$。我们问：哪些同态 $\phi: \mathbb{Z} \to \mathbb{Z}/2\mathbb{Z}$ 可以提升到中间的 $\mathbb{Z}$？
一个同态 $\phi$ 若能提升，则 $\phi = \psi \circ (\times 2)$。但对于任何 $\psi: \mathbb{Z} \to \mathbb{Z}/2\mathbb{Z}$，其在偶数上的取值 $\psi(2n) = 2\psi(n) = 0$。这意味着只有零同态可以被提升。非零同态 $\phi_1(n) = n \pmod 2$ 就无法提升。
根据我们的理论，这意味着 $\delta(\phi_1)$ 必定是 $\text{Ext}^1_{\mathbb{Z}}(\mathbb{Z}/2\mathbb{Z}, \mathbb{Z}/2\mathbb{Z})$ 中的一个非零元素。事实上，可以计算出 $\text{Ext}^1_{\mathbb{Z}}(\mathbb{Z}/2\mathbb{Z}, \mathbb{Z}/2\mathbb{Z}) \cong \mathbb{Z}/2\mathbb{Z}$。这个非零元就对应着唯一的非可裂扩张 $0 \to \mathbb{Z}/2\mathbb{Z} \to \mathbb{Z}/4\mathbb{Z} \to \mathbb{Z}/2\mathbb{Z} \to 0$。这个例子完美地将提升问题、连接同态和非可裂扩张联系在了一起。

### 高阶 Ext 群与 Yoneda 积

`Ext` 的理论不止于 $\text{Ext}^1$。$\text{Ext}^n_R(C, A)$ 对所有的 $n \ge 1$ 都有类似的解释，它们分类了所谓的 **$n$-扩张**，即形如 $0 \to A \to M_{n-1} \to \dots \to M_0 \to C \to 0$ 的长正合序列。

不同阶数的 `Ext` 群之间也存在代数结构，其中最重要的是 **Yoneda 积**。它提供了一个配对：
$$ \text{Ext}^m_R(C, B) \times \text{Ext}^n_R(B, A) \to \text{Ext}^{m+n}_R(C, A) $$
这个乘积的本质是“拼接”扩张。例如，我们可以将一个代表 $[e_B] \in \text{Ext}^1_R(C, B)$ 的 1-扩张
$$ e_B: 0 \to B \xrightarrow{i} E \xrightarrow{p} C \to 0 $$
和一个代表 $[e_A] \in \text{Ext}^1_R(B, A)$ 的 1-扩张
$$ e_A: 0 \to A \xrightarrow{j} F \xrightarrow{q} B \to 0 $$
拼接起来，得到一个代表 Yoneda 积 $[e_B] \circ [e_A] \in \text{Ext}^2_R(C, A)$ 的 2-扩张。

这个拼接过程是通过将第一个扩张的满射 $q$ 与第二个扩张的单射 $i$ 复合起来完成的，形成一个映射 $i \circ q: F \to E$。这会产生一个新的、更长的序列：
$$ 0 \to A \xrightarrow{j} F \xrightarrow{i \circ q} E \xrightarrow{p} C \to 0 $$
通过逐项检查，可以验证这个构造出的序列确实是一个正合序列，即一个 2-扩张。这为我们提供了一种理解和构造高阶 `Ext` 群元素的具体方法，展示了 `Ext` 群之间丰富的代数结构。

总而言之，`Ext` 函子从一个用于“校正”`Hom` 函子非正合性的抽象工具出发，最终发展成为描述模扩张、刻画模基本性质以及揭示同态提升阻碍的强大理论。它在代数几何、代数拓扑和表示论等众多领域都扮演着核心角色。