## 引言
在结构力学领域，精确预测板壳结构的行为是工程设计的核心。[经典板理论](@entry_id:191723)，即基尔霍夫-勒夫理论，虽然简洁，但其忽略[横向剪切变形](@entry_id:176673)的假设使其仅适用于薄板分析，在面对厚板、夹层结构或剪切刚度较低的[复合材料](@entry_id:139856)时，会产生显著误差。为了弥补这一知识鸿沟，一阶剪切变形板理论（FSDT）应运而生，它通过放宽经典理论的运动学约束，提供了一个既简洁又更为精确的分析模型。本文旨在系统性地阐述[一阶剪切变形理论](@entry_id:198781)。在“原理与机制”一章中，我们将深入探讨其基本假设、[本构关系](@entry_id:186508)和控制方程，并揭示剪切修正与剪切闭锁等核心概念。随后的“应用与交叉学科联系”章节将展示该理论如何在[复合材料](@entry_id:139856)、[结构动力学](@entry_id:172684)、[热力学](@entry_id:141121)和[断裂力学](@entry_id:141480)等领域发挥关键作用。最后，“动手实践”部分将通过具体问题引导读者将理论应用于实际计算。通过这三章的学习，读者将能够全面掌握FSDT的理论精髓及其在现代工程分析中的强大功能。

## 原理与机制

[一阶剪切变形理论](@entry_id:198781)（First-order Shear Deformation Theory, FSDT）通过放宽[经典板理论](@entry_id:191723)中的一个关键约束，为分析厚板和[复合材料](@entry_id:139856)板提供了一个更精确的模型。本章将深入探讨该理论的基本原理和内在机制，从运动学假设出发，推导其应变场、本构关系和控制方程，并阐明其与经典理论的联系及其在数值应用中的一个重要现象。

### 基本[运动学](@entry_id:173318)假设

[经典板理论](@entry_id:191723)，即基尔霍夫-勒夫（Kirchhoff-Love）理论，其核心假设是“法线假设”：初始垂直于板中面的直线元（称为**[法线](@entry_id:167651)**或**导向矢量**）在变形后仍然保持为直线，且垂直于变形后的中面。这一假设直接导致横向剪切应变为零，因此该理论仅适用于薄板。

[一阶剪切变形理论](@entry_id:198781)，亦称**雷斯纳-明德林（Reissner-Mindlin）理论**，其关键创新在于对法线假设的放宽。FSDT保留了法线在变形后仍为直线且不可伸长的假定，但不再要求其必须垂直于变形后的中面 。这一改变允许了[横向剪切变形](@entry_id:176673)的存在，从而使理论能够描述厚板的行为。

基于此假设，板中任意一点 $(x,y,z)$ 的[位移场](@entry_id:141476)可以表示为中面 $(z=0)$ 的位移和转角的函数。设板的中面位移在 $x, y, z$ 方向的分量分别为 $u_0(x,y)$, $v_0(x,y)$, $w_0(x,y)$。设[法线](@entry_id:167651)绕 $y$ 轴的转角为 $\theta_x(x,y)$，绕 $-x$ 轴的转角为 $\theta_y(x,y)$。[位移场](@entry_id:141476)可表达为：
$$
u(x,y,z) = u_0(x,y) + z \theta_x(x,y)
$$
$$
v(x,y,z) = v_0(x,y) + z \theta_y(x,y)
$$
$$
w(x,y,z) = w_0(x,y)
$$
此运动学模型由五个独立的场变量描述：三个中面位移 $(u_0, v_0, w_0)$ 和两个独立的转角 $(\theta_x, \theta_y)$ 。其中，$w$ 不依赖于 $z$ 坐标的假设体现了法线的不可伸长性，即厚度方向的[正应变](@entry_id:204633) $\epsilon_{zz} = \frac{\partial w}{\partial z} = 0$ 。

### 广义应变及其物理诠释

基于上述位移场和线性[应变-位移关系](@entry_id:173321)，我们可以推导出板的应变[分布](@entry_id:182848)。

板的**面内应变** $(\epsilon_{xx}, \epsilon_{yy}, \gamma_{xy})$ 随厚度坐标 $z$ 线性变化，可以分解为两部分：中面应变和曲率。
$$
\boldsymbol{\epsilon}(z) = \begin{pmatrix} \epsilon_{xx} \\ \epsilon_{yy} \\ \gamma_{xy} \end{pmatrix} = \begin{pmatrix} \frac{\partial u_0}{\partial x} \\ \frac{\partial v_0}{\partial y} \\ \frac{\partial u_0}{\partial y} + \frac{\partial v_0}{\partial x} \end{pmatrix} + z \begin{pmatrix} \frac{\partial \theta_x}{\partial x} \\ \frac{\partial \theta_y}{\partial y} \\ \frac{\partial \theta_x}{\partial y} + \frac{\partial \theta_y}{\partial x} \end{pmatrix} = \boldsymbol{\epsilon}_0 + z \boldsymbol{\kappa}
$$
这里，$\boldsymbol{\epsilon}_0$ 是**中面应变矢量**，代表中面的拉伸和剪切；$\boldsymbol{\kappa}$ 是**曲率矢量**，代表板的弯曲和扭转。

**横向剪切应变** $(\gamma_{xz}, \gamma_{yz})$ 是FSDT理论的核心。根据工程应变的定义：
$$
\gamma_{xz} = \frac{\partial u}{\partial z} + \frac{\partial w}{\partial x} = \theta_x + \frac{\partial w_0}{\partial x}
$$
$$
\gamma_{yz} = \frac{\partial v}{\partial z} + \frac{\partial w}{\partial y} = \theta_y + \frac{\partial w_0}{\partial y}
$$
一个至关重要的结论是：根据FSDT的[运动学](@entry_id:173318)假设，横向剪切应变 $\gamma_{xz}$ 和 $\gamma_{yz}$ 不依赖于厚度坐标 $z$，即在整个板厚度上为**常数** 。

从物理上看，横向剪切应变代表了法线转角与中面坡度之间的不匹配 。在经典理论中，法线始终垂直于中面，意味着[法线](@entry_id:167651)转角必须等于中面坡度的相反数，即 $\theta_x = -\frac{\partial w_0}{\partial x}$ 和 $\theta_y = -\frac{\partial w_0}{\partial y}$。在这种情况下，$\gamma_{xz}$ 和 $\gamma_{yz}$ 恒为零。FSDT通过将 $\theta_x$ 和 $\theta_y$ 作为独立于 $w_0$ 的变量，允许了这种不匹配，从而引入了非零的[横向剪切变形](@entry_id:176673)。

### FSDT运动学局限性与剪切修正

尽管FSDT成功引入了横向剪切效应，但其“横向剪切应变沿厚度为常数”的预测存在一个根本性的物理缺陷。对于一个顶部和底部表面 $(z = \pm h/2)$ 不受切向力作用的板，其横向[剪切应力](@entry_id:137139) $\tau_{xz}$ 和 $\tau_{yz}$ 在这些表面上必须为零。根据[胡克定律](@entry_id:149682) $(\tau = G\gamma)$，这意味着横向剪切应变在顶面和底面也应为零 。

FSDT的[运动学](@entry_id:173318)假设无法满足这一**[自由表面边界条件](@entry_id:749579)**。如果强制在 $z = \pm h/2$ 处剪切应变为零，由于应变沿厚度是常数，那么整个厚度上的剪切应变都将为零。这将导致横向剪切合力 $Q_x$ 和 $Q_y$ 为零，进而与板在横向载荷作用下的[平衡方程](@entry_id:172166) $(\frac{\partial Q_x}{\partial x} + \frac{\partial Q_y}{\partial y} + p = 0)$ 相矛盾 。

为了弥补这一理论上的不自洽，同时保留模型的简洁性，FSDT引入了一个**[剪切修正因子](@entry_id:164451)**（shear correction factor），通常记为 $\kappa$（或 $k_s$）。这个因子的作用不是改变[运动学](@entry_id:173318)假设，而是修正[本构关系](@entry_id:186508)，使得在理论框架内计算的剪切应变能，等于根据更真实的、沿厚度非[均匀分布](@entry_id:194597)（通常接近抛物线形）的[剪切应力](@entry_id:137139)场计算出的应变能。简言之，它是一个能量等效的“修正”系数 。

[剪切修正因子](@entry_id:164451) $\kappa$ 的推导可以通过以下能量等效原理完成：
$$
U_{s}^{\text{FSDT}} = U_{s}^{\text{3D}}
$$
FSDT中的剪切应变能（单位面积）为 $\frac{1}{2} Q_x \gamma_{xz}^0$，其中 $Q_x = \kappa G h \gamma_{xz}^0$。因此 $U_{s}^{\text{FSDT}} = \frac{Q_x^2}{2\kappa G h}$。
三维[弹性理论](@entry_id:184142)给出的剪切[应变能](@entry_id:162699)为 $U_{s}^{\text{3D}} = \int_{-h/2}^{h/2} \frac{\tau_{xz}(z)^2}{2G} dz$。
令二者相等，可解得：
$$
\kappa = \frac{Q_x^2}{h \int_{-h/2}^{h/2} \tau_{xz}(z)^2 dz}
$$
对于均质矩形[截面](@entry_id:154995)，其[剪切应力](@entry_id:137139)近似为抛物线[分布](@entry_id:182848)，代入上式可计算出典型的修正因子值为 $\kappa = 5/6$ 。

更高阶的剪切变形理论通过在位移场中引入关于 $z$ 的更高次项来解决此问题，使得剪切应变可以沿厚度变化（例如，呈抛物线[分布](@entry_id:182848)），从而直接满足[自由表面边界条件](@entry_id:749579)，无需引入修正因子 。

### [应力合力](@entry_id:180269)与[本构关系](@entry_id:186508)

为了将三维问题[降维](@entry_id:142982)到二维，我们通过对整个厚度积分来定义**[应力合力](@entry_id:180269)**。它们是单位长度上的力和力矩。

- **薄膜力** (Membrane forces): $N_{xx}, N_{yy}, N_{xy}$
- **[弯矩](@entry_id:202968)和扭矩** (Bending and twisting moments): $M_{xx}, M_{yy}, M_{xy}$
- **横向[剪力](@entry_id:172634)** (Transverse shear forces): $Q_x, Q_y$

这些合力由三维应力分量沿厚度 $z \in [-h/2, h/2]$ 积分得到 ：
$$
\begin{pmatrix} N_{xx} \\ N_{yy} \\ N_{xy} \end{pmatrix} = \int_{-h/2}^{h/2} \begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \sigma_{xy} \end{pmatrix} dz, \quad
\begin{pmatrix} M_{xx} \\ M_{yy} \\ M_{xy} \end{pmatrix} = \int_{-h/2}^{h/2} z \begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \sigma_{xy} \end{pmatrix} dz
$$
$$
\begin{pmatrix} Q_x \\ Q_y \end{pmatrix} = \int_{-h/2}^{h/2} \begin{pmatrix} \tau_{xz} \\ \tau_{yz} \end{pmatrix} dz
$$
将三维材料[本构关系](@entry_id:186508) $(\boldsymbol{\sigma} = \mathbf{C} \boldsymbol{\epsilon})$ 代入应变表达式 $\boldsymbol{\epsilon}(z) = \boldsymbol{\epsilon}_0 + z \boldsymbol{\kappa}$，然后积分，即可得到板的二维[本构方程](@entry_id:138559)。

对于**层合板**，这一关系通常写成矩阵形式 ：
$$
\begin{bmatrix} \mathbf{N} \\ \mathbf{M} \end{bmatrix} = \begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B} & \mathbf{D} \end{bmatrix} \begin{bmatrix} \boldsymbol{\epsilon}_0 \\ \boldsymbol{\kappa} \end{bmatrix}, \quad \mathbf{Q} = \mathbf{A}_s \boldsymbol{\gamma}_0
$$
其中 $\mathbf{N}, \mathbf{M}, \boldsymbol{\epsilon}_0, \boldsymbol{\kappa}$ 均为三维列向量，$\mathbf{Q}, \boldsymbol{\gamma}_0$ 为二维列向量。矩阵 $\mathbf{A}, \mathbf{B}, \mathbf{D}$ 分别是 $3 \times 3$ 的**[拉伸刚度](@entry_id:193973)矩阵**、**耦合刚度矩阵**和**弯曲刚度矩阵**，它们通过对各单层板的[刚度矩阵](@entry_id:178659) $\bar{\mathbf{Q}}^{(k)}$ 沿厚度积分得到：
$$
(\mathbf{A}, \mathbf{B}, \mathbf{D}) = \sum_{k=1}^{n} \int_{z_{k-1}}^{z_k} (1, z, z^2) \bar{\mathbf{Q}}^{(k)} dz
$$
$\mathbf{A}_s$ 是 $2 \times 2$ 的**横向剪切[刚度矩阵](@entry_id:178659)**，它包括了对[剪切修正因子](@entry_id:164451)的考虑。对于非对称铺层的层合板，$\mathbf{B}$ 矩阵非零，体现了拉伸与弯曲之间的耦合效应。对于均质各向同性板，该方程简化，$\mathbf{B} = \mathbf{0}$，拉伸和弯曲解耦。

### 控制平衡方程

板的控制方程由[静力平衡](@entry_id:163498)原理导出。考虑一个微元体，其[力平衡](@entry_id:267186)和[力矩平衡](@entry_id:752138)条件给出如下微分方程组：
1.  面内[力平衡](@entry_id:267186)：
    $$
    \frac{\partial N_{xx}}{\partial x} + \frac{\partial N_{xy}}{\partial y} = 0
    $$
    $$
    \frac{\partial N_{xy}}{\partial x} + \frac{\partial N_{yy}}{\partial y} = 0
    $$
2.  横向[力平衡](@entry_id:267186)：
    $$
    \frac{\partial Q_x}{\partial x} + \frac{\partial Q_y}{\partial y} + p = 0
    $$
3.  [力矩平衡](@entry_id:752138)：
    $$
    \frac{\partial M_{xx}}{\partial x} + \frac{\partial M_{xy}}{\partial y} - Q_x = 0
    $$
    $$
    \frac{\partial M_{xy}}{\partial x} + \frac{\partial M_{yy}}{\partial y} - Q_y = 0
    $$
将前面推导的[本构关系](@entry_id:186508)和广义[应变-位移关系](@entry_id:173321)代入这些平衡方程，即可得到一组关于五个基本[运动学](@entry_id:173318)变量 $(u_0, v_0, w_0, \theta_x, \theta_y)$ 的[偏微分方程组](@entry_id:172573)。对于均质各向同性板，这五个方程可以写成一个 $5 \times 5$ 的[矩阵算子](@entry_id:269557)形式 $\mathcal{L}\mathbf{u} = \mathbf{f}$ 。该算子矩阵 $\mathcal{L}$ 的分块结构清晰地显示了面内问题（由 $u_0, v_0$ 控制）与弯曲-剪切问题（由 $w_0, \theta_x, \theta_y$ 控制）的解耦。

### 与[经典板理论](@entry_id:191723)的关系及剪切闭锁现象

FSDT 与[经典板理论](@entry_id:191723)（CPT）之间存在深刻的联系。当横向剪切应变 $\boldsymbol{\gamma} = \boldsymbol{0}$ 时，FSDT的运动学约束 $\theta_x = -\frac{\partial w_0}{\partial x}$ 和 $\theta_y = -\frac{\partial w_0}{\partial y}$ 被精确满足，理论退化为CPT 。这种情况在以下几种条件下发生：

1.  **物理上**，对于处于[纯弯曲](@entry_id:202969)状态的板，其横向剪力处处为零，这直接导致剪切应变为零 。
2.  **数学上**，可以将CPT视为FSDT在横向剪切刚度趋于无穷大 $(kGh \to \infty)$ 时的极限情况。在这种极限下，为了保持有限的应变能，剪切应变必须趋于零 。
3.  **渐近地**，对于薄板 $(h/L \to 0)$，FSDT的解会收敛于CPT的解。

这种关系在有限元分析中会引发一个著名的数值问题——**剪切闭锁**（shear locking）。当使用低阶有限元（例如，对 $w_0$ 和 $\theta_x, \theta_y$ 使用相同的线性或[双线性插值](@entry_id:170280)函数）求解薄板问题时，会出现该现象 。

剪切闭锁的根源在于离散空间的失配。随着板厚 $h$ 趋于零，剪切能项在总[势能](@entry_id:748988)中的权重以 $O(h^{-2})$ 的速度增长，迫使数值解必须严格满足零剪切应变条件 $\boldsymbol{\gamma}_h = \boldsymbol{\theta}_h + \nabla w_h \approx \boldsymbol{0}$。然而，对于标准的 $C^0$ 连续单元，插值后的转角场 $\boldsymbol{\theta}_h$ 是跨单元连续的，而位移的[梯度场](@entry_id:264143) $\nabla w_h$ 却是跨单元不连续的。这两个[函数空间](@entry_id:143478)无法在一般弯曲模式下精确匹配以满足零剪切条件。结果是，为了最小化巨大的剪切能惩罚，有限元解会抑制本应发生的弯曲变形，表现出远超实际的刚度，即“闭锁” 。

从[混合有限元](@entry_id:178533)的角度看，这相当于所选的[插值函数](@entry_id:262791)空间对 $(\boldsymbol{V}_\theta^h, V_w^h)$ 违反了LBB（Ladyzhenskaya–Babuška–Brezzi）稳定性条件，导致了数值方案的不稳定。解决剪切闭锁的方法包括使用[选择性减缩积分](@entry_id:168281)、假设应变法（如[MITC单元](@entry_id:752016)）或使用不满足[LBB条件](@entry_id:746626)的混合插值单元等，这些技术旨在放松或重新协调离散的剪切约束。