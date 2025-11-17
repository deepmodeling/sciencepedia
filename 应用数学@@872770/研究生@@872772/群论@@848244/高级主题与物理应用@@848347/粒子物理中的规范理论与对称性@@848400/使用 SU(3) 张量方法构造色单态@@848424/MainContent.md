## 引言
在强相互作用的理论——量子色动力学（QCD）中，一个最基本的原则是[色禁闭](@entry_id:143757)，即自然界中只能观测到色荷为零的“[色单态](@entry_id:159293)”粒子，也就是我们熟知的[强子](@entry_id:158325)。这一原则意味着，所有由夸克和胶子这些带色荷的基本粒子构成的束缚态，其总[色荷](@entry_id:151924)必须精确抵消。那么，我们如何从数学上精确地描述这些色中性的[复合粒子](@entry_id:150176)呢？如何从带色的组分（夸克、反夸克、胶子）出发，系统地构建出它们的[色单态](@entry_id:159293)[波函数](@entry_id:147440)，并进一步理解维系它们稳定的内部动力学？

解答这些问题的关键，在于熟练运用SU($N_c$)[规范群](@entry_id:144761)的张量方法。这套强大的数学工具不仅能让我们构造出所有可能的[色单态](@entry_id:159293)结构，还能精确计算出[强子](@entry_id:158325)内部不同组分间的相互作用强度，从而揭示强子世界的丰富性和复杂性。本文将引导读者系统地掌握这一核心技术。在“原理与机制”一章中，我们将奠定理论基础，学习如何利用[不变张量](@entry_id:203823)和卡西米尔算符来构建和分析[色单态](@entry_id:159293)。接着，在“应用与跨学科联系”一章中，我们将看到这些原理如何被应用于粒子散射、[奇特强子](@entry_id:185108)谱学等前沿领域，展现其强大的物理预测能力。最后，“动手实践”部分将通过具体的计算问题，帮助读者将理论知识转化为解决实际问题的技能。

## 原理与机制

在量子色动力学 (QCD) 的框架中，一个核心的禁闭原则是，自然界中只存在[色单态](@entry_id:159293)的[强子](@entry_id:158325)。这意味着任何可观测的粒子，无论是介子还是重子，其总色荷必须为零。从群论的角度来看，这意味着构成[强子](@entry_id:158325)的夸克和胶子的色[波函数](@entry_id:147440)必须在 SU($N_c$) 色规范群的变换下保持不变。本章将系统地阐述如何利用张量方法来构建这些[色单态](@entry_id:159293)，并介绍计算其内部动力学性质的关键原理和机制。

### [色单态](@entry_id:159293)与 SU($N_c$) [不变张量](@entry_id:203823)

在 SU($N_c$) 群中，夸克 ($q$) 处于[基本表示](@entry_id:157678) $N_c$ 中，其色态可以被描述为一个 $N_c$ 维的矢量 $q_i$，其中 $i=1, \dots, N_c$。反夸克 ($\bar{q}$) 处于共轭[基本表示](@entry_id:157678) $\bar{N}_c$ 中，其色态被描述为一个上指标的协矢量（或对偶矢量）$\bar{q}^j$，其中 $j=1, \dots, N_c$。一个由多个夸克和反夸克组成的复合系统的色态，是一个[张量积](@entry_id:140694)空间中的矢量。要构建一个[色单态](@entry_id:159293)，我们必须将这些粒子的色指标通过 SU($N_c$) 的[不变张量](@entry_id:203823)进行缩并，最终得到一个没有[自由指标](@entry_id:189430)的标量。SU($N_c$) 群最基本的[不变张量](@entry_id:203823)是克罗内克符号 $\delta_j^i$ 和[列维-奇维塔符号](@entry_id:193594) $\epsilon_{i_1 \dots i_{N_c}}$ 及 $\epsilon^{j_1 \dots j_{N_c}}$。

#### [介子](@entry_id:184535)与克罗内克符号

最简单的[强子](@entry_id:158325)是介子，由一个夸克和一个反夸克构成 ($q\bar{q}$)。夸克的色指标是下指标 $i$，反夸克的色指标是上指标 $j$。我们可以使用克罗内克符号 $\delta_j^i$ 将这两个[指标缩并](@entry_id:180403)，从而构造一个[色单态](@entry_id:159293)。其[波函数](@entry_id:147440)形式如下：
$$
|\Psi_{\text{meson}}\rangle = \mathcal{N} \sum_{i=1}^{N_c} |q_i \bar{q}^i\rangle
$$
这里的 $|q_i \bar{q}^j\rangle$ 代表夸克色态为 $i$、反夸克色态为 $j$ 的[基矢](@entry_id:199546)。为了使态矢量归一化，即 $\langle\Psi_{\text{meson}}|\Psi_{\text{meson}}\rangle = 1$，我们需要确定[归一化常数](@entry_id:752675) $\mathcal{N}$。假设色[基矢](@entry_id:199546)是正交的，$\langle q_{i'} \bar{q}^{j'} | q_i \bar{q}^j \rangle = \delta_{i'i} \delta^{j'j}$，我们计算其模方：
$$
\langle\Psi_{\text{meson}}|\Psi_{\text{meson}}\rangle = |\mathcal{N}|^2 \sum_{i,k=1}^{N_c} \langle q_k \bar{q}^k | q_i \bar{q}^i \rangle = |\mathcal{N}|^2 \sum_{i,k=1}^{N_c} \delta_{ki}\delta^{ki} = |\mathcal{N}|^2 \sum_{i=1}^{N_c} \delta_{ii} = |\mathcal{N}|^2 N_c
$$
因此，选择正实数 $\mathcal{N}$，我们得到 $\mathcal{N} = \frac{1}{\sqrt{N_c}}$。这个结果表明，一个夸克和一个反夸克有 $N_c$ 种方式配对成[色单态](@entry_id:159293)，每种方式的[概率幅](@entry_id:150609)相等。

#### 重子与[列维-奇维塔符号](@entry_id:193594)

对于由三个夸克组成的重子（在 $N_c=3$ 的 QCD 中），情况则有所不同。为了将三个下指标 $i,j,k$ 缩并成一个标量，我们需要使用三阶全反对称的[列维-奇维塔符号](@entry_id:193594) $\epsilon_{ijk}$。根据[泡利不相容原理](@entry_id:141850)，对于[基态](@entry_id:150928)重子（如质子和中子），其自旋-[味觉](@entry_id:164776)和空间[波函数](@entry_id:147440)是全对称的，因此色[波函数](@entry_id:147440)必须是全反对称的，这恰好与使用 $\epsilon_{ijk}$ 构建的[色单态](@entry_id:159293)的性质相符。其未归一化的色[波函数](@entry_id:147440)为：
$$
|\Psi_C\rangle = \sum_{i,j,k=1}^3 \epsilon_{ijk} |q_i q_j q_k\rangle
$$
为了对此态进行归一化，我们计算其模方 [@problem_id:651881]：
$$
\langle\Psi_C|\Psi_C\rangle = \sum_{i,j,k} \sum_{i',j',k'} \epsilon_{ijk}^* \epsilon_{i'j'k'} \langle q_{i'} q_{j'} q_{k'} | q_i q_j q_k \rangle = \sum_{i,j,k} \epsilon_{ijk} \epsilon_{ijk}
$$
$\epsilon_{ijk}$ 的非零取值为 $\pm 1$。当 $i,j,k$ 是 $(1,2,3)$ 的偶[排列](@entry_id:136432)时为 $+1$，奇[排列](@entry_id:136432)时为 $-1$。总共有 $3! = 6$ 个非零项，每一项的平方都为 $1$。因此，$\sum_{i,j,k} \epsilon_{ijk}^2 = 3! = 6$。[归一化条件](@entry_id:156486) $1 = |\mathcal{N}|^2 \langle\Psi_C|\Psi_C\rangle$ 给出 $\mathcal{N} = \frac{1}{\sqrt{6}}$。

对于一般的 SU($N_c$)，重子由 $N_c$ 个夸克组成，其[色单态](@entry_id:159293)[波函数](@entry_id:147440)由 $N_c$ 阶[列维-奇维塔符号](@entry_id:193594) $\epsilon_{i_1 \dots i_{N_c}}$ 构造。

### 复合系统的[色单态](@entry_id:159293)[基矢](@entry_id:199546)

当系统包含更多粒子时，例如四夸克态 ($qq\bar{q}\bar{q}$) 或由 $M$ 个夸克和 $M$ 个反夸克组成的系统，构造[色单态](@entry_id:159293)的方式不再唯一，这引出了关于色结构[基矢](@entry_id:199546)的独立性和正交性的重要问题。

考虑一个由两个夸克 $q_1, q_2$ 和两个反夸克 $\bar{q}_1, \bar{q}_2$ 组成的系统。我们可以通过两种不同的方式将它们的色[指标缩并](@entry_id:180403)成单态 [@problem_id:651836]：
1.  将 $q_1$ 与 $\bar{q}_1$ 配对，将 $q_2$ 与 $\bar{q}_2$ 配对。这对应于张量结构 $\delta_{i_1}^{k_1} \delta_{i_2}^{k_2}$，其[波函数](@entry_id:147440)为 $|\Psi_A\rangle = \frac{1}{N_c} \sum_{i,j} |q_{1,i} q_{2,j} \bar{q}_1^i \bar{q}_2^j\rangle$。这可以看作是两个介子 $(q_1\bar{q}_1)$ 和 $(q_2\bar{q}_2)$ 组成的“分子”态。
2.  将 $q_1$ 与 $\bar{q}_2$ 配对，将 $q_2$ 与 $\bar{q}_1$ 配对。这对应于张量结构 $\delta_{i_1}^{k_2} \delta_{i_2}^{k_1}$，其[波函数](@entry_id:147440)为 $|\Psi_B\rangle = \frac{1}{N_c} \sum_{i,j} |q_{1,i} q_{2,j} \bar{q}_1^j \bar{q}_2^i\rangle$。

这两个归一化后的态矢量是否正交？我们可以通过计算它们的[内积](@entry_id:158127)来回答这个问题：
$$
\langle\Psi_A|\Psi_B\rangle = \frac{1}{N_c^2} \sum_{i,j,k,l} \langle q_{1,k} q_{2,l} \bar{q}_1^k \bar{q}_2^l | q_{1,i} q_{2,j} \bar{q}_1^j \bar{q}_2^i \rangle = \frac{1}{N_c^2} \sum_{i,j,k,l} \delta_{ki} \delta_{lj} \delta^{kj} \delta^{li}
$$
对指标进行缩并，我们得到：
$$
\langle\Psi_A|\Psi_B\rangle = \frac{1}{N_c^2} \sum_{i,j} \delta_{ji} \delta^{ji} = \frac{1}{N_c^2} \sum_{i} \delta_{ii} = \frac{N_c}{N_c^2} = \frac{1}{N_c}
$$
这个结果表明，这两种不同的[色单态](@entry_id:159293)结构并非正交，它们的交叠程度为 $1/N_c$。这意味着它们不是完全独立的[基矢](@entry_id:199546)。在 $N_c \to \infty$ 的大 $N_c$ 极限下，这两种结构才趋于正交。

更一般地，对于一个由 $M$ 个夸克和 $M$ 个反夸克组成的系统，[色单态](@entry_id:159293)是通过将 $M$ 个上指标与 $M$ 个下指标完全配对缩并而形成的。如果 $M \le N_c$，所有可能的配对方式（即[置换](@entry_id:136432)）都会产生[线性独立](@entry_id:153759)的[色单态](@entry_id:159293)。例如，对于一个由 $N_c$ 个夸克和 $N_c$ 个反夸克组成的系统，总共有 $N_c!$ 种不同的方式将夸克与反夸克配对，从而形成 $N_c!$ 个[线性独立](@entry_id:153759)的[色单态](@entry_id:159293) [@problem_id:651854]。这一结论源于[舒尔-韦尔对偶](@entry_id:146686)性 (Schur-Weyl duality)，它将 SU($N_c$) 的表示论与对称群 $S_M$ 的[表示论](@entry_id:137998)联系起来。

### 色动力学与卡西米尔算符

为了深入理解强子内部的动力学，我们需要从静态的态构建转向相互作用的描述。SU($N_c$) 的动力学由其[李代数](@entry_id:137954)的生成元 $T^a$ 决定，其中 $a=1, \dots, N_c^2-1$。这些生成元是无迹厄米矩阵。

一个核心的工具是二次卡西米尔算符 (quadratic Casimir operator)，定义为 $C_2 = \sum_a T^a T^a$。根据[舒尔引理](@entry_id:136779) (Schur's Lemma)，由于 $C_2$ 与代数的所有生成元都对易，它在任意一个不可约表示 (irrep) $R$ 中必然是单位算符 $\mathbb{1}$ 的一个倍数。这个倍数，记为 $C_2(R)$，是该表示的一个[不变量](@entry_id:148850)，可以看作是该表示的“总色荷平方”的量度。

#### [基本表示](@entry_id:157678)与伴随表示的[卡西米尔不变量](@entry_id:181340)

对于夸克所在的[基本表示](@entry_id:157678)，其[卡西米尔不变量](@entry_id:181340)记为 $C_F$。我们可以通过一个简单的迹技巧来计算它 [@problem_id:651751]。我们有关系式 $\sum_a T^a T^a = C_F \mathbb{1}_{N_c \times N_c}$。同时，生成元通常按照 $\text{Tr}(T^a T^b) = T_F \delta^{ab}$ 的约定进行归一化，其中对于[基本表示](@entry_id:157678)，习惯上取 $T_F = 1/2$。对卡西米尔算符的关系式两边取迹，可得：
$$
\text{Tr}\left(\sum_a T^a T^a\right) = \text{Tr}(C_F \mathbb{1}) = C_F N_c
$$
另一方面，利用[迹的线性](@entry_id:199170)和[归一化条件](@entry_id:156486)：
$$
\sum_a \text{Tr}(T^a T^a) = \sum_a T_F \delta^{aa} = T_F \sum_{a=1}^{N_c^2-1} 1 = T_F(N_c^2-1)
$$
联立两式，并代入 $T_F=1/2$，我们得到 $C_F N_c = \frac{1}{2}(N_c^2-1)$，从而解出：
$$
C_F = \frac{N_c^2-1}{2N_c}
$$
对于 $N_c=3$，我们得到 $C_F = \frac{3^2-1}{2 \cdot 3} = \frac{8}{6} = \frac{4}{3}$。

另一个重要的表示是伴随表示，胶子就处于此表示中。其[卡西米尔不变量](@entry_id:181340) $C_A$ 与代数的[结构常数](@entry_id:157960) $f^{abc}$ 密切相关。[结构常数](@entry_id:157960)由生成元的对易关系定义：$[T^a, T^b] = i f^{abc} T^c$。$C_A$ 由以下关系式定义：
$$
\sum_{c,d} f^{acd}f^{bcd} = C_A \delta^{ab}
$$
通过一系列代数推导，可以证明一个非常简洁和深刻的结果 [@problem_id:651749]：
$$
C_A = N_c
$$
对于 $N_c=3$， $C_A=3$。这个量在计算胶子相互作用的[圈图](@entry_id:149287)中起着至关重要的作用。

### 色荷关联与内部相互作用

卡西米尔算符的威力在于它能够用来计算[复合粒子](@entry_id:150176)内部不同组分之间的色荷关联，由算符 $\vec{T}_i \cdot \vec{T}_j \equiv \sum_a T_i^a T_j^a$ 来描述。对于一个由两个粒子组成的系统，总的卡西米尔算符为：
$$
C_2(\text{total}) = (\vec{T}_1 + \vec{T}_2)^2 = \vec{T}_1^2 + \vec{T}_2^2 + 2\vec{T}_1 \cdot \vec{T}_2
$$
其[期望值](@entry_id:153208)等于 $C_2(1) + C_2(2) + 2\langle\vec{T}_1 \cdot \vec{T}_2\rangle$。如果我们知道系统所处的总的[不可约表示](@entry_id:263310)（因此知道 $C_2(\text{total})$），以及其组分的表示（知道 $C_2(1)$ 和 $C_2(2)$），我们就能直接计算出组分间的色荷关联。

#### 示例：介子与双夸克

- **[介子](@entry_id:184535)**：一个介子是 $q\bar{q}$ 对构成的[色单态](@entry_id:159293)。单态的定义是总色荷为零，即 $\vec{T}_{\text{total}} = \vec{T}_q + \vec{T}_{\bar{q}} = 0$。因此，总卡西米尔算符的[期望值](@entry_id:153208)为零。夸克和反夸克都处于[基本表示](@entry_id:157678)（或其共轭），所以它们的[卡西米尔不变量](@entry_id:181340)都是 $C_F$。于是：
  $$
  0 = C_F + C_F + 2\langle\vec{T}_q \cdot \vec{T}_{\bar{q}}\rangle \quad \implies \quad \langle\vec{T}_q \cdot \vec{T}_{\bar{q}}\rangle = -C_F = -\frac{N_c^2-1}{2N_c}
  $$
  这个负值表示夸克和反夸克之间存在强烈的吸引作用，这是它们能稳定束缚成[介子](@entry_id:184535)的动力学基础。

- **双夸克系统**：考虑一个由两个夸克组成的假设性系统（双夸克）。其色空间是 $N_c \otimes N_c$ 的张量积，可以分解为对称表示和反对称表示。对于 SU(3)，即 $3 \otimes 3 = 6_S \oplus \bar{3}_A$。我们可以计算这两个表示中的夸克-夸克[色荷](@entry_id:151924)关联 [@problem_id:651774]。我们可以直接应用卡西米尔算符的方法。
  - 对于反对称的 $\bar{3}_A$ 态，总表示为 $\bar{3}$，其[卡西米尔不变量](@entry_id:181340)为 $C_2(\bar{3}) = C_F$。因此 $C_2(\text{total}) = C_F$。我们有： $C_F = C_F + C_F + 2\langle\vec{T}_1 \cdot \vec{T}_2\rangle_A$，解得 $\langle\vec{T}_1 \cdot \vec{T}_2\rangle_A = -C_F/2$。对于 $N_c=3$，该值为 $-2/3$。
  - 对于对称的 $6_S$ 态, 总表示为 $6$，其[卡西米尔不变量](@entry_id:181340)为 $C_2(6) = \frac{(N_c+1)(N_c-2)}{N_c}$（对于SU(N)）。对于 $N_c=3$，$C_2(6) = \frac{4 \cdot 1}{3} = 4/3$ 是错误的，应该是 $C_2(6)=\frac{10}{3}$。利用 $C_2(6) = C_F + C_F + 2\langle\vec{T}_1 \cdot \vec{T}_2\rangle_S$，我们得到 $\frac{10}{3} = \frac{4}{3} + \frac{4}{3} + 2\langle\vec{T}_1 \cdot \vec{T}_2\rangle_S$，解得 $\langle\vec{T}_1 \cdot \vec{T}_2\rangle_S = \frac{1}{3}$。
  负的[色荷](@entry_id:151924)关联值代表吸引，正值代表排斥。因此，反对称色态中的夸克相互吸引，而对称色态中的夸克相互排斥，这解释了为何在重子中，反对称的色态组合是[基态](@entry_id:150928)结构。

#### 示例：复杂多夸克态

卡西米尔方法可以推广到更复杂的系统。例如，考虑一个由三个夸克构成的、处于伴随表示 $\mathbf{8}$ 的[激发态](@entry_id:261453)，其内部结构是先将夸克 $q_1, q_2$ 组合成一个对称的双夸克 $\mathbf{6}$ 态，然后再与第三个夸克 $q_3$ 耦合形成 $\mathbf{8}$ 态。我们可以计算这个态中任意两夸克之间的[色荷](@entry_id:151924)关联 [@problem_id:651811]。
1.  首先，在 $(q_1q_2)$ 构成的 $\mathbf{6}$ 子系统中，我们已知 $\langle\vec{T}_1 \cdot \vec{T}_2\rangle = 1/3$。
2.  然后，考虑整个三夸克系统，其总[卡西米尔不变量](@entry_id:181340)为 $C_2(\mathbf{8}) = C_A = 3$。
    $$
    C_2(\mathbf{8}) = (\vec{T}_1+\vec{T}_2+\vec{T}_3)^2 = 3C_F + 2(\langle\vec{T}_1 \cdot \vec{T}_2\rangle + \langle\vec{T}_1 \cdot \vec{T}_3\rangle + \langle\vec{T}_2 \cdot \vec{T}_3\rangle)
    $$
3.  代入已知数值：$3 = 3(4/3) + 2(1/3 + \langle\vec{T}_1 \cdot \vec{T}_3\rangle + \langle\vec{T}_2 \cdot \vec{T}_3\rangle)$。由于 $q_1, q_2$ 在子系统中是对称的，它们与 $q_3$ 的关联也必然相等，即 $\langle\vec{T}_1 \cdot \vec{T}_3\rangle = \langle\vec{T}_2 \cdot \vec{T}_3\rangle$。
4.  求解得到 $3 = 4 + 2/3 + 4\langle\vec{T}_2 \cdot \vec{T}_3\rangle$，即 $4\langle\vec{T}_2 \cdot \vec{T}_3\rangle = -1 - 2/3 = -5/3$。因此 $\langle\vec{T}_2 \cdot \vec{T}_3\rangle = -5/12$。这说明即使在同一个强子内部，不同夸克对之间的色相互作用强度也可能因为内部色结构的差异而大相径庭。

### 高级工具：菲尔兹恒等式与[投影算符](@entry_id:154142)

[色因子](@entry_id:159844)计算的核心工具是所谓的菲尔兹恒等式，它允许我们将生成元的乘积用更简单的张量结构表示。

#### 基本菲尔兹恒等式

对于 SU($N_c$) 的[基本表示](@entry_id:157678)，最常用的菲尔兹恒等式是：
$$
\sum_{a=1}^{N_c^2-1} (T^a)_{ij} (T^a)_{kl} = \frac{1}{2} \left( \delta_{il}\delta_{jk} - \frac{1}{N_c} \delta_{ij}\delta_{kl} \right)
$$
这个恒等式（已使用 $T_F=1/2$ 的约定）是 QCD 计算的基石。例如，在夸克-反夸克散射过程中，单胶子交换的[色因子](@entry_id:159844)张量就可以通过此恒等式来分析 [@problem_id:651753]。它也是推导许多其他关系，如 $C_A=N_c$ [@problem_id:651749] 和色荷关联算符性质 [@problem_id:651769] 的基础。例如，在由两个色八重态 $(q_1\bar{q}_3)$ 和 $(q_2\bar{q}_4)$ 构成的四夸克[色单态](@entry_id:159293)中，可以利用此恒等式计算出夸克-夸克之间的色荷关联为 $\langle \vec{T}_1 \cdot \vec{T}_2 \rangle = -1/N_c$ [@problem_id:651769]。此外，还有涉及对称[结构常数](@entry_id:157960) $d_{abc}$ 的恒等式，如 $\sum_{c,d} d^{acd}d^{bcd} = \frac{N_c^2-4}{N_c} \delta^{ab}$，由此可以计算出[标量不变量](@entry_id:193787) $\sum_{a,b,c} d_{abc}^2 = \frac{(N_c^2-1)(N_c^2-4)}{N_c}$。对于 SU(3)，这个值为 $40/3$ [@problem_id:651855]。

#### 投影算符

菲尔兹恒等式的一个强大应用是构建[投影算符](@entry_id:154142)，它可以将一个给定的色态投影到特定的不可约表示[子空间](@entry_id:150286)上。以 $q\bar{q}$ 系统为例，其色空间可以分解为单态和伴随[表示的直和](@entry_id:138310)：$N_c \otimes \bar{N}_c = 1 \oplus (N_c^2 - 1)$。我们可以构建一个算符 $P_1$ 来将任意 $q\bar{q}$ 态投影到单态[子空间](@entry_id:150286)。这个算符必须是 SU($N_c$) 不变的，因此它可以写成单位算符 $I$ 和[色荷](@entry_id:151924)关联算符 $K = \sum_a T_q^a \otimes T_{\bar{q}}^a$ 的线性组合 [@problem_id:651889]：
$$
P_1 = \alpha I + \beta K
$$
为了确定系数 $\alpha$ 和 $\beta$，我们可以利用 $P_1$ 作用于单态和伴随态上的性质：$P_1 |s\rangle = |s\rangle$ 和 $P_1 |a\rangle = 0$。同时，我们需要知道算符 $K$ 在这两个[子空间](@entry_id:150286)上的[本征值](@entry_id:154894)。这可以通过总卡西米尔算符 $C_{tot} = 2C_F I + 2K$ 来获得。我们知道 $C_{tot}$ 在单态上的[本征值](@entry_id:154894)为 0，在伴随态上的[本征值](@entry_id:154894)为 $C_A=N_c$。由此可解出 $K$ 在单态上的[本征值](@entry_id:154894) $k_s = -C_F$，在伴随态上的[本征值](@entry_id:154894) $k_a = (C_A-2C_F)/2 = 1/(2N_c)$。
将这些[本征值](@entry_id:154894)代入投影条件[方程组](@entry_id:193238)：
$$
\begin{cases} \alpha + \beta k_s = 1 \\ \alpha + \beta k_a = 0 \end{cases}
$$
解得 $\beta(k_s - k_a) = 1$。代入 $k_s$ 和 $k_a$ 的表达式，经过计算可得一个非常简洁的结果：
$$
\beta = -\frac{2}{N_c}
$$
从而得到 $\alpha = -\beta k_a = 1/N_c^2$。最终，单态[投影算符](@entry_id:154142)为：
$$
P_1 = \frac{1}{N_c^2} I - \frac{2}{N_c} \sum_a T_q^a \otimes T_{\bar{q}}^a
$$
这个算符为从复杂的色[态混合](@entry_id:148060)物中分离出物理上可观测的[色单态](@entry_id:159293)提供了一个具体而强大的数学工具。

本章所介绍的原理和方法构成了理解和计算[强子结构](@entry_id:160640)与性质的理论基础。通过熟练运用 SU($N_c$) 的张量方法、[卡西米尔不变量](@entry_id:181340)和菲尔兹恒等式，我们可以对强子内部复杂的色动力学进行定量分析。