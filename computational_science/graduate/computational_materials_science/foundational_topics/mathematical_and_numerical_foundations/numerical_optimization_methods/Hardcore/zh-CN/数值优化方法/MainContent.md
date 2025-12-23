## 引言
[数值优化](@entry_id:138060)方法是现代[计算材料科学](@entry_id:145245)的基石，它将抽象的理论模型与可预测的物理现实紧密相连。无论是探索新材料的[基态](@entry_id:150928)结构，模拟[化学反应](@entry_id:146973)的路径，还是校准描述复杂相互作用的[力场](@entry_id:147325)，其核心都归结为一个共同的挑战：如何在广阔而复杂的参数空间中高效地找到最优解。这一挑战构成了理论与实践之间的关键知识鸿沟，掌握其解决方法是所有计算科学家的必备技能。

本文旨在系统性地梳理[数值优化](@entry_id:138060)的核心理论与前沿应用。我们将从第一章“原理与机制”开始，深入剖析支撑优化的数学基础，包括[势能面](@entry_id:147441)、梯度与Hessian矩阵，并系统评述从[梯度下降](@entry_id:145942)到[准牛顿法](@entry_id:138962)、再到[贝叶斯优化](@entry_id:175791)等一系列关键算法。随后的第二章“应用与跨学科联系”将视野拓宽，通过丰富的案例展示这些算法如何在结构预测、模型开发、拓扑优化等具体研究中发挥作用。最后，在“动手实践”部分，读者将有机会通过解决具体问题来巩固所学知识。

通过这一结构化的学习路径，本文将引导读者建立一个从理论到实践的完整知识框架，不仅理解“如何”使用优化工具，更能洞察其“为何”如此工作的深层原理。

## 原理与机制

在[计算材料科学](@entry_id:145245)中，从原子尺度到宏观尺度，优化是连接理论模型与可预测模拟的核心。无论是预测晶体的[基态](@entry_id:150928)结构、确定[相变](@entry_id:147324)路径，还是校准一个经验性[原子间势](@entry_id:177673)，其核心任务都可以表述为寻找一个能量或[误差函数](@entry_id:176269)的最小值。本章旨在阐述支撑这些[数值优化](@entry_id:138060)任务的基本原理和关键机制。我们将从描绘[优化问题](@entry_id:266749)所在的“能量形貌”开始，介绍表征该形貌的数学工具，然后系统地探讨一系列从基本到前沿的[优化算法](@entry_id:147840)，并揭示它们在求解[材料科学](@entry_id:152226)问题中的作用和行为。

### 优化形貌：[势能面](@entry_id:147441)

在[原子模拟](@entry_id:199973)中，系统的构型可以用一个高维向量 $\mathbf{x}$ 来描述，该向量通常包含了所有原子的坐标。系统的总势能 $E(\mathbf{x})$ 是一个依赖于这些坐标的标量函数，构成了所谓的**[势能面](@entry_id:147441)（Potential Energy Surface, PES）**。从物理学的角度看，稳定的材料结构对应于[势能面](@entry_id:147441)上的极小值点。其中，能量最低的极小值点被称为**[全局最小值](@entry_id:165977)**，对应于系统的**[基态](@entry_id:150928)**；而其他的局部极小值点则对应于**亚稳态**结构。

为周期性系统（如晶体）定义一个明确的[势能面](@entry_id:147441)需要特别注意。在一个由[晶格矢量](@entry_id:161583)矩阵 $\mathbf{A}$ 定义的元胞中，原子的位置通常用分数坐标 $\mathbf{s} \in ([0,1)^3)^N$ 表示。由于系统的周期性，原子间的相互作用必须考虑其所有周期性映象。对于[短程相互作用](@entry_id:145678)势 $\varphi(r)$，这通常通过**最小映象约定（minimum image convention）**来实现，即仅考虑一对原子之间所有周期性映象中最短的距离。因此，系统的总能量可以严谨地定义为：
$$
E(\mathbf{s}) = \frac{1}{2}\sum_{i \ne j} \varphi\left( \min_{\mathbf{n}\in \mathbb{Z}^3} \left\| \mathbf{A}(\mathbf{s}_i - \mathbf{s}_j + \mathbf{n}) \right\|_2 \right)
$$
此能量函数具有[平移不变性](@entry_id:195885)，即同时平移所有原子，能量不变。这意味着[势能面](@entry_id:147441)在与整体平移对应的方向上是“平坦的”。为了正确地定义极小值，我们通常在除去这些平移自由度的商[构型空间](@entry_id:149531) $\mathcal{C}$ 上进行分析 。

一个构型 $\mathbf{s}^{\text{loc}}$ 如果是[局部极小值](@entry_id:143537)，意味着任何对其微小的扰动都会导致能量升高。而全局最小值 $\mathbf{s}^{\star}$ 则是整个[势能面](@entry_id:147441)上能量最低的点。亚稳态的“稳定性”是一个动力学概念。一个系统从一个亚稳态（[局部极小值](@entry_id:143537)）转变为另一个能量更低的状态，必须克服一个能量壁垒。这个壁垒的最小高度 $\Delta E^\ddagger$ 定义了该状态的[动力学稳定性](@entry_id:150175)。根据**[过渡态理论](@entry_id:178694)（Transition State Theory）**，在有限温度 $T$ 下，系统逃离该亚稳态的速率 $k$ 与壁垒高度呈指数关系，即 $k \propto \exp(-\Delta E^\ddagger / (k_{\mathrm{B}} T))$。当能量壁垒远大于热能（$\Delta E^\ddagger \gg k_{\mathrm{B}} T$）时，系统会在该亚稳态停留很长时间，从而在实验上可观测到，并表现出诸如[磁滞](@entry_id:145766)等现象 。

### 形貌的数学表征：梯度与Hessian矩阵

为了在[势能面](@entry_id:147441)上导航并定位极小值，我们需要局部几何信息，这由能量函数的一阶和[二阶导数](@entry_id:144508)提供。

#### 梯度：力与最速下降方向

[势能面](@entry_id:147441) $E(\mathbf{x})$ 的**梯度（gradient）**是一个向量，记作 $\nabla E(\mathbf{x})$，其每个分量是能量对相应坐标的偏导数，即 $[\nabla E(\mathbf{x})]_{i\alpha} = \frac{\partial E}{\partial x_{i\alpha}}$。在物理上，作用在原子 $i$ 上的力 $F_i$ 与能量梯度的关系为 $F(\mathbf{x}) = -\nabla E(\mathbf{x})$。因此，梯度的负方向即为系统受力的方向，也是能量下降最快的**[最速下降](@entry_id:141858)方向**。

在[势能面](@entry_id:147441)的任何一个平稳点（包括极小值、极大值和[鞍点](@entry_id:142576)），作用在每个原子上的净力为零，这意味着[梯度向量](@entry_id:141180)为零：
$$
\nabla E(\mathbf{x}^\star) = \mathbf{0}
$$
这个条件被称为**[一阶必要条件](@entry_id:170730)**，是所有[优化算法](@entry_id:147840)寻找目标的基础 。

#### Hessian矩阵：刚度与曲率

**Hessian矩阵** $\nabla^2 E(\mathbf{x})$ 是一个由能量[二阶偏导数](@entry_id:635213)组成的方阵，其元素为 $(\nabla^2 E)_{i\alpha, j\beta} = \frac{\partial^2 E}{\partial x_{i\alpha} \partial x_{j\beta}}$。由于能量函数通常是二次连续可微的（$C^2$），根据[Clairaut定理](@entry_id:139814)，混合偏导的次序无关紧要，因此Hessian矩阵是对称的。

Hessian矩阵描述了[势能面](@entry_id:147441)的局部曲率。它的物理意义是**刚度矩阵**或**[力常数](@entry_id:156420)矩阵**。在一个[平衡点](@entry_id:272705) $\mathbf{x}^\star$ 附近，对于一个微小的位移 $\delta \mathbf{x}$，系统产生的恢复力近似为[线性关系](@entry_id:267880)：
$$
F(\mathbf{x}^\star + \delta \mathbf{x}) \approx -\nabla^2 E(\mathbf{x}^\star)\,\delta \mathbf{x}
$$
这本质上是胡克定律的推广。Hessian矩阵的[本征值](@entry_id:154894)和[本征向量](@entry_id:151813)对应于系统的[振动](@entry_id:267781)模式（[声子](@entry_id:140728)）及其频率的平方 。

Hessian矩阵的谱（[本征值](@entry_id:154894)集合）是区分不同类型[临界点](@entry_id:144653)的关键，这构成了**[二阶充分条件](@entry_id:635498)** ：
*   **严格局部极小值 (Strict Local Minimum)**：所有[本征值](@entry_id:154894)均为正。这表示[势能面](@entry_id:147441)在所有方向上都是向上弯曲的。
*   **严格[局部极大值](@entry_id:137813) (Strict Local Maximum)**：所有[本征值](@entry_id:154894)均为负。
*   **[鞍点](@entry_id:142576) (Saddle Point)**：[本征值](@entry_id:154894)中既有正值也有负值。[势能面](@entry_id:147441)在某些方向上像山谷，在另一些方向上像山脊。

对于一个孤立的原子团簇或一个具有连续对称性的周期性系统，其Hessian矩阵必然存在零[本征值](@entry_id:154894)。例如，整个系统的刚性平移或旋转不会改变其能量。这些[零能模式](@entry_id:172472)对应于Hessian矩阵的零[本征值](@entry_id:154894)，这意味着二阶测试在这些方向上是无结论的。在这种情况下，Hessian矩阵是半正定的（对于一个非严格的[局部极小值](@entry_id:143537)），而不是严格正定的  。

### [无约束优化](@entry_id:137083)核心算法

大多数[结构弛豫](@entry_id:263707)问题在形式上是[无约束优化](@entry_id:137083)问题。算法的目标是从一个初始猜测点出发，迭代地走向一个能量更低的局部极小值。

#### 一阶方法：最速下降法

最简单的方法是**[梯度下降法](@entry_id:637322)（Gradient Descent）**，或称**[最速下降法](@entry_id:140448)**。其迭代格式为：
$$
\mathbf{x}_{k+1} = \mathbf{x}_{k} - \alpha_k \nabla E(\mathbf{x}_k)
$$
其中 $\alpha_k > 0$ 是步长，可以通过线搜索等策略确定。该方法直观地沿着能量下降最快的方向移动。然而，它的[收敛速度](@entry_id:636873)可能非常慢，尤其是在狭长的“山谷”中会表现出锯齿形路径。更严重的是，在梯度下降法在高维非凸问题中，它很容易在[鞍点](@entry_id:142576)附近**停滞**。在一个典型的[鞍点](@entry_id:142576)附近，存在曲率大的“陡峭”方向和曲率小（甚至为负）的“平缓”方向。为了在陡峭方向上保持稳定，步长 $\alpha_k$ 必须非常小，但这使得沿平缓[负曲率](@entry_id:159335)方向（逃离[鞍点](@entry_id:142576)的方向）的移动极其缓慢 。

#### 二阶方法：牛顿法

**牛顿法（Newton's Method）**利用了二阶信息（曲率）来寻找更优的[下降方向](@entry_id:637058)。该方法通过构建一个当前点 $\mathbf{x}_k$ 附近的二次模型 $m_k(\mathbf{p}) = E(\mathbf{x}_k) + \nabla E(\mathbf{x}_k)^\top \mathbf{p} + \frac{1}{2}\mathbf{p}^\top \nabla^2 E(\mathbf{x}_k) \mathbf{p}$ 来近似[势能面](@entry_id:147441)，并直接跳到这个模型的极小值点。这给出了[牛顿步长](@entry_id:177069) $\mathbf{p}_k = -[\nabla^2 E(\mathbf{x}_k)]^{-1} \nabla E(\mathbf{x}_k)$，迭代格式为：
$$
\mathbf{x}_{k+1} = \mathbf{x}_{k} - [\nabla^2 E(\mathbf{x}_k)]^{-1} \nabla E(\mathbf{x}_k)
$$
在局部极小值附近，牛顿法展现出极快的**二次收敛**速度。然而，它也有显著的缺点：(1) 需要计算并求解Hessian矩阵的逆，这对于[大规模系统](@entry_id:166848)来说计算成本高昂；(2) 当Hessian矩阵不是正定时（例如在[鞍点](@entry_id:142576)附近），[牛顿步长](@entry_id:177069)可能指向能量更高的方向，导致算法发散 。

#### 准牛顿方法：BFGS

**准牛顿方法（Quasi-Newton Methods）**旨在结合[梯度下降法](@entry_id:637322)的低成本和牛顿法的快速收敛性。它通过迭代地构建Hessian矩阵的近似（或其逆矩阵的近似）来实现这一点，而无需显式计算[二阶导数](@entry_id:144508)。

核心思想是**[割线条件](@entry_id:164914)（secant condition）**。令 $\mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k$ 和 $\mathbf{y}_k = \nabla E(\mathbf{x}_{k+1}) - \nabla E(\mathbf{x}_k)$。[割线条件](@entry_id:164914)要求Hessian的逆[矩阵近似](@entry_id:149640) $H_{k+1}$ 满足 $H_{k+1}\mathbf{y}_k = \mathbf{s}_k$。在众多满足此条件的更新方案中，**BFGS (Broyden–Fletcher–Goldfarb–Shanno)** 更新公式最为成功和常用。对于逆Hessian的近似，其更[新形式](@entry_id:199611)为：
$$
H_{k+1} = \left(I - \rho_{k}\, \mathbf{s}_{k} \mathbf{y}_{k}^{\top}\right) H_{k} \left(I - \rho_{k}\, \mathbf{y}_{k} \mathbf{s}_{k}^{\top}\right) + \rho_{k}\, \mathbf{s}_{k} \mathbf{s}_{k}^{\top}, \quad \text{其中 } \rho_{k} = \frac{1}{\mathbf{y}_{k}^{\top} \mathbf{s}_{k}}
$$
[BFGS算法](@entry_id:263685)的一个关键优点是，只要初始近似 $H_0$ 是对称正定的，并且满足**曲率条件** $\mathbf{y}_k^\top \mathbf{s}_k > 0$（这在[线搜索](@entry_id:141607)中可以保证），那么后续所有的 $H_k$ 都会保持[对称正定](@entry_id:145886)性。这确保了每一步都是下降方向，使得算法稳健而高效 。

#### [信赖域方法](@entry_id:138393)

**[信赖域方法](@entry_id:138393)（Trust-Region Methods）**是另一类稳健的二阶方法，它为牛顿法的不稳定性提供了一个优雅的解决方案。其核心思想是，在每一步迭代中，首先确定一个“信赖域”（通常是围绕当前点 $\mathbf{x}_k$ 的一个半径为 $\Delta_k$ 的球），然后在这个区域内求解二次模型 $m_k(\mathbf{p})$ 的最小化问题：
$$
\min_{\mathbf{p}\in\mathbb{R}^n:\,\|\mathbf{p}\|\le \Delta_k} \; m_k(\mathbf{p}) \equiv \mathbf{g}_k^\top \mathbf{p} + \tfrac{1}{2}\,\mathbf{p}^\top B_k \mathbf{p}
$$
其中 $\mathbf{g}_k$ 是梯度， $B_k$ 是Hessian或其近似。如果求出的步长 $\mathbf{p}_k$ 使得真实能量下降显著，则可以扩大信赖域；否则，缩小信赖域。

精确求解这个子问题可能很困难。实践中通常采用近似解。例如：
*   **[柯西点](@entry_id:177064)（Cauchy point）**：沿着[最速下降](@entry_id:141858)方向 $-\mathbf{g}_k$ 寻找模型 $m_k(\mathbf{p})$ 在信赖域内的极小值点。这保证了算法的[全局收敛性](@entry_id:635436)。
*   **[狗腿法](@entry_id:139912)（Dogleg method）**：当 $B_k$ 正定时，该方法构造一条连接原点、[柯西点](@entry_id:177064)和（无约束）[牛顿步长](@entry_id:177069)点的分段线性路径。最终的步长是这条路径与信赖域边界的交点，巧妙地在[最速下降](@entry_id:141858)和牛顿法之间进行了插值 。

[信赖域方法](@entry_id:138393)的一个重要优势是，即使 $B_k$ 不定（有负[本征值](@entry_id:154894)），子问题仍然是良定义的，并且可以设计算法利用[负曲率](@entry_id:159335)方向来获得更大的能量下降，从而有效地逃离[鞍点](@entry_id:142576)。

### 高级优化[范式](@entry_id:161181)

许多现代[材料科学](@entry_id:152226)问题超出了简单[无约束优化](@entry_id:137083)的范畴，需要更复杂的框架。

#### 约束优化：[KKT条件](@entry_id:185881)

在[材料设计](@entry_id:160450)中，我们常常需要在满足某些物理或化学约束的条件下进行优化，例如，在设计合金时保持[化学计量](@entry_id:137450)比固定。这类问题属于**约束优化**。一个通用的[约束优化](@entry_id:635027)问题形式如下：
$$
\begin{aligned}
\text{minimize} \quad  f(\mathbf{x}) \\
\text{subject to} \quad  A \mathbf{x} = \mathbf{b} \quad \text{(等式约束)} \\
 C \mathbf{x} \le \mathbf{d} \quad \text{(不等式约束)}
\end{aligned}
$$
解决此类问题的理论基石是**[Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)**。这些条件通过引入[拉格朗日乘子](@entry_id:142696) $\boldsymbol{\lambda}$ 和 $\boldsymbol{\mu}$，将约束问题转化为无约束的[拉格朗日函数](@entry_id:174593) $L(\mathbf{x}, \boldsymbol{\lambda}, \boldsymbol{\mu}) = f(\mathbf{x}) + \boldsymbol{\lambda}^{\top}(A \mathbf{x} - \mathbf{b}) + \boldsymbol{\mu}^{\top}(C \mathbf{x} - \mathbf{d})$ 的分析。对于一个凸[优化问题](@entry_id:266749)，一个点 $\mathbf{x}^\star$ 是最优解的充要条件是存在乘子 $\boldsymbol{\lambda}^\star, \boldsymbol{\mu}^\star$ 使得以下四个条件成立 ：
1.  **平稳性 (Stationarity)**：$\nabla_{\mathbf{x}} L(\mathbf{x}^{\star}, \boldsymbol{\lambda}^{\star}, \boldsymbol{\mu}^{\star}) = \nabla f(\mathbf{x}^{\star}) + A^{\top} \boldsymbol{\lambda}^{\star} + C^{\top} \boldsymbol{\mu}^{\star} = \mathbf{0}$。
2.  **原始可行性 (Primal feasibility)**：$A \mathbf{x}^{\star} = \mathbf{b}$ and $C \mathbf{x}^{\star} \le \mathbf{d}$。
3.  **对偶可行性 (Dual feasibility)**：$\boldsymbol{\mu}^{\star} \ge \mathbf{0}$。
4.  **[互补松弛性](@entry_id:141017) (Complementary slackness)**：$\mu^{\star}_{i} ( (C \mathbf{x}^{\star} - \mathbf{d})_{i} ) = 0$ 对所有 $i$ 成立。

[KKT条件](@entry_id:185881)为[约束优化](@entry_id:635027)算法的设计和验证提供了理论基础。

#### 分解方法：[交替方向乘子法](@entry_id:163024) ([ADMM](@entry_id:163024))

许多问题具有一种特殊结构：目标函数可以分解为几个部分的和，这些部分只通过一个[线性约束](@entry_id:636966)耦合在一起。一个典型的例子是 $\min_{\mathbf{x},\mathbf{z}} f(\mathbf{x})+g(\mathbf{z})$ subject to $A \mathbf{x} + B \mathbf{z} = \mathbf{c}$。

**[交替方向乘子法](@entry_id:163024)（Alternating Direction Method of Multipliers, [ADMM](@entry_id:163024)）**是解决此类问题的强大工具。它基于**增广拉格朗日函数**：
$$
L_{\rho}(\mathbf{x}, \mathbf{z}, \mathbf{y}) = f(\mathbf{x}) + g(\mathbf{z}) + \mathbf{y}^{\top}(A \mathbf{x} + B \mathbf{z} - \mathbf{c}) + \frac{\rho}{2}\|A \mathbf{x} + B \mathbf{z} - \mathbf{c}\|_2^2
$$
ADMM通过将复杂的联合最小化[问题分解](@entry_id:272624)为三个更简单的子问题，并交替进行求解：
1.  **x-更新**: $x^{k+1} = \arg\min_x\; L_{\rho}(x, z^k, y^k)$
2.  **z-更新**: $z^{k+1} = \arg\min_z\; L_{\rho}(x^{k+1}, z, y^k)$
3.  **对偶更新**: $y^{k+1} = y^k + \rho(A x^{k+1} + B z^{k+1} - c)$

该算法的收敛性可以通过监控**原始残差** $r^{k+1} = A x^{k+1} + B z^{k+1} - c$ 和**对偶残差** $s^{k+1} = \rho A^{\top} B (z^{k+1} - z^k)$ 是否趋近于零来判断。ADMM因其分解能力和稳健性，在机器学习、信号处理和[材料信息学](@entry_id:197429)中得到了广泛应用 。

#### [非光滑优化](@entry_id:167581)

在参数校准或逆问题中，[目标函数](@entry_id:267263)可能包含非光滑的正则化项，例如促进稀疏性的 $\ell_1$ 范数，或表示物理可行集的[指示函数](@entry_id:186820)。这类问题属于**非光滑[复合优化](@entry_id:165215)**，其形式通常为 $F(\mathbf{x}) = f(\mathbf{x}) + g(\mathbf{x})$，其中 $f$ 光滑，$g$ 非光滑但凸。

由于梯度在某些点上没有定义，我们需要新的工具。**[次梯度](@entry_id:142710)（subgradient）** $\partial g(\mathbf{x})$ 是梯度概念的推广，它是一个向量集合，其中每个向量都定义了函数 $g$ 的一个[支撑超平面](@entry_id:274981)。[最优性条件](@entry_id:634091)也相应地推广为 $0 \in \nabla f(\mathbf{x}^\star) + \partial g(\mathbf{x}^\star)$。

在算法层面，**[近端算子](@entry_id:635396)（proximal operator）**是解决这类问题的关键。函数 $g$ 的[近端算子](@entry_id:635396)定义为一个微型[优化问题](@entry_id:266749)：
$$
\mathrm{prox}_{\lambda g}(\mathbf{v})=\arg\min_\mathbf{x} \left( g(\mathbf{x})+\tfrac{1}{2\lambda}\|\mathbf{x}-\mathbf{v}\|_2^2 \right)
$$
它在点 $\mathbf{v}$ 附近寻找一个权衡 $g(\mathbf{x})$ 和与 $\mathbf{v}$ 的接近度的点。像**[近端梯度法](@entry_id:634891)（Proximal Gradient Method）**这样的算法利用[近端算子](@entry_id:635396)，将迭代步骤分解为一个在光滑部分 $f$ 上的标准梯度步和一个在非光滑部分 $g$ 上的近端步，从而高效地求解[复合优化](@entry_id:165215)问题 。

#### 内部子问题的求解：[共轭梯度法](@entry_id:143436)与预条件

许多高级优化算法（如[牛顿法](@entry_id:140116)、信赖域法）在其内部迭代中需要求解一个大规模的[线性方程组](@entry_id:148943) $A\mathbf{x}=\mathbf{b}$。当矩阵 $A$ 对称正定（SPD）时，**[共轭梯度法](@entry_id:143436)（Conjugate Gradient, CG）**是一种非常高效的迭代求解器。

CG的收敛速度主要由矩阵 $A$ 的谱特性决定，特别是其**[条件数](@entry_id:145150)** $\kappa(A) = \lambda_{\max}(A)/\lambda_{\min}(A)$。条件数越大，收敛越慢。然而，一个更精细的观点是，[收敛速度](@entry_id:636873)实际上取决于整个[本征值分布](@entry_id:194746)。

**预条件（Preconditioning）**技术通过将原系统转化为一个等价但谱特性更好的系统来加速CG的收敛，例如求解 $M^{-1}A\mathbf{x} = M^{-1}\mathbf{b}$，其中 $M$ 是一个易于求逆的[预条件子](@entry_id:753679)，且 $M \approx A$。一个好的预条件子会使得 $M^{-1}A$ 的[本征值](@entry_id:154894)聚集在一个或几个小区间内。当大部分[本征值](@entry_id:154894)紧密地聚集在1附近，只有少数离群[本征值](@entry_id:154894)时，CG会表现出**[超线性收敛](@entry_id:141654)**：它会在最初的少数几次迭代中“消除”离群[本征值](@entry_id:154894)的影响，然后以与密集谱簇所对应的极低条件数相关的速率快速收敛 。

### [全局优化](@entry_id:634460)与昂贵函数：[贝叶斯优化](@entry_id:175791)

我们前面讨论的算法主要是寻找[局部极小值](@entry_id:143537)。但在许多应用中，我们真正关心的是全局最小值。当函数评估本身非常昂贵时（例如，一次[第一性原理计算](@entry_id:198754)可能需要数小时或数天），传统的[全局优化方法](@entry_id:169046)（如[模拟退火](@entry_id:144939)或[遗传算法](@entry_id:172135)）由于需要大量函数评估而变得不可行。

**[贝叶斯优化](@entry_id:175791)（Bayesian Optimization）**是为这类“昂贵黑箱”函数设计的[全局优化](@entry_id:634460)策略。其核心思想是：
1.  **代理模型 (Surrogate Model)**：用一个廉价的[概率模型](@entry_id:265150)来近似昂贵的真实函数。**[高斯过程](@entry_id:182192)（Gaussian Process, GP）**是一个常用且强大的选择。给定已有的观测数据，GP不仅能提供在任意新点 $\mathbf{x}$ 的函数值的预测均值 $\mu(\mathbf{x})$，还能提供该预测的不确定性（[方差](@entry_id:200758)）$s^2(\mathbf{x})$。
2.  **[采集函数](@entry_id:168889) (Acquisition Function)**：利用GP的[后验分布](@entry_id:145605)（均值和[方差](@entry_id:200758)）来构造一个函数，该函数评估在每个点进行下一次昂贵计算的“价值”，并选择价值最高的点作为下一个采样点。

一个流行的[采集函数](@entry_id:168889)是**[期望提升](@entry_id:749168)（Expected Improvement, EI）**。它计算在某点采样预期能比当前观测到的最优值 $f_{\text{best}}$ 带来多大的提升。对于最大化问题，其[闭式](@entry_id:271343)解为：
$$
\mathrm{EI}(\mathbf{x}) = (\mu(\mathbf{x}) - f_{\mathrm{best}})\,\Phi(z) + s(\mathbf{x})\,\phi(z), \quad \text{其中 } z = \dfrac{\mu(\mathbf{x}) - f_{\mathrm{best}}}{s(\mathbf{x})}
$$
其中 $\Phi$ 和 $\phi$ 分别是[标准正态分布](@entry_id:184509)的CDF和PDF。这个公式优雅地体现了**探索（exploration）**与**利用（exploitation）**的权衡：第一项 $(\mu(\mathbf{x}) - f_{\mathrm{best}})\,\Phi(z)$ 倾向于在预测均值高的区域进行采样（利用），而第二项 $s(\mathbf{x})\,\phi(z)$ 则倾向于在不确定性大的区域进行采样（探索）。[贝叶斯优化](@entry_id:175791)通过这种智能的[采样策略](@entry_id:188482)，力求用最少的函数评估次数找到[全局最优解](@entry_id:175747) 。