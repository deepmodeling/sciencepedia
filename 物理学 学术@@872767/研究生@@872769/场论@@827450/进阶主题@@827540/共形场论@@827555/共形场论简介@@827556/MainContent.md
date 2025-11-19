## 引言
共形场论（Conformal Field Theory, CFT）是现代理论物理的基石之一，它源于对[统计力](@entry_id:194984)学中[临界点](@entry_id:144653)[相变](@entry_id:147324)的深刻理解，如今已发展成为连接[量子场论](@entry_id:138177)、弦论、凝聚态物理和量子引力等多个领域的强大理论框架。其核心力量在于对称性——在二维空间中，[共形对称性](@entry_id:142366)是无限维的，这为理论施加了极强的约束，使得许多在其他框架中难以解决的强耦合问题变得精确可解。这填补了传统微扰方法在处理标度不变系统时的空白，为我们提供了一扇洞察物理世界非微扰本质的独特窗口。

本文旨在为读者提供一份系统而深入的[共形场论](@entry_id:145449)指南。我们将从第一部分“原理与机制”出发，深入剖析CFT的代数心脏——[Virasoro代数](@entry_id:143942)、[表示论](@entry_id:137998)和[算符乘积展开](@entry_id:141941)（OPE），揭示对称性如何决定[理论的谱](@entry_id:634092)与关联函数。随后，在“应用与跨学科联系”部分，我们将展示这些抽象原理的巨大威力，探讨CFT如何在描述[临界现象](@entry_id:144727)、分数[量子霍尔效应](@entry_id:136283)、量子纠缠乃至[黑洞](@entry_id:158571)物理和全息[引力](@entry_id:175476)中扮演关键角色。最后，“动手实践”部分将通过一系列具体的计算问题，帮助读者将理论知识转化为解决问题的实践能力，从而真正掌握这一优雅而强大的物理工具。

## 原理与机制

[二维共形场论](@entry_id:148817)（CFT）的强大之处在于其对称性对理论的结构施加了极强的约束。这些约束不仅固定了关联函数的形式，还决定了[理论的谱](@entry_id:634092)（即算符的维度和种类）以及它们在不同几何背景下的行为。本章将系统地阐述[二维共形场论](@entry_id:148817)的核心原理与机制，从其底层的[代数结构](@entry_id:137052)出发，逐步深入到表示论、关联函数、高级模型和不变性等关键概念。

### [共形对称性](@entry_id:142366)与[Virasoro代数](@entry_id:143942)

在二维[欧几里得空间](@entry_id:138052)中，共形变换是保持角度不变的坐标变换。对于复坐标 $z = x+iy$ 和 $\bar{z} = x-iy$，任何解析函数 $z \to w(z)$ 和反[解析函数](@entry_id:139584) $\bar{z} \to \bar{w}(\bar{z})$ 都是[共形变换](@entry_id:159863)。这种无限维的对称性是[二维共形场论](@entry_id:148817)具有精确可解性的根源。

与任何连续对称性一样，[共形对称性](@entry_id:142366)也对应着一个[守恒流](@entry_id:148966)。这个[守恒流](@entry_id:148966)的各个分量组成了对称的、无迹的[能量-动量张量](@entry_id:203902) $T_{\mu\nu}$。在复坐标下，守恒和[平移不变性](@entry_id:195885)意味着分量 $T_{zz}$ 仅依赖于 $z$，而 $T_{\bar{z}\bar{z}}$ 仅依赖于 $\bar{z}$。我们分别将它们记为全纯部分 $T(z)$ 和反全纯部分 $\bar{T}(\bar{z})$。这两个算符是理论中最重要的对象，它们是共形[变换的生成元](@entry_id:172031)。

[共形场论](@entry_id:145449)中的算符及其关联函数可以通过**[算符乘积展开](@entry_id:141941)（OPE）**来研究。当两个算符的位置非常接近时，它们的乘积可以展开为一列位于其中一个位置的局域算符，其系数是关于它们之间距离的函数。$T(z)$ 与自身的OPE定义了理论的核心[代数结构](@entry_id:137052)：

$$
T(z) T(w) \sim \frac{c/2}{(z-w)^4} + \frac{2 T(w)}{(z-w)^2} + \frac{\partial T(w)}{z-w} + \text{正则项}
$$

其中，符号 $\sim$ 表示在 $z \to w$ 极限下的奇异行为。这个展开式中的系数是普适的。最重要的系数是中心项（$1/(z-w)^4$ 的系数）中的常数 $c$，它被称为**中心荷（central charge）**。[中心荷](@entry_id:155921) $c$ 是一个描述共形场论基本性质的关键参数，它衡量了[共形对称性](@entry_id:142366)在量子化后出现的反常（anomaly）。

[能量-动量张量](@entry_id:203902) $T(z)$ 可以围绕原点进行Laurent展开，其模式 $L_n$ 被称为**[Virasoro生成元](@entry_id:190266)**：

$$
T(z) = \sum_{n \in \mathbb{Z}} \frac{L_n}{z^{n+2}}
$$

将此展开代入 $T(z)T(w)$ 的OPE，可以推导出[Virasoro生成元](@entry_id:190266)之间的[对易关系](@entry_id:136780)，即**[Virasoro代数](@entry_id:143942)**:

$$
[L_m, L_n] = (m-n)L_{m+n} + \frac{c}{12}m(m^2-1)\delta_{m+n,0}
$$

这个代数是所有[二维共形场论](@entry_id:148817)的基石。经典情况下（$c=0$），它退化为Witt代数。量子效应导致了中心项的出现，这是CFT丰富结构的核心来源。$L_0$ 算符在[径向量子化](@entry_id:149452)中扮演[哈密顿量](@entry_id:172864)的角色，而 $L_{-1}$ 和 $L_1$ 分别生成平移和[特殊共形变换](@entry_id:148985)，它们共同构成了全局[共形代数](@entry_id:159054) $SL(2, \mathbb{C})$。

### [表示论](@entry_id:137998)：主场、后代与[零态](@entry_id:154996)

[共形场论](@entry_id:145449)中的物理态和算符被组织成[Virasoro代数](@entry_id:143942)的表示。其中最重要的是最高权重表示，它由一个**主态（primary state）** $|h\rangle$ 生成。一个主态由两个条件定义：

1.  它是 $L_0$ 的本征态，[本征值](@entry_id:154894)为**共形维度（conformal dimension）** $h$：$L_0|h\rangle = h|h\rangle$。
2.  它被所有下降算符（$n>0$）湮灭：$L_n|h\rangle = 0$ for $n>0$。

与主态 $|h\rangle$ 对应的算符 $\phi(z)$ 被称为**[主场](@entry_id:153633)（primary field）**。通过将[上升算符](@entry_id:191512) $L_{-n}$ ($n>0$) 作用于主态，我们可以生成无穷多个新的态，称为**[后代态](@entry_id:153392)（descendant states）**，例如 $L_{-1}|h\rangle, L_{-2}|h\rangle, L_{-1}^2|h\rangle$ 等。由一个主态及其所有[后代态](@entry_id:153392)张成的[线性空间](@entry_id:151108)构成了一个[Virasoro代数](@entry_id:143942)的表示，称为**[Verma模](@entry_id:201926)**。

在某些特定的共形维度 $h$ 和中心荷 $c$ 下，[Verma模](@entry_id:201926)中可能出现一种特殊的非零[后代态](@entry_id:153392) $|\chi\rangle$，它自身也满足主态的条件，即对于所有 $n>0$ 都有 $L_n|\chi\rangle=0$。这种态被称为**[零态](@entry_id:154996)（null state）**。[零态](@entry_id:154996)的存在意味着[Verma模](@entry_id:201926)是可约的，因为由[零态](@entry_id:154996)及其后代张成的[子空间](@entry_id:150286)是一个不变[子模](@entry_id:148922)。在幺正理论中，为了保持[内积](@entry_id:158127)的正定性，我们必须将[零态](@entry_id:154996)及其所有[后代态](@entry_id:153392)从[希尔伯特空间](@entry_id:261193)中除去。这极大地简化了[理论的谱](@entry_id:634092)，是构造有理共形场论（如极简模型）的关键。

[零态](@entry_id:154996)的存在条件为 $(c, h)$ 的值施加了强有力的约束。例如，我们可以考察一个二级[后代态](@entry_id:153392) $|\chi\rangle = (L_{-2} - k L_{-1}^2)|h\rangle$ 成为[零态](@entry_id:154996)的条件 [@problem_id:335306]。要求 $L_1|\chi\rangle=0$ 和 $L_2|\chi\rangle=0$ 会导出一个关于 $c$ 和 $h$ 的[代数方程](@entry_id:272665)。通过直接计算，可以发现，当 $k = \frac{3}{2(2h+1)}$ 时，$L_1|\chi\rangle=0$ 成立。进一步要求 $L_2|\chi\rangle=0$ 则给出了一个非平凡的约束：

$$
c = \frac{2h(5-8h)}{2h+1}
$$

这个结果揭示了理论的动力学内容是如何被其[代数结构](@entry_id:137052)所决定的。对于满足这类关系的 $(c, h)$，[理论的谱](@entry_id:634092)将变得更为简单和受限。

### 关联函数与共形[Ward恒等式](@entry_id:147000)

[共形对称性](@entry_id:142366)最强大的应用之一是其对关联函数的约束。能量-动量张量 $T(z)$ 与一个共形维度为 $h_i$ 的主场 $\phi_i(w)$ 的OPE具有普适形式：

$$
T(z) \phi_i(w) \sim \frac{h_i}{(z-w)^2} \phi_i(w) + \frac{1}{z-w} \partial_w \phi_i(w) + \dots
$$

这个OPE可以理解为算符 $\phi_i(w)$ 在由 $T(z)$ 生成的无穷小[共形变换](@entry_id:159863) $z \to z + \epsilon(z)$下的响应。第一项反映了 $\phi_i$ 作为密度权重为 $h_i$ 的张量的变换，而第二项则反映了其坐标的平移。

将 $T(z)$ 插入到一个由主场构成的关联函数中，并利用上述OPE，我们可以推导出**共形[Ward恒等式](@entry_id:147000)**。它将一个包含 $T(z)$ 的 $(n+1)$-点函数与一个 $n$-点函数及其导数联系起来：

$$
\langle T(z) \phi_1(w_1) \dots \phi_n(w_n) \rangle = \sum_{i=1}^n \left( \frac{h_i}{(z-w_i)^2} + \frac{1}{z-w_i} \frac{\partial}{\partial w_i} \right) \langle \phi_1(w_1) \dots \phi_n(w_n) \rangle
$$

这个恒等式是计算和约束关联函数的强大工具。作为一个直接的应用，我们可以计算三点函数 $\langle T(z) \phi_1(w_1) \phi_2(w_2) \rangle$，其中 $\phi_1, \phi_2$ 是两个共形维度均为 $h$ 的不同主场 [@problem_id:335308]。它们的二点函数由[共形对称性](@entry_id:142366)固定为 $\langle \phi_1(w_1) \phi_2(w_2) \rangle = \frac{C_{12}}{(w_1-w_2)^{2h}}$。应用[Ward恒等式](@entry_id:147000)，我们发现：

$$
\langle T(z) \phi_1(w_1) \phi_2(w_2) \rangle = h \frac{(w_1 - w_2)^2}{(z - w_1)^2 (z - w_2)^2} \langle \phi_1(w_1) \phi_2(w_2) \rangle
$$

这个结果完美地展示了[Ward恒等式](@entry_id:147000)如何将一个看似复杂的三点函数完全由一个更简单的两点函数和场的共形维度所确定。全局[共形对称性](@entry_id:142366)（$SL(2,\mathbb{C})$）足以固定两点和三点函数的形式，而四点函数则被固定为一个依赖于交叉比 $x = \frac{(z_1-z_2)(z_3-z_4)}{(z_1-z_3)(z_2-z_4)}$ 的任意函数。

### [共形映射](@entry_id:271672)与真空结构

[共形场论](@entry_id:145449)的一个核心技术是通过[共形映射](@entry_id:271672)将理论从一个复杂的几何背景变换到一个简单的背景（如复平面或[上半平面](@entry_id:199119)）上进行计算。算符在共形变换 $z \to w(z)$ 下的变换法则取决于它的共形维度。对于一个准主场（quasi-primary field，仅对全局[共形变换](@entry_id:159863)有简单变换法则的场），其变换法则是简单的。然而，能量-动量张量 $T(z)$ 本身不是主场，它的变换法则包含一个反常项：

$$
T_{old}(z) = \left(\frac{dw}{dz}\right)^2 T_{new}(w(z)) + \frac{c}{12} \{w, z\}
$$

这里的 $\{w, z\}$ 是**[Schwarzian导数](@entry_id:161840)**：

$$
\{w, z\} = \frac{w'''(z)}{w'(z)} - \frac{3}{2} \left(\frac{w''(z)}{w'(z)}\right)^2
$$

[Schwarzian导数](@entry_id:161840)项的存在具有深刻的物理意义。它表明CFT的真空态不是在所有几何背景下都相同的。当我们将平坦空间（其[真空期望值](@entry_id:146340) $\langle T(z) \rangle_{plane} = 0$）映射到一个弯曲或有边界的空间时，新的真空态会产生非零的能量-动量张量[期望值](@entry_id:153208)。这正是**[Casimir效应](@entry_id:148651)**在CFT中的体现。

我们可以通过两个例子来阐明这一点。首先，考虑一个张角为 $\alpha$ 的楔形区域 $W_\alpha$。它可以通过映射 $w(z) = z^{\pi/\alpha}$ 变换到上半平面 $\mathbb{H}$，而已知 $\langle T(w) \rangle_{\mathbb{H}} = 0$。利用 $T(z)$ 的变换法则，我们可以计算出在楔形区域中的[真空期望值](@entry_id:146340) [@problem_id:335310]：

$$
\langle T(z) \rangle_{W_{\alpha}} = \frac{c}{12} \{w, z\} = \frac{c (\alpha^2 - \pi^2)}{24 \alpha^2 z^2}
$$

另一个重要的例子是将复平面映射到一个半径为 $R$ 的柱面。该映射为 $z(\zeta) = \exp(-i\zeta/R)$，其中 $\zeta=\tau+i\sigma$ 是柱面坐标。利用 $T(z)$ 的变换法则和平面上的两点函数 $\langle T_{plane}(z_1) T_{plane}(z_2) \rangle = \frac{c/2}{(z_1 - z_2)^4}$，我们可以计算出柱面上的两点函数 [@problem_id:335463]。计算结果包含两个部分：

$$
\langle T_{cyl}(\zeta_1) T_{cyl}(\zeta_2) \rangle = \frac{c}{32 R^4 \sin^4\left( \frac{\zeta_1 - \zeta_2}{2 R} \right)} + \frac{c^2}{576 R^4}
$$

第一项来自平面上两点函数的变换，而第二项则是一个常数，它源于在柱面上非零的单点函数 $\langle T_{cyl}(\zeta) \rangle = -\frac{c}{24R^2}$ 的乘积。这再次展示了[Casimir效应](@entry_id:148651)：在紧凑的空间维度上，真空具有非零的能量密度。

### 高级结构与模型实例

在掌握了[Virasoro代数](@entry_id:143942)、表示论和关联函数的基本工具后，我们可以探索CFT中更深刻的结构和具体的模型。

#### [算符乘积展开](@entry_id:141941)与共形块

OPE不仅是一种计算工具，它本身也定义了一个满足结合律的算符代数。一个四点关联函数 $\langle \phi_1(z_1) \phi_2(z_2) \phi_3(z_3) \phi_4(z_4) \rangle$ 可以通过两种不同的方式进行OPE分解（例如，先合并12和34，或先合并14和23）。这两种分解方式结果的相等性，即**[交叉对称性](@entry_id:145431)**，是CFT的核心约束。

当我们将 $\phi_1(z_1)\phi_2(z_2)$ 的OPE代入四点函数时，会得到一个对所有出现在OPE中的中间[主场](@entry_id:153633) $\mathcal{O}_p$ 的求和：

$$
\langle \phi_1(z_1) \phi_2(z_2) \phi_3(z_3) \phi_4(z_4) \rangle = \sum_p C_{12p} C_{p34} \mathcal{F}(c, h_p, h_i; x)
$$

这里的 $C_{ijk}$ 是OPE系数，而 $\mathcal{F}(c, h_p, h_i; x)$ 是**共形块（conformal block）**。共形块是普适的函数，它由对称性完全确定，封装了中间[主场](@entry_id:153633) $\mathcal{O}_p$ 及其所有Virasoro后代对四点函数的贡献。理论的非普适信息（动力学）则完全包含在OPE系数 $C_{ijk}$ 和谱 $\{h_p, c\}$ 中。

共形块可以展开为交叉比 $x$ 的[幂级数](@entry_id:146836)。例如，对于四个相同的标量场，其s-channel共形块具有 $x^{h_p - 2h}(1 + \mathcal{F}_1 x + \mathcal{F}_2 x^2 + \dots)$ 的形式。低阶系数 $\mathcal{F}_k$ 是 $c, h, h_p$ 的函数。例如，$\mathcal{F}_2$ 的表达式中包含一个仅由全局 $SL(2, \mathbb{C})$ 对称性决定的部分，以及一个正比于中心荷 $c$ 的纯Virasoro修正项 $\Delta\mathcal{F}_2$。在特定条件下，这个修正项可以为零 [@problem_id:335327]。例如，当 $c = \frac{4h^2 (h_p - 1)}{h_p}$ 时，$\Delta\mathcal{F}_2=0$，此时Virasoro共形块的行为在低阶与全局共形块完全一致，这揭示了[中心荷](@entry_id:155921)在区分全局[共形对称性](@entry_id:142366)与完整Virasoro对称性中的关键作用。

#### [共形自举](@entry_id:153253)

[交叉对称性](@entry_id:145431)将四点函数在不同通道的共形块展开联系起来，形成一个泛函方程，即**自举方程（bootstrap equation）**。这个方程提供了一套关于CFT数据（维度 $h_p$ 和OPE系数 $C_{ijk}$）的自洽性约束。现代**[共形自举](@entry_id:153253)（conformal bootstrap）**方法正是利用这些约束，在不知道拉格朗日量的情况下，以极高的精度确定CFT的谱和OPE系数。

例如，通过对自举方程作用一个特定的[微分](@entry_id:158718)算符，可以得到关于CFT数据的求和规则 [@problem_id:335379]。对于3D Ising模型中的自旋场 $\sigma$ 的四点函数，这个求和规则（在截断到只包含单位算符 $I$、能量算符 $\epsilon$ 和[能量-动量张量](@entry_id:203902) $T$ 的近似下）可以写为：

$$
\sum_{\mathcal{O}=I,\epsilon,T} \lambda_{\sigma\sigma\mathcal{O}} \mathcal{D}_{\mathcal{O}} \approx 0
$$

其中 $\lambda_{\sigma\sigma\mathcal{O}}$ 是OPE系数的平方，$\mathcal{D}_{\mathcal{O}}$ 是由共形块导数决定的已知量。这个方程允许我们求解一个CFT数据，例如 $\lambda_{\sigma\sigma\epsilon}$，来表示其他的CFT数据，如 $\lambda_{\sigma\sigma\epsilon} = \frac{\Delta_\sigma-\lambda_{\sigma\sigma T}\,\mathcal{D}_T}{\mathcal{D}_\epsilon}$。这个简单的例子捕捉了[共形自举](@entry_id:153253)方法的核心思想：将理论的动力学转化为一个代数问题。

#### 扩展对称性：[WZW模型](@entry_id:148102)

除了[Virasoro代数](@entry_id:143942)，许多CFT还拥有额外的对称性，最典型的例子是**Wess-Zumino-Witten (WZW) 模型**。[WZW模型](@entry_id:148102)不仅具有[共形对称性](@entry_id:142366)，还具有一个**仿射[Kac-Moody代数](@entry_id:154948)**，它由一组流算符 $J^a(z)$ 生成。对于基于群 $SU(N)$ 的[WZW模型](@entry_id:148102)，这些流的OPE为：

$$
J^a(z) J^b(w) \sim \frac{k\, \delta^{ab}}{(z-w)^2} + \frac{i f^{abc} J^c(w)}{z-w} + \text{正则项}
$$

其中 $f^{abc}$ 是李代数 $\mathfrak{su}(N)$ 的[结构常数](@entry_id:157960)，整数 $k$ 被称为**级别（level）**。[WZW模型](@entry_id:148102)的一个美妙之处在于，其能量-动量张量可以完全由流算符通过**[Sugawara构造](@entry_id:156751)**得到：

$$
T(z) = \frac{1}{2(k+g)} \sum_{a} :J^a(z) J^a(z):
$$

其中 $g$ 是李代数的对偶[Coxeter数](@entry_id:185785)（对于SU(N)为 $N$）。这个构造直接将[能量-动量张量](@entry_id:203902)与[流代数](@entry_id:162160)联系起来。通过计算这个 $T(z)$ 的OPE，可以确定[WZW模型](@entry_id:148102)的[中心荷](@entry_id:155921) [@problem_id:335433]，对于SU(N)在级别k的模型，其[中心荷](@entry_id:155921)为：

$$
c = \frac{k \dim(G)}{k+g} = \frac{k(N^2-1)}{k+N}
$$

[Kac-Moody代数](@entry_id:154948)的OPE结构同样具有结合律，这可以用来推导新的OPE关系。例如，通过考察三阶OPE $J^b(z)J^a(y)\phi_j(w)$ 的不同展开方式，可以确定流算符与[主场](@entry_id:153633)后代之间的OPE系数 [@problem_id:335360]，这为研究[WZW模型](@entry_id:148102)的关联函数提供了具体的计算工具。

#### 有理[共形场论](@entry_id:145449)与[模不变性](@entry_id:150402)

当一个CFT只包含有限个主场时，它被称为**有理[共形场论](@entry_id:145449)（Rational CFT, RCFT）**。上文提到的Virasoro[零态](@entry_id:154996)所导出的**极简模型**（如Ising模型）和[WZW模型](@entry_id:148102)都是RCFT的典型例子。

RCFT的谱可以用**特征标（character）**来描述。一个[主场](@entry_id:153633) $\phi_j$ 的特征标 $\chi_j(\tau)$ 是一个关于[复变量](@entry_id:175312) $\tau$ 的函数，它对该[主场](@entry_id:153633)所在[Verma模](@entry_id:201926)中所有态的简并度进行编码：

$$
\chi_j(\tau) = \text{Tr}_{\mathcal{V}_j}(q^{L_0 - c/24}) = q^{h_j - c/24} \sum_{N=0}^\infty d_j(N) q^N
$$

其中 $q=e^{2\pi i \tau}$，$d_j(N)$ 是在[主场](@entry_id:153633) $h_j$ 之上第 $N$ 级[后代态](@entry_id:153392)的数目。

将CFT定义在一个环面上，其[复结构](@entry_id:269128)由 $\tau$ 描述，理论的[配分函数](@entry_id:193625) $Z(\tau, \bar{\tau})$ 可以表示为特征标的组合。对于最简单的**对角模型**，[配分函数](@entry_id:193625)是：

$$
Z(\tau, \bar{\tau}) = \sum_j \chi_j(\tau) \bar{\chi}_j(\bar{\tau}) = \sum_j |\chi_j(\tau)|^2
$$

[配分函数](@entry_id:193625)物理上不应依赖于我们如何选择环面的[基本周期](@entry_id:267619)，这意味着它必须在**[模群](@entry_id:184647)** $SL(2, \mathbb{Z})$ 的变换下保持不变。[模群](@entry_id:184647)由两个生成元：$T: \tau \to \tau+1$ 和 $S: \tau \to -1/\tau$ 生成。[配分函数](@entry_id:193625)的[不变性](@entry_id:140168)，特别是对 $S$ 变换的[不变性](@entry_id:140168)，即**[模不变性](@entry_id:150402)**，对特征标的行为施加了极强的约束。在 $S$ 变换下，特征标本身会线性组合：

$$
\chi_i(-1/\tau) = \sum_j S_{ij} \chi_j(\tau)
$$

矩阵 $S_{ij}$ 被称为**模[S矩阵](@entry_id:137017)**，它的元素是理论的重要数据。对于Virasoro极简模型，S矩阵的元素由著名的**Kac-[Verlinde公式](@entry_id:145134)**给出。例如，对于2D Ising模型（$c=1/2$），它有三个[主场](@entry_id:153633)：单[位场](@entry_id:143025) $I(h=0)$，自旋场 $\sigma(h=1/16)$，能量场 $\epsilon(h=1/2)$。利用Kac-[Verlinde公式](@entry_id:145134)，我们可以计算出其[S矩阵](@entry_id:137017)的各个元素，例如连接自旋场和能量场的[矩阵元](@entry_id:186505)为 [@problem_id:335337]：

$$
S_{\sigma\epsilon} = -\frac{\sqrt{2}}{2}
$$

[模不变性](@entry_id:150402)是一个深刻的自洽性条件，它将紫外（算符谱）和红外（环面上的物理）联系起来，并成为分类和解决有理[共形场论](@entry_id:145449)的中心原则。例如，在[SU(2)](@entry_id:136274)级别为1的[WZW模型](@entry_id:148102)中，只有两个主场（$j=0, 1/2$），我们可以利用特征标来计算在特定能量级别的态简并度。例如，在能量为 $(\Delta, \bar{\Delta})=(1,1)$ 的级别上，只有 $j=0$ 扇区有贡献，其贡献来自于左右两边的1级[后代态](@entry_id:153392)，其数量等于 $\mathfrak{su}(2)$ 代数的维度，即3。因此，总共有 $3 \times 3 = 9$ 个态 [@problem_id:335434]。这个看似简单的计数，其背后是整个模不变的结构在起作用。