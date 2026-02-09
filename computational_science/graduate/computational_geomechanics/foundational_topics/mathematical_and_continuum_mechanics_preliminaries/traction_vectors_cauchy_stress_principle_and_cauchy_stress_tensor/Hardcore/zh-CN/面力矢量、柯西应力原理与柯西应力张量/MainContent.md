## 引言
在连续介质力学中，理解物体内部如何传递力是分析其变形与运动的基础。描述这些内力的核心概念便是“应力”。然而，如何精确地、普适地量化一个点周围的受力状态，使其不依赖于我们观察它的特定角度，构成了一个根本性的挑战。若我们仅用作用于某个特定平面上的力（即牵引力）来描述，则每变换一个观察平面，力的描述就会改变，这无疑会使分析变得异常繁琐。

本文旨在系统性地解决这一问题，引导读者构建起从物理直观到严谨数学表达的桥梁。我们将从最基本的牵引力矢量概念出发，揭示Augustin-Louis Cauchy如何通过其卓越的应力原理，引入了柯西应力张量这一强大工具，从而一劳永逸地解决了应力状态的描述难题。

在接下来的章节中，你将学到：第一章“原理与机制”将深入剖析牵引力矢量、柯西应力张量的定义、推导过程及其对称性、主应力等关键数学物理性质。第二章“应用与交叉学科联系”将展示这些理论概念如何在岩土工程的稳定性分析、复杂材料的失效预测、以及有限元等前沿计算力学方法中发挥核心作用。最后，在“动手实践”部分，你将通过具体的计算练习，将理论知识应用于解决实际问题，从而巩固和深化对柯西应力理论的理解。

## 原理与机制

在本章中，我们将深入探讨连续介质力学的核心概念：应力。我们将从物理直观出发，建立起描述物体内部相互作用力的数学框架。我们将首先引入**牵引力矢量**的概念，以量化一个表面对另一个表面的作用力。随后，我们将引出著名的**柯西应力原理**，并由此定义**柯西应力张量**——一个描述某一点应力状态的强大数学工具。最后，我们将探讨该张量的关键性质，例如对称性、不变量、主应力，以及它在描述岩土材料力学行为（如受压和剪切滑移）中的应用。

### 牵引力矢量：表面的作用力

想象一个处于载荷作用下的连续体，例如地壳中的一块岩石。如果我们用一个假想的平面将其切开，那么被分开的两部分之间必然存在着相互作用力，否则它们无法保持平衡或按牛顿定律运动。这些分布在假想切面上的内力，正是应力概念的物理来源。

为了精确描述这种作用力，我们考虑在物体内部的任意一点 $\boldsymbol{x}$，并设想一个通过该点的光滑微小表面元，其面积为 $\Delta A$，方向由单位法向量 $\boldsymbol{n}$ 定义。这个表面元将物体分为两部分：法向量 $\boldsymbol{n}$ 指向的一侧，以及与 $\boldsymbol{n}$ 相反的一侧。根据连续介质假设，由“反侧”作用于“正侧”的合力 $\Delta \boldsymbol{F}$ 是一个定义明确的量。我们可以定义在点 $\boldsymbol{x}$ 处作用于法向为 $\boldsymbol{n}$ 的平面上的**牵引力矢量** (traction vector) $\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n})$ 为该力密度：

$$
\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n}) = \lim_{\Delta A \to 0} \frac{\Delta \boldsymbol{F}}{\Delta A}
$$

从这个定义中，我们可以得出几个关键结论 [@problem_id:3568358]：
1.  **牵引力是一个矢量**：它既有大小，也有方向。这个方向不一定与平面的法向 $\boldsymbol{n}$ 平行。
2.  **牵引力依赖于位置和方向**：在同一点 $\boldsymbol{x}$，不同方向的切面（即不同的 $\boldsymbol{n}$）所受的牵引力通常是不同的。

一个与牵引力矢量相关的基本原理是其作用-反作用特性。考虑一个极薄的、包裹着内表面的“药盒”形控制体。通过对该控制体应用线性动量守恒定律，可以证明，在极限情况下（即“药盒”厚度趋于零），体积力（如重力）和惯性力的贡献将消失，因为它们与体积成正比，比与面积成正比的表面力是更高阶的无穷小量。这导出了一个类似于牛顿第三定律的结论：在同一个点 $\boldsymbol{x}$，作用于法向为 $-\boldsymbol{n}$ 的平面上的牵引力，恰好是作用于法向为 $\boldsymbol{n}$ 的平面上的牵引力的负值 [@problem_id:3568379]。

$$
\boldsymbol{t}(\boldsymbol{x}, -\boldsymbol{n}) = -\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n})
$$

这个关系被称为**柯西引理** (Cauchy's Lemma)，它体现了内力的平衡本质。值得注意的是，该关系在动态和静态情况下均成立，只要假定不存在集中的面力源。

### 柯西应力原理与应力张量

牵引力矢量的定义虽然直观，但它依赖于平面的方向 $\boldsymbol{n}$，这在实际应用中显得不够方便。我们更希望找到一个只与点 $\boldsymbol{x}$ 相关、能够完全描述该点应力状态的量。法国数学家Augustin-Louis Cauchy通过一个巧妙的思维实验——**柯西四面体论证** (Cauchy's tetrahedron argument)——解决了这个问题。

考虑一个以点 $\boldsymbol{x}$ 为顶点、由三个相互正交的坐标平面和一个斜面组成的微小四面体。对这个四面体应用线性动量守恒定律（即牛顿第二定律），其总合力（包括所有面上的牵引力和体积力）等于其总质量乘以加速度。当四面体的尺寸 $h$ 趋于零时，一个关键的标度关系便显现出来 [@problem_id:3568370]：
-   作用在每个面上的总牵引力与面的面积成正比，即与 $h^2$ 成正比。
-   体积力（如重力）和惯性力（质量乘以加速度）与四面体的体积成正比，即与 $h^3$ 成正比。

因此，当 $h \to 0$ 时，与体积相关的项会比与面积相关的项更快地趋于零。在极限情况下，动量平衡方程简化为一个只包含四个面上牵引力的纯静态平衡方程。通过这个过程可以证明，作用在任意斜面上的牵引力矢量 $\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n})$ 可以表示为作用在三个坐标平面上的牵引力矢量的线性组合，其系数恰好是斜面法向量 $\boldsymbol{n}$ 的三个分量 [@problem_id:3568394]。

这个线性关系意味着存在一个二阶张量，我们称之为**柯西应力张量** (Cauchy stress tensor) $\boldsymbol{\sigma}(\boldsymbol{x})$，它将单位法向量 $\boldsymbol{n}$ 线性映射到相应的牵引力矢量 $\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n})$。这便是**柯西应力定理** (Cauchy's Stress Theorem)：

$$
\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n}) = \boldsymbol{\sigma}(\boldsymbol{x}) \cdot \boldsymbol{n}
$$

或者用分量形式写作 $t_i = \sigma_{ij} n_j$（采用爱因斯坦求和约定）。这里的 $\sigma_{ij}$ 是应力张量 $\boldsymbol{\sigma}$ 在特定坐标系下的分量。$\sigma_{ij}$ 的物理意义是：作用在单位法向量为 $\boldsymbol{e}_j$ 的平面上牵引力矢量的第 $i$ 个分量。

这个定理是连续介质力学的基石。它清晰地区分了两个概念 [@problem_id:3568358]：
-   **柯西应力张量 $\boldsymbol{\sigma}(\boldsymbol{x})$**：描述物质点 $\boldsymbol{x}$ 处**应力状态**的二阶张量。它是一个与观察平面方向无关的、内在的物理量。在三维空间中，它可以由一个 $3 \times 3$ 的矩阵表示。
-   **牵引力矢量 $\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n})$**：作用在通过点 $\boldsymbol{x}$、法向为 $\boldsymbol{n}$ 的**特定平面**上的单位面积力矢量。它是应力张量作用于特定法向量的结果。

### 牵引力的分解与物理诠释

牵引力矢量 $\boldsymbol{t}$ 通常不与平面法向 $\boldsymbol{n}$ 平行。为了更好地理解其物理效应，我们可以将其分解为两个相互垂直的分量：一个垂直于平面（法向分量），另一个平行于平面（剪切分量）[@problem_id:3568362]。

-   **法向应力** (Normal stress) $\sigma_n$ 是 $\boldsymbol{t}$ 在 $\boldsymbol{n}$ 方向上的投影：
    $$
    \sigma_n = \boldsymbol{t} \cdot \boldsymbol{n} = (\boldsymbol{\sigma} \boldsymbol{n}) \cdot \boldsymbol{n} = \boldsymbol{n}^T \boldsymbol{\sigma} \boldsymbol{n}
    $$
    法向应力描述了作用于平面上的“推”或“拉”的效应。$\sigma_n > 0$ 通常表示张力（拉伸），$\sigma_n  0$ 表示压力（压缩）。

-   **剪切应力** (Shear stress) $\tau$ 是 $\boldsymbol{t}$ 在平面内的分量的大小。其矢量为 $\boldsymbol{t}_s = \boldsymbol{t} - \sigma_n \boldsymbol{n}$，大小为：
    $$
    \tau = \|\boldsymbol{t}_s\| = \sqrt{\|\boldsymbol{t}\|^2 - \sigma_n^2}
    $$
    剪切应力描述了使平面两侧材料相互滑动的趋势。

在**岩土力学** (geomechanics) 领域，由于地壳中的应力状态绝大多数是压缩状态，为了方便起见，通常采用**压为正**的符号约定。在此约定下，$\sigma_n > 0$ 表示压力，$\sigma_n  0$ 表示张力。这种约定对于分析土壤和岩石的压实和破坏行为尤其方便，因为它们的抗压强度远大于抗拉强度。

让我们通过一个实例来理解这些概念 [@problem_id:3568362]。假设在某土壤点处，应力张量（压为正，单位为 kPa）为：
$$
\boldsymbol{\sigma} =
\begin{bmatrix}
220  40  0 \\
40  180  30 \\
0  30  150
\end{bmatrix}
$$
我们想要求解通过该点、法向量为 $\boldsymbol{n} = \frac{1}{\sqrt{2}}(1, 1, 0)^T$ 的平面上的牵引力。根据柯西公式：
$$
\boldsymbol{t} = \boldsymbol{\sigma} \boldsymbol{n} = \begin{bmatrix} 220  40  0 \\ 40  180  30 \\ 0  30  150 \end{bmatrix} \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix} = \frac{1}{\sqrt{2}} \begin{pmatrix} 260 \\ 220 \\ 30 \end{pmatrix} \, \text{kPa}
$$
该平面上的法向应力为：
$$
\sigma_n = \boldsymbol{t} \cdot \boldsymbol{n} = \frac{1}{\sqrt{2}} \begin{pmatrix} 260 \\ 220 \\ 30 \end{pmatrix} \cdot \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix} = \frac{1}{2}(260 + 220) = 240 \, \text{kPa}
$$
由于我们采用压为正的约定，$\sigma_n = 240 \, \text{kPa}$ 表示该平面受到压缩。

剪切应力的大小为：
$$
\tau^2 = \|\boldsymbol{t}\|^2 - \sigma_n^2 = \left(\frac{1}{2}(260^2 + 220^2 + 30^2)\right) - 240^2 = 58450 - 57600 = 850
$$
$$
\tau = \sqrt{850} \approx 29.15 \, \text{kPa}
$$
这个剪切应力 $\tau$ 量化了沿该平面驱动潜在滑移的切向力。在岩土工程中，这个值将与材料的抗剪强度（由摩擦和黏聚力决定）进行比较，以评估边坡或地基的稳定性。

### 柯西应力张量的性质

柯西应力张量作为一个数学对象，具有一系列深刻的物理性质，这些性质极大地简化了应力分析。

#### 对称性

在经典连续介质力学中，一个至关重要的结论是**柯西应力张量是对称的**，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ 或 $\sigma_{ij} = \sigma_{ji}$。这个性质并非数学上的要求，而是源于物理上的**角动量守恒定律**。

通过对一个微小立方体单元应用角动量守恒，可以证明，如果不存在分布式的**体力矩** (body couples) 或**面力矩** (couple stresses)，那么为了使单元体不发生无限大的角加速度，应力张量必须是对称的。这一假设在大多数宏观工程问题中是成立的。

然而，在某些更高级的连续体模型中，例如**微极连续体** (micropolar continua) 或**Cosserat连续体**，这一假设被放宽了 [@problem_id:3568401] [@problem_id:3568423]。这些模型被用来描述具有内部微观结构的材料，如颗粒材料（土壤、砂石）、多晶体或泡沫。在这些材料中，颗粒的旋转可能是显著的，从而产生体力矩和面力矩。在这种情况下，应力张量可以有非对称部分，并且需要引入一个额外的**力偶应力张量** $\boldsymbol{\mu}$ 来描述力矩的传递，从而形成一个更完备但更复杂的理论。对于本课程的大部分内容，我们都将假定应力张量是对称的。

#### 应力不变量与应力分解

应力张量虽然有9个分量（对称时为6个独立分量），但其某些组合在坐标系旋转下保持不变，这些量被称为**应力不变量** (stress invariants)。对于一个三维应力张量，有三个基本不变量。一个常用的不变量集合是：
-   $I_1 = \mathrm{tr}(\boldsymbol{\sigma}) = \sigma_{11} + \sigma_{22} + \sigma_{33}$
-   $I_2 = \frac{1}{2} \left[ (\mathrm{tr}(\boldsymbol{\sigma}))^2 - \mathrm{tr}(\boldsymbol{\sigma}^2) \right]$
-   $I_3 = \det(\boldsymbol{\sigma})$

这些不变量的物理意义在于，它们表征了应力状态的内在属性，与我们选择如何观察（即坐标系的选择）无关。

在塑性力学和岩土力学中，将应力张量分解为两个部分通常更有启发性：**球形应力张量** (spherical stress tensor) 和**偏应力张量** (deviatoric stress tensor) [@problem_id:3568377]。

-   **平均应力** (mean stress) 或**静水压力** (hydrostatic pressure) $p$ 定义为：
    $$
    p = \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3} I_1
    $$
    平均应力代表了应力状态的“平均”压力或张力。球形应力张量即为 $p\boldsymbol{I}$，其中 $\boldsymbol{I}$ 是单位张量。这部分应力主要引起物体的体积变化。

-   **偏应力张量** $\boldsymbol{s}$ 定义为总应力减去球形应力部分：
    $$
    \boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}
    $$
    偏应力张量的迹为零 ($\mathrm{tr}(\boldsymbol{s}) = 0$)，它代表了应力状态中导致形状改变（畸变）而非体积改变的部分。材料的屈服和塑性流动主要由偏应力驱动。

基于这种分解，作用在任意平面上的牵引力也可以被分解为由平均应力和偏应力贡献的两部分：
$$
\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n} = (p\boldsymbol{I} + \boldsymbol{s})\boldsymbol{n} = p\boldsymbol{n} + \boldsymbol{s}\boldsymbol{n}
$$
其中，$p\boldsymbol{n}$ 是沿法向的静水压力贡献，而 $\boldsymbol{s}\boldsymbol{n}$ 是由偏应力引起的附加牵引力，它通常既有法向分量也有剪切分量。

#### 主应力与主方向

由于对称的应力张量 $\boldsymbol{\sigma}$ 是一个对称的线性算子，它必然存在一个由相互正交的特征向量组成的基。在力学中，这些特征向量被称为**主方向** (principal directions)，而对应的特征值则被称为**主应力** (principal stresses)。

主应力（记为 $\sigma_1, \sigma_2, \sigma_3$）和主方向（记为 $\boldsymbol{n}_1, \boldsymbol{n}_2, \boldsymbol{n}_3$）由以下特征值问题定义：
$$
\boldsymbol{\sigma}\boldsymbol{n}_i = \sigma_i \boldsymbol{n}_i \quad (\text{no summation over } i)
$$
这个方程的物理意义是：在主方向所定义的平面（即法向量为 $\boldsymbol{n}_i$ 的平面）上，牵引力矢量 $\boldsymbol{t}$ 与法向量 $\boldsymbol{n}_i$ 是平行的，这意味着该平面上**没有剪切应力** [@problem_id:3568391]。主应力就是作用在这些“无剪切”平面上的法向应力。

主应力代表了某一点处所有可能平面上法向应力的极值。通常按代数大小排序，例如 $\sigma_1 \ge \sigma_2 \ge \sigma_3$。
-   最大主应力 $\sigma_1$ 是该点所有平面上可能出现的最大法向应力。
-   最小主应力 $\sigma_3$ 是该点所有平面上可能出现的最小法向应力。

#### 最大剪切应力

与法向应力不同，剪切应力的最大值并不出现在主平面上（主平面上剪切应力为零）。通过分析，可以证明，一个材料点处所能承受的**最大剪切应力** $\tau_{\max}$ 出现在那些法线方向平分最大和最小主应力方向的平面上。其值为：
$$
\tau_{\max} = \frac{\sigma_1 - \sigma_3}{2}
$$
这个量在材料破坏理论中至关重要，例如Tresca屈服准则和Mohr-Coulomb破坏准则都直接与剪切应力相关。它表明，材料的剪切破坏是由最大和最小主应力之差所驱动的。[@problem_id:3568391]

#### 客观性原理

最后，一个在计算力学中至关重要的概念是**客观性** (objectivity) 或称**标架无关性** (frame-indifference)。物理定律不应依赖于观察者。对于应力张量，这意味着当观察者的参考系发生刚体旋转时（由一个正交旋转矩阵 $\mathbf{Q}$ 描述），各物理量必须遵循特定的变换法则，以保证物理定律的形式不变。

对于柯西应力原理 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$，客观性要求：
-   矢量（如 $\boldsymbol{t}$ 和 $\boldsymbol{n}$）变换为 $\boldsymbol{t}' = \mathbf{Q}\boldsymbol{t}$ 和 $\boldsymbol{n}' = \mathbf{Q}\boldsymbol{n}$。
-   二阶张量（如 $\boldsymbol{\sigma}$）变换为 $\boldsymbol{\sigma}' = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$。

将这些变换规则代入旋转后的坐标系中的柯西定律 $\boldsymbol{t}' = \boldsymbol{\sigma}'\boldsymbol{n}'$，我们得到：
$$
\mathbf{Q}\boldsymbol{t} = (\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T)(\mathbf{Q}\boldsymbol{n}) = \mathbf{Q}\boldsymbol{\sigma}(\mathbf{Q}^T\mathbf{Q})\boldsymbol{n} = \mathbf{Q}(\boldsymbol{\sigma}\boldsymbol{n})
$$
这与原始定律是自洽的。在开发和验证数值模拟代码时，必须通过类似的测试来确保所实现的算法是客观的，从而保证计算结果的物理真实性 [@problem_id:3568407]。