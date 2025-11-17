## 引言
在原子尺度的模拟中，我们长期面临一个两难选择：是选择精度高但计算成本巨大的[量子化学](@entry_id:140193)方法，还是选择速度快但精度和普适性有限的[经典力场](@entry_id:747367)？[神经网络势能面](@entry_id:184102)（[NN-PES](@entry_id:184102)）作为一种前沿的机器学习方法，正是在这一挑战中应运而生。它旨在构建一个能够以接近[量子化学](@entry_id:140193)的精度来描述原子间相互作用的数学模型，同时保持与[经典力场](@entry_id:747367)相媲美的[计算效率](@entry_id:270255)，从而彻底改变我们模拟和理解复杂化学与材料体系的能力。

本文将系统地引导您进入[NN-PES](@entry_id:184102)的世界。在第一章“原理与机制”中，我们将从第一性原理出发，揭示[势能面](@entry_id:147441)的物理本质及其必须遵守的基本对称性，并探讨现代[神经网络架构](@entry_id:637524)如何巧妙地将这些物理约束融入其设计之中。接着，在第二章“应用与跨学科连接”中，我们将展示[NN-PES](@entry_id:184102)如何在化学、物理和[材料科学](@entry_id:152226)等多个领域大放异彩，从揭示[反应机理](@entry_id:149504)到预测材料的宏观性质。最后，在第三章“动手实践”中，将通过具体的计算问题，帮助您巩固对核心概念的理解。

通过这三个章节的学习，您将不仅掌握[NN-PES](@entry_id:184102)的理论基础，还能领会其在解决前沿科学问题中的巨大潜力，并为进一步的深入研究打下坚实的基础。

## 原理与机制

本章旨在深入阐述[神经网络势能面](@entry_id:184102)（[NN-PES](@entry_id:184102)）的核心科学原理与作用机制。我们将从量子力学的第一性原理出发，系统地建立[势能面](@entry_id:147441)的概念，探讨其必须遵循的基本物理对称性，并在此基础上，详细介绍为满足这些要求而设计的各类[神经网络架构](@entry_id:637524)。最后，我们将讨论这些模型的训练方法及其在[计算效率](@entry_id:270255)和数据效率方面的优势。

### [势能面](@entry_id:147441)的基本概念

#### 玻恩–奥本海默近似与[势能面](@entry_id:147441)

在[分子量子力学](@entry_id:203843)中，一个包含 $N$ 个[原子核](@entry_id:167902)和若干电子的孤立分子的完整（非相对论）[哈密顿量](@entry_id:172864)可以写为：

$$ \hat{H} = \hat{T}_N + \hat{T}_e + \hat{V}_{NN} + \hat{V}_{ee} + \hat{V}_{Ne} $$

其中，$\hat{T}_N$ 和 $\hat{T}_e$ 分别是[原子核](@entry_id:167902)与电子的[动能算符](@entry_id:265633)，而 $\hat{V}_{NN}$、$\hat{V}_{ee}$ 和 $\hat{V}_{Ne}$ 则分别代表[原子核](@entry_id:167902)-[原子核](@entry_id:167902)、电子-电子以及[原子核](@entry_id:167902)-电子之间的[库仑相互作用](@entry_id:747947)势。由于[原子核](@entry_id:167902)的质量远大于电子（通常超过三个[数量级](@entry_id:264888)），其运动速度也远慢于电子。这使得我们可以采用**玻恩–奥本海默（Born-Oppenheimer, BO）近似**。

该近似的核心思想是“[钳定原子核](@entry_id:169539)”，即在任意给定的[原子核](@entry_id:167902)构型 $\lbrace\mathbf{R}_I\rbrace$下，将[原子核](@entry_id:167902)视为静止的[电荷](@entry_id:275494)点，从而求解电子在此时的运动状态。这允许我们将完整的[哈密顿量分离](@entry_id:192546)为一个依赖于[原子核](@entry_id:167902)坐标 $\lbrace\mathbf{R}_I\rbrace$ 的参数化[电子哈密顿量](@entry_id:177588) $\hat{H}_{el}$ 和[原子核](@entry_id:167902)[动能算符](@entry_id:265633) $\hat{T}_N$：

$$ \hat{H} = \hat{T}_N + \hat{H}_{el}(\lbrace\mathbf{R}_I\rbrace) $$

其中，[电子哈密顿量](@entry_id:177588)为：

$$ \hat{H}_{el}(\lbrace\mathbf{R}_I\rbrace) = \hat{T}_e + \hat{V}_{ee} + \hat{V}_{Ne}(\lbrace\mathbf{r}_i\rbrace; \lbrace\mathbf{R}_I\rbrace) + V_{NN}(\lbrace\mathbf{R}_I\rbrace) $$

这里，$V_{NN}$ 是[原子核](@entry_id:167902)间的经典[静电排斥](@entry_id:162128)能。对于每一个固定的[原子核](@entry_id:167902)构型 $\lbrace\mathbf{R}_I\rbrace$，我们可以求解相应的定态[电子薛定谔方程](@entry_id:177999)：

$$ \hat{H}_{el}(\lbrace\mathbf{R}_I\rbrace) \Psi_k(\lbrace\mathbf{r}_i\rbrace; \lbrace\mathbf{R}_I\rbrace) = E_k(\lbrace\mathbf{R}_I\rbrace) \Psi_k(\lbrace\mathbf{r}_i\rbrace; \lbrace\mathbf{R}_I\rbrace) $$

该方程的解是一系列绝热电子态 $\lbrace\Psi_k\rbrace$ 及其对应的[能量本征值](@entry_id:144381) $\lbrace E_k \rbrace$。其中，最低的[能量本征值](@entry_id:144381) $E_0(\lbrace\mathbf{R}_I\rbrace)$ 被定义为电子基态的**玻恩–奥本海默[势能面](@entry_id:147441)（Potential Energy Surface, PES）**。它是一个仅依赖于[原子核](@entry_id:167902)坐标的[标量场](@entry_id:151443)，描述了在电子保持[基态](@entry_id:150928)时，[原子核](@entry_id:167902)间相互作用的[有效势能](@entry_id:171609) [@problem_id:2908409]。

根据变分原理，基态能量 $E_0(\lbrace\mathbf{R}_I\rbrace)$ 是通过在所有满足[泡利不相容原理](@entry_id:141850)（即对电子坐标反对称）的电子波[函数空间](@entry_id:143478)中，最小化[电子哈密顿量](@entry_id:177588)的[瑞利商](@entry_id:137794)（Rayleigh quotient）得到的。这为使用高精度的从头计算方法（ab initio methods）来获得 $E_0(\lbrace\mathbf{R}_I\rbrace)$ 的精确数值提供了理论依据，而这些数值正是训练[神经网络势能面](@entry_id:184102)的“标签”（labels）[@problem_id:2908409]。

在BO近似下，[原子核](@entry_id:167902)的运动被简化为在一个单一的[势能面](@entry_id:147441) $E_0(\lbrace\mathbf{R}_I\rbrace)$ 上的运动，其动力学行为由原子[核[哈密顿](@entry_id:752710)量](@entry_id:172864) $\hat{H}_{N,BO} = \hat{T}_N + E_0(\lbrace\mathbf{R}_I\rbrace)$ 决定。然而，必须强调，BO近似忽略了不同电子态之间的耦合，即**[非绝热耦合](@entry_id:198018)项**。这些耦合项源于[原子核](@entry_id:167902)[动能算符](@entry_id:265633) $\hat{T}_N$ 作用于完整的[波函数](@entry_id:147440)展开式 $\Psi_{tot} = \sum_k \chi_k(\lbrace\mathbf{R}_I\rbrace) \Psi_k(\lbrace\mathbf{r}_i\rbrace; \lbrace\mathbf{R}_I\rbrace)$ 时产生的对[原子核](@entry_id:167902)坐标的[导数耦合](@entry_id:202003)，例如 $\langle \Psi_j | \nabla_I \Psi_k \rangle$。这些耦合项在[势能面](@entry_id:147441)发生交叉或[近简并](@entry_id:172107)时变得至关重要，并导致[非绝热跃迁](@entry_id:199204)。因此，一个仅被训练来复现[基态](@entry_id:150928)[势能面](@entry_id:147441) $E_0(\lbrace\mathbf{R}_I\rbrace)$ 的标准[NN-PES](@entry_id:184102)，其本身无法描述光化学反应、电子转移等[非绝热动力学](@entry_id:189808)过程 [@problem_id:2908409]。

#### [势能面](@entry_id:147441)的[基本对称性](@entry_id:161256)

一个物理上合理的[势能面](@entry_id:147441)必须反映其所描述的孤立分子系统所处的物理空间的对称性，即[空间的均匀性](@entry_id:172987)和各向同性，以及同种粒子的不可区分性。这些对称性源于系统库仑[哈密顿量](@entry_id:172864)的不变性，并[对势能](@entry_id:203104)面函数 $E(\lbrace\mathbf{R}_I, Z_I\rbrace)$ 施加了严格的约束 [@problem_id:2908405]。

1.  **[平移不变性](@entry_id:195885)（Translational Invariance）**: [孤立系统](@entry_id:159201)的总能量不应依赖于其在空间中的绝对位置。将所有[原子核](@entry_id:167902)同时平移一个任意的矢量 $\mathbf{t} \in \mathbb{R}^3$，[势能面](@entry_id:147441)的值保持不变。
    $$ E(\lbrace\mathbf{R}_I + \mathbf{t}\rbrace, \lbrace Z_I \rbrace) = E(\lbrace\mathbf{R}_I\rbrace, \lbrace Z_I \rbrace) $$

2.  **[旋转不变性](@entry_id:137644)（Rotational Invariance）**: [孤立系统](@entry_id:159201)的总能量也不应依赖于其在空间中的绝对取向。将所有[原子核](@entry_id:167902)围绕原点进行一次任意的[正常旋转](@entry_id:141831)（proper rotation）$\mathbf{Q} \in \mathrm{SO}(3)$，[势能面](@entry_id:147441)的值同样保持不变。
    $$ E(\lbrace\mathbf{Q}\mathbf{R}_I\rbrace, \lbrace Z_I \rbrace) = E(\lbrace\mathbf{R}_I\rbrace, \lbrace Z_I \rbrace) $$

3.  **[置换不变性](@entry_id:753356)（Permutational Invariance）**: 量子力学中的[全同粒子](@entry_id:142755)是不可区分的。因此，交换任意两个相同种类原子（即具有相同核[电荷](@entry_id:275494) $Z$）的标签（或索引），系统的物理[状态和](@entry_id:193625)能量均不改变。若 $\pi$ 是一个仅在相同种类原子间进行交换的[置换](@entry_id:136432)操作，则：
    $$ E(\lbrace\mathbf{R}_{\pi(I)}\rbrace, \lbrace Z_I \rbrace) = E(\lbrace\mathbf{R}_I\rbrace, \lbrace Z_I \rbrace) $$
    这里利用了 $Z_{\pi(I)} = Z_I$ 的条件。

这些[不变性](@entry_id:140168)要求是构建任何形式的[势能面](@entry_id:147441)（包括[NN-PES](@entry_id:184102)）时必须遵守的先验物理法则。

#### 能量的不变性与力的[协变](@entry_id:634097)性

[势能面](@entry_id:147441)的一个核心应用是计算作用在[原子核](@entry_id:167902)上的力，这对于分子动力学模拟至关重要。根据经典力学的定义，作用在[原子核](@entry_id:167902) $I$ 上的力 $\mathbf{F}_I$ 是[势能](@entry_id:748988) $E$ 对其位置坐标 $\mathbf{R}_I$ 的负梯度：

$$ \mathbf{F}_I(\lbrace\mathbf{R}_J, Z_J\rbrace) = -\nabla_{\mathbf{R}_I} E(\lbrace\mathbf{R}_J, Z_J\rbrace) $$

能量 $E$ 是一个标量，而力 $\lbrace \mathbf{F}_I \rbrace$ 是一个矢量场。它们在上述对称性变换下的行为是不同的。能量满足**[不变性](@entry_id:140168)（invariance）**，而[力场](@entry_id:147325)则满足**协变性（equivariance）**。[协变](@entry_id:634097)性意味着当输入（[原子核](@entry_id:167902)构型）发生变换时，输出（力矢量）也以一种特定的、与输入变换相关联的方式进行变换 [@problem_id:2908382]。

具体而言，对于上述三种变换：

*   **平移**：对整个系统进行平移 $\mathbf{t}$ 时，由于能量不变，其梯度也不变。因此，力矢量是**平移不变的**。
    $$ \mathbf{F}_I(\lbrace\mathbf{R}_J + \mathbf{t}, Z_J\rbrace) = \mathbf{F}_I(\lbrace\mathbf{R}_J, Z_J\rbrace) $$

*   **旋转**：对整个系统进行旋转 $\mathbf{Q}$ 时，力矢量作为空间中的一个方向性物理量，必须随之旋转。这是**旋转协变的**。
    $$ \mathbf{F}_I(\lbrace\mathbf{Q}\mathbf{R}_J, Z_J\rbrace) = \mathbf{Q} \, \mathbf{F}_I(\lbrace\mathbf{R}_J, Z_J\rbrace) $$
    这个关系可以通过[链式法则](@entry_id:190743)从能量的[旋转不变性](@entry_id:137644)推导得出。

*   **[置换](@entry_id:136432)**：对同种原子进行[置换](@entry_id:136432) $\pi$ 时，作用在[新构型](@entry_id:199611)中原子 $\pi(I)$ 上的力，应该等于原构型中作用在原子 $I$ 上的力。这是一种**[置换](@entry_id:136432)[协变](@entry_id:634097)的**关系。
    $$ \mathbf{F}_{\pi(I)}(\lbrace\mathbf{R}_{\pi(J)}, Z_{\pi(J)}\rbrace) = \mathbf{F}_I(\lbrace\mathbf{R}_J, Z_J\rbrace) $$

在设计[NN-PES](@entry_id:184102)时，确保能量的不变性和力的协变性是模型物理真实性的根本保证。任何违反这些对称性的模型都将导致非物理的行为，例如在[分子动力学模拟](@entry_id:160737)中产生虚假的[净力](@entry_id:163825)和力矩，从而破坏动量和[角动量守恒](@entry_id:156798)。

### 分子几何的机器学习表征

直接将一个标准的[神经网](@entry_id:276355)络（如全连接网络）应用于笛卡尔坐标 $\lbrace\mathbf{R}_I\rbrace$ 是不可行的。因为这样的网络不具备内禀的对称性知识，它会错误地学习到能量与分子的绝对位置和取向有关，这在物理上是荒谬的。因此，必须通过模型的设计来**强制执行（enforce by design）**这些物理对称性，而不是期望模型从有限的数据中“学习”到它们 [@problem_id:2908409] [@problem_id:2952097]。

处理这些对称性的策略主要分为两大类：基于[不变性](@entry_id:140168)特征的表征和基于协变性架构的表征。

#### 基于不变性特征的表征

这种策略的思想是在将几何信息输入[神经网](@entry_id:276355)络之前，先将其转换为一组内禀满足平移、旋转和[置换不变性](@entry_id:753356)的描述符（descriptors）。

一个简单而有效的方法是使用原子间的相对距离 $r_{IJ} = \lVert \mathbf{R}_I - \mathbf{R}_J \rVert$ 作为输入。一个分子的几何形状（不考虑手性）可以由其所有原子间距离的集合唯一确定。由于距离是标量，它们天然地对平移和旋转不变。然后，通过对这些距离信息进行[置换](@entry_id:136432)不变的操作，就可以构建一个完全对称的表征 [@problem_id:2908414]。

**[原子中心对称函数](@entry_id:174796)（Atom-Centered Symmetry Functions, ACSF）**是这一思想的成熟实现，是[Behler-Parrinello](@entry_id:177243)类型[神经网](@entry_id:276355)络的核心 [@problem_id:2952097]。对于每个原子 $i$，其局部化学环境被编码成一个[特征向量](@entry_id:151813) $\mathbf{G}_i$。这个向量由一系列[对称函数](@entry_id:177113)构成，这些函数本身对邻近原子的[置换](@entry_id:136432)以及整个系统的旋转和平移是不变的。例如，径向对称函数可以是：
$$ G_i^{\text{rad}} = \sum_{j \neq i} \exp(-\eta (r_{ij} - R_s)^2) f_c(r_{ij}) $$
而角向[对称函数](@entry_id:177113)可以是：
$$ G_i^{\text{ang}} = 2^{1-\zeta} \sum_{j,k \neq i} (1 + \lambda \cos\theta_{ijk})^\zeta \exp(-\eta(r_{ij}^2+r_{ik}^2+r_{jk}^2)) f_c(r_{ij})f_c(r_{ik}) $$
其中 $f_c(r)$ 是一个平滑的截断函数，用于限制考虑的邻域范围。由于求和操作 $\sum$ 满足交换律，这些函数对于邻居原子 $j,k$ 的[置换](@entry_id:136432)是不变的。

通过这种方式，分子的几何被分解为一系列与原子相关联的、不变的局部环境描述符 $\lbrace \mathbf{G}_i \rbrace$。

#### 基于协变性架构的表征

与将所有几何信息预处理为不变标量不同，[协变](@entry_id:634097)架构的思想是让网络直接处理几何对象（如相对位置矢量），并在网络的每一层中保持它们的[协变](@entry_id:634097)性。这类模型，通常被称为**E(3)-协变[神经网](@entry_id:276355)络**（E(3)代表三维欧几里得群，即平移和旋转的组合），将中间层的特征组织成不同阶的张量，这些张量在旋转下遵循特定的变换规则（不可约表示，irreducible representations, or irreps）[@problem_id:2760132]。

这些网络的核心组件包括：
*   **输入**: 使用相对位置矢量 $\mathbf{r}_{ij} = \mathbf{r}_i - \mathbf{r}_j$ 作为输入，这保证了平移不变性。
*   **几何张量**: 通过球谐函数 $Y_{lm}(\hat{\mathbf{r}}_{ij})$ 将方向信息编码成不同阶的几何张量，这些张量在旋转下具有明确的变换性质。
*   **张量积**: 通过[张量积](@entry_id:140694)（tensor products）和[克莱布施-高登系数](@entry_id:142551)（Clebsch-Gordan coefficients）将不同层的[特征和](@entry_id:189446)几何信息组合起来，以生成新的、同样满足协变性的特征。
*   **协变[消息传递](@entry_id:751915)**: 在[图神经网络](@entry_id:136853)的框架下，节点（原子）之间传递的“消息”本身就是[协变张量](@entry_id:634493)。

通过精心设计这些操作，可以保证网络的每一层都满足旋转[协变](@entry_id:634097)性。

### [神经网络势能面](@entry_id:184102)的架构

#### 局域性与可加性假设

现代[NN-PES](@entry_id:184102)架构普遍基于**局域性（locality）**和**可加性（additivity）**的假设。总能量 $\hat{E}_\theta$ 被分解为每个原子的能量贡献之和：

$$ \hat{E}_\theta(\lbrace\mathbf{R}_I\rbrace) = \sum_{I=1}^{N} \varepsilon_\theta(\mathcal{D}_I) $$

其中，$\varepsilon_\theta$ 是一个（对于同种原子）共享参数的[神经网](@entry_id:276355)络，它将原子 $I$ 的局部环境描述符 $\mathcal{D}_I$ 映射到一个原子能量。$\mathcal{D}_I$ 只依赖于距原子 $I$ 一定**[截断半径](@entry_id:136708)（cutoff radius, $r_c$）**内的邻居原子 [@problem_id:2908380]。

这一假设的物理基础是**电子物质的[近视](@entry_id:178989)性（nearsightedness）原理**。对于具有[能隙](@entry_id:191975)的系统（如绝缘体和大多数分子）或在有限温度下的任何系统，局域的[电子结构](@entry_id:145158)性质（如电子[密度矩阵](@entry_id:139892)）随距离呈指数衰减。这意味着一个原子的能量主要由其近邻环境决定，来自远处原子的影响可以忽略不计。因此，使用有限的[截断半径](@entry_id:136708) $r_c$ 是一个受控的近似，其引入的误差会随 $r_c$ 的增大而指数减小。

这种局域分解带来了巨大的计算优势。在均匀体系中，每个原子邻居的数量在统计上是一个常数，与系统总原子数 $N$ 无关。通过使用邻居列表等高效算法，计算总能量和力的总成本可以实现与系统大小成**[线性标度](@entry_id:197235)（linear scaling, $\mathcal{O}(N)$）**，这使得模拟大体系成为可能 [@problem_id:2908380]。

然而，这种局域模型本质上是短程的，无法描述像[离子晶体](@entry_id:138598)或[极性分子](@entry_id:144673)体系中存在的长程静电相互作用（衰减如 $1/r$）。在这些情况下，必须将短程[NN-PES](@entry_id:184102)与一个显式的长程物理模型（如基于预测[原子电荷](@entry_id:204820)的库仑项）相结合。

#### 主要架构类型

1.  **原子中心模型（如[Behler-Parrinello网络](@entry_id:202059)）**: 这是基于[不变性](@entry_id:140168)特征的典型代表。如前所述，它首先计算每个原子的[原子中心对称函数](@entry_id:174796)（ACSFs）作为描述符，然后将这些描述符输入到各自的原子[神经网](@entry_id:276355)络中得到原子能量，最后将所有原子能量相加得到总能量 [@problem_id:2952097]。该架构通过设计保证了所有必要的对称性。

2.  **[图神经网络](@entry_id:136853)（Graph Neural Networks, GNNs）**: GNNs将分子视为一个图，原子是节点，原子间的关系（如键或距离）是边。通过**消息传递（message passing）**机制，每个原子节点迭代地从其邻居节点收集信息来更新自身的[特征向量](@entry_id:151813)（或称嵌入，embedding）。如果消息聚合函数（如求和、均值）是[置换](@entry_id:136432)不变的，那么经过多轮消息传递后，每个原子最终的[特征向量](@entry_id:151813)将以一种[置换](@entry_id:136432)协变的方式编码了其多层邻域内的化学环境。最后，通过一个[置换](@entry_id:136432)不变的读出函数（readout function），如对所有原子特征求和，得到总能量。这种架构同样能保证对称性，并且由于其可加性结构，有助于模型向更大体系的泛化 [@problem_id:2952097]。

3.  **E(3)-[协变](@entry_id:634097)网络**: 这是当前最先进的架构之一。它们将GNN的[消息传递范式](@entry_id:635682)与严格的群论约束相结合。在网络的每一层，特征都被表示为不同阶的[SO(3)](@entry_id:138200)不可约表示（$l=0$为标量，$l=1$为矢量等）。消息的构建和聚合都通过保证协变性的[张量积](@entry_id:140694)操作来完成。为了得到最终的标量总能量，网络最后会将所有非标量（$l>0$）的原子特征通过[协变](@entry_id:634097)操作（如取范数）转换为标量，然后进行求和。这种架构的优势在于它不丢弃任何几何信息（如方向），从而可能实现更高的[表达能力](@entry_id:149863)和数据效率 [@problem_id:2760132]。

#### 表达能力与普适近似定理

我们为何相信[神经网](@entry_id:276355)络有能力表示任意复杂的真实[势能面](@entry_id:147441)？理论上的支持来自**普适近似定理（Universal Approximation Theorem, UAT）**。该定理指出，一个具有足够宽度和[非线性激活函数](@entry_id:635291)的[前馈神经网络](@entry_id:635871)，可以在一个紧致（compact）定义域上以任意精度逼近任何[连续函数](@entry_id:137361)。

对于[NN-PES](@entry_id:184102)，这意味着只要我们将对称性正确地编码在架构中（例如，通过不变性描述符），一个足够大的[神经网](@entry_id:276355)络原则上就可以学习[势能面](@entry_id:147441)这个复杂的、高维的[连续函数](@entry_id:137361)。类似地，对于[置换](@entry_id:136432)不变函数，**DeepSets**等理论证明了形如 $\rho(\sum_i \phi(x_i))$ 的结构是普适的，这为基于求和的GNN架构提供了理论基础 [@problem_id:2908414]。对于E(3)-[协变](@entry_id:634097)网络，也有相应的普适近似定理被证明，表明它们可以逼近任何连续的协变函数。

### [NN-PES](@entry_id:184102)的训练与应用

#### 训练目标：能量与力的联合拟合

为了让[NN-PES](@entry_id:184102)不仅能预测准确的能量，还能产生用于[分子动力学模拟](@entry_id:160737)的可靠[力场](@entry_id:147325)，通常采用一个包含能量和力误差的联合损失函数进行训练：

$$ \mathcal{L}(\theta) = \sum_{i=1}^{M} \left[ \alpha \left( \hat{E}_\theta(\mathbf{R}_i) - E_i \right)^2 + \frac{\beta}{3N} \sum_{I=1}^{3N} \left( -\frac{\partial \hat{E}_\theta(\mathbf{R}_i)}{\partial R_{I}} - F_{i,I} \right)^2 \right] $$

其中，$(\mathbf{R}_i, E_i, \mathbf{F}_i)$ 是训练集中的样本，$\hat{E}_\theta$ 是[神经网](@entry_id:276355)络预测的能量，$\alpha$ 和 $\beta$ 是用于平衡能量和力误差贡献的超参数。

一个至关重要的概念是，只要预测的力 $\hat{\mathbf{F}}_\theta$ 是通过对预测的能量 $\hat{E}_\theta$ 求梯度得到的（即 $\hat{\mathbf{F}}_\theta = -\nabla \hat{E}_\theta$），那么所学的[力场](@entry_id:147325)就**通过构造保证是保守的（conservative by construction）** [@problem_id:2908431]。一个保守[力场的旋度](@entry_id:174409)恒为零（$\nabla \times \mathbf{F} = \mathbf{0}$），这是[能量守恒](@entry_id:140514)的必要条件。因此，那种试图训练一个独立的[神经网](@entry_id:276355)络来预测力，或者在[损失函数](@entry_id:634569)中加入显式旋度惩罚项的做法，都是没有必要且基于错误理解的。训练过程只是在所有可能的[保守力场](@entry_id:164320)中，寻找一个最接近参考数据的[力场](@entry_id:147325)。即使只使用力的信息进行训练（即 $\alpha=0$），所恢复的[势能面](@entry_id:147441)也是明确的（仅相差一个无关紧要的常数），且[力场](@entry_id:147325)依然是保守的。

#### 导数计算：[自动微分](@entry_id:144512)的角色

在训练和使用[NN-PES](@entry_id:184102)时，我们需要高效地计算能量对原子坐标的梯度（即力）。**[自动微分](@entry_id:144512)（Automatic Differentiation, AD）**是实现这一目标的关键技术。与引入[截断误差](@entry_id:140949)的数值有限差分法不同，AD通过对计算过程中的每一步基本运算应用链式法则，能够计算出函数导数的精确值（在[浮点精度](@entry_id:138433)范围内） [@problem_id:2908469]。

AD分为前向模式和反向模式。
*   **前向模式（Forward Mode）**：计算[雅可比-向量积](@entry_id:162748)（Jacobian-vector product）。对于输入维度远大于输出维度的函数，如 $\mathbb{R}^{3N} \to \mathbb{R}$ 的[势能函数](@entry_id:200753)，计算完整的梯度需要 $3N$ 次[前向传播](@entry_id:193086)。
*   **反向模式（Reverse Mode）**：也称为**[反向传播](@entry_id:199535)（backpropagation）**，计算向量-雅可比积（vector-Jacobian product）。对于势能函数这种情况，反向模式惊人地高效：它仅需一次[前向传播](@entry_id:193086)（计算能量）和一次[反向传播](@entry_id:199535)，就能计算出所有 $3N$ 个梯度分量。其计算成本仅为能量计算成本的一个小的常数倍。

因此，在[NN-PES](@entry_id:184102)中，我们总是使用反向模式AD来高效、精确地获得力。此外，通过组合使用AD，我们还可以高效地计算**黑塞-[向量积](@entry_id:156672)（Hessian-vector product）**，即 $\mathbf{H}\mathbf{v} = (\nabla^2 E)\mathbf{v}$，而无需显式构造和存储巨大的、需要 $\mathcal{O}(N^2)$ 内存的黑塞矩阵 $\mathbf{H}$。这对于[振动分析](@entry_id:146266)和高级的[几何优化](@entry_id:151817)算法至关重要 [@problem_id:2908469]。

#### 实践考量：样本效率与主动学习

尽管[NN-PES](@entry_id:184102)非常强大，但训练它们需要大量高质量的[量子化学](@entry_id:140193)计算数据，而这些数据非常昂贵。因此，提高**样本效率（sample complexity）**至关重要。

模型的架构选择直接影响样本效率。具有正确物理[归纳偏置](@entry_id:137419)（inductive bias）的模型，如局域性和对称性的模型，通常比通用模型需要更少的数据就能达到同等精度。例如，一个局域可加模型 $E = \sum_i \varepsilon(\rho_i)$ 的学习任务本质上是学习单个函数 $\varepsilon$。训练数据的价值在于提供了多样的局部环境 $\rho_i$ 样本。因此，其样本复杂度与不同局部环境的数量有关，而不是与训练分子的大小或数量直接相关，这使得模型具有很好的迁移性，能够从对小分子的学习泛化到大体系 [@problem_id:2760103]。

**[主动学习](@entry_id:157812)（Active Learning, AL）**是一种进一步提高样本效率的策略。它通过一个迭代循环来智能地选择下一个要计算的训练数据点：
1.  用现有数据训练一个[NN-PES](@entry_id:184102)模型。
2.  使用该模型（通常是一个不确定性量化模型，如[高斯过程](@entry_id:182192)或[深度集成](@entry_id:636362)模型）在大量未标记的候选构型中进行预测。
3.  选择模型最不确定（uncertain）的构型。
4.  对该构型进行昂贵的[量子化学](@entry_id:140193)计算，获得其能量和力。
5.  将这个新的数据点加入[训练集](@entry_id:636396)，并重复循环。

通过这种方式，AL主动探索[势能面](@entry_id:147441)中模型尚未充分学习的区域。在这里，模型的对称性再次显示出其优越性。一个严格的E(3)-协变模型，其预测的能量和不确定性（作为一个标量）都将是旋转和平移不变的。这可以防止AL算法浪费计算资源去查询一个已知构型的不同旋转或平移版本，从而使对[构型空间](@entry_id:149531)的探索更加高效 [@problem_id:2760132]。