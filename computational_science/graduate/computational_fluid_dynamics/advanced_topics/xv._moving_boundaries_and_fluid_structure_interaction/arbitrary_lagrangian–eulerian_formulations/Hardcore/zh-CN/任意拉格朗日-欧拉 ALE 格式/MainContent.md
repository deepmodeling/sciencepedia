## 引言
在计算科学与工程领域，对包含移动或变形边界的物理系统进行精确模拟，始终是一项艰巨的挑战。无论是飞行器机翼的振颤、心脏瓣膜的开合，还是激光制造中的熔池演化，传统的计算框架都面临着两难的境地：固定的欧拉网格难以精确贴合复杂的边界运动，而随物质运动的拉格朗日网格则在大变形下极易发生扭曲失效。如何建立一个既能精确追踪边界，又能保持高质量网格的通用描述方法，成为了计算流体动力学及相关领域亟待解决的关键问题。

为应对这一挑战，任意拉格朗日-欧拉（Arbitrary Lagrangian–Eulerian, ALE）方法应运而生。它巧妙地结合了欧拉方法与拉格朗日方法的优点，通过引入一个独立于物质运动的、可任意移动的计算网格，提供了一个无与伦比的灵活框架。ALE方法不仅是解决流固耦合问题的经典工具，更是一种深刻的运动学思想，其应用已渗透到众多前沿交叉学科领域。

本文旨在为读者提供一个关于ALE方法的全面而深入的理解。在第一章“原理与机制”中，我们将深入探讨其运动学基础、控制方程的推导，并重点剖析确保数值稳定性和一致性的基石——几何守恒律（GCL）。随后，在第二章“应用与跨学科联系”中，我们将展示ALE如何在流固耦合、多物理场仿真、自适应网格划分乃至天体物理学等广阔舞台上发挥其强大威力。最后，通过第三章“动手实践”中的具体问题，您将有机会将理论知识付诸实践，加深对核心概念的理解。通过本次学习，您将掌握驾驭复杂动态系统的强大计算工具。

## 原理与机制

在任意拉格朗日-欧拉 (Arbitrary Lagrangian–Eulerian, ALE) 描述中，我们不再局限于固定的欧拉网格或随物质运动的拉格朗日网格，而是引入了一个独立的计算网格。该网格可以任意运动，为模拟流固耦合、自由表面流以及其他涉及边界运动的复杂问题提供了一个强大而灵活的框架。本章将深入探讨ALE方法的运动学基础、控制方程的推导、几何守恒律的关键作用，以及网格运动的实现机制。

### ALE描述的运动学基础

ALE方法的核心在于引入了一个独立的参考构型，它通过一个时变的映射与物理域联系起来。这个框架为我们分离流体运动和网格运动提供了数学基础。

#### ALE映射

我们考虑一个固定的、通常是计算上方便的 **参考构型** 或 **计算域** $\widehat{\Omega}$，其坐标用 $\boldsymbol{X}$ 表示。物理现象发生在随时间变化的 **物理构型** 或 **物理域** $\Omega(t)$ 中，其坐标用 $\boldsymbol{x}$ 表示。ALE方法通过一个单参数的映射族 $\boldsymbol{\chi}$ 来关联这两个域：
$$
\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)
$$
这个 **ALE映射** $\boldsymbol{\chi}$ 定义了在时刻 $t$ 参考点 $\boldsymbol{X}$ 的物理位置 $\boldsymbol{x}$。它描述了计算网格随时间的运动。

为了使这种描述在数学上和物理上都有意义，映射 $\boldsymbol{\chi}$ 必须是良态的。具体来说，对于每个时刻 $t$，映射 $\boldsymbol{\chi}(\cdot, t)$ 必须是一个 **微分同胚**（diffeomorphism）。这意味着：
1.  **双射性**：映射必须是双射的（一对一且映上），这样每个物理点都唯一对应一个参考点，反之亦然。这确保了网格不会发生自相交。
2.  **光滑性**：映射 $\boldsymbol{\chi}$ 及其逆映射 $\boldsymbol{\chi}^{-1}$ 都必须是连续可微的。这保证了我们可以进行必要的微分运算。
3.  **非奇异性**：映射的雅可比行列式（Jacobian determinant）必须处处非零。在计算实践中，通常要求其严格为正，以保持网格单元的朝向，避免网格翻转或退化。

这些条件共同确保了从参考域到物理域的坐标变换是平滑且可逆的 [@problem_id:3292256]。

#### 形变梯度与雅可比行列式

为了量化局部变形，我们引入 **形变梯度张量** $\boldsymbol{F}$，定义为物理坐标 $\boldsymbol{x}$ 对参考坐标 $\boldsymbol{X}$ 的梯度：
$$
\boldsymbol{F}(\boldsymbol{X}, t) = \nabla_{\boldsymbol{X}}\boldsymbol{\chi} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}}
$$
$\boldsymbol{F}$ 是一个二阶张量，它将参考域中的一个无穷小向量映射到物理域中的对应向量。

形变梯度张量的行列式被称为 **雅可比行列式**（或简称 **雅可比**），记为 $J$：
$$
J(\boldsymbol{X}, t) = \det(\boldsymbol{F})
$$
雅可比行列式 $J$ 具有明确的物理意义：它是一个无穷小体积元从参考构型映射到物理构型时的局部体积变化率。即，$dV_x = J dV_X$。因此，$J>1$ 表示局部体积膨胀，$J1$ 表示局部体积压缩，而 $J=1$ 表示保体积（等容）变形。物理上合理的变形要求 $J>0$ 始终成立。

例如，考虑一个从参考坐标 $\boldsymbol{X}=(X_1, X_2, X_3)$ 到物理坐标 $\boldsymbol{x}=(x_1, x_2, x_3)$ 的二维映射 [@problem_id:3292240]：
$$
\begin{align*}
x_{1} = \left(1+\alpha t\right)X_{1} + \beta t\,X_{2} \\
x_{2} = \gamma t\,X_{1} + \left(1+\delta t\right)X_{2} + \epsilon t^{2} X_{3} \\
x_{3} = \left(1+\zeta t\right)X_{3}\,\exp\left(\kappa X_{1}\right)
\end{align*}
$$
通过直接求导，我们可以得到形变梯度 $\boldsymbol{F} = \partial \boldsymbol{x} / \partial \boldsymbol{X}$，并计算其行列式得到雅可比 $J(\boldsymbol{X}, t)$。这个具体的例子展示了 $J$ 通常既依赖于时间 $t$ 也依赖于参考位置 $\boldsymbol{X}$，反映了非均匀的网格变形。

#### 速度场

在ALE框架中，区分三种不同的速度场至关重要：
1.  **物质速度** $\boldsymbol{u}(\boldsymbol{x}, t)$：这是流体质点的真实速度，描述了物理介质本身的运动。
2.  **网格速度** $\boldsymbol{w}(\boldsymbol{x}, t)$：这是计算网格点的速度。它由ALE映射的时间导数定义，即保持参考坐标 $\boldsymbol{X}$ 不变，对 $\boldsymbol{\chi}$ 求时间偏导：
    $$
    \boldsymbol{w}_{\text{ref}}(\boldsymbol{X}, t) = \left.\frac{\partial \boldsymbol{\chi}(\boldsymbol{X}, t)}{\partial t}\right|_{\boldsymbol{X}}
    $$
    为了在物理域中定义网格速度场，我们需要使用逆映射 $\boldsymbol{X} = \boldsymbol{\chi}^{-1}(\boldsymbol{x}, t)$ 进行坐标变换：
    $$
    \boldsymbol{w}(\boldsymbol{x}, t) = \left.\frac{\partial \boldsymbol{\chi}(\boldsymbol{X}, t)}{\partial t}\right|_{\boldsymbol{X}=\boldsymbol{\chi}^{-1}(\boldsymbol{x},t)}
    $$
    [@problem_id:3292256]
3.  **对流速度** $\boldsymbol{c}(\boldsymbol{x}, t)$：这是物质相对于运动网格的速度，定义为物质速度与网格速度之差：
    $$
    \boldsymbol{c}(\boldsymbol{x}, t) = \boldsymbol{u}(\boldsymbol{x}, t) - \boldsymbol{w}(\boldsymbol{x}, t)
    $$
    这个相对速度是ALE描述中对流通量的核心。当 $\boldsymbol{w}=\boldsymbol{0}$ 时，我们回到经典的 **欧拉描述**，网格固定，对流速度即为物质速度 $\boldsymbol{u}$。当 $\boldsymbol{w}=\boldsymbol{u}$ 时，我们得到 **拉格朗日描述**，网格随流体质点一起运动，对流速度为零。一般的ALE描述则处于这两者之间，即 $\boldsymbol{0} \neq \boldsymbol{w} \neq \boldsymbol{u}$。

### ALE框架下的控制方程

将流体力学中的守恒定律从传统的欧拉或拉格朗日框架转换到ALE框架，需要仔细处理时间导数和积分域的变化。

#### 不同参考系下的时间导数

对于一个标量场 $\phi(\boldsymbol{x}, t)$，存在三种主要的时间导数：
- **欧拉时间导数** $\left.\frac{\partial \phi}{\partial t}\right|_{\boldsymbol{x}}$：在物理空间中一个固定点 $\boldsymbol{x}$ 处 $\phi$ 的变化率。
- **ALE时间导数** $\left.\frac{\partial \phi}{\partial t}\right|_{\boldsymbol{X}}$：跟随一个固定参考点 $\boldsymbol{X}$（即一个网格点）的观察者所测得的 $\phi$ 的变化率。根据链式法则，我们有：
  $$
  \left.\frac{\partial \phi}{\partial t}\right|_{\boldsymbol{X}} = \frac{\partial}{\partial t}\left[ \phi(\boldsymbol{\chi}(\boldsymbol{X}, t), t) \right] = \left.\frac{\partial \phi}{\partial t}\right|_{\boldsymbol{x}} + \nabla\phi \cdot \left.\frac{\partial \boldsymbol{\chi}}{\partial t}\right|_{\boldsymbol{X}} = \left.\frac{\partial \phi}{\partial t}\right|_{\boldsymbol{x}} + \boldsymbol{w} \cdot \nabla\phi
  $$
- **物质导数** (或拉格朗日导数) $\frac{D \phi}{D t}$：跟随一个流体质点的观察者所测得的 $\phi$ 的变化率，其定义为：
  $$
  \frac{D \phi}{D t} = \left.\frac{\partial \phi}{\partial t}\right|_{\boldsymbol{x}} + \boldsymbol{u} \cdot \nabla\phi
  $$

通过组合这些定义，我们可以得到物质导数和ALE导数之间的基本关系。将 $\left.\frac{\partial \phi}{\partial t}\right|_{\boldsymbol{x}} = \left.\frac{\partial \phi}{\partial t}\right|_{\boldsymbol{X}} - \boldsymbol{w} \cdot \nabla\phi$ 代入物质导数的定义，可得：
$$
\frac{D \phi}{D t} = \left.\frac{\partial \phi}{\partial t}\right|_{\boldsymbol{X}} + (\boldsymbol{u} - \boldsymbol{w}) \cdot \nabla\phi = \left.\frac{\partial \phi}{\partial t}\right|_{\boldsymbol{X}} + \boldsymbol{c} \cdot \nabla\phi
$$
这个重要的恒等式 [@problem_id:3292294] 表明，一个流体质点的属性变化率等于在相应网格点上的变化率加上由相对速度 $\boldsymbol{c}$ 引起的对流变化。

#### 雷诺输运定理

雷诺输运定理 (Reynolds Transport Theorem, RTT) 是推导积分形式守恒律的基石，它描述了在一个随时间变化的控制体积 $V(t)$ 上物理量积分的时间导数。对于一个标量场 $\phi$，其通用形式为：
$$
\frac{d}{dt} \int_{V(t)} \phi \, dV = \int_{V(t)} \frac{\partial \phi}{\partial t} \, dV + \int_{\partial V(t)} \phi (\boldsymbol{v}_b \cdot \boldsymbol{n}) \, dS
$$
其中 $\boldsymbol{v}_b$ 是控制体积边界 $\partial V(t)$ 的速度，$\boldsymbol{n}$ 是边界的外法向单位向量。

在ALE框架中，我们的控制体积就是计算网格单元，其边界以网格速度 $\boldsymbol{w}$ 运动。因此，ALE形式的雷诺输运定理为 [@problem_id:3292294] [@problem_id:3292270]：
$$
\frac{d}{dt} \int_{\Omega(t)} \phi \, dV = \int_{\Omega(t)} \frac{\partial \phi}{\partial t} \, dV + \int_{\partial \Omega(t)} \phi (\boldsymbol{w} \cdot \boldsymbol{n}) \, dS
$$
这个定理可以通过将积分变换到固定的参考域，然后利用雅可比的时间演化关系从第一性原理推导出来。例如，在一个以速度 $\boldsymbol{w}(\boldsymbol{x},t) = \frac{\dot{R}(t)}{R(t)} \boldsymbol{x}$ 均匀膨胀的球形域 $\Omega(t) = \{\boldsymbol{x} : |\boldsymbol{x}|  R(t)\}$ 中，我们可以对给定的标量场 $\phi(\boldsymbol{x},t)$ 应用此定理，精确计算其总积分随时间的变化率 [@problem_id:3292270]。

#### ALE形式的守恒律

一个一般的标量守恒律，在欧拉框架下的积分形式为：
$$
\frac{d}{dt} \int_{V} q \, dV + \int_{\partial V} \boldsymbol{F} \cdot \boldsymbol{n} \, dS = \int_{V} S \, dV
$$
其中 $V$ 是一个固定的控制体积，$q$ 是守恒量密度，$\boldsymbol{F}$ 是通量，而 $S$ 是源项。

要在ALE框架下表述此定律，我们考虑一个随网格运动的控制体积 $\Omega(t)$。物质通过控制体积边界的净通量是由相对速度（对流速度）$\boldsymbol{c} = \boldsymbol{u} - \boldsymbol{w}$ 驱动的。因此，ALE积分形式的守恒律为：
$$
\frac{d}{dt} \int_{\Omega(t)} q \, dV + \int_{\partial \Omega(t)} (q\boldsymbol{c}) \cdot \boldsymbol{n} \, dS = \int_{\Omega(t)} S' \, dV
$$
这里的通量项包括了物质对流和物理扩散（如果存在的话），源项 $S'$ 可能也包含由坐标变换产生的几何项。

结合雷诺输运定理，我们可以得到另一种常用的积分形式：
$$
\int_{\Omega(t)} \frac{\partial q}{\partial t} \, dV + \int_{\partial \Omega(t)} q (\boldsymbol{u} \cdot \boldsymbol{n}) \, dS = \int_{\Omega(t)} S \, dV
$$
注意这里的 $\frac{\partial q}{\partial t}$ 是欧拉导数。将此守恒定律转换到ALE框架下，通常最终会得到以ALE时间导数 $\frac{\partial}{\partial t}|_{\boldsymbol{X}}$ 和对流通量 $\boldsymbol{c}$ 为核心的方程。这个过程对于建立离散的有限体积格式至关重要。

特别地，边界上的流入和流出条件也取决于对流速度。流入（物质进入计算域）的条件是 $\boldsymbol{c} \cdot \boldsymbol{n}  0$，即 $(\boldsymbol{u}-\boldsymbol{w}) \cdot \boldsymbol{n}  0$。这与欧拉框架下的流入条件 $\boldsymbol{u} \cdot \boldsymbol{n}  0$ 形成对比 [@problem_id:3292294]。

### 几何守恒律 (GCL)

在ALE模拟中，一个至关重要的概念是 **几何守恒律** (Geometric Conservation Law, GCL)。GCL并非一个新的物理定律，而是一个为了确保数值格式一致性所必须满足的运动学约束。它要求网格运动本身必须精确地满足体积守恒。

#### GCL的原理与推导

GCL的本质是，一个控制体积的变化率必须等于其边界速度通量的积分。这可以从雷诺输运定理中通过令被积函数为1得到：
$$
\frac{d}{dt} \int_{\Omega(t)} 1 \, dV = \int_{\partial \Omega(t)} \boldsymbol{w} \cdot \boldsymbol{n} \, dS
$$
左边是控制体积 $V(t)$ 的时间变化率，右边是网格速度在边界上的通量。利用散度定理，我们可以得到其微分形式。在物理坐标系下，这等价于：
$$
\frac{d V}{dt} = \int_{\Omega(t)} (\nabla \cdot \boldsymbol{w}) \, dV
$$
要得到在ALE计算中更有用的形式，我们需要将这个关系与雅可比 $J$ 的演化联系起来。可以证明，雅可比的时间演化遵循以下恒等式 [@problem_id:3292294] [@problem_id:3292251]：
$$
\left.\frac{\partial J}{\partial t}\right|_{\boldsymbol{X}} = J (\nabla \cdot \boldsymbol{w})
$$
这个关系被称为 **欧拉展开公式**，它对任何ALE运动都成立，而不仅限于拉格朗日运动。如果我们将此关系应用于计算雅可比的倒数 $\mathcal{J} = 1/J$，我们可以得到GCL的一个常见微分形式：
$$
\left.\frac{\partial \mathcal{J}}{\partial t}\right|_{\boldsymbol{X}} + \mathcal{J} (\nabla \cdot \boldsymbol{w}) = 0
$$

#### 违反GCL的后果

在数值实现中，网格节点的更新和网格速度的计算可能通过不同的途径完成。如果计算守恒律方程时所用的网格速度 $\boldsymbol{w}$ 与实际的网格几何更新（即 $\mathcal{J}$ 的变化）不一致，GCL就会被违反。这将导致一个非零的残差：
$$
R = \left.\frac{\partial \mathcal{J}}{\partial t}\right|_{\boldsymbol{X}} + \mathcal{J} (\nabla \cdot \boldsymbol{w}) \neq 0
$$
这个残差 $R$ 会在守恒律方程中表现为一个虚假的、非物理的源项，从而破坏数值解的守恒性和准确性。例如，即使在均匀流场（常数解）中，一个不满足GCL的ALE格式也会错误地产生非零的流场变化，这种现象被称为无法保持 **自由流**（freestream preservation）[@problem_id:3292251]。在一个封闭系统（如周期性边界）中模拟均匀流场时，满足GCL是确保总能量等守恒量不因网格运动而产生虚假变化的必要条件 [@problem_id:3292297]。

#### 离散GCL

在有限体积法 (FVM) 等离散方法中，GCL必须在每个离散的控制体积（网格单元）上得到满足。对于一个体积为 $V_i$ 的网格单元，其离散GCL可以写为：
$$
\frac{d V_i}{dt} - \sum_{f \in \partial V_i} (\boldsymbol{w}_f \cdot \boldsymbol{S}_f) = 0
$$
其中，$\boldsymbol{S}_f$ 是单元面 $f$ 的面积向量，$\boldsymbol{w}_f$ 是在该面上定义的网格速度。这个方程要求单元体积的变化率必须精确等于通过其所有面的网格速度通量之和。

为了满足这个离散GCL，必须谨慎选择面速度 $\boldsymbol{w}_f$ 的计算方式。一个常见的做法是基于构成该面的节点速度进行插值。可以证明，对于线性运动的单元（如二维平行四边形或三维平行六面体），将面心速度取为该面所有顶点速度的算术平均值（即中点法则），可以精确满足离散GCL [@problem_id:3292280]。例如，对于一个由顶点 $i$ 和 $i+1$ 构成的面，选择面速度为 $\boldsymbol{w}_{f} = \frac{1}{2}(\boldsymbol{v}_i + \boldsymbol{v}_{i+1})$，就能保证自由流守恒。

### 网格运动机制

ALE框架的灵活性源于网格速度 $\boldsymbol{w}$ 的任意性。然而，这种任意性也带来了挑战：我们必须设计一种策略来规定网格的运动。一个好的网格运动策略应能适应边界的变形，同时在内部区域保持高质量的网格（即避免单元过度拉伸、压缩或扭曲）。

实践中，网格速度通常不是直接规定的，而是通过求解网格位移场 $\boldsymbol{d}(\boldsymbol{X}, t)$ 得到的，其中 $\boldsymbol{x}(\boldsymbol{X}, t) = \boldsymbol{X} + \boldsymbol{d}(\boldsymbol{X}, t)$。一旦在每个时间步求解出位移场 $\boldsymbol{d}$，网格速度就可以通过时间差分（例如，$\boldsymbol{w} \approx \frac{\boldsymbol{d}^{n+1} - \boldsymbol{d}^n}{\Delta t}$）来近似。

求解位移场 $\boldsymbol{d}$ 的常用方法是引入一种“伪物理”模型，将网格视为一个虚拟的连续介质，并求解其在边界位移驱动下的平衡方程。三种经典的伪物理方法包括 [@problem_id:3292272]：

1.  **拉普拉斯平滑 (Laplacian Smoothing)**：此方法旨在生成尽可能平滑的位移场。它通过求解一个向量形式的拉普拉斯方程来实现：
    $$
    \nabla \cdot (\boldsymbol{K} \nabla \boldsymbol{d}) = \boldsymbol{0}
    $$
    其中 $\boldsymbol{K}$ 是一个“扩散”张量。在最简单的情况下，$\boldsymbol{K}$ 是一个常数标量，方程简化为 $\nabla^2 \boldsymbol{d} = \boldsymbol{0}$。更高级的实现中，$\boldsymbol{K}$ 可以是空间变化的、各向异性的张量，例如使其与网格单元的体积或形状相关，以更好地控制网格质量。

2.  **线弹性类比 (Linear Elasticity)**：此方法将计算网格视为一个虚拟的线弹性固体，并求解其在准静态平衡下的位移。在没有体力的情况下，平衡方程为 $\nabla \cdot \boldsymbol{\sigma} = \boldsymbol{0}$，其中 $\boldsymbol{\sigma}$ 是应力张量。对于各向同性线弹性材料，应力-应变关系（胡克定律）导致了如下关于位移 $\boldsymbol{d}$ 的纳维-柯西方程 (Navier-Cauchy equation)：
    $$
    \mu \nabla^2 \boldsymbol{d} + (\lambda + \mu) \nabla(\nabla \cdot \boldsymbol{d}) = \boldsymbol{0}
    $$
    其中 $\lambda$ 和 $\mu$ 是拉梅参数。相比于拉普拉斯平滑，弹性模型能更好地抵抗大变形下的网格扭曲，尤其是在处理旋转运动时。

3.  **弹簧类比 (Spring Analogy)**：这是一个离散的方法，将网格的每条边都看作一根弹簧。每个内部节点的位置通过使其所连接的所有弹簧力达到平衡来确定。对于节点 $i$，其平衡方程为：
    $$
    \sum_{j \in \mathcal{N}(i)} k_{ij} (\boldsymbol{d}_j - \boldsymbol{d}_i) = \boldsymbol{0}
    $$
    其中 $k_{ij}$ 是连接节点 $i$ 和 $j$ 的弹簧刚度。刚度 $k_{ij}$ 通常被设置为与边长成反比，以使较短的边（更易受挤压）具有更大的抵抗力。可以证明，在连续介质的极限下，弹簧类比方法等价于一个具有非均匀、各向异性扩散系数的拉普拉斯平滑模型。

### 应用与背景

#### 物理源项与几何源项

在进行坐标变换时，区分 **物理源项** 和 **几何源项** 至关重要。物理源项（如化学反应速率、体力）是独立于坐标系存在的。在坐标变换下，一个单位物理体积的物理源项 $S_{\text{phys}}$ 会变为单位计算体积的源项 $J S_{\text{phys}}$。

然而，控制方程在非笛卡尔坐标系下（如柱坐标或ALE框架）的表达形式中，常常会出现一些看起来像源项的附加项。这些项源于基向量或度量系数随空间位置的变化，它们是坐标系本身的几何属性，而非物理过程。例如，在柱坐标下的动量方程中出现的科里奥利力项和离心力项（如 $u_{\theta}^2/r$）就是几何源项。它们在笛卡尔坐标系下会自然消失。在ALE方程中，由网格运动产生的项（如包含 $\boldsymbol{w}$ 或 $\partial J / \partial t$ 的项）同样是几何性质的 [@problem_id:3363953]。将这些几何项与真实的物理源项混淆会导致严重的建模错误。

#### ALE在界面流问题中的应用

ALE方法的一个关键应用领域是两相流或多相流问题，特别是当需要精确追踪流体之间界面的时候。在这种 **界面拟合** (interface-fitting) 方法中，网格边界与物理界面 $\Gamma(t)$ 完全重合。这与 **界面捕捉** (interface-capturing) 方法（如流体体积法VOF或水平集法Level Set）形成对比，后者在固定的欧拉网格上通过一个辅助标量场来隐式地表示界面的位置。

- **运动学条件**：
    - 在ALE中，为了让网格与物质界面保持一致，网格的法向速度必须等于流体的法向速度，即 $(\boldsymbol{u} - \boldsymbol{w}) \cdot \boldsymbol{n} = 0$。
    - 在界面捕捉方法中，定义界面的标量函数（如水平集函数 $\phi$）必须随流体一起平流，即满足 $\frac{D\phi}{Dt} = \frac{\partial \phi}{\partial t} + \boldsymbol{u} \cdot \nabla\phi = 0$。

- **适用场景**：
    - **ALE** 的优势在于它能提供一个清晰、无扩散的界面表示。这使得计算界面曲率等几何量非常精确，对于表面张力主导的流动至关重要。此外，界面上的边界条件（如流固耦合约束）可以被精确施加。其主要缺点是难以处理剧烈的界面拓扑变化，如界面的断裂和融合，因为这会导致网格严重扭曲甚至失效。
    - **界面捕捉** 方法的主要优势是其处理复杂拓扑变化的鲁棒性。界面的融合与断裂可以被自动、自然地处理。其缺点是界面在数值上是弥散的（通常跨越几个网格单元），导致几何属性计算不精确，且在界面上施加精确边界条件较为困难。

因此，当界面在模拟过程中保持拓扑简单（无断裂或融合），且需要高精度地施加界面边界条件（如研究小幅振荡的液滴或稳定的流固耦合问题）时，ALE方法是首选。反之，对于涉及剧烈拓扑变化的现象（如射流雾化、波浪破碎），界面捕捉方法则更为合适 [@problem_id:3292246]。