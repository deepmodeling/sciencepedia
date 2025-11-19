## 引言
在量子世界中，粒子间的相互作用大多通过[散射实验](@entry_id:173304)来探测。S矩阵与[散射理论](@entry_id:143476)为描述这些碰撞过程的结果提供了一套基本且强大的语言。它不仅是理论物理的基石，也是连接理论预言与高能、[核物理](@entry_id:136661)及凝聚态实验数据的核心桥梁。面对复杂的相互作用，我们如何从一个给定的初态系统地预测所有可能的末态，并揭示相互作用势的内在性质？[S矩阵理论](@entry_id:138072)正是为了解决这一核心问题而建立的，它将抽象的动力学演化封装在一个定义明确的数学对象中。

本文将引导读者深入S矩阵的世界。在“原理与机制”一章中，我们将建立形式[散射理论](@entry_id:143476)，定义S矩阵并探讨其幺正性、解析性等基本性质，并介绍分波分析这一关键工具。接下来的“应用与跨学科联系”一章将展示[S矩阵理论](@entry_id:138072)如何在[核物理](@entry_id:136661)、粒子物理、原子物理乃至前沿理论中发挥作用，揭示其强大的解释力和普适性。最后，通过“动手实践”部分，读者将有机会运用所学知识解决具体问题，加深理解。

## 原理与机制

本章旨在深入探讨[量子散射理论](@entry_id:140687)的核心原理与机制。在前一章介绍背景之后，我们将系统地建立描述散射过程的数学框架，从散射[波函数](@entry_id:147440)的物理图像出发，逐步引入S矩阵的形式化定义，并阐述其[幺正性](@entry_id:138773)、解析性等基本性质。我们将详细讨论分波方法，并揭示[散射振幅](@entry_id:155369)的奇异性如何与束缚态、共振态等物理现象[一一对应](@entry_id:143935)。

### 散射[波函数](@entry_id:147440)与[截面](@entry_id:154995)

在量子力学中，散射过程通常被描述为一个入射粒子束与一个靶（或势场）相互作用，然后向各个方向散射开来。在[定态](@entry_id:137260)图景下，整个系统由一个单一的能量本征态——**[散射态](@entry_id:150968)**——来描述。对于一个沿 $z$ 轴入射、动量为 $\hbar\mathbf{k}$ 的粒子束，其对应的散射[波函数](@entry_id:147440) $\psi(\mathbf{r})$ 在远离散射中心（$r \to \infty$）的区域，具有一种特定的渐近形式。

这个渐近形式由两部分构成：一部分是未受扰动的入射[平面波](@entry_id:189798) $e^{i\mathbf{k}\cdot\mathbf{r}}$，另一部分则是向外传播的[球面波](@entry_id:200471)。[球面波](@entry_id:200471)的振幅随着距离 $r$ 按 $1/r$ 的规律减小，以保证通过任何以散射中心为球心的球面总几率流守恒。因此，[波函数](@entry_id:147440)的渐近形式可以写为：
$$
\psi(\mathbf{r}) \sim e^{i\mathbf{k}\cdot\mathbf{r}} + f(\theta, \phi) \frac{e^{ikr}}{r}
$$
其中 $k = |\mathbf{k}|$ 是[波数](@entry_id:172452)，$(\theta, \phi)$ 是描述散射方向的[球坐标](@entry_id:146054)。系数 $f(\theta, \phi)$ 被称为**[散射振幅](@entry_id:155369)**，它描述了散射粒子在不同方向上的[分布](@entry_id:182848)，是连接理论与实验的关键。

实验上可测量的物理量是**[微分截面](@entry_id:137333)** $\frac{d\sigma}{d\Omega}$，它被定义为单位时间内散射到某个立体角元 $d\Omega$ 内的粒子数（即散射通量），与单位面积的入射粒子束通量之比。我们可以通过量子力学的几率流密度来建立[散射振幅](@entry_id:155369)与[微分截面](@entry_id:137333)之间的关系 [@problem_id:2664494]。

[定态](@entry_id:137260)[波函数](@entry_id:147440)的几率流密度由下式给出：
$$
\mathbf{j}(\mathbf{r}) = \frac{\hbar}{2mi}(\psi^*\nabla\psi - \psi\nabla\psi^*) = \frac{\hbar}{m}\text{Im}(\psi^*\nabla\psi)
$$
对于入射波 $\psi_{inc} = e^{i\mathbf{k}\cdot\mathbf{r}}$，入射流密度为 $\mathbf{j}_{inc} = \frac{\hbar\mathbf{k}}{m}$，其大小为 $j_{inc} = \frac{\hbar k}{m}$。

对于散射波 $\psi_{sc} = f(\theta, \phi) \frac{e^{ikr}}{r}$，在 $r \to \infty$ 的极限下，[梯度算子](@entry_id:275922) $\nabla$ 的主要贡献来自对 $e^{ikr}$ 的径向求导，即 $\nabla\psi_{sc} \approx \hat{\mathbf{r}} \frac{\partial\psi_{sc}}{\partial r} \approx \hat{\mathbf{r}} (ik) \psi_{sc}$。因此，散射[粒子流](@entry_id:753205)密度在渐近区是沿径向向外的：
$$
\mathbf{j}_{sc} \approx \frac{\hbar}{m}\text{Im}\left( f^* \frac{e^{-ikr}}{r} \cdot \hat{\mathbf{r}} (ik) f \frac{e^{ikr}}{r} \right) = \hat{\mathbf{r}} \frac{\hbar k}{m} \frac{|f(\theta, \phi)|^2}{r^2}
$$
穿过半径为 $r$ 的球面上一个面积元 $d\mathbf{S} = \hat{\mathbf{r}}r^2 d\Omega$ 的散射通量为 $d\Phi_{sc} = \mathbf{j}_{sc} \cdot d\mathbf{S} = \frac{\hbar k}{m}|f(\theta, \phi)|^2 d\Omega$。

根据[微分截面](@entry_id:137333)的定义，我们得到：
$$
\frac{d\sigma}{d\Omega} = \frac{d\Phi_{sc}/d\Omega}{j_{inc}} = \frac{(\hbar k/m)|f(\theta, \phi)|^2}{\hbar k/m} = |f(\theta, \phi)|^2
$$
这个简洁而深刻的公式表明，[微分截面](@entry_id:137333)就是[散射振幅](@entry_id:155369)模的平方。它构成了[量子散射理论](@entry_id:140687)中连接理论计算与实验测量的基本桥梁。值得注意的是，散射振幅 $f(\theta, \phi)$ 的量纲是长度，而[微分截面](@entry_id:137333) $\frac{d\sigma}{d\Omega}$ 的量纲是面积，这与它们的物理意义相符。

### 形式[散射理论](@entry_id:143476)：渐近态与[S矩阵](@entry_id:137017)

为了更严谨地处理散射问题，我们需要一个更形式化的数学框架。考虑一个系统的总[哈密顿量](@entry_id:172864) $H = H_0 + V$，其中 $H_0$ 是自由[哈密顿量](@entry_id:172864)，$V$ 是相互作用势。在[相互作用绘景](@entry_id:198213)中，我们比较真实系统的[演化算符](@entry_id:182628) $U(t) = e^{-iHt/\hbar}$ 与自由系统的[演化算符](@entry_id:182628) $U_0(t) = e^{-iH_0t/\hbar}$。

一个在遥远过去 ($t \to -\infty$) 表现为自由态 $|\phi_{in}\rangle$ 的[散射态](@entry_id:150968)，在 $t=0$ 时刻的真实状态 $|\Psi^{(+)}\rangle$ 可以通过**Møller波算符** $\Omega^{(+)}$ 从 $|\phi_{in}\rangle$ 构造出来：
$$
|\Psi^{(+)}\rangle = \Omega^{(+)} |\phi_{in}\rangle
$$
其中，Møller算符被定义为强极限 [@problem_id:2664459]：
$$
\Omega^{(\pm)} = \operatorname*{s-lim}_{t \to \mp\infty} e^{iHt/\hbar}e^{-iH_0t/\hbar}
$$
这里的强极限（strong limit, $\operatorname*{s-lim}$）意味着算符作用在任何一个态矢量上都收敛。$\Omega^{(+)}$ 将一个在 $t=0$ 时刻的自由态演化到 $t \to -\infty$，再用真实[哈密顿量](@entry_id:172864)演化回 $t=0$，从而将一个“入”自由态映射为真实的[散射态](@entry_id:150968)。同理，$\Omega^{(-)}$ 将一个“出”自由态（在 $t \to +\infty$ 时的渐近态）映射为 $t=0$ 的真实[散射态](@entry_id:150968)。

对于短程势（例如，[势函数](@entry_id:176105) $V(r)$ 的衰减速度比 $1/r$ 更快），这些极限存在且Møller算符是等距算符，即 $\Omega^{(\pm)\dagger}\Omega^{(\pm)} = I$。如果系统的所有[散射态](@entry_id:150968)可以由所有入射自由态生成，我们就称系统是**渐近完备**的。这时，Møller算符的[靶空间](@entry_id:143180)是 $H$ 的绝对连续谱[子空间](@entry_id:150286) $\mathcal{H}_{ac}(H)$，即 $\text{Ran}\,\Omega^{(\pm)} = \mathcal{H}_{ac}(H)$。

同一个[散射态](@entry_id:150968) $|\Psi\rangle$，在遥远的过去来自某个入射态 $|\phi_{in}\rangle$，在遥远的未来将演化为某个出射态 $|\phi_{out}\rangle$。它们之间的关系是：
$$
|\Psi\rangle = \Omega^{(+)} |\phi_{in}\rangle = \Omega^{(-)} |\phi_{out}\rangle
$$
由此，我们可以定义一个算符，它直接将入射态映射到相应的出射态。这个算符就是大名鼎鼎的**[散射矩阵](@entry_id:137017)**（S-matrix）：
$$
|\phi_{out}\rangle = (\Omega^{(-)})^{-1} \Omega^{(+)} |\phi_{in}\rangle = \Omega^{(-)\dagger} \Omega^{(+)} |\phi_{in}\rangle \equiv S |\phi_{in}\rangle
$$
因此，S矩阵的定义为 [@problem_id:2664490]：
$$
S = \Omega^{(-)\dagger} \Omega^{(+)}
$$
[S矩阵](@entry_id:137017)包含了散射过程的所有信息，它将一个给定的初态演化为所有可能的末态的线性叠加。

### [S矩阵](@entry_id:137017)的基本性质

[S矩阵](@entry_id:137017)的定义本身蕴含了它的一些普适性质，这些性质源于物理学的[基本对称性](@entry_id:161256)。

#### [幺正性](@entry_id:138773)与几率守恒

如果总[哈密顿量](@entry_id:172864) $H$ 是厄米的（对应于一个孤立系统），那么[时间演化算符](@entry_id:196774) $U(t)$ 就是幺正的。对于渐近完备的短程势，可以证明[S矩阵](@entry_id:137017)也是幺正的：$S^\dagger S = I$ [@problem_id:2664490]。
$$
S^\dagger S = (\Omega^{(-)\dagger} \Omega^{(+)})^\dagger (\Omega^{(-)\dagger} \Omega^{(+)}) = \Omega^{(+)\dagger} \Omega^{(-)} \Omega^{(-)\dagger} \Omega^{(+)}
$$
由于 $\Omega^{(-)}\Omega^{(-)\dagger}$ 是到 $H$ 的[散射态](@entry_id:150968)[子空间](@entry_id:150286)上的投影算符 $P_{ac}(H)$，并且 $\Omega^{(+)}$ 的值域也在此空间内，因此 $P_{ac}(H)\Omega^{(+)} = \Omega^{(+)}$。于是：
$$
S^\dagger S = \Omega^{(+)\dagger} \Omega^{(+)} = I
$$
同理可证 $SS^\dagger = I$。S矩阵的幺正性是几率守恒在[散射理论](@entry_id:143476)中的直接体现：从一个归一化的初态出发，散射到所有可能的末态的总几率必须为1。

#### [能量守恒](@entry_id:140514)

S矩阵与自由[哈密顿量](@entry_id:172864) $H_0$ 对易，即 $[S, H_0] = 0$。这可以通过Møller算符的交织性质 $H\Omega^{(\pm)} = \Omega^{(\pm)}H_0$ 来证明 [@problem_id:2664490]。
$$
S H_0 = \Omega^{(-)\dagger} \Omega^{(+)} H_0 = \Omega^{(-)\dagger} (H \Omega^{(+)}) = (H_0 \Omega^{(-)\dagger}) \Omega^{(+)} = H_0 S
$$
这个[对易关系](@entry_id:136780)意味着，如果初态是 $H_0$ 的一个本征态，能量为 $E_i$，那么末态也必须是能量为 $E_i$ 的[态的叠加](@entry_id:273993)。在连续谱基底下，S矩阵的矩阵元 $S_{fi} = \langle f | S | i \rangle$ 必须包含一个[能量守恒](@entry_id:140514)的狄拉克 $\delta$ 函数：
$$
\langle \mathbf{k}_f | S | \mathbf{k}_i \rangle \propto \delta(E_f - E_i)
$$
这表明在散射过程中，渐近初态和末态的总能量是严格相等的。

#### [时间反演不变性](@entry_id:152159)与[细致平衡原理](@entry_id:200508)

如果系统的动力学在[时间反演](@entry_id:182076)下保持不变，那么S矩阵将满足一个由时间反演算符 $\mathcal{T}$ 决定的对称性关系。对于自旋不为零的粒子，$\mathcal{T}$ 是一个[反幺正算符](@entry_id:197532)。[时间反演不变性](@entry_id:152159)意味着从初态 $|i\rangle$ 到末态 $|f\rangle$ 的跃迁振幅，与从[时间反演](@entry_id:182076)后的末态 $|\mathcal{T}f\rangle$ 到时间反演后的初态 $|\mathcal{T}i\rangle$ 的跃迁振幅大小相等：
$$
|S_{fi}| = |S_{\mathcal{T}i, \mathcal{T}f}|
$$
对于简单的情形（例如自旋为零），这可以简化为 $S_{fi} = S_{if}$。这一性质导致了所谓的**[细致平衡原理](@entry_id:200508)**（Principle of Detailed Balance）[@problem_id:1194523]。该原理指出，一个反应 $A+B \to C+D$ 的正向过程[截面](@entry_id:154995)与它的逆过程 $C+D \to A+B$ 的[截面](@entry_id:154995)之间存在一个简单的关系。对于非极化[截面](@entry_id:154995)，在相同的总[质心能量](@entry_id:265852)下，这个关系是：
$$
\frac{(d\sigma/d\Omega)_{A+B \to C+D}}{(d\sigma/d\Omega)_{C+D \to A+B}} = \frac{(2s_C+1)(2s_D+1)}{(2s_A+1)(2s_B+1)} \left(\frac{p_f}{p_i}\right)^2
$$
其中 $p_i, p_f$ 分别是初态和末态的[质心动量](@entry_id:171180)大小，$s_A, s_B, s_C, s_D$ 是各粒子的自旋。这个关系式在核物理和粒子物理中有重要的应用，它允许我们通过测量一个方向的[反应截面](@entry_id:191218)来推断逆反应的[截面](@entry_id:154995)。

### [T矩阵](@entry_id:145367)与K矩阵

[S矩阵](@entry_id:137017)描述了从初态到末态的整个跃迁，它包含了未发生散射的部分（由单位算符 $I$ 表示）和发生了散射的部分。为了分离出真正由相互作用引起的散射，我们定义了**跃迁矩阵**（T-matrix）。在能量壳上（即[能量守恒](@entry_id:140514)的态之间），它们的关系通常写作：
$$
\mathbf{S} = \mathbf{I} - 2\pi i \mathbf{T}
$$
其中 $\mathbf{S}$ 和 $\mathbf{T}$ 都是作用在能量为 $E$ 的定能[子空间](@entry_id:150286)上的算符。[T矩阵](@entry_id:145367)的[矩阵元](@entry_id:186505)直接与散射振幅成正比，因此它是一个核心的计算对象。

S矩阵的[幺正性](@entry_id:138773)给[T矩阵](@entry_id:145367)施加了一个[非线性](@entry_id:637147)的约束：
$$
\mathbf{S}^\dagger \mathbf{S} = (\mathbf{I} + 2\pi i \mathbf{T}^\dagger)(\mathbf{I} - 2\pi i \mathbf{T}) = \mathbf{I} \implies \mathbf{T} - \mathbf{T}^\dagger = -2\pi i \mathbf{T}^\dagger \mathbf{T}
$$
这个关系式被称为广义[光学定理](@entry_id:140058)。

在某些计算中，处理厄米算符比处理幺正算符更方便。为此，我们引入**反应矩阵**（K-matrix），它通过[Cayley变换](@entry_id:167155)与[S矩阵](@entry_id:137017)相关联。一个常见的定义是 [@problem_id:1194452]：
$$
\mathbf{S} = (\mathbf{I} + i\pi \mathbf{K})^{-1} (\mathbf{I} - i\pi \mathbf{K})
$$
这个定义的美妙之处在于，如果[S矩阵](@entry_id:137017)是幺正的，那么K矩阵就是厄米的（$\mathbf{K}^\dagger = \mathbf{K}$）。这使得在参数化[散射振幅](@entry_id:155369)时，只需使用实数参数，大大简化了问题。

我们可以推导[T矩阵](@entry_id:145367)和K矩阵之间的关系 [@problem_id:1194452]。将两个[S矩阵](@entry_id:137017)的表达式相等，经过一番代数运算，可以得到一个类似于[Lippmann-Schwinger方程](@entry_id:142814)的方程，称为Heitler方程：
$$
\mathbf{T} = \mathbf{K} - i\pi \mathbf{K} \mathbf{T}
$$
这个方程可以形式上求解为：
$$
\mathbf{T} = (\mathbf{I} + i\pi \mathbf{K})^{-1} \mathbf{K}
$$
这个关系式在实际计算中非常有用，例如，如果可以通过某种模型计算出厄米的K矩阵，就可以通过这个公式得到具有正确幺正性的[T矩阵](@entry_id:145367)，进而得到所有可观测的散射量。

### 分波分析

当散射势 $V(r)$ 是球对称时，角动量是守恒量。这使得我们可以将复杂的散射[问题分解](@entry_id:272624)为一系列独立的、针对每个角动量 $l$ 的一维问题。这个方法被称为**分波分析**。

#### 相位移与分波振幅

在分波分析中，散射[波函数](@entry_id:147440)被展开为[球谐函数](@entry_id:178380)的级数：
$$
\psi(\mathbf{r}) = \sum_{l=0}^\infty A_l R_{l}(r) P_l(\cos\theta)
$$
其中 $R_l(r)$ 是[径向波函数](@entry_id:266233)，它满足相应的[径向薛定谔方程](@entry_id:148306)。在没有势的区域（$r \to \infty$），$R_l(r)$ 的行为像[自由粒子](@entry_id:148748)的[径向波函数](@entry_id:266233)，但会有一个相位差。这个由相互作用势引起的相位差被称为**相位移** $\delta_l$。渐近地，
$$
R_l(r) \sim \frac{1}{kr} \sin\left(kr - \frac{l\pi}{2} + \delta_l\right)
$$
没有势时 $\delta_l=0$。因此，$\delta_l$ 包含了势对角动量为 $l$ 的分波的全部影响。

对于每个分波 $l$，由于几率守恒，入射的[球面波](@entry_id:200471)和出射的[球面波](@entry_id:200471)振幅大小必须相等，只能有一个相位差。这反映在[S矩阵](@entry_id:137017)上，就是在角[动量表象](@entry_id:156131)中，S矩阵是对角的，其对角元 $S_l$ 是模为1的复数 [@problem_id:2664486]：
$$
S_l = e^{2i\delta_l}
$$
这个关系将形式化的S矩阵元与直观的相位移联系起来。

通过将散射[波函数](@entry_id:147440)的渐近形式 $e^{ikz} + f(\theta)e^{ikr}/r$ 也按[分波展开](@entry_id:158933)，并与上述含有相位移的[径向波函数](@entry_id:266233)表达式进行匹配，我们可以推导出[散射振幅](@entry_id:155369) $f(\theta)$ 的[分波展开](@entry_id:158933)式 [@problem_id:2664468], [@problem_id:2664486]：
$$
f(\theta) = \sum_{l=0}^\infty (2l+1) f_l(k) P_l(\cos\theta)
$$
其中**分波振幅** $f_l(k)$ 为：
$$
f_l(k) = \frac{S_l - 1}{2ik} = \frac{e^{2i\delta_l} - 1}{2ik} = \frac{e^{i\delta_l}\sin\delta_l}{k}
$$
于是，完整的散射振幅可以表示为：
$$
f(\theta) = \frac{1}{k} \sum_{l=0}^\infty (2l+1) e^{i\delta_l} \sin\delta_l P_l(\cos\theta)
$$

#### 分波[截面](@entry_id:154995)与[光学定理](@entry_id:140058)

将[分波展开](@entry_id:158933)式代入[总截面](@entry_id:151809)的积分公式 $\sigma_{tot} = \int |f(\theta)|^2 d\Omega$，并利用[勒让德多项式的正交性](@entry_id:264861)，可以得到[总截面](@entry_id:151809)也分解为各分波贡献之和 $\sigma_{tot} = \sum_l \sigma_l$。其中**分波[截面](@entry_id:154995)** $\sigma_l$ 为 [@problem_id:2664486]：
$$
\sigma_l = \frac{4\pi}{k^2} (2l+1) \sin^2\delta_l
$$
这个公式揭示了每个分波对[总截面](@entry_id:151809)的贡献由其相位移决定。当 $\delta_l = (n+1/2)\pi$ 时，该分波的贡献达到最大值，称为幺正极限或共振。

利用[分波展开](@entry_id:158933)，我们还能优雅地证明**[光学定理](@entry_id:140058)**。该定理将总截面与[前向散射振幅](@entry_id:154109)（$\theta=0$）的虚部联系起来。由于 $P_l(\cos 0) = P_l(1) = 1$，[前向散射振幅](@entry_id:154109)为：
$$
f(0) = \frac{1}{k} \sum_{l=0}^\infty (2l+1) (\cos\delta_l + i\sin\delta_l)\sin\delta_l
$$
取其虚部：
$$
\text{Im}[f(0)] = \frac{1}{k} \sum_{l=0}^\infty (2l+1) \sin^2\delta_l
$$
比较[总截面](@entry_id:151809)的表达式 $\sigma_{tot} = \sum_l \sigma_l = \frac{4\pi}{k^2} \sum_l (2l+1)\sin^2\delta_l$，我们立即得到[光学定理](@entry_id:140058) [@problem_id:2664486]：
$$
\sigma_{tot} = \frac{4\pi}{k} \text{Im}[f(0)]
$$
这个定理是幺正性的直接结果，具有深刻的物理意义：散射体从入射束中移除了粒子（既通过[弹性散射](@entry_id:152152)也通过非弹性过程），这种“损失”表现为对[前向传播](@entry_id:193086)波的干涉相消，而干涉效应的大小正比于总截面。

#### [低能散射](@entry_id:156179)与散射长度

在低能极限下（$k \to 0$），对于短程势，角动量为 $l>0$ 的粒子由于受到离心势垒 $\frac{\hbar^2 l(l+1)}{2mr^2}$ 的阻碍，很难接近散射中心。因此，散射主要由 $l=0$ 的s波主导。对于s波，其低能行为可以用一个重要的参数——**[散射长度](@entry_id:142881)** $a_s$ 来描述。相位移在低能下的展开为 [@problem_id:2664486]：
$$
k \cot\delta_0 \approx -\frac{1}{a_s}
$$
当 $k \to 0$ 时，$\delta_0$ 也很小，$\cot\delta_0 \approx 1/\delta_0$，因此我们得到一个非常重要的关系：
$$
\delta_0(k) \approx -k a_s
$$
[散射长度](@entry_id:142881) $a_s$ 的物理意义是：它是低能下[径向波函数](@entry_id:266233)与 $r$ 轴的交点。$a_s$ 的正负和大小反映了势在低能下的性质（是等效吸引还是排斥，以及强度）。在 $k \to 0$ 极限下，[总截面](@entry_id:151809)趋于一个常数：
$$
\sigma_{tot} \approx \sigma_0 = \frac{4\pi}{k^2}\sin^2\delta_0 \approx \frac{4\pi}{k^2}(-ka_s)^2 = 4\pi a_s^2
$$

#### 应用实例：[玻恩近似](@entry_id:138141)

当散射势很弱时，我们可以使用**[玻恩近似](@entry_id:138141)**来计算散射振幅。[一阶玻恩近似](@entry_id:201729)给出：
$$
f_B(\mathbf{q}) = -\frac{m}{2\pi\hbar^2} \int d^3r' V(\mathbf{r}') e^{-i\mathbf{q}\cdot\mathbf{r}'}
$$
其中 $\mathbf{q} = \mathbf{k}' - \mathbf{k}$ 是动量转移。这个结果可以和分波分析结合。例如，对于[汤川势](@entry_id:139645) $V(r) = V_0 e^{-\mu r}/r$，其[傅里叶变换](@entry_id:142120)是 $\tilde{V}(q) = 4\pi V_0 / (q^2+\mu^2)$。通过将玻恩振幅按勒让德多项式投影，可以得到各阶分波振幅的近似值。对于s波，在弱势（小相位移）情况下 $\delta_0 \approx k f_0$，我们可以得到s波相位移的近似表达式 [@problem_id:1194436]：
$$
\delta_0(k) \approx -\frac{mV_0}{2\hbar^2 k} \ln\left(1+\frac{4k^2}{\mu^2}\right)
$$
这提供了一个从给定的势函数直接计算散射相位移的具体例子。

### 非弹性散射

当散射过程的能量足够高，使得粒子可能发生内部状态的改变，或者转变为其他种类的粒子时，我们就进入了**[非弹性散射](@entry_id:138624)**的领域。在这种情况下，存在多个可能的出射“通道”。

对于一个多通道系统，S矩阵和[T矩阵](@entry_id:145367)都成为真正的矩阵，其下标表示不同的通道。例如，一个两通道体系的S矩阵是一个 $2 \times 2$ 矩阵：
$$
S = \begin{pmatrix} S_{11}  S_{12} \\ S_{21}  S_{22} \end{pmatrix}
$$
其中 $S_{11}$ 描述弹性散射（$1 \to 1$），而 $S_{12}$ 描述非弹性散射（$1 \to 2$）。

[幺正性](@entry_id:138773)条件 $S^\dagger S=I$ 依然成立，但现在它联系着所有通道。例如，其第一列表明：
$$
|S_{11}|^2 + |S_{21}|^2 = 1
$$
这意味着从通道1入射的粒子，一部分保持在通道1（弹性散射），另一部分跃迁到通道2（[非弹性散射](@entry_id:138624)），总几率守恒。如果存在非弹性过程（$S_{21} \neq 0$），那么弹性散射的几率必须小于1，即 $|S_{11}|^2  1$。对于分波 $l$，我们定义**非弹性参数** $\eta_l = |S_{11}^{(l)}|$，它取值在0和1之间，量度了弹性通道的几率保持程度 [@problem_id:1194458]。

在这种情况下，[光学定理](@entry_id:140058)需要被推广。它依然将前向[弹性散射](@entry_id:152152)振幅的虚部与总截面联系起来，但这里的**总截面** $\sigma_{tot}$ 是从初始通道出发的所有可能过程的[截面](@entry_id:154995)之和，包括[弹性散射](@entry_id:152152)[截面](@entry_id:154995) $\sigma_{el}$ 和所有非弹性（或称反应）[截面](@entry_id:154995) $\sigma_{re}$ [@problem_id:1194513]。对于从通道1出发的散射，广义[光学定理](@entry_id:140058)的形式为：
$$
\sigma_{tot}^{(1)} = \sigma_{el}^{(1 \to 1)} + \sigma_{re}^{(1 \to 2)} + \dots = \frac{4\pi}{k_1} \text{Im}[f_{11}(0)]
$$
其中 $k_1$ 是入射通道的[波数](@entry_id:172452)，$f_{11}(0)$ 是前向弹性散射振幅。这个定理再次强调了[幺正性](@entry_id:138773)的强大威力，它将一个纯粹弹性通道的量（前向振幅）与所有通道的总效应（总截面）联系在了一起。

### [S矩阵](@entry_id:137017)的[解析性](@entry_id:140716)质

[S矩阵理论](@entry_id:138072)最深刻和强大的方面在于，S矩阵的[矩阵元](@entry_id:186505)（以及相关的[散射振幅](@entry_id:155369)）可以被看作是能量或动量等运动学变量的解析函数。这些函数在复平面上的奇异性结构（极点、[支点](@entry_id:166575)等）与物理过程直接对应。

#### [Green函数](@entry_id:147802)与[Lippmann-Schwinger方程](@entry_id:142814)

[散射振幅](@entry_id:155369)的解析性源于其动力学方程，即[Lippmann-Schwinger方程](@entry_id:142814)。以[T矩阵](@entry_id:145367)为例，它满足：
$$
T(E) = V + V G_0(E) T(E)
$$
这里的关键是自由[哈密顿量](@entry_id:172864)的[预解式](@entry_id:199555)，或称**Green函数**，$G_0(E) = (E - H_0)^{-1}$。在 $H_0$ 的[连续谱](@entry_id:155477)上，这个算符是奇异的。为了赋予它明确的定义，我们需要指定如何处理极点。这通过引入一个无穷小量 $i\epsilon$ 来实现，得到两种不同的Green函数 [@problem_id:2664416]：
$$
G_0^{(\pm)}(E) = \frac{1}{E - H_0 \pm i\epsilon}
$$
这个 $\pm i\epsilon$ 的规定不是数学上的投机，而是由**因果律**决定的。retarded Green函数 $G_0^{(+)}$ 对应于只在未来 ($t0$) 传播的信号，它在构造[散射态](@entry_id:150968)时给出了物理上正确的“出射波”边界条件。而 advanced [Green函数](@entry_id:147802) $G_0^{(-)}$ 对应于只在过去 ($t0$) 传播的信号，它用于构造具有“入射波”边界条件的态。[Sokhotski-Plemelj定理](@entry_id:167505)告诉我们这个无穷小量的作用：
$$
\frac{1}{x \pm i\epsilon} = \mathcal{P}\left(\frac{1}{x}\right) \mp i\pi \delta(x)
$$
其中 $\mathcal{P}$ 表示[柯西主值](@entry_id:192761)。$i\epsilon$ 的规定决定了在能量壳上的散射波如何传播。

#### 在壳与离壳[矩阵元](@entry_id:186505)

[能量守恒](@entry_id:140514)条件 $E_f = E_i$ 定义了一个[曲面](@entry_id:267450)，称为**能量壳**（energy shell）。物理上可观测的散射过程，其初态和末态都必须在能量壳上。因此，如我们之前所见，只有[T矩阵](@entry_id:145367)的**在壳**（on-shell）[矩阵元](@entry_id:186505) $\langle \mathbf{k}_f | T(E) | \mathbf{k}_i \rangle$（其中 $|\mathbf{k}_f|=|\mathbf{k}_i|$）直接贡献给可观测的[截面](@entry_id:154995) [@problem_id:2664412]。

然而，在计算在壳[T矩阵](@entry_id:145367)元的[Lippmann-Schwinger方程](@entry_id:142814)中，例如在[玻恩级数](@entry_id:195385)展开 $T = V + V G_0 V + \dots$ 中，我们需要对所有中间态求和（或积分）。这些中间态的能量通常不等于初末态能量，它们被称为**离壳**（off-shell）的。这些离壳的“虚过程”虽然不能被直接观测，但它们是构建物理（在壳）[散射振幅](@entry_id:155369)所必需的数学构件。一个重要的推论是，可能存在不同的势函数，它们有不同的离壳行为，但产生完全相同的在壳[S矩阵](@entry_id:137017)。这样的势被称为“相移等效势”，它们无法通过两体[散射实验](@entry_id:173304)来区分。

#### 奇异性及其物理意义

将[散射振幅](@entry_id:155369) $f_l(s)$（其中 $s=k^2$ 是能量变量）看作复变量 $s$ 的函数，其[奇异点](@entry_id:199525)蕴含着丰富的物理信息。

*   **极点 (Poles)**：如果分波S矩阵 $S_l(k)$ 在[复动量](@entry_id:201607) $k$ 平面的正虚轴上有一个极点，即 $k = i\kappa$ ($\kappa  0$)，那么这个极点对应一个束缚态 [@problem_id:2140289]。此时能量为 $E = \frac{\hbar^2 k^2}{2m} = -\frac{\hbar^2 \kappa^2}{2m}$，是一个负实数。对应的[波函数](@entry_id:147440)在空间中呈指数衰减 $e^{-\kappa r}$，是可归一化的束缚态[波函数](@entry_id:147440)。如果极点出现在下半复平面 $k = k_R - i\Gamma$ ($\Gamma0$)，它对应一个**共振态**，能量为复数 $E_R - i\Gamma_E/2$。其实部 $E_R$ 是[共振能量](@entry_id:147349)，虚部 $\Gamma_E$ 是[共振宽度](@entry_id:186927)，与共振态的寿命 $\tau = \hbar/\Gamma_E$ 成反比。

*   **[支点](@entry_id:166575)与[割线](@entry_id:178768) (Branch Points and Cuts)**：[散射振幅](@entry_id:155369)还具有[支点](@entry_id:166575)和相应的割线。沿着正实 $s$ 轴（物理区域）的割线称为**幺正割线**或右侧[割线](@entry_id:178768)，它源于S矩阵的幺正性。沿着负实 $s$ 轴的[割线](@entry_id:178768)称为**力学割线**或左侧[割线](@entry_id:178768)，它反映了[散射力](@entry_id:159368)的具体性质。例如，对于[汤川势](@entry_id:139645) $V(r) \propto e^{-\mu r}/r$，其力程有限但呈指数衰减。这种势可以看作是交换了一个质量为 $\mu$ 的粒子。这种交换过程在散射振幅中体现为一个从 $s = -\mu^2/4$ 开始沿负实轴延伸的[割线](@entry_id:178768) [@problem_id:1194567]。更复杂的交换过程（例如所谓的“[反常阈](@entry_id:194503)”现象 [@problem_id:1194434]）会导致更复杂的[奇异结构](@entry_id:260616)，但原理是相同的：[解析函数](@entry_id:139584)的奇异性编码了物理过程。

#### [Levinson定理](@entry_id:146309)

解析性理论的一个优美结果是**[Levinson定理](@entry_id:146309)**。它将一个纯粹的散射量（零能相位移）与一个谱信息（束缚态数目）联系起来。对于角动量为 $l$ 的分波，该定理表述为 [@problem_id:1194486]：
$$
\delta_l(0) - \delta_l(\infty) = n_l \pi
$$
其中 $n_l$ 是角动量为 $l$ 的束缚态的数目。按照惯例，我们取 $\delta_l(\infty)=0$（在无穷高能量下粒子穿透势场，不受影响），于是定理简化为：
$$
\delta_l(0) = n_l \pi
$$
这个定理意味着，零能相位移是量子化的！每当势的强度增加到足以束缚一个新的 $l$-波束缚态时，$\delta_l(0)$ 就会跳跃一个 $\pi$。例如，如果一个势被告知支持2个s波束缚态（$n_0=2$）和1个p波束缚态（$n_1=1$），那么我们可以立刻断定 $\delta_0(0) = 2\pi$ 且 $\delta_1(0) = \pi$ [@problem_id:1194486]。反之，通过实验测量不同能量下的相位移并外推到 $k=0$，我们就可以推断出该势中存在多少个束缚态 [@problem_id:894312]。

#### 色散关系与高能界

[散射振幅](@entry_id:155369)的解析性，结合[幺正性](@entry_id:138773)和多项式有界性（即振幅随能量的增长不能过快），允许我们写出所谓的**[色散关系](@entry_id:140395)**。这是一种积分关系，它将散射振幅的实部表示为其虚部在整个能量轴上的积分。这提供了一个强大的自洽性约束。

这些原理的另一个深刻推论是**Froissart-Martin界** [@problem_id:1194495]。它为[总截面](@entry_id:151809)在能量极高时的增长设定了一个严格的上限：
$$
\sigma_{tot}(s) \le \frac{\pi}{m_\pi^2} \ln^2(s/s_0)
$$
其中 $s$ 是[质心能量](@entry_id:265852)的平方，$m_\pi$ 是可交换的最轻粒子的质量，它决定了力程。这个对数平方的增长是[量子场论](@entry_id:138177)中允许的最快增长速度，它来源于解析性和[幺正性](@entry_id:138773)的共同约束。这一界限表明，尽管相互作用可能在能量升高时变得更强，但其总效应的增长受到了基本原理的严格限制。