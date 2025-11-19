## 引言
同调代数是现代数学的一个核心分支，它提供了一套强大的代数工具来研究不同数学领域中的“结构”。这门学科最初起源于拓扑学，旨在用代数[不变量](@entry_id:148850)（如同调群）来区分和分类几何空间。然而，其思想的深刻性和方法的普适性很快使其超越了最初的背景，成为一门研究“[代数结构](@entry_id:137052)中的结构”的[元理论](@entry_id:638043)。在许多数学分支中，我们常常遇到一些不“完美”的代数过程。例如，一个映射可能不是[单射](@entry_id:183792)或满射，一个序列可能不完全正合。同调代数的核心问题，便是如何系统地度量、理解并利用这些“不完美性”。它将核、像、正合性等基本概念置于一个更广阔的框架中，从而揭示出隐藏在表象之下的深刻联系。

本文将引导你逐步进入同调代数的世界。在第一章“原理与机制”中，我们将建立这门学科的基础，从核心的[链复形](@entry_id:150246)与同调群出发，学习[长正合序列](@entry_id:153438)这一基本工具，并最终接触到用于度量非正合性的[导出函子](@entry_id:156814)。第二章“应用与[交叉](@entry_id:147634)学科联系”将展示这些抽象工具的威力，看它们如何在代数拓扑、[模论](@entry_id:139410)、群论乃至数论等领域中被用来解决具体问题，将几何直觉转化为代数计算。最后，在“动手实践”部分，你将有机会通过解决一系列精心设计的问题，来巩固所学概念，将理论知识转化为实践能力。

## 原理与机制

在介绍性章节之后，我们现在深入探讨同调代数的核心概念和基本机制。本章将系统地建立同调代数的基础，从[链复形](@entry_id:150246)和同调群的定义，到作为学科基石的长正合序列，再到衡量函子非正合性的[导出函子](@entry_id:156814)。这些工具共同构成了一个强大的框架，用于研究不同数学领域中的深刻结构。

### 链、圈与洞：[链复形](@entry_id:150246)与同调

同调代数的研究始于一个核心[代数结构](@entry_id:137052)：**[链复形](@entry_id:150246) (chain complex)**。抽象地说，一个[链复形](@entry_id:150246) $(C_\bullet, d_\bullet)$ 是一个由阿贝尔群（或更一般地，环 $R$ 上的模）构成的序列 $\{C_n\}_{n \in \mathbb{Z}}$，并配以一系列称为**[边界映射](@entry_id:151165) (boundary maps)** 或**[微分](@entry_id:158718) (differentials)** 的同态 $d_n: C_n \to C_{n-1}$。这些映射必须满足一个关键条件：任意两个[连续映射](@entry_id:153855)的复合为零，即 $d_{n-1} \circ d_n = 0$ 对所有整数 $n$ 成立。

这个条件 $d^2 = 0$ 意义重大。它告诉我们，一个元素的边界的边界必定是零。从[集合论](@entry_id:137783)的角度看，这意味着第 $n$ 个映射的像 $\operatorname{im}(d_n)$ 总是包含在第 $n-1$ 个映射的核 $\ker(d_{n-1})$ 之中。

为了具体理解这个定义，让我们看一个基于[向量空间的例子](@entry_id:203231)。考虑一个分次[向量空间](@entry_id:151108) $C_* = C_2 \oplus C_1 \oplus C_0$，其中每个分量都有给定的基。我们定义一度为 $-1$ 的线性映射 $d: C_* \to C_*$，它由分量映射 $d_2: C_2 \to C_1$ 和 $d_1: C_1 \to C_0$ 构成。为了使 $(C_*, d)$ 成为一个[链复形](@entry_id:150246)，唯一的非平凡条件是复合映射 $d_1 \circ d_2: C_2 \to C_0$ 必须是零映射。这意味着对于 $C_2$ 的任何[基向量](@entry_id:199546) $e$，我们都必须有 $d_1(d_2(e)) = 0$。通过将 $d_1$ 和 $d_2$ 的作用表示为矩阵，这个条件就转化为一系列关于映射定义中参数的[线性方程](@entry_id:151487)。例如，在问题 [@problem_id:1805744] 中，通过求解这些方程，我们可以确定使 $d \circ d = 0$ 成立的唯一参数值，从而构造出一个合法的[链复形](@entry_id:150246)。

有了[链复形](@entry_id:150246)，我们便可以定义其**同调群 (homology group)**。对于每个维度 $n$，我们有两个特殊的[子群](@entry_id:146164)：
- **$n$-圈 (cycles)** 的群，记为 $Z_n(C) = \ker(d_n)$。这些是经 $d_n$ 映射后变为零的元素。
- **$n$-边界 (boundaries)** 的群，记为 $B_n(C) = \operatorname{im}(d_{n+1})$。这些是来自更高维度的元素的像。

$d^2=0$ 的条件保证了 $B_n(C) \subseteq Z_n(C)$，即每个边界都是一个圈。这引发了一个自然的问题：是否存在不是边界的圈？同调群正是为了度量这种差异而生。第 $n$ 个同调群 $H_n(C)$ 定义为圈群对边界群的商群：
$$ H_n(C) = Z_n(C) / B_n(C) = \ker(d_n) / \operatorname{im}(d_{n+1}) $$
直观上，同调群计算的是[链复形](@entry_id:150246)在维度 $n$ 的“洞”的数量。一个非零的同调类 $[z] \in H_n(C)$ 对应一个圈 $z$，它自身不是任何更高维元素的边界。

这个看似抽象的定义实际上是对我们熟悉的代数概念的推广。考虑任意一个[模同态](@entry_id:148144) $f: M \to N$。我们可以将其视为一个只在维度 1 和 0 非零的[链复形](@entry_id:150246) $C_\bullet$：
$$ \dots \to 0 \to C_1 = M \xrightarrow{d_1=f} C_0 = N \to 0 \to \dots $$
其中所有其他[微分](@entry_id:158718)都是零映射。现在我们来计算它的同调群 [@problem_id:1805707]：
- **一阶同调 $H_1(C)$**: 定义为 $\ker(d_1) / \operatorname{im}(d_2)$。这里 $d_1 = f$，而 $d_2: C_2 \to C_1$ 是零映射，所以 $\operatorname{im}(d_2) = \{0\}$。因此，$H_1(C) = \ker(f) / \{0\} \cong \ker(f)$。
- **[零阶同调](@entry_id:269016) $H_0(C)$**: 定义为 $\ker(d_0) / \operatorname{im}(d_1)$。这里 $d_0: C_0 \to C_{-1}$ 是零映射，所以 $\ker(d_0) = C_0 = N$。而 $\operatorname{im}(d_1) = \operatorname{im}(f)$。因此，$H_0(C) = N / \operatorname{im}(f) = \operatorname{coker}(f)$，即 $f$ 的**余核 (cokernel)**。

这个例子揭示了一个深刻的联系：同调论将核与余核这两个基本概念统一到一个更广阔的框架中。$H_1$ 衡量了映射的非[单射性](@entry_id:147722)，而 $H_0$ 衡量了其非满射性。

### 关联复形：[链映射](@entry_id:268209)与[正合序列](@entry_id:151503)

一旦我们有了研究对象（[链复形](@entry_id:150246)），就需要工具来比较它们。**[链映射](@entry_id:268209) (chain map)** $f_\bullet: C_\bullet \to D_\bullet$ 正是这样的工具。它是一族同态 $f_n: C_n \to D_n$，与[链复形](@entry_id:150246)的[边界映射](@entry_id:151165)“交换”，即满足如下[交换图](@entry_id:747516)对所有 $n$ 成立：$f_{n-1} \circ d_n^C = d_n^D \circ f_n$。

[链映射](@entry_id:268209)最重要的性质是它们能够在同调层面引发映射。一个[链映射](@entry_id:268209) $f_\bullet$ 将圈映为圈，将边界映为边界，因此它自然地导出一个同调群上的同态 $f_*: H_n(C) \to H_n(D)$，定义为 $f_*([z]) = [f_n(z)]$。这个过程是良定义的，因为它保持了等价关系。例如，在 [@problem_id:1805749] 中，我们考虑一个由乘以整数 $k$ 定义的自[链映射](@entry_id:268209) $f_\bullet: C_\bullet \to C_\bullet$。通过计算可以发现，它在[零阶同调](@entry_id:269016)上引发的映射 $f_{*,0}$ 同样是乘以整数 $k$。这直观地表明，同调群不仅是群，而且其上的诱导映射也保留了原始[链映射](@entry_id:268209)的[代数结构](@entry_id:137052)。

另一个基本概念是**[正合序列](@entry_id:151503) (exact sequence)**。一个模与同态的序列 $\dots \to A \xrightarrow{f} B \xrightarrow{g} C \to \dots$ 被称为在 $B$ 处**正合 (exact)**，如果 $\operatorname{im}(f) = \ker(g)$。一个序列如果在每个位置都正合，则称为[正合序列](@entry_id:151503)。这个看似简单的条件具有强大的[约束力](@entry_id:170052)。例如，考虑一个具体序列 $\mathbb{R}^{1} \xrightarrow{S} \mathbb{R}^{3} \xrightarrow{T} \mathbb{R}^{2}$，其中 $S$ 和 $T$ 由矩阵 $A$ 和 $B$ 表示。要使序列在 $\mathbb{R}^3$ 处正合，我们需要满足两个条件：首先，$\operatorname{im}(S)$ 必须包含在 $\ker(T)$ 中，这意味着 $B$ 乘以 $A$ 的列向量结果为[零向量](@entry_id:156189)；其次，这两个[子空间](@entry_id:150286)的维度必须相等，即 $\dim(\operatorname{im}(S)) = \dim(\ker(T))$。在问题 [@problem_id:1805722] 中，这些条件共同确定了矩阵 $B$ 中一个未知参数的唯一值。

特别重要的一类[正合序列](@entry_id:151503)是**短[正合序列](@entry_id:151503) (short exact sequence)**，其形式为 $0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0$。这里的正合性意味着 $f$ 是单射， $g$ 是满射，且 $\operatorname{im}(f) = \ker(g)$。短[正合序列](@entry_id:151503)在代数中无处不在，它们将模 $B$ 分解为其子模 $A$ (通过 $f$) 和[商模](@entry_id:155903) $C$ (通过 $g$)。

### 从短到长：同调的长正合序列

同调代数最强大和最基本的工具之一，是将短[正合序列](@entry_id:151503)转化为长正合序列的能力。**长正合序列基本定理**指出，如果 $0 \to A_\bullet \xrightarrow{f_\bullet} B_\bullet \xrightarrow{g_\bullet} C_\bullet \to 0$ 是一个[链复形](@entry_id:150246)的短[正合序列](@entry_id:151503)，那么它会诱导出一个同调群的**[长正合序列](@entry_id:153438) (long exact sequence)**：
$$ \dots \to H_n(A) \xrightarrow{f_*} H_n(B) \xrightarrow{g_*} H_n(C) \xrightarrow{\partial} H_{n-1}(A) \to H_{n-1}(B) \to \dots $$
这个序列是无穷的，并且在每个位置都是正合的。其中 $f_*$ 和 $g_*$ 是由[链映射](@entry_id:268209) $f_\bullet$ 和 $g_\bullet$ 诱导的自然同态。序列中真正的新结构是**[连接同态](@entry_id:160713) (connecting homomorphism)** $\partial: H_n(C) \to H_{n-1}(A)$。它将一个 $n$ 维的“洞”与一个 $(n-1)$ 维的“洞”联系起来，其构造过程被称为“[图追踪](@entry_id:263851)法”(diagram chasing)：

1.  取 $H_n(C)$ 中的一个同调类 $[z]$，其代表元为 $z \in \ker(d_n^C)$。
2.  由于 $g_n$ 是满射，存在 $b \in B_n$ 使得 $g_n(b) = z$。这个 $b$ 是 $z$ 的一个“提升”。
3.  将 $b$ 通过 $B_\bullet$ 的[微分](@entry_id:158718)映射到 $d_n^B(b) \in B_{n-1}$。通过[交换图](@entry_id:747516)的性质可以证明 $g_{n-1}(d_n^B(b)) = 0$，因此 $d_n^B(b) \in \ker(g_{n-1})$。
4.  根据序列在 $B_{n-1}$ 处的正合性，$\ker(g_{n-1}) = \operatorname{im}(f_{n-1})$。因此，存在唯一的 $a \in A_{n-1}$ 使得 $f_{n-1}(a) = d_n^B(b)$。
5.  可以证明这个 $a$ 是一个圈，即 $a \in \ker(d_{n-1}^A)$。我们定义 $\partial([z]) = [a] \in H_{n-1}(A)$。

尽管这个构造过程涉及选择，但最终的同调类 $[a]$ 是良定义的，不依赖于 $z$ 的提升 $b$ 的具体选择。问题 [@problem_id:1805711] 提供了一个计算[连接同态](@entry_id:160713)的绝佳实例。通过追踪一个具体的同调类，我们可以显式地计算出它在[连接同态](@entry_id:160713)下的像。

[长正合序列](@entry_id:153438)的一个关键特性是其**自然性 (naturality)**。如果存在两个[链复形](@entry_id:150246)的短[正合序列](@entry_id:151503)，并且它们通过一系列[链映射](@entry_id:268209)（构成一个[交换图](@entry_id:747516)）联系起来，那么它们各自诱导的[长正合序列](@entry_id:153438)也会通过诱导映射构成一个“交换梯形图”。这意味着，先走“横向”的[连接同态](@entry_id:160713)，再走“纵向”的诱导映射，其结果与先走“纵向”再走“横向”是相同的。问题 [@problem_id:1805711] 中的计算 $\alpha_*(\partial([z]))$ 正是这一深刻原理的具体体现。

作为[长正合序列](@entry_id:153438)理论的一个直接且重要的推论，**[蛇引理](@entry_id:152840) (Snake Lemma)** 提供了一个连接垂直映射的核与余核的工具。给定一个行皆正合的模[交换图](@entry_id:747516)，如 [@problem_id:1805706] 的设置，[蛇引理](@entry_id:152840)构造了一个包含六项的[正合序列](@entry_id:151503)：
$$ \ker(\alpha) \to \ker(\beta) \to \ker(\gamma) \xrightarrow{\delta} \operatorname{coker}(\alpha) \to \operatorname{coker}(\beta) \to \operatorname{coker}(\gamma) $$
这个引理的名字来源于其在[图追踪](@entry_id:263851)证明中出现的蛇形路径。它为我们提供了一种系统的方式来理解映射之间的相互关系。例如，在 [@problem_id:1805706] 中，虽然可以直接通过交换性计算 $\gamma$ 的核，但[蛇引理](@entry_id:152840)提供了一个更概念化的视角，将 $\ker(\gamma)$ 嵌入到一个更大的结构中。

### 函子与[导出函子](@entry_id:156814)：度量非正合性

同调代数的许多应用都涉及研究函子如何作用于模的范畴。两个最重要的[函子](@entry_id:150427)是 **Hom 函子** $\operatorname{Hom}_R(M, -)$ 和**[张量积](@entry_id:140694)[函子](@entry_id:150427) (tensor product functor)** $- \otimes_R M$。然而，这些函子通常不是“完美”的。当它们作用于一个短[正合序列](@entry_id:151503) $0 \to A \to B \to C \to 0$ 时，得到的序列通常不再是短正合的。

具体来说，$\operatorname{Hom}_R(M, -)$ 是**左正合的 (left-exact)**。这意味着对于任何短[正合序列](@entry_id:151503)，序列
$$ 0 \to \operatorname{Hom}_R(M, A) \to \operatorname{Hom}_R(M, B) \to \operatorname{Hom}_R(M, C) $$
是正合的。但最后的映射 $\operatorname{Hom}_R(M, B) \to \operatorname{Hom}_R(M, C)$ 通常不是满射。
反之，$- \otimes_R M$ 是**右正合的 (right-exact)**。作用于短[正合序列](@entry_id:151503)后，序列
$$ A \otimes_R M \to B \otimes_R M \to C \otimes_R M \to 0 $$
是正合的。但最左边的映射 $A \otimes_R M \to B \otimes_R M$ 通常不是单射。问题 [@problem_id:1805767] 中，将[函子](@entry_id:150427) $- \otimes_{\mathbb{Z}} (\mathbb{Z}/2\mathbb{Z})$ 应用于短[正合序列](@entry_id:151503) $0 \to \mathbb{Z} \xrightarrow{\times 2} \mathbb{Z} \to \mathbb{Z}/2\mathbb{Z} \to 0$，我们发现得到的序列在左端不再正合，因为原先的[单射](@entry_id:183792)变成了零映射。

**[导出函子](@entry_id:156814) (derived functors)** 的思想应运而生，它们正是为了“修复”和“度量”这种非正合性而设计的。
- 对于左正合函子 $F$（如 $\operatorname{Hom}(M,-)$），我们定义其**右[导出函子](@entry_id:156814) (right derived functors)** $R^n F$。这些函子构成了**Ext 群** $\operatorname{Ext}_R^n(M, -)$。
- 对于右正合[函子](@entry_id:150427) $F$（如 $- \otimes M$），我们定义其**左[导出函子](@entry_id:156814) (left derived functors)** $L_n F$。这些函子构成了**Tor 群** $\operatorname{Tor}_R^n(-, M)$。

计算这些[导出函子](@entry_id:156814)的标准方法是使用**投射分解 (projective resolution)** 或**[内射分解](@entry_id:156320) (injective resolution)**。例如，为了计算 $R^n F(A)$，我们首先找到 $A$ 的一个[内射分解](@entry_id:156320)（一个由[内射模](@entry_id:154413)构成的[长正合序列](@entry_id:153438)），然后将函子 $F$ 应用于这个分解（去掉 $A$），最后计算所得上[链复形](@entry_id:150246)的[上同调](@entry_id:160558)。

一个基本结果是，第零个[导出函子](@entry_id:156814)与原始[函子](@entry_id:150427)是自然同构的。即 $R^0 F \cong F$ 和 $L_0 F \cong F$。问题 [@problem_id:1805746] 验证了这一点。通过使用 $\mathbb{Z}_m$ 的一个[内射分解](@entry_id:156320)来计算 $\operatorname{Ext}^0(\mathbb{Z}_n, \mathbb{Z}_m)$，我们最终发现它同构于 $\operatorname{Hom}(\mathbb{Z}_n, \mathbb{Z}_m)$，这正是 $F=\operatorname{Hom}(\mathbb{Z}_n, -)$ 应用于 $\mathbb{Z}_m$ 的结果。

那么，何时一个函子是完全**正合 (exact)** 的（既左正合又右正合）？对于 Hom 函子，这与**投射模 (projective module)** 的概念紧密相连。一个模 $P$ 是投射的，当且仅当函子 $\operatorname{Hom}_R(P, -)$ 是正合的。如 [@problem_id:1805728] 所示，投射模的“[提升性质](@entry_id:156717)”恰好保证了 $\operatorname{Hom}_R(P, B) \to \operatorname{Hom}_R(P, C)$ 的满射性，从而使 $\operatorname{Hom}_R(P, -)$ 成为一个正合函子。类似地，**[平坦模](@entry_id:153965) (flat module)** $M$ 定义为使 $- \otimes_R M$ 成为正合函子的模。

这引出了[导出函子](@entry_id:156814)的核心哲学：**高阶[导出函子](@entry_id:156814) ($n \ge 1$) 度量了函子偏离正合性的程度。** 如果一个函子本身就是正合的，那么它不需要任何“修复”，其所有高阶[导出函子](@entry_id:156814)都必然是零。问题 [@problem_id:1805723] 完美地说明了这一点。[函子](@entry_id:150427) $F(A) = A \otimes_{\mathbb{Z}} \mathbb{Q}$ 是一个正合函子（因为 $\mathbb{Q}$ 是一个平坦 $\mathbb{Z}$-模）。因此，它的所有高阶左[导出函子](@entry_id:156814) $L_n F(M) = \operatorname{Tor}_n^{\mathbb{Z}}(M, \mathbb{Q})$ 对于 $n \ge 1$ 都必须为零。计算 $L_1 F(\mathbb{Z}/12\mathbb{Z})$ 的结果为零，正是这个普遍原理的一个具体实例。

通过本章的学习，我们已经建立了同调代数的基本词汇和语法。[链复形](@entry_id:150246)、同调、[正合序列](@entry_id:151503)和[导出函子](@entry_id:156814)这些概念共同构成了一个强大的理论框架，我们将在后续章节中应用它们来解决更复杂的问题。