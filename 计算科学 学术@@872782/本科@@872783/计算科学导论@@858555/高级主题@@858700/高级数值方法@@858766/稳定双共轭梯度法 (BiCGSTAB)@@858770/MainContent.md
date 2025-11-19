## 引言
在科学与工程计算领域，求解大型线性方程组 $A\mathbf{x} = \mathbf{b}$ 是一项基础而关键的任务。虽然[共轭梯度](@entry_id:145712)（CG）法为[对称正定系统](@entry_id:172662)提供了高效的解决方案，但现实世界中的许多问题——从[流体动力学](@entry_id:136788)中的[输运现象](@entry_id:147655)到[经济网络](@entry_id:140520)中的非互易关系——本质上都是非对称的，这使得CG方法[无能](@entry_id:201612)为力。这一知识鸿沟催生了为非对称系统设计的迭代方法，其中，稳定[双共轭梯度法](@entry_id:746788)（BiCGSTAB）因其卓越的收敛稳定性与[计算效率](@entry_id:270255)而脱颖而出，成为应用最广泛的求解器之一。本文旨在为读者提供一个关于[BiCGSTAB方法](@entry_id:175494)的全面而深入的指南。

在接下来的内容中，我们将首先在“原理与机制”一章中，剖析[BiCGSTAB](@entry_id:143406)如何通过巧妙的[混合策略](@entry_id:145261)克服其前身BiCG算法的缺陷，并与GMRES等方法进行对比。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将探索该方法在[流体力学](@entry_id:136788)、[网络科学](@entry_id:139925)、经济建模等多个领域的实际应用案例，展示其解决现实问题的强大能力。最后，“动手实践”部分将提供精心设计的编程练习，帮助读者将理论知识转化为实践技能。让我们首先深入其核心，探究BiCGSTAB的原理与机制。

## 原理与机制

在求解大型[线性方程组](@entry_id:148943) $A\mathbf{x} = \mathbf{b}$ 的征途中，[共轭梯度法](@entry_id:143436) (Conjugate Gradient, CG) 因其卓越的效率和简洁性而备受推崇。然而，正如前文所述，CG 方法的理论保证严格依赖于一个前提：[系统矩阵](@entry_id:172230) $A$ 必须是**对称正定 (symmetric positive-definite, SPD)** 的。当面对在[流体力学](@entry_id:136788)、电磁学、[网络分析](@entry_id:139553)等众多科学与工程领域中普遍存在的[非对称线性系统](@entry_id:164317)时，CG 方法便[无能](@entry_id:201612)为力。为了应对这一挑战，研究者们开发了一系列适用于更一般矩阵的克雷洛夫子空间 (Krylov subspace) 方法。其中，稳定[双共轭梯度法](@entry_id:746788) (Biconjugate Gradient Stabilized method, BiCGSTAB) 以其高效、稳健和易于实现的特性，成为应用最广泛的算法之一。本章将深入剖析 [BiCGSTAB](@entry_id:143406) 的核心原理与内在机制。

### 从[共轭梯度法](@entry_id:143436)到非对称系统

要理解 [BiCGSTAB](@entry_id:143406)，我们必须首先认识到从对称到非对称世界的过渡所带来的根本困难。CG 方法的优雅之处在于，通过利用 $A$ 的对称性，可以在一个由 $A$ 定义的[内积](@entry_id:158127)（即 $A$-[内积](@entry_id:158127)）下，构造一组 $A$-正交（或称共轭）的搜索方向。这使得每一步迭代都能在已搜索过的方向上保持最优性，从而保证了在理想情况下的快速收敛。

当矩阵 $A$ 非对称时，$A$-[内积](@entry_id:158127)不再成立，CG 的整个理论框架随之瓦解。因此，为非对称系统设计的迭代方法必须另辟蹊径。BiCGSTAB 正是这一探索过程中的杰出成果，它巧妙地绕开了对称性的限制，为求解一般线性系统提供了强大的工具。与 CG 方法不同，[BiCGSTAB](@entry_id:143406) 不要求矩阵 $A$ 具有对称性或[正定性](@entry_id:149643)；只要 $A$ 是可逆的，它原则上就可以应用 [@problem_id:2208857]。

### 前驱算法：[双共轭梯度法](@entry_id:746788) (BiCG) 及其局限性

在 [BiCGSTAB](@entry_id:143406) 诞生之前，[双共轭梯度法](@entry_id:746788) (Biconjugate Gradient, BiCG) 是推广 CG 思想至[非对称矩阵](@entry_id:153254)的直接尝试。BiCG 的核心思想是，既然无法构造单一的正交基，那就同时构造两组“双正交”的序列。具体而言，它并行地为原始系统 $A\mathbf{x}=\mathbf{b}$ 和一个伴随的“影子”系统 $A^T\mathbf{y}=\mathbf{c}$ 生成[克雷洛夫子空间](@entry_id:751067)。通过强制这两个[子空间](@entry_id:150286)中的残差向量序列相互正交，BiCG 得以建立起类似于 CG 的短递归关系。

尽管 BiCG 在理论上是一个优美的推广，但在实际应用中却暴露了几个显著的弱点，这些弱点也正是 [BiCGSTAB](@entry_id:143406) 旨在解决的问题：

1.  **不规则的收敛行为**: BiCG 的[残差范数](@entry_id:754273) $\|\mathbf{r}_k\|$ 在迭代过程中常常表现出剧烈[振荡](@entry_id:267781)甚至增大的行为。这种不稳定的收敛曲线使得预测收敛所需步数变得困难，有时甚至导致收敛极其缓慢或失败。这种现象在当矩阵 $A$ 具有复数[特征值](@entry_id:154894)时尤为突出 [@problem_id:2208875]。

2.  **依赖矩阵的转置**: BiCG 的每一次迭代不仅需要计算一次矩阵-向量乘积 $A\mathbf{p}_k$，还需要计算一次转置矩阵-向量乘积 $A^T\mathbf{p}_k^*$。在许多实际应用中，矩阵 $A$ 可能是通过一个复杂的函数或程序隐式定义的，计算 $A^T\mathbf{v}$ 可能非常不便，甚至无法实现。[BiCGSTAB](@entry_id:143406) 的一个重要优势便是它完全避免了与 $A^T$ 的运算 [@problem_id:2208875]。

3.  **可能发生的算法崩溃**: BiCG 的迭代公式中包含形如 $\langle \mathbf{p}_k^*, A\mathbf{p}_k \rangle$ 的分母项。在某些情况下，即使所有向量都非零，这个[内积](@entry_id:158127)也可能为零（或接近于零），导致算法因除零错误而“严重崩溃” (serious breakdown)。例如，在特定[初始条件](@entry_id:152863)下，构造出使 $A$-[正交关系](@entry_id:145540) $\mathbf{p}_0^{*T} A \mathbf{p}_0 = 0$ 成立是可能的，这会导致 BiCG 在第一步就无法进行 [@problem_id:2427438]。

### BiCGSTAB 的核心思想：混合与稳定

为了克服 BiCG 的上述缺陷，荷兰数学家 Henk van der Vorst 于 1992 年提出了 BiCGSTAB 算法。其名称“Biconjugate Gradient Stabilized”已暗示了其核心思想：它并非一个全新的方法，而是对 BiCG 的一种“稳定化”改造。

BiCGSTAB 的精髓在于它是一种**[混合方法](@entry_id:163463) (hybrid method)**。它将 BiCG 的迭代步骤与一种局部最优化的思想相结合，从而在保持[计算效率](@entry_id:270255)的同时，极大地改善了收敛的平滑性和稳健性。具体来说，[BiCGSTAB](@entry_id:143406) 的每一次迭代都由两个关键阶段构成：

1.  **BiCG 阶段**: 算法首先像 BiCG 一样，沿着一个搜索方向 $\mathbf{p}_k$ 前进一定步长 $\alpha_k$。这一步旨在利用 BiCG 的多项式性质来有效地缩减残差。然而，它并不直接接受这一步的结果。

2.  **稳定化阶段**: 在 BiCG 步骤之后，算法会得到一个中间残差 $\mathbf{s}_k$。[BiCGSTAB](@entry_id:143406) 接着执行一个额外的“稳定化”步骤。这个步骤本质上是一个一维的最小残差方法 (a GMRES(1)-like step)，它计算一个稳定化参数 $\omega_k$，使得更新后的残差 $\mathbf{r}_{k+1}$ 的欧几里得范数 $\| \cdot \|_2$ 在局部达到最小。正是这个步骤有效地抑制了 BiCG 的[振荡](@entry_id:267781)行为，赋予了算法“稳定”的特性。

通过这种“先推进，后修正”的策略，[BiCGSTAB](@entry_id:143406) 巧妙地结合了 BiCG 算法的快速[传播能力](@entry_id:756124)和最小残差方法的稳定特性。

### BiCGSTAB 算法的单步迭代机制

让我们通过剖析单次迭代的计算流程来具体理解 BiCGSTAB 的工作机制。假设我们从解的初始猜测 $\mathbf{x}_0$ 开始，第 $k$ 次迭代的目标是从当前解 $\mathbf{x}_k$ 计算出更精确的解 $\mathbf{x}_{k+1}$。

算法维护着当前解 $\mathbf{x}_k$、残差 $\mathbf{r}_k = \mathbf{b} - A\mathbf{x}_k$ 和搜索方向 $\mathbf{p}_k$。此外，它还需要一个固定的“影子”残差 $\hat{\mathbf{r}}_0$，通常简单地取为初始残差 $\mathbf{r}_0$。

**第 $k$ 次迭代 ($k=0, 1, 2, \dots$)**

1.  **计算 BiCG 步长 $\alpha_k$**:
    首先，计算一个标量 $\rho_k = \hat{\mathbf{r}}_0^T \mathbf{r}_k$。然后，计算矩阵-[向量积](@entry_id:156672) $\mathbf{v}_k = A\mathbf{p}_k$。步长 $\alpha_k$ 由下式给出：
    $$ \alpha_k = \frac{\rho_k}{\hat{\mathbf{r}}_0^T \mathbf{v}_k} $$
    这个公式源于 BiCG 的[双正交性](@entry_id:746831)要求。

2.  **计算中间残差 $\mathbf{s}_k$**:
    使用步长 $\alpha_k$ 进行一次临时更新，得到中间残差 $\mathbf{s}_k$：
    $$ \mathbf{s}_k = \mathbf{r}_k - \alpha_k \mathbf{v}_k = \mathbf{r}_k - \alpha_k A\mathbf{p}_k $$
    如果 BiCGSTAB 在这里停止，它就退化为了一个 BiCG 步骤。$\mathbf{s}_k$ 可以被看作是 BiCG 步骤产生的“候选”残差。

3.  **计算稳定化步长 $\omega_k$**:
    这是稳定化的核心。我们的目标是寻找一个标量 $\omega$ 来最小化新残差的范数，即最小化 $\| \mathbf{s}_k - \omega A\mathbf{s}_k \|_2^2$。这是一个关于 $\omega$ 的二次函数的最小化问题 [@problem_id:3210163]。通过对 $\omega$ 求导并令其为零，可以得到最优的 $\omega_k$：
    $$ \omega_k = \frac{(A\mathbf{s}_k)^T \mathbf{s}_k}{(A\mathbf{s}_k)^T (A\mathbf{s}_k)} = \frac{\langle A\mathbf{s}_k, \mathbf{s}_k \rangle}{\| A\mathbf{s}_k \|_2^2} $$
    为了计算 $\omega_k$，我们需要进行第二次矩阵-向量乘积运算 $\mathbf{t}_k = A\mathbf{s}_k$。

4.  **更新解和残差**:
    使用计算出的两个步长 $\alpha_k$ 和 $\omega_k$，对解进行最终更新：
    $$ \mathbf{x}_{k+1} = \mathbf{x}_k + \alpha_k \mathbf{p}_k + \omega_k \mathbf{s}_k $$
    相应地，最终的残差为：
    $$ \mathbf{r}_{k+1} = \mathbf{s}_k - \omega_k \mathbf{t}_k = \mathbf{s}_k - \omega_k A\mathbf{s}_k $$

5.  **更新下一个搜索方向 $\mathbf{p}_{k+1}$**:
    最后，为下一次迭代准备新的搜索方向。这同样通过一个短递归完成：
    $$ \beta_k = \frac{\rho_{k+1}}{\rho_k} \frac{\alpha_k}{\omega_k} \quad (\text{其中 } \rho_{k+1} = \hat{\mathbf{r}}_0^T \mathbf{r}_{k+1}) $$
    $$ \mathbf{p}_{k+1} = \mathbf{r}_{k+1} + \beta_k (\mathbf{p}_k - \omega_k \mathbf{v}_k) $$

通过一个具体的数值示例 [@problem_id:2182348]，我们可以更清晰地看到这些步骤。考虑系统 $A\mathbf{x} = \mathbf{b}$，其中 $A = \begin{pmatrix} 3 & -1 \\ 1 & 2 \end{pmatrix}$，$\mathbf{b} = \begin{pmatrix} 1 \\ 4 \end{pmatrix}$，从 $\mathbf{x}_0 = \mathbf{0}$ 开始。
- **初始化**: $\mathbf{r}_0 = \mathbf{b} = \begin{pmatrix} 1 \\ 4 \end{pmatrix}$。设 $\hat{\mathbf{r}}_0 = \mathbf{r}_0$ 且 $\mathbf{p}_0 = \mathbf{r}_0$。
- **计算 $\alpha_0$**: $\mathbf{v}_0 = A\mathbf{p}_0 = \begin{pmatrix} -1 \\ 9 \end{pmatrix}$。$\rho_0 = \mathbf{r}_0^T \hat{\mathbf{r}}_0 = 17$。$\hat{\mathbf{r}}_0^T \mathbf{v}_0 = 35$。因此 $\alpha_0 = 17/35$。
- **计算 $\mathbf{s}_0$**: $\mathbf{s}_0 = \mathbf{r}_0 - \alpha_0 \mathbf{v}_0 = \frac{1}{35}\begin{pmatrix} 52 \\ -13 \end{pmatrix}$。
- **计算 $\omega_0$**: $\mathbf{t}_0 = A\mathbf{s}_0 = \frac{1}{35}\begin{pmatrix} 169 \\ 26 \end{pmatrix}$。根据公式，我们计算出 $\omega_0 = 50/173$。
- **更新 $\mathbf{x}_1$**: $\mathbf{x}_1 = \mathbf{x}_0 + \alpha_0 \mathbf{p}_0 + \omega_0 \mathbf{s}_0 \approx \begin{pmatrix} 0.9151 \\ 1.8355 \end{pmatrix}$。
这个简单的计算过程展示了算法每一步中向量和标量的精确流动。

### 收敛行为与稳健性分析

[BiCGSTAB](@entry_id:143406) 的设计初衷就是为了获得更平滑、更可靠的收敛。

**平滑收敛**

$\omega_k$ 稳定化步骤的效果立竿见影。对于那些导致 BiCG 剧烈[振荡](@entry_id:267781)的系统（特别是当 $A$ 的谱包含复共轭[特征值](@entry_id:154894)对时），[BiCGSTAB](@entry_id:143406) 的[残差范数](@entry_id:754273)通常会呈现出近乎单调的下降趋势 [@problem_id:2208875]。每一次迭代中的局部最小化步骤有效地“削平”了残差曲线上的“峰值”，从而避免了大幅度的[振荡](@entry_id:267781)。这种平滑的收敛行为不仅在数值上更受欢迎，也使得基于残差的[停止准则](@entry_id:136282)更加可靠。

**算法崩溃与停滞**

BiCGSTAB 成功地规避了 BiCG 中因 $\langle \mathbf{p}_k^*, A\mathbf{p}_k \rangle = 0$ 导致的“严重崩溃”，因为它完全不依赖于影[子序列](@entry_id:147702) $\mathbf{p}_k^*$。它在计算 $\alpha_k$ 时使用的分母是 $\hat{\mathbf{r}}_0^T A \mathbf{p}_k$。在标准选择 $\hat{\mathbf{r}}_0 = \mathbf{r}_0$ 且 $\mathbf{p}_0 = \mathbf{r}_0$ 的情况下，第一步的分母是 $\mathbf{r}_0^T A \mathbf{r}_0$，这在 BiCG 可能崩溃的场景中通常是非零的，从而使得算法可以顺利启动 [@problem_id:2427438]。

然而，[BiCGSTAB](@entry_id:143406) 并非绝对不会失败。它可能会遇到自己的问题，尽管发生的概率较低：
- **$\alpha_k$ 崩溃**: 如果 $\hat{\mathbf{r}}_0^T A \mathbf{p}_k = 0$，计算 $\alpha_k$ 时会除以零。
- **$\omega_k$ 崩溃或停滞**: 如果 $A\mathbf{s}_k=0$ 而 $\mathbf{s}_k \neq 0$，这意味着 $\mathbf{s}_k$ 是 $A$ 的零空间的非零向量，这在 $A$ 可逆时不可能发生。但如果 $A\mathbf{s}_k \neq 0$ 且 $(A\mathbf{s}_k)^T(A\mathbf{s}_k) = \|A\mathbf{s}_k\|_2^2$ 非常接近于零，数值上仍可能出现问题。
- 另一种更微妙的停滞发生在 $\omega_k=0$ 时。这种情况可能出现，例如，当矩阵 $A$ 是**斜对称 (skew-symmetric)** 的（$A^T = -A$）。在这种情况下，对于任何向量 $\mathbf{s}$，[内积](@entry_id:158127) $\langle A\mathbf{s}, \mathbf{s} \rangle = \mathbf{s}^T A^T \mathbf{s} = -\mathbf{s}^T A \mathbf{s} = -\langle A\mathbf{s}, \mathbf{s} \rangle$ 恒为零。这意味着 $\omega_k$ 的分子为零，导致 $\omega_k=0$。此时，稳定化步骤完全失效，算法可能停滞不前。一种解决方法是轻微扰动矩阵，例如用 $A_\delta = A + \delta I$ 替代 $A$，其中 $\delta$ 是一个小的正数，这可以打破斜对称性，使 $\omega_k$ 恢复非零值 [@problem_id:3210197]。
- 此外，如果 $\rho_k = \hat{\mathbf{r}}_0^T \mathbf{r}_k = 0$，也会导致算法停滞。这种情况可以通过选择不同的 $\hat{\mathbf{r}}_0$ 来避免，尽管 $\hat{\mathbf{r}}_0 = \mathbf{r}_0$ 是最常见的选择。

### 计算成本与内存需求

在评估一个迭代方法的实用性时，其计算开销和内存占用是两个关键指标。

**短递归特性**

[BiCGSTAB](@entry_id:143406) 的一个核心优势是它属于**短递归 (short-term recurrence)** 方法。这意味着在第 $k$ 次迭代中，计算所有必需的量只需要来自第 $k-1$ 次迭代的少数几个向量。它不需要存储从开始到当前迭代的所有历史信息。这与诸如[广义最小残差法](@entry_id:139566) (GMRES) 等**长递归 (long-term recurrence)** 方法形成鲜明对比。

**内存与计算量**

- **内存**: 由于其短递归特性，[BiCGSTAB](@entry_id:143406) 的内存需求是固定的，与迭代次数无关。一个典[型的实现](@entry_id:637593)需要存储大约 6 到 8 个大小为 $N$ 的向量（$N$ 是矩阵的维度），包括解、残差、搜索方向以及一些临时工作向量。这与 BiCG 的内存需求相当 [@problem_id:2208874]，但远小于需要存储整个[克雷洛夫子空间](@entry_id:751067)基的（未重启的）GMRES。

- **计算量**: BiCGSTAB 每一次迭代的主要计算成本在于**两次**矩阵-向量乘积（$A\mathbf{p}_k$ 和 $A\mathbf{s}_k$）。此外，还包括少量（通常是 4 次）向量[内积](@entry_id:158127)和数次向量的线性组合（AXPY 操作）。

**与 GMRES 的对比**

将 [BiCGSTAB](@entry_id:143406) 与另一个流行的非对称系统求解器 GMRES 进行比较，可以更清楚地看到其设计上的权衡 [@problem_id:3102092]。

- **内存占用**: [BiCGSTAB](@entry_id:143406) 的内存占用是常数级别的，非常适合内存受限的环境。而重启的 [GMRES(m)](@entry_id:749937) 的内存需求随重启周期 $m$ [线性增长](@entry_id:157553)。当 $m$ 较大时，GMRES 的内存开销会显著高于 [BiCGSTAB](@entry_id:143406)。

- **计算成本**: GMRES 每次（内部）迭代只需要**一次**矩阵-向量乘积，但它需要将新生成的[基向量](@entry_id:199546)与所有先前存储的[基向量](@entry_id:199546)进行正交化。这个正交化的成本随迭代次数的增加而[线性增长](@entry_id:157553)。因此，[BiCGSTAB](@entry_id:143406) 的每次迭代成本是固定的，而 [GMRES(m)](@entry_id:749937) 在一个重启周期内的平均迭代成本则依赖于 $m$。

- **收敛性**: GMRES 在每个重启周期内都保证[残差范数](@entry_id:754273)最小，具有最优性。[BiCGSTAB](@entry_id:143406) 没有这种严格的最优性保证，但其[混合策略](@entry_id:145261)通常在实践中表现优异。

选择哪种算法取决于具体问题。对于内存非常宝贵或矩阵-向量乘积相对便宜而向量操作昂贵的场景，[BiCGSTAB](@entry_id:143406) 可能是更好的选择。一个具体的例子是在电池供电的移动设备上进行科学计算，其中内存访问的能耗远高于浮点运算。在这种情况下，GMRES 随 $m$ 增长的内存占用和正交化带来的大量内存读写可能导致其总能耗高于 BiCGSTAB，即使 GMRES 可能需要更少的矩阵-向量乘积 [@problem_id:3102092]。

### [预处理](@entry_id:141204)的角色：[左预处理](@entry_id:165660)与[右预处理](@entry_id:173546)

对于所有[克雷洛夫子空间方法](@entry_id:144111)而言，**预处理 (preconditioning)** 都是提升性能、加速收敛的关键。[预处理](@entry_id:141204)旨在将原始系统 $A\mathbf{x}=\mathbf{b}$ 变换为一个谱特性更好（例如，[特征值](@entry_id:154894)更聚集）的等价系统，从而使迭代求解器能更快地收敛。预处理矩阵 $M$ 的应用方式分为两种：[左预处理](@entry_id:165660)和[右预处理](@entry_id:173546)。这两种方式对 BiCGSTAB 的行为，特别是[收敛监控](@entry_id:747855)，有着微妙而重要的影响 [@problem_id:3210141]。

**[左预处理](@entry_id:165660) (Left Preconditioning)**

在[左预处理](@entry_id:165660)中，我们求解变换后的系统：
$$ (M^{-1}A)\mathbf{x} = M^{-1}\mathbf{b} $$
[BiCGSTAB](@entry_id:143406) 算法被直接应用于矩阵 $\hat{A} = M^{-1}A$ 和右端项 $\hat{\mathbf{b}} = M^{-1}\mathbf{b}$。因此，算法内部计算和最小化的残差是**预处理后的残差** $\hat{\mathbf{r}}_k = \hat{\mathbf{b}} - \hat{A}\mathbf{x}_k = M^{-1}(\mathbf{b}-A\mathbf{x}_k) = M^{-1}\mathbf{r}_k$。
这意味着 [BiCGSTAB](@entry_id:143406) 的稳定化步骤旨在减小 $\|M^{-1}\mathbf{r}_k\|_2$ 的范数。然而，我们通常关心的[停止准则](@entry_id:136282)是基于**真实残差** $\mathbf{r}_k$ 的范数，例如 $\|\mathbf{r}_k\|_2 \le \epsilon \|\mathbf{b}\|_2$。由于 $\|M^{-1}\mathbf{r}_k\|_2$ 与 $\|\mathbf{r}_k\|_2$ 并不直接相等（除非 $M$ 是[正交矩阵](@entry_id:169220)），仅监控预处理残差的减小可能会导致对真实误差的错误估计，从而过早或过晚地终止迭代。

**[右预处理](@entry_id:173546) (Right Preconditioning)**

在[右预处理](@entry_id:173546)中，我们通过变量替换 $\mathbf{x} = M^{-1}\mathbf{y}$ 来求解系统：
$$ (AM^{-1})\mathbf{y} = \mathbf{b} $$
BiCGSTAB 被应用于矩阵 $\bar{A} = AM^{-1}$ 和右端项 $\mathbf{b}$，以求解中间变量 $\mathbf{y}$。然后通过 $\mathbf{x}_k = M^{-1}\mathbf{y}_k$ 恢复原始解的近似。
[右预处理](@entry_id:173546)的一个美妙之处在于其残差的性质。算法内部计算的残差是：
$$ \bar{\mathbf{r}}_k = \mathbf{b} - \bar{A}\mathbf{y}_k = \mathbf{b} - (AM^{-1})\mathbf{y}_k = \mathbf{b} - A\mathbf{x}_k = \mathbf{r}_k $$
这意味着在[右预处理](@entry_id:173546)下，[BiCGSTAB](@entry_id:143406) 算法内部自然计算和更新的残差**就是真实的残差** $\mathbf{r}_k$。因此，它的稳定化步骤直接作用于减小 $\|\mathbf{r}_k\|_2$。这使得[收敛监控](@entry_id:747855)变得非常直接和方便：我们可以直接使用算法内部的[残差范数](@entry_id:754273)来应用[停止准则](@entry_id:136282)，而无需任何额外的计算或转换。

综上所述，虽然左、[右预处理](@entry_id:173546)在理论上都可以加速收敛，但从实现和[收敛监控](@entry_id:747855)的便利性角度看，**[右预处理](@entry_id:173546)与 [BiCGSTAB](@entry_id:143406) 的结合更为自然和稳健**。

本章系统地阐述了 [BiCGSTAB](@entry_id:143406) 方法的原理、机制、性能特点及其在实践中的重要考量。通过与 BiCG 和 GMRES 的对比，以及对预处理技术的深入分析，我们希望读者能够全面地掌握这一强大的数值工具，并能在未来的[科学计算](@entry_id:143987)实践中灵活应用。