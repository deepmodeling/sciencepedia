## 引言

在[几何分析](@entry_id:157700)领域，对[曲面](@entry_id:267450)及其性质的研究占据着核心地位。然而，经典[微分几何](@entry_id:145818)的工具在处理带有[奇点](@entry_id:137764)（如肥[皂膜](@entry_id:267628)的交点）或在[变分问题](@entry_id:756445)中作为极限出现的“退化”[曲面](@entry_id:267450)时，往往会显得力不从心。为了克服这些局限性，[几何测度论](@entry_id:187987)发展出了一套强大的框架，其核心概念之一便是“[流形](@entry_id:153038)”（varifold）。[流形理论](@entry_id:263722)为我们提供了一种严谨的方式来研究和分析这些广义[曲面](@entry_id:267450)，使其成为现代几何[变分问题](@entry_id:756445)的基石。

本文旨在系统性地介绍[流形理论](@entry_id:263722)的入门知识，重点聚焦于[面积的第一变分](@entry_id:195526)及其深刻的几何意义。我们将揭示这一看似抽象的变分概念如何自然地引出[广义平均曲率](@entry_id:199614)，并最终定义了作为广义[极小曲面](@entry_id:157732)的“平[稳流](@entry_id:266861)形”。通过本文的学习，读者将能够理解[流形理论](@entry_id:263722)如何为处理不光滑几何对象提供坚实的分析基础。

文章将分为三个核心部分展开：
- **原理与机制**：本章将从[流形](@entry_id:153038)的基本定义出发，详细阐述其作为广义[曲面](@entry_id:267450)的数学构造。我们将深入探讨面积[第一变分](@entry_id:174697)的计算与结构，并介绍其如何定义平[稳流](@entry_id:266861)形与[广义平均曲率](@entry_id:199614)。最后，我们将学习Allard的两大基本定理，它们是连接[流形理论](@entry_id:263722)与经典几何的桥梁。
- **应用与跨学科联系**：在理论基础之上，本章将展示[流形理论](@entry_id:263722)的强大应用价值。我们将探讨其在极小曲面稳定性与[奇点分析](@entry_id:198717)、[自由边界问题](@entry_id:636836)、以及纯粹数学中里程碑式的[存在性定理](@entry_id:261096)（如Almgren-Pitts理论）中的作用。此外，我们还将探索其与[材料科学](@entry_id:152226)、[几何流](@entry_id:195216)等领域的深刻联系。
- **动手实践**：为了巩固理论知识，本章将提供一系列精心设计的实践问题，引导读者亲手计算[流形](@entry_id:153038)的构造、[第一变分](@entry_id:174697)以及相关几何量，从而将抽象概念转化为具体的计算技能。

通过这一结构化的学习路径，我们将从基本原理走向前沿应用，全面掌握[流形](@entry_id:153038)与面积[第一变分](@entry_id:174697)的核心内容。

## 原理与机制

本章旨在深入探讨[流形](@entry_id:153038)（varifold）理论的核心原理与机制。我们将从[流形](@entry_id:153038)的基本定义出发，阐明其作为广义[曲面](@entry_id:267450)的数学形式。随后，我们将引入[面积的第一变分](@entry_id:195526)，并展示它如何引出[广义平均曲率](@entry_id:199614)的概念，以及作为[变分问题](@entry_id:756445)[欧拉-拉格朗日方程](@entry_id:137827)[弱形式](@entry_id:142897)的[平稳性条件](@entry_id:191085)。最后，我们将介绍Allard的[可求长性](@entry_id:202091)（rectifiability）和正则性（regularity）两大基本定理，它们揭示了[流形](@entry_id:153038)在何种条件下具备良好的几何结构（即可求长的，甚至是光滑的）。

### 基本概念：作为广义[曲面](@entry_id:267450)的[流形](@entry_id:153038)

在[几何测度论](@entry_id:187987)中，[流形](@entry_id:153038)提供了一个强大框架，用于研究和分析比光滑[嵌入子流形](@entry_id:273162)更广泛的几何对象，例如带[奇异点](@entry_id:199525)的[曲面](@entry_id:267450)或测度意义下的极限[曲面](@entry_id:267450)。

#### [流形](@entry_id:153038)的定义

一个在$\mathbb{R}^n$中的**$k$-维[流形](@entry_id:153038)**（$k$-varifold）$V$ 被定义为在乘[积空间](@entry_id:151693)$\mathbb{R}^n \times G(n,k)$上的一个[拉东测度](@entry_id:188027)（Radon measure）。其中，$G(n,k)$ 是$\mathbb{R}^n$中所有$k$维无定向[线性子空间](@entry_id:151815)构成的格拉斯曼[流形](@entry_id:153038)（Grassmannian）。[@problem_id:3037016] 这个定义在直观上捕捉了一个广义[曲面](@entry_id:267450)的本质：在每一点$x \in \mathbb{R}^n$，“附近”可能存在着不同方向的“[切空间](@entry_id:199137)”$S \in G(n,k)$，而测度$V$ 则量化了在点$x$ 处以$S$ 为切空间的“[曲面](@entry_id:267450)”的密度或权重。

#### [流形](@entry_id:153038)的无定向性

选择无定向的格拉斯曼[流形](@entry_id:153038)$G(n,k)$是[流形理论](@entry_id:263722)的一个根本特征。其动机源于[流形理论](@entry_id:263722)主要用于研究[面积泛函](@entry_id:635965)的[变分问题](@entry_id:756445)，而**面积**本身是一个不依赖于定向的几何量。例如，一个光滑[曲面](@entry_id:267450)的面积是通过对面积元$\mathrm{d}\mathcal{H}^k$进行积分得到的，这个[面积元](@entry_id:263205)不因[曲面](@entry_id:267450)定向的改变而改变。

与此形成鲜明对比的是**[整流](@entry_id:197363)（integral current）**理论，后者建立在有定向的格拉斯曼[流形](@entry_id:153038)$\widetilde{G}(n,k)$之上。[整流](@entry_id:197363)理论旨在推广带有边界的有向[曲面](@entry_id:267450)，并保留[斯托克斯定理](@entry_id:264534)（Stokes' Theorem）的结构，而这一定理的[边界算子](@entry_id:160216)$\partial$的定义本质上依赖于定向。因此，当我们反转一个[流形](@entry_id:153038)$M$ 的定向时，其关联的整流$T_M$会变为$-T_M$，而关联的[流形](@entry_id:153038)$V_M$则保持不变。[@problem_id:3037023] [@problem_id:3036972] 这种差异也体现在叠加效应上：两个方向相反的[整流](@entry_id:197363)$T_M$和$-T_M$叠加会相互抵消，得到零整流；而两个相同的[流形](@entry_id:153038)$V_M$叠加则会得到一个重数为2的新[流形](@entry_id:153038)，其质量是原来的两倍。[@problem_id:3036972] 这正体现了[流形](@entry_id:153038)“累积质量”而[整流](@entry_id:197363)“计入代数抵消”的本质区别。

#### 权重测度与质量

每个$k$-维[流形](@entry_id:153038)$V$ 都关联着一个定义在$\mathbb{R}^n$上的**权重测度**（weight measure）$\mu_V$。它是[流形](@entry_id:153038)测度$V$ 在[投影映射](@entry_id:153398)$\pi: \mathbb{R}^n \times G(n,k) \to \mathbb{R}^n$（即$\pi(x,S) = x$）下的推[前测度](@entry_id:192696)（pushforward measure）。对任意$\mathbb{R}^n$中的[博雷尔集](@entry_id:144507)$A$，其定义为：
$$
\mu_V(A) = V(A \times G(n,k))
$$
由于$V$ 是一个[拉东测度](@entry_id:188027)，且$G(n,k)$ 是紧的，可以证明$\mu_V$也是$\mathbb{R}^n$上的一个[拉东测度](@entry_id:188027)。[@problem_id:3037016] 权重测度$\mu_V(A)$描述了广义[曲面](@entry_id:267450)在集合$A$中的总“质量”或“面积”，它忽略了切空间在各点的具体朝向。

根据推[前测度](@entry_id:192696)的[积分变换](@entry_id:186209)公式，对任意有界博雷尔函数$f: \mathbb{R}^n \to \mathbb{R}$，我们有：
$$
\int_{\mathbb{R}^n} f(x)\, d\mu_V(x) = \int_{\mathbb{R}^n \times G(n,k)} f(x)\, dV(x,S)
$$
[@problem_id:3037016]

#### 可求长[流形](@entry_id:153038)与整流形

在所有[流形](@entry_id:153038)中，最重要的一类是**可求长[流形](@entry_id:153038)**（rectifiable varifolds），它们对应于我们传统观念中的[曲面](@entry_id:267450)。

首先，一个集合$S \subset \mathbb{R}^n$被称为**可数$k$-可求长的**（countably $k$-rectifiable），如果它能被可数个$\mathbb{R}^k$的$C^1$像所覆盖，除去一个$k$-维[豪斯多夫测度](@entry_id:200740)（Hausdorff measure）为零的零集。对于这样的集合，在$\mathcal{H}^k$-几乎所有的点$x \in S$处，其**近似切空间**（approximate tangent plane）$T_x S \in G(n,k)$都是良定义的。

一个$k$-维[流形](@entry_id:153038)$V$ 被称为**可求长的**，如果存在一个可数$k$-[可求长集](@entry_id:635569)$S \subset \mathbb{R}^n$和一个非负的、在$S$上局部$\mathcal{H}^k$-可积的**[重数](@entry_id:136466)函数**$\theta \in L^1_{\mathrm{loc}}(\mathcal{H}^k \llcorner S)$，使得$V$ 可以表示为：
$$
V = \int_S \delta_{(x, T_x S)} \theta(x) \, \mathrm{d}\mathcal{H}^k(x)
$$
这意味着对任意检验函数$\varphi \in C_c^0(\mathbb{R}^n \times G(n,k))$，有：
$$
\int_{\mathbb{R}^n \times G(n,k)} \varphi(x,P) \, \mathrm{d}V(x,P) = \int_S \varphi(x, T_x S) \, \theta(x) \, \mathrm{d}\mathcal{H}^k(x)
$$
[@problem_id:3036991] 此时，其权重测度为$\mu_V = \theta \, \mathcal{H}^k \llcorner S$。需要强调的是，一个[流形](@entry_id:153038)的权重测度是可求长的（即形如$\theta \, \mathcal{H}^k \llcorner S$），并不足以保证[流形](@entry_id:153038)本身是可求长的。因为[流形](@entry_id:153038)还包含了切空间[分布](@entry_id:182848)的信息，而权重测度没有。[@problem_id:3036991]

若一个可求长[流形](@entry_id:153038)的重数函数$\theta(x)$在$\mathcal{H}^k$-几乎处处取正整数值，则称该[流形](@entry_id:153038)为**[整流](@entry_id:197363)形**（integral varifold）。[@problem_id:3036991]

### [面积的第一变分](@entry_id:195526)

[第一变分](@entry_id:174697)是分析[面积泛函](@entry_id:635965)[临界点](@entry_id:144653)的核心工具，它在[流形理论](@entry_id:263722)中扮演着中心角色。

#### 定义

[流形](@entry_id:153038)$V$ 在一个[紧支撑](@entry_id:276214)$C^1$ 向量场$X \in C_c^1(\mathbb{R}^n; \mathbb{R}^n)$方向上的**[第一变分](@entry_id:174697)**$\delta V(X)$定义为：
$$
\delta V(X) = \int_{\mathbb{R}^n \times G(n,k)} \operatorname{div}_S X(x) \, dV(x,S)
$$
其中$\operatorname{div}_S X(x)$是向量场$X$ 沿[切空间](@entry_id:199137)$S$ 的**切向散度**（tangential divergence）。若$\{e_1, \dots, e_k\}$是$S$ 的一个标准正交基，则$\operatorname{div}_S X(x) = \sum_{i=1}^k \langle D_x X(e_i), e_i \rangle$。这个量描述了由$X$ 生成的流在$S$ 方向上使[面积元](@entry_id:263205)产生的无穷小变化率。

值得注意的是，切向散度$\operatorname{div}_S X$通常不等于背景空间中的全散度$\operatorname{div} X$。[@problem_id:3037016] 全散度是所有方向上变化率的总和，而切向散度只考虑沿给定$k$-维[子空间](@entry_id:150286)的变化。

对于一个由光滑无边$k$-维[子流形](@entry_id:159439)$M$ 和单位重数生成的[流形](@entry_id:153038)$V_M$，其[第一变分](@entry_id:174697)与经典定义相符：
$$
\delta V_M(X) = \int_M \operatorname{div}_M X \, d\mathcal{H}^k
$$
其中$\operatorname{div}_M X$是$X$ 沿[流形](@entry_id:153038)$M$ 的切向散度，即$\operatorname{div}_{T_x M} X(x)$。[@problem_id:3037016]

#### [第一变分](@entry_id:174697)公式的结构

通过在[流形](@entry_id:153038)上应用散度定理，我们可以揭示[第一变分](@entry_id:174697)公式的[精细结构](@entry_id:140861)。考虑一个由$C^2$ [流形](@entry_id:153038)$M$ 和$C^1$ 权重函数$w$ 生成的可求长[流形](@entry_id:153038)$V_w$。其[第一变分](@entry_id:174697)$\delta V_w(X) = \int_M w(x) \operatorname{div}_M X(x) \, d\mathcal{H}^k(x)$。利用[散度定理](@entry_id:143110)和[分部积分](@entry_id:136350)，可以推导出如下重要的公式：
$$
\delta V_w(X) = - \int_M \langle X, w(x)H(x) + \nabla^M w(x) \rangle \, d\mathcal{H}^k(x) + \int_{\partial M} w(x) \langle X(x), \nu(x) \rangle \, d\mathcal{H}^{k-1}(x)
$$
[@problem_id:3037021] 这里，$H(x)$ 是[流形](@entry_id:153038)$M$ 在点$x$ 的**[平均曲率向量](@entry_id:199617)**（mean curvature vector），$\nabla^M w$是权重函数$w$ 在$M$ 上的切向梯度，而$\nu$是边界$\partial M$在$M$ 中的向外单位**余[法向量](@entry_id:264185)**（conormal vector）。

这个公式表明，[第一变分](@entry_id:174697)由两部分贡献：一部分是来自[流形](@entry_id:153038)内部的积分，它与[平均曲率](@entry_id:162147)和权重函数的梯度有关；另一部分是来自[流形](@entry_id:153038)边界的积分。这清楚地显示了[第一变分](@entry_id:174697)如何捕捉到[曲面](@entry_id:267450)的内在几何（曲率）和边界行为。

### 平[稳流](@entry_id:266861)形与[广义平均曲率](@entry_id:199614)

[第一变分](@entry_id:174697)公式为定义弱意义下的[极小曲面](@entry_id:157732)（即平[稳流](@entry_id:266861)形）和[广义平均曲率](@entry_id:199614)铺平了道路。

#### [广义平均曲率](@entry_id:199614)

对于一般的[流形](@entry_id:153038)$V$，其[第一变分](@entry_id:174697)$\delta V$是一个向量值的[分布](@entry_id:182848)。如果这个[分布](@entry_id:182848)可以被一个向量值的[拉东测度](@entry_id:188027)表示，我们就称$V$ 具有**局部有界[第一变分](@entry_id:174697)**。进一步，如果$\delta V$关于权重测度$\mu_V$是绝对连续的（记作$\delta V \ll \mu_V$），即任何$\mu_V$-零测集上的[第一变分](@entry_id:174697)也为零，那么根据拉东-尼科迪姆（Radon-Nikodym）定理，存在一个$\mu_V$-可测的向量场$H_V$，使得：
$$
d(\delta V) = -H_V \, d\mu_V
$$
这个向量场$H_V$ 被称为[流形](@entry_id:153038)$V$ 的**[广义平均曲率](@entry_id:199614)向量**。[@problem_id:3037015] 它是在$\mu_V$-[几乎处处](@entry_id:146631)唯一确定的$L^1_{\mathrm{loc}}(\mu_V; \mathbb{R}^n)$ 函数。

有了$H_V$，[第一变分](@entry_id:174697)可以写成一个更直观的[弱形式](@entry_id:142897)（weak formulation）：
$$
\delta V(X) = - \int_{\mathbb{R}^n} \langle X(x), H_V(x) \rangle \, d\mu_V(x)
$$
[@problem_id:3037015] [@problem_id:3036976] 这个公式是广义[曲面](@entry_id:267450)理论的基石，它将抽象的变分概念与一个具体的、[几乎处处](@entry_id:146631)定义的几何量——平均曲率——联系起来。

#### 平[稳流](@entry_id:266861)形与[极小曲面方程](@entry_id:187309)

一个[流形](@entry_id:153038)$V$ 如果对于任意[紧支撑](@entry_id:276214)向量场$X$ 都满足$\delta V(X) = 0$，则称之为**平[稳流](@entry_id:266861)形**（stationary varifold）。这一定义是[面积泛函](@entry_id:635965)的[欧拉-拉格朗日方程](@entry_id:137827)的弱形式。

从[广义平均曲率](@entry_id:199614)的定义可以看出，一个[流形](@entry_id:153038)是平稳的，当且仅当其[广义平均曲率](@entry_id:199614)在$\mu_V$-几乎处处为零，即$H_V = 0$。[@problem_id:3036976] 因此，平[稳流](@entry_id:266861)形正是广义的、弱意义下的[极小曲面](@entry_id:157732)。它们可以包含经典[极小曲面](@entry_id:157732)无法描述的[奇异点](@entry_id:199525)。一个简单的例子是$\mathbb{R}^n$中的任何$k$-维平面，它是一个平[稳流](@entry_id:266861)形，但其支撑集的[勒贝格测度](@entry_id:139781)为零。[@problem_id:3037016]

这种联系在研究函数图像时尤为清晰。对于一个$C^2$ 函数$u: \Omega \subset \mathbb{R}^n \to \mathbb{R}$，其图像$\Sigma = \{(x, u(x))\}$所诱导的[流形](@entry_id:153038)是平稳的，当且仅当$u$ 满足经典的**[极小曲面方程](@entry_id:187309)**（minimal surface equation）：
$$
\operatorname{div}\left(\frac{Du}{\sqrt{1+|Du|^{2}}}\right) = 0
$$
[@problem_id:3036976] 对于正则性更低的索伯列夫函数（Sobolev function）$u$，平稳性则等价于该方程的[弱形式](@entry_id:142897)。[@problem_id:3036976] 需要注意的是，[极小曲面方程](@entry_id:187309)是一个[非线性](@entry_id:637147)的[偏微分方程](@entry_id:141332)，它不同于线性的拉普拉斯方程$\Delta u = 0$。[@problem_id:3036976]

### [流形](@entry_id:153038)的结构与正则性

[流形理论](@entry_id:263722)的深刻之处在于它不仅提供了一个广义的框架，还包含了一系列强大的定理，用以说明在适当的分析条件下，一个抽象的[流形](@entry_id:153038)确实具有良好的几何结构。

#### [流形](@entry_id:153038)的收敛性

序列$\{V_i\}$**收敛**到[流形](@entry_id:153038)$V$，是指$V_i$作为$\mathbb{R}^n \times G(n,k)$上的[拉东测度](@entry_id:188027)[弱*收敛](@entry_id:196227)到$V$。这意味着对所有[检验函数](@entry_id:166589)$\varphi \in C_c^0(\mathbb{R}^n \times G(n,k))$，积分$\int \varphi \, dV_i$收敛到$\int \varphi \, dV$。[@problem_id:3037022]

由于$\operatorname{div}_S X(x)$是一个合法的检验函数，[流形](@entry_id:153038)的收敛性直接蕴含了[第一变分](@entry_id:174697)的收敛性：$\delta V_i(X) \to \delta V(X)$。[@problem_id:3037022] 此外，如果一列[流形](@entry_id:153038)的[第一变分](@entry_id:174697)的总变差是一致有界的（$\sup_i \|\delta V_i\|  \infty$），那么极限[流形](@entry_id:153038)的[第一变分](@entry_id:174697)也是一个有界测度，并且其总变差满足下半连续性：$\|\delta V\| \le \liminf_{i\to\infty} \|\delta V_i\|$。[@problem_id:3037022] 这是Allard紧性定理的关键组成部分。

[流形](@entry_id:153038)的收敛性与[整流](@entry_id:197363)的**平坦收敛**（flat convergence）有本质区别。平坦收敛允许质量因定向相反的[曲面](@entry_id:267450)相互靠近而抵消。而[流形](@entry_id:153038)收敛则总是累积质量。一个典型的例子是，一列相互抵消的整流$T_i$可以平坦收敛到零，但它们对应的[流形](@entry_id:153038)序列$V_{T_i}$却可以收敛到一个质量不为零的、重数为2的[流形](@entry_id:153038)。[@problem_id:3037022]

#### Allard [可求长性](@entry_id:202091)定理

一个自然而深刻的问题是：一个一般的[流形](@entry_id:153038)在何种条件下才是一个真正意义上的“[曲面](@entry_id:267450)”（即[可求长集](@entry_id:635569)）？**Allard[可求长性](@entry_id:202091)定理**（Allard's Rectifiability Theorem）给出了一个优雅的回答。

**定理 (Allard, 1972):** 设$V$ 是一个$\mathbb{R}^n$中的$k$-维[流形](@entry_id:153038)。若
1.  $V$ 具有局部有界[第一变分](@entry_id:174697)；
2.  其权重测度$\mu_V$的$k$-维密度$\Theta^k(\mu_V, x) = \lim_{r \to 0} \frac{\mu_V(B_r(x))}{\omega_k r^k}$在$\mu_V$-几乎所有的点$x$都存在且为正有限值。

则$V$ 是一个$k$-可求长[流形](@entry_id:153038)。[@problem_id:3036992]

直观上，密度条件保证了在无穷小尺度上，[流形](@entry_id:153038)看起来像一个$k$-维平面；而有界[第一变分](@entry_id:174697)条件则提供了足够的分析控制，排除了那些虽然满足密度条件但结构过于“卷曲”或“分形”的非可求长对象。

#### Allard 正则性定理

[可求长性](@entry_id:202091)定理告诉我们[流形](@entry_id:153038)的“存在性”，而**[Allard正则性定理](@entry_id:204743)**（Allar[d'](@entry_id:189153)s Regularity Theorem）则更进一步，回答了何时一个可求长[流形](@entry_id:153038)是“光滑”的。这是一个$\varepsilon$-正则性结果。

为了陈述该定理，我们需要引入**倾斜过度量**（tilt-excess），它度量了[流形](@entry_id:153038)的切空间在一个球内偏离某个固定平面$P$的平均程度。同时，我们还需要一个[尺度不变的](@entry_id:178566)平均曲率积分量。

**定理 (Allard, 1975):** 设$V$ 是一个$k$-维可求长[流形](@entry_id:153038)，其[广义平均曲率](@entry_id:199614)$H_V \in L^p(\mu_V)$，其中$p > k$。对任意给定的$k, n, p$，存在一个正常数$\varepsilon_0 > 0$，使得如果在一个球$B_\rho(x_0)$中，$V$ 的密度比接近1，并且其倾斜过度量和[尺度不变的](@entry_id:178566)$L^p$-曲率积分都小于$\varepsilon_0$，那么在一个更小的球$B_{\gamma\rho}(x_0)$内，$V$ 的支撑集是一个$C^{1, \alpha}$ 函数的图像。其中，Hölder指数$\alpha = 1 - k/p$。[@problem_id:3037003]

这个深刻的定理是[几何分析](@entry_id:157700)的巅峰成果之一。它表明，如果一个广义[曲面](@entry_id:267450)在某个尺度上足够“平坦”且其[平均曲率](@entry_id:162147)足够“小”，那么它在该尺度附近必然是光滑的。这为从弱的、测度论的设定过渡到强的、[微分几何](@entry_id:145818)的结论提供了坚实的桥梁，构成了分析极小曲面及其[奇异点](@entry_id:199525)集合的理论基础。