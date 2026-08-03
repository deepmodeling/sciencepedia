## 引言
间断伽辽金（Discontinuous Galerkin, DG）方法已成为数值求解双曲守恒律的主流方法之一，这类方程描述了从航空航天中的高速流体到地面上的交通拥堵等多种关键物理现象。DG方法凭借其对复杂几何的适应性、灵活的p自适应能力以及出色的并行扩展性，在高阶计算领域备受青睐。

尽管DG方法功能强大，但其理论核心——弱形式的构建、数值通量的选择及其对稳定性和精度的深远影响——对于初学者和研究人员而言可能显得错综复杂。如何将抽象的弱形式理论与稳健、精确的数值格式联系起来，是有效应用DG方法的关键所在。

本文旨在系统性地揭示DG弱形式的精髓。我们将首先在“原理与机制”一章中，从第一性原理出发，推导DG弱形式，阐明数值通量的作用，并分析其基本性质。随后，在“应用与交叉学科联系”一章中，我们将展示该方法如何被应用于解决地球物理、工程和网络科学等领域的复杂问题。最后，“动手实践”部分将通过具体的计算练习，将理论与实践紧密结合，帮助读者巩固所学知识。通过这一层层递进的结构，本文将引导读者从基本概念的建立，逐步深入到方法的实际应用与前沿拓展，最终全面掌握双曲系统DG弱形式的理论与实践。

## 原理与机制

本章旨在深入阐述间断伽辽金（Discontinuous Galerkin, DG）方法求解双曲系统的核心原理与关键机制。我们将从单个计算单元上的弱形式推导入手，逐步揭示数值通量的作用、半离散系统的构建、基本性质（如守恒性与稳定性），并探讨实际应用中的关键技术环节，如时间步长限制、精度分析和数值积分。最后，我们将介绍一些旨在提升非线性问题鲁棒性与计算效率的现代DG方法变体。

### 单元弱形式的推导

我们从一个$d$维空间中的双曲守恒律系统出发：
$$
\boldsymbol{u}_t + \nabla\cdot \boldsymbol{f}(\boldsymbol{u}) = \boldsymbol{0}
$$
其中，$\boldsymbol{u}: \Omega \times 0, T) \to \mathbb{R}^m$ 是[守恒变量的向量，$\boldsymbol{f}: \mathbb{R}^m \to \mathbb{R}^{m \times d}$ 是通量张量。DG方法的核心思想在于将求解域 $\Omega$ 剖分为一系列不重叠的单元 $K$，并在每个单元上使用多项式来逼近解。与连续伽辽金方法不同，DG方法允许逼近解 $\boldsymbol{u}_h$ 在单元边界处存在间断。

为了推导DG方法的弱形式，我们在一个单元 $K$ 上，将上述偏微分方程（PDE）与一个任意的矢量值测试函数 $\boldsymbol{v}_h$ 做内积，然后进行积分。测试函数 $\boldsymbol{v}_h$ 与逼近解 $\boldsymbol{u}_h$ 来自同一个预先定义好的分片多项式函数空间。
$$
\int_K \boldsymbol{v}_h^\top \boldsymbol{u}_{h,t} \,d\boldsymbol{x} + \int_K \boldsymbol{v}_h^\top (\nabla\cdot \boldsymbol{f}(\boldsymbol{u}_h)) \,d\boldsymbol{x} = 0
$$
由于 $\boldsymbol{u}_h$ 在单元间是间断的，其导数在边界上没有良好定义，直接处理包含 $\nabla\cdot \boldsymbol{f}(\boldsymbol{u}_h)$ 的第二项会遇到困难。DG方法的关键步骤是对第二项使用分部积分（或高斯散度定理），将微分算子从通量 $\boldsymbol{f}(\boldsymbol{u}_h)$ 转移到测试函数 $\boldsymbol{v}_h$ 上。经过分部积分，我们得到：
$$
\int_K \boldsymbol{v}_h^\top (\nabla\cdot \boldsymbol{f}(\boldsymbol{u}_h)) \,d\boldsymbol{x} = \int_{\partial K} \boldsymbol{v}_h^\top (\boldsymbol{f}(\boldsymbol{u}_h)\cdot \boldsymbol{n}) \,ds - \int_K \nabla \boldsymbol{v}_h : \boldsymbol{f}(\boldsymbol{u}_h) \,d\boldsymbol{x}
$$
其中，$\partial K$ 是单元 $K$ 的边界，$\boldsymbol{n}$ 是指向单元外部的单位法向量，而 $\nabla \boldsymbol{v}_h : \boldsymbol{f}(\boldsymbol{u}_h)$ 是一个缩写，表示 $\sum_{j=1}^d (\partial_{x_j}\boldsymbol{v}_h)^\top \boldsymbol{f}_j(\boldsymbol{u}_h)$。将此式代回原积分方程，便得到单元上的初步弱形式：
$$
\int_K \boldsymbol{v}_h^\top \boldsymbol{u}_{h,t} \,d\boldsymbol{x} - \int_K \nabla \boldsymbol{v}_h : \boldsymbol{f}(\boldsymbol{u}_h) \,d\boldsymbol{x} + \int_{\partial K} \boldsymbol{v}_h^\top (\boldsymbol{f}(\boldsymbol{u}_h)\cdot \boldsymbol{n}) \,ds = 0
$$
这个形式将原始PDE转化为了一个只涉及单元内部积分和边界积分的方程，为处理间断解铺平了道路 [@problem_id:3377294]。

### 数值通量的角色

上述弱形式中的边界积分项 $\int_{\partial K} \boldsymbol{v}_h^\top (\boldsymbol{f}(\boldsymbol{u}_h)\cdot \boldsymbol{n}) \,ds$ 存在一个本质上的模糊性。由于解 $\boldsymbol{u}_h$ 在单元边界上是间断的，它在边界 $F \subset \partial K$ 上同时存在两个值：来自单元 $K$ 内部的迹（interior trace），记为 $\boldsymbol{u}_h^-$，以及来自相邻单元的迹（exterior trace），记为 $\boldsymbol{u}_h^+$。因此，物理通量 $\boldsymbol{f}(\boldsymbol{u}_h)\cdot \boldsymbol{n}$ 在边界上是多值的，这使得积分无法确定。

DG方法通过引入一个**数值通量 (numerical flux)** $\hat{\boldsymbol{f}}$ 来解决这个问题。数值通量是一个单值函数，它依赖于界面两侧的解的状态（$\boldsymbol{u}_h^-$ 和 $\boldsymbol{u}_h^+$）以及法向量 $\boldsymbol{n}$，即 $\hat{\boldsymbol{f}}(\boldsymbol{u}_h^-, \boldsymbol{u}_h^+; \boldsymbol{n})$。我们用这个单值的数值通量来代替模糊的物理通量。因此，最终的DG弱形式为：在每个单元 $K \in \mathcal{T}_h$ 上，寻找 $\boldsymbol{u}_h$ 使得对于所有测试函数 $\boldsymbol{v}_h$，下式成立：
$$
\int_K \boldsymbol{v}_h^\top \boldsymbol{u}_{h,t} \,d\boldsymbol{x} - \int_K \nabla \boldsymbol{v}_h : \boldsymbol{f}(\boldsymbol{u}_h) \,d\boldsymbol{x} + \int_{\partial K} \boldsymbol{v}_h^{-\top} \hat{\boldsymbol{f}}(\boldsymbol{u}_h^-, \boldsymbol{u}_h^+; \boldsymbol{n}) \,ds = 0
$$
这里，测试函数的迹也取自单元内部，即 $\boldsymbol{v}_h^-$。一个合理的数值通量必须满足两个基本属性 [@problem_id:3377294]：

1.  **相容性 (Consistency)**：如果界面两侧的解恰好相等，即 $\boldsymbol{u}^- = \boldsymbol{u}^+ = \boldsymbol{u}$，数值通量必须退化为物理通量。数学上表示为 $\hat{\boldsymbol{f}}(\boldsymbol{u}, \boldsymbol{u}; \boldsymbol{n}) = \boldsymbol{f}(\boldsymbol{u})\cdot \boldsymbol{n}$。这个属性确保了当数值解足够光滑时，我们的格式能够正确地逼近原始的PDE。

2.  **守恒性 (Conservation)**：为了保证离散格式在全局上是守恒的（即总质量不随时间增减），数值通量必须满足一个反对称关系。通过在所有单元上对弱形式求和，并取测试函数 $\boldsymbol{v}_h = \text{const}$，可以推导出，为了使边界通量项在内部界面上两两抵消，数值通量必须满足 $\hat{\boldsymbol{f}}(\boldsymbol{u}^-, \boldsymbol{u}^+; \boldsymbol{n}) + \hat{\boldsymbol{f}}(\boldsymbol{u}^+, \boldsymbol{u}^-; -\boldsymbol{n}) = \boldsymbol{0}$。这里，$-\boldsymbol{n}$ 是相邻单元相对于同一界面的外法向量。

一个广泛使用的数值通量是**迎风通量 (upwind flux)**。对于线性双曲系统，其思想是根据特征波的传播方向来选择通量。例如，对于线性平流方程 $u_t + \nabla \cdot (\boldsymbol{a} u) = 0$，法向通量为 $(\boldsymbol{a} \cdot \boldsymbol{n}) u$。迎风通量的定义为：如果 $\boldsymbol{a} \cdot \boldsymbol{n} \ge 0$（信息从单元内部流向外部），则取内部值 $u^-$ 计算通量；如果 $\boldsymbol{a} \cdot \boldsymbol{n}  0$（信息从外部流入），则取外部值 $u^+$ 计算通量。

让我们通过一个具体的例子来理解数值通量的计算，该例子涉及几何变换和迎风通量的确定 [@problem_id:3377335]。考虑二维常系数线性平流方程 $u_{t} + \nabla \cdot (\boldsymbol{a} u) = 0$，其中速度向量为 $\boldsymbol{a} = (1, -2)$。假设一个物理单元 $\Omega_e$ 是通过双线性映射从参考正方形 $\hat{\Omega} = [-1,1]^2$ 变换得到的。我们关注其底边，对应于参考坐标 $\eta=-1$。通过给定的映射关系 $x(\xi,\eta) = \frac{1}{4}(1+\xi)(3-\eta)$ 和 $y(\xi,\eta) = \frac{1}{2}(1+\eta)$，我们可以发现当 $\eta=-1$ 时，物理坐标为 $(x, y) = (1+\xi, 0)$。这是一条从 $(0,0)$ 到 $(2,0)$ 的直线段。该单元位于 $y>0$ 的区域，因此底边的外法向量为 $\hat{\boldsymbol{n}}=(0,-1)$。为了确定迎风方向，我们计算 $\boldsymbol{a} \cdot \hat{\boldsymbol{n}} = (1, -2) \cdot (0, -1) = 2$。因为结果为正，表示流动方向朝向单元外部，所以应采用内部迹 $u^-$ 来计算通量。因此，该边界上的数值通量为 $F^* = (\boldsymbol{a} \cdot \hat{\boldsymbol{n}}) u^- = 2u^-$。此后，通过计算测试函数和逼近解在该边界上的迹，并将它们代入边界积分 $\int_{\eta=-1} v^{-} F^* ds$，即可得到该边界对弱形式的贡献。这个过程展示了在实际计算中如何处理几何、确定法向量以及应用数值通量法则。

### 半离散系统：从PDE到ODE

DG弱形式将时空连续的PDE转化为了一个在空间上离散、在时间上连续的方程。为了进行数值求解，我们需要将此积分方程转化为一个常微分方程（ODE）组。

这一步通过在每个单元的多项式空间 $V_h(K)$ 中选取一组基函数 $\{\phi_j(\boldsymbol{x})\}_{j=1}^{N_p}$ 来实现，其中 $N_p$ 是该空间维度。逼近解 $\boldsymbol{u}_h$ 和测试函数 $\boldsymbol{v}_h$ 可以表示为这些基函数的线性组合：
$$
\boldsymbol{u}_h(\boldsymbol{x}, t) = \sum_{j=1}^{N_p} \boldsymbol{c}_j(t) \phi_j(\boldsymbol{x})
$$
其中，$\boldsymbol{c}_j(t) \in \mathbb{R}^m$ 是随时间变化的待求系数向量。将此展开式代入弱形式，并依次选取测试函数为每个基函数 $\boldsymbol{v}_h = \phi_i(\boldsymbol{x}) \boldsymbol{e}_k$（其中 $\boldsymbol{e}_k$ 是 $\mathbb{R}^m$ 的标准基向量），我们将得到一个关于系数向量 $\vec{\boldsymbol{c}} = (\boldsymbol{c}_1, \dots, \boldsymbol{c}_{N_p})^\top$ 的ODE系统。该系统通常具有以下形式：
$$
\boldsymbol{M} \frac{d\vec{\boldsymbol{c}}}{dt} = \vec{\boldsymbol{R}}(\vec{\boldsymbol{c}})
$$
其中，$\boldsymbol{M}$ 是**质量矩阵 (mass matrix)**，$\vec{\boldsymbol{R}}(\vec{\boldsymbol{c}})$ 是包含了体积积分和边界通量积分贡献的**残差向量 (residual vector)**。质量矩阵的元素由基函数的内积定义：$M_{ij} = \int_K \phi_i(\boldsymbol{x}) \phi_j(\boldsymbol{x}) \,d\boldsymbol{x}$。由于基函数仅在单元 $K$ 内部有支撑，质量矩阵是块对角的，每个块对应一个单元的局部质量矩阵。

基函数的选择对结果有重要影响。例如，在参考单元 $K=[-1,1]$ 上，我们可以选择最简单的**单项式基** $\{1, \xi, \xi^2, \dots, \xi^p\}$。对于 $p=2$ 的情况，基函数为 $\{1, \xi, \xi^2\}$ [@problem_id:3377336]。对应的 $3 \times 3$ 局部质量矩阵 $M$ 的元素 $M_{ij} = \int_{-1}^1 \xi^i \xi^j d\xi$ (对于 $i,j=0,1,2$) 可以精确计算出来：
$$
M = \begin{pmatrix} 2  0  \frac{2}{3} \\ 0  \frac{2}{3}  0 \\ \frac{2}{3}  0  \frac{2}{5} \end{pmatrix}
$$
这个矩阵是对称正定的。然而，单项式基在 $p$ 较大时会变得近似线性相关，导致质量矩阵是**病态的 (ill-conditioned)**。例如，对于上述 $p=2$ 的单项式基，质量矩阵的谱条件数（最大特征值与最小特征值之比）为 $\kappa(M) = (71 + 9\sqrt{61})/10 \approx 14.1$ [@problem_id:3377336]。随着 $p$ 的增加，该条件数会迅速增长，给求解线性系统带来数值困难。为了改善条件数，通常选用**正交基**，如勒让德多项式基 [@problem_id:3377306]，它能产生对角的质量矩阵，从而大大简化计算。

### 基本性质：守恒性与稳定性

一个可靠的数值格式必须具备某些与原始PDE相符的基本性质，其中最重要的是质量守恒和能量稳定性。

#### 质量守恒

正如之前在讨论数值通量时提到的，守恒性是数值通量的一个核心要求。对于半离散（也称**线方法 Method-of-Lines, MoL**）DG格式，我们可以严格证明其质量守恒性。通过在所有单元上对弱形式求和，并选择测试函数为常数 $v_h=1$（这是一个0次多项式，因此是任何 $p \ge 0$ 的多项式空间中的有效测试函数），体积积分中的梯度项 $\nabla v_h$ 为零。整个方程简化为所有边界通量之和。由于周期性边界条件和数值通量的守恒性质，所有界面通量贡献相互抵消，最终得到总质量的时间变化率为零：
$$
\frac{d}{dt} \int_{\Omega} u_h \,dx = \sum_K \frac{d}{dt} \int_K u_h \,dx = 0
$$
这一性质对于任何满足守恒性的数值通量都成立，并且与网格是否均匀无关。此外，由于总质量是系数向量的线性组合，任何龙格-库塔（Runge-Kutta）类的时间积分方法都能精确地保持这种守恒性 [@problem_id:3377327]。

#### 能量稳定性 ($L^2$-稳定性)

对于双曲问题，解的能量（通常用 $L^2$ 范数的平方来衡量）不应无界增长。一个稳定的数值格式应能模拟这一特性。通过在弱形式中选择测试函数与解相同，即 $v_h = u_h$，我们可以分析离散能量 $E(t) = \frac{1}{2}\int_\Omega u_h^2 \,dx$ 的时间演化。

对于线性平流方程，可以证明，如果使用**迎风通量**，能量的时间变化率满足 $\frac{dE}{dt} \le 0$。能量的耗散来源于单元界面上解的跳跃项。具体来说，每个界面上的能量耗散项形如 $-\frac{1}{2} |\lambda| [u_h]^2$，其中 $\lambda$ 是特征速度，$[u_h] = u_h^+ - u_h^-$ 是解在界面上的跳跃。由于该项总是非正的，总能量是单调不增的。这保证了半离散格式的 $L^2$-稳定性。而如果使用**中心通量**（即两侧状态的简单平均），界面上的耗散项为零，格式是能量守恒的，但这通常会牺牲鲁棒性 [@problem_id:3377327]。

当使用**强稳定保持（Strong Stability Preserving, SSP）**的龙格-库塔方法进行时间积分时，只要时间步长满足一定条件（通常是前向欧拉法稳定的CFL条件），这种半离散的能量不增性质就可以在全离散层面上得以保持 [@problem_id:3377327]。

除了线方法，还有一种**时空DG (Space-Time DG)** 方法，它将时间和空间同等对待，在时空单元上构建弱形式。时空DG方法同样具有精确的质量守恒性，其能量稳定性也取决于时空界面上数值通量的选择，与线方法DG有着相似的性质 [@problem_id:3377327]。

### 实际实现与分析

将DG方法付诸实践涉及几个关键环节：时间积分方案的选择、数值精度的评估以及数值积分的准确性。

#### 时间积分与CFL条件

半离散DG方法产生了一个大型ODE系统 $\boldsymbol{M} \frac{d\vec{\boldsymbol{c}}}{dt} = \vec{\boldsymbol{R}}(\vec{\boldsymbol{c}})$。对于双曲问题，通常采用显式时间积分方法，如显式龙格-库塔方法。显式方法的稳定性受到时间步长 $\Delta t$ 的限制，这通常由**Courant-Friedrichs-Lewy (CFL)** 条件给出。对于DG方法，一个充分的CFL条件为 [@problem_id:3377303]：
$$
\Delta t \le C \frac{h}{\alpha_{\max}(2p+1)}
$$
其中，$h$ 是单元尺寸，$\alpha_{\max}$ 是最大特征波速的绝对值，$p$ 是多项式次数，$C$ 是一个与具体时间积分方法相关的常数。这个公式揭示了时间步长限制的几个关键依赖关系：
-   与单元尺寸 $h$ 成正比：网格越细，允许的时间步长越小。
-   与最大波速 $\alpha_{\max}$ 成反比：物理波速越快，时间步长需越小。
-   与 $(2p+1)$ 成反比：多项式次数 $p$ 越高，允许的时间步长越小。这一依赖关系源于高次多项式在单元边界上的值可能远大于其在单元内部的平均值，这种关系可以通过多项式迹不等式来量化。例如，在参考区间上的迹不等式表明 $|v(-1)|^2 + |v(1)|^2 \le (p+1)^2 \|v\|_{L^2(-1,1)}^2/\|v\|_{L^2(-1,1)}^2$。

#### 色散与耗散分析

为了评估DG格式的精度，我们可以对其进行**傅里叶分析**（或对于周期网格的**Bloch-Floquet分析**）。这种分析研究格式如何传播具有不同波数 $k$ 的平面波解。理想情况下，数值解的波应以与精确解相同的速度传播。偏差表现为两种主要误差：

-   **色散误差 (Dispersion error)**：数值相速度 $c_{\text{DG}}$ 依赖于波数，导致不同波长的波以不同速度传播，造成波形变形。
-   **耗散误差 (Dissipation error)**：数值波的振幅随时间衰减，即使原始PDE是纯守恒的。

以一维线性平流方程 $u_t - a u_x = 0$（精确相速度为 $c_{\text{exact}} = -a$）的DG($p=0$)格式为例，通过傅里叶分析可以推导出数值相速度与波数的关系。使用迎风通量，最终得到的符号相对相速度误差为 [@problem_id:3377312]：
$$
\varepsilon(\theta) = \frac{c_{\text{DG}}(\theta)}{c_{\text{exact}}} - 1 = \frac{\sin(kh)}{kh} - 1
$$
其中 $\theta = kh$ 是无量纲波数。由于 $\sin(kh)/(kh) \le 1$，这表明所有波长的数值波都比精确解传播得慢（滞后相误差）。对于高频波（$kh \to \pi$），相速度误差最严重。对于更高阶的DG($p=1$)格式，同样可以进行此分析，得到更复杂的色散关系，但其在高频区的精度通常优于低阶格式 [@problem_id:3377306]。

#### 数值积分与非线性问题

在前面的讨论中，我们假设所有积分都能精确计算。然而，对于非线性通量或弯曲边界的单元，弱形式中的积分 $\int_K \nabla \boldsymbol{v} : \boldsymbol{f}(\boldsymbol{u}_h) \,d\boldsymbol{x}$ 和 $\int_{\partial K} \boldsymbol{v}^\top \hat{\boldsymbol{f}} \,ds$ 必须通过**数值求积 (numerical quadrature)** 来近似。一个求积阶为 $Q$ 的求积公式能精确积分所有次数不超过 $Q$ 的多项式。

如果求积精度不足，会导致**混淆误差 (aliasing error)**，即被积函数中的高频分量被错误地表示为低频分量，这会破坏格式的稳定性，尤其是在求解非线性问题时。为了保持（熵）稳定性，我们需要确保求积公式能精确计算弱形式中的所有积分。

我们可以通过分析被积函数的最高多项式次数来确定所需的最小求积阶 $Q$ [@problem_id:3377334]。假设解和测试函数是 $p$ 次多项式，通量函数 $\boldsymbol{f}(\boldsymbol{u})$ 本身是关于其变量 $\boldsymbol{u}$ 的 $r$ 次多项式。
-   在**体积积分** $\int_K \nabla \boldsymbol{v} : \boldsymbol{f}(\boldsymbol{u}_h) \,d\boldsymbol{x}$ 中，$\nabla \boldsymbol{v}$ 的次数是 $p-1$，而 $\boldsymbol{f}(\boldsymbol{u}_h)$ 是一个复合函数，其空间多项式次数为 $rp$。因此，被积函数的总次数为 $(p-1) + rp$。
-   在**面积分** $\int_{\partial K} \boldsymbol{v}^\top \hat{\boldsymbol{f}} \,ds$ 中，$\boldsymbol{v}$ 的次数是 $p$，而数值通量 $\hat{\boldsymbol{f}}$（假设其多项式次数与物理通量一致）的次数是 $rp$。因此，被积函数的总次数为 $p + rp$。

为了确保两个积分都精确，求积阶 $Q$ 必须大于等于两者中的较大值。因此，所需的最小求积阶为：
$$
Q \ge p(r+1)
$$
例如，对于带有二次通量（如Burgers方程，$r=2$）的P2（$p=2$）格式，需要求积阶至少为 $Q \ge 2(2+1)=6$ 才能避免体积积分和面积分中的混淆误差。

### 高级主题与现代变体

标准的DG方法虽然强大，但在处理某些复杂情况（如包含激波的非线性问题）时可能会遇到挑战，或者在计算成本上不是最优的。这催生了许多高级的变体。

#### 非线性问题的熵稳定性

对于非线性守恒律，仅有 $L^2$ 稳定性是不够的，还需要满足物理上的**熵条件**，以保证解的唯一性和物理相关性。标准的DG格式，尤其是在数值积分不精确时，可能会产生非物理的振荡并导致计算崩溃。

一种增强稳定性的现代技术是构造**熵守恒 (entropy-conservative)** 或**熵稳定 (entropy-stable)** 的格式。对于某些问题，如Burgers方程 $u_t + \partial_x(u^2/2)=0$，这可以通过精心设计弱形式中的非线性项来实现。例如，使用所谓的**分裂形式 (split-form)**，将非线性项 $\partial_x f(u)$ 分解为强形式和弱形式的加权平均。通过利用Summation-By-Parts (SBP) 性质的离散算子，可以证明，当强弱形式的权重参数 $\alpha$ 取特定值时，体积积分项对离散能量（或熵）的贡献可以完全转化为边界项，从而消除内部的伪能量产生源 [@problem_id:3377315]。对于Burgers方程，这个理想的参数值是 $\alpha=1/2$。

#### 可混合DG方法 (HDG)

尽管DG方法具有高度的并行性和灵活性，但其全局耦合的自由度数量可能非常大（每个单元内的所有系数都参与全局求解）。**可混合DG（Hybridizable DG, HDG）**方法是一种旨在降低计算成本的变体 [@problem_id:3377337]。

HDG的核心思想是在网格的所有边（或面）上引入一个新的全局未知量——**迹 (trace)** $\widehat{\boldsymbol{w}}$。这个迹变量是单值的，充当了相邻单元间通信的桥梁。HDG格式包含两组方程：
1.  **局部方程**：在每个单元上，求解一个只涉及该单元内部未知量 $\boldsymbol{w}$ 和其边界上迹变量 $\widehat{\boldsymbol{w}}$ 的方程。对于给定的迹 $\widehat{\boldsymbol{w}}$，内部解 $\boldsymbol{w}$ 可以在每个单元上独立并行地求解出来。
2.  **全局方程**：通过要求数值通量在单元界面上弱连续，建立一个只涉及所有迹变量 $\widehat{\boldsymbol{w}}$ 的全局耦合系统。

这个过程被称为**静态凝聚 (static condensation)**。它允许我们将单元内部的自由度在局部消除，最终得到一个规模小得多的全局线性系统，其未知量仅为网格骨架上的迹变量。

HDG方法的效率优势体现在全局耦合自由度的数量上。在一个大型的二维三角网格上，对于 $p$ 次多项式，HDG方法的全局自由度数量与标准DG方法的全局自由度数量之比为 [@problem_id:3377337]：
$$
R(k) = \frac{3}{k+2}
$$
这个比率表明，随着多项式次数 $k$ 的增加，HDG方法在全局求解阶段的计算成本相比于标准DG方法有显著的降低（例如，对于 $k=4$，自由度数量减少到 DG 的一半），使其在高阶模拟中极具吸引力。