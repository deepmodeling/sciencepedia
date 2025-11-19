## 引言
在几何学与物理学中，寻求“最优”形状是一个永恒的主题。从悬挂的链条到漂浮的肥皂泡，自然界似乎总在遵循某种形式的能量最小化或面积[最小化原理](@entry_id:169952)。极小[流形理论](@entry_id:263722)正是对这一古老[变分问题](@entry_id:756445)的数学精确化：在所有具有相同边界的[曲面](@entry_id:267450)中，哪一个的面积最小？尽管这个问题的[全局解](@entry_id:180992)（Plateau问题）极为复杂，但对其局部性质的研究引出了“极小[流形](@entry_id:153038)”这一核心概念——即[面积泛函](@entry_id:635965)的[临界点](@entry_id:144653)。本文旨在为读者提供一个关于极小[流形](@entry_id:153038)及其控制方程的全面而深入的介绍，揭示其背后深刻的数学结构与广泛的应用价值。

本文的探索将分为三个章节。首先，在“原理与机制”一章中，我们将从变分定义出发，推导[极小曲面方程](@entry_id:187309)，并通过悬链面、[螺旋面](@entry_id:264087)等经典实例加深理解，同时介绍[Weierstrass-Enneper表示](@entry_id:264077)等强大的构造工具，最后深入探讨[Bernstein问题](@entry_id:636802)和min-max理论等现代几何分析的前沿成果。接着，在“应用与交叉学科联系”一章中，我们将展示极小[流形理论](@entry_id:263722)如何作为一种工具，在拓扑学、[复几何](@entry_id:159080)乃至理论化学等不同领域中解决关键问题，揭示其强大的学科交叉能力。最后，通过“动手实践”部分的系列练习，读者将有机会亲手应用这些理论，从验证经典[曲面](@entry_id:267450)到构造新[曲面](@entry_id:267450)，从而将抽象的数学原理内化为扎实的分析与计算技能。

## 原理与机制

本章旨在深入探讨[极小曲面](@entry_id:157732)的基本原理与核心机制。继引言章节之后，我们将直接从[极小曲面](@entry_id:157732)的变分定义出发，逐步推导其在不同坐标表示下的具体形式，即[极小曲面方程](@entry_id:187309)。随后，我们将通过分析一系列经典的极小曲面实例，展示这些原理的实际应用。在此基础上，我们将介绍构造和分析[极小曲面](@entry_id:157732)的高级工具，包括[Weierstrass-Enneper表示](@entry_id:264077)、共轭[曲面](@entry_id:267450)与守恒律。最后，本章将引入几何分析中的深刻思想，探讨[极小曲面](@entry_id:157732)的体积增长、稳定性、以及存在性理论，包括著名的[Bernstein问题](@entry_id:636802)、[Jacobi算子](@entry_id:195512)，以及现代的min-max理论。

### 变分基础：平均曲率与极小性

在几何学中，极小曲面的概念源于一个经典的[变分问题](@entry_id:756445)：在所有具有相同边界的[曲面](@entry_id:267450)中，哪一个的面积最小？尽管这个问题的答案（即Plateau问题）相当复杂，但其局部版本为我们提供了[极小曲面](@entry_id:157732)的现代定义。一个光滑浸入的$k$维子流形$(\Sigma^k, g_\Sigma)$被定义为**极小的 (minimal)**，如果它在所有具有[紧支集](@entry_id:276214)的法向变动下一阶变分[临界点](@entry_id:144653)。

更精确地，考虑一个[浸入](@entry_id:161534)$\iota: \Sigma^k \to (M^n, g)$。该[浸入](@entry_id:161534)在$\Sigma$上诱导了一个度量$g_\Sigma = \iota^*g$。对于$\Sigma$上的任意[切向量](@entry_id:265494)场$X, Y$，我们可以将背景[流形](@entry_id:153038)$M$上的Levi-Civita联络$\nabla^M_X Y$分解为切向部分$\nabla^\Sigma_X Y$和法向部分$A(X,Y)$。这个法向部分定义了**第二基本形式 (second fundamental form)**，它是一个对称的、取值于[法丛](@entry_id:272447)$N\Sigma$的二阶张量：
$$
\nabla^M_X Y = \nabla^\Sigma_X Y + A(X,Y)
$$
第二基本形式衡量了[子流形](@entry_id:159439)$\Sigma$在背景[流形](@entry_id:153038)$M$中的弯曲程度。它的迹，即**[平均曲率向量](@entry_id:199617) (mean curvature vector)** $H$，是通过在任意局部$g_\Sigma$-标准正交切标架$\{e_i\}_{i=1}^k$下求和得到的：
$$
H = \mathrm{tr}_{g_\Sigma} A = \sum_{i=1}^k A(e_i, e_i)
$$
[平均曲率向量](@entry_id:199617)$H$是一个沿$\Sigma$定义的[法向量场](@entry_id:268853)，它指向面积局部增长最快的方向。

体积泛函的一阶变分公式精确地将体积的变化与[平均曲率](@entry_id:162147)联系起来。对于一个由法向变分场$V^\perp$生成的单参数变分$\Sigma_t$，其体积泛函在$t=0$处的[一阶导数](@entry_id:749425)为：
$$
\left.\frac{d}{dt}\right|_{t=0} \mathrm{Vol}(\Sigma_t) = -\int_{\Sigma} \langle H, V^\perp \rangle \, d\mu_\Sigma
$$
其中$d\mu_\Sigma$是$\Sigma$上的[体积元](@entry_id:267802)。从这个公式可以看出，[子流形](@entry_id:159439)$\Sigma$是体积泛函的[临界点](@entry_id:144653)（即在所有[紧支集](@entry_id:276214)变分下，体积的一阶变分为零）的充要条件是其[平均曲率向量](@entry_id:199617)恒为零。这便是[极小曲面](@entry_id:157732)的核心定义 [@problem_id:3032209]。

**定义：** 一个[浸入子流形](@entry_id:264923)$\Sigma \subset M$是**极小的**，当且仅当它的[平均曲率向量](@entry_id:199617)$H$恒等于零。

值得注意的是，“极小”这个术语可能引起误解。一个$H=0$的[曲面](@entry_id:267450)仅仅是[面积泛函](@entry_id:635965)的一个[临界点](@entry_id:144653)，它可能是一个局部极小值点（[稳定极小曲面](@entry_id:636062)）、一个[鞍点](@entry_id:142576)（[不稳定极小曲面](@entry_id:636974)），甚至是一个[局部极大值](@entry_id:137813)点。

### 图形的[极小曲面方程](@entry_id:187309)

当一个[超曲面](@entry_id:159491)（$k=n-1$）可以表示为一个函数图像时，其平均曲率为零的条件可以简化为一个[非线性偏微分方程](@entry_id:169481)。考虑[欧几里得空间](@entry_id:138052)$\mathbb{R}^{k+1}$中的一个图形$\Sigma = \{ (x, u(x)) \in \mathbb{R}^{k+1} \mid x \in \mathbb{R}^k \}$，其中$u: \mathbb{R}^k \to \mathbb{R}$是一个[光滑函数](@entry_id:267124)。其[面积泛函](@entry_id:635965)为：
$$
\mathcal{A}[u] = \int \sqrt{1 + |\nabla u|^2} \, dx
$$
这个泛函的Euler-Lagrange方程给出了图形是[极小曲面](@entry_id:157732)的条件。该方程被称为**[极小曲面方程](@entry_id:187309) (minimal surface equation)**：
$$
\operatorname{div}\left(\frac{\nabla u}{\sqrt{1 + |\nabla u|^2}}\right) = 0
$$
在二维情况$u=u(x,y)$下，该方程展开为：
$$
(1 + u_y^2)u_{xx} - 2u_x u_y u_{xy} + (1 + u_x^2)u_{yy} = 0
$$
这个方程是一个[拟线性](@entry_id:637689)（quasilinear）[椭圆偏微分方程](@entry_id:178258)。它的解描述了所有可以表示为$\mathbb{R}^2$上函数图像的极小曲面。

一个经典的非平面极小曲面例子是**Scherk[曲面](@entry_id:267450)**。在特定区域内，它可以由[隐式方程](@entry_id:177636)$\sin z = \sinh x \sinh y$定义。通过[隐式微分法](@entry_id:137929)计算$z(x,y)$的各阶偏导数，并将其代入二维[极小曲面方程](@entry_id:187309)，可以验证该方程的左侧恒为零，从而证明Scherk[曲面](@entry_id:267450)确实是一个[极小曲面](@entry_id:157732) [@problem_id:3032208]。

### $\mathbb{R}^3$中的经典实例

除了平面和函数图形，还存在许多由[参数化](@entry_id:272587)描述的著名[极小曲面](@entry_id:157732)。计算它们的平均曲率需要用到[曲面](@entry_id:267450)微分几何的基本工具。对于一个[参数化曲面](@entry_id:181980)$X(u,v)$，其[第一基本形式](@entry_id:274022)由系数$E = \langle X_u, X_u \rangle$, $F = \langle X_u, X_v \rangle$, $G = \langle X_v, X_v \rangle$定义，而[第二基本形式](@entry_id:161454)由$L = \langle X_{uu}, n \rangle$, $M = \langle X_{uv}, n \rangle$, $N = \langle X_{vv}, n \rangle$定义，其中$n$是[单位法向量](@entry_id:178851)。[平均曲率](@entry_id:162147)$H$（在这里指平均曲率数值，即$H = \frac{1}{2} \mathrm{tr}_g A$）由以下公式给出：
$$
H = \frac{EN - 2FM + GL}{2(EG - F^2)}
$$

#### 悬链面 (Catenoid)

[悬链面](@entry_id:271627)是唯一一个通过旋转曲线生成的[极小曲面](@entry_id:157732)。它由参数化给出：
$$
X(u,v) = (\cosh v \cos u, \cosh v \sin u, v)
$$
通过直接计算，可以得到其[第一和第二基本形式](@entry_id:192112)的系数为：$E = \cosh^2 v$, $F=0$, $G=\cosh^2 v$；以及$L=-1$, $M=0$, $N=1$。将这些系数代入平均曲率公式，得到：
$$
H(u,v) = \frac{(\cosh^2 v)(1) - 2(0)(0) + (\cosh^2 v)(-1)}{2((\cosh^2 v)(\cosh^2 v) - 0^2)} = 0
$$
这验证了悬链面是一个[极小曲面](@entry_id:157732) [@problem_id:3032203]。

#### [螺旋面](@entry_id:264087) (Helicoid)

[螺旋面](@entry_id:264087)由以下参数化描述：
$$
X(u,v) = (u \cos v, u \sin v, v)
$$
这是一个直纹[曲面](@entry_id:267450)，即它是由一条直线（$v$坐标固定的线）沿着一条螺旋线运动而形成的。与[悬链面](@entry_id:271627)类似，我们可以计算出其[第一和第二基本形式](@entry_id:192112)的系数：$E=1$, $F=0$, $G=u^2+1$；以及$L=0$, $M = -1/\sqrt{1+u^2}$, $N=0$。代入[平均曲率](@entry_id:162147)公式后，同样得到$H(u,v)=0$ [@problem_id:3032206]。

[螺旋面](@entry_id:264087)不仅是一个[极小曲面](@entry_id:157732)，它还是一个**正常嵌入 (properly embedded)** 的[曲面](@entry_id:267450)。这意味着[参数化](@entry_id:272587)映射$X: \mathbb{R}^2 \to \mathbb{R}^3$是一个[同胚](@entry_id:146933)到其像的映射，并且是**正常的 (proper)**，即$\mathbb{R}^3$中任意紧集的原像是$\mathbb{R}^2$中的紧集。这个性质意味着[曲面](@entry_id:267450)不会在有限区域内“无限[振荡](@entry_id:267781)”或“自我积累”，其两端以一种受控的方式延伸至无穷远 [@problem_id:3032206]。

有趣的是，[悬链面](@entry_id:271627)和[螺旋面](@entry_id:264087)在局部上是等距的，它们构成了一个单参数的[极小曲面](@entry_id:157732)族，可以通过一个称为Bonnet变换的过程相互转化。

### 构造机制：[Weierstrass-Enneper表示](@entry_id:264077)

虽然逐一验证[曲面](@entry_id:267450)是否极小是一种方法，但是否存在一种系统性的方式来构造它们呢？对于$\mathbb{R}^3$中的[极小曲面](@entry_id:157732)，答案是肯定的，这便是强大的**[Weierstrass-Enneper表示](@entry_id:264077)**。该理论指出，任何一个在单连通[黎曼曲面](@entry_id:178613)$M$上的保角极小[浸入](@entry_id:161534)$X: M \to \mathbb{R}^3$都可以由一对[复变函数](@entry_id:175282)数据——一个[亚纯函数](@entry_id:171058)$g$和一个全纯1-形式$dh$——来构造。

具体而言，定义一个复值向量1-形式$\Phi = (\phi_1, \phi_2, \phi_3)$：
$$
\phi_1 = \frac{1}{2}\left(\frac{1}{g} - g\right) dh, \quad \phi_2 = \frac{i}{2}\left(\frac{1}{g} + g\right) dh, \quad \phi_3 = dh
$$
则极小[浸入](@entry_id:161534)由下式给出，不计平移：
$$
X(p) = \operatorname{Re} \int^p \Phi
$$
这里，$g$可以被解释为[高斯映射](@entry_id:260784)的球极投影，$dh$则被称为高度[微分](@entry_id:158718)。

当定义域$M$不是单连通时（例如，一个环面或带洞的平面），积分的[路径依赖性](@entry_id:186326)会带来一个**周期问题 (period problem)**。为了使浸入$X$在$M$上是良定义的，$\Phi$在$M$的任何闭路$\gamma$上的积分（即周期）其实部必须为零：
$$
\operatorname{Re} \oint_\gamma \Phi = 0
$$
这个条件对Weierstrass数据$(g, dh)$施加了强有力的约束。

我们可以通过这个方法重新构造[悬链面](@entry_id:271627)。考虑在穿孔复平面$\mathbb{C}^* = \mathbb{C} \setminus \{0\}$上，设Weierstrass数据为$g(z) = \alpha z^m$ 和 $dh = \beta z^{-m} dz$。为了得到一个非平凡的[极小曲面](@entry_id:157732)（如悬链面，它有上下两个无限延伸的“端”），我们需要第三分量$\phi_3$有非零的纯虚周期，这要求$m=1$。周期闭合条件$\operatorname{Re} \oint \phi_3 = 0$则迫使$\beta$为实数。通过参数变换，可以将$\alpha$[标准化](@entry_id:637219)为1。最后，通过计算浸入并要求其“腰部”半径为1，可以确定$\beta=1$。因此，参数三元组$(m, \alpha, \beta) = (1, 1, 1)$通过Weierstrass表示精确地生成了标准悬链面 [@problem_id:3032216]。

### 守恒律与共轭[曲面](@entry_id:267450)

Weierstrass表示不仅是构造工具，它还揭示了深刻的内在结构。其中一个便是**共轭[曲面](@entry_id:267450) (conjugate surface)** 的概念。对于一个由$\Phi$生成的[极小曲面](@entry_id:157732)$X = \operatorname{Re} \int \Phi$，它的共轭[曲面](@entry_id:267450)$X^*$被定义为：
$$
X^*(p) = \operatorname{Im} \int^p \Phi
$$
由于$\Phi$是全纯的，其共轭$\Phi^*$也是全纯的，因此$X^*$也是一个[极小曲面](@entry_id:157732)。悬链面和[螺旋面](@entry_id:264087)就是一对经典的共轭[曲面](@entry_id:267450)。

这个结构与物理中的守恒律密切相关。定义一个极小曲面的**通量向量 (flux vector)** 为沿[闭合曲线](@entry_id:264519)$\gamma$的积分$F(\gamma) = \int_\gamma *dX$，其中$*dX$是$dX = \mathrm{Re}(\Phi)$的[Hodge对偶](@entry_id:263610)。由于在保角度量下$*dX = \mathrm{Im}(\Phi)$，我们得到一个优美的关系：
$$
F(\gamma) = \int_\gamma \mathrm{Im}(\Phi) = \mathrm{Im} \left( \int_\gamma \Phi \right)
$$
通量向量就是$\Phi$的周期的虚部，也是共轭[曲面](@entry_id:267450)$X^*$的周期。由于$\Phi$是全纯的，根据[Cauchy积分定理](@entry_id:194141)，这个积分值（从而通量）在环域内不依赖于曲线的选取，只要曲线是同伦的。这构成了一个几何上的守恒律。例如，对于Weierstrass数据$g(z)=z^k$和$dh = a \frac{dz}{z}$（其中$a$为实数），无论自然数$k$取何值，也无论积分路径（只要环绕原点），计算出的通量向量总是常数$\begin{pmatrix} 0 & 0 & 2\pi a \end{pmatrix}$ [@problem_id:3032204]。

### 极小曲面的分析理论

超越具体构造，几何分析提供了研究[极小曲面](@entry_id:157732)一般性质的强大工具，包括它们的增长行为、稳定性和存在性。

#### 体积增长与[Bernstein问题](@entry_id:636802)

[极小曲面](@entry_id:157732)的几何性质受到严格的限制。一个基本结果是关于极小图形的[体积增长](@entry_id:274676)。如果一个定义在整个$\mathbb{R}^k$上的极小图形$\Sigma$（由函数$u: \mathbb{R}^k \to \mathbb{R}$给出）具有一致的梯度界$|\nabla u| \le K$，那么其在半径为$r$的背景球内的[体积增长](@entry_id:274676)速度不会超过$r^k$。具体来说，其体积满足如下估计：
$$
\operatorname{Vol}_k(\Sigma \cap B_r^{k+1}(0)) \le \omega_k \sqrt{1+K^2} \, r^k
$$
其中$\omega_k$是$\mathbb{R}^k$中单位球的体积。这个估计可以通过直接对体积元$\sqrt{1+|\nabla u|^2}$在投影区域上积分得到 [@problem_id:3032207]。

这一性质与[微分几何](@entry_id:145818)中一个深刻的问题——**[Bernstein问题](@entry_id:636802)**——密切相关。该问题提问：一个在整个[欧氏空间](@entry_id:138052)$\mathbb{R}^n$上定义的极小图形是否必须是[超平面](@entry_id:268044)？答案出人意料地依赖于维数。
- **[Bernstein定理](@entry_id:181399) (1915-1968):** 对于$n \le 7$，答案是肯定的。任何完整的极小图形$\Sigma \subset \mathbb{R}^{n+1}$都必须是[超平面](@entry_id:268044)。
- **Bombieri-De Giorgi-Giusti (1969):** 对于$n \ge 8$，答案是否定的。存在非平面的完[整极小图](@entry_id:190967)形。

[Bernstein定理](@entry_id:181399)的失败与**极小锥 (minimal cones)** 的存在性紧密相关。在低维（$n \le 7$）中，任何稳定且在原点外光滑的极小锥都必须是超平面。然而，在$\mathbb{R}^8$中，存在一个著名的非平面、面积极小化且仅在原点奇异的**[Simons锥](@entry_id:180725)** $\mathcal{C}_S = \{(x',x'') \in \mathbb{R}^4 \times \mathbb{R}^4 : |x'|=|x''|\}$。Bombieri、De Giorgi和Giusti的杰出工作正是利用了这个[Simons锥](@entry_id:180725)作为“无穷远处的[切锥](@entry_id:191609)模型”，通过精细的分析技术（求解一系列Dirichlet问题并取极限），构造出了一个非平面的、在整个$\mathbb{R}^8$上定义的极小图形。这个构造精妙地展示了高维空间中几何结构的丰富性如何改变分析问题的答案 [@problem_id:3032210]。

#### 稳定性与[Jacobi算子](@entry_id:195512)

一个极小曲面作为[面积泛函](@entry_id:635965)的[临界点](@entry_id:144653)，其稳定性由面积的二阶变分决定。一个[极小曲面](@entry_id:157732)是**稳定的 (stable)**，如果所有法向变分都使其面积二阶增加。主导二阶变分的算子是**[Jacobi算子](@entry_id:195512) (Jacobi operator)**。对于法向变分$\varphi\nu$，[平均曲率](@entry_id:162147)的一阶变分（即线性化）由[Jacobi算子](@entry_id:195512)$L$作用在$\varphi$上给出：
$$
\left.\frac{d H}{d t}\right|_{t=0} = L\varphi = \Delta_\Sigma \varphi + (|A|^2 + \operatorname{Ric}(\nu,\nu))\varphi
$$
其中$\Delta_\Sigma$是[曲面](@entry_id:267450)上的[Laplace-Beltrami算子](@entry_id:267002)，$|A|^2$是[第二基本形式](@entry_id:161454)范数的平方，$\operatorname{Ric}(\nu,\nu)$是背景[流形](@entry_id:153038)沿法向$\nu$的Ricci曲率。

[Jacobi算子](@entry_id:195512)在两个方面至关重要：
1.  **稳定性：** [Jacobi算子](@entry_id:195512)$L$的谱（[特征值](@entry_id:154894)）决定了[曲面](@entry_id:267450)的稳定性。$L$的负[特征值](@entry_id:154894)的数量被称为该[极小曲面](@entry_id:157732)的**[Morse指数](@entry_id:159485) (Morse index)**。指数大于零意味着[曲面](@entry_id:267450)是不稳定的。
2.  **形变：** [Jacobi算子](@entry_id:195512)的核（kernel），即满足$L\varphi=0$的函数$\varphi$构成的空间，描述了保持[曲面](@entry_id:267450)极小性的所有无穷小法向形变。这个空间的维数被称为[曲面](@entry_id:267450)的**零度 (nullity)** [@problem_id:3032217]。

以$S^3$中的**[Clifford环面](@entry_id:180700)** $\mathbb{T}_{\mathrm{Cl}}$为例，这是一个经典的紧致[极小曲面](@entry_id:157732)。对于单位球面$S^3$，$\operatorname{Ric}(\nu,\nu)=2$。通过计算，我们发现Clifford环的第二基本形式范数平方为$|A|^2=2$。因此，其[Jacobi算子](@entry_id:195512)为$L = \Delta_{\mathbb{T}_{\mathrm{Cl}}} + 4$。求解$L\varphi=0$等价于求解[特征值问题](@entry_id:142153)$\Delta_{\mathbb{T}_{\mathrm{Cl}}}\varphi = -4\varphi$。Clifford环的诱导度量是平坦的，其Laplacian的[特征值](@entry_id:154894)为$-2(m^2+n^2)$（对于适当的归一化）。满足$-2(m^2+n^2)=-4$的整数对$(m,n)$有四对：$(1,1), (1,-1), (-1,1), (-1,-1)$。这对应于四个[线性无关](@entry_id:148207)的实值[特征函数](@entry_id:186820)，因此Clifford环的[零度](@entry_id:156285)为4 [@problem_id:3032217]。

#### 存在性理论：Min-Max方法

我们如何在一个一般的闭[流形](@entry_id:153038)中证明[极小曲面](@entry_id:157732)的存在性？Plateau问题在[流形](@entry_id:153038)中的推广是困难的，因为解可能不存在或不唯一。现代[几何分析](@entry_id:157700)通过**min-max理论**，特别是**Almgren-Pitts理论**，为这个问题提供了强大的框架。

该理论的思想是在一个无穷维的“[圈空间](@entry_id:265325)”（由[流形](@entry_id:153038)中的[曲面](@entry_id:267450)或更一般的链构成）上寻找[面积泛函](@entry_id:635965)的[鞍点](@entry_id:142576)。考虑一个“扫过 (sweepout)”[流形](@entry_id:153038)的[曲面](@entry_id:267450)族$\{\Sigma_t\}_{t \in [0,1]}$，它从一个点（零链）开始，扩张并最终收缩回一个点。这个族中面积最大的那个[曲面](@entry_id:267450)的面积给出了一个数值。Min-max理论旨在通过在所有与给定族[同伦](@entry_id:139266)的族中，寻找这个最大面积的[下确界](@entry_id:140118)，即所谓的**宽度 (width)** $W$。

Almgren-Pitts理论的核心成果是：这个宽度值$W$是由一个或多个[光滑嵌入](@entry_id:637480)的[极小超曲面](@entry_id:188002)实现的。在满足一定维数（$n \le 6$）和度量[一般性](@entry_id:161765)（“bumpy metric”，即没有非平凡Jacobi场的[极小曲面](@entry_id:157732)）的条件下，该理论保证：
- 对于一个$k$参数的扫过族，min-max过程会产生一个或一族光滑、嵌入、[重数](@entry_id:136466)为一的[极小超曲面](@entry_id:188002)$\Sigma$。
- 这些[曲面](@entry_id:267450)的总[Morse指数](@entry_id:159485)满足一个关键的不等式：$\operatorname{index}(\Sigma) \le k$ [@problem_id:3032202]。

对于最简单的单参数扫过（$k=1$），这意味着得到的极小曲面$\Sigma$的[Morse指数](@entry_id:159485)$\operatorname{index}(\Sigma) \le 1$。又因为它是通过一个“山路”过程找到的，它不可能是面积的局部极小值（稳定[曲面](@entry_id:267450)，指数为0），所以必须是 不稳定的，即$\operatorname{index}(\Sigma) \ge 1$。结合这两个条件，我们得出$\operatorname{index}(\Sigma)=1$。因此，Almgren-Pitts理论不仅证明了极小曲面的存在性，还精确地构造出了[Morse指数](@entry_id:159485)为1的[不稳定极小曲面](@entry_id:636974)，极大地丰富了我们[对流](@entry_id:141806)形上[极小曲面](@entry_id:157732)种群的理解 [@problem_id:3032202]。