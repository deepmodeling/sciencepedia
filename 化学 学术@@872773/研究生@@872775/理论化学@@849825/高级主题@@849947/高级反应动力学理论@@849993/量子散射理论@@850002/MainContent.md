## 引言
[量子散射](@entry_id:147453)理论是量子力学的基石之一，它为描述和理解粒子间的相互作用提供了核心语言和数学工具。从[原子核](@entry_id:167902)的碰撞、[化学反应](@entry_id:146973)的发生，到电子在固体材料中的输运，几乎所有涉及粒子间相互作用的微观过程的最终表现形式都是散射。该理论致力于回答一个根本性问题：给定粒子间的相互作用势，我们如何预测一次碰撞事件的结果？它构筑了从微观动力学定律到宏观实验[可观测量](@entry_id:267133)（如[反应速率](@entry_id:139813)和输运系数）之间的桥梁，是连接理论与实验不可或缺的一环。

本文旨在为读者系统地构建[量子散射](@entry_id:147453)理论的知识体系。我们将分三个章节展开：

第一章“原理与机制”，将深入探讨理论的核心，从[散射态](@entry_id:150968)、[散射振幅](@entry_id:155369)与[截面](@entry_id:154995)的定义出发，建立严谨的[李普曼-施温格方程](@entry_id:142814)和[S矩阵](@entry_id:137017)形式化理论。我们将阐明幺正性、[能量守恒](@entry_id:140514)等[基本对称性](@entry_id:161256)如何塑造散射过程，并介绍[玻恩近似](@entry_id:138141)与分波分析这两种关键的计算方法。

第二章“应用与跨学科关联”，将展示该理论的强大威力，探索其如何在[化学反应动力学](@entry_id:274455)、[超冷原子](@entry_id:137057)物理、凝聚态物理与[材料科学](@entry_id:152226)等前沿领域中，为解释复杂现象、调控量子系统以及设计新材料提供深刻的物理洞见。

最后，在“动手实践”部分，我们将通过一系列精心设计的计算问题，引导读者亲手应用所学知识，将抽象的理论公式转化为解决具体物理问题的能力，从而加深对核心概念的理解。

## 原理与机制

本章旨在深入探讨[量子散射](@entry_id:147453)理论的核心原理与基本机制。我们将从[散射态](@entry_id:150968)的数学描述出发，建立散射振幅与可观测[截面](@entry_id:154995)之间的联系，进而引入更为严谨的[李普曼-施温格方程](@entry_id:142814)和S矩阵形式化理论。在此基础上，我们将探讨该理论的几个基本支柱——[幺正性](@entry_id:138773)、[能量守恒](@entry_id:140514)和[时间反演对称性](@entry_id:138094)——以及它们对散射过程的深刻影响。最后，我们将介绍求解散射问题的两种关键方法（[玻恩近似](@entry_id:138141)和分波分析），并将其应用于描述真实[分子碰撞](@entry_id:137334)中至关重要的多通道散射与共振现象。

### [散射态](@entry_id:150968)与[散射振幅](@entry_id:155369)

[量子散射](@entry_id:147453)理论旨在描述一束入射粒子与一个靶相互作用后被散射的过程。在[稳态](@entry_id:182458)图像中，整个系统由一个单一的、覆盖全空间的**[定态](@entry_id:137260)散射[波函数](@entry_id:147440)** $\psi(\mathbf{r})$ 来描述。这个[波函数](@entry_id:147440)是含相互作用的全[哈密顿量](@entry_id:172864) $H = H_0 + V$ 的本征函数。对于短程势 $V(\mathbf{r})$（即当 $r \to \infty$ 时，势比 $1/r$ 更快趋于零），该[波函数](@entry_id:147440)在远离散射中心（$r \to \infty$）时必须满足一个特定的渐近边界条件：

$$
\psi(\mathbf{r}) \xrightarrow{r\to\infty} e^{i\mathbf{k} \cdot \mathbf{r}} + f(\mathbf{k}',\mathbf{k})\,\frac{e^{ikr}}{r}
$$

其中，入射波矢量为 $\mathbf{k}$，散射[波矢](@entry_id:178620)量为 $\mathbf{k}'$，且对于[弹性散射](@entry_id:152152)，它们的模相等，$|\mathbf{k}| = |\mathbf{k}'| = k$。为方便起见，通常将[坐标系](@entry_id:156346)的 $z$ 轴沿入射方向 $\mathbf{k}$ 对齐。此时，$\mathbf{k} \cdot \mathbf{r} = kz$，散射方向 $\mathbf{k}'$ 由球面坐标 $(\theta, \phi)$ 确定。于是，渐近形式可写为我们更熟悉的形式 [@problem_id:2798179] [@problem_id:2798196]：

$$
\psi(\mathbf{r}) \xrightarrow{r\to\infty} e^{ikz} + f(\theta,\phi)\,\frac{e^{ikr}}{r}
$$

这个表达式具有清晰的物理诠释。第一项 $e^{ikz}$ 代表沿 $+z$ 方向传播的**入射[平面波](@entry_id:189798)**，其振幅被约定俗成地归一化为1。第二项 $f(\theta,\phi)\,\frac{e^{ikr}}{r}$ 代表从散射中心向外传播的**[出射球面波](@entry_id:201591)**。因子 $1/r$ 描述了[球面波](@entry_id:200471)振幅随距离的减小，以保证总概率通量的守恒。而系数 $f(\theta,\phi)$ 则被称为**散射振幅**，它描述了散射到不同方向 $(\theta, \phi)$ 的波的振幅和相位，是[散射理论](@entry_id:143476)的核心物理量。值得注意的是，[散射振幅](@entry_id:155369)的量纲是长度（$L$），这使得其模方的量纲（$L^2$）恰好是面积。

这个渐近边界条件不仅定义了散射振幅，更重要的是，它从薛定谔方程的众多可能解中唯一地选择出了符合物理散射情景的解——即一个入射波和一个纯粹向外传播的散射波的叠加。

### [微分散射截面](@entry_id:172304)

散射振幅的物理意义通过**[微分截面](@entry_id:137333)**（differential cross section）$d\sigma/d\Omega$ 得以彰显。[微分截面](@entry_id:137333)的定义是单位时间内散射到单位[立体角](@entry_id:154756)内的粒子数与入射[粒子通量](@entry_id:753207)密度的比值。

首先，我们定义量子力学中的**[概率流密度](@entry_id:152013)** $\mathbf{j}$：

$$
\mathbf{j}(\mathbf{r})=\frac{\hbar}{2mi}\left[ \psi^*(\nabla\psi) - (\nabla\psi^*)\psi \right] = \frac{\hbar}{m}\text{Im}(\psi^*\nabla\psi)
$$

对于振幅为1的入射[平面波](@entry_id:189798) $\psi_{\mathrm{in}} = e^{ikz}$，其[概率流密度](@entry_id:152013)（即**入射通量**）为：

$$
\mathbf{j}_{\mathrm{in}} = \frac{\hbar}{m}\text{Im}(e^{-ikz} (ik\hat{\mathbf{z}}e^{ikz})) = \frac{\hbar k}{m}\hat{\mathbf{z}} = v\hat{\mathbf{z}}
$$

其大小 $j_{\mathrm{in}} = \hbar k/m$ 就是入射粒子的速度 $v$。

对于散射波部分 $\psi_{\mathrm{sc}} = f(\theta,\phi)\frac{e^{ikr}}{r}$，在 $r \to \infty$ 的极限下，梯度 $\nabla$ 主要作用于快速[振荡](@entry_id:267781)的指数项 $e^{ikr}$，即 $\nabla\psi_{\mathrm{sc}} \approx ik\psi_{\mathrm{sc}}\hat{\mathbf{r}}$。因此，散射[概率流密度](@entry_id:152013)近似为：

$$
\mathbf{j}_{\mathrm{sc}} \approx \frac{\hbar k}{m}|\psi_{\mathrm{sc}}|^2\hat{\mathbf{r}} = \frac{\hbar k}{m}\frac{|f(\theta,\phi)|^2}{r^2}\hat{\mathbf{r}}
$$

可以看到，散射[概率流](@entry_id:150949)的密度与 $r^{-2}$ 成正比。穿过一个位于远处、半径为 $r$ 的球面上一块[面积元](@entry_id:263205) $d\mathbf{A} = r^2 d\Omega\,\hat{\mathbf{r}}$ 的散射粒子数率为 $d\Phi_{\mathrm{sc}} = \mathbf{j}_{\mathrm{sc}} \cdot d\mathbf{A}$。因此，散射到[立体角](@entry_id:154756) $d\Omega$ 内的通量为：

$$
d\Phi_{\mathrm{sc}} = \left(\frac{\hbar k}{m}\frac{|f(\theta,\phi)|^2}{r^2}\right) (r^2 d\Omega) = \frac{\hbar k}{m}|f(\theta,\phi)|^2 d\Omega
$$

请注意，这里的 $r^2$ 因子被精确地抵消了，这意味着通过任何一个包围散射中心的大球面的总散射通量是一个与半径无关的常数，这正是[概率守恒](@entry_id:149166)的体现 [@problem_id:2798179]。

根据定义，[微分截面](@entry_id:137333)就是散射通量率除以入射通量密度：

$$
\frac{d\sigma}{d\Omega} = \frac{d\Phi_{\mathrm{sc}}/d\Omega}{j_{\mathrm{in}}} = \frac{(\hbar k/m)|f(\theta,\phi)|^2}{\hbar k/m}
$$

于是我们得到了[散射理论](@entry_id:143476)中最基本和最重要的关系之一 [@problem_id:2798179] [@problem_id:2798196]：

$$
\frac{d\sigma}{d\Omega} = |f(\theta,\phi)|^2
$$

这个公式表明，实验上可测量的[微分截面](@entry_id:137333)直接等于[散射振幅](@entry_id:155369)模的平方。因此，理论计算的目标就变成了求解[散射振幅](@entry_id:155369) $f(\theta,\phi)$。值得强调的是，尽管我们可以任意改变整个[波函数](@entry_id:147440) $\psi$ 的归一化常数，但这将同等比例地改变入射通量和散射通量，二者的比值（即[截面](@entry_id:154995)）保持不变。然而，[散射振幅](@entry_id:155369) $f$ 的具体数值是与单位振幅的入射平面波相关联的，上述边界条件的写法已经隐含了这一约定 [@problem_id:2798196]。

### [李普曼-施温格方程](@entry_id:142814)

为了从第一性原理出发求解散射振幅，我们需要一个比渐近形式更严谨的数学框架。这个框架由**[李普曼-施温格方程](@entry_id:142814)**（Lippmann-Schwinger equation）提供。

我们从[定态](@entry_id:137260)薛定谔方程 $(E - H_0 - V)|\psi\rangle = 0$ 出发，其中 $H_0$ 是自由粒子[哈密顿量](@entry_id:172864)，$V$ 是相互作用势。我们可以将其形式上改写为：

$$
(E - H_0)|\psi\rangle = V|\psi\rangle
$$

这个方程的通解是[齐次方程](@entry_id:163650) $(E-H_0)|\phi\rangle = 0$ 的解（即入射波 $|\phi\rangle$）与一个[特解](@entry_id:149080)的和。特解可以通过形式上地反演算符 $(E - H_0)$ 得到。然而，当能量 $E$ 处于 $H_0$ 的连续谱中时，算符 $(E - H_0)$ 是奇异的，其逆算符没有良好定义。为了解决这个问题，我们引入一个无穷小正数 $\epsilon$，并将能量替换为 $E \pm i\epsilon$，从而定义了**自由格林算符**（或称为**自由[预解式](@entry_id:199555)**）：

$$
G_0^\pm(E) = \frac{1}{E - H_0 \pm i\epsilon}
$$

这里的 $\epsilon \to 0^+$ 的极限是隐含的。这个小小的虚部 $i\epsilon$ 使得分母不再为零，从而使逆算符有了明确的数学意义。正负号的选择对应着不同的物理边界条件。由此，我们得到[李普曼-施温格方程](@entry_id:142814)的两种形式 [@problem_id:2798166]：

$$
|\psi_E^\pm\rangle = |\phi_E\rangle + G_0^\pm(E) V |\psi_E^\pm\rangle = |\phi_E\rangle + \frac{1}{E - H_0 \pm i\epsilon} V |\psi_E^\pm\rangle
$$

这里的 $|\psi_E^+\rangle$ 对应**出射波**（outgoing-wave）边界条件，而 $|\psi_E^-\rangle$ 对应**入射波**（incoming-wave）边界条件。在典型的[散射实验](@entry_id:173304)中，粒子从无穷远入射，散射后向无穷远传播出去，这对应着[出射波边界条件](@entry_id:753026)。因此，我们主要关心 $|\psi_E^+\rangle$ 解。

$i\epsilon$ 规则的物理内涵在格林算符的位置表象中最为清晰。通过[傅里叶变换](@entry_id:142120)和[留数定理](@entry_id:164878)可以证明，在三维空间中，对应出射波的[格林函数](@entry_id:147802) $G_0^{(+)}$ 的渐近形式为 [@problem_id:2798166] [@problem_id:2798179]：

$$
G_0^{(+)}(\mathbf{r}, \mathbf{r}') = \langle \mathbf{r} | G_0^+(E) | \mathbf{r}' \rangle \xrightarrow{|\mathbf{r}-\mathbf{r}'|\to\infty} -\frac{m}{2\pi\hbar^2} \frac{e^{ik|\mathbf{r}-\mathbf{r}'|}}{|\mathbf{r}-\mathbf{r}'|}
$$

这个形式正比于 $e^{ikr}/r$，代表一个由[点源](@entry_id:196698) $\mathbf{r}'$ 发出的[球面波](@entry_id:200471)。因此，[李普曼-施温格方程](@entry_id:142814)中的 $+i\epsilon$ 规则，也被称为**[索末菲辐射条件](@entry_id:168772)**（Sommerfeld radiation condition），是确保散射[波函数](@entry_id:147440)具有正确的物理[渐近行为](@entry_id:160836)（即纯粹向外传播）的数学手段。

### S矩阵及其性质

虽然定态方法直观，但一个更强大和普适的理论框架是基于时间演化的**S矩阵**（Scattering matrix）理论。S矩阵描述了系统从遥远的过去（$t \to -\infty$）一个特定的入射渐近态，演化到遥远的未来（$t \to +\infty$）一个特定的出射渐近态的整个过程。

形式上，[S矩阵](@entry_id:137017)是通过**Møller波算符** $\Omega^{(\pm)}$ 定义的。Møller算符将 $t=\mp\infty$ 时的自由演化态（入射/出射态）映射到 $t=0$ 时的全[哈密顿量](@entry_id:172864)下的真实相互作用态：

$$
\Omega^{(\pm)} = \lim_{t \to \mp \infty} e^{iHt/\hbar} e^{-iH_0t/\hbar}
$$

一个从初态 $|\phi_{\mathrm{in}}\rangle$ 开始的散射过程，其在 $t=0$ 时的状态是 $|\Psi(0)\rangle = \Omega^{(+)} |\phi_{\mathrm{in}}\rangle$。这个状态将继续演化，并在 $t \to +\infty$ 时趋近于某个末态 $|\phi_{\mathrm{out}}\rangle$，两者之间的关系是 $|\Psi(0)\rangle = \Omega^{(-)} |\phi_{\mathrm{out}}\rangle$。联立这两个关系，我们得到 $|\phi_{\mathrm{out}}\rangle = (\Omega^{(-)})^{-1} \Omega^{(+)} |\phi_{\mathrm{in}}\rangle$。[S矩阵](@entry_id:137017)被定义为 [@problem_id:2664490]：

$$
S = (\Omega^{(-)})^\dagger \Omega^{(+)}
$$

因此，[S矩阵](@entry_id:137017)的作用就是将入射态直接映射到出射态：$|\phi_{\mathrm{out}}\rangle = S |\phi_{\mathrm{in}}\rangle$。如果入射态由一组系数 $a_{\mathrm{in}}(\mathbf{k}, \alpha)$ 描述，那么出射态的系数 $a_{\mathrm{out}}(\mathbf{k}', \alpha')$ 就由[S矩阵](@entry_id:137017)的[矩阵元](@entry_id:186505) $S_{\mathbf{k}'\alpha'; \mathbf{k}\alpha}$ 决定。

S矩阵的性质蕴含了散射过程最基本的物理定律。

#### [幺正性](@entry_id:138773)与[概率守恒](@entry_id:149166)

如果系统的总[哈密顿量](@entry_id:172864) $H$ 是厄米的，那么[时间演化算符](@entry_id:196774) $U(t) = e^{-iHt/\hbar}$ 是幺正的，这意味着总概率在演化过程中守恒。这一基本原理直接导致S矩阵也是**幺正**的，即 $S^\dagger S = S S^\dagger = \mathbb{I}$。

[幺正性](@entry_id:138773)的物理意义是总散射概率为1。考虑一个从初态 $|i\rangle$ 开始的散射，跃迁到任意末态 $|f\rangle$ 的概率是 $|S_{fi}|^2$。[幺正性](@entry_id:138773)条件 $(S^\dagger S)_{ii} = 1$ 展开后即为 [@problem_id:2916847]：

$$
\sum_f (S^\dagger)_{if} S_{fi} = \sum_f S_{fi}^* S_{fi} = \sum_f |S_{fi}|^2 = 1
$$

这表明，从一个给定的初态出发，散射到所有可能的末态的概率之和等于1。

[幺正性](@entry_id:138773)还导出了著名的**[光学定理](@entry_id:140058)**（Optical Theorem）。通常将S矩阵分解为未散射[部分和](@entry_id:162077)散射部分，定义**跃迁算符**（T-matrix）$T$ 使得 $S = \mathbb{I} - 2\pi i \delta(E_f - E_i) T$。在另一种约定下，$S=\mathbb{I}+iT$ (符号约定不同，但物理内容一致)。利用后一种约定，幺正性 $S^\dagger S = \mathbb{I}$ 意味着 $T - T^\dagger = i T^\dagger T$。这个算符方程的对角元给出了广义[光学定理](@entry_id:140058)，它将[前向散射振幅](@entry_id:154109)的虚部（与 $\text{Im}(T_{ii})$ 相关）与[总散射截面](@entry_id:168963)（与 $\sum_f |T_{fi}|^2$ 相关）联系起来，是[概率守恒](@entry_id:149166)的直接体现 [@problem_id:2916847]。

#### [能量守恒](@entry_id:140514)

如果[哈密顿量](@entry_id:172864)不显含时间，那么[能量守恒](@entry_id:140514)。在[S矩阵理论](@entry_id:138072)中，这表现为S矩阵与自由[哈密顿量](@entry_id:172864) $H_0$ 对易：$[S, H_0] = 0$。这意味着S矩阵的[矩阵元](@entry_id:186505)必须在能量上是对角的。对于连续谱，这意味着 [@problem_id:2664490]：

$$
S_{\beta\alpha} \propto \delta(E_\beta - E_\alpha)
$$

也就是说，只有当初始能量 $E_\alpha$ 和最终能量 $E_\beta$ 相等时，散射过程才可能发生。

#### 时间反演对称性

如果[哈密顿量](@entry_id:172864)在时间反演操作 $\mathcal{T}$ 下保持不变，即 $\mathcal{T}H\mathcal{T}^{-1} = H$，那么散射过程也应具有相应的对称性。时间反演算符 $\mathcal{T}$ 是一个[反幺正算符](@entry_id:197532)。这一对称性导致了[S矩阵](@entry_id:137017)的**互易性**（reciprocity）。其一般形式为：

$$
S_{\beta\alpha} = S_{\alpha_T\beta_T}
$$

其中 $|\alpha_T\rangle = \mathcal{T}|\alpha\rangle$ 是 $|\alpha\rangle$ 的[时间反演](@entry_id:182076)态。这个关系表明，从态 $\alpha$ 散射到态 $\beta$ 的过程，其S矩阵元等于其时间反演过程（即从 $\beta_T$ 散射到 $\alpha_T$）的S矩阵元。对于无自旋的粒子，[时间反演](@entry_id:182076)操作等效于反转运动方向，即 $\mathbf{k} \to -\mathbf{k}$。在特定基底下，这个关系可以简化为S矩阵的对称性 $S_{\beta\alpha} = S_{\alpha\beta}$ [@problem_id:2664446]。

然而，这种互易性并非总是成立。以下几种情况会破坏时间反演对称性，从而导致互易性失效：
1.  **外[磁场](@entry_id:153296)**：[磁场](@entry_id:153296) $\mathbf{B}$ 在时间反演下会反向，$\mathbf{B} \to -\mathbf{B}$。因此，在[磁场](@entry_id:153296)中 $H(\mathbf{B})$ 不满足[时间反演不变性](@entry_id:152159)，导致 $S_{\beta\alpha}(\mathbf{B}) = S_{\alpha_T\beta_T}(-\mathbf{B})$，而不是简单的互易关系。
2.  **非厄米[哈密顿量](@entry_id:172864)**：在某些模型中，为了描述粒子被吸收或损失到[模型空间](@entry_id:635763)之外的通道，会引入具有虚部的“[光学势](@entry_id:156352)”。这种非厄米[哈密顿量](@entry_id:172864)描述的是一个[开放系统](@entry_id:147845)，其演化不幺正，时间反演对称性被破坏。
3.  **特定的含时驱动**：一个[行波](@entry_id:185008)形式的含时势，如 $V(t) = V_0 \cos(\mathbf{q}\cdot\mathbf{r} - \omega t)$，虽然没有[磁场](@entry_id:153296)，但其本身具有[方向性](@entry_id:266095)，破坏了[时间反演对称性](@entry_id:138094)，因为 $H(t) \neq H(-t)$ [@problem_id:2664446]。

### 散射计算方法

#### [玻恩近似](@entry_id:138141)

对于弱相互作用或[高能散射](@entry_id:151941)，迭代求解[李普曼-施温格方程](@entry_id:142814)是一个有效的方法。**[玻恩近似](@entry_id:138141)**（Born approximation）是该迭代级数的第一项。它通过在积分方程的右端用未受扰的入射波 $e^{i\mathbf{k}\cdot\mathbf{r}'}$ 来近似真实的[波函数](@entry_id:147440) $\psi^{(+)}(\mathbf{r}')$ 得到。

通过这个近似，可以推导出[第一玻恩近似](@entry_id:201729)下的散射振幅为 [@problem_id:2798189]：

$$
f^{(1)}(\mathbf{k}',\mathbf{k}) = -\frac{\mu}{2\pi\hbar^2} \int d^3r' \, e^{-i\mathbf{k}'\cdot\mathbf{r}'} V(\mathbf{r}') e^{i\mathbf{k}\cdot\mathbf{r}'} = -\frac{\mu}{2\pi\hbar^2} \int d^3r' \, V(\mathbf{r}') e^{-i(\mathbf{k}'-\mathbf{k})\cdot\mathbf{r}'}
$$

令**动量转移** $\mathbf{q} = \mathbf{k}' - \mathbf{k}$，上式可以写为：

$$
f^{(1)}(\mathbf{q}) = -\frac{\mu}{2\pi\hbar^2} \tilde{V}(\mathbf{q})
$$

其中 $\tilde{V}(\mathbf{q})$ 是相互作用势 $V(\mathbf{r})$ 关于动量转移 $\mathbf{q}$ 的[傅里叶变换](@entry_id:142120)。这个简洁而优美的结果表明，在弱散射极限下，散射振幅直接正比于[势的傅里叶变换](@entry_id:149425)。

[玻恩近似](@entry_id:138141)的有效性取决于散射波相对于入射波是否是一个小扰动。这通常在两种情况下成立：(1) 势 $V$ 在整个作用范围内都足够“弱”；(2) 入射能量 $E$ 足够高，使得粒子穿过[势场](@entry_id:143025)的时间很短，受到的扰动很小。对于长程势，如库仑势 $V(r) \propto 1/r$，其[傅里叶变换](@entry_id:142120)发散，[玻恩近似](@entry_id:138141)的数学形式失效，需要采用更特殊的处理方法 [@problem_id:2798189] [@problem_id:2798196]。

#### 分波分析

对于球[对称势](@entry_id:148561) $V(r)$，由于[角动量守恒](@entry_id:156798)，问题可以大大简化。我们可以将入射平面波和散射[波函数](@entry_id:147440)都按照角动量[本征态](@entry_id:149904)（即[勒让德多项式](@entry_id:141510) $P_l(\cos\theta)$）展开，这个方法称为**分波分析**（partial wave analysis）。

入射[平面波](@entry_id:189798) $e^{ikz}$ 可以展开为无穷多个球面波的叠加：

$$
e^{ikz} = \sum_{l=0}^{\infty} i^l (2l+1) j_l(kr) P_l(\cos\theta)
$$

其中 $j_l(kr)$ 是[球贝塞尔函数](@entry_id:153247)。在散射势 $V(r)$ 的作用下，每一个角动量分量（称为一个“分波”）的[径向波函数](@entry_id:266233)会经历一个相位的变化，这个变化由**相移**（phase shift）$\delta_l$ 来描述。通过匹配总[波函数](@entry_id:147440)在 $r \to \infty$ 处的渐近形式与标准散射形式 $e^{ikz} + f(\theta)e^{ikr}/r$，可以推导出[散射振幅](@entry_id:155369)的[分波展开](@entry_id:158933)式 [@problem_id:2798199]：

$$
f(\theta) = \sum_{l=0}^{\infty} \frac{(2l+1)}{k} e^{i\delta_l} \sin\delta_l P_l(\cos\theta)
$$

这个表达式也可以写成等价形式：

$$
f(\theta) = \frac{1}{2ik} \sum_{l=0}^{\infty} (2l+1)(e^{2i\delta_l}-1)P_l(\cos\theta)
$$

这表明，对于[中心势](@entry_id:148563)场，我们只需要计算出一系列相移 $\delta_l$，就可以完全确定[散射振幅](@entry_id:155369)和[截面](@entry_id:154995)。

从[S矩阵](@entry_id:137017)的观点看，对于[中心势](@entry_id:148563)的[弹性散射](@entry_id:152152)，[S矩阵](@entry_id:137017)在分波表象中是对角的。其对角元 $S_l$ 与相移的关系是：

$$
S_l = e^{2i\delta_l}
$$

幺正性条件 $|S_l|^2 = 1$ 在这里自动满足，因为相移 $\delta_l$ 是实数。这个关系式将抽象的[S矩阵性质](@entry_id:196356)与一个具体的、可计算的物理量（相移）联系了起来。

### 多通道散射与共振

真实的原子分子碰撞往往更加复杂，因为碰撞伙伴可能处于不同的内部[量子态](@entry_id:146142)（如电子态、[振动](@entry_id:267781)或[转动态](@entry_id:158866)）。每个内部态都构成一个**散射通道**。

#### [耦合通道理论](@entry_id:747955)

在多通道问题中，我们需要求解一个耦合的[径向薛定谔方程](@entry_id:148306)组。例如，对于一个双通道问题，[径向波函数](@entry_id:266233)是一个二维矢量 $\mathbf{u}(r) = (u_1(r), u_2(r))^{\mathrm{T}}$，它满足如下形式的耦合方程 [@problem_id:2798206]：

$$
\begin{aligned}
\frac{d^2 u_1}{dr^2}+\left[k_1^2-\frac{l(l+1)}{r^2}-\frac{2\mu}{\hbar^2}U_1(r)\right]u_1(r) = \frac{2\mu}{\hbar^2}V_{12}(r)\,u_2(r) \\
\frac{d^2 u_2}{dr^2}+\left[k_2^2-\frac{l(l+1)}{r^2}-\frac{2\mu}{\hbar^2}U_2(r)\right]u_2(r) = \frac{2\mu}{\hbar^2}V_{12}(r)\,u_1(r)
\end{d}
$$

这里的 $U_i(r)$ 是第 $i$ 通道的势能，$V_{12}(r)$ 是通道间的耦合势。$k_i = \sqrt{2\mu(E-\varepsilon_i)}/\hbar$ 是第 $i$ 通道的[波数](@entry_id:172452)，其中 $\varepsilon_i$ 是该通道的能量阈值。

根据总能量 $E$ 与通道阈值 $\varepsilon_i$ 的关系，通道分为两类：
-   **开放通道**：$E > \varepsilon_i$，$k_i$ 为实数。粒子有足够的能量进入该通道并到达无穷远，[波函数](@entry_id:147440)在 $r \to \infty$ 时是[振荡](@entry_id:267781)的。
-   **关闭通道**：$E  \varepsilon_i$，$k_i$ 为纯虚数。粒子能量不足以进入该通道，[波函数](@entry_id:147440)在 $r \to \infty$ 时必须呈指数衰减，以保证物理上可接受。

S矩阵此时是一个 $N \times N$ 矩阵（$N$ 为开放通道数）。其[矩阵元](@entry_id:186505) $S_{ji}$ 描述了从入射通道 $i$ 散射到出射通道 $j$ 的振幅。对于弹性散射（$j=i$）和[非弹性散射](@entry_id:138624)（$j \neq i$），[幺正性](@entry_id:138773)条件 $\sum_j |S_{ji}|^2=1$ 依然成立。在分波表象中，对角元可以参数化为 $S_{l,aa} = \eta_l e^{2i\delta_l}$，其中 **非弹性参数** $\eta_l$ 满足 $0 \le \eta_l \le 1$。$\eta_l=1$ 意味着没有非弹性过程，而 $\eta_l  1$ 则表示有部分[概率流](@entry_id:150949)失到了其他非弹性或反应通道中 [@problem_id:2916847]。

#### [散射共振](@entry_id:149812)

在散射截面随能量变化的曲线上，我们常常会观察到一些尖锐的峰或谷结构，这些被称为**[散射共振](@entry_id:149812)**。共振的本质是系统形成了一个寿命有限的[准束缚态](@entry_id:144141)。主要有两种机制 [@problem_id:2798190]：

1.  **形态共振（Shape Resonance）**：这是一种单通道现象。对于 $l>0$ 的分波，其有效势 $V_{\mathrm{eff},l}(r) = V(r) + \frac{\hbar^2l(l+1)}{2\mu r^2}$ 可能由于吸引势 $V(r)$ 和排斥性[离心势](@entry_id:172447)的共同作用，形成一个势垒。当入射能量恰好与[势阱](@entry_id:151413)中某个准束缚能级相近时，粒子会被暂时囚禁在[势阱](@entry_id:151413)中，然后通过隧穿效应逃逸。
    *   **特征**：仅发生在 $l>0$ 的分波中；主要增强弹性散射[截面](@entry_id:154995)；其能量位置对外部[磁场](@entry_id:153296)等不敏感。

2.  **[费什巴赫共振](@entry_id:138465)（Feshbach Resonance）**：这是一种多通道现象。它发生在入射开放通道的能量与某个关闭通道中的一个真实束缚态能量发生简并时。通过通道间的耦合，系统可以从开放通道“借居”到关闭通道的束缚态中，形成一个长寿命的复合体，然后再衰变回开放通道。
    *   **特征**：本质是多[通道耦合](@entry_id:161648)效应；可以发生在任何分波（包括 $l=0$）；其能量位置对能够改变不同通道相对能量的外部场（如[磁场](@entry_id:153296)）极为敏感，因此是实验上实现量子调控的重要手段。

这两种共振机制虽然来源不同，但都极大地丰富了散射动力学，是理解和控制[化学反应](@entry_id:146973)、超[冷原子相互作用](@entry_id:162043)等前沿领域的关键。