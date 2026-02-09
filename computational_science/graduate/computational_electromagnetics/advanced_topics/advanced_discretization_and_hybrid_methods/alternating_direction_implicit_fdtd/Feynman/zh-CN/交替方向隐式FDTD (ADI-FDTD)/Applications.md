## 应用与[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)学科联系

在上一章中，我们已经深入探讨了交替方向隐式[时域有限差分](@keyword=finite_difference_time_domain|lang=zh-CN|style=Feynman)（[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)）方法的核心原理。我们了解到，通过将一个复杂的多维问题巧妙地分解为一系列简单的一维问题，[ADI方法](@keyword=alternating_direction_implicit_method|lang=zh-CN|style=Feynman)打破了传统显式[FDTD方法](@keyword=fdtd_method|lang=zh-CN|style=Feynman)中由库朗-弗里德里希斯-列维（CFL）条件施加的严格束缚。我们不再受限于光速与网格尺寸所决定的微小时间步长。这种解放似乎赋予了我们无限的自由，仿佛我们可以随心所欲地驾驭时间的流逝。

然而，正如物理学中屡见不鲜的情形一样，更大的威力也伴随着更深刻的责任与洞察。这种“无条件稳定”的自由并非一张可以肆意挥霍的空白支票。它开启了一个充满无限可能的新世界，但同时也引入了其独特的物理实在——一种由算法自身定义的“数值实在”。本章将带领我们踏上一段旅程，探索如何运用[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)这把强大的钥匙，去开启哪些崭新的科学与工程大门，同时，我们也将警惕地审视这把钥匙可能带来的微妙扭曲，以及它在开启某些门时可能遇到的困难。

### 构筑虚拟世界：基本要素

要模拟真实世界的电磁现象，我们首先需要在计算机中构建一个自洽的虚拟“剧场”。这个剧场需要有明确的边界和注入能量的方式。[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)为这些基本要素的实现提供了独特而优雅的途径。

#### 设定边界：世界的尽头

我们模拟的空间不可能是无限的。我们如何为这个有限的计算区域定义边界呢？

最简单的边界或许是**[理想电导体](@keyword=perfect_electric_conductor|lang=zh-CN|style=Feynman)（PEC）**墙壁，就像一个完美的镜子盒子。在物理上，这意味着[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)在导体表面的切向分量必须为零。在[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的数值框架中，这个物理定律被转化成一个极其简洁的代数约束。在[线性方程组](@keyword=systems_of_linear_equations|lang=zh-CN|style=Feynman)的隐式求解过程中，我们不再需要为边界上的场点求解复杂的[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)，而是直接用一个形如“此处的场值为零”的[狄利克雷条件](@keyword=dirichlet_conditions|lang=zh-CN|style=Feynman)来替代。这在三对角矩阵中体现为一行简单的 `(0, 1, 0)` 系数，它以最直接的方式强制执行了物理定律，既优雅又高效 。这正是模拟[波导](@keyword=waveguides|lang=zh-CN|style=Feynman)、谐振腔或金属物体散射等问题的基石。

然而，我们常常对无限重复的结构感兴趣，例如[光子晶体](@keyword=photonic_crystals|lang=zh-CN|style=Feynman)、超材料或频率选择表面。这时，我们需要**[周期性边界条件](@keyword=periodic_boundary_conditions|lang=zh-CN|style=Feynman)（PBC）**，即一侧的波“穿出”后，会原封不动地从另一侧“进入”。这种“环绕”的物理特性，在数值上深刻地改变了我们求解的[线性系统](@keyword=linear_systems|lang=zh-CN|style=Feynman)的结构。原本简洁的[三对角矩阵](@keyword=tridiagonal_matrix|lang=zh-CN|style=Feynman)，因为首尾相连，在矩阵的右上角和左下角出现了非零元素，形成了一个所谓的**循环[三对角矩阵](@keyword=tridiagonal_matrix|lang=zh-CN|style=Feynman)**。标准的[托马斯算法](@keyword=tridiagonal_matrix_algorithm|lang=zh-CN|style=Feynman)（Thomas algorithm）在这种情况下会束手无策。这迫使我们寻找更精妙的算法，例如利用舍曼-莫里森-伍德伯里（Sherman-Morrison-Woodbury）公式的循环[托马斯算法](@keyword=tridiagonal_matrix_algorithm|lang=zh-CN|style=Feynman)，或者在一个更深刻的层面上，认识到对于均匀介质，这个周期性系统具有[循环矩阵](@keyword=circulant_matrix|lang=zh-CN|style=Feynman)的优美结构，可以被[离散傅里叶变换](@keyword=discrete_fourier_transform|lang=zh-CN|style=Feynman)（DFT）完美[对角化](@keyword=diagonalization|lang=zh-CN|style=Feynman)。这意味着我们可以切换到[频谱](@keyword=magnitude_spectrum|lang=zh-CN|style=Feynman)空间，将复杂的线性代数问题转化为简单的标量乘法，再通过快速傅里叶变换（FFT）以极高的效率求解 。物理上的周期性与数学上的[傅里叶变换](@keyword=fourier_transform|lang=zh-CN|style=Feynman)在此处实现了完美的统一。

当然，更多情况下，我们希望模拟的是一个向无限广阔空间辐射的开放问题，比如[天线辐射](@keyword=antenna_radiation|lang=zh-CN|style=Feynman)。这时，我们需要**[吸收边界条件](@keyword=absorbing_boundary_conditions|lang=zh-CN|style=Feynman)（ABC）**，它就像一扇通往虚空的窗户，能够让[电磁波](@keyword=electromagnetic_wave|lang=zh-CN|style=Feynman)毫无反射地穿过。在这里，[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的“无条件稳定”特性向我们展现了它复杂的一面。一个看似合理的想法是，直接将显式FDTD中使用的默尔（Mur）二阶[吸收边界条件](@keyword=absorbing_boundary_conditions|lang=zh-CN|style=Feynman)移植过来。然而，一个深刻的警示出现了：尽管[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)在数值上是稳定的，但当时间步长 $\Delta t$ 远超CFL限制时，其精度，特别是**相位精度**，会显著下降。这意味着在ADI的数值世界中，[波的传播](@keyword=wave_propagation|lang=zh-CN|style=Feynman)速度会依赖于其方向和频率，这种现象被称为**[数值色散](@keyword=numerical_dispersion|lang=zh-CN|style=Feynman)**。而默尔[吸收边界](@keyword=absorbing_boundary|lang=zh-CN|style=Feynman)是基于理想波动方程设计的，它假设波以光速传播。当一个在ADI世界中已经“变形”的[波前](@keyword=wavefront|lang=zh-CN|style=Feynman)到达这个为理想世界设计的边界时，速度失配会导致严重的伪反射。因此，随着 $\Delta t$ 的增大，[吸收边界](@keyword=absorbing_boundary|lang=zh-CN|style=Feynman)的性能反而会急剧恶化，尤其对于[斜入射](@keyword=oblique_incidence|lang=zh-CN|style=Feynman)的波更是如此 。这是一个至关重要的教训：**稳定性不等于准确性**。

为了实现真正高性能的吸收，我们需要更复杂的**[完美匹配层](@keyword=perfectly_matched_layers|lang=zh-CN|style=Feynman)（PML）**。PML本身就是一个精妙的物理构造，它通过一种坐标变换在边界处创造一个既能吸收波又不产生反射的“人造材料”。有趣的是，为了让PML与[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)协同工作，PML的数学公式本身也必须被“分裂”，以匹配ADI算法中按方向交替进行隐式计算的节拍。将PML中的损耗项在对应的方向上进行隐式处理，是确保整个方案[无条件稳定性](@keyword=unconditional_stability|lang=zh-CN|style=Feynman)的关键。这种算法与物理模型的深度融合，是现代计算电磁学中一个优美的范例 。

#### 注入能量：点燃第一束光

有了边界，我们还需要在虚拟世界中引入波源。无论是模拟[天线辐射](@keyword=antenna_radiation|lang=zh-CN|style=Feynman)还是散射问题，我们都需要精确地注入指定的[电磁波](@keyword=electromagnetic_wave|lang=zh-CN|style=Feynman)。在[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)这样的多步长[隐式格式](@keyword=implicit_schemes|lang=zh-CN|style=Feynman)中，如何注入波源同样充满技巧。简单粗暴地在每个完整时间步结束后强制设定源点的场值（硬源），会因为时序上的错位而引入显著的相位误差。为了保持方案的二阶时间精度，必须在每个隐式子步中都以符合其时间中心的方式注入源场。无论是通过直接设定场值的**硬源**，还是通过添加等效电流的**软源**，都必须遵循严格的时间中心化原则，例如对软源的电流项使用[梯形法则](@keyword=trapezoidal_rule|lang=zh-CN|style=Feynman)进行时间平均。只有这样，注入的波才能与算法的内在节奏和谐共振，最大限度地减少因源实现不当而产生的数值噪声和伪反射 。

### 浸染新色：模拟[复杂介质](@keyword=complex_medium|lang=zh-CN|style=Feynman)

[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)真正的威力，体现在它处理与物质相互作用时的非凡能力。许多真实材料的响应在时间上可能是瞬时的，也可能是有“记忆”的，其响应速度可能非常快，构成所谓的“刚性”（stiff）问题。对于显式方法，这种刚性会带来极其苛刻的稳定性限制，而[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的隐式特性使其能够从容应对。

#### 导[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)：从波动到[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)

当[电磁波](@keyword=electromagnetic_wave|lang=zh-CN|style=Feynman)进入良导体时，它的行为会发生戏剧性的转变。描述这一过程的**[电报方程](@keyword=telegraph_equation|lang=zh-CN|style=Feynman)（Telegrapher's equation）**告诉我们，在高频或低[电导率](@keyword=conductivity|lang=zh-CN|style=Feynman)时，场表现为有阻尼的波；而在低频或高[电导率](@keyword=conductivity|lang=zh-CN|style=Feynman)时，其行为更像是热量在金属中[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)。显式方法在模拟高[电导率](@keyword=conductivity|lang=zh-CN|style=Feynman)介质时，会因为介质弛豫时间远小于波的传播时间而需要极小的时间步长。[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)通过将[电导](@keyword=conductance|lang=zh-CN|style=Feynman)项 $\sigma \mathbf{E}$ 隐式处理，完美地克服了这一[刚性问题](@keyword=stiff_problems|lang=zh-CN|style=Feynman)。它不仅在数值上[无条件稳定](@keyword=unconditionally_stable|lang=zh-CN|style=Feynman)，而且能够准确地模拟从波动到[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)的整个物理谱系。这也揭示了另一个深刻的道理：虽然稳定性不再是问题，但为了准确捕捉物理过程，时间步长必须能够分辨该过程的特征时间尺度。在[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)主导的区域，这个尺度不再是 $\Delta x/c$，而是由[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)系数决定的 $\mu\sigma(\Delta x)^2$ 。

#### [色散介质](@keyword=dispersive_medium|lang=zh-CN|style=Feynman)：拥有记忆的材料

许多材料，如水、生物组织以及众多光学材料，其[介电常数](@keyword=dielectric_constant|lang=zh-CN|style=Feynman)随频率而变，这种现象称为**[色散](@keyword=chromatic_dispersion|lang=zh-CN|style=Feynman)**。这意味着材料的响应不是瞬时的，而是依赖于场的历史，仿佛拥有“记忆”。模拟这类材料通常需要引入**辅助[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)（[ADE](@keyword=antibody_dependent_enhancement|lang=zh-CN|style=Feynman)）**来描述材料内部的极化状态。以经典的**德拜（Debye）模型**为例，描述其极化演化的[ADE](@keyword=antibody_dependent_enhancement|lang=zh-CN|style=Feynman)可能包含一个非常快的弛豫过程。[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)再次展现了其优势：通过将[ADE](@keyword=antibody_dependent_enhancement|lang=zh-CN|style=Feynman)与麦克斯韦方程组进行隐式耦合，利用梯形法则等[时间中心格式](@keyword=time_centered_scheme|lang=zh-CN|style=Feynman)进行离散，即使[弛豫时间](@keyword=relaxation_times|lang=zh-CN|style=Feynman)极短，该方案也能保持稳定性和二阶精度。这使得对生物组织中的[电磁波传播](@keyword=electromagnetic_wave_propagation|lang=zh-CN|style=Feynman)等复杂问题的长时间、大尺度模拟成为可能 。

#### [各向异性介质](@keyword=anisotropic_medium|lang=zh-CN|style=Feynman)：方向的魔力

在晶体或磁化等离子体中，电磁波的传播行为依赖于其[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)方向。这种**各向异性**在数学上通过一个[介电常数张量](@keyword=permittivity_tensor|lang=zh-CN|style=Feynman) $\boldsymbol{\epsilon}$ 来描述。当这个张量存在非对角元素时，它会在麦克斯韦方程中直接耦合[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)的不同分量（例如，$D_x$ 同时依赖于 $E_x, E_y, E_z$）。这对[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的结构产生了根本性的影响。原本每个场分量各自对应一个标量[三对角线性系统](@keyword=tridiagonal_linear_systems|lang=zh-CN|style=Feynman)，现在因为分量间的局部耦合，这些系统合并成了一个**块[三对角系统](@keyword=tridiagonal_systems|lang=zh-CN|style=Feynman)**。矩阵中的每个元素不再是一个标量，而是一个 $3 \times 3$ 的小矩阵。求解这样的系统需要相应的**块[托马斯算法](@keyword=tridiagonal_matrix_algorithm|lang=zh-CN|style=Feynman)**。这完美地体现了物理世界的内在结构（材料的各向异性）如何直接映射到计算世界的[代数结构](@keyword=algebraic_structure|lang=zh-CN|style=Feynman)（矩阵的块状特征）之上 。

#### [非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)介质：当材料开始“回应”

在强场（如高功率[激光](@keyword=laser|lang=zh-CN|style=Feynman)）作用下，许多材料的响应不再是线性的。例如，在具有**克尔（Kerr）效应**的介质中，[介电常数](@keyword=dielectric_constant|lang=zh-CN|style=Feynman)本身依赖于[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)强度的平方。这使得控制方程变成了[非线性方程](@keyword=nonlinear_equations|lang=zh-CN|style=Feynman)。即使[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的线性波传播部分是[无条件稳定](@keyword=unconditionally_stable|lang=zh-CN|style=Feynman)的，求解这个[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)代数方程本身也带来了新的挑战。通常需要采用[不动点迭代](@keyword=fixpoint_iteration|lang=zh-CN|style=Feynman)等方法。分析发现，这种[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)迭代的收敛性是有条件的，当时间步长过大时，即使线性部分稳定，[非线性求解器](@keyword=nonlinear_solvers|lang=zh-CN|style=Feynman)也可能发散。这揭示了一个深刻的层次：一个多物理场耦合的数值方案，其整体稳定性取决于最薄弱的环节。[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)带来的大时间步长自由，可能会被[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)过程的收敛性重新戴上枷锁 。

#### 磁化等离子体：集大成者

模拟[磁化等离子体](@keyword=magnetized_plasma|lang=zh-CN|style=Feynman)（如在地球电离层或[聚变反应堆](@keyword=fusion_reactor|lang=zh-CN|style=Feynman)中）是计算电磁学的一项终极挑战。它集多种复杂性于一身：它既是[色散](@keyword=chromatic_dispersion|lang=zh-CN|style=Feynman)的，又是各向异性的（更准确地说是**[旋光性](@keyword=optical_activity|lang=zh-CN|style=Feynman)**的），其响应由一个复杂的张量描述。描述等离子体中电流的运动方程与麦克斯韦方程紧密耦合，且[回旋运动](@keyword=gyromotion|lang=zh-CN|style=Feynman)项和空间[旋度算子](@keyword=curl_operator|lang=zh-CN|style=Feynman)互不对易，给高阶算法的设计带来了巨大困难。然而，[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)框架，如果构建得当——采用对称的[算子分裂](@keyword=operator_splitting|lang=zh-CN|style=Feynman)，并在每个子步中对材料（等离子体）方程进行隐式、时间中心化的处理——就能够驾驭这种复杂性，实现对这一复杂系统的[无条件稳定](@keyword=unconditionally_stable|lang=zh-CN|style=Feynman)和二阶精度模拟 。

### 跨越尺度：多物理与[多尺度建模](@keyword=multiscale_modeling|lang=zh-CN|style=Feynman)

[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的灵活性不仅体现在处理复杂材料上，更体现在它能够将不同尺度、甚至不同物理领域的模型无缝地集成在一起。

#### 子网格技术：在需要之处“放大”

在许多问题中，我们只对一小部分区域的精细结构感兴趣，例如天线馈电点或散射体的尖锐边缘。在整个计算域都使用精细网格会造成巨大的计算资源浪费。**子网格（Subgridding）**技术允许我们在感兴趣的区域局部加密网格。这种方法的关键和难点在于粗、细网格交界面的处理。为了保证整个方案的稳定性，界面上的场量传递算子必须是**[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)**或至少是能量稳定的。一个优美的理论结果表明，如果传递[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的算子 $\mathcal{T}_H$ 是传递[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)算子 $\mathcal{T}_E$ 的转置（或伴随），即 $\mathcal{T}_H = (\mathcal{T}_E)^T$，那么通过界面的离散坡印廷[能量流](@keyword=energy_flow|lang=zh-CN|style=Feynman)就能得到守恒。这为构建稳健的多尺度算法提供了坚实的理论基础 。

#### 集总元件：将电路嵌入场

有时，我们需要模拟的系统中包含一些尺寸远小于网格的结构，如细导线、电阻或电容。直接用麦克斯韦方程解析这些结构是不现实的。一个聪明的办法是用**集总电路元件**的常微分方程（ODE）来描述它们的行为，并将这些ODE耦合到FDTD网格中。例如，一个细导线段可以被等效为一个[LC电路](@keyword=lc_circuits|lang=zh-CN|style=Feynman)。[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的隐式特性再次发挥作用：通过将电路元件的ODE进行隐式离散并与场的[更新方程](@keyword=renewal_equation|lang=zh-CN|style=Feynman)联立求解，即使电路参数（L或C）非常极端（构成“刚性”问题），整个混合方案也能保持稳定 。

#### [粒子模拟](@keyword=particle_simulation|lang=zh-CN|style=Feynman)：场与物质的共舞

在等离子体物理或[粒子加速器](@keyword=particle_accelerators|lang=zh-CN|style=Feynman)模拟中，我们需要同时求解描述[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)的麦克斯韦方程和描述[带电粒子运动](@keyword=charged_particle_motion|lang=zh-CN|style=Feynman)的牛顿-洛伦兹方程。这种方法被称为**胞中粒子（Particle-In-Cell, PIC）**。将[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)作为场求解器与PIC耦合，可以允许使用更大的时间步长，这对于长时间的模拟至关重要。然而，这种耦合也可能催生一种臭名昭著的数值伪影——**数值[切伦科夫辐射](@keyword=čerenkov_radiation|lang=zh-CN|style=Feynman)**。其根源在于，以接近光速运动的粒子，其在离散时空网格上产生的“驱动”[频谱](@keyword=magnitude_spectrum|lang=zh-CN|style=Feynman)，可能会与网格自身支持的[电磁模式](@keyword=electromagnetic_modes|lang=zh-CN|style=Feynman)发生共振，从而激发出大量非物理的噪声。[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的[数值色散关系](@keyword=numerical_dispersion_relation|lang=zh-CN|style=Feynman)与标准FDTD不同，这使得其共振条件也随之改变。理解这一机制后，我们可以设计相应的数字滤波器，在保持方案稳定性的同时，精确地“切除”那些最容易被激发的、靠近网格奈奎斯特频率的有害模式 。

### 一点警示：洞穴中的阴影

我们已经见证了[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的强大与优雅，但正如柏拉图洞穴寓言中的囚徒，我们必须认识到，任何数值方法都只是对真实世界的一种投影，一种近似。[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的投影方式有其独特的“阴影”。

我们之前提到，[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)的无条件稳定是以牺牲部分精度为代价的，特别是它引入了各向异性的[数值色散](@keyword=numerical_dispersion|lang=zh-CN|style=Feynman)。这种[色散](@keyword=chromatic_dispersion|lang=zh-CN|style=Feynman)对于传播波的影响或许尚可接受，但对于**[倏逝波](@keyword=evanescent_waves|lang=zh-CN|style=Feynman)（evanescent waves）**，其影响可能是致命的。[倏逝波](@keyword=evanescent_waves|lang=zh-CN|style=Feynman)是那些在空间中快速衰减的近场分量，它们携带了物体的亚波长精细信息，在[纳米光子学](@keyword=nanophotonics|lang=zh-CN|style=Feynman)、表面等离激元等前沿领域至关重要。

分析表明，[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)中的[算子分裂](@keyword=operator_splitting|lang=zh-CN|style=Feynman)误差项，会人为地**增加**倏逝[波的衰减](@keyword=wave_attenuation|lang=zh-CN|style=Feynman)速率。这意味着，当使用[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)模拟亚波长谐振器（如[纳米天线](@keyword=nanoantennas|lang=zh-CN|style=Feynman)）的近场时，计算出的场强会比真实值（甚至是比标准FDTD计算的值）偏低。在这种对近场精度要求极高的应用中，[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)虽然稳定，但其结果的保真度可能反而不如受[CFL条件](@keyword=courant–friedrichs–lewy_condition|lang=zh-CN|style=Feynman)限制的显式[FDTD方法](@keyword=fdtd_method|lang=zh-CN|style=Feynman)。我们用稳定性换来的，可能是对倏逝世界的“视而不见”。

这最终将我们引向作为科学家和工程师的终极智慧：没有万能的工具，只有最合适的工具。理解一个方法的局限性，与掌握它的威力同等重要。[ADI-FDTD](@keyword=adi_fdtd|lang=zh-CN|style=Feynman)为我们打破CFL壁垒提供了一把钥匙，但用好这把钥匙，需要我们深刻理解它所揭示的那个既广阔又略带扭曲的数值新世界。