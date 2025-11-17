## 引言
在[连续介质力学](@entry_id:155125)中，材料的变形通常是体积改变与形状改变同时发生的复杂过程。为了精确地描述、量化并建立这两类变形模式的物理模型，将[应变张量分解](@entry_id:184653)为其体积（球形）部分和偏量部分，是一种基础而极其重要的分析方法。这种分解不仅在理论上具有优雅的数学结构，更在工程实践中为理解和预测材料行为提供了深刻的洞察力。本文旨在系统性地阐述这一核心概念，填补从理论定义到实际应用之间的知识鸿沟。

为实现这一目标，本文将分为三个核心章节。在第一章 **“原理与机制”** 中，我们将深入探讨该分解的数学基础，从线性小应变理论出发，建立其运动学定义、[不变性](@entry_id:140168)以及与能量的内在联系，并将其推广至更为普适的[有限应变理论](@entry_id:176941)框架。接着，在第二章 **“应用与跨学科联系”** 中，我们将展示这一理论工具的巨大威力，考察它如何成为建立塑性、粘弹性等非弹性[本构模型](@entry_id:174726)的基石，并揭示其在计算力学领域（尤其是在有限元法中）解决关键数值问题的核心作用。最后，在 **“动手实践”** 章节中，通过一系列精心设计的练习，您将有机会亲手应用所学知识，巩固并深化对概念的理解。

通过本次学习，您将掌握一个贯穿于现代固体力学的强大分析工具，并理解为何区分体积变化与形状变化对于[材料建模](@entry_id:751724)与数值分析至关重要。让我们从第一章开始，探索体积与偏量[应变分解](@entry_id:186005)的基本原理。

## 原理与机制

在连续介质力学中，材料的变形是一个复杂的现象，可以被视为体积改变和形状改变的叠加。为了对这些不同的变形模式进行精确的量化和建模，将[应变张量分解](@entry_id:184653)为体积[部分和](@entry_id:162077)偏量部分是一种基本而强大的方法。本章将从基本原理出发，系统地阐述这种分解的[运动学](@entry_id:173318)基础、本构意义及其在有限变形理论中的推广。

### 小应变理论中的基本分解

对于小变形问题，我们使用线性化的应变张量 $\boldsymbol{\varepsilon}$ 来描述材料的局部变形，其定义为[位移梯度](@entry_id:165352) $\nabla \mathbf{u}$ 的对称部分：$\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\mathsf{T}})$。

#### [体积应变](@entry_id:267252)与[偏应变](@entry_id:201263)的定义

变形过程中的局部体积变化由变形梯度 $\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$ 的[行列式](@entry_id:142978) $J = \det \mathbf{F}$ 描述。在小应变假设下（即 $\nabla \mathbf{u}$ 的分量远小于1），[行列式](@entry_id:142978)可以进行[一阶近似](@entry_id:147559)：$J \approx 1 + \mathrm{tr}(\nabla \mathbf{u})$。由于应变张量的迹等于[位移梯度](@entry_id:165352)的迹，即 $\mathrm{tr}(\boldsymbol{\varepsilon}) = \mathrm{tr}(\nabla \mathbf{u})$，因此，相对体积变化 $\frac{\Delta V}{V_0} = J - 1$ 近似等于[应变张量](@entry_id:193332)的迹。

基于此，我们定义 **[体积应变](@entry_id:267252)** (volumetric strain) 为[应变张量](@entry_id:193332)的迹，记为 $\varepsilon_v = \mathrm{tr}(\boldsymbol{\varepsilon})$。这个标量代表了材料单元纯粹的[体积膨胀](@entry_id:144241)或压缩。

为了将体积变化从总应变中分离出来，我们将[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 分解为一个球形（或体积）[部分和](@entry_id:162077)一个偏（或形状）部分。球形部分在所有方向上都引起相同的拉伸或压缩，因此它必须是一个与单位张量 $\mathbf{I}$ 成正比的[各向同性张量](@entry_id:195105)。为了保持一致性，我们将该部分定义为平均[正应变](@entry_id:204633)乘以单位张量，即 $\boldsymbol{\varepsilon}_{\text{vol}} = \frac{1}{3}\mathrm{tr}(\boldsymbol{\varepsilon})\mathbf{I}$。这里的系数 $\frac{1}{3}$ 确保了在三维空间中，该[张量的迹](@entry_id:190669)等于总体积应变 $\mathrm{tr}(\boldsymbol{\varepsilon})$。

**偏应变张量** (deviatoric strain tensor) $\boldsymbol{\varepsilon}'$ 则定义为总应变减去其球形部分：
$$
\boldsymbol{\varepsilon}' = \boldsymbol{\varepsilon} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\varepsilon})\mathbf{I}
$$
通过对上式取迹，我们可以立即验证偏应变[张量的迹](@entry_id:190669)恒为零：$\mathrm{tr}(\boldsymbol{\varepsilon}') = \mathrm{tr}(\boldsymbol{\varepsilon}) - \mathrm{tr}(\frac{1}{3}\mathrm{tr}(\boldsymbol{\varepsilon})\mathbf{I}) = \mathrm{tr}(\boldsymbol{\varepsilon}) - \frac{1}{3}\mathrm{tr}(\boldsymbol{\varepsilon}) \cdot 3 = 0$。一个迹为零的应变状态在物理上对应于一个保持体积不变的纯形状改变（畸变）。因此，这个分解 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_{\text{vol}} + \boldsymbol{\varepsilon}'$ 唯一地将任何小应变状态分解为一个引起体积变化的纯球形应变和一个引起形状变化的纯[偏应变](@entry_id:201263) [@problem_id:2917866]。

为了建立直观理解，我们考虑一个均匀膨胀的位移场 $\mathbf{u}(x,y,z) = (\epsilon x, \epsilon y, \epsilon z)$，其中 $|\epsilon| \ll 1$。其[位移梯度](@entry_id:165352)为 $\nabla \mathbf{u} = \epsilon \mathbf{I}$，这是一个[对称张量](@entry_id:148092)，因此应变张量就是 $\boldsymbol{\varepsilon} = \epsilon \mathbf{I}$。这是一个纯球形应变张量。它的迹为 $\mathrm{tr}(\boldsymbol{\varepsilon}) = 3\epsilon$，这与线性化的体积变化 $\theta = 3\epsilon$ 完全一致。根据定义计算其[偏应变](@entry_id:201263)部分：
$$
\boldsymbol{\varepsilon}' = \boldsymbol{\varepsilon} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\varepsilon})\mathbf{I} = \epsilon\mathbf{I} - \frac{1}{3}(3\epsilon)\mathbf{I} = \epsilon\mathbf{I} - \epsilon\mathbf{I} = \mathbf{0}
$$
这表明该变形完全是体[积性](@entry_id:187940)的，不包含任何形状改变，这与我们对均匀膨胀的物理直觉相符 [@problem_id:2710026]。

值得强调的是，[体积应变](@entry_id:267252)的大小并不能约束[偏应变](@entry_id:201263)的大小。一个变形可以有极小的体积变化，但同时经历剧烈的形状扭曲。例如，我们可以构造一个[应变张量](@entry_id:193332)序列，其迹保持为一个很小的常数 $\delta$，但其[偏应变](@entry_id:201263)部分的范数可以任意大。这说明[体积应变和偏应变](@entry_id:197710)在描述变形时是[相互独立](@entry_id:273670)的度量 [@problem_id:2709969]。这一点对于理解塑性力学中的屈服现象至关重要，因为材料的屈服通常是由[偏应力](@entry_id:163323)（与[偏应变](@entry_id:201263)共轭）达到临界值引起的，而与体积应力关系不大。

### [不变性](@entry_id:140168)、正交性与普适性

物理定律不应依赖于观察者所选择的[坐标系](@entry_id:156346)。[体积-偏量分解](@entry_id:183756)的优美之处在于其良好的坐标变换性质。

[体积应变](@entry_id:267252) $\mathrm{tr}(\boldsymbol{\varepsilon})$ 是一个[标量不变量](@entry_id:193787)。在任意[正交坐标](@entry_id:166074)变换下（由正交张量 $\mathbf{Q}$ 代表，$\mathbf{Q}\mathbf{Q}^{\mathsf{T}}=\mathbf{I}$），[应变张量变换](@entry_id:187049)为 $\boldsymbol{\varepsilon}^{\star} = \mathbf{Q}\boldsymbol{\varepsilon}\mathbf{Q}^{\mathsf{T}}$。新[坐标系](@entry_id:156346)下的迹为：
$$
\mathrm{tr}(\boldsymbol{\varepsilon}^{\star}) = \mathrm{tr}(\mathbf{Q}\boldsymbol{\varepsilon}\mathbf{Q}^{\mathsf{T}}) = \mathrm{tr}(\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\boldsymbol{\varepsilon}) = \mathrm{tr}(\mathbf{I}\boldsymbol{\varepsilon}) = \mathrm{tr}(\boldsymbol{\varepsilon})
$$
这证明了[体积应变](@entry_id:267252)是一个不随[坐标系](@entry_id:156346)选择而改变的客观物理量。同时，偏应变张量作为一个[二阶张量](@entry_id:199780)，其变换规律是协变的，即 $\boldsymbol{\varepsilon}'^{\star} = \mathbf{Q}\boldsymbol{\varepsilon}'\mathbf{Q}^{\mathsf{T}}$ [@problem_id:2917866]。

这个分解可以更抽象地理解为在一个张量空间内的正交投影。对于 $n$ 维空间中的任意[二阶张量](@entry_id:199780) $\mathbf{A}$，我们可以定义一个球形部分 $A_{\text{vol}} = \frac{\mathrm{tr}(\mathbf{A})}{n}\mathbf{I}$ 和一个偏量部分 $A' = \mathbf{A} - A_{\text{vol}}$。在[弗罗贝尼乌斯内积](@entry_id:153693)（$A:B = \mathrm{tr}(A^{\mathsf{T}}B)$）的定义下，所有球形张量构成的[子空间](@entry_id:150286)与所有[偏张量](@entry_id:185837)（迹为零的张量）构成的[子空间](@entry_id:150286)是正交的。因此，这个分解是一个[正交分解](@entry_id:148020)，并满足毕达哥拉斯定理：
$$
\lVert \mathbf{A} \rVert^{2} = \lVert \mathbf{A}_{\text{vol}} \rVert^{2} + \lVert \mathbf{A}' \rVert^{2}
$$
这个普适的框架引出了一个在建模时必须注意的关键点：维度 $n$ 的选择。在处理一个三维物体的 **[平面应变](@entry_id:167046)** 问题时，尽管[运动学](@entry_id:173318)被限制在二维平面内，但其应力[状态和](@entry_id:193625)体积响应本质上是三维的，因此分解时必须使用 $n=3$。然而，对于一个真正的二维连续体（如石墨烯或薄膜），其物理空间就是二维的，“体积”变化实际上是面积变化，因此应使用 $n=2$ [@problem_id:2709994]。

### 本构与能量的[解耦](@entry_id:637294)

[体积-偏量分解](@entry_id:183756)的威力在考察材料本构关系时表现得淋漓尽致。对于一个[各向同性线弹性](@entry_id:185899)材料，其[应力-应变关系](@entry_id:274093)（[胡克定律](@entry_id:149682)）为：
$$
\boldsymbol{\sigma} = \lambda(\mathrm{tr}\boldsymbol{\varepsilon})\mathbf{I} + 2\mu\boldsymbol{\varepsilon}
$$
其中 $\lambda$ 和 $\mu$ 是拉梅参数。将[应变分解](@entry_id:186005) $\boldsymbol{\varepsilon} = \frac{1}{3}(\mathrm{tr}\boldsymbol{\varepsilon})\mathbf{I} + \boldsymbol{\varepsilon}'$ 代入上式，并对结果进行重新整理，我们可以得到应力的分解形式：
$$
\boldsymbol{\sigma} = \left(\lambda + \frac{2}{3}\mu\right)(\mathrm{tr}\boldsymbol{\varepsilon})\mathbf{I} + 2\mu\boldsymbol{\varepsilon}'
$$
如果我们对[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 也进行同样的分解，令其球形部分为平均应力 $p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$，[偏应力](@entry_id:163323)部分为 $\mathbf{s} = \boldsymbol{\sigma} - p\mathbf{I}$，那么通过比较上述方程的两边，我们可以得到两组完全解耦的[本构关系](@entry_id:186508)：
1.  **体积响应**: $p = K \cdot \mathrm{tr}(\boldsymbol{\varepsilon})$，其中 $K = \lambda + \frac{2}{3}\mu$ 是[体积模量](@entry_id:160069)。
2.  **形状响应**: $\mathbf{s} = 2\mu \boldsymbol{\varepsilon}'$，其中 $\mu$ 是[剪切模量](@entry_id:167228)。

这个结果表明，对于各向同性材料，[体积应变](@entry_id:267252)仅由[静水压力](@entry_id:275365)（平均应力）引起，而形状改变（[偏应变](@entry_id:201263)）仅由偏应力引起。两者之间没有耦合。这正是“[偏应力](@entry_id:163323)主导形状改变”这一论断的精确数学表述。需要强调的是，这种解耦是 **材料各向同性** 的直接结果，而非普适的[运动学](@entry_id:173318)规律。对于各向异性材料，静水压力完全可能引起[剪切变形](@entry_id:170920) [@problem_id:2920794]。

这种[解耦](@entry_id:637294)也反映在[应变能密度函数](@entry_id:755490) $\psi$ 上。对于[各向同性线弹性](@entry_id:185899)体，其[应变能密度](@entry_id:200085)为 $\psi = \frac{\lambda}{2}(\mathrm{tr}\boldsymbol{\varepsilon})^{2} + \mu\boldsymbol{\varepsilon}:\boldsymbol{\varepsilon}$。利用分解的正交性，$\boldsymbol{\varepsilon}:\boldsymbol{\varepsilon} = \frac{1}{3}(\mathrm{tr}\boldsymbol{\varepsilon})^2 + \boldsymbol{\varepsilon}':\boldsymbol{\varepsilon}'$，我们可以将能量函数重写为：
$$
\psi(\boldsymbol{\varepsilon}) = \frac{K}{2}(\mathrm{tr}\boldsymbol{\varepsilon})^{2} + \mu(\boldsymbol{\varepsilon}':\boldsymbol{\varepsilon}') = \psi_{\text{vol}} + \psi_{\text{dev}}
$$
[应变能](@entry_id:162699)被完美地分解为仅依赖于体积变化的体积能 $\psi_{\text{vol}}$ 和仅依赖于形状变化的[畸变能](@entry_id:198925) $\psi_{\text{dev}}$ [@problem_id:2688026]。

### 向[有限应变理论](@entry_id:176941)的推广

在有限变形中，应变的叠加性不再成立，我们需要采用[乘法分解](@entry_id:199514)。

#### 变形梯度的[乘法分解](@entry_id:199514)

变形梯度 $\mathbf{F}$ 本身可以被[乘法分解](@entry_id:199514)为一个纯[体积膨胀](@entry_id:144241)[部分和](@entry_id:162077)一个保体积（等容）变形部分。令 $J = \det \mathbf{F}$，我们可以定义一个唯一的分解：
$$
\mathbf{F} = (J^{1/3}\mathbf{I}) \bar{\mathbf{F}}
$$
这里，$J^{1/3}\mathbf{I}$ 是一个球形张量，代表均匀的体积膨胀。$\bar{\mathbf{F}} = J^{-1/3}\mathbf{F}$ 是[等容变形](@entry_id:196451)梯度，其[行列式](@entry_id:142978)为 $\det \bar{\mathbf{F}} = (J^{-1/3})^3 \det \mathbf{F} = 1$。从[李群](@entry_id:137659)的角度看，这对应于将属于[一般线性群](@entry_id:141275) $\mathrm{GL}^{+}(3)$ 的 $\mathbf{F}$ 分解为一个属于正扩张群 $\mathcal{D}^{+}$ 的元素和一个属于[特殊线性群](@entry_id:139538) $\mathrm{SL}(3)$ 的元素 [@problem_id:2710032]。

#### 基于应变张量的分解与客观性

在建立本构模型时，使用[应变张量](@entry_id:193332)通常更为方便。通过极分解 $\mathbf{F} = \mathbf{R}\mathbf{U}$，变形可以分解为拉伸（由对称正定的右[拉伸张量](@entry_id:193200) $\mathbf{U}$ 描述）和旋转（由转动张量 $\mathbf{R}$ 描述）。基于此，我们定义右柯西-格林[应变张量](@entry_id:193332) $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{U}^2$。

为了分离体积效应，我们对 $\mathbf{C}$ 进行修正，定义 **等容[右柯西-格林张量](@entry_id:174156)**：
$$
\bar{\mathbf{C}} = J^{-2/3}\mathbf{C}
$$
可以验证 $\det \bar{\mathbf{C}} = (J^{-2/3})^3 \det \mathbf{C} = J^{-2} \cdot J^2 = 1$。类似地，也可以定义等容右[拉伸张量](@entry_id:193200) $\bar{\mathbf{U}} = J^{-1/3}\mathbf{U}$。这两个张量仅包含关于形状改变的信息 [@problem_id:2709999]。

这个框架的关键优势在于 **客观性**（或称观察者无关性）。物理上合理的[本构关系](@entry_id:186508)不应随观察者的刚体运动而改变。在数学上，这意味着在变形梯度上叠加一个任意的刚性转动 $\mathbf{F} \to \mathbf{Q}\mathbf{F}$（其中 $\mathbf{Q}$ 是转动张量）时，本构关系中的变量应保持不变。可以证明，$J$, $\mathbf{U}$ 和 $\mathbf{C}$ 都是客观的，因此它们的等容版本 $\bar{\mathbf{U}}$ 和 $\bar{\mathbf{C}}$ 也是客观的。这就解释了为什么在现代超弹性理论中，[应变能函数](@entry_id:178435)通常写成如下形式：
$$
W(\mathbf{F}) = \Psi_{\text{vol}}(J) + \Psi_{\text{iso}}(\bar{\mathbf{C}})
$$
这种形式的能量函数自动满足[客观性原理](@entry_id:185412)，并且清晰地分离了材料对体积变化和形状变化的响应 [@problem_id:2709977]。这一原理同样适用于应力，推导出的[基尔霍夫应力](@entry_id:751039)张量也自然地分解为一个球形[部分和](@entry_id:162077)一个偏量部分 [@problem_id:2920794]。

### 计算力学中的[矩阵表示](@entry_id:146025)

在[有限元分析](@entry_id:138109)等计算方法中，为了方便数值计算，对称的二阶张量通常用一个列[向量表示](@entry_id:166424)，即 **Voigt 表示法**。例如，一个三维对称应变张量可以表示为一个 $6 \times 1$ 的向量 $\mathbf{v}(\boldsymbol{\varepsilon}) = (\varepsilon_{11}, \varepsilon_{22}, \varepsilon_{33}, \varepsilon_{23}, \varepsilon_{13}, \varepsilon_{12})^{\mathsf{T}}$。

在这种表示下，[偏应变](@entry_id:201263)投影操作 $\boldsymbol{\varepsilon} \to \boldsymbol{\varepsilon}'$ 可以通过一个 $6 \times 6$ 的矩阵 $\mathbf{P}_{\text{dev}}$ 来实现，即 $\mathbf{v}(\boldsymbol{\varepsilon}') = \mathbf{P}_{\text{dev}} \mathbf{v}(\boldsymbol{\varepsilon})$。通过前述的分解定义，可以推导出这个 **[偏应变](@entry_id:201263)[投影矩阵](@entry_id:154479)** 的具体形式：
$$
\mathbf{P}_{\text{dev}} =
\begin{pmatrix}
\frac{2}{3}  -\frac{1}{3}  -\frac{1}{3}  0  0  0 \\
-\frac{1}{3}  \frac{2}{3}  -\frac{1}{3}  0  0  0 \\
-\frac{1}{3}  -\frac{1}{3}  \frac{2}{3}  0  0  0 \\
0  0  0  1  0  0 \\
0  0  0  0  1  0 \\
0  0  0  0  0  1
\end{pmatrix}
$$
这个矩阵是一个[投影算子](@entry_id:154142)，因此它具有 **[幂等性](@entry_id:190768)**，即 $\mathbf{P}_{\text{dev}}^2 = \mathbf{P}_{\text{dev}}$。这在物理上意味着对一个已经是偏量的张量再次进行偏量投影，结果不会改变。这个矩阵在[弹塑性](@entry_id:193198)[本构模型](@entry_id:174726)的数值实现中扮演着核心角色 [@problem_id:2710030]。