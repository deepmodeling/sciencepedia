## 引言

在探索晶体材料的微观[世界时](@entry_id:275204)，其原子结构固有的周期性既是其独特物理性质的根源，也对理论分析提出了独特的挑战。要精确描述电子在[晶格](@entry_id:148274)中的运动、[晶格](@entry_id:148274)自身的振动（声子），或是外部探针（如X射线）与晶体的相互作用，仅仅依赖我们所熟悉的[实空间](@entry_id:754128)是远远不够的。为了应对这一挑战，物理学家和材料科学家发展出了一套强大而优美的数学工具——**倒易空间（Reciprocal Space）**及其核心区域**第一布里渊区（First Brillouin Zone）**。它们构成了整个固体物理学的基石，是将微观的量子力学与宏观的[材料性能](@entry_id:146723)联系起来的桥梁。

本文旨在系统性地梳理[倒易空间](@entry_id:754151)与[第一布里渊区](@entry_id:269110)的理论、应用与计算实践，填补从基础[晶体学](@entry_id:140656)到高级[量子理论](@entry_id:145435)之间的知识鸿沟。我们将从最基本的原理出发，逐步揭示为何倒易空间是描述晶体中“波”行为的自然舞台，以及[第一布里渊区](@entry_id:269110)如何成为容纳晶体所有电子态信息的最小“地图”。

读者将通过本文的学习，循序渐进地掌握以下核心内容。在 **“原理与机制”** 一章中，我们将建立[倒易晶格](@entry_id:136718)的数学定义，理解其作为实空间[晶格](@entry_id:148274)[傅里叶对偶](@entry_id:200473)的深刻含义，并阐明[布洛赫定理](@entry_id:137461)如何将电子[波函数](@entry_id:201714)与[倒易空间](@entry_id:754151)中的[波矢](@entry_id:178620) $\mathbf{k}$ 联系起来，最终定义出第一布里渊区这一关键分析区域。接下来，在 **“应用与跨学科联系”** 一章中，我们将展示这些理论概念如何在实践中大放异彩，从解读衍射图谱、表征半导体的[电子结构](@entry_id:145158)，到探索石墨烯和[拓扑绝缘体](@entry_id:137834)等前沿材料的新奇物性。最后，在 **“动手实践”** 部分，我们提供了一系列计算练习，引导读者亲手实现从实空间到倒易空间的转换，并应用能带反折叠等高级技术来分析计算模拟结果。

通过这一系列的学习，你将不再视倒易空间为抽象的数学构造，而是将其看作一个强大而直观的工具，用以洞察和设计[功能材料](@entry_id:194894)的未来。

## 原理与机制

在研究晶体材料的物理性质时，我们面临的核心挑战是处理其原子结构内在的周期性。无论是电子的运动、[晶格](@entry_id:148274)的振动，还是与外部探针（如X射线或中子）的相互作用，都受到这种平移对称性的深刻影响。为了构建一个能够有效描述这些现象的理论框架，我们必须从真实的三维空间（[实空间](@entry_id:754128)）过渡到一个与之对偶的数学空间——**倒易空间**（或称**倒空间**，Reciprocal Space）。本章将系统地阐述倒易空间和第一布里渊区的基本原理及其物理机制。

### [倒易晶格](@entry_id:136718)：[晶格](@entry_id:148274)的[傅里叶对偶](@entry_id:200473)

晶体中的许多物理量，如电子密度 $\rho(\mathbf{r})$ 或有效势 $V(\mathbf{r})$，都具有与[晶格](@entry_id:148274)完全相同的周期性。这意味着，对于任何[晶格矢量](@entry_id:161583) $\mathbf{R}$，这些函数都满足 $f(\mathbf{r} + \mathbf{R}) = f(\mathbf{r})$。处理[周期函数](@entry_id:139337)的自然数学工具是[傅里叶分析](@entry_id:137640)。一个在实空间中具有离散平移对称性的函数，其傅里叶变换将表现出一种独特的结构。

考虑一个一般的[晶格](@entry_id:148274)[周期函数](@entry_id:139337) $f(\mathbf{r})$。我们可以将其展开为傅里叶级数。由于该函数在[晶格](@entry_id:148274)上是周期的，因此展开所用的基函数也必须具有相同的周期性。满足这一要求的[平面波基](@entry_id:140187)函数形式为 $e^{i\mathbf{G}\cdot\mathbf{r}}$，其中向量 $\mathbf{G}$ 必须满足条件 $e^{i\mathbf{G}\cdot(\mathbf{r}+\mathbf{R})} = e^{i\mathbf{G}\cdot\mathbf{r}}$。这直接导出了一个关键条件：$e^{i\mathbf{G}\cdot\mathbf{R}} = 1$ 对于所有实空间[晶格矢量](@entry_id:161583) $\mathbf{R}$ 必须成立。

所有满足此条件的矢量 $\mathbf{G}$ 的集合构成了一个新的、离散的格点结构，我们称之为**[倒易晶格](@entry_id:136718)**（Reciprocal Lattice）。因此，任何[晶格](@entry_id:148274)[周期函数](@entry_id:139337)都可以写成如下的[傅里叶级数](@entry_id:139455)：

$$
f(\mathbf{r}) = \sum_{\mathbf{G}} f_{\mathbf{G}} e^{i\mathbf{G}\cdot\mathbf{r}}
$$

其中 $f_{\mathbf{G}}$ 是[傅里叶系数](@entry_id:144886)。这个展开式揭示了一个深刻的对偶关系：实空间中的周期性结构，在傅里叶变换后的空间中，其信息被“压缩”到了[倒易晶格](@entry_id:136718)的离散点上。如果我们计算 $f(\mathbf{r})$ 的傅里叶变换 $F(\mathbf{k})$，我们会发现它仅在 $\mathbf{k}$ 等于某个[倒易晶格矢量](@entry_id:263351) $\mathbf{G}$ 时才非零 。[倒易空间](@entry_id:754151)本质上是[晶格](@entry_id:148274)[实空间](@entry_id:754128)的[傅里叶对偶](@entry_id:200473)空间。

为了更具体地理解这一点，我们可以考虑一个理想化的晶体，其原子核密度由位于每个[晶格](@entry_id:148274)点 $\mathbf{R}$ 上的狄拉克 $\delta$ 函数之和来表示：$\rho(\mathbf{r}) = \sum_{\mathbf{R}} \delta(\mathbf{r} - \mathbf{R})$。这个函数（称为狄拉克梳）的傅里叶变换，可以通过泊松求和公式（Poisson Summation Formula）证明，它本身也是一个[倒易晶格](@entry_id:136718)上的狄拉克梳 ：

$$
\tilde{\rho}(\mathbf{k}) = \int \rho(\mathbf{r}) e^{-i\mathbf{k}\cdot\mathbf{r}} d^3\mathbf{r} = \frac{(2\pi)^3}{V_c} \sum_{\mathbf{G}} \delta(\mathbf{k} - \mathbf{G})
$$

其中 $V_c$ 是[实空间](@entry_id:754128)原胞的体积。这个结果清晰地表明，一个实空间中的[无限晶格](@entry_id:1126489)，在[倒易空间](@entry_id:754151)中对应着另一个无限的[倒易晶格](@entry_id:136718)。这与自由空间形成鲜明对比，后者的连续[平移对称性](@entry_id:171614)意味着其[波矢](@entry_id:178620)空间是连续且无限的，不存在晶格结构 。

如果实空间[晶格](@entry_id:148274)由[原胞基矢](@entry_id:142930) $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$ 生成，则[倒易晶格](@entry_id:136718)可以由一组倒易[基矢](@entry_id:199546) $\mathbf{b}_1, \mathbf{b}_2, \mathbf{b}_3$ 生成。这些[基矢](@entry_id:199546)由标准关系式 $\mathbf{a}_i \cdot \mathbf{b}_j = 2\pi \delta_{ij}$ 定义，其中 $\delta_{ij}$ 是克罗内克符号 。任何一个[倒易晶格矢量](@entry_id:263351) $\mathbf{G}$ 都可以写成 $\mathbf{G} = m_1 \mathbf{b}_1 + m_2 \mathbf{b}_2 + m_3 \mathbf{b}_3$，其中 $m_i$ 为整数。

### [布洛赫定理](@entry_id:137461)与[波矢](@entry_id:178620) k 的物理意义

[倒易空间](@entry_id:754151)最重要的应用之一是描述电子在周期性势场中的行为。一个电子在晶体中运动的哈密顿量 $\hat{H} = \frac{\hat{\mathbf{p}}^2}{2m} + V(\mathbf{r})$ 具有[晶格](@entry_id:148274)的[平移对称性](@entry_id:171614)，因为势能项 $V(\mathbf{r})$ 是周期性的。这意味着 $\hat{H}$ 与所有[晶格](@entry_id:148274)[平移算符](@entry_id:756122) $\hat{T}_{\mathbf{R}}$ 对易，即 $[\hat{H}, \hat{T}_{\mathbf{R}}] = 0$  。

根据量子力学和群论的基本原理，由于所有[平移算符](@entry_id:756122)相互对易（它们构成一个[阿贝尔群](@entry_id:150284)），我们可以找到一组同时是 $\hat{H}$ 和所有 $\hat{T}_{\mathbf{R}}$ 的共同[本征态](@entry_id:149904)。对于一个[本征态](@entry_id:149904) $\psi(\mathbf{r})$，我们有：

$$
\hat{T}_{\mathbf{R}} \psi(\mathbf{r}) = \psi(\mathbf{r}+\mathbf{R}) = c(\mathbf{R}) \psi(\mathbf{r})
$$

其中 $c(\mathbf{R})$ 是本征值。由于平移的[组合性](@entry_id:637804)质，这些本征值必须满足 $c(\mathbf{R}_1)c(\mathbf{R}_2) = c(\mathbf{R}_1+\mathbf{R}_2)$。又因为 $\hat{T}_{\mathbf{R}}$ 是幺正算符，其本征值的模必须为 $1$。满足这些条件的唯一连续函数形式是 $c(\mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}}$，其中 $\mathbf{k}$ 是一个实矢量，被称为**[波矢](@entry_id:178620)**（wavevector）。

这就是**[布洛赫定理](@entry_id:137461)**的核心内容：在[周期性势场](@entry_id:140652)中，[能量本征态](@entry_id:152154)可以被一个波矢 $\mathbf{k}$ 标记，并满足以下关系：

$$
\psi_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}} \psi_{\mathbf{k}}(\mathbf{r})
$$

这个定理通常被写成等价的形式 $\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})$，其中 $u_{n\mathbf{k}}(\mathbf{r})$ 是一个具有[晶格](@entry_id:148274)周期的函数，即 $u_{n\mathbf{k}}(\mathbf{r}+\mathbf{R}) = u_{n\mathbf{k}}(\mathbf{r})$ 。这里的整数 $n$ 称为能带指标。

从[群表示论](@entry_id:141930)的观点来看，[波矢](@entry_id:178620) $\mathbf{k}$ 的作用是标记[晶格](@entry_id:148274)平移群的[不可约表示](@entry_id:263310)（irreducible representations）。由于平移群是[阿贝尔群](@entry_id:150284)，其所有[不可约表示](@entry_id:263310)都是一维的，由特征标（character）$\chi_{\mathbf{k}}(\mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}}$ 给出  。

必须强调，与[波矢](@entry_id:178620) $\mathbf{k}$ 相关的量 $\hbar\mathbf{k}$ 被称为**[晶体动量](@entry_id:136369)**（crystal momentum），它**不是**电子的真实[机械动量](@entry_id:156068)。电子的真实[动量算符](@entry_id:151743)的[期望值](@entry_id:150961) $\langle\hat{\mathbf{p}}\rangle$ 通常不等于 $\hbar\mathbf{k}$，因为它还包含[布洛赫函数](@entry_id:189422)周期部分 $u_{n\mathbf{k}}(\mathbf{r})$ 的贡献 。[晶体动量](@entry_id:136369)是一个与晶体[平移对称性](@entry_id:171614)相关的[量子数](@entry_id:145558)，而不是诺特定理意义下与连续空间平移对称性相关联的守恒动量。

### [第一布里渊区](@entry_id:269110)：波矢的唯一表示域

[布洛赫定理](@entry_id:137461)的一个直接推论是，并非所有 $\mathbf{k}$ 矢量都标记了物理上不同的状态。考虑一个波矢 $\mathbf{k}$ 和另一个波矢 $\mathbf{k}' = \mathbf{k} + \mathbf{G}$，其中 $\mathbf{G}$ 是任意一个[倒易晶格矢量](@entry_id:263351)。这两个波矢对应的布洛赫相位因子是相同的，因为：

$$
e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}} e^{i\mathbf{G}\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}} \times 1 = e^{i\mathbf{k}\cdot\mathbf{R}}
$$

这意味着波矢 $\mathbf{k}$ 和 $\mathbf{k}+\mathbf{G}$ 标记了平移群的同一个[不可约表示](@entry_id:263310)，它们在物理上是等价的  。这一等价性导致了所有[物理可观测量](@entry_id:154692)，如能带能量 $E_n(\mathbf{k})$，在倒易空间中也必须是周期的：

$$
E_n(\mathbf{k}) = E_n(\mathbf{k}+\mathbf{G})
$$

既然所有信息都以[倒易晶格](@entry_id:136718) $\mathbf{G}$ 为周期重复出现，我们只需要在一个[倒易晶格](@entry_id:136718)的原胞内[分析物](@entry_id:199209)理性质就足够了。这个为分析选取的、包含所有不等价 $\mathbf{k}$ 矢量的基本区域，就被称为**第一布里渊区（First Brillouin Zone, FBZ）**。

从几何上看，[第一布里渊区](@entry_id:269110)被定义为[倒易晶格](@entry_id:136718)的**维格纳-赛兹（Wigner-Seitz）原胞**。这是一个围绕倒易空间原点 $(\mathbf{k}=\mathbf{0})$ 的区域，该区域内的任何一点 $\mathbf{k}$ 到原点的距离比它到任何其他[倒易晶格](@entry_id:136718)点 $\mathbf{G} (\mathbf{G} \neq \mathbf{0})$ 的距离都更近（或相等）。这个定义可以形式化地写为 ：

$$
\text{FBZ} = \{\mathbf{k} : |\mathbf{k}| \le |\mathbf{k}-\mathbf{G}| \text{ for all } \mathbf{G} \in \Lambda^*, \mathbf{G} \neq \mathbf{0}\}
$$

这个不等式 $|\mathbf{k}| \le |\mathbf{k}-\mathbf{G}|$ 等价于 $2\mathbf{k}\cdot\mathbf{G} \le |\mathbf{G}|^2$，它定义的[半空间](@entry_id:634770)边界是垂直平分连接原点和倒易格点 $\mathbf{G}$ 的线段的平面。因此，第一布里渊区是由一系列这样的平面的交集构成的封闭区域。

例如，对于一个二维三角[晶格](@entry_id:148274)（其[倒易晶格](@entry_id:136718)也是一个三角[晶格](@entry_id:148274)，旋转了 $30^\circ$），其最近邻的倒易格点有六个。这六个点对应的[垂直平分线](@entry_id:163148)构成了一个正六边形，这就是该[晶格](@entry_id:148274)的[第一布里渊区](@entry_id:269110) 。一个常见的误解是认为第一布里渊区就是包含所有最小模长 $\mathbf{k}$ 矢量的区域。然而，如该六边形例子所示，[布里渊区](@entry_id:142395)角点的模长可能大于某些位于第二[布里渊区](@entry_id:142395)内、靠近第一布里渊区边界中点的模长 。

第一布里渊区的体积与实空间[原胞](@entry_id:159354)的体积 $V_c$ 之间存在一个简单的倒数关系：$V_{BZ} = (2\pi)^3 / V_c$  。

### 物理后果与应用

[倒易空间](@entry_id:754151)和[布里渊区](@entry_id:142395)的概念不仅仅是数学上的构造，它们直接关联到晶体材料可观测的物理性质。

#### [能带隙](@entry_id:156238)的形成

在[近自由电子模型](@entry_id:138124)中，我们可以将晶体的弱[周期势](@entry_id:140652) $V(\mathbf{r})$ 展开为傅里叶级数 $V(\mathbf{r})=\sum_{\mathbf{G}}V_{\mathbf{G}}e^{i\mathbf{G}\cdot \mathbf{r}}$。这个[势场](@entry_id:143025)会引起不同平面波态 $| \mathbf{k} \rangle$ 之间的耦合。哈密顿量的[矩阵元](@entry_id:186505)表明，[势场](@entry_id:143025)仅耦合那些波矢相差一个[倒易晶格矢量](@entry_id:263351) $\mathbf{G}$ 的平面波态，其耦合强度正比于[傅里叶系数](@entry_id:144886) $V_{\mathbf{G}}$ 。

当电子的[波矢](@entry_id:178620) $\mathbf{k}$ 恰好位于[布里渊区](@entry_id:142395)边界上时，这种耦合效应最为显著。布里渊区边界满足条件 $2\mathbf{k}\cdot\mathbf{G} = |\mathbf{G}|^2$，这恰好也是自由电子态 $| \mathbf{k} \rangle$ 和 $| \mathbf{k}-\mathbf{G} \rangle$ [能量简并](@entry_id:203091)的条件。根据[简并微扰理论](@entry_id:143587)，一个非零的[势场](@entry_id:143025)分量 $V_{\mathbf{G}}$ 会解除这个简并，在布里渊区边界上打开一个宽度为 $2|V_{\mathbf{G}}|$ 的**[能隙](@entry_id:138445)（energy gap）**。这正是晶体中半导体和绝缘体[带隙形成](@entry_id:265171)的根本原因 。

#### 衍射与[晶体动量守恒](@entry_id:145588)

[倒易晶格](@entry_id:136718)最直接的实验证据来自衍射实验，如X射[线或](@entry_id:170208)[中子衍射](@entry_id:140330)。当一个波矢为 $\mathbf{k}$ 的平面波入射到晶体上并发生[弹性散射](@entry_id:152152)，出射[波矢](@entry_id:178620)为 $\mathbf{k}'$。在玻恩一级近似下，[散射强度](@entry_id:202196)正比于晶体势场 $V(\mathbf{r})$ 在动量转移 $\mathbf{Q} = \mathbf{k}' - \mathbf{k}$ 处的傅里叶变换的模方。

由于 $V(\mathbf{r})$ 是[晶格](@entry_id:148274)[周期函数](@entry_id:139337)，其傅里叶变换仅在 $\mathbf{Q}$ 等于某个[倒易晶格矢量](@entry_id:263351) $\mathbf{G}$ 时非零。因此，要观察到相干的、建设性干涉产生的衍射峰，动量转移必须满足**[劳厄条件](@entry_id:147541)（Laue condition）** ：

$$
\mathbf{k}' - \mathbf{k} = \mathbf{G}
$$

这个条件表明，衍射峰的位置直接映射出晶体的[倒易晶格](@entry_id:136718)结构。结合[弹性散射](@entry_id:152152)条件 $|\mathbf{k}'| = |\mathbf{k}|$，[劳厄条件](@entry_id:147541)可以被重写为 $2\mathbf{k}\cdot\mathbf{G} + G^2 = 0$，这正是[布拉格定律](@entry_id:140129)的矢量形式。

这一[选择定则](@entry_id:140784)也阐明了**[晶体动量守恒](@entry_id:145588)**的含义。在一个晶体内部的相互作用过程中（如[电子-声子散射](@entry_id:138098)），总的晶体动量是守恒的，但这个守恒是“模 $\mathbf{G}$”意义下的守恒，即 $\sum \mathbf{k}_{initial} = \sum \mathbf{k}_{final} + \mathbf{G}$。[晶格](@entry_id:148274)整体可以吸收或提供一个大小为 $\hbar\mathbf{G}$ 的动量，而其自身状态不发生改变。因此，电子的真实[机械动量](@entry_id:156068)在与[晶格](@entry_id:148274)的相互作用中并不守恒  。例如，在一个体心立方（BCC）[晶格](@entry_id:148274)中，只有当衍射指标 $(h,k,l)$ 的和 $h+k+l$ 为偶数时，[结构因子](@entry_id:158623)才非零，才会出现衍射峰。利用这一规则和[劳厄条件](@entry_id:147541)，可以精确预测特定波长的中子在晶体上的最小衍射角 。

### [材料模拟](@entry_id:176516)中的计算考量

在现代计算材料科学中，特别是在基于密度泛函理论（DFT）的[多尺度模拟](@entry_id:752335)中，对倒易空间和布里渊区的精确处理至关重要。

#### [能带折叠](@entry_id:272980)

为了研究缺陷、表面或复杂的[磁序](@entry_id:161845)，研究人员常常需要使用比[晶体学](@entry_id:140656)[原胞](@entry_id:159354)大得多的**超胞（supercell）**。例如，构造一个 $N \times N \times N$ 的超胞，其实空间基矢变为 $\mathbf{A}_i = N\mathbf{a}_i$。根据[实空间](@entry_id:754128)与[倒易空间](@entry_id:754151)的倒数关系，这会导致[倒易空间](@entry_id:754151)的基矢缩短为 $\mathbf{B}_i = \mathbf{b}_i / N$，第一布里渊区的线性尺寸在每个方向上都缩小为原来的 $1/N$，体积则缩小为 $1/N^3$ 。

原本在较大的[原胞](@entry_id:159354)[布里渊区](@entry_id:142395)中描述的[能带结构](@entry_id:139379) $E(\mathbf{k})$，现在必须被“折叠”到这个更小的超胞布里渊区中。任何一个在[原胞](@entry_id:159354)B.Z.中的[波矢](@entry_id:178620) $\mathbf{k}$，在超胞表象下被重新标记为一个等效的[波矢](@entry_id:178620) $\mathbf{k}'$，两者之间通过一个超胞的倒易格矢 $\mathbf{G}'$ 相关联：$\mathbf{k} = \mathbf{k}' + \mathbf{G}'$。

这意味着，对于超胞B.Z.中的每一个点 $\mathbf{k}'$，会对应原能带结构中 $N^3$ 个不同点（由 $N^3$ 个不同的折叠矢量 $\mathbf{G}'$ 连接）的能量值。因此，原胞中的一条能带，在超胞的[能带图](@entry_id:1124081)中会表现为 $N^3$ 条折叠后的能带 。这些折叠矢量 $\mathbf{G}'$ 构成了超胞[倒易晶格](@entry_id:136718)关于[原胞](@entry_id:159354)[倒易晶格](@entry_id:136718)的[商群](@entry_id:145113)的代表元集 。例如，对于一个[自由电子气](@entry_id:145649)，其抛物线能带 $E(\mathbf{k}) \propto |\mathbf{k}|^2$ 在一个 $2 \times 2 \times 2$ 的超胞中会折叠成 $8$ 支抛物线，每一支都以不同的倒易格点为中心 。这一**[能带折叠](@entry_id:272980)（band folding）**现象是理解超胞计算结果的关键。

#### 不可约[布里渊区](@entry_id:142395)

计算晶体的体性质（如总能、电荷密度）通常需要对整个第一布里渊区进行积分。然而，大多数晶体除了[平移对称性](@entry_id:171614)外，还具有[点群对称性](@entry_id:141230)（如旋转、反映）。这些[对称操作](@entry_id:143398) $g$ 构成了晶体的**[点群](@entry_id:142456)** $G$。[物理可观测量](@entry_id:154692)，如能带能量，通常在[点群](@entry_id:142456)操作下保持不变：$E(g\mathbf{k}) = E(\mathbf{k})$ 。

利用这一对称性，我们可以将积分范围从整个[第一布里渊区](@entry_id:269110)（BZ）缩小到一个更小的区域，称为**不可约[布里渊区](@entry_id:142395)（Irreducible Brillouin Zone, IBZ）**。IBZ是BZ在[点群](@entry_id:142456) $G$ 作用下的一个基本畴，其通过[点群](@entry_id:142456)操作可以生成整个BZ。对BZ的积分可以简化为对IBZ的积分，并乘以点[群的阶](@entry_id:137115)数 $|G|$：

$$
\int_{\mathrm{BZ}} F(\mathbf{k}) \, d^d k = |G| \int_{\mathrm{IBZ}} F(\mathbf{k}) \, d^d k
$$

在实际计算中，我们使用离散的 $\mathbf{k}$ 点网格来近似积分。对称性同样可以减少需要计算的 $\mathbf{k}$ 点数量。我们只需在IBZ内选择 $\mathbf{k}$ 点，然后通过赋予每个点一个合适的“权重”来重构整个BZ的和。一个IBZ内的 $\mathbf{k}$ 点的权重等于其在[点群](@entry_id:142456)操作下生成的不同 $\mathbf{k}$ 点的数目（即其轨道的尺寸）。这个数目由轨道-稳定子定理决定，取决于该 $\mathbf{k}$ 点的对称性。例如，在一个具有 $D_4$ [点群](@entry_id:142456)（阶数为8）的二维方格子上，一个普通位置的 $\mathbf{k}$ 点权重为 $8$，而位于[对称轴](@entry_id:177299)上的点（如[X点](@entry_id:1134148)）权重会更小（如 $2$），位于中心的$\Gamma$点权重则为 $1$ 。精确使用IBZ和 $\mathbf{k}$ 点权重是进行高效、准确的第一性原理计算的标准做法。