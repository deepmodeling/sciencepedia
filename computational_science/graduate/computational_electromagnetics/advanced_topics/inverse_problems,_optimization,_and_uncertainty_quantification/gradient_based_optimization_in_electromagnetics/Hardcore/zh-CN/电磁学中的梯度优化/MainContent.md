## 引言
电磁学[逆向设计](@entry_id:158030)旨在自动发现满足特定性能指标的新型器件结构，已成为推动[光子](@entry_id:145192)学、天线工程和超构材料发展的关键引擎。[基于梯度的优化](@entry_id:169228)算法是实现这一目标的强大工具，它能高效地在高维设计空间中搜索最优解。然而，当设计参数多达数百万时，如何以可承受的计算成本精确获得目标函数相对于每个参数的梯度，便成为一个根本性的挑战，传统的有限差分或直接[微分](@entry_id:158718)方法在此类问题面前均显无力。

本文系统性地阐述了解决这一挑战的核心技术——伴随法。通过本文的学习，您将掌握大规模电磁优化的基本原理和前沿应用。

*   在“原理与机制”一章中，我们将从第一性原理出发，详细推导伴随方程，阐明其如何以与参数数量无关的计算成本解决梯度计算难题，并探讨其在不同物理模型和高级优化场景下的实现机制。
*   在“应用与跨学科连接”一章中，我们将展示伴随法在[隐身技术](@entry_id:264201)、超构表面设计、[光子](@entry_id:145192)器件[拓扑优化](@entry_id:147162)以及多物理场耦合问题等前沿领域的具体应用，彰显其作为统一设计框架的强大能力。
*   最后，在“动手实践”部分，您将通过具体的编程练习，亲手实现和验证伴随法，将理论知识转化为解决实际问题的能力。

现在，让我们首先深入其核心，探究梯度优化背后的基本原理与精妙机制。

## 原理与机制

在电磁学[逆向设计](@entry_id:158030)与优化领域，我们的目标是寻找一种材料[分布](@entry_id:182848)或激励源，以使某个性能指标（[目标函数](@entry_id:267263)）达到最优。这些问题通常可以被表述为一个由[偏微分方程](@entry_id:141332)（PDE）约束的[优化问题](@entry_id:266749)。[基于梯度的优化](@entry_id:169228)算法，如梯度下降法或其变种，是解决此类问题的强大工具。然而，这些算法的一个核心挑战在于如何高效且精确地计算目标函数相对于成千上万甚至数百万个设计参数的梯度。本章将深入探讨解决这一挑战的关键技术——伴随法（Adjoint Method），从其基本原理出发，系统地阐述其在[频域](@entry_id:160070)和时域、[微分方程](@entry_id:264184)和积分方程等不同电磁学模型中的实现机制，并延伸至[拓扑优化](@entry_id:147162)和[二阶优化](@entry_id:175310)等高级主题。

### 梯度计算的根本挑战

考虑一个泛型[优化问题](@entry_id:266749)，其目标是最小化一个实值[目标函数](@entry_id:267263) $J(\mathbf{p})$。这里的 $\mathbf{p} \in \mathbb{R}^N$ 是一个高维设计参数矢量，例如介质中每个点的[介电常数](@entry_id:146714)值。[目标函数](@entry_id:267263)通常依赖于一个状态场 $\mathbf{u}$（如[电场](@entry_id:194326)或[磁场](@entry_id:153296)），而该状态场本身又通过一个物理约束方程（如麦克斯韦方程）与设计参数 $\mathbf{p}$ 相关联。在离散形式下，此约束通常表现为一个线性（或[非线性](@entry_id:637147)）[方程组](@entry_id:193238)：

$$
\mathbf{A}(\mathbf{p})\mathbf{u}(\mathbf{p}) = \mathbf{b}
$$

其中 $\mathbf{A}$ 是系统矩阵，$\mathbf{u}$ 是状态矢量，$\mathbf{b}$ 是源项。[目标函数](@entry_id:267263)则可以写为 $J(\mathbf{p}) = f(\mathbf{u}(\mathbf{p}), \mathbf{p})$。

为了使用梯度下降法，我们需要计算梯度 $\nabla_{\mathbf{p}} J$。根据[链式法则](@entry_id:190743)，[目标函数](@entry_id:267263)对第 $i$ 个设计参数 $p_i$ 的导数为：

$$
\frac{dJ}{dp_i} = \frac{\partial f}{\partial p_i} + \left( \frac{\partial f}{\partial \mathbf{u}} \right)^T \frac{\partial \mathbf{u}}{\partial p_i}
$$

这种方法被称为**直接[微分](@entry_id:158718)法**。它需要计算状态场对每个设计参数的灵敏度 $\frac{\partial \mathbf{u}}{\partial p_i}$。这可以通过对状态方程求导得到：

$$
\mathbf{A}\frac{\partial \mathbf{u}}{\partial p_i} + \frac{\partial \mathbf{A}}{\partial p_i}\mathbf{u} = 0 \quad \implies \quad \frac{\partial \mathbf{u}}{\partial p_i} = -\mathbf{A}^{-1}\frac{\partial \mathbf{A}}{\partial p_i}\mathbf{u}
$$

计算完整的梯度 $\nabla_{\mathbf{p}} J$ 需要对每个设计参数 $p_i$（共 $N$ 个）求解一次上述线性方程组。在现代电磁设计问题中，设计参数的数量 $N$ 常常达到数百万，这意味着需要进行数百万次[大型线性系统](@entry_id:167283)求解。这种计算代价是无法承受的，从而使得直接法不切实际。

另一种方法是**[有限差分法](@entry_id:147158)**，例如，通过中心差分来近似梯度：

$$
\frac{\partial J}{\partial p_i} \approx \frac{J(\mathbf{p} + h\mathbf{e}_i) - J(\mathbf{p} - h\mathbf{e}_i)}{2h}
$$

其中 $\mathbf{e}_i$ 是第 $i$ 个标准[基矢](@entry_id:199546)量，$h$ 是一个小的步长。这种方法需要对每个参数进行两次正向求解（计算目标函数 $J$），因此总共需要 $2N$ 次求解。虽然避免了求解灵敏度，但计算量仍然与参数数量成正比，在大规模问题中同样不可行。此外，步长 $h$ 的选择还会引入[数值精度](@entry_id:173145)问题 。

显然，我们需要一种计算成本与设计参数数量无关的梯度计算方法。这正是伴随法的威力所在。

### 伴随法：高效计算的革命

伴随法的核心思想是引入一个辅助的“伴随”状态，通过一次额外的模拟来一次性获得目标函数对所有设计参数的梯度信息。这种方法的计算成本主要由两次系统求解（一次正向，一次伴随）决定，与设计参数的数量 $N$ 无关。

#### 从[拉格朗日乘子法](@entry_id:176596)到伴随方程

让我们从离散化的[频域](@entry_id:160070)电磁问题出发，来系统地推导伴随法。考虑一个由[有限元法](@entry_id:749389)（FEM）离散的[麦克斯韦方程组](@entry_id:150940)，其形式为 $\mathbf{A}(\mathbf{p})\mathbf{x}(\mathbf{p})=\mathbf{b}$，其中场分量 $\mathbf{x} \in \mathbb{C}^n$ 是复数。[目标函数](@entry_id:267263)通常是一个实数值，例如 $J = \frac{1}{2}\|\mathbf{C}\mathbf{x}-\mathbf{d}\|_2^2$ 。我们可以构造一个[拉格朗日函数](@entry_id:174593) $\mathcal{L}$，将PDE约束通过[拉格朗日乘子](@entry_id:142696)（即伴随矢量）$\boldsymbol{\lambda}$ 引入到[目标函数](@entry_id:267263)中：

$$
\mathcal{L}(\mathbf{p}, \mathbf{x}, \boldsymbol{\lambda}) = J(\mathbf{x}, \mathbf{p}) + \text{Re}[\boldsymbol{\lambda}^H (\mathbf{A}(\mathbf{p})\mathbf{x} - \mathbf{b})]
$$

这里，上标 $H$ 表示共轭转置。当[状态方程](@entry_id:274378)被满足时（即 $\mathbf{A}\mathbf{x}=\mathbf{b}$），$\mathcal{L} = J$。因此，目标函数对参数 $\mathbf{p}$ 的[全导数](@entry_id:137587)等于拉格朗日函数对 $\mathbf{p}$ 的[全导数](@entry_id:137587)。考虑一个微小的参数扰动 $\delta\mathbf{p}$，它会引起状态场扰动 $\delta\mathbf{x}$ 和目标函数变化 $\delta J$。$\mathcal{L}$ 的一阶变为：

$$
\delta \mathcal{L} = \frac{\partial J}{\partial \mathbf{p}}\delta\mathbf{p} + \text{Re}\left[\left(\frac{\partial J}{\partial \mathbf{x}^*}\right)^H \delta\mathbf{x}\right] + \text{Re}\left[\boldsymbol{\lambda}^H (\mathbf{A}\delta\mathbf{x} + \delta\mathbf{A}\mathbf{x})\right]
$$

这里我们使用了[复变函数](@entry_id:175282)的Wirtinger记法，并将[内积](@entry_id:158127)定义为第一个变量[共轭线性](@entry_id:268590)。重新整理关于 $\delta\mathbf{x}$ 的项：

$$
\delta \mathcal{L} = \frac{\partial J}{\partial \mathbf{p}}\delta\mathbf{p} + \text{Re}\left[\boldsymbol{\lambda}^H \delta\mathbf{A}\mathbf{x}\right] + \text{Re}\left[\left(\left(\frac{\partial J}{\partial \mathbf{x}^*}\right)^H + \boldsymbol{\lambda}^H\mathbf{A}\right)\delta\mathbf{x}\right]
$$

伴随法的精髓在于，我们可以通过巧妙地选择伴随矢量 $\boldsymbol{\lambda}$ 来消除上式中棘手的 $\delta\mathbf{x}$ 项。我们定义**伴随方程**如下：

$$
\mathbf{A}^H \boldsymbol{\lambda} = -\frac{\partial J}{\partial \mathbf{x}^*}
$$

注意到，这个方程的右端项是[目标函数](@entry_id:267263)对状态场共轭 $\mathbf{x}^*$ 的导数，它代表了“目标函数对状态场的敏感度”。求解这个方程，我们就能得到伴随场 $\boldsymbol{\lambda}$。由于 $\mathbf{A}^H \boldsymbol{\lambda} = -\frac{\partial J}{\partial \mathbf{x}^*}$ 蕴含着 $(\boldsymbol{\lambda}^H \mathbf{A})^H = - \frac{\partial J}{\partial \mathbf{x}^*}$，所以 $\boldsymbol{\lambda}^H \mathbf{A} = -(\frac{\partial J}{\partial \mathbf{x}^*})^H$。代入 $\delta\mathcal{L}$ 的表达式，关于 $\delta\mathbf{x}$ 的项正好被抵消。

此时，拉格朗日函数的变化简化为：

$$
\delta J = \delta \mathcal{L} = \frac{\partial J}{\partial \mathbf{p}}\delta\mathbf{p} + \text{Re}\left[\boldsymbol{\lambda}^H \delta\mathbf{A}\mathbf{x}\right]
$$

对于[线性依赖](@entry_id:185830)于参数的矩阵 $\mathbf{A}(\mathbf{p})$，我们有 $\delta\mathbf{A} = \sum_i \frac{\partial\mathbf{A}}{\partial p_i}\delta p_i$。因此，我们可以直接读出目标函数对每个参数 $p_i$ 的梯度：

$$
\frac{dJ}{dp_i} = \frac{\partial J}{\partial p_i} + \text{Re}\left[\boldsymbol{\lambda}^H \frac{\partial\mathbf{A}}{\partial p_i} \mathbf{x}\right]
$$

如果目标函数不直接依赖于 $\mathbf{p}$（即 $\frac{\partial J}{\partial \mathbf{p}}=0$），则梯度表达式进一步简化。这个最终的梯度表达式只依赖于正向场 $\mathbf{x}$、伴随场 $\boldsymbol{\lambda}$ 和系统矩阵对参数的导数 $\frac{\partial\mathbf{A}}{\partial p_i}$。后者通常很容易解析计算。

**结论**：计算包含任意数量参数的完整梯度，其计算成本主要在于：
1.  **一次正向求解**：解 $\mathbf{A}(\mathbf{p})\mathbf{x}=\mathbf{b}$ 得到状态场 $\mathbf{x}$。
2.  **一次伴随求解**：解 $\mathbf{A}^H \boldsymbol{\lambda} = -\frac{\partial J}{\partial \mathbf{x}^*}$ 得到伴随场 $\boldsymbol{\lambda}$。

这种计算成本的独立性使得伴随法成为大规模电磁[逆向设计](@entry_id:158030)的基石。

### 不同物理模型中的伴随法

伴随法的原理是普适的，可以应用于各种电磁学建模方法。

#### [微分方程](@entry_id:264184)方法 (FEM/FDM)

在有限元法（FEM）或[有限差分法](@entry_id:147158)（FDM）中，物理系统的[偏微分方程](@entry_id:141332)被离散为[大型稀疏矩阵](@entry_id:144372)方程。例如，对于[频域](@entry_id:160070)麦克斯韦方程  或[亥姆霍兹方程](@entry_id:149977) ，我们得到的离散系统矩阵 $\mathbf{A}$ 直接对应于微分算子（如旋度-[旋度算子](@entry_id:184984)或拉普拉斯算子）。在这些情况下，[伴随算子](@entry_id:140236) $\mathbf{A}^H$ 是离散算子的[共轭转置](@entry_id:147909)。如果原始算子是自伴的（在物理上对应于无损互易系统），则 $\mathbf{A}^H = \mathbf{A}$，正向和伴随方程具有相同的系统矩阵，但源项不同。

#### [积分方程方法](@entry_id:750697) (MoM/BEM)

在[矩量法](@entry_id:752140)（MoM）或[边界元法](@entry_id:141290)（BEM）中，电磁问题被转化为积分方程。例如，利用格林函数和[Lippmann-Schwinger方程](@entry_id:142814)来描述散射问题  。离散化后得到的[系统矩阵](@entry_id:172230) $\mathbf{Z}$ 通常是稠密的。尽管矩阵形式不同，伴随法的原理完全适用。

一个特别富有洞察力的例子是[格林函数](@entry_id:147802)本身的函数导数。对于一个由[介电常数](@entry_id:146714) $\epsilon(\mathbf{r}')$ 扰动引起的[格林函数](@entry_id:147802) $G(\mathbf{r}_o, \mathbf{r}_s)$ 的变化，其函数导数可以被证明为 ：

$$
\frac{\delta G(\mathbf{r}_o, \mathbf{r}_s)}{\delta \epsilon(\mathbf{r}')} \propto G(\mathbf{r}_o, \mathbf{r}') G(\mathbf{r}', \mathbf{r}_s)
$$

这个优美的公式表明，在 $\mathbf{r}'$ 处的[介电常数](@entry_id:146714)扰动对从源 $\mathbf{r}_s$ 到观察点 $\mathbf{r}_o$ 的场的影响，等于从源到扰动点、再从扰动点到观察点的场的乘积。这正是伴随思想的连续形式体现：正向传播的场 $G(\mathbf{r}', \mathbf{r}_s)$ 与[反向传播](@entry_id:199535)的“伴随”场 $G(\mathbf{r}_o, \mathbf{r}')$ 在扰动点处相互作用。

另一个简洁的例子是**[近场](@entry_id:269780)到远场（NTF）变换算子** 。这个算子通常是一个[傅里叶变换](@entry_id:142120)类型的积分，将[表面电流](@entry_id:261791)[分布](@entry_id:182848) $J_s$ 映射到[远场](@entry_id:269288)方向图 $E_\infty$。其伴随算子 $\mathcal{N}^\dagger$ 则具有清晰的物理解释：它将[远场](@entry_id:269288)中的“敏感度”信息传播回溯，变为表面上的等效“伴随”源。这种对偶性是所有伴随方法的核心。

### 高级机制与扩展

伴随法不仅限于简单的线性、静态问题，它可以被扩展以处理更复杂的物理和优化场景。

#### 时域伴随法：时间反演的视角

对于时域问题，如使用[FDTD方法](@entry_id:263763)求解麦克斯韦方程，我们同样可以推导伴随法 。此时，[拉格朗日函数](@entry_id:174593)需要在整个时空域上进行积分。推导过程（通过时空积分的[分部积分](@entry_id:136350)）揭示了一个关键特征：**时域伴随方程必须在时间上反向求解**。

具体来说，正向模拟从 $t=0$ 演化到 $t=T$，并记录下[目标函数](@entry_id:267263)所依赖的场量的时间历史。然后，伴随模拟从一个零值的终端条件 $t=T$ 开始，在时间上向 $t=0$ 反向演化。伴随方程的源项则由正向模拟中记录的场历史提供。

从物理上看，伴随场代表了最终目标函数对时空中任意一点的脉冲扰动的敏感度。为了评估这种敏感度，信息必须从最终时刻 $T$ “[反向传播](@entry_id:199535)”回扰动发生的时刻。

一个重要的细节是，如果正向模型包含损耗（如电导率 $\sigma > 0$），其控制方程中会出现耗散项，例如 $-\sigma E$。在推导出的伴随方程中，对应的项会变为 $+\sigma E^a$，表现为增益。这是符合物理直觉的：伴随系统必须“补偿”正向传播过程中因损耗而丢失的信息，才能准确地将敏感度传播回去 。

#### 处理[色散材料](@entry_id:748559)：[ADE](@entry_id:198734)伴随法

当材料的[介电常数](@entry_id:146714)随频率变化时（即存在[色散](@entry_id:263750)），例如金属的Drude模型，直接在[频域](@entry_id:160070)对每个频率点进行优化会变得复杂。**辅助[微分方程](@entry_id:264184)（[ADE](@entry_id:198734)）**方法通过引入额外的场变量（如[极化场](@entry_id:197617) $\mathbf{P}$）来将频率依赖性转化为一个与频率无关的、更大的[方程组](@entry_id:193238) 。

例如，对于Drude模型，我们可以将状态矢量扩充为 $(\mathbf{E}, \mathbf{P})$。离散后，每个频率 $\omega_k$ 的正向问题都具有相同的[块矩阵](@entry_id:148435)结构，只是矩阵中的某些块依赖于 $\omega_k$。

$$
\begin{pmatrix} \mathbf{A}_{EE}(\omega_k) & \mathbf{A}_{EP}(\omega_k) \\ \mathbf{A}_{PE}(\omega_k, \mathbf{p}) & \mathbf{A}_{PP}(\omega_k) \end{pmatrix} \begin{pmatrix} \mathbf{E}_k \\ \mathbf{P}_k \end{pmatrix} = \begin{pmatrix} \mathbf{s}_k \\ \mathbf{0} \end{pmatrix}
$$

设计参数（如等离激元频率 $\omega_p^2$）可能只出现在其中一个[块矩阵](@entry_id:148435)中。对这个增广系统应用伴随法，我们会得到一个具有相同块结构的伴随[方程组](@entry_id:193238)，求解伴随场 $(\boldsymbol{\lambda}_E, \boldsymbol{\lambda}_P)$。最终的梯度表达式将优雅地耦合正向场和伴随场，例如，可能只涉及 $\mathbf{E}_k$ 和 $\boldsymbol{\lambda}_{P,k}$ 的乘积 。这种方法在宽带器件优化中至关重要。

#### 拓扑优化与投影方法

在许多设计问题中，我们希望得到的是由两种或几种离散材料构成的“黑白”或“0-1”式设计。直接优化[离散变量](@entry_id:263628)是一个[组合优化](@entry_id:264983)问题，通常非常困难。**[拓扑优化](@entry_id:147162)**通过引入连续的设计变量来规避这个问题。

一种常用的技术是**[水平集方法](@entry_id:165633)**，其中设计由一个连续的“[水平集](@entry_id:751248)函数” $\phi$ 的符号决定。为了便于梯度优化，通常使用一个平滑的[Heaviside函数](@entry_id:176879)（或其近似）来将 $\phi$ 映射到材料属性上，例如，使用 $\tanh$ 函数 ：

$$
m(\phi, \beta) = \tanh(\beta\phi)
$$

这里的 $m$ 是一个在-1到1之间的中间变量，可以被[线性映射](@entry_id:185132)到两种材料的[介电常数](@entry_id:146714)之间。$\beta$ 是一个锐化参数。设计变量现在是光滑的场 $\phi$。

梯度计算可以通过[链式法则](@entry_id:190743)完成。[目标函数](@entry_id:267263)对 $\phi$ 的梯度可以分解为：

$$
\nabla_{\phi} J = \frac{\partial m}{\partial \phi} \odot \frac{\partial \epsilon}{\partial m} \odot \nabla_{\epsilon} J
$$

其中 $\odot$ 表示逐元素乘积，$\nabla_{\epsilon} J$ 由标准的伴随法计算。链式法则中的前两项通常是简单的[对角算子](@entry_id:262993)，易于计算。

在优化过程中，可以采用**连续化（Continuation）**策略：从一个较小的 $\beta$ 值（对应于模糊的、混合材料的设计）开始优化，然后逐渐增大 $\beta$ 值，迫使设计结果趋向于“黑白分明” 。这种方法有助于避免陷入不良的局部最优解。

### 超越一阶：Hessian矢量积

梯度为我们指明了最优化的“下山”方向，但并未提供关于目标函数曲率的信息。二阶方法，如牛顿法，利用Hessian矩阵（梯度的梯度）来寻找更优的下降步长，从而可能实现更快的收敛。然而，对于一个有 $N$ 个参数的系统，Hessian矩阵 $\mathbf{H}$ 是一个 $N \times N$ 的稠密矩阵，直接计算和存储它比计算梯度还要昂贵得多。

幸运的是，许多先进的优化算法（如Newton-CG）并不需要完整的Hessian矩阵，而只需要计算**Hessian矢量积 (Hessian-vector product, HVP)**，即 $\mathbf{H}\mathbf{v}$，其中 $\mathbf{v}$ 是一个给定的方向矢量。HVP可以通过一种称为“二阶伴随法”或“增量伴随法”的技术高效计算，其计算成本同样与参数数量 $N$ 无关。

该方法的核心是对计算梯度的一阶伴随系统再次求导。推导过程表明，计算一次HVP需要求解两个额外的[线性方程组](@entry_id:148943)（一个增量正向方程和一个增量伴随方程），其[系统矩阵](@entry_id:172230)与原始的正向/伴随问题相同 。因此，一次HVP的计算成本大约是梯度计算的两倍，这使得基于HVP的[二阶优化](@entry_id:175310)方法成为可能。

### 特殊主题：处理[简并系统](@entry_id:203460)

在光子晶体等周期性结构的研究中，我们经常遇到[能带结构计算](@entry_id:270613)，这本质上是一个求解[本征值](@entry_id:154894)的问题。在布里渊区的高[对称点](@entry_id:174836)，能带（[本征值](@entry_id:154894)）可能会出现简并，即多个[本征态](@entry_id:149904)对应于同一个本征频率 。

在这种情况下，标准的[非简并微扰理论](@entry_id:153724)和[Hellmann-Feynman定理](@entry_id:173798)失效。为了计算与能带分裂相关的物理量（如群速度或[狄拉克锥](@entry_id:144336)斜率）的梯度，必须使用**[简并微扰理论](@entry_id:143587)**。这要求我们将微扰算子（例如，由[波矢](@entry_id:178620) $\mathbf{k}$ 的微小变化引起的算子变化）投影到简并[子空间](@entry_id:150286)上，并求解一个更小的、在简并[子空间](@entry_id:150286)内部的有效[本征问题](@entry_id:748835)。通过对这个小系统的分析，我们可以推导出简并频率分裂的梯度，并进而优化[色散](@entry_id:263750)特性 。

### 实践中的黄金法则：梯度检验

伴随法的推导和实现涉及复杂的数学和编程细节，极易出错。因此，**梯度检验（Gradient Check）**是开发和调试过程中的一个不可或缺的步骤。

梯度检验的原理基于[泰勒展开](@entry_id:145057)。一个函数在一个方向 $\mathbf{v}$ 上的[方向导数](@entry_id:189133) $(\nabla J)^T \mathbf{v}$ 可以通过[中心差分](@entry_id:173198)来高精度地近似：

$$
(\nabla J)^T \mathbf{v} \approx \frac{J(\mathbf{p} + h\mathbf{v}) - J(\mathbf{p} - h\mathbf{v})}{2h}
$$

实践中的检验流程如下 ：
1.  使用伴随法计算梯度 $\mathbf{g}_{\text{adj}}$。
2.  选择一个随机的单位方向矢量 $\mathbf{v}$。
3.  计算伴随法得到的[方向导数](@entry_id:189133)：$D_{\text{adj}} = \mathbf{g}_{\text{adj}}^T \mathbf{v}$。
4.  使用[有限差分](@entry_id:167874)计算数值方向导数：$D_{\text{fd}} = \frac{J(\mathbf{p} + h\mathbf{v}) - J(\mathbf{p} - h\mathbf{v})}{2h}$。这需要两次额外的正向求解。
5.  比较 $D_{\text{adj}}$ 和 $D_{\text{fd}}$。两者应该在很高的精度下吻合。

如果两者不符，则说明伴随法的推导或实现中存在错误。这个简单的检验步骤能够为复杂的梯度计算代码提供强大的信心保证。