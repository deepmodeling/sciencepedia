## 引言
[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)是[流体力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)中一个悬而未决的难题，其混沌和多尺度的特性使得从第一性原理直接求解变得异常困难。我们如何才能在不追踪每一个微小涡旋的前提下，对飞机周围的气流或大气中的天气模式进行有效预测？这正是Osborne Reynolds的革命性思想所要解决的核心问题。通过将复杂的瞬时流动分解为平滑的平均部分和随机的脉动部分，[雷诺分解](@keyword=reynolds_decomposition|lang=zh-CN|style=Feynman)为我们提供了一种全新的视角，让我们得以绕开瞬时细节的泥潭，转而捕捉流动的统计规律。然而，这种简化带来了一个新的挑战——雷诺应力的出现以及随之而来的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)“封闭问题”。

本文旨在系统性地介绍[雷诺分解](@keyword=reynolds_decomposition|lang=zh-CN|style=Feynman)以及由此衍生的[雷诺平均](@keyword=reynolds_averaging|lang=zh-CN|style=Feynman)[Navier-Stokes](@keyword=navier_stokes|lang=zh-CN|style=Feynman) (RANS) 方程。通过学习，您将能够理解[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)研究中最核心的建模思想。
- 在**“原理与机制”**一章中，我们将深入探讨[雷诺分解](@keyword=reynolds_decomposition|lang=zh-CN|style=Feynman)的数学形式，揭示雷诺应力作为脉动[动量输运](@keyword=momentum_transport|lang=zh-CN|style=Feynman)的物理本质，并解释为何它会导致[湍流封闭问题](@keyword=turbulence_closure_problem|lang=zh-CN|style=Feynman)。我们还将介绍Boussinesq涡黏度假设这一里程碑式的概念，以及[湍动能](@keyword=turbulent_kinetic_energy|lang=zh-CN|style=Feynman)($k$)和[耗散率](@keyword=dissipation_rate|lang=zh-CN|style=Feynman)($\epsilon$)在[湍流建模](@keyword=turbulence_modeling|lang=zh-CN|style=Feynman)中的关键角色。
- 接下来，**“应用与跨学科连接”**一章将展示[RANS模型](@keyword=rans_models|lang=zh-CN|style=Feynman)如何在航空航天、地球物理流体和燃烧等领域大放异彩，例如解释经典的“[壁面律](@keyword=logarithmic_law_of_the_wall|lang=zh-CN|style=Feynman)”。同时，本章也会剖析其在[旋转流](@keyword=rotational_flow|lang=zh-CN|style=Feynman)、曲率流等复杂情况下的局限性，并阐明为何RANS方法无法捕捉声学或泥沙输运等由瞬时事件主导的现象。
- 最后，**“动手实践”**部分提供了一系列精选的计算与分析问题，旨在帮助您巩固对雷诺应力[可实现性](@keyword=realizability|lang=zh-CN|style=Feynman)、[湍流生成](@keyword=turbulence_production|lang=zh-CN|style=Feynman)机制以及涡黏度模型局限性的理解，将理论知识转化为实践能力。

现在，让我们一同踏上这段从混沌中寻找秩序的旅程，揭开[雷诺平均](@keyword=reynolds_averaging|lang=zh-CN|style=Feynman)方法的神秘面纱。

## 原理与机制

[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)，这个[流体力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)中最后的“未解之谜”，以其变幻莫测的混沌特性挑战着我们。如果我们试[图追踪](@keyword=diagram_chasing|lang=zh-CN|style=Feynman)每一个微小漩涡的每一次翻滚和每一次碰撞，那么即便是最强大的超级计算机也会束手无策。然而，Osborne Reynolds在19世纪末提出了一个天才般的思想，它不求洞悉每一个细节，而是试图捕捉[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的“统计特性”。这个思想，我们称之为**[雷诺分解](@keyword=reynolds_decomposition|lang=zh-CN|style=Feynman)**（Reynolds decomposition），为我们理解和预测[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)打开了一扇全新的大门。

### 流动的双重性格：平均与脉动

想象一条奔腾的河流。它有一个明确的总趋势——从上游流向下游。这是它的**平均流**（mean flow）。但如果你仔细观察，会发现河水充满了各种漩涡、湍动和随机的翻滚。这些是它的**脉动**（fluctuations）。雷诺的洞见在于，任何一个[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)物理量，比如速度$u$，都可以被看作是这两个部分的叠加：

$$
u = \overline{u} + u'
$$

这里，$\overline{u}$是稳定而可预测的平均部分，而$u'$则是瞬息万变、看似随机的脉动部分。这个简单的公式，就是[雷诺分解](@keyword=reynolds_decomposition|lang=zh-CN|style=Feynman)的核心。

那么，我们如何定义这个“平均”呢？一种直观的方式是在空间中的某一点上，架设一台“摄像机”，长时间地记录流速，然后取其时间平均值[@problem_id:3357789]。另一种方式，则更具哲学意味：想象我们能无数次地重复同一个实验，每次实验都是[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的一个“实现”。将所有这些“实现”在同一时刻、同一位置的流速进行平均，我们得到的是**系综平均**（ensemble average）。奇妙的是，对于许多在统计上不随[时间演化](@keyword=time_evolution|lang=zh-CN|style=Feynman)的“定常”[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)，这两种平均方法会得到相同的结果。这个被称为**遍历性**（ergodicity）的性质，是大自然赠予我们的一个礼物，它允许我们用一次长时间的观测来代替无数次的重复实验[@problem_id:3357789]。

通过这个分解，我们将一个复杂得令人望而生畏的问题，拆分成了两个部分：一个是我们希望求解的、相对平滑的平均流场；另一个是我们需要理解其统计效应的[脉动流](@keyword=pulsatile_flow|lang=zh-CN|style=Feynman)场。按照定义，脉动部分的平均值为零，即$\overline{u'}=0$。这看起来似乎让问题变简单了。但当我们把这个分解带入[流体运动](@keyword=fluid_motion|lang=zh-CN|style=Feynman)的基本定律——[Navier-Stokes方程](@keyword=navier_stokes_equation|lang=zh-CN|style=Feynman)时，一个意想不到的“不速之客”出现了。

### 平均的代价：[雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)的诞生

[Navier-Stokes方程](@keyword=navier_stokes_equation|lang=zh-CN|style=Feynman)描述了流体动量的守恒。其中最棘手的一项是**[对流](@keyword=convection|lang=zh-CN|style=Feynman)项**$u_j \frac{\partial u_i}{\partial x_j}$，它描述了流体自身运动所带来的[动量输运](@keyword=momentum_transport|lang=zh-CN|style=Feynman)。这是一个[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)项，因为速度既是被输运的量，也是输运的媒介。正是这个[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)，成为了[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)混沌特性的根源。

当我们对方程进行[雷诺平均](@keyword=reynolds_averaging|lang=zh-CN|style=Feynman)时，那些线性的项都表现得很好，例如，压力的平均就是平均压力。但[对流](@keyword=convection|lang=zh-CN|style=Feynman)项的平均却给我们带来了麻烦。让我们看看对$u_i u_j$这个速度乘积项进行平均会发生什么[@problem_id:3357825]：

$$
\overline{u_i u_j} = \overline{(\overline{u_i} + u_i')(\overline{u_j} + u_j')} = \overline{\overline{u_i}\overline{u_j} + \overline{u_i}u_j' + u_i'\overline{u_j} + u_i'u_j'}
$$

利用平均运算的性质（$\overline{\overline{u_i}\overline{u_j}} = \overline{u_i}\overline{u_j}$ 以及 $\overline{\overline{u_i}u_j'} = \overline{u_i}\overline{u_j'}=0$），我们得到：

$$
\overline{u_i u_j} = \overline{u_i}\overline{u_j} + \overline{u_i'u_j'}
$$

看！平均后的方程中，除了我们期望的[平均速度](@keyword=average_velocity|lang=zh-CN|style=Feynman)的乘积$\overline{u_i}\overline{u_j}$之外，还凭空多出了一项：$\overline{u_i'u_j'}$。这是一个源于脉动速度乘积的平均值。尽管单个脉动的平均值为零，但它们乘积的平均值通常不为零。

这一项被移到方程的另一侧后，其物理效应如同一个额外的应力。我们称其为**[雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)**（Reynolds stress），通常记为$\tau_{ij} = -\rho \overline{u_i'u_j'}$[@problem_id:3382031]。它不是像黏性力那样的真实应力，而是脉动运动对平均流产生的宏观效应，是一种“表观应力”。经过平均后的[Navier-Stokes方程](@keyword=navier_stokes_equation|lang=zh-CN|style=Feynman)，现在被称为**[雷诺平均](@keyword=reynolds_averaging|lang=zh-CN|style=Feynman)[Navier-Stokes](@keyword=navier_stokes|lang=zh-CN|style=Feynman)（RANS）方程**。[雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)的出现，就是我们为简化问题、进行平均所付出的“代价”。

### [雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)是什么？一个关于动量交换的故事

这个神秘的雷诺应力到底是什么？让我们用一个生动的例子来理解它。想象在一个平直的河道中流动的水，越靠近中心流速越快，越靠近河岸流速越慢。现在，考虑两个相邻的水层，A层流速快，B[层流](@keyword=laminar_flow|lang=zh-CN|style=Feynman)速慢[@problem_id:3357820]。

由于[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)脉动，总会有一些水团（fluid parcels）从A层“跳”到B层。这些来自高速区的水团，自身携带了较高的 streamwise (沿主流方向) 动量。当它们混入B层时，就像给B层注入了额外的“推力”。反过来，也会有水团从慢速的B层“跳”到A层，它们携带的较低动量会对A层产生“拖拽”效应。

这种由脉动引起的动量交换，在宏观上看，就表现为快慢水层之间的一种“[摩擦力](@keyword=friction_force|lang=zh-CN|style=Feynman)”。这个“[摩擦力](@keyword=friction_force|lang=zh-CN|style=Feynman)”就是[雷诺切应力](@keyword=reynolds_shear_stress|lang=zh-CN|style=Feynman)。具体来说，如果$x$是主流方向，$y$是垂直于岸壁的方向，那么从A到B的运动对应于一个负的法向脉动速度$v'0$，而它带来的通常是一个正的流向脉动速度$u'>0$。从B到A的运动则相反（$v'>0, u'0$）。在这两种主要情况下，乘积$u'v'$都是负的。因此，在整个流场中，这个相关性$\overline{u'v'}$是一个负值。那么，[雷诺切应力](@keyword=reynolds_shear_stress|lang=zh-CN|style=Feynman)$-\rho \overline{u'v'}$就是一个正值，它切实地在不同流层间传递动量，塑造了平均速度剖面[@problem_id:3357820]。

雷诺应力的法向分量，如$\overline{u'^2}$、$\overline{v'^2}$，则代表了脉动在各个方向上的强度，也就是[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的**各向异性**（anisotropy）。在靠近壁面的地方，壁的存在会“压扁”垂直于壁面的脉动，所以$v'$的强度会远小于平行于壁面的$u'$，[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)呈现出强烈的各向异性。而在远离壁面的流场中心，[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)则趋向于在各个方向上“一视同仁”，即趋向于各向同性[@problem_id:3357820]。

### 封闭问题：永无止境的链条

雷诺应力的出现带来了一个根本性的难题。我们原本的目标是求解平均速度$\overline{u_i}$和平均压力$\overline{p}$，总共有4个未知数，对应4个方程（3个[动量方程](@keyword=momentum_equation|lang=zh-CN|style=Feynman)和1个[连续性方程](@keyword=equation_of_continuity|lang=zh-CN|style=Feynman)）。但现在，[RANS方程](@keyword=rans_equations|lang=zh-CN|style=Feynman)中引入了新的未知数——[雷诺应力张量](@keyword=reynolds_stress_tensor|lang=zh-CN|style=Feynman)$\overline{u_i'u_j'}$的6个独立分量。未知数的数量超过了方程的数量！这个系统在数学上是“不封闭的”。这就是著名的**[湍流封闭问题](@keyword=turbulence_closure_problem|lang=zh-CN|style=Feynman)**（turbulence closure problem）[@problem_id:3382031]。

我们或许会想，能不能为雷诺应力$\overline{u_i'u_j'}$也推导一个控制方程呢？答案是可以的。但这就像打开了一个潘多拉魔盒：在为$\overline{u_i'u_j'}$推导的方程中，又会出现更复杂的未知项，比如脉动速度的三阶相关项$\overline{u_i'u_j'u_k'}$和压力-应变相关项。如果我们再为这些三阶项推导方程，又会引出四阶项……这就形成了一个永无止境的链条。我们必须在某个环节“斩断”这个链条，引入近似关系，这就是**[湍流模型](@keyword=turbulence_models|lang=zh-CN|style=Feynman)**的使命。

### 建模的艺术：Boussinesq猜想

如何斩断这个链条？最经典也最广泛应用的思想来自于 Joseph Boussinesq 的一个天才猜想。他注意到，分子运动通过碰撞传递动量，产生了我们熟悉的黏性应力，其大小与流体的[应变率](@keyword=strain_rate|lang=zh-CN|style=Feynman)成正比。那么，[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)中那些翻滚的漩涡（eddies）不也在传递动量吗？

[Boussinesq假设](@keyword=boussinesq_hypothesis|lang=zh-CN|style=Feynman)，雷诺应力这个“表观应力”可以仿照黏性应力来处理[@problem_id:3357801]。他提出，[雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)的 deviatoric (偏) 部分与平均流的[应变率张量](@keyword=strain_rate_tensor_2|lang=zh-CN|style=Feynman)$S_{ij} = \frac{1}{2} (\frac{\partial \overline{u}_i}{\partial x_j} + \frac{\partial \overline{u}_j}{\partial x_i})$成正比：

$$
-\rho \overline{u_i'u_j'} + \frac{2}{3}\rho k \delta_{ij} = 2 \mu_t S_{ij}
$$

这里的比例系数$\mu_t$被称为**[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)黏度**或**涡黏度**（eddy viscosity）。它不是流体本身的物理属性，而是[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)流动状态的一个特征，反映了[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)脉动混合动量的效率。这个模型之所以是“猜想”或“假设”，是因为它并非从第一性原理推导而来，而是一种基于物理类比的绝妙近似[@problem_id:3357825]。这个模型的优雅之处在于，它必须满足基本的物理约束，比如[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)[旋转不变性](@keyword=rotational_invariance|lang=zh-CN|style=Feynman)（frame indifference），这意味着模型必须依赖于流体的变形（应变），而不是纯粹的[刚体转动](@keyword=solid_body_rotation|lang=zh-CN|style=Feynman)[@problem_id:3357801]。

### [湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)能量的舞蹈：$k$与$\epsilon$

Boussinesq猜想将封闭问题的核心转化为了如何确定涡黏度$\mu_t$。直观地想，脉动越剧烈，涡团越大，动量交换就越高效，$\mu_t$也就越大。我们需要一个量来衡量[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)脉动的剧烈程度。这个量就是**湍动能**（turbulent kinetic energy, TKE），通常用$k$表示[@problem_id:3357779]：

$$
k = \frac{1}{2} \overline{u_i' u_i'} = \frac{1}{2} (\overline{u'^2} + \overline{v'^2} + \overline{w'^2})
$$

$k$代表了单位质量流体中，储存在脉动运动里的[平均动能](@keyword=average_kinetic_energy|lang=zh-CN|style=Feynman)。然而，光有能量还不够。一个充满能量但耗散缓慢的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)，和一个能量中等但耗散迅速的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)，其混合特性是不同的。因此，我们还需要另一个关键量：**湍[动能耗散](@keyword=kinetic_energy_dissipation|lang=zh-CN|style=Feynman)率**（dissipation rate of TKE），$\epsilon$。

$\epsilon$代表了[湍动能](@keyword=turbulent_kinetic_energy|lang=zh-CN|style=Feynman)由于黏性作用转化为内能（热量）的速率。这是[湍流能量级串](@keyword=turbulent_energy_cascade|lang=zh-CN|style=Feynman)（energy cascade）的终点：大尺度涡团从平均流中“窃取”能量，然后破碎成更小的涡团，能量逐级传递，最终在极小的尺度上（柯尔莫哥洛夫尺度），黏性力占据主导，将这些动能彻底“磨”成热量[@problem_id:3357779]。在一个没有外界能量输入的孤立[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)系统中，TKE的衰减率就等于[耗散率](@keyword=dissipation_rate|lang=zh-CN|style=Feynman)：$\frac{dk}{dt} = -\epsilon$[@problem_id:3357779]。

有了$k$和$\epsilon$，我们就可以构建涡黏度的表达式，例如，在著名的**标准$k-\epsilon$模型**中，$\mu_t = C_\mu \rho \frac{k^2}{\epsilon}$，其中$C_\mu$是一个经验常数[@problem_id:3382031]。通过为$k$和$\epsilon$分别建立输运方程，我们最终得到一个封闭的[方程组](@keyword=simultaneous_equations|lang=zh-CN|style=Feynman)，从而能够求解平均流场。

### 更深层次的观察：应力的内在生命

涡黏度模型虽然强大，但它是一个巨大的简化。它假设[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)脉动对动量的输运是顺着梯度的，即总是从高处流向低处，就像热量传导一样。但[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)的内部世界远比这更复杂。

在[雷诺应力](@keyword=reynolds_stresses|lang=zh-CN|style=Feynman)自身的[输运方程](@keyword=transport_equations|lang=zh-CN|style=Feynman)中，有一个至关重要的项叫做**压力-应变相关项**（pressure-strain correlation term），$\phi_{ij}$ [@problem_id:3357785]。这一项描述了脉动压力$p'$如何与脉动[应变率](@keyword=strain_rate|lang=zh-CN|style=Feynman)相互作用。它的一个神奇特性是，其迹为零（$\phi_{ii}=0$）。这意味着它本身不产生也不耗散总的湍动能$k$。那么它做什么呢？它扮演着能量“再分配”的角色[@problem_id:3357785]。

想象一下，在靠近壁面的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)中，主流方向的脉动$u'$从平均流的剪切中获得了大量能量，变得异常“肥胖”，而垂直壁面的脉动$v'$则因壁的阻挡而“营养不良”。此时，$\phi_{ij}$就会起作用，它像一个公平的仲裁者，将能量从过强的$u'$脉动中“抽取”一部分，转移给较弱的$v'$和$w'$脉动，从而有一种趋势使[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)回归各向同性。

更重要的是，压[力场](@keyword=force_field|lang=zh-CN|style=Feynman)具有**非局部性**（non-locality）[@problem_id:3357788]。某一点的压力脉动是由整个流场的速度[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)通过一个椭圆形的泊松方程决定的。这意味着，一个远处的壁面或者河道的拐弯，可以通过压[力场](@keyword=force_field|lang=zh-CN|style=Feynman)“鬼魅般”地影响到当前点的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)结构。这种“超距作用”是涡黏度模型这类局部模型无法捕捉的。这也解释了为何在处理具有强烈旋转、弯曲或浮力效应的[复杂流动](@keyword=complex_flows|lang=zh-CN|style=Feynman)时，我们需要更高级的、直接对雷诺应力进行建模的**[雷诺应力模型](@keyword=reynolds_stress_models|lang=zh-CN|style=Feynman)**（RSM）。

从一个简单的平均思想出发，我们踏上了一段揭示[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)内在秩序的旅程。我们发现了雷诺应力，遭遇了封闭问题，并学会了用智慧的物理模型来近似求解。这条路充满了精妙的物理洞察与数学构造，它向我们展示了科学如何在混沌中寻找规律，并最终驯服自然界最桀骜不驯的现象之一。