## 引言
[非共线磁性](@entry_id:181233)，即材料中[原子磁矩](@entry_id:173739)不相互平行或反平行的[排列](@entry_id:136432)方式，是现代凝聚态物理与[材料科学](@entry_id:152226)的前沿领域。它孕育了诸如自旋螺旋、斯格明子（[Skyrmions](@entry_id:141088)）等复杂的[磁织构](@entry_id:751636)，这些不仅带来了新奇的物理现象，也为下一代高密度、低[功耗](@entry_id:264815)的自旋电子学器件提供了巨大的应用潜力。然而，准确预测和理解这些复杂磁结构的形成机理与稳定性，对理论计算提出了巨大挑战，超越了传统共线磁性计算的范畴。因此，建立一个能够从第一性原理出发，精确描述和模拟[非共线磁性](@entry_id:181233)的计算框架至关重要。

本篇文章旨在系统性地介绍[非共线磁性](@entry_id:181233)的第一性原理计算方法。我们将带领读者深入探索这一强大工具的理论核心与实际应用，弥合微观量子力学与宏观磁现象之间的鸿沟。文章分为三个核心部分：首先，在“原理与机制”一章中，我们将奠定坚实的理论基础，详细阐述非共线[自旋密度泛函理论](@entry_id:755223)、自旋轨道耦合的角色以及对称性在其中扮演的关键作用。接着，在“应用与[交叉](@entry_id:147634)学科关联”一章中，我们将展示如何应用这些原理来参数化有效模型、预测实验可观测的物理量（如[拓扑霍尔效应](@entry_id:138853)），并揭示其与[材料科学](@entry_id:152226)、自旋电子学等领域的深刻联系。最后，通过“动手实践”部分提供的具体计算问题，读者将有机会巩固所学知识，掌握核心的计算技巧。通过这一系列的学习，读者将能够全面理解如何运用第一性原理计算来探索和设计新奇的[非共线磁性](@entry_id:181233)材料。

## 原理与机制

在深入探讨[非共线磁性](@entry_id:181233)的[第一性原理计算](@entry_id:198754)细节之前，我们必须首先建立一个坚实的理论基础。本章旨在系统地阐述描述和计算[非共线磁性](@entry_id:181233)结构所需的核心原理与关键机制。我们将从密度泛函理论（DFT）框架下的基本物理量出发，逐步揭示交换关联相互作用、[自旋轨道](@entry_id:274032)耦合（SOC）以及拓扑学在塑造复杂[磁织构](@entry_id:751636)中的作用。

### 非共线[自旋密度泛函理论](@entry_id:755223)的基本变量

在传统的共线磁性计算中，系统在任意点的磁化方向都沿着一个全局的[自旋量子化](@entry_id:197800)轴（通常是 $\hat{\mathbf{z}}$ 轴）。这种情况下，电子系统可以用两个独立的标量场来完全描述：总电子密度 $n(\mathbf{r})$ 和[自旋极化](@entry_id:164038)密度 $m_z(\mathbf{r}) = n_\uparrow(\mathbf{r}) - n_\downarrow(\mathbf{r})$。然而，对于[非共线磁性](@entry_id:181233)系统，磁化方向在空间中是连续变化的，因此我们需要一个矢量场——**磁化密度矢量** $\mathbf{m}(\mathbf{r})$——来描述局域的磁矩大小和方向。

为了在量子力学框架内严谨地定义这些量，非共线[自旋密度泛函理论](@entry_id:755223)（spin-DFT）引入了 $2 \times 2$ 的**局域自旋密度矩阵** $\rho_{\alpha\beta}(\mathbf{r})$ 作为其核心变量。这个矩阵是从系统的 Kohn-Sham (KS) [旋量](@entry_id:158054)[轨道](@entry_id:137151) $\Psi_n(\mathbf{r})$ 构建的。每个KS[轨道](@entry_id:137151)本身就是一个二维旋量，可以表示为：
$$
\Psi_n(\mathbf{r}) = \begin{pmatrix} \Psi_{n\uparrow}(\mathbf{r}) \\ \Psi_{n\downarrow}(\mathbf{r}) \end{pmatrix}
$$
其中 $\Psi_{n\alpha}(\mathbf{r})$ 是[旋量](@entry_id:158054)的分量。给定一组占据数为 $f_n$ 的KS[轨道](@entry_id:137151)，局域自旋密度矩阵定义为：
$$
\rho_{\alpha\beta}(\mathbf{r}) \equiv \sum_{n} f_{n} \Psi_{n\beta}(\mathbf{r}) \Psi_{n\alpha}^{*}(\mathbf{r})
$$
这个矩阵是一个 Hermitian 矩阵，它包含了描述电子系统所需的所有局域信息。总电子密度 $n(\mathbf{r})$ 和磁化密度矢量 $\mathbf{m}(\mathbf{r})$ 可以通过对该矩阵取迹得到。总电子密度是该[矩阵的迹](@entry_id:139694)：
$$
n(\mathbf{r}) = \mathrm{Tr}[\rho(\mathbf{r})] = \rho_{\uparrow\uparrow}(\mathbf{r}) + \rho_{\downarrow\downarrow}(\mathbf{r})
$$
磁化密度矢量则通过泡利矩阵 $\boldsymbol{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$ 来提取，其定义为（在没有自旋轨道耦合和外[磁场](@entry_id:153296)的情况下）：
$$
\mathbf{m}(\mathbf{r}) \equiv -\mu_{B} \mathrm{Tr}[\boldsymbol{\sigma} \rho(\mathbf{r})]
$$
其中 $\mu_B$ 是[玻尔磁子](@entry_id:151037)。这个表达式将磁化密度的三个分量 $m_x, m_y, m_z$ 与密度矩阵的四个元素联系起来。

为了具体理解这些定义如何运作，我们可以考虑一个假设性的例子 [@problem_id:3468681]。假设在空间中的某一点 $\mathbf{r}_0$，我们有两个占据的KS[旋量](@entry_id:158054)[轨道](@entry_id:137151) $\Psi_1$ 和 $\Psi_2$。通过计算每个[轨道](@entry_id:137151)对密度矩阵的贡献 $\rho_n = f_n \Psi_n \Psi_n^\dagger$，然后将它们相加得到总的密度矩阵 $\rho(\mathbf{r}_0)$。一旦我们得到了 $\rho(\mathbf{r}_0)$ 的 $2 \times 2$ [矩阵元](@entry_id:186505)素，我们就可以通过与[泡利矩阵](@entry_id:139493)相乘并取迹，直接计算出[磁化矢量](@entry_id:180304)的三个笛卡尔分量 $(m_x, m_y, m_z)$。例如，$m_z = -\mu_B (\rho_{\uparrow\uparrow} - \rho_{\downarrow\downarrow})$，$m_x = -\mu_B (\rho_{\uparrow\downarrow} + \rho_{\downarrow\uparrow})$，以及 $m_y = -i\mu_B (\rho_{\uparrow\downarrow} - \rho_{\downarrow\uparrow})$。这个过程清晰地展示了宏观的[磁化矢量](@entry_id:180304)是如何从微观的电子[旋量](@entry_id:158054)[波函数](@entry_id:147440)中涌现出来的。

相应地，Kohn-Sham 有效势在非共线表述中也变成一个 $2 \times 2$ 的矩阵算符，通常可以写为：
$$
V_{\mathrm{KS}}(\mathbf{r}) = v_{\mathrm{eff}}(\mathbf{r}) I + \mathbf{B}_{\mathrm{eff}}(\mathbf{r}) \cdot \boldsymbol{\sigma}
$$
其中 $I$ 是 $2 \times 2$ 单位矩阵，$v_{\mathrm{eff}}(\mathbf{r})$ 是标量有效势，而 $\mathbf{B}_{\mathrm{eff}}(\mathbf{r})$ 是一个等效的**有效磁场**或交换场。这个场与电子自旋耦合，其方向和大小在空间中变化，从而稳定了非共线的[磁结构](@entry_id:201216)。

### 从微观密度到宏观磁矩的表征

磁化密度 $\mathbf{m}(\mathbf{r})$ 是一个连续的矢量场，为我们提供了最精细的磁性描述。然而，在分析晶体材料的磁性时，将这种连续描述简化为一组离散的、与原子位置相关的**局域磁矩** $\mathbf{M}_i$ 通常更为直观和有用。这可以通过在每个原子周围定义的积分体积 $\Omega_i$（例如 Voronoi 胞或球形积分区域）内对磁化密度进行积分来实现：
$$
\mathbf{M}_{i} = \int_{\Omega_{i}} \mathbf{m}(\mathbf{r}) \, d^{3} r
$$
这样，一个复杂的[磁织构](@entry_id:751636)就可以被看作是[晶格](@entry_id:196752)上每个位置 $i$ 处的一个矢量 $\mathbf{M}_i$ 的集合。

一旦我们有了一组[局域磁矩](@entry_id:138106) $\{\mathbf{M}_i\}$，我们就可以对磁结构的非[共线性](@entry_id:270224)进行量化表征。一个最直接的、具有物理意义的非[共线性](@entry_id:270224)度量是相邻磁矩之间的夹角。为了构建一个不依赖于[坐标系](@entry_id:156346)选择的、具有[旋转不变性](@entry_id:137644)的标量度量，我们可以计算代表磁矩方向的单位矢量 $\mathbf{n}_i = \mathbf{M}_i / |\mathbf{M}_i|$ 之间的[点积](@entry_id:149019) [@problem_id:3468679]。两个单位矢量 $\mathbf{n}_i$ 和 $\mathbf{n}_j$ 之间的夹角 $\theta_{ij}$ 可以通过它们[点积](@entry_id:149019)的反余弦得到：
$$
\theta_{ij} = \arccos(\mathbf{n}_i \cdot \mathbf{n}_j)
$$
$\theta_{ij} = 0$ 对应[铁磁性](@entry_id:137256)（FM）[排列](@entry_id:136432)，$\theta_{ij} = \pi$ 对应反铁磁性（AFM）[排列](@entry_id:136432)，而任何介于两者之间的值都表示非共线[排列](@entry_id:136432)。

为了得到一个描述整个系统非共线程度的单一标量，我们可以对所有近邻键上的夹角进行平均。如果我们用 $B$ 表示所有近邻键 $(i,j)$ 的集合，用 $N_b$ 表示键的总数，那么**键平均非共线性度** $\Theta_{NC}$ 可以定义为：
$$
\Theta_{NC} = \frac{1}{N_b} \sum_{(i,j) \in B} \theta_{ij} = \frac{1}{N_b} \sum_{(i,j) \in B} \arccos(\mathbf{n}_i \cdot \mathbf{n}_j)
$$
这个量提供了一个简洁而强大的工具，用于比较不同非共线结构的“扭曲”程度。例如，在一个假想的由四个原子组成的方形团簇中，给定每个原子上的磁矩矢量，我们可以依次计算每条边上相邻磁矩的夹角，然后取其算术平均值，从而得到一个表征该团簇整体非共线性的数值 [@problem_id:3468679]。

### 交换关联泛函的角色与对称性约束

在[自旋密度泛函理论](@entry_id:755223)中，交换关联（XC）能 $E_{\mathrm{xc}}[n, \mathbf{m}]$ 是决定系统[磁基态](@entry_id:142500)的核心。XC势（包括标量部分 $v_{\mathrm{xc}}$ 和矢量场部分 $\mathbf{B}_{\mathrm{xc}}$）是通过对 XC 能进行泛函求导得到的：
$$
v_{\mathrm{xc}}(\mathbf{r}) = \frac{\delta E_{\mathrm{xc}}}{\delta n(\mathbf{r})}, \quad \mathbf{B}_{\mathrm{xc}}(\mathbf{r}) = \frac{\delta E_{\mathrm{xc}}}{\delta \mathbf{m}(\mathbf{r})}
$$
在没有自旋轨道耦合的情况下，[多电子哈密顿量](@entry_id:164643)在自旋空间中具有全局[旋转不变性](@entry_id:137644)。这意味着，如果我们将系统中的所有自旋都绕同一个轴旋转同一个角度，系统的总能量应该保持不变。这个[基本对称性](@entry_id:161256)对 XC 泛函的形式施加了严格的约束。

考虑一个无穷小的全局自旋旋转，它使磁化密度发生变化 $\delta \mathbf{m}(\mathbf{r}) = \boldsymbol{\theta} \times \mathbf{m}(\mathbf{r})$，其中 $\boldsymbol{\theta}$ 是一个[无穷小旋转](@entry_id:166635)矢量。由于能量不变，$\delta E_{\mathrm{xc}}$ 必须为零。这导出了一个重要的结论，即**零力矩定理** [@problem_id:3468674]：
$$
\int \mathbf{m}(\mathbf{r}) \times \mathbf{B}_{\mathrm{xc}}(\mathbf{r}) \, d^3 r = \mathbf{0}
$$
这个定理表明，由交换关联相互作用产生的[总自旋](@entry_id:153335)力矩必须为零。然而，这并不意味着局域的 XC 力矩密度 $\boldsymbol{\tau}_{\mathrm{xc}}(\mathbf{r}) = \mathbf{m}(\mathbf{r}) \times \mathbf{B}_{\mathrm{xc}}(\mathbf{r})$ 在每一点都必须为零。

不同的 XC 泛函近似以不同的方式满足这个约束：

*   **局域[自旋密度](@entry_id:267742)近似 (LSDA)**：在 LSDA 中，XC 能密度在 $\mathbf{r}$ 点的值仅取决于该点的电子密度 $n(\mathbf{r})$ 和磁化密度的大小 $|\mathbf{m}(\mathbf{r})|$。因此，$E_{\mathrm{xc}}^{\mathrm{LSDA}} = \int e_{\mathrm{xc}}^{\mathrm{unif}}(n(\mathbf{r}), |\mathbf{m}(\mathbf{r})|) \, d^3 r$。对这个泛函求导可以发现，$\mathbf{B}_{\mathrm{xc}}^{\mathrm{LSDA}}(\mathbf{r})$ 总是与 $\mathbf{m}(\mathbf{r})$ 平行。这意味着局域 XC 力矩处处为零：$\boldsymbol{\tau}_{\mathrm{xc}}(\mathbf{r}) = \mathbf{0}$。虽然这满足了零力矩定理，但它无法描述某些由梯度效应驱动的非共线结构。

*   **[广义梯度近似 (GGA)](@entry_id:140295)**：GGA 泛函除了依赖于 $n$ 和 $|\mathbf{m}|$ 外，还依赖于它们的梯度。为了保持自旋[旋转不变性](@entry_id:137644)，一个正确的非共线 GGA 泛函必须通过[旋转不变量](@entry_id:170459)（如 $|\nabla n|^2, |\mathbf{m}|, |\nabla\mathbf{m}|^2 \equiv \sum_{i,\alpha} (\partial_i m_\alpha)^2$）来构建 [@problem_id:3468674]。由于包含了梯度项，$\mathbf{B}_{\mathrm{xc}}^{\mathrm{GGA}}(\mathbf{r})$ 的方向通常不再与 $\mathbf{m}(\mathbf{r})$ 平行，导致局域 XC 力矩 $\boldsymbol{\tau}_{\mathrm{xc}}(\mathbf{r})$ 可以不为零。这对于正确描述平滑变化的[磁织构](@entry_id:751636)（如自旋螺旋）至关重要。尽管局域力矩非零，但通过恰当的构造，泛函仍然可以满足全局零力矩定理。

### [磁各向异性](@entry_id:138218)的起源：[自旋轨道](@entry_id:274032)耦合

到目前为止，我们讨论的物理都基于一个没有自旋轨道耦合（SOC）的[哈密顿量](@entry_id:172864)。在这种情况下，系统的总能量仅依赖于各个[自旋磁矩](@entry_id:272337)之间的相对取向，而与它们相对于[晶格](@entry_id:196752)的整体取向无关。换句话说，将整个[磁结构](@entry_id:201216)作为一个刚体在自旋空间中任意旋转，系统的能量不会改变。这可以通过一个简单的[紧束缚模型](@entry_id:143446)清晰地展示出来：在没有 SOC 的情况下（即 SOC 强度 $\lambda=0$），对所有局域自旋方向 $\mathbf{n}_i$ 应用一个全局旋转 $R$，即 $\mathbf{n}_i \to R\mathbf{n}_i$，计算得到的总能量（[本征值](@entry_id:154894)之和）将保持严格不变 [@problem_id:3468722]。

然而，真实材料中的磁矩通常会指向某些特定的[晶体学](@entry_id:140656)方向，这种现象被称为**[磁晶各向异性](@entry_id:144488)**。将磁矩从这些“易轴”方向偏转需要能量，这个能量就是**[磁晶各向异性](@entry_id:144488)（MAE）**。这种将自旋方向“钉扎”到[晶格](@entry_id:196752)上的相互作用，其微观起源正是**自旋轨道耦合（SOC）**。

SOC 是一种相对论效应，它耦合了电子的自旋角动量和其在[原子核](@entry_id:167902)[电场](@entry_id:194326)中运动所产生的[轨道角动量](@entry_id:191303)。由于轨道角动量的[空间分布](@entry_id:188271)是由[晶格](@entry_id:196752)的对称性决定的，SOC 就充当了自旋与[晶格](@entry_id:196752)之间的桥梁。当 SOC 被引入[哈密顿量](@entry_id:172864)后（$\lambda \neq 0$），上述的全局自旋[旋转不变性](@entry_id:137644)就被打破了。再次对所有自旋方向进行旋转，总能量将会发生改变，这个能量变化即反映了 MAE [@problem_id:3468722]。

除了产生单离子各向异性（即单个离子的磁矩倾向于指向特定方向）外，SOC 在非共线磁体中还能催生更奇特的相互作用。其中最著名的是**Dzyaloshinskii-Moriya 相互作用 (DMI)**，这是一种反对称的交换作用，形式为 $E_{\mathrm{DM}} = \mathbf{D}_{ij} \cdot (\mathbf{S}_i \times \mathbf{S}_j)$。DMI 倾向于使相邻的自旋呈一定的倾斜角（canting），而不是完全平行或反平行。其微观根源在于，当存在[非共线磁性](@entry_id:181233)时，SOC 可以通过二阶微扰过程混合不同的电子态，从而导致能量的降低或升高。在一个简化的双态模型中，可以证明由 SOC 引起的一阶微扰[能量修正](@entry_id:198270)为零，但[二阶修正](@entry_id:199233)正比于 SOC 矩阵元模的平方，即 $|\langle n| H_{\text{SOC}} |m \rangle|^2$。如果这个[矩阵元](@entry_id:186505)本身依赖于自旋倾角 $\theta$（例如，正比于 $\sin\theta$），那么 SOC 就会引入一个与非共线构型相关的能量项，从而可能稳定特定的非共线[基态](@entry_id:150928) [@problem_id:3468660]。

需要注意的是，体系的能量对磁构型旋转的依赖性可能有两个来源。即使没有 SOC，改变非共线结构（例如，改变其相对于[晶格](@entry_id:196752)的旋转）也可能通过改变[电子能带](@entry_id:175335)的杂化而导致能量变化。然而，只有当 SOC 存在时，才会出现与[晶格](@entry_id:196752)轴相关的、真正的[磁晶各向异性](@entry_id:144488) [@problem_id:3468697]。因此，在分析 MAE 时，将 SOC 的贡献与其他效应分离开来是理解其物理本质的关键。

### 连接第一性原理与模型[哈密顿量](@entry_id:172864)

尽管第一性原理的 DFT 计算功能强大，能够从头预测材料的磁性，但对于模拟大尺度[磁织构](@entry_id:751636)或磁动力学过程而言，其计算成本往往过高。在这种情况下，一个非常有效的研究策略是使用高精度的 DFT 计算来为更简洁的经典或量[子模](@entry_id:148922)型[哈密顿量](@entry_id:172864)提供参数。

一个广泛使用的模型是**广义[海森堡哈密顿量](@entry_id:146333)**，它可以包含多种[相互作用项](@entry_id:637283)。