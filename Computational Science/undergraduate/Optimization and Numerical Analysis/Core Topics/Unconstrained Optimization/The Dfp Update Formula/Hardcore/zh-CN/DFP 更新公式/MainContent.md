## 引言
在解决[非线性优化](@entry_id:143978)问题时，[牛顿法](@entry_id:140116)因其二次收敛速度而备受青睐，但其对Hessian矩阵的计算和求逆要求使得它在许多大规模实际应用中不切实际。为了克服这一障碍，[拟牛顿法](@entry_id:138962)应运而生，它通过迭代近似Hessian矩阵或其[逆矩阵](@entry_id:140380)，在效率和速度之间取得了出色的平衡。其中，Davidon-Fletcher-Powell（DFP）更新公式是历史上第一个，也是最具影响力的拟牛顿法之一，为整个领域的发展奠定了基础。

本文旨在全面解析DFP公式。我们首先将在“原理与机制”章节中深入探讨其核心数学思想，从作为拟牛顿法基石的[割线方程](@entry_id:164522)出发，详细推导[DFP更新公式](@entry_id:170404)，并分析其保持对称性和[正定性](@entry_id:149643)的关键条件。接着，在“应用与跨学科联系”部分，我们将考察DFP在实际优化任务中的表现，将其与更现代的[BFGS方法](@entry_id:263685)进行比较，并探讨其思想如何扩展以解决大规模及带约束的复杂问题。最后，通过一系列精心设计的“动手实践”，读者将有机会亲手实现和检验DFP算法的关键步骤，从而将理论知识转化为实践能力。

## 原理与机制

在[非线性优化](@entry_id:143978)领域，[牛顿法](@entry_id:140116)通过使用[目标函数](@entry_id:267263)的[二阶导数](@entry_id:144508)（Hessian 矩阵）来指导搜索方向，从而实现了快速收敛。然而，计算和求逆 Hessian 矩阵的成本在许多实际问题中高得令人望而却步。[拟牛顿法](@entry_id:138962)（Quasi-Newton methods）应运而生，其核心思想是绕过显式计算 Hessian 矩阵及其[逆矩阵](@entry_id:140380)，转而通过迭代的方式构建一个近似。本章将深入探讨拟牛顿法家族中一个开创性的成员——Davidon-Fletcher-Powell (DFP) 公式的核心原理与工作机制。

### 拟牛顿更新的理论基础：[割线方程](@entry_id:164522)

拟牛顿法的目标是构建一个矩阵 $H_k$，使其能够有效地近似[目标函数](@entry_id:267263) $f(\mathbf{x})$ 在点 $\mathbf{x}_k$ 处真实 Hessian [矩阵的逆](@entry_id:140380)矩阵，即 $H_k \approx [\nabla^2 f(\mathbf{x}_k)]^{-1}$。这个近似矩阵将用于确定搜索方向 $\mathbf{p}_k = -H_k \nabla f(\mathbf{x}_k)$。

为了构建这个近似，我们需要利用从上一步迭代中获得的信息。假设我们从点 $\mathbf{x}_k$ 移动到点 $\mathbf{x}_{k+1}$。我们可以将梯度函数 $\nabla f(\mathbf{x})$ 在 $\mathbf{x}_{k+1}$ 附近进行一阶[泰勒展开](@entry_id:145057)：
$$ \nabla f(\mathbf{x}) \approx \nabla f(\mathbf{x}_{k+1}) + \nabla^2 f(\mathbf{x}_{k+1}) (\mathbf{x} - \mathbf{x}_{k+1}) $$
令 $\mathbf{x} = \mathbf{x}_k$，并进行移项，我们得到：
$$ \nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k) \approx \nabla^2 f(\mathbf{x}_{k+1}) (\mathbf{x}_{k+1} - \mathbf{x}_k) $$
为了简化符号，我们定义两个关键向量：
- **位移向量 (step vector)**: $\mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k$
- **梯度差向量 (gradient difference vector)**: $\mathbf{y}_k = \nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k)$

于是，上述近似关系可以写为：
$$ \mathbf{y}_k \approx B_{k+1} \mathbf{s}_k $$
其中 $B_{k+1} = \nabla^2 f(\mathbf{x}_{k+1})$ 是在**新点** $\mathbf{x}_{k+1}$ 处的真实 Hessian 矩阵。拟牛顿法的核心思想是将这个近似关系强化为一个必须满足的**等式**，施加于我们正在构建的 Hessian 近似矩阵 $B_{k+1}$ 上。这个条件被称为**[割线方程](@entry_id:164522) (secant equation)**：
$$ B_{k+1} \mathbf{s}_k = \mathbf{y}_k $$
这个方程的几何意义是，新的 Hessian 近似矩阵 $B_{k+1}$ 在方向 $\mathbf{s}_k$ 上的作用效果，应该与真实 Hessian 矩阵在该方向上的平均作用效果相匹配。

由于 DFP 方法直接更新 Hessian [矩阵的逆](@entry_id:140380) $H_k$，我们需要将[割线方程](@entry_id:164522)转换为对 $H_{k+1}$ 的约束。假设 $H_{k+1} = B_{k+1}^{-1}$，用 $H_{k+1}$ 左乘[割线方程](@entry_id:164522)的两边，我们得到：
$$ H_{k+1} (B_{k+1} \mathbf{s}_k) = H_{k+1} \mathbf{y}_k $$
$$ (H_{k+1} B_{k+1}) \mathbf{s}_k = H_{k+1} \mathbf{y}_k $$
$$ I \mathbf{s}_k = H_{k+1} \mathbf{y}_k $$
最终，我们得到了 DFP 更新所必须满足的核心条件，即**逆[割线方程](@entry_id:164522) (inverse secant equation)** ：
$$ H_{k+1} \mathbf{y}_k = \mathbf{s}_k $$
任何旨在更新逆 Hessian 矩阵的拟牛顿公式，都必须以满足这个方程为首要目标。

### Davidon-Fletcher-Powell (DFP) 更新公式

DFP 公式是满足逆[割线方程](@entry_id:164522)的众多更新方案中最早也是最著名的之一。它通过对当前的逆 Hessian 近似 $H_k$ 进行一次**秩二校正 (rank-two update)** 来生成新的近似 $H_{k+1}$。DFP 更新公式如下：
$$ H_{k+1} = H_k + \frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k} - \frac{H_k \mathbf{y}_k \mathbf{y}_k^T H_k}{\mathbf{y}_k^T H_k \mathbf{y}_k} $$
其中，$\mathbf{u} \mathbf{v}^T$ 表示向量 $\mathbf{u}$ 和 $\mathbf{v}$ 的[外积](@entry_id:147029)，结果是一个矩阵。公式中的第一项是当前的近似 $H_k$。第二项 $\frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k}$ 是一个[秩一矩阵](@entry_id:199014)，其目的是确保最终结果满足逆[割线方程](@entry_id:164522)。第三项 $\frac{H_k \mathbf{y}_k \mathbf{y}_k^T H_k}{\mathbf{y}_k^T H_k \mathbf{y}_k}$ 也是一个[秩一矩阵](@entry_id:199014)，它对更新进行调整，以保持其他期望的性质。

我们可以直接验证 DFP 公式确实满足逆[割线方程](@entry_id:164522)。将公式右侧乘以 $\mathbf{y}_k$ ：
$$ H_{k+1} \mathbf{y}_k = H_k \mathbf{y}_k + \frac{\mathbf{s}_k (\mathbf{s}_k^T \mathbf{y}_k)}{\mathbf{s}_k^T \mathbf{y}_k} - \frac{H_k \mathbf{y}_k (\mathbf{y}_k^T H_k \mathbf{y}_k)}{\mathbf{y}_k^T H_k \mathbf{y}_k} $$
注意到 $\mathbf{s}_k^T \mathbf{y}_k$ 和 $\mathbf{y}_k^T H_k \mathbf{y}_k$ 都是标量。假设它们非零，我们可以进行化简：
$$ H_{k+1} \mathbf{y}_k = H_k \mathbf{y}_k + \mathbf{s}_k - H_k \mathbf{y}_k $$
$$ H_{k+1} \mathbf{y}_k = \mathbf{s}_k $$
这个简单的代数推导证明了 DFP 公式在设计上是自洽的，它精确地实现了逆[割线方程](@entry_id:164522)所要求的目标。

### DFP 更新的基本性质

一个好的 Hessian 逆近似矩阵 $H_k$ 应该具备真实 Hessian [逆矩阵](@entry_id:140380)的一些关键性质。对于一个在极小值点附近的良好表现的函数，其 Hessian 矩阵是对称且正定的。因此，我们希望 $H_k$ 也能保持这些性质。

#### 对称性
如果初始近似 $H_0$ 是对称的（通常选择为单位矩阵 $I$），那么 DFP 公式在每次迭代中都会保持矩阵的对称性。我们可以通过对 $H_{k+1}$ 求[转置](@entry_id:142115)来验证这一点 ：
$$ H_{k+1}^T = \left( H_k + \frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k} - \frac{H_k \mathbf{y}_k \mathbf{y}_k^T H_k}{\mathbf{y}_k^T H_k \mathbf{y}_k} \right)^T $$
利用 $(A+B)^T = A^T+B^T$ 和 $(AB)^T=B^T A^T$，我们得到：
$$ H_{k+1}^T = H_k^T + \frac{(\mathbf{s}_k \mathbf{s}_k^T)^T}{\mathbf{s}_k^T \mathbf{y}_k} - \frac{(H_k \mathbf{y}_k \mathbf{y}_k^T H_k)^T}{\mathbf{y}_k^T H_k \mathbf{y}_k} $$
由于 $(\mathbf{s}_k \mathbf{s}_k^T)^T = \mathbf{s}_k \mathbf{s}_k^T$，并且假设 $H_k$ 是对称的（$H_k^T = H_k$），则 $(H_k \mathbf{y}_k \mathbf{y}_k^T H_k)^T = H_k^T (\mathbf{y}_k^T)^T \mathbf{y}_k^T H_k^T = H_k \mathbf{y}_k \mathbf{y}_k^T H_k$。因此，
$$ H_{k+1}^T = H_k + \frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k} - \frac{H_k \mathbf{y}_k \mathbf{y}_k^T H_k}{\mathbf{y}_k^T H_k \mathbf{y}_k} = H_{k+1} $$
通过[数学归纳法](@entry_id:138544)，只要 $H_0$ 对称，所有的 $H_k$ 都将保持对称。

#### 正定性
保持[正定性](@entry_id:149643)是[拟牛顿法](@entry_id:138962)稳定性的关键。如果 $H_k$ 是正定的，那么搜索方向 $\mathbf{p}_k = -H_k \nabla f_k$ 就是一个**下降方向**，因为它保证了 $\nabla f_k^T \mathbf{p}_k = -\nabla f_k^T H_k \nabla f_k  0$（只要 $\nabla f_k \neq \mathbf{0}$）。这确保了沿该方向进行足够小的移动总能降低函数值 。

DFP 更新能否保持[正定性](@entry_id:149643)，取决于一个至关重要的条件。可以证明，如果 $H_k$ 是对称正定的，那么 $H_{k+1}$ 也是[对称正定](@entry_id:145886)的**当且仅当**满足以下条件 ：
$$ \mathbf{s}_k^T \mathbf{y}_k > 0 $$
这个不等式被称为**曲率条件 (curvature condition)**。它的直观解释是，沿着位移方向 $\mathbf{s}_k$，梯度的变化 $\mathbf{y}_k$ 必须与位移本身形成一个锐角。这在某种程度上反映了函数在该方向上具有正曲率（即向上弯曲），这是迈向一个极小值点的典型特征。

如果曲率条件不被满足，例如 $\mathbf{s}_k^T \mathbf{y}_k \le 0$，DFP 更新就可能（并且通常会）破坏 $H_k$ 的正定性。考虑一个由于线搜索程序错误而导致曲率条件被违反的场景 。设 $H_k = I$（[单位矩阵](@entry_id:156724)，是正定的），$\mathbf{s}_k = \begin{pmatrix} 2 \\ 0 \end{pmatrix}$，$\mathbf{y}_k = \begin{pmatrix} -1 \\ 1 \end{pmatrix}$。
首先，我们检查曲率条件：$\mathbf{s}_k^T \mathbf{y}_k = (2)(-1) + (0)(1) = -2  0$。
然后，我们计算 DFP 更新中的各个项：
$$ \frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k} = \frac{1}{-2} \begin{pmatrix} 4  0 \\ 0  0 \end{pmatrix} = \begin{pmatrix} -2  0 \\ 0  0 \end{pmatrix} $$
$$ \frac{H_k \mathbf{y}_k \mathbf{y}_k^T H_k}{\mathbf{y}_k^T H_k \mathbf{y}_k} = \frac{\mathbf{y}_k \mathbf{y}_k^T}{\mathbf{y}_k^T \mathbf{y}_k} = \frac{1}{(-1)^2 + 1^2} \begin{pmatrix} 1  -1 \\ -1  1 \end{pmatrix} = \begin{pmatrix} 0.5  -0.5 \\ -0.5  0.5 \end{pmatrix} $$
将它们代入 DFP 公式：
$$ H_{k+1} = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + \begin{pmatrix} -2  0 \\ 0  0 \end{pmatrix} - \begin{pmatrix} 0.5  -0.5 \\ -0.5  0.5 \end{pmatrix} = \begin{pmatrix} -1.5  0.5 \\ 0.5  0.5 \end{pmatrix} $$
这个新的近似矩阵 $H_{k+1}$ 的[特征值](@entry_id:154894)为 $\lambda \approx -1.618$ 和 $\lambda \approx 0.618$。由于出现了一个负[特征值](@entry_id:154894)，矩阵 $H_{k+1}$ 不再是正定的。在下一次迭代中，算法可能会选择一个导致函数值增加的方向，从而导致优化失败。这凸显了满足曲率条件的绝对重要性。

### 在实践中确保曲率条件：[线搜索](@entry_id:141607)

既然曲率条件 $\mathbf{s}_k^T \mathbf{y}_k > 0$如此关键，我们如何在算法中确保它得到满足呢？答案在于**线搜索 (line search)** 过程，即确定步长 $\alpha_k$ 的过程。一个设计良好的[线搜索算法](@entry_id:139123)不仅要确保函数值有足够的下降，还要能保证曲率条件成立。

**[强沃尔夫条件](@entry_id:173436) (strong Wolfe conditions)** 是一种常用的线搜索标准，它能为 DFP 和其他拟牛顿方法的稳定性提供理论保障。对于一个给定的[下降方向](@entry_id:637058) $\mathbf{p}_k$，步长 $\alpha_k$ 必须满足以下两个不等式，其中 $0  c_1  c_2  1$ 是预设的常数：
1.  **充分下降条件 (Sufficient Decrease Condition)**:
    $f(\mathbf{x}_k + \alpha_k \mathbf{p}_k) \le f(\mathbf{x}_k) + c_1 \alpha_k \nabla f_k^T \mathbf{p}_k$
2.  **曲率条件 (Curvature Condition)**:
    $|\nabla f(\mathbf{x}_k + \alpha_k \mathbf{p}_k)^T \mathbf{p}_k| \le c_2 |\nabla f_k^T \mathbf{p}_k|$

第一个条件确保了步长 $\alpha_k$ 能够带来函数值的显著减小。第二个条件（强沃尔夫形式）直接约束了新点 $\mathbf{x}_{k+1}$ 处的梯度在方向 $\mathbf{p}_k$ 上的投影。

我们可以证明，满足[强沃尔夫条件](@entry_id:173436)的步长必然满足 DFP 所需的曲率条件 $\mathbf{s}_k^T \mathbf{y}_k > 0$ 。展开 $\mathbf{s}_k^T \mathbf{y}_k$：
$$ \mathbf{s}_k^T \mathbf{y}_k = (\alpha_k \mathbf{p}_k)^T (\nabla f_{k+1} - \nabla f_k) = \alpha_k (\nabla f_{k+1}^T \mathbf{p}_k - \nabla f_k^T \mathbf{p}_k) $$
根据[强沃尔夫条件](@entry_id:173436)的第二条，我们有 $\nabla f_{k+1}^T \mathbf{p}_k \ge -c_2 |\nabla f_k^T \mathbf{p}_k|$。因为 $\mathbf{p}_k$ 是下降方向，$\nabla f_k^T \mathbf{p}_k  0$，所以 $|\nabla f_k^T \mathbf{p}_k| = -\nabla f_k^T \mathbf{p}_k$。代入得：
$$ \nabla f_{k+1}^T \mathbf{p}_k \ge -c_2 (-\nabla f_k^T \mathbf{p}_k) = c_2 \nabla f_k^T \mathbf{p}_k $$
将这个不等式代回 $\mathbf{s}_k^T \mathbf{y}_k$ 的表达式：
$$ \mathbf{s}_k^T \mathbf{y}_k \ge \alpha_k (c_2 \nabla f_k^T \mathbf{p}_k - \nabla f_k^T \mathbf{p}_k) = \alpha_k (c_2 - 1) \nabla f_k^T \mathbf{p}_k $$
因为 $c_2  1$ 且 $\nabla f_k^T \mathbf{p}_k  0$，所以 $(c_2 - 1)  0$ 且 $\alpha_k > 0$，这意味着整个表达式的右侧是正的：
$$ \mathbf{s}_k^T \mathbf{y}_k \ge (1-c_2) (-\alpha_k \nabla f_k^T \mathbf{p}_k) > 0 $$
因此，通过实施满足[强沃尔夫条件](@entry_id:173436)的[线搜索](@entry_id:141607)，我们可以从程序上保证 DFP 更新的[正定性](@entry_id:149643)得以维持。

### DFP 算法的一次完整迭代

让我们通过一个具体的例子来整合以上所有概念 。考虑最小化二次函数 $f(x_1, x_2) = x_1^2 + 2x_2^2$。我们从初始点 $\mathbf{x}_0 = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$ 和初始逆 Hessian 近似 $H_0 = I = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}$ 开始。

1.  **计算梯度和搜索方向**:
    $\nabla f(\mathbf{x}) = \begin{pmatrix} 2x_1 \\ 4x_2 \end{pmatrix}$。在 $\mathbf{x}_0$，梯度为 $\nabla f(\mathbf{x}_0) = \begin{pmatrix} 4 \\ 4 \end{pmatrix}$。
    搜索方向为 $\mathbf{p}_0 = -H_0 \nabla f(\mathbf{x}_0) = -I \begin{pmatrix} 4 \\ 4 \end{pmatrix} = \begin{pmatrix} -4 \\ -4 \end{pmatrix}$。

2.  **执行[精确线搜索](@entry_id:170557)**:
    我们需要找到 $\alpha_0 > 0$ 来最小化 $\phi(\alpha) = f(\mathbf{x}_0 + \alpha \mathbf{p}_0) = f(2-4\alpha, 1-4\alpha)$。
    $\phi(\alpha) = (2-4\alpha)^2 + 2(1-4\alpha)^2 = 6 - 32\alpha + 48\alpha^2$。
    令 $\phi'(\alpha) = -32 + 96\alpha = 0$，解得 $\alpha_0 = \frac{1}{3}$。

3.  **更新位置**:
    $\mathbf{x}_1 = \mathbf{x}_0 + \alpha_0 \mathbf{p}_0 = \begin{pmatrix} 2 \\ 1 \end{pmatrix} + \frac{1}{3} \begin{pmatrix} -4 \\ -4 \end{pmatrix} = \begin{pmatrix} 2/3 \\ -1/3 \end{pmatrix}$。

4.  **计算 $\mathbf{s}_0$ 和 $\mathbf{y}_0$**:
    $\mathbf{s}_0 = \mathbf{x}_1 - \mathbf{x}_0 = \begin{pmatrix} -4/3 \\ -4/3 \end{pmatrix}$。
    新点的梯度为 $\nabla f(\mathbf{x}_1) = \begin{pmatrix} 4/3 \\ -4/3 \end{pmatrix}$。
    $\mathbf{y}_0 = \nabla f(\mathbf{x}_1) - \nabla f(\mathbf{x}_0) = \begin{pmatrix} 4/3 \\ -4/3 \end{pmatrix} - \begin{pmatrix} 4 \\ 4 \end{pmatrix} = \begin{pmatrix} -8/3 \\ -16/3 \end{pmatrix}$。

5.  **应用 DFP 公式更新 $H_0$**:
    首先计算所需的标量和矩阵项：
    - $\mathbf{s}_0^T \mathbf{y}_0 = (-\frac{4}{3})(-\frac{8}{3}) + (-\frac{4}{3})(-\frac{16}{3}) = \frac{32}{9} + \frac{64}{9} = \frac{96}{9} = \frac{32}{3}$。 (曲率条件满足)
    - $\mathbf{y}_0^T H_0 \mathbf{y}_0 = \mathbf{y}_0^T \mathbf{y}_0 = (-\frac{8}{3})^2 + (-\frac{16}{3})^2 = \frac{64+256}{9} = \frac{320}{9}$。
    - $\frac{\mathbf{s}_0 \mathbf{s}_0^T}{\mathbf{s}_0^T \mathbf{y}_0} = \frac{1}{32/3} \begin{pmatrix} 16/9  16/9 \\ 16/9  16/9 \end{pmatrix} = \frac{1}{6} \begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix}$。
    - $\frac{H_0 \mathbf{y}_0 \mathbf{y}_0^T H_0}{\mathbf{y}_0^T H_0 \mathbf{y}_0} = \frac{1}{320/9} \begin{pmatrix} 64/9  128/9 \\ 128/9  256/9 \end{pmatrix} = \frac{1}{320} \begin{pmatrix} 64  128 \\ 128  256 \end{pmatrix} = \frac{1}{5} \begin{pmatrix} 1  2 \\ 2  4 \end{pmatrix}$。

    最后，组合这些项：
    $$ H_1 = H_0 + \frac{\mathbf{s}_0 \mathbf{s}_0^T}{\mathbf{s}_0^T \mathbf{y}_0} - \frac{H_0 \mathbf{y}_0 \mathbf{y}_0^T H_0}{\mathbf{y}_0^T H_0 \mathbf{y}_0} = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + \begin{pmatrix} 1/6  1/6 \\ 1/6  1/6 \end{pmatrix} - \begin{pmatrix} 1/5  2/5 \\ 2/5  4/5 \end{pmatrix} $$
    $$ H_1 = \begin{pmatrix} 1 + \frac{1}{6} - \frac{1}{5}  \frac{1}{6} - \frac{2}{5} \\ \frac{1}{6} - \frac{2}{5}  1 + \frac{1}{6} - \frac{4}{5} \end{pmatrix} = \begin{pmatrix} \frac{29}{30}  -\frac{7}{30} \\ -\frac{7}{30}  \frac{11}{30} \end{pmatrix} $$
    我们得到了新的逆 Hessian 近似 $H_1$。它是一个[对称矩阵](@entry_id:143130)，并且可以验证它是正定的，为下一次迭代做好了准备。我们可以计算它的迹，$\operatorname{tr}(H_1) = \frac{29}{30} + \frac{11}{30} = \frac{40}{30} = \frac{4}{3}$ 。

### 理论性能与对偶性

DFP 方法不仅在实践中有效，还具有强大的理论性质，尤其是在应用于特定类型的函数时。

#### 二次终止性
DFP 方法的一个显著理论成就是其**二次终止性 (quadratic termination)**。该性质指出，当 DFP 算法应用于一个 $n$ 维严格凸二次函数 $f(\mathbf{x}) = \frac{1}{2}\mathbf{x}^T Q \mathbf{x} - \mathbf{b}^T \mathbf{x}$（其中 $Q$ 是[对称正定矩阵](@entry_id:136714)），并使用**[精确线搜索](@entry_id:170557)**时，它具有以下特性 ：
1.  算法产生的搜索方向 $\{\mathbf{p}_0, \mathbf{p}_1, \dots, \mathbf{p}_{n-1}\}$ 是相互 **$Q$-共轭**的，即 $\mathbf{p}_i^T Q \mathbf{p}_j = 0$ 对所有 $i \neq j$ 成立。
2.  算法至多经过 $n$ 次迭代，其生成的逆 Hessian 近似矩阵 $H_n$ 会精确地等于真实的逆 Hessian 矩阵，即 $H_n = Q^{-1}$。
3.  因此，算法至多在 $n+1$ 步内就能找到该二次函数的唯一极小值点。

这个性质非常重要，因为它表明 DFP 方法能够在有限步内精确解决一类重要的[优化问题](@entry_id:266749)。由于任何一般光滑函数在其极小值点附近都可以由一个凸二次函数很好地近似，二次终止性解释了 DFP 方法在一般[非线性](@entry_id:637147)问题上表现出快速收敛（[超线性收敛](@entry_id:141654)）的原因。

#### DFP 与 BFGS 的对偶性
DFP 公式属于一个更广泛的拟牛顿更新家族，称为 Broyden 族。在这个家族中，另一个极为重要和流行的成员是 **Broyden–Fletcher–Goldfarb–Shanno (BFGS)** 公式。

DFP 和 BFGS 之间存在一种优美的**对偶关系 (duality)**。回想 DFP 更新的是逆 Hessian 近似 $H_k$。如果我们转而更新 Hessian 近似本身 $B_k = H_k^{-1}$，可以推导出相应的更新公式。有趣的是，BFGS 更新 $B_k$ 的公式，其结构与 DFP 更新 $H_k$ 的公式惊人地相似，只需将 $\mathbf{s}_k$ 和 $\mathbf{y}_k$ 的角色互换即可 。

- **DFP 更新 $H_k$**:
  $H_{k+1}^{\text{DFP}} = H_k + \frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k} - \frac{H_k \mathbf{y}_k \mathbf{y}_k^T H_k}{\mathbf{y}_k^T H_k \mathbf{y}_k}$

- **BFGS 更新 $B_k$ (DFP 的对偶形式)**:
  $B_{k+1}^{\text{BFGS}} = B_k + \frac{\mathbf{y}_k \mathbf{y}_k^T}{\mathbf{y}_k^T \mathbf{s}_k} - \frac{B_k \mathbf{s}_k \mathbf{s}_k^T B_k}{\mathbf{s}_k^T B_k \mathbf{s}_k}$

同样地，BFGS 更新 $H_k$ 的公式也可以通过在 DFP 更新 $B_k$ 的公式中交换 $\mathbf{s}_k$ 和 $\mathbf{y}_k$ 得到。这种对偶性不仅在理论上十分优雅，也为分析和理解整个拟牛顿方法家族提供了深刻的洞见。尽管 DFP 方法具有开创性意义，但在现代实践中，BFGS 方法由于其在[非精确线搜索](@entry_id:637270)下的数值稳定性和鲁棒性通常表现更佳，因此得到了更广泛的应用。