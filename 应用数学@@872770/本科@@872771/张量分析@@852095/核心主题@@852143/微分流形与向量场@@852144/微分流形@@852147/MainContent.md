## 引言
[微分](@entry_id:158718)[流形](@entry_id:153038)是现代数学和理论物理的基石，它将我们对[欧几里得空间](@entry_id:138052)的直观理解推广到了更广泛的弯曲空间。然而，当空间不再平直时，我们如何定义导数、积分和几何结构呢？传统微积分的方法在此失效，这构成了理解复杂系统的核心知识鸿沟。本文旨在系统地填补这一鸿沟，为读者提供一个关于[微分](@entry_id:158718)[流形](@entry_id:153038)的全面介绍。在接下来的章节中，你将首先通过“原理与机制”部分，从最基本的[坐标卡](@entry_id:262338)和图册出发，逐步构建起切空间、矢量场和[纤维丛](@entry_id:159565)等核心数学工具。随后，在“应用与跨学科联系”部分，我们将展示这些抽象概念如何在物理学、几何学、信息论乃至工程控制等领域大放异彩。最后，通过“动手实践”部分，你将有机会运用所学知识解决具体问题，从而巩固你的理解。

## 原理与机制

继前一章对[微分](@entry_id:158718)[流形](@entry_id:153038)的直观介绍之后，本章将深入探讨其核心的原理与机制。我们将从构建[流形](@entry_id:153038)的基本单元——坐标卡和图册——开始，系统地建立[切空间](@entry_id:199137)、矢量场、微分形式等关键概念。通过理解这些构造，我们将揭示如何在弯曲的空间上进行微积分，并最终将这些局部结构“捆绑”成一个统一的整体，即[切丛](@entry_id:161294)。本章旨在为读者提供一个坚实的基础，以便后续章节能够应用这些强大的工具来解决几何学与物理学中的问题。

### [流形](@entry_id:153038)：从局部到整体的观点

[微分](@entry_id:158718)[流形](@entry_id:153038)的核心思想是，一个在宏观上可能非常复杂的弯曲空间，在微观局部上却与我们熟悉的欧几里得空间 $\mathbb{R}^n$ 别无二致。这种“局部欧氏化”的特性是通过 **[坐标卡](@entry_id:262338) (chart)** 来精确描述的。一个 $n$ 维[流形](@entry_id:153038) $M$ 上的坐标卡是一个二元组 $(U, \varphi)$，其中 $U$ 是 $M$ 上的一个开集，而 $\varphi: U \to V$ 是一个从 $U$ 到 $\mathbb{R}^n$ 中某个开集 $V$ 的[同胚](@entry_id:146933)映射（即一个保持拓扑结构的双向连续映射）。映射 $\varphi$ 为 $U$ 中的每一点 $p$ 赋予了一组[局部坐标](@entry_id:181200) $(x^1(p), \dots, x^n(p)) \in \mathbb{R}^n$。

然而，单个坐标卡通常不足以覆盖整个[流形](@entry_id:153038)。例如，我们无法用一张无[奇异点](@entry_id:199525)的地图来完整地绘制整个地球表面。因此，我们需要一个 **图册 (atlas)**，它是由一系列坐标卡 $\{(U_\alpha, \varphi_\alpha)\}$ 组成的集合，其定义域 $U_\alpha$ 的并集能够完全覆盖[流形](@entry_id:153038) $M$。

为了在[流形](@entry_id:153038)上进行微积分，仅仅拥有一个图册是不够的。我们必须确保当两个坐标卡 $(U_\alpha, \varphi_\alpha)$ 和 $(U_\beta, \varphi_\beta)$ 的定义域重叠时，从一个[局部坐标系](@entry_id:751394)到另一个的转换是平滑的。具体来说，在重叠区域 $U_\alpha \cap U_\beta$ 上，**转换映射 (transition map)** $\varphi_\beta \circ \varphi_\alpha^{-1}$ 必须是一个从 $\varphi_\alpha(U_\alpha \cap U_\beta) \subset \mathbb{R}^n$ 到 $\varphi_\beta(U_\alpha \cap U_\beta) \subset \mathbb{R}^n$ 的[光滑映射](@entry_id:203730)（即无限可微）。一个配备了这种[光滑转换映射](@entry_id:192056)的图册被称为 **[微分](@entry_id:158718)结构 (differentiable structure)**。

一个经典的例子是环面 $T^2$ [@problem_id:1506488]。我们可以将环面视为两个圆的乘积 $S^1 \times S^1$。由于环面是紧致的（即闭合且有界），它不能被单个坐标卡所覆盖，因为 $\mathbb{R}^2$ 中任何非空开集都不是紧致的。因此，要为环面构造一个图册，我们至少需要两个[坐标卡](@entry_id:262338)。一种构造方法是，从环面上移除一条经线和一条纬线，剩下的部分可以被同胚地映射到 $\mathbb{R}^2$ 的一个开集。通过巧妙地选择移除的曲线，例如，在环面上定义两条不相交的[闭合曲线](@entry_id:264519) $C_1$ 和 $C_2$，然后考虑两个开集 $U_1 = T^2 \setminus C_1$ 和 $U_2 = T^2 \setminus C_2$，这两个[开集的并集](@entry_id:152269)覆盖了整个环面，并且每一个都可以被映射到 $\mathbb{R}^2$ 的一个开集。这证明了为环面构造一个有效的图册，最少需要两个[坐标卡](@entry_id:262338)。

[流形](@entry_id:153038)的[子集](@entry_id:261956)也可以是[流形](@entry_id:153038)。任何 $n$ 维[流形](@entry_id:153038) $M$ 的一个开[子集](@entry_id:261956) $U \subset M$ 本身就是一个 $n$ 维[流形](@entry_id:153038)。它的[微分](@entry_id:158718)结构可以自然地由 $M$ 的图册继承而来：只需将 $M$ 的每个坐标卡 $(U_\alpha, \varphi_\alpha)$ 的定义域限制在 $U$ 内，形成新的[坐标卡](@entry_id:262338) $(U_\alpha \cap U, \varphi_\alpha|_{U_\alpha \cap U})$ 即可 [@problem_id:1506470]。例如，球面 $S^2 = \{(x,y,z) \in \mathbb{R}^3 \mid x^2+y^2+z^2=1\}$ 是一个[二维流形](@entry_id:188198)，其北半球 $U = \{(x,y,z) \in S^2 \mid z>0\}$ 是 $S^2$ 的一个开[子集](@entry_id:261956)，因此北半球本身也是一个[二维流形](@entry_id:188198)。

此外，[流形](@entry_id:153038)的概念可以推广到包含边界的情况。一个 **[带边流形](@entry_id:159788) (manifold with boundary)** 是一个拓扑空间，其中每个点都拥有一个邻域，该邻域[同胚](@entry_id:146933)于欧几里得半空间 $H^n = \{ (x_1, \dots, x_n) \in \mathbb{R}^n \mid x_n \ge 0 \}$ 中的一个开集。那些被映射到 $H^n$ 边界 $\{x_n = 0\}$ 上的点构成了[流形](@entry_id:153038)的 **边界 (boundary)** $\partial M$。一个典型的例子是闭合单位球 $D^n = \{x \in \mathbb{R}^n : \|x\| \le 1\}$ [@problem_id:1506509]。对于球内部的点（$\|x\|  1$），其邻域[同胚](@entry_id:146933)于 $\mathbb{R}^n$ 中的开集。对于球面上的点（$\|x\| = 1$），可以证明其邻域同胚于 $H^n$ 中的开集。因此，$D^n$ 是一个光滑[带边流形](@entry_id:159788)，其边界 $\partial D^n$ 正是 $(n-1)$ 维球面 $S^{n-1} = \{x \in \mathbb{R}^n : \|x\| = 1\}$。

### 切空间：[流形](@entry_id:153038)的线性近似

一旦我们有了[微分](@entry_id:158718)结构，就可以在[流形](@entry_id:153038)的每一点上定义一个[线性空间](@entry_id:151108)，称为 **[切空间](@entry_id:199137) (tangent space)**，记作 $T_pM$。切空间可以被认为是[流形](@entry_id:153038)在点 $p$ 处的一阶线性近似，它包含了所有可能的“速度”或“方向”。

#### 切矢量的几何定义

最直观的理解是将切矢量视为穿过点 $p$ 的光滑曲线的[速度矢量](@entry_id:269648)。设 $\gamma: (-\epsilon, \epsilon) \to M$ 是一条光滑曲线，且 $\gamma(0) = p$。这条曲线在 $t=0$ 处的速度矢量就是 $T_pM$ 中的一个元素。
例如，考虑一个粒子沿双曲线 $x^2 - y^2 = a^2$ 运动，其轨迹由 $\gamma(t) = (a \cosh(\omega t), a \sinh(\omega t))$ 描述 [@problem_id:1506528]。其[速度矢量](@entry_id:269648)是 $V(t) = \gamma'(t) = (\frac{dx}{dt}, \frac{dy}{dt}) = (a\omega\sinh(\omega t), a\omega\cosh(\omega t))$。在 $t=0$ 时，粒子位于点 $p=(a,0)$，其速度矢量为 $V(0) = (0, a\omega)$。这个矢量就是曲线 $\gamma$ 在点 $p$ 处的一个切矢量。

在给定的[局部坐标系](@entry_id:751394) $(x^1, \dots, x^n)$ 中，曲线 $\gamma(t)$ 可以表示为 $(x^1(t), \dots, x^n(t))$。其[速度矢量](@entry_id:269648)在点 $p=\gamma(0)$ 的分量就是 $(\frac{dx^1}{dt}|_{t=0}, \dots, \frac{dx^n}{dt}|_{t=0})$。例如，考虑球面 $S^2$ 上的一个点 $p = (\frac{1}{\sqrt{3}}, \frac{1}{\sqrt{3}}, \frac{1}{\sqrt{3}})$ 和一条穿过该点的曲线 $\gamma(\tau)$ [@problem_id:1506470]。如果我们使用从南极出发的球极投影[坐标系](@entry_id:156346) $(s,t)$，其中 $s = \frac{x}{1+z}$，$t=\frac{y}{1+z}$，那么曲线的[速度矢量](@entry_id:269648) $X_p = \gamma'(0)$ 在这个[坐标系](@entry_id:156346)下的分量 $(X_s, X_t)$ 就是 $s$ 和 $t$ 沿曲线对参数 $\tau$ 的导数在 $\tau=0$ 处的值，即 $X_s = \frac{d}{d\tau}s(\gamma(\tau))|_{\tau=0}$ 和 $X_t = \frac{d}{d\tau}t(\gamma(\tau))|_{\tau=0}$。

#### 切矢量的代数定义

一个更深刻且在代数上更灵活的定义是将切矢量视为作用在[光滑函数](@entry_id:267124)上的 **导子 (derivation)**。一个在点 $p$ 的切矢量 $v_p \in T_pM$ 是一个线性映射 $v_p: C^\infty(M) \to \mathbb{R}$，它作用于[流形](@entry_id:153038) $M$ 上的[光滑函数](@entry_id:267124) $f$，并满足[莱布尼茨法则](@entry_id:157949)（Leibniz rule）：$v_p(fg) = f(p)v_p(g) + g(p)v_p(f)$。本质上， $v_p(f)$ 就是函数 $f$ 在点 $p$ 沿 $v_p$ 方向的方向导数。

在局部坐标系 $(x^1, \dots, x^n)$ 中，偏导数算子 $\{\frac{\partial}{\partial x^1}|_p, \dots, \frac{\partial}{\partial x^n}|_p\}$ 构成了[切空间](@entry_id:199137) $T_pM$ 的一组基。任何切矢量 $v_p$ 都可以唯一地表示为这些[基矢](@entry_id:199546)量的线性组合：
$v_p = \sum_{i=1}^n v^i \frac{\partial}{\partial x^i}\bigg|_p$
其中 $v^i$ 是 $v_p$ 在这个基下的分量。
这个定义的美妙之处在于它将几何对象（切矢量）与代数对象（导子）联系起来。例如，考虑 $\mathbb{R}^2$ 上的一个切矢量 $v_p = 4 \frac{\partial}{\partial x}|_p - x_0 y_0 \frac{\partial}{\partial y}|_p$ 在点 $p=(x_0, y_0)$ 的作用 [@problem_id:1506477]。它作用在函数 $f(x,y) = \exp(x^2 y)$ 上的结果是：
$v_p(f) = 4 \left(\frac{\partial f}{\partial x}\right)\bigg|_p - x_0 y_0 \left(\frac{\partial f}{\partial y}\right)\bigg|_p$
通过计算偏导数并代入点 $p$ 的坐标，我们可以得到一个具体的数值结果，它代表了函数 $f$ 在该点沿 $v_p$ 方向的变化率。

### [光滑映射](@entry_id:203730)及其导数

[流形理论](@entry_id:263722)的威力体现在研究它们之间的 **[光滑映射](@entry_id:203730) (smooth map)**。一个从[流形](@entry_id:153038) $M$ 到[流形](@entry_id:153038) $N$ 的映射 $F: M \to N$ 被称为光滑的，如果当它在 $M$ 和 $N$ 的[局部坐标](@entry_id:181200)中表示时，它是一个光滑函数。

对于每个[光滑映射](@entry_id:203730) $F$，我们可以在每一点 $p \in M$ 定义一个线性映射，称为 **推前 (pushforward)** 或 **[微分](@entry_id:158718) (differential)**，记作 $F_{*p}$ 或 $dF_p$。这个映射将 $M$ 在点 $p$ 的[切空间](@entry_id:199137) $T_pM$ 线性地映射到 $N$ 在点 $F(p)$ 的切空间 $T_{F(p)}N$：
$F_{*p}: T_pM \to T_{F(p)}N$
推前 $F_{*p}$ 描述了映射 $F$ 如何变换切矢量。如果一个切矢量 $v_p \in T_pM$ 是曲线 $\gamma(t)$ 在 $t=0$ 的速度矢量，那么 $F_{*p}(v_p)$ 就是复合曲线 $F(\gamma(t))$ 在 $t=0$ 的[速度矢量](@entry_id:269648)。

在[局部坐标](@entry_id:181200)中，推前由雅可比矩阵表示。假设 $p$ 的[局部坐标](@entry_id:181200)为 $(u^1, \dots, u^m)$，$F(p)$ 的[局部坐标](@entry_id:181200)为 $(x^1, \dots, x^n)$。如果 $v_p = \sum_j v^j \frac{\partial}{\partial u^j}|_p$，那么它的推前 $w_{F(p)} = F_{*p}(v_p) = \sum_i w^i \frac{\partial}{\partial x^i}|_{F(p)}$ 的分量由下式给出：
$w^i = \sum_{j=1}^m v^j \frac{\partial x^i}{\partial u^j}\bigg|_p$
这正是多元微积分中的[链式法则](@entry_id:190743)。

一个非常重要的例子是嵌入到高维[欧氏空间](@entry_id:138052)中的[流形](@entry_id:153038) [@problem_id:1506523]。考虑一个由光滑函数 $f: \mathbb{R}^2 \to \mathbb{R}$ 的图像定义的[曲面](@entry_id:267450) $M \subset \mathbb{R}^3$。我们可以用一个映射 $\phi: \mathbb{R}^2 \to \mathbb{R}^3$ 来参数化这个[曲面](@entry_id:267450)，$\phi(u^1, u^2) = (u^1, u^2, f(u^1, u^2))$。这个映射 $\phi$ 将[参数空间](@entry_id:178581) $\mathbb{R}^2$ 的切矢量推前为[嵌入空间](@entry_id:637157) $\mathbb{R}^3$ 中[曲面](@entry_id:267450) $M$ 的切矢量。例如，对于 $\mathbb{R}^2$ 中的矢量场 $X = u^2 \frac{\partial}{\partial u^1} - u^1 \frac{\partial}{\partial u^2}$，其在点 $p$ 的值 $X_p$ 是一个 $\mathbb{R}^2$ 中的切矢量。推前 $\phi_*(X_p)$ 是 $M$ 在 $\phi(p)$ 点的一个切矢量，它生活在 $\mathbb{R}^3$ 中。其分量可以通过计算[雅可比矩阵](@entry_id:264467)与 $X_p$ 分量的乘积得到。具体而言，$\phi$ 的雅可比矩阵的列是 $\frac{\partial \phi}{\partial u^1} = (1, 0, \frac{\partial f}{\partial u^1})$ 和 $\frac{\partial \phi}{\partial u^2} = (0, 1, \frac{\partial f}{\partial u^2})$。因此，如果 $X_p = a \frac{\partial}{\partial u^1} + b \frac{\partial}{\partial u^2}$，则 $\phi_*(X_p)$ 在 $\mathbb{R}^3$ 的标准基下的分量为 $(a, b, a\frac{\partial f}{\partial u^1} + b\frac{\partial f}{\partial u^2})$。

### 矢量场与[李括号](@entry_id:636461)

**矢量场 (vector field)** $X$ 是在[流形](@entry_id:153038) $M$ 的每一点 $p$ 上平滑地指定一个切矢量 $X_p \in T_pM$ 的对象。在[局部坐标](@entry_id:181200)中，矢量场可以写成 $X = \sum_i X^i(x) \frac{\partial}{\partial x^i}$，其中系数 $X^i(x)$ 是光滑函数。矢量场可以被看作是定义在[流形](@entry_id:153038)上的[一阶常微分方程组](@entry_id:635184)。

给定一个矢量场 $X$，它的 **[积分曲线](@entry_id:161858) (integral curve)** 是处处与该矢量场相切的曲线 $\gamma(t)$，即 $\gamma'(t) = X(\gamma(t))$。通过[流形](@entry_id:153038)上每一点的[积分曲线](@entry_id:161858)族构成了矢量场的 **流 (flow)**，记作 $\phi_t^X$。流是一个单参数的微分同胚群，它描述了[流形](@entry_id:153038)上的点如何沿着矢量场 $X$ "流动" $t$ 时间。

当存在两个矢量场 $X$ 和 $Y$ 时，一个自然的问题是：沿着 $X$ 流动 $t$ 时间再沿着 $Y$ 流动 $s$ 时间，与先沿着 $Y$ 流动 $s$ 时间再沿着 $X$ 流动 $t$ 时间，结果是否相同？通常情况下，答案是否定的，即 $\phi_t^X \circ \psi_s^Y \neq \psi_s^Y \circ \phi_t^X$。

**李括号 (Lie bracket)** $[X, Y]$ 正是衡量这两个流的非对易性的工具。从代数上看，李括号被定义为两个矢量场作用在[光滑函数](@entry_id:267124)上时的交换子：$[X, Y](f) = X(Y(f)) - Y(X(f))$。可以证明，$[X, Y]$ 本身也是一个矢量场。

李括号的深刻几何意义在于它与流的[交换子](@entry_id:158878)的关系。考虑从一点 $p_0$ 出发，依次经过 $\phi_{\sqrt{\tau}}^X$, $\psi_{\sqrt{\tau}}^Y$, $\phi_{-\sqrt{\tau}}^X$, $\psi_{-\sqrt{\tau}}^Y$ 的变换，最终回到 $p_0$ 附近的一点 $\gamma(\tau)$ [@problem_id:1506507]。当 $\tau \to 0$ 时，这个闭合回路的“缺口”有多大？可以证明，点 $\gamma(\tau)$ 的位置与初始点 $p_0$ 的偏离在 $\tau$ 的[一阶近似](@entry_id:147559)下由李括号 $[X,Y]$ 在 $p_0$ 的值决定：
$\gamma(\tau) = p_0 + \tau [X,Y]|_{p_0} + O(\tau^{3/2})$
因此，$\gamma(\tau)$ 在 $\tau=0$ 处的“速度”矢量恰好就是[李括号](@entry_id:636461)矢量 $[X, Y]|_{p_0}$。
例如，对于 $\mathbb{R}^3$ 上的两个矢量场 $X = \frac{\partial}{\partial x} - y \frac{\partial}{\partial z}$ 和 $Y = \frac{\partial}{\partial y} + x \frac{\partial}{\partial z}$，我们可以分别计算它们的流 $\phi_t$ 和 $\psi_s$。通过显式地计算复合映射 $(\psi_{-\sqrt{\tau}} \circ \phi_{-\sqrt{\tau}} \circ \psi_{\sqrt{\tau}} \circ \phi_{\sqrt{\tau}})(p_0)$，我们会发现结果点的 $x$ 和 $y$ 坐标与 $p_0$ 相同，而 $z$ 坐标增加了 $2\tau$。因此，该路径在 $\tau=0$ 处的切矢量是 $(0, 0, 2)$。另一方面，直接计算[李括号](@entry_id:636461)得到 $[X,Y] = 2\frac{\partial}{\partial z}$。这完美地印证了李括号的几何意义。

### 对偶概念：余切矢量与[微分形式](@entry_id:146747)

对于每个切空间 $T_pM$，都存在一个对偶矢量空间，称为 **[余切空间](@entry_id:270516) (cotangent space)**，记为 $T_p^*M$。它的元素被称为 **余切矢量 (covector)** 或 **1-形式 (1-form)**。每个余切矢量 $\omega_p \in T_p^*M$ 是一个作用于切矢量的线性实值函数，即 $\omega_p: T_pM \to \mathbb{R}$。

如果 $\{ \frac{\partial}{\partial x^i}|_p \}$ 是 $T_pM$ 的一组基，那么 $T_p^*M$ 也有一组相应的 **对偶基 (dual basis)**，记作 $\{ dx^i|_p \}$。它们的定义是：
$dx^i\left(\frac{\partial}{\partial x^j}\right) = \delta^i_j$
其中 $\delta^i_j$ 是克罗内克 delta 符号。任何一个 1-形式 $\omega_p$ 都可以表示为 $\omega_p = \sum_i \omega_i dx^i|_p$，其中系数 $\omega_i = \omega_p(\frac{\partial}{\partial x^i}|_p)$。

基底 1-形式在[坐标变换](@entry_id:172727)下的行为与基底矢量不同。考虑从[笛卡尔坐标](@entry_id:167698) $(x,y)$ 到极坐标 $(r, \theta)$ 的变换。我们有 $x = r\cos\theta$ 和 $y = r\sin\theta$。我们可以通过全[微分法则](@entry_id:169252)找到新旧基底 1-形式之间的关系。例如，为了将 $d\theta$ 用 $dx$ 和 $dy$ 表示 [@problem_id:1506466]，我们先写出 $dx$ 和 $dy$：
$dx = \cos\theta dr - r\sin\theta d\theta$
$dy = \sin\theta dr + r\cos\theta d\theta$
这是一个关于 $dr$ 和 $d\theta$ 的线性方程组。通过求解这个[方程组](@entry_id:193238)（或巧妙地组合方程，例如计算 $-y\,dx + x\,dy$），我们可以消去 $dr$，得到：
$d\theta = \frac{-y}{x^2+y^2} dx + \frac{x}{x^2+y^2} dy$
这显示了 [1-形式](@entry_id:270392)在坐标变换下的转换法则。

与将切矢量从一个[流形](@entry_id:153038)“推向”另一个[流形](@entry_id:153038)的推前相反，我们可以将 1-形式从目标[流形](@entry_id:153038)“[拉回](@entry_id:160816)”到源[流形](@entry_id:153038)。给定一个[光滑映射](@entry_id:203730) $F: M \to N$，**[拉回](@entry_id:160816) (pullback)** 映射 $F^*$ 将 $N$ 上的 1-形式 $\omega$ 变换为 $M$ 上的 [1-形式](@entry_id:270392) $F^*\omega$。其定义在任意点 $p \in M$ 和任意切矢量 $v_p \in T_pM$ 上给出：
$(F^*\omega)_p(v_p) = \omega_{F(p)}(F_{*p}(v_p))$
这个定义确保了所有运算的协调性。

在[局部坐标](@entry_id:181200)中，计算[拉回](@entry_id:160816)是一个直接的代换过程。如果 $N$ 上有 [1-形式](@entry_id:270392) $\omega = \sum_i g_i(x) dx^i$，并且映射 $F$ 由函数 $x^i = x^i(u)$ 给出，那么[拉回](@entry_id:160816) $F^*\omega$ 就是将每个 $g_i$ 替换为 $g_i(x(u))$，并将每个 $dx^i$ 替换为它的[全微分](@entry_id:171747) $dx^i = \sum_j \frac{\partial x^i}{\partial u^j} du^j$。
例如，考虑从 $M=\mathbb{R}^2$ 到 $N=\mathbb{R}^3$ 的映射 $F(u,v) = (u\cos v, u\sin v, v)$，以及 $N$ 上的 1-形式 $\omega = z\,dx - x\,dy + y\,dz$ [@problem_id:1506475]。要计算[拉回](@entry_id:160816) $F^*\omega$，我们只需将 $x, y, z$ 和 $dx, dy, dz$ 都用 $u, v$ 和 $du, dv$ 表示，然后代入 $\omega$ 的表达式即可。这个过程虽然可能涉及繁琐的代数运算，但原理上是清晰直接的。

### 纤维丛：将碎片组装起来

我们已经看到，[流形](@entry_id:153038) $M$ 的每一点 $p$ 都附着一个切空间 $T_pM$。我们可以将所有这些切空间“粘合”在一起，形成一个更大的空间，称为 **[切丛](@entry_id:161294) (tangent bundle)**，记为 $TM$。它定义为所有[切空间](@entry_id:199137)的并集：
$TM = \bigsqcup_{p \in M} T_pM = \{ (p, v) \mid p \in M, v \in T_pM \}$

[切丛](@entry_id:161294)本身不仅仅是一个集合，它也具有一个 $2n$ 维的[光滑流形](@entry_id:160799)结构。如果 $(U, \varphi)$ 是 $M$ 上的一个坐标卡，坐标为 $(x^1, \dots, x^n)$，那么它可以在 $TM$ 上诱导一个坐标卡。对于 $TM$ 中的任意一点 $(p, w)$，其中 $p \in U$，我们可以将矢量 $w$ 在基底下展开为 $w = \sum_i w^i \frac{\partial}{\partial x^i}|_p$。这样，点 $(p,w)$ 就可以由 $2n$ 个数 $(x^1(p), \dots, x^n(p), w^1, \dots, w^n)$ 来唯一确定。这组数构成了 $TM$ 在 $p$ 点附近的[局部坐标](@entry_id:181200)。

为了证明 $TM$ 确实是一个[光滑流形](@entry_id:160799)，我们需要验证不同坐标卡之间的转换映射是光滑的。这需要我们考察当底[流形](@entry_id:153038) $M$ 的坐标发生变化时，切矢量的分量是如何变化的。这正是[雅可比矩阵](@entry_id:264467)所描述的。
考虑球面 $S^2$ 的切丛 $TS^2$ [@problem_id:1506489]。我们可以用两个球极投影[坐标卡](@entry_id:262338)来覆盖 $S^2$：一个是从北极 $N$ 投影的 $(u,v)$ [坐标系](@entry_id:156346)，另一个是从南极 $S$ 投影的 $(\tilde{u}, \tilde{v})$ [坐标系](@entry_id:156346)。这两个[坐标系](@entry_id:156346)分别在 $TS^2$ 上诱导出[坐标系](@entry_id:156346) $(u, v, w^u, w^v)$ 和 $(\tilde{u}, \tilde{v}, \tilde{w}^{\tilde{u}}, \tilde{w}^{\tilde{v}})$。
在两个[坐标卡](@entry_id:262338)的重叠区域，底空间坐标的转换关系为 $\tilde{u} = \frac{u}{u^2+v^2}$ 和 $\tilde{v} = \frac{v}{u^2+v^2}$。根据[链式法则](@entry_id:190743)，切矢量的分量 $(w^u, w^v)$ 和 $(\tilde{w}^{\tilde{u}}, \tilde{w}^{\tilde{v}})$ 通过底空间[坐标变换](@entry_id:172727)的[雅可比矩阵](@entry_id:264467)相关联：
$\begin{pmatrix} \tilde{w}^{\tilde{u}} \\ \tilde{w}^{\tilde{v}} \end{pmatrix} = \begin{pmatrix} \frac{\partial \tilde{u}}{\partial u}  \frac{\partial \tilde{u}}{\partial v} \\ \frac{\partial \tilde{v}}{\partial u}  \frac{\partial \tilde{v}}{\partial v} \end{pmatrix} \begin{pmatrix} w^{u} \\ w^{v} \end{pmatrix}$
由于底空间的转换映射是光滑的，其[雅可比矩阵](@entry_id:264467)的元素也是关于 $(u,v)$ 的[光滑函数](@entry_id:267124)。因此，从 $(u, v, w^u, w^v)$ 到 $(\tilde{u}, \tilde{v}, \tilde{w}^{\tilde{u}}, \tilde{w}^{\tilde{v}})$ 的完整转换映射也是光滑的。这证实了 $TS^2$ 确实是一个 $4$ 维的光滑流形。这个例子清晰地展示了[流形](@entry_id:153038)的[微分](@entry_id:158718)结构如何自然地诱导出其切丛上的[微分](@entry_id:158718)结构，这是微分几何中一个具有普遍性的深刻原理。