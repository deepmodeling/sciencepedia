## 引言
在[计算电磁学](@entry_id:265339)领域，有限元方法（FEM）作为一种功能强大且适应性强的数值工具，被广泛应用于求解各种复杂的[电磁场](@entry_id:265881)问题。无论是[天线设计](@entry_id:746476)、微波[电路分析](@entry_id:261116)还是散射特性预测，其核心都离不开将连续的麦克斯韦方程转化为离散的[代数方程](@entry_id:272665)组。这一转化的关键桥梁，正是单元[刚度矩阵与质量矩阵](@entry_id:173907)的构建与组装。然而，许多学习者和初级研究人员在面对这一过程时，常常困于繁杂的数学公式与抽象的理论概念，难以将其与物理直觉和实际应用有效连接。

本文旨在填补这一知识鸿沟，系统性地阐述单元刚度与[质量矩阵](@entry_id:177093)组装的完整图景。我们将带领读者从理论走向实践，不仅理解“如何计算”，更洞悉“为何如此计算”。
- 在“原理与机制”一章中，我们将从麦克斯韦方程的弱形式出发，详细拆解刚度与质量矩阵的物理意义、数学定义以及在参考单元上的计算方法，并探讨材料属性、集成过程等关键技术细节。
- 随后的“应用与跨学科联系”一章将展示这一基本框架的强大扩展性，探讨如何利用它来模拟高级边界条件（如[完美匹配层](@entry_id:753330)）、分析周期性结构（如光子晶体），并揭示其与固体物理、[材料科学](@entry_id:152226)等领域的深刻联系。
- 最后，通过“动手实践”部分提供的精选编程与分析练习，读者将有机会亲手实现并验证所学概念，将理论知识转化为解决实际问题的能力。

通过这一结构化的学习路径，本文将为读者在[计算电磁学](@entry_id:265339)领域的深入研究与开发工作奠定坚实的基础。

## 原理与机制

在上一章中，我们介绍了在计算电磁学中使用有限元方法 (FEM) 的基本思想。本章将深入探讨该方法的核心——[单元刚度矩阵](@entry_id:139369)和[质量矩阵](@entry_id:177093)的构建与集成。我们将从麦克斯韦方程的弱形式出发，系统地阐述这些矩阵的定义、计算、集成过程以及它们的物理与数值特性。这些矩阵构成了离散化后代数系统的基础，对其原理的深刻理解是精确高效地求解电磁问题的关键。

### 基本双线性形式：刚度与质量

我们从时谐麦克斯韦方程的[电场](@entry_id:194326)[旋度-旋度方程](@entry_id:748113)出发。在无源区域中，其强形式为：
$$ \nabla \times (\mu^{-1} \nabla \times \mathbf{E}) - \omega^2 \epsilon \mathbf{E} = \mathbf{0} $$
其中 $\mathbf{E}$ 是[电场](@entry_id:194326)强度，$\mu$ 是磁导率，$\epsilon$ 是[介电常数](@entry_id:146714)，$\omega$ 是角频率。

通过[Galerkin方法](@entry_id:260906)，我们将此[偏微分方程](@entry_id:141332)转换为一个[弱形式](@entry_id:142897)或[变分形式](@entry_id:166033)。我们将方程与一个取自适当函数空间（如 $H(\mathrm{curl})$ 空间）的矢量测试函数 $\mathbf{v}$ 做[内积](@entry_id:158127)，并在整个计算域 $\Omega$ 上积分。经过分部积分（使用矢量恒等式 $\nabla \cdot (\mathbf{A} \times \mathbf{B}) = (\nabla \times \mathbf{A}) \cdot \mathbf{B} - \mathbf{A} \cdot (\nabla \times \mathbf{B})$）并应用适当的边界条件（例如，在[理想电导体](@entry_id:753331)边界上，[电场](@entry_id:194326)的切向分量为零），我们得到如下的[弱形式](@entry_id:142897)：寻找 $\mathbf{E} \in H_0(\mathrm{curl};\Omega)$ 使得对于所有测试函数 $\mathbf{v} \in H_0(\mathrm{curl};\Omega)$，
$$ \int_{\Omega} \mu^{-1} (\nabla \times \mathbf{E}) \cdot (\nabla \times \mathbf{v}) \, dV - \omega^2 \int_{\Omega} \epsilon \, \mathbf{E} \cdot \mathbf{v} \, dV = 0 $$

这个方程的核心是两个[双线性形式](@entry_id:746794)：

1.  **刚度[双线性形式](@entry_id:746794)** $a(\mathbf{u}, \mathbf{v})$，它与[磁场能量](@entry_id:267501)有关：
    $$ a(\mathbf{u}, \mathbf{v}) = \int_{\Omega} \mu^{-1} (\nabla \times \mathbf{u}) \cdot (\nabla \times \mathbf{v}) \, dV $$
    从物理上看，[时谐场](@entry_id:755985)存储的平均[磁场能量](@entry_id:267501)为 $U_m = \frac{1}{4} \int_{\Omega} \mu |\mathbf{H}|^2 dV$。利用法拉第定律 $\nabla \times \mathbf{E} = -i\omega\mu\mathbf{H}$，我们可以发现 $a(\mathbf{E}, \mathbf{E})$ 正比于[磁场能量](@entry_id:267501)。

2.  **质量[双线性形式](@entry_id:746794)** $m(\mathbf{u}, \mathbf{v})$，它与[电场能量](@entry_id:193072)有关：
    $$ m(\mathbf{u}, \mathbf{v}) = \int_{\Omega} \epsilon \, \mathbf{u} \cdot \mathbf{v} \, dV $$
    类似地，[时谐场](@entry_id:755985)存储的平均[电场能量](@entry_id:193072)为 $U_e = \frac{1}{4} \int_{\Omega} \epsilon |\mathbf{E}|^2 dV$，因此 $m(\mathbf{E}, \mathbf{E})$ 正比于[电场能量](@entry_id:193072)。

在有限元方法中，我们将场 $\mathbf{E}$ 表示为一组[基函数](@entry_id:170178) $\mathbf{N}_j$ 的[线性组合](@entry_id:154743)：$\mathbf{E} \approx \sum_j e_j \mathbf{N}_j(\mathbf{x})$。将此展开式代入[弱形式](@entry_id:142897)，并选择[基函数](@entry_id:170178)自身作为测试函数（即 $\mathbf{v} = \mathbf{N}_i$），我们得到一个矩阵方程。这个过程的核心是在每个单元（例如，一个四面体或三角形）上计算局部贡献，即**[单元刚度矩阵](@entry_id:139369)** $K^e$ 和**[单元质量矩阵](@entry_id:748930)** $M^e$。其矩阵元定义为：
$$ [K^e]_{ij} = a(\mathbf{N}_j^e, \mathbf{N}_i^e) = \int_{\Omega_e} \mu^{-1} (\nabla \times \mathbf{N}_i^e) \cdot (\nabla \times \mathbf{N}_j^e) \, dV $$
$$ [M^e]_{ij} = m(\mathbf{N}_j^e, \mathbf{N}_i^e) = \int_{\Omega_e} \epsilon \, \mathbf{N}_i^e \cdot \mathbf{N}_j^e \, dV $$
其中 $\mathbf{N}_i^e$ 是在单元 $\Omega_e$ 上的第 $i$ 个[局部基](@entry_id:151573)函数 。

### 参考单元上的离散化

直接在任意形状和大小的物理单元 $\Omega_e$ 上计算上述积分是极其繁琐的。因此，标准做法是引入一个固定的**[参考单元](@entry_id:168425)** $\hat{\Omega}$（例如，单位立方体或单位四面体），并通过一个**[等参映射](@entry_id:173239)** $\mathbf{x} = \Phi_e(\boldsymbol{\xi})$ 将参考单元上的点 $\boldsymbol{\xi}$ 映射到物理单元上的点 $\mathbf{x}$。

为了在[参考单元](@entry_id:168425)上进行计算，我们必须对积分中的所有项进行[坐标变换](@entry_id:172727)。这涉及到三个关键的变换法则：
1.  **体积元变换**：$d V = \det(J) \, d\hat{V}$，其中 $J(\boldsymbol{\xi}) = \frac{\partial \mathbf{x}}{\partial \boldsymbol{\xi}}$ 是映射的**[雅可比矩阵](@entry_id:264467)**。
2.  **基[函数变换](@entry_id:141095)**：对于 $H(\mathrm{curl})$ 空间，矢量[基函数](@entry_id:170178)需要使用保持切向连续性的特殊变换，即**[协变Piola变换](@entry_id:747991)** (covariant Piola transform)。物理[基函数](@entry_id:170178) $\mathbf{N}^e$ 与参考[基函数](@entry_id:170178) $\hat{\mathbf{N}}$ 之间的关系为：
    $$ \mathbf{N}^e(\mathbf{x}(\boldsymbol{\xi})) = J(\boldsymbol{\xi})^{-T} \hat{\mathbf{N}}(\boldsymbol{\xi}) $$
    其中 $J^{-T} = (J^{-1})^T$。
3.  **[旋度算子](@entry_id:184984)变换**：对于服从[协变Piola变换](@entry_id:747991)的矢量场，其[旋度算子](@entry_id:184984)的变换法则为：
    $$ (\nabla_{\mathbf{x}} \times \mathbf{N}^e)(\mathbf{x}(\boldsymbol{\xi})) = \frac{1}{\det J(\boldsymbol{\xi})} J(\boldsymbol{\xi}) (\nabla_{\boldsymbol{\xi}} \times \hat{\mathbf{N}}(\boldsymbol{\xi})) $$

将这些变换规则代入[单元刚度矩阵](@entry_id:139369)的定义中 ，我们得到其在[参考单元](@entry_id:168425)上的计算形式：
$$ [K^e]_{ij} = \int_{\hat{\Omega}_e} \mu^{-1}(\mathbf{x}(\boldsymbol{\xi})) \left( \frac{J (\nabla_{\boldsymbol{\xi}} \times \hat{\mathbf{N}}_i)}{\det J} \right) \cdot \left( \frac{J (\nabla_{\boldsymbol{\xi}} \times \hat{\mathbf{N}}_j)}{\det J} \right) \det J \, d\hat{V} $$
整理后得到：
$$ [K^e]_{ij} = \int_{\hat{\Omega}_e} \mu^{-1}(\mathbf{x}(\boldsymbol{\xi})) \frac{1}{\det J(\boldsymbol{\xi})} (\nabla_{\boldsymbol{\xi}} \times \hat{\mathbf{N}}_i)^T (J(\boldsymbol{\xi})^T J(\boldsymbol{\xi})) (\nabla_{\boldsymbol{\xi}} \times \hat{\mathbf{N}}_j) \, d\hat{V} $$
这个公式是有限元程序中计算[刚度矩阵](@entry_id:178659)的核心。类似地，通过变换法则，[单元质量矩阵](@entry_id:748930)的计算公式为：
$$ [M^e]_{ij} = \int_{\hat{\Omega}_e} \epsilon(\mathbf{x}(\boldsymbol{\xi})) (\hat{\mathbf{N}}_i^T J^{-1} J^{-T} \hat{\mathbf{N}}_j) \det J(\boldsymbol{\xi}) \, d\hat{V} $$
这些积分通常使用数值求积（如高斯求积）来计算。

### 案例研究：最低阶Nédélec单元

为了使上述抽象的公式具体化，我们考察最常用的 $H(\mathrm{curl})$ 单元之一：**最低阶Nédélec（第一类）边元** (Nédélec first-kind edge elements)。其自由度与单元的边相关联。

#### 二维[三角形单元](@entry_id:167871)

在一个顶点为 $\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3$ 的[三角形单元](@entry_id:167871) $T$ 上，我们可以使用**[重心坐标](@entry_id:155488)** $\lambda_1, \lambda_2, \lambda_3$ 来构建[基函数](@entry_id:170178)。与边 $e_k$（由顶点 $i,j$ 构成）相关的[基函数](@entry_id:170178)可以定义为 $\mathbf{N}_k = s_k(\lambda_i \nabla \lambda_j - \lambda_j \nabla \lambda_i)$，其中 $s_k$ 是与边方向相关的符号。

一个关键特性是，对于仿射单元（即顶点[线性映射](@entry_id:185132)构成的单元），[重心坐标](@entry_id:155488)的梯度 $\nabla \lambda_i$ 是常矢量。因此，这些[基函数](@entry_id:170178)的旋度也是常数。例如，对于 $\mathbf{N}_{12} = \lambda_1 \nabla \lambda_2 - \lambda_2 \nabla \lambda_1$，其旋度为 $\nabla \times \mathbf{N}_{12} = 2(\nabla \lambda_1 \times \nabla \lambda_2)$。在二维情况下，这简化为一个标量，其值等于 $\pm 2/A_T$，其中 $A_T$ 是三角形的面积。

**示例计算** 
考虑一个顶点位于 $\mathbf{v}_1=(0,0)$, $\mathbf{v}_2=(2,0)$ 和 $\mathbf{v}_3=(0,3)$ 的[三角形单元](@entry_id:167871)。其面积为 $A_T = 3$。[基函数](@entry_id:170178) $\mathbf{N}_1, \mathbf{N}_2, \mathbf{N}_3$ 分别对应边 (2,3), (3,1), (1,2)（或其某个[排列](@entry_id:136432)）。可以计算出，所有这些[基函数](@entry_id:170178)的旋度大小都是一个常数 $|\nabla \times \mathbf{N}_k| = 2/A_T = 2/3$。假设我们使用[基函数](@entry_id:170178)定义 $\mathbf{N}_1 \equiv \lambda_2\nabla\lambda_3 - \lambda_3\nabla\lambda_2$ 等，并选择边方向使得 $\nabla \times \mathbf{N}_1$ 和 $\nabla \times \mathbf{N}_2$ 均为正值。若介质的磁导率在该单元上为常数 $\mu=1.5$，则[单元刚度矩阵](@entry_id:139369)的非对角元 $K_{12}$ 为：
$$ K_{12} = \int_T \mu^{-1} (\nabla \times \mathbf{N}_1) \cdot (\nabla \times \mathbf{N}_2) \, dA = \frac{1}{1.5} \left(\frac{2}{3}\right) \left(\frac{2}{3}\right) \int_T dA = \frac{1}{1.5} \times \frac{4}{9} \times 3 = \frac{8}{9} \approx 0.8889 $$
这个例子清晰地展示了从[基函数](@entry_id:170178)定义到具体矩阵元值的计算过程。

#### 三维[四面体单元](@entry_id:168311)

同样的概念可以推广到三维。在一个[四面体单元](@entry_id:168311)上，最低阶Nédélec空间有6个[基函数](@entry_id:170178)，每个对应一条边。例如，在单位参考四面体上，其顶点为 $\mathbf{v}_1=(0,0,0), \mathbf{v}_2=(1,0,0), \mathbf{v}_3=(0,1,0), \mathbf{v}_4=(0,0,1)$，边 $(a,b)$ 对应的[基函数](@entry_id:170178)为 $\mathbf{N}_{ab} = \lambda_a \nabla \lambda_b - \lambda_b \nabla \lambda_a$ 。

同样，由于[重心坐标](@entry_id:155488)的梯度是常矢量，这些[基函数](@entry_id:170178)的旋度 $\nabla \times \mathbf{N}_{ab} = 2(\nabla \lambda_a \times \nabla \lambda_b)$ 也是常矢量。这极大地简化了[刚度矩阵](@entry_id:178659)的计算，因为被积函数变为常数，积分值就是该常数乘以单元的体积。

### 材料属性的集成

材料的电磁特性，如[介电常数](@entry_id:146714) $\epsilon$ 和[磁导率](@entry_id:154559) $\mu$，作为权重函数出现在质量和[刚度矩阵](@entry_id:178659)的积分中。

对于**各向同性**材料，$\epsilon$ 和 $\mu$ 是标量函数。如果它们在单元上是常数，就可以被提到积分号外面。如果它们是空间变化的，则需要在数值求积过程中，在每个求积点上计算其值。

对于**各向异性**材料，$\epsilon$ 和/或 $\mu$ 是张量（即矩阵）。这会引入方向耦合。例如，考虑一个具有对角各向异性[介电张量](@entry_id:194185) $\boldsymbol{\epsilon} = \mathrm{diag}(\epsilon_x, \epsilon_y, \epsilon_z)$ 的情况 。[质量矩阵](@entry_id:177093)的定义变为：
$$ [M^e]_{ij} = \int_{\Omega_e} \mathbf{N}_i^T \boldsymbol{\epsilon} \, \mathbf{N}_j \, dV $$
考虑在一个六面体[参考单元](@entry_id:168425)上，两个边 (2,3) 和 (2,4) 对应的[基函数](@entry_id:170178)可以表示为 $\mathbf{N}_{23} = (-y, x, 0)^T$ 和 $\mathbf{N}_{24} = (-z, 0, x)^T$。对角质量项 $M_{23,23}$ 的被积函数为 $\mathbf{N}_{23}^T \boldsymbol{\epsilon} \mathbf{N}_{23} = \epsilon_x y^2 + \epsilon_y x^2$。非对角耦合项 $M_{23,24}$ 的被积函数为 $\mathbf{N}_{23}^T \boldsymbol{\epsilon} \mathbf{N}_{24} = \epsilon_x yz$。

如果介质是各向同性的，即 $\epsilon_x = \epsilon_y = \epsilon_z$，则[质量矩阵](@entry_id:177093)与[基函数](@entry_id:170178)的简单[点积](@entry_id:149019) $\mathbf{N}_i \cdot \mathbf{N}_j$ 成正比。但在各向异性情况下，$\boldsymbol{\epsilon}$ 的不同分量会以不同方式加权[基函数](@entry_id:170178)的不同矢量分量，从而在原本可能正交的方向之间引入耦合。

### 集成过程：从局部到全局

计算出所有单元的局部矩阵 $K^e$ 和 $M^e$ 后，需要将它们**集成** (assemble) 到全局的系统矩阵 $K$ 和 $M$ 中。集成过程本质上是将与同一个全局自由度相关的局部贡献相加。

对于边元，全局自由度与网格中的每条边相关联。集成过程中的一个关键且微妙之处在于处理**边的方向** 。通常，我们会为网格中的每条全局边定义一个唯一的全局方向（例如，从索引号较小的顶点指向索引号较大的顶点）。然而，在每个单元内部，[局部基](@entry_id:151573)函数也与一个局部边的方向相关。

当一个单元的局部边方向与对应的全局边方向一致时，其贡献直接相加。当方向相反时，必须引入一个符号因子。具体来说，[局部基](@entry_id:151573)函数 $\mathbf{N}^e_l$ 与[全局基函数](@entry_id:749917) $\mathbf{W}_g$ 的关系是 $\left. \mathbf{W}_{g_l}(\mathbf{x}) \right|_{\Omega_e} = s_l \mathbf{N}^e_l(\mathbf{x})$，其中 $s_l \in \{+1, -1\}$ 是方向符号（+1代表方向相同，-1代表相反）。因此，将局部矩阵元 $(K^e)_{lm}$ 添加到全局矩阵的 $(g_l, g_m)$ 位置时，必须乘以符号因子 $s_l s_m$。
$$ K_{g_l, g_m} \leftarrow K_{g_l, g_m} + s_l s_m (K^e)_{lm} $$
对质量矩阵也应用相同的规则。

**集成示例** 
考虑一个由两个共享面 $(1,2,3)$ 的四面体 $T_1=(0,1,2,3)$ 和 $T_2=(1,2,3,4)$ 组成的简单网格。我们想计算与全局边 $(1,2)$ 相关的全局矩阵对角元 $A_{g,g} = K_{g,g} - \omega^2 M_{g,g}$。这个全局自由度从两个单元获得贡献：$T_1$ 中的局部边 $(1,2)$ 和 $T_2$ 中的局部边 $(1,2)$。假设全局方向和两个局部方向都定义为从顶点1到顶点2，则两个方向符号都为+1。因此，全局对角元就是两个局部对角元的直接相加：
$$ K_{g,g} = K^{(T_1)}_{e_{12},e_{12}} + K^{(T_2)}_{e_{12},e_{12}} $$
$$ M_{g,g} = M^{(T_1)}_{e_{12},e_{12}} + M^{(T_2)}_{e_{12},e_{12}} $$
通过对每个四面体进行详细计算，我们可以得到这两个局部贡献，并将它们相加以获得最终的全局[矩阵元](@entry_id:186505)。

### 集成矩阵的属性

集成后的全局矩阵 $K$ 和 $M$ 具有重要的数学和物理特性，这些特性直接影响到求解的稳定性和准确性 。

-   **[质量矩阵](@entry_id:177093) M**: 由于 $\epsilon > 0$ 且[基函数](@entry_id:170178)是[线性无关](@entry_id:148207)的，质量双线性形式 $m(\mathbf{u}, \mathbf{u}) = \int \epsilon |\mathbf{u}|^2 dV$ 是一个[内积](@entry_id:158127)。因此，**质量矩阵 $M$ 是[对称正定](@entry_id:145886)的 (Symmetric Positive Definite, SPD)**。

-   **刚度矩阵 K**: 刚度双线性形式 $a(\mathbf{u}, \mathbf{u}) = \int \mu^{-1} |\nabla \times \mathbf{u}|^2 dV$ 总是非负的。然而，如果存在一个非[零场](@entry_id:199169) $\mathbf{u}$ 使得 $\nabla \times \mathbf{u} = \mathbf{0}$，则 $a(\mathbf{u}, \mathbf{u}) = 0$。这种[无旋场](@entry_id:183486)（即[梯度场](@entry_id:264143) $\mathbf{u} = \nabla \phi$）构成了[旋度算子](@entry_id:184984)的**核 (kernel)**。由于标准的Nédélec单元空间包含了非平凡的梯度场[子空间](@entry_id:150286)，**[刚度矩阵](@entry_id:178659) $K$ 只是对称半正定的 (Symmetric Positive Semidefinite, SPSD)**。

$K$ 的非平凡核空间是FEM求解麦克斯韦方程时产生**伪模** (spurious modes) 的根源。在求解[特征值问题](@entry_id:142153) $K \mathbf{e} = \lambda M \mathbf{e}$ 时，这些对应于 $K$ 的核的模式会导致大量的、非物理的零（或接近零）[特征值](@entry_id:154894)，污染物理谱。

### 高级主题与实践考量

#### 散度惩罚

为了处理由刚度矩阵的核引起的伪模问题，一种常用的技术是**散度惩罚** (divergence penalty) 。物理上，在无源区域中，[电场](@entry_id:194326)应满足高斯定律 $\nabla \cdot (\epsilon \mathbf{E}) = 0$。我们可以将这个约束弱形式地加入到原始的[变分问题](@entry_id:756445)中，形成一个增广的[双线性形式](@entry_id:746794)：
$$ a_{aug}(\mathbf{u}, \mathbf{v}) = a(\mathbf{u}, \mathbf{v}) + \alpha \int_{\Omega} (\nabla \cdot (\epsilon \mathbf{u})) (\nabla \cdot (\epsilon \mathbf{v})) \, dV $$
其中 $\alpha > 0$ 是一个用户选择的惩罚参数。

-   **对伪模的影响**：对于一个属于 $K$ 的核的伪模 $\mathbf{u}_h = \nabla \phi_h$，其 $a(\mathbf{u}_h, \mathbf{u}_h) = 0$。然而，除非 $\nabla \cdot (\epsilon \nabla \phi_h) = 0$，其惩罚项将为正。这使得增广的[刚度矩阵](@entry_id:178659) $K_{aug} = K + \alpha G$（其中 $G$ 是来自惩罚项的矩阵）在该模式下不再为零。其对应的[特征值](@entry_id:154894)会从零被“提升”到 $\mathcal{O}(\alpha)$ 的量级，从而将伪模与物理模式在[频谱](@entry_id:265125)上分开。
-   **对物理模式的影响**：对于满足 $\nabla \cdot (\epsilon \mathbf{E}) = 0$ 的理想物理模式，惩罚项为零，因此理论上不影响物理[特征值](@entry_id:154894)。在离散情况下，由于数值误差，物理模式的散度可能不完全为零（即存在“散度缺陷”），惩罚项会引入微小的扰动，但此扰动会随着网格加密而减小。
-   **参数选择**：$\alpha$ 的选择是一个权衡。太小则无法有效分离伪模；太大则可能导致[增广矩阵](@entry_id:150523)的**条件数**恶化，给[线性系统](@entry_id:147850)的求解带来数值困难。

#### 质量矩阵集总

在时域瞬态仿真中，常使用[显式时间步进](@entry_id:168157)算法（如[蛙跳法](@entry_id:751210)）。这需要每一步求解一个形如 $M \mathbf{a}^{n+1} = \mathbf{f}$ 的线性系统。如果使用标准的**[一致质量矩阵](@entry_id:174630)** (consistent mass matrix) $M$（它是稀疏但非对角的），这一步就需要一个[线性求解器](@entry_id:751329)，成本高昂。

为了规避这个问题，可以使用**[集总质量矩阵](@entry_id:173011)** (lumped mass matrix) $M_L$ 。$M_L$ 是 $M$ 的一个[对角近似](@entry_id:270948)，通常通过“行和”方法（将每行的非对角元素加到对角元上）或其他基于特殊求积点的方法构造。使用 $M_L$ 后，求解 $M_L \mathbf{a}^{n+1} = \mathbf{f}$ 就变成了一个简单的逐点除法，大大提高了[计算效率](@entry_id:270255)。

-   **谱等价性**：尽管集总改变了矩阵，但对于标准的有限元和合适的集总方案，可以证明 $M_L$ 和 $M$ 是**谱等价**的。这意味着它们的最大和最小特征值具有相同的[数量级](@entry_id:264888)和随网格尺寸 $h$ 变化的趋势。
-   **稳定性**：由于谱等价性，使用 $M_L$ 的[显式时间步进](@entry_id:168157)格式的稳定性条件（如[CFL条件](@entry_id:178032)）与使用 $M$ 的格式具有相同的渐近行为，仅相差一个与网格无关的常数因子。
-   **对边元的挑战**：值得注意的是，为[Nédélec边元](@entry_id:275164)设计保持收敛阶的有效集总方案比为标准的拉格朗日节点元要困难得多 。因此，在实践中，边元的质量集总需要更谨慎的处理。

#### [曲边单元](@entry_id:748117)与[数值求积](@entry_id:136578)

当使用[高阶单元](@entry_id:750328)来模拟弯曲的几何边界或接口时，从[参考单元](@entry_id:168425)到物理单元的映射 $\mathbf{x}(\boldsymbol{\xi})$ 不再是仿射的（即 $p_m > 1$）。这对[数值求积](@entry_id:136578)提出了新的挑战 。

-   **仿射情况** ($p_m = 1$)：雅可比矩阵 $J$ 是常数。质量和刚度矩阵的被积函数都是 $\boldsymbol{\xi}$ 的多项式。其次数由[基函数](@entry_id:170178)的次数决定。例如，对于次数为 $r$ 的标量[拉格朗日基](@entry_id:751105)函数，质量矩阵被积函数的次数为 $2r$，[刚度矩阵](@entry_id:178659)被积函数的次数为 $2(r-1)$。我们可以选择一个能精确积分这些多项式的[高斯求积法](@entry_id:146011)则。

-   **非仿射情况** ($p_m > 1$)：[雅可比矩阵](@entry_id:264467) $J$ 不再是常数，而是 $\boldsymbol{\xi}$ 的多项式函数。
    -   对于**标量[质量矩阵](@entry_id:177093)**，被积函数 $\hat{N}_i \hat{N}_j \det(J)$ 仍然是多项式，但其次数现在也依赖于映射的次数 $p_m$ 和维度 $d$，通常为 $2r + d(p_m-1)$。需要更高阶的求积法则才能精确积分。
    -   对于**标量刚度矩阵**和**矢量质量/[刚度矩阵](@entry_id:178659)**（使用[Piola变换](@entry_id:163790)），情况更为复杂。被积函数中出现了 $J^{-1}$ 项。由于 $J^{-1} = \frac{\mathrm{adj}(J)}{\det(J)}$，被积函数变成了**[有理函数](@entry_id:154279)**（多项式除以多项式），而不再是多项式。这意味着标准的[高斯求积法](@entry_id:146011)则无法再“精确”地计算积分。在这种情况下，必须使用足够高阶的[求积法则](@entry_id:753909)来确保[积分误差](@entry_id:171351)不会破坏有限元方法的整体收敛精度。

综上所述，单元刚度与质量矩阵的构建是有限元方法在电磁学中应用的技术核心。从基本定义到考虑材料、几何和[数值稳定性](@entry_id:146550)等实际因素，每一步都蕴含着深刻的物理原理和数学机制。对这些细节的掌握是成为一名合格的计算科学家或工程师的必经之路。