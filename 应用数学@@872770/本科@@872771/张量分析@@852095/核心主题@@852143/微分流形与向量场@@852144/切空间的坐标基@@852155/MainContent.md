## 引言
在从熟悉的平直欧几里得空间过渡到更广义的弯曲[流形](@entry_id:153038)（如[曲面](@entry_id:267450)或广义相对论中的时空）时，我们面临一个根本性挑战：如何一致地描述矢量、变化率以及几何本身？传统的笛卡尔[基矢](@entry_id:199546)在整个空间中恒定不变，但在[曲线坐标系](@entry_id:172561)或弯曲空间中，这一便利不复存在。为了解决这个问题，数学家和物理学家发展了 **[切空间](@entry_id:199137) (tangent space)** 的概念，以及在其中定义局部[参考系](@entry_id:169232)的系统方法——**[坐标基](@entry_id:270149) (coordinate basis)**。[坐标基](@entry_id:270149)为我们提供了一个随点而变的“标尺”，使我们能够在任何局部区域内进行精确的几何和物理计算。

本文旨在系统地阐明[切空间](@entry_id:199137)[坐标基](@entry_id:270149)这一核心概念。我们将穿越三个章节，构建一个从基本原理到实际应用的完整理解框架。首先，在 **“原理与机制”** 一章中，我们将深入探讨[坐标基](@entry_id:270149)的两种等价定义——几何定义和代数定义，并揭示其关键性质，如可交换性，以及它如何催生[出度](@entry_id:263181)量张量。接着，在 **“应用与跨学科联系”** 一章中，我们将展示这一理论工具的强大威力，看它如何被应用于描述弯曲几何，并在从经典力学到广义相对论的广阔物理学领域中扮演核心角色。最后，通过 **“动手实践”** 部分，你将有机会通过解决具体问题来巩固所学知识。现在，让我们从[坐标基](@entry_id:270149)最基本的原理与机制开始。

## 原理与机制

在深入研究[张量分析](@entry_id:161423)的广阔领域之前，我们必须首先建立一个坚实的基础，以理解如何在弯曲空间或使用[曲线坐标系](@entry_id:172561)时描述矢量等几何对象。这个基础的核心是 **切空间 (tangent space)** 的概念，以及在该空间中定义一个可靠的基底——即 **[坐标基](@entry_id:270149) (coordinate basis)** 的方法。本章将系统地阐述[坐标基](@entry_id:270149)的定义、性质及其在描述几何与物理中的核心作用。

### [切向量](@entry_id:265494)的几何直观：[坐标基](@entry_id:270149)矢

想象一个平坦的二维欧几里得平面。我们可以用熟悉的[笛卡尔坐标系](@entry_id:169789) $(x, y)$ 来标记其中的每一个点。任何一点的位置都可以由位置矢量 $\mathbf{r} = x \hat{\mathbf{i}} + y \hat{\mathbf{j}}$ 描述，其中 $\hat{\mathbf{i}}$ 和 $\hat{\mathbf{j}}$ 是沿着 $x$ 轴和 $y$ 轴的[标准正交基](@entry_id:147779)矢。

现在，假设我们引入一套新的[坐标系](@entry_id:156346)，例如极坐标 $(r, \theta)$ 或其他更复杂的[曲线坐标系](@entry_id:172561) $(u^1, u^2)$。这意味着原来的笛卡尔坐标 $(x, y)$ 可以表示为新坐标 $(u^1, u^2)$ 的函数：$x = x(u^1, u^2)$，$y = y(u^1, u^2)$。因此，位置矢量也成为了新坐标的函数：$\mathbf{r}(u^1, u^2)$。

在新的[坐标系](@entry_id:156346)中，我们可以设想“坐标线”组成的网格。一条 $u^1$-坐标线是指在保持 $u^2$ 恒定的情况下，仅改变 $u^1$ 所形成的曲线。同样地，一条 $u^2$-坐标线是保持 $u^1$ 恒定、仅改变 $u^2$ 而得到的曲线。在任意一点 $P$，这两条穿过该点的坐标线都有一个[切线](@entry_id:268870)方向。这两个方向是描述该点局部几何性质的自然选择。

由此，我们引出 **[坐标基](@entry_id:270149)矢 (coordinate basis vectors)** 的几何定义。对应于坐标 $u^i$ 的[基矢](@entry_id:199546) $\mathbf{e}_i$ 被定义为位置矢量 $\mathbf{r}$ 沿着 $u^i$ 坐标线方向的变化率，即对 $u^i$ 的[偏导数](@entry_id:146280)：

$$
\mathbf{e}_i = \frac{\partial \mathbf{r}}{\partial u^i}
$$

这些[基矢](@entry_id:199546) $\mathbf{e}_i$ 张成了点 $P$ 处的 **[切空间](@entry_id:199137)** $T_P M$。切空间可以被想象成一个与[流形](@entry_id:153038)（例如[曲面](@entry_id:267450)）在点 $P$ “相切”的线性矢量空间。[坐标基](@entry_id:270149)矢 $\lbrace \mathbf{e}_1, \mathbf{e}_2, \dots, \mathbf{e}_n \rbrace$ 为这个空间提供了一组基底。与笛卡尔[基矢](@entry_id:199546) $\lbrace \hat{\mathbf{i}}, \hat{\mathbf{j}} \rbrace$ 不同，这些新的[基矢](@entry_id:199546)有几个重要特征：
1.  **局部性 (Local)**：[基矢](@entry_id:199546) $\mathbf{e}_i$ 的方向和大小通常依赖于它们所在的空间点。也就是说，$\mathbf{e}_i$ 是坐标 $(u^1, u^2, \dots)$ 的函数。
2.  **[非正交性](@entry_id:192553) (Non-orthogonal)**：[坐标基](@entry_id:270149)矢之间通常不是相互垂直的。
3.  **非单位长度 (Non-unit length)**：[坐标基](@entry_id:270149)矢的长度通常不为1。

**示例：[抛物线坐标](@entry_id:166304)系**

让我们通过一个具体的例子来理解这个定义。考虑一个从笛卡尔坐标 $(x, y)$ 到[抛物线坐标](@entry_id:166304) $(\sigma, \tau)$ 的变换 [@problem_id:1499494]：
$$
x = \sigma \tau
$$
$$
y = \frac{1}{2}(\tau^2 - \sigma^2)
$$
位置矢量为 $\mathbf{r}(x, y) = x \hat{\mathbf{i}} + y \hat{\mathbf{j}}$。通过代入坐标变换关系，我们得到 $\mathbf{r}(\sigma, \tau)$。现在，我们可以根据定义计算[坐标基](@entry_id:270149)矢 $\mathbf{e}_\sigma$ 和 $\mathbf{e}_\tau$：

$$
\mathbf{e}_\sigma = \frac{\partial \mathbf{r}}{\partial \sigma} = \frac{\partial x}{\partial \sigma} \hat{\mathbf{i}} + \frac{\partial y}{\partial \sigma} \hat{\mathbf{j}}
$$
$$
\mathbf{e}_\tau = \frac{\partial \mathbf{r}}{\partial \tau} = \frac{\partial x}{\partial \tau} \hat{\mathbf{i}} + \frac{\partial y}{\partial \tau} \hat{\mathbf{j}}
$$

计算所需的偏导数：
$$
\frac{\partial x}{\partial \sigma} = \tau, \quad \frac{\partial y}{\partial \sigma} = -\sigma
$$
$$
\frac{\partial x}{\partial \tau} = \sigma, \quad \frac{\partial y}{\partial \tau} = \tau
$$

将这些结果代入，我们得到[抛物线坐标](@entry_id:166304)系的[基矢](@entry_id:199546)，并用笛卡尔[基矢](@entry_id:199546)表示：
$$
\mathbf{e}_\sigma = \tau \hat{\mathbf{i}} - \sigma \hat{\mathbf{j}}
$$
$$
\mathbf{e}_\tau = \sigma \hat{\mathbf{i}} + \tau \hat{\mathbf{j}}
$$
正如预期的那样，这些[基矢](@entry_id:199546)的分量依赖于点在空间中的位置（由 $\sigma$ 和 $\tau$ 指定）。我们可以通过计算它们的[点积](@entry_id:149019) $\mathbf{e}_\sigma \cdot \mathbf{e}_\tau = (\tau)(\sigma) + (-\sigma)(\tau) = 0$ 来检验它们是否正交。在这个特殊的例子中，[基矢](@entry_id:199546)恰好是正交的，但这并非普遍情况。

### [切向量](@entry_id:265494)的代数观点：[方向导数](@entry_id:189133)算子

虽然将[切向量](@entry_id:265494)视为坐标曲线的[切线](@entry_id:268870)方向在几何上非常直观，但在更抽象的数学和物理理论中，另一种观点更为强大和普适。这个观点将切向量视为作用在标量场（即函数）上的 **[方向导数](@entry_id:189133)算子 (directional derivative operator)**。

想象一个定义在空间中的[标量场](@entry_id:151443) $f$。在点 $P$，我们想知道 $f$ 沿着某个矢量 $\mathbf{v}$ 方向的变化率。这正是[方向导数](@entry_id:189133) $\nabla_{\mathbf{v}} f$ 的定义。我们可以将矢量 $\mathbf{v}$ 本身 *等同于* 它所定义的那个求导操作。也就是说，矢量就是方向导数算子。

对于[坐标基](@entry_id:270149)矢 $\mathbf{e}_i = \partial \mathbf{r} / \partial u^i$，它所代表的方向是沿着 $u^i$ 坐标线增加的方向。一个函数 $f$ 沿着这个方向的变化率，根据[多元链式法则](@entry_id:635606)，正是 $f$ 对坐标 $u^i$ 的偏导数。因此，我们将[坐标基](@entry_id:270149)矢 $\mathbf{e}_i$ 等同于[偏导数](@entry_id:146280)算子 $\partial/\partial u^i$（常简记为 $\partial_i$）。

$$
\mathbf{e}_i \equiv \partial_i \equiv \frac{\partial}{\partial u^i}
$$

在这个视图下，$\partial_i$ 作为一个算子，其“作用”在一个标量函数 $f$ 上，结果是一个新的标量函数 $\partial_i(f) = \partial f / \partial u^i$。这个新函数在每一点的值，就是原函数 $f$ 在该点沿着 $u^i$ 方向的变化率。

**示例：[柱坐标](@entry_id:271645)中的[方向导数](@entry_id:189133)**

考虑三维空间中的[柱坐标](@entry_id:271645) $(\rho, \phi, z)$，以及一个用[笛卡尔坐标](@entry_id:167698)定义的[标量场](@entry_id:151443) $f(x, y, z) = x^2 + zy$ [@problem_id:1499482]。我们想计算[基矢](@entry_id:199546) $\partial_\rho$ 作用在 $f$ 上的结果，并在特定的点 $(\rho_0, \phi_0, z_0) = (2, \pi/6, 5)$ 求值。

首先，我们将函数 $f$ 用[柱坐标](@entry_id:271645)表示。利用变换关系 $x = \rho \cos\phi$，$y = \rho \sin\phi$ 和 $z=z$：
$$
f(\rho, \phi, z) = (\rho \cos\phi)^2 + z(\rho \sin\phi) = \rho^2 \cos^2\phi + z\rho \sin\phi
$$
现在，将[基矢](@entry_id:199546) $\partial_\rho$ 视为[偏导数](@entry_id:146280)算子 $\partial/\partial \rho$ 来作用于 $f$：
$$
\partial_\rho(f) = \frac{\partial}{\partial \rho} (\rho^2 \cos^2\phi + z\rho \sin\phi) = 2\rho \cos^2\phi + z \sin\phi
$$
这是一个新的[标量场](@entry_id:151443)，它在空间中每一点给出了 $f$ 沿径向的变化率。最后，我们在指定点进行求值：
$$
\partial_\rho(f) \bigg|_{(2, \pi/6, 5)} = 2(2) \cos^2\left(\frac{\pi}{6}\right) + 5 \sin\left(\frac{\pi}{6}\right) = 4\left(\frac{\sqrt{3}}{2}\right)^2 + 5\left(\frac{1}{2}\right) = 4\left(\frac{3}{4}\right) + \frac{5}{2} = 3 + \frac{5}{2} = \frac{11}{2}
$$
这个结果 $\frac{11}{2}$ 就是在点 $P$ 处，函数 $f$ 沿着 $\rho$ 坐标线方向的瞬时变化率。这种算子观点是现代[微分几何](@entry_id:145818)的基石，它使我们能够不依赖于特定的背景[嵌入空间](@entry_id:637157)（如[欧几里得空间](@entry_id:138052)）来定义和操作切向量。

### [坐标基](@entry_id:270149)的根本性质

作为一套基底，[坐标基](@entry_id:270149)矢拥有一系列深刻且普适的性质。这些性质不仅是理论推导的关键，也揭示了[坐标系](@entry_id:156346)本身的内在结构。

#### 对偶性：[基矢](@entry_id:199546)对坐标函数的作用

[坐标基](@entry_id:270149)矢 $\partial_i$ 和坐标函数 $u^j$ 之间存在一种基本的对偶关系。当我们将[基矢](@entry_id:199546)算子 $\partial_i$ 作用在坐标函数 $u^j$ 本身上时，我们会得到什么？根据定义，这相当于计算[偏导数](@entry_id:146280) $\partial u^j / \partial u^i$。这个结果很简单：如果 $i=j$，导数为1；如果 $i \neq j$，导数为0。这正是 **克罗内克 δ (Kronecker delta)** 的定义：

$$
\partial_i(u^j) = \frac{\partial u^j}{\partial u^i} = \delta_i^j = 
\begin{cases} 
1  \text{if } i = j \\
0  \text{if } i \neq j 
\end{cases}
$$

这个性质看起来似乎是平凡的同义反复，但它具有深刻的几何意义。它表明，[坐标基](@entry_id:270149)矢 $\partial_i$ 正是沿着 $u^i$ 坐标方向“探测”变化率的工具，而对其他坐标方向 $u^j$ (其中 $j \neq i$) 的变化不敏感。

我们可以通过一个不那么平凡的计算来验证这一性质，从而加深理解 [@problem_id:1499511]。让我们在二维平面上，使用极坐标 $(r, \theta)$，完全在[笛卡尔坐标](@entry_id:167698) $(x,y)$ 的框架内验证 $\partial_r(r)=1$ 和 $\partial_r(\theta)=0$。

1.  **在笛卡尔框架下表达算子和函数**：
    *   变换关系：$x = r \cos\theta$, $y = r \sin\theta$。
    *   [逆变](@entry_id:192290)换关系：$r(x,y) = \sqrt{x^2+y^2}$, $\theta(x,y) = \arctan(y/x)$。
    *   算子 $\partial_r$ 使用[链式法则](@entry_id:190743)展开：
        $$
        \partial_r = \frac{\partial x}{\partial r} \partial_x + \frac{\partial y}{\partial r} \partial_y = \cos\theta \, \partial_x + \sin\theta \, \partial_y
        $$
    *   函数 $r(x,y)$ 对 $x,y$ 的偏导数：
        $$
        \frac{\partial r}{\partial x} = \frac{x}{\sqrt{x^2+y^2}} = \frac{r\cos\theta}{r} = \cos\theta
        $$
        $$
        \frac{\partial r}{\partial y} = \frac{y}{\sqrt{x^2+y^2}} = \frac{r\sin\theta}{r} = \sin\theta
        $$
    *   函数 $\theta(x,y)$ 对 $x,y$ 的偏导数：
        $$
        \frac{\partial \theta}{\partial x} = \frac{-y}{x^2+y^2} = \frac{-r\sin\theta}{r^2} = -\frac{\sin\theta}{r}
        $$
        $$
        \frac{\partial \theta}{\partial y} = \frac{x}{x^2+y^2} = \frac{r\cos\theta}{r^2} = \frac{\cos\theta}{r}
        $$

2.  **进行计算**：
    *   计算 $\partial_r(r)$:
        $$
        \partial_r(r) = (\cos\theta \, \partial_x + \sin\theta \, \partial_y)(r) = \cos\theta \frac{\partial r}{\partial x} + \sin\theta \frac{\partial r}{\partial y} = \cos\theta(\cos\theta) + \sin\theta(\sin\theta) = \cos^2\theta + \sin^2\theta = 1
        $$
    *   计算 $\partial_r(\theta)$:
        $$
        \partial_r(\theta) = (\cos\theta \, \partial_x + \sin\theta \, \partial_y)(\theta) = \cos\theta \frac{\partial \theta}{\partial x} + \sin\theta \frac{\partial \theta}{\partial y} = \cos\theta\left(-\frac{\sin\theta}{r}\right) + \sin\theta\left(\frac{\cos\theta}{r}\right) = 0
        $$
    通过这个显式计算，我们验证了 $\partial_r(r)=1$ 和 $\partial_r(\theta)=0$，即 $\partial_r(u^j) = \delta_r^j$。类似的计算可以证明 $\partial_\theta(r)=0$ 和 $\partial_\theta(\theta)=1$。这个例子清晰地展示了算子观点的一致性和威力。

#### [可交换性](@entry_id:263314)：[李括号](@entry_id:636461)的消失

两个矢量场 $X$ 和 $Y$ 的 **李括号 (Lie bracket)**，记作 $[X, Y]$，衡量了沿着这两个矢量场方向的微小移动是否可以交换顺序。它的定义是 $[X, Y] = XY - YX$，其中 $XY$ 表示先按 $Y$ 再按 $X$ 的顺序作用在函数上。

对于任意两个[坐标基](@entry_id:270149)矢 $\partial_i$ 和 $\partial_j$，它们的李括号是什么？让我们把它作用在一个任意的[光滑函数](@entry_id:267124) $f$ 上：
$$
[\partial_i, \partial_j](f) = \partial_i(\partial_j f) - \partial_j(\partial_i f) = \frac{\partial}{\partial u^i}\left(\frac{\partial f}{\partial u^j}\right) - \frac{\partial}{\partial u^j}\left(\frac{\partial f}{\partial u^i}\right)
$$
根据微积分中著名的[克莱罗定理](@entry_id:139814) (Clairaut's theorem)，对于足够光滑的函数，[混合偏导数](@entry_id:139334)的顺序无关紧要，即 $\frac{\partial^2 f}{\partial u^i \partial u^j} = \frac{\partial^2 f}{\partial u^j \partial u^i}$。因此，上式的结果为零。

$$
[\partial_i, \partial_j] = 0
$$

这意味着 **任意两个[坐标基](@entry_id:270149)矢都是相互可交换的**。这是一个极为重要的性质，它将[坐标基](@entry_id:270149)从一般的矢量场基底中区分出来。一个任意选择的矢量场基底（例如，由电场线和[磁场](@entry_id:153296)线构成的基底）通常不具有可交换性。这个性质在几何与物理中有深刻的推论，例如它与“[积分流形](@entry_id:270062)”的存在性紧密相关。

同样，我们可以通过一个具体的、看似复杂的例子来验证这一点 [@problem_id:1499479]。考虑椭[圆柱坐标系](@entry_id:266798) $(u, v, z')$，其变换关系为：
$$
x = a \cosh u \cos v, \quad y = a \sinh u \sin v, \quad z = z'
$$
尽管[基矢](@entry_id:199546) $\partial_u$ 和 $\partial_v$ 在笛卡尔坐标系中的表达式相当复杂，但我们仍然可以证明它们的[李括号](@entry_id:636461)为零。一个直接的方法是验证 $[ \partial_u, \partial_v ]$ 作用在笛卡尔坐标函数 $x, y, z$ 上都得到零：
$$
[\partial_u, \partial_v](x) = \frac{\partial}{\partial u}\left(\frac{\partial x}{\partial v}\right) - \frac{\partial}{\partial v}\left(\frac{\partial x}{\partial u}\right) = \frac{\partial}{\partial u}(-a \cosh u \sin v) - \frac{\partial}{\partial v}(a \sinh u \cos v)
$$
$$
= (-a \sinh u \sin v) - (-a \sinh u \sin v) = 0
$$
对 $y$ 和 $z$ 进行类似的计算同样得到零。由于李括号作用在所有坐标函数上都为零，它必然是[零矢量](@entry_id:155273)。这再次印证了[坐标基](@entry_id:270149)矢的可交换性，无论坐标变换本身多么复杂。

### 从[基矢](@entry_id:199546)构建度量张量

[坐标基](@entry_id:270149)矢不仅为[切空间](@entry_id:199137)提供了[代数结构](@entry_id:137052)，它们还携带了空间的 **度量信息 (metric information)**，即关于长度和角度的信息。这是通过计算[基矢](@entry_id:199546)之间的[内积](@entry_id:158127)（[点积](@entry_id:149019)）来实现的。

**度量张量 (metric tensor)** 的分量 $g_{ij}$ 被定义为[坐标基](@entry_id:270149)矢 $\mathbf{e}_i$ 和 $\mathbf{e}_j$ 的[内积](@entry_id:158127)：
$$
g_{ij} = \mathbf{e}_i \cdot \mathbf{e}_j
$$
在欧几里得空间中，这等价于 $g_{ij} = \frac{\partial \mathbf{r}}{\partial u^i} \cdot \frac{\partial \mathbf{r}}{\partial u^j}$。度量张量是[张量分析](@entry_id:161423)的核心对象，它包含了描述空间局部几何的所有信息：
*   **长度**：沿 $u^i$ 坐标线的一小段位移 $du^i$ 的弧长平方是 $ds^2 = g_{ii} (du^i)^2$（无求和）。[基矢](@entry_id:199546) $\mathbf{e}_i$ 的长度是 $|\mathbf{e}_i| = \sqrt{g_{ii}}$。
*   **角度**：[基矢](@entry_id:199546) $\mathbf{e}_i$ 和 $\mathbf{e}_j$ 之间的夹角 $\theta_{ij}$ 由 $\cos\theta_{ij} = \frac{g_{ij}}{\sqrt{g_{ii}g_{jj}}}$ 给出。如果 $g_{ij} = 0$ ($i \neq j$)，则[基矢](@entry_id:199546)是正交的。
*   **体积**：空间中的微元体积由 $dV = \sqrt{\det(g_{ab})} \, du^1 du^2 \dots du^n$ 给出。

**示例：柱坐标的度量**

让我们计算[柱坐标](@entry_id:271645) $(\rho, \phi, z)$ 下的度量张量 $g_{ab}$ [@problem_id:1499507]。首先，我们需要[基矢](@entry_id:199546)：
$\mathbf{r} = (\rho \cos\phi) \hat{\mathbf{i}} + (\rho \sin\phi) \hat{\mathbf{j}} + z \hat{\mathbf{k}}$
$$
\mathbf{e}_\rho = \frac{\partial \mathbf{r}}{\partial \rho} = \cos\phi \, \hat{\mathbf{i}} + \sin\phi \, \hat{\mathbf{j}}
$$
$$
\mathbf{e}_\phi = \frac{\partial \mathbf{r}}{\partial \phi} = -\rho \sin\phi \, \hat{\mathbf{i}} + \rho \cos\phi \, \hat{\mathbf{j}}
$$
$$
\mathbf{e}_z = \frac{\partial \mathbf{r}}{\partial z} = \hat{\mathbf{k}}
$$
现在计算所有[内积](@entry_id:158127)：
$$
g_{\rho\rho} = \mathbf{e}_\rho \cdot \mathbf{e}_\rho = \cos^2\phi + \sin^2\phi = 1
$$
$$
g_{\phi\phi} = \mathbf{e}_\phi \cdot \mathbf{e}_\phi = (-\rho\sin\phi)^2 + (\rho\cos\phi)^2 = \rho^2(\sin^2\phi + \cos^2\phi) = \rho^2
$$
$$
g_{zz} = \mathbf{e}_z \cdot \mathbf{e}_z = 1
$$
$$
g_{\rho\phi} = \mathbf{e}_\rho \cdot \mathbf{e}_\phi = (\cos\phi)(-\rho\sin\phi) + (\sin\phi)(\rho\cos\phi) = 0
$$
类似地，$g_{\rho z} = 0$ 和 $g_{\phi z} = 0$。因此，度量张量以矩阵形式表示为：
$$
(g_{ab}) = \begin{pmatrix} 1  0  0 \\ 0  \rho^2  0 \\ 0  0  1 \end{pmatrix}
$$
这是一个对角矩阵，表明[柱坐标系](@entry_id:266798)的[基矢](@entry_id:199546)是相互正交的。对角线上的元素 $g_{\rho\rho}=1$ 和 $g_{zz}=1$ 说明 $\mathbf{e}_\rho$ 和 $\mathbf{e}_z$ 是单位长度的，而 $g_{\phi\phi}=\rho^2$ 说明 $\mathbf{e}_\phi$ 的长度是 $|\mathbf{e}_\phi| = \sqrt{\rho^2} = \rho$。这与我们的几何直观相符：离 $z$ 轴越远，沿角向移动相同的角度 $\Delta\phi$，走过的[弧长](@entry_id:191173)就越长。

度量张量的[行列式](@entry_id:142978)为 $\det(g_{ab}) = 1 \cdot \rho^2 \cdot 1 = \rho^2$。因此，[柱坐标系](@entry_id:266798)下的体积微元是 $dV = \sqrt{\rho^2} \, d\rho d\phi dz = \rho \, d\rho d\phi dz$，这正是我们从[多变量微积分](@entry_id:147547)中熟悉的公式。

计算[抛物线坐标](@entry_id:166304)系中的一个度量分量 $g_{\sigma\sigma}$ 也是一个很好的练习 [@problem_id:1499517]。我们已经求得 $\mathbf{e}_\sigma = \tau \hat{\mathbf{i}} - \sigma \hat{\mathbf{j}}$，因此：
$$
g_{\sigma\sigma} = \mathbf{e}_\sigma \cdot \mathbf{e}_\sigma = (\tau)^2 + (-\sigma)^2 = \sigma^2 + \tau^2
$$

### 矢量分量及其变换

一旦我们有了[坐标基](@entry_id:270149)底 $\{\mathbf{e}_i\}$，[切空间](@entry_id:199137)中的任何矢量 $\mathbf{V}$ 都可以被唯一地分解为这些[基矢](@entry_id:199546)的[线性组合](@entry_id:154743)：
$$
\mathbf{V} = V^1 \mathbf{e}_1 + V^2 \mathbf{e}_2 + \dots + V^n \mathbf{e}_n = V^i \mathbf{e}_i
$$
这里的系数 $(V^1, V^2, \dots, V^n)$ 被称为矢量 $\mathbf{V}$ 在该[坐标基](@entry_id:270149)下的 **[逆变分量](@entry_id:185440) (contravariant components)**。上标 $i$ 是一种约定，用于标识[逆变分量](@entry_id:185440)。

物理学中一个自然出现[逆变分量](@entry_id:185440)的例子是速度。如果一个粒子的轨迹由坐标函数 $u^i(t)$ 描述，其速度矢量 $\mathbf{v}$ 可以通过链式法则计算：
$$
\mathbf{v} = \frac{d\mathbf{r}}{dt} = \frac{\partial \mathbf{r}}{\partial u^i} \frac{du^i}{dt} = \left(\frac{du^i}{dt}\right) \mathbf{e}_i
$$
比较上式与 $\mathbf{v} = v^i \mathbf{e}_i$，我们发现速度的[逆变分量](@entry_id:185440)就是坐标对时间的导数：$v^i = \frac{du^i}{dt}$。这个关系在分析粒子运动时非常有用 [@problem_id:1500]。例如，通过分析一个约束条件（如粒子在一个特定[曲面](@entry_id:267450)上运动），我们可以找到不同[坐标速度](@entry_id:272549)分量之间的关系，例如 $|v^\phi / v^\theta| = |d\phi/d\theta|$。

除了[逆变分量](@entry_id:185440)，还有另一种描述矢量的方式，即 **协变分量 (covariant components)**，用下标表示 $V_i$。它被定义为矢量 $\mathbf{V}$ 在[基矢](@entry_id:199546) $\mathbf{e}_i$ 方向上的投影，通过[内积](@entry_id:158127)计算：
$$
V_i = \mathbf{V} \cdot \mathbf{e}_i
$$
将 $\mathbf{V} = V^j \mathbf{e}_j$ 代入，我们得到：
$$
V_i = (V^j \mathbf{e}_j) \cdot \mathbf{e}_i = V^j (\mathbf{e}_j \cdot \mathbf{e}_i) = V^j g_{ji} = g_{ij} V^j
$$
这个公式 $V_i = g_{ij} V^j$ 是度量张量的核心功能之一：它在[逆变和协变分量](@entry_id:268728)之间建立了联系，被称为 **降下标 (lowering an index)**。

当[坐标系](@entry_id:156346)改变时，[基矢](@entry_id:199546)会改变，因此矢量的分量也必须相应改变，以保证矢量本身（作为一个几何对象）保持不变。分量的变换法则与[基矢](@entry_id:199546)的变换法则是“相反”的。协变分量遵循的变换法则是：
$$
\bar{V}_i = \frac{\partial x^j}{\partial \bar{x}^i} V_j
$$
其中 $x^j$ 是旧坐标，$\bar{x}^i$ 是新坐标。$\frac{\partial x^j}{\partial \bar{x}^i}$ 是逆变换的[雅可比矩阵](@entry_id:264467)。让我们通过一个[各向异性缩放](@entry_id:261477)的例子来理解这一点 [@problem_id:1499452]。

**示例：[各向异性缩放](@entry_id:261477)下的[协变](@entry_id:634097)分量**

假设从[笛卡尔坐标](@entry_id:167698) $(x^1, x^2, x^3)$ 变换到一个新的[坐标系](@entry_id:156346) $(\bar{x}^1, \bar{x}^2, \bar{x}^3)$，变换关系为 $\bar{x}^i = \alpha_i x^i$（$i=1,2,3$，无求和），其中 $\alpha_i$ 是非零常数。[逆变](@entry_id:192290)换为 $x^i = \bar{x}^i / \alpha_i$。逆变换的[雅可比矩阵](@entry_id:264467)为：
$$
\frac{\partial x^j}{\partial \bar{x}^i} = \frac{\partial}{\partial \bar{x}^i} \left(\frac{\bar{x}^j}{\alpha_j}\right) = \frac{1}{\alpha_j} \delta_i^j = \frac{1}{\alpha_i} \delta_i^j
$$
假设在原[笛卡尔坐标系](@entry_id:169789)中有一个常矢量场 $\mathbf{V} = V^j \mathbf{e}_j$。由于原[坐标系](@entry_id:156346)是笛卡尔的，$g_{ij} = \delta_{ij}$，所以其[协变](@entry_id:634097)分量 $V_j = g_{jk} V^k = \delta_{jk}V^k = V^j$。现在，我们可以计算在新[坐标系](@entry_id:156346)中的[协变](@entry_id:634097)分量 $\bar{V}_i$：
$$
\bar{V}_i = \frac{\partial x^j}{\partial \bar{x}^i} V_j = \left(\frac{1}{\alpha_i} \delta_j^i\right) V_j = \frac{1}{\alpha_i} V_i
$$
因此，新的[协变](@entry_id:634097)分量是 $(\bar{V}_1, \bar{V}_2, \bar{V}_3) = \left(\frac{V^1}{\alpha_1}, \frac{V^2}{\alpha_2}, \frac{V^3}{\alpha_3}\right)$。

在更复杂的[坐标系](@entry_id:156346)（如[球坐标](@entry_id:146054)）中分解一个给定的笛卡尔矢量场，则需要更详细的计算，通常涉及求解一个[线性方程组](@entry_id:148943)或利用对偶基的概念 [@problem_id:1499516]。

### [坐标系](@entry_id:156346)的局限性：[基矢](@entry_id:199546)的退化与[奇异点](@entry_id:199525)

[坐标系](@entry_id:156346)是描述空间的强大工具，但它们本质上是局部的，并且可能在某些点上失效。这些失效的点被称为 **坐标[奇异点](@entry_id:199525) (coordinate singularities)**。一个典型的例子是[球坐标系](@entry_id:167517) $(r, \theta, \phi)$ 在 $z$ 轴上的表现。

在 $z$ 轴上（即 $\theta=0$ 或 $\theta=\pi$），方位角 $\phi$ 的定义变得模糊不清。一个在北极点上的点，其 $\phi$ 值可以是任何数，但描述的都是同一个点。这种几何上的模糊性在[坐标基](@entry_id:270149)矢中有着明确的体现。

让我们回顾一下球坐标的[基矢](@entry_id:199546)，特别是 $\mathbf{e}_\phi$：
$$
\mathbf{e}_\phi = \frac{\partial \mathbf{r}}{\partial \phi} = -r\sin\theta\sin\phi \, \hat{\mathbf{i}} + r\sin\theta\cos\phi \, \hat{\mathbf{j}}
$$
这个[基矢](@entry_id:199546)的长度（范数）是：
$$
|\mathbf{e}_\phi| = \sqrt{(-r\sin\theta\sin\phi)^2 + (r\sin\theta\cos\phi)^2} = \sqrt{r^2\sin^2\theta(\sin^2\phi+\cos^2\phi)} = r\sin\theta
$$
当一个点趋向于 $z$ 轴时，即 $\theta \to 0$ 或 $\theta \to \pi$，我们看到 $\sin\theta \to 0$，因此 $|\mathbf{e}_\phi| \to 0$。这意味着[基矢](@entry_id:199546) $\mathbf{e}_\phi$ 的长度缩减为零！

在[奇异点](@entry_id:199525)上，$\mathbf{e}_\phi$ 变成了[零矢量](@entry_id:155273)。因此，原来的三个[基矢](@entry_id:199546) $\{\mathbf{e}_r, \mathbf{e}_\theta, \mathbf{e}_\phi\}$ 不再能张成一个三维的[切空间](@entry_id:199137)；它们变得[线性相关](@entry_id:185830)（因为其中一个是[零矢量](@entry_id:155273)）。这意味着[球坐标](@entry_id:146054)基在 $z$ 轴上是 **退化 (degenerate)** 的。这并不是说空间本身在这些点有什么问题——[切空间](@entry_id:199137)仍然是一个正常的三维空间——而是我们选择的[坐标系](@entry_id:156346)在这些点上无法提供一个良好的基底。

一个有趣的问题是，当 $\theta$ 趋近于零时，$\mathbf{e}_\phi$ 是如何“消失”的 [@problem_id:1499490]。考虑在常数半径 $R$ 和一个很小的极角 $\alpha$ 上，$\mathbf{e}_\phi$ 的行为。上面我们看到 $|\mathbf{e}_\phi| = R \sin\alpha$。对于很小的 $\alpha$，我们有 $\sin\alpha \approx \alpha$。因此，[基矢](@entry_id:199546)的长度与到 $z$ 轴的角度距离成正比。

通过分析在不同 $\phi$ 值处的 $\mathbf{e}_\phi$ 矢量的组合，例如在 $\phi=0$ 和 $\phi=\pi/2$ 处的矢量和，我们可以更定量地研究这种行为。计算表明，某些涉及 $|\mathbf{e}_\phi|$ 的组合在 $\alpha \to 0$ 的极限下会收敛到一个有限的非零值，这精确地刻画了[基矢](@entry_id:199546)退化的速率。

理解坐标[奇异点](@entry_id:199525)至关重要，因为它们在物理学中频繁出现，例如在[黑洞视界](@entry_id:746859)的描述（[史瓦西坐标](@entry_id:185992)）或[规范场](@entry_id:159627)论中。识别一个[奇异点](@entry_id:199525)是真实的[物理奇点](@entry_id:260744)还是仅仅是[坐标系](@entry_id:156346)选择不当造成的“人造物”，是理论物理中的一项基本技能。