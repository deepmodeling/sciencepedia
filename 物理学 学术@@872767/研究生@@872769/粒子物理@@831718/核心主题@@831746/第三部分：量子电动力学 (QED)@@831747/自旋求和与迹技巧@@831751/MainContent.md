## 引言
在[粒子物理学](@entry_id:145253)的宏伟画卷中，理论预测与实验观测的精确对比是检验我们对自然基本规律理解的最终标准。然而，从一个理论的拉格朗日量出发，推导出可供实验测量的物理量，如散射截面或[粒子衰变宽度](@entry_id:198040)，是一条充满计算挑战的道路。一个核心难题在于，大多数实验涉及非极化的粒子束，且无法追踪末态粒子的自旋状态。因此，理论计算必须对所有可能的自旋构型进行平均（初态）和求和（末态），直接处理[旋量](@entry_id:158054)分量的代数运算极为繁琐且容易出错。

本文旨在系统介绍一套强大而优雅的解决方案：**[自旋求和](@entry_id:162099)与迹技术 (Spin Sums and Trace Techniques)**。通过本篇文章，你将深入理解这一粒子物理学家的基本功。

- **第一章“原理与机制”** 将揭示迹技术如何巧妙地将复杂的旋量代数转化为[协变](@entry_id:634097)的矩阵迹运算。
- **第二章“应用与跨学科关联”** 将展示该技术在标准模型、新物理探索乃至核物理等领域的广泛应用，连接理论与唯象。
- **最后，第三章“动手实践”** 将通过具体的计算问题，巩固你对这些核心技能的掌握。

## 原理与机制

在粒子物理学的探索中，理论预测与实验观测的对比是推动科学进步的核心环节。绝大多数对撞机实验涉及的是非极化的初态粒子束（例如，质子对撞），并且通常不会或无法测量末态所有粒子的自旋状态。因此，为了得到能够与实验数据直接比较的物理量，如散射截面或[衰变宽度](@entry_id:153846)，理论计算必须对初态自旋进行平均，并对末态自旋进行求和。直接对旋量（spinor）的各个分量进行繁琐的代数运算是极其低效且容易出错的。幸运的是，[量子场论](@entry_id:138177)为我们提供了一套强大而优雅的协变计算方法——**迹技术 (trace techniques)**。本章将系统阐述其基本原理和关键机制。

### 为何需要[自旋求和](@entry_id:162099)与迹技巧

考虑一个一般的 $2 \to n$ 散射过程，其散射振幅（matrix element）$\mathcal{M}$ 是初态和末态[粒子自旋](@entry_id:142910)的函数。一个非极化的散射截面 $\sigma$ 的计算涉及到对[散射振幅](@entry_id:155369)的模方 $|\mathcal{M}|^2$ 进行如下操作：

1.  **对末态[自旋求和](@entry_id:162099) ($\sum_{s_f}$)**：由于我们不观测末态粒子的自旋，我们必须将所有可能的末态自旋构型所对应的几率加起来。
2.  **对初态自旋平均 ($\frac{1}{(2s_A+1)(2s_B+1)}\sum_{s_i}$)**：由于初态粒子是无规取向的，我们需要计算所有初态自旋构型的平均贡献。对于自旋为 $1/2$ 的[费米子](@entry_id:146235)，这个平均因子是 $\frac{1}{2 \times 2} = \frac{1}{4}$。

综合起来，我们需要计算的量是**自旋平均的振幅平方**，记为 $\overline{|\mathcal{M}|^2}$：
$$
\overline{|\mathcal{M}|^2} = \frac{1}{\text{初态自旋自由度}} \sum_{\text{初态自旋}} \sum_{\text{末态自旋}} |\mathcal{M}|^2
$$
迹技术，有时也被称为**Casimir技巧 (Casimir's trick)**，其精髓在于将对[旋量](@entry_id:158054)分量的直接求和，转化为对狄拉克 $\gamma$ 矩阵乘积的求迹（trace）运算。这不仅极大地简化了计算，而且全程保持了[洛伦兹协变性](@entry_id:161987)。

### 核心技术：从旋量到迹

迹技术的核心在于**[自旋求和](@entry_id:162099)投影算符**。对于一个质量为 $m$，[四动量](@entry_id:264378)为 $p$ 的自旋 $1/2$ [费米子](@entry_id:146235)，其正频解（粒子）$u(p, s)$ 和负频解（反粒子）$v(p, s)$ 的[自旋求和](@entry_id:162099)公式构成了一座桥梁，将旋量空间与算符空间联系起来：

$$
\sum_s u(p,s) \bar{u}(p,s) = \not p + m
$$
$$
\sum_s v(p,s) \bar{v}(p,s) = \not p - m
$$

其中 $\not p = p_\mu \gamma^\mu$ 是[费曼斜杠表示法](@entry_id:147031)，而 $\bar{u} = u^\dagger \gamma^0$。这两个恒等式是[狄拉克方程](@entry_id:147922)的直接推论，它们本质上是向相应动量的正能量和负能量解[子空间](@entry_id:150286)投影的算符。

让我们看这是如何工作的。考虑一个典型的[费米子](@entry_id:146235)[散射振幅](@entry_id:155369)，它具有“旋量三明治”结构 $\mathcal{M} = \bar{u}(p_3) \Gamma u(p_1)$，其中 $\Gamma$ 是由 $\gamma$ 矩阵构成的某个算符。其模方为：
$$
|\mathcal{M}|^2 = \mathcal{M} \mathcal{M}^* = \left( \bar{u}(p_3) \Gamma u(p_1) \right) \left( \bar{u}(p_3) \Gamma u(p_1) \right)^*
$$
利用关系 $(\bar{u}_A \Gamma u_B)^* = u_B^\dagger \Gamma^\dagger \bar{u}_A^{\dagger T} = \bar{u}_B \gamma^0 \Gamma^\dagger \gamma^0 u_A = \bar{u}_B \bar{\Gamma} u_A$，其中 $\bar{\Gamma} = \gamma^0 \Gamma^\dagger \gamma^0$，我们可以将上式写成：
$$
|\mathcal{M}|^2 = \left( \bar{u}(p_3) \Gamma u(p_1) \right) \left( \bar{u}(p_1) \bar{\Gamma} u(p_3) \right)
$$
注意，现在表达式变成了 $\bar{u} \dots u \bar{u} \dots u$ 的形式。对初末态[自旋求和](@entry_id:162099)时，我们就可以插入[自旋求和](@entry_id:162099)投影算符：
\begin{align*}
\sum_{s_1, s_3} |\mathcal{M}|^2  &= \sum_{s_1, s_3} \left( \bar{u}(p_3, s_3) \Gamma u(p_1, s_1) \right) \left( \bar{u}(p_1, s_1) \bar{\Gamma} u(p_3, s_3) \right) \\
 &= \sum_{s_3} \bar{u}(p_3, s_3) \Gamma \left( \sum_{s_1} u(p_1, s_1) \bar{u}(p_1, s_1) \right) \bar{\Gamma} u(p_3, s_3) \\
 &= \sum_{s_3} \bar{u}(p_3, s_3) \Gamma (\not p_1 + m_1) \bar{\Gamma} u(p_3, s_3)
\end{align*}
这个表达式依然包含 $\bar{u}_3$ 和 $u_3$。但是，我们可以利用[迹的循环性质](@entry_id:153103) $\operatorname{Tr}(AB) = \sum_{i,j} A_{ij} B_{ji}$。上式可以被看作是矩阵乘积 $\left[ \Gamma (\not p_1 + m_1) \bar{\Gamma} \right]$ 与矩阵 $u(p_3, s_3) \bar{u}(p_3, s_3)$ 的乘积的迹。于是：
\begin{align*}
\sum_{s_1, s_3} |\mathcal{M}|^2  &= \operatorname{Tr} \left[ \Gamma (\not p_1 + m_1) \bar{\Gamma} \left( \sum_{s_3} u(p_3, s_3) \bar{u}(p_3, s_3) \right) \right] \\
 &= \operatorname{Tr} \left[ \Gamma (\not p_1 + m_1) \bar{\Gamma} (\not p_3 + m_3) \right]
\end{align*}
至此，我们成功地将关于[旋量](@entry_id:158054)分量的复杂求和，转化为了一个关于 $4 \times 4$ 狄拉克[矩阵乘积的迹](@entry_id:150319)。这个过程可以推广到任意数量的[费米子](@entry_id:146235)流。

例如，在[Drell-Yan过程](@entry_id:154547)中，夸克-反夸克[对湮灭](@entry_id:154046)产生一个[虚光子](@entry_id:184381) $q(p_a) \bar{q}(p_b) \to \gamma^*(q)$ [@problem_id:200396]。描述这个过程的[强子](@entry_id:158325)张量 $H^{\mu\nu}$ 需要对初态夸克和反夸克的自旋进行平均。其振幅为 $\mathcal{M}^\mu = \bar{v}_{s_b}(p_b) \gamma^\mu u_{s_a}(p_a)$。自旋平均后的张量计算就变成了一个典型的迹问题：
\begin{align*}
H^{\mu\nu}  &= \frac{1}{4} \sum_{s_a, s_b} \mathcal{M}^\mu (\mathcal{M}^{\nu})^* \\
 &= \frac{1}{4} \sum_{s_a, s_b} \left(\bar{v}_{s_b}(p_b) \gamma^\mu u_{s_a}(p_a)\right) \left(\bar{u}_{s_a}(p_a) \gamma^\nu v_{s_b}(p_b)\right) \\
 &= \frac{1}{4} \operatorname{Tr} \left[ \gamma^\mu \left(\sum_{s_a} u_{s_a}(p_a) \bar{u}_{s_a}(p_a)\right) \gamma^\nu \left(\sum_{s_b} v_{s_b}(p_b) \bar{v}_{s_b}(p_b)\right) \right] \\
 &= \frac{1}{4} \operatorname{Tr} \left[ \gamma^\mu (\not p_a + m_q) \gamma^\nu (\not p_b - m_q) \right]
\end{align*}
这个表达式只涉及[四动量](@entry_id:264378)和 $\gamma$ 矩阵，所有的[旋量](@entry_id:158054)都消失了。剩下的工作就是计算这个迹。

### [狄拉克矩阵](@entry_id:155614)迹的计算

一旦将问题转化为迹的形式，我们就需要一套代数规则来求解它。所有这些规则都源于 $\gamma$ 矩阵的定义——[Clifford代数](@entry_id:137625) $\{\gamma^\mu, \gamma^\nu\} = 2g^{\mu\nu}$。

#### 基本[迹恒等式](@entry_id:188149)

- **迹的循环性**: $\operatorname{Tr}(A B C) = \operatorname{Tr}(B C A) = \operatorname{Tr}(C A B)$。
- **奇数 $\gamma$ [矩阵的迹](@entry_id:139694)为零**: $\operatorname{Tr}(\gamma^{\mu_1} \dots \gamma^{\mu_{2n+1}}) = 0$。这是一个极其有用的性质，可以迅速排除许多项。
- **基本迹**:
  $$ \operatorname{Tr}(I) = 4 \quad (\text{在4维时空}) $$
  $$ \operatorname{Tr}(\gamma^\mu \gamma^\nu) = 4 g^{\mu\nu} $$
  $$ \operatorname{Tr}(\gamma^\mu \gamma^\nu \gamma^\rho \gamma^\sigma) = 4 (g^{\mu\nu}g^{\rho\sigma} - g^{\mu\rho}g^{\nu\sigma} + g^{\mu\sigma}g^{\nu\rho}) $$
  更高阶的迹（如6个、8个$\gamma$矩阵）也可以被计算出来，但通常可以通过重复使用[Clifford代数](@entry_id:137625)将其化简为更低阶的迹。

#### 包含 $\gamma_5$ 的迹

第五个 $\gamma$ 矩阵 $\gamma_5 = i\gamma^0\gamma^1\gamma^2\gamma^3$ 在描述宇称破缺的[弱相互作用](@entry_id:157579)中至关重要。它的性质如下：
- $(\gamma_5)^2 = 1$
- $\{\gamma^\mu, \gamma_5\} = 0$
- $\operatorname{Tr}(\gamma_5) = 0$
- $\operatorname{Tr}(\gamma^\mu \gamma^\nu \gamma_5) = 0$
- **四个 $\gamma$ 矩阵与 $\gamma_5$ 的迹**: 这是最关键的恒等式之一，它将迹与完全反对称的[Levi-Civita符号](@entry_id:155382)联系起来。
  $$ \operatorname{Tr}(\gamma^\mu \gamma^\nu \gamma^\rho \gamma^\sigma \gamma_5) = -4i \epsilon^{\mu\nu\rho\sigma} $$
  其中 $\epsilon^{0123} = +1$。注意，由于[Levi-Civita符号](@entry_id:155382)的完全反对称性，如果四个指标 $\mu, \nu, \rho, \sigma$ 中有任何两个相同，迹就为零。

#### 应用实例：一个假设的[μ子衰变](@entry_id:160958)

让我们通过一个具体的例子来演练这些技巧。考虑一个假设的[μ子衰变](@entry_id:160958)过程 $\mu^-(p) \to e^-(k_1) + \bar{\nu}_e(k_2) + \nu_\mu(k_3)$，其相互作用由有效[拉格朗日量](@entry_id:174593) $\mathcal{L}_{int} = G (\bar{\psi}_{\nu_\mu} \gamma^\alpha \psi_\mu) (\bar{\psi}_e \gamma_\alpha \gamma_5 \psi_{\nu_e})$ 描述 [@problem_id:200388]。这个相互作用包含一个矢量流和一个[轴矢量](@entry_id:196296)流。

振幅为 $\mathcal{M} = G [\bar{u}(k_3)\gamma^\alpha u(p)] [\bar{u}(k_1)\gamma_\alpha\gamma_5 v(k_2)]$。我们假设除μ子外所有粒子均无质量。自旋平均的振幅平方为：
$$
\overline{|\mathcal{M}|^2} = \frac{1}{2} G^2 \sum_{\text{spins}} [\bar{u}_3\gamma^\alpha u_p][\bar{u}_1\gamma_\alpha\gamma_5 v_2] [\bar{v}_2\gamma_\beta\gamma_5 u_1][\bar{u}_p\gamma^\beta u_3]
$$
通过重新[排列](@entry_id:136432)并插入[自旋求和](@entry_id:162099)算符，我们将得到两个独立的迹：
$$
\overline{|\mathcal{M}|^2} = \frac{G^2}{2} \operatorname{Tr}[(\not p + m_\mu)\gamma^\beta \not k_3 \gamma^\alpha] \operatorname{Tr}[\not k_1 \gamma_\alpha \gamma_5 \not k_2 \gamma_\beta \gamma_5]
$$
第一个迹 $T_1^{\alpha\beta} = \operatorname{Tr}[(\not p + m_\mu)\gamma^\beta \not k_3 \gamma^\alpha]$ 中，包含 $m_\mu$ 的项是 $\operatorname{Tr}[m_\mu \gamma^\beta \not k_3 \gamma^\alpha]$，它含有奇数个$\gamma$矩阵，因此为零。所以 $T_1^{\alpha\beta} = \operatorname{Tr}[\not p \gamma^\beta \not k_3 \gamma^\alpha] = 4(p^\beta k_3^\alpha - p \cdot k_3 g^{\beta\alpha} + p^\alpha k_3^\beta)$。

第二个迹为 $T_{2, \alpha\beta} = \operatorname{Tr}[\not k_1 \gamma_\alpha \gamma_5 \not k_2 \gamma_\beta \gamma_5]$。为了计算它，我们利用[迹的循环性质](@entry_id:153103)以及 $\gamma_5$ 的属性。通过循环性，我们可以将表达式中的一个 $\gamma_5$ 移动到另一端与另一个 $\gamma_5$ 相邻。在移动过程中，该 $\gamma_5$ 会穿过两个伽马矩阵（在 $\not k_2$ 中有一个，以及 $\gamma_\beta$），每次穿过都会根据[反对易关系](@entry_id:153815) $\{\gamma^\mu, \gamma_5\}=0$ 产生一个负号，因此总的符号变化是 $(-1)^2=1$。于是，利用 $(\gamma_5)^2=1$：
$$
T_{2, \alpha\beta} = \operatorname{Tr}[\not k_1 \gamma_\alpha \not k_2 \gamma_\beta (\gamma_5)^2] = \operatorname{Tr}[\not k_1 \gamma_\alpha \not k_2 \gamma_\beta] = 4(k_{1\alpha}k_{2\beta} - k_1 \cdot k_2 g_{\alpha\beta} + k_{1\beta}k_{2\alpha})
$$
最后，将两个[张量缩并](@entry_id:193373) $T_1^{\alpha\beta} T_{2, \alpha\beta}$，经过一番代数运算后，便可得到最终的物理结果，它只依赖于粒子[四动量](@entry_id:264378)之间的[内积](@entry_id:158127)。

### 进阶主题与应用

掌握了基本技巧后，我们可以将其应用于更复杂的场景。

#### 矢量[玻色子](@entry_id:138266)的极化求和

当末态包含矢量[玻色子](@entry_id:138266)（如[光子](@entry_id:145192) $\gamma$、W 或 Z [玻色子](@entry_id:138266)）时，我们也需要对其极化（polarization）进行求和。
- 对于**无质量**的矢量[玻色子](@entry_id:138266)（[光子](@entry_id:145192)），在费曼规范下，极化求和公式为：
  $$ \sum_{\lambda=1,2} \epsilon_\mu(k, \lambda) \epsilon_\nu^*(k, \lambda) = -g_{\mu\nu} $$
- 对于**有质量**的矢量[玻色子](@entry_id:138266)（如 Z [玻色子](@entry_id:138266)，质量为 $M_Z$），它有三个物理极化态，求和公式为：
  $$ \sum_{\lambda=1,2,3} \epsilon_\mu(k, \lambda) \epsilon_\nu^*(k, \lambda) = -g_{\mu\nu} + \frac{k_\mu k_\nu}{M_Z^2} $$
这个求和张量需要与从[费米子](@entry_id:146235)流计算出的迹张量进行缩并。例如，在一个重[马约拉纳中微子](@entry_id:160033)衰变为[Z玻色子](@entry_id:162007)和轻中微子的过程中 $N \to Z\nu$ [@problem_id:200381]，计算出的[费米子](@entry_id:146235)部分迹张量 $T^{\mu\nu}$ 就要与[Z玻色子](@entry_id:162007)的极化张量 $P_{\mu\nu} = -g_{\mu\nu} + k_\mu k_\nu/M_Z^2$ 缩并，即 $T^{\mu\nu}P_{\mu\nu}$，才能得到完整的自旋/极化求和结果。

#### [圈图计算](@entry_id:751472)中的迹技术

迹技术在更高阶的圈图（loop）计算中同样不可或缺。此时，迹的内部不再仅仅是外部粒子的动量，还包含了圈图中的虚粒子动量，计算结果通常是关于圈动量的一个张量，之后还需要对圈动量进行积分。

例如，在希格斯玻色子通过胶子聚变产生 ($gg \to H$) 的主要机制中，该过程由一个重夸克（主要是顶夸克）圈图介导 [@problem_id:200378]。在低能极限下（$k_1, k_2 \to 0$），两个图贡献的分子求和后，需要计算的迹为：
$$
N_{\mu\nu} \propto \operatorname{Tr}\left[ (\gamma_\mu (\not p+m) \gamma_\nu + \gamma_\nu (\not p+m) \gamma_\mu) (\not p+m)^2 \right]
$$
其中 $p$ 是圈动量，$m$ 是[顶夸克质量](@entry_id:160842)。通过展开并使用[迹恒等式](@entry_id:188149)，这个复杂的表达式可以被计算出来，结果是圈动量 $p$ 和[顶夸克质量](@entry_id:160842) $m$ 的一个张量函数。

另一个有趣的例子是[光子](@entry_id:145192)-[光子散射](@entry_id:194085) $\gamma\gamma \to \gamma\gamma$ [@problem_id:200393]，其领头阶贡献来自于一个电子[圈图](@entry_id:149287)（box diagram）。其中一个图的贡献涉及到包含八个$\gamma$矩阵的迹。然而，利用外部[光子](@entry_id:145192)的[运动学](@entry_id:173318)约束条件，即 $k^2=0$ 和横截条件 $k \cdot \epsilon = 0$，可以证明这个看似恐怖的迹中，所有包含动量 $\not k$ 的项最终都为零，只有完全由质量项贡献的 $m^4 \operatorname{Tr}[\not\epsilon_1\not\epsilon_2\not\epsilon_3\not\epsilon_4]$ 存活下来，极大地简化了计算。这揭示了运动学约束在简化迹计算中的巨大威力。

#### [色因子](@entry_id:159844)

在处理强相互作用（QCD）过程时，除了自旋平均/求和，我们还必须处理色的自由度。夸克和胶子带有[色荷](@entry_id:151924)。对于一个 $SU(N_c)$ 的规范理论（QCD中 $N_c=3$），我们需要对初态色进行平均，对末态色进行求和。
例如，在[Drell-Yan过程](@entry_id:154547) $q\bar{q} \to \ell^+\ell^-$ [@problem_id:361280]，由于[光子](@entry_id:145192)不带色荷，夸克和反夸克必须处于[色单态](@entry_id:159293)才能湮灭。振幅的色结构部分为 $\delta_{ab}$，其中 $a,b$ 是夸克和反夸克的色指标。对色进行求和与平均引入一个**[色因子](@entry_id:159844) (color factor)**：
$$
\text{Color Factor} = \frac{1}{N_c^2} \sum_{a,b=1}^{N_c} |\delta_{ab}|^2 = \frac{1}{N_c^2} \sum_{a,b=1}^{N_c} \delta_{ab} \delta_{ba} = \frac{1}{N_c^2} \sum_{a=1}^{N_c} \delta_{aa} = \frac{N_c}{N_c^2} = \frac{1}{N_c}
$$
这个因子会乘在自旋平均的振幅平方上，共同构成完整的非极化[截面](@entry_id:154995)计算。

#### 手征性、螺旋度与投影算符

[弱相互作用](@entry_id:157579)是手征性的，它只与左手[费米子](@entry_id:146235)和右手反[费米子](@entry_id:146235)耦合。这通过**手征投影算符** $P_L = \frac{1}{2}(1-\gamma_5)$ 和 $P_R = \frac{1}{2}(1+\gamma_5)$ 来实现。这些算符是真正的[投影算符](@entry_id:154142)，满足 $P_L^2=P_L, P_R^2=P_R, P_L P_R = 0, P_L+P_R=1$。在迹计算中，它们可以被自由地插入和移动，极大地简化了涉及[弱相互作用](@entry_id:157579)的计算。

当我们不仅想对[自旋求和](@entry_id:162099)，而是想计算产生特定**螺旋度 (helicity)**（自旋在动量方向的投影）的[费米子](@entry_id:146235)的几率时，我们需要使用**[自旋投影算符](@entry_id:158519)**。对于一个动量为 $p$、质量为 $m$ 的[费米子](@entry_id:146235)，其自旋四矢量为 $s$，满足 $s \cdot p = 0$ 和 $s^2=-1$。产生该[自旋态](@entry_id:149436)的投影算符为：
$$
\Pi(s) = \frac{1+\gamma_5 \not s}{2}
$$
在计算中，我们不再使用 $\not p + m$ 进行求和，而是在其旁边插入 $\Pi(s)$ 来“挑选”出特定的[自旋态](@entry_id:149436)。例如，在t道单顶夸克产生过程 $ub \to dt$ 中 [@problem_id:200417]，若要计算产生一个具有特定自旋 $s_t$ 的顶夸克的[截面](@entry_id:154995)，其振幅平方的计算将包含对顶夸克[自旋求和](@entry_id:162099)算符 $(\not p_t + m_t)$ 与其[自旋投影算符](@entry_id:158519) $\Pi(s_t)$ 的乘积。

#### [马约拉纳费米子](@entry_id:137199)的计算

迹技术也可以推广到马约拉纳费米子。马约拉纳费米子是自身的反粒子，其场满足 $\psi^C = C\bar{\psi}^T = \psi$。这导致了新的[费曼规则](@entry_id:156797)和迹计算方法。一个连接两个[产生算符](@entry_id:191512)（例如 $e^-(k_1)$ 和 $e^-(k_2)$）的马约拉纳费米子线，其振幅结构为 $\mathcal{M} \propto \bar{u}(k_1) \Gamma u^C(k_2)$。对于无质量的末态[费米子](@entry_id:146235)，其[自旋求和](@entry_id:162099)的模方由一个新的迹规则给出：
$$
\sum_{s_1, s_2} |\bar{u}(k_1) \Gamma u^C(k_2)|^2 = \operatorname{Tr}[\not k_1 \Gamma \not k_2 \bar{\Gamma}]
$$
这个规则是计算任何涉及[马约拉纳中微子](@entry_id:160033)的过程（如[无中微子双贝塔衰变](@entry_id:151392)或问题 [@problem_id:200374] 中描述的轻子数破坏过程 $\phi^-\phi^- \to e^-e^-$）的基础。

#### 对称性与迹的消失

有时，迹的计算结果为零，这往往反映了某种深刻的物理对称性。考虑[康普顿散射](@entry_id:150648)中，假如电子除了[电荷](@entry_id:275494)外还有一个[电偶极矩](@entry_id:178520)（EDM）[@problem_id:200399]。E[DM相互作用](@entry_id:141331)顶点 $\Gamma_{EDM} \propto \sigma^{\mu\nu}\gamma_5$ 是破坏宇称（P）和时间反演（T）对称性的。
在计算标准QED振幅与EDM振幅的干涉项时，$\Delta \overline{|\mathcal{M}|^2} = 2\operatorname{Re}(\overline{\mathcal{M}_{QED}^* \mathcal{M}_{EDM}})$，我们会遇到一个包含单个 $\gamma_5$ 的迹。这个迹通常非零，会产生一个与[Levi-Civita张量](@entry_id:191101) $\epsilon^{\alpha\beta\gamma\delta}$ 成正比的项。然而，在对[光子](@entry_id:145192)极化求和后，这个反对称的[Levi-Civita张量](@entry_id:191101)需要与一个由[度规张量](@entry_id:160222)和动量构成的对称张量进行缩并，其结果必然为零。
这个数学上的零结果，其物理根源在于对称性：一个非极化的[总截面](@entry_id:151809)是一个P标量和T标量，它不能接收来自P-奇、T-奇的干涉项的贡献。迹技术以一种自动化的方式保证了这些对称性约束。

#### Fierz 恒等式

最后，Fierz恒等式是一类强大的重排工具，用于改变[四费米子相互作用](@entry_id:184227)中[旋量](@entry_id:158054)场的顺序。例如，它可以将 $(\bar{\psi}_1 \Gamma_A \psi_2)(\bar{\psi}_3 \Gamma_B \psi_4)$ 形式的算符，重写为 $(\bar{\psi}_1 \Gamma_C \psi_4)(\bar{\psi}_3 \Gamma_D \psi_2)$ 形式的算符的线性组合。这在比较或转化不同的有效场论时非常有用。例如，在问题 [@problem_id:200416] 中，通过Fierz恒等式可以证明，一个特定的标量-标量型[四费米子相互作用](@entry_id:184227) $(\bar{u}_4 u_1)(\bar{u}_3 u_2)$，经过重排后，无法产生一个 (V-A) $\times$ (V-A) 型的结构 $(\bar{u}_3 \gamma^\mu P_L u_1)(\bar{u}_4 \gamma_\mu P_L u_2)$。这直接导致它们之间的干涉项在[自旋求和](@entry_id:162099)后为零，揭示了不同洛伦兹结构之间的正交性。

综上所述，[自旋求和](@entry_id:162099)与迹技术是粒子物理学理论计算的基石。它将复杂的旋量代数转化为一套优雅的、协变的矩阵运算规则，不仅极大地提高了计算效率，而且其结构本身也深刻地反映了[量子场论](@entry_id:138177)的对称性与运动学约束。