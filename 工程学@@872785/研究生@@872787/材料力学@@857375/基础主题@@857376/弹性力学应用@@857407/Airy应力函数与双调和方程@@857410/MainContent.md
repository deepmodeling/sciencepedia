## 引言
在[连续介质力学](@entry_id:155125)领域，求解弹性体的应力与变形状态是一项基础而核心的任务。然而，其控制[方程组](@entry_id:193238)（包含[平衡方程](@entry_id:172166)、[几何方程](@entry_id:173321)和[本构关系](@entry_id:186508)）的复杂性常常给解析求解带来巨大挑战。为了应对这一挑战，数学家和力学家们发展出了一系列精妙的数学工具，其中，**[艾里应力函数](@entry_id:191331) (Airy stress function)** 无疑是最优雅和强大的方法之一。它通过巧妙的数学构造，将原本复杂的应力分量求解问题，转化为求解一个单一的[标量势](@entry_id:276177)函数，极大地简化了二维弹性问题的理论分析。

本文旨在系统性地介绍[艾里应力函数](@entry_id:191331)理论及其应用。我们将揭示这一理论如何将物理世界的力学平衡与几何协调性，统一在一个简洁的数学方程——**[双调和方程](@entry_id:165706) (biharmonic equation)** 之中。通过本文的学习，读者将不仅理解其深刻的力学原理，还能掌握其在解决实际工程问题中的强大威力。

文章将分为三个核心部分展开：
- **原理与机制**：我们将从弹性力学的第一性原理出发，推导[艾里应力函数](@entry_id:191331)的定义及其控制方程（[双调和方程](@entry_id:165706)），并阐明其与平衡、协调、本构关系之间的深刻联系。
- **应用与交叉学科联系**：本章将展示[艾里应力函数](@entry_id:191331)在工程力学、断裂力学、[材料科学](@entry_id:152226)和[计算力学](@entry_id:174464)等多个领域的广泛应用，重点解析其在应力集中、裂纹分析和内应力计算等关键问题中的作用。
- **动手实践**：通过一系列精心设计的计算练习，读者将有机会亲手应用[艾里应力函数](@entry_id:191331)求解具体问题，从而将理论知识转化为解决实际问题的能力。

## 原理与机制

本章旨在系统地阐述二维弹性力学中一个极其优雅且强大的数学工具——**[艾里应力函数](@entry_id:191331) (Airy stress function)**。我们将从弹性力学的基本控制方程出发，揭示[艾里应力函数](@entry_id:191331)是如何巧妙地将应力分量的求解问题转化为一个标量势函数的求解问题。核心在于理解该函数如何自动满足平衡方程，以及在何种条件下，其控制方程简化为经典的**[双调和方程](@entry_id:165706) (biharmonic equation)**。本章将深入探讨这一方法的原理、应用边界、以及其在三维问题中的推广，为解决复杂的弹性力学边值问题奠定坚实的理论基础。

### 二维弹性力学的基本方程

在深入探讨[艾里应力函数](@entry_id:191331)之前，我们必须首先回顾构成平面弹性问题理论框架的三个基本要素：平衡方程、[几何方程](@entry_id:173321)和本构关系。

#### 平衡方程与[应力张量](@entry_id:148973)

对于一个处于静态平衡状态的连续体，其内部任意部分的受力也必须是平衡的。这由**柯西应力张量 (Cauchy stress tensor)** $\boldsymbol{\sigma}$ 来描述，它反映了物体内部单位面积上的[内力](@entry_id:167605)[分布](@entry_id:182848)。在没有[体力](@entry_id:174230)（如重力）的情况下，二维笛卡尔坐标系 $(x, y)$ 中的静态平衡[微分方程](@entry_id:264184)（或称柯西-[欧拉方程](@entry_id:177914)）表达为：

$$
\begin{align*}
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} = 0 \\
\frac{\partial \sigma_{yx}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} = 0
\end{align*}
$$

其中 $\sigma_{xx}$ 和 $\sigma_{yy}$ 是正应力分量，$\sigma_{xy}$ 和 $\sigma_{yx}$ 是剪应力分量。在经典柯西连续介质理论中，若不存在体力矩或[力偶应力](@entry_id:747952)，动量矩[守恒定律](@entry_id:269268)将导致应力张量是对称的，即 $\sigma_{xy} = \sigma_{yx}$。因此，上述两个[平衡方程](@entry_id:172166)可以写为：

$$
\begin{align}
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} = 0 \label{eq:equil1} \\
\frac{\partial \sigma_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} = 0 \label{eq:equil2}
\end{align}
$$

当存在[体力](@entry_id:174230) $\boldsymbol{b} = (b_x, b_y)$（单位体积上的力）时，[平衡方程](@entry_id:172166)则变为：

$$
\begin{align*}
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} + b_x = 0 \\
\frac{\partial \sigma_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + b_y = 0
\end{align*}
$$

值得注意的是，这些[平衡方程](@entry_id:172166)是在当前构型下精确成立的，其本身并不依赖于小变形假设 [@problem_id:2866208]。

#### 几何关系：应变与协调性

弹性体的变形由位移场 $\boldsymbol{u}(x, y) = (u(x, y), v(x, y))$ 描述。在[线性弹性力学](@entry_id:166983)中，我们采用**小变形假设**，即[位移梯度](@entry_id:165352)远小于1 ($|\partial u_i / \partial x_j| \ll 1$)。在此假设下，应变与位移之间的几何关系（或称运动学关系）简化为：

$$
\varepsilon_{xx} = \frac{\partial u}{\partial x}, \quad \varepsilon_{yy} = \frac{\partial v}{\partial y}, \quad \varepsilon_{xy} = \frac{1}{2} \left( \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x} \right)
$$

这里，$\varepsilon_{xx}$ 和 $\varepsilon_{yy}$ 是[正应变](@entry_id:204633)，$\varepsilon_{xy}$ 是张量[剪应变](@entry_id:175241)。工程实践中也常用**工程[剪应变](@entry_id:175241)** $\gamma_{xy} = 2\varepsilon_{xy} = \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x}$。

由于三个应变分量（$\varepsilon_{xx}$, $\varepsilon_{yy}$, $\varepsilon_{xy}$）是由两个位移分量（$u$, $v$）导出的，它们之间并非[相互独立](@entry_id:273670)。为了保证一个给定的应变场能够积分得到一个单值、连续的位移场，该应变场必须满足一个约束条件，即**[圣维南协调方程](@entry_id:754487) (Saint-Venant compatibility condition)**。通过对[应变-位移关系](@entry_id:173321)式进行[微分](@entry_id:158718)消去 $u$ 和 $v$，我们可以在二维情况下得到如下的协调方程 [@problem_id:2614048]：

$$
\frac{\partial^2 \varepsilon_{xx}}{\partial y^2} + \frac{\partial^2 \varepsilon_{yy}}{\partial x^2} = 2 \frac{\partial^2 \varepsilon_{xy}}{\partial x \partial y}
$$

若使用工程[剪应变](@entry_id:175241) $\gamma_{xy}$，该方程则写为：

$$
\frac{\partial^2 \varepsilon_{xx}}{\partial y^2} + \frac{\partial^2 \varepsilon_{yy}}{\partial x^2} = \frac{\partial^2 \gamma_{xy}}{\partial x \partial y}
$$

协调方程是一个纯粹的运动学约束，它保证了变形的几何相容性。

#### [本构关系](@entry_id:186508)：[平面应力与平面应变](@entry_id:172357)

[本构关系](@entry_id:186508)描述了材料的力学响应，即[应力与应变](@entry_id:137374)之间的关系。对于均匀、各向同性的线弹性材料，该关系由[胡克定律](@entry_id:149682)给出。在二维问题中，通常考虑两种简化模型：

1.  **平面应力 (Plane Stress)**: 适用于薄板问题，假设垂直于平面的应力分量为零，即 $\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0$。此时，面内应变与应力的关系为：
    $$
    \varepsilon_{xx} = \frac{1}{E}(\sigma_{xx} - \nu \sigma_{yy}), \quad \varepsilon_{yy} = \frac{1}{E}(\sigma_{yy} - \nu \sigma_{xx}), \quad \gamma_{xy} = \frac{2(1+\nu)}{E} \sigma_{xy}
    $$
    其中 $E$ 是[杨氏模量](@entry_id:140430)，$\nu$ 是[泊松比](@entry_id:158876)。在这种情况下，面外应变通常不为零：$\varepsilon_{zz} = -\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy})$ [@problem_id:2866246]。

2.  **[平面应变](@entry_id:167046) (Plane Strain)**: 适用于长柱体问题，假设垂直于平面的应变分量为零，即 $\varepsilon_{zz} = \varepsilon_{xz} = \varepsilon_{yz} = 0$。此时，面[内应力](@entry_id:193721)会引起一个面外正应力 $\sigma_{zz} = \nu(\sigma_{xx} + \sigma_{yy})$。面内应变与应力的关系变为：
    $$
    \varepsilon_{xx} = \frac{1-\nu^2}{E} \sigma_{xx} - \frac{\nu(1+\nu)}{E} \sigma_{yy}, \quad \varepsilon_{yy} = \frac{1-\nu^2}{E} \sigma_{yy} - \frac{\nu(1+\nu)}{E} \sigma_{xx}, \quad \gamma_{xy} = \frac{2(1+\nu)}{E} \sigma_{xy}
    $$

### [艾里应力函数](@entry_id:191331)：一种巧妙的求解策略

在求解弹性力学问题时，我们通常需要同时处理多个未知量和方程。[艾里应力函数](@entry_id:191331)的引入，旨在通过一种巧妙的代换，大幅简化这个问题。

#### 引入势函数以满足平衡方程

[艾里应力函数](@entry_id:191331)的核心思想是引入一个标量势函数 $\phi(x, y)$，使得应力分量由它的[二阶偏导数](@entry_id:635213)表示。对于无体力的情况，应力分量定义如下 [@problem_id:2866237]：

$$
\sigma_{xx} = \frac{\partial^2 \phi}{\partial y^2}, \quad \sigma_{yy} = \frac{\partial^2 \phi}{\partial x^2}, \quad \sigma_{xy} = -\frac{\partial^2 \phi}{\partial x \partial y}
$$

这一代换的精妙之处在于，它能**自动满足**[平衡方程](@entry_id:172166)。我们将上述定义代入[平衡方程](@entry_id:172166) (\ref{eq:equil1}) 和 (\ref{eq:equil2})：

$$
\frac{\partial}{\partial x} \left( \frac{\partial^2 \phi}{\partial y^2} \right) + \frac{\partial}{\partial y} \left( -\frac{\partial^2 \phi}{\partial x \partial y} \right) = \frac{\partial^3 \phi}{\partial x \partial y^2} - \frac{\partial^3 \phi}{\partial y \partial x \partial y} = 0
$$

$$
\frac{\partial}{\partial x} \left( -\frac{\partial^2 \phi}{\partial x \partial y} \right) + \frac{\partial}{\partial y} \left( \frac{\partial^2 \phi}{\partial x^2} \right) = -\frac{\partial^3 \phi}{\partial x^2 \partial y} + \frac{\partial^3 \phi}{\partial y \partial x^2} = 0
$$

根据[克莱罗定理](@entry_id:139814) (Clairaut's theorem)，只要函数 $\phi$ 足够光滑（至少具有三阶连续偏导数），其[混合偏导数](@entry_id:139334)的求导次序无关。因此，上述两个等式恒成立。这意味着，对于任意一个足够光滑的标量函数 $\phi(x,y)$，通过上述定义生成的应[力场](@entry_id:147325)都天然地满足平衡要求。

这样，两个关于三个应力分量的[偏微分方程](@entry_id:141332)就被一个标量函数 $\phi$ 的定义所取代。求解问题的核心不再是寻找满足平衡的应[力场](@entry_id:147325)，而是寻找一个合适的[艾里应力函数](@entry_id:191331) $\phi$。

这种[势函数](@entry_id:176105)的表示方法的存在性，在数学上与向量场的[亥姆霍兹分解](@entry_id:181767)有关。对于无体力的情况，平衡方程意味着[应力张量](@entry_id:148973)的每一行（或每一列）都是一个[无散场](@entry_id:260932)。在**单连通区域 (simply connected domain)** 内，这样的场可以表示为另一个场的旋度，这正是[艾里函数](@entry_id:198690)表示法所利用的原理 [@problem_id:2866205]。

#### [双调和方程](@entry_id:165706)：协调性的体现

既然[平衡方程](@entry_id:172166)已被自动满足，我们剩下的任务就是确保由 $\phi$ 导出的应[力场](@entry_id:147325)能够对应一个几何上可能的变形，即满足[应变协调方程](@entry_id:195003)。这一步将[运动学](@entry_id:173318)约束和本构关系引入问题中，并最终给出了 $\phi$ 必须满足的控制方程。

推导过程如下 [@problem_id:2687282]：
1.  **将协调方程用应力表示**：我们将[胡克定律](@entry_id:149682)（无论是平面应力还是平面应变形式）代入[应变协调方程](@entry_id:195003)。以[平面应力](@entry_id:172193)为例：
    $$
    \frac{\partial^2}{\partial y^2} \left[ \frac{1}{E}(\sigma_{xx} - \nu \sigma_{yy}) \right] + \frac{\partial^2}{\partial x^2} \left[ \frac{1}{E}(\sigma_{yy} - \nu \sigma_{xx}) \right] = \frac{\partial^2}{\partial x \partial y} \left[ \frac{2(1+\nu)}{E} \sigma_{xy} \right]
    $$

2.  **化简**：对于均匀材料（$E$ 和 $\nu$ 是常数），我们可以将它们提到[微分算子](@entry_id:140145)之外并乘以 $E$。经过一系列[微分](@entry_id:158718)和代数运算，并利用平衡方程可以证明，最终可以将应力形式的协调方程简化为一个非常简洁的形式，即[应力张量](@entry_id:148973)的迹是一个**调和函数 (harmonic function)**：
    $$
    \left( \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2} \right) (\sigma_{xx} + \sigma_{yy}) = \nabla^2 (\sigma_{xx} + \sigma_{yy}) = 0
    $$

3.  **代入艾里函数定义**：最后，我们将[艾里函数](@entry_id:198690)的定义代入上式。注意到：
    $$
    \sigma_{xx} + \sigma_{yy} = \frac{\partial^2 \phi}{\partial y^2} + \frac{\partial^2 \phi}{\partial x^2} = \nabla^2 \phi
    $$
    其中 $\nabla^2$ 是[拉普拉斯算子](@entry_id:146319)。于是，协调方程最终转化为关于[艾里应力函数](@entry_id:191331) $\phi$ 的一个[四阶偏微分方程](@entry_id:176247)：
    $$
    \nabla^2 (\nabla^2 \phi) = \nabla^4 \phi = \frac{\partial^4 \phi}{\partial x^4} + 2 \frac{\partial^4 \phi}{\partial x^2 \partial y^2} + \frac{\partial^4 \phi}{\partial y^4} = 0
    $$

这个方程被称为**[双调和方程](@entry_id:165706)**。令人瞩目的是，对于均匀、各向同性的线弹性材料，在无体力的情况下，无论是[平面应力](@entry_id:172193)还是平面应变问题，最终的控制方程都是同一个——[双调和方程](@entry_id:165706) [@problem_id:2866246]。这揭示了[艾里函数](@entry_id:198690)方法深刻的普适性。问题的全部复杂性——包括平衡、协调和[本构关系](@entry_id:186508)——都被封装在了求解这个单一的标量PDE中。

### 使用艾里函数求解边值问题

将一个弹性力学问题转化为求解[双调和方程](@entry_id:165706) $\nabla^4 \phi = 0$ 后，我们还需要为 $\phi$ 设定合适的边界条件，这些条件源于物体边界上施加的物理约束。

#### 边界条件

边界条件通常分为两类：[位移边界条件](@entry_id:203261)和力（或称牵[引力](@entry_id:175476)）边界条件。对于艾里函数，力边界条件有更直接的表达。

考虑边界 $\partial\Omega$ 上的一段，其弧长坐标为 $s$。可以证明，边界上的牵[引力](@entry_id:175476)向量 $\boldsymbol{t} = (t_x, t_y)$ 与[艾里应力函数](@entry_id:191331)的一阶[偏导数](@entry_id:146280)沿边界弧长的变化率直接相关 [@problem_id:2866219]：
$$
\frac{d}{ds}\left(\frac{\partial \phi}{\partial x}\right) = -t_y, \quad \frac{d}{ds}\left(\frac{\partial \phi}{\partial y}\right) = t_x
$$
通过对这些关系沿边界进行积分，我们可以将规定的边界牵[引力](@entry_id:175476)（力的边界条件）转化为对 $\phi$ 及其梯度 $\nabla\phi$ 在边界上的约束。例如，沿边界从点 A 到点 B 积分，可以确定 $\nabla\phi$ 在 B 点相对于在 A 点的值。这些构成了求解[双调和方程](@entry_id:165706)的**自然边界条件 (natural boundary conditions)**。

#### [解的唯一性](@entry_id:143619)与[适定性](@entry_id:148590)

[艾里应力函数](@entry_id:191331) $\phi$ 自身并不是唯一的。考察艾里函数的定义式可以发现，如果给 $\phi$ 加上一个任意的[仿射函数](@entry_id:635019)（一次多项式） $f(x, y) = ax + by + c$，其中 $a, b, c$ 为常数，那么新的应力函数 $\tilde{\phi} = \phi + f$ 所对应的应力分量与原来完全相同 [@problem_id:2866221]：

$$
\Delta \sigma_{xx} = \frac{\partial^2 f}{\partial y^2} = 0, \quad \Delta \sigma_{yy} = \frac{\partial^2 f}{\partial x^2} = 0, \quad \Delta \sigma_{xy} = -\frac{\partial^2 f}{\partial x \partial y} = 0
$$

这意味着，[艾里应力函数](@entry_id:191331)在确定应[力场](@entry_id:147325)时，存在一个**仿射不确定性 (affine indeterminacy)**。这个不确定性对应三个自由度（$a, b, c$），在求解 $\phi$ 的[边值问题](@entry_id:193901)时必须通过施加额外的约束来消除，例如在边界某一点固定 $\phi$ 及其梯度 $\nabla \phi$ 的值。

更深层次地，一个适定的牵[引力](@entry_id:175476)边值问题的解的存在性，依赖于施加的边界牵[引力](@entry_id:175476)本身满足**全局平衡条件**。即，作用在整个边界上的总主矢和总主矩必须为零 [@problem_id:2866241]：

$$
\int_{\partial\Omega} \boldsymbol{t} \, \mathrm{d}s = \boldsymbol{0}, \quad \int_{\partial\Omega} (\boldsymbol{r} \times \boldsymbol{t}) \cdot \boldsymbol{e}_z \, \mathrm{d}s = 0
$$

其中 $\boldsymbol{t}$ 是边界牵[引力](@entry_id:175476)，$\boldsymbol{r}$ 是位置向量。这些条件是物体保持静态平衡的物理必然要求。从数学上看，它们保证了[艾里函数](@entry_id:198690) $\phi$ 及其[一阶导数](@entry_id:749425)是单值的。在满足这些条件的区域上，对于给定的牵[引力](@entry_id:175476)数据，[双调和方程](@entry_id:165706)存在一个解，且该解在相差一个[仿射函数](@entry_id:635019)的意义下是唯一的。

### 扩展与推广

[艾里应力函数](@entry_id:191331)方法虽然强大，但其经典形式主要适用于特定情况。了解其适用范围的边界和推广的可能性至关重要。

#### [体力](@entry_id:174230)的影响

当存在体力 $\boldsymbol{b}=(b_x, b_y)$ 时，经典的艾里函数定义不再能自动满足非齐次的[平衡方程](@entry_id:172166)。一种处理方法是，如果体力是**保守的**，即可以写成一个[势函数](@entry_id:176105) $V$ 的梯度（$\boldsymbol{b} = -\nabla V$），则可以通过修正[艾里函数](@entry_id:198690)的定义来纳入[体力](@entry_id:174230)的影响。例如，定义 $\sigma_{xx} = \frac{\partial^2 \phi}{\partial y^2} + V$ 和 $\sigma_{yy} = \frac{\partial^2 \phi}{\partial x^2} + V$。此时，[平衡方程](@entry_id:172166)得到满足，但控制方程 $\nabla^4\phi$ 的右端将出现与 $V$ 相关的非齐次项。

#### 各向异性材料

[艾里应力函数](@entry_id:191331)作为满足[平衡方程](@entry_id:172166)的[势函数](@entry_id:176105)，其存在性仅依赖于[静力平衡](@entry_id:163498)，而与材料的本构性质无关。因此，对于**[各向异性材料](@entry_id:184874)**，我们仍然可以采用艾里函数来表示应力。然而，当我们将各向异性的[本构关系](@entry_id:186508)代入[应变协调方程](@entry_id:195003)时，最终得到的关于 $\phi$ 的控制方程将不再是简单的[双调和方程](@entry_id:165706)，而是一个更复杂的四阶线性椭圆型[偏微分方程](@entry_id:141332)，其系数与材料的弹性常数有关 [@problem_id:2866205]。

#### 从二维到三维：贝尔特拉米应力函数

将艾里函数直接推广到三维是不可行的。一个关键的原因在于自由度的不匹配 [@problem_id:2866234]。在三维空间中，对称的应力张量有6个独立分量，而平衡方程有3个。因此，一个一般的自平衡应[力场](@entry_id:147325)应由 $6-3=3$ 个独立的标量函数来参数化。而单个标量势函数 $\phi(x,y,z)$ 仅提供一个自由度，不足以描述一般的应力状态。

三维弹性力学中与[艾里函数](@entry_id:198690)思想对应的是**贝尔特拉米-米切尔 (Beltrami-Michell) 应力函数**。这需要引入一个对称的**[二阶张量](@entry_id:199780)势函数** $\boldsymbol{\Phi}$。[应力张量](@entry_id:148973)可以通过对 $\boldsymbol{\Phi}$ 进行二次旋度运算得到：

$$
\sigma_{ij} = \epsilon_{ik\ell} \epsilon_{jmn} \partial_k \partial_m \Phi_{\ell n}
$$

其中 $\epsilon_{ijk}$ 是[列维-奇维塔符号](@entry_id:193594)。这个表示法自动满足了应力[张量的对称性](@entry_id:202126)和无散性（即平衡方程）。张量势 $\boldsymbol{\Phi}$ 有6个分量，但在扣除[规范自由度](@entry_id:160491)后，恰好剩下3个独立的函数，与所需的自由度相符。在各向同性材料中，施加协调条件和适当的[规范条件](@entry_id:749730)后，每个[势函数](@entry_id:176105)分量 $\Phi_{ij}$ 也都满足[双调和方程](@entry_id:165706) $\nabla^4 \Phi_{ij} = 0$。这是[艾里函数](@entry_id:198690)思想在三维空间中的深刻而优美的推广。