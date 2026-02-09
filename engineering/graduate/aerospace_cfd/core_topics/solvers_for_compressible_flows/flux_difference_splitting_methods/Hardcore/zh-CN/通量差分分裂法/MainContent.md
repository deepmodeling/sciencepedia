## 引言
在现代计算流体力学（CFD）领域，精确模拟包含激波、接触间断等复杂流动现象是航空航天工程设计的核心挑战。通量差分分裂（Flux-Difference Splitting, FDS）方法作为一类先进的迎风格式，为此提供了强大而物理意义明确的解决方案，已成为当代高保真CFD求解器的基石。

然而，如何稳定且高效地离散双曲守恒律方程中的对流通量，同时准确捕捉间断处的物理特性，是数值方法开发中的一个核心难题。传统的中心差分格式易产生非物理振荡，而简单的迎风格式则可能引入过多的数值耗散，模糊流动的精细结构。FDS方法旨在通过近似求解局部黎曼问题来克服这些困难，但其理论的深刻性和实践中的数值陷阱对初学者和研究人员构成了不小的挑战。

本文旨在为研究生及以上水平的读者提供一份关于FDS方法的全面指南。在接下来的内容中，我们将分三步系统地展开：第一章 **“原理与机制”** 将深入剖析FDS方法的核心思想，从其物理基准——Godunov方法和黎曼问题出发，详细阐述基于特征分解的通量分裂机制，并探讨其线性化带来的关键数值问题。第二章 **“应用与跨学科联系”** 将展示FDS如何从一维理论走向多维高阶的实际应用，如何与粘性、多物理场模型耦合，以及如何集成于自适应网格、隐式求解等先进计算框架中。最后，在第三章 **“动手实践”** 中，读者将通过具体的计算练习，将理论知识转化为解决实际问题的能力。

通过这一结构化的学习路径，本文将带领读者不仅理解FDS“是什么”，更掌握其“为什么”和“怎么用”，从而为进行前沿的CFD研究与开发打下坚实基础。让我们首先进入第一章，探索通量差分分裂方法的精妙原理与内在机制。

## 原理与机制

在计算流体力学 (CFD) 中，求解双曲守恒律方程组（如欧拉方程）的核心挑战在于如何精确且稳定地离散通量项的导数。有限体积法将这一挑战转化为在控制体单元的交界面上确定一个**数值通量 (numerical flux)**。通量差分分裂 (Flux-Difference Splitting, FDS) 方法为构造这种数值通量提供了一个强大且物理意义明确的框架。本章将深入探讨通量差分分裂的基本原理、数学机制及其在实践中遇到的关键问题。

### 黎曼问题与戈杜诺夫方法：物理基准

为求解形如 $\partial_t \boldsymbol{U} + \partial_x \boldsymbol{F}(\boldsymbol{U}) = 0$ 的一维双曲守恒律，有限体积法通过对控制体 $[x_{i-1/2}, x_{i+1/2}]$ 进行积分，得到单元平均值 $\boldsymbol{U}_i$ 的半离散更新格式 [@problem_id:3960559]：

$$
\frac{d\boldsymbol{U}_i}{dt} = -\frac{1}{\Delta x} \left( \hat{\boldsymbol{F}}_{i+1/2} - \hat{\boldsymbol{F}}_{i-1/2} \right)
$$

其中 $\hat{\boldsymbol{F}}_{i+1/2}$ 和 $\hat{\boldsymbol{F}}_{i-1/2}$ 分别是位于单元右侧和左侧交界面的数值通量。问题的核心便在于如何定义这个数值通量函数 $\hat{\boldsymbol{F}}(\boldsymbol{U}_L, \boldsymbol{U}_R)$，它依赖于交界面左右两侧的状态 $\boldsymbol{U}_L$ 和 $\boldsymbol{U}_R$。

一个具有深刻物理背景的方法是**戈杜诺夫 (Godunov) 方法**。该方法假设在每个时间步开始时，解在每个单元内是分片常数。因此，在任意两个相邻单元（例如，单元 $i$ 和 $i+1$）的交界面 $x_{i+1/2}$ 处，存在一个由状态 $\boldsymbol{U}_L = \boldsymbol{U}_i^n$ 和 $\boldsymbol{U}_R = \boldsymbol{U}_{i+1}^n$ 构成的间断。这个初始条件定义了一个经典的**黎曼问题 (Riemann problem)** [@problem_id:3960638]。黎曼问题的解是一组自相似的波系（由激波、稀疏波和接触间断组成），从初始间断位置传播开来。

戈杜诺夫方法利用这个精确的物理图像，将数值通量定义为黎曼问题精确解在交界面位置 $x/t=0$ 处的物理通量。由于解是自相似的，该位置的状态在时间上是恒定的（在波系不相互作用的时间内）。因此，戈杜诺夫通量为 $\hat{\boldsymbol{F}}_G = \boldsymbol{F}(\boldsymbol{U}(x/t=0))$。

戈杜诺夫方法因其直接利用了控制方程的物理特性而被视为迎风格式的“黄金标准”。然而，对于像欧拉方程这样的非线性系统，求解黎曼问题通常需要代价高昂的迭代过程，例如求解星区的压力和速度。考虑到在实际的航空航天 CFD 应用中，网格可能包含数百万甚至更多的交界面，在每个时间步的每个交界面上都执行迭代求解是难以承受的计算负担 [@problem_id:3960606]。这促使了近似黎曼求解器的发展，其中通量差分分裂方法是应用最广泛的一类。

### 通量差分分裂的核心思想：基于特征的分解

通量差分分裂 (FDS) 方法的宗旨是，在避免求解完整非线性黎曼问题的同时，尽可能地保留其关键的波结构信息。其核心思想是，交界面两侧的状态差 $\Delta \boldsymbol{U} = \boldsymbol{U}_R - \boldsymbol{U}_L$ 可以被分解为一系列在该物理系统中传播的**特征波 (characteristic waves)** 的线性叠加 [@problem_id:3960590]。

这种分解是借助通量雅可比矩阵 $\boldsymbol{A}(\boldsymbol{U}) = \partial \boldsymbol{F} / \partial \boldsymbol{U}$ 的**特征结构 (eigenstructure)** 实现的。对于双曲系统，雅可比矩阵 $\boldsymbol{A}$ 具有完备的实特征值 $\lambda_p$ 和对应的右特征向量 $\boldsymbol{r}_p$。这些特征向量构成了一个状态空间的基。因此，状态跳跃 $\Delta \boldsymbol{U}$ 可以唯一地表示为：

$$
\Delta \boldsymbol{U} = \sum_p \alpha_p \boldsymbol{r}_p
$$

其中，系数 $\alpha_p$ 被称为**波强度 (wave strengths)**，它表示状态差 $\Delta \boldsymbol{U}$ 在第 $p$ 个特征方向上的投影。如果 $\boldsymbol{R}$ 是由右特征向量 $\boldsymbol{r}_p$ 作为列向量构成的矩阵，那么波强度向量 $\boldsymbol{\alpha}$ 可以通过 $\boldsymbol{\alpha} = \boldsymbol{R}^{-1} \Delta \boldsymbol{U}$ 计算得到。

通过对状态差进行特征分解，通量差 $\Delta \boldsymbol{F} = \boldsymbol{F}(\boldsymbol{U}_R) - \boldsymbol{F}(\boldsymbol{U}_L)$ 也可以相应地被“分裂”。通过近似线性化（下文将详细介绍），我们有 $\Delta \boldsymbol{F} \approx \boldsymbol{A} \Delta \boldsymbol{U}$。利用特征分解 $\boldsymbol{A} = \boldsymbol{R} \boldsymbol{\Lambda} \boldsymbol{R}^{-1}$（其中 $\boldsymbol{\Lambda}$ 是由特征值 $\lambda_p$ 构成的对角矩阵），我们得到：

$$
\Delta \boldsymbol{F} \approx \boldsymbol{A} \left( \sum_p \alpha_p \boldsymbol{r}_p \right) = \sum_p \alpha_p (\boldsymbol{A} \boldsymbol{r}_p) = \sum_p \alpha_p \lambda_p \boldsymbol{r}_p
$$

这个表达式是 FDS 的核心：它将总的通量差分解为一系列贡献项，每一项 $\alpha_p \lambda_p \boldsymbol{r}_p$ 都与一个以速度 $\lambda_p$ 传播、强度为 $\alpha_p$、结构为 $\boldsymbol{r}_p$ 的特征波相对应。通过判断每个特征值 $\lambda_p$ 的符号，我们就能知道信息是从左向右传播（$\lambda_p > 0$）还是从右向左传播（$\lambda_p  0$），从而构造出能够正确反映信息传播方向的**迎风 (upwind)** 数值通量。

### 欧拉方程的特征结构

为了将上述抽象原理具体化，我们考察一维欧拉方程。其守恒变量为 $\boldsymbol{U} = [\rho, \rho u, E]^T$，物理通量为 $\boldsymbol{F}(\boldsymbol{U}) = [\rho u, \rho u^2 + p, u(E + p)]^T$ [@problem_id:3960559]。通过对该系统进行线性化分析，可以推导出其通量雅可比矩阵 $\boldsymbol{A}(\boldsymbol{U})$ 的特征值和特征向量 [@problem_id:3960604]。

雅可比矩阵 $\boldsymbol{A}(\boldsymbol{U})$ 具有三个不同的实特征值：

$$
\lambda_1 = u - a, \quad \lambda_2 = u, \quad \lambda_3 = u + a
$$

其中 $u$ 是流体速度，$a = \sqrt{\gamma p / \rho}$ 是声速。这三个特征值代表了系统中三种不同波的传播速度：
*   $\lambda_1 = u - a$ 和 $\lambda_3 = u + a$ 对应**声波 (acoustic waves)**，它们以相对于流体以声速 $a$ 向下游和上游传播。
*   $\lambda_2 = u$ 对应**接触间断 (contact discontinuity)**（或熵波），它以流体自身的速度传播。

与这些特征值相对应的（一组常用的）右特征向量为：

$$
\boldsymbol{r}_1 = \begin{pmatrix} 1 \\ u - a \\ H - ua \end{pmatrix}, \quad 
\boldsymbol{r}_2 = \begin{pmatrix} 1 \\ u \\ \frac{1}{2}u^2 \end{pmatrix}, \quad 
\boldsymbol{r}_3 = \begin{pmatrix} 1 \\ u + a \\ H + ua \end{pmatrix}
$$

其中 $H = (E+p)/\rho$ 是比总焓。这些特征向量描述了每种波所携带的扰动结构。例如，$\boldsymbol{r}_2$ 对应速度和压力的扰动为零，只有密度的扰动，这正是接触间断的物理特性。

在数值格式中，最大的特征波速决定了信息传播的最大速度，从而制约了稳定的时间步长（CFL 条件）。这个速度由雅可比矩阵的**谱半径 (spectral radius)** 给出，即 $\rho(\boldsymbol{A}) = \max_k |\lambda_k| = |u| + a$。例如，对于一个给定的状态 $\rho = 1.0 \, \mathrm{kg/m^3}$, $u = 250.0 \, \mathrm{m/s}$, $p = 1.0 \times 10^5 \, \mathrm{Pa}$, 和 $\gamma = 1.4$，我们可以计算出声速 $a \approx 374.2 \, \mathrm{m/s}$。因此，三个特征速度分别为 $\lambda_1 \approx -124.2 \, \mathrm{m/s}$, $\lambda_2 = 250.0 \, \mathrm{m/s}$, $\lambda_3 \approx 624.2 \, \mathrm{m/s}$。该状态下的谱半径为 $\max(|\lambda_1|, |\lambda_2|, |\lambda_3|) \approx 624.2 \, \mathrm{m/s}$ [@problem_id:3960604]。

### Roe 近似黎曼求解器

直接使用局部状态（如 $\boldsymbol{U}_L$ 或 $\boldsymbol{U}_R$）的特征结构来分解 $\Delta \boldsymbol{U}$ 会引入不一致性。**Roe 近似黎曼求解器**通过引入一个精心构造的**Roe 平均矩阵 (Roe-averaged matrix)** $\tilde{\boldsymbol{A}}$ 解决了这个问题。这个矩阵 $\tilde{\boldsymbol{A}}(\boldsymbol{U}_L, \boldsymbol{U}_R)$ 被构造成一个常数矩阵，但它精确地满足关系式：

$$
\boldsymbol{F}(\boldsymbol{U}_R) - \boldsymbol{F}(\boldsymbol{U}_L) = \tilde{\boldsymbol{A}} (\boldsymbol{U}_R - \boldsymbol{U}_L)
$$

这个性质被称为 Roe 的 Property U，它保证了对于单个激波，该线性化模型能够给出与非线性系统完全一致的跳跃关系。对于理想气体欧拉方程，可以推导出 Roe 平均状态（如 Roe 平均密度 $\tilde{\rho} = \sqrt{\rho_L \rho_R}$ 等）的显式表达式，从而构造出 $\tilde{\boldsymbol{A}}$。

有了这个线性化关系，数值通量可以被构建为一个中心通量项加上一个起耗散作用的迎风修正项：

$$
\hat{\boldsymbol{F}}_{\text{Roe}} = \frac{1}{2}\left[\boldsymbol{F}(\boldsymbol{U}_L) + \boldsymbol{F}(\boldsymbol{U}_R)\right] - \frac{1}{2}|\tilde{\boldsymbol{A}}|(\boldsymbol{U}_R - \boldsymbol{U}_L)
$$

这里的 $|\tilde{\boldsymbol{A}}|$ 是矩阵的“绝对值”，定义为 $|\tilde{\boldsymbol{A}}| = \tilde{\boldsymbol{R}} |\tilde{\boldsymbol{\Lambda}}| \tilde{\boldsymbol{R}}^{-1}$，其中 $|\tilde{\boldsymbol{\Lambda}}|$ 是由 Roe 平均特征值 $\tilde{\lambda}_k$ 的绝对值 $| \tilde{\lambda}_k |$ 构成的对角矩阵。耗散项 $-\frac{1}{2}|\tilde{\boldsymbol{A}}|(\boldsymbol{U}_R - \boldsymbol{U}_L)$ 确保了对于每个特征波，都施加了与其传播方向相适应的数值黏性，从而稳定了计算并实现了迎风效果。

### 与通量矢量分裂 (FVS) 的对比

为了更好地理解 FDS 的本质，有必要将其与另一大类迎风格式——**通量矢量分裂 (Flux-Vector Splitting, FVS)**——进行对比 [@problem_id:3960625]。

*   **通量差分分裂 (FDS)** 的核心是**分裂状态差** $\Delta \boldsymbol{U}$。它着眼于交界面上的**波的相互作用**，通过一个（平均的）雅可比矩阵的特征结构来近似黎曼问题的解。

*   **通量矢量分裂 (FVS)** 的核心是**分裂通量矢量本身** $\boldsymbol{F}(\boldsymbol{U})$。它将物理通量 $\boldsymbol{F}$ 分解为与正特征值相关的部分 $\boldsymbol{F}^+$（代表信息向右传播）和与负特征值相关的部分 $\boldsymbol{F}^-$（代表信息向左传播）。分裂过程在交界面的左右两个状态上分别独立进行。数值通量则由左侧状态的右行通量和右侧状态的左行通量组合而成：$\hat{\boldsymbol{F}}_{\text{FVS}} = \boldsymbol{F}^+(\boldsymbol{U}_L) + \boldsymbol{F}^-(\boldsymbol{U}_R)$。

这两种方法的哲学差异导致了它们性能上的显著不同。一个典型的例子是对接触间断的解析能力 [@problem_id:3960593]。接触间断的物理特性是压力和速度连续，而密度有跳跃。它由线性退化的特征场 $\lambda_2=u$ 承载。高质量的 FDS 格式（如 Roe 格式）能够识别出这种纯接触间断只涉及一个特征场，并且不会在该场上施加不必要的数值耗散，因此能够非常尖锐地（在某些情况下是精确地）捕捉接触间断。相比之下，FVS 格式由于其分裂机制，通常会在所有特征场上都引入数值耗散，包括线性退化的接触场。这导致 FVS 格式在计算中会严重地模糊和耗散接触间断和剪切层。

### 线性化求解器的缺陷及其修正

尽管 Roe 格式等 FDS 方法因其高分辨率和物理保真度而备受推崇，但其线性化的本质也带来了一些严重的数值缺陷（或称“病态”），在研究生级别的学习和研究中必须予以重视。

#### 熵增条件的违背与熵修正

物理上，流体穿过激波时熵必须增加，而穿过稀疏波时熵应保持不变。这构成了双曲守恒律弱解的**熵增条件 (entropy condition)**。然而，标准的 Roe 格式在某些情况下会产生违反熵增条件的解 [@problem_id:3960624]。

这个问题最常出现在**跨音速稀疏波 (transonic rarefaction)** 中，即流场从亚音速平滑过渡到超音速。在这种情况下，某个特征值（例如 $\lambda_1 = u-a$）会平滑地从负值变为正值，必然会穿过零点。Roe 格式的线性化模型无法分辨这种平滑过渡，它只看到一个特征值符号发生变化的间断。当 Roe 平均特征值 $\tilde{\lambda}_k$ 恰好接近零时，数值耗散项 $| \tilde{\lambda}_k |$ 也趋于零。耗散的缺失使得格式允许一个不符合物理规律的、熵减的固定激波——即**膨胀激波 (expansion shock)**——的形成 [@problem_id:3960537]。

为了解决这个问题，必须引入**熵修正 (entropy fix)**。其思想是确保即使在特征速度接近零时，数值耗散也不会完全消失。一种常用的方法（如 Harten-Hyman 熵修正）是修改绝对值函数，例如，当 $|\lambda_k|  \delta$（$\delta$ 是一个小阈值）时，用一个平滑的正函数（如 $(\lambda_k^2 + \delta^2)/(2\delta)$）来代替 $|\lambda_k|$。这人为地在声速点附近增加了少量数值黏性，足以将稀疏波铺展在几个网格单元上，从而阻止了膨胀激波的形成。

#### 正定性的违背

另一个关键问题是**正定性保持 (positivity preservation)** [@problem_id:3960596]。物理上，密度 $\rho$ 和压力 $p$ 必须始终为正。一个数值格式如果能保证在初始状态为正定的情况下，后续所有时间步的计算结果也保持正定，则称其为保正定的。

对于一阶格式，一个保证正定性的充分条件是，在满足某个 CFL 时间步长限制下，更新后的状态可以表示为若干个物理允许状态的凸组合。像 HLL（Harten-Lax-van Leer）这类更具鲁棒性的格式，通过构造保证包含所有物理波速的信号速度，可以满足这个条件，因此是天然保正定的。

然而，标准的 Roe 格式不具备这个性质。尤其是在强稀疏波或接近真空的情况下，其线性化模型所提供的耗散可能不足以将更新后的状态限制在物理允许的凸集内。这可能导致计算出的新状态出现负密度或负压力，造成计算的崩溃。因此，开发保正定的 Roe 类型格式是 CFD 领域一个活跃的研究方向。

#### 多维问题：附体激波现象

当将基于一维黎曼问题构建的 FDS 格式应用于多维问题时，可能会出现新的数值不稳定现象，其中最著名的就是**附体激波现象 (carbuncle phenomenon)** [@problem_id:3960530]。

这种非物理不稳定性通常出现在高马赫数绕钝头体流动中，当弓形激波与计算网格近乎对齐时。其表现为激波阵面上出现奇怪的凸起或扭结。其根源在于 Roe 格式的耗散机制是纯粹一维的。对于一个与网格对齐的激波，沿激波切向（即垂直于法向）的数值通量计算中，法向速度 $u_n$ 接近于零。由于对应于剪切波和熵波的耗散正比于 $|u_n|$，这导致在激波切向上的数值耗散几乎为零。这种耗散的缺失使得切向的数值扰动（特别是奇偶解耦模式）无法被抑制，从而发展成宏观的、非物理的“附体激波”。

解决这个问题需要引入真正的多维耗散机制。例如，使用本身耗散性更强的格式（如 HLL），或者设计能够感知激波方向并施加额外切向耗散的修正项。这表明，虽然一维 FDS 原理是基础，但在多维复杂流动中，必须谨慎处理其局限性。