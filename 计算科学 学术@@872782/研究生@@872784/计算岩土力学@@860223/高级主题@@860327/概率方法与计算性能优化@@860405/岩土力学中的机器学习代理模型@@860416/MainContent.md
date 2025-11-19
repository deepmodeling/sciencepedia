## 引言
在计算岩[土力学](@entry_id:180264)的研究与工程实践中，高保真度[数值模拟](@entry_id:137087)（如[有限元法](@entry_id:749389)）虽然精确，但其高昂的计算成本常常成为大规模分析、[设计优化](@entry_id:748326)和不确定性评估的瓶颈。机器学习（ML）代理模型作为一种数据驱动的方法，通过学习复杂输入-输出关系，为加速这些计算过程提供了极具前景的解决方案。然而，一个核心挑战在于如何确保这些本质上是“黑箱”的模型能够遵守基本的物理定律，从而保证其预测的物理真实性和在训练数据之外的泛化能力。若缺乏物理约束，代理模型可能产生违反[能量守恒](@entry_id:140514)或[材料稳定性](@entry_id:183933)的荒谬结果，使其在安全攸关的工程应用中变得不可靠。

本文旨在系统性地解决这一知识鸿沟，全面阐述如何构建、验证和应用物理上可靠的[机器学习代理模型](@entry_id:751597)。通过本文的学习，读者将掌握一套从理论到实践的完整方法论。在“原理与机制”一章中，我们将深入探讨代理模型的数学定义，区分其与[降阶模型](@entry_id:754172)的本质不同，并重点介绍两种主流的[物理信息](@entry_id:152556)嵌入策略：将物理作为惩罚项的PINN方法和将物理作为求解器的嵌入式方法。随后，在“应用与跨学科[交叉](@entry_id:147634)”一章中，我们将展示这些原理如何应用于增强[本构模拟](@entry_id:183370)、加速复杂的流固耦合与动力问题求解，以及如何驱动[贝叶斯优化](@entry_id:175791)和[可靠性分析](@entry_id:192790)等前沿应用。最后，“动手实践”部分将引导读者亲身体验如何检验和强制执行模型的物理一致性。

## 原理与机制

在计算岩[土力学](@entry_id:180264)领域，[机器学习代理模型](@entry_id:751597)作为一种强大的工具，旨在加速或替代传统的[高保真度模拟](@entry_id:750285)。然而，为了确保这些数据驱动模型的物理真实性和预测可靠性，必须将深刻的物理原理和力学机制融入其设计、训练和应用的全过程。本章将系统地阐述构建有效[机器学习代理模型](@entry_id:751597)的关键原理与核心机制，从模型的数学定义、物理定律的嵌入方法，到基本物理约束的强制执行，以及这些选择对数值穩定性的影响。

### 代理模型的定义与应用[范式](@entry_id:161181)

在深入探讨物理原理之前，我们首先需要精确定义[机器学习代理模型](@entry_id:751597)在计算力学中的角色，并将其与相关[模型降阶](@entry_id:171175)方法区分开来。

#### 代理模型与降阶模型的区别

一个典型的岩[土力学](@entry_id:180264)问题可以被抽象为一个输入到输出的映射。输入通常包括材料参数、荷载、边界条件等，而输出则是我们关心的物理场，如[位移场](@entry_id:141476)或应[力场](@entry_id:147325)。高保真度求解器（如有限元法，FEM）通过求解控制[偏微分方程](@entry_id:141332)（PDE）来完成这一映射，但其计算成本可能非常高昂。

**机器学习 (ML) 代理模型** 本质上是一个数据驱动的函数逼近器。它将高保真度求解器视为一个“黑箱”，旨在直接学习从输入到输出的映射关系。具体而言，代理模型是一个[参数化](@entry_id:272587)映射 $\widehat{\mathcal{S}}_{\boldsymbol{\phi}}: \text{输入} \mapsto \text{输出}$，其可训练参数 $\boldsymbol{\phi}$ 是通过最小化代理模型预测与高保真度求解器产生的一系列“输入-输出”样本对之间的差异来学习的。关键在于，在预测阶段（或称为查询阶段），训练好的代理模型通过一次快速的[前向传播](@entry_id:193086)直接给出预测结果，而**不再求解**控制物理方程。物理信息仅仅**隐式地**编码在用于训练的数据集中 [@problem_id:3540251]。

相比之下，**[降阶模型](@entry_id:754172) (Reduced Order Model, ROM)**，尤其是[基于投影的ROM](@entry_id:753808)，是一种**侵入式**的物理驱动方法。它首先通过对一组高保真度解（称为“快照”）进行分析（如[本征正交分解](@entry_id:165074), POD），构建一个低维的[解空间](@entry_id:200470)基底。然后，通过将原始的控制方程（如有限元系统 $\mathbf{K}(\boldsymbol{\theta}) \mathbf{u} = \mathbf{f}$）投影到这个低维[子空间](@entry_id:150286)上，得到一个规模小得多的[方程组](@entry_id:193238)。在查询阶段，ROM需要**求解**这个降阶后的物理[方程组](@entry_id:193238)来获得解的降维坐标，然后再重构出全维度的近似解。因此，ROM在预测时仍然强制执行了（投影意义下的）物理定律 [@problem_id:3540251]。

简而言之，ML代理模型学习的是“解的映射”，而ROM学习的是“方程的低维空间”。

#### 代理模型的应用合理性：精度与效率的权衡

用ML代理模型替代[高保真度模拟](@entry_id:750285)的决策，必须基于对精度和[计算效率](@entry_id:270255)的审慎权衡。这个决策过程本身就是一个需要定量分析的科学问题。

首先，**精度控制**是前提。代理模型的最终误差来源于两个部分：(1) 高保真度模型（如FEM）相对于真实物理过程的[离散化误差](@entry_id:748522)，我们记作 $\eta_h$；(2) ML代理模型相对于高保真度模型的[泛化误差](@entry_id:637724)，记作 $\delta$。假设我们的工程设计要求最终预测解 $\hat{u}$ 相对于真实解 $u$ 的误差在某个范数（如[能量范数](@entry_id:274966) $\|\cdot\|_E$）下不超过容忍度 $\varepsilon$。根据范数的[三角不等式](@entry_id:143750)，总误差可以被界定为：
$$
\|u - \hat{u}\|_E \le \|u - u_h\|_E + \|u_h - \hat{u}\|_E \le \eta_h + \delta
$$
因此，只有当 $\eta_h + \delta \le \varepsilon$ 时，使用代理模型在认识论上才是合理的。例如，在一个具体的岩土设计场景中，若FEM的[后验误差估计](@entry_id:167288)为 $\|\boldsymbol{u} - \boldsymbol{u}_h\|_E \le 5 \times 10^{-3}$，代理模型的[泛化误差](@entry_id:637724)为 $\|\boldsymbol{u}_h - \hat{\boldsymbol{u}}\|_E \le 4 \times 10^{-3}$，而设计安全容忍度为 $\varepsilon = 10^{-2}$，那么由于 $5 \times 10^{-3} + 4 \times 10^{-3} = 9 \times 10^{-3} \le 10^{-2}$，代理模型的精度满足要求 [@problem_id:3540269]。

其次，**计算效率**是动机。代理模型的优势在于其极低的单次查询成本 $C_{\mathrm{sur}}$，但需要付出昂贵的离线训练成本 $C_{\mathrm{off}}$。与之相比，高保真度模型虽无需训练，但单次求解成本 $C_{\mathrm{FEM}}$ 很高。对于需要进行 $M$ 次查询的应用（如[不确定性量化](@entry_id:138597)或[设计优化](@entry_id:748326)），采用代理模型的总成本为 $T_{\mathrm{surrogate}} = C_{\mathrm{off}} + M \cdot C_{\mathrm{sur}}$，而完全使用高保真度模型的总成本为 $T_{\mathrm{FEM}} = M \cdot C_{\mathrm{FEM}}$。只有当 $M$ 足够大，使得 $T_{\mathrm{surrogate}}  T_{\mathrm{FEM}}$ 时，才具有经济性。我们可以计算出“盈亏[平衡点](@entry_id:272705)”的查询次数 $M^\star$：
$$
M^\star = \frac{C_{\mathrm{off}}}{C_{\mathrm{FEM}} - C_{\mathrm{sur}}}
$$
当预期查询次数 $M > M^\star$ 时，使用代理模型才具有净收益。例如，若 $C_{\mathrm{off}} = 10^5\,\mathrm{s}$, $C_{\mathrm{FEM}} = 500\,\mathrm{s}$, $C_{\mathrm{sur}} = 0.5\,\mathrm{s}$，则 $M^\star \approx 200.2$。如果需要进行 $M=300$ 次查询，那么使用代理模型是合理的，其净加速比为 $S_{\mathrm{net}} = \frac{M C_{\mathrm{FEM}}}{C_{\mathrm{off}} + M C_{\mathrm{sur}}} \approx 1.50$ [@problem_id:3540269]。

### [物理信息](@entry_id:152556)的嵌入方法

将物理定律嵌入ML代理模型是确保其泛化能力和物理真实性的核心。主流方法可分为两大类：将物理定律作为惩罚项的方法，和将物理定律作为求解器的方法。

#### 将物理作为惩罚：[物理信息神经网络](@entry_id:145229)（PINN）

**物理信息神经网络 (Physics-Informed Neural Network, PINN)** 是一种优雅的框架，它将[神经网](@entry_id:276355)络的函数逼近能力与物理定律的数学形式直接结合。其核心思想是将待求解的物理场（如位移 $\boldsymbol{u}(\boldsymbol{x},t)$ 和[孔隙水压力](@entry_id:753587) $p(\boldsymbol{x},t)$）直接[参数化](@entry_id:272587)为[神经网](@entry_id:276355)络的输出，例如 $\hat{\boldsymbol{u}}(\boldsymbol{x},t;\boldsymbol{\theta})$ 和 $\hat{p}(\boldsymbol{x},t;\boldsymbol{\theta})$。然后，通过最小化一个复合[损失函数](@entry_id:634569)来训练网络参数 $\boldsymbol{\theta}$，该损失函数包括：

1.  **控制方程残差**：将网络输出代入PDE，其结果应趋于零。
2.  **边界条件残差**：网络输出在边界上应满足给定的Dirichlet或[Neumann条件](@entry_id:165471)。
3.  **初始条件残差**：对于瞬态问题，网络输出在初始时刻应满足给定的初始条件。

以岩土工程中经典的**Biot[固结理论](@entry_id:747736)**为例，这是一个描述饱和[多孔介质](@entry_id:154591)中[流固耦合](@entry_id:171183)行为的瞬态问题。其控制方程包括力学[平衡方程](@entry_id:172166)和流体质量守恒方程。对于一个小应变、准静态、线性 poroelastic 问题，其强形式[方程组](@entry_id:193238)为 [@problem_id:3540256]：

-   **力学平衡方程**（动量守恒）：
    $$
    \nabla \cdot \big(\boldsymbol{\sigma}'(\boldsymbol{u}) - \alpha\,p\,\boldsymbol{I}\big) + \boldsymbol{b} = \boldsymbol{0}
    $$
    其中 $\boldsymbol{\sigma}'(\boldsymbol{u}) = \mathbb{C}:\boldsymbol{\varepsilon}(\boldsymbol{u})$ 是[有效应力](@entry_id:198048)，$\boldsymbol{\varepsilon}(\boldsymbol{u})$ 是[应变张量](@entry_id:193332)，$p$ 是孔压，$\alpha$ 是[Biot系数](@entry_id:183813)，$\boldsymbol{b}$ 是体力。

-   **流体[质量守恒](@entry_id:204015)方程**：
    $$
    \alpha\,\dot{\varepsilon}_v(\boldsymbol{u}) + \frac{1}{M}\,\dot{p} - \nabla \cdot \Big(\frac{k}{\mu}\,\nabla p\Big) = q
    $$
    其中 $\varepsilon_v = \operatorname{tr}(\boldsymbol{\varepsilon})$ 是体积应变，上标点表示对时间的导数，$M$ 是[Biot模量](@entry_id:746835)，$k$ 是渗透率，$\mu$ 是[流体粘度](@entry_id:267219)，$q$ 是流体源。

一个PINN代理模型需要定义相应的损失项来惩罚对这些定律的违反。例如，动量和[质量守恒](@entry_id:204015)的残差损失项（以[均方误差](@entry_id:175403)MSE计）可以写成 [@problem_id:3540250]：
$$
L_{\mathrm{mom}} = \mathrm{MSE}_{\mathcal{D}_{\Omega}}\left(\nabla \cdot \boldsymbol{\sigma}'(\hat{\boldsymbol{u}}) - \alpha \nabla \hat{p} + \boldsymbol{b}\right)
$$
$$
L_{\mathrm{mass}} = \mathrm{MSE}_{\mathcal{D}_{\Omega}}\left(\frac{1}{M}\frac{\partial \hat{p}}{\partial t} + \alpha \frac{\partial}{\partial t}\left(\nabla \cdot \hat{\boldsymbol{u}}\right) - \nabla \cdot \left(\frac{\boldsymbol{k}}{\mu}\nabla \hat{p}\right) - q\right)
$$
其中 $\mathcal{D}_{\Omega}$ 是在时空域内采样的[配置点](@entry_id:169000)集。类似地，所有的边界条件（位移、应力、压力、流量）和初始条件（初始位移、初始压力）都必须转化为相应的MSE损失项。总损失函数是所有这些残差项的加权和。

一个关键的挑战是**损失项的加权**。力学和[流体流动](@entry_id:201019)方程的物理单位和数值尺度差异巨大，简单的等权[重求和](@entry_id:275405)会导致训练过程被某个尺度最大的损失项主导，而其他物理规律则被忽略。有效的加权策略至关重要，常见的包括：
- **量纲归一化**：在构建[损失函数](@entry_id:634569)之前，对所有变量和方程进行无量纲化处理，使各項在量级上具有可比性。
- **[自适应加权](@entry_id:638030)**：在训练过程中动态调整权重，例如通过平衡不同损失项的梯度范数，或使用基于不确定性的方法，为每个损失项分配一个可学习的噪声参数，权重与其成反比 [@problem_id:3540250]。

#### 将物理作为求解器：嵌入式本构代理

PINN将整个物理问题转化为一个[优化问题](@entry_id:266749)，而另一种[范式](@entry_id:161181)则是将[机器学习模型](@entry_id:262335)仅用于替代系统中计算最昂贵或形式最复杂的部分，通常是**本构关系**。在这种**混合**或**嵌入式**方法中，代理模型 $\boldsymbol{\sigma}_{\boldsymbol{\phi}}(\boldsymbol{\varepsilon})$ 学习从应变到应力的映射，然后被嵌入到一个传统的有限元求解器中。

在这种框架下，物理定律的执行方式截然不同 [@problem_id:3540246]：
- **内部循环（求解器）**：对于一组给定的[本构模型](@entry_id:174726)参数 $\boldsymbol{\phi}$，FE求解器通过求解（离散化的）弱形式平衡方程（如 $\mathbf{R}(\mathbf{u},\boldsymbol{\phi}) = \mathbf{0}$）来严格执行动量守恒。Dirichlet和[Neumann边界条件](@entry_id:142124)被作为[本质边界条件和自然边界条件](@entry_id:168198)在求解过程中被**强制**满足。
- **外部循环（训练）**：训练的目标是优化本构参数 $\boldsymbol{\phi}$。其[损失函数](@entry_id:634569)**不包含**PDE或边界条件的残差项，因为这些已由内部求解器负责。相反，[损失函数](@entry_id:634569)度量的是模型在更高层次上的表现，例如：
    - **材料数据拟合**：$\mathcal{L}_{\mathrm{data}}(\boldsymbol{\phi}) = \sum_j \|\boldsymbol{\sigma}_{\boldsymbol{\phi}}(\boldsymbol{\varepsilon}_j) - \boldsymbol{\sigma}_j^{\mathrm{exp}}\|^2$，即在应力-应变层面上与实验数据匹配。
    - **[系统响应](@entry_id:264152)匹配**：$\mathcal{L}_{\mathrm{resp}}(\boldsymbol{\phi}) = \| \mathbf{y}_{\mathrm{pred}}(\boldsymbol{\phi}) - \mathbf{y}_{\mathrm{obs}} \|^2$，即在整个系统响应层面上（如边界反力或特定点的位移）与观测值匹配。

这种“物理作为求解器”的方法，将数值方法的严谨性与机器学习的灵活性结合起来，尤其适用于学习复杂的[非线性](@entry_id:637147)、历史依赖的材料行为。

### 保证基本的物理原理

无论采用何种[范式](@entry_id:161181)，一个可靠的代理模型都必须遵守材料行为的基本物理原理。这些原理通常作为“硬约束”通过模型架构本身来强制执行，而不是作为“软约束”通过损失函数来鼓励。

#### [热力学一致性](@entry_id:138886)

对于耗散材料（如[弹塑性](@entry_id:193198)或[粘弹性材料](@entry_id:194223)），任何本构模型都必须满足热力学第二定律，即在任何过程中，材料的耗散必须是非负的。

对于[等温过程](@entry_id:143096)，这具体表现为**[Clausius-Duhem不等式](@entry_id:193424)**。从[热力学](@entry_id:141121)第一和第二定律出发，可以推导出，对于一个由应变 $\boldsymbol{\varepsilon}$ 和一组内变量 $\mathbf{z}$ 描述状态的材料，其[耗散率](@entry_id:748577) $\mathcal{D}$ 必须满足 [@problem_id:3540287]：
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$
其中 $\psi(\boldsymbol{\varepsilon}, \mathbf{z})$ 是Helmholtz自由能密度。通过Coleman-Noll程序，这可以分解为两个条件：
1.  **[状态方程](@entry_id:274378)**：应力是自由能对应变的[偏导数](@entry_id:146280)，$\boldsymbol{\sigma} = \frac{\partial\psi}{\partial\boldsymbol{\varepsilon}}$。这定义了响应的弹性（可恢复）部分。
2.  **[耗散不等式](@entry_id:188634)**：$\mathbf{Y} \cdot \dot{\mathbf{z}} \ge 0$，其中 $\mathbf{Y} = -\frac{\partial\psi}{\partial\mathbf{z}}$ 是与内变量 $\mathbf{z}$ 共轭的[热力学力](@entry_id:161907)。

为了在代理模型中强制执行这些条件，可以采用**基于势的架构**：
- **构建自由能势 $\psi$**：使用保证 convexity 的[网络架构](@entry_id:268981)，如**输入凸[神经网](@entry_id:276355)络 (Input Convex Neural Network, ICNN)**，来表示自由能 $\psi$。然后通过[自动微分](@entry_id:144512)精确计算应力 $\boldsymbol{\sigma}$ 和[热力学力](@entry_id:161907) $\mathbf{Y}$。
- **构建耗散势 $\phi$**：定义一个关于内变量率 $\dot{\mathbf{z}}$ 的[凸函数](@entry_id:143075) $\phi(\dot{\mathbf{z}})$ 作为耗散势，并规定演化法则遵循正交流动法则，如 $\mathbf{Y} \in \partial \phi(\dot{\mathbf{z}})$。这种构造保证了耗散非负。
- 一个更简单的特例是，假设线性的流动关系 $\mathbf{Y} = \mathbf{L}\dot{\mathbf{z}}$。此时耗散为 $\mathcal{D} = \dot{\mathbf{z}}^\top \mathbf{L} \dot{\mathbf{z}}$。只要保证矩阵 $\mathbf{L}$ 是对称半正定的（例如，通过[Cholesky分解](@entry_id:147066)[参数化](@entry_id:272587) $\mathbf{L} = \mathbf{M}^\top\mathbf{M}$），耗散非负性就能得到保证 [@problem_id:3540287]。

对于简单的[线性粘弹性](@entry_id:181219)模型，如[Kelvin-Voigt模型](@entry_id:195229) $\boldsymbol{\sigma} = \mathbb{C}\boldsymbol{\varepsilon} + \boldsymbol{\eta}\dot{\boldsymbol{\varepsilon}}$，其耗散为 $\mathcal{D} = \dot{\boldsymbol{\varepsilon}}:\boldsymbol{\eta}:\dot{\boldsymbol{\varepsilon}}$。只要粘性张量 $\boldsymbol{\eta}$ 是半正定的，[热力学一致性](@entry_id:138886)就得以满足 [@problem_id:3540287]。

#### 材料[坐标系](@entry_id:156346)无关性（客观性）

[本构关系](@entry_id:186508)描述的是材料的内在属性，它不应依赖于观察者所处的[坐标系](@entry_id:156346)。这一原理称为**材料[坐标系](@entry_id:156346)无关性**或**客观性 (objectivity)**。对于小应变问题，这表现为在[刚体转动](@entry_id:191086)下的**旋转[等变性](@entry_id:636671) (rotational equivariance)**。若一个刚性转动由[旋转矩阵](@entry_id:140302) $\mathbf{Q} \in \mathrm{SO}(3)$ 描述，则应变和[应力张量](@entry_id:148973)会相应地变换为 $\boldsymbol{\varepsilon} \mapsto \mathbf{Q}\boldsymbol{\varepsilon}\mathbf{Q}^\top$ 和 $\boldsymbol{\sigma} \mapsto \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^\top$。客观性要求本构映射函数 $\mathcal{F}$ 满足：
$$
\mathcal{F}(\mathbf{Q}\boldsymbol{\varepsilon}\mathbf{Q}^\top) = \mathbf{Q}\mathcal{F}(\boldsymbol{\varepsilon})\mathbf{Q}^\top
$$
在代理模型中强制执行此属性的有效策略包括 [@problem_id:3540263]：
1.  **基于[不变量](@entry_id:148850)的表示 (适用于[各向同性材料](@entry_id:170678))**：将应变张量 $\boldsymbol{\varepsilon}$ 分解为其[旋转不变量](@entry_id:170459)（如[主应变](@entry_id:197797)，或迹、[偏应变](@entry_id:201263)二阶矩、[行列式](@entry_id:142978)等[标量不变量](@entry_id:193787)）和旋转本身。模型的核心部分仅学习[不变量](@entry_id:148850)到[不变量](@entry_id:148850)的映射（如[主应变](@entry_id:197797)到[主应力](@entry_id:176761)）。最后，利用旋转信息重构出完整的应力张量。例如，应力可以表示为张量基 $\{ \mathbf{I}, \boldsymbol{\varepsilon}, \boldsymbol{\varepsilon}^2 \}$ 的线性组合，其系数是关于 $\boldsymbol{\varepsilon}$ 的[标量不变量](@entry_id:193787)的函数。
2.  **谱分解方法 (适用于各向同性材料)**：对输入应变张量 $\boldsymbol{\varepsilon}$ 进行[特征分解](@entry_id:181333)，得到[特征值](@entry_id:154894)（[主应变](@entry_id:197797)） $\boldsymbol{\Lambda}$ 和[特征向量](@entry_id:151813)（[主方向](@entry_id:276187)） $\mathbf{V}$。用一个[神经网](@entry_id:276355)络学习[主应力](@entry_id:176761)与[主应变](@entry_id:197797)之间的关系 $\boldsymbol{\sigma}_p = g(\boldsymbol{\Lambda})$。由于[主应变](@entry_id:197797)是[旋转不变量](@entry_id:170459)，主应力也只依赖于它們。最后，利用相同的[主方向](@entry_id:276187)重构[应力张量](@entry_id:148973) $\boldsymbol{\sigma} = \mathbf{V} \boldsymbol{\sigma}_p \mathbf{V}^\top$。这种方法通过架构保证了各向同性响应的旋转[等变性](@entry_id:636671)。
3.  **[等变神经网络](@entry_id:137437)层**：采用专门设计的群等变（Group-equivariant）[神经网](@entry_id:276355)络层，这些层在数学上被构造成天然满足对 $\mathrm{SO}(3)$ 群作用的[等变性](@entry_id:636671)。这是最通用和强大的方法，适用于各向同性及各向异性材料。

值得注意的是，仅通过[数据增强](@entry_id:266029)（即用随机旋转的数据扩充[训练集](@entry_id:636396)）来学习客观性是一种“软”方法，它不能**保证**在所有旋转下都精确满足[等变性](@entry_id:636671)，而只能在统计意义上近似 [@problem_id:3540263]。

#### [材料稳定性](@entry_id:183933)

为了保证[数值模拟](@entry_id:137087)的稳定性，本构模型必须是材料稳定的。根据**[Drucker稳定性公设](@entry_id:200080)**，对于一个稳定的[弹塑性](@entry_id:193198)材料，在任何塑性加载过程中，应力增量 $d\boldsymbol{\sigma}$ 与塑性应变增量 $d\boldsymbol{\varepsilon}^{\mathrm{p}}$ 的[内积](@entry_id:158127)必须非负，即 $d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^{\mathrm{p}} \ge 0$。

一个更通用的[稳定性判据](@entry_id:755304)是要求在任何应变增量 $d\boldsymbol{\varepsilon}$ 作用下，材料的二阶功 $d^2W = \frac{1}{2} d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}$ 必须非负。这导致了对（算法）[切线刚度](@entry_id:166213)张量 $\mathbb{C}_{\mathrm{alg}} = \frac{\partial \boldsymbol{\sigma}}{\partial \boldsymbol{\varepsilon}}$ 的一个关键要求。在Voigt表示下，[切线刚度](@entry_id:166213)是一个矩阵 $\mathbf{C}$，二阶功为 $\frac{1}{2} (d\boldsymbol{\varepsilon})^\top \mathbf{C} (d\boldsymbol{\varepsilon})$。该二次型仅依赖于 $\mathbf{C}$ 的对称部分 $\mathbf{C}_{\mathrm{s}} = \frac{1}{2}(\mathbf{C} + \mathbf{C}^\top)$。因此，[材料稳定性](@entry_id:183933)要求 $\mathbf{C}_{\mathrm{s}}$ 必须是**半正定**的 [@problem_id:3540324]。

对于一个输出[切线刚度矩阵](@entry_id:170852)的ML代理模型，我们可以通过计算其对称部分的最小特征值来检验其是否满足稳定性。如果[最小特征值](@entry_id:177333)为非负，则模型在该状态下是稳定的。例如，对于一个预测的平面应变[切线刚度矩阵](@entry_id:170852)（单位GPa）：
$$
\mathbf{C}^{\mathrm{ML}} = 
\begin{pmatrix}
12   5   0.2 \\
4   10  0.3 \\
0   0   3
\end{pmatrix}
$$
我们首先计算其对称部分：
$$
\mathbf{C}_{\mathrm{s}} = \begin{pmatrix}
12   4.5  0.1 \\
4.5  10   0.15 \\
0.1  0.15  3
\end{pmatrix}
$$
通过计算，该矩阵的最小特征值约为 $2.997$ GPa。由于所有[特征值](@entry_id:154894)均为正，该代理模型预测的[切线刚度](@entry_id:166213)满足[材料稳定性](@entry_id:183933)要求 [@problem_id:3540324]。

### 数值考量：硬约束与软约束

在PINN或嵌入式代理模型的训练中，上述物理原理的实施方式对[优化问题](@entry_id:266749)的** conditioning **和收敛行为有深远影响。

**硬约束 (Hard constraint)** 指的是通过[模型参数化](@entry_id:752079)或架构设计来**先验地**强制满足物理约束。例如，使用[Cholesky分解](@entry_id:147066)来参数化一个[对称正定](@entry_id:145886)张量，或使用ICNN来构建凸函数。硬约束的优点在于，它将优化搜索空间限制在物理上有意义的范围内。对于如线弹性这类由[双线性形式](@entry_id:746794) $a(u,v) = \int_{\Omega} \varepsilon(u) : C : \varepsilon(v) \, dx$ 定义的问题，强制 $C$ 的[对称正定](@entry_id:145886)性保证了算子的**矫顽性 (coercivity)**。这反过来保证了物理问题本身的良定性，并使得[优化问题](@entry_id:266749)的[损失景观](@entry_id:635571)更加良好，避免了由于物理简并（如刚度为零）而导致的病态（即雅可比矩阵出现接近零的奇异值）[@problem_id:3540320]。

**软约束 (Soft constraint)** 指的是将违反物理约束的度量作为惩罚项加入到[损失函数](@entry_id:634569)中。例如，添加惩罚项 $R_{\mathrm{pd}}(C) = \sum_{i} \max(0,-\lambda_i(C))^2$ 来鼓励 $C$ 的正定性。软约束的缺点在于，它允许优化器在训练过程中暂时进入物理上不允许的区域。当模型参数进入使物理问题变得病态或不适定的区域时（例如，$C$ 失去[正定性](@entry_id:149643)），[优化问题](@entry_id:266749)的 conditioning 会急剧恶化，导致梯度消失或爆炸，从而使训练停滞。若试图通过设置极大的惩罚权重来避免这种情况，又会引发新的问题：[损失函数](@entry_id:634569)的不同项之间尺度差异过大，同样导致Hessian[矩阵的条件数](@entry_id:150947)过大，损害收敛性 [@problem_id:3540320]。

因此，从[数值稳定性](@entry_id:146550)和收敛效率的角度看，只要可行，**硬约束**通常是比软约束更优越的选择。它将先验物理知识牢固地嵌入模型结构中，从而构建了一个更稳定、更易于优化的学习问题。

最后，选择合适的**误差度量**也至关重要。对于输出场的代理模型，仅控制位移的 $L^2$ 范数误差 $\int_{\Omega}|\hat{\boldsymbol{u}}-\boldsymbol{u}^\star|^2 d\Omega$ 是不够的，因为它不控制梯度的误差，从而无法保证应变或应力误差足够小。**能量范数**误差，$\int_{\Omega}\boldsymbol{\varepsilon}(\hat{\boldsymbol{u}}-\boldsymbol{u}^\star):\mathbb{C}:\boldsymbol{\varepsilon}(\hat{\boldsymbol{u}}-\boldsymbol{u}^\star) d\Omega$，直接度量了应变误差，因此是更有物理意义的度量。有趣的是，对于满足运动学边界条件的近似解 $\hat{\boldsymbol{u}}$，其[能量范数误差](@entry_id:170379)与总[势能](@entry_id:748988)的误差之间存在精确关系：$\|\hat{\boldsymbol{u}}-\boldsymbol{u}^\star\|_{E}^2=2\big(J(\hat{\boldsymbol{u}})-J(\boldsymbol{u}^\star)\big)$，这为误差评估提供了深刻的物理联系 [@problem_id:3540253]。