## 引言
在现代[计算固体力学](@entry_id:169583)中，对复杂[非线性](@entry_id:637147)问题的分析已成为标准实践，其核心依赖于强大的[迭代求解器](@entry_id:136910)。然而，每一个迭代过程都面临一个根本性问题：何时可以停止迭代，并确信我们得到的近似解已经“足够精确”？这个问题的答案，正是由**[残差范数](@entry_id:754273)与[收敛准则](@entry_id:158093)**所定义。它们是确保[数值模拟](@entry_id:137087)结果既准确又高效的关键，构成了连接理论方程与可靠工程预测之间的最后一道关卡。

若[收敛准则](@entry_id:158093)过于宽松，可能导致解严重偏离真实的物理平衡状态；若过于严苛，则可能导致计算资源的大量浪费，甚至在有限精度下永不收敛。因此，理解并正确设置[收敛准则](@entry_id:158093)，是高级[有限元分析](@entry_id:138109)中一项至关重要的技能。本文旨在填补理论学习与实际应用之间的知识鸿沟，系统性地揭示收敛判断背后的力学原理与数值考量。

通过本文，读者将踏上一段从基础到前沿的探索之旅。在“**原理与机制**”一章中，我们将深入剖析残差的物理本质、不同范数的力学含义以及如何构建稳健的[收敛判据](@entry_id:158093)。接着，在“**应用与跨学科连接**”一章中，我们将展示这些准则如何在塑性、接触、断裂力学、[多尺度模拟](@entry_id:752335)等复杂场景中发挥关键作用。最后，“**动手实践**”部分将通过具体的计算练习，帮助您将理论知识转化为实践能力。让我们首先从第一章开始，揭开残差与[收敛准则](@entry_id:158093)的基本原理，为后续的深入学习奠定坚实的基础。

## 原理与机制

在[计算固体力学](@entry_id:169583)中，对[非线性](@entry_id:637147)问题的求解本质上是一个迭代过程，其核心目标是找到一个[位移场](@entry_id:141476)，使得离散系统中的[内力与外力](@entry_id:170589)[达到平衡](@entry_id:170346)。为了量化这一平衡状态，并确定迭代何时可以停止，我们必须引入**残差（residual）**的概念。本章将深入探讨残差的定义、物理意义、度量方法以及如何基于残差构建稳健的[收敛准则](@entry_id:158093)。

### 残差的定义与物理内涵

在[有限元离散化](@entry_id:193156)后，一个静态或准静态问题的控制方程可以从[虚功原理](@entry_id:138749)中导出。对于一个[非线性](@entry_id:637147)材料或经历大变形的物体，虚功原理指出，对于任意[运动学](@entry_id:173318)容许的[虚位移](@entry_id:168781) $\delta\mathbf{u}$，[内力](@entry_id:167605)[虚功](@entry_id:176403)等于外力[虚功](@entry_id:176403)。经过有限元离散，这一原理最终转化为一个关于节点位移向量 $\mathbf{d}$ 的[非线性](@entry_id:637147)[代数方程](@entry_id:272665)组：

$\mathbf{f}_{\mathrm{int}}(\mathbf{d}) = \mathbf{f}_{\mathrm{ext}}$

其中，$\mathbf{f}_{\mathrm{ext}}$ 是由外部载荷（如[体力](@entry_id:174230)、面力）转化而来的等效节点力向量，通常在载荷步内是恒定的。而 $\mathbf{f}_{\mathrm{int}}(\mathbf{d})$ 是与当前节点位移 $\mathbf{d}$ 对应的等效节点[内力向量](@entry_id:750751)，它通过对单元应力进行积分得到，并且是位移 $\mathbf{d}$ 的一个复杂[非线性](@entry_id:637147)函数。

在迭代求解过程中，我们得到一系列位移的近似解 $\mathbf{d}^{(k)}$。在任意一次迭代中，当前的位移解 $\mathbf{d}^{(k)}$ 几乎不可能精确满足上述平衡方程。此时，[内力与外力](@entry_id:170589)之间存在一个差值，我们将其定义为**残差向量（residual vector）** $\mathbf{r}(\mathbf{d})$：

$\mathbf{r}(\mathbf{d}) = \mathbf{f}_{\mathrm{ext}} - \mathbf{f}_{\mathrm{int}}(\mathbf{d})$

从物理上看，[残差向量](@entry_id:165091) $\mathbf{r}(\mathbf{d})$ 代表了在当前位移状态下，施加在每个节点自由度上的**净[不平衡力](@entry_id:753019)（net out-of-balance force）**。当系统达到真正的离散平衡时，每个节点上的[合力](@entry_id:163825)必须为零，这意味着[残差向量](@entry_id:165091)的所有分量都必须为零，即 $\mathbf{r}(\mathbf{d})=\mathbf{0}$。因此，[非线性有限元](@entry_id:173184)求解的整个过程，可以被视为一个寻找[位移场](@entry_id:141476) $\mathbf{d}$ 以使[残差向量](@entry_id:165091)趋近于零的寻根过程 [@problem_id:3595533]。

对于保守系统（即载荷和材料行为可以从一个[势能](@entry_id:748988)中导出），残差向量与系统的总势能 $\Pi(\mathbf{d})$ 之间存在深刻的联系。总[势能](@entry_id:748988)是[应变能](@entry_id:162699)与外力[势能](@entry_id:748988)之和，而平衡状态对应于总势能的驻点。在数学上，这意味着总势能对节点位移的梯度为零。可以证明，[残差向量](@entry_id:165091)正是总[势能梯度](@entry_id:167095)的负值：

$\mathbf{r}(\mathbf{d}) = -\nabla_{\mathbf{d}} \Pi(\mathbf{d})$

因此，驱动残差 $\mathbf{r}(\mathbf{d})$ 趋于零的过程，在数学上等价于寻找系统总势能 $\Pi(\mathbf{d})$ 的一个[驻点](@entry_id:136617)（通常是极小值点）[@problem_id:3595533]。

为了更具体地理解残差的构成，我们可以考察一个简单的例子。考虑一根一维杆，我们将其离散为有限个单元。其[残差向量](@entry_id:165091) $\mathbf{r}$ 的计算需要两个部分：外力向量 $\mathbf{f}_{\mathrm{ext}}$ 和[内力向量](@entry_id:750751) $\mathbf{f}_{\mathrm{int}}$。外力向量由施加的[体力](@entry_id:174230)（如重力）和端点处的面力（牵[引力](@entry_id:175476)）通过形函数积分得到。[内力向量](@entry_id:750751)则通过组装每个单元的内力来获得，而单元内力由[单元刚度矩阵](@entry_id:139369)与单元节点位移的乘积计算得出，即 $\mathbf{f}_{\mathrm{int}} = \mathbf{K}\mathbf{d}$（在线性情况下）。给定一个试验位移场 $\mathbf{d}_{\text{trial}}$，我们可以计算出对应的[内力](@entry_id:167605) $\mathbf{f}_{\mathrm{int}}(\mathbf{d}_{\text{trial}})$，然后从外力向量中减去它，从而得到在每个节点上具体的数值[不平衡力](@entry_id:753019) [@problem_id:3595499]。

### 度量残差：范数及其解释

残差是一个向量，为了在[收敛判据](@entry_id:158093)中使用它，我们需要一个标量来衡量其“大小”。这个标量就是**范数（norm）**。不同的范数从不同角度衡量向量的大小，因此它们对残差的[分布](@entry_id:182848)具有不同的敏感性。

最常用的范数包括：

*   **欧几里得范数（Euclidean norm, $\ell_2$ norm）**: 定义为 $\left\| \mathbf{r} \right\|_2 = \sqrt{\sum_i r_i^2}$。它衡量了[残差向量](@entry_id:165091)的总体大小，对所有分量的贡献进行了平方和平均。因此，它对于[分布](@entry_id:182848)在多个自由度上的中等大小的残差分量较为敏感。

*   **[无穷范数](@entry_id:637586)（Infinity norm, $\ell_\infty$ norm）**: 定义为 $\left\| \mathbf{r} \right\|_\infty = \max_i |r_i|$。它只关注最大的那个[不平衡力](@entry_id:753019)分量，对于局部出现的“尖峰”状残差最为敏感。如果一个模型的某个局部区域出现严重的[平衡问题](@entry_id:636409)，[无穷范数](@entry_id:637586)会很有效地捕捉到它。

为了理解不同范数的敏感性差异，设想一个由三个独立的弹簧组成的系统，其刚度差异很大。若残差向量为 $\mathbf{r} = [10, 100, 12]^\top$，[无穷范数](@entry_id:637586)会立即识别出第二个自由度（分量为100）是最大的不[平衡点](@entry_id:272705)。而欧几里得范数则会综合考量所有分量 [@problem_id:3595489]。

除了这些标[准范数](@entry_id:753960)，力学中还有一个至关重要的范数——**能量范数（energy norm）**。要理解它，我们必须首先区分**代数残差（algebraic residual）** $\mathbf{r}(\mathbf{u})$ 和**位移误差（displacement error）** $\mathbf{e} = \mathbf{u} - \mathbf{u}^\star$，其中 $\mathbf{u}^\star$ 是离散方程的精确解。残差是在力空间中衡量[平衡方程](@entry_id:172166)被违反的程度，而误差是在位移空间中衡量当前解与精确解的距离。对于[线性系统](@entry_id:147850) $\mathbf{K}\mathbf{u}=\mathbf{f}$，这两者通过刚度矩阵 $\mathbf{K}$ 精确关联 [@problem_id:3595481]：

$\mathbf{r}(\mathbf{u}) = \mathbf{f} - \mathbf{K}\mathbf{u} = \mathbf{K}\mathbf{u}^\star - \mathbf{K}\mathbf{u} = \mathbf{K}(\mathbf{u}^\star - \mathbf{u}) = \mathbf{K}(-\mathbf{e}) = -\mathbf{K}\mathbf{e}$

这个关系表明，残差是位移误差通过[刚度矩阵](@entry_id:178659)“映射”到力空间的结果。

基于此，我们可以定义一个由 $\mathbf{K}^{-1}$ 诱导的范数，通常称为**[对偶范数](@entry_id:200340)（dual norm）**或[能量范数](@entry_id:274966)的对偶：

*   **$K^{-1}$-范数**: $\left\| \mathbf{r} \right\|_{\mathbf{K}^{-1}} = \sqrt{\mathbf{r}^\top \mathbf{K}^{-1} \mathbf{r}}$

这个范数具有非凡的物理意义。位移误差 $\mathbf{e}$ 所对应的应变能为 $\frac{1}{2}\mathbf{e}^\top \mathbf{K} \mathbf{e}$。利用关系 $\mathbf{e} = -\mathbf{K}^{-1}\mathbf{r}$，可以证明：

$\left( \left\| \mathbf{r} \right\|_{\mathbf{K}^{-1}} \right)^2 = \mathbf{r}^\top \mathbf{K}^{-1} \mathbf{r} = \mathbf{e}^\top \mathbf{K} \mathbf{e} = \left( \left\| \mathbf{e} \right\|_{\mathbf{K}} \right)^2$

其中 $\left\| \mathbf{e} \right\|_{\mathbf{K}} = \sqrt{\mathbf{e}^\top \mathbf{K} \mathbf{e}}$ 是误差的[能量范数](@entry_id:274966)。这意味着，我们虽然无法直接计算不可知的位移误差 $\mathbf{e}$ 的[能量范数](@entry_id:274966)，但它竟然精确地等于我们可计算的残差 $\mathbf{r}$ 的 $K^{-1}$-范数 [@problem_id:3595468]。

$K^{-1}$-范数对残差分量的加权方式非常独特。对于对角刚度矩阵 $\mathbf{K} = \mathrm{diag}(k_i)$，$\left\| \mathbf{r} \right\|_{\mathbf{K}^{-1}}^2 = \sum_i r_i^2/k_i$。这表明，残差分量 $r_i$ 的贡献被其对应方向的刚度 $k_i$ 所缩放。如果某个方向非常**柔顺（compliant）**（即刚度 $k_i$ 很小），那么即使是一个很小的残差 $r_i$ 也会被放大，从而对范数产生巨大贡献。反之，在非常**刚硬（stiff）**的方向上，较大的残差也可能被忽略。因此，$K^{-1}$-范数对结构中柔性区域的力不[平衡问题](@entry_id:636409)最为敏感，而这些区域往往是产生最大位移误差的地方 [@problem_id:3595489]。

### 制定稳健的[收敛准则](@entry_id:158093)

一个好的[收敛准则](@entry_id:158093)必须能够可靠地判断迭代解是否“足够接近”真实解，同时要对不同问题、不同载荷工况和不同模型尺度都具有稳健性。

#### 残差准则 vs. 位移增量准则

在[非线性](@entry_id:637147)分析中，牛顿法（Newton's method）的每一步都求解一个线性方程组：

$\mathbf{J}(\mathbf{u}_k) \Delta \mathbf{u}_k = \mathbf{r}(\mathbf{u}_k)$

其中 $\mathbf{J}(\mathbf{u}_k)$ 是在当前位移 $\mathbf{u}_k$ 处的**[切线刚度矩阵](@entry_id:170852)（tangent stiffness matrix）**，$\Delta \mathbf{u}_k$ 是位移增量。这个关系揭示了两种主要的[收敛判据](@entry_id:158093)家族：

1.  **残差准则**: 基于[残差范数](@entry_id:754273)，如 $\left\| \mathbf{r}(\mathbf{u}_k) \right\| \le \tau_R$。
2.  **位移增量准则**: 基于位移增量范数，如 $\left\| \Delta \mathbf{u}_k \right\| \le \tau_D$。

这两种准则各有优劣。从上述关系可得 $\Delta \mathbf{u}_k = \mathbf{J}_k^{-1} \mathbf{r}_k$ 以及 $\mathbf{r}_k = \mathbf{J}_k \Delta \mathbf{u}_k$。取范数后，我们得到两个不等式：

$\left\| \Delta \mathbf{u}_k \right\| \le \left\| \mathbf{J}_k^{-1} \right\| \left\| \mathbf{r}_k \right\|$
$\left\| \mathbf{r}_k \right\| \le \left\| \mathbf{J}_k \right\| \left\| \Delta \mathbf{u}_k \right\|$

这些不等式揭示了两种准则的“盲点”[@problem_id:3595484]：
*   **[病态问题](@entry_id:137067)（Ill-conditioned Problem）**: 当系统接近失稳点（如屈曲）时，[切线刚度矩阵](@entry_id:170852) $\mathbf{J}_k$ 变得奇[异或](@entry_id:172120)接近奇异，其逆的范数 $\left\| \mathbf{J}_k^{-1} \right\|$ 会非常大。此时，即使[残差范数](@entry_id:754273) $\left\| \mathbf{r}_k \right\|$ 已经很小，位移增量 $\left\| \Delta \mathbf{u}_k \right\|$ 仍可能非常大。如果只使用残差准则，求解器可能会在解仍在剧烈变化时过早地宣告收敛。
*   **刚硬问题（Stiff Problem）**: 对于非常刚硬的结构，$\left\| \mathbf{J}_k \right\|$ 会很大。此时，即使位移增量 $\left\| \Delta \mathbf{u}_k \right\|$ 已经很小，[残差范数](@entry_id:754273) $\left\| \mathbf{r}_k \right\|$ 仍可能很大。如果只使用位移增量准则，求解器可能会在系统仍存在显著的力不平衡时停止迭代。

因此，一个真正稳健的求解器通常会同时监控残差和位移增量，或者使用一个能同时反映两者的组合准则，例如基于能量的准则 [@problem_id:3595484]。

#### 绝对容差 vs. 相对容差

仅使用一个固定的绝对容差（absolute tolerance）$\tau_{abs}$，如 $\left\| \mathbf{r}_k \right\| \le \tau_{abs}$，是不可靠的。对于一个承受巨大载荷的桥梁模型和一个承受微小载荷的微机电系统（MEMS）模型，一个固定的力容差（如 $1\ \mathrm{N}$）的物理意义天差地别。

更稳健的方法是使用**相对容差（relative tolerance）** $\tau_{rel}$，将当前残差与一个代表问题尺度的参考力进行比较。一个关键问题是：选择哪个参考力？

*   **选项1：外力范数 $\left\| \mathbf{f}_{\mathrm{ext}} \right\|$**: 一个看似自然的选择是使用外载荷[向量的范数](@entry_id:154882)，判据为 $\left\| \mathbf{r}_k \right\| / \left\| \mathbf{f}_{\mathrm{ext}} \right\| \le \tau_{rel}$。然而，这种方法在很多重要情况下会失效，例如[位移控制](@entry_id:748569)加载、[热应力分析](@entry_id:154981)或者卸载过程，这些情况下 $\mathbf{f}_{\mathrm{ext}}$ 可能为零或非常小，导致分母为零或判据变得异常严格 [@problem_id:3595530]。

*   **选项2：初始[残差范数](@entry_id:754273) $\left\| \mathbf{r}_0 \right\|$**: 一个更通用的选择是使用当前增量步开始时的初始残差 $\mathbf{r}_0$ 作为参考。$\mathbf{r}_0$ 代表了该增量步需要消除的总不平衡量。判据 $\left\| \mathbf{r}_k \right\| / \left\| \mathbf{r}_0 \right\| \le \tau_{rel}$ 要求残差相比于初始值有一个显著的下降。

最先进的商业有限元软件通常采用一种组合策略，结合了绝对容差和相对容差 [@problem_id:3595530]：

$\left\| \mathbf{r}_k \right\| \le \tau_{abs} + \tau_{rel} \left\| \mathbf{r}_0 \right\|$

这种形式的优点在于：
*   当初始残差 $\left\| \mathbf{r}_0 \right\|$ 很大时，$\tau_{rel} \left\| \mathbf{r}_0 \right\|$ 项占主导，确保了残差的相对减小。
*   当初始残差 $\left\| \mathbf{r}_0 \right\|$ 本身就很小（例如，在一个非常小的载荷步中），或者当迭代接近收敛时，$\tau_{abs}$ 项提供了一个绝对的“地板”，防止求解器在已经足够精确的情况下进行不必要的过度迭代。

#### 残差与误差的关系及[条件数](@entry_id:145150)

[收敛准则](@entry_id:158093)的目标是间接地控制我们真正关心的位移误差 $\mathbf{e}$。从关系式 $\mathbf{e} = -\mathbf{K}^{-1}\mathbf{r}$ 可得不等式：

$\left\| \mathbf{e} \right\| \le \left\| \mathbf{K}^{-1} \right\| \left\| \mathbf{r} \right\|$

这个不等式是[计算力学](@entry_id:174464)的核心关系之一 [@problem_id:3595481]。它表明，[残差范数](@entry_id:754273) $\left\| \mathbf{r} \right\|$ 与[误差范数](@entry_id:176398) $\left\| \mathbf{e} \right\|$ 之间的[转换因子](@entry_id:142644)是 $\left\| \mathbf{K}^{-1} \right\|$。如果系统是病态的，即 $\mathbf{K}$ 接近奇异，那么 $\left\| \mathbf{K}^{-1} \right\|$ 会非常大。在这种情况下，一个很小的残差仍然可能对应一个很大的误差。

这个概念可以用**[条件数](@entry_id:145150)（condition number）** $\kappa(\mathbf{K}) = \left\| \mathbf{K} \right\| \left\| \mathbf{K}^{-1} \right\|$ 来更正式地表述。对于相对误差，我们有如下经典界 [@problem_id:3595468]：

$\frac{\left\| \mathbf{e} \right\|}{\left\| \mathbf{u}^\star \right\|} \le \kappa(\mathbf{K}) \frac{\left\| \mathbf{r} \right\|}{\left\| \mathbf{f} \right\|}$

这个不等式清晰地表明，[病态问题](@entry_id:137067)（大[条件数](@entry_id:145150) $\kappa(\mathbf{K})$）会放大相对残差，导致相对误差可能比我们从残差大小所预期的要大得多。因此，仅仅残差小并不足以保证误差也小，系统的**条件（conditioning）**至关重要。这也解释了为什么在病态问题中，即使残差准则满足了，有时仍需检查位移增量，因为后者可能更能揭示解的真实变化。为了改善求解的稳健性，可以使用**[预条件子](@entry_id:753679)（preconditioner）** $\mathbf{M}$，它近似于 $\mathbf{K}$ 但更容易求逆，通过求解等价的预条件系统来降低有效条件数，从而使残差能更可靠地控制误差 [@problem_id:3595468]。

### 实际应用中的高级考量

在真实的工程应用中，构建一个放之四海而皆准的[收敛准则](@entry_id:158093)还需要考虑更多细节。

#### 处理混合单位自由度

许多有限元模型，如[壳单元](@entry_id:176094)和[梁单元](@entry_id:746744)，在每个节点上包含具有不同物理单位的自由度（例如，[平动](@entry_id:187700)位移，单位为米；转动位移，单位为弧度）。对应的[残差向量](@entry_id:165091)也包含混合单位的分量（例如，力，单位为牛顿；力矩，单位为牛顿·米）。

在这种情况下，直接计算[欧几里得范数](@entry_id:172687) $\sqrt{r_x^2 + r_y^2 + r_\theta^2}$ 是物理上无意义的，因为这相当于将力的平方与力矩的平方相加。其结果会随着单位制（例如，米 vs. 毫米）的选择而剧烈变化。

正确的做法是对残差向量进行**缩放（scaling）**，使其[无量纲化](@entry_id:136704)。这通常通过一个[对角缩放](@entry_id:748382)矩阵 $\mathbf{W}$ 来实现，[收敛判据](@entry_id:158093)作用于缩放后的[残差范数](@entry_id:754273) $\left\| \mathbf{W} \mathbf{r} \right\|$。一个物理上一致的缩放方法是，用力分量除以一个参考力 $F_{\mathrm{ref}}$，用力矩分量除以一个参考力矩 $M_{\mathrm{ref}}$。为了保持物理平衡，参考力矩不应随意选取，而应由参考力和一个模型的**特征长度（characteristic length）** $L_{\mathrm{char}}$ 导出，即 $M_{\mathrm{ref}} = F_{\mathrm{ref}} \cdot L_{\mathrm{char}}$。因此，一个合理的[缩放矩阵](@entry_id:188350)形如 [@problem_id:3595465]：

$\mathbf{W} = \mathrm{diag} \left( \frac{1}{F_{\mathrm{ref}}}, \dots, \frac{1}{F_{\mathrm{ref}} \cdot L_{\mathrm{char}}}, \dots \right)$

通过这种方式，缩放后的残差向量 $\mathbf{W}\mathbf{r}$ 的所有分量都变成无量纲的，可以有意义地进行范数计算。

#### 网格无关的[收敛准则](@entry_id:158093)

当对一个模型进行网格加密时，自由度的总数 $n_{\mathrm{dof}}$ 会增加。标准的 $\ell_2$ 范数 $\left\| \mathbf{r} \right\|_2 = \sqrt{\sum r_i^2}$ 会随着 $n_{\mathrm{dof}}$ 的增加而系统性地变化（通常是减小，因为总载荷[分布](@entry_id:182848)在更多节点上）。这意味着，对于不同密度的网格，一个固定的[收敛容差](@entry_id:635614)在物理上代表了不同的平衡精度。

为了获得一个**网格无关（mesh-independent）**的准则，我们需要将范数以某种方式归一化。一个有效的方法是控制每个自由度的平均不平衡量。例如，我们可以使用**均方根（Root-Mean-Square, RMS）**残差 [@problem_id:3595458]：

$\frac{\left\| \mathbf{r} \right\|_2}{\sqrt{n_{\mathrm{dof}}}} \le \tau$

这个准则衡量的就是“平均每个自由度”的残差大小，它在[网格细化](@entry_id:168565)时表现得更为稳定。[无穷范数](@entry_id:637586) $\left\| \mathbf{r} \right\|_\infty$ 本身就是一种“每个自由度”的度量（因为它只看最大的那个），因此它天然具有较好的[网格无关性](@entry_id:634417) [@problem_id:3595458]。

#### 有限精度下的收敛极限

最后，我们必须认识到，计算机使用有限精度[浮点数](@entry_id:173316)进行运算，这为收敛设定了最终的极限。残差的计算 $ \mathbf{r}_k = \mathbf{f}_{\mathrm{ext}} - \mathbf{f}_{\mathrm{int}}(\mathbf{u}_k) $ 涉及到两个大小相近的向量相减。当迭代解 $\mathbf{u}_k$ 非常接近精确解时，$\mathbf{f}_{\mathrm{int}}(\mathbf{u}_k)$ 在数值上会非常接近 $\mathbf{f}_{\mathrm{ext}}$。此时，浮点减法会产生巨大的**抵消误差（cancellation error）**。

这意味着，即使理论上的真实残差可以继续减小，计算出的[残差范数](@entry_id:754273)也会被累积的**舍入误差（round-off error）**所主导，从而在一个非零的“噪声平台”上停滞不前。如果[收敛容差](@entry_id:635614)设置得低于这个噪声平台，求解器将永远无法满足判据，最终因达到最大迭代次数而失败。

从观测到的[残差范数](@entry_id:754273)历史中可以清晰地看到这种平台效应。例如，[残差范数](@entry_id:754273)序列可能呈现 $10^{-3}, 10^{-5}, 10^{-7}, 8\times10^{-9}, 8.1\times10^{-9}, 8.0\times10^{-9}, \dots$ 的行为。一旦[残差范数](@entry_id:754273)停止显著下降并开始在一个水平上[振荡](@entry_id:267781)，就表明已经达到了[机器精度](@entry_id:756332)的极限 [@problem_id:3595520]。

一个先进的[收敛准则](@entry_id:158093)必须能够识别这种停滞现象。除了标准的[绝对和相对容差](@entry_id:163682)检查外，还应包含一个**平台检测（plateau detection）**机制。该机制会监控最近几次迭代中[残差范数](@entry_id:754273)的下降率。如果[残差范数](@entry_id:754273)已经进入了预估的噪声区域，并且在连续数次迭代内几乎没有变化，求解器就应该宣告收敛，并认为已经达到了在该计算精度下可能达到的最佳平衡状态 [@problem_id:3595520]。