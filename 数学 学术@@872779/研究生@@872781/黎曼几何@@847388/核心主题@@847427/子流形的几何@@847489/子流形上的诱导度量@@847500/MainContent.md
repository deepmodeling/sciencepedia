## 引言
在自然界和科学的各个领域中，我们研究的许多几何对象，例如行星的[轨道](@entry_id:137151)、DNA的双[螺旋结构](@entry_id:183721)或物理理论中的“膜”，都天然地存在于某个更高维度的空间之中。这些对象构成了所谓的“[子流形](@entry_id:159439)”。一个根本性的问题随之产生：我们如何精确地描述和量化这些嵌入对象的几何特性？它们自身的几何（[内蕴几何](@entry_id:158788)）与其在周围空间中的弯曲方式（外蕴几何）之间又存在怎样的深刻联系？

本文旨在系统地回答这些问题，其核心工具便是“诱导度量”的概念。诱导度量是子流形从其所处的[环境空间](@entry_id:184743)中“继承”而来的一种自然的几何结构，它构成了研究[子流形](@entry_id:159439)一切几何性质的基石。通过本文的学习，读者将掌握从基本原理到前沿应用的完整知识体系。

文章将分为三个主要部分展开。在第一章“原理与机制”中，我们将从诱导度量的严格定义出发，学习如何在[局部坐标](@entry_id:181200)下进行计算。随后，我们将引入第二基本形式、形算子等一系列强大的工具来刻画外蕴几何，并最终推导连接内蕴与外蕴几何的基石——[高斯方程](@entry_id:192573)和[科达齐方程](@entry_id:635135)。接下来，在“应用与跨学科联系”一章中，我们将展示诱导度量的概念如何超越纯数学的范畴，在广义相对论、弦理论、[李群论](@entry_id:204663)乃至[信息几何](@entry_id:141183)等多个前沿领域中扮演着至关重要的角色。最后，通过“动手实践”环节，读者将有机会通过解决具体的计算问题，来巩固和深化对核心概念的理解。

## 原理与机制

在上一章中，我们介绍了[黎曼流形](@entry_id:261160)作为[内蕴几何](@entry_id:158788)研究的核心对象。然而，许多在几何学和物理学中至关重要的[流形](@entry_id:153038)，自然地作为更高维空间中的[子集](@entry_id:261956)出现。例如，二维球面可以被看作是三维欧几里得空间中的一个[曲面](@entry_id:267450)。这种“嵌入”的观点引出了一个基本问题：子流形如何从其所在的[环境空间](@entry_id:184743)（称为“环境[流形](@entry_id:153038)”）中继承[黎曼度量](@entry_id:754359)？这种继承的度量（称为“诱导度量”）的几何性质又如何？

本章将系统地探讨这些问题。我们将从诱导度量的基本定义出发，学习如何通过[拉回运算](@entry_id:753859)来构造它。随后，我们将展示如何利用诱导度量来计算子流形上的长度、面积等[内蕴几何](@entry_id:158788)量。然而，子流形的完整几何故事并不仅仅是其内蕴几何。它在[环境空间](@entry_id:184743)中的弯曲方式，即其“外蕴几何”，同样至关重要。我们将建立一套分析外蕴几何的系统工具，包括[法丛](@entry_id:272447)、[第二基本形式](@entry_id:161454)和形算子。最后，我们将推导连接内蕴曲率与外蕴曲率的[高斯方程](@entry_id:192573)和[科达齐方程](@entry_id:635135)——它们是子流形[黎曼几何](@entry_id:160508)的基石。

### 诱导度量的定义与计算

#### 作为[拉回](@entry_id:160816)的度量

考虑一个[光滑映射](@entry_id:203730) $F: M \to N$，其中 $(N, g_N)$ 是一个[黎曼流形](@entry_id:261160)。如果对于 $M$ 中的每一点 $p$，[微分](@entry_id:158718)映射 $dF_p: T_pM \to T_{F(p)}N$ 都是单射的，那么我们称 $F$ 为一个**浸入 (immersion)**。这个条件保证了 $M$ 在局部上被“无[褶皱](@entry_id:199664)地”置于 $N$ 中。当 $F$ 是一个[单射](@entry_id:183792)[浸入](@entry_id:161534)时，我们称其为**嵌入 (embedding)**，此时 $M$ 可以被视为 $N$ 的一个**[子流形](@entry_id:159439)**。

一个浸入的[子流形](@entry_id:159439) $M$ 可以通过[拉回运算](@entry_id:753859)继承其环境[流形](@entry_id:153038) $(N, g_N)$ 的[黎曼度量](@entry_id:754359)。在 $M$ 上的**诱导度量 (induced metric)** $g_M$ 定义为 $g_M = F^*g_N$。根据[拉回](@entry_id:160816)的定义，对于 $M$ 上任意一点 $p$ 和任意[切向量](@entry_id:265494) $v, w \in T_pM$，我们有：

$$
(g_M)_p(v, w) = (F^*g_N)_p(v, w) := (g_N)_{F(p)}(dF_p(v), dF_p(w))
$$

这个定义直观地表示：要测量 $M$ 上两个[切向量](@entry_id:265494) $v$ 和 $w$ 的[内积](@entry_id:158127)，我们首先通过[微分](@entry_id:158718) $dF_p$ 将它们“推送”到环境空间 $N$ 的切空间 $T_{F(p)}N$ 中，得到向量 $dF_p(v)$ 和 $dF_p(w)$，然后用环境度量 $(g_N)_{F(p)}$ 来测量这两个新向量的[内积](@entry_id:158127)。

浸入的条件——$dF_p$ 的[单射性](@entry_id:147722)——至关重要。正是这个条件保证了 $g_M$ 是一个真正的[黎曼度量](@entry_id:754359)。具体来说，要使 $g_M$ 成为一个[黎曼度量](@entry_id:754359)，它必须在每一点都是正定的。这意味着对于任意非零切向量 $v \in T_pM$，必须有 $(g_M)_p(v, v) > 0$。根据定义，$(g_M)_p(v, v) = (g_N)_{F(p)}(dF_p(v), dF_p(v))$。因为 $g_N$ 是一个黎曼度量，所以它是正定的。因此，只要 $dF_p(v)$ 不为零，上述表达式就为正。而 $dF_p$ 的[单射性](@entry_id:147722)恰好保证了当 $v \neq 0$ 时，$dF_p(v) \neq 0$。反之，如果 $F$ 在某点 $p$ 不是一个浸入，那么存在一个非零向量 $v \in \ker(dF_p)$，此时 $(F^*g_N)_p(v,v) = (g_N)_{F(p)}(0,0) = 0$，诱导的张量在该点是退化的，不能构成黎曼度量 [@problem_id:2980779]。

#### [局部坐标](@entry_id:181200)下的计算

在实际计算中，[子流形](@entry_id:159439)通常由一个局部[参数化](@entry_id:272587)给出。假设 $M$ 是一个 $m$ 维[流形](@entry_id:153038)，$N$ 是一个 $n$ 维[流形](@entry_id:153038) ($m \le n$)。设 $(x^1, \dots, x^m)$ 是 $M$ 的[局部坐标](@entry_id:181200)，$(y^1, \dots, y^n)$ 是 $N$ 的[局部坐标](@entry_id:181200)。浸入 $F: M \to N$ 可以用一组函数 $y^\alpha = y^\alpha(x^1, \dots, x^m)$ 来表示。

在这些[坐标系](@entry_id:156346)下，$M$ 的[切空间](@entry_id:199137)由[基向量](@entry_id:199546) $\{\frac{\partial}{\partial x^i}\}$ 张成，$N$ 的[切空间](@entry_id:199137)由 $\{\frac{\partial}{\partial y^\alpha}\}$ 张成。[微分](@entry_id:158718) $dF$ 将 $M$ 的[基向量](@entry_id:199546)映为：
$$
dF\left(\frac{\partial}{\partial x^i}\right) = \sum_{\alpha=1}^n \frac{\partial y^\alpha}{\partial x^i} \frac{\partial}{\partial y^\alpha}
$$
环境度量 $g_N$ 在[局部坐标](@entry_id:181200)下可以写为 $g_N = \sum_{\alpha, \beta=1}^n (g_N)_{\alpha\beta} dy^\alpha \otimes dy^\beta$。诱导度量 $g_M$ 的分量 $(g_M)_{ij}$ 可以通过计算[基向量](@entry_id:199546)的[内积](@entry_id:158127)得到：
$$
(g_M)_{ij} = (g_M)\left(\frac{\partial}{\partial x^i}, \frac{\partial}{\partial x^j}\right) = (g_N)\left(dF\left(\frac{\partial}{\partial x^i}\right), dF\left(\frac{\partial}{\partial x^j}\right)\right)
$$
代入表达式，我们得到诱导度量分量的**基本计算公式**：
$$
(g_M)_{ij} = \sum_{\alpha, \beta=1}^n (g_N)_{\alpha\beta}(y(x)) \frac{\partial y^\alpha}{\partial x^i} \frac{\partial y^\beta}{\partial x^j}
$$
这组系数 $(g_M)_{ij}$ 通常被称为**[第一基本形式](@entry_id:274022)**的系数，尤其是在[曲面](@entry_id:267450)理论中。

**示例：非欧几里得空间中的诱导度量** [@problem_id:2980776]

考虑环境[流形](@entry_id:153038)为 $\mathbb{R}^3$，其坐标为 $(x, y, z)$，但其黎曼度量 $g$ 并非标准的[欧几里得度量](@entry_id:147197)，而是由下式定义：
$$
g_{(x,y,z)}((a,b,c),(a',b',c')) = a a' + \exp(2x) b b' + \exp(-2x) c c'
$$
或者用度量[矩阵表示](@entry_id:146025)为 $\text{diag}(1, \exp(2x), \exp(-2x))$。现在，考虑一个由参数 $(u, v)$ 给出的浸入 $F: \mathbb{R}^2 \to \mathbb{R}^3$，$F(u,v) = (u, v, uv)$。这定义了一个[双曲抛物面](@entry_id:275753)。我们来计算其上的诱导度量 $\gamma = F^*g$。

首先，建立坐标关系：$x=u, y=v, z=uv$。然后，计算[参数曲面](@entry_id:273105)上的切向量基底，即 $F$ 对参数的偏导数：
$$
\frac{\partial F}{\partial u} = \left(\frac{\partial x}{\partial u}, \frac{\partial y}{\partial u}, \frac{\partial z}{\partial u}\right) = (1, 0, v)
$$
$$
\frac{\partial F}{\partial v} = \left(\frac{\partial x}{\partial v}, \frac{\partial y}{\partial v}, \frac{\partial z}{\partial v}\right) = (0, 1, u)
$$
现在，我们可以使用诱导度量的定义来计算其分量 $\gamma_{ij}$。注意，环境度量 $g$ 的系数依赖于点的位置，因此我们需要将在 $F(u,v)=(u,v,uv)$ 点的度量代入计算。
$$
\gamma_{11}(u,v) = g_{F(u,v)}\left(\frac{\partial F}{\partial u}, \frac{\partial F}{\partial u}\right) = g_{(u,v,uv)}((1,0,v), (1,0,v))
$$
$$
= 1 \cdot 1 + \exp(2u) \cdot 0 \cdot 0 + \exp(-2u) \cdot v \cdot v = 1 + v^2 \exp(-2u)
$$
$$
\gamma_{22}(u,v) = g_{F(u,v)}\left(\frac{\partial F}{\partial v}, \frac{\partial F}{\partial v}\right) = g_{(u,v,uv)}((0,1,u), (0,1,u))
$$
$$
= 1 \cdot 0 \cdot 0 + \exp(2u) \cdot 1 \cdot 1 + \exp(-2u) \cdot u \cdot u = \exp(2u) + u^2 \exp(-2u)
$$
$$
\gamma_{12}(u,v) = g_{F(u,v)}\left(\frac{\partial F}{\partial u}, \frac{\partial F}{\partial v}\right) = g_{(u,v,uv)}((1,0,v), (0,1,u))
$$
$$
= 1 \cdot 0 + \exp(2u) \cdot 0 \cdot 1 + \exp(-2u) \cdot v \cdot u = uv \exp(-2u)
$$
因此，在 $(u,v)$ [坐标系](@entry_id:156346)下，该[曲面](@entry_id:267450)上的诱导度量张量矩阵为：
$$
(\gamma_{ij}) = \begin{pmatrix} 1 + v^2 \exp(-2u) & uv \exp(-2u) \\ uv \exp(-2u) & \exp(2u) + u^2 \exp(-2u) \end{pmatrix}
$$
这个例子清楚地表明，诱导度量的形式不仅取决于子流形的参数化方式，还深刻地依赖于环境空间的度量结构。

### [子流形](@entry_id:159439)上的几何测量

一旦我们获得了[子流形](@entry_id:159439)上的诱导度量 $g_M$，我们就可以将其视为一个独立的黎曼流形 $(M, g_M)$，并运用黎曼几何的所有标准工具来研究其内蕴几何。这包括计算曲线的长度、向量间的角度、区域的面积或体积等。

对于一个 $m$ 维[子流形](@entry_id:159439) $M$，如果它由[局部坐标](@entry_id:181200) $(u^1, \dots, u^m)$ 参数化，并且诱导度量的矩阵为 $(g_{ij})$，那么 $m$ 维的**体积元 (volume element)** $d\text{vol}_M$ 由下式给出：
$$
d\text{vol}_M = \sqrt{\det(g_{ij})} \, du^1 \wedge \dots \wedge du^m
$$
一个区域 $\Omega \subset M$ 的体积（或面积，如果 $m=2$）就是对该[体积元](@entry_id:267802)在该区域上的积分：
$$
\text{Vol}(\Omega) = \int_\Omega d\text{vol}_M = \int_{\Phi^{-1}(\Omega)} \sqrt{\det(g_{ij})} \, du^1 \dots du^m
$$
其中 $\Phi$ 是该区域的参数化。

**示例：计算[曲面](@entry_id:267450)面积** [@problem_id:2980763]

让我们计算一个在非欧空间中[曲面块的面积](@entry_id:261296)。设[环境空间](@entry_id:184743)为 $(\mathbb{R}^3, g)$，度量为 $g = dx^2 + dy^2 + \exp(2z) dz^2$。考虑由[参数化](@entry_id:272587) $\Phi(u,v) = (u, v, \ln(1+u^2+v^2))$ 定义的[曲面](@entry_id:267450) $S$。我们想计算参数域为圆盘 $D_R = \{(u,v) : u^2+v^2 \le R^2\}$ 的那部分[曲面](@entry_id:267450)的面积。

首先，计算诱导度量的分量。切向量为：
$$
\frac{\partial \Phi}{\partial u} = \left(1, 0, \frac{2u}{1+u^2+v^2}\right), \quad \frac{\partial \Phi}{\partial v} = \left(0, 1, \frac{2v}{1+u^2+v^2}\right)
$$
在[曲面](@entry_id:267450)上，$\exp(2z) = \exp(2\ln(1+u^2+v^2)) = (1+u^2+v^2)^2$。
诱导度量的分量为：
$$
g_{uu} = 1^2 + 0^2 + \exp(2z)\left(\frac{2u}{1+u^2+v^2}\right)^2 = 1 + (1+u^2+v^2)^2 \frac{4u^2}{(1+u^2+v^2)^2} = 1+4u^2
$$
$$
g_{vv} = 0^2 + 1^2 + \exp(2z)\left(\frac{2v}{1+u^2+v^2}\right)^2 = 1 + (1+u^2+v^2)^2 \frac{4v^2}{(1+u^2+v^2)^2} = 1+4v^2
$$
$$
g_{uv} = \exp(2z)\left(\frac{2u}{1+u^2+v^2}\right)\left(\frac{2v}{1+u^2+v^2}\right) = 4uv
$$
度量矩阵的行列式为 $\det(g_{ij}) = (1+4u^2)(1+4v^2) - (4uv)^2 = 1+4(u^2+v^2)$。
[面积元](@entry_id:263205)为 $dA = \sqrt{1+4(u^2+v^2)} \,du\,dv$。
现在，我们在圆盘 $D_R$ 上积分。使用极坐标 $u=r\cos\theta, v=r\sin\theta$，我们得到 $u^2+v^2=r^2$，$du\,dv=r\,dr\,d\theta$。
$$
\text{Area}(R) = \int_0^{2\pi} \int_0^R \sqrt{1+4r^2} \cdot r \,dr\,d\theta
$$
这个积分可以精确计算，结果为：
$$
\text{Area}(R) = \frac{\pi}{6}((1+4R^2)^{3/2} - 1)
$$
这个例子再次强调了，即使[子流形](@entry_id:159439)生活在一个弯曲的环境中，一旦诱导度量被确定，所有后续的[内蕴几何](@entry_id:158788)计算都遵循标准的黎曼几何法则 [@problem_id:2980782]。

### 外蕴几何：[第二基本形式](@entry_id:161454)

到目前为止，我们只关注了子流形的[内蕴几何](@entry_id:158788)。然而，子流形在[环境空间](@entry_id:184743)中的嵌入方式本身就包含了丰富的几何信息。例如，一个平面和一个圆柱面都可以被展平成一个欧几里得平面（它们的内蕴曲率都为零），但它们在三维空间中的形状显然不同。这种差异由**外蕴几何 (extrinsic geometry)** 来描述。

#### [法丛](@entry_id:272447)与切[空间分解](@entry_id:755142)

研究外蕴几何的第一步是理解[子流形](@entry_id:159439)的[切空间](@entry_id:199137) $TM$ 如何坐落在环境[流形](@entry_id:153038)的切空间 $TN$ 中。对于[子流形](@entry_id:159439) $M \subset N$ 上的每一点 $p$，切空间 $T_pM$ 是 $T_pN$ 的一个[线性子空间](@entry_id:151815)。由于 $(N, g_N)$ 是一个黎曼流形，$T_pN$ 上的度量 $g_N$ 提供了一个[内积](@entry_id:158127)。这使得我们可以定义 $T_pM$ 在 $T_pN$ 中的**[正交补](@entry_id:149922) (orthogonal complement)**，称为 $p$ 点的**法空间 (normal space)** $N_pM$：
$$
N_pM = \{ v \in T_pN \mid (g_N)_p(v,w) = 0 \text{ for all } w \in T_pM \}
$$
所有这些法空间的并集构成了 $M$ 的**[法丛](@entry_id:272447) (normal bundle)** $NM = \bigsqcup_{p \in M} N_pM$。由于 $M$ 是[光滑嵌入](@entry_id:637480)的，并且 $g_N$ 是光滑的，[法丛](@entry_id:272447) $NM$ 本身也是一个光滑的向量丛。

这样，在 $M$ 上的每一点 $p$，环境空间的切空间 $T_pN$ 都被正交[直和分解](@entry_id:263004)为切向[部分和](@entry_id:162077)法向部分：
$$
T_pN = T_pM \oplus N_pM
$$
这个分解是研究外蕴几何的基础。它允许我们将任何作用在 $T_pN$ 中的向量或[算子分解](@entry_id:154443)为切向分量和法向分量 [@problem_id:3000930]。我们将这两个投影分别记为 $(\cdot)^\top$ 和 $(\cdot)^\perp$。

#### 高斯公式与第二基本形式

现在我们提出一个关键问题：如果我们沿着[子流形](@entry_id:159439) $M$ 取两个[切向量](@entry_id:265494)场 $X, Y$，并在环境[流形](@entry_id:153038) $N$ 中计算它们的[协变导数](@entry_id:152476) $\nabla^N_X Y$（使用 $N$ 的[Levi-Civita联络](@entry_id:161107) $\nabla^N$），结果会是怎样的？$\nabla^N_X Y$ 在每一点 $p$ 的值是一个位于 $T_pN$ 中的向量，但它不一定保持在 $T_pM$ [子空间](@entry_id:150286)内。

这个向量可以被分解为它的切向和法向分量：
$$
\nabla^N_X Y = (\nabla^N_X Y)^\top + (\nabla^N_X Y)^\perp
$$
这被称为**高斯公式 (Gauss formula)**。这个公式的两个组成部分都具有深刻的几何意义：
1.  **[诱导联络](@entry_id:635081) (Induced Connection)**：切向分量 $(\nabla^N_X Y)^\top$ 定义了 $M$ 上的一个联络，我们记为 $\nabla^M_X Y$。可以证明，这个[诱导联络](@entry_id:635081) $\nabla^M$ 恰好是诱导度量 $g_M$ 的Levi-Civita联络。它无挠且与 $g_M$ 度量兼容，完全描述了 $M$ 的内蕴几何 [@problem_id:2980760]。
2.  **第二基本形式 (Second Fundamental Form)**：法向分量 $(\nabla^N_X Y)^\perp$ 衡量了 $M$ 在 $N$ 中弯曲的程度。它被称为第二基本形式，记为 $\mathrm{II}(X,Y)$。
    $$
    \mathrm{II}(X,Y) := (\nabla^N_X Y)^\perp
    $$

因此，高斯公式可以写为：
$$
\nabla^N_X Y = \nabla^M_X Y + \mathrm{II}(X,Y)
$$
第二基本形式 $\mathrm{II}$ 是一个从 $TM \times TM$ 到[法丛](@entry_id:272447) $NM$ 的[双线性映射](@entry_id:186502)。它最重要的一个性质是**对称性**：$\mathrm{II}(X,Y) = \mathrm{II}(Y,X)$。这个性质是环境联络 $\nabla^N$ 无挠性的直接推论 [@problem_id:2984398]。因为 $\nabla^N$ 无挠，所以 $\nabla^N_X Y - \nabla^N_Y X = [X,Y]$。由于 $X, Y$ 是 $M$ 上的切向量场，它们的李括号 $[X,Y]$ 也切于 $M$。因此，$[X,Y]$ 的法向分量为零。于是：
$$
\mathrm{II}(X,Y) - \mathrm{II}(Y,X) = (\nabla^N_X Y)^\perp - (\nabla^N_Y X)^\perp = (\nabla^N_X Y - \nabla^N_Y X)^\perp = ([X,Y])^\perp = 0
$$
如果 $\mathrm{II}(X,Y)$ 对于所有切于 $M$ 的 $X, Y$ 恒为零，那么子流形 $M$ 被称为**[全测地子流形](@entry_id:637049) (totally geodesic submanifold)**。这意味着任何在 $M$ 中开始的[测地线](@entry_id:269969)（相对于诱导度量 $g_M$），也必定是环境[流形](@entry_id:153038) $N$ 中的[测地线](@entry_id:269969)。例如，$\mathbb{S}^3$ 中的一个“大球面” $\mathbb{S}^2$ 就是一个[全测地子流形](@entry_id:637049)。沿着 $\mathbb{S}^2$ 上大圆（即 $\mathbb{S}^2$ 的[测地线](@entry_id:269969)）的加速度向量始终切于 $\mathbb{S}^2$，因此其在 $\mathbb{S}^3$ 中的法向分量为零 [@problem_id:2980756]。

#### 形算子

[第二基本形式](@entry_id:161454) $\mathrm{II}(X,Y)$ 是一个取值于[法丛](@entry_id:272447) $NM$ 的向量。为了将其与[切空间](@entry_id:199137)上的几何联系起来，我们引入了**形算子 (shape operator)**（或称[Weingarten映射](@entry_id:271773)）。对于[法丛](@entry_id:272447)中的任意一个[法向量场](@entry_id:268853) $\nu$，我们定义形算子 $A_\nu$ 是一个作用在[切丛](@entry_id:161294) $TM$ 上的线性算子（一个 $(1,1)$-张量），$A_\nu: TM \to TM$，它通过以下关系与[第二基本形式](@entry_id:161454)联系起来：
$$
g_M(A_\nu X, Y) = g_N(\mathrm{II}(X,Y), \nu)
$$
对于所有的切向量场 $X, Y$。这个定义利用了 $g_N$ 在 $T_pN$ 上的[内积](@entry_id:158127)结构。形算子 $A_\nu$ 描述了[子流形](@entry_id:159439)在 $\nu$ 方向上的弯曲情况。

利用 $\mathrm{II}$ 的对称性，我们可以证明 $A_\nu$ 是一个**[自伴算子](@entry_id:152188)**，即关于度量 $g_M$ 是对称的：
$$
g_M(A_\nu X, Y) = g_N(\mathrm{II}(X,Y), \nu) = g_N(\mathrm{II}(Y,X), \nu) = g_M(A_\nu Y, X) = g_M(X, A_\nu Y)
$$
这个性质非常重要，因为它保证了在每一点 $p \in M$，$A_\nu$ 都有实[特征值](@entry_id:154894)。对于[余维](@entry_id:273141)为1的超曲面，这些[特征值](@entry_id:154894)被称为**[主曲率](@entry_id:270598) (principal curvatures)**，它们描述了[曲面](@entry_id:267450)在主方向上的弯曲程度 [@problem_id:2984398]。

形算子也出现在对[法向量场](@entry_id:268853)进行[协变微分](@entry_id:263981)的公式中。**魏因加滕公式 (Weingarten formula)** 描述了 $\nabla^N_X \nu$ 的分解：
$$
\nabla^N_X \nu = -A_\nu(X) + \nabla^\perp_X \nu
$$
其中 $-A_\nu(X)$ 是其切向分量，而 $\nabla^\perp_X \nu = (\nabla^N_X \nu)^\perp$ 是其法向分量，它定义了[法丛](@entry_id:272447)中的一个联络。$g_M(A_\nu X, Y) = g_N(\mathrm{II}(X,Y), \nu)$ 这个基本关系式可以从 $\nabla^N$ 的[度量兼容性](@entry_id:265910)直接导出 [@problem_id:2980760, @problem_id:3000930]。

### 子流形的曲率：[高斯和](@entry_id:196588)[科达齐方程](@entry_id:635135)

我们现在已经拥有了联系[内蕴几何](@entry_id:158788)（由 $\nabla^M$ 描述）和外蕴几何（由 $\mathrm{II}$ 和 $A_\nu$ 描述）的工具。这些工具的最终结合体现在一组基本方程中，它们将[子流形](@entry_id:159439)的曲率张量 $R^M$ 与环境[流形](@entry_id:153038)的[曲率张量](@entry_id:181383) $R^N$ 联系起来。

#### [高斯方程](@entry_id:192573)

[黎曼曲率张量](@entry_id:160189) $R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]} Z$ 衡量了[协变导数](@entry_id:152476)沿不同路径的不[可交换性](@entry_id:263314)。通过反复应用高斯公式和魏因加滕公式，并细致地将各项分解到切空间和法空间，我们可以推导出[子流形](@entry_id:159439)的[曲率张量](@entry_id:181383) $R^M$ 与环境[流形](@entry_id:153038)的曲率张量 $R^N$ 之间的关系。这个著名的关系式被称为**[高斯方程](@entry_id:192573) (Gauss equation)**：
$$
g_M(R^M(X,Y)Z, W) = g_N(R^N(X,Y)Z, W) + g_N(\mathrm{II}(X,W), \mathrm{II}(Y,Z)) - g_N(\mathrm{II}(X,Z), \mathrm{II}(Y,W))
$$
其中 $X,Y,Z,W$ 都是 $M$ 的[切向量](@entry_id:265494)场。

[高斯方程](@entry_id:192573)揭示了一个深刻的真理：子流形的内蕴曲率由两部分贡献。第一部分 $g_N(R^N(X,Y)Z, W)$ 是直接从环境空间的曲率中“继承”来的。第二部分 $g_N(\mathrm{II}(X,W), \mathrm{II}(Y,Z)) - g_N(\mathrm{II}(X,Z), \mathrm{II}(Y,W))$ 则完全由[第二基本形式](@entry_id:161454)决定，纯粹是由于子流形在[环境空间](@entry_id:184743)中的弯曲而产生的。

高斯最著名的“[绝妙定理](@entry_id:159067) (Theorema Egregium)”是该方程的一个直接推论。对于一个嵌入在三维[欧几里得空间](@entry_id:138052) $\mathbb{R}^3$ 中的二维[曲面](@entry_id:267450)，环境空间是平坦的，即 $R^N=0$。此时，[高斯方程](@entry_id:192573)简化为：
$$
g_M(R^M(X,Y)Z, W) = g_N(\mathrm{II}(X,W), \mathrm{II}(Y,Z)) - g_N(\mathrm{II}(X,Z), \mathrm{II}(Y,W))
$$
这表明[曲面](@entry_id:267450)的内蕴曲率（例如[高斯曲率](@entry_id:149725) $K$）完全由其[第二基本形式](@entry_id:161454)（即[第一基本形式](@entry_id:274022)和[第二基本形式](@entry_id:161454)的系数）确定。高斯曲率 $K$ 恰好是形算子的[行列式](@entry_id:142978)。

**示例：环面的[高斯曲率](@entry_id:149725)** [@problem_id:2980778]

考虑一个由参数 $a>b>0$ 定义的环面，[浸入](@entry_id:161534)到 $\mathbb{R}^3$ 中。我们可以计算其[第一基本形式](@entry_id:274022) $(g_{ij})$ 和[第二基本形式](@entry_id:161454) $(h_{ij})$ 的系数，发现[坐标系](@entry_id:156346)是正交的（$g_{12}=0$）且是[主曲率](@entry_id:270598)方向（$h_{12}=0$）。[高斯曲率](@entry_id:149725) $K$ 是两个[主曲率](@entry_id:270598)的乘积，也可以通过公式 $K = \frac{\det(h_{ij})}{\det(g_{ij})}$ 计算得出。对于由参数 $(u,v)$ 参数化的环面 $X(u,v) = ((a+b\cos v)\cos u, (a+b\cos v)\sin u, b\sin v)$，计算可得：
$$
K(u,v) = \frac{\cos v}{b(a+b\cos v)}
$$
这个结果表明，环面外圈（$v \approx 0, \cos v > 0$）的高斯曲率为正，内圈（$v \approx \pi, \cos v < 0$）的[高斯曲率](@entry_id:149725)为负，而顶部和底部的两个圆周（$v = \pm \pi/2, \cos v=0$）高斯曲率为零。这完全符合我们的直观想象，并且这个内蕴几何量是通过外蕴的嵌入方式计算出来的。

#### [科达齐方程](@entry_id:635135)

[高斯方程](@entry_id:192573)描述了切向的几何。还有另一个基本方程，称为**科达齐-迈纳尔迪方程 (Codazzi-Mainardi equation)**，它描述了[第二基本形式](@entry_id:161454)的协变导数必须满足的约束。它本质上是 $\nabla^N_X \nabla^N_Y Z$ 的法向分量对称性的体现。[科达齐方程](@entry_id:635135)可以写作：
$$
(\nabla_X \mathrm{II})(Y,Z) = (\nabla_Y \mathrm{II})(X,Z)
$$
其中 $(\nabla_X \mathrm{II})(Y,Z)$ 是[第二基本形式](@entry_id:161454)的协变导数，它混合了 $M$ 和 $NM$ 上的联络。这个方程可以被看作是子流形能够存在于环境空间中的“[可积性](@entry_id:142415)条件”。对于前述的环面例子，我们可以直接计算并验证[科达齐方程](@entry_id:635135)成立 [@problem_id:2980778]。

### 全局性质：完备性

最后，我们简要讨论一个全局性的问题。一个自然的疑问是：如果环境[流形](@entry_id:153038) $(N, g_N)$ 是完备的（即每条[测地线](@entry_id:269969)都可以无限延伸），那么其上的子流形 $(M, g_M)$ 是否也一定是完备的？

答案是否定的。子流形的完备性与其在[环境空间](@entry_id:184743)中的[拓扑性质](@entry_id:141605)密切相关。**[霍普夫-里诺定理](@entry_id:160628) (Hopf-Rinow Theorem)** 的一个重要推论是：**[完备黎曼流形](@entry_id:182954) $(N, g_N)$ 的一个连通子流形 $(M, g_M)$ 是完备的，当且仅当 $M$ 是 $N$ 的一个[闭集](@entry_id:136446)。**

**示例：不完备的子流形** [@problem_id:3028619]

考虑[环境空间](@entry_id:184743)为完备的欧几里得平面 $\mathbb{R}^2$。令[子流形](@entry_id:159439) $S$ 是由开区间 $(0,1)$ 参数化的抛物线弧 $i(t) = (t, t^2)$。$S$ 是一个[浸入子流形](@entry_id:264923)，但它不是 $\mathbb{R}^2$ 中的[闭集](@entry_id:136446)，因为它的闭包包含了点 $(0,0)$ 和 $(1,1)$，而这两点都不属于 $S$。

根据[霍普夫-里诺定理](@entry_id:160628)的推论，$S$ 上的诱导度量应该是不完备的。我们可以构造一个柯西序列来验证这一点。考虑序列 $p_n = i(1/n) = (1/n, 1/n^2)$，其中 $n \ge 2$。这个序列在[环境空间](@entry_id:184743) $\mathbb{R}^2$ 中收敛于 $(0,0)$。然而，在 $S$ 的内蕴度量（即弧长）下，这个序列是柯西的，但它在 $S$ 中没有[极限点](@entry_id:177089)，因为它“逃逸”到了 $S$ 的一个“边界洞”——点 $(0,0)$。我们可以计算从 $t=0$ 到 $t=1$ 的总[弧长](@entry_id:191173)，发现它是一个有限值：$\frac{\sqrt{5}}{2} + \frac{1}{4}\ln(2+\sqrt{5})$。这直观地解释了不完备性：一个身处 $S$ 上的观察者可以在有限的时间内“走到”[流形](@entry_id:153038)的尽头。

这个例子说明，即使环境空间是“良好”的（完备的），[子流形](@entry_id:159439)也可能因为其“开放”的[拓扑性质](@entry_id:141605)而表现出不完备的几何行为。