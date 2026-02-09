## 引言
在工程与科学领域，准确描述和分析物体内部的受力状态是确保结构安全与性能的基石。然而，一点的应力状态是复杂的，其分量值会随着我们观察坐标系的改变而变化。这引出了一个核心问题：我们如何才能客观地、不依赖于坐标系地量化应力，并找出决定材料成败的关键指标？应力不变量与莫尔圆正是解决这一问题的两大利器，它们构成了从理论力学到工程实践的桥梁。
本文旨在系统性地构建您对二维及三维应力分析的深入理解。在接下来的章节中，我们将首先深入“原理与机制”，从柯西应力张量出发，揭示主应力、应力不变量以及静水/偏应力分解的数学基础与物理内涵。随后，在“应用与交叉学科联系”中，我们将展示这些概念如何应用于材料的屈服与断裂准则、压力敏感材料分析以及高级接触力学问题。最后，通过“动手实践”部分提供的精选习题，您将把理论付诸实践，巩固从张量计算到几何图解的各项核心技能。

## 原理与机制

本章旨在系统地阐述应力状态的核心描述工具：应力不变量与莫尔圆。我们将从柯西应力张量的基本定义出发，逐步深入探讨主应力、应力不变量的物理意义与数学基础，并最终通过莫尔圆这一强大的几何工具，将这些抽象概念直观化。本章内容是理解材料强度、塑性以及破坏理论的基石。

### 应力概念与柯西应力张量

在连续介质力学中，物体内部任意一点的受力状态是通过作用在过该点的任意截面上的力来描述的。定义一个单位法向向量为 $\mathbf{n}$ 的微小截面，作用在该截面上的单位面积力被称为**面力**（traction），记为 $\mathbf{t}(\mathbf{n})$。面力是一个向量，它的大小和方向通常都依赖于截面的方位，即 $\mathbf{n}$ 的指向。

一个根本性的问题是：我们是否需要无限多的信息（即所有可能方向 $\mathbf{n}$ 对应的面力 $\mathbf{t}(\mathbf{n})$）才能完整描述一点的应力状态？伟大的数学家和物理学家 Augustin-Louis Cauchy 给出了否定的答案。通过对一个无穷小四面体进行动量平衡分析，可以证明，在任意一点，面力向量 $\mathbf{t}(\mathbf{n})$ 与该平面的单位法向量 $\mathbf{n}$ 之间存在一个线性映射关系。这个关系由一个二阶张量来表征，我们称之为**柯西应力张量**（Cauchy stress tensor），记为 $\boldsymbol{\sigma}$。这个关系式，即**柯西应力定理**（Cauchy's Stress Theorem），表达为：

$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma}\mathbf{n}
$$

这个公式是固体力学的基石之一。它意味着，只要我们知道了二阶张量 $\boldsymbol{\sigma}$ 在某坐标系下的九个分量，我们就能计算出通过该点的**任何**截面上的面力。此外，对于非极性连续体（即不存在体力偶和面力偶），动量矩平衡定律要求柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。这意味着九个分量中只有六个是独立的。对称性还导出了**柯西对等律**（Cauchy's reciprocal theorem），即作用在法向相反的两个面上的面力大小相等、方向相反：$\mathbf{t}(-\mathbf{n}) = -\mathbf{t}(\mathbf{n})$。[@problem_id:2690964]

作用在任意截面上的面力 $\mathbf{t}(\mathbf{n})$ 可以分解为两个相互垂直的分量：一个沿着法向方向 $\mathbf{n}$ 的**正应力**（normal stress）$\sigma_n$，另一个在截面内的**剪应力**（shear stress）$\boldsymbol{\tau}_n$。按照惯例，当面力在 $\mathbf{n}$ 的正方向上有分量时，正应力为拉伸（通常定义为正），反之为压缩（定义为负）。

$$
\sigma_n = \mathbf{t}(\mathbf{n}) \cdot \mathbf{n}
$$

剪应力向量则为 $\boldsymbol{\tau}_n = \mathbf{t}(\mathbf{n}) - \sigma_n\mathbf{n}$，其大小为 $\tau_n = |\boldsymbol{\tau}_n|$。

例如，考虑一个二维平面应力状态，其应力张量在某坐标系下表示为（单位为 MPa）：
$$
\boldsymbol{\sigma} = \begin{bmatrix} 120  35 \\ 35  50 \end{bmatrix}
$$
我们希望求解法向量为 $\mathbf{n} = (\frac{3}{5}, \frac{4}{5})^{\mathsf{T}}$ 的截面上的应力状态。首先计算面力向量：
$$
\mathbf{t}(\mathbf{n}) = \begin{bmatrix} 120  35 \\ 35  50 \end{bmatrix} \begin{pmatrix} 3/5 \\ 4/5 \end{pmatrix} = \begin{pmatrix} 72 + 28 \\ 21 + 40 \end{pmatrix} = \begin{pmatrix} 100 \\ 61 \end{pmatrix} \, \text{MPa}
$$
该截面上的正应力为：
$$
\sigma_n = \mathbf{t}(\mathbf{n}) \cdot \mathbf{n} = (100 \cdot \frac{3}{5}) + (61 \cdot \frac{4}{5}) = 60 + 48.8 = 108.8 \, \text{MPa}
$$
由于 $\sigma_n > 0$，这是一个拉应力。如果我们定义一个面内切向方向 $\mathbf{a}_1 = (-\frac{4}{5}, \frac{3}{5})^{\mathsf{T}}$，则该方向上的剪应力分量为：
$$
\tau_{n1} = \mathbf{t}(\mathbf{n}) \cdot \mathbf{a}_1 = (100 \cdot -\frac{4}{5}) + (61 \cdot \frac{3}{5}) = -80 + 36.6 = -43.4 \, \text{MPa}
$$
这个计算过程展示了应力张量如何将一点的抽象应力状态与特定物理截面上的具体作用力联系起来。[@problem_id:2690964]

### 主应力与主方向

在无数个通过某一点的截面中，是否存在一些特殊的截面，其上的应力状态具有特别简洁的形式？答案是肯定的。这些特殊截面被称为**主平面**（principal planes），其上的剪应力为零。在主平面上，面力向量 $\mathbf{t}(\mathbf{n})$ 完全沿着法向方向 $\mathbf{n}$，即 $\mathbf{t}(\mathbf{n})$ 与 $\mathbf{n}$ 共线。[@problem_id:2690989]

这个物理定义可以直接转化为一个数学问题。如果 $\mathbf{t}(\mathbf{n})$ 与 $\mathbf{n}$ 共线，那么必然存在一个标量 $\lambda$ 使得 $\mathbf{t}(\mathbf{n}) = \lambda\mathbf{n}$。结合柯西应力定理 $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma}\mathbf{n}$，我们得到：

$$
\boldsymbol{\sigma}\mathbf{n} = \lambda\mathbf{n}
$$

这正是线性代数中标准的**特征值问题**（eigenvalue problem）。因此，寻找主平面和相应的正应力，等价于求解应力张量 $\boldsymbol{\sigma}$ 的特征向量和特征值。

- **主方向**（principal directions）是应力张量的单位特征向量 $\mathbf{n}$。
- **主应力**（principal stresses）是应力张量对应的特征值 $\lambda$。

由于应力张量 $\boldsymbol{\sigma}$ 是一个实对称张量，根据线性代数中的**谱定理**（Spectral Theorem），我们可以得出几个重要的结论：
1.  所有的主应力（特征值）都是实数。
2.  对于三个互不相同的主应力，其对应的主方向（特征向量）是相互正交的。即使在主应力有重根的情况下，也总能找到一组相互正交的主方向。
3.  因此，在任意一点，总存在一组由三个相互正交的主方向构成的坐标系。

当我们将应力张量表示在这个**主坐标系**中时，它的矩阵形式是一个对角矩阵，对角线上的元素就是三个主应力，通常记为 $\sigma_1, \sigma_2, \sigma_3$。

$$
\boldsymbol{\sigma}' = \begin{pmatrix} \sigma_1  0  0 \\ 0  \sigma_2  0 \\ 0  0  \sigma_3 \end{pmatrix}
$$

在这个坐标系中，作用在坐标面上的应力只有正应力，剪应力全为零。这极大地简化了应力状态的描述。

主应力还有一个重要的物理意义：它们是正应力 $\sigma_n$ 在所有可能方向上所能达到的极值（最大值、最小值和鞍点值）。通过使用拉格朗日乘子法求解函数 $\sigma_n(\mathbf{n}) = \mathbf{n}\cdot\boldsymbol{\sigma}\mathbf{n}$ 在约束 $|\mathbf{n}|=1$ 下的极值，可以证明，使 $\sigma_n$ 取得极值的方向恰好就是满足特征值方程 $\boldsymbol{\sigma}\mathbf{n} = \lambda\mathbf{n}$ 的主方向。这为我们理解主应力提供了变分原理的视角。[@problem_id:2690989]

### 应力不变量：不依赖于坐标系的应力量度

应力张量的分量 $\sigma_{ij}$ 的数值依赖于我们选择的坐标系。如果我们将坐标系进行一次刚性旋转（由正交矩阵 $\mathbf{Q}$ 描述），新的应力张量分量 $\boldsymbol{\sigma}'$ 将通过张量变换法则得到：$\boldsymbol{\sigma}' = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\mathsf{T}}$。然而，材料的物理行为，如屈服或断裂，不应依赖于观察者选择的坐标系。这就要求我们寻找那些在坐标旋转下保持不变的量，即**应力不变量**（stress invariants）。[@problem_id:2690948]

寻找主应力的代数方法为我们提供了寻找不变量的系统途径。主应力是特征方程 $\det(\boldsymbol{\sigma} - \lambda\mathbf{I}) = 0$ 的根。对于三维问题，这个方程是一个关于 $\lambda$ 的三次多项式：

$$
p(\lambda) = -\lambda^3 + I_1\lambda^2 - I_2\lambda + I_3 = 0
$$

由于主应力（$\sigma_1, \sigma_2, \sigma_3$）是应力状态的内在物理量，不随坐标系改变，因此这个特征多项式本身及其系数也必须是与坐标系无关的。这三个系数 $I_1, I_2, I_3$ 就是**主应力[不变量](@entry_id:148850)**。[@problem_id:2690985]

它们可以通过应力张量的分量直接计算，也可以用主应力简洁地表示：

1.  **第一不变量 $I_1$**：
    $$
    I_1 = \text{tr}(\boldsymbol{\sigma}) = \sigma_{11} + \sigma_{22} + \sigma_{33} = \sigma_1 + \sigma_2 + \sigma_3
    $$

2.  **第二不变量 $I_2$**：
    $$
    I_2 = \frac{1}{2}[(\text{tr}\boldsymbol{\sigma})^2 - \text{tr}(\boldsymbol{\sigma}^2)] = \sigma_{11}\sigma_{22} + \sigma_{22}\sigma_{33} + \sigma_{33}\sigma_{11} - \sigma_{12}^2 - \sigma_{23}^2 - \sigma_{31}^2 = \sigma_1\sigma_2 + \sigma_2\sigma_3 + \sigma_3\sigma_1
    $$

3.  **第三不变量 $I_3$**：
    $$
    I_3 = \det(\boldsymbol{\sigma}) = \sigma_1\sigma_2\sigma_3
    $$
这些不变量构成了描述应力状态的一组最基本的标量。任何其他应力不变量都可以表示为这三个主不变量的函数。

### 静水应力与偏应力

实验表明，许多材料（尤其是金属）的屈服和塑性变形主要由形状改变引起，而对均匀的静水压力（导致体积改变）不敏感。为了在数学上区分这两种效应，我们将应力张量分解为两部分：

1.  **静水应力**（hydrostatic stress）：也称为球形应力张量，它代表了应力状态中能引起体积均匀胀缩的部分。它被定义为 $\boldsymbol{\sigma}_h = \sigma_m \mathbf{I}$，其中 $\mathbf{I}$ 是单位张量，而 $\sigma_m$ 是**平均正应力**（mean normal stress）。
    $$
    \sigma_m = \frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33}) = \frac{1}{3} \text{tr}(\boldsymbol{\sigma}) = \frac{I_1}{3}
    $$
    静水应力是一个各向同性的应力状态。在工程中，通常定义压应力为正的**静水压力**（hydrostatic pressure）$p = -\sigma_m = -I_1/3$。[@problem_id:2690971] [@problem_id:2690984]

2.  **偏应力**（deviatoric stress）：它代表了应力状态中引起形状改变（畸变）的部分。它被定义为总应力减去静水应力：
    $$
    \mathbf{s} = \boldsymbol{\sigma} - \boldsymbol{\sigma}_h = \boldsymbol{\sigma} - \sigma_m \mathbf{I}
    $$
    偏应力张量最重要的一个特性是它的迹为零，$\text{tr}(\mathbf{s}) = 0$。

这种分解在数学上是**正交**的。如果我们使用二阶张量的Frobenius内积（定义为 $\mathbf{A}:\mathbf{B} = \text{tr}(\mathbf{A}^{\mathsf{T}}\mathbf{B})$），可以证明静水应力张量与偏应力张量是正交的，即 $\boldsymbol{\sigma}_h : \mathbf{s} = 0$。这源于 $\mathbf{s}$ 的迹为零，导致 $\mathbf{s}:\mathbf{I} = \text{tr}(\mathbf{s}) = 0$。这种正交性从几何上强化了静水应力与偏应力分别代表了应力状态中两个独立方面的思想。[@problem_id:2690984]

### 偏应力[不变量](@entry_id:148850)与罗德角

由于材料的塑性行为主要由偏应力驱动，因此偏应力张量的不变量在材料本构理论中扮演着核心角色。我们可以为偏应力张量 $\mathbf{s}$ 定义一套类似的不变量。最常用的是第二和第三偏应力[不变量](@entry_id:148850)，$J_2$ 和 $J_3$。

一个至关重要的性质是，偏应力张量 $\mathbf{s}$ 及其不变量 $J_2$ 和 $J_3$ 都**不依赖于静水压力**。如果我们给一个应力状态 $\boldsymbol{\sigma}$ 叠加上一个任意大小的静水应力 $p\mathbf{I}$，得到新的应力状态 $\boldsymbol{\sigma}' = \boldsymbol{\sigma} + p\mathbf{I}$，其对应的偏应力张量 $\mathbf{s}'$ 仍然与原来的 $\mathbf{s}$ 完全相同。[@problem_id:2690963] 这是因为在计算 $\mathbf{s}'$ 时，新增加的静水应力部分会被刚好减掉：
$$
\mathbf{s}' = \boldsymbol{\sigma}' - \frac{\text{tr}(\boldsymbol{\sigma}')}{3}\mathbf{I} = (\boldsymbol{\sigma} + p\mathbf{I}) - \frac{\text{tr}(\boldsymbol{\sigma})+3p}{3}\mathbf{I} = (\boldsymbol{\sigma} - \frac{\text{tr}(\boldsymbol{\sigma})}{3}\mathbf{I}) + (p\mathbf{I} - p\mathbf{I}) = \mathbf{s}
$$
这说明偏应力[不变量](@entry_id:148850)真正地捕捉了应力状态的“畸变”部分，而滤掉了“体积变化”部分。[@problem_id:2690990]

**第二偏应力[不变量](@entry_id:148850) $J_2$** 定义为：
$$
J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s} = \frac{1}{2} s_{ij}s_{ij}
$$
$J_2$ 总是非负的，它度量了偏应力的“强度”或“大小”。事实上，单位体积的弹性畸变能正比于 $J_2$。著名的 von Mises 屈服准则就是假设当 $J_2$ 达到一个临界值时材料开始屈服。$J_2$ 也可以表示为总应力主应力的函数：
$$
J_2 = \frac{1}{6}[(\sigma_1-\sigma_2)^2 + (\sigma_2-\sigma_3)^2 + (\sigma_3-\sigma_1)^2]
$$
从这个形式可以再次看出，主应力同加一个常数（即施加静水压力）不会改变 $J_2$ 的值。[@problem_id:2690990]

**第三偏应力[不变量](@entry_id:148850) $J_3$** 定义为：
$$
J_3 = \det(\mathbf{s})
$$

$J_2$ 和 $J_3$ 加上 $I_1$ 同样可以完整地描述一个应力状态。然而，为了更细致地描述偏应力状态的“类型”或“模式”，人们引入了**罗德角**（Lode angle）。它由 $J_2$ 和 $J_3$ 构成的一个无量纲参数定义：
$$
\cos(3\theta_L) = \frac{3\sqrt{3}}{2} \frac{J_3}{J_2^{3/2}}
$$
通过这个关系式，我们可以定义罗德角为 $\theta_L = \frac{1}{3}\arccos\left(\frac{3\sqrt{3}}{2}\frac{J_3}{J_2^{3/2}}\right)$。在主应力排序为 $\sigma_1 \ge \sigma_2 \ge \sigma_3$ 的约定下，$\theta_L$ 的取值范围是 $[0, \pi/3]$。罗德角描述了在给定偏应力强度（由$J_2$确定）下，应力状态在不同“剪切模式”之间的分布。[@problem_id:2690966]

-   **$\theta_L = 0$** ($J_3$ 取最大正值) 对应**广义拉伸**状态，其偏应力主值为 $(s_1, -s_1/2, -s_1/2)$。一个典型的例子是 $\sigma_2 = \sigma_3$ 的轴对称拉伸。
-   **$\theta_L = \pi/3$** ($J_3$ 取最大负值) 对应**广义压缩**状态，其偏应力主值为 $(s_1/2, s_1/2, -s_1)$。一个典型的例子是 $\sigma_1 = \sigma_2$ 的轴对称压缩。
-   **$\theta_L = \pi/6$** ($J_3=0$) 对应所谓的**纯剪切**状态，其偏应力主值为 $(s_1, 0, -s_1)$。这意味着中间主应力 $\sigma_2$ 正好是最大和最小主应力的平均值，即 $\sigma_2 = (\sigma_1+\sigma_3)/2$。

罗德角是一个纯粹的“形状”参数，它与静水压力无关，并且在坐标旋转下保持不变，是一个客观的度量。[@problem_id:2690966]

### 莫尔圆：应力的几何表示

尽管应力不变量提供了应力状态的完备代数描述，但它们较为抽象。工程师奥托·莫尔（Otto Mohr）在19世纪末提出了一种巧妙的图解法，将复杂的应力变换关系转化为直观的几何图形——**莫尔圆**（Mohr's Circle）。

对于一个三维应力状态，其主应力为 $\sigma_1 \ge \sigma_2 \ge \sigma_3$，存在三个莫尔圆。每个圆都对应于绕一个主轴旋转的平面系列上的应力状态。具体而言，在 $(\sigma_n, \tau)$ 坐标平面上：

-   **圆12**：由主应力 $\sigma_1$ 和 $\sigma_2$ 定义。圆心在 $(\frac{\sigma_1+\sigma_2}{2}, 0)$，半径为 $R_{12} = \frac{\sigma_1-\sigma_2}{2}$。
-   **圆23**：由主应力 $\sigma_2$ 和 $\sigma_3$ 定义。圆心在 $(\frac{\sigma_2+\sigma_3}{2}, 0)$，半径为 $R_{23} = \frac{\sigma_2-\sigma_3}{2}$。
-   **圆13**：由主应力 $\sigma_1$ 和 $\sigma_3$ 定义。圆心在 $(\frac{\sigma_1+\sigma_3}{2}, 0)$，半径为 $R_{13} = \frac{\sigma_1-\sigma_3}{2}$。

这三个圆构成了莫尔图。一个核心结论是，通过该点的**任意**截面上的应力状态 $(\sigma_n, \tau_n)$ 在莫尔图上对应的点，必定位于由这三个圆所围成的阴影区域内或其边界上。[@problem_id:2690981]

从莫尔图中，我们可以直观地得到几个重要信息：
-   **主应力**：三个圆与横轴的六个交点中的三个（最右、中间、最左）对应于三个主应力 $\sigma_1, \sigma_2, \sigma_3$。
-   **最大剪应力**：材料在该点所承受的**绝对最大剪应力** $\tau_{\max}$ 等于最大的莫尔圆（即圆13）的半径。
    $$
    \tau_{\max} = R_{13} = \frac{\sigma_1 - \sigma_3}{2}
    $$
    这是 Tresca 屈服准则的基础。[@problem_id:2690981]
-   **静水应力的影响**：如果在原始应力状态 $\boldsymbol{\sigma}$ 上叠加一个静水应力 $p\mathbf{I}$，由于所有主应力都增加了 $p$（即 $\sigma_i' = \sigma_i+p$），而主应力之差不变，因此三个莫尔圆的**半径和形状完全不变**，只是整体沿着 $\sigma_n$ 轴平移了 $p$ 的距离。这再次从几何上证明了最大剪应力以及所有偏应力[不变量](@entry_id:148850)（如 $J_2, J_3$）都独立于静水压力。[@problem_id:2690963]
-   **与不变量的联系**：莫尔圆的几何参数与应力不变量之间存在直接联系。例如，我们之前看到 $J_2$ 可以通过三个莫尔圆的半径来表示：$J_2 = \frac{2}{3}(R_{12}^2 + R_{23}^2 + R_{13}^2)$。[@problem_id:2690981] 此外，当 $J_3=0$ 时（罗德角 $\theta_L=\pi/6$），中间主应力是两端的平均，这在莫尔图上表现为两个较小的圆（圆12和圆23）半径相等，且最大的圆（圆13）的半径是它们的二倍。[@problem_id:2690966]

综上所述，应力张量、主应力、应力不变量和莫尔圆共同构成了一套描述和分析应力状态的强大理论框架。代数方法（不变量）提供了精确、客观的度量，而几何方法（莫爾圆）则为这些抽象概念提供了无与伦比的直观理解。