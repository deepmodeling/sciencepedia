## 引言
在材料物理中，理解物质如何响应[电场](@entry_id:194326)是描述和设计功能材料的核心。然而，在原子尺度的微观世界与我们日常经验的宏观世界之间，存在着一道理论的鸿沟：由[原子核](@entry_id:167902)与电子构成的剧烈变化的微观[电场](@entry_id:194326)，如何过渡为我们在[电容器](@entry_id:267364)或半导体器件中处理的平滑、可预测的[宏观电场](@entry_id:196409)？本文旨在系统性地回答这一问题，为读者构建一个关于[宏观电场](@entry_id:196409)与极化的坚实理论框架。在接下来的内容中，我们将首先在“原理与机制”一章中，从空间平均的数学方法出发，建立宏观场的定义，并深入探讨局域场、[频率色散](@entry_id:198142)以及几何效应等核心概念。随后，在“应用与跨学科联系”一章中，我们将展示这些原理如何应用于从[复合材料](@entry_id:139856)到压电器件，再到拓扑绝缘体等前沿领域的实际问题中。最后，通过“动手实践”部分的具体计算，您将有机会将理论知识付诸实践，加深对这些关键物理概念的掌握。

## 原理与机制

在上一章中，我们介绍了在[介电材料](@entry_id:147163)中应用宏观电磁理论的基本概念。本章将深入探讨这些宏观量的微观起源和它们之间的深刻联系。我们将从最基本的层面出发，即如何从充满剧烈变化的微观[电场](@entry_id:194326)中定义一个平滑的宏观场。随后，我们将探讨[材料的极化](@entry_id:271610)响应、频率依赖性、[能量耗散](@entry_id:147406)，以及更高级的概念，如[空间色散](@entry_id:141344)和几何形状对内部场的影响。

### 从微观到宏观：[空间平均](@entry_id:203499)的角色

在原子尺度上，物质由带正电的[原子核](@entry_id:167902)和带负电的电子构成。这些[点电荷](@entry_id:263616)产生的微观[电场](@entry_id:194326) $\mathbf{e}(\mathbf{r})$ 在原子间距（埃，Å）的尺度上会发生剧烈的、快速的[振荡](@entry_id:267781)。直接处理这样的场来描述材料的宏观性质（例如，在[电容器](@entry_id:267364)中的行为）是极其复杂且不切实际的。因此，我们需要一个系统性的方法来滤除这些微观涨落，同时保留在宏观尺度上（例如，微米或更大）变化的[电场](@entry_id:194326)特征。

这个方法就是**空间平均**。我们将[宏观电场](@entry_id:196409) $\mathbf{E}(\mathbf{R})$ 定义为微观[电场](@entry_id:194326) $\mathbf{e}(\mathbf{r})$ 在一个以宏观点 $\mathbf{R}$ 为中心的小区域内的加权平均。最通用的形式是[卷积积分](@entry_id:155865)：

$$
\mathbf{E}(\mathbf{R}) = \int_{\mathbb{R}^3} \mathrm{d}^3 r\, w(\mathbf{R}-\mathbf{r})\, \mathbf{e}(\mathbf{r})
$$

这里的 $w(\mathbf{r})$ 是一个“窗口函数”或权重函数，它定义了如何进行平均。为了使这个定义在物理上有效并与[宏观麦克斯韦方程组](@entry_id:201246)相容，窗口函数 $w(\mathbf{r})$ 必须满足一系列关键条件 [@problem_id:2838412]。

1.  **归一化**：为了确保一个均匀的微观场在平均后保持不变，窗口函数必须归一化，即其在整个空间中的积分为1。
    $$
    \int_{\mathbb{R}^3} \mathrm{d}^3 r\, w(\mathbf{r}) = 1
    $$

2.  **[尺度分离](@entry_id:270204) (Scale Separation)**：窗口函数的特征宽度 $L$ 必须满足一个关键的尺度等级关系。一方面，$L$ 必须远大于原子间距 $a$（例如[晶格常数](@entry_id:158935)），以便能有效地平滑掉原子尺度的[振荡](@entry_id:267781) ($L \gg a$)。另一方面，$L$ 必须远小于[宏观电场](@entry_id:196409)本身发生显著变化的长度尺度 $\ell_E$，以避免模糊我们想要描述的宏观特征 ($L \ll \ell_E$)。因此，我们必须处在一个存在尺度分离的体系中：$a \ll L \ll \ell_E$。

3.  **对称性与局部性**：为了使在 $\mathbf{R}$ 点的宏观场 $\mathbf{E}(\mathbf{R})$ 成为该点附[近场](@entry_id:269780)的一个良好代表，窗口函数应是[中心对称](@entry_id:144242)的偶函数，即 $w(\mathbf{r}) = w(-\mathbf{r})$。这个性质保证了其一阶矩为零 ($\int \mathbf{r} w(\mathbf{r}) \mathrm{d}^3 r = \mathbf{0}$)，从而消除了平均过程中的[一阶修正](@entry_id:155896)项，使得 $\mathbf{E}(\mathbf{R})$ 近似于 $\mathbf{e}(\mathbf{R})$ 的局部平均值，误差阶数为 $(L/\ell_E)^2$。

4.  **算符[交换性](@entry_id:140240)**：为了从微观[麦克斯韦方程组](@entry_id:150940) $\nabla \cdot \mathbf{e} = \rho_{\text{total}}/\epsilon_0$ 过渡到宏观形式，平均算符必须能与[微分](@entry_id:158718)算符（如散度）近似交换。使用一个与平移无关的卷积核 $w(\mathbf{R}-\mathbf{r})$ 并通过分部积分可以证明，$\nabla_{\mathbf{R}} \cdot \mathbf{E}(\mathbf{R}) = \langle \nabla_{\mathbf{r}} \cdot \mathbf{e}(\mathbf{r}) \rangle$。这使得宏观高斯定律得以建立。

这个平均过程不仅定义了[宏观电场](@entry_id:196409) $\mathbf{E}$，也同样定义了宏观[电荷密度](@entry_id:144672) $\langle\rho\rangle$，并允许我们将总[电荷密度](@entry_id:144672)分解为束缚电荷密度 $\rho_b$ 和自由电荷密度 $\rho_f$。宏观**极化强度 (polarization)** $\mathbf{P}$ 正是通过束缚电荷密度定义的，即 $\rho_b = -\nabla \cdot \mathbf{P}$。最终，我们得到了熟悉的宏观静电学基本方程：$\nabla \cdot \mathbf{D} = \rho_f$，其中**[电位移场](@entry_id:273493) (electric displacement field)** $\mathbf{D} = \epsilon_0 \mathbf{E} + \mathbf{P}$。

### 极化与[局域场](@entry_id:146504)

[宏观极化](@entry_id:141855)强度 $\mathbf{P}$ 是单位体积内的平均[电偶极矩](@entry_id:178520)。当一个外加[电场](@entry_id:194326)作用于[介电材料](@entry_id:147163)时，它会诱导原子或分子产生偶极矩。然而，真正作用于单个原子或分子，使其发生极化的场，并不是宏观场 $\mathbf{E}$，而是**局域场 (local field)** $\mathbf{E}_{\text{loc}}$。局域场不仅包含外部施加的宏观场，还包含了材料中所有*其他*偶极子所产生的[电场](@entry_id:194326)。

$$
\mathbf{E}_{\text{loc}} = \mathbf{E} + \mathbf{E}_{\text{internal}}
$$

对 $\mathbf{E}_{\text{internal}}$ 的计算是理解[介电常数](@entry_id:146714)微观起源的核心。一个著名的近似是由Lorentz提出的。他将[局域场](@entry_id:146504)分解为三部分贡献：来自远处偶极子的宏观场，来自假想的Lorentz球面上的表面束缚[电荷](@entry_id:275494)的场，以及球内近邻偶极子的场。对于具有立方对称性的晶体，近邻贡献为零，球面贡献为 $\mathbf{P}/(3\epsilon_0)$，从而得到著名的**Lorentz[局域场](@entry_id:146504)**：

$$
\mathbf{E}_{\text{loc}} = \mathbf{E} + \frac{\mathbf{P}}{3\epsilon_0}
$$

然而，在更复杂的[晶体结构](@entry_id:140373)中，近邻原子（离子）的[排列](@entry_id:136432)方式对局域场有重要且复杂的贡献。此时，内部场与各个子[晶格](@entry_id:196752)上的偶极矩 $\mathbf{p}_{\kappa'}$ 的关系需要通过一个无量纲的**[洛伦兹因子](@entry_id:159588)张量 (Lorentz factor tensor)** $\mathbf{S}(\kappa, \kappa')$ 来描述。这个张量本质上是一个[晶格](@entry_id:196752)求和，它描述了晶体几何结构对[局域场](@entry_id:146504)的影响。例如，我们可以通过计算一个钙钛矿（如SrTiO$_3$）[晶胞](@entry_id:143489)内部的离子对某个特定氧离子位置处局域场的贡献，来具体感受这种几何效应 [@problem_id:147474]。对位于 $a(1/2, 0, 0)$ 的氧离子，仅考虑单元晶胞内其他四个离子（位于 $(0,0,0)$ 的Ti，位于 $a(1/2, 1/2, 1/2)$ 的Sr，以及另外两个O）对其洛伦兹和张量分量 $S_{zz}$ 的贡献，通过直接求和可以发现，即使是这样一个小的离子簇，其贡献也是显著且不平凡的，这凸显了近邻环境在决定局域场中的关键作用。

### 频率相关的[介电响应](@entry_id:140146)：[Drude-Lorentz模型](@entry_id:188313)

[材料的极化](@entry_id:271610)响应并非瞬时完成。当外加[电场](@entry_id:194326)随时间变化时（例如[电磁波](@entry_id:269629)），[介电常数](@entry_id:146714)会表现出对频率 $\omega$ 的依赖性，即**[频率色散](@entry_id:198142) (frequency dispersion)**。

理解[频率色散](@entry_id:198142)的一个经典而强大的模型是**[Drude-Lorentz模型](@entry_id:188313)** [@problem_id:2838420]。该模型将[介电材料](@entry_id:147163)中的束缚电子（或离子）视为一个受驱动的、有阻尼的[谐振子](@entry_id:155622)。在[电场](@entry_id:194326) $\mathbf{E}(t)$ 的驱动下，一个[电荷](@entry_id:275494)为 $-e$、质量为 $m$ 的束缚电子的运动方程为：

$$
m\ddot{\mathbf{x}}(t) + m\gamma\dot{\mathbf{x}}(t) + m\omega_0^2 \mathbf{x}(t) = -e\mathbf{E}(t)
$$

这里，$\omega_0$ 是[谐振子](@entry_id:155622)的固有[共振频率](@entry_id:265742)，$\gamma$ 是描述[能量耗散](@entry_id:147406)的阻尼率。对于一个谐波[电场](@entry_id:194326) $\mathbf{E}(t) = \mathbf{E}_0 e^{-i\omega t}$，我们可以解得电子的[稳态](@entry_id:182458)位移 $\mathbf{x}(\omega)$，进而得到单个偶极矩 $\mathbf{p}(\omega) = -e\mathbf{x}(\omega)$，然后得到[宏观极化](@entry_id:141855)强度 $\mathbf{P}(\omega) = N\mathbf{p}(\omega)$（$N$为单位体积内的[振子](@entry_id:271549)数）。

最终，通过关系 $\mathbf{P} = \epsilon_0 \chi_e \mathbf{E}$ 和 $\varepsilon(\omega) = 1 + \chi_e(\omega)$，我们得到复相对[介电函数](@entry_id:136859) $\varepsilon(\omega)$：

$$
\varepsilon(\omega) = 1 + \frac{\omega_p^2}{\omega_0^2 - \omega^2 + i\omega\gamma}
$$

其中，$\omega_p = \sqrt{Ne^2/(\epsilon_0 m)}$ 是**等离子体频率 (plasma frequency)**，它表征了[电荷](@entry_id:275494)响应的强度。这个公式优雅地捕捉了[介电响应](@entry_id:140146)的丰富物理。

将 $\varepsilon(\omega)$ 分解为实部和虚部 $\varepsilon(\omega) = \varepsilon'(\omega) + i\varepsilon''(\omega)$：

$$
\varepsilon'(\omega) = 1 + \frac{\omega_p^2 (\omega_0^2 - \omega^2)}{(\omega_0^2 - \omega^2)^2 + (\omega\gamma)^2}
$$
$$
\varepsilon''(\omega) = \frac{\omega_p^2 \omega\gamma}{(\omega_0^2 - \omega^2)^2 + (\omega\gamma)^2}
$$

根据实部 $\varepsilon'(\omega)$ 的符号，材料的行为可以分为不同类型。当 $\varepsilon'(\omega)  0$ 时，材料表现出类似金属的行为，[电磁波](@entry_id:269629)无法在其中传播而被强烈反射。这通常发生在驱动频率 $\omega$ 略高于[共振频率](@entry_id:265742) $\omega_0$ 的一个频窗内。当 $\varepsilon'(\omega) > 0$ 时，材料表现为[电介质](@entry_id:147163)，允许[电磁波传播](@entry_id:272130)。虚部 $\varepsilon''(\omega)$ 在共振频率 $\omega \approx \omega_0$ 附近达到峰值，代表了材料在该频率下最强的能量吸收。

### [复介电函数](@entry_id:143480)的物理诠释

[复介电函数](@entry_id:143480)的实部和虚部各自具有明确的物理意义，这可以通过分析[电磁场](@entry_id:265881)与介质的能量交换来揭示。

#### 虚部与能量耗散

考虑一个时谐[电场](@entry_id:194326)作用于介质，单位体积内[电场](@entry_id:194326)对介质做功的[瞬时功率](@entry_id:174754)为 $\mathbf{E}(t) \cdot \frac{\partial \mathbf{D}(t)}{\partial t}$。在一个周期内对该功率进行时间平均，得到的就是单位体积内的平均[耗散功率](@entry_id:177328) $p_{\text{diss}}$。使用复数表示法（采用物理学中常见的 $e^{-i\omega t}$ 约定），可以证明 [@problem_id:2838437]：

$$
p_{\text{diss}} = \frac{1}{2} \Re\{ i\omega \mathbf{E}^* \cdot \mathbf{D} \} = \frac{1}{2} \Re\{ i\omega \epsilon_0 \varepsilon(\omega) |\mathbf{E}|^2 \} = \frac{1}{2} \omega \epsilon_0 \varepsilon''(\omega) |\mathbf{E}|^2
$$

这个结果清晰地表明，**介电函数的虚部 $\varepsilon''(\omega)$直接度量了材料在交变[电场](@entry_id:194326)下的能量吸收或[介电损耗](@entry_id:160863)**。对于一个无源介质（passive medium），它只能吸收能量而不能产生能量，因此必须有 $p_{\text{diss}} \geq 0$，这意味着对所有频率 $\omega > 0$，**$\varepsilon''(\omega) \geq 0$**。

如果材料中还存在自由电荷（如导体中的电子），会产生[传导电流](@entry_id:265343) $\mathbf{J}_{\text{free}} = \sigma \mathbf{E}$，这会带来额外的欧姆损耗 $p_{\text{Ohmic}} = \frac{1}{2}\sigma|\mathbf{E}|^2$。我们可以将这两种损耗统一起来。在[频域](@entry_id:160070)中，[安培-麦克斯韦定律](@entry_id:266368)写作 $\nabla \times \mathbf{H} = \mathbf{J}_{\text{free}} - i\omega\mathbf{D}$。将[本构关系](@entry_id:186508)代入，可以得到：

$$
\nabla \times \mathbf{H} = (\sigma - i\omega\epsilon_0\varepsilon(\omega))\mathbf{E} = -i\omega\epsilon_0 \left( \varepsilon(\omega) + i\frac{\sigma}{\epsilon_0\omega} \right) \mathbf{E}
$$

这启发我们定义一个**有效[复介电函数](@entry_id:143480) (effective complex permittivity)** [@problem_id:2838413]：

$$
\varepsilon_{\text{eff}}(\omega) = \varepsilon(\omega) + i\frac{\sigma}{\epsilon_0\omega}
$$

其虚部 $\varepsilon''_{\text{eff}}(\omega) = \varepsilon''(\omega) + \frac{\sigma}{\epsilon_0\omega}$ 就包含了[介电损耗](@entry_id:160863)和传导损耗两种机制。

#### 实部与[储能](@entry_id:264866)及Kramers-Kronig关系

[介电函数](@entry_id:136859)的**实部 $\varepsilon'(\omega)$ 则与介质中可恢复的储能有关**。它决定了[电磁波](@entry_id:269629)在介质中的传播相速度 $v_p = c/n(\omega)$，其中[折射率](@entry_id:168910) $n(\omega) \approx \sqrt{\varepsilon'(\omega)}$。$\varepsilon'(\omega)$ 描述的是[材料的极化](@entry_id:271610)响应与外场同相的部分，对应于能量的暂时储存与释放。

一个深刻的物理原理是**因果律 (causality)**，即响应不能先于驱动。在数学上，这一物理约束导致[介电函数](@entry_id:136859)的实部和虚部并非相互独立，而是通过**Kramers-Kronig关系**联系在一起：

$$
\varepsilon'(\omega) - 1 = \frac{2}{\pi} \mathcal{P} \int_{0}^{\infty} \frac{\omega' \varepsilon''(\omega')}{\omega'^2 - \omega^2} d\omega'
$$
$$
\varepsilon''(\omega) = -\frac{2\omega}{\pi} \mathcal{P} \int_{0}^{\infty} \frac{\varepsilon'(\omega') - 1}{\omega'^2 - \omega^2} d\omega'
$$

这里 $\mathcal{P}$ 代表[柯西主值](@entry_id:192761)积分。这些关系意味着，只要我们知道了材料在所有频率下的吸收谱（$\varepsilon''(\omega)$），原则上就可以计算出它在任意频率下的[色散](@entry_id:263750)（$\varepsilon'(\omega)$），反之亦然。例如，我们可以为一个理想化的吸收模型，如一个矩形吸收窗口（$\varepsilon_2$ 在 $[\omega_1, \omega_2]$ 之间为常数$A$，其他地方为零），通过Kramers-Kronig积分，精确地计算出其对应的实部 $\varepsilon_1(\omega)$ [@problem_id:147535]。这展示了[吸收与色散](@entry_id:159734)之间不可分割的内在联系。

### 集体激发模式与[介电函数](@entry_id:136859)

介电函数的结构，特别是其[零点和极点](@entry_id:177073)，揭示了材料中**[集体激发](@entry_id:145026)模式 (collective excitations)** 的存在。

-   **极点与[横向模式](@entry_id:163265) (Poles and Transverse Modes)**：在[Drude-Lorentz模型](@entry_id:188313)中，$\varepsilon(\omega)$ 在 $\omega \approx \omega_0$ 处有一个极点。这个共振频率对应于材料中的一种[元激发](@entry_id:140859)。在离子晶体中，这对应于**[横向光学声子](@entry_id:139212) (transverse optical, TO, phonon)** 的频率 $\omega_T$。在此频率下，[晶格振动](@entry_id:140970)与横向[电磁波](@entry_id:269629)（光）发生强烈耦合。

-   **零点与纵向模式 (Zeros and Longitudinal Modes)**：考虑一个没有外部源（$\rho_f=0$）的介质。根据[高斯定律](@entry_id:141493) $\nabla \cdot \mathbf{D} = 0$。是否存在一种可能性，即[电位移场](@entry_id:273493) $\mathbf{D}=0$ 但[电场](@entry_id:194326) $\mathbf{E} \ne 0$？如果存在，那么 $\mathbf{D} = \epsilon_0 \varepsilon(\omega) \mathbf{E} = 0$ 意味着必须有 $\varepsilon(\omega) = 0$。这种情况下存在的[电场](@entry_id:194326)是[纵向场](@entry_id:264833)（$\nabla \times \mathbf{E}=0$）。因此，**介电函数的零点对应于纵向集体激发的频率**。
    -   在离子晶体中，$\varepsilon(\omega_L) = 0$ 定义了**[纵向光学声子](@entry_id:140641) (longitudinal optical, LO, phonon)** 的频率 $\omega_L$。
    -   在金属中（Drude模型，$\omega_0=0$），$\varepsilon(\omega_p) = 0$ 定义了[等离子体频率](@entry_id:137429)，即电子气[集体振荡](@entry_id:158973)（**[等离激元](@entry_id:146184)/plasmon**）的频率。

**Lyddane-Sachs-Teller (LST) 关系**深刻地揭示了这两种模式与材料静态介电性质的联系。通过分析[离子晶体](@entry_id:138598)的[介电函数](@entry_id:136859)表达式，我们可以推导出静态[介电常数](@entry_id:146714) $\epsilon(0)$ 和高频[介电常数](@entry_id:146714) $\epsilon_\infty$（仅包含电子贡献）与[声子频率](@entry_id:753407)的关系 [@problem_id:147479]：

$$
\frac{\epsilon(0)}{\epsilon_\infty} = \left( \frac{\omega_L}{\omega_T} \right)^2
$$

这个关系表明，纵向与[横向光学声子](@entry_id:139212)频率的分裂程度，直接决定了离子对静态[介电常数](@entry_id:146714)的贡献大小。

### [空间色散](@entry_id:141344)：非局域响应

到目前为止，我们都假设某一点的极化强度 $\mathbf{P}(\mathbf{r})$ 只依赖于同一点的[电场](@entry_id:194326) $\mathbf{E}(\mathbf{r})$。这被称为**局域响应近似 (local response approximation)**。然而，在某些情况下，$\mathbf{P}(\mathbf{r})$ 可能还依赖于 $\mathbf{r}$ 点附近邻域的[电场](@entry_id:194326)。这种效应被称为**非局域响应 (nonlocal response)** 或**[空间色散](@entry_id:141344) (spatial dispersion)**。

在傅里叶空间中，这意味着介电函数不仅依赖于频率 $\omega$，还依赖于[波矢](@entry_id:178620) $\mathbf{k}$，即 $\varepsilon(\mathbf{k}, \omega)$。对于各向同性介质，介电函数是一个张量，它可以分解为与波矢 $\mathbf{k}$ 平行的纵向[部分和](@entry_id:162077)垂直的横向部分 [@problem_id:2838399]：

$$
\varepsilon_{ij}(\mathbf{k},\omega) = \varepsilon_{T}(k,\omega)\left(\delta_{ij}-\frac{k_i k_j}{k^2}\right) + \varepsilon_{L}(k,\omega)\frac{k_i k_j}{k^2}
$$

其中 $\varepsilon_T$ 和 $\varepsilon_L$ 分别是**横向和纵向介电函数**。这一分解有重要的物理后果：
-   纵向波（如等离激元）的[色散关系](@entry_id:140395)由 $\varepsilon_L(k, \omega) = 0$ 决定。
-   横向波（如光波）的色散关系由 $k^2 = (\omega^2/c^2) \varepsilon_T(k, \omega)$ 决定。

在长波极限下 ($k \to 0$)，非局域效应消失，横向与纵向介电函数趋于一致，$\varepsilon_T(k\to 0, \omega) = \varepsilon_L(k\to 0, \omega) = \varepsilon(\omega)$，从而回到我们之前讨论的局域[响应理论](@entry_id:188225)。

[空间色散](@entry_id:141344)的一个微观来源可以是原子/分子被诱导出的[四极矩](@entry_id:157717)等更高阶的多极矩。一个[唯象模型](@entry_id:273816)可以通过在极化关系中引入 $\nabla^2 \mathbf{P}$ 项来描述这种效应。分析这种模型可以得到[介电常数](@entry_id:146714)对 $k$ 的最低阶修正，即 $\epsilon_r(k) \approx \epsilon_{r,CM} + S k^2$，其中 $S$ 是[空间色散](@entry_id:141344)系数，它的大小与[非局域耦合](@entry_id:271652)的强度直接相关 [@problem_id:147459]。

### 有限几何中的宏观场：退极化效应

我们之前的所有讨论都隐含地假设介质是无限大的。对于一个有限尺寸的样品，其**形状**对内部[电场](@entry_id:194326)有着至关重要的影响。

当一个介电样品被均匀极化时，它的表面会出现束缚[电荷](@entry_id:275494) $\sigma_b = \mathbf{P} \cdot \hat{\mathbf{n}}$。这些表面电荷自身会产生一个[电场](@entry_id:194326)，该[电场](@entry_id:194326)在样品内部通常与极化方向 $\mathbf{P}$相反，因此被称为**退[极化场](@entry_id:197617) (depolarization field)** $\mathbf{E}_{\text{dep}}$。样品内部的总[电场](@entry_id:194326)是外部施加场与退[极化场](@entry_id:197617)的矢量和：

$$
\mathbf{E}_{\text{in}} = \mathbf{E}_{\text{ext}} + \mathbf{E}_{\text{dep}}
$$

退[极化场](@entry_id:197617)的大小和方向取决于样品的几何形状。一个特别重要且具有解析解的例子是均匀极化的**[椭球体](@entry_id:165811)**。对于一个置于真空中的椭球体，如果其极化强度 $\mathbf{P}$ 沿着一个[主轴](@entry_id:172691)方向，那么其内部的退[极化场](@entry_id:197617) $\mathbf{E}_{\text{dep}}$ 也是均匀的，并且与 $\mathbf{P}$ 方向相反 [@problem_id:2838444]。其关系可以简洁地表示为：

$$
\mathbf{E}_{\text{dep}, i} = -\frac{N_i}{\varepsilon_0} P_i
$$

这里的 $N_i$ 是一个无量纲的**退极化因子 (depolarization factor)**，它只依赖于椭球体三个半轴的比例。三个主轴的退极化因子满足一个重要的求和规则：$N_x + N_y + N_z = 1$。

几个典型的例子包括：
-   **球体**：由于对称性，$N_x=N_y=N_z=1/3$。
-   **垂直于z轴的薄圆盘**：近似于一个在z方向被压扁的椭球，因此 $N_z \approx 1, N_x=N_y \approx 0$。内部的退[极化场](@entry_id:197617)接近于[平行板电容器](@entry_id:266922)的场 $E_z = -P_z/\epsilon_0$。
-   **沿z轴的细长针**：近似于一个在z方向被拉长的椭球，因此 $N_z \approx 0, N_x=N_y \approx 1/2$。沿针方向的退[极化场](@entry_id:197617)几乎为零。

退极化效应在实验和器件应用中至关重要。它意味着，即使对由相同材料制成的不同形状的样品施加相同的外部[电场](@entry_id:194326)，它们内部经历的实际场也可能大相径庭，从而导致截然不同的宏观响应。理解并计算退[极化场](@entry_id:197617)是将无限介质理论应用于现实世界样品的关键一步。