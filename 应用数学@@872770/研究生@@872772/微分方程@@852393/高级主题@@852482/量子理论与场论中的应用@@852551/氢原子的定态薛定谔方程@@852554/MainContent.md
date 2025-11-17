## 引言
氢原子，作为自然界最简单的原子，是量子力学发展史上的一个里程碑。精确描述其结构和[光谱](@entry_id:185632)不仅验证了新生的[量子理论](@entry_id:145435)，更提供了一套至今仍在物理学各领域发挥核心作用的分析工具。然而，如何从第一性原理出发，超越玻尔的半经典模型，完全在量子力学框架内解释氢原子的稳定性、分立能级以及[光谱](@entry_id:185632)规律，是早期量子力学面临的核心挑战。本文旨在系统地回答这一问题，深入剖析氢原子的定态薛定谔方程。

在接下来的内容中，我们将分三个部分展开：第一部分“原理与机制”将深入探讨薛定谔方程的数学结构，从直接求解微分方程到揭示其背后深刻的SO(4)代数对称性；第二部分“应用与跨学科联系”将展示氢原子模型如何作为理论基石，被应用于原子物理、凝聚态物理乃至粒子物理等多个前沿领域；最后，在“动手实践”部分，我们将通过具体的计算问题，巩固并加深对[波函数](@entry_id:147440)、量子效应等核心概念的理解。让我们首先进入第一部分，探索氢原子薛定谔方程的基本原理与内在机制。

## 原理与机制

在对氢原子进行量子力学描述时，核心是求解其[定态](@entry_id:137260)薛定谔方程。本章将深入探讨该方程的原理与机制，从直接求解其[微分方程](@entry_id:264184)到分析其解的普适性质，再到揭示其背后深刻的代数对称性。

### 氢原子薛定谔方程及其结构

氢原子（或[类氢原子](@entry_id:164890)）系统由一个带[电荷](@entry_id:275494) $+Ze$ 的[原子核](@entry_id:167902)和一个质量为 $m$、[电荷](@entry_id:275494)为 $-e$ 的电子构成，两者通过库仑力相互作用。在[质心系](@entry_id:168444)下，该系统的[定态](@entry_id:137260)薛定谔方程为：
$$
\left[ -\frac{\hbar^2}{2m}\nabla^2 - \frac{Ze^2}{4\pi\epsilon_0 r} \right] \psi(\mathbf{r}) = E \psi(\mathbf{r})
$$
其中 $m$ 是电子与[原子核](@entry_id:167902)的[折合质量](@entry_id:152420)，$\hbar$ 是约化普朗克常数，$\epsilon_0$ 是[真空介电常数](@entry_id:204253)，$r=|\mathbf{r}|$ 是电子到[原子核](@entry_id:167902)的距离。方程中的第一项是[动能算符](@entry_id:265633) $\hat{T}$，第二项是[库仑势能](@entry_id:263842)算符 $\hat{V}$。

由于库仑势 $V(r)$ 是中心对称的，我们可以在球坐标系 $(r, \theta, \phi)$ 中分离变量求解。[波函数](@entry_id:147440) $\psi(\mathbf{r})$ 可以写成径向部分 $R(r)$ 和角向部分 $Y_{lm}(\theta, \phi)$（即球谐函数）的乘积：
$$
\psi_{nlm}(r, \theta, \phi) = R_{nl}(r) Y_{lm}(\theta, \phi)
$$
角向部分的方程解出了球谐函数，并引入了[轨道角动量量子数](@entry_id:167573) $l$ 和[磁量子数](@entry_id:145584) $m_l$。我们在此重点关注描述电子径向行为的**[径向薛定谔方程](@entry_id:148306)**：
$$
-\frac{\hbar^2}{2m} \frac{1}{r^2} \frac{d}{dr} \left( r^2 \frac{dR(r)}{dr} \right) + \left[ \frac{\hbar^2 l(l+1)}{2mr^2} - \frac{Ze^2}{4\pi\epsilon_0 r} \right] R(r) = E R(r)
$$
这个方程的各项具有明确的物理意义。第一项是径向动能部分。方括号中的第一项，$\frac{\hbar^2 l(l+1)}{2mr^2}$，被称为**[离心势垒](@entry_id:147153)**（centrifugal barrier），它源于角动量守恒，在经典力学中相当于排斥性的“离心力”效应，使得具有角动量（$l>0$）的粒子难以接近原点。第二项是吸引性的库仑势。能量 $E$ 是整个系统的总能量。

### [径向波函数](@entry_id:266233)的性质与求解

求解[径向方程](@entry_id:191687)需要施加物理上合理的边界条件。物理上可接受的[波函数](@entry_id:147440)必须在全空间是归一化的，这意味着当 $r \to \infty$ 时，$R(r)$ 必须足够快地趋于零。同时，[波函数](@entry_id:147440)在原点 $r=0$ 处必须是正则的（即行为良好）。

#### [波函数](@entry_id:147440)在原点附近的行为

让我们考察当 $r \to 0$ 时[径向方程](@entry_id:191687)的性质。此时，离心势垒项（$\sim 1/r^2$）和库仑势项（$\sim 1/r$）相比于常数能量项 $E$ 变得非常大，因此 $E$ 项可以暂时忽略。方程近似为：
$$
\frac{1}{r^2}\frac{d}{dr}\left(r^2 \frac{dR}{dr}\right) - \frac{l(l+1)}{r^2}R \approx 0
$$
这是一个[欧拉-柯西方程](@entry_id:191139)，其解的形式为 $R(r) \sim r^s$。代入后可得特征方程 $s(s+1) - l(l+1) = 0$，其解为 $s=l$ 或 $s=-(l+1)$。由于[波函数](@entry_id:147440)在原点必须是正则的，我们必须舍弃发散的解 $r^{-(l+1)}$，保留 $R_{nl}(r) \sim C r^l$。这表明，在原点附近，[波函数](@entry_id:147440)的行为主要由离心势垒决定，角动量越大，[波函数](@entry_id:147440)在原点被抑制得越厉害。

然而，[库仑势](@entry_id:154276)的存在会对这种简单的[幂律](@entry_id:143404)行为引入修正。为了探究这种修正，我们可以考察[对数导数](@entry_id:169238) $f_{nl}(r) = \frac{r}{R_{nl}(r)}\frac{dR_{nl}(r)}{dr}$。对于纯[幂律](@entry_id:143404) $r^l$，我们有 $f_{nl}(r) = l$。包含库仑势的完整方程会给这个函数带来一个与 $r$ 相关的修正。通过将 $R_{nl}(r)$ 在原点附近展开为 $R_{nl}(r) = C r^l(1+\alpha r + \dots)$ 并代入完整的[径向方程](@entry_id:191687)，我们可以精确地确定系数 $\alpha$。[@problem_id:1160697]
经过计算，可以得到 $f_{nl}(r)$ 在原点的[一阶导数](@entry_id:749425)：
$$
\lim_{r\to 0} \frac{df_{nl}(r)}{dr} = \alpha = -\frac{mZe^2}{(l+1)4\pi\epsilon_0\hbar^2} = -\frac{Z}{(l+1)a_0}
$$
其中 $a_0 = \frac{4\pi\epsilon_0\hbar^2}{me^2}$ 是[玻尔半径](@entry_id:154675)。这表明 $f_{nl}(r)$ 在原点附近的行为是 $f_{nl}(r) \approx l - \frac{Z}{(l+1)a_0}r$。这个结果揭示了[库仑势](@entry_id:154276)是如何精细地调整[波函数](@entry_id:147440)在[原子核](@entry_id:167902)附近的行为的。

一个特别重要且具有物理意义的特例是 s-波（$l=0$）。此时[离心势垒](@entry_id:147153)消失。[波函数](@entry_id:147440)在原点处取有限值（$R(0) \neq 0$），但其导数在该点不为零，形成一个“尖点”（cusp）。这被称为**[Kato尖点条件](@entry_id:190242)**。我们可以通过考察 $r \to 0$ 时的[径向方程](@entry_id:191687)来推导它。对于 $l=0$，[波函数](@entry_id:147440) $R(r)$ 在原点附近可以展开为 $R(r) \approx A + Br$。代入薛定谔方程并分析主导项，可以得到 $A$ 和 $B$ 之间的关系。[@problem_id:1160703] 这直接给出了[波函数](@entry_id:147440)在原点的[对数导数](@entry_id:169238)值：
$$
\lim_{r \to 0} \left[ \frac{1}{R(r)} \frac{dR(r)}{dr} \right] = \frac{B}{A} = -\frac{mZe^2}{4\pi\epsilon_0\hbar^2} = -\frac{Z}{a_0}
$$
这个条件具有深刻的物理意义：在[原子核](@entry_id:167902)处，吸引[势能](@entry_id:748988)发散，为了保持能量有限，电子的动能也必须在该点发散以作补偿，而[波函数](@entry_id:147440)的尖点正是这种高动能的表现。

#### 一个精确可解的实例：“经典[圆形轨道](@entry_id:178728)”

虽然[径向方程](@entry_id:191687)的一般解涉及[缔合拉盖尔多项式](@entry_id:189823)，显得相当复杂，但我们可以通过一个特殊情况来直观地理解[能量量子化](@entry_id:137825)的来源。考虑所谓的“经典圆形轨道”态，其[角动量量子数](@entry_id:172069) $l$ 取给定[主量子数](@entry_id:143678) $n$ 下的最大值，即 $l=n-1$。对于这些态，[径向波函数](@entry_id:266233)具有特别简单的形式。[@problem_id:1160686]

让我们尝试一个形式为 $R(r) = C r^k e^{-\alpha r}$ 的试探解，并将其代入[径向方程](@entry_id:191687)。通过计算其导数并代入方程，我们要求方程对所有 $r$ 都成立。这意味着不同 $r$ 次幂的系数必须分别消失。通过匹配系数，我们可以唯一地确定参数 $k$ 和 $\alpha$，以及能量 $E$。

1.  分析方程在 $r \to \infty$ 和 $r \to 0$ 的行为，可以确定 $k=l$。由于我们考虑 $l=n-1$，所以 $k=n-1$。
2.  匹配 $1/r$ 项的系数，可以确定衰减参数 $\alpha$：
    $$
    \alpha = \frac{Zme^2}{4\pi\epsilon_0\hbar^2 n} = \frac{Z}{na_0}
    $$
3.  匹配常数项（与 $r$ 无关的项），最终确定了[能量本征值](@entry_id:144381) $E_n$：
    $$
    E_n = -\frac{\hbar^2 \alpha^2}{2m} = -\frac{mZ^2e^4}{2(4\pi\epsilon_0)^2\hbar^2 n^2}
    $$
    
因此，对于 $l=n-1$ 的态，其未归一化的[径向波函数](@entry_id:266233)为 $R_n(r) = r^{n-1} \exp\left(-\frac{Z}{na_0}r\right)$。这个例子清晰地表明，施加在[微分方程](@entry_id:264184)解上的物理约束（在原点和无穷远处的良好行为）导致了能量的量子化，并且能量值仅依赖于[主量子数](@entry_id:143678) $n$。

### 氢原子态的普适性质与基本定理

氢原子[本征态](@entry_id:149904)除具有特定的数学形式外，还遵循一些不依赖于具体量子数 $(n, l, m_l)$ 的普适定理。

#### 能量谱与简并性

从上述例子以及对[径向方程](@entry_id:191687)的完整分析中，我们得到氢原子束缚态（$E0$）的[能量本征值](@entry_id:144381)公式：
$$
E_n = -\frac{E_R Z^2}{n^2}, \quad \text{其中 } E_R = \frac{me^4}{2(4\pi\epsilon_0)^2\hbar^2} \approx 13.6 \, \text{eV}
$$
$E_R$ 是里德伯能量。最引人注目的特征是，能量仅依赖于**主量子数** $n=1, 2, 3, \dots$，而与[轨道角动量量子数](@entry_id:167573) $l$（$l=0, 1, \dots, n-1$）和磁量子数 $m_l$（$m_l=-l, \dots, l$）无关。这种能量对 $l$ 的不依赖性被称为**[偶然简并](@entry_id:141689)**（accidental degeneracy），它暗示了氢原子系统除了明显的[SO(3)旋转对称性](@entry_id:188417)之外，还存在一个更深层次的“隐藏”对称性。对于给定的 $n$，总简并度为 $\sum_{l=0}^{n-1}(2l+1) = n^2$。

#### [维里定理](@entry_id:146441)

**维里定理** (Virial Theorem) 是一个联系[定态](@entry_id:137260)动能[期望值](@entry_id:153208) $\langle \hat{T} \rangle$ 和势能[期望值](@entry_id:153208) $\langle \hat{V} \rangle$ 的基本关系。对于库仑势 $V(r) \propto r^{-1}$，维里定理断言 $2\langle \hat{T} \rangle = -\langle \hat{V} \rangle$。我们可以利用[变分原理](@entry_id:198028)来证明这一点。[@problem_id:1160546]

考虑一个归一化的真实本征态 $\psi(\mathbf{r})$，其能量为 $E = \langle \hat{T} \rangle + \langle \hat{V} \rangle$。我们构造一个由标度参数 $\lambda$ 控制的归一化[试探波函数](@entry_id:142892)族 $\psi_\lambda(\mathbf{r}) = \lambda^{3/2} \psi(\lambda\mathbf{r})$。根据[变分原理](@entry_id:198028)，对于这个[试探函数](@entry_id:756165)计算的[能量期望值](@entry_id:174035) $E(\lambda)$，在 $\lambda=1$ 处（即[试探函数](@entry_id:756165)变回真实[本征函数](@entry_id:154705)时）必须取[极值](@entry_id:145933)。

$E(\lambda)$ 的表达式可以计算如下：
$$
E(\lambda) = \langle\psi_\lambda| \hat{T} + \hat{V} |\psi_\lambda\rangle = \lambda^2 \langle\psi| \hat{T} |\psi\rangle + \lambda \langle\psi| \hat{V} |\psi\rangle = \lambda^2 \langle \hat{T} \rangle + \lambda \langle \hat{V} \rangle
$$
[动能算符](@entry_id:265633)包含[二阶导数](@entry_id:144508)（$\nabla^2$），因此缩放因子为 $\lambda^2$，而[势能](@entry_id:748988)算符仅与 $r$ 相关，缩放因子为 $\lambda$。
令其对 $\lambda$ 的导数在 $\lambda=1$ 处为零：
$$
\frac{dE(\lambda)}{d\lambda}\bigg|_{\lambda=1} = [2\lambda \langle \hat{T} \rangle + \langle \hat{V} \rangle]_{\lambda=1} = 2\langle \hat{T} \rangle + \langle \hat{V} \rangle = 0
$$
于是我们得到了维里定理：
$$
\frac{\langle \hat{T} \rangle}{\langle \hat{V} \rangle} = -\frac{1}{2}
$$
这一定理为我们提供了深刻的洞察：总能量 $E = \langle \hat{T} \rangle + \langle \hat{V} \rangle = -\langle \hat{T} \rangle = \frac{1}{2}\langle \hat{V} \rangle$。对于束缚态，$E0$，因此[势能](@entry_id:748988)[期望值](@entry_id:153208)是负的，而动能[期望值](@entry_id:153208)是正的，且大小是总能量的[绝对值](@entry_id:147688)。

#### 对应原理

玻尔的**[对应原理](@entry_id:155778)** (correspondence principle) 指出，在[大量子数](@entry_id:263219)极限下，量子力学的预言应该趋于经典物理学的预言。对于氢原子，这意味着当主量子数 $n$ 非常大时，从能级 $n$ 到 $n-1$ 跃迁所发射[光子](@entry_id:145192)的频率，应该等于电子在[经典轨道](@entry_id:177335)上运动的频率。[@problem_id:1160724]

从 $n$ 到 $n-1$ 跃迁的[光子](@entry_id:145192)频率 $f$ 为：
$$
f = \frac{E_n - E_{n-1}}{h} = \frac{E_R Z^2}{h} \left( \frac{1}{(n-1)^2} - \frac{1}{n^2} \right) = \frac{E_R Z^2}{h} \frac{2n-1}{n^2(n-1)^2}
$$
在 $n \gg 1$ 的极限下，$2n-1 \approx 2n$ 且 $(n-1)^2 \approx n^2$，所以：
$$
f \approx \frac{E_R Z^2}{h} \frac{2n}{n^4} = \frac{2E_R Z^2}{h n^3}
$$
这个频率应该等于[经典轨道](@entry_id:177335)周期 $T$ 的倒数。由此我们可以推导出大 $n$ 态的[经典轨道](@entry_id:177335)周期：
$$
T = \frac{1}{f} \approx \frac{h n^3}{2E_R Z^2} = \frac{2\pi(4\pi\epsilon_0)^2\hbar^3 n^3}{Z^2 m e^4}
$$
这个结果与完全基于经典力学（[开普勒第三定律](@entry_id:157744)）和[玻尔模型](@entry_id:146013)所推导出的周期完全一致，完美地展示了量子力学在其经典极限下的[自洽性](@entry_id:160889)。

### [代数结构](@entry_id:137052)与[隐藏对称性](@entry_id:169281)

氢原子能谱中出乎意料的 $l$ 简并性，暗示着存在比球对称性[SO(3)](@entry_id:138200)更高的对称性。这种对称性是由一个额外的[守恒量](@entry_id:150267)——**拉普拉斯-龙格-楞次（LRL）矢量**——所产生的。

#### [龙格-楞次矢量](@entry_id:168301)与SO(4)代数

在量子力学中，LRL矢量的厄米形式被定义为：
$$
\vec{A} = \frac{1}{2m}(\vec{p} \times \vec{L} - \vec{L} \times \vec{p}) - \frac{Ze^2}{4\pi\epsilon_0 r}\vec{r}
$$
可以证明 $[\hat{H}, \vec{A}] = 0$，因此 LRL 矢量是一个守恒量。为了揭示其[代数结构](@entry_id:137052)，我们研究[角动量算符](@entry_id:153013) $\vec{L}$ 和 LRL 算符 $\vec{A}$ 各分量之间的[对易关系](@entry_id:136780)。
除了熟知的[角动量对易关系](@entry_id:150953) $[L_i, L_j] = i\hbar\epsilon_{ijk}L_k$ 外，$\vec{L}$ 和 $\vec{A}$ 之间以及 $\vec{A}$ 各分量之间的[对易关系](@entry_id:136780)也至关重要。例如，通过冗长的但直接的计算，可以得到：
$$
[A_x, A_y] = -\frac{2i\hbar}{m} H L_z
$$
以及 $[L_x, A_y] = i\hbar A_z$。[@problem_id:1160547]

为了简化代数，我们通常只考虑束缚态[子空间](@entry_id:150286)（$E0$），并定义一个重新标度的无量纲LRL矢量：
$$
\mathbf{K} = \sqrt{\frac{-m}{2H}} \mathbf{A}
$$
在能量为 $E$ 的本征态[子空间](@entry_id:150286)上，这相当于 $\mathbf{K} = \sqrt{\frac{-m}{2E}} \mathbf{A}$。$\mathbf{L}$ 和 $\mathbf{K}$ 的分量满足以下[对易关系](@entry_id:136780)：
$$
[L_i, L_j] = i\hbar \epsilon_{ijk} L_k \\
[L_i, K_j] = i\hbar \epsilon_{ijk} K_k \\
[K_i, K_j] = i\hbar \epsilon_{ijk} L_k
$$
这组对易关系定义了四维旋转群SO(4)的李代数。这证实了[SO(4)对称性](@entry_id:142529)就是氢原子“[偶然简并](@entry_id:141689)”的根源。此外，这些算符还满足两个重要的恒等式：$\mathbf{L} \cdot \mathbf{K} = 0$ 和 $\mathbf{L}^2 + \mathbf{K}^2 = -\frac{m Z^2 e^4}{(4\pi\epsilon_0)^2 2E} - \hbar^2$。

#### 能量谱的纯代数推导

[SO(4)对称性](@entry_id:142529)的强大之处在于，它允许我们在不直接求解薛定谔方程的情况下，纯粹通过代数方法推导出氢原子的能谱。[@problem_id:1160654]

这个推导的精髓在于构造两个新的矢量算符：
$$
\mathbf{J}_1 = \frac{1}{2}(\mathbf{L} + \mathbf{K}) \quad \text{和} \quad \mathbf{J}_2 = \frac{1}{2}(\mathbf{L} - \mathbf{K})
$$
利用 $\mathbf{L}$ 和 $\mathbf{K}$ 的对易关系，可以证明 $\mathbf{J}_1$ 和 $\mathbf{J}_2$ 的分量各自满足一个独立的[SU(2)](@entry_id:136274)（角动量）代数，并且它们之间相互对易：$[J_{1,i}, J_{2,j}] = 0$。这意味着SO(4)代数同构于两个独立的SU(2)代数，即 SO(4) $\cong$ [SU(2)](@entry_id:136274) $\otimes$ SU(2)。

因此，我们可以用两个独立的角动量量子数 $j_1$ 和 $j_2$ 来标记系统的状态。根据角动量理论，$\mathbf{J}_1^2$ 和 $\mathbf{J}_2^2$ 的[本征值](@entry_id:154894)分别为 $j_1(j_1+1)\hbar^2$ 和 $j_2(j_2+1)\hbar^2$。

现在我们利用恒等式 $\mathbf{L} \cdot \mathbf{K} = 0$。将其用 $\mathbf{J}_1$ 和 $\mathbf{J}_2$ 表示，我们得到 $\mathbf{J}_1^2 - \mathbf{J}_2^2 = 0$，这意味着 $j_1(j_1+1) = j_2(j_2+1)$，所以 $j_1=j_2$。令 $j_1=j_2=j$，其中 $j$ 可以取 $0, 1/2, 1, 3/2, \dots$。

接下来，我们使用第二个恒等式：
$$
\mathbf{L}^2 + \mathbf{K}^2 = 2(\mathbf{J}_1^2 + \mathbf{J}_2^2) = 2(j(j+1)\hbar^2 + j(j+1)\hbar^2) = 4j(j+1)\hbar^2
$$
将此结果与原始恒等式 $\mathbf{L}^2 + \mathbf{K}^2 = -\frac{m Z^2 e^4}{(4\pi\epsilon_0)^2 2E} - \hbar^2$ 相结合，得到：
$$
4j(j+1)\hbar^2 = -\frac{m Z^2 e^4}{(4\pi\epsilon_0)^2 2E} - \hbar^2
$$
整理后得到：
$$
-\frac{m Z^2 e^4}{(4\pi\epsilon_0)^2 2E} = \hbar^2(4j(j+1)+1) = \hbar^2(2j+1)^2
$$
我们定义**主量子数** $n = 2j+1$。由于 $j$ 可以是 $0, 1/2, 1, \dots$，所以 $n$ 必须是正整数 $1, 2, 3, \dots$。最后，我们解出能量 $E$：
$$
E_n = -\frac{mZ^2e^4}{2(4\pi\epsilon_0)^2\hbar^2 n^2}
$$
这与我们通过[求解微分方程](@entry_id:137471)得到的结果完全一致，但此推导完全基于对称性原理，揭示了问题背后更深刻的数学结构。

### 不同表象与推广

#### [动量空间波函数](@entry_id:272371)

[对氢](@entry_id:753096)原子的分析通常在位置表象 $\psi(\mathbf{r})$ 中进行。然而，我们也可以在[动量表象](@entry_id:156131)中描述原子状态，即研究[动量空间波函数](@entry_id:272371) $\phi(\mathbf{p})$。两者通过三维[傅里叶变换](@entry_id:142120)相关联：
$$
\phi(\mathbf{p}) = \frac{1}{(2\pi\hbar)^{3/2}} \int d^3\mathbf{r} \, \psi(\mathbf{r}) \, e^{-i\mathbf{p}\cdot\mathbf{r}/\hbar}
$$
以氢[原子基态](@entry_id:194487)（$n=1, l=0, m_l=0$）为例，其位置空间[波函数](@entry_id:147440)为 $\psi_{100}(\mathbf{r}) = (\pi a_0^3)^{-1/2} e^{-r/a_0}$。我们可以通过直接计算傅里叶积分来求其[动量空间波函数](@entry_id:272371)。[@problem_id:1160623]
计算结果为：
$$
\phi(\mathbf{p}) = \frac{2\sqrt{2}\,a_0^{3/2}}{\pi\,\hbar^{3/2}}\frac{1}{\left(1 + \frac{p^2 a_0^2}{\hbar^2}\right)^2}
$$
其中 $p=|\mathbf{p}|$ 是动量的大小。这个结果表明，即使在能量最低的[基态](@entry_id:150928)，电子的动量也并非确定为零，而是遵循一个[分布](@entry_id:182848)。动量大小为 $p \approx \hbar/a_0$ 的概率最大，但存在一个扩展到很高动量的“尾巴”。这正是海森堡不确定性原理的体现：电子被束缚在[原子核](@entry_id:167902)周围一个大小约为 $a_0$ 的区域内，导致其动量具有一个约为 $\hbar/a_0$ 的不确定度。

#### 推广至D维空间

将[氢原子问题](@entry_id:270913)推广到任意 $D$ 维空间，是检验我们对问题结构理解深度的一个有效方法。在 $D$ 维空间中，[能量本征值](@entry_id:144381)仍然只依赖于[主量子数](@entry_id:143678) $n$，但简并度的计算方式会发生改变。给定[主量子数](@entry_id:143678) $n$，[轨道角动量量子数](@entry_id:167573) $l$ 的取值范围仍然是 $l = 0, 1, \dots, n-1$。然而，在 $D$ 维空间中，对应于一个给定 $l$ 值的超[球谐函数](@entry_id:178380)的数量（即 $l$-multiplet的简并度）为：
$$
d_l(D) = \binom{l+D-1}{D-1} - \binom{l+D-3}{D-1}
$$
其中 $\binom{N}{K}$ 是二项式系数。那么，第 $n$ 能级的总简并度 $g_n(D)$ 就是对所有可能的 $l$ 求和：[@problem_id:1160578]
$$
g_n(D) = \sum_{l=0}^{n-1} d_l(D) = \sum_{l=0}^{n-1} \left[ \binom{l+D-1}{D-1} - \binom{l+D-3}{D-1} \right]
$$
这是一个伸缩求和，利用[组合恒等式](@entry_id:272246) $\sum_{k=0}^{N}\binom{k+r}{r}=\binom{N+r+1}{r+1}$，可以得到一个封闭的表达式：
$$
g_n(D) = \binom{n+D-1}{D} - \binom{n+D-3}{D}
$$
这个结果对于 $D \ge 2$ 都成立。例如，在熟悉的 $D=3$ 维空间中，我们有 $g_n(3) = \binom{n+2}{3} - \binom{n}{3} = \frac{(n+2)(n+1)n}{6} - \frac{n(n-1)(n-2)}{6} = n^2$，这与我们熟知的结果一致。而在 $D=2$ 维空间中，$g_n(2) = \binom{n+1}{2} - \binom{n-1}{2} = 2n-1$。这种推广不仅是一个数学练习，它加深了我们对量子数和对称性如何共同决定量子系统[简并模式](@entry_id:196301)的理解。