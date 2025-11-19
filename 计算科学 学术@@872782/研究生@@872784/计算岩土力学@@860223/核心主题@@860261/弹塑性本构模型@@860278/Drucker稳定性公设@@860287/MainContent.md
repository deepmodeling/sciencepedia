## 引言
在计算岩[土力学](@entry_id:180264)的广阔领域中，构建能够准确预测材料行为的本构模型至关重要。然而，如何确保这些数学模型在物理上是合理且稳定的？Daniel C. Drucker 提出的稳定性公设正是为了回答这一根本问题，它为评估和约束[弹塑性](@entry_id:193198)材料模型提供了一个严谨而深刻的准则，成为了连接理论力学与工程实践的桥梁。该公设解决了将“稳定性”这一直观物理概念形式化为具体数学约束的知识空白，并揭示了其对模型行为的深远影响。

本文将系统地引导读者深入理解[德鲁克稳定性公设](@entry_id:200080)。在“**原理与机制**”一章中，我们将追溯其物理思想，阐明其数学表述，并探讨其对[屈服面凸性](@entry_id:756808)和关联[流动法则](@entry_id:177163)的决定性作用。接下来，在“**应用与跨学科联系**”一章中，我们将展示该公设如何被应用于分析岩土材料的非关联性失稳、预测[应变局部化](@entry_id:176973)、验证[计算模型](@entry_id:152639)，并触及其在[损伤力学](@entry_id:178377)等领域的延伸。最后，通过“**动手实践**”部分的引导，您将有机会通过具体的推导和计算练习，将理论知识转化为解决实际问题的能力。让我们从这一基本原理出发，开启对[材料稳定性](@entry_id:183933)的探索之旅。

## 原理与机制

在连续介质力学和[弹塑性](@entry_id:193198)理论的框架下，材料的稳定性是一个核心概念。它确保了在给定的边界条件下，材料的本构响应是唯一且物理上合理的。Daniel C. Drucker 提出的稳定性公设为评估和约束[弹塑性](@entry_id:193198)材料本构模型提供了一个强有力的准则。本章将深入探讨 Drucker 稳定性公设的物理基础、数学表述、几何解释及其在计算岩[土力学](@entry_id:180264)中的深远影响。

### 物理基础：封闭循环中的功

Drucker 稳定性公设最初的构想源于一个直观的物理思想实验。考虑一个处于平衡状态的[弹塑性](@entry_id:193198)体。一个外部作用源对该物体施加一个应力-应变循环，即加载至某一状态，然后卸载，使物体恢复到其初始的应力状态。Drucker 假设，对于一个“稳定”的材料，在任何此类的封闭[应力循环](@entry_id:200486)中，外部作用源所做的净功必须是非负的。

换句话说，材料本身不能成为一个净能量的来源。如果在一个封闭循环中，材料对外界做了净正功（即外部作用源做了净负功），那么我们就可以通过反复[循环加载](@entry_id:181502)来从该材料中无限地提取能量。这相当于制造了一个[第二类永动机](@entry_id:139670)，它能在单一热源下持续做功，这显然违背了热力学第二定律。[@problem_id:3519480]

这个概念可以被数学化地表述为对任意封闭[应力循环](@entry_id:200486)的塑性[功积分](@entry_id:181218)：

$$
\oint \boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^p \ge 0
$$

这里，$\boldsymbol{\sigma}$ 是柯西应力张量，$d\boldsymbol{\varepsilon}^p$ 是塑性应变增量，冒号 $:$ 代表张量的[双点积](@entry_id:748648)。由于在封闭的[应力循环](@entry_id:200486)后，弹性应变恢复原状，因此外部作用源所做的总净功等于净塑性功。该积分非负的要求，从根本上排除了材料因变形循环而自发释放能量的可能性，从而保证了本构上的[热力学一致性](@entry_id:138886)。[@problem_id:3519480]

### 局部增量形式：微观稳定性

虽然封闭循环的概念在物理上很直观，但在建立增量式的[本构关系](@entry_id:186508)时，一个更实用、更局部的准则显得更为重要。通过考虑一个无穷小的应力-应变循环（加载一个无穷小应力增量 $d\boldsymbol{\sigma}$，然后立即卸载），Drucker 导出了其公设的局部或增量形式，通常被称为“微观稳定性”(stability in the small)。

该公设规定：**对于任何可容许的塑性增量，由应力增量 $d\boldsymbol{\sigma}$ 在塑性应变增量 $d\boldsymbol{\varepsilon}^p$ 上所做的二阶功必须是非负的。** [@problem_id:3519455]

其数学表达式为：

$$
d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^p \ge 0
$$

为了精确理解此不等式，我们必须定义何为“可容许的塑性增量”。一个塑性增量是可容许的，必须满足两个条件 [@problem_id:3519500]：
1.  **初始状态条件**：材料的应力状态必须位于[屈服面](@entry_id:175331)上，即 $f(\boldsymbol{\sigma}, k) = 0$，其中 $f$ 是[屈服函数](@entry_id:167970)，$k$ 代表[硬化](@entry_id:177483)参数。塑性变形只能从已经达到屈服的状态开始。
2.  **加载条件**：应力增量必须指向[屈服面](@entry_id:175331)的外部或与其相切，即不能是卸载。这通常表示为[屈服函数](@entry_id:167970)的[全微分](@entry_id:171747) $df(\boldsymbol{\sigma}, k) \ge 0$。这个条件确保了应力增量不会将应力状态点带回到弹性域内部。

这个不等式可以用指标符号更严谨地写出，即 $d\sigma_{ij} d\varepsilon^p_{ij} \ge 0$。根据爱因斯坦求和约定，该式代表对所有重复的指标 $i,j \in \{1,2,3\}$ 求和。在标准的[连续介质力学](@entry_id:155125)中，由于角动量守恒（无体力矩），柯西应力张量是对称的（$\sigma_{ij} = \sigma_{ji}$）；同样，[小应变张量](@entry_id:754968)根据其定义也是对称的（$\varepsilon^p_{ij} = \varepsilon^p_{ji}$）。因此，这个[双点积](@entry_id:748648)是一个定义明确的标量。[@problem_id:3519512]

### 稳定性与[热力学](@entry_id:141121)耗散的区别

初学者常常将 Drucker 稳定性公设与[热力学第二定律](@entry_id:142732)直接导出的[塑性耗散](@entry_id:201273)原理相混淆。区分这两者至关重要。

根据克劳修斯-杜亨不等式（Clausius-Duhem inequality），在等温条件下，任何不[可逆过程](@entry_id:276625)的内[耗散率](@entry_id:748577)必须是非负的。对于[弹塑性](@entry_id:193198)材料，这主要表现为塑性功率的非负性 [@problem_id:3519448]：

$$
\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p \ge 0
$$

其中 $\dot{\boldsymbol{\varepsilon}}^p$ 是塑性[应变率](@entry_id:154778)。这是一个**一阶**功量，它直接源于[热力学](@entry_id:141121)基本定律，适用范围非常广泛，包括黏塑性模型，并且不要求关联流动法则或[屈服面凸性](@entry_id:756808)。

相比之下，Drucker 公设 $d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^p \ge 0$ 是一个关于**二阶**功的不等式。它不是[热力学第二定律](@entry_id:142732)的直接推论，而是一个更强的、为保证[材料稳定性](@entry_id:183933)而额外引入的**本构假设**。Drucker 公设主要适用于准静态、率无关的[弹塑性](@entry_id:193198)理论，它对[本构模型](@entry_id:174726)施加了比[热力学](@entry_id:141121)耗散原理更严格的约束。[@problem_id:3519448]

### 公设的推论：[凸性](@entry_id:138568)与关联流动法则

Drucker 稳定性公设之所以在塑性力学中如此重要，是因为它直接导出了两个基本性质：屈服面的**[凸性](@entry_id:138568)** (convexity) 和塑性流动的**关联性** (associativity) 或称正交性 (normality)。

让我们从几何角度来理解这一点。考虑一个关联[流动法则](@entry_id:177163)，即塑性应变增量的方向与屈服面在该应力点的外法线方向一致：

$$
d\boldsymbol{\varepsilon}^p = d\lambda \, \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$

其中 $d\lambda \ge 0$ 是一个非负的标量，称为塑性乘子，而梯度 $\frac{\partial f}{\partial \boldsymbol{\sigma}}$ （或 $\nabla_{\boldsymbol{\sigma}} f$）代表了[屈服面](@entry_id:175331)的外法线方向。将此关联流动法则代入 Drucker 公设：

$$
d\boldsymbol{\sigma} : \left( d\lambda \, \frac{\partial f}{\partial \boldsymbol{\sigma}} \right) \ge 0
$$

由于 $d\lambda \ge 0$，这直接意味着：

$$
d\boldsymbol{\sigma} : \frac{\partial f}{\partial \boldsymbol{\sigma}} \ge 0
$$

这个不等式有一个清晰的几何解释：在塑性加载过程中，应力增量向量 $d\boldsymbol{\sigma}$ 与屈服面的外[法线](@entry_id:167651)向量 $\frac{\partial f}{\partial \boldsymbol{\sigma}}$ 的夹角不能大于 $90^\circ$。换言之，$d\boldsymbol{\sigma}$ 必须指向由[屈服面](@entry_id:175331)在当前应力点的[切平面](@entry_id:136914)所定义的“外部”[半空间](@entry_id:634770)。[@problem_id:3519510] 这个简单的几何约束是屈服面必须为**[凸集](@entry_id:155617)**的直接原因。如果屈服面在某处是凹的，我们就可以找到两个屈服面上的点，其连线（代表一个应力增量 $d\boldsymbol{\sigma}$）完全位于弹性域内部，这会违反上述条件。

反之，Drucker 公设也要求[流动法则](@entry_id:177163)是关联的。如果流动方向 $d\boldsymbol{\varepsilon}^p$ 不平行于法线方向 $\frac{\partial f}{\partial \boldsymbol{\sigma}}$，那么它在[屈服面](@entry_id:175331)的[切平面](@entry_id:136914)上必有非零投影。这样我们总可以找到一个沿着切平面的应力增量 $d\boldsymbol{\sigma}$，它与 $d\boldsymbol{\varepsilon}^p$ 的投影方向相反，从而导致 $d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^p  0$，违反了稳定性。

因此，对于满足 Drucker 稳定性的材料，其屈服面必须是凸的，且其塑性流动必须遵循关联流动法则。

### 与[材料硬化](@entry_id:175896)/软化的关系

Drucker 公设与材料的[硬化](@entry_id:177483)或软化行为密切相关。通过塑性一致性条件 $df=0$，我们可以将[二阶塑性功](@entry_id:754602) $d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^p$ 与材料的[硬化](@entry_id:177483)模量联系起来。在塑性加载期间，应力点必须保持在演化的[屈服面](@entry_id:175331)上，因此[屈服函数](@entry_id:167970)的[全微分](@entry_id:171747)为零：

$$
df = \frac{\partial f}{\partial \boldsymbol{\sigma}} : d\boldsymbol{\sigma} + \frac{\partial f}{\partial k} dk = 0
$$

对于关联流动，$d\boldsymbol{\varepsilon}^p = d\lambda \frac{\partial f}{\partial \boldsymbol{\sigma}}$。结合以上两式，可以推导出[二阶塑性功](@entry_id:754602) $dW^{(2)} = d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^p$ 与[硬化](@entry_id:177483)模量 $H$（定义了 $dk$ 与塑性应变大小的关系）成正比。对于常见的模型，可以得到类似 $dW^{(2)} = \mathcal{H} (d\lambda)^2$ 的关系，其中 $\mathcal{H}$ 是一个与[硬化](@entry_id:177483)模量同号的量。[@problem_id:3519455]

因此，Drucker 公设 $d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^p \ge 0$ 直接对应于：
-   **[应变硬化](@entry_id:160669) (Strain Hardening)**：$H > 0 \implies dW^{(2)} > 0$，材料是严格稳定的。
-   **[理想塑性](@entry_id:753335) (Perfect Plasticity)**：$H = 0 \implies dW^{(2)} = 0$，材料是中性稳定的。
-   **[应变软化](@entry_id:755491) (Strain Softening)**：$H  0 \implies dW^{(2)}  0$，材料是不稳定的。

这揭示了 Drucker 稳定性公设的一个核心作用：它从根本上排除了在标准[弹塑性](@entry_id:193198)框架内的[应变软化](@entry_id:755491)行为。

### 公设的违背及其后果

尽管 Drucker 公设为建立稳定、行为良好的[本构模型](@entry_id:174726)提供了坚实基础，但在岩土材料的建模中，常常需要采用违背该公设的模型来描述真实的物理现象。

#### [非关联流动](@entry_id:199220)

岩土材料（如土壤、岩石和混凝土）的一个显著特征是其[剪胀性](@entry_id:201001)（dilatancy），即在剪切作用下发生[体积膨胀](@entry_id:144241)。如果采用关联流动法则，剪胀的大小将由[屈服函数](@entry_id:167970)对[平均应力](@entry_id:751819)的依赖性唯一确定，这往往会严重高估实际的剪胀行为。因此，在岩[土力学](@entry_id:180264)中，广泛采用**[非关联流动法则](@entry_id:752544)** (non-associated flow rule)，即塑性势函数 $g$ 与[屈服函数](@entry_id:167970) $f$ 不一致 ($g \neq f$)。

$$
d\boldsymbol{\varepsilon}^p = d\lambda \, \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$

在这种情况下，塑性流动的方向 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 不再保证与[屈服面](@entry_id:175331) $f=0$ 正交。当流动方向与[法线](@entry_id:167651)方向偏离足够大时，就可能违反 Drucker 稳定性。[@problem_id:3519499] 几何上，这意味着流动向量 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 不再位于屈服面[法锥](@entry_id:272387)之内。此时，可以找到一个沿[屈服面](@entry_id:175331)切向的应力增量 $d\boldsymbol{\sigma}$，使得 $d\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}}  0$，从而导致 $d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^p  0$。例如，考虑一个圆形的 von Mises [屈服面](@entry_id:175331) ($f$) 和一个椭圆形的塑性[势函数](@entry_id:176105) ($g$)，在某些应力点，流动方向会向内偏离法线，导致与某些切向应力增量的[点积](@entry_id:149019)为负，从而违反稳定性。[@problem_id:3519499]

#### 后果：解的非唯一性

违反 Drucker 稳定性最严重的后果之一是在增量[边值问题](@entry_id:193901)中可能导致**解的非唯一性** (non-uniqueness of the solution)。在[计算塑性力学](@entry_id:171377)中，增量[本构关系](@entry_id:186508)通常可以写成 $d\boldsymbol{\sigma} = \mathbf{C}_{ep} : d\boldsymbol{\varepsilon}$，其中 $\mathbf{C}_{ep}$ 是[弹塑性切线模量](@entry_id:189492)。Drucker 公设（对于关联流动）保证了 $\mathbf{C}_{ep}$ 的对称性和正定性。当公设被违背后，例如由于[非关联流动](@entry_id:199220)或[应变软化](@entry_id:755491)，[切线](@entry_id:268870)模量 $\mathbf{C}_{ep}$ 可能变得非对称，甚至不再是正定的。

一个非对称的[切线](@entry_id:268870)算子意味着在[有限元法](@entry_id:749389)中会产生非对称的[刚度矩阵](@entry_id:178659)，增加了计算成本。更严重的是，当 $\mathbf{C}_{ep}$ 失去正定性时，控制方程可能会失去[双曲性](@entry_id:262766)或椭圆性，导致[应变局部化](@entry_id:176973)（strain localization）等物理失稳现象，并且增量问题的解可能不再唯一。

让我们通过一个简单的例子来说明解的非唯一性 [@problem_id:3519485]。考虑一个材料点，其塑性行为由两个同时激活的线性屈服面 $F_1, F_2$ 和一个[非关联流动法则](@entry_id:752544)控制。在给定的总应变增量 $d\boldsymbol{\varepsilon}$ 下，我们需要求解塑性乘子增量 $d\lambda_1, d\lambda_2$。求解过程需要满足一致性条件，即加载后的应力状态仍在两个[屈服面](@entry_id:175331)上。这导出一个关于 $d\lambda_1, d\lambda_2$ 的[线性方程组](@entry_id:148943) $\mathbf{H} \begin{pmatrix} d\lambda_1 \\ d\lambda_2 \end{pmatrix} = \mathbf{b}$。其中，矩阵 $\mathbf{H}$ (称为相互作用矩阵) 的项依赖于[屈服面](@entry_id:175331)法向 $\mathbf{n}_i$ 和流动方向 $\mathbf{m}_j$。在设计巧妙的[非关联流动](@entry_id:199220)（即 $\mathbf{m}_j$ 与 $\mathbf{n}_i$ 严重偏离）下，矩阵 $\mathbf{H}$ 可能变成奇异的（$\det(\mathbf{H})=0$）。如果同时右端项 $\mathbf{b}$ 与 $\mathbf{H}$ 的列向量线性相关，该[方程组](@entry_id:193238)将拥有无穷多组满足 $d\lambda_1, d\lambda_2 \ge 0$ 的解。每一组解 $(d\lambda_1, d\lambda_2)$ 都对应一个不同的、但同样“可容许”的塑性应变增量 $d\boldsymbol{\varepsilon}^p$。这表明，对于同一个总应变增量，材料的响应是不确定的，这在物理和计算上都是一个严重的问题。[@problem_id:3519485]

### [复杂介质](@entry_id:164088)中的应用与推广

Drucker 稳定性公设的概念可以被推广到更复杂的力学环境中。

#### 饱和多孔介质

在岩土工程中，材料通常是饱和的多孔介质。根据 Terzaghi 和 Biot 的[有效应力原理](@entry_id:755871)，固相骨架的变形行为主要由**[有效应力](@entry_id:198048)** $\boldsymbol{\sigma}'$ 控制，而非总应力 $\boldsymbol{\sigma}$。[有效应力](@entry_id:198048)定义为 $\boldsymbol{\sigma}' = \boldsymbol{\sigma} - \alpha p \boldsymbol{I}$，其中 $p$ 是孔隙[流体压力](@entry_id:142203)，$\alpha$ 是 Biot 系数，$\boldsymbol{I}$ 是单位张量。

由于塑性变形是固相骨架的不可[逆变](@entry_id:192290)形，因此稳定性公设必须应用于驱动这种变形的有效应力。因此，对于饱和[多孔介质](@entry_id:154591)，Drucker 公设应写为 [@problem_id:3519493]：

$$
d\boldsymbol{\sigma}' : d\boldsymbol{\varepsilon}^p \ge 0
$$

这一形式要求[屈服面](@entry_id:175331)在[有效应力](@entry_id:198048)空间中是凸的。同时，在计算上，如果采用基于有效应力的关联[流动法则](@entry_id:177163)，它将保证[弹塑性切线模量](@entry_id:189492) $\mathbf{C}_{ep}$ 的对称性，这对于大型有限元模拟的效率至关重要。[@problem_id:3519493]

#### [有限应变理论](@entry_id:176941)

当变形不再微小时，必须采用[有限应变理论](@entry_id:176941)。在这种情况下，需要仔细选择[功共轭](@entry_id:194957)的应力-[应变率](@entry_id:154778)对。一个常用的选择是**[基尔霍夫应力](@entry_id:751039)** $\boldsymbol{\tau} = J \boldsymbol{\sigma}$（其中 $J=\det(\mathbf{F})$ 是变形梯度的[行列式](@entry_id:142978)）和**塑性变形率张量** $\mathbf{D}^p$。[基尔霍夫应力](@entry_id:751039)与总变形率张量 $\mathbf{D}$ 的[点积](@entry_id:149019)给出了单位参考体积的功率。

在此框架下，[塑性耗散](@entry_id:201273)率（单位参考体积）为 $\boldsymbol{\tau} : \mathbf{D}^p$。因此，Drucker 稳定性公设的直接推广形式（更准确地说是[热力学](@entry_id:141121)耗散原理）是要求[塑性耗散](@entry_id:201273)率非负 [@problem_id:3519504]：

$$
\boldsymbol{\tau} : \mathbf{D}^p \ge 0
$$

这个不等式确保了在有限变形下，塑性过程总是耗散能量的，为建立[热力学一致的](@entry_id:755906)[大变形](@entry_id:167243)本构模型提供了基础。更严格的二阶功形式的稳定性公设也可以在此框架下建立，但其表述更为复杂，通常涉及到应力率的客观性问题。

综上所述，Drucker 稳定性公设不仅是[弹塑性](@entry_id:193198)理论的基石，也为理解和构建岩土材料的本构模型提供了深刻的洞察。它将[材料稳定性](@entry_id:183933)与屈服面几何、流动法则、硬化行为以及数值[解的唯一性](@entry_id:143619)紧密联系在一起，是连接理论力学与计算实践的关键桥梁。