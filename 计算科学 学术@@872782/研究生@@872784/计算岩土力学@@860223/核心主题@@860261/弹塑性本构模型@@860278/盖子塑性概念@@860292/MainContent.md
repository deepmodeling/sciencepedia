## 引言
岩土材料，如土壤和岩石，表现出极其复杂的力学行为，这对[土木工程](@entry_id:267668)、地质灾害预测和资源开采等领域构成了巨大挑战。一个核心的难题在于，这些材料在不同应力条件下会展现出截然不同的响应：在较高剪应力下它们会发生剪切破坏，而在较高静水压力下它们则会发生塑性压密。传统的单一屈服准则模型难以同时捕捉这两种关键机制，从而限制了其预测能力。

[帽盖塑性](@entry_id:747120)模型（Cap Plasticity Model）正是为了解决这一知识鸿沟而提出的。它通过一个巧妙的复合[屈服面](@entry_id:175331)结构，成功地将剪切破坏行为和体积压密行为统一在一个连贯的[弹塑性](@entry_id:193198)框架之内。本文旨在为读者提供一个关于[帽盖塑性](@entry_id:747120)模型的全面而深入的指南，从基本原理到前沿应用，帮助您建立起对这一强大分析工具的深刻理解。

在接下来的内容中，我们将分三步展开：首先，在**“原理与机制”**一章中，我们将从[应力不变量](@entry_id:170526)讲起，详细拆解屈服面的几何构成、[硬化](@entry_id:177483)规律的物理内涵以及[塑性流动](@entry_id:201346)的数学框架，并介绍其数值实现的核心算法。随后，在**“应用与[交叉](@entry_id:147634)学科联系”**一章中，我们将展示该模型如何应用于实际的岩土工程问题，如参数标定和复杂行为模拟，并探讨其在[粘塑性](@entry_id:165397)、多物理场耦合、[计算力学](@entry_id:174464)乃至[行星科学](@entry_id:158926)等[交叉](@entry_id:147634)领域的扩展。最后，**“动手实践”**部分将提供具体的计算练习，让您有机会亲手应用所学知识，巩固对核心概念的掌握。

## 原理与机制

本章旨在系统阐述土体材料[帽盖塑性](@entry_id:747120)模型的基本原理和核心机制。我们将从[应力不变量](@entry_id:170526)的定义出发，构建[屈服面](@entry_id:175331)的几何架构，深入探讨硬化规律和[塑性流动法则](@entry_id:189597)的物理内涵，并最终建立起连接理论与计算的数学框架。本章内容是后续章节中数值实现和应用分析的理论基石。

### [应力不变量](@entry_id:170526)与屈服面表示

为了客观描述各向同性材料的力学行为，其[本构关系](@entry_id:186508)必须独立于[坐标系](@entry_id:156346)的选择。这意味着，定义了[材料弹性](@entry_id:751729)与塑性行为边界的**[屈服函数](@entry_id:167970)** (yield function) 只能通过[应力张量](@entry_id:148973)的[标量不变量](@entry_id:193787)来表达。在[土力学](@entry_id:180264)中，最常用且最具物理意义的[不变量](@entry_id:148850)是基于[应力张量](@entry_id:148973)分解得到的。

任何对称的柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 都可以分解为一个球量部分和一个偏量部分：
$$
\boldsymbol{\sigma} = p\boldsymbol{I} + \boldsymbol{s}
$$
其中，$\boldsymbol{I}$ 是二阶单位张量。

球量部分由**[平均应力](@entry_id:751819)** (mean stress) $p$ 度量，它代表了应力状态下的静水压力分量，主要引起材料的体积变形。在岩土力学中，通常约定压应力为正，其定义为[应力张量](@entry_id:148973)第一[不变量](@entry_id:148850) $I_1 = \mathrm{tr}(\boldsymbol{\sigma})$ 的三分之一：
$$
p = \frac{1}{3} I_1 = \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3} (\sigma_{11} + \sigma_{22} + \sigma_{33})
$$
式中，$\sigma_{11}, \sigma_{22}, \sigma_{33}$ 是[主应力](@entry_id:176761)。

偏量部分由**[偏应力张量](@entry_id:267642)** (deviatoric stress tensor) $\boldsymbol{s}$ 表示，它代表了应力状态下的剪切分量，主要引起材料的形状改变（畸变）。其定义为：
$$
\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}
$$
根据定义，[偏应力张量](@entry_id:267642)的迹恒为零，即 $\mathrm{tr}(\boldsymbol{s}) = 0$。

对于各向同性材料，[屈服函数](@entry_id:167970) $F$ 可以表示为[平均应力](@entry_id:751819) $p$ 以及偏[应力[不变](@entry_id:170526)量](@entry_id:148850)的函数。最常用的偏[应力[不变](@entry_id:170526)量](@entry_id:148850)是第二[不变量](@entry_id:148850) $J_2$ 和第三[不变量](@entry_id:148850) $J_3$。$J_2$ 与剪切应变能相关，定义为：
$$
J_2 = \frac{1}{2} \mathrm{tr}(\boldsymbol{s}^2) = \frac{1}{2} s_{ij}s_{ij}
$$
为了在二维平面上直观地表示屈服面，我们需要一个标量来度量偏应力的大小。[土力学](@entry_id:180264)中广泛采用**等效剪应力** (equivalent shear stress) $q$，其定义与 $J_2$ 直接相关：
$$
q = \sqrt{3J_2}
$$
这个定义形式十分便利。例如，在常规三轴试验的[轴对称](@entry_id:173333)应力状态下（$\sigma_2 = \sigma_3$），$q$ 可以简化为[主应力](@entry_id:176761)差的[绝对值](@entry_id:147688) $|\sigma_1 - \sigma_3|$ [@problem_id:3505343]。

许多经典的塑性模型，如 Drucker-Prager 模型和 Cam-Clay 模型，为了简化，都假设材料的屈服行为与第三偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_3$ 无关（或忽略其影响）。$J_3$ 描述了[屈服面](@entry_id:175331)在偏平面（$\pi$ 平面）上的形状。当忽略 $J_3$ 的影响时，[屈服面](@entry_id:175331)在[主应力空间](@entry_id:184388)中是一个绕静水压力轴（$p$ 轴）旋转的[曲面](@entry_id:267450)，其在 $\pi$ 平面上的[截面](@entry_id:154995)为圆形。在这种情况下，[屈服函数](@entry_id:167970)可以完全由 $p$ 和 $q$ 两个[不变量](@entry_id:148850)来描述，即 $F(p, q, \boldsymbol{\kappa}) = 0$，其中 $\boldsymbol{\kappa}$ 代表一组硬化参数。这使得在 $(p, q)$ 平面内表示和分析屈服面成为可能且完备的 [@problem_id:3505343]。

### [帽盖塑性](@entry_id:747120)模型的架构

土体等岩土材料的力学行为表现出双重特性：在较高剪应力下发生剪切破坏，在较高[静水压力](@entry_id:275365)下发生塑性压缩（压密）。单一的屈服面（如 Drucker-Prager 准则）难以同时捕捉这两种机制。因此，[帽盖塑性](@entry_id:747120)模型应运而生，它通常采用一个复合屈服面。

一个典型的帽盖模型由两部分构成：
1.  一个固定的或缓慢演化的**剪切破坏面** (shear failure surface)，用于描述材料在剪切作用下的屈服极限。
2.  一个移动的**帽盖面** (cap surface)，用于描述材料在静水压力作用下的塑性压密行为。

总的屈服域是这两个[曲面](@entry_id:267450)所围成的空间。

#### 帽盖屈服面

帽盖面是模型的核心，它控制着材料的塑性[体积应变](@entry_id:267252)和[硬化](@entry_id:177483)行为。在 $(p, q)$ 平面中，帽盖通常被描绘成一个光滑的[凸性](@entry_id:138568)曲线，它在高的平均压力侧“封闭”了弹性区域。椭圆是描述帽盖最常用的几何形状之一。

一个典型的椭圆形帽盖[屈服函数](@entry_id:167970)可以根据其几何特征来构建 [@problem_id:3505403]。假设该椭圆的中心位于 $p$ 轴上的点 $(p_c, 0)$，其在 $p$ 轴方向的半轴长为 $A$，在 $q$ 轴方向的半轴长为 $B$。根据标准[椭圆方程](@entry_id:169190)，[屈服函数](@entry_id:167970) $f_c$ 可以写为：
$$
f_c(p, q) = \left(\frac{p - p_c}{A}\right)^2 + \left(\frac{q}{B}\right)^2 - 1 = 0
$$
在帽盖模型中，这些几何参数被赋予了明确的物理意义：
-   $p_c$ 是一个**硬化变量** (hardening variable)，它表征了材料的历史最大压密程度（或称预固结压力）。随着塑性[体积应变](@entry_id:267252)的累积，$p_c$ 会发生变化，导致帽盖沿 $p$ 轴平移或缩放，这就是**硬化**机制。
-   参数 $A$ 和 $B$ 控制着椭圆的形状。它们可以被定义为 $p_c$ 的函数，例如，$A = R \cdot p_c$，$B = M \cdot p_c$ 或 $B=M$。其中，$R$ 是帽盖的**长宽比** (aspect ratio)，$M$ 则与材料的临界状态或[剪切强度](@entry_id:754762)相关。例如，一个常见的形式是 [@problem_id:3505403]：
    $$
    f_c(p, q, p_c) = \left(\frac{p - p_c}{R p_c}\right)^2 + \left(\frac{q}{M}\right)^2 - 1 = 0
    $$
    这里，$M$ 是 $p=p_c$ 处帽盖的 $q$ 轴截距，而 $R$ 是一个无量纲参数，定义了帽盖在 $p$ 轴方向的跨度与 $p_c$ 的比例。

#### 复合屈服面与光滑过渡

将剪切破坏面 $f_s(p,q)=0$（例如，Drucker-Prager 线 $q - M(p - p_t) = 0$）与帽盖面 $f_c(p,q,p_c)=0$ 组合起来，就形成了一个完整的屈服面。然而，在两个[曲面](@entry_id:267450)的交点处（称为**角点**或**[奇异点](@entry_id:199525)**），[屈服面](@entry_id:175331)的法向不唯一，这会给数值计算带来困难。

为了避免这种困难，一种常见的策略是确保两个面在交点处**光滑过渡** ($C^1$ 连续)。这要求在交点 $(p^*, q^*)$ 处，两个函数不仅值相等（均为零），而且它们的梯度（法向）也必须共线，即它们的斜率相等 [@problem_id:3505330]：
$$
\left. \frac{dq}{dp} \right|_{f_s} = \left. \frac{dq}{dp} \right|_{f_c} \quad \text{at } (p^*, q^*)
$$
通过施加这个几何约束，可以建立模型参数之间的内在联系。例如，可以推导出椭圆帽盖的半轴长 $A$ (或 $X$) 必须满足特定的表达式，从而确保[屈服面](@entry_id:175331)的光滑性 [@problem_id:3505330]。另一种处理角点问题的方法是在数值实现中采用**多表面塑性** (multi-surface plasticity) 理论，或者使用一个光滑函数来“圆化”角点 [@problem_id:3505359]。

### [硬化](@entry_id:177483)机制

塑性模型的一个核心特征是**[硬化](@entry_id:177483)** (hardening)，即[屈服面](@entry_id:175331)随塑性变形而演化的现象。对于帽盖模型，硬化主要表现为帽盖的位置 $p_c$ 随塑性压密而增大。这意味着材料在经历塑性压缩后，能够承受更高的应力而不屈服。

[硬化](@entry_id:177483)规律定义了[硬化](@entry_id:177483)变量（如 $p_c$）的变化率与塑性应变增量之间的关系。在经典的[临界状态土力学](@entry_id:748062)（CSSM）框架中，[硬化](@entry_id:177483)规律可以从材料在 $(v, \ln p)$ 平面（$v$为比容，$v=1+e$，$e$为孔隙比）中的基本行为推导出来 [@problem_id:3505422]。

土体在各向同性压缩下，其状态会沿着两条特征线演化：
- **正常固结线 (NCL)**: $v = v_N - \lambda \ln(p/p_{\text{ref}})$
- **[弹性卸载](@entry_id:748863)-再加载线 (URL)**: $v = v_{\kappa} - \kappa \ln(p/p_{\text{ref}})$

其中，$\lambda$ 是压缩指数，$\kappa$ 是[回弹](@entry_id:275734)指数。[硬化](@entry_id:177483)变量 $p_c$ 正是当前状态点在 NCL 上的投影。

总的比容变化 $dv$ 可以分解为弹性部分 $dv^e$ 和塑性部分 $dv^p$。弹性部分遵循 URL 的斜率，而总变化遵循 NCL 的斜率（在塑性加载期间）。因此，塑性比容变化 $dv^p$ 可以表示为：
$$
dv^p = dv - dv^e = -\frac{\lambda}{p_c} dp_c - \left(-\frac{\kappa}{p_c} dp_c\right) = -(\lambda - \kappa) \frac{dp_c}{p_c}
$$
塑性[体积应变](@entry_id:267252)增量 $d\varepsilon_{vp}$ (压为正) 与塑性比容变化的关系为 $d\varepsilon_{vp} = -dv^p/v$。结合上式，我们得到 $p_c$ 和 $\varepsilon_{vp}$ 之间的[微分](@entry_id:158718)关系：
$$
d\varepsilon_{vp} = \frac{\lambda - \kappa}{v} \frac{dp_c}{p_c}
$$
通过积分这个[微分方程](@entry_id:264184)，可以得到描述 $p_c$ 如何随 $\varepsilon_{vp}$ 演化的[硬化](@entry_id:177483)规律 [@problem_id:3505422]。一个简化的、但广泛使用的指数形式[硬化](@entry_id:177483)规律如下 [@problem_id:3505334]：
$$
p_c = p_{c0} \exp\left(\frac{\varepsilon_{vp}}{C}\right)
$$
其中 $p_{c0}$ 是初始预固结压力，常数 $C$ 与材料的塑性压缩性有关，在 Cam-Clay 模型中，它近似等于 $(\lambda - \kappa)/v_0$。

从这个关系中，我们可以定义**体积塑性硬化模量** $H_v$，它描述了单位塑性[体积应变](@entry_id:267252)引起的预固结压力增长率：
$$
H_v = \frac{dp_c}{d\varepsilon_{vp}} = \frac{p_c}{C}
$$
这个模量表明，硬化速率与当前帽盖的大小成正比。材料的塑性压缩性 $(\lambda - \kappa)$ 越大，[硬化](@entry_id:177483)越慢 [@problem_id:3505334]。

### [塑性流动法则](@entry_id:189597)

当应力状态达到[屈服面](@entry_id:175331)并持续加载时，材料将产生塑性应变。**[塑性流动法则](@entry_id:189597)** (plastic flow rule) 规定了塑性应变增量 $\dot{\boldsymbol{\varepsilon}}^p$ 的方向。在率无关塑性理论中，该方向由一个称为**塑性势** (plastic potential) 的函数 $g(\boldsymbol{\sigma})$ 的梯度决定：
$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$
其中，$\dot{\lambda} \ge 0$ 是一个称为**塑性乘子** (plastic multiplier) 的标量，它的大小决定了塑性变形的量值。这个关系被称为**法向法则** (normality rule)。

根据塑性[势函数](@entry_id:176105) $g$ 与[屈服函数](@entry_id:167970) $f$ 的关系，流动法则分为两类 [@problem_id:3505399]：
- **关联[流动法则](@entry_id:177163) (Associated Flow Rule)**: 当塑性势函数与[屈服函数](@entry_id:167970)相同时，即 $g=f$。这意味着塑性[应变率](@entry_id:154778)的方向垂直于[屈服面](@entry_id:175331)。关联[流动法则](@entry_id:177163)具有理论上的简洁性和良好的数学性质（如 Drucker's stability postulate），但对于岩土材料，它往往会过高地预测剪胀（剪切引起的[体积膨胀](@entry_id:144241)）。
- **[非关联流动法则](@entry_id:752544) (Non-associated Flow Rule)**: 当塑性势函数与[屈服函数](@entry_id:167970)不同时，即 $g \neq f$。这允许塑性应变率的方向不垂直于[屈服面](@entry_id:175331)。通过独立选择 $g$ 函数，可以更灵活、更准确地模拟材料的塑性流动行为，尤其是剪胀或剪缩。例如，可以选择一个与屈服面形状不同但能更好地描述体积变化的 $g$ 函数。

#### 剪胀的控制

[塑性流动法则](@entry_id:189597)直接控制着材料的**剪胀** (dilatancy) 行为，即剪切变形伴随的体积变化。对于以 $(p,q)$ [不变量](@entry_id:148850)表示的模型，塑性[体积应变率](@entry_id:272471) $\dot{\varepsilon}_v^p$ 和等效塑性[剪应变率](@entry_id:189459) $\dot{\varepsilon}_s^p$ 可以推导为 [@problem_id:3505399]：
$$
\dot{\varepsilon}_v^p = \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \dot{\lambda} \frac{\partial g}{\partial p}
$$
$$
\dot{\varepsilon}_s^p = \sqrt{\frac{2}{3} \dot{\boldsymbol{e}}^p : \dot{\boldsymbol{e}}^p} = \dot{\lambda} \frac{\partial g}{\partial q}
$$
其中 $\dot{\boldsymbol{e}}^p$ 是塑性[应变率](@entry_id:154778)的偏量部分。

剪胀率 $\Psi$ 定义为塑性[体积应变率](@entry_id:272471)与塑性[剪应变率](@entry_id:189459)之比：
$$
\Psi = \frac{\dot{\varepsilon}_v^p}{\dot{\varepsilon}_s^p} = \frac{\partial g / \partial p}{\partial g / \partial q}
$$
这个比率完全由塑性[势函数](@entry_id:176105) $g$ 在 $(p,q)$ 平面内的梯度方向决定。
- 如果 $\partial g / \partial p > 0$，则 $\dot{\varepsilon}_v^p > 0$（约定压缩为正），发生塑性压缩（**剪缩**）。这通常发生在帽盖区域。
- 如果 $\partial g / \partial p  0$，则 $\dot{\varepsilon}_v^p  0$，发生塑性膨胀（**剪胀**）。这通常发生在剪切破坏面上。
- 如果 $\partial g / \partial p = 0$，则 $\dot{\varepsilon}_v^p = 0$，发生等体积[塑性流动](@entry_id:201346)（**[临界状态](@entry_id:160700)**）。非关联模型常通过构造一个在剪切面上满足此条件的 $g$ 函数来模拟[临界状态](@entry_id:160700)行为 [@problem_id:3505399]。

### 塑性流动的数学框架

为了在数值计算中严格区分弹性行为和塑性行为，我们需要一个清晰的数学框架。这个框架由 **Kuhn-Tucker (KKT) 条件** 和**一致性条件** (consistency condition) 构成。

#### Kuhn-Tucker 加载/卸载条件

KKT 条件是描述约束优化问题的必要条件，在塑性力学中，它优雅地概括了加载和卸载的逻辑 [@problem_id:3505391]。对于一个由 $f(\boldsymbol{\sigma}, \kappa) \le 0$ 定义的弹性域，KKT 条件包括：
1.  **许可条件 (Admissibility)**: 应力状态必须位于弹性域内部或边界上，即 $f(\boldsymbol{\sigma}, \kappa) \le 0$。
2.  **非负性条件 (Non-negativity)**: 塑性乘子必须非负，$\dot{\lambda} \ge 0$。这保证了塑性过程的不[可逆性](@entry_id:143146)和耗散性，符合热力学第二定律。
3.  **互补松弛条件 (Complementarity)**: $f \cdot \dot{\lambda} = 0$。

这组条件完美地描述了三种可能的响应模式：
- **弹性状态**: 应力点在屈服面内部 ($f  0$)。根据[互补条件](@entry_id:747558)，必须有 $\dot{\lambda} = 0$。没有塑性流动发生。
- **塑性加载**: 应力点位于屈服面上 ($f=0$)，且正在发生塑性变形 ($\dot{\lambda} > 0$)。
- **中性加载/[弹性卸载](@entry_id:748863)**: 应力点位于屈服面上 ($f=0$)，但没有塑性变形发生 ($\dot{\lambda} = 0$)。这对应于应力路径沿[屈服面](@entry_id:175331)切向移动或向弹性域内部移动的情况。

#### [一致性条件](@entry_id:637057)

在塑性加载过程中（$f=0, \dot{\lambda}>0$），应力点必须始终保持在不断演化的[屈服面](@entry_id:175331)上。这意味着[屈服函数](@entry_id:167970)的时间变化率必须为零，这就是**一致性条件**：
$$
\dot{f} = 0
$$
利用链式法则，我们可以将 $\dot{f}$ 展开为 [@problem_id:3505354]：
$$
\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \kappa} \dot{\kappa} = 0
$$
这个条件是求解塑性乘子 $\dot{\lambda}$ 的关键。通过将弹性应力率关系 $\dot{\boldsymbol{\sigma}} = \mathbb{C}^e : (\dot{\boldsymbol{\varepsilon}} - \dot{\boldsymbol{\varepsilon}}^p)$、流动法则 $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} (\partial f/\partial \boldsymbol{\sigma})$ 和[硬化](@entry_id:177483)规律 $\dot{\kappa} = \dot{\lambda} h$ 代入一致性条件，我们可以解出 $\dot{\lambda}$ 的表达式。$\dot{\lambda}$ 通常表示为[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$ 的线性函数，其分子包含一个加载项 $\frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C}^e : \dot{\boldsymbol{\varepsilon}}$，分母则包含一个与[硬化](@entry_id:177483)模量相关的项 [@problem_id:3505354]。

### 数值实现：[返回映射算法](@entry_id:168456)

在有限元等数值方法中，[本构关系](@entry_id:186508)是在离散的时间（或荷载）增量步内进行积分的。**[返回映射算法](@entry_id:168456)** (Return Mapping Algorithm) 是一种高效且稳健的应力更新方法，它将 KKT 和一致性条件完美地融合在一个**[弹性预测-塑性修正](@entry_id:748860)**的框架中 [@problem_id:3505413]。

对于一个应变增量 $\Delta\boldsymbol{\varepsilon}$，算法步骤如下：

1.  **弹性预测**: 首先假设整个增量步是纯弹性的。计算一个**试验应力** (trial stress) $\boldsymbol{\sigma}^{\text{tr}}$：
    $$
    \boldsymbol{\sigma}^{\text{tr}} = \boldsymbol{\sigma}^n + \mathbb{C}^e : \Delta\boldsymbol{\varepsilon}
    $$
    在 $(p,q)$ 空间中，这对应于 $p^{\text{tr}} = p^n + K \Delta\varepsilon_v$ 和 $q^{\text{tr}} = q^n + 3G \Delta\varepsilon_s$。

2.  **屈服检查**: 用试验应力评估[屈服函数](@entry_id:167970) $f(\boldsymbol{\sigma}^{\text{tr}}, \kappa^n)$。
    - 如果 $f \le 0$，说明试验应力在弹性域内或其边界上。该假设成立，应力更新完成：$\boldsymbol{\sigma}^{n+1} = \boldsymbol{\sigma}^{\text{tr}}$，$\kappa^{n+1} = \kappa^n$。
    - 如果 $f > 0$，说明试验应力超出了[屈服面](@entry_id:175331)，该步发生了塑性变形。必须进行塑性修正。

3.  **塑性修正**: 这个步骤的目标是找到一个最终应力状态 $(\boldsymbol{\sigma}^{n+1}, \kappa^{n+1})$，它既满足屈服条件 $f(\boldsymbol{\sigma}^{n+1}, \kappa^{n+1})=0$，又满足离散形式的流动法则和[硬化](@entry_id:177483)规律。
    在几何上，塑性修正过程相当于将试验应力点 $\boldsymbol{\sigma}^{\text{tr}}$ “返回”到更新后的[屈服面](@entry_id:175331)上。对于关联塑性，这个返回路径是法向的，并且是在一个由弹性模量定义的能量范数下的**[最近点投影](@entry_id:168047)** (closest-point projection) [@problem_id:3505413]。
    
    在 $(p,q)$ 空间中，应力[更新方程](@entry_id:264802)为：
    $$
    p^{n+1} = p^{\text{tr}} - K \Delta\varepsilon_v^p = p^{\text{tr}} - K \Delta\lambda \frac{\partial f}{\partial p}
    $$
    $$
    q^{n+1} = q^{\text{tr}} - 3G \Delta\varepsilon_s^p = q^{\text{tr}} - 3G \Delta\lambda \frac{\partial f}{\partial q}
    $$
    硬化变量更新为：
    $$
    \kappa^{n+1} = \kappa^n + \Delta\varepsilon_v^p = \kappa^n + \Delta\lambda \frac{\partial f}{\partial p}
    $$
    将这些更新后的状态变量代入一致性条件 $f(p^{n+1}, q^{n+1}, \kappa^{n+1}) = 0$，我们得到一个关于单个未知数——离散塑性乘子 $\Delta\lambda$ 的[非线性](@entry_id:637147)标量方程。求解这个方程（通常使用 [Newton-Raphson](@entry_id:177436) [迭代法](@entry_id:194857)）即可得到 $\Delta\lambda$，从而完成所有状态变量的更新 [@problem_id:3505413]。

#### 角点处的挑战

当复合[屈服面](@entry_id:175331)存在角点时（例如剪切面与帽盖的交点），[屈服面](@entry_id:175331)的法向不唯一。在角点处，法向由一个**法向锥** (normal cone) 定义，它是构成该角点的两个[曲面](@entry_id:267450)法向的正[线性组合](@entry_id:154743)。根据 KKT 条件，塑性[应变率](@entry_id:154778)的方向必须位于此法向锥内 [@problem_id:3505359]。

这意味着，如果试验应力的[最近点投影](@entry_id:168047)恰好是角点，那么[塑性流动](@entry_id:201346)的方向是不确定的，这导致了[返回映射](@entry_id:754324)的模糊性。为了解决这个问题，需要采用特殊的多表面塑性算法，同时激活两个屈服面并求解两个塑性乘子，或者采用[光滑函数](@entry_id:267124)对角点进行“圆化”处理，从而在任何地方都得到唯一的法向 [@problem_id:3505359]。