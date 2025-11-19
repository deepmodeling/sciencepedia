## 引言
在探索由大量粒子构成的量子世界的奥秘时，理解粒子之间如何相互“感知”并[排列](@entry_id:136432)彼此的位置至关重要。[密度关联](@entry_id:157860)正是描述这种微观结构和内在联系的核心物理量，它不仅揭示了粒子间相互作用的细节，也反映了其固有的量子统计属性，是连接微观[哈密顿量](@entry_id:172864)与宏观可观测现象的桥梁。然而，尽管其定义简洁，但[密度关联](@entry_id:157860)在不同物理系统和能量尺度下展现出的丰富行为，及其在看似无关的科学领域中的普适性，往往构成了一道知识上的鸿沟。本篇文章旨在系统性地跨越这一鸿沟，为读者提供一个关于[玻色气体](@entry_id:155364)中[密度关联](@entry_id:157860)的全面视角。

在接下来的内容中，我们将分三步展开。首先，在“原理与机制”一章中，我们将奠定理论基础，从关联函数的基本定义出发，逐步剖析其在无相互作用热气体、[弱相互作用](@entry_id:157579)[玻色-爱因斯坦凝聚体](@entry_id:145990)（BEC）中的表现，并最终触及描述强关联效应的普适Tan接触理论。随后，在“应用与跨学科联系”一章中，我们将展示这一理论工具的强大威力，看它如何被用来探测[量子晶体](@entry_id:196740)与[拓扑缺陷](@entry_id:138787)、解码[元激发](@entry_id:140859)谱，乃至在[非平衡动力学](@entry_id:160262)、[量子信息](@entry_id:137721)和[基因组学](@entry_id:138123)等前沿[交叉](@entry_id:147634)领域中发挥关键作用。最后，通过“动手实践”部分的精选问题，读者将有机会亲手运用所学知识，解决具体物理情境下的关联问题，从而深化理解。通过这一结构化的学习路径，我们将共同揭示[密度关联](@entry_id:157860)作为理解多体世界通用语言的深刻内涵。

## 原理与机制

在理解[多体系统](@entry_id:144006)的物理学时，对其组分粒子间的位置与动量关联进行表征是至关重要的。这些关联不仅揭示了粒子间的相互作用，还反映了其固有的量子统计性质。在本章中，我们将深入探讨[玻色气体](@entry_id:155364)中[密度关联](@entry_id:157860)的原理与机制，从基本定义出发，逐步过渡到描述非相互作用热气体、[弱相互作用](@entry_id:157579)玻色-爱因斯坦凝聚体（BEC）以及最终触及[强关联体系](@entry_id:145791)中的普适物理。

### 关联函数：定义与诠释

描述粒子[空间[分](@entry_id:188271)布](@entry_id:182848)的统计特性，最直接的工具是 **$N$ 阶归一化关联函数** (normalized $N$-th order correlation function)，其定义为：
$$ g^{(N)}(\mathbf{r}_1, \dots, \mathbf{r}_N) = \frac{\langle \hat{\psi}^\dagger(\mathbf{r}_1) \dots \hat{\psi}^\dagger(\mathbf{r}_N) \hat{\psi}(\mathbf{r}_N) \dots \hat{\psi}(\mathbf{r}_1) \rangle}{\langle \hat{n}(\mathbf{r}_1) \rangle \dots \langle \hat{n}(\mathbf{r}_N) \rangle} $$
其中 $\hat{\psi}^\dagger(\mathbf{r})$ 和 $\hat{\psi}(\mathbf{r})$ 分别是在位置 $\mathbf{r}$ 处的玻色场产生和[湮灭算符](@entry_id:165390)，$\hat{n}(\mathbf{r}) = \hat{\psi}^\dagger(\mathbf{r})\hat{\psi}(\mathbf{r})$ 是粒子数[密度算符](@entry_id:138151)，而 $\langle \dots \rangle$ 表示在给定系综（如[巨正则系综](@entry_id:141562)）下的[热力学平均](@entry_id:755909)。

$g^{(N)}$ 的物理意义是，在位置 $\mathbf{r}_1, \dots, \mathbf{r}_N$ 同时找到一个粒子的[联合概率](@entry_id:266356)，与假设[粒子分布](@entry_id:158657)完全随机（即各点密度乘积）时的概率之比。因此，它直接量化了由[量子统计](@entry_id:143815)或相互作用引起的偏离随机[分布](@entry_id:182848)的程度。

在实践中，最常用的是 **二阶关联函数**（或称 **对关联函数**）$g^{(2)}(\mathbf{r}_1, \mathbf{r}_2)$。它描述了在 $\mathbf{r}_1$ 处找到一个粒子的条件下，在 $\mathbf{r}_2$ 处找到另一个粒子的相对概率。对于均匀系统，该函数仅依赖于相对坐标 $\mathbf{R} = \mathbf{r}_1 - \mathbf{r}_2$，记作 $g^{(2)}(\mathbf{R})$。
*   若 $g^{(2)}(\mathbf{R}) > 1$，则表明粒子倾向于聚集在一起，称为 **聚束 (bunching)**。
*   若 $g^{(2)}(\mathbf{R})  1$，则表明粒子相互排斥，称为 **[反聚束](@entry_id:194774) (antibunching)**。
*   若 $g^{(2)}(\mathbf{R}) = 1$，则表示粒子之间没有关联，其[分布](@entry_id:182848)是泊松式的。

一个特别重要的物理量是 **局域关联函数** (local correlation function)，即所有坐标重合时的值，例如 $g^{(N)}(0)$。$g^{(2)}(0)$ 描述了在同一点找到两个粒子的相对概率，它[直接探测](@entry_id:748463)了体系的短程物理。

### 无相互作用热[玻色气体](@entry_id:155364)中的关联

即使在没有粒子间相互作用的情况下，仅由量子统计所决定的不可区分性也会在多粒子[波函数](@entry_id:147440)中引入深刻的关联。对于[玻色子](@entry_id:138266)系统，这种关联表现为众所周知的 **[玻色子](@entry_id:138266)聚束 (boson bunching)** 效应。

考虑一个处于正常相（即未发生[玻色-爱因斯坦凝聚](@entry_id:144849)）的均匀、无相互作用的热[玻色气体](@entry_id:155364)。我们可以计算其局域二阶关联函数 $g^{(2)}(0)$ [@problem_id:1238067]。其定义为：
$$ g^{(2)}(0) = \frac{\langle \hat{\psi}^\dagger(\mathbf{r})\hat{\psi}^\dagger(\mathbf{r})\hat{\psi}(\mathbf{r})\hat{\psi}(\mathbf{r}) \rangle}{\langle \hat{\psi}^\dagger(\mathbf{r})\hat{\psi}(\mathbf{r}) \rangle^2} $$
为了计算分子上的四算符平均值，我们将[场算符](@entry_id:140269)按[平面波展开](@entry_id:152012) $\hat{\psi}(\mathbf{r}) = \frac{1}{\sqrt{V}} \sum_{\mathbf{k}} e^{i\mathbf{k}\cdot\mathbf{r}} \hat{a}_{\mathbf{k}}$。对于[无相互作用系统](@entry_id:143064)，其[热力学态](@entry_id:755916)是高斯态，因此[高阶矩](@entry_id:266936)可以通过 **维克定理 (Wick's theorem)** 分解为二阶矩的乘积。对于[玻色子](@entry_id:138266)，四算符的平均值为：
$$ \langle\hat{a}_{\mathbf{p}}^\dagger \hat{a}_{\mathbf{q}}^\dagger \hat{a}_{\mathbf{r}} \hat{a}_{\mathbf{s}}\rangle = \langle\hat{a}_{\mathbf{p}}^\dagger \hat{a}_{\mathbf{s}}\rangle \langle\hat{a}_{\mathbf{q}}^\dagger \hat{a}_{\mathbf{r}}\rangle + \langle\hat{a}_{\mathbf{p}}^\dagger \hat{a}_{\mathbf{r}}\rangle \langle\hat{a}_{\mathbf{q}}^\dagger \hat{a}_{\mathbf{s}}\rangle $$
在[巨正则系综](@entry_id:141562)中，动量模式的平均占据数由[玻色-爱因斯坦分布](@entry_id:145257)给出：$\langle \hat{a}_{\mathbf{k}}^\dagger \hat{a}_{\mathbf{k}'} \rangle = \delta_{\mathbf{k},\mathbf{k}'} n_{\mathbf{k}}$，其中 $n_{\mathbf{k}} = (z^{-1}e^{\beta \varepsilon_{\mathbf{k}}} - 1)^{-1}$，$z=e^{\beta\mu}$ 是逸度。

将[平面波展开](@entry_id:152012)代入 $g^{(2)}(0)$ 的分子，并应用维克定理，我们得到：
$$ \langle (\hat{\psi}^\dagger)^2 (\hat{\psi})^2 \rangle = \frac{1}{V^2} \sum_{\mathbf{p},\mathbf{q},\mathbf{r},\mathbf{s}} \langle \hat{a}_{\mathbf{p}}^\dagger \hat{a}_{\mathbf{q}}^\dagger \hat{a}_{\mathbf{r}} \hat{a}_{\mathbf{s}} \rangle = \frac{1}{V^2} \sum_{\mathbf{p},\mathbf{q}} (n_{\mathbf{p}}n_{\mathbf{q}} + n_{\mathbf{p}}n_{\mathbf{q}}) = \frac{2}{V^2} \left( \sum_{\mathbf{k}} n_{\mathbf{k}} \right)^2 $$
注意到系统的平均密度 $n = \frac{1}{V} \sum_{\mathbf{k}} n_{\mathbf{k}}$，因此分子等于 $2n^2$。分母是 $\langle \hat{n} \rangle^2 = n^2$。于是我们得到了一个惊人而普适的结果：
$$ g^{(2)}(0) = \frac{2n^2}{n^2} = 2 $$
这个结果表明，在任意一点找到两个无相互作用的[玻色子](@entry_id:138266)的概率是随机[分布](@entry_id:182848)情况下的两倍。这种聚束效应是[玻色子](@entry_id:138266)[交换对称性](@entry_id:151892)的直接体现。值得注意的是，该结果不依赖于温度或密度，只要系统处于热平衡的正常相即可。

这一结论可以推广到更高阶的局域关联。例如，通过类似的方法计算三阶局域关联函数 $g^{(3)}(0)$ [@problem_id:1238164]，需要计算 $\langle (\hat{\psi}^\dagger)^3 (\hat{\psi})^3 \rangle$。应用维克定理，对六个算符进行配对，共有 $3! = 6$ 种不同的完全收缩方式。每种方式都贡献一个 $( \sum_{\mathbf{k}} n_{\mathbf{k}} )^3$ 项。因此，分子为 $6n^3$，我们得到：
$$ g^{(3)}(0) = \frac{6n^3}{n^3} = 6 $$
可以进一步推广，对于一个无相互作用的热[玻色气体](@entry_id:155364)，其 $N$ 阶局域关联函数为：
$$ g^{(N)}(0) = N! $$
这个[阶乘增长](@entry_id:144229)的行为是热[玻色气体](@entry_id:155364)中量子聚束效应的鲜明特征。

### 结构因子：在动量空间中探测关联

除了在[实空间](@entry_id:754128)中研究对关联函数，在[动量空间](@entry_id:148936)中考察关联通常更为便捷，并且与实验直接相关。关键的物理量是 **[结构因子](@entry_id:158623) (structure factor)**。

**动力学结构因子** $S(\mathbf{k}, \omega)$ 定义为密度-[密度关联](@entry_id:157860)函数的时空[傅里叶变换](@entry_id:142120)：
$$ S(\mathbf{k}, \omega) = \frac{1}{N} \int dt d^3\mathbf{r} \, e^{i(\omega t - \mathbf{k}\cdot\mathbf{r})} \langle \hat{n}(\mathbf{r}, t) \hat{n}(0, 0) \rangle $$
它描述了系统在受到一个具有波矢 $\mathbf{k}$ 和频率 $\omega$ 的微扰时，产生[密度涨落](@entry_id:143540)的能力。$S(\mathbf{k}, \omega)$ 是非弹性散射实验（如[中子散射](@entry_id:142835)或布拉格谱学）中直接测量的量，它揭示了系统的[元激发](@entry_id:140859)谱。

对频率积分，我们得到 **[静态结构因子](@entry_id:141682)** $S(\mathbf{k})$：
$$ S(\mathbf{k}) = \frac{1}{N} \langle \hat{\rho}_{-\mathbf{k}} \hat{\rho}_{\mathbf{k}} \rangle = 1 + n \int d^3\mathbf{R} \, e^{-i\mathbf{k}\cdot\mathbf{R}} [g^{(2)}(\mathbf{R}) - 1] $$
其中 $\hat{\rho}_{\mathbf{k}} = \sum_j e^{-i\mathbf{k}\cdot\hat{\mathbf{r}}_j}$ 是[密度算符](@entry_id:138151)的傅里叶分量。$S(\mathbf{k})$ 描述了系统中[密度涨落](@entry_id:143540)的空间关联，可以看作是 $g^{(2)}(\mathbf{R})$ 在[动量空间](@entry_id:148936)的对应物。

系统的涨落性质（由[结构因子](@entry_id:158623)描述）和其对外界微扰的响应性质（由响应函数描述）之间存在着深刻的联系，这一联系由 **涨落-耗散定理 (fluctuation-dissipation theorem)** 给出。在零温极限下 ($T=0$)，这个定理有一个简洁而强大的形式。系统的线性密度[响应函数](@entry_id:142629) $\chi(\mathbf{k}, \omega)$ 描述了系统密度对一个频率为 $\omega$、波矢为 $\mathbf{k}$ 的微弱外势的[线性响应](@entry_id:146180)。在 $T=0$ 时，动力学结构因子 $S(\mathbf{k}, \omega)$ 和响应函数 $\chi(\mathbf{k}, \omega)$ 的虚部之间存在精确关系 [@problem_id:1238064]：
$$ S(\mathbf{k}, \omega) = -\frac{\hbar}{\pi} \Theta(\omega) \text{Im}[\chi(\mathbf{k}, \omega)] $$
其中 $\Theta(\omega)$ 是亥维赛德[阶跃函数](@entry_id:159192)。该关系式表明，系统自发的密度涨落谱（$S(\mathbf{k}, \omega)$）完全由其[能量耗散](@entry_id:147406)谱（$\text{Im}[\chi(\mathbf{k}, \omega)]$）决定。这一定理是现代多体物理的基石之一，它允许我们通过测量一个量来推断另一个量。

### 弱相互作用[玻色-爱因斯坦凝聚体](@entry_id:145990)中的关联

当温度降低到[临界温度](@entry_id:146683)以下，相互作用的[玻色气体](@entry_id:155364)进入[玻色-爱因斯坦凝聚](@entry_id:144849)（BEC）相。此时，宏观数量的粒子占据动量为零的单粒[子基](@entry_id:151637)态。系统的关联性质不再由热涨落主导，而是由粒子间的相互作用和凝聚体的量子多体[基态](@entry_id:150928)结构所决定。

描述[弱相互作用](@entry_id:157579)BEC的理论是 **[Bogoliubov理论](@entry_id:143375)**。该理论将零动量模式的算符 $\hat{a}_0, \hat{a}_0^\dagger$ 替换为经典数 $\sqrt{N_0}$，从而将[哈密顿量](@entry_id:172864)近似为一个关于非零[动量算符](@entry_id:151743)（$\mathbf{k} \neq 0$）的二次型。通过 **[Bogoliubov变换](@entry_id:160944)**，引入新的[玻色算符](@entry_id:148361)，即 **[准粒子](@entry_id:136584) (quasiparticle)** 算符 $\hat{\beta}_{\mathbf{k}}, \hat{\beta}_{\mathbf{k}}^\dagger$，可以使[哈密顿量对角化](@entry_id:139738)。相互作用[基态](@entry_id:150928) $|\Psi_G\rangle$ 被定义为[准粒子](@entry_id:136584)真空态，即对于所有 $\mathbf{k} \neq 0$，满足 $\hat{\beta}_{\mathbf{k}} |\Psi_G\rangle = 0$。这意味着在[基态](@entry_id:150928)中，[准粒子](@entry_id:136584)的激发数为零。一个直接的推论是，任何产生[准粒子](@entry_id:136584)对的算符在[基态](@entry_id:150928)中的[期望值](@entry_id:153208)都为零，例如 $\langle \Psi_G | \hat{\beta}_{\mathbf{k}}^\dagger \hat{\beta}_{-\mathbf{k}}^\dagger | \Psi_G \rangle = 0$ [@problem_id:1238055]。

在[Bogoliubov理论](@entry_id:143375)框架下，我们可以计算出BEC的[静态结构因子](@entry_id:141682) $S(k)$ [@problem_id:1238088]。对于一个均匀的三维BEC，其粒子质量为 $m$，平均密度为 $n$，[相互作用强度](@entry_id:192243)为 $U_0$，其结果为：
$$ S(k) = \frac{\varepsilon_k^0}{E_k} = \sqrt{\frac{\varepsilon_k^0}{\varepsilon_k^0 + 2nU_0}} $$
其中 $\varepsilon_k^0 = \frac{\hbar^2 k^2}{2m}$ 是自由粒子的动能，$E_k = \sqrt{\varepsilon_k^0 (\varepsilon_k^0 + 2nU_0)}$ 是[Bogoliubov准粒子](@entry_id:139560)的激发能谱。引入一个重要的长度标度——**愈合长度 (healing length)** $\xi = \frac{\hbar}{\sqrt{2mnU_0}}$，它描述了[凝聚体波函数](@entry_id:162144)在受到局域扰动后恢复到其体值的特征距离。利用 $\xi$，[静态结构因子](@entry_id:141682)可以被写成一个更紧凑和普适的形式：
$$ S(k) = \frac{k\xi}{\sqrt{2 + (k\xi)^2}} $$
这个表达式揭示了BEC中[密度关联](@entry_id:157860)的丰富物理：

1.  **长波极限 ($k\xi \ll 1$)**: 当 $k \to 0$ 时，$S(k)$ 呈线性行为 $S(k) \approx \frac{\xi}{\sqrt{2}} k$。这种[线性依赖](@entry_id:185830)关系是[声子](@entry_id:140728)存在的直接标志。一般而言，在存在线性[色散](@entry_id:263750)[元激发](@entry_id:140859) $\omega_k = ck$ 的系统中，$S(k)$ 在小 $k$ 极限下趋近于 $S(k) \approx \frac{\hbar k}{2mc}$。通过比较这两个表达式，我们可以确定BEC中的声速 [@problem_id:1238163]：
    $$ c = \sqrt{\frac{nU_0}{m}} $$
    这个声速恰好与[Bogoliubov色散](@entry_id:157826)关系在小 $k$ 极限下的斜率 $E_k/\hbar \approx ck$ 相吻合。此外，利用[流体动力学](@entry_id:136788)关系 $c^2 = (m\kappa_T)^{-1}$（在 $T=0$ 时[等温压缩率](@entry_id:140894) $\kappa_T$ 等于[绝热压缩率](@entry_id:139833)），我们可以将[静态结构因子](@entry_id:141682)的长波行为与系统的宏观[热力学性质](@entry_id:146047)联系起来。例如，可以推导出系统的[等温压缩率](@entry_id:140894) [@problem_id:1238085]。

2.  **短波极限 ($k\xi \gg 1$)**: 当 $k \to \infty$ 时，$S(k) \to 1$。这表明在高动量（短距离）下，粒子表现得好像彼此不相关，符合经典气体的图像。然而，我们稍后会看到，这只是[Bogoliubov近似](@entry_id:145204)的结果，更精确的理论会给出修正。

Bogoliubov[基态](@entry_id:150928) $|\Psi_G\rangle$ 虽然是[准粒子](@entry_id:136584)的真空，但对于原始的原子算符而言，它是一个复杂的关联态。具体来说，相互作用导致原子不断地从凝聚体中以动量相反的对 $(\mathbf{k}, -\mathbf{k})$ 的形式被散射出去，并重新复合回到凝聚体中。这导致即使在[基态](@entry_id:150928)中，非零动量模式的占据数 $n_k = \langle \hat{a}_{\mathbf{k}}^\dagger \hat{a}_{\mathbf{k}} \rangle = v_k^2$ 也不为零，这被称为 **凝聚体损耗 (condensate depletion)**。这种成对的关联可以在动量空间中的密度-[密度关联](@entry_id:157860)中看到。我们可以计算[动量空间](@entry_id:148936)对关联函数 $\langle \hat{n}_{\mathbf{k}} \hat{n}_{-\mathbf{k}} \rangle$ [@problem_id:1238086]。利用维克定理对高斯型的Bogoliubov[基态](@entry_id:150928)进行计算，可以得到：
$$ \langle \hat{n}_{\mathbf{k}} \hat{n}_{-\mathbf{k}} \rangle = \langle \hat{a}_{\mathbf{k}}^\dagger \hat{a}_{\mathbf{k}} \hat{a}_{-\mathbf{k}}^\dagger \hat{a}_{-\mathbf{k}} \rangle = n_k + 2n_k^2 $$
这个结果显著区别于无关联情况下的 $n_k n_{-k} = n_k^2$。额外的项 $n_k+n_k^2$ 反映了 $(\mathbf{k}, -\mathbf{k})$ 对之间存在强烈的正关联，这是相互作用BEC[基态](@entry_id:150928)的一个关键特征。

### 超越平均场：普适的[短程关联](@entry_id:158693)

标准的[Bogoliubov理论](@entry_id:143375)是一个平均场理论，它在描述长波（小动量）物理方面非常成功，但在短波（大动量）区域存在不足。为了更精确地描述系统，需要考虑超越平均场的量子涨落效应。

第一个重要的修正是 **Lee-Huang-Yang (LHY) 修正**。它为[基态能量](@entry_id:263704)密度引入了首个超越平均场的修正项，该项正比于 $(na^3)^{1/2}$，其中 $n$ 是密度，$a$ 是s波散射长度。这个修正会改变系统的化学势 $\mu = \partial\mathcal{E}/\partial n$ 和压缩性 $\partial\mu/\partial n$。通过推广的[Bogoliubov理论](@entry_id:143375)，我们可以研究[LHY修正](@entry_id:159197)对激发谱和[静态结构因子](@entry_id:141682)的影响。例如，可以计算出LHY效应对特定动量 $k_c$（定义为自由粒子动能等于[平均场相互作用](@entry_id:200557)能，$E_{k_c}^0 = gn_0$）处[静态结构因子](@entry_id:141682) $S(k_c)$ 的修正值 [@problem_id:1238049]。这个修正量 $\delta S(k_c)$ 正比于 $\sqrt{n_0 a^3}$，表明它是一个纯粹的[量子涨落](@entry_id:154889)效应。

近年来，一个更深刻的图像浮现出来，即对于具有[短程相互作用](@entry_id:145678)的量子气体，其许多性质在短距离（大动量）极限下表现出一种普适性，这种普适性由一个单一的参数——**Tan接触 ([Tan's contact](@entry_id:140662))** $C$ 所支配。接触参数 $C$ 量化了系统中因相互作用而形成的近距离粒子对的密度。

Tan接触参数的引入，建立了一系列被称为 **Tan关系 (Tan relations)** 的普适联系。其中两个重要的关系描述了大动量行为：
1.  单粒子动量分布 $n_k$ 的尾部：
    $$ n_k \xrightarrow{k\to\infty} \frac{C}{k^4} $$
2.  [静态结构因子](@entry_id:141682) $S(k)$ 的尾部。

我们可以从实空间[短程关联](@entry_id:158693)来推导 $S(k)$ 的大动量行为。接触物理指出，对关联函数 $g^{(2)}(r)$ 在短距离 $r \to 0$ 处具有普适的奇异性：
$$ g^{(2)}(r) \approx \frac{C}{2\pi^2 n^2 r^2} \quad (r \to 0) $$
这个 $1/r^2$ 的发散行为反映了两个粒子在极近距离相遇的概率增强。将这个奇异行为代入 $S(k)$ 的[傅里叶变换](@entry_id:142120)定义中，可以推导出 $S(k)$ 在 $k \to \infty$ 时的渐近形式 [@problem_id:1238102]。在大 $k$ 极限下，傅里叶积分主要由 $r \to 0$ 的奇异部分贡献：
$$ S(k) - 1 = n \int d^3\mathbf{r} \, e^{-i\mathbf{k} \cdot \mathbf{r}} [g^{(2)}(r) - 1] \approx n \int d^3\mathbf{r} \, e^{-i\mathbf{k} \cdot \mathbf{r}} \left( \frac{C}{2\pi^2 n^2 r^2} \right) $$
计算该傅里叶积分得到 $\frac{2\pi^2}{k}$。因此，我们得到[静态结构因子](@entry_id:141682)的普适大动量尾部：
$$ S(k) \approx 1 + \frac{C}{nk} $$
这个 $1/k$ 的尾部行为与标准[Bogoliubov理论](@entry_id:143375)预测的 $S(k) \to 1$ 形成鲜明对比。它是一个深刻的结果，表明即使在[弱相互作用](@entry_id:157579)的BEC中，短程物理也留下了不可磨灭的印记，并可以通过测量 $S(k)$ 的高动量尾部来实验性地确定Tan接触参数 $C$。这一普适关系不仅适用于零温BEC，也适用于有限温度的[玻色气体](@entry_id:155364)，甚至[强相互作用](@entry_id:159198)的[幺正费米气体](@entry_id:160541)，展示了其在现代多体物理中的核心地位。