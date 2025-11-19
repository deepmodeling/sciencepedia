## 引言
超[导电性](@entry_id:137481)，作为一种[宏观量子现象](@entry_id:144018)，自其发现以来一直吸引着物理学家的极大兴趣。然而，其微观机制在长达半个世纪的时间里都是一个未解之谜。本文旨在深入探讨解决这一谜题的核心理论——[库珀问题](@entry_id:161364)与BCS配对理论，它们共同揭示了[费米子](@entry_id:146235)体系在吸引相互作用下如何自发形成宏观相干态。通过学习本章，读者将系统地掌握从基本物理图像到[多体理论](@entry_id:169452)框架，再到实验验证和跨学科应用的完整知识体系。

为了实现这一目标，文章将分为三个核心部分。第一章**“原理与机制”**将从著名的[库珀问题](@entry_id:161364)入手，揭示费米海的不稳定性，并在此基础上构建完整的BCS[多体理论](@entry_id:169452)，详细阐述[BCS基态](@entry_id:136275)、[准粒子激发](@entry_id:138475)和超导能隙等核心概念。第二章**“应用与[交叉](@entry_id:147634)学科联系”**将展示[BCS理论](@entry_id:144185)的强大预测能力和普适性，探讨其在解释传统超导实验、理解杂质效应，以及在非常规超导和[冷原子](@entry_id:144092)物理等前沿领域的推广与应用。最后，**“动手实践”**部分将提供一系列计算练习，帮助读者亲手推导关键结果，从而将理论知识内化为解决实际问题的能力。

## 原理与机制

继前一章对[超导现象](@entry_id:142943)的宏观介绍之后，本章将深入探讨其微观理论基础。我们将从理解[费米子](@entry_id:146235)体系中吸引相互作用的基本不稳定性开始，即著名的[库珀问题](@entry_id:161364)，然后构建完整的巴丁-库珀-施里弗（Bardeen-Cooper-Schrieffer, BCS）[多体理论](@entry_id:169452)。本章的目标是系统地阐明[库珀对](@entry_id:143370)的形成、[BCS基态](@entry_id:136275)的性质、[准粒子激发](@entry_id:138475)谱以及超导态的一系列可观测物理特性。

### [库珀不稳定性](@entry_id:145007)：配对的前奏

在经典物理和单粒子量子力学中，一个微弱的吸引[势阱](@entry_id:151413)不一定能束缚一个粒子，尤其是在三维空间中，[势阱](@entry_id:151413)的强度和范围必须超过一个临界值。然而，在[费米子](@entry_id:146235)构成的多体系统中，情况发生了根本性的变化。1956年，Leon Cooper 提出了一个惊人的思想实验，揭示了在费米面附近，无论吸引相互作用多么微弱，都足以将两个[费米子](@entry_id:146235)束缚在一起形成一个“[库珀对](@entry_id:143370)”。这一发现是理解超导微观机制的基石。

[库珀问题](@entry_id:161364)的核心设定是：考虑一个在零温下的[费米气体](@entry_id:145305)，所有能量低于[费米能](@entry_id:143977) $E_F$ 的单粒子态都已被占据，形成一个“惰性”的[费米海](@entry_id:136725)。现在，将两个具有相反自旋和相反动量（[总动量](@entry_id:173071)为零）的[费米子](@entry_id:146235)置于费米海之上。由于[泡利不相容原理](@entry_id:141850)，这两个[费米子](@entry_id:146235)只能占据能量 $\epsilon_{\mathbf{k}}$ 大于 $E_F$ 的空态。假设这两个[费米子](@entry_id:146235)之间存在一种有效的吸引相互作用 $V_{\mathbf{k}, \mathbf{k'}}$。问题是，这个两粒子体系的总能量是否会低于它们在费米面上的能量之和 $2E_F$？如果低于，就意味着形成了一个束缚态。

为了求解这个束缚态的能量，我们可以在[动量表象](@entry_id:156131)中写出这两个[费米子](@entry_id:146235)的[定态](@entry_id:137260)薛定谔方程。对于一个总能量为 $E$ 的束缚态[波函数](@entry_id:147440) $|\psi\rangle = \sum_{|\mathbf{k}|>k_F} g_{\mathbf{k}} |\mathbf{k}\uparrow, -\mathbf{k}\downarrow\rangle$，其中 $|\mathbf{k}\uparrow, -\mathbf{k}\downarrow\rangle$ 表示两个[费米子](@entry_id:146235)分别占据动量为 $\mathbf{k}$ 和 $-\mathbf{k}$ 的态，可以推导出关于系数 $g_{\mathbf{k}}$ 的方程。在一个简化的模型中，吸引相互作用 $V_{\mathbf{k}, \mathbf{k'}}$ 在费米能之上一个很薄的能量壳层（宽度为 $\hbar\omega_c$）内是一个常数 $-v_0$（$v_0 > 0$），在此范围外为零。这导出了束缚态能量 $E$ 必须满足的[自洽方程](@entry_id:155949)：

$$
1 = v_0 \sum_{E_F  \epsilon_{\mathbf{k}}  E_F+\hbar\omega_c} \frac{1}{2\epsilon_{\mathbf{k}} - E}
$$

这里的关键在于将求和转化为对能量的积分。通过引入[费米面](@entry_id:137798)处的单自旋态密度 $N(\epsilon)$，求和可以近似为 $\int_{E_F}^{E_F+\hbar\omega_c} N(\epsilon) d\epsilon$。定义束缚能 $\Delta_B = 2E_F - E$，它表示将[库珀对](@entry_id:143370)拆散成两个位于费米面的非[相互作用费米子](@entry_id:160994)所需的能量。那么，方程中的分母变为 $2\epsilon - E = 2(\epsilon - E_F) + 2E_F - E = 2\xi + \Delta_B$，其中 $\xi = \epsilon - E_F$ 是相对于[费米能](@entry_id:143977)的能量。[自洽方程](@entry_id:155949)变为：

$$
1 \approx v_0 \int_{0}^{\hbar\omega_c} \frac{N(E_F+\xi)}{2\xi + \Delta_B} d\xi
$$

在通常的三维情况下，$N(\epsilon)$ 在费米面附近可以近似为常数 $N(0)$。积分后可以得到 $\Delta_B \approx 2\hbar\omega_c \exp(-2/(v_0 N(0)))$。这个结果揭示了两个核心特征：
1.  **束缚态的存在性**：对于任何大于零的吸引相互作用 $v_0$，总能找到一个正的束缚能 $\Delta_B$ 的解。这说明费米海的存在从根本上改变了束缚的条件，使其对微弱吸引变得不稳定。
2.  **非微扰性质**：束缚能与[相互作用强度](@entry_id:192243) $v_0$ 之间是指数关系，而不是简单的幂次关系。在[弱耦合](@entry_id:140994)极限下（即 $v_0 N(0) \ll 1$），束缚能非常小。这解释了为什么在超导理论出现之前，人们很难从微扰论的角度理解这种[配对机制](@entry_id:145844)。

以二维费米气体为例，其态密度 $N_{2D}$ 是一个与能量无关的常数。这种简化的模型可以精确求解。通过定义无量纲[耦合常数](@entry_id:747980) $\lambda = v_0 N_{2D}$，可以精确地解出束缚能 [@problem_id:1271941]：

$$
\Delta_B = \frac{2\hbar\omega_c}{\exp(2/\lambda) - 1}
$$

在弱耦合极限 $\lambda \to 0$ 时，该表达式也趋向于 $2\hbar\omega_c \exp(-2/\lambda)$，与三维情况下的结果形式一致。[库珀问题](@entry_id:161364)清晰地表明，一个正常的费米海在存在任意弱的吸引相互作用时是不稳定的，它倾向于形成由[费米子配对](@entry_id:158762)构成的能量更低的新[基态](@entry_id:150928)。

### [BCS基态](@entry_id:136275)：库珀对的相干凝聚

[库珀问题](@entry_id:161364)只解决了两个[费米子](@entry_id:146235)在惰性[费米海](@entry_id:136725)背景下的配对问题。一个真正的多体系统包含大量的[费米子](@entry_id:146235)，它们都可以参与配对。[BCS理论](@entry_id:144185)通过一个精妙的[变分波函数](@entry_id:144043)描述了由大量[库珀对](@entry_id:143370)构成的宏观量子基态。

[BCS基态](@entry_id:136275)[波函数](@entry_id:147440) $|\Psi_{BCS}\rangle$ 被构造为所有动量相反、自旋相反的[费米子](@entry_id:146235)对 $(\mathbf{k}\uparrow, -\mathbf{k}\downarrow)$ 的状态的乘积 [@problem_id:1272005] [@problem_id:1271937]：

$$
|\Psi_{BCS}\rangle = \prod_{\mathbf{k}} (u_k + v_k c^\dagger_{\mathbf{k}\uparrow} c^\dagger_{-\mathbf{k}\downarrow}) |0\rangle
$$

这里，$|0\rangle$ 是[费米子](@entry_id:146235)真空态，$c^\dagger_{\mathbf{k}\sigma}$ 是产生一个动量为 $\mathbf{k}$、自旋为 $\sigma$ 的[费米子](@entry_id:146235)的[产生算符](@entry_id:191512)。系数 $u_k$ 和 $v_k$ 是实数，且满足[归一化条件](@entry_id:156486) $u_k^2 + v_k^2 = 1$。

这个[波函数](@entry_id:147440)的物理意义极为深刻：
-   $v_k^2$ 代表了动量对态 $(\mathbf{k}\uparrow, -\mathbf{k}\downarrow)$ 被占据的概率。
-   $u_k^2$ 代表了该对态为空的概率。
-   整个[基态](@entry_id:150928)是不同数目的库珀对的相干叠加。它不是一个[粒子数算符](@entry_id:153568) $\hat{N}$ 的[本征态](@entry_id:149904)，这意味着[BCS基态](@entry_id:136275)中的粒子数是不确定的。

粒子数的不确定性是BCS理论采用大[正则系综](@entry_id:142391)处理的直接体现，也是其成功的关键之一。我们可以直接计算总粒子数在[BCS基态](@entry_id:136275)中的涨落（[方差](@entry_id:200758)）来量化这一点。一个动量对 $\mathbf{k}$ 的[粒子数算符](@entry_id:153568)为 $\hat{n}_{\mathbf{k}} = c_{\mathbf{k}\uparrow}^\dagger c_{\mathbf{k}\uparrow} + c_{-\mathbf{k}\downarrow}^\dagger c_{-\mathbf{k}\downarrow}$。在该对态的[子空间](@entry_id:150286)中，粒子数为0的概率是 $u_k^2$，粒子数为2的概率是 $v_k^2$。因此，该对态的[平均粒子数](@entry_id:151202)为 $\langle \hat{n}_{\mathbf{k}} \rangle = 2v_k^2$，而粒子数的平方平均为 $\langle \hat{n}_{\mathbf{k}}^2 \rangle = 4v_k^2$。其[方差](@entry_id:200758)为 $\langle (\Delta \hat{n}_{\mathbf{k}})^2 \rangle = \langle \hat{n}_{\mathbf{k}}^2 \rangle - \langle \hat{n}_{\mathbf{k}} \rangle^2 = 4v_k^2 - 4v_k^4 = 4u_k^2 v_k^2$。

由于不同动量对之间的状态是独立的，总粒子数的[方差](@entry_id:200758)就是所有对的[方差](@entry_id:200758)之和 [@problem_id:1271937]：

$$
\langle (\Delta \hat{N})^2 \rangle = \sum_{\mathbf{k}} \langle (\Delta \hat{n}_{\mathbf{k}})^2 \rangle = \sum_{\mathbf{k}} 4u_k^2v_k^2
$$

这个结果明确显示，只要存在某些 $k$ 值使得 $u_k$ 和 $v_k$ 都不为零（这正是BCS态的核心特征），总粒子数的涨落就不为零。

### 自洽[能隙方程](@entry_id:141924)与[准粒子激发](@entry_id:138475)

[BCS理论](@entry_id:144185)的核心成果之一是预言了在单粒子激发谱中存在一个能量间隔，即**超导能隙** $\Delta$。这个[能隙](@entry_id:191975)同时也是理论中的[序参量](@entry_id:144819)。$u_k$ 和 $v_k$ 的具体形式，以及[能隙](@entry_id:191975) $\Delta$ 的大小，是通过最小化系统总能量得到的。这一过程最终导出了一个关于 $\Delta$ 的[自洽方程](@entry_id:155949)。

在零温下，[BCS能隙方程](@entry_id:184182)的形式如下 [@problem_id:1272047]：

$$
1 = \frac{V}{2} \sum_{\mathbf{k}}' \frac{1}{\sqrt{\xi_{\mathbf{k}}^2 + \Delta_0^2}}
$$

其中，$V$ 是有效吸引相互作用强度，$\Delta_0$ 是零温[能隙](@entry_id:191975)，$\xi_{\mathbf{k}} = \epsilon_{\mathbf{k}} - E_F$ 是[单粒子能量](@entry_id:160812)相对于费米能的能量。带撇号的求和表示仅对[费米面](@entry_id:137798)附近一个能量壳层（通常由德拜能量 $\hbar\omega_D$ 决定，即 $|\xi_{\mathbf{k}}|  \hbar\omega_D$）内的动量态进行。

为了求解这个方程，我们再次将求和转化为积分，并假设在能量壳层内态密度为常数 $N(0)$。利用被积函数是 $\xi_{\mathbf{k}}$ 的偶函数，积分范围可以从 $[-\hbar\omega_D, \hbar\omega_D]$ 折半为 $[0, \hbar\omega_D]$ 并乘以2。方程变为：

$$
\frac{1}{N(0)V} = \int_{0}^{\hbar\omega_D} \frac{d\xi}{\sqrt{\xi^2 + \Delta_0^2}} = \ln\left(\frac{\hbar\omega_D + \sqrt{(\hbar\omega_D)^2+\Delta_0^2}}{\Delta_0}\right)
$$

在[弱耦合](@entry_id:140994)极限下（$N(0)V \ll 1$），我们预期 $\Delta_0 \ll \hbar\omega_D$。因此，根号项可以近似为 $\sqrt{(\hbar\omega_D)^2+\Delta_0^2} \approx \hbar\omega_D$。方程简化为 $\frac{1}{N(0)V} \approx \ln(\frac{2\hbar\omega_D}{\Delta_0})$。最终解得零温[能隙](@entry_id:191975)的著名表达式 [@problem_id:1272047]：

$$
\Delta_0 = 2\hbar\omega_D \exp\left(-\frac{1}{N(0)V}\right)
$$

这个结果与[库珀问题](@entry_id:161364)的解在形式上高度一致，再次体现了超导配对的非微扰本质。

有了[能隙](@entry_id:191975) $\Delta$，[BCS理论](@entry_id:144185)中的[元激发](@entry_id:140859)——**[准粒子](@entry_id:136584)**——的能量谱也就确定了。通过所谓的**[Bogoliubov变换](@entry_id:160944)**，可以将原来的电子产生湮灭算符线性组合成新的[准粒子](@entry_id:136584)算符。这种变换使得BCS[哈密顿量对角化](@entry_id:139738)，其[能量本征值](@entry_id:144381)为：

$$
E_k = \sqrt{\xi_k^2 + \Delta^2}
$$

这就是[准粒子](@entry_id:136584)的[激发能](@entry_id:190368)。从这个色散关系可以看出，激发一个[准粒子](@entry_id:136584)所需的最小能量是 $\Delta$（当 $\xi_k=0$ 时），这正是[超导能隙](@entry_id:145058)的物理意义：它是破坏一个库珀对、在系统中产生两个[准粒子激发](@entry_id:138475)所需能量的一半。

[Bogoliubov变换](@entry_id:160944)的系数正是前面提到的 $u_k$ 和 $v_k$。它们与[能隙](@entry_id:191975)和[单粒子能量](@entry_id:160812)的关系为：

$$
u_k^2 = \frac{1}{2}\left(1 + \frac{\xi_k}{E_k}\right), \quad v_k^2 = \frac{1}{2}\left(1 - \frac{\xi_k}{E_k}\right)
$$

这些[准粒子](@entry_id:136584)并非简单的电子或空穴，而是它们的相干叠加。一个准[粒子[产](@entry_id:158755)生算符](@entry_id:191512) $\gamma^\dagger_{\mathbf{k}\uparrow}$ 可以表示为 $\gamma^\dagger_{\mathbf{k}\uparrow} = u_k c^\dagger_{\mathbf{k}\uparrow} - v_k c_{-\mathbf{k}\downarrow}$。这意味着产生一个 $\mathbf{k}\uparrow$ [准粒子](@entry_id:136584)，既有 $u_k^2$ 的概率产生一个 $\mathbf{k}\uparrow$ 电子，又有 $v_k^2$ 的概率湮灭一个 $-\mathbf{k}\downarrow$ 电子（即产生一个 $-\mathbf{k}\downarrow$ 空穴）。

这种电子-空穴的混合特性可以从[准粒子](@entry_id:136584)的**有效电荷**中得到验证。考虑一个能量为 $E > \Delta$ 的[准粒子](@entry_id:136584)，它可能对应于电子型分支（$\xi_k = \sqrt{E^2-\Delta^2} > 0$）或空穴型分支（$\xi_k = -\sqrt{E^2-\Delta^2}  0$）。通过计算当一个[准粒子](@entry_id:136584)被激发时系统总[电荷](@entry_id:275494)的变化，可以定义其[有效电荷](@entry_id:748807) $e^*$。计算表明，[准粒子](@entry_id:136584)的[有效电荷](@entry_id:748807)为 $e^* = e(u_k^2 - v_k^2) = e(\xi_k/E_k)$ [@problem_id:1272009]。

这个结果非常直观：
-   对于费米面上的激发（$\xi_k = 0, E_k = \Delta$），$e^*=0$。[准粒子](@entry_id:136584)是电子和空穴的等量叠加，呈电中性。
-   对于远离[费米面](@entry_id:137798)的电子型激发（$\xi_k \gg \Delta, E_k \approx \xi_k$），$e^* \approx e$。[准粒子](@entry_id:136584)几乎就是一个纯电子。
-   对于远离费米面的空穴型激发（$-\xi_k \gg \Delta, E_k \approx -\xi_k$），$e^* \approx -e$。[准粒子](@entry_id:136584)几乎就是一个纯空穴。

### BCS态的可观测性质

[BCS理论](@entry_id:144185)的强大之处在于它不仅提供了一个优美的理论框架，还对[超导体](@entry_id:191025)的各种物理性质做出了可供实验检验的定量预言。

#### [动量分布](@entry_id:162113)函数

在正常的费米金属中，零温下的电子[动量分布](@entry_id:162113) $\langle n_{k\sigma} \rangle = \langle c^\dagger_{k\sigma} c_{k\sigma} \rangle$ 是一个阶跃函数：在费米面以内为1，以外为0。而在[BCS基态](@entry_id:136275)中，由于库珀对的形成，费米面被“模糊”了。我们可以利用[Bogoliubov变换](@entry_id:160944)来计算这个平均占据数。

在[BCS基态](@entry_id:136275)（即[准粒子](@entry_id:136584)真空态）中，$\langle \gamma^\dagger \gamma \rangle=0$。通过将 $c^\dagger, c$ 用 $\gamma^\dagger, \gamma$ 表示，可以计算出 [@problem_id:1272045]：

$$
\langle n_{k\sigma} \rangle = \langle \Psi_{BCS} | c^\dagger_{k\sigma} c_{k\sigma} | \Psi_{BCS} \rangle = v_k^2 = \frac{1}{2}\left(1 - \frac{\xi_k}{\sqrt{\xi_k^2 + \Delta^2}}\right)
$$

这个函数在[费米面](@entry_id:137798)（$\xi_k=0$）附近平滑地从接近1过渡到接近0，而不是一个突变。对于能量远低于费米能的态（$\xi_k \to -\infty$），$v_k^2 \to 1$，态被占据。对于能量远高于费米能的态（$\xi_k \to +\infty$），$v_k^2 \to 0$，态为空。这种[费米面](@entry_id:137798)的[模糊化](@entry_id:260771)是库珀对凝聚的直接后果，也是实验上可以通过角分辨光电子能谱（ARPES）等技术观测到的关键特征。相应地，对态 $(\mathbf{k}\uparrow, -\mathbf{k}\downarrow)$ 为空的概率为 $u_k^2 = 1 - v_k^2 = \frac{1}{2}\left(1 + \frac{\xi_k}{\sqrt{\xi_k^2 + \Delta^2}}\right)$ [@problem_id:1272005]。

#### [凝聚能](@entry_id:195476)

[超导相变](@entry_id:141757)之所以发生，是因为[BCS基态](@entry_id:136275)的能量比正常金属态的基态能量更低。这个能量差被称为**[凝聚能](@entry_id:195476)**。[凝聚能](@entry_id:195476)密度 $\mathcal{E}_c$ 可以通过计算超导态能量 $E_S$ 和正常态能量 $E_N$ 的差值得到。

在一个细致的计算中，我们需要分别写出 $E_S$ 和 $E_N$ 的表达式，并利用[能隙方程](@entry_id:141924)来消去相互作用参数 $V$。经过一番代数运算和在弱耦合极限（$\Delta \ll \hbar\omega_D$）下的积分近似，可以得到一个非常简洁而重要的结果 [@problem_id:1271962]：

$$
\mathcal{E}_c = \frac{E_S - E_N}{V_{\text{vol}}} = -\frac{1}{2} N(0) \Delta^2
$$

这个结果表明，超导态的[能量稳定性](@entry_id:748991)正比于[费米面态密度](@entry_id:161911)和[能隙](@entry_id:191975)的平方。[能隙](@entry_id:191975)越大，超导态就越稳定。这个[凝聚能](@entry_id:195476)最终与[热力学](@entry_id:141121)[临界磁场](@entry_id:145488)直接相关，是超[导电性](@entry_id:137481)[热力学性质](@entry_id:146047)的基础。

#### 空间结构与相干长度

[库珀对](@entry_id:143370)不是点状粒子，它具有一定的空间尺度。这个尺度被称为**[BCS相干长度](@entry_id:189204)** $\xi_0$，可以理解为构成一个[库珀对](@entry_id:143370)的两个电子之间的平均距离。从[波函数](@entry_id:147440)的角度看，它描述了对关联函数 $F(\mathbf{r}) = \langle \psi_\uparrow(\mathbf{r}) \psi_\downarrow(0) \rangle$ 的衰减长度。

$F(\mathbf{r})$ 是其[傅里叶变换](@entry_id:142120) $F_{\mathbf{k}} = \langle c_{\mathbf{k}\uparrow} c_{-\mathbf{k}\downarrow} \rangle$ 的空间对应物。在[BCS理论](@entry_id:144185)中，$F_{\mathbf{k}} = u_k v_k = \frac{\Delta_0}{2E_k}$。为了得到 $F(\mathbf{r})$ 的长程行为，我们需要对 $F_{\mathbf{k}}$ 进行[傅里叶变换](@entry_id:142120)。由于 $F_{\mathbf{k}}$ 主要在[费米面](@entry_id:137798)（$k \approx k_F$）附近有较大贡献，并且其能量依赖性由 $E_k = \sqrt{(\hbar v_F(k-k_F))^2 + \Delta_0^2}$ 决定，变换的结果显示 $F(r)$ 在大 $r$ 处呈指数衰减 $e^{-r/\xi_0}$。衰减长度（即[相干长度](@entry_id:139128)）为 [@problem_id:1272029]：

$$
\xi_0 = \frac{\hbar v_F}{\Delta_0}
$$

这个关系式揭示了相干长度与费米速度成正比，与[能隙](@entry_id:191975)成反比。物理图像是：[能隙](@entry_id:191975)越小，对的束缚越弱，两个电子分得越开，[相干长度](@entry_id:139128)越大。费米速度越大，在发生一次有效的吸引散射之前，电子能跑得更远，因此配对的空间尺度也更大。在传统[超导体](@entry_id:191025)中，$\xi_0$ 通常在几百到几千埃，远大于原子间距。这意味着在任何一个[库珀对](@entry_id:143370)占据的空间内，都包含了大量其他[库珀对](@entry_id:143370)的中心，这正是平均场理论得以适用的原因。

更进一步，我们可以计算完整的对[波函数](@entry_id:147440) $\Psi(\mathbf{r})$，它是[动量空间](@entry_id:148936)对振幅 $g_k = v_k/u_k$ 的[傅里叶变换](@entry_id:142120)。对于一个s波[超导体](@entry_id:191025)，在一些合理的近似下，对[波函数](@entry_id:147440)的形式为 [@problem_id:1271922]：

$$
\Psi(r) \propto \frac{\sin(k_F r)}{r} \exp\left(-\frac{\Delta r}{\hbar v_F}\right) = \frac{\sin(k_F r)}{r} \exp\left(-\frac{r}{\xi_0}\right)
$$

这个形式优美地展示了[库珀对](@entry_id:143370)的内部结构：一个以费米波长 $\lambda_F = 2\pi/k_F$ 为周期的快速[振荡](@entry_id:267781)部分，被一个以相干长度 $\xi_0$ 为特征长度的指数衰减包络所调制。

#### [热力学普适性](@entry_id:147476)

BCS理论的一个惊人预言是，许多[热力学](@entry_id:141121)量之间的比值是与具体材料无关的[普适常数](@entry_id:165600)。其中最著名的就是零温[能隙](@entry_id:191975) $\Delta_0$ 和超导临界温度 $T_c$ 之间的关系。$T_c$ 是超导能隙消失的温度。

通过求解有限温度下的[能隙方程](@entry_id:141924)，并在 $T \to T_c$ 时将其线性化，可以得到 $T_c$ 的表达式。将其与零温[能隙](@entry_id:191975) $\Delta_0$ 的表达式联系起来，可以在弱耦合极限下推导出以下普适比值 [@problem_id:1272040]：

$$
\frac{2\Delta_0}{k_B T_c} = \frac{2\pi}{e^\gamma} \approx 3.528
$$

或者写作 $\Delta_0 / (k_B T_c) = \pi e^{-\gamma}$。这里的 $\gamma \approx 0.577$ 是[欧拉-马歇罗尼常数](@entry_id:146205)。这个比值不依赖于 $N(0)$, $V$, $\omega_D$ 等任何材料参数，是BCS理论的一个核心预言。实验上，许多传统[超导体](@entry_id:191025)（如铝、锡、铅）的测量值都非常接近3.5，这为BCS理论的正确性提供了强有力的支持。

综上所述，从[库珀不稳定性](@entry_id:145007)出发，BCS理论成功地构建了一个描述超导态的微观模型。它不仅解释了[能隙](@entry_id:191975)的存在和库珀对的形成，还定量地预言了[超导体](@entry_id:191025)的动量分布、[凝聚能](@entry_id:195476)、相干长度和[热力学](@entry_id:141121)[普适常数](@entry_id:165600)等一系列关键物理性质，标志着[凝聚态物理学](@entry_id:140205)的一个伟大胜利。