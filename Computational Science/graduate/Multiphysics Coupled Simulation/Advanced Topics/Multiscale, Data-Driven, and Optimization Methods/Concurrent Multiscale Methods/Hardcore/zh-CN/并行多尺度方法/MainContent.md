## 引言
现代工程与科学领域对[材料性能](@entry_id:146723)的预测精度要求日益严苛，尤其对于具有复杂微观结构（如[复合材料](@entry_id:139856)、多晶金属、生物组织）的[非均质材料](@entry_id:196262)。传统的宏观唯象[本构模型](@entry_id:174726)往往难以准确捕捉微观结构细节对其整体行为的决定性影响，这构成了一个显著的知识鸿沟。并发多尺度方法，特别是基于[计算均匀化](@entry_id:163942)的[FE²方法](@entry_id:194603)，应运而生，它通过在不同尺度间进行直接的数值模拟，为建立从微观机理到宏观响应的物理桥梁提供了一条革命性的途径。

本文旨在系统性地介绍并发多尺度方法的核心思想与前沿应用。在“原理与机制”一章中，我们将深入探讨[尺度分离](@entry_id:270204)假设、[计算均匀化](@entry_id:163942)理论以及代表性体积单元（RVE）等基本概念，揭示该方法的力学基础。随后，“应用与跨学科连接”一章将通过一系列覆盖[材料力学](@entry_id:201885)、地球科学及[生物力学](@entry_id:153973)等领域的实例，展示该方法在解决复杂[多物理场耦合](@entry_id:171389)问题中的强大能力。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识转化为实践技能。通过本次学习，读者将能够全面理解并发多尺度方法的工作原理，并掌握如何运用它来分析和预测具有复杂内部结构的材料和系统的力学行为。

## 原理与机制

并发多尺度方法的核心在于，它并非采用简化的解析模型来描述材料的微观行为，而是通过在宏观问题的每个求解点上直接进行微观结构的数值模拟，来实时“计算”出材料的等效本构响应。这种“有限元中的有限元”(Finite Element squared, FE²)思想，赋予了我们前所未有的能力来预测具有复杂微观结构的材料和系统的行为。本章将深入探讨支撑这一强大框架的核心科学原理与关键力学机制。

### 核心思想：[尺度分离](@entry_id:270204)与[计算均匀化](@entry_id:163942)

并发多尺度方法得以成立的基石是**尺度分离假设 (scale separation assumption)**。该假设认为，材料的微观非[均匀性](@entry_id:152612)（例如晶粒、纤维、孔隙的尺寸和间距）具有一个[特征长度](@entry_id:265857) $\ell_{\mathrm{micro}}$，而我们关心的宏观结构或工程部件的特征尺寸为 $L_{\mathrm{macro}}$，且两者之间存在显著的尺度差异，即 $\ell_{\mathrm{micro}} \ll L_{\mathrm{macro}}$。

为了更精确地描述这一概念，我们可以引入一个无量纲小参数 $\epsilon = \ell_{\mathrm{micro}} / L_{\mathrm{macro}}$，其中 $0  \epsilon \ll 1$。在渐近均匀化理论中，这对应于引入两种[坐标系](@entry_id:156346)：一个是在宏观尺度上变化的“慢”坐标 $\boldsymbol{x}$，另一个是在微观尺度上快速变化的“快”坐标 $\boldsymbol{y} = \boldsymbol{x} / \epsilon$。任何物理场量，如位移 $\boldsymbol{u}$，都被假定为同时依赖于这两个坐标，即 $\boldsymbol{u}(\boldsymbol{x}, \boldsymbol{y})$。

[FE²方法](@entry_id:194603)巧妙地将这一理论思想转化为一种可計算的框架。它在宏观有限元模型的每个积分点（[高斯点](@entry_id:170251)）上，求解一个定义在**代表性体积单元 (Representative Volume Element, RVE)** 上的微观[边值问题](@entry_id:193901)。RVE的尺寸 $L_{\mathrm{RVE}}$ 必须满足一个双重约束：它需要足够大以包含足够多的微观结构信息，从而在统计意义上“代表”材料的局部特性 ($L_{\mathrm{RVE}} \gg \ell_{\mathrm{micro}}$)；同时，它又必须相对于宏观梯度变化的尺度足够小 ($L_{\mathrm{RVE}} \ll L_{\mathrm{macro}}$)。

$L_{\mathrm{RVE}} \ll L_{\mathrm{macro}}$ 这一条件至关重要。考虑宏观应变场 $\boldsymbol{E}(\boldsymbol{x})$ 在某宏观点 $\boldsymbol{x}_0$ 附近的[泰勒展开](@entry_id:145057)：
$$ \boldsymbol{E}(\boldsymbol{x}) = \boldsymbol{E}(\boldsymbol{x}_0) + (\boldsymbol{x} - \boldsymbol{x}_0) \cdot \nabla\boldsymbol{E}(\boldsymbol{x}_0) + \dots $$
对于位于以 $\boldsymbol{x}_0$ 为中心的RVE内部的任何一点 $\boldsymbol{x}$，距离 $\|\boldsymbol{x} - \boldsymbol{x}_0\|$ 的量级为 $L_{\mathrm{RVE}}$。而宏观[应变梯度](@entry_id:204192) $\nabla\boldsymbol{E}$ 的变化尺度为 $1/L_{\mathrm{macro}}$。因此，$\boldsymbol{E}$ 在整个RVE上的变化量级的阶为 $L_{\mathrm{RVE}}/L_{\mathrm{macro}}$，这恰好是小参数 $\epsilon$ 的量级。既然这是一个小量，一阶均匀化理论便作出了核心简化：忽略宏观应变在RVE内的空间变化，认为整个RVE受到一个均匀的宏观应变 $\boldsymbol{E}(\boldsymbol{x}_0)$ 的驱动。这正是[FE²方法](@entry_id:194603)中将宏观积分点的[应变张量](@entry_id:193332)作为微观RVE问题的边界驱动条件的理论依据 。

然而，也正是因为这种[一阶近似](@entry_id:147559)忽略了与 $\nabla\boldsymbol{E}$ 相关的高阶项，标准的[FE²方法](@entry_id:194603)无法捕捉那些由应变梯度引起的内在**[尺度效应](@entry_id:153734) (size effects)**。例如，在微尺度弯曲或扭转问题中，材料的响应可能依赖于结构的绝对尺寸。要捕捉这类现象，就需要超越一阶均匀化，例如发展二阶[计算均匀化](@entry_id:163942)方法，或者在宏观模型中引入[应变梯度理论](@entry_id:180517)，这些方法本质上保留了展开式中与 $\epsilon$ 相关的高阶项 。

### 能量一致性：[Hill-Mandel条件](@entry_id:163076)与容许边界条件

将微观行为与宏观响应联系起来，必须遵循基本的物理[守恒定律](@entry_id:269268)，其中最核心的是[能量守恒](@entry_id:140514)。**Hill-Mandel宏观[均匀性](@entry_id:152612)条件 (Hill-Mandel macro-homogeneity condition)** 提供了连接两个尺度的能量桥梁。它要求在任意虚拟变形过程中，宏观应力与宏观[应变率](@entry_id:154778)所做的功（[功率密度](@entry_id:194407)）必须等于微观应力与微观应变率所做功在RVE上的体积平均值。

在小应变设定下，令 $\boldsymbol{\Sigma}$ 和 $\boldsymbol{E}$ 分别为宏观应力和应变，$\boldsymbol{\sigma}$ 和 $\boldsymbol{\varepsilon}$ 为微观应力和应变，该条件可写为：
$$ \boldsymbol{\Sigma} : \dot{\boldsymbol{E}} = \langle \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} \rangle = \frac{1}{|\Omega_{\mu}|} \int_{\Omega_{\mu}} \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}\,\mathrm{d}\Omega $$
其中 $\langle \cdot \rangle$ 表示在微观RVE域 $\Omega_{\mu}$ 上的体积平均。这个条件保证了从微观到宏观的能量转化是自洽的，不会凭空产生或消失能量。

为了确保[Hill-Mandel条件](@entry_id:163076)成立，RVE的边界条件必须精心设计。我们可以证明，该条件等价于要求应力涨落和[应变率](@entry_id:154778)涨落在RVE边界上所做的功为零。具体来说，如果我们将微观位移分解为一个宏观均匀部分和一个涨落部分 $\boldsymbol{u}(\boldsymbol{x}) = \boldsymbol{E}\boldsymbol{x} + \tilde{\boldsymbol{u}}(\boldsymbol{x})$，[Hill-Mandel条件](@entry_id:163076)最终归结为边界积分 $\int_{\partial \Omega_{\mu}} \dot{\tilde{\boldsymbol{u}}} \cdot \boldsymbol{t} \, \mathrm{d}S = 0$ 必须成立，其中 $\boldsymbol{t}$ 是边界上的traction 。

满足这一要求的边界条件被称为**容许边界条件 (admissible boundary conditions)**。主要有三类：

1.  **运动学均匀边界条件 (Kinematic Uniform Boundary Conditions, KUBC)**：也称为狄利克雷(Dirichlet)型边界条件。在RVE的整个边界 $\partial\Omega_{\mu}$ 上施加线性的[位移场](@entry_id:141476)：$\boldsymbol{u}(\boldsymbol{x}) = \boldsymbol{E}\boldsymbol{x}$。在这种情况下，边界上的位移涨落 $\tilde{\boldsymbol{u}}$ 恒为零，因此边界积分自然为零。

2.  **静力学均匀边界条件 (Static Uniform Boundary Conditions, SUBC)**：也称为诺伊曼(Neumann)型边界条件。在RVE的整个边界上施加与均匀宏观应[力场](@entry_id:147325) $\boldsymbol{\Sigma}$ 相平衡的面力：$\boldsymbol{t}(\boldsymbol{x}) = \boldsymbol{\Sigma}\boldsymbol{n}$。这种条件下，可以证明应变涨落的体积平均为零，进而使得[能量条件](@entry_id:158507)满足。

3.  **[周期性边界条件](@entry_id:147809) (Periodic Boundary Conditions, PBC)**：要求RVE相对的面上的位移涨落 $\tilde{\boldsymbol{u}}$ 相等，而面力 $\boldsymbol{t}$ 则相反（反周期）。这种“头尾相接”的约束方式也能使边界[功积分](@entry_id:181218)为零。

这三种边界条件都确保了能量的一致性，是[FE²方法](@entry_id:194603)中应用最广泛的选择 。

### [代表性](@entry_id:204613)体积单元：理论与实践

RVE的选择和边界条件的施加，在理论和实践层面都具有深刻的 implications。

#### 周期性单元胞 vs. 统计性RVE

微观域的选择主要取决于微观结构的 nature。
*   对于具有严格周期性[排列](@entry_id:136432)的微观结构，例如[复合材料](@entry_id:139856)中的纤维规则[排列](@entry_id:136432)或完美晶体，最 natural 的选择是**周期性单元胞 (Periodic Unit Cell, PUC)**。PUC是能够通过平移操作重构整个微观结构的最小几何单元。结合[周期性边界条件(PBC)](@entry_id:753346)，PUC能够精确地代表无限周期性介质的行为，且其尺寸可以非常小，大大节省了计算成本 。
*   对于随机或[非周期性](@entry_id:275873)的微观结构，例如多晶金属、泡沫材料或具有随机[分布](@entry_id:182848)夹杂物的[复合材料](@entry_id:139856)，我们必须使用**统计性[代表性](@entry_id:204613)体积单元 (Statistical RVE)**。一个RVE要成为“统计性代表”，其尺寸 $L$ 必须远大于材料非[均匀性](@entry_id:152612)的相关长度 $\ell_c$ ($L \gg \ell_c$)。只有这样，RVE的计算结果（如等效模量）才能摆脱具体微观结构 realization 和边界条件选择的影响，收敛到一个稳定的、代表材料宏观属性的数值 。

#### 有限尺寸RVE的[边界层](@entry_id:139416)效应与偏差

在实践中，由于计算成本的限制，我们无法使用无限大的RVE。对于有限尺寸的RVE，人为施加的边界条件会在RVE边界附近产生一个非物理的**[边界层](@entry_id:139416) (boundary layer)**，其厚度与微观特征尺寸 $\ell$ 同量级。这个[边界层](@entry_id:139416)的存在会使计算出的等效属性产生偏差。

基于变分原理，我们可以 elegant 地理解这种偏差的方向：
*   **KUBC** (Dirichlet BCs) 对边界位移施加了过强的约束，抑制了RVE边界处的自然变形。根据[最小势能原理](@entry_id:173340)，更强的约束会导致更高的系统能量，从而使得计算出的等效刚度 $\mathbb{C}^{\mathrm{eff}}_{\mathrm{K}}$ 偏高。它构成了真实等效刚度的一个**上界**。
*   **SUBC** (Neumann BCs) 对边界traction的约束相对宽松，允许RVE产生一些非物理的“软”变形模式。根据[最小余能原理](@entry_id:200382)，这会导致计算出的等效刚度 $\mathbb{C}^{\mathrm{eff}}_{\mathrm{S}}$ 偏低，构成了真实值的**下界**。
*   **PBC** 通常被认为能在RVE尺寸较小时更快地收敛到真实值，其结果介于KUBC和SUBC之间：$\mathbb{C}^{\mathrm{eff}}_{\mathrm{S}} \preceq \mathbb{C}^{\mathrm{eff}}_{\mathrm{PBC}} \preceq \mathbb{C}^{\mathrm{eff}}_{\mathrm{K}}$ 。

这种偏差的大小与[边界层](@entry_id:139416)体积占RVE总体积的比例有关。由于[边界层](@entry_id:139416)体积正比于 $L^{d-1}\ell$（d为维度），RVE体积正比于 $L^d$，因此偏差的量级为 $O(\ell/L)$。这意味着，RVE越大，边界效应的影响越小，不同边界条件得到的结果也越接近  。

为了在有限的计算资源下减小这种偏差，研究者们提出了一些修正策略：
1.  **[混合边界条件](@entry_id:176456) (Mixed Boundary Conditions)**：在RVE边界的大部分区域施加较为宽松的 traction 条件 (SUBC)，仅在少数几个点上施加位移约束以消除刚体位移。这种方法可以获得接近SUBC下界的“软”响应，但偏差依然存在 。
2.  **[过采样](@entry_id:270705) (Oversampling)**：在一个较大的RVE上施加KUBC，但在进行体积平均以计算宏观应力时，只使用远离边界的内部核心区域。这样，核心区域受[边界层](@entry_id:139416)的影响较小，得到的结果更准确。这本质上是用更大的计算量换取更高的精度 。

### 推导宏观[本构关系](@entry_id:186508)：一种变分方法

[计算均匀化](@entry_id:163942)的过程，本质上是一个能量最小化问题。我们可以通过一个简单的例子来阐明其核心思想。

考虑一个一维[复合材料](@entry_id:139856)杆，由两种不同线弹性材料构成，其刚度分别为 $k_1$ 和 $k_2$，[体积分数](@entry_id:756566)分别为 $f_1$ 和 $f_2$。RVE的长度为 $L$。当施加宏观应变 $E$ 时，微观位移场可以写为 $u(x) = E x + w(x)$，其中 $w(x)$ 是位移涨落。微观应变为 $\varepsilon(x) = u'(x) = E + w'(x)$。

系统的宏观[应变能密度](@entry_id:200085) $\Psi(E)$ 定义为微观[应变能密度](@entry_id:200085)的体积平均。根据[最小势能原理](@entry_id:173340)，真实的位移涨落场 $w(x)$ 应该使 $\Psi(E)$ 最小化：
$$ \Psi(E) = \min_{w(x)} \frac{1}{L} \int_{0}^{L} \frac{1}{2} k(x) \left(E + w'(x)\right)^{2} \,\mathrm{d}x $$
其中 $k(x)$ 是随位置变化的刚度。我们对施加[周期性边界条件](@entry_id:147809)下的 $w(x)$ 求解此[变分问题](@entry_id:756445)。其stationarity condition ([欧拉-拉格朗日方程](@entry_id:137827)的弱形式) 要求：
$$ \int_{0}^{L} \sigma(x) \delta w'(x) \,\mathrm{d}x = 0 $$
对于所有满足约束的[虚位移](@entry_id:168781)涨落 $\delta w(x)$。这里的微观应力为 $\sigma(x) = k(x)(E+w'(x))$。这个弱形式的解表明，微观应[力场](@entry_id:147325) $\sigma(x)$ 在整个RVE上必须是一个常数，即 **iso-stress ([等应力](@entry_id:204402))** 条件。

利用[等应力](@entry_id:204402)条件 $\sigma(x)=\sigma_0$ 和应变涨落的平均值为零的约束 $\langle w'(x) \rangle = 0$，我们可以反解出 $\sigma_0$ 与宏观应变 $E$ 的关系，并最终推导出宏观应力 $\Sigma = \langle \sigma \rangle = \sigma_0$。这个过程给出的等效刚度 $K_{\mathrm{eff}}$ 为：
$$ K_{\mathrm{eff}} = \frac{1}{\frac{f_1}{k_1} + \frac{f_2}{k_2}} = \frac{k_1 k_2}{f_1 k_2 + f_2 k_1} $$
这正是[材料力学](@entry_id:201885)中[串联](@entry_id:141009)弹簧的等效刚度，即著名的**Reuss下界** 。

与此相对，如果我们直接假设一个iso-strain ([等应变](@entry_id:184570)) 条件，即假设微观应变处处等于宏观应变 $\varepsilon(x)=E$ (这对应于KUBC的 trial field)，那么宏观应力 $\Sigma = \langle \sigma \rangle = \langle k(x) \varepsilon(x) \rangle = \langle k(x) E \rangle = (f_1 k_1 + f_2 k_2) E$。此时的等效刚度为：
$$ K_{\mathrm{eff}} = f_1 k_1 + f_2 k_2 $$
这对应于并联弹簧的刚度，即**Voigt上界**。这个结果可以通过在[最小势能原理](@entry_id:173340)中选择一个简单的 trial field $\boldsymbol{u}_{\text{trial}}(\boldsymbol{x}) = \boldsymbol{E}\boldsymbol{x}$ 来直接获得，它为真实的等效能量提供了一个[上界](@entry_id:274738)，从而为等效刚度提供了[上界](@entry_id:274738) 。这两个经典界限清晰地展示了不同的[运动学](@entry_id:173318)假设是如何导致不同的均匀化结果的。

### 并发多尺度建模中的进阶主题

#### 对非弹性材料的扩展

当微观材料行为是[弹塑性](@entry_id:193198)、[粘塑性](@entry_id:165397)或存在損傷時，其响应不僅取決於當前的應變，還依賴於加載歷史。這種歷史依賴性通常通过一组**内禀变量 (internal variables)** $\boldsymbol{\alpha}(\mathbf{x}, t)$ 来描述。此时，均匀化过程不仅需要计算宏观应力，还需要定义和演化宏观層面的内禀变量 $\bar{\boldsymbol{\alpha}}(t)$。

一个自然且广泛采用的选择是，将宏观内禀变量定义为微观内禀变量的体积平均：
$$ \bar{\boldsymbol{\alpha}}(t) = \langle \boldsymbol{\alpha}(\mathbf{x}, t) \rangle_V $$
这个选择的合理性可以从[热力学一致性](@entry_id:138886)的角度来理解。我们需要确保宏观模型的耗散与微观模型的平均耗散相符，即**耗散一致性 (dissipation consistency)** $\bar{D}(t) = \langle D(\mathbf{x}, t) \rangle_V$。可以证明，只要宏观自由能 $\bar{\Psi}$ 定义为微观自由能 $\psi$ 的平均，并且[Hill-Mandel条件](@entry_id:163076)成立，这个耗散[一致性关系](@entry_id:157858)就会自动满足。因此，选择 $\bar{\boldsymbol{\alpha}} = \langle \boldsymbol{\alpha} \rangle$ 是一种简单且[热力学一致的](@entry_id:755906)[一阶近似](@entry_id:147559)，它旨在将宏观[热力学](@entry_id:141121)框架构建为微观框架的直接平均 。

#### 均匀化[切线](@entry_id:268870)模量及其对称性

在[非线性](@entry_id:637147)问题中，宏观有限元求解器（通常是[Newton-Raphson法](@entry_id:140620)）的效率严重依赖于**一致性[切线](@entry_id:268870)模量 (consistent tangent modulus)** $\mathbb{C}^{\mathrm{hom}} = \frac{\partial \boldsymbol{\Sigma}}{\partial \boldsymbol{E}}$。这个[四阶张量](@entry_id:181350)描述了宏观应力如何随宏观应变的微小变化而变化。

一个关键的理论与实践问题是 $\mathbb{C}^{\mathrm{hom}}$ 的对称性。如果 $\mathbb{C}^{\mathrm{hom}}$ 具有主对称性 ($C_{ijkl} = C_{klij}$)，宏观刚度矩阵将是对称的，从而可以使用更高效的[对称矩阵](@entry_id:143130)求解器。$\mathbb{C}^{\mathrm{hom}}$ 是否对称，取决于是否存在一个宏观[应变能势](@entry_id:755493)函数 $W^{\mathrm{hom}}(\boldsymbol{E})$，使得 $\boldsymbol{\Sigma} = \frac{\partial W^{\mathrm{hom}}}{\partial \boldsymbol{E}}$。若存在，则 $\mathbb{C}^{\mathrm{hom}}$作为势函数的[二阶导数](@entry_id:144508)（Hessian矩阵）必然是对称的。

宏观[势函数](@entry_id:176105)的存在性，又取决于微观RVE[边值问题](@entry_id:193901)是否是**保守的 (conservative)**。
*   **对称性得以保证的情况**：如果微观材料是[超弹性](@entry_id:159356)的（即存在[应变能函数](@entry_id:178435)$\psi$），并且施加的边界条件和外力都是保守的（如KUBC, SUBC, PBC），那么即使存在[几何非线性](@entry_id:169896)（大变形），整个微观系统仍然是保守的。此时，可以定义宏观[势函数](@entry_id:176105) $W^{\mathrm{hom}}$，得到的 $\mathbb C^{\mathrm{hom}}$ 具有主对称性。
*   **对称性被破坏的情况**：当微观系统变为非保守时，$\mathbb{C}^{\mathrm{hom}}$ 通常会失去对称性。非保守性的来源包括：
    1.  **材料耗散**：例如，非关联[塑性流动法则](@entry_id:189597)或[库仑摩擦](@entry_id:169196)等，这些模型的本构关系无法从一个[势函数](@entry_id:176105)导出。
    2.  **[非保守力](@entry_id:163431)**：例如，随变形转动的“追随力”（follower forces）或速度相关的[阻尼力](@entry_id:265706)。

理解[切线](@entry_id:268870)模量的对称性来源，对于正确和高效地实现并发[多尺度模拟](@entry_id:752335)至关重要 。

#### FE²格式的数值收敛性

[FE²方法](@entry_id:194603)本质上是一个嵌套的[非线性](@entry_id:637147)求解过程。宏观[Newton-Raphson](@entry_id:177436)迭代的收敛性能，尤其是能否达到理想的**二次收敛 (quadratic convergence)**，对计算总效率有决定性影响。

要实现二次收敛，必须满足经典Newton法的所有条件，并将其 carefully 移植到FE²框架中：
1.  **使用一致性[切线](@entry_id:268870)模量**：宏观刚度矩阵必须是宏观[残差向量](@entry_id:165091)的精确Jacobian矩阵。这意味着在每个积分点使用的 $\mathbb{C}^{\mathrm{hom}}$ 必须是 $\boldsymbol{\Sigma}$ 对 $\boldsymbol{E}$ 的精确导数。任何近似，如使用[割线模量](@entry_id:199454)或不精确的有限差分，都会将算法降级为拟Newton法，其[收敛率](@entry_id:146534)最多为超线性。
2.  **控制微观求解精度**：在宏观Newton迭代的第 $k$ 步，RVE求解器计算出的宏观应力 $\boldsymbol{\Sigma}_k$ 实际上是有误差的。这使得宏观Newton法成为一种**非精确Newton法 (Inexact Newton method)**。理论和实践都表明，要保持二次收敛，微观求解的精度必须与宏观残差的减小相匹配。具体而言，微观求解的残差或误差必须与宏观[残差范数](@entry_id:754273) $\|R(E_k)\|$ 成正比，即求解精度需要随着宏观迭代的进行而不断提高。如果使用一个固定的、不够 stringent 的微观求解容差，当宏观残差减小到与微观求解误差相当的水平时，收敛过程就会停滞或退化为[线性收敛](@entry_id:163614)。

此外，如果微观本构行为本身是**非光滑的**（例如，[理想弹塑性模型](@entry_id:181091)中的屈服角点），宏观[响应函数](@entry_id:142629)的[光滑性](@entry_id:634843)也会被破坏。这违反了Newton法要求Jacobian矩阵[Lipschitz连续的](@entry_id:267396)基本前提，同样会导致收敛性的恶化 。理解这些收敛性的陷阱，是开发鲁棒且高效的并发多尺度代码的关键。