## 引言
波的行为——从在晶体原子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中穿行的电子到穿过经工程设计的光学材料的光——都受复杂的原理支配。预测这种行为是现代物理学和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的基石，然而，在周期性环境中直接求解其底层的波方程会带来巨大的计算挑战。这一困难在基本定律和我们设计具有特定性质的材料与器件的能力之间造成了知识鸿沟。本文将揭示为弥合这一鸿沟而开发出的最强大的计算工具之一：[平面波展开法](@keyword=plane_wave_expansion_method|lang=zh-CN|style=Feynman)。通过将波方程的微积分问题转化为矩阵代数问题，该方法为理解波在周期性系统中的复杂运动提供了清晰的途径。

接下来的章节将引导您了解这项精妙的技术。首先，在“原理与机制”一章中，我们将探讨该方法的理论基础，包括布洛赫定理和[傅里叶分析](@keyword=fourier_analysis|lang=zh-CN|style=Feynman)，并了解它们如何结合起来创建一个可解的特征值问题。我们还将考察一些实际考虑因素，例如使该方法对真实材料有效的[赝势](@keyword=effective_core_potentials|lang=zh-CN|style=Feynman)。随后，“应用与跨学科联系”一章将展示该方法的巨大影响，从解释固体的基本电子性质到推动[光纤](@keyword=optical_fiber|lang=zh-CN|style=Feynman)和激光器等先进[光子](@keyword=photon|lang=zh-CN|style=Feynman)器件的创新。

## 原理与机制

想象一下，您正试图理解一个宏伟音乐厅的声学特性。但这并非普通的大厅，而是一个由圆柱构成的、完全有序的无限晶体。[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)进入这个大厅后，不会简单地[直线传播](@keyword=rectilinear_propagation|lang=zh-CN|style=Feynman)。它会以一种由圆柱的重复[排列](@keyword=permutation|lang=zh-CN|style=Feynman)所决定的复杂模式进行反弹、反射和干涉。这个晶体有其自身的[共振频率](@keyword=resonant_frequency|lang=zh-CN|style=Feynman)和谐波。某些音符可能会永远回响，而另一些则可能被完全压制。我们如何才能预测这种复杂的行为呢？这正是物理学家们在研究电子或[光子](@keyword=photon|lang=zh-CN|style=Feynman)在晶体的周期性环境中运动时所面临的难题。答案就是计算物理学家工具库中最强大的工具之一，一种被称为**[平面波展开法](@keyword=plane_wave_expansion_method|lang=zh-CN|style=Feynman)**的优美策略。

### [晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的“乐章”：从波到代数

其核心问题是在一个周期性环境中求解波方程——对于电子是薛定谔方程，对于光是麦克斯韦方程组。这个周期性环境可以是由晶体原子产生的周期性势，也可以是[光子](@keyword=photon|lang=zh-CN|style=Feynman)器件中[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)的周期性[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。这些控制方程是[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)，处理起来可能非常困难。[平面波展开法](@keyword=plane_wave_expansion_method|lang=zh-CN|style=Feynman)的奇妙之处在于将这个微积分问题转化为一个代数问题。

第一个关键见解来自物理学中一个被称为**布洛赫定理**的卓越发现。它揭示了关于任何周期性系统中波的深刻性质。这些解，也就是被允许存在的波模式，并非任意的波。它们必须采取一种特殊形式：一个简单的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman) $e^{i\mathbf{k}\cdot\mathbf{r}}$ 乘以一个与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)本身具有相同周期性的函数。可以把它想象成一个基本的“[载波](@keyword=carrier_wave|lang=zh-CN|style=Feynman)”，其上“装饰”着一个从一个[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)到下一个[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)重复的复杂图案。

第二个关键见解来自 Joseph Fourier，是整个科学界最著名的思想之一。他证明了*任何*[周期函数](@keyword=periodic_functions|lang=zh-CN|style=Feynman)都可以完美地描述为一系列简单的[正弦波和余弦波](@keyword=sine_and_cosine_waves|lang=zh-CN|style=Feynman)之和。在我们的情况下，[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的天然“[谐波](@keyword=harmonic_waves|lang=zh-CN|style=Feynman)”是一组特殊的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)，其[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman) $\mathbf{G}$ 构成了所谓的**[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)**。这个[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)是实空间[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)在傅里叶空间中的“指纹”；原子紧密堆积的晶体（实空间[晶格矢量](@keyword=lattice_vectors|lang=zh-CN|style=Feynman)小）将具有稀疏的[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)（[倒易晶格矢量](@keyword=reciprocal_lattice_vectors|lang=zh-CN|style=Feynman)大），反之亦然。[@problem_id:2509798]

现在，我们将这两个思想结合起来。我们可以用这些特殊的[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)平面波来展开*所有*相关的量。我们展开[布洛赫波](@keyword=bloch_waves|lang=zh-CN|style=Feynman)的[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)周期部分，同时还展开周期性势 $V(\mathbf{r})$（对电子而言）或周期性介电函数 $\epsilon(\mathbf{r})$（对[光子](@keyword=photon|lang=zh-CN|style=Feynman)而言）。当我们将这些展开式代回原始的波方程时，奇妙的事情发生了。[导数](@keyword=derivative|lang=zh-CN|style=Feynman)和复杂的空间函数都消失了，剩下的是一个[代数方程](@keyword=algebraic_equations|lang=zh-CN|style=Feynman)。具体来说，它变成了一个矩阵**特征值问题**。[@problem_id:1812224]

对于我们选择研究的每一个载波[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman) $\mathbf{k}$，我们都会得到一个矩阵。求解这个矩阵问题会得到一组[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)，它们对应于该 $\mathbf{k}$ 值下所允许的能量 $E_n(\mathbf{k})$ 或频率 $\omega_n(\mathbf{k})$。通过沿晶体**[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)**（即倒易晶格的基本晶胞）中的高对称性路径对许多不同的 $\mathbf{k}$ 矢量进行求解，我们就可以描绘出完整的**能带结构**。这张图告诉我们一切：材料是金属还是绝缘体，或者它允许什么颜色的光通过。我们已经“驯服”了晶体中波的无限复杂性，并将其转化为一组可由计算机求解的矩阵。

### 构建矩阵：一首简单的交响曲

那么这些矩阵是什么样的呢？我们来看一个非常简单的一维例子。想象一个电子在晶体中运动，其势场是一个简单的余弦波, $V(x) = V_0 \cos(G_0 x)$，其中 $G_0 = 2\pi/a$ 是最小的非零[倒易晶格矢量](@keyword=reciprocal_lattice_vectors|lang=zh-CN|style=Feynman)。[@problem_id:155586]

我们的[基函数](@keyword=basis_functions|lang=zh-CN|style=Feynman)是平面波 $|k+G\rangle$，其中 $G = n G_0$，$n$ 为整数。哈密顿矩阵的对角元 $H_{G,G}$ 就是这些平面波的动能 $(k+G)^2$。这是在晶体势关闭时电子所具有的能量。

有趣的部分是非对角元 $H_{G',G}$，它告诉我们晶体势如何耦合不同的平面波。对于我们这个简单的余弦势，它可以写成 $\frac{V_0}{2}(e^{iG_0x} + e^{-iG_0x})$，它只有两个傅里叶分量，分别位于 $+G_0$ 和 $-G_0$。令人难以置信的结果是，这个势只将一个平面波 $|k+G\rangle$ 与其在倒易空间中的最近邻耦合，即 $|k+G+G_0\rangle$ 和 $|k+G-G_0\rangle$。这种耦合的大小，即非对角矩阵元的值，就是简单的 $\frac{V_0}{2}$。[@problem_id:155586]

这是一个优美而普适的原理。周期性势的傅里叶分量直接成为控制电子量子力学行为的[哈密顿矩阵](@keyword=hamiltonian_matrix|lang=zh-CN|style=Feynman)的非对角元。具有许多傅里叶分量的复杂势会产生一个[稠密矩阵](@keyword=dense_matrix|lang=zh-CN|style=Feynman)，耦合许多不同的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)。一个简单的势则产生一个[稀疏矩阵](@keyword=sparse_matrix|lang=zh-CN|style=Feynman)。[电子散射](@keyword=electron_scattering|lang=zh-CN|style=Feynman)的物理学被直接编码在该矩阵的数学结构中。

### 因材施用：为何选择平面波？

这种方法总是最佳选择吗？当然不是。一个好的物理学家，就像一个好木匠一样，知道必须为工作选择合适的工具。[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)是描述[离域](@keyword=delocalization|lang=zh-CN|style=Feynman)和“波状”事物的自然语言。

考虑两个固体的极端例子。[@problem_id:1814794] 一方面，像铝这样的简单金属。其价电子不与任何特定原子绑定；它们形成一个在整个晶体中流动的“电子海”。它们的行为非常像“近自由”[电子气](@keyword=electron_gas|lang=zh-CN|style=Feynman)，仅受到离子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的轻微扰动。对于这个系统，使用[平面波基组](@keyword=plane_wave_basis_sets|lang=zh-CN|style=Feynman)是一个极其高效且物理上直观的起点。真实状态非常接近于一个简单的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)，所以我们只需要少数几个平面波来描述修正，PWE 方法收敛得很快。

另一方面，考虑像氯化钠（食盐）这样的离子绝缘体。在这里，价电子紧密地束缚在氯阴离子上。它们是高度局域化的。试图用空间延展的平面波来构建这样一个局域函数，就像试图用[水波](@keyword=water_waves|lang=zh-CN|style=Feynman)来建造一座砖房——你可以做到，但这需要数量巨大的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)进行精确的干涉，这在计算上是非常昂贵的。对于这样的系统，一种名为**[紧束缚](@keyword=binding_constraints|lang=zh-CN|style=Feynman)（TB）法**的不同方法，即从原子轨道本身构建晶体[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)，是一个远为自然和高效的选择。

因此，[平面波展开法](@keyword=plane_wave_expansion_method|lang=zh-CN|style=Feynman)的威力在于它完美地适用于粒子或波不被强局域化的系统——这是一类庞大且重要的材料和器件，从[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)到[光子](@keyword=photon|lang=zh-CN|style=Feynman)电路都属此列。

### 方法实践：塑造光与物质

让我们从电子转向[光子](@keyword=photon|lang=zh-CN|style=Feynman)。完全相同的原理使我们能够设计**光子晶体**——一种具有周期性[介电常数](@keyword=permittivity|lang=zh-CN|style=Feynman)的材料，它对[光子](@keyword=photon|lang=zh-CN|style=Feynman)的作用就像[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)晶体对电子的作用一样。通过创造一个具有**[光子带隙](@keyword=photonic_bandgaps|lang=zh-CN|style=Feynman)**的结构，我们可以真正地禁止特定颜色的光在其中传播，从而为创造光路、高效LED和新型激光器打开了大门。

出发点仍然是[麦克斯韦方程组](@keyword=maxwell_s_equations|lang=zh-CN|style=Feynman)，它可以被巧妙地整理成一个与薛定谔方程惊人相似的[特征值方程](@keyword=eigenvalue_equations|lang=zh-CN|style=Feynman)。[@problem_id:1812224] 此时，故事的主角不再是周期性势 $V(\mathbf{r})$，而是周期性的逆介电函数 $\kappa(\mathbf{r}) = 1/\epsilon(\mathbf{r})$。

和之前一样，我们将 $\kappa(\mathbf{r})$ 展开成[傅里叶级数](@keyword=fourier_series|lang=zh-CN|style=Feynman)。傅里叶系数 $\kappa(\mathbf{G})$ 告诉矩阵，空间变化的[介电常数](@keyword=permittivity|lang=zh-CN|style=Feynman)如何将一个波矢为 $\mathbf{k}+\mathbf{G}'$ 的平面光波散射成另一个波矢为 $\mathbf{k}+\mathbf{G}$ 的光波。[@problem_id:2509798] 由此产生的[矩阵方程](@keyword=matrix_equations|lang=zh-CN|style=Feynman)给出了[光子](@keyword=photon|lang=zh-CN|style=Feynman)[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman) $\omega_n(\mathbf{k})$。

这不仅仅是一个抽象的概念。我们可以为真实世界的设计计算出这些关键的傅里叶系数。例如，考虑一个在硅板上钻有圆形空[气孔](@keyword=stomata|lang=zh-CN|style=Feynman)的二维方格子。该结构的[傅里叶系数](@keyword=fourier_coefficients|lang=zh-CN|style=Feynman) $\kappa(\mathbf{G})$ 可以通过一个直接的积分计算出来，答案涉及一个著名的数学函数：**贝塞尔函数** $J_1$。具体来说，该系数正比于 $(\frac{1}{\epsilon_a}-\frac{1}{\epsilon_b})\frac{J_1(GR)}{GR}$，其中 $R$ 是孔的半径，$G$ 是[倒易晶格矢量](@keyword=reciprocal_lattice_vectors|lang=zh-CN|style=Feynman)的大小。[@problem_id:1179064] 更复杂的六方[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的矩阵元也可以用类似的方式找到。[@problem_id:1596483] 这向我们展示了，几何结构（[晶格类型](@keyword=crystal_lattice_types|lang=zh-CN|style=Feynman)、孔半径）和[材料属性](@keyword=material_properties|lang=zh-CN|style=Feynman)（[介电常数](@keyword=permittivity|lang=zh-CN|style=Feynman) $\epsilon_a, \epsilon_b$）如何通过[傅里叶分析](@keyword=fourier_analysis|lang=zh-CN|style=Feynman)的语言直接转化为填充我们矩阵的数字，并最终决定器件的光学性质。

### 应对现实：赝势和其他巧妙技巧

我们所描绘的[简单图](@keyword=simple_graphs|lang=zh-CN|style=Feynman)景功能强大，但要将其应用于真实、复杂的材料，需要面对一些严酷的现实。物理学家们以其持久的创造力，发展出一些真正巧妙的技巧来克服这些障碍。

首先是**核心电子问题**。在一个真实的原子中，电子感受到的势能在靠近原子核的地方变得极其强大（以 $1/r$ 的形式发散）。此外，负责化学键合的价电子，其[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在这个核心区域必须是褶皱且快速[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的，以保证与[紧束缚](@keyword=binding_constraints|lang=zh-CN|style=Feynman)的核心电子正交。用光滑的平面波来描述这些尖峰和快速摆动是一场噩梦——这将需要计算上不可能实现的大量[基函数](@keyword=basis_functions|lang=zh-CN|style=Feynman)。但诀窍在于：对于化学而言，我们并不真正关心电子在原子核深处的复杂运动。重要的是价电子在该区域*之外*的行为。这就是**[赝势近似](@keyword=pseudopotential_approximation|lang=zh-CN|style=Feynman)**的动机。[@problem_id:2480449] 我们用一个更弱、更平滑、更温和的**赝势**来取代极其复杂的全电子势。这种“定制”的势被精心构建，使其在某个核心半径之外与真实势完全相同，但在内部却是平滑且无节点的。由此产生的“赝[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)”现在是[光滑函数](@keyword=smooth_functions|lang=zh-CN|style=Feynman)，非常适合高效的[平面波展开](@keyword=plane_wave_expansion|lang=zh-CN|style=Feynman)，同时仍能正确描述化学键合的所有重要物理特性。像**投影缀加波（PAW）**这样的现代方法进一步完善了这一思想，提供了一种形式化的数学方法来以惊人的准确度恢复全电子属性，让我们两全其美。[@problem_id:2915064]

其次是[库仑定律](@keyword=coulomb_s_law|lang=zh-CN|style=Feynman)的长程作用。在计算离子晶体的总能量时，我们必须对无限[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上的 $1/r$ 库仑相互作用进行求和。这个求和在数学上是一场灾难。它收敛得如此之慢，以至于其值实际上取决于你求和的晶体块的形状！这种“灾难”也出现在[倒易空间](@keyword=reciprocal_space|lang=zh-CN|style=Feynman)中，其中[势的傅里叶变换](@keyword=fourier_transform_of_potential|lang=zh-CN|style=Feynman) $1/G^2$ 在 $G=0$ 处发散。[@problem_id:2460257] 优美的解决方案是**[Ewald求和](@keyword=ewald_summation|lang=zh-CN|style=Feynman)**。其思想是将有问题的 $1/r$ 相互作用分为短程部分和长程部分。短程部分在实空间中求和，现在收敛得很快。长程部分由于是平滑的，被转换到倒易空间中，其傅里eleaf变换现在衰减得非常快。结果是两个快速收敛的和以及一些修正项，从而得到一个定义明确、与形状无关的能量。

最后，需要提醒一点。PWE方法通常在计算机上实现，而计算机会完全按照指令行事。我们的[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)必须是有限的，因此我们通过包含所有动能直到某个**[动能截断](@keyword=kinetic_energy_cutoff|lang=zh-CN|style=Feynman)值** $E_{cut}$ 的平面波来截断它。一个微妙的问题随之产生，因为这个截断规则意味着当你在[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)内扫描波矢 $\mathbf{k}$ 时，[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)的大小可能会改变。对于某个 $\mathbf{k}$ 值被包含的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)，对于其邻近的 $\mathbf{k}'$ 值可能被排除在外。[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)的这种突变会导致计算出的能带结构中出现不符合物理的跳跃和不连续性。这些人为产物被恰当地称为**“鬼带”**。[@problem_id:2387862] 它们提醒我们，即使有了一个优美的理论框架，也必须是一个谨慎的实践者，时刻警惕机器中可能出现的“鬼魂”。