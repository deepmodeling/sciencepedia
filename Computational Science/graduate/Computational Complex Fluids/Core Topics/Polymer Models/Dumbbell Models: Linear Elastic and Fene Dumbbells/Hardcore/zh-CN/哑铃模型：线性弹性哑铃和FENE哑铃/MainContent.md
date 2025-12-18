## 引言
[聚合物流体](@entry_id:1129919)的行为复杂而迷人，其独特的粘弹性源于其微观链状分子的[构象动力学](@entry_id:747687)。理解这种从分子尺度到宏观流动的联系，是[流变学](@entry_id:138671)、材料科学和流体力学等领域的核心挑战。为了应对这一挑战，科学家们发展了多种理论模型，其中，哑铃模型以其极致的简约和深刻的物理内涵，成为了连接微观世界与宏观现象的基石。它将复杂的聚合物链简化为一个由弹簧连接的两个珠子的力学系统，从而使我们能够解析地或半解析地探讨聚合物在流动和热涨落共同作用下的行为。然而，如何选择合适的弹簧力，以及如何从[微观动力学](@entry_id:1127874)过渡到可计算的宏观应力，引出了一系列深刻的理论问题。

本文旨在系统地阐述哑铃模型的核心理论及其应用，特别聚焦于两种最经典的弹簧模型：线性的胡克（Hookean）模型和[非线性](@entry_id:637147)的有限拉伸[非线性弹性](@entry_id:185743)（FENE）模型。通过本文的学习，您将能够掌握哑铃模型的物理图像，并理解它们在预测和解释复杂流变现象中的威力与局限。
- 在“**原理与机制**”一章中，我们将从第一性原理出发，构建哑铃模型的[动力学方程](@entry_id:751029)，深入剖析胡克弹簧与FENE弹簧的物理差异，并阐明连接微观构象与宏观应力的Kramers表达式，最终引出非线性模型所面临的“封闭问题”及其近似解。
- 随后的“**应用与跨学科交叉**”一章将展示这些模型如何用于预测剪切变稀、法向应力、应力[过冲](@entry_id:147201)等关键流变特性，并解释线圈-拉伸转变这一核心物理现象。我们还将探讨其在计算科学、生物物理等前沿领域的交叉应用。
- 最后，在“**动手实践**”部分，我们提供了一系列引导性问题，旨在帮助您通过实际计算，加深对模型[平衡态](@entry_id:270364)性质、线性响应以及其内在局限性的理解。

## 原理与机制

本章旨在阐述聚合物稀溶液的哑铃模型背后的基本原理与核心机制。我们将从构建一个聚合物链的[粗粒化](@entry_id:141933)表述出发，推导其在流动和热涨落共同作用下的[动力学方程](@entry_id:751029)。随后，我们将深入探讨两种关键的弹簧力模型——胡克（Hookean）模型和有限拉伸[非线性弹性](@entry_id:185743)（FENE）模型——的物理内涵与数学形式。最后，我们将连接微观构象与宏观应力，并讨论从精确的动力学描述过渡到可计算的宏观本构方程时所面临的“封闭问题”及其近似解。

### 哑铃模型：聚合物的[粗粒化](@entry_id:141933)表征

为了在理论上和计算上处理聚合物链在溶液中的复杂行为，我们采用一种称为**[粗粒化](@entry_id:141933)（coarse-graining）**的简化策略。哑铃模型是这种策略最简洁而深刻的体现。在该模型中，一个长而柔顺的聚合物链的所有复杂细节被简化为两个由无质量刚性杆或弹簧连接的“珠子”（beads）。

这些模型组件各自承载着明确的物理意义 ：

1.  **珠子（Beads）**：每个珠子代表了聚合物链的一部分，它是与周围溶剂流体发生水动力相互作用的中心。在稀溶液中，我们通常假设珠子之间的水动力相互作用可以忽略不计（即**自由[排泄](@entry_id:138819)近似，free-draining approximation**）。每个珠子在流体中运动时会受到一个阻力，该阻力通常由[斯托克斯定律](@entry_id:147173)（Stokes' law）描述，其大小由**珠子阻力系数 $\zeta$** 决定。

2.  **连接体（Connector）**：连接珠子的弹簧代表了连接两个亚链段的整个聚合物链的构象自由度和[熵弹性](@entry_id:151071)。它的状态由**连接体向量 $\mathbf{Q}(t) = \mathbf{r}_2(t) - \mathbf{r}_1(t)$** 描述，其中 $\mathbf{r}_1(t)$ 和 $\mathbf{r}_2(t)$ 分别是两个珠子的位置向量。$\mathbf{Q}$ 是描述聚合物内构象（如拉伸和取向）的核心变量。

3.  **弹簧力（Spring Force）**：弹簧所产生的力 $\mathbf{F}_s(\mathbf{Q})$ 是一种恢复力，它源于聚合物链的熵。当链被拉伸，远离其最概然的卷曲状态时，其[构象熵](@entry_id:170224)减少，根据[热力学原理](@entry_id:142232)，这会产生一个试图使链恢复到[无规线团](@entry_id:194950)状态的力。因此，弹簧力本质上是**[熵力](@entry_id:137746)（entropic force）**。

4.  **[热涨落](@entry_id:143642)（Thermal Fluctuations）**：溶解在流体中的聚合物链会持续不断地受到溶剂分子的随机碰撞，这导致了布朗运动。在模型中，这种效应通过一个随机热力（Brownian force）来体现，其统计性质由**涨落-耗散定理（Fluctuation-Dissipation Theorem, FDT）**确定，确保模型在没有外加流动时能够达到正确的统计力学[平衡态](@entry_id:270364)。

### 单个哑铃的动力学

现在我们构建描述连接体向量 $\mathbf{Q}$ 如何随时间演化的数学方程。

#### 力平衡与仿射形变

在[低雷诺数流](@entry_id:1127490)体中，珠子的惯性可以忽略不计（即**[过阻尼极限](@entry_id:161869)，overdamped limit**）。因此，作用在每个珠子上的力的总和为零。对于珠子 $i$（$i=1, 2$），其力[平衡方程](@entry_id:172166)（即[朗之万方程](@entry_id:144277)）为：

$$
\zeta(\dot{\mathbf{r}}_i - \mathbf{u}(\mathbf{r}_i, t)) = \mathbf{F}_{s,i} + \mathbf{F}_{B,i}(t)
$$

其中，左侧是流体施加在珠子上的[斯托克斯阻力](@entry_id:168107)，$\dot{\mathbf{r}}_i$ 是珠子速度，$\mathbf{u}(\mathbf{r}_i, t)$ 是珠子所在位置的溶剂速度。右侧 $\mathbf{F}_{s,i}$ 是弹簧对珠子 $i$ 的作用力，而 $\mathbf{F}_{B,i}(t)$ 是作用在珠子 $i$ 上的随机布朗力。根据[牛顿第三定律](@entry_id:166652)，$\mathbf{F}_{s,1} = -\mathbf{F}_{s,2}$。我们通常将弹簧对珠子2的作用力定义为弹簧力 $\mathbf{F}_s(\mathbf{Q})$，因此对珠子1的作用力为 $-\mathbf{F}_s(\mathbf{Q})$。

溶剂的流动如何影响哑铃的构象？我们考虑一个宏观均匀的流动，其特征是[速度梯度张量](@entry_id:270928) $\boldsymbol{\kappa}(t) = \nabla \mathbf{u}$。假设聚合物的尺寸（由 $|\mathbf{Q}|$ 表征）远小于[速度梯度](@entry_id:261686)发生显著变化的宏观长度尺度，我们可以对珠子2相对于珠子1的[流体速度](@entry_id:267320)差进行一阶[泰勒展开](@entry_id:145057) ：

$$
\mathbf{u}(\mathbf{r}_2, t) - \mathbf{u}(\mathbf{r}_1, t) = \mathbf{u}(\mathbf{r}_1 + \mathbf{Q}, t) - \mathbf{u}(\mathbf{r}_1, t) \approx (\nabla \mathbf{u})|_{\mathbf{r}_1} \cdot \mathbf{Q} = \boldsymbol{\kappa}(t) \cdot \mathbf{Q}
$$

这个关系被称为**仿射形变（affine deformation）**。它意味着，仅考虑流场的运动学效应时，连接体向量 $\mathbf{Q}$ 的端点就像嵌入连续介质中的物质点一样，被宏观[速度梯度](@entry_id:261686)拉伸和旋转。这一假设是稀溶液动理学理论的基石，它将宏观流动与微观[结构动力学](@entry_id:172684)联系起来。它的有效性依赖于稀溶液条件（$c \ll c^*$）、[蠕动流](@entry_id:263844)（$Re \ll 1$）以及聚合物尺寸与流动梯度特征长度之间的尺度分离。

#### 连接体向量的随机微分方程

为了得到 $\mathbf{Q}$ 的演化方程，我们将珠子2和珠子1的力平衡方程相减 ：

$$
\zeta(\dot{\mathbf{r}}_2 - \dot{\mathbf{r}}_1) - \zeta(\mathbf{u}(\mathbf{r}_2) - \mathbf{u}(\mathbf{r}_1)) = (\mathbf{F}_{s,2} - \mathbf{F}_{s,1}) + (\mathbf{F}_{B,2} - \mathbf{F}_{B,1})
$$

利用 $\dot{\mathbf{Q}} = \dot{\mathbf{r}}_2 - \dot{\mathbf{r}}_1$、仿射形变近似、以及弹簧力的关系，上式变为：

$$
\zeta(\dot{\mathbf{Q}} - \boldsymbol{\kappa} \cdot \mathbf{Q}) = 2\mathbf{F}_s(\mathbf{Q}) + (\mathbf{F}_{B,2} - \mathbf{F}_{B,1})
$$

整理后得到：

$$
\dot{\mathbf{Q}} = \boldsymbol{\kappa} \cdot \mathbf{Q} + \frac{2}{\zeta}\mathbf{F}_s(\mathbf{Q}) + \frac{1}{\zeta}(\mathbf{F}_{B,2} - \mathbf{F}_{B,1})
$$

随机力 $\mathbf{F}_{B,i}$ 是[高斯白噪声](@entry_id:749762)，其统计特性由涨落-耗散定理给出：$\langle \mathbf{F}_{B,i}(t) \rangle = \mathbf{0}$ 且 $\langle \mathbf{F}_{B,i}(t) \mathbf{F}_{B,j}(t')^T \rangle = 2k_B T \zeta \mathbf{I} \delta_{ij} \delta(t-t')$，其中 $k_B$ 是[玻尔兹曼常数](@entry_id:142384)，$T$ 是[绝对温度](@entry_id:144687)，$\mathbf{I}$ 是单位张量。由于两个珠子的[热涨落](@entry_id:143642)是[相互独立](@entry_id:273670)的，相对随机力 $(\mathbf{F}_{B,2} - \mathbf{F}_{B,1})$ 的协方差是各[自协方差](@entry_id:270483)之和，即 $4k_B T \zeta \mathbf{I} \delta(t-t')$。

因此，连接体向量的最终随机微分方程（SDE）为  ：

$$
d\mathbf{Q} = \left( \boldsymbol{\kappa} \cdot \mathbf{Q} + \frac{2}{\zeta}\mathbf{F}_s(\mathbf{Q}) \right) dt + \sqrt{\frac{4k_B T}{\zeta}} d\mathbf{W}(t)
$$

其中 $d\mathbf{W}(t)$ 是一个标准矢量[维纳过程](@entry_id:137696)的增量。这个方程优雅地概括了驱动[聚合物构象](@entry_id:180389)演化的三种核心机制：由宏观流动引起的仿射拉伸和旋转（$\boldsymbol{\kappa} \cdot \mathbf{Q}$ 项），由[熵弹性](@entry_id:151071)产生的恢复力（$\mathbf{F}_s(\mathbf{Q})$ 项），以及由溶剂[分子碰撞](@entry_id:137334)引起的随机扩散（噪声项）。请注意弹簧力项前面的因子 $2$ 和噪声项中根号下的因子 $4$，它们都源于哑铃模型包含两个独立的珠子这一事实。

### [熵弹簧](@entry_id:136248)力的模型

弹簧力 $\mathbf{F}_s(\mathbf{Q})$ 的具体形式取决于我们如何对聚合物链的[熵弹性](@entry_id:151071)进行建模。它通常由一个势能函数 $U(\mathbf{Q})$ 导出：$\mathbf{F}_s(\mathbf{Q}) = -\nabla_{\mathbf{Q}} U(\mathbf{Q})$。

#### 胡克（Hookean）弹簧

最简单的模型是**胡克弹簧**，其势能为：

$$
U_H(\mathbf{Q}) = \frac{1}{2} H |\mathbf{Q}|^2
$$

其中 $H$ 是[弹簧常数](@entry_id:167197)。这对应于一个线性力：

$$
\mathbf{F}_s^H(\mathbf{Q}) = -H\mathbf{Q}
$$

胡克模型在物理上对应于理想[高斯链](@entry_id:154876)的近似，即链的构象分布是高斯分布。这个模型的优点是其线性性质使得相关的动力学方程和应力表达式变得数学上易于处理。然而，它有一个显著的缺陷：它允许链被无限拉伸，这与[真实聚合物链](@entry_id:1130709)具有有限轮廓长度的物理事实相悖。

#### 有限拉伸[非线性弹性](@entry_id:185743)（FENE）弹簧

为了克服胡克模型的非物理性，**FENE模型**被引入。它采用了一个更真实的[非线性弹簧](@entry_id:173069)力。一个标准的[FENE势](@entry_id:1124903)能函数是 ：

$$
U_F(\mathbf{Q}) = -\frac{1}{2} H Q_0^2 \ln\left(1 - \frac{|\mathbf{Q}|^2}{Q_0^2}\right)
$$

其中 $Q_0$ 是哑铃的最大可能拉伸长度，对应于聚合物链完全伸直时的长度。当 $|\mathbf{Q}|$ 趋近于 $Q_0$ 时，势能 $U_F$ 趋于无穷大。

对应的弹簧力为：

$$
\mathbf{F}_s^F(\mathbf{Q}) = -\frac{H\mathbf{Q}}{1 - |\mathbf{Q}|^2/Q_0^2}
$$

这个力具有两个重要的特性：

1.  **与胡克模型的联系**：当拉伸程度很小（$|\mathbf{Q}| \ll Q_0$）时，我们可以对分母进行[泰勒展开](@entry_id:145057) $(1-x)^{-1} \approx 1+x+\dots$。此时，FENE力近似为 $\mathbf{F}_s^F(\mathbf{Q}) \approx -H\mathbf{Q}(1 + |\mathbf{Q}|^2/Q_0^2) = -H\mathbf{Q} - \frac{H}{Q_0^2}|\mathbf{Q}|^2\mathbf{Q}$。其[主导项](@entry_id:167418) $-H\mathbf{Q}$ 与胡克力完全相同，表明FENE模型在小变形下恢复到[线性弹性](@entry_id:166983)行为。第一个[非线性](@entry_id:637147)修正项为 $- \frac{H}{Q_0^2}|\mathbf{Q}|^2\mathbf{Q}$，它是一个三次项，表示了偏离线性行为的开始 。

2.  **有限拉伸性**：当 $|\mathbf{Q}|$ 接近 $Q_0$ 时，分母趋于零，导致恢复力 $\mathbf{F}_s^F$ 的大小急剧地、无界地增长。这种力的**发散（divergence）**是FENE模型的核心特征，它在数学上强制哑铃的长度不能超过 $Q_0$，从而正确地反映了[真实聚合物链](@entry_id:1130709)的有限轮廓长度。

FEN[E模](@entry_id:160271)型通过一个[无量纲参数](@entry_id:169335) $b$ 来表征，该参数定义为 ：

$$
b = \frac{H Q_0^2}{k_B T}
$$

（在三维空间中，有时会包含一个因子3，即 $b=HQ_0^2/(3k_BT)$，这取决于具体文献的定义约定）。这个参数 $b$ 衡量了在最大拉伸长度 $Q_0$ 处的弹性势能尺度（以 $\frac{1}{2}HQ_0^2$ 为代表）与热能尺度 $k_B T$ 之间的比率。
*   当 $b \gg 1$ 时，意味着链非常“硬”，弹性势能远大于热能。在这种情况下，[热涨落](@entry_id:143642)只能在远小于 $Q_0$ 的范围内探索构象，哑铃的行为在绝大多数情况下近似于胡克弹簧，只有在极强的流动作用下，[非线性](@entry_id:637147)效应才会显现。
*   当 $b = \mathcal{O}(10)$ 或更小时，意味着链相对“软”，热能与[弹性势能](@entry_id:168893)的尺度相当。即使在适度的流动下，哑铃也可能被拉伸到其[非线性响应](@entry_id:188175)区域，因此有限拉伸效应更为显著。

### 从微观构象到宏观应力

哑铃模型最重要的应用之一是预测[聚合物溶液](@entry_id:145399)的宏观[流变性](@entry_id:152243)质，如粘度和[法向应力差](@entry_id:199507)。这需要建立微观构象与宏观[应力张量](@entry_id:148973)之间的联系。

#### Kramers应力表达式与[平衡态](@entry_id:270364)

聚合物对总应力张量的贡献，即**聚合物额外应力 $\boldsymbol{\tau}_p$**，可以通过Kramers表达式给出。一个普遍接受的形式是：

$$
\boldsymbol{\tau}_p = n \langle \mathbf{Q} \mathbf{F}_s^T \rangle - n k_B T \mathbf{I}
$$

其中 $n$ 是单位体积内哑铃的数量，$\langle \cdot \rangle$ 表示对所有哑铃构象的系综平均。这个表达式由两部分组成：第一项 $n \langle \mathbf{Q} \mathbf{F}_s^T \rangle$ 是** virial应力**，源于弹簧力在分子间传递的动量；第二项 $-n k_B T \mathbf{I}$ 是一个各向同性的贡献。

这个各向同性项的存在至关重要，它保证了在没有流动（quiescent equilibrium）的[平衡态](@entry_id:270364)下，聚合物的额外应力为零 。在[平衡态](@entry_id:270364)，构象的概率分布遵循玻尔兹曼分布 $\psi_{eq}(\mathbf{Q}) \propto \exp(-U(\mathbf{Q})/k_B T)$。通过分部积分可以证明一个非常普适的结论：

$$
\langle \mathbf{Q} \mathbf{F}_s^T \rangle_{eq} = \langle \mathbf{Q} (-\nabla_{\mathbf{Q}} U)^T \rangle_{eq} = k_B T \mathbf{I}
$$

这个结果与弹簧势能 $U(\mathbf{Q})$ 的具体形式无关，无论是胡克势还是[FENE势](@entry_id:1124903)都成立。将此结果代入Kramers表达式，我们得到 $\boldsymbol{\tau}_{p, eq} = n(k_B T \mathbf{I}) - n k_B T \mathbf{I} = \mathbf{0}$。因此，$-n k_B T \mathbf{I}$ 项可以被理解为哑铃作为溶质粒子的动能（或渗透压）贡献，它在[平衡态](@entry_id:270364)下恰好抵消了弹簧力的平均 virial 贡献。

#### 强流场下的行为：拉伸灾变

胡克模型和FENE模型在强流场下的预测行为截然不同。考虑一个强的[单轴拉伸](@entry_id:188287)流，其特征是拉伸速率 $\dot{\epsilon}$。
*   对于**胡克哑铃**，当拉伸速率超过一个临界值时（具体为 $\dot{\epsilon} \ge 1/(2\lambda_H)$，其中 $\lambda_H$ 是胡克哑铃的松弛时间），其线性恢复力不足以抵抗流场的强烈拉伸。模型会预测哑铃的平均拉伸长度 $\langle |\mathbf{Q}|^2 \rangle$ 和聚合物应力会发散到无穷大。这种非物理的预测被称为**拉伸灾变（extensional catastrophe）**。
*   对于**FENE哑铃**，情况则大为改观。由于其弹簧力在 $|\mathbf{Q}| \to Q_0$ 时会发散，它总能提供足够强大的恢复力来对抗任何强度的流场拉伸 。这保证了哑铃的平均拉伸长度 $\langle |\mathbf{Q}|^2 \rangle$ 始终有界（小于 $Q_0^2$），从而聚合物应力和[拉伸粘度](@entry_id:1124791)在所有拉伸速率下都保持有限。FEN[E模](@entry_id:160271)型因此成功地“修正”了胡克模型的拉伸灾变，更真实地描述了聚合物在强拉伸流中的行为。

### 封闭问题与[本构模型](@entry_id:174726)

虽然我们有了描述单个哑铃构象演化的SDE，但要计算宏观应力，我们需要的是系综平均量，如构象张量 $\mathbf{A}(t) = \langle \mathbf{Q} \mathbf{Q}^T \rangle$。通过对SDE进行平均，我们可以推导出 $\mathbf{A}(t)$ 的演化方程。然而，这一过程引出了所谓的**封闭问题（closure problem）**。

从SDE出发，可以推导出[构象张量](@entry_id:1122882) $\mathbf{A}$ 的精确演化方程形如：

$$
\frac{d\mathbf{A}}{dt} - \boldsymbol{\kappa}\cdot\mathbf{A} - \mathbf{A}\cdot\boldsymbol{\kappa}^T = -\frac{4}{\zeta} \langle \mathbf{Q} \mathbf{F}_s^T \rangle + \frac{4k_B T}{\zeta} \mathbf{I}
$$

这里的核心问题在于如何处理平均项 $\langle \mathbf{Q} \mathbf{F}_s^T \rangle$ 。

*   **胡克模型（精确封闭）**：对于胡克弹簧，$\mathbf{F}_s = -H\mathbf{Q}$。由于力的线性性质，平均项可以精确地写成 $\langle \mathbf{Q} \mathbf{F}_s^T \rangle = \langle \mathbf{Q} (-H\mathbf{Q})^T \rangle = -H \langle \mathbf{Q} \mathbf{Q}^T \rangle = -H\mathbf{A}$。因此，$\mathbf{A}$ 的[演化方程](@entry_id:268137)只依赖于 $\mathbf{A}$ 自身，形成一个封闭的、可解的[微分方程组](@entry_id:148215)。同样，应力也可以直接表示为 $\mathbf{A}$ 的函数。

*   **FENE模型（封闭问题）**：对于FENE弹簧，$\mathbf{F}_s = -H f(|\mathbf{Q}|^2)\mathbf{Q}$，其中 $f(|\mathbf{Q}|^2) = (1-|\mathbf{Q}|^2/Q_0^2)^{-1}$。平均项变为 $\langle \mathbf{Q} \mathbf{F}_s^T \rangle = -H \langle f(|\mathbf{Q}|^2) \mathbf{Q} \mathbf{Q}^T \rangle$。由于 $f$ 是 $|\mathbf{Q}|^2$ 的[非线性](@entry_id:637147)函数，一般而言，乘积的平均不等于平均的乘积，即 $\langle f(|\mathbf{Q}|^2) \mathbf{Q} \mathbf{Q}^T \rangle \neq \langle f(|\mathbf{Q}|^2) \rangle \langle \mathbf{Q} \mathbf{Q}^T \rangle$。这个平均项依赖于比二阶矩 $\mathbf{A}$ 更高阶的构象信息，因此 $\mathbf{A}$ 的[演化方程](@entry_id:268137)不是封闭的。

为了得到一个可用的FENE本构模型，必须引入**封闭近似（closure approximation）**来用低阶矩（如 $\mathbf{A}$）近似表达高阶矩项。

*   **[Peterlin近似](@entry_id:1129541)**：一个广泛应用的近似是**[Peterlin近似](@entry_id:1129541)**（或称预平均近似），它将耦合的平均项[解耦](@entry_id:160890) ：
    $$
    \langle f(|\mathbf{Q}|^2) \mathbf{Q} \mathbf{Q}^T \rangle \approx \langle f(|\mathbf{Q}|^2) \rangle \mathbf{A}
    $$
    并进一步用 $\mathbf{A}$ 的迹（trace）来近似标量平均项：
    $$
    \langle f(|\mathbf{Q}|^2) \rangle \approx f(\langle |\mathbf{Q}|^2 \rangle) = f(\text{tr}(\mathbf{A})) = \frac{1}{1 - \text{tr}(\mathbf{A})/Q_0^2}
    $$
    这种近似使得FEN[E模](@entry_id:160271)型的构象方程和应力表达式都变成了关于 $\mathbf{A}$ 的[封闭形式](@entry_id:272960)，从而可以进行数值求解。该近似保持了模型的客观性（rotational covariance），并在 $Q_0 \to \infty$ 的极限下能正确退化到胡克模型。

*   **FENE-P与[FENE-CR模型](@entry_id:1124901)**：基于[Peterlin近似](@entry_id:1129541)，发展出了不同的本构模型。其中两种常见的模型是FENE-P和FENE-CR 。
    *   **FENE-P (Peterlin)** 模型将[Peterlin近似](@entry_id:1129541)一致地应用于构象方程和应力表达式中。其松弛项的形式为 $\propto (f(\text{tr}\mathbf{A})\mathbf{A} - \mathbf{I})$，应力也与该项成正比。
    *   **FENE-CR (Chilcott-Rallison)** 模型则是一种更具启发性的构造。它保留了胡克模型（即[Oldroyd-B模型](@entry_id:752895)）的应力表达式形式 $\boldsymbol{\tau}_p \propto (\mathbf{A} - \mathbf{I})$，但将构象方程中的松弛项乘以了[非线性](@entry_id:637147)因子 $f(\text{tr}\mathbf{A})$，使其形式变为 $\propto f(\text{tr}\mathbf{A})(\mathbf{A} - \mathbf{I})$。这相当于引入了一个依赖于构象的松弛时间。

这些近似模型虽然牺牲了动理学理论的精确性，但它们在保留有限拉伸性这一关键物理特性的同时，提供了计算上可行且在许多[流变学](@entry_id:138671)应用中表现良好的宏观本构方程。