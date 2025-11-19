## 引言
[流形](@entry_id:153038)是现代数学与物理学的基石，它们将我们对曲线和[曲面](@entry_id:267450)的直观理解推广到任意维度。然而，从抽象的定义过渡到能够进行具体计算和应用的实例，是学习[微分几何](@entry_id:145818)的关键一步。本文旨在填补这一鸿沟，通过系统地介绍四类最重要的[流形](@entry_id:153038)范例——球面、环面、[射影空间](@entry_id:157963)和李群，来揭示微分几何的强大威力与深远影响。

在接下来的内容中，读者将踏上一段从原理到应用的探索之旅。第一章“原理与机制”将深入探讨如何通过嵌入、[商空间](@entry_id:274314)和[代数结构](@entry_id:137052)为这些[流形](@entry_id:153038)赋予几何生命，并演示曲率等核心概念的具体计算。第二章“应用与交叉学科联系”将展示这些基础[流形](@entry_id:153038)如何在理论物理、拓扑学和[代数几何](@entry_id:156300)等前沿领域中扮演关键角色。最后，通过“动手实践”部分，你将有机会亲自运用所学知识解决具体问题，从而真正内化这些重要的几何思想。

## 原理与机制

继引言章节之后，本章将深入探讨[微分几何](@entry_id:145818)中一些最基本且最重要的[流形](@entry_id:153038)实例：球面、环面、[射影空间](@entry_id:157963)和李群。我们的目标不仅是描述这些对象的拓扑形态，更重要的是揭示它们的几何结构。我们将系统地阐述定义这些[流形](@entry_id:153038)上[黎曼度量](@entry_id:754359)的核心原理，并演示如何运用这些原理来计算关键的[几何不变量](@entry_id:178611)，如曲率。通过这些具体的例子，我们将理解那些在更广泛的几何与物理理论中扮演核心角色的基本机制。

### 通过嵌入和坐标定义的[流形](@entry_id:153038)

在微分几何中，定义一个[流形](@entry_id:153038)及其几何结构最直观的方法之一，便是将其视为嵌入在高维[欧几里得空间](@entry_id:138052) $\mathbb{R}^N$ 中的一个[子集](@entry_id:261956)。高维空间的标准[欧几里得度量](@entry_id:147197)会自然地在子流形上“诱导”出一个[黎曼度量](@entry_id:754359)，这个诱导度量（induced metric）完全捕捉了[流形](@entry_id:153038)作为 $\mathbb{R}^N$ [子集](@entry_id:261956)的内在几何。

给定一个 $n$ 维[流形](@entry_id:153038) $M$ 的一个[参数化](@entry_id:272587)映射 $\mathbf{X}: U \to \mathbb{R}^N$，其中 $U \subseteq \mathbb{R}^n$ 是一个开集，[局部坐标](@entry_id:181200)为 $(u^1, \dots, u^n)$。$M$ 上的诱导度量张量 $g$ 的分量 $g_{ij}$ 可以通过切向量的[内积](@entry_id:158127)来计算。在点 $\mathbf{X}(u)$ 处的[切空间](@entry_id:199137)由向量 $\{\frac{\partial \mathbf{X}}{\partial u^1}, \dots, \frac{\partial \mathbf{X}}{\partial u^n}\}$ 张成。因此，度量分量由下式给出：

$g_{ij}(u) = \left\langle \frac{\partial \mathbf{X}}{\partial u^i}, \frac{\partial \mathbf{X}}{\partial u^j} \right\rangle_{\mathbb{R}^N} = \sum_{k=1}^{N} \frac{\partial X^k}{\partial u^i} \frac{\partial X^k}{\partial u^j}$

其中 $X^k$ 是 $\mathbf{X}$ 在 $\mathbb{R}^N$ 中的第 $k$ 个分量函数。一旦我们获得了度量张量 $g_{ij}$，所有其他的几何量，如联络（Christoffel 符号）和曲率，原则上都可以从中导出。

#### 示例：嵌入的环面

让我们以一个嵌入在 $\mathbb{R}^3$ 中的二维环面为例来阐明这个过程。考虑一个由参数 $(\theta, \phi) \in [0, 2\pi) \times [0, 2\pi)$ 定义的[曲面](@entry_id:267450)，其参数化方程为 [@problem_id:950737]：
$$
\mathbf{X}(\theta, \phi) = (a\cos\theta, b\sin\theta + r\cos\phi, r\sin\phi)
$$
这里 $a, b, r$ 是正常数。这个[曲面](@entry_id:267450)可以被看作是一个半径为 $r$ 的圆，其圆心沿着一个在 $xy$ 平面内[半长轴](@entry_id:164167)和半短轴分别为 $a$ 和 $b$ 的椭圆运动。

为了计算诱导度量，我们首先计算切向量 $\mathbf{X}_\theta = \frac{\partial \mathbf{X}}{\partial \theta}$ 和 $\mathbf{X}_\phi = \frac{\partial \mathbf{X}}{\partial \phi}$：
$$
\mathbf{X}_\theta = (-a\sin\theta, b\cos\theta, 0)
$$
$$
\mathbf{X}_\phi = (0, -r\sin\phi, r\cos\phi)
$$
然后，我们计算这些切向量的[内积](@entry_id:158127)来得到度量分量 $g_{\theta\theta}, g_{\theta\phi}, g_{\phi\phi}$：
$$
g_{\theta\theta} = \mathbf{X}_\theta \cdot \mathbf{X}_\theta = (-a\sin\theta)^2 + (b\cos\theta)^2 = a^2\sin^2\theta + b^2\cos^2\theta
$$
$$
g_{\theta\phi} = \mathbf{X}_\theta \cdot \mathbf{X}_\phi = -br\cos\theta\sin\phi
$$
$$
g_{\phi\phi} = \mathbf{X}_\phi \cdot \mathbf{X}_\phi = (-r\sin\phi)^2 + (r\cos\phi)^2 = r^2
$$
这就给出了环面在 $(\theta, \phi)$ [坐标系](@entry_id:156346)下的度量张量。从这些分量出发，我们可以进一步计算 Christoffel 符号，例如 $\Gamma^\theta_{\phi\phi}$，它描述了沿 $\phi$ 方向移动时切向量 $\mathbf{X}_\phi$ 的变化在 $\mathbf{X}_\theta$ 方向上的分量，这反映了[流形](@entry_id:153038)的弯曲。通过标准公式 $\Gamma^i_{jk} = \frac{1}{2} g^{i\ell}(\partial_j g_{\ell k} + \partial_k g_{\ell j} - \partial_\ell g_{jk})$，可以推导出 $\Gamma^\theta_{\phi\phi} = -\frac{b r \cos\theta\cos\phi}{a^2\sin^2\theta+b^2\cos^2\theta\cos^2\phi}$ [@problem_id:950737]。这个非零的结果明确地表明，即使环面是由直线段的[笛卡尔积](@entry_id:154642)在拓扑上构成的，其作为 $\mathbb{R}^3$ 中弯曲[子集](@entry_id:261956)的几何形状也具有内在的曲率。

#### 示例：球面与球极投影

球面 $S^n$ 是另一个可以通过嵌入 $\mathbb{R}^{n+1}$ 中定义的典型例子。半径为 $R$ 的 $n$ 维球面由方程 $\sum_{A=1}^{n+1} (X^A)^2 = R^2$ 定义。虽然我们也可以直接在球坐标下计算其诱导度量，但一种更强大且富有启发性的方法是使用**球极投影**（stereographic projection）。

球极投影将球面（除去一点，如北极 $N=(0, \dots, 0, R)$）映射到赤道[超平面](@entry_id:268044)（通常等同于 $\mathbb{R}^n$）。这个映射是一个**共形映射**（conformal map），这意味着它保持角度不变。在度量层面，这意味着球面的度量 $g_{S^n}$ 在投影坐标 $(x_1, \dots, x_n)$ 下，与 $\mathbb{R}^n$ 的标准[欧几里得度量](@entry_id:147197) $g_{\mathbb{E}} = \sum dx_i^2$ 仅相差一个标量因子。这个因子被称为**[共形因子](@entry_id:267682)**（conformal factor），通常记作 $\Omega(x)$。关系式可以写为：
$$
g_{S^n} = \Omega(x)^2 g_{\mathbb{E}}
$$
通过显式地写出球极投影的逆映射，即从平面上的点 $(x_1, \dots, x_n)$ 找到球面上对应的点 $(X^1, \dots, X^{n+1})$，并计算诱导度量，我们可以推导出这个[共形因子](@entry_id:267682) [@problem_id:950577]。对于从北极投影到赤道平面的二维球面 $S^2$，其逆映射为：
$$
(X, Y, Z) = \left( \frac{2R^2 x}{R^2+x^2+y^2}, \frac{2R^2 y}{R^2+x^2+y^2}, R\frac{x^2+y^2-R^2}{R^2+x^2+y^2} \right)
$$
经过一番计算，球面上由 $\mathbb{R}^3$ 诱导的线元 $ds^2 = dX^2+dY^2+dZ^2$ 可以表示为平面坐标 $(x,y)$ 的形式：
$$
ds^2 = \left( \frac{2R^2}{R^2+x^2+y^2} \right)^2 (dx^2+dy^2)
$$
这精确地揭示了共形结构。对于一般的 $n$ 维球面 $S^n$，[共形因子](@entry_id:267682)为 [@problem_id:950692] [@problem_id:950577]：
$$
\Omega(x) = \frac{2R^2}{R^2 + |x|^2}
$$
其中 $|x|^2 = \sum_{i=1}^n x_i^2$。这一结果表明 $n$ 维球面是**[共形平坦](@entry_id:260902)**的（conformally flat），即它的度量可以通过一个标量函数与平坦空间（欧几里得空间）的度量联系起来。这个性质是研究[球面几何](@entry_id:268217)的基石。

### [共形几何](@entry_id:186351)与曲率

[共形平坦](@entry_id:260902)性为计算曲率等[几何不变量](@entry_id:178611)提供了一条捷径。给定一个度量 $g = e^{2\omega} \bar{g}$（这里我们令 $\Omega = e^\omega$），其[标量曲率](@entry_id:157547) $S_g$ 与背景度量 $\bar{g}$ 的[标量曲率](@entry_id:157547) $S_{\bar{g}}$ 之间存在一个精确的变换关系。对于 $n>2$ 的维度，该关系为：
$$
S_g = e^{-2\omega} \left( S_{\bar{g}} - 2(n-1)\bar{\Delta}\omega - (n-1)(n-2)|\bar{\nabla}\omega|^2_{\bar{g}} \right)
$$
其中 $\bar{\Delta}$ 和 $\bar{\nabla}$ 是与背景度量 $\bar{g}$ 相关联的 Laplace 算子和[梯度算子](@entry_id:275922)。

#### 应用：n-球面的标量曲率

我们可以利用这个强大的公式来计算 $n$ 维球面 $S^n(R)$ 的标量曲率 [@problem_id:950692]。我们已知球面的度量是[共形平坦](@entry_id:260902)的，即 $g_{S^n} = \Omega^2 g_{\mathbb{E}}$。因此，我们可以取背景度量为平坦的[欧几里得度量](@entry_id:147197) $\bar{g} = g_{\mathbb{E}}$，其标量曲率 $S_{\bar{g}} = 0$。[共形因子](@entry_id:267682)函数为 $\Omega(x) = \frac{2R^2}{R^2+|x|^2}$，因此 $\omega = \ln \Omega(x) = \ln(2R^2) - \ln(R^2+|x|^2)$。

接下来，我们在平坦的 $\mathbb{R}^n$ 中计算 $\omega$ 的梯度和拉普拉斯：
$$
\bar{\nabla}\omega = -\frac{2x}{R^2+|x|^2} \quad \implies \quad |\bar{\nabla}\omega|^2_{\bar{g}} = \frac{4|x|^2}{(R^2+|x|^2)^2}
$$
$$
\bar{\Delta}\omega = \bar{\nabla} \cdot \bar{\nabla}\omega = -\frac{2n}{R^2+|x|^2} + \frac{4|x|^2}{(R^2+|x|^2)^2}
$$
将这些结果代入标量曲率的变换公式，并注意到 $e^{-2\omega} = \Omega^{-2} = (\frac{R^2+|x|^2}{2R^2})^2$，经过一番代数化简，所有对 $x$ 的依赖项都会奇迹般地消去，最终得到一个常数：
$$
S_g = \frac{n(n-1)}{R^2}
$$
这是一个非常深刻的结果。它表明 $n$ 维球面是一个**[常曲率空间](@entry_id:161841)**，其标量曲率仅由其维度 $n$ 和半径 $R$ 决定。这证实了球面的几何是均匀和各向同性的。

#### 度量与体积形式

一个黎曼度量不仅定义了长度和角度，还定义了体积。在[局部坐标](@entry_id:181200) $(x^1, \dots, x^n)$ 中，与度量 $g$ 相关联的[体积形式](@entry_id:203000)（volume form）$\omega_g$ 由下式给出：
$$
\omega_g = \sqrt{\det(g)} \, dx^1 \wedge \dots \wedge dx^n
$$
其中 $\det(g)$ 是度量张量 $g_{ij}$ 的[行列式](@entry_id:142978)。
[共形变换](@entry_id:159863)对[体积形式](@entry_id:203000)有直接影响。例如，考虑一个由标[准球](@entry_id:169696)面度量 $g_0$ 经过共形缩放得到的新度量 $g = f \cdot g_0$，其中 $f$ 是一个光滑函数 [@problem_id:950632]。在二维情况下，若 $g_0$ 在[局部坐标](@entry_id:181200) $(x,y)$ 中表示为 $g_0 = \sigma^2 (dx^2+dy^2)$，则其面积形式为 $\sigma^2 dx \wedge dy$。新度量 $g$ 在这些坐标中是一个对角矩阵乘以 $f$，其[行列式](@entry_id:142978)为 $\det(g) = (f\sigma^2)^2$。因此，新的面积形式 $\omega_g$ 为：
$$
\omega_g = \sqrt{(f\sigma^2)^2} \, dx \wedge dy = f \sigma^2 \, dx \wedge dy
$$
这表明面积元的密度函数直接乘以了[共形因子](@entry_id:267682) $f$。通过将 $f$ 和 $\sigma$ 用球极投影坐标表示，我们可以得到在平面坐标下显式的面积形式表达式。这个过程展示了度量、共形变换和积分测度之间的紧密联系。

### [商流形](@entry_id:190622)：[射影空间](@entry_id:157963)

除了嵌入，**商构造**（quotient construction）是构建新[流形](@entry_id:153038)的又一种基本方法。[实射影空间](@entry_id:149094) $\mathbb{R}P^n$ 就是这种构造的典型例子。

$\mathbb{R}P^n$ 的定义是 $\mathbb{R}^{n+1}$ 中所有穿过原点的直线的集合。这等价于将单位球面 $S^n$ 上的一对对径点（antipodal points）$\mathbf{x}$ 和 $-\mathbf{x}$ 视为同一个点，即通过[等价关系](@entry_id:138275) $\mathbf{x} \sim -\mathbf{x}$ 对 $S^n$ 进行商运算：$\mathbb{R}P^n = S^n / \{\pm 1\}$。

从 $S^n$到 $\mathbb{R}P^n$ 的[商映射](@entry_id:140877) $\pi: S^n \to \mathbb{R}P^n$ 是一个**[覆盖映射](@entry_id:169347)**（covering map）。我们可以赋予 $\mathbb{R}P^n$ 一个黎曼度量，使得这个映射成为一个**[局部等距](@entry_id:158618)同构**（local isometry）。这意味着 $\mathbb{R}P^n$ 在局部上继承了 $S^n$ 的所有几何性质。因此，如果 $S^n$ 具有半径 $R$ 的标[准圆](@entry_id:175119)形度量，那么 $\mathbb{R}P^n$ 也成为一个[常截面曲率](@entry_id:272200)为 $K=1/R^2$ 的[黎曼流形](@entry_id:261160)。

#### $\mathbb{R}P^n$ 的[局部坐标](@entry_id:181200)与度量计算

要在 $\mathbb{R}P^n$ 上进行具体计算，我们需要引入[局部坐标](@entry_id:181200)。一个常用的[坐标系](@entry_id:156346)是**仿射[坐标图](@entry_id:156506)**（affine chart）。例如，在 $\mathbb{R}P^2$ 中，点可以用[齐次坐标](@entry_id:154569) $[x_0:x_1:x_2]$ 表示。一个[坐标图](@entry_id:156506) $U_0$ 可以由所有 $x_0 \neq 0$ 的点组成。在 $U_0$ 上，我们可以定义[局部坐标](@entry_id:181200) $(u,v)$ 为 $u=x_1/x_0, v=x_2/x_0$。

为了在这些坐标下使用度量，我们需要将 $(u,v)$ 处的[切向量](@entry_id:265494)与 $S^2$ 上的[切向量](@entry_id:265494)联系起来。一个从 $U_0$ 到 $S^2$ 上半球的映射可以定义为 $\phi(u,v) = \frac{(1,u,v)}{\sqrt{1+u^2+v^2}}$。$\mathbb{R}P^2$ 上的诱导度量就是 $S^2$ 的标准度量通过这个映射的[拉回](@entry_id:160816)。我们可以利用这个框架来计算 $\mathbb{R}P^2$ 上向量场的长度 [@problem_id:950711]。例如，对于向量场 $X = u \frac{\partial}{\partial u} + v \frac{\partial}{\partial v}$，其范数的平方 $\|X\|^2=g(X,X)$ 可以通过计算其在 $S^2$ 中对应[向量的范数](@entry_id:154882)来得到。经过计算，我们发现：
$$
\|X\|^2 = \frac{u^2+v^2}{(1+u^2+v^2)^2}
$$
这个例子展示了如何将商空间的抽象定义转化为在[局部坐标](@entry_id:181200)中的具体几何计算。

#### $\mathbb{R}P^n$ 的曲率

由于 $\mathbb{R}P^n$ 是 $S^n$ 的[局部等距](@entry_id:158618)覆盖，它继承了 $S^n$ 的[常截面曲率](@entry_id:272200) $K=1/R^2$。对于一个 $n$ 维[常截面曲率](@entry_id:272200)空间，其 Ricci [曲率张量](@entry_id:181383) $Ric$ 和度量张量 $g$ 之间有简单的关系：
$$
Ric(X,Y) = (n-1) K g(X,Y)
$$
对于任意[单位切向量](@entry_id:262985) $V \in T_p(\mathbb{R}P^n)$（即 $g(V,V)=1$），其 Ricci 曲率的值为 [@problem_id:950700]：
$$
Ric(V,V) = (n-1) K g(V,V) = (n-1) \frac{1}{R^2} \cdot 1 = \frac{n-1}{R^2}
$$
这个结果简洁地将 $\mathbb{R}P^n$ 的 Ricci 曲率与其维度以及其覆盖空间 $S^n$ 的半径联系起来，完美地体现了商构造在几何学中的力量。

### 对称性的几何：[李群](@entry_id:137659)与[李代数](@entry_id:137954)

[李群](@entry_id:137659)是既是群又是[光滑流形](@entry_id:160799)，且群运算（乘法和求逆）是[光滑映射](@entry_id:203730)的数学对象。它们是数学和物理中对称性的语言。例子包括三维空间中的旋转群 $SO(3)$、二维欧氏运动群 $SE(2)$ 和作为[量子力学自旋](@entry_id:157916)群的[特殊酉群](@entry_id:138145) $SU(2)$。

#### 李代数：在[单位元处的切空间](@entry_id:266468)

每个李群 $G$ 在其单位元 $e$ 处都有一个切空间 $T_eG$，它本身构成一个[向量空间](@entry_id:151108)。这个[向量空间](@entry_id:151108)配备了一个额外的结构——**[李括号](@entry_id:636461)**（Lie bracket），从而成为一个**[李代数](@entry_id:137954)**（Lie algebra），记为 $\mathfrak{g}$。对于[矩阵李群](@entry_id:145968)，李代数也是由矩阵组成的，李括号就是矩阵的**交换子**（commutator）：
$$
[A, B] = AB - BA
$$
[李代数](@entry_id:137954)是[李群](@entry_id:137659)的“无穷小”版本，它捕捉了群在单位元附近的结构。例如，二维[刚体运动](@entry_id:193355)群 $SE(2)$ 的李代数 $\mathfrak{se}(2)$ 是一个三维[向量空间](@entry_id:151108)。给定一组基底矩阵，我们可以计算它们的李括号来揭示代数的结构。例如，对于 $\mathfrak{se}(2)$ 的一组基 $\{X_1, X_2, X_3\}$，计算 $[X_1, X_3]$ 会得到[基向量](@entry_id:199546)的一个线性组合 [@problem_id:950765]。这种计算会引出**[结构常数](@entry_id:157960)**（structure constants）$c^k_{ij}$，它们定义了李代数的乘法表：$[X_i, X_j] = \sum_k c^k_{ij} X_k$。

#### [指数映射](@entry_id:137184)：从代数到群

**[指数映射](@entry_id:137184)**（exponential map）$\exp: \mathfrak{g} \to G$ 是连接李代数和[李群](@entry_id:137659)的桥梁。对于[矩阵李群](@entry_id:145968)，它就是矩阵的[指数函数](@entry_id:161417)：$\exp(A) = \sum_{k=0}^\infty \frac{1}{k!} A^k$。
一个经典例子是[旋转群](@entry_id:204412) $SO(3)$ 及其李代数 $\mathfrak{so}(3)$（所有 $3 \times 3$ 实反对称矩阵的空间）。$\mathfrak{so}(3)$ 中的每个矩阵 $A$ 都可以与一个向量 $\vec{\omega} \in \mathbb{R}^3$ 相关联，使得 $A\vec{r} = \vec{\omega} \times \vec{r}$。[指数映射](@entry_id:137184) $\exp(A)$ 生成一个绕轴 $\vec{\omega}/|\vec{\omega}|$ 旋转角度为 $\theta = |\vec{\omega}|$ 的旋转矩阵 $R(\vec{\omega})$。这个映射有一个优美的[闭合形式](@entry_id:271343)，即**Rodrigues 公式**：
$$
R(\vec{\omega}) = \exp(A) = I + \frac{\sin\theta}{\theta} A + \frac{1-\cos\theta}{\theta^2} A^2
$$
利用这个公式，我们可以推导出一个联系[矩阵表示](@entry_id:146025)和几何意义的重要关系。通过计算旋转矩阵的迹（trace），我们发现 [@problem_id:950682]：
$$
\text{tr}(R(\vec{\omega})) = 1 + 2\cos\theta
$$
这个公式表明，我们可以直接从[旋转矩阵](@entry_id:140302)的迹中恢复出旋转的角度，这是几何与代数之间深刻联系的一个体现。

#### 伴随表示与[双不变度量](@entry_id:184842)

[李群](@entry_id:137659)可以通过**伴随表示**（adjoint representation）作用于其自身的[李代数](@entry_id:137954)。这个作用由共轭定义：$\text{Ad}_g(X) = gXg^{-1}$，其中 $g \in G, X \in \mathfrak{g}$。对于每个 $g$，$\text{Ad}_g$ 是 $\mathfrak{g}$ 上的一个[线性变换](@entry_id:149133)。我们可以计算这个变换在[李代数](@entry_id:137954)基底下的[矩阵表示](@entry_id:146025) [@problem_id:950763]。例如，对于 $SU(2)$，其伴随表示揭示了它与 $SO(3)$ 之间的著名 $2:1$ 同态关系。

李群的几何结构可以通过引入一个**黎曼度量**来丰富。特别重要的一类度量是**[双不变度量](@entry_id:184842)**（bi-invariant metric），它在左乘和右乘下都保持不变。这样一个度量完全由其在单位元处的值，即[李代数](@entry_id:137954) $\mathfrak{g}$ 上的一个[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle_e$ 所决定。这个[内积](@entry_id:158127)必须是 $\text{Ad}$-不变的，即 $\langle \text{Ad}_g(X), \text{Ad}_g(Y) \rangle_e = \langle X, Y \rangle_e$ 对所有 $g \in G$ 成立。

对于装备了[双不变度量](@entry_id:184842)的[李群](@entry_id:137659)，其几何曲率与李代数的[代数结构](@entry_id:137052)之间存在一个惊人的简单关系。由一对标准正交的[左不变向量场](@entry_id:637116) $X, Y$ 张成的平面[截面曲率](@entry_id:159738) $K$ 由下式给出：
$$
K(X, Y) = \frac{1}{4} \langle [X,Y], [X,Y] \rangle_e
$$
这意味着[流形](@entry_id:153038)的几何曲率可以直接从李括号的范数中计算出来。

让我们以 $SU(2)$ 为例 [@problem_id:950785]。它的李代数 $\mathfrak{su}(2)$ 由无迹斜[厄米矩阵](@entry_id:155147)构成。我们可以选择一个由[泡利矩阵](@entry_id:139493)生成的[标准正交基](@entry_id:147779) $\{X_1, X_2, X_3\}$。利用[泡利矩阵](@entry_id:139493)的对易关系，我们可以计算出[基向量](@entry_id:199546)的[李括号](@entry_id:636461)，例如 $[X_1, X_2] = c X_3$，其中常数 $c$ 取决于基的归一化。将此代入[截面曲率公式](@entry_id:204815)，我们发现 $SU(2)$ 在此[双不变度量](@entry_id:184842)下是一个[常曲率空间](@entry_id:161841)，其[截面曲率](@entry_id:159738) $K$ 是一个正的常数。例如，若基的选择使得 $\langle [X_1,X_2], [X_1,X_2] \rangle_e = 4/S^2$，则[截面曲率](@entry_id:159738)为 $K=1/S^2$。这表明 $SU(2)$ 的几何类似于一个[三维球面](@entry_id:261323)，再次印证了[代数结构](@entry_id:137052)如何决定其作为[流形](@entry_id:153038)的几何形态。

通过这些范例，我们看到了定义和分析[流形](@entry_id:153038)几何的多种原理和机制：从具体的嵌入参数化，到更抽象的共形变换和[商空间](@entry_id:274314)构造，再到李群中代数与几何的深刻融合。这些基本例子不仅是理论的试验场，更是通向现代微分几何与理论物理宏伟殿堂的基石。