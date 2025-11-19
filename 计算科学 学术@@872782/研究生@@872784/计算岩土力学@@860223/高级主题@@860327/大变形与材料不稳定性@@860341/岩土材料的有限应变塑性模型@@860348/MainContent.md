## 引言
当岩土结构（如边坡、地基和隧道）经历大变形时，传统的小应变理论便显得力不从心。准确预测滑坡、桩贯入或[地震液化](@entry_id:748774)等现象，要求我们必须采用能够处理[几何非线性](@entry_id:169896)和[材料非线性](@entry_id:162855)耦合的先进力学框架。岩土材料的[有限应变塑性](@entry_id:185352)模型正是为此而生，它为描述材料在极端载荷下的复杂行为提供了坚实的理论基础。然而，掌握这一理论并非易事，它涉及复杂的[运动学](@entry_id:173318)、严谨的热力学原理以及精密的数值算法。本文旨在系统性地梳理这一知识体系，填补基础理论与高级应用之间的鸿沟。

在接下来的内容中，我们将分三章进行探讨。首先，在“原理与机制”一章中，我们将建立[有限应变塑性](@entry_id:185352)理论的数学和物理基础，从变形梯度到[热力学](@entry_id:141121)耗散，再到针对岩土材料的本构要素。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示如何运用这些原理来构建和解释经典及高级的岩土模型，并探讨其在[多物理场耦合](@entry_id:171389)问题中的应用。最后，“动手实践”部分将提供具体的计算练习，帮助您将理论知识转化为实践能力。

让我们从第一章开始，深入探索[有限应变塑性](@entry_id:185352)理论的核心原理与机制。

## 原理与机制

本章旨在系统性阐述适用于岩土材料的有限应变[弹塑性](@entry_id:193198)模型的理论基础和核心机制。我们将从有限变形[运动学](@entry_id:173318)的基本概念出发，建立描述[材料变形](@entry_id:169356)的数学语言。随后，引入[弹塑性](@entry_id:193198)变形的[乘法分解](@entry_id:199514)，这是[有限应变塑性](@entry_id:185352)理论的基石。在此基础上，我们将构建一个完整的[热力学一致的](@entry_id:755906)本构框架，探讨如何通过[亥姆霍兹自由能](@entry_id:136442)定义[超弹性](@entry_id:159356)响应，并满足材料[坐标系](@entry_id:156346)无关性原理。最后，我们将深入探讨针对岩土材料的特定本构要素，如[应力不变量](@entry_id:170526)、[非关联流动法则](@entry_id:752544)、硬化变量，并介绍求解这些复杂模型的标准计算方法——[返回映射算法](@entry_id:168456)。

### 有限变形运动学基础

为了精确描述材料在大变形下的行为，我们必须超越小应变理论的局限，采用有限变形运动学的语言。这一框架的核心是**变形梯度**（deformation gradient）。

考虑一个连续体，其在未变形的**参考构型**中的物[质点](@entry_id:186768)由[坐标向量](@entry_id:153319) $\mathbf{X}$ 描述，在变形后的**当前构型**中，该物[质点](@entry_id:186768)的位置则由空间[坐标向量](@entry_id:153319) $\mathbf{x}$ 描述。变形过程可以看作一个映射 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$。变形梯度张量 $\mathbf{F}$ 定义为该映射对参考构型坐标的梯度：

$ \mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} $

$\mathbf{F}$ 是一个[二阶张量](@entry_id:199780)，它包含了关于局部变形的完整信息。它的一个关键作用是，将参考构型中一个无穷小的物质线元 $d\mathbf{X}$ 映射到当前构型中的对应[线元](@entry_id:196833) $d\mathbf{x}$ [@problem_id:3530589]：

$ d\mathbf{x} = \mathbf{F} d\mathbf{X} $

$\mathbf{F}$ 的[行列式](@entry_id:142978) $J = \det(\mathbf{F})$ 代表了局部体积的变化率，即 $dV = J dV_0$，其中 $dV_0$ 和 $dV$ 分别是参考构型和当前构型中的微元体积。对于物理上可能的变形，物质不能相互穿透，因此必须有 $J > 0$。

变形梯度 $\mathbf{F}$ 能够通过**极分解**（polar decomposition）唯一地分解为一个纯旋转和一个纯拉伸的乘积 [@problem_id:3530589]。这有两种形式：

$ \mathbf{F} = \mathbf{R}\mathbf{U} = \mathbf{V}\mathbf{R} $

其中，$\mathbf{R}$ 是一个正常正交张量（proper orthogonal tensor），代表变形中的刚体旋转部分（$\mathbf{R}^T\mathbf{R}=\mathbf{I}$ 且 $\det(\mathbf{R})=1$）。$\mathbf{U}$ 和 $\mathbf{V}$ 分别是**右[拉伸张量](@entry_id:193200)**（right stretch tensor）和**左[拉伸张量](@entry_id:193200)**（left stretch tensor），它们都是对称正定张量，描述了材料在三个相互正交的[主方向](@entry_id:276187)上的拉伸或压缩。

为了度量应变，我们引入**柯西-格林张量**（Cauchy-Green tensors）。**[右柯西-格林张量](@entry_id:174156)** $\mathbf{C}$ 定义在参考构型上，它通过变形梯度与自身转置的乘积得到：

$ \mathbf{C} = \mathbf{F}^{T}\mathbf{F} = \mathbf{U}^2 $

$\mathbf{C}$ 度量了参考构型中线元长度的平方在变形后的变化。具体来说，当前构型中线元长度的平方 $ds^2$ 可以通过 $\mathbf{C}$ 在参考构型中表示：$ds^2 = d\mathbf{x}^T d\mathbf{x} = ( \mathbf{F}d\mathbf{X} )^T (\mathbf{F}d\mathbf{X}) = d\mathbf{X}^T \mathbf{C} d\mathbf{X}$。类似地，**[左柯西-格林张量](@entry_id:186163)** $\mathbf{B}$ 定义在当前构型上：

$ \mathbf{B} = \mathbf{F}\mathbf{F}^{T} = \mathbf{V}^2 $

$\mathbf{C}$ 和 $\mathbf{B}$ 的[特征值](@entry_id:154894)是相同的，它们等于主拉伸 $\lambda_i$ 的平方（$\lambda_i^2$）。然而，它们的[特征向量](@entry_id:151813)（即[主应变](@entry_id:197797)方向）通常是不同的：$\mathbf{C}$ 的[特征向量](@entry_id:151813)位于参考构型中，而 $\mathbf{B}$ 的[特征向量](@entry_id:151813)位于当前构型中。

### 变形的[乘法分解](@entry_id:199514)

在小应变塑性理论中，总应变 $\boldsymbol{\varepsilon}$ 被简单地分解为弹性部分 $\boldsymbol{\varepsilon}_e$ 和塑性部分 $\boldsymbol{\varepsilon}_p$ 的和：$\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_e + \boldsymbol{\varepsilon}_p$。然而，在有限应变情况下，由于大转动的存在，这种加法分解不再是客观的（即，在叠加一个[刚体转动](@entry_id:191086)后，其形式会发生改变）。

[有限应变塑性](@entry_id:185352)理论的基石是由Kröner和Lee等人提出的**变形梯度[乘法分解](@entry_id:199514)**（multiplicative decomposition）。该理论假设存在一个虚拟的、局部无应力的**[中间构型](@entry_id:193000)** $\mathcal{B}_*$。总变形过程 $\mathbf{F}$ 可以被分解为两步 [@problem_id:3524968]：
1.  首先，一个不可恢复的**塑性变形** $\mathbf{F}_p$ 将材料从参考构型 $\mathcal{B}_0$ 映射到[中间构型](@entry_id:193000) $\mathcal{B}_*$。
2.  随后，一个可恢复的**弹性变形** $\mathbf{F}_e$ 将材料从[中间构型](@entry_id:193000) $\mathcal{B}_*$ 映射到最终的、有应力的当前构型 $\mathcal{B}_t$。

因此，总变形梯度是这两部分的乘积：

$ \mathbf{F} = \mathbf{F}_e \mathbf{F}_p $

这个乘法结构是保证[本构关系](@entry_id:186508)在有限转动下客观性的关键。对于这一分解，有几个重要的物理约束 [@problem_id:3524968]。首先，为了保证[中间构型](@entry_id:193000)和当前构型的物理实在性，$\mathbf{F}_e$ 和 $\mathbf{F}_p$ 都必须是可逆的，即 $\det(\mathbf{F}_e) > 0$ 且 $\det(\mathbf{F}_p) > 0$。其次，虽然总变形梯度 $\mathbf{F}$ 作为一个从全局连续[位移场](@entry_id:141476)导出的量，必然是**协调的**（compatible，即其旋度为零），但塑性变形梯度 $\mathbf{F}_p$ 通常是**不协调的**（incompatible，$\text{curl}(\mathbf{F}_p) \neq \mathbf{0}$）。$\mathbf{F}_p$ 的不协调性在物理上代表了由于[塑性流动](@entry_id:201346)（如[位错](@entry_id:157482)、[晶界](@entry_id:196965)滑移、颗粒重排）而在[材料微观结构](@entry_id:198422)中产生的几何不匹配和[残余应力](@entry_id:138788)。

体积变形也遵循[乘法规则](@entry_id:197368)。总的体积比 $J = \det(\mathbf{F})$ 是弹性体积比 $J_e = \det(\mathbf{F}_e)$ 和塑性体积比 $J_p = \det(\mathbf{F}_p)$ 的乘积：$J = J_e J_p$。取对数后，我们得到对数体积应变的加法分解：

$ \ln(J) = \ln(J_e) + \ln(J_p) \implies \varepsilon^v = \varepsilon_e^v + \varepsilon_p^v $

这揭示了金属和岩土材料在塑性行为上的一个根本区别 [@problem_id:3524990]。对于金属，塑性变形通常被认为是**保体积的**（isochoric），即 $J_p = 1$，因此所有体积变化都是弹性的（$J = J_e$）。然而，对于岩土材料，如砂土和粘土，[塑性流动](@entry_id:201346)伴随着显著的体积变化——压实（compaction, $J_p  1$）或剪胀（dilation, $J_p > 1$）。

例如，考虑一个岩土样本，其总体积比测量为 $J=0.92$，同时累积的塑性对数[体积应变](@entry_id:267252)为 $\varepsilon_p^v = -0.08$（代表塑性压实）。我们可以计算出塑性体积比 $J_p = \exp(-0.08) \approx 0.9231$。因此，弹性体积比为 $J_e = J / J_p = 0.92 / 0.9231 \approx 0.9966$。对应的弹性对数体积应变为 $\varepsilon_e^v = \ln(J_e) \approx -0.0034$。这表明，总的8%的体积减小中，绝大部分（约7.7%）是塑性的，只有很小一部分（约0.34%）是弹性的 [@problem_id:3524990]。

### [热力学](@entry_id:141121)框架与本构原理

一个严谨的[弹塑性](@entry_id:193198)模型必须基于热力学原理。对于[等温过程](@entry_id:143096)，**克劳修斯-杜亨不等式**（Clausius-Duhem inequality）要求材料内部的[耗散功率](@entry_id:177328)必须非负。以单位参考体积表示，该不等式可写为 [@problem_id:3524995]：

$ \mathcal{D} = P:\dot{F} - \dot{\psi} \ge 0 $

其中，$P$ 是第一皮奥拉-基尔霍夫（Piola-Kirchhoff）[应力张量](@entry_id:148973)，$\dot{F}$ 是变形梯度的[物质时间导数](@entry_id:190892)，$\psi$ 是单位参考体积的亥姆霍兹自由能。

为了便于在当前构型中进行分析，我们需要引入**[功共轭](@entry_id:194957)**（work-conjugate）的应力-应变率对。可以证明，单位参考体积的内功率 $p_0$ 具有以下等价形式 [@problem_id:3524999]：

$ p_0 = P:\dot{F} = S:\dot{E} = \boldsymbol{\tau}:d $

这里，$\dot{E} = \frac{1}{2}\dot{C}$ 是格林-拉格朗日（Green-Lagrange）应变张量的率；$S = J F^{-1} \sigma F^{-T}$ 是[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量，它与 $\dot{E}$ [功共轭](@entry_id:194957)；$\boldsymbol{\tau} = J\sigma$ 是基尔霍夫（Kirchhoff）[应力张量](@entry_id:148973)（$\sigma$ 是柯西应力），它与变形率张量 $d = \text{sym}(\dot{F}F^{-1})$ [功共轭](@entry_id:194957)。

利用 $\boldsymbol{\tau}:d$ 的形式，克劳修斯-杜亨不等式在当前构型中写为 $\mathcal{D} = \boldsymbol{\tau}:d - \dot{\psi} \ge 0$。

在**超[弹塑性](@entry_id:193198)**（hyperelastic-plastic）模型中，我们假设自由能 $\psi$ 仅是弹性[状态和](@entry_id:193625)一组**内变量** $\alpha_A$（例如硬化参数）的函数：$\psi = \psi(C_e, \alpha_A)$。这里的 $C_e = F_e^T F_e$ 是**弹性[右柯西-格林张量](@entry_id:174156)**。根据**物质[坐标系](@entry_id:156346)无关性原理**（Principle of Material Frame Indifference, MFI），[本构关系](@entry_id:186508)不能依赖于观察者的[参考系](@entry_id:169232)。让 $\psi$ 依赖于 $C_e$（一个在叠加[刚体转动](@entry_id:191086)下不变的客观张量）而不是依赖于包含旋转的 $F_e$，正是满足MFI的关键 [@problem_id:3524966]。

通过[Coleman-Noll方法](@entry_id:747468)，我们可以从自由能中推导出弹性本构关系和耗散的表达式。对于弹性部分，我们得到[第二皮奥拉-基尔霍夫应力](@entry_id:173163)（在[中间构型](@entry_id:193000)中定义）：

$ S_e = 2 \frac{\partial \psi}{\partial C_e} $

然后通过**[前推](@entry_id:158718)**（push-forward）操作得到当前构型中的柯西应力 [@problem_id:3530589]：

$ \sigma = \frac{1}{J} F_e S_e F_e^T $

这个过程确保了应力响应的客观性，因为整个推导都建立在客观的能量函数和[应变度量](@entry_id:755495)之上。弹性变形梯度 $F_e$（包含了弹性旋转 $R_e$）在此过程中起到了将应力从[中间构型](@entry_id:193000)正确地旋转和拉伸到当前构型的关键作用 [@problem_id:3524966]。

在[耗散不等式](@entry_id:188634)中，我们可以分离出与内变量演化相关的部分，得到**折减[耗散不等式](@entry_id:188634)**（reduced dissipation inequality）。定义[热力学力](@entry_id:161907) $Y_A = -\frac{\partial \psi}{\partial \alpha_A}$，不等式表明[耗散功率](@entry_id:177328) $\mathcal{D} = \boldsymbol{\tau}:d^p + \sum_A Y_A \dot{\alpha}_A \ge 0$ [@problem_id:3524995]，其中 $d^p$ 是变形率张量的塑性部分。

这种基于能量函数的**超[弹塑性](@entry_id:193198)**方法与早期的**次[弹塑性](@entry_id:193198)**（hypoelastic-plastic）方法形成对比 [@problem_id:3524978]。次弹性模型直接以率的形式定义[本构关系](@entry_id:186508)，例如 $\overset{\triangledown}{\sigma} = \mathbb{C}:d$。然而，柯西应力的[物质时间导数](@entry_id:190892) $\dot{\sigma}$ 并非客观的。在纯刚体旋转下（$d=0$），$\dot{\sigma}$ 并不为零，这会产生虚假的应力。因此，次弹性模型必须引入**[客观应力率](@entry_id:199282)**，如**Jaumann率**或**[Green-Naghdi率](@entry_id:190839)**，它们通过减去[自旋张量](@entry_id:187346) $W$ 的影响来修正 $\dot{\sigma}$，从而保证[本构关系](@entry_id:186508)的客观性。相比之下，超[弹塑性](@entry_id:193198)模型通过其构造方式从根本上保证了客观性，无需显式引入[客观应力率](@entry_id:199282)。

### 针对岩土材料的[本构模型](@entry_id:174726)

为了构建能够描述岩土材料复杂行为的实际模型，我们需要引入更具体的本构要素。

#### [应力不变量](@entry_id:170526)
对于各向同性材料，其屈服和破坏行为仅依赖于应力状态的[标量不变量](@entry_id:193787)，而不依赖于[坐标系](@entry_id:156346)的选择。在岩土力学中，最关键的三个[不变量](@entry_id:148850)是 [@problem_id:3524979]：
1.  **平均应力** $p$：$p = \frac{1}{3}\text{tr}(\boldsymbol{\sigma})$。它度量了应力状态的静水压力部分，主要控制材料的体积响应和压敏性（例如，固结和[硬化](@entry_id:177483)）。
2.  **偏应力大小** $q$：$q = \sqrt{\frac{3}{2}\boldsymbol{s}:\boldsymbol{s}}$，其中 $\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$ 是[偏应力张量](@entry_id:267642)，$J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$ 是偏应力第二[不变量](@entry_id:148850)。$q$ 度量了应力状态的剪切部分，主要驱动材料的剪切变形和破坏。
3.  **洛德角** $\theta$：$\cos(3\theta) = \frac{3\sqrt{3}}{2}\frac{J_3}{J_2^{3/2}}$，其中 $J_3 = \det(\boldsymbol{s})$ 是偏应力第三[不变量](@entry_id:148850)。$\theta$ 描述了屈服面在偏平面（$\pi$ 平面）上的形状，反映了**中主应力**对材料强度的影响。对于许多土壤，其在三轴压缩（$\theta=0^\circ$）和三轴拉伸（$\theta=60^\circ$）下的强度不同，[屈服面](@entry_id:175331)呈现出非圆形（如三角形或六边形）的[截面](@entry_id:154995)。

#### [非关联流动法则](@entry_id:752544)
[塑性流动法则](@entry_id:189597)规定了塑性应变增量的方向。它通常写为：

$ d^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}} $

其中 $\dot{\lambda} \ge 0$ 是塑性乘子，$g$ 是**塑性势函数**（plastic potential）。如果塑性势函数 $g$ 与**[屈服函数](@entry_id:167970)** $f$ 相同或成正比（$g \propto f$），则称为**关联[流动法则](@entry_id:177163)**。然而，对于大多数岩土材料，关联流动法则会预测出远大于实验观测值的[塑性剪胀](@entry_id:188905) [@problem_id:3524977]。

例如，对于一个Drucker-Prager类型的材料，其强度由摩擦角决定，这反映在[屈服函数](@entry_id:167970) $f$ 的压力梯度 $\partial f / \partial p$ 上。如果采用关联流动，塑性[体积应变率](@entry_id:272471)（剪胀率）也将由 $\partial f / \partial p$ 控制，导致“摩擦即剪胀”的结论。实验表明，密砂的摩擦角远大于其[剪胀角](@entry_id:748435)。

为了解决这一矛盾，我们采用**[非关联流动法则](@entry_id:752544)**（non-associative flow rule），即选取一个与[屈服函数](@entry_id:167970)不同的塑性[势函数](@entry_id:176105) $g \neq f$。这样，我们可以独立地校准材料的强度（通过 $f$）和其塑性体积变化特性（通过 $g$）。例如，我们可以选择一个压力梯度较小的塑性[势函数](@entry_id:176105)（$\partial g / \partial p  \partial f / \partial p$）来匹配观测到的较低的剪胀率。这种[非关联流动](@entry_id:199220)在满足[热力学](@entry_id:141121)耗散非负的条件下是完全允许的 [@problem_id:3524977]。

#### 内变量与[硬化](@entry_id:177483)
塑性模型通过引入**内变量**来描述材料在塑性变形过程中的状态演化，即**[硬化](@entry_id:177483)**（hardening）或**软化**（softening）。
- **累积塑性应变** $\bar{\varepsilon}_p$：通常定义为塑性[偏应变](@entry_id:201263)率的积分，例如 $\dot{\bar{\varepsilon}}_p = \sqrt{\frac{2}{3} \text{dev}(d^p):\text{dev}(d^p)}$，用于度量累积的剪切塑性变形量 [@problem_id:3524981]。
- **[各向同性硬化](@entry_id:164486)**：屈服面大小的变化。在修正剑桥（Modified Cam-Clay）模型中，这是由**[前期](@entry_id:170157)固结压力** $p_c$ 控制的。$p_c$ 的演化与塑性[体积应变率](@entry_id:272471)紧密耦合，遵循 $\dot{p}_c = \frac{p_c(1+e)}{\lambda-\kappa} \text{tr}(d^p)$ 的关系，其中 $\lambda$ 和 $\kappa$ 是材料的压缩和[回弹](@entry_id:275734)指数 [@problem_id:3524981]。
- **[运动硬化](@entry_id:172077)**：[屈服面](@entry_id:175331)在[应力空间](@entry_id:199156)中的平移，用于描述[Bauschinger效应](@entry_id:173790)等现象。这是通过**背[应力张量](@entry_id:148973)** $X$ 实现的。背应力的演化法则通常包含一个随[塑性流动](@entry_id:201346)方向增加的项和一个“动态恢复”项，例如Armstrong-Frederick类型的法则：$\dot{X} = c_1 \dot{\lambda} \mathbf{N}^{\text{dev}} - c_2 \dot{\lambda} X$，其中 $\mathbf{N}^{\text{dev}}$ 是[塑性流动](@entry_id:201346)方向的偏量部分 [@problem_id:3524981]。

这些内变量的[演化方程](@entry_id:268137)都与塑性乘子 $\dot{\lambda}$ 成正比，表明只有在发生[塑性流动](@entry_id:201346)时，材料状态才会改变。

### 计算框架：[返回映射算法](@entry_id:168456)

由于有限应变[弹塑性](@entry_id:193198)[本构方程](@entry_id:138559)是高度[非线性](@entry_id:637147)的，并且以率的形式给出，因此在[有限元分析](@entry_id:138109)中需要采用稳健的[数值积分](@entry_id:136578)算法来更新应力和[状态变量](@entry_id:138790)。最广泛使用的算法是基于**隐式[后向欧拉法](@entry_id:139674)**的**[弹性预测-塑性修正](@entry_id:748860)**方案，也称为**[返回映射算法](@entry_id:168456)**（return mapping algorithm） [@problem_id:3524994]。

在一个时间步从 $t_n$ 到 $t_{n+1}$，已知该步的总变形梯度 $\mathbf{F}_{n+1}$ 以及上一步的状态 $(\mathbf{F}_p^n, \kappa^n)$。算法分为两步：

1.  **弹性预测**：
    首先，假设整个时间步是纯弹性的。这意味着塑性变量保持不变：$\mathbf{F}_p^{\text{tr}} = \mathbf{F}_p^n$。基于此，计算**试探弹性变形梯度** $\mathbf{F}_e^{\text{tr}} = \mathbf{F}_{n+1} (\mathbf{F}_p^n)^{-1}$。然后，利用超弹性本构律计算出试探应力状态（例如，试探[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}^{\text{tr}}$）。最后，检查试探应力是否满足屈服条件：$\Phi(\boldsymbol{\tau}^{\text{tr}}, \kappa^n) \le 0$？

2.  **塑性修正**：
    如果 $\Phi(\boldsymbol{\tau}^{\text{tr}}, \kappa^n) > 0$，则弹性预测无效，必须进行塑性修正。这一步的目标是找到一个增量塑性乘子 $\Delta\gamma > 0$，使得在时间步末端 $t_{n+1}$ 的状态 $(\boldsymbol{\tau}_{n+1}, \kappa_{n+1})$ 满足所有[本构方程](@entry_id:138559)。在后向欧拉格式下，这意味着所有率相关的量都取在 $t_{n+1}$ 时刻的值。我们需要求解一个[非线性](@entry_id:637147)[代数方程](@entry_id:272665)组，其核心是：
    - **一致性条件**：最终的应力状态必须位于更新后的[屈服面](@entry_id:175331)上：$\Phi(\boldsymbol{\tau}_{n+1}, \kappa_{n+1}) = 0$。
    - **离散化的演化方程**：塑性变形梯度和内变量根据[后向欧拉法](@entry_id:139674)更新。例如，[硬化](@entry_id:177483)变量的[更新方程](@entry_id:264802)为：$\kappa_{n+1} - \kappa^n - \Delta\gamma H(\boldsymbol{\tau}_{n+1}, \kappa_{n+1}) = 0$。

    对于塑性变形梯度 $\mathbf{F}_p$ 的更新，为了保持客观性，必须使用**指数映射**（exponential map） [@problem_id:3524994]：
    $ \mathbf{F}_p^{n+1} = \exp(\Delta\gamma \mathbf{N}_{n+1}) \mathbf{F}_p^n $
    其中 $\mathbf{N}_{n+1}$ 是在最终状态下计算的塑性流动方向。

这些方程构成了一个耦合的非线性系统，其未知数是最终的状态变量。这个系统通常通过牛顿-拉夫逊（[Newton-Raphson](@entry_id:177436)）等迭代方法求解。求解成功后，我们就得到了在时间步末端与总变形 $\mathbf{F}_{n+1}$ 一致的、满足所有[弹塑性](@entry_id:193198)本构关系的应力和内变量。这个将不满足屈服条件的试探应力“[拉回](@entry_id:160816)”到屈服面上的过程，正是“[返回映射](@entry_id:754324)”名称的由来。