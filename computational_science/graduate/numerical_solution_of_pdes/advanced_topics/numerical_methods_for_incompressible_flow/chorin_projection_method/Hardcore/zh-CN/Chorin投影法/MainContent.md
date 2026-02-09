## 引言
在计算流体力学（CFD）领域，对不可压缩流动的精确模拟是一项基础而又充满挑战的任务。其核心困难在于不可压缩Navier-Stokes方程中压力与速度之间的瞬时耦合关系，这在数学上形成了一个难以直接求解的微分-代数鞍点问题。为了规避这一难题，Alexandre Chorin于20世纪60年代提出了一种革命性的数值方法——投影法。该方法通过巧妙的算子分裂思想，将求解过程分解为一系列更简单、更易于处理的步骤，极大地提高了计算效率，并成为此后数十年CFD领域最重要的算法基石之一。

本文旨在为读者提供一个关于Chorin投影法的全面而深入的理解。我们将带领您穿越该方法的三个核心层面：
- 在“原理与机制”一章中，我们将从压力-速度耦合的挑战出发，详细阐释算子分裂策略和作为其理论支柱的亥姆霍兹-霍奇分解，并推导其核心算法流程与误差来源。
- 在“应用与跨学科联系”一章中，我们将展示该方法如何从理论走向实践，探讨其在不同离散化方案、复杂物理现象（如多相流、非牛顿流）和高性能计算中的应用与演进，并揭示其与地球物理、电磁学等领域的深刻联系。
- 最后，在“动手实践”部分，我们设计了一系列编程练习，旨在通过代码实现，加深您对离散算子、迭代求解和网格效应等关键概念的理解。

通过本次学习，您将不仅掌握Chorin投影法的基本原理，更能领会其作为一种通用计算框架的强大威力与灵活性。

## 原理与机制

本章深入探讨了Chorin投影法的核心原理与机制。我们将从不可压缩流动的基本挑战——压力-速度耦合——出发，揭示该方法如何通过算子分裂策略巧妙地解耦这一难题。我们将详细阐述作为其理论基石的亥姆霍兹-霍奇分解（Helmholtz-Hodge decomposition），并由此推导出投影法的具体算法步骤。此外，本章还将分析该方法的误差来源，并介绍旨在提高其精度与稳定性的重要改进。

### 不可压缩性的挑战：压力-速度耦合

不可压缩流动的控制方程——不可压缩Navier-Stokes方程——由动量守恒和质量守恒（即不可压缩性约束）两部分组成。对于一个密度为常数 $\rho$、运动粘度为 $\nu$ 的牛顿流体，其方程组可写为：

$$
\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u}\cdot\nabla)\mathbf{u} = -\frac{1}{\rho}\nabla p + \nu \nabla^2 \mathbf{u} + \mathbf{f}
$$

$$
\nabla\cdot\mathbf{u} = 0
$$

其中 $\mathbf{u}$ 是速度场，$p$ 是压力场，$\mathbf{f}$ 是单位质量的体积力。

这组方程的求解面临一个独特的挑战：压力 $p$ 的角色。与可压缩流不同，不可压缩流体中的压力并非由状态方程（如理想气体定律）决定的热力学变量。相反，它是一个力学变量，其瞬时调整是为了确保速度场在任何时刻都满足**不可压缩性约束** $\nabla\cdot\mathbf{u} = 0$。从数学上看，压力 $p$ 充当了一个**拉格朗日乘子**（Lagrange multiplier），其梯度 $\nabla p$ 是一个约束力，将速度场“强制”保持在无散度（divergence-free）的函数子空间内 [@problem_id:3301180]。

这种耦合特性使得方程组成为一个微分-代数系统，直接求解（即**整体式方法**或monolithic method）通常会导致一个大型的、耦合的**鞍点问题**（saddle-point problem）。在离散形式下，这表现为一个块状矩阵系统 [@problem_id:3371146]：

$$
\begin{pmatrix}
\mathbf{A} & \mathbf{G} \\
\mathbf{D} & \mathbf{0}
\end{pmatrix}
\begin{pmatrix}
\mathbf{U} \\
\mathbf{P}
\end{pmatrix}
=
\begin{pmatrix}
\mathbf{F} \\
\mathbf{0}
\end{pmatrix}
$$

其中 $\mathbf{A}$ 代表动量输运的离散算子，$\mathbf{G}$ 和 $\mathbf{D}$ 分别代表离散的梯度和散度算子，而 $\mathbf{U}$ 和 $\mathbf{P}$ 是速度和压力的未知系数向量。这个系统的矩阵是非正定的，求解起来非常困难。此外，为了保证离散系统的稳定性和解的唯一性，速度和压力的离散函数空间必须满足严格的兼容性条件，即**Ladyzhenskaya–Babuška–Brezzi (LBB) inf-sup 条件**。

Chorin投影法及其变种的提出，其核心动机正是为了规避直接求解这个复杂的鞍点问题。

### 算子分裂策略：解耦压力与速度

投影法的核心思想是**算子分裂**（operator splitting），也称为**分数步法**（fractional-step method）。它将一个复杂的时间步推进过程分解为一系列更简单、更易于求解的子步骤。对于Navier-Stokes方程，投影法将动量方程中的压力梯度项与其他项（对流、扩散、外力）分离开来。一个典型的时间步（从 $t^n$ 到 $t^{n+1}$）被分为两个主要阶段：

1.  **预测步 (Prediction Step)**：首先，计算一个不包含压力梯度项的动量方程，从而得到一个“中间速度”或“预测速度” $\mathbf{u}^\star$。这一步主要处理流体的对流和扩散过程。由于忽略了压力梯度这个约束力，得到的 $\mathbf{u}^\star$ 通常不满足不可压缩性约束，即 $\nabla \cdot \mathbf{u}^\star \neq 0$。

2.  **投影步 (Projection Step)**：接着，将预测速度 $\mathbf{u}^\star$ “投影”到无散度的函数空间上，得到满足不可压缩性约束的最终速度 $\mathbf{u}^{n+1}$。这个投影是通过引入一个标量势（与压力相关）的梯度来实现的，它会减去 $\mathbf{u}^\star$ 中的“可压缩”部分。

通过这种分裂，原本耦合的压力-速度系统被解耦为两个相对独立的子问题：一个关于速度的（通常是类热传导或对流-扩散）问题，和一个关于压力的（通常是泊松）问题。这大大简化了每个时间步的计算。

### 数学基础：亥姆霍兹-霍奇分解

投影步的数学合法性来源于一个深刻的矢量分析定理——**亥姆霍兹-霍奇分解**（Helmholtz-Hodge decomposition），或称为**勒雷分解**（Leray decomposition）。该定理指出，在合适的边界条件下，任何一个矢量场 $\mathbf{w}$ 都可以唯一地分解为一个无散度（螺线管）部分 $\mathbf{v}$ 和一个无旋（梯度）部分 $\nabla\phi$ 的和 [@problem_id:3301199]：

$$
\mathbf{w} = \mathbf{v} + \nabla\phi, \quad \text{其中} \quad \nabla \cdot \mathbf{v} = 0
$$

这两个分量在 $L^2$ 内积意义下是正交的。在流体力学中，这对应于将一个任意流场分解为一个满足不可压缩性的物理流场和一个非物理的势流场。

投影法的核心正是利用了这个分解。预测速度 $\mathbf{u}^\star$ 扮演了任意矢量场 $\mathbf{w}$ 的角色。我们的目标是找到它的无散度部分，即最终的速度场 $\mathbf{u}^{n+1}$。根据分解，我们有：

$$
\mathbf{u}^{n+1} = \mathbf{u}^\star - \nabla\phi
$$

其中 $\mathbf{u}^{n+1}$ 就是我们想要的无散度速度场 $\mathbf{v}$。为了求出这个修正项 $\nabla\phi$，我们对上式两边取散度：

$$
\nabla \cdot \mathbf{u}^{n+1} = \nabla \cdot \mathbf{u}^\star - \nabla \cdot (\nabla\phi)
$$

由于我们强制要求最终速度是无散度的，即 $\nabla \cdot \mathbf{u}^{n+1} = 0$，并利用矢量恒等式 $\nabla \cdot (\nabla\phi) = \nabla^2\phi = \Delta\phi$，我们得到了一个关于标量势 $\phi$ 的**泊松方程**（Poisson equation）[@problem_id:3353835]：

$$
\Delta\phi = \nabla \cdot \mathbf{u}^\star
$$

一旦解出 $\phi$，就可以通过修正步骤 $\mathbf{u}^{n+1} = \mathbf{u}^\star - \nabla\phi$ 得到最终的无散度速度场。这清晰地表明，预测速度的散度 $\nabla \cdot \mathbf{u}^\star$ 成为了驱动压力修正的源项。

### 核心算法：一阶投影法

现在我们可以整合上述思想，构建一个具体的一阶非增量式投影法算法 [@problem_id:3301193] [@problem_id:3371178]。

**第一步：预测速度求解**

在时间步 $\Delta t$ 内，我们首先求解一个不含压力项的动量方程来获得中间速度 $\mathbf{u}^\star$。使用显式欧拉格式处理对流和扩散项，该方程的离散形式为：

$$
\frac{\mathbf{u}^\star - \mathbf{u}^n}{\Delta t} = -(\mathbf{u}^n \cdot \nabla)\mathbf{u}^n + \nu \nabla^2 \mathbf{u}^n + \mathbf{f}^n
$$

整理后得到 $\mathbf{u}^\star$ 的表达式：

$$
\mathbf{u}^\star = \mathbf{u}^n + \Delta t \left[ -(\mathbf{u}^n \cdot \nabla)\mathbf{u}^n + \nu \nabla^2 \mathbf{u}^n + \mathbf{f}^n \right]
$$

**第二步：压力泊松方程求解**

接下来，我们建立并求解一个关于压力 $p^{n+1}$ 的泊松方程。将亥姆霍兹分解中的标量势 $\phi$ 与物理压力 $p^{n+1}$ 联系起来。修正步骤可以写作：

$$
\frac{\mathbf{u}^{n+1} - \mathbf{u}^\star}{\Delta t} = -\frac{1}{\rho}\nabla p^{n+1}
$$

这表明 $\nabla\phi$ 实际上就是 $\frac{\Delta t}{\rho}\nabla p^{n+1}$。因此，我们之前为 $\phi$ 推导的泊松方程可以改写为关于 $p^{n+1}$ 的方程：

$$
\Delta \left( \frac{\Delta t}{\rho}p^{n+1} \right) = \nabla \cdot \mathbf{u}^\star
$$

由于 $\Delta t$ 和 $\rho$ 是常数，我们得到经典的**压力泊松方程 (PPE)**:

$$
\Delta p^{n+1} = \frac{\rho}{\Delta t} \nabla \cdot \mathbf{u}^\star
$$

**第三步：速度修正**

一旦求解PPE得到压力场 $p^{n+1}$，我们就可以用它来修正中间速度，得到最终的、满足不可压缩性约束的速度场 $\mathbf{u}^{n+1}$：

$$
\mathbf{u}^{n+1} = \mathbf{u}^\star - \frac{\Delta t}{\rho} \nabla p^{n+1}
$$

这个三步流程——预测、求解PPE、修正——构成了Chorin投影法的核心循环。它成功地将一个复杂的耦合问题分解为两个更易处理的子问题：一个速度预测问题和一个标量泊松问题。

### 投影算子的性质

投影法的名称来源于其第二步的数学本质。我们可以定义一个算子 $\mathbb{P}$，它将任意矢量场 $\mathbf{w}$ 映射到其无散度分量上。根据亥姆霍兹-霍奇分解，这个操作等价于从原场中减去其梯度分量。

$$
\mathbb{P}(\mathbf{w}) = \mathbf{w} - \nabla\phi = \mathbf{w} - \nabla(\Delta^{-1}(\nabla \cdot \mathbf{w}))
$$

其中 $\Delta^{-1}$ 表示泊松方程的求解算子。在周期性边界条件下，这个算子在傅里叶空间中具有非常清晰的形式 [@problem_id:3301181]。对于任意一个波数向量 $\mathbf{k}$，一个矢量场 $\hat{\mathbf{u}}(\mathbf{k})$ 的梯度分量（非螺线管部分）是其在 $\mathbf{k}$ 方向上的投影，而无散度分量（螺线管部分）是其在与 $\mathbf{k}$ 正交的平面上的投影。傅里叶空间中的投影算子 $P(\mathbf{k})$ 是一个矩阵：

$$
P(\mathbf{k}) = I - \frac{\mathbf{k}\mathbf{k}^T}{|\mathbf{k}|^2} \quad (\text{for } \mathbf{k} \neq \mathbf{0})
$$

其中 $I$ 是单位矩阵。这个算子具有一个真正投影算子应有的所有性质：

*   **对称性 (Symmetry)**: $P(\mathbf{k})^T = P(\mathbf{k})$。
*   **幂等性 (Idempotence)**: $P(\mathbf{k})^2 = P(\mathbf{k})$。这意味着一次投影之后，再次投影不会改变结果。

其本征分析也揭示了其几何作用：它有一个本征值为 0，对应的本征向量是 $\mathbf{k}$ 本身，这意味着它会“消除”速度场沿波数向量方向的分量（即梯度部分）。其余的 $d-1$ 个本征值均为 1，对应的本征向量与 $\mathbf{k}$ 正交，这意味着它会“保留”速度场中与波数向量正交的分量（即无散度部分）。这为“投影”一词提供了坚实的数学和几何解释。

### 压力泊松方程的求解

求解压力泊松方程是投影法的关键步骤，其适定性（well-posedness）需要特别注意 [@problem_id:3371189]。

首先是**边界条件**。在周期性域中，压力也满足周期性边界条件。在有固壁的区域，压力的边界条件必须从速度的边界条件中推导出来。例如，如果最终速度 $\mathbf{u}^{n+1}$ 在边界 $\partial\Omega$ 上满足无穿透条件 $\mathbf{n} \cdot \mathbf{u}^{n+1} = 0$（$\mathbf{n}$ 为边界外法线），我们可以对速度修正方程 $\mathbf{u}^{n+1} = \mathbf{u}^\star - \frac{\Delta t}{\rho}\nabla p^{n+1}$ 两边点乘 $\mathbf{n}$：

$$
\mathbf{n} \cdot \mathbf{u}^{n+1} = \mathbf{n} \cdot \mathbf{u}^\star - \frac{\Delta t}{\rho} \mathbf{n} \cdot \nabla p^{n+1}
$$

将 $\mathbf{n} \cdot \mathbf{u}^{n+1} = 0$ 和 $\mathbf{n} \cdot \nabla p^{n+1} = \frac{\partial p^{n+1}}{\partial n}$ 代入，我们得到压力的**诺伊曼边界条件 (Neumann boundary condition)**：

$$
\frac{\partial p^{n+1}}{\partial n} = \frac{\rho}{\Delta t} \mathbf{n} \cdot \mathbf{u}^\star
$$

这个边界条件确保了修正后的速度场在边界上是无穿透的 [@problem_id:3353835]。

其次是**解的存在性和唯一性**。对于一个全诺伊曼或全周期性边界条件的泊松问题 $\Delta p = f$，其解存在一个**零空间**（null space），即常数函数。因为 $\Delta(p+C) = \Delta p$ 对任意常数 $C$ 成立。这意味着压力的解只能确定到一个任意常数，这与物理现实相符（在不可压缩流中只有压力梯度才有意义）。为了得到唯一解，通常会施加一个额外的约束，例如令域内压力的平均值为零，即 $\int_\Omega p \,d\Omega = 0$。

此外，这类问题有解的前提是其源项必须满足一个**相容性条件**（compatibility condition）。通过对泊松方程在全域积分并使用散度定理，可以得到：

$$
\int_\Omega \Delta p^{n+1} \,d\Omega = \int_{\partial\Omega} \frac{\partial p^{n+1}}{\partial n} \,dS = \int_\Omega \frac{\rho}{\Delta t} \nabla \cdot \mathbf{u}^\star \,d\Omega = \frac{\rho}{\Delta t} \int_{\partial\Omega} \mathbf{n} \cdot \mathbf{u}^\star \,dS
$$

结合我们推导出的诺伊曼边界条件，可以发现这个条件是自动满足的。对于周期性边界或无滑移壁（$\mathbf{u}^\star \cdot \mathbf{n} = 0$），该条件简化为源项的积分为零，即 $\int_\Omega \nabla \cdot \mathbf{u}^\star \,d\Omega = 0$。

### 误差分析与方法改进

尽管投影法在计算上十分高效，但其基本形式存在一些固有的精度问题，主要源于算子分裂和边界条件的处理。

#### 分裂误差与压力精度

将压力项从动量方程中分裂出来，会引入一个**分裂误差**（splitting error）。在最基本的非增量式投影法中，由于在预测步完全忽略了压力，或使用了前一时刻的压力 $\nabla p^n$，这导致数值压力 $p^{n+1}$ 与真实压力 $p(t^{n+1})$ 之间存在一个量级为 $\mathcal{O}(\Delta t)$ 的误差。因此，尽管速度场可能达到更高阶的精度，压力场的精度通常只有一阶 [@problem_id:3301238]。这种误差是通过泊松方程的非局部性（椭圆性）传播到整个计算域的。

#### 边界层误差

一个更严重的问题发生在固壁边界附近。如前所述，为了保证最终速度的无穿透性，我们推导出了一个关于压力的诺伊曼边界条件。然而，这个边界条件（即使是更简单的 $\frac{\partial p}{\partial n} = 0$）通常与从完整Navier-Stokes方程在边界上直接推导出的真实压力边界条件不符 [@problem_id:3371150]。真实的压力法向梯度应该平衡粘性应力和外力，即 $\frac{\partial p}{\partial n} = \mathbf{n} \cdot (\mu \Delta \mathbf{u} + \mathbf{f})$。

这种数值边界条件与物理边界条件的不一致，会在靠近壁面的地方产生一个厚度约为 $\mathcal{O}(\sqrt{\nu\Delta t})$ 的**数值边界层**，层内的压力和速度解的精度会显著下降，甚至降到零阶 [@problem_id:3301238]。

#### 改进方法：增量式压力修正格式

为了克服这些精度问题，研究者们提出了多种改进方案，其中最著名的是**增量式压力修正**（incremental pressure-correction）格式 [@problem_id:3371137]。这类方法的核心思想是：

1.  在**预测步**中包含上一时刻的压力梯度 $\nabla p^n$。这使得预测速度 $\mathbf{u}^\star$ 是对动量方程更完整的近似。
    $$
    \frac{\mathbf{u}^\star - \mathbf{u}^n}{\Delta t} = -(\mathbf{u}^n \cdot \nabla)\mathbf{u}^n + \nu \nabla^2 \mathbf{u}^n - \frac{1}{\rho}\nabla p^n + \mathbf{f}^n
    $$

2.  求解一个关于**压力增量** $\phi = p^{n+1} - p^n$ 的泊松方程。
    $$
    \Delta \phi = \frac{\rho}{\Delta t} \nabla \cdot \mathbf{u}^\star
    $$

3.  在**修正步**中，不仅更新速度，还要对压力进行更精确的更新。一个简单更新是 $p^{n+1} = p^n + \phi$。然而，为了进一步减小分裂误差，特别是与粘性项相关的误差，可以使用所谓的“旋转形式”压力更新：
    $$
    p^{n+1} = p^n + \phi - \nu \nabla \cdot \mathbf{u}^\star
    $$
    这里的额外项 $-\nu \nabla \cdot \mathbf{u}^\star$ (或 $-\mu/\rho \nabla \cdot \mathbf{u}^\star$) 有助于补偿因分裂带来的误差，显著改善压力场的精度。

对于边界层误差问题，最根本的解决方案是使用**一致性压力边界条件**（consistent pressure boundary condition），即在求解压力泊松方程时，直接施加从动量方程推导出的物理边界条件 $\frac{\partial p}{\partial n} = \mathbf{n} \cdot (\mu \Delta \mathbf{u} + \mathbf{f})$ 的离散近似形式 [@problem_id:3371150]。这虽然增加了实现的复杂性，但能有效地消除数值边界层，将壁面附近的解恢复到应有的精度阶。

总而言之，Chorin投影法通过巧妙的算子分裂，将复杂的不可压缩流问题转化为一系列更易处理的步骤，极大地提高了计算效率。然而，使用者必须清醒地认识到其基本形式存在的精度缺陷，并根据具体应用的需求，选择合适的增量式格式或边界条件修正来确保计算结果的准确性。