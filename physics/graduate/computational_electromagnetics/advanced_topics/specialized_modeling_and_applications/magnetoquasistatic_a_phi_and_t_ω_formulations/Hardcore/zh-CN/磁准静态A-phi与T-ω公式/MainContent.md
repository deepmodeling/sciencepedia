## 引言
在计算电磁学领域，为了高效求解电机、变压器、感应加热和磁共振成像（MRI）线圈等低频设备中的复杂电磁现象，直接求解麦克斯韦方程组往往成本高昂。磁准静态（MQS）近似通过忽略位移电流，为这类磁场主导的问题提供了精确且高效的建模框架。然而，在MQS框架内，如何选择合适的势函数公式——例如，是采用全局的磁矢量势-电标量势（A-φ）法，还是采用区域分解的电流矢量势-磁标量势（T-ω）法——是每个研究者和工程师必须面对的关键抉择，这直接影响到模型的计算效率、数值稳定性和处理复杂几何拓扑的能力。

本文旨在填补理论与实践之间的鸿沟，为读者提供一个关于A-φ与T-ω公式的系统性、比较性的深度指南。我们将通过三个章节的递进式探讨，帮助您全面掌握这两种核心方法：

- **第一章：原理与机制**，将从麦克斯韦方程组出发，详细推导两种公式的控制方程，探讨其背后的物理意义、规范自由度问题及其数值处理方法，并深入分析在复杂拓扑结构下两种公式的理论完备性。
- **第二章：应用与跨学科连接**，将展示这些理论如何在实际工程问题中发挥作用，涵盖从经典的涡流分析、电路参数提取，到先进的场路耦合仿真和MRI梯度线圈设计等跨学科应用。
- **第三章：动手实践**，将通过一系列精心设计的编程练习，引导您亲手解决数值实现中的关键挑战，如边界条件处理和规范固定，从而将理论知识转化为实践能力。

现在，让我们首先进入第一章，深入探索这两种强大公式的底层原理与核心机制。

## 原理与机制

本章深入探讨磁准静态（Magnetoquasistatic, MQS）近似下的两种核心势函数表述：磁矢量势-电标量势（$\mathbf{A}-\phi$）法和电流矢量势-磁标量势（$\mathbf{T}-\Omega$）法。我们将从基本物理原理出发，推导这些表述的控制方程，分析其数学性质，并探讨其在有限元数值计算中的实现细节、优缺点以及在复杂拓扑结构下的理论完备性。

### 磁准静态近似

电磁学的完整描述由麦克斯韦方程组给出。然而，在许多工程应用中，系统的工作频率和尺寸使得某些电磁效应可以被忽略，从而简化模型。磁准静态（MQS）近似是其中一种至关重要的简化。

MQS近似的核心思想是，在良导体或低频应用中，位移电流密度 $\partial \mathbf{D}/\partial t$ 的贡献远小于传导电流密度 $\mathbf{J}$。从安培-麦克斯韦定律 $\nabla \times \mathbf{H} = \mathbf{J} + \partial \mathbf{D}/\partial t$ 出发，MQS近似假设：

$$
\left| \frac{\partial \mathbf{D}}{\partial t} \right| \ll |\mathbf{J}|
$$

对于一个角频率为 $\omega$ 的时谐过程，并考虑线性各向同性介质，其中电导率为 $\sigma$，介电常数为 $\epsilon$，上述条件可以表示为一个无量纲参数 $\kappa$ 远小于1：

$$
\kappa \equiv \frac{|\epsilon \partial \mathbf{E}/\partial t|}{|\sigma \mathbf{E}|} \approx \frac{\omega\epsilon}{\sigma} \ll 1
$$

这个参数完全由材料属性（$\epsilon, \sigma$）和工作频率（$\omega$）决定，与系统的特征尺寸 $L$ 或磁导率 $\mu$ 无关。在此近似下，安培-麦克斯韦定律简化为安培定律：

$$
\nabla \times \mathbf{H} \approx \mathbf{J}
$$

重要的是，MQS近似完整保留了法拉第电磁感应定律 $\nabla \times \mathbf{E} = -\partial \mathbf{B}/\partial t$，因为正是这一项描述了变化的磁场如何感生电场，从而产生涡流——这是MQS问题研究的核心物理现象。因此，MQS近似适用于电感、变压器、电机和涡流无损检测等磁效应主导的设备。必须注意，$\kappa \ll 1$ 这个条件不同于所有准静态近似（包括MQS和EQS）都需满足的另一个条件，即系统尺寸 $L$ 远小于波长 $\lambda$（等价于 $\omega L \sqrt{\mu\epsilon} \ll 1$），后者保证了电磁波传播的延迟效应可以忽略不计 [@problem_id:3328296]。

MQS近似的一个直接物理后果是电磁场在导体中的扩散行为，即集肤效应。我们可以通过一个简单的思想实验来揭示这一点。考虑一个均匀的良导体半空间（$z>0$），其电导率为 $\sigma$，磁导率为 $\mu$。在MQS近似下，并采用一种将在后文介绍的 $\mathbf{A}-\phi$ 势函数表示，可以推导出磁矢量势 $\mathbf{A}$ 在无源导体区域内遵循一个扩散型偏微分方程 [@problem_id:3328293]：

$$
\sigma \frac{\partial \mathbf{A}}{\partial t} - \frac{1}{\mu} \nabla^2 \mathbf{A} = \mathbf{0}
$$

对于一个施加在导体表面（$z=0$）的频率为 $\omega$ 的时谐切向磁场，此方程的解表明，场在导体内部的幅度呈指数衰减，其形式为 $\exp(-z/\delta)$，其中 $\delta = \sqrt{2/(\omega\mu\sigma)}$ 是著名的**集肤深度**。这清晰地表明了MQS模型如何捕捉到高频电流趋于导体表面的关键物理现象。

### 磁矢量势 ($\mathbf{A}-\phi$) 法

$\mathbf{A}-\phi$ 法是一种在整个计算域中求解电磁场的“全局”方法。它通过引入势函数来自动满足麦克斯韦方程组中的两个齐次方程。

根据高斯磁定律 $\nabla \cdot \mathbf{B} = 0$，我们可以引入**磁矢量势** $\mathbf{A}$，使得：

$$
\mathbf{B} = \nabla \times \mathbf{A}
$$

因为任何旋度场的散度恒为零。接着，将此定义代入法拉第定律 $\nabla \times \mathbf{E} = -\partial \mathbf{B}/\partial t$，得到 $\nabla \times (\mathbf{E} + \partial \mathbf{A}/\partial t) = \mathbf{0}$。一个无旋场可以表示为某个标量势的梯度。因此，我们引入**电标量势** $\phi$，使得：

$$
\mathbf{E} = -\frac{\partial \mathbf{A}}{\partial t} - \nabla \phi
$$

在电准静态（EQS）近似下，$\partial \mathbf{B}/\partial t \approx \mathbf{0}$，因此 $\nabla \times \mathbf{E} \approx \mathbf{0}$，电场可以被简化为 $\mathbf{E} = -\nabla\phi$，此时磁矢量势 $\mathbf{A}$ 的动态项可以忽略。然而，在MQS中，$\partial \mathbf{A}/\partial t$ 项是描述电磁感应的核心，不可或缺 [@problem_id:3328300]。

将这些势函数定义代入MQS安培定律 $\nabla \times \mathbf{H} = \mathbf{J}$ 和本构关系 $\mathbf{J}=\sigma\mathbf{E}$，即可得到关于 $\mathbf{A}$ 和 $\phi$ 的耦合偏微分方程组。

这种势函数表示的一个关键特性是**规范自由度**。对于任意一个足够光滑的标量场 $\psi(\mathbf{x}, t)$，进行如下变换：

$$
\mathbf{A}' = \mathbf{A} + \nabla \psi, \quad \phi' = \phi - \frac{\partial \psi}{\partial t}
$$

可以验证，变换后的势函数 $(\mathbf{A}', \phi')$ 产生的物理场 $\mathbf{E}$ 和 $\mathbf{B}$ 与原始势函数 $(\mathbf{A}, \phi)$ 产生的完全相同 [@problem_id:3328300]。这种不唯一性意味着，为了得到唯一的数值解，我们必须施加一个额外的约束条件，即选择一个“规范”。一个常见的选择是**库伦规范**：

$$
\nabla \cdot \mathbf{A} = 0
$$

在MQS近似下，安培定律 $\nabla \times \mathbf{H} \approx \mathbf{J}$ 意味着传导电流是无散的，即 $\nabla \cdot \mathbf{J} = 0$。但这并不意味着电标量势 $\phi$ 可以被忽略。将 $\mathbf{J} = \sigma(-\partial\mathbf{A}/\partial t - \nabla\phi)$ 代入 $\nabla \cdot \mathbf{J} = 0$ 可得关于 $\phi$ 的方程。例如，在均匀电导率的导体中，此方程变为 $-\sigma\nabla \cdot (\partial\mathbf{A}/\partial t) - \sigma\nabla^2\phi = 0$。这表明 $\phi$ 通常不为零，它描述了由电磁感应和电荷分布（尽管在MQS中时间变化率 $\partial\rho/\partial t = -\nabla \cdot \mathbf{J} \approx 0$）所产生的非旋电场部分，这部分电场对于驱动导体中的电流至关重要 [@problem_id:3328300]。

### $\mathbf{A}-\phi$ 法的数值实现

将 $\mathbf{A}-\phi$ 方程组转化为可计算的离散形式，通常采用有限元方法（FEM）。这需要将问题表述为弱形式，并为未知量选择合适的函数空间（Sobolev空间）。

对于一个有限能量的系统，磁场能量 $\int \mu^{-1} |\mathbf{B}|^2 dV$ 和焦耳损耗 $\int \sigma |\mathbf{E}|^2 dV$ 必须是有限的。这直接决定了势函数所需的数学正则性 [@problem_id:3328316]：
-   由于磁场能量包含 $\mathbf{B} = \nabla \times \mathbf{A}$，因此 $\mathbf{A}$ 的旋度必须是平方可积的。这自然地将 $\mathbf{A}$ 归入 **$H(\mathrm{curl})$ 空间**。
-   焦耳损耗包含 $\mathbf{E}$，而 $\mathbf{E}$ 的一部分来自 $-\nabla\phi$。这要求 $\phi$ 的梯度必须是平方可积的，因此 $\phi$ 必须属于 **$H^1$ 空间**。

为了构建满足这些正则性要求的“适定”有限元逼近，需要选择特定的有限元基函数：
-   对于 $H(\mathrm{curl})$ 空间的矢量场 $\mathbf{A}$，通常使用**Nédélec边元（edge elements）**。这种单元的自由度与单元的边相关联，能够精确地保证矢量场在单元间的切向分量连续，这正是 $H(\mathrm{curl})$ 空间的核心要求。
-   对于 $H^1$ 空间的标量场 $\phi$，则使用标准的**Lagrange节单元（nodal elements）**，其自由度位于单元的顶点。这保证了 $\phi$ 在单元间的 $C^0$ 连续性，从而使其梯度（虽然可能不连续）是平方可积的。

即使选择了正确的有限元，规范自由度问题依然存在于离散系统中，表现为最终的代数矩阵方程是奇异的。为了解决这个问题，可以采用多种规范固定技术。一种流行的方法是**梯度-散度惩罚法**。该方法通过在弱形式中添加一个惩罚项来近似地强制执行库伦规范 [@problem_id:3328301]：

$$
\alpha \int_{\Omega} (\nabla \cdot \mathbf{A})(\nabla \cdot \mathbf{v}) dV
$$

其中 $\mathbf{v}$ 是测试函数，$\alpha$ 是一个正的惩罚参数。这个项惩罚了那些散度不为零的解。选择合适的 $\alpha$ 是一种权衡：
-   一个非常大的 $\alpha$ 会更严格地强制 $\nabla \cdot \mathbf{A} \approx 0$，但会导致系统矩阵的条件数恶化（通常与 $\alpha$ 成正比），使得迭代求解器收敛缓慢或失败。
-   一个太小的 $\alpha$ 对改善奇异性作用不大，规范约束的满足程度也较差。

在实践中，通常选择 $\alpha$ 与磁阻率 $\nu = 1/\mu$ 的量级相当，以平衡旋度项和散度项的贡献。这使得在 $\alpha$ 不太小的情况下，总误差由空间离散化主导，同时 divergence error 则大致按 $\mathcal{O}(\alpha^{-1})$ 的比例减小 [@problem_id:3328301]。

### 电流矢量势 ($\mathbf{T}-\Omega$) 法

$\mathbf{T}-\Omega$ 法是一种混合方法，它在问题的不同区域使用不同的势函数，通常在计算上比 $\mathbf{A}-\phi$ 法更高效。

其核心思想是在导电区域 $\mathcal{C}$ 和非导电区域 $\mathcal{I}$ 分别引入最适合描述该区域物理的势：
-   在导电区域 $\mathcal{C}$，MQS安培定律 $\nabla \times \mathbf{H} = \mathbf{J}$ 意味着电流密度是无散的，$\nabla \cdot \mathbf{J} = 0$。因此，我们可以引入**电流矢量势** $\mathbf{T}$（在文献中也称为电矢量势），使得：
    $$
    \mathbf{J} = \nabla \times \mathbf{T}
    $$
-   在非导电（绝缘）区域 $\mathcal{I}$，电流密度为零，因此 $\nabla \times \mathbf{H} = \mathbf{0}$。这表明 $\mathbf{H}$ 是一个无旋场，可以表示为**磁标量势** $\Omega$ 的负梯度：
    $$
    \mathbf{H} = -\nabla \Omega
    $$

为了构建完整的模型，我们还需要知道导体内部的磁场 $\mathbf{H}$。从 $\nabla \times \mathbf{H} = \mathbf{J} = \nabla \times \mathbf{T}$ 可得 $\nabla \times (\mathbf{H} - \mathbf{T}) = \mathbf{0}$。这意味着向量 $(\mathbf{H}-\mathbf{T})$ 是无旋的，因此也可以表示为某个标量势的负梯度。为了与绝缘区的势函数保持一致性，我们将其写为 $-\nabla\Omega$，从而得到导体内部磁场的表达式 [@problem_id:3328332]：

$$
\mathbf{H} = \mathbf{T} - \nabla\Omega \quad (\text{in } \mathcal{C})
$$

这里的 $\Omega$ 通常被延拓至整个计算域。两种势函数通过界面 $\Gamma$ 上的物理边界条件耦合起来。在界面上没有表面电流的假设下，这些条件是：
1.  **切向磁场 $\mathbf{H}$ 的连续性**: $\mathbf{n} \times \mathbf{H}_{\mathcal{C}} = \mathbf{n} \times \mathbf{H}_{\mathcal{I}}$
2.  **法向磁通密度 $\mathbf{B}$ 的连续性**: $\mathbf{n} \cdot \mathbf{B}_{\mathcal{C}} = \mathbf{n} \cdot \mathbf{B}_{\mathcal{I}}$

将势函数表达式代入，并采用一个常见的规范选择即 $\mathbf{T}$ 在界面上是切向的（$\mathbf{n} \cdot \mathbf{T} = 0$），我们得到耦合方程 [@problem_id:3328368]：

$$
\mathbf{n} \times (\mathbf{T} - \nabla\Omega) = \mathbf{n} \times (-\nabla\Omega)
$$
$$
\mathbf{n} \cdot (\mu_{\mathcal{C}}(\mathbf{T} - \nabla\Omega)) = \mathbf{n} \cdot (\mu_{\mathcal{I}}(-\nabla\Omega)) \implies \mu_{\mathcal{C}}(-\frac{\partial\Omega}{\partial n}) = \mu_{\mathcal{I}}(-\frac{\partial\Omega}{\partial n})
$$

$\mathbf{T}-\Omega$ 法同样具有规范自由度。变换 $\mathbf{T} \mapsto \mathbf{T} + \nabla\psi$ 不改变物理量 $\mathbf{J}$，而变换 $\Omega \mapsto \Omega + C$（$C$为常数）不改变物理量 $\mathbf{H}$。为了确保解的唯一性，必须固定这些规范。对于 $\mathbf{T}$，可以施加类似于库伦规范的条件 $\nabla \cdot \mathbf{T} = 0$，或采用基于图论的**树-余树（tree-cotree）分解**来消除离散系统中的梯度场自由度。对于 $\Omega$，只需在某个点或区域将其值固定（例如，$\Omega=0$），或者施加零均值条件即可 [@problem_id:3328348]。

在函数空间和有限元选择上，$\mathbf{T}-\Omega$ 法与 $\mathbf{A}-\phi$ 法类似：$\mathbf{T}$ 属于 $H(\mathrm{curl})$ 空间，用边元离散；$\Omega$ 属于 $H^1$ 空间，用节元离散 [@problem_id:3328316]。

### 对比与进阶论题

选择 $\mathbf{A}-\phi$ 还是 $\mathbf{T}-\Omega$ 法，很大程度上取决于具体问题的计算成本和数值稳定性。

#### 数值性能比较

对于典型的涡流问题，即导体被大片空气或绝缘体包围的情况，$\mathbf{T}-\Omega$ 法通常具有显著优势 [@problem_id:3328355]。
-   **系统规模与稀疏性**：在 $\mathbf{A}-\phi$ 法中，磁矢量势 $\mathbf{A}$ 必须在整个计算域（包括广阔的空气域）中求解，这导致自由度数量巨大。相比之下，$\mathbf{T}-\Omega$ 法将自由度限制在它们“活跃”的区域：$\mathbf{T}$ 仅在导体内部，$\Omega$ 仅在导体外部。这通常会产生一个规模小得多的代数系统。
-   **条件数与稳定性**：未经规范固定的 $\mathbf{A}-\phi$ 法在数值上存在一个严重缺陷。其离散算子的零空间不仅包含全局的梯度场，还包含了所有仅存在于绝缘区域内的梯度场。这个庞大的零空间使得系统矩阵严重病态或奇异，给求解带来了巨大困难。而 $\mathbf{T}-\Omega$ 法，通过分离变量，其唯一的非物理零空间来自 $\Omega$ 的一个常数自由度，这很容易通过固定一点来消除。因此，$\mathbf{T}-\Omega$ 法产生的矩阵系统通常具有更好的条件数，求解更为稳定和高效。

#### 多连通域中的拓扑问题

当计算域（导体或绝缘体）的拓扑结构变得复杂时（例如，带有孔洞或环柄），势函数的简单定义可能不再完备。这种复杂性通过**Betti数**来量化，其中一阶Betti数 $b_1$ 表示域中独立的“环”或“隧道”的数量。

在多连通域中，存在所谓的**谐波场**——它们既无旋又无散，但不能表示为全局单值势的梯度或旋度。
-   在绝缘区 $I$ 中，如果 $b_1(I) > 0$，则存在 $b_1(I)$ 个独立的谐波磁场。这些场对应于环绕 $I$ 中“隧道”的非零环路积分，它们无法由单值的 $-\nabla\Omega$ 表示。
-   在导电区 $C$ 中，如果 $b_1(C) > 0$，则存在 $b_1(C)$ 个独立的谐波电流。这些电流对应于流经 $C$ 中“环柄”的净电流，它们无法由全局的 $\nabla \times \mathbf{T}$ 表示。

为了使两种 formulation 在拓扑复杂的域中等价并能描述所有物理现象，必须对它们进行扩展，以包含这些谐波场。这通常通过向有限元空间中添加一个维度为 $b_1(I) + b_1(C)$ 的谐波场基函数空间来实现。每增加一个基函数，就需要一个额外的约束（例如，指定通过某个环路的净电流或磁通量）来获得唯一解 [@problem_id:3328308]。

物理上，绝缘区中的谐波磁场是由流经导体并与绝缘区“隧道”相链接的电流产生的。数学上，这体现为绝缘区的一阶上同调群 $H^1(I)$ 与导电区的一阶同调群 $H_1(C)$ 之间存在一个非简并的“环绕数”配对。这种配对的非简并性要求 $\dim(H^1(I)) = \dim(H_1(C))$，即 $b_1(I)=b_1(C)$。这个拓扑条件是保证两种 formulation 能够一致地描述复杂域中磁场与电流耦合的基础。例如，在一个具有 $b_1(I)=4$ 和 $b_1(C)=4$ 的域中，总共需要 $4+4=8$ 个独立的谐波基函数来完备地描述系统中的所有拓扑效应 [@problem_id:3328308]。