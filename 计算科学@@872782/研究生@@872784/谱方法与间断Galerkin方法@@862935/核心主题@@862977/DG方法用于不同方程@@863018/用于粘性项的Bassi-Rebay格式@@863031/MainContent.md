## 引言
在计算科学与工程领域，对包含黏性或扩散过程的物理现象进行精确仿真是至关重要的，尤其是在求解[Navier-Stokes方程](@entry_id:161487)以模拟[流体运动](@entry_id:182721)时。间断Galerkin (DG) 方法因其卓越的局部守恒性、处理复杂几何的能力以及对[高阶近似](@entry_id:262792)的天然支持，已成为该领域的有力工具。然而，将DG方法直接应用于包含[二阶导数](@entry_id:144508)（如黏性项）的方程会带来独特的理论和实践挑战，简单的离散格式往往会导致数值不稳定。Bassi-Rebay (BR) 格式正是一族为应对此挑战而设计的优雅且强大的解决方案。

本文旨在系统性地剖析[Bassi-Rebay格式](@entry_id:746696)。我们将从基本原理出发，逐步深入到其在复杂问题中的前沿应用。通过本文的学习，您将掌握该方法的核心思想，并理解其在现代[计算模拟](@entry_id:146373)中的地位和价值。

*   在第一章 **“原理与机制”** 中，我们将深入探讨BR格式的数学基础。您将了解到为何简单的[中心通量](@entry_id:747204)方法会失效，以及BR2格式如何通过引入核心概念——“[提升算子](@entry_id:751273)”——来重构梯度并巧妙地实现格式的稳定性。我们还将揭示BR2格式与其他经典[DG方法](@entry_id:748369)（如SIPG）的内在联系，并讨论在[高阶谱](@entry_id:191458)元法背景下实现一个鲁棒高效的BR2格式所需考虑的关键实践问题。

*   第二章 **“应用与交叉学科联系”** 将展示BR格式的强大功能和灵活性。我们将探索其在计算流体动力学、[各向异性扩散](@entry_id:151085)以及[流固耦合](@entry_id:171183)等多物理场问题中的应用。通过这些案例，您将看到理论原理如何转化为解决真实世界复杂工程与科学问题的工具。

*   最后，在第三章 **“动手实践”** 中，我们提供了一系列精心设计的练习，旨在将理论知识转化为实践技能。通过亲手推导和分析，您将对矩阵组装、方法间的等价性以及数值积分的精度要求等关键环节有更具体的认识。

通过这一从理论到应用再到实践的[结构化学](@entry_id:176683)习路径，本文将为您构建一个关于[Bassi-Rebay格式](@entry_id:746696)的完整知识体系。

## 原理与机制

本章深入探讨[Bassi-Rebay格式](@entry_id:746696)的数学原理和核心机制。我们将从离散黏性项的基本挑战出发，分析以[中心通量](@entry_id:747204)为基础的简单格式为何不稳定，从而引出通过稳定化[梯度重构](@entry_id:749996)来确保稳定性的Bassi-Rebay二类（BR2）格式。本章的核心内容将集中于定义和理解[提升算子](@entry_id:751273)（lifting operator）——BR2格式的基石，并阐明其如何确保格式的[能量稳定性](@entry_id:748991)。此外，我们还将探讨BR2格式与其他经典间断Galerkin（DG）方法（如[对称内部罚](@entry_id:755719)分格式，SIPG）之间的深刻联系。最后，我们将讨论在[高阶谱](@entry_id:191458)元法背景下实现一个鲁棒且高效的BR2格式所需考虑的关键实践问题，包括稳定化参数的选取、数值积分的精度要求以及所得线性系统的求解策略。

### 黏性项的离散：一阶系统方法

[间断Galerkin方法](@entry_id:748369)因其局部性、[高阶精度](@entry_id:750325)和处理复杂几何的能力，在求解偏微分方程（PDEs）方面表现出色，尤其对于[双曲守恒律](@entry_id:147752)。然而，当应用于包含[二阶导数](@entry_id:144508)的方程（如[热传导方程](@entry_id:194763)或[Navier-Stokes方程](@entry_id:161487)中的黏性项）时，会遇到一个基本挑战。标准的[DG弱形式](@entry_id:748377)涉及在单元内部对[试探函数](@entry_id:756165)进行[分部积分](@entry_id:136350)，这自然地将一阶空间导数转移到[试探函数](@entry_id:756165)上。对于二阶算子，如拉普拉斯算子 $-\nabla^2 u$，直接应用两次分部积分会引入解在界面上的[法向导数](@entry_id:169511)通量，这在DG框架中不易处理。

一个强大而系统的方法是将原始的[二阶PDE](@entry_id:175326)重写为一个等价的[一阶系统](@entry_id:147467)。考虑一个标量热传导方程，可以引入一个辅助变量 $\boldsymbol{q}$ 来表示温度 $u$ 的梯度 [@problem_id:3366130]：
$$
\partial_t u = \nabla \cdot (\kappa \boldsymbol{q}), \qquad \boldsymbol{q} = \nabla u
$$
其中 $\kappa > 0$ 是热导率。通过这种方式，我们将一个二阶问题转化为了两个耦合的一阶问题。现在，我们可以对这个[一阶系统](@entry_id:147467)应用标准的[DG方法](@entry_id:748369)。

我们将解 $u$ 和 $\boldsymbol{q}$ 的近似解 $u_h$ 和 $\boldsymbol{q}_h$ 以及相应的[试探函数](@entry_id:756165) $\phi_h$ 和 $\boldsymbol{\psi}_h$ 限制在每个单元 $K$ 上的分片[多项式空间](@entry_id:144410)中。通过将方程乘以[试探函数](@entry_id:756165)并在每个单元 $K$ 上积分，再进行分部积分，我们得到如下的[DG弱形式](@entry_id:748377)：
$$
\int_K (\partial_t u_h) \phi_h \, dx = - \int_K \kappa \boldsymbol{q}_h \cdot \nabla \phi_h \, dx + \int_{\partial K} \phi_h (\kappa \boldsymbol{q}^\star \cdot \boldsymbol{n}) \, ds
$$
$$
\int_K \boldsymbol{q}_h \cdot \boldsymbol{\psi}_h \, dx = - \int_K u_h (\nabla \cdot \boldsymbol{\psi}_h) \, dx + \int_{\partial K} u^\star (\boldsymbol{\psi}_h \cdot \boldsymbol{n}) \, ds
$$
这里的 $\boldsymbol{n}$ 是单元边界 $\partial K$ 上的单位外法向向量。[分部积分](@entry_id:136350)产生了边界积分项，这些项耦合了相邻的单元。为了封闭这个系统，我们必须在每个单元界面上定义**数值通量** $u^\star$ 和 $\boldsymbol{q}^\star \cdot \boldsymbol{n}$。这些数值通量的选择至关重要，它直接决定了最终离散格式的稳定性、精度和守恒性。

### [中心通量](@entry_id:747204)的挑战与Bassi-Rebay一类格式

在选择[数值通量](@entry_id:752791)时，一个自然且简单的出发点是满足**一致性 (consistency)**、**守恒性 (conservation)** 和 **对称性 (symmetry)** 的基本原则 [@problem_id:3366112]。一致性要求当精确解足够光滑时，数值通量能够恢复为精确通量。守恒性（对于黏性通量）要求在内部界面上，一个单元的流出通量精确等于相邻单元的流入通量，这保证了全局守恒。对称性则要求通量的定义不依赖于我们从界面的哪一侧观察。

对于一个在界面上具有左右迹 $u^-$ 和 $u^+$ 的标量场，可以证明，唯一同时满足这三个属性的线性两点通量是[算术平均值](@entry_id:165355) [@problem_id:3366112]：
$$
u^\star = \frac{1}{2}(u^- + u^+) = \{u_h\}
$$
将这个思想应用于我们的一阶系统，最直接的通量选择是所谓的**[中心通量](@entry_id:747204) (central fluxes)**，即在所有界面上都取解和其梯度的[算术平均值](@entry_id:165355)：
$$
u^\star = \{u_h\}, \qquad \boldsymbol{q}^\star = \{\boldsymbol{q}_h\}
$$
这种选择构成了**Bassi-Rebay一类 (BR1)** 格式的基础。BR1格式通过一个使用[中心通量](@entry_id:747204) $u^\star$ 的弱形式来重构梯度 $\boldsymbol{q}_h$，然后在其自身的[弱形式](@entry_id:142897)中使用[中心通量](@entry_id:747204) $\boldsymbol{q}^\star$。

尽管[中心通量](@entry_id:747204)看起来非常优雅和简单，但它对于纯[扩散](@entry_id:141445)问题存在一个致命缺陷：**不稳定性**。我们可以通过能量分析来揭示这一点。对于[周期性边界条件](@entry_id:147809)下的热传导问题，离散能量为 $E(t) = \frac{1}{2} \sum_K \int_K u_h^2 \, dx$。通过在[弱形式](@entry_id:142897)中取[试探函数](@entry_id:756165)为解本身（即 $\phi_h = u_h, \boldsymbol{\psi}_h = \boldsymbol{q}_h$），并对所有单元求和，可以推导出能量的变化率 [@problem_id:3366090]：
$$
\frac{dE}{dt} + \kappa \sum_K \int_K |\boldsymbol{q}_h|^2 \, dx + \kappa \sum_{f \in \mathcal{F}} \int_f \left( (\{u_h\} - u^\star)[\boldsymbol{q}_h \cdot \boldsymbol{n}] + ( \{\boldsymbol{q}_h \cdot \boldsymbol{n}\} - \boldsymbol{q}^\star \cdot \boldsymbol{n} )[u_h] \right) \, ds = 0
$$
其中 $[\cdot]$ 代表界面上的跃变。当我们代入[中心通量](@entry_id:747204) $u^\star = \{u_h\}$ 和 $\boldsymbol{q}^\star \cdot \boldsymbol{n} = \{\boldsymbol{q}_h \cdot \boldsymbol{n}\}$ 时，界[面积分](@entry_id:275394)项完全消失！能量方程简化为：
$$
\frac{dE}{dt} = - \kappa \sum_K \int_K |\boldsymbol{q}_h|^2 \, dx
$$
虽然这个方程表明能量是不增的，但它并不足以保证稳定性。一个稳定的格式必须能够抑制所有非物理的、高频的[数值振荡](@entry_id:163720)。然而，在DG框架中，一个非零的解跃变 $[u_h] \neq 0$ 可能产生一个在体积上积分为零的[离散梯度](@entry_id:171970)场 $\boldsymbol{q}_h$。在这种情况下，[能量耗散](@entry_id:147406)项为零，而数值解中可能存在非物理的棋盘状伪影，这些伪影不会随时间衰减。因此，纯[中心通量](@entry_id:747204)格式（包括BR1）对于[扩散](@entry_id:141445)问题是无条件不稳定的 [@problem_id:3366130]。

为了克服这一问题，必须引入额外的稳定化机制。一种常见策略是在通量中加入一个惩罚项，如在**局部间断Galerkin ([LDG](@entry_id:751395))** 方法中所做的 [@problem_id:3366090]：
$$
\boldsymbol{q}^\star \cdot \boldsymbol{n} = \{\boldsymbol{q}_h \cdot \boldsymbol{n}\} - \tau [u_h]
$$
其中 $\tau \ge 0$ 是一个稳定化参数。这个额外的项会在能量方程中产生一个正定的界面耗散项 $\sum_f \int_f \tau |[u_h]|^2 ds$，从而通过惩罚解的跃变来抑制[振荡](@entry_id:267781)，确保稳定性。Bassi-Rebay二类格式则采用了另一种更微妙的稳定化途径。

### [提升算子](@entry_id:751273)：Bassi-Rebay二类格式的核心

Bassi-Rebay二类（BR2）格式的精妙之处在于它不是通过修改通量来直接添加罚项，而是通过**修正[离散梯度](@entry_id:171970)**的定义来隐式地引入稳定化。实现这一点的核心工具是**[提升算子](@entry_id:751273) (lifting operator)**。

[提升算子](@entry_id:751273)是一个将定义在单元界面上的数据“提升”为定义在单元体积内的多项式场的映射。更具体地说，对于一个界面 $F$ 和一个定义在其上的标量函数 $\phi$，其对应的（向量）[提升算子](@entry_id:751273) $\boldsymbol{r}_F(\phi)$ 是一个定义在与 $F$ 相邻的单元体积上的向量多项式场。它由以下变分关系唯一确定：对于任意向量[试探函数](@entry_id:756165) $\boldsymbol{w}_h$，满足
$$
\int_{\mathcal{N}(F)} \boldsymbol{r}_F(\phi) \cdot \boldsymbol{w}_h \, dx = - \int_F \phi \, \{\boldsymbol{w}_h \cdot \boldsymbol{n}\} \, ds
$$
其中 $\mathcal{N}(F)$ 是与界面 $F$ 相邻的单元的并集。这个定义虽然抽象，但其本质是要求提升后的场 $\boldsymbol{r}_F(\phi)$ 在 $L^2$ 意义下代表了界面上的通量。

为了让这个概念更具体，我们来推导一个简单情况下的[提升算子](@entry_id:751273) [@problem_id:3366072]。考虑在一维[参考单元](@entry_id:168425) $K=[-1,1]$ 上，[多项式空间](@entry_id:144410)为 $\mathbb{P}^1(K)$（线性多项式）。设左右界面 $x=-1$ 和 $x=1$ 上的法向分别为 $n_L = -1$ 和 $n_R = +1$。我们要寻找一个标量提升 $r(x) \in \mathbb{P}^1(K)$，它将界面数据 $(\psi_L, \psi_R) = (a, b)$ 提升到体积中。根据定义，对于所有 $v \in \mathbb{P}^1(K)$，它必须满足：
$$
\int_{-1}^1 r(x) v(x) \, dx = \psi_R v(1) n_R + \psi_L v(-1) n_L = b v(1) - a v(-1)
$$
由于 $r(x)$ 是线性的，我们可以写成 $r(x) = c_0 + c_1 x$。我们只需在 $\mathbb{P}^1(K)$ 的一组基上（例如 $\{1, x\}$）强制执行上述关系即可求出系数 $c_0$ 和 $c_1$。
1.  取 $v(x) = 1$：
    $$
    \int_{-1}^1 (c_0 + c_1 x) \cdot 1 \, dx = 2c_0
    $$
    $$
    b \cdot 1 - a \cdot 1 = b-a
    $$
    因此，$2c_0 = b-a \implies c_0 = \frac{b-a}{2}$。
2.  取 $v(x) = x$：
    $$
    \int_{-1}^1 (c_0 + c_1 x) \cdot x \, dx = \frac{2}{3}c_1
    $$
    $$
    b \cdot 1 - a \cdot (-1) = b+a
    $$
    因此，$\frac{2}{3}c_1 = b+a \implies c_1 = \frac{3}{2}(b+a)$。

将系数代回，我们得到该[提升算子](@entry_id:751273)的显式表达式：
$$
r(x) = \frac{b-a}{2} + \frac{3}{2}(b+a)x
$$
这个例子清晰地表明，[提升算子](@entry_id:751273)是一个定义明确、可计算的[线性算子](@entry_id:149003)。在BR2格式中，我们正是利用了这种算子来处理界面上的解的跃变。

### BR2格式的构造与稳定性

BR2格式通过一个精巧的多步过程来构建一个既一致又稳定的[离散梯度](@entry_id:171970)，从而确保整个黏性离散格式的稳定性 [@problem_id:3366076] [@problem_id:3366130]。其实现步骤如下：

1.  **计算破碎梯度 (Broken Gradient)**：在每个单元 $K$ 内部，独立地计算解 $u_h$ 的梯度，记为 $\nabla_h u_h$。这是一个分片多项式向量场，在单元边界上是不连续的。

2.  **计算解的跃变 (Solution Jumps)**：对于每个内部界面 $F$，计算解在该界面上的跃变 $[u_h]$。

3.  **提升跃变 (Lift the Jumps)**：对每个界面 $F$ 上的跃变 $[u_h]$，应用前面定义的向量[提升算子](@entry_id:751273) $\boldsymbol{r}_F$，得到一个局部的向量修正场 $\boldsymbol{r}_F([u_h])$。

4.  **构造稳定化梯度 (Form Stabilized Gradient)**：将破碎梯度和所有界面上的提升修正场加权求和，形成最终的**稳定化梯度** $\tilde{\boldsymbol{q}}_h$：
    $$
    \tilde{\boldsymbol{q}}_h = \nabla_h u_h + \sum_{F \in \mathcal{F}_h^{\text{int}}} \eta_F \boldsymbol{r}_F([u_h])
    $$
    其中 $\eta_F$ 是一个依赖于单元尺寸和多项式次数的稳定化参数，我们将在后面详细讨论它的选择。

5.  **组装[弱形式](@entry_id:142897) (Assemble the Weak Form)**：在原始的[DG弱形式](@entry_id:748377)中，使用这个新构造的稳定化梯度 $\tilde{\boldsymbol{q}}_h$ 来代替 $\boldsymbol{q}_h$，并为黏性通量 $\nu \tilde{\boldsymbol{q}}_h \cdot \boldsymbol{n}$ 选择[中心通量](@entry_id:747204)，即 $\nu \{\tilde{\boldsymbol{q}}_h\} \cdot \boldsymbol{n}$。

BR2格式的稳定性正来源于稳定化梯度定义中的附加项 $\sum \eta_F \boldsymbol{r}_F([u_h])$。当进行能量分析时，这个修正项会在最终的[能量耗散](@entry_id:147406)中产生一个与解的跃变范数的平方成正比的正定项。这与[LDG](@entry_id:751395)或SIPG等方法通过显式罚项达到的效果异曲同工，但其实现方式更为内蕴，是通过对[梯度算子](@entry_id:275922)本身的重构来完成的。这种构造方式不仅确保了稳定性，还保持了紧凑的计算模板（stencil），因为每个[提升算子](@entry_id:751273) $\boldsymbol{r}_F$ 的支集仅限于与界面 $F$ 直接相邻的单元 [@problem_id:3366130] [@problem_id:3366144]。

### BR2、SIPG与[LDG](@entry_id:751395)之间的联系

初看起来，BR2的“稳定化[梯度重构](@entry_id:749996)”哲学与SIPG（[对称内部罚](@entry_id:755719)分格式）的“显式界面惩罚”哲学似乎截然不同。然而，在某些简单情况下，这两种方法实际上是代数等价的，这揭示了它们之间深刻的内在联系。

我们来考察一维情况下，使用分片线性（P1）多项式时，BR2的稳定化项与SIPG的罚分项之间的关系 [@problem_id:3366061]。
- SIPG的稳定化项在一个界面 $e$ 上具有形式 $S_{\text{SIPG}} = \frac{\sigma}{h} [u][v]$，其中 $\sigma$ 是无量纲的罚参数，$h$ 是单元尺寸。
- BR2的稳定化项（源于稳定化梯度中的附加项对最终双线性形式的贡献）具有形式 $S_{\text{BR2}} = \tau \int_{K_L \cup K_R} r_e([u]) r_e([v]) \, dx$，其中 $\tau$ 是BR2的稳定化参数。

对于P1多项式，其梯度是分片常数。为简化分析，我们考虑一种在每个单元上为常数的简化[提升算子](@entry_id:751273)。例如，如果[提升算子](@entry_id:751273) $r_e([u])$ 在左单元 $K_L$ 上的值为 $-\frac{[u]}{h}$，在右单元 $K_R$ 上的值为 $+\frac{[u]}{h}$，则可以进行如下计算：
$$
S_{\text{BR2}} = \tau \left( \int_{K_L} \left(-\frac{[u]}{h}\right)\left(-\frac{[v]}{h}\right) dx + \int_{K_R} \left(\frac{[u]}{h}\right)\left(\frac{[v]}{h}\right) dx \right)
$$
$$
= \tau \left( \frac{[u][v]}{h^2} \cdot h + \frac{[u][v]}{h^2} \cdot h \right) = \frac{2\tau}{h} [u][v]
$$
通过比较 $S_{\text{SIPG}}$ 和 $S_{\text{BR2}}$，我们立即得到 $\frac{\sigma}{h} = \frac{2\tau}{h}$，即 $\sigma = 2\tau$。

这个简单的推导表明，对于一维P1单元，BR2格式与一个特定罚参数的SIPG格式是完[全等](@entry_id:273198)价的。这说明，尽管它们的表述和推导路径不同，但它们都实现了对解的界面跃变的相同数学控制。这一认识有助于我们将不同的DG方法统一到一个更广阔的理论框架之下。

### 高阶方法的实践考量

要在实际中成功地应用高阶BR2格式，特别是在$hp$-自适应或高多项式次数的[谱元法](@entry_id:755171)背景下，必须仔细处理几个关键的理论和实践问题。

#### 稳定化参数的标度

稳定化参数 $\eta_F$ 的选择对于格式的稳定性和精度至关重要。一个与网格尺寸 $h$ 和多项式次数 $p$ 无关的常数是不够的。为了保证格式在[网格加密](@entry_id:168565)（$h \to 0$）和多项式次数增加（$p \to \infty$）时都能保持稳定（即所谓的$hp$-鲁棒性），$\eta_F$ 必须进行适当的标度。

正确的标度可以通过[稳定性分析](@entry_id:144077)推导出来，其核心在于利用[多项式空间](@entry_id:144410)的两个基本性质：[迹不等式](@entry_id:756082) (trace inequality) 和[逆不等式](@entry_id:750800) (inverse inequality) [@problem_id:3366089]。在证明双线性形式的矫顽性时，需要用一个正定的稳定化项来控制一个由[分部积分](@entry_id:136350)产生的、符号不定的界面项。这个界面项的大小可以通过[迹不等式](@entry_id:756082)来估计，而[迹不等式](@entry_id:756082)本身依赖于 $h$ 和 $p$。为了“压制”住这个界面项，稳定化参数 $\eta_F$ 必须足够大。对于一个$d$维问题，标准的分析表明，稳定化参数需要满足如下[标度关系](@entry_id:273705) [@problem_id:3366089] [@problem_id:3366144]：
$$
\eta_F \propto \frac{(p+1)^2}{h_F} \quad \text{或更一般地} \quad \eta_F \propto \frac{p^2}{h_F}
$$
其中 $h_F$ 是界面的特征尺寸。这个标度确保了无论 $h$ 多小或 $p$ 多大，格式的[矫顽性](@entry_id:159399)常数都保持有界，从而保证了[能量稳定性](@entry_id:748991)和最终[线性系统](@entry_id:147850)[解的唯一性](@entry_id:143619)。

#### 数值积分与混淆

DG方法的[弱形式](@entry_id:142897)中充满了各种体积和界面积分。在计算机上，这些积分通常使用数值积分（quadrature）来近似。如果[数值积分](@entry_id:136578)的精度不够高，它将无法精确计算多项式乘积的积分，从而引入所谓的**混淆误差 (aliasing error)**。这种误差不仅会降低格式的精度，甚至可能破坏其稳定性 [@problem_id:3366114]。

为避免混淆，数值积分规则的精度必须足以精确计算出现在[弱形式](@entry_id:142897)中的所有多项式被积函数。我们需要仔细分析每个积分项中被积函数的最高多项式次数 [@problem_id:3366114] [@problem_id:3366137]。
- **梯度方程体积项**: 如 $\int_K r_h \partial_x u_h \, dx$。被积函数 $r_h (\partial_x u_h)$ 的次数为 $p + (p-1) = 2p-1$。
- **[扩散方程](@entry_id:170713)体积项**: 如 $\int_K (\partial_x v_h) q_h \, dx$。被积函数 $(\partial_x v_h) q_h$ 的次数为 $(p-1) + p = 2p-1$。
- **BR2稳定化项**: 形式为 $\int_K l_u l_v \, dx$，其中 $l_u, l_v \in \mathbb{P}_p(K)$。被积函数 $l_u l_v$ 的次数为 $p + p = 2p$。
- **可变系数**: 如果[扩散](@entry_id:141445)系数 $\kappa$ 本身是次数为 $r$ 的多项式，那么上述次数还会相应增加。例如，体积项 $\int_K \kappa \nabla u_h \cdot \nabla v_h \, dx$ 的被积函数次数将是 $r + 2(p-1) = r+2p-2$。

综合来看，为了对所有项都进行精确积分，体积积分的精度至少需要达到 $\max(r+2p-2, 2p)$，而界面积分则需要达到 $\max(r+2p-1, 2p)$ [@problem_id:3366137]。例如，使用 $p+1$ 个节点的Gauss-Legendre积分规则，其精度为 $2(p+1)-1 = 2p+1$，这足以精确计算上述所有体积项，从而避免混淆误差 [@problem_id:3366114]。

#### 线性系统与求解器

BR2格式离散一个[稳态扩散](@entry_id:154663)问题后，会产生一个[大型稀疏线性系统](@entry_id:137968) $A \boldsymbol{u} = \boldsymbol{f}$。该系统的性质决定了其求解策略。由于BR2格式（采用对称通量和对称稳定化）的[双线性形式](@entry_id:746794)是**对称**的，并且在施加齐次[Dirichlet边界条件](@entry_id:142800)后是**正定**的，因此其产生的[刚度矩阵](@entry_id:178659) $A$ 是[对称正定](@entry_id:145886)（SPD）的 [@problem_id:3366144]。

这一优良性质意味着我们可以使用最高效的Krylov[子空间迭代](@entry_id:168266)法之一：**共轭梯度法 (Conjugate Gradient, CG)**。相比于需要存储大量历史向量的GMRES等非对称求解器，CG法的计算和存储成本都更低。

然而，由$hp$-DG方法产生的线性系统的[条件数](@entry_id:145150)通常会随着 $h^{-2}$ 和 $p^4$ 而恶化，导致CG等[迭代法的收敛](@entry_id:139832)速度急剧下降。因此，一个高效的**预条件子 (preconditioner)** 是必不可少的。对于像BR2这样具有紧凑计算模板的格式，**多重网格 (multigrid)** 方法是一类非常有效的[预条件子](@entry_id:753679)。无论是[代数多重网格](@entry_id:140593)（AMG）还是几何$p$-[多重网格](@entry_id:172017)，它们都能够显著改善条件数，实现接近于 $O(N)$ 的求解效率，其中 $N$ 是自由度总数。此外，对于[高阶张量](@entry_id:200122)积[基函数](@entry_id:170178)，利用**[和因子分解](@entry_id:755628) (sum-factorization)** 技术的无矩阵（matrix-free）方法可以极大地降低算子作用于向量的计算复杂度，使其从 $O(p^{2d})$ 降至 $O(p^{d+1})$，这对于三维[高阶模](@entry_id:750331)拟尤为关键 [@problem_id:3366144]。