## 引言
材料的光学和光电子特性，如颜色、[发光效率](@entry_id:176455)和光电转换能力，从根本上由其电子激发态决定。当材料与光相互作用时，电子从[基态](@entry_id:150928)跃迁至[激发态](@entry_id:261453)，这一过程远比由电子密度决定的[基态](@entry_id:150928)性质复杂，是一个内在的多体问题。标准的[密度泛函理论](@entry_id:139027)（DFT）在描述[基态](@entry_id:150928)时非常成功，但其Kohn-Sham能级本身并不能准确描述激发过程，导致在预测[带隙](@entry_id:191975)和光学[光谱](@entry_id:185632)时常出现显著偏差。因此，发展并应用能够精确处理[电子激发](@entry_id:190531)和相互作用的理论方法，是理解和设计新型[功能材料](@entry_id:194894)的关键所在。

本篇文章旨在系统性地介绍计算[电子激发](@entry_id:190531)态和吸收光谱的先进理论与应用。读者将通过以下三个章节，逐步建立从量子力学第一性原理到宏观[可观测性](@entry_id:152062)质的完整知识框架：
*   在 **“原理与机制”** 一章中，我们将深入探讨两种主流方法：[含时密度泛函理论](@entry_id:200019)（TDDFT）和基于多体微扰论的[GW近似](@entry_id:140388)与[贝特-萨尔皮特方程](@entry_id:142429)（[GW-BSE](@entry_id:142900)）。我们将阐明[准粒子](@entry_id:136584)、[激子](@entry_id:147299)等核心概念，并解释如何从这些理论计算出振子强度和[光谱](@entry_id:185632)形状等可观测量。
*   在 **“应用与[交叉](@entry_id:147634)学科联系”** 一章中，我们将展示这些理论如何在物理、化学、[材料科学](@entry_id:152226)等多个领域中解决实际问题，例如表征材料基本性质、研究外场调控效应、理解复杂的[多体相互作用](@entry_id:751663)，并最终应用于光电器件的模[拟设](@entry_id:184384)计。
*   最后，在 **“动手实践”** 部分，我们提供了一系列精心设计的计算练习，引导读者亲身体验和解决[激发态计算](@entry_id:749156)中的关键技术问题，如收敛性测试和[有限尺寸效应](@entry_id:155681)的处理。

通过学习本章内容，您将掌握[激发态计算](@entry_id:749156)的核心思想，并有能力将其应用于解决前沿的科学与工程挑战。现在，让我们从[激发态计算](@entry_id:749156)的基石——其背后的基本原理与机制开始。

## 原理与机制

在理解材料的光学和光电子特性时，[电子激发](@entry_id:190531)态的计算是核心。与[基态](@entry_id:150928)性质主要由电子密度决定不同，[激发态](@entry_id:261453)涉及电子从占据态到非占据态的跃迁，这一过程本质上是一个[多体问题](@entry_id:138087)。本章将深入探讨计算[激发态](@entry_id:261453)和吸收光谱的主要理论框架和机制，从多体微扰论的基础出发，系统介绍[含时密度泛函理论](@entry_id:200019)（TDDFT）和[贝特-萨尔皮特方程](@entry_id:142429)（BSE）这两种主流方法，并阐明如何将计算结果与实验可观测的[光谱](@entry_id:185632)联系起来。

### [准粒子](@entry_id:136584)与[GW近似](@entry_id:140388)

在密度泛函理论（DFT）的Kohn-Sham (KS)框架中，KS轨道能量（[本征值](@entry_id:154894)）常被用作[电子能带结构](@entry_id:136694)的零阶近似。然而，必须强调的是，KS[本征值](@entry_id:154894)在物理上并不严格对应于加入或移出一个电子所需的能量。这些真实的单粒子[激发能](@entry_id:190368)被称为**[准粒子](@entry_id:136584) (quasiparticle)** 能量。一个[准粒子](@entry_id:136584)可以被看作是一个电子（或空穴）与其周围电子云（即所谓的“屏蔽云”）共同构成的复合体。这种“穿上”了相互作用外衣的电子，其能量和寿命都与裸露的KS电子不同。

为了精确计算[准粒子能量](@entry_id:173936)，我们需要借助**[多体微扰理论](@entry_id:168555) (Many-Body Perturbation Theory, MBPT)**。在MBPT框架中，[准粒子能量](@entry_id:173936) $E_{n}^{\mathrm{QP}}$ 是通过求解戴森（Dyson）方程得到的，其中引入了一个关键的、能量依赖的、非局域的算符——**[自能](@entry_id:145608) (self-energy)** $\Sigma(\omega)$。[自能](@entry_id:145608)描述了电子与系统中其他所有电子之间复杂的动态相互作用，它取代了KS理论中更简单的局域交换关联势 $v_{xc}$。

在实践中，最广泛使用的计算[自能](@entry_id:145608)的方法是**[GW近似](@entry_id:140388)**。其中，$G$ 代表[单粒子格林函数](@entry_id:140400)（Green's function），$W$ 代表[屏蔽库仑相互作用](@entry_id:164093)。[GW近似](@entry_id:140388)的核心思想是，[准粒子能量](@entry_id:173936) $E_{n}^{\mathrm{QP}}$ 满足以下[非线性方程](@entry_id:145852)：

$$
E_{n}^{\mathrm{QP}} = \varepsilon_{n}^{\mathrm{KS}} + \langle \phi_{n} | \mathrm{Re}\,\Sigma(E_{n}^{\mathrm{QP}}) - v_{xc} | \phi_{n} \rangle
$$

这里，$\varepsilon_{n}^{\mathrm{KS}}$ 和 $|\phi_{n}\rangle$ 分别是KS[本征值](@entry_id:154894)和[本征态](@entry_id:149904)。由于[自能](@entry_id:145608) $\Sigma$ 依赖于待求的[准粒子能量](@entry_id:173936) $E_{n}^{\mathrm{QP}}$，这个方程需要自洽求解。然而，一种常见的简化方法是围绕KS能量 $\varepsilon_{n}^{\mathrm{KS}}$ 对[自能](@entry_id:145608)进行一阶泰勒展开 [@problem_id:3451121]。定义[准粒子](@entry_id:136584)修正项 $\Delta\Sigma_{n}(\omega) \equiv \langle \phi_{n}|\mathrm{Re}\,\Sigma(\omega) - v_{xc}|\phi_{n}\rangle$，其在 $\varepsilon_{n}^{\mathrm{KS}}$ 附近的线性化形式为：

$$
\Delta\Sigma_{n}(E_{n}^{\mathrm{QP}}) \approx \Delta\Sigma_{n}(\varepsilon_{n}^{\mathrm{KS}}) + (E_{n}^{\mathrm{QP}} - \varepsilon_{n}^{\mathrm{KS}}) \left. \frac{\partial \Delta\Sigma_{n}(\omega)}{\partial \omega} \right|_{\omega=\varepsilon_{n}^{\mathrm{KS}}}
$$

将此式代入[准粒子](@entry_id:136584)方程并求解 $E_{n}^{\mathrm{QP}}$，我们得到：

$$
E_{n}^{\mathrm{QP}} = \varepsilon_{n}^{\mathrm{KS}} + Z_{n} \Delta\Sigma_{n}(\varepsilon_{n}^{\mathrm{KS}})
$$

其中，$Z_{n} = (1 - \Lambda_{n})^{-1}$ 被称为**[准粒子](@entry_id:136584)[重整化](@entry_id:143501)因子 (quasiparticle renormalization factor)**，而 $\Lambda_{n} = \left. \frac{\partial}{\partial \omega}\langle \phi_{n}|\mathrm{Re}\,\Sigma(\omega)|\phi_{n}\rangle\right|_{\omega=\varepsilon_{n}^{\mathrm{KS}}}$。这个公式清晰地表明，[GW近似](@entry_id:140388)通过一个在KS能量上计算的修正项 $\Delta\Sigma_{n}(\varepsilon_{n}^{\mathrm{KS}})$ 和一个重整化因子 $Z_n$ 来修正KS[本征值](@entry_id:154894)。对于[半导体](@entry_id:141536)和绝缘体，GW计算通常会显著地“打开”KS[带隙](@entry_id:191975)，即增大了[价带](@entry_id:158227)顶和导带底之间的能量差，从而得到与实验（如光电子能谱）更吻合的[准粒子](@entry_id:136584)[带隙](@entry_id:191975) [@problem_id:3451121]。这个[准粒子](@entry_id:136584)[带隙](@entry_id:191975)是计算光学吸收的正确起点。

### 中性激发：电子-空穴图像

与[准粒子](@entry_id:136584)（带电激发）不同，光学吸收过程通常涉及**中性激发 (neutral excitation)**，即一个电子从占据态跃迁到非占据态，同时在原来的位置留下一个**空穴 (hole)**。新产生的[电子和空穴](@entry_id:274534)通过[库仑相互作用](@entry_id:747947)相互吸引，可能形成一个束缚态，即**[激子](@entry_id:147299) (exciton)**。这种电子-空穴吸引能使得[光学跃迁](@entry_id:160047)的能量（光学[带隙](@entry_id:191975)）通常低于[准粒子](@entry_id:136584)[带隙](@entry_id:191975)。因此，简单地用[准粒子](@entry_id:136584)能级差来描述光学吸收是不够的，我们必须考虑电子-空穴相互作用。

### [含时密度泛函理论](@entry_id:200019) (TDDFT)

TDDFT是一种计算中性激发的高效方法，它将[多体问题](@entry_id:138087)转化为求解一个等效的非相互作用KS系统的含时演化。TDDFT主要有两种实现方式：[频域](@entry_id:160070)的[线性响应理论](@entry_id:145737)和时域的[实时传播](@entry_id:199067)方法。

#### 线性响应TDDFT与[Casida方程](@entry_id:183031)

在[线性响应](@entry_id:146180)（或称[频域](@entry_id:160070)）方法中，我们研究系统电子密度对一个微弱的、随时间[振荡](@entry_id:267781)的外部[电场](@entry_id:194326)（如光）的响应。系统的真实[激发能](@entry_id:190368)对应于密度响应[函数的极点](@entry_id:189069)。通过数学推导，可以证明这个问题等价于求解一个称为**[Casida方程](@entry_id:183031)**的非厄米[本征值问题](@entry_id:142153) [@problem_id:3451155]。

对于[单重态](@entry_id:154728)（spin-singlet）激发，[Casida方程](@entry_id:183031)的形式为一个 $2N_v N_c \times 2N_v N_c$ 的矩阵方程，其中 $N_v$ 是占据态数量，$N_c$ 是非占据态数量：

$$
\begin{pmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B}^* & \mathbf{A}^* \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix} = \Omega \begin{pmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & -\mathbf{1} \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix}
$$

其中，$\Omega$ 是激发能。矩阵 $\mathbf{A}$ 和 $\mathbf{B}$ 的元素由KS[轨道能量](@entry_id:158481)差和**[相互作用核](@entry_id:193790) (interaction kernel)** $K$ 决定。$\mathbf{A}$ 块描述了从占据态到非占据态的“共振”跃迁（粒子-空穴对的产生），而 $\mathbf{B}$ 块描述了“反共振”的去激发过程（粒子-空穴对的湮灭）。对于一个由占据态 $i$ 到非占据态 $a$ 的跃迁，以及另一个从 $j$到$b$的跃迁，矩阵元可以写为：

$$
A_{ia,jb} = \delta_{ij}\delta_{ab}(\varepsilon_a - \varepsilon_i) + K_{ia,jb}
$$
$$
B_{ia,jb} = K_{ia,jb}
$$

这里的 $K_{ia,jb}$ 是包含库仑作用和交换关联核 $f_{xc}$ 的积分。这个方程可以通过变换，化为一个关于 $\Omega^2$ 的标准厄米[本征值问题](@entry_id:142153)：

$$
(\mathbf{A}-\mathbf{B})^{1/2}(\mathbf{A}+\mathbf{B})(\mathbf{A}-\mathbf{B})^{1/2} \mathbf{Z} = \Omega^2 \mathbf{Z}
$$

或者，在更简单的形式下，如果 $\mathbf{A}-\mathbf{B}$ 是正定的，则问题等价于求解 $(\mathbf{A}-\mathbf{B})(\mathbf{A}+\mathbf{B})$ 的[本征值](@entry_id:154894)。以一个简化的例子说明，如果我们忽略不同跃迁之间的耦合，对于单个跃迁，激发能 $\Omega$ 与KS能级差 $\Delta\varepsilon$ 和核对角元 $K$ 的关系为 $\Omega^2 = \Delta\varepsilon(\Delta\varepsilon + 2K)$ [@problem_id:3451155]。这清楚地表明，TDDFT激发能不仅仅是KS能级差，还包含了电子-空穴相互作用的修正。

一个常见的简化是**塔姆-丹柯夫近似 (Tamm-Dancoff Approximation, TDA)**，它完全忽略了去激发过程，即令 $\mathbf{B}=\mathbf{0}$。此时，[Casida方程](@entry_id:183031)简化为一个标准的厄米[本征值问题](@entry_id:142153)：$\mathbf{A}\mathbf{X} = \Omega \mathbf{X}$。TDA在计算上更简单，并且对于许多系统的价[电子激发](@entry_id:190531)能给出了合理的结果。然而，对于具有显著电荷转移特性的激发，或者在某些体系中存在所谓的“[三重态不稳定性](@entry_id:181992)”时，$\mathbf{B}$ 矩阵变得至关重要，TDA可能会失效，导致激发能出现较大误差甚至得到非物理的结果 [@problem_id:3451154]。因此，在处理这类系统时，必须使用完整的[Casida方程](@entry_id:183031)。

#### [实时TDDFT](@entry_id:754140)

与在[频域](@entry_id:160070)求解本征值问题不同，**实时 (real-time)** TDDFT直接在时域中模拟电子系统的动力学。这种方法在概念上非常直观 [@problem_id:3451109]。其基本流程如下：

1.  系统初始处于其电子基态。
2.  在 $t=0$ 时刻，施加一个弱而短促的[电场](@entry_id:194326)脉冲（称为“**delta-kick**”），这个脉冲将系统从[基态](@entry_id:150928)激发到一个含时的、非定常的叠加态。
3.  随后，在没有外部[电场](@entry_id:194326)的情况下，通过数值求解含时[Kohn-Sham方程](@entry_id:143968)来传播电子[波函数](@entry_id:147440)随时间的演化。
4.  在演化过程中，持续记录系统的**含时偶极矩** $d(t)$。
5.  最后，对含时偶极矩信号 $d(t)$ 进行[傅里叶变换](@entry_id:142120)，即可得到系统的吸收光谱。[光谱](@entry_id:185632)的峰位对应于系统的激发能。

为了获得平滑且物理上合理的[光谱](@entry_id:185632)，通常需要对原始的 $d(t)$ 信号进行处理，例如乘以一个**[窗函数](@entry_id:139733) (window function)** 来减少[截断误差](@entry_id:140949)，以及一个**指数衰减因子**来模拟[激发态](@entry_id:261453)的有限寿命 [@problem_id:3451109]。[实时TDDFT](@entry_id:754140)方法对于计算宽频范围内的整个[光谱](@entry_id:185632)非常有效，并且能够自然地处理[非线性](@entry_id:637147)效应，是[线性响应方法](@entry_id:751324)的有力补充。

### [贝特-萨尔皮特方程](@entry_id:142429) (BSE)

尽管TDDFT在许多情况下表现出色，但它依赖于对交换关联核的近似，这些近似在描述长程[电荷转移激发](@entry_id:174772)或某些材料（如[宽禁带半导体](@entry_id:267755)）中的[激子](@entry_id:147299)效应时可能不够准确。为了获得更高的精度，人们转向基于[多体微扰理论](@entry_id:168555)的**[贝特-萨尔皮特方程](@entry_id:142429) (Bethe-Salpeter Equation, BSE)**。

BSE可以被看作是一个描述[电子-空穴对](@entry_id:142506)的有效薛定谔方程。它建立在GW计算得到的[准粒子能量](@entry_id:173936)之上，并明确地包含电子-空穴间的相互作用。BSE的本征值问题形式上类似于TDA，但其物理内涵更为丰富：

$$
(E_c^{\mathrm{QP}} - E_v^{\mathrm{QP}})\mathbf{A}_{vc} + \sum_{v'c'} K_{vc,v'c'} \mathbf{A}_{v'c'} = \Omega \mathbf{A}_{vc}
$$

其中，$\Omega$ 是激子能量，$E_c^{\mathrm{QP}} - E_v^{\mathrm{QP}}$ 是GW[准粒子](@entry_id:136584)[带隙](@entry_id:191975)，$\mathbf{A}_{vc}$ 是[激子](@entry_id:147299)[波函数](@entry_id:147440)在[电子-空穴对](@entry_id:142506)[基矢](@entry_id:199546)上的展开系数。核心在于**BSE核** $K$，它包含两部分：一个排斥性的、未屏蔽的**交换项**，以及一个吸引性的、被**屏蔽的库仑直接项** $W$。

$$
K = K_{\mathrm{exc}} + K_{\mathrm{dir}}
$$

[屏蔽相互作用](@entry_id:136395) $W(\omega) = \varepsilon^{-1}(\omega)v$ 是BSE方法成功的关键，它描述了[电子和空穴](@entry_id:274534)之间的有效相互作用是如何被材料中其他电子的极化所减弱的。这里，$\varepsilon(\omega)$ 是材料的动态介电函数。对介电函数的处理直接影响了激子能量的计算精度 [@problem_id:3451135]。
- **[静态屏蔽](@entry_id:262850)**：一种简单的近似是使用静态[介电常数](@entry_id:146714) $\varepsilon_0$，即 $W(\omega=0) = \varepsilon_0^{-1}v$。这种近似对于束缚得很紧的[Wannier-Mott激子](@entry_id:140412)是合理的。
- **[动态屏蔽](@entry_id:267421)**：更精确的方法是考虑介电函数的频率依赖性 $\varepsilon(\omega)$。当激子能量 $\Omega$ 接近材料的等离激元能量时，屏蔽效应会发生剧烈变化，此时必须使用[动态屏蔽](@entry_id:267421)。由于 $W$ 依赖于待求的能量 $\Omega$，这使得BSE成为一个需要自洽求解的[非线性](@entry_id:637147)问题 [@problem_id:3451135]。[动态屏蔽](@entry_id:267421)对于正确描述不同类型的激子，如紧束缚的Rydberg[激子](@entry_id:147299)和空间分离的[电荷转移激子](@entry_id:162658)，至关重要。

### 从激发到[光谱](@entry_id:185632)：可观测的性质

计算得到的激发能和[波函数](@entry_id:147440)最终需要与实验测量的[光谱](@entry_id:185632)联系起来。这涉及到[光学跃迁](@entry_id:160047)的强度、选择定则以及[谱线](@entry_id:193408)的形状。

#### 振子强度与选择定则

一个[激发态](@entry_id:261453)是否能在[光谱](@entry_id:185632)中被观测到，以及其强度如何，取决于它的**[振子强度](@entry_id:147221) (oscillator strength)** $f_k$。振子强度与从[基态](@entry_id:150928) $| \Psi_i \rangle$ 到[激发态](@entry_id:261453) $| \Psi_f \rangle$ 的**跃迁偶极矩**的平方成正比：

$$
f_k \propto \Omega_k |\langle \Psi_f | \mathbf{d} | \Psi_i \rangle|^2
$$

其中 $\mathbf{d}$ 是电偶极算符。如果跃迁偶极矩为零，则该跃迁是**偶极禁戒的 (dipole-forbidden)**，对应的[激发态](@entry_id:261453)被称为**暗激子 (dark exciton)**；反之，则为**偶极允许的 (dipole-allowed)**，[激发态](@entry_id:261453)为**亮[激子](@entry_id:147299) (bright exciton)**。

跃迁是否允许，可以由**[对称性选择定则](@entry_id:156619) (symmetry selection rules)** 来判断 [@problem_id:3451126]。在群论的语言中，跃迁偶极矩积分不为零的条件是，被积函数所属的[不可约表示](@entry_id:263310)的[直积](@entry_id:143046)中必须包含全对称表示。对于一个具有反演对称中心的系统，其[基态](@entry_id:150928)通常是偶宇称（gerade, g）。由于偶极算符是奇宇称（ungerade, u），所以只有跃迁到奇宇称的[激发态](@entry_id:261453)才是允许的 ($g \to u$ 跃迁)。此外，吸收强度还依赖于入射光的偏振方向与跃迁偶极矩方向的相对取向，这导致了材料的**[光学各向异性](@entry_id:170933)** [@problem_id:3451126]。

#### [振子强度](@entry_id:147221)的规范不变性

[振子强度](@entry_id:147221)的计算有两种等价的数学形式：**长度规范 (length gauge)** 和**速度规范 (velocity gauge)**，它们分别与位置算符 $\hat{\mathbf{r}}$ 和动量算符 $\hat{\mathbf{p}}$ 的矩阵元相关。在精确的理论中，这两种规范给出的结果必须相同。这种**[规范不变性](@entry_id:137857) (gauge invariance)** 源于[海森堡运动方程](@entry_id:140445)所导出的一个基本关系式 [@problem_id:3451143]：

$$
\langle f | \hat{\mathbf{p}} | i \rangle = i m \omega_{fi} \langle f | \hat{\mathbf{r}} | i \rangle
$$

其中 $\omega_{fi} = E_f - E_i$ 是跃迁频率。在实际计算中，如果[哈密顿量](@entry_id:172864) $H$ 和算符 $\hat{\mathbf{r}}, \hat{\mathbf{p}}$ 的定义不完全自洽（例如，使用非局域赝势时），这个等式可能被破坏，导致两种规范给出不同的结果。检查[规范不变性](@entry_id:137857)是验证计算设置和近似可靠性的一个重要手段 [@problem_id:3451143]。

#### [谱线形状](@entry_id:172308)与求和定则

理论计算得到的[激发能](@entry_id:190368)和振子强度对应于一系列离散的[谱线](@entry_id:193408)（狄拉克 $\delta$ 函数）。然而，实验[光谱](@entry_id:185632)总是展宽的。这种**[谱线](@entry_id:193408)展宽 (line broadening)** 源于[激发态](@entry_id:261453)的有限寿命，它受到各种弛豫和**[退相干](@entry_id:145157) (dephasing)** 过程（如[声子散射](@entry_id:140674)）的影响。一个简单的模型是将每条[谱线](@entry_id:193408)描述为一个**[洛伦兹函数](@entry_id:199503) (Lorentzian)**，其半高全宽（FWHM）与[退相干时间](@entry_id:154396) $T_2$ 成反比 [@problem_id:3451101]。

最后，任何物理上合理的[光谱](@entry_id:185632)都必须满足某些基本定律，其中最重要的是**f-求和定则 (f-sum rule)**。对于光导率 $\sigma_1(\omega)$ 的实部，该定则指出其在所有频率上的积分是一个仅依赖于电子密度 $n$ 和电子质量 $m$ 的常数 [@problem_id:3451147]：

$$
\int_0^\infty \sigma_1(\omega) d\omega = \frac{\pi n e^2}{2m}
$$

这个定则意味着总的光[谱权重](@entry_id:144751)是守恒的。在数值计算中，验证f-求和定则是否满足是检验计算收敛性的一个强有力工具。例如，不充分的**[k点取样](@entry_id:177715)**或过小的**频率积分范围**都会导致计算出的总积分值偏离理论值，从而表明计算结果尚未收敛 [@problem_id:3451147]。

此外，[激发态](@entry_id:261453)还具有自旋属性，可以分为[单重态和三重态](@entry_id:148894)。它们的能量差，即**单重态-三重态劈裂 (singlet-triplet splitting)**，主要由电子-空穴交换作用决定。在重元素存在的体系中，**[自旋-轨道耦合](@entry_id:143520) (spin-orbit coupling, SOC)** 会混合这两种[自旋态](@entry_id:149436)，进一步影响它们的能量和[光学活性](@entry_id:139326) [@problem_id:3451154]。这些更精细的效应也必须在精确的[激发态计算](@entry_id:749156)中加以考虑。