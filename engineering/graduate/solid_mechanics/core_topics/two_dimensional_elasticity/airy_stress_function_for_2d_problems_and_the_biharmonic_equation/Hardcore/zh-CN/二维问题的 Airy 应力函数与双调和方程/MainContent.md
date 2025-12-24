## 引言
在固体力学的广阔领域中，求解弹性体的应力[分布](@entry_id:182848)是核心任务之一。然而，直接求解描述应[力平衡](@entry_id:267186)、几何协调和材料本构的[耦合偏微分方程组](@entry_id:198181)通常极其复杂。为了应对这一挑战，力学家们发展了多种精巧的数学方法，其中，[艾里应力函数](@entry_id:191331)（Airy Stress Function）无疑是解决二维弹性力学问题最强大、最优雅的工具之一。它巧妙地将满足一组方程的难题，转化为求解一个更高阶但单一的标量方程。

本文旨在系统性地介绍[艾里应力函数](@entry_id:191331)法及其在现代工程与科学研究中的核心地位。文章将引领读者深入理解这一方法的理论精髓，并探索其在解决实际问题中的巨大威力。

在接下来的内容中，我们将首先在“原理与机制”一章中，从基本定义出发，阐明[艾里应力函数](@entry_id:191331)如何自动满足[平衡方程](@entry_id:172166)，并详细推导其如何与协调方程及[本构关系](@entry_id:186508)结合，最终形成著名的双谐和方程。随后，在“应用与跨学科联系”一章，我们将展示该理论如何被用于分析工程中的关键现象，如孔口周围的应力集中、裂纹尖端的[应力奇异性](@entry_id:166362)，并探讨其与板弯曲理论、[流体力学](@entry_id:136788)等其他物理领域之间惊人的数学类比。最后，在“动手实践”部分，读者将有机会通过解决一系列精心设计的练习题，将理论知识转化为解决实际问题的能力。

## 原理与机制

在二维弹性力学问题的求解中，Airy 应力函数法是一种极为巧妙且强大的解析工具。该方法的核心思想在于引入一个[标量势](@entry_id:276177)函数，即 Airy 应力函数，通过对其求导来构造应力分量，从而自动满足[平衡方程](@entry_id:172166)。这样，原本需要求解多个耦合[偏微分方程](@entry_id:141332)的复杂问题，被转化为求解一个关于该标量函数的单一高阶[偏微分方程](@entry_id:141332)。本章将系统阐述 Airy 应力函数法的基本原理、控制方程的推导、[叠加原理的应用](@entry_id:266111)，以及在处理边界条件、体力、[多连通域](@entry_id:185277)等复杂情况下的推广和机制。

### Airy 应力函数与平衡方程的自动满足

在二维问题中，若不考虑[体力](@entry_id:174230)，一个处于静态平衡状态的物体，其内部任一点的应力分量必须满足如下的平衡[微分方程](@entry_id:264184)：

$$
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} = 0
$$
$$
\frac{\partial \sigma_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} = 0
$$

这些方程构成了求解弹性力学问题的基本约束之一。Airy 应力函数法的精髓在于，它引入一个标量函数 $\phi(x,y)$，并用如下方式定义应力分量：

$$
\sigma_{xx} = \frac{\partial^2\phi}{\partial y^2}, \quad \sigma_{yy} = \frac{\partial^2\phi}{\partial x^2}, \quad \sigma_{xy} = -\frac{\partial^2\phi}{\partial x \partial y}
$$

这组定义的巧妙之处在于，只要函数 $\phi$ 具有足够的光滑性（至少是三阶连续可导，即 $C^3$ 类函数），它所定义的应[力场](@entry_id:147325)就能自动地、恒等地满足平衡方程。我们可以通过直接代入来验证这一点 。

对于第一个[平衡方程](@entry_id:172166)：
$$
\frac{\partial}{\partial x}\left(\frac{\partial^2\phi}{\partial y^2}\right) + \frac{\partial}{\partial y}\left(-\frac{\partial^2\phi}{\partial x \partial y}\right) = \frac{\partial^3\phi}{\partial x \partial y^2} - \frac{\partial^3\phi}{\partial y \partial x \partial y}
$$
根据[克莱罗定理](@entry_id:139814)（Clairaut's theorem），对于[光滑函数](@entry_id:267124)，[混合偏导数](@entry_id:139334)的求导次序无关，因此 $\frac{\partial^3\phi}{\partial y \partial x \partial y} = \frac{\partial^3\phi}{\partial x \partial y^2}$。于是上式变为 $0$，第一个平衡方程恒成立。

对于第二个平衡方程：
$$
\frac{\partial}{\partial x}\left(-\frac{\partial^2\phi}{\partial x \partial y}\right) + \frac{\partial}{\partial y}\left(\frac{\partial^2\phi}{\partial x^2}\right) = -\frac{\partial^3\phi}{\partial x^2 \partial y} + \frac{\partial^3\phi}{\partial y \partial x^2}
$$
同样由于求导次序可以交换，上式也恒为 $0$。

因此，通过引入 Airy 应力函数，我们将满足平衡方程这一约束“内嵌”到了应力分量的定义之中。这使得我们不必再直接处理平衡方程，从而极大地简化了问题的数学结构。问题的核心随之转化为：这个[势函数](@entry_id:176105) $\phi$ 本身需要满足什么条件，才能确保其导出的应[力场](@entry_id:147325)不仅满足平衡，还能对应一个物理上可能的变形状态？

### 双谐方程：协调性、运动学与[本构关系](@entry_id:186508)的融合

一个物理上可能的变形状态，要求由应[力场](@entry_id:147325)通过本构关系计算出的应变场必须是**协调的**。所谓协调，是指该应变场可以从一个单值的、连续的[位移场](@entry_id:141476)中导出。

首先，我们回顾描述物体变形的**运动学关系**。在小变形假设下，应变张量的分量与[位移场](@entry_id:141476) $(u(x,y), v(x,y))$ 的关系为：

$$
\varepsilon_{xx} = \frac{\partial u}{\partial x}, \quad \varepsilon_{yy} = \frac{\partial v}{\partial y}, \quad \gamma_{xy} = 2\varepsilon_{xy} = \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x}
$$

这里，$\varepsilon_{ij}$ 是张量应变分量，而 $\gamma_{xy}$ 是工程[剪应变](@entry_id:175241) 。由于三个应变分量是由两个位移分量通过[微分](@entry_id:158718)得到的，它们之间并非[相互独立](@entry_id:273670)。通过对上述运动学关系式进行[微分](@entry_id:158718)并消去位移分量 $u$ 和 $v$，我们可以得到一个只包含应变分量的约束方程，即**[圣维南协调方程](@entry_id:754487)**（Saint-Venant compatibility condition）。在二维情况下，它具有如下形式：

$$
\frac{\partial^2\varepsilon_{xx}}{\partial y^2} + \frac{\partial^2\varepsilon_{yy}}{\partial x^2} = \frac{\partial^2\gamma_{xy}}{\partial x \partial y} \quad \text{或} \quad \frac{\partial^2\varepsilon_{xx}}{\partial y^2} + \frac{\partial^2\varepsilon_{yy}}{\partial x^2} = 2\frac{\partial^2\varepsilon_{xy}}{\partial x \partial y}
$$

此方程确保了应变场可以被积分为一个单值的位移场 。

接下来，我们需要引入连接[应力与应变](@entry_id:137374)的桥梁——**本构关系**。对于均匀、各向同性的线弹性材料，其本构关系由胡克定律描述。在二维情况下，我们需要区分**平面应力**（薄板问题，$\sigma_{zz}=0$）和**[平面应变](@entry_id:167046)**（长柱体问题，$\varepsilon_{zz}=0$）两种状态。

对于**平面应力**状态，应变与应力的关系为：
$$
\varepsilon_{xx} = \frac{1}{E}(\sigma_{xx} - \nu \sigma_{yy}), \quad \varepsilon_{yy} = \frac{1}{E}(\sigma_{yy} - \nu \sigma_{xx}), \quad \gamma_{xy} = \frac{2(1+\nu)}{E}\sigma_{xy}
$$

对于**[平面应变](@entry_id:167046)**状态，[应力与应变](@entry_id:137374)的关系更为常用：
$$
\sigma_{xx} = \frac{E}{(1+\nu)(1-2\nu)}\left[(1-\nu)\varepsilon_{xx} + \nu\varepsilon_{yy}\right], \quad \sigma_{yy} = \frac{E}{(1+\nu)(1-2\nu)}\left[\nu\varepsilon_{xx} + (1-\nu)\varepsilon_{yy}\right], \quad \sigma_{xy} = \frac{E}{2(1+\nu)}\gamma_{xy}
$$
其中 $E$ 是杨氏模量，$\nu$ 是泊松比 。

现在，我们可以将所有部分整合起来。我们将 Airy 函数定义的应力分量代入[本构关系](@entry_id:186508)，得到用 $\phi$ 的[二阶导数](@entry_id:144508)表示的应变分量。然后，再将这些应变表达式代入协调方程。以[平面应力](@entry_id:172193)为例 ：

将 $\sigma_{xx} = \phi_{,yy}$ 和 $\sigma_{yy} = \phi_{,xx}$ 等代入[平面应力](@entry_id:172193)[本构关系](@entry_id:186508)，得到：
$$
\varepsilon_{xx} = \frac{1}{E}(\phi_{,yy} - \nu \phi_{,xx}), \quad \varepsilon_{yy} = \frac{1}{E}(\phi_{,xx} - \nu \phi_{,yy}), \quad \gamma_{xy} = -\frac{2(1+\nu)}{E}\phi_{,xy}
$$
将这些代入协调方程 $\frac{\partial^2\varepsilon_{xx}}{\partial y^2} + \frac{\partial^2\varepsilon_{yy}}{\partial x^2} = \frac{\partial^2\gamma_{xy}}{\partial x \partial y}$，经过整理和化简，我们最终得到一个关于 $\phi$ 的[四阶偏微分方程](@entry_id:176247)：

$$
\frac{\partial^4\phi}{\partial x^4} + 2\frac{\partial^4\phi}{\partial x^2 \partial y^2} + \frac{\partial^4\phi}{\partial y^4} = 0
$$

这个方程可以被紧凑地写为 $\nabla^4\phi = 0$ 或 $\nabla^2(\nabla^2\phi) = 0$，其中 $\nabla^2 = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2}$ 是拉普拉斯算子。这个方程被称为**双谐方程**（Biharmonic Equation）。

值得注意的是，对于[平面应变](@entry_id:167046)问题，采用类似但稍有不同的推导过程，最终也会得到相同的双谐方程 $\nabla^4\phi=0$。这表明，在没有体力的情况下，对于均匀[各向同性线弹性](@entry_id:185899)体，无论是平面应力还是平面应变问题，其 Airy 应力函数都必须是双谐函数。求解弹性力学问题从而转化为：在给定的边界条件下，求解双谐方程。

### 线性与叠加原理

双谐方程 $\nabla^4\phi = 0$ 是一个线性、齐次的[偏微分方程](@entry_id:141332)。这一线性特性带来了极其重要且实用的性质——**叠加原理**（Principle of Superposition）。

[叠加原理](@entry_id:144649)指出，如果 $\phi_1$ 和 $\phi_2$ 都是双谐方程的解，那么它们的任意线性组合 $\phi = c_1\phi_1 + c_2\phi_2$（其中 $c_1$ 和 $c_2$ 为常数）也必然是双谐方程的解 。这是因为[微分算子](@entry_id:140145) $\nabla^4$ 是线性算子：
$$
\nabla^4(c_1\phi_1 + c_2\phi_2) = c_1\nabla^4\phi_1 + c_2\nabla^4\phi_2 = c_1(0) + c_2(0) = 0
$$

由于应力分量和边界上的面力也是通过对 $\phi$ 的线性[微分](@entry_id:158718)运算得到的，因此[叠加原理](@entry_id:144649)同样适用于应[力场](@entry_id:147325)和面[力场](@entry_id:147325)。即，由 $\phi_1$ 和 $\phi_2$ 产生的应[力场](@entry_id:147325)分别为 $\boldsymbol{\sigma}_1$ 和 $\boldsymbol{\sigma}_2$，则由 $\phi = c_1\phi_1 + c_2\phi_2$ 产生的应[力场](@entry_id:147325)就是 $\boldsymbol{\sigma} = c_1\boldsymbol{\sigma}_1 + c_2\boldsymbol{\sigma}_2$。如果 $\phi_1$ 和 $\phi_2$ 在同一边界上产生的面力均为零，那么它们的[线性组合](@entry_id:154743)在该边界上产生的面力也必然为零 。

叠加原理使得我们可以将一个复杂的[问题分解](@entry_id:272624)为若干个更简单的子问题的和。例如，一个同时承受拉伸和弯曲的梁，其应[力场](@entry_id:147325)可以看作是一个纯拉伸状态的应[力场](@entry_id:147325)和一个[纯弯曲](@entry_id:202969)状态的应[力场](@entry_id:147325)的叠加。在 Airy 函数的框架下，一个简单的[单轴拉伸](@entry_id:188287)应力 $\sigma_{xx}=T$ 可由 $\phi_1 = \frac{T}{2}y^2$ 产生，而一个线性变化的弯曲应力 $\sigma_{xx}=Ky$ 可由 $\phi_2 = \frac{K}{6}y^3$ 产生。这两个函数都是双谐函数（任何次数不高于3的多项式都是双谐函数）。因此，它们的和 $\phi = \frac{T}{2}y^2 + \frac{K}{6}y^3$ 就给出了组合应[力场](@entry_id:147325) $\sigma_{xx} = T+Ky$ 的解 。

然而，必须强调的是，叠加原理仅适用于线性量。对于[应变能](@entry_id:162699)这类二次量，叠加原理不成立。一个组合状态的[应变能](@entry_id:162699) $U$ 并不等于各个子状态应变能的简单加和，而是包含了一个**交互能**项 $U_{12}$：
$$
U(\phi_1+\phi_2) = U(\phi_1) + U(\phi_2) + U_{12}
$$
其中 $U_{12} = \int_A \boldsymbol{\sigma}_1 : \boldsymbol{\varepsilon}_2 \, dA$，这里 $\boldsymbol{\varepsilon}_2$ 是由 $\boldsymbol{\sigma}_2$ 产生的应变场 。

叠加原理的根基在于整个弹性力学系统（包括[运动学](@entry_id:173318)、平衡方程和[本构关系](@entry_id:186508)）的线性。一旦引入[非线性](@entry_id:637147)因素，例如**[几何非线性](@entry_id:169896)**（即大变形或大转动），运动学关系就不再是线性的，此时叠加原理将失效。在这种情况下，两个解的和不再是一个解 。不过，值得一提的是，在[非线性力学](@entry_id:178303)中，可以通过在某个已知的变形状态附近进行**增量分析**，将问题线性化。对于这个线性化的增量问题，叠加原理可以被重新应用 。

### 唯一性与边界条件

在应用 Airy 函数法解决具体问题时，两个核心议题是[解的唯一性](@entry_id:143619)和边界条件的施加。

#### [解的唯一性](@entry_id:143619)

弹性力学理论保证，对于一个[适定问题](@entry_id:176268)，其应[力场](@entry_id:147325)是唯一的。那么，这对应力函数 $\phi$ 意味着什么呢？由于应力分量是由 $\phi$ 的[二阶导数](@entry_id:144508)定义的，任何一个[二阶导数](@entry_id:144508)全为零的函数，即使加到 $\phi$ 上，也不会改变最终的应[力场](@entry_id:147325)。满足这一条件的函数是形如 $ax+by+c$ 的**[仿射函数](@entry_id:635019)**（affine function），其中 $a, b, c$ 为任意常数。

因此，Airy 应力函数 $\phi$ 的解不是绝对唯一的，而是在相差一个任意[仿射函数](@entry_id:635019)的意义下是唯一的。这个[仿射函数](@entry_id:635019)集合构成了从 $\phi$ 到[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的[线性算子](@entry_id:149003)的**核**（kernel） 。在实际求解中，这个不确定性通常可以通过设定 $\phi$ 及其[一阶导数](@entry_id:749425)在某一点的值来消除，但这对于应力结果没有影响。

#### 边界条件

弹性力学问题的边界条件通常分为两类：

1.  **自然边界条件（静力边界条件）**：在边界上给定面力（traction）。设边界上的外[法线](@entry_id:167651)向量为 $\boldsymbol{n}=(n_x, n_y)$，则面力分量为 $t_x = \sigma_{xx}n_x + \sigma_{xy}n_y$ 和 $t_y = \sigma_{xy}n_x + \sigma_{yy}n_y$。将 Airy 函数的定义代入，面力就可以表示为 $\phi$ 的导数。例如，对于一条位于 $y=0$ 的直边界，其外[法线](@entry_id:167651)为 $\boldsymbol{n}=(0,1)$，则法向面力 $t_n = \sigma_{yy}$，切向面力 $t_s = \sigma_{xy}$。用 $\phi$ 表示即为 ：
    $$
    t_n(x) = \sigma_{yy}(x,0) = \frac{\partial^2\phi}{\partial x^2}\bigg|_{y=0}
    $$
    $$
    t_s(x) = \sigma_{xy}(x,0) = -\frac{\partial^2\phi}{\partial x \partial y}\bigg|_{y=0}
    $$
    可见，[面力边界条件](@entry_id:167112)转化为 $\phi$ 及其导数在边界上的**局部**（pointwise）条件，在数学上相对容易处理。

2.  **本质边界条件（几何边界条件）**：在边界上给定各点的位移。这类边界条件在 Airy 函数框架下处理起来要复杂得多。[位移场](@entry_id:141476) $(u,v)$ 无法直接由 $\phi$ 的局部值得到，而是需要通过对应变场进行积分。具体来说，首先由 $\phi$ 计算应力，再由[本构关系](@entry_id:186508)计算应变，最后对运动学关系进行积分才能得到位移。例如：
    $$
    u(x,y) = \int \varepsilon_{xx} \, dx + f(y) = \int \frac{1}{E}\left(\frac{\partial^2\phi}{\partial y^2} - \nu \frac{\partial^2\phi}{\partial x^2}\right) dx + f(y)
    $$
    因此，在边界上指定位移，相当于对 $\phi$ 施加了一种**非局部的、积分形式的约束**，这通常比处理[面力边界条件](@entry_id:167112)更为困难 。

### 推广与高等论题

Airy 应力函数法可以被推广以处理更复杂的情况，例如包含体力、[曲线坐标系](@entry_id:172561)和[多连通域](@entry_id:185277)等问题。

#### 体力的处理

标准的 Airy 函数定义仅适用于没有[体力](@entry_id:174230)的情况。当存在体力（如重力）$\boldsymbol{b}=(b_x, b_y)$ 时，平衡方程变为非齐次形式：$\sigma_{ij,j} + b_i = 0$。此时，直接套用标准定义将不再满足[平衡方程](@entry_id:172166) 。

正确的处理方法是利用叠加原理。我们将总应[力场](@entry_id:147325) $\boldsymbol{\sigma}$ 分解为一个**特解** $\boldsymbol{\sigma}^p$ 和一个**齐次解** $\boldsymbol{\sigma}^h$ 的和，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^h + \boldsymbol{\sigma}^p$。其中，特解 $\boldsymbol{\sigma}^p$ 只需要满足非齐次的平衡方程 $\sigma^p_{ij,j} + b_i = 0$，而无需满足协调性。齐次解 $\boldsymbol{\sigma}^h$ 则满足齐次平衡方程 $\sigma^h_{ij,j} = 0$。我们对这个[齐次解](@entry_id:274365) $\boldsymbol{\sigma}^h$ 使用 Airy 应力函数表示。

如果体力是保守的，即可以表示为一个势函数 $U$ 的负梯度（$\boldsymbol{b}=-\nabla U$），那么可以采用修正的 Airy 函数定义。例如，将应力分量定义为 $\sigma_{xx}=\frac{\partial^{2}\phi}{\partial y^{2}}+U$, $\sigma_{yy}=\frac{\partial^{2}\phi}{\partial x^{2}}+U$ 和 $\sigma_{xy}=-\frac{\partial^{2}\phi}{\partial x \partial y}$，即可自动满足包含[体力](@entry_id:174230)的[平衡方程](@entry_id:172166) $\sigma_{ij,j}+b_i=0$ 。无论采用哪种方法，最终 Airy 函数 $\phi$ 所满足的方程将变为一个**非齐次的双谐方程**，形如 $\nabla^4\phi = F(\boldsymbol{b})$，其中 $F$ 是一个与[体力](@entry_id:174230)相关的函数。需要明确的是，[体力](@entry_id:174230)的存在使得控制方程变为非齐次，但并未破坏系统的线性，[叠加原理](@entry_id:144649)对于不同的载荷组合依然有效 。此外，在构建解的过程中，向 $\phi$ 中添加三次多项式项可以用于调整边界上的局部面力[分布](@entry_id:182848)，而不会改变由 $\phi$ 的高阶项产生的自平衡应[力场](@entry_id:147325)的合力与[合力矩](@entry_id:166772) 。

#### 极[坐标系](@entry_id:156346)

对于包含圆孔、圆盘等具有轴对称或圆形几何特征的问题，使用笛卡尔坐标系会非常不便。在这种情况下，将 Airy 应力函数理论推广到极[坐标系](@entry_id:156346) $(r, \theta)$ 是非常自然的。在极[坐标系](@entry_id:156346)中，应力分量 $(\sigma_{rr}, \sigma_{\theta\theta}, \sigma_{r\theta})$ 可以用极坐标下的 Airy 函数 $\Phi(r, \theta)$ 表示为 ：

$$
\sigma_{rr} = \frac{1}{r}\frac{\partial\Phi}{\partial r} + \frac{1}{r^2}\frac{\partial^2\Phi}{\partial\theta^2}
$$
$$
\sigma_{\theta\theta} = \frac{\partial^2\Phi}{\partial r^2}
$$
$$
\sigma_{r\theta} = \frac{1}{r^2}\frac{\partial\Phi}{\partial\theta} - \frac{1}{r}\frac{\partial^2\Phi}{\partial r \partial\theta} = -\frac{\partial}{\partial r}\left(\frac{1}{r}\frac{\partial\Phi}{\partial\theta}\right)
$$

同样地，在极坐标下，Airy 函数 $\Phi(r, \theta)$ 必须满足双谐方程，其形式为：
$$
\nabla^4\Phi = \left(\frac{\partial^2}{\partial r^2} + \frac{1}{r}\frac{\partial}{\partial r} + \frac{1}{r^2}\frac{\partial^2}{\partial\theta^2}\right)^2 \Phi = 0
$$

#### [多连通域](@entry_id:185277)问题

当物体含有孔洞时，其拓扑结构变为**多连通**的。在这种情况下，即使找到了一个满足双谐方程并在所有物理边界（外边界和内孔边界）上满足给定边界条件的 Airy 函数 $\phi$，也不能保证其对应的[位移场](@entry_id:141476)是单值的。当沿一条环绕孔洞的闭合路径积分时，位移可能会出现一个非零的“跳跃”，这在物理上对应于[位错](@entry_id:157482)。

为了保证[位移场](@entry_id:141476)的[单值性](@entry_id:174849)，必须对解施加额外的约束。这些约束由 **Michell 条件**给出：对于每一个独立的孔洞，沿环绕该孔洞的任意闭合路径 $C_k$ 计算的面力，其合力与[合力矩](@entry_id:166772)都必须为零 。数学上表示为：

$$
\oint_{C_k} \boldsymbol{t} \, ds = \oint_{C_k} \boldsymbol{\sigma}\boldsymbol{n} \, ds = \boldsymbol{0}
$$
$$
\oint_{C_k} (\boldsymbol{x} \times \boldsymbol{t})_z \, ds = \oint_{C_k} \varepsilon_{pq} x_p (\sigma_{qj}n_j) \, ds = 0
$$

这些积分条件是确保[多连通域](@entry_id:185277)中弹性体位移[单值性](@entry_id:174849)的充要条件。它们构成了对 Airy 函数解的全局性约束，是处理带孔结构问题的关键。