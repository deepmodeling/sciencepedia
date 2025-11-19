## 引言
在描述材料如何响应[大变形](@entry_id:167243)时，连续介质力学提供了一套强大的数学框架。然而，仅靠变形梯度张量本身不足以构建物理上合理的材料模型，因为它会随观察者的刚体旋转而改变，违背了[客观性原理](@entry_id:185412)。为了解决这一根本问题，我们需要引入不依赖于观察者的变形度量。本文旨在深入探讨两个这样的核心运动学量：右柯西-格林（Right Cauchy-Green）和左柯西-格林（Left Cauchy-Green）变形张量。

通过本文的学习，读者将掌握这些张量从第一性原理出发的推导过程，理解其深刻的物理内涵，并了解它们在现代工程与科学计算中的广泛应用。文章分为三个核心部分：第一章“原理与机制”将奠定理论基础，阐明柯西-格林张量的定义、性质及其与旋转和拉伸的内在联系；第二章“应用与跨学科交叉”将展示这些理论在[计算力学](@entry_id:174464)、先进[材料建模](@entry_id:751724)和生物力学等前沿领域的实际应用；第三章“动手实践”则提供了一系列编程练习，旨在将理论知识转化为解决实际问题的计算技能。

让我们首先进入第一章，从变形梯度的概念开始，逐步揭示柯西-格林张量的奥秘。

## 原理与机制

在连续介质力学中，为了描述一个物体从其初始（或**参考**）构型到当前（或**空间**）构型的变形，我们需要一套能够精确量化局部几何变化的数学工具。虽然变形梯度张量为我们提供了这一信息的基础，但它本身在构建[本构关系](@entry_id:186508)时存在局限性。本章将深入探讨两个核心的[运动学](@entry_id:173318)量——**右柯西-格林（Right Cauchy-Green）**和**左柯西-格林（Left Cauchy-Green）**变形张量。我们将从第一性原理出发，阐明它们的定义、物理意义，以及它们在描述有限变形和建立客观[本构模型](@entry_id:174726)中的关键作用。

### 变形梯度：局部变形的度量

考虑一个连续体，其在参考构型 $\Omega_0$ 中的物[质点](@entry_id:186768)由位置向量 $\boldsymbol{X}$ 描述。经过一个变形过程，该物[质点](@entry_id:186768)运动到当前构型 $\Omega_t$ 中的位置 $\boldsymbol{x}$。这个过程可以通过一个足够光滑的映射 $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$ 来描述。

为了量化点 $\boldsymbol{X}$ 邻域内的局部变形，我们考察一个从 $\boldsymbol{X}$ 点出发的无限小物质线元 $d\boldsymbol{X}$。在变形后，它被映射为当前构型中的空间线元 $d\boldsymbol{x}$。通过对映射 $\boldsymbol{\varphi}$ 进行一阶[泰勒展开](@entry_id:145057)，我们得到这两个[线元](@entry_id:196833)之间的线性关系：
$$
d\boldsymbol{x} = \frac{\partial \boldsymbol{\varphi}}{\partial \boldsymbol{X}} d\boldsymbol{X}
$$
这个关系中的线性算子，即变形映射 $\boldsymbol{\varphi}$ 相对于参考坐标 $\boldsymbol{X}$ 的梯度，被称为**变形梯度张量（deformation gradient tensor）**，记为 $\boldsymbol{F}$：
$$
\boldsymbol{F} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}}
$$
因此，变形梯度是连接参考构型中无限小[线元](@entry_id:196833)与其在当前构型中像的[切线](@entry_id:268870)映射，即 $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$。[@problem_id:3596623]

变形梯度 $\boldsymbol{F}$ 包含了关于局部变形的所有信息。它的[行列式](@entry_id:142978)，即[雅可比行列式](@entry_id:137120) $J = \det(\boldsymbol{F})$，具有明确的物理意义。它表示了局部体积的变化率，即一个无限小的参考体元 $dV$ 经过变形后，其在当前构型中的体积 $dv$ 满足关系 $dv = J dV$。[@problem_id:3596623] 为了保证物质不会发生自我穿透或体积变为零甚至负值，物理上可接受的变形必须满足 $J > 0$。这个条件确保了变形映射在局部是可逆且保向的。

同样地，变形梯度也决定了[面积元](@entry_id:263205)的变化。一个在参考构型中面积为 $dA$、[单位法向量](@entry_id:178851)为 $\boldsymbol{N}$ 的面元，在变形后其面积矢量 $d\boldsymbol{a} = \boldsymbol{n} da$ 由著名的**南松公式（Nanson's relation）**给出：$d\boldsymbol{a} = J \boldsymbol{F}^{-\mathsf{T}} \boldsymbol{N} dA$。[@problem_id:3596623]

### 长度变化的测量：柯西-格林变形张量

变形梯度 $\boldsymbol{F}$ 本身虽然强大，但在直接用于构建材料[本构关系](@entry_id:186508)时存在一个严重问题：它不是**客观的（objective）**，即它的值会随着观察者[参考系](@entry_id:169232)的[刚体转动](@entry_id:191086)而改变。为了构建独立于观察者的[本构方程](@entry_id:138559)，我们需要寻找不随[刚体转动](@entry_id:191086)而变化的变形量度。这引导我们从最基本的物理量——长度的平方——出发，来定义新的变形张量。

#### 右柯西-格林变形张量

我们首先考虑一个参考[线元](@entry_id:196833) $d\boldsymbol{X}$ 及其变形后的像 $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$。变形后线元的长度平方为：
$$
|d\boldsymbol{x}|^2 = d\boldsymbol{x} \cdot d\boldsymbol{x} = (\boldsymbol{F} d\boldsymbol{X}) \cdot (\boldsymbol{F} d\boldsymbol{X})
$$
利用张量与向量乘积的性质，上式可以改写为：
$$
|d\boldsymbol{x}|^2 = d\boldsymbol{X} \cdot (\boldsymbol{F}^{\mathsf{T}} \boldsymbol{F} d\boldsymbol{X})
$$
这个表达式揭示了一个重要的张量 $\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$，它将变形后长度的计算“[拉回](@entry_id:160816)”到了参考构型中。我们将其定义为**右柯西-格林变形张量（right Cauchy-Green deformation tensor）**，记为 $\boldsymbol{C}$：
$$
\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}} \boldsymbol{F}
$$
因此，我们有 $|d\boldsymbol{x}|^2 = d\boldsymbol{X} \cdot (\boldsymbol{C} d\boldsymbol{X})$。从这个定义可以看出，$\boldsymbol{C}$ 是一个作用于参考构型中向量的张量，它是一个**拉格朗日（Lagrangian）**量。由于 $(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F})^{\mathsf{T}} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$，$\boldsymbol{C}$ 是对称的。只要 $\boldsymbol{F}$ 可逆，对于任何非零向量 $d\boldsymbol{X}$，都有 $|d\boldsymbol{x}|^2 > 0$，这意味着 $\boldsymbol{C}$ 是正定的。[@problem_id:3596616]

$\boldsymbol{C}$ 的物理意义可以通过**拉伸比（stretch）** $\lambda$ 的概念进一步阐明。拉伸比定义为变形后长度与初始长度之比，$\lambda = |d\boldsymbol{x}| / |d\boldsymbol{X}|$。考虑一根初始方向为[单位向量](@entry_id:165907) $\boldsymbol{N}$ 的材料纤维，其线元可表示为 $d\boldsymbol{X} = |d\boldsymbol{X}| \boldsymbol{N}$。该纤维的拉伸比平方为：
$$
\lambda^2 = \frac{|d\boldsymbol{x}|^2}{|d\boldsymbol{X}|^2} = \frac{d\boldsymbol{X} \cdot (\boldsymbol{C} d\boldsymbol{X})}{|d\boldsymbol{X}|^2} = \frac{(|d\boldsymbol{X}|\boldsymbol{N}) \cdot (\boldsymbol{C} (|d\boldsymbol{X}|\boldsymbol{N}))}{|d\boldsymbol{X}|^2} = \boldsymbol{N} \cdot (\boldsymbol{C} \boldsymbol{N})
$$
这个简洁的结果 $\lambda^2 = \boldsymbol{N} \cdot \boldsymbol{C} \boldsymbol{N}$ 表明，[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$ 直接提供了沿任意物质方向 $\boldsymbol{N}$ 的拉伸平方值。例如，对于一个变形梯度为 $\boldsymbol{F}=\mathrm{diag}(2, 1, 1/2)$ 的纯拉伸变形，一根初始方向为 $\boldsymbol{N}=\frac{1}{\sqrt{6}}(1, 2, -1)^{\mathsf{T}}$ 的纤维，其[右柯西-格林张量](@entry_id:174156)为 $\boldsymbol{C} = \boldsymbol{F}^2 = \mathrm{diag}(4, 1, 1/4)$，拉伸平方值为 $\lambda^2 = \boldsymbol{N}^{\mathsf{T}}\boldsymbol{C}\boldsymbol{N} = \frac{11}{8}$。[@problem_id:3596607]

#### 左柯西-格林变形张量

与上述问题对偶，我们也可以问：一个在当前构型中方向为[单位向量](@entry_id:165907) $\boldsymbol{n}$、长度为 $d\ell$ 的[线元](@entry_id:196833) $d\boldsymbol{x} = d\ell \boldsymbol{n}$，它在变形前的原始长度 $|d\boldsymbol{X}|$ 是多少？
利用关系 $d\boldsymbol{X} = \boldsymbol{F}^{-1} d\boldsymbol{x}$，我们计算其长度平方：
$$
|d\boldsymbol{X}|^2 = d\boldsymbol{X} \cdot d\boldsymbol{X} = (\boldsymbol{F}^{-1} d\boldsymbol{x}) \cdot (\boldsymbol{F}^{-1} d\boldsymbol{x}) = d\boldsymbol{x} \cdot (\boldsymbol{F}^{-\mathsf{T}} \boldsymbol{F}^{-1} d\boldsymbol{x})
$$
这里出现了一个新的张量 $\boldsymbol{F}^{-\mathsf{T}} \boldsymbol{F}^{-1}$。我们可以将其视为另一个张量的逆，这个张量就是**左柯西-格林变形张量（left Cauchy-Green deformation tensor）**，记为 $\boldsymbol{B}$：
$$
\boldsymbol{B} = \boldsymbol{F} \boldsymbol{F}^{\mathsf{T}}
$$
于是，$\boldsymbol{B}^{-1} = (\boldsymbol{F} \boldsymbol{F}^{\mathsf{T}})^{-1} = \boldsymbol{F}^{-\mathsf{T}} \boldsymbol{F}^{-1}$。因此，我们可以将原始长度的平方表示为：
$$
|d\boldsymbol{X}|^2 = d\boldsymbol{x} \cdot (\boldsymbol{B}^{-1} d\boldsymbol{x})
$$
$\boldsymbol{B}$ 是一个作用于当前构型中向量的张量，它是一个**欧拉（Eulerian）**量。与 $\boldsymbol{C}$ 类似，$\boldsymbol{B}$ 也是对称且正定的。[@problem_id:3596616]

将 $d\boldsymbol{x} = d\ell \boldsymbol{n}$ 代入，我们得到 $|d\boldsymbol{X}|^2 = d\ell^2 (\boldsymbol{n} \cdot \boldsymbol{B}^{-1} \boldsymbol{n})$。对于这个特定的纤维，其拉伸比平方的倒数为 $\lambda^{-2} = |d\boldsymbol{X}|^2/|d\boldsymbol{x}|^2 = \boldsymbol{n} \cdot \boldsymbol{B}^{-1} \boldsymbol{n}$。这个关系式给出了 $\boldsymbol{B}$ 的物理意义：它描述了从当前构型回溯到参考构型时的长度变化，是衡量那些**当前**[排列](@entry_id:136432)在特定空间方向 $\boldsymbol{n}$ 的纤维所经历的变形。[@problem_id:3596644]

总结来说，$\boldsymbol{C}$ 和 $\boldsymbol{B}$ 都是从长度平方变化中自然产生的变形度量，但它们作用的构型不同：$\boldsymbol{C}$ 作用于参考构型，而 $\boldsymbol{B}$ 作用于当前构型。

### [拉伸与旋转](@entry_id:150197)的物理内涵

为了更深刻地理解 $\boldsymbol{C}$ 和 $\boldsymbol{B}$ 的物理意义，我们引入**极分解（polar decomposition）**。任何可逆的变形梯度 $\boldsymbol{F}$ 都可以唯一地分解为一个纯拉伸（对称正定张量）和一个刚体旋转（正交张量）的乘积。这种分解有两种形式：
$$
\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U} = \boldsymbol{V}\boldsymbol{R}
$$
其中，$\boldsymbol{R}$ 是[旋转张量](@entry_id:191990)，$\boldsymbol{U}$ 是**右[拉伸张量](@entry_id:193200)（right stretch tensor）**，$\boldsymbol{V}$ 是**左[拉伸张量](@entry_id:193200)（left stretch tensor）**。$\boldsymbol{U}$ 和 $\boldsymbol{V}$ 都是[对称正定](@entry_id:145886)张量。$\boldsymbol{U}$ 描述了在参考构型[坐标系](@entry_id:156346)下的纯拉伸，而 $\boldsymbol{V}$ 描述了在当前构型[坐标系](@entry_id:156346)下的纯拉伸。

将极分解代入 $\boldsymbol{C}$ 和 $\boldsymbol{B}$ 的定义中：
$$
\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = (\boldsymbol{R}\boldsymbol{U})^{\mathsf{T}}(\boldsymbol{R}\boldsymbol{U}) = \boldsymbol{U}^{\mathsf{T}}\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}\boldsymbol{U} = \boldsymbol{U}^{\mathsf{T}}\boldsymbol{I}\boldsymbol{U} = \boldsymbol{U}^2
$$
$$
\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}} = (\boldsymbol{V}\boldsymbol{R})(\boldsymbol{V}\boldsymbol{R})^{\mathsf{T}} = \boldsymbol{V}\boldsymbol{R}\boldsymbol{R}^{\mathsf{T}}\boldsymbol{V}^{\mathsf{T}} = \boldsymbol{V}\boldsymbol{I}\boldsymbol{V}^{\mathsf{T}} = \boldsymbol{V}^2
$$
这两个简洁的结果 $\boldsymbol{C}=\boldsymbol{U}^2$ 和 $\boldsymbol{B}=\boldsymbol{V}^2$ 极大地澄清了它们的物理本质。[@problem_id:3596642] 它们分别是右[拉伸张量](@entry_id:193200)和左[拉伸张量](@entry_id:193200)的平方。这解释了为何 $\boldsymbol{C}$ 和 $\boldsymbol{B}$ 常被视为“拉伸平方”的度量。术语“右”和“左”也因此变得清晰：“右”柯西-格林张量 $\boldsymbol{C}$ 与极分解中出现在“右边”的右[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 相关，两者都作用于参考构型；而“左”柯西-格林张量 $\boldsymbol{B}$ 与出现在“左边”的左[拉伸张量](@entry_id:193200) $\boldsymbol{V}$ 相关，两者都作用于当前构型。

由于 $\boldsymbol{C}=\boldsymbol{U}^2$ 且 $\boldsymbol{B}=\boldsymbol{V}^2$，并且 $\boldsymbol{U}$ 和 $\boldsymbol{V}$ 通过相似变换 $\boldsymbol{V} = \boldsymbol{R}\boldsymbol{U}\boldsymbol{R}^{\mathsf{T}}$ 相关联，因此 $\boldsymbol{C}$ 和 $\boldsymbol{B}$ 拥有相同的**[特征值](@entry_id:154894)**。这些[特征值](@entry_id:154894)是主拉伸比 $\lambda_1, \lambda_2, \lambda_3$ 的平方，即 $\{\lambda_1^2, \lambda_2^2, \lambda_3^2\}$。由于张量的[主不变量](@entry_id:193522)是其[特征值](@entry_id:154894)的[对称函数](@entry_id:177113)，所以 $\boldsymbol{C}$ 和 $\boldsymbol{B}$ 也拥有完全相同的**[主不变量](@entry_id:193522)（principal invariants）**，例如 $I_1(\boldsymbol{C}) = \mathrm{tr}(\boldsymbol{C}) = \mathrm{tr}(\boldsymbol{B}) = I_1(\boldsymbol{B})$ 和 $\det(\boldsymbol{C}) = (\det(\boldsymbol{F}))^2 = \det(\boldsymbol{B})$。[@problem_id:3596616]

然而，尽管[特征值](@entry_id:154894)相同，$\boldsymbol{C}$ 和 $\boldsymbol{B}$ 的**[特征向量](@entry_id:151813)**通常是不同的。$\boldsymbol{C}$ 的[特征向量](@entry_id:151813)（记为 $\boldsymbol{N}_i$）定义了参考构型中的**主拉伸方向**（物质方向）。$\boldsymbol{B}$ 的[特征向量](@entry_id:151813)（记为 $\boldsymbol{n}_i$）定义了当前构型中的主拉伸方向（空间方向）。它们之间的关系恰好由[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 给出：
$$
\boldsymbol{n}_i = \boldsymbol{R} \boldsymbol{N}_i
$$
这意味着当前构型的主拉伸方向是参考构型主拉伸方向经过刚体旋转 $\boldsymbol{R}$ 后的结果。[@problem_id:3596676]

这种[特征向量](@entry_id:151813)的差异在[各向异性材料](@entry_id:184874)的[本构模型](@entry_id:174726)中至关重要。例如，对于[纤维增强复合材料](@entry_id:194995)，其能量可能依赖于沿纤维方向的拉伸。如果纤维在参考构型中的方向为 $\boldsymbol{M}$，一个自然的能量项会涉及[不变量](@entry_id:148850) $I_4 = \boldsymbol{M} \cdot \boldsymbol{C} \boldsymbol{M} = \boldsymbol{M}^{\mathsf{T}}\boldsymbol{C}\boldsymbol{M}$。这个量等于沿该纤维方向的拉伸平方 $\lambda^2_{\boldsymbol{M}}$。然而，如果我们试图在当前构型中用变形后的纤维方向 $\boldsymbol{m} = \boldsymbol{F}\boldsymbol{M}/|\boldsymbol{F}\boldsymbol{M}|$ 和张量 $\boldsymbol{B}$ 来构造一个类似的量，例如 $i_4 = \boldsymbol{m}^{\mathsf{T}}\boldsymbol{B}\boldsymbol{m}$，我们会发现这两个量通常并不相等。这个差异精确地反映了 $\boldsymbol{C}$ 和 $\boldsymbol{B}$ 在描述定向变形时的不同角色和数学结构。[@problem_id:3596676]

### 客观性与[本构模型](@entry_id:174726)

**物质[坐标系](@entry_id:156346)无关性原理（principle of material frame-indifference）**，或称**[客观性原理](@entry_id:185412)（principle of objectivity）**，是连续介质力学的一条基本公理。它要求材料的[本构关系](@entry_id:186508)（如[应力-应变关系](@entry_id:274093)）不能依赖于观察者。一个观察者的改变，在数学上等价于在当前构型上叠加一个刚体运动。对于一个给定的变形 $\boldsymbol{x}(\boldsymbol{X})$，叠加刚体运动后得到新的变形 $\widehat{\boldsymbol{x}}(\boldsymbol{X}) = \boldsymbol{c} + \boldsymbol{Q}\boldsymbol{x}(\boldsymbol{X})$，其中 $\boldsymbol{c}$ 是一个平移向量，$\boldsymbol{Q}$ 是一个[旋转张量](@entry_id:191990)（$\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}=\boldsymbol{I}, \det(\boldsymbol{Q})=1$）。

我们来考察各种运动学量在叠加[刚体运动](@entry_id:193355)下的变换规律：
*   变形梯度：$\widehat{\boldsymbol{F}} = \frac{\partial \widehat{\boldsymbol{x}}}{\partial \boldsymbol{X}} = \boldsymbol{Q}\frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}} = \boldsymbol{Q}\boldsymbol{F}$
*   [右柯西-格林张量](@entry_id:174156)：$\widehat{\boldsymbol{C}} = \widehat{\boldsymbol{F}}^{\mathsf{T}}\widehat{\boldsymbol{F}} = (\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{C}$
*   [左柯西-格林张量](@entry_id:186163)：$\widehat{\boldsymbol{B}} = \widehat{\boldsymbol{F}}\widehat{\boldsymbol{F}}^{\mathsf{T}} = (\boldsymbol{Q}\boldsymbol{F})(\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}} = \boldsymbol{Q}\boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}} = \boldsymbol{Q}\boldsymbol{B}\boldsymbol{Q}^{\mathsf{T}}$

从这些变换关系中可以得出几个关键结论：[@problem_id:3596634] [@problem_id:3596633]
1.  变形梯度 $\boldsymbol{F}$ **不是**客观的，因为它随观察者的旋转 $\boldsymbol{Q}$ 而改变。因此，[应变能函数](@entry_id:178435)不能直接写成 $\boldsymbol{F}$ 的任意函数。例如，即使对于一个简单的拉伸变形 $\boldsymbol{F}_0=\mathrm{diag}(2, 1, 1/2)$，叠加一个 $\pi/3$ 的旋转后，新的变形梯度 $\widehat{\boldsymbol{F}}$ 与 $\boldsymbol{F}_0$ 的差异（例如，由[弗罗贝尼乌斯范数](@entry_id:143384)的平方 $\|\widehat{\boldsymbol{F}} - \boldsymbol{F}_0\|_F^2$ 度量）不为零，清晰地表明了其非客观性。[@problem_id:3596634]
2.  [右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$ 在叠加刚体运动下**保持不变**（$\widehat{\boldsymbol{C}} = \boldsymbol{C}$）。这意味着任何以 $\boldsymbol{C}$ 为变量的标量函数，如[应变能密度](@entry_id:200085) $\Psi(\boldsymbol{C})$，都自动满足客观性要求。这是 $\boldsymbol{C}$ 在[超弹性](@entry_id:159356)本构理论中被广泛使用的根本原因。[@problem_id:3596602] [@problem_id:3596633]
3.  [左柯西-格林张量](@entry_id:186163) $\boldsymbol{B}$ 的变换规律 $\widehat{\boldsymbol{B}} = \boldsymbol{Q}\boldsymbol{B}\boldsymbol{Q}^{\mathsf{T}}$ 符合一个**客观欧拉张量**的定义。这意味着，如果[应变能密度](@entry_id:200085)写成 $\boldsymbol{B}$ 的函数 $\hat{\Psi}(\boldsymbol{B})$，那么为了满足客观性 $\hat{\Psi}(\widehat{\boldsymbol{B}}) = \hat{\Psi}(\boldsymbol{B})$，该函数必须满足 $\hat{\Psi}(\boldsymbol{Q}\boldsymbol{B}\boldsymbol{Q}^{\mathsf{T}}) = \hat{\Psi}(\boldsymbol{B})$。这个条件定义了一个**[各向同性张量](@entry_id:195105)函数**。根据[张量表示](@entry_id:180492)理论，任何标值[各向同性张量](@entry_id:195105)函数都必须是其张量[自变量](@entry_id:267118)的[主不变量](@entry_id:193522)的函数。因此，$\hat{\Psi}$ 必须可以表示为 $\hat{\Psi}(I_1(\boldsymbol{B}), I_2(\boldsymbol{B}), I_3(\boldsymbol{B}))$ 的形式。[@problem_id:3596633]

对于**[各向同性材料](@entry_id:170678)**，其材料响应不应依赖于其在参考构型中的初始取向。这意味着[应变能函数](@entry_id:178435)也必须对参考构型的任意旋转保持不变。这个物理要求同样会限制[应变能函数](@entry_id:178435)的形式，使其最终只能依赖于 $\boldsymbol{C}$ 的[主不变量](@entry_id:193522)。由于 $\boldsymbol{C}$ 和 $\boldsymbol{B}$ 共享相同的[主不变量](@entry_id:193522)，对于各向同性[超弹性材料](@entry_id:190241)，[应变能密度](@entry_id:200085)最终总可以写成[不变量](@entry_id:148850)的函数，例如 $\Psi(I_1, I_2, I_3)$。

在数值计算中，保证旋转矩阵 $\boldsymbol{Q}$ 的精确正交性至关重要。由于[浮点运算](@entry_id:749454)的舍入误差，一个理论上正交的矩阵在数值上可能会有微小的偏差，导致 $Q^T Q \neq I$。这种微小的误差会破坏 $\boldsymbol{C}$ 的不变性，从而导致[应变能](@entry_id:162699)计算出现非物理的误差。在实际应用中，通常需要通过极分解或奇异值分解（SVD）等方法对数值[旋转矩阵](@entry_id:140302)进行“修正”，将其投影到最近的正交矩阵上，以确保[客观性原理](@entry_id:185412)在离散计算中得以严格遵守。[@problem_id:3596602]

### 体积变形与偏变形

在许多应用中，特别是对于近似[不可压缩材料](@entry_id:159741)（如橡胶），将变形分解为改变体积的部分和保持体积（等容）的部分是非常有益的。这种分解可以在[运动学](@entry_id:173318)层面通过对变形梯度进行[乘法分解](@entry_id:199514)来实现。
$$
\boldsymbol{F} = J^{1/3} \bar{\boldsymbol{F}}
$$
这里，$J = \det(\boldsymbol{F})$ 是体积比，而 $\bar{\boldsymbol{F}} = J^{-1/3}\boldsymbol{F}$ 被称为**等容（isochoric）**或**偏（deviatoric）**变形梯度。通过取[行列式](@entry_id:142978)可以验证 $\det(\bar{\boldsymbol{F}}) = J^{-1} \det(\boldsymbol{F}) = 1$，表明 $\bar{\boldsymbol{F}}$ 描述的是一个纯粹改变形状而不改变体积的变形。[@problem_id:3596669]

这种分解可以自然地传递到柯西-格林张量上。我们定义等容[右柯西-格林张量](@entry_id:174156)为 $\bar{\boldsymbol{C}} = \bar{\boldsymbol{F}}^{\mathsf{T}}\bar{\boldsymbol{F}}$。将 $\boldsymbol{F}$ 的分解代入 $\boldsymbol{C}$ 的定义：
$$
\boldsymbol{C} = (J^{1/3}\bar{\boldsymbol{F}})^{\mathsf{T}}(J^{1/3}\bar{\boldsymbol{F}}) = J^{2/3}(\bar{\boldsymbol{F}}^{\mathsf{T}}\bar{\boldsymbol{F}}) = J^{2/3}\bar{\boldsymbol{C}}
$$
我们同样可以验证 $\det(\bar{\boldsymbol{C}}) = (\det(\bar{\boldsymbol{F}}))^2 = 1$。这个关系式将完整的变形度量 $\boldsymbol{C}$ 分解为标量体积因子 $J^{2/3}$ 和一个[行列式](@entry_id:142978)为1的[等容变形](@entry_id:196451)张量 $\bar{\boldsymbol{C}}$。

这种分解对于构建本构模型极其有用。例如，一个各向同性[超弹性材料](@entry_id:190241)的应变能可以被假设为体积响应和等容响应两部分的和：
$$
\Psi(\boldsymbol{C}) = \Psi_{\text{vol}}(J) + \Psi_{\text{iso}}(\bar{\boldsymbol{C}})
$$
其中，$\Psi_{\text{vol}}$ 仅依赖于体积比 $J$，描述材料对压缩或膨胀的抵抗；而 $\Psi_{\text{iso}}$ 依赖于[等容变形](@entry_id:196451)张量 $\bar{\boldsymbol{C}}$（通常是通过其[不变量](@entry_id:148850) $\bar{I}_1 = \mathrm{tr}(\bar{\boldsymbol{C}})$ 和 $\bar{I}_2$），描述材料对剪切变形的抵抗。许多流行的模型，如可压缩Neo-Hookean模型，都采用了这种形式。[@problem_id:3596602] [@problem_id:3596669]