## 引言
在[连续介质力学](@entry_id:155125)中，描述材料从弹性到塑性状态的转变是理解其力学响应的核心。一旦[材料屈服](@entry_id:751736)，其变形变得不可逆，并开始“流动”。一个关键的科学问题是：[塑性流动](@entry_id:201346)将沿哪个方向发生？**流动法则 (Flow Rule)** 正是回答这一问题的本构关系，它规定了塑性应变增量的方向，是现代塑性力学理论的基石。

然而，[流动法则](@entry_id:177163)的构建并非只有一种方式。理论家和工程师面临一个根本性的选择：是采用在数学上优雅且与[材料稳定性](@entry_id:183933)公设紧密相连的**关联[流动法则](@entry_id:177163) (associated flow rule)**，还是选择更具灵活性、能够捕捉复杂物理现象（如剪胀）的**[非关联流动法则](@entry_id:752544) (non-associated flow rule)**？这一选择构成了[本构建模](@entry_id:183370)中的一个核心知识鸿沟，它不仅影响模型预测的准确性，还深刻关系到数值模拟的稳定性与效率。

本文旨在系统性地阐明这两种流动法则的原理、应用与计算实现。在“**原理与机制**”一章中，我们将建立[塑性流动](@entry_id:201346)的完整框架，从[屈服函数](@entry_id:167970)、塑性势到加载-卸载条件，详细区分关联与[非关联流动](@entry_id:199220)的定义、[热力学](@entry_id:141121)基础和理论推论。接下来，在“**应用与跨学科联系**”一章中，我们将通过对金属、岩土材料、[聚合物力学](@entry_id:198930)乃至[晶体塑性](@entry_id:141273)等领域的案例分析，展示这两种法则在工程与科学实践中的具体应用和必要性。最后，“**动手实践**”部分将提供一系列计算练习，引导读者从解析推导到编写[返回映射算法](@entry_id:168456)，将理论知识转化为解决实际问题的能力。

## 原理与机制

在塑性力学中，材料一旦进入塑性状态，其应变将不可逆地增长。为了描述这一过程，我们需要一个本构框架来规定塑性应变的演化。本章旨在系统地阐述控制[塑性流动](@entry_id:201346)方向和大小的基本原理和机制，重点区分**关联[流动法则](@entry_id:177163) (associated flow rule)** 和 **[非关联流动法则](@entry_id:752544) (non-associated flow rule)**，并探讨其[热力学](@entry_id:141121)基础、物理动机和计算后果。

### 塑性流动的基本框架

描述[速率无关塑性](@entry_id:754082)理论需要三个核心要素：一个定义弹性变形极限的**屈服准则 (yield criterion)**，一个确定塑性应变增量方向的**[流动法则](@entry_id:177163) (flow rule)**，以及一个描述[材料强度](@entry_id:158701)随塑性变形而变化的**硬化法则 (hardening law)**。

#### [屈服函数](@entry_id:167970)与弹性域

材料的弹性行为范围由一个在应力空间中定义的**弹性域 (elastic domain)** $\mathcal{E}$ 来界定。这个域的边界被称为**屈服面 (yield surface)**。我们通过一个标量**[屈服函数](@entry_id:167970) (yield function)** $f(\boldsymbol{\sigma}, \boldsymbol{\alpha})$ 来数学地描述这个区域，其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\boldsymbol{\alpha}$ 是一组描述材料内部状态的**内变量 (internal variables)**，它们控制着硬化行为。

根据约定，弹性域由不等式 $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0$ 定义。
*   当 $f(\boldsymbol{\sigma}, \boldsymbol{\alpha})  0$ 时，应力状态位于[屈服面](@entry_id:175331)内部，材料行为是纯弹性的。
*   当 $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0$ 时，应力状态位于屈服面上，可能发生[塑性流动](@entry_id:201346)。
*   $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) > 0$ 的应力状态在标准塑性理论中是不允许的。

内变量 $\boldsymbol{\alpha}$ 的演化描述了**硬化 (hardening)** 现象，即[屈服面](@entry_id:175331)随塑性变形而发生变化。例如，如果 $\boldsymbol{\alpha}$ 是一个标量（如等效塑性应变），它的演化可能导致[屈服面](@entry_id:175331)的扩张或收缩，这被称为**[各向同性硬化](@entry_id:164486) (isotropic hardening)**。如果 $\boldsymbol{\alpha}$ 是一个二阶张量（称为**背应力 (backstress)**），它的演化可能导致屈服面在应力空间中平移，这被称为**[运动硬化](@entry_id:172077) (kinematic hardening)** 。

#### 塑性势与[流动法则](@entry_id:177163)

当塑性变形发生时，塑性[应变率张量](@entry_id:266108) $\dot{\boldsymbol{\varepsilon}}^p$ 的方向由一个称为**塑性势 (plastic potential)** 的标量函数 $g(\boldsymbol{\sigma}, \boldsymbol{\alpha})$ 决定。[塑性流动](@entry_id:201346)的基本假设是，塑性应变率的方向**正交 (normal)** 于塑性势函数 $g$ 在应力空间中的[等值面](@entry_id:196027)。这被称为**正交流动法则 (normality rule)**，其数学表达式为：

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$

在这个**流动法则 (flow rule)** 中 ：
*   $\dot{\lambda}$ 是一个非负的标量，称为**塑性乘子 (plastic multiplier)**。它确定了[塑性流动](@entry_id:201346)的**速率或大小 (magnitude)**。当 $\dot{\lambda} > 0$ 时，发生塑性加载；当 $\dot{\lambda} = 0$ 时，材料处于弹性状态或卸载。$\dot{\lambda}$ 的非负性反映了塑性变形的不[可逆性](@entry_id:143146)。
*   梯度 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 是一个[二阶张量](@entry_id:199780)，它在几何上代表了塑性[势函数](@entry_id:176105) $g$ 在当前应力点 $\boldsymbol{\sigma}$ 的[等值面](@entry_id:196027)的法向量。因此，它确定了塑性应变率张量的**方向 (direction)** 。

这个框架将塑性流动分解为大小和方向两部分，为建立具体的[本构模型](@entry_id:174726)提供了极大的灵活性。

### 加载-卸载条件与一致性

为了完整地描述材料何时以及如何发生塑性变形，我们需要一套逻辑条件来控制塑性乘子 $\dot{\lambda}$ 的激活。这些条件在数学上表现为 [Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)，它们构成了[计算塑性力学](@entry_id:171377)中状态更新算法的基础 。

#### [Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)

对于[速率无关塑性](@entry_id:754082)，KKT 条件包括以下三个部分  ：
1.  **应力容许条件 (Primal feasibility)**: $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0$。这表明应力状态必须始终位于弹性域内部或其边界上。

2.  **塑性流动不可逆性 (Dual feasibility)**: $\dot{\lambda} \ge 0$。塑性乘子必须为非负，这体现了塑性变形是一个耗散过程，不能自发逆转。

3.  **互补松弛条件 (Complementary slackness)**: $\dot{\lambda} f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0$。这个核心条件将前两者联系起来，它规定：
    *   如果应力状态严格位于弹性域内部 ($f  0$)，则必须有 $\dot{\lambda} = 0$，即没有塑性流动。
    *   如果发生[塑性流动](@entry_id:201346) ($\dot{\lambda} > 0$)，则应力状态必须位于[屈服面](@entry_id:175331)上 ($f = 0$)。

#### [一致性条件](@entry_id:637057)

在持续的塑性加载过程中，应力点必须停留在不断演化的屈服面上。这意味着在 $\dot{\lambda} > 0$ 时，[屈服函数](@entry_id:167970)的值必须保持为零，因此其时间变化率也必须为零，即 $\dot{f}=0$。这个要求被称为**[一致性条件](@entry_id:637057) (consistency condition)**。

我们可以将一致性条件与[互补条件](@entry_id:747558)结合成一个速率形式的表达式：$\dot{\lambda}\dot{f} = 0$ 。通过对 $f(\boldsymbol{\sigma}(t), \boldsymbol{\alpha}(t))$ 应用链式法则，我们得到：

$$
\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} = 0 \quad (\text{当 } \dot{\lambda} > 0)
$$

这个方程至关重要，因为它提供了一个求解塑性乘子 $\dot{\lambda}$ 的途径。通过代入[弹塑性](@entry_id:193198)[本构关系](@entry_id:186508)（包括弹性定律、[流动法则](@entry_id:177163)和硬化法则），可以将 $\dot{f}$ 表示为总[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$ 和 $\dot{\lambda}$ 的函数，然后从 $\dot{f}=0$ 中解出 $\dot{\lambda}$。

值得强调的是，一致性条件是关于应力状态保持在由 $f$ 定义的[屈服面](@entry_id:175331)上的约束，因此它**始终与[屈服函数](@entry_id:167970) $f$ 相关**，而与塑性势 $g$ 无关，无论[流动法则](@entry_id:177163)是关联还是非关联的  。

这些条件共同定义了材料响应的逻辑：
*   **弹性状态**: $f  0$ 或 $f=0$ 且 $\dot{f}  0$（从[屈服面](@entry_id:175331)卸载）。此时 $\dot{\lambda} = 0$。
*   **塑性加载**: $f=0$ 且 $\dot{f} = 0$。此时 $\dot{\lambda} > 0$。

### 关联与[非关联流动法则](@entry_id:752544)

基于塑性势 $g$ 和[屈服函数](@entry_id:167970) $f$ 之间的关系，我们可以将[流动法则](@entry_id:177163)分为两类。

#### 关联[流动法则](@entry_id:177163)

当塑性势函数与[屈服函数](@entry_id:167970)相同时，即 $g = f$，[流动法则](@entry_id:177163)被称为**关联流动法则 (associated flow rule)**。此时，流动法则写为：

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$

在这种情况下，塑性应变率的方向正交于**[屈服面](@entry_id:175331)本身**。这种选择具有深刻的理论优势，因为它与[材料稳定性](@entry_id:183933)的基本假设（如[Drucker公设](@entry_id:180546)）直接相关，并且可以从[最大塑性耗散](@entry_id:184825)原理中导出 。由于其理论上的简洁性和良好的稳定性，关联流动法则在[金属塑性](@entry_id:176585)等领域得到了广泛应用。

#### [非关联流动法则](@entry_id:752544)

在更一般的情况下，塑性[势函数](@entry_id:176105)可以独立于[屈服函数](@entry_id:167970)，即 $g \ne f$。这被称为**[非关联流动法则](@entry_id:752544) (non-associated flow rule)** 。在这种情况下，[屈服函数](@entry_id:167970) $f$ 仍然定义弹性域的边界和加载条件，而一个独立的塑性势函数 $g$ 定义了[塑性流动](@entry_id:201346)的方向。

虽然[非关联流动法则](@entry_id:752544)在理论上更为复杂，但它为模拟某些材料（如土壤、岩石、混凝土和一些聚合物）的复杂行为提供了必要的灵活性。这些材料的塑性流动方向（特别是体积变化）与[屈服准则](@entry_id:193897)所预测的法线方向有显著差异。

### [热力学约束](@entry_id:755911)与[材料稳定性](@entry_id:183933)

塑性本构模型必须遵守[热力学第二定律](@entry_id:142732)，即在[等温过程](@entry_id:143096)中，材料的内耗散必须是非负的。对于简单的塑性模型（不考虑[硬化](@entry_id:177483)[储能](@entry_id:264866)），这简化为塑性功率耗散 $\mathcal{D}^p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$ 必须大于等于零。

#### 关联流动的稳定性

对于关联流动法则 ($g=f$)，[塑性耗散](@entry_id:201273)为：
$$
\mathcal{D}^p = \boldsymbol{\sigma} : \left(\dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}\right) = \dot{\lambda} \left(\boldsymbol{\sigma} : \frac{\partial f}{\partial \boldsymbol{\sigma}}\right)
$$
如果[屈服面](@entry_id:175331) $f$ 是应力 $\boldsymbol{\sigma}$ 的凸函数，并且包含了零应力状态（即 $f(\boldsymbol{0}, \boldsymbol{\alpha}) \le 0$），那么根据[凸分析](@entry_id:273238)的性质，对于任何位于[屈服面](@entry_id:175331)上的应力点 $\boldsymbol{\sigma}$，必然有 $\boldsymbol{\sigma} : \frac{\partial f}{\partial \boldsymbol{\sigma}} \ge 0$。由于 $\dot{\lambda} \ge 0$，这自动保证了 $\mathcal{D}^p \ge 0$。

因此，**采用关联[流动法则](@entry_id:177163)并选择凸的[屈服函数](@entry_id:167970)是确保材料模型[热力学稳定性](@entry_id:142877)的一个充分条件** 。这一性质被称为**[Drucker稳定性公设](@entry_id:200080) (Drucker's stability postulate)**。

#### [非关联流动](@entry_id:199220)的[热力学](@entry_id:141121)容许性

对于[非关联流动法则](@entry_id:752544)，[塑性耗散](@entry_id:201273)为：
$$
\mathcal{D}^p = \dot{\lambda} \left(\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}}\right)
$$
在这种情况下，即使 $f$ 是凸的，也不能保证 $\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \ge 0$。因此，非关联模型不自动满足热力学稳定性要求。为了确保模型的物理有效性，必须对塑性势 $g$ 施加额外的约束，即对于所有可能发生[塑性流动](@entry_id:201346)的应力状态（即所有在[屈服面](@entry_id:175331)上的点），都必须满足：
$$
\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \ge 0
$$
这个条件确保了即使流动方向与屈服面法向不一致，塑性变形过程仍然是耗能的，而不会产生能量 。例如，在经典的[Mohr-Coulomb模型](@entry_id:752108)中，为了保证稳定性，要求材料的**[剪胀角](@entry_id:748435) (dilation angle)** $\psi$ (与 $g$ 相关) 不能超过其**[内摩擦角](@entry_id:197521) (friction angle)** $\varphi$ (与 $f$ 相关)，即 $\psi \le \varphi$ 。选择一个非凸的塑性势 $g$ 可能会导致在某些应力区域 $\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}}  0$，从而违反[热力学第二定律](@entry_id:142732) 。

### [非关联流动](@entry_id:199220)的物理动机：以[颗粒材料](@entry_id:750005)为例

[非关联流动法则](@entry_id:752544)的必要性在压力敏感材料（如土壤和岩石）中表现得尤为突出。这些材料的强度（摩擦特性）和塑性体积应变（剪胀或剪缩）是两个相对独立的物理现象。

以一个简化的[Drucker-Prager模型](@entry_id:180845)为例，其[屈服函数](@entry_id:167970)和塑性势可以写为 ：
*   **[屈服函数](@entry_id:167970)**: $f(\boldsymbol{\sigma}) = q + \alpha p - k = 0$
*   **塑性势**: $g(\boldsymbol{\sigma}) = q + \beta p$

这里，$p$ 是平均应力（[静水压力](@entry_id:275365)），$q$ 是等效剪应力。参数 $\alpha$ 与材料的[内摩擦角](@entry_id:197521)相关，决定了[屈服强度](@entry_id:162154)对压力的依赖性。参数 $\beta$ 则控制塑性[体积应变率](@entry_id:272471) $\dot{\varepsilon}_v^p = \dot{\lambda} \beta$，因此被称为**剪胀参数 (dilatancy parameter)**。

如果采用关联[流动法则](@entry_id:177163)，则必须有 $\beta = \alpha$。这意味着材料的摩擦强度和剪胀行为被同一个参数锁定。然而，实验表明，对于密砂等[颗粒材料](@entry_id:750005)，其[剪胀角](@entry_id:748435)通常远小于[内摩擦角](@entry_id:197521)。因此，关联法则会严重高估材料在剪切过程中的体积膨胀 。

通过采用[非关联流动法则](@entry_id:752544)，我们可以独立选择 $\beta$ 和 $\alpha$ (通常 $\beta  \alpha$)。这使得模型能够分别校准摩擦和剪胀行为，从而更准确地预测材料响应。特别地，当材料达到**临界状态 (critical state)** 时，它会在恒定体积下持续剪切。这可以通过设置 $\beta = 0$ 来实现，而此时材料仍然可以具有非零的摩擦强度 ($\alpha > 0$) 。对于[塑性流动](@entry_id:201346)保持体积不变的金属材料，其塑性势通常只依赖于偏应力（等效于 $\beta = 0$），这正是 $J_2$ (von Mises) 塑性理论的核心假设之一 。

### 理论与计算的推论

关联与[非关联流动](@entry_id:199220)的选择不仅影响物理描述的准确性，还对模型的数学结构和数值计算方法产生深远影响。

#### 变分原理的存在性

关联[流动法则](@entry_id:177163)的一个优美特性是它确保了[弹塑性](@entry_id:193198)[切线刚度](@entry_id:166213)算子 $\mathbb{C}^{ep} = \frac{\partial \boldsymbol{\sigma}}{\partial \boldsymbol{\varepsilon}}$ 的**对称性**。这种对称性意味着[弹塑性](@entry_id:193198)增量问题可以从一个[标量势](@entry_id:276177)函数的最小化问题中导出，即存在一个**增量[变分原理](@entry_id:198028) (incremental variational principle)** 。这为塑性理论提供了坚实的数学基础，并与[热力学](@entry_id:141121)中的最大耗散原理紧密联系。在数值计算中，这意味着基于能量最小化的有限元方法具有稳固的理论支持。

#### [非关联流动](@entry_id:199220)的计算挑战

相反，[非关联流动法则](@entry_id:752544)导致了**非对称的**[切线刚度](@entry_id:166213)算子 $\mathbb{C}^{ep}$。这对基于[牛顿-拉弗森法](@entry_id:140620) ([Newton-Raphson](@entry_id:177436)) 的[非线性有限元分析](@entry_id:167596)带来了直接的挑战 ：
1.  **[全局刚度矩阵](@entry_id:138630)非对称**: 组装后的全局[切线刚度矩阵](@entry_id:170852) $\mathbf{K}$ 将是非对称的。
2.  **需要非对称求解器**: 这意味着不能使用为[对称矩阵](@entry_id:143130)设计的标准高效[线性求解器](@entry_id:751329)，如共轭梯度法 (Conjugate Gradient)。必须采用为非对称系统设计的求解器，例如[广义最小残差法](@entry_id:139566) (GMRES) 或直接法（如[LU分解](@entry_id:144767)）。
3.  **收敛性**: 尽管矩阵非对称，但如果使用精确的（非对称）[切线刚度矩阵](@entry_id:170852)，[牛顿-拉弗森法](@entry_id:140620)仍然能保持其标志性的**二次收敛速率**。一个常见的错误是人为地将[刚度矩阵](@entry_id:178659)对称化以使用对称求解器，但这会破坏牛顿法的基本假设，通常会导致收敛速率下降为线性或超线性，甚至不收敛 。

### 对非光滑屈服面的推广

许多经典的[屈服准则](@entry_id:193897)，如[Tresca准则](@entry_id:167002)和[Mohr-Coulomb准则](@entry_id:198821)，其[屈服面](@entry_id:175331)在[主应力空间](@entry_id:184388)中包含**角点 (corners)** 和**棱边 (edges)**。在这些非光滑点，[屈服函数](@entry_id:167970)的梯度不是唯一的，因此经典的流动法则 $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}$ 不再适用。

为了处理这种情况，我们需要借助[凸分析](@entry_id:273238)的工具。对于关联流动，正交[流动法则](@entry_id:177163)被推广为 ：

$$
\dot{\boldsymbol{\varepsilon}}^p \in \mathcal{N}_{\mathcal{K}}(\boldsymbol{\sigma}_0)
$$

这里，$\boldsymbol{\sigma}_0$ 是屈服面上的一个角点，$\mathcal{K}$ 是弹性域，$\mathcal{N}_{\mathcal{K}}(\boldsymbol{\sigma}_0)$ 是集合 $\mathcal{K}$ 在 $\boldsymbol{\sigma}_0$ 点的**[法锥](@entry_id:272387) (normal cone)**。[法锥](@entry_id:272387)包含了所有从 $\boldsymbol{\sigma}_0$ 指向集合 $\mathcal{K}$ 外部的向量。

对于由多个[光滑函数](@entry_id:267124) $f_i$ 交汇而成的角点，[法锥](@entry_id:272387)可以具体化。此时，塑性[应变率](@entry_id:154778)是各个光滑屈服[面法向量](@entry_id:749211)的非负线性组合，即：

$$
\dot{\boldsymbol{\varepsilon}}^p = \sum_{i \in \mathcal{I}_0} \dot{\lambda}_i \frac{\partial f_i}{\partial \boldsymbol{\sigma}}
$$

其中 $\mathcal{I}_0$ 是在 $\boldsymbol{\sigma}_0$ 点激活的屈服面索引集合 ($f_i(\boldsymbol{\sigma}_0)=0$)，$\dot{\lambda}_i \ge 0$ 是相应的塑性乘子。这被称为**Koiter组合流动法则 (Koiter's generalized flow rule)**，它为在非光滑[屈服点](@entry_id:188474)上的[塑性流动](@entry_id:201346)提供了明确的数学描述 。这一推广在处理实际工程材料的复杂屈服行为时至关重要。