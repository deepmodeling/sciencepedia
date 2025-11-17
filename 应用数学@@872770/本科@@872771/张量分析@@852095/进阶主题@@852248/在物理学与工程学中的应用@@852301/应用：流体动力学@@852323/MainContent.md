## 引言
流体无处不在，从我们呼吸的空气到星球内部的熔融金属，其运动复杂而迷人。要精确描述流体的平移、旋转、拉伸和剪切，需要一种超越简单标量和向量的数学语言。[张量分析](@entry_id:161423)正是为此而生的强大工具，它提供了一个统一的框架来捕捉流体行为的丰富细节。然而，对于初学者而言，张量的抽象性往往掩盖了其直观的物理意义和巨大的实用价值。本文旨在弥合这一差距，系统地揭示张量在[流体动力学](@entry_id:136788)中的核心作用。

在接下来的内容中，我们将分三步展开：首先，在“原理与机制”一章中，我们将深入探讨描述流体运动和内力的基本张量，如应变率张量和应力张量，并推导出[流体运动](@entry_id:182721)的控制方程。接着，在“应用与跨学科联系”一章中，我们将展示这些理论如何应用于解决从[生物力学](@entry_id:153973)到天体物理学的各种实际问题。最后，通过“动手实践”部分，您将有机会通过具体计算来巩固所学知识。让我们从构建描述[流体运动](@entry_id:182721)的数学基石开始。

## 原理与机制

在上一章对[流体动力学](@entry_id:136788)中的张量应用进行了初步介绍后，本章将深入探讨其核心原理与内在机制。我们将系统地构建描述[流体运动](@entry_id:182721)与受力的数学框架，从[运动学分解](@entry_id:751020)到动力学[本构关系](@entry_id:186508)，最终推导出流体运动的基本控制方程。本章旨在揭示张量如何以其强大的形式，将流体的物理行为精确地表达为严谨的数学语言。

### 流体运动的[运动学](@entry_id:173318)：[速度梯度张量](@entry_id:270928)

[流体动力学](@entry_id:136788)的核心任务是描述流体在空间和时间中的演化，其基础是**速度场** $\mathbf{v}(\mathbf{x}, t)$。然而，仅仅知道一个点上的速度是不够的。为了理解一个无限小的流体微团（fluid element）的局部行为——它如何平移、旋转、拉伸和剪切——我们必须考察速度在空间中的变化情况。这个变化由**[速度梯度张量](@entry_id:270928)** $L_{ij}$ 来完整描述，其定义为：

$L_{ij} = \frac{\partial v_i}{\partial x_j}$

其中，$v_i$ 是速度向量的第 $i$ 个分量，$x_j$ 是位置坐标的第 $j$ 个分量。这个[二阶张量](@entry_id:199780)包含了流体微团附近所有运动学信息的宝库。为了揭示其物理意义，我们可以将其分解为一个对称部分和一个反对称部分。

$L_{ij} = \frac{1}{2} (L_{ij} + L_{ji}) + \frac{1}{2} (L_{ij} - L_{ji})$

这个简单的代数分解具有深刻的物理意义。对称部分描述了流体微团的变形（deformation），而反对称部分则描述了它的刚性旋转（rigid rotation）。

### 变形与旋转：[应变率张量](@entry_id:266108)与[涡量张量](@entry_id:189621)

#### 应变率张量

速度梯度[张量的对称部分](@entry_id:182434)被称为**应变率张量**（rate-of-strain tensor），通常记为 $E_{ij}$ 或 $D_{ij}$：

$E_{ij} = \frac{1}{2} \left( \frac{\partial v_i}{\partial x_j} + \frac{\partial v_j}{\partial x_i} \right)$

[应变率张量](@entry_id:266108)的对角分量（如 $E_{11}, E_{22}, E_{33}$）代表了流体微团沿着坐标轴方向的线性拉伸或压缩速率。例如，$E_{11} = \frac{\partial v_1}{\partial x_1}$ 描述了微团在 $x_1$ 方向上的伸长率。其迹（trace）$E_{kk} = \frac{\partial v_k}{\partial x_k} = \nabla \cdot \mathbf{v}$ 代表了微团体积的膨胀率。对于[不可压缩流体](@entry_id:181066)，我们有 $\nabla \cdot \mathbf{v} = 0$，这意味着应变率张量的迹为零。

应变率张量的非对角分量（如 $E_{12}$）则代表了流体微团的[剪切变形](@entry_id:170920)速率，即初始互相垂直的两个线元之间夹角的变化率。我们可以通过一个具体的例子来理解这一点 [@problem_id:1490123]。考虑一个[二维流](@entry_id:266853)场 $\mathbf{v} = (\alpha y^2, 0)$，在 $t=0$ 时刻，位于点 $(x_0, y_0)$ 的两个初始分别沿 $x$ 轴和 $y$ 轴的无限小材料[线元](@entry_id:196833)，它们之间的夹角最初为 $\frac{\pi}{2}$。该夹角随时间的变化率可以被证明为 $-2E_{xy}$。对于这个流场，[应变率张量](@entry_id:266108)的 $E_{xy}$ 分量为：

$E_{xy} = \frac{1}{2} \left( \frac{\partial v_x}{\partial y} + \frac{\partial v_y}{\partial x} \right) = \frac{1}{2} (2\alpha y + 0) = \alpha y$

在点 $(x_0, y_0)$ 处，夹角的变化率为 $-2E_{xy}|_{(x_0, y_0)} = -2\alpha y_0$。这清晰地表明，应变率张量的非对角分量直接量化了流体的角变形速率。

一个至关重要的特性是，[应变率张量](@entry_id:266108)是**伽利略不变的**（Galilean invariant）[@problem_id:1490157]。这意味着，如果我们从一个以恒定速度 $\mathbf{U}$ 运动的[参考系](@entry_id:169232)中观察流体，其变形物理学保持不变。在移动[参考系](@entry_id:169232)中，新的[速度场](@entry_id:271461)为 $\mathbf{v}' = \mathbf{v} - \mathbf{U}$。由于 $\mathbf{U}$ 是一个常向量，其空间导数为零，因此新的[应变率张量](@entry_id:266108) $E'_{ij}$ 与原始张量 $E_{ij}$ 完全相同：

$E'_{ij} = \frac{1}{2} \left( \frac{\partial v'_i}{\partial x_j} + \frac{\partial v'_j}{\partial x_i} \right) = \frac{1}{2} \left( \frac{\partial (v_i - U_i)}{\partial x_j} + \frac{\partial (v_j - U_j)}{\partial x_i} \right) = \frac{1}{2} \left( \frac{\partial v_i}{\partial x_j} + \frac{\partial v_j}{\partial x_i} \right) = E_{ij}$

这证实了应变率张量描述的是流体固有的、不依赖于观察者匀速运动的变形行为。

#### [涡量张量](@entry_id:189621)

速度梯度[张量的反对称部分](@entry_id:193562)被称为**[涡量张量](@entry_id:189621)**（vorticity tensor）或[自旋张量](@entry_id:187346)（spin tensor），记为 $\Omega_{ij}$：

$\Omega_{ij} = \frac{1}{2} \left( \frac{\partial v_i}{\partial x_j} - \frac{\partial v_j}{\partial x_i} \right)$

这个张量描述了流体微团的**局部刚性旋转速率**。例如，在一个简单的剪切流 $\mathbf{v} = (k x_2, 0, 0)$ 中 [@problem_id:1490139]，[速度梯度张量](@entry_id:270928)为：

$\mathbf{L} = \begin{pmatrix} 0  k  0 \\ 0  0  0 \\ 0  0  0 \end{pmatrix}$

其[应变率张量](@entry_id:266108)和[涡量张量](@entry_id:189621)分别为：

$\boldsymbol{E} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T) = \begin{pmatrix} 0  k/2  0 \\ k/2  0  0 \\ 0  0  0 \end{pmatrix}$
$\boldsymbol{\Omega} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T) = \begin{pmatrix} 0  k/2  0 \\ -k/2  0  0 \\ 0  0  0 \end{pmatrix}$

这表明，一个简单的[剪切流](@entry_id:266817)可以被看作是纯剪切变形（由 $\boldsymbol{E}$ 描述）和刚性旋转（由 $\boldsymbol{\Omega}$ 描述）的叠加。

[涡量张量](@entry_id:189621)与一个更为人熟知的矢量——**[涡量矢量](@entry_id:187667)** $\boldsymbol{\omega}$ 密切相关，[涡量矢量](@entry_id:187667)定义为[速度场的旋度](@entry_id:183606) $\boldsymbol{\omega} = \nabla \times \mathbf{v}$。它们之间的关系可以通过[列维-奇维塔符号](@entry_id:193594) $\epsilon_{ijk}$ 表示：

$\Omega_{ij} = -\frac{1}{2} \epsilon_{ijk} \omega_k$  或  $\omega_i = -\epsilon_{ijk} \Omega_{jk}$

这说明[涡量张量](@entry_id:189621)和[涡量矢量](@entry_id:187667)包含了相同的旋转信息。考虑一个以恒定角[速度矢量](@entry_id:269648) $\boldsymbol{\omega}$ 进行[刚体转动](@entry_id:191086)的流体 [@problem_id:1490168]，其[速度场](@entry_id:271461)为 $v_i = \epsilon_{ijk} \omega_j x_k$。我们可以计算其[涡量张量](@entry_id:189621)：

$\frac{\partial v_i}{\partial x_j} = \epsilon_{imn} \omega_m \frac{\partial x_n}{\partial x_j} = \epsilon_{imn} \omega_m \delta_{nj} = \epsilon_{imj} \omega_m$

代入[涡量张量](@entry_id:189621)的定义：

$\Omega_{ij} = \frac{1}{2} (\epsilon_{imj}\omega_m - \epsilon_{jmi}\omega_m) = \frac{1}{2} (\epsilon_{imj}\omega_m + \epsilon_{imj}\omega_m) = \epsilon_{imj}\omega_m$

利用[列维-奇维塔符号](@entry_id:193594)的性质 $\epsilon_{imj} = -\epsilon_{ijm}$，并重命名[哑指标](@entry_id:188070) $m \to k$，我们得到 $\Omega_{ij} = -\epsilon_{ijk} \omega_k$。这直接证实了[涡量张量](@entry_id:189621)与角[速度矢量](@entry_id:269648)之间的关系。一个有趣的结果是，对于[刚体转动](@entry_id:191086)，$\nabla \times \mathbf{v} = 2\boldsymbol{\omega}$。由于流体微团的局部旋转角速度被定义为[涡量矢量](@entry_id:187667)（即速度旋度）的一半，这意味着在这种情况下，流体微团的旋转角速度恰好等于宏观角速度矢量 $\boldsymbol{\omega}$。

### 流体中的力：柯西应力张量

描述完[运动学](@entry_id:173318)，我们转向动力学，即研究引起运动的力。在连续介质中，力分为两类：作用于整个体积的**[体力](@entry_id:174230)**（body forces），如重力；以及作用于微团表面的**面力**（surface forces），如压力和[摩擦力](@entry_id:171772)。

**柯西[应力张量](@entry_id:148973)** $\sigma_{ij}$ 是描述面力的核心工具。它的物理意义是：在一个流体微团内部，通过某一点并带有[单位法向量](@entry_id:178851) $\mathbf{n}$ 的假想面，该表面单位面积上所受的力（称为**牵[引力](@entry_id:175476)矢量** $\mathbf{T}$）由下式给出：

$T_j = \sigma_{ij} n_i$  (注意索引顺序，一些文献使用 $T_i = \sigma_{ji} n_j$)

$\sigma_{ij}$ 的分量代表了在 $i$ 方向的法平面上作用的力的第 $j$ 个分量。因此，对角分量 $\sigma_{11}, \sigma_{22}, \sigma_{33}$ 是**[正应力](@entry_id:260622)**（normal stresses），而非对角分量 $\sigma_{12}, \sigma_{21}$ 等是**剪应力**（shear stresses）。

#### 应力[张量的对称性](@entry_id:202126)

一个基本原理是，在没有体力矩或内部耦合应力的情况下，柯西应力张量必须是**对称的**，即 $\sigma_{ij} = \sigma_{ji}$。这个结论源于[角动量守恒](@entry_id:156798)。我们可以通过一个思想实验来证明这一点 [@problem_id:1490180]。

考虑一个边长为 $\epsilon$ 的无限小立方体流体微团。假设应力张量不是对称的，例如 $\sigma_{xy} = A$ 而 $\sigma_{yx} = B$，且 $A \neq B$。作用在 $x=+\epsilon/2$ 面上的力为 $A \epsilon^2 \mathbf{\hat{j}}$，其[力臂](@entry_id:162693)为 $(\epsilon/2)\mathbf{\hat{i}}$，产生的 $z$ 方向力矩为 $(A\epsilon^3/2)\mathbf{\hat{k}}$。类似的，作用在 $y=+\epsilon/2$ 面上的力为 $B \epsilon^2 \mathbf{\hat{i}}$，其[力臂](@entry_id:162693)为 $(\epsilon/2)\mathbf{\hat{j}}$，产生的 $z$ 方向力矩为 $(-B\epsilon^3/2)\mathbf{\hat{k}}$。考虑所有六个面，作用在微团上的总 $z$ 方向力矩 $\tau_z$ 为 $(A-B)\epsilon^3$。

根据转动定律 $\tau_z = I_z \alpha_z$，其中 $I_z$ 是绕 $z$ 轴的转动惯量，$\alpha_z$ 是角加速度。立方体的质量 $m = \rho \epsilon^3$，转动惯量 $I_z \propto m \epsilon^2 \propto \rho \epsilon^5$。因此，[角加速度](@entry_id:177192)为：

$\alpha_z = \frac{\tau_z}{I_z} = \frac{(A-B)\epsilon^3}{\text{const} \cdot \rho \epsilon^5} = \frac{6(A-B)}{\rho \epsilon^2}$

当微团体积趋于零（$\epsilon \to 0$）时，如果 $A \neq B$，角加速度 $\alpha_z$ 将趋于无穷大。这在物理上是不可能的。因此，为了保证有限的[角加速度](@entry_id:177192)，必须有 $A=B$，即 $\sigma_{xy} = \sigma_{yx}$。此论证可以推广到所有分量，从而证明 $\sigma_{ij} = \sigma_{ji}$。

### 连接应力与应变：[本构方程](@entry_id:138559)

我们已经分别定义了描述变形的[应变率张量](@entry_id:266108) $E_{ij}$ 和描述[内力](@entry_id:167605)的[应力张量](@entry_id:148973) $\sigma_{ij}$。**[本构方程](@entry_id:138559)**（constitutive equation）的作用就是建立它们之间的关系，它反映了特定材料的物理属性。

#### [理想流体](@entry_id:161909)

最简单的流体模型是**理想流体**（ideal fluid），即无粘性（inviscid）流体。无粘性意味着流体不能承受剪应力，因此[应力张量](@entry_id:148973)的所有非对角分量都为零。此外，对于静止的理想流体，作用在任何表面上的力都必定垂直于该表面且大小与方向无关（各向同性）。这个力就是我们所熟知的**[静水压力](@entry_id:275365)** $p$。根据[连续介质力学](@entry_id:155125)的惯例，压应力为负。因此，静止理想流体的[应力张量](@entry_id:148973)为 [@problem_id:1490177]：

$\sigma_{ij} = -p \delta_{ij}$

其中 $\delta_{ij}$ 是克罗内克符号。这个张量是一个对角矩阵，所有对角元素均为 $-p$。

$\boldsymbol{\sigma} = \begin{pmatrix} -p  0  0 \\ 0  -p  0 \\ 0  0  -p \end{pmatrix}$

#### [牛顿流体](@entry_id:263796)

对于真实流体，运动会产生由粘性引起的[摩擦力](@entry_id:171772)，即剪应力。对于**牛顿流体**（Newtonian fluid），我们假设 viscous stress（[粘性应力](@entry_id:261328)张量 $\tau_{ij}$）与[应变率张量](@entry_id:266108) $E_{ij}$ 之间存在线性关系。总[应力张量](@entry_id:148973)是静水压力和[粘性应力](@entry_id:261328)的和：$\sigma_{ij} = -p\delta_{ij} + \tau_{ij}$。

对于一个各向同性的牛顿流体，最一般的[线性关系](@entry_id:267880)为：
$\tau_{ij} = \lambda (E_{kk}) \delta_{ij} + 2\mu E_{ij}$
其中 $\mu$ 是[动力粘度](@entry_id:268228)（dynamic viscosity），$\lambda$ 是[第二粘度](@entry_id:189253)系数。

对于**不可压缩牛顿流体**，情况得到简化 [@problem_id:1490122]。不可压缩性意味着流体密度不变，其[运动学](@entry_id:173318)约束为 $\nabla \cdot \mathbf{v} = 0$。我们已经知道 $E_{kk} = \nabla \cdot \mathbf{v}$，因此对于[不可压缩流体](@entry_id:181066)，$E_{kk}=0$。这使得包含 $\lambda$ 的项消失，[粘性应力](@entry_id:261328)张量简化为：

$\tau_{ij} = 2\mu E_{ij}$

因此，不可压缩牛顿流体的完整[本构方程](@entry_id:138559)为：

$\sigma_{ij} = -p \delta_{ij} + 2\mu E_{ij} = -p \delta_{ij} + \mu \left( \frac{\partial v_i}{\partial x_j} + \frac{\partial v_j}{\partial x_i} \right)$

这个方程是[流体动力学](@entry_id:136788)中最重要的关系式之一，它将流体内部的应力状态与[速度场](@entry_id:271461)的梯度直接联系起来。

### 基本运动定律

有了运动学描述、动力学工具和本构关系，我们现在可以构建流体运动的完整控制方程。这些方程本质上是在连续介质框架下对基本物理[守恒定律](@entry_id:269268)的数学表述。

#### [质量守恒](@entry_id:204015)：连续性方程

[质量守恒定律](@entry_id:147377)指出，在一个没有源或汇的系统中，质量不能被创造或毁灭。对于一个流体系统，这意味着控制体内质量的变化率必须等于通过其表面的净质量通量。其微分形式，即**连续性方程**，为 [@problem_id:1490125]：

$\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0$

使用张量指标表示法，散度 $\nabla \cdot \mathbf{A}$ 写作 $\frac{\partial A_i}{\partial x_i}$。因此，[连续性方程](@entry_id:195013)的[指标形式](@entry_id:183467)为：

$\frac{\partial \rho}{\partial t} + \frac{\partial (\rho v_i)}{\partial x_i} = 0$

这里，重复的索引 $i$ 暗示了对所有三个空间方向求和。

#### 动量守恒：[柯西动量方程](@entry_id:187010)

[动量守恒](@entry_id:149964)定律是牛顿第二定律在连续介质中的体现：一个流体微团的质量乘以其加速度等于作用于其上的合力。

首先，我们需要正确定义流体微团的加速度。流体微团既随时间变化，又在空间中移动。因此，其速度变化包含两部分：当地速度场随时间的变化（当地加速度），以及微团移动到速度不同新位置引起的变化（[对流加速度](@entry_id:263153)）。总加速度由**[物质导数](@entry_id:172646)**（material derivative）$\frac{D}{Dt}$ 给出：

$\frac{D\mathbf{v}}{Dt} = \frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla)\mathbf{v}$

使用指标符号，第 $i$ 个分量的加速度为 [@problem_id:1490160]：

$\frac{D v_i}{D t} = \frac{\partial v_i}{\partial t} + v_j \frac{\partial v_i}{\partial x_j}$

作用在质量为 $\rho dV$ 的微团上的合力是面力（应力[张量的散度](@entry_id:191736)）和体力之和。因此，**[柯西动量方程](@entry_id:187010)**的[指标形式](@entry_id:183467)为：

$\rho \frac{D v_i}{D t} = \frac{\partial \sigma_{ji}}{\partial x_j} + \rho f_i$

其中 $\rho f_i$ 是单位体积的[体力](@entry_id:174230)。注意应力张量散度中索引的顺序 $\frac{\partial \sigma_{ji}}{\partial x_j}$（由于 $\sigma$ 的对称性，也可写为 $\frac{\partial \sigma_{ij}}{\partial x_j}$）。

在许多情况下，比如重力，[体力](@entry_id:174230) $f_i$ 是保守的，可以写成一个势 $\Phi$ 的梯度，$f_i = -\frac{\partial \Phi}{\partial x_i}$。对于密度恒定的流体，我们可以将体力项吸收到应力项中 [@problem_id:1490167]。定义一个修正压力 $p^* = p + \rho\Phi$ 或者一个修正应力张量 $\tilde{\sigma}_{ji} = \sigma_{ji} - \rho\Phi\delta_{ji}$。这样，[动量方程](@entry_id:197225)可以写成更简洁的形式：

$\rho \frac{D v_i}{D t} = \frac{\partial \tilde{\sigma}_{ji}}{\partial x_j}$

将不可压缩[牛顿流体](@entry_id:263796)的[本构方程](@entry_id:138559) $\sigma_{ij} = -p \delta_{ij} + 2\mu E_{ij}$ 代入[柯西动量方程](@entry_id:187010)，经过整理便得到[流体动力学](@entry_id:136788)中最著名的方程之一——**[纳维-斯托克斯方程](@entry_id:142275)**（[Navier-Stokes](@entry_id:276387) equations）。这一过程完美地展示了[张量分析](@entry_id:161423)如何将关于运动、力和材料属性的独立概念统一到一个单一的、强大的预测性框架中。