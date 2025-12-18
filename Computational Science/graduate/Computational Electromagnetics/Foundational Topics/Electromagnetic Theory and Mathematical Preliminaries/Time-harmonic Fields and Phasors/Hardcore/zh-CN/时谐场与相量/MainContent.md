## 引言
在电磁学领域，直接求解完整时域形式的麦克斯韦方程组来分析[电磁波](@entry_id:269629)与物质的相互作用，往往是一项复杂且计算量巨大的任务，尤其是在处理正弦变化的场时。为了应对这一挑战，计算电磁学引入了一种极为强大的数学工具——[相量](@entry_id:270266)（Phasor）变换。该方法专门针对线性时不变（LTI）系统，通过将问题从时域转换到[频域](@entry_id:160070)，巧妙地将复杂的微分方程组转化为易于求解的代数方程组，从而极大地简化了分析过程并提供了深刻的物理洞见。

本文旨在系统性地剖析[时谐场](@entry_id:755985)与[相量](@entry_id:270266)方法的核心理论及其广泛应用。在“原理与机制”一章中，我们将从第一性原理出发，建立相量变换的数学基础，推导[频域](@entry_id:160070)中的麦克斯韦方程，并探讨如何通过复数材料参数来描述介质的[色散](@entry_id:263750)和损耗。随后，在“应用与跨学科连接”一章中，我们将展示[相量法](@entry_id:165812)如何在[材料科学](@entry_id:152226)、[射频工程](@entry_id:274860)、[无损检测](@entry_id:273209)乃至[变换光学](@entry_id:268029)等前沿领域中解决实际问题。最后，“动手实践”部分将通过具体的计算练习，巩固您对理论的理解，并展示如何将这些概念应用于仿真和设计中。通过这三章的学习，您将全面掌握这一分析时谐电磁问题的基石性工具。

## 原理与机制

在分析[电磁场](@entry_id:265881)与物质的相互作用时，直接求解时域中的[麦克斯韦方程组](@entry_id:150940)通常是一项艰巨的任务，尤其是当源和场以正弦形式随时间变化时。幸运的是，对于**线性时不变 (LTI)** 系统，我们可以采用一种强大的数学工具——**相量 (phasor)**，将时域中的[微分方程](@entry_id:264184)转化为[频域](@entry_id:160070)中更易于处理的[代数方程](@entry_id:272665)。本章将从第一性原理出发，系统地阐述[时谐场](@entry_id:755985)与相量的基本原理、核心机制及其在[计算电磁学](@entry_id:265339)中的高级应用。

### 相量变换：从时域到[频域](@entry_id:160070)

处理随时间正弦变化的场的核心思想是，将场的时空依赖性分离开来。一个普遍存在的时谐[标量场](@entry_id:151443)或矢量场分量 $F(\mathbf{r}, t)$，其在空间中每一点都以[角频率](@entry_id:261565) $\omega$ 作正弦[振荡](@entry_id:267781)，可以表示为一个仅依赖于空间位置的[复振幅](@entry_id:164138) $\tilde{F}(\mathbf{r})$ 与一个复指数时间项的乘积的实部。这个[复振幅](@entry_id:164138) $\tilde{F}(\mathbf{r})$ 就是我们所说的**[相量](@entry_id:270266)**。它编码了场在空间各点的振幅和相位信息。

从时域物理场 $F(\mathbf{r}, t)$ 恢复到相量 $\tilde{F}(\mathbf{r})$ 的过程，即**相量变换**，依赖于所选择的时间约定。在电磁学领域，主要存在两种约定 ：

1.  **工程约定 ($e^{j\omega t}$)**: 在电气工程和[计算电磁学](@entry_id:265339)中广泛采用。物理场由下式恢复：
    $$
    \mathbf{E}(\mathbf{r}, t) = \Re\{\tilde{\mathbf{E}}(\mathbf{r}) e^{j\omega t}\}
    $$
    在这种约定下，对时间求导的操作等效于乘以因子 $j\omega$。这是因为：
    $$
    \frac{\partial \mathbf{E}(\mathbf{r}, t)}{\partial t} = \frac{\partial}{\partial t} \Re\{\tilde{\mathbf{E}}(\mathbf{r}) e^{j\omega t}\} = \Re\{\frac{\partial}{\partial t} (\tilde{\mathbf{E}}(\mathbf{r}) e^{j\omega t})\} = \Re\{j\omega \tilde{\mathbf{E}}(\mathbf{r}) e^{j\omega t}\}
    $$
    因此，在[频域](@entry_id:160070)中，我们有变换关系：$\frac{\partial}{\partial t} \leftrightarrow j\omega$。

2.  **物理学约定 ($e^{-i\omega t}$)**: 在[理论物理学](@entry_id:154070)，特别是量子力学中更为常见（通常写作 $e^{-i\omega t}$，其中 $i$ 是虚数单位）。物理场由下式恢复：
    $$
    \mathbf{E}(\mathbf{r}, t) = \Re\{\tilde{\mathbf{E}}(\mathbf{r}) e^{-i\omega t}\}
    $$
    相应地，对时间求导的操作等效于乘以因子 $-i\omega$：$\frac{\partial}{\partial t} \leftrightarrow -i\omega$。

约定的选择是任意的，只要在整个分析过程中保持一致即可。然而，这个选择会直接影响[频域](@entry_id:160070)方程的形式。让我们以麦克斯韦的旋度方程为例。在时域中，它们是：
$$
\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}, \quad \nabla \times \mathbf{H} = \mathbf{J} + \frac{\partial \mathbf{D}}{\partial t}
$$
应用相量变换后，我们得到[频域](@entry_id:160070)（或[相量](@entry_id:270266)域）的麦克斯韦方程组。假设本构关系为 $\mathbf{D} = \epsilon \mathbf{E}$ 和 $\mathbf{B} = \mu \mathbf{H}$，那么：

-   在**工程约定 ($e^{j\omega t}$)** 下：
    $$
    \nabla \times \tilde{\mathbf{E}} = -j\omega \mu \tilde{\mathbf{H}}, \quad \nabla \times \tilde{\mathbf{H}} = \tilde{\mathbf{J}} + j\omega \epsilon \tilde{\mathbf{E}}
    $$

-   在**物理学约定 ($e^{-i\omega t}$)** 下：
    $$
    \nabla \times \tilde{\mathbf{E}} = i\omega \mu \tilde{\mathbf{H}}, \quad \nabla \times \tilde{\mathbf{H}} = \tilde{\mathbf{J}} - i\omega \epsilon \tilde{\mathbf{E}}
    $$

可以看到，方程中虚数单位的符号完全取决于时间约定的选择。在本书的其余部分，除非特别说明，我们将遵循**工程约定 ($e^{j\omega t}$)**。

### [频域](@entry_id:160070)中的[本构关系](@entry_id:186508)

[相量法](@entry_id:165812)的威力不仅在于简化了微分算子，还在于它能优雅地处理材料的[色散](@entry_id:263750)和损耗特性。在[频域](@entry_id:160070)中，材料的响应通常通过复数形式的本构参数来描述。

#### [复介电常数](@entry_id:160910)与[有效介电常数](@entry_id:748820)

对于一个有损耗的[色散介质](@entry_id:180771)，[电位移矢量](@entry_id:197092) $\tilde{\mathbf{D}}$ 与[电场](@entry_id:194326) $\tilde{\mathbf{E}}$ 之间的关系可能存在相位差，这通过**[复介电常数](@entry_id:160910)** $\tilde{\epsilon}(\omega)$ 来描述：
$$
\tilde{\mathbf{D}}(\omega) = \tilde{\epsilon}(\omega) \tilde{\mathbf{E}}(\omega)
$$
通常，[复介电常数](@entry_id:160910)写作 $\tilde{\epsilon}(\omega) = \epsilon'(\omega) - j\epsilon''(\omega)$。实部 $\epsilon'(\omega)$ 与能量存储有关，而虚部 $\epsilon''(\omega)$ 与介质中的极化损耗（即[电磁能](@entry_id:264720)转化为热能）有关。对于无源介质，能量只能被消耗而不能被产生，这要求 $\epsilon''(\omega) \ge 0$。

此外，许多材料同时表现出[介电极化](@entry_id:156345)和欧姆传导两种响应。在时域中，[安培-麦克斯韦定律](@entry_id:266368)包含[传导电流](@entry_id:265343)密度 $\mathbf{J}_c = \sigma \mathbf{E}$ 和位移电流密度 $\frac{\partial \mathbf{D}}{\partial t}$。在[频域](@entry_id:160070)中，这表现为 ：
$$
\nabla \times \tilde{\mathbf{H}} = \tilde{\mathbf{J}}_c + j\omega \tilde{\mathbf{D}} = \sigma \tilde{\mathbf{E}} + j\omega \tilde{\epsilon}(\omega) \tilde{\mathbf{E}}
$$
为了简化方程，通常会将欧姆传导的效应吸收到一个**有效[复介电常数](@entry_id:160910)** $\tilde{\epsilon}_{\text{eff}}(\omega)$ 中。通过合并右侧项，我们得到：
$$
\nabla \times \tilde{\mathbf{H}} = (\sigma + j\omega \tilde{\epsilon}(\omega)) \tilde{\mathbf{E}}
$$
为了将其写成[标准形式](@entry_id:153058) $\nabla \times \tilde{\mathbf{H}} = j\omega \tilde{\epsilon}_{\text{eff}}(\omega) \tilde{\mathbf{E}}$，我们进行比较，可以得到：
$$
j\omega \tilde{\epsilon}_{\text{eff}}(\omega) = \sigma + j\omega \tilde{\epsilon}(\omega)
$$
解出 $\tilde{\epsilon}_{\text{eff}}(\omega)$，我们得到：
$$
\tilde{\epsilon}_{\text{eff}}(\omega) = \tilde{\epsilon}(\omega) + \frac{\sigma}{j\omega} = \tilde{\epsilon}(\omega) - j\frac{\sigma}{\omega}
$$
这个表达式非常重要，它将传导电流视为[位移电流](@entry_id:190231)的异相（相差 $90^\circ$）分量，从而统一了[安培定律](@entry_id:140092)右侧的两个源项。有效[介电常数的虚部](@entry_id:269742)现在包含了[介电损耗](@entry_id:160863)和传导损耗两部分。同样，我们也可以定义复磁导率 $\tilde{\mu}(\omega) = \mu'(\omega) - j\mu''(\omega)$ 来描述磁损耗。

### 平面波与本征阻抗

有了[频域](@entry_id:160070)中的[麦克斯韦方程组](@entry_id:150940)和本构关系，我们便可以分析最基本也是最重要的波动解——均匀[平面波](@entry_id:189798)。在一个无源、均匀、各向同性的介质中，通过对[频域](@entry_id:160070)麦克斯韦方程进行解耦，可以得到关于[电场](@entry_id:194326)相量的矢量[亥姆霍兹方程](@entry_id:149977)：
$$
\nabla^2 \tilde{\mathbf{E}} + k^2 \tilde{\mathbf{E}} = \mathbf{0}
$$
其中 $k = \omega\sqrt{\tilde{\mu}\tilde{\epsilon}}$ 是[复波数](@entry_id:274896)。[平面波解](@entry_id:195230)的形式为 $\tilde{\mathbf{E}}(\mathbf{r}) = \mathbf{E}_0 e^{-j\mathbf{k}\cdot\mathbf{r}}$，其中 $\mathbf{k}$ 是波矢，其大小为 $k$。

对于[平面波](@entry_id:189798)，[电场](@entry_id:194326) $\tilde{\mathbf{E}}$、[磁场](@entry_id:153296) $\tilde{\mathbf{H}}$ 和[波矢](@entry_id:178620) $\mathbf{k}$ 三者相互正交。它们振幅之间的比例由介质的**本征阻抗 (intrinsic impedance)** $\eta$ 决定 。通过求解[平面波](@entry_id:189798)的麦克斯韦方程，可以导出：
$$
\eta = \frac{|\tilde{\mathbf{E}}|}{|\tilde{\mathbf{H}}|} = \sqrt{\frac{\tilde{\mu}}{\tilde{\epsilon}}}
$$
本征阻抗是一个描述介质对[电磁波](@entry_id:269629)“阻碍”程度的量，类似于电路中的阻抗。它的性质深刻地揭示了波的传播特性：

-   **无损介质**: 若介质是无损的（$\tilde{\epsilon}$ 和 $\tilde{\mu}$ 均为实数），则 $\eta = \sqrt{\mu/\epsilon}$ 是一个纯实数。这意味着 $\tilde{\mathbf{E}}$ 和 $\tilde{\mathbf{H}}$ 的[相量](@entry_id:270266)是同相的，即它们的[振荡](@entry_id:267781)在时间和空间上[完全同步](@entry_id:267706)。

-   **有损介质**: 若介质是有损的，例如良导体，其[有效介电常数](@entry_id:748820)近似为 $\tilde{\epsilon} \approx -j\sigma/\omega$（在 $\sigma \gg \omega\epsilon$ 的条件下）。假设介质无磁性（$\tilde{\mu}=\mu_0$），则本征阻抗为：
    $$
    \eta = \sqrt{\frac{\mu_0}{-j\sigma/\omega}} = \sqrt{\frac{j\omega\mu_0}{\sigma}} = \sqrt{\frac{\omega\mu_0}{\sigma}} \sqrt{j} = \sqrt{\frac{\omega\mu_0}{2\sigma}}(1+j)
    $$
    此时，$\eta$ 是一个复数，其相位角为 $\arg(\eta) = \arctan(1) = \pi/4$ 或 $45^\circ$。由于 $\tilde{E} = \eta \tilde{H}$（对于标量分量），这意味着[电场](@entry_id:194326) $\tilde{\mathbf{E}}$ 的[相位超前](@entry_id:269084)[磁场](@entry_id:153296) $\tilde{\mathbf{H}}$ 的相位 $45^\circ$。这种由介质损耗引起的相移是理解有损介质中功率流和能量耗散的关键。

### 界面上的波传播：倏逝与反射

[相量法](@entry_id:165812)在处理边界值问题时尤其有效。考虑一个[平面波](@entry_id:189798)从介质1（[折射率](@entry_id:168910) $n_1$）入射到介质2（[折射率](@entry_id:168910) $n_2$）的平直界面上。根据边界处的[相位匹配](@entry_id:189362)条件，波矢的切向分量必须连续。这直接导出了斯涅尔定律。

更有趣的情况发生在波从光密介质射向光疏介质时（$n_1 > n_2$）。当[入射角](@entry_id:192705) $\theta_1$ 足够大，满足**[全内反射](@entry_id:179014) (Total Internal Reflection, TIR)** 条件 $n_1 \sin\theta_1 > n_2$ 时，透射波将呈现出一种独特的行为 。

在介质2中，[波矢](@entry_id:178620)的法向分量 $k_{z,2}$ 由色散关系 $k_{x,2}^2 + k_{z,2}^2 = k_2^2 = (k_0 n_2)^2$ 决定。由于切向分量连续，$k_{x,2} = k_{x,1} = k_0 n_1 \sin\theta_1$。因此：
$$
k_{z,2}^2 = k_0^2 n_2^2 - (k_0 n_1 \sin\theta_1)^2 = k_0^2 (n_2^2 - n_1^2 \sin^2\theta_1)
$$
在TIR条件下，$n_1^2 \sin^2\theta_1 > n_2^2$，导致 $k_{z,2}^2$ 为负值。这意味着 $k_{z,2}$ 是一个纯虚数。我们将其写作 $k_{z,2} = -j\alpha$，其中衰减常数 $\alpha$ 为正实数，以确保场在 $z \to \infty$ 时衰减：
$$
\alpha = k_0 \sqrt{n_1^2 \sin^2\theta_1 - n_2^2}
$$
此时，介质2中的场具有 $e^{-j k_{x,2} x} e^{-j k_{z,2} z} = e^{-j k_{x,2} x} e^{-\alpha z}$ 的形式。这种场在界面法线方向上（$z$方向）不传播相位，而是呈指数衰减，但在界面[切线](@entry_id:268870)方向上（$x$方向）仍然传播。这种波被称为**倏逝波 (evanescent wave)**。

例如，对于一个频率为 $100 \, \mathrm{GHz}$ 的波，从[折射率](@entry_id:168910) $n_1=1.8$ 的介质以 $50^\circ$ 入射到 $n_2=1.2$ 的介质中，我们发现 $n_1 \sin\theta_1 \approx 1.379 > 1.2$，满足TIR条件。计算出的衰减常数约为 $\alpha \approx 1.42 \times 10^3 \, \mathrm{m}^{-1}$ 。这意味着场强在离开界面约 $1/\alpha \approx 0.7 \, \mathrm{mm}$ 的距离内就会衰减到其表面值的 $1/e$。对于倏逝波，在无损介质中，沿法线方向的时间平均功率流为零，表明能量没有净传入第二介质，而是被完[全反射](@entry_id:179014)。

### [时谐场](@entry_id:755985)中的功率与能量

为了量化[时谐场](@entry_id:755985)中的能量流动和存储，我们引入**复[坡印廷矢量](@entry_id:269386) (complex Poynting vector)** ：
$$
\tilde{\mathbf{S}} = \frac{1}{2} \tilde{\mathbf{E}} \times \tilde{\mathbf{H}}^*
$$
其中 $*$ 表示复共轭。复[坡印廷矢量](@entry_id:269386)是一个功能强大的工具，它的实部和虚部各自具有明确的物理意义。通过对[频域](@entry_id:160070)麦克斯韦方程的操作，可以推导出复[坡印廷定理](@entry_id:261580)的微分形式：
$$
\nabla \cdot \tilde{\mathbf{S}} = -\frac{1}{2}\left( \tilde{\mathbf{E}} \cdot \tilde{\mathbf{J}}_s^* + \sigma |\tilde{\mathbf{E}}|^2 \right) + 2j\omega (w_e - w_m)
$$
其中 $w_e = \frac{1}{4}\epsilon|\tilde{\mathbf{E}}|^2$ 和 $w_m = \frac{1}{4}\mu|\tilde{\mathbf{H}}|^2$ 分别是时间平均的电能密度和[磁能密度](@entry_id:193006)。

-   **实部**: $\tilde{\mathbf{S}}$ 的实部 $\Re\{\tilde{\mathbf{S}}\}$ 等于[时间平均](@entry_id:267915)的功率流密度，即真实的[坡印廷矢量](@entry_id:269386)在一个周期内的平均值。上式实部描述了[能量守恒](@entry_id:140514)：$\Re\{\tilde{\mathbf{S}}\}$ 的散度等于单位体积内消耗的功率（欧姆损耗）和源所做的功。

-   **虚部**: $\tilde{\mathbf{S}}$ 的虚部 $\Im\{\tilde{\mathbf{S}}\}$ 代表**[无功功率](@entry_id:192818)流密度 (reactive power flow density)**。上式虚部 $\nabla \cdot \Im\{\tilde{\mathbf{S}}\} = 2\omega(w_e - w_m)$ 表明，[无功功率](@entry_id:192818)流的散度与[时间平均](@entry_id:267915)的电能密度和[磁能密度](@entry_id:193006)之差成正比。这揭示了一个深刻的物理图像：
    -   当一个区域的平均电能存储大于[磁能](@entry_id:268850)存储（$w_e > w_m$）时，该点表现为“容性”，是[无功功率](@entry_id:192818)的“源”。
    -   当平均[磁能](@entry_id:268850)存储大于电能存储（$w_m > w_e$）时，该点表现为“感性”，是[无功功率](@entry_id:192818)的“汇”。

这种能量在电场和磁场之间的来回[振荡](@entry_id:267781)交换，而不是净的单向传输，是[驻波](@entry_id:148648)和**无功近场 (reactive near-field)** 的典型特征。例如，在一个小电偶极子天线的[近场](@entry_id:269780)区域，电能存储远大于[磁能](@entry_id:268850)存储（$w_e \gg w_m$），因此该区域向外发出大量的[无功功率](@entry_id:192818)，表现为净的正 $\Im\{\tilde{\mathbf{S}}\}$ 通量 。当电场和磁场相位相差 $90^\circ$（正交）时，$\Re\{\tilde{\mathbf{S}}\}=0$，表示没有净功率传输，只有纯粹的能量[振荡](@entry_id:267781)交换。

### 高级主题与扩展

[相量法](@entry_id:165812)是分析复杂电磁现象的基石，其适用范围远不止各向同性介质。

#### [各向异性介质](@entry_id:187796)

在**各向异性 (anisotropic)** 介质（如晶体）中，[介电常数](@entry_id:146714)是一个[二阶张量](@entry_id:199780) $\bar{\bar{\epsilon}}$，$\tilde{\mathbf{D}} = \bar{\bar{\epsilon}} \cdot \tilde{\mathbf{E}}$ 。这导致了一系列丰富的现象：
-   **双折射 (Birefringence)**: 通常情况下，对于给定的传播方向，存在两个具有不同[传播常数](@entry_id:272712)和正交偏振的本征模式。这导致[线偏振光](@entry_id:165445)在传播过程中会演变为[椭圆偏振光](@entry_id:195140)。
-   **场矢量关系**: 在[各向异性介质](@entry_id:187796)中，虽然 $\tilde{\mathbf{D}}$ 始终垂直于波矢 $\mathbf{k}$，但 $\tilde{\mathbf{E}}$ 通常不垂直于 $\mathbf{k}$，即[电场](@entry_id:194326)可以有纵向分量。
-   **[二向色性](@entry_id:166658) (Dichroism)**: 如果 $\bar{\bar{\epsilon}}$ 是复数张量，不同偏振的[本征模](@entry_id:174677)式会经历不同的衰减。这会导致最初的[线偏振光](@entry_id:165445)在传播过程中不仅变为[椭圆偏振](@entry_id:270497)，而且其[主轴](@entry_id:172691)会逐渐趋向于衰减最小的那个主轴方向 。
-   **[旋光性](@entry_id:139326) (Gyrotropy)**: 在某些磁化介质中，$\bar{\bar{\epsilon}}$ 是一个非对称的厄米张量。这会导致沿特定方向传播的[本征模](@entry_id:174677)式是左旋和右旋圆偏振波，它们有不同的[传播速度](@entry_id:189384)，从而产生法拉第旋光效应 。

#### 手性介质

**双各向同性 (bi-isotropic)** 或**手性 (chiral)** 介质表现出更复杂的[电磁耦合](@entry_id:203990)，其本构关系为 ：
$$
\mathbf{D} = \epsilon\mathbf{E} + \xi \mathbf{H}, \quad \mathbf{B} = \mu\mathbf{H} + \zeta \mathbf{E}
$$
在这种介质中，[电场和磁场](@entry_id:261347)相互耦合。其本征模式是左旋和[右旋圆偏振](@entry_id:267955)波，它们的[传播常数](@entry_id:272712) $k_+$ 和 $k_-$ 不同。这种差异导致：
-   **[旋光](@entry_id:201162) (Optical Rotation)**: 由 $\Re(k_+)$ 和 $\Re(k_-)$ 的差异引起，[线偏振光](@entry_id:165445)的偏振面会随着传播而旋转。
-   **[圆二色性](@entry_id:165862) (Circular Dichroism)**: 由 $\Im(k_+)$ 和 $\Im(k_-)$ 的差异引起，左旋和[右旋圆偏振](@entry_id:267955)分量被不同程度地吸收，导致线偏振光变为[椭圆偏振光](@entry_id:195140)。

#### 运动介质与计算考虑

[相量法](@entry_id:165812)甚至可以推广到处理**运动介质 (moving media)** 中的电磁学问题。使用一阶近似的闵可夫斯基关系，可以分析光在运动介质中的传播。一个关键效应是，当光从静止介质入射到运动介质时，透射波的频率会发生[多普勒频移](@entry_id:158041) 。这给计算带来了挑战，因为不同区域的场具有不同的频率，需要在数值方法（如[有限元法](@entry_id:749389)）中采用特殊的多[频域](@entry_id:160070)耦合策略。

在[计算电磁学](@entry_id:265339)中，求解开放区域的亥姆霍兹方程时，需要施加边界条件来模拟波向无穷远处的辐射，即**[索末菲辐射条件](@entry_id:168772) (Sommerfeld radiation condition)**。为了保证数值[解的唯一性](@entry_id:143619)和物理正确性，**极限吸收原理 (limiting absorption principle)** 提供了一个强大的正则化工具 。该原理指出，通过在介质中引入一个微小的、趋于零的损耗项（例如，$\epsilon \to \epsilon - j\eta$），可以唯一地选出物理上正确的向外辐射解。这在理论上确立了计算中[辐射边界条件](@entry_id:176215)的合法性。

### [适用范围](@entry_id:636189)与局限性：[非线性](@entry_id:637147)介质

尽管[相量法](@entry_id:165812)功能强大，但其应用有一个根本性的前提：**线性**。[相量法](@entry_id:165812)的数学基础是[傅里叶变换](@entry_id:142120)，它依赖于叠加原理，而[叠加原理](@entry_id:144649)仅在 LTI 系统中成立。

当介质具有**[非线性](@entry_id:637147) (nonlinear)** 响应时，例如存在二阶[非线性极化](@entry_id:272949) $P_{\mathrm{NL}}(t) = \epsilon_0 \chi^{(2)} E^2(t)$，情况会发生根本性改变 。考虑一个双频激励信号 $E(t) = E_1 \cos(\omega_1 t) + E_2 \cos(\omega_2 t)$。[非线性](@entry_id:637147)项 $E^2(t)$ 将会产生新的频率分量：
$$
E^2(t) \Rightarrow \text{DC (0)}, 2\omega_1, 2\omega_2, \omega_1+\omega_2, |\omega_1-\omega_2|
$$
这些新产生的频率被称为**[谐波](@entry_id:181533) (harmonics)** 和**互调产物 (intermodulation products)**。由于输出包含了输入中不存在的频率，系统不再是线性的。在[频域](@entry_id:160070)中，这意味着不同频率分量之间发生了耦合。例如，$\omega_1+\omega_2$ 处的响应同时依赖于 $\omega_1$ 和 $\omega_2$ 处的激励。

因此，标准的单频[相量法](@entry_id:165812)在此失效。为了在[频域](@entry_id:160070)中分析此类[非线性](@entry_id:637147)问题，需要使用更高级的技术，如**[谐波平衡法](@entry_id:166315) (Harmonic Balance, HB)**。[谐波平衡法](@entry_id:166315)的核心思想是，假设解是所有相关频率（[基频](@entry_id:268182)、[谐波](@entry_id:181533)、互调产物）的相量之和。然后，它将在时域中的非线性关系（如乘法）转化为[频域](@entry_id:160070)中的卷积，从而建立一个耦合的[非线性](@entry_id:637147)[代数方程](@entry_id:272665)组，求解这个[方程组](@entry_id:193238)可以得到所有频率分量的[稳态](@entry_id:182458)[相量](@entry_id:270266)。从这个角度看，[谐波平衡法](@entry_id:166315)可以被视为[相量法](@entry_id:165812)向[非线性](@entry_id:637147)周期性或多频激励问题的一个自然推广。