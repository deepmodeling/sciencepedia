## 引言
在平坦的[欧氏空间](@entry_id:138052)中，布朗运动作为一种无处不在的[随机过程](@entry_id:159502)，其数学描述已臻于成熟。然而，当我们将视线投向弯曲的几何空间，如地球表面或更抽象的数学[流形](@entry_id:153038)时，一个根本性的问题浮现出来：我们如何定义一个“无方向偏好”的随机漫步？简单地在[局部坐标](@entry_id:181200)中应用[标准布朗运动](@entry_id:197332)会破坏其内在的几何一致性，使得过程依赖于观察者的坐标选择。这一知识鸿沟催生了“[流形上的布朗运动](@entry_id:188542)”这一深刻而优美的理论，它不仅是[随机分析](@entry_id:188809)的自然延伸，更是连接现代微分几何、概率论与[偏微分方程分析](@entry_id:753283)三大领域的关键桥梁。

本文旨在系统地阐述[流形](@entry_id:153038)上布朗运动的核心理论及其广泛影响。我们将带领读者穿越这一交叉学科的迷人景观，从基本原理出发，直至前沿应用。在“原理与机制”一章中，我们将奠定必要的黎曼几何基础，并从无穷小生成元、[随机微分方程](@entry_id:146618)和随机展开三个互补的视角严格定义布朗运动，揭示其内在的几何本质。随后，在“应用与跨学科联系”一章中，我们将展示这一理论如何化身为强大的分析工具，用于探测[流形](@entry_id:153038)的几何与拓扑，并作为一种通用语言，在物理学、生物学甚至金融学中构建和解决问题。最后，“动手实践”部分将通过具体的计算问题，巩固读者对核心概念的理解，将抽象理论付诸实践。通过这一旅程，读者将领会到，[流形上的布朗运动](@entry_id:188542)不仅是一个数学对象，更是一种用随机方法思考和理解几何世界的强大[范式](@entry_id:161181)。

## 原理与机制

本章旨在深入探讨[流形](@entry_id:153038)上布朗运动的核心原理与机制。在前一章介绍其背景与意义之后，我们现在将系统地建立在黎曼流形上定义和分析扩散过程所需的几何与[随机分析](@entry_id:188809)工具。我们将从黎曼几何的基本构件开始，逐步引入三种等价但视角各异的布朗运动定义方式，并最终探讨其深刻的路径性质及其在[几何分析](@entry_id:157700)中的应用。

### [流形](@entry_id:153038)上的几何基础

一个[光滑流形](@entry_id:160799)本身只具备拓扑和[微分](@entry_id:158718)结构，不足以定义如长度、角度或体积等几何概念。为了进行[几何分析](@entry_id:157700)，我们必须为[流形](@entry_id:153038)赋予额外的结构，其中最核心的就是**黎曼度量 (Riemannian metric)**。

一个[黎曼度量](@entry_id:754359) $g$ 是在[流形](@entry_id:153038) $M$ 上光滑指定的一个(0,2)-型[对称正定](@entry_id:145886)张量场。这意味着，在[流形](@entry_id:153038)上的每一点 $x \in M$， $g_x$ 都为该点的[切空间](@entry_id:199137) $T_xM$ 赋予了一个[内积](@entry_id:158127) [@problem_id:2995634]。具体来说，$g_x: T_xM \times T_xM \to \mathbb{R}$ 是一个[双线性形式](@entry_id:746794)，满足：
1.  **对称性**: 对任意 $u, v \in T_xM$，有 $g_x(u, v) = g_x(v, u)$。
2.  **[正定性](@entry_id:149643)**: 对任意非[零向量](@entry_id:156189) $v \in T_xM$，有 $g_x(v, v) > 0$。

一旦每个切空间都具备了[内积](@entry_id:158127)结构，我们便可以自然地定义[切向量](@entry_id:265494)的**长度 (length)** 或范数，以及向量间的**角度 (angle)**。对于 $v \in T_xM$，其长度为 $\|v\|_g = \sqrt{g_x(v, v)}$。对于两个非零向量 $u, v \in T_xM$，它们之间的夹角 $\theta$ 由下式确定 [@problem_id:2995634]：
$$
\cos\theta = \frac{g_x(u,v)}{\|u\|_g \|v\|_g}
$$
柯西-施瓦茨不等式保证了上式右边的值总在 $[-1, 1]$ 区间内。值得注意的是，这些几何量是内蕴的，其值不依赖于我们如何描述或嵌入[流形](@entry_id:153038)。例如，一条光滑曲线 $\gamma: [a,b] \to M$ 的长度可以通过对其速度[向量的范数](@entry_id:154882)进行积分来计算 [@problem_id:2995634]：
$$
L_g(\gamma) = \int_a^b \|\dot{\gamma}(t)\|_g \,dt = \int_a^b \sqrt{g_{\gamma(t)}(\dot{\gamma}(t),\dot{\gamma}(t))} \,dt
$$
在[局部坐标](@entry_id:181200)图 $(U, (x^1, \dots, x^n))$ 中，度量 $g$ 可以由一个光滑的 $n \times n$ 对称正定矩阵场 $[g_{ij}(x)]$ 来表示，其分量为 $g_{ij}(x) = g_x(\frac{\partial}{\partial x^i}, \frac{\partial}{\partial x^j})$。两个向量 $v = v^i \frac{\partial}{\partial x^i}$ 和 $w = w^j \frac{\partial}{\partial x^j}$ 的[内积](@entry_id:158127)可以表示为 $g_x(v,w) = g_{ij}(x) v^i w^j$（这里使用了爱因斯坦求和约定）。当[坐标系](@entry_id:156346)变换时，$g_{ij}$ 的分量会遵循张量的变换法则，从而确保 $g_x(v,w)$ 的计算结果是一个与坐标选择无关的标量，这体现了黎曼度量的[几何不变性](@entry_id:637068) [@problem_id:2995634]。

[黎曼度量](@entry_id:754359)还提供了一个在[切丛](@entry_id:161294) $TM$ 和其对偶丛——[余切丛](@entry_id:185138) $T^*M$ 之间建立联系的规范方式。这种联系通过**[音乐同构](@entry_id:199976) (musical isomorphisms)** 来实现。**降号 (flat)** 同构 $\flat: TM \to T^*M$ 将一个向量 $v$ 映射到一个[余向量](@entry_id:157727) $v^\flat$，其定义为 $v^\flat(w) = g(v, w)$ 对所有向量 $w$ 成立。由于度量 $g$ 的非退化性，这个映射是可逆的。其逆映射称为**升号 (sharp)** 同构 $\sharp: T^*M \to TM$，它通过黎曼度量诱导的[里斯表示定理](@entry_id:140012)将一个[余向量](@entry_id:157727) $\alpha$ 转换回一个向量 $\alpha^\sharp$。这两个同构在建立梯度和散度等概念时至关重要 [@problem_id:2995634]。

### [流形上的微积分](@entry_id:270207)：[联络与曲率](@entry_id:158520)

在欧氏空间中，我们可以通过简单地对向量的各个分量求导来计算向量场的变化率。然而，在弯曲的[流形](@entry_id:153038)上，不同点的切空间是不同的[向量空间](@entry_id:151108)，直接比较和求导失去了意义。为了克服这一困难，我们需要引入一个**联络 (connection)** 的概念，它提供了在相邻[切空间](@entry_id:199137)之间“连接”或识别向量的方法。

对于一个黎曼流形 $(M,g)$，存在一个唯一的联络，称为**[列维-奇维塔联络](@entry_id:161107) (Levi-Civita connection)**，记作 $\nabla$。它满足两个关键属性：无挠（torsion-free）和与度量相容（metric-compatible），即 $X g(Y,Z) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z)$。与度量相容保证了向量在沿曲线平行移动时其长度和向量间的角度保持不变。

联络的核心作用是定义了**协变导数 (covariant derivative)**。给定向量场 $X$ 和 $Y$，协变导数 $\nabla_X Y$ 衡量了 $Y$ 沿 $X$ 方向的无穷小变化。基于此，我们可以定义一个向量场 $V$ 沿着一条光滑曲线 $\gamma(t)$ 的**[平行输运](@entry_id:160671) (parallel transport)**。如果 $V$ 沿着 $\gamma$ 的协变导数为零，即 $\nabla_{\dot{\gamma}(t)}V(t)=0$ 对所有 $t$ 成立，那么我们就说 $V$ 是沿着 $\gamma$ 平行输运的 [@problem_id:2970335]。

在[局部坐标](@entry_id:181200)中，列维-奇维塔联络由一组称为**克里斯托费尔符号 (Christoffel symbols)** 的系数 $\Gamma_{ij}^k$ 完全确定。它们定义了基[向量的[协变导](@entry_id:191566)数](@entry_id:152476)：$\nabla_{\frac{\partial}{\partial x^i}} \frac{\partial}{\partial x^j} = \Gamma_{ij}^k \frac{\partial}{\partial x^k}$。[平行输运](@entry_id:160671)的条件可以转化为一个关于向量分量 $V^k(t)$ 的[一阶常微分方程组](@entry_id:635184) [@problem_id:2970335]：
$$
\frac{dV^k}{dt}(t) + \Gamma_{ij}^k(\gamma(t)) \dot{\gamma}^i(t) V^j(t) = 0
$$
这个方程描述了为了保持“平行”，向量分量必须如何随曲线的移动而变化。

[流形](@entry_id:153038)的弯曲程度可以通过平行输运来探测。将一个向量沿一条闭合回路进行[平行输运](@entry_id:160671)，当回到起点时，它通常不会恢复到初始状态，而是会有一个旋转。所有这些可能的[旋转变换](@entry_id:200017)构成的群被称为[流形](@entry_id:153038)在该点的**和乐群 (holonomy group)** [@problem_id:2997164]。对于列维-奇维塔联络，由于它保持度量，所以[和乐群](@entry_id:191471)是[正交群](@entry_id:152531) $O(n)$ 的一个[子群](@entry_id:146164)。和乐群的非平凡性直接反映了[流形](@entry_id:153038)的**曲率 (curvature)** 不为零。

### [流形](@entry_id:153038)上布朗运动的定义：三种视角

有了黎曼几何的基本工具，我们现在可以从不同角度来定义[流形上的布朗运动](@entry_id:188542)。这三种视角最终被证明是等价的，但它们各自揭示了这一核心概念的不同层面。

#### 生成元方法 (The Generator Approach)

在概率论中，一个[马尔可夫过程](@entry_id:160396)的性质完全由其**[无穷小生成元](@entry_id:270424) (infinitesimal generator)** 决定。生成元是一个[微分算子](@entry_id:140145)，它描述了过程在无穷小时间步长内的期望变化。对于欧氏空间 $\mathbb{R}^n$ 中的标准布朗运动，其生成元是[拉普拉斯算子](@entry_id:146319) $\Delta = \sum_{i=1}^n \frac{\partial^2}{\partial (x^i)^2}$ 的一半。将这个思想推广到黎曼流形上，最自然的方式是使用[流形](@entry_id:153038)内蕴的拉普拉斯算子。

首先，我们需要在[流形](@entry_id:153038)上定义梯度和散度。对于一个光滑函数 $f \in C^\infty(M)$，其**梯度 (gradient)** $\nabla f$ 是一个向量场，由度量对偶性定义：对任意向量场 $Y$，都满足 $g(\nabla f, Y) = df(Y)$，其中 $df$ 是 $f$ 的[外微分](@entry_id:161900) [@problem_id:3028966]。接着，对于一个光滑向量场 $X$，其**散度 (divergence)** $\text{div} X$ 是一个标量函数，由下式定义：$\mathcal{L}_X d\mu_g = (\text{div} X) d\mu_g$，其中 $\mathcal{L}_X$ 是沿 $X$ 的李导数，$d\mu_g$ 是黎曼[体积元](@entry_id:267802) [@problem_id:3028966]。

有了这两个概念，**[拉普拉斯-贝尔特拉米算子](@entry_id:267002) (Laplace-Beltrami operator)** $\Delta_g$ 就可以被简洁地定义为[梯度的散度](@entry_id:270716) [@problem_id:3028966]：
$$
\Delta_g f := \text{div}(\nabla f)
$$
这个算子是欧氏空间拉普拉斯算子在[黎曼流形](@entry_id:261160)上的直接推广。在[局部坐标](@entry_id:181200)下，它可以表示为 [@problem_id:3028966] [@problem_id:2970356]：
$$
\Delta_g f = \frac{1}{\sqrt{\det(g_{kl})}} \partial_i \left( \sqrt{\det(g_{kl})} g^{ij} \partial_j f \right) = g^{ij} \left( \frac{\partial^2 f}{\partial x^i \partial x^j} - \Gamma_{ij}^k \frac{\partial f}{\partial x^k} \right)
$$
其中 $g^{ij}$ 是度量矩阵 $[g_{ij}]$ 的[逆矩阵](@entry_id:140380)。

**定义**：[流形](@entry_id:153038) $(M,g)$ 上的**布朗运动 (Brownian motion)** 是一个[马尔可夫过程](@entry_id:160396)，其[无穷小生成元](@entry_id:270424)为 $\mathcal{L} = \frac{1}{2}\Delta_g$ [@problem_id:2970356] [@problem_id:2970334]。

需要特别注意符号约定。在[几何分析](@entry_id:157700)中，为了让[拉普拉斯算子](@entry_id:146319)具有非负谱，通常定义 $\widetilde{\Delta} = -\text{div}(\nabla f)$。此时[热方程](@entry_id:144435)写作 $\partial_t u = -\widetilde{\Delta} u$。而在概率论中，我们定义的 $\Delta_g = \text{div}(\nabla f)$ 是一个非[正算子](@entry_id:263696)（在 $L^2$ 空间中，$\langle f, \Delta_g f \rangle = - \int_M \|\nabla f\|^2 d\mu_g \le 0$），生成元 $\mathcal{L} = \frac{1}{2}\Delta_g$ 也是非正的，[热方程](@entry_id:144435)则写作 $\partial_t u = \mathcal{L} u$ [@problem_id:3028966]。

#### 随机微分方程方法 (The SDE Approach)

另一种定义布朗运动的方法是通过[随机微分方程](@entry_id:146618)（SDE）。然而，直接在[流形](@entry_id:153038)的[局部坐标](@entry_id:181200)中写下 SDE 会遇到一个棘手的问题：坐标变换下的[不变性](@entry_id:140168)。一个在某个[坐标系](@entry_id:156346)下看似合理的 SDE，在另一个[坐标系](@entry_id:156346)下可能会呈现出完全不同的形式，这与[流形](@entry_id:153038)上过程的[内蕴几何](@entry_id:158788)性质相悖。

这一问题的根源在于两种主要的[随机积分](@entry_id:198356)——**伊藤 (Itô)** 积分和**斯特拉托诺维奇 (Stratonovich)** 积分——在坐标变换下的不同表现。[斯特拉托诺维奇积分](@entry_id:266086)遵循经典的[链式法则](@entry_id:190743)，这使得基于它的 SDE 具有良好的几何变换性质。例如，考虑一个由向量场 $V_i$ 驱动的 [Stratonovich SDE](@entry_id:193247)：
$$
dX_t = \sum_{i=1}^m V_i(X_t) \circ dW_t^i
$$
在光滑坐标变换 $\varphi$ 下，新过程 $Y_t = \varphi(X_t)$ 的 SDE 可以通过链式法则直接得到，其形式保持不变，驱动的向量场变为原向量场的**[前推](@entry_id:158718) (pushforward)** $\varphi_* V_i$ [@problem_id:2995619]。

相反，伊藤积分服从更为复杂的[伊藤公式](@entry_id:159684)，其中包含一个[二阶修正](@entry_id:199233)项。一个“原始的”伊藤 SDE 在[坐标变换](@entry_id:172727)下会产生一个额外的漂移项，该项依赖于[坐标变换](@entry_id:172727)函数的[二阶导数](@entry_id:144508)，因此它不是坐标不变的 [@problem_id:2995619]。

为了用伊藤 SDE 来描述一个几何上不变的过程（如布朗运动），必须在方程中手动加入一个特定的**修正漂移项**，这个漂移项的作用恰好是抵消在[坐标变换](@entry_id:172727)时产生的非张量项。对于生成元为 $\frac{1}{2}\Delta_g$ 的布朗运动，其在[局部坐标](@entry_id:181200)下的伊藤 SDE 形式为 [@problem_id:2970356]：
$$
dX_t^i = \sigma_\alpha^i(X_t) dW_t^\alpha + \frac{1}{2} b^i(X_t) dt
$$
其中 $\sigma_\alpha^i$ 是局部正交[标架场](@entry_id:160577)的分量，满足 $\sum_\alpha \sigma_\alpha^i \sigma_\alpha^j = g^{ij}$。为了使该 SDE 的生成元恰好是 $\frac{1}{2}\Delta_g$，所需的漂移项 $b^i$ 必须是 [@problem_id:2970356]：
$$
b^i(x) = -g^{jk}(x) \Gamma_{jk}^i(x)
$$
这个漂移项在几何上被称为**伊藤-斯特拉托诺维奇修正项**。它精确地编码了[流形](@entry_id:153038)的几何信息（通过克里斯托费尔符号），以确保伊藤 SDE 描述的是一个内蕴的、与坐标选择无关的扩散过程 [@problem_id:2995619]。

#### 随机展开方法 (The Stochastic Development Approach)

最优雅和几何直观的构造方法是**随机展开 (stochastic development)**，也常被比喻为“在[流形](@entry_id:153038)上无滑、无扭地滚动欧氏空间”。这个方法将[欧氏空间](@entry_id:138052) $\mathbb{R}^n$ 中的[标准布朗运动](@entry_id:197332)“展开”到弯曲的黎曼流形 $M$ 上。

这个构造需要借助**正交[标架丛](@entry_id:187852) (orthonormal frame bundle)** $O(M)$。$O(M)$ 的每个元素 $u$ 是一个从标准[欧氏空间](@entry_id:138052) $\mathbb{R}^n$ 到某个[切空间](@entry_id:199137) $T_xM$ 的线性[等距同构](@entry_id:273188)（即一个正交标架）。列维-奇维塔联络在 $O(M)$ 上定义了一个**[水平分布](@entry_id:196663) (horizontal distribution)**，它将 $O(M)$ 的每个切[空间分解](@entry_id:755142)为**水平[子空间](@entry_id:150286) (horizontal subspace)** 和**垂直[子空间](@entry_id:150286) (vertical subspace)**。直观上，水平方向的移动对应于在底[流形](@entry_id:153038) $M$ 上的移动，而垂直方向的移动对应于在[固定点](@entry_id:156394) $x$ 处旋转标架。

在 $O(M)$ 上，我们可以定义一组**典范水平向量场 (canonical horizontal vector fields)** $H_1, \dots, H_n$ [@problem_id:2970354]。每个 $H_i(u)$ 都是一个水平向量，其在底[流形](@entry_id:153038) $M$ 上的投影恰好是标架 $u$ 的第 $i$ 个向量，即 $d\pi_u(H_i(u)) = u(e_i)$，其中 $\{e_i\}$ 是 $\mathbb{R}^n$ 的标准基。

随机展开的构造如下：
1.  从 $\mathbb{R}^n$ 中的一个标准布朗运动 $B_t$ 开始。
2.  将 $B_t$ 的[路径提升](@entry_id:154354)到 $O(M)$ 上的一个**水平路径 (horizontal path)** $U_t$。这个提升过程由一个定义在 $O(M)$ 上的 [Stratonovich SDE](@entry_id:193247) 描述：
    $$
    dU_t = \sum_{i=1}^n H_i(U_t) \circ dB_t^i
    $$
3.  这个水平路径 $U_t$ 在底[流形](@entry_id:153038) $M$ 上的投影 $X_t = \pi(U_t)$ 就是 $(M,g)$ 上的布朗运动。

“无滑、无扭地滚动”这一直观图像精确地对应了这个数学构造 [@problem_id:2970334]：
-   **无滑 (no slip)**: $X_t$ 的[无穷小位移](@entry_id:202209) $dX_t$ 是 $B_t$ 的[无穷小位移](@entry_id:202209) $dB_t$ 通过当前标架 $U_t$ 作用的结果。在 Stratonovich 的意义下，这表示为 $dX_t = U_t \circ dB_t$。
-   **无扭 (no twist)**: 标架 $U_t$ 在沿路径 $X_t$ 移动时自身保持“平行”。这正是[水平提升](@entry_id:160651)的定义，即 $U_t$ 是沿着 $X_t$ 进行[平行输运](@entry_id:160671)的。

这个构造方法天然地产生了一个 [Stratonovich SDE](@entry_id:193247)，因此是坐标无关的。并且，可以证明通过这种方式构造的[随机过程](@entry_id:159502) $X_t$，其生成元恰好是 $\frac{1}{2}\Delta_g$ [@problem_id:2970334]。随机展开方法完美地统一了概率论与微分几何，展示了[流形](@entry_id:153038)布朗运动的深刻几何内涵。

### 性质及其在几何分析中的应用

定义了[流形上的布朗运动](@entry_id:188542)后，我们可以进一步研究其性质，以及它如何作为工具来探测[流形](@entry_id:153038)的几何与拓扑。

#### [鞅问题](@entry_id:204145) (The Martingale Problem)

除了生成元和 SDE，还有一种更抽象但功能强大的方法来刻画扩散过程，即由 Stroock 和 Varadhan 提出的**[鞅问题](@entry_id:204145) (martingale problem)**。它完全通过一个算子 $L$ 的性质来定义一个[随机过程](@entry_id:159502)的概率律，而无需直接构造路径。

对于一个给定的[微分算子](@entry_id:140145) $L$（例如 $\frac{1}{2}\Delta_g$），其定义域为 $C_c^\infty(M)$（[紧支集](@entry_id:276214)[光滑函数](@entry_id:267124)），从点 $x$ 出发的[鞅问题](@entry_id:204145)的解是一个定义在路径空间上的[概率测度](@entry_id:190821) $\mathbb{P}_x$，满足：
1.  过程从 $x$ 开始：$\mathbb{P}_x(X_0=x)=1$。
2.  对任意 $f \in C_c^\infty(M)$，过程 $M_t^f$ 是一个 $\mathbb{P}_x$-鞅，其中 [@problem_id:2970349]：
    $$
    M_t^f = f(X_{t\wedge \zeta}) - f(X_0) - \int_0^{t\wedge \zeta} L f(X_s) \,ds
    $$
这里 $\zeta$ 是过程的**生命期 (lifetime)**，即过程可能在有限时间内“爆炸”或逃逸到无穷远的时间。如果对于任意初值，[鞅问题](@entry_id:204145)的解存在且唯一，则称该[鞅问题](@entry_id:204145)是**适定的 (well-posed)** [@problem_id:2970349]。对于[流形上的布朗运动](@entry_id:188542)，其概率律就是算子 $L = \frac{1}{2}\Delta_g$ 的[鞅问题](@entry_id:204145)的解。

#### 路径性质与二次变差

随机展开方法直观地表明，[流形上的布朗运动](@entry_id:188542)在无穷小尺度上继承了欧氏空间布朗运动的“粗糙性”。它的样本路径几乎[处处连续但处处不可微](@entry_id:276434)，其局部赫尔德指数严格小于 $\frac{1}{2}$ [@problem_id:2970334]。

一个核心的分析工具是计算关于[过程函数](@entry_id:144689)值的**二次变差 (quadratic variation)**。对于[流形上的布朗运动](@entry_id:188542) $X_t$ 和两个光滑函数 $f, g \in C^\infty(M)$，它们复合过程的二次协变差由一个优美的公式给出，该公式被称为**场方算子恒等式 (carré du champ identity)** [@problem_id:2970334]：
$$
d\langle f(X), g(X) \rangle_t = g(\nabla f, \nabla g)(X_t) \,dt
$$
这个公式是[流形](@entry_id:153038)上[伊藤公式](@entry_id:159684)的核心部分。特别地，当 $f=g$ 时，它给出了 $f(X_t)$ 的二次变差，它衡量了 $f$ 沿布朗路径累积的平方增量：$d\langle f(X) \rangle_t = \|\nabla f\|_g^2(X_t) \,dt$ [@problem_id:3028966]。这个结果表明，只要函数 $f$ 不是常数（即其梯度不为零），$f(X_t)$ 就会有非零的二次变差，这再次印证了布朗路径的粗糙性。

#### 长时间行为：[随机完备性](@entry_id:182502)

一个自然的问题是：[流形](@entry_id:153038)上的布朗粒子是否会永远存活，或者它是否可能在有限时间内“逃逸”到无穷远？这引出了**[随机完备性](@entry_id:182502) (stochastic completeness)** 的概念。

一个黎曼流形 $(M,g)$ 被称为是随机完备的，如果其上的布朗运动不会爆炸，即对于任意起点 $x \in M$，生命期 $\zeta$ 是无穷大的概率为1：$\mathbb{P}_x(\zeta = \infty) = 1$。这等价于说，由热核 $p_t(x,y)$ 定义的转移概率在任何时刻 $t>0$ 都是守恒的，即 $\int_M p_t(x,y) d\mu_g(y) = 1$ [@problem_id:2970350]。

[随机完备性](@entry_id:182502)是一个深刻的几何性质，它与[流形](@entry_id:153038)的曲率和[体积增长](@entry_id:274676)率密切相关。
-   任何紧致无边的黎曼流形都是随机完备的，因为布朗粒子无处可逃。
-   **[测地完备性](@entry_id:160280) (geodesic completeness)**（即任何[测地线](@entry_id:269969)都可以无限延伸）与[随机完备性](@entry_id:182502)并不等价。存在测地完备但随机不完备的[流形](@entry_id:153038)（通常具有极快的[体积增长](@entry_id:274676)），也存在随机完备但[测地不完备](@entry_id:266320)的[流形](@entry_id:153038)（如 $\mathbb{R}^n \setminus \{0\}$ for $n \ge 2$） [@problem_id:2970350]。
-   一个里程碑式的定理（[丘成桐定理](@entry_id:190158)）指出：任何测地完备且具有非负**[里奇曲率](@entry_id:162038) (Ricci curvature)** 的[黎曼流形](@entry_id:261160)都是随机完备的 [@problem_id:2970350]。这揭示了曲率对布朗粒子长时间行为的控制作用：非负的[里奇曲率](@entry_id:162038)在某种意义上会阻止粒子过快地逃逸。

#### [随机和](@entry_id:266003)乐

最后，我们回到[和乐](@entry_id:137051)与曲率的概念。正如确定性的平行输运可以探测曲率，随机的平行输运也可以。考虑沿一条布朗路径 $X_t$ 进行[平行输运](@entry_id:160671)。如果我们考察一条始于 $p$ 点的、在微小时间 $\varepsilon$ 内形成的随机回路，那么沿该回路的平行输运将产生一个随机的和乐元素 $H_\varepsilon \in O(n)$。

一个深刻的结果，即**随机和乐定理 (Stochastic Holonomy Theorem)**，指出当 $\varepsilon \to 0$ 时，这个[随机和](@entry_id:266003)乐元素 $H_\varepsilon$ 的期望行为和涨落由[流形](@entry_id:153038)的[曲率张量](@entry_id:181383)决定。更具体地说，$H_\varepsilon$ 与单位阵的偏差，其主导项由曲率二形式作用在驱动布朗运动的**随机[列维面积](@entry_id:634943) (stochastic Lévy area)** 上给出 [@problem_id:2997164]。这表明，布朗运动不仅能“感受”到[流形](@entry_id:153038)的曲率（表现为伊藤SDE中的漂移项），还能通过其路径的[平行输运](@entry_id:160671)来“测量”曲率，从而为研究[流形](@entry_id:153038)的几何结构提供了一种强大的[随机分析](@entry_id:188809)工具。