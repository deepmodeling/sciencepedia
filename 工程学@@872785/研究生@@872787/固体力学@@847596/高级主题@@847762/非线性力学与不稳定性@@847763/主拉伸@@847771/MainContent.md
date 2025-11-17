## 引言
在连续介质力学领域，当材料经历显著的形状或尺寸变化时，线性应变理论不再适用，我们需要更普适的工具来描述变形。主拉伸（Principal Stretches）正是这样一个核心概念，它能够精确量化材料在局部经受的纯粹拉伸或压缩，同时剥离了[刚体转动](@entry_id:191086)的影响。然而，其背后深刻的数学原理和广泛的物理应用常常构成学习的难点，尤其是在如何将其从抽象的张量运算与具体的材料行为联系起来时。

本文旨在系统性地解析主拉伸的理论与实践。我们将从第一性原理出发，带领读者深入理解这一关键的运动学度量。在“原理与机制”章节中，您将学习主拉伸如何从变形梯度中导出，其与柯西-格林张量和极分解的内在联系，以及其客观性为何至关重要。接着，在“应用与跨学科联系”章节中，我们将展示主拉伸如何成为连接理论与实际的桥梁，探讨其在软材料本构、[金属塑性](@entry_id:176585)、固态[相变](@entry_id:147324)乃至[无损检测](@entry_id:273209)等前沿领域的应用。最后，通过“动手实践”部分提供的一系列精选问题，您将有机会将理论知识付诸实践，巩固对计算方法和物理概念的掌握。

## 原理与机制

### 主拉伸的[运动学](@entry_id:173318)定义与物理诠释

在有限变形理论中，描述[材料变形](@entry_id:169356)最基本的方式是通过**变形梯度** (deformation gradient) $\boldsymbol{F}$。它将参考构型中的一个无穷小材料线元 $d\boldsymbol{X}$ 映射到当前构型中的对应线元 $d\boldsymbol{x}$，即 $d\boldsymbol{x} = \boldsymbol{F}d\boldsymbol{X}$。为了量化一个特定方向上的伸长或缩短，我们引入**拉伸比** (stretch ratio) $\lambda$ 的概念。对于沿参考构型中单位矢量 $\boldsymbol{N}$ 方向的材料纤维，其拉伸比定义为变形后与变形前长度之比：$\lambda(\boldsymbol{N}) = |d\boldsymbol{x}| / |d\boldsymbol{X}|$。

为了便于分析，通常使用拉伸比的平方：
$$ \lambda^2(\boldsymbol{N}) = \frac{|d\boldsymbol{x}|^2}{|d\boldsymbol{X}|^2} = \frac{(\boldsymbol{F}d\boldsymbol{X}) \cdot (\boldsymbol{F}d\boldsymbol{X})}{(d\boldsymbol{X}) \cdot (d\boldsymbol{X})} $$
利用 $d\boldsymbol{X} = |\boldsymbol{d\boldsymbol{X}}|\boldsymbol{N}$ 和矩阵[转置的性质](@entry_id:148302)，上式可以写为：
$$ \lambda^2(\boldsymbol{N}) = \frac{d\boldsymbol{X} \cdot (\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}d\boldsymbol{X})}{d\boldsymbol{X} \cdot d\boldsymbol{X}} = \boldsymbol{N} \cdot (\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}\boldsymbol{N}) $$
这里，我们定义了一个核心的[对称张量](@entry_id:148092)——**右柯西-格林变形张量** (right Cauchy-Green deformation tensor) $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$。于是，沿任意方向 $\boldsymbol{N}$ 的拉伸平方可以简洁地表示为 $\lambda^2(\boldsymbol{N}) = \boldsymbol{N} \cdot \boldsymbol{C}\boldsymbol{N}$。

自然而然地，我们会问：在所有可能方向中，哪些方向经历了最大和最小的拉伸？这些极值拉伸是多少？这引导我们去寻找函数 $\lambda^2(\boldsymbol{N})$ 在约束条件 $|\boldsymbol{N}|=1$ 下的极值。这本质上是一个约束优化问题，可以通过[拉格朗日乘子法](@entry_id:176596)解决。我们构建[拉格朗日函数](@entry_id:174593) $\mathcal{L}(\boldsymbol{N}, \mu) = \boldsymbol{N} \cdot \boldsymbol{C}\boldsymbol{N} - \mu (\boldsymbol{N} \cdot \boldsymbol{N} - 1)$，其中 $\mu$ 是拉格朗日乘子。令其关于 $\boldsymbol{N}$ 的梯度为零，得到：
$$ 2\boldsymbol{C}\boldsymbol{N} - 2\mu\boldsymbol{N} = \boldsymbol{0} \quad \implies \quad \boldsymbol{C}\boldsymbol{N} = \mu\boldsymbol{N} $$
这个结果揭示了一个深刻的物理-数学联系：经历[极值](@entry_id:145933)拉伸的材料方向 $\boldsymbol{N}$，正是[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$ 的[特征向量](@entry_id:151813)。这些特殊的、相互正交的方向被称为**主方向** (principal directions)。而对应的[特征值](@entry_id:154894) $\mu$ 则是这些方向上的拉伸平方。我们将这些[特征值](@entry_id:154894)记为 $\lambda_i^2$，其中 $\lambda_i > 0$ 称为**主拉伸** (principal stretches)。因此，主拉伸和主方向由以下[特征值问题](@entry_id:142153)确定 [@problem_id:2675205]：
$$ \boldsymbol{C}\boldsymbol{N}_i = \lambda_i^2 \boldsymbol{N}_i $$
由于 $\boldsymbol{C}$ 是对称正定张量（只要 $\boldsymbol{F}$ 可逆），它保证有三个实且正的[特征值](@entry_id:154894) $\lambda_1^2, \lambda_2^2, \lambda_3^2$，以及一组对应的标准[正交特征向量](@entry_id:155522)基 $\{\boldsymbol{N}_1, \boldsymbol{N}_2, \boldsymbol{N}_3\}$。主拉伸 $\lambda_i$ 是这些[特征值](@entry_id:154894)的正平方根。

### [拉伸张量](@entry_id:193200)与极分解

虽然[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$ 在数学上很方便，但它度量的是拉伸的平方，并且将旋转与拉伸耦合在一起。为了更纯粹地描述拉伸，我们引入**右[拉伸张量](@entry_id:193200)** (right stretch tensor) $\boldsymbol{U}$。根据极分解定理，任何可逆的变形梯度 $\boldsymbol{F}$ 都可以唯一地分解为一个[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 和一个[对称正定](@entry_id:145886)张量 $\boldsymbol{U}$ 的乘积：
$$ \boldsymbol{F} = \boldsymbol{R}\boldsymbol{U} $$
这里，$\boldsymbol{R}$ 是一个纯旋转（$\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R} = \mathbf{I}, \det(\boldsymbol{R})=1$），描述了材料的[刚体转动](@entry_id:191086)；而 $\boldsymbol{U}$ 完全描述了在参考构型[坐标系](@entry_id:156346)下材料的拉伸。

将极分解代入 $\boldsymbol{C}$ 的定义，我们发现 $\boldsymbol{C} = (\boldsymbol{R}\boldsymbol{U})^{\mathsf{T}}(\boldsymbol{R}\boldsymbol{U}) = \boldsymbol{U}^{\mathsf{T}}\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}\boldsymbol{U} = \boldsymbol{U}^2$。这表明，右[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 是[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$ 的唯一正定平方根，即 $\boldsymbol{U} = \sqrt{\boldsymbol{C}}$。

这个关系使得我们可以直接从 $\boldsymbol{C}$ 的谱分解来构造 $\boldsymbol{U}$。若 $\boldsymbol{C}$ 的[谱分解](@entry_id:173707)为 $\boldsymbol{C} = \sum_{i=1}^3 \lambda_i^2 (\boldsymbol{N}_i \otimes \boldsymbol{N}_i)$，则 $\boldsymbol{U}$ 的[谱分解](@entry_id:173707)为 [@problem_id:2675198]：
$$ \boldsymbol{U} = \sum_{i=1}^{3} \lambda_{i} (\boldsymbol{N}_{i} \otimes \boldsymbol{N}_{i}) $$
这清晰地表明，右[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 与 $\boldsymbol{C}$ 共享相同的主方向（[特征向量](@entry_id:151813)）$\boldsymbol{N}_i$，而其[特征值](@entry_id:154894)恰好是主拉伸 $\lambda_i$。$\boldsymbol{U}$ 的[正定性](@entry_id:149643)直接保证了所有主拉伸 $\lambda_i$ 均为正实数。

类似地，存在**左极分解** $\boldsymbol{F} = \boldsymbol{V}\boldsymbol{R}$，其中 $\boldsymbol{V}$ 是**左[拉伸张量](@entry_id:193200)** (left stretch tensor)，描述在当前构型[坐标系](@entry_id:156346)下的拉伸。它与**[左柯西-格林张量](@entry_id:186163)** $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}$ 相关，满足 $\boldsymbol{B} = \boldsymbol{V}^2$。通过 $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}} = (\boldsymbol{R}\boldsymbol{U})(\boldsymbol{R}\boldsymbol{U})^{\mathsf{T}} = \boldsymbol{R}\boldsymbol{U}^2\boldsymbol{R}^{\mathsf{T}} = \boldsymbol{R}\boldsymbol{C}\boldsymbol{R}^{\mathsf{T}}$，我们看到 $\boldsymbol{B}$ 和 $\boldsymbol{C}$ 是[相似矩阵](@entry_id:155833)，因此它们拥有相同的[特征值](@entry_id:154894) $\lambda_i^2$。这意味着，无论是在参考构型还是当前构型中观察，材料经历的三个主拉伸值是相同的。它们的主方向则通过[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 相关联：当前构型中的[主方向](@entry_id:276187) $\boldsymbol{m}_i$ 是参考构型中[主方向](@entry_id:276187) $\boldsymbol{N}_i$ 的旋转结果，即 $\boldsymbol{m}_i = \boldsymbol{R}\boldsymbol{N}_i$ [@problem_id:2675205]。

### 客观性与标架无关性

在连续介质力学中，一个物理量如果在一个[刚体运动](@entry_id:193355)叠加后保持不变，则称该量是**客观的** (objective) 或**标架无关的** (frame-indifferent)。考虑一个已发生的变形 $\boldsymbol{F}$，再对其当前构型施加一个刚体旋转 $\boldsymbol{Q}$，新的变形梯度变为 $\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}$。

让我们来考察主拉伸的客观性。新的[右柯西-格林张量](@entry_id:174156)为：
$$ \boldsymbol{C}^* = (\boldsymbol{F}^*)^{\mathsf{T}}\boldsymbol{F}^* = (\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\mathbf{I}\boldsymbol{F} = \boldsymbol{C} $$
由于 $\boldsymbol{C}$ 在[刚体转动](@entry_id:191086)下保持不变，其[特征值](@entry_id:154894) $\lambda_i^2$ 也保持不变，因此主拉伸 $\lambda_i$ 是客观的物理量。这符合我们的物理直觉：材料的真实拉伸不应随观察者[坐标系](@entry_id:156346)的旋转而改变。

然而，变形梯度 $\boldsymbol{F}$ 本身的[特征值](@entry_id:154894)却不具备客观性。例如，考虑一个纯拉伸变形 $\boldsymbol{F}_0 = \mathrm{diag}(2, 1/2, 1)$，其[特征值](@entry_id:154894)为 $2, 1/2, 1$。对其施加一个旋转 $\boldsymbol{Q}$，得到 $\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}_0$。一般情况下，$\boldsymbol{F}^*$ 的[特征值](@entry_id:154894)将不同于 $\boldsymbol{F}_0$ 的[特征值](@entry_id:154894) [@problem_id:2675194]。这突显了为何不能简单地用 $\boldsymbol{F}$ 的[特征值](@entry_id:154894)来度量材料的拉伸，而必须使用从 $\boldsymbol{C}$ 或 $\boldsymbol{U}$ 导出的主拉伸。主拉伸是真正描述材料内禀变形状态的核心运动学量。

### 与[应变度量](@entry_id:755495)的关系

主拉伸是最基本的变形度量，其他常用的有限[应变张量](@entry_id:193332)的主值都可以由主拉伸导出。

**[格林-拉格朗日应变张量](@entry_id:187745)** (Green-Lagrange strain tensor) $\boldsymbol{E}$ 定义为 $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \mathbf{I})$。由于 $\boldsymbol{E}$ 是 $\boldsymbol{C}$ 的线性函数，它与 $\boldsymbol{C}$ 和 $\boldsymbol{U}$ 共享相同的[主方向](@entry_id:276187) $\boldsymbol{N}_i$。其主值 $E_i$ 可以通过将特征值问题应用于 $\boldsymbol{E}$ 得到：
$$ \boldsymbol{E}\boldsymbol{N}_i = \frac{1}{2}(\boldsymbol{C}\boldsymbol{N}_i - \mathbf{I}\boldsymbol{N}_i) = \frac{1}{2}(\lambda_i^2\boldsymbol{N}_i - \boldsymbol{N}_i) = \frac{1}{2}(\lambda_i^2 - 1)\boldsymbol{N}_i $$
因此，[格林-拉格朗日应变](@entry_id:170427)的主值与主拉伸的关系为 [@problem_id:2675215]：
$$ E_i = \frac{1}{2}(\lambda_i^2 - 1) $$
这个关系在小变形情况下 ($\lambda_i \approx 1+\epsilon_i, |\epsilon_i| \ll 1$)，退化为线性应变 $E_i \approx \epsilon_i$。

**[对数应变](@entry_id:751438)张量** (logarithmic strain tensor)，也称 Hencky 应变，定义为 $\boldsymbol{H} = \ln(\boldsymbol{U})$。该张量的定义依赖于张量函数理论，通过对 $\boldsymbol{U}$ 的[谱分解](@entry_id:173707)进行操作：
$$ \boldsymbol{H} = \ln(\boldsymbol{U}) = \sum_{i=1}^3 \ln(\lambda_i)(\boldsymbol{N}_i \otimes \boldsymbol{N}_i) $$
从这个[谱分解](@entry_id:173707)形式可以直接看出，$\boldsymbol{H}$ 的主方向也是 $\boldsymbol{N}_i$，其主值 $H_i$ 为 [@problem_id:2675215]：
$$ H_i = \ln(\lambda_i) $$
[对数应变](@entry_id:751438)具有良好的可加性，因此在某些塑性理论中得到广泛应用。

### 体积-等容分解

任何变形都可以概念上分解为两部分：一部分改变体积（**体积变形**），另一部分只改变形状而不改变体积（**[等容变形](@entry_id:196451)**或畸变）。这种分解在可压缩材料的[本构模型](@entry_id:174726)中至关重要。

变形引起的局部体积变化由变形梯度的[行列式](@entry_id:142978) $J = \det(\boldsymbol{F})$ 描述。由于 $\det(\boldsymbol{R})=1$ 且 $\det(\boldsymbol{U}) = \lambda_1\lambda_2\lambda_3$，我们有 $J = \lambda_1\lambda_2\lambda_3$。

为了分离体积和形状变化，我们引入**修正的** (modified) 或**等容的** (isochoric) 变形量。例如，我们可以将 $\boldsymbol{F}$ 分解为一个纯各向同性膨胀和一个保体积变形的乘积 [@problem_id:2675204]：
$$ \boldsymbol{F} = \boldsymbol{F}_{\mathrm{vol}}\boldsymbol{F}_{\mathrm{iso}} = (J^{1/3}\mathbf{I})(\boldsymbol{R}\bar{\boldsymbol{U}}) $$
其中，体积部分 $\boldsymbol{F}_{\mathrm{vol}} = J^{1/3}\mathbf{I}$ 是一个均匀的、各向同性的缩放，其[行列式](@entry_id:142978)为 $J$。等容部分 $\boldsymbol{F}_{\mathrm{iso}} = J^{-1/3}\boldsymbol{F} = \boldsymbol{R}\bar{\boldsymbol{U}}$ 的[行列式](@entry_id:142978)为 1，它包含了所有的旋转和形状变化。

与此对应，我们定义了**修正右[拉伸张量](@entry_id:193200)** $\bar{\boldsymbol{U}} = J^{-1/3}\boldsymbol{U}$。其[特征值](@entry_id:154894)，即**修正主拉伸** $\bar{\lambda}_i$，满足：
$$ \bar{\lambda}_i = J^{-1/3}\lambda_i \quad \text{且} \quad \bar{\lambda}_1\bar{\lambda}_2\bar{\lambda}_3 = 1 $$
这表明修正主拉伸只描述形状改变，其乘积恒为 1。

对于各向同性[超弹性材料](@entry_id:190241)，其[应变能函数](@entry_id:178435) $\Psi$ 必须是主拉伸的[对称函数](@entry_id:177113)，等价地，是 $\boldsymbol{C}$ 的[主不变量](@entry_id:193522) $I_1, I_2, I_3$ 的函数。通过体积-等容分解，[应变能](@entry_id:162699)可以[解耦](@entry_id:637294)为两部分：
$$ \Psi(I_1, I_2, I_3) = \Psi_{\mathrm{vol}}(J) + \Psi_{\mathrm{iso}}(\bar{I}_1, \bar{I}_2) $$
其中，$\Psi_{\mathrm{vol}}$ 只依赖于体积比 $J=\sqrt{I_3}$。$\Psi_{\mathrm{iso}}$ 描述[畸变能](@entry_id:198925)，它依赖于修正[右柯西-格林张量](@entry_id:174156) $\bar{\boldsymbol{C}} = J^{-2/3}\boldsymbol{C}$ 的[不变量](@entry_id:148850)。这两个[不变量](@entry_id:148850) $\bar{I}_1$ 和 $\bar{I}_2$ 与原始[不变量](@entry_id:148850)的关系为 [@problem_id:2675195, @problem_id:2675204]：
$$ \bar{I}_1 = \mathrm{tr}(\bar{\boldsymbol{C}}) = J^{-2/3}I_1 $$
$$ \bar{I}_2 = \frac{1}{2}[(\mathrm{tr}\bar{\boldsymbol{C}})^2 - \mathrm{tr}(\bar{\boldsymbol{C}}^2)] = J^{-4/3}I_2 $$
由于 $\bar{I}_3 = \det(\bar{\boldsymbol{C}}) = 1$ 是一个常数，[畸变能](@entry_id:198925) $\Psi_{\mathrm{iso}}$ 只需要 $\bar{I}_1$ 和 $\bar{I}_2$ 这两个独立的变量来完整描述。

### 高等议题：计算、简并与敏感性

#### 数值计算：[奇异值分解](@entry_id:138057)

在数值计算中，直接通过求解 $\boldsymbol{C}=\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$ 的[特征值问题](@entry_id:142153)来获得主拉伸平方是不可取的。这是因为计算 $\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$ 会平方 $\boldsymbol{F}$ 的[条件数](@entry_id:145150)，对于病态（ill-conditioned）的 $\boldsymbol{F}$，这可能导致严重的精度损失。

一个数值上更稳健、更精确的方法是直接对变形梯度 $\boldsymbol{F}$ 进行**奇异值分解** (Singular Value Decomposition, SVD) [@problem_id:2675186]：
$$ \boldsymbol{F} = \boldsymbol{U}_{\mathrm{svd}}\boldsymbol{\Sigma}\boldsymbol{V}_{\mathrm{svd}}^{\mathsf{T}} $$
其中 $\boldsymbol{U}_{\mathrm{svd}}$ 和 $\boldsymbol{V}_{\mathrm{svd}}$ 是[正交矩阵](@entry_id:169220)，$\boldsymbol{\Sigma}$ 是一个对角矩阵，其对角元是 $\boldsymbol{F}$ 的[奇异值](@entry_id:152907) $\sigma_i$。[奇异值](@entry_id:152907)被定义为非负的，通常按降序[排列](@entry_id:136432)。

将SVD与极分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$ 联系起来，我们可以发现：
-   主拉伸 $\lambda_i$ 正是 $\boldsymbol{F}$ 的[奇异值](@entry_id:152907) $\sigma_i$。
-   右[拉伸张量](@entry_id:193200) $\boldsymbol{U} = \boldsymbol{V}_{\mathrm{svd}}\boldsymbol{\Sigma}\boldsymbol{V}_{\mathrm{svd}}^{\mathsf{T}}$。
-   [旋转张量](@entry_id:191990) $\boldsymbol{R} = \boldsymbol{U}_{\mathrm{svd}}\boldsymbol{V}_{\mathrm{svd}}^{\mathsf{T}}$。

因此，SVD提供了一个直接、稳定地计算主拉伸、右[拉伸张量](@entry_id:193200)和[旋转张量](@entry_id:191990)的黄金标准方法，完全避免了计算 $\boldsymbol{C}$。

#### 简并情况：主方向的非唯一性

当两个或三个主拉伸值相等时，我们称之为**简并** (degeneracy)。这种情况在物理上对应于具有对称性的变形状态。例如，如果 $\lambda_1 = \lambda_2 \neq \lambda_3$，变形状态具有横观各向同性。

在这种情况下，主方向不再是唯一的。如果 $\lambda_1=\lambda_2=\lambda$，那么与[特征值](@entry_id:154894) $\lambda$ 对应的[特征空间](@entry_id:638014)是一个二维平面。该平面内的**任何**[单位向量](@entry_id:165907)都是一个有效的主方向。我们可以选择该平面内的任意一对[标准正交向量](@entry_id:152061)作为 $\boldsymbol{N}_1$ 和 $\boldsymbol{N}_2$ [@problem_id:2675201]。尽管主方向的选择具有任意性，但这个二维特征[子空间](@entry_id:150286)本身是唯一确定的，其上的正交投影算子 $\boldsymbol{P}$ 也是唯一的。这种情况下，[拉伸张量](@entry_id:193200)可以优雅地写为 $\boldsymbol{U} = \lambda\boldsymbol{P} + \lambda_3(\mathbf{I}-\boldsymbol{P})$ [@problem_id:2675201]。

特别地，如果所有三个主拉伸都相等，$\lambda_1=\lambda_2=\lambda_3=\lambda$，则变形是纯各向同性的（静水压力状态）。此时 $\boldsymbol{U} = \lambda\mathbf{I}$，任何[单位向量](@entry_id:165907)都是[主方向](@entry_id:276187)，任何标准正交三轴系都可以作为主方向基。

需要强调的是，即使主方向不唯一，极分解中的右[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 和[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 仍然是唯一确定的 [@problem_id:2675201]。[主方向](@entry_id:276187)的非唯一性是[特征基](@entry_id:151409)选择的自由度，而不影响张量算子本身的唯一性。

#### [连续性与可微性](@entry_id:160718)

考虑一个沿光滑路径 $t$ 变化的变形过程 $\boldsymbol{F}(t)$。主拉伸和主方向的连续性和可微性表现出一些微妙的特性。

- **主拉伸的连续性**：作为对称矩阵 $\boldsymbol{U}(t)$ 的[特征值](@entry_id:154894)，主拉伸的**无序集合** $\{\lambda_1(t), \lambda_2(t), \lambda_3(t)\}$ 总是随 $t$ 连续变化 [@problem_id:2675208]。然而，如果我们对它们进行排序，例如 $\lambda_{(1)} \ge \lambda_{(2)} \ge \lambda_{(3)}$，这些排序后的函数虽然仍然是连续的，但在主拉伸值发生交叉（即出现简并）的点，它们可能变得不可微，函数图像上表现为“尖点” [@problem_id:2675167]。

- **主方向的连续性**：如果主拉伸始终是互不相同的，那么[主方向](@entry_id:276187)（除去符号）也可以被定义为[连续函数](@entry_id:137361)。然而，当主拉伸发生[交叉](@entry_id:147634)时，例如 $\lambda_{(1)}$ 和 $\lambda_{(2)}$ 在 $t=0$ 时交叉，与排序后的主拉伸 $\lambda_{(1)}(t)$ 和 $\lambda_{(2)}(t)$ 相关联的[主方向](@entry_id:276187) $\boldsymbol{N}_{(1)}(t)$ 和 $\boldsymbol{N}_{(2)}(t)$ 几乎不可避免地会在 $t=0$ 处发生跳跃不连续 [@problem_id:2675208]。这是因为当 $t$ 穿过 0 时，排序会强制交换两个原本光滑演化的[特征向量](@entry_id:151813)分支。

- **函数的[可微性](@entry_id:140863)**：尽管排序后的单个主拉伸在简并点不可微，但一个关键的结论是：**任何关于主拉伸的光滑[对称函数](@entry_id:177113)**，其值对于变形梯度 $\boldsymbol{F}$ 而言是可微的 [@problem_id:2675167]。例如，[不变量](@entry_id:148850) $I_1 = \lambda_1^2 + \lambda_2^2 + \lambda_3^2$ 或在优化中用作 $\lambda_{\max}$ 的平滑代理的函数，如 $p$-均值 $(\sum \lambda_i^p)^{1/p}$，在整个变形空间上都是光滑的。这一性质对于建立能够处理简并情况的、鲁棒的[本构模型](@entry_id:174726)和[优化算法](@entry_id:147840)至关重要。

最后，从数值角度看，当两个主拉伸非常接近时，对应的主方向对微小的扰动会变得极其敏感。其敏感度（或条件数）与主拉伸值之差的倒数成正比 [@problem_id:2675227]。这解释了为什么在简并点附近，数值计算出的主方向可能会剧烈波动。然而，特征[子空间](@entry_id:150286)本身（例如，由两个几乎相等的主拉伸所张成的平面）是稳定的 [@problem_id:2675227]，这再次强调了在理论和计算中处理[子空间](@entry_id:150286)而非单个向量的重要性。