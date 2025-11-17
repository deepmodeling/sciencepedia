## 引言
在探索[量子多体系统](@entry_id:141221)的奥秘时，一个根本性的挑战是如何将微观世界的[哈密顿量](@entry_id:172864)与实验中可测量的宏观物理量联系起来。莱曼[谱表示](@entry_id:153219)（Lehmann spectral representation）正是为解决这一难题而生的强大理论框架，它为系统的动态响应函数提供了一个直接关联其完整能谱的精确表达式，弥合了理论模型与实验观测之间的鸿沟。本文将系统地引导读者深入理解这一核心工具。

在“原理与机制”一章中，我们将从第一性原理出发，详细推导莱曼[谱表示](@entry_id:153219)，并揭示[谱函数](@entry_id:147628)的深刻物理内涵。随后，在“应用与[交叉](@entry_id:147634)学科关联”一章中，我们将展示该表示如何在凝聚态物理、[量子化学](@entry_id:140193)等领域中被用于阐释单粒子谱、[集体激发](@entry_id:145026)和强关联效应等复杂现象。最后，通过一系列“动手实践”练习，读者将有机会将理论知识应用于具体物理模型，从而巩固和深化对莱曼[谱表示](@entry_id:153219)的理解。

## 原理与机制

在[量子多体系统](@entry_id:141221)的研究中，一个核心挑战是将系统的微观[哈密顿量](@entry_id:172864)及其本征态与实验中可观测的宏观物理量联系起来。莱曼[谱表示](@entry_id:153219)（Lehmann spectral representation），或称[Källén-Lehmann谱表示](@entry_id:155294)，正是为了应对这一挑战而建立的强大形式理论框架。它为双时间关联函数（或[格林函数](@entry_id:147802)）提供了一个精确的、非微扰的表达式，该表达式直接与系统的完整多体能谱相关联。本章将深入探讨莱曼[谱表示](@entry_id:153219)的基本原理、推导过程及其在不同物理情境下的各种形式与应用。

### 核心思想：连接微观与宏观的桥梁

莱曼[谱表示](@entry_id:153219)的根本思想是，任何描述系统动态响应的[线性响应函数](@entry_id:160418)，其在频率空间的结构，都完全由系统从一个本征态到另一个[本征态](@entry_id:149904)的所有可能跃迁所决定。每一次跃迁都对应谱中的一个[奇点](@entry_id:137764)（在有限体系中是极点，在无限体系中可能形成[连续谱](@entry_id:155477)），其位置由跃迁的能量差决定，其强度（或权重）则由跃迁[矩阵元](@entry_id:186505)的平方决定。

这个表示的有效性建立在几个基本假设之上 [@problem_id:3020315]：
1.  系统的[哈密顿量](@entry_id:172864) $\hat{H}$ 不随时间变化。
2.  [哈密顿量](@entry_id:172864) $\hat{H}$ 存在一个完备的正交归一的本征态基 $\{ \lvert n \rangle \}$，满足 $\hat{H} \lvert n \rangle = E_n \lvert n \rangle$。对于存在[连续谱](@entry_id:155477)的系统，求和需要被替换为积分。
3.  系统处于热平衡态，其状态由一个与[哈密顿量](@entry_id:172864)对易的密度矩阵 $\hat{\rho}$ 描述（例如，正则系综中的 $\hat{\rho} \propto \exp(-\beta \hat{H})$）。这一条件保证了关联函数具有[时间平移不变性](@entry_id:270209)。

在这些假设下，我们可以将复杂的、通常无法直接求解的关联函数的计算，转化为一个原则上可行的、对系统所有[本征态](@entry_id:149904)求和（或积分）的问题。

### 一般形式的推导：[推迟格林函数](@entry_id:139183)

为了具体说明[谱表示](@entry_id:153219)的推导过程，我们以一个普遍定义的[推迟格林函数](@entry_id:139183)（[retarded Green's function](@entry_id:139183)）为例。考虑两个任意的算符 $A$ 和 $B$，它们在[海森堡绘景](@entry_id:141162)中随[时间演化](@entry_id:153943)，即 $A(t) = e^{iHt} A e^{-iHt}$。[推迟格林函数](@entry_id:139183)定义为：
$$
G^{R}_{AB}(t) \equiv -i\, \theta(t)\, \langle [A(t), B(0)]_{\eta} \rangle
$$
其中 $\theta(t)$ 是亥维赛德[阶跃函数](@entry_id:159192)，保证了因果性（响应不先于驱动）；$\langle \cdot \rangle$ 表示在给定系综下的[热力学平均](@entry_id:755909)；广义对易子 $[X,Y]_{\eta} \equiv XY - \eta YX$，其中对于[玻色子](@entry_id:138266)系统 $\eta=+1$，对于[费米子](@entry_id:146235)系统 $\eta=-1$。

我们的目标是找到其[傅里叶变换](@entry_id:142120) $G^{R}_{AB}(\omega) = \int_{-\infty}^{\infty} dt\, e^{i \omega t}\, G^{R}_{AB}(t)$ 的[谱表示](@entry_id:153219) [@problem_id:3020323]。

首先，我们将热平均展开在[哈密顿量](@entry_id:172864)的本征态基 $\{ \lvert n \rangle \}$ 上。利用迹的循环不变性，并插入两组[完备基](@entry_id:143908) $\sum_m \lvert m \rangle \langle m \rvert = 1$，对易子的[期望值](@entry_id:153208)可以写为：
$$
\langle [A(t), B]_{\eta} \rangle = \frac{1}{Z} \sum_{m,n} \left(e^{-\beta E_m} - \eta e^{-\beta E_n}\right) \langle m|A|n \rangle \langle n|B|m \rangle e^{i(E_m-E_n)t}
$$
其中 $Z = \mathrm{Tr}(e^{-\beta H})$ 是[配分函数](@entry_id:193625)。注意，我们已经交换了第二个项中的求和指标 $m \leftrightarrow n$ 以便提取公因子。

接下来，进行[傅里叶变换](@entry_id:142120)。由于 $\theta(t)$ 的存在，积分范围为 $[0, \infty)$。为了保证积分在 $t \to \infty$ 时收敛，我们为频率 $\omega$ 引入一个无穷小的正虚部，即 $\omega \to \omega + i0^+$。
$$
G^{R}_{AB}(\omega) = -i \int_{0}^{\infty} dt\, e^{i \omega t}\, \langle [A(t), B]_{\eta} \rangle
$$
将对易子的表达式代入并对时间 $t$ 积分，我们得到：
$$
\int_{0}^{\infty} dt\, e^{i(\omega + E_m-E_n)t} = \frac{i}{\omega - (E_n-E_m) + i0^+}
$$
将所有部分组合起来，最终得到[推迟格林函数](@entry_id:139183)的莱曼[谱表示](@entry_id:153219)：
$$
G^{R}_{AB}(\omega) = \frac{1}{Z}\, \sum_{m,n} \frac{\left(e^{-\beta E_m} - \eta\, e^{-\beta E_n}\right)\, \langle m \lvert A \rvert n \rangle \langle n \lvert B \rvert m \rangle}{\omega - (E_n - E_m) + i 0^{+}}
$$
这个表达式是莱曼[表示的核](@entry_id:202190)心。它清晰地表明，格林函数 $G^{R}_{AB}(\omega)$ 在复频率平面上的[奇点](@entry_id:137764)位于[实轴](@entry_id:148276)上，其位置对应于系统本征态之间的能量差 $E_n - E_m$。这些[奇点](@entry_id:137764)是简单的极点，其留数由跃迁矩阵元 $\langle m \lvert A \rvert n \rangle \langle n \lvert B \rvert m \rangle$ 和玻尔兹曼热权重因子 $(e^{-\beta E_m} - \eta\, e^{-\beta E_n})$ 共同决定。

### 谱函数及其物理意义

上述莱曼表示虽然精确，但形式较为复杂。为了提炼其物理内涵，我们引入一个核心概念——**[谱函数](@entry_id:147628)**（spectral function），通常记为 $A(\omega)$。[谱函数](@entry_id:147628)与[推迟格林函数](@entry_id:139183)通过一个深刻的关系（本质上是Kramers-Kronig关系的一种体现）联系在一起。对于[单粒子格林函数](@entry_id:140400)（即 $A=c, B=c^\dagger$），谱函数通常定义为 [@problem_id:3020316]：
$$
A(\omega) \equiv -\frac{1}{\pi}\operatorname{Im} G^{R}(\omega)
$$
利用关系式 $\operatorname{Im}\left(\frac{1}{x + i0^{+}}\right) = -\pi \delta(x)$，我们可以从 $G^R(\omega)$ 的莱曼表示中直接读出[谱函数](@entry_id:147628)的表达式。以单[费米子](@entry_id:146235)[格林函数](@entry_id:147802)为例（$A=c, B=c^\dagger, \eta=-1$）：
$$
A(\omega) = \frac{1}{Z} \sum_{m,n} (e^{-\beta E_m} + e^{-\beta E_n}) |\langle m|c|n \rangle|^2 \delta(\omega - (E_n - E_m))
$$
谱函数的物理意义至关重要：
-   **激发谱的密度**：谱函数 $A(\omega)$ 是一个关于能量 $\omega$ 的[分布函数](@entry_id:145626)。$\delta(\omega - (E_n - E_m))$ 项表明，谱函数只在系统允许的激发能量 $\omega = E_n - E_m$ 处有值。因此，$A(\omega)$ 给出了在能量 $\omega$ 处，增加一个粒子（当 $E_n > E_m$ 时）或移除一个粒子（当 $E_n  E_m$ 时）的[激发态](@entry_id:261453)密度。
-   **跃迁几率**：$A(\omega)$ 在每个能量点上的权重由 $|\langle m|c|n \rangle|^2$ 给出，这是从态 $\lvert m \rangle$ 跃迁到态 $\lvert n \rangle$ 的量子力学几率幅的模方，代表了跃迁的强度。
-   **正定性**：从其表达式可以看出，[谱函数](@entry_id:147628) $A(\omega)$ 是一个由正权重构成的和，因此它总是非负的，$A(\omega) \ge 0$。

此外，[谱函数](@entry_id:147628)还满足重要的**求和规则**（sum rules）。其零阶矩由等时[对易关系](@entry_id:136780)决定 [@problem_id:3020294]：
$$
M_0 = \int_{-\infty}^{\infty} d\omega\, A(\omega) = \langle \{c, c^{\dagger}\} \rangle = 1
$$
这个求和规则意味着谱函数的总积分是守恒的，反映了粒子数的守恒性。更高阶的矩，如一阶矩 $M_1 = \int \omega A(\omega) d\omega$，也与系统的基本物理量（如动能）相关。

### [谱表示](@entry_id:153219)的变体与推广

莱曼表示的框架非常灵活，可以适应不同的理论表述和物理情境。

#### 虚时形式与[松原频率](@entry_id:197724)

在许多[量子场论](@entry_id:138177)计算中，尤其是在使用路径积分方法时，采用虚时（imaginary time）$\tau = it$ 更为方便。虚时格林函数定义为 $G(\tau) = -\langle \mathcal{T}_{\tau}\, c(\tau)\, c^{\dagger}(0) \rangle$，其中 $\mathcal{T}_{\tau}$ 是虚时排序算符。通过类似的推导，可以得到 $G(\tau)$ 的莱曼表示 [@problem_id:3020296]。更有用的是，它的[傅里叶变换](@entry_id:142120)——[松原格林函数](@entry_id:199218) $G(i\omega_n)$，可以直接通过[谱函数](@entry_id:147628) $A(\omega)$ 表示：
$$
G(i\omega_n) = \int_{-\infty}^{\infty} d\omega' \frac{A(\omega')}{i\omega_n - \omega'}
$$
其中 $i\omega_n = i(2n+1)\pi/\beta$ 是[费米子](@entry_id:146235)的[松原频率](@entry_id:197724)。这个简洁的公式是连接平衡态[多体理论](@entry_id:169452)计算（通常在[松原频率](@entry_id:197724)上进行）和可观测物理量（包含在实频谱函数 $A(\omega)$ 中）的枢纽。通过[解析延拓](@entry_id:147225)（analytic continuation），人们可以从计算出的 $G(i\omega_n)$ 反演出 $A(\omega)$。

#### [大格林函数](@entry_id:142137)与[小格林函数](@entry_id:141540)

为了更细致地分析激发过程，可以定义[大格林函数](@entry_id:142137)（greater Green's function）$G^{>}(t) = -i\langle A(t)B(0)\rangle$ 和[小格林函数](@entry_id:141540)（lesser Green's function）$G^{}(t) = \mp i\langle B(0)A(t)\rangle$。它们的莱曼表示直接反映了系统中的粒子发射和吸收过程 [@problem_id:3020281]：
$$
G^{>}(\omega) \propto \sum_{m,n} e^{-\beta E_m} |\langle m|A|n \rangle|^2 \delta(\omega - (E_n - E_m))
$$
$$
G^{}(\omega) \propto \sum_{m,n} e^{-\beta E_n} |\langle m|A|n \rangle|^2 \delta(\omega - (E_n - E_m))
$$
$G^{>}(\omega)$ 的权重是初态 $m$ 的[玻尔兹曼因子](@entry_id:141054) $e^{-\beta E_m}$，描述了从 $m$ 态到 $n$ 态的跃迁（能量为 $\omega$ 的激发被发射）。相反，$G^{}(\omega)$ 的权重是末态（此时作为初态）$n$ 的玻尔兹曼因子，描述了吸收一个能量为 $\omega$ 的激发的逆过程。这两者之间存在一个精确的关系，即**Kubo-Martin-Schwinger (KMS) 关系**：$G^{>}(\omega) = e^{\beta\omega} G^{}(\omega)$（对[玻色子](@entry_id:138266)而言）。这个关系是[热平衡](@entry_id:141693)态[细致平衡原理](@entry_id:200508)在[量子统计](@entry_id:143815)中的深刻体现。

#### [正则系综](@entry_id:142391)与[巨正则系综](@entry_id:141562)

在处理粒子数可变的系统时，通常采用[巨正则系综](@entry_id:141562)。这会对莱曼表示产生直接影响 [@problem_id:3020293]。在[巨正则系综](@entry_id:141562)中，系统的演化和[统计权重](@entry_id:186394)由巨正则[哈密顿量](@entry_id:172864) $\hat{K} = \hat{H} - \mu \hat{N}$ 决定。因此，推导中的所有步骤都将使用 $\hat{K}$ 的[本征值](@entry_id:154894) $\mathcal{E}_n = E_n - \mu N_n$ 和[本征态](@entry_id:149904)。最终，[谱表示](@entry_id:153219)中的两个关键部分都会发生改变：
1.  **[玻尔兹曼权重](@entry_id:137515)**：由 $e^{-\beta E_n}$ 变为 $e^{-\beta \mathcal{E}_n} = e^{-\beta (E_n - \mu N_n)}$。
2.  **跃迁频率**：由 $E_n - E_m$ 变为 $\mathcal{E}_n - \mathcal{E}_m = (E_n - E_m) - \mu(N_n - N_m)$。
对于[单粒子格林函数](@entry_id:140400)，跃迁前后粒子数变化为 $\Delta N = N_n - N_m = \pm 1$，因此跃迁频率会包含一个化学势 $\mu$ 的平移项。

### 应用与物理实例

#### 一个精确可解的模型：原子极限

为了使这些抽象的公式变得具体，让我们考虑一个简单的可解模型：单[轨道](@entry_id:137151)原子极限 [@problem_id:3020291]。其[哈密顿量](@entry_id:172864)为 $H = \epsilon \sum_{\sigma} n_{\sigma} + U n_{\uparrow} n_{\downarrow}$。该系统只有四个态：空态 $|0\rangle$，单占据态 $|\sigma\rangle$，和双占据态 $|d\rangle$。在[巨正则系综](@entry_id:141562)中，它们的能量（$\hat{K}$ 的[本征值](@entry_id:154894)）分别为 $\mathcal{E}_0 = 0$、$\mathcal{E}_1 = \epsilon - \mu$、$\mathcal{E}_2 = 2\epsilon + U - 2\mu$。

假设化学势 $\mu$ 处于 $\epsilon  \mu  \epsilon+U$ 之间，此时[基态](@entry_id:150928)是单占据态，能量为 $\mathcal{E}_{GS} = \epsilon - \mu$。我们来计算此时的单粒子[谱函数](@entry_id:147628) $A(\omega)$。
-   **移除粒子（空穴激发）**：我们从[基态](@entry_id:150928) $|\sigma\rangle$ 移除一个电子，系统跃迁到空态 $|0\rangle$。根据莱曼表示，谱峰位置为 $\omega_{rem} = \mathcal{E}_{GS} - \mathcal{E}_0 = (\epsilon - \mu) - 0 = \epsilon - \mu$。
-   **增加粒子（电子激发）**：我们向[基态](@entry_id:150928) $|\bar{\sigma}\rangle$（与移除的[电子自旋](@entry_id:137016)相反）增加一个电子，系统跃迁到双占据态 $|d\rangle$。谱峰位置为 $\omega_{add} = \mathcal{E}_2 - \mathcal{E}_{GS} = (2\epsilon + U - 2\mu) - (\epsilon - \mu) = \epsilon + U - \mu$。

结果表明，[谱函数](@entry_id:147628)在 $\omega = \epsilon - \mu$ 和 $\omega = \epsilon + U - \mu$ 处有两个 $\delta$-函数峰。这清晰地展示了化学势 $\mu$ 的作用：它充当了能量的参考零点，将整个[能谱](@entry_id:181780)统一平移了 $-\mu$。

#### 具有配对的系统：Nambu 形式

在超导等具有[库珀配对](@entry_id:195218)的系统中，粒子数不再是严格守恒的量。为了处理这种情况，引入了 Nambu 旋量 formalism。例如，可以定义一个二维的 Nambu [旋量](@entry_id:158054) $\Psi_{k}^{\dagger}=\big(c_{k\uparrow}^{\dagger},\,c_{-k\downarrow}\big)$。其格林函数 $\hat{G}(k,\tau)=-\langle T_{\tau}\, \Psi_{k}(\tau)\,\Psi_{k}^{\dagger}(0)\rangle$ 是一个 $2 \times 2$ 矩阵。莱曼表示可以自然地推广到这种矩阵形式 [@problem_id:3020284]。矩阵[谱函数](@entry_id:147628) $\hat{A}(k,\omega)$ 同样由[本征态](@entry_id:149904)之间的跃迁决定：
$$
A_{ab}(k,\omega) = \frac{1}{Z}\sum_{m,n}\big(e^{-\beta E_{m}}+e^{-\beta E_{n}}\big)\,\langle m|\Psi_{k,a}|n\rangle\,\langle n|\Psi_{k,b}^{\dagger}|m\rangle\,\delta\big(\omega-(E_{n}-E_{m})\big)
$$
其中 $a,b \in \{1,2\}$ 是 Nambu 指数。对角元 $A_{11}$ 和 $A_{22}$ 分别对应于粒子和空穴的谱函数，而非对角元 $A_{12}$ 和 $A_{21}$（称为反常[谱函数](@entry_id:147628)）则描述了粒子与空穴之间的转换，其非零值是存在配对序的直接证据。

#### 多粒子激发与连续谱

莱曼表示同样适用于多粒子算符。例如，考虑[密度算符](@entry_id:138151) $\hat{\rho}_{\mathbf{q}} = \sum_{\mathbf{k},\sigma} \hat{c}^{\dagger}_{\mathbf{k}+\mathbf{q},\sigma} \hat{c}_{\mathbf{k},\sigma}$ 的关联函数 [@problem_id:3020312]。这个算符在[基态](@entry_id:150928)上作用，会产生粒子-空穴对激发。在相互作用体系中，一个粒子-空穴对并非系统的[本征态](@entry_id:149904)，而是许多具有相同[总动量](@entry_id:173071) $\mathbf{q}$ 的[精确本征态](@entry_id:138620)的叠加。

在有限体积中，这些本征态的能量是离散的，[谱函数](@entry_id:147628)是一系列密集的 $\delta$-峰。然而，当取[热力学极限](@entry_id:143061) $V \to \infty$ 时，这些离散的能级会合并形成**[连续谱](@entry_id:155477)**（continuum）。这是因为对于一个给定的总动量 $\mathbf{q}$，粒子-空穴对的相对动量可以连续变化，从而形成一个能量带。此时，莱曼表示中的求和自然地过渡为积分：
$$
A_{\rho \rho}^{\text{cont}}(\mathbf{q},\omega) \propto \int d^d \mathbf{k} \,| M(\mathbf{q},\mathbf{k}) |^2 \,\delta(\omega - \omega(\mathbf{q}, \mathbf{k}))
$$
这里 $\omega(\mathbf{q}, \mathbf{k})$ 是一个具有[总动量](@entry_id:173071) $\mathbf{q}$ 和内部动量 $\mathbf{k}$ 的[粒子-空穴激发](@entry_id:137289)的能量。这个积分形式明确地展示了多粒子激发如何导致[谱函数](@entry_id:147628)中出现宽阔的连续区域，这与可能存在的、对应于束缚态（如激子）的尖锐 $\delta$-峰形成对比。

### 实际计算中的考虑：截断与求和规则

尽管莱曼表示在形式上是精确的，但在实际数值计算中（如精确[对角化](@entry_id:147016)或[密度矩阵重整化群](@entry_id:137826)），我们只能处理一个有限的、被截断的希尔伯特空间。这意味着计算出的谱函数 $A_{\mathrm{tr}}(\omega)$ 只包含了能量低于某个[截断能](@entry_id:177594) $\Lambda$ 的跃迁，而忽略了所有高能贡献 [@problem_id:3020294]。

由于谱函数 $A(\omega)$ 的[正定性](@entry_id:149643)，这种截断必然导致谱矩求和规则的违反。例如，计算出的零阶矩 $M_{0}^{\mathrm{tr}} = \int A_{\mathrm{tr}}(\omega)d\omega$ 将小于其精确值 $M_0=1$。这个差额 $\Delta_0 = M_0 - M_{0}^{\mathrm{tr}}$ 正是所有被忽略的高能跃迁的总[谱权重](@entry_id:144751)。

为了修正这个问题，同时保留来之不易的低能谱信息的准确性，可以采用一种物理上合理的修正方案。我们可以构造一个只在高能区（$|\omega| > \Lambda$）有值的“尾巴”函数 $T(\omega) \ge 0$，并将其加到截断谱上：$A_{\mathrm{corr}}(\omega) = A_{\mathrm{tr}}(\omega) + T(\omega)$。这个尾巴函数的形式可以很简单（例如，一个或几个 $\delta$-函数），但其总权重和一阶矩被设定为恰好弥补截断谱的矩亏损：
$$
\int d\omega\, T(\omega) = \Delta_0, \quad \int d\omega\, \omega\, T(\omega) = \Delta_1 = M_1 - M_{1}^{\mathrm{tr}}
$$
这种方法不仅能恢复精确的求和规则，而且因为它只在计算不可靠的高能区进行修正，所以它能最大程度地尊[重数](@entry_id:136466)值计算给出的低能物理。这体现了莱曼表示不仅是理论分析的工具，也能指导和改进数值计算的实践。