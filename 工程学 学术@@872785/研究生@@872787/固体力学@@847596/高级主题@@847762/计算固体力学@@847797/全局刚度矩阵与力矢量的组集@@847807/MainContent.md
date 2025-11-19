## 引言
在[有限元分析](@entry_id:138109)中，从描述单个单元（element）的局部力学行为，到求解整个结构的宏观响应，其间的关键桥梁便是[全局刚度矩阵](@entry_id:138630)与[全局力向量](@entry_id:194422)的组装。这个过程是将离散化的物理原理转化为一个可计算的代数系统的核心，是所有有限元软件的基石。然而，许多初学者在理解了单元级方程后，常常对如何系统性地将成千上万个单元的贡献整合成一个统一的、巨大的[方程组](@entry_id:193238)感到困惑。本文旨在填补这一知识鸿沟，全面阐释组装过程的原理、实现与应用。

在接下来的内容中，我们将分三步深入探讨这一主题。“原理与机制”一章将从虚功原理出发，推导[单元刚度矩阵](@entry_id:139369)与力向量的由来，并详细介绍实现组装的“散开-相加”算法。“应用与跨学科联系”一章将展示该组装框架的强大灵活性，探讨其如何处理复杂材料、[非线性](@entry_id:637147)问题，并延伸至[生物力学](@entry_id:153973)等交叉领域。最后，在“动手实践”部分，您将通过具体的编程练习，亲手实现组装过程，将理论知识转化为实践能力。

## 原理与机制

在[有限元法](@entry_id:749389)应用于固体力学时，其核心任务是将连续体的控制方程转化为一个离散的[代数方程](@entry_id:272665)组。本章将深入探讨其核心构建模块的原理与机制：即如何从单个单元（element）的力学行为出发，系统地构建描述整个结构响应的**[全局刚度矩阵](@entry_id:138630) (global stiffness matrix)** 与**[全局力向量](@entry_id:194422) (global force vector)**。我们将从变分原理出发，推导单元级的方程，探讨如何处理复杂的几何与载荷，并最终阐明将这些局部贡献“组装”成一个可解的全局系统的系统化过程。

### 基于虚功原理的单元方程

有限元法的数学基础根植于[变分原理](@entry_id:198028)，其中**虚功原理 (principle of virtual work)** 提供了一个普适且强大的出发点。对于任意满足[位移边界条件](@entry_id:203261)的[虚位移](@entry_id:168781)场，一个处于平衡状态的弹性体，其[内力](@entry_id:167605)所做的[虚功](@entry_id:176403)（[内虚功](@entry_id:172278)）等于外力所做的[虚功](@entry_id:176403)（外[虚功](@entry_id:176403)）。这可以表示为总[势能](@entry_id:748988) $\Pi$ 的一阶变分为零，即 $\delta \Pi = 0$。总[势能](@entry_id:748988)由内应变能和外力势能组成，其[变分形式](@entry_id:166033)为：

$$
\delta \Pi = \int_{\Omega} \delta \boldsymbol{\varepsilon}^{T} \boldsymbol{\sigma} \,d\Omega - \int_{\Omega} \delta \mathbf{u}^{T} \mathbf{b} \,d\Omega - \int_{\Gamma_t} \delta \mathbf{u}^{T} \overline{\mathbf{t}} \, d\Gamma = 0
$$

其中，$\boldsymbol{\sigma}$ 是[应力张量](@entry_id:148973)，$\delta \boldsymbol{\varepsilon}$ 是虚应变张量，$\delta \mathbf{u}$ 是[虚位移](@entry_id:168781)向量，$\mathbf{b}$ 是单位体积的[体力](@entry_id:174230)，$\overline{\mathbf{t}}$ 是在力边界 $\Gamma_t$ 上施加的面力。

有限元法的核心思想在于将位移场 $\mathbf{u}$ 在每个单元 $\Omega_e$ 内通过节点位移 $\mathbf{d}_e$ 和**形函数 (shape functions)** $\mathbf{N}$ 进行插值：
$$
\mathbf{u}(\mathbf{x}) = \mathbf{N}(\mathbf{x}) \mathbf{d}_e
$$
同样，[虚位移](@entry_id:168781)场也表示为 $\delta \mathbf{u}(\mathbf{x}) = \mathbf{N}(\mathbf{x}) \delta \mathbf{d}_e$。

应变场是位移的导数。在小应变假设下，[应变-位移关系](@entry_id:173321)是线性的，可以写成：
$$
\boldsymbol{\varepsilon}(\mathbf{x}) = \mathbf{L} \mathbf{u}(\mathbf{x}) = (\mathbf{L}\mathbf{N}(\mathbf{x})) \mathbf{d}_e = \mathbf{B}(\mathbf{x}) \mathbf{d}_e
$$
这里，$\mathbf{L}$ 是应变-位移[微分算子](@entry_id:140145)，而 $\mathbf{B} = \mathbf{L}\mathbf{N}$ 被称为**[应变-位移矩阵](@entry_id:163451) (strain-displacement matrix)**。它将单元的节点位移直接关联到单元内部的应变场。相应地，虚应变为 $\delta \boldsymbol{\varepsilon}(\mathbf{x}) = \mathbf{B}(\mathbf{x}) \delta \mathbf{d}_e$。

在线弹性材料中，[应力与应变](@entry_id:137374)通过本构关系 $\boldsymbol{\sigma} = \mathbf{D} \boldsymbol{\varepsilon}$ 联系起来，其中 $\mathbf{D}$ 是**[弹性矩阵](@entry_id:189189) (elasticity matrix)** 或**[本构矩阵](@entry_id:164908) (constitutive matrix)**。

将这些离散化的场代入虚功原理的表达式中，并考虑其对单个单元的贡献，我们得到：
$$
\delta \mathbf{d}_e^T \left( \int_{\Omega_e} \mathbf{B}^T \mathbf{D} \mathbf{B} \,d\Omega \right) \mathbf{d}_e - \delta \mathbf{d}_e^T \int_{\Omega_e} \mathbf{N}^T \mathbf{b} \,d\Omega - \delta \mathbf{d}_e^T \int_{\Gamma_{t,e}} \mathbf{N}^T \overline{\mathbf{t}} \,d\Gamma = 0
$$
由于虚节点位移 $\delta \mathbf{d}_e$ 是任意的，括号内的表达式必须为零。这便导出了单元级的[平衡方程](@entry_id:172166)：
$$
\mathbf{k}_e \mathbf{d}_e = \mathbf{f}_e
$$
其中，**[单元刚度矩阵](@entry_id:139369) (element stiffness matrix)** $\mathbf{k}_e$ 和**单元力向量 (element force vector)** $\mathbf{f}_e$ 的定义为：
$$
\mathbf{k}_e = \int_{\Omega_e} \mathbf{B}^T \mathbf{D} \mathbf{B} \,d\Omega
$$
$$
\mathbf{f}_e = \mathbf{f}_{b,e} + \mathbf{f}_{t,e} = \int_{\Omega_e} \mathbf{N}^T \mathbf{b} \,d\Omega + \int_{\Gamma_{t,e}} \mathbf{N}^T \overline{\mathbf{t}} \,d\Gamma
$$
这个结果是至关重要的。它表明，无论问题的维度或几何形状如何，单元的刚度贡献本质上都是一个积分，其被积函数 $\mathbf{B}^T \mathbf{D} \mathbf{B}$ 融合了单元的几何信息（通过 $\mathbf{B}$）和材料属性（通过 $\mathbf{D}$）。单元力向量则将[分布](@entry_id:182848)式的[体力](@entry_id:174230) $\mathbf{b}$ 和面力 $\overline{\mathbf{t}}$ 转化为作用在节点上的等效集中力。[@problem_id:2615759]

### [单元刚度矩阵](@entry_id:139369)的计算

[单元刚度矩阵](@entry_id:139369)的计算是有限元分析的核心步骤。其具体形式取决于单元的类型、几何形状和材料属性。

#### [一维杆单元](@entry_id:171268)

最简单的例子是[一维杆单元](@entry_id:171268)。考虑一个长度为 $h$、[横截面](@entry_id:154995)积为 $A$、杨氏模量为 $E$ 的杆单元。其[位移场](@entry_id:141476) $u(x)$ 由两个节点的位移 $d_1, d_2$ 线性插值得到。形函数为 $N_1(x) = 1 - x/h$ 和 $N_2(x) = x/h$。对于一维问题，[轴向应变](@entry_id:160811)为 $\varepsilon = du/dx$。因此，[应变-位移矩阵](@entry_id:163451) $\mathbf{B}$ 为：
$$
\mathbf{B}(x) = \frac{d\mathbf{N}}{dx} = \begin{pmatrix} -\frac{1}{h} & \frac{1}{h} \end{pmatrix}
$$
注意到对于线性单元，$\mathbf{B}$ 矩阵是常数。一维线弹性材料的[本构矩阵](@entry_id:164908) $\mathbf{D}$ 就是杨氏模量 $E$。体积微元 $d\Omega = A\,dx$。代入刚度矩阵的积分公式：
$$
\mathbf{k}_e = \int_{0}^{h} \begin{pmatrix} -1/h \\ 1/h \end{pmatrix} E \begin{pmatrix} -1/h & 1/h \end{pmatrix} A \,dx = AE \int_{0}^{h} \frac{1}{h^2} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix} dx = \frac{AE}{h} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}
$$
这个结果与[材料力学](@entry_id:201885)中基于平衡推导出的结果完全一致，展示了[变分原理](@entry_id:198028)的普适性。[@problem_id:2615759]

#### 二维和三维的等参元

对于具有复杂形状的二维或三维问题，直接在物理[坐标系](@entry_id:156346)下进行积分可能非常困难。**等参元 (isoparametric element)** 概念提供了一个优雅的解决方案。其核心思想是，使用相同的形函数既插值单元的几何形状，又插值其内的[位移场](@entry_id:141476)。

几何形状通过其节点坐标 $\mathbf{x}_i$ 进行插值：
$$
\mathbf{x}(\boldsymbol{\xi}) = \sum_i N_i(\boldsymbol{\xi}) \mathbf{x}_i
$$
这里，$\boldsymbol{\xi}$ 是一个规则、简单的“父单元”或“母元”（例如，对于四边形是 $[-1, 1] \times [-1, 1]$ 的正方形）的[局部坐标](@entry_id:181200)。这个过程建立了一个从父单元到物理单元的映射。

[刚度矩阵](@entry_id:178659)积分需要计算 $\mathbf{B}$ 矩阵，而 $\mathbf{B}$ 矩阵包含对物理坐标 $(x,y)$ 的导数。通过[链式法则](@entry_id:190743)，这些导数可以与对[局部坐标](@entry_id:181200) $(\xi, \eta)$ 的导数联系起来：
$$
\begin{pmatrix} \frac{\partial}{\partial x} \\ \frac{\partial}{\partial y} \end{pmatrix} = \mathbf{J}^{-1} \begin{pmatrix} \frac{\partial}{\partial \xi} \\ \frac{\partial}{\partial \eta} \end{pmatrix}
$$
其中 $\mathbf{J}$ 是[坐标映射](@entry_id:747874)的**[雅可比矩阵](@entry_id:264467) (Jacobian matrix)**：
$$
\mathbf{J} = \begin{pmatrix} \frac{\partial x}{\partial \xi} & \frac{\partial y}{\partial \xi} \\ \frac{\partial x}{\partial \eta} & \frac{\partial y}{\partial \eta} \end{pmatrix}
$$
同时，积分的面积微元也发生变换：$d\Omega = t \,dA = t \det(\mathbf{J}) \,d\xi \,d\eta$（对于厚度为 $t$ 的平面问题）。因此，[单元刚度矩阵](@entry_id:139369)的积分被转换到父单元上进行：
$$
\mathbf{k}_e = \int_{-1}^{1} \int_{-1}^{1} \mathbf{B}(\xi, \eta)^T \mathbf{D} \mathbf{B}(\xi, \eta) \,t \det(\mathbf{J}(\xi, \eta)) \,d\xi \,d\eta
$$
这个表达式清晰地展示了刚度矩阵如何依赖于材料（通过 $\mathbf{D}$）和几何（通过 $\mathbf{B}$ 和 $\det(\mathbf{J})$）。例如，对于一个由节点 $(0,0), (a,0), (a,b), (0,b)$ 定义的矩形四[节点单元](@entry_id:752523)，其雅可比矩阵是一个常数矩阵 $\mathbf{J} = \begin{pmatrix} a/2 & 0 \\ 0 & b/2 \end{pmatrix}$，这大大简化了积分过程。然而，对于任意扭曲的四边形，$\mathbf{J}$ 将是 $(\xi, \eta)$ 的函数，积分通常需要通过[高斯求积](@entry_id:146011)等数值方法完成。[@problem_id:2615795]

### 等效节点力的计算

与刚度矩阵一样，将[分布](@entry_id:182848)式载荷转化为节点力的过程也遵循[虚功](@entry_id:176403)等效的原则，这被称为**协调节点力 (consistent nodal forces)**。

#### 体力

对于体力 $\mathbf{b}$，其等效节点力向量为：
$$
\mathbf{f}_{b,e} = \int_{\Omega_e} \mathbf{N}^T \mathbf{b} \,d\Omega
$$
考虑一个二维三节点线性[三角形单元](@entry_id:167871)，其面积为 $A_e$，厚度为 $t$，并承受一个恒定的[体力](@entry_id:174230) $\mathbf{b} = \begin{pmatrix} b_x & b_y \end{pmatrix}^T$。线性[三角形单元](@entry_id:167871)的形函数有一个重要特性：$\int_{A_e} N_i \,dA = A_e/3$。利用这个性质，我们可以推导出该单元的体力向量为：
$$
\mathbf{f}_{b,e} = \frac{A_e t}{3} \begin{pmatrix} b_x \\ b_y \\ b_x \\ b_y \\ b_x \\ b_y \end{pmatrix}
$$
这个结果直观地表明，对于线性[三角形单元](@entry_id:167871)和恒定[体力](@entry_id:174230)，总的[体力](@entry_id:174230) $(A_e t) \mathbf{b}$被平均分配到三个节点上。[@problem_id:2615782]

#### 面力

对于施加在单元边界 $\Gamma_e$ 上的面力 $\overline{\mathbf{t}}$，其等效节点力向量为：
$$
\mathbf{f}_{t,e} = \int_{\Gamma_e} \mathbf{N}^T \overline{\mathbf{t}} \,d\Gamma
$$
计算这个积分，尤其是对于弯曲边界和变化的载荷，同样可以借助[等参映射](@entry_id:173239)。例如，考虑施加在二次[四边形单元](@entry_id:176937)的弯曲边上的法向压力 $\bar{p}$ [@problem_id:2615744]。该边界由三个节点定义，其几何和位移可以用一维二次形函数 $L_i(\xi)$ 在父坐标 $\xi \in [-1, 1]$ 上进行参数化。

面力向量 $\overline{\mathbf{t}}$ 等于压力乘以向外的[单位法向量](@entry_id:178851) $\mathbf{n}$，即 $\overline{\mathbf{t}} = \bar{p}\mathbf{n}$。边界上的线微元 $d\Gamma$ 可以通过雅可比行列式（在此为切向量的模长）与父坐标微元 $d\xi$ 联系起来。一个更巧妙的方法是利用关系 $\mathbf{n} \,d\Gamma = \mathbf{R} \mathbf{t} \,d\xi$，其中 $\mathbf{t}$ 是切向量，$\mathbf{R}$ 是 $90^\circ$ [旋转矩阵](@entry_id:140302)。这避免了计算法向量的模长。最终，力向量的积分可以完全在父[坐标系](@entry_id:156346)下进行：
$$
\mathbf{f}_{t,e} = \int_{-1}^{1} \mathbf{N}_e^T(\xi) \bar{p}(\xi) (\mathbf{R} \mathbf{t}(\xi)) \,d\xi
$$
其中 $\mathbf{N}_e$ 是仅包含该边界上节点的形函数的矩阵。这个过程能够精确地将复杂的法向[压力分布](@entry_id:275409)转化为作用在边界节点上的等效力和力矩。

### 组装过程：从局部到全局

我们已经为每个单元建立了方程 $\mathbf{k}_e \mathbf{d}_e = \mathbf{f}_e$。下一步是将这些独立的单元[方程组](@entry_id:193238)装成一个描述整个系统行为的全局[方程组](@entry_id:193238) $\mathbf{K}\mathbf{U} = \mathbf{F}$。组装过程基于两个物理原则：**位移协调性**（共享节点的单元在该节点处具有相同的位移）和**力的平衡**（作用于一个节点上的所有内力和外力总和为零）。

#### 节点和自由度编号

在计算上，组装过程是一个系统化的[数据管理](@entry_id:635035)任务。首先，必须为模型中的所有节点和自由度（Degree of Freedom, DOF）建立一个唯一的**全局编号方案**。例如，在一个 $n_x \times n_y$ 的[结构化网格](@entry_id:170596)中，可以按行（或按列）为节点编号。如果每个节点有两个[平动自由度](@entry_id:140257) $(u, v)$，则全局自由度可以按节点顺序依次编号。例如，节点 $N$ 的 $u$ 和 $v$ 自由度可以编号为 $2N-1$ 和 $2N$。[@problem_id:2615739]

#### 连接性映射与“Scatter-Add”算法

组装的核心是**连接性映射 (connectivity map)**，通常表示为一个列表或数组 $L_e$。对于每个单元 $e$，$L_e$ 存储了其局部自由度（例如，按单元节点顺序[排列](@entry_id:136432)）对应的全局自由度编号。

在形式上，组装过程可以通过一个布尔“放置”矩阵 $A_e$ 来描述，该矩阵将全局位移向量 $\mathbf{U}$ 映射到单元位移向量 $\mathbf{d}_e = A_e \mathbf{U}$。基于能量相加的原则，可以证明[全局刚度矩阵](@entry_id:138630)和力向量是所有单元贡献的总和：
$$
\mathbf{K} = \sum_e A_e^T \mathbf{k}_e A_e \quad , \quad \mathbf{F} = \sum_e A_e^T \mathbf{f}_e
$$
这个 $A_e^T (\cdot) A_e$ 操作被称为**“散开”(scatter)** 操作，它将一个小的单元矩阵“散布”到一个与全局系统同样大小的矩阵的正确位置。

在计算实践中，我们并不显式地构造和乘以 $A_e$ 矩阵。取而代之的是一个更高效的**“散开-相加” (scatter-add)** 算法 [@problem_id:2615798]：
1.  初始化一个大小为 $N_{dof} \times N_{dof}$ 的全零[全局刚度矩阵](@entry_id:138630) $\mathbf{K}$ 和一个大小为 $N_{dof} \times 1$ 的[全局力向量](@entry_id:194422) $\mathbf{F}$。
2.  遍历所有单元 $e$：
    a. 计算[单元刚度矩阵](@entry_id:139369) $\mathbf{k}_e$ 和单元力向量 $\mathbf{f}_e$。
    b. 获取该单元的连接性列表 $L_e$。
    c. 遍历 $\mathbf{k}_e$ 的所有元素 $k_{ij}^{(e)}$。令其对应的全局行索引 $I = L_e[i]$，全局列索引 $J = L_e[j]$。然后执行加法：$K_{IJ} = K_{IJ} + k_{ij}^{(e)}$。
    d. 遍历 $\mathbf{f}_e$ 的所有元素 $f_{i}^{(e)}$。令其对应的全局索引 $I = L_e[i]$。然后执行加法：$F_{I} = F_{I} + f_{i}^{(e)}$。

这个过程自动确保了在共享节点上的刚度和力贡献被正确地累加起来。值得注意的是，力向量的组装也必须使用[转置](@entry_id:142115)的连接性映射，即 $A_e^T \mathbf{f}_e$。这意味着，$\mathbf{f}_e$ 的第 $i$ 个分量被添加到由 $L_e$ 的第 $i$ 个条目指定的全局自由度上，这严格依赖于单元局部自由度的定义顺序。[@problem_id:2615783]

### 施加本质边界条件

组装完成的全局系统 $\mathbf{K}\mathbf{U} = \mathbf{F}$ 通常是奇异的，因为它尚未包含防止刚体运动的约束。**[本质边界条件](@entry_id:173524) (essential boundary conditions)**（或[Dirichlet边界条件](@entry_id:142800)）规定了某些自由度的位移值，例如 $u_i = g_i$。有多种方法来施加这些条件。

#### 消除法

最直接的方法是**消除法 (elimination method)** [@problem_id:2615720]。我们将全局自由度向量 $\mathbf{U}$ 划分为未知的**自由自由度 (free DOFs)** $\mathbf{u}_f$ 和已知的**指定自由度 (prescribed DOFs)** $\mathbf{u}_p = \mathbf{g}$。相应地，全局系统可以被分块：
$$
\begin{pmatrix} \mathbf{K}_{ff} & \mathbf{K}_{fp} \\ \mathbf{K}_{pf} & \mathbf{K}_{pp} \end{pmatrix} \begin{pmatrix} \mathbf{u}_{f} \\ \mathbf{u}_{p} \end{pmatrix} = \begin{pmatrix} \mathbf{f}_{f} \\ \mathbf{f}_{p} \end{pmatrix}
$$
展开第一行方程：
$$
\mathbf{K}_{ff} \mathbf{u}_{f} + \mathbf{K}_{fp} \mathbf{u}_{p} = \mathbf{f}_{f}
$$
将已知值 $\mathbf{u}_p = \mathbf{g}$ 代入并整理，我们得到一个只包含未知量 $\mathbf{u}_f$ 的简化系统：
$$
\mathbf{K}_{ff} \mathbf{u}_{f} = \mathbf{f}_{f} - \mathbf{K}_{fp} \mathbf{g}
$$
只要施加的约束足以消除所有刚体模式，矩阵 $\mathbf{K}_{ff}$ 就将是正定的，因此是可逆的。求解这个简化系统即可得到所有自由自由度的位移 $\mathbf{u}_f = \mathbf{K}_{ff}^{-1}(\mathbf{f}_{f} - \mathbf{K}_{fp}\mathbf{g})$。项 $-\mathbf{K}_{fp}\mathbf{g}$ 可以被理解为指定位移 $\mathbf{g}$ 在自由自由度上引起的等效力。

#### [罚函数法](@entry_id:636090)与拉格朗日乘子法

对于复杂的约束或大规模计算，**[罚函数法](@entry_id:636090) (penalty method)** 和 **拉格朗日乘子法 (Lagrange multiplier method)** 提供了更通用的替代方案 [@problem_id:2615803]。

*   **罚函数法**通过向总[势能](@entry_id:748988)中添加一个惩罚项 $\frac{1}{2}\alpha (\mathbf{C}\mathbf{U} - \mathbf{g})^T(\mathbf{C}\mathbf{U} - \mathbf{g})$ 来近似满足约束 $\mathbf{C}\mathbf{U} = \mathbf{g}$。这导致修改后的系统为 $(\mathbf{K} + \alpha\mathbf{C}^{T}\mathbf{C})\mathbf{U} = \mathbf{F} + \alpha\mathbf{C}^{T}\mathbf{g}$。该方法保持系统大小不变且矩阵[对称正定](@entry_id:145886)，但约束是近似满足的，且大的罚参数 $\alpha$ 会导致系统矩阵的条件数恶化。

*   **[拉格朗日乘子法](@entry_id:176596)**通过引入一组新的变量——[拉格朗日乘子](@entry_id:142696) $\boldsymbol{\lambda}$——来精确地强制执行约束。这会形成一个更大的增广系统：
    $$
    \begin{pmatrix}\mathbf{K} & \mathbf{C}^{T} \\ \mathbf{C} & \mathbf{0}\end{pmatrix}\begin{pmatrix}\mathbf{U} \\ \boldsymbol{\lambda}\end{pmatrix} = \begin{pmatrix}\mathbf{F} \\ \mathbf{g}\end{pmatrix}
    $$
    该方法能精确满足约束，且没有参数引发的病态问题，但代价是系统规模增大，且[增广矩阵](@entry_id:150523)是**对称不定的 (symmetric indefinite)**，需要特殊的求解器。

### 关于[非线性](@entry_id:637147)的注记

本章所建立的框架 $\mathbf{K}\mathbf{U} = \mathbf{F}$ 隐含了一个基本假设：这是一个线性系统。这种线性源于两个方面：**[几何线性](@entry_id:203076)**（[应变-位移关系](@entry_id:173321)线性）和**材料线性**（[应力-应变关系](@entry_id:274093)线性）。在这种情况下，内能是位移的二次函数 $\Pi_{\text{int}} = \frac{1}{2}\mathbf{U}^T\mathbf{K}\mathbf{U}$，其梯度（即[内力](@entry_id:167605)）是位移的线性函数 $\mathbf{f}_{\text{int}} = \mathbf{K}\mathbf{U}$。[@problem_id:2615765]

当遇到大位移、大转动（[几何非线性](@entry_id:169896)）或材料响应[非线性](@entry_id:637147)时，内能不再是位移的简单二次函数。因此，[内力向量](@entry_id:750751) $\mathbf{f}_{\text{int}}(\mathbf{U})$ 成为位移的[非线性](@entry_id:637147)函数。[平衡方程](@entry_id:172166)变为一个[非线性方程组](@entry_id:178110)：
$$
\mathbf{R}(\mathbf{U}) = \mathbf{f}_{\text{int}}(\mathbf{U}) - \mathbf{F} = \mathbf{0}
$$
这个[方程组](@entry_id:193238)必须通过迭代方法（如牛顿-拉夫逊法）求解。这类方法需要计算[内力向量](@entry_id:750751)关于位移的[雅可比矩阵](@entry_id:264467)，即**切向刚度矩阵 (tangent stiffness matrix)**:
$$
\mathbf{K}_T(\mathbf{U}) = \frac{\partial \mathbf{f}_{\text{int}}(\mathbf{U})}{\partial \mathbf{U}}
$$
$\mathbf{K}_T$ 不再是一个常数，而是依赖于当前的变形状态。尽管如此，本章介绍的从单元到全局的组装思想，即通过连接性映射进行“散开-相加”，在[非线性](@entry_id:637147)分析中依然适用，只不过组装的对象变成了依赖于构型的单元切向刚度矩阵和[内力向量](@entry_id:750751)。