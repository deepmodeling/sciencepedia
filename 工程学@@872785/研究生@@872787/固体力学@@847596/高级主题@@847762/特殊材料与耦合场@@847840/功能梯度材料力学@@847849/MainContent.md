## 引言
[功能梯度材料](@entry_id:157846)（Functionally Graded Materials, FGM）代表了一类先进的[复合材料](@entry_id:139856)，其成分和微观结构在空间上呈连续性梯度变化，从而使其宏观材料属性（如[弹性模量](@entry_id:198862)、[热导率](@entry_id:147276)、硬度等）也表现出平滑的过渡。这种独特的设计理念克服了传统[复合材料](@entry_id:139856)在界面处因属性突变而引发的[应力集中](@entry_id:160987)和过早失效等瓶颈，为在极端环境下服役的结构提供了前所未有的设计自由度。然而，要充分发挥其潜力，就必须建立一个能够精确描述其复杂力学行为的系统性理论框架，这正是当前[固体力学](@entry_id:164042)研究中的一个重要课题。

本文旨在为研究生及相关领域的研究人员提供一个关于[功能梯度材料](@entry_id:157846)力学的全面而深入的指南。我们将从最基本的力学原理出发，逐步构建分析和设计功能梯度结构的完整知识体系。
*   在**原理与机制**一章中，我们将奠定理论基石，详细推导FGM的[本构关系](@entry_id:186508)、平衡控制方程，并探讨其[微观力学](@entry_id:195009)起源，为理解其独特的力学行为提供数学和物理基础。
*   接下来，在**应用与跨学科连接**一章中，我们将展示这些原理如何应用于解决实际工程问题，包括[热应力](@entry_id:180613)管理、结构稳定性分析、断裂与[损伤容限设计](@entry_id:193674)，并探索其在[生物力学](@entry_id:153973)和智能材料等前沿领域的深刻联系。
*   最后，通过**动手实践**部分提供的一系列计算问题，读者将有机会亲手应用所学知识，加深对核心概念的理解。

让我们从[功能梯度材料](@entry_id:157846)力学的基本原理与核心机制开始，深入探索这一迷人领域。

## 原理与机制

本章旨在深入探讨[功能梯度材料](@entry_id:157846)（Functionally Graded Materials, FGM）力学行为背后的基本原理与核心机制。在前一章介绍其背景与应用之后，我们将系统性地建立描述 FGM 行为的数学与物理框架。我们将从连续介质力学的角度出发，定义其本构关系，推导其平衡控制方程，并探讨其微观结构与宏观性能之间的联系。随后，我们将这些基本原理应用于[热弹性](@entry_id:158447)问题及梁、板等典型结构元件的分析中，最后以对解的数学正则性的讨论作为本章的收尾，从而为研究生层次的读者提供一个严谨且全面的理论基础。

### 功能梯度弹性力学的本构框架

在连续介质力学框架下，[功能梯度材料](@entry_id:157846)最核心的特征在于其材料属性是空间位置的[光滑函数](@entry_id:267124)。这与传统[复合材料](@entry_id:139856)中材料属性在相界面上发生阶跃式突变形成鲜明对比。对于一个处于小应变状态下的线性弹性功能梯度体，其任意一点 $\boldsymbol{x}$ 的应力状态与应变状态之间的关系，可以通过一个依赖于位置的[局部线性](@entry_id:266981)[本构关系](@entry_id:186508)来描述。

假设不存在[体力](@entry_id:174230)偶，柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$（分量为 $\sigma_{ij}$）与[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon}$（分量为 $\varepsilon_{ij}$）是[功共轭](@entry_id:194957)的。若材料是超弹性的，则存在一个[应变能密度函数](@entry_id:755490) $W(\boldsymbol{x}, \boldsymbol{\varepsilon})$，其不仅依赖于应变，也显式地依赖于空间位置 $\boldsymbol{x}$。对于[线性弹性](@entry_id:166983)响应，该[本构关系](@entry_id:186508)可以写作：

$$
\sigma_{ij}(\boldsymbol{x}) = C_{ijkl}(\boldsymbol{x}) \varepsilon_{kl}(\boldsymbol{x})
$$

此式是胡克定律在非均匀材料中的直接推广。其中，$C_{ijkl}(\boldsymbol{x})$ 是四阶**[弹性张量](@entry_id:170728)场**。要完整地定义一个功能梯度弹性体，我们必须明确该张量场必须满足的对称性与稳定性条件 [@problem_id:2660853]。

1.  **次对称性 (Minor Symmetries)**：[弹性张量](@entry_id:170728)的次对称性源于[应力张量和应变张量](@entry_id:755512)自身的对称性，这一性质与材料是否均匀无关。
    *   在没有体力偶的情况下，动量矩平衡要求柯西[应力张量](@entry_id:148973)必须是对称的，即 $\sigma_{ij} = \sigma_{ji}$。
    *   [小应变张量](@entry_id:754968)根据其定义 $\varepsilon_{ij} = \frac{1}{2}(\partial u_i / \partial x_j + \partial u_j / \partial x_i)$，天然就是对称的，即 $\varepsilon_{ij} = \varepsilon_{ji}$。
    *   这些对称性要求[弹性张量](@entry_id:170728)必须满足**次对称性**：$C_{ijkl}(\boldsymbol{x}) = C_{jikl}(\boldsymbol{x})$ 和 $C_{ijkl}(\boldsymbol{x}) = C_{ijlk}(\boldsymbol{x})$。这意味着，在 81 个分量中，只有 36 个是独立的。

2.  **主对称性 (Major Symmetry)**：主对称性是超弹性（即存在[应变能密度函数](@entry_id:755490)）的直接结果。[应力张量](@entry_id:148973)可以通过[应变能密度](@entry_id:200085)对应变求导得到：$\sigma_{ij} = \frac{\partial W}{\partial \varepsilon_{ij}}$。对于[线性弹性](@entry_id:166983)材料，[应变能密度](@entry_id:200085)是应变的二次型：
    $$
    W(\boldsymbol{x}, \boldsymbol{\varepsilon}) = \frac{1}{2} \varepsilon_{ij} C_{ijkl}(\boldsymbol{x}) \varepsilon_{kl}
    $$
    为了使[应力与应变](@entry_id:137374)能函数的关系得以满足，[弹性张量](@entry_id:170728)必须是[应变能密度](@entry_id:200085)对应变的[二阶导数](@entry_id:144508)：$C_{ijkl}(\boldsymbol{x}) = \frac{\partial^2 W}{\partial \varepsilon_{ij} \partial \varepsilon_{kl}}$。对于一个行为良好的能量函数，求导次序可以交换，即 $\frac{\partial^2 W}{\partial \varepsilon_{ij} \partial \varepsilon_{kl}} = \frac{\partial^2 W}{\partial \varepsilon_{kl} \partial \varepsilon_{ij}}$。这直接导出了**主对称性**：
    $$
    C_{ijkl}(\boldsymbol{x}) = C_{klij}(\boldsymbol{x})
    $$
    值得强调的是，超弹性是一个**局部**概念，因此即使材料属性随空间变化，主对称性在每一点 $\boldsymbol{x}$ 上依然成立。材料的非[均匀性](@entry_id:152612)不会破坏主对称性。主对称性将[独立弹性常数](@entry_id:203649)的数量从 36 个减少到 21 个。

3.  **点态[正定性](@entry_id:149643) (Pointwise Positive-Definiteness)**：为了保证材料的内在稳定性，任何非零的应变状态都必须对应一个正的储蓄应变能。这意味着[应变能密度函数](@entry_id:755490)必须是正定的。对于[线性弹性](@entry_id:166983)材料，这转化为对[弹性张量](@entry_id:170728)的要求：
    $$
    \varepsilon_{ij} C_{ijkl}(\boldsymbol{x}) \varepsilon_{kl} > 0, \quad \forall \boldsymbol{\varepsilon} \neq \mathbf{0}
    $$
    这个条件被称为**点态严格正定性**，它必须在材料域内的每一点 $\boldsymbol{x}$ 都得到满足。一个较弱的半正定条件（$\ge 0$）将允许在零能量消耗下产生非零变形，这对应于材料失稳（[软模式](@entry_id:137007)）。同样，一个关于能量在整个区域上积分的全局条件（例如，$\int_{\Omega} W \, \mathrm{d}V > 0$）也不足以保证[材料稳定性](@entry_id:183933)，因为它可能允许局部区域的失稳。

综上所述，一个线性超弹性[功能梯度材料](@entry_id:157846)在每一点 $\boldsymbol{x}$ 都由一个满足次对称性、主对称性和严格正定性的[四阶弹性张量](@entry_id:188318) $C_{ijkl}(\boldsymbol{x})$ 所描述 [@problem_id:2660853]。

### 平衡控制方程

定义了本构关系之后，我们需将其纳入平衡方程中，以构建边值问题的完整数学描述。在准静态、小应变假设下，局部[线性[动量平](@entry_id:193575)衡](@entry_id:193575)（或称力平衡）方程为：

$$
\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \mathbf{0} \quad \text{或} \quad \sigma_{ij,j} + b_i = 0
$$

其中 $\boldsymbol{b}$ 是单位体积的体力。这个形式的平衡方程对于任何连续介质都是普适的。

当我们将 FGM 的本构关系 $\sigma_{ij} = C_{ijkl}(\boldsymbol{x}) \varepsilon_{kl}(\boldsymbol{u})$ 代入时，可以得到以位移场 $\boldsymbol{u}$ 为未知量的控制方程。一个关键且微妙的问题随之出现：材料属性的空间梯度 $\nabla C$ 如何体现在方程中？[@problem_id:2660858] [@problem_id:2660862]

将本构关系代入平衡方程，得到：

$$
\nabla \cdot (\mathbb{C}(\boldsymbol{x}) : \boldsymbol{\varepsilon}(\boldsymbol{u})) + \boldsymbol{b} = \mathbf{0}
$$

这是一个[散度形式](@entry_id:748608)的方程。若我们利用求导的乘法法则展开散度项，可以更清晰地看到材料梯度的影响。在[指标记法](@entry_id:191923)下：

$$
(\sigma_{ij})_{,j} = (C_{ijkl}(\boldsymbol{x}) \varepsilon_{kl}(\boldsymbol{u}))_{,j} = C_{ijkl,j}(\boldsymbol{x}) \varepsilon_{kl} + C_{ijkl}(\boldsymbol{x}) \varepsilon_{kl,j}
$$

完整的平衡方程（用位移表示）变为：

$$
C_{ijkl}(\boldsymbol{x}) u_{k,lj} + C_{ijkl,j}(\boldsymbol{x}) u_{k,l} + b_i = 0
$$

（这里利用了对称性进行了简化）。从中我们可以清楚地看到，出现了包含[弹性张量](@entry_id:170728)梯度 $C_{ijkl,j}(\boldsymbol{x})$ 的项。这一项有时被通俗地称为“伪[体力](@entry_id:174230)”(fictitious body force)，因为它与[体力](@entry_id:174230)项 $b_i$ 相加。然而，这种称谓具有误导性。真正的**体力**项 $\boldsymbol{b}$ 是独立于物体响应（即位移场 $\boldsymbol{u}$）的外部载荷。而项 $C_{ijkl,j}(\boldsymbol{x}) \varepsilon_{kl}$ 依赖于应变 $\boldsymbol{\varepsilon}$，因此也依赖于未知的[位移场](@entry_id:141476) $\boldsymbol{u}$。所以，它并非一个新的载荷项，而是作用于位移场 $\boldsymbol{u}$ 的**变系数微分算子**的一部分。它改变了[偏微分方程](@entry_id:141332)中关于位移[一阶导数](@entry_id:749425)的系数 [@problem_id:2660858]。

从[变分原理](@entry_id:198028)的角度看，这一结论更为自然。物体的总势能泛函为：

$$
\Pi[\boldsymbol{u}] = \int_{\Omega} \frac{1}{2} \boldsymbol{\varepsilon}(\boldsymbol{u}) : \mathbb{C}(\boldsymbol{x}) : \boldsymbol{\varepsilon}(\boldsymbol{u}) \, \mathrm{d}\Omega - \int_{\Omega} \boldsymbol{b} \cdot \boldsymbol{u} \, \mathrm{d}\Omega - \int_{\Gamma_{t}} \bar{\boldsymbol{t}} \cdot \boldsymbol{u} \, \mathrm{d}\Gamma
$$

通过对位移变分 $\delta \boldsymbol{u}$ 取[极值](@entry_id:145933)（$\delta \Pi = 0$），并利用[分部积分](@entry_id:136350)和[散度定理](@entry_id:143110)，可以直接得到[平衡方程](@entry_id:172166)的[弱形式](@entry_id:142897)，并最终导出其强形式 $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \mathbf{0}$ 以及自然边界条件 $\boldsymbol{\sigma} \cdot \boldsymbol{n} = \bar{\boldsymbol{t}}$。在此推导过程中，变分和[分部积分](@entry_id:136350)是作用在位移场 $\boldsymbol{u}$ 及其变分 $\delta \boldsymbol{u}$ 上的，而不是作用在固定的材料属性场 $\mathbb{C}(\boldsymbol{x})$ 上。因此，$\nabla \mathbb{C}$ 项不会在最终的[散度形式](@entry_id:748608)平衡方程中显式出现。只有当我们选择将 $\boldsymbol{\sigma}$ 用位移 $\boldsymbol{u}$ 展开时，$\nabla \mathbb{C}$ 才作为[微分算子](@entry_id:140145)的一部分出现 [@problem_id:2660862]。这种[散度形式](@entry_id:748608)对于有限元等数值方法的建立至关重要。

### [微观力学](@entry_id:195009)起源与均匀化方法

[功能梯度材料](@entry_id:157846)的宏观属性梯度，源于其微观组分的[体积分数](@entry_id:756566)或微观结构的连续变化。为了在设计和分析 FGM 时能够预测其有效的宏观属性，我们需要借助**均匀化**理论。其基本思想在于，对包含微观非均匀结构的[代表性体积元](@entry_id:164290)（Representative Volume Element, RVE）进行分析，从而得到其等效的、均匀的宏观[力学性能](@entry_id:201145)。对于 FGM 而言，这意味着在每一个宏观点 $\boldsymbol{x}$，都存在一个虚拟的 RVE，其微观结构（如组分相的[体积分数](@entry_id:756566)）由该点的位置决定。

考虑一个由两种[各向同性线弹性](@entry_id:185899)相（相1和相2）组成的 FGM 板，其厚度为 $h$，坐标为 $z \in [-h/2, h/2]$。假设相1作为球形夹杂，弥散在相2基体中，其体积分数 $c(z)$ 随厚度变化，例如遵循[幂律分布](@entry_id:262105) [@problem_id:2660857]：

$$
c(z) = \left(\frac{z + h/2}{h}\right)^{n}, \quad n>0
$$

这使得板的底部 ($z=-h/2$) 为纯粹的相2 ($c=0$)，顶部 ($z=h/2$) 为纯粹的相1 ($c=1$)。我们的目标是确定在任意厚度位置 $z$ 的[有效弹性模量](@entry_id:181086) $E(z)$。

最简单的均匀化模型是**混合率 (Rule of Mixtures)**，也称为 **Voigt 模型**。它假设在 RVE 中所有组分承受相同的应变。这导致有效[弹性张量](@entry_id:170728)是各组分[弹性张量](@entry_id:170728)的体积分数加权平均。对于[杨氏模量](@entry_id:140430)，这通常简化为：

$$
E_{\mathrm{V}}(z) = c(z) E_1 + (1-c(z)) E_2
$$

Voigt 模型提供了一个[运动学](@entry_id:173318)上容许的应变场，但通常不满足应[力平衡](@entry_id:267186)，因此其预测结果是有效刚度的**上界**。

一个更精确的模型是 **Mori-Tanaka (MT) 格式**。它是一种考虑了基体与夹杂之间相互作用的[平均场方法](@entry_id:141668)。它将夹杂物视为嵌入在一个承受着[复合材料](@entry_id:139856)中基体相所经历的平均应变的无限大基体中。对于球形夹杂，MT 格式给出了有效体积模量 $K_{\mathrm{MT}}(z)$ 和剪切模量 $G_{\mathrm{MT}}(z)$ 的显式表达式：

$$
K_{\mathrm{MT}}(z) = K_{2} + \frac{c(z)(K_{1} - K_{2})}{1 + (1 - c(z))\frac{K_{1} - K_{2}}{K_{2} + \frac{4}{3}G_{2}}}
$$

$$
G_{\mathrm{MT}}(z) = G_{2} + \frac{c(z)(G_{1} - G_{2})}{1 + (1 - c(z))\frac{G_{1} - G_{2}}{G_{2} + \beta_{2}}}
$$

其中 $\beta_{2} = \frac{G_{2}(9K_{2} + 8G_{2})}{6(K_{2} + 2G_{2})}$ 是一个依赖于基体（相2）属性的因子，与 Eshelby 夹杂问题相关。一旦得到 $K_{\mathrm{MT}}(z)$ 和 $G_{\mathrm{MT}}(z)$，有效的杨氏模量就可以通过标准公式计算：

$$
E_{\mathrm{MT}}(z) = \frac{9 K_{\mathrm{MT}}(z) G_{\mathrm{MT}}(z)}{3 K_{\mathrm{MT}}(z) + G_{\mathrm{MT}}(z)}
$$

与 Voigt 模型不同，Mori-Tanaka 模型的结果依赖于哪一相是基体，哪一相是夹杂，这反映了真实的物理情况。其预测值通常位于 Voigt [上界](@entry_id:274738)和 Reuss 下界（基于[等应力](@entry_id:204402)假设）之间，被认为是对于中等体积分数下颗粒增强[复合材料](@entry_id:139856)的一个相当准确的估计。两种模型预测值的差异在两相模量差异较大且[体积分数](@entry_id:756566)居中时最为显著 [@problem_id:2660857]。

### FGM 的[热弹性](@entry_id:158447)行为

[功能梯度材料](@entry_id:157846)最成功的应用之一是在高温环境中管理[热应力](@entry_id:180613)。这得益于其平滑变化的材料属性可以缓和由不同材料热膨胀失配引起的应力集中。为了分析这类问题，我们需要将热效用纳入本构框架。

在小应变线性热弹性理论中，总应变张量 $\varepsilon_{ij}$ 可以分解为**[弹性应变](@entry_id:189634)** $\varepsilon^{e}_{ij}$ 和**[热应变](@entry_id:187744)** $\varepsilon^{\theta}_{ij}$ 之和：

$$
\varepsilon_{ij}(\boldsymbol{x}) = \varepsilon^{e}_{ij}(\boldsymbol{x}) + \varepsilon^{\theta}_{ij}(\boldsymbol{x})
$$

应力仅由[弹性应变](@entry_id:189634)产生，因此胡克定律写为 $\sigma_{ij}(\boldsymbol{x}) = C_{ijkl}(\boldsymbol{x}) \varepsilon^{e}_{kl}(\boldsymbol{x})$。将[应变分解](@entry_id:186005)式代入，我们得到[热弹性](@entry_id:158447)[本构方程](@entry_id:138559)：

$$
\sigma_{ij}(\boldsymbol{x}) = C_{ijkl}(\boldsymbol{x}) \left[ \varepsilon_{kl}(\boldsymbol{x}) - \varepsilon^{\theta}_{kl}(\boldsymbol{x}) \right]
$$

这里的关键是确定 FGM 的[热应变](@entry_id:187744)项。对于在每一点都局部各向同性的材料，一个均匀的温度变化 $\Delta T$ 会引起在所有方向上相同的[自由膨胀](@entry_id:139216)或收缩。因此，热[应变张量](@entry_id:193332)是一个球张量。其大小由该点的**线性热膨胀系数** $\alpha(\boldsymbol{x})$ 决定 [@problem_id:2660890]。

$$
\varepsilon^{\theta}_{ij}(\boldsymbol{x}) = \alpha(\boldsymbol{x}) \Delta T \delta_{ij}
$$

其中 $\delta_{ij}$ 是克罗内克符号。重要的是，[热应变](@entry_id:187744)由**局部**的热膨胀系数 $\alpha(\boldsymbol{x})$ 决定。这正是 FGM 的核心思想：本构行为是点态的。使用材料属性的空间平均值来计算[热应变](@entry_id:187744)是错误的，因为它忽略了材料的非[均匀性](@entry_id:152612)。

这个看似简单的公式具有深远的意义。即使一个 FGM 构件经受均匀的温度变化 $\Delta T$，如果其[热膨胀系数](@entry_id:150685) $\alpha(\boldsymbol{x})$ 或弹性模量 $C_{ijkl}(\boldsymbol{x})$ 随空间变化，并且构件受到约束（无论是外部约束还是内部自约束），那么即使没有外力作用，其内部也会产生应[力场](@entry_id:147325)，这被称为**热应力**。FGM 的设计目标之一就是通过合理设计属性梯度 $\alpha(\boldsymbol{x})$ 和 $E(\boldsymbol{x})$，来使这些[热应力](@entry_id:180613)最小化。

### 在结构元件中的应用：梁与板

将 FGM 的基本力学原理应用于梁和板等工程结构，可以揭示非均匀性如何影响结构的宏观响应，如刚度、变形和应力[分布](@entry_id:182848)。

#### FGM 梁的弯曲

考虑一个由 FGM 制成的梁，其杨氏模量 $E(z)$ 沿厚度方向 $z$ 变化。一个经典的问题是确定在[纯弯曲](@entry_id:202969)下的**中性轴**位置 $z_n$。根据 Euler-Bernoulli [梁理论](@entry_id:176426)，[轴向应变](@entry_id:160811) $\epsilon_x$ 沿厚度线性[分布](@entry_id:182848)：$\epsilon_x(z) = \kappa (z - z_n)$，其中 $\kappa$ 是曲率。轴向应力为 $\sigma_x(z) = E(z) \epsilon_x(z)$。

对于[纯弯曲](@entry_id:202969)，[截面](@entry_id:154995)上的轴向合力必须为零：

$$
N = \int_A \sigma_x(z) \, dA = \int_A E(z) \kappa (z - z_n) \, dA = 0
$$

由于 $\kappa \neq 0$，这要求中性轴 $z_n$ 必须满足：

$$
\int_A E(z) (z - z_n) \, dA = 0 \quad \implies \quad z_n = \frac{\int_A z E(z) \, dA}{\int_A E(z) \, dA}
$$

这个结果表明，FGM 梁的中性轴是[截面](@entry_id:154995)**模量加权面积的形心**，而不再是均匀材料梁的几何形心。中性轴会向着材料更硬的区域移动 [@problem_id:2660879]。例如，对于一个厚度为 $H$、模量按 $E(z) = E_0 \exp(\beta z/H)$ [分布的矩](@entry_id:156454)形[截面](@entry_id:154995)梁，其中 $z \in [0, H]$，可以精确求解得到 $z_n$ 的位置。若 $\beta > 0$，则顶部更硬，$z_n > H/2$；若 $\beta  0$，则底部更硬，$z_n  H/2$；只有当 $\beta=0$（均匀材料）时，$z_n = H/2$。

对于更高级的[梁理论](@entry_id:176426)，如 **Timoshenko [梁理论](@entry_id:176426)**，它同时考虑了弯曲变形和[剪切变形](@entry_id:170920)。对于 FGM 梁，其弯曲刚度 $B(x) = E(x)I$ 和剪切刚度 $S(x) = k_s G(x) A$ 会沿轴向 $x$ 变化。控制方程是一对耦合的[微分方程](@entry_id:264184)，描述横向位移 $w(x)$ 和[截面](@entry_id:154995)转角 $\varphi(x)$：

$$
\frac{d}{dx} \left[ S(x) (w'(x) - \varphi(x)) \right] + q(x) = 0
$$
$$
\frac{d}{dx} \left[ B(x) \varphi'(x) \right] - S(x) (w'(x) - \varphi(x)) = 0
$$

关键在于，由于 $B(x)$ 和 $S(x)$ 是 $x$ 的函数，微分算子必须作用于整个乘积项，这与均匀[梁理论](@entry_id:176426)有本质区别 [@problem_id:2660863]。

#### FGM 板的力学行为

当 FGM 用于板结构时，其非[均匀性](@entry_id:152612)会导致更复杂的耦合行为。在**[经典层合板理论](@entry_id:182456) (CLPT)** 框架下，板的[本构关系](@entry_id:186508)由一个 $6 \times 6$ 的 **ABD 矩阵**描述，它关联了中面应变 $\boldsymbol{\varepsilon}_0$ 和曲率 $\boldsymbol{\kappa}$ 与面内力合量 $\mathbf{N}$ 和弯矩合量 $\mathbf{M}$：

$$
\begin{pmatrix} \mathbf{N} \\ \mathbf{M} \end{pmatrix} = \begin{pmatrix} \mathbf{A}  \mathbf{B} \\ \mathbf{B}  \mathbf{D} \end{pmatrix} \begin{pmatrix} \boldsymbol{\varepsilon}_0 \\ \boldsymbol{\kappa} \end{pmatrix}
$$

其中，**[拉伸刚度](@entry_id:193973)矩阵 A**、**耦合刚度矩阵 B** 和 **[弯曲刚度](@entry_id:180453)矩阵 D** 分别通过对厚度积分得到：

$$
(\mathbf{A}, \mathbf{B}, \mathbf{D}) = \int_{-h/2}^{h/2} \mathbf{Q}(z) (1, z, z^2) \, dz
$$

这里 $\mathbf{Q}(z)$ 是随厚度 $z$ 变化的[平面应力](@entry_id:172193)折减[刚度矩阵](@entry_id:178659)。

对于 FGM 板，由于材料属性通常不对中面 ($z=0$) 对称，导致**耦合刚度矩阵 B** 通常不为零 [@problem_id:2660908]。一个非零的 $\mathbf{B}$ 矩阵意味着**[拉伸-弯曲耦合](@entry_id:755518)**：
*   施加纯面[内载荷](@entry_id:195654)（$\boldsymbol{\varepsilon}_0 \neq \mathbf{0}, \boldsymbol{\kappa}=\mathbf{0}$）会产生[弯矩](@entry_id:202968)（$\mathbf{M} = \mathbf{B} \boldsymbol{\varepsilon}_0$），导致板发生翘曲。
*   施加[纯弯曲](@entry_id:202969)（$\boldsymbol{\kappa} \neq \mathbf{0}, \boldsymbol{\varepsilon}_0=\mathbf{0}$）会产生面[内力](@entry_id:167605)（$\mathbf{N} = \mathbf{B} \boldsymbol{\kappa}$），导致板在弯曲时发生拉伸或收缩。

这种耦合效应在[对称层合板](@entry_id:187524)或均匀板中是不存在的（因为积分项 $z \mathbf{Q}(z)$ 是奇函数，在对称区间上的积分为零）。

对于更通用的**Mindlin-Reissner 板理论**，它考虑了[横向剪切变形](@entry_id:176673)。其控制[方程组](@entry_id:193238)更为复杂，包含五个[平衡方程](@entry_id:172166)，分别对应面[内力](@entry_id:167605)、横向剪切力和[弯矩](@entry_id:202968)的平衡。对于沿板面 $(x,y)$ 变化的 FGM 板，其刚度矩阵 $\mathbf{A}, \mathbf{B}, \mathbf{D}$ 以及横向剪切刚度矩阵 $\mathbf{S}$ 都将是 $(x,y)$ 的函数。其平衡方程在用应力合量表示时，形式是普适的 [@problem_id:2660827]：

$$
\begin{aligned}
 N_{ij,j} + b_i = 0 \\
 M_{ij,j} - Q_i + m_i = 0 \\
 Q_{i,i} + p = 0
\end{aligned}
$$

其中 $Q_i$ 是横向剪力。当这些方程用位移场表示时，[刚度矩阵](@entry_id:178659)的空间梯度将显式出现，使得控制[偏微分方程组](@entry_id:172573)的系数成为变量。

### 数学考量：界面与解的正则性

最后，我们从[数学分析](@entry_id:139664)的角度探讨一个深刻的问题：[功能梯度材料](@entry_id:157846)属性的连续性如何影响其弹性力学问题的解（即位移场）的[光滑性](@entry_id:634843)或**正则性**？

考虑弹性力学平衡方程组 $-\partial_j ( C_{ijkl}(x) \varepsilon_{kl}(u) ) = f_i(x)$。这是一个二阶椭圆型[偏微分方程组](@entry_id:172573)。解 $\boldsymbol{u}$ 的正则性（即其可微性质）强烈地依赖于系数 $C_{ijkl}(x)$、[体力](@entry_id:174230)项 $f_i(x)$ 以及求解域 $\Omega$ 边界的[光滑性](@entry_id:634843)。

我们对比两种情况 [@problem_id:2660896]：

*   **情形 I：连续变化的 FGM**
    如果[弹性张量](@entry_id:170728) $C_{ijkl}(x)$ 在整个区域 $\overline{\Omega}$ 上是连续的（例如，Hölder 连续 $C^{0,\alpha}$），并且载荷和边界也足够光滑，那么椭圆型 PDE [正则性理论](@entry_id:194071)保证解 $\boldsymbol{u}$ 也是更光滑的。具体来说，位移场 $\boldsymbol{u}$ 至少是 $C^{1,\alpha}$ 连续的。这意味着位移的梯度，也就是应变场 $\boldsymbol{\varepsilon}$，在整个区域内是连续的。

*   **情形 II：含界面的 FGM (或层状[复合材料](@entry_id:139856))**
    在许多实际情况中，FGM 可能由具有不同属性的多个层组成，或者在数值模型中被近似为分片连续的材料。在这种情况下，$C_{ijkl}(x)$ 在子区域 $\Omega_m$ 内部是光滑的，但在子区域之间的界面 $\Gamma$ 上存在**跳跃不连续**。
    在这种情况下，物理上合理的[界面条件](@entry_id:750725)是：
    1.  **位移连续性**：$[\boldsymbol{u}]_\Gamma = \boldsymbol{u}^+ - \boldsymbol{u}^- = \mathbf{0}$。这保证了材料的完整性。
    2.  **[牵引力连续性](@entry_id:756091)**：$[\boldsymbol{\sigma} \cdot \boldsymbol{n}]_\Gamma = \mathbf{0}$。这源于牛顿第三定律。
    
    [牵引力连续性](@entry_id:756091)条件可以写作：$(C_{ijkl} \varepsilon_{kl})^+ n_j = (C_{ijkl} \varepsilon_{kl})^- n_j$。由于[弹性张量](@entry_id:170728)在界面上存在跳跃，即 $[C_{ijkl}]_\Gamma \neq 0$，为了使该等式对于任意变形都成立，应变张量 $\varepsilon_{kl}$ 必然在界面上发生**跳跃**，即 $[\varepsilon_{kl}]_\Gamma \neq 0$。
    
    应变的跳跃意味着位移的梯度 $\nabla \boldsymbol{u}$ 在界面上是不连续的。因此，[全局解](@entry_id:180992) $\boldsymbol{u}$ 不再是 $C^1$ 连续的。它只是一个在全局上属于 Sobolev 空间 $H^1(\Omega)$（保证了位移的平方[可积性](@entry_id:142415)和一阶导数的平方可积性，从而位移是连续的），但在每个子区域内部更加光滑（例如 $C^{1,\alpha}(\overline{\Omega_m})$）的函数。
    
这个结论揭示了一个深刻的物理-数学联系：材料属性的**不连续性**直接导致了应变场的**不连续性**，即使[位移场](@entry_id:141476)本身保持连续。这是理解层状[复合材料](@entry_id:139856)和具有尖锐梯度变化的 FGM 中应力集中和界面[失效机制](@entry_id:184047)的关键。