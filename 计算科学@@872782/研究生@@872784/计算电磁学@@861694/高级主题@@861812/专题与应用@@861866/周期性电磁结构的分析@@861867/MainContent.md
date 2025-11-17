## 引言

[周期性电磁结构](@entry_id:753348)，从自然界的蝴蝶翅膀到人造的光子晶体和超材料，是物理学与工程学[交叉](@entry_id:147634)领域中一个至关重要的研究对象。这些结构通过在亚波长到数个波长的尺度上对材料进行周期性排布，能够以非凡的方式操控电磁波的传播、散射和局域化，从而实现传统均匀材料无法企及的功能。理解并精确分析[电磁波](@entry_id:269629)与这些周期性介质的相互作用，是设计新型光学和微波器件，乃至探索新奇物理现象的理论基础。然而，其内在的复杂性，如[带隙](@entry_id:191975)的形成、多重衍射、以及对称性诱导的[奇异模](@entry_id:183903)式，对理论分析和数值计算都构成了独特的挑战。

本文旨在为读者构建一个关于[周期性电磁结构](@entry_id:753348)分析的完整知识框架。我们将从最基本的波动理论出发，逐步深入到当代前沿研究。在第一章“原理与机制”中，我们将详细阐述弗洛凯-布洛赫定理，并介绍[能带结构](@entry_id:139379)、[布里渊区](@entry_id:142395)、[态密度](@entry_id:147894)等核心概念，为整个领域奠定数学和物理基础。随后，在第二章“应用与跨学科连接”中，我们将展示这些基本原理如何应用于衍射光栅、超材料、[拓扑光子学](@entry_id:146464)等广泛领域，并揭示其与声学、凝聚态物理等其他波动系统的深刻类比。最后，在第三章“动手实践”中，我们将通过具体的计算问题，引导读者将理论知识转化为实际的分析能力。通过这三个章节的学习，读者将能够系统地掌握分析[周期性电磁结构](@entry_id:753348)的核心思想与方法。

## 原理与机制

在对[周期性电磁结构](@entry_id:753348)进行分析时，其核心在于理解[电磁波](@entry_id:269629)与周期性介质的相互作用方式。与在均匀介质中的传播不同，周期性结构中的波展现出丰富的现象，如[光子带隙](@entry_id:272781)、衍射和对称性保护的简并等。本章将深入探讨支配这些现象的基本原理和关键机制，为计算分析和器件设计奠定理论基础。

### 弗洛凯-布洛赫定理：周期性的基本法则

分析[周期结构](@entry_id:753351)的第一步是认识到其内在的[平移对称性](@entry_id:171614)。考虑一个[介电常数张量](@entry_id:274052) $\boldsymbol{\varepsilon}(\mathbf{r})$ 和[磁导率](@entry_id:154559)张量 $\boldsymbol{\mu}(\mathbf{r})$ 具有空间周期性的无源线性介质，即对于任何[晶格矢量](@entry_id:161583) $\mathbf{R}$，都有 $\boldsymbol{\varepsilon}(\mathbf{r}+\mathbf{R})=\boldsymbol{\varepsilon}(\mathbf{r})$ 和 $\boldsymbol{\mu}(\mathbf{r}+\mathbf{R})=\boldsymbol{\mu}(\mathbf{r})$。在[频域](@entry_id:160070)中，麦克斯韦方程可以组合成一个关于[电场](@entry_id:194326) $\mathbf{E}$ 的[波动方程](@entry_id:139839)（[主方程](@entry_id:142959)）：
$$ \nabla\times \left( \boldsymbol{\mu}^{-1}(\mathbf{r}) \nabla\times \mathbf{E}(\mathbf{r}) \right) = \left(\frac{\omega}{c}\right)^2 \boldsymbol{\varepsilon}(\mathbf{r}) \mathbf{E}(\mathbf{r}) $$
这是一个广义[本征值问题](@entry_id:142153)，形式为 $\hat{\Theta}\mathbf{E} = \lambda \mathbf{E}$，其中 $\hat{\Theta}$ 是一个包含旋度和介质参数的[微分](@entry_id:158718)算符。

由于介质参数具有周期性，该算符 $\hat{\Theta}$ 与[晶格](@entry_id:196752)[平移算符](@entry_id:756122) $T_{\mathbf{R}}$（定义为 $T_{\mathbf{R}} f(\mathbf{r}) = f(\mathbf{r}+\mathbf{R})$）是对易的，即 $[T_{\mathbf{R}}, \hat{\Theta}] = 0$。根据量子力学和线性代数的基本原理，两个对易的算符拥有一组共同的本征函数。[平移算符](@entry_id:756122)的[本征函数](@entry_id:154705)是满足 $T_{\mathbf{R}} \mathbf{E}(\mathbf{r}) = \lambda_{\mathbf{R}} \mathbf{E}(\mathbf{r})$ 的函数，其[本征值](@entry_id:154894)必须具有 $\lambda_{\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}$ 的形式，其中 $\mathbf{k}$ 是一个常数矢量。

这一结论直接导出了适用于周期性系统中[波动方程](@entry_id:139839)的**弗洛凯-布洛赫定理 (Floquet-Bloch theorem)**。该定理指出，[周期系统](@entry_id:185882)中的[电磁场](@entry_id:265881)[本征模](@entry_id:174677)式（称为**布洛赫模 (Bloch modes)**）可以写成一个平面波与一个具有[晶格](@entry_id:196752)周期性的函数的乘积 [@problem_id:3289507]：
$$ \mathbf{E}_{\mathbf{k}}(\mathbf{r}) = \mathbf{u}_{\mathbf{k}}(\mathbf{r}) e^{i\mathbf{k}\cdot \mathbf{r}} $$
其中 $\mathbf{u}_{\mathbf{k}}(\mathbf{r})$ 是一个矢量函数，它具有与[晶格](@entry_id:196752)相同的周期性，即 $\mathbf{u}_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = \mathbf{u}_{\mathbf{k}}(\mathbf{r})$。矢量 $\mathbf{k}$ 被称为**[布洛赫波矢](@entry_id:746866) (Bloch wavevector)** 或[晶体动量](@entry_id:136369)，它标志着特定布洛赫模的相位特性。

从这种形式可以看出，布洛赫模并非严格的[周期函数](@entry_id:139337)，而是一种**准周期 (quasi-periodic)** 函数。在一个[晶格](@entry_id:196752)周期平移后，场本身会获得一个相位因子：
$$ \mathbf{E}_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = \mathbf{u}_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) e^{i\mathbf{k}\cdot (\mathbf{r}+\mathbf{R})} = \mathbf{u}_{\mathbf{k}}(\mathbf{r}) e^{i\mathbf{k}\cdot \mathbf{r}} e^{i\mathbf{k}\cdot \mathbf{R}} = \mathbf{E}_{\mathbf{k}}(\mathbf{r}) e^{i\mathbf{k}\cdot \mathbf{R}} $$
这个准周期边界条件是数值求解[周期结构](@entry_id:753351)中麦克斯韦方程的核心，它允许我们将计算域从整个无限大的结构缩减到一个单位[晶胞](@entry_id:143489)。对于一个给定的电磁[本征模](@entry_id:174677)式，[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{H}$ 必须共享相同的[布洛赫波矢](@entry_id:746866) $\mathbf{k}$，以保证麦克斯韦方程在整个空间中的一致性 [@problem_id:3289507]。

### [倒易空间](@entry_id:754151)与布里渊区：波传播的舞台

[布洛赫波矢](@entry_id:746866) $\mathbf{k}$ 的引入自然地将我们带入**[倒易空间](@entry_id:754151) (reciprocal space)** 的概念。[倒易空间](@entry_id:754151)是[实空间](@entry_id:754128)[晶格](@entry_id:196752)的[傅里叶对偶](@entry_id:200473)。对于由[基矢](@entry_id:199546) $\{\mathbf{a}_i\}$ 定义的实空间[晶格](@entry_id:196752)，其倒易晶格[基矢](@entry_id:199546) $\{\mathbf{b}_i\}$ 由关系式 $\mathbf{b}_{i}\cdot\mathbf{a}_{j}=2\pi\delta_{ij}$ 定义，其中 $\delta_{ij}$ 是克罗内克符号 [@problem_id:3289447]。倒易晶格由所有形如 $\mathbf{G} = \sum n_i \mathbf{b}_i$（其中 $n_i$ 为整数）的矢量构成。这些[倒易晶格矢量](@entry_id:263351)的关键特性是，对于任何[实空间](@entry_id:754128)[晶格矢量](@entry_id:161583) $\mathbf{R}$，它们的[点积](@entry_id:149019)满足 $e^{i\mathbf{G}\cdot\mathbf{R}} = 1$。

这个特性揭示了[布洛赫波矢](@entry_id:746866)的一个重要性质：冗余性。考虑一个[波矢](@entry_id:178620)为 $\mathbf{k}$ 的布洛赫模 $\mathbf{E}_{\mathbf{k}}(\mathbf{r}) = \mathbf{u}_{\mathbf{k}}(\mathbf{r}) e^{i\mathbf{k}\cdot \mathbf{r}}$。我们可以将其重写为：
$$ \mathbf{E}(\mathbf{r}) = \left( \mathbf{u}_{\mathbf{k}}(\mathbf{r}) e^{-i\mathbf{G}\cdot \mathbf{r}} \right) e^{i(\mathbf{k}+\mathbf{G})\cdot \mathbf{r}} $$
定义一个新的周期[包络函数](@entry_id:749028) $\mathbf{u}'(\mathbf{r}) = \mathbf{u}_{\mathbf{k}}(\mathbf{r}) e^{-i\mathbf{G}\cdot \mathbf{r}}$。由于 $e^{-i\mathbf{G}\cdot(\mathbf{r}+\mathbf{R})} = e^{-i\mathbf{G}\cdot\mathbf{r}} e^{-i\mathbf{G}\cdot\mathbf{R}} = e^{-i\mathbf{G}\cdot\mathbf{r}}$，函数 $\mathbf{u}'(\mathbf{r})$ 仍然是[晶格](@entry_id:196752)周期的。这意味着同一个物理场可以由波矢 $\mathbf{k}$ 或 $\mathbf{k}+\mathbf{G}$ 来标记。因此，所有物理上不等价的[布洛赫波矢](@entry_id:746866)都局限在一个倒易空间的原胞内 [@problem_id:3289507]。

这个用于描述所有唯一布洛赫模的最小区域被称为**[第一布里渊区](@entry_id:269110) (first Brillouin zone, BZ)**。[第一布里渊区](@entry_id:269110)是[倒易晶格](@entry_id:136718)的维格纳-塞茨原胞 (Wigner-Seitz cell)，即[倒易空间](@entry_id:754151)中比到其他任何格点都更接近原点 $(\mathbf{k}=\mathbf{0})$ 的点集。例如，对于一个[三维晶格](@entry_id:188146)，其[基矢](@entry_id:199546)为 $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$，[实空间](@entry_id:754128)原胞的体积为 $V_{\text{cell}} = |\mathbf{a}_{1} \cdot (\mathbf{a}_{2} \times \mathbf{a}_{3})|$。相应地，[第一布里渊区](@entry_id:269110)的体积为 $V_{\text{BZ}} = (2\pi)^3 / V_{\text{cell}}$。这个体积在分析[态密度](@entry_id:147894)等物理量时至关重要 [@problem_id:3289447]。

### [光子](@entry_id:145192)能带结构与态密度

对于布里渊区中的每一个[布洛赫波矢](@entry_id:746866) $\mathbf{k}$，麦克斯韦方程的[本征值问题](@entry_id:142153)会给出一系列离散的本征频率 $\omega_n(\mathbf{k})$，其中 $n$ 是能带指数。这些色散关系 $\omega_n(\mathbf{k})$ 构成了**[光子](@entry_id:145192)[能带结构](@entry_id:139379) (photonic band structure)**。能带结构是理解周期介质中波传播行为的“地图”。

在某些频率范围内，对于任何[波矢](@entry_id:178620) $\mathbf{k}$ 都不存在传播的布洛赫模。这些频率范围被称为**[光子带隙](@entry_id:272781) (photonic bandgaps, PBGs)** 或禁带 (stop bands)。[光子带隙](@entry_id:272781)是[光子晶体](@entry_id:137347)最重要的特性之一，它使得控制光流成为可能。

一维[周期结构](@entry_id:753351)，如多层膜（[布拉格反射](@entry_id:184358)镜），是理解[带隙形成](@entry_id:265171)机理的绝佳模型。我们可以使用**传输矩阵法 (Transfer Matrix Method, TMM)** 来分析这种结构。对于一个由两种介质（[折射率](@entry_id:168910) $n_1, n_2$，厚度 $d_1, d_2$）交替构成的双层单位[晶胞](@entry_id:143489)，其周期为 $a = d_1+d_2$。TMM 通过级联单层传输矩阵来获得单位[晶胞](@entry_id:143489)的总传输矩阵 $T_{\text{cell}}$。结合布洛赫定理，可以推导出[色散关系](@entry_id:140395) [@problem_id:3289424]：
$$ \cos(\beta a) = \cos(k_1 d_1)\cos(k_2 d_2) - \frac{1}{2}\left(\eta + \frac{1}{\eta}\right)\sin(k_1 d_1)\sin(k_2 d_2) $$
其中 $\beta$ 是[布洛赫波](@entry_id:144558)数，$k_j = \omega n_j / c$ 是第 $j$ 层中的波数，$\eta$ 是两层之间的阻抗比。当上式右侧的[绝对值](@entry_id:147688)小于等于 $1$ 时，$\beta$ 为实数，对应于传播模式（通带）。当其[绝对值](@entry_id:147688)大于 $1$ 时，$\beta$ 必须是复数，形式为 $\beta = m\pi/a + i\kappa$，对应于倏逝模式，其振幅随传播呈指数衰减，这便形成了[光子带隙](@entry_id:272781) [@problem_id:3289424]。

与能带结构密切相关的一个概念是**态密度 (density of states, DOS)**，$g(\omega)$，它定义为单位频率间隔内的模式数量。在二维情况下，其形式化定义为：
$$ g(\omega) = \frac{1}{(2\pi)^2} \iint_{\text{BZ}} \delta(\omega - \omega(\mathbf{k}))\, d^2 \mathbf{k} $$
态密度在能带的边界或某些内部点处会出现奇异性，这些点被称为**[范霍夫奇点](@entry_id:144019) (van Hove singularities)**。这些[奇点](@entry_id:137764)发生在能带结构 $\omega(\mathbf{k})$ 的[临界点](@entry_id:144653)上，即[群速度](@entry_id:147686) $\mathbf{v}_g(\mathbf{k}) = \nabla_{\mathbf{k}} \omega(\mathbf{k})$ 为零的点（能带的极大值、极小值或[鞍点](@entry_id:142576)）。在二维系统中，[鞍点](@entry_id:142576)通常会导致态密度的对数发散，这在实验上是可以测量的，并对材料的光学性质产生显著影响 [@problem_id:3289423]。

### 周期界面上的波散射：衍射与倏逝

除了无限大的[周期结构](@entry_id:753351)，更常见的情况是有限或半无限的[周期结构](@entry_id:753351)，例如衍射光栅。当一束平面波入射到周期性界面时，它会散射成一系列离散的**[衍射级](@entry_id:174263) (diffraction orders)**，这些[衍射级](@entry_id:174263)也被称为**[弗洛凯谐波](@entry_id:749458) (Floquet harmonics)**。

这一现象源于切向[波矢](@entry_id:178620)的[相位匹配](@entry_id:189362)条件。入射波在界面上产生了一个切向相位[分布](@entry_id:182848) $e^{i k_{x,i} x}$。由于界面的周期性（周期为 $\Lambda$），散射场必须满足由入射场相位和结构周期性共同决定的[准周期性](@entry_id:272343)。这导致散射场的切向[波矢](@entry_id:178620)只能取一系列离散值 [@problem_id:3289421]：
$$ k_{x,m} = k_{x,i} + \frac{2\pi m}{\Lambda} $$
其中 $m$ 是一个整数，代表[衍射级](@entry_id:174263)次。这个关系是**[光栅方程](@entry_id:174509) (grating equation)** 的波矢形式。

对于每一个[衍射级](@entry_id:174263) $m$，其在介质中的纵向[波矢](@entry_id:178620) $k_{z,m}$ 由[色散关系](@entry_id:140395)决定，例如在均匀介质中，$k_{z,m}^2 = k_{\text{medium}}^2 - k_{x,m}^2$。这里存在两种可能性：
1.  **传播级 (Propagating Orders)**：如果 $|k_{x,m}| \leq k_{\text{medium}}$，那么 $k_{z,m}$ 是实数，对应的[衍射级](@entry_id:174263)是一个在空间中传播的[平面波](@entry_id:189798)。
2.  **倏逝级 (Evanescent Orders)**：如果 $|k_{x,m}| > k_{\text{medium}}$，那么 $k_{z,m}$ 是纯虚数，对应的波场分量 $e^{i k_{z,m} z} = e^{-|k_{z,m}| z}$ 会随着离开界面的距离呈指数衰减，不会将能量带到远场。

因此，对于给定的波长、[入射角](@entry_id:192705)和光栅周期，只有有限个[衍射级](@entry_id:174263)是传播的 [@problem_id:3289431]。

在处理开放的辐射系统时，正确选择 $k_{z,m}$ 的符号至关重要。这由**[索末菲辐射条件](@entry_id:168772) (Sommerfeld Radiation Condition)** 决定，该条件要求在源区域之外，波必须是向外传播或衰减的。对于 $e^{-i\omega t}$ 的时间约定，在 $z>0$ 的[半空间](@entry_id:634770)中，这意味着对于传播级，必须选择 $\mathrm{Re}\{k_{z,m}\} > 0$（代表向 $+z$ 方向传播）；对于倏逝级，必须选择 $\mathrm{Im}\{k_{z,m}\} > 0$（代表向 $+z$ 方向衰减）。合并起来，物理上合理的解要求所有[衍射级](@entry_id:174263)的纵向[波矢](@entry_id:178620)都满足 $\mathrm{Im}\{k_{z,m}\} \ge 0$ 并且对于传播级有 $\mathrm{Re}\{k_{z,m}\} \ge 0$ [@problem_id:3289451]。

### 高级分析方法

#### [对称性与群论](@entry_id:185778)

[晶格](@entry_id:196752)的对称性不仅导致了布洛赫定理，还为模式分类和预测简并性提供了强大的工具——群论。在布里渊区的高对称点（如 $\Gamma, X, M$ 点），波矢 $\mathbf{k}$ 会被[晶格](@entry_id:196752)点群的某些或全部操作保持不变（或仅相差一个倒易晶格矢）。这些操作构成了**[波矢群](@entry_id:203048) (little group)** $G_{\mathbf{k}}$ [@problem_id:3289445]。

布洛赫模可以根据 $G_{\mathbf{k}}$ 的**[不可约表示](@entry_id:263310) (irreducible representations, irreps)** 进行分类。不可约表示的维度决定了在该 $\mathbf{k}$ 点处由对称性保护的最小简并度。例如，对于二维方格子，其点群为 $C_{4v}$。在 $\Gamma$ 点 $(\mathbf{k}=\mathbf{0})$ 和 $M$ 点 $(\mathbf{k}=(\pi/a, \pi/a))$，[波矢群](@entry_id:203048)是整个 $C_{4v}$ 群。该群有一个二维不可约表示 $E$，因此在这些点上可能存在对称性保护的二重[简并态](@entry_id:274678)。而在 $X$ 点 $(\mathbf{k}=(\pi/a, 0))$，[波矢群](@entry_id:203048)降为 $C_{2v}$，其所有不可约表示都是一维的，因此在 $X$ 点没有对称性保护的简并 [@problem_id:3289445]。

此外，对称性还决定了**选择定则 (selection rules)**。一个外部激励源只能激发那些与源具有相同对称性（即变换性质属于同一个不可约表示）的布洛赫模。例如，在 $\Gamma$ 点，[正入射](@entry_id:260681)的平面波，其面内[电场](@entry_id:194326) $(E_x, E_y)$ 变换性质如同矢量，属于 $E$ 表示；而[TM模](@entry_id:266144)式的 $E_z$ 分量（标量）属于全对称表示 $A_1$；[TE模](@entry_id:269850)式的 $H_z$ 分量（[赝标量](@entry_id:196696)）则属于 $A_2$ 表示。因此，[正入射](@entry_id:260681)的平面波只能激发 $E$ 对称性的模式，而无法激发 $A_1$ 或 $A_2$ 对称性的模式，这些模式被称为“暗模式” [@problem_id:3289445]。

#### 损耗、辐射与复数波矢

在理想的无损耗、封闭[周期结构](@entry_id:753351)中，[布洛赫波矢](@entry_id:746866) $\mathbf{k}$ 和频率 $\omega$ 都是实数。然而，在实际系统中，**材料损耗**或向外界的**辐射损耗**会使系统变为非厄米（non-Hermitian）的。在这种情况下，对于给定的实数频率 $\omega$，[布洛赫波矢](@entry_id:746866) $\mathbf{k}$ 会变为复数。

复数波矢的虚部 $\mathrm{Im}(k)$ 描述了布洛赫模在传播过程中的振幅衰减或增长。**因果律 (causality)** 要求，在无源或有损介质中，由源激发的波在远离源的方向上传播时，其振幅必须衰减。对于一个在 $x>0$ 区域向右传播的波，并采用 $e^{-i\omega t}$ 的时间约定，其振幅因子为 $e^{-\mathrm{Im}(k)x}$。为了保证衰减，必须有 $\mathrm{Im}(k) > 0$ [@problem_id:3289428]。

这种衰减的来源可以是：
1.  **材料吸收**：[介电常数](@entry_id:146714)存在正的虚部 $\mathrm{Im}(\epsilon) > 0$，导致能量耗散。
2.  **辐射损耗**：在开放结构中（如[光子晶体波导](@entry_id:160774)），模式的能量可以泄漏到周围的自由空间中，形成所谓的**泄漏模式 (leaky modes)**。
3.  **[带隙](@entry_id:191975)衰减**：即使在无损结构中，当频率处于[光子带隙](@entry_id:272781)内时，波矢也会有虚部，导致倏逝衰减。

在数值计算中，选择具有正确虚部符号的解是保证物理现实性的关键。这通常与正确处理[辐射边界条件](@entry_id:176215)（索末菲条件）直接相关。对于向右传播的泄漏或衰减模式，其布洛赫因子 $q = e^{ika}$ 的模必须小于1，即 $|q|1$，这等价于 $\mathrm{Im}(k)>0$ [@problem_id:3289428]。

#### 数值收敛性与李氏分解法则

在诸如**严格耦合波分析 (Rigorous Coupled-Wave Analysis, RCWA)** 或**傅里叶模态法 (Fourier Modal Method, FMM)** 等基于傅里叶展开的数值方法中，一个核心的挑战是如何处理[介电常数](@entry_id:146714)不连续的界面。当一个函数不连续时，其[傅里叶级数](@entry_id:139455)存在[吉布斯现象](@entry_id:138701)，收敛缓慢。

在计算中，形如 $\mathbf{D} = \epsilon_0\epsilon\mathbf{E}$ 的本构关系在傅里叶空间中变为矩阵乘法。如果直接用 $\epsilon(x)$ 的[傅里叶系数](@entry_id:144886)构建的[托普利茨矩阵](@entry_id:271334) $\llbracket \epsilon \rrbracket$ 来计算，即 $[\mathbf{D}] = \epsilon_0\llbracket \epsilon \rrbracket [\mathbf{E}]$，会遇到严重的收敛问题，特别是在TM偏振下。

对于TM偏振，[电场](@entry_id:194326)的法向分量 $E_x$ 在介质界面上是不连续的，而[电位移场](@entry_id:273493)的法向分量 $D_x$ 却是连续的。这意味着，两个[不连续函数](@entry_id:143848) $\epsilon(x)$ 和 $E_x(x)$ 的乘积是一个[连续函数](@entry_id:137361) $D_x(x)/\epsilon_0$。直接对两个[不连续函数](@entry_id:143848)的傅里叶级数进行卷积，无法有效地重构出一个连续的乘积函数。

L. Li 提出的**分解法则 (factorization rules)** 解决了这个问题。其核心思想是，当两个[不连续函数](@entry_id:143848)的乘积是一个[连续函数](@entry_id:137361)时，应使用**逆规则 (inverse rule)**。我们不直接计算 $D_x$，而是从连续的 $D_x$ 出发来求解不连续的 $E_x$：
$$ [\mathbf{E}_x] = \frac{1}{\epsilon_0} \llbracket \epsilon \rrbracket^{-1} [\mathbf{D}_x] $$
通过对 $\epsilon$ 的[托普利茨矩阵](@entry_id:271334)求逆，该方法在截断的傅里叶空间中隐式地强制了 $D_x$ 的连续性，从而有效抑制了吉布斯现象的影响，极大地提高了TM偏振下RCWA方法的[收敛速度](@entry_id:636873)和精度 [@problem_id:3289452]。正确应用这些法则是[精确模拟](@entry_id:749142)[周期性电磁结构](@entry_id:753348)的关键技术之一。