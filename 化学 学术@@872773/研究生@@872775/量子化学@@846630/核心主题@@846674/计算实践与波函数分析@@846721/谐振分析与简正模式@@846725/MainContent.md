## 引言
分子世界充满了永不停歇的运动，其中[振动](@entry_id:267781)是其最基本的表现形式之一，深刻影响着分子的结构、稳定性、[光谱](@entry_id:185632)特性及化学反应性。然而，一个[多原子分子的振动](@entry_id:198539)是所有原子协同运动的复杂舞蹈，如何从理论上精确地描述并解析这些运动，是[量子化学](@entry_id:140193)面临的核心挑战。[谐振分析](@entry_id:199012)与正交模理论正是为解决这一问题而生的强大框架，它通过一个优雅的数学近似，将看似混沌的原子[核[集体运](@entry_id:752691)动](@entry_id:747472)分解为一组简单、独立且具有明确物理图像的“基本[振动](@entry_id:267781)”。

本文旨在系统性地介绍[谐振分析](@entry_id:199012)的原理及其在现代化学研究中的广泛应用。我们将从第一性原理出发，逐步揭示这一理论的内在逻辑与强大功能。
在接下来的“原理与机制”一章中，我们将建立[势能面](@entry_id:147441)的概念，并详细推导如何从谐振近似过渡到求解正交模。我们将探讨频率的物理意义，特别是如何利用[虚频](@entry_id:165180)来识别[化学反应](@entry_id:146973)的过渡态。
随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示[谐振分析](@entry_id:199012)如何成为连接理论与实验的桥梁，内容涵盖[光谱学](@entry_id:141940)（红外、拉曼、[振动](@entry_id:267781)-[电子光谱](@entry_id:154403)）、[热化学](@entry_id:137688)（[零点能](@entry_id:142176)、熵）以及[反应动力学](@entry_id:150220)（过渡态理论、[同位素效应](@entry_id:164159)）。我们还将探讨该理论如何扩展到生物大分子和晶体材料等复杂体系。
最后，在“动手实践”部分，我们提供了一系列计算练习，旨在帮助读者将理论知识转化为解决实际问题的能力。

通过这三个层次的深入探讨，读者将不仅掌握[谐振分析](@entry_id:199012)的计算方法，更能深刻理解其在揭示微观世界规律中的核心作用。

## 原理与机制

在上一章中，我们介绍了[分子振动](@entry_id:140827)的基本概念。本章将深入探讨[量子化学](@entry_id:140193)中用于分析这些[振动](@entry_id:267781)的核心理论框架——[谐振分析](@entry_id:199012)。我们将从第一性原理出发，构建[势能面](@entry_id:147441)（Potential Energy Surface, PES）的概念，并推导谐振近似，最终引出正交模（normal modes）的概念。此外，我们还将探讨如何利用这些正交模来解释红外与拉曼[光谱](@entry_id:185632)，并讨论谐振模型的局限性及其修正方法。

### [势能面](@entry_id:147441)与谐振近似

分子振动理论的基石是 **玻恩–奥本海默（Born–Oppenheimer, BO）近似**。该近似允许我们将电子运动与[原子核](@entry_id:167902)运动分离开来。由于电子的质量远小于[原子核](@entry_id:167902)，我们可以假定电子能够瞬时地适应[原子核](@entry_id:167902)位置的变化。因此，对于一个给定的[原子核](@entry_id:167902)构型 $\mathbf{R}$，我们可以求解[电子薛定谔方程](@entry_id:177999)，得到一个电子能量 $E_k(\mathbf{R})$ 和对应的电子[波函数](@entry_id:147440) $\phi_k(\mathbf{r};\mathbf{R})$。这个随[原子核](@entry_id:167902)构型变化的电子能量 $E_k(\mathbf{R})$ 便构成了第 $k$ 个电子态的 **[势能面](@entry_id:147441)（Potential Energy Surface, PES）**。[原子核](@entry_id:167902)的运动，如[振动](@entry_id:267781)和转动，便可视为在这样一个固定的[势能面](@entry_id:147441)上进行 [@problem_id:2895033]。

将总[波函数](@entry_id:147440)在电子[绝热态](@entry_id:265086)[基矢](@entry_id:199546)上展开，可以得到一组关于[原子核](@entry_id:167902)[波函数](@entry_id:147440)的耦合方程。当所研究的电子态（例如，[基态](@entry_id:150928) $k=0$）与其他电子态的能量差 $\Delta E_{k0}(\mathbf{R})$ 远大于[原子核](@entry_id:167902)的特征动能时，我们可以忽略不同[势能面](@entry_id:147441)之间的[非绝热耦合](@entry_id:198018)项。这便是 **[绝热近似](@entry_id:143074)（adiabatic approximation）**。在此近似下，[原子核](@entry_id:167902)的动力学行为被限制在单一的[势能面](@entry_id:147441)上。然而，值得注意的是，当不同[势能面](@entry_id:147441)彼此靠近甚至相交（例如在 **[锥形交叉点](@entry_id:202598)** 处），[绝热近似](@entry_id:143074)会失效，此时单一[势能面](@entry_id:147441)的图像不再成立 [@problem_id:2894916]。

在一个给定的[势能面](@entry_id:147441)上，化学中最受关注的构型是 **[稳定点](@entry_id:136617)（stationary points）**，即[势能面](@entry_id:147441)对[原子核](@entry_id:167902)坐标的一阶导数（梯度）为零的点：$\nabla V(\mathbf{R}) = \mathbf{0}$。这些点对应于分子的平衡结构（[势能极小点](@entry_id:159163)）或[化学反应](@entry_id:146973)的过渡态（[一阶鞍点](@entry_id:165164)）。为了研究分子在平衡结构 $\mathbf{R}_0$ 附近的[振动](@entry_id:267781)，我们将[势能面](@entry_id:147441) $V(\mathbf{R})$ 在 $\mathbf{R}_0$ 附近进行[泰勒展开](@entry_id:145057)。令位移向量为 $\Delta\mathbf{R} = \mathbf{R} - \mathbf{R}_0$，则有：

$$
V(\mathbf{R}) = V(\mathbf{R}_0) + \left. \nabla V \right|_{\mathbf{R}_0} \cdot \Delta\mathbf{R} + \frac{1}{2} \Delta\mathbf{R}^{\mathsf{T}} \cdot \mathbf{H} \cdot \Delta\mathbf{R} + \mathcal{O}(\Delta R^3)
$$

由于我们在[稳定点](@entry_id:136617)进行展开，梯度项（线性项）$\nabla V |_{\mathbf{R}_0}$ 精确为零。如果我们将能量零点设在[平衡点](@entry_id:272705)处，即 $V(\mathbf{R}_0) = 0$，并忽略三阶及更高阶的项，[势能](@entry_id:748988)就简化为一个二次型。这便是 **谐振近似（harmonic approximation）** [@problem_id:2895007]。

$$
V_{\text{harm}}(\Delta\mathbf{R}) \approx \frac{1}{2} \Delta\mathbf{R}^{\mathsf{T}} \mathbf{H} \Delta\mathbf{R}
$$

其中的矩阵 $\mathbf{H}$ 是[势能面](@entry_id:147441)对[原子核](@entry_id:167902)笛卡尔坐标的[二阶导数](@entry_id:144508)矩阵，在[平衡点](@entry_id:272705) $\mathbf{R}_0$ 处求值得到，称为 **赫森矩阵（Hessian matrix）**：

$$
H_{ij} = \left. \frac{\partial^2 V}{\partial R_i \partial R_j} \right|_{\mathbf{R}_0}
$$

谐振近似的物理意义是将复杂的分子[势能面](@entry_id:147441)局部地用一个多维[抛物面](@entry_id:264713)来替代。这个近似的有效性取决于[原子核](@entry_id:167902)的[振动](@entry_id:267781)幅度。从量子力学的角度看，当分子的零点[振动](@entry_id:267781)及低[激发态](@entry_id:261453)[振动](@entry_id:267781)[波函数](@entry_id:147440)主要[分布](@entry_id:182848)在[势能面](@entry_id:147441)近似为抛物线的盆地区域时，谐振近似才是可靠的。对于那些[振动频率](@entry_id:199185)很低、[势能面](@entry_id:147441)非常平缓的“柔性”模式（如弱氢[键伸缩](@entry_id:172690)或大基团的内部扭转），其[波函数](@entry_id:147440)会扩展到非谐性（anharmonicity）显著的区域，导致谐振近似失效 [@problem_id:2894916]。

### 正交模分析：[解耦](@entry_id:637294)[振动](@entry_id:267781)

在谐振近似下，[原子核](@entry_id:167902)的运动方程由[牛顿第二定律](@entry_id:274217)给出。对于 $3N$ 个[笛卡尔坐标](@entry_id:167698)（$N$为[原子数](@entry_id:746561)），其矩阵形式为：

$$
\mathbf{M} \ddot{\mathbf{x}}(t) = -\mathbf{H} \mathbf{x}(t)
$$

其中 $\mathbf{x}$ 是位移向量（即上文的 $\Delta\mathbf{R}$），$\mathbf{M}$ 是一个对角矩阵，其对角线元素为各个[原子核](@entry_id:167902)的质量。这是一个耦合的[常微分方程组](@entry_id:266774)，因为赫森矩阵 $\mathbf{H}$ 通常不是[对角矩阵](@entry_id:637782)，一个原子的运动会通过[势能](@entry_id:748988)影响其他原子。为了[解耦](@entry_id:637294)这套方程，我们引入 **[质量加权坐标](@entry_id:164904)（mass-weighted coordinates）** [@problem_id:2895023]。

定义[质量加权坐标](@entry_id:164904)向量 $\mathbf{q}$ 为：

$$
q_i = \sqrt{m_i} x_i \quad \text{或} \quad \mathbf{q} = \mathbf{M}^{1/2} \mathbf{x}
$$

通过这个变换，[原子核](@entry_id:167902)的动能 $T = \frac{1}{2}\dot{\mathbf{x}}^{\mathsf{T}}\mathbf{M}\dot{\mathbf{x}}$ 简化为 $T = \frac{1}{2}\dot{\mathbf{q}}^{\mathsf{T}}\dot{\mathbf{q}}$，其形式如同单位质量的质点。势能则变为：

$$
V = \frac{1}{2} \mathbf{x}^{\mathsf{T}} \mathbf{H} \mathbf{x} = \frac{1}{2} \mathbf{q}^{\mathsf{T}} (\mathbf{M}^{-1/2} \mathbf{H} \mathbf{M}^{-1/2}) \mathbf{q}
$$

我们定义 **质量加权赫森矩阵** $\mathbf{F} = \mathbf{M}^{-1/2} \mathbf{H} \mathbf{M}^{-1/2}$。$\mathbf{F}$ 是一个[实对称矩阵](@entry_id:192806)。[运动方程](@entry_id:170720)在[质量加权坐标](@entry_id:164904)下变为一个标准的[特征值问题](@entry_id:142153)形式：

$$
\ddot{\mathbf{q}}(t) + \mathbf{F} \mathbf{q}(t) = \mathbf{0}
$$

寻找[简谐运动](@entry_id:148744)解 $\mathbf{q}(t) = \mathbf{l} \exp(i\omega t)$，我们得到[特征方程](@entry_id:265849)：

$$
\mathbf{F} \mathbf{l} = \omega^2 \mathbf{l}
$$

对[实对称矩阵](@entry_id:192806) $\mathbf{F}$进行[对角化](@entry_id:147016)，可以得到一组[本征值](@entry_id:154894) $\lambda_k = \omega_k^2$ 和对应的正交归一的[本征向量](@entry_id:151813) $\mathbf{l}_k$。这些[本征向量](@entry_id:151813)定义了一组新的坐标，称为 **正交模坐标（normal coordinates）** $Q_k$，它们是[质量加权坐标](@entry_id:164904)的[线性组合](@entry_id:154743)。在正交模坐标下，系统的[哈密顿量](@entry_id:172864)被完全解耦，变成了一系列独立的、互不干扰的一维[谐振子](@entry_id:155622)的总和。每个独立的[谐振子](@entry_id:155622)就称为一个 **正交模（normal mode）**，其[角频率](@entry_id:261565)为 $\omega_k = \sqrt{\lambda_k}$ [@problem_id:2895023]。

举一个简单的例子，考虑一个仅沿直线运动的一维双原子分子，两原子质量均为 $m$，位移分别为 $x_1$ 和 $x_2$。假设[势能](@entry_id:748988)仅依赖于键长变化 $s = x_1 - x_2$，且 $V = \frac{1}{2} k s^2 = \frac{1}{2} k (x_1 - x_2)^2$。展开后可得笛卡尔坐标下的赫森矩阵为 [@problem_id:2895007]：

$$
\mathbf{H} = \begin{pmatrix} k & -k \\ -k & k \end{pmatrix}
$$

质量加权赫森矩阵为 $\mathbf{F} = \frac{1}{m}\mathbf{H}$。其[本征值](@entry_id:154894)之一对应于反对称模式（伸缩[振动](@entry_id:267781)），其[本征值](@entry_id:154894)为 $\lambda = \frac{2k}{m}$，因此该[振动](@entry_id:267781)模式的角频率的平方为 $\omega^2 = \frac{2k}{m}$。

### [振动频率](@entry_id:199185)与模式的诠释

通过对质量加权赫森矩阵的对角化，我们得到了一组频率和对应的[振动](@entry_id:267781)模式。这些结果的物理意义与[势能面](@entry_id:147441)的拓扑结构密切相关。

#### 稳定最小值与内外运动分离

对于一个处于[势能面](@entry_id:147441) **稳定最小值** 的分子，任何微小的[振动](@entry_id:267781)位移都会导致能量上升。这意味着质量加权赫森矩阵 $\mathbf{F}$ 在[振动](@entry_id:267781)[子空间](@entry_id:150286)内是正定的，其所有[振动](@entry_id:267781)相关的[本征值](@entry_id:154894) $\lambda_k$ 都必须是正数，从而得到实的[振动频率](@entry_id:199185) $\omega_k$。

然而，对于一个孤立的分子（$N \ge 2$），其[势能](@entry_id:748988)不随整体的平移和转动而改变。这导致赫森矩阵必然存在零[本征值](@entry_id:154894)。对于一个[非线性分子](@entry_id:175085)，存在3个平移自由度和3个[转动自由度](@entry_id:141502)，共对应6个零频率模式。对于线性分子，则有3个平移和2个[转动自由度](@entry_id:141502)，共5个零频率模式。剩下的 $3N-6$（[非线性](@entry_id:637147)）或 $3N-5$（线性）个具有正[本征值](@entry_id:154894)（实频率）的模式，才是真正的 **内禀[振动](@entry_id:267781)模式** [@problem_id:2894916]。

在数值计算中，由于[几何优化](@entry_id:151817)和赫森矩阵计算的微小误差，这些外部模式的频率通常不会精确为零，而是表现为很小的正值或负值。这会与真实的低频[振动](@entry_id:267781)模式混淆，造成困扰。一个严谨的处理方法是在对角化之前，通过 **[投影法](@entry_id:144836)** 将平移和转动分量从赫森矩阵中移除。具体做法是：首先在[质量加权坐标](@entry_id:164904)空间中构建对应于平移和转动的6个（或5个）[基向量](@entry_id:199546)，将它们正交化后构成一个矩阵 $\mathbf{B}$，然后构造[投影算符](@entry_id:154142) $\mathbf{P} = \mathbf{I} - \mathbf{B}\mathbf{B}^{\mathsf{T}}$，该算符能将任意[向量投影](@entry_id:147046)到与外部运动正交的内部（[振动](@entry_id:267781)）[子空间](@entry_id:150286)。最后，对投影后的质量加权赫森矩阵 $\tilde{\mathbf{F}} = \mathbf{P}\mathbf{F}\mathbf{P}$ 进行对角化，即可得到纯净的[振动频率](@entry_id:199185)和模式 [@problem_id:2894964]。

#### 过渡态与[虚频](@entry_id:165180)

[谐振分析](@entry_id:199012)不仅能描述稳定分子，更是鉴定 **过渡态（transition state）** 的有力工具。根据过渡态理论，[化学反应](@entry_id:146973)的过渡态对应于[势能面](@entry_id:147441)上的 **[一阶鞍点](@entry_id:165164)**。它在一个方向（[反应坐标](@entry_id:156248)）上是能量的极大值，而在所有其他与之正交的方向上是能量的极小值。

这个独特的拓扑结构在[谐振分析](@entry_id:199012)中有明确的标志。在排除了平移和转动后，过渡态的赫森矩阵恰好有 **一个负[本征值](@entry_id:154894)**。这个负[本征值](@entry_id:154894) $\lambda_k < 0$ 意味着沿该方向的[势能面](@entry_id:147441)是向下弯曲的。对应的“频率”为 $\omega_k = \sqrt{\lambda_k} = i\sqrt{|\lambda_k|}$，是一个纯 **虚数**。这个 **虚频（imaginary frequency）** 标志着结构的不稳定性，对应的正交模描绘了原子如何协同运动以越过能垒，从反应物走向产物，因此它正是 **[反应坐标](@entry_id:156248)** 的体现 [@problem_id:2894937]。赫森矩阵的负[本征值](@entry_id:154894)数量被称为 **赫森指数**。一个真正的过渡态，其赫森指数必须为1 [@problem_id:2894916]。

###[光谱学](@entry_id:141940)应用：红外与[拉曼活性](@entry_id:264824)

[谐振分析](@entry_id:199012)最重要的应用之一是预测和解释分子的振动光谱。

#### 红外（IR）[光谱](@entry_id:185632)

红外[光谱](@entry_id:185632)源于分子振动能级跃迁时与红外[光子](@entry_id:145192)的相互作用。在[电偶极近似](@entry_id:150449)下，该相互作用由[哈密顿量](@entry_id:172864) $H' = -\boldsymbol{\mu} \cdot \mathbf{E}$ 描述，其中 $\boldsymbol{\mu}$ 是分子的[电偶极矩](@entry_id:178520)算符，$\mathbf{E}$ 是光的[电场](@entry_id:194326)。根据[费米黄金定则](@entry_id:146239)，从初态 $|i\rangle$ 到末态 $|f\rangle$ 的跃迁速率正比于跃迁偶极矩的平方 $| \langle f | \boldsymbol{\mu} | i \rangle |^2$。

对于基频跃迁（$v_k: 0 \to 1$），我们需要计算 $\langle 1_k | \boldsymbol{\mu} | 0_k \rangle$。我们将[分子偶极矩](@entry_id:152656) $\boldsymbol{\mu}$ 按正交模坐标 $Q_k$ 进行[泰勒展开](@entry_id:145057)：

$$
\boldsymbol{\mu}(\{Q_k\}) = \boldsymbol{\mu}_0 + \sum_k \left( \frac{\partial \boldsymbol{\mu}}{\partial Q_k} \right)_0 Q_k + \dots
$$

其中 $\boldsymbol{\mu}_0$ 是平衡构型下的[永久偶极矩](@entry_id:163961)。由于谐振子波[函数的正交性](@entry_id:160337)，$\langle 1_k | \boldsymbol{\mu}_0 | 0_k \rangle = 0$。因此，跃迁是否发生取决于线性项。跃迁偶极矩近似为：

$$
\langle 1_k | \boldsymbol{\mu} | 0_k \rangle \approx \left( \frac{\partial \boldsymbol{\mu}}{\partial Q_k} \right)_0 \langle 1_k | Q_k | 0_k \rangle
$$

$\langle 1_k | Q_k | 0_k \rangle$ 是一个非零常数。因此，我们得到了红外[光谱](@entry_id:185632)的 **[选择定则](@entry_id:140784)**：一个[振动](@entry_id:267781)模式是 **[红外活性](@entry_id:267987)的（IR active）**，当且仅当该振动能够引起[分子偶极矩](@entry_id:152656)的改变，即偶极矩对该正交模坐标的导数不为零，$\left| (\partial \boldsymbol{\mu}/\partial Q_k)_0 \right|^2 \neq 0$ [@problem_id:2894883]。对于气体或液体等各向同性样品，由于分子的随机取向，测得的吸收强度需要对所有空间取向进行平均，这会引入一个 $1/3$ 的因子 [@problem_id:2894883]。

#### 拉曼（Raman）[光谱](@entry_id:185632)

拉曼[光谱](@entry_id:185632)是一种散射[光谱](@entry_id:185632)。当[光子](@entry_id:145192)与[分子相互作用](@entry_id:263767)时，分子[电场](@entry_id:194326)会诱导出一个偶极矩 $\boldsymbol{\mu}_{\text{ind}} = \boldsymbol{\alpha} \mathbf{E}$，其中 $\boldsymbol{\alpha}$ 是分子的 **[极化率张量](@entry_id:191938)**。这个[诱导偶极矩](@entry_id:262417)会辐射出[电磁波](@entry_id:269629)，即发生散射。

由于分子在[振动](@entry_id:267781)，其极化率 $\boldsymbol{\alpha}$ 也随[原子核](@entry_id:167902)构型（即正交模坐标 $Q_k$）变化。我们将 $\boldsymbol{\alpha}$ 也在[平衡点](@entry_id:272705)附近展开：

$$
\boldsymbol{\alpha}(Q_k) \approx \boldsymbol{\alpha}_0 + \left(\frac{\partial \boldsymbol{\alpha}}{\partial Q_k}\right)_0 Q_k(t) + \dots
$$

其中 $Q_k(t) = Q_{k,0} \cos(\omega_k t)$ 描述了频率为 $\omega_k$ 的[分子振动](@entry_id:140827)，而入射光[电场](@entry_id:194326)为 $\mathbf{E}(t) = \mathbf{E}_0 \cos(\omega_0 t)$。代入[诱导偶极矩](@entry_id:262417)表达式后，利用[三角函数](@entry_id:178918)积化和差公式，我们发现[诱导偶极矩](@entry_id:262417)的振荡频率包含了三部分：[瑞利散射](@entry_id:178255)（$\omega_0$）、[斯托克斯散射](@entry_id:159214)（$\omega_0 - \omega_k$）和[反斯托克斯散射](@entry_id:271867)（$\omega_0 + \omega_k$）。后两者即为拉曼散射信号。

拉曼散射的强度取决于频率为 $\omega_0 \pm \omega_k$ 的[振荡](@entry_id:267781)项的幅度，而该幅度正比于极化率的导数 $(\partial \boldsymbol{\alpha}/\partial Q_k)_0$。因此，拉曼[光谱](@entry_id:185632)的 **选择定则** 是：一个[振动](@entry_id:267781)模式是 **拉曼活性的（Raman active）**，当且仅当该[振动能](@entry_id:157909)够引起[分子极化率](@entry_id:143365)的改变，即 $(\partial \boldsymbol{\alpha}/\partial Q_k)_0$ 至少有一个张量分量不为零 [@problem_id:2894894]。对于各向同性样品，拉曼散射强度与[极化率导数](@entry_id:183119)张量的两个[不变量](@entry_id:148850)，即平均[极化率导数](@entry_id:183119)的平方 $a_k^{\prime\,2}$ 和[各向异性极化率](@entry_id:168660)导数的平方 $\gamma_k^{\prime\,2}$，有关：$S_k \propto 45 a_k^{\prime\,2} + 7 \gamma_k^{\prime\,2}$ [@problem_id:2894894]。

### 超越谐振近似

谐振模型功能强大，但终究是一个近似。真实的分子[势能面](@entry_id:147441)不是完美的[抛物面](@entry_id:264713)，这种偏离称为 **[非谐性](@entry_id:137191)（anharmonicity）**。

#### 非谐性修正

在[势能面](@entry_id:147441)的泰勒展开中，被我们忽略的三阶（立方）和四阶（四次）[力常数](@entry_id:156420) $\Phi_{ijk}$ 和 $\Phi_{ijkl}$ 正是量化非谐性的关键。我们可以通过[微扰理论](@entry_id:138766)来评估它们的影响 [@problem_id:2894967]。
-   **立方项 $\Phi_{ijk}$**：它们在微扰理论的[一阶修正](@entry_id:155896)中不起作用（因为宇称禁戒），但在[二阶修正](@entry_id:199233)中起主导作用。它们描述了[势能面](@entry_id:147441)的不对称性，并导致了不同[振动](@entry_id:267781)模式之间的 **耦合**。当两个[振动能级](@entry_id:193001)（例如一个[基频](@entry_id:268182)和一个泛频或组合频）能量相近时，这种耦合会引起强烈的能量交换和能级推斥，即 **[费米共振](@entry_id:160855)（Fermi resonance）**。
-   **四次项 $\Phi_{ijkl}$**：它们在[一阶微扰理论](@entry_id:153242)中就会给出非零的[能量修正](@entry_id:198270)，直接改变了能级的间隔。它们描述了[势能面](@entry_id:147441)曲率随[振动](@entry_id:267781)振幅的变化。

对于典型的[化学键伸缩](@entry_id:172690)[振动](@entry_id:267781)（其[势能](@entry_id:748988)可用[Morse势](@entry_id:147996)描述），非谐性的总[体效应](@entry_id:261475)是使振动能级随着[量子数](@entry_id:145558)增加而变得更加密集。这意味着谐振近似计算出的[基频](@entry_id:268182)跃迁能量通常会 **系统性地高于** 实验观测值。因此，为了精确预测[振动频率](@entry_id:199185)，非谐性修正是不可或缺的 [@problem_id:2894967]。

#### 大振幅运动

[谐振分析](@entry_id:199012)的另一个根本限制在于它是一个 **局域** 和 **微振幅** 模型。对于某些分子内部的大幅度运动，例如绕[单键](@entry_id:188561)的内部转动（扭转），谐振模型会彻底失效。原因在于：
1.  **[势能](@entry_id:748988)形式错误**：内部转动的[势能](@entry_id:748988)是关于扭转角 $\phi$ 的周期函数（例如 $V(\phi) \approx \sum_n V_n \cos(n\phi)$），具有多个[势阱](@entry_id:151413)和势垒，而谐振模型只用一个抛物线[势阱](@entry_id:151413)来描述。
2.  **坐标性质不符**：正交模是基于笛卡尔坐标的[线性组合](@entry_id:154743)，描述的是直线往复运动。而内部转动是天然的 **曲线运动**，其坐标是角度。

当转动能垒较低，与热能 $k_B T$ 或低位[振动能级](@entry_id:193001)相当时，分子可以发生大幅度扭转甚至近乎自由的转动。此时，必须放弃谐振模型，采用专门的处理方法。一种标准做法是 **一维受阻转[子模](@entry_id:148922)型**：
首先，通过[量子化学](@entry_id:140193)计算，沿着扭转角 $\phi$ 进行“ relaxed scan ”（即在每个固定的 $\phi$ 值下优化其他所有几何参数），得到一维的周期性势能函数 $V(\phi)$。然后，计算出该转动对应的有效转动惯量 $I(\phi)$（通常近似为一个常数）。最后，求解包含该势能和转动惯量的一维薛定谔方程，并施加[周期性边界条件](@entry_id:147809) $\psi(\phi+2\pi) = \psi(\phi)$：

$$
-\frac{\hbar^2}{2} \frac{d}{d\phi} \left( \frac{1}{I(\phi)} \frac{d}{d\phi} \psi(\phi) \right) + V(\phi)\psi(\phi) = E\psi(\phi)
$$

解出的能级可用于精确[计算热力学](@entry_id:148023)函数（如[配分函数](@entry_id:193625)和熵）以及[光谱](@entry_id:185632)。这种方法能够正确地描述跨越能垒的运动和[量子隧穿效应](@entry_id:149523)，这是[谐振分析](@entry_id:199012)完全无法做到的 [@problem_id:2894974]。