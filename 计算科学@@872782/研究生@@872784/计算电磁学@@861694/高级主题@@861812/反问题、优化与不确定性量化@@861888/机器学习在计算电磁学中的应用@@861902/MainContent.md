## 引言
计算电磁学作为现代科学与工程的基石，其核心挑战之一是传统数值方法（如[有限元法](@entry_id:749389)和[时域有限差分法](@entry_id:141865)）带来的巨大计算开销。近年来，机器学习以其强大的数据拟合与[模式识别](@entry_id:140015)能力，为加速[电磁仿真](@entry_id:748890)和解决复杂设计问题带来了新的希望。然而，一个关键的知识鸿沟随之出现：纯数据驱动的“黑箱”模型往往缺乏物理一致性，其预测结果可能违背基本的电磁学定律，限制了其在严谨科学研究与高[可靠性工程](@entry_id:271311)应用中的价值。

本文旨在系统性地解决这一问题，深入探讨如何将机器学习与电磁学的物理原理进行深度融合，即所谓的“物理感知机器学习”。读者将学习到，这种融合远不止于数据拟合，而是要将深刻的物理洞察力[植入](@entry_id:177559)模型的“基因”之中。

本文将通过以下三个章节，引领读者全面掌握这一前沿领域：
*   **原理与机制**：本章将深入剖析核心技术，阐述如何通过[物理信息神经网络](@entry_id:145229)（[PINNs](@entry_id:145229)）将控制方程编码至[损失函数](@entry_id:634569)，如何通过特殊[网络架构](@entry_id:268981)植入互易性和旋转[等变性](@entry_id:636671)等对称性，以及如何利用伴随方法实现传统求解器的可微化。
*   **应用与[交叉](@entry_id:147634)学科联系**：本章将展示这些原理在实际问题中的强大威力，包括构建快速且物理一致的代理模型，利用学习到的先验知识增强[逆散射](@entry_id:182338)成像，以及自动化复杂的[多物理场仿真](@entry_id:145294)工作流。
*   **动手实践**：本章提供了一系列精心设计的编程练习，引导读者亲手实现伴随状态法、构建物理归纳的图神经网络以及训练用于诊断伪模的分类器，将理论知识转化为实践能力。

通过本文的学习，读者将能够理解并应用这些先进方法，从而在自己的研究与工作中，更高效、更可靠地解决[计算电磁学](@entry_id:265339)中的挑战性问题。

## 原理与机制

本章在前一章介绍的基础上，深入探讨了将机器学习应用于[计算电磁学](@entry_id:265339)的核心科学原理和实现机制。[现代机器学习](@entry_id:637169)方法在计算科学中的成功，已远超纯粹数据驱动的“黑箱”预测。其真正的威力在于能够将深刻的物理定律、对称性和数学结构融入模型的设计与训练过程中。这种“物理感知”的方法不仅能显著提高模型的准确性、泛化能力和数据效率，还能保证其预测结果在物理上是合理和一致的。本章将系统地阐述如何实现这一点，重点关注控制方程的编码、[基本对称性](@entry_id:161256)的[植入](@entry_id:177559)、因果性约束的满足，以及[机器学习模型](@entry_id:262335)与传统数值求解器的深度融合。

### 编码控制方程：物理信息神经网络方法

将物理学知识融入机器学习模型的最直接方法之一，是强制模型输出严格遵守其所描述系统的基本控制方程。**物理信息神经网络 (Physics-Informed Neural Networks, PINNs)** 正是实现这一目标的强大框架。其核心思想是将[偏微分方程](@entry_id:141332) (PDEs)、边界条件 (BCs) 和[初始条件](@entry_id:152863) (ICs) 直接作为惩罚项加入[神经网](@entry_id:276355)络的损失函数中。

我们以无源区域中的时域麦克斯韦方程组为例来说明这一概念。考虑在一个有界区域 $\Omega \subset \mathbb{R}^3$ 内，[电场](@entry_id:194326) $\mathbf{E}(\mathbf{x}, t)$ 和[磁场](@entry_id:153296) $\mathbf{H}(\mathbf{x}, t)$ 的演化由以下方程决定：
$$
\nabla \times \mathbf{E} + \frac{\partial \mathbf{B}}{\partial t} = 0 \quad (\text{法拉第定律})
$$
$$
\nabla \times \mathbf{H} - \frac{\partial \mathbf{D}}{\partial t} = 0 \quad (\text{安培-麦克斯韦定律})
$$
其中，[本构关系](@entry_id:186508)为 $\mathbf{D} = \boldsymbol{\epsilon}(\mathbf{x})\mathbf{E}$ 和 $\mathbf{B} = \boldsymbol{\mu}(\mathbf{x})\mathbf{H}$。

在PINN框架中，我们不再试图直接从数据中学习场到场的映射，而是用两个[神经网](@entry_id:276355)络 $\mathbf{E}_\theta(\mathbf{x}, t)$ 和 $\mathbf{H}_\theta(\mathbf{x}, t)$ 来直接逼近时空中的[电磁场](@entry_id:265881)解本身，其中 $\theta$ 是网络的可训练参数。这些网络的输入是时空坐标 $(\mathbf{x}, t)$，输出是该点的场矢量。

PINN的关键技术是**[自动微分](@entry_id:144512) (Automatic Differentiation, AD)**。通过AD，我们可以精确计算网络输出相对于其输入的任意阶导数，例如旋度 ($\nabla \times$) 和时间[偏导数](@entry_id:146280) ($\partial_t$)。这使得我们能够定义**物理残差 (physics residuals)**，即[神经网](@entry_id:276355)络输出代入控制方程后产生的不平衡量：
$$
\mathbf{r}_F(\mathbf{x},t) = \nabla\times \mathbf{E}_\theta(\mathbf{x},t) + \frac{\partial}{\partial t} \left(\boldsymbol{\mu}(\mathbf{x})\mathbf{H}_\theta(\mathbf{x},t)\right)
$$
$$
\mathbf{r}_A(\mathbf{x},t) = \nabla\times \mathbf{H}_\theta(\mathbf{x},t) - \frac{\partial}{\partial t} \left(\boldsymbol{\epsilon}(\mathbf{x})\mathbf{E}_\theta(\mathbf{x},t)\right)
$$
一个完美的解应该使这些残差在整个时空域内处处为零。因此，我们可以将这些残差的$L_2$范数平方的积分作为[损失函数](@entry_id:634569)的一部分，以驱动网络学习满足麦克斯韦方程的解。

除了内部的物理定律，一个适定的[边值问题](@entry_id:193901)还需要边界条件。例如，在边界 $\partial\Omega$ 上可能规定了[切向电场](@entry_id:267195)（狄利克雷型边界条件）或切向[磁场](@entry_id:153296)（诺伊曼型边界条件）：
$$
\mathbf{n}(\mathbf{x})\times \mathbf{E}(\mathbf{x},t) = \mathbf{g}_D(\mathbf{x},t) \quad \text{on } \partial\Omega
$$
$$
\mathbf{n}(\mathbf{x})\times \mathbf{H}(\mathbf{x},t) = \mathbf{g}_N(\mathbf{x},t) \quad \text{on } \partial\Omega
$$
其中 $\mathbf{n}$ 是边界外法向单位矢量。这些条件同样可以作为损失项被包含进来，通过惩罚网络预测的边界值与给定函数 $\mathbf{g}_D$ 或 $\mathbf{g}_N$ 之间的偏差。初始条件，即 $t=0$ 时刻的场[分布](@entry_id:182848)，也以类似的方式处理。

综合起来，一个针对时域麦克斯韦方程的完整[PINN损失函数](@entry_id:137288) $\mathcal{L}(\theta)$ 可以构建为内部残差、边界条件残差和[初始条件](@entry_id:152863)残差的加权和 [@problem_id:3327836]：
$$
\mathcal{L}(\theta) = w_{pde} \mathcal{L}_{pde} + w_{bc} \mathcal{L}_{bc} + w_{ic} \mathcal{L}_{ic}
$$
其中，例如，
$$
\mathcal{L}_{pde} = \int_0^T \int_{\Omega} \left( \|\mathbf{r}_F\|_2^2 + \|\mathbf{r}_A\|_2^2 \right) \mathrm{d}\mathbf{x}\mathrm{d}t
$$
$$
\mathcal{L}_{bc} = \int_0^T \int_{\partial\Omega} \|\mathbf{n}\times \mathbf{E}_\theta - \mathbf{g}_D\|_2^2 \mathrm{d}s\mathrm{d}t
$$
在实践中，这些积分通过在时空域内部、边界和初始时刻[随机采样](@entry_id:175193)的**[配置点](@entry_id:169000) (collocation points)** 上的均值来近似，这是一种[蒙特卡洛积分](@entry_id:141042)方法。通过最小化总损失函数 $\mathcal{L}(\theta)$，[神经网](@entry_id:276355)络被训练成一个能够近似满足整个物理问题（PDEs、BCs、ICs）的[连续函数](@entry_id:137361)。

### [植入](@entry_id:177559)[基本对称性](@entry_id:161256)与不变性

物理定律通常表现出深刻的对称性，例如互易性、[旋转不变性](@entry_id:137644)和规范不变性。如果一个[机器学习模型](@entry_id:262335)能够在其架构中内在地尊重这些对称性，它不仅能更好地泛化到未见过的数据，还能从更少的训练样本中学习，因为它的[解空间](@entry_id:200470)已经被物理原理所约束。

#### 互易性

**互易性 (Reciprocity)** 是[线性时不变](@entry_id:276287) (LTI) 电磁系统的一个基本属性，源于麦克斯韦方程在时间和空间上的对称性。洛伦兹互易性定理指出，在由满足对称本构关系 ($\boldsymbol{\epsilon}^T=\boldsymbol{\epsilon}, \boldsymbol{\mu}^T=\boldsymbol{\mu}$) 的材料构成的系统中，源和场可以互换位置而响应不变。

这一物理原理对机器学习模型施加了具体的数学约束。例如，对于一个N端口网络，互易性要求其[散射矩阵](@entry_id:137017) $S$ 是对称的，即 $S = S^T$ [@problem_id:3327840]。一个未经约束的[神经网](@entry_id:276355)络直接从数据中学习[散射参数](@entry_id:754557)，其预测的矩阵 $\hat{S}$ 很可能不满足此对称性。为了强制模型遵守物理定律，我们可以通过[正交投影](@entry_id:144168)来修正其输出。对于给定的[非对称矩阵](@entry_id:153254) $\hat{S}$，在[弗罗贝尼乌斯范数](@entry_id:143384)意义下，最接近它的[对称矩阵](@entry_id:143130)是其对称部分：
$$
S_{\text{reciprocal}} = \frac{1}{2}(\hat{S} + \hat{S}^T)
$$
将这个投影操作作为网络的一层，可以保证其输出始终是物理上一致的。

同样，对于由体积分方程描述的散射问题，其核心是[格林函数核](@entry_id:750050) $G(\mathbf{r}, \mathbf{r}')$。互易性要求该核函数在源点 $\mathbf{r}'$ 和场点 $\mathbf{r}$ 的交换下是对称的，即 $G(\mathbf{r}, \mathbf{r}') = G(\mathbf{r}', \mathbf{r})$ [@problem_id:3327846]。在设计学习格林函数的[神经网](@entry_id:276355)络时，必须注意这一点。一个常见的错误是将其与[厄米对称性](@entry_id:266311) ($G(\mathbf{r}, \mathbf{r}') = G^*(\mathbf{r}', \mathbf{r})$) 混淆，后者对于描述能量向外辐射的开放系统是**不物理的**。正确的架构设计可以硬性编码这种对称性。例如，可以让网络 $H_\theta$ 学习一个通用的[平滑核](@entry_id:195877)，然后通过后处理 symmetrize 它：
$$
\tilde{H}_{\theta}(\mathbf{r}, \mathbf{r}') = \frac{1}{2}\left(H_{\theta}(\mathbf{r}, \mathbf{r}') + H_{\theta}(\mathbf{r}', \mathbf{r})\right)
$$
这种方法确保了模型输出的对称性，而无需依赖于训练数据隐式地学习到这一属性。

#### 旋转[等变性](@entry_id:636671)

在各向同性介质中，物理定律不应依赖于我们如何选择[坐标系](@entry_id:156346)。如果我们将一个系统旋转，其产生的场也应该相应地旋转。这种性质被称为**旋转[等变性](@entry_id:636671) (rotational equivariance)**。对于一个将输入矢量场 $\mathbf{J}$ 映射到输出矢量场 $\mathbf{E}$ 的操作 $\Phi$，[等变性](@entry_id:636671)要求，对于任意旋转 $R \in \mathrm{SO}(3)$，都有 $\Phi(R\mathbf{J}(R^{-1}\mathbf{r})) = R(\Phi\mathbf{J})(R^{-1}\mathbf{r})$。

当用[卷积神经网络](@entry_id:178973)实现这种映射时，例如 $\mathbf{E} = K * \mathbf{J}$，[等变性](@entry_id:636671)要求对[卷积核](@entry_id:635097) $K(\mathbf{x})$ 施加严格的约束 [@problem_id:3327858]：
$$
K(R\mathbf{x}) = R K(\mathbf{x}) R^{-1}
$$
这意味着当输入[坐标旋转](@entry_id:164444)时，核张量本身也以特定的方式变换。

**[等变神经网络](@entry_id:137437) (Equivariant Neural Networks, ENNs)** 通过利用[群表示论](@entry_id:141930)来构建满足此类约束的层。其核心思想是将场分解为不同角动量（或称不可约表示）的分量，并通过[球谐函数](@entry_id:178380)进行参数化。通过克莱布施-戈登系数所规定的耦合规则，可以精确地确定哪些类型的核（由其球谐度 $\ell$ 表征）可以将特定类型的输入（如矢量，$\ell=1$）映射到特定类型的输出（如矢量，$\ell=1$）。对于矢量到矢量的映射，只有角向阶数 $\ell \in \{0, 1, 2\}$ 的核才是允许的。这种基于群论的架构设计原则，从根本上保证了网络的物理一致性，将先验知识硬编码到模型的结构中。

#### 规范不变性

在电磁理论中，矢量磁势 $\mathbf{A}$ 的选择不是唯一的，任何[标量场](@entry_id:151443) $\phi$ 的梯度都可以加到 $\mathbf{A}$ 上（$\mathbf{A} \to \mathbf{A} + \nabla\phi$）而不会改变[物理可观测量](@entry_id:154692)——[磁场](@entry_id:153296) $\mathbf{B} = \nabla \times \mathbf{A}$。这种自由度被称为**规范不变性 (gauge invariance)**。一个鲁棒的数值或学习模型应当尊重这种[不变性](@entry_id:140168)。

**图神经网络 (Graph Neural Networks, GNNs)** 与**离散[外微分](@entry_id:161900) (Discrete Exterior Calculus, DEC)** 的结合为处理[非结构化网格](@entry_id:756356)上的电磁问题提供了完美的框架。在这个框架中 [@problem_id:3327865]，物理量和算子被离散化到网格的几何元素上：
*   标量场（0-形式）位于节点上。
*   矢量场（1-形式）位于边上。
*   通量场（[2-形式](@entry_id:188008)）位于面上。

微分算子则由元素之间的[关联矩阵](@entry_id:263683)表示：
*   [离散梯度](@entry_id:171970) $D_0$（节点到边）。
*   离散旋度 $D_1$（边到面）。

这些离散算子继承了[连续算子](@entry_id:143297)的一个基本[拓扑性质](@entry_id:141605)：“[边界的边界为零](@entry_id:269907)”，其代数形式为 $D_1 D_0 = 0$。这正是离散版本的恒等式 $\nabla \times (\nabla \phi) = 0$。

如果我们将一个GNN层定义为通过离散[旋度算子](@entry_id:184984) $D_1$ 将边上的矢量势 $A$ 映射到面上的[磁通量](@entry_id:268943) $B$，即 $B = D_1 A$，那么这个层就**自动地、结构上地**满足规范不变性。这是因为对于一个[规范变换](@entry_id:176521) $A' = A + D_0 \phi$，新的[磁通量](@entry_id:268943)为：
$$
B' = D_1 A' = D_1 (A + D_0 \phi) = D_1 A + D_1 D_0 \phi = D_1 A = B
$$
这个结果不依赖于任何训练，而是源于模型架构的正确拓扑构造。相比之下，一个忽略边和面方向的“朴素”GNN 将会违反规范不变性。此外，这个框架还允许我们通过求解一个由[图拉普拉斯算子](@entry_id:275190) $L = D_0^T D_0$ 定义的[泊松方程](@entry_id:143763)来强制执行特定的规范，如[库仑规范](@entry_id:273044)（$\nabla \cdot \mathbf{A} = 0$）。

### 因果性及其对学习模型的影响

**因果性 (Causality)** 是一个基本物理原理，即系统的响应不能先于其受到的激励。对于描述材料响应的[线性时不变系统](@entry_id:276591)，这表现为[冲激响应函数](@entry_id:137098)（或称[磁化率](@entry_id:138219)）$\chi(t)$ 在 $t  0$ 时必须为零。

这个看似简单的时间域约束，在[频域](@entry_id:160070)中却有着深远的影响。它要求材料的[复介电常数](@entry_id:160910) $\epsilon(\omega)$ 或[磁导率](@entry_id:154559) $\mu(\omega)$ 必须是复频率[上半平面](@entry_id:199119)的解析函数。通过应用[柯西积分公式](@entry_id:169692)和[复分析](@entry_id:167282)中的Sokhotski–Plemelj定理，可以推导出连接复响应函数实部和虚部的积分关系，即**[克拉默斯-克勒尼希关系](@entry_id:140966) (Kramers-Kronig relations)** [@problem_id:3327896]。对于[介电常数](@entry_id:146714) $\epsilon(\omega) = \Re\epsilon(\omega) + i\Im\epsilon(\omega)$，其中一个关系式为：
$$
\Re \epsilon(\omega_{0}) = \epsilon_{\infty} + \frac{2}{\pi} \mathcal{P}\!\!\int_{0}^{\infty} \frac{\Omega\,\Im \epsilon(\Omega)}{\Omega^{2}-\omega_{0}^{2}}\,\mathrm{d}\Omega
$$
这里 $\mathcal{P}$ 表示[柯西主值](@entry_id:192761)积分，$\epsilon_{\infty}$ 是无限频率下的[介电常数](@entry_id:146714)。这个关系式与另一个给出虚部的积分式一起，表明[复介电常数](@entry_id:160910)的实部和虚部不是独立的，而是由因果性这一基本原理紧密联系在一起。

当训练一个[神经网](@entry_id:276355)络来学习材料的[色散](@entry_id:263750)特性，即 $\epsilon(\omega)$ 时，可以直接将[克拉默斯-克勒尼希关系](@entry_id:140966)作为一个软约束或正则化项加入到损失函数中。这可以确保学习到的[色散曲线](@entry_id:197598)不仅拟合数据，而且还符合因果性和被动性（$\Im\epsilon(\omega) \ge 0$），从而避免产生非物理的预测。

### 融合机器学习与传统求解器

[机器学习模型](@entry_id:262335)不必完全取代传统的数值求解器，二者可以协同工作。例如，我们可以用机器学习来求解逆问题（如从散射数据推断材料参数），或者加速传统求解器的某个计算瓶颈。这种深度融合的关键在于让整个计算流程变得**可微 (differentiable)**。

#### 可微求解器与伴随方法

假设我们有一个由参数 $\theta$（例如某个区域的[介电常数](@entry_id:146714)）决定的有限元方法 (FEM) 系统 $A(\theta)x = b$，其中 $x$ 是待求解的场。我们的目标是最小化一个依赖于场 $x$ 的损失函数 $L(x)$ 来找到最优的参数 $\theta$。使用梯度下降法需要计算损失对参数的导数 $\frac{dL}{d\theta}$。

通过链式法则，$\frac{dL}{d\theta} = \frac{\partial L}{\partial x} \frac{\partial x}{\partial \theta}$。这里的挑战在于计算 $\frac{\partial x}{\partial \theta}$。我们可以对 $A(\theta)x(\theta)=b$ 两边关于 $\theta$ 求导，利用[隐函数定理](@entry_id:147247)得到 [@problem_id:3327895]：
$$
\frac{\partial x}{\partial \theta} = - A(\theta)^{-1} \frac{\partial A(\theta)}{\partial \theta} x
$$
直接计算这个表达式的代价是高昂的，因为它需要求解一个矩阵的逆 $A^{-1}$，对于大规模系统来说这几乎是不可行的。

**伴随方法 (Adjoint Method)** 提供了一种极其高效的替代方案。它通过引入一个“伴随”变量 $\lambda$ 来避免计算矩阵的逆。总导数可以重写为：
$$
\frac{dL}{d\theta} = - \left( (\nabla_x L)^T A^{-1} \right) \left( \frac{\partial A}{\partial \theta} x \right)
$$
我们定义伴随变量 $\lambda$ 为以下[线性系统](@entry_id:147850)的解：
$$
A^T \lambda = \nabla_x L
$$
这个**伴随系统**的求解代价与求解原始的FEM系统 $Ax=b$ 相当。一旦求得 $\lambda$，梯度就可以通过一个简单的[内积](@entry_id:158127)计算出来：
$$
\frac{dL}{d\theta} = - \lambda^T \frac{\partial A}{\partial \theta} x
$$
这个过程将一个昂贵的[矩阵求逆](@entry_id:636005)问题替换为求解另一个（与原始系统同等规模的）[线性系统](@entry_id:147850)，极大地提高了[计算效率](@entry_id:270255)，使得将复杂的传统求解器嵌入端到端的学习框架成为可能。

#### 学习算子的[误差分析](@entry_id:142477)

当[机器学习模型](@entry_id:262335)被用来学习数值算子本身时，例如一个[有限差分模板](@entry_id:749381)或一个[积分方程](@entry_id:138643)核，我们必须严格分析模型近似误差如何传播到最终的物理场解中。

##### 学习离散化方案的[截断误差](@entry_id:140949)

考虑一个学习到的五点[有限差分模板](@entry_id:749381)，用于近似[一阶导数](@entry_id:749425) $\partial_y u$。该模板的权重 $w_k(\mathbf{x})$ 是空间位置 $\mathbf{x}$ 的函数，由[神经网](@entry_id:276355)络学习得到。通过[泰勒展开](@entry_id:145057)可以发现，为了使该格式的[局部截断误差](@entry_id:147703)达到 $O(h^p)$，权重不仅需要满足一系列代数**[矩条件](@entry_id:136365) (moment conditions)**，而且权重函数 $w_k(\mathbf{x})$ 本身也需要具有一定的空间光滑度 [@problem_id:3327852]。

一个深刻的结论是，最终的[收敛阶](@entry_id:146394)数 $p$ 受限于两个因素的最小值：模板能够满足的最高代数阶数 $M$（由模板点数决定），以及权重函数 $w_k(\mathbf{x})$ 的空间光滑度阶数 $s$。即：
$$
p = \min(M, s)
$$
例如，即使一个[五点模板](@entry_id:174268)在代数上能够达到四阶精度（$M=4$），但如果学习到的权重函数在空间上仅是 $C^3$ 光滑的（$s=3$），那么整个离散化方案的最终精度将被限制在 $O(h^3)$。这揭示了学习化离散格式中，模型的光滑度与[数值精度](@entry_id:173145)之间一个微妙而关键的联系。

##### 学习[积分算子](@entry_id:262332)的[误差传播](@entry_id:147381)

在体[积分方程](@entry_id:138643) (VIE) 方法中，总场 $\mathbf{E}$ 由算子方程 $(I-K)\mathbf{E} = \mathbf{E}_{\mathrm{inc}}$ 决定。如果一个[机器学习模型](@entry_id:262335)学习了一个近似的积分核，从而定义了一个近似的算子 $\hat{K}$，那么得到的近似解 $\hat{\mathbf{E}}$ 的误差是多少？

利用[算子理论](@entry_id:139990)和[诺伊曼级数](@entry_id:191685)，我们可以推导出解的[误差范数](@entry_id:176398) $\|\hat{\mathbf{E}} - \mathbf{E}\|$ 的一个严格[上界](@entry_id:274738) [@problem_id:3327888]。误差满足关系式 $(I-\hat{K})(\hat{\mathbf{E}}-\mathbf{E}) = (\hat{K}-K)\mathbf{E}$。由此可得解的[误差界](@entry_id:139888)为：
$$
\|\hat{\mathbf{E}}-\mathbf{E}\| \le \|(I-\hat{K})^{-1}\| \|\hat{K}-K\| \|\mathbf{E}\|
$$
将[诺伊曼级数](@entry_id:191685)界 $\|(I-A)^{-1}\| \le \frac{1}{1-\|A\|}$ 应用于此，并设 $\|K\|=\alpha$ 和算子误差 $\|\hat{K}-K\|=\epsilon$，我们得到：
$$
\|\hat{\mathbf{E}}-\mathbf{E}\| \le \frac{\epsilon}{(1-\alpha)(1-\alpha-\epsilon)} \|\mathbf{E}_{\mathrm{inc}}\|
$$
这个不等式清晰地量化了[模型误差](@entry_id:175815)（$\epsilon$）如何通过一个依赖于原始问题和扰动问题稳定性的[放大因子](@entry_id:144315)（由 $\alpha$ 和 $\epsilon$ 决定）传播到最终的物理场解中。这一分析为评估和控制基于学习的求解器的精度提供了坚实的理论基础。