## 引言
在计算固体力学领域，J₂塑性理论是描述金属等延性材料在载荷下发生永久变形行为的基石。然而，要将这一理论精确地应用于有限元分析等现代工程仿真中，面临着一个核心挑战：如何开发一个既准确又高效的数值算法来追踪材料从弹性到塑性的复杂演化过程？这个知识缺口催生了计算塑性力学中最为重要和广泛应用的算法之一——径向返回映射算法。

本文旨在为读者提供一份关于J₂塑性径向返回映射算法的全面指南。通过学习本文，您将不仅掌握其理论精髓，还能理解其在实际工程和前沿科研中的强大应用能力。
*   在第一章 **“原理与机制”** 中，我们将从J₂塑性理论的基本构成——应力分解、屈服准则与流动法则——出发，系统推导“弹性预测-塑性修正”这一核心算法框架，并揭示其背后优美的几何诠释。
*   随后的 **“应用与交叉学科联系”** 章节将视野拓展到实践层面，探讨该算法如何嵌入有限元程序，如何特化以适应平面应力等工程问题，以及如何扩展以模拟运动硬化、热-力耦合和有限变形等更复杂的物理现象。
*   最后，在 **“动手实践”** 部分，我们通过一系列精心设计的练习，帮助您将理论知识转化为解决实际问题的能力，巩固对算法关键细节的理解。

## 原理与机制

在计算塑性力学中，率无关 $J_2$ 塑性模型是描述金属等延性材料行为的基石。为了在有限元分析等数值模拟中准确地实现这一模型，必须采用一种鲁棒且高效的应力更新算法。**径向返回映射算法** (radial return mapping algorithm) 正是为此目的而设计的标准方法。本章将深入探讨该算法的基本原理和内在机制，从其赖以建立的物理和数学基础，到其算法步骤的推导，再到其优雅的几何诠释。

### J₂ 塑性理论的基石：应力与应变的分解

金属材料的一个显著特征是其塑性变形行为在很大程度上与静水压力无关。例如，对一块金属施加巨大的均匀压力，其体积会发生微小变化，但这并不会使其进入塑性状态。真正导致材料屈服并产生永久变形的是**剪切应力**。为了在数学上描述这一物理现象，我们将应力张量 $\boldsymbol{\sigma}$ 分解为其**球量** (volumetric) 部分和**偏量** (deviatoric) 部分。

球量部分由平均应力或静水压力 $p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$ 乘以单位张量 $\boldsymbol{I}$ 构成，即 $p\boldsymbol{I}$。它描述了引起体积变化的应力分量。偏量部分，即**偏应力张量** (deviatoric stress tensor) $\boldsymbol{s}$，定义为总应力减去其球量部分：

$$
\boldsymbol{s} = \boldsymbol{\sigma} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})\boldsymbol{I}
$$

偏应力张量是一个迹为零的张量（$\mathrm{tr}(\boldsymbol{s}) = 0$），它代表了应力状态中引起形状改变（剪切变形）的部分。

$J_2$ 塑性理论的核心在于，其屈服条件仅依赖于偏应力张量的大小。这个大小通过**偏应力第二不变量** ($J_2$) 来度量，其定义为：

$$
J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s} = \frac{1}{2}s_{ij}s_{ij}
$$

其中 $:$ 表示张量的双点积。$J_2$ 的一个关键性质是其对静水压力的不敏感性。考虑一个应力状态 $\boldsymbol{\sigma}$，如果我们给它叠加一个任意大小的静水压力 $p_0\boldsymbol{I}$，得到新的应力状态 $\boldsymbol{\sigma}' = \boldsymbol{\sigma} + p_0\boldsymbol{I}$，其偏应力部分 $s'$ 保持不变 [@problem_id:3592711]：

$$
\boldsymbol{s}' = \boldsymbol{\sigma}' - \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma}')\boldsymbol{I} = (\boldsymbol{\sigma} + p_0\boldsymbol{I}) - \frac{1}{3}(\mathrm{tr}(\boldsymbol{\sigma}) + 3p_0)\boldsymbol{I} = \boldsymbol{\sigma} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})\boldsymbol{I} = \boldsymbol{s}
$$

由于偏应力部分不变，$J_2$ 的值也保持不变。这意味着，仅通过施加或改变静水压力，无法使材料屈服。同样地，在数值算法的框架内，一个纯体积应变增量只会产生一个纯静水压应力增量，而不会改变 $J_2$ 的值，因此也不会触发塑性流动。

### 本构模型：屈服、硬化与流动

为了完整描述材料行为，我们需要定义屈服准则、硬化规律和流动法则。

#### 屈服面与等效应力

von Mises 屈服准则假定，当 $J_2$ 的某个函数达到临界值时，材料开始屈服。为了将复杂的多轴应力状态与简单的单轴拉伸试验结果联系起来，我们定义了**等效应力** (equivalent stress)，通常记为 $\sigma_{eq}$ 或 $q$。对于 von Mises 模型，其标准定义为 [@problem_id:3592684]：

$$
\sigma_{eq} = \sqrt{3J_2} = \sqrt{\frac{3}{2}\boldsymbol{s}:\boldsymbol{s}}
$$

这个定义的巧妙之处在于，对于单轴拉伸状态（$\sigma_{11} = \sigma_{uni}$，其他分量为零），计算得到的等效应力恰好等于拉伸应力 $\sigma_{uni}$。这样，屈服就可以通过一个简单的函数来描述：

$$
f(\boldsymbol{\sigma}, \alpha) = \sigma_{eq} - \sigma_y(\alpha) \le 0
$$

其中 $\sigma_y$ 是材料当前的单轴拉伸屈服强度，它可能随一个或多个**内禀变量** (internal variables) $\alpha$ 的演化而改变。当 $f=0$ 时，应力状态位于**屈服面** (yield surface) 上；当 $f  0$ 时，应力状态处于弹性域内。

#### 各向同性硬化

许多材料在经历塑性变形后，其屈服强度会提高，这种现象称为**硬化** (hardening)。在**各向同性硬化** (isotropic hardening) 模型中，我们假设屈服面在应力空间中均匀扩张，而不改变其形状或中心位置。这通常通过让屈服强度 $\sigma_y$ 成为**累积等效塑性应变** $\alpha$ (或记为 $\bar{\varepsilon}^p$) 的函数来实现。

最简单的硬化模型包括：
- **理想塑性** (Perfect Plasticity)：屈服强度为常数，$\sigma_y = \sigma_{y0}$，硬化模量 $H=0$ [@problem_id:3592713]。
- **线性各向同性硬化** (Linear Isotropic Hardening)：屈服强度随累积塑性应变线性增长，$\sigma_y(\alpha) = \sigma_{y0} + H\alpha$，其中 $H$ 为常数硬化模量 [@problem_id:3592662] [@problem_id:3592693]。
- **非线性各向同性硬化** (Nonlinear Isotropic Hardening)：更真实地描述材料行为，例如常用的 Voce 硬化定律 [@problem_id:3592654]：
  $$
  \sigma_y(\alpha) = \sigma_{y\infty} - (\sigma_{y\infty} - \sigma_{y0})\exp(-b\alpha)
  $$
  其中 $\sigma_{y\infty}$ 是饱和屈服应力， $b$ 是描述饱和速率的材料参数。

#### 关联流动法则

**流动法则** (flow rule) 规定了塑性应变增量 $\mathrm{d}\boldsymbol{\varepsilon}^p$ 的方向。对于金属，广泛采用**关联流动法则** (associative flow rule)，它假定塑性流动方向与屈服面在当前应力点的外法线方向一致。数学上，这意味着塑性应变增量正比于屈服函数对应力的梯度：

$$
\mathrm{d}\boldsymbol{\varepsilon}^p = \mathrm{d}\gamma \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$

其中 $\mathrm{d}\gamma \ge 0$ 是一个非负标量，称为**塑性乘子** (plastic multiplier)。对于上述 von Mises 屈服函数，其对应力的梯度为：

$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{\partial \sigma_{eq}}{\partial \boldsymbol{\sigma}} = \frac{3}{2} \frac{\boldsymbol{s}}{\sigma_{eq}}
$$

由于该梯度是一个纯偏量张量（迹为零），关联流动法则导出一个至关重要的结论：**$J_2$ 塑性流动是体积不可压缩的**，即 $\mathrm{tr}(\mathrm{d}\boldsymbol{\varepsilon}^p) = 0$ [@problem_id:3592711]。这意味着材料的体积变化完全由弹性部分承担，由体积模量 $K$ 和静水压力控制。

### 核心算法：弹性预测-塑性修正

径向返回映射算法是一个两步过程：首先进行弹性预测，然后根据需要进行塑性修正。

#### 步骤一：弹性预测

在一个时间步（或增量步）开始时，我们拥有上一步结束时的所有状态变量（如应力 $\boldsymbol{\sigma}_n$、塑性应变 $\boldsymbol{\varepsilon}^p_n$）。给定当前步的总应变增量 $\Delta\boldsymbol{\varepsilon}$，我们首先**假设**整个增量步完全是弹性的。基于这个假设，我们计算出一个**试探应力** (trial stress) $\boldsymbol{\sigma}^{\mathrm{tr}}$：

$$
\boldsymbol{\sigma}^{\mathrm{tr}} = \boldsymbol{\sigma}_n + \mathbb{C} : \Delta\boldsymbol{\varepsilon}
$$

其中 $\mathbb{C}$ 是四阶弹性刚度张量。对于各向同性线弹性材料，$\mathbb{C} = K \boldsymbol{I} \otimes \boldsymbol{I} + 2G \boldsymbol{I}^{\mathrm{dev}}$，其中 $K$ 是体积模量，$G$ 是剪切模量。利用这一形式，试探应力可以更直观地分解为 [@problem_id:3592689]：

$$
\boldsymbol{\sigma}^{\mathrm{tr}} = \boldsymbol{\sigma}_n + 2G \Delta\boldsymbol{\varepsilon} + \left(K - \frac{2G}{3}\right)\mathrm{tr}(\Delta\boldsymbol{\varepsilon})\boldsymbol{I}
$$

由于塑性流动只与偏应力相关，我们更关心**试探偏应力** $\boldsymbol{s}^{\mathrm{tr}}$。可以证明，它的更新只依赖于初始偏应力 $\boldsymbol{s}_n$ 和应变增量的偏量部分 $\mathrm{dev}(\Delta\boldsymbol{\varepsilon})$：

$$
\boldsymbol{s}^{\mathrm{tr}} = \mathrm{dev}(\boldsymbol{\sigma}_n) + 2G\,\mathrm{dev}(\Delta\boldsymbol{\varepsilon})
$$

这清晰地表明，在弹性预测阶段，体积变形和剪切变形是解耦的。

#### 步骤二：屈服检查

接下来，我们需要检查试探应力状态是否违反了屈服条件。我们使用试探应力计算试探等效应力 $\sigma_{eq}^{\mathrm{tr}} = \sqrt{\frac{3}{2}\boldsymbol{s}^{\mathrm{tr}}:\boldsymbol{s}^{\mathrm{tr}}}$，并将其与上一步结束时的屈服强度 $\sigma_y(\alpha_n)$ 进行比较，定义试探屈服函数 $f_{\mathrm{tr}}$：

$$
f_{\mathrm{tr}} = \sigma_{eq}^{\mathrm{tr}} - \sigma_y(\alpha_n)
$$

- 如果 $f_{\mathrm{tr}} \le 0$，说明试探应力位于弹性域或恰好在屈服面上。弹性假设成立，无需塑性修正。我们接受试探状态为最终状态：$\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\mathrm{tr}}$，并且没有塑性应变增量，$\Delta\gamma = 0$。这个过程也被称为**中性加载** [@problem_id:3592713]。

- 如果 $f_{\mathrm{tr}} > 0$，说明试探应力超出了屈服面，这在物理上是不允许的。弹性假设不成立，材料在本步内发生了塑性变形。此时，必须启动塑性修正步骤 [@problem_id:3592657]。

例如，考虑一个初始屈服应力为 $250 \text{ MPa}$、硬化模量为 $1000 \text{ MPa}$ 的材料，其在加载前已累积了 $0.02$ 的等效塑性应变。那么它当前的屈服强度为 $\sigma_y(\alpha_n) = 250 + 1000 \times 0.02 = 270 \text{ MPa}$。若一个应变增量导致的试探等效应力为 $283 \text{ MPa}$，则 $f_{\mathrm{tr}} = 283 - 270 = 13 \text{ MPa} > 0$，表明需要进行塑性修正 [@problem_id:3592657]。

#### 步骤三：塑性修正（径向返回）

当需要塑性修正时，我们的目标是找到最终的应力状态 $\boldsymbol{\sigma}_{n+1}$，使其满足屈服条件 $f(\boldsymbol{\sigma}_{n+1}, \alpha_{n+1}) = 0$，这个条件被称为**一致性条件** (consistency condition)。

最终应力 $\boldsymbol{\sigma}_{n+1}$ 与试探应力 $\boldsymbol{\sigma}^{\mathrm{tr}}$ 的关系为：

$$
\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\mathrm{tr}} - \mathbb{C} : \Delta\boldsymbol{\varepsilon}^p
$$

由于塑性应变是不可压缩的 ($\mathrm{tr}(\Delta\boldsymbol{\varepsilon}^p)=0$)，对于各向同性弹性，$\mathbb{C}:\Delta\boldsymbol{\varepsilon}^p = 2G\Delta\boldsymbol{\varepsilon}^p$。因此，应力修正只影响偏应力部分，静水压力保持不变 [@problem_id:3592711]：

$$
\mathrm{tr}(\boldsymbol{\sigma}_{n+1}) = \mathrm{tr}(\boldsymbol{\sigma}^{\mathrm{tr}})
$$
$$
\boldsymbol{s}_{n+1} = \boldsymbol{s}^{\mathrm{tr}} - 2G\Delta\boldsymbol{\varepsilon}^p
$$

这是算法的核心。现在，我们结合关联流动法则（采用**后向欧拉**格式，即在时间步末端评估流动方向）：

$$
\Delta\boldsymbol{\varepsilon}^p = \Delta\gamma \frac{\partial f}{\partial \boldsymbol{\sigma}}\bigg|_{n+1} = \Delta\gamma \frac{3}{2} \frac{\boldsymbol{s}_{n+1}}{\sigma_{eq,n+1}}
$$

将流动法则代入偏应力修正方程：

$$
\boldsymbol{s}_{n+1} = \boldsymbol{s}^{\mathrm{tr}} - 2G \left( \Delta\gamma \frac{3}{2} \frac{\boldsymbol{s}_{n+1}}{\sigma_{eq,n+1}} \right) = \boldsymbol{s}^{\mathrm{tr}} - 3G\Delta\gamma \frac{\boldsymbol{s}_{n+1}}{\sigma_{eq,n+1}}
$$

整理上式可得：

$$
\boldsymbol{s}_{n+1} \left( 1 + \frac{3G\Delta\gamma}{\sigma_{eq,n+1}} \right) = \boldsymbol{s}^{\mathrm{tr}}
$$

这个方程揭示了径向返回的本质：最终偏应力 $\boldsymbol{s}_{n+1}$ 与试探偏应力 $\boldsymbol{s}^{\mathrm{tr}}$ 的方向完全相同，只是大小被一个标量因子缩放了 [@problem_id:3592655]。在以原点为中心的偏应力空间中，这个修正过程就是将 $\boldsymbol{s}^{\mathrm{tr}}$ 沿其径向方向“拉回”到屈服面上。

为了求解未知的塑性乘子 $\Delta\gamma$，我们对上式两边取等效应力范数，得到一个标量关系：

$$
\sigma_{eq,n+1} \left( 1 + \frac{3G\Delta\gamma}{\sigma_{eq,n+1}} \right) = \sigma_{eq}^{\mathrm{tr}} \quad \implies \quad \sigma_{eq,n+1} = \sigma_{eq}^{\mathrm{tr}} - 3G\Delta\gamma
$$

结合一致性条件 $\sigma_{eq,n+1} = \sigma_y(\alpha_{n+1})$ 和硬化定律，我们就可以求解 $\Delta\gamma$。对于**线性硬化** $\sigma_y(\alpha_{n+1}) = \sigma_y(\alpha_n) + H\Delta\gamma$（注意：对于关联 $J_2$ 塑性，累积塑性应变增量 $\Delta\alpha$ 等于塑性乘子 $\Delta\gamma$），我们有：

$$
\sigma_y(\alpha_n) + H\Delta\gamma = \sigma_{eq}^{\mathrm{tr}} - 3G\Delta\gamma
$$

从而得到 $\Delta\gamma$ 的解析解：

$$
\Delta\gamma = \frac{\sigma_{eq}^{\mathrm{tr}} - \sigma_y(\alpha_n)}{3G + H} = \frac{f_{\mathrm{tr}}}{3G + H}
$$

例如，在一个初始偏应力为零、初始屈服强度为 $430 \text{ MPa}$ 的线性硬化材料（$H=1500 \text{ MPa}$）中，若一个纯偏应变增量导致试探等效应力为 $\frac{1260}{1.3} \approx 969.23 \text{ MPa}$，则塑性乘子增量为 $\Delta\gamma = \frac{969.23 - 430}{3G + 1500}$，计算可得 $\Delta\gamma \approx 0.0022117$ [@problem_id:3592662]。

对于**非线性硬化**，例如 Voce 定律，$\sigma_y(\alpha_{n+1})$ 是 $\Delta\gamma$ 的非线性函数。此时，一致性条件会变成一个关于 $\Delta\gamma$ 的标量非线性方程，需要使用牛顿-拉夫逊法等数值方法求解 [@problem_id:3592654]。

一旦求得 $\Delta\gamma$，最终的偏应力就可以通过径向缩放得到：

$$
\boldsymbol{s}_{n+1} = \frac{\sigma_{eq,n+1}}{\sigma_{eq}^{\mathrm{tr}}} \boldsymbol{s}^{\mathrm{tr}} = \frac{\sigma_y(\alpha_{n+1})}{\sigma_{eq}^{\mathrm{tr}}} \boldsymbol{s}^{\mathrm{tr}}
$$

### 几何诠释：能量范数下的最近点投影

径向返回算法不仅在代数上简洁，在几何上也具有深刻的含义。整个应力更新过程可以被诠释为一个在特定范数下的**最近点投影** (closest-point projection) 问题 [@problem_id:3592659]。

从变分原理的角度看，材料的真实应力状态 $\boldsymbol{\sigma}_{n+1}$ 是在所有满足屈服条件的应力状态中，与试探应力 $\boldsymbol{\sigma}^{\mathrm{tr}}$ 的“距离”最小的那一个。这里的“距离”并非普通的欧几里得距离，而是由弹性关系定义的**能量范数**。这个范数由弹性柔度张量 $\mathbb{C}^{-1}$ 导出。

由于 $J_2$ 塑性的塑性流动是体积不可压缩的，整个修正过程在偏应力空间和静水压力空间中是解耦的。静水压力部分保持不变，因此我们只需关注偏应力空间。在偏应力空间中，相关的能量范数由剪切柔度 $(2G)^{-1}$ 定义。因此，寻找 $\boldsymbol{s}_{n+1}$ 的问题等价于求解以下约束最小化问题：

$$
\text{minimize} \quad \frac{1}{2} (\boldsymbol{s}^{\mathrm{tr}} - \boldsymbol{s}) : (2G)^{-1}(\boldsymbol{s}^{\mathrm{tr}} - \boldsymbol{s}) \quad \text{subject to} \quad \sqrt{\frac{3}{2}\boldsymbol{s}:\boldsymbol{s}} - \sigma_y(\alpha_{n+1}) \le 0
$$

von Mises 屈服面（$\sigma_{eq} = \text{const.}$）在偏应力空间中是一个以原点为中心的超球面。而最小化问题中的目标函数所定义的距离，其等值线也是以 $\boldsymbol{s}^{\mathrm{tr}}$ 为中心的同心超球面。求解这个问题的几何直观是：从点 $\boldsymbol{s}^{\mathrm{tr}}$ 向屈服面这个球体作垂线，垂足就是解 $\boldsymbol{s}_{n+1}$。由于屈服面和距离等值线都是球面，这条垂线必然通过屈服面的球心，即原点。因此，$\boldsymbol{s}_{n+1}$ 必然位于连接原点和 $\boldsymbol{s}^{\mathrm{tr}}$ 的射线上，这正是“径向”返回的几何本质。

这个“毕达哥拉斯”视角还提供了一个优雅的正交性条件：从试探点到投影点的向量（即应力修正量 $\boldsymbol{s}^{\mathrm{tr}} - \boldsymbol{s}_{n+1}$）必须与屈服面在投影点处的切空间正交。这里的正交性同样是在能量内积 $\langle \boldsymbol{a}, \boldsymbol{b} \rangle = (2G)^{-1}\boldsymbol{a}:\boldsymbol{b}$ 的意义下定义的 [@problem_id:3592659]。这一观点不仅为算法提供了坚实的理论基础，也为推广到更复杂的塑性模型提供了指导。