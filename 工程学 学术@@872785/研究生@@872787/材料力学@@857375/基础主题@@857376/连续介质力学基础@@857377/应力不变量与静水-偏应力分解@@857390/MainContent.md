## 引言
在工程与科学分析中，准确描述和预测材料在复杂载荷下的行为是核心挑战。材料内部任意一点的受力状态由柯西应力张量描述，但其六个独立分量会随[坐标系](@entry_id:156346)变化，这使得直接洞察其物理效应变得困难。如何从复杂的张量信息中提取出内在的、不依赖于观察者[坐标系](@entry_id:156346)的物理量，从而将应力状态与材料的宏观响应（如变形、屈服、破坏）联系起来？这便是固体力学中的一个根本性问题。

本文旨在系统性地回答这一问题，为读者构建一个清晰而强大的理论框架。我们将深入探讨应力张量分析的两个核心概念：[静水-偏应力分解](@entry_id:196441)与[应力不变量](@entry_id:170526)。通过这些工具，任何复杂的应力状态都能被优雅地拆解为两个物理意义明确的部分——一个驱动体积变化，另一个驱动形状改变。

在接下来的章节中，你将学到：
*   **原理与机制**：我们将首先阐明[应力分解](@entry_id:272862)的数学基础和物理意义，介绍[主不变量](@entry_id:193522)与偏[应力[不变](@entry_id:170526)量](@entry_id:148850)的定义，并通过[主应力空间](@entry_id:184388)的几何图像直观地理解它们的作用。
*   **应用与跨学科联系**：随后，我们将展示这一理论框架的强大应用价值，解释它如何成为区分[金属塑性](@entry_id:176585)（压力不敏感）与岩土破坏（压力敏感）等不同材料模型的基石。
*   **动手实践**：最后，通过一系列精心设计的计算练习，你将有机会亲自应用这些概念，巩固对核心计算技能的掌握，并加深对理论内涵的理解。

让我们从最基本的原理开始，揭示隐藏在[应力张量](@entry_id:148973)背后的深刻物理与几何结构。

## 原理与机制

在连续介质力学中，理解材料内部任意一点的受力状态是至关重要的。这一状态由柯西应力张量 $\boldsymbol{\sigma}$ 所描述，它是一个二阶对称张量。然而，一个完整的二阶张量包含六个独立分量，这使得直接从其分量来洞察材料的物理行为变得复杂。更为根本的是，张量的分量会随着[坐标系](@entry_id:156346)的旋转而改变，但材料的物理响应（例如屈服或断裂）不应依赖于我们选择的[坐标系](@entry_id:156346)。因此，我们需要一种更内在、更物理的方法来描述和分析应力状态。

本章的核心目标是建立这样一个框架。我们将阐明，任何复杂的应力状态都可以被唯一地分解为两个基本部分的和：一个引起体积变化的**[静水应力](@entry_id:186327)**（hydrostatic stress）[部分和](@entry_id:162077)一个引起形状变化的**[偏应力](@entry_id:163323)**（deviatoric stress）部分。随后，我们将引入不随[坐标系](@entry_id:156346)改变的标量——**[应力不变量](@entry_id:170526)**（stress invariants），它们为客观地描述应力状态提供了数学语言。最后，我们将探讨这些概念如何成为连接应力状态与材料宏观力学行为（如弹性变形与塑性屈服）的关键机制。

### 应力的[静水-偏应力分解](@entry_id:196441)

描述应力状态的第一步是将其分解为物理上更易于理解的组成部分。任何一个对称的二阶应力张量 $\boldsymbol{\sigma}$ 都可以被唯一地分解为一个球形张量（静水部分）和一个[无迹张量](@entry_id:274053)（[偏应力](@entry_id:163323)部分）的和。

#### 基于[正交投影](@entry_id:144168)的推导

我们可以从一个更严谨的数学视角来理解这种分解。所有对称[二阶张量](@entry_id:199780)的集合构成一个六维[向量空间](@entry_id:151108)，我们可以在这个空间上定义一个弗罗宾尼斯[内积](@entry_id:158127)（Frobenius inner product）：$\mathbf{A}:\mathbf{B} = \operatorname{tr}(\mathbf{A}^{\mathsf{T}}\mathbf{B})$。在这个空间中，单位张量 $\mathbf{I}$ 张成一个一维的“各向同性”或“球形”[子空间](@entry_id:150286)。[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 在这个[子空间](@entry_id:150286)上的[正交投影](@entry_id:144168)，就定义了它的静水部分 $\boldsymbol{\sigma}_{\text{hyd}}$ [@problem_id:2911568]。

根据[正交投影](@entry_id:144168)的公式，我们有：
$$
\boldsymbol{\sigma}_{\text{hyd}} = \frac{\boldsymbol{\sigma}:\mathbf{I}}{\mathbf{I}:\mathbf{I}}\mathbf{I}
$$
我们来计算[内积](@entry_id:158127)。分子是 $\boldsymbol{\sigma}:\mathbf{I} = \operatorname{tr}(\boldsymbol{\sigma}^{\mathsf{T}}\mathbf{I}) = \operatorname{tr}(\boldsymbol{\sigma})$。分母是 $\mathbf{I}:\mathbf{I} = \operatorname{tr}(\mathbf{I}^2) = \operatorname{tr}(\mathbf{I})$。在三维空间中，$\operatorname{tr}(\mathbf{I}) = \delta_{11}+\delta_{22}+\delta_{33} = 3$。因此，投影结果为：
$$
\boldsymbol{\sigma}_{\text{hyd}} = \frac{\operatorname{tr}(\boldsymbol{\sigma})}{3}\mathbf{I}
$$
我们定义一个标量，称为**平均应力**（mean stress），记为 $p$（在某些文献中也记为 $\sigma_m$），其值为：
$$
p = \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_{11}+\sigma_{22}+\sigma_{33})
$$
于是，[静水应力](@entry_id:186327)张量可以简洁地写为 $\boldsymbol{\sigma}_{\text{hyd}} = p\mathbf{I}$。

应力张量的剩余部分，即从 $\boldsymbol{\sigma}$ 中减去其在球形[子空间](@entry_id:150286)上的投影，定义为**[偏应力张量](@entry_id:267642)**（deviatoric stress tensor），记为 $\mathbf{s}$：
$$
\mathbf{s} = \boldsymbol{\sigma} - \boldsymbol{\sigma}_{\text{hyd}} = \boldsymbol{\sigma} - p\mathbf{I}
$$
通过这种方式，我们得到了应力张量的**[静水-偏应力分解](@entry_id:196441)**：$\boldsymbol{\sigma} = p\mathbf{I} + \mathbf{s}$。

这个分解是唯一的 [@problem_id:2920790]。要验证这一点，我们只需证明[偏应力张量](@entry_id:267642) $\mathbf{s}$ 确实位于球形[子空间](@entry_id:150286)的正交补空间中，即 $\mathbf{s}$ 与任意球形张量（特别是 $\mathbf{I}$）的[内积](@entry_id:158127)为零。这等价于证明 $\mathbf{s}$ 的迹为零：
$$
\operatorname{tr}(\mathbf{s}) = \operatorname{tr}(\boldsymbol{\sigma} - p\mathbf{I}) = \operatorname{tr}(\boldsymbol{\sigma}) - \operatorname{tr}(p\mathbf{I}) = \operatorname{tr}(\boldsymbol{\sigma}) - p\operatorname{tr}(\mathbf{I}) = 3p - p(3) = 0
$$
由于[偏应力张量](@entry_id:267642)的迹恒为零，它也被称为[无迹张量](@entry_id:274053)。

#### 物理诠释

这种数学上的分解具有深刻的物理意义。

**[静水应力](@entry_id:186327)** $\boldsymbol{\sigma}_{\text{hyd}}$ 代表了应力状态中均匀、各向同性的部分。它在所有方向上施加相同的[正应力](@entry_id:260622)，类似于流体中的[静水压力](@entry_id:275365)。事实上，**[热力学](@entry_id:141121)压力**（thermodynamic pressure） $p_{\text{pressure}}$ 通常定义为与[平均应力](@entry_id:751819)符号相反的量，因为在固体力学中通常规定拉伸为正，而在[流体力学](@entry_id:136788)和[热力学](@entry_id:141121)中规定压缩为正。因此，
$$
p_{\text{pressure}} = -p = -\frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})
$$
例如，对于一个应力状态 $\boldsymbol{\sigma}=\begin{bmatrix} -100  20  0\\ 20  -130  0\\ 0  0  -110 \end{bmatrix}\,\text{MPa}$，其迹为 $I_1 = -100 - 130 - 110 = -340\,\text{MPa}$。[平均应力](@entry_id:751819)为 $p = -340/3 \approx -113.3\,\text{MPa}$（表示平均受压），而[热力学](@entry_id:141121)压力为 $p_{\text{pressure}} \approx 113.3\,\text{MPa}$（一个正值，表示压缩）[@problem_id:2920831]。

[静水应力](@entry_id:186327)部分对任何[截面](@entry_id:154995)产生的作用力都只包含法向分量，且大小恒为 $p$，不产生任何剪切作用 [@problem_id:2630210]。在小应变[各向同性线弹性](@entry_id:185899)理论中，正是[静水应力](@entry_id:186327)部分导致了材料的[体积应变](@entry_id:267252) $\varepsilon_v$，两者通过[体积模量](@entry_id:160069) $K$ 联系起来：$p = K \varepsilon_v$ [@problem_id:2920831]。

**[偏应力](@entry_id:163323)** $\mathbf{s}$ 则代表了应力状态中引起形状改变（畸变）的部分。它所产生的[法向应力](@entry_id:260622)在不同方向上是变化的，且其在所有方向上的平均值为零。更重要的是，偏应力是产生剪切应力的根源。在小应变[各向同性线弹性](@entry_id:185899)理论中，[偏应力张量](@entry_id:267642)与偏[应变张量](@entry_id:193332)（代表形状改变）通过[剪切模量](@entry_id:167228) $G$ 联系起来。因此，[偏应力](@entry_id:163323)导致材料的畸变，而不引起体积变化。

总结来说，[静水-偏应力分解](@entry_id:196441)将应力张量优雅地分离为两个正交且物理意义明确的部分：一个与体积变化相关（[静水应力](@entry_id:186327)），一个与形状变化相关（偏应力）。这一分离是理解和建模复杂材料行为的基础。

### 坐标无关的描述：[应力不变量](@entry_id:170526)

尽管[应力张量](@entry_id:148973)的分量依赖于[坐标系](@entry_id:156346)的选择，但应力状态的某些内在属性是客观存在的。这些属性由[应力不变量](@entry_id:170526)来量化，它们是不随[坐标系](@entry_id:156346)旋转而改变的标量。对于[各向同性材料](@entry_id:170678)，其本构关系（如[应变能函数](@entry_id:178435)或屈服准则）必须只依赖于这些[不变量](@entry_id:148850)，以保证其响应的客观性 [@problem_id:2920793]。

#### 柯西[应力张量](@entry_id:148973)的三个[主不变量](@entry_id:193522)

任何二阶张量 $\boldsymbol{\sigma}$ 的[主不变量](@entry_id:193522)可以通过其[特征方程](@entry_id:265849) $\det(\boldsymbol{\sigma} - \lambda\mathbf{I}) = -\lambda^3 + I_1\lambda^2 - I_2\lambda + I_3 = 0$ 的系数来定义。这三个[主不变量](@entry_id:193522) $I_1, I_2, I_3$ 也可以直接通过张量运算得到：
$$
I_1 = \operatorname{tr}(\boldsymbol{\sigma})
$$
$$
I_2 = \frac{1}{2}\left[ (\operatorname{tr}\boldsymbol{\sigma})^2 - \operatorname{tr}(\boldsymbol{\sigma}^2) \right]
$$
$$
I_3 = \det(\boldsymbol{\sigma})
$$
这些[不变量](@entry_id:148850)与[应力张量](@entry_id:148973)的三个[主应力](@entry_id:176761)（[特征值](@entry_id:154894)）$\sigma_1, \sigma_2, \sigma_3$ 之间有直接的关系 [@problem_id:2920825]：
$$
I_1 = \sigma_1 + \sigma_2 + \sigma_3
$$
$$
I_2 = \sigma_1\sigma_2 + \sigma_2\sigma_3 + \sigma_3\sigma_1
$$
$$
I_3 = \sigma_1\sigma_2\sigma_3
$$
主应力本身也是[不变量](@entry_id:148850)，它们代表了在某些特定方向（主方向）上作用的纯正应力。一个应力状态的[主应力](@entry_id:176761)和主方向是唯一的（除非出现[特征值](@entry_id:154894)简并），它们在[坐标旋转](@entry_id:164444)下保持不变，只是其主方向的矢量分量会随[坐标系](@entry_id:156346)变化而改变 [@problem_id:2920793]。

#### [偏应力张量](@entry_id:267642)的[不变量](@entry_id:148850)

在许多物理模型中，特别是塑性力学，[偏应力张量](@entry_id:267642) $\mathbf{s}$ 的[不变量](@entry_id:148850)扮演着更为核心的角色。我们记其[不变量](@entry_id:148850)为 $J_1, J_2, J_3$。

- **第一[不变量](@entry_id:148850) $J_1$**: 根据定义，[偏应力](@entry_id:163323)是无迹的，所以 $J_1 = \operatorname{tr}(\mathbf{s}) = 0$。

- **第二[不变量](@entry_id:148850) $J_2$**: 这个[不变量](@entry_id:148850)是迄今为止最重要的一个，它量化了偏应力的“大小”或畸变强度。其定义为：
$$
J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s} = \frac{1}{2}\operatorname{tr}(\mathbf{s}^2)
$$
$J_2$ 与材料的[畸变能](@entry_id:198925)密度直接相关。用主应力可以表示为 [@problem_id:2920825]：
$$
J_2 = \frac{1}{6}\left[ (\sigma_1-\sigma_2)^2 + (\sigma_2-\sigma_3)^2 + (\sigma_3-\sigma_1)^2 \right]
$$
这个表达式清楚地表明，$J_2$ 衡量了主应力之间的差异，即剪切效应的强度。

- **第三[不变量](@entry_id:148850) $J_3$**: 它描述了偏应力状态的“模式”或“类型”。其定义为：
$$
J_3 = \det(\mathbf{s})
$$

#### 物理意义最清晰的[不变量](@entry_id:148850)组合 $(I_1, J_2, J_3)$

虽然 $(I_1, I_2, I_3)$ 是一组完备的[不变量](@entry_id:148850)，但组合 $(I_1, J_2, J_3)$ 在物理上更为直观，因为它直接对应于[静水-偏应力分解](@entry_id:196441) [@problem_id:2686708]。
- $I_1$ 直接度量了[静水应力](@entry_id:186327)水平。
- $J_2$ 和 $J_3$ 完整地描述了偏应力状态的强度和模式。

一个至关重要的特性是，当给应力状态叠加一个任意的[静水应力](@entry_id:186327) $q\mathbf{I}$ 时，新的应力张量为 $\boldsymbol{\sigma}' = \boldsymbol{\sigma} + q\mathbf{I}$。其[偏应力](@entry_id:163323)部分保持不变：$\mathbf{s}' = \mathbf{s}$。因此，偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2$ 和 $J_3$ 也保持不变 [@problem_id:2920790] [@problem_id:2686708]。这一性质对于建立与静水压力无关的材料模型（如金属的[经典塑性理论](@entry_id:167389)）至关重要。

例如，考虑一个主应力状态 $\boldsymbol{\sigma}=\mathrm{diag}(100, 40, -20)\,\text{MPa}$。我们可以计算出：
- $I_1 = 100 + 40 - 20 = 120\,\text{MPa}$。
- [平均应力](@entry_id:751819) $p = 120/3 = 40\,\text{MPa}$。
- [偏应力](@entry_id:163323)主值为 $s_1 = 100-40=60$, $s_2=40-40=0$, $s_3=-20-40=-60$ (MPa)。
- $J_2 = \frac{1}{2}(60^2 + 0^2 + (-60)^2) = 3600\,\text{MPa}^2$。
- $J_3 = (60)(0)(-60) = 0\,\text{MPa}^3$。
如果在这个应力状态上叠加一个 $50\,\text{MPa}$ 的静水拉应力，新的[主应力](@entry_id:176761)为 $(150, 90, 30)$。新的 $I_1$ 变为 $270\,\text{MPa}$，但 $J_2$ 和 $J_3$ 的值将完全不变 [@problem_id:2686708]。

### 几何解释：[主应力空间](@entry_id:184388)

为了更直观地理解这些[不变量](@entry_id:148850)，我们可以将应力状态视为三维[主应力空间](@entry_id:184388)（也称为[Haigh-Westergaard空间](@entry_id:750130)）中的一个点 $(\sigma_1, \sigma_2, \sigma_3)$。

#### 静水轴与[偏应力](@entry_id:163323)平面

在这个空间中，所有形如 $(\sigma, \sigma, \sigma)$ 的点构成一条直线，称为**静水轴**。这条线上的任何一点都代表一个纯[静水应力](@entry_id:186327)状态。

与静水轴正交的所有平面族，即满足 $\sigma_1+\sigma_2+\sigma_3 = \text{常数}$ 的平面，被称为**偏应力平面**（或 $\pi$ 平面）。任何一个应力点 $(\sigma_1, \sigma_2, \sigma_3)$ 都可以被投影到静水轴上的一点 $(p, p, p)$，以及偏应力平面上的一个向量。

#### [不变量](@entry_id:148850)的几何意义

在这个几何框架中，[不变量](@entry_id:148850)的意义变得非常清晰 [@problem_id:2920792]：
- 第一[不变量](@entry_id:148850) $I_1 = 3p$ 决定了应力点所在的[偏应力](@entry_id:163323)平面的位置，它与点到原点的投影在静水轴上的距离成正比。
- 第二偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2$ 与应力点到静水轴的距离的平方成正比。具体来说，该距离 $\rho$ 为 $\rho = \sqrt{s_1^2+s_2^2+s_3^2} = \sqrt{2J_2}$。因此，[屈服准则](@entry_id:193897)中常见的条件 $J_2 = \text{常数}$ 在[主应力空间](@entry_id:184388)中对应一个以静水轴为中心轴的圆柱面。

#### 洛德角 (Lode Angle)

为了完整描述应力点在偏应力平面内的位置，我们还需要一个角度坐标。这个角色由**洛德角** $\theta$ 扮演。它定义了[偏应力](@entry_id:163323)状态的“类型”。洛德角由以下关系隐式定义 [@problem_id:2920792]：
$$
\cos(3\theta) = \frac{3\sqrt{3}}{2}\frac{J_3}{J_2^{3/2}}
$$
通过将[主应力](@entry_id:176761)排序（例如 $\sigma_1 \ge \sigma_2 \ge \sigma_3$），洛德角可以被唯一地确定在区间 $[0, \pi/3]$ 内。这个角度有明确的物理对应：
- $\theta=0$：对应**三轴压缩**状态（例如 $\sigma_1 > \sigma_2 = \sigma_3$），此时 $\cos(3\theta)=1$。
- $\theta=\pi/3$：对应**三轴拉伸**状态（例如 $\sigma_1 = \sigma_2 > \sigma_3$），此时 $\cos(3\theta)=-1$。
- $\theta=\pi/6$：对应**纯剪切**状态（例如 $\sigma_1 = -\sigma_3, \sigma_2=0$），此时 $J_3=0$，$\cos(3\theta)=0$。

洛德角 $\theta$ 只依赖于 $J_2$ 和 $J_3$ 的比值，这意味着它与[偏应力](@entry_id:163323)的大小无关，只取决于其“方向” [@problem_id:2920792]。因此，$(I_1, J_2, \theta)$ 构成了一套描述应力状态的[柱坐标系](@entry_id:266798)，其中 $I_1$ 是“高度”，$\sqrt{2J_2}$ 是“半径”，$\theta$ 是“角度”。这套[坐标系](@entry_id:156346)在构建依赖于应力状态类型的复杂材料模型时至关重要。

### 机制与应用

[应力分解](@entry_id:272862)与[不变量理论](@entry_id:145135)之所以如此重要，是因为它们构成了描述和预测[材料力学](@entry_id:201885)行为的核心机制。

#### [各向同性弹性](@entry_id:203237)中的解耦

在线性、[各向同性弹性](@entry_id:203237)材料中，[静水应力](@entry_id:186327)和偏应力的力学效应是完全**[解耦](@entry_id:637294)**的。这意味着，[静水应力](@entry_id:186327)只产生体积应变，而[偏应力](@entry_id:163323)只产生畸变（形状）应变。它们的本构关系可以写成两个独立的方程：
$$
p = K \operatorname{tr}(\boldsymbol{\varepsilon}) \quad \text{和} \quad \mathbf{s} = 2G \operatorname{dev}(\boldsymbol{\varepsilon})
$$
其中 $\boldsymbol{\varepsilon}$ 是应变张量，$K$ 是体积模量，$G$ 是[剪切模量](@entry_id:167228)。

这种[解耦](@entry_id:637294)现象的根本原因在于**各向同性**这一对称性要求。从[群表示论](@entry_id:141930)的观点看，对称二阶张量空间可以分解为两个不等价的不可约[子空间](@entry_id:150286)：1维的球形[子空间](@entry_id:150286)和5维的无迹[子空间](@entry_id:150286)。根据[舒尔引理](@entry_id:136779)（Schur's Lemma），任何与[旋转群](@entry_id:204412)可交换的线性算子（即各向同性本构算子）在这两个[子空间](@entry_id:150286)之间不能有“[交叉](@entry_id:147634)”项，并且在每个[子空间](@entry_id:150286)内只能表现为一个标量乘子（即 $K$ 和 $2G$）[@problem_id:2920832]。简单来说，各向同性意味着材料没有“特殊方向”，因此无法将一个纯球形（各向同性）的输入（如静水应变）映射到一个具有方向性的非球形输出（如[偏应力](@entry_id:163323)）[@problem_id:2920832]。

#### [应力功率](@entry_id:182907)的分解

这种解耦也体现在[应力功率](@entry_id:182907)（单位体积[内应力](@entry_id:193721)所做的功的速率）上。总[应力功率](@entry_id:182907) $\mathcal{P} = \boldsymbol{\sigma} : \mathbf{d}$（其中 $\mathbf{d}$ 是变形率张量）可以被精确地分解为两部分 [@problem_id:2630210]：
$$
\mathcal{P} = (p\mathbf{I}+\mathbf{s}) : (\frac{1}{3}\operatorname{tr}(\mathbf{d})\mathbf{I} + \operatorname{dev}(\mathbf{d})) = p \operatorname{tr}(\mathbf{d}) + \mathbf{s} : \operatorname{dev}(\mathbf{d})
$$
第一项 $p \operatorname{tr}(\mathbf{d})$ 是**体积功率**，代表用于改变体积的功率。第二项 $\mathbf{s} : \operatorname{dev}(\mathbf{d})$ 是**畸变功率**，代表用于改变形状的功率。由于球形张量和[偏张量](@entry_id:185837)在弗罗宾尼斯[内积](@entry_id:158127)下正交，交叉项为零。这再次表明，与体积变化和形状变化相关的力学过程是能量上独立的。

#### 塑性力学中的屈服准则

在塑性理论中，[屈服准则](@entry_id:193897)定义了材料从弹性变形过渡到永久（塑性）变形的应力边界。
- 对于[延性](@entry_id:160108)金属等**压力不敏感**材料，实验表明其屈服很大程度上不受静水压力的影响。因此，它们的屈服准则只依赖于偏[应力[不变](@entry_id:170526)量](@entry_id:148850)。最著名的**冯·米塞斯（von Mises）[屈服准则](@entry_id:193897)**就是一个典型的例子，它假定当 $J_2$ 达到一个临界值时材料开始屈服：$f(J_2) = \sqrt{3J_2} - Y_0 = 0$，其中 $Y_0$ 是[单轴拉伸](@entry_id:188287)下的屈服应力。在这个模型下，一个纯静水加载路径（$\mathbf{s}=\mathbf{0}$, $J_2=0$）永远不会引起塑性流动 [@problem_id:2630210]。

- 对于土壤、岩石、混凝土等**压力敏感**材料，其强度（屈服应力）显著依赖于所受的围压。因此，它们的[屈服准则](@entry_id:193897)必须同时是 $I_1$ 和偏[应力[不变](@entry_id:170526)量](@entry_id:148850)的函数。**德鲁克-普拉格（Drucker-Prager）屈服准则**是一个简单的[线性模型](@entry_id:178302)：$f(I_1, J_2) = \alpha I_1 + \sqrt{J_2} - k = 0$。这里的 $I_1$ 项就体现了对[静水压力](@entry_id:275365)的依赖性 [@problem_id:2911568]。更复杂的模型，如**莫尔-库仑（Mohr-Coulomb）准则**，还会引入对 $J_3$（或洛德角 $\theta$）的依赖，以区分材料在不同剪切模式下的强度差异。

### 高等话题：有限应变下的考虑

以上讨论主要基于小应变理论框架。当变形很大时，必须使用[有限应变理论](@entry_id:176941)，并区分不同的应力张量（如Cauchy应力 $\boldsymbol{\sigma}$、[Kirchhoff应力](@entry_id:751039) $\boldsymbol{\tau}$、[第二Piola-Kirchhoff应力](@entry_id:173163) $\mathbf{S}$ 等）。此时，[静水-偏应力分解](@entry_id:196441)的概念需要更仔细地审视 [@problem_id:2920809]。

- **客观性**：对于定义在当前构型下的张量（如 $\boldsymbol{\sigma}$ 和 $\boldsymbol{\tau}$）和定义在参考构型下的张量（如 $\mathbf{S}$），可以在它们各自的构型中进行[静水-偏应力分解](@entry_id:196441)。可以证明，这些分解在刚体运动叠加下是**客观的**。例如，对于柯西应力，其迹 $I_1(\boldsymbol{\sigma})$ 是一个客观标量，而其[偏应力](@entry_id:163323)部分 $\mathbf{s}$ 则遵循客观张量的变换规律 [@problem_id:2920809]。

- **度量依赖性**：然而，一个关键的复杂性在于，这种分解**不是**在不同应力度量之间保持不变的。换言之，一个在参考构型中是纯球形的[第二Piola-Kirchhoff应力](@entry_id:173163) $\mathbf{S}=p_S\mathbf{I}$，在通过推前（push-forward）操作映射到当前构型后，得到的柯西应力 $\boldsymbol{\sigma} = \frac{p_S}{J}\mathbf{F}\mathbf{F}^{\mathsf{T}} = \frac{p_S}{J}\mathbf{B}$（其中 $\mathbf{B}$ 是左Cauchy-Green变形张量）通常**不是**球形的 [@problem_id:2920809]。它仅在变形是纯粹[均匀缩放](@entry_id:267671)时（即 $\mathbf{B}$ 是 $\mathbf{I}$ 的标量倍）才是球形的。这意味着，在有限变形理论中，不存在一个跨越不同构型和不同应力度量的、统一的“静水压力”概念。必须根据所选的应力度量和构型来精确定义和解释静水和偏应力部分。

总之，应力的[静水-偏应力分解](@entry_id:196441)及相关的[不变量理论](@entry_id:145135)，为我们提供了一套强大而深刻的工具，用以剖析复杂的应力状态，并将其与材料的物理行为（如体积变化、形状改变、弹性和塑性）联系起来。这一框架不仅是现代[固体力学](@entry_id:164042)分析的基石，也是高级材料[本构模型](@entry_id:174726)发展的理论基础。