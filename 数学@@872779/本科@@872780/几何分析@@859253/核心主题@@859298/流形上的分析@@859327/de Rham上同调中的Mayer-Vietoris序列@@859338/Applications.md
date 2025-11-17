## 应用与跨学科联系

在前面的章节中，我们已经建立了[德拉姆上同调](@entry_id:158673)中[Mayer-Vietoris序列](@entry_id:161286)的理论基础和核心机制。现在，我们将注意力转向其实际应用，探索如何运用这一强大工具来计算各种[流形](@entry_id:153038)的上同调群，并揭示其在不同数学分支中的深刻联系。本章的目的不是重复理论，而是通过一系列精心挑选的范例，展示[Mayer-Vietoris序列](@entry_id:161286)在解决具体问题中的威力与灵活性。我们将从经典的球面计算出发，扩展到环面、亏格为$g$的[曲面](@entry_id:267450)以及[非紧空间](@entry_id:273664)，最终触及[相对上同调](@entry_id:272456)等更高级的主题。

### 原型应用：[球面的上同调](@entry_id:636700)

计算$n$维球面$S^n$的[上同调](@entry_id:160558)是[Mayer-Vietoris序列](@entry_id:161286)最基本也是最具代表性的应用之一。通过将球面分解为两个可缩的开集，我们可以利用归纳法精确确定其所有上同调群的维数。

#### 基始情形：圆周 $S^1$

我们从最简单的情形，$n=1$时的圆周$S^1$开始。考虑$S^1$的一个开覆盖$U, V$，其中$U$和$V$均为$S^1$上略长于半圆的开弧。这样，$U$和$V$本身都是可缩的（它们微分同胚于[开区间](@entry_id:157577)），而它们的交集$U \cap V$则由两个不相交的开弧组成。

根据上[同调的[同伦不变](@entry_id:157491)性](@entry_id:150428)，$U$和$V$作为[可缩空间](@entry_id:153541)，其上同调群与一个单点相同：
$H^k_{\mathrm{dR}}(U) \cong H^k_{\mathrm{dR}}(V) \cong \begin{cases} \mathbb{R}  \text{若 } k=0 \\ 0  \text{若 } k > 0 \end{cases}$

而交集$U \cap V$有两个连通分支，每个分支都是可缩的。因此，其上同调群为：
$H^k_{\mathrm{dR}}(U \cap V) \cong \begin{cases} \mathbb{R} \oplus \mathbb{R}  \text{若 } k=0 \\ 0  \text{若 } k > 0 \end{cases}$

现在，我们考察[Mayer-Vietoris序列](@entry_id:161286)的低阶部分：
$0 \to H^0_{\mathrm{dR}}(S^1) \to H^0_{\mathrm{dR}}(U) \oplus H^0_{\mathrm{dR}}(V) \xrightarrow{s_0^*} H^0_{\mathrm{dR}}(U \cap V) \xrightarrow{\delta_0} H^1_{\mathrm{dR}}(S^1) \to H^1_{\mathrm{dR}}(U) \oplus H^1_{\mathrm{dR}}(V) \to \dots$

将已知的上同调群代入，序列变为：
$0 \to H^0_{\mathrm{dR}}(S^1) \to \mathbb{R} \oplus \mathbb{R} \xrightarrow{s_0^*} \mathbb{R} \oplus \mathbb{R} \xrightarrow{\delta_0} H^1_{\mathrm{dR}}(S^1) \to 0$

由于$S^1$是连通的，$\dim H^0_{\mathrm{dR}}(S^1) = 1$。$0$阶的映射$s_0^*$将$U$和$V$上的[常函数](@entry_id:152060)对$(c_U, c_V)$映为它们在$U \cap V$上限制的差。由于$U \cap V$有两个连通分支，这个差在两个分支上都是$c_U - c_V$。因此，$s_0^*(c_U, c_V) = (c_U - c_V, c_U - c_V)$。此映射的像（image）是$\mathbb{R} \oplus \mathbb{R}$中的对角线[子空间](@entry_id:150286)，维数为1。根据序列的精确性，$\text{im}(\delta_0) \cong \text{coker}(s_0^*) = H^0_{\mathrm{dR}}(U \cap V) / \text{im}(s_0^*)$。因此，$\dim H^1_{\mathrm{dR}}(S^1) = \dim(\mathbb{R} \oplus \mathbb{R}) - \dim(\text{im}(s_0^*)) = 2 - 1 = 1$。由于$S^1$是[一维流](@entry_id:269448)形，更高阶的[上同调群](@entry_id:142450)为零。综上，我们得到$S^1$的[上同调](@entry_id:160558)维数：$\dim H^0_{\mathrm{dR}}(S^1) = 1$, $\dim H^1_{\mathrm{dR}}(S^1) = 1$。

[连接同态](@entry_id:160713)$\delta_0: H^0_{\mathrm{dR}}(U \cap V) \to H^1_{\mathrm{dR}}(S^1)$为我们提供了构造$H^1_{\mathrm{dR}}(S^1)$生成元的具体方法。交集$U\cap V$由两个不相交的开弧组成。考虑一个$0$-形式（函数）$\eta$，它在一个开弧上恒为1，在另一个上恒为0。这个函数$\eta$是闭的（$d\eta=0$），因此定义了$H^0_{\mathrm{dR}}(U \cap V)$中的一个[上同调类](@entry_id:263961)$[\eta]$。根据[连接同态](@entry_id:160713)的构造，$\delta_0([\eta])$由一个全局$1$-形式$\omega$的同调类给出。这个$\omega$可以通过[单位分解](@entry_id:150115)显式构造，并最终被证明与规范的角度形式$d\theta$（在[局部坐标](@entry_id:181200)下）同调。在$\mathbb{R}^2$的环境坐标$(x,y)$中，这个生成元可以写作$x\,dy - y\,dx$（或其常数倍）。这个形式是闭的，但它在$S^1$上的积分不为零（等于$2\pi$），因此它不是一个恰当形式。这清晰地展示了[Mayer-Vietoris序列](@entry_id:161286)如何将局部信息（交集的连通性）转化为全局[拓扑不变量](@entry_id:138526)（非平凡的1-上同调类）。

#### 一般情形：$n$维球面 $S^n$

现在我们转向一般维度的球面$S^n$（$n \ge 2$）。一个经典的策略是使用$U = S^n \setminus \{\text{北极}\}$和$V = S^n \setminus \{\text{南极}\}$来覆盖$S^n$。通过球极投影，我们知道$U$和$V$都[微分同胚](@entry_id:147249)于$\mathbb{R}^n$，因此它们都是可缩的。它们的交集$U \cap V$[同伦等价](@entry_id:150816)于赤道球面$S^{n-1}$。

根据[庞加莱引理](@entry_id:160150)，[可缩空间](@entry_id:153541)的正阶上同调群为零。因此，对于$k \ge 1$，$H^k_{\mathrm{dR}}(U) = H^k_{\mathrm{dR}}(V) = \{0\}$。而根据[同伦不变性](@entry_id:150428)，$H^k_{\mathrm{dR}}(U \cap V) \cong H^k_{\mathrm{dR}}(S^{n-1})$。

我们分情况讨论[Mayer-Vietoris序列](@entry_id:161286)：
$$ \dots \to H^{k-1}_{\mathrm{dR}}(U \cap V) \xrightarrow{\delta_{k-1}} H^k_{\mathrm{dR}}(S^n) \to H^k_{\mathrm{dR}}(U) \oplus H^k_{\mathrm{dR}}(V) \to \dots $$

*   **$k=0$**：由于$n \ge 1$时$S^n$是连通的，$\dim H^0_{\mathrm{dR}}(S^n)=1$。这也可以从序列$0 \to H^0_{\mathrm{dR}}(S^n) \to H^0_{\mathrm{dR}}(U) \oplus H^0_{\mathrm{dR}}(V) \to H^0_{\mathrm{dR}}(U \cap V)$中得出。由于$U, V, U \cap V$都是连通的（因为$n-1 \ge 1$），该片段变为$0 \to \mathbb{R} \to \mathbb{R}\oplus\mathbb{R} \to \mathbb{R}$。分析映射可知，中心映射的核（kernel）是一维的，这迫使$H^0_{\mathrm{dR}}(S^n)$的维数为1。

*   **$0  k  n$**：序列的相关部分为$H^{k-1}_{\mathrm{dR}}(U) \oplus H^{k-1}_{\mathrm{dR}}(V) \to H^{k-1}_{\mathrm{dR}}(U \cap V) \xrightarrow{\delta_{k-1}} H^k_{\mathrm{dR}}(S^n) \to H^k_{\mathrm{dR}}(U) \oplus H^k_{\mathrm{dR}}(V)$。
    由于$k \ge 1$，两端的项$H^{k-1}_{\mathrm{dR}}(U) \oplus H^{k-1}_{\mathrm{dR}}(V)$和$H^k_{\mathrm{dR}}(U) \oplus H^k_{\mathrm{dR}}(V)$均为零（除了$k=1$时$H^0$项不为零，但该情况的分析显示映射是满射）。这导致了同构关系：$H^k_{\mathrm{dR}}(S^n) \cong H^{k-1}_{\mathrm{dR}}(U \cap V) \cong H^{k-1}_{\mathrm{dR}}(S^{n-1})$。
    假设我们已经知道$S^{n-1}$的上同调（[归纳假设](@entry_id:139767)），即$\dim H^j_{\mathrm{dR}}(S^{n-1})$仅在$j=0$和$j=n-1$时为1。对于$1  k  n$，我们有$0  k-1  n-1$。因此，$H^{k-1}_{\mathrm{dR}}(S^{n-1}) = \{0\}$，从而$H^k_{\mathrm{dR}}(S^n) = \{0\}$。对于$k=1$，由于$n \ge 2$，$H^0_{\mathrm{dR}}(S^{n-1}) \cong \mathbb{R}$。但序列的前一部分显示，从$H^0(U)\oplus H^0(V)$到$H^0(U \cap V)$的映射是满射，导致[连接同态](@entry_id:160713)$\delta_0$是零映射，因此$H^1_{\mathrm{dR}}(S^n)$也是零。综上，对于$0  k  n$，$H^k_{\mathrm{dR}}(S^n) = \{0\}$。

*   **$k=n$**：同理，我们有同构$H^n_{\mathrm{dR}}(S^n) \cong H^{n-1}_{\mathrm{dR}}(S^{n-1})$。根据[归纳假设](@entry_id:139767)，$\dim H^{n-1}_{\mathrm{dR}}(S^{n-1}) = 1$，因此$\dim H^n_{\mathrm{dR}}(S^n) = 1$。

结合所有情况，我们通过归纳法证明了$S^n$（$n \ge 1$）的[上同调群](@entry_id:142450)为：
$H^k_{\mathrm{dR}}(S^n) \cong \begin{cases} \mathbb{R}  \text{若 } k=0 \text{ 或 } k=n \\ \{0\}  \text{其他情况} \end{cases}$
这个结果可以用克罗内克$\delta$符号简洁地表示为 $\dim H^k_{\mathrm{dR}}(S^n) = \delta_{k,0} + \delta_{k,n}$。

一个直接的推论是关于球面的欧拉示性数$\chi(S^n)$。[欧拉示性数](@entry_id:152513)定义为贝蒂数的交错和，即$\chi(M) = \sum_k (-1)^k \dim H^k_{\mathrm{dR}}(M)$。对于球面，我们得到：
$\chi(S^n) = (-1)^0 \dim H^0_{\mathrm{dR}}(S^n) + (-1)^n \dim H^n_{\mathrm{dR}}(S^n) = 1 + (-1)^n$。
这个结果也可以通过分析[Mayer-Vietoris序列](@entry_id:161286)的维数关系得到。长正合序列的一个代数性质是，各项维数的交错和为零。应用于我们的覆盖，这导出了一个优美的加性公式：$\chi(S^n) = \chi(U) + \chi(V) - \chi(U \cap V)$。代入$\chi(U)=\chi(V)=\chi(\mathbb{R}^n)=1$和$\chi(U \cap V)=\chi(S^{n-1})$，我们得到[递推关系](@entry_id:189264)$\chi(S^n) = 2 - \chi(S^{n-1})$。结合基始情形$\chi(S^0)=2$（两个点），我们可以解出同样的[封闭形式表达式](@entry_id:267458)。

### 扩展到其他空间与跨学科联系

[Mayer-Vietoris序列](@entry_id:161286)的威力远不止于球面。它适用于任何可以用合适的开集覆盖的[流形](@entry_id:153038)，使其成为计算几何与拓扑学中众多空间上同调的通用引擎。

#### 乘[积空间](@entry_id:151693)：[2-环面](@entry_id:265991) $T^2$

考虑2-维环面$T^2 = S^1 \times S^1$。我们可以选择一个巧妙的开覆盖来分解它。令$U = S^1 \times (S^1 \setminus \{p\})$和$V = (S^1 \setminus \{q\}) \times S^1$，其中$p,q$是$S^1$上的点。这里，$U$同伦于第一个$S^1$因子，而$V$同伦于第二个$S^1$因子。它们的交集$U \cap V = (S^1 \setminus \{q\}) \times (S^1 \setminus \{p\})$同伦于$\mathbb{R} \times \mathbb{R}$，因而是可缩的。

我们有$H^1_{\mathrm{dR}}(U) \cong H^1_{\mathrm{dR}}(S^1) \cong \mathbb{R}$，并且$H^1_{\mathrm{dR}}(V) \cong H^1_{\mathrm{dR}}(S^1) \cong \mathbb{R}$。而交集$U \cap V$是可缩的，所以$H^1_{\mathrm{dR}}(U \cap V)=\{0\}$。[Mayer-Vietoris序列](@entry_id:161286)中围绕$H^1_{\mathrm{dR}}(T^2)$的部分是：
$$ \dots \to H^0_{\mathrm{dR}}(U \cap V) \xrightarrow{\delta_0} H^1_{\mathrm{dR}}(T^2) \xrightarrow{r_1^*} H^1_{\mathrm{dR}}(U) \oplus H^1_{\mathrm{dR}}(V) \xrightarrow{s_1^*} H^1_{\mathrm{dR}}(U \cap V) \to \dots $$
代入我们知道的群，序列变为：
$$ \dots \to \mathbb{R} \xrightarrow{\delta_0} H^1_{\mathrm{dR}}(T^2) \xrightarrow{r_1^*} \mathbb{R} \oplus \mathbb{R} \to 0 $$
从右侧的$0$和序列的精确性可知，$r_1^*$是满射。同时，对$0$阶上同调的分析表明$\delta_0$是零映射。这意味着$r_1^*$的核是零，因此$r_1^*$是[单射](@entry_id:183792)。一个既是[单射](@entry_id:183792)又是满射的线性映射是同构。因此，我们得到了一个重要的同构：
$H^1_{\mathrm{dR}}(T^2) \cong H^1_{\mathrm{dR}}(U) \oplus H^1_{\mathrm{dR}}(V) \cong \mathbb{R} \oplus \mathbb{R}$。
这表明环面的第一贝蒂数$b_1(T^2) = 2$。这两个维度直观地对应于环面上的两个独立的“洞”或“圈”。这个例子展示了[Mayer-Vietoris序列](@entry_id:161286)如何优雅地将乘积空间的拓扑分解为各个因子的贡献。

#### 拓扑构造：[连通和](@entry_id:263574)

[Mayer-Vietoris序列](@entry_id:161286)在处理“切粘贴”拓扑操作（如[连通和](@entry_id:263574)）时尤其有效。考虑一个亏格为2的[曲面](@entry_id:267450)$X_2$，它可以看作是两个环面$T_1$和$T_2$的[连通和](@entry_id:263574)$T_1 \# T_2$。构造过程是从每个环面上挖去一个小开圆盘，然后将得到的带边界的[曲面](@entry_id:267450)沿着圆形边界粘合起来。

我们可以将$X_2$分解为两个开集$U$和$V$，其中$U$是$T_1$挖掉一个圆盘再稍微“加厚”到粘合区域，而$V$是$T_2$挖掉一个圆盘再稍微“加厚”。这两个开集$U$和$V$都同伦等价于两个圆的[楔和](@entry_id:270607)（bouquet of two circles），即$S^1 \vee S^1$。它们的交集$U \cap V$则是一个开圆柱体，同伦等价于一个圆$S^1$。我们已知$\dim H^1_{\mathrm{dR}}(S^1 \vee S^1) = 2$和$\dim H^1_{\mathrm{dR}}(S^1) = 1$。通过分析可以证明，从$H^1_{\mathrm{dR}}(U)$和$H^1_{\mathrm{dR}}(V)$到$H^1_{\mathrm{dR}}(U\cap V)$的限制映射都是零映射，因此$s_1^*$为零映射。再结合$0$阶部分的分析可知$\delta_0$为零映射，这使得$r_1^*$是[单射](@entry_id:183792)。于是序列$0 \to H^1_{\mathrm{dR}}(X_2) \xrightarrow{r_1^*} H^1_{\mathrm{dR}}(U) \oplus H^1_{\mathrm{dR}}(V) \xrightarrow{s_1^*=0} H^1_{\mathrm{dR}}(U \cap V)$成为一个短[正合序列](@entry_id:151503)，给出$H^1_{\mathrm{dR}}(X_2) \cong H^1_{\mathrm{dR}}(U) \oplus H^1_{\mathrm{dR}}(V) \cong \mathbb{R}^2 \oplus \mathbb{R}^2$，其维数为$4$。这直观地反映了亏格为2的[曲面](@entry_id:267450)有4个独立的1-循环。

#### [非紧空间](@entry_id:273664)

[Mayer-Vietoris序列](@entry_id:161286)同样适用于[非紧空间](@entry_id:273664)。一个重要的例子是计算穿孔[欧氏空间](@entry_id:138052)$\mathbb{R}^n \setminus \{0\}$的[上同调](@entry_id:160558)。这个空间同伦等价于球面$S^{n-1}$，因此它们的[上同调群](@entry_id:142450)是同构的。我们可以通过[Mayer-Vietoris序列](@entry_id:161286)直接证明这一点。令$U = \{x \in \mathbb{R}^n : 0  |x|  2\}$，$V = \{x \in \mathbb{R}^n : |x| > 1\}$。那么$U \cup V = \mathbb{R}^n \setminus \{0\}$。$U$同伦等价于$S^{n-1}$，$V$[同伦等价](@entry_id:150816)于一个点（即可缩），而它们的交集$U \cap V = \{x : 1  |x|  2\}$也同伦等价于$S^{n-1}$。通过分析[Mayer-Vietoris序列](@entry_id:161286)中的映射，可以推导出对于$k \ge 1$，$H^k_{\mathrm{dR}}(\mathbb{R}^n \setminus \{0\}) \cong H^k_{\mathrm{dR}}(S^{n-1})$。因此，$\mathbb{R}^n \setminus \{0\}$的非平凡上同调仅出现在$k=n-1$阶，且$\dim H^{n-1}_{\mathrm{dR}}(\mathbb{R}^n \setminus \{0\}) = 1$。

这个1维的[上同调群](@entry_id:142450)有一个非常具体的代表元，它在物理学中尤为重要。这个生成元是$(n-1)$-形式，通常被称为“[立体角](@entry_id:154756)形式”。通过将$S^{n-1}$上的标准[体积形式](@entry_id:203000)经过径向投影$r(x) = x/\|x\|$[拉回](@entry_id:160816)到$\mathbb{R}^n \setminus \{0\}$，我们可以得到该形式的显式表达式：
$$ \omega = C_n \sum_{i=1}^{n} (-1)^{i-1} \frac{x_{i}}{\|x\|^{n}} \, dx_{1} \wedge \cdots \wedge \widehat{dx_{i}} \wedge \cdots \wedge dx_{n} $$
其中$C_n$是[归一化常数](@entry_id:752675)。这个形式是闭的但不是正合的，它在任何包围原点的$(n-1)$-维球面上的积分都是非零的。在$n=3$时，这与[静电学](@entry_id:140489)中[点电荷](@entry_id:263616)的[电场](@entry_id:194326)有关，其[通量积分](@entry_id:138365)（[高斯定律](@entry_id:141493)）揭示了中心“[奇点](@entry_id:137764)”的存在。

另一个有趣的[非紧空间](@entry_id:273664)例子是挖掉$n$个点的平面$M_n = \mathbb{R}^2 \setminus \{p_1, \dots, p_n\}$。我们可以通过归纳法和巧妙地应用[Mayer-Vietoris序列](@entry_id:161286)来计算其第一贝蒂数$b_1(M_n)$。假设这些点不共线，我们可以画一条直线$L$将点$p_n$与其余$n-1$个点分开。设$H_1$和$H_2$是由$L$分开的两个开半平面，使得$\{p_1, \dots, p_{n-1}\} \subset H_1$且$p_n \in H_2$。我们构造开覆盖$M_n = U \cup V$，其中$U$是$H_1$加上$L$的一个邻域（并从$\mathbb{R}^2$中挖掉相应的点），$V$是$H_2$加上$L$的同一个邻域（也挖掉相应的点）。这样构造的$U$同伦等价于挖掉$n-1$个点的平面$M_{n-1}$，$V$同伦等价于挖掉一个点的平面$M_1$，而它们的交集$U \cap V$是一个开带，是可缩的。[Mayer-Vietoris序列](@entry_id:161286)的相关部分给出$H^1(M_n) \cong H^1(U) \oplus H^1(V)$。根据[归纳假设](@entry_id:139767)$b_1(M_{n-1}) = n-1$和基础情况$b_1(M_1)=1$，我们得到递推关系$b_1(M_n) = b_1(M_{n-1}) + b_1(M_1) = (n-1) + 1 = n$。这直观地表明，每个挖掉的点都贡献了一个“洞”，可以被一个独立的闭合[1-形式](@entry_id:270392)环绕积分而不为零。

### 高级主题与展望

#### [紧支撑上同调](@entry_id:634085)

$S^n$的上同调与$\mathbb{R}^n$的[紧支撑上同调](@entry_id:634085)$H_{\mathrm{dR},c}^*(\mathbb{R}^n)$之间存在深刻的对偶关系。可以将$S^n$看作是$\mathbb{R}^n$的[单点紧化](@entry_id:153786)$S^n \cong \mathbb{R}^n \cup \{\infty\}$。存在一个长正合序列，将$\mathbb{R}^n$的[紧支撑上同调](@entry_id:634085)与$S^n$的（普通）[上同调](@entry_id:160558)联系起来。利用我们已知的$S^n$的[上同调](@entry_id:160558)结果，这个序列可以反过来用于计算$H_{\mathrm{dR},c}^*(\mathbb{R}^n)$。结果表明：
$$ H_{\mathrm{dR},c}^k(\mathbb{R}^n) \cong \begin{cases} \mathbb{R}  \text{若 } k=n \\ \{0\}  \text{其他情况} \end{cases} $$
$H_{\mathrm{dR},c}^n(\mathbb{R}^n)$的非平凡性与在$\mathbb{R}^n$上对一个[紧支撑](@entry_id:276214)$n$-形式进行积分的能力直接相关，这是[庞加莱对偶](@entry_id:161676)性的一个体现。

#### [相对上同调](@entry_id:272456)与[带边流形](@entry_id:159788)

当处理[带边流形](@entry_id:159788)时，标准的[Mayer-Vietoris序列](@entry_id:161286)需要修正，以妥善处理边界上的行为。这自然地引出了[相对上同调](@entry_id:272456)$H^*(X, A)$的概念，它研究的是在[子空间](@entry_id:150286)$A$上为零的微分形式。对于[带边流形](@entry_id:159788)$M$及其上的[开覆盖](@entry_id:140020)$U, V$，正确的工具是相对[Mayer-Vietoris序列](@entry_id:161286)，它涉及[相对上同调](@entry_id:272456)群，如$H^k(U \cup V, \partial M \cap (U \cup V))$等。使用相对形式的关键在于，它保证了在应用斯托克斯定理时边界项自动消失，从而使得许多在无边[流形](@entry_id:153038)上的证明可以推广。

一个典型的应用是计算[相对上同调](@entry_id:272456)群$H^k(D^n, S^{n-1})$，其中$D^n$是$n$维[闭球](@entry_id:157850)，$S^{n-1}$是其边界。通过将$D^n$分解为两个重叠的“半球”邻域，并应用相对[Mayer-Vietoris序列](@entry_id:161286)，可以建立一个[递推关系](@entry_id:189264)$H^{k+1}(D^n, S^{n-1}) \cong H^k(D^{n-1}, S^{n-2})$。最终解出：
$$ H^k(D^n, S^{n-1}) \cong \begin{cases} \mathbb{R}  \text{若 } k=n \\ \{0\}  \text{其他情况} \end{cases} $$
这个结果本身是拓扑学中的一个基石，它在证明[庞加莱对偶](@entry_id:161676)性、Lefschetz[不动点定理](@entry_id:143811)等核心结果中扮演着重要角色。这展示了[Mayer-Vietoris序列](@entry_id:161286)作为一种思想工具，其适用范围可以延伸到更广阔和更抽象的数学领域。

总而言之，[Mayer-Vietoris序列](@entry_id:161286)不仅是一个计算公式，更是一种将“局部”与“全局”联系起来的哲学思想。通过将复杂的[空间分解](@entry_id:755142)为更简单的部分，它使我们能够系统地推导出空间的全局[拓扑不变量](@entry_id:138526)，深刻地揭示了[微分](@entry_id:158718)[流形](@entry_id:153038)的结构。