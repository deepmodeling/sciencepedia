## 引言
在[多体物理学](@entry_id:144526)的宏伟画卷中，[玻色-爱因斯坦凝聚](@entry_id:144849)（BEC）代表了物质的一种极致相态，其中宏观数量的粒子协同一致地占据同一个[量子态](@entry_id:146142)。然而，理想教科书中的无相互作用BEC模型，忽略了真实世界中粒子间无处不在的相互作用力。正是这些相互作用，从根本上重塑了系统的[基态](@entry_id:150928)，催生了一种纯粹的量子现象——量子耗尽。即使在绝对零度，[量子涨落](@entry_id:154889)也会将一部分粒子“踢”出凝聚体，占据非零动量态。理解这一现象不仅是对理想BEC模型的关键修正，更是通往探索相互作用[多体系统](@entry_id:144006)[基态](@entry_id:150928)中深刻量子关联和新奇[物相](@entry_id:196677)的门户。本文旨在系统性地剖析量子耗尽的物理内涵。我们将从第一章“原理与机制”出发，借助[Bogoliubov理论](@entry_id:143375)深入其微观起源，揭示其背后的[准粒子](@entry_id:136584)图像与量子关联。随后，在第二章“应用与跨学科联系”中，我们将探索量子耗尽在不同物理系统（从囚禁冷原子到[拓扑缺陷](@entry_id:138787)）中的多样化表现，并建立其与凝聚态物理及量子信息等领域的深刻联系。最后，第三章“动手实践”将通过具体的计算问题，帮助读者巩固所学知识，将理论应用于实践。

## 原理与机制

在[理想玻色气体](@entry_id:150722)中，零温下的[基态](@entry_id:150928)是一个纯粹的玻色-爱因斯坦凝聚体 (Bose-Einstein Condensate, BEC)，其中所有粒子都占据动量为零的单粒子态。然而，真实物理系统中的原子间总是存在相互作用。这些相互作用从根本上改变了[基态](@entry_id:150928)的性质。即使在绝对零度，相互作用也会导致一部分粒子被“激发”出凝聚体，占据非零动量的[量子态](@entry_id:146142)。这种纯粹由[量子涨落](@entry_id:154889)驱动的现象被称为**量子耗尽 (quantum depletion)**。本章将深入探讨量子耗尽的物理原理和核心机制，从[Bogoliubov理论](@entry_id:143375)出发，揭示其内在的量子关联结构及其对系统物理性质的深刻影响。

### 量子耗尽的起源：[Bogoliubov近似](@entry_id:145204)

考虑一个由 $N$ 个质量为 $m$ 的[玻色子](@entry_id:138266)组成的均匀气体，处于体积为 $V$ 的空间中。粒子间的相互作用假设为低能下的短程接触势，其强度由s波散射长度 $a_s$ 描述，对应的[耦合常数](@entry_id:747980) $g = 4\pi\hbar^2 a_s / m$。系统的[哈密顿量](@entry_id:172864)在[二次量子化](@entry_id:137766)形式下为：
$$
\hat{H} = \sum_{\mathbf{k}} \frac{\hbar^2 k^2}{2m} \hat{a}_{\mathbf{k}}^{\dagger} \hat{a}_{\mathbf{k}} + \frac{g}{2V} \sum_{\mathbf{k}, \mathbf{p}, \mathbf{q}} \hat{a}_{\mathbf{k}+\mathbf{q}}^{\dagger} \hat{a}_{\mathbf{p}-\mathbf{q}}^{\dagger} \hat{a}_{\mathbf{p}} \hat{a}_{\mathbf{k}}
$$
其中 $\hat{a}_{\mathbf{k}}^{\dagger}$ 和 $\hat{a}_{\mathbf{k}}$ 分别是动量为 $\mathbf{k}$ 的粒子的产生和[湮灭算符](@entry_id:165390)。

对于[弱相互作用](@entry_id:157579)的BEC，绝大多数粒子 ($N_0$) 宏观占据在 $\mathbf{k}=0$ 的[基态](@entry_id:150928)。**[Bogoliubov近似](@entry_id:145204)**的核心思想是，由于 $N_0$ 极大，$\mathbf{k}=0$ 模式的算符可以被一个经典数（c-number）替代：$\hat{a}_0, \hat{a}_0^\dagger \to \sqrt{N_0}$。然后，我们将[哈密顿量](@entry_id:172864)按非凝聚体算符（$\mathbf{k} \neq 0$）的幂次展开，并保留至二次项。

在这种近似下，描述[激发态](@entry_id:261453)的[哈密顿量](@entry_id:172864)变为：
$$
\hat{H}_{\text{ex}} \approx \sum_{\mathbf{k}\neq 0} \left[ \left(\frac{\hbar^2 k^2}{2m} + g n_0\right) \hat{a}_{\mathbf{k}}^{\dagger} \hat{a}_{\mathbf{k}} + \frac{g n_0}{2} (\hat{a}_{\mathbf{k}}^{\dagger} \hat{a}_{-\mathbf{k}}^{\dagger} + \hat{a}_{\mathbf{k}} \hat{a}_{-\mathbf{k}}) \right]
$$
其中 $n_0 = N_0/V$ 是凝聚体密度。这个[哈密顿量](@entry_id:172864)包含两个关键部分：第一项描述了非凝聚体原子在凝聚体平均场（能量为 $gn_0$）中的运动；第二项，即**反常项 (anomalous term)**，描述了从凝聚体中同时产生一对具有相反动量 $(\mathbf{k}, -\mathbf{k})$ 的粒子，或湮灭这样一对粒子的过程。正是这个不保持粒子数的反常项，成为了量子耗尽以及[基态](@entry_id:150928)中复杂量子关联的根源。[@problem_id:1264342]

### [准粒子](@entry_id:136584)与[Bogoliubov变换](@entry_id:160944)

上述[哈密顿量](@entry_id:172864) $\hat{H}_{\text{ex}}$ 在粒子表象中不是对角的，因为它混合了 $\hat{a}_{\mathbf{k}}^\dagger \hat{a}_{-\mathbf{k}}^\dagger$ 和 $\hat{a}_{\mathbf{k}} \hat{a}_{-\mathbf{k}}$。为了[对角化](@entry_id:147016)它，我们引入一套新的算符，即**[准粒子](@entry_id:136584) (quasi-particle)** 算符 $\hat{\beta}_{\mathbf{k}}$ 和 $\hat{\beta}_{\mathbf{k}}^\dagger$，它们通过**[Bogoliubov变换](@entry_id:160944)**与原子算符相联系：
$$
\hat{a}_{\mathbf{k}} = u_k \hat{\beta}_{\mathbf{k}} + v_k \hat{\beta}_{-\mathbf{k}}^{\dagger}
$$
$$
\hat{a}_{\mathbf{k}}^{\dagger} = u_k \hat{\beta}_{\mathbf{k}}^{\dagger} + v_k \hat{\beta}_{-\mathbf{k}}
$$
其中系数 $u_k$ 和 $v_k$ 是依赖于动量大小 $k=|\mathbf{k}|$ 的实函数。为了使[准粒子](@entry_id:136584)算符满足[玻色子](@entry_id:138266)[对易关系](@entry_id:136780) $[\hat{\beta}_{\mathbf{k}}, \hat{\beta}_{\mathbf{k}'}^{\dagger}] = \delta_{\mathbf{k},\mathbf{k}'}$，这些系数必须满足[归一化条件](@entry_id:156486) $u_k^2 - v_k^2 = 1$。对于排斥相互作用 ($g>0$)，[对角化](@entry_id:147016)过程要求 $u_k$ 和 $v_k$ 具有相反的符号。[@problem_id:1264451]

通过这个变换，[哈密顿量](@entry_id:172864)可以被对角化为 $\hat{H}_{\text{ex}} = \sum_{\mathbf{k}\neq 0} E_k \hat{\beta}_{\mathbf{k}}^{\dagger} \hat{\beta}_{\mathbf{k}} + E_{GS}$，其中 $E_k$ 是[准粒子](@entry_id:136584)的能量，而 $E_{GS}$ 是相互作用系统的[基态能量](@entry_id:263704)。相互作用系统的真正[基态](@entry_id:150928) $|G\rangle$ 是[准粒子](@entry_id:136584)的真空态，即对于所有 $\mathbf{k} \neq 0$，满足 $\hat{\beta}_{\mathbf{k}} |G\rangle = 0$。

对角化过程确定了系数 $u_k$ 和 $v_k$ 以及[准粒子能量](@entry_id:173936) $E_k$：
$$
u_k^2 = \frac{1}{2}\left(\frac{\epsilon_k + g n_0}{E_k} + 1\right), \quad v_k^2 = \frac{1}{2}\left(\frac{\epsilon_k + g n_0}{E_k} - 1\right)
$$
$$
E_k = \sqrt{\epsilon_k (\epsilon_k + 2gn_0)}
$$
这里 $\epsilon_k = \frac{\hbar^2 k^2}{2m}$ 是[自由粒子](@entry_id:148748)的动能。$E_k$ 被称为**[Bogoliubov色散](@entry_id:157826)关系**。在小动量极限下（$k \to 0$），$E_k \approx \sqrt{gn_0/m} \cdot \hbar k = c \hbar k$，表现为[声子](@entry_id:140728)般的线性[色散](@entry_id:263750)，其中 $c = \sqrt{gn_0/m}$ 是系统的声速。在大动量极限下（$k \to \infty$），$E_k \approx \epsilon_k$，恢复为[自由粒子](@entry_id:148748)的二次[色散](@entry_id:263750)。

[Bogoliubov变换](@entry_id:160944)的系数 $u_k$ 和 $v_k$ 的相对大小反映了[准粒子](@entry_id:136584)中“粒子”和“空穴”成分的权重。我们可以通过一个具体的例子来理解这一点：考虑一个特殊的动量，使得自由粒子动能恰好等于[平均场相互作用](@entry_id:200557)能，即 $\epsilon_k = gn_0$。在此条件下，[准粒子能量](@entry_id:173936)为 $E_k = \sqrt{gn_0(gn_0 + 2gn_0)} = \sqrt{3}gn_0$。代入系数表达式，可以计算出 $|v_k/u_k| = \sqrt{(2\sqrt{3}-3)/(2\sqrt{3}+3)}$，这是一个不为零的确定值，表明[准粒子](@entry_id:136584)总是粒子和空穴的混合体。[@problem_id:1264447]

### 量子耗尽的表征

量子耗尽最直接的体现是在动量空间中，非零动量态被占据。

#### [动量分布](@entry_id:162113)

在相互作用[基态](@entry_id:150928) $|G\rangle$ 中，动量为 $\mathbf{k}$ 的原子的平均占据数是 $\langle \hat{n}_{\mathbf{k}} \rangle = \langle G | \hat{a}_{\mathbf{k}}^{\dagger} \hat{a}_{\mathbf{k}} | G \rangle$。利用[Bogoliubov变换](@entry_id:160944)和 $\hat{\beta}_{\mathbf{k}} |G\rangle = 0$ 的性质，我们可以直接计算这个[期望值](@entry_id:153208)：
$$
\langle \hat{n}_{\mathbf{k}} \rangle = \langle G | (u_k \hat{\beta}_{\mathbf{k}}^{\dagger} + v_k \hat{\beta}_{-\mathbf{k}})(u_k \hat{\beta}_{\mathbf{k}} + v_k \hat{\beta}_{-\mathbf{k}}^{\dagger}) | G \rangle = v_k^2 \langle G | \hat{\beta}_{-\mathbf{k}} \hat{\beta}_{-\mathbf{k}}^{\dagger} | G \rangle = v_k^2
$$
这个结果是[Bogoliubov理论](@entry_id:143375)的核心之一：即使在零温[基态](@entry_id:150928)，动量为 $\mathbf{k}$ 的模式的[平均粒子数](@entry_id:151202)也为 $v_k^2$，它不为零。这部分粒子就是被耗尽出凝聚体的粒子。[@problem_id:1264451]

$v_k^2$ 的大小依赖于动量。例如，在[静态结构因子](@entry_id:141682) $S(k) = \epsilon_k / E_k$ 取值为 $1/2$ 的特殊动量 $k_0$ 处，可以计算出该处的粒子占据数为 $n(k_0) = v_{k_0}^2 = 1/8$。[@problem_id:514119]

#### 总耗尽分数

总的耗尽原子密度 $n_{ex}$ 是对所有非零动量模式占据数的积分：
$$
n_{ex} = \int \frac{d^3k}{(2\pi)^3} \langle \hat{n}_{\mathbf{k}} \rangle = \int \frac{d^3k}{(2\pi)^3} v_k^2
$$
对于一个三维均匀[玻色气体](@entry_id:155364)，在[弱相互作用](@entry_id:157579)极限下（由无量纲气体参数 $\sqrt{na_s^3} \ll 1$ 表征，其中 $n$ 是总密度），这个积分可以被解析计算。结果表明，耗尽分数（耗尽原子密度与总密度的比值）为：
$$
\frac{n_{ex}}{n} = \frac{8}{3\sqrt{\pi}} (na_s^3)^{1/2}
$$
这个著名的公式量化了量子耗尽的程度，表明它正比于气体参数的平方根。[@problem_id:1184007]

这个微观的耗尽结果也可以用宏观可测量的量来表示。系统的化学势 $\mu \approx gn$ 和声速 $c = \sqrt{gn/m}$ 之间存在关系 $\mu=mc^2$。利用这些关系，可以将耗尽密度 $n_{ex}$ 表示为：
$$
n_{ex} = \frac{m^{3/2}\mu^{3/2}}{3\pi^2\hbar^3}
$$
这表明，可以通过测量化学势和声速来确定量子耗尽的密度。[@problem_id:1184025] 此外，由于耗尽直接依赖于[相互作用强度](@entry_id:192243)，我们可以研究耗尽分数如何随散射长度 $a_s$ 变化。计算其导数可以得到 $\frac{d}{da_s}(\frac{n_{ex}}{n}) = \frac{4\sqrt{na_s}}{\sqrt{\pi}}$，这揭示了增强相互作用会如何更有效地将粒子“踢”出凝聚体。[@problem_id:1184029]

### 相互作用[基态](@entry_id:150928)中的[量子关联](@entry_id:136327)

量子耗尽不仅是粒子占据数的重新[分布](@entry_id:182848)，它还伴随着深刻的量子关联结构。

#### 反常平均值与粒子对

Bogoliubov[基态](@entry_id:150928)的一个显著特征是它具有非零的**反常平均值 (anomalous average)**，如 $\langle \hat{a}_{\mathbf{k}} \hat{a}_{-\mathbf{k}} \rangle$。这个[期望值](@entry_id:153208)不为零，意味着[基态](@entry_id:150928)不是一个具有确定粒子数的[本征态](@entry_id:149904)。物理上，它表示从凝聚体中产生的粒子总是以动量相反的粒子对 $(\mathbf{k}, -\mathbf{k})$ 的形式出现。利用[Bogoliubov变换](@entry_id:160944)，可以算出：
$$
\langle \hat{a}_{\mathbf{k}} \hat{a}_{-\mathbf{k}} \rangle = u_k v_k
$$
由于 $u_k$ 和 $v_k$ 符号相反，该平均值为负。在 $\epsilon_k = \mu$ (这里 $\mu=gn_0$) 的条件下，这个反常配对幅度的值为 $-\frac{1}{2\sqrt{3}}$。[@problem_id:1264342]

#### [量子涨落](@entry_id:154889)与[压缩态](@entry_id:148885)

由于[基态](@entry_id:150928)不是[粒子数算符](@entry_id:153568) $\hat{n}_{\mathbf{k}}$ 的[本征态](@entry_id:149904)，$\hat{n}_{\mathbf{k}}$ 的测量结果存在涨落。其[方差](@entry_id:200758)为：
$$
\text{Var}(\hat{n}_{\mathbf{k}}) = \langle \hat{n}_{\mathbf{k}}^2 \rangle - \langle \hat{n}_{\mathbf{k}} \rangle^2
$$
通过计算可以证明，$\text{Var}(\hat{n}_{\mathbf{k}}) = (u_k v_k)^2$。这个非零的[方差](@entry_id:200758)是[基态](@entry_id:150928)量子特性的直接体现。[@problem_id:1183979]

从量子光学的角度看，Bogoliubov[基态](@entry_id:150928)对于每一个 $(\mathbf{k}, -\mathbf{k})$ 模式对，都是一个**[双模压缩真空态](@entry_id:147759) (two-mode squeezed vacuum state)**。[哈密顿量](@entry_id:172864)中的配对项 $\hat{a}_{\mathbf{k}}^{\dagger} \hat{a}_{-\mathbf{k}}^{\dagger} + \text{h.c.}$ 扮演了[双模压缩](@entry_id:183898)算符的角色。压缩的程度由一个实参数 $r_k$ 描述，它与[Bogoliubov系数](@entry_id:197738)的关系是 $u_k = \cosh(r_k)$ 和 $|v_k| = \sinh(r_k)$。由此可以推导出压缩参数 $r_k$ 与系统[能量尺度](@entry_id:196201)的关系：
$$
r_k = \frac{1}{4} \ln\left(\frac{\epsilon_k+2gn_0}{\epsilon_k}\right)
$$
这个结果将多体物理中的量子耗尽与量子信息中的[资源理论](@entry_id:142789)（[压缩态](@entry_id:148885)）紧密联系起来。[@problem_id:1264369]

#### 占据数关联

$(\mathbf{k}, -\mathbf{k})$ 粒子对的产生机制意味着这两个模式的粒子数是关联的。这种关联可以通过计算占据数算符的协[方差](@entry_id:200758)来量化：
$$
\text{Cov}(\hat{n}_{\mathbf{k}}, \hat{n}_{-\mathbf{k}}) = \langle \hat{n}_{\mathbf{k}} \hat{n}_{-\mathbf{k}} \rangle - \langle \hat{n}_{\mathbf{k}} \rangle \langle \hat{n}_{-\mathbf{k}} \rangle
$$
对于Bogoliubov[基态](@entry_id:150928)，这个协[方差](@entry_id:200758)为 $\text{Cov}(\hat{n}_{\mathbf{k}}, \hat{n}_{-\mathbf{k}}) = (u_k v_k)^2$。这个正值协[方差](@entry_id:200758)表明，如果在动量 $\mathbf{k}$ 处探测到一个粒子，那么在动量 $-\mathbf{k}$ 处探测到另一个粒子的概率会增加。这正是粒子对关联的直接证据。[@problem_id:1184070]

### 物理表现与后果

量子耗尽及其伴随的关联结构会在多种可观测的物理量中留下印记。

#### [静态结构因子](@entry_id:141682)

**[静态结构因子](@entry_id:141682)** $S(\mathbf{k})$ 描述了系统密度涨落的空间关联性。在[Bogoliubov理论](@entry_id:143375)中，它可以被计算得出 $S(k) = \epsilon_k / E_k$。这个结果与[准粒子色散](@entry_id:161746) $E_k$ 一起，完美地验证了**[Feynman关系](@entry_id:199893)**：
$$
E_k = \frac{\hbar^2 k^2}{2m S(k)}
$$
这揭示了系统的动态响应（由激发谱 $E_k$ 描述）和静态结构（由 $S(k)$ 描述）之间存在深刻的内在联系。[@problem_id:1264338]

在大动量极限下 ($k\xi \gg 1$，其中 $\xi = \hbar/\sqrt{mgn_0}$ 是**治疗长度 (healing length)**)，粒子应该表现得像[自由粒子](@entry_id:148748)。此时，动量分布 $n_k$ 有一个普适的[渐近行为](@entry_id:160836) $n_k \propto k^{-4}$。这个著名的 $k^{-4}$ 行为是短程[接触相互作用](@entry_id:150822)的直接后果，与所谓的“Tan接触”密切相关。更有趣的是，这个渐进行为与[静态结构因子](@entry_id:141682)偏离1的程度相关，其关系为 $\lim_{k\xi \gg 1} n_k / (1-S(k))^2 = 1/4$。[@problem_id:1264452]

#### 对关联函数

**对关联函数** $g^{(2)}(\mathbf{r})$ 给出了在某处发现一个粒子的条件下，在距离 $\mathbf{r}$ 处发现另一个粒子的相对概率。零距离对关联函数 $g^{(2)}(0)$ 尤其重要，因为它探测了原子“聚束”(bunching)或“[反聚束](@entry_id:194774)”(antibunching)的倾向。对于一个相互作用的BEC，由于相互作用排斥，人们可能直觉地认为 $g^{(2)}(0) \lt 1$。然而，量子耗尽的复杂性导致了更有趣的结果。在[Bogoliubov近似](@entry_id:145204)下，可以推导出 $g^{(2)}(0)$ 与耗尽分数的关系：
$$
g^{(2)}(0) \approx 1 + 2\frac{n_{ex}}{n} - \left(\frac{n_{ex}}{n}\right)^2
$$
在[弱相互作用](@entry_id:157579)下，由于 $n_{ex}/n \ll 1$，我们得到 $g^{(2)}(0) \approx 1$。[@problem_id:1184002]

更有启发性的是，如果我们只考虑被耗尽出凝聚体的原子云，并计算它们自身的对关联函数 $g^{(2)}_{ex}(0)$，我们会发现在领头阶近似下，$g^{(2)}_{ex}(0) = 3$。这个远大于1的值表明，被耗尽的原子表现出强烈的聚束行为，这与它们以粒子对的形式产生是相符的。[@problem_id:1183995]

#### 热力学性质：[Lee-Huang-Yang修正](@entry_id:159197)

量子耗尽不仅仅是一个结构上的现象，它也对系统的能量和压强等热力学性质产生重要影响。[Bogoliubov准粒子](@entry_id:139560)模式的零点能之和 $\frac{1}{2}\sum_{\mathbf{k}}(E_k - \epsilon_k - gn_0)$ 对系统的[基态能量](@entry_id:263704)有一个修正项。这个修正被称为**Lee-Huang-Yang (LHY)修正**，是超越平均场理论的第一个量子修正。对于三维系统，它对能量密度的贡献为：
$$
\mathcal{E}_{\text{LHY}}(n) = \frac{128 \sqrt{\pi} \hbar^2 a_s^{5/2}}{15 m} n^{5/2}
$$
这个[能量修正](@entry_id:198270)相应地会产生一个对压强的修正，称为**[量子压强](@entry_id:154143) (quantum pressure)** $P_Q$。在零温下，压强可以通过 $P = n^2 \frac{d(\mathcal{E}/n)}{dn}$ 计算。LHY能量项对应的[量子压强](@entry_id:154143)为：
$$
P_Q = \frac{64 \sqrt{\pi} \hbar^2 a_s^{5/2}}{5 m} n^{5/2}
$$
这表明量子涨落对系统的压强有正的贡献。[@problem_id:1264340] [@problem_id:1183989] 这些[热力学](@entry_id:141121)量与量子耗尽之间的联系可以通过系统的可压缩性来建立。例如，[等温压缩率](@entry_id:140894) $\kappa_T = \frac{1}{n}(\frac{\partial n}{\partial P})_T$ 可以与耗尽分数对密度的导数关联起来，进一步说明了量子耗尽的宏观物理效应。[@problem_id:1184003]

### 超越领头阶：高阶修正

[Bogoliubov理论](@entry_id:143375)为我们理解量子耗尽提供了坚实的基础，但它只是一个在弱相互作用极限下的领头阶近似。考虑更高阶的修正可以让我们更精确地描述系统。

#### 自洽修正

一种简单的改进方法是采用自洽的思想。我们知道，耗尽改变了凝聚体和非凝聚体的粒子数，这反过来又会影响化学势。[LHY修正](@entry_id:159197)给出了化学势的下[一阶修正](@entry_id:155896)：
$$
\mu = gn \left( 1 + \frac{32}{3\sqrt{\pi}}\sqrt{na_s^3} \right)
$$
如果我们把这个修正后的化学势代入之[前推](@entry_id:158718)导出的耗尽密度公式 $n_{ex}(\mu) = (m\mu)^{3/2}/(3\pi^2\hbar^3)$ 中，就可以得到耗尽分数的一个更高阶的修正项。这个修正项 $\delta(n_{ex}/n)$ 的量级为 $(na_s^3)$，具体为：
$$
\delta\left(\frac{n_{ex}}{n}\right) = \frac{128}{3\pi} n a_s^3
$$
这是一个系统性的方法，用于将不同阶的修正联系起来。[@problem_id:1184108]

#### [多体相互作用](@entry_id:751663)效应

真实的[冷原子系统](@entry_id:157548)中可能存在不可忽略的[三体](@entry_id:265960)相互作用。假设除了二体相互作用 $g_2$ 外，还有一个弱的三体排斥相互作用 $g_3$。这会修正Bogoliubov[哈密顿量](@entry_id:172864)中的系数，从而改变耗尽分数。通过计算可以发现，[三体](@entry_id:265960)相互作用对耗尽分数的领头阶修正为：
$$
\delta\left(\frac{N_{ex}}{N}\right) = \frac{m g_3}{\pi^{3/2} \hbar^2} n^{3/2} a_s^{1/2}
$$
这个结果在精确研究和模拟现代[冷原子](@entry_id:144092)实验中非常重要。[@problem_id:1264438]

#### [准粒子相互作用](@entry_id:146832)

[Bogoliubov理论](@entry_id:143375)得到的[准粒子](@entry_id:136584)是无相互作用的，但这仅仅是在[哈密顿量](@entry_id:172864)被近似为二次型时成立。原始[哈密顿量](@entry_id:172864)中的高阶项（三次、四次等）描述了[准粒子](@entry_id:136584)之间的相互作用，例如一个[准粒子衰变](@entry_id:137436)为两个[准粒子](@entry_id:136584)（[Beliaev阻尼](@entry_id:141908)）等过程。这些相互作用会进一步修正[基态](@entry_id:150928)[波函数](@entry_id:147440)和[可观测量](@entry_id:267133)。例如，一个简单的微扰理论模型可以说明，[准粒子](@entry_id:136584)间的相互作用如何将[准粒子](@entry_id:136584)真空态 $|G_0\rangle$ 与三[准粒子](@entry_id:136584)[态混合](@entry_id:148060)，从而导致对总耗尽[原子数](@entry_id:746561)的修正。这个修正的大小与相互作用[矩阵元](@entry_id:186505)的平方成正比，与能量分母的平方成反比，揭示了更高阶[量子涨落](@entry_id:154889)对耗尽的贡献。[@problem_id:1184065]

综上所述，量子耗尽是相互作用[玻色子](@entry_id:138266)系统[基态](@entry_id:150928)的一个基本特征，它源于零点量子涨落。[Bogoliubov理论](@entry_id:143375)为我们提供了理解其起源、量化其大小、并揭示其深刻量子关联结构的强大框架。同时，量子耗尽也通过对系统能量、压强、关联函数等物理量的影响而得以体现，并且可以通过更高阶的理论进行更精确的描述。