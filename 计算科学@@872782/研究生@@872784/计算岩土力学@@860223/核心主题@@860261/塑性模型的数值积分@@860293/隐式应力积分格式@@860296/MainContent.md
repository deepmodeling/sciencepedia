## 引言
在计算岩[土力学](@entry_id:180264)领域，对复杂[弹塑性](@entry_id:193198)本构关系的精确[数值积分](@entry_id:136578)是进行可靠有限元模拟的基石。材料进入塑性状态后，其行为由一组[刚性常微分方程](@entry_id:175905)描述，如何稳定、准确且高效地求解这些方程，是[计算力学](@entry_id:174464)中的一个核心挑战。隐式应力积分格式，因其卓越的[数值稳定性](@entry_id:146550)，已成为解决此类问题的首选方法。

本文旨在全面深入地解析隐式应力积分的理论、应用与实现，弥合理论推导与实际工程模拟之间的鸿沟。通过本文，读者将系统地掌握这一关键数值技术。

文章首先在“原理与机制”一章中，深入剖析[后向欧拉法](@entry_id:139674)和[返回映射算法](@entry_id:168456)的数学框架，探讨其[无条件稳定性](@entry_id:145631)、变分解释以及[求解非线性方程](@entry_id:177343)组的牛顿法，并阐明[一致算法切线模量](@entry_id:747730)对[全局收敛](@entry_id:635436)的重要性。接着，在“应用与交叉学科联系”一章中，将展示这些核心算法如何被用于模拟[非关联塑性](@entry_id:186531)、[材料软化](@entry_id:169591)等复杂岩土行为，并阐明其在水-力-热[多物理场耦合](@entry_id:171389)问题中的关键作用。最后，“动手实践”部分将引导读者通过具体的编程练习，从简单的J2塑性模型到复杂的[Mohr-Coulomb模型](@entry_id:752108)，亲手实现和验证[返回映射算法](@entry_id:168456)，将理论知识转化为实践能力。

## 原理与机制

在计算岩土力学中，对[弹塑性](@entry_id:193198)[本构关系](@entry_id:186508)的精确和稳健的数值积分是进行可靠模拟的基础。上一章介绍了[弹塑性](@entry_id:193198)问题的背景，本章将深入探讨在[有限元分析](@entry_id:138109)框架内求解这些[本构关系](@entry_id:186508)的“原理与机制”，重点关注在岩土工程中占主导地位的隐式应力积分格式。

### 隐式后向欧拉格式：公式与稳定性

[弹塑性](@entry_id:193198)材料的行为通常由一组率形式的方程描述，包括[应力-应变关系](@entry_id:274093)、流动法则和硬化法则。这些方程构成了一个[刚性常微分方程](@entry_id:175905)（ODE）系统，其[数值积分](@entry_id:136578)是[计算力学](@entry_id:174464)中的一个核心挑战。隐式积分格式，特别是**后向欧拉法 (Backward Euler method)**，因其优越的稳定性而被广泛采用。

考虑一个一般的关联[弹塑性](@entry_id:193198)模型，其[屈服函数](@entry_id:167970)为 $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0$，其中 $\boldsymbol{\sigma}$ 是柯西应力张量，$\boldsymbol{\alpha}$ 是一组内蕴硬化变量。应力率由弹性定律给出：$\dot{\boldsymbol{\sigma}} = \mathbb{C}:(\dot{\boldsymbol{\varepsilon}} - \dot{\boldsymbol{\varepsilon}}^{p})$，其中 $\mathbb{C}$ 是四阶弹性劲度张量，$\dot{\boldsymbol{\varepsilon}}$ 是总应变率，$\dot{\boldsymbol{\varepsilon}}^{p}$ 是塑性应变率。对于关联塑性，[塑性流动](@entry_id:201346)方向 $\mathbf{n}$ 垂直于[屈服面](@entry_id:175331)，即 $\mathbf{n} = \partial f / \partial \boldsymbol{\sigma}$，塑性应变率为 $\dot{\boldsymbol{\varepsilon}}^{p} = \dot{\gamma} \mathbf{n}$，其中 $\dot{\gamma} \ge 0$ 是塑性乘子率。

在一个时间步 $\Delta t$（从 $t_n$ 到 $t_{n+1}$）内，给定总应变增量 $\Delta \boldsymbol{\varepsilon}$，我们的目标是更新[状态变量](@entry_id:138790) $(\boldsymbol{\sigma}_{n+1}, \boldsymbol{\alpha}_{n+1})$。后向欧拉法通过在时间步的*末端*（即 $t_{n+1}$ 时刻）评估所有率相关的项来实现积分：

$$
\frac{\boldsymbol{\sigma}_{n+1} - \boldsymbol{\sigma}_n}{\Delta t} \approx \mathbb{C} : \left( \frac{\Delta \boldsymbol{\varepsilon}}{\Delta t} - \dot{\gamma}_{n+1} \mathbf{n}_{n+1} \right)
$$
$$
\frac{\boldsymbol{\alpha}_{n+1} - \boldsymbol{\alpha}_n}{\Delta t} \approx \dot{\gamma}_{n+1} \mathbf{h}(\boldsymbol{\sigma}_{n+1}, \boldsymbol{\alpha}_{n+1})
$$

其中，所有下标为 $n+1$ 的量都在时间步的末端进行评估。将这些方程重新整理并引入塑性乘子增量 $\Delta \gamma = \dot{\gamma}_{n+1} \Delta t$，我们得到一组[非线性](@entry_id:637147)[代数方程](@entry_id:272665)。这个过程通常被构建为一个**弹性预测/塑性修正 (elastic predictor/plastic corrector)** 的框架。

1.  **弹性预测步**：首先，假设整个应变增量 $\Delta \boldsymbol{\varepsilon}$ 都是弹性的。我们计算一个**试探应力 (trial stress)**：
    $$
    \boldsymbol{\sigma}^{\mathrm{trial}} = \boldsymbol{\sigma}_{n} + \mathbb{C}:\Delta \boldsymbol{\varepsilon}
    $$
2.  **屈服检查**：用试探应力评估[屈服函数](@entry_id:167970) $f(\boldsymbol{\sigma}^{\mathrm{trial}}, \boldsymbol{\alpha}_n)$。
    *   如果 $f(\boldsymbol{\sigma}^{\mathrm{trial}}, \boldsymbol{\alpha}_n) \le 0$，说明试探应力在弹性域内或其边界上，弹性假设成立。该步为弹性步，更新的应力就是试探应力：$\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\mathrm{trial}}$。
    *   如果 $f(\boldsymbol{\sigma}^{\mathrm{trial}}, \boldsymbol{\alpha}_n) > 0$，说明试探应力超出了屈服面，弹性假设不成立。必须进行塑性修正。

3.  **塑性修正步**：在这一步中，我们求解 $\Delta\gamma > 0$，使得最终的应力 $\boldsymbol{\sigma}_{n+1}$ 满足屈服条件。应力[更新方程](@entry_id:264802)为：
    $$
    \boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\mathrm{trial}} - \Delta\gamma \, \mathbb{C}:\mathbf{n}_{n+1}
    $$
    同时，内变量和离散形式的 [Kuhn-Tucker 条件](@entry_id:185881)也必须在 $t_{n+1}$ 时刻满足：
    $$
    \boldsymbol{\alpha}_{n+1} = \boldsymbol{\alpha}_{n} + \Delta\gamma \, \mathbf{h}(\boldsymbol{\sigma}_{n+1}, \boldsymbol{\alpha}_{n+1})
    $$
    $$
    \Delta \gamma \ge 0, \quad f(\boldsymbol{\sigma}_{n+1}, \boldsymbol{\alpha}_{n+1}) \le 0, \quad \Delta \gamma \cdot f(\boldsymbol{\sigma}_{n+1}, \boldsymbol{\alpha}_{n+1}) = 0
    $$
    这个将试探应力“[拉回](@entry_id:160816)”到屈服面的过程，被称为**[返回映射算法](@entry_id:168456) (return mapping algorithm)** [@problem_id:3532208]。

这种[隐式格式](@entry_id:166484)的主要优点是其卓越的[数值稳定性](@entry_id:146550)。对于[刚性微分方程](@entry_id:139505)系统，稳定性的一个关键度量是**[A-稳定性](@entry_id:144367) (A-stability)**。一个数值方法如果应用于标量测试方程 $\dot{y} = \lambda y$（其中 $\lambda$ 是一个具有非正实部的复数）时，其[放大因子](@entry_id:144315) $G(z) = y_{n+1}/y_n$（其中 $z = \lambda \Delta t$）的模总是不大于1（$|G(z)| \le 1$），则该方法是 A-稳定的。后向欧拉法的[放大因子](@entry_id:144315)是 $G(z) = 1/(1-z)$，对于所有 $\operatorname{Re}(z) \le 0$，我们都有 $|G(z)| \le 1$。因此，后向欧拉法是 A-稳定的。

在物理上，塑性是一种耗散过程，对应于系统[雅可比矩阵的特征值](@entry_id:264008)具有非正实部。[A-稳定性](@entry_id:144367)保证了无论时间步长 $\Delta t$ 有多大，数值解都不会产生虚假的[振荡](@entry_id:267781)或无限增长。这使得[隐式格式](@entry_id:166484)对于模拟塑性问题具有**[无条件稳定性](@entry_id:145631) (unconditional stability)**，与通常需要很小时间步来维持稳定性的显式格式（如前向欧拉法）形成鲜明对比 [@problem_id:2678286]。

### [返回映射](@entry_id:754324)的变分解释

对于关联塑性模型（即流动法则是关联的），[返回映射算法](@entry_id:168456)有一个深刻的几何和变分解释。塑性修正过程在数学上等价于在一个凸的容许应力空间中，寻找距离弹性试探应力 $\boldsymbol{\sigma}^{\mathrm{trial}}$ 最近的点。这里的“距离”是在由[弹性柔度](@entry_id:189433)张量 $\mathbb{C}^{-1}$ 定义的[能量范数](@entry_id:274966)下度量的 [@problem_id:2678286]。

具体来说，塑性[返回映射](@entry_id:754324)求解的是以下[约束最小化](@entry_id:747762)问题：
$$
\min_{\boldsymbol{\sigma}_{n+1}} \left\{ \frac{1}{2}(\boldsymbol{\sigma}_{n+1} - \boldsymbol{\sigma}^{\mathrm{trial}}) : \mathbb{C}^{-1} : (\boldsymbol{\sigma}_{n+1} - \boldsymbol{\sigma}^{\mathrm{trial}}) \right\} \quad \text{subject to} \quad f(\boldsymbol{\sigma}_{n+1}, \boldsymbol{\alpha}_{n+1}) \le 0
$$
这种将应力更新视为到[凸集](@entry_id:155617)上的**[最近点投影](@entry_id:168047) (closest-point projection)** 的观点，带来了几个重要的理论保证：
1.  **解的存在性和唯一性**：由于是将一个点投影到一个凸集上，对于任何试探应力，都存在一个唯一的解 $\boldsymbol{\sigma}_{n+1}$。
2.  **[无条件稳定性](@entry_id:145631)**：该算法对于任何时间步长 $\Delta t > 0$ 都是稳健和稳定的，在材料本构层面没有稳定性限制。
3.  **[热力学一致性](@entry_id:138886)**：该算法与[最大塑性耗散](@entry_id:184825)原理一致，保证了在任何步长下塑性功都为非负值。

### 求解[返回映射](@entry_id:754324)方程

[返回映射](@entry_id:754324)的隐式性质意味着最终状态 $(\boldsymbol{\sigma}_{n+1}, \boldsymbol{\alpha}_{n+1}, \Delta\gamma)$ 是通过求解一组[非线性](@entry_id:637147)[代数方程](@entry_id:272665)得到的。最常用的方法是**局部[牛顿-拉弗森法](@entry_id:140620) (local [Newton-Raphson](@entry_id:177436) method)**。

#### 局部[牛顿-拉弗森](@entry_id:177436)迭代

为了应用[牛顿法](@entry_id:140116)，我们将[返回映射](@entry_id:754324)[方程组](@entry_id:193238)写成一个残差向量 $\mathbf{r}$ 等于零的形式。例如，对于一个包含应力、一个标量[硬化](@entry_id:177483)变量 $\kappa$ 和塑性乘子 $\Delta\lambda$ 的系统，残差向量可以定义为 [@problem_id:3508048]：
$$
\mathbf{r}(\boldsymbol{\sigma}_{n+1}, \kappa_{n+1}, \Delta\lambda) = 
\begin{bmatrix}
\boldsymbol{\sigma}_{n+1} - \boldsymbol{\sigma}^{\text{tr}} + \mathbb{C} : (\Delta\lambda\,\mathbf{m}(\boldsymbol{\sigma}_{n+1})) \\
f(\boldsymbol{\sigma}_{n+1}, \kappa_{n+1}) \\
\kappa_{n+1} - \kappa_n - \Delta\lambda
\end{bmatrix} = \mathbf{0}
$$
其中，为了简化，我们假设[硬化](@entry_id:177483)率是1，并且流动向量 $\mathbf{m}$ 可能依赖于应力。牛顿法的核心是在每次迭代 $k$ 中，通过求解一个[线性系统](@entry_id:147850)来更新未知量：
$$
\mathbf{J}^{(k)} \delta\mathbf{y} = -\mathbf{r}^{(k)}
$$
其中 $\delta\mathbf{y}$ 是未知量的修正量，$\mathbf{r}^{(k)}$ 是当前迭代的残差，而 $\mathbf{J}^{(k)}$ 是残差向量 $\mathbf{r}$ 关于未知量 $\mathbf{y} = [\boldsymbol{\sigma}_{n+1}, \kappa_{n+1}, \Delta\lambda]^T$ 的**[雅可比矩阵](@entry_id:264467) (Jacobian matrix)**。该雅可比矩阵的精确形式对于保证[牛顿法](@entry_id:140116)的二次收敛速率至关重要。对于上述残差，雅可比矩阵具有如下结构：
$$
\mathbf{J}^{(k)} =
\begin{bmatrix}
\mathbf{I} + \mathbb{C} : (\Delta\lambda^{(k)} \,\frac{\partial \mathbf{m}}{\partial \boldsymbol{\sigma}})  \mathbf{0}  \mathbb{C} : \mathbf{m} \\
\frac{\partial f}{\partial \boldsymbol{\sigma}}  \frac{\partial f}{\partial \kappa}  0 \\
\mathbf{0}  1  -1
\end{bmatrix}^{(k)}
$$
注意到 $(1,1)$ 区块中的 $\frac{\partial \mathbf{m}}{\partial \boldsymbol{\sigma}}$ 项，它来自于流动方向对应力状态的依赖性。在迭代求解中包含这个项，是实现**[一致线性化](@entry_id:747732) (consistent linearization)** 的关键。

#### 算法的稳健性

在实际应用中，数值算法的稳健性至关重要。
首先，判断一个增量步是弹性还是塑性的理论界限 $f^{\text{tr}} \le 0$ 在有限精度计算中过于苛刻。由于[数值积分](@entry_id:136578)的[截断误差](@entry_id:140949)和浮点运算的[舍入误差](@entry_id:162651)，即使在真实解是弹性的情况下，计算出的 $f^{\text{tr}}$ 也可能略大于零，从而错误地触发代价高昂的塑性计算。一个更稳健的准则是引入一个数值容差 $\eta$ [@problem_id:3532224]：
$$
f^{\text{tr}} \le \eta
$$
这个容差 $\eta$ 应该反映误差的来源。它通常由两部分组成：一部分是与机器精度 $\varepsilon_{\text{mach}}$ 和参考应力 $\sigma_{\text{ref}}$ 成正比的常数项，用于处理舍入误差；另一部分是与应变增量大小（例如 $||\mathbb{C}:\Delta\boldsymbol{\varepsilon}||$）成正比的项，用于处理[后向欧拉法](@entry_id:139674)带来的一阶截断误差。因此，一个合理的容差形式为：
$$
\eta = c_1 \varepsilon_{\text{mach}} \sigma_{\text{ref}} + c_2 ||\mathbb{C}:\Delta\boldsymbol{\varepsilon}||
$$

其次，对于非常大的应变增量，即使是[牛顿法](@entry_id:140116)也可能难以收敛。这通常是因为初始猜测（弹性试探解）距离真实解太远。一个有效的策略是**自动子步法 (automatic substepping)**。当局部牛顿迭代不收敛或收敛缓慢时，该算法会拒绝当前增量步，将其分割成两个或多个更小的子步，然后依次求解。这种策略的有效性可以通过**[压缩映射原理](@entry_id:153489) (contraction mapping principle)** 来解释 [@problem_id:3532238]。通过减小应变增量，可以证明局部迭代映射的[压缩因子](@entry_id:145979) $\rho$ 会减小，当 $\rho  1$ 时，迭代收敛得到保证。如果初始估计的 $\rho$ 值过高，通过子步减小应变增量，可以有效地将 $\rho$ 降低到安全范围内，从而确保算法的稳健收敛。

### [一致算法切线模量](@entry_id:747730)

在[非线性有限元分析](@entry_id:167596)中，[全局平衡方程](@entry_id:272290)通常也是通过[牛顿-拉弗森法](@entry_id:140620)求解的。该全局迭代的收敛性能在很大程度上取决于是否使用了正确的[切线刚度矩阵](@entry_id:170852)。刚度矩阵的材料贡献部分被称为**[一致算法切线模量](@entry_id:747730) (consistent algorithmic tangent modulus)**，定义为本构更新后应力对应变增量的精确导数：
$$
\mathbb{C}_{\mathrm{ep}}^{\text{alg}} = \frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}}
$$
这个模量之所以被称为“算法的”，是因为它的值取决于所使用的特定[数值积分](@entry_id:136578)算法（例如后向欧拉法）。使用与应力[积分算法](@entry_id:192581)相一致的[切线](@entry_id:268870)模量，对于保持全局[牛顿法](@entry_id:140116)的二次收敛速率至关重要。若使用简化的模量（如弹性模量），[全局收敛](@entry_id:635436)速度将退化为线性甚至更差 [@problem_id:3532237]。

为了建立对不同模量的直观理解，我们考虑一个[单轴拉伸](@entry_id:188287)下的线性硬化[弹塑性](@entry_id:193198)材料 [@problem_id:2694657]。在这种情况下，可以推导出三个关键的标量模量：
1.  **弹性模量 (Young's Modulus)** $E$：材料在弹性范围内的初始刚度。
2.  **[割线模量](@entry_id:199454) (Secant Modulus)** $E^{\text{sec}} = \sigma_{n+1}/\varepsilon_{n+1}$：从原点到当前应力-应变点的直线斜率。
3.  **[一致算法切线模量](@entry_id:747730) (Algorithmic Tangent Modulus)** $E^{\text{alg}} = \frac{d \sigma_{n+1}}{d \varepsilon_{n+1}}$：在塑性加载下，该模量为 $\frac{EH}{E+H}$，其中 $H$ 是塑性[硬化](@entry_id:177483)模量。它代表了[应力-应变曲线](@entry_id:159459)在当前点的真实斜率。

对于一个标准的应变硬化材料（$H0$），这些模量的大小关系为：
$$
E^{\text{alg}}  E^{\text{sec}}  E
$$
这个关系清晰地表明，在塑性变形过程中，材料的瞬时刚度 ($E^{\text{alg}}$) 小于其平均刚度 ($E^{\text{sec}}$)，而两者都小于其初始弹性刚度 ($E$)。

### 岩[土力学](@entry_id:180264)中的高级考虑因素

虽然上述原理构成了隐式积分的核心，但岩土材料的复杂行为要求我们考虑一些更高级的机制。

#### [非关联塑性](@entry_id:186531)

许多岩土材料，如土壤和岩石，表现出**[非关联塑性](@entry_id:186531) (non-associated plasticity)**，这意味着塑性流动的方向不是由[屈服函数](@entry_id:167970) $f$ 的梯度决定的，而是由一个独立的**塑性[势函数](@entry_id:176105) (plastic potential function)** $g$ 的梯度决定的，即 $\mathbf{m} = \partial g/\partial \boldsymbol{\sigma}$。一个典型的例子是，剪胀（塑性剪切引起的体积膨胀）是由[剪胀角](@entry_id:748435) $\psi$ 控制的，而[剪切强度](@entry_id:754762)是由[内摩擦角](@entry_id:197521) $\varphi$ 控制的，通常 $\psi  \varphi$。

在非关联模型中 ($g \neq f$)，[返回映射](@entry_id:754324)的方向由塑性势 $g$ 决定，而塑性[一致性条件](@entry_id:637057)（即最终应力必须位于[屈服面](@entry_id:175331)上）仍然由[屈服函数](@entry_id:167970) $f$ 决定 [@problem_id:3532190]。这导致[返回映射](@entry_id:754324)方程变为：
$$
\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\mathrm{tr}}_{n+1} - \Delta\gamma \, \mathbb{C} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \Biggr|_{n+1}
$$
同时要求 $f(\boldsymbol{\sigma}_{n+1}, \boldsymbol{\alpha}_{n+1}) = 0$。

这种非关联性对[一致切线模量](@entry_id:168075)有重要影响。推导出的[切线](@entry_id:268870)模量变为：
$$
\mathbb{C}_{\mathrm{ep}} = \mathbb{C} - \frac{(\mathbb{C}:\frac{\partial g}{\partial \boldsymbol{\sigma}}) \otimes (\frac{\partial f}{\partial \boldsymbol{\sigma}}:\mathbb{C})}{H_{p} + \frac{\partial f}{\partial \boldsymbol{\sigma}}:\mathbb{C}:\frac{\partial g}{\partial \boldsymbol{\sigma}}}
$$
由于 $f \neq g$，[张量积](@entry_id:140694)项 $(\mathbb{C}:\frac{\partial g}{\partial \boldsymbol{\sigma}}) \otimes (\frac{\partial f}{\partial \boldsymbol{\sigma}}:\mathbb{C})$ 通常不具备主对称性。因此，**[非关联塑性](@entry_id:186531)导致了一个非对称的[一致切线模量](@entry_id:168075)**。这要求全局有限元求解器能够处理非对称刚度矩阵。

#### 非光滑[屈服面](@entry_id:175331)

许多经典的岩土模型，如**摩尔-库仑 (Mohr-Coulomb)** 和 **德鲁克-普拉格 (Drucker-Prager)** 模型，其屈服面在应力空间中存在角点或棱线。例如，在[主应力空间](@entry_id:184388)中，摩尔-库仑[屈服面](@entry_id:175331)是一个六棱锥，在偏平面（$\pi$-plane）上表现为六边形。在这些**非光滑 (non-smooth)** 的区域，屈服面的法向是不唯一确定的。

标准的[返回映射算法](@entry_id:168456)假设[屈服面](@entry_id:175331)是光滑的，因此在角点处会失效。处理非光滑[屈服面](@entry_id:175331)需要更复杂的算法，通常基于前面提到的[最近点投影](@entry_id:168047)的[变分原理](@entry_id:198028) [@problem_id:3532160]。当试探应力落在某个区域，其[最近点投影](@entry_id:168047)可能是一个角点或棱线时，算法必须能够确定正确的**[活动约束](@entry_id:636830)集 (active set)**。例如，在摩尔-库仑的偏平面上，返回点可能位于一个面上（一个[活动约束](@entry_id:636830)），也可能位于一个角点上（两个[活动约束](@entry_id:636830)）。算法必须通过系统性的检查来识别正确的情况，并求解相应的KKT ([Karush-Kuhn-Tucker](@entry_id:634966)) 条件，以确保找到唯一的、正确的塑性修正。

#### 大变形与[客观应力率](@entry_id:199282)

当处理[大应变](@entry_id:751152)或大转动问题时，材料的变形和[刚体转动](@entry_id:191086)交织在一起。**[物质客观性原理](@entry_id:191727) (principle of material objectivity)** 或称**标架无关性 (frame indifference)** 要求[本构方程](@entry_id:138559)必须独立于观察者的刚体运动。

简单的应力时间导数，即**物质导数 (material derivative)** $\dot{\boldsymbol{\sigma}}$，并不能满足这一要求。这是因为它会受到材料[刚体转动](@entry_id:191086)的影响。在一个纯[刚体转动](@entry_id:191086)中，材料没有变形（$\boldsymbol{D}=\mathbf{0}$），因此不应产生应力，但 $\dot{\boldsymbol{\sigma}}$ 却不为零。

为了解决这个问题，必须使用**[客观应力率](@entry_id:199282) (objective stress rate)**，它能够从总的应力变化中移除由[自旋张量](@entry_id:187346) $\boldsymbol{W}$（速度梯度的反对称部分）引起的转动效应。一个常用的[客观率](@entry_id:198692)是**Jaumann率 (Jaumann rate)** 或**协同转动率 (co-rotational rate)** [@problem_id:3532162]：
$$
\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$
使用这样的[客观率](@entry_id:198692)（$\overset{\triangle}{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$）可以确保本构模型只响应变形（由变形率张量 $\boldsymbol{D}$ 度量），而对纯[刚体转动](@entry_id:191086)不敏感。将隐式积分格式推广到大变形问题，是岩土工程中许多重要应用（如滑坡和贯入问题）的关键步骤。