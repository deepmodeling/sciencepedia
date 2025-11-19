## 引言
在[代数拓扑学](@entry_id:138192)中，我们常常使用[上同调环](@entry_id:160158)等代数[不变量](@entry_id:148850)来研究和区分拓扑空间。然而，有时仅靠[上同调环](@entry_id:160158)的结构并不足以揭示空间的全部拓扑奥秘。为了获得更精细的“指纹”，我们需要超越环结构本身，引入作用于其上的运算。**Steenrod 平方 (Steenrod Squares)** 正是这样一类强大而深刻的[上同调运算](@entry_id:263436)，它们构成了现代代数[拓扑的基](@entry_id:148152)石。

本文旨在系统地介绍 Steenrod 平方这一核心理论。我们将解决一个关键问题：如何利用超越[上同调环](@entry_id:160158)结构的代数工具来揭示空间的深层拓扑性质？通过学习，读者将掌握一套能够区分[同伦](@entry_id:139266)不等[价空间](@entry_id:756405)、证明映射存在性障碍以及连接[拓扑学与几何学](@entry_id:634069)的强大方法。

文章将分为三个核心部分。在“**原理与机制**”一章中，我们将从公理化定义出发，深入探讨 Steenrod 平方的基本性质，如自然性、Cartan 公式和 Adem 关系，并学习其在[射影空间](@entry_id:157963)等经典范例上的计算方法。随后，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将展示这些运算的威力，看它们如何被用于区分空间（如 $\mathbb{C}P^2$ 与 $S^2 \vee S^4$）、解决[同伦论](@entry_id:150876)中的经典问题（如证明 Hopf 映射非零伦），以及如何与微分几何中的[示性类](@entry_id:160596)理论建立深刻联系。最后，“**动手实践**”部分将提供一系列练习，帮助读者巩固理论知识并将其应用于具体计算中。

## 原理与机制

在上一章中，我们介绍了[上同调运算](@entry_id:263436)的概念，即在不同拓扑空间的[上同调群](@entry_id:142450)之间保持自然的[代数结构](@entry_id:137052)。在本章中，我们将深入研究一类最重要、最强大的[上同调运算](@entry_id:263436)——**Steenrod 平方 (Steenrod Squares)**。这些运算作用于模 2 系数的上同调群 $H^*(X; \mathbb{Z}_2)$，为我们提供了一套丰富的代数[不变量](@entry_id:148850)，能够揭示空间的深层[拓扑性质](@entry_id:141605)。它们是连接[上同调环](@entry_id:160158)结构、向量丛理论以及[同伦论](@entry_id:150876)的桥梁。

本章的目标是系统地阐述 Steenrod 平方的公理化定义、核心代数性质以及关键的计算机制。我们将从基本公理出发，逐步揭示这些运算的内在结构和威力。

### Steenrod 平方的公理化基础

Steenrod 平方是一族运算 $Sq^i$（其中 $i \ge 0$），对于任意[拓扑空间](@entry_id:155056) $X$ 和任意整数 $n \ge 0$，它定义了一个[群同态](@entry_id:140603)：
$$Sq^i: H^n(X; \mathbb{Z}_2) \to H^{n+i}(X; \mathbb{Z}_2)$$
这意味着 $Sq^i$ 将一个 $n$ 维的[上同调类](@entry_id:263961)映射到一个 $(n+i)$ 维的[上同调类](@entry_id:263961)。这些运算并非孤立存在，而是遵循一套严格的公理，这些公理共同决定了它们的性质。

#### 自然性：[上同调运算](@entry_id:263436)的本质

Steenrod 平方的第一个，也是最根本的性质是**自然性 (naturality)**。这意味着对于任意连续映射 $f: X \to Y$，它所诱导的上同调同态 $f^*: H^*(Y; \mathbb{Z}_2) \to H^*(X; \mathbb{Z}_2)$ 与 Steenrod 平方运算是可交换的。换言之，对于任意上同调类 $a \in H^*(Y; \mathbb{Z}_2)$，以下图表是可交换的：

$$
\begin{aligned}
H^n(Y; \mathbb{Z}_2)  \xrightarrow{\quad Sq^i \quad} H^{n+i}(Y; \mathbb{Z}_2) \\
\downarrow f^* \quad  \qquad \qquad \downarrow f^* \\
H^n(X; \mathbb{Z}_2)  \xrightarrow{\quad Sq^i \quad} H^{n+i}(X; \mathbb{Z}_2)
\end{aligned}
$$

这可以用一个等式简洁地表达：$f^*(Sq^i(a)) = Sq^i(f^*(a))$。

自然性是一个极其强大的属性。它保证了 Steenrod 平方是真正依赖于空间的拓扑结构，而非其[上同调群](@entry_id:142450)的某种特定表示。这也意味着，如果我们知道了 $Sq^i$ 在一个“典范”空间上的作用，我们就可以利用自然性来推断它在其他相关空间上的作用。

例如，考虑标准嵌入映射 $i: \mathbb{R}P^2 \to \mathbb{R}P^\infty$。我们知道 $H^*(\mathbb{R}P^\infty; \mathbb{Z}_2) \cong \mathbb{Z}_2[y]$，其中 $|y|=1$；而 $H^*(\mathbb{R}P^2; \mathbb{Z}_2) \cong \mathbb{Z}_2[x]/(x^3)$，其中 $|x|=1$。诱导映射 $i^*$ 将 $y$ 映为 $x$，即 $i^*(y)=x$。假设我们已知 $Sq^1(y) = y^2$。利用自然性，我们可以直接计算 $Sq^1(x)$：
$$Sq^1(x) = Sq^1(i^*(y)) = i^*(Sq^1(y)) = i^*(y^2) = (i^*(y))^2 = x^2$$
这个计算过程明确地展示了自然性如何成为在不同空间之间传递运算信息的工具 [@problem_id:1675091] [@problem_id:1662987]。

#### 基本性质与次数公理

除了自然性，Steenrod 平方还满足以下几条基本的公理：

1.  **线性 (Linearity)**: $Sq^i$ 是一个[群同态](@entry_id:140603)，即 $Sq^i(u+v) = Sq^i(u) + Sq^i(v)$。由于我们工作在 $\mathbb{Z}_2$ 系数下，这等价于线性。

2.  **单位元 (Identity)**: 对于任意[上同调类](@entry_id:263961) $u$，有 $Sq^0(u) = u$。这意味着 $Sq^0$ 是恒等运算。这是一个基础的起点。

3.  **次数公理 (Dimension Axiom)**: 如果[上同调类](@entry_id:263961) $u$ 的次数 $|u|=k$，则 $Sq^k(u) = u \smile u = u^2$。这条公理将 $Sq^k$ 与[上同调环](@entry_id:160158)的**杯积 (cup product)** 结构直接联系起来，表明 $Sq^k$ 是一种“平方”运算。

4.  **不稳定性 (Instability)**: 如果 $i > |u|$，则 $Sq^i(u) = 0$。这条公理极大地限制了非零的 Steenrod 平方。它表明 $Sq^i$ 不能将一个上同调类“提升”到一个过高的维度。

不稳定性公理在复合运算中尤其有用。例如，考虑一个复合运算 $Sq^i(Sq^j(x))$，其中 $x \in H^n(X; \mathbb{Z}_2)$。内部运算 $Sq^j(x)$ 产生一个次数为 $n+j$ 的上同调类。根据不稳定性公理，如果外部运算的指标 $i$ 大于这个新类的次数，即 $i > n+j$，那么整个复合运算的结果必定为零。

举个例子，设 $x \in H^4(X; \mathbb{Z}_2)$。我们来判断 $Sq^7(Sq^2(x))$ 是否必定为零。这里 $n=4, j=2, i=7$。内部运算 $Sq^2(x)$ 的结果是一个次数为 $4+2=6$ 的类。由于外部运算的指标 $7$ 大于这个类的次数 $6$，根据不稳定性公理，$Sq^7(Sq^2(x))$ 必须为零，这与空间 $X$ 或[上同调类](@entry_id:263961) $x$ 的具体形态无关 [@problem_id:1675150]。

### Steenrod 运算的[代数结构](@entry_id:137052)

Steenrod 平方不仅仅是一系列孤立的运算，它们之间通过深刻的代数关系联系在一起，形成一个[代数结构](@entry_id:137052)，即 **Steenrod 代数 (Steenrod algebra)**。其中最重要的两个关系是 Cartan 公式和 Adem 关系。

#### Cartan 公式：与杯积的互动

**Cartan 公式 (Cartan Formula)** 描述了 Steenrod 平方如何作用于两个[上同调类](@entry_id:263961)的[杯积](@entry_id:159554)。其具体形式为：
$$Sq^k(u \smile v) = \sum_{i+j=k} Sq^i(u) \smile Sq^j(v)$$
这个公式是进行具体计算的核心工具。

为了更简洁地使用 Cartan 公式，我们常常引入**总 Steenrod 平方 (total Steenrod square)** $Sq = \sum_{i=0}^\infty Sq^i$。这是一个作用于整个[上同调环](@entry_id:160158) $H^*(X; \mathbb{Z}_2)$ 的运算。利用 $Sq$，Cartan 公式可以被优美地写成：
$$Sq(u \smile v) = Sq(u) \smile Sq(v)$$
这表明，总 Steenrod 平方 $Sq$ 是[上同调环](@entry_id:160158) $H^*(X; \mathbb{Z}_2)$ 上的一个[环同态](@entry_id:153804)。

Cartan 公式有许多直接而重要的推论。例如，我们可以用它来证明对于任意[上同调类](@entry_id:263961) $x$，总有 $Sq^1(x^2)=0$。计算过程如下：
$$Sq^1(x^2) = Sq^1(x \smile x) = Sq^1(x) \smile Sq^0(x) + Sq^0(x) \smile Sq^1(x)$$
利用 $Sq^0(x)=x$ 以及在 $\mathbb{Z}_2$ 系数下杯积的[交换性](@entry_id:140240)，上式变为：
$$Sq^1(x) \smile x + x \smile Sq^1(x) = 2(x \smile Sq^1(x))$$
因为我们工作在模 2 系数下，$2=0$，所以 $Sq^1(x^2)=0$ [@problem_id:1675140]。这表明 $Sq^1$ 在某种意义上表现得像一个关于平方运算的导子。

Cartan 公式使得我们可以通过对生成元的作用来计算对整个[上同调环](@entry_id:160158)的作用。例如，在[克莱因瓶](@entry_id:149661) $K$ 的[上同调环](@entry_id:160158) $H^*(K; \mathbb{Z}_2) \cong \mathbb{Z}_2[x, y] / (x^2, xy+y^2)$ 中，我们可以计算 $Sq$ 对所有基元素的作用。对于生成元 $y \in H^1(K; \mathbb{Z}_2)$：
$$Sq(y) = Sq^0(y) + Sq^1(y) = y + y^2$$
然后，我们可以利用 Cartan 公式的[环同态](@entry_id:153804)形式来计算 $Sq(y^2)$：
$$Sq(y^2) = Sq(y \smile y) = Sq(y) \smile Sq(y) = (y+y^2) \smile (y+y^2) = y^2 + 2y^3 + y^4$$
由于 $H^n(K; \mathbb{Z}_2)=0$ 对 $n>2$ 成立，所以 $y^3=y^4=0$。因此 $Sq(y^2)=y^2$ [@problem_id:1675132]。这个例子展示了 Cartan 公式与空间的具体[上同调环](@entry_id:160158)结构如何结合在一起进行计算。

#### 在[射影空间](@entry_id:157963)上的计算

[实射影空间](@entry_id:149094) $\mathbb{R}P^\infty$ 的模 2 [上同调环](@entry_id:160158) $H^*(\mathbb{R}P^\infty; \mathbb{Z}_2)$ 是 Steenrod 平方理论中最重要的计算范例。该环是一个单变量[多项式环](@entry_id:152854) $\mathbb{Z}_2[x]$，其中 $x$ 是 1 维生成元。Steenrod 平方在 $x$ 上的作用完全由公理决定：
*   $Sq^0(x) = x$ (单位元)
*   $Sq^1(x) = x^2$ (次数公理)
*   $Sq^i(x) = 0$ 对 $i > 1$ (不稳定性)

有了在生成元 $x$ 上的作用，我们可以利用 Cartan 公式递归地计算出 $Sq^i$ 在任意次幂 $x^k$ 上的作用。例如，要计算 $Sq^1(x^2)$，我们已知结果为 0。使用 Cartan 公式：$Sq^1(x^2) = Sq^1(x)x + xSq^1(x) = x^2x + xx^2 = 2x^3 = 0$。

通过对 $k$ 进行[数学归纳法](@entry_id:138544)，可以得到一个普适的公式：
$$Sq^i(x^k) = \binom{k}{i} x^{k+i}$$
其中二项式系数 $\binom{k}{i}$ 在模 2 意义下取值。这个公式是 Steenrod 平方计算的基石。

利用这个公式，我们可以验证一些更深层次的性质。例如，次数公理断言，对于一个 $k$ 维的类 $u$，有 $Sq^k(u)=u^2$。让我们在 $\mathbb{R}P^n$（其中 $n \ge 2k$）中验证这一点。令 $u = x^k \in H^k(\mathbb{R}P^n; \mathbb{Z}_2)$。根据上述公式：
$$Sq^k(x^k) = \binom{k}{k} x^{k+k} = 1 \cdot x^{2k} = (x^k)^2$$
这完美地验证了次数公理 [@problem_id:1675138]。我们甚至可以反过来，从 $Sq^1(\alpha)=\alpha^2$ 和 Cartan 公式出发，推导出 $Sq^k(\alpha^k)=\alpha^{2k}$，这显示了理论的内在一致性。

### 更深层的结构性质

除了上述基本公理和代数关系，Steenrod 平方还具有更深层的结构，这些结构将它们与拓扑学的其他分支联系起来。

#### 稳定性与悬挂同构

一个重要的拓扑构造是**悬挂 (suspension)**。对于一个[带基点的空间](@entry_id:273706) $X$，其**约化悬挂 (reduced suspension)** $\Sigma X$ 在[同伦论](@entry_id:150876)中扮演着核心角色。悬挂运算诱导了一个[上同调群](@entry_id:142450)之间的同构，称为**悬挂同构 (suspension isomorphism)**：
$$\sigma: \tilde{H}^n(X; \mathbb{Z}_2) \to \tilde{H}^{n+1}(\Sigma X; \mathbb{Z}_2)$$
Steenrod 平方的一个非凡性质是它们与悬挂同构的**[可交换性](@entry_id:263314)**，这被称为**稳定性 (stability)**：
$$Sq^k(\sigma(x)) = \sigma(Sq^k(x))$$
对于任意上同调类 $x$ 和所有 $k \ge 0$ 都成立。这意味着 Steenrod 平方是**稳定[上同调运算](@entry_id:263436) (stable cohomology operations)**。这个性质是稳定[同伦论](@entry_id:150876)的出发点之一，它表明 Steenrod 运算在悬挂下保持不变，揭示了独立于维度的深层结构 [@problem_id:1675102]。

#### Adem 关系与 Bockstein 同态

Steenrod 平方不仅可以逐个作用，还可以复合作用，例如 $Sq^i \circ Sq^j$。**Adem 关系 (Adem relations)** 是一组公式，它们描述了这种复合运算如何分解为其他 Steenrod 平方的[线性组合](@entry_id:154743)。对于 $a  2b$，Adem 关系的一般形式是：
$$Sq^a Sq^b = \sum_{j=0}^{\lfloor a/2 \rfloor} \binom{b-j-1}{a-2j} Sq^{a+b-j} Sq^j$$
这些关系定义了 Steenrod 代数的乘法结构。

在本科或研究生入门阶段，我们通常只关注最简单但最有用的 Adem 关系，例如 $Sq^1 Sq^2 = Sq^3$ 和 $Sq^2 Sq^2 = Sq^3 Sq^1$。

最重要的 Adem 关系之一是 $Sq^1 \circ Sq^1 = 0$。我们可以通过在 $H^*(\mathbb{R}P^\infty; \mathbb{Z}_2)$ 上进行直接计算来验证这一点。对于任意 $x^k$：
$$Sq^1(Sq^1(x^k)) = Sq^1\left(\binom{k}{1} x^{k+1}\right) = \binom{k}{1} Sq^1(x^{k+1}) = \binom{k}{1} \binom{k+1}{1} x^{k+2}$$
模 2 [二项式系数](@entry_id:261706) $\binom{n}{1}$ 当且仅当 $n$ 是奇数时为 1。因此，$\binom{k}{1} \binom{k+1}{1}$ 的值总是 0，因为 $k$ 和 $k+1$ 中必有一个是偶数。这表明 $Sq^1(Sq^1(x^k))=0$。通过线性，可知 $Sq^1 \circ Sq^1 = 0$ 在整个环上成立 [@problem_id:1675128]。

$Sq^1 \circ Sq^1 = 0$ 这个关系意味着 $Sq^1$ 表现得像一个**[微分算子](@entry_id:140145) (differential)**，它使得我们可以用 $(H^*(X; \mathbb{Z}_2), Sq^1)$ 来构造一个[链复形](@entry_id:150246)。

这个性质与另一个重要的[上同调运算](@entry_id:263436)——**Bockstein 同态 (Bockstein homomorphism)** $\beta$ 密切相关。Bockstein 同态 $\beta: H^n(X; \mathbb{Z}_2) \to H^{n+1}(X; \mathbb{Z}_2)$ 是由系数群的短[正合序列](@entry_id:151503) $0 \to \mathbb{Z}_2 \to \mathbb{Z}_4 \to \mathbb{Z}_2 \to 0$ 诱导的[长正合序列](@entry_id:153438)中的[连接同态](@entry_id:160713)。一个深刻的结论是，这个 Bockstein 同态与第一个 Steenrod 平方是同一个运算：
$$\beta = Sq^1$$
从长正合序列的性质我们知道 $\beta \circ \beta = 0$，这立即为 $Sq^1 \circ Sq^1 = 0$ 提供了一个概念性的解释。这个等式将 Steenrod 运算与系数理论联系起来，为我们提供了两种不同的视角来理解 $Sq^1$。例如，知道了这个等式，我们就可以立即推断出，对于任意上同调类 $u$，类 $Sq^1(\beta(u))$ 和 $\beta(\beta(u))$ 都必定为零 [@problem_id:1675146]。

通过本章的学习，我们建立了 Steenrod 平方的公理化框架，并通过 Cartan 公式和在[射影空间](@entry_id:157963)上的作用掌握了其计算方法。我们还初步接触了稳定性和 Adem 关系等更深层的结构。这些原理和机制共同构成了研究模 2 [上同调](@entry_id:160558)[代数结构](@entry_id:137052)不可或缺的工具箱。