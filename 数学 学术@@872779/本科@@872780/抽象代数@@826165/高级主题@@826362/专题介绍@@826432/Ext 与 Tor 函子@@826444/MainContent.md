## 引言
在现代[抽象代数](@entry_id:145216)的宏伟殿堂中，Ext 和 Tor [函子](@entry_id:150427)是同调代数领域的两大基石。它们为[代数结构](@entry_id:137052)的研究提供了超越经典[模论](@entry_id:139410)的深刻视角和强大工具。这些[函子](@entry_id:150427)源于一个基本问题：在代数运算中，我们习以为常的工具，如取同态群（Hom）和张量积（⊗），在多大程度上“保持”了结构的精确性？当它们不保持时，我们又该如何精确地量化和理解这种“损失”？Ext 和 Tor 函子正是对这个问题的系统性回答。

本文将带领读者踏上一段探索 Ext 和 Tor [函子](@entry_id:150427)的旅程。我们将从它们的起源动机开始，逐步揭示其严谨的数学构造，并最终领略它们在纯数学多个前沿领域的广泛应用。

- 在第一章**“原理与机制”**中，我们将深入探讨 Ext 和 Tor 函子的形式化定义。通过投射分解和[导出函子](@entry_id:156814)的概念，我们将理解这些抽象工具是如何从基本的 Hom 和张量积函子中“导出”的，并掌握它们的核心性质与计算方法。

- 在第二章**“应用与交叉学科联系”**中，我们将展示这些函子的威力。您将看到它们如何作为“诊断工具”，用于刻画模的平坦性、可除性和挠性，并如何在[交换代数](@entry_id:149047)、代数拓扑、群论乃至数论中建立起令人惊叹的深刻联系。

- 最后，在**“动手实践”**部分，我们将通过一系列精心设计的计算问题，引导您亲手操作，将理论知识转化为解决具体问题的能力，从而真正内化对 Ext 和 Tor 函子的理解。

通过本次学习，您将不仅掌握两个重要的代数[不变量](@entry_id:148850)，更将体会到同调代数思想如何用统一的语言揭示不同数学领域之间内在的结构性真理。

## 原理与机制

在介绍性章节之后，我们现在深入探讨 Ext 和 Tor [函子](@entry_id:150427)的核心原理与机制。这些函子是同调代数中的基本工具，为我们提供了超越经典模理论的深刻视角。它们不仅量化了某些代数运算（如取同态群和张量积）的“不精确性”，还在模的结构分类和代数拓扑等领域发挥着关键作用。本章将系统地阐述它们的定义、基本性质以及计算方法。

### [函子](@entry_id:150427)的非正合性：Ext 与 Tor 的动机

在[模论](@entry_id:139410)中，我们经常将[函子](@entry_id:150427)应用于短[正合序列](@entry_id:151503)，并观察其结果。一个由 $R$-模构成的**短[正合序列](@entry_id:151503)** (short exact sequence) 是形如 $0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0$ 的序列，其中 $f$ 是[单射](@entry_id:183792)，$g$ 是满射，且 $\mathrm{Im}(f) = \ker(g)$。这本质上意味着 $A$ 可以被看作 $B$ 的一个子模，而 $C$ 是[商模](@entry_id:155903) $B/A$。

让我们考虑两个基本的[函子](@entry_id:150427)：**Hom 函子**与**[张量积](@entry_id:140694)函子** (tensor product functor)。

对于任意 $R$-模 $M$，协变 Hom [函子](@entry_id:150427) $\mathrm{Hom}_R(M, -)$ 是一个**左正合[函子](@entry_id:150427)** (left exact functor)。这意味着，将它应用于上述短[正合序列](@entry_id:151503)，会得到一个[正合序列](@entry_id:151503)：
$$
0 \to \mathrm{Hom}_R(M, A) \xrightarrow{f_*} \mathrm{Hom}_R(M, B) \xrightarrow{g_*} \mathrm{Hom}_R(M, C)
$$
这里的 $f_*(\phi) = f \circ \phi$。然而，这个序列在右端通常不是正合的，即 $g_*$ 不一定是满射。换言之，一个从 $M$ 到 $C$ 的同态不一定能“提升”为一个从 $M$ 到 $B$ 的同态。**Ext [函子](@entry_id:150427)** $\mathrm{Ext}_R^n(M, -)$ 正是为此而生，它们测量并弥补了这种右侧的“非正合性”。

类似地，[张量积](@entry_id:140694)函子 $- \otimes_R M$ 是一个**右正合[函子](@entry_id:150427)** (right exact functor)。将其应用于短[正合序列](@entry_id:151503)，我们得到一个[正合序列](@entry_id:151503)：
$$
A \otimes_R M \xrightarrow{f \otimes 1} B \otimes_R M \xrightarrow{g \otimes 1} C \otimes_R M \to 0
$$
然而，这个序列在左端通常不是正合的，即 $f \otimes 1$ 不一定是[单射](@entry_id:183792)。**Tor 函子** $\mathrm{Tor}_n^R(-, M)$ 就是用来量化这种左侧的“非正合性”的工具。例如，一个映射 $f: \mathbb{Z} \to \mathbb{Z}$ 定义为乘以 $n$，即 $f(k) = nk$。这是一个[单射](@entry_id:183792)。但当我们用 $\mathbb{Z}/m\mathbb{Z}$ 对其进行张量积后，得到的映射 $\tilde{f}: \mathbb{Z} \otimes_{\mathbb{Z}} (\mathbb{Z}/m\mathbb{Z}) \to \mathbb{Z} \otimes_{\mathbb{Z}} (\mathbb{Z}/m\mathbb{Z})$ 却可能不再是[单射](@entry_id:183792)。它的核，即 $\ker(\tilde{f})$，正是由 $\mathrm{Tor}_1^{\mathbb{Z}}$ 描述的 [@problem_id:1793085]。

### 形式化机制：分解与[导出函子](@entry_id:156814)

Ext 和 Tor 函子的系统性定义依赖于**投射分解** (projective resolution) 的概念。一个 $R$-模 $A$ 的投射分解是一个由投射模 (projective modules) 组成的长正合序列：
$$
\dots \xrightarrow{d_3} P_2 \xrightarrow{d_2} P_1 \xrightarrow{d_1} P_0 \xrightarrow{\epsilon} A \to 0
$$
其中每个 $P_i$ 都是投射模。任何模都至少存在一个投射分解（实际上，存在一个[自由模](@entry_id:152514)分解，而[自由模](@entry_id:152514)都是投射模）。

#### Ext [函子](@entry_id:150427)的构造

**Ext [函子](@entry_id:150427)** $\mathrm{Ext}_R^n(A, B)$ 被定义为 Hom [函子](@entry_id:150427)的**右[导出函子](@entry_id:156814)** (right derived functors)。其构造过程如下 [@problem_id:1681297]：

1.  取模 $A$ 的一个投射分解 $\dots \to P_1 \to P_0 \to A \to 0$。
2.  将模 $A$ 从序列中去掉，得到一个[链复形](@entry_id:150246) $P_\bullet = (\dots \xrightarrow{d_2} P_1 \xrightarrow{d_1} P_0 \to 0)$。
3.  对这个复形应用**[逆变](@entry_id:192290)** (contravariant) [函子](@entry_id:150427) $\mathrm{Hom}_R(-, B)$。由于其[逆变性](@entry_id:192290)，它会反转箭头方向，从而得到一个**上[链复形](@entry_id:150246)** (cochain complex)：
    $$
    0 \to \mathrm{Hom}_R(P_0, B) \xrightarrow{d_1^*} \mathrm{Hom}_R(P_1, B) \xrightarrow{d_2^*} \mathrm{Hom}_R(P_2, B) \to \dots
    $$
    其中 $d_n^*(\phi) = \phi \circ d_n$。
4.  $\mathrm{Ext}_R^n(A, B)$ 被定义为这个上[链复形](@entry_id:150246)的第 $n$ 个**上同调群** (cohomology group)：
    $$
    \mathrm{Ext}_R^n(A, B) = H^n(\mathrm{Hom}_R(P_\bullet, B)) = \frac{\ker(d_{n+1}^*)}{\mathrm{Im}(d_n^*)}
    $$
    一个重要的事实是，这样定义的 $\mathrm{Ext}_R^n(A, B)$ 在同构意义下不依赖于我们为 $A$ 选择的具体投射分解。

#### Tor [函子](@entry_id:150427)的构造

与此平行，**Tor 函子** $\mathrm{Tor}_n^R(A, B)$ 被定义为张量积函子的**左[导出函子](@entry_id:156814)** (left derived functors)。其构造步骤如下：

1.  同样，从模 $A$ 的一个投射分解开始。
2.  去掉模 $A$，得到[链复形](@entry_id:150246) $P_\bullet$。
3.  对这个复形应用**[协变](@entry_id:634097)** (covariant) 函子 $- \otimes_R B$，得到一个新的[链复形](@entry_id:150246)：
    $$
    \dots \to P_2 \otimes_R B \xrightarrow{d_2 \otimes 1} P_1 \otimes_R B \xrightarrow{d_1 \otimes 1} P_0 \otimes_R B \to 0
    $$
4.  $\mathrm{Tor}_n^R(A, B)$ 被定义为这个[链复形](@entry_id:150246)的第 $n$ 个**同调群** (homology group)：
    $$
    \mathrm{Tor}_n^R(A, B) = H_n(P_\bullet \otimes_R B) = \frac{\ker(d_n \otimes 1)}{\mathrm{Im}(d_{n+1} \otimes 1)}
    $$
    同样，这个定义不依赖于投射分解的选择。

### 核心性质与基本计算

#### 零阶[函子](@entry_id:150427)

通过上述构造，我们可以立即得到零阶函子的特性。

对于 Ext [函子](@entry_id:150427)，$\mathrm{Ext}_R^0(A, B) = \ker(d_1^*) / \mathrm{Im}(d_0^*)$。由于原序列在 $\mathrm{Hom}_R(P_1, B)$ 之前是 $0$，所以 $d_0^*$ 是零映射，其像为 $0$。而 $\ker(d_1^*)$ 恰好就是那些满足 $\phi \circ d_1 = 0$ 的同态 $\phi: P_0 \to B$。由分解的正合性，这等价于 $\phi$ 可以通过 $A$ 分解，即存在一个唯一的 $\bar{\phi}: A \to B$。因此，我们有基本的同构关系：
$$
\mathrm{Ext}_R^0(A, B) \cong \mathrm{Hom}_R(A, B)
$$
例如，要计算 $\mathrm{Ext}_{\mathbb{Z}}^0(\mathbb{Z}/4\mathbb{Z}, \mathbb{Z}/6\mathbb{Z})$，我们只需计算 $\mathrm{Hom}_{\mathbb{Z}}(\mathbb{Z}/4\mathbb{Z}, \mathbb{Z}/6\mathbb{Z})$。任何一个从 $\mathbb{Z}/4\mathbb{Z}$ 到 $\mathbb{Z}/6\mathbb{Z}$ 的同态 $f$ 都由 $\overline{1}$ 的像唯一确定。设 $f(\overline{1}) = b \in \mathbb{Z}/6\mathbb{Z}$。由于 $4 \cdot \overline{1} = \overline{0}$，我们必须有 $4b = \overline{0}$。在 $\mathbb{Z}/6\mathbb{Z}$ 中，这个条件意味着 $b$ 必须是 $\overline{0}$ 或 $\overline{3}$。因此，存在两个这样的同态，它们构成一个同构于 $\mathbb{Z}/2\mathbb{Z}$ 的群 [@problem_id:1793105]。一个更一般的结果是 $\mathrm{Hom}_{\mathbb{Z}}(\mathbb{Z}/n\mathbb{Z}, \mathbb{Z}/m\mathbb{Z}) \cong \mathbb{Z}/\gcd(n,m)\mathbb{Z}$。

对于 Tor 函子，$\mathrm{Tor}_0^R(A, B) = \ker(d_0 \otimes 1) / \mathrm{Im}(d_1 \otimes 1)$。由于 $d_0$ 就是 $\epsilon: P_0 \to A$，所以 $\mathrm{Im}(d_1 \otimes 1) = \ker(\epsilon \otimes 1)$。因此，我们有：
$$
\mathrm{Tor}_0^R(A, B) \cong \frac{P_0 \otimes_R B}{\ker(\epsilon \otimes 1)} \cong \mathrm{Im}(\epsilon \otimes 1) \cong A \otimes_R B
$$

#### 投射模的角色

如果模 $A$ 本身就是一个**投射模**，那么它的投射分解可以取得非常简单：
$$
\dots \to 0 \to P_0 \to A \to 0
$$
其中 $P_0 = A$，并且 $\epsilon$ 是恒等映射。这意味着分解中的所有 $P_n$ 对于 $n \ge 1$ 都是零模。

将这个平凡分解代入 Ext 和 Tor 的构造中，我们发现对应的（上）[链复形](@entry_id:150246)在 $n \ge 1$ 的阶次上都是零。因此，它们的（上）同调群也都是零。这导出了一个至关重要的性质：
- 如果 $A$ 是投射模，则 $\mathrm{Ext}_R^n(A, B) = 0$ 对所有 $n \ge 1$ 和所有模 $B$ 成立。
- 如果 $A$ 是投射模，则 $\mathrm{Tor}_n^R(A, B) = 0$ 对所有 $n \ge 1$ 和所有模 $B$ 成立。

例如，由于[自由模](@entry_id:152514)总是投射模，$\mathbb{Z}$ 和 $\mathbb{Z}^k$ 都是投射 $\mathbb{Z}$-模。因此，$\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z} \times \mathbb{Z}, \mathbb{Z}/30\mathbb{Z})$ 必须为零群 [@problem_id:1793091]。类似地，$\mathrm{Tor}_1^{\mathbb{Z}}(\mathbb{Z}^3, \mathbb{Q}/\mathbb{Z})$ 也为零 [@problem_id:1793110]。

#### 函子的不对称性

与 Hom 和张量积不同，Ext 和 Tor [函子](@entry_id:150427)在它们的两个变量中通常是**不对称的**。一个经典的例子可以说明这一点 [@problem_id:1793080]。考虑 $R=\mathbb{Z}$，我们来计算 $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}, \mathbb{Z}/n\mathbb{Z})$ 和 $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/n\mathbb{Z}, \mathbb{Z})$。

-   对于 $G_1 = \mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}, \mathbb{Z}/n\mathbb{Z})$，第一个参数 $\mathbb{Z}$ 是投射模。根据我们刚讨论的性质，所有高阶 Ext 群都消失，因此 $G_1 = 0$。

-   对于 $G_2 = \mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/n\mathbb{Z}, \mathbb{Z})$，第一个参数 $\mathbb{Z}/n\mathbb{Z}$ 不是投射模。我们需要使用它的投射分解。一个标准的[自由分解](@entry_id:266531)是短[正合序列](@entry_id:151503) $0 \to \mathbb{Z} \xrightarrow{\cdot n} \mathbb{Z} \to \mathbb{Z}/n\mathbb{Z} \to 0$。应用 $\mathrm{Hom}_{\mathbb{Z}}(-, \mathbb{Z})$ 会导出一条[长正合序列](@entry_id:153438)：
    $$
    \dots \to \mathrm{Hom}_{\mathbb{Z}}(\mathbb{Z}, \mathbb{Z}) \xrightarrow{(\cdot n)^*} \mathrm{Hom}_{\mathbb{Z}}(\mathbb{Z}, \mathbb{Z}) \to \mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/n\mathbb{Z}, \mathbb{Z}) \to \mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}, \mathbb{Z}) \to \dots
    $$
    我们知道 $\mathrm{Hom}_{\mathbb{Z}}(\mathbb{Z}, \mathbb{Z}) \cong \mathbb{Z}$，且 $(\cdot n)^*$ 映射正是乘以 $n$。同时，$\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}, \mathbb{Z}) = 0$ 因为 $\mathbb{Z}$ 是投射的。序列变为：
    $$
    \mathbb{Z} \xrightarrow{\cdot n} \mathbb{Z} \to G_2 \to 0
    $$
    根据正合性， $G_2$ 必须同构于映射 $\mathbb{Z} \xrightarrow{\cdot n} \mathbb{Z}$ 的上核 (cokernel)，即 $\mathbb{Z}/n\mathbb{Z}$。

因此，我们得到 $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}, \mathbb{Z}/n\mathbb{Z}) = 0$ 但 $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/n\mathbb{Z}, \mathbb{Z}) \cong \mathbb{Z}/n\mathbb{Z}$，这清晰地展示了 Ext 函子的不对称性。

### 特例：[主理想整环上的模](@entry_id:152666)

当环 $R$ 是一个**[主理想整环](@entry_id:152359)** (Principal Ideal Domain, [PID](@entry_id:174286))，例如整数环 $\mathbb{Z}$ 或域 $k$ 上的多项式环 $k[x]$ 时，Ext 和 Tor 函子的理论得到了极大的简化。

其根本原因是一个关于 [PID](@entry_id:174286) 上[模的结构定理](@entry_id:150651)：**在一个 [PID](@entry_id:174286) 上，任何[自由模](@entry_id:152514)的[子模](@entry_id:148922)仍然是[自由模](@entry_id:152514)**。这个强大的定理意味着任何 [PID](@entry_id:174286) 上的模 $A$ 都存在一个长度至多为 1 的[自由分解](@entry_id:266531)（因此也是投射分解）。我们可以如下构造它：
1.  任取一个满射 $\epsilon: F_0 \to A$，其中 $F_0$ 是一个[自由模](@entry_id:152514)。
2.  令 $F_1 = \ker(\epsilon)$。由于 $F_1$ 是[自由模](@entry_id:152514) $F_0$ 的子模，所以 $F_1$ 本身也是自由的。
3.  这样我们就得到了一个短的[自由分解](@entry_id:266531)：$0 \to F_1 \to F_0 \to A \to 0$。

这个简短的分解可以被看作一个无限长的分解，只需令所有 $P_n = 0$（对于 $n \ge 2$）。将这个分解代入 Ext 和 Tor 的定义，我们立即发现对应的（上）[链复形](@entry_id:150246)在阶数 $n \ge 2$ 的位置都是零。因此，我们得到了一个关于 [PID](@entry_id:174286) 的普遍结论 [@problem_id:1793061] [@problem_id:1793097]：

如果 $R$ 是一个 [PID](@entry_id:174286)，那么对于任意的 $R$-模 $A$ 和 $B$：
$$
\mathrm{Ext}_R^n(A, B) = 0 \quad \text{且} \quad \mathrm{Tor}_n^R(A, B) = 0 \quad \text{对所有 } n \ge 2
$$
这意味着在 [PID](@entry_id:174286) 上，我们只需要关心 $\mathrm{Ext}^1$ 和 $\mathrm{Tor}_1$。这使得计算变得可行。

例如，对于 $R=\mathbb{Z}$：
-   $\mathrm{Tor}_1^{\mathbb{Z}}(\mathbb{Z}/n\mathbb{Z}, B)$ 可以通过分解 $0 \to \mathbb{Z} \xrightarrow{\cdot n} \mathbb{Z} \to \mathbb{Z}/n\mathbb{Z} \to 0$ 计算。[张量积](@entry_id:140694)后得到 $B \xrightarrow{\cdot n} B$。$\mathrm{Tor}_1$ 就是这个映射的核，即 $B$ 中所有被 $n$ 零化的元素，也称为 $B$ 的 **$n$-[挠子群](@entry_id:139454)** (n-torsion subgroup)。特别地，$\mathrm{Tor}_1^{\mathbb{Z}}(\mathbb{Z}/n\mathbb{Z}, \mathbb{Z}/m\mathbb{Z}) \cong \mathbb{Z}/\gcd(n,m)\mathbb{Z}$ [@problem_id:1793085]。这解释了为什么在 [@problem_id:1793110] 的选项中，$\mathrm{Tor}_1^{\mathbb{Z}}(\mathbb{Z}/12\mathbb{Z}, \mathbb{Z}/12\mathbb{Z}) \cong \mathbb{Z}/12\mathbb{Z}$ 是非零的，而 $\mathrm{Tor}_1^{k[x]}(k[x]/(x-1), k[x]/(x-2))$ 为零（因为后者的核是平凡的）。

-   $\mathrm{Ext}_{\mathbb{Z}}^1(\mathbb{Z}/n\mathbb{Z}, B)$ 可以通过同样的方式计算，它同构于映射 $B \xrightarrow{\cdot n} B$ 的上核，即 $B/nB$ [@problem_id:1793064]。

### Ext¹ 的意义：扩张的分类

现在我们回到 Ext 函子的最初动机：理解模的扩张。一个 $R$-模 $E$ 被称为**由 $A$ 对 $C$ 的扩张** (extension of $C$ by $A$)，如果它能放入一个短[正合序列](@entry_id:151503) $0 \to A \to E \to C \to 0$。

一个基本的问题是：给定模 $A$ 和 $C$，存在多少个“不同”的扩张 $E$？这里的“不同”是指在保持 $A$ 和 $C$ 不变的同构意义下。同调代数给出了一个惊人的答案：
**所有由 $A$ 对 $C$ 的扩张的等价类集合，与群 $\mathrm{Ext}_R^1(C, A)$ 的元素之间存在一个[双射](@entry_id:138092)。**

这个对应关系赋予了 $\mathrm{Ext}_R^1(C, A)$ 中的每个元素一个具体的代数意义。
-   **零元素**：群 $\mathrm{Ext}_R^1(C, A)$ 中的零元素对应于**[可裂扩张](@entry_id:143915)** (split extension)。这意味着短[正合序列](@entry_id:151503)是可裂的，此时 $E$ 同构于直和 $A \oplus C$。这是最平凡的扩张方式。
-   **非零元素**：每个非零元素都对应一个非平凡的扩张，即 $E$ 不能分解为 $A$ 和 $C$ 的[直和](@entry_id:156782)。

我们可以通过构造上循环 (cocycle) 来明确这种对应关系。考虑可裂短[正合序列](@entry_id:151503) $0 \to A \xrightarrow{i} A \oplus C \xrightarrow{p} C \to 0$。根据上述理论，它应该对应 $\mathrm{Ext}_{\mathbb{Z}}^1(C, A)$ 中的零元素。这意味着与之关联的 [1-上循环](@entry_id:144864)必须是一个 1-上边缘 (coboundary) [@problem_id:1793095]。

让我们在 $R=\mathbb{Z}$，$C=\mathbb{Z}/6\mathbb{Z}$，$A=\mathbb{Z}/9\mathbb{Z}$ 的情境下验证这一点。我们使用 $C$ 的[自由分解](@entry_id:266531) $0 \to \mathbb{Z} \xrightarrow{d_1} \mathbb{Z} \xrightarrow{\epsilon} \mathbb{Z}/6\mathbb{Z} \to 0$，其中 $d_1$ 是乘以 6。
1.  我们将映射 $\epsilon: \mathbb{Z} \to \mathbb{Z}/6\mathbb{Z}$ 提升为一个同态 $\beta: \mathbb{Z} \to \mathbb{Z}/9\mathbb{Z} \oplus \mathbb{Z}/6\mathbb{Z}$，使得 $p \circ \beta = \epsilon$。一个可能的提升是 $\beta(1) = (5, 1)$。
2.  通过关系 $i \circ \alpha = \beta \circ d_1$ 定义一个 [1-上循环](@entry_id:144864) $\alpha \in \mathrm{Hom}_{\mathbb{Z}}(\mathbb{Z}, \mathbb{Z}/9\mathbb{Z})$。计算可得 $\alpha(1)=\overline{3}$。
3.  因为原始序列是可裂的，所以 $\alpha$ 必须是一个上边缘，即存在一个同态 $\phi \in \mathrm{Hom}_{\mathbb{Z}}(\mathbb{Z}, \mathbb{Z}/9\mathbb{Z})$ 使得 $\alpha = d_1^*(\phi) = \phi \circ d_1$。
4.  设 $\phi(1)=x \in \mathbb{Z}/9\mathbb{Z}$。那么 $\alpha(1) = (\phi \circ d_1)(1) = \phi(6) = 6x$。
5.  我们得到方程 $6x \equiv 3 \pmod 9$。这个同余方程的解是 $x \equiv 2 \pmod 3$，在 $\mathbb{Z}/9\mathbb{Z}$ 中即 $x \in \{2, 5, 8\}$。
6.  我们确实找到了一个这样的 $\phi$（例如，$\phi(1)=2$），证明了 $\alpha$ 是一个上边缘。这具体地展示了[可裂扩张](@entry_id:143915)如何对应于上同调群中的零元素（即一个上边缘）。

因此，$\mathrm{Ext}^1$ 不仅是一个抽象的代数对象，它还是一个强大的分类工具，其[群结构](@entry_id:146855)（例如，群的阶 [@problem_id:1793064]）直接反映了模之间所有可能的“扭曲”组合方式。