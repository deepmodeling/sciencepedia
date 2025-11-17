## 引言
在工程设计领域，从高耸的桥梁到精密的航空发动机，理解结构的[振动](@entry_id:267781)特性至关重要。结构的固有频率和振型决定了其对动态载荷的响应，是避免灾难性共振、优化性能和确保安全可靠性的关键。[有限元法](@entry_id:749389)（FEM）为分析这些动态特性提供了强有力的工具，其核心在于求解一个被称为“[广义特征值问题](@entry_id:151614)”的数学方程。然而，许多工程师和研究者虽然熟练使用商业软件获取[振动分析](@entry_id:146266)结果，却对这一核心问题的物理起源、数学内涵及其在不同领域中的深刻联系缺乏系统性的认识。

本文旨在填补这一知识鸿沟，为读者提供一个关于自由[振动](@entry_id:267781)[广义特征值问题](@entry_id:151614)的全面而深入的视角。我们将在三个循序渐进的章节中展开探讨：

首先，在**“原理与机制”**一章中，我们将回归本源，从连续介质力学出发，推导出控制[振动](@entry_id:267781)行为的[广义特征值方程](@entry_id:265750)。读者将学习到刚度与质量矩阵的构建方法、问题的数学性质，以及在实践中可能遇到的剪切闭锁等数值陷阱。

接着，**“应用与跨学科联系”**一章将视野从基础理论拓展至前沿应用。我们将探讨如何运用Lanczos等先进算法求解数百万自由度的大型问题，并展示该理论框架如何扩展以分析旋转机械的[陀螺效应](@entry_id:163568)、结构的[屈曲](@entry_id:162815)稳定性，乃至在计算化学等交叉学科中发挥作用。

最后，**“动手实践”**部分将理论付诸实践，通过一系列精心设计的编程练习，引导读者亲手实现从单元矩阵推导到完整[振动分析](@entry_id:146266)的全过程，从而巩固所学知识。

通过这一结构化的学习路径，本文旨在将抽象的数学方程与鲜活的物理世界联系起来，使读者不仅知其然，更知其所以然。让我们从第一章开始，深入探索自由[振动分析](@entry_id:146266)的基石。

## 原理与机制

本章旨在阐述结构自由[振动分析](@entry_id:146266)中的核心原理和机制。我们将从连续介质力学的控制方程出发，推导出有限元法所求解的[广义特征值问题](@entry_id:151614)的弱形式。随后，我们将详细讨论[有限元离散化](@entry_id:193156)过程，包括[刚度矩阵](@entry_id:178659)和[质量矩阵](@entry_id:177093)的构建、组装与约束处理。本章还将深入探讨该[特征值问题](@entry_id:142153)的数学性质、不同质量矩阵公式的理论基础，以及在特定[数值条件](@entry_id:136760)下可能出现的病态问题，如[沙漏模式](@entry_id:174855)和剪切闭锁。最后，我们将简要介绍[比例阻尼模型](@entry_id:753818)，及其在[振动分析](@entry_id:146266)中的重要作用。

### 从连续介质力学到[变分形式](@entry_id:166033)

[结构动力学](@entry_id:172684)的研究始于连续介质的[动量平衡](@entry_id:193575)方程。对于一个占据有界区域 $\Omega \subset \mathbb{R}^d$ 的线弹性体，在无[体力](@entry_id:174230)作用的情况下，其运动方程（牛顿第二定律的连续介质形式）为：

$ \nabla \cdot \boldsymbol{\sigma} = \rho \frac{\partial^2 \boldsymbol{u}}{\partial t^2} $

其中，$\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\rho$ 是材料密度，$\boldsymbol{u}$ 是[位移场](@entry_id:141476)。在自由[振动分析](@entry_id:146266)中，我们探求系统的固有[振动](@entry_id:267781)模式，这些模式以[谐波](@entry_id:181533)形式运动。因此，我们假设位移场具有如下形式：$\boldsymbol{u}(\boldsymbol{x}, t) = \boldsymbol{u}(\boldsymbol{x}) e^{i\omega t}$，其中 $\boldsymbol{u}(\boldsymbol{x})$ 是不依赖于时间的[振型](@entry_id:179030)（mode shape），$\omega$ 是[振动](@entry_id:267781)的角频率。将此假设代入[运动方程](@entry_id:170720)，时间[二阶导数](@entry_id:144508)变为 $\frac{\partial^2 \boldsymbol{u}}{\partial t^2} = -\omega^2 \boldsymbol{u}(\boldsymbol{x}) e^{i\omega t}$，从而得到不含时间的控制方程：

$ \nabla \cdot \boldsymbol{\sigma}(\boldsymbol{u}) + \omega^2 \rho \boldsymbol{u} = \mathbf{0} $

为了利用有限元方法求解，我们需将其转化为等价的[弱形式](@entry_id:142897)或[变分形式](@entry_id:166033)。为此，我们将上式与一个任意的、满足齐次本质边界条件的[虚位移](@entry_id:168781)场（或称为[检验函数](@entry_id:166589)）$\boldsymbol{v}$ 做[内积](@entry_id:158127)，并在整个区域 $\Omega$ 上积分。这个检验函数 $\boldsymbol{v}$ 必须属于一个合适的[函数空间](@entry_id:143478)，通常是索伯列夫空间 $H^1$ 的一个[子空间](@entry_id:150286)。

$ \int_\Omega (\nabla \cdot \boldsymbol{\sigma}(\boldsymbol{u})) \cdot \boldsymbol{v} \, \mathrm{d}x + \int_\Omega \omega^2 \rho \boldsymbol{u} \cdot \boldsymbol{v} \, \mathrm{d}x = 0 $

应用散度定理（分部积分）于第一项，我们得到：

$ -\int_\Omega \boldsymbol{\sigma}(\boldsymbol{u}) : \nabla \boldsymbol{v} \, \mathrm{d}x + \int_{\partial\Omega} (\boldsymbol{\sigma}(\boldsymbol{u})\boldsymbol{n}) \cdot \boldsymbol{v} \, \mathrm{d}S + \omega^2 \int_\Omega \rho \boldsymbol{u} \cdot \boldsymbol{v} \, \mathrm{d}x = 0 $

边界积分项 $\int_{\partial\Omega} (\boldsymbol{\sigma}(\boldsymbol{u})\boldsymbol{n}) \cdot \boldsymbol{v} \, \mathrm{d}S$ 在自由[振动](@entry_id:267781)问题中通常会消失。这是因为在边界 $\partial\Omega$ 的狄利克雷（Dirichlet）部分 $\Gamma_D$ 上，[本质边界条件](@entry_id:173524)要求位移为零，我们选择的[检验函数](@entry_id:166589) $\boldsymbol{v}$ 也必须满足 $\boldsymbol{v}=0$ on $\Gamma_D$；而在诺伊曼（Neumann）部分 $\Gamma_N$ 上，自然边界条件通常为零面力，即 $\boldsymbol{\sigma}(\boldsymbol{u})\boldsymbol{n} = \mathbf{0}$。因此，边界项为零。

利用线弹性[本构关系](@entry_id:186508) $\boldsymbol{\sigma}(\boldsymbol{u}) = \boldsymbol{C} : \boldsymbol{\varepsilon}(\boldsymbol{u})$ 和[小应变运动学](@entry_id:192140)关系 $\boldsymbol{\varepsilon}(\boldsymbol{u}) = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^\top)$，并考虑到[应力张量和应变张量](@entry_id:755512)的对称性，上述[积分方程](@entry_id:138643)可以写为：

$ \int_\Omega \boldsymbol{\varepsilon}(\boldsymbol{u}) : \boldsymbol{C} : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, \mathrm{d}x = \omega^2 \int_\Omega \rho \boldsymbol{u} \cdot \boldsymbol{v} \, \mathrm{d}x $

这正是自由[振动](@entry_id:267781)问题的连续[广义特征值问题](@entry_id:151614)的弱形式。我们可以定义两个双线性形式：

- **刚度[双线性形式](@entry_id:746794)**: $a(\boldsymbol{u}, \boldsymbol{v}) := \int_\Omega \boldsymbol{\varepsilon}(\boldsymbol{u}) : \boldsymbol{C} : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, \mathrm{d}x$
- **质量双线性形式**: $m(\boldsymbol{u}, \boldsymbol{v}) := \int_\Omega \rho \boldsymbol{u} \cdot \boldsymbol{v} \, \mathrm{d}x$

令[特征值](@entry_id:154894) $\lambda = \omega^2$，则连续问题可以优雅地表述为：寻找 $(\lambda, \boldsymbol{u}) \in \mathbb{R}_{\ge 0} \times (V \setminus \{\mathbf{0}\})$，使得对于所有 $\boldsymbol{v} \in V$ 均成立：

$ a(\boldsymbol{u}, \boldsymbol{v}) = \lambda m(\boldsymbol{u}, \boldsymbol{v}) $

这里的[函数空间](@entry_id:143478) $V$ 是所有满足齐次本质边界条件的、能量有限的位移场构成的空间，例如 $V := \{\boldsymbol{v} \in [H^1(\Omega)]^d : \boldsymbol{v} = \mathbf{0} \text{ on } \Gamma_D\}$ [@problem_id:2562501]。这个[变分形式](@entry_id:166033)是后续[有限元离散化](@entry_id:193156)的理论基石。

### 有限元离散与[代数特征值问题](@entry_id:169099)

有限元法的核心思想是在一个有限维的函数[子空间](@entry_id:150286)中寻找上述[变分问题](@entry_id:756445)的近似解。我们将连续[位移场](@entry_id:141476) $\boldsymbol{u}(\boldsymbol{x})$ 通过形函数（或[基函数](@entry_id:170178)）$\boldsymbol{N}(\boldsymbol{x})$ 和节点位移向量 $\boldsymbol{d}$ 来近似：$\boldsymbol{u}_h(\boldsymbol{x}, t) = \boldsymbol{N}(\boldsymbol{x}) \boldsymbol{d}(t)$。同样地，检验函数也取自同一空间，$\boldsymbol{v}_h(\boldsymbol{x}) = \boldsymbol{N}(\boldsymbol{x}) \boldsymbol{c}$，其中 $\boldsymbol{c}$ 是任意的常数向量。

将此离散形式代入动态问题的[弱形式](@entry_id:142897)（即包含时间导数的[变分方程](@entry_id:635018)），由于 $\boldsymbol{c}$ 的任意性，[积分方程](@entry_id:138643)转化为一个关于节点位移的[二阶常微分方程](@entry_id:204212)组：

$ \boldsymbol{M} \ddot{\boldsymbol{d}}(t) + \boldsymbol{K} \boldsymbol{d}(t) = \boldsymbol{0} $

其中，**[全局刚度矩阵](@entry_id:138630)** $\boldsymbol{K}$ 和**全局[质量矩阵](@entry_id:177093)** $\boldsymbol{M}$ 由单元矩阵 $\boldsymbol{K}^e$ 和 $\boldsymbol{M}^e$ 组装而成。单元矩阵的定义源于上述[双线性形式](@entry_id:746794)在单元上的离散化：

$ \boldsymbol{K}^e_{ij} = a(N_i, N_j) \quad \text{and} \quad \boldsymbol{M}^e_{ij} = m(N_i, N_j) $

组装过程遵循标准的有限元“[直接刚度法](@entry_id:176969)”，即根据单元的节点连接关系，将单元矩阵的各项贡献累加到全局矩阵的相应位置 [@problem_id:2562448]。例如，对于一个由两个线性杆单元连接节点1-2和2-3构成的一维杆系，节点2的自由度会同时接收来自单元1和单元2的刚度和质量贡献，导致其在全局矩阵中的对角项是两个单元相应项的和。

为了求解该[常微分方程组](@entry_id:266774)，我们再次假设[谐波运动](@entry_id:171819)，令 $\boldsymbol{d}(t) = \boldsymbol{\phi} e^{i\omega t}$，其中 $\boldsymbol{\phi}$ 是描述离散系统[振型](@entry_id:179030)的常数向量。代入后得到：

$ (-\omega^2 \boldsymbol{M} + \boldsymbol{K}) \boldsymbol{\phi} e^{i\omega t} = \boldsymbol{0} $

消去 $e^{i\omega t}$ 并整理，我们便得到了最终的**代数[广义特征值问题](@entry_id:151614) (GEP)**：

$ \boldsymbol{K}\boldsymbol{\phi} = \lambda \boldsymbol{M}\boldsymbol{\phi} $

其中，[特征值](@entry_id:154894) $\lambda = \omega^2$ 是系统固有频率的平方，对应的[特征向量](@entry_id:151813) $\boldsymbol{\phi}$ 是该频率下的离散[振型](@entry_id:179030) [@problem_id:2562593]。求解这个[矩阵特征值问题](@entry_id:142446)是有限元自由[振动分析](@entry_id:146266)的最终目标。

### 质量矩阵的构建：一致质量与集总质量

在构建[质量矩阵](@entry_id:177093) $\boldsymbol{M}$ 时，存在两种主流方法，它们在精度和计算成本之间做出了不同的权衡。

**[一致质量矩阵](@entry_id:174630) (Consistent Mass Matrix)** 直接源于[伽辽金法](@entry_id:749698)对动能项的系统性离散。其单元形式为：

$ \boldsymbol{M}^e_{\text{cons}} = \int_{\Omega_e} \rho \boldsymbol{N}^\top \boldsymbol{N} \, dV $

由于形函数 $\boldsymbol{N}$ 的非局部性（一个节点的形函数会延伸到相邻节点），$\boldsymbol{M}^e_{\text{cons}}$ 通常是一个非对角、耦合的矩阵。例如，对于一个长度为 $L$、密度为 $\rho$、[截面](@entry_id:154995)积为 $A$ 的线性杆单元，其[一致质量矩阵](@entry_id:174630)为 [@problem_id:2562450]：

$ \boldsymbol{M}^e_{\text{cons}} = \frac{\rho A L}{6} \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix} $

从理论上看，[一致质量矩阵](@entry_id:174630)是最优的选择。这是因为它保证了离散系统的动能 $\frac{1}{2}\dot{\boldsymbol{d}}^\top \boldsymbol{M}_{\text{cons}} \dot{\boldsymbol{d}}$ 精确等于在有限元[子空间](@entry_id:150286)中定义的连续体动能 $T(\dot{\boldsymbol{u}}_h) = \frac{1}{2}\int_{\Omega_h} \rho \dot{\boldsymbol{u}}_h \cdot \dot{\boldsymbol{u}}_h \, dV$。这种**能量等价性**使得采用[一致质量矩阵](@entry_id:174630)的有限元方法成为一种真正的[里兹法](@entry_id:168680)（Ritz method），其计算出的[特征值](@entry_id:154894)具有确定的变分界（即上界）和收敛性保证 [@problem_id:2562574]。

**[集总质量矩阵](@entry_id:173011) (Lumped Mass Matrix)** 是一种简化处理，它将单元的总[质量集中](@entry_id:175432)分配到各个节点上，从而得到一个对角矩阵。最常用的集总方法是“行和”法，即将[一致质量矩阵](@entry_id:174630)每行的元素相加，置于对角线位置。对于上述线性杆单元，其总质量为 $\rho A L$，均匀分配给两个节点，得到：

$ \boldsymbol{M}^e_{\text{lump}} = \frac{\rho A L}{2} \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} $

使用[集总质量矩阵](@entry_id:173011)会破坏能量等价性，使其不再是严格的[里兹法](@entry_id:168680)。然而，它的优势在于极大地简化了计算。由于 $\boldsymbol{M}$ 是对角矩阵，特征值问题 $K\phi = \lambda M\phi$ 可以转化为[标准特征值问题](@entry_id:755346) $(M^{-1/2}KM^{-1/2}) (M^{1/2}\phi) = \lambda (M^{1/2}\phi)$，且 $M^{-1/2}$ 的计算非常简单。在[显式动力学](@entry_id:171710)分析中，[对角质量矩阵](@entry_id:173002)更是必不可少的。有趣的是，对于某些低阶单元和粗糙网格，集总质量法有时会因[误差抵消](@entry_id:749073)而偶然得到比一致质量法更接近精确解的频率 [@problem_id:2562450]。

### [广义特征值问题](@entry_id:151614)的性质

[代数特征值问题](@entry_id:169099) $\boldsymbol{K}\boldsymbol{\phi} = \lambda \boldsymbol{M}\boldsymbol{\phi}$ 的解具有一系列优良的数学和物理性质，这源于 $\boldsymbol{K}$ 和 $\boldsymbol{M}$ 矩阵的特性。

由其定义可知，刚度矩阵 $\boldsymbol{K}$ 和[质量矩阵](@entry_id:177093) $\boldsymbol{M}$ 均为[实对称矩阵](@entry_id:192806)。质量矩阵 $\boldsymbol{M}$ 表示系统的动能，对于任何非零运动，动能总是正的，因此 $\boldsymbol{M}$ 是**[对称正定](@entry_id:145886) (SPD)** 的。[刚度矩阵](@entry_id:178659) $\boldsymbol{K}$ 表示系统的应变能，对于任何变形，应变能是非负的，因此 $\boldsymbol{K}$ 是**对称半正定 (SPSD)** 的。

**受[约束系统](@entry_id:164587)**：当施加足够的本质边界条件以消除所有[刚体运动](@entry_id:193355)时（例如，固定梁的一端），任何非零的节点位移都会引起应变能。此时，$\boldsymbol{K}$ 矩阵也变为**对称正定 (SPD)**。在这种情况下，$(K, M)$ 构成一个[对称正定](@entry_id:145886)特征对，可以保证所有[特征值](@entry_id:154894) $\lambda_i = \omega_i^2$ 都是实数且严格为正 [@problem_id:2562518]。

**振型正交性**：对于对称正定[特征值问题](@entry_id:142153)，其[特征向量](@entry_id:151813)（[振型](@entry_id:179030)）具有重要的正交性。对于两个对应于不同[特征值](@entry_id:154894) $\lambda_i \neq \lambda_j$ 的振型 $\boldsymbol{\phi}_i$ 和 $\boldsymbol{\phi}_j$，它们同时满足**[M-正交性](@entry_id:178008)**和**K-正交性**：

$ \boldsymbol{\phi}_i^\top \boldsymbol{M} \boldsymbol{\phi}_j = 0 $
$ \boldsymbol{\phi}_i^\top \boldsymbol{K} \boldsymbol{\phi}_j = 0 $

这个性质是[模态分析](@entry_id:163921)和[模态叠加法](@entry_id:175774)的基础。通常，我们会对[振型](@entry_id:179030)进行**[质量归一化](@entry_id:178966)**，即缩放每个[振型](@entry_id:179030)使其满足 $\boldsymbol{\phi}_i^\top \boldsymbol{M} \boldsymbol{\phi}_i = 1$。经过归一化后，自动有 $\boldsymbol{\phi}_i^\top \boldsymbol{K} \boldsymbol{\phi}_i = \lambda_i$ [@problem_id:2562593]。

**无[约束系统](@entry_id:164587) (自由-自由)**：当结构没有足够的约束来限制其整体[平动](@entry_id:187700)和转动时，例如在太空中飞行的卫星或自由放置在地面上的物体，它会存在**[刚体模态](@entry_id:754366) (rigid-body modes)**。刚体运动不会引起任何内部应变，因此其[应变能](@entry_id:162699)为零。在离散系统中，这意味着存在非零的位移向量 $\boldsymbol{\phi}_{rb}$ 使得 $\boldsymbol{K}\boldsymbol{\phi}_{rb} = \mathbf{0}$。这些向量构成了刚度矩阵 $\boldsymbol{K}$ 的零空间 (nullspace)。

对于一个三维实体，存在6个独立的刚体运动：3个沿坐标轴的[平动](@entry_id:187700)和3个绕坐标轴的转动。因此，其[刚度矩阵](@entry_id:178659) $\boldsymbol{K}$ 的零空间维度为6，这将导致[特征值问题](@entry_id:142153)有6个为零的[特征值](@entry_id:154894)（$\lambda=0$），对应于这6个零频率的[刚体模态](@entry_id:754366) [@problem_id:2562607]。这些[刚体模态](@entry_id:754366)向量可以通过平移向量和旋转向量在每个节点上的位移来精确描述。

### 变分特性与收敛性

[特征值](@entry_id:154894)的计算精度与有限元空间的近似能力密切相关。**瑞利商 (Rayleigh Quotient)** 提供了一个将[特征值](@entry_id:154894)与能量联系起来的强大工具：

$ R(\boldsymbol{\phi}) = \frac{\boldsymbol{\phi}^\top \boldsymbol{K} \boldsymbol{\phi}}{\boldsymbol{\phi}^\top \boldsymbol{M} \boldsymbol{\phi}} $

对于任意[振型](@entry_id:179030) $\boldsymbol{\phi}_i$，其瑞利商的值等于对应的[特征值](@entry_id:154894) $\lambda_i$。更重要的是，**Courant-Fischer 极小极大原理**为我们提供了对[特征值](@entry_id:154894)的变分描述。该定理表明，第 $i$ 个[特征值](@entry_id:154894) $\lambda_i$ 可以表示为在所有 $i$ 维[子空间](@entry_id:150286)中瑞利商最大值的最小值。

[有限元法](@entry_id:749389)本质上是在一个 $k$ 维的试探[子空间](@entry_id:150286) $V_h$ 中寻找最优解（即[里兹法](@entry_id:168680)）。Courant-Fischer 原理的一个直接推论是，通过这种方法计算得到的第 $i$ 个近似[特征值](@entry_id:154894) $\tilde{\lambda}_i$ 总是真实[特征值](@entry_id:154894) $\lambda_i$ 的**[上界](@entry_id:274738)**，即 $\lambda_i \le \tilde{\lambda}_i$ [@problem_id:2562602]。

这个[上界](@entry_id:274738)性质具有深刻的意义：它保证了当我们加密网格或提高单元阶次（即丰富试探[子空间](@entry_id:150286)，例如对于嵌套网格有 $V_H \subset V_h$）时，近似[特征值](@entry_id:154894)会单调非增地逼近真实值，即 $\tilde{\lambda}_i^{(h)} \le \tilde{\lambda}_i^{(H)}$ [@problem_id:2562602]。这为[有限元振动分析](@entry_id:749287)的收敛性提供了坚实的理论基础。

### [数值病态](@entry_id:169044)问题

尽管有限元法具有坚实的理论基础，但在特定情况下，不恰当的单元技术会导致严重的[数值病态](@entry_id:169044)，产生虚假的、非物理的计算结果。

**[减缩积分](@entry_id:167949)与[沙漏模式](@entry_id:174855)**：为了降低计算成本或改善某些单元的性能，有时会采用**[减缩积分](@entry_id:167949) (reduced integration)**，即使用比精确积分所需更少的[高斯点](@entry_id:170251)来计算[单元刚度矩阵](@entry_id:139369)。然而，对于某些单元，这会导致刚度矩阵的秩降低，从而引入额外的、非物理的[零能模式](@entry_id:172472)，称为**[沙漏模式](@entry_id:174855) (hourglass modes)**。

例如，对一个[双线性](@entry_id:146819)[四边形单元](@entry_id:176937)采用单[点积](@entry_id:149019)[分时](@entry_id:274419)，其刚度[矩阵的零空间](@entry_id:152429)维度会从物理上正确的3（2个平动，1个转动）增加到5。多出来的两个[零能模式](@entry_id:172472)就是[沙漏模式](@entry_id:174855)，它们对应着单元在不变形的情况下可以自由“摆动”的模式。这些虚假的[零能模式](@entry_id:172472)会污染[特征值](@entry_id:154894)谱，引入虚假的[零频模](@entry_id:166697)态，使得结构在数值上变得不稳定 [@problem_id:2562519]。在实际应用中，必须采用[沙漏控制](@entry_id:163812)技术来抑制这些非物理模式。

**剪切闭锁 (Shear Locking)**：此现象主要发生在使用低阶、等阶插值的[梁单元](@entry_id:746744)或[壳单元](@entry_id:176094)模拟薄结构时。以铁木辛柯梁（Timoshenko beam）为例，其应变能包含[弯曲能](@entry_id:174691)和剪切能两部分。当梁的厚度 $h$ 变得很小时，剪切刚度相对于弯曲刚度的比例会急剧增大（量级为 $O(h^{-2})$），从而在能量上强制剪切应变 $\gamma = \varphi - w' \approx 0$。

问题在于，如果横向位移 $w$ 和[截面](@entry_id:154995)转角 $\varphi$ 都采用[线性插值](@entry_id:137092)，离散的剪切应变 $\gamma_h$ 是一个线性函数。要使一个线性函数在整个单元上都趋于零，其斜率必须趋于零。这会错误地约束[截面](@entry_id:154995)转角 $\varphi_h$ 也必须是常数，从而导致弯曲应变（曲率）$\varphi'_h \approx 0$。单元因此失去了[弯曲能](@entry_id:174691)力，表现出虚假的、极高的刚度，这种现象称为**剪切闭锁**。其后果是，计算出的固有频率（尤其是高频）会被严重高估，甚至在网格固定的情况下随 $h \to 0$ 而发散 [@problem_id:2562463]。解决剪切闭锁的常用方法包括采用[选择性减缩积分](@entry_id:168281)或发展更高级的混合单元列式。

### 延伸至阻尼系统：比例阻尼

实际结构中总是存在[能量耗散](@entry_id:147406)，即阻尼。引入阻尼后，系统的[运动方程](@entry_id:170720)变为：

$ \boldsymbol{M} \ddot{\boldsymbol{d}} + \boldsymbol{C} \dot{\boldsymbol{d}} + \boldsymbol{K} \boldsymbol{d} = \boldsymbol{0} $

其中 $\boldsymbol{C}$ 是阻尼矩阵。一般情况下，$\boldsymbol{C}$ 的存在会使[运动方程](@entry_id:170720)耦合，求解变得复杂。然而，一个重要且广泛应用的简化是**比例阻尼 (Proportional Damping)**，也称[瑞利阻尼](@entry_id:172362) (Rayleigh Damping)。它假设阻尼矩阵可以表示为质量矩阵和[刚度矩阵](@entry_id:178659)的[线性组合](@entry_id:154743)：

$ \boldsymbol{C} = \alpha \boldsymbol{M} + \beta \boldsymbol{K} $

其中 $\alpha$ 和 $\beta$ 是通过实验数据确定的常数。[比例阻尼模型](@entry_id:753818)的美妙之处在于，无阻尼系统的[振型](@entry_id:179030) $\boldsymbol{\Phi}$ 同样能够对角化阻尼矩阵 $\boldsymbol{C}$。即，在模态[坐标系](@entry_id:156346)下，阻尼矩阵 $\boldsymbol{\Phi}^\top \boldsymbol{C} \boldsymbol{\Phi}$ 也是对角的。

这一特性意味着，即使存在阻尼，整个多自由度系统的[运动方程](@entry_id:170720)在模态[坐标系](@entry_id:156346)下也能完全解耦，分解为一系列独立的、带阻尼的单自由度[振子](@entry_id:271549)方程。这极大地简化了动态响应分析，并构成了**[模态叠加法](@entry_id:175774)**的理论基础 [@problem_id:2562518]。