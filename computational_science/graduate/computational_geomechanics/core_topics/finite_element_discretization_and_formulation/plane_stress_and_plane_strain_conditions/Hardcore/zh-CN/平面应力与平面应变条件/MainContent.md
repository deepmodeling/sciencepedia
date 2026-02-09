## 引言
在计算岩土力学等工程领域，对复杂三维（3D）问题的完整分析往往伴随着高昂的计算成本。然而，许多工程结构（如长坝、隧道和薄板）的几何与荷载特性使其能够被二维（2D）模型有效简化。平面应力与平面应变条件正是实现这种简化的两种最基本、最重要的理论。然而，如何正确选择和应用这两种理想化模型，并理解其对分析结果——尤其是在处理岩土材料的压力相关性、塑性破坏及多物理场耦合行为时——的深远影响，是工程师和研究人员面临的一个关键挑战。

本文旨在系统性地阐明这一核心课题。在**“原理与机制”**一章中，我们将深入探讨平面应力与平面应变的基本定义、本构关系推导、以及它们在变分原理中的体现。接下来，在**“应用与跨学科联系”**一章中，我们将通过一系列涵盖固体力学、断裂力学及耦合多物理场的实例，展示这些理论在解决实际工程问题中的强大作用。最后，在**“动手实践”**一章中，您将通过解决具体问题来巩固理论知识，从而将抽象概念与计算实践紧密联系起来。

## 原理与机制

在计算岩土力学领域，对三维（3D）问题的精确分析往往需要巨大的计算资源。幸运的是，许多岩土工程结构，如长坝、隧道、管道和条形基础，其几何形状、材料属性和荷载条件在某一方向上是恒定或近似恒定的。这种特性使得我们可以通过二维（2D）理想化模型来极大地简化问题，同时仍能获得足够精确的解。本章旨在深入阐述两种最核心的二维简化理论——**平面应力**（plane stress）和**平面应变**（plane strain）——的基本原理、本构关系、变分形式及其在岩土工程分析中的关键影响。

### 基本理想化：定义平面应力与平面应变

三维连续体中的任何一点都由一个对称的应力张量 $\boldsymbol{\sigma}$ 和一个应变张量 $\boldsymbol{\varepsilon}$ 来描述。二维简化的核心思想是在假定某个方向（通常是 $z$ 轴）上的某些分量为零，从而将问题简化到 $(x, y)$ 平面上。

#### 平面应变条件

**平面应变**（plane strain）是一种**运动学约束**，它假设物体在平面外（$z$ 方向）的变形受到完全抑制。这适用于那些沿 $z$ 轴非常长、且横截面和荷载不沿该轴线变化的结构，例如长隧道、堤坝或挡土墙。在这种情况下，可以合理地假设每个横截面的变形模式都是相同的，且没有沿 $z$ 轴的位移变化。

严格的数学定义是，所有与 $z$ 方向相关的应变分量均为零 [@problem_id:3550706] [@problem_id:3550719]：
$$
\varepsilon_{zz} = 0, \quad \varepsilon_{xz} = 0, \quad \varepsilon_{yz} = 0
$$
在小应变假设下，应变由位移场 $\boldsymbol{u}=(u, v, w)$ 的梯度定义，即 $\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$。为了满足平面应变条件，位移场必须具有以下形式：
$$
u = u(x,y), \quad v = v(x,y), \quad w = \text{常数}
$$
通常，为了消除刚体平移，我们设 $w=0$。这种位移形式确保了面外法向应变 $\varepsilon_{zz} = \partial w / \partial z = 0$ 和面外剪切应变 $\varepsilon_{xz}$ 与 $\varepsilon_{yz}$ 均为零。

一个至关重要的推论是，为了维持 $\varepsilon_{zz}=0$ 的约束，通常需要在 $z$ 方向上施加一个**约束应力**（confining stress）$\sigma_{zz}$。对于各向同性材料，该应力为 $\sigma_{zz} = \nu(\sigma_{xx} + \sigma_{yy})$，其中 $\nu$ 是泊松比。因此，平面应变状态下，面外应变为零，但面外应力通常不为零。

#### 平面应力条件

与平面应变相反，**平面应力**（plane stress）是一种**静力学约束**。它假设物体在平面外（$z$ 方向）是自由的，无法承受应力。这适用于那些厚度 $h$ 远小于其平面尺寸的薄板结构，且荷载作用于板的平面内。

其数学定义是，所有与 $z$ 方向相关的应力分量均为零 [@problem_id:3550706]：
$$
\sigma_{zz} = 0, \quad \sigma_{xz} = 0, \quad \sigma_{yz} = 0
$$
为了满足这些应力条件，并简化为二维问题，通常假设位移场具有如下形式：面内位移不随厚度变化，即 $u=u(x,y)$ 和 $v=v(x,y)$，而面外位移 $w$ 可以是 $z$ 的函数，即 $w=w(z)$ [@problem_id:3550706]。

在平面应力状态下，由于泊松效应，面外应变 $\varepsilon_{zz}$ 通常不为零。对于各向同性材料，$\varepsilon_{zz} = -\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy})$。这意味着当板在平面内受拉伸时，其厚度会减小。因此，平面应力状态下，面外应力为零，但面外应变通常不为零。

### 二维本构关系

为了在计算模型中使用这些理想化，我们需要推导相应的二维应力-应变关系。我们从三维各向同性线弹性本构定律（胡克定律）出发。其柔度形式为：
$$
\varepsilon_{ij} = \frac{1+\nu}{E}\sigma_{ij} - \frac{\nu}{E}\delta_{ij}\sigma_{kk}
$$
其中 $E$ 是杨氏模量，$\nu$ 是泊松比，$\delta_{ij}$ 是克罗内克符号，$\sigma_{kk} = \sigma_{xx}+\sigma_{yy}+\sigma_{zz}$。

#### 平面应力本构矩阵

在平面应力条件下，我们设置 $\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0$。三维关系式直接简化为平面内的应力-应变关系 [@problem_id:3550715]：
$$
\begin{pmatrix} \varepsilon_{xx} \\ \varepsilon_{yy} \\ \gamma_{xy} \end{pmatrix} = \frac{1}{E} \begin{pmatrix} 1 & -\nu & 0 \\ -\nu & 1 & 0 \\ 0 & 0 & 2(1+\nu) \end{pmatrix} \begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \tau_{xy} \end{pmatrix}
$$
其中 $\gamma_{xy} = 2\varepsilon_{xy}$ 是工程剪应变。通过矩阵求逆，我们可以得到用于有限元分析的**平面应力刚度矩阵** $[D_{ps}]$ [@problem_id:3550742]：
$$
\begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \tau_{xy} \end{pmatrix} = \frac{E}{1-\nu^2} \begin{pmatrix} 1 & \nu & 0 \\ \nu & 1 & 0 \\ 0 & 0 & \frac{1-\nu}{2} \end{pmatrix} \begin{pmatrix} \varepsilon_{xx} \\ \varepsilon_{yy} \\ \gamma_{xy} \end{pmatrix}
$$

#### 平面应变本构矩阵

在平面应变条件下，我们利用运动学约束 $\varepsilon_{zz}=0$。从三维胡克定律的第三行 $\varepsilon_{zz} = \frac{1}{E}[\sigma_{zz} - \nu(\sigma_{xx}+\sigma_{yy})]$，我们解出 $\sigma_{zz} = \nu(\sigma_{xx}+\sigma_{yy})$ [@problem_id:3550778]。将此表达式代回关于 $\varepsilon_{xx}$ 和 $\varepsilon_{yy}$ 的方程中，经过整理，可以得到平面应变下的应力-应变关系。其**平面应变刚度矩阵** $[D_{pe}]$ 形式如下 [@problem_id:3550713] [@problem_id:3550742]：
$$
\begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \tau_{xy} \end{pmatrix} = \frac{E}{(1+\nu)(1-2\nu)} \begin{pmatrix} 1-\nu & \nu & 0 \\ \nu & 1-\nu & 0 \\ 0 & 0 & \frac{1-2\nu}{2} \end{pmatrix} \begin{pmatrix} \varepsilon_{xx} \\ \varepsilon_{yy} \\ \gamma_{xy} \end{pmatrix}
$$

#### 响应对比与等效参数

比较这两种本构矩阵可以发现，平面应变条件下材料的“表观”刚度更高。考虑一个单轴应力状态 $\sigma_{xx}=\sigma_0, \sigma_{yy}=0$。我们可以定义一个“表观平面内泊松比” $\nu_{app} = -\varepsilon_{yy}/\varepsilon_{xx}$ [@problem_id:3550715]。
- 对于平面应力：$\varepsilon_{xx} = \sigma_0/E$, $\varepsilon_{yy} = -\nu\sigma_0/E$，因此 $\nu_{app}^{(ps)} = \nu$。
- 对于平面应变：通过求解其本构关系可得，$\nu_{app}^{(pe)} = \frac{\nu}{1-\nu}$。

由于对于岩土材料 $0 < \nu < 0.5$，所以 $\nu/(1-\nu) > \nu$。这定量地表明，在平面应变约束下，材料在横向上的收缩效应更为显著，因为 $z$ 方向的变形被抑制了。二者之差为 $\Delta\nu_{app} = \frac{\nu^2}{1-\nu}$ [@problem_id:3550715]。

一个有趣的问题是，我们能否找到一组“等效”的材料参数 $(E', \nu')$，使得一个使用这些参数的平面应力模型能够精确复制真实材料 $(E, \nu)$ 在平面应变下的响应？答案是肯定的。通过令 $D_{ps}(E', \nu') = D_{pe}(E, \nu)$，可以解出 [@problem_id:3550742]：
$$
E' = \frac{E}{1-\nu^2}, \quad \nu' = \frac{\nu}{1-\nu}
$$
这种参数替换在纯弹性、仅关心平面内应力应变场时是有效的。然而，如下一节所述，这种等效性具有极大的误导性，在岩土工程中必须慎用。

### 对三维应力状态和岩土分析的影响

二维理想化虽然简化了计算，但它掩盖了两种模型背后截然不同的三维应力现实。这对依赖于完整三维应力状态的岩土分析（如塑性、破坏和流固耦合）至关重要。

考虑一个给定的平面内应力状态，例如 $\sigma_{xx}=64\,\text{MPa}$, $\sigma_{yy}=12\,\text{MPa}$, $\tau_{xy}=20\,\text{MPa}$，材料泊松比 $\nu=0.327$ [@problem_id:3550778]。
- 在**平面应力**下，完整的应力张量中的第三个主应力为 $\sigma_3 = \sigma_{zz} = 0$。
- 在**平面应变**下，第三个主应力为 $\sigma_3 = \sigma_{zz} = \nu(\sigma_{xx} + \sigma_{yy}) = 0.327 \times (64+12) = 24.85\,\text{MPa}$。

这 $24.85\,\text{MPa}$ 的差异对分析结果有深远影响 [@problem_id:3550742]：

1.  **压力相关的屈服准则**：岩土材料的强度（如摩尔-库伦或德鲁克-普拉格准则）强烈依赖于平均应力或静水压力 $p = (\sigma_{xx}+\sigma_{yy}+\sigma_{zz})/3$。在平面应变中，非零的 $\sigma_{zz}$ 显著增加了平均应力，从而提高了材料的抗剪强度和承载能力。如果错误地使用平面应力模型（即忽略 $\sigma_{zz}$），将会严重低估材料的强度，导致不安全的非保守设计。

2.  **体积响应与孔隙水压力**：在饱和土的固结或不排水剪切分析中，孔隙水压力的变化与土骨架的体积应变 $\varepsilon_v = \varepsilon_{xx}+\varepsilon_{yy}+\varepsilon_{zz}$ 密切相关（Biot 理论）。
    - 在平面应变中，$\varepsilon_v = \varepsilon_{xx}+\varepsilon_{yy}$。
    - 在平面应力中，$\varepsilon_v = \varepsilon_{xx}+\varepsilon_{yy}+\varepsilon_{zz} = \varepsilon_{xx}+\varepsilon_{yy} - \frac{\nu}{E}(\sigma_{xx}+\sigma_{yy})$。
    这两种模型预测的体积应变完全不同。平面应变的高度约束性意味着更小的体积变化，这在不排水条件下将导致更大的孔压响应。使用平面应力模型（或其等效参数 $(E', \nu')$）会完全错误地预测孔压的产生与消散，因此不适用于任何流固耦合分析。

### 变分原理与弱形式

在计算力学中，我们通常求解控制方程的**弱形式**（weak form），它源于**虚功原理**（Principle of Virtual Work, PVW）。从三维虚功原理出发，可以严格推导出二维模型的弱形式。

三维虚功原理指出，对于任意运动学容许的虚位移场 $\delta\boldsymbol{u}$，内虚功等于外虚功：
$$
\int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta \mathbf{u}) \, \mathrm{d}\Omega \;=\; \int_{\Omega} \mathbf{b} \cdot \delta \mathbf{u} \, \mathrm{d}\Omega \;+\; \int_{\partial \Omega_{t}} \mathbf{t} \cdot \delta \mathbf{u} \, \mathrm{d}\Gamma
$$
其中 $\boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta \mathbf{u}) = \sigma_{ij}\delta\varepsilon_{ij}$。

#### 平面应变弱形式

在平面应变中，运动学约束 $u_z=0$ 也适用于虚位移场，即 $\delta u_z=0$。这导致所有面外虚应变分量为零：$\delta\varepsilon_{zz} = \delta\varepsilon_{xz} = \delta\varepsilon_{yz} = 0$ [@problem_id:3550713]。因此，内虚功的被积函数简化为：
$$
\sigma_{ij}\delta\varepsilon_{ij} = \sigma_{xx}\delta\varepsilon_{xx} + \sigma_{yy}\delta\varepsilon_{yy} + 2\tau_{xy}\delta\varepsilon_{xy}
$$
一个微妙但关键的结论是：尽管 $\sigma_{zz}$ 在平面应变中非零且对储存的应变能有贡献，但由于其对应的虚应变 $\delta\varepsilon_{zz}$ 恒为零，所以 $\sigma_{zz}$ 对**虚功方程没有任何直接贡献** [@problem_id:3550713] [@problem_id:3550759]。问题被严格地简化为仅涉及平面内分量的二维弱形式。

#### 平面应力弱形式

在平面应力中，简化来自静力学约束 $\sigma_{zz}=\sigma_{xz}=\sigma_{yz}=0$。内虚功的被积函数自然地简化为平面内分量的乘积之和，因为与面外应力相关的项均为零 [@problem_id:3550759]。
对于一个厚度为 $h$ 的薄板，我们需要将三维虚功原理沿厚度方向积分。假设荷载和位移在厚度方向上是均匀的，对外荷载项的积分表明，三维体力 $\mathbf{b}$（单位体积力）和三维面力 $\mathbf{t}$（单位面积力）在二维模型中分别转化为等效的二维面荷载 $h\mathbf{b}$ 和二维线荷载 $h\mathbf{t}$ [@problem_id:3550779]。因此，在有限元列式中，二维外部荷载向量需要乘以厚度 $h$。

### 适用性与扩展概念

#### 平面应变假设的适用判据

平面应变假设仅在特定条件下成立。对于长度为 $L$、宽度为 $B$ 的矩形加载区域，其与理想的无限长条带荷载之间的差异会在加载区的两端产生“端部效应”。根据**圣维南原理**（Saint-Venant’s principle），这些端部效应的影响范围（或衰减长度）与问题的横向特征尺寸（如宽度 $B$ 和土层深度 $H$）相当 [@problem_id:3550702]。

因此，只有当结构的长度 $L$ 远大于此特征尺寸时（例如，$L/B \gg 5$ 或 $10$），在远离两端的中心区域，端部效应才会衰减到可以忽略不计的程度，平面应变假设才近似成立。以下因素会增长端部效应的衰减长度，从而要求更大的长宽比 [@problem_id:3550702]：

- **强刚度反差**：当上覆土层远硬于下卧土层时，会产生“剪力滞后”（shear-lag）效应，使应力沿结构长度方向传递得更远。
- **近乎不可压缩性**：在饱和土不排水条件下，泊松比 $\nu$ 接近 $0.5$。这种材料的侧向耦合极强，使得局部扰动能传播到更远的距离。

#### 广义平面应变

经典平面应变假设可以被推广以适应更复杂的情况，例如允许结构在轴向（$z$ 方向）发生均匀的拉伸/压缩。这种**广义平面应变**（generalized plane strain）模型假设位移场为 [@problem_id:3550719]：
$$
u = u(x,y), \quad v = v(x,y), \quad w = \bar{\varepsilon}_{zz} z + c
$$
其中 $\bar{\varepsilon}_{zz}$ 是一个常数，代表均匀的轴向应变。这种模型允许截面发生整体的轴向伸长，但仍保持为平面。为了确保这样的应变场是**协调的**（compatible），即可以由一个连续的单值位移场导出，它必须满足特定的协调性条件。该模型在分析受轴向力或温度变化影响的长结构（如隧道衬砌）时非常有用。

#### 向各向异性材料的推广

平面应变的概念同样适用于各向异性材料，例如具有层理的沉积岩。对于一个主轴与坐标轴对齐的正交各向异性材料，其本构关系更为复杂 [@problem_id:3550763]。尽管如此，平面应变的运动学约束 $\varepsilon_{zz}=0$ 仍然适用。通过求解三维正交各向异性本构方程，我们可以得到面外应力 $\sigma_{zz}$ 的表达式。它将不再是简单的 $\nu(\sigma_{xx}+\sigma_{yy})$，而是依赖于多个弹性常数，如 $E_z, \nu_{xz}, \nu_{yz}$。例如，在给定的平面内应变 $(\bar{\varepsilon}_x, \bar{\varepsilon}_y)$ 下，$\sigma_{zz}$ 会是这些应变和多个材料参数的线性组合。这表明，平面应变的基本物理原理——即通过施加面外约束应力来抑制面外变形——是普适的，但其具体的数学表达则依赖于材料的本构特性。