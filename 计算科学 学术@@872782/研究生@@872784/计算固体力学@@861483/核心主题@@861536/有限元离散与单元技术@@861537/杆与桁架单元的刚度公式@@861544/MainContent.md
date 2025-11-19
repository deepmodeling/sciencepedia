## 引言
杆与[桁架单元](@entry_id:177354)的[刚度矩阵](@entry_id:178659)公式是计算[结构力学](@entry_id:276699)乃至整个有限元方法的基石。从宏伟的桥梁到微观的细胞骨架，无数复杂系统的力学行为分析都依赖于这一基本构件。然而，将一个连续的物理结构转化为可由计算机求解的[离散数学](@entry_id:149963)模型，面临着如何精确捕捉其力学本质的挑战。本文旨在系统性地解决这一问题，为读者构建一个从理论基础到前沿应用的完整知识框架。

本文将通过三个章节层层递进。在“原理与机制”一章中，我们将回归第一性原理，从位移插值和[能量守恒](@entry_id:140514)出发，一步步推导出[单元刚度矩阵](@entry_id:139369)，并探讨如何将各个[单元组装](@entry_id:140000)成一个完整的结构系统。随后，在“应用与跨学科连接”一章中，我们将展示这一基本模型如何演化和扩展，以应对[结构动力学](@entry_id:172684)、几何与[材料非线性](@entry_id:162855)、多物理场耦合等高级工程难题，并揭示其在[生物力学](@entry_id:153973)、[结构优化](@entry_id:176910)等交叉学科中的强大生命力。最后，“动手实践”部分将提供一系列精心设计的编程练习，帮助您将理论知识转化为可靠的计算工具。现在，让我们从最核心的原理开始，深入探索杆与[桁架单元](@entry_id:177354)的力学世界。

## 原理与机制

本章旨在从第一性原理出发，系统地阐述构成计算结构力学基础的杆和[桁架单元](@entry_id:177354)的[刚度矩阵](@entry_id:178659)公式。我们将从最基本的运动学假设开始，通过能量原理推导出[单元刚度矩阵](@entry_id:139369)，然后探讨坐标变换和[全局系统组装](@entry_id:749932)的方法，并最终分析所得[系统矩阵](@entry_id:172230)的内在物理意义。

### 有限元概念：从连续介质到离散系统

正如前言所述，有限元方法的核心思想在于将一个连续的物理场（如[位移场](@entry_id:141476)）离散为一组有限数量的节点值的组合。对于[一维杆单元](@entry_id:171268)，这意味着我们将沿着杆件轴线变化的连续位移函数 $u(x)$ 用其在端点处的位移值来近似表示。这种近似是通过引入一组[插值函数](@entry_id:262791)来实现的，这些函数在有限[元理论](@entry_id:638043)中被称为**形函数 (Shape Functions)**。

### 杆单元的[运动学](@entry_id:173318)描述

#### [位移场](@entry_id:141476)插值

形函数是建立离散节点位移与单元内任意点连续位移之间关系的关键。对于一个位于 $x \in [0, L]$ 区间、拥有两个节点（节点1在 $x=0$，节点2在 $x=L$）的直杆单元，其内部任意一点的轴向位移 $u(x)$ 可以通过节点位移 $u_1$ 和 $u_2$ 进行[线性插值](@entry_id:137092)：

$u(x) = N_1(x) u_1 + N_2(x) u_2$

其中，$N_1(x)$ 和 $N_2(x)$ 就是形函数。这些函数必须满足一些基本性质，才能保证近似的合理性。我们可以从以下几个基本要求出发来构建它们 [@problem_id:3602955]：

1.  **克罗内克-德尔塔 (Kronecker-delta) 性质**：在任意一个节点上，该节点的形函数值必须为1，而所有其他节点的形函数值必须为0。这保证了插值位移在节点处与节点位移值完全吻合。
    *   在节点1 ($x=0$): $N_1(0)=1$, $N_2(0)=0$
    *   在节点2 ($x=L$): $N_1(L)=0$, $N_2(L)=1$

2.  **[单位分解](@entry_id:150115) (Partition of Unity) 性质**：单元内任意一点的所有形函数之和必须恒等于1，即 $N_1(x) + N_2(x) = 1$。这个性质保证了当所有节点位移相同时（即 $u_1 = u_2 = c$），单元内的位移场也是一个常数（$u(x)=c$）。这对应于物理上的**刚体平动 (rigid body motion)**，这种运动不应产生任何应变。

假设形函数为 $x$ 的线性多项式，例如 $N_i(x) = a_i + b_i x$，利用上述克罗内克-德尔[塔性质](@entry_id:273153)，我们可以唯一地确定这些系数，得到：

$N_1(x) = 1 - \frac{x}{L}$

$N_2(x) = \frac{x}{L}$

可以验证，这两个函数确实满足单位分解性质。此外，它们还满足**线性完备性 (linear completeness)**，即能够精确地表示任意线性[位移场](@entry_id:141476) $u(x) = a+bx$。这保证了单元能够精确地模拟**常应变状态 (constant strain state)**，这是有限元单元收敛性的一个基本要求。

#### [应变-位移关系](@entry_id:173321)

在小变形假设下，一维[轴向应变](@entry_id:160811) $\varepsilon$ 定义为位移场的空间导数：

$\varepsilon(x) = \frac{du}{dx}$

将插值位移表达式代入，我们得到：

$\varepsilon(x) = \frac{d}{dx}(N_1(x) u_1 + N_2(x) u_2) = \frac{dN_1}{dx} u_1 + \frac{dN_2}{dx} u_2$

计算形函数的导数：

$\frac{dN_1}{dx} = -\frac{1}{L}, \quad \frac{dN_2}{dx} = \frac{1}{L}$

因此，应变可以表示为：

$\varepsilon(x) = -\frac{1}{L} u_1 + \frac{1}{L} u_2 = \frac{u_2 - u_1}{L}$

这个结果至关重要：对于采用线性形函数的二节点杆单元，其内部的应变场是**常数**。我们可以将此关系写成矩阵形式：

$\varepsilon = \mathbf{B} \mathbf{d}_e$

其中，$\mathbf{d}_e = \begin{pmatrix} u_1 \\ u_2 \end{pmatrix}$ 是单元节点位移向量，而 $\mathbf{B} = \begin{pmatrix} -\frac{1}{L} & \frac{1}{L} \end{pmatrix}$ 被称为**[应变-位移矩阵](@entry_id:163451)**或几何矩阵。

#### [桁架单元](@entry_id:177354)的基本假设

虽然我们推导了杆单元的[轴向变形](@entry_id:180213)，但在将其应用于桁架结构时，我们隐含了一些重要的物理假设 [@problem_id:3602959]。[桁架单元](@entry_id:177354)被定义为仅能承受轴向拉伸或压缩的构件，其节点被视为理想的**铰接 (pin-jointed)**。这意味着：

1.  **纯轴向[位移场](@entry_id:141476)**：在单元的局部坐标系中，我们只考虑引起应变的轴向位移 $u(x)$。横向位移（垂直于杆轴的位移）在[一阶近似](@entry_id:147559)下只引起单元的[刚体转动](@entry_id:191086)，而不产生应变。虽然高阶效应中横向位移差会引起[轴向应变](@entry_id:160811)（[几何非线性](@entry_id:169896)效应），但在小变形线性理论中，这一效应被忽略。
2.  **无剪切应变**：[桁架单元](@entry_id:177354)假设不具备抗剪能力。为了保证这一点，运动学上必须强制剪切应变为零。例如，对于三维情况，剪切应变 $\varepsilon_{xy} = \frac{1}{2}(\frac{\partial u}{\partial y} + \frac{\partial v}{\partial x})$。假设位移场只沿轴向 $x$ 变化，则 $\frac{\partial u}{\partial y}=0$。为使 $\varepsilon_{xy}=0$，必须有 $\frac{dv}{dx}=0$，即横向位移 $v$ 沿杆长为常数。这再次表明，横向位移仅与[刚体运动](@entry_id:193355)相关。
3.  **排除[转动自由度](@entry_id:141502)**：由于节点是理想铰接，它们不能传递[弯矩](@entry_id:202968)。在能量原理中，力和位移是共轭的（做功），同样，弯矩和转角也是共轭的。因为没有[弯矩](@entry_id:202968)传递，节点的[转动自由度](@entry_id:141502)不会对单元的[应变能](@entry_id:162699)产生任何贡献。因此，在推导单元刚度时，[转动自由度](@entry_id:141502)被排除在外。

### [单元刚度矩阵](@entry_id:139369)的推导（[局部坐标系](@entry_id:751394)）

[单元刚度矩阵](@entry_id:139369) $k_e$ 将单元的节点力向量 $f_e$ 与其节点位移向量 $d_e$ 联系起来：$f_e = k_e d_e$。我们可以通过两个等价的能量原理来推导它。

#### 方法一：[最小势能原理](@entry_id:173340)

[最小势能原理](@entry_id:173340)指出，在平衡状态下，弹性体的总[势能](@entry_id:748988)取得最小值。总[势能](@entry_id:748988) $\Pi$ 由内部[应变能](@entry_id:162699) $U$ 和外力[势能](@entry_id:748988) $W_{pot}$ 组成。我们关注应变能部分。对于[线性弹性](@entry_id:166983)材料，应变能为：

$U = \frac{1}{2} \int_V \sigma \varepsilon \, dV$

其中 $\sigma$ 是应力。对于一根[横截面](@entry_id:154995)积为 $A$ 的杆，体积微元 $dV = A \, dx$。利用胡克定律 $\sigma = E \varepsilon$（$E$ 为杨氏模量），并将应变与节点位移关联起来 $\varepsilon = \mathbf{B} \mathbf{d}_e$，我们得到 [@problem_id:3603024]：

$U = \frac{1}{2} \int_0^L (\mathbf{B} \mathbf{d}_e)^T E (\mathbf{B} \mathbf{d}_e) A \, dx$

由于节点位移向量 $\mathbf{d}_e$ 不随积分变量 $x$ 变化，可以将其移到积分号外：

$U = \frac{1}{2} \mathbf{d}_e^T \left( \int_0^L \mathbf{B}^T E A \mathbf{B} \, dx \right) \mathbf{d}_e$

此表达式具有二次型 $U = \frac{1}{2} \mathbf{d}_e^T k_e \mathbf{d}_e$ 的形式。通过比较，我们识别出[单元刚度矩阵](@entry_id:139369)为：

$k_e = \int_0^L \mathbf{B}^T E A \mathbf{B} \, dx$

对于具有恒定 $E$ 和 $A$ 的均匀杆，$\mathbf{B}$ 也是常数，积分变得非常简单：

$k_e = \mathbf{B}^T E A \mathbf{B} \int_0^L dx = (\mathbf{B}^T E A \mathbf{B}) L$

代入 $\mathbf{B} = \frac{1}{L} \begin{pmatrix} -1 & 1 \end{pmatrix}$：

$k_e = \begin{pmatrix} -1/L \\ 1/L \end{pmatrix} E A \begin{pmatrix} -1/L & 1/L \end{pmatrix} L = \frac{EA}{L^2} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix} L = \frac{EA}{L} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}$

这就是二节点杆单元在局部坐标系下的[刚度矩阵](@entry_id:178659)。

#### 方法二：虚功原理

[虚功原理](@entry_id:138749) (PVW) 是一个更为普适的原理，它指出对于任何满足运动学约束的[虚位移](@entry_id:168781) $\delta u$，[内力](@entry_id:167605)所做的[虚功](@entry_id:176403) $\delta W_{int}$ 等于外力所做的[虚功](@entry_id:176403) $\delta W_{ext}$ [@problem_id:3602996]。

$\delta W_{int} = \delta W_{ext}$

[内力](@entry_id:167605)[虚功](@entry_id:176403)是应力与虚应变在体积上的积分：

$\delta W_{int} = \int_V \sigma^T \delta \varepsilon \, dV = \int_0^L (E \varepsilon)^T (\delta \varepsilon) A \, dx$

将位移和[虚位移](@entry_id:168781)都用形函数离散化：$\varepsilon = \mathbf{B} \mathbf{d}_e$ 和 $\delta \varepsilon = \mathbf{B} \delta \mathbf{d}_e$。

$\delta W_{int} = \int_0^L (\mathbf{B} \mathbf{d}_e)^T E (\mathbf{B} \delta \mathbf{d}_e) A \, dx = \delta \mathbf{d}_e^T \left( \int_0^L \mathbf{B}^T E A \mathbf{B} \, dx \right) \mathbf{d}_e$

我们看到，括号中的表达式正是我们通过[势能](@entry_id:748988)原理得到的[刚度矩阵](@entry_id:178659) $k_e$。根据定义，[内力](@entry_id:167605)[虚功](@entry_id:176403)也可以表示为节点[内力](@entry_id:167605)与节点[虚位移](@entry_id:168781)的[点积](@entry_id:149019) $\delta W_{int} = \delta \mathbf{d}_e^T f_{int}$，其中 $f_{int} = k_e \mathbf{d}_e$。这再次确认了刚度矩阵的表达式。

#### 刚度矩阵的物理解释

我们推导出的刚度矩阵 $k_e = \frac{EA}{L} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}$ 蕴含着丰富的物理意义 [@problem_id:3603005]。矩阵的每一列代表了对相应自由度施加单位位移，同时保持其他自由度为零时，在所有节点上产生的反力向量。

*   **第1列**: 施加位移 $u_1=1, u_2=0$。这相当于将杆件压缩了单位长度。产生的节点力为 $f_e = k_e \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \frac{EA}{L} \begin{pmatrix} 1 \\ -1 \end{pmatrix}$。$f_1 = \frac{EA}{L} > 0$，表示在节点1需要一个沿+x方向的力来维持位移；$f_2 = -\frac{EA}{L} < 0$，表示在节点2产生一个沿-x方向的反力，以保持平衡。

*   **第2列**: 施加位移 $u_1=0, u_2=1$。这相当于将杆件拉伸了单位长度。产生的节点力为 $f_e = k_e \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \frac{EA}{L} \begin{pmatrix} -1 \\ 1 \end{pmatrix}$。$f_1 = -\frac{EA}{L} < 0$，为节点1的反力；$f_2 = \frac{EA}{L} > 0$，为在节点2施加的拉力。

*   **对角项 ($k_{11}, k_{22}$)** 总是正的，代表了在一个节点施加位移时，该节点自身产生的直接抵抗力。
*   **非对角项 ($k_{12}, k_{21}$)** 总是负的，代表了在一个节点施加位移时，另一个节点上产生的反力，体现了节点间的力学耦合。
*   **[刚体运动](@entry_id:193355)**: 考虑刚体平动，$u_1=u_2=c$。产生的节点力为 $f_e = k_e \begin{pmatrix} c \\ c \end{pmatrix} = \frac{EA}{L} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix} \begin{pmatrix} c \\ c \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$。这表明刚体运动不产生内力，这是任何[单元刚度矩阵](@entry_id:139369)必须满足的基本性质。

### 推广与外载荷

[刚度矩阵](@entry_id:178659)的积分形式使其能够轻松处理更复杂的情况，如材料属性或几何形状沿杆长变化。

#### 非均匀属性的单元

考虑一个[杨氏模量](@entry_id:140430)沿杆长线性变化的情况，$E(x) = E_0 + E_1 x$ [@problem_id:3602990]。[刚度矩阵](@entry_id:178659)的计算只需在积[分时](@entry_id:274419)使用这个变化的 $E(x)$：

$k_e = A \int_0^L (E_0 + E_1 x) \mathbf{B}^T \mathbf{B} \, dx = \frac{A}{L^2} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix} \int_0^L (E_0 + E_1 x) \, dx$

计算积分：$\int_0^L (E_0 + E_1 x) \, dx = E_0 L + \frac{E_1 L^2}{2}$。

代回得到：$k_e = \frac{A}{L} (E_0 + \frac{E_1 L}{2}) \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix} = \frac{A \bar{E}}{L} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}$，其中 $\bar{E} = E_0 + \frac{E_1 L}{2}$ 是杆件的平均[杨氏模量](@entry_id:140430)。这表明，对于线性单元，使用平均模量的均匀杆模型可以得到相同的结果。

#### 等效节点载荷

当结构承受沿其长度[分布](@entry_id:182848)的载荷 $q(x)$（力/单位长度）时，我们需要将此连续载荷转换为一组在能量上等效的**节点[载荷向量](@entry_id:635284) (consistent nodal load vector)**。这同样可以从[虚功原理](@entry_id:138749)得到。外力[虚功](@entry_id:176403)项为：

$\delta W_{ext} = \int_0^L \delta u(x) q(x) \, dx$

用形函数表示[虚位移](@entry_id:168781) $\delta u(x) = \mathbf{N}(x) \delta \mathbf{d}_e = (N_1(x) \delta u_1 + N_2(x) \delta u_2)$：

$\delta W_{ext} = \int_0^L (\mathbf{N}(x) \delta \mathbf{d}_e)^T q(x) \, dx = \delta \mathbf{d}_e^T \int_0^L \mathbf{N}(x)^T q(x) \, dx$

外力[虚功](@entry_id:176403)也可以表示为 $\delta W_{ext} = \delta \mathbf{d}_e^T f_b$，其中 $f_b$ 就是等效节点[载荷向量](@entry_id:635284)。因此：

$f_b = \int_0^L \mathbf{N}(x)^T q(x) \, dx$

对于一个[均匀分布](@entry_id:194597)的载荷 $q$，我们计算得到 [@problem_id:3602990]：

$f_b = q \int_0^L \begin{pmatrix} 1 - x/L \\ x/L \end{pmatrix} dx = q \begin{pmatrix} L/2 \\ L/2 \end{pmatrix} = \frac{qL}{2} \begin{pmatrix} 1 \\ 1 \end{pmatrix}$

这意味着一个作用在整个单元上的均布载荷 $qL$ 在能量上等效于将总载荷平均分配到两个节点上。

### 从局部到全局：桁架[结构分析](@entry_id:153861)

单个单元的物理行为在其[局部坐标系](@entry_id:751394)（轴线方向）中描述最为简单。然而，一个完整的结构由许多不同方向的单元组成，需要在统一的[全局坐标系](@entry_id:171029)中进行分析。

#### [坐标变换](@entry_id:172727)

考虑一个在三维空间中的[桁架单元](@entry_id:177354)，连接节点1和节点2 [@problem_id:3602993]。定义一个从节点1指向节点2的单位向量 $\mathbf{\hat{e}}$，其在[全局坐标系](@entry_id:171029) $(X,Y,Z)$ 下的分量为**[方向余弦](@entry_id:170591) (direction cosines)** $(c_x, c_y, c_z)$。

一个节点的局部轴向位移 $u_a$ 是其全局位移向量 $\mathbf{d}_{global} = (u_X, u_Y, u_Z)$ 在单位向量 $\mathbf{\hat{e}}$ 上的投影：

$u_a = \mathbf{d}_{global} \cdot \mathbf{\hat{e}} = c_x u_X + c_y u_Y + c_z u_Z$

对于一个二[节点单元](@entry_id:752523)，其局部节点位移向量 $\mathbf{d}_e = \begin{pmatrix} u_{1a} \\ u_{2a} \end{pmatrix}$ 与其全局节点位移向量 $\mathbf{d}_g = (u_{1X}, u_{1Y}, u_{1Z}, u_{2X}, u_{2Y}, u_{2Z})^T$ 之间的关系可以写成：

$\mathbf{d}_e = T \mathbf{d}_g$

其中 $T$ 是一个 $2 \times 6$ 的**[变换矩阵](@entry_id:151616) (transformation matrix)**：

$T = \begin{pmatrix} c_x & c_y & c_z & 0 & 0 & 0 \\ 0 & 0 & 0 & c_x & c_y & c_z \end{pmatrix}$

#### [全局坐标系](@entry_id:171029)下的单元刚度

单元的[应变能](@entry_id:162699) $U$ 是一个标量，其值不应依赖于[坐标系](@entry_id:156346)的选择。利用这一能量[不变性原理](@entry_id:199405)，我们可以推导出[全局坐标系](@entry_id:171029)下的[单元刚度矩阵](@entry_id:139369) $K_e$ [@problem_id:3603023]。

$U = \frac{1}{2} \mathbf{d}_e^T k_e \mathbf{d}_e = \frac{1}{2} (T \mathbf{d}_g)^T k_e (T \mathbf{d}_g) = \frac{1}{2} \mathbf{d}_g^T (T^T k_e T) \mathbf{d}_g$

比较二次型 $U = \frac{1}{2} \mathbf{d}_g^T K_e \mathbf{d}_g$，我们得到全局[单元刚度矩阵](@entry_id:139369)：

$K_e = T^T k_e T$

对于一个二维平面[桁架单元](@entry_id:177354)，其方向由与全局x轴的夹角 $\theta$ 定义，[方向余弦](@entry_id:170591)为 $c = \cos\theta, s = \sin\theta$。其 $4 \times 4$ [全局刚度矩阵](@entry_id:138630)为：

$K_e = \frac{EA}{L} \begin{pmatrix} c^2 & cs & -c^2 & -cs \\ cs & s^2 & -cs & -s^2 \\ -c^2 & -cs & c^2 & cs \\ -cs & -s^2 & cs & s^2 \end{pmatrix}$

这里的非对角项 $cs$ 体现了**坐标耦合**。例如，$K_{e,12} = \frac{EA}{L}cs$ 表示在节点1施加一个y方向的位移 $u_{1y}$，会在该节点产生一个x方向的反力 $F_{1x}$。这是因为y方向的位移会使倾斜的杆件产生轴向伸长或缩短，从而产生轴向力，而这个轴向力在全局x轴上有一个分量。当杆件与坐标轴平行时（$\theta=0$ 或 $\pi/2$），$cs=0$，耦合项消失。

#### [全局刚度矩阵](@entry_id:138630)的组装

得到所有单元的[全局刚度矩阵](@entry_id:138630) $K_e$ 后，最后一步是将它们**组装 (assemble)** 成整个结构的**[全局刚度矩阵](@entry_id:138630) $K$**。这个过程被称为**[直接刚度法](@entry_id:176969) (Direct Stiffness Method)** [@problem_id:3603032]。

1.  **自由度索引 (DOF Indexing)**：首先，为整个结构的所有自由度建立一个唯一的编号系统。一个通用的方法是按节点顺序遍历，对每个节点的自由度（如$u_x, u_y$）进行编号。例如，对于一个有 $N$ 个节点的二维桁架，节点 $i$ 的自由度 $(u_{ix}, u_{iy})$ 可以编号为 $(2i-1, 2i)$。

2.  **散布-累加 (Scatter-Add)**：对于每个单元，我们根据其连接的节点号和上述索引规则，确定其4个自由度在全局自由度向量中的位置。然后，将该单元 $4 \times 4$ 刚度矩阵 $K_e$ 的每个元素 $K_{e,pq}$ 加到[全局刚度矩阵](@entry_id:138630) $K$ 中对应于这些全局位置的条目上。

例如，考虑一个由节点 $(1,2)$, $(2,3)$, $(2,4)$ 连接的三杆桁架。
*   单元 $e_1$ (节点1,2) 的自由度对应全局索引 $[1,2,3,4]$。
*   单元 $e_2$ (节点2,3) 的自由度对应全局索引 $[3,4,5,6]$。
*   单元 $e_3$ (节点2,4) 的自由度对应全局索引 $[3,4,7,8]$。

组装时，单元 $e_1$ 的刚度矩阵被添加到 $K$ 的左上角 $4 \times 4$ 区域。单元 $e_2$ 的刚度矩阵则加到由全局行/列 $[3,4,5,6]$ 定义的区域。注意到节点2是共享节点，其对应的全局自由度 $(3,4)$ 会接收来自所有三个单元的刚度贡献。这种累加操作在物理上反映了作用在共享节点上的力是所有连接到该节点的单元[内力](@entry_id:167605)的总和。

### 组装系统的性质

组装完成的[全局刚度矩阵](@entry_id:138630) $K$ 包含了整个结构的力学行为信息。

#### [刚体模态](@entry_id:754366)与[零空间](@entry_id:171336)

对于一个未施加任何位移约束（即“自由漂浮”）的结构，其[全局刚度矩阵](@entry_id:138630) $K$ 是奇异的（即[行列式](@entry_id:142978)为零）。这是因为结构可以作为一个整体进行**刚体运动**（如平动和转动），而这种运动不会在结构内部产生任何应变或应力，因此不储存应变能 [@problem_id:3602969]。

一个对应于刚体运动的节点位移向量 $\mathbf{d}_{rb}$，代入[应变能](@entry_id:162699)表达式中，会得到零能量：

$U = \frac{1}{2} \mathbf{d}_{rb}^T K \mathbf{d}_{rb} = 0$

同时，这也意味着 $K \mathbf{d}_{rb} = \mathbf{0}$。在代数上，这意味着刚体位移向量 $\mathbf{d}_{rb}$ 位于矩阵 $K$ 的**[零空间](@entry_id:171336) (null space)** 中。[零空间](@entry_id:171336)的维度等于矩阵 $K$ 的[秩亏](@entry_id:754065)数，也等于其零[特征值](@entry_id:154894)的[几何重数](@entry_id:155584)。

对于一个二维平面结构，存在三个独立的[刚体模态](@entry_id:754366)：沿x轴平动、沿y轴平动和绕平面外z轴的转动。因此，其[全局刚度矩阵](@entry_id:138630)的[零空间](@entry_id:171336)维度至少为3。

考虑一个由三根杆件组成的三角形桁架。我们可以组装其 $6 \times 6$ 的[全局刚度矩阵](@entry_id:138630) $K$，并找到其[刚体模态](@entry_id:754366)向量：
*   **x-平动**: $\mathbf{d}_{Tx} = (1, 0, 1, 0, 1, 0)^T$
*   **y-[平动](@entry_id:187700)**: $\mathbf{d}_{Ty} = (0, 1, 0, 1, 0, 1)^T$
*   **绕原点转动**: 对于一个绕原点的小角度 $\phi$ 转动，节点 $i$ 在 $(x_i, y_i)$ 处的位移为 $(-\phi y_i, \phi x_i)$。因此，相应的[刚体模态](@entry_id:754366)向量为 $\mathbf{d}_{R} \propto (-y_1, x_1, -y_2, x_2, \dots, -y_N, x_N)^T$。

我们可以验证这些向量确实满足 $K \mathbf{d} = \mathbf{0}$。

一个关键问题是：是否存在除[刚体模态](@entry_id:754366)之外的其他[零能模](@entry_id:172472)态？如果存在，这些模态被称为**机构 (mechanisms)**或**零能机制**，它们代表结构在不储存能量的情况下可以发生内部变形。一个稳定的结构，如基本的三角形桁架，是没有机构的。因此，对于一个稳定的自由结构，其刚度矩阵[零空间](@entry_id:171336)的维度恰好等于其[刚体模态](@entry_id:754366)的数量（二维为3，三维为6）。这个结论是评估[结构稳定性](@entry_id:147935)和进行有限元分析前进行模型检查的重要依据。