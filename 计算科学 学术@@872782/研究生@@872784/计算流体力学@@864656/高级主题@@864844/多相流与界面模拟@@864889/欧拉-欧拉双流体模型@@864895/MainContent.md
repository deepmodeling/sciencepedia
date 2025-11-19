## 引言
欧拉-欧拉[双流体模型](@entry_id:139846)是计算多相[流[体力](@entry_id:136788)](@entry_id:174230)学领域的一块基石，为模拟和理解那些由多个互不相溶的相（如气-液、液-固）组成的复杂系统提供了强大的宏观框架。从核反应堆的安全运行、化工过程的效率优化，到自然灾害的预测，精确描述相间复杂的相互作用至关重要。然而，直接解析每个相界面的动态演化在计算上往往是不可行的。欧拉-欧拉方法通过将各相视为可相互渗透的连续介质，并对控制方程进行平均化处理，巧妙地回避了这一难题，但其代价是引入了必须通过物理模型（即“闭合关系”）来描述的未知相间交换项。

本文旨在系统性地阐述欧拉-欧拉[双流体模型](@entry_id:139846)的理论体系、应用范畴及数值实践中的关键考量。读者将通过本文的学习，构建一个从基本原理到前沿应用的完整知识图谱。在“原理与机制”一章中，我们将深入剖析模型的数学基础，从平均守恒方程出发，详细阐述相间动量、质量和能量交换的核心闭合关系，并介绍处理非平衡、[湍流](@entry_id:151300)和[多分散性](@entry_id:163107)等复杂现象的高级模型框架。接下来，在“应用与跨学科交叉”一章中，我们将通过一系列实际案例，展示该模型如何通过模块化的闭合关系，灵活地应用于[沸腾传热](@entry_id:155823)、空化、[雪崩动力学](@entry_id:269104)乃至非牛顿流体等多样化的科学与工程问题中，凸显其强大的跨学科连接能力。最后，在“动手实践”部分，我们将引导读者思考并解决在数值实现该模型时遇到的典型挑战，如[数值振荡](@entry_id:163720)、[时间步长限制](@entry_id:756010)和解的物理可容许性。

## 原理与机制

在“引言”章节中，我们已经对欧拉-欧拉[双流体模型](@entry_id:139846)的基本思想进行了概述。本章将深入探讨该模型的数学原理和物理机制。我们将从基本的[守恒定律](@entry_id:269268)出发，构建控制[方程组](@entry_id:193238)，并详细阐述封闭这些方程所需的关键物理模型，即相间交换的闭合关系。最后，我们将介绍一些用于处理特定物理现象（如力学非平衡、多相[湍流](@entry_id:151300)和[多分散性](@entry_id:163107)）的高级模型框架。

### 平均守恒方程

欧拉-欧拉方法的核心思想是将互不相溶的多个相（例如，气-液、液-固）均视为可相互渗透的连续介质。在空间中的任意一点，每个相都由其自身的物理量来描述，但这些量是在一个[代表性](@entry_id:204613)单元体积（Representative Elementary Volume, REV）上进行平均的结果。最重要的平均量是**[体积分数](@entry_id:756566)**（volume fraction），记为 $\alpha_k$，它表示在REV中第 $k$ 相所占体积的比例，且满足约束条件 $\sum_k \alpha_k = 1$。其他[相变](@entry_id:147324)量，如密度 $\rho_k$、速度 $\mathbf{u}_k$ 和温度 $T_k$，也都是在各自相所占空间内进行平均后得到的场变量。

通过对每个相的瞬时局部[守恒定律](@entry_id:269268)进行体积平均，我们可以得到宏观的双流体控制[方程组](@entry_id:193238)。这些方程描述了平均量的时空演化，但代价是引入了新的、未知的项，这些项代表了相间界面上的质量、动量和能量交换。

#### 相[质量守恒](@entry_id:204015)

第 $k$ 相的质量守恒（或连续性）方程描述了该相的质量如何因[对流](@entry_id:141806)和相间[质量传递](@entry_id:151080)而改变。其[守恒形式](@entry_id:747710)为：

$$
\frac{\partial (\alpha_k \rho_k)}{\partial t} + \nabla \cdot (\alpha_k \rho_k \mathbf{u}_k) = \Gamma_k
$$

其中，$\alpha_k \rho_k$ 是第 $k$ 相的**偏密度**（partial density），即单位混合物体积中第 $k$ 相的质量。左侧第一项是质量的瞬时变化率，第二项是质量的[对流通量](@entry_id:158187)散度。

右侧的 $\Gamma_k$ 是**相间[质量传递](@entry_id:151080)率**，表示由于蒸发、冷凝等相变过程，单位体积内第 $k$ 相质量的净生成速率。根据总质量守恒，所有相的[质量传递](@entry_id:151080)率之和必须为零，即 $\sum_k \Gamma_k = 0$。

为了封闭方程，我们需要为 $\Gamma_k$ 提供一个物理模型。这个模型通常与[相界面](@entry_id:172947)的微观物理过程相关。例如，考虑一个从相1到相2的净[传质](@entry_id:151908)过程（如蒸发），我们可以定义单位界面面积上的质量通量为 $m_i$（$m_i > 0$ 表示质量从1流向2）。如果单位混合物体积中的[相界面](@entry_id:172947)面积密度为 $a_i$，那么相1的质量[源项](@entry_id:269111)为一个汇项，相2的质量源项为一个[源项](@entry_id:269111)，其大小与总的界面传质速率成正比 [@problem_id:3315422]。具体而言，源项可以表示为：

$$
\Gamma_1 = -a_i m_i, \quad \Gamma_2 = +a_i m_i
$$

这种形式确保了 $\Gamma_1 + \Gamma_2 = 0$，并且其符号与物理过程直观一致：相1失去质量，相2获得质量。

#### 相动量守恒

第 $k$ 相的动量守恒方程是[牛顿第二定律](@entry_id:274217)在可变形、流动的连续介质中的体现：

$$
\frac{\partial (\alpha_k \rho_k \mathbf{u}_k)}{\partial t} + \nabla \cdot (\alpha_k \rho_k \mathbf{u}_k \otimes \mathbf{u}_k) = -\alpha_k \nabla p_k + \nabla \cdot \boldsymbol{\Sigma}_k + \alpha_k \rho_k \mathbf{g} + \mathbf{M}_k
$$

方程左侧是动量的瞬时变化和[对流](@entry_id:141806)项。右侧的项代表了作用在第 $k$ 相上的各种力（单位混合物体积）：
- $-\alpha_k \nabla p_k$ 是由第 $k$ 相内部压力梯度引起的力。
- $\nabla \cdot \boldsymbol{\Sigma}_k$ 是由[粘性应力](@entry_id:261328)和[湍流](@entry_id:151300)[雷诺应力](@entry_id:263788)引起的力。
- $\alpha_k \rho_k \mathbf{g}$ 是重力。
- $\mathbf{M}_k$ 是**相间动量交换项**，代表其他所有相对第 $k$ 相的总作用力。根据牛顿第三定律，这些力成对出现且大小相等、方向相反，因此 $\sum_k \mathbf{M}_k = \mathbf{0}$。

我们来更深入地分析应力项。对于[牛顿流体](@entry_id:263796)，第 $k$ 相的**柯西应力张量**（Cauchy stress tensor）$\boldsymbol{\sigma}_k$ 可以分解为压力和[偏应力](@entry_id:163323)部分：$\boldsymbol{\sigma}_k = -p_k \mathbf{I} + \boldsymbol{\tau}_k$，其中 $\boldsymbol{\tau}_k$ 是**[偏应力张量](@entry_id:267642)**（deviatoric stress tensor），它与流体的形变率有关。对于采用[斯托克斯假设](@entry_id:195909)（Stokes' hypothesis）的线性、各向同性牛顿流体，[偏应力张量](@entry_id:267642)为 [@problem_id:3315470]：

$$
\boldsymbol{\tau}_k = \mu_k \left( \nabla \mathbf{u}_k + (\nabla \mathbf{u}_k)^T - \frac{2}{3}(\nabla \cdot \mathbf{u}_k)\mathbf{I} \right)
$$

其中 $\mu_k$ 是第 $k$ 相的[动力粘度](@entry_id:268228)。

在体积平均的框架下，作用在第 $k$ 相上的总应力力密度是**[偏应力张量](@entry_id:267642)**（partial stress tensor）$\alpha_k \boldsymbol{\sigma}_k$ 的散度。使用[乘法法则](@entry_id:144424)展开，我们可以得到压力和粘性力的具体形式 [@problem_id:3315470]：

$$
\nabla \cdot (\alpha_k \boldsymbol{\sigma}_k) = \nabla \cdot (-\alpha_k p_k \mathbf{I} + \alpha_k \boldsymbol{\tau}_k) = -\alpha_k \nabla p_k - p_k \nabla \alpha_k + \nabla \cdot (\alpha_k \boldsymbol{\tau}_k)
$$

这里出现了两个重要的压力项：$-\alpha_k \nabla p_k$ 是作用在相体（bulk）上的[压力梯度力](@entry_id:262279)，而 $-p_k \nabla \alpha_k$ 是一个**非守恒项**（non-conservative term），它表示作用在[相界面](@entry_id:172947)上的压力。这个力只在[体积分数](@entry_id:756566)存在梯度（即[相界面](@entry_id:172947)的宏观位置）的地方出现。在更复杂的模型中，这里的压力 $p_k$ 可能会被一个专门的**界面压力**（interfacial pressure）$p_I$ 所取代，以更精确地描述界面上的力学平衡。

#### 相[能量守恒](@entry_id:140514)

[能量守恒方程](@entry_id:748978)遵循类似的结构，描述了总能量（内能与动能之和）的变化：

$$
\frac{\partial (\alpha_k \rho_k E_k)}{\partial t} + \nabla \cdot (\alpha_k \rho_k E_k \mathbf{u}_k) = \nabla \cdot (-\alpha_k p_k \mathbf{u}_k + \alpha_k \boldsymbol{\tau}_k \cdot \mathbf{u}_k) + Q_k + \dots
$$

其中 $E_k = e_k + \frac{1}{2}|\mathbf{u}_k|^2$ 是第 $k$ 相单位质量的总能量。方程右侧包括压力和[粘性应力](@entry_id:261328)所做的功、以及**相间能量交换项** $Q_k$。$Q_k$ 包含了相间的[热传导](@entry_id:147831)以及由相间动量交换所做的功。与动量交换类似，总能量必须守恒，因此 $\sum_k Q_k = 0$。

### 相间闭合关系：[双流体模型](@entry_id:139846)的核心

守恒方程本身是不封闭的，因为它们引入了未知的相间交换项（$\Gamma_k$, $\mathbf{M}_k$, $Q_k$ 等）。为这些项提供准确的物理模型——即**闭合关系**（closure laws）——是双流体建模中最关键、最具挑战性的部分。这些模型通常基于微观或介观尺度上的物理现象，如单个气泡或颗粒的动力学。

#### 相间动量交换 $\mathbf{M}_k$

相间动量交换项 $\mathbf{M}_k$ 通常被分解为几个具有明确物理意义的力的叠加 [@problem_id:3315421]。对于一个[分散相](@entry_id:748551)（如气泡或颗粒，标记为 $d$）在连续相（标记为 $c$）中的流动，作用在[分散相](@entry_id:748551)上的力 $\mathbf{M}_d$ 可以写为：

$$
\mathbf{M}_d = \mathbf{M}_D + \mathbf{M}_L + \mathbf{M}_{VM} + \mathbf{M}_{TD} + \dots
$$

其中连续相受到的力为 $\mathbf{M}_c = -\mathbf{M}_d$。

- **曳力 (Drag Force, $\mathbf{M}_D$)**: 这是最主要的相间作用力，它源于两相之间的[相对运动](@entry_id:169798)（滑移速度 $\mathbf{u}_r = \mathbf{u}_d - \mathbf{u}_c$）所引起的压差和粘性摩擦。曳力的方向总是与滑移速度相反，倾向于减小两相的速度差。其典型的形式为：
  $$
  \mathbf{M}_D \propto C_D \rho_c a_i |\mathbf{u}_r| (\mathbf{u}_c - \mathbf{u}_d)
  $$
  其中 $C_D$ 是曳力系数，依赖于相对[雷诺数](@entry_id:136372)等[无量纲参数](@entry_id:169335)。

- **[升力](@entry_id:274767) (Lift Force, $\mathbf{M}_L$)**: 当[分散相](@entry_id:748551)在具有[速度梯度](@entry_id:261686)的流场（[剪切流](@entry_id:266817)）中运动时，会受到一个垂直于滑移速度方向的力，即升力。例如，一个气泡在靠近壁面的液体中上升时，会因液体速度梯度而受到一个推向主流区或壁面的横向力。[升力](@entry_id:274767)的方向与连续相的涡量（vorticity）$\boldsymbol{\omega}_c = \nabla \times \mathbf{u}_c$ 和滑移速度 $\mathbf{u}_r$ 的叉乘相关：
  $$
  \mathbf{M}_L \propto C_L \rho_c \alpha_d (\mathbf{u}_r \times \boldsymbol{\omega}_c)
  $$

- **虚拟质量力 (Virtual Mass Force, $\mathbf{M}_{VM}$)**: 这个力源于一个加速的物体必须同时加速其周围的流体。当[分散相](@entry_id:748551)相对于连续相加速时，连续相会产生一个反作用力来抵抗这种加速。因此，虚拟质量力正比于**相对加速度**，并且其大小与被排开的连续相的质量（即“附加质量”）有关 [@problem_id:3315459]。一个物理上完备且伽利略不变的虚拟质量力模型必须依赖于相对加速度的[物质导数](@entry_id:172646)：
  $$
  \mathbf{M}_{VM} = C_{VM} \rho_c \alpha_d \left( \frac{D\mathbf{u}_c}{Dt} - \frac{D\mathbf{u}_d}{Dt} \right)
  $$
  其中 $D/Dt$ 是物质导数。在更通用的、可以处理相转变的对称形式中，连续相密度 $\rho_c$ 常常被混合密度 $\rho_m$ 替代，并乘以 $\alpha_c \alpha_d$ 因子以保证在任一相消失时力也为零 [@problem_id:3315459]。

- **[湍流弥散](@entry_id:197290)力 (Turbulent Dispersion Force, $\mathbf{M}_{TD}$)**: 在[湍流](@entry_id:151300)中，连续相的速度脉动会对[分散相](@entry_id:748551)产生随机的推力，导致[分散相](@entry_id:748551)从高浓度区域向低浓度区域“弥散”，类似于分子扩散。因此，这个力通常被建模为与[分散相](@entry_id:748551)[体积分数](@entry_id:756566)的负梯度成正比，其大小则与连续相的[湍动能](@entry_id:262712) $k_c$ 有关 [@problem_id:3315421]：
  $$
  \mathbf{M}_{TD} \propto C_{TD} \rho_c k_c (-\nabla \alpha_d)
  $$

### 高级模型框架与闭合概念

标准的[双流体模型](@entry_id:139846)通常基于一些简化假设，如相间瞬时达到力学平衡（压力相等）和热力学平衡（温度相等），以及[分散相](@entry_id:748551)是单尺寸的。为了描述更复杂的物理现象，需要引入更高级的模型框架。

#### 七方程模型：捕捉非平衡物理

在许多快速瞬态过程中，例如激波与多相介质的相互作用，两相的压力可能不相等，即存在**力学非平衡**（mechanical non-equilibrium）。为了捕捉这种现象，需要一个允许两相压力 $p_1$ 和 $p_2$ 不同的模型。**Baer-Nunziato (BN) 七方程模型**就是这类模型的典型代表 [@problem_id:3315447]。

该模型由每个相的质量、动量、[能量守恒方程](@entry_id:748978)（共6个方程）以及一个独立的体积分数[输运方程](@entry_id:756133)组成，总计七个方程。其关键特征在于：

1.  **独立的相压力**: 模型求解两个不同的压[力场](@entry_id:147325) $p_1$ 和 $p_2$。
2.  **体积分数方程**: 体积分数 $\alpha_1$ 的演化由一个独立的方程描述，其[对流](@entry_id:141806)速度为**界面速度** $\mathbf{u}_I$：
    $$
    \frac{\partial \alpha_1}{\partial t} + \mathbf{u}_I \cdot \nabla \alpha_1 = \lambda_p(p_2 - p_1)
    $$
3.  **松弛源项**: [方程组](@entry_id:193238)中包含了驱动系统趋向平衡的**松弛项**（relaxation terms）。上式右侧的压力松弛项使得压力差以有限的速率 $\lambda_p$ 减小。类似地，动量和能量方程中也包含速度和温度的松弛项。
4.  **非守恒项**: 动量和能量方程中的非守恒项（如 $-p_I \nabla \alpha_k$ 和 $-p_I \mathbf{u}_I \cdot \nabla \alpha_k$）是精确描述界面上力和功传递所必需的，它们与界面压力 $p_I$ 和界面速度 $\mathbf{u}_I$ 相关。

这个七方程模型构成了一个[双曲型偏微分方程](@entry_id:144631)组，保证了模型的[适定性](@entry_id:148590)（well-posedness），即解是存在、唯一且稳定的。

#### [双曲性](@entry_id:262766)与刚性松弛极限

一个PDE系统是否**双曲**（hyperbolic）决定了其是否适定。[双曲性](@entry_id:262766)要求系统的[雅可比矩阵](@entry_id:264467)的所有[特征值](@entry_id:154894)都是实数。对于七方程模型，这意味着每个相自身的声速 $c_k$ 必须是实数，这通常与热力学稳定性条件等价。例如，对于**刚性气体[状态方程](@entry_id:274378)**（Stiffened Gas Equation of State） $p_k = (\gamma_k - 1)\rho_k e_k - \gamma_k \pi_k$，声速的平方为 $c_k^2 = \gamma_k (p_k + \pi_k) / \rho_k$。[双曲性](@entry_id:262766)条件即为 $p_k + \pi_k \ge 0$ [@problem_id:3315471]。

在**刚性松弛极限**（stiff relaxation limit）下，即压力松弛速率 $\lambda_p \to \infty$ 时，压力差会瞬时消失，系统被约束在 $p_1 = p_2 = p$ 的平衡[流形](@entry_id:153038)上。在这种情况下，七方程模型退化为一个压力平衡的五方程模型。有趣的是，此时混合物表现出一种新的**有效声速**（effective speed of sound）$c_{\text{eq}}$。这个声速可以通过混合物的有效压缩性推导出来，其结果通常被称为**伍德声速**（Wood's speed of sound） [@problem_id:3315471]：

$$
\frac{1}{\rho_m c_{\text{eq}}^2} = \frac{\alpha_1}{\rho_1 c_1^2} + \frac{\alpha_2}{\rho_2 c_2^2}
$$

其中 $\rho_m = \alpha_1 \rho_1 + \alpha_2 \rho_2$ 是混合物密度。这个公式揭示了一个重要的物理现象：在液体中掺入少量气体，会急剧降低混合物的声速。例如，在常压水中（$c_1 \approx 1500 \text{ m/s}$）加入仅仅10%[体积分数](@entry_id:756566)的气体（$c_2 \approx 340 \text{ m/s}$），混合物的声速会骤降至约 $100 \text{ m/s}$ 的量级。这是因为气体的[可压缩性](@entry_id:144559)远大于液体，主导了整个混合物的[声学](@entry_id:265335)响应。

#### [多相流中的湍流](@entry_id:756225)

在工业应用中，大多数[多相流](@entry_id:146480)都是[湍流](@entry_id:151300)。在RANS (Reynolds-Averaged Navier-Stokes) 框架下模拟[湍流](@entry_id:151300)，需要引入额外的模型，如标准的 $k-\epsilon$ 模型。在[双流体模型](@entry_id:139846)中，存在两种主要方法 [@problem_id:3315450]：

1.  **混合[湍流模型](@entry_id:190404)**: 求解一组基于混合物性质（如混合密度和混合速度）的[湍流输运](@entry_id:150198)方程（例如，针对 $k_m$ 和 $\epsilon_m$）。这种方法假设两相共享相同的[湍流](@entry_id:151300)场，计算成本较低，但物理假设较强。

2.  **分相[湍流模型](@entry_id:190404)**: 为每个相求解其各自的[湍流输运](@entry_id:150198)方程（例如，针对 $k_\ell, \epsilon_\ell$ 和 $k_g, \epsilon_g$）。这种方法更为普适和精确，因为它能捕捉到两相不同的[湍流](@entry_id:151300)特性，但模型更复杂，需要对相间的[湍流](@entry_id:151300)能量交换进行建模。

一个关键的物理现象是**气泡诱导[湍流](@entry_id:151300)**（Bubble-Induced Turbulence, BIT）。当气泡在液体中上升时，其尾迹会产生涡旋，将平均流的动能转化为湍动能，从而增强液相的[湍流](@entry_id:151300)。这种[能量转换](@entry_id:165656)的速率与相间曳力所做的功有关。在分相湍流模型中，这被建模为液相湍动能方程 $k_\ell$ 中的一个源项 $S_k^{\text{BIT}}$：

$$
S_k^{\text{BIT}} \propto \mathbf{M}_\ell \cdot \mathbf{u}_r
$$

其中 $\mathbf{M}_\ell$ 是作用在液相上的相间曳力。为了保持模型的一致性，[湍流耗散率](@entry_id:756234)方程 $\epsilon_\ell$ 中也需要加入一个相应的源项 $S_\epsilon^{\text{BIT}}$。基于[湍流](@entry_id:151300)的时间尺度 ($k_\ell/\epsilon_\ell$)，该[源项](@entry_id:269111)通常被建模为：

$$
S_\epsilon^{\text{BIT}} \propto \frac{\epsilon_\ell}{k_\ell} S_k^{\text{BIT}}
$$

这种处理方式能够物理地描述[分散相](@entry_id:748551)对连续相[湍流](@entry_id:151300)场的额外贡献。

#### 专用闭合关系：[颗粒流](@entry_id:750004)动力学理论 (KTGF)

对于稠密的[颗粒流](@entry_id:750004)（如[流化床](@entry_id:191273)、气力输送），颗粒间的碰撞变得至关重要。**[颗粒流](@entry_id:750004)[动力学理论](@entry_id:136901)** (Kinetic Theory of Granular Flow, KTGF) 提供了一个强大的理论框架来建立这些流动的闭合关系 [@problem_id:3315434]。

KTGF将颗粒的随机脉动运动类比于气体分子的热运动，并引入一个关键概念——**颗粒温度**（granular temperature）$\Theta$。它被定义为单位质量颗粒的脉动动能，即 $\Theta = \frac{1}{3} \langle \mathbf{v}' \cdot \mathbf{v}' \rangle$，其中 $\mathbf{v}'$ 是颗粒的脉动速度。

基于颗粒温度，KTGF可以推导出颗粒相的宏观输运性质，如**颗粒相粘度**（solids-phase viscosity）$\mu_s$ 和**颗粒相体粘度**（solids-phase bulk viscosity）$\lambda_s$。这些粘度通常包含两个部分的贡献：

- **动力学部分 ($\mu_{s,k}$)**: 源于颗粒在两次碰撞之间通过“自由飞行”输运动量，类似于稀疏气体。这部分正比于 $\sqrt{\Theta}$。
- **碰撞部分 ($\mu_{s,c}$)**: 源于颗粒碰撞瞬间的动量交换，在稠密流动中占主导。这部分也正比于 $\sqrt{\Theta}$，并依赖于碰撞的频繁程度（与 $\phi^2 g_0(\phi)$ 相关，其中 $g_0(\phi)$ 是[径向分布函数](@entry_id:171547)）和碰撞的[冲量](@entry_id:178343)（与[恢复系数](@entry_id:170710) $e$ 相关，通常为 $(1+e)$）。

因此，KTGF将微观的颗粒性质（直径 $d_p$、密度 $\rho_p$、[恢复系数](@entry_id:170710) $e$）与介观的流动状态（颗粒温度 $\Theta$、[体积分数](@entry_id:756566) $\phi$）联系起来，为颗粒相的[应力张量](@entry_id:148973)提供了封闭的本构关系 [@problem_id:3315434]。

#### 描述[多分散性](@entry_id:163107)：群体平衡方程 (PBE)

标准[双流体模型](@entry_id:139846)通常假设[分散相](@entry_id:748551)是**单分散**（monodisperse）的，即所有颗粒/气泡/液滴都具有相同的尺寸。然而，在许多实际应用中，[分散相](@entry_id:748551)具有一个尺寸[分布](@entry_id:182848)，并且这个[分布](@entry_id:182848)会因破碎（breakage）和聚并（coalescence）而演化。为了描述这种**多分散**（polydisperse）系统，[双流体模型](@entry_id:139846)需要与**群体平衡方程**（Population Balance Equation, PBE）耦合 [@problem_id:3315454]。

PBE描述了粒子**[数密度](@entry_id:268986)函数**（number density function）$n(v, \mathbf{x}, t)$ 的演化。这里的 $v$ 是一个内部坐标，通常代表粒子的体积或直径。$n(v, \mathbf{x}, t) dv dV$ 表示在时间 $t$、位置 $\mathbf{x}$ 附近的[体积元](@entry_id:267802) $dV$ 内，尺寸在 $[v, v+dv]$ 区间内的粒子数量。

PBE是一个作用于扩展相空间（物理空间+尺寸空间）的[守恒定律](@entry_id:269268)，其[守恒形式](@entry_id:747710)为：

$$
\frac{\partial n}{\partial t} + \nabla_{\mathbf{x}} \cdot (n \mathbf{u}_d) + \frac{\partial}{\partial v} (n G) = B - D
$$

这个方程的各项物理意义明确 [@problem_id:3315454]：
- $\frac{\partial n}{\partial t}$ 是[数密度](@entry_id:268986)的瞬时变化率。
- $\nabla_{\mathbf{x}} \cdot (n \mathbf{u}_d)$ 是粒子在物理空间中由于[对流](@entry_id:141806) $\mathbf{u}_d$ 产生的通量散度。
- $\frac{\partial}{\partial v} (n G)$ 是粒子在尺寸空间中由于连续生长或收缩（速率为 $G=\dot{v}$）产生的“通量”散度。
- $B$ 和 $D$ 分别是由于破碎和聚并事件引起的粒子“出生率”和“死亡率”。

通过求解PBE，可以追踪整个粒子尺寸[分布](@entry_id:182848)的动态演化，并为[双流体模型](@entry_id:139846)提供更精确的相间交换项（因为曳力、[传质](@entry_id:151908)等都强烈依赖于粒子尺寸）。