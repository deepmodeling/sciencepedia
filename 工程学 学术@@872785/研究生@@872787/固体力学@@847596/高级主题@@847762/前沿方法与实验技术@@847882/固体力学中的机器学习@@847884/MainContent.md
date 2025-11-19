## 引言
机器学习正在深刻地改变科学与工程计算的[范式](@entry_id:161181)，而[固体力学](@entry_id:164042)作为工程科学的基石，正处在这场变革的前沿。传统的力学建模方法在面对极端复杂的材料行为、多尺度耦合效应以及对高昂计算成本的挑战时，常常显得力不从心。机器学习，尤其是[深度学习](@entry_id:142022)，凭借其强大的函数逼近能力，为从数据中发现并表达复杂的物理规律提供了前所未有的机遇。然而，如何确保这些数据驱动的“黑箱”模型能够遵守基本的物理定律（如[能量守恒](@entry_id:140514)、客观性），并建立对其预测结果的信任，是当前该领域面临的核心知识鸿沟。

本文旨在系统性地解决这一挑战。在接下来的内容中，我们将首先在 **“原理与机制”** 部分，深入剖析将物理学原理融入机器学习模型的核心思想与技术框架，探讨如何构建[热力学一致的](@entry_id:755906)本构模型和[求解偏微分方程](@entry_id:138485)的物理信息网络。随后，在 **“应用与交叉学科联系”** 部分，我们将展示这些先进方法如何在[材料塑性](@entry_id:186852)、[多尺度模拟](@entry_id:752335)和[可靠性分析](@entry_id:192790)等实际问题中发挥作用，并揭示其与其他学科的深刻联系。最后，通过 **“动手实践”** 部分，读者将有机会通过具体的编码练习来巩固所学知识。让我们首先从支撑这一切的基础——机器学习在固体力学中的核心原理与机制——开始探索。

## 原理与机制

本章旨在深入探讨在[固体力学](@entry_id:164042)中应用机器学习（ML）模型所依据的核心科学原理与关键技术机制。我们将从两个主要应用[范式](@entry_id:161181)出发——构建[数据驱动的本构模型](@entry_id:748172)和求解宏观边界值问题——然后系统性地阐述如何将基本的物理学原理（如客观性、[热力学定律](@entry_id:202285)）融入这些模型。最后，我们将讨论评估这些新兴计算工具可信度的严谨框架，包括[不确定性量化](@entry_id:138597)以及[验证与确认](@entry_id:173817)（Verification and Validation, [V&V](@entry_id:173817)）。

### 机器学习在固体力学中的两种主要[范式](@entry_id:161181)

机器学习在固体力学领域的应用，大体上可归结为两大类任务：一是在材料点尺度上学习[本构关系](@entry_id:186508)，二是在结构尺度上学习整个系统的响应。

#### [数据驱动的本构模型](@entry_id:748172)

传统[固体力学](@entry_id:164042)的核心在于本构模型，即描述材料[应力-应变关系](@entry_id:274093)的数学方程。这些模型通常基于物理洞察和实验观测，通过具有明确物理意义的少数参数（如杨氏模量、[泊松比](@entry_id:158876)）来表达。一个新兴的[范式](@entry_id:161181)是利用机器学习直接从实验或高保真模拟数据中学习[本构关系](@entry_id:186508)，这被称为**数据驱动[本构模型](@entry_id:174726)**。

最直接的方法是建立一个从应变到应力的逐点映射（pointwise mapping）。然而，这种方法的适用性依赖于一系列严格的物理假设 [@problem_id:2656040]。从连续介质[热力学](@entry_id:141121)的基本公理出发，特别是局部作用原理和克劳修斯-杜亥姆不等式（Clausius-Duhem inequality），我们可以推导出，只有在满足以下条件时，应力 $\boldsymbol{\sigma}$ 才是应变 $\boldsymbol{\epsilon}$ 的一个单值函数 $\boldsymbol{\sigma}(\boldsymbol{\epsilon})$：
1.  **局部性（Locality）**：材料响应仅取决于该物[质点](@entry_id:186768)的状态，排除了应变梯度等[非局部效应](@entry_id:198046)。
2.  **弹性行为（Elasticity）**：材料是无记忆和可逆的，排除了塑性、损伤或蠕变等历史依赖的耗散过程。这意味着[亥姆霍兹自由能](@entry_id:136442)（Helmholtz free energy）仅是当前应变的函数。
3.  **[等温过程](@entry_id:143096)（Isothemality）**：过程在恒定温度下发生，排除了[热力耦合](@entry_id:183230)效应。
4.  **小应变与小转动（Small Strains and Rotations）**：在此假设下，[无穷小应变张量](@entry_id:167211) $\boldsymbol{\epsilon}$ 是一个客观的[应变度量](@entry_id:755495)。
5.  **材料[均匀性](@entry_id:152612)（Homogeneity）**：用于训练模型的所有数据点都来自具有相同本构行为的材料。

当这些条件满足时，监督学习方法，例如训练一个[神经网](@entry_id:276355)络，从应变-应力数据对 $\{(\boldsymbol{\epsilon}^{(i)}, \boldsymbol{\sigma}^{(i)})\}$ 中学习映射关系，是物理上自洽的。

即便如此，数据驱动模型与传统的[唯象模型](@entry_id:273816)在本质上仍有显著区别 [@problem_id:2656079]。
*   一个**数据驱动[本构定律](@entry_id:178936)**通常被表示为一个[参数化](@entry_id:272587)的函数逼近器，如[神经网](@entry_id:276355)络 $\hat{\boldsymbol{\sigma}}=\mathcal{N}_{\boldsymbol{\theta}}(\boldsymbol{\epsilon})$。其参数 $\boldsymbol{\theta}$（即[神经网](@entry_id:276355)络的权重和偏置）通常维度很高，缺乏直接的物理诠释。这些参数是通过最小化模型预测与实验数据之间的[经验风险](@entry_id:633993)（empirical risk）来确定的。
*   相比之下，一个**唯象本构模型**具有一个由物理假设预先设定的函数形式，例如 $\boldsymbol{\sigma}(\boldsymbol{\epsilon},\boldsymbol{p})$。其参数 $\boldsymbol{p}$ 维度较低，且通常具有明确的物理意义（如拉梅参数、硬化模量）。这些参数是通过求解一个[逆问题](@entry_id:143129)，在给定的函数形式约束下对实验数据进行校准而得到的。

数据驱动模型的主要优势在于其强大的函数表达能力，能够捕捉传统模型难以描述的复杂[非线性](@entry_id:637147)行为。然而，其挑战在于如何确保模型在训练数据之外的区域仍能遵守基本的物理定律，这便是“[物理信息](@entry_id:152556)机器学习”（Physics-Informed Machine Learning, PIML）研究的核心。

#### 求解边界值问题的代理模型

第二个主要[范式](@entry_id:161181)是将机器学习应用于整个边界值问题（Boundary Value Problem, BVP）的求解。考虑一个线性弹性体，其位移场 $\boldsymbol{u}$ 由[平衡方程](@entry_id:172166)、[本构关系](@entry_id:186508)和边界条件共同决定。对于给定的[体力](@entry_id:174230) $\boldsymbol{f}$，存在一个唯一的位移解 $\boldsymbol{u}$。这个从输入（荷载、边界条件、材料属性等）到输出（位移场、应[力场](@entry_id:147325)等）的映射被称为**解算子（solution operator）** [@problem_id:2656064]。

以线性[弹性静力学](@entry_id:198298)为例，解算子 $\mathcal{G}$ 将体力场 $\boldsymbol{f}$ 映射到满足弱形式方程的唯一[位移场](@entry_id:141476) $\boldsymbol{u} = \mathcal{G}[\boldsymbol{f}]$。在机器学习的背景下，我们可以区分两种学习目标：
1.  **[函数逼近](@entry_id:141329)（Function Approximation）**：对于一个**固定**的[体力](@entry_id:174230)场 $\boldsymbol{f}$，学习其对应的解函数，即映射关系 $\boldsymbol{x} \mapsto \boldsymbol{u}(\boldsymbol{x})$。这相当于为单个特定问题学习一个解。
2.  **算子逼近（Operator Approximation）**：学习整个解算子 $\mathcal{G}$。一个训练好的算子模型可以接受**任意**属于某个函数空间的体力场 $\boldsymbol{f}$ 作为输入，并快速预测相应的解 $\boldsymbol{u}$，而无需重新训练。

显然，算子逼近是更强大、更通用的目标，尤其适用于需要快速、重复求解[参数化偏微分方程](@entry_id:753165)（PDE）的场景，如优化设计、[不确定性量化](@entry_id:138597)和[实时控制](@entry_id:754131)。诸如[傅里叶神经算子](@entry_id:189138)（Fourier Neural Operator）等现代架构，其设计目标正是学习这种无限维空间之间的映射，它们通过学习积分算子的[核函数](@entry_id:145324)（或其在[频域](@entry_id:160070)的等价形式）来实现对不同输入函数的泛化，并且具有对输入函数离散化方式不变的优良特性 [@problem_id:2656064]。

### 构建物理约束的本构模型

一个纯粹由数据驱动的“黑箱”模型很可能在物理上是不自洽的。例如，它可能不满足[能量守恒](@entry_id:140514)，或者在[坐标系](@entry_id:156346)旋转后给出不同的预测。因此，将物理约束整合到模型架构或训练过程中至关重要。

#### 客观性与各向同性

**[客观性原理](@entry_id:185412)（Principle of Objectivity）**或称物质坐标[不变性](@entry_id:140168)，要求[本构定律](@entry_id:178936)在[刚体运动](@entry_id:193355)（旋转和平移）下保持形式不变。对于各向同性材料，这意味着[应力张量](@entry_id:148973)必须是[应变张量](@entry_id:193332)和单位张量 $\boldsymbol{I}$ 的[各向同性张量](@entry_id:195105)函数。根据[张量表示](@entry_id:180492)定理（[Cayley-Hamilton定理](@entry_id:150551)的推论），任何此类函数都可以表达为 $\boldsymbol{\sigma} = \alpha_0 \boldsymbol{I} + \alpha_1 \boldsymbol{\epsilon} + \alpha_2 \boldsymbol{\epsilon}^2$，其中标量系数 $\alpha_0, \alpha_1, \alpha_2$ 是[应变不变量](@entry_id:190518)（如 $I_1 = \operatorname{tr}(\boldsymbol{\epsilon})$, $I_2$, $I_3$）的函数。

这一结构为构建物理上合理的模型提供了明确的指导。例如，在从数据中发现[本构关系](@entry_id:186508)时，我们可以不采用通用的[神经网](@entry_id:276355)络，而是构建一个由[各向同性张量](@entry_id:195105)[基函数](@entry_id:170178)组成的库，然后通过[稀疏回归](@entry_id:276495)来寻找一个简洁、可解释的模型 [@problem_id:2656022]。一个适用于二次[非线性弹性](@entry_id:185743)模型的[基函数](@entry_id:170178)库可以包括：
$$
\{ \operatorname{tr}(\boldsymbol{\epsilon})\boldsymbol{I}, \boldsymbol{\epsilon}, [\operatorname{tr}(\boldsymbol{\epsilon})]^2\boldsymbol{I}, I_2(\boldsymbol{\epsilon})\boldsymbol{I}, \operatorname{tr}(\boldsymbol{\epsilon})\boldsymbol{\epsilon}, \boldsymbol{\epsilon}^2 \}
$$
模型可以表达为这些[基函数](@entry_id:170178)的线性组合 $\widehat{\boldsymbol{\sigma}}(\boldsymbol{\epsilon}) = \sum_{k} w_k \boldsymbol{\phi}_k(\boldsymbol{\epsilon})$。为了求解权重 $w_k$，我们需要将张量方程转化为标准的[向量化](@entry_id:193244)[线性系统](@entry_id:147850)。此时，必须使用保持[张量内积](@entry_id:190619)的向量化方法，如**开尔文-曼德尔（Kelvin-Mandel）表示法**，它通过在剪切分量上引入 $\sqrt{2}$ 因子，确保了张量的[弗罗贝尼乌斯内积](@entry_id:153693)（Frobenius inner product）等价于向量的[点积](@entry_id:149019)。然后，可以求解一个[LASSO](@entry_id:751223)（Least Absolute Shrinkage and Selection Operator）问题：
$$
\min_{\boldsymbol{w}} \frac{1}{2}\|\boldsymbol{\Phi}\boldsymbol{w} - \boldsymbol{s}\|_2^2 + \lambda \|\boldsymbol{w}\|_1
$$
其中 $\boldsymbol{\Phi}$ 是由[基函数](@entry_id:170178)在数据点上的值构成的[设计矩阵](@entry_id:165826)，$\boldsymbol{s}$ 是堆叠的应力观测向量，$\lambda$ 是[正则化参数](@entry_id:162917)。这种方法不仅保证了客观性和各向同性，还可能发现形式简单、易于理解的[本构方程](@entry_id:138559)。

#### [热力学一致性](@entry_id:138886) (I): [超弹性](@entry_id:159356)

热力学第二定律对[本构关系](@entry_id:186508)施加了更强的约束。对于弹性材料，一个关键的约束是**[超弹性](@entry_id:159356)（hyperelasticity）**，即应力可以从一个[标量势](@entry_id:276177)函数——**[应变能密度函数](@entry_id:755490)** $W(\boldsymbol{\epsilon})$——通过求导得到：
$$
\boldsymbol{\sigma} = \frac{\partial W}{\partial \boldsymbol{\epsilon}}
$$
这一特性保证了弹性变形过程的[路径无关性](@entry_id:163750)（功守恒），并直接导出一个重要的数学属性：材料的[切线刚度](@entry_id:166213)张量 $\mathbb{C}_{ijkl} = \frac{\partial \sigma_{ij}}{\partial \epsilon_{kl}} = \frac{\partial^2 W}{\partial \epsilon_{ij} \partial \epsilon_{kl}}$ 具有**主对称性（major symmetry）**，即 $\mathbb{C}_{ijkl} = \mathbb{C}_{klij}$。

一个通用的神经[网络模型](@entry_id:136956) $\mathcal{N}_{\boldsymbol{\theta}}(\boldsymbol{\epsilon})$ 的[雅可比矩阵](@entry_id:264467)（Jacobian）通常不具备这种对称性 [@problem_id:2656079]。为了强制施加[超弹性](@entry_id:159356)约束，主要有两种策略 [@problem_id:2656012]：

1.  **依构造施加（By Construction）**：这是最严格和理想的方法。我们不再直接对应力进行建模，而是用一个[神经网](@entry_id:276355)络来表示标量的[应变能密度函数](@entry_id:755490) $W_{\boldsymbol{\theta}}(\boldsymbol{\epsilon})$。然后，应力通过[自动微分](@entry_id:144512)（Automatic Differentiation, AD）精确地计算为 $\widehat{\boldsymbol{\sigma}} = \frac{\partial W_{\boldsymbol{\theta}}}{\partial \boldsymbol{\epsilon}}$。由于 $\widehat{\boldsymbol{\sigma}}$ 是一个[势函数](@entry_id:176105)的梯度，其[切线刚度](@entry_id:166213)（即 $W_{\boldsymbol{\theta}}$ 的海森矩阵）必然是对称的。这种方法从根本上保证了[热力学一致性](@entry_id:138886)。

2.  **通过[罚函数](@entry_id:638029)施加（By Penalty）**：我们可以继续使用一个直接映射应力的网络 $\mathcal{N}_{\boldsymbol{\theta}}(\boldsymbol{\epsilon})$，但在损失函数中加入一个正则化项，惩罚其[切线刚度](@entry_id:166213)的不对称性。例如，在训练过程中最小化 $\mathcal{L}_{\text{data}} + \lambda \|\mathbb{C}_{\boldsymbol{\theta}} - \mathbb{C}_{\boldsymbol{\theta}}^T\|_F^2$，其中 $\mathbb{C}_{\boldsymbol{\theta}}$ 是网络雅可比矩阵的张量形式。这种“软”约[束方法](@entry_id:636307)只能在训练数据点附近近似满足对称性，而不能在整个输入空间中提供严格保证。

因此，对于需要严格保证[能量守恒](@entry_id:140514)的场景，“依构造”的[势函数](@entry_id:176105)方法是首选。

#### [热力学一致性](@entry_id:138886) (II): [耗散系统](@entry_id:151564)

对于更普遍的非弹性材料（如塑性、黏弹性材料），存在[能量耗散](@entry_id:147406)。此时，材料状态不仅取决于当前的应变 $\boldsymbol{\epsilon}$，还取决于一组描述材料内部微观结构状态的**内变量（internal variables）** $\boldsymbol{\alpha}$。[亥姆霍兹自由能](@entry_id:136442)是两者的函数：$\psi(\boldsymbol{\epsilon}, \boldsymbol{\alpha})$。

对于[等温过程](@entry_id:143096)，克劳修斯-杜亥姆不等式可以简化为局部[耗散不等式](@entry_id:188634) [@problem_id:2656091]：
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\epsilon}} - \dot{\psi} \ge 0
$$
其中 $\mathcal{D}$ 是单位体积的耗散率，必须非负。通过标准的科尔曼-诺尔（Coleman-Noll）论证，可以得到弹性应力关系 $\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\epsilon}}$，并将[耗散不等式](@entry_id:188634)简化为：
$$
\mathcal{D} = \boldsymbol{A} \cdot \dot{\boldsymbol{\alpha}} \ge 0
$$
其中 $\boldsymbol{A} := -\frac{\partial \psi}{\partial \boldsymbol{\alpha}}$ 是与内变量共轭的**[热力学力](@entry_id:161907)**。这个不等式意味着内变量的演化方向必须使得能量耗散为非负。

挑战在于如何为内变量的演化率 $\dot{\boldsymbol{\alpha}}$ 构建一个模型，使其永久满足此不等式。同样，“依构造”满足[热力学约束](@entry_id:755911)的结构化机器学习方法是关键。两种有效的框架是 [@problem_id:2656091]：

1.  **[线性动力学](@entry_id:177848)假设**：假设内变量的演化率与[热力学力](@entry_id:161907)成正比，即 $\dot{\boldsymbol{\alpha}} = \boldsymbol{L}\boldsymbol{A}$。为了保证 $\mathcal{D} = \boldsymbol{A} \cdot (\boldsymbol{L}\boldsymbol{A}) = \boldsymbol{A}^T \boldsymbol{L} \boldsymbol{A} \ge 0$ 对任意 $\boldsymbol{A}$ 成立，算子 $\boldsymbol{L}$ 必须是**对称正半定（symmetric positive semidefinite）**的。因此，我们可以用一个[神经网](@entry_id:276355)络来学习自由能 $\psi_{\boldsymbol{\theta}}$，并用另一个网络来参数化一个对称正半定的矩阵 $\boldsymbol{L}_{\boldsymbol{\theta}}$（例如，通过[Cholesky分解](@entry_id:147066) $\boldsymbol{L}_{\boldsymbol{\theta}} = \boldsymbol{M}_{\boldsymbol{\theta}} \boldsymbol{M}_{\boldsymbol{\theta}}^T$），从而构建一个[热力学一致的](@entry_id:755906)非弹性模型。

2.  **广义标准材料（Generalized Standard Materials, GSM）框架**：引入一个关于[热力学力](@entry_id:161907)的**耗散[势函数](@entry_id:176105)** $\Phi(\boldsymbol{A})$，它是一个非负的凸函数且 $\Phi(\boldsymbol{0}) = 0$。然后，假设演化定律遵循关联流动法则，即 $\dot{\boldsymbol{\alpha}}$ 位于 $\Phi$ 在 $\boldsymbol{A}$ 点的次梯度（subdifferential）集合中：$\dot{\boldsymbol{\alpha}} \in \partial \Phi(\boldsymbol{A})$。根据[凸分析](@entry_id:273238)的性质，这个结构可以保证[耗散不等式](@entry_id:188634) $\boldsymbol{A} \cdot \dot{\boldsymbol{\alpha}} \ge \Phi(\boldsymbol{A}) \ge 0$ 恒成立。我们可以使用**输入凸[神经网](@entry_id:276355)络（Input-Convex Neural Networks, ICNN）**等特殊架构来参数化耗散势 $\Phi_{\boldsymbol{\theta}}$，从而构建更复杂的、[热力学一致的](@entry_id:755906)非弹性本构模型。

这些结构化方法为将机器学习应用于黏塑性等复杂材料行为的建模提供了坚实的物理基础。

### 求解偏微分方程的物理信息神经网络

除了本构建模，机器学习，特别是深度学习，也为直接求解描述固体力学行为的[偏微分方程](@entry_id:141332)（PDE）提供了新工具。

#### 基于残差的方法：[PINNs](@entry_id:145229)

**物理信息神经网络（Physics-Informed Neural Networks, PINN）**是一种通过最小化控制方程残差来训练[神经网](@entry_id:276355)络[求解PDE](@entry_id:138485)的框架。其核心思想是，将待求解的物理场（如位移场 $\boldsymbol{u}$）用一个以空间坐标 $\boldsymbol{x}$ 为输入的[神经网](@entry_id:276355)络 $\boldsymbol{u}_{\boldsymbol{\theta}}(\boldsymbol{x})$ 来表示。网络的参数 $\boldsymbol{\theta}$ 通过最小化一个复合[损失函数](@entry_id:634569)来优化，该[损失函数](@entry_id:634569)包含了对物理定律的强制执行。

以线性[弹性静力学](@entry_id:198298)为例，一个典型的[PINN损失函数](@entry_id:137288)由三部分构成 [@problem_id:2656090]：
$$
\mathcal{L}(\boldsymbol{\theta}) = w_{\Omega}\mathcal{L}_{\Omega} + w_D\mathcal{L}_D + w_N\mathcal{L}_N
$$
其中：
1.  **域内残差损失 $\mathcal{L}_{\Omega}$**：惩罚在求解域 $\Omega$ 内部不满足[平衡方程](@entry_id:172166)的行为。它被定义为平衡方程残差的均方误差：
    $$
    \mathcal{L}_{\Omega} = \frac{1}{N_{\Omega}} \sum_{i=1}^{N_{\Omega}} \|\nabla \cdot \boldsymbol{\sigma}_{\boldsymbol{\theta}}(\boldsymbol{x}_i) + \boldsymbol{b}(\boldsymbol{x}_i)\|_2^2
    $$
    其中 $\boldsymbol{\sigma}_{\boldsymbol{\theta}} = \mathbb{C}:\boldsymbol{\epsilon}(\boldsymbol{u}_{\boldsymbol{\theta}})$，$\{\boldsymbol{x}_i\}$ 是从 $\Omega$ 内部采样的 collocation 点。所有的导数（如 $\nabla \cdot$ 和 $\boldsymbol{\epsilon}(\boldsymbol{u}_{\boldsymbol{\theta}})$）都通过[自动微分](@entry_id:144512)精确计算。

2.  **狄利克雷边界损失 $\mathcal{L}_D$**：惩罚在狄利克雷边界 $\Gamma_D$ 上不满足[位移边界条件](@entry_id:203261)的网络输出：
    $$
    \mathcal{L}_D = \frac{1}{N_D} \sum_{j=1}^{N_D} \|\boldsymbol{u}_{\boldsymbol{\theta}}(\boldsymbol{x}_j) - \bar{\boldsymbol{u}}(\boldsymbol{x}_j)\|_2^2
    $$
    其中 $\{\boldsymbol{x}_j\}$ 是从 $\Gamma_D$ [上采样](@entry_id:275608)的点。

3.  **诺伊曼边界损失 $\mathcal{L}_N$**：惩罚在诺伊曼边界 $\Gamma_N$ 上不满足力边界条件的网络输出：
    $$
    \mathcal{L}_N = \frac{1}{N_N} \sum_{k=1}^{N_N} \|\boldsymbol{\sigma}_{\boldsymbol{\theta}}(\boldsymbol{x}_k)\boldsymbol{n}(\boldsymbol{x}_k) - \bar{\boldsymbol{t}}(\boldsymbol{x}_k)\|_2^2
    $$
    其中 $\{\boldsymbol{x}_k\}$ 是从 $\Gamma_N$ [上采样](@entry_id:275608)的点。

$w_{\Omega}, w_D, w_N$ 是用于平衡不同损失项的权重。这种方法的优点在于其无网格的特性和处理复杂几何的灵活性，但训练过程可能很困难，尤其对于多尺度或[刚性问题](@entry_id:142143)。

#### 基于变分的方法：[深度里兹法](@entry_id:748271)

作为对PINN的补充，另一大类方法基于物理问题的**[变分原理](@entry_id:198028)（variational principle）**，如[最小势能原理](@entry_id:173340)。**[深度里兹法](@entry_id:748271)（Deep Ritz Method）**是其中的代表。

对于[超弹性材料](@entry_id:190241)，平衡态对应于系统总势能 $\Pi(\boldsymbol{u})$ 的一个驻点（通常是最小值）。总[势能](@entry_id:748988)由储存的[应变能](@entry_id:162699)和外力所做的功组成 [@problem_id:2656078]：
$$
\Pi(\boldsymbol{u}) = \int_{\Omega} W(\boldsymbol{\epsilon}(\boldsymbol{u}))\,d\Omega - \int_{\Omega} \boldsymbol{b}\cdot \boldsymbol{u}\,d\Omega - \int_{\Gamma_t} \bar{\boldsymbol{t}}\cdot \boldsymbol{u}\,d\Gamma
$$
[深度里兹法](@entry_id:748271)同样使用[神经网](@entry_id:276355)络 $\boldsymbol{u}_{\boldsymbol{\theta}}(\boldsymbol{x})$ 作为位移场的 ansatz，但其目标是直接最小化离散形式的总[势能](@entry_id:748988)泛函 $\Pi(\boldsymbol{u}_{\boldsymbol{\theta}})$，而不是PDE的残差。

这种变分方法与PINN相比有几个特点：
*   **适用性**：它要求问题存在一个等价的[变分形式](@entry_id:166033)，这在许多物理系统中是成立的。
*   **导数阶数**：[能量泛函](@entry_id:170311)通常只包含场变量的一阶导数（例如 $\boldsymbol{\epsilon}(\boldsymbol{u})$），而强形式PDE残差可能包含二阶或更高阶导数。这使得变分法的[损失函数](@entry_id:634569)计算可能更稳定。
*   **边界条件**：在变分框架中，力边界条件（诺伊曼BC）是**自然边界条件（natural boundary conditions）**，它们通过能量泛函中的边界积分项被自动满足，无需额外惩罚。而[位移边界条件](@entry_id:203261)（狄利克雷BC）是**[本质边界条件](@entry_id:173524)（essential boundary conditions）**，必须被强制施加，例如通过[罚函数](@entry_id:638029)或设计满足条件的[网络结构](@entry_id:265673)。
*   **数值挑战**：对于特定问题，如[近不可压缩材料](@entry_id:752388)，朴素的位移基[深度里兹法](@entry_id:748271)可能会遭遇与传统有限元方法中类似的**[体积锁定](@entry_id:172606)（volumetric locking）**现象，导致模型病态和解的不准确 [@problem_id:2656078]。

### 模型的评估与可信度

开发一个能够运行的ML模型只是第一步；建立对其预测结果的信任是更关键的挑战。这需要一个系统的评估框架，涵盖不确定性量化和严格的[验证与确认](@entry_id:173817)流程。

#### [不确定性量化](@entry_id:138597)：认知不确定性与[偶然不确定性](@entry_id:154011)

在数据驱动的[科学计算](@entry_id:143987)中，预测的不确定性主要来自两个截然不同的来源，区分它们至关重要 [@problem_id:2656063]。

1.  **[偶然不确定性](@entry_id:154011)（Aleatoric Uncertainty）**：源于系统或测量过程中的**固有随机性**。在固体力学中，这可能来自于[材料微观结构](@entry_id:198422)的统计异质性（如晶粒取向、夹杂物[分布](@entry_id:182848)）或传感器测量时的噪声。这种不确定性是不可约减的（irreducible），即使拥有无限多的训练数据，这种随机性依然存在。

2.  **[认知不确定性](@entry_id:149866)（Epistemic Uncertainty）**：源于我们对最优模型的**知识欠缺**。这通常是由于训练数据量有限、数据覆盖不全，或是模型本身的结构不足以完美描述物理现实。这种不确定性是可约减的（reducible），通过收集更多的信息（如更多、更高质量的训练数据），我们可以减少对模型参数或模型形式的无知，从而降低[认知不确定性](@entry_id:149866)。

在贝叶斯框架下，这两种不确定性可以通过总[方差](@entry_id:200758)定律（law of total variance）进行分解。对于一个新输入 $\boldsymbol{\epsilon}$ 的预测应力 $\boldsymbol{\sigma}$，其总预测[方差](@entry_id:200758)为：
$$
\mathrm{Var}(\boldsymbol{\sigma} | \boldsymbol{\epsilon}, \mathcal{D}) = \underbrace{\mathbb{E}_{\boldsymbol{\theta}|\mathcal{D}}\! \big[ \mathrm{Var}(\boldsymbol{\sigma}|\boldsymbol{\epsilon},\boldsymbol{\theta}) \big]}_{\text{偶然不确定性}} + \underbrace{\mathrm{Var}_{\boldsymbol{\theta}|\mathcal{D}}\! \big( \mathbb{E}[\boldsymbol{\sigma}|\boldsymbol{\epsilon},\boldsymbol{\theta}] \big)}_{\text{认知不确定性}}
$$
第一项是模型在给定参数 $\boldsymbol{\theta}$ 下的预测[方差](@entry_id:200758)的[期望值](@entry_id:153208)，反映了数据本身的噪声水平。第二项是[模型平均](@entry_id:635177)预测随参数 $\boldsymbol{\theta}$ [后验分布](@entry_id:145605)变化的[方差](@entry_id:200758)，反映了我们对模型参数的不确定性。量化并分离这两种不确定性，对于评估模型的置信度和指导后续实验设计至关重要。

#### [验证与确认](@entry_id:173817) ([V&V](@entry_id:173817)): 建立[计算模型](@entry_id:152639)的信誉

将ML模型嵌入[固体力学](@entry_id:164042)求解器中，形成了一个复杂的混合[计算模型](@entry_id:152639)。评估其可信度，必须遵循计算科学与工程领域已建立的**[验证与确认](@entry_id:173817)（Verification and Validation, [V&V](@entry_id:173817)）**的严谨层级框架 [@problem_id:2656042]。

[V&V](@entry_id:173817)包含一系列按顺序进行的活动，它们回答了三个不同的问题：

1.  **[代码验证](@entry_id:146541)（Code Verification）**：“我们是否正确地求解了方程？”
    这是一个纯数学和软件工程的活动，旨在确认软件代码准确地实现了其意图解决的数学模型（离散方程）。它与物理现实无关。最强大的工具是**制造解方法（Method of Manufactured Solutions, MMS）**，即构造一个解析解，并[反向代入](@entry_id:168868)控制方程以导出[源项](@entry_id:269111)和边界条件。然后运行代码求解此“制造”的问题，并验证随着网格或时间步的细化，数值解与制造解之间的误差是否以理论预期的速率收敛。

2.  **解的验证（Solution Verification）**：“我们的数值解有多精确？”
    在确认代码无误后，此步骤旨在为某个具体、实际的模拟任务量化其数值解的误差。由于真实问题的精确解通常是未知的，误差必须被估计。常用方法包括系统性的[网格加密研究](@entry_id:750067)（例如，使用[理查森外推法](@entry_id:137237)）或[后验误差估计](@entry_id:167288)器。这一步的目的是确保[离散化误差](@entry_id:748522)和迭代误差被控制在可接受的范围内。

3.  **确认（Validation）**：“我们求解的方程是否正确？”
    这是[V&V](@entry_id:173817)过程的最后一步，旨在通过将模型的计算预测与物理现实（通常是实验数据）进行比较，来确定数学模型在多大程度上代表了目标应用。它评估的是物理模型的保真度。

这三个步骤必须按顺序执行：**[代码验证](@entry_id:146541) $\rightarrow$ 解的验证 $\rightarrow$ 确认**。在一个有缺陷的代码上进行模拟是无意义的；用一个充满[数值误差](@entry_id:635587)的解去和实验比较，可能会错误地否定一个正确的物理模型，或错误地接受一个有缺陷的模型。对ML增强的[固体力学](@entry_id:164042)求解器应用这一纪律严明的流程，是确保其在工程和科学应用中安全、可靠和可信的基石。