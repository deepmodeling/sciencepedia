## 引言
奇异值分解（SVD）是数值线性代数中一个极其强大的工具，在数据压缩、信号处理和机器学习等领域有着广泛应用。然而，对于当今科学与工程中常见的大型稀疏矩阵，计算完整的SVD在计算和内存上都代价高昂，甚至不可行。这一挑战催生了对高效迭代方法的需求，其中，Lanczos双对角化方法脱颖而出，成为计算部分SVD，特别是最大奇异值的首选算法之一。

本文旨在全面剖析使用Lanczos双对角化计算SVD的核心思想与实践。在“原理与机制”一章中，我们将深入探讨算法的数学推导、与Krylov子空间的深刻联系，以及其收敛性和误差估计的机制。接着，在“应用与跨学科联系”一章中，我们将展示该方法如何在数据科学等领域发挥作用，并讨论移位求逆、分块等高级算法扩展。最后，通过一系列精心设计的“动手实践”练习，读者将有机会将理论知识应用于具体问题，从而巩固对残差计算、误差界定等关键概念的理解。

## 原理与机制

在上一章引言的基础上，本章深入探讨了利用 Lanczos 双对角化计算大型稀疏矩阵奇异值分解（SVD）的核心原理与底层机制。我们将系统地阐述算法的推导过程，分析其收敛特性，并探讨其与数值分析中其他深刻概念（如 Krylov 子空间、Ritz-Galerkin 方法和 Gauss Quadrature）的内在联系。通过对这些机制的剖析，读者将能够理解该方法的威力所在，并掌握其在实际应用中的关键考量。

### Lanczos 双对角化过程

Lanczos 双对角化是一个迭代过程，它能够将一个大型矩阵 $A \in \mathbb{R}^{m \times n}$ 投影到一个极小的双对角矩阵上，从而将原矩阵的谱信息（奇异值）浓缩到这个小矩阵中。该过程主要有两种形式：右始式（right-start）和左始式（left-start）。此处，我们以右始式为例进行阐述。

给定一个初始单位向量 $v_1 \in \mathbb{R}^n$，算法通过一个三项递推关系，逐步构建两个正交向量集 $\{v_1, v_2, \dots\}$ 和 $\{u_1, u_2, \dots\}$。经过 $k$ 步迭代，该过程生成两个矩阵 $V_k = [v_1, \dots, v_k] \in \mathbb{R}^{n \times k}$ 和 $U_{k+1} = [u_1, \dots, u_{k+1}] \in \mathbb{R}^{m \times (k+1)}$，它们的列向量均为单位正交向量。同时，算法生成一个 $(k+1) \times k$ 的下双对角矩阵 $\widehat{B}_k$，其对角线元素为 $\alpha_i > 0$，次对角线元素为 $\beta_i > 0$：
$$
\widehat{B}_k = \begin{pmatrix}
\alpha_1    \\
\beta_2 & \alpha_2   \\
 & \beta_3 & \ddots  \\
 & & \ddots & \alpha_k \\
 & & & \beta_{k+1}
\end{pmatrix}
$$
这些矩阵和向量满足以下核心关系：
$$
A V_k = U_{k+1} \widehat{B}_k
$$
$$
A^\top U_{k+1} = V_k \widehat{B}_k^\top + \beta_{k+1} v_{k+1} e_{k+1}^\top
$$
其中 $e_{k+1} \in \mathbb{R}^{k+1}$ 是第 $k+1$ 个标准基向量。第二式中的 $\beta_{k+1} v_{k+1} e_{k+1}^\top$ 项代表了在第 $k$ 步之后，子空间尚未捕捉到的“残余”信息。

### Krylov 子空间联系

Lanczos 双对角化的核心在于它与 **Krylov 子空间** 方法的深刻联系。将上述两式联立，可以揭示其本质。从第一式可得 $U_k^\top A V_k = B_k$，其中 $B_k$ 是 $\widehat{B}_k$ 的前 $k \times k$ 主子矩阵。将此关系代入第二式的转置，我们发现：
$$
V_k^\top A^\top U_k = B_k^\top
$$
进而可以推导出：
$$
V_k^\top (A^\top A) V_k = (V_k^\top A^\top U_k) (U_k^\top A V_k) = B_k^\top B_k
$$
令 $T_k = B_k^\top B_k$，$T_k$ 是一个 $k \times k$ 的对称三对角矩阵。上式表明，$T_k$ 是矩阵 $A^\top A$ 在 Krylov 子空间 $\mathcal{K}_k(A^\top A, v_1) = \mathrm{span}\{v_1, (A^\top A)v_1, \dots, (A^\top A)^{k-1}v_1\}$ 上的 **Rayleigh-Ritz 投影**。这意味着，Lanczos 双对角化过程隐式地对 $A^\top A$（或 $AA^\top$）执行了对称 Lanczos 算法。因此，$T_k$ 的特征值（称为 **Ritz 值**）是 $A^\top A$ 特征值的近似，而 $T_k$ 的特征向量经过 $V_k$ 变换后得到的向量（称为 **Ritz 向量**）则是 $A^\top A$ 特征向量（即 $A$ 的右奇异向量）的近似。

### Ritz 逼近与 Petrov-Galerkin 条件

算法的核心思想是通过计算小尺寸双对角矩阵 $\widehat{B}_k$ 的奇异值来逼近原矩阵 $A$ 的奇异值。设 $(\sigma, s, t)$ 是 $\widehat{B}_k$ 的一个奇异三元组，满足 $\widehat{B}_k t = \sigma s$ 和 $\widehat{B}_k^\top s = \sigma t$，其中 $\sigma \geq 0$, $s \in \mathbb{R}^{k+1}$, $t \in \mathbb{R}^{k}$。

我们可以将这个近似解“提升”回原始空间，构造 $A$ 的近似奇异三元组，即 **Ritz 三元组** $(\sigma, u, v)$：
$$
u = U_{k+1} s, \quad v = V_k t
$$
这两个近似向量 $u$ 和 $v$ 分别被称为左、右 Ritz 向量，而 $\sigma$ 则被称为 Ritz 奇异值。

一个重要的问题是，这些 Ritz 向量满足什么样的最优性条件？为此，我们考察左、右残差 $r_L = A v - \sigma u$ 和 $r_R = A^\top u - \sigma v$。根据 Lanczos 关系式进行推导 [@problem_id:3539932]：
对于左残差 $r_L$：
$$
r_L = A(V_k t) - \sigma(U_{k+1} s) = (AV_k)t - \sigma U_{k+1} s = (U_{k+1} \widehat{B}_k)t - \sigma U_{k+1} s = U_{k+1}(\widehat{B}_k t - \sigma s) = 0
$$
这个结果表明，左残差恒为零。这源于 Ritz 向量的构造方式，它满足所谓的 **Petrov-Galerkin 条件** $U_{k+1}^\top (A v - \sigma u) = 0$。这意味着近似解的残差与左测试子空间 $\mathrm{span}(U_{k+1})$ 正交。

然而，右残差 $r_R$ 通常不为零 [@problem_id:3539929]：
$$
r_R = A^\top(U_{k+1} s) - \sigma(V_k t) = (A^\top U_{k+1})s - \sigma V_k t = (V_k \widehat{B}_k^\top + \beta_{k+1} v_{k+1} e_{k+1}^\top)s - \sigma V_k t
$$
$$
= V_k(\widehat{B}_k^\top s) + \beta_{k+1}(e_{k+1}^\top s)v_{k+1} - \sigma V_k t = V_k(\sigma t) + \beta_{k+1}(e_{k+1}^\top s)v_{k+1} - \sigma V_k t = \beta_{k+1}(e_{k+1}^\top s)v_{k+1}
$$
其中 $e_{k+1}^\top s$ 是 $\widehat{B}_k$ 的左奇异向量 $s$ 的最后一个分量。

### 收敛性分析与误差估计

#### 作为终止条件的残差范数

上述推导揭示了一个至关重要的事实：右残差的范数提供了一个可计算的、廉价的误差估计。其二范数为：
$$
\|r_R\|_2 = \|A^\top u - \sigma v\|_2 = \beta_{k+1} |e_{k+1}^\top s|
$$
这个公式 [@problem_id:3539929] 是 Lanczos SVD 算法中**终止判据**的理论基础。当计算得到的 Ritz 奇异值 $\sigma$ 和 Ritz 向量 $u, v$ 足够好时，其残差范数 $\|r_R\|_2$ 将会变得非常小。在实践中，我们可以监控相对残差 $\|r_R\|_2 / \sigma$，当它小于预设的容差 $\epsilon$ 时，便可认为 Ritz 三元组 $(\sigma, u, v)$ 已经收敛，并停止迭代。

例如，在一个 $k$ 步计算后，若得到下一个次对角元 $\beta_k = 1.7 \times 10^{-9}$，最大 Ritz 奇异值 $\widehat{\sigma}_1 = 3.2$，且对应的左奇异向量 $\widehat{p}_1$ 的最后一个分量为 $e_k^\top \widehat{p}_1 = 0.45$，则对应的相对残差可以被精确计算为 $\rho_1 = \frac{\beta_k |e_k^\top \widehat{p}_1|}{\widehat{\sigma}_1} = \frac{(1.7 \times 10^{-9})|0.45|}{3.2} \approx 2.391 \times 10^{-10}$。这表明该 Ritz 三元组已经是一个非常高质量的近似解。

#### 收敛性质与谱隙

Lanczos 方法的收敛速度与矩阵的谱分布密切相关，特别是**谱隙**的大小。

*   **极端奇异值**：对于矩阵 $A$ 的最大奇异值 $\sigma_1$，其收敛速度非常快，特别是当它与次大奇异值 $\sigma_2$ 有较大差距时（即 $\sigma_1 - \sigma_2$ 较大）。收敛率通常是几何级的，其速率与一个依赖于谱隙的 Chebyshev 多项式相关。

*   **内部奇异值**：对于内部的奇异值，Lanczos 方法的收敛通常很慢。这是因为 Krylov 子空间是通过 $A^\top A$ 的幂次构建的，这种方式天然地放大了与最大特征值相关联的分量。需要非常高阶的多项式（即非常多的迭代步数）才能精确地分离出内部的谱信息。

*   **聚集奇异值**：如果一组奇异值 $\sigma_j, \dots, \sigma_{j+m-1}$ 形成一个紧密的**簇**，并且这个簇与谱的其他部分（如 $\sigma_{j-1}$ 和 $\sigma_{j+m}$）有明显的分离，那么 Lanczos 算法会首先快速地捕捉到与整个簇对应的 $m$ 维奇异子空间。然而，要区分簇内部的各个奇异值和奇异向量则非常困难，收敛会很慢。Ritz 值会整体趋向于这个簇，然后在后续迭代中慢慢“分裂”开来，收敛到各自对应的真实奇异值。

#### 后验误差界

除了逐个奇异值的残差，我们还可以估计整个低秩近似的误差。假设经过 $k$ 步 bidiagonalization，我们得到了 $B_k$ 的 SVD，并取其前 $r$ 个奇异三元组构造了 $A$ 的一个秩-$r$ 近似 $\widehat{A}_r = \widehat{U}_r \Sigma_r \widehat{V}_r^\top$。那么，这个近似的谱范数误差 $\|A - \widehat{A}_r\|_2$ 是多少呢？

我们可以推导出一个后验误差上界 [@problem_id:3539884]。这个误差可以分解为两部分：一部分是 $A$ 与其在子空间 $\mathrm{span}(U_k) \times \mathrm{span}(V_k)$ 上的投影 $A_k = P_U A P_V$ 之间的误差，另一部分是 $A_k$ 与其秩-$r$ 近似 $\widehat{A}_r$ 之间的误差。
$$
\|A - \widehat{A}_r\|_2 \le \|A - A_k\|_2 + \|A_k - \widehat{A}_r\|_2
$$
第一项，即投影误差，可以被界定为 $\|A - A_k\|_2 \le \|(I - P_U)A\|_2 + \|A(I-P_V)\|_2$。这两个范数在实践中可以通过Lanczos过程中的残差信息来估计。第二项，即子空间内的近似误差，根据 Eckart-Young-Mirsky 定理，等于 $B_k$ 的第 $r+1$ 个奇异值 $\sigma_{r+1}(B_k)$。综合起来，我们得到一个非常有用的误差界：
$$
\|A - \widehat{A}_r\|_2 \le \|(I - P_U)A\|_2 + \|A(I-P_V)\|_2 + \sigma_{r+1}(B_k)
$$
这个界告诉我们，近似误差由两部分贡献：Lanczos 子空间捕捉 $A$ 的能力（由投影残差范数衡量）以及在子空间内进行截断的误差（由 $B_k$ 的被忽略的奇异值衡量）。

### 高级视角

#### 与 Gauss Quadrature 的联系

Lanczos 过程与数值积分中的 **Gauss Quadrature** 理论有着惊人的联系 [@problem_id:3539880]。对于任意函数 $f$，矩阵函数 $v_1^\top f(A^\top A) v_1$ 可以被看作是一个黎曼-斯蒂尔切斯积分 $\int f(\lambda) d\mu(\lambda)$，其中 $\mu$是由初始向量 $v_1$ 和 $A^\top A$ 的谱定义的测度。

对称 Lanczos 算法（等价于 Lanczos 双对角化中的 $T_k = B_k^\top B_k$）生成的 $T_k$ 的特征值（Ritz 值）和相应特征向量的分量，恰好构成了对上述积分的 $k$ 点 Gauss Quadrature 法则的节点和权重。Gauss Quadrature 法则对于次数不超过 $2k-1$ 的多项式是精确的。

这个深刻的联系带来了实际的应用。例如，矩阵的 Frobenius 范数平方 $\|A\|_F^2 = \mathrm{trace}(A^\top A)$。如果我们选择一个特殊的起始向量，如 $v_1 = \frac{1}{\sqrt{n}}\mathbf{1}$（其中 $\mathbf{1}$ 是全1向量），并且 $A^\top A$ 的特征向量恰好是标准基，那么有 $\mathrm{trace}(A^\top A) = n \cdot v_1^\top (A^\top A) v_1$。由于 $v_1^\top (A^\top A) v_1$ 是一个关于 $A^\top A$ 的线性函数（1次多项式），Gauss Quadrature (for $k \ge 1$) 是精确的，即 $v_1^\top (A^\top A) v_1 = (T_k)_{1,1}$。因此，我们可以用 $n \cdot (T_k)_{1,1}$ 来估计总能量 $\|A\|_F^2$。

更进一步，总能量减去已捕獲的能量（即 $T_k$ 的特征值之和）就可以得到“尾部能量”的估计：$\widehat{E}_{\mathrm{tail}}(k) = n (T_k)_{1,1} - \mathrm{trace}(T_k)$。这为评估低秩近似捕获了多少原矩阵的“能量”提供了一个廉价的手段。

#### 计算双对角矩阵的 SVD

Lanczos 过程的最后一步是计算小双对角矩阵 $B_k$ 的奇异值。虽然这一步通常通过数值方法（如 QR 迭代或分治法）高效完成，但考察一个可解析的例子有助于加深理解 [@problem_id:3539923]。

考虑一个 $(n+1) \times n$ 的下双对角矩阵 $B$，其对角元均为 $a>0$，次对角元均为 $b>0$。要计算其奇异值，我们需求解其 Gram 矩阵 $T = B^\top B$ 的特征值。$T$ 是一个 $n \times n$ 的对称三对角 Toeplitz 矩阵：
$$
T = \begin{pmatrix}
a^2+b^2 & ab &  &   \\
ab & a^2+b^2 & \ddots &  \\
 & \ddots & \ddots & ab \\
 & & ab & a^2+b^2
\end{pmatrix}
$$
这类矩阵的特征值有著名的解析表达式：
$$
\lambda_j = (a^2+b^2) + 2ab \cos\left(\frac{j\pi}{n+1}\right), \quad j = 1, 2, \dots, n
$$
$B$ 的奇异值 $\sigma_j$ 就是 $\sqrt{\lambda_j}$。要找到最大的奇异值 $\sigma_{\max}$，我们只需找到最大的特征值 $\lambda_{\max}$。由于 $a, b > 0$，这等价于最大化 $\cos\left(\frac{j\pi}{n+1}\right)$。当 $j=1$ 时，该项取最大值。因此，最大奇异值为：
$$
\sigma_{\max} = \sqrt{a^2+b^2 + 2ab \cos\left(\frac{\pi}{n+1}\right)}
$$
这个例子清晰地展示了从双对角矩阵 $B$ 到三对角矩阵 $T=B^\top B$，再到求解其谱的完整路径。

### 实践考量与算法变体

#### 起始向量的角色

Lanczos 算法的性能很大程度上取决于起始向量 $v_1$ 的选择。为了使算法快速收敛到某个特定的奇异向量 $v_j$，起始向量 $v_1$ 中必须包含 $v_j$ 的分量。如果 $v_1$ 恰好与某个奇异子空间正交，那么算法在精确算术下永远无法找到该子空间中的奇异向量。

在实践中，我们通常不知道真实的奇异向量。一个普遍且有效的策略是使用**随机向量**作为 $v_1$。一个随机向量以极高的概率在所有奇异向量方向上都有非零分量。我们可以更定量地分析这一点 [@problem_id:3539902]。假设 $v_1$ 是一个随机向量，其协方差矩阵在 $A$ 的右奇异向量基 $V$下是对角的，$\operatorname{Cov}(v_1) = V \operatorname{diag}(\tau_1, \dots, \tau_n) V^\top$，其中 $\sum \tau_i = 1$。$\tau_i$ 代表了 $v_1$ 在第 $i$ 个奇异向量方向上的期望能量。那么，$v_1$ 在前 $k$ 个奇异向量张成的子空间上的投影的期望能量为：
$$
\mathbb{E}\|V_k^\top v_1\|^2 = \sum_{i=1}^k \tau_i
$$
这个结果直观地表明，如果起始向量的“能量”更多地分布在主奇异方向上（即 $\tau_1, \dots, \tau_k$ 较大），Lanczos 过程就能更快地捕获这些方向。均匀分布的随机向量（所有 $\tau_i$ 相等）是一种无偏的选择，确保了对所有奇异模式的公平探索。

#### 处理矩形矩阵的非对称性

前面我们看到，右始式 Lanczos 过程的左右残差表现出非对称性（$\|r_L\|_2=0$ 而 $\|r_R\|_2 \ne 0$）。这种非对称性在处理高度矩形的矩阵（即 $m \gg n$ 或 $n \gg m$）时可能会带来问题，导致左右 Ritz 向量的收敛速度看起来不平衡。

有几种策略可以缓解这个问题 [@problem_id:3539932]：

1.  **矩阵均衡 (Equilibration)**：在运行 Lanczos 之前，对 $A$ 进行对角缩放，即 $A \to D_r A D_c$，其中 $D_r, D_c$ 是对角矩阵。目标是使新矩阵的行范数和列范数大致相等。这通常能使生成的双对角元 $\alpha_i, \beta_i$ 的量级更加均衡，从而改善收敛行为。计算完成后，再将结果映射回原始坐标系。

2.  **在 $A^\top$ 上运行**：如果 $n \gg m$，在 $A$上运行右始式 Lanczos 不如在 $A^\top$ 上运行高效。在 $A^\top$ 上运行右始式 Lanczos 等价于在 $A$ 上运行左始式 Lanczos。这将交换左右残差的角色，使得右残差（相对于 $A$）为零，而左残差非零。通过在 $A$ 和 $A^\top$ 之间切换，可以平衡对左右奇异向量的精化。

值得注意的是，一个看似直接的平衡方法——构造法方程 $A^\top A$ 并对其使用对称 Lanczos 算法——是**绝对应该避免**的。虽然这在理论上等价，但在数值上，计算 $A^\top A$ 会将矩阵的条件数平方 ($\kappa(A^\top A) = \kappa(A)^2$)，这会严重破坏与小奇异值相关的信息，导致数值不稳定。Lanczos 双对角化直接作用于 $A$，从而避免了这种数值灾难。

#### 与其他方法的比较：Lanczos vs. Jacobi-Davidson

Lanczos 双对角化是计算若干个**最大**奇异值的首选方法之一。但如果目标是计算某个指定 target $\tau$ 附近的**内部**奇异值，它的效率就会很低。

在这种情况下，**Jacobi-Davidson (JD) 方法** 通常是更好的选择 [@problem_id:3539928]。JD 方法通过求解一个所谓的**校正方程**来迭代地扩展其搜索子空间。对于 SVD 问题，校正方程的形式近似为：
$$
(A^\top A - \tau^2 I) t \approx -r
$$
其中 $r$ 是当前近似解的残差，$t$ 是寻求的校正向量。当目标 $\tau$ 接近某个奇异值 $\sigma_j$ 时，矩阵 $(A^\top A - \tau^2 I)$ 是近奇异的。通过 (近似地) 求解这个病态的线性系统，得到的解 $t$ 会被放大，且主要富含目标奇异向量 $v_j$ 的方向。

JD 方法的强大之处在于它可以集成**预条件子 (preconditioner)** $M \approx (A^\top A - \tau^2 I)^{-1}$ 来高效地求解校正方程。如果能找到一个好的预条件子，JD 方法可以非常快速地收敛到内部奇异值。

总结来说：
*   对于计算**极端（最大）奇异值**，尤其是在没有好的预条件子的情况下，Lanczos 双对角化是高效且鲁棒的选择。
*   对于计算**内部奇异值**，特别是当存在有效的预条件子时，Jacobi-Davidson 方法通常具有显著的性能优势。