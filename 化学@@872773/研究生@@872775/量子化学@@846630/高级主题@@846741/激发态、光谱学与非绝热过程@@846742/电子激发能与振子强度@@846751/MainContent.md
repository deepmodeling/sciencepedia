## 引言
电子激发是自然界中最基本的物理化学过程之一，它驱动着从光合作用到视觉感知，再到有机发光二极管（OLED）等现代技术的一切。当分子吸收[光子](@entry_id:145192)时，电子从低能级[轨道](@entry_id:137151)跃迁到高能级[轨道](@entry_id:137151)，这一过程的细节决定了物质的颜色、光化学反应性和发光特性。然而，要将分子与光相互作用的宏观现象与微观的量子力学世界精确地联系起来，需要一个严谨的理论框架。这正是本篇文章旨在解决的核心问题：我们如何从第一性原理出发，定量地计算和理解电子激发能和跃迁强度？

本文为研究生水平的学习者设计，旨在系统地阐述电子激发能和[振子强度](@entry_id:147221)的理论、计算与应用。通过本文的学习，您将能够：

- 在 **“原理与机制”** 章节中，掌握描述[电子跃迁](@entry_id:152949)的量子力学基础，包括[势能面](@entry_id:147441)、[弗兰克-康登原理](@entry_id:151864)、跃迁偶极矩以及决定跃迁强度的振子强度。您将理解[对称性选择定则](@entry_id:156619)的起源，以及[自旋-轨道耦合](@entry_id:143520)等效应如何打破这些规则。
- 在 **“应用与交叉学科联系”** 章节中，探索这些理论概念在[分子光谱学](@entry_id:148164)、[光化学](@entry_id:140933)和[材料科学](@entry_id:152226)中的实际应用。您将学习如何通过计算来预测分子颜色、评估防晒剂性能、设计高效OLED材料，并理解环境效应对激发过程的影响。
- 在 **“动手实践”** 部分，通过一系列精心设计的计算练习，将理论知识转化为实践技能，从推导氢原子的振子强度到应用高级计算方法，从而巩固您的理解。

本文将引导您深入探索光与[分子相互作用](@entry_id:263767)的奥秘，为您在[量子化学](@entry_id:140193)及相关领域的研究打下坚实的基础。

## 原理与机制

在“引言”章节中，我们概述了电子激发在化学和物理学中的核心地位。本章将深入探讨控制这些过程的量子力学原理和基本机制。我们将从分子结构与能量的关系出发，建立[电子跃迁](@entry_id:152949)的理论框架，进而量化其与[电磁辐射](@entry_id:152916)相互作用的强度，并最终阐述决定跃迁“允许”或“禁戒”的[对称性选择定则](@entry_id:156619)。

### 电子跃迁的量子力学图像

在[分子量子力学](@entry_id:203843)中，**玻恩-奥本海默近似 (Born-Oppenheimer approximation)** 是一个基石性的概念。由于[原子核](@entry_id:167902)的质量远大于电子，我们可以假定在电子运动的瞬间，[原子核](@entry_id:167902)的位置是固定的。这使得我们能够将分子的总[哈密顿量分离](@entry_id:192546)，首先在固定的[原子核](@entry_id:167902)构型 $\mathbf{R}$ 下求解[电子薛定谔方程](@entry_id:177999)，得到一系列电子态及其对应的能量 $E_i(\mathbf{R})$。这些能量作为[原子核](@entry_id:167902)坐标 $\mathbf{R}$ 的函数，构成了**[势能面](@entry_id:147441) (Potential Energy Surfaces, PESs)**。

每个电子态（如[基态](@entry_id:150928) $S_0$ 和第一电子激发态 $S_1$）都拥有其自身的[势能面](@entry_id:147441)。分子的平衡几何构型对应于其所在电子态[势能面](@entry_id:147441)的最低点。我们将[基态](@entry_id:150928) $S_0$ 和[激发态](@entry_id:261453) $S_1$ 的平衡构型分别记为 $\mathbf{R}_g$ 和 $\mathbf{R}_e$。

基于[势能面](@entry_id:147441)的概念，我们可以精确定义两种重要的电子激发能 [@problem_id:2889023]：

1.  **[垂直激发能](@entry_id:165593) ($\Delta E_{\mathrm{vert}}$)**：根据**[弗兰克-康登原理](@entry_id:151864) (Franck-Condon principle)**，[电子跃迁](@entry_id:152949)（吸收或发射[光子](@entry_id:145192)）发生得如此之快，以至于[原子核](@entry_id:167902)来不及移动。因此，从[基态](@entry_id:150928)吸收[光子](@entry_id:145192)最可能发生的跃迁是在[基态](@entry_id:150928)的平衡构型 $\mathbf{R}_g$ 处“垂直”向上跃迁到[激发态](@entry_id:261453)的[势能面](@entry_id:147441)上。[垂直激发能](@entry_id:165593)即为在[基态](@entry_id:150928)平衡构型 $\mathbf{R}_g$ 处，[激发态](@entry_id:261453)与[基态](@entry_id:150928)之间的能量差：
    $$
    \Delta E_{\mathrm{vert}} = E_{S_1}(\mathbf{R}_g) - E_{S_0}(\mathbf{R}_g)
    $$
    这个能量通常对应于分子吸收光谱中的最大吸收峰位置。

2.  **绝热激发能 ($\Delta E_{\mathrm{adia}}$)**：绝热激发能被定义为[激发态](@entry_id:261453)[势能面](@entry_id:147441)的最低点与[基态](@entry_id:150928)[势能面](@entry_id:147441)的最低点之间的能量差。若不考虑[振动](@entry_id:267781)零点能 (Zero-Point Energy, ZPE) 的修正，该能量为：
    $$
    \Delta E_{\mathrm{adia}} = E_{S_1}(\mathbf{R}_e) - E_{S_0}(\mathbf{R}_g)
    $$
    绝[热激发](@entry_id:275697)能代表了从一个稳定结构转变为另一个稳定结构所需的最少能量。在实验上，它与[光谱](@entry_id:185632)中 **[0-0跃迁](@entry_id:261697)** 的能量密切相关。[0-0跃迁](@entry_id:261697)指的是[激发态](@entry_id:261453)的最低振动能级 ($v'=0$) 与[基态](@entry_id:150928)的最低振动能级 ($v=0$) 之间的跃迁。其能量为 $\Delta E_{0-0} = \Delta E_{\mathrm{adia}} + [\text{ZPE}(S_1) - \text{ZPE}(S_0)]$。只有当两个电子态的零点能恰好相同时，绝[热激发](@entry_id:275697)能才等于[0-0跃迁](@entry_id:261697)能，但这通常不成立。

### 与光的相互作用和跃迁概率

电子跃迁是由分子与电磁辐射的相互作用诱导的。在弱场和长波长极限下，这种相互作用主要由**[电偶极近似](@entry_id:150449) (electric-dipole approximation)** 描述。在此近似下，分子与光的[相互作用哈密顿量](@entry_id:181720)为 $\hat{H}'(t) = -\hat{\boldsymbol{\mu}} \cdot \mathbf{E}(t)$，其中 $\mathbf{E}(t)$ 是光的[时变电场](@entry_id:197741)，而 $\hat{\boldsymbol{\mu}}$ 是分子的[电偶极矩](@entry_id:178520)算符。

分子的总[电偶极矩](@entry_id:178520)算符包含对电子和[原子核](@entry_id:167902)的贡献：
$$
\hat{\boldsymbol{\mu}} = -\ e\sum_{i}\hat{\mathbf{r}}_i + e\sum_{A} Z_A \hat{\mathbf{R}}_A = \hat{\boldsymbol{\mu}}_e + \hat{\boldsymbol{\mu}}_n
$$
其中，$\hat{\mathbf{r}}_i$ 是电子的位置算符，$\hat{\mathbf{R}}_A$ 是[原子核](@entry_id:167902)的位置算符，$Z_A$ 是核[电荷](@entry_id:275494)数，$e$ 是基本电荷。

根据[含时微扰理论](@entry_id:141200)，从初态 $|i\rangle$ 到末态 $|f\rangle$ 的跃迁概率正比于**跃迁偶极矩 (transition dipole moment, TDM)** 的平方，即 $|\boldsymbol{\mu}_{if}|^2 = |\langle f | \hat{\boldsymbol{\mu}} | i \rangle|^2$。对于电子跃迁，初末态是不同的电子态[波函数](@entry_id:147440)，例如 $|\Psi_0\rangle$ 和 $|\Psi_n\rangle$。一个关键问题是，在计算电子跃迁的 TDM 时，我们是否需要考虑[原子核](@entry_id:167902)的贡献 $\hat{\boldsymbol{\mu}}_n$ [@problem_id:2889002]。

在[玻恩-奥本海默近似](@entry_id:146252)的框架下，电子[波函数](@entry_id:147440) $|\Psi_k(\mathbf{r}; \mathbf{R})\rangle$ 是在[固定核](@entry_id:169539)构型 $\mathbf{R}$ 下求解的。作为同一厄米算符（[电子哈密顿量](@entry_id:177588) $\hat{H}_e$）的不同本征态，它们是正交的：$\langle \Psi_0 | \Psi_n \rangle = \delta_{0n}$。我们来考察 TDM 中[原子核](@entry_id:167902)项的贡献：
$$
\langle \Psi_0 | \hat{\boldsymbol{\mu}}_n | \Psi_n \rangle = \left\langle \Psi_0 \left| e\sum_{A} Z_A \mathbf{R}_A \right| \Psi_n \right\rangle
$$
由于 $\hat{\boldsymbol{\mu}}_n$ 是一个只依赖于核坐标 $\mathbf{R}$ 的乘法算符，在对电子坐标 $\mathbf{r}$ 积[分时](@entry_id:274419)可被视为常数提出：
$$
\langle \Psi_0 | \hat{\boldsymbol{\mu}}_n | \Psi_n \rangle = \left( e\sum_{A} Z_A \mathbf{R}_A \right) \langle \Psi_0 | \Psi_n \rangle = \hat{\boldsymbol{\mu}}_n(\mathbf{R}) \cdot \delta_{0n}
$$
对于电子激发（$n \neq 0$），电子态的正交性导致 $\langle \Psi_0 | \Psi_n \rangle = 0$，因此[原子核](@entry_id:167902)项的贡献严格为零。这意味着，计算[电子跃迁](@entry_id:152949)的跃迁偶极矩时，我们只需考虑电子部分 $\hat{\boldsymbol{\mu}}_e$。这一结论并非近似，而是在玻恩-奥本海默框架下的严格推论，它不依赖于分子的总[电荷](@entry_id:275494)是中性还是离子。

因此，电子跃迁偶极矩为：
$$
\boldsymbol{\mu}_{0n} = \langle \Psi_0 | \hat{\boldsymbol{\mu}} | \Psi_n \rangle = \langle \Psi_0 | \hat{\boldsymbol{\mu}}_e | \Psi_n \rangle
$$
一个重要的物理性质是，跃迁偶极矩 $\boldsymbol{\mu}_{0n}$ 是与坐标原点选择无关的。如果将坐标原点移动一个矢量 $\mathbf{a}$，新的偶极算符为 $\hat{\boldsymbol{\mu}}' = \hat{\boldsymbol{\mu}} - Q_{\text{tot}}\mathbf{a}$，其中 $Q_{\text{tot}}$ 是体系的总[电荷](@entry_id:275494)。新的 TDM 为 $\boldsymbol{\mu}'_{0n} = \boldsymbol{\mu}_{0n} - Q_{\text{tot}}\mathbf{a} \langle 0 | n \rangle$。由于电子态的正交性 $\langle 0 | n \rangle = 0$，我们得到 $\boldsymbol{\mu}'_{0n} = \boldsymbol{\mu}_{0n}$，证明了其原点无关性 [@problem_id:2889002]。

### 量化跃迁强度：[振子强度](@entry_id:147221)

虽然跃迁偶极矩的平方决定了跃迁概率，但在[光谱学](@entry_id:141940)中，我们通常使用一个更方便的无量纲量——**[振子强度](@entry_id:147221) (oscillator strength)** $f_{0n}$ 来量化跃迁的强度。它代表了一个电子跃迁吸收或发射[光子](@entry_id:145192)的能力，相当于经典力学中一个谐振子的强度。

在[原子单位](@entry_id:166762)制（$e=m_e=\hbar=1$）和长度规范（length gauge）下，对于从[基态](@entry_id:150928) $|0\rangle$ 到[激发态](@entry_id:261453) $|n\rangle$ 的吸收跃迁，经过对[分子取向](@entry_id:198082)的各向同性平均后，振子强度的定义为 [@problem_id:2889028]：
$$
f_{0n} = \frac{2}{3} \Delta E_{n0} \left| \langle 0 | \hat{\boldsymbol{\mu}}_e | n \rangle \right|^2 = \frac{2}{3} \Delta E_{n0} \sum_{\alpha=x,y,z} \left| \langle 0 | \hat{\mu}_{e,\alpha} | n \rangle \right|^2
$$
其中：
-   $\Delta E_{n0} = E_n - E_0$ 是以 Hartree 为单位的[垂直激发能](@entry_id:165593)，对于吸收过程 $\Delta E_{n0} > 0$。
-   $\hat{\boldsymbol{\mu}}_e = -\sum_i \hat{\mathbf{r}}_i$ 是总的电子偶极矩算符。
-   $\langle 0 | \hat{\mu}_{e,\alpha} | n \rangle$ 是跃迁偶极矩的笛卡尔分量。
-   $\frac{1}{3}$ 因子来源于对分子随机取向相对于光偏振方向的三维[空间平均](@entry_id:203499)。

从物理意义上讲，振子强度 $f_{0n}$ 正比于实验上可观测的吸收谱带的积分面积（积分[吸收截面](@entry_id:172609)），因此它量化了该跃迁所携带的**谱重 (spectral weight)**，且该积分值与[谱线](@entry_id:193408)展宽的具体机制无关 [@problem_id:2889025]。

[振子强度](@entry_id:147221)的一个极为重要的性质由**托马斯-赖歇-库恩 (Thomas-Reiche-Kuhn, TRK) 加和定则**所描述。该定则指出，对于一个包含 $N_e$ 个电子的非相对论性体系，从[基态](@entry_id:150928) $|0\rangle$ 出发到所有可能的[激发态](@entry_id:261453) $|n\rangle$（包括束缚态和电离[连续谱](@entry_id:155477)）的振子强度之和，等于体系的总电子数 [@problem_id:2889059] [@problem_id:2889025]：
$$
\sum_{n} f_{0n} = N_e
$$
TRK加和定则是一个精确的量子力学结果，其成立的条件非常普适：它仅要求[哈密顿量](@entry_id:172864)中的势能项只依赖于坐标（即局域势），而与[电子-电子相互作用](@entry_id:139900)的具体形式无关，也无需采用独立粒子近似。该定则为理论计算提供了一个重要的检验标准。在实际的[量子化学](@entry_id:140193)计算中，由于通常采用有限的[基组](@entry_id:160309)和不完整的激发空间，计算得到的振子强度之和往往不等于 $N_e$。计算结果与 $N_e$ 的偏离程度，以及长度规范和速度规范（另一种等价的[振子强度](@entry_id:147221)形式）计算结果之间的一致性，可以作为衡量计算完备性和准确性的指标 [@problem_id:2889025]。

### [电子跃迁的选择定则](@entry_id:192423)

跃迁偶极矩的表达式 $\boldsymbol{\mu}_{if} = \langle f | \hat{\boldsymbol{\mu}} | i \rangle$ 意味着，如果这个积分因对称性原因而恒等于零，那么该跃迁就是**禁戒的 (forbidden)**，其[振子强度](@entry_id:147221)为零。这些导致跃迁偶极矩为零的对称性约束被称为**选择定则 (selection rules)**。

#### 宇称和角动量[选择定则](@entry_id:140784)

在具有[中心对称](@entry_id:144242)性的体系中（如原子），[波函数](@entry_id:147440)具有确定的**宇称 (parity)**。在空间反演操作 $\hat{\Pi}$（即 $\mathbf{r} \to -\mathbf{r}$）下，偶极矩算符是[奇宇称](@entry_id:147965)的（$\hat{\Pi} \hat{\boldsymbol{\mu}} \hat{\Pi}^{-1} = -\hat{\boldsymbol{\mu}}$），而原子轨道[波函数的宇称](@entry_id:183828)为 $(-1)^l$，其中 $l$ 是[轨道角动量量子数](@entry_id:167573)。为了使跃迁偶极矩的积分不为零，被积函数 $\Psi_f^* \hat{\boldsymbol{\mu}} \Psi_i$ 的整体宇称必须为偶。这要求初末态的宇称必须相反，即 $(-1)^{l_f} \neq (-1)^{l_i}$。这一结论被称为**拉波特定则 (Laporte rule)**，它要求跃迁过程中宇称必须改变 [@problem_id:2889040]。

此外，[电偶极矩](@entry_id:178520)算符 $\hat{\mathbf{r}}$ 在[旋转操作](@entry_id:140575)下表现为一个秩为1的[球张量算符](@entry_id:150041)。根据**[维格纳-埃卡特定理](@entry_id:144878) (Wigner-Eckart theorem)**，这导致了对[角动量量子数](@entry_id:172069)变化的严格限制。综合宇称和角动量两个方面的要求，我们得到单[光子](@entry_id:145192)[电偶极跃迁](@entry_id:149662)的完整选择定则：
-   **[轨道角动量](@entry_id:191303)变化**：$\Delta l = l_f - l_i = \pm 1$。$\Delta l=0$ 的跃迁因不改变宇称而被禁戒。
-   **[磁量子数](@entry_id:145584)变化**：$\Delta m = m_f - m_i = 0, \pm 1$。$\Delta m=0$ 对应[线偏振光](@entry_id:165445)，$\Delta m=\pm 1$ 对应[圆偏振光](@entry_id:198374)。

任何不满足这些规则的[原子跃迁](@entry_id:158267)（如 $s \to s$ 或 $s \to d$ 跃迁）都是[电偶极禁戒](@entry_id:180237)的，其振子强度为零。

#### [自旋选择定则](@entry_id:146964)

在不考虑相对论效应的非[相对论哈密顿量](@entry_id:176823)中，体系的总[自旋算符](@entry_id:155419) $S^2$ 与[哈密顿量](@entry_id:172864)和[电偶极矩](@entry_id:178520)算符 $\hat{\boldsymbol{\mu}}$ 都是对易的（$[H_0, S^2]=0$, $[\hat{\boldsymbol{\mu}}, S^2]=0$）。这意味着体系的本征态可以被标记为具有确定的总[自旋[量子](@entry_id:142550)数](@entry_id:145558) $S$，例如[单重态](@entry_id:154728) ($S=0$) 或[三重态](@entry_id:156705) ($S=1$)。

由于 $\hat{\boldsymbol{\mu}}$ 是一个纯粹的空间坐标算符，它不作用于电子的自旋坐标。因此，在计算跃迁偶极矩时，自旋部分和空间部分可以分离 [@problem_id:2889031]：
$$
\boldsymbol{\mu}_{if} = \langle \Phi_f | \hat{\boldsymbol{\mu}}_e | \Phi_i \rangle_{\text{spatial}} \langle \chi_{S_f, M_f} | \chi_{S_i, M_i} \rangle_{\text{spin}}
$$
不同总自旋 $S$ 的[自旋波函数](@entry_id:190161)是正交的，即 $\langle \chi_{S_f, M_f} | \chi_{S_i, M_i} \rangle = \delta_{S_f S_i} \delta_{M_f M_i}$。因此，如果初末态的自旋量子数不同 ($S_f \neq S_i$)，自旋积分部分为零，导致整个跃迁偶极矩为零。这就引出了**[自旋选择定则](@entry_id:146964)**：
$$
\Delta S = S_f - S_i = 0
$$
例如，从[单重态](@entry_id:154728)[基态](@entry_id:150928)到三重态[激发态](@entry_id:261453)的跃迁（$S=0 \to S=1$）是自旋禁戒的，其振子强度理论上为零。这类跃迁被称为**[系间窜越](@entry_id:139758) (intersystem crossing)**。

然而，在现实中，许多名义上“禁戒”的跃迁仍然可以被微弱地观测到，例如[磷光](@entry_id:155173)现象就源于自旋禁戒的[三重态](@entry_id:156705)-单重态跃迁。这是因为存在一些被我们忽略了的次级效应，它们可以打破严格的[选择定则](@entry_id:140784)。对于自旋禁戒，最重要的机制是**[自旋-轨道耦合](@entry_id:143520) (spin-orbit coupling, SOC)**。这是一个相对论效应，它耦合了电子的自旋角动量和[轨道角动量](@entry_id:191303)。当包含[自旋-轨道耦合](@entry_id:143520)[哈密顿量](@entry_id:172864) $H_{\mathrm{SO}}$后，总[哈密顿量](@entry_id:172864) $H = H_0 + H_{\mathrm{SO}}$ 不再与 $S^2$ 对易。结果是，体系的真实本征态不再是纯粹的单重态或[三重态](@entry_id:156705)，而是两者的混合。

例如，一个名义上的三重态 $|T_1\rangle$ 会因为SOC而混入微量的单重态成分：$|\Psi'_{T_1}\rangle \approx |T_1\rangle + c|S_k\rangle$，其中 $c$ 是一个小的混合系数。因此，从单重态[基态](@entry_id:150928) $|S_0\rangle$ 到这个“污染”了的[三重态](@entry_id:156705) $|\Psi'_{T_1}\rangle$ 的跃迁偶极矩将不再是零，而是近似正比于混合系数 $c$：
$$
\boldsymbol{\mu}_{S_0 \to T'_1} = \langle S_0 | \hat{\boldsymbol{\mu}} | \Psi'_{T_1} \rangle \approx c \langle S_0 | \hat{\boldsymbol{\mu}} | S_k \rangle
$$
这个过程通常被称为**强度借贷 (intensity borrowing)**，即自旋禁戒的跃迁从一个能量相近的自旋允许的跃迁（$S_0 \to S_k$）那里“借来”了强度。由于混合系数 $c$ 通常很小，振子强度（正比于 $|\boldsymbol{\mu}|^2 \propto c^2$）会非常弱，比自旋允许的跃迁要弱上好几个[数量级](@entry_id:264888) [@problem_id:2889031]。

### 激发的分类与计算

#### 价层激发与里德堡激发

在分子中，电子激发通常被分为两大类：**价层激发 (valence excitations)** 和 **里德堡激发 (Rydberg excitations)**。区分它们对于理解和诠释[光谱](@entry_id:185632)至关重要。

-   **价层激发**：涉及电子从一个被占据的价层[轨道](@entry_id:137151)跃迁到一个未被占据的价层[轨道](@entry_id:137151)（如 $\pi \to \pi^*$ 或 $n \to \pi^*$ 跃迁）。这些[轨道](@entry_id:137151)在空间上相对紧凑，局限在分子骨架的范围内。
-   **里德堡激发**：涉及电子被激发到一个空间上非常弥散的[轨道](@entry_id:137151)，远离分子离子实（molecular ion core）。这些**里德堡[轨道](@entry_id:137151)**类似于氢原子中[主量子数](@entry_id:143678) $n$ 较大的[轨道](@entry_id:137151)。里德堡态的能量可以用[类氢原子](@entry_id:164890)公式描述：$E_n = I_{\mathrm{vert}} - \frac{R_H}{(n-\delta)^2}$，其中 $I_{\mathrm{vert}}$ 是分子的[电离能](@entry_id:136678)，$n$ 是主量子数，$\delta$ 是[量子亏损](@entry_id:269980)。它们形成一个收敛于电离极限的序列。

在[量子化学](@entry_id:140193)计算中，区分这两种激发类型的一个有效方法是考察计算结果对[基组](@entry_id:160309)中**弥散函数 (diffuse functions)** 的依赖性 [@problem_id:2889016]。弥散函数是空间范围很大的[基函数](@entry_id:170178)，对于准确描述里德堡[轨道](@entry_id:137151)的长程行为至关重要。

考虑一个假设的计算案例，我们使用不含弥散函数的[基组](@entry_id:160309) ([cc-pVTZ](@entry_id:176016)) 和添加了弥散函数的[基组](@entry_id:160309) ([aug-cc-pVTZ](@entry_id:274779)) 计算了某分子的四个[激发态](@entry_id:261453)，其[垂直电离能](@entry_id:171391)为 $10.60\,\mathrm{eV}$：

-   **T1**: $E_{\mathrm{aug}} = 6.85\,\mathrm{eV}$ (从 $6.90\,\mathrm{eV}$ 下降 $0.05\,\mathrm{eV}$), $f_{\mathrm{aug}} = 0.21$。
-   **T2**: $E_{\mathrm{aug}} = 8.10\,\mathrm{eV}$ (从 $9.20\,\mathrm{eV}$ 下降 $1.10\,\mathrm{eV}$), $f_{\mathrm{aug}} = 0.045$。
-   **T3**: $E_{\mathrm{aug}} = 8.56\,\mathrm{eV}$ (从 $8.60\,\mathrm{eV}$ 下降 $0.04\,\mathrm{eV}$), $f_{\mathrm{aug}} = 0.29$。
-   **T4**: $E_{\mathrm{aug}} = 8.98\,\mathrm{eV}$ (从 $9.00\,\mathrm{eV}$ 下降 $0.02\,\mathrm{eV}$), $f_{\mathrm{aug}} = 0.0007$。

我们可以进行如下分析：
-   T1, T3 和 T4 的能量在加入弥散函数后几乎不变，表明它们的[波函数](@entry_id:147440)是紧凑的，这是**价层激发**的典型特征。T1 和 T3 具有很大的[振子强度](@entry_id:147221)，是“亮的”价层激发；而 T4 的[振子强度](@entry_id:147221)极小，是“暗的”价层激发。
-   T2 的能量在加入弥散函数后显著下降了 $1.10\,\mathrm{eV}$，这是**里德堡激发**的明确标志，说明不含[弥散函数](@entry_id:267705)的[基组](@entry_id:160309)无法正确描述其弥散的末态[轨道](@entry_id:137151)。其能量 $8.10\,\mathrm{eV}$ 相对接近[电离能](@entry_id:136678) $10.60\,\mathrm{eV}$，且振子强度适中，这些都与里德堡态的特征相符。

#### [激发态](@entry_id:261453)的计算方法

为了从理论上获得[激发能](@entry_id:190368)和振子强度，我们需要求解多电子体系的[激发态](@entry_id:261453)。现代[量子化学](@entry_id:140193)提供了多种方法，如**[含时密度泛函理论 (TD-DFT)](@entry_id:192176)** 和**[运动方程耦合簇](@entry_id:185022) ([EOM-CC](@entry_id:266204))** 等。这些方法的核心都是在某种近似下求解[激发态](@entry_id:261453)[波函数](@entry_id:147440)和能量。

一个更普遍的描述跃迁性质的方式是使用**单粒子跃迁密度矩阵 (one-particle transition density matrix, 1-TDM)** [@problem_id:2889000]。在[二次量子化](@entry_id:137766)的语言中，从态 $|0\rangle$ 到 $|n\rangle$ 的 1-TDM 定义为：
$$
\gamma_{pq}^{(0n)} \equiv \langle 0 | \hat{a}_q^\dagger \hat{a}_p | n \rangle
$$
其中 $\hat{a}_p^\dagger$ 和 $\hat{a}_p$ 是在某个单粒[子基](@entry_id:151637)（如分子[轨道](@entry_id:137151)）上的产生和湮灭算符。这个矩阵包含了从态 $|0\rangle$ 跃迁到 $|n\rangle$ 时电子“重新排布”的全部信息。任何[单电子算符](@entry_id:191980)（如偶极矩算符）的跃迁[矩阵元](@entry_id:186505)都可以通过 1-TDM 计算得到。对于跃迁偶极矩，其关系为：
$$
\mu_{\alpha}^{0n} = \sum_{pq} \gamma_{pq}^{(0n)} \langle \phi_q | \hat{r}_{\alpha} | \phi_p \rangle
$$
其中 $\langle \phi_q | \hat{r}_{\alpha} | \phi_p \rangle$ 是在单粒子[基函数](@entry_id:170178)下的偶极矩积分。这个表达式将多电子的跃迁问题转化为了单粒子算符矩阵与描述多[电子跃迁](@entry_id:152949)的[密度矩阵](@entry_id:139892)的缩并，是分析电子激发特性的有力工具。1-TDM 的一个重要性质是其迹为零（$\mathrm{Tr}\,\gamma^{(0n)} = 0$），这反映了跃迁过程中粒子数守恒以及初末态的正交性。

作为一个具体的例子，我们来看最简单的[激发态方法](@entry_id:190102)之一：**[单激发组态相互作用](@entry_id:174866) (Configuration Interaction Singles, CIS)** [@problem_id:2889054]。在CIS中，[激发态](@entry_id:261453) $|n\rangle$ 被近似为[基态](@entry_id:150928)（通常是[Hartree-Fock](@entry_id:142303)[参考态](@entry_id:151465) $|0\rangle$）所有可能的单激发的[线性组合](@entry_id:154743)：
$$
|n\rangle = \sum_{i,a} c_{ai}^{(n)} |\Psi_i^a\rangle
$$
其中 $|\Psi_i^a\rangle$ 表示电子从占据[轨道](@entry_id:137151) $i$ 跃迁到空[轨道](@entry_id:137151) $a$ 的组态，$c_{ai}^{(n)}$ 是通过[对角化](@entry_id:147016)CIS[哈密顿矩阵](@entry_id:136233)得到的组合系数。对于一个封闭壳层体系的单重态激发，其跃迁偶极矩可以推导为：
$$
\boldsymbol{\mu}_{0n} = \sqrt{2} \sum_{i,a} c_{ai}^{(n)} \boldsymbol{\mu}_{ia}
$$
其中 $\boldsymbol{\mu}_{ia} = \langle \varphi_i | \hat{\boldsymbol{\mu}}_e | \varphi_a \rangle$ 是分子[轨道](@entry_id:137151)之间的偶极矩积分。这个公式清晰地展示了多电子的跃迁偶极矩是如何由各个单粒子[轨道](@entry_id:137151)跃迁（$i \to a$）的贡献加权（由 $c_{ai}^{(n)}$ 系数）求和得到的。这里的 $\sqrt{2}$ 因子源于对单重态自旋适配函数的正确归一化。