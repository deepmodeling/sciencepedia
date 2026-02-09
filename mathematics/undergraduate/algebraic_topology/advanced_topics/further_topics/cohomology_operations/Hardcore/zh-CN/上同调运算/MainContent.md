## 引言
上同调论是代数拓扑学的基石，它通过将代数结构（如群或环）赋予拓扑空间来研究它们的性质。然而，在许多情况下，仅凭上同调群或上同调环的结构不足以区分两个本质上不同的空间，或完全理解它们之间的映射关系。这一知识上的空白，正是通过研究上同调群自身内在的代数结构——即**上同调运算**——来填补的。这些运算是比杯积更精细的代数不变量，为我们提供了洞察拓扑现象的强大显微镜。

本文将系统地引导读者探索上同调运算的世界。在“原理与机制”一章中，我们将建立上同调运算的严格定义，并深入探讨博克斯坦同态和斯廷罗德平方这两类核心范例。接着，在“应用与交叉学科联系”一章中，我们将展示如何运用这些运算来解决具体的拓扑问题，例如区分空间、证明霍普夫映射的非平凡性，并揭示其与微分几何等领域的深刻联系。最后，“动手实践”一章将提供一系列练习，帮助读者巩固所学知识并提升计算能力。现在，让我们从上同调运算的基本定义和性质开始。

## 原理与机制

上同调论不仅为拓扑空间赋予了代数不变量——上同调群，更重要的是，它还揭示了这些不变量之间深刻的内在联系。这些联系通过所谓的 **上同调运算 (cohomology operations)** 来表达。本章将深入探讨上同调运算的定义、关键性质及其主要范例，特别是博克斯坦同态和斯廷罗德平方。

### 什么是上同调运算？

从最根本的层面看，上同调本身可以被视为一个从拓扑空间范畴到分次交换环范畴的（反变）函子。上同调运算则是这些函子之间的自然变换。

**定义**：一个类型为 $(n, G; m, H)$ 的上同调运算 $\theta$ 是一个函数族 $\theta_X: H^n(X; G) \to H^m(X; H)$，对每个拓扑空间 $X$ 都对应一个函数，并且该函数族满足 **自然性 (naturality)**。自然性意味着对于任意连续映射 $f: X \to Y$ 和任意上同调类 $\alpha \in H^n(Y; G)$，下述等式成立：
$$ f^*(\theta_Y(\alpha)) = \theta_X(f^*(\alpha)) $$
这里 $f^*$ 是由 $f$ 在相应的上同调群上诱导的同态。这个条件可以用一个交换图来直观表示：
$$
\begin{CD}
H^n(Y; G) @>{\theta_Y}>> H^m(Y; H) \\
@V{f^*}VV @VV{f^*}V \\
H^n(X; G) @>{\theta_X}>> H^m(X; H)
\end{CD}
$$

自然性是一个非常强的约束。它要求运算 $\theta$ 的定义是“普适的”，不依赖于特定空间的几何细节，并且与所有连续映射的拉回作用相容。

最直接的一类上同调运算源于系数群之间的同态。假设我们有一个群同态 $\rho: G \to H$。这个同态可以在上链层面诱导一个映射 $\rho_*: C^k(X; G) \to C^k(X; H)$，其定义为对任意上链 $\phi: S_k(X) \to G$，有 $\rho_*(\phi) = \rho \circ \phi$。由于 $\rho$ 是一个同态，这个上链映射与余边缘算子 $\delta$ 可交换，即 $\rho_* \circ \delta = \delta \circ \rho_*$。这意味着 $\rho_*$ 将闭上链映为闭上链，将恰当上链映为恰当上链，因此它在商空间上诱导了一个定义良好的同态 $\rho_{**}: H^k(X; G) \to H^k(X; H)$。

我们可以验证这个诱导映射 $\rho_{**}$ 确实构成一个上同调运算。其良定义性已如上述。对于自然性，考虑任意连续映射 $f: X \to Y$ 和类 $[\phi] \in H^n(Y; G)$。一方面，$f^*(\rho_{**}([\phi])) = f^*([\rho \circ \phi]) = [(\rho \circ \phi) \circ f_*]$。另一方面，$\rho_{**}(f^*([\phi])) = \rho_{**}([ \phi \circ f_* ]) = [\rho \circ (\phi \circ f_*)]$。由于函数复合的结合律，两者相等。因此，由系数同态诱导的映射是一个上同调运算。例如，由典范投射 $\rho: \mathbb{Z} \to \mathbb{Z}_2$ 诱导的映射 $\Theta_X: H^n(X; \mathbb{Z}) \to H^n(X; \mathbb{Z}_2)$ 就是一个 $(n, \mathbb{Z}; n, \mathbb{Z}_2)$ 型的上同调运算。[@problem_id:1641159]

相比之下，任何依赖于对每个空间 $X$ 进行任意选择的构造通常都会破坏自然性。例如，如果我们试图通过与一个在每个空间 $X$ 中任意选定的上同调类 $\alpha_X$ 作杯积来定义一个运算，那么自然性通常会失效。考虑一个映射 $\Theta_X(\beta) = \rho_{**}(\beta) \cup \alpha_X$，其中 $\alpha_X \in H^1(X; \mathbb{Z}_2)$ 是任意选的。自然性要求 $f^*(\rho_{**}(\gamma) \cup \alpha_Y) = \rho_{**}(f^*\gamma) \cup \alpha_X$ 对所有 $f: X \to Y$ 和 $\gamma \in H^n(Y; G)$ 成立。利用杯积和 $\rho_{**}$ 的自然性，这简化为要求 $f^*(\alpha_Y) = \alpha_X$。这个条件显然无法对任意的 $f$ 和任意的选择成立。例如，取 $Y$ 为一个单点空间，则 $\alpha_Y=0$。对于任何具有非平凡一阶上同调的 $X$（例如圆环 $S^1$），我们可以选取 $\alpha_X \neq 0$。对于常值映射 $f: X \to Y$，我们得到 $f^*(\alpha_Y)=0 \neq \alpha_X$，自然性遭到破坏。[@problem_id:1641159]

另一个重要的反例是，尝试通过与某个特定空间中的一个固定上同调类作杯积来定义运算。设想在 $S^2$ 上定义一个映射 $\theta_{S^2}: H^0(S^2; \mathbb{Z}) \to H^2(S^2; \mathbb{Z})$ 为 $\theta_{S^2}(y) = y \cup \sigma$，其中 $\sigma$ 是 $H^2(S^2; \mathbb{Z})$ 的生成元。为了检验这是否能成为一个自然变换的一部分，我们考虑一个度为 $d=5$ 的自映射 $f: S^2 \to S^2$。令 $y_0$ 为 $H^0(S^2; \mathbb{Z})$ 的生成元 $1$。一方面，我们计算 $f^*(\theta_{S^2}(y_0)) = f^*(1 \cup \sigma) = f^*(\sigma)$。由度数的定义，$f^*(\sigma) = d\sigma = 5\sigma$。另一方面，$\theta_{S^2}(f^*(y_0)) = \theta_{S^2}(f^*(1)) = \theta_{S^2}(1) = 1 \cup \sigma = \sigma$。由于 $5\sigma \neq \sigma$，自然性条件不成立。这表明，仅仅在一个空间上定义良好的映射，并不能保证它是一个普适的上同调运算。[@problem_id:1641166]

### 基本范例：博克斯坦同态

一类非常重要的上同调运算是 **博克斯坦同态 (Bockstein homomorphisms)**。它产生于系数群的任意一个短正合序列 $0 \to G \xrightarrow{i} E \xrightarrow{p} H \to 0$。这个序列会在上同调中诱导一个长正合序列：
$$ \dots \to H^n(X; G) \xrightarrow{i_*} H^n(X; E) \xrightarrow{p_*} H^n(X; H) \xrightarrow{\beta} H^{n+1}(X; G) \to \dots $$
其中的 **连接同态 (connecting homomorphism)** $\beta: H^n(X; H) \to H^{n+1}(X; G)$ 就是一个博克斯坦同态。它是一个 $(n, H; n+1, G)$ 型的上同调运算。

我们来验证一下 $\beta$ 的自然性。考虑一个连续映射 $f: X \to Y$。由于函子的性质，这个映射诱导了两个长正合序列之间的链映射。这意味着下图中的每一个方格都是交换的：
$$
\begin{CD}
\dots @>>> H^n(Y; H) @>{\beta_Y}>> H^{n+1}(Y; G) @>>> \dots \\
  @. @V{f^*}VV @VV{f^*}V @. \\
\dots @>>> H^n(X; H) @>{\beta_X}>> H^{n+1}(X; G) @>>> \dots
\end{CD}
$$
特别地，标有 $\beta$ 的那个方格的交换性 $f^* \circ \beta_Y = \beta_X \circ f^*$ 正是上同调运算所要求的自然性条件。例如，我们可以对实射影直线到实射影平面的标准包含映射 $i: \mathbb{R}P^1 \hookrightarrow \mathbb{R}P^2$ 来显式验证这一点。考虑由 $0 \to \mathbb{Z} \xrightarrow{\times 2} \mathbb{Z} \to \mathbb{Z}_2 \to 0$ 诱导的博克斯坦 $\beta$。令 $\alpha_2$ 为 $H^1(\mathbb{R}P^2; \mathbb{Z}_2)$ 的生成元。一方面，$(\beta \circ i^*)(\alpha_2) = \beta(i^*(\alpha_2))$。由于 $i^*$ 是一个同构， $i^*(\alpha_2)$ 是 $H^1(\mathbb{R}P^1; \mathbb{Z}_2)$ 的生成元 $\alpha_1$。而 $\beta(\alpha_1)$ 属于 $H^2(\mathbb{R}P^1; \mathbb{Z})$，这是一个平凡群，所以 $\beta(\alpha_1)=0$。另一方面，$(i^* \circ \beta)(\alpha_2) = i^*(\beta(\alpha_2))$。无论 $\beta(\alpha_2) \in H^2(\mathbb{R}P^2; \mathbb{Z})$ 是什么，它在 $i^*$ 作用下都会被映到 $H^2(\mathbb{R}P^1; \mathbb{Z}) = 0$ 中，因此结果也为零。双方相等验证了自然性。[@problem_id:1641119]

博克斯坦同态的定义虽然抽象，但在实践中是完全可以计算的。其计算方式遵循“蛇引理”的构造。对于一个上同调类 $[\phi] \in H^k(X; \mathbb{Z}_2)$，我们首先找到一个上链 $\tilde{\phi} \in C^k(X; \mathbb{Z}_4)$，它在模2规约下映到 $\phi$，即 $p_*(\tilde{\phi}) = \phi$。由于 $\delta \phi = 0$，我们有 $p_*(\delta \tilde{\phi}) = \delta(p_*(\tilde{\phi})) = \delta\phi = 0$。根据短正合序列的性质，这意味着 $\delta \tilde{\phi}$ 必然是某个 $\mathbb{Z}_2$ 系数上链 $\psi$ 在映射 $i$ 下的像，即 $\delta \tilde{\phi} = i_*(\psi)$。可以证明 $\psi$ 是一个闭上链，它所代表的上同调类 $[\psi] \in H^{k+1}(X; \mathbb{Z}_2)$ 就是 $\beta([\phi])$。

让我们以 $X = \mathbb{R}P^3$ 和由 $0 \to \mathbb{Z}_2 \xrightarrow{i} \mathbb{Z}_4 \xrightarrow{p} \mathbb{Z}_2 \to 0$（其中 $i(1)=2$）诱导的博克斯坦 $\beta$ 为例。$H^*(\mathbb{R}P^3; \mathbb{Z}_2)$ 是由1次类 $w$ 生成的截断多项式代数 $\mathbb{Z}_2[w]/(w^4)$。我们来计算 $\beta(w)$。$\mathbb{R}P^3$ 的胞腔链复形由各维的一个胞腔 $e^k$ 构成，其边界映射为 $\partial_2(e^2) = 2e^1$。$w$ 可以由在 $e^1$ 上取值为1的1-维胞腔上链 $\phi_1$ 代表。我们在 $\mathbb{Z}_4$ 系数下提升 $\phi_1$ 为 $\tilde{\phi}_1$，令 $\tilde{\phi}_1(e^1)=1$。然后计算其余边缘 $d\tilde{\phi}_1 \in C^2(X; \mathbb{Z}_4)$：
$$ d\tilde{\phi}_1(e^2) = \tilde{\phi}_1(\partial_2 e^2) = \tilde{\phi}_1(2e^1) = 2 \cdot \tilde{\phi}_1(e^1) = 2 \in \mathbb{Z}_4 $$
注意到 $2 \in \mathbb{Z}_4$ 正是 $1 \in \mathbb{Z}_2$ 在包含映射 $i$ 下的像。因此，$d\tilde{\phi}_1 = i_*(\phi_2)$，其中 $\phi_2$ 是在 $e^2$ 上取值为1的2-维胞腔上链。这个 $\phi_2$ 代表了 $H^2(\mathbb{R}P^3; \mathbb{Z}_2)$ 的生成元，即 $w^2$。因此，我们得到 $\beta(w) = w^2$。[@problem_id:1641121]

### 斯廷罗德代数：一个更丰富的结构

对于 $\mathbb{Z}_2$ 系数上同调，存在着一族极为强大的上同调运算，称为 **斯廷罗德平方 (Steenrod squares)**，记作 $Sq^i$。这些运算 $Sq^i: H^n(X; \mathbb{Z}_2) \to H^{n+i}(X; \mathbb{Z}_2)$ 构成了一个丰富的代数结构，即 **斯廷罗德代数 (Steenrod algebra)** $\mathcal{A}_2$。

在介绍斯廷罗德平方之前，有必要先思考一个更朴素的“平方”运算，即杯积平方 $u \mapsto u \cup u$。这个映射一般不是群同态。例如，考虑4维环面 $T^4$ 的整系数上同调 $H^*(T^4; \mathbb{Z}) \cong \Lambda_{\mathbb{Z}}[\alpha_1, \alpha_2, \alpha_3, \alpha_4]$。令 $S(u) = u \cup u$。取 $x = \alpha_1 \cup \alpha_2$ 和 $y = \alpha_3 \cup \alpha_4$ 为 $H^2(T^4; \mathbb{Z})$ 中的两个元素。由于分次交换性，$\alpha_i \cup \alpha_j = -\alpha_j \cup \alpha_i$，我们有 $S(x) = x^2 = (\alpha_1 \cup \alpha_2)^2 = 0$ 和 $S(y) = y^2 = 0$。然而，
$$ S(x+y) = (x+y)^2 = x^2 + x \cup y + y \cup x + y^2 $$
由于 $x, y$ 都是偶数次类，它们满足交换律 $y \cup x = x \cup y$。因此 $S(x+y) = 2(x \cup y)$。这表明 $S(x+y) \neq S(x) + S(y)$。这个映射不是同态。[@problem_id:1641169]

斯廷罗德平方修正了这一缺陷，它们都是群同态，并满足一系列优美的公理：

1.  **自然性**：对任意连续映射 $f:X \to Y$，$f^* \circ Sq^i = Sq^i \circ f^*$。
2.  **线性**：$Sq^i(u+v) = Sq^i(u) + Sq^i(v)$。
3.  **$Sq^0$ 是恒等运算**：对任意类 $u$，有 $Sq^0(u) = u$。例如，在 $T^2$ 的 $\mathbb{Z}_2$ 上同调环 $H^*(T^2; \mathbb{Z}_2)$ 中，对任意元素 $u = c_0 \cdot 1 + c_1 \alpha + c_2 \beta + c_3 (\alpha \cup \beta)$，根据线性和公理，$Sq^0(u) = u$。[@problem_id:1641125]
4.  **次数公理 (Dimension axiom)**：若 $i > \deg(u)$，则 $Sq^i(u)=0$。
5.  **不稳定公理 (Instability axiom)**：若 $\deg(u) = i$，则 $Sq^i(u) = u \cup u = u^2$。
6.  **与博克斯坦的关系**：$Sq^1$ 等于由 $0 \to \mathbb{Z}_2 \to \mathbb{Z}_4 \to \mathbb{Z}_2 \to 0$ 诱导的博克斯坦同态 $\beta$。

这些公理本身就具有强大的约束力。例如，考虑3-维球面 $S^3$ 的 $\mathbb{Z}_2$ 上同调，它只在0次和3次非零。令 $g$ 为 $H^3(S^3; \mathbb{Z}_2)$ 的生成元。
-   $Sq^0(g) = g \neq 0$。
-   对于 $k \ge 1$，$Sq^k(g)$ 的次数为 $3+k$，而 $H^{3+k}(S^3; \mathbb{Z}_2)=0$，因此 $Sq^k(g)=0$。
-   特别地，$Sq^3(g) = g \cup g$。由于 $g \cup g \in H^6(S^3; \mathbb{Z}_2)=0$，这也与前述结论一致。
因此，对于 $S^3$ 上的3次生成元，唯一能产生非零结果的斯廷罗德平方只有 $Sq^0$。[@problem_id:1641145]

### 计算工具：嘉当公式

斯廷罗德平方之所以如此有用，一个关键原因是它们与上同调环的乘法结构（杯积）之间存在一个简单的关系，即 **嘉当公式 (Cartan formula)**：
$$ Sq^k(u \cup v) = \sum_{i+j=k} Sq^i(u) \cup Sq^j(v) $$
这个公式的强大之处在于，只要我们知道了斯廷罗德平方在一个上同调环的代数生成元上的作用，我们就可以通过归纳法计算出它在环中任意元素上的作用。

我们来看一个例子。考虑无限复射影空间 $\mathbb{C}P^\infty$，其 $\mathbb{Z}_2$ 上同调环是 $H^*(\mathbb{C}P^\infty; \mathbb{Z}_2) \cong \mathbb{Z}_2[x]$，其中 $x$ 是一个2次类。我们来计算 $Sq^2(x+x^2)$。
首先，根据线性， $Sq^2(x+x^2) = Sq^2(x) + Sq^2(x^2)$。
-   对于第一项，由于 $\deg(x)=2$，根据不稳定公理，$Sq^2(x) = x^2$。
-   对于第二项，我们使用嘉当公式计算 $Sq^2(x^2) = Sq^2(x \cup x)$：
    $$ Sq^2(x \cup x) = Sq^0(x) \cup Sq^2(x) + Sq^1(x) \cup Sq^1(x) + Sq^2(x) \cup Sq^0(x) $$
    我们知道 $Sq^0(x)=x$ 和 $Sq^2(x)=x^2$。而 $Sq^1(x)$ 的次数为 $\deg(x)+1=3$。由于 $H^3(\mathbb{C}P^\infty; \mathbb{Z}_2)=0$，我们必有 $Sq^1(x)=0$。代入上式，得到：
    $$ Sq^2(x^2) = x \cup x^2 + 0 \cup 0 + x^2 \cup x = x^3 + x^3 = 0 \pmod 2 $$
因此，最终结果为 $Sq^2(x+x^2) = x^2 + 0 = x^2$。[@problem_id:1641167]

嘉当公式在处理更复杂的表达式时同样有效。例如，考虑空间 $X = \mathbb{R}P^\infty \times \mathbb{R}P^\infty$，其上同调环为 $\mathbb{Z}_2[x_1, x_2]$，其中 $x_1, x_2$ 都是1次类。我们来计算 $Sq^2(x_1^2 x_2)$。
首先，我们需要知道 $Sq^i$ 在生成元 $x_1, x_2$ 上的作用：$Sq^0(x_j)=x_j$, $Sq^1(x_j)=x_j^2$，且当 $i>1$ 时 $Sq^i(x_j)=0$。
然后，计算 $Sq^i$ 在因子 $x_1^2$ 上的作用：
-   $Sq^0(x_1^2) = x_1^2$
-   $Sq^1(x_1^2) = Sq^1(x_1 \cup x_1) = Sq^1(x_1)x_1 + x_1Sq^1(x_1) = x_1^2 x_1 + x_1 x_1^2 = 2x_1^3 = 0$
-   $Sq^2(x_1^2) = Sq^1(x_1)Sq^1(x_1) + \dots = (x_1^2)(x_1^2) = x_1^4$
现在，应用嘉当公式到 $x_1^2 x_2$：
$$ Sq^2(x_1^2 x_2) = \sum_{i+j=2} Sq^i(x_1^2) \cup Sq^j(x_2) = Sq^0(x_1^2)Sq^2(x_2) + Sq^1(x_1^2)Sq^1(x_2) + Sq^2(x_1^2)Sq^0(x_2) $$
代入已知结果：
$$ Sq^2(x_1^2 x_2) = (x_1^2) \cdot 0 + 0 \cdot (x_2^2) + (x_1^4) \cdot (x_2) = x_1^4 x_2 $$
这个计算展示了如何系统地运用嘉当公式来分解和解决问题。[@problem_id:1641127]

### 代数结构：阿德姆关系式

斯廷罗德平方不仅是一系列独立的运算，它们之间的复合（作为函数的复合）也遵循着严格的代数法则。这些法则是斯廷罗德代数 $\mathcal{A}_2$ 的定义关系式，称为 **阿德姆关系式 (Adem relations)**。其一般形式为，若 $i  2j$，则：
$$ Sq^i Sq^j = \sum_{k=0}^{\lfloor i/2 \rfloor} \binom{j-k-1}{i-2k} Sq^{i+j-k} Sq^k $$
其中二项式系数在 $\mathbb{Z}_2$ 中取值。

这些关系式看起来可能很复杂，但它们揭示了斯廷罗德代数深刻的内在结构。最简单但非平凡的阿德姆关系式是当 $i=1, j=2$ 时，此时 $i  2j$ 成立。上述公式中 $k$ 只能取0，二项式系数为 $\binom{2-0-1}{1-0} = \binom{1}{1}=1$。因此，该关系式简化为：
$$ Sq^1 Sq^2 = Sq^3 $$
我们可以通过在一个具体的上同调类上进行计算来验证这个关系式。让我们在 $H^*(\mathbb{R}P^n; \mathbb{Z}_2) \cong \mathbb{Z}_2[a]/(a^{n+1})$ （其中 $n \ge 6$）的3次类 $a^3$ 上验证它。
首先计算左边：$Sq^1(Sq^2(a^3))$。
我们需要 $Sq^2(a^3) = Sq^2(a \cup a^2)$。利用嘉当公式：
$$ Sq^2(a \cup a^2) = Sq^0(a)Sq^2(a^2) + Sq^1(a)Sq^1(a^2) + Sq^2(a)Sq^0(a^2) $$
我们需要 $Sq^1(a^2)=0$ 和 $Sq^2(a^2)=a^4$（可以通过嘉当公式或公理得到）。另外 $Sq^2(a)=0$。代入得到：
$$ Sq^2(a^3) = a \cdot a^4 + a^2 \cdot 0 + 0 \cdot a^2 = a^5 $$
现在计算 $Sq^1(a^5)$。同样使用嘉当公式 $Sq^1(a^5) = Sq^1(a \cup a^4) = Sq^1(a)a^4 + a Sq^1(a^4) = a^2 \cdot a^4 + a \cdot 0 = a^6$。
因此，左边等于 $a^6$。

再计算右边：$Sq^3(a^3)$。
由于 $a^3$ 的次数为3，根据不稳定公理，$Sq^3(a^3) = (a^3)^2 = a^6$。
左右两边都等于 $a^6$，从而验证了关系式 $Sq^1 Sq^2 = Sq^3$ 在这个例子中的成立。[@problem_id:1641154]

总而言之，上同调运算为上同调理论增添了至关重要的第二层代数结构。从基本的博克斯坦同态到复杂的斯廷罗德代数，这些运算提供了强大的工具，使我们能够区分那些仅凭上同调环无法区分的拓扑空间，并对空间之间的映射施加了强有力的限制。它们是现代代数拓扑中不可或缺的一部分。