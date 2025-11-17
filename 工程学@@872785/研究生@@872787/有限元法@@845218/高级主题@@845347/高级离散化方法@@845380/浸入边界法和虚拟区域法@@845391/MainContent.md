## 引言
模拟包含复杂几何形状或大规模移动边界的物理问题，是计算科学与工程领域长期面临的挑战。传统的体合网格方法要求网格边界与物理边界完全贴合，当几何发生变形或移动时，高质量网格的重新生成往往成为整个计算流程的性能瓶颈。为了摆脱这一束缚，[浸入边界法](@entry_id:174123)（Immersed Boundary, IB）与[虚拟区域法](@entry_id:178677)（Fictitious Domain, FD）等[非贴体网格](@entry_id:168901)方法应运而生。其核心思想是：在一个固定的、结构简单的背景网格上求解控制方程，而将复杂几何“浸入”其中，通过特殊的数学方法处理[界面条件](@entry_id:750725)。这极大地简化了前处理工作，并为动态界面问题提供了高效、灵活的数值框架。

本文旨在对[浸入边界法](@entry_id:174123)和[虚拟区域法](@entry_id:178677)进行系统性的深入探讨，揭示其背后的数学原理、数值实现的关键技术以及在多学科交叉领域的应用。文章将不仅区分两类方法在哲学思想上的根本差异，还将深入分析它们在实际应用中遇到的挑战与前沿解决方案，为读者构建一个完整的知识体系。

在接下来的章节中，您将学习到：
*   **原理与机制**：我们将首先剖析两类方法的核心思想，即弥散界面与锐利界面的区别，详细阐述经典[浸入边界法](@entry_id:174123)的欧拉-拉格朗日耦合机制，以及[虚拟区域法](@entry_id:178677)中用于施加边界约束的[Nitsche方法](@entry_id:175793)等关键技术。此外，还会探讨小切割[单元稳定化](@entry_id:175935)、质量守恒等高级数值问题。
*   **应用与跨学科[交叉](@entry_id:147634)**：随后，我们将展示这些方法在[流体动力学](@entry_id:136788)、[流固耦合](@entry_id:171183)、[生物力学](@entry_id:153973)等领域的广泛应用。通过具体案例，如[多相流模拟](@entry_id:752305)、轻质结构[附加质量效应](@entry_id:746267)和纤维[网络动力学](@entry_id:268320)，揭示这些方法在解决真实世界问题时的强大能力。
*   **动手实践**：最后，本部分将通过一系列精心设计的问题，引导读者思考如何实现切割单元求积、验证[流固耦合](@entry_id:171183)代码的准确性，并将理论知识应用于解决一个经典的[流体动力学](@entry_id:136788)问题，从而巩固和深化所学内容。

## 原理与机制

处理含复杂或[移动边界问题](@entry_id:170533)的传统数值方法，如体合网格（body-fitted meshing），通常需要生成与几何边界完全贴合的网格。当边界几何形状复杂或在仿真过程中发生显著变形时，重复生成高质量的体合网格可能极其耗时，甚至成为整个计算流程的瓶颈。为了克服这一挑战，计算科学家发展了一系列[非贴体网格](@entry_id:168901)方法（unfitted mesh methods），其核心思想是在一个固定的、简单的背景网格上求解控制方程，而无需让网格与内部的几何边界对齐。[浸入边界法](@entry_id:174123)（Immersed Boundary, IB）和[虚拟区域法](@entry_id:178677)（Fictitious Domain, FD）是这类方法中最具[代表性](@entry_id:204613)的两大家族。本章将深入探讨这些方法的内在原理与核心机制。

### 两种核心思想：弥散界面与锐利界面

尽管都旨在避免使用[贴体网格](@entry_id:746935)，但浸入式方法大体上遵循两种截然不同的哲学思想，其根本区别在于如何表示和处理浸入的界面 [@problem_id:2567777]。

第一种是**弥散界面（diffuse-interface）**方法，其典型代表是经典的**[浸入边界法](@entry_id:174123)（Immersed Boundary Method, IBM）**。在这种[范式](@entry_id:161181)中，流体与结构之间的界面被视为一个在流体区域内施加局部体积力的源。界面本身在计算网格上没有一个无限薄的、锐利的几何表示，而是被“弥散”到一个厚度与网格尺寸相当的薄层中。界面上的力（例如，弹性力或[膜张力](@entry_id:153270)）通过一个光滑的核函数[分布](@entry_id:182848)到周围的流体节点上，从而在动量方程中表现为一个连续但高度集中的[体力](@entry_id:174230)项。相应地，流体速度对界面运动的约束也是通过在同一个弥散层内进行速度插值来实现的。

第二种是**锐利界面（sharp-interface）**方法，这一范畴包括了广义的**[虚拟区域法](@entry_id:178677)（Fictitious Domain Methods, FDM）**、**[切割有限元法](@entry_id:163318)（Cut Finite Element Method, [CutFEM](@entry_id:163318)）**以及相关的技术。这类方法在概念上将浸入的边界$\Gamma$视为一个精确的几何实体。即使$\Gamma$切割了背景网格单元，控制方程的积分区域也严格限制在物理域$\Omega$内，并且边界条件被明确地施加在精确的界面$\Gamma$上。这种处理方式保留了界面的“锐利”特性，允许在界面两侧的物理量（如压力或应力）存在不连续性。其核心挑战在于如何在不与网格对齐的界面上稳定且准确地施加这些边界条件。

总的来说，这两种方法的根本区别在于 [@problem_id:2567711]：
- **[浸入边界法](@entry_id:174123)**将[流体方程](@entry_id:195729)扩展到包含固体的整个计算域，并通过一个定义在界面上的拉格朗日力与欧拉流场耦合的体力项来弱化地施加[界面条件](@entry_id:750725)。
- **虚拟区域/锐利界面法**同样将方程扩展到整个计算域，但它们通过在固体区域或其边界上施加严格的[运动学](@entry_id:173318)约束来处理界面。这些约束可以通过拉格朗日乘子法、[罚函数法](@entry_id:636090)或[Nitsche方法](@entry_id:175793)等多种技巧来实现。

接下来，我们将分别深入探讨这两种方法的机制。

### [浸入边界法](@entry_id:174123)：欧拉-拉格朗日耦合机制

经典的[浸入边界法](@entry_id:174123)由Charles Peskin开创，用于模拟心脏瓣膜的血流动力学。其核心是一种精妙的**欧拉-拉格朗日耦合（Eulerian-Lagrangian coupling）**机制。[流体动力学](@entry_id:136788)方程（如[Navier-Stokes方程](@entry_id:161487)）在固定的欧拉[坐标系](@entry_id:156346)下的背景网格上求解，而浸入的弹性结构则由一组离散的[拉格朗日点](@entry_id:142288)来描述。两者之间的相互作用通过力的“散播”（spreading）和速度的“插值”（interpolation）来完成。

#### 力的散播与速度的插值

想象一个[浸入](@entry_id:161534)在流体中的弹性纤维，它被离散成一系列由拉格朗日坐标$s$参数化的点$\boldsymbol{X}(s,t)$。在每一个[拉格朗日点](@entry_id:142288)上，我们可以根据其位置计算出弹性力密度$\boldsymbol{F}(s,t)$。为了让流体“感受”到这个力，我们需要将这个定义在[拉格朗日点](@entry_id:142288)上的力转化为定义在欧拉网格上的体力场$\boldsymbol{f}(\boldsymbol{x},t)$。这个过程被称为**力的散播**。

反之，[浸入](@entry_id:161534)的结构必须以其所在位置的局部流体速度运动（即[无滑移条件](@entry_id:275670)）。这意味着我们需要知道在每个[拉格朗日点](@entry_id:142288)$\boldsymbol{X}(s,t)$处的流体速度。然而，我们的[流体速度](@entry_id:267320)$\boldsymbol{u}(\boldsymbol{x},t)$是定义在欧拉网格节点上的。因此，我们需要根据周围欧拉节点上的速度值来计算[拉格朗日点](@entry_id:142288)处的速度$\boldsymbol{U}(s,t)$。这个过程被称为**速度的插值**。

这两个过程构成了[浸入边界法](@entry_id:174123)的核心循环：
1.  **插值**：计算结构在当前位置的运动速度$\boldsymbol{U}$，这通过插值周围的欧拉流场$\boldsymbol{u}$得到。
2.  **计算力**：根据结构当前构型（由$\boldsymbol{X}$给出）以及其目标状态，计算出拉格朗日力$\boldsymbol{F}$。在某些反馈力模型中，$\boldsymbol{F}$也可能依赖于插值速度$\boldsymbol{U}$与结构自身速度的差异。
3.  **散播力**：将拉格朗日力$\boldsymbol{F}$散播到欧拉网格上，形成体力项$\boldsymbol{f}$。
4.  **求解流场**：求解包含[体力](@entry_id:174230)项$\boldsymbol{f}$的[流体动力学](@entry_id:136788)方程，更新欧拉流场$\boldsymbol{u}$和压力$p$。
5.  **更新结构位置**：根据插值得到的速度$\boldsymbol{U}$，更新[拉格朗日点](@entry_id:142288)的位置$\boldsymbol{X}$。

#### 正则化狄拉克Delta函数

实现散播和插值的数学工具是**正则化狄拉克Delta函数**（regularized Dirac delta function），记作$\delta_h$（或$\delta_\epsilon$），其中$h$是网格尺寸。这是一个光滑的、具有[紧支集](@entry_id:276214)的函数，它在积分意义上逼近了理想的狄拉克$\delta$函数。

根据$\delta$函数的采样特性，一个点$\boldsymbol{X}$处的函数值可以表示为$u(\boldsymbol{X}) = \int u(\boldsymbol{x})\delta(\boldsymbol{x}-\boldsymbol{X})d\boldsymbol{x}$。在[浸入边界法](@entry_id:174123)中，无滑移条件的运动学约束正是基于此原理来施加的。[拉格朗日点](@entry_id:142288)的速度$\boldsymbol{U}(s,t)$被设定为通过正则化$\delta_h$函数插值得到的局部流体速度 [@problem_id:2567770]：
$$
\boldsymbol{U}(s,t) = \int_{\Omega} \boldsymbol{u}(\boldsymbol{x},t)\,\delta_h(\boldsymbol{x} - \boldsymbol{X}(s,t))\,d\boldsymbol{x}
$$
在离散形式下，这个积分变成一个求和：
$$
\boldsymbol{U}(\boldsymbol{X}) = \sum_{i} \boldsymbol{u}(\boldsymbol{x}_i)\,\delta_h(\boldsymbol{x}_i-\boldsymbol{X})\,h^d
$$
其中$\boldsymbol{x}_i$是欧拉网格节点，$h^d$是网格单元的体积。

类似地，力的散播操作将定义在[拉格朗日点](@entry_id:142288)$\boldsymbol{X}(s)$上的力密度$\boldsymbol{F}(s)$转化为欧拉网格上的[体力](@entry_id:174230)场$\boldsymbol{f}(\boldsymbol{x})$ [@problem_id:2567777]：
$$
\boldsymbol{f}(\boldsymbol{x}) = \int_{\Gamma} \boldsymbol{F}(s) \, \delta_h\left(\boldsymbol{x} - \boldsymbol{X}(s)\right) \, ds
$$
离散形式为：
$$
\boldsymbol{f}(\boldsymbol{x}_i) = \sum_{q} \boldsymbol{F}(\boldsymbol{X}_q)\,\delta_h(\boldsymbol{x}_i-\boldsymbol{X}_q)\,\Delta V_q
$$
其中$\boldsymbol{X}_q$是离散的[拉格朗日点](@entry_id:142288)，$\Delta V_q$是其对应的体积或面积权重。这两个算子在离散意义下是互为伴随的，这保证了[能量守恒](@entry_id:140514)。

#### [核函数](@entry_id:145324)的[矩条件](@entry_id:136365)

为了保证[浸入边界法](@entry_id:174123)的精度和稳定性，正则化Delta函数$\delta_h$（或其无量纲形式$\phi(r)=\delta_h(rh)h$）必须满足一系列**[矩条件](@entry_id:136365)**（moment conditions）[@problem_id:2567780]。这些条件确保了在耦合过程中，一些基本物理量（如力和力矩）能够被准确地传递。

对于一个光滑的欧拉场$u(\boldsymbol{x})$，其在[拉格朗日点](@entry_id:142288)$\boldsymbol{X}$的[插值误差](@entry_id:139425)可以通过泰勒展开来分析。为了使插值至少达到[一阶精度](@entry_id:749410)（即对于线性的速度场[插值误差](@entry_id:139425)为$O(h^2)$），核函数必须满足以下离散[矩条件](@entry_id:136365)：

- **零阶[矩条件](@entry_id:136365)（Partition of Unity）**:
$$
M^{(0)}(\boldsymbol{X}) = \sum_{i} \delta_h(\boldsymbol{x}_i-\boldsymbol{X})\,h^d = 1
$$
这个条件保证了一个常数场能够被精确地插值，也确保了力的总和在散播过程中是守恒的。

- **一阶[矩条件](@entry_id:136365)**:
$$
\boldsymbol{M}^{(1)}(\boldsymbol{X}) = \sum_{i} (\boldsymbol{x}_i-\boldsymbol{X})\,\delta_h(\boldsymbol{x}_i-\boldsymbol{X})\,h^d = \boldsymbol{0}
$$
这个条件保证了一个线性场能够被精确插值（至$O(h^2)$），并且确保了力矩在散播过程中是守恒的。

- **二阶[矩条件](@entry_id:136365)**:
$$
\mathsf{M}^{(2)}(\boldsymbol{X}) = \sum_{i} (\boldsymbol{x}_i-\boldsymbol{X})\otimes(\boldsymbol{x}_i-\boldsymbol{X})\,\delta_h(\boldsymbol{x}_i-\boldsymbol{X})\,h^d = C\mathsf{I}
$$
为了获得更好的数值特性，例如使[插值误差](@entry_id:139425)的领先项不依赖于[拉格朗日点](@entry_id:142288)在网格内的子格点位置（grid-translation invariance），通常要求二阶矩张量$\mathsf{M}^{(2)}$是一个与$\boldsymbol{X}$无关的常数张量。为了消除方向偏差（各向同性），这个张量应该是一个标量$C$与单位矩阵$\mathsf{I}$的乘积。

一个满足这些条件的经典例子是Peskin的4点[核函数](@entry_id:145324)。在无量纲坐标$r=x/h$下，其一维形式为 [@problem_id:2567668]：
$$
\phi(r) = 
\begin{cases}
\frac{1}{2} - \frac{1}{4}r^{2}, & |r| \le 1 \\
\frac{1}{4}(2-|r|)^{2}, & 1  |r| \le 2 \\
0,  |r| > 2
\end{cases}
$$
这个函数是$C^1$连续的，具有[紧支集](@entry_id:276214)$[-2, 2]$，并且被构造成能够满足上述零阶和一阶[矩条件](@entry_id:136365)。多维核函数通常通过一维[核函数](@entry_id:145324)的张量积来构造。

### [虚拟区域法](@entry_id:178677)与[切割有限元法](@entry_id:163318)：锐利界面约束

与[浸入边界法](@entry_id:174123)不同，[虚拟区域法](@entry_id:178677)（FDM）和[切割有限元法](@entry_id:163318)（[CutFEM](@entry_id:163318)）将界面$\Gamma$视为一个几何上精确的边界。这些方法的核心是在一个简单的背景网格上求解覆盖整个物理域和部分“虚拟”域的方程，同时通过特殊技术在$\Gamma$上施加边界条件。

#### 约束施加方法

假设我们需要在[浸入](@entry_id:161534)的边界$\Gamma$上施加一个狄氏边界条件，例如$\boldsymbol{u} = \boldsymbol{g}$。由于背景网格的节点通常不在$\Gamma$上，我们无法像传统有限元方法那样通过简单地固定节点值来强加此条件。以下是几种主流的弱约束施加技术。

##### 1. 体积罚函数法（Brinkman罚函数法）

这是一种在[虚拟区域法](@entry_id:178677)中常用的技术。其思想是，在被固体占据的区域$\Omega_s$内，通过向[动量方程](@entry_id:197225)添加一个[罚函数](@entry_id:638029)项来强制流体速度$\boldsymbol{u}$趋近于指定的固体速度$\boldsymbol{u}_b$ [@problem_id:2567665]。被惩罚的[Stokes方程](@entry_id:196346)的强形式可以写为：
$$
-\nabla \cdot \boldsymbol{\sigma}(\boldsymbol{u}, p) + \frac{1}{\eta}\chi(x)(\boldsymbol{u} - \boldsymbol{u}_b) = \boldsymbol{f} \quad \text{in } \Omega
$$
$$
\nabla \cdot \boldsymbol{u} = 0 \quad \text{in } \Omega
$$
其中，$\eta$是一个很小的罚参数（$\eta \to 0$），$\chi(x)$是一个[指示函数](@entry_id:186820)，它在固体区域$\Omega_s$内取值为1，在流体区域$\Omega_f$内取值为0。当$\eta$非常小时，为了使方程有界，必须有$\boldsymbol{u} \approx \boldsymbol{u}_b$在$\Omega_s$内成立。这个[罚函数](@entry_id:638029)项在[弱形式](@entry_id:142897)中表现为一个体积积分：
$$
\frac{1}{\eta}\int_{\Omega_s} (\boldsymbol{u} - \boldsymbol{u}_b) \cdot \boldsymbol{v} \,dx
$$
这种方法的优点是实现简单，因为它只在标准弱形式上增加了一个体积积分项。然而，它也存在一些缺点 [@problem_id:2567663]：
- **不一致性**：对于任何有限的$\eta$，该方法引入了一个[建模误差](@entry_id:167549)。它实际上施加的是一个Robin型边界条件，只有在$\eta \to 0$的极限下才恢复为狄氏条件。
- **病态条件数**：罚参数$\eta$的减小虽然能提高精度，但会导致系统[矩阵的条件数](@entry_id:150947)急剧恶化（通常是$O(1/\eta)$），给代数求解器带来巨大挑战。

##### 2. 拉格朗日乘子法

这是一种更严格的约束施加方法。它引入一个新的未知场——拉格朗日乘子$\boldsymbol{\lambda}$——定义在界面$\Gamma$上（或者在体积$\Omega_s$上）。这个乘子在物理上可以解释为维持约束所需的力。通过引入乘子，原始的最小化问题变成了一个[鞍点问题](@entry_id:174221)。

例如，要在$\Gamma$上施加$\boldsymbol{u}=\boldsymbol{g}$，[弱形式](@entry_id:142897)会包含一个耦合项$\int_{\Gamma} \boldsymbol{\lambda} \cdot \boldsymbol{v} \,ds$和一个约束方程$\int_{\Gamma} \boldsymbol{\mu} \cdot (\boldsymbol{u}-\boldsymbol{g}) \,ds = 0$，其中$\boldsymbol{\mu}$是乘[子空间](@entry_id:150286)的测试函数。这种方法 [@problem_id:2567663]：
- **是一致的**：它没有引入[建模误差](@entry_id:167549)，其连续形式精确地等价于原始问题。乘子$\boldsymbol{\lambda}$通常可以解释为界面上的法向应力（法向通量）。
- **导致[鞍点问题](@entry_id:174221)**：最终的代数系统是一个不定号的[鞍点系统](@entry_id:754480)，需要使用专门的求解器。
- **需要满足[LBB条件](@entry_id:746626)**：为了保证稳定，速度和乘子的离散空间必须满足Ladyzhenskaya–Babuška–Brezzi（LBB）稳定条件。在[非贴体网格](@entry_id:168901)上，要构造满足[LBB条件](@entry_id:746626)的稳定单元对非常困难，尤其是在存在任意切割单元的情况下。

为了克服[LBB条件](@entry_id:746626)的限制，**[增广拉格朗日法](@entry_id:170637)**（Augmented Lagrangian Method）被提出。它结合了[拉格朗日乘子](@entry_id:142696)和[罚函数法](@entry_id:636090)的思想，通过在拉格朗日函数中增加一个约束残差的惩罚项（如$\frac{\gamma}{2}\int_\Gamma (\boldsymbol{u}-\boldsymbol{g})^2 ds$）来改善系统的稳定性和条件数，同时保持方法的一致性 [@problem_id:2567663]。

##### 3. [Nitsche方法](@entry_id:175793)

[Nitsche方法](@entry_id:175793)是一种特别强大和灵活的技术，用于在不引入新变量的情况下弱施加狄氏边界条件。它最初为[贴体网格](@entry_id:746935)设计，后被广泛应用于[非贴体网格](@entry_id:168901)场景 [@problem_id:2567747]。对于标量[扩散](@entry_id:141445)问题$-\nabla \cdot (\mu \nabla u) = f$和边界条件$u=g$，对称[Nitsche方法](@entry_id:175793)的弱形式通过在标准[弱形式](@entry_id:142897)的基础上增加三个边界积分项来构建：

$$
a_h(u,v) = \int_{\Omega} \mu \nabla u \cdot \nabla v \, dx \underbrace{- \int_{\Gamma_D} \mu (\partial_n u)\, v \, ds}_{\text{一致性项}} \underbrace{- \int_{\Gamma_D} \mu (\partial_n v)\, u \, ds}_{\text{对称性项}} + \underbrace{\int_{\Gamma_D} \frac{\gamma_N \mu}{h_\Gamma}\, u\, v \, ds}_{\text{罚函数/稳定项}}
$$
$$
\ell_h(v) = \int_{\Omega} f\, v \, dx \underbrace{- \int_{\Gamma_D} \mu (\partial_n v)\, g \, ds}_{\text{来自对称项}} + \underbrace{\int_{\Gamma_D} \frac{\gamma_N \mu}{h_\Gamma}\, g\, v \, ds}_{\text{来自稳定项}}
$$

- **一致性项**：自然地由[分部积分](@entry_id:136350)产生，保证了当精确解代入时方程成立。
- **对称性项**：为了使[双线性形式](@entry_id:746794)$a_h(u,v)$对称而添加。
- **稳定项**：一个惩罚项，用于补偿对称项带来的矫顽性损失，从而保证整个系统的稳定性。罚参数$\gamma_N$必须足够大，其缩放因子$\mu/h_\Gamma$对于保证稳定性和鲁棒性至关重要。

[Nitsche方法](@entry_id:175793)是一致的，并且产生的代数系统是正定的，避免了[鞍点问题](@entry_id:174221)。这使得它在[CutFEM](@entry_id:163318)等现代非贴体方法中备受青睐。

### 关键数值挑战及高级主题

无论是[浸入边界法](@entry_id:174123)还是[虚拟区域法](@entry_id:178677)，当它们应用于[非贴体网格](@entry_id:168901)时，都会面临一些独特的数值挑战。

#### 小切割单元问题与稳定性

对于锐利界面方法（如[CutFEM](@entry_id:163318)），一个核心的挑战是**小切割单元问题**（small cut-cell problem）。当背景网格单元被界面切割成一个体积非常小的子单元时，标准的有限元分析理论可能会失效 [@problem_id:2567663]。

为了具体理解这个问题，我们考虑一个二维$Q_1$（[双线性](@entry_id:146819)）单元被切割成一个体积份额为$\theta \ll 1$的薄带区域 [@problem_id:2567727]。在该切割单元上计算的局部质量矩阵$M$和刚度矩阵$K$会表现出病态行为。
- **局部[质量矩阵](@entry_id:177093)**：其不同项的缩放行为会截然不同。靠近流体区域的[基函数](@entry_id:170178)对应的对角元$M_{ii}$与$\theta$成正比，而远离的[基函数](@entry_id:170178)（其值在薄带上很小）对应的对角元则可能与$\theta^3$成正比。这导致局部质量矩阵的条件数$\kappa(M)$会像$\theta^{-2}$一样爆炸。
- **局部[刚度矩阵](@entry_id:178659)**：虽然局部[刚度矩阵](@entry_id:178659)本身可能是良态的（其所有项大致都与$\theta$成正比），但在组装到[全局刚度矩阵](@entry_id:138630)后会引发问题。一个主要由这种“小刚度”单元支撑的自由度，其在[全局刚度矩阵](@entry_id:138630)中的对角元大小约为$O(\theta)$，而位于实体区域的自由度对应的对角元则为$O(1)$。这种对角元[数量级](@entry_id:264888)的巨大差异导致[全局刚度矩阵](@entry_id:138630)的[条件数](@entry_id:145150)恶化，其恶化程度约为$O(\theta^{-1})$。

这种病态条件数不仅拖慢了[迭代求解器](@entry_id:136910)的收敛速度，还会严重污染数值解的精度。为了解决这个问题，必须引入**稳定化**技术。

#### 稳定化技术：[鬼点](@entry_id:177889)罚函数法

**[鬼点](@entry_id:177889)罚函数法**（Ghost Penalty Method）是解决小切割单元问题的一种有效稳定化策略 [@problem_id:2567663]。其核心思想是，在切割单元周围的“[鬼点](@entry_id:177889)区域”（即位于虚拟域一侧的单元部分）内，通过惩罚解在相邻单元间[法向导数](@entry_id:169511)的跳跃来施加额外的控制。

这种方法在切割单元及其邻近单元所构成的面片内部的所有内侧面$F \in \mathcal{F}_G$上添加一个稳定项$G_h$。对于[Stokes问题](@entry_id:755479)，这个稳定项需要同时控制速度和压力。其通用形式为一系列[法向导数](@entry_id:169511)跳跃的积分之和 [@problem_id:2567761]：
$$
G_{h}\big((\boldsymbol{u}_{h},p_{h}),(\boldsymbol{v}_{h},q_{h})\big) = \sum_{F \in \mathcal{F}_{G}} \int_{F} \sum_{m=0}^{k} \left( \gamma_{u} h^{2m-1} [\partial_{n}^{m}\boldsymbol{u}_{h}] \cdot [\partial_{n}^{m}\boldsymbol{v}_{h}] + \gamma_{p} h^{2m+1} [\partial_{n}^{m}p_{h}] [\partial_{n}^{m}q_{h}] \right) dS
$$
其中，$k$是多项式次数，$[\cdot]$表示面上的跳跃，$\partial_n^m$表示$m$阶[法向导数](@entry_id:169511)。
- 速度稳定项的缩放因子$h^{2m-1}$旨在控制速度的$H^1$[半范数](@entry_id:264573)。
- 压力稳定项的缩放因子$h^{2m+1}$旨在控制压力的$L^2$范数。

这些精心设计的缩放因子确保了稳定项与物理能量项的量纲一致，并且对于高阶[多项式逼近](@entry_id:137391)是鲁棒的。通过这种方式，[鬼点](@entry_id:177889)罚函数有效地将切割单元内的自由度与邻近的“健康”单元耦合起来，从而恢复了整个系统的稳定性和[矫顽性](@entry_id:159399)。

#### [浸入边界法](@entry_id:174123)中的[质量守恒](@entry_id:204015)问题

在经典的[浸入边界法](@entry_id:174123)中，尽管全局[质量守恒](@entry_id:204015)是以[弱形式](@entry_id:142897)施加的，但在界面附近常常会观察到显著的局部**质量不守恒**现象，即$\nabla \cdot \boldsymbol{u}_h \neq 0$ [@problem_id:2567704]。这种“界面泄漏”是一个众所周知的数值伪影。

其根本原因在于，标准[混合有限元](@entry_id:178533)方法仅以[弱形式](@entry_id:142897)（即在与离散压力空间正交的意义下）保证无散。当一个高度集中的、近似奇异的[界面力](@entry_id:184024)$\boldsymbol{f}_\Gamma$被引入动量方程时，它会诱导出同样奇异的压力梯度（在连续层面上有$\Delta p = \nabla \cdot \boldsymbol{f}_\Gamma$）。离散的多项式压力空间无法精确捕捉这种尖锐的压力变化。压力近似的误差会通过离散[动量方程](@entry_id:197225)“污染”速度场，导致离散速度场$\boldsymbol{u}_h$的散度局部不为零，以在离散意义下平衡动量。

为了恢复局部的[质量守恒](@entry_id:204015)，需要采用更强的[无散约束](@entry_id:755035)。有两种主要途径：
1.  **使用精确无散的有限元空间**：选择特定的有限元速度-压力对，使得离散[速度空间](@entry_id:181216)中任意函数都逐单元地满足[无散条件](@entry_id:755034)（$\nabla \cdot \boldsymbol{u}_h|_T = 0$）。例如，在特定的[重心](@entry_id:273519)加密单纯形网格上使用Scott–Vogelius单元（当多项式次数$k \geq d$时）可以达到此目的。
2.  **投影方法**：采用一个两步算法。首先，求解一个不包含压力项的[动量方程](@entry_id:197225)得到一个中间速度场$\tilde{\boldsymbol{u}}_h$。然后，通过求解一个离散的[亥姆霍兹-霍奇分解](@entry_id:140525)问题，将$\tilde{\boldsymbol{u}}_h$投影到精确无散的[子空间](@entry_id:150286)上。这个投影步骤通常在$H(\text{div})$协调的有限元空间（如Raviart–Thomas或Brezzi–Douglas–Marini单元）中进行，因为这些空间的设计保证了离散[散度算子](@entry_id:265975)的满射性，从而可以构造出$\nabla \cdot \boldsymbol{u}_h = 0$的解。

通过这些方法，可以从根本上消除由弱约束和奇异力源共同导致的界面泄漏问题。