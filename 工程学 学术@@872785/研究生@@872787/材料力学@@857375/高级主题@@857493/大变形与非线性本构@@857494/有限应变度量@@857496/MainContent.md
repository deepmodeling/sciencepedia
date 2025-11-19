## 引言
在工程与科学实践中，许多材料（如橡胶、生物软组织和经历塑性成形的金属）会经受巨大的变形，其位移、转动和应变远超出了经典小应变理论的适用范畴。在这些情况下，线性化的[运动学](@entry_id:173318)假设不再成立，必须采用更为严谨的[有限应变理论](@entry_id:176941)。然而，描述大变形的核心挑战在于如何精确地区分材料的真实形状改变（应变）与不产生[内力](@entry_id:167605)的[刚体运动](@entry_id:193355)（平移和转动）。本文旨在系统地解决这一问题，为读者构建一个关于有限[应变度量](@entry_id:755495)的完整知识体系。

本文将分为三个核心章节。在“原理和机制”中，我们将从最基本的变形梯度出发，引入极分解定理，并在此基础上定义和比较一系列关键的有限应变张量，如柯西-格林张量、[格林-拉格朗日应变](@entry_id:170427)、[欧拉-阿尔曼西应变](@entry_id:187104)及[亨基应变](@entry_id:191329)，同时探讨[客观性原理](@entry_id:185412)和[功共轭](@entry_id:194957)关系。接着，在“应用与交叉学科联系”一章，我们将展示这些理论工具如何在材料本构模型（超弹性、[弹塑性](@entry_id:193198)）、计算力学、[生物力学](@entry_id:153973)和[固态物理学](@entry_id:142261)等领域中发挥关键作用。最后，通过“动手实践”部分提供的具体问题，您将有机会亲手计算和分析这些[应变度量](@entry_id:755495)，从而加深理解。通过本文的学习，您将掌握分析和建模[大变形](@entry_id:167243)问题的核心运动学工具。

## 原理和机制

在连续介质力学中，描述物体从初始（参考）构型到当前（变形后）构型的[大变形](@entry_id:167243)过程需要一套严谨的运动学框架。与仅适用于微小位移和转动的小应变理论不同，[有限应变理论](@entry_id:176941)必须能够精确处理任意大小的拉伸、压缩、剪切和[刚体转动](@entry_id:191086)。本章将系统地阐述描述有限变形的核心[运动学](@entry_id:173318)量，定义和比较主要的有限[应变张量](@entry_id:193332)，并探讨它们在能量原理、本构关系和计算力学中的作用机制。

### 变形梯度

描述有限变形的出发点是**运动**（motion）映射，它定义了物体中每个物[质点](@entry_id:186768)从其在**参考构型** $\mathcal{B}_0$ 中的位置 $\boldsymbol{X}$ 到其在**当前构型** $\mathcal{B}_t$ 中的位置 $\boldsymbol{x}$ 的对应关系：$\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)$。

为了量化变形在局部是如何发生的，我们引入一个核心的运动学量：**变形梯度**（deformation gradient）张量 $\boldsymbol{F}$。它被定义为当前位置 $\boldsymbol{x}$ 相对于[参考位](@entry_id:754187)置 $\boldsymbol{X}$ 的梯度：

$$
\boldsymbol{F} = \frac{\partial \boldsymbol{\chi}}{\partial \boldsymbol{X}} = \nabla_{\boldsymbol{X}} \boldsymbol{\chi}
$$

变形梯度的物理意义在于它是一个[线性映射](@entry_id:185132)，将参考构型中一个无穷小的物质[线元](@entry_id:196833) $d\boldsymbol{X}$ 变换为当前构型中对应的空间[线元](@entry_id:196833) $d\boldsymbol{x}$。由定义可知，这个关系可以表示为 [@problem_id:2886622]：

$$
d\boldsymbol{x} = \boldsymbol{F} \, d\boldsymbol{X}
$$

从这个定义可以看出，$\boldsymbol{F}$ 捕捉了物[质点](@entry_id:186768)邻域内变形的全部局部信息，包括拉伸和旋转。$\boldsymbol{F}$ 是一个**两点张量**（two-point tensor），因为它将一个属于参考构型切空间 $T_X \mathcal{B}_0$ 的向量 $d\boldsymbol{X}$ 映射到当前构型切空间 $T_x \mathcal{B}_t$ 的向量 $d\boldsymbol{x}$ [@problem_id:2886622]。

变形梯度也描述了体积的局部变化。一个无穷小的参考[体元](@entry_id:267802) $dV$ 经过变形后，其当前[体元](@entry_id:267802) $dv$ 的大小由下式给出：

$$
dv = J \, dV
$$

其中 $J = \det \boldsymbol{F}$ 是变形梯度的[行列式](@entry_id:142978)，被称为**雅可比行列式**（Jacobian determinant）。对于物理上可能的变形，物质不能相互穿透，因此要求 $J > 0$。这个条件保证了变形是保定向的 [@problem_id:2886622]。

### 极分解：分离转动与拉伸

变形梯度 $\boldsymbol{F}$ 同时包含了拉伸（改变形状和尺寸）与旋转（改变方向）的信息。为了将这两种效应[解耦](@entry_id:637294)，**极分解定理**（polar decomposition theorem）指出，任何具有正[行列式](@entry_id:142978)的可逆张量 $\boldsymbol{F}$ 都可以唯一地分解为两种形式 [@problem_id:2640372]：

1.  **右极分解**：$\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$
2.  **左极分解**：$\boldsymbol{F} = \boldsymbol{V}\boldsymbol{R}$

其中：
- $\boldsymbol{R}$ 是一个**纯[旋转张量](@entry_id:191990)**，属于[特殊正交群](@entry_id:146418) $\mathrm{SO}(3)$，满足 $\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R} = \boldsymbol{I}$ 且 $\det \boldsymbol{R} = 1$。
- $\boldsymbol{U}$ 是**右[拉伸张量](@entry_id:193200)**（right stretch tensor），它是一个对称正定（SPD）张量。
- $\boldsymbol{V}$ 是**左[拉伸张量](@entry_id:193200)**（left stretch tensor），它也是一个对称正定张量。

右极分解的物理解释是，一个局部变形过程可以看作是先在参考构型中进行纯拉伸（由 $\boldsymbol{U}$ 描述），然后再进行刚体旋转（由 $\boldsymbol{R}$ 描述）。而左极分解则可以看作是先进行同样的刚体旋转，然后再在当前构型中进行纯拉伸（由 $\boldsymbol{V}$ 描述）。

两个[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 和 $\boldsymbol{V}$ 以及[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 之间存在密切联系。通过联立两种分解形式，可以得到 $\boldsymbol{V} = \boldsymbol{R}\boldsymbol{U}\boldsymbol{R}^{\mathsf{T}}$ [@problem_id:2640372]。这表明 $\boldsymbol{V}$ 是 $\boldsymbol{U}$ 的一个相似变换，因此它们拥有相同的[特征值](@entry_id:154894)。这些[特征值](@entry_id:154894)被称为**主拉伸**（principal stretches），记为 $\lambda_i$（$i=1, 2, 3$）。主拉伸量化了在三个相互正交的方向上材料纤维的伸长或缩短程度。这些方向被称为**主方向**（principal directions），它们是[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 和 $\boldsymbol{V}$ 的[特征向量](@entry_id:151813)。特别地，$\boldsymbol{U}$ 的[特征向量](@entry_id:151813)（记为 $\boldsymbol{N}_i$）定义了参考构型中的主方向，而 $\boldsymbol{V}$ 的[特征向量](@entry_id:151813)（记为 $\boldsymbol{n}_i$）定义了当前构型中的主方向，它们之间的关系为 $\boldsymbol{n}_i = \boldsymbol{R}\boldsymbol{N}_i$ [@problem_id:2640415]。

### 柯西-格林变形张量

应变的本质是衡量变形引起的长度和角度的变化，而不是刚体运动。因此，一个合理的[应变度量](@entry_id:755495)应该只与[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 或 $\boldsymbol{V}$ 有关，而与[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 无关。

我们可以通过比较变形前后线元平方长度的变化来构建这样的度量。一个物质[线元](@entry_id:196833) $d\boldsymbol{X}$ 的初始平方长度为 $dS^2 = d\boldsymbol{X} \cdot d\boldsymbol{X}$。变形后，其对应的空间线元 $d\boldsymbol{x} = \boldsymbol{F}d\boldsymbol{X}$ 的平方长度为：

$$
ds^2 = d\boldsymbol{x} \cdot d\boldsymbol{x} = (\boldsymbol{F}d\boldsymbol{X}) \cdot (\boldsymbol{F}d\boldsymbol{X}) = d\boldsymbol{X}^{\mathsf{T}} \boldsymbol{F}^{\mathsf{T}} \boldsymbol{F} d\boldsymbol{X}
$$

这启发我们定义一个只依赖于变形的纯拉伸部分的张量。**右柯西-格林变形张量**（right Cauchy-Green deformation tensor）$\boldsymbol{C}$ 定义为：

$$
\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}
$$

利用极分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$，我们发现 $\boldsymbol{C} = (\boldsymbol{R}\boldsymbol{U})^{\mathsf{T}}(\boldsymbol{R}\boldsymbol{U}) = \boldsymbol{U}^{\mathsf{T}}\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}\boldsymbol{U} = \boldsymbol{U}^2$。这表明 $\boldsymbol{C}$ 完全由右[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 决定，与旋转无关。它是一个定义在参考构型上的**物质张量**（material tensor）。它的[特征值](@entry_id:154894)是主拉伸的平方，即 $\lambda_i^2$ [@problem_id:2886612, 2640415]。

类似地，我们可以定义一个与当前构型相关的张量。**左柯西-格林变形张量**（left Cauchy-Green deformation tensor）$\boldsymbol{b}$ 定义为：

$$
\boldsymbol{b} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}
$$

利用极分解 $\boldsymbol{F}=\boldsymbol{V}\boldsymbol{R}$，可得 $\boldsymbol{b} = \boldsymbol{V}^2$。这表明 $\boldsymbol{b}$ 完全由左[拉伸张量](@entry_id:193200) $\boldsymbol{V}$ 决定。它是一个定义在当前构型上的**[空间张量](@entry_id:185799)**（spatial tensor）。$\boldsymbol{b}$ 和 $\boldsymbol{C}$ 之间通过[旋转张量](@entry_id:191990)联系：$\boldsymbol{b} = \boldsymbol{R}\boldsymbol{C}\boldsymbol{R}^{\mathsf{T}}$。因此，$\boldsymbol{b}$ 也拥有[特征值](@entry_id:154894) $\lambda_i^2$ [@problem_id:2640340, 2640415]。

### [客观性原理](@entry_id:185412)

在构建本构关系时，一个基本要求是材料的响应不应依赖于观察者的[参考系](@entry_id:169232)。这意味着[本构方程](@entry_id:138559)的形式在叠加一个任意的[刚体运动](@entry_id:193355)（即改变观察者）后应该保持不变。这个要求被称为**[客观性原理](@entry_id:185412)**（principle of objectivity）或**物质标架无关性**（material frame-indifference）。

当对当前构型叠加一个[刚体运动](@entry_id:193355) $\boldsymbol{x}^* = \boldsymbol{c} + \boldsymbol{Q}\boldsymbol{x}$（其中 $\boldsymbol{Q} \in \mathrm{SO}(3)$ 是一个[旋转张量](@entry_id:191990)）时，变形梯度会变为 $\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}$ [@problem_id:2640387]。

根据这个变换法则，我们可以定义不同类型张量的客观性 [@problem_id:2640387]：
- 一个**物质应变张量** $\boldsymbol{S}(\boldsymbol{F})$ 是客观的，如果它在叠加[刚体运动](@entry_id:193355)后保持不变，即 $\boldsymbol{S}(\boldsymbol{F}^*) = \boldsymbol{S}(\boldsymbol{F})$。
- 一个**空间应变张量** $\boldsymbol{s}(\boldsymbol{F})$ 是客观的，如果它随空间[坐标系](@entry_id:156346)一起旋转，即 $\boldsymbol{s}(\boldsymbol{F}^*) = \boldsymbol{Q}\boldsymbol{s}(\boldsymbol{F})\boldsymbol{Q}^{\mathsf{T}}$。

基于这些定义，我们可以检验柯西-格林张量的客观性。对于[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$：
$$
\boldsymbol{C}^* = (\boldsymbol{F}^*)^{\mathsf{T}}\boldsymbol{F}^* = (\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{C}
$$
$\boldsymbol{C}$ 是不变的，因此是客观的物质张量。这也解释了为何任何只依赖于 $\boldsymbol{C}$ 的物质[应变度量](@entry_id:755495)（如 $\boldsymbol{E}$ 和 $\boldsymbol{H}$）都是客观的 [@problem_id:2640387]。直接依赖于 $\boldsymbol{F}$ 的线性函数通常不是客观的，除非它恒为零 [@problem_id:2640387]。

对于[左柯西-格林张量](@entry_id:186163) $\boldsymbol{b}$：
$$
\boldsymbol{b}^* = \boldsymbol{F}^*(\boldsymbol{F}^*)^{\mathsf{T}} = (\boldsymbol{Q}\boldsymbol{F})(\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}} = \boldsymbol{Q}\boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}} = \boldsymbol{Q}\boldsymbol{b}\boldsymbol{Q}^{\mathsf{T}}
$$
$\boldsymbol{b}$ 遵循[空间张量](@entry_id:185799)的客观性变换规则。任何作为 $\boldsymbol{b}$ 的[各向同性张量](@entry_id:195105)函数（isotropic tensor function）的空间[应变度量](@entry_id:755495)（如 $\boldsymbol{e}$ 和 $\boldsymbol{h}$）也都将是客观的 [@problem_id:2640387]。

### 有限[应变度量](@entry_id:755495)大全

基于柯西-格林张量，我们可以定义一系列常用的有限应变张量。

#### [格林-拉格朗日应变张量](@entry_id:187745) (E)

**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange strain tensor）$\boldsymbol{E}$ 通过量化参考构型中[线元](@entry_id:196833)平方长度的变化来定义。其定义源于以下关系 [@problem_id:2886612]：
$$
ds^2 - dS^2 = d\boldsymbol{X}^{\mathsf{T}}(\boldsymbol{C} - \boldsymbol{I})d\boldsymbol{X} = 2 d\boldsymbol{X}^{\mathsf{T}}\boldsymbol{E}d\boldsymbol{X}
$$
由此可得其定义式：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I}) = \frac{1}{2}(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} - \boldsymbol{I})
$$
$\boldsymbol{E}$ 是一个定义在参考构型中的物质张量，由于它仅依赖于 $\boldsymbol{C}$，所以是客观的。对于纯刚体运动（$\boldsymbol{F}=\boldsymbol{R}$），$\boldsymbol{C}=\boldsymbol{I}$，因此 $\boldsymbol{E}=\boldsymbol{0}$，这符合[应变度量](@entry_id:755495)应为零的物理直觉 [@problem_id:2886612]。

$\boldsymbol{E}$ 的主值与其[主方向](@entry_id:276187)（与 $\boldsymbol{U}$ 和 $\boldsymbol{C}$ 相同）上的主拉伸 $\lambda_i$ 呈二次关系 [@problem_id:2886612]：
$$
E_i = \frac{1}{2}(\lambda_i^2 - 1)
$$
当[位移梯度](@entry_id:165352) $\boldsymbol{H} = \nabla_{\boldsymbol{X}} \boldsymbol{u}$ 很小时，$\boldsymbol{F} = \boldsymbol{I} + \boldsymbol{H}$，$\boldsymbol{E}$ 可以展开为：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{H} + \boldsymbol{H}^{\mathsf{T}} + \boldsymbol{H}^{\mathsf{T}}\boldsymbol{H})
$$
这表明 $\boldsymbol{E}$ 在小变形极限下可以近似为线性[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon} = \frac{1}{2}(\boldsymbol{H} + \boldsymbol{H}^{\mathsf{T}})$，但它本身包含了一个重要的[非线性](@entry_id:637147)项 $\frac{1}{2}\boldsymbol{H}^{\mathsf{T}}\boldsymbol{H}$ [@problem_id:2886612]。

#### [欧拉-阿尔曼西应变张量](@entry_id:194948) (e)

与 $\boldsymbol{E}$ 对偶，**[欧拉-阿尔曼西应变张量](@entry_id:194948)**（Euler-Almansi strain tensor）$\boldsymbol{e}$ 是一个定义在当前构型中的空间度量。它通过比较当前构型中线元的当前长度和“[拉回](@entry_id:160816)”到参考构型的长度来定义 [@problem_id:2886634]：
$$
ds^2 - dS^2 = d\boldsymbol{x}^{\mathsf{T}}(\boldsymbol{I} - \boldsymbol{b}^{-1})d\boldsymbol{x} = 2 d\boldsymbol{x}^{\mathsf{T}}\boldsymbol{e}d\boldsymbol{x}
$$
其定义式为：
$$
\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{b}^{-1})
$$
$\boldsymbol{e}$ 是一个[空间张量](@entry_id:185799)，并且是客观的。对于纯[刚体运动](@entry_id:193355)，$\boldsymbol{b}=\boldsymbol{I}$，因此 $\boldsymbol{e}=\boldsymbol{0}$ [@problem_id:2886622]。

$\boldsymbol{e}$ 的主值在其[主方向](@entry_id:276187)（与 $\boldsymbol{V}$ 和 $\boldsymbol{b}$ 相同）上与主拉伸 $\lambda_i$ 的关系为 [@problem_id:2886634, 2640415]：
$$
e_i = \frac{1}{2}(1 - \lambda_i^{-2})
$$
在小变形极限下，$\boldsymbol{e}$ 同样可以近似为线性[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ [@problem_id:2886634]。$\boldsymbol{E}$ 和 $\boldsymbol{e}$ 之间可以通过变形梯度进行变换，例如，将 $\boldsymbol{e}$ 从当前构型“[拉回](@entry_id:160816)”到参考构型，即可得到 $\boldsymbol{E}$：$\boldsymbol{E} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{e}\boldsymbol{F}$ [@problem_id:2886634]。

#### 亨基（对数）应变张量 (H, h)

格林-拉格朗日和[欧拉-阿尔曼西应变](@entry_id:187104)虽然常用，但它们不具备“可加性”。例如，对一个物体施加两次同轴的拉伸，其总的 $\boldsymbol{E}$ 或 $\boldsymbol{e}$ 并不等于两次变形各自应变之和。为了获得一个具有可加性的[应变度量](@entry_id:755495)，我们引入**[亨基应变](@entry_id:191329)张量**（Hencky strain tensor），也称**[对数应变](@entry_id:751438)**（logarithmic strain）。

其物质形式和[空间形式](@entry_id:186145)分别定义为右[拉伸张量](@entry_id:193200)和左[拉伸张量](@entry_id:193200)的对数 [@problem_id:2640338]：
$$
\boldsymbol{H} = \ln \boldsymbol{U} = \frac{1}{2}\ln \boldsymbol{C} \quad (\text{物质形式})
$$
$$
\boldsymbol{h} = \ln \boldsymbol{V} = \frac{1}{2}\ln \boldsymbol{b} \quad (\text{空间形式})
$$
这里的张量对数是通过谱分解定义的。如果一个对称正定张量 $\boldsymbol{T}$ 的谱分解为 $\boldsymbol{T} = \sum_{i} \lambda_i \boldsymbol{n}_i \otimes \boldsymbol{n}_i$，那么 $\ln \boldsymbol{T} = \sum_{i} (\ln \lambda_i) \boldsymbol{n}_i \otimes \boldsymbol{n}_i$ [@problem_id:2640338]。因此，[亨基应变](@entry_id:191329)的主值就是主拉伸的自然对数，即 $\ln \lambda_i$。

[亨基应变](@entry_id:191329)具有两个极其重要的特性 [@problem_id:2640409]：
1.  **可加性**：对于两个同轴（即可交换的[拉伸张量](@entry_id:193200) $\boldsymbol{U}_1, \boldsymbol{U}_2$）的连续变形，总的[亨基应变](@entry_id:191329)为各自[亨基应变](@entry_id:191329)之和：$\ln(\boldsymbol{U}_2 \boldsymbol{U}_1) = \ln \boldsymbol{U}_2 + \ln \boldsymbol{U}_1$ [@problem_id:2640338]。
2.  **精确的[体积-偏量分解](@entry_id:183756)**：[亨基应变](@entry_id:191329)的迹直接与体积变化的对数相关：$\mathrm{tr}(\boldsymbol{H}) = \sum_i \ln \lambda_i = \ln(\prod_i \lambda_i) = \ln J$。这意味着[亨基应变](@entry_id:191329)可以精确地、可加地分解为引起体积变化的球量[部分和](@entry_id:162077)引起形状变化的偏量部分 [@problem_id:2640338]。

### [功共轭](@entry_id:194957)与[虚功原理](@entry_id:138749)

在建立材料本构模型时，[应力张量和应变张量](@entry_id:755512)的选择并非任意，它们必须通过能量原理相互关联。这种关联通过**[功共轭](@entry_id:194957)**（work conjugacy）的概念来体现。如果一个应力张量与一个应变率张量的[内积](@entry_id:158127)等于单位体积的功率耗散（即[功率密度](@entry_id:194407)），那么这对张量就是[功共轭](@entry_id:194957)的。

**虚功原理**（Principle of Virtual Work）是寻找[功共轭](@entry_id:194957)对的系统方法，它本质上是平衡方程的弱形式（积分形式）。考虑一个处于准静态平衡的物体，其[平衡方程](@entry_id:172166)在当前构型中为 $\nabla \cdot \boldsymbol{\sigma} + \rho\boldsymbol{b} = \boldsymbol{0}$。将其与任意一个运动学容许的虚[速度场](@entry_id:271461) $\delta\boldsymbol{v}$ 做[点积](@entry_id:149019)并在当前体积 $v(t)$ 上积分，经过一系列推导，可得 [@problem_id:2886630]：

$$
\int_{v(t)} \boldsymbol{\sigma} : \delta\boldsymbol{d} \, \mathrm{d}v = \int_{v(t)} \rho\boldsymbol{b} \cdot \delta\boldsymbol{v} \, \mathrm{d}v + \int_{\partial v(t)} \boldsymbol{t} \cdot \delta\boldsymbol{v} \, \mathrm{d}a
$$

其中 $\boldsymbol{\sigma}$ 是**柯西应力**（Cauchy stress），$\delta\boldsymbol{d}$ 是虚**变形率张量**（rate of deformation tensor，即虚速度梯度的对称部分）。左边是[内虚功](@entry_id:172278)率，右边是外[虚功](@entry_id:176403)率。这表明，单位当前体积的[功率密度](@entry_id:194407)为 $\boldsymbol{\sigma}:\boldsymbol{d}$。因此，$(\boldsymbol{\sigma}, \boldsymbol{d})$ 是一对[功共轭](@entry_id:194957)的应力-应变率对。

通过坐标变换，我们可以将虚功原理表达式转换到参考构型，从而得到其他[功共轭](@entry_id:194957)对 [@problem_id:2886630]：
- 单位参考体积的[功率密度](@entry_id:194407)可以表示为 $\boldsymbol{P}:\dot{\boldsymbol{F}}$。因此，**第一类[皮奥拉-基尔霍夫应力](@entry_id:173629)**（1st Piola-Kirchhoff stress）$\boldsymbol{P}$ 与**变形梯度率** $\dot{\boldsymbol{F}}$ [功共轭](@entry_id:194957)。
- 单位参考体积的[功率密度](@entry_id:194407)也可以表示为 $\boldsymbol{S}:\dot{\boldsymbol{E}}$。因此，**第二类[皮奥拉-基尔霍夫应力](@entry_id:173629)**（2nd Piola-Kirchhoff stress）$\boldsymbol{S}$ 与**[格林-拉格朗日应变](@entry_id:170427)率** $\dot{\boldsymbol{E}}$ [功共轭](@entry_id:194957)。

### [应变度量](@entry_id:755495)的应用与选择

不同的有限[应变度量](@entry_id:755495)各有其理论和计算上的优缺点，适用于不同的应用场景。选择哪种[应变度量](@entry_id:755495)取决于问题的物理特性和所采用的[数值格式](@entry_id:752822) [@problem_id:2640409]。

- **[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$**：它是**全拉格朗日**（Total Lagrangian）有限元方法的自然选择。在这种方法中，所有积分和变量都定义在固定的参考构型上。$\boldsymbol{E}$ 及其[功共轭应力](@entry_id:182069) $\boldsymbol{S}$ 都是物质张量，这使得计算框架非常一致。对于以 $\boldsymbol{C}$ 的[不变量](@entry_id:148850)表示应变能的[超弹性材料](@entry_id:190241)（如橡胶），$\boldsymbol{E}$ 是最直接和方便的选择。

- **[亨基应变](@entry_id:191329) $\boldsymbol{H}$ (或 $\boldsymbol{h}$)**：它在[大应变](@entry_id:751152)[弹塑性](@entry_id:193198)理论中占据核心地位。其**可加性**对于处理弹性和塑性变形的[乘法分解](@entry_id:199514)（$\boldsymbol{F} = \boldsymbol{F}^e \boldsymbol{F}^p$）以及增量式的计算算法至关重要。其**精确的[体积-偏量分解](@entry_id:183756)**特性，使得区分材料的体积响应（弹性）和剪切响应（塑性）变得清晰，这对于金属等材料的建模至关重要。

- **[欧拉-阿尔曼西应变](@entry_id:187104) $\boldsymbol{e}$**：它是**欧拉**（Eulerian）或**更新拉格朗日**（Updated Lagrangian）方法的首选。在这些方法中，计算在当前或不断更新的构型上进行。例如，在流固耦合或[流体动力学](@entry_id:136788)问题中，状态变量通常存储在空间网格点上。作为一种空间度量，$\boldsymbol{e}$ 及其[功共轭应力](@entry_id:182069)（柯西应力 $\boldsymbol{\sigma}$）天然地与这种描述方式相匹配。

### [运动学](@entry_id:173318)协调性

到目前为止，我们都是从一个已知的变形映射 $\boldsymbol{\varphi}$ 出发来推导应变场。然而，一个反向的问题同样重要：给定一个[应变张量](@entry_id:193332)场，例如 $\boldsymbol{C}(\boldsymbol{X})$，是否存在一个连续、单值的变形场 $\boldsymbol{\varphi}(\boldsymbol{X})$ 与之对应？这个问题被称为**运动学协调性**（kinematic compatibility）问题。

如果应变场不满足某些可积性条件，那么它可能无法对应于一个真实的、物理上可能的变形（例如，可能导致材料内部出现不应有的孔洞或重叠）。对于小应变理论，这些条件就是著名的**[圣维南协调方程](@entry_id:754487)**（Saint-Venant's compatibility conditions）。然而，对于有限应变，这些线性条件是不充分的 [@problem_id:2886615]。

在有限变形理论中，一个给定的[对称正定](@entry_id:145886)[张量场](@entry_id:190170) $\boldsymbol{C}(\boldsymbol{X})$ 能够成为某个变形的[右柯西-格林张量](@entry_id:174156)的充分必要条件是，与度量张量 $\boldsymbol{C}$ 相关联的**黎曼-克里斯托费尔曲率张量**（Riemann-Christoffel curvature tensor）在整个区域内恒为零 [@problem_id:2886615]。这个条件在几何上的意义是，被赋予了由 $\boldsymbol{C}$ 定义的“内在距离”的物质体，其几何结构必须是“平直的”，即局部上可以无扭曲地展开到欧几里得空间中。一个等价的、在操作上更有用的条件是：存在一个张量场 $\boldsymbol{F}$ 使得 $\boldsymbol{C}=\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$，并且该场 $\boldsymbol{F}$ 的旋度为零（$\mathrm{Curl}\,\boldsymbol{F}=\boldsymbol{0}$）[@problem_id:2886615]。在单连通区域中，一个场的旋度为零是它能够表示为某个梯度的充分必要条件，即存在 $\boldsymbol{\varphi}$ 使得 $\boldsymbol{F} = \nabla\boldsymbol{\varphi}$。