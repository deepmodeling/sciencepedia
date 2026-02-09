## 引言
复合材料层合板因其卓越的比强度和比刚度，已成为航空航天、交通运输等尖端工程领域的关键结构材料。然而，要充分发挥其性能优势，必须依赖精确的力学分析模型。经典层合板理论（CLT）虽然简洁，但其忽略横向剪切变形的假设使其仅适用于薄板结构，在分析中厚板或剪切刚度较弱的夹层结构时会产生显著误差。

为解决这一难题，一阶剪切变形理论（First-order Shear Deformation Theory, FSDT）应运而生。它通过放宽经典理论的运动学约束，计入了横向剪切变形的影响，极大地扩展了板壳理论的适用范围，成为现代复合材料结构分析的基石。本文将系统地引导读者深入探索FSDT的理论精髓与工程智慧。

在“原理与机制”一章中，我们将从FSDT的基本运动学假设出发，详细推导其应变场和著名的ABD本构关系，并剖析剪切修正因子背后的物理思想。随后，在“应用与跨学科交叉”一章中，我们将展示该理论如何在结构稳定性、动力学分析、夹层结构设计以及热力学行为预测等实际工程问题中发挥关键作用。最后，通过“动手实践”一章提供的精选计算练习，您将有机会亲手应用所学知识，解决具体的力学问题，从而巩固对FSDT的理解。通过这三章的学习，您将构建起一个完整而坚实的FSDT知识体系。

## 原理与机制

本章在前一章介绍的背景之上，将深入探讨层合板一阶剪切变形理论（First-order Shear Deformation Theory, FSDT）的核心原理与力学机制。我们将从其基本运动学假设出发，推导应变场和本构关系，并讨论该理论的关键特征，包括拉伸-弯曲耦合、横向剪切效应的处理及其固有的局限性，最后还将触及相关的计算力学问题。

### FSDT运动学假设

经典层合板理论（Classical Lamination Theory, CLT）建立在Kirchhoff-Love假设之上，即板的变形过程中，初始垂直于中面的法线始终保持为伸直、不可伸长且垂直于变形后的中面。这一假设直接导致横向剪切应变为零，因此CLT适用于薄板结构，但对于中厚板，其横向剪切变形的贡献不可忽略，CLT会低估板的挠度并高估其刚度。

为了克服这一限制，一阶剪切变形理论（FSDT），又称Reissner-Mindlin板理论，对Kirchhoff-Love假设进行了关键性的松弛。FSDT的核心运动学假设是：

1.  **法线保持伸直**: 初始垂直于中面的法线在变形后仍然保持为直线。
2.  **法线不再保持垂直**: 该直线不再被强制要求垂直于变形后的中面，而是可以独立于中面坡度发生转动。
3.  **厚度不可压缩**: 板的横向位移沿厚度方向不发生变化，即板的厚度在变形过程中保持不变。

基于这些假设，对于一个中面位于 $z=0$ 的板，其上任意一点 $(x, y, z)$ 的位移场可以表示为：
$$
\begin{align*}
u(x,y,z) = u_0(x,y) + z \phi_x(x,y) \\
v(x,y,z) = v_0(x,y) + z \phi_y(x,y) \\
w(x,y,z) = w_0(x,y)
\end{align*}
$$
其中，$u_0(x,y)$、$v_0(x,y)$ 和 $w_0(x,y)$ 分别是中面沿 $x$、$y$ 和 $z$ 方向的位移分量。与CLT不同，这里的 $\phi_x(x,y)$ 和 $\phi_y(x,y)$ 是两个独立的运动学变量，它们分别代表了横截面法线绕 $y$ 轴和 $x$ 轴的转角 [@problem_id:2887260]。这两个转角与中面挠度的偏导数（即中面坡度）$-\frac{\partial w_0}{\partial x}$ 和 $-\frac{\partial w_0}{\partial y}$ 不再强制相等，正是这种独立性使得理论能够计入横向剪切变形。放宽Kirchhoff约束的物理动机在于，对于中厚板，横向剪切应变能对总应变能的贡献变得显著，强制其为零会引入较大误差 [@problem_id:2642022]。

### 运动学推论与应变场

根据FSDT的位移场假设，我们可以利用小应变几何关系推导出板内的应变分量。

**面内应变与横向正应变**

面内应变分量（$\epsilon_{xx}$, $\epsilon_{yy}$, $\gamma_{xy}$）由位移场对 $x$ 和 $y$ 求导得到。将FSDT位移表达式代入应变-位移关系，可得：
$$
\boldsymbol{\epsilon}(z) =
\begin{Bmatrix} \epsilon_{xx} \\ \epsilon_{yy} \\ \gamma_{xy} \end{Bmatrix} =
\begin{Bmatrix} \frac{\partial u_0}{\partial x} \\ \frac{\partial v_0}{\partial y} \\ \frac{\partial u_0}{\partial y} + \frac{\partial v_0}{\partial x} \end{Bmatrix} +
z \begin{Bmatrix} \frac{\partial \phi_x}{\partial x} \\ \frac{\partial \phi_y}{\partial y} \\ \frac{\partial \phi_x}{\partial y} + \frac{\partial \phi_y}{\partial x} \end{Bmatrix}
$$
这表明面内应变沿厚度坐标 $z$呈线性分布。我们可以将此表达式分解为中面应变 $\boldsymbol{\epsilon}_0$ 和板的曲率 $\boldsymbol{\kappa}$ 的组合：
$$
\boldsymbol{\epsilon}(z) = \boldsymbol{\epsilon}_0 + z \boldsymbol{\kappa}
$$
其中：
$$
\boldsymbol{\epsilon}_0 = \begin{Bmatrix} \frac{\partial u_0}{\partial x} \\ \frac{\partial v_0}{\partial y} \\ \frac{\partial u_0}{\partial y} + \frac{\partial v_0}{\partial x} \end{Bmatrix}, \quad
\boldsymbol{\kappa} = \begin{Bmatrix} \frac{\partial \phi_x}{\partial x} \\ \frac{\partial \phi_y}{\partial y} \\ \frac{\partial \phi_x}{\partial y} + \frac{\partial \phi_y}{\partial x} \end{Bmatrix}
$$
这里的 $\boldsymbol{\epsilon}_0$ 描述了中面的拉伸与剪切变形，而 $\boldsymbol{\kappa}$ 则描述了板的弯曲与扭转变形 [@problem_id:2887241]。

此外，FSDT的第三条运动学假设 $w(x,y,z) = w_0(x,y)$ 直接导致了横向正应变 $\epsilon_{zz}$ 恒为零：
$$
\epsilon_{zz} = \frac{\partial w}{\partial z} = \frac{\partial w_0(x,y)}{\partial z} = 0
$$
这意味着该理论不考虑板的厚度拉伸或压缩变形 [@problem_id:2641975]。同时，由于面内位移 $u$ 和 $v$ 仅是 $z$ 的线性函数，这表明初始为平面的横截面在变形后仍然保持为平面，即FSDT不考虑横截面的翘曲（warping） [@problem_id:2641975]。

**横向剪切应变**

FSDT与CLT最本质的区别体现在横向剪切应变上。根据应变-位移关系：
$$
\gamma_{xz} = \frac{\partial u}{\partial z} + \frac{\partial w}{\partial x} = \phi_x(x,y) + \frac{\partial w_0(x,y)}{\partial x}
$$
$$
\gamma_{yz} = \frac{\partial v}{\partial z} + \frac{\partial w}{\partial y} = \phi_y(x,y) + \frac{\partial w_0(x,y)}{\partial y}
$$
由于 $\phi_x, \phi_y$ 和 $w_0$ 都是 $x, y$ 的函数，与 $z$ 无关，因此FSDT预测的横向剪切应变 $\gamma_{xz}$ 和 $\gamma_{yz}$ 在整个板的厚度上是**常数** [@problem_id:2887315]。只有当法线转角恰好等于中面坡度的负值（即 $\phi_x = -\partial w_0 / \partial x$ 和 $\phi_y = -\partial w_0 / \partial y$）时，横向剪切应变才为零，此时FSDT退化为CLT的运动学关系。

### 层合板本构关系

层合板的宏观力学行为是通过对其各组成单层（lamina）的力学行为沿厚度积分得到的。

#### 单层本构

首先考虑构成层合板的单个正交各向异性（orthotropic）材料层，在平面应力（plane stress）状态下，其主方向坐标系 $(1,2)$ 中的应力-应变关系为 $\boldsymbol{\sigma} = \mathbf{Q} \boldsymbol{\epsilon}$。其中，$\mathbf{Q}$ 是约化刚度矩阵，其各分量可由材料的工程常数表示。为满足热力学第二定律，刚度矩阵必须对称，这要求材料的泊松比和弹性模量之间满足互易关系 $\nu_{21}/E_2 = \nu_{12}/E_1$。由此，$\mathbf{Q}$ 矩阵的完整形式为 [@problem_id:2641953]：
$$
\mathbf{Q} = \begin{bmatrix}
Q_{11} & Q_{12} & 0 \\
Q_{12} & Q_{22} & 0 \\
0 & 0 & Q_{66}
\end{bmatrix} =
\begin{bmatrix}
\frac{E_1}{1-\nu_{12}\nu_{21}} & \frac{\nu_{12}E_2}{1-\nu_{12}\nu_{21}} & 0 \\
\frac{\nu_{12}E_2}{1-\nu_{12}\nu_{21}} & \frac{E_2}{1-\nu_{12}\nu_{21}} & 0 \\
0 & 0 & G_{12}
\end{bmatrix}
$$
在层合板分析中，需将各单层的刚度矩阵 $\mathbf{Q}$ 从其材料主方向转换到层合板的全局坐标系 $(x,y)$，得到转换后的刚度矩阵 $\bar{\mathbf{Q}}$。

#### ABD 刚度矩阵

层合板的力学行为通常用内力（单位宽度上的力）和内力矩（单位宽度上的力矩）来描述。它们通过对整个厚度 $h$ 上的应力进行积分得到：
$$
\mathbf{N} = \begin{Bmatrix} N_x \\ N_y \\ N_{xy} \end{Bmatrix} = \int_{-h/2}^{h/2} \begin{Bmatrix} \sigma_x \\ \sigma_y \\ \tau_{xy} \end{Bmatrix} dz
$$
$$
\mathbf{M} = \begin{Bmatrix} M_x \\ M_y \\ M_{xy} \end{Bmatrix} = \int_{-h/2}^{h/2} z \begin{Bmatrix} \sigma_x \\ \sigma_y \\ \tau_{xy} \end{Bmatrix} dz
$$
将单层本构关系 $\boldsymbol{\sigma}(z) = \bar{\mathbf{Q}}(z) \boldsymbol{\epsilon}(z)$ 和FSDT应变关系 $\boldsymbol{\epsilon}(z) = \boldsymbol{\epsilon}_0 + z \boldsymbol{\kappa}$ 代入积分，即可建立层合板的宏观本构方程：
$$
\begin{Bmatrix} \mathbf{N} \\ \mathbf{M} \end{Bmatrix} =
\begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B} & \mathbf{D} \end{bmatrix}
\begin{Bmatrix} \boldsymbol{\epsilon}_0 \\ \boldsymbol{\kappa} \end{Bmatrix}
$$
这就是著名的 **ABD 刚度矩阵**。其中，$\mathbf{A}$、$\mathbf{B}$、$\mathbf{D}$ 分别是 $3 \times 3$ 的子矩阵，分别称为拉伸刚度矩阵、耦合刚度矩阵和弯曲刚度矩阵。它们的定义为 [@problem_id:2887241, 2641993]：
$$
A_{ij} = \sum_{k=1}^{N} \bar{Q}_{ij}^{(k)} (z_k - z_{k-1})
$$
$$
B_{ij} = \frac{1}{2} \sum_{k=1}^{N} \bar{Q}_{ij}^{(k)} (z_k^2 - z_{k-1}^2)
$$
$$
D_{ij} = \frac{1}{3} \sum_{k=1}^{N} \bar{Q}_{ij}^{(k)} (z_k^3 - z_{k-1}^3)
$$
这里，$z_{k-1}$ 和 $z_k$ 是第 $k$ 铺层的下、上表面坐标。$\mathbf{A}$ 矩阵关联了中面应变与面内力，$\mathbf{D}$ 矩阵关联了曲率与弯矩，而 $\mathbf{B}$ 矩阵则描述了拉伸与弯曲之间的耦合效应。

#### 拉伸-弯曲耦合

**耦合刚度矩阵 $\mathbf{B}$** 具有重要的物理意义。当 $\mathbf{B}$ 矩阵非零时，面内载荷（$\mathbf{N}$）可以引起弯曲和扭转变形（$\boldsymbol{\kappa}$），反之亦然。这种现象称为**拉伸-弯曲耦合**。考虑一个思想实验：对一个层合板仅施加面内力 $\mathbf{N}^{\text{ext}}$，而不施加任何外部弯矩（$\mathbf{M}^{\text{ext}}=\mathbf{0}$）。根据本构关系，我们有：
$$
\mathbf{N}^{\text{ext}} = \mathbf{A}\boldsymbol{\epsilon}_0 + \mathbf{B}\boldsymbol{\kappa}
$$
$$
\mathbf{0} = \mathbf{B}\boldsymbol{\epsilon}_0 + \mathbf{D}\boldsymbol{\kappa}
$$
从第二个方程可解得 $\boldsymbol{\kappa} = -\mathbf{D}^{-1}\mathbf{B}\boldsymbol{\epsilon}_0$。这意味着，只要 $\mathbf{B}$ 矩阵非零，且施加的载荷使得中面应变 $\boldsymbol{\epsilon}_0$ 非零，板就必然会产生曲率 $\boldsymbol{\kappa}$，即便没有外部弯矩作用 [@problem_id:2641982]。

$\mathbf{B}$ 矩阵是否为零，取决于铺层顺序的对称性。从其定义 $\mathbf{B} = \int z \bar{\mathbf{Q}}(z) dz$ 可以看出，它代表了刚度沿厚度的“一阶矩”。如果层合板的铺层关于中面（$z=0$）是几何和材料对称的（即对于任意 $z$，都有 $\bar{\mathbf{Q}}(z) = \bar{\mathbf{Q}}(-z)$），则被积函数 $z \bar{\mathbf{Q}}(z)$ 是一个奇函数，其在对称区间 $[-h/2, h/2]$ 上的积分恒为零，即 $\mathbf{B} = \mathbf{0}$。对于对称层合板，拉伸与弯曲行为是解耦的 [@problem_id:2641982, 2641993]。值得注意的是，拉伸刚度矩阵 $\mathbf{A}$ 的定义是 $\int \bar{\mathbf{Q}}(z) dz$，它与坐标原点的选择无关；而耦合刚度矩阵 $\mathbf{B}$ 则依赖于 $z=0$ 参考面的选取 [@problem_id:2641993]。

### 横向剪切本构及其局限性

#### 横向剪切刚度与剪切修正因子

除了面内行为，FSDT还需建立横向剪切力与剪切应变之间的关系。横向剪力合力 $\mathbf{Q}$ 定义为：
$$
\mathbf{Q} = \begin{Bmatrix} Q_x \\ Q_y \end{Bmatrix} = \int_{-h/2}^{h/2} \begin{Bmatrix} \tau_{xz} \\ \tau_{yz} \end{Bmatrix} dz
$$
在FSDT框架下，横向剪切应变 $\boldsymbol{\gamma}_0$ 在厚度上为常数。因此，剪力合力与剪切应变的关系可以写为 $\mathbf{Q} = \mathbf{A}_s \boldsymbol{\gamma}_0$，其中 $\mathbf{A}_s$ 是层合板的横向剪切刚度矩阵 [@problem_id:2887241]。其定义为各单层横向剪切刚度沿厚度的积分。

然而，这里存在一个严重的问题。如前所述，FSDT的恒定剪切应变假设，通过线弹性本构关系，将导致分片恒定的剪切应力分布。这与物理现实严重不符——对于顶部和底部表面无切向载荷的板，其横向剪切应力在这些表面必须为零。真实的剪切应力分布更接近于抛物线形 [@problem_id:2641975, 2887280]。

直接使用恒定应力模型会显著高估板的抗剪刚度。为了弥补这一理论缺陷，FSDT引入了**剪切修正因子** $k$（或写作 $\kappa$）。这个因子的核心思想是**能量等效** [@problem_id:2642009]。它通过修正（通常是折减）横向剪切刚度，使得在给定剪力合力 $Q_x$ 的情况下，FSDT模型计算出的剪切应变能，与基于更精确的三维弹性理论计算出的剪切应变能相等。通过令FSDT的应变能 $U^{\text{FSDT}} = \frac{1}{2} Q_x \gamma_{xz}^0$ 等于三维理论的应变能 $U^{\text{3D}} = \frac{1}{2} \int_{-h/2}^{h/2} \frac{\tau_{xz}(z)^2}{G_{xz}(z)} dz$，可以推导出剪切修正因子的精确表达式 [@problem_id:2642009, 2642018]：
$$
k = \frac{\left(\int_{-h/2}^{h/2} \tau_{xz}(z) dz\right)^2}{\left(\int_{-h/2}^{h/2} G_{xz}(z) dz\right) \left(\int_{-h/2}^{h/2} \frac{\tau_{xz}(z)^2}{G_{xz}(z)} dz\right)}
$$
经过修正后，层合板的横向剪切本构关系写作 $\mathbf{Q} = k \mathbf{A}_s^* \boldsymbol{\gamma}_0$，其中 $\mathbf{A}_s^*$ 是未修正的剪切刚度。剪切修正因子的引入是对FSDT简单运动学假设的一种“事后”能量校准，它使得FSDT在宏观响应（如挠度）上能给出更准确的预测。需要强调的是，剪切修正因子只作用于横向剪切刚度，并不会改变 $\mathbf{A}$, $\mathbf{B}$, $\mathbf{D}$ 矩阵的定义 [@problem_id:2641993, 2641993]。

#### 真实剪切应力的恢复

由于FSDT通过本构关系直接给出的剪切应力分布是错误的，当需要精确的层间剪切应力时（例如用于失效分析），必须采用后处理方法进行恢复。标准的恢复方法是利用三维弹性力学的平衡方程 [@problem_id:2887280]：
$$
\frac{\partial \tau_{xz}}{\partial z} = - \left( \frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} \right)
$$
$$
\frac{\partial \tau_{yz}}{\partial z} = - \left( \frac{\partial \sigma_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} \right)
$$
该方法的步骤是：首先，利用已求得的FSDT解（即中面应变 $\boldsymbol{\epsilon}_0$ 和曲率 $\boldsymbol{\kappa}$），计算出面内应力 $\boldsymbol{\sigma}(z) = \bar{\mathbf{Q}}(z) (\boldsymbol{\epsilon}_0 + z \boldsymbol{\kappa})$ 沿厚度的分布。然后，将面内应力对 $x, y$ 的导数代入上述平衡方程。最后，从一个已知剪应力的表面（如板的底面 $z=-h/2$，此处 $\tau_{xz}=0$）开始，沿厚度方向对平衡方程进行积分，即可逐层恢复出满足平衡条件和边界条件的、物理上更真实的（通常是分片抛物线形）横向剪切应力分布 [@problem_id:2887280]。

### 计算方法与剪切闭锁

将FSDT理论付诸于有限元（Finite Element, FE）实现时，会遇到一个著名的数值问题——**剪切闭锁**（shear locking）。

FSDT的运动学场 $(u_0, v_0, w_0, \phi_x, \phi_y)$ 只要求 $C^0$ 连续性，这使得采用简单的 $C^0$ 单元（如四节点四边形单元）进行离散成为可能，这是其相对于需要 $C^1$ 连续性的CLT的一大优势 [@problem_id:2642022]。在典型的单元实现中，所有五个运动学变量都采用相同的插值函数（例如，双线性插值）[@problem_id:2641963]。

问题的根源在于薄板极限情况。当板的厚度 $h \to 0$ 时，其行为应趋近于CLT，即横向剪切应变 $\boldsymbol{\gamma}_s$ 必须趋于零。在离散的有限元模型中，$\boldsymbol{\gamma}_s = \mathbf{0}$ 这一约束条件必须在单元的积分点上得到满足。然而，由于插值函数的不匹配（例如，对 $\phi_x$ 的插值和对 $\partial w_0 / \partial x$ 的插值多项式阶次不同），标准的全积分（fully integrated）单元无法在满足 $\boldsymbol{\gamma}_s=\mathbf{0}$ 的同时还能表示出非零的弯曲变形。为了避免产生巨大的、非物理的剪切应变能（其刚度项与厚度 $h$ 成正比，而弯曲能刚度与 $h^3$ 成正比），单元被迫进入一种几乎无变形的“闭锁”状态，导致计算结果严重偏刚，无法准确捕捉弯曲行为 [@problem_id:2641963]。

为解决剪切闭锁问题，研究者们发展了多种技术，其核心思想是削弱或重新构造离散的剪切应变场，使其能够更好地适应薄板极限下的运动学约束。常用的有效方法包括 [@problem_id:2641963]：

1.  **减缩积分/选择性积分 (Reduced/Selective Integration)**: 对单元刚度矩阵中的剪切能部分采用比弯曲能部分更低阶的积分法则。这相当于在更少的点上施加 $\boldsymbol{\gamma}_s = \mathbf{0}$ 约束，从而“放松”了单元，使其能够更好地表现弯曲。

2.  **假定应变/混合单元法 (Assumed Strain / Mixed Methods)**: 不直接从位移插值中导出剪切应变，而是为剪切应变场构造一个独立的、阶次更低的插值。例如，混合插值张量分量法（MITC）就是一种非常成功的技术。这类方法旨在构造一个能够通过“零剪切应变片检验”（zero-shear patch test）的离散剪切应变场，确保在纯弯曲状态下不会产生寄生的剪切能。

通过这些技术，基于FSDT的 $C^0$ 板单元可以在从厚板到薄板的广泛范围内都表现出良好的精度和收敛性。