## 引言
在计算流体力学领域，对不可压缩Navier-Stokes方程的数值求解是一个长期存在的挑战。其核心困难在于速度场与压力场的紧密耦合：动量方程描述了速度的演化，而不可压缩约束则是一个必须瞬时满足的代数条件，这使得整个系统呈现出复杂的微分-代数结构。直接求解这一耦合系统会形成一个大型、不定的鞍点问题，计算成本高昂且数值处理困难。为了克服这一障碍，压力修正格式应运而生，它通过一种巧妙的分裂思想，将原问题分解为一系列计算上更易于处理的子问题，极大地提升了求解效率。

本文将系统性地探讨这类方法中的两种主流变体：增量式（incremental）与旋转式（rotational）压力修正格式。在“原理与机制”一章中，我们将深入其核心的投影思想和代数构造。接着，在“应用与跨学科连接”中，我们将探索这些方法在进阶分析、复杂流动模拟以及与其他学科交叉领域的应用与扩展。最后，通过“动手实践”部分，您将有机会通过具体的数值练习来巩固所学知识。现在，让我们从理解这些方法的基本原理开始，揭示它们如何巧妙地解耦速度与压力。

## 原理与机制

在数值求解不可压缩Navier-Stokes方程时，一个核心的挑战源于其独特的数学结构。速度场 $\boldsymbol{u}$ 和压力场 $p$ 通过一个微分-代数系统耦合在一起：动量方程是一个关于速度的演化方程，而不可压缩条件 $\nabla \cdot \boldsymbol{u} = 0$ 则是一个瞬时满足的约束。本章将深入探讨一类广泛用于应对这一挑战的高效算法——压力修正格式（pressure-correction schemes），重点阐述其增量（incremental）和旋转（rotational）两种主要变体的基本原理与核心机制。

### 鞍点问题与分裂策略

为了理解压力修正法的动机，我们首先考察Navier-Stokes方程在时间和空间上离散后产生的代数系统。以一个简单的向后欧拉时间离散为例，在时间层 $n$ 求解 $(\boldsymbol{u}^n, p^n)$ 的全耦合（monolithic）系统可以写成如下的矩阵形式 [@problem_id:3408455] [@problem_id:3408456]：

$$
\begin{pmatrix}
A  B^{\top} \\
B  0
\end{pmatrix}
\begin{pmatrix}
\boldsymbol{u}^{n} \\
p^{n}
\end{pmatrix}
=
\begin{pmatrix}
\boldsymbol{r} \\
0
\end{pmatrix}
$$

这里，$\boldsymbol{u}^{n}$ 和 $p^{n}$ 分别是速度和压力的离散未知向量。矩阵 $A$ 代表动量输运算子，包含了由时间导数项产生的质量矩阵以及对流和扩散项的离散化形式。矩阵 $B$ 是离散散度算子，其转置 $B^{\top}$ 则是离散梯度算子。右端项 $\boldsymbol{r}$ 包含了上一时间步的信息和外力项。

这个系统的关键特征在于其左侧系数矩阵的 $(2,2)$ 区块为零。这反映了压力 $p$ 在不可压缩流体中扮演的角色：它不是一个由本构关系决定的状态变量，而是一个拉格朗日乘子，其唯一的作用是施加 $\nabla \cdot \boldsymbol{u} = 0$ 这个约束。这种结构导致整个矩阵是**不定（indefinite）**的，形成了一个典型的**鞍点问题（saddle-point problem）**。直接求解这样的大型不定系统在计算上是昂贵且复杂的，通常需要专门的预条件子和迭代方法。

压力修正法提供了一种巧妙的替代方案，其核心思想是**分裂（splitting）**或**解耦（decoupling）**。它避免了直接求解庞大而复杂的鞍点问题，代之以一系列更小、性质更好的子问题。具体来说，该方法将一个时间步内的求解过程分解为两个主要阶段：

1.  **预测步（Predictor Step）**：首先求解一个不包含或仅使用旧压力信息的动量方程，得到一个中间速度场，称为**暂估速度（tentative velocity）** $\boldsymbol{u}^*$。这个速度场通常不满足不可压缩约束，即 $\nabla \cdot \boldsymbol{u}^* \neq 0$。

2.  **修正步（Correction Step）**：然后，通过求解一个关于压力的方程来修正暂估速度，使得最终得到的速度场 $\boldsymbol{u}^n$ 满足不可压缩约束。

这种解耦策略的主要优势在于，压力子问题通常可以转化为一个**对称正定（Symmetric Positive Definite, SPD）**的泊松型方程。这类方程可以使用高效的迭代方法（如共轭梯度法）快速求解。然而，这种计算效率的提升是以引入**分裂误差（splitting error）**为代价的。分裂误差源于对速度-压力耦合的近似处理，它会影响算法的整体精度和稳定性，尤其是在边界附近 [@problem_id:3408455]。

### 投影法的核心机制与增量格式

压力修正法的修正步在数学上可以被理解为一个**投影（projection）**操作。其理论基础是**亥姆霍兹-霍奇分解（Helmholtz-Hodge decomposition）**，该定理指出任何一个足够光滑的向量场都可以唯一地分解为一个无散场（divergence-free field）和一个无旋场（curl-free field，即梯度场）的和。投影步的目标就是从暂估速度 $\boldsymbol{u}^*$ 中移除那个导致其不满足无散条件的梯度分量。

#### 约束优化视角

一个深刻的理解方式是将投影步视为一个带约束的优化问题 [@problem_id:3408466]。我们寻求一个新的速度场 $\boldsymbol{u}^{n+1}$，它在所有满足离散无散约束 $D \boldsymbol{u}^{n+1} = 0$ 的速度场中，与暂估速度 $\boldsymbol{u}^*$ 的“距离”最近。这里的“距离”通常由离散动能的差异来度量。该优化问题可表述为：

$$
\min_{\boldsymbol{u}} \frac{1}{2} (\boldsymbol{u} - \boldsymbol{u}^*)^{\top} M (\boldsymbol{u} - \boldsymbol{u}^*) \quad \text{subject to} \quad D \boldsymbol{u} = 0
$$

其中 $M$ 是离散质量矩阵。引入拉格朗日乘子 $\phi$ 来处理约束条件，我们可以构造拉格朗日函数并求解其KKT（Karush-Kuhn-Tucker）条件。这直接导出了修正步的核心方程：

1.  **速度修正**：$\boldsymbol{u}^{n+1} = \boldsymbol{u}^* - \Delta t G \phi$
2.  **无散约束**：$D \boldsymbol{u}^{n+1} = 0$

这里，$G$ 是离散梯度算子（在适当定义下为 $-D^{\top}$），$\phi$ 是一个与压力相关的标量场。拉格朗日乘子 $\phi$ 的出现，恰恰揭示了压力在不可压缩流中的本质——作为强制执行无散约束的工具。

#### 标准增量压力修正格式（IPCS）

基于上述思想，标准的**增量压力修正格式（Incremental Pressure-Correction Scheme, IPCS）**将一个完整的时间步分解为以下几个子步骤 [@problem_id:3408404]：

1.  **暂估速度步**：求解动量方程以获得暂估速度 $\boldsymbol{u}^*$。此时，压力梯度项使用上一时间步的压力 $p^n$：
    $$
    \frac{\boldsymbol{u}^* - \boldsymbol{u}^n}{\Delta t} + \mathcal{N}(\boldsymbol{u}^n) - \nu \Delta \boldsymbol{u}^* + \nabla p^n = \boldsymbol{f}^{n+1}
    $$
    其中 $\mathcal{N}(\boldsymbol{u}^n)$ 代表对流项的离散形式。

2.  **压力泊松方程（PPE）**：将速度修正公式 $\boldsymbol{u}^{n+1} = \boldsymbol{u}^* - \Delta t \nabla \phi$ 代入无散约束 $\nabla \cdot \boldsymbol{u}^{n+1} = 0$ 中，我们得到一个关于压力增量 $\phi$ 的泊松方程 [@problem_id:3408403]：
    $$
    \nabla^2 \phi = \frac{1}{\Delta t} \nabla \cdot \boldsymbol{u}^*
    $$

3.  **PPE的边界条件**：为了求解上述泊松方程，还需要边界条件。在固壁边界上，物理条件是法向速度为零，即 $\boldsymbol{n} \cdot \boldsymbol{u}^{n+1} = 0$。将速度修正公式代入此条件，可推导出 $\phi$ 的诺伊曼（Neumann）边界条件 [@problem_id:3408403]：
    $$
    \frac{\partial \phi}{\partial n} = \boldsymbol{n} \cdot \nabla \phi = \frac{1}{\Delta t} \boldsymbol{n} \cdot \boldsymbol{u}^*
    $$

4.  **速度与压力更新**：求解得到 $\phi$ 后，便可以完成速度和压力的更新：
    $$
    \boldsymbol{u}^{n+1} = \boldsymbol{u}^* - \Delta t \nabla \phi
    $$
    $$
    p^{n+1} = p^n + \phi
    $$
    通过这种构造，最终得到的速度场 $\boldsymbol{u}^{n+1}$ 在离散意义上是精确无散的，即 $D \boldsymbol{u}^{n+1} = 0$ [@problem_id:3408404]。

值得注意的是，纯诺伊曼边界条件的泊松问题存在一个**可解性条件（compatibility condition）** [@problem_id:3408389]。对方程 $\nabla^2 \phi = g$ 在全域积分并使用散度定理，可得 $\int_{\Omega} g \, dV = \int_{\partial\Omega} \frac{\partial \phi}{\partial n} \, dS$。这意味着源项的体积积分必须等于边界通量的面积分。在离散层面，这对应于压力泊松方程的系数矩阵是奇异的，其核空间为常数向量。因此，方程有解的条件是右端项向量与常数向量正交。这也意味着压力（或压力增量）的解是不唯一的，相差一个任意常数，必须通过施加额外约束（如指定某点压力值或要求全域平均值为零）来确定唯一解。

### 分裂误差与旋转压力修正格式

尽管IPCS在计算上颇具吸引力，但其引入的分裂误差限制了其精度。这种误差主要源于在暂估速度步中对压力梯度的近似处理，以及在修正步中对速度边界条件的近似满足。一个显著的后果是在固壁边界附近产生非物理性的**数值边界层（numerical boundary layer）**，导致压力和切向速度的精度下降。

为了缓解这一问题，**旋转压力修正格式（Rotational Pressure-Correction Scheme, RPCS）**应运而生 [@problem_id:3408467]。其核心思想是对动量方程中的粘性项进行更精细的处理。利用矢量恒等式，拉普拉斯算子可以分解为：
$$
- \nu \Delta \boldsymbol{u} = \nu \nabla \times (\nabla \times \boldsymbol{u}) - \nu \nabla(\nabla \cdot \boldsymbol{u})
$$
对于精确的不可压缩流，$\nabla \cdot \boldsymbol{u} = 0$，因此粘性项等价于其旋转部分 $\nu \nabla \times (\nabla \times \boldsymbol{u})$。然而，在暂估速度步，$\boldsymbol{u}^*$ 的散度通常不为零。RPCS的思想是，由 $\nabla \cdot \boldsymbol{u}^*$ 产生的 $-\nu \nabla(\nabla \cdot \boldsymbol{u}^*)$ 这一项是一个纯梯度场，其贡献可以被吸收到压力项中，而不是作为误差遗留下来。

通过对分裂格式的仔细推导，可以发现在IPCS的基础上，为了系统性地消除这一主要的分裂误差项，压力更新步骤需要进行修正。RPCS的压力更新公式为 [@problem_id:3408467]：
$$
p^{n+1}_{\mathrm{RPCS}} = p^n + \phi - \nu \nabla \cdot \boldsymbol{u}^*
$$
与IPCS的更新公式 $p^{n+1}_{\mathrm{IPCS}} = p^n + \phi$ 相比，RPCS增加了一个修正项 $-\nu \nabla \cdot \boldsymbol{u}^*$ [@problem_id:3408403]。这一项正比于暂估速度的散度，即对无散约束的违背程度。它有效地将粘性项中由于散度非零而产生的梯度部分从速度场转移到了压力场，从而提高了压力边界条件的精度，并减小了分裂误差。从约束优化的角度看，这个额外的修正项使得最终的解状态更接近于全耦合系统的KKT条件，从而减小了系统的残差 [@problem_id:3408466]。

尽管RPCS的压力更新公式有所不同，但其核心求解步骤仍然是求解一个关于 $\phi$ 的对称正定泊松方程，保留了压力修正法的主要计算优势 [@problem_id:3408455]。

### 数值分析的深层视角

最后，我们将压力修正法置于更广阔的数值分析框架下，探讨几个相关的深层概念。

#### 压力鲁棒性与Grad-Div稳定性

一个理想的不可压缩流求解器应该具有**压力鲁棒性（pressure-robustness）**，即其计算出的速度场不应受到任意无旋（irrotational）外力的影响。换言之，如果外力 $\boldsymbol{f}$ 是一个梯度场 $\nabla \psi$，那么精确解的速度应为零。然而，许多标准的数值方法（包括基于普通混合有限元的IPCS）不具备这一性质，会导致在纯梯度力作用下产生虚假的非零速度 [@problem_id:3408408]。

旋转压力修正格式通过修正压力更新，有效地消除了导致对梯度力敏感的主要分裂误差项，从而显著改善了压力鲁棒性。有趣的是，RPCS在代数上近似等价于在标准IPCS的动量方程中添加一个**Grad-Div稳定项** $\gamma \nabla(\nabla \cdot \boldsymbol{u})$，并取稳定化参数 $\gamma = \nu$ [@problem_id:3408462] [@problem_id:3408408]。这揭示了RPCS与现代稳定性增强技术之间的深刻联系。

#### LBB条件的角色

需要强调的是，压力修正法是一种**求解策略（solver strategy）**，它本身并不能修复空间离散格式的内在缺陷。有限元方法中，速度和压力空间的选取必须满足**Ladyzhenskaya–Babuška–Brezzi（LBB）条件**（或称inf-sup条件），才能保证离散鞍点问题的适定性。

如果选用的有限元空间对不满足LBB条件（例如，使用等阶次的P1-P1单元），那么即使采用压力修正法，离散压力泊松算子也会是奇异或病态的，导致压力场出现非物理的、棋盘状的伪振荡。因此，LBB条件的满足对于获得稳定、无伪振荡的压力解仍然是至关重要的，无论采用的是全耦合求解器还是压力修正求解器 [@problem_id:3408462] [@problem_id:3408455]。

#### 方法谱系

最后，值得一提的是，压力修正法是更广泛的**投影类方法**中的一个重要分支。在数值CFD的谱系中，还存在其他类型的分裂格式，如**速度修正法（velocity-correction schemes）**和**规范场方法（gauge methods）** [@problem_id:3408388]。这些方法在如何定义和求解用于投影的辅助变量上有所不同。例如，速度修正法将投影视为一个纯粹的运动学步骤，其辅助标量势与物理压力没有直接关系，物理压力需要通过额外的步骤恢复。规范场方法则引入一个辅助的规范场变量来解耦无散约束。理解这些不同方法的区别与联系，有助于我们更全面地把握求解不可压缩流问题的各种数值策略。