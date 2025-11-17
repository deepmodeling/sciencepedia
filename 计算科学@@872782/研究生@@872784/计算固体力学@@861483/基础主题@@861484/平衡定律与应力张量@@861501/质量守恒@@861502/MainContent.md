## 引言
质量守恒是物理学的基本定律之一，在[计算固体力学](@entry_id:169583)领域，它更是构建可靠数值模型的基石。任何力学仿真若要声称其物理真实性，都必须在离散化的计算世界中严格遵循这一基本公理。然而，从连续介质的理论方程到计算机中的代数方程，这一转化过程充满了挑战。许多数值误差和非物理现象，如[体积锁定](@entry_id:172606)、质量漂移或不真实的界面行为，都源于对[质量守恒定律](@entry_id:147377)及其推论在计算层面处理不当。因此，深刻理解并精确实现质量守恒，是高级计算力学工程师和研究者必须掌握的核心技能。

本文旨在系统性地解决这一知识鸿沟，引领读者从基本原理深入到高级应用和计算实践。我们将分三步展开：

- 在 **第一章：原理与机制** 中，我们将从最基本的积分形式出发，严谨推导[质量守恒](@entry_id:204015)在拉格朗日和[欧拉描述](@entry_id:264722)下的局部[微分形式](@entry_id:146747)，并探讨在有限元框架下施加这一约束的关键技术，如混合公式和[ALE方法](@entry_id:746347)。
- 接着，在 **第二章：应用与[交叉](@entry_id:147634)学科联系** 中，我们将展示[质量守恒](@entry_id:204015)如何在[有限应变塑性](@entry_id:185352)、材料断裂、流固耦合等前沿问题中作为核心约束，并探索其如何作为统一的原则，连接固体力学与计算生物学、地球科学等不同学科。
- 最后，在 **第三章：动手实践** 中，您将通过具体的编程练习，亲手处理数值积分中的质量漂移、[空间离散化](@entry_id:172158)引发的[沙漏模式](@entry_id:174855)以及在[拓扑变化](@entry_id:136654)中保持[质量守恒](@entry_id:204015)等实际问题，将理论知识转化为解决问题的能力。

通过这一系列的学习，您将不仅掌握[质量守恒](@entry_id:204015)的理论，更能将其作为一把标尺，去评判、设计和实现物理上一致且数值上稳健的计算力学模型。

## 原理与机制

在连续介质力学中，质量守恒是一条基本公理，它构成了所有力学分析的基石。本章旨在深入阐述[质量守恒定律](@entry_id:147377)在[计算固体力学](@entry_id:169583)中的核心原理与关键机制。我们将从其最根本的积分形式出发，推导在不同运动学描述下的局部[微分形式](@entry_id:146747)，并探讨在计算框架下，特别是有限元方法中，如何精确、稳健地施加这一物理约束。

### 质量守恒的基本原理与描述

质量守恒定律的普适性表述是：对于任意一个由相同物质点构成的**物质体（material volume）**，其总质量不随时间改变。设想一个在时刻 $t$ 占据空间区域 $\Omega(t)$ 的物质体，其空间密度场为 $\rho(\mathbf{x}, t)$，其中 $\mathbf{x}$ 是空间坐标。该物质体的总质量 $m$ 可以通过对当前构型 $\Omega(t)$ 的体积积分得到：

$m(t) = \int_{\Omega(t)} \rho(\mathbf{x}, t) \, \mathrm{d}v$

[质量守恒](@entry_id:204015)公理断言，对于一个与物质一同运动的体积（即物质体），其质量是恒定的，即 $\frac{\mathrm{d}m}{\mathrm{d}t} = 0$。因此，我们有以下基本积分方程 [@problem_id:3550631]：

$\frac{\mathrm{d}}{\mathrm{d}t} \int_{\Omega(t)} \rho(\mathbf{x}, t) \, \mathrm{d}v = 0$

从这一积分形式出发，我们可以根据所选择的运动学描述框架——**拉格朗日（Lagrangian）描述**或**欧拉（Eulerian）描述**——推导出相应的局部（[微分](@entry_id:158718)）形式。

#### 拉格朗日（物质）描述

在[拉格朗日描述](@entry_id:264498)中，我们追踪每个物[质点](@entry_id:186768) $\mathbf{X}$ 的运动。$\mathbf{X}$ 是物[质点](@entry_id:186768)在选定的**参考构型** $\Omega_0$ 中的坐标。运动由映射 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$ 给出。体积微元在参考构型和当前构型之间通过变形梯度的[雅可比行列式](@entry_id:137120) $J$ 建立联系：$\mathrm{d}v = J(\mathbf{X}, t) \, \mathrm{d}V$，其中 $J = \det(\mathbf{F})$ 且 $\mathbf{F} = \nabla_{\mathbf{X}} \boldsymbol{\varphi}$。

将质量[积分变换](@entry_id:186209)到不随时间变化的参考构型 $\Omega_0$ 上进行：

$m = \int_{\Omega_0} \rho(\boldsymbol{\varphi}(\mathbf{X}, t), t) J(\mathbf{X}, t) \, \mathrm{d}V$

由于积分域 $\Omega_0$ 是固定的，我们可以将时间导数移入积分号内：

$\frac{\mathrm{d}m}{\mathrm{d}t} = \int_{\Omega_0} \frac{\partial}{\partial t} \left[ \rho(\boldsymbol{\varphi}(\mathbf{X}, t), t) J(\mathbf{X}, t) \right] \mathrm{d}V = 0$

由于这个等式对任意物质[子域](@entry_id:155812) $V_0 \subseteq \Omega_0$ 都成立，根据局部化原理，被积函数本身必须处处为零。这便得到了[质量守恒](@entry_id:204015)在[拉格朗日描述](@entry_id:264498)下的局部形式 [@problem_id:3550631]：

$\frac{\partial}{\partial t} \left[ \rho(\boldsymbol{\varphi}(\mathbf{X}, t), t) J(\mathbf{X}, t) \right] = 0$

此式表明，对于一个给定的物[质点](@entry_id:186768) $\mathbf{X}$，乘积 $\rho J$ 是一个不随时间变化的量。我们可以通过其在初始时刻 $t=0$ 的值来确定这个量。在 $t=0$ 时，当前构型与参考构型重合，因此 $J(\mathbf{X}, 0)=1$，而密度 $\rho(\mathbf{X}, 0)$ 就是定义上的**参考密度** $\rho_0(\mathbf{X})$。由此，我们得到一个在[计算固体力学](@entry_id:169583)中至关重要的关系式：

$\rho(\boldsymbol{\varphi}(\mathbf{X}, t), t) J(\mathbf{X}, t) = \rho_0(\mathbf{X})$

这个关系直观地说明了密度的变化与体积变化的代偿关系：当一个物质微元被压缩时（$J \lt 1$），其密度增加；当它膨胀时（$J \gt 1$），其密度减小，以保持其质量不变 [@problem_id:3550646]。

#### 欧拉（空间）描述

在[欧拉描述](@entry_id:264722)中，我们关注空间中固定的点，并观察物质流过这些点时的性质变化。为了从基本积分形式推导[欧拉描述](@entry_id:264722)下的局部形式，我们需要使用**[雷诺输运定理](@entry_id:191217)（Reynolds Transport Theorem）**。该定理建立了物质体积积分的时间导数与空间体积积分内的导数之间的联系。应用于密度场 $\rho$ 和物质体积 $\Omega(t)$，定理给出：

$\frac{\mathrm{d}}{\mathrm{d}t} \int_{\Omega(t)} \rho \, \mathrm{d}v = \int_{\Omega(t)} \left( \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) \right) \mathrm{d}v$

其中，$\mathbf{v}(\mathbf{x}, t)$ 是物质在空间点 $\mathbf{x}$ 的[速度场](@entry_id:271461)，$\frac{\partial \rho}{\partial t}$ 是在固定空间点上的时间[偏导数](@entry_id:146280)，$\nabla \cdot$ 是空间[散度算子](@entry_id:265975)。

将此结果代入[质量守恒的积分形式](@entry_id:750704)，得到：

$\int_{\Omega(t)} \left( \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) \right) \mathrm{d}v = 0$

同样，根据局部化原理，被积函数必须为零，这便产生了质量守恒的**守恒型**欧拉方程，也称为**连续性方程**：

$\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0$

利用矢量微积分的乘法法则，$\nabla \cdot (\rho \mathbf{v}) = (\nabla \rho) \cdot \mathbf{v} + \rho (\nabla \cdot \mathbf{v})$，我们可以将上式展开。同时，我们定义场的**[物质时间导数](@entry_id:190892)**（material time derivative），它表示跟随一个物质点运动时观察到的场量变化率：

$\frac{D\rho}{Dt} \equiv \dot{\rho} = \frac{\partial \rho}{\partial t} + \mathbf{v} \cdot \nabla \rho$

将这两者结合，我们得到连续性方程的另一种常用形式 [@problem_id:3550631]：

$\dot{\rho} + \rho (\nabla \cdot \mathbf{v}) = 0$

此方程将物[质点](@entry_id:186768)的密度变化率 $\dot{\rho}$ 与该点的速度场的散度 $\nabla \cdot \mathbf{v}$（即[体积应变率](@entry_id:272471)）联系起来。

### 特殊情况：[不可压缩材料](@entry_id:159741)

一个重要的特殊情况是**[不可压缩材料](@entry_id:159741)**。根据定义，[不可压缩材料](@entry_id:159741)中任何物质点的密度在运动过程中都保持不变。这意味着[物质时间导数](@entry_id:190892)为零，即 $\dot{\rho} = 0$ [@problem_id:3550674]。

将此条件代入[欧拉形式](@entry_id:637896)的[连续性方程](@entry_id:195013) $\dot{\rho} + \rho (\nabla \cdot \mathbf{v}) = 0$，由于密度 $\rho$ 恒为正，我们立即得到不可压缩流动的运动学约束：

$\nabla \cdot \mathbf{v} = 0$

这意味着在[不可压缩材料](@entry_id:159741)中，速度场必须是无散的（solenoidal）。

同样，将 $\dot{\rho}=0$ 的条件（意味着 $\rho$ 恒等于其初始值 $\rho_0$）代入[拉格朗日形式](@entry_id:145697)的质量守恒关系 $\rho J = \rho_0$，我们得到在大变形下描述[不可压缩性](@entry_id:274914)的几何约束 [@problem_id:3550674]：

$J = \det(\mathbf{F}) = 1$

这个条件表明，[不可压缩材料](@entry_id:159741)的运动必须是**保体积的（isochoric）**。需要强调的是，在有限变形理论中，[运动学](@entry_id:173318)约束是 $J=1$，而非[小变形理论](@entry_id:174991)中的 $\nabla \cdot \mathbf{u} = 0$（其中 $\mathbf{u}$ 是[位移场](@entry_id:141476)）。后者仅是前者在线性化假设下的一阶近似。

### 推广：考虑质量源

在某些[多物理场](@entry_id:164478)问题中，如[化学反应](@entry_id:146973)或[相变](@entry_id:147324)，物质的质量可能不是守恒的，而是存在源或汇。我们可以引入一个空间质量源密度场 $\gamma(\mathbf{x}, t)$（单位体积、单位时间的质量变化率）来描述这一效应。此时，质量守恒的基本积分形式修正为：

$\frac{\mathrm{d}}{\mathrm{d}t} \int_{\Omega(t)} \rho \, \mathrm{d}v = \int_{\Omega(t)} \gamma \, \mathrm{d}v$

遵循与之前相同的推导路径，我们可以得到包含[源项](@entry_id:269111)的局部守恒方程 [@problem_id:3550644]：

- **[欧拉形式](@entry_id:637896)**: $\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = \gamma$
- **[拉格朗日形式](@entry_id:145697)**: 若定义参考构型下的质量源密度 $\gamma_0 = \gamma J$，则有 $\frac{D(\rho J)}{Dt} = \gamma_0$。注意到 $\rho_0 = \rho J$ 定义了物质密度（单位参考体积的质量），此方程可写作 $\frac{D\rho_0}{Dt} = \gamma_0$。这表明物质密度的变化率等于参考构型下的质量源。

### 计算框架下的质量守恒

在[计算固体力学](@entry_id:169583)中，将连续的[守恒定律](@entry_id:269268)转化为离散的[代数方程](@entry_id:272665)是核心任务。这一过程必须谨慎处理，以确保数值解的准确性和物理真实性。

#### 弱形式与[混合有限元法](@entry_id:165231)

在有限元方法（FEM）中，[微分方程](@entry_id:264184)通常通过其**弱形式**来求解。对于[不可压缩性约束](@entry_id:750592)，无论是速率形式 $\nabla \cdot \mathbf{v} = 0$还是有限变形形式 $J - 1 = 0$，都可以通过引入一个**拉格朗日乘子（Lagrange multiplier）**场来施加。这个[拉格朗日乘子](@entry_id:142696)在物理上通常对应于[静水压力](@entry_id:275365) $p$。

以有限变形的约束 $J-1=0$ 为例，其弱形式通过乘以一个任意的标量测试函数 $q$ 并在参考域上积分得到 [@problem_id:3550674]：

$\int_{\Omega_0} q (J - 1) \, \mathrm{d}V = 0$

在**[混合有限元法](@entry_id:165231)**中，位移场和压[力场](@entry_id:147325)被视为独立的未知量。系统的[势能](@entry_id:748988)泛函被增广为混合[势能](@entry_id:748988)形式，例如，对于一个近乎不可压缩的[超弹性材料](@entry_id:190241)，其单位参考体积的势能可以写为 [@problem_id:3550641]：

$W(\mathbf{F}, p) = W_{\text{iso}}(\mathbf{F}) - p(J-1)$

其中 $W_{\text{iso}}$ 是材料的等容（保体积）[应变能](@entry_id:162699)部分。对该泛函关于位移和压力进行变分，便可导出求解系统所需的耦合[方程组](@entry_id:193238)。压[力场](@entry_id:147325) $p$ 的物理意义可以通过分析本构关系来揭示。例如，对于一个不可压缩的新胡克（neo-Hookean）材料，其柯西应力（Cauchy stress）张量 $\boldsymbol{\sigma}$ 与压力 $p$ 的关系为 $\boldsymbol{\sigma} = \mu \mathbf{B} - p \mathbf{I}$，其中 $\mu$ 是[剪切模量](@entry_id:167228)，$\mathbf{B} = \mathbf{F}\mathbf{F}^T$ 是左柯西-格林（Cauchy-Green）张量。在一个具体的边界值问题中，如[单轴拉伸](@entry_id:188287)一个侧向自由的试样，可以通过施加边界条件（如侧向应力为零）来确定压力 $p$ 的值 [@problem_id:3550641]。

类似地，速率形式的约束 $\nabla \cdot \mathbf{v}=0$ 也可以通过[弱形式](@entry_id:142897) $\int_{\Omega} q (\nabla \cdot \mathbf{v}) \, \mathrm{d}\Omega = 0$ 来施加，这在[流体力学](@entry_id:136788)和一些固体力学的[流体动力学](@entry_id:136788)公式中非常普遍 [@problem_id:3550659]。

#### 约束的线性化

混合公式得到的[非线性](@entry_id:637147)[代数方程](@entry_id:272665)组通常使用牛顿-拉夫逊（[Newton-Raphson](@entry_id:177436)）等迭代法求解。这要求对系统中的所有残差方程进行**一致性线性化（consistent linearization）**。以[拉格朗日形式](@entry_id:145697)的[质量守恒](@entry_id:204015) $\rho J = \rho_0$ 为例，我们可以定义一个残差函数 $c(\mathbf{F}, \rho) = \rho J - \rho_0 = 0$。

为了进行牛顿迭代，我们需要计算该残差对主要变量（如 $\mathbf{F}$ 和 $\rho$）的增量 $\delta\mathbf{F}$ 和 $\delta\rho$ 的 Gâteaux 导数 $\delta c$ [@problem_id:3550646]。应用[乘法法则](@entry_id:144424)：

$\delta c = (\delta \rho) J + \rho (\delta J)$

其中 $\delta J$ 是[雅可比行列式](@entry_id:137120)对变形梯度增量 $\delta\mathbf{F}$ 的线性化。通过[矩阵微积分](@entry_id:181100)的基本性质可以推导出：

$\delta J = \frac{d}{d\epsilon} \det(\mathbf{F} + \epsilon \delta \mathbf{F}) \bigg|_{\epsilon=0} = J \operatorname{tr}(\mathbf{F}^{-1} \delta\mathbf{F})$

将此代入，得到残差的完整线性化表达式：

$\delta c = J \delta \rho + \rho J \operatorname{tr}(\mathbf{F}^{-1} \delta \mathbf{F})$

这个线性化表达式是构建[切线刚度矩阵](@entry_id:170852)的关键部分，对于保证[牛顿法](@entry_id:140116)的二次收敛性至关重要。

#### 任意拉格朗日-欧拉（ALE）方法

在许多计算问题中，尤其是在涉及大变形或流固耦合的情况下，纯粹的拉格朗日网格可能会因过度扭曲而失效，而纯粹的欧拉网格则难以精确追踪移动的边界。**任意拉格朗日-欧拉（Arbitrary Lagrangian-Eulerian, ALE）**方法通过引入一个独立的[计算网格](@entry_id:168560)运动来解决这一问题。网格可以根据需要任意移动，既不完全跟随物质（拉格朗日），也不完全固定于空间（欧拉）。

在ALE框架中，我们需要区分物质速度 $\mathbf{v}$ 和网格速度 $\mathbf{w}$。物质相对于网格的[对流](@entry_id:141806)速度为 $\mathbf{c} = \mathbf{v} - \mathbf{w}$。质量守恒定律需要在一个随[网格运动](@entry_id:163293)的控制体上重新表述。通过严谨的推导，可以得到ALE框架下的[质量守恒](@entry_id:204015)方程 [@problem_id:3550676] [@problem_id:3550672]：

$\frac{\partial \rho}{\partial t}\bigg|_{\mathrm{ALE}} + \nabla \cdot \big(\rho(\mathbf{v} - \mathbf{w})\big) + \rho \nabla \cdot \mathbf{w} = 0$

其中 $\frac{\partial \rho}{\partial t}\big|_{\mathrm{ALE}}$ 是在固定网格点上观察到的时间导数。这个方程优雅地统一了拉格朗日（$\mathbf{w}=\mathbf{v}$）和欧拉（$\mathbf{w}=0$）描述。在实际操作中，[ALE方法](@entry_id:746347)通常分解为两个步骤：一个纯拉格朗日步骤，网格随物质运动；然后是一个**重映（remapping）**或**重分区（rezoning）**步骤，将拉格朗日步骤计算出的物理量守恒地投影到一个新的、质量更好的网格上 [@problem_id:3550672]。这个重映过程必须是守恒的，以确保在网格调整过程中总质量等物理量不会凭空产生或消失。

#### 保守型离散格式与[几何积分子](@entry_id:138085)

无论采用何种描述，数值方法的关键目标之一是确保离散方程能精确地反映连续方程的守恒性质。这样的[数值格式](@entry_id:752822)被称为**保守型格式（conservative scheme）**。

在拉格朗日[有限体积法](@entry_id:749372)中，每个网格单元就是一个物质体。根据 $\rho J = \rho_0$，我们可以直接推导出二维情况下，单元平均密度的离散更新法则 [@problem_id:3550677]：

$\rho_c^{n+1} A_c^{n+1} = \rho_c^n A_c^n \quad \implies \quad \rho_c^{n+1} = \rho_c^n \frac{A_c^n}{A_c^{n+1}}$

其中 $\rho_c$ 和 $A_c$ 分别是单元 $c$ 的平均密度和面积。这种格式通过直接将密度更新与几何面积的变化联系起来，在离散层面上精确地保证了每个单元的[质量守恒](@entry_id:204015)。这种性质也被称为满足**[几何守恒律](@entry_id:170384)（Geometric Conservation Law, GCL）**。

更进一步，我们还可以考察[时间积分格式](@entry_id:165373)本身是否保持物理[不变量](@entry_id:148850)。考虑由 $\dot{\rho} + \rho\theta = 0$ 和 $\dot{J} - J\theta = 0$（其中 $\theta = \nabla \cdot \mathbf{v}$）组成的[微分方程组](@entry_id:148215)。它们共同导出的[不变量](@entry_id:148850)是 $\frac{d}{dt}(\rho J) = 0$。然而，若使用标准的[时间积分格式](@entry_id:165373)，如前向或[后向欧拉法](@entry_id:139674)，来离散这两个方程，我们会发现离散后的更新值 $\rho_{n+1}$ 和 $J_{n+1}$ 通常不满足 $\rho_{n+1}J_{n+1} = \rho_n J_n$。

为了在时间离散上也能精确保持这种乘法结构的[不变量](@entry_id:148850)，需要采用所谓的**[几何积分子](@entry_id:138085)（geometric integrators）**。例如，通过[对数变换](@entry_id:267035)将原方程化为 $\frac{d(\ln \rho)}{dt} = -\theta$ 和 $\frac{d(\ln J)}{dt} = \theta$，然后应用[积分因子法](@entry_id:167338)，可以得到指数映射形式的更新 [@problem_id:3550635]：

$\rho_{n+1} = \rho_n \exp(-\Delta t \bar{\theta})$
$J_{n+1} = J_n \exp(+\Delta t \bar{\theta})$

其中 $\bar{\theta}$ 是时间步长内[速度散度](@entry_id:264117)的某个平均值。这种格式通过其指数形式，在代数上保证了 $\rho_{n+1}J_{n+1} = \rho_n J_n$ 对任意时间步长 $\Delta t$ 都精确成立，从而在时间维度上完美地继承了[连续系统](@entry_id:178397)的几何结构。这对于需要长期模拟或对守恒性有极高要求的计算任务至关重要。