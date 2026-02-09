## 引言
向列相液晶是一种独特的物质状态，它既像液体一样能够流动，又像晶体一样具有长程取向有序。这种“有序流体”的独特性质——流动与分子取向之间的深刻耦合——使其在显示技术、传感器和生物系统中扮演着核心角色。然而，要精确描述这种复杂的耦合行为，需要一个能够同时捕捉流体力学和取向动力学的统一理论框架。简单地将牛顿流体力学应用于液晶是远远不够的，因为它忽略了材料内部的各向异性结构及其动态演化。

本文旨在系统地建立和阐释描述向列相流体动力学的两大核心理论。在第一章“原理与机制”中，我们将深入探讨描述向列相序的数学工具（指向矢与Q张量），建立决定其平衡构象的自由能，并推导耦合流动与取向的完整动力学方程。随后，在第二章“应用与跨学科连接”中，我们将展示这些理论如何应用于解释复杂的流变现象、相变过程以及拓扑缺陷的物理。最后，在第三章“动手实践”中，读者将通过具体的计算练习，加深对关键概念的理解。本文将从最基本的原理出发，引领读者逐步构建起向列相液晶连续介质理论的宏伟大厦。

## 原理与机制

本章旨在深入探讨向列相液晶的连续介质理论，从描述静态有序结构的序参量，到控制其平衡构象的自由能，最终建立描述其流动的完整流体动力学方程。我们将首先介绍两种核心的描述框架——基于指向矢的Leslie-Ericksen (LE) 理论和基于张量序参量的Landau-de Gennes (LdG) 理论，并阐明它们各自的原理和适用范围。

### 描述向列相序：从指向矢到Q张量

#### 向列相态与对称性破缺

从微观上看，向列相液晶由各向异性的棒状或盘状分子构成。在高温的各向同性相中，分子的质心位置和取向都是无序的，体系因此具有完全的平移和旋转对称性（$O(3)$旋转群）。当温度降低到某个临界点以下时，体系会自发地选择一个特定的方向，分子倾向于沿着这个方向排列，同时其质心位置仍然保持无序。这种长程取向有序但没有长程位置有序的状态，就是**向列相**（nematic phase）。

这一相变过程是**自发对称性破缺**的典型例子：描述体系的哈密顿量本身在所有方向上是等价的，但体系的基态（或热力学平衡态）却选择了一个特定的方向，从而破坏了完全的旋转对称性。具体而言，围绕这个自发选择的轴的旋转对称性被保留了下来，而其他方向的旋转对称性则被破坏了 [@problem_id:4096745]。

#### 指向矢场 $\mathbf{n}$

为了在宏观连续介质的尺度上描述这种取向有序，我们引入了**指向矢**（director）场 $\mathbf{n}(\mathbf{x})$。它是一个单位矢量（$|\mathbf{n}|=1$），代表在空间点 $\mathbf{x}$ 处分子取向的局部平均方向。

向列相分子通常是非极性的，这意味着将分子“头尾翻转”后其物理性质不变。这一微观特性在宏观上体现为指向矢的**头尾对称性**（head-tail symmetry），即 $\mathbf{n}$ 和 $-\mathbf{n}$ 描述的是完全相同的物理状态。因此，我们必须进行等同识别：$\mathbf{n} \equiv -\mathbf{n}$。这个性质至关重要，它意味着向列相的序参量空间并非单位球面 $S^2$（如同铁磁体中的磁矩），而是将球面上所有对径点对等同起来的空间，即**实射影平面** $\mathbb{RP}^2$ ($S^2/\mathbb{Z}_2$) [@problem_id:4096745]。这一拓扑特性是向列相中存在半整数拓扑缺陷（如$s=1/2$的向错线）的根本原因。

#### Q张量：一个更普适的描述

尽管指向矢 $\mathbf{n}$ 直观地捕捉了取向有序的方向，但它有两个主要局限性：(1) 它隐含地假设了取向有序的程度在整个材料中是恒定的；(2) 它本身是一个矢量，而由于头尾对称性，任何可观测量都必须是 $\mathbf{n}$ 的偶函数。

为了克服这些局限性，一个更基本、更普适的序参量被引入，即**Landau-de Gennes (LdG) Q张量**。它定义为分子取向分布函数的二阶矩。对于由单位矢量 $\mathbf{u}$ 描述的微观分子取向，$\mathbf{Q}$张量定义为：
$$
Q_{ij} = S_0 \left\langle u_i u_j - \frac{1}{3}\delta_{ij} \right\rangle
$$
其中 $\langle \dots \rangle$ 表示对分子取向分布函数的系综平均，$\delta_{ij}$ 是克罗内克符号，$S_0$ 是一个归一化常数。这个定义确保了 $\mathbf{Q}$ 是一个对称（$Q_{ij} = Q_{ji}$）且无迹（$\operatorname{tr}(\mathbf{Q}) = Q_{ii} = 0$）的二阶张量。

$\mathbf{Q}$张量的优越性在于：
1.  它自然地满足头尾对称性。因为 $Q_{ij}$ 是由微观取向矢量 $\mathbf{u}$ 的二次项 $u_i u_j$ 构成的，所以当 $\mathbf{u} \to -\mathbf{u}$ 时，$\mathbf{Q}$ 保持不变。因此，任何基于 $\mathbf{Q}$ 构建的物理理论都自动地遵守了向列相的非极性要求 [@problem_id:4096745]。
2.  它的本征值和本征矢提供了关于取向序的更完整信息，包括序的程度和对称性（单轴或双轴）。

#### 单轴序与双轴序

在最简单的情况下，分子围绕一个主方向 $\mathbf{n}$ 呈轴对称分布。这种状态被称为**单轴向列相**（uniaxial nematic）。此时，$\mathbf{Q}$张量可以完全由指向矢 $\mathbf{n}$ 和一个标量序参量 $S$ 来描述：
$$
Q_{ij} = \frac{3}{2}S \left( n_i n_j - \frac{1}{3}\delta_{ij} \right)
$$
这种形式的$\mathbf{Q}$张量具有本征值 $\{S, -S/2, -S/2\}$。最大的本征值 $S$ 对应于本征矢 $\mathbf{n}$，它量化了沿主方向排列的有序程度 [@problem_id:4096797] [@problem_id:4096789]。

这个**标量序参量S**（scalar order parameter）定义为第二勒让德多项式 $P_2(\cos\theta)$ 的系综平均值：
$$
S = \langle P_2(\cos\theta) \rangle = \left\langle \frac{3\cos^2\theta - 1}{2} \right\rangle
$$
其中 $\theta$ 是单个分子轴线与指向矢 $\mathbf{n}$ 之间的夹角。$S$ 的取值范围和物理意义如下 [@problem_id:4096789]：
-   **各向同性相** ($S=0$)：分子取向完全随机，$\langle \cos^2\theta \rangle = 1/3$。
-   **完美取向相** ($S=1$)：所有分子都精确地沿着指向矢方向排列（$\theta=0$）。这代表了棒状分子的最有序状态。
-   **完美垂直排列相** ($S=-1/2$)：所有分子都精确地位于垂直于指向矢的平面内（$\theta=\pi/2$）。这代表了盘状分子的最有序状态（oblate order）。

在更一般的情况下，分子取向在垂直于主指向矢 $\mathbf{n}$ 的平面内也存在各向异性。这种状态被称为**双轴向列相**（biaxial nematic），它需要三个相互正交的本征矢和三个互不相同的本征值来描述，此时$\mathbf{Q}$张量不能简化为上述单轴形式。

#### 指向矢描述的局限性

LdG理论之所以比LE理论更为根本，是因为它能够描述后者无法处理的关键物理现象 [@problem_id:4096741]：
1.  **拓扑缺陷核**：在拓扑缺陷（如向错线）的核心区域，为了避免无限大的弹性畸变能，液晶的有序程度会降低，即 $S \to 0$。指向矢 $\mathbf{n}$ 的定义（$|\mathbf{n}|=1$）隐含了 $S$ 为常数，无法描述这种“熔化”到各向同性相的核结构。而$\mathbf{Q}$张量可以通过变为零张量（$\mathbf{Q} \to \mathbf{0}$）来自然地、正则化地处理缺陷核。
2.  **双轴性**：LE理论天生是单轴的，无法描述在强畸变区域或特定流场下可能出现的双轴相。$\mathbf{Q}$张量通过其三个本征值，可以无缝地描述从单轴到双轴的转变。
3.  **相变动力学**：LE理论假设有序度恒定，因此无法描述温度驱动的各向同性-向列相相变，也无法描述流场诱导的有序-无序转变（如剪切熔化）。LdG理论包含一个依赖于 $S$ 的体自由能，因此能够自然地描述这些相变现象。

### 静态学：向列相体系的自由能

材料的平衡构象由其总自由能的最小值决定。对于向列相液晶，总自由能通常包含两部分：依赖于序参量大小的体自由能，和依赖于序参量空间梯度的弹性自由能。

#### 体自由能：Landau-de Gennes势

LdG理论的核心是构造一个唯象的**体自由能密度** $f_b$，它必须是一个标量，并由序参量 $\mathbf{Q}$ 的旋转不变量构成。根据对称性原理，在 $\mathbf{Q}$ 的低阶展开中，只有两个独立的旋转不变量：$\operatorname{tr}(\mathbf{Q}^2)$ 和 $\operatorname{tr}(\mathbf{Q}^3)$。（对于3x3无迹对称张量，更高阶的不变量如 $\operatorname{tr}(\mathbf{Q}^4)$ 并非独立，例如 $\operatorname{tr}(\mathbf{Q}^4) = \frac{1}{2}(\operatorname{tr}(\mathbf{Q}^2))^2$）。

为了描述各向同性-向列相的一级相变，LdG体自由能密度通常被展开到四阶，其最小形式为 [@problem_id:4096725]：
$$
f_b = \frac{A}{2}\operatorname{tr}(\mathbf{Q}^2) - \frac{B}{3}\operatorname{tr}(\mathbf{Q}^3) + \frac{C}{4}(\operatorname{tr}(\mathbf{Q}^2))^2
$$
这里的唯象系数具有明确的物理意义：
-   系数 $A$ 控制着各向同性相（$\mathbf{Q}=\mathbf{0}$）的稳定性。它主要依赖于温度，通常近似为 $A = a_0(T - T^*)$，其中 $a_0>0$，$T^*$ 是一个特征温度，略低于实际的相变温度。当 $T > T^*$ 时，$A>0$，自由能在 $\mathbf{Q}=\mathbf{0}$ 处有局部极小值；当 $T < T^*$ 时，$A<0$，各向同性相变得不稳定。
-   系数 $B>0$ 破坏了自由能相对于 $\mathbf{Q} \to -\mathbf{Q}$ 的对称性。值得注意的是，$\operatorname{tr}(\mathbf{Q}^3)$ 这一项在头尾对称性下是允许的，因为它本身是 $\mathbf{Q}$ 的不变量。正是这个三阶项的存在，使得自由能势垒出现，导致了相变的一级特征（即在相变点，序参量 $S$ 从0跃变到一个有限值）。
-   系数 $C>0$ 保证了当序参量很大时自由能有下界，从而确保了体系的全局稳定性。

#### 弹性自由能：Frank-Oseen模型

当指向矢场 $\mathbf{n}(\mathbf{x})$ 在空间上不再均匀时，会产生**弹性畸变**（elastic distortion），这会增加体系的自由能。**Frank-Oseen自由能密度** $f_{\mathrm{OF}}$ 描述了这种弹性成本。它是通过构造 $\mathbf{n}$ 的空间梯度 $\nabla\mathbf{n}$ 的二次型标量不变量得到的，并且必须满足头尾对称性（即关于 $\mathbf{n}$ 是偶函数）。

对于非手性的向列相，存在三种基本的弹性畸变模式 [@problem_id:4096804]：
1.  **展曲**（Splay）：$\nabla \cdot \mathbf{n} \neq 0$。对应能量项为 $\frac{1}{2}K_1(\nabla\cdot\mathbf{n})^2$。
2.  **扭曲**（Twist）：$\mathbf{n} \cdot (\nabla \times \mathbf{n}) \neq 0$。对应能量项为 $\frac{1}{2}K_2(\mathbf{n}\cdot\nabla\times\mathbf{n})^2$。对于非手性体系，能量必须是扭曲标量的偶次幂，因为 $\mathbf{n}\cdot\nabla\times\mathbf{n}$ 本身是一个伪标量，它在空间反演下会变号。
3.  **弯曲**（Bend）：$\mathbf{n} \times (\nabla \times \mathbf{n}) \neq 0$。对应能量项为 $\frac{1}{2}K_3|\mathbf{n}\times\nabla\times\mathbf{n}|^2$。

这里的 $K_1, K_2, K_3$ 分别是**展曲、扭曲和弯曲弹性常数**。

此外，还存在一个可以写成全散度形式的**鞍展曲**（saddle-splay）项，它在体内的贡献为零，但会影响表面能和拓扑。

综上，非手性向列相的总Frank-Oseen弹性自由能密度为：
$$
f_{\mathrm{OF}} = \frac{1}{2}K_1(\nabla\cdot\mathbf{n})^2 + \frac{1}{2}K_2(\mathbf{n}\cdot\nabla\times\mathbf{n})^2 + \frac{1}{2}K_3|\mathbf{n}\times\nabla\times\mathbf{n}|^2 + K_{24} \nabla \cdot \left[ \mathbf{n}(\nabla\cdot\mathbf{n}) - (\mathbf{n}\cdot\nabla)\mathbf{n} \right]
$$
其中 $K_{24}$ 是鞍展曲弹性常数。

### 动力学：Leslie-Ericksen流体动力学理论

Leslie-Ericksen (LE) 理论描述了在流动和外场作用下，指向矢场 $\mathbf{n}$ 和速度场 $\mathbf{v}$ 如何耦合演化。这是一个基于不可逆过程热力学和对称性原理建立的唯象理论。

#### 向列相流动的运动学

LE理论建立在几个关键的运动学量之上 [@problem_id:4096786]：
-   **应变率张量**（rate-of-strain tensor）$\mathbf{D}$：速度梯度 $\nabla\mathbf{v}$ 的对称部分，$D_{ij} = \frac{1}{2}(\partial_j v_i + \partial_i v_j)$。它描述了流体微元的形变速率。
-   **涡量张量**（vorticity tensor）$\mathbf{W}$：速度梯度 $\nabla\mathbf{v}$ 的反对称部分，$W_{ij} = \frac{1}{2}(\partial_j v_i - \partial_i v_j)$。它描述了流体微元的刚性旋转速率。
-   **协同旋转指向矢速率**（co-rotational director rate）$\mathbf{N}$：指向矢的物质导数 $\dot{\mathbf{n}} = \partial_t \mathbf{n} + (\mathbf{v}\cdot\nabla)\mathbf{n}$ 本身不是一个**客观**（objective）或**标架无关**（frame-indifferent）的量，因为它包含了流体微元刚性旋转带来的变化。为了得到一个客观的量，必须减去这部分旋转，从而定义了协同旋转速率 $\mathbf{N} = \dot{\mathbf{n}} - \mathbf{W}\cdot\mathbf{n}$。本构关系必须依赖于客观的运动学量，如 $\mathbf{D}$ 和 $\mathbf{N}$。

#### 本构关系：Leslie黏性应力

LE理论的核心是黏性应力张量 $\boldsymbol{\sigma}^L$ 的本构关系。该关系假设应力是应变率 $\mathbf{D}$ 和协同旋转指向矢速率 $\mathbf{N}$ 的线性函数，并且必须满足头尾对称性（即关于 $\mathbf{n}$ 是偶函数）。

根据对称性分析，可以构建出满足这些条件的张量基底 [@problem_id:4096805]。对于不可压缩流体，黏性应力张量最一般的形式可以写成六个**Leslie黏性系数** $\alpha_1, \dots, \alpha_6$ 的线性组合：
$$
\sigma^{L}_{ij} = \alpha_1 n_k n_l D_{kl} n_i n_j + \alpha_2 n_j N_i + \alpha_3 n_i N_j + \alpha_4 D_{ij} + \alpha_5 n_i n_k D_{kj} + \alpha_6 n_j n_k D_{ki}
$$
每个 $\alpha_i$ 系数都描述了流体的一种独特的黏性响应。

#### 指向矢动力学与力矩平衡

在忽略指向矢的惯性的情况下（这在大多数情况下是很好的近似），指向矢的演化由一个**力矩平衡方程**（torque balance equation）决定。作用在指向矢上的力矩有两个来源：
1.  **弹性力矩**：由自由能 $F = \int f dV$ 的空间变化产生，通过**分子场**（molecular field）$\mathbf{h} = -\frac{\delta F}{\delta \mathbf{n}}$ 来体现。
2.  **黏性力矩**：由流体流动产生，是 $\mathbf{D}$ 和 $\mathbf{N}$ 的线性函数。

力矩平衡方程要求总力矩为零（在投影到垂直于 $\mathbf{n}$ 的方向上），其标准形式为 [@problem_id:4096759]：
$$
\mathbf{h} - \gamma_1 \mathbf{N} - \gamma_2 \mathbf{D} \cdot \mathbf{n} = \mathbf{0} \quad (\text{projected } \perp \mathbf{n})
$$
这里引入了两个重要的黏性系数组合：
-   **转动黏度**（rotational viscosity）$\gamma_1 = \alpha_3 - \alpha_2$。它描述了抵抗指向矢转动的黏性阻尼。
-   **流动排列参数**（flow-alignment parameter）$\gamma_2 = \alpha_6 - \alpha_5$。它描述了剪切流场对指向矢的排列效应。根据 $\gamma_2$ 和 $\gamma_1$ 的比值，向列相可以表现为流动排列型（flow-aligning）或翻滚型（tumbling）。

#### Onsager倒易关系与Parodi关系

Leslie黏性系数并非完全独立。不可逆过程热力学的基本原理——**Onsager倒易关系**（Onsager's reciprocal relations）——对它们施加了约束。该关系源于微观可逆性原理。

在LE理论中，单位体积的熵产生率 $T\dot{s}$ 可以写成广义通量和广义力的双线性形式 [@problem_id:4096723]：
$$
T\dot{s} = \boldsymbol{\sigma}^L : \mathbf{D} + \mathbf{h} \cdot \mathbf{N}
$$
这里，$(\mathbf{D}, \mathbf{N})$ 可视为广义力，$(\boldsymbol{\sigma}^L, \mathbf{h})$ 可视为广义通量。Onsager关系要求连接这些力和通量的唯象系数矩阵是对称的。

另一方面，角动量守恒定律要求总应力张量的反对称部分必须与分子场产生的内部力偶相平衡。将这两个基本原理（Onsager关系和角动量守恒）结合起来，可以导出一个深刻的约束条件，即**Parodi关系**（Parodi relation）[@problem_id:4096723] [@problem_id:4096786]：
$$
\alpha_2 + \alpha_3 = \alpha_6 - \alpha_5
$$
这个关系也可以写作 $\gamma_2 = \alpha_2 + \alpha_3$。它将六个独立的Leslie黏性系数减少到了五个，是向列相流体动力学理论的一个基石。