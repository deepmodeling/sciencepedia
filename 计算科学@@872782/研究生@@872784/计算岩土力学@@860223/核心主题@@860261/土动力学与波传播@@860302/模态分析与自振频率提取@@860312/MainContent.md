## 引言
[模态分析](@entry_id:163921)与自振频率提取是理解和预测岩土结构（如大坝、地基、隧道）在地震、风或交通等动力荷载下行为的基石。在计算岩土力学领域，这些概念为我们提供了一个强大的框架，用以剖析复杂的动力响应。然而，岩土系统的复杂性——包括材料的非均质性、土-结构相互作用、孔隙流体的存在以及无限域的效应——给动力分析带来了独特的挑战，使得直接求解[时域响应](@entry_id:271891)变得异常困难和昂贵。

本文旨在系统地解决这一知识鸿沟，为读者提供一套从基础理论到高级应用的完整指南。通过本文的学习，您将能够掌握如何将复杂的连续介质问题转化为可解的离散特征值问题，并理解各种建模选择对分析结果的深远影响。

文章将分为三个核心章节展开。在**“原理与机制”**中，我们将从[弹性动力学](@entry_id:175818)的基本方程出发，推导[广义特征值问题](@entry_id:151614)，并深入探讨[有限元法](@entry_id:749389)中的关键构件，如[质量矩阵](@entry_id:177093)、[阻尼模型](@entry_id:748160)和高效数值求解器。接着，在**“应用与交叉学科联系”**中，我们将展示[模态分析](@entry_id:163921)如何在土-结构相互作用、孔隙介质力学和实验系统识别等实际工程场景中发挥作用，揭示其跨学科的强大生命力。最后，通过**“动手实践”**环节，您将有机会通过具体的编程练习，将理论知识转化为解决实际问题的能力。

## 原理与机制

本章旨在深入探讨计算岩土力学中[模态分析](@entry_id:163921)与自振频率提取的核心原理和基本机制。在“引言”章节的基础上，我们将从[弹性动力学](@entry_id:175818)的基本运动方程出发，系统地构建用于[模态分析](@entry_id:163921)的[广义特征值问题](@entry_id:151614)。随后，我们将阐述[有限元法](@entry_id:749389)如何将连续介质问题离散化为矩阵形式，并详细讨论质量矩阵和阻尼矩阵的不同构建方法及其对系统动力特性的影响。最后，我们将介绍针对岩土工程中常见的大规模复杂系统（如饱和[多孔介质](@entry_id:154591)和[半无限域](@entry_id:175316)）的先进分析技术与高效数值求解策略。

### [弹性动力学](@entry_id:175818)中的[广义特征值问题](@entry_id:151614)

在对岩土结构（如土-结构相互作用体系）进行线性、无[阻尼自由振动](@entry_id:166590)分析时，其动力学行为可通过有限元法[空间离散化](@entry_id:172158)，得到如下形式的[半离散运动方程](@entry_id:754679)：

$$
M \ddot{u}(t) + K u(t) = 0
$$

其中，$u(t) \in \mathbb{R}^n$ 是系统的全局节点位移向量，$M \in \mathbb{R}^{n \times n}$ 和 $K \in \mathbb{R}^{n \times n}$ 分别是系统的全局质量矩阵和[刚度矩阵](@entry_id:178659)。这两个矩阵均为[实对称矩阵](@entry_id:192806)，$M$ 通常是正定的，而 $K$ 在施加了足以消除刚体运动的边界条件后也是正定的。

为了求解该系统的自振频率和[振型](@entry_id:179030)，我们采用分离变量法，并假设系统进行简谐[振动](@entry_id:267781)。这意味着位移向量可以表示为空间分布（振型）与时间谐[波函数](@entry_id:147440)的乘积。采用复数形式的**[谐波](@entry_id:181533) ansatz**（ansatz 意为“设定”或“假设”），我们设：

$$
u(t) = \phi e^{i \omega t}
$$

其中，$\phi \in \mathbb{R}^n$ 是一个不随时间变化的向量，代表了[振动](@entry_id:267781)的空间形态，即**[振型](@entry_id:179030)**（mode shape）；$\omega$ 是[振动](@entry_id:267781)的**圆频率**（circular frequency）；$i$ 是虚数单位。对时间求导可得：

$$
\ddot{u}(t) = (i \omega)^2 \phi e^{i \omega t} = -\omega^2 \phi e^{i \omega t}
$$

将 $u(t)$ 和 $\ddot{u}(t)$ 的表达式代入运动方程，得到：

$$
M(-\omega^2 \phi e^{i \omega t}) + K(\phi e^{i \omega t}) = 0
$$

由于[谐波](@entry_id:181533)因子 $e^{i \omega t}$ 在任何时刻均不为零，我们可以将其从方程中约去，得到：

$$
-\omega^2 M \phi + K \phi = 0
$$

整理后，我们便得到了一个**[广义特征值问题](@entry_id:151614)**（Generalized Eigenvalue Problem, GEP）：

$$
K \phi = \omega^2 M \phi
$$

为方便求解，我们通常定义[特征值](@entry_id:154894) $\lambda = \omega^2$。于是，问题就变成了标准形式的 GEP：

$$
K \phi = \lambda M \phi
$$

该方程对于任意位移都成立的解是 $\phi = 0$，即静止状态，这被称为**[平凡解](@entry_id:155162)**。为了得到描述系统[振动](@entry_id:267781)的非[平凡解](@entry_id:155162)（$\phi \neq 0$），矩阵 $(K - \lambda M)$ 必须是奇异的。这一条件等价于其[行列式](@entry_id:142978)为零，即所谓的**[特征方程](@entry_id:265849)**：

$$
\det(K - \lambda M) = 0
$$

该方程的解是一系列[特征值](@entry_id:154894) $\lambda_1, \lambda_2, \dots, \lambda_n$，它们对应着系统自振频率的平方。对于每个[特征值](@entry_id:154894) $\lambda_i$，都存在一个或多个对应的[特征向量](@entry_id:151813) $\phi_i$，即系统的第 $i$ 阶**[振型](@entry_id:179030)**或**模态**。系统的第 $i$ 阶**自振圆频率**则为 $\omega_i = \sqrt{\lambda_i}$。由于 $K$ 和 $M$ 的性质，所有[特征值](@entry_id:154894) $\lambda_i$ 均为实数且非负，因此自振频率 $\omega_i$ 也是实数 [@problem_id:3543943]。

#### 模态的正交性

由于质量矩阵 $M$ 和刚度矩阵 $K$ 均为[实对称矩阵](@entry_id:192806)，系统的模态（[特征向量](@entry_id:151813)）具有重要的**正交性**。对于两个与不同[特征值](@entry_id:154894) $\lambda_i \neq \lambda_j$ 相关联的模态 $\phi_i$ 和 $\phi_j$，它们不仅是几何上的正交，更是在由 $M$ 和 $K$ 定义的[内积](@entry_id:158127)意义下正交。

考虑两个不同的特征对 $(\lambda_i, \phi_i)$ 和 $(\lambda_j, \phi_j)$：
1. $K \phi_i = \lambda_i M \phi_i$
2. $K \phi_j = \lambda_j M \phi_j$

用 $\phi_j^T$ 左乘方程 (1)，得到 $\phi_j^T K \phi_i = \lambda_i \phi_j^T M \phi_i$。
将方程 (2) 转置，并利用 $K$ 和 $M$ 的对称性 ($K^T = K, M^T = M$)，得到 $\phi_j^T K = \lambda_j \phi_j^T M$。再用 $\phi_i$ 右乘该式，得到 $\phi_j^T K \phi_i = \lambda_j \phi_j^T M \phi_i$。
比较两个关于 $\phi_j^T K \phi_i$ 的表达式，我们有 $(\lambda_i - \lambda_j) \phi_j^T M \phi_i = 0$。因为 $\lambda_i \neq \lambda_j$，所以必然有：

$$
\phi_j^T M \phi_i = 0 \quad (\text{for } i \neq j)
$$

这表明，不同模态之间关于质量矩阵是正交的，称为 **[M-正交性](@entry_id:178008)**。利用这个性质，我们可以进一步推导出**K-正交性**：

$$
\phi_j^T K \phi_i = \phi_j^T (\lambda_i M \phi_i) = \lambda_i (\phi_j^T M \phi_i) = 0 \quad (\text{for } i \neq j)
$$

这两个正交性是[模态分析](@entry_id:163921)的基石，它使得复杂的耦合系统运动可以分解为一系列独立的单自由度[振子](@entry_id:271549)运动的叠加，极大地简化了动力响应分析 [@problem_id:3543943]。

#### [刚体模态](@entry_id:754366)

在某些情况下，例如对一个未施加足够约束的结构（如无基岩约束的自由地基）进行建模时，刚度矩阵 $K$ 可能是奇异的。这意味着存在一个非零的位移向量 $\phi_{rbm}$（刚体位移模式），使得 $K \phi_{rbm} = 0$。这种位移不会在系统内部产生任何[应变能](@entry_id:162699)。将此代入[特征值问题](@entry_id:142153) $K \phi_{rbm} = \lambda M \phi_{rbm}$，我们得到 $0 = \lambda M \phi_{rbm}$。由于 $M$ 是正定的且 $\phi_{rbm}$ 非零，这要求 $\lambda = 0$。对应的频率 $\omega = \sqrt{\lambda} = 0$。这些**[零频模](@entry_id:166697)态**即为**[刚体模态](@entry_id:754366)**，代表系统作为一个整体在空间中的平动或转动，而没有内部变形 [@problem_id:3543943]。

### 从连续介质到离散系统：有限元公式

上一节中出现的质量矩阵 $M$ 和[刚度矩阵](@entry_id:178659) $K$ 并非凭空而来，它们是基于连续介质力学原理并通过有限元法（FEM）推导出的离散化产物。这个过程始于固体力学的基本控制方程——[线性动量守恒](@entry_id:165717)（牛顿第二定律）：

$$
\nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b} = \rho \ddot{\boldsymbol{u}}
$$

其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\rho$ 是密度，$\boldsymbol{b}$ 是单位质量[体力](@entry_id:174230)，$\boldsymbol{u}$ 是位移场。

为了导出有限元方程，我们应用**虚功原理**，将上述[偏微分方程](@entry_id:141332)转化为等价的积分形式（[弱形式](@entry_id:142897)）。通过乘以一个任意的[虚位移](@entry_id:168781)（或称[检验函数](@entry_id:166589)）$\delta \boldsymbol{u}$ 并在单元域 $\Omega_e$ 上积分，经过分部积分（[格林公式](@entry_id:173118)）并引入本构关系（如[胡克定律](@entry_id:149682) $\boldsymbol{\sigma} = \mathbb{D} \boldsymbol{\varepsilon}$），我们可以得到适用于自由[振动分析](@entry_id:146266)（即忽略体力 $\boldsymbol{b}$ 和面力 $\boldsymbol{t}$）的弱形式：

$$
\int_{\Omega_e} \rho \delta \boldsymbol{u} \cdot \ddot{\boldsymbol{u}} \, dV + \int_{\Omega_e} \delta \boldsymbol{\varepsilon} : \boldsymbol{\sigma} \, dV = 0
$$

在有限元框架下，单元内的连续位移场 $\boldsymbol{u}(\boldsymbol{x}, t)$ 通过节点位移向量 $\boldsymbol{q}(t)$ 和形函数矩阵 $\boldsymbol{N}(\boldsymbol{x})$ 进行插值：$\boldsymbol{u}(\boldsymbol{x}, t) = \boldsymbol{N}(\boldsymbol{x}) \boldsymbol{q}(t)$。同样地，应变场 $\boldsymbol{\varepsilon}$ 与节点位移的关系通过[应变-位移矩阵](@entry_id:163451) $\boldsymbol{B}$ 给出：$\boldsymbol{\varepsilon} = \boldsymbol{B} \boldsymbol{q}$。

将这些[有限元近似](@entry_id:166278)代入[弱形式](@entry_id:142897)，并考虑到[虚位移](@entry_id:168781) $\delta\boldsymbol{q}$ 的任意性，我们最终得到单元级的[半离散运动方程](@entry_id:754679)：

$$
\boldsymbol{M}_e \ddot{\boldsymbol{q}} + \boldsymbol{K}_e \boldsymbol{q} = \boldsymbol{0}
$$

其中，单元**[一致质量矩阵](@entry_id:174630)**（consistent mass matrix）$\boldsymbol{M}_e$ 和**刚度矩阵** $\boldsymbol{K}_e$ 由以下积分定义：

$$
\boldsymbol{M}_e = \int_{\Omega_e} \rho \boldsymbol{N}^T \boldsymbol{N} \, dV \quad , \quad \boldsymbol{K}_e = \int_{\Omega_e} \boldsymbol{B}^T \mathbb{D} \boldsymbol{B} \, dV
$$

这些积分通常通过数值积分（如[高斯积分](@entry_id:187139)）在标准化的“母元”上进行计算。例如，通过对一个三维[六面体单元](@entry_id:174602)施加[运动学](@entry_id:173318)约束，可以将其简化为一个二维杆模型，并从中提取出轴向[振动](@entry_id:267781)的自振频率 [@problem_id:3543987]。这个过程清晰地展示了如何从最基本的三维连续介质力学出发，通过系统性的有限元推导，最终得到用于[模态分析](@entry_id:163921)的离散矩阵。

### 质量矩阵：一致式与集中式

在动力分析中，质量矩阵的构造方式对计算结果，尤其是高阶频率，有显著影响。除了前述通过形函数积分得到的[一致质量矩阵](@entry_id:174630)，还存在一种更简化的形式——**[集中质量矩阵](@entry_id:173011)**（lumped mass matrix）。

**[一致质量矩阵](@entry_id:174630)** $\boldsymbol{M}_e^{\text{cons}}$ 是一个全矩阵（非对角），它反映了单元内[质量分布](@entry_id:158451)的连续性以及各节点位移之间的惯性耦合。例如，对于一个面积为 $A$ 的线性常应变三角形（CST）单元，其[一致质量矩阵](@entry_id:174630)为：

$$
\boldsymbol{M}_e^{\text{CST, cons}} = \frac{\rho A}{12} \begin{pmatrix} 2  1  1 \\ 1  2  1 \\ 1  1  2 \end{pmatrix}
$$

而对于一个尺寸为 $B \times H$ 的矩形双线性四节点（Q4）单元，其[一致质量矩阵](@entry_id:174630)为：

$$
\boldsymbol{M}_e^{\text{Q4, cons}} = \frac{\rho B H}{36} \begin{pmatrix} 4  2  1  2 \\ 2  4  2  1 \\ 1  2  4  2 \\ 2  1  2  4 \end{pmatrix}
$$

**[集中质量矩阵](@entry_id:173011)** $\boldsymbol{M}_e^{\text{lump}}$ 则是一个[对角矩阵](@entry_id:637782)，它将单元的总质量按某种规则分配到各个节点上，忽略了节点间的惯性耦合。最常用的方法是**行和集中法**（row-sum lumping），即将[一致质量矩阵](@entry_id:174630)每行的所有元素相加，然后将总和置于该行对应的对[角位置](@entry_id:174053)。对于上述[CST单元](@entry_id:748101)，每行的和为 $\frac{\rho A}{12}(2+1+1) = \frac{\rho A}{3}$，因此其[集中质量矩阵](@entry_id:173011)为：

$$
\boldsymbol{M}_e^{\text{CST, lump}} = \text{diag} \left\{ \frac{\rho A}{3}, \frac{\rho A}{3}, \frac{\rho A}{3} \right\}
$$

对于[Q4单元](@entry_id:176936)，每行的和为 $\frac{\rho B H}{36}(4+2+1+2) = \frac{\rho B H}{4}$，其[集中质量矩阵](@entry_id:173011)为：

$$
\boldsymbol{M}_e^{\text{Q4, lump}} = \text{diag} \left\{ \frac{\rho B H}{4}, \frac{\rho B H}{4}, \frac{\rho B H}{4}, \frac{\rho B H}{4} \right\}
$$

使用[集中质量矩阵](@entry_id:173011)的主要优点是计算效率高，因为[对角质量矩阵](@entry_id:173002)的求逆操作非常简单。然而，这种简化也付出了代价。一般而言，对于低阶单元，使用[集中质量矩阵](@entry_id:173011)会使系统模型变得“更柔”，从而**低估**自振频率。例如，对于一个用单个[Q4单元](@entry_id:176936)模拟的悬臂土柱，使用[一致质量矩阵](@entry_id:174630)得到的无量纲基频为 $\omega H \sqrt{\rho/G} = \sqrt{3}$，而使用[集中质量矩阵](@entry_id:173011)得到的结果为 $\sqrt{2}$，后者明显更低 [@problem_id:3544000]。这种差异在高频模态中更为显著。因此，在需要精确预测系统动力响应时，通常推荐使用[一致质量矩阵](@entry_id:174630)。

### 阻尼的作用

真实的岩土系统总是存在能量耗散，即阻尼。在动力学模型中引入阻尼项 $C \dot{u}(t)$，运动方程变为：

$$
M \ddot{u}(t) + C \dot{u}(t) + K u(t) = 0
$$

阻尼的来源多种多样，包括材料的内在滞回效应、波在无限介质中的辐射等。

#### 比例阻尼（[瑞利阻尼](@entry_id:172362)）

在许多工程应用中，精确确定阻尼矩阵 $C$ 的物理形式非常困难。一种广泛采用的简化模型是**[瑞利阻尼](@entry_id:172362)**（Rayleigh damping），它假设阻尼矩阵是质量矩阵 $M$ 和刚度矩阵 $K$ 的[线性组合](@entry_id:154743)：

$$
C = \alpha M + \beta K
$$

其中 $\alpha$ 和 $\beta$ 是通过实验数据或经验确定的比例系数。[瑞利阻尼](@entry_id:172362)的主要优点在于，它保持了阻尼矩阵在模态坐标下的对角性。将位移分解到模态空间 $u(t) = \sum_i \phi_i q_i(t)$，并利用模态的正交性，原先耦合的[方程组](@entry_id:193238)可以[解耦](@entry_id:637294)为一系列独立的单自由度[阻尼振子](@entry_id:173004)方程：

$$
\ddot{q}_i(t) + (\alpha + \beta \omega_i^2) \dot{q}_i(t) + \omega_i^2 q_i(t) = 0
$$

将此方程与标准的二阶[振子](@entry_id:271549)方程 $\ddot{x}(t) + 2\zeta_i\omega_i \dot{x}(t) + \omega_i^2 x(t) = 0$ 对比，我们可以直接得到第 $i$ 阶模态的**阻尼比** $\zeta_i$ [@problem_id:3543981]：

$$
\zeta_i = \frac{\alpha}{2\omega_i} + \frac{\beta\omega_i}{2}
$$

这个著名的公式表明，质量相关阻尼项 ($\alpha M$) 对低频模态的贡献更大，而刚度相关阻尼项 ($\beta K$) 对高频模态的贡献更大。通过在两个目标频率上设定期望的阻尼比，可以求解出系数 $\alpha$ 和 $\beta$。

#### [辐射阻尼](@entry_id:270883)与[吸收边界](@entry_id:201489)

在模拟[地震工程](@entry_id:748777)等涉及[半无限域](@entry_id:175316)（如地基）的问题时，一个关键挑战是如何在有限的计算区域内处理从模型内部传播出去的波。如果边界被设置为固定或自由，波会被不切实际地反射回计算域，污染模拟结果。为了模拟能量向无限远处的辐射，需要设置**[吸收边界条件](@entry_id:164672)**（Absorbing Boundary Conditions, ABCs）。

一种经典的方法是 Lysmer-Kuhlemeyer 提出的**粘性边界**（viscous boundary）。其基本思想是，在边界上施加一个与质点运动速度成正比并反向的力，模拟远场介质对边界的动力作用。对于[正入射](@entry_id:260681)到边界的平面[P波](@entry_id:178440)（压缩波）和S波（剪切波），为实现完全吸收，所需的[法向应力](@entry_id:260622) $t_n$ 和切向应力 $t_s$ 应满足：

$$
t_n = -\rho c_p v_n \quad , \quad t_s = -\rho c_s v_s
$$

其中，$c_p$ 和 $c_s$ 分别是P波和S波的[波速](@entry_id:186208)，$v_n$ 和 $v_s$ 是边界质点的法向和切向速度。这个关系在形式上与[粘性阻尼](@entry_id:168972)器（dashpot）完全一致。因此，可以在有限元模型的截断边界上布置一系列法向和切向的阻尼器来近似[吸收边界](@entry_id:201489)。

引入这种物理阻尼后，系统的阻尼矩阵 $C$ 不再为零，动力系统变为[耗散系统](@entry_id:151564)。进行[模态分析](@entry_id:163921)时，特征值问题会变为**非自伴随**的，其解——[复特征值](@entry_id:156384)——将成共轭对出现：$\lambda_{\text{eig}, j} = -\xi_j \omega_j \pm i \omega_{d,j}$。其中，虚部 $\omega_{d,j}$ 是**阻尼自振频率**，而实部则代表了模态振幅的衰减速率。与刚性边界相比，[吸收边界](@entry_id:201489)是一种“柔性”约束，通常会降低系统的自振频率，并引入**[辐射阻尼](@entry_id:270883)**，使模态振幅随时间衰减 [@problem_id:3543997]。

### 岩土系统的专门主题

岩土材料的复杂性给[模态分析](@entry_id:163921)带来了特殊的挑战和考虑。

#### 多孔介质：排水与不排水[模态分析](@entry_id:163921)

饱水土体是典型的[多孔介质](@entry_id:154591)，其动力行为受固相骨架和孔隙流体相互作用的控制。Biot 理论是描述这种耦合行为的经典框架。在[有限元离散化](@entry_id:193156)后，完全耦合的 $u-p$ （固相骨架位移-[孔隙水压力](@entry_id:753587)）[动力学方程组](@entry_id:202106)可以写成如下形式：

$$
\begin{pmatrix} M  0 \\ 0  0 \end{pmatrix} \begin{pmatrix} \ddot{\boldsymbol{u}} \\ \ddot{\boldsymbol{p}} \end{pmatrix} + \begin{pmatrix} 0  0 \\ H^T  S \end{pmatrix} \begin{pmatrix} \dot{\boldsymbol{u}} \\ \dot{\boldsymbol{p}} \end{pmatrix} + \begin{pmatrix} K  -H \\ 0  C_p \end{pmatrix} \begin{pmatrix} \boldsymbol{u} \\ \boldsymbol{p} \end{pmatrix} = \boldsymbol{f}
$$

其中 $K$ 是骨架的排水[刚度矩阵](@entry_id:178659)，$H$ 是[耦合矩阵](@entry_id:191757)，$S$ 是储水矩阵，$C_p$ 是渗透矩阵。直接求解这个耦合系统的特征值问题非常复杂。在工程实践中，通常考虑两种极限情况：

1.  **不排水极限 (Undrained Limit)**：当[振动频率](@entry_id:199185)很高或土体[渗透性](@entry_id:154559)很低 ($\kappa \to 0$) 时，孔隙流体来不及流出，被“锁”在骨架孔隙中与固相一起运动。在这种情况下，孔压可以通过运动学位移来表达，从而消去压力自由度。最终得到的等效单场特征值问题为 $(K_u - \omega^2 M_u) \boldsymbol{U} = 0$。其**有效不排水刚度** $K_u = K + H S^{-1} H^T$ 大于排水刚度 $K$，因为受困流体的压力提供了额外的刚度。其**有效不排[水质](@entry_id:180499)量**则由混合物的总密度决定，即 $\rho_u = (1-\phi)\rho_s + \phi\rho_f$，其中 $\phi$ 是孔隙率，$\rho_s$ 和 $\rho_f$ 分别是固体颗粒和流体的密度 [@problem_id:3543961] [@problem_id:3543966]。

2.  **排水极限 (Drained Limit)**：当[振动频率](@entry_id:199185)很低或土体渗透性很高时，任何超[孔隙水压力](@entry_id:753587)都能瞬间消散，即 $\boldsymbol{p} \approx 0$。此时，系统退化为一个简单的单场问题 $(K_d - \omega^2 M_d) \boldsymbol{U} = 0$。其**有效排水刚度** $K_d$ 就是骨架的排水刚度 $K$。由于流体可以[自由流](@entry_id:159506)动，不一定与骨架同步运动，因此其**有效排水质量**通常只考虑固体骨架的质量，对应密度为 $\rho_d = (1-\phi)\rho_s$ [@problem_id:3543961]。

#### 模型降阶：盖扬凝聚

对于包含大量自由度的大型模型，直接求解[特征值问题](@entry_id:142153)可能成本过高。**盖扬凝聚**（Guyan condensation），或称静力凝聚，是一种常用的模型降阶技术。其基本思想是将系统的自由度划分为少数“主自由度”（master DOFs, $u_m$）和大量“从自由度”（slave DOFs, $u_s$）。通过假设从自由度上的[惯性力](@entry_id:169104)可以忽略不计，可以建立从自由度与主自由度之间的静力约束关系：

$$
u_s \approx -K_{ss}^{-1} K_{sm} u_m
$$

利用这个变换关系，可以将原始的大型质量和[刚度矩阵](@entry_id:178659)“凝聚”到仅包含主自由度的小型等效矩阵 $M_R$ 和 $K_R$：

$$
K_R = K_{mm} - K_{ms} K_{ss}^{-1} K_{sm}
$$
$$
M_R = M_{mm} - M_{ms}K_{ss}^{-1}K_{sm} - K_{sm}^T(K_{ss}^{-1})^T M_{sm} + K_{sm}^T(K_{ss}^{-1})^T M_{ss} K_{ss}^{-1}K_{sm}
$$

然后，在这个降阶后的系统上求解特征值问题 $(K_R - \omega^2 M_R) \phi_m = 0$。盖扬凝聚的本质是忽略了从自由度的惯性释放效应，这使得降阶后的系统比原始系统**人为地更硬**。因此，通过静力凝聚计算出的自振频率通常是真实频率的**上限**，即会高估系统的自振频率。这种方法的精度对于低阶模态较高，而对于[高阶模](@entry_id:750331)态则误差较大 [@problem_id:3543940]。

### [大规模系统](@entry_id:166848)的数值求解器

在现代计算岩土力学中，模型自由度数达到百万量级已是常态。对于这样的大规模稀疏[矩阵[特征值问](@entry_id:142446)题](@entry_id:142153)，选择合适的数值算法至关重要。

#### 寻找低频模态的挑战

大多[数基](@entry_id:634389)本的迭代[特征值](@entry_id:154894)求解算法，如幂法及其变种（[子空间迭代](@entry_id:168266)、Lanczos 算法），本质上是为寻找矩阵的**最大**（主导）[特征值](@entry_id:154894)而设计的。然而，在[结构动力学](@entry_id:172684)和[地震工程](@entry_id:748777)中，我们最关心的通常是系统的**最低**几个自振频率和[振型](@entry_id:179030)，因为它们往往主导着系统对动力荷载的响应。直接应用这些算法于 $K\phi = \lambda M\phi$ 会收敛到不想要的最高频率。

#### 移动-求逆策略

为了高效地求解最低频率，最强大的技术是**移动-求逆谱变换**（Shift-and-Invert Spectral Transformation）。其思想是通过一个简单的代数变换，将原始问题 $K\phi = \lambda M\phi$ 转化为一个新的[特征值问题](@entry_id:142153)，使得我们感兴趣的[特征值](@entry_id:154894)在新问题中成为主导[特征值](@entry_id:154894)。

我们选择一个**移动点** $\sigma$，该值接近我们想要寻找的[特征值](@entry_id:154894) $\lambda$（对于基频，通常取 $\sigma \approx 0$）。原始问题可以改写为：

$$
(K - \sigma M) \phi = (\lambda - \sigma) M \phi
$$

假设 $(K - \sigma M)$ 非奇异，两边同乘以其逆，并整理可得：

$$
(K - \sigma M)^{-1} M \phi = \frac{1}{\lambda - \sigma} \phi
$$

这是一个新的[标准特征值问题](@entry_id:755346) $A \phi = \mu \phi$，其中变换后的算子为 $A = (K - \sigma M)^{-1} M$，变换后的[特征值](@entry_id:154894)为 $\mu = \frac{1}{\lambda - \sigma}$。

这个变换的巧妙之处在于，原始问题中离移动点 $\sigma$ 最近的[特征值](@entry_id:154894) $\lambda_p$，经过变换后，其对应的[特征值](@entry_id:154894) $\mu_p$ 的[绝对值](@entry_id:147688) $|\mu_p| = 1/|\lambda_p - \sigma|$ 将会是最大的。因此，现在我们只需对变换后的算子 $A$ 使用 Lanczos 等迭代算法，就能快速收敛到其主导[特征值](@entry_id:154894) $\mu_p$，然后通过关系式 $\lambda_p = \sigma + 1/\mu_p$ 即可求得我们最初想要的 $\lambda_p$ [@problem_id:3543948]。

移动-求逆策略的收敛速度由变换后主导与次主导[特征值](@entry_id:154894)的模长之比决定。这个比值 $r(\sigma) = |\lambda_p - \sigma| / |\lambda_q - \sigma|$（其中 $\lambda_q$ 是第二靠近 $\sigma$ 的[特征值](@entry_id:154894)）通常远小于1，保证了算法的快速收敛，即使原始问题中的低频[特征值](@entry_id:154894)非常密集（聚集）[@problem_id:3543948]。

该方法的核心计算开销在于迭代过程中需要反复求解形如 $(K - \sigma M) y = z$ 的大型稀疏[线性方程组](@entry_id:148943)。对于现代高性能计算平台，有两种主流高效的解决方案：
1.  **稀疏直接法**：在迭代开始前，对矩阵 $(K - \sigma M)$ 进行一次性的、计算量巨大的 $LDL^T$ 分解。在后续的每次迭代中，[求解方程组](@entry_id:152624)就简化为非常快速的[回代](@entry_id:146909)过程。
2.  **迭代法**：在每次迭代中，使用预条件共轭梯度法（PCG）等迭代方法求解该[方程组](@entry_id:193238)。其效率高度依赖于一个高质量的预条件子。对于有限元问题，**[代数多重网格](@entry_id:140593)法（AMG）** 是一种近乎最优的[预条件子](@entry_id:753679)，具有极佳的[计算效率](@entry_id:270255)和并行扩展性 [@problem_id:3543957]。

综上所述，结合了移动-求逆谱变换和高效[线性求解器](@entry_id:751329)（如稀疏直接法或 AMG-PCG）的 [Krylov 子空间方法](@entry_id:144111)（如隐式重启动 Lanczos 法），是当前解决大规模岩土工程[模态分析](@entry_id:163921)问题的最先进和最可靠的技术。