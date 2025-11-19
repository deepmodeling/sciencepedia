## 引言
[实二次域](@entry_id:636720)中的单位是[代数数论](@entry_id:148067)的核心研究对象之一，其结构和性质深刻地影响着数域的算术特性。理解这些乘法可[逆元](@entry_id:140790)不仅是理论上的追求，更是解决一系列经典数学问题（如[佩尔方程](@entry_id:136532)）的关键。然而，抽象的代数定义与具体的计算方法之间存在着知识鸿沟，同时，单位这一概念与其他数学领域的深层联系也往往不为人所知。本文旨在系统地填补这一鸿沟，引领读者深入探索[实二次域](@entry_id:636720)单位的完整图景。

在接下来的章节中，我们将首先在“原理与机制”一章中，从[狄利克雷单位定理](@entry_id:155550)出发，奠定[单位群](@entry_id:184012)的理论基础，并探讨其几何诠释与计算方法。随后，在“应用与跨学科联系”一章，我们将展示这些原理如何应用于[求解丢番图方程](@entry_id:149511)、影响类[群结构](@entry_id:146855)，并延伸至[解析数论](@entry_id:158402)和[双曲几何](@entry_id:158454)等领域。最后，“动手实践”部分将通过具体的计算问题，帮助读者巩固所学知识，将理论应用于实践。通过这一结构化的学习路径，读者将全面掌握[实二次域](@entry_id:636720)中单位的理论、计算与应用。

## 原理与机制

本章旨在深入探讨[实二次域](@entry_id:636720)中单位的[代数结构](@entry_id:137052)、几何表示、计算方法及其在数论中的深刻应用。在前一章介绍背景知识的基础上，我们将系统地阐述单位群的原理与机制，从[狄利克雷单位定理](@entry_id:155550)的抽象结构出发，过渡到[对数嵌入](@entry_id:148678)下的几何图像，再到与[佩尔方程](@entry_id:136532)和[连分数](@entry_id:264019)的具体计算联系，最后探讨其范数对[理想类群](@entry_id:153974)结构的影响。

### [单位群](@entry_id:184012)的结构：[狄利克雷单位定理](@entry_id:155550)

在任意[数域](@entry_id:155558) $K$ 中，其整数环 $\mathcal{O}_K$ 的一个**单位**（unit）是指一个元素 $u \in \mathcal{O}_K$，其乘法[逆元](@entry_id:140790) $u^{-1}$ 也存在于 $\mathcal{O}_K$ 中。所有单位构成一个[乘法群](@entry_id:155975)，称为 **[单位群](@entry_id:184012)**（unit group），记作 $\mathcal{O}_K^\times$。一个[代数整数](@entry_id:151672)是单位的一个等价判别准则，是其在 $K/\mathbb{Q}$ 上的范数 $N_{K/\mathbb{Q}}(u)$ 是 $\mathbb{Z}$ 中的单位，即 $N_{K/ \mathbb{Q}}(u) = \pm 1$ [@problem_id:3014839]。

对于[实二次域](@entry_id:636720) $K = \mathbb{Q}(\sqrt{d})$（其中 $d>0$ 为无平方因子整数），其单位群的结构由著名的 **[狄利克雷单位定理](@entry_id:155550)**（Dirichlet's Unit Theorem）精确描述。该定理指出，对于一个有 $r_1$ 个实嵌入和 $r_2$ 对共轭[复嵌入](@entry_id:189961)的数域，其[单位群的秩](@entry_id:150706)为 $r = r_1 + r_2 - 1$。[实二次域](@entry_id:636720)有两个实嵌入（$r_1=2$）而没有[复嵌入](@entry_id:189961)（$r_2=0$），因此其[单位群的秩](@entry_id:150706)为 $r=2+0-1=1$。

具体而言，$\mathcal{O}_K^\times$ 的结构是[有限循环群](@entry_id:147298)与一个[无限循环群](@entry_id:139160)的[直积](@entry_id:143046)。这个结构可以表示为：
$$ \mathcal{O}_K^\times \cong \mu_K \times \mathbb{Z} $$
其中 $\mu_K$ 是 $K$ 中所有[单位根](@entry_id:143302)构成的**[挠子群](@entry_id:139454)**（torsion subgroup）[@problem_id:3029638]。对于任何实域，包括[实二次域](@entry_id:636720)，其包含的[单位根](@entry_id:143302)仅有 $\{+1, -1\}$。因此，对于 $K=\mathbb{Q}(\sqrt{d})$，我们有：
$$ \mathcal{O}_K^\times \cong \{\pm 1\} \times \mathbb{Z} $$
无限循环部分 $\mathbb{Z}$ 由一个生成元生成。我们可以选择这个生成元 $\varepsilon > 1$，并称之为**[基本单位](@entry_id:148878)**（fundamental unit）。这意味着 $K$ 中的任何单位 $u$ 都可以唯一地表示为 $u = \pm \varepsilon^n$ 的形式，其中 $n$ 是某个整数 [@problem_id:3014839] [@problem_id:3030739]。[基本单位](@entry_id:148878)的存在是[实二次域](@entry_id:636720)算术理论的基石。

### 几何诠释：[对数嵌入](@entry_id:148678)与正则子

[狄利克雷单位定理](@entry_id:155550)的证明及其几何直觉，源于将[单位群](@entry_id:184012)嵌入到一个实[向量空间](@entry_id:151108)中。对于[实二次域](@entry_id:636720) $K = \mathbb{Q}(\sqrt{d})$，它有两个实嵌入 $\sigma_1, \sigma_2: K \hookrightarrow \mathbb{R}$，通常定义为 $\sigma_1(a+b\sqrt{d}) = a+b\sqrt{d}$ 和 $\sigma_2(a+b\sqrt{d}) = a-b\sqrt{d}$。

我们可以定义一个**[对数嵌入](@entry_id:148678)**（logarithmic embedding）映射 $L$:
$$ L: \mathcal{O}_K^\times \longrightarrow \mathbb{R}^2, \qquad u \longmapsto (\log|\sigma_1(u)|, \log|\sigma_2(u)|) $$
这个映射是一个从[乘法群](@entry_id:155975) $\mathcal{O}_K^\times$ 到[加法群](@entry_id:151801) $\mathbb{R}^2$ 的[群同态](@entry_id:140603)。对于任何单位 $u$，其范数 $N(u) = \sigma_1(u)\sigma_2(u) = \pm 1$，因此 $|N(u)| = |\sigma_1(u)||\sigma_2(u)| = 1$。对该式取对数，我们得到：
$$ \log|\sigma_1(u)| + \log|\sigma_2(u)| = \log(1) = 0 $$
这表明，所有单位在[对数嵌入](@entry_id:148678)下的像都位于 $\mathbb{R}^2$ 中由方程 $x_1+x_2=0$ 定义的超平面（在此为一条直线）$H$ 上 [@problem_id:3030808]。

根据[狄利克雷单位定理](@entry_id:155550)，$\mathcal{O}_K^\times$ 的[挠子群](@entry_id:139454) $\{\pm 1\}$ 在 $L$ 映射下都映为原点 $(0,0)$。而自由部分由基本单位 $\varepsilon$ 生成，其在 $L$ 下的像是 $L(\varepsilon)$。由于 $L$ 是同态，$\mathcal{O}_K^\times$ 的像 $L(\mathcal{O}_K^\times)$ 是由向量 $L(\varepsilon)$ 生成的 $\mathbb{R}^2$ 中的一个 **秩为1的格**（rank-1 lattice）[@problem_id:3030724]。

我们可以具体计算这个生成向量。按惯例取 $\varepsilon > 1$，并设 $\sigma_1$ 为恒等嵌入，则 $|\sigma_1(\varepsilon)| = \varepsilon$。由 $|\sigma_1(\varepsilon)||\sigma_2(\varepsilon)|=1$ 可得 $|\sigma_2(\varepsilon)| = 1/\varepsilon$。因此，格的生成元是：
$$ L(\varepsilon) = (\log\varepsilon, \log(1/\varepsilon)) = (\log\varepsilon, -\log\varepsilon) $$
这个向量确实位于直线 $x_1+x_2=0$ 上。

这个几何图像引出了**正则子**（regulator）$R_K$ 的概念，它衡量了[单位群](@entry_id:184012)在对数空间中所占“体积”的大小。根据一般定义，对于秩为 $r=1$ 的情况，正则子是 $1 \times 1$ 矩阵 $[\log|\sigma_i(\varepsilon)|]$ [行列式](@entry_id:142978)的[绝对值](@entry_id:147688)，其中 $\sigma_i$ 是任选的一个嵌入 [@problem_id:3030739]。
- 若选择 $\sigma_1$，矩阵为 $[\log|\sigma_1(\varepsilon)|] = [\log\varepsilon]$，其[行列式](@entry_id:142978)为 $\log\varepsilon$。
- 若选择 $\sigma_2$，矩阵为 $[\log|\sigma_2(\varepsilon)|] = [-\log\varepsilon]$，其[行列式](@entry_id:142978)为 $-\log\varepsilon$。
取[绝对值](@entry_id:147688)后，两种选择都得到相同的结果。因为我们选择 $\varepsilon > 1$，所以 $\log\varepsilon > 0$。因此，[实二次域](@entry_id:636720)的正则子就是：
$$ R_K = \log\varepsilon $$
从几何上看，$R_K$ 是格 $L(\mathcal{O}_K^\times)$ 在超平面 $H$ 中的[协体积](@entry_id:186549)（covolume）。[协体积](@entry_id:186549)的定义依赖于 $H$ 上的测度。若将 $H$ 通过投影（例如，$(x_1, x_2) \mapsto x_1$）与 $\mathbb{R}$ 等同，则[协体积](@entry_id:186549)就是生成元 $L(\varepsilon)$ 在该投影下的长度，即 $|\log\varepsilon| = \log\varepsilon$。这正是正则子的标准定义 [@problem_id:3030746]。需要注意的是，如果在 $H$ 上使用由 $\mathbb{R}^2$ 诱导的欧几里得长度测度，那么[协体积](@entry_id:186549)（即生成元的欧几里得长度）将是 $\|(\log\varepsilon, -\log\varepsilon)\| = \sqrt{(\log\varepsilon)^2 + (-\log\varepsilon)^2} = \sqrt{2}\log\varepsilon = \sqrt{2}R_K$ [@problem_id:3030746]。

### 单位与丢番图方程：[佩尔方程](@entry_id:136532)

寻找单位的充要条件 $N(u)=\pm 1$ 自然地将问题转化求解一个[丢番图方程](@entry_id:148433)。该方程的具体形式取决于 $\mathcal{O}_K$ 的结构，即取决于 $d \pmod 4$ 的值。

#### 情形一：$d \equiv 2, 3 \pmod 4$

此时，[整数环](@entry_id:181003)是 $\mathcal{O}_K = \mathbb{Z}[\sqrt{d}]$。环中任意元素形如 $x+y\sqrt{d}$，其中 $x, y \in \mathbb{Z}$。其范数为 $N(x+y\sqrt{d}) = x^2 - dy^2$。因此，$\mathcal{O}_K$ 中的单位与著名的**[佩尔方程](@entry_id:136532)**（Pell's equation）的整数解一一对应：
$$ x^2 - dy^2 = \pm 1 $$
每一个整数解 $(x,y)$ 都给出一个单位 $u=x+y\sqrt{d}$ [@problem_id:3030786] [@problem_id:3014839]。

#### 情形二：$d \equiv 1 \pmod 4$

此时，整数环是 $\mathcal{O}_K = \mathbb{Z}\left[\frac{1+\sqrt{d}}{2}\right]$。环中任意元素可以写成 $\frac{x+y\sqrt{d}}{2}$ 的形式，其中 $x, y \in \mathbb{Z}$ 且必须满足奇偶性相同的条件，即 $x \equiv y \pmod 2$。其范数为 $N\left(\frac{x+y\sqrt{d}}{2}\right) = \frac{x^2 - dy^2}{4}$。因此，单位对应于满足以下条件的整数解 $(x,y)$：
$$ x^2 - dy^2 = \pm 4, \quad \text{其中 } x \equiv y \pmod 2 $$
这种形式的方程有时被称为广义[佩尔方程](@entry_id:136532)。需要强调的是，在这种情况下，仅仅考虑 $x^2-dy^2=\pm 1$ 的解会遗漏掉那些分母为2的“非显然”单位，例如在 $\mathbb{Q}(\sqrt{5})$ 中，基本单位是 $\varepsilon=\frac{1+\sqrt{5}}{2}$，它来自于 $1^2-5(1^2)=-4$ [@problem_id:3030786]。

[基本单位](@entry_id:148878) $\varepsilon$ 本身作为一个[代数整数](@entry_id:151672)，满足一个以有理数为系数的极小多项式。由于 $\varepsilon \notin \mathbb{Q}$，这是一个二次多项式：$x^2 - T x + N = 0$，其中 $T = \mathrm{Tr}_{K/\mathbb{Q}}(\varepsilon) = \varepsilon + \sigma_2(\varepsilon)$ 是迹， $N = N_{K/\mathbb{Q}}(\varepsilon) = \varepsilon\sigma_2(\varepsilon)$ 是范数。$T$ 和 $N$ 都是整数，且 $N = \pm 1$ [@problem_id:3030777]。这些系数与佩尔型方程的解直接相关。例如，若 $\varepsilon = \frac{u+v\sqrt{d}}{2}$，则其迹为 $T=u$，范数为 $N=\frac{u^2-dv^2}{4}$。由此可得一个重要关系式，即该极小[多项式的判别式](@entry_id:148721) $T^2-4N = (u)^2 - 4(\frac{u^2-dv^2}{4}) = v^2d$ [@problem_id:3030777]。

### 寻找基本单位：[连分数](@entry_id:264019)方法

尽管我们已经建立了单位与[佩尔方程](@entry_id:136532)解之间的联系，但如何有效地找到这些解，特别是给出基本单位的最小解，仍然是一个挑战。**[连分数](@entry_id:264019)**（continued fraction）算法为此提供了一个强大而系统的工具。

对于任意无理数 $\sqrt{d}$，其[简单连分数](@entry_id:634874)展开是最终周期性的，形式为 $[a_0; \overline{a_1, a_2, \ldots, a_\ell}]$，其中 $\ell$ 是周期长度。该展开的第 $k$ 个**渐近分式**（convergent）$p_k/q_k$ 逼近 $\sqrt{d}$。一个关键的定理指出，对于周期为 $\ell$ 的[连分数展开](@entry_id:636208)，在周期结束前的最后一个渐近分式 $p_{\ell-1}/q_{\ell-1}$ 满足：
$$ p_{\ell-1}^2 - d q_{\ell-1}^2 = (-1)^\ell $$
这表明元素 $\eta = p_{\ell-1} + q_{\ell-1}\sqrt{d}$ 是一个范数为 $(-1)^\ell$ 的单位。事实上，$\eta$ 正是序 $\mathbb{Z}[\sqrt{d}]$ 的基本单位。

我们通过一个例子来说明这个过程。考虑 $K=\mathbb{Q}(\sqrt{14})$ [@problem_id:3029612]。
1.  **计算连分数**：$\sqrt{14}$ 的[连分数展开](@entry_id:636208)可以通过标准算法得到，其系数序列为 $a_0=3, a_1=1, a_2=2, a_3=1, a_4=6, \ldots$。我们发现这个序列从 $a_1$ 开始以长度 $\ell=4$ 为周期重复：$\sqrt{14} = [3; \overline{1, 2, 1, 6}]$。
2.  **寻找单位**：由于周期 $\ell=4$ 是偶数，我们知道 $p_{4-1}^2 - 14q_{4-1}^2 = p_3^2 - 14q_3^2 = (-1)^4 = 1$。我们计算第3个渐近分式 $p_3/q_3$。
    - $p_0/q_0 = 3/1$
    - $p_1/q_1 = 4/1$
    - $p_2/q_2 = 11/3$
    - $p_3/q_3 = 15/4$
    因此，$(x,y)=(15,4)$ 是方程 $x^2-14y^2=1$ 的一个解。
3.  **确定[基本单位](@entry_id:148878)**：由于 $14 \equiv 2 \pmod 4$，$\mathcal{O}_K = \mathbb{Z}[\sqrt{14}]$。我们找到的单位 $\varepsilon = 15+4\sqrt{14}$ 是 $\mathcal{O}_K$ 中的一个单位。可以证明，由[连分数算法](@entry_id:146381)找到的第一个范数为 $\pm 1$ 的解总是给出了基本单位（或者在范数为-1时，给出基本单位的平方）。因此，$15+4\sqrt{14}$ 是 $\mathbb{Q}(\sqrt{14})$ 的[基本单位](@entry_id:148878) [@problem_id:3029612]。

需要注意的是，当 $d \equiv 1 \pmod 4$ 时，由 $p_{\ell-1}^2-dq_{\ell-1}^2=\pm 1$ 得到的单位 $\eta = p_{\ell-1} + q_{\ell-1}\sqrt{d}$ 是序 $\mathbb{Z}[\sqrt{d}]$ 的基本单位，但不一定是最大序 $\mathcal{O}_K$ 的基本单位 $\varepsilon$。有时 $\eta$ 可能是 $\varepsilon$ 的某个幂次。例如，对于 $d=17 \equiv 1 \pmod 4$，$\sqrt{17}=[4;\overline{8}]$，周期 $\ell=1$。$p_0=4, q_0=1$ 给出 $4^2-17(1^2)=-1$，因此 $\varepsilon=4+\sqrt{17}$ 是一个范数为-1的单位。在这种情况下，它就是 $\mathcal{O}_K$ 的基本单位。它的平方 $\varepsilon^2 = (4+\sqrt{17})^2 = 33+8\sqrt{17}$ 是范数为+1的最小单位 [@problem_id:3030694]。

### [基本单位](@entry_id:148878)的范数及其推论

[基本单位](@entry_id:148878) $\varepsilon$ 的范数是 $+1$ 还是 $-1$，这是一个至关重要的问题，它不仅决定了[佩尔方程](@entry_id:136532) $x^2-dy^2=-1$ 是否有解，还对更高等的[代数结构](@entry_id:137052)（如窄[类群](@entry_id:182524)）有深刻影响。

一个深刻的定理将[基本单位](@entry_id:148878)的范数与 $\sqrt{d}$ 的[连分数](@entry_id:264019)周期长度 $\ell(d)$ 联系起来：
$$ N_{K/\mathbb{Q}}(\varepsilon) = -1 \iff \ell(d) \text{ 是奇数} $$
等价地，总有 $N_{K/\mathbb{Q}}(\varepsilon) = (-1)^{\ell(d)}$ [@problem_id:3030774]。因此，通过计算连分数周期长度的奇偶性，我们就可以判定是否存在范数为 $-1$ 的单位。

这个性质最引人注目的应用之一是它与**窄类群**（narrow class group）$\mathrm{Cl}^+(K)$ 的关系。窄类群的定义与普通理想类群 $\mathrm{Cl}(K)$ 类似，但它在等价关系上要求更严：两个理想等价，当且仅当它们的商是由一个**全正元素**（totally positive element，即在两个实嵌入下均为正的元素）生成的。

普通[类群](@entry_id:182524)与窄[类群](@entry_id:182524)之间的关系由以下精确准则决定 [@problem_id:3030701]：
- 如果 $K$ 中存在范数为 $-1$ 的单位（即 $N(\varepsilon)=-1$），则 $\mathrm{Cl}^+(K) \cong \mathrm{Cl}(K)$。
- 如果 $K$ 中不存在范数为 $-1$ 的单位（即所有单位的范数均为 $+1$），则 $|\mathrm{Cl}^+(K)| = 2|\mathrm{Cl}(K)|$。

其背后的机制是：如果存在一个范数为 $-1$ 的单位 $u$，那么它的两个嵌入值必定异号（例如 $\sigma_1(u)>0, \sigma_2(u)<0$）。对于任何主理想 $(\alpha)$，如果其生成元 $\alpha$ 不是全正的，我们可以通过乘以 $u$ 或 $-u$ 来调整其嵌入的符号，从而找到一个全正的生成元。例如，若 $\sigma_1(\alpha)>0, \sigma_2(\alpha)<0$，那么 $\alpha u$ 的嵌入符号为 $(\sigma_1(\alpha)\sigma_1(u), \sigma_2(\alpha)\sigma_2(u)) = (+ \cdot +, - \cdot -) = (+,+)$，因此 $\alpha u$ 是一个全正的生成元。这意味着每个[主理想](@entry_id:152760)都有一个全正生成元，故 $P_K = P_K^+$，两个类群等同 [@problem_id:3030701] [@problem_id:3030786]。反之，若不存在范数为 $-1$ 的单位，则无法改变嵌入值的符号组合，由全正元素生成的[主理想](@entry_id:152760)群 $P_K^+$ 成为所有[主理想](@entry_id:152760)群 $P_K$ 的一个指数为2的[真子群](@entry_id:141915)，导致窄类群的阶数是普通[类群](@entry_id:182524)的两倍 [@problem_id:3030774]。