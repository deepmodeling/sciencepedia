## 引言
Cheeger-Colding理论是现代[黎曼几何](@entry_id:160508)和[几何分析](@entry_id:157700)的基石，它深刻地改变了我们对仅有Ricci曲率下界这一弱曲率条件的[流形](@entry_id:153038)几何的理解。在经典几何中，强大的[截面曲率](@entry_id:159738)条件能严格控制[流形的拓扑](@entry_id:267834)与几何，但现实世界和理论研究中的许多问题，如Ricci流的[奇点分析](@entry_id:198717)或[Kähler-Einstein度量](@entry_id:270601)的退化，都自然地导向了只满足[Ricci曲率界](@entry_id:635813)的更广阔的几何情境。这就带来了一个核心的知识缺口：当[流形](@entry_id:153038)序列仅在[Ricci曲率](@entry_id:162038)下界意义下受控时，它们的极限行为是什么？这些通常不再是[光滑流形](@entry_id:160799)的[极限空间](@entry_id:636945)，又具有怎样的结构？

本文旨在系统性地回答这些问题，为读者呈现Cheeger-Colding理论的全貌。在第一章**“原理和机制”**中，我们将奠定理论的基石，从[Ricci曲率与体积](@entry_id:191680)比较的关系出发，引入[Gromov-Hausdorff收敛](@entry_id:158087)，并详细剖析[极限空间](@entry_id:636945)中正则集与[奇异集](@entry_id:186233)的精细结构。随后，在第二章**“应用与跨学科联系”**中，我们将展示这一理论的强大威力，探讨其如何将经典[刚性定理](@entry_id:198222)推广为稳定性定理，并应用于解决[复几何](@entry_id:159080)、代数几何乃至[数学物理](@entry_id:265403)中的前沿问题。最后，在第三章**“动手实践”**中，我们将通过一系列具体的计算练习，帮助读者将抽象的理论概念内化为可操作的技能，从而更深入地理解曲率、体积与极限之间的定量关系。通过这三个章节的学习，读者将能够全面掌握Cheeger-Colding理论的核心思想及其在现代数学中的重要作用。

## 原理和机制

本章深入探讨Cheeger-Colding理论的核心原理与机制。在前一章介绍背景之后，我们将系统地构建这一理论的基石，从Ricci曲率控制下的几何性质出发，到度量空间的[收敛理论](@entry_id:176137)，再到[极限空间](@entry_id:636945)的[精细结构](@entry_id:140861)。我们将阐明关键的定理，如体积比较、[几乎分裂定理](@entry_id:187886)和[极限空间](@entry_id:636945)的正规性，揭示Ricci曲率下限如何深刻地塑造了[黎曼流形](@entry_id:261160)的几何与拓扑。

### 几何基础与[收敛理论](@entry_id:176137)

Cheeger-Colding理论建立在几个核心概念之上：[Ricci曲率](@entry_id:162038)下界所蕴含的几何控制，以及能够描述[流形](@entry_id:153038)[序列极限](@entry_id:188751)的[Gromov-Hausdorff收敛](@entry_id:158087)。

#### [Ricci曲率与体积](@entry_id:191680)比较

Ricci曲率是[黎曼几何](@entry_id:160508)中最核心的曲率[不变量](@entry_id:148850)之一，它在一个点的特定方向上，度量了该点附近[体积元](@entry_id:267802)的扭曲程度。一个$n$维[黎曼流形](@entry_id:261160)$(M^n, g)$的[Ricci曲率张量](@entry_id:271424)$\operatorname{Ric}$在每一点$x \in M$都是切空间$T_xM$上的[对称双线性形式](@entry_id:148281)。说一个[流形](@entry_id:153038)的Ricci曲率有下界$\operatorname{Ric} \ge (n-1)k$，其精确含义是：对于任意点$x \in M$和任意[单位切向量](@entry_id:262985)$v \in T_xM$，都有$\operatorname{Ric}_x(v,v) \ge (n-1)k$成立。这里，$k$是一个实常数，而$(n-1)k$这个归一化因子是为了方便与[常截面曲率](@entry_id:272200)为$k$的典范空间模型（如球面、欧氏空间、双曲空间）进行比较。

[Ricci曲率](@entry_id:162038)下界最重要的几何推论之一是**[Bishop-Gromov体积比较定理](@entry_id:182112)**。该定理指出，如果一个完备$n$维[黎曼流形](@entry_id:261160)$(M^n, g)$满足$\operatorname{Ric} \ge (n-1)k$，那么对于[流形](@entry_id:153038)中的任意一点$p$，函数
$r \mapsto \frac{\operatorname{Vol}(B_p(r))}{\operatorname{Vol}_k(r)}$
是关于半径$r > 0$的非增函数。其中，$B_p(r)$是$M$中以$p$为中心、半径为$r$的测地 球，$ \operatorname{Vol}$是其黎曼体积；而$\operatorname{Vol}_k(r)$是$n$维[常截面曲率](@entry_id:272200)为$k$的[单连通空间](@entry_id:263761)模型$M_k^n$中半径为$r$的测地 球的体积。

这个定理的直观含义是，Ricci曲率越大，测地 球的[体积增长](@entry_id:274676)得越慢。其证明的核心思想是在[测地极坐标](@entry_id:194605)下比较距离函数的[拉普拉斯算子](@entry_id:146319)，这与沿径向[测地线](@entry_id:269969)的雅可比行列式满足的[Riccati方程](@entry_id:184132)有关。[Ricci曲率](@entry_id:162038)下界$\operatorname{Ric} \ge (n-1)k$保证了$M$中测地 球面的径向平均曲率不会超过模型空间$M_k^n$中的对应值。通过对曲率不等式进行积分，便可得到体积增长率的比较，进而得到体积比值的[单调性](@entry_id:143760)。值得注意的是，这一[单调性](@entry_id:143760)在[流形](@entry_id:153038)的[割迹](@entry_id:161337)（cut locus）之外也成立，在全局范围内对所有$r>0$都有效[@problem_id:3039752]。

#### 度量空间的[Gromov-Hausdorff收敛](@entry_id:158087)

为了研究[流形](@entry_id:153038)[序列的极限](@entry_id:159239)行为，我们需要一种能够比较不同[度量空间](@entry_id:138860)的“形状”的工具。**Gromov-Hausdorff (GH)距离**应运而生。对于两个[紧致度量空间](@entry_id:156601)$(X, d_X)$和$(Y, d_Y)$，它们的GH距离$d_{GH}(X, Y)$是$X$和$Y$在某个公共[度量空间](@entry_id:138860)$Z$中的[等距嵌入](@entry_id:152303)$\varphi(X)$和$\psi(Y)$之间的[Hausdorff距离](@entry_id:152367)的下确界。它度量了两个空间在多大程度上可以被看作是“几乎等距”的。

然而，许多有趣的[流形](@entry_id:153038)（如[欧氏空间](@entry_id:138052)）是非紧的。为了处理这种情况，我们使用**带基点的[Gromov-Hausdorff收敛](@entry_id:158087)**（pointed Gromov-Hausdorff convergence）。一个带基点的度量空间是一个偶对$(X, p)$，其中$p \in X$是基点。一个带基点的度量空间序列$(X_i, p_i)$收敛到$(X, p)$，直观上是指在任意固定的半径$R$下，$p_i$周围的球$B_{X_i}(p_i, R)$的几何越来越像$p$周围的球$B_X(p, R)$。

这个直观想法的严格定义是：序列$(X_i, p_i)$在带基点的Gromov-Hausdorff意义下收敛到$(X, p)$，当且仅当对于任意$R > 0$，紧致度量球序列$(B_{X_i}(p_i, R), d_{X_i})$在GH距离下收敛到度量球$(B_X(p, R), d_X)$，即
$$ \lim_{i\to\infty} d_{GH}\big(B_{X_i}(p_i, R), B_X(p, R)\big) = 0 $$
这等价于存在一个$\varepsilon_i \to 0$的序列，使得对于每个$R>0$，都存在一个**$\varepsilon_i$-近似映射** $f_i^R: B_{X_i}(p_i, R) \to X$，它近似地保持距离（即$|d_X(f_i^R(x), f_i^R(y)) - d_{X_i}(x,y)| \le \varepsilon_i$），并且其像在$B_X(p,R)$中是$\varepsilon_i$-稠密的，同时保持基点$f_i^R(p_i)=p$。

对于黎曼流形序列$(M_i, g_i, p_i)$，我们将它们视为带基点的[度量空间](@entry_id:138860)$(M_i, d_{g_i}, p_i)$。一个至关重要的事实是，即使序列中的每个空间都是光滑流形，它们的GH极限$(X, p)$通常也仅仅是一个[度量空间](@entry_id:138860)，未必具有[流形](@entry_id:153038)结构。例如，一列半径越来越小的[二维环面](@entry_id:265991)可以GH收敛到一个一维的圆周。理解这种[极限空间](@entry_id:636945)的结构正是Cheeger-Colding理论的核心目标[@problem_id:3039756]。

#### 带测度的[Gromov-Hausdorff收敛](@entry_id:158087)

在黎曼几何中，我们不仅关心距离，还关心体积。因此，将测度融入[收敛理论](@entry_id:176137)是至关重要的。一个**[度量测度空间](@entry_id:180197)**是一个三元组$(Y, d_Y, \nu)$，其中$(Y, d_Y)$是一个完备可分的[度量空间](@entry_id:138860)，$\nu$是其上的一个有限[Borel测度](@entry_id:187965)。对于一个[黎曼流形](@entry_id:261160)序列$(M_i, g_i)$，我们可以赋予其黎曼体[积测度](@entry_id:266846)$\operatorname{Vol}_{g_i}$。为了避免总测度趋于无穷或零，我们常常进行归一化，例如在紧致情形下定义概率测度$\mu_i = \operatorname{Vol}_{g_i} / \operatorname{Vol}_{g_i}(M_i)$。这样我们就得到一个[度量测度空间](@entry_id:180197)序列$(M_i, d_{g_i}, \mu_i)$。

**带测度的Gromov-Hausdorff (mGH)收敛**的概念结合了[几何收敛](@entry_id:201608)和测度收敛。一个[度量测度空间](@entry_id:180197)序列$(X_i, d_i, \mu_i)$ mGH收敛到$(X, d, \mu)$，是指：
1.  [度量空间](@entry_id:138860)$(X_i, d_i)$在GH意义下收敛到$(X, d)$。
2.  存在$\varepsilon_i \to 0$的$\varepsilon_i$-近似映射序列$f_i: X_i \to X$，使得**[前推测度](@entry_id:201640)**$(f_i)_* \mu_i$在[极限空间](@entry_id:636945)$X$上**弱收敛**到测度$\mu$。

[前推测度](@entry_id:201640)$(f_i)_* \mu_i$定义为$((f_i)_* \mu_i)(A) = \mu_i(f_i^{-1}(A))$。弱收敛意味着对于$X$上任意有界[连续函数](@entry_id:137361)$\varphi$，都有$\int_X \varphi \, d((f_i)_* \mu_i) \to \int_X \varphi \, d\mu$。

在黎曼流形序列$(M_i, d_{g_i})$ GH收敛到$(X, d_X)$的背景下，我们可以考虑归一化体[积测度](@entry_id:266846)序列$\mu_i = \operatorname{Vol}_{g_i}/\operatorname{Vol}_{g_i}(M_i)$。由于$X$是紧的，根据[Prokhorov定理](@entry_id:196729)，$X$上的概率测度序列是弱收敛意义下列紧的。这意味着，我们可以（沿着一个子列）找到一个极限Borel概率测度$\mu$，使得$(f_i)_*\mu_i$弱收敛到$\mu$。这就保证了在GH极限下，我们总能得到一个伴随的极限测度[@problem_id:3039732]。

### [极限空间](@entry_id:636945)的结构

有了收敛的框架，我们现在可以研究[极限空间](@entry_id:636945)的性质。Gromov的一个奠基性的定理表明，一列具有一致[Ricci曲率](@entry_id:162038)下界的$n$维黎曼流形总是列紧的，即总能提取一个带基点的[Gromov-Hausdorff收敛](@entry_id:158087)子列。Cheeger和Colding的工作深刻地揭示了这些[极限空间](@entry_id:636945)的结构。

#### 体积收敛与非塌缩条件

在GH收敛的背景下，一个自然的问题是：[流形](@entry_id:153038)序列上球的体积是否收敛到[极限空间](@entry_id:636945)中球的体积？答案是肯定的，但这需要一个额外的条件。

我们定义**非塌缩条件**（noncollapse condition）为一个在单位尺度上的体积下界。对于带基点的序列$(M_i^n, g_i, p_i)$，如果存在一个常数$v_0 > 0$使得$\operatorname{Vol}_{g_i}(B_{p_i}(1)) \ge v_0$对所有$i$成立，我们就说这个序列在基点处是非塌缩的。这个条件防止了[流形](@entry_id:153038)在极限过程中“压扁”成一个更低维的空间。

**Cheeger-Colding体积收敛定理**指出：给定一个满足$\operatorname{Ric}_{M_i} \ge -(n-1)\kappa$和非塌缩条件$\operatorname{Vol}_{g_i}(B_{p_i}(1)) \ge v_0 > 0$的[流形](@entry_id:153038)序列$(M_i, g_i, p_i)$，如果它pGH收敛到$(X, d, p)$，那么黎曼体[积测度](@entry_id:266846)$\operatorname{Vol}_{g_i}$会[弱收敛](@entry_id:146650)到一个极限[Radon测度](@entry_id:188027)$\mu$。这种弱收敛的一个重要推论是球体积的收敛：对于任意使得$\mu(\partial B_p(r)) = 0$的半径$r > 0$（即$B_p(r)$是极限测度$\mu$的一个[连续集](@entry_id:186725)），我们有
$$ \lim_{i \to \infty} \operatorname{Vol}_{g_i}(B_{p_i}(r)) = \mu(B_p(r)) $$
这个定理是联系$M_i$的几何与$X$的几何的桥梁。其证明依赖于[Bishop-Gromov定理](@entry_id:183135)给出的体积双倍性质，它保证了测度序列的弱[列紧性](@entry_id:264557)[@problem_id:3039766]。

#### 正则集与[奇异集](@entry_id:186233)

Cheeger-Colding理论最引人注目的成果之一，是对[极限空间](@entry_id:636945)$X$进行了精细的结构分解。这个分解基于**[切锥](@entry_id:191609)**（tangent cone）的概念。在[极限空间](@entry_id:636945)$X$的一点$x$处的[切锥](@entry_id:191609)，是通过不断放大$x$周围的几何得到的[极限空间](@entry_id:636945)。形式上，它是任何带基点序列$(X, r_j^{-1}d, x)$在$r_j \to 0$时的pGH极限。[切锥](@entry_id:191609)描述了$X$在$x$点的无穷小结构。

基于[切锥](@entry_id:191609)的性质，我们将[极限空间](@entry_id:636945)$X$分解为两个部分：
- **正则集 (regular set)** $\mathcal{R}$：由那些所有[切锥](@entry_id:191609)都等距于[欧氏空间](@entry_id:138052)$\mathbb{R}^n$的点$x \in X$组成。这些点在无穷小尺度下看起来是欧氏的。
- **[奇异集](@entry_id:186233) (singular set)** $\mathcal{S}$：由正则集之外的点组成，即$\mathcal{S} = X \setminus \mathcal{R}$。在[奇异点](@entry_id:199525)处，至少存在一个[切锥](@entry_id:191609)不等距于$\mathbb{R}^n$。

关于这个分解，Cheeger和Colding证明了一系列深刻的性质[@problem_id:3039761]：
1.  **拓扑性质**: 正则集$\mathcal{R}$是$X$中的一个开集，因此[奇异集](@entry_id:186233)$\mathcal{S}$是[闭集](@entry_id:136446)。
2.  **[切锥](@entry_id:191609)唯一性**: 对任意正则点$x \in \mathcal{R}$，其[切锥](@entry_id:191609)不仅存在，而且是唯一的（在等距意义下），且等于$\mathbb{R}^n$。
3.  **[奇异集](@entry_id:186233)的大小**: [奇异集](@entry_id:186233)$\mathcal{S}$非常小。其[Hausdorff维数](@entry_id:158929)$\dim_{\mathcal{H}}(\mathcal{S})$有一个尖锐的上界：$\dim_{\mathcal{H}}(\mathcal{S}) \le n-2$。这意味着[奇异集](@entry_id:186233)的[余维数](@entry_id:273141)至少为2 [@problem_id:3039769]。
4.  **正则集的测度**: 作为上述维度估计的直接推论，[奇异集](@entry_id:186233)的$n$维[Hausdorff测度](@entry_id:200740)为零，即$\mathcal{H}^n(\mathcal{S}) = 0$。这意味着正则集$\mathcal{R}$具有全测度，从测度的角度看，[极限空间](@entry_id:636945)$X$几乎完全由正则点构成。

这些结果表明，尽管GH极限可能不是光滑流形，但在非塌缩和[Ricci曲率](@entry_id:162038)有下界的条件下，它的结构受到了极大的限制。它在“几乎所有”地方都表现出[欧氏空间](@entry_id:138052)的特性，而“坏点”（[奇异点](@entry_id:199525)）则被限制在一个低维的集合中。

### 刚性、稳定性与局部结构

Cheeger-Colding理论的一个核心思想是**稳定性**（stability）：如果一个几何对象几乎满足某个[刚性定理](@entry_id:198222)的条件，那么它的结构也必定近似于该[刚性定理](@entry_id:198222)所描述的结构。这一思想通过“几乎分裂”和“几乎锥”定理得到了完美的体现。

#### [分裂定理](@entry_id:197795)：从刚性到稳定性

经典的**Cheeger-Gromoll[分裂定理](@entry_id:197795)**是一个[刚性定理](@entry_id:198222)。它断言：如果一个[完备黎曼流形](@entry_id:182954)$M$满足$\operatorname{Ric}_M \ge 0$并且包含一条**直线**（即一条对所有参数都极小化的[测地线](@entry_id:269969)$\gamma: \mathbb{R} \to M$），那么$M$必定**等距分裂**为一个乘[积空间](@entry_id:151693)$M \cong \mathbb{R} \times N$，其中$N$是一个满足$\operatorname{Ric}_N \ge 0$的[流形](@entry_id:153038)。

**Cheeger-Colding[几乎分裂定理](@entry_id:187886)**（almost splitting theorem）是上述定理的稳定性版本。它处理的是条件被“几乎”满足的情形：
- Ricci曲率条件被放宽为$\operatorname{Ric}_M \ge -(n-1)\delta$ (其中$\delta \ge 0$很小)。
- “直线”条件被放宽为存在一条“$\epsilon$-直线”。一条$\epsilon$-直线是一个局部概念，指的是存在一个长的[极小测地线](@entry_id:636159)段，其附近的点到该线段两端的距离之和与线段长度的差（即“过剩函数”$e(y)$）很小。

定理的结论相应地也是一个“几乎”结论：如果这些“几乎”条件满足，那么[流形](@entry_id:153038)的一个局部区域（一个球）在Gromov-Hausdorff意义下**几乎分裂**。也就是说，这个球GH-接近于一个乘积空间中的球。更精确地，对于每个$n$，存在一个函数$\Psi(n, \epsilon, \delta)$，当$\epsilon, \delta \to 0$时$\Psi \to 0$，使得若$B_2(p)$上$\operatorname{Ric} \ge -(n-1)\delta$且$B_1(p)$中存在一条$\epsilon$-直线，那么球$B_1(p)$与某个乘[积空间](@entry_id:151693)$\mathbb{R} \times Y$中的一个单位球的GH距离不超过$\Psi(n, \epsilon, \delta)$ [@problem_id:3039742]。

这种从精确的等距分裂（刚性）到近似的GH接近（稳定性）的推广，是Cheeger-Colding理论的标志性成就，它允许我们在更广泛、更现实的几何情境中应用分裂的思想 [@problem_id:3039771]。

#### 几乎锥结构

另一个体现稳定性思想的重要结果是关于锥结构的。在[Bishop-Gromov体积比较](@entry_id:189849)中，如果体积比$r^{-n}\operatorname{Vol}(B_p(r))$对于所有$r>0$都**恰好**是一个常数，那么[流形](@entry_id:153038)$M$本身就是一个度量锥。

**Cheeger-Colding几乎锥定理**（almost cone theorem）是这个刚性结果的稳定性版本。它指出，如果在一个满足Ricci曲率下界和非塌缩条件的[流形](@entry_id:153038)中，体积比$r^{-n}\operatorname{Vol}(B_p(r))$在某个尺度区间（例如$[r, 2r]$）上**几乎**是常数，那么在该尺度上，球$B_p(r)$的几何结构在GH意义下**几乎**是一个度量锥。

更精确地，对于任意$\epsilon>0$和非塌缩常数$v_0>0$，存在一个$\delta > 0$，使得如果$\operatorname{Ric}_M \ge 0$，$\operatorname{Vol}(B_p(r)) \ge v_0 r^n$，并且体积比在$[r, 2r]$上的变化小于$\delta$，那么带基点的球$(B_p(r), p)$与某个度量锥$C(Z)$中的一个球$(B_o(r), o)$的GH距离小于$\epsilon r$。这里的$Z$是一个紧致[长度空间](@entry_id:202714)，其直径满足$\operatorname{diam}(Z) \le \pi$[@problem_id:3_039_735]。这个定理揭示了体积增长率与局部几何形状之间的深刻定量联系。

### [极限空间](@entry_id:636945)的正规性

稳定性定理为我们提供了理解[极限空间](@entry_id:636945)局部几何的工具。Cheeger-Colding理论的最终成果是关于[极限空间](@entry_id:636945)正则集$\mathcal{R}$的精细正规性（regularity）的描述。

#### 正则集的[可求长性](@entry_id:202091) (Rectifiability)

[几何测度论](@entry_id:187987)中的**[可求长性](@entry_id:202091)**（rectifiability）概念，用于描述一个集合在多大程度上可以被[欧氏空间](@entry_id:138052)的片段所覆盖。一个度量空间中的[子集](@entry_id:261956)$E$被称为**可数$n$-可求长的**（countably $n$-rectifiable），如果它在$\mathcal{H}^n$-测度零的意义下可以被可数个从$\mathbb{R}^n$的[子集](@entry_id:261956)出发的[Lipschitz映射](@entry_id:199171)的像所覆盖。

Cheeger和Colding证明了一个远比这更强的结论。在非塌缩Ricci极限的背景下，正则集$\mathcal{R}$不仅是可数$n$-可求长的，而且具有定量的**双向Lipschitz[可求长性](@entry_id:202091)**（bi-Lipschitz rectifiability）。具体来说，对于任意$\varepsilon > 0$，正则集$\mathcal{R}$（除去一个$\mathcal{H}^n$-[零测集](@entry_id:157694)）可以被可数个区域$U_j$覆盖，其中每个$U_j$都存在一个到$\mathbb{R}^n$中某个[子集](@entry_id:261956)$V_j$的**$(1+\varepsilon)$-双向Lipschitz**映射$\phi_j: U_j \to V_j$。这意味着每个$U_j$的度量结构都与欧氏空间的度量结构极其相似，其距离畸变不超过$1+\varepsilon$。这表明正则集几乎完全由“几乎欧氏”的碎片拼接而成 [@problem_id:3039729]。

#### [微分](@entry_id:158718)结构与度量正规性

[可求长性](@entry_id:202091)是关于度量结构的陈述。更进一步，Cheeger和Colding证明了正则集$\mathcal{R}$上存在一个相容的[微分](@entry_id:158718)结构。最终的、也是最强的正规性结果是：

在非塌缩条件下，正则集$\mathcal{R}$是一个$C^{1,\alpha}$**黎曼$n$-[流形](@entry_id:153038)**，其中$\alpha \in (0, 1)$是一个Hölder指数。

这意味着我们可以在$\mathcal{R}$的每一点附近找到[坐标图](@entry_id:156506)册，使得[坐标变换](@entry_id:172727)函数是$C^{1,\alpha}$的。更重要的是，存在一种特殊的[坐标系](@entry_id:156346)，即**[调和坐标](@entry_id:192917)系**（harmonic coordinates，其坐标函数$u^j$满足$\Delta_g u^j = 0$），在这些[坐标系](@entry_id:156346)中，[黎曼度量张量](@entry_id:198086)的分量$g_{jk}$本身是$C^{1,\alpha}$函数。这意味着度量张量不仅连续可微，而且其一阶导数还是Hölder连续的。

这一结果的证明是该理论的技术顶峰。它依赖于在[流形](@entry_id:153038)序列上构造近似的调和函数，并利用非塌缩条件和[Ricci曲率](@entry_id:162038)下界来获得关于曲率的$L^p$积分估计。然后，通过[椭圆偏微分方程](@entry_id:178258)的[正则性理论](@entry_id:194071)，这些[曲率估计](@entry_id:192169)转化为[调和坐标](@entry_id:192917)下度量张量的$W^{2,p}$模估计，再通过[Sobolev嵌入定理](@entry_id:192380)得到$C^{1,\alpha}$模估计。这些定量的估计在GH收敛下得以保持，从而赋予了[极限空间](@entry_id:636945)的正则集一个$C^{1,\alpha}$的黎曼结构[@problem_id:3039775]。

总之，Cheeger-Colding理论通过一系列精妙的原理和机制，揭示了在Ricci曲率下界这一看似宽松的条件下，黎曼流形的[极限空间](@entry_id:636945)展现出惊人的结构和正规性。它不仅是现代黎曼几何的里程碑，也为[几何分析](@entry_id:157700)提供了强大的工具。