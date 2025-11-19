## 引言
在[固体力学](@entry_id:164042)及更广泛的物理科学领域，张量是描述方向依赖物理量（如应力、应变、导热率）不可或缺的数学语言。一个物理现象的本质，例如材料内部某一点的受力状态，并不会因为我们选择用哪个[坐标系](@entry_id:156346)去观察它而改变。然而，描述这一状态的数值——张量的分量——却深刻地依赖于[坐标系](@entry_id:156346)的选择。这一看似矛盾的现象引出了一个核心问题：我们如何系统地、精确地将在一个[坐标系](@entry_id:156346)下获得的知识，转换到另一个[坐标系](@entry_id:156346)中去？正确回答这个问题，对于求解复杂的工程问题、建立普适的物理定律至关重要。

本文旨在为读者构建一个关于张量[坐标变换](@entry_id:172727)的完整知识体系。我们将从基本原理出发，逐步深入到高级应用，带领您全面掌握这一核心概念。文章结构如下：
- 在“**原理和机制**”一章中，我们将奠定数学基础，从正交基底下的[旋转变换](@entry_id:200017)出发，推导二阶及[高阶张量](@entry_id:200122)的变换法则，并将其推广至[曲线坐标系](@entry_id:172561)和[非线性](@entry_id:637147)[大变形理论](@entry_id:188422)，最后探讨保证物理定律客观性的关键概念——[客观率](@entry_id:198692)。
- 在“**应用与跨学科联系**”一章中，我们将展示这些原理的强大威力，探讨它们如何确保物理定律的普适性、如何精确表征各向异性材料，并揭示[张量不变量](@entry_id:203254)如何对应物理系统的内在属性和极值状态。
- 在“**动手实践**”部分，我们精选了一系列计算问题，旨在通过实际操作，加深您对[张量变换](@entry_id:183453)理论的理解，并揭示实践中可能遇到的陷阱。

通过本次学习，您将不仅掌握[张量变换](@entry_id:183453)的计算方法，更能深刻理解其背后的物理思想，从而在面对不同学科背景下的力学问题时，能够游刃有余地进行分析与建模。

## 原理和机制

在[连续介质力学](@entry_id:155125)中，张量是描述物理量（如应力、应变和材料属性）的核心数学工具。张量的一个基本特性是其物理意义独立于用于描述它的[坐标系](@entry_id:156346)。然而，张量的分量——即其在特定基底上的“投影”——会随着[坐标系](@entry_id:156346)的改变而改变。理解这些分量如何变换，对于在不同参考标架下正确地表述和求解物理问题至关重要。本章深入探讨张量坐标变换的原理和机制，从[正交基](@entry_id:264024)底下的旋转，到[曲线坐标系](@entry_id:172561)中的一般变换，再到[非线性](@entry_id:637147)变形和[客观率](@entry_id:198692)的复杂情况。

### 张量的本质：不变性与表示

在深入研究变换法则的细节之前，我们必须首先理解张量的一个核心概念：**物理[不变性](@entry_id:140168)**。一个二阶张量，例如柯西应力张量 $\boldsymbol{\sigma}$，是一个将向量（例如，平面的[法向量](@entry_id:264185) $\mathbf{n}$）[线性映射](@entry_id:185132)到另一个向量（例如，该平面上的牵[引力](@entry_id:175476)向量 $\mathbf{t}$）的数学实体。这个映射关系 $\mathbf{t} = \boldsymbol{\sigma}(\mathbf{n})$ 是物理定律的体现，其本身并不依赖于任何[坐标系](@entry_id:156346)。

然而，为了进行计算，我们必须在选定的基底中表示张量和向量。张量 $\boldsymbol{\sigma}$ 在一个基底中的表示是一个分量矩阵 $[\sigma]$。张量的某些内在属性，无论我们选择哪个基底，都保持不变。其中最重要的是其**[主值](@entry_id:189577)**（principal values）和**主方向**（principal directions）。主值和[主方向](@entry_id:276187)由固有[特征值问题](@entry_id:142153) $\boldsymbol{\sigma}(\mathbf{n}_p) = \sigma_p \mathbf{n}_p$ 定义，其中 $\sigma_p$ 是主应力，$\mathbf{n}_p$ 是对应的[主方向](@entry_id:276187)。

为什么[主值](@entry_id:189577)是[坐标系](@entry_id:156346)无关的呢？我们可以通过考察其在任意正交基底中的矩阵表示来证明这一点。在任何[正交基](@entry_id:264024)底中，[特征值问题](@entry_id:142153)都表现为[矩阵特征值问题](@entry_id:142446) $[\sigma][n_p] = \sigma_p[n_p]$。其解，即[特征值](@entry_id:154894) $\sigma_p$，由特征方程 $\det([\sigma] - \lambda I) = 0$ 给出。

现在，考虑从一个[正交基](@entry_id:264024)底到另一个[正交基](@entry_id:264024)底的变换。如我们将在下一节中详细推导的，新旧基底中的张量分量矩阵 $[\sigma]'$ 和 $[\sigma]$ 通过一个正交矩阵 $[Q]$ 以**相似变换**（similarity transformation）相关联：$[\sigma]' = [Q][\sigma][Q]^T$。由于 $[Q]$ 是正交的，我们有 $[Q]^T = [Q]^{-1}$。因此，变换可以写成 $[\sigma]' = [Q][\sigma][Q]^{-1}$。新基底中的[特征方程](@entry_id:265849)是 $\det([\sigma]' - \lambda I) = 0$。代入变换法则：

$$
\det([Q][\sigma][Q]^{-1} - \lambda [Q][I][Q]^{-1}) = \det([Q]([\sigma] - \lambda I)[Q]^{-1}) = \det([Q])\det([\sigma] - \lambda I)\det([Q]^{-1}) = \det([\sigma] - \lambda I) = 0
$$

这表明，张量分量矩阵的[特征方程](@entry_id:265849)在所有[正交基](@entry_id:264024)底下都是相同的。因此，其根——即张量的主值——是**[不变量](@entry_id:148850)**（invariants）。这个重要的结论意味着，无论我们在哪个[坐标系](@entry_id:156346)中计算，材料某一点的主应力都是唯一的 [@problem_id:2625105]。

[特征方程](@entry_id:265849)通常写作多项式形式：$-\lambda^3 + I_1 \lambda^2 - I_2 \lambda + I_3 = 0$。由于该方程本身是不变的，其系数 $I_1 = \mathrm{tr}(\boldsymbol{\sigma})$、$I_2 = \frac{1}{2}[\mathrm{tr}(\boldsymbol{\sigma})^2 - \mathrm{tr}(\boldsymbol{\sigma}^2)]$ 和 $I_3 = \det(\boldsymbol{\sigma})$ 也必须是[不变量](@entry_id:148850)。它们被称为应力张量的**主[标量不变量](@entry_id:193787)**（principal scalar invariants），并在材料本构理论中扮演着核心角色。

例如，给定一个在某[坐标系](@entry_id:156346) $\mathcal{B}'$ 中的应力张量 [@problem_id:2625105]：
$$
[\boldsymbol{\sigma}]_{\mathcal{B}'} = \begin{pmatrix} \frac{11}{2}  \frac{3}{2}  0 \\ \frac{3}{2}  \frac{11}{2}  0 \\ 0  0  2 \end{pmatrix} \text{ (MPa)}
$$
我们无需知道这个[坐标系](@entry_id:156346) $\mathcal{B}'$ 与实验室坐标系 $\mathcal{B}$ 的关系，就可以直接计算其主应力。通过求解特征方程 $\det([\boldsymbol{\sigma}]_{\mathcal{B}'} - \sigma_p I) = 0$，我们发现[主应力](@entry_id:176761)为 $7 \text{ MPa}$、$4 \text{ MPa}$ 和 $2 \text{ MPa}$。这些值是该应力状态的内在属性。

### 正交基底变换下的张量分量

现在我们来建立张量分量在不同[正交基](@entry_id:264024)底之间变换的精确法则。首先，区分两种基本的变换视角至关重要：**被动变换**（passive transformation）和**主动变换**（active transformation）。

- **被动变换**：物理实体（如向量或张量）保持固定，而我们改变观察它的[坐标系](@entry_id:156346)（基底）。这本质上是一种“改变视角”或“换基”。
- **主动变换**：[坐标系](@entry_id:156346)保持固定，而物理实体本身在空间中发生移动或旋转。

尽管这两种变换在概念上不同，但它们在数学上密切相关，通常都涉及**正交张量**（或其矩阵表示，即**正交矩阵** $\mathbf{Q}$，满足 $\mathbf{Q}\mathbf{Q}^T = \mathbf{Q}^T\mathbf{Q} = \mathbf{I}$）。

让我们从第一性原理推导二阶张量在被动变换下的分量变换法则 [@problem_id:2625106]。设 $\boldsymbol{\sigma}$ 是一个二阶张量，它将向量 $\mathbf{v}$ 映射为向量 $\mathbf{u}$，即 $\mathbf{u} = \boldsymbol{\sigma}(\mathbf{v})$。在初始[坐标系](@entry_id:156346) $\mathcal{S}$ 中，该关系的分量形式为 $[u]_{\mathcal{S}} = [\sigma]_{\mathcal{S}} [v]_{\mathcal{S}}$。

现在，我们引入一个新的[正交坐标](@entry_id:166074)系 $\mathcal{S}'$。从 $\mathcal{S}$ 到 $\mathcal{S}'$ 的基底变换由一个正交矩阵 $\mathbf{Q}$ 描述，其定义为 $Q_{ij} = \mathbf{e}'_i \cdot \mathbf{e}_j$。任何向量（如 $\mathbf{u}$ 和 $\mathbf{v}$）在两个[坐标系](@entry_id:156346)中的分量通过 $\mathbf{Q}$ 关联：$[v]_{\mathcal{S}'} = \mathbf{Q} [v]_{\mathcal{S}}$。反之，$[v]_{\mathcal{S}} = \mathbf{Q}^T [v]_{\mathcal{S}'}$。

我们将这些关系代入原始的张量映射方程 $[u]_{\mathcal{S}} = [\sigma]_{\mathcal{S}} [v]_{\mathcal{S}}$：
$$
\mathbf{Q}^T [u]_{\mathcal{S}'} = [\sigma]_{\mathcal{S}} (\mathbf{Q}^T [v]_{\mathcal{S}'})
$$
为了得到新[坐标系](@entry_id:156346)下的关系式 $[u]_{\mathcal{S}'} = [\sigma]_{\mathcal{S}'} [v]_{\mathcal{S}'}$，我们将上式两边左乘 $\mathbf{Q}$：
$$
(\mathbf{Q}\mathbf{Q}^T) [u]_{\mathcal{S}'} = (\mathbf{Q} [\sigma]_{\mathcal{S}} \mathbf{Q}^T) [v]_{\mathcal{S}'}
$$
由于 $\mathbf{Q}\mathbf{Q}^T = \mathbf{I}$，我们得到：
$$
[u]_{\mathcal{S}'} = (\mathbf{Q} [\sigma]_{\mathcal{S}} \mathbf{Q}^T) [v]_{\mathcal{S}'}
$$
通过与定义式 $[u]_{\mathcal{S}'} = [\sigma]_{\mathcal{S}'} [v]_{\mathcal{S}'}$ 比较，我们最终确定了[二阶张量](@entry_id:199780)分量的变换法则：
$$
[\sigma]_{\mathcal{S}'} = \mathbf{Q} [\sigma]_{\mathcal{S}} \mathbf{Q}^T
$$
或者用分量形式表示为 $\sigma'_{kl} = Q_{ki} \sigma_{ij} Q_{lj}$。

**重要约定**：值得注意的是，[变换矩阵](@entry_id:151616)的定义约定会影响公式的形式。在一些文献中，[变换矩阵](@entry_id:151616)被定义为主动旋转的矩阵，导致被动变换下的向量分量变换为 $[v]' = \mathbf{Q}^T [v]$。在这种约定下，[张量变换法则](@entry_id:185176)变为 $[\sigma]' = \mathbf{Q}^T [\sigma] \mathbf{Q}$ [@problem_id:2625088]。这两种形式是等价的，只是对 $\mathbf{Q}$ 的定义不同。在本文中，我们将坚持使用 $[\sigma]' = \mathbf{Q} [\sigma] \mathbf{Q}^T$ 的形式，其中 $Q_{ij} = \mathbf{e}'_i \cdot \mathbf{e}_j$。

作为一个应用实例，考虑一个应力张量 $[\sigma]_{\mathcal{S}}$，并将其[坐标系](@entry_id:156346)绕 $\mathbf{e}_3$ 轴旋转 $\theta = \pi/4$ [@problem_id:2625106]。变换矩阵为：
$$
\mathbf{Q} = \begin{pmatrix} \cos(\pi/4)  \sin(\pi/4)  0 \\ -\sin(\pi/4)  \cos(\pi/4)  0 \\ 0  0  1 \end{pmatrix} = \frac{1}{\sqrt{2}}\begin{pmatrix} 1  1  0 \\ -1  1  0 \\ 0  0  \sqrt{2} \end{pmatrix}
$$
使用变换法则，我们可以计算出旋转后[坐标系](@entry_id:156346)中的任意应力分量，例如 $\sigma'_{12}$。

主动变换则描述了物理对象自身的旋转。例如，我们可以考虑一个初始方向为 $\mathbf{e}_1$ 的平面，在经过一个由[旋转张量](@entry_id:191990) $\mathbf{R}$ 描述的主动旋转后，其新的[法向量](@entry_id:264185)为 $\mathbf{n} = \mathbf{R} \mathbf{e}_1$。作用在该新平面上的[法向应力](@entry_id:260622) $\sigma_n$ 就可以通过二次型 $\sigma_n = \mathbf{n}^T \boldsymbol{\sigma} \mathbf{n} = (\mathbf{R}\mathbf{e}_1)^T \boldsymbol{\sigma} (\mathbf{R}\mathbf{e}_1)$ 来计算 [@problem_id:2625102]。这展示了旋转后的向量如何与一个固定的张量场相互作用。

### [高阶张量](@entry_id:200122)的推广

张量分量的变换法则可以自然地推广到更高阶的张量。其基本原理是，张量的每个“索引”或“腿”都对应一个[基向量](@entry_id:199546)，因此在基底变换时，每个索引都需要用一个[变换矩阵](@entry_id:151616) $\mathbf{Q}$ 来进行转换。

对于一个[四阶张量](@entry_id:181350)，例如[弹性张量](@entry_id:170728) $\mathbf{C}$，其分量为 $C_{ijkl}$，变换法则涉及四个[变换矩阵](@entry_id:151616)。我们可以从物理原理出发推导这个法则，例如要求[应变能密度](@entry_id:200085)或[功率密度](@entry_id:194407) $p = \sigma_{ij}\dot{\varepsilon}_{ij}$ 在[坐标变换](@entry_id:172727)下保持不变 [@problem_id:2625099]。

在[线性弹性](@entry_id:166983)中，本构关系为 $\sigma_{ij} = C_{ijkl}\varepsilon_{kl}$。在旋转后的[坐标系](@entry_id:156346)中，此关系的形式必须保持不变：$\sigma'_{pq} = C'_{pqrs}\varepsilon'_{rs}$。我们知道[应力张量和应变张量](@entry_id:755512)都是[二阶张量](@entry_id:199780)，它们的变换遵循 $\sigma'_{pq} = Q_{pi}Q_{qj}\sigma_{ij}$ 和 $\varepsilon'_{rs} = Q_{ri}Q_{sj}\varepsilon_{ij}$。将这些关系代入旋转后的[本构方程](@entry_id:138559)，并与原始方程进行比较，经过一系列代数运算，我们可以推导出[四阶弹性张量](@entry_id:188318)的变换法则：
$$
C'_{pqrs} = Q_{pi}Q_{qj}Q_{rk}Q_{sl}C_{ijkl}
$$
这个表达式看起来很复杂，但在实践中，[材料对称性](@entry_id:190289)（如[正交各向异性](@entry_id:196967)）会使大量的 $C_{ijkl}$ 分量为零，从而简化计算。例如，对于一个初始沿坐标轴方向的[正交各向异性材料](@entry_id:190111)，在绕 $\mathbf{e}_3$ 轴旋转 $30^{\circ}$ 后，新的刚度分量 $C'_{1111}$ 将是原始分量 $C_{1111}$, $C_{2222}$, $C_{1122}$ 和 $C_{1212}$ 的特定组合，其系数是旋转角度的正弦和余弦的[幂函数](@entry_id:166538) [@problem_id:2625099]。

### [曲线坐标系](@entry_id:172561)中的变换

在许多工程问题中（例如圆柱壳或球形压力容器），使用[曲线坐标系](@entry_id:172561)（如[柱坐标](@entry_id:271645)或[球坐标](@entry_id:146054)）比[笛卡尔坐标系](@entry_id:169789)更为方便。在[曲线坐标系](@entry_id:172561)中，[基向量](@entry_id:199546)本身不再是常数，而是空间位置的函数。这引入了新的概念，如**[协变](@entry_id:634097)**（covariant）和**逆变**（contravariant）[基向量](@entry_id:199546)和张量分量。

给定一个从[曲线坐标](@entry_id:178535) $q^\alpha$ 到[笛卡尔坐标](@entry_id:167698) $x^i$ 的映射 $\mathbf{x}(q^1, q^2, q^3)$，我们定义**[协变基](@entry_id:198968)向量**为：
$$
\mathbf{g}_\alpha = \frac{\partial \mathbf{x}}{\partial q^\alpha}
$$
这些[基向量](@entry_id:199546)是[局部坐标](@entry_id:181200)曲线的[切线](@entry_id:268870)方向。例如，在[柱坐标系](@entry_id:266798) $(r, \theta, z)$ 中，$\mathbf{g}_\theta = \partial\mathbf{x}/\partial\theta = -r\sin\theta\,\mathbf{e}_x + r\cos\theta\,\mathbf{e}_y$ [@problem_id:2625101]。

有了[局部基向量](@entry_id:163370)，二阶张量 $\mathbf{T}$ 的**协变分量** $T_{\alpha\beta}$ 定义为张量与[基向量](@entry_id:199546)的双线性作用：
$$
T_{\alpha\beta} = \mathbf{g}_\alpha \cdot \mathbf{T}(\mathbf{g}_\beta)
$$
这个定义为我们提供了一个从笛卡尔分量计算[曲线坐标](@entry_id:178535)分量的方法。例如，要计算应力张量 $\boldsymbol{\sigma}$ 的协变分量 $\sigma_{\theta\theta}$，我们只需计算 $\sigma_{\theta\theta} = \mathbf{g}_\theta \cdot (\boldsymbol{\sigma} \mathbf{g}_\theta)$。这个计算过程需要在笛卡尔坐标系中表示所有向量和张量，进行[矩阵向量乘法](@entry_id:140544)和[点积](@entry_id:149019)运算，最后得到所需的分量值 [@problem_id:2625101]。

更一般地，不同[坐标系](@entry_id:156346)（例如，笛卡尔坐标系 $x^i$ 和另一个[坐标系](@entry_id:156346) $\bar{x}^a$）中张量分量之间的变换由[雅可比矩阵](@entry_id:264467)（Jacobian matrices）$\partial x^i / \partial \bar{x}^a$ 控制。例如，一个二阶[协变张量](@entry_id:634493) $T$ 的分量变换法则为：
$$
\bar{T}_{ab} = T_{ij} \frac{\partial x^i}{\partial \bar{x}^a} \frac{\partial x^j}{\partial \bar{x}^b}
$$
这个通用法则适用于任何[坐标系](@entry_id:156346)之间的转换，包括从笛卡尔坐标到极坐标的转换。例如，给定[笛卡尔坐标系](@entry_id:169789)下的[逆变分量](@entry_id:185440) $T^{ij}$，我们可以首先使用度量张量 $g_{ij}$ 将其降低指标得到协变分量 $T_{ij} = g_{ik}g_{jl}T^{kl}$（在标准笛卡尔坐标系中 $g_{ij}=\delta_{ij}$，所以 $T_{ij}=T^{ij}$），然后应用上述变换法则计算出在极[坐标系](@entry_id:156346)中的[协变](@entry_id:634097)分量 $T_{\theta\theta}$ [@problem_id:2625087]。

### [非线性](@entry_id:637147)[连续介质力学](@entry_id:155125)中的变换

在处理[大变形](@entry_id:167243)问题时，我们不仅要考虑[坐标系](@entry_id:156346)的旋转，还要考虑材料本身的变形。描述这种变形的核心工具是**变形梯度张量**（deformation gradient tensor） $\mathbf{F}$。它定义为当前构形中的位置向量 $\mathbf{x}$ 相对于参考构形中位置向量 $\mathbf{X}$ 的梯度：
$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}
$$
$\mathbf{F}$ 将参考构形中的一个微元线段映射到当前构形中的对应线段。

由于材料点在变形过程中移动，我们需要在两个不同的构形（参考构形和当前构形）之间建立联系。这导致了不同[应力张量](@entry_id:148973)的定义：
- **柯西应力张量**（Cauchy stress）$\boldsymbol{\sigma}$：定义在当前构形上，是“真实”的物理应力。
- **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量**（Second Piola-Kirchhoff stress, PK2）$\mathbf{S}$：定义在参考构形上，与[应变能](@entry_id:162699)共轭，对于描述材料[本构关系](@entry_id:186508)非常方便。

这两个张量之间的关系是通过变形梯度 $\mathbf{F}$ 建立的。从力平衡和面积微元变换关系（Nanson 公式）出发，可以推导出联系 $\boldsymbol{\sigma}$ 和 $\mathbf{S}$ 的重要关系式 [@problem_id:2625085] [@problem_id:2625103]：
$$
\boldsymbol{\sigma} = \frac{1}{J} \mathbf{F} \mathbf{S} \mathbf{F}^T
$$
其中 $J = \det(\mathbf{F})$ 是体积变化率。这个操作被称为从参考构形到当前构形的**推前**（push-forward）操作。反之，将张量从当前构形映射回参考构形称为**[拉回](@entry_id:160816)**（pull-back）操作。这个关系式是有限元分析等[计算力学](@entry_id:174464)方法中进行应力更新的基础。在等参元公式中，变形梯度 $\mathbf{F}$ 本身可以通过对父单元坐标的雅可比矩阵 $\mathbf{J}_x = \partial\mathbf{x}/\partial\boldsymbol{\xi}$ 和 $\mathbf{J}_X = \partial\mathbf{X}/\partial\boldsymbol{\xi}$ 来计算，即 $\mathbf{F} = \mathbf{J}_x \mathbf{J}_X^{-1}$ [@problem_id:2625103]。

### 客观性与张量的时间导数

在建立描述材料行为随[时间演化](@entry_id:153943)的本构模型时，我们经常需要用到应力张量的时间导数。然而，一个直接的问题出现了：标准的[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ 并不是一个**客观**（objective）的量。这意味着它的值依赖于观察者的刚体旋转运动。

**物质[标架无关性原理](@entry_id:200995)**（Principle of Material Frame-Indifference），或称[客观性原理](@entry_id:185412)，要求[本构方程](@entry_id:138559)在所有刚体运动的观察者看来都具有相同的形式。为了满足这一原理，我们需要定义一个客观的应力率，它能够从 $\dot{\boldsymbol{\sigma}}$ 中移除观察者旋转所带来的非客观部分。

一种常用的[客观率](@entry_id:198692)是**[共旋应力率](@entry_id:747894)**（corotational stress rate），也称为 **[Jaumann 率](@entry_id:185572)**，记作 $\stackrel{\circ}{\boldsymbol{\sigma}}$。它通过引入**[自旋张量](@entry_id:187346)**（spin tensor）$\mathbf{W}$ 来修正[物质导数](@entry_id:172646)。[自旋张量](@entry_id:187346)是[速度梯度](@entry_id:261686) $\mathbf{L} = \partial\mathbf{v}/\partial\mathbf{x}$ 的反对称部分，$\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$，它描述了材料微元的瞬时旋转速率。

[Jaumann 率](@entry_id:185572)的定义为 [@problem_id:2625095]：
$$
\stackrel{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W}
$$
可以证明，如此定义的 $\stackrel{\circ}{\boldsymbol{\sigma}}$ 是一个客观张量，即在叠加了一个刚体旋转运动后，它能像一个普通的[二阶张量](@entry_id:199780)那样变换。直观地看，[Jaumann 率](@entry_id:185572)衡量的是在一个与材料一同旋转的（共旋）标架中观察到的应力变化率。

在实际计算中，我们首先根据给定的速度梯度 $\mathbf{L}$ 计算出[自旋张量](@entry_id:187346) $\mathbf{W}$，然后利用上述公式计算出 [Jaumann 率](@entry_id:185572)张量的分量。一旦得到了[客观率](@entry_id:198692)张量 $\stackrel{\circ}{\boldsymbol{\sigma}}$，它就可以像任何其他二阶张量一样，使用我们之前讨论过的法则进行[坐标变换](@entry_id:172727)，例如，计算其在另一个[旋转坐标系](@entry_id:170324)中的分量 [@problem_id:2625095]。

总之，张量[坐标变换](@entry_id:172727)是[连续介质力学](@entry_id:155125)的基石。无论是在简单的刚体旋转、复杂的[曲线坐标系](@entry_id:172561)，还是在有限变形和随[时间演化](@entry_id:153943)的过程中，理解和掌握这些变换法则是正确应用力学原理和建立有效本构模型的关键。