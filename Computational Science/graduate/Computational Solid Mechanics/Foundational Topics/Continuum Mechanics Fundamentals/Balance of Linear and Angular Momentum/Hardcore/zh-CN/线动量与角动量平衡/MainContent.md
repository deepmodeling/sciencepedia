## 引言
[动量平衡原理](@entry_id:196256)是物理学中最基本、最普适的[守恒定律](@entry_id:269268)之一，它由[牛顿运动定律](@entry_id:163846)推广而来，构成了描述连续介质体（无论是固体、液体还是气体）力学行为的数学模型的基石。从设计宏伟的桥梁到模拟微观的[分子碰撞](@entry_id:137334)，对这些原理的深刻理解是解决几乎所有力学与工程问题的先决条件。然而，从抽象的物理公设到能够求解实际问题的具体方程，再到跨越不同学科的应用，这一过程涉及复杂的数学推导和概念演化。本文旨在填补这一知识鸿沟，系统性地梳理[线动量](@entry_id:174467)与[角动量平衡](@entry_id:181848)的完整图景。

在接下来的内容中，读者将踏上一段从理论到实践的旅程。第一章“原理与机制”将奠定理论基础，详细阐述[动量平衡](@entry_id:193575)的积分与[微分形式](@entry_id:146747)，引入关键的[应力张量](@entry_id:148973)概念，并探讨其在不同[坐标系](@entry_id:156346)和弱形式下的表达，最终延伸至超越经典理论的广义连续介质模型。第二章“应用与跨学科联系”将展示这些原理的强大威力，通过一系列涵盖土木工程、计算科学乃至[物理化学](@entry_id:145220)的实例，揭示[动量守恒](@entry_id:149964)如何在不同尺度和领域中发挥核心作用。最后，在“动手实践”部分，我们将通过具体的编程练习，将理论知识转化为解决实际计算力学问题的能力。通过这一结构化的学习路径，本文旨在为您提供一个关于[动量平衡原理](@entry_id:196256)的全面、深入且实用的视角。

## 原理与机制

在对连续介质体的力学行为进行[数学建模](@entry_id:262517)时，其运动必须遵循由[牛顿运动定律](@entry_id:163846)推广而来的基本物理原理。这些原理构成了[动量守恒](@entry_id:149964)定律，是所有[连续介质力学](@entry_id:155125)分析的基石。本章旨在系统地阐述[线动量](@entry_id:174467)与[角动量平衡](@entry_id:181848)的基本原理，并探讨这些原理如何从其公理化的积分形式，通过局部化过程，转化为描述点态行为的[微分方程](@entry_id:264184)。我们还将研究这些定律在不同参考[坐标系](@entry_id:156346)下的表达形式，并最终揭示它们在有限元等离散化数值方法中得以保持的机制。

### 积分形式的平衡律：基本公设

我们首先考虑一个在[欧几里得空间](@entry_id:138052)中运动和变形的连续介质体。我们关注其中任意一个由相同物质点构成的子区域，称为**物质体积** (material volume)，在时刻 $t$ 占据的空间区域记为 $\Omega(t)$。该区域的边界为 $\partial\Omega(t)$。

#### 线[动量平衡](@entry_id:193575)

线[动量平衡原理](@entry_id:196256)是牛顿第二定律在连续介质中的直接体现。它断言，物质体积 $\Omega(t)$ 中[总线动量](@entry_id:173071)的变化率等于作用在该体积上的所有外力之和。

首先，我们需要精确定义相关的物理量 。在空间点 $\mathbf{x}$ 和时刻 $t$，设连续介质的质量密度为 $\rho(\mathbf{x}, t)$，[速度场](@entry_id:271461)为 $\mathbf{v}(\mathbf{x}, t)$。一个无穷小体积元 $dV$ 的质量为 $dm = \rho dV$，其[线动量](@entry_id:174467)为 $dm\,\mathbf{v} = \rho\mathbf{v}\,dV$。因此，**线动量密度** (linear momentum density) 场被定义为向量场 $\mathbf{p}(\mathbf{x}, t) = \rho(\mathbf{x}, t)\mathbf{v}(\mathbf{x}, t)$。物质体积 $\Omega(t)$ 的**[总线动量](@entry_id:173071)** (total linear momentum) $\mathbf{P}(t)$ 是该密度场在整个体积上的积分：
$$
\mathbf{P}(t) = \int_{\Omega(t)} \rho(\mathbf{x}, t)\mathbf{v}(\mathbf{x}, t) \,dV
$$

作用于物质体积 $\Omega(t)$ 的外力分为两类：**体力** (body forces) 和**面力** (surface forces)。[体力](@entry_id:174230)作用于体积内的每个物[质点](@entry_id:186768)，例如重力。若 $\mathbf{b}(\mathbf{x}, t)$ 表示单位质量的体力，则总[体力](@entry_id:174230)为 $\int_{\Omega(t)} \rho\mathbf{b} \,dV$。面力是外界通过接触边界 $\partial\Omega(t)$ 施加于该物质体积的作用力，通过**牵[引力](@entry_id:175476)向量** (traction vector) $\mathbf{t}(\mathbf{x}, t, \mathbf{n})$ 来描述，它表示在法向为 $\mathbf{n}$ 的单位面积上所受的力。总面力是牵[引力](@entry_id:175476)在整个边界上的积分 $\int_{\partial\Omega(t)} \mathbf{t} \,dS$。

根据线[动量平衡原理](@entry_id:196256)，我们得到线[动量平衡](@entry_id:193575)的积分表达式，也称为**柯西第一运动定律** (Cauchy's first law of motion)：
$$
\frac{d}{dt}\int_{\Omega(t)}\rho\mathbf{v}\,dV = \int_{\Omega(t)}\rho\mathbf{b}\,dV + \int_{\partial\Omega(t)}\mathbf{t}\,dS
$$
此方程指出，一个物质体积的[总线动量](@entry_id:173071)对时间的导数（左侧），等于作用于其上的总[体力](@entry_id:174230)与总面力之和（右侧）。

#### [角动量平衡](@entry_id:181848)

同样地，角[动量平衡原理](@entry_id:196256)指出，物质体积 $\Omega(t)$ 相对于某个[固定点](@entry_id:156394)（通常取坐标原点 $\mathbf{o}$）的[总角动量](@entry_id:155748)的变化率，等于所有外力对同一点的力矩之和。

无穷小质量元 $dm$ 的角动量为 $\mathbf{x} \times (dm\,\mathbf{v})$，其中 $\mathbf{x}$ 是从原点指向该质量元的位置向量。因此，**角动量密度** (angular momentum density) 场为 $\mathbf{h}_{\mathbf{o}}(\mathbf{x}, t) = \mathbf{x} \times (\rho\mathbf{v})$。物质体积 $\Omega(t)$ 相对于原点的**[总角动量](@entry_id:155748)** (total angular momentum) $\mathbf{L}(t)$ 为：
$$
\mathbf{L}(t) = \int_{\Omega(t)} \mathbf{x} \times \big(\rho(\mathbf{x}, t)\mathbf{v}(\mathbf{x}, t)\big) \,dV
$$

外力的力矩同样源于体力和面力。单位质量体力 $\mathbf{b}$ 产生的力矩密度为 $\mathbf{x} \times (\rho\mathbf{b})$，牵[引力](@entry_id:175476) $\mathbf{t}$ 产生的力矩密度为 $\mathbf{x} \times \mathbf{t}$。在经典连续介质理论中，我们假设不存在[分布](@entry_id:182848)式的**[体力](@entry_id:174230)矩** (body couples) 或**面力偶** (surface couples)。

因此，[角动量平衡](@entry_id:181848)的积分表达式，也称为**柯西第二运动定律** (Cauchy's second law of motion)，可写作  ：
$$
\frac{d}{dt}\int_{\Omega(t)} \mathbf{x} \times (\rho\mathbf{v}) \,dV = \int_{\Omega(t)} \mathbf{x} \times (\rho\mathbf{b}) \,dV + \int_{\partial\Omega(t)} \mathbf{x} \times \mathbf{t} \,dS
$$
此方程的左侧是总角动量的物质导数，右侧是体力与面力产生的总力矩。

### 局部化与[应力张量](@entry_id:148973)

积分形式的平衡定律描述了宏观物质体积的整体行为。为了得到描述介质内每一点行为的**局部** (local) 或[微分形式](@entry_id:146747)的[平衡方程](@entry_id:172166)，我们需要进行“局部化”过程。这一过程的核心是引入一个关键概念：应力张量。

#### 柯西应力定理

牵[引力](@entry_id:175476)向量 $\mathbf{t}$ 不仅依赖于位置 $\mathbf{x}$ 和时间 $t$，还依赖于其作用平面的法向 $\mathbf{n}$。一个深刻的结论，即**柯西应力定理** (Cauchy's stress theorem)，指出 $\mathbf{t}$ 与 $\mathbf{n}$ 之间存在[线性关系](@entry_id:267880)。这可以通过对一个无穷小的四面体应用线[动量平衡](@entry_id:193575)定律来证明 。该定理断言，在每一点 $\mathbf{x}$ 和每一时刻 $t$，存在一个二阶张量场 $\boldsymbol{\sigma}(\mathbf{x}, t)$，称为**柯西应力张量** (Cauchy stress tensor)，使得对于任意[单位法向量](@entry_id:178851) $\mathbf{n}$，牵[引力](@entry_id:175476)向量由下式给出：
$$
\mathbf{t}(\mathbf{x}, t, \mathbf{n}) = \boldsymbol{\sigma}(\mathbf{x}, t)\mathbf{n}
$$
$\boldsymbol{\sigma}$ 的物理意义是内部相互作用力的量度。其分量 $\sigma_{ij}$ 表示在 $i$ 方向上的单位面积上作用的力的第 $j$ 个分量。因此，应力的单位是力每单位面积，即帕斯卡 (Pa或$\mathrm{N/m^2}$) 。柯西应力张量是一个客观张量，在[刚体转动](@entry_id:191086) $\mathbf{Q}$ 下，其变换规律为 $\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$ 。

#### [动量平衡](@entry_id:193575)的局部形式

一旦建立了 $\mathbf{t}$ 与 $\boldsymbol{\sigma}$ 的关系，我们就可以将积分平衡定律转化为[微分方程](@entry_id:264184)。将 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ 代入线[动量平衡](@entry_id:193575)的[积分方程](@entry_id:138643)，并对面力积分项应用**[高斯散度定理](@entry_id:188065)** (Gauss's divergence theorem)，同时对左侧的物质导数应用**[雷诺输运定理](@entry_id:191217)** (Reynolds transport theorem)，我们可以得到：
$$
\int_{\Omega(t)} \rho\dot{\mathbf{v}} \,dV = \int_{\Omega(t)} (\nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b}) \,dV
$$
其中 $\dot{\mathbf{v}}$ 是[速度场](@entry_id:271461)的物质导数，即加速度 $\mathbf{a}$。由于此式对任意物质体积 $\Omega(t)$ 都成立，只要被积函数是连续的，那么被积函数本身必须处处相等。这就得到了线[动量平衡](@entry_id:193575)的局部形式：
$$
\rho\dot{\mathbf{v}} = \nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b}
$$
这个方程是[连续介质力学](@entry_id:155125)中最核心的方程之一。

#### [角动量平衡](@entry_id:181848)与[应力对称性](@entry_id:181689)

对[角动量平衡](@entry_id:181848)定律进行类似的局部化操作，会导出一个关于柯西[应力张量对称性](@entry_id:201218)的惊人而深刻的结论。将 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ 代入角动量[积分方程](@entry_id:138643)，并应用一系列张量恒等式和[散度定理](@entry_id:143110)，最终可以证明，为了使角动量在任意无穷小体积上都得到平衡（在没有[体力](@entry_id:174230)矩和面力偶的情况下），柯西[应力张量](@entry_id:148973)必须是**对称**的   。
$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^T
$$
用分量表示即 $\sigma_{ij} = \sigma_{ji}$。这一结论极大地简化了[应力分析](@entry_id:168804)，因为它将一个二阶张量中独立的未知分量从9个减少到了6个。这个对称性是角动量守恒在经典连续介质模型中的直接体现。

### 面向计算力学的替代表述

求解上述[局部平衡](@entry_id:156295)方程通常需要数值方法，而这些方法往往基于不同的数学表述。

#### 物质描述与空间描述

到目前为止，我们的讨论都是在**当前构型** (current configuration) 或**空间描述** (spatial description, Eulerian description) 中进行的，物理量是空间位置 $\mathbf{x}$ 和时间 $t$ 的函数。然而，在固体力学中，跟踪物质点的运动更为自然，这引出了**参考构型** (reference configuration) 或**物质描述** (material description, Lagrangian description)。

在这种描述下，物理量被视为初始位置 $\mathbf{X}$ 和时间 $t$ 的函数。为了转换平衡定律，我们需要引入新的[应力量度](@entry_id:198799)。**第一类皮奥拉-基尔霍夫(Piola-Kirchhoff)[应力张量](@entry_id:148973)** (First Piola-Kirchhoff stress tensor) $\mathbf{P}$ 就是为此而生，它关联了参考构型中的力与面积。它与柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的关系通过变形梯度 $\mathbf{F} = \nabla_0 \mathbf{x}$ 和其[雅可比行列式](@entry_id:137120) $J = \det(\mathbf{F})$ 给出 ：
$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}
$$
通过将空间描述下的平衡方程[拉回](@entry_id:160816) (pullback) 到参考构型，我们得到物质描述下的局部线[动量平衡](@entry_id:193575)方程 ：
$$
\rho_0 \ddot{\mathbf{x}} = \nabla_0 \cdot \mathbf{P} + \rho_0 \mathbf{b}_0
$$
这里，$\rho_0(\mathbf{X})$ 是参考构型下的质量密度（它与当前密度 $\rho$ 的关系是 $\rho_0 = J\rho$），$\ddot{\mathbf{x}}$ 是物质点加速度，$\nabla_0 \cdot$ 是对参考坐标的散度，$\mathbf{b}_0$ 是在参考构型中定义的单位质量[体力](@entry_id:174230)。一个重要的区别是，即使柯西应力张量 $\boldsymbol{\sigma}$ 是对称的，第一类[Piola-Kirchhoff应力](@entry_id:173629)张量 $\mathbf{P}$ 通常是**非对称**的 。

#### 任意拉格朗日-欧拉 (ALE) 描述

在某些问题中（如流固耦合），固定网格（欧拉）或随物质运动的网格（拉格朗日）都非最优选择。**任意拉格朗日-欧拉** (Arbitrary Lagrangian-Eulerian, ALE) 方法提供了一种折中方案，其控制体积的边界以任意指定的速度 $\mathbf{w}(\mathbf{x}, t)$ 运动。在这种情况下，[动量平衡](@entry_id:193575)方程必须考虑物质穿越控制体积边界所带来的动量流。通过[雷诺输运定理](@entry_id:191217)的一般形式，可以推导出适用于ALE框架的线[动量平衡](@entry_id:193575)积分形式 ：
$$
\frac{d}{dt}\int_{\Omega(t)}\rho\mathbf{v}\,dV = \int_{\Omega(t)}\rho\mathbf{b}\,dV + \int_{\partial\Omega(t)}\boldsymbol{\sigma}\mathbf{n}\,dA - \int_{\partial\Omega(t)}\rho\mathbf{v}\,[(\mathbf{v}-\mathbf{w})\cdot\mathbf{n}]\,dA
$$
最后一项即为通过控制边界的相对法向速度 $(\mathbf{v}-\mathbf{w})\cdot\mathbf{n}$ 带出的动量通量。

#### [虚功原理](@entry_id:138749)

有限元方法 (FEM) 等数值技术通常不直接求解强形式 (strong form) 的[微分](@entry_id:158718)平衡方程，而是求解其等价的**[弱形式](@entry_id:142897)** (weak form) 或[变分形式](@entry_id:166033)。对于静态[平衡问题](@entry_id:636409) ($\nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b} = \mathbf{0}$)，其弱形式就是**虚功原理** (principle of virtual work)。

我们通过将平衡方程乘以一个任意的、满足[运动学](@entry_id:173318)约束的**[虚位移](@entry_id:168781)** (virtual displacement) 场 $\delta\mathbf{u}$，然后在全域上积分得到。通过分部积分（即应用散度定理），我们将应力张量上的[微分算子](@entry_id:140145)转移到[虚位移](@entry_id:168781)场上。这个过程将一个二阶微分方程降阶为一阶，从而降低了对解的[光滑性](@entry_id:634843)要求 。

最终得到的[虚功](@entry_id:176403)方程为：
$$
\underbrace{\int_\Omega \boldsymbol{\sigma} : \nabla(\delta\mathbf{u}) \,d\Omega}_{\delta W_{\text{int}}} = \underbrace{\int_\Omega \rho\mathbf{b} \cdot \delta\mathbf{u} \,d\Omega + \int_{\Gamma_t} \bar{\mathbf{t}} \cdot \delta\mathbf{u} \,dS}_{\delta W_{\text{ext}}}
$$
这个方程声明，对于任何[虚位移](@entry_id:168781)，**内力[虚功](@entry_id:176403)** (internal virtual work) $\delta W_{\text{int}}$ 等于**外力[虚功](@entry_id:176403)** (external virtual work) $\delta W_{\text{ext}}$。利用应力[张量的对称性](@entry_id:202126)，[内力](@entry_id:167605)[虚功](@entry_id:176403)项可以被写成[应力张量](@entry_id:148973)与**虚应变张量** $\boldsymbol{\varepsilon}(\delta\mathbf{u}) = \frac{1}{2}(\nabla\delta\mathbf{u} + (\nabla\delta\mathbf{u})^T)$ 的[点积](@entry_id:149019) ：
$$
\delta W_{\text{int}} = \int_\Omega \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta\mathbf{u}) \,d\Omega
$$
在[弱形式](@entry_id:142897)的推导过程中，边界条件被清晰地分为两类 ：
1.  **[本质边界条件](@entry_id:173524)** (Essential boundary conditions, or Dirichlet conditions)：如在边界 $\Gamma_u$ 上指定位移 $\mathbf{u} = \bar{\mathbf{u}}$。这类条件必须在求[解空间](@entry_id:200470)的函数选取时就强制满足，并且要求相应的[虚位移](@entry_id:168781)在 $\Gamma_u$ 上为零，即 $\delta\mathbf{u} = \mathbf{0}$ on $\Gamma_u$。
2.  **自然边界条件** (Natural boundary conditions, or Neumann conditions)：如在边界 $\Gamma_t$ 上指定牵[引力](@entry_id:175476) $\mathbf{t} = \bar{\mathbf{t}}$。这类条件是作为[虚功](@entry_id:176403)方程中边界积分项自然出现的，不需要在求[解空间](@entry_id:200470)上强加。

### 超越经典连续介质：[非对称应力](@entry_id:191550)

柯西应力[张量的对称性](@entry_id:202126)是经典连续介质理论的一个标志性结果。然而，当材料的微观结构变得重要时，例如在[颗粒材料](@entry_id:750005)、泡沫或[复合材料](@entry_id:139856)中，物质点不仅可以平移，还可以独立于宏观变形而发生转动。

#### 极性介质理论简介

为了描述这类现象，**极性介质** (polar media) 理论，如**Cosserat连续介质**或**微极性介质** (micropolar continuum) 理论被提出 。这些理论引入了额外的自由度，即**微观转动** (microrotation) 场 $\boldsymbol{\varphi}$，它独立于宏观位移场。与之相应，理论中也引入了新的力和力矩量度：**偶应力张量** (couple stress tensor) $\boldsymbol{\mu}$，**[体力](@entry_id:174230)偶密度** (body couple density) $\mathbf{c}$，以及描述转动惯性的**微惯性张量** (micro-inertia tensor) $\mathbf{J}$。

#### 修正的[角动量平衡](@entry_id:181848)

在微极性理论中，[总角动量](@entry_id:155748)不仅包含由宏观速度 $\mathbf{v}$ 产生的[轨道角动量](@entry_id:191303)，还包含由微观转动 $\boldsymbol{\varphi}$ 产生的**自旋角动量** (spin angular momentum)。[角动量平衡](@entry_id:181848)定律现在必须同时考虑这两种角动量以及偶应力和体力偶产生的力矩。

对修正后的[角动量平衡](@entry_id:181848)定律进行局部化，会得到两个方程：一个仍是关于[轨道角动量](@entry_id:191303)的，另一个则是全新的、关于[自旋角动量](@entry_id:149719)的平衡方程 。这个新的方程揭示了柯西应力[张量的反对称部分](@entry_id:193562) $\operatorname{skw}\boldsymbol{\sigma} = \frac{1}{2}(\boldsymbol{\sigma}-\boldsymbol{\sigma}^T)$ 与其他微极性量的关系。其一般形式为 ：
$$
\rho\mathbf{J}\ddot{\boldsymbol{\varphi}} = \nabla\cdot\boldsymbol{\mu} + \mathbf{c} + \boldsymbol{\epsilon}:\boldsymbol{\sigma}
$$
其中 $\boldsymbol{\epsilon}:\boldsymbol{\sigma}$ 是一个与 $\operatorname{skw}\boldsymbol{\sigma}$ 直接相关的项（通过轴矢算子 $\operatorname{axl}(\cdot)$，$\boldsymbol{\epsilon}:\boldsymbol{\sigma} = 2\operatorname{axl}(\operatorname{skw}\boldsymbol{\sigma})$）。这个方程的关键启示是，在微极性介质中，柯西应力张量**不再必须是对称的**。它的反对称部分现在有了明确的物理意义：它平衡了由于偶应力、体力偶和微观转动惯性而产生的[净力矩](@entry_id:166772)。只有当所有微极性效应都消失时（即 $\boldsymbol{\mu}=\mathbf{0}, \mathbf{c}=\mathbf{0}, \mathbf{J}=\mathbf{0}$），我们才恢复到经典情况，即 $\operatorname{skw}\boldsymbol{\sigma}=\mathbf{0}$ 。

### 离散系统中的守恒原理

将连续介质问题转化为可在计算机上求解的[代数方程](@entry_id:272665)组，需要进[行空间](@entry_id:148831)和时间的离散化。一个核心问题是，连续系统所固有的[守恒定律](@entry_id:269268)在离散化之后是否还能得到精确保持。

#### [空间离散化](@entry_id:172158)与[动量守恒](@entry_id:149964)

在有限元方法中，连续的位移场被一组**形函数** (shape functions) $N_a(\mathbf{x})$ 和节点位移 $\mathbf{d}_a(t)$ 插值近似。对于一个不受外力的自由运动系统，其[半离散化](@entry_id:163562)的运动方程为 $\mathbf{M}\ddot{\mathbf{d}} = \mathbf{f}_{\text{int}}(\mathbf{d})$，其中 $\mathbf{M}$ 是[质量矩阵](@entry_id:177093)，$\mathbf{f}_{\text{int}}$ 是节点[内力向量](@entry_id:750751)。

系统的总线动量离散近似为 $\mathbf{P}^h = \int_\Omega \rho \mathbf{v}^h d\Omega$。其守恒性要求 $\dot{\mathbf{P}}^h=\mathbf{0}$。可以证明，如果形函数具有**单位分解** (partition of unity) 性质（即 $\sum_a N_a(\mathbf{x}) = 1$），那么节点[内力向量](@entry_id:750751)的总和恒为零，$\sum_a \mathbf{f}_{\text{int},a} = \mathbf{0}$。

在这种情况下，[线动量](@entry_id:174467)是否守恒完全取决于[质量矩阵](@entry_id:177093)的构造。一个关键的结果是，只要形函数满足[单位分解](@entry_id:150115)性质，无论是**协调质量矩阵** (consistent mass matrix) $M^C_{ab} = \int_\Omega \rho N_a N_b d\Omega$，还是通过行和技巧构造的**[集中质量矩阵](@entry_id:173011)** (lumped mass matrix)，都能精确地保持离散系统的[总线动量](@entry_id:173071)守恒 。这两种[质量矩阵](@entry_id:177093)都确保了[惯性力](@entry_id:169104)的总和也为零，从而使总动量的时间导数为零。

#### [时间离散化](@entry_id:169380)与[不变量](@entry_id:148850)的保持

[时间离散化](@entry_id:169380)将[微分方程组](@entry_id:148215)变为[代数方程](@entry_id:272665)。不同的[时间积分算法](@entry_id:756002)在保持[守恒量](@entry_id:150267)方面的能力差异巨大。

对于一个孤立的、满足[线动量](@entry_id:174467)和[角动量守恒](@entry_id:156798)的[哈密顿系统](@entry_id:143533)，**辛[积分算法](@entry_id:192581)** (symplectic integrators) 表现出色。这类算法的特点是能精确保持相空间的辛结构。**变分[积分算法](@entry_id:192581)** (variational integrators) 是一类特殊的辛[积分算法](@entry_id:192581)，它们通过离散化[作用量泛函](@entry_id:169216)（如[哈密顿原理](@entry_id:175601)）来构造。根据**离散[诺特定理](@entry_id:145690)** (discrete Noether's theorem)，如果离散的作用量（离散[拉格朗日函数](@entry_id:174593)）在某种变换（如刚体平移或转动）下保持不变，那么[积分算法](@entry_id:192581)将精确地保持与该对称性对应的离散动量（如总线动量或[总角动量](@entry_id:155748)）。例如，Störmer-Verlet 算法就是一个简单的变分[积分算法](@entry_id:192581)，它能同时精确保持[线动量](@entry_id:174467)和角动量。

相比之下，非辛[积分算法](@entry_id:192581)通常无法精确保持所有[不变量](@entry_id:148850)。例如，经典的四阶[龙格-库塔方法](@entry_id:144251)，虽然精度很高，但通常不能精确保持角动量，并且会引起能量的[长期漂移](@entry_id:172399)。一些隐式算法，如后向欧拉法，虽然稳定，但其固有的[数值耗散](@entry_id:168584)会使系统的总能量、甚至角动量随时间衰减 。因此，在需要长期[精确模拟](@entry_id:749142)动力学行为并保持守恒律的场合，选择变分或辛[积分算法](@entry_id:192581)至关重要。