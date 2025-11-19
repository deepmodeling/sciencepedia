## 应用与跨学科联系

在前面的章节中，我们已经阐述了Langlands纲领的核心原理，特别是[函子性](@entry_id:150069)原理。该原理预言了不同约化群上的[自守表示](@entry_id:181931)之间应存在深刻的联系，这种联系由它们L-群之间的同态所支配。本章旨在展示这些抽象原理的巨大威力，探讨它们如何在具体的数学问题中被应用，并揭示它们如何将数论的不同分支（如[模形式](@entry_id:160014)、Galois表示、[算术几何](@entry_id:189136)）与表示论和分析数论紧密地联系在一起。我们的目标不是重复理论，而是通过一系列关键应用来展示[函子性](@entry_id:150069)原理的效用、延伸及其在解决重大问题中的核心地位。

### [函子性](@entry_id:150069)提升的具体实例

[函子性](@entry_id:150069)原理最直接的体现是“[函子性](@entry_id:150069)提升”（functorial lift），即从一个群上的[自守表示](@entry_id:181931)构造出另一个群上的[自守表示](@entry_id:181931)。这些提升构成了Langlands纲领的骨架，其具体实例为了解其运作机制提供了最清晰的窗口。

#### 基变更

基变更（Base Change）是最早被深入研究且最为基础的[函子性](@entry_id:150069)提升之一。它涉及将一个[数域](@entry_id:155558) $F$ 上的[自守表示](@entry_id:181931)提升到一个扩域 $E/F$ 上。在Galois方面，域的扩张 $F \hookrightarrow E$ 诱导了Weil群的限制映射 $W_E \to W_F$。[函子性](@entry_id:150069)原理预言，给定 $\mathrm{GL}_n(\mathbb{A}_F)$ 上的一个[自守表示](@entry_id:181931) $\pi$，应该存在一个 $\mathrm{GL}_n(\mathbb{A}_E)$ 上的[自守表示](@entry_id:181931) $\Pi$（称为$\pi$的基变更提升），其L-参数恰好是$\pi$的L-参数限制在 $W_E$ 上的结果。

这一预测在局部层面有非常具体的体现。对于 $F$ 的一个未分歧素处 $v$ 以及 $E$ 中位于 $v$ 之上的素处 $w$，[局部基](@entry_id:151573)变更意味着 $\Pi_w$ 的L-参数 $\phi_{\Pi_w}$ 是 $\pi_v$ 的L-参数 $\phi_{\pi_v}$ 在局部Weil群 $W_{E_w}$ 上的限制。这直接导出了它们Satake参数之间的关系。根据[局部类域论](@entry_id:193658)，几何[Frobenius元](@entry_id:181102) $\mathrm{Frob}_w$ 在自然嵌入 $W_{E_w} \hookrightarrow W_{F_v}$ 下的像，是 $\mathrm{Frob}_v$ 的 $f(w|v)$ 次幂，其中 $f(w|v)$ 是剩余[域[扩张的次](@entry_id:149430)数](@entry_id:151271)。由于未分歧表示的Satake参数 $s(\pi_v)$ 就是 $\phi_{\pi_v}(\mathrm{Frob}_v)$ 的[共轭类](@entry_id:143916)，我们立即推导出 $\Pi_w$ 的Satake参数 $s(\Pi_w)$ 应该是 $s(\pi_v)$ 的 $f(w|v)$ 次幂。这个简单的幂次关系精确地描述了在未分歧处[自守表示](@entry_id:181931)的Hecke[特征值](@entry_id:154894)在[域扩张](@entry_id:153187)下的行为。[@problem_id:3027567] [@problem_id:3027520]

对于循环扩张 $E/F$，基变更的存在性最初由Arthur和Clozel通过比较Arthur-[Selberg迹公式](@entry_id:187042)与一个“扭曲”迹公式得以证明。这个深刻的证明策略本身就是方法论上的一个里程碑，我们将在后续章节中进一步探讨。[@problem_id:3027521]

#### 对称幂与外幂

另一类重要的[函子性](@entry_id:150069)提升来自于L-[群的表示](@entry_id:140711)。给定一个从源L-群到目标L-群的同态 $r: {}^L H \to {}^L G$，[函子性](@entry_id:150069)预言了从 $H$ 上的[自守表示](@entry_id:181931)到 $G$ 上的[自守表示](@entry_id:181931)的提升。当 $H=G=\mathrm{GL}_n$ 时，我们可以考虑 $\mathrm{GL}_n(\mathbb{C})$ 的任何一个[代数表示](@entry_id:143783) $r: \mathrm{GL}_n(\mathbb{C}) \to \mathrm{GL}_N(\mathbb{C})$。

最典型的例子是标准表示的对称幂和外幂。例如，考虑 $m$ 次对称幂表示 $\mathrm{Sym}^m: \mathrm{GL}_2(\mathbb{C}) \to \mathrm{GL}_{m+1}(\mathbb{C})$。给定 $\mathrm{GL}_2(\mathbb{A}_F)$ 上的一个尖形式[自守表示](@entry_id:181931) $\pi$，[函子性](@entry_id:150069)预言存在一个 $\mathrm{GL}_{m+1}(\mathbb{A}_F)$ 上的[自守表示](@entry_id:181931) $\mathrm{Sym}^m(\pi)$。在未[分歧](@entry_id:193119)素处 $v$，如果 $\pi_v$ 的Satake参数（在对角化后）为 $\mathrm{diag}(\alpha_v, \beta_v)$，那么 $\mathrm{Sym}^m(\pi)_v$ 的Satake参数则由 $\mathrm{Sym}^m(\mathrm{diag}(\alpha_v, \beta_v))$ 的[特征值](@entry_id:154894)给出。通过标准[表示论](@entry_id:137998)的计算可知，这些[特征值](@entry_id:154894)是 $\{\alpha_v^{m-j}\beta_v^j\}_{j=0}^m$。相应地，局部L-因子也从一个关于 $s$ 的二次多项式的倒数，变成了一个 $m+1$ 次多项式的倒数：
$$ L(s, \mathrm{Sym}^m\pi_v) = \prod_{j=0}^{m} (1 - \alpha_v^{m-j}\beta_v^j q_v^{-s})^{-1} $$
这个明确的公式展示了[函子性](@entry_id:150069)原理如何预测新的L-函数的结构。[@problem_id:3027553] [@problem_id:3027558]

类似地，对于 $\mathrm{GL}_n(\mathbb{A}_F)$ 上的表示 $\Pi$，其二阶外幂提升 $\wedge^2(\Pi)$ 是一个到 $\mathrm{GL}_{n(n-1)/2}(\mathbb{A}_F)$ 的[函子性](@entry_id:150069)提升。如果 $\Pi_v$ 的Satake参数为 $\{\gamma_{v,1}, \dots, \gamma_{v,n}\}$，那么 $\wedge^2(\Pi)_v$ 的Satake参数就是两两之积 $\{\gamma_{v,i}\gamma_{v,j}\}_{1\le i  j \le n}$。[@problem_id:3027558] 这些对称幂和外幂提升在现代数论中扮演着至关重要的角色，尤其是在证明Sato-Tate猜想等问题中。

#### [张量积](@entry_id:140694)与Rankin-Selberg [L-函数](@entry_id:193304)

[函子性](@entry_id:150069)的框架也自然地解释了经典的Rankin-Selberg [L-函数](@entry_id:193304)的来源。给定 $\mathrm{GL}_m(\mathbb{A}_F)$ 上的[自守表示](@entry_id:181931) $\pi$ 和 $\mathrm{GL}_n(\mathbb{A}_F)$ 上的[自守表示](@entry_id:181931) $\sigma$，我们可以考虑L-群的[张量积表示](@entry_id:143629) $r: \mathrm{GL}_m(\mathbb{C}) \times \mathrm{GL}_n(\mathbb{C}) \to \mathrm{GL}_{mn}(\mathbb{C})$。

[函子性](@entry_id:150069)原理预言，存在一个 $\mathrm{GL}_{mn}(\mathbb{A}_F)$ 上的[自守表示](@entry_id:181931)，通常记为 $\pi \boxtimes \sigma$，其L-参数是 $\pi$ 和 $\sigma$ 的L-参数的张量积。在未分歧素处 $v$，如果 $\pi_v$ 和 $\sigma_v$ 的Satake参数分别为 $\{\alpha_i\}$ 和 $\{\beta_j\}$，那么 $\pi \boxtimes \sigma$ 在该处的Satake参数就是所有可能的乘积 $\{\alpha_i \beta_j\}$。

因此，$\pi \boxtimes \sigma$ 的标准[L-函数](@entry_id:193304)（即全局L-函数）的局部因子是：
$$ L_v(s, \pi \boxtimes \sigma) = \prod_{i=1}^m \prod_{j=1}^n (1 - \alpha_i \beta_j q_v^{-s})^{-1} $$
这个L-函数正是经典的Rankin-Selberg [L-函数](@entry_id:193304) $L(s, \pi \times \sigma)$。因此，[函子性](@entry_id:150069)原理为Rankin-Selberg [L-函数](@entry_id:193304)的自守性提供了深刻的理论解释：它是一个更高阶GL群上某个[自守表示](@entry_id:181931)的标准[L-函数](@entry_id:193304)。这一认识是研究L-函数[解析性](@entry_id:140716)质（如解析延拓、[函数方程](@entry_id:199663)）的基石。[@problem_id:3027555]

### 与重要猜想及[分类理论](@entry_id:153976)的联系

Langlands纲领的深远影响不仅在于构造新的[自守表示](@entry_id:181931)，更在于它为数论中一些最核心的猜想提供了统一的框架和语言，并最终导向了对自守谱的宏大分类。

#### 从[上同调](@entry_id:160558)表示到纯粹动机：权重与Satake参数

Langlands纲领的一个核心思想是，源于[算术几何](@entry_id:189136)的Galois表示应该与[自守表示](@entry_id:181931)相对应。特别是，那些出现在代数簇上同调中的Galois表示，被期望对应于一类特殊的“[上同调](@entry_id:160558)[自守表示](@entry_id:181931)”。这些Galois表示（或其背后的“动机”）具有一个重要的性质，即“纯粹性”。

根据Deligne的理论，一个权重为 $w$ 的纯粹动机（或其 $\ell$-adic实现），其在好约化素数 $v$ 处的Frobenius[特征值](@entry_id:154894)是权重为 $w$ 的Weil数，即在任何[复嵌入](@entry_id:189961)下，它们的[绝对值](@entry_id:147688)都等于 $q_v^{w/2}$。

另一方面，一个在无穷处具有代数性的上同调[自守表示](@entry_id:181931) $\pi$ of $\mathrm{GL}_n(\mathbb{A}_F)$，根据Clozel等人的工作，也被赋予了一个整的“纯粹权重” $w(\pi)$。Langlands对应关系预言，与 $\pi$ 关联的Galois表示 $\rho_{\pi}$ 正是纯粹的，且其权重就是 $w(\pi)$。

通过这个对应关系，我们可以直接读出 $\pi$ 的（算术归一化）Satake参数 $\alpha_{v,i}$ 的[绝对值](@entry_id:147688)。它们必须满足：
$$ |\alpha_{v,i}| = q_v^{w(\pi)/2} $$
对于几乎所有的素处 $v$。这个等式完美地连接了[自守表示](@entry_id:181931)在无穷处的分析性质（决定了 $w(\pi)$）和它在有限素数处的算术性质（Satake参数）。反过来看，这意味着通过一个合适的扭变换 $\pi \otimes |\det|^{-w(\pi)/2}$，我们可以将一个[上同调](@entry_id:160558)表示“单位化”，使其在几乎所有未[分歧](@entry_id:193119)处的Satake参数[绝对值](@entry_id:147688)都为1。这为我们提供了研究和分类这类重要[自守表示](@entry_id:181931)的代数工具。[@problem_id:3027563]

#### [Ramanujan-Petersson猜想](@entry_id:181349)的现代表述

经典的Ramanujan猜想是关于Ramanujan $\tau$ [函数增长](@entry_id:267648)阶的一个估计，它等价于 $\mathrm{GL}_2$ 上与某个[模形式](@entry_id:160014)相关的[自守表示](@entry_id:181931)的Hecke[特征值](@entry_id:154894)的界。这个猜想被推广到 $\mathrm{GL}_n(\mathbb{A}_F)$ 上的任意尖形式[自守表示](@entry_id:181931) $\pi$（具有酉中心特征），被称为广义[Ramanujan-Petersson猜想](@entry_id:181349)。

在Langlands纲领的语言中，这个猜想有了一个极为优雅和深刻的表述：$\pi$ 的所有局部成员 $\pi_v$ 都应该是“温性”（tempered）的。

“温性”是一个[表示论](@entry_id:137998)中的概念，粗略地说，它意味着一个表示是构成 $L^2$ 空间的基本构件（离散级数）的“最基本”的酉诱导。
- 在一个未分歧的有限素处 $v$，$\pi_v$ 是温性的当且仅当它的所有Satake参数 $\alpha_{v,i}$ 的复[绝对值](@entry_id:147688)为1，即 $|\alpha_{v,i}| = 1$。
- 在一个阿基米德素处 $v$，$\pi_v$ 是温性的当且仅当其无穷小特征是纯虚的。

因此，[Ramanujan-Petersson猜想](@entry_id:181349)——一个关于算术数据（Hecke[特征值](@entry_id:154894)）大小的深刻断言——在Langlands的框架下被统一地表述为一个关于表示在所有[局部域](@entry_id:195717)上都是“温性”的纯粹表示论性质。这一重新表述不仅揭示了猜想的内在结构，也指明了证明它的可能途径，即通过研究[自守表示](@entry_id:181931)的局部和全局性质。[@problem_id:3027544]

#### Sato-Tate猜想的证明策略

Sato-Tate猜想描述了非[CM椭圆曲线](@entry_id:197957) $E/\mathbb{Q}$ 的[Frobenius迹](@entry_id:197951) $a_p(E)$ 的统计分布规律。通过关系式 $a_p(E) = 2p^{1/2}\cos\theta_p$，它等价于角度序列 $\{\theta_p\}$ 在 $[0, \pi]$ 上关于 $\frac{2}{\pi}\sin^2\theta \,d\theta$ 测度[等分布](@entry_id:194597)。

证明这个猜想是Langlands纲领思想的一次伟大胜利，其核心策略完美地展示了[函子性](@entry_id:150069)的力量。根据Serre的一个判则，证明[等分布](@entry_id:194597)等价于证明对于每一个整数 $n \ge 1$，由[Chebyshev多项式](@entry_id:145074) $U_n(\cos\theta_p)$ 构成的[L-函数](@entry_id:193304)在临界线的关键点 $s=1$ 附近具有良好的[解析性](@entry_id:140716)质（无[零点和极点](@entry_id:177073)）。

这里的关键一步是将 $U_n(\cos\theta_p)$ 与一个Galois表示的迹联系起来。与椭圆曲线 $E$ 相伴的2维 $\ell$-adic Galois表示 $\rho_{E,\ell}$ 的 $n$ 次对称幂 $\mathrm{Sym}^n \rho_{E,\ell}$ 是一个 $(n+1)$ 维的Galois表示。其[Frobenius迹](@entry_id:197951)恰好是 $p^{n/2}U_n(\cos\theta_p)$。因此，Serre判则中的L-函数本质上是与 $\mathrm{Sym}^n \rho_{E,\ell}$ 相关的[Artin L-函数](@entry_id:185194) $L(s, \mathrm{Sym}^n E)$ 的一个平移。

Langlands纲领预言，$L(s, \mathrm{Sym}^n E)$ 应该是一个 $\mathrm{GL}_{n+1}(\mathbb{A}_{\mathbb{Q}})$ 上某个[自守表示](@entry_id:181931)的[L-函数](@entry_id:193304)。证明Sato-Tate猜想的突破口，正是由Taylor及其合作者通过“潜在自守性”技术实现的。他们证明了对于每一个 $n \ge 1$，表示 $\mathrm{Sym}^n \rho_{E,\ell}$ 在限制到一个合适的（可解的）数[域扩张](@entry_id:153187) $F/\mathbb{Q}$ 后是自守的，即它来自于一个 $\mathrm{GL}_{n+1}(\mathbb{A}_F)$ 上的尖形式[自守表示](@entry_id:181931)。

一旦建立了这种（潜在）自守性，就可以动用关于自守L-函数的强有力的解析理论（如Jacquet-Shalika的结果），证明这些L-函数在[临界带](@entry_id:638010) $\mathrm{Re}(s)=1$ 上无零点。通过可解基变更和Brauer诱导定理等工具，这些良好的[解析性](@entry_id:140716)质可以从扩张域 $F$ “下降”到 $\mathbb{Q}$ 上。最终，这为应用Serre判则提供了所需的全部解析输入，从而完成了Sato-Tate猜想的证明。这个过程是[函子性](@entry_id:150069)原理、模性提升和[L-函数](@entry_id:193304)分析理论协同作用的典范。[@problem_id:3029314] [@problem_id:3014878]

### 证明[函子性](@entry_id:150069)的方法论支柱

建立Langlands纲领的预测，尤其是[函子性](@entry_id:150069)原理，是过去半个世纪数论的核心任务之一。几种宏大的方法论被发展出来，它们共同构成了我们理解这一领域的基础。

#### [志村簇](@entry_id:204503)的上同调与Galois表示的构造

许多已知的Langlands对应关系的例子来源于代数几何。[志村簇](@entry_id:204503)是一类特殊的代数簇，其定义依赖于一个约化群 $G$ 和一个相关的复流形族 $X$。它们可以被看作是[模曲线](@entry_id:199342)的高维推广。[志村簇](@entry_id:204503)的精妙之处在于它们同时具有丰富的算术和几何结构。

根据Deligne的理论，[志村簇](@entry_id:204503) $\mathrm{Sh}_K(G,X)$ 在其“反射域” $E$ 上有[典范模型](@entry_id:198268)。这使得我们可以研究它们的算术性质。特别地，其$\ell$-adic[上同调群](@entry_id:142450) $H^i_{\text{ét}}(\mathrm{Sh}_K(G,X)_{\overline{E}}, \mathbb{Q}_\ell)$ 成为一个关键的研究对象。作为一个定义在 $E$ 上的代数簇的上同调，它自然地带有一个由绝对Galois群 $\mathrm{Gal}(\overline{E}/E)$ 诱导的连续作用。

另一方面，[志村簇](@entry_id:204503)的点集可以被解释为某个带附加结构的Abel簇的[模空间](@entry_id:159780)，这使得[Hecke算子](@entry_id:181282)可以在其上几何地定义为代数对应。这些[Hecke算子](@entry_id:181282)也在上同调群上诱导作用，并且这个作用与Galois群的作用是可交换的。

因此，上同调群 $H^i_{\text{ét}}$ 成为了一个同时承载着Galois表示和[Hecke代数](@entry_id:192416)表示的“桥梁”。通过分解这个空间，人们可以在一个尖形式[自守表示](@entry_id:181931)所生成的Hecke特征空间上，直接“读出”一个与之匹配的Galois表示。这个构造为无数的Langlands对应实例提供了源头，并构成了证明模性猜想的几何基础。[@problem_id:3023629]

#### 迹公式、内窥与基变更

Arthur-[Selberg迹公式](@entry_id:187042)是比较两个不同群上自守谱的强大分析工具。它的一边（谱展开）与群的[自守表示](@entry_id:181931)的谱有关，而另一边（几何展开）则与群的[共轭类](@entry_id:143916)的[轨道](@entry_id:137151)积分有关。证明[函子性](@entry_id:150069)原理的一个基本策略，就是通过精心[选择检验](@entry_id:182706)函数，使得一个群 $H$ 上的迹公式的几何边能够与另一个群 $G$ 上的（可能是扭曲的）迹公式的几何边相匹配。如果几何边相等，那么谱边也必须相等，从而建立起 $H$ 和 $G$ 谱之间的一一对应。

基变更是这个策略最早的成功案例。通过比较 $\mathrm{GL}_n$ 在域 $F$ 上的标准迹公式和在循环扩张 $E/F$ 上的扭曲迹公式，Arthur和Clozel成功证明了循环基变更的存在性。这里的关键技术挑战是证明局部检验函数的[轨道](@entry_id:137151)积分在基变更映射下能够匹配，这被称为“基本引理”。Ngô Bảo Châu因证明了迹公式方法所需的“基本引理”而获得菲尔兹奖，这一突破为整个领域开辟了道路。[@problem_id:3027521]

“内窥”（Endoscopy）是这一思想的深刻推广。对于一个群 $G$，存在一系列所谓的“内窥群” $H$。这些群的L-群嵌入到 $G$ 的L-群中，并且与 $G$ 的某些非温性[自守表示](@entry_id:181931)（那些违反广义[Ramanujan-Petersson猜想](@entry_id:181349)的表示）的构造密切相关。内窥分类纲领的目标是，通过系统地比较 $G$ 的稳定迹公式与它所有内窥群的稳定迹公式，来分解 $G$ 的自守谱。这个极其复杂的纲领最终由Arthur完成，并导向了对[典型群](@entry_id:203721)自守谱的分类。[@problem_id:3027510]

#### 逆定理与[L-函数](@entry_id:193304)的分析性质

与迹公式的“几何”方法相对，还存在一种“分析”方法来证明自守性，即所谓的“逆定理”。逆定理的思想是，一个表示的自守性可以通过其[L-函数](@entry_id:193304)的[解析性](@entry_id:140716)质来判定。

最早由Hecke为 $\mathrm{GL}_2$ 提出，后由Weil、Jacquet-Langlands、Cogdell和Piatetski-Shapiro等人推广到 $\mathrm{GL}_n$。一个典型的逆定理断言，如果一个 $\mathrm{GL}_n(\mathbb{A}_F)$ 上的一个可容许表示 $\Pi$，其本身以及它与所有 $\mathrm{GL}_m(\mathbb{A}_F)$ 上的尖形式[自守表示](@entry_id:181931) $\sigma$ (对于 $1 \le m \le n-2$) 的扭L-函数 $L(s, \Pi \times \sigma)$ 都满足预期的[解析性](@entry_id:140716)质（解析延拓、函数方程、在竖直带内有界），那么 $\Pi$ 本身就是一个[自守表示](@entry_id:181931)。

在证明[函子性](@entry_id:150069)提升时，逆定理提供了一个强大的策略：
1. 从一个源[自守表示](@entry_id:181931)（或一个猜测的Galois表示）出发，利用[函子性](@entry_id:150069)原理的预测来“定义”一个目标表示 $\Pi$ 的L-函数。
2. 证明这个（以及其所有必要的扭）L-函数满足逆定理所需的全部解析性质。
3. 应用逆定理，断定 $\Pi$ 确实是自守的，从而实现了[函子性](@entry_id:150069)提升。

这一方法在Sato-Tate猜想的证明中发挥了核心作用，其中潜在自守性的确立正是为了保证相应的L-函数具有所需的[解析性](@entry_id:140716)质。[@problem_id:3027537]

#### 模性[提升技术](@entry_id:634420)与Serre猜想

Serre模性猜想（现已成为定理）断言，任何一个来自 $\mathbb{Q}$ 上的奇、不可约的2维 mod $p$ Galois表示都来自于一个[模形式](@entry_id:160014)。这个猜想的证明是数论中的一座丰碑，其核心是“模性提升”定理。

[模性提升定理](@entry_id:204337)通常断言，如果一个 mod $p$ Galois表示 $\bar{\rho}$ 是模的，那么在一定技术条件下，它的任何一个合适的 $p$-adic Galois表示“提升” $\rho$ 也必须是模的。证明这类定理是Langlands纲领中各种思想和技术的集结点。

一个常见的策略是，如果给定的提升 $\rho_p$ 不满足[模性提升定理](@entry_id:204337)所需的局部条件（例如，在 $p$ 处不是“普通”的，或者Hodge-Tate权不合适），可以采用“可解基变更”的技巧。通过将问题基变更到一个精心选择的可解扩张域 $F/\mathbb{Q}$，原来的表示 $\rho_p$ 的限制 $\rho_p|_{G_F}$ 可能就会满足某个[模性提升定理](@entry_id:204337)的条件（例如，在 $F$ 的所有位于 $p$ 之上的素数处都变得普通）。然后，可以在域 $F$ 上证明 $\rho_p|_{G_F}$ 的模性，再利用Langlands的可解基变更理论将模性“下降”回 $\mathbb{Q}$，最终证明 $\rho_p$ 是模的。

在这个过程中，“[相容系统](@entry_id:153969)”的概念至关重要。它允许在不同的素数 $\ell$ 之间传递信息。例如，有时可以通过在一个辅助素数 $\ell \neq p$ 处证明模性，然后利用相容性将这一信息传递回我们关心的 $p$-adic表示。可解基变更保持了[相容系统](@entry_id:153969)在各个[局部域](@entry_id:195717)上的关键性质，使得这一复杂的多步论证得以顺利进行。[@problem_id:3023484]

### 集大成之作：Arthur的内窥分类

Langlands纲领的最终目标之一是理解和分类所有约化群上的[自守表示](@entry_id:181931)。对于拟分裂的[典型群](@entry_id:203721)（如[辛群](@entry_id:189031)和[正交群](@entry_id:152531)），这一宏伟目标在James Arthur的工作中达到了一个顶峰。他的“内窥分类”是对这些群的离散自守谱的完整描述。

Arthur的分类不是直接使用Langlands参数（即从Weil-Deligne群到L-群的同态），而是使用一类更广义的对象，称为“Arthur参数”（或A-参数）。一个A-参数可以看作是一个从 $L_F \times \mathrm{SL}_2(\mathbb{C})$ 到 ${}^L G$ 的同态。$\mathrm{SL}_2(\mathbb{C})$ 因子的引入是为了系统地解释那些非温性的[离散谱](@entry_id:150970)表示。

对于[典型群](@entry_id:203721)，A-参数可以更具体地用 $\mathrm{GL}_n$ 上的[自守表示](@entry_id:181931)来构造。它们是形如 $\boxplus_i \pi_i \boxtimes S_{d_i}$ 的形式和，其中每个 $\pi_i$ 是 $\mathrm{GL}_{n_i}(\mathbb{A}_F)$ 上的一个自偶尖形式[自守表示](@entry_id:181931)，而 $S_{d_i}$ 是 $\mathrm{SL}_2(\mathbb{C})$ 的 $d_i$ 维[不可约表示](@entry_id:263310)。

Arthur理论的核心成果是：
1.  **A-包（A-packets）**：每个全局A-参数 $\psi$ 对应一个有限的[自守表示](@entry_id:181931)集合 $\Pi_\psi$，称为一个全局A-包。
2.  **[谱分解](@entry_id:173707)**：$G$ 的离散自守谱 $L^2_{\mathrm{disc}}(G(F)\backslash G(\mathbb{A}_F))$ 可以分解为这些A-包的直和。
3.  **重数公式**：一个给定的A-包中的成员在[离散谱](@entry_id:150970)中出现的重数由一个复杂的“[重数](@entry_id:136466)公式”给出。这个公式与参数 $\psi$ 的[中心化子](@entry_id:146604)以及内窥理论密切相关。

Arthur的分类是对[函子性](@entry_id:150069)原理的一次巨大成功实现。它表明，[典型群](@entry_id:203721)上的[自守表示](@entry_id:181931)谱在很大程度上可以由 $\mathrm{GL}_n$ 上的[自守表示](@entry_id:181931)（这是我们理解得最好的）通过[函子性](@entry_id:150069)（包括内窥提升）来构建和理解。这是Langlands纲领思想力量的终极证明之一。[@problem_id:3027505]

### 结论

从具体的[函子性](@entry_id:150069)提升实例，到它们在解决Ramanujan-Petersson和Sato-Tate等重大猜想中的应用，再到迹公式和逆定理等深刻的证明方法论，直至Arthur的宏大分类，我们看到Langlands[函子性](@entry_id:150069)原理如同一条金线，贯穿了现代数论的织锦。它不仅为看似无关的现象提供了统一的解释，还为未来的研究指明了方向，继续激励着数学家们去探索[自守形式](@entry_id:186448)、Galois表示和[算术几何](@entry_id:189136)之间更深层次的奥秘。