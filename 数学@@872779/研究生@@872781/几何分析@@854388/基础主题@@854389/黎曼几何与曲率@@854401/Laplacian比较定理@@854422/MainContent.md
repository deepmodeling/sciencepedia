## 引言
在黎曼几何中，一个核心问题是：空间的局部弯曲程度（曲率）如何决定其整体的几何与拓扑结构？[拉普拉斯比较定理](@entry_id:194055)为回答这一问题提供了最强有力的分析工具之一。它通过一个看似简单的[微分不等式](@entry_id:137452)，精确地量化了[Ricci曲率](@entry_id:162038)对空间中[测地线汇](@entry_id:160274)聚或发散行为的影响，从而在局部曲率与全局性质之间架起了一座坚实的桥梁。本文旨在对[拉普拉斯比较定理](@entry_id:194055)进行系统而深入的探讨，从基本原理到前沿应用，为读者构建一个完整的知识框架。我们将分三个章节展开：首先，在“原理与机制”一章中，我们将从[拉普拉斯算子](@entry_id:146319)和距离函数等基本概念出发，详细剖析[比较定理](@entry_id:637672)的证明机制，揭示[Bochner公式](@entry_id:187951)与[Riccati方程](@entry_id:184132)在其中的关键作用。接着，在“应用与跨学科联系”一章中，我们将展示该定理如何催生出诸如体积比较、[刚性定理](@entry_id:198222)和[分裂定理](@entry_id:197795)等一系列深刻的几何结论，并探讨其在[谱几何](@entry_id:186460)、[几何流](@entry_id:195216)和[随机过程](@entry_id:159502)等领域的广泛影响。最后，通过“动手实践”部分中的具体计算练习，读者将有机会亲手应用这些理论，加深对核心概念的理解。让我们首先进入第一章，从最基本的定义开始，探索这些强大定理的内在构造。

## 原理与机制

本章旨在深入探讨[拉普拉斯比较定理](@entry_id:194055)的内在原理与核心机制。我们将从定义[黎曼流形](@entry_id:261160)上的核心算子——[拉普拉斯-贝尔特拉米算子](@entry_id:267002)（Laplace-Beltrami operator）入手，进而研究距离函数及其拉普拉斯量的几何意义。在此基础上，我们将陈述核心的[拉普拉斯比较定理](@entry_id:194055)，并通过分析其证明机制来揭示曲率如何控制几何。最后，我们将讨论该定理的一系列深刻推论及其在更广义的[度量测度空间](@entry_id:180197)中的推广。

### 黎曼[流形上的拉普拉斯算子](@entry_id:184243)

在[黎曼几何](@entry_id:160508)分析中，[拉普拉斯-贝尔特拉米算子](@entry_id:267002)（或简称为[拉普拉斯算子](@entry_id:146319)）是一个典范的二阶[椭圆微分算子](@entry_id:635792)，它将欧几里得空间中的标准[拉普拉斯算子](@entry_id:146319)推广到[黎曼流形](@entry_id:261160) $(M, g)$ 上。该算子的一个关键特性是其**内在性**（intrinsically defined），即它的定义完全依赖于[流形](@entry_id:153038)的黎曼度量，而与任何特定的[局部坐标系](@entry_id:751394)选择无关。

我们可以通过两种等价的、坐标无关的方式来定义作用于光滑函数 $f \in C^\infty(M)$ 上的拉普拉斯算子 $\Delta f$。

第一种定义是构造性的，通过组合梯度和散度这两个同样内在的算子得到。
首先，我们定义函数 $f$ 的**梯度**（gradient）向量场 $\nabla f$。它是由度量 $g$ 通过对偶关系唯一确定的向量场，满足对任意向量场 $X$，都有 $g(\nabla f, X) = df(X)$。这里 $df$ 是 $f$ 的外微分，是一个[1-形式](@entry_id:270392)。
其次，我们定义向量场 $X$ 的**散度**（divergence）$\operatorname{div} X$。它是一个标量函数，描述了 $X$ 产生的流在每一点上使体积元发生变化的无穷小率。其内在定义为 $\mathcal{L}_X \mu_g = (\operatorname{div} X) \mu_g$，其中 $\mu_g$ 是[黎曼体积形式](@entry_id:275973)，$\mathcal{L}_X$ 表示沿向量场 $X$ 的[李导数](@entry_id:171745)。
基于这两个定义，拉普拉斯算子被定义为[梯度场](@entry_id:264143)的散度：
$$
\Delta f := \operatorname{div}(\nabla f)
$$
由于梯度和散度的定义都只依赖于度量 $g$ 及其诱导的体积形式 $\mu_g$，它们的复合算子 $\Delta$ 显然也是一个内在的标量微分算子。在任意[局部坐标系](@entry_id:751394) $(x^1, \dots, x^n)$ 中，若度量矩阵为 $(g_{ij})$，其逆矩阵为 $(g^{ij})$，体积元为 $\sqrt{\det g} \, dx^1 \wedge \dots \wedge dx^n$，则上述定义可具体表示为以下公式：
$$
\Delta f = \frac{1}{\sqrt{\det g}} \sum_{i,j=1}^n \frac{\partial}{\partial x^i} \left( \sqrt{\det g} \, g^{ij} \frac{\partial f}{\partial x^j} \right)
$$
这个公式明确展示了算子对度量及其导数的依赖性，并保证了在坐标变换下的[不变性](@entry_id:140168)。[@problem_id:3031713]

第二种定义是变分的或弱的定义，它通过积分恒等式来刻画[拉普拉斯算子](@entry_id:146319)。对于无边界的[流形](@entry_id:153038)，$\Delta$ 是唯一满足以下条件的[微分算子](@entry_id:140145)：对所有具有[紧支集](@entry_id:276214)的测试函数 $u, v \in C_c^\infty(M)$，[格林第一恒等式](@entry_id:170345)（Green's first identity）成立：
$$
\int_M u (\Delta v) \, d\mu_g = - \int_M \langle \nabla u, \nabla v \rangle_g \, d\mu_g
$$
其中 $\langle \cdot, \cdot \rangle_g$ 是由度量 $g$ 诱导的逐点[内积](@entry_id:158127)，$d\mu_g$ 是黎曼体[积测度](@entry_id:266846)。这个积分公式的两边都是由内蕴的几何量（函数、梯度、[内积](@entry_id:158127)、[体积元](@entry_id:267802)）定义的，因此它提供了一个完全内在的、不依赖于坐标的拉普拉斯算子特征。这个定义在[偏微分方程](@entry_id:141332)的现代理论中尤为重要。[@problem_id:3031713]

### 距离函数的几何学与平均曲率

[拉普拉斯比较定理](@entry_id:194055)的核心研究对象是**[黎曼距离函数](@entry_id:198905)**。给定[流形](@entry_id:153038) $M$ 上一点 $p$，距离函数 $r(x) := d(p,x)$ 测量了点 $x$ 到 $p$ 的[最短路径](@entry_id:157568)长度。除了点 $p$ 本身以及 $p$ 的**[割迹](@entry_id:161337)**（cut locus）$\operatorname{Cut}(p)$ 之外，$r(x)$ 是一个[光滑函数](@entry_id:267124)。[割迹](@entry_id:161337)是这样一个点集，从 $p$ 出发的[测地线](@entry_id:269969)在到达该点后便不再是唯一的[极小测地线](@entry_id:636159)。在光滑区域 $M \setminus (\{p\} \cup \operatorname{Cut}(p))$ 内，梯度 $\nabla r$ 是一个单位向量场，指向沿[极小测地线](@entry_id:636159)远离 $p$ 的方向。

为了研究 $\Delta r$ 的几何意义，我们引入**[测地极坐标](@entry_id:194605)**（geodesic polar coordinates）。在 $p$ 点的一个邻域内（不含[割迹](@entry_id:161337)），任何点 $x$ 可以由它到 $p$ 的距离 $r(x)$ 和从 $p$ 出发到达 $x$ 的唯一[极小测地线](@entry_id:636159)的初始[方向向量](@entry_id:169562) $\theta \in S^{n-1} \subset T_pM$ 唯一确定。在该[坐标系](@entry_id:156346) $(r, \theta)$下，[黎曼度量](@entry_id:754359)具有特殊形式：
$$
g = dr^2 + G(r, \theta)
$$
其中 $G(r, \theta)$ 是一个依赖于 $r$ 和 $\theta$ 的 $(n-1) \times (n-1)$ 正定矩阵，代表了在半径为 $r$ 的[测地球](@entry_id:201133)面上的度量。黎曼体积元可以写作 $d\mu_g = J(r, \theta) dr d\theta$，其中 $J(r, \theta) = \sqrt{\det G(r, \theta)}$ 称为**体积密度函数**。

在此[坐标系](@entry_id:156346)下，我们可以直接计算距离函数 $r$ 的拉普拉斯。由于 $r$ 仅依赖于坐标 $r$，其梯度为 $\nabla r = \partial_r$。根据[拉普拉斯算子](@entry_id:146319)的坐标表达式，我们得到：
$$
\Delta r = \frac{1}{J(r,\theta)} \frac{\partial}{\partial r} \left( J(r, \theta) g^{rr} \frac{\partial r}{\partial r} \right) = \frac{1}{J(r,\theta)} \frac{\partial J(r,\theta)}{\partial r} = \frac{\partial}{\partial r} \big(\log J(r,\theta)\big)
$$
这个结果揭示了一个深刻的几何联系：$\Delta r$ 描述了体积密度函数沿径向的对数变化率。另一方面，一个经典的[黎曼几何](@entry_id:160508)结果指出，半径为 $r$ 的[测地球](@entry_id:201133)面 $S_r(p)$ 相对于向外的[单位法向量](@entry_id:178851) $\nabla r = \partial_r$ 的**平均曲率**（mean curvature） $H$ 也由同一表达式给出。因此，我们得到一个至关重要的等式：
$$
\Delta r = H(S_r(p))
$$
即距离函数的拉普拉斯量等于测地 球面的平均曲率。这个等式将一个分析量（$\Delta r$）和一个几何量（$H$）联系起来，是[比较定理](@entry_id:637672)的桥梁。[@problem_id:3031709] [@problem_id:3031723]

### [拉普拉斯比较定理](@entry_id:194055)

[拉普拉斯比较定理](@entry_id:194055)的核心思想是：一个黎曼流形的[Ricci曲率](@entry_id:162038)如果有一个下界，那么它的测地球面[平均曲率](@entry_id:162147)（即 $\Delta r$）就相应地有一个[上界](@entry_id:274738)，这个上界由一个具有恒定曲率的“[模型空间](@entry_id:635763)”给出。

为了精确陈述该定理，我们需要定义[模型空间](@entry_id:635763)中的几何量。$n$ 维**[常曲率空间](@entry_id:161841)形式**（space form）$M_\kappa^n$ 是指具有[常截面曲率](@entry_id:272200) $\kappa$ 的单连通[完备黎曼流形](@entry_id:182954)。
- 若 $\kappa > 0$，它是球面 $\mathbb{S}^n$（适当缩放）。
- 若 $\kappa = 0$，它是欧几里得空间 $\mathbb{R}^n$。
- 若 $\kappa  0$，它是双曲空间 $\mathbb{H}^n$。

在 $M_\kappa^n$ 中，[测地球](@entry_id:201133)面 $S_r(p)$ 的几何性质是各向同性的，仅依赖于半径 $r$。描述这些性质的关键函数是 $s_\kappa(r)$，它是以下[二阶常微分方程](@entry_id:204212)（标量[Jacobi方程](@entry_id:158713)）的唯一解：
$$
s_\kappa''(r) + \kappa s_\kappa(r) = 0, \quad \text{初始条件为} \quad s_\kappa(0) = 0, \ s_\kappa'(0) = 1
$$
根据 $\kappa$ 的值的不同，我们可以解出 $s_\kappa(r)$ 的具体形式 [@problem_id:3031706]：
- **$\kappa=1$** (球面模型): $s_1(r) = \sin(r)$
- **$\kappa=0$** (欧氏模型): $s_0(r) = r$
- **$\kappa=-1$** (双曲模型): $s_{-1}(r) = \sinh(r)$

在 $M_\kappa^n$ 中，距离函数 $r$ 的拉普拉斯量，我们记为 $m_\kappa(r)$，完全由 $s_\kappa(r)$ 决定：
$$
m_\kappa(r) = (n-1) \frac{s_\kappa'(r)}{s_\kappa(r)}
$$
这个量也被称为**[模型平均](@entry_id:635177)曲率**。具体来说 [@problem_id:2984944] [@problem_id:3031728]：
- 若 $\kappa > 0$: $m_\kappa(r) = (n-1)\sqrt{\kappa}\cot(\sqrt{\kappa}r)$
- 若 $\kappa = 0$: $m_0(r) = \frac{n-1}{r}$
- 若 $\kappa  0$: $m_\kappa(r) = (n-1)\sqrt{-\kappa}\coth(\sqrt{-\kappa}r)$

现在我们可以陈述定理。

**定理（[拉普拉斯比较定理](@entry_id:194055)）**：
设 $(M^n, g)$ 是一个[完备黎曼流形](@entry_id:182954)，其Ricci曲率满足 $\operatorname{Ric} \ge (n-1)\kappa$ 对于某个常数 $\kappa \in \mathbb{R}$ 成立。令 $r(x)=d(p,x)$ 为到[固定点](@entry_id:156394) $p$ 的距离函数。那么，在 $r$ 光滑的区域 $M \setminus (\{p\} \cup \operatorname{Cut}(p))$ 内，以下不等式成立：
$$
\Delta r(x) \le m_\kappa(r(x))
$$
这个不等式在[分布](@entry_id:182848)意义下（in the sense of distributions）在整个 $M \setminus \{p\}$ 上都成立。[@problem_id:3031728] [@problem_id:2984944]

### 机制：[Bochner公式](@entry_id:187951)与[Riccati方程](@entry_id:184132)

[拉普拉斯比较定理](@entry_id:194055)的证明深刻地揭示了曲率、Hessian和拉普拉斯算子之间的相互作用。其核心工具是**[Bochner恒等式](@entry_id:193184)**和一个Riccati型[微分方程](@entry_id:264184)的[比较原理](@entry_id:165563)。

对于任何[光滑函数](@entry_id:267124) $u$，[Bochner恒等式](@entry_id:193184)给出了其梯度模长平方的拉普拉斯：
$$
\frac{1}{2}\Delta(|\nabla u|^2) = |\operatorname{Hess} u|^2 + g(\nabla(\Delta u), \nabla u) + \operatorname{Ric}(\nabla u, \nabla u)
$$
我们将此恒等式应用于距离函数 $u=r$。在其光滑域内，$|\nabla r|^2=1$，因此左边 $\Delta(|\nabla r|^2) = \Delta(1) = 0$。于是恒等式简化为：
$$
0 = |\operatorname{Hess} r|^2 + g(\nabla(\Delta r), \nabla r) + \operatorname{Ric}(\nabla r, \nabla r)
$$
我们来分析每一项。令 $H(r) = \Delta r$ 为沿某条[极小测地线](@entry_id:636159) $\gamma(r)$ 的[平均曲率](@entry_id:162147)。那么 $g(\nabla(\Delta r), \nabla r)$ 正是 $H(r)$ 沿径向的导数 $H'(r)$。$\operatorname{Hess} r$ 是 $r$ 的Hessian矩阵，其迹为 $\Delta r = H(r)$。根据柯西-施瓦茨不等式，对于一个[对称矩阵](@entry_id:143130)，其[Frobenius范数](@entry_id:143384)的平方不小于其迹的平方除以矩阵的阶数。应用到在测地球面[切空间](@entry_id:199137)上作用的 $\operatorname{Hess} r$（阶数为 $n-1$），我们有 $|\operatorname{Hess} r|^2 \ge \frac{(\Delta r)^2}{n-1} = \frac{H(r)^2}{n-1}$。[@problem_id:3034472]

将这些代入简化的[Bochner恒等式](@entry_id:193184)，并使用[Ricci曲率](@entry_id:162038)下界假设 $\operatorname{Ric}(\nabla r, \nabla r) \ge (n-1)\kappa$，我们得到一个关于 $H(r)$ 的**Riccati[微分不等式](@entry_id:137452)**：
$$
H'(r) + \frac{H(r)^2}{n-1} + (n-1)\kappa \le 0
$$
另一方面，[模型平均](@entry_id:635177)曲率 $m_\kappa(r)$ 精确地满足相应的**[Riccati微分方程](@entry_id:200429)** [@problem_id:3031728]：
$$
m_\kappa'(r) + \frac{m_\kappa(r)^2}{n-1} + (n-1)\kappa = 0
$$
在 $r \to 0^+$ 时，$M$ 局部近似于[欧氏空间](@entry_id:138052)，因此 $H(r)$ 和 $m_\kappa(r)$ 都有相同的渐近行为，即 $H(r) \sim \frac{n-1}{r}$。根据[常微分方程](@entry_id:147024)的[比较原理](@entry_id:165563)，一个满足不等式的解将被满足等式的解所控制。因此，对于所有 $r > 0$（在[割迹](@entry_id:161337)之前），我们必然有 $H(r) \le m_\kappa(r)$，这正是[拉普拉斯比较定理](@entry_id:194055)的结论。

这个推导过程清楚地展示了曲率（通过Ricci项）如何通过一个一阶[非线性微分方程](@entry_id:175929)来约束[平均曲率](@entry_id:162147)（$\Delta r$）的增长。作为一个具体的例子，在[常曲率空间](@entry_id:161841) $M^n_{-\kappa^2}$（[双曲空间](@entry_id:268092)）中，我们有 $\operatorname{Ric} = -(n-1)\kappa^2 g$，上述推导中的所有不等式都变成等式，最终解出 $\Delta r = (n-1)\kappa \coth(\kappa r)$，这与模型函数 $m_{-\kappa^2}(r)$ 的表达式完全吻合。[@problem_id:3031708]

### 解释与推论

[拉普拉斯比较定理](@entry_id:194055)不仅是一个技术性的不等式，它还蕴含着丰富的几何直观和深刻的全局性推论。

#### [曲率与测地线](@entry_id:201184)的汇聚/发散

定理的直观含义是，正的Ricci曲率会加速[测地线](@entry_id:269969)的汇聚，而负的[Ricci曲率](@entry_id:162038)会加速[测地线](@entry_id:269969)的发散。我们可以通过比较不同曲率的模型函数 $m_\kappa(r)$ 来理解这一点。可以证明，对于固定的 $r>0$，函数 $m_\kappa(r)$ 是关于 $\kappa$ 的严格单调递减函数。[@problem_id:3031727]
这意味着，如果 $\kappa_1  \kappa_2$，则 $m_{\kappa_1}(r) > m_{\kappa_2}(r)$。换言之，**更高的曲率会导致更小的$\Delta r$**（即更小的测地球面平均曲率）。因为正曲率使原本平行的[测地线](@entry_id:269969)相互靠拢（汇聚），导致测地球面面积的增长比欧氏空间慢，从而其[对数导数](@entry_id:169238) $\Delta r$ 就更小。反之，负曲率使[测地线](@entry_id:269969)相互远离（发散），导致测地球面面积增长更快，$\Delta r$ 也更大。

例如，在非负[Ricci曲率](@entry_id:162038)（$\operatorname{Ric} \ge 0$）的情况下，即 $\kappa=0$ 的情形，我们有 $\Delta r \le \frac{n-1}{r}$。由于 $\Delta r = H(S_r(p))$，其导数为 $H'(r) = -|\operatorname{Hess} r|^2 - \operatorname{Ric}(\nabla r, \nabla r) \le 0$。这意味着在非负[Ricci曲率](@entry_id:162038)[流形](@entry_id:153038)上，测地 球面的[平均曲率](@entry_id:162147)沿径向是单调非增的。[@problem_id:3031709]

#### [刚性定理](@entry_id:198222)

[拉普拉斯比较定理](@entry_id:194055)是“尖锐的”（sharp），意味着不等式中的等号成立条件蕴含了强烈的几何结论。**Cheng[刚性定理](@entry_id:198222)**指出，如果在 $p$ 点的一个球邻域内（除去 $p$ 点）处处有 $\Delta r(x) = m_\kappa(r(x))$，那么这个球邻域就[等距同构](@entry_id:273188)于[常曲率空间](@entry_id:161841) $M_\kappa^n$ 中的相应半径的球。也就是说，如果一个[流形](@entry_id:153038)的测地球面[平均曲率](@entry_id:162147)和模型空间完全一样，那它局部就一定是[模型空间](@entry_id:635763)。[@problem_id:3031728]

#### [全局几何](@entry_id:197506)推论：[割迹](@entry_id:161337)与[直径界](@entry_id:276406)

[比较定理](@entry_id:637672)是连接局部曲率和全局拓扑的有力工具。一个关键应用是估计[割迹](@entry_id:161337)的距离和[流形的直径](@entry_id:634967)。以正Ricci曲率的情形为例，即 $\operatorname{Ric} \ge (n-1)\kappa > 0$。[比较定理](@entry_id:637672)给出 $\Delta r \le m_\kappa(r) = (n-1)\sqrt{\kappa}\cot(\sqrt{\kappa}r)$。
模型函数 $m_\kappa(r)$ 在 $r \to \pi/\sqrt{\kappa}$ 时会趋于 $-\infty$。由于 $\Delta r$ 被它从上方限定，这意味着[流形](@entry_id:153038)上的 $\Delta r$ 也必须在此之前就发散到 $-\infty$。我们知道 $\Delta r = \partial_r (\log J)$，它的发散意味着体积密度函数 $J(r,\theta)$ 在某个 $r_0 \le \pi/\sqrt{\kappa}$ 处必须变为零。$J$ 变为零的点正是 $p$ 的**[共轭点](@entry_id:160335)**（conjugate point），也叫[焦点](@entry_id:174388)。[共轭点](@entry_id:160335)必定位于[割迹](@entry_id:161337)上。
因此，对于任何从 $p$ 出发的[测地线](@entry_id:269969)，它在距离不超过 $\pi/\sqrt{\kappa}$ 时必定会遇到一个割点。这证明了[流形](@entry_id:153038)是紧的，并且其直径满足著名的**Bonnet-Myers直径上界**: $\operatorname{diam}(M) \le \pi/\sqrt{\kappa}$。[@problem_id:3031723]

#### [分布](@entry_id:182848)意义下的定理

经典[拉普拉斯算子](@entry_id:146319) $\Delta r$ 仅在 $M \setminus (\{p\} \cup \operatorname{Cut}(p))$ 上有定义。然而，[比较定理](@entry_id:637672)可以在[分布](@entry_id:182848)（测度）的意义下推广到包含[割迹](@entry_id:161337)在内的整个空间。[割迹](@entry_id:161337) $\operatorname{Cut}(p)$ 是一个[闭集](@entry_id:136446)，其 $n$ 维[Hausdorff测度](@entry_id:200740)为零。[@problem_id:3031740]
可以将 $\Delta r$ 视为一个[Radon测度](@entry_id:188027)，它可以分解为一个关于体[积测度](@entry_id:266846)绝对连续的[部分和](@entry_id:162077)一个奇异部分 $(\Delta r)_{\text{sing}}$。绝对连续部分的密度就是经典的 $\Delta r$，而奇异部分支撑在[割迹](@entry_id:161337)上。一个深刻的结论是，在[Ricci曲率](@entry_id:162038)有下界的条件下，这个[奇异测度](@entry_id:191565)是**非正**的。这可以直观理解为，在[割迹](@entry_id:161337)处[测地线汇](@entry_id:160274)聚，对应于一种“负的”散度。正是因为 $(\Delta r)_{\text{sing}} \le 0$，经典的比较不等式 $\Delta_{\text{class}} r \le m_\kappa(r)$ 才能够推广为测度不等式 $\Delta r \le m_\kappa(r) d\mu_g$。[@problem_id:3031740]

### 对[度量测度空间](@entry_id:180197)的推广

[拉普拉斯比较定理](@entry_id:194055)的强大之处在于其思想可以被推广到更一般的几何结构中。一个重要的例子是**光滑[度量测度空间](@entry_id:180197)** $(M, g, e^{-f}d\mu_g)$。在这种空间中，体[积测度](@entry_id:266846)被一个权重函数 $e^{-f}$ 修正了。

在这种设定下，我们定义**[加权拉普拉斯算子](@entry_id:634510)**（或Witten拉普拉斯算子） $\Delta_f$ 和**Bakry-Émery [Ricci张量](@entry_id:159336)** $\operatorname{Ric}_f$：
$$
\Delta_f u := \Delta u - g(\nabla f, \nabla u)
$$
$$
\operatorname{Ric}_f := \operatorname{Ric} + \operatorname{Hess} f
$$
$\Delta_f$ 是在加权体[积测度](@entry_id:266846)下的自伴算子。$\operatorname{Ric}_f$ 结合了通常的[Ricci曲率](@entry_id:162038)和权重函数 $f$ 的Hessian。
惊人的是，经典[比较定理](@entry_id:637672)的整个结构几乎原封不动地推广了过来。

**定理（Bakry-Émery[拉普拉斯比较定理](@entry_id:194055)）**：
若在一个完备光滑[度量测度空间](@entry_id:180197)中，Bakry-Émery [Ricci张量](@entry_id:159336)满足 $\operatorname{Ric}_f \ge (n-1)\kappa g$，那么对于距离函数 $r$，在其光滑域内有：
$$
\Delta_f r \le m_\kappa(r)
$$
同样，这个定理也存在相应的刚性版本：如果在 $p$ 的一个邻域内等号成立，那么该邻域不仅等距于[模型空间](@entry_id:635763) $M_\kappa^n$，而且权重函数 $f$ 必须为常数。[@problem_id:3031724]

这个推广意义重大，它表明[比较几何](@entry_id:180578)的核心思想并不局限于经典的黎曼几何，而是与一种更广义的“曲率-维数”条件相关联，这一思想在热流、[最优输运](@entry_id:196008)理论和[随机过程](@entry_id:159502)等领域都有着深刻的应用。