## 引言
在计算燃烧学及更广泛的流体科学领域，精确描述流体的运动、热量传递和化学反应是核心挑战。所有这些复杂现象都受制于一组基本的物理定律：质量、动量、能量和[组分守恒](@entry_id:197272)。这些守恒方程构成了我们理解、预测和模拟反应流行为的数学基石，无论是在内燃机、航空发动机的设计中，还是在火灾安全与环境科学的研究中，都扮演着不可或缺的角色。

然而，将这些物理原理转化为一套可解的、适用于复杂工程问题的数学方程组，并非一件直截了当的事情。本文旨在系统性地解决这一问题，为读者构建一个从基本理论到实际应用的完整知识框架。文章将分为三个核心部分：首先，在“原理与机制”一章中，我们将从第一性原理出发，利用[雷诺输运定理](@entry_id:191217)和高斯散度定理，严谨地推导守恒方程的积分与[微分形式](@entry_id:146747)，并阐明封闭这些方程所需的本构关系。

接着，在“应用与跨学科联系”一章中，我们将展示这些看似抽象的方程如何被应用于简化和建模多样化的物理现象，从[准一维喷管流](@entry_id:267550)到高速激波，再到湍流模拟和宏大的[地球系统模型](@entry_id:1124096)，揭示其作为连接不同学科的通用语言的威力。最后，通过“动手实践”部分，读者将有机会运用所学知识解决具体的分析与计算问题，从而加深对理论的理解。通过这一结构化的学习路径，本文将引导读者全面掌握描述反应流的核心数学物理工具。

## 原理与机制

在理解反应流的复杂性时，我们必须首先建立一个描述其行为的数学框架。该框架基于几个基本的物理守恒定律：[质量守恒](@entry_id:204015)、[动量守恒](@entry_id:149964)、能量守恒以及化学组分的[质量守恒](@entry_id:204015)。本章旨在从第一性原理出发，系统地推导这些守恒定律的积分和微分形式，并阐明描述流体输运和化学反应所需的关键机制和[本构关系](@entry_id:186508)。我们将首先介绍适用于任何[守恒量](@entry_id:161475)的通用[输运定理](@entry_id:176504)，然后将其应用于推导具体的守恒方程，并最终讨论封闭这些方程所需的模型。

### 输运的基本原理

在[连续介质力学](@entry_id:155125)中，我们可以在两种参考系下描述物理量的变化：一种是跟随特定流体团的**拉格朗日（Lagrangian）**观点，另一种是观察固定空间区域内[流体性质](@entry_id:200256)变化的**欧拉（Eulerian）**观点。为了将适用于流体系统（即一组固定的流体粒子）的物理定律转化为在计算中更方便的固定或[移动控制体](@entry_id:265261)（control volume）中的形式，我们需要一个普适的数学工具。

#### [雷诺输运定理](@entry_id:191217)

**[雷诺输运定理](@entry_id:191217) (Reynolds Transport Theorem, RTT)** 提供了拉格朗日和[欧拉描述](@entry_id:264722)之间的桥梁。它将一个[广延性质](@entry_id:145410) $B$ 在一个随流体运动的物质系统（material system）中的总时间变化率（即物质导数 $\frac{DB_{sys}}{Dt}$），与在一个[固定控制体](@entry_id:272149)（control volume）中的变化关联起来。

考虑一个[广延性质](@entry_id:145410) $B$，它由某个单位质量的物理量（或称比性质，specific property）$\beta$ 定义，即 $B(t) = \int_{V(t)} \rho \beta \, dV$，其中 $\rho$ 是流体密度。

对于一个固定在空间中的控制体 $V$（其边界为 $S$），[雷诺输运定理](@entry_id:191217)指出：
$$
\frac{DB_{sys}}{Dt} = \frac{d}{dt} \int_V \rho \beta \, dV + \oint_S \rho \beta (\mathbf{u} \cdot \mathbf{n}) \, dA
$$
其中 $\mathbf{u}$ 是[流体速度](@entry_id:267320)，$\mathbf{n}$ 是指向外部的[单位法向量](@entry_id:178851)。这个方程的物理意义是：物质系统中[广延性质](@entry_id:145410)的总变化率，等于控制体内部该性质的时间变化率，加上流出控制体的净通量。由于控制体是固定的，时间导数可以移到积分号内部：
$$
\frac{DB_{sys}}{Dt} = \int_V \frac{\partial (\rho\beta)}{\partial t} \, dV + \oint_S \rho \beta (\mathbf{u} \cdot \mathbf{n}) \, dA
$$
这个关系是推导所有[守恒方程](@entry_id:1122898)积分形式的出发点。它将一个系统（[拉格朗日观点](@entry_id:1127015)）的守恒定律（例如，对于质量守恒，$\frac{DB_{sys}}{Dt}=0$）转换为了一个适用于固定观测区域（[欧拉观点](@entry_id:198701)）的方程。

#### 高斯散度定理

从守恒定律的积分形式过渡到其[微分](@entry_id:158422)（或局部）形式，需要一个核心的数学工具——**[高斯散度定理](@entry_id:188065) (Gauss's divergence theorem)**。该定理建立了穿过一个封闭曲面的矢量场的通量与该矢量场在曲面所包围体积内的散度的积分之间的关系 。

对于一个有界区域 $V \subset \mathbb{R}^3$，其边界 $S = \partial V$ 是分片光滑的，单位外[法向量](@entry_id:264185)为 $\mathbf{n}$。如果一个矢量场 $\mathbf{F}$ 在包含 $V$ 的一个开集上是连续可微的，则[高斯散度定理](@entry_id:188065)表明：
$$
\oint_S \mathbf{F} \cdot \mathbf{n} \, dS = \int_V \nabla \cdot \mathbf{F} \, dV
$$
其中 $\nabla \cdot \mathbf{F}$ 是矢量场 $\mathbf{F}$ 的**散度**。在物理上，散度衡量了矢量场在某一点的源或汇的强度。

此定理的强大之处在于，它允许我们将一个涉及边界面上通量的表面积分，转化为一个涉及整个体积内性质的体积积分。在推导守恒方程时，输运项通常表现为表面积分。通过应用散度定理，我们可以将所有项都写成体积积分的形式。由于该积分等式必须对任意选择的控制体 $V$ 都成立，因此被积函数本身必须处处为零。这正是从宏观的积分守恒定律得到微观的[微分](@entry_id:158422)[守恒方程](@entry_id:1122898)的逻辑飞跃。例如，在[组分守恒](@entry_id:197272)中，总通量矢量为 $\mathbf{F} = \rho Y_k \mathbf{u} + \mathbf{J}_k$，应用[散度定理](@entry_id:143110)可得：
$$
\int_S \left( \rho Y_k \mathbf{u} + \mathbf{J}_k \right) \cdot \mathbf{n} \, dS = \int_V \nabla \cdot \left( \rho Y_k \mathbf{u} + \mathbf{J}_k \right) \, dV
$$
这个转换是后续所有[微分](@entry_id:158422)方程推导的基础。

### 守恒方程

装备了雷诺输运定理和高斯散度定理，我们现在可以系统地推导质量、组分、动量和能量的[守恒方程](@entry_id:1122898)。我们将对每个守恒定律采用相同的推导路径：从基本物理原理出发，应用RTT得到积分形式，再应用散度定理得到微分形式。

#### 质量守恒：连续性方程

物理原理是**质量守恒定律**：一个封闭物质系统（即固定的一组流体粒子）的总质量不随时间改变。数学上，$\frac{D M_{sys}}{Dt} = 0$。

我们将[雷诺输运定理](@entry_id:191217)应用于总质量。此时，[广延性质](@entry_id:145410) $B$ 就是总质量 $M$，相应的比性质 $\beta$ 是单位质量的质量，即 $\beta = 1$。对于一个固定的控制体 $V$，我们有：
$$
\frac{D M_{sys}}{Dt} = \frac{d}{dt} \int_V \rho \cdot 1 \, dV + \oint_S \rho \cdot 1 (\mathbf{u} \cdot \mathbf{n}) \, dS = 0
$$
这是质量守恒的**积分形式**，它表明控制体内质量的增加率等于净流入控制体的质量流率。

为了得到[微分形式](@entry_id:146747)，我们将时间导数移入积分内（因为控制体是固定的），并对表面积分应用高斯散度定理：
$$
\int_V \frac{\partial \rho}{\partial t} \, dV + \int_V \nabla \cdot (\rho \mathbf{u}) \, dV = \int_V \left( \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) \right) dV = 0
$$
由于此式对任意控制体 $V$ 均成立，被积函数必须处处为零。这就得到了质量守恒的**[微分形式](@entry_id:146747)**，即**[连续性方程](@entry_id:195013) (continuity equation)**：
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0
$$
这个方程描述了任意一点处密度的局部变化与其质量[通量散度](@entry_id:1125154)之间的关系。

一个重要的问题是，为什么在化学反应流中，混合物的连续性方程没有包含化学反应源项？毕竟，化学反应会消耗一些组分并生成另一些组分。答案可以通过加总所有组分的[质量守恒](@entry_id:204015)方程来揭示 。单个组分 $k$ 的[守恒方程](@entry_id:1122898)（我们将在下一节推导）包含对流、扩散和化学反应源项 $\dot{\omega}_k$。将所有组分的方程相加：
$$
\sum_k \left( \frac{\partial \rho_k}{\partial t} + \nabla \cdot (\rho_k \mathbf{u} + \mathbf{J}_k) \right) = \sum_k \dot{\omega}_k
$$
其中 $\rho_k$ 是组分 $k$ 的分密度，$\mathbf{J}_k$ 是其[扩散通量](@entry_id:748422)。通过利用混合物密度 $\rho = \sum_k \rho_k$ 和[质量平均速度](@entry_id:149575)的定义，上式可以整理为：
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = \sum_k \dot{\omega}_k - \nabla \cdot \left(\sum_k \mathbf{J}_k\right)
$$
方程右侧的两项恰好都恒等于零。首先，由于化学反应只是原子的重新排列，总质量必须守恒，因此所有组分的净[质量生成](@entry_id:161427)率之和为零，即 $\sum_k \dot{\omega}_k = 0$。其次，根据[质量平均速度](@entry_id:149575)的定义，所有组分相对于[质量平均速度](@entry_id:149575)的扩散质量通量之和也必须为零，即 $\sum_k \mathbf{J}_k = \mathbf{0}$。因此，混合物连续性方程的右侧为零，不含源项。只有当存在相变（如[液滴蒸发](@entry_id:748678)）或外部质量注入等跨相[质量传递](@entry_id:151080)时，混合物[连续性方程](@entry_id:195013)才会出现非零源项。

#### [组分守恒](@entry_id:197272)：[组分输运方程](@entry_id:1132067)

对于多组分反应流，我们还需要追踪每种化学组分的质量。组分 $k$ 的质量守恒原理是：控制体内组分 $k$ 的质量变化率，等于通过边界的净输运率，加上由于化学反应在体积内的净生成率。

组分 $k$ 的质量为 $M_k = \int_V \rho Y_k \, dV$，其中 $Y_k$ 是组分 $k$ 的质量分数。组分 $k$ 的总通量包括**[对流通量](@entry_id:158187)**（随主流体运动）$\rho Y_k \mathbf{u}$ 和**扩散通量**（相对于主流体的运动）$\mathbf{J}_k$。化学反应的净生成率为 $\dot{\omega}_k$（单位体积单位时间生成的质量）。

根据守恒原理，积分形式的方程为 ：
$$
\frac{d}{dt} \int_V \rho Y_k \, dV = - \oint_S (\rho Y_k \mathbf{u} + \mathbf{J}_k) \cdot \mathbf{n} \, dS + \int_V \dot{\omega}_k \, dV
$$
将所有项移到一边，并应用高斯散度定理，我们得到：
$$
\int_V \left( \frac{\partial (\rho Y_k)}{\partial t} + \nabla \cdot (\rho Y_k \mathbf{u} + \mathbf{J}_k) - \dot{\omega}_k \right) dV = 0
$$
由于 $V$ 的任意性，我们得到**[组分输运方程](@entry_id:1132067) (species transport equation)** 的[微分形式](@entry_id:146747)：
$$
\frac{\partial (\rho Y_k)}{\partial t} + \nabla \cdot (\rho Y_k \mathbf{u} + \mathbf{J}_k) = \dot{\omega}_k
$$
这个方程是[守恒形式](@entry_id:1122899)的，各项的物理意义如下：
*   $\frac{\partial (\rho Y_k)}{\partial t}$：**瞬态累积项**，表示单位体积内组分 $k$ 质量的[局部变化率](@entry_id:264961)。
*   $\nabla \cdot (\rho Y_k \mathbf{u})$：**对流项**，表示由于宏观流动导致的组分 $k$ 质量的净流出率。
*   $\nabla \cdot \mathbf{J}_k$：**扩散项**，表示由于分子扩散导致的组分 $k$ 质量的净流出率。
*   $\dot{\omega}_k$：**源项**，表示由于化学反应导致的单位体积内组分 $k$ 质量的净生成率。

这个方程引入了两个新的未知量，扩散通量 $\mathbf{J}_k$ 和[化学源项](@entry_id:747323) $\dot{\omega}_k$，它们需要通过**封闭模型**来与主要变量（如密度、温度和[组分浓度](@entry_id:197022)）联系起来。

#### 动量守恒：[Navier-Stokes](@entry_id:276387) 方程

[动量守恒](@entry_id:149964)源于牛顿第二定律：一个物质系统的总动量的时间变化率等于作用在其上的所有外力之和。这些力包括作用于整个体积的**[体力](@entry_id:174230) (body forces)**（如重力）和作用于其表面的**面力 (surface forces)**（如压力和[粘性力](@entry_id:263294)）。

对于一个控制体 $V$，系统的动量为 $\int_V \rho \mathbf{u} \, dV$。作用在流体上的面力可以通过**柯西应力张量 (Cauchy stress tensor)** $\boldsymbol{\sigma}$ 来描述。$\boldsymbol{\sigma}$ 作用在[单位法向量](@entry_id:178851)为 $\mathbf{n}$ 的表面元素上产生的力为 $\boldsymbol{\sigma} \cdot \mathbf{n}$。[应力张量](@entry_id:148973)通常分解为各向同性的压力部分和[偏应力](@entry_id:163323)部分，后者即**粘性应力张量 (viscous stress tensor)** $\boldsymbol{\tau}$：$\boldsymbol{\sigma} = -p \mathbf{I} + \boldsymbol{\tau}$，其中 $p$ 是[热力学压力](@entry_id:1133073)，$\mathbf{I}$ 是单位张量。

将雷诺输运定理应用于动量（比性质 $\beta = \mathbf{u}$），并考虑[体力](@entry_id:174230)和面力，我们得到[动量守恒](@entry_id:149964)的积分形式：
$$
\frac{d}{dt} \int_V \rho \mathbf{u} \, dV + \oint_S (\rho \mathbf{u} \otimes \mathbf{u}) \cdot \mathbf{n} \, dS = \oint_S \boldsymbol{\sigma} \cdot \mathbf{n} \, dS + \int_V \rho \mathbf{g} \, dV
$$
其中 $\mathbf{u} \otimes \mathbf{u}$ 是速度并矢，代表动量的对流输运；$\mathbf{g}$ 是单位质量的[体力](@entry_id:174230)。

应用[高斯散度定理](@entry_id:188065)的张量形式，并将 $\boldsymbol{\sigma}$ 的分解代入，经过整理可以得到**[动量守恒](@entry_id:149964)方程**，也即**[Navier-Stokes](@entry_id:276387) 方程**的守恒形式 ：
$$
\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \otimes \mathbf{u}) = -\nabla p + \nabla \cdot \boldsymbol{\tau} + \rho \mathbf{g}
$$
为了在计算中获得更好的守恒性，通常将所有通量项都写在同一个[散度算子](@entry_id:265975)下：
$$
\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \otimes \mathbf{u} + p \mathbf{I} - \boldsymbol{\tau}) = \rho \mathbf{g}
$$
这个方程描述了动量的瞬态变化、对流输运、压力[梯度力](@entry_id:166847)、[粘性力](@entry_id:263294)以及体力之间的平衡。这里，粘性应力张量 $\boldsymbol{\tau}$ 是一个新的未知量，需要[封闭模型](@entry_id:1122505)。

#### 能量守恒：能量方程

能量守恒是[热力学第一定律](@entry_id:146485)的体现。对于一个流体系统，其总能量（内能与动能之和）的变化等于外界对系统做的功和传递给系统的热量之和。在燃烧学中，使用焓（enthalpy）来表示能量通常更为方便，特别是对于[低马赫数](@entry_id:1127478)、定压过程。

一个完整的能量方程推导相当复杂，它包含动能、内能、[热传导](@entry_id:143509)、组分扩散带来的焓输运、[粘性耗散](@entry_id:143708)以及化学[反应热](@entry_id:140993)等多个方面。我们可以从一个适用于燃烧问题的简化形式入手，以理解其核心物理。考虑一个[稳态](@entry_id:139253)、一维的流动，[总能量方程](@entry_id:1133263)可以表示为[总焓](@entry_id:197863) $h_{tot} = h + \frac{1}{2}u^2$ 的守恒，其中 $h$ 是混合物的比显焓 (specific sensible enthalpy)。

对于[稳态](@entry_id:139253)一维火焰，能量平衡可以写作 ：
$$
\frac{d}{dx}(\rho u h) = -\frac{dq_x}{dx} + \dot{Q}_{visc} + \dot{Q}_{chem}
$$
左边是对流项，右边是热通量的散度、[粘性耗散](@entry_id:143708)和化学反应放热率。热通量 $q_x$ 包含两部分：由温度梯度引起的**傅里叶[热传导](@entry_id:143509)**和由组分扩散引起的**焓输运**：
$$
q_x = -\lambda \frac{dT}{dx} + \sum_k J_{k,x} h_k
$$
其中 $\lambda$ 是热导率，$h_k$ 是组分 $k$ 的比显焓。在许多燃烧问题中，粘性耗散 $\dot{Q}_{visc}$ 可以忽略。代入热通量表达式，我们得到一维[稳态](@entry_id:139253)能量方程的焓形式：
$$
\rho u \frac{dh}{dx} = \frac{d}{dx}\left(\lambda \frac{dT}{dx}\right) - \frac{d}{dx}\left(\sum_k h_k J_{k,x}\right) + \dot{Q}_{chem}
$$
这个方程清楚地展示了对流、[热传导](@entry_id:143509)、焓扩散和[化学热释放](@entry_id:1122340)之间的平衡。它引入了热通量（需要 $\lambda$ 的模型）和扩散通量（需要 $J_k$ 的模型）。

### 封闭模型：[本构关系](@entry_id:186508)

至此，我们推导出的守恒方程组（连续性、组分、动量、能量）包含了一些非基本变量的通量项（$\boldsymbol{\tau}, \mathbf{q}, \mathbf{J}_k$）和源项（$\dot{\omega}_k$）。为了使方程组封闭可解，我们必须建立这些项与基本变量（$\rho, \mathbf{u}, T, Y_k$）之间的关系。这些关系被称为**本构关系 (constitutive relations)** 或封闭模型。

#### 粘性应力张量

对于**牛顿流体 (Newtonian fluid)**，粘性应力被假定为与应变率张量 $\mathbf{S} = \frac{1}{2}[\nabla \mathbf{u} + (\nabla \mathbf{u})^{\top}]$ 呈线性关系。对于可压缩流体，最一般的线性各向同性关系为：
$$
\boldsymbol{\tau} = 2\mu \mathbf{S} + \kappa (\nabla \cdot \mathbf{u}) \mathbf{I} = \mu [\nabla \mathbf{u} + (\nabla \mathbf{u})^{\top}] + \kappa (\nabla \cdot \mathbf{u}) \mathbf{I}
$$
其中 $\mu$ 是[动力粘度](@entry_id:268228)（或剪切粘度），$\kappa$ 是[体胀](@entry_id:268293)粘度 (bulk viscosity)。

在大多数工程应用中，**[斯托克斯假设](@entry_id:195909) (Stokes' hypothesis)** 被采用，该假设认为[体胀](@entry_id:268293)粘度为零，即 $\kappa = 0$。这等价于假设在流体快速压缩或膨胀时没有额外的熵产生。在某些文献中，[体胀](@entry_id:268293)粘度由[第二粘度](@entry_id:189253)系数 $\lambda$ 表示，关系为 $\kappa = \lambda + \frac{2}{3}\mu$。因此，[斯托克斯假设](@entry_id:195909)等价于 $\lambda = -\frac{2}{3}\mu$。代入这个关系，我们得到可压缩牛顿流体的粘性应力张量表达式 ：
$$
\boldsymbol{\tau} = \mu \left[\nabla \mathbf{u} + (\nabla \mathbf{u})^{\top}\right] - \frac{2}{3}\mu (\nabla \cdot \mathbf{u}) \mathbf{I}
$$
这个模型封闭了[动量方程](@entry_id:197225)中的粘性项。[动力粘度](@entry_id:268228) $\mu$ 本身通常是温度和组分的函数。

#### 热通量矢量

如前所述，热通量矢量 $\mathbf{q}$ 主要由两部分贡献：
$$
\mathbf{q} = \mathbf{q}_{cond} + \mathbf{q}_{diff}
$$
第一部分是[热传导](@entry_id:143509)，由**[傅里叶定律](@entry_id:136311) (Fourier's Law)** 描述，即热量从高温区域流向低温区域，速率与温度梯度成正比：
$$
\mathbf{q}_{cond} = -\lambda \nabla T
$$
其中 $\lambda$ 是热导率。在燃烧等高温应用中，[热导](@entry_id:189019)率 $\lambda$ 强烈依赖于温度，通常随温度升高而增大。这种依赖性会对[能量输运](@entry_id:183081)产生显著影响 。例如，[热传导](@entry_id:143509)项的散度变为：
$$
\nabla \cdot (-\lambda \nabla T) = -\nabla \lambda \cdot \nabla T - \lambda \nabla^2 T = - \frac{d\lambda}{dT} |\nabla T|^2 - \lambda \nabla^2 T
$$
与常数 $\lambda$ 的情况相比，多出的一项 $- \frac{d\lambda}{dT} |\nabla T|^2$ 是[非线性](@entry_id:637147)的。由于在气体中 $\frac{d\lambda}{dT} > 0$，这一项总是负的（或零），意味着它在温度梯度大的区域（如火焰锋面）充当一个额外的热汇，增强了从高温区到低温区的热量输运。

热通量的第二部分是由于不同组分扩散速率不同而引起的焓输运：
$$
\mathbf{q}_{diff} = \sum_k h_k \mathbf{J}_k
$$
这一项将能量方程与组分[扩散耦合](@entry_id:155952)起来。

#### 组分扩散通量矢量

组分[扩散通量](@entry_id:748422)的建模是计算燃烧学中最具挑战性的部分之一，因为它涉及复杂的多组分相互作用。

最简单的模型是**[菲克定律](@entry_id:155177) (Fick's Law)** 的推广，即**混合物平均模型 (mixture-averaged model)**。该模型假设每种组分的[扩散通量](@entry_id:748422)只与其自身的浓度梯度成正比 ：
$$
\mathbf{J}_k^{\text{Fick}} = -\rho D_{k,m} \nabla Y_k
$$
其中 $D_{k,m}$ 是组分 $k$ 在混合物中的有效扩散系数。然而，这个简单的形式不能自动满足 $\sum_k \mathbf{J}_k = \mathbf{0}$ 的约束。为了强制满足该约束，必须引入一个**修正速度 (correction velocity)**，使得最终的扩散通量为：
$$
\mathbf{J}_k = -\rho D_{k,m} \nabla Y_k + Y_k \sum_{j=1}^N \rho D_{j,m} \nabla Y_j
$$
混合物平均模型在所有组分的扩散特性相似（即所有**刘易斯数 (Lewis number)** $Le_k = \lambda / (\rho c_p D_k)$ 都接近1）时是较好的近似。

然而，在许多燃烧现象中，尤其是有轻质组分（如氢气 $\mathrm{H}_2$）存在的火焰中，不同组分的扩散速率差异巨大。此时，更复杂的物理效应变得重要：
1.  **[索雷效应](@entry_id:146479) (Soret effect)** 或**热扩散 (thermal diffusion)**：由温度梯度驱动的质量扩散。通常，轻分子倾向于向高温区扩散，而重分子倾向于向低温区扩散。包含[热扩散](@entry_id:148740)的扩散通量模型可以写为 ：
    $$
    \mathbf{J}_k = -\rho D_{k,m} \nabla Y_k - D_{k}^T \nabla \ln T
    $$
    其中 $D_{k}^T$ 是[热扩散](@entry_id:148740)系数。对于氢气，其质量远小于空气中的氮气和氧气，因此它会强烈地向火焰的高温区扩散。在贫燃氢气火焰中，这种效应会使燃料在反应区富集，从而显著提高[层流火焰速度](@entry_id:202145)，并使火焰锋面变薄。

2.  **[多组分扩散](@entry_id:1128256) (Multicomponent diffusion)**：更严格的理论，如**斯特藩-麦克斯韦方程 (Stefan-Maxwell equations)**，描述了每种组分的扩散不仅受自身梯度影响，还受所有其他组分梯度的影响（交叉扩散）。在刘易斯数差异很大的情况下，例如氢气火焰（$Le_{\mathrm{H}_2} \ll 1$）中，忽略这些交叉项的混合物平均模型会失去准确性，无法预测诸如优先扩散、[火焰拉伸](@entry_id:186928)响应和熄火等关键现象 。对于一个[二元混合物](@entry_id:168452)，斯特藩-麦克斯韦方程可以精确简化为菲克形式，此时混合物平均模型是精确的。但在三组分及以上的系统中，它始终是一个近似。

#### 化学反应源项

[组分守恒方程](@entry_id:151288)中的源项 $\dot{\omega}_k$ 描述了化学反应对组分 $k$ 质量的净生成或消耗速率。它由所有涉及该组分的[基元反应](@entry_id:177550)的贡献加总而成。

对于一个由 $N_r$ 个[基元反应](@entry_id:177550)组成的反应机理，组分 $k$ 的质量源项可以表示为 ：
$$
\dot{\omega}_k = W_k \sum_{r=1}^{N_r} \nu_{k,r} \mathcal{R}_r
$$
这里的各项定义如下：
*   $W_k$ 是组分 $k$ 的摩尔质量 (mass/mole)。
*   $\mathcal{R}_r$ 是第 $r$ 个反应的**净[反应速率](@entry_id:185114) (net rate of progress)**，单位是 (moles/volume/time)。它由正向[反应速率](@entry_id:185114)减去逆向[反应速率](@entry_id:185114)得到，通常由**[质量作用定律](@entry_id:916274) (law of mass action)** 给出。
*   $\nu_{k,r}$ 是组分 $k$ 在反应 $r$ 中的**[化学计量系数](@entry_id:204082) (stoichiometric coefficient)**。这是一个无量纲的纯数，其符号约定至关重要：
    *   对于**产物**，$\nu_{k,r} > 0$。
    *   对于**反应物**，$\nu_{k,r}  0$。
    *   对于不参与反应的组分，$\nu_{k,r} = 0$。

例如，对于反应 $2\mathrm{H}_2 + \mathrm{O}_2 \rightarrow 2\mathrm{H}_2\mathrm{O}$，计量系数分别为 $\nu_{\mathrm{H}_2} = -2$, $\nu_{\mathrm{O}_2} = -1$, $\nu_{\mathrm{H}_2\mathrm{O}} = 2$。这种约定确保了当一个反应净向正方向进行时（$\mathcal{R}_r  0$），产物的源项为正（生成），反应物的源项为负（消耗）。同时，只要每个基元反应本身是[质量平衡](@entry_id:181721)的，这种形式就能保证总质量守恒，即 $\sum_k \dot{\omega}_k = 0$。

### 应用：一维预混火焰的结构

为了将上述原理和模型联系在一起，我们考虑一个理想化但极具启发性的例子：[稳态](@entry_id:139253)、一维、平面的预混火焰。在这种火焰中，燃料和氧化剂在进入反应区之前已经均匀混合。火焰结构通常分为三个区域：未燃混合物区、[预热](@entry_id:159073)区和反应/已燃区。

让我们专注于预热区 。在这个区域，温度开始从初始的未燃温度 $T_u$ 上升，但还不足以引发显著的化学反应。因此，我们可以做出如下简化：
1.  [化学反应速率](@entry_id:147315)为零，即 $\dot{Q}_{chem} = 0$ 和 $\dot{\omega}_k = 0$。
2.  由于没有反应，组分质量分数保持不变，这意味着[扩散通量](@entry_id:748422) $J_{k,x}$ 为零（假设没有[热扩散](@entry_id:148740)）。

在这些假设下，[稳态](@entry_id:139253)一维能量方程简化为：
$$
\rho u \frac{dh}{dx} = \frac{d}{dx}\left(\lambda \frac{dT}{dx}\right)
$$
如果我们进一步假设混合物的比热 $c_p$ 是常数，那么 $dh = c_p dT$。再假设在一维[稳态流](@entry_id:275664)动中质量通量 $\dot{m} = \rho u$ 和热导率 $\lambda$ 在预热区内为常数，方程变为一个[二阶常微分方程](@entry_id:204212)：
$$
\dot{m} c_p \frac{dT}{dx} = \lambda \frac{d^2T}{dx^2}
$$
这个方程描述了[热对流](@entry_id:144912)（左侧）与[热传导](@entry_id:143509)（右侧）之间的平衡。为了求解它，我们需要边界条件。典型的边界条件是：
*   在上游无穷远处 ($x \to -\infty$)，温度为未燃混合物温度 $T_u$。
*   在反应区的入口（我们定义为 $x=0$），温度达到一个足以引发反应的“点火”温度 $T_s$。

求解上述常微分方程并应用边界条件，我们得到[预热](@entry_id:159073)区 ($x \le 0$) 的温度分布：
$$
T(x) = T_u + (T_s - T_u) \exp\left(\frac{\rho u c_p}{\lambda} x\right)
$$
这个解清晰地展示了火焰[预热](@entry_id:159073)区的指数型温度剖面，其特征厚度由 $\delta_T = \lambda / (\rho u c_p)$ 决定。这个简单的例子说明了如何从普适的守恒方程出发，通过引入适当的简化和[封闭模型](@entry_id:1122505)，来分析和预测具体的燃烧现象。