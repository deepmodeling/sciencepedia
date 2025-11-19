## 引言
XY模型是[多体物理学](@entry_id:144526)中的一个基石，它以惊人的简洁性捕捉了从[量子磁性](@entry_id:145792)到拓扑物态等一系列复杂现象的本质。在面对充满挑战性的强关联系统时，物理学家们常常寻求可精确求解的模型作为理论的试金石和洞察力的源泉。XY模型正是这样一个典范，它为我们打开了一扇精确理解量子相变、临界现象和非[平凡拓扑](@entry_id:154009)效应的窗口，解决了直接研究更复杂模型时遇到的许多棘手难题。

本文将带领读者系统地探索XY模型的丰富内涵。在“原理与机制”一章中，我们将深入其核心，通过Jordan-Wigner变换和[Bogoliubov变换](@entry_id:160944)，揭示一维量子XY模型如何被精确地映射和[对角化](@entry_id:147016)，从而理解其能谱、[量子相变](@entry_id:146027)和[拓扑性质](@entry_id:141605)。随后的“应用与跨学科联系”一章将视野拓宽，展示XY模型的思想如何渗透到凝聚态物理、[量子信息](@entry_id:137721)和[冷原子](@entry_id:144092)等多个前沿领域，并重点介绍二维经典模型中的[Kosterlitz-Thouless相变](@entry_id:141676)。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者巩固理论知识并将其应用于具体计算。通过这三章的学习，你将全面掌握这一强大模型，并领会其在现代物理学中的深远影响。
## 原理与机制

继前一章对一维量子自旋模型的背景介绍之后，本章将深入探讨一类极其重要的可解模型——XY模型及其相关变体的核心物理原理与求解机制。我们将从模型的[哈密顿量](@entry_id:172864)出发，通过一系列精确的数学变换，揭示其丰富的物理内涵，包括量子相变、[临界现象](@entry_id:144727)、拓扑物态以及与多体物理中其他核心概念的深刻联系。

### 模型[哈密顿量](@entry_id:172864)及其特例

一维各向异性横场XY模型的[哈密顿量](@entry_id:172864)描述了一条自旋-1/2链，其中自旋在 $xy$ 平面内的相互作用具有各向异性，同时受到一个垂直于该平面的横向[磁场](@entry_id:153296)的影响。其[哈密顿量](@entry_id:172864)通常写作：

$$
H = - \sum_{i} \left( J_x S_i^x S_{i+1}^x + J_y S_i^y S_{i+1}^y \right) - h \sum_{i} S_i^z
$$

其中，$S_i^\alpha$（$\alpha = x, y, z$）是位于格点 $i$ 上的自旋-1/2算符，$J_x$ 和 $J_y$ 是最近邻自旋在 $x$ 和 $y$ 方向上的[交换耦合](@entry_id:154848)强度，$h$ 是横向[磁场](@entry_id:153296)的强度。为了方便分析，我们通常引入总[耦合强度](@entry_id:275517) $J$ 和各向异性参数 $\gamma$，将[哈密顿量](@entry_id:172864)改写为：

$$
H = -J \sum_{i} \left( \frac{1+\gamma}{2} S_i^x S_{i+1}^x + \frac{1-\gamma}{2} S_i^y S_{i+1}^y \right) - h \sum_{i} S_i^z
$$

这里，$J_x = J\frac{1+\gamma}{2}$ 和 $J_y = J\frac{1-\gamma}{2}$（假设总[耦合强度](@entry_id:275517)被归一化）。这个形式清晰地展示了模型的几个重要特例：

1.  **横场伊辛模型 (Transverse Field Ising Model, TFIM):** 当各向异性参数 $\gamma=1$ 时（即 $J_y=0$），模型退化为横场[伊辛模型](@entry_id:139066) [@problem_id:1224185]。这是研究[量子相变](@entry_id:146027)的最基本模型之一，其有序相对应于 $x$ 方向的[铁磁性](@entry_id:137256)。

2.  **各向同性XY模型 (XX模型):** 当 $\gamma=0$ 时（即 $J_x = J_y$），模型被称为XX模型 [@problem_id:1224186]。该模型具有围绕 $z$ 轴旋转的连续[U(1)对称性](@entry_id:154785)，这导致了其与TFIM截然不同的物理性质。

值得注意的是，一维量子XY模型应与二维经典XY模型区分开来。后者描述的是在二维平面上可以自由旋转的经典自旋，其在有限温度下的行为由著名的Kosterlitz-Thouless (KT) [相变](@entry_id:147324)所主导 [@problem_id:1224129]，我们将在本章末尾探讨这一联系与区别。

### [费米化](@entry_id:146892)：通往精确解的路径

XY模型能够被精确求解的关键在于它可以通过 **Jordan-Wigner (JW) 变换** 映射为一个无相互作用的[费米子](@entry_id:146235)系统。这个变换在[自旋算符](@entry_id:155419)和无自旋[费米子算符](@entry_id:149120)之间建立了一一对应的关系。

JW变换将每个格点上的自旋状态与[费米子](@entry_id:146235)占据数联系起来：自旋向下态 $(S_i^z = -1/2)$ 对应于[费米子](@entry_id:146235)真空态 ($n_i=0$)，自旋向上态 $(S_i^z = +1/2)$ 对应于[费米子](@entry_id:146235)占据态 ($n_i=1$)。这体现在 $z$ 分量[自旋算符](@entry_id:155419)与[费米子](@entry_id:146235)数算符的关系上：

$$
S_i^z = c_i^\dagger c_i - \frac{1}{2}
$$

其中 $c_i^\dagger$ 和 $c_i$ 是在格点 $i$ 上满足标准[反交换关系](@entry_id:153815)的[费米子](@entry_id:146235)产生和湮灭算符。对整个链求和，我们可以得到总磁化与总[费米子](@entry_id:146235)数之间的直接关系 [@problem_id:1224261]：

$$
\sum_{i=1}^N S_i^z = \sum_{i=1}^N \left( c_i^\dagger c_i - \frac{1}{2} \right) = \hat{N}_f - \frac{N}{2}
$$

其中 $\hat{N}_f = \sum_i c_i^\dagger c_i$ 是总[费米子](@entry_id:146235)数算符。

更重要的是，自旋的[升降算符](@entry_id:197899) $S_i^\pm = S_i^x \pm iS_i^y$ 被映射为[费米子算符](@entry_id:149120)，但带有一个非定域的“弦”因子，以保证不同格点上的[费米子算符](@entry_id:149120)满足正确的[反交换关系](@entry_id:153815)：

$$
S_i^+ = c_i^\dagger \exp\left(i\pi \sum_{j=1}^{i-1} c_j^\dagger c_j\right), \quad S_i^- = \exp\left(-i\pi \sum_{j=1}^{i-1} c_j^\dagger c_j\right) c_i
$$

尽管这个变换看起来很复杂，但幸运的是，对于最近邻[相互作用项](@entry_id:637283)，弦因子会相互抵消。例如，XY相互作用项 $S_i^x S_{i+1}^x + S_i^y S_{i+1}^y = \frac{1}{2}(S_i^+ S_{i+1}^- + S_i^- S_{i+1}^+)$ 变换后会变成一个简单的[费米子](@entry_id:146235)跃迁项 [@problem_id:1224195]：

$$
S_i^x S_{i+1}^x + S_i^y S_{i+1}^y = \frac{1}{2}(c_i^\dagger c_{i+1} + c_{i+1}^\dagger c_i)
$$

类似地，TFIM中的[相互作用项](@entry_id:637283)和各向异性项会产生[费米子配对](@entry_id:158762)项。例如，对于 $p$ 波配对[超导体](@entry_id:191025)中的配对项 $\Delta(c_i^\dagger c_{i+1}^\dagger + c_{i+1} c_i)$ [@problem_id:1224225]，它在自旋语言中就对应于 $\frac{1+\gamma}{2} S_i^x S_{i+1}^x - \frac{1-\gamma}{2} S_i^y S_{i+1}^y$ 类型的项。

经过JW变换，完整的XY[哈密顿量](@entry_id:172864)被转化为一个二次型的[费米子](@entry_id:146235)[哈密顿量](@entry_id:172864)，形如：

$$
H = \sum_{i,j} \left( A_{ij} c_i^\dagger c_j + \frac{1}{2} (B_{ij} c_i^\dagger c_j^\dagger + \text{h.c.}) \right)
$$

这是一个描述超导[费米子](@entry_id:146235)的[哈密顿量](@entry_id:172864)，其中包含跃迁项（$c_i^\dagger c_j$）和[库珀配对](@entry_id:195218)项（$c_i^\dagger c_j^\dagger$）。至此，一个复杂的自旋问题被转化为了一个可解的二次[费米子](@entry_id:146235)问题。

### 通过[Bogoliubov变换](@entry_id:160944)进行[对角化](@entry_id:147016)

为了求解上述二次[费米子](@entry_id:146235)[哈密顿量](@entry_id:172864)，我们通常分两步走：首先进行[傅里叶变换](@entry_id:142120)到[动量空间](@entry_id:148936)，然后进行[Bogoliubov变换](@entry_id:160944)。

对于一个具有平移不变性的周期性链，我们可以引入动量空间的[费米子算符](@entry_id:149120)：

$$
c_k = \frac{1}{\sqrt{N}} \sum_{j=1}^N e^{-ikj} c_j
$$

[哈密顿量](@entry_id:172864)随即变为一系列关于动量 $k$ 的[解耦](@entry_id:637294)块之和。对于每个动量 $k$，[哈密顿量](@entry_id:172864)通常具有如下的 **Bogoliubov-de Gennes (BdG)** 形式，它耦合了动量为 $k$ 和 $-k$ 的模式 [@problem_id:1224254]：

$$
H = \sum_{k>0} \Psi_k^\dagger \mathcal{H}_k \Psi_k + \text{常数}
$$

其中 $\Psi_k^\dagger = (c_k^\dagger, c_{-k})$ 是一个二分量[旋量](@entry_id:158054)，而 $\mathcal{H}_k$ 是一个 $2 \times 2$ 矩阵：

$$
\mathcal{H}_k = \begin{pmatrix} \xi_k  \Delta_k \\ \Delta_k^*  -\xi_{-k} \end{pmatrix}
$$

对于XY模型，我们有 $\xi_k = -J\cos k - h$ 和 $\Delta_k = iJ\gamma \sin k$（系数可能因具体定义而异）。对角项 $\xi_k$ 代表了[自由费米子](@entry_id:140103)的能量[色散](@entry_id:263750)，而非对角项 $\Delta_k$ 是[动量空间](@entry_id:148936)中的超导配对振幅。

这个 $2 \times 2$ 矩阵可以通过 **[Bogoliubov变换](@entry_id:160944)** [对角化](@entry_id:147016)。该变换定义了一组新的[费米子](@entry_id:146235)[准粒子](@entry_id:136584)算符 $\gamma_k$，它们是原有粒子 ($c_k$) 和空穴 ($c_{-k}^\dagger$) 的线性组合：

$$
c_k = u_k \gamma_k + i v_k \gamma_{-k}^\dagger
$$
$$
c_k^\dagger = u_k \gamma_k^\dagger - i v_k \gamma_{-k}
$$
其中 $u_k$ 和 $v_k$ 是满足[归一化条件](@entry_id:156486) $u_k^2 + v_k^2 = 1$ 的实系数 [@problem_id:1224172]。

通过这个变换，[哈密顿量](@entry_id:172864)被对角化为描述无相互作用的[Bogoliubov准粒子](@entry_id:139560)的形式：

$$
H = \sum_k E_k \left( \gamma_k^\dagger \gamma_k - \frac{1}{2} \right)
$$

其中 $E_k$ 是[准粒子](@entry_id:136584)的能量谱，它正是BdG矩阵 $\mathcal{H}_k$ 的正[本征值](@entry_id:154894)。通过简单的计算可知 [@problem_id:1224156]：

$$
E_k = \sqrt{\xi_k^2 + |\Delta_k|^2} = \sqrt{(-J\cos k - h)^2 + (J\gamma \sin k)^2}
$$

这个能量谱 $E_k$ 是系统的[元激发](@entry_id:140859)谱。系统的[基态](@entry_id:150928) $|GS\rangle$ 被定义为所有[Bogoliubov准粒子](@entry_id:139560)的真空态，即 $\gamma_k |GS\rangle = 0$ 对所有 $k$ 成立。

重要的是，这个[准粒子](@entry_id:136584)真空态并非[费米子](@entry_id:146235)真空。我们可以计算在[基态](@entry_id:150928)中原有[费米子](@entry_id:146235)的[动量分布](@entry_id:162113)函数 $n(k) = \langle GS| c_k^\dagger c_k |GS \rangle$。计算结果为 $n(k) = |v_k|^2$ [@problem_id:1224254]，其中

$$
|v_k|^2 = \frac{1}{2} \left( 1 - \frac{\xi_k}{E_k} \right) = \frac{1}{2} \left( 1 + \frac{J\cos k + h}{\sqrt{(-J\cos k - h)^2 + (J\gamma\sin k)^2}} \right)
$$

这个非零的占据数表明，即使在零温[基态](@entry_id:150928)下，动量为 $k$ 的[费米子](@entry_id:146235)态也有一定概率被占据，这是由[费米子配对](@entry_id:158762)效应引起的。

### 量子相变与[临界现象](@entry_id:144727)

[准粒子激发](@entry_id:138475)谱 $E_k$ 是理解系统[量子相变](@entry_id:146027)的关键。在零温下，量子相变发生在系统的一个或多个控制参数（如 $h/J$）变化时，导致[基态](@entry_id:150928)性质发生突变。这种突变通常与激发谱中的[能隙](@entry_id:191975) $\Delta = \min_k E_k$ 的关闭和重开联系在一起。

#### [相图](@entry_id:144015)与[临界线](@entry_id:171260)

对于各向异性XY模型，[能隙](@entry_id:191975)关闭的条件是 $E_k=0$ 对某个 $k$ 成立。由于 $E_k$ 是两个平方项之和的平方根，这要求两个平方项同时为零 [@problem_id:1224156]：
1.  $-J\cos k - h = 0$
2.  $J\gamma \sin k = 0$

对于非平庸的情况（$\gamma \neq 0$），第二式要求 $\sin k = 0$，即 $k=0$ 或 $k=\pi$。
-   若 $k=0$，第一式给出 $-J-h = 0 \implies h = -J$。
-   若 $k=\pi$，第一式给出 $J-h = 0 \implies h = J$。

因此，在 $(h/J, \gamma)$ [参数平面](@entry_id:195289)上，存在临界线 $h = J$ 和 $h=-J$（通常考虑 $h, J \ge 0$，故只关注 $h=J$），它们将不同的量子相分离开来：
-   **有序相 (铁[磁相](@entry_id:161372)):** 当 $|h|  J$ 时，系统存在一个有限的激发能隙，但自旋在 $xy$ 平面内具有长程关联（对于 $\gamma=1$ 的伊辛情况是[长程有序](@entry_id:155156)）。
-   **无序相 (顺磁相):** 当 $|h| > J$ 时，系统同样有[能隙](@entry_id:191975)，但[基态](@entry_id:150928)性质由横场主导，自旋倾向于沿着 $z$ 方向[排列](@entry_id:136432)，破坏了 $xy$ 平面的有序。

在[临界点](@entry_id:144653) $h=J$ 上，[能隙](@entry_id:191975)关闭，系统变为临界的。

#### [临界指数](@entry_id:142071)

在[量子临界点](@entry_id:144325)附近，许多物理量都表现出普适的标度行为，由一组临界指数描述。其中一个关键指数是关联长度指数 $\nu$。关联长度 $\xi$ 描述了关联函数指数衰减的特征尺度，它在[临界点](@entry_id:144653)发散。对于一维有[能隙](@entry_id:191975)系统，关联长度与[能隙](@entry_id:191975)成反比，$\xi \propto \Delta^{-1}$。

我们可以通过考察[能隙](@entry_id:191975) $\Delta$ 在[临界点](@entry_id:144653) $h_c = J$ 附近的行为来确定 $\nu$ [@problem_id:1224162]。对于 $h=J$ 的[相变](@entry_id:147324)，[能隙](@entry_id:191975)在 $k=\pi$ 处关闭。因此[能隙](@entry_id:191975)由 $E_\pi$ 决定：
$$
\Delta = E_\pi = \sqrt{(-J\cos\pi - h)^2} = |J-h|
$$
因此，关联长度 $\xi \propto |h-J|^{-1}$。根据定义 $\xi \sim |h-h_c|^{-\nu}$，我们立即得到[临界指数](@entry_id:142071) $\nu=1$。这个结果对于所有 $\gamma > 0$ 的情况都成立，表明它们都属于伊辛普适类。

#### [基态能量](@entry_id:263704)与物理可观测量

系统的[基态能量](@entry_id:263704)可以通过对所有负能[准粒子](@entry_id:136584)模式求和得到。在[热力学极限](@entry_id:143061)下，这个求和变成积分。例如，对于TFIM（$\gamma=1$），其[基态能量](@entry_id:263704)密度 $\mathcal{E}_{\text{Ising}}$ 可以通过对[准粒子](@entry_id:136584)谱积分得到，最终结果可以用第二类[完全椭圆积分](@entry_id:202935) $E(m)$ 表示 [@problem_id:1224185]：
$$
\mathcal{E}_{\text{Ising}} = -\frac{J}{\pi} (1+\frac{h}{J}) E\left( \frac{4 h/J}{(1 + h/J)^{2}} \right)
$$

在[基态](@entry_id:150928)上计算[物理可观测量](@entry_id:154692)是一个核心任务。由于局域的[自旋算符](@entry_id:155419)在[对角化](@entry_id:147016)的[准粒子](@entry_id:136584)基底下通常是非定域的复杂算符 [@problem_id:1224172]，计算关联函数通常需要细致的代数运算。