## 引言
在[非线性固体力学](@entry_id:171757)中，分析同时经历大范围[刚体转动](@entry_id:191086)和小尺度材料应变的结构（如柔性机械臂或薄壳的[屈曲](@entry_id:162815)）是一项独特的挑战。传统的线性有限[元理论](@entry_id:638043)在此失效，而完全[非线性](@entry_id:637147)理论虽精确但计算成本高昂。协同转动（Corotational）列式恰好填补了这一空白，为这类“中等转动、小应变”问题提供了一种计算高效且物理上精确的解决方案。

本文旨在全面解析协同转动列式的理论与实践。我们将从第一部分“原理与机制”入手，深入探讨其[运动学分解](@entry_id:751020)、[客观性原理](@entry_id:185412)及核心算法流程。接着，在“应用与跨学科连接”部分，我们将展示该方法在梁、壳[结构分析](@entry_id:153861)、稳定性预测及处理路径依赖材料等方面的广泛应用，并揭示其与[连续介质力学](@entry_id:155125)、[材料科学](@entry_id:152226)的深刻联系。最后，通过“动手实践”环节的一系列引导性问题，您将有机会亲手应用这些知识，巩固对关键概念的理解。通过本次学习，您将掌握一种强大而优雅的[计算力学](@entry_id:174464)工具，能够有效解决工程与科学中的一类重要[非线性](@entry_id:637147)问题。

## 原理与机制

在[非线性固体力学](@entry_id:171757)的有限元分析中，我们经常遇到一类特殊但重要的问题：结构或构件经历了显著的[刚体转动](@entry_id:191086)，但其材料本身的变形（即应变）却很小。典型的例子包括细长梁的弯曲、薄壳的屈曲以及柔性机械臂的运动。对于这类问题，完全线性的有限[元理论](@entry_id:638043)因无法处理大转动而失效，而完全[非线性](@entry_id:637147)的有限[元理论](@entry_id:638043)（例如，基于全拉格朗日或更新[拉格朗日描述](@entry_id:264498)）虽然精确，但计算成本高昂。协同转动（Corotational）列式为这类“中等转动、小应变”问题提供了一种高效且精确的解决方案。本章将深入探讨协同转动列式的基本原理与核心机制。

### 运动的[运动学分解](@entry_id:751020)与[客观性原理](@entry_id:185412)

为了理解协同转动列式的精髓，我们必须首先回到连续介质力学的基本原理。任何物体的运动都可以通过其变形梯度张量 $\mathbf{F}$ 来描述，它将参考构型中的一个无穷小[线元](@entry_id:196833) $\mathrm{d}\mathbf{X}$ 映射到当前构型中的[线元](@entry_id:196833) $\mathrm{d}\mathbf{x}$，即 $\mathrm{d}\mathbf{x} = \mathbf{F} \mathrm{d}\mathbf{X}$。

#### 极分解

极分解定理是[运动学分解](@entry_id:751020)的核心。它指出，任何可逆的变形梯度 $\mathbf{F}$ (假设 $\det \mathbf{F} > 0$ 以保持物理上的合理性) 都可以唯一地分解为一个旋转和一个拉伸的乘积。具体而言，存在两种形式：

1.  **右极分解**: $\mathbf{F} = \mathbf{R}\mathbf{U}$
2.  **左极分解**: $\mathbf{F} = \mathbf{V}\mathbf{R}$

在这里，$\mathbf{R}$ 是一个正常正交张量（$\mathbf{R}^{\mathsf{T}}\mathbf{R}=\mathbf{I}$ 且 $\det \mathbf{R}=+1$），代表了运动中的纯刚体旋转部分。$\mathbf{U}$ 是右[拉伸张量](@entry_id:193200)，而 $\mathbf{V}$ 是左[拉伸张量](@entry_id:193200)，它们都是[对称正定](@entry_id:145886)张量，分别描述了在旋转之前（在参考构型中）和旋转之后（在当前构型中）的纯拉伸变形。它们可以通过格林-柯西张量 $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 和芬格张量 $\mathbf{b} = \mathbf{F}\mathbf{F}^{\mathsf{T}}$ 计算得到，即 $\mathbf{U} = \sqrt{\mathbf{C}}$ 和 $\mathbf{V} = \sqrt{\mathbf{b}}$。这两个[拉伸张量](@entry_id:193200)通过关系 $\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^{\mathsf{T}}$ 相互关联 [@problem_id:2550527]。

这种分解的物理意义在于，它将复杂的变形过程概念化为两步：首先是纯变形（拉伸和剪切），然后是刚体旋转。协同转动列式的基本思想就是利用这种分解，在数值计算中将大刚体旋转 $\mathbf{R}$ 的影响“过滤”掉，从而只处理剩余的“小”变形。在中等转动、小应变的情况下，这意味着[拉伸张量](@entry_id:193200) $\mathbf{U}$ 和 $\mathbf{V}$ 与单位张量 $\mathbf{I}$ 的偏差很小，即使旋转 $\mathbf{R}$ 本身可能代表一个很大的角度 [@problem_id:2550498]。

#### 材料[坐标系](@entry_id:156346)无关性原理 ([客观性原理](@entry_id:185412))

为什么分离[刚体转动](@entry_id:191086)如此重要？答案在于**材料[坐标系](@entry_id:156346)无关性原理**，也称为**[客观性原理](@entry_id:185412)**。该原理要求材料的本构关系（即应力与应变之间的关系）必须独立于观察者的[参考系](@entry_id:169232)。两个[参考系](@entry_id:169232)之间的变换等效于一个附加的刚体运动。形式上，如果一个运动由映射 $\mathbf{x}(\mathbf{X}, t)$ 描述，另一个观察者看到的运动将是 $\mathbf{x}^{\ast}(t) = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}(t)$，其中 $\mathbf{c}(t)$ 是一个平移向量，$\mathbf{Q}(t)$ 是一个正常正交[旋转张量](@entry_id:191990)。

在该变换下，变形梯度、柯西应力等物理量会相应地变换：
$\mathbf{F} \rightarrow \mathbf{F}^{\ast} = \mathbf{Q}\mathbf{F}$
$\boldsymbol{\sigma} \rightarrow \boldsymbol{\sigma}^{\ast} = \mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^{\mathsf{T}}$

[客观性原理](@entry_id:185412)要求本构函数的形式在变换后保持不变。例如，对于一个柯西应力本构函数 $\boldsymbol{\sigma} = \widehat{\boldsymbol{\sigma}}(\mathbf{F})$，它必须满足关系式：
$\widehat{\boldsymbol{\sigma}}(\mathbf{Q}\mathbf{F}) = \mathbf{Q} \widehat{\boldsymbol{\sigma}}(\mathbf{F}) \mathbf{Q}^{\mathsf{T}}$
对于所有正常正交的 $\mathbf{Q}$ 成立 [@problem_id:2550539]。这一要求的一个重要推论是，对于一个[超弹性材料](@entry_id:190241)，其[应变能密度函数](@entry_id:755490) $\Psi$ 只能依赖于变形梯度 $\mathbf{F}$ 中不受[刚体转动](@entry_id:191086)影响的部分，也就是右格林-柯西张量 $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$。即 $\Psi(\mathbf{F}) = \widetilde{\Psi}(\mathbf{C})$。这对于[各向异性材料](@entry_id:184874)和[各向同性材料](@entry_id:170678)都成立，是[客观性原理](@entry_id:185412)的直接结果 [@problem_id:2550539]。

如果一个本构模型不满足客观性，它就会在纯[刚体转动](@entry_id:191086)下产生虚假的、非物理的应力。一个经典的例子是使用简单的材料时间导数来定义的次弹性模型 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{D}$，其中 $\mathbf{D}$ 是变形率张量（[速度梯度](@entry_id:261686)的对称部分）。考虑一个仅承受纯刚体旋转的物体，其[初始应力](@entry_id:750652)为 $\boldsymbol{\sigma}_0$。由于[刚体运动](@entry_id:193355)中没有拉伸，变形率 $\mathbf{D}$ 恒为零。上述天真的[本构模型](@entry_id:174726)会预测 $\dot{\boldsymbol{\sigma}} = \mathbf{0}$，从而 $\boldsymbol{\sigma}(t) = \boldsymbol{\sigma}_0$。然而，物理上正确的应力应该随物体一起旋转，即 $\boldsymbol{\sigma}(t) = \mathbf{Q}(t)\boldsymbol{\sigma}_0\mathbf{Q}^{\mathsf{T}}(t)$。这种不满足客观性的模型错误地预测应力在空间中保持不变，从而导致完全错误的物理结果 [@problem_id:2550518]。这清晰地表明，在处理大转动问题时，必须采用一种能正确处理旋转、保证客观性的列式。

### 协同转动框架的构建

协同转动列式通过在每个有限元上定义一个局部坐标系（即**协同转动[坐标系](@entry_id:156346)**）来系统地满足[客观性原理](@entry_id:185412)。这个局部坐标系随单元的刚体运动一起平移和旋转，因此在该[坐标系](@entry_id:156346)下观察到的变形不包含刚体运动。

#### 协同转动[坐标系](@entry_id:156346)的提取

如何确定这个随动的局部坐标系，尤其是它的旋转 $\mathbf{R}_e$？一种通用且稳健的方法是寻找一个“最佳拟合”的旋转，使得单元的当前构型与经过该旋转后的参考构型之间的差异最小。这可以被形式化为一个最小二乘问题，即所谓的**正交普罗克汝斯问题** (Orthogonal Procrustes problem)。

考虑一个具有 $n$ 个节点的单元，其参考构型中的节点坐标为 $\{\mathbf{X}_i\}_{i=1}^n$，当前构型中的节点坐标为 $\{\mathbf{x}_i\}_{i=1}^n$。我们的目标是找到一个旋转 $\mathbf{R} \in \mathrm{SO}(d)$ 和一个平移 $\mathbf{t} \in \mathbb{R}^d$ ($d$ 为空间维度)，使得加权的平方误差和最小化：
$L(\mathbf{R}, \mathbf{t}) = \sum_{i=1}^n w_i \|\mathbf{x}_i - (\mathbf{R}\mathbf{X}_i + \mathbf{t})\|^2$
其中 $w_i > 0$ 是权重。

通过求解这个[优化问题](@entry_id:266749)，可以证明最优平移 $\mathbf{t}^{\star}$ 使得两个构型的加权质心重合，即 $\mathbf{t}^{\star} = \mathbf{c} - \mathbf{R}^{\star}\mathbf{C}$，其中 $\mathbf{C}$ 和 $\mathbf{c}$ 分别是参考构型和当前构型的加权[质心](@entry_id:265015)。代入此最优平移后，问题简化为寻找最优旋转 $\mathbf{R}^{\star}$，使得迹 $\mathrm{tr}(\mathbf{R}^{\mathsf{T}}\mathbf{H})$ 最大化。这里的 $\mathbf{H}$ 是加权的互[协方差矩阵](@entry_id:139155)：
$\mathbf{H} = \sum_{i=1}^n w_i (\mathbf{x}_i - \mathbf{c})(\mathbf{X}_i - \mathbf{C})^{\mathsf{T}}$

这个最大化问题的解可以通过对 $\mathbf{H}$ 进行[奇异值分解 (SVD)](@entry_id:172448) 得到。若 $\mathbf{H} = \mathbf{U}\boldsymbol{\Sigma}\mathbf{V}^{\mathsf{T}}$，则最优的、保持方向的旋转为：
$\mathbf{R}^{\star} = \mathbf{U}\,\mathrm{diag}(1,\ldots,1,\det(\mathbf{U}\mathbf{V}^{\mathsf{T}}))\,\mathbf{V}^{\mathsf{T}}$
这个公式确保了即使在发生反射的情况下，我们也能得到一个纯旋转矩阵 ($\det \mathbf{R}^{\star}=+1$) [@problem_id:2550523]。这种方法为从任意节点位移中稳健地提取单元的平均刚体旋转提供了一个明确的算法。

#### 旋转的[参数化](@entry_id:272587)

在数值实现中，[三维旋转矩阵](@entry_id:152550) $\mathbf{R} \in \mathrm{SO}(3)$ 有9个分量但只有3个独立自由度。我们需要选择一种[参数化](@entry_id:272587)方法来表示它。常见的选择包括：

-   **[欧拉角](@entry_id:171794) (Euler angles)**: 例如 ZYX 顺序的三个转角。这种方法直观，但存在“[万向节死锁](@entry_id:171734)”（gimbal lock）的奇异性问题，当中间转角为 $\pm 90^{\circ}$ 时，会导致数值不稳定，因此在稳健的有限元程序中应谨慎使用。

-   **旋转矢量 (Rotation vector)**: 用一个三维矢量 $\boldsymbol{\phi}$ 来表示，其方向为[旋转轴](@entry_id:187094)，模长 $|\boldsymbol{\phi}|$ 为旋转角。它是一种最小[参数表示](@entry_id:173803)，通过指数映射 $\mathbf{R} = \exp([\boldsymbol{\phi}])$ 与[旋转矩阵](@entry_id:140302)关联。这种表示在旋转角为 $\pi$ 的整数倍时存在非唯一性，但在[增量更新](@entry_id:750602)的框架下表现稳健，没有类似[万向节死锁](@entry_id:171734)的运动学奇异性。

-   **[单位四元数](@entry_id:204470) (Unit quaternions)**: 使用一个四维矢量 $\mathbf{q}$ 并附加一个单位长度约束 $\|\mathbf{q}\|=1$。[四元数表示](@entry_id:146458)法没有奇异性（除了 $\mathbf{q}$ 和 $-\mathbf{q}$ 代表同一旋转的符号冗余外），并且旋转的复合运算（对应[四元数乘法](@entry_id:154753)）在计算上非常高效。

在协同转动列式中，特别是在需要计算[一致切线刚度矩阵](@entry_id:747734)的场合，**旋转矢量**和**[单位四元数](@entry_id:204470)**通常比[欧拉角](@entry_id:171794)更受欢迎，因为它们能提供更稳健和精确的线性化。这两种方法在每次更新的计算成本上的差异，通常远小于求解全局[方程组](@entry_id:193238)的成本 [@problem_id:2550515]。

### 计算流程与算法

协同转动列式的核心思想是在单元的局部（协同转动）[坐标系](@entry_id:156346)中计算应变和应力，然后将产生的内力转换回[全局坐标系](@entry_id:171029)进行组装。

#### 虚功原理与力的变换

根据**虚功原理**，系统的总[虚功](@entry_id:176403)为零：$\delta \Pi = \sum_{e} ( \delta W_{\text{int},e} - \delta W_{\text{ext},e} ) = 0$。对于单个单元，其[内虚功](@entry_id:172278) $\delta W_{\text{int},e}$ 是一个不依赖于[坐标系](@entry_id:156346)选择的标量。在[全局坐标系](@entry_id:171029)中，它表示为全局节点[虚位移](@entry_id:168781) $\delta \mathbf{u}_e$ 与全局[内力向量](@entry_id:750751) $\mathbf{f}_{\text{int},e}$ 的[点积](@entry_id:149019)：
$\delta W_{\text{int},e} = \delta \mathbf{u}_e^{\mathsf{T}} \mathbf{f}_{\text{int},e}$

在协同转动[坐标系](@entry_id:156346)中，它表示为局部[虚位移](@entry_id:168781) $\delta \hat{\mathbf{u}}_e$ 与局部[内力向量](@entry_id:750751) $\hat{\mathbf{f}}_{\text{int},e}$ 的[点积](@entry_id:149019)：
$\delta W_{\text{int},e} = \delta \hat{\mathbf{u}}_e^{\mathsf{T}} \hat{\mathbf{f}}_{\text{int},e}$

节点位移（及其变分）是从全局到局部的**[协变](@entry_id:634097)**变换，即 $\hat{\mathbf{u}}_e = \mathbf{T}_e \mathbf{u}_e$ 和 $\delta \hat{\mathbf{u}}_e = \mathbf{T}_e \delta \mathbf{u}_e$，其中 $\mathbf{T}_e$ 是由单元旋转 $\mathbf{R}_e$ 构成的块对角变换矩阵。为了保持[虚功](@entry_id:176403)这个标量的不变性，我们必须有：
$\delta \mathbf{u}_e^{\mathsf{T}} \mathbf{f}_{\text{int},e} = (\mathbf{T}_e \delta \mathbf{u}_e)^{\mathsf{T}} \hat{\mathbf{f}}_{\text{int},e} = \delta \mathbf{u}_e^{\mathsf{T}} \mathbf{T}_e^{\mathsf{T}} \hat{\mathbf{f}}_{\text{int},e}$

由于 $\delta \mathbf{u}_e$ 的任意性，我们得到力的变换关系：
$\mathbf{f}_{\text{int},e} = \mathbf{T}_e^{\mathsf{T}} \hat{\mathbf{f}}_{\text{int},e}$

这表明，力作为位移的对偶量，遵循**逆变**变换规则。这就是将局部计算的[内力](@entry_id:167605)转换回[全局坐标系](@entry_id:171029)以进行力平衡计算的正确方式 [@problem_id:2550526]。

#### 牛顿-拉夫逊迭代步骤

在[非线性有限元分析](@entry_id:167596)中，通常采用牛顿-拉夫逊 ([Newton-Raphson](@entry_id:177436)) 方法求解[平衡方程](@entry_id:172166)。对于一个协同转动单元，在每个迭代步中的计算流程如下 [@problem_id:2550485]：

1.  **提取旋转**: 根据当前迭代步的节点位移 $\mathbf{d}^{(i)}$，使用前述方法（如基于SVD的[最小二乘拟合](@entry_id:751226)）计算出单元的刚体旋转 $\mathbf{R}(\mathbf{d}^{(i)})$，并构建[变换矩阵](@entry_id:151616) $\mathbf{T}(\mathbf{R})$。

2.  **计算局部变形**: 将全局节点位移变换到局部坐标系，得到局部节点位移 $\mathbf{d}_{\ell}^{(i)} = \mathbf{T}(\mathbf{R}) \mathbf{d}^{(i)}$。

3.  **局部应变-应力更新**: 使用一个简单的、基于小应变理论的[应变-位移关系](@entry_id:173321)（例如，$\boldsymbol{\varepsilon}_{\ell} = \mathbf{B}_{\ell} \mathbf{d}_{\ell}^{(i)}$）计算局部应变。然后，使用线性本构律（例如，$\boldsymbol{\sigma}_{\ell} = \mathbb{C}:\boldsymbol{\varepsilon}_{\ell}$）更新局部应力。这是协同转动列式计算效率高的关键所在。

4.  **计算并变换内力**: 在局部坐标系中积分得到局部[内力向量](@entry_id:750751) $\mathbf{f}^{\mathrm{int}}_{\ell} = \int \mathbf{B}_{\ell}^{\mathsf{T}} \boldsymbol{\sigma}_{\ell} \mathrm{d}V$。然后，使用逆变变换将其转换回[全局坐标系](@entry_id:171029)：$\mathbf{f}^{\mathrm{int}} = \mathbf{T}(\mathbf{R})^{\mathsf{T}} \mathbf{f}^{\mathrm{int}}_{\ell}$。

5.  **计算[一致切线刚度矩阵](@entry_id:747734)**: 为了实现牛顿-拉夫逊方法的二次收敛性，必须计算**[一致切线刚度矩阵](@entry_id:747734)** $\mathbf{K} = \partial \mathbf{f}^{\mathrm{int}} / \partial \mathbf{d}$。由于全局[内力](@entry_id:167605) $\mathbf{f}^{\mathrm{int}}$ 通过[旋转矩阵](@entry_id:140302) $\mathbf{R}(\mathbf{d})$ 依赖于节点位移 $\mathbf{d}$，其求导变得复杂。使用链式法则，[切线刚度矩阵](@entry_id:170852)通常包含三个部分：
    -   旋转后的**[材料刚度](@entry_id:158390)矩阵**：$\mathbf{T}^{\mathsf{T}} \mathbf{K}^{\mathrm{mat}}_{\ell} \mathbf{T}$
    -   旋转后的**[几何刚度矩阵](@entry_id:162967)**（或初应力刚度矩阵）：$\mathbf{T}^{\mathsf{T}} \mathbf{K}^{\mathrm{geo}}_{\ell} \mathbf{T}$
    -   由[旋转矩阵](@entry_id:140302)对位移的导数产生的附加项，这些项描述了[内力](@entry_id:167605)随旋转变化的效应。
    忽略任何一项都会破坏二次收敛性，并可能导致数值不稳定。

6.  **组装与求解**: 将单元的[内力向量](@entry_id:750751)和[切线刚度矩阵](@entry_id:170852)组装到全局系统中，形成全局[残差向量](@entry_id:165091)和[切线刚度矩阵](@entry_id:170852)，然后求解线性方程组得到位移增量，更新节点位移并进入下一次迭代。

### 局限性与讨论

尽管协同转动列式非常强大，但理解其适用范围和局限性至关重要。

#### 局部[大应变](@entry_id:751152)下的失效

协同转动列式的核心假设是“小应变”，但这指的是**局部坐标系**中的应变。如果材料本身经历了大的塑性变形或在应力集中区域产生了大的弹性应变，那么即使整体转动是中等的，局部应变也可能变得很大（例如，超过5-10%）。在这种情况下，基于小应变理论的局部[运动学](@entry_id:173318)（如应变的加法分解）和本构模型将不再有效 [@problem_id:2550514]。

具体来说，当局部应变很大时：
-   线性化的[应变-位移关系](@entry_id:173321)不再精确。
-   在塑性力学中，应变率的加法分解 ($\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p$) 失去其[运动学](@entry_id:173318)基础。正确的描述应基于变形梯度的[乘法分解](@entry_id:199514) ($\mathbf{F} = \mathbf{F}_e \mathbf{F}_p$)。
-   （应力，应变）对的能量共轭关系被破坏，违反了[热力学一致性](@entry_id:138886)。

因此，当预期有大的局部应变时，必须在协同转动框架内采用一个完全的有限应变[本构模型](@entry_id:174726)，而不是简单的小应变模型。协同转动框架仍然可以有效地处理[刚体转动](@entry_id:191086)，但其内部的“引擎”需要升级 [@problem_id:2550514] [@problem_id:2550498]。

#### 无法解决闭锁问题

另一个常见的误解是认为协同转动列式可以解决**剪切闭锁 (shear locking)** 或**膜闭锁 (membrane locking)** 问题。闭锁是由于单元的[插值函数](@entry_id:262791)无法精确表示某些变形模式（如薄梁或薄壳中的零剪切[纯弯曲](@entry_id:202969)）而导致的数值刚度过大现象。

闭锁本质上是一个**插值问题**，与单元的插值阶次和约束条件的离散表示有关。协同转动列式处理的是运动学中的**[刚体转动](@entry_id:191086)**部分，它并不改变单元的[插值函数](@entry_id:262791)或其[应变-位移矩阵](@entry_id:163451)的内在属性。因此，一个在小位移下会发生闭锁的单元，在协同转动框架下，当它经历大转动时，同样会在其[局部坐标系](@entry_id:751394)中表现出闭锁行为。要解决闭锁，必须采用诸如[减缩积分](@entry_id:167949)、选择性积分、或混合/增强应变格式等专门技术。这些技术可以与协同转动列式结合使用，但协同转动本身并不能治愈闭锁 [@problem_id:2550544]。

总而言之，协同转动列式是一种优雅而高效的工具，它通过将[刚体转动](@entry_id:191086)与局部小变形分离，成功地将线性、小应变单元的简单性扩展到了大转动、小应变问题的分析中。然而，用户必须清楚其核心假设和局限性，确保其在适用的物理场景中得到正确的应用。