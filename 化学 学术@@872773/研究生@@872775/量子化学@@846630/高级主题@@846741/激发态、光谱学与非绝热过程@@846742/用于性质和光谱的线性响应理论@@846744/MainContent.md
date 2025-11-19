## 引言
[线性响应理论](@entry_id:145737)是现代物理和化学中一个极其强大和普适的理论框架，它为我们理解和预测物质如何对外界微弱的刺激（如[电磁场](@entry_id:265881)）做出反应提供了数学语言。从分子的颜色到材料的[导电性](@entry_id:137481)，许多基本性质的根源都可以通过[线性响应](@entry_id:146180)的视角来揭示。然而，将这一抽象理论应用于真实的[量子多体系统](@entry_id:141221)，并从中提取出可与实验相比较的精确数据，是理论化学领域面临的核心挑战之一。本文旨在系统性地填补这一知识鸿沟，为读者提供一个从基本原理到前沿计算实践的完整指南。

本文将分为三个核心部分。在第一章“原理与机制”中，我们将从第一性原理出发，构建[线性响应理论](@entry_id:145737)的数学形式体系，推导关键的[久保公式](@entry_id:144041)，并阐明其与涨落-耗散定理等基本物理原理的深刻联系。我们还将深入探讨含时Hartree-Fock和[密度泛函理论](@entry_id:139027)（TDHF/TDDFT）等实用计算方法背后的[代数结构](@entry_id:137052)。随后，在第二章“应用与跨学科关联”中，我们将展示该理论在计算分子[光谱](@entry_id:185632)、手性、[溶剂效应](@entry_id:147658)乃至凝聚态物理中的广泛应用，并揭示其与信号处理等其他学科的内在关联。最后，在“动手实践”部分，我们将通过一系列精选的计算问题，引导读者亲手应用这些理论，解决从推导基本求和规则到分析TDHF方法局限性的具体挑战。通过本次学习，读者将能够全面掌握[线性响应理论](@entry_id:145737)，并有能力将其应用于解决实际的化学与物理问题。

## 原理与机制

本章旨在深入阐述[线性响应理论](@entry_id:145737)的核心原理与机制。我们将从第一性原理出发，构建该理论的数学框架，并探讨其在计算分子性质和[光谱](@entry_id:185632)中的广泛应用。本章内容假定读者已具备量子力学和[统计力](@entry_id:194984)学的基本知识。

### [线性响应理论](@entry_id:145737)的形式体系

[线性响应理论](@entry_id:145737)为研究量子体系在微弱外界微扰下如何响应提供了一个普适而强大的形式体系。其核心思想是，对于一个足够弱的微扰，体系的响应与微扰强度成[线性关系](@entry_id:267880)。

考虑一个由不[含时哈密顿量](@entry_id:136684) $H_0$ 描述的量子体系。在 $t \to -\infty$ 的遥远过去，体系处于由[密度算符](@entry_id:138151) $\rho_0$ 描述的初始状态。在 $t_0$ 之后，我们施加一个微弱的[含时微扰](@entry_id:171975) $V(t)$。一个常见的微扰形式是 $V(t) = -F(t)B$，其中 $F(t)$ 是一个标量“[广义力](@entry_id:169699)”，$B$ 是一个不含时的[厄米算符](@entry_id:153410)。我们的目标是计算另一个可观测量 $A$ 的[期望值](@entry_id:153208)变化 $\delta\langle A(t) \rangle$。

为了简化推导，我们采用[相互作用绘景](@entry_id:198213)。该绘景下的算符由 $O_I(t) = \exp(\frac{i}{\hbar}H_0 t) O \exp(-\frac{i}{\hbar}H_0 t)$ 定义。[密度算符](@entry_id:138151) $\rho_I(t)$ 的[演化方程](@entry_id:268137)（刘维尔-冯诺依曼方程）变为：
$$
i\hbar \frac{d\rho_I(t)}{dt} = [V_I(t), \rho_I(t)]
$$
其中 $V_I(t) = -F(t)B_I(t)$。对该方程进行积分，并进行一级近似（即用零级[密度算符](@entry_id:138151) $\rho_0$ 替换积分内的 $\rho_I(t')$），我们得到对[密度算符](@entry_id:138151)的[一阶修正](@entry_id:155896)：
$$
\rho_I^{(1)}(t) = -\frac{i}{\hbar} \int_{-\infty}^{t} dt' [V_I(t'), \rho_0] = -\frac{i}{\hbar} \int_{-\infty}^{t} dt' [-F(t')B_I(t'), \rho_0] = \frac{i}{\hbar} \int_{-\infty}^{t} dt' F(t') [B_I(t'), \rho_0]
$$
[可观测量](@entry_id:267133) $A$ [期望值](@entry_id:153208)的变化 $\delta\langle A(t) \rangle$ 线性于微扰，由下式给出：
$$
\delta\langle A(t) \rangle = \mathrm{Tr}\{\rho_I^{(1)}(t) A_I(t)\} = \frac{i}{\hbar} \int_{-\infty}^{t} dt' F(t') \mathrm{Tr}\{[B_I(t'), \rho_0] A_I(t)\}
$$
利用迹的轮换对称性 $\mathrm{Tr}(XYZ) = \mathrm{Tr}(ZXY)$，我们可以简化迹的计算：
$$
\mathrm{Tr}\{[B_I(t'), \rho_0] A_I(t)\} = \mathrm{Tr}\{\rho_0 [A_I(t), B_I(t')]\} = \langle [A_I(t), B_I(t')] \rangle_0
$$
其中 $\langle \dots \rangle_0$ 表示在未微扰态 $\rho_0$ 下的[期望值](@entry_id:153208)。然而，在标准定义中，微扰通常写为 $H'(t)=-AF(t)$，响应函数 $\chi$ 的符号约定可能不同。为了与广泛接受的惯例保持一致，即对于 $V(t) = -F(t)B$ 的微扰，响应为 $\delta\langle A(t) \rangle = \int dt' \chi_{AB}(t-t')F(t')$，我们最终得到的表达式包含一个负号 [@problem_id:2902134]。

为了得到一个简单的卷积形式，我们需要做出一个关键假设：初始态 $\rho_0$ 是[稳态](@entry_id:182458)，即它与未微扰[哈密顿量](@entry_id:172864)对易，$[H_0, \rho_0] = 0$。例如，$\rho_0$ 可以是 $H_0$ 的一个本征态，或者是一个正则系综的[密度算符](@entry_id:138151) $\rho_0 \propto \exp(-\beta H_0)$。在此条件下，二时关联函数具有[时间平移不变性](@entry_id:270209)，即 $\langle [A_I(t), B_I(t')] \rangle_0$ 仅依赖于时间差 $t-t'$。因此，响应可以写成一个[卷积积分](@entry_id:155865)：
$$
\delta\langle A(t) \rangle = \int_{-\infty}^{\infty} dt' \chi_{AB}(t-t') F(t')
$$
这里的积分核 $\chi_{AB}(\tau)$ 被称为**推迟磁化率 (retarded susceptibility)** 或**[线性响应函数](@entry_id:160418)**。其定义为 [@problem_id:2902134]：
$$
\chi_{AB}(\tau) = -\frac{i}{\hbar} \theta(\tau) \langle [A_I(\tau), B_I(0)] \rangle_0
$$
其中 $\tau=t-t'$，$\theta(\tau)$ 是亥维赛德[阶跃函数](@entry_id:159192)，它保证了**因果性 (causality)**：体系在时刻 $t$ 的响应只能由过去时刻 $t' \le t$ 的微扰引起。这个公式是[线性响应理论](@entry_id:145737)的基石，它将宏观的[响应函数](@entry_id:142629) $\chi_{AB}$ 与微观的[量子力学对易子](@entry_id:149438)[期望值](@entry_id:153208)联系起来。

### [频域](@entry_id:160070)性质与格林函数

在处理[光谱学](@entry_id:141940)问题时，将[响应理论](@entry_id:188225)转换到[频域](@entry_id:160070)通常更为方便。通过[傅里叶变换](@entry_id:142120)，时间域的卷积运算变成了[频域](@entry_id:160070)中的简单乘积：
$$
\delta\langle A(\omega) \rangle = \chi_{AB}(\omega) F(\omega)
$$
其中 $\delta\langle A(\omega) \rangle$ 和 $F(\omega)$ 分别是 $\delta\langle A(t) \rangle$ 和 $F(t)$ 的[傅里叶变换](@entry_id:142120)。$\chi_{AB}(\omega)$ 被称为**广义[磁化率](@entry_id:138219) (generalized susceptibility)**，它是推迟[响应函数](@entry_id:142629) $\chi_{AB}(t)$ 的[傅里叶变换](@entry_id:142120) [@problem_id:2902137]。

广义[磁化率](@entry_id:138219)与其他几个重要的物理量密切相关。

**[推迟格林函数](@entry_id:139183) (Retarded Green's Function)**: 在[多体物理学](@entry_id:144526)中，[推迟格林函数](@entry_id:139183)通常被定义为：
$$
G^R_{AB}(t) = -i \theta(t) \langle [A_I(t), B_I(0)] \rangle_0
$$
通过比较这个定义和 $\chi_{AB}(t)$ 的表达式，我们可以立即得到它们之间的关系：
$$
\chi_{AB}(\omega) = \frac{1}{\hbar} G^R_{AB}(\omega)
$$
需要注意的是，[格林函数](@entry_id:147802)的定义并非完全统一，有时其定义中会包含因子 $1/\hbar$。因此，在不同文献中，$\chi_{AB}(\omega)$ 和 $G^R_{AB}(\omega)$ 之间的关系可能只是一个简单的等号。关键在于，推迟磁化率和[推迟格林函数](@entry_id:139183)都描述了体系的因果响应，其核心都是由算符的对易子决定的 [@problem_id:2902137]。

**静态[磁化率](@entry_id:138219) (Static Susceptibility)**: 当外场不随时间变化时（即 $\omega=0$），体系的响应由**静态磁化率** $\chi_{AB}^{\mathrm{stat}}$ 描述。它被定义为平衡态下可观测量 $A$ 的[期望值](@entry_id:153208)对静态场强 $f$ 的一阶导数：
$$
\chi_{AB}^{\mathrm{stat}} = \left. \frac{\partial \langle A \rangle_f}{\partial f} \right|_{f=0}
$$
这一定义源于[平衡态](@entry_id:168134)[统计力](@entry_id:194984)学。一个自然的问题是，[动态磁化率](@entry_id:139739)在零频极限下是否等于静态[磁化率](@entry_id:138219)？即 $\lim_{\omega\to 0} \chi_{AB}(\omega) = \chi_{AB}^{\mathrm{stat}}$ 是否成立？答案是，对于大多数体系（满足[遍历性假设](@entry_id:147104)的体系），这个等式是成立的。然而，如果体系中存在与算符 $B$ 不正交的守恒量（除了能量），这个关系可能会被破坏。这种情况会导致[响应函数](@entry_id:142629)在 $\omega=0$ 处出现奇异性（例如，在[电导](@entry_id:177131)中的德鲁德峰），此时需要更仔细地处理极限 [@problem_id:2902137]。

### 涨落-耗散定理

[线性响应理论](@entry_id:145737)最深刻的结果之一是**涨落-耗散定理 (Fluctuation-Dissipation Theorem, FDT)**。该定理揭示了体系对外界微扰的响应（耗散）与其自身在平衡态下的自发涨落之间的内在联系。

体系的涨落可以通过**对称化关联函数**来表征：
$$
S_{AB}(t) = \frac{1}{2} \langle \{ \Delta A(t), \Delta B(0) \} \rangle_\beta = \frac{1}{2} \langle \Delta A(t)\Delta B(0) + \Delta B(0)\Delta A(t) \rangle_\beta
$$
其中 $\Delta A(t) = A(t) - \langle A \rangle$ 是涨落算符，$\langle\dots\rangle_\beta$ 表示在[逆温](@entry_id:140086)度为 $\beta=1/(k_B T)$ 的[正则系综](@entry_id:142391)下的平均。$S_{AB}(t)$ 的[傅里叶变换](@entry_id:142120) $S_{AB}(\omega)$ 描述了平衡态下涨落的[能谱](@entry_id:181780)。

涨落-耗散定理将 $S_{AB}(\omega)$ 与响应函数 $\chi_{AB}(\omega)$ 的虚部（耗散部分）联系起来。利用平衡态关联函数的久保-马丁-施温格 (Kubo-Martin-Schwinger, KMS) 条件，可以推导出它们之间的精确关系 [@problem_id:2902147]：
$$
S_{AB}(\omega) = \hbar \coth\left(\frac{\beta\hbar\omega}{2}\right) \mathrm{Im}\,\chi_{AB}(\omega)
$$
这个公式非常深刻。它表明，我们只需测量一个体系在[平衡态](@entry_id:168134)下的自发涨落（例如，通过[非弹性中子散射](@entry_id:140691)），就可以预测该体系在外场作用下的能量耗散谱（例如，通过[红外吸收](@entry_id:188893)[光谱](@entry_id:185632)）。

关系式中的 $\coth(\frac{\beta\hbar\omega}{2})$ 因子至关重要，它体现了[量子统计](@entry_id:143815)的效应。我们可以将其重写为 $1 + 2n_B(\omega)$，其中 $n_B(\omega) = [\exp(\beta\hbar\omega)-1]^{-1}$ 是[玻色-爱因斯坦分布](@entry_id:145257)函数。
*   常数 ‘1’ 代表即使在绝对零度下也存在的**量子涨落**（[零点能](@entry_id:142176)）。
*   $2n_B(\omega)$ 项代表由[热激发](@entry_id:275697)引起的**热涨落**。

在经典高温极限下 ($\hbar\omega \ll k_B T$)，$\coth(\frac{\beta\hbar\omega}{2}) \approx \frac{2}{\beta\hbar\omega} = \frac{2k_B T}{\hbar\omega}$。此时，FDT 简化为经典形式：
$$
S_{AB}(\omega) \approx \frac{2k_B T}{\omega} \mathrm{Im}\,\chi_{AB}(\omega)
$$
这表明在经典体系中，涨落的强度与热能 $k_B T$ 成正比。

### [光谱学](@entry_id:141940)的态-和表达式与温度效应

为了将抽象的理论应用于具体的[光谱](@entry_id:185632)问题，例如分子对光的吸收，我们可以在[能量本征态](@entry_id:152154)的表象下展开[响应函数](@entry_id:142629)。

考虑一个分子与频率为 $\omega$ 的[电场](@entry_id:194326)相互作用，微扰[哈密顿量](@entry_id:172864)为 $V(t) = -\boldsymbol{\mu}\cdot\mathbf{E}(t)$。我们感兴趣的响应是[诱导偶极矩](@entry_id:262417) $\langle \mu_i \rangle$，它与外[电场](@entry_id:194326)通过**动态偶极极化张量** $\alpha_{ij}(\omega)$ 联系起来。通过将[线性响应函数](@entry_id:160418) $\chi_{\mu_i \mu_j}(\omega)$ 在 $H_0$ 的本征态 $\{|n\rangle\}$ 基上展开，可以得到 $\alpha_{ij}(\omega)$ 的**态-和 (sum-over-states)** 表达式，也称为克拉默斯-海森堡 (Kramers-Heisenberg) 公式 [@problem_id:2902165]：
$$
\alpha_{ij}(\omega) = \sum_{n \neq 0} \left( \frac{\langle 0|\mu_i|n \rangle \langle n|\mu_j|0 \rangle}{\omega_{n0} - \omega - i0^+} + \frac{\langle 0|\mu_j|n \rangle \langle n|\mu_i|0 \rangle}{\omega_{n0} + \omega + i0^+} \right)
$$
这里，我们假设体系初始处于[基态](@entry_id:150928) $|0\rangle$，$\omega_{n0} = (E_n - E_0)/\hbar$ 是从[基态](@entry_id:150928)到[激发态](@entry_id:261453) $|n\rangle$ 的跃迁频率。表达式中的两项分别对应于**共振项**和**非共振项**。当入射光频率 $\omega$ 接近某个跃迁频率 $\omega_{n0}$ 时，第一项的分母趋于零，导致共振吸收。分母中的无穷小量 $i0^+$ 确保了因果性，并给出了描述吸收的虚部。

[光谱](@entry_id:185632)的强度通常用无量纲的**振子强度 (oscillator strength)** $f_{0n}$ 来描述，它与跃迁偶极矩的平方成正比。在[原子单位](@entry_id:166762)制中，其定义为 [@problem_id:2902165]：
$$
f_{0n} = \frac{2}{3} \omega_{n0} \sum_{i=x,y,z} |\langle 0|r_i|n \rangle|^2
$$

当温度不为零时，体系不再单纯处于[基态](@entry_id:150928)，而是以[玻尔兹曼分布](@entry_id:142765) $\rho_n \propto \exp(-\beta E_n)$ 占据一系列的能级。这会对[吸收光谱](@entry_id:144611)产生显著影响。净[吸收功率](@entry_id:265908)正比于[响应函数](@entry_id:142629) $\chi''(\omega)$ 的虚部，其在有限温度下的态-和表达式为 [@problem_id:2902127]：
$$
\chi''(\omega) \propto \sum_{n,m} (\rho_n - \rho_m) |\mu_{mn}|^2 \delta(\omega - \omega_{mn})
$$
这个表达式清楚地表明，在频率 $\omega_{mn}$ 处的净吸收（或发射）由两个过程决定：
1.  **受激吸收 (Stimulated Absorption)**: 体系从低能级 $|n\rangle$ 吸收一个[光子](@entry_id:145192)跃迁到高能级 $|m\rangle$，其速率正比于初态的布居数 $\rho_n$。
2.  **受激发射 (Stimulated Emission)**: 体系在高能级 $|m\rangle$ 上受光场刺激，发射一个同频同相的[光子](@entry_id:145192)回到低能级 $|n\rangle$，其速率正比于初态的布居数 $\rho_m$。

净吸收是这两个过程速率之差，因此正比于布居数之差 $\rho_n - \rho_m$。由于 $\rho_m = \rho_n \exp(-\beta(E_m-E_n)) = \rho_n \exp(-\beta\hbar\omega_{mn})$，布居数之差可以写作 $\rho_n(1-\exp(-\beta\hbar\omega_{mn}))$。这个 $[1 - \exp(-\beta\hbar\omega)]$ 因子是有限温度下吸收光谱的标志，它恰当地解释了为何在净吸收谱中会出现[受激发射](@entry_id:150501)的“负”贡献，并且这个效应随着温度升高而愈发重要 [@problem_id:2902127] [@problem_id:2902147]。

### [量子化学](@entry_id:140193)中的实用计算方法

对于真实的分子体系，我们无法获得精确的[多电子波函数](@entry_id:156344)本征态。因此，上述的态-和表达式在实践中难以直接使用。取而代之的是，我们采用近似的[基态](@entry_id:150928)理论（如 Hartree-Fock 或[密度泛函理论](@entry_id:139027)）并在此基础上发展[线性响应方法](@entry_id:751324)。

#### TDHF/TDDFT 框架与 RPA 方程

**[含时 Hartree-Fock (TDHF)](@entry_id:198498)** 和 **[含时密度泛函理论](@entry_id:200019) (TDDFT)** 是计算电子激发谱最常用的两种方法。它们都可被表述为一个具有相同[代数结构](@entry_id:137052)的非厄米本征方程，通常称为**随机相近似 (Random Phase Approximation, RPA)** 方程。

在单激发和单退激发的粒子-空穴对[基矢](@entry_id:199546)下，RPA 方程可以写成如下的[块矩阵](@entry_id:148435)形式：
$$
\begin{pmatrix} \mathbf{A}  \mathbf{B} \\ \mathbf{B}^*  \mathbf{A}^* \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix} = \omega \begin{pmatrix} \mathbf{1}  \mathbf{0} \\ \mathbf{0}  -\mathbf{1} \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix}
$$
其中，$\omega$ 是激发能。$\mathbf{X}$ 和 $\mathbf{Y}$ 分别是激发和退激发振幅向量。矩阵 $\mathbf{A}$ 和 $\mathbf{B}$ 由[基态](@entry_id:150928)[轨道](@entry_id:137151)能和[双电子积分](@entry_id:261879)（或在 TDDFT 中为[交换相关核](@entry_id:195258)）构成。
*   **A 矩阵** 描述了不同[粒子-空穴激发](@entry_id:137289)之间的耦合。
*   **B 矩阵** 描述了[粒子-空穴激发](@entry_id:137289)与退激发的耦合。从物理上看，$\mathbf{B}$ 矩阵的出现是由于[基态](@entry_id:150928)本身也对外场做出了响应（[基态关联](@entry_id:186115)效应），而不仅仅是简单的激发 [@problem_id:2902136]。

#### Tamm-Dancoff 近似 (TDA)

RPA 方程是一个非厄米的广义本征值问题，求解起来较为复杂。**Tamm-Dancoff 近似 (Tamm-Dancoff Approximation, TDA)** 通过完全忽略 $\mathbf{B}$ 矩阵来简化问题，即令 $\mathbf{B}=\mathbf{0}$。这使得 RPA 方程解耦，退化为一个标准的厄米本征值问题：
$$
\mathbf{A}\mathbf{X} = \omega_{\mathrm{TDA}} \mathbf{X}
$$
在 [Hartree-Fock](@entry_id:142303) 理论的框架下，TDA 等价于[单激发组态相互作用](@entry_id:174866) (CIS) 方法。虽然 TDA 在计算上更简单且数值性质更稳定，但它是一种近似。与完整的 RPA 相比，TDA 的主要后果包括 [@problem_id:2902136]：
1.  **[激发能](@entry_id:190368)**: TDA 计算出的低洼价层[激发能](@entry_id:190368)通常系统性地高于 RPA 的结果。
2.  **振子强度**: TDA 通常会低估强跃迁的[振子强度](@entry_id:147221)。
3.  **守恒律**: TDA 不再严格满足 Thomas-Reiche-Kuhn (TRK) [振子强度求和规则](@entry_id:183363)。

#### Casida 方程

在 TDDFT 的实践中，虽然底层的 RPA 形式方程是非厄米的，但 M. E. Casida 推导出了一个等价的、但形式上是厄米的[本征值问题](@entry_id:142153)，极大地简化了计算。这个被称为 **Casida 方程** 的形式如下 [@problem_id:2902126]：
$$
\mathbf{\Omega}(\omega) \mathbf{F} = \omega^2 \mathbf{F}
$$
其中，$\omega$ 是激发能，$\mathbf{\Omega}$ 是一个[厄米矩阵](@entry_id:155147)，其矩阵元为：
$$
\Omega_{ia,jb}(\omega) = \delta_{ij}\delta_{ab}(\varepsilon_a - \varepsilon_i)^2 + 2\sqrt{(\varepsilon_a - \varepsilon_i)(\varepsilon_b - \varepsilon_j)} K_{ia,jb}(\omega)
$$
这里，$\varepsilon$ 是 Kohn-Sham [轨道](@entry_id:137151)能，$i,j$ 指占据[轨道](@entry_id:137151)，$a,b$ 指非占[轨道](@entry_id:137151)。$K_{ia,jb}$ 是[耦合矩阵](@entry_id:191757)元，它包含库仑相互作用和[交换相关核](@entry_id:195258) $f_{\mathrm{Hxc}}$ 的贡献。Casida 方程的[本征值](@entry_id:154894)是[激发能](@entry_id:190368)的平方 $\omega^2$，这直接避免了求解非厄米问题。

#### [响应理论](@entry_id:188225)与[基态](@entry_id:150928)不稳定性

[线性响应理论](@entry_id:145737)还提供了一个强大的工具来诊断[基态](@entry_id:150928)计算的稳定性。HF 或 KS [基态](@entry_id:150928)解只是能量对[轨道](@entry_id:137151)转动的一阶变分为零的点，但不保证是能量的局域最小值。能量的二阶变分（Hessian 矩阵）的[本征值](@entry_id:154894)决定了其稳定性。

TDHF/RPA 的数学结构与 HF 稳定性分析的 Hessian 矩阵密切相关。可以证明，当 HF/KS [基态](@entry_id:150928)[参考态](@entry_id:151465)存在不稳定性时（即 Hessian 矩阵存在负[本征值](@entry_id:154894)），相应的 TDHF/RPA 计算会产生虚数[激发能](@entry_id:190368)（即 $\omega^2  0$）。一个纯虚数的[激发能](@entry_id:190368) $\omega=i\gamma$ ($\gamma > 0$) 标志着[参考态](@entry_id:151465)在该对称性通道上是一个[鞍点](@entry_id:142576)，而非真正的最小值。因此，通过检查 TDHF/TDDFT 计算是否给出实数激发能，可以有效地判断所用[参考态](@entry_id:151465)的稳定性 [@problem_id:2902148]。

### 规范不变性及相关进阶问题

在计算与[电磁场](@entry_id:265881)相互作用相关的性质时，例如光学吸收谱，理论上结果不应依赖于所选的电磁规范。最常见的两种规范是**长度规范 (length gauge)** 和**速度规范 (velocity gauge)**，它们分别通过偶极算符 $\mathbf{r}$ 和速度（或动量）算符 $\mathbf{v}$ (或 $\mathbf{p}$) 来描述相互作用。

对于一个只含局域势 $V_{\mathrm{loc}}(\mathbf{r})$ 的[哈密顿量](@entry_id:172864)，速度算符就是 $\mathbf{v}=\mathbf{p}/m$。利用算符[对易关系](@entry_id:136780) $[H, \mathbf{r}] = -i\hbar \mathbf{p}/m$，可以证明对于[哈密顿量](@entry_id:172864)的[精确本征态](@entry_id:138620) $|n\rangle$ 和 $|m\rangle$，其位置和动量[矩阵元](@entry_id:186505)之间存在严格的正比关系 [@problem_id:2902142]：
$$
\langle n|\mathbf{p}|m\rangle = im\omega_{nm}\langle n|\mathbf{r}|m\rangle
$$
这个关系确保了如果使用一个完备的[基组](@entry_id:160309)，长度规范和速度规范计算出的[光谱](@entry_id:185632)是完全相同的。然而，在实际计算中，我们总是使用有限的、不完备的[基组](@entry_id:160309)，这会破坏规范不变性。因此，比较两种规范下的计算结果成为检验[基组](@entry_id:160309)完备性的一个常用手段。

当[哈密顿量](@entry_id:172864)包含**非局域势** $V_{\mathrm{nl}}$ 时（例如，在赝势计算中非常普遍），情况会变得更加复杂。此时，速度算符不再是 $\mathbf{p}/m$，而变为 [@problem_id:2902142]：
$$
\mathbf{v} = \frac{i}{\hbar}[H, \mathbf{r}] = \frac{\mathbf{p}}{m} + \frac{i}{\hbar}[V_{\mathrm{nl}}, \mathbf{r}]
$$
如果在速度规范计算中忽略了额外的非局域项 $[V_{\mathrm{nl}}, \mathbf{r}]$，就会导致与长度规范结果的严重偏差，并违反[振子强度求和规则](@entry_id:183363)等基本物理定律。

最后，对于**周期性体系**（晶体），位置算符 $\mathbf{r}$ 本身是无定义的。现代固体理论通过**[贝里联络](@entry_id:136662) (Berry connection)** 的概念解决了这个问题。在长度规范的表述中，跃迁偶极矩被一个涉及[布洛赫波函数](@entry_id:144223)对波矢 $\mathbf{k}$ 的导数的项 $i\langle u_{n\mathbf{k}}|\nabla_{\mathbf{k}}|u_{m\mathbf{k}}\rangle$ 所替代。这种形式化的处理方式重新建立了长度规范和速度规范之间的一致性，使得在周期性体系中进行规范不变的计算成为可能 [@problem_id:2902142]。