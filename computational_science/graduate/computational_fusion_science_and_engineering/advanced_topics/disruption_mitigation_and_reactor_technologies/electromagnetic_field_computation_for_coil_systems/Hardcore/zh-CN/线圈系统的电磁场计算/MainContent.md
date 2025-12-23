## 引言
在线圈系统的设计与分析中，精确计算其产生的电磁场是所有后续工程应用的基础。无论是在磁约束聚变装置、高场磁体，还是在[无线电能传输](@entry_id:269194)系统中，对磁场分布、能量存储和电磁力的深刻理解都是不可或缺的。然而，从基本的麦克斯韦方程到能够指导实际工程设计的数值工具，其中涉及复杂的物理近似、数学变换和计算挑战。本文旨在填补这一知识鸿沟，系统性地阐述计算线圈系统电磁场的核心原理、方法及其在尖端科技领域的应用。

本文将分为三个核心部分。在“原理与机制”一章中，我们将深入探讨从[麦克斯韦方程组](@entry_id:150940)出发，如何通过[磁准静态近似](@entry_id:1127597)简化问题，并引入磁矢势和[毕奥-萨伐尔定律](@entry_id:267294)作为核心计算工具，同时解决数值计算中的奇异性难题。接着，在“应用与跨学科联系”一章中，我们将展示这些理论如何在磁约束聚变、[结构力学](@entry_id:276699)和控制理论等交叉学科中发挥关键作用，例如通过求解[逆问题](@entry_id:143129)来优化线圈设计或通过[多物理场耦合](@entry_id:171389)分析评估设备可靠性。最后，“实践练习”部分将提供一系列具体问题，帮助读者巩固理论知识并将其应用于实际计算任务中。通过学习本文，读者将建立一个从第一性原理到高级应用的完整知识框架，掌握分析和设计复杂电磁系统的核心能力。

## 原理与机制

本章旨在深入探讨计算线圈系统产生电磁场的核心原理与关键机制。在“引言”章节的基础上，我们将直接进入控制方程、数学工具及其在聚变工程等领域的实际应用。我们将从基本的麦克斯韦方程组出发，建立适用于大多数线圈系统计算的物理模型，然后系统地介绍求解这些模型所必需的数学框架和数值技术。本章的最终目标是为读者提供一个坚实的理论基础，以便理解和执行复杂的电磁场计算任务。

### 电磁场控制方程与准静态近似

从根本上讲，任何电磁现象都由麦克斯韦方程组所描述。然而，在全时域求解完整的[麦克斯韦方程组](@entry_id:150940)在计算上是极其昂贵的，而且对于许多工程问题而言并非必要。因此，识别并应用恰当的物理近似是[计算电磁学](@entry_id:265339)中的首要步骤。对于典型的线圈系统，尤其是那些用于产生和控制等离子体的聚变装置，电流和场的时变速率相对较慢，这使得**磁准静态（Magneto-Quasistatic, MQS）**近似成为一个极其有效且准确的工具。

MQS近似的本质在于忽略安培-麦克斯韦方程中的位移电流项 $\varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}$。完整的安培-麦克斯韦方程为：
$$ \nabla \times \mathbf{B} = \mu_0 \mathbf{J} + \mu_0 \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t} $$
其中 $\mathbf{B}$ 是[磁感应强度](@entry_id:144179)，$\mathbf{J}$ 是[自由电流](@entry_id:191634)密度，$\mathbf{E}$ 是电场强度，$\mu_0$ 和 $\varepsilon_0$ 分别是[真空磁导率](@entry_id:186031)和介[电常数](@entry_id:272823)。[位移电流](@entry_id:190231)的物理意义在于，变化的电场可以像[传导电流](@entry_id:265343)一样激发出磁场，这是[电磁波传播](@entry_id:272130)的关键。忽略它意味着我们放弃了对[电磁辐射](@entry_id:152916)和波传播效应的描述，而专注于由[传导电流](@entry_id:265343)主导的感应效应。

要证明忽略位移电流的合理性，必须满足两个核心条件 。

1.  **在导体内部**：在良导体（如铜或[不锈钢](@entry_id:276767)）中，电流密度由[欧姆定律](@entry_id:276027) $\mathbf{J} = \sigma \mathbf{E}$ 给出，其中 $\sigma$ 是电导率。对于一个以[角频率](@entry_id:261565) $\omega$ 变化的[时变场](@entry_id:180620)，位移电流密度的幅值约为 $|\varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}| \approx \varepsilon_0 \omega |\mathbf{E}|$，而传导电流密度的幅值为 $|\mathbf{J}| = \sigma |\mathbf{E}|$。为了使[位移电流](@entry_id:190231)远小于传导电流，必须满足：
    $$ \varepsilon_0 \omega \ll \sigma $$
    对于金属导体和聚变装置中典型的控制频率（通常低于数千赫兹），这个条件能够以多个数量级的优势被满足。

2.  **在真空或绝缘区域**：在真空中，$\mathbf{J} = \mathbf{0}$，因此我们不能直接比较位移电流和传导电流。此时，我们必须考虑系统的全局特性。MQS近似成立的条件是，电磁信息（以光速 $c = 1/\sqrt{\mu_0\varepsilon_0}$ 传播）横越整个系统所需的时间 $\tau_{\text{prop}} \approx L/c$（其中 $L$ 是系统的特征尺寸），必须远小于场变化的特征时间 $\tau_{\text{var}} \approx 1/\omega$。这等价于要求系统的尺寸远小于电磁波的波长。该条件可表示为：
    $$ \frac{\omega L}{c} \ll 1 $$
    这个条件保证了系统各部分的电磁场可以被认为是瞬时响应[电流源](@entry_id:275668)的变化，从而忽略了[传播延迟](@entry_id:170242)（retardation）效应。

当这两个条件同时满足时，安培定律简化为磁静力学形式，即使在场随时间变化的情况下也是如此。此时，控制磁场的方程组为：
$$ \nabla \times \mathbf{B} = \mu_0 \mathbf{J} $$
$$ \nabla \cdot \mathbf{B} = 0 $$
[高斯磁定律](@entry_id:182942) $\nabla \cdot \mathbf{B} = 0$ 是一个基本物理定律，它始终成立。在MQS近似下，时间仅仅作为一个参数出现，即电流密度 $\mathbf{J}(\mathbf{r}, t)$ 是时间的函数，而在任意时刻 $t$，磁场 $\mathbf{B}(\mathbf{r}, t)$ 的[空间分布](@entry_id:188271)都由该时刻的电流分布瞬时确定。

MQS近似的一个重要应用场景是分析[磁场穿透](@entry_id:1127581)导电壁（如[托卡马克](@entry_id:160432)真空室）的过程。考虑一个由外部线圈产生的时变磁场，它需要穿透由[不锈钢](@entry_id:276767)等材料制成的真空室壁。变化的磁场会在导电壁中根据法拉第感应定律（$\nabla\times \mathbf{E}=-\partial \mathbf{B}/ \partial t$）和[欧姆定律](@entry_id:276027)（$\mathbf{J}=\sigma \mathbf{E}$）感应出[涡电流](@entry_id:275449)。这些[涡电流](@entry_id:275449)反过来又会产生一个抵抗外部磁场变化的磁场，从而对内部区域产生屏蔽效应。

在MQS近似下，可以推导出磁场在导体中的演化遵循一个**[磁扩散方程](@entry_id:181381)** ：
$$ \frac{\partial \mathbf{B}}{\partial t} = \frac{1}{\mu_0\sigma}\nabla^2\mathbf{B} $$
这个方程的形式与[热传导方程](@entry_id:194763)类似，表明磁场的变化是以扩散而非波动的方式“渗透”进导体。我们可以定义一个**磁[扩散时间](@entry_id:274894)** $\tau_d$，它描述了[磁场穿透](@entry_id:1127581)厚度为 $L$ 的导体的特征时间：
$$ \tau_d \sim \mu_0 \sigma L^2 $$
现在，我们可以将这个物理量用于判断[准静态近似](@entry_id:167818)的适用性。假设一个[托卡马克](@entry_id:160432)的极向场线圈电流以特征时间 $\tau_c$ 变化，例如，一个电流爬升过程 $I(t) = I_0(1-\exp(-t/\tau_c))$ 的特征时间为 $\tau_c=0.2\,\mathrm{s}$。真空室壁厚 $L=0.04\,\mathrm{m}$，电导率 $\sigma=1.4\times 10^{6}\,\mathrm{S/m}$。我们可以计算出磁扩散时间：
$$ \tau_d \approx (4\pi\times 10^{-7}\,\mathrm{H/m}) \times (1.4\times 10^{6}\,\mathrm{S/m}) \times (0.04\,\mathrm{m})^2 \approx 2.8 \times 10^{-3}\,\mathrm{s} $$
由于线圈电流的变化时间 $\tau_c = 200\,\mathrm{ms}$ 远大于[磁场穿透](@entry_id:1127581)壁的时间 $\tau_d \approx 2.8\,\mathrm{ms}$ ($\tau_c \gg \tau_d$)，这意味着在电流变化的任何瞬间，磁场都有足够的时间穿透导电壁并在真空室内达到平衡。涡流的[屏蔽效应](@entry_id:136974)可以忽略不计。在这种情况下，我们可以放心地使用准静态模型，即在每个时刻，都将问题视为一个由瞬时线圈电流决定的[静磁场](@entry_id:924015)边值问题来求解。反之，如果 $\tau_c \lesssim \tau_d$，则[涡流](@entry_id:275449)[屏蔽效应](@entry_id:136974)会非常显著，必须求解完整的[磁扩散](@entry_id:187718)或更复杂的电磁场方程。

### 磁矢势与拓扑约束

在确定了磁准静态方程组 $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}$ 和 $\nabla \cdot \mathbf{B} = 0$ 后，下一步是寻找求解方法。[高斯磁定律](@entry_id:182942) $\nabla \cdot \mathbf{B} = 0$ 在数学上意味着磁场是一个**螺线向量场**。根据[亥姆霍兹定理](@entry_id:275687)或更基本的向量恒等式 $\nabla \cdot (\nabla \times \mathbf{A}) = 0$，这个条件保证了我们可以引入一个**[磁矢势](@entry_id:141246) (magnetic vector potential)** $\mathbf{A}$，使得：
$$ \mathbf{B} = \nabla \times \mathbf{A} $$
引入磁矢势的巨大优势在于它将求解三个耦合的 $\mathbf{B}$ 分量的[一阶偏微分方程](@entry_id:178306)问题，转化为求解三个 $\mathbf{A}$ 分量的[二阶偏微分方程](@entry_id:175326)问题。

然而，磁矢势的定义并非唯一。对于任意标量场 $\psi$，进行**[规范变换](@entry_id:176521) (gauge transformation)** $\mathbf{A}' = \mathbf{A} + \nabla \psi$，磁场 $\mathbf{B}$ 保持不变：
$$ \mathbf{B}' = \nabla \times \mathbf{A}' = \nabla \times (\mathbf{A} + \nabla \psi) = \nabla \times \mathbf{A} + \nabla \times (\nabla \psi) = \mathbf{B} $$
因为[梯度的旋度](@entry_id:274168)恒为零。为了得到一个确定的解，我们必须施加一个额外的条件来固定规范，这称为**规范选择 (gauge fixing)**。在磁静力学中，最常用的是**[库仑规范](@entry_id:273044) (Coulomb gauge)** ：
$$ \nabla \cdot \mathbf{A} = 0 $$
将 $\mathbf{B} = \nabla \times \mathbf{A}$ 和[库仑规范](@entry_id:273044)代入[安培定律](@entry_id:140092) $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}$，并利用向量恒等式 $\nabla \times (\nabla \times \mathbf{A}) = \nabla(\nabla \cdot \mathbf{A}) - \nabla^2 \mathbf{A}$，我们得到：
$$ \nabla(\nabla \cdot \mathbf{A}) - \nabla^2 \mathbf{A} = \mu_0 \mathbf{J} \implies \nabla(0) - \nabla^2 \mathbf{A} = \mu_0 \mathbf{J} $$
最终得到关于 $\mathbf{A}$ 的**向量泊松方程**：
$$ \nabla^2 \mathbf{A} = -\mu_0 \mathbf{J} $$
这个方程是磁场计算的基石之一。但值得注意的是，这个方程的成立依赖于一个重要的[自洽性](@entry_id:160889)条件。对方程两边取散度，并利用散度与[拉普拉斯算符](@entry_id:146319)的可交换性，我们得到 $\nabla^2(\nabla \cdot \mathbf{A}) = -\mu_0 \nabla \cdot \mathbf{J}$。由于[库仑规范](@entry_id:273044)要求 $\nabla \cdot \mathbf{A} = 0$，方程左边为零，因此必须有 $\nabla \cdot \mathbf{J} = 0$。这正是[静磁学](@entry_id:140120)中[稳恒电流](@entry_id:271551)所满足的电荷守恒定律。

磁矢势的存在性虽然在局部总是得到保证，但在全局范围内则受到计算区域拓扑结构的制约 。
- **局部存在性**：对于计算区域 $\Omega$ 中的任意一点，总能找到一个足够小的邻域（例如一个球体），在这个邻域内可以定义一个光滑的[磁矢势](@entry_id:141246) $\mathbf{A}$ 使得 $\mathbf{B} = \nabla \times \mathbf{A}$。这由数学上的**[庞加莱引理](@entry_id:160150) (Poincaré lemma)** 保证，它指出在一个可收缩的区域内，任何[无散场](@entry_id:260932)（对应于闭合的[2-形式](@entry_id:188008)）都必然是某个向量场的旋度（对应于恰当的1-形式）。
- **全局存在性**：然而，在一个具有复杂拓扑结构的区域（例如，一个环形真空室，其拓扑结构为 $\mathbb{R}^3$ 挖去一个环体），全局单值的[磁矢势](@entry_id:141246)可能不存在。其存在的充要条件与区域的**第二[德拉姆上同调](@entry_id:158673)群 $H^2(\Omega; \mathbb{R})$** 有关。一个全局的、单值的[磁矢势](@entry_id:141246)存在，当且仅当磁场 $\mathbf{B}$ 对应的2-形式的[上同调类](@entry_id:263961)在 $H^2(\Omega; \mathbb{R})$ 中为零。如果 $H^2(\Omega; \mathbb{R})$ 是一个非零群，则意味着区域中存在不可收缩的二维闭合曲面。物理上，如果一个磁场穿过这样一个“拓扑洞”的净磁通量不为零（这在数学上是可能的，尽管物理上这意味着存在被包裹的磁单极子），那么就不可能在该区域内定义一个全局单值的[磁矢势](@entry_id:141246)。

在聚变装置的环形真空区域 $\Omega$ 这样的多连通区域中，即使在无源区（$\mathbf{J}=\mathbf{0}$），[库仑规范](@entry_id:273044)也不能完全固定[磁矢势](@entry_id:141246)。此时 $\mathbf{A}$ 满足 $\nabla^2 \mathbf{A} = \mathbf{0}$ 和 $\nabla \cdot \mathbf{A} = \mathbf{0}$。除了一个[特解](@entry_id:149080)外，还可以任意添加一个同时无旋无散的**调和向量场 $\mathbf{H}$**（即 $\nabla \times \mathbf{H} = \mathbf{0}$ 且 $\nabla \cdot \mathbf{H} = \mathbf{0}$）。这样的场不改变 $\mathbf{B}$，也满足[库仑规范](@entry_id:273044)，从而导致解的不唯一性。为了获得唯一解，必须施加额外的拓扑约束，例如，固定[磁矢势](@entry_id:141246) $\mathbf{A}$ 沿着环向和极向等基本闭合回路的[线积分](@entry_id:141417)，这等效于固定穿过这些回路所张开的曲面的磁通量 。

### 磁场计算的积分方法：[毕奥-萨伐尔定律](@entry_id:267294)

向量泊松方程 $\nabla^2 \mathbf{A} = -\mu_0 \mathbf{J}$ 是一个[线性偏微分方程](@entry_id:172517)，其解可以通过格林函数方法表示为对源项（电流密度 $\mathbf{J}$）的积分。在无界自由空间中，并要求场在无穷远处衰减，拉普拉斯算子的格林函数为 $G(\mathbf{r}, \mathbf{r}') = 1/(4\pi |\mathbf{r} - \mathbf{r}'|)$。因此，磁矢势 $\mathbf{A}$ 的解为：
$$ \mathbf{A}(\mathbf{r}) = \frac{\mu_0}{4\pi} \int_{V'} \frac{\mathbf{J}(\mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|} dV' $$
其中积分遍布所有[电流源](@entry_id:275668)所在的体积 $V'$。这个积分形式的解自动满足[库仑规范](@entry_id:273044)（只要 $\nabla \cdot \mathbf{J} = 0$）和无穷远边界条件。对于由总电流为 $I$ 的细导线（**线电流**）构成的线圈，[体积元](@entry_id:267802) $dV'$ 中的[电流元](@entry_id:188466) $\mathbf{J}(\mathbf{r}')dV'$ 可以被替换为线[电流元](@entry_id:188466) $I d\boldsymbol{\ell}'$，其中 $d\boldsymbol{\ell}'$ 是沿着线圈路径 $C$ 的有向线元。此时，磁矢势的表达式简化为[线积分](@entry_id:141417)：
$$ \mathbf{A}(\mathbf{r}) = \frac{\mu_0 I}{4\pi} \oint_{C} \frac{d\boldsymbol{\ell}'}{|\mathbf{r} - \mathbf{r}'|} $$
为了得到磁场 $\mathbf{B}$，我们对上式求旋度。由于[旋度算子](@entry_id:184984) $\nabla$ 是对场点坐标 $\mathbf{r}$ [微分](@entry_id:158422)，而积分是对源点坐标 $\mathbf{r}'$ 进行，我们可以将[旋度算子](@entry_id:184984)移入积分号内 ：
$$ \mathbf{B}(\mathbf{r}) = \nabla \times \mathbf{A}(\mathbf{r}) = \frac{\mu_0 I}{4\pi} \oint_{C} \nabla \times \left( \frac{d\boldsymbol{\ell}'}{|\mathbf{r} - \mathbf{r}'|} \right) $$
利用向量恒等式 $\nabla \times (f\mathbf{V}) = (\nabla f) \times \mathbf{V} + f(\nabla \times \mathbf{V})$，并注意到 $d\boldsymbol{\ell}'$ 对于 $\mathbf{r}$ 而言是常向量（$\nabla \times d\boldsymbol{\ell}' = \mathbf{0}$），以及 $\nabla (1/|\mathbf{r} - \mathbf{r}'|) = -(\mathbf{r} - \mathbf{r}')/|\mathbf{r} - \mathbf{r}'|^3$，经过推导可得：
$$ \mathbf{B}(\mathbf{r}) = \frac{\mu_0 I}{4\pi} \oint_{C} \frac{d\boldsymbol{\ell}' \times (\mathbf{r} - \mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|^{3}} $$
这就是著名的**[毕奥-萨伐尔定律](@entry_id:267294) (Biot–Savart law)**。它是直接从电流分布计算磁场的最基本和最常用的工具。这个定律表明，每个[电流元](@entry_id:188466) $I d\boldsymbol{\ell}'$ 在空间点 $\mathbf{r}$ 处产生的微小磁场 $d\mathbf{B}$ 的大小与 $I |d\boldsymbol{\ell}'|$ 成正比，与到[电流元](@entry_id:188466)的距离的平方成反比，其方向由[右手定则](@entry_id:156766)确定，垂直于 $d\boldsymbol{\ell}'$ 和连接源点与场点的向量 $\mathbf{r} - \mathbf{r}'$ 所构成的平面。

### 线圈模型的物理近似

[毕奥-萨伐尔定律](@entry_id:267294)为计算磁场提供了精确的积分表达式，但前提是电流密度 $\mathbf{J}(\mathbf{r}')$ 的分布是已知的。在实际工程中，线圈具有有限的几何尺寸，对 $\mathbf{J}(\mathbf{r}')$ 进行精确建模可能非常复杂。因此，我们需要对线圈本身进行模型简化。

最常见的简化是**线电流模型 (filamentary model)**，即将具有有限[截面](@entry_id:154995)的导体线圈理想化为一根无限细的、携带全部电流 $I$ 的几何曲线。我们上面推导的[毕奥-萨伐尔定律](@entry_id:267294)的[线积分](@entry_id:141417)形式就是基于这个模型。然而，理解这个模型的[适用范围](@entry_id:636189)和局限性至关重要。

线电流模型本质上是对真实电流分布所产生磁场的[多极展开](@entry_id:144850)的零阶近似 。对于一个具有有限[截面](@entry_id:154995)的导体，其[体积形式](@entry_id:203000)的[毕奥-萨伐尔定律](@entry_id:267294)为：
$$ \mathbf{B}(\mathbf{r}) = \frac{\mu_0}{4\pi} \int_V \frac{\mathbf{J}(\mathbf{r}') \times (\mathbf{r} - \mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|^3} \, dV' $$
当观测点 $\mathbf{r}$ 远离导体（即观测点到线圈中心线的距离 $|\mathbf{R}|$ 远大于线圈[截面](@entry_id:154995)的特征尺寸 $a$，$|\mathbf{R}| \gg a$）时，我们可以对积分[核函数](@entry_id:145324) $1/|\mathbf{r} - \mathbf{r}'|^3$ 进行泰勒展开。展开的零阶项（[单极矩](@entry_id:267768)项）恰好对应于将所有电流集中在中心线上的线电流模型所产生的场。高阶项（偶极矩、[四极矩](@entry_id:157717)等）则依赖于电流密度在[截面](@entry_id:154995)上的具体分布形状和对称性。

- 如果电流密度在[截面](@entry_id:154995)上关于中心线对称分布，那么[一阶修正](@entry_id:155896)项（偶极矩项）为零。此时，线电流模型的近似误差主要由二阶项（[四极矩](@entry_id:157717)项）贡献，其相对误差的量级为 $\mathcal{O}((a/|\mathbf{R}|)^2)$。
- 在**[远场区](@entry_id:185115)** ($|\mathbf{R}| \gg a$)，线电流模型是一个非常好的近似。
- 在**近场区** ($|\mathbf{R}| \sim a$ 或更小），[多极展开](@entry_id:144850)收敛很慢或不收敛，所有高阶项的贡献都变得显著，此时线电流模型会产生巨大误差，甚至给出无物理意义的发散结果。因此，在评估导体表面或内部的磁场时，必须使用更精细的有限[截面](@entry_id:154995)模型。

### 数值计算中的奇异性问题与正则化

即使采用了线电流模型，[毕奥-萨伐尔定律](@entry_id:267294)的数值计算也面临着一个严峻的挑战：当场点 $\mathbf{r}$ 趋近于线圈路径 $\Gamma$ 时，积分[核函数](@entry_id:145324)的分母 $|\mathbf{r} - \mathbf{r}'|^3$ 趋于零，导致被积函数出现**奇异性 (singularity)** 。

对奇异性的局部行为进行分析可以发现，当场点 $\mathbf{r}$ 到线圈的[最近距离](@entry_id:164459) $\rho$ 趋于零时，磁场 $\mathbf{B}$ 的大小表现出 $1/\rho$ 的奇异性，其行为与一根无限长直导线产生的场相同：
$$ \mathbf{B}_{\text{sing}}(\mathbf{r}) \sim \frac{\mu_0 I}{2\pi \rho} \hat{\boldsymbol{\phi}} $$
其中 $\hat{\boldsymbol{\phi}}$ 是围绕线圈局部切线方向的[方位角](@entry_id:164011)[单位向量](@entry_id:165907)。这种奇异性使得标准的[数值积分方法](@entry_id:141406)（如[高斯求积](@entry_id:146011)）在近场点失效，因为被积函数变得非常尖锐甚至发散。为了解决这个问题，必须采用**正则化 (regularization)** 技术。

1.  **物理正则化：有限半径模型**
    一种方法是用一个更符合物理实际的模型来替代无限细的线电流。我们可以假设线圈是由半径为 $a$ 的圆形[截面](@entry_id:154995)导线构成，电流在[截面](@entry_id:154995)内均匀分布。通过应用安培定律，可以得到一个在任何地方都有界的磁场分布。在导线外部（$\rho \ge a$），磁场与线电流模型相同；而在导线内部（$0 \le \rho \le a$），磁场随半径线性增加：
    $$
    \mathbf{B}(\mathbf{r})=
    \begin{cases}
    \dfrac{\mu_0 I \rho}{2\pi a^2}\hat{\boldsymbol{\phi}},  \text{for } 0 \le \rho \le a \\
    \dfrac{\mu_0 I}{2\pi \rho}\hat{\boldsymbol{\phi}},  \text{for } \rho \ge a
    \end{cases}
    $$
    在导线表面 $\rho=a$ 处，磁场达到最大值 $|\mathbf{B}| = \mu_0 I / (2\pi a)$，并且是连续的。这种方法通过引入物理尺寸 $a$ 消除了奇异性。

2.  **数值正则化：奇异性减除法**
    另一种更通用的数值技术是**奇异性减除法 (singularity subtraction)**。其核心思想是“先加后减”一个与原被积函数具有相同奇异性、但又可以解析积分的项 。对于离散化的线圈（由一系列曲线段或“面板”组成），我们可以对每个面板的积分进行如下处理：
    $$ \int_{\text{panel}} K_{\text{exact}}(u) du = \int_{\text{panel}} \left( K_{\text{exact}}(u) - K_{\text{approx}}(u) \right) du + \int_{\text{panel}} K_{\text{approx}}(u) du $$
    这里，$K_{\text{exact}}(u)$ 是原始的、奇异的毕奥-萨伐尔积分核，$K_{\text{approx}}(u)$ 是一个近似核，它捕捉了 $K_{\text{exact}}(u)$ 的全部奇异行为。一个好的选择是用一段直线段（连接面板端点）的积分核作为 $K_{\text{approx}}(u)$。
    - 第一项的被积函数 $K_{\text{exact}}(u) - K_{\text{approx}}(u)$ 现在是光滑的，因为奇异部分被精确地抵消了。这一项可以用标准的[高斯求积](@entry_id:146011)等方法进行高精度数值计算。
    - 第二项 $\int K_{\text{approx}}(u) du$ 是一个直线段电流产生的磁场，它可以被解析地计算出来。
    通过这种方式，我们既保持了计算结果的精确性（因为恒等式是严格成立的），又使得需要数值处理的部分变得良态，从而大大提高了[近场](@entry_id:269780)计算的精度和效率。例如，一个直线段电流对空间一点产生的磁场可以表示为：
    $$ \mathbf{B}_{\text{segment}}(\boldsymbol{p}) = \frac{\mu_0 I}{4\pi}\,\frac{\hat{\mathbf{t}} \times \boldsymbol{\rho}}{\|\boldsymbol{\rho}\|^2} \left[ \frac{u_{+}}{\sqrt{\|\boldsymbol{\rho}\|^2 + u_{+}^2}} - \frac{u_{-}}{\sqrt{\|\boldsymbol{\rho}\|^2 + u_{-}^2}} \right] $$
    其中 $\boldsymbol{\rho}$ 是场点到直线的垂直矢量， $u_{\pm}$ 是场点投影到直线上后到线段两端的距离。

### 导出物理量：能量、电感与电磁力

一旦能够精确计算磁场 $\mathbf{B}$，我们就可以进一步计算对工程设计至关重要的其他物理量。

#### 磁能与电感

磁场在空间中存储能量，其能量密度为 $u(\mathbf{r}) = |\mathbf{B}(\mathbf{r})|^2 / (2\mu_0)$。通过对全空间积分，可以得到总[磁能](@entry_id:268850) $W$。利用向量恒等式和MQS方程，总[磁能](@entry_id:268850)可以被等价地表示为电流和[磁矢势](@entry_id:141246)的积分形式 ：
$$ W = \int \frac{|\mathbf{B}|^2}{2\mu_0} d^3 r = \frac{1}{2} \int \mathbf{J} \cdot \mathbf{A} \, d^3 r $$
对于一个由 $N$ 个独立的线圈组成的系统，每个线圈携带电流 $I_i$，上式可以转化为一个关于电流的二次型：
$$ W = \frac{1}{2} \sum_{i=1}^N I_i \Psi_i = \frac{1}{2} \sum_{i,j=1}^N I_i L_{ij} I_j $$
其中 $\Psi_i = \oint_{C_i} \mathbf{A} \cdot d\boldsymbol{\ell}_i$ 是穿过第 $i$ 个线圈回路的**磁链 (flux linkage)**。$L_{ij}$ 是**电感矩阵 (inductance matrix)** 的元素。
-   **[自感](@entry_id:265778) (Self-inductance)** $L_{ii}$ 表示第 $i$ 个线圈自身电流产生的[磁链](@entry_id:261236)与该电流的比值。
-   **互感 (Mutual inductance)** $L_{ij}$ ($i \neq j$) 表示第 $j$ 个线圈的电流在第 $i$ 个线圈处产生的磁链与电流 $I_j$ 的比值。

电感矩阵是对称的（$L_{ij} = L_{ji}$），并且是正定的（对于任何非零电流组合，总[磁能](@entry_id:268850) $W > 0$）。对于线电流模型，电感系数可以通过**诺依曼公式 (Neumann's formula)** 计算：
$$ L_{ij} = \frac{\mu_0}{4\pi} \oint_{C_i} \oint_{C_j} \frac{d\boldsymbol{\ell}_i \cdot d\boldsymbol{\ell}_j}{|\mathbf{r}_i - \mathbf{r}_j|} $$
这个公式为从线圈几何计算电路参数提供了直接的联系。然而需要注意，对于理想的线电流模型，[自感](@entry_id:265778) $L_{ii}$ 的积分会发散，这再次说明了线电流模型在[近场](@entry_id:269780)分析中的局限性，需要正则化或有限[截面](@entry_id:154995)模型来获得有限的[自感](@entry_id:265778)值。

#### [电磁力](@entry_id:196024)与麦克斯韦张量

线圈在磁场中会受到[洛伦兹力](@entry_id:145104)，力密度为 $\mathbf{f} = \mathbf{J} \times \mathbf{B}$。要计算作用在整个线圈或其一部分上的总力 $\mathbf{F} = \int_V \mathbf{f} dV$，直接对力密度进行体积积分在数值上可能很困难。一种更强大、更优雅的方法是使用**[麦克斯韦应力张量](@entry_id:153513) (Maxwell stress tensor)** 。

[麦克斯韦应力张量](@entry_id:153513)的思想是将作用在物体上的体积力，等效地转化为作用在该物体周围一个封闭曲面上的“[表面力](@entry_id:188034)”或“牵[引力](@entry_id:189550)”。在磁准静态和真空条件下，该张量定义为：
$$ T_{ij} = \frac{1}{\mu_0} \left( B_i B_j - \frac{1}{2}\delta_{ij}|\mathbf{B}|^2 \right) $$
其中 $\delta_{ij}$ 是克罗内克符号。作用在一个被光滑闭合曲面 $\mathcal{S}$ 包围的物体上的总机械力 $\mathbf{F}$，可以通过对此张量在曲面 $\mathcal{S}$ 上积分得到：
$$ F_i = \oint_{\mathcal{S}} \sum_j T_{ij} n_j \, dS $$
其中 $\mathbf{n}$ 是曲面 $\mathcal{S}$ 的外法向[单位向量](@entry_id:165907)。这个公式的强大之处在于：
1.  它将一个困难的体积积分（需要知道物体内部的电流和磁场）转化为了一个[面积分](@entry_id:275394)（只需要知道物体外部真空中的磁场）。
2.  只要曲面 $\mathcal{S}$ 完全包围目标物体且自身处于无源的真空中，计算得到的力与曲面 $\mathcal{S}$ 的具体形状和大小无关。

这为计算复杂形状线圈（如聚变装置中D型线圈）上的电磁力提供了一个极其有用的工具，因为我们可以在远离线圈、磁场行为更平滑的区域设置[积分曲面](@entry_id:175238)，从而简化计算并提高精度。