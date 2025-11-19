## 引言
在[连续介质力学](@entry_id:155125)的宏伟蓝图中，理解力如何在物体内部传递是分析其变形、流动与失效的基础。当我们观察一个受载的结构，例如一座桥梁或一块岩石时，外部施加的力会通过其内部无数个微元，以一种复杂但有序的方式进行传递。一个核心问题随之而来：我们如何精确地描述和量化物体内部任意一点的受力状态？仅仅知道作用在整个物体上的合力是远远不够的，我们需要一个能够刻画局部相互作用的数学工具。

本文旨在系统地回答这一问题，为读者构建关于[体力](@entry_id:174230)、表面曳引和应力矢量的完整知识体系。我们将带领读者经历一个从物理直觉到严谨数学表述的旅程，最终掌握[连续介质力学](@entry_id:155125)中最为核心的概念之一——柯西[应力张量](@entry_id:148973)。

为了实现这一目标，本文分为三个循序渐进的章节。在“原理和机制”一章中，我们将从第一性原理出发，区分体力与面力，引入曳引矢量的概念，并通过经典的柯西四面体论证，揭示[应力张量](@entry_id:148973)的必然存在性及其物理内涵。接下来的“应用与跨学科联系”一章，将展示这些理论工具在解决流体静力学、结构平衡、[材料界面](@entry_id:751731)乃至[断裂力学](@entry_id:141480)等前沿问题中的强大威力。最后，“动手实践”部分提供了一系列精心设计的问题，旨在帮助读者巩固理论知识，并将其应用于具体的计算与分析中。

现在，让我们开启这段探索之旅，首先深入到连续介质内部，探究其最基本的力学原理和作用机制。

## 原理和机制

在前一章中，我们介绍了连续介质力学的基本概念。现在，我们将深入探讨描述连续体内部和表面相互作用力的核心原理。本章的目标是系统地建立体力、[表面力](@entry_id:188034)和应力矢量之间的关系，并最终推导出柯西[应力张量](@entry_id:148973)的概念，它是描述连续体内任意一点应力状态的数学工具。

### 连续体中的力：[体力](@entry_id:174230)与面力

作用于连续[体力](@entry_id:174230)学系统中的力可分为两大类：**体力（Body Forces）** 和 **面力（Surface Forces）**。

**[体力](@entry_id:174230)** 是指作用于物体体积内每个[质点](@entry_id:186768)上的力，通常被视为“[超距作用](@entry_id:264202)”。这些力的大小与物体的质量或体积成正比。体力密度矢量 $\mathbf{b}$ 定义为单位体积所受的体力。一些典型的[体力](@entry_id:174230)包括：

*   **[引力](@entry_id:175476)：** 在重[力场](@entry_id:147325) $\mathbf{g}$（定义为单位质量所受的力，即加速度）中，质量密度为 $\rho$ 的连续体所受的体力密度为 $\mathbf{b}_g = \rho \mathbf{g}$。值得注意的是，这里的 $\mathbf{g}$ 是一个场变量，可以在空间和时间上变化，即 $\mathbf{g}(\mathbf{x}, t)$ [@problem_id:2619681]。

*   **[电磁力](@entry_id:196024)：** 对于带有[电荷](@entry_id:275494)的连续介质，[电磁场](@entry_id:265881)会施加[体力](@entry_id:174230)。如果介质的[电荷密度](@entry_id:144672)为 $\rho_e(\mathbf{x}, t)$，电流密度为 $\mathbf{J}(\mathbf{x}, t)$，并且处于[电场](@entry_id:194326) $\mathbf{E}(\mathbf{x}, t)$ 和[磁场](@entry_id:153296) $\mathbf{B}(\mathbf{x}, t)$ 中，那么根据[洛伦兹力定律](@entry_id:270735)，其电磁体力密度为 $\mathbf{b}_{\mathrm{em}} = \rho_e \mathbf{E} + \mathbf{J} \times \mathbf{B}$。必须强调，[电场](@entry_id:194326)力作用于[电荷密度](@entry_id:144672) $\rho_e$，而非质量密度 $\rho$ [@problem_id:2619681]。

*   **惯性力：** 当在[非惯性参考系](@entry_id:169712)中描述运动时，会出现视在的[体力](@entry_id:174230)，即惯性力。例如，在一个以加速度 $\mathbf{a}_O(t)$ 平动、以角速度 $\boldsymbol{\omega}(t)$ 和角加速度 $\boldsymbol{\alpha}(t)$ 转动的[参考系](@entry_id:169232)中，为了使牛顿第二定律的形式得以保持，必须引入一个惯性体力密度项 $\mathbf{b}_{\mathrm{inert}}$。该项包括[平动](@entry_id:187700)惯性力、[欧拉力](@entry_id:173795)、离心力和[科里奥利力](@entry_id:160096)，其表达式为 $\mathbf{b}_{\mathrm{inert}} = - \rho [ \mathbf{a}_O + \boldsymbol{\alpha} \times \mathbf{r} + \boldsymbol{\omega} \times (\boldsymbol{\omega} \times \mathbf{r}) + 2 \boldsymbol{\omega} \times \mathbf{v}_{\mathrm{rel}} ]$，其中 $\mathbf{r}$ 是[质点](@entry_id:186768)相对于[非惯性系](@entry_id:168746)原点的位置矢量，$\mathbf{v}_{\mathrm{rel}}$ 是相对速度 [@problem_id:2619681]。

与[体力](@entry_id:174230)不同，**面力** 是通过物理接触，跨越物体内部或外部的表面而传递的力。为了精确描述这种相互作用，我们引入**柯西应力原理（Cauchy's Postulate of Local Action）**。该原理断言，在连续体中任意一点 $\mathbf{x}$，通过一个具有[单位法向量](@entry_id:178851) $\mathbf{n}$ 的假想[截面](@entry_id:154995)，[截面](@entry_id:154995)一侧的物质对另一侧物质的作用，可以完全由一个矢量场来描述，这个矢量被称为**曳引矢量（Traction Vector）** 或应力矢量，记为 $\mathbf{t}(\mathbf{x}, \mathbf{n}, t)$ [@problem_id:2619656]。

曳引矢量的正式定义为：作用在以 $\mathbf{x}$ 为中心、法向为 $\mathbf{n}$ 的微小面元 $\Delta S$ 上的[接触力](@entry_id:165079) $\Delta \mathbf{F}$ 与该面元面积 $\Delta A$ 之比在 $\Delta A \to 0$ 时的极限：
$$
\mathbf{t}(\mathbf{x}, \mathbf{n}, t) \equiv \lim_{\Delta A \to 0} \frac{\Delta \mathbf{F}}{\Delta A}
$$
这个定义的关键在于**局部作用假设**：曳引矢量 $\mathbf{t}$ 仅依赖于作用点 $\mathbf{x}$ 和[截面](@entry_id:154995)的方向 $\mathbf{n}$，而与[截面](@entry_id:154995)元的大小、形状或曲率无关。这是一个深刻的简化，它构成了经典[连续介质力学](@entry_id:155125)的基础。必须认识到，这是一种理想化模型。在更广义的连续介质理论中，如**偶应力理论（couple-stress theories）**、**高阶梯[度理论](@entry_id:636058)（higher-gradient theories）** 和**[非局部理论](@entry_id:752667)（nonlocal theories）** 中，这一假设被放宽，从而能够描述材料内部微结构或长程力所带来的更复杂效应 [@problem_id:2619656] [@problem_id:2619640] [@problem_id:2619673]。

### 柯西[应力张量](@entry_id:148973) (σ)

曳引矢量的定义引出了一个核心问题：曳引矢量 $\mathbf{t}$ 如何依赖于[截面](@entry_id:154995)方向 $\mathbf{n}$？答案蕴含于动量守恒定律之中，并通过一个巧妙的思维实验——**柯西四面体论证（Cauchy Tetrahedron Argument）**——得以揭示。

#### 四面体论证

我们考虑连续体内任意一点 $\mathbf{x}_0$，并在该点构建一个无限小的四面体。该四面体有三个面与[笛卡尔坐标系](@entry_id:169789)的坐标平面重合，其向外的[单位法向量](@entry_id:178851)分别为 $-\mathbf{e}_1, -\mathbf{e}_2, -\mathbf{e}_3$。第四个面是一个斜面，其面积为 $A$，向外的[单位法向量](@entry_id:178851)为 $\mathbf{n}$。

我们将线动量守恒的积分形式应用于这个四面体。该定律指出，作用在一个物质体积上的所有外力之和等于其内部物质的[总动量](@entry_id:173071)变化率：
$$
\int_{\partial V} \mathbf{t}(\mathbf{m}) \, dS + \int_V \mathbf{b} \, dV = \int_V \rho \mathbf{a} \, dV
$$
其中 $\mathbf{m}$ 是边界 $\partial V$ 上任意点的外法线。

为了揭示 $\mathbf{t}$ 与 $\mathbf{n}$ 的关系，我们考察当四面体收缩到点 $\mathbf{x}_0$ 时的极限行为。设四面体的特征尺寸为 $\ell$。其表面积（包括斜面 $A$ 和三个坐标面 $A_i$）与 $\ell^2$ 成正比，而其体积 $V$ 与 $\ell^3$ 成正比。因此，面力（曳[引力](@entry_id:175476)积分）的量级为 $O(\ell^2)$，而[体力](@entry_id:174230)与[惯性力](@entry_id:169104)（体积力积分）的量级为 $O(\ell^3)$。

**关键的标度分析 (Scaling Argument)**
在取极限 $\ell \to 0$ 的过程中，体积项 $O(\ell^3)$ 比表面项 $O(\ell^2)$ 更快地趋近于零。因此，只要[体力](@entry_id:174230)密度 $\mathbf{b}$ 和惯性项 $\rho \mathbf{a}$ 在点 $\mathbf{x}_0$ 附近是有界的，体积积分的贡献就可以在极限情况下被忽略。这使得我们能够孤立出表面曳[引力](@entry_id:175476)之间的关系 [@problem_id:2619646]。这一论证的严格性要求应[力场](@entry_id:147325)本身具有一定的光滑性（至少是连续的），以确保用点 $\mathbf{x}_0$ 处的曳[引力](@entry_id:175476)来近似整个微小面上的曳[引力](@entry_id:175476)所产生的误差也是高阶小量（$O(\ell^3)$），不会影响[主导项](@entry_id:167418)的平衡 [@problem_id:2619646] [@problem_id:2619673]。

动量守恒定律应用于一个无限小的“药盒”形[体积元](@entry_id:267802)并取极限，可以得到**柯西引理（Cauchy's Lemma）**，它本质上是[牛顿第三定律](@entry_id:166652)在连续体中的体现：
$$
\mathbf{t}(\mathbf{x}, -\mathbf{n}, t) = -\mathbf{t}(\mathbf{x}, \mathbf{n}, t)
$$
这意味着在同一界面两侧的曳[引力](@entry_id:175476)大小相等、方向相反 [@problem_id:2619651]。

将此引理和标度分析的结果应用于四面体的力[平衡方程](@entry_id:172166)，在极限情况下我们得到：
$$
\mathbf{t}(\mathbf{n}) A - \mathbf{t}(\mathbf{e}_1) A_1 - \mathbf{t}(\mathbf{e}_2) A_2 - \mathbf{t}(\mathbf{e}_3) A_3 = \mathbf{0}
$$
其中 $A_j = A (\mathbf{n} \cdot \mathbf{e}_j) = A n_j$ 是斜面在第 $j$ 个坐标平面上的投影面积。用 $A_j$ 的表达式代入并除以 $A$，我们便得到**柯西基本定理（Cauchy's Fundamental Theorem）**：
$$
\mathbf{t}(\mathbf{n}) = n_1 \mathbf{t}(\mathbf{e}_1) + n_2 \mathbf{t}(\mathbf{e}_2) + n_3 \mathbf{t}(\mathbf{e}_3) = \sum_{j=1}^{3} n_j \mathbf{t}(\mathbf{e}_j)
$$

#### [应力张量](@entry_id:148973)的存在性与定义

柯西基本定理揭示了一个深刻的性质：曳引矢量 $\mathbf{t}(\mathbf{n})$ 是[法向量](@entry_id:264185) $\mathbf{n}$ 的**线性函数**。在数学上，任何将一个矢量[线性映射](@entry_id:185132)到另一个矢量的算子都可以用一个[二阶张量](@entry_id:199780)来表示。因此，必然存在一个[二阶张量](@entry_id:199780) $\boldsymbol{\sigma}$，使得：
$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}
$$
这个[二阶张量](@entry_id:199780) $\boldsymbol{\sigma}$ 就是**柯西[应力张量](@entry_id:148973)**。它完全描述了连续体内一点的应力状态。从一个更高等的数学视角看，柯西定理确立了从 $\mathbf{n}$到曳[引力](@entry_id:175476)分量 $t_i(\mathbf{n})$ 的映射是一个[线性泛函](@entry_id:276136)。根据**[里斯表示定理](@entry_id:140012)（Riesz Representation Theorem）**，在欧几里得空间中，任何一个线性泛函都可以唯一地表示为与某个固定矢量的[点积](@entry_id:149019)。这个固定矢量就构成了[应力张量](@entry_id:148973)的一行，从而保证了[应力张量](@entry_id:148973)的存在性和唯一性 [@problem_id:2619676]。

写成坐标分量的形式，上述关系为：
$$
t_i = \sum_{j=1}^{3} \sigma_{ij} n_j
$$
其中 $t_i$ 是曳引矢量 $\mathbf{t}$ 的第 $i$ 个分量，$\sigma_{ij}$ 是应力张量 $\boldsymbol{\sigma}$ 的分量，而 $n_j$ 是[单位法向量](@entry_id:178851) $\mathbf{n}$ 的第 $j$ 个分量 [@problem_id:2619653]。

**应力分量的物理解释**
通过比较柯西基本定理的分量形式 $t_i(\mathbf{n}) = \sum_{j=1}^{3} n_j t_i(\mathbf{e}_j)$ 和应力张量的定义 $t_i(\mathbf{n}) = \sum_{j=1}^{3} \sigma_{ij} n_j$，我们可以直接得到应力张量分量的物理意义 [@problem_id:2619608]：
$$
\sigma_{ij} = t_i(\mathbf{e}_j)
$$
这个等式表明，应力分量 $\sigma_{ij}$ 是作用在**法向为 $\mathbf{e}_j$ 的平面**上曳引矢量的**第 $i$ 个分量**。换言之，[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的第 $j$ 列，就是作用在 $x_j$ 平面上的曳引矢量 $\mathbf{t}(\mathbf{e}_j)$。

### 应力矢量的性质与应用

#### 正应力与切[应力分解](@entry_id:272862)

在任意给定的[截面](@entry_id:154995)上，曳引矢量 $\mathbf{t}^{(\mathbf{n})}$ 可以唯一地分解为一个垂直于[截面](@entry_id:154995)的分量和一个平行于[截面](@entry_id:154995)的分量。

*   **正应力分量（Normal Component）** $\mathbf{t}_n$ 是 $\mathbf{t}^{(\mathbf{n})}$ 在[法线](@entry_id:167651)方向 $\mathbf{n}$ 上的投影：
    $$
    \mathbf{t}_n = (\mathbf{t}^{(\mathbf{n})} \cdot \mathbf{n}) \mathbf{n}
    $$
    其标量值 $\sigma_n = \mathbf{t}^{(\mathbf{n})} \cdot \mathbf{n}$ 被称为**正应力**。按照惯例，当 $\sigma_n > 0$ 时为**拉伸应力（tension）**，表示[截面](@entry_id:154995)两侧的物质被拉开；当 $\sigma_n  0$ 时为**压缩应力（compression）**，表示物质被推挤在一起。在[流体力学](@entry_id:136788)和接触力学中，压力 $p$ 通常定义为正值，表示压缩，因此 $p = -\sigma_n$ [@problem_id:2619657]。

*   **切应力分量（Shear Component）** $\mathbf{t}_s$ 是 $\mathbf{t}^{(\mathbf{n})}$ 中位于[截面](@entry_id:154995)内的部分：
    $$
    \mathbf{t}_s = \mathbf{t}^{(\mathbf{n})} - \mathbf{t}_n
    $$
    由其定义可知，$\mathbf{t}_s \cdot \mathbf{n} = 0$。其大小 $\tau = \|\mathbf{t}_s\|$ 被称为**[切应力](@entry_id:137139)**。

由于 $\mathbf{t}_n$ 和 $\mathbf{t}_s$ 相互正交，曳引矢量的大小满足勾股定理：$\|\mathbf{t}^{(\mathbf{n})}\|^2 = \|\mathbf{t}_n\|^2 + \|\mathbf{t}_s\|^2 = \sigma_n^2 + \tau^2$。

#### 应用：由曳[引力](@entry_id:175476)测量重建[应力张量](@entry_id:148973)

$\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$ 的关系不仅是理论上的，也具有重要的实践意义。它表明，如果我们能够通过实验测量出某一点上作用于三个线性无关平面上的曳引矢量，我们就可以唯一地确定该点的完整[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$。

例如，假设我们在某一点测得了作用于三个独立平面（[法向量](@entry_id:264185)为 $\mathbf{n}^{(1)}, \mathbf{n}^{(2)}, \mathbf{n}^{(3)}$）上的曳引矢量（$\mathbf{t}^{(1)}, \mathbf{t}^{(2)}, \mathbf{t}^{(3)}$）。我们可以将这三个矢量[方程组](@entry_id:193238)合成一个[矩阵方程](@entry_id:203695) [@problem_id:2619653]：
$$
\begin{pmatrix} |  |  | \\ \mathbf{t}^{(1)}  \mathbf{t}^{(2)}  \mathbf{t}^{(3)} \\ |  |  | \end{pmatrix} = \boldsymbol{\sigma} \begin{pmatrix} |  |  | \\ \mathbf{n}^{(1)}  \mathbf{n}^{(2)}  \mathbf{n}^{(3)} \\ |  |  | \end{pmatrix}
$$
记曳[引力](@entry_id:175476)矩阵为 $\mathbf{T}$，法向量矩阵为 $\mathbf{N}$，则有 $\mathbf{T} = \boldsymbol{\sigma} \mathbf{N}$。由于法向量是线性无关的，矩阵 $\mathbf{N}$ 是可逆的。因此，应力张量可以通过下式求解：
$$
\boldsymbol{\sigma} = \mathbf{T} \mathbf{N}^{-1}
$$

**示例**
假设在某点测得如下数据（单位为 MPa）[@problem_id:2619653]：
*   在法向 $\mathbf{n}^{(1)} = \frac{1}{\sqrt{2}}(1, 1, 0)^{\top}$ 的平面上，曳[引力](@entry_id:175476)为 $\mathbf{t}^{(1)} = \frac{1}{\sqrt{2}}(1, 7, -2)^{\top}$。
*   在法向 $\mathbf{n}^{(2)} = \frac{1}{\sqrt{2}}(0, 1, 1)^{\top}$ 的平面上，曳[引力](@entry_id:175476)为 $\mathbf{t}^{(2)} = \frac{1}{\sqrt{2}}(-1, 5, 3)^{\top}$。
*   在法向 $\mathbf{n}^{(3)} = \frac{1}{\sqrt{2}}(1, 0, 1)^{\top}$ 的平面上，曳[引力](@entry_id:175476)为 $\mathbf{t}^{(3)} = \frac{1}{\sqrt{2}}(2, 4, 5)^{\top}$。

构建矩阵 $\mathbf{T}$ 和 $\mathbf{N}$ (忽略公共因子 $\frac{1}{\sqrt{2}}$)：
$$
\mathbf{T} = \begin{pmatrix} 1  -1  2 \\ 7  5  4 \\ -2  3  5 \end{pmatrix}, \quad \mathbf{N} = \begin{pmatrix} 1  0  1 \\ 1  1  0 \\ 0  1  1 \end{pmatrix}
$$
计算 $\mathbf{N}$ 的逆矩阵 $\mathbf{N}^{-1}$，然后进行[矩阵乘法](@entry_id:156035) $\boldsymbol{\sigma} = \mathbf{T} \mathbf{N}^{-1}$，可得该点的[应力张量](@entry_id:148973)为：
$$
\boldsymbol{\sigma} = \begin{pmatrix} 2  -1  0 \\ 3  4  1 \\ 0  -2  5 \end{pmatrix} \text{ MPa}
$$
这个例子具体展示了如何从可测量的[表面力](@entry_id:188034)确定描述内部应力状态的抽象张量。

### 从局部应力到控制方程

柯西应力张量是连接局部相互作用与宏观物体运动的桥梁。我们可以通过它将线[动量守恒](@entry_id:149964)的积分形式转化为局部微分形式。

再次考虑线动量守恒的积分形式：
$$
\int_V \rho \mathbf{a} \, dV = \int_{\partial V} \mathbf{t}(\mathbf{n}) \, dS + \int_V \mathbf{b} \, dV
$$
利用关系式 $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}$，并将**[高斯散度定理](@entry_id:188065)（Gauss's Divergence Theorem）** 应用于[表面力](@entry_id:188034)积分项，我们可以将表[面积分](@entry_id:275394)转化为体积积分。[散度定理](@entry_id:143110)的一个张量形式是 $\int_{\partial V} \boldsymbol{\sigma} \mathbf{n} \, dS = \int_V (\nabla \cdot \boldsymbol{\sigma}) \, dV$。这里，$\nabla \cdot \boldsymbol{\sigma}$ 是应力[张量的散度](@entry_id:191736)，在分量形式下其第 $i$ 个分量为 $(\nabla \cdot \boldsymbol{\sigma})_i = \sum_{j=1}^{3} \frac{\partial \sigma_{ij}}{\partial x_j}$。

将此结果代入[动量平衡](@entry_id:193575)方程，我们得到：
$$
\int_V \rho \mathbf{a} \, dV = \int_V (\nabla \cdot \boldsymbol{\sigma}) \, dV + \int_V \mathbf{b} \, dV
$$
由于该等式必须对**任意**物质体积 $V$ 成立，因此被积函数必须处处相等。这便得到了**柯西第一运动定律（Cauchy's First Law of Motion）** 的局部（[微分](@entry_id:158718)）形式：
$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \rho \mathbf{a}
$$
这个方程是连续介质力学的基本[运动方程](@entry_id:170720)之一。它描述了在任意一点，应力的空间变化率（通过散度体现）和[体力](@entry_id:174230)密度如何共同产生物质的加速度。

对于**静态平衡（static equilibrium）** 的情况，加速度 $\mathbf{a} = \mathbf{0}$，[运动方程](@entry_id:170720)简化为 [@problem_id:2619663]：
$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}
$$
这是固体力学中求解静态问题的核心方程。

最后，除了线[动量守恒](@entry_id:149964)，[角动量守恒](@entry_id:156798)也对[应力张量](@entry_id:148973)施加了重要约束。在没有体力偶或面力偶的经典柯西连续体中，角动量守恒定律要求柯西[应力张量](@entry_id:148973)必须是**对称的**，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ 或 $\sigma_{ij} = \sigma_{ji}$ [@problem_id:2619656]。这意味着描述一点的应力状态只需要 6 个独立的应力分量，而不是 9 个。

### 柯西模型的局限性与推广

本章所建立的经典柯西应力理论是一个极其成功和广泛应用的物理模型。然而，认识到其固有的假设和局限性也同样重要。

该理论的核心是**局部作用原理**，即一点的应力只取决于该点的变形状态，而与邻近点无关。这排除了材料内部可能存在的[特征长度尺度](@entry_id:266383)。

在以下几种情况下，经典柯西模型需要修正或推广：

1.  **几何[奇异点](@entry_id:199525)：** 在物体的尖角或边缘处，表面的[法向量](@entry_id:264185)不是唯一确定的。因此，在这些点上，经典曳引矢量的概念本身就变得不明确，应[力场](@entry_id:147325)通常会表现出奇异性，使得经典的四面体论证失效 [@problem_id:2619673]。

2.  **[广义连续介质理论](@entry_id:193621)：** 为了描述具有复杂微观结构的材料（如[晶格](@entry_id:196752)材料、泡沫、[颗粒材料](@entry_id:750005)等），发展出了多种[广义连续介质理论](@entry_id:193621)。
    *   在**偶应力或 Cosserat 理论**中，物[质点](@entry_id:186768)不仅有[平动自由度](@entry_id:140257)，还有[转动自由度](@entry_id:141502)。这引入了**偶应力（couple-stress）** 的概念，并导致力应力张量 $\boldsymbol{\sigma}$ 不再对称 [@problem_id:2619640]。
    *   在**高阶梯度理论**中，材料的内能被认为不仅依赖于变形梯度，还依赖于变形的更高阶梯度。这导致了更高阶的应力张量（如三阶的超应力），并且曳[引力](@entry_id:175476)可能依赖于表面的曲率 [@problem_id:2619673]。

本章所介绍的柯西应力理论是[连续介质力学](@entry_id:155125)的基石。理解其推导过程、物理意义和应用方法，是进一步学习弹性、塑性、[流体力学](@entry_id:136788)以及更前沿力学理论的先决条件。