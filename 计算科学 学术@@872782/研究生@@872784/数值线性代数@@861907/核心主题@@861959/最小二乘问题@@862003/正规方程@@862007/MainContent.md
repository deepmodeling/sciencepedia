## 引言
正规方程是[数值线性代数](@entry_id:144418)和[科学计算](@entry_id:143987)中的一个基石概念，为求解线性最小二乘问题提供了最直接的代数方法。在处理超定线性系统 $A\mathbf{x} = \mathbf{b}$ 时，精确解通常不存在。最小二乘法通过寻找一个使[残差范数](@entry_id:754273) $\|A\mathbf{x} - \mathbf{b}\|$ 最小化的解 $\mathbf{x}$ 来解决这一问题，而正规方程正是实现这一目标的[经典途径](@entry_id:198762)。然而，其理论上的优雅性背后隐藏着实践中的数值陷阱，理解其原理与局限性对于任何计算科学家都至关重要。

本文将系统性地剖析[正规方程](@entry_id:142238)。在“原理与机制”一章中，我们将从几何投影的视角推导该方程，并分析其解的性质与[数值稳定性](@entry_id:146550)。接着，“应用与跨学科联系”一章将展示正规方程如何在[统计建模](@entry_id:272466)、[机器学习正则化](@entry_id:636017)以及复杂优化算法中扮演核心角色。最后，“动手实践”部分将通过具体的编程练习，让读者亲身体验其数值特性，并与更稳健的算法进行对比。

## 原理与机制

在理解任何计算方法时，不仅要掌握其操作步骤，更要洞悉其背后的数学原理和内在机制。[正规方程](@entry_id:142238)作为求解线性[最小二乘问题](@entry_id:164198)的经典方法，其深刻之处在于它将一个[优化问题](@entry_id:266749)转化为一个线性代数问题，其背后蕴含着丰富的几何直观和数值考量。本章将深入探讨[正规方程](@entry_id:142238)的基础原理，从几何投影的视角推导其形式，辨析解的性质，并剖析其在有限精度计算环境下的数值特性。

### [最小二乘问题](@entry_id:164198)的几何诠释：正交投影

线性最小二乘问题的核心目标是，对于一个给定的线性系统 $A\mathbf{x}=\mathbf{b}$，其中 $A \in \mathbb{R}^{m \times n}$，$b \in \mathbb{R}^m$，当该系统无解时（通常在 $m > n$ 的[超定系统](@entry_id:151204)中发生），寻找一个最优的近似解 $\mathbf{x}_{\star}$。这里的“最优”定义为能够最小化[残差向量](@entry_id:165091) $\mathbf{r} = A\mathbf{x} - \mathbf{b}$ 的[欧几里得范数](@entry_id:172687)，即最小化[目标函数](@entry_id:267263) $f(\mathbf{x}) = \|A\mathbf{x} - \mathbf{b}\|_{2}^{2}$。

这个[优化问题](@entry_id:266749)有一个优美的几何解释。向量集合 $\{A\mathbf{x} \mid \mathbf{x} \in \mathbb{R}^n\}$ 构成了矩阵 $A$ 的**[列空间](@entry_id:156444)**（或称为**值域**），记作 $\operatorname{range}(A)$。这是一个 $\mathbb{R}^m$ 中的 $n$ 维或更低维的[子空间](@entry_id:150286)。最小二乘问题等价于在[子空间](@entry_id:150286) $\operatorname{range}(A)$ 中寻找一个向量 $\mathbf{p}$，使其与向量 $\mathbf{b}$ 的距离最近。

根据有限维[内积空间](@entry_id:271570)中的**[投影定理](@entry_id:142268)**，对于任何[闭子空间](@entry_id:267213) $S \subseteq \mathbb{R}^m$ 和任意向量 $\mathbf{b} \in \mathbb{R}^m$，存在唯一的向量 $\mathbf{p}_{\star} \in S$ 是 $\mathbf{b}$ 在 $S$ 上的最佳逼近。这个最佳逼近点 $\mathbf{p}_{\star}$ 正是 $\mathbf{b}$ 在 $S$ 上的**正交投影**。其充要条件是，差向量（即残差）$\mathbf{b} - \mathbf{p}_{\star}$ 必须与[子空间](@entry_id:150286) $S$ 本身正交 [@problem_id:3592597]。

将此定理应用于最小二乘问题，令 $S = \operatorname{range}(A)$，最优解 $\mathbf{x}_{\star}$ 对应的向量 $A\mathbf{x}_{\star}$ 必然是 $\mathbf{b}$ 在 $\operatorname{range}(A)$ 上的正交投影。因此，在最优解处，残差向量 $\mathbf{r}_{\star} = \mathbf{b} - A\mathbf{x}_{\star}$ 必须与 $\operatorname{range}(A)$ 中的任何向量正交。[@problem_id:3592637]

这个**[正交性条件](@entry_id:168905)**是导出[正规方程](@entry_id:142238)的关键。一个向量与整个[子空间](@entry_id:150286) $\operatorname{range}(A)$ 正交，等价于它与该[子空间](@entry_id:150286)的一组基正交。矩阵 $A$ 的各列构成了 $\operatorname{range}(A)$ 的一组[生成集](@entry_id:156303)。因此，残差 $\mathbf{r}_{\star}$ 必须与 $A$ 的每一列都正交。在标准的欧几里得[内积](@entry_id:158127) $\langle\mathbf{u}, \mathbf{v}\rangle = \mathbf{u}^\top\mathbf{v}$下，这个条件可以写作：
$$ A^\top \mathbf{r}_{\star} = \mathbf{0} $$
将 $\mathbf{r}_{\star} = \mathbf{b} - A\mathbf{x}_{\star}$ 代入，我们便得到了著名的**正规方程**（Normal Equations）：
$$ A^\top (\mathbf{b} - A\mathbf{x}_{\star}) = \mathbf{0} $$
整理后得到其[标准形式](@entry_id:153058)：
$$ (A^\top A) \mathbf{x}_{\star} = A^\top \mathbf{b} $$
这个方程将一个[优化问题](@entry_id:266749)转化为了一个 $n \times n$ 的方阵[线性系统](@entry_id:147850)求解问题。值得注意的是，这个推导过程也可以通过微积分完成。目标函数 $f(\mathbf{x}) = \|A\mathbf{x} - \mathbf{b}\|_{2}^{2} = (A\mathbf{x} - \mathbf{b})^\top(A\mathbf{x} - \mathbf{b})$ 是一个凸函数，其梯度为 $\nabla f(\mathbf{x}) = 2A^\top(A\mathbf{x} - \mathbf{b})$。令梯度为零即可得到相同的正规方程 [@problem_id:3592614]。

几何上的[正交性原理](@entry_id:153755)还揭示了一个深刻的性质：[最小二乘解](@entry_id:152054)对于那些正交于 $\operatorname{range}(A)$ 的扰动是不变的。根据[线性代数基本定理](@entry_id:190797)，$\operatorname{range}(A)$ 的[正交补](@entry_id:149922)是 $A^\top$ 的零空间，即 $\operatorname{range}(A)^\perp = \mathcal{N}(A^\top)$。如果我们将向量 $\mathbf{b}$ 替换为 $\mathbf{b} + \mathbf{n}$，其中 $\mathbf{n} \in \mathcal{N}(A^\top)$，那么 $\mathbf{b} + \mathbf{n}$ 在 $\operatorname{range}(A)$ 上的[正交投影](@entry_id:144168)与 $\mathbf{b}$ 的投影完全相同。因此，[最小二乘解](@entry_id:152054) $\mathbf{x}_{\star}$ 保持不变。这在数值实验中可以清晰地观察到 [@problem_id:3592597]。

### [正规方程](@entry_id:142238)的解

[正规方程](@entry_id:142238) $(A^\top A) \mathbf{x} = A^\top \mathbf{b}$ 的解的性质取决于系数矩阵 $G = A^\top A$。这个矩阵始终是**对称半正定**的，因为对于任意向量 $\mathbf{z} \in \mathbb{R}^n$，$\mathbf{z}^\top G \mathbf{z} = \mathbf{z}^\top (A^\top A) \mathbf{z} = (A\mathbf{z})^\top(A\mathbf{z}) = \|A\mathbf{z}\|_2^2 \ge 0$。

解的存在性和唯一性与矩阵 $A$ 的秩密切相关：

1.  **存在性**：[最小二乘解](@entry_id:152054) $\mathbf{x}_{\star}$ 总是存在的。这是因为 $\operatorname{range}(A)$ 是一个有限维[子空间](@entry_id:150286)，因此是[闭集](@entry_id:136446)，保证了正交投影的存在性。代数上，这也与 $A^\top \mathbf{b}$始终位于 $A^\top A$ 的值域内这一事实相符。

2.  **唯一性**：[最小二乘解](@entry_id:152054) $\mathbf{x}_{\star}$ 是否唯一，取决于 $A^\top A$ 是否可逆。$A^\top A$ 可逆当且仅当它是**正定**的，这又等价于 $\|A\mathbf{z}\|_2^2 > 0$ 对所有非零 $\mathbf{z}$ 成立。这正是矩阵 $A$ **列满秩**（即 $A$ 的列线性无关）的条件。
    *   如果 $\operatorname{rank}(A) = n$（列满秩），则 $A^\top A$ 是[对称正定矩阵](@entry_id:136714)，因而可逆。此时，正规方程存在唯一解：$\mathbf{x}_{\star} = (A^\top A)^{-1} A^\top \mathbf{b}$。
    *   如果 $\operatorname{rank}(A)  n$（列亏秩），则 $A^\top A$ 是奇异的。此时，[最小二乘解](@entry_id:152054)不唯一。若 $\mathbf{x}_p$ 是一个特解，则通解的集合构成一个仿射[子空间](@entry_id:150286) $\mathbf{x}_p + \mathcal{N}(A)$，其中 $\mathcal{N}(A)$ 是 $A$ 的[零空间](@entry_id:171336) [@problem_id:3592637]。尽管 $\mathbf{x}_{\star}$ 不唯一，但其在 $\operatorname{range}(A)$ 上的像 $A\mathbf{x}_{\star}$（即 $\mathbf{b}$ 的投影）是唯一的。

一个特别有启发性的例子是当矩阵 $A$ 的列是**标准正交**的。在这种情况下，$A^\top A = I_n$（$n \times n$ 的[单位矩阵](@entry_id:156724)）。[正规方程](@entry_id:142238) $A^\top A \mathbf{x} = A^\top \mathbf{b}$ 急剧简化为 $I_n \mathbf{x} = A^\top \mathbf{b}$，直接给出唯一解：
$$ \mathbf{x}_{\star} = A^\top \mathbf{b} $$
这表明，当[基向量](@entry_id:199546)（$A$的列）是标准正交时，寻找最佳线性组合的系数（$x$ 的分量）只需将目标向量 $\mathbf{b}$ 分别投影到每个[基向量](@entry_id:199546)上即可 [@problem_id:3592614]。

### 推广与辨析

#### 残差与误差
在实际应用中，我们常常假设数据由一个真实模型生成：$\mathbf{b} = A \mathbf{x}_{\text{true}} + \mathbf{e}$，其中 $\mathbf{x}_{\text{true}}$ 是未知的真实参数，$\mathbf{e}$ 是测量噪声。必须严格区分两个概念 [@problem_id:3592605]：
- **残差 (Residual)**: $\mathbf{r} = \mathbf{b} - A\mathbf{x}$。这是一个可观测的量，因为它只依赖于给定的数据 $(A, \mathbf{b})$ 和我们选择的解 $\mathbf{x}$。[最小二乘法](@entry_id:137100)直接最小化的是残差的范数。
- **解的误差 (Solution Error)**: $\mathbf{x} - \mathbf{x}_{\text{true}}$。这是一个不可观测的量，因为我们不知道 $\mathbf{x}_{\text{true}}$。

最小二乘法之所以最小化[残差范数](@entry_id:754273)，是因为这是在仅有 $(A, \mathbf{b})$ 的情况下唯一可行的、衡量[数据拟合](@entry_id:149007)优劣的策略。它旨在找到模型[子空间](@entry_id:150286) $\operatorname{range}(A)$ 中与观测数据 $\mathbf{b}$ 最“接近”的点。解的误差与残差之间存在联系，但并不等同。将 $\mathbf{b} = A\mathbf{x}_{\text{true}} + \mathbf{e}$ 代入[最小二乘解](@entry_id:152054) $\mathbf{x}_{\star} = (A^\top A)^{-1}A^\top \mathbf{b}$，可得：
$$ \mathbf{x}_{\star} - \mathbf{x}_{\text{true}} = (A^\top A)^{-1}A^\top \mathbf{e} $$
这表明，解的误差取决于噪声 $\mathbf{e}$ 是如何通过算子 $(A^\top A)^{-1}A^\top$ 传播的。最小化残差并不等同于最小化解的误差。

#### 通过[内积](@entry_id:158127)进行推广
正规方程的推导依赖于标准的欧几里得[内积](@entry_id:158127)。如果我们在 $\mathbb{R}^m$ 中定义一个不同的[内积](@entry_id:158127)，正交性的概念就会改变，从而改变[正规方程](@entry_id:142238)的形式。一个常见的推广是**加权最小二乘**，其中我们最小化一个加权范数 $\|A\mathbf{x} - \mathbf{b}\|_W^2 = (A\mathbf{x} - \mathbf{b})^\top W (A\mathbf{x} - \mathbf{b})$，其中 $W$ 是一个对称正定 (SPD) 矩阵。

这个加权范数是由 $W$ 定义的[内积](@entry_id:158127) $\langle \mathbf{u}, \mathbf{v} \rangle_W = \mathbf{u}^\top W \mathbf{v}$ 导出的。在此[内积](@entry_id:158127)下，残差 $r = b-Ax$ 与 $\operatorname{range}(A)$ 正交的条件变为 $\langle Ay, r \rangle_W = 0$ 对所有 $y \in \mathbb{R}^n$ 成立。这可以写为：
$$ (Ay)^\top W r = 0 \implies y^\top (A^\top W r) = 0 $$
由于此式对所有 $y$ 成立，我们得到 $A^\top W r = 0$。代入 $r=b-Ax$，我们得到**加权[正规方程](@entry_id:142238)** [@problem_id:3592613] [@problem_id:3592602]：
$$ (A^\top W A) \mathbf{x} = A^\top W \mathbf{b} $$
更一般地，我们可以在 $\mathbb{R}^n$ 和 $\mathbb{R}^m$ 上都定义广义[内积](@entry_id:158127)，分别由 SPD 矩阵 $H$ 和 $W$ 给出。此时，算子 $A$ 的**[伴随算子](@entry_id:140236)** $A^\ast$ 由关系 $\langle A\mathbf{x}, \mathbf{y} \rangle_W = \langle \mathbf{x}, A^\ast\mathbf{y} \rangle_H$ 定义。可以证明 $A^\ast = H^{-1}A^\top W$。广义上的正规方程总是 $A^\ast A \mathbf{x} = A^\ast \mathbf{b}$ [@problem_id:3592602]。

#### 扩展到[复数域](@entry_id:153768)
当处理复数矩阵 $A \in \mathbb{C}^{m \times n}$ 和向量 $\mathbf{b} \in \mathbb{C}^m$ 时，必须使用正确的[复内积](@entry_id:261242)定义。[复向量空间](@entry_id:264355) $\mathbb{C}^m$ 上的标准[内积](@entry_id:158127)是 $\langle \mathbf{u}, \mathbf{v} \rangle = \mathbf{v}^* \mathbf{u}$，其中 $\mathbf{v}^*$ 是 $\mathbf{v}$ 的**共轭转置**（Hermitian transpose）。范数的平方为 $\|\mathbf{u}\|_2^2 = \mathbf{u}^* \mathbf{u}$。

遵循与实数情况相同的几何原理，[最小二乘解](@entry_id:152054) $\mathbf{x}_{\star}$ 必须满足残差 $\mathbf{r}_{\star} = \mathbf{b} - A\mathbf{x}_{\star}$ 与 $\operatorname{range}(A)$ 正交。这意味着对于 $A$ 的任意一列 $\mathbf{a}_j$，我们有 $\langle \mathbf{r}_{\star}, \mathbf{a}_j \rangle = 0$，即 $\mathbf{a}_j^* \mathbf{r}_{\star} = 0$。将所有列的条件整合起来，得到 $A^* \mathbf{r}_{\star} = \mathbf{0}$。代入残差的表达式，便得到复数域中的[正规方程](@entry_id:142238) [@problem_id:3592646]：
$$ (A^* A) \mathbf{x}_{\star} = A^* \mathbf{b} $$
一个常见的错误是错误地使用普通[转置](@entry_id:142115) $A^\top$ 代替共轭转置 $A^*$。得到的方程 $(A^\top A)\mathbf{x} = A^\top \mathbf{b}$ 通常会给出一个完全错误的、无意义的解。这是因为它对应于一个不满足[内积](@entry_id:158127)正定性的双线性型下的“伪正交”条件。

幸运的是，这种错误可以通过一个简单的检查来发现。正确的系数矩阵 $M_\star = A^*A$ 必然是**[埃尔米特矩阵](@entry_id:155147)**（Hermitian matrix），即 $M_\star^* = M_\star$。而错误的矩阵 $M_{\text{bad}} = A^\top A$ 通常不是埃尔米特矩阵。因此，通过数值检验 $M - M^*$ 是否接近于零矩阵，可以有效地判断是否正确使用了[共轭转置](@entry_id:147909) [@problem_id:3592646]。

### 数值稳定性与[条件数](@entry_id:145150)

虽然正规方程在理论上优雅简洁，但在有限精度的浮点运算中，直接构造并求解它可能存在严重的[数值稳定性](@entry_id:146550)问题。这是[数值线性代数](@entry_id:144418)领域的一个核心教训。

#### 条件数的平方
问题的根源在于从矩阵 $A$ 到 $A^\top A$ 的变换过程。一个矩阵的**[条件数](@entry_id:145150)** $\kappa(A)$ 衡量了其解对输入数据微小扰动的敏感度。对于[最小二乘问题](@entry_id:164198)，相关的条件数是 $\kappa_2(A) = \sigma_{\max}(A)/\sigma_{\min}(A)$，其中 $\sigma_{\max}$ 和 $\sigma_{\min}$ 分别是 $A$ 的最大和最小奇异值。

系数矩阵 $A^\top A$ 的条件数与 $A$ 的条件数之间有一个关键关系。由于 $A^\top A$ 的[特征值](@entry_id:154894)是 $A$ 的奇异值的平方，其[条件数](@entry_id:145150)为：
$$ \kappa_2(A^\top A) = \frac{\sigma_{\max}(A)^2}{\sigma_{\min}(A)^2} = (\kappa_2(A))^2 $$
这意味着，通过构建 $A^\top A$，我们将问题的[条件数](@entry_id:145150)**平方**了 [@problem_id:3567270] [@problem_id:3592619]。如果 $A$ 本身是良态的（$\kappa_2(A)$ 较小），这不成问题。但如果 $A$ 是病态的（$\kappa_2(A)$ 很大，例如 $10^7$），那么 $A^\top A$ 的条件数将变得极大（例如 $10^{14}$），使得求解[正规方程](@entry_id:142238)的过程对舍入误差极为敏感。

#### 信息丢失与稳定性分析
这种[条件数](@entry_id:145150)的平方不仅仅是一个理论上的坏兆头，它反映了在计算 $A^\top A$ 过程中可能发生的**信息丢失**。假设[浮点运算](@entry_id:749454)的[单位舍入误差](@entry_id:756332)为 $u$（对于[双精度](@entry_id:636927)，约为 $10^{-16}$）。如果 $A$ 的一个很小的奇异值 $\sigma_n$ 满足 $\sigma_n \lesssim \sqrt{u} \sigma_1$，那么 $\sigma_n^2 \lesssim u \sigma_1^2$。这意味着 $\sigma_n^2$ 的量级可能与计算 $A^\top A$ 时产生的[舍入误差](@entry_id:162651)相当。其后果是，计算出的矩阵 $\text{fl}(A^\top A)$ 可能在数值上是奇异的，即使理论上的 $A^\top A$ 是可逆的。这有效地抹去了关于 $A$ 的最[精细结构](@entry_id:140861)的信息 [@problem_id:3592619]。

更正式地，我们可以从**向后稳定性**（backward stability）的角度分析。一个数值稳定的最小二乘求解器，其计算出的解 $\hat{\mathbf{x}}$ 应该是某个略微扰动问题 $(A+\Delta A, \mathbf{b})$ 的精确解，其中 $\|\Delta A\|_2 \le c u \|A\|_2$。基于 QR 分解等[正交变换](@entry_id:155650)的方法是向后稳定的。然而，通过显式构造 $A^\top A$ 再求解的[正规方程](@entry_id:142238)法**不是**向后稳定的 [@problem_id:3567270] [@problem_id:3592634]。

这种稳定性上的差异直接影响了最终解的精度。对于 QR 方法，解的相对误差通常与 $u \kappa_2(A)$ 成正比。而对于正规方程法，误差与 $u \kappa_2(A)^2$ 成正比。这意味着，对于一个病态问题，正规方程法损失的有效数字位数大约是 QR 方法的两倍。例如，如果 $\kappa_2(A) \approx 10^8$，在双精度下（$u \approx 10^{-16}$），QR 方法可能仍能得到约 $16-8=8$ 位[有效数字](@entry_id:144089)，而[正规方程](@entry_id:142238)法的误差因子 $\approx 10^{-16} \cdot (10^8)^2 = 1$，可能导致解中没有任何一位是正确的 [@problem_id:3592634]。

#### 实践考量与替代方法
尽管存在数值缺陷，正规方程法由于其简洁性和潜在的计算效率（尤其当 $m \gg n$ 时，其计算量约为 $mn^2$ flops，而 Householder QR 分解约为 $2mn^2$ flops）在某些场合仍有应用 [@problem_id:3592634]。然而，在面对病态问题或需要高精度解的场景时，应优先选用更稳定的方法，例如：
1.  **QR 分解**：通过将 $A$分解为[正交矩阵](@entry_id:169220) $Q$和上三角矩阵 $R$的乘积，将最小二乘问题转化为求解一个良态的三角系统。这是求解中小型稠密[最小二乘问题](@entry_id:164198)的标准方法。
2.  **SVD 分解**：[奇异值分解](@entry_id:138057)提供了最可靠、最全面的诊断信息，但计算成本也最高。
3.  **迭代方法**：对于大规模稀疏问题，直接法变得不可行。此时，可以应用诸如**[共轭梯度法](@entry_id:143436) (Conjugate Gradient, CG)** 到正规方程系统上。关键在于，CG 算法只需要计算矩阵-向量乘积，即 $A^\top A$ 与某个向量的乘积。这可以分两步完成：先计算 $A\mathbf{v}$，再计算 $A^\top(A\mathbf{v})$，从而**避免显式地构造** $A^\top A$。这种方法（称为 CGNR 或 CGLS）保留了[正规方程](@entry_id:142238)的结构，但回避了其最致命的数值缺陷。LSQR 算法是另一个基于 Golub-Kahan [双对角化](@entry_id:746789)的迭代方法，它在精确算术下等价于 CGNR，但在数值上通常表现更佳 [@problem_id:3592619]。

总之，正规方程为我们理解[最小二乘问题](@entry_id:164198)提供了不可或缺的理论基石。然而，作为一种数值计算策略，它的应用必须审慎，时刻警惕其固有的数值不稳定性。在现代数值计算中，它更多地是作为理论分析的工具或启发更高级算法（如[迭代法](@entry_id:194857)）的起点，而非[高精度计算](@entry_id:200567)的首选。