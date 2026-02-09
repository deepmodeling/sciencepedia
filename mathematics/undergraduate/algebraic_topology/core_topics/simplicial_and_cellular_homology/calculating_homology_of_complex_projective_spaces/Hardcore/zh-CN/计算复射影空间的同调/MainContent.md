## 引言
复射影空间 $\mathbb{C}P^n$ 是代数拓扑学与几何学中最为经典和重要的研究对象之一。它不仅结构优美，而且与数学和物理的众多分支有着深刻的联系。理解其拓扑性质的核心步骤之一便是精确计算其同调群。同调群作为一种基本的代数不变量，能够揭示空间的深层结构，为我们提供一把“代数钥匙”来解锁复杂的几何问题。本文旨在系统地阐述计算 $\mathbb{C}P^n$ 同调群的多种方法，并展示这些计算结果的广泛应用。

本文将引导读者从基础原理出发，逐步深入这一迷人的领域。在第一章“原理与机制”中，我们将从 $\mathbb{C}P^n$ 最基本的胞腔结构入手，利用胞腔同调这一强有力的工具直接计算出其同调群。随后，我们将通过相对同调的长正合序列和来自纤维丛理论的Gysin序列等不同视角，反复验证并加深对这一结果的理解。在第二章“应用与交叉学科联系”中，我们将展示这一看似抽象的计算成果如何成为解决具体问题的利器。我们将探讨如何利用同调群来区分不同的拓扑空间，分析连续映射的可能性，并揭示其与代数几何、微分几何的内在联系。最后，在第三章“动手实践”中，你将有机会通过解决一系列精心设计的问题，亲自运用所学理论，将抽象知识转化为具体的计算和论证能力。通过这一系列的学习，你不仅将掌握计算复射影空间同调的技巧，更能体会到代数拓扑是如何将代数方法与几何直观巧妙地结合在一起的。

## 原理与机制

在本章中，我们将深入探讨计算复射影空间 $\mathbb{C}P^n$ 同调群的原理和机制。复射影空间是代数拓扑和几何学中的核心研究对象。我们将从其最基本的拓扑构造——胞腔结构（CW complex structure）出发，通过几种不同的方法来揭示其深刻的同调特性。这些方法不仅能让我们得到最终的计算结果，更重要的是，它们将展示代数拓扑中一些最强大工具的实际应用，例如胞腔同调、长正合序列和纤维丛理论。

### 复射影空间的胞腔结构

理解一个拓扑空间的同调群，最直接的方法之一是分析其胞腔分解。复射影空间 $\mathbb{C}P^n$ 拥有一个非常简洁优美的 **CW复形** 结构。

从定义上看，$\mathbb{C}P^n$ 是 $\mathbb{C}^{n+1}$ 中所有过原点的复一维子空间（即复直线）构成的空间。这个空间可以被归纳地构造。$\mathbb{C}P^0$ 只是一个点，因为它对应 $\mathbb{C}^1$ 中唯一的过原点的复直线（原点自身）。然后，我们可以通过在一个 $2n$ 维圆盘 $D^{2n}$ 的边界 $S^{2n-1}$ 上定义一个贴合映射，将其贴合到 $\mathbb{C}P^{n-1}$ 上，从而得到 $\mathbb{C}P^n$。这个过程表明 $\mathbb{C}P^n$ 是由 $\mathbb{C}P^{n-1}$ 和一个 $2n$ 维胞腔 $e^{2n}$ 构成的。

通过重复这个过程，我们发现 $\mathbb{C}P^n$ 的CW复形结构极其简单：对于每一个从 $0$ 到 $n$ 的整数 $k$，它都恰好有一个 $2k$ 维的胞腔，而在所有奇数维度上都没有任何胞腔 [@problem_id:1635120]。

例如：
- $\mathbb{C}P^0$ 是一个 $0$ 维胞腔 $e^0$（一个点）。
- $\mathbb{C}P^1$ 是在 $\mathbb{C}P^0$ 上贴合一个 $2$ 维胞腔 $e^2$ 得到的。拓扑上，$\mathbb{C}P^1$ 同胚于二维球面 $S^2$ [@problem_id:1635092]。
- $\mathbb{C}P^2$ 是由 $e^0$, $e^2$, $e^4$ 三个偶数维胞腔构成的 [@problem_id:1635090]。

这个“只有偶数维胞腔”的特性是计算其同调群的关键。

### 通过胞腔同调计算

胞腔同调是为CW复形量身定制的强大计算工具。一个CW复形的胞腔链群 $C_k^{\text{cell}}(X; \mathbb{Z})$ 是一个自由阿贝尔群，其生成元与空间的 $k$ 维胞腔一一对应。

对于 $\mathbb{C}P^n$，其胞腔链群由其CW结构直接确定：
$$
C_k(\mathbb{C}P^n; \mathbb{Z}) \cong
\begin{cases}
\mathbb{Z}  & \text{若 } k \in \{0, 2, 4, \dots, 2n\} \\
0  & \text{其它情况}
\end{cases}
$$
胞腔同调群由链复形的同调 $H_k = \ker(d_k) / \operatorname{im}(d_{k+1})$ 给出，其中 $d_k: C_k \to C_{k-1}$ 是边界映射。

对于 $\mathbb{C}P^n$ 的链复形，所有 **边界映射 $d_k$ 均为零映射**。理由非常直接 [@problem_id:1635120] [@problem_id:1635099]：
- 如果 $k$ 是偶数，那么边界映射 $d_k: C_k \to C_{k-1}$ 的目标群 $C_{k-1}$ 是 $0$（因为 $k-1$ 是奇数），所以 $d_k$ 必然是零映射。
- 如果 $k$ 是奇数，那么边界映射 $d_k: C_k \to C_{k-1}$ 的定义域 $C_k$ 本身就是 $0$，所以 $d_k$ 也必然是零映射。

既然所有的边界映射都是零，那么对于任意 $k$：
- $\ker(d_k) = C_k$
- $\operatorname{im}(d_{k+1}) = 0$

因此，同调群的计算变得异常简单：
$$
H_k(\mathbb{C}P^n; \mathbb{Z}) \cong \frac{\ker(d_k)}{\operatorname{im}(d_{k+1})} \cong \frac{C_k}{0} \cong C_k
$$
这导出了复射影空间同调群的最终结构：
$$
H_k(\mathbb{C}P^n; \mathbb{Z}) \cong
\begin{cases}
\mathbb{Z}  & \text{若 } k \text{ 是偶数且 } 0 \le k \le 2n \\
0  & \text{其它情况}
\end{cases}
$$

例如，对于复射影平面 $\mathbb{C}P^2$，它有 $0,2,4$ 维胞腔，所以它的同调群为 [@problem_id:1635090]：
$H_0(\mathbb{C}P^2; \mathbb{Z}) \cong \mathbb{Z}$
$H_1(\mathbb{C}P^2; \mathbb{Z}) = 0$
$H_2(\mathbb{C}P^2; \mathbb{Z}) \cong \mathbb{Z}$
$H_3(\mathbb{C}P^2; \mathbb{Z}) = 0$
$H_4(\mathbb{C}P^2; \mathbb{Z}) \cong \mathbb{Z}$
所有更高维的同调群都为零。

### 一阶同调与基本群

我们刚刚看到，对于所有 $n \ge 1$，$\mathbb{C}P^n$ 的一阶同调群 $H_1(\mathbb{C}P^n; \mathbb{Z})$ 都是零。这个结果与空间的另一个基本拓扑不变量——基本群 $\pi_1(\mathbb{C}P^n)$——密切相关。

根据Hurewicz定理，对于任意路径连通的空间 $X$，其一阶同调群是其基本群的[阿贝尔化](@entry_id:140523)：$H_1(X; \mathbb{Z}) \cong \pi_1(X)^{\text{ab}}$。这意味着如果 $H_1(X; \mathbb{Z})=0$，那么 $\pi_1(X)$ 的任何阿贝尔商群都必然是平凡群，这强烈暗示了 $\pi_1(X)$ 可能是平凡群。

对于 $\mathbb{C}P^n$（当 $n \ge 1$ 时），我们可以通过其CW结构直接证明它的基本群是平凡的 [@problem_id:1635093]。一个CW复形的基本群完全由它的二维骨架（2-skeleton）决定。$\mathbb{C}P^n$ 的二维骨架是 $\mathbb{C}P^1$，它同胚于球面 $S^2$。由于 $\pi_1(S^2) = 0$，而向一个单连通空间附加维度大于等于3的胞腔不会改变其基本群，因此我们得出结论：
$$
\pi_1(\mathbb{C}P^n) = 0 \quad \text{对于所有 } n \ge 1
$$
一个基本群为平凡群的空间被称为 **单连通的 (simply connected)**。因此，所有 $\mathbb{C}P^n$ ($n \ge 1$) 都是单连通的。这个结果与我们计算出的 $H_1(\mathbb{C}P^n; \mathbb{Z}) = 0$ 完全一致，再次验证了我们结论的正确性。

### 通过长正合序列的归纳方法

除了直接的胞腔同调计算，我们还可以采用一种更具启发性的归纳方法，该方法依赖于相对同调和长正合序列。

如前所述，$\mathbb{C}P^n$ 是通过将一个 $2n$ 维胞腔 $e^{2n}$ 贴合到 $\mathbb{C}P^{n-1}$ 上得到的。这为我们提供了 **CW对 $(\mathbb{C}P^n, \mathbb{C}P^{n-1})$**。对于一个好的CW对 $(X, A)$，由商映射 $X \to X/A$（将子空间 $A$ 压缩为一个点）诱导的同调关系非常强大。具体来说，商空间 $\mathbb{C}P^n / \mathbb{C}P^{n-1}$ 同胚于 $2n$ 维球面 $S^{2n}$ [@problem_id:1635094]。

一个关键定理指出，相对同调群与商空间的约化同调群是同构的：
$$
H_k(\mathbb{C}P^n, \mathbb{C}P^{n-1}; \mathbb{Z}) \cong \tilde{H}_k(\mathbb{C}P^n / \mathbb{C}P^{n-1}; \mathbb{Z}) \cong \tilde{H}_k(S^{2n}; \mathbb{Z})
$$
由于球面 $S^{2n}$ 的约化同调只在 $2n$ 维非零（为 $\mathbb{Z}$），我们得到：
$$
H_k(\mathbb{C}P^n, \mathbb{C}P^{n-1}; \mathbb{Z}) \cong
\begin{cases}
\mathbb{Z}  & \text{若 } k = 2n \\
0  & \text{若 } k \neq 2n
\end{cases}
$$

现在，我们可以利用CW对 $(\mathbb{C}P^n, \mathbb{C}P^{n-1})$ 的同调长正合序列进行归纳论证 [@problem_id:1635098]。序列的一部分如下：
$$
\dots \to H_k(\mathbb{C}P^{n-1}) \xrightarrow{i_*} H_k(\mathbb{C}P^n) \xrightarrow{j_*} H_k(\mathbb{C}P^n, \mathbb{C}P^{n-1}) \to \dots
$$
- 对于 $k \le 2n-2$，长正合序列中围绕 $H_k(\mathbb{C}P^{n-1}) \to H_k(\mathbb{C}P^n)$ 的相对同调项 $H_{k+1}(\mathbb{C}P^n, \mathbb{C}P^{n-1})$ 和 $H_k(\mathbb{C}P^n, \mathbb{C}P^{n-1})$ 均为零。由正合性可知，包含映射 $i: \mathbb{C}P^{n-1} \hookrightarrow \mathbb{C}P^n$ 诱导的同态 $i_*: H_k(\mathbb{C}P^{n-1}) \to H_k(\mathbb{C}P^n)$ 是一个同构。这表明在维度不高于 $2n-2$ 的范围内，$\mathbb{C}P^n$ 的同调群与 $\mathbb{C}P^{n-1}$ 完全相同。

- 当 $k=2n$ 时，序列的相关部分是：
$$
H_{2n}(\mathbb{C}P^{n-1}) \to H_{2n}(\mathbb{C}P^n) \to H_{2n}(\mathbb{C}P^n, \mathbb{C}P^{n-1}) \to H_{2n-1}(\mathbb{C}P^{n-1})
$$
由于 $\mathbb{C}P^{n-1}$ 是一个 $2(n-1)$ 维的CW复形，它的 $2n$ 维和 $2n-1$ 维同调群都是零。代入我们已知的相对同调群 $H_{2n}(\mathbb{C}P^n, \mathbb{C}P^{n-1}; \mathbb{Z}) \cong \mathbb{Z}$，上述序列简化为：
$$
0 \to H_{2n}(\mathbb{C}P^n) \to \mathbb{Z} \to 0
$$
这表明 $H_{2n}(\mathbb{C}P^n; \mathbb{Z})$ 同构于 $\mathbb{Z}$。

结合归纳假设（$\mathbb{C}P^{n-1}$ 的同调群已知），这个论证精确地重现了我们之前用胞腔同调得到的结果。此外，这个视角还揭示了标准包含映射 $i: \mathbb{C}P^m \hookrightarrow \mathbb{C}P^n$ ($m  n$) 在同调层面上的作用：它在 $k \le 2m$ 的维度上诱导了同构 $i_*: H_k(\mathbb{C}P^m; \mathbb{Z}) \to H_k(\mathbb{C}P^n; \mathbb{Z})$。这意味着 $H_{2k}(\mathbb{C}P^m; \mathbb{Z})$ 的生成元被映射为 $H_{2k}(\mathbb{C}P^n; \mathbb{Z})$ 的生成元，体现了这些同调类的内在自然性 [@problem_id:1635080]。

### 庞加莱多项式

同调群的结构可以用一个简洁的代数对象来编码，即 **庞加莱多项式 (Poincaré polynomial)**。对于一个空间 $X$，其 $k$ 阶 **贝蒂数 (Betti number)** $b_k(X)$ 定义为同调群 $H_k(X; \mathbb{Z})$ 的秩。庞加莱多项式是这些贝蒂数的生成函数：
$$
P_X(t) = \sum_{k=0}^{\infty} b_k(X) t^k
$$
根据我们对 $\mathbb{C}P^n$ 同调群的计算，它的贝蒂数为：
$$
b_k(\mathbb{C}P^n) =
\begin{cases}
1   \text{若 } k \text{ 是偶数且 } 0 \le k \le 2n \\
0   \text{其它情况}
\end{cases}
$$
因此，$\mathbb{C}P^n$ 的庞加莱多项式是一个简单的几何级数 [@problem_id:1635127]：
$$
P_{\mathbb{C}P^n}(t) = t^0 + t^2 + t^4 + \dots + t^{2n} = \sum_{j=0}^{n} t^{2j}
$$
使用标准几何级数求和公式，我们可以将其写成一个优雅的闭合形式 [@problem_id:1635098]：
$$
P_{\mathbb{C}P^n}(t) = \frac{1 - (t^2)^{n+1}}{1 - t^2} = \frac{1 - t^{2(n+1)}}{1 - t^2}
$$
这个多项式完美地封装了 $\mathbb{C}P^n$ 所有同调群的秩的信息。

### 从纤维丛的视角：Gysin序列

最后，我们介绍一种源于微分几何和纤维丛理论的、更为深刻的方法——**Gysin序列**。这不仅能再次验证我们的计算，还能揭示 $\mathbb{C}P^n$ 与球面之间深刻的几何联系。

存在一个著名的主圆丛，称为 **Hopf纤维化 (Hopf fibration)**：
$$
S^1 \to S^{2n+1} \to \mathbb{C}P^n
$$
这里 $S^{2n+1}$ 是 $\mathbb{C}^{n+2}$ 中的单位球面，投影映射将球面上的一个点映到穿过该点的复直线上。

这个定向球面丛引出一个关于同调的长正合序列，即Gysin序列 [@problem_id:1635126]：
$$
\dots \to H_k(\mathbb{C}P^n; \mathbb{Z}) \xrightarrow{\frown e} H_{k-2}(\mathbb{C}P^n; \mathbb{Z}) \to H_{k-1}(S^{2n+1}; \mathbb{Z}) \to H_k(S^{2n+1}; \mathbb{Z}) \to \dots
$$
其中 $\frown e$ 表示与该丛的欧拉类 $e \in H^2(\mathbb{C}P^n; \mathbb{Z})$ 的cap积。

对于 $2  k  2n+1$ 的范围，序列中的球面同调群 $H_{k-1}(S^{2n+1}; \mathbb{Z})$ 和 $H_k(S^{2n+1}; \mathbb{Z})$ 均为零。因此，Gysin序列在该范围内给出了一个短正合序列：
$$
0 \to H_k(\mathbb{C}P^n; \mathbb{Z}) \xrightarrow{\frown e} H_{k-2}(\mathbb{C}P^n; \mathbb{Z}) \to 0
$$
这意味着对于 $2  k  2n+1$，映射 $\frown e$ 是一个同构。这个同构完美地解释了 $\mathbb{C}P^n$ 同调群的周期性结构：
$$
H_k(\mathbb{C}P^n; \mathbb{Z}) \cong H_{k-2}(\mathbb{C}P^n; \mathbb{Z})
$$
从已知的 $H_0(\mathbb{C}P^n; \mathbb{Z}) \cong \mathbb{Z}$ 和 $H_1(\mathbb{C}P^n; \mathbb{Z})=0$ 出发，我们可以利用这个同构关系，通过归纳法轻松地推导出所有同调群的结构，再次得到我们熟悉的结果。这个视角展示了代数拓扑中不同理论工具的内在和谐与强大威力。