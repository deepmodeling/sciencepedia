## 引言
在现代[偏微分方程](@entry_id:141332)（PDE）理论和以谱方法、间断Galerkin（DG）方法为代表的高级数值计算领域，函数在区域边界或内部界面上的行为占据着核心地位。然而，许多问题的自然设定是在Sobolev空间（如$H^1(\Omega)$）中，其中的函数未必足够光滑，以至于在边界上拥有经典意义下的逐点值。这就引出了一个基础性难题：对于一个$H^1$函数，我们如何严格地谈论它的边界值？本文旨在系统性地解答这一问题，深入剖析作为解决方案的**[迹定理](@entry_id:203967)（trace theorems）**与**[迹空间](@entry_id:756085)（trace spaces）**。

本文将带领读者跨越三个章节，构建对迹理论的全面理解。首先，在“原理与机制”一章中，我们将奠定理论基础，阐明为何需要[迹算子](@entry_id:183665)，并详细介绍其如何将定义在区域内部的函数映射到边界上的分数阶[Sobolev空间](@entry_id:141995)。我们将探讨这一映射的性质、相关的[迹不等式](@entry_id:756082)及其对几何和多项式次数的依赖性，并将理论从[标量场](@entry_id:151443)推广到电磁学中至关重要的$H(\mathrm{curl})$矢量场。

接下来，在“应用与跨学科连接”一章中，我们将展示这些抽象理论的强大应用价值。我们将看到迹理论如何为PDE的边界条件提供严谨诠释，并成为[DG方法](@entry_id:748369)、[区域分解法](@entry_id:165176)等现代数值算法设计的语言和支柱。通过连接固体力学中的接触问题、[流体力学](@entry_id:136788)以及反问题等领域，本章将揭示迹理论作为一种通用工具在不同学科中的统一作用。

最后，“动手实践”部分将提供一系列练习，帮助读者将理论知识转化为解决实际问题的能力，加深对迹的正则性、[迹不等式](@entry_id:756082)及其在离散设定中应用的理解。

现在，让我们从第一章开始，深入探索[迹定理](@entry_id:203967)与[迹空间](@entry_id:756085)的原理与机制，揭开其神秘的面纱。

## 原理与机制

在[偏微分方程](@entry_id:141332)的现代理论和[数值分析](@entry_id:142637)中，尤其是在谱方法和间断Galerkin（DG）方法等高阶方法中，函数在区域边界或内部单元交界面上的行为至关重要。然而，许多自然的问题框架都设定在Sobolev空间中，例如$H^1(\Omega)$，其中的函数不一定足够光滑以至于拥有经典意义上的点态边界值。本章将深入探讨**[迹定理](@entry_id:203967)**（trace theorems）和相关的**[迹空间](@entry_id:756085)**（trace spaces）的原理与机制。这些理论为在[Sobolev空间](@entry_id:141995)框架内严格定义和处理边界值提供了数学基础，是构建和分析现代数值方法的基石。

### 为何需要迹：$H^1$函数的边界值问题

考虑Sobolev空间$H^1(\Omega)$，它由定义在区域$\Omega \subset \mathbb{R}^d$上的所有$L^2$函数组成，且其[弱导数](@entry_id:189356)也属于$L^2$。在处理[偏微分方程](@entry_id:141332)时，我们通常需要施加边界条件，例如在$\partial\Omega$上规定$u$的值。这就提出了一个深刻的问题：对于一个任意的$u \in H^1(\Omega)$，其在边界$\partial\Omega$上的“值”是否有明确的定义？

当空间维度$d=1$时，[Sobolev嵌入定理](@entry_id:192380)保证了$H^1(\Omega)$中的每个函数都等价于一个[连续函数](@entry_id:137361)（在$\overline{\Omega}$上）。因此，点态值，包括[边界点](@entry_id:176493)上的值，是明确定义的。然而，当维度$d \ge 2$时，情况发生了根本性变化。$H^1(\Omega)$不再连续嵌入到$C^0(\overline{\Omega})$中。这意味着存在$H^1(\Omega)$中的函数，它们不具有任何连续的代表元，甚至可能在某些点上是无界的。

为了具体理解这一点，我们可以构造一些反例[@problem_id:3425078]。
- 在$d \ge 3$维空间中，考虑函数$u(x) = |x|^{-\alpha}$，其中$x=0$是$\Omega$的一个[内点](@entry_id:270386)。通过计算可以验证，只要$0  \alpha  (d-2)/2$，该函数及其梯度在原点附近都是平方可积的，因此（通过一个光滑截断函数将其限制在$\Omega$内）$u \in H^1(\Omega)$。然而，当$x \to 0$时，$u(x)$是无界的，因此它不可能是连续的。
- 在$d=2$维空间中，[幂律](@entry_id:143404)函数不再适用，但我们可以构造一个增长更缓慢的函数，例如$u(x) = \ln(\ln(e/|x|))$。同样可以验证，该函数属于$H^1(\Omega)$，但它在原点附近也是无界的。

这些例子清晰地表明，在二维及更高维度中，我们不能想当然地谈论一个$H^1$函数在边界上某一点的值。然而，DG方法中的数值通量、边界元方法中的[积分方程](@entry_id:138643)，以及[谱方法](@entry_id:141737)中边界条件的施加，都迫切需要一种严格的方式来处理边界值。**迹理论**应运而生，它通过定义一个**[迹算子](@entry_id:183665)**（trace operator），将定义在“体积”$\Omega$上的函数映射到其“边界”$\partial\Omega$上，从而完美地解决了这一难题。这个算子不是产生点态值，而是将函数映射到一个定义在边界上的、具有较低正则性的新函数空间——**[迹空间](@entry_id:756085)**。

### [标量场](@entry_id:151443)的迹理论

#### 基本[迹定理](@entry_id:203967)

迹理论的核心是**[迹定理](@entry_id:203967)**。它断言，对于一个有界Lipschitz区域$\Omega \subset \mathbb{R}^d$，存在一个唯一的、有界的[线性算子](@entry_id:149003)，称为**[迹算子](@entry_id:183665)**，通常记作$\mathcal{T}$或$\gamma$。

这个算子将$H^1(\Omega)$空间中的函数映射到边界上的分数阶[Sobolev空间](@entry_id:141995)$H^{1/2}(\partial\Omega)$中：
$$
\mathcal{T}: H^1(\Omega) \to H^{1/2}(\partial\Omega)
$$
此算子具有以下关键性质：
1.  **线性性**：对于任意$u, v \in H^1(\Omega)$和标量$a, b$，有$\mathcal{T}(au+bv) = a\mathcal{T}u + b\mathcal{T}v$。
2.  **有界性（连续性）**：存在一个常数$C_{\mathcal{T}} > 0$，使得对于所有$u \in H^1(\Omega)$，都有
    $$
    \|\mathcal{T}u\|_{H^{1/2}(\partial\Omega)} \le C_{\mathcal{T}} \|u\|_{H^1(\Omega)}
    $$
3.  **与经典限制的一致性**：如果一个函数$u$足够光滑（例如，$u \in C^\infty(\overline{\Omega})$），那么[迹算子](@entry_id:183665)的作用结果就等于该函数在边界上的经典限制，即$\mathcal{T}u = u|_{\partial\Omega}$。由于[光滑函数](@entry_id:267124)在$H^1(\Omega)$中是稠密的，这保证了[迹算子](@entry_id:183665)是经典限制概念的唯一[连续延拓](@entry_id:161021)。

目标空间$H^{1/2}(\partial\Omega)$是一个分数阶Sobolev空间。它的范数刻画了边界上函数的“半阶”正则性。对于定义在$(d-1)$维边界[流形](@entry_id:153038)$\partial\Omega$上的函数$v$，其$H^{1/2}(\partial\Omega)$范数通常由$L^2(\partial\Omega)$范数和一个**Gagliardo-Slobodeckij半范**组成[@problem_id:3425078]：
$$
\|v\|_{H^{1/2}(\partial\Omega)}^2 = \|v\|_{L^2(\partial\Omega)}^2 + |v|_{H^{1/2}(\partial\Omega)}^2 = \|v\|_{L^2(\partial\Omega)}^2 + \int_{\partial\Omega}\int_{\partial\Omega} \frac{|v(x)-v(y)|^2}{|x-y|^d} \, \mathrm{d}s_x \, \mathrm{d}s_y
$$
请注意半范定义中分母的幂次$|x-y|^d$。这里的$d$是**体积空间**$\mathbb{R}^d$的维度，而不是边界$\partial\Omega$的维度$d-1$。这个幂次精确地反映了从$H^1$（[一阶导数](@entry_id:749425)可积）到$H^{1/2}$（半阶导数可积）的“半阶正则性损失”。

#### 分数阶[Sobolev空间](@entry_id:141995)与广义[迹定理](@entry_id:203967)

[迹定理](@entry_id:203967)可以推广到更广泛的Sobolev空间$W^{s,p}(\Omega)$。对于$p=2$的Hilbert空间情形，即$H^s(\Omega)$，我们可以定义一个完整的标度。

对于非整数$s \in (0,1)$，空间$H^s(\Omega)$由所有$L^2(\Omega)$中的函数$u$构成，其Gagliardo-Slobodeckij半范有限[@problem_id:3425091]：
$$
|u|_{H^s(\Omega)}^2 = \int_{\Omega} \int_{\Omega} \frac{|u(x) - u(y)|^2}{|x - y|^{d + 2s}} \, dx \, dy
$$
相应的范数为$\|u\|_{H^s(\Omega)}^2 = \|u\|_{L^2(\Omega)}^2 + |u|_{H^s(\Omega)}^2$。空间$H^0(\Omega)$定义为$L^2(\Omega)$，$H^1(\Omega)$是标准的一阶Sobolev空间。

广义[迹定理](@entry_id:203967)指出，对于$s \in (1/2, \infty)$，存在一个有界的[迹算子](@entry_id:183665)$\mathcal{T}: H^s(\Omega) \to H^{s-1/2}(\partial\Omega)$。这揭示了一个深刻的正则性阈值：**一个函数必须至少比$H^{1/2}(\Omega)$更光滑，才能保证其在边界上有一个$L^2(\partial\Omega)$的迹**。当$s \le 1/2$时，一般不存在从$H^s(\Omega)$到$L^2(\partial\Omega)$的有界线性[迹算子](@entry_id:183665)。

对于一般的$W^{s,p}(\Omega)$空间（其中$1  p  \infty$），也存在类似的[迹定理](@entry_id:203967)[@problem_id:3425124]。这里的关键阈值变为$s > 1/p$。当此条件满足时，存在唯一的有界线性[迹算子](@entry_id:183665)$\mathcal{T}: W^{s,p}(\Omega) \to B_{p,p}^{s-1/p}(\partial\Omega)$，其中目标空间是一个Besov空间。反之，若$s \le 1/p$，则不存在这样的[迹算子](@entry_id:183665)。这解释了为何$H^s = W^{s,2}$的阈值是$s > 1/2$。

对于$s \le 1/2$的情况，虽然不存在到$L^2$或更光滑空间的迹，但我们仍然可以利用对偶性来定义**负阶迹**[@problem_id:3425076]。具体来说，[迹算子](@entry_id:183665)$\mathcal{T}: H^s(\Omega) \to H^{s-1/2}(\partial\Omega)$仍然是有界的。此时，$s-1/2$是负数或零，而负阶Sobolev空间$H^{s-1/2}(\partial\Omega)$被定义为其[对偶空间](@entry_id:146945)的正阶空间的对偶，即$H^{s-1/2}(\partial\Omega) = (H^{1/2-s}(\partial\Omega))'$。这个迹可以通过对偶性来定义。对于任意测试函数 $\psi \in H^{1/2-s}(\partial\Omega)$，其对偶作用 $\langle \mathcal{T}u, \psi \rangle_{\partial\Omega}$ 可以通过[格林公式](@entry_id:173118)来定义。这通常涉及将 $\psi$ 扩张为一个定义在整个区域上的函数 $E\psi \in H^{1-s}(\Omega)$，然后计算 $u$ 与 $E\psi$ 及其导数在区域 $\Omega$ 上的积分，而$\langle \cdot, \cdot \rangle_{\partial\Omega}$表示对偶作用。

#### 迹的[右逆](@entry_id:161498)：扩张算子

[迹定理](@entry_id:203967)的一个重要方面是[迹算子](@entry_id:183665)$\mathcal{T}$的**满射性**（surjectivity）。对于$H^1(\Omega)$到$H^{1/2}(\partial\Omega)$的[迹算子](@entry_id:183665)，满射性意味着对于边界上任意给定的函数$g \in H^{1/2}(\partial\Omega)$，我们总能找到一个定义在体积$\Omega$上的函数$u \in H^1(\Omega)$，使得$u$在边界上的迹恰好是$g$（即$\mathcal{T}u = g$）。

这个性质等价于存在一个有界的线性**[右逆](@entry_id:161498)算子**，也称为**扩张算子**（extension operator）$E: H^{1/2}(\partial\Omega) \to H^1(\Omega)$，它满足$\mathcal{T} \circ E = \mathrm{Id}$（在$H^{1/2}(\partial\Omega)$上的[恒等算子](@entry_id:204623)），并且有界，即$\|Eg\|_{H^1(\Omega)} \le C \|g\|_{H^{1/2}(\partial\Omega)}$[@problem_id:3425088]。

扩张算子的构造通常依赖于局部化和拼接技术。其基本思想是[@problem_id:3425088]：
1.  **局部化**：使用从属于边界图册的[单位分解](@entry_id:150115)，将边界函数$g$分解为一系列具有[紧支集](@entry_id:276214)的局部函数$g_j = \varphi_j g$。
2.  **展平**：通过Lipschitz坐标变换，将每个局部边界片和邻近的区域内部映射到半空间$\mathbb{R}^d_+$及其边界$\mathbb{R}^{d-1}$。
3.  **[半空间](@entry_id:634770)扩张**：在[半空间](@entry_id:634770)上，存在一个已知的、有界的扩张算子$E_+$，它将定义在$\mathbb{R}^{d-1}$上的函数扩张为$\mathbb{R}^d_+$上的$H^1$函数。将此算子应用于变换后的局部函数$\tilde{g}_j$。
4.  **变换回**：将[半空间](@entry_id:634770)上的扩张函数通过[坐标变换](@entry_id:172727)的逆映射回原始的弯曲几何。
5.  **拼接**：使用光滑截断函数将所有局部的扩张[函数平滑](@entry_id:201048)地拼接在一起，形成一个定义在整个$\Omega$上的全局扩张函数$Eg$。

这个构造过程保证了最终得到的算子$E$是线性和有界的，并且是[迹算子](@entry_id:183665)的[右逆](@entry_id:161498)。类似地，对于广义[迹定理](@entry_id:203967)$\mathcal{T}: H^s(\Omega) \to H^{s-1/2}(\partial\Omega)$（$s>1/2$），同样存在有界的[右逆](@entry_id:161498)。

### [迹不等式](@entry_id:756082)及其标度律

[迹定理](@entry_id:203967)的有界性可以用**[迹不等式](@entry_id:756082)**来量化，这在[数值分析](@entry_id:142637)的[误差估计](@entry_id:141578)和稳定性证明中至关重要。

#### 等度规情形与几何依赖性

[迹不等式](@entry_id:756082)的一个更精确的版本揭示了其对区域几何尺寸的依赖性。对于一个直径为$D$的有界Lipschitz区域$\Omega$，[迹不等式](@entry_id:756082)可以写作[@problem_id:3425132]：
$$
\|\mathcal{T}u\|_{L^2(\partial\Omega)} \le C_{\mathrm{tr}} \left( D^{-1/2} \|u\|_{L^2(\Omega)} + D^{1/2} \|\nabla u\|_{L^2(\Omega)} \right)
$$
其中常数$C_{\mathrm{tr}}$仅依赖于区域的“形状”（通过[Lipschitz常数](@entry_id:146583)等来量化），而与区域的尺寸$D$无关。这个形式在通过标度分析从一个参考区域推导到任意尺寸区域时自然出现。$D^{-1/2}$和$D^{1/2}$这两个因子对于DG方法的分析尤为重要，它与单元尺寸$h$的依赖性直接相关。

人们可能会问，区域的**曲率**（curvature）是否会显式地出现在[迹不等式](@entry_id:756082)的常数中？答案是，对于标准的[迹定理](@entry_id:203967)，曲率的影响是间接的[@problem_id:3425081]。在基于局部展平和[单位分解](@entry_id:150115)的证明中，常数取决于Lipschitz图册的性质（如bi-[Lipschitz常数](@entry_id:146583)和覆盖重叠数）。对于一个光滑的弯曲边界，其曲率会影响我们能构造的多么“好”的（即失真多小）的bi-Lipschitz图册。高曲率区域可能需要更小的图卡来维持小的失真，但这最终还是被封装在bi-[Lipschitz常数](@entry_id:146583)中。因此，曲率不是一个独立的、额外的参数。我们可以用一种依赖于[曲率界](@entry_id:200421)和[管状邻域](@entry_id:269959)宽度的替代证明方法得到显式依赖于曲率的常数，但这些常数最终可以被更普适的bi-Lipschitz图册常数所界定。

#### 各向异性[迹不等式](@entry_id:756082)

在许多应用中，例如模拟[边界层](@entry_id:139416)或薄壁结构，[计算网格](@entry_id:168560)可能包含**各向异性单元**（anisotropic elements），即在不同方向上尺寸差异很大的单元（例如，扁平的矩形或三角形）。在这种情况下，标准的等度规[迹不等式](@entry_id:756082)（其常数仅依赖于单元的[形状规则性](@entry_id:754733)，而不依赖于其宽高比）会给出过于悲观的估计。

我们需要一个能精确反映各向异性影响的[迹不等式](@entry_id:756082)。考虑一个矩形单元$K = (0,h_{\perp}) \times (0,h_{\parallel})$[@problem_id:3425134]。通过沿法向进行一维[迹不等式](@entry_id:756082)估计并积分，可以得到一个面向特定面的[迹不等式](@entry_id:756082)。对于一个面$F \subset \partial K$，其迹范数可以被如下控制：
$$
\|u\|_{L^2(F)} \lesssim h_n(F)^{-1/2} \|u\|_{L^2(K)} + h_n(F)^{1/2} \|\partial_{n_F} u\|_{L^2(K)}
$$
这里，$h_n(F)$是单元$K$在垂直于面$F$方向上的**厚度**，而$\partial_{n_F} u$是$u$沿该法向的方向导数。这个不等式清晰地表明，迹的大小主要由函数在法向上的行为决定。例如，在一个非常扁平的单元上，一个“长边”上的迹范数主要由单元的“短边”厚度控制。

### 在间断Galerkin方法中的应用

迹理论是间断Galerkin（DG）方法数学框架的支柱。DG方法使用的函数空间是分片[Sobolev空间](@entry_id:141995)，例如$H^1(\mathcal{T}_h) = \{ v \in L^2(\Omega) : v|_K \in H^1(K) \text{ for all } K \in \mathcal{T}_h \}$，其中$\mathcal{T}_h$是$\Omega$的一个网格剖分。这些函数在单元边界上可以是间断的。

#### 跳跃和[平均算子](@entry_id:746605)

[DG方法](@entry_id:748369)的公式化依赖于在内部单元交界面$F$上定义的**跳跃**（jump）和**平均**（average）算子。设$F$是单元$K^+$和$K^-$的公共面，$\boldsymbol{n}^\pm$是从$K^\pm$指向外部的[单位法向量](@entry_id:178851)。对于一个标量函数$u \in H^1(\mathcal{T}_h)$，其在$F$上的单边迹为$u^\pm = \mathcal{T}(u|_{K^\pm})$。根据[迹定理](@entry_id:203967)，这些单边迹是$H^{1/2}(F)$中的良定义元素。

基于这些单边迹，我们可以定义跳跃和[平均算子](@entry_id:746605)。存在多种约定，一种常用于对称内罚法（SIPG）的约定是[@problem_id:3425104]：
- **[平均算子](@entry_id:746605)**（标量值）：$\lbrace u \rbrace := \frac{1}{2}(u^+ + u^-)$
- **跳跃算子**（矢量值）：$[\boldsymbol{u}] := u^+ \boldsymbol{n}^+ + u^- \boldsymbol{n}^-$

由于$u^\pm \in H^{1/2}(F)$，且$H^{1/2}(F)$是一个[向量空间](@entry_id:151108)，我们立即得出$\lbrace u \rbrace \in H^{1/2}(F)$。类似地，跳跃算子的每个分量都是$u^\pm$的线性组合，因此$[\boldsymbol{u}] \in (H^{1/2}(F))^d$。迹理论的严格性保证了这些[DG方法](@entry_id:748369)的核心构件是数学上良定义的。

#### 稳定项与罚参数的设计

[DG方法](@entry_id:748369)通过在[变分形式](@entry_id:166033)中加入**稳定项**（或称罚项）来弱施加单元间的连续性并保证方法的稳定性。一个典型的稳定项是SIPG罚项，它惩罚函数在交界面上的跳跃：
$$
\sum_{F \in \mathcal{F}_h^{\mathrm{int}}} \sigma_F \int_F [u_h] \cdot [v_h] \, dS
$$
（这里使用了一种跳跃为标量的约定）。为了保证DG[双线性形式](@entry_id:746794)的矫顽性（coercivity），罚参数$\sigma_F$必须选择得足够大。需要多大呢？这恰恰是由[迹不等式](@entry_id:756082)决定的。

稳定性分析表明，$\sigma_F$必须大于一个依赖于单元上[迹不等式](@entry_id:756082)和[逆不等式](@entry_id:750800)常数的阈值。
- 在**等度规网格**上，这个阈值通常与$p^2/h$成正比，其中$p$是多项式次数，$h$是单元尺寸。
- 在**[各向异性网格](@entry_id:746450)**上，正确的罚参数缩放行为至关重要。使用各向异性[迹不等式](@entry_id:756082)进行分析可知，罚参数必须与单元在**法向上的厚度**的倒数成正比[@problem_id:3425134]。即，对于面$F$，应选择$\sigma_F \sim p^2 / h_n(F)$。如果错误地使用了面直径$h_F$（例如，在扁平单元的长边上，$h_F \gg h_n(F)$），则罚参数会过小，导致在宽高比$\rho \to \infty$时稳定性丧失。

在处理低正则性问题（例如，解$u$仅属于$H^s(\Omega)$，其中$s  1/2$）时，甚至需要设计更精巧的稳定项来匹配解的真实正则性。这可能涉及惩罚前面提到的**负阶迹范数**，例如$\|[u_h]\|_{H^{s-1/2}(F)}$。这种范数本身不易计算，但可以通过引入局部**[提升算子](@entry_id:751273)**（lifting operator）来构造一个等价且可计算的稳定项[@problem_id:3425076]。

#### 离散[迹不等式](@entry_id:756082)与多项式次数的依赖性

当我们将注意力限制在单元$K$上的[多项式空间](@entry_id:144410)$V_p(K)$时，我们可以研究迹[算子范数](@entry_id:752960)对多项式次数$p$的依赖性。
首先，一个直接的结论是，多项式空间是$H^1(K)$的[子空间](@entry_id:150286)，因此标准[迹不等式](@entry_id:756082)仍然适用[@problem_id:3425092]。这意味着[迹算子](@entry_id:183665)从$V_p(K)$到$H^{1/2}(\partial K)$的范数是一致有界的，**不依赖于$p$**。
$$
\|\mathcal{T}v_p\|_{H^{1/2}(\partial K)} \le C \|v_p\|_{H^1(K)} \quad \forall v_p \in V_p(K)
$$
然而，在DG分析中，一种不同类型的[迹不等式](@entry_id:756082)——**离散[迹不等式](@entry_id:756082)**或**[逆迹不等式](@entry_id:750809)**（inverse trace inequality）——也扮演着核心角色。它用单元内部的范数来控制边界上的范数（通常是同阶的）。这种不等式的常数确实依赖于$p$。一个典型的例子是[@problem_id:3425092]：
$$
\|v_p\|_{L^2(\partial K)} \le C p h^{-1/2} \|v_p\|_{L^2(K)} \quad \forall v_p \in V_p(K)
$$
其中$h$是单元尺寸。在[仿射映射](@entry_id:746332)的情况下，该不等式简化为$\|v_p\|_{L^2(\partial K)} \le C p h^{-1/2} \|v_p\|_{L^2(K)}$。这种$p$和$h$的显式依赖性是[高阶方法](@entry_id:165413)分析中的一个关键特征。

### 矢量场的迹理论：$H(\mathrm{curl})$空间

迹理论不仅限于$H^1$等标量函数空间。在电磁学等领域，我们需要处理矢量场，其自然函数空间是$H(\mathrm{curl}, \Omega)$和$H(\mathrm{div}, \Omega)$。这里我们关注前者，它对分析Maxwell方程至关重要。$H(\mathrm{curl}, \Omega) = \{\boldsymbol{u} \in (L^2(\Omega))^3 : \nabla \times \boldsymbol{u} \in (L^2(\Omega))^3\}$。

#### 切向[迹算子](@entry_id:183665)

对于$H(\mathrm{curl})$空间中的矢量场，其法向分量和切向分量在边界上的行为截然不同。对于一个$H(\mathrm{curl})$中的场$\boldsymbol{u}$，其在边界$\Gamma = \partial\Omega$上的法向分量$\boldsymbol{u} \cdot \boldsymbol{n}$一般没有定义。然而，其**切向迹**是良定义的。事实上，存在两种互补的切向[迹算子](@entry_id:183665)[@problem_id:3425120]：

1.  **旋转切向迹 (Tangential-rotational trace)** $\gamma_t$:
    $$
    \gamma_t(\boldsymbol{u}) = \boldsymbol{n} \times \boldsymbol{u}|_\Gamma
    $$
    这个算子将$H(\mathrm{curl}, \Omega)$有界地映射到[迹空间](@entry_id:756085)$H^{-1/2}(\mathrm{div}_\Gamma, \Gamma)$。这个[迹空间](@entry_id:756085)由$\Gamma$上的切向矢量场组成，其自身和其[曲面](@entry_id:267450)散度（surface divergence）都具有$-1/2$阶的正则性。$\gamma_t$的核（kernel）正是$H_0(\mathrm{curl}, \Omega)$，即切向分量在边界上为零的场的空间。

2.  **切向分量迹 (Tangential-component trace)** $\gamma_T$:
    $$
    \gamma_T(\boldsymbol{u}) = (\boldsymbol{u} \times \boldsymbol{n}) \times \boldsymbol{n}|_\Gamma = \boldsymbol{u}_t|_\Gamma
    $$
    这个算子提取了矢量场本身的切向分量。它将$H(\mathrm{curl}, \Omega)$有界地映射到另一个[迹空间](@entry_id:756085)$H^{-1/2}(\mathrm{curl}_\Gamma, \Gamma)$。这个空间由$\Gamma$上的切向矢量场组成，其自身和其[曲面](@entry_id:267450)旋度（surface curl）都具有$-1/2$阶的正则性。

这两个[迹空间](@entry_id:756085)$H^{-1/2}(\mathrm{div}_\Gamma, \Gamma)$和$H^{-1/2}(\mathrm{curl}_\Gamma, \Gamma)$互为对偶空间。

#### [Green公式](@entry_id:173118)与Maxwell方程的边界条件

这两种切向[迹算子](@entry_id:183665)在矢量场的[Green公式](@entry_id:173118)中自然成对出现。对于任意$\boldsymbol{u}, \boldsymbol{v} \in H(\mathrm{curl}, \Omega)$，有如下的[Green公式](@entry_id:173118)[@problem_id:3425120]：
$$
\int_\Omega (\nabla \times \boldsymbol{u}) \cdot \boldsymbol{v} \, dx - \int_\Omega \boldsymbol{u} \cdot (\nabla \times \boldsymbol{v}) \, dx = \langle \gamma_t(\boldsymbol{u}), \gamma_T(\boldsymbol{v}) \rangle_\Gamma
$$
这里的$\langle \cdot, \cdot \rangle_\Gamma$表示$H^{-1/2}(\mathrm{div}_\Gamma, \Gamma)$和其[对偶空间](@entry_id:146945)$H^{-1/2}(\mathrm{curl}_\Gamma, \Gamma)$之间的对偶作用。

这个公式是推导和分析电磁问题数值方法的出发点。Maxwell方程的各种边界条件可以用这些切向迹优美地表达[@problem_id:3425120]：
- **[理想电导体](@entry_id:753331) (PEC) 边界条件**：要求[电场](@entry_id:194326)$\boldsymbol{E}$的切向分量为零。这等价于$\gamma_T(\boldsymbol{E}) = \boldsymbol{E}_t = \boldsymbol{0}$。
- **[理想磁导体](@entry_id:753334) (PMC) 边界条件**：要求[磁场](@entry_id:153296)$\boldsymbol{H}$的切向分量为零。这等价于$\gamma_T(\boldsymbol{H}) = \boldsymbol{H}_t = \boldsymbol{0}$。
- **[阻抗边界条件](@entry_id:750536) (Impedance Boundary Condition)**：将电场和磁场的切向分量联系起来，例如$\boldsymbol{n} \times (\boldsymbol{n} \times \boldsymbol{E}) = Z (\boldsymbol{n} \times \boldsymbol{H})$，其中$Z$是阻抗。这可以简洁地写成迹的形式：$\gamma_t(\boldsymbol{E}) = -Z \gamma_t(\boldsymbol{H})$。

在[DG方法](@entry_id:748369)中，单元交界面上电场和磁场切向分量的连续性是通过对$\gamma_t$和$\gamma_T$迹的跳跃项和平均项进行控制来实现的。这再次凸显了迹理论作为设计和理解高级数值方案的通用语言的强大功能。