## 引言
在黎曼几何中，理解子流形如何嵌入或浸入到环境空间中是一个核心问题。仅仅依靠子流形自身的[内蕴曲率](@entry_id:161701)（如高斯曲率）不足以完全描述其几何形态，我们还需要量化它在外在空间中的“弯曲”方式。[平均曲率向量](@entry_id:199617)正是为了解决这一问题而生的关键概念，它为衡量[子流形](@entry_id:159439)的外在弯曲提供了一个简洁而深刻的[平均度](@entry_id:261638)量，成为连接[内蕴几何与外在几何](@entry_id:161677)的桥梁。

本文将系统地引导读者深入探索[平均曲率向量](@entry_id:199617)的理论与实践。在“**原理与机制**”一章中，我们将从第一性原理出发，通过高斯公式和第二基本形式严格定义[平均曲率向量](@entry_id:199617)，并探讨其与形算子的对偶关系、变分特征以及在[几何流](@entry_id:195216)中的作用。随后，在“**应用与跨学科联系**”一章中，我们将展示这一概念的强大生命力，考察它在[极小曲面](@entry_id:157732)理论、广义相对论、弦理论乃至现代[几何分析](@entry_id:157700)等前沿领域的具体应用。最后，通过“**动手实践**”部分，读者将有机会通过解决具体问题来巩固理论知识，并将抽象概念应用于实际计算中。通过这一结构化的学习路径，本文旨在为读者构建一个关于[平均曲率向量](@entry_id:199617)的完整知识体系。

## 原理与机制

本章旨在深入探讨[平均曲率向量](@entry_id:199617)的定义、几何意义及其在[子流形理论](@entry_id:190701)中的核心作用。我们将从[浸入子流形](@entry_id:264923)的基本结构出发，通过分解环境空间的协变导数，引出[第二基本形式](@entry_id:161454)，并将其迹定义为[平均曲率向量](@entry_id:199617)。随后，我们将探讨其对偶概念——形算子，并展示如何在不同余维情况下计算和理解平均曲率。最后，我们将揭示[平均曲率向量](@entry_id:199617)与[曲率张量](@entry_id:181383)、[面积泛函](@entry_id:635965)变分以及几何分析中重要概念（如[平均曲率流](@entry_id:184231)与和谐映射）之间的深刻联系。

### 高斯公式：[协变导数](@entry_id:152476)的分解

[黎曼几何](@entry_id:160508)中研究子流形 $(M, g)$ 在环境[流形](@entry_id:153038) $(N, \bar{g})$ 中的几何性质时，其核心思想是比较两种几何结构：$M$ 的[内蕴几何](@entry_id:158788)（由 $g$ 决定）和它作为 $N$ 的一部分所表现出的外在几何。这两种几何之间的联系，是通过分解 $N$ 上的列维-奇维塔联络 $\overline{\nabla}$ 来建立的。

设 $M$ 是 $N$ 的一个[浸入子流形](@entry_id:264923)。对于 $M$ 上的每一点 $p$，[切空间](@entry_id:199137) $T_pM$ 是 $T_pN$ 的一个[线性子空间](@entry_id:151815)。由于 $N$ 上的黎曼度规 $\bar{g}$ 在每个切空间上都定义了一个[内积](@entry_id:158127)，我们可以定义 $T_pM$ 在 $T_pN$ 中的正交补，即法空间 $N_pM$：
$$ N_pM = \{ v \in T_pN \mid \bar{g}_p(v,w)=0 \text{ for all } w \in T_pM \} $$
这就在每一点上给出了一个正交[直和分解](@entry_id:263004) $T_pN = T_pM \oplus N_pM$。当点 $p$ 在 $M$ 上变动时，这些法空间汇集在一起，形成一个光滑的向量丛，称为 $M$ 在 $N$ 中的**[法丛](@entry_id:272447)**（normal bundle），记作 $NM$。因此，限制在 $M$ 上的 $N$ 的切丛 $TN|_M$ 可以光滑地分解为 $M$ 的切丛 $TM$ 和[法丛](@entry_id:272447) $NM$ 的惠特尼和：$TN|_M = TM \oplus NM$。这一分解是研究外在几何的基石，它依赖于黎曼度规的存在，并非对所有子流形都成立的特殊性质。[@problem_id:3000930]

现在，考虑 $M$ 上的两个切向量场 $X, Y$。在环境[流形](@entry_id:153038) $N$ 中对它们求协变导数 $\overline{\nabla}_X Y$，其结果是 $TN|_M$ 的一个[截面](@entry_id:154995)，但它不一定与 $M$ 相切。利用上述的[正交分解](@entry_id:148020)，我们可以将 $\overline{\nabla}_X Y$ 分解为其切向分量和法向分量：
$$ \overline{\nabla}_X Y = (\overline{\nabla}_X Y)^\top + (\overline{\nabla}_X Y)^\perp $$
其中 $(\cdot)^\top$ 表示到 $TM$ 的[正交投影](@entry_id:144168)，$(\cdot)^\perp$ 表示到 $NM$ 的[正交投影](@entry_id:144168)。

令人惊奇的是，切向分量 $(\overline{\nabla}_X Y)^\top$ 恰好是 $M$ 上由[诱导度规](@entry_id:160616) $g$ 所唯一决定的列维-奇维塔联络。我们将其记为 $\nabla_X Y$。法向分量则定义了**[第二基本形式](@entry_id:161454)**（second fundamental form），记为 $\mathrm{II}(X,Y)$。这样，我们就得到了**高斯公式**（Gauss formula）：
$$ \overline{\nabla}_X Y = \nabla_X Y + \mathrm{II}(X,Y) $$
其中 $\mathrm{II}(X,Y) = (\overline{\nabla}_X Y)^\perp$。[@problem_id:3000904]

[第二基本形式](@entry_id:161454) $\mathrm{II}$ 是一个取值于[法丛](@entry_id:272447) $NM$ 的[对称双线性形式](@entry_id:148281)。它的对称性 $\mathrm{II}(X,Y) = \mathrm{II}(Y,X)$ 源于 $\overline{\nabla}$ 的无挠性。从几何上看，$\mathrm{II}(X,Y)$ 衡量了 $M$ 在 $N$ 中的弯曲程度。如果 $\mathrm{II}$ 在某点为零，意味着在该点附近 $M$ 与其切空间“无限接近”，几乎没有弯曲。如果 $\mathrm{II}$ 在 $M$ 上恒为零，我们称 $M$ 是**[全测地子流形](@entry_id:637049)**（totally geodesic submanifold）。在这种情况下，任何 $M$ 中的[测地线](@entry_id:269969)也是 $N$ 中的[测地线](@entry_id:269969)。

### [平均曲率向量](@entry_id:199617)的定义与几何意义

[第二基本形式](@entry_id:161454) $\mathrm{II}$ 包含了关于 $M$ 外在曲率的全部信息。为了从中提炼出一个简洁而有力的[不变量](@entry_id:148850)，我们取其关于度规 $g$ 的迹。

**[平均曲率向量](@entry_id:199617)**（mean curvature vector）$H$ 定义为[第二基本形式](@entry_id:161454)的迹：
$$ H = \mathrm{tr}_g(\mathrm{II}) = \sum_{i=1}^{m} \mathrm{II}(e_i, e_i) $$
其中 $\{e_1, \dots, e_m\}$ 是切空间 $T_pM$ 的任意一个 $g$-[标准正交基](@entry_id:147779)，$m = \dim M$。根据定义，$H$ 是一个[法向量场](@entry_id:268853)，即 $H \in \Gamma(NM)$。它代表了子流形在一点处所有切方向上弯曲的“平均值”。[@problem_id:3000904]

如果[平均曲率向量](@entry_id:199617)在 $M$ 上恒为零，即 $H \equiv 0$，则称 $M$ 为**[极小曲面](@entry_id:157732)**（minimal submanifold）。这个名称源于其变分性质，我们将在后面讨论。极小性是一个比全测地性弱得多的条件。例如，在 $\mathbb{R}^3$ 中，悬链面和[螺旋面](@entry_id:264087)都是极小曲面，但它们显然不是平面（全测地[曲面](@entry_id:267450)）。在这些[曲面](@entry_id:267450)上，$H=0$ 意味着[主曲率](@entry_id:270598)之和为零，但[主曲率](@entry_id:270598)自身未必为零，因此第二基本形式 $\mathrm{II}$ 不为零。[@problem_id:3000930]

### 对偶视角：形算子

除了通过对切向量场求导来研究[外在曲率](@entry_id:160405)，我们还可以考察[法向量场](@entry_id:268853)的变化，这为我们提供了对偶的视角。

考虑 $M$ 上的一个光滑[法向量场](@entry_id:268853) $\nu \in \Gamma(NM)$。当我们沿着 $M$ 上的一个切方向 $X$ 对 $\nu$ 求[协变导数](@entry_id:152476)时，$\overline{\nabla}_X \nu$ 同样可以分解为切向和法向分量。其切向分量定义了**形算子**（shape operator），也称**温加滕映射**（Weingarten map），记为 $S_\nu$：
$$ S_\nu(X) = -(\overline{\nabla}_X \nu)^\top $$
负号是一个重要的约定，它使得形算子与第二基本形式的关系更为简洁。这个关系可以通过对 $\bar{g}(Y, \nu) = 0$ 求导来建立。对于任意切向量场 $X, Y$，我们有：
$$ 0 = X(\bar{g}(Y, \nu)) = \bar{g}(\overline{\nabla}_X Y, \nu) + \bar{g}(Y, \overline{\nabla}_X \nu) $$
利用高斯公式和形算子的定义，上式变为：
$$ 0 = \bar{g}(\nabla_X Y + \mathrm{II}(X,Y), \nu) + \bar{g}(Y, -S_\nu(X) + (\overline{\nabla}_X \nu)^\perp) $$
由于 $\nabla_X Y$ 和 $S_\nu(X)$ 是切向的，而 $\mathrm{II}(X,Y)$ 和 $(\overline{\nabla}_X \nu)^\perp$ 是法向的，正交性使得上式简化为：
$$ 0 = \bar{g}(\mathrm{II}(X,Y), \nu) - \bar{g}(Y, S_\nu(X)) $$
于是我们得到了[第二基本形式](@entry_id:161454)与形算子之间的基本对偶关系：
$$ \bar{g}(\mathrm{II}(X,Y), \nu) = g(S_\nu(X), Y) $$
这个恒等式表明，知道了所有法方向上的形算子，就等价于知道了[第二基本形式](@entry_id:161454)。利用 $\mathrm{II}$ 的对称性和 $g$ 的对称性，可以证明 $S_\nu$ 是一个关于度规 $g$ 的自伴算子，即 $g(S_\nu(X), Y) = g(X, S_\nu(Y))$。[@problem_id:3000930]

### [平均曲率](@entry_id:162147)的表征与计算

借助形算子，我们可以更具体地刻画[平均曲率向量](@entry_id:199617)。

#### [余维](@entry_id:273141)为1的情形：超曲面
当 $M^m$ 是 $N^{m+1}$ 中的[超曲面](@entry_id:159491)时，[法丛](@entry_id:272447) $NM$ 是一维的。我们可以选取一个[单位法向量](@entry_id:178851)场 $\nu$。此时，第二基本形式可以完全由一个标量函数和 $\nu$ 描述，$\mathrm{II}(X,Y) = h(X,Y)\nu$，其中 $h(X,Y) = g(S_\nu(X),Y)$ 是标量[第二基本形式](@entry_id:161454)。[平均曲率向量](@entry_id:199617) $H$ 也必然平行于 $\nu$：
$$ H = H_{\text{scalar}} \nu $$
其中 $H_{\text{scalar}}$ 是一个标量函数，称为**标量[平均曲率](@entry_id:162147)**。根据定义，我们有：
$$ H = \sum_{i=1}^m \mathrm{II}(e_i, e_i) = \left( \sum_{i=1}^m g(S_\nu(e_i), e_i) \right) \nu = (\mathrm{tr}_g S_\nu) \nu $$
因此，对于[超曲面](@entry_id:159491)，$H_{\text{scalar}} = \mathrm{tr}_g(S_\nu)$。

符号约定在此处至关重要。如果我们反转[法向量](@entry_id:264185)的选择，即令 $\tilde{\nu} = -\nu$，那么新的形算子 $\tilde{S}_{\tilde{\nu}} = -(\overline{\nabla}_X(-\nu))^\top = -S_\nu$。因此，标量[平均曲率](@entry_id:162147)变号：$\tilde{H}_{\text{scalar}} = \mathrm{tr}(\tilde{S}_{\tilde{\nu}}) = -\mathrm{tr}(S_\nu) = -H_{\text{scalar}}$。然而，[平均曲率向量](@entry_id:199617)本身保持不变：
$$ \tilde{H} = \tilde{H}_{\text{scalar}} \tilde{\nu} = (-H_{\text{scalar}})(-\nu) = H_{\text{scalar}} \nu = H $$
[平均曲率向量](@entry_id:199617)是一个不依赖于[法向量](@entry_id:264185)方向选择的几何量。

以 $\mathbb{R}^{n+1}$ 中的球面 $S^n(r)$ 为例，若选取向外的[单位法向量](@entry_id:178851) $\nu_{\text{out}}$，其形算子为 $S_{\nu_{\text{out}}}(X) = -\frac{1}{r}X$。因此，标量[平均曲率](@entry_id:162147)是 $H_{\text{scalar}} = \mathrm{tr}(-\frac{1}{r} I) = -\frac{n}{r}$。[平均曲率向量](@entry_id:199617)为 $H = (-\frac{n}{r})\nu_{\text{out}}$，它指向球心，即指向[曲面](@entry_id:267450)的“凹”侧。[@problem_id:3000915]

#### 高[余维](@entry_id:273141)情形
当[余维数](@entry_id:273141) $k > 1$ 时，$H$ 是一个真正的向量。设 $\{\nu_1, \dots, \nu_k\}$ 是[法丛](@entry_id:272447) $NM$ 的一个局部[标准正交标架](@entry_id:189702)。$H$ 可以分解为：
$$ H = \sum_{\alpha=1}^k \bar{g}(H, \nu_\alpha) \nu_\alpha $$
利用对偶关系，我们可以计算其分量：
$$ \bar{g}(H, \nu_\alpha) = \bar{g}\left(\sum_{i=1}^m \mathrm{II}(e_i, e_i), \nu_\alpha\right) = \sum_{i=1}^m \bar{g}(\mathrm{II}(e_i, e_i), \nu_\alpha) = \sum_{i=1}^m g(S_{\nu_\alpha}(e_i), e_i) = \mathrm{tr}_g(S_{\nu_\alpha}) $$
因此，[平均曲率向量](@entry_id:199617)可以表示为各个法方向上形算子[迹的线性](@entry_id:199170)组合：
$$ H = \sum_{\alpha=1}^k (\mathrm{tr}_g S_{\nu_\alpha}) \nu_\alpha $$
这清晰地展示了 $H$ 作为向量的本质。每个分量 $\mathrm{tr}_g S_{\nu_\alpha}$ 是在 $\nu_\alpha$ 方向上的主曲率之和，它衡量了 $M$ 在该法方向上的平均弯曲程度。[@problem_id:3000926]

#### 坐标表示
对于 $\mathbb{R}^3$ 中的一个[参数曲面](@entry_id:273105) $F(u,v)$，平均曲率有经典的坐标表达式。设[第一基本形式](@entry_id:274022)的系数为 $E, F, G$，[第二基本形式](@entry_id:161454)的系数为 $e, f, g$（相对于[单位法向量](@entry_id:178851) $\mathbf{N}$）。形算子 $S_\mathbf{N}$ 在基 $\{F_u, F_v\}$ 下的矩阵为 $I^{-1}II = \begin{pmatrix} E  F \\ F  G \end{pmatrix}^{-1} \begin{pmatrix} e  f \\ f  g \end{pmatrix}$。其迹为：
$$ H_{\text{scalar}} = \mathrm{tr}(S_\mathbf{N}) = \frac{Eg - 2Ff + Ge}{EG - F^2} $$
因此，[平均曲率向量](@entry_id:199617)为 $H = \left( \frac{Eg - 2Ff + Ge}{EG - F^2} \right) \mathbf{N}$。注意，此处的 $H_{\text{scalar}}$ 是形[算子的迹](@entry_id:185149)，即[主曲率](@entry_id:270598)之和 $k_1+k_2$。在一些经典文献中，平均曲率常定义为[主曲率](@entry_id:270598)的平均值 $\frac{1}{2}(k_1+k_2)$，这会导致公式中出现一个额外的因子 $\frac{1}{2}$。[@problem_id:3000910]

### 曲率关系：[高斯绝妙定理](@entry_id:159067)的延伸

第二基本形式不仅定义了平均曲率，它还充当了[内蕴曲率与外在曲率](@entry_id:192678)之间的桥梁。**[高斯方程](@entry_id:192573)**（Gauss equation）精确地描述了这一关系。对于 $M$ 上的任意切向量场 $X,Y,Z,W$，我们有：
$$ g(R^M(X,Y)Z, W) = \bar{g}(R^N(X,Y)Z, W) + \bar{g}(\mathrm{II}(X,W), \mathrm{II}(Y,Z)) - \bar{g}(\mathrm{II}(X,Z), \mathrm{II}(Y,W)) $$
其中 $R^M$ 和 $R^N$ 分别是 $M$ 和 $N$ 的黎曼曲率张量。[@problem_id:3000906]

该方程表明，$M$ 的[内蕴曲率](@entry_id:161701)（左侧）由两部分构成：一部分来自[环境空间](@entry_id:184743) $N$ 的曲率（右侧第一项），另一部分完全由[第二基本形式](@entry_id:161454)决定（右侧后两项），即纯粹的[外在曲率](@entry_id:160405)贡献。

一个特别重要的例子是 $M^2 \subset \mathbb{R}^3$。此时环境空间是平坦的（$R^N=0$）。[高斯方程](@entry_id:192573)简化后可得到著名的**[高斯绝妙定理](@entry_id:159067)**（Theorema Egregium）：$M$ 的高斯曲率 $K$ 完全由其[第一基本形式](@entry_id:274022)决定。用外在几何的语言，它也可以表示为形算子的[行列式](@entry_id:142978)：
$$ K = \det(S_\nu) = k_1 k_2 $$
这与标量[平均曲率](@entry_id:162147)形成鲜明对比：
$$ H_{\text{scalar}} = \mathrm{tr}(S_\nu) = k_1 + k_2 $$
[高斯曲率](@entry_id:149725)是内蕴的，即使把[曲面](@entry_id:267450)“弯曲”而不“拉伸”（即保持度规），$K$ 也不会改变。而平均曲率是外在的，它会随着[曲面](@entry_id:267450)在空间中的弯曲方式而改变。[@problem_id:3000918]

### 变分表征与[几何流](@entry_id:195216)

[平均曲率向量](@entry_id:199617)最深刻的几何意义之一在于它与[面积泛函](@entry_id:635965)的关系。考虑一个[浸入](@entry_id:161534) $F: M \to N$，其面积为 $\mathcal{A}(F) = \int_M d\mu_g$。如果我们对[浸入](@entry_id:161534)做一个微小的扰动，生成一族[浸入](@entry_id:161534) $F_t$，其在 $t=0$ 处的变分向量场为 $V = \frac{\partial F_t}{\partial t}|_{t=0}$，那么面积的一阶变分为：
$$ \frac{d}{dt}\bigg|_{t=0} \mathcal{A}(F_t) = - \int_M \bar{g}(H, V) \, d\mu_g $$
这个公式表明，[平均曲率向量](@entry_id:199617) $H$ 是[面积泛函](@entry_id:635965)在 $L^2$ [内积](@entry_id:158127)下的“负梯度”的法向部分。更准确地说，由于面积在切向变分（重参数化）下不变，其梯度必然是法向的。在[法向量场](@entry_id:268853)的 $L^2$ [内积](@entry_id:158127)下，[面积泛函](@entry_id:635965)的梯度就是 $-H$。[@problem_id:3000915] [@problem_id:3000922]

因此，极小曲面（$H=0$）正是[面积泛函](@entry_id:635965)的[临界点](@entry_id:144653)。它们就像是无限维[浸入](@entry_id:161534)空间中的“山峰、山谷或[鞍点](@entry_id:142576)”。

如果 $M$ 有边界 $\partial M$，一阶变分公式会多出一个边界项：
$$ \frac{d}{dt}\bigg|_{t=0} \mathcal{A}(F_t) = - \int_M \bar{g}(H, V) \, d\mu_g + \int_{\partial M} g(V, \eta) \, ds $$
其中 $\eta$ 是 $\partial M$ 在 $M$ 中的单位外[法向量](@entry_id:264185)（共[法向量](@entry_id:264185)）。这个边界项衡量了边界移动对面积的贡献。例如，对于 $\mathbb{R}^3$ 中的一个[单位圆盘](@entry_id:172324)（$H=0$），如果用径向扩张的向量场 $V(x)=x$ 去变分，面积的变化完全来自于边界的拉伸，其变化率为 $2\pi$。[@problem_id:3000907]

利用平均曲率是面积“最陡下降方向”这一思想，可以定义**[平均曲率流](@entry_id:184231)**（Mean Curvature Flow），这是一个[几何演化方程](@entry_id:636858)：
$$ \frac{\partial F_t}{\partial t} = H(F_t) $$
在此流动下，[子流形](@entry_id:159439) $M_t = F_t(M)$ 的每一点都沿着其[平均曲率向量](@entry_id:199617)的方向移动。这是[面积泛函](@entry_id:635965)的负梯度流。根据变分公式，面积的变化率为：
$$ \frac{d}{dt} \mathcal{A}(F_t) = - \int_M \|H\|^2 \, d\mu_g \le 0 $$
这意味着面积会以最快的速度减小，使得[曲面](@entry_id:267450)趋向于“平滑”和“简化”，最终（在理想情况下）收缩为一个点。这个过程是[几何分析](@entry_id:157700)中的一个核心研究对象。[@problem_id:3000922]

### 高阶性质：平行平均曲率与和谐性

除了[平均曲率](@entry_id:162147)本身，其协变导数 $\nabla^\perp H$ 也蕴含着重要的几何信息。如果 $\nabla^\perp H = 0$，我们称该[子流形](@entry_id:159439)具有**平行[平均曲率向量](@entry_id:199617)**。

对于浸入到[欧氏空间](@entry_id:138052) $F: M \to \mathbb{R}^{m+k}$，这个条件与[子流形](@entry_id:159439)的**[高斯映射](@entry_id:260784)**（Gauss map）$\gamma: M \to G_m(\mathbb{R}^{m+k})$ 的性质密切相关。[高斯映射](@entry_id:260784)将 $M$ 上的每一点 $p$ 映到其切空间 $T_pM$ 所代表的格拉斯曼[流形](@entry_id:153038)中的一个点。**Ruh-Vilms 定理**指出，[高斯映射](@entry_id:260784) $\gamma$ 是一个和谐映射（harmonic map）当且仅当 $M$ 具有平行[平均曲率向量](@entry_id:199617)。[@problem_id:3000893]

和谐映射是[能量泛函](@entry_id:170311)（或[狄利克雷能量](@entry_id:276589)）的[临界点](@entry_id:144653)，是[测地线](@entry_id:269969)概念到映射的推广。因此，Ruh-Vilms 定理揭示了[平均曲率](@entry_id:162147)的又一深刻变分意义。

这一结论有几个直接推论：
1.  任何[极小曲面](@entry_id:157732)（$H=0$）都具有平行[平均曲率向量](@entry_id:199617)，因此其[高斯映射](@entry_id:260784)是和谐的。
2.  对于[欧氏空间](@entry_id:138052)中的超曲面，$\nabla^\perp H = 0$ 等价于其标量平均曲率 $H_{\text{scalar}}$ 为常数。这类[曲面](@entry_id:267450)被称为**[常平均曲率](@entry_id:194008)**（Constant Mean Curvature, CMC）[曲面](@entry_id:267450)。因此，CMC [超曲面](@entry_id:159491)的[高斯映射](@entry_id:260784)是和谐的。
3.  需要注意的是，“平行[平均曲率向量](@entry_id:199617)”是一个比“平行[第二基本形式](@entry_id:161454)”（$\nabla \mathrm{II}=0$）弱得多的条件。后者要求第二基本形式的所有分量都不变，是一个非常刚性的条件，而前者只要求其迹（平均值）平行。[@problem_id:3000893]

最后，值得强调的是，Ruh-Vilms 定理在弯曲的环境[流形](@entry_id:153038)中一般不成立，因为环境空间的曲率会为[高斯映射](@entry_id:260784)的[张力场](@entry_id:188540)贡献一个附加项，从而打破 $\nabla^\perp H=0$ 与和谐性之间的等价关系。[@problem_id:3000893]