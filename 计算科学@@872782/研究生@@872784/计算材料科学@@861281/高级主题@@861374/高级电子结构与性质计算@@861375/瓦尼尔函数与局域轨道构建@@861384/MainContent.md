## 引言
[瓦尼尔函数](@entry_id:145994)作为晶体中[布洛赫态](@entry_id:147552)的实空间表示，为理解材料的电子结构提供了一个既有化学直觉又具备强大计算能力的框架。尽管[第一性原理计算](@entry_id:198754)能够精确地描述离域的[布洛赫波](@entry_id:144558)，但在将其转化为局域的、可移植的[化学键](@entry_id:138216)和低能物理模型方面，存在着一条明显的鸿沟。本文旨在跨越这一鸿沟，为构建和应用局域化[轨道](@entry_id:137151)，特别是最大局域化瓦尼尔函数（MLWFs），提供一份全面的理论与实践指南。

本文的结构旨在引导读者从基础理论走向实际应用。第一章**“原理与机制”**将深入探讨核心的数学形式。我们将探索如何利用布洛赫[子空间](@entry_id:150286)内的[规范自由度](@entry_id:160491)来系统性地最小化“展宽泛函”，从而获得尽可能局域化的[轨道](@entry_id:137151)。我们还将直面[拓扑阻碍](@entry_id:634492)和纠缠能带带来的挑战，并介绍陈数和退纠缠程序等关键概念。

在这一理论基础上，第二章**“应用与[交叉](@entry_id:147634)学科联系”**将展示[瓦尼尔函数](@entry_id:145994)的巨大通用性。您将学习它如何通过[瓦尼尔插值](@entry_id:140778)法实现[布里渊区](@entry_id:142395)性质的高效计算，如何为现代电极化理论提供基石，如何作为[拓扑材料](@entry_id:142123)的诊断工具，以及如何作为系统性的“下折叠”引擎，用于推导[强关联体系](@entry_id:145791)的哈勃模型等低能有效模型。

最后，为巩固您的理解，第三章**“动手实践”**提供了一系列引导性的计算练习。这些问题将让您有机会亲手实现关键算法，探索不同选择对最终结果的影响，并获得将这些强大技术应用于实际[材料科学](@entry_id:152226)问题的实践经验。通过学习这几章内容，您将掌握在自己的研究中运用[瓦尼尔函数](@entry_id:145994)的关键知识和技能，将复杂的[电子结构](@entry_id:145158)数据转化为深刻的物理洞见。

## 原理与机制

本章深入探讨了构建局域化[轨道](@entry_id:137151)（尤其是最大局域化[瓦尼尔函数](@entry_id:145994)）的核心原理与机制。在前一章介绍其基本概念和应用之后，我们现在将系统地阐述其理论框架，从布洛赫[子空间](@entry_id:150286)中的规范自由度出发，介绍展宽泛函的最小化过程，并讨论[拓扑阻碍](@entry_id:634492)和能带纠缠等复杂情况下的处理方法。

### 布洛赫[子空间](@entry_id:150286)中的规范自由度

周期性晶体中的电子态由布洛赫定理描述，其[波函数](@entry_id:147440)形式为 $\lvert \psi_{n\mathbf{k}} \rangle = \exp(i\mathbf{k}\cdot\mathbf{r}) \lvert u_{n\mathbf{k}} \rangle$，其中 $\lvert u_{n\mathbf{k}} \rangle$ 是具有[晶格](@entry_id:196752)周期性的[细胞周期](@entry_id:140664)部分。在许多应用中，我们关注的不是整个[能谱](@entry_id:181780)，而是一个由 $N$ 个能带构成的孤立或复合的[子空间](@entry_id:150286) $\mathcal{S}(\mathbf{k})$。在每个波矢 $\mathbf{k}$ 处，这个[子空间](@entry_id:150286)由一组[布洛赫态](@entry_id:147552) $\lbrace\lvert \psi_{n\mathbf{k}}\rangle\rbrace_{n=1}^N$ 张成。

然而，对于给定的[子空间](@entry_id:150286) $\mathcal{S}(\mathbf{k})$，其[基矢](@entry_id:199546)的选择并非唯一。我们可以通过一个依赖于 $\mathbf{k}$ 的 $N \times N$ 幺[正矩阵](@entry_id:149490) $U(\mathbf{k})$ 对[基矢](@entry_id:199546)进行任意的[酉变换](@entry_id:152599)（或称**[规范变换](@entry_id:176521)**），从而得到一组新的[布洛赫态](@entry_id:147552)：

$
\lvert \tilde{\psi}_{n\mathbf{k}} \rangle = \sum_{m=1}^{N} \lvert \psi_{m\mathbf{k}} \rangle U_{mn}(\mathbf{k})
$

这组新的[基矢](@entry_id:199546) $\lbrace\lvert \tilde{\psi}_{n\mathbf{k}}\rangle\rbrace_{n=1}^N$ 同样能够张成完全相同的[子空间](@entry_id:150286) $\mathcal{S}(\mathbf{k})$。这一点至关重要，因为它意味着该[子空间](@entry_id:150286)的[投影算符](@entry_id:154142) $P(\mathbf{k}) = \sum_{n=1}^{N} \lvert \psi_{n\mathbf{k}} \rangle \langle \psi_{n\mathbf{k}} \rvert$ 在此规范变换下是**[不变量](@entry_id:148850)**。由于能带能量、态密度等物理可观测量仅依赖于[投影算符](@entry_id:154142) $P(\mathbf{k})$，因此这种[规范变换](@entry_id:176521)不会改变这些基本性质 [@problem_id:3502354]。

[瓦尼尔函数](@entry_id:145994)（Wannier Functions, WFs）被定义为[布洛赫态](@entry_id:147552)的[傅里叶变换](@entry_id:142120)。具体而言，与某个[晶格矢量](@entry_id:161583) $\mathbf{R}$ 关联的[瓦尼尔函数](@entry_id:145994)由下式给出：

$
\lvert \mathbf{R}n \rangle = \frac{V}{(2\pi)^d} \int_{\text{BZ}} d^d\mathbf{k} \, \exp(-i\mathbf{k}\cdot\mathbf{R}) \lvert \tilde{\psi}_{n\mathbf{k}} \rangle
$

其中 $V$ 是[原胞](@entry_id:159354)体积，$d$ 是空间维度，积分在整个布里渊区（BZ）上进行。从这个定义可以看出，瓦尼尔函数的性质——特别是它们在实空间中的形状和局域性——直接依赖于所选的[布洛赫态](@entry_id:147552)[基矢](@entry_id:199546) $\lvert \tilde{\psi}_{n\mathbf{k}} \rangle$。因此，$\mathbf{k}$ 依赖的幺[正矩阵](@entry_id:149490) $U(\mathbf{k})$ 所代表的**规范自由度**，成为了调控瓦尼尔函数局域性的关键工具。一个平滑的、周期性的规范选择（即 $\lvert \tilde{\psi}_{n\mathbf{k}} \rangle$ 作为 $\mathbf{k}$ 的函数是平滑且周期的）是获得局域化瓦尼尔函数的前提。

### 最大局域化[瓦尼尔函数](@entry_id:145994)：展宽泛函

既然规范选择会影响局域性，一个自然的问题是：是否存在一个“最佳”规范，能够产生“最局域”的[瓦尼尔函数](@entry_id:145994)？Marzari和Vanderbilt的理论为此提供了肯定的回答和系统的构造方法。他们引入了一个总的二次**展宽泛函**（spread functional）$\Omega$，作为衡量一组[瓦尼尔函数](@entry_id:145994)局域性的量化指标：

$
\Omega = \sum_{n=1}^{N} \Omega_n = \sum_{n=1}^{N} \left( \langle \mathbf{0}n \rvert r^2 \lvert \mathbf{0}n \rangle - \langle \mathbf{0}n \rvert \mathbf{r} \lvert \mathbf{0}n \rangle^2 \right)
$

这里，$\Omega_n$ 是第 $n$ 个位于[原胞](@entry_id:159354)（$\mathbf{R}=\mathbf{0}$）的[瓦尼尔函数](@entry_id:145994)的[方差](@entry_id:200758)，或称二次展宽。**最大局域化瓦尼尔函数（Maximally Localized Wannier Functions, MLWFs）**就是通过选择规范 $U(\mathbf{k})$ 来最小化总展宽 $\Omega$ 而得到的一组瓦尼尔函数。

至关重要的是，总展宽 $\Omega$ 并非在所有规范下都相同 [@problem_id:3502354]。它可以被分解为两个部分：

$
\Omega = \Omega_I + \tilde{\Omega}
$

其中 $\Omega_I$ 是**规范不变**的部分，它只依赖于[子空间](@entry_id:150286) $P(\mathbf{k})$ 的几何性质，而 $\tilde{\Omega}$ 是**规范依赖**的部分。最小化 $\Omega$ 的任务等价于最小化 $\tilde{\Omega}$。规范依赖的展宽 $\tilde{\Omega}$ 可以进一步表示为非对角和对角两部分之和，$\tilde{\Omega} = \Omega_{\mathrm{OD}} + \Omega_{\mathrm{D}}$。在许多情况下，起主导作用的是非对角项：

$
\Omega_{\mathrm{OD}} = \sum_{n=1}^{N} \sum_{m \neq n} \int_{\text{BZ}} \frac{d^d\mathbf{k}}{(2\pi)^d} \lvert A_{mn}(\mathbf{k}) \rvert^2
$

这里的 $A_{mn}(\mathbf{k}) = i\langle u_{m\mathbf{k}} \rvert \nabla_{\mathbf{k}} u_{n\mathbf{k}} \rangle$ 是在所选规范下的**非阿贝尔[贝里联络](@entry_id:136662)**（non-Abelian Berry connection）的[矩阵元](@entry_id:186505)。这个表达式清晰地揭示了局域化的物理图像：为了使[瓦尼尔函数](@entry_id:145994)在[实空间](@entry_id:754128)中局域，我们需要选择一个规范，使得[布洛赫态](@entry_id:147552)的[细胞周期](@entry_id:140664)部分 $\lvert u_{n\mathbf{k}} \rangle$ 随 $\mathbf{k}$ 的变化尽可能“平滑”。这种平滑性体现在[贝里联络](@entry_id:136662)的非对角元尽可能小，这在几何上对应于在布里渊区的 $\mathbf{k}$ 点之间进行**平行输运** [@problem_id:3502354]。

考虑一个简单的一维双能带玩具模型来说明这一点 [@problem_id:3502307]。假设在一个初始规范下，[贝里联络](@entry_id:136662)矩阵为 $A(k) = \begin{pmatrix} \Delta \cos k  \Gamma \\ \Gamma  -\Delta \cos k \end{pmatrix}$。我们可以通过一个不依赖于 $k$ 的旋转矩阵 $U(\theta) = \begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix}$ 来混合这两个能带，从而改变规范。变换后的联络为 $A'(k) = U(\theta)^{\dagger}A(k)U(\theta)$。通过计算，可以得到总的规范依赖展宽为 $\tilde{\Omega}(\theta) = \Delta^2 + 2\Gamma^2\cos^2(2\theta)$。为了最小化展宽，我们需要最小化 $\cos^2(2\theta)$，即令其为零。这发生在 $2\theta = \pi/2$，或 $\theta = \pi/4$ 时。这个简单的例子生动地展示了通过[规范旋转](@entry_id:749732)将[贝里联络](@entry_id:136662)的“非对角”部分（在变换后的基底下）最小化，从而达到最佳局域化的过程。

### [瓦尼尔中心](@entry_id:145840)与[贝里相位](@entry_id:159450)

除了展宽（二阶矩），[瓦尼尔函数](@entry_id:145994)的一阶矩——它的中心位置 $\overline{\mathbf{r}}_n = \langle \mathbf{0}n \rvert \mathbf{r} \lvert \mathbf{0}n \rangle$——也具有深刻的物理意义。在一维情况下，对于一个孤立的能带，其[瓦尼尔中心](@entry_id:145840) $\bar{x}$ 直接与该能带的**贝里相位**（或称**[扎克相位](@entry_id:144645)**，Zak phase）$\phi$ 相关联：

$
\bar{x} = \frac{a}{2\pi} \phi \pmod a
$

这里的 $a$ 是晶格常数。贝里相位本身是[贝里联络](@entry_id:136662) $A(k) = i \langle u(k) \rvert \partial_{k} u(k) \rangle$ 沿整个布里渊区的[闭路积分](@entry_id:164828)：

$
\phi = \int_{\text{BZ}} A(k) dk
$

这个关系将一个[实空间](@entry_id:754128)属性（[瓦尼尔中心](@entry_id:145840)位置）与一个[倒空间](@entry_id:754151)中的纯几何（或拓扑）量（[贝里相位](@entry_id:159450)）联系起来，是现代电极化理论的基石。在数值计算中，贝里相位通常通过离散化的[布里渊区](@entry_id:142395)路径来计算。我们将[布里渊区](@entry_id:142395)划分为 $N$ 个小段，其端点为 $k_j$ ($j=0, \dots, N$)，其中 $k_N \equiv k_0 + G$，$G$ 是[倒格矢](@entry_id:263351)。贝里相位可以通过计算相邻 $\mathbf{k}$ 点上细胞周期[波函数](@entry_id:147440)之间的交叠矩阵的乘积来得到。对于单能带情况，交叠是标量 $M_j = \langle u(k_j) \rvert u(k_{j+1}) \rangle$，贝里相位则为：

$
\phi = \text{Im} \left[ \ln \left( \prod_{j=0}^{N-1} M_j \right) \right]
$

例如，考虑一个一维[晶格](@entry_id:196752)，晶格常数 $a=3.0$ Å，布里渊区被离散为6个点。如果我们从数值计算中得到了一系列交叠的相位，如 $M_0 = \exp(i\pi/12)$, $M_1 = \exp(i\pi/6)$, $M_2 = \exp(i\pi/4)$, $M_3 = \exp(i\pi/4)$, $M_4 = \exp(-i\pi/6)$, $M_5 = \exp(i\pi/12)$ [@problem_id:3502304]。将这些交叠的相位全部乘起来，总的相位因子为 $\exp(i( \pi/12 + \pi/6 + \pi/4 + \pi/4 - \pi/6 + \pi/12 )) = \exp(i 2\pi/3)$。因此，贝里相位 $\phi = 2\pi/3$。利用上述关系，我们可以立即得到[瓦尼尔中心](@entry_id:145840)的位置：$\bar{x} = (a/2\pi) \phi = (3.0 \text{ Å}/2\pi) \times (2\pi/3) = 1.0$ Å。这个计算清晰地展示了如何从倒空间的[波函数](@entry_id:147440)几何信息中提取出[实空间](@entry_id:754128)的[物理可观测量](@entry_id:154692)。

### 局域化的[拓扑阻碍](@entry_id:634492)

到目前为止，我们都假设可以找到一个平滑、周期的规范来构造局域化的瓦尼尔函数。然而，这并非总是可能的。能否为一组能带构造出指数局域化的瓦尼尔函数，是一个深刻的**拓扑问题**。

指数局域化的[瓦尼尔函数](@entry_id:145994)存在的充要条件是，相应的布洛赫[子空间](@entry_id:150286) $\mathcal{S}(\mathbf{k})$ 能够容纳一个在整个[布里渊区](@entry_id:142395)上都是**平滑且周期**的布洛赫[基矢](@entry_id:199546)框架 [@problem_id:3502354]。在数学上，这个布洛赫[子空间](@entry_id:150286)构成了一个向量丛。是否存在一个全局平滑的[基矢](@entry_id:199546)框架，取决于这个向量丛的拓扑性质。

对于二维系统中的一个孤立能带（或一组孤立能带），其[拓扑性质](@entry_id:141605)由一个整数[不变量](@entry_id:148850)——**陈数**（Chern number）$C$ 来表征。陈数是贝里曲率 $F_{xy}(\mathbf{k}) = \partial_{k_x} A_y - \partial_{k_y} A_x$ 在整个[布里渊区](@entry_id:142395)上的积分：

$
C = \frac{1}{2\pi} \int_{\text{BZ}} d^2k \, F_{xy}(\mathbf{k})
$

根据陈-[高斯-博内定理](@entry_id:160424)，这个积分必须是整数。如果一个能带（或能带[子空间](@entry_id:150286)）的陈数 $C \neq 0$，则它对应的向量丛是拓扑非平庸的。这意味着，我们**不可能**在整个布里渊区上找到一个同时满足平滑性和周期性的规范 [@problem_id:3502361]。任何试图构造这样一个规范的尝试，都必然会在布里渊区的某些地方引入[奇点](@entry_id:137764)或不连续的“接缝”（branch cut）[@problem_id:3502309]。由于指数局域化要求[布洛赫函数](@entry_id:189422)在 $\mathbf{k}$ 空间中是解析的（这比平滑更强），一个非零的陈数构成了构造指数局域化[瓦尼尔函数](@entry_id:145994)的根本性**[拓扑阻碍](@entry_id:634492)**。

在数值上，这种[拓扑阻碍](@entry_id:634492)表现为展宽泛函 $\Omega$ 在对 $\mathbf{k}$ 点网格进行加密时不会收敛到一个有限值，而是会发散 [@problem_id:3502309]。这是因为，为了满足非零陈数所蕴含的[全局相位](@entry_id:147947)缠绕，规范必然在某些地方发生剧烈变化，导致[贝里联络](@entry_id:136662)的非对角元很大，从而使展宽泛函发散。

这个看似棘手的问题有一个重要的解决方案：虽然单个或一组总陈数非零的能带无法瓦尼尔化，但如果我们考虑一个更大的、由多组能带构成的**复合[子空间](@entry_id:150286)**，只要这个复合[子空间](@entry_id:150286)的总陈数为零，那么原则上就可以为这个更大的[子空间](@entry_id:150286)构建一组指数局域化的瓦尼尔函数 [@problem_id:3502309]。这为处理拓扑非平庸的材料提供了出路。

此外，在受[时间反演对称性](@entry_id:138094)（TRS）保护的系统中，也存在类似的[拓扑阻碍](@entry_id:634492)。对于具有 $\Theta^2=-1$ 的[费米子](@entry_id:146235)系统（如电子），TRS保证了能带的克拉默简并，并使得总陈数为零。然而，在二维或三维中，可能存在非平庸的 $\mathbb{Z}_2$ [拓扑不变量](@entry_id:138526)。这种 $\mathbb{Z}_2$ 拓扑序也对构造*同时满足局域性和时间反演对称性*的瓦尼尔函数构成阻碍。诊断这种 $\mathbb{Z}_2$ [拓扑阻碍](@entry_id:634492)的有力工具是计算**威尔逊环**（Wilson loop）的本征相位谱。威尔逊环是沿布里渊区某个非收缩闭合路径的非阿贝尔[贝里相位](@entry_id:159450)的路径有序指数。在 $\mathbb{Z}_2$ [拓扑绝缘体](@entry_id:137834)中，这些本征相位在沿另一个方向演化时会表现出一种“交叉”或“配对交换”的奇特行为，其交叉次数的奇偶性直接对应于 $\mathbb{Z}_2$ [不变量](@entry_id:148850) [@problem_id:3502312]。

### 处理纠缠能带：退纠缠方法

在金属或具有复杂[能带结构](@entry_id:139379)的材料中，我们感兴趣的能带（例如，费米能级附近的[导带](@entry_id:159736)）往往与其他能带发生交叉和纠缠，形成一个无法用单一能量阈值清晰分离的复合体。在这种情况下，我们无法简单地选取一个维度固定的孤立能带[子空间](@entry_id:150286)。为了解决这个问题，需要采用一种称为**退纠缠**（disentanglement）的程序。

该程序的目标是从一个较大的、包含所有[相关能](@entry_id:144432)带的“外部”空间中，为每个 $\mathbf{k}$ 点选择一个维度固定为 $N$（$N$ 是我们想要构造的[瓦尼尔函数](@entry_id:145994)的数量）的最优[子空间](@entry_id:150286) $\mathcal{S}(\mathbf{k})$，并使得这个[子空间](@entry_id:150286)簇 $\lbrace \mathcal{S}(\mathbf{k}) \rbrace$ 作为 $\mathbf{k}$ 的函数尽可能平滑。

具体操作中，我们定义两个能量窗口 [@problem_id:3502339]：
1.  **冻结窗口**（frozen window）$[E_{f}^{\min}, E_{f}^{\max}]$：位于此能量范围内的能带被认为是物理上最重要的，必须被完整地包含在目标[子空间](@entry_id:150286) $S(\mathbf{k})$ 中。这些能带构成的[子空间](@entry_id:150286)记为 $F(\mathbf{k})$。
2.  **外部窗口**（outer window）$[E_{o}^{\min}, E_{o}^{\max}]$：它定义了一个更大的能量范围。所有位于此范围内的能带构成了“候选池”，即环境[子空间](@entry_id:150286) $O(\mathbf{k})$。目标[子空间](@entry_id:150286) $S(\mathbf{k})$ 必须完全由 $O(\mathbf{k})$ 中的态构成。

因此，在每个 $\mathbf{k}$ 点，我们寻找的 $N$ 维[子空间](@entry_id:150286) $S(\mathbf{k})$ 必须满足 $F(\mathbf{k}) \subseteq S(\mathbf{k}) \subseteq O(\mathbf{k})$。这立即导出一个**可行性条件**：对于所有 $\mathbf{k}$，必须满足 $\dim F(\mathbf{k}) \le N \le \dim O(\mathbf{k})$。如果在一个 $\mathbf{k}$ 点，冻结窗口中的能带数超过了 $N$，或者外部窗口中的能带总数少于 $N$，那么该参数选择就是不合理的 [@problem_id:3502339]。

当可行性条件满足时，退纠缠算法的目标就是在每个 $\mathbf{k}$ 点，从 $O(\mathbf{k}) \setminus F(\mathbf{k})$ 的态中，选择 $N - \dim F(\mathbf{k})$ 个态，与 $F(\mathbf{k})$ 中的态一起构成最优的 $N$ 维[子空间](@entry_id:150286) $S(\mathbf{k})$。选择的判据是最小化一个“溢出”（spillage）泛函，该泛函衡量了相邻 $\mathbf{k}$ 点的[子空间](@entry_id:150286)之间的不匹配程度，从而确保了[子空间](@entry_id:150286)簇 $\lbrace S(\mathbf{k}) \rbrace$ 的最大平滑性。

一个清晰的解析例子可以阐明这个过程 [@problem_id:3502360]。考虑一个一维双[能带交叉](@entry_id:161733)模型，其能量为 $\epsilon_{1}(k) = -\alpha k$ 和 $\epsilon_{2}(k) = \alpha k$，在 $k=0$ 处交叉。我们希望构造一个光滑的一维[子空间](@entry_id:150286)。我们设定一个冻结窗口，使得当 $k \ge k_f$ 时，[子空间](@entry_id:150286)必须是能量较低的 $\lvert 1 \rangle$ 态；当 $k \le -k_f$ 时，[子空间](@entry_id:150286)必须是 $\lvert 2 \rangle$ 态。在中间的纠缠区域 $-k_f  k  k_f$ 内，没有能带处于冻结窗口。退纠缠的目标就是找到一个平滑的函数 $\lvert u(k) \rangle$ 来连接 $\lvert u(-k_f) \rangle = \lvert 2 \rangle$ 和 $\lvert u(k_f) \rangle = \lvert 1 \rangle$。最平滑的连接方式是在由态 $\lvert 1 \rangle$ 和 $\lvert 2 \rangle$ 构成的[布洛赫球面](@entry_id:138823)上走一条[测地线](@entry_id:269969)（大圆路径）。这给出了解析的[投影算符](@entry_id:154142)，例如在纠缠区域内为 $P(k) = \frac{1}{2} \begin{pmatrix} 1 + \sin(\frac{\pi k}{2k_f})  \cos(\frac{\pi k}{2k_f}) \\ \cos(\frac{\pi k}{2k_f})  1 - \sin(\frac{\pi k}{2k_f}) \end{pmatrix}$。这个结果平滑地连接了两个[冻结区](@entry_id:262730)域的投影算符，从而成功地“退纠缠”了[能带交叉](@entry_id:161733)。

### [瓦尼尔函数](@entry_id:145994)构造中的高等主题

#### 旋量与[时间反演对称性](@entry_id:138094)

在包含重元素的真实材料中，**自旋-轨道耦合**（SOC）效应显著，此时电子[波函数](@entry_id:147440)必须被描述为**旋量**（spinors），即具有自旋分量 $\lvert u_{n\mathbf{k}} \rangle = \begin{pmatrix} u_{n\mathbf{k},\uparrow}(\mathbf{r}) \\ u_{n\mathbf{k},\downarrow}(\mathbf{r}) \end{pmatrix}$。[瓦尼尔函数](@entry_id:145994)的整个理论框架可以自然地推广到[旋量](@entry_id:158054)情况 [@problem_id:3502319]。

关键在于将所有[内积](@entry_id:158127)的定义推广到[旋量](@entry_id:158054)形式，即在对空间坐标积分的同时，也对自旋分量求和。例如，交叠矩阵的定义变为：
$
M_{mn}^{(\mathbf{k},\mathbf{b})} = \langle u_{m\mathbf{k}} \rvert u_{n,\mathbf{k}+\mathbf{b}} \rangle = \int_{V_c} d^3\mathbf{r} \sum_{s \in \{\uparrow, \downarrow\}} u_{m\mathbf{k},s}^*(\mathbf{r}) u_{n,\mathbf{k}+\mathbf{b},s}(\mathbf{r})
$
尽管计算交叠矩阵的底层操作变了，但后续的数学结构——包括[规范变换](@entry_id:176521)定律 $M' = U(\mathbf{k})^\dagger M U(\mathbf{k}+\mathbf{b})$ 和展宽泛函 $\Omega$ 的形式——都保持不变。这意味着最小化算法的核心逻辑无需修改。

然而，对称性（特别是[时间反演对称性](@entry_id:138094)，TRS）会对规范自由度施加额外的约束。对于自旋-1/2的电子，[时间反演](@entry_id:182076)算符 $\Theta$ 满足 $\Theta^2 = -1$。如果一个包含 $N_w$ 个能带的[子空间](@entry_id:150286)整体上是[时间反演](@entry_id:182076)不变的，并且我们希望构造出的[瓦尼尔函数](@entry_id:145994)也满足TRS，那么允许的[规范变换](@entry_id:176521) $U(\mathbf{k})$ 就不再是任意的 $\mathrm{U}(N_w)$ 矩阵。在这种情况下，$N_w$ 必须是偶数，[能带形成](@entry_id:746661) $N_K = N_w/2$ 个克拉默对。保持TRS的[规范变换](@entry_id:176521)矩阵必须属于**酉[辛群](@entry_id:189031)** $\mathrm{USp}(2N_K)$。这个群的维度（即自由参数的数量）为 $\frac{N_w(N_w+1)}{2}$，小于一般[酉群](@entry_id:138602) $\mathrm{U}(N_w)$ 的维度 $N_w^2$。这种规范自由度的减少，正是在TRS系统中可能出现 $\mathbb{Z}_2$ [拓扑阻碍](@entry_id:634492)的根源。

#### 对称性匹配的[瓦尼尔函数](@entry_id:145994)

在许多应用中，我们不仅希望瓦尼尔函数是局域的，还希望它们能反映[晶格](@entry_id:196752)的**[点群对称性](@entry_id:141230)**。例如，在一个立方钙钛矿中，我们可能希望构造三个分别具有 $d_{xy}$、$d_{yz}$、$d_{zx}$ 特征的[瓦尼尔函数](@entry_id:145994)，它们共同构成中心过渡金属原子位点 $O_h$ 点群的 $t_{2g}$ 不可约表示。

要实现这一点，必须在展宽泛函的最小化过程中施加额外的对称性约束 [@problem_id:3502342]。如果一组[瓦尼尔函数](@entry_id:145994) $\lbrace \lvert w_{n\mathbf{0}} \rangle \rbrace$ 构成了某个[不可约表示](@entry_id:263310)的[基矢](@entry_id:199546)，那么在任意一个点群[对称操作](@entry_id:143398) $\hat{g}$ 的作用下，它们必须按相应的表示矩阵 $D(g)$进行变换：
$
\hat{g}\lvert w_{n\mathbf{0}}\rangle = \sum_{m=1}^{N} \lvert w_{m\mathbf{0}}\rangle D_{mn}(g)
$
这个[实空间](@entry_id:754128)中的对称性要求，可以转化为对[倒空间](@entry_id:754151)中规范矩阵 $U(\mathbf{k})$ 的一个约束条件，即**缝合矩阵条件**（sewing matrix condition）：
$
U(g\mathbf{k}) = V_g(\mathbf{k}) U(\mathbf{k}) D(g)^{\dagger}
$
其中 $V_g(\mathbf{k})$ 是描述原始布洛赫[基矢](@entry_id:199546)在[对称操作](@entry_id:143398)下如何变换的缝合矩阵。

在实践中，强制执行此约束通常通过以下方式实现：
1.  **初始投影**：选择一组具有正确对称性的局域化**试探[轨道](@entry_id:137151)**（trial orbitals），如原子 $d$ [轨道](@entry_id:137151)，并将[布洛赫态](@entry_id:147552)投影到这些[轨道](@entry_id:137151)上，从而构造一个满足近似对称性的初始规范 $U(\mathbf{k})$。
2.  **[约束最小化](@entry_id:747762)**：在迭代最小化展宽泛函的每一步之后，对更新后的规范矩阵进行**再对称化**处理。这个过程将规范矩阵投影回满足缝合矩阵条件的对称性允许的[子空间](@entry_id:150286)中，从而确保最终得到的MLWFs是严格对称匹配的。

通过这些方法，我们可以构造出既最大局域又具有明确物理和化学意义的[瓦尼尔函数](@entry_id:145994)，为理解电子结构和构建有效的低能模型提供了强大的工具。