## 引言
在微分几何的研究中，仿射联络为我们提供了在弯曲流形上比较和微分向量场的关键工具。然而，联络本身蕴含着丰富的几何结构，其中一个核心概念便是**挠率**（Torsion）。挠率从本质上捕捉了由联络定义的平行移动在无穷小尺度下产生的“扭曲”或“缠绕”效应，是衡量联络对称性的基本不变量。尽管标准黎曼几何主要研究无挠的Levi-Civita联络，但对挠率的深入理解对于探索更广阔的几何世界——包括李群理论、广义相对论的替代理论以及材料科学中的缺陷模型——是不可或缺的。本文旨在系统性地填补这一认知空白，全面解析挠率的理论与实践。

本文将分为三个核心部分，带领读者层层深入。在“**原理与机制**”一章中，我们将从挠率的定义出发，证明其张量性，并揭示其与Christoffel符号的直接关系，最终阐明它在黎曼几何基本定理中的关键作用。接下来，“**应用与跨学科联系**”一章将展示挠率远非纯粹的数学抽象，我们将探讨它如何作为一种描述性语言，在引力理论、连续介质力学和现代几何结构理论中发挥核心作用，并揭示挠率与曲率的独立性。最后，在“**动手实践**”部分，读者将通过一系列精心设计的问题，将理论知识转化为具体的计算和推导能力，从而真正内化对挠率的理解。通过这一完整的学习路径，读者将能够掌握联络挠率的深刻内涵及其在现代科学中的广泛影响。

## 原理与机制

在引入了光滑流形上的仿射联络之后，我们现在转向研究其内在结构的一个基本方面：**挠率**（Torsion）。正如其名，挠率捕捉了联络所定义的平行移动在无穷小尺度下的“扭曲”或“缠绕”程度。虽然在纯粹的黎曼几何中，我们主要关注的Levi-Civita联络是无挠的，但理解挠率的概念对于更广泛的微分几何、李群理论乃至广义相对论的某些替代理论（如爱因斯坦-嘉当理论）都至关重要。本章将系统地阐述挠率的定义、基本性质及其深刻的几何意义。

### 挠率的定义与张量性

回想一下，一个仿射联络 $\nabla$ 提供了沿一个向量场方向对另一个向量场进行求导的方法。一个自然的问题是，沿着两个不同方向的无穷小位移所构成的“平行四边形”是否能够闭合。具体来说，从一点 $p$ 出发，先沿向量场 $X$ 的方向移动一个无穷小量 $\epsilon$，再沿 $Y$ 的方向移动 $\delta$，与先沿 $Y$ 移动 $\delta$ 再沿 $X$ 移动 $\epsilon$ 所到达的终点是否相同？这两个路径的终点之间的无穷小位移向量由李括号 $[X,Y]$ 描述。

然而，联络 $\nabla$ 本身也定义了一种沿着曲线移动向量的方式。我们可以用 $\nabla_X Y$ 和 $\nabla_Y X$ 来衡量向量场 $Y$ 沿 $X$ 的变化以及 $X$ 沿 $Y$ 的变化。挠率张量正是联络定义的这种非交换性（$\nabla_X Y$ 与 $\nabla_Y X$）与向量场本身的非交换性（由 $[X,Y]$ 描述）之间的差异。

**定义 2.1 (挠率张量)**：设 $\nabla$ 是光滑流形 $M$ 上的一个仿射联络。其**挠率张量**（Torsion Tensor）$T$ 是一个映射 $T: \mathfrak{X}(M) \times \mathfrak{X}(M) \to \mathfrak{X}(M)$，定义为：
$$
T(X, Y) = \nabla_X Y - \nabla_Y X - [X, Y]
$$
对于任意光滑向量场 $X, Y \in \mathfrak{X}(M)$。

一个第一眼看上去并不明显的关键性质是，尽管 $T$ 的定义中包含了联络和李括号这两个微分算子，其结果 $T(X,Y)$ 在某点 $p$ 的值却只依赖于 $X$ 和 $Y$ 在 $p$ 点的向量值 $X_p$ 和 $Y_p$。换言之，$T$ 是一个张量场，而非微分算子。这源于一个精巧的代数抵消 [@problem_id:1685041]。

为了证明 $T$ 是一个 $(1,2)$-张量场，我们需要验证它对于 $C^\infty(M)$ 中的光滑函数是双线性的。我们来检验其在第一个变量上的 $C^\infty(M)$-线性，设 $f \in C^\infty(M)$：
$$
T(fX, Y) = \nabla_{fX} Y - \nabla_Y (fX) - [fX, Y]
$$
根据联络和李括号的性质 [@problem_id:2996967] [@problem_id:1685041]：
1.  $\nabla_{fX} Y = f \nabla_X Y$ （联络在第一个变量上的 $C^\infty(M)$-线性）
2.  $\nabla_Y (fX) = (Yf)X + f \nabla_Y X$ （联络在第二个变量上的Leibniz法则）
3.  $[fX, Y] = f[X, Y] - (Yf)X$ （李括号的性质）

将这些代入上式：
$$
\begin{aligned}
T(fX, Y)  &= (f \nabla_X Y) - \big( (Yf)X + f \nabla_Y X \big) - \big( f[X, Y] - (Yf)X \big) \\
 &= f \nabla_X Y - (Yf)X - f \nabla_Y X - f[X, Y] + (Yf)X \\
 &= f (\nabla_X Y - \nabla_Y X - [X, Y]) \\
 &= f T(X, Y)
\end{aligned}
$$
可以看到，来自 $\nabla_Y(fX)$ 的非张量项 $(Yf)X$ 与来自 $[fX,Y]$ 的非张量项 $-(Yf)X$ 恰好相互抵消了。同理可证 $T(X, fY) = f T(X, Y)$。因此，$T$ 确实是一个 $(1,2)$-张量场。

此外，从定义可以直接看出挠率张量是**反对称**的：
$$
T(Y, X) = \nabla_Y X - \nabla_X Y - [Y, X] = -(\nabla_X Y - \nabla_Y X - [X, Y]) = -T(X, Y)
$$
如果一个联络的挠率张量恒为零，$T \equiv 0$，我们称该联络是**无挠**（torsion-free）或**对称**（symmetric）的。由定义可知，无挠条件等价于 $\nabla_X Y - \nabla_Y X = [X, Y]$ 对于所有向量场 $X, Y$ 成立 [@problem_id:2996967]。

### 局部坐标下的挠率

为了更具体地理解挠率，我们考察其在局部坐标系 $(x^i)$ 中的表达式。设 $\{\partial_i\}$ 是坐标基向量场，联络的Christoffel符号 $\Gamma^k_{ij}$ 定义为 $\nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k$（此处及以后均使用Einstein求和约定）。

由于坐标基向量场的李括号为零，即 $[\partial_i, \partial_j] = 0$，我们可以直接计算挠率张量在基向量场上的分量 [@problem_id:3032135] [@problem_id:3032134]：
$$
\begin{aligned}
T(\partial_i, \partial_j) &= \nabla_{\partial_i} \partial_j - \nabla_{\partial_j} \partial_i - [\partial_i, \partial_j] \\
&= \Gamma^k_{ij} \partial_k - \Gamma^k_{ji} \partial_k - 0 \\
&= (\Gamma^k_{ij} - \Gamma^k_{ji}) \partial_k
\end{aligned}
$$
挠率张量的分量 $T^k_{ij}$ 定义为 $T(\partial_i, \partial_j) = T^k_{ij} \partial_k$。比较两式，我们得到挠率分量的坐标表达式：
$$
T^k_{ij} = \Gamma^k_{ij} - \Gamma^k_{ji}
$$
这个表达式非常直观地揭示了挠率的本质：它就是Christoffel符号在下面两个指标上的反对称部分。从这个表达式可以立刻看出 $T^k_{ij} = -T^k_{ji}$。

因此，一个联络是**无挠的，当且仅当其Christoffel符号对于下指标是对称的**，即 $\Gamma^k_{ij} = \Gamma^k_{ji}$ 对于所有 $i, j, k$ 成立 [@problem_id:3032134] [@problem_id:2996967]。这就是为什么无挠联络有时也被称为对称联络。

**示例 2.1**：考虑 $\mathbb{R}^3$ 上的一个仿射联络 $\nabla$，其在标准直角坐标系 $(x^1, x^2, x^3)$ 中的非零Christoffel符号仅为 $\Gamma^3_{12} = x^1$ 和 $\Gamma^3_{21} = x^2$。对于向量场 $X = x^1 \frac{\partial}{\partial x^1}$ 和 $Y = x^2 \frac{\partial}{\partial x^2}$，我们可以计算 $T(X,Y)$ [@problem_id:1685048]。
其挠率分量中，唯一可能非零的是
$$ T^3_{12} = \Gamma^3_{12} - \Gamma^3_{21} = x^1 - x^2 $$
且 $T^3_{21} = -T^3_{12} = x^2 - x^1$。根据挠率的张量性，$T(X,Y)$ 的第 $k$ 个分量为 $T^k_{ij} X^i Y^j$。在本例中，
$$ T(X,Y) = (T^3_{12} X^1 Y^2 + T^3_{21} X^2 Y^1) \frac{\partial}{\partial x^3} = ((x^1 - x^2)(x^1)(x^2) + 0) \frac{\partial}{\partial x^3} = x^1 x^2 (x^1 - x^2) \frac{\partial}{\partial x^3} $$
这提供了一个具体的例子，说明非对称的Christoffel符号如何产生非零的挠率。

### 联络的分解

挠率的坐标表达式启发了一个优美的结构性结果：任何仿射联络都可以唯一地分解为一个无挠联络和一个张量场之和。

设 $\nabla$ 是一个任意的仿射联络，其Christoffel符号为 $\Gamma^k_{ij}$。我们可以定义一个新的联络 $\mathring{\nabla}$，其Christoffel符号 $\mathring{\Gamma}^k_{ij}$ 是 $\Gamma^k_{ij}$ 的对称部分 [@problem_id:1685031]：
$$
\mathring{\Gamma}^k_{ij} = \frac{1}{2} (\Gamma^k_{ij} + \Gamma^k_{ji})
$$
显然，$\mathring{\Gamma}^k_{ij} = \mathring{\Gamma}^k_{ji}$，所以 $\mathring{\nabla}$ 是一个无挠联络。
原联络 $\nabla$ 和这个无挠部分 $\mathring{\nabla}$ 的差是一个张量 $A$：
$$
A(X,Y) = \nabla_X Y - \mathring{\nabla}_X Y
$$
其坐标分量为：
$$
A^k_{ij} = \Gamma^k_{ij} - \mathring{\Gamma}^k_{ij} = \Gamma^k_{ij} - \frac{1}{2} (\Gamma^k_{ij} + \Gamma^k_{ji}) = \frac{1}{2} (\Gamma^k_{ij} - \Gamma^k_{ji}) = \frac{1}{2} T^k_{ij}
$$
因此，我们有 $\nabla_X Y = \mathring{\nabla}_X Y + \frac{1}{2} T(X, Y)$。这表明任何联络 $\nabla$ 都可以被看作是其内在的无挠部分 $\mathring{\nabla}$ 加上一个由其自身挠率决定的张量项 $\frac{1}{2}T$。这种分解是唯一的。

### 挠率、度量与Levi-Civita联络

在黎曼流形 $(M, g)$ 上，联络除了挠率性质外，还可以与度量 $g$ 发生相互作用。如果一个联络 $\nabla$ 在平行移动下保持向量的内积不变，则称该联络是**度量兼容**（metric-compatible）的。这等价于协变导数 $\nabla g$ 为零，或者用Leibniz法则的形式表达为 [@problem_id:3032134]：
$$
X\big(g(Y,Z)\big) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z)
$$
对于任意向量场 $X, Y, Z$ 成立。

**黎曼几何基本定理**断言：在任意黎曼流形 $(M, g)$ 上，**存在唯一一个**既**度量兼容**又**无挠**的仿射联络。这个特殊的联络被称为**Levi-Civita联络**或黎曼联络，记为 $\nabla^g$。

这个定理的唯一性部分至关重要，它凸显了无挠条件和度量兼容条件的根本性。我们可以通过考察两个联络 $\nabla$ 和 $\widetilde{\nabla}$ 的差 $A_X Y = \widetilde{\nabla}_X Y - \nabla_X Y$ 来理解为什么需要这两个条件 [@problem_id:3032163]。
- 如果两个联络都是度量兼容的，它们的差张量 $A$ 满足 $g(A_X Y, Z) + g(Y, A_X Z) = 0$。这意味着对任意 $X$，$A_X$ 是一个反对称的线性变换。
- 如果两个联络都是无挠的，它们的差张量 $A$ 满足 $A_X Y = A_Y X$。这意味着张量 $A$ 在其低维指标上是对称的。

如果一个张量 $g(A_X Y, Z)$ 同时满足关于后两个变量的反对称性和关于前两个变量的对称性，那么它必然恒为零。这证明了同时满足这两个条件的联络是唯一的。

如果放弃其中任何一个条件，唯一性就将丧失：
- **放弃无挠性**：我们可以从Levi-Civita联络 $\nabla^g$ 出发，构造新的度量兼容联络。任取一个非零的3-形式 $\beta$，定义一个张量 $A$ 使得 $g(A_X Y, Z) = \beta(X,Y,Z)$。这样构造的联络 $\widetilde{\nabla} = \nabla^g + A$ 仍然是度量兼容的，但其挠率 $T^{\widetilde{\nabla}}$ 非零，由关系 $g(T^{\widetilde{\nabla}}(X,Y), Z) = 2\beta(X,Y,Z)$ 给出。这意味着存在无穷多个有挠的度量兼容联络 [@problem_id:3032163]。
- **放弃度量兼容性**：同样，我们可以构造新的无挠联络。任取一个非零的1-形式 $\omega$，定义 $A_X Y = \omega(X)Y + \omega(Y)X - g(X,Y)\omega^\sharp$（其中 $\omega^\sharp$ 是 $\omega$ 的度量对偶）。这样构造的联络 $\widetilde{\nabla} = \nabla^g + A$ 仍然是无挠的，但不再是度量兼容的 [@problem_id:3032163]。

### 挠率的几何后果

挠率的存在会对流形的几何产生深刻影响，改变了我们对“直线”和“平坦”等基本概念的理解。

#### 自平行曲线与测地线

在黎曼几何中，“直线”的概念由测地线（geodesics）来扮演。测地线是局部最短路径的曲线，它们是能量泛函 $E(\gamma) = \frac{1}{2} \int g(\dot{\gamma}, \dot{\gamma}) dt$ 的临界点。其变分所得到的Euler-Lagrange方程是**测地线方程**：
$$
\nabla^g_{\dot{\gamma}} \dot{\gamma} = 0
$$
注意到这个方程只依赖于度量 $g$ 及其诱导的Levi-Civita联络 $\nabla^g$ [@problem_id:3032127]。

然而，对于一个任意的仿射联络 $\nabla$（可能有挠），我们可以定义另一类“直”线，即**自平行曲线**（autoparallel curves）。这些曲线的切向量在沿自身移动时保持“平行”，其方程为：
$$
\nabla_{\dot{\gamma}} \dot{\gamma} = 0
$$
如果联络 $\nabla$ 无挠且度量兼容（即 $\nabla = \nabla^g$），那么自平行曲线和测地线是同一回事。但如果 $\nabla$ 有挠率，这两者通常是不同的。设 $\nabla = \nabla^g + K$，其中 $K$ 是一个张量场，被称为**挠差张量**（contorsion tensor）。自平行方程变为：
$$
\nabla^g_{\dot{\gamma}} \dot{\gamma} + K(\dot{\gamma}, \dot{\gamma}) = 0
$$
这表明，一个有挠联络的自平行曲线的“测地曲率”$\nabla^g_{\dot{\gamma}} \dot{\gamma}$ 等于 $-K(\dot{\gamma}, \dot{\gamma})$。一般情况下 $K(X,X)$ 不为零，因此自平行曲线不再是测地线 [@problem_id:3032127]。

一个有趣且重要的特例是，当挠率张量 $T$ 所对应的 $(0,3)$-张量 $H(X,Y,Z) = g(T(X,Y),Z)$ 是一个3-形式（即全反对称）时，可以证明 $K(X,X)=0$。在这种情况下，尽管挠率非零，自平行曲线与测地线仍然重合 [@problem_id:3032127]。这在爱因斯坦-嘉当理论等物理模型中具有重要意义。

#### 活动标架法中的挠率

挠率在Élie Cartan的活动标架法中有着尤为简洁和深刻的表述。设 $\{e_i\}$ 是一个局部标架场，$\{\theta^i\}$ 是其对偶余标架场。联络 $\nabla$ 由一组联络1-形式 $\omega^i{}_j$ 定义，满足 $\nabla e_j = \omega^i{}_j \otimes e_i$。挠率被表示为一组2-形式 $T^i$，它们由**Cartan第一结构方程**给出 [@problem_id:3032140] [@problem_id:3032157]：
$$
T^i = d\theta^i + \omega^i{}_j \wedge \theta^j
$$
这个方程优雅地将挠率 $T^i$ 与余标架的非完整性（由 $d\theta^i$ 衡量）和联络形式 $\omega^i{}_j$联系在一起。无挠条件 $T^i=0$ 变为 $d\theta^i = -\omega^i{}_j \wedge \theta^j$。

如果标架是**正交**的（即 $g(e_i, e_j) = \delta_{ij}$），那么度量兼容性条件等价于联络1-形式矩阵 $(\omega_{ij})$ 的反对称性，$\omega_{ij} + \omega_{ji} = 0$，其中 $\omega_{ij} = \delta_{ik}\omega^k{}_j$ [@problem_id:3032140] [@problem_id:3032157]。结合无挠条件，这两个代数约束唯一确定了Levi-Civita联络的联络形式。

#### 挠率与分布的可积性

挠率与子流形几何及叶状结构理论中的可积性问题密切相关。根据Frobenius定理，一个秩为 $r$ 的分布 $D \subset TM$ 是可积的（即局部上是 $r$ 维子流形的切空间的集合），当且仅当它在李括号下是闭合的。

使用无挠联络，我们可以将这个条件转化为对联络形式的约束。设有一个适应于分布 $D$ 的局部标架，使得 $D = \mathrm{span}\{e_1, \dots, e_r\}$。其零化子由 $\{\theta^{r+1}, \dots, \theta^n\}$ 张成。Frobenius可积性条件等价于 $d\theta^a \equiv 0 \pmod{I}$，其中 $I$ 是由 $\{\theta^{r+1}, \dots, \theta^n\}$ 生成的理想，$a \in \{r+1, \dots, n\}$。

对于一个无挠联络，Cartan第一结构方程给出 $d\theta^a = - \sum_{i=1}^r \omega^a{}_i \wedge \theta^i - \sum_{b=r+1}^n \omega^a{}_b \wedge \theta^b$。可积性条件于是简化为 $\sum_{i=1}^r \omega^a{}_i \wedge \theta^i \equiv 0 \pmod{I}$ [@problem_id:3032157]。进一步分析可知，这等价于分布的第二基本形式的对称性。这揭示了挠率（或其缺失）在判定几何结构是否能“平滑地”拼凑成更高维对象方面所扮演的核心角色。

总结而言，挠率张量是仿射联络的一个基本不变量。它衡量了无穷小平行四边形的不闭合性，其消失与否定义了联络的对称性，并从根本上区分了作为最短路径的测地线与作为“最直”路径的自平行曲线。在黎曼几何的框架下，无挠条件与度量兼容条件一起，唯一地指定了与度量结构内在关联的Levi-Civita联络，从而将挠率的存在视为一种可被施加于黎曼流形之上的附加几何结构。