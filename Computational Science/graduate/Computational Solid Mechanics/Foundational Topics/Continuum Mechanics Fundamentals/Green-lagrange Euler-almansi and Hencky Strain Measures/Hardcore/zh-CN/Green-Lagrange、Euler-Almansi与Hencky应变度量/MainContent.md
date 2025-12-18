## 引言
在工程和科学领域，从金属成型到[生物组织力学](@entry_id:194951)，许多关键问题都涉及材料的大变形，此时经典的[无穷小应变](@entry_id:197162)理论不再适用。为了精确描述这些现象，连续介质力学引入了[有限应变理论](@entry_id:176941)。然而，该理论提供了多种[应变度量](@entry_id:755495)方式，如格林-拉格朗日（Green-Lagrange）应变、欧拉-阿尔曼西（Euler-Almansi）应变和亨奇（Hencky）应变，它们各自具有独特的物理内涵和数学特性。对于研究者和工程师而言，一个常见的困惑是：在特定问题中应如何选择最合适的[应变度量](@entry_id:755495)？以及这种选择会对材料模型的预测和数值计算的稳定性产生何种影响？本文旨在系统地解答这些问题，为读者构建一个关于[有限应变度量](@entry_id:185716)的清晰框架。在接下来的章节中，我们将首先在“原理与机制”中详细推导每种[应变度量](@entry_id:755495)的定义并比较其根本差异。随后，在“应用与[交叉](@entry_id:147634)学科联系”中，我们将展示这些理论如何应用于[本构模型](@entry_id:174726)构建、计算力学挑战以及[生物力学](@entry_id:153973)等交叉学科。最后，“动手实践”部分将通过具体问题巩固您的理解。

## 原理与机制

在连续介质力学中，为了量化物体在经历变形时的局部拉伸与形状改变，我们需要精确的应变定义。当变形很小时，经典的[无穷小应变](@entry_id:197162)理论提供了简洁而有效的描述。然而，在许多工程应用中，例如金属成型、橡胶部件的[大变形](@entry_id:167243)以及生物软组织的力学行为，变形的量级很大，以至于[几何非线性](@entry_id:169896)效应变得不可忽略。在这种情况下，我们必须采用[有限应变理论](@entry_id:176941)，它提供了多种不同的[应变度量](@entry_id:755495)方式。本章将深入探讨三种最重要和最常用的[有限应变度量](@entry_id:185716)：**[格林-拉格朗日应变](@entry_id:170427) (Green-Lagrange strain)**、**[欧拉-阿尔曼西应变](@entry_id:187104) (Euler-Almansi strain)** 和 **亨奇应变 (Hencky strain)**。我们将从它们的基本定义出发，通过分析简单和复杂的变形模式，揭示它们各自的物理内涵、数学特性及其在计算和本构模型中的应用。

### 有限变形[运动学](@entry_id:173318)基础

在深入探讨各种[应变度量](@entry_id:755495)之前，我们必须首先建立描述有限变形的[运动学](@entry_id:173318)框架。一个连续体的运动可以被描述为一个从**参考构型**（或称初始构型、未变形构型）到**当前构型**（或称空间构型、变形后构型）的映射。参考构型中的物[质点](@entry_id:186768)由其位置向量 $\boldsymbol{X}$ 标识，而在当前构型中，同一物质点的位置由 $\boldsymbol{x}$ 给出。这个映射关系为 $\boldsymbol{x} = \boldsymbol{\phi}(\boldsymbol{X}, t)$。

描述局部变形的核心工具是**变形梯度张量 (deformation gradient tensor)** $\boldsymbol{F}$，其定义为：
$$
\boldsymbol{F} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}}
$$
$\boldsymbol{F}$ 将参考构型中的一个无穷小线元 $d\boldsymbol{X}$ 映射到当前构型中的对应[线元](@entry_id:196833) $d\boldsymbol{x}$，即 $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$。物理上，变形必须是可逆的，且不能使体积变为零或负值，这要求 $\boldsymbol{F}$ 的[行列式](@entry_id:142978)，即**雅可比行列式 (Jacobian)** $J = \det(\boldsymbol{F})$，必须为正值，$J > 0$。

为了从变形梯度中分离出纯拉伸和纯转动，我们引入**极分解 (polar decomposition)**。任何可逆的[二阶张量](@entry_id:199780) $\boldsymbol{F}$ 都可以唯一地分解为：
$$
\boldsymbol{F} = \boldsymbol{R} \boldsymbol{U} = \boldsymbol{V} \boldsymbol{R}
$$
其中，$\boldsymbol{R}$ 是一个正交[旋转张量](@entry_id:191990)（$\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R} = \boldsymbol{R}\boldsymbol{R}^{\mathsf{T}} = \boldsymbol{I}$ 且 $\det(\boldsymbol{R})=1$），$\boldsymbol{U}$ 是**右[拉伸张量](@entry_id:193200) (right stretch tensor)**，$\boldsymbol{V}$ 是**左[拉伸张量](@entry_id:193200) (left stretch tensor)**。$\boldsymbol{U}$ 和 $\boldsymbol{V}$ 都是[对称正定](@entry_id:145886)张量，它们分别描述了参考构型和当前构型中的纯拉伸。

为了方便地量化拉伸，我们还定义了两个重要的张量：
- **右柯西-格林变形张量 (right Cauchy-Green deformation tensor)** $\boldsymbol{C}$，定义在参考构型上：
$$
\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{U}^2
$$
- **左柯西-格林变形张量 (left Cauchy-Green deformation tensor)** $\boldsymbol{B}$ (也称为芬格张量 Finger tensor)，定义在当前构型上：
$$
\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}} = \boldsymbol{V}^2
$$
张量 $\boldsymbol{C}$ 和 $\boldsymbol{B}$ 直接关联于长度的平方变化。如果一个线元在参考构型中是 $d\boldsymbol{X}$，在当前构型中是 $d\boldsymbol{x}$，那么它们的长度平方之差可以表示为：
$$
|d\boldsymbol{x}|^2 - |d\boldsymbol{X}|^2 = (d\boldsymbol{X})^{\mathsf{T}} \boldsymbol{F}^{\mathsf{T}} \boldsymbol{F} (d\boldsymbol{X}) - (d\boldsymbol{X})^{\mathsf{T}} \boldsymbol{I} (d\boldsymbol{X}) = (d\boldsymbol{X})^{\mathsf{T}} (\boldsymbol{C} - \boldsymbol{I}) (d\boldsymbol{X})
$$
这个关系是定义[格林-拉格朗日应变](@entry_id:170427)的基础。

### [应变度量](@entry_id:755495)的定义与物理诠释

基于上述运动学量，我们可以定义三种核心的有限[应变张量](@entry_id:193332)。

#### [格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange Strain Tensor)

**[格林-拉格朗日应变张量](@entry_id:187745)** $\boldsymbol{E}$ 是一个**物质 (material)** 或**拉格朗日 (Lagrangian)** 度量，因为它是在参考构型中定义的。它的定义直接源于上述线元长度平方的变化：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I}) = \frac{1}{2}(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} - \boldsymbol{I})
$$
从定义可以看出，$\boldsymbol{E}$ 完全由[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$ 决定，因此它只度量了变形中的拉伸部分，而与[刚体转动](@entry_id:191086)无关。这一点至关重要：任何有效的[应变度量](@entry_id:755495)都必须对纯[刚体运动](@entry_id:193355)不敏感，即**物质客观性 (material frame-indifference)**。如果变形只是一个纯[刚体转动](@entry_id:191086)，即 $\boldsymbol{F} = \boldsymbol{R}$，那么 $\boldsymbol{C} = \boldsymbol{R}^{\mathsf{T}}\boldsymbol{R} = \boldsymbol{I}$，从而 $\boldsymbol{E} = \boldsymbol{0}$。这验证了 $\boldsymbol{E}$ 满足这一基本要求 。

#### [欧拉-阿尔曼西应变张量](@entry_id:194948) (Euler-Almansi Strain Tensor)

与 $\boldsymbol{E}$ 相对，**[欧拉-阿尔曼西应变张量](@entry_id:194948)** $\boldsymbol{e}$ 是一个**空间 (spatial)** 或**欧拉 (Eulerian)** 度量，因为它是在当前构型中定义的。其定义形式上与 $\boldsymbol{E}$ 对偶：
$$
\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{B}^{-1}) = \frac{1}{2}(\boldsymbol{I} - (\boldsymbol{F}\boldsymbol{F}^{\mathsf{T}})^{-1})
$$
$\boldsymbol{e}$ 通过[左柯西-格林张量](@entry_id:186163) $\boldsymbol{B}$ 度量了相对于当前构型的变形。类似于 $\boldsymbol{E}$，$\boldsymbol{e}$ 也满足物质客观性。对于纯[刚体转动](@entry_id:191086) $\boldsymbol{F} = \boldsymbol{R}$，我们有 $\boldsymbol{B} = \boldsymbol{R}\boldsymbol{R}^{\mathsf{T}} = \boldsymbol{I}$，因此 $\boldsymbol{e} = \boldsymbol{0}$ 。

#### 亨奇应变张量 (Hencky Strain Tensor)

**亨奇应变**，又称**[对数应变](@entry_id:751438) (logarithmic strain)** 或**真应变 (true strain)**，其定义基于[拉伸张量](@entry_id:193200)的对数。它同样具有物质（拉格朗日）和空间（欧拉）两种形式：
- **物质亨奇应变** $\boldsymbol{H} = \ln \boldsymbol{U} = \frac{1}{2}\ln\boldsymbol{C}$
- **空间亨奇应变** $\boldsymbol{h} = \ln \boldsymbol{V} = \frac{1}{2}\ln\boldsymbol{B}$

这里，$\ln$ 表示主[矩阵对数](@entry_id:169041)。对于一个对称正定张量 $\boldsymbol{A}$，其[谱分解](@entry_id:173707)为 $\boldsymbol{A} = \sum_{i} \lambda_i \boldsymbol{v}_i \otimes \boldsymbol{v}_i$，其对数为 $\ln \boldsymbol{A} = \sum_{i} (\ln \lambda_i) \boldsymbol{v}_i \otimes \boldsymbol{v}_i$。计算亨奇应变在数值上需要进行谱分解，这在计算上比 $\boldsymbol{E}$ 和 $\boldsymbol{e}$ 更昂贵，但它具有一些独特的优良性质，我们将在后面探讨。同样，对于纯[刚体转动](@entry_id:191086)，$\boldsymbol{U}=\boldsymbol{V}=\boldsymbol{I}$，因此 $\boldsymbol{H}=\boldsymbol{h}=\boldsymbol{0}$ 。

### 简单拉伸下的[应变度量](@entry_id:755495)比较

为了直观地理解这三种[应变度量](@entry_id:755495)的区别，我们来分析最简单的变形模式：一维均匀拉伸。考虑一个杆件沿其轴线方向均匀拉伸，其变形映射为 $x = \lambda X$，其中 $\lambda > 0$ 是**拉伸比 (stretch ratio)**。当 $\lambda > 1$ 时为拉伸，当 $\lambda  1$ 时为压缩。

在这种一维情况下，张量退化为标量。变形梯度 $F = \lambda$，[右柯西-格林张量](@entry_id:174156) $C = \lambda^2$，[左柯西-格林张量](@entry_id:186163) $B = \lambda^2$，右[拉伸张量](@entry_id:193200) $U = \lambda$。代入各自的定义，我们得到这三种应变的标量表达式  ：

- **[格林-拉格朗日应变](@entry_id:170427):** $E = \frac{1}{2}(\lambda^2 - 1)$
- **[欧拉-阿尔曼西应变](@entry_id:187104):** $e = \frac{1}{2}(1 - \lambda^{-2})$
- **亨奇应变:** $H = \ln \lambda$

现在我们来比较它们的行为：

1.  **小应变极限**：当变形很小时，$\lambda = 1 + \varepsilon$，其中 $|\varepsilon| \ll 1$。通过泰勒展开，我们发现：
    - $E = \frac{1}{2}((1+\varepsilon)^2 - 1) = \frac{1}{2}(1 + 2\varepsilon + \varepsilon^2 - 1) \approx \varepsilon$
    - $e = \frac{1}{2}(1 - (1+\varepsilon)^{-2}) = \frac{1}{2}(1 - (1 - 2\varepsilon + \dots)) \approx \varepsilon$
    - $H = \ln(1+\varepsilon) \approx \varepsilon$
    这表明，在小应变极限下，所有三种[有限应变度量](@entry_id:185716)都退化为经典的**工程应变 (engineering strain)** $\varepsilon$。这个结论对于三维情况也成立：当[位移梯度](@entry_id:165352) $\nabla\boldsymbol{u}$ 很小时，$\boldsymbol{E}$、$\boldsymbol{e}$ 和 $\boldsymbol{H}$ 均近似等于[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^{\mathsf{T}})$ 。这确保了[有限应变理论](@entry_id:176941)与线性弹性理论在小变形范围内的兼容性。

2.  **大拉伸** ($\lambda \gg 1$)：
    - $E \approx \frac{1}{2}\lambda^2$ （二次方增长）
    - $e \to \frac{1}{2}$ （饱和，趋于一个常数）
    - $H = \ln \lambda$ （对数增长）
    在大拉伸时，三者的数值差异巨大，其中 $E$ 的增长最快。

3.  **大压缩** ($\lambda \to 0^+$)：
    - $E \to -\frac{1}{2}$ （饱和，趋于一个常数）
    - $e \to -\infty$ （以 $-\lambda^{-2}$ 的速度趋于负无穷）
    - $H \to -\infty$ （以 $\ln \lambda$ 的速度趋于负无穷）
    在大压缩时，$E$ 表现出饱和特性，而 $e$ 和 $H$ 则无界。

这些显著的差异揭示了选择不同[应变度量](@entry_id:755495)的深刻后果。$E$ 对于拉伸比压缩更敏感，而 $e$ 则相反。$H$ 在拉伸和压缩之间表现出一种对数对称性。

### 不同构型间的转换关系

由于 $\boldsymbol{E}$ 是在参考构型中定义的，而 $\boldsymbol{e}$ 和 $\boldsymbol{h}$ 是在当前构型中定义的，理解它们之间的转换关系对于在不同框架下（例如，有限元方法中的[拉格朗日描述](@entry_id:264498)和[欧拉描述](@entry_id:264722)）建立本构关系至关重要。

对于一个在参考构型中定义的二阶[协变张量](@entry_id:634493)（如 $\boldsymbol{E}$），将其**[前推](@entry_id:158718) (push-forward)** 到当前构型，得到一个[空间张量](@entry_id:185799)的操作由下式给出：
$$
(\text{pushed-forward tensor}) = \boldsymbol{F}^{-\mathsf{T}} (\text{material tensor}) \boldsymbol{F}^{-1}
$$
一个重要的定理是，[欧拉-阿尔曼西应变](@entry_id:187104) $\boldsymbol{e}$ 正是[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ 的[前推](@entry_id:158718)结果：
$$
\boldsymbol{e} = \boldsymbol{F}^{-\mathsf{T}} \boldsymbol{E} \boldsymbol{F}^{-1}
$$
这个关系在数学上是恒等的，可以通过代数推导证明，也可以通过数值实验进行验证 。它将拉格朗日[应变度量](@entry_id:755495)与欧拉[应变度量](@entry_id:755495)直接联系起来。

然而，对于亨奇应变，情况则有所不同。物质亨奇应变 $\boldsymbol{H}$ 和空间亨奇应变 $\boldsymbol{h}$ 之间的关系不是通过简单的[前推](@entry_id:158718)操作，而是通过[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 的共轭变换：
$$
\boldsymbol{h} = \boldsymbol{R} \boldsymbol{H} \boldsymbol{R}^{\mathsf{T}}
$$
这意味着，简单地对物质亨奇应变 $\boldsymbol{H}$ 进行[前推](@entry_id:158718)操作 $\boldsymbol{F}^{-\mathsf{T}}\boldsymbol{H}\boldsymbol{F}^{-1}$，通常不会得到正确的空间亨奇应变 $\boldsymbol{h}$。只有在变形是纯拉伸（$\boldsymbol{F}=\boldsymbol{U}=\boldsymbol{V}, \boldsymbol{R}=\boldsymbol{I}$）的特殊情况下，两种变换才会给出相同的结果。这个区别非常重要，它强调了亨奇应变与变形的旋转部分有着更紧密的内在联系 。

### 在[本构模型](@entry_id:174726)中的意义

[应变度量](@entry_id:755495)的选择不仅仅是数学上的便利，它对材料[本构模型](@entry_id:174726)的物理行为有着深远的影响。一个经典的例子是基于不同[应变度量](@entry_id:755495)构建的二次型[弹性势能](@entry_id:168893)函数。

考虑一个简单的[超弹性材料](@entry_id:190241)，其[应变能密度函数](@entry_id:755490) $W$ 与某种[应变度量](@entry_id:755495)的二次方成正比。我们定义一个不对称指数 $S_W(\lambda) = \frac{W(\lambda) - W(1/\lambda)}{W(\lambda) + W(1/\lambda)}$ 来衡量材料在拉伸 ($\lambda$) 和等量压缩 ($1/\lambda$) 下的能量响应差异 。

- 如果我们选择基于[格林-拉格朗日应变](@entry_id:170427)的能量函数 $W_E = \frac{1}{2}k E^2$，在一维情况下，这变为 $W_E = \frac{k}{8}(\lambda^2 - 1)^2$。计算其不对称指数得到 $S_{W_E}(\lambda) = \frac{\lambda^4 - 1}{\lambda^4 + 1}$。这个结果不为零（除非 $\lambda=1$），表明该模型预测材料在拉伸时比在等量压缩时更“硬”（存储更多能量）。

- 相反，如果我们选择基于亨奇应变的能量函数 $W_h = \frac{1}{2}k H^2$，在一维情况下，这变为 $W_h = \frac{k}{2}(\ln \lambda)^2$。由于 $\ln(1/\lambda) = -\ln \lambda$，我们发现 $W_h(1/\lambda) = W_h(\lambda)$。因此，其不对称指数 $S_{W_h}(\lambda) = 0$。这表明基于亨奇应变的二次模型预测了拉伸和压缩之间完全对称的能量响应。

这个例子清楚地说明，仅仅通过改变底层的[应变度量](@entry_id:755495)，我们就可以构建出具有截然不同物理行为的材料模型。亨奇应变的这种对称性使其在描述某些材料（如在[对数应变](@entry_id:751438)空间中表现出线性行为的材料）时特别有用。

此外，[应变度量](@entry_id:755495)与其[功共轭](@entry_id:194957)的应力度量直接相关。例如，对于一个以空间亨奇应变 $\boldsymbol{h}$ 为变量的[应变能函数](@entry_id:178435) $W(\boldsymbol{h})$，其关于 $\boldsymbol{h}$ 的导数给出了**[基尔霍夫应力](@entry_id:751039)张量 (Kirchhoff stress tensor)** $\boldsymbol{\tau}$ ：
$$
\boldsymbol{\tau} = \frac{\partial W}{\partial \boldsymbol{h}}
$$
对于一个[各向同性材料](@entry_id:170678)，其能量可以分解为体积[部分和](@entry_id:162077)偏量部分，例如 $W(h)=\mu\|\operatorname{dev} \boldsymbol{h}\|^{2}+\frac{\kappa}{2}(\operatorname{tr} \boldsymbol{h})^{2}$，其中 $\mu$ 是剪切模量，$\kappa$ 是[体积模量](@entry_id:160069)。由此得到的[本构关系](@entry_id:186508)为 $\boldsymbol{\tau} = 2\mu \operatorname{dev} \boldsymbol{h} + \kappa (\operatorname{tr} \boldsymbol{h}) \boldsymbol{I}$。在小应变极限下，$h \approx \varepsilon$，$\tau \approx \sigma$，这个关系可以退化为经典的[胡克定律](@entry_id:149682) $\sigma = 2\mu \varepsilon + (\kappa - \frac{2\mu}{3})(\operatorname{tr} \varepsilon) \boldsymbol{I}$，其中拉梅第一常数 $\lambda_{\text{Lamé}} = \kappa - \frac{2\mu}{3}$。

### 复杂变形模式分析：简单剪切

简单剪切是一种包含旋转的非平凡变形，其变形梯度在二维情况下可表示为 $\boldsymbol{F} = \boldsymbol{I} + \gamma \boldsymbol{e}_1 \otimes \boldsymbol{e}_2$，其中 $\gamma$ 是剪切量。分析此种变形下不同[应变度量](@entry_id:755495)的主值，可以进一步揭示它们的特性 。

通过计算 $\boldsymbol{C}$ 和 $\boldsymbol{B}$ 的[特征值](@entry_id:154894)，并应用各自的定义，可以得到 $\boldsymbol{E}$, $\boldsymbol{e}$ 和 $\boldsymbol{h}$ 的[主值](@entry_id:189577)。特别地，对于亨奇应变 $\boldsymbol{h}$，其两个主值大小相等、符号相反，为 $h_{\pm} = \pm \operatorname{arcsinh}(\gamma/2)$。这再次体现了亨奇应变的对称性。

而对于[格林-拉格朗日应变](@entry_id:170427)，当 $\gamma \to \infty$ 时，其一个[主值](@entry_id:189577) $E_+$ 随 $\gamma^2$ 无界增长，而另一个[主值](@entry_id:189577) $E_-$ 趋于饱和值 $-1/2$。[欧拉-阿尔曼西应变](@entry_id:187104)则表现出互补的行为：一个[主值](@entry_id:189577) $e_-$ 随 $-\gamma^2$ 发散，而另一个主值 $e_+$ 趋于饱和值 $+1/2$。这种由[应变度量](@entry_id:755495)选择本身导致的、在主方向上响应的显著差异，被称为**度量诱导的各向异性 (measure-induced anisotropy)**。它说明即使是施加一个看似简单的[剪切变形](@entry_id:170920)，不同的[应变度量](@entry_id:755495)也会以截然不同的方式“感知”和量化材料内部的拉伸状态。

### 计算与数值方面的考量

在[计算力学](@entry_id:174464)中，尤其是在[有限元分析](@entry_id:138109)中，[应变度量](@entry_id:755495)的选择和计算方式对算法的鲁棒性和稳定性有直接影响。

#### 大压缩下的[数值稳定性](@entry_id:146550)

正如我们在一维拉伸分析中看到的，当材料经历大压缩时 ($\lambda \to 0^+$)，变形梯度 $\boldsymbol{F}$ 及其相关张量 $\boldsymbol{B}$ 变得奇[异或](@entry_id:172120)接近奇异（$\det \boldsymbol{B} = J^2 \to 0$）。

- **[欧拉-阿尔曼西应变](@entry_id:187104) $\boldsymbol{e}$ 的计算**：其定义 $\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{B}^{-1})$ 需要计算 $\boldsymbol{B}$ 的逆。当 $\boldsymbol{B}$ 接近奇异时，求逆是一个**病态 (ill-conditioned)** 的数值操作，微小的输入误差可能导致巨大的计算误差，从而破坏数值稳定性。

- **[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ 的计算**：其定义 $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} - \boldsymbol{I})$ 只涉及矩阵乘法和减法，这些操作在数值上是稳健的。因此，从给定的变形梯度 $\boldsymbol{F}$ 直接计算应变时，$\boldsymbol{E}$ 在大压缩下通常比 $\boldsymbol{e}$ 更为鲁棒 。

有趣的是，这个结论在求解**逆问题**时会反转。如果我们已知应变值，需要反求拉伸比 $\lambda$，我们会发现从 $e_{11}$ 恢复 $\lambda$ 是一个良态问题（导数 $\frac{d\lambda}{de_{11}} \to 0$），而从 $E_{11}$ 恢复 $\lambda$ 则是病态的（导数 $\frac{d\lambda}{dE_{11}} \to \infty$）。

#### 亨奇应变的计算

计算亨奇应变 $\boldsymbol{H} = \ln \boldsymbol{U}$ 或 $\boldsymbol{h} = \ln \boldsymbol{V}$ 需要计算对称正定矩阵的对数。最稳定和通用的方法是利用[谱分解](@entry_id:173707) ：
1.  对[拉伸张量](@entry_id:193200)（例如 $\boldsymbol{U}$）进行[特征值分解](@entry_id:272091)，得到其[特征值](@entry_id:154894) $\lambda_i$（即主拉伸）和对应的[正交特征向量](@entry_id:155522)矩阵 $\boldsymbol{Q}$，使得 $\boldsymbol{U} = \boldsymbol{Q} \operatorname{diag}(\lambda_i) \boldsymbol{Q}^{\mathsf{T}}$。
2.  对每个[特征值](@entry_id:154894)取自然对数，得到亨奇应变的[主值](@entry_id:189577) $\ln \lambda_i$。
3.  使用与 $\boldsymbol{U}$ 相同的[特征向量基](@entry_id:163721)底重构亨奇[应变张量](@entry_id:193332)：$\boldsymbol{H} = \boldsymbol{Q} \operatorname{diag}(\ln \lambda_i) \boldsymbol{Q}^{\mathsf{T}}$。

在数值实现中，需要注意处理[特征值](@entry_id:154894)重复或非常接近的情况。幸运的是，[谱分解](@entry_id:173707)算法对于对称矩阵是极其稳健的，并且最终计算出的 $\boldsymbol{H}$ 对于在重根[特征空间](@entry_id:638014)中选择哪组正交基是无关的。此外，为了避免对由于[浮点误差](@entry_id:173912)可能出现的微小负[特征值](@entry_id:154894)取对数，通常需要对计算出的[特征值](@entry_id:154894)进行截断处理，例如将其限制在一个小的正数阈值以上。

### 总结

本章详细介绍了格林-拉格朗日、欧拉-阿尔曼西和亨奇这三种[有限应变度量](@entry_id:185716)。我们看到，尽管它们在小变形极限下趋于一致，但在有限变形领域，它们具有截然不同的数学特性和物理内涵。
- **[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$** 是一个拉格朗日度量，计算稳健，但在拉伸和压缩之间表现出不对称性，且在大压缩下会饱和。
- **[欧拉-阿尔曼西应变](@entry_id:187104) $\boldsymbol{e}$** 是一个欧拉度量，与 $\boldsymbol{E}$ 通过[前推](@entry_id:158718)操作相联系，但在大压缩下其直接计算是不稳定的。
- **亨奇应变 $\boldsymbol{H}$/$\boldsymbol{h}$** 提供了对“真应变”的度量，具有良好的对称性，并且对于同轴应变增量是可加的，但其计算更为复杂，且与其他张量的变换关系也更特殊。

在工程实践和科学研究中，没有哪一种[应变度量](@entry_id:755495)是绝对“最佳”的。选择哪一种取决于具体的应用场景、所研究的材料特性、本构模型的形式以及数值算法的框架。深刻理解这些度量之间的差异和联系，是进行高级[非线性力学](@entry_id:178303)分析和建模的关键。