## 引言
率无关塑性理论是[固体力学](@entry_id:164042)领域的基石，它为描述和预测工程材料在超过[弹性极限](@entry_id:186242)后发生的永久变形提供了基本框架。从金属的成型到结构的[失效分析](@entry_id:266723)，理解材料如何以及为何会产生不可恢复的变形至关重要。然而，这一理论涉及一系列环环相扣的概念，包括应力与应变的分解、屈服的起始、[塑性流动](@entry_id:201346)的方向和大小，以及材料在变形过程中的“记忆”效应（即[硬化](@entry_id:177483)），这为初学者构建了一个知识上的挑战。本文旨在系统性地梳理这些核心概念，填补从基础理论到高级应用的认知鸿沟。

通过本文的学习，读者将建立一个关于率无关塑性的完整知识体系。我们将分三个层次展开：首先，在“原理与机制”一章中，我们将深入剖析理论的数学和物理基础，从[运动学分解](@entry_id:751020)、J2[屈服准则](@entry_id:193897)到关联[流动法则](@entry_id:177163)和[硬化](@entry_id:177483)模型，并探讨其内在的[热力学一致性](@entry_id:138886)。接着，在“应用与跨学科连接”一章中，我们将展示这些原理如何转化为强大的计算工具（如[返回映射算法](@entry_id:168456)），并应用于[结构工程](@entry_id:152273)、[地质力学](@entry_id:175967)和[材料科学](@entry_id:152226)等多个领域。最后，在“动手实践”部分，读者将通过具体的编程练习，将理论知识转化为解决实际问题的能力，亲手实现和验证核心的塑性算法。

## 原理与机制

本章旨在系统性地阐述率无关塑性理论的基本原理和核心机制。我们将从基本的运动学和静力学分解入手，逐步深入到屈服准则、[塑性流动法则](@entry_id:189597)、硬化模型，最终探讨其内在的[热力学](@entry_id:141121)和变分结构。这些构成了理解和计算模拟[材料塑性](@entry_id:186852)行为的基石。

### 运动学与静力学基础

在深入塑性流动规律之前，我们必须首先建立描述变形和应力的基本框架。这包括如何将总[应变分解](@entry_id:186005)为弹性和塑性部分，以及如何将[应力张量](@entry_id:148973)分解为引起体积变化和形状改变的分量。

#### [应变分解](@entry_id:186005)的加法形式

在小应变假设下，一个正在经历[弹塑性](@entry_id:193198)变形的连续体中，总[应变张量](@entry_id:193332) $ \boldsymbol{\varepsilon} $ 可以被线性地分解为弹性应变 $ \boldsymbol{\varepsilon}^e $（可恢复部分）和塑性应变 $ \boldsymbol{\varepsilon}^p $（不可恢复部分）之和。这被称为 **应变的加法分解** ：

$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p
$$

这个分解是小应变理论的核心假设之一，它极大地简化了[本构模型](@entry_id:174726)的构建。弹性应变 $ \boldsymbol{\varepsilon}^e $ 与应力通过弹性本构关系（如[胡克定律](@entry_id:149682)）相关联，而塑性应变 $ \boldsymbol{\varepsilon}^p $ 的演化则由[塑性流动](@entry_id:201346)理论描述。值得注意的是，在[大应变](@entry_id:751152)情况下，这种简单的加法分解不再适用，需要采用更为复杂的[乘法分解](@entry_id:199514)形式。

#### [应力分解](@entry_id:272862)：[静水压力与偏应力](@entry_id:750463)

与[应变分解](@entry_id:186005)相对应，[应力张量](@entry_id:148973) $ \boldsymbol{\sigma} $ 也可以分解为两个具有明确物理意义的部分：**球形应力张量**（或静水压力部分）和 **[偏应力张量](@entry_id:267642)**。球形[应力张量](@entry_id:148973) $ p\boldsymbol{I} $ 描述了引起材料体积变化的均匀压力，而[偏应力张量](@entry_id:267642) $ \boldsymbol{s} $ 则描述了引起材料形状改变（[剪切变形](@entry_id:170920)）的应力状态。

[应力张量](@entry_id:148973)的第一[不变量](@entry_id:148850) $ I_1 = \operatorname{tr}(\boldsymbol{\sigma}) $ 代表了应力状态的“体积”效应。[平均应力](@entry_id:751819)或 **静水压力** 定义为 $ p = \frac{1}{3} I_1 $。因此，球形[应力张量](@entry_id:148973)为 $ \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})\boldsymbol{I} $。[偏应力张量](@entry_id:267642) $ \boldsymbol{s} $ 则通过从总应力中减去球形应力部分得到 ：

$$
\boldsymbol{s} = \boldsymbol{\sigma} - \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})\boldsymbol{I}
$$

根据定义，[偏应力张量](@entry_id:267642)的迹恒为零，即 $ \operatorname{tr}(\boldsymbol{s}) = 0 $。这意味着偏应力是一种纯剪切状态。在塑性理论中，尤其是对于金属材料，[偏应力](@entry_id:163323)起着至关重要的作用。许多塑性理论（如接下来将讨论的 von Mises 理论）假设材料的屈服仅由[偏应力](@entry_id:163323)决定，而与[静水压力](@entry_id:275365)无关。

[偏应力张量](@entry_id:267642)的 **第二[不变量](@entry_id:148850)** $ J_2 $ 是塑性力学中的一个关键量，它量化了[偏应力](@entry_id:163323)状态的“大小”或强度。其标准定义为：

$$
J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s} = \frac{1}{2}s_{ij}s_{ij}
$$

这里 $ : $ 表示张量的[双点积](@entry_id:748648)。$ J_2 $ 总是非负的，并且与[坐标系](@entry_id:156346)的选择无关。例如，对于一个给定的应力状态，如  中所示的张量，我们可以首先计算其迹 $ I_1 $ 和平均应力 $ p $，然后求出[偏应力张量](@entry_id:267642) $ \boldsymbol{s} $，最后通过计算 $ \boldsymbol{s} $ 各分量的平方和的一半来得到 $ J_2 $ 的值。

#### [塑性不可压缩性](@entry_id:183440)

对于大多数金属材料，在典型的工程温度和应变率下，塑性变形主要是由晶体内的[位错滑移](@entry_id:275474)机制主导的。从微观角度看，[位错滑移](@entry_id:275474)是一个剪切过程，它改变了晶粒的形状，但基本上不改变其体积，因为该过程不涉及原子的长程[扩散](@entry_id:141445)或[晶格](@entry_id:196752)体积的净变化。

当我们将这一微观物理机制推广到宏观连续介质模型时，一个自然且广泛应用的假设便是 **塑性体积不可压缩性**，即塑性变形不引起体积变化。在小应变理论中，这表现为塑性[应变张量](@entry_id:193332)的迹为零 ：

$$
\operatorname{tr}(\boldsymbol{\varepsilon}^p) = 0
$$

这意味着塑性[应变率](@entry_id:154778) $ \dot{\boldsymbol{\varepsilon}}^p $ 也是一个迹为零的张量，即 $ \operatorname{tr}(\dot{\boldsymbol{\varepsilon}}^p) = 0 $。这个假设不仅有坚实的物理基础，而且与后续将要介绍的、基于偏应力的 J2 塑性理论的本构结构完全自洽。

### 弹性域与[屈服准则](@entry_id:193897)

塑性理论的核心在于区分材料的弹性行为和塑性行为。这通过引入一个 **[屈服准则](@entry_id:193897)** 来实现，它在应力空间中定义了一个边界，称为 **[屈服面](@entry_id:175331)**。

#### 定义[弹性极限](@entry_id:186242)

我们假设在[应力空间](@entry_id:199156)中存在一个区域，称为 **弹性域**。只要应力状态位于该域的内部，材料的响应就是纯弹性的，卸载后不会产生残余应变。[屈服面](@entry_id:175331)是弹性域的边界。当应力路径达到并试图穿越[屈服面](@entry_id:175331)时，塑性变形便开始发生。

这个弹性域可以通过一个或多个标量值的 **[屈服函数](@entry_id:167970)** $ f(\boldsymbol{\sigma}, \boldsymbol{q}) $ 来描述，其中 $ \boldsymbol{q} $ 代表了一组描述材料内部状态的硬化变量。弹性域被定义为满足以下条件的所有应力状态的集合：

$$
f(\boldsymbol{\sigma}, \boldsymbol{q}) \le 0
$$

当 $ f  0 $ 时，应力状态在弹性域内部；当 $ f = 0 $ 时，应力状态在[屈服面](@entry_id:175331)上；而 $ f  0 $ 是不允许出现的应力状态（在率无关塑性中）。

#### von Mises (J2) 屈服准则

对于对[静水压力](@entry_id:275365)不敏感的材料（如大多数金属），一个被广泛应用的[屈服准则](@entry_id:193897)是 **von Mises** 或 **J2 屈服准则**。该准则假定，当[偏应力](@entry_id:163323)第二[不变量](@entry_id:148850) $ J_2 $ 达到一个临界值时，材料开始屈服。[屈服函数](@entry_id:167970)可以写作：

$$
f(\boldsymbol{\sigma}, \kappa) = \sqrt{3J_2} - \sigma_y(\kappa) \le 0
$$

其中 $ \sigma_y $ 是材料的当前单轴[屈服应力](@entry_id:274513)，它可能随一个标量硬化变量 $ \kappa $（如等效塑性应变）而演化。使用 $ J_2 = \frac{1}{2}\|\boldsymbol{s}\|^2 $，其中 $ \|\boldsymbol{s}\| = \sqrt{\boldsymbol{s}:\boldsymbol{s}} $ 是[偏应力张量](@entry_id:267642)的 Frobenius 范数，该准则也可等价地写为 ：

$$
f(\boldsymbol{\sigma}, \kappa) = \sqrt{\frac{3}{2}}\|\boldsymbol{s}\| - \sigma_y(\kappa) \le 0
$$

这个公式明确显示了屈服只依赖于偏应力 $ \boldsymbol{s} $ 的大小，而与静水压力 $ p $ 无关。

#### 几何解释

von Mises 屈服准则在[主应力空间](@entry_id:184388) $ (\sigma_1, \sigma_2, \sigma_3) $ 中具有清晰的几何图像。[主应力空间](@entry_id:184388)中的[静水压力](@entry_id:275365)轴是满足 $ \sigma_1 = \sigma_2 = \sigma_3 = p $ 的直线。对于任意应力点 $ (\sigma_1, \sigma_2, \sigma_3) $，其到[静水压力](@entry_id:275365)轴的[垂直距离](@entry_id:176279)的平方恰好是 $ s_1^2 + s_2^2 + s_3^2 = \|\boldsymbol{s}\|^2 $。

因此，屈服条件 $ \|\boldsymbol{s}\| = \sqrt{\frac{2}{3}}\sigma_y(\kappa) $ 描述了在[主应力空间](@entry_id:184388)中所有与静水压力轴保持恒定距离的点。这个几何轨迹是一个以[静水压力](@entry_id:275365)轴为中心轴的 **无限长圆柱**。圆柱的半径为 $ R(\kappa) = \sqrt{\frac{2}{3}}\sigma_y(\kappa) $ 。这个圆柱面就是 von Mises 屈服面。由于屈服面沿[静水压力](@entry_id:275365)轴无限延伸，任何纯静水压力状态 $ \boldsymbol{\sigma} = p\boldsymbol{I} $ 都位于圆柱内部，永远不会导致屈服，这直观地体现了 J2 塑性的压力无关性。

#### 屈服面的数学性质

为了保证塑性模型在数学上是 **适定的 (well-posed)** 并且材料响应是稳定的，[屈服函数](@entry_id:167970)和能量函数必须满足一系列数学条件。其中最关键的一条是，对于任意固定的内部状态，由 $ f \le 0 $ 定义的弹性域在应力空间中必须是一个 **凸集**。这通常通过要求[屈服函数](@entry_id:167970) $ f $ 本身是关于应力 $ \boldsymbol{\sigma} $ 的[凸函数](@entry_id:143075)来保证。

[凸性](@entry_id:138568)确保了当应力达到[屈服面](@entry_id:175331)时，材料的响应是唯一的且稳定的。此外，为了保证增量问题的解的存在性和唯一性，通常还要求[自由能函数](@entry_id:749582) $ \psi $ 是严格凸的，并且[屈服函数](@entry_id:167970) $ f $ 及其梯度是光滑和有界的。这些条件共同构成了所谓的 **广义标准材料 (Generalized Standard Material, GSM)** 框架的基础，为构建稳健的计算模型提供了理论保障 。

### [塑性流动法则](@entry_id:189597)

当应力状态达到[屈服面](@entry_id:175331)时，材料如何产生塑性变形？[塑性流动法则](@entry_id:189597)回答了这个问题，它规定了塑性应变率的方向和大小。

#### 关联流动法则

一个被广泛接受的假设是 **关联[流动法则](@entry_id:177163)**，它源于 Drucker 的稳定性公设或[最大塑性耗散](@entry_id:184825)原理。该法则指出，塑性[应变率](@entry_id:154778)的方向垂直于[屈服面](@entry_id:175331)。在数学上，这意味着塑性[应变率](@entry_id:154778) $ \dot{\boldsymbol{\varepsilon}}^p $ 与[屈服函数](@entry_id:167970)对应力的梯度 $ \frac{\partial f}{\partial \boldsymbol{\sigma}} $ 成正比：

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$

其中 $ \dot{\lambda} \ge 0 $ 是一个非负的标量，称为 **塑性乘子** 或一致性参数。它的值决定了[塑性流动](@entry_id:201346)的大小：当 $ \dot{\lambda}  0 $ 时，发生[塑性流动](@entry_id:201346)；当 $ \dot{\lambda} = 0 $ 时，则没有塑性流动。

#### [Kuhn-Tucker 条件](@entry_id:185881)：塑性的逻辑开关

塑性乘子 $ \dot{\lambda} $ 的行为由一组被称为 **Kuhn-Tucker (KKT) [互补条件](@entry_id:747558)** 的数学关系来控制。这些条件构成了率无关塑性理论的[逻辑核心](@entry_id:751444)，优雅地描述了加载和卸载的判断机制 ：

1.  **应力许可条件**: $ f(\boldsymbol{\sigma}, \boldsymbol{q}) \le 0 $
2.  **流动非负条件**: $ \dot{\lambda} \ge 0 $
3.  **互补或开关条件**: $ \dot{\lambda} f(\boldsymbol{\sigma}, \boldsymbol{q}) = 0 $

这三个条件共同决定了材料的响应状态：
*   **弹性状态**: 如果应力在屈服面内部 ($ f  0 $)，为了满足[互补条件](@entry_id:747558)，必须有 $ \dot{\lambda} = 0 $。此时没有[塑性流动](@entry_id:201346)，材料行为是纯弹性的。
*   **塑性加载**: 如果发生[塑性流动](@entry_id:201346) ($ \dot{\lambda}  0 $)，为了满足[互补条件](@entry_id:747558)，应力状态必须位于[屈服面](@entry_id:175331)上 ($ f = 0 $)。在持续的塑性加载过程中，应力状态必须始终保持在屈服面上，这要求[屈服函数](@entry_id:167970)的时间导数必须为零，即 $ \dot{f} = 0 $。这被称为 **[一致性条件](@entry_id:637057)**。
*   **[弹性卸载](@entry_id:748863)或中性加载**: 如果应力状态在屈服面上 ($ f = 0 $)，但应力增量指向弹性域内部（导致 $ \dot{f}  0 $）或沿着屈服面切向（导致 $ \dot{f}=0 $），则不会产生[塑性流动](@entry_id:201346)，即 $ \dot{\lambda}=0 $。

#### J2 塑性中的流动

将关联[流动法则](@entry_id:177163)应用于 J2 [屈服准则](@entry_id:193897) $ f = \sqrt{\frac{3}{2}}\|\boldsymbol{s}\| - \sigma_y $，我们可以计算其梯度：

$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} = \sqrt{\frac{3}{2}} \frac{\partial \|\boldsymbol{s}\|}{\partial \boldsymbol{\sigma}} = \sqrt{\frac{3}{2}} \frac{\boldsymbol{s}}{\|\boldsymbol{s}\|}
$$

由于[偏应力张量](@entry_id:267642) $ \boldsymbol{s} $ 的迹为零，梯度 $ \frac{\partial f}{\partial \boldsymbol{\sigma}} $ 的迹也为零。因此，根据关联[流动法则](@entry_id:177163) $ \dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}} $，塑性应变率的迹也必然为零：

$$
\operatorname{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \dot{\lambda} \operatorname{tr}\left(\frac{\partial f}{\partial \boldsymbol{\sigma}}\right) = 0
$$

这从本构理论的角度再次证明了 J2 塑性理论内在的[塑性不可压缩性](@entry_id:183440)  ，与前述的微观物理机制完美契合。

#### 超越光滑表面：多面塑性

当屈服面不是光滑的，而是在某些点存在角点或棱线时（例如 Tresca [屈服面](@entry_id:175331)或组合多个[屈服面](@entry_id:175331)的模型），[流动法则](@entry_id:177163)需要被推广。在这些非光滑点，梯度是不唯一的。此时，塑性应变率的方向位于由所有激活的屈服面（即 $ f_i=0 $ 的那些面）在角点处的外法线张成的 **法向锥** 内。这意味着塑性[应变率](@entry_id:154778)可以表示为所有激活面法向的非负线性组合 ：

$$
\dot{\boldsymbol{\varepsilon}}^p = \sum_{i \in \mathcal{I}_{act}} \dot{\lambda}_i \frac{\partial f_i}{\partial \boldsymbol{\sigma}}
$$

其中 $ \mathcal{I}_{act} $ 是激活[屈服面](@entry_id:175331)的索引集合，并且每个塑性乘子 $ \dot{\lambda}_i $ 都必须满足各自的 [Kuhn-Tucker 条件](@entry_id:185881) ($ \dot{\lambda}_i \ge 0, f_i \le 0, \dot{\lambda}_i f_i = 0 $)。这为处理更复杂的材料行为，如各向异性或在复杂应力路径下的响应，提供了坚实的框架。

### [屈服面](@entry_id:175331)的演化：[硬化](@entry_id:177483)

实验表明，当材料发生塑性变形时，其[屈服应力](@entry_id:274513)通常会发生变化。这种现象被称为 **硬化**（或软化）。[硬化](@entry_id:177483)模型描述了[屈服面](@entry_id:175331)如何随着塑性变形历史而演化。

#### [各向同性硬化](@entry_id:164486)

最简单的硬化模型是 **[各向同性硬化](@entry_id:164486)**。它假设[屈服面](@entry_id:175331)在[应力空间](@entry_id:199156)中均匀地膨胀，而不改变其形状或中心位置。这通过让[屈服应力](@entry_id:274513) $ \sigma_y $ 成为一个标量内部变量 $ \kappa $（通常是累积塑性应变的某种度量）的函数来实现 。

一个常见的线性[各向同性硬化](@entry_id:164486)法则是：

$$
\sigma_y(\kappa) = \sigma_{y0} + H\kappa
$$

其中 $ \sigma_{y0} $ 是初始[屈服应力](@entry_id:274513)，$ H \ge 0 $ 是塑性[硬化](@entry_id:177483)模量。对于 J2 塑性，这意味着屈服圆柱的半径 $ R(\kappa) = \sqrt{\frac{2}{3}}\sigma_y(\kappa) $ 会随着塑性应变 $ \kappa $ 的累积而增大。其归一化半径可以表示为 $ r(\kappa) = R(\kappa)/R(0) = 1 + \frac{H\kappa}{\sigma_{y0}} $ 。该模型能很好地描述材料在单向拉伸下的强化现象，但无法解释某些更复杂的效应，如 Bauschinger 效应。

#### [随动硬化](@entry_id:172077)

**[随动硬化](@entry_id:172077)** 模型假设[屈服面](@entry_id:175331)在[应力空间](@entry_id:199156)中平移，而不改变其大小或形状。这种平移由一个称为 **[背应力](@entry_id:198105) (backstress)** 的张量内部变量 $ \boldsymbol{\alpha} $ 来描述。[屈服函数](@entry_id:167970)通常写成[有效应力](@entry_id:198048) $ \boldsymbol{s} - \boldsymbol{\alpha} $ 的函数，例如：

$$
f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = \sqrt{\frac{3}{2}}\|\boldsymbol{s} - \boldsymbol{\alpha}\| - \sigma_{y0} \le 0
$$

[背应力](@entry_id:198105) $ \boldsymbol{\alpha} $ 的演化与塑性[应变率](@entry_id:154778)相关。一个简单的线性演化法则是 Prager 模型：

$$
\dot{\boldsymbol{\alpha}} = c \dot{\boldsymbol{\varepsilon}}^p
$$

其中 $ c $ 是[随动硬化](@entry_id:172077)模量。[随动硬化](@entry_id:172077)能够捕捉 **Bauschinger 效应**，即材料在反向加载时，其[屈服强度](@entry_id:162154)会低于初始屈服强度。这是因为在初始拉伸塑性变形后，背应力 $ \boldsymbol{\alpha} $ 向拉伸方向移动，使得[屈服面](@entry_id:175331)中心偏离原点。当反向压缩加载时，应力路径会更快地接触到屈服面的另一侧 。

#### 混合硬化

**混合硬化** 结合了[各向同性硬化和随动硬化](@entry_id:195752)，允许屈服面同时膨胀和平移。这是描述真实材料行为更具现实性的模型。其[屈服函数](@entry_id:167970)结合了两种效应：

$$
f(\boldsymbol{\sigma}, \boldsymbol{\alpha}, \kappa) = \sqrt{\frac{3}{2}}\|\boldsymbol{s} - \boldsymbol{\alpha}\| - \sigma_y(\kappa) \le 0
$$

在这种模型中，标量硬化变量 $ \kappa $ 和张量硬化变量 $ \boldsymbol{\alpha} $ 都随着塑性变形而演化，从而提供了对[循环加载](@entry_id:181502)下材料复杂行为的更精确描述 。

### [热力学](@entry_id:141121)与变分观点

为了确保[本构模型](@entry_id:174726)的物理一致性，特别是满足热力学第二定律，我们需要从一个更基本的、基于能量和耗散的视角来审视塑性理论。

#### 严谨的[热力学](@entry_id:141121)框架

在[等温过程](@entry_id:143096)中，热力学第二定律要求材料的内耗散 $ \mathcal{D} $ 必须非负。内耗散可以表示为[应力功率](@entry_id:182907)减去 Helmholtz 自由能的变化率：$ \mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0 $。我们假设自由能 $ \psi $ 是[弹性应变](@entry_id:189634) $ \boldsymbol{\varepsilon}^e $ 和内部变量（如 $ \kappa $ 和 $ \boldsymbol{\alpha} $）的函数，即 $ \psi(\boldsymbol{\varepsilon}^e, \kappa, \boldsymbol{\alpha}) $。

通过标准的 Coleman-Noll 程序，我们可以从[耗散不等式](@entry_id:188634)中推导出与状态变量率无关的[本构关系](@entry_id:186508)。这导出了弹性应力 $ \boldsymbol{\sigma} $ 和共轭于内部变量的 **[热力学力](@entry_id:161907)**（如[各向同性硬化](@entry_id:164486)力 $ r $ 和[随动硬化](@entry_id:172077)力 $ \boldsymbol{q} $）的表达式 ：

$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^e}, \quad r = -\frac{\partial \psi}{\partial \kappa}, \quad \boldsymbol{q} = -\frac{\partial \psi}{\partial \boldsymbol{\alpha}}
$$

将这些关系代入，[耗散不等式](@entry_id:188634)被简化为一个只包含塑性“通量”（如 $ \dot{\boldsymbol{\varepsilon}}^p, \dot{\kappa}, \dot{\boldsymbol{\alpha}} $）和其共轭力的形式：

$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p + r\dot{\kappa} + \boldsymbol{q}:\dot{\boldsymbol{\alpha}} \ge 0
$$

这个 **简化[耗散不等式](@entry_id:188634)** 必须通过定义塑性流动的[演化方程](@entry_id:268137)来满足。这为构建[热力学一致的](@entry_id:755906)流动和[硬化](@entry_id:177483)法则提供了坚实的基础。

#### 耗散与[路径依赖性](@entry_id:186326)

塑性变形是一个耗散过程，意味着机械能被不可逆地转化为热能。总的塑性功（单位体积内耗散的能量）由积分 $ W_p = \int_0^t \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p dt $ 给出。一个至关重要的特性是，塑性功是一个 **[路径依赖](@entry_id:138606)** 的量，而不是一个状态函数。

这意味着，即使两个不同的加载历史的起点和终点状态（应力、应变、内部变量）完全相同，它们所累积的塑性功也可能不同。例如，在  的算例中，路径 A 经历了简单的单向塑性加载，而路径 B 经历了更大幅度的拉伸塑性变形和随后的反向压缩塑性变形。尽管最终的塑性应变相同，但路径 B 经历了更多的“微观摩擦”过程，因此耗散了更多的能量。这凸显了塑性变形的历史依赖性，与弹性变形的路径无关性形成鲜明对比。

#### 变分原理与率无关性

现代[连续介质力学](@entry_id:155125)越来越多地采用[变分原理](@entry_id:198028)来构建本构理论。对于率无关塑性，其增量问题可以在一个时间步内被表述为一个能量泛函的最小化问题。这个泛函通常包含三部分：存储的弹性能、耗散的能量以及外力所做的功 。

$$
E(\boldsymbol{u}, \boldsymbol{z}) = \int_{\Omega} \left[ W(\boldsymbol{\varepsilon}(\boldsymbol{u})-\boldsymbol{z}, \boldsymbol{z}) + R(\boldsymbol{z}-\boldsymbol{z}_n) \right] dV - \Pi_{ext}(\boldsymbol{u})
$$

这里的关键在于耗散势 $ R $ 的数学性质。对于 **率无关** 材料，耗散势 $ R $ 必须是关于其宗量（内部变量的增量）的 **正一次齐次函数**，即 $ R(\lambda \Delta \boldsymbol{z}) = \lambda R(\Delta \boldsymbol{z}) $ 对于所有 $ \lambda \ge 0 $。这个性质确保了增量耗散项 $ R(\Delta \boldsymbol{z}) $ 与时间步长 $ \Delta t $ 无关，从而使得整个最小化问题的解也与时间步长无关。这正是“率无关”的数学本质：材料的响应只取决于加载路径的几何形状，而与沿该路径加载的速度无关。

与此相对，**[粘塑性](@entry_id:165397)**（率相关塑性）模型的耗散势通常是超线性的（例如，二次齐次的）。在这种情况下，增量耗散项会显式地依赖于时间步长 $ \Delta t $，导致材料响应对[应变率](@entry_id:154778)敏感。率无关塑性可以被视为[粘塑性](@entry_id:165397)在粘性参数趋于零时的极限情况。这个极限过程将一个率相关的、非一次齐次的耗散势转变为一个率无关的、正一次齐次的耗散势 。这种变分观点不仅为理论提供了优雅的数学结构，也为开发稳健的数值算法（如[能量最小化算法](@entry_id:175155)）奠定了基础。