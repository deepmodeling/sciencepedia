## 引言
在量子多体物理的广阔领域中，理解相互作用系统的集体行为是一个核心挑战。通常，系统的[哈密顿量](@entry_id:172864)因包含粒子间的复杂相互作用而难以精确求解。然而，有一大类重要问题，其[哈密顿量](@entry_id:172864)可以简化为产生和湮灭算符的二次型。尽管形式上简化，但这些[哈密顿量](@entry_id:172864)常常包含如粒子对的产生或湮灭等“反常”项，使得以裸粒子数为基础的传统图像失效。解决这类问题的关键，在于找到一种方法来识别系统的真正[元激发](@entry_id:140859)，即[准粒子](@entry_id:136584)。玻戈留波夫变换正是实现这一目标的核心数学工具。

本文将系统地引导你掌握玻戈留波夫变换。在第一章“原理与机制”中，我们将深入探讨变换的数学基础，区分[玻色子](@entry_id:138266)和[费米子](@entry_id:146235)两种情况，并揭示其如何通过保持基本对易/[反对易关系](@entry_id:153815)来[对角化](@entry_id:147016)[哈密顿量](@entry_id:172864)。接下来，在第二章“应用与跨学科联系”中，我们将展示这一变换的强大威力，看它如何统一解释从凝聚态物理中的超导、超流，到[量子光学](@entry_id:140582)中的[压缩光](@entry_id:166152)，乃至宇宙学中的[安鲁效应](@entry_id:146787)等前沿现象。最后，通过第三章“动手实践”中的精选习题，你将有机会亲手计算，将抽象的理论应用于具体问题，从而真正巩固所学知识。

## 原理与机制

在多体系统的量子理论中，我们经常遇到这样一类[哈密顿量](@entry_id:172864)：它们是产生和[湮灭算符](@entry_id:165390)的二次型，但并非对角化的。这些[哈密顿量](@entry_id:172864)除了包含像 $a_k^\dagger a_k$ 这样描述粒子数的项外，还常常包含形如 $a_k a_{-k}$ 或 $c_k^\dagger c_{-k}^\dagger$ 的“反常”项。这些项描述了粒子对的产生或湮灭，意味着由原始[粒子数算符](@entry_id:153568)的本征态构成的福克（Fock）基不再是系统的[能量本征态](@entry_id:152154)。因此，这些原始的“裸”粒子并非系统的真正[元激发](@entry_id:140859)。

为了解决这个问题，我们需要寻找到一种新的算符，使其能够将[哈密顿量对角化](@entry_id:139738)。这种[对角化](@entry_id:147016)的[哈密顿量](@entry_id:172864)将具有 $H = E_0 + \sum_k E_k \alpha_k^\dagger \alpha_k$ 的形式，其中 $\alpha_k$ 和 $\alpha_k^\dagger$ 是新算符，它们描述了系统的真正[元激发](@entry_id:140859)——**[准粒子](@entry_id:136584)（quasiparticles）**。$E_k$ 是[准粒子](@entry_id:136584)的激发能，而 $E_0$ 则是系统新的、真实的[基态能量](@entry_id:263704)。实现这一目标的数学工具，即通过对原始产生和湮灭算符进行[线性组合](@entry_id:154743)来构造新的[准粒子](@entry_id:136584)算符，就是**玻戈留波夫变换（Bogoliubov Transformation）**。根据所处理粒子的统计性质，该变换可以分为[玻色子](@entry_id:138266)和[费米子](@entry_id:146235)两种情况，它们在具体形式和约束条件上有所不同，但其核心物理思想是一致的：找到系统的“简正模式”，即稳定的[元激发](@entry_id:140859)。

### [玻色子](@entry_id:138266)玻戈留波夫变换

对于玻色系统，玻戈留波夫变换通过混合原始的产生和[湮灭算符](@entry_id:165390)来定义新的[玻色算符](@entry_id:148361)。这个过程必须保持[玻色子](@entry_id:138266)[代数结构](@entry_id:137052)的核心——**[对易关系](@entry_id:136780)（Canonical Commutation Relations, CCR）**。

#### 典范[对易关系](@entry_id:136780)的保持

让我们从最简单的单模系统开始。假设有一组[玻色算符](@entry_id:148361) $(a, a^\dagger)$ 满足 $[a, a^\dagger] = 1$。我们定义一组新的算符 $(b, b^\dagger)$，它们是 $(a, a^\dagger)$ 的[线性组合](@entry_id:154743)：
$$
b = u a + v a^\dagger
$$
其中 $u$ 和 $v$ 是复数系数。为了让 $b$ 和 $b^\dagger$ 也描述一个合法的[玻色子](@entry_id:138266)模式，它们必须满足相同的对易关系，即 $[b, b^\dagger] = 1$。为了推导 $u$ 和 $v$ 必须满足的条件，我们来计算这个新的对易子 [@problem_id:2768492]：
$$
\begin{align}
[b, b^\dagger]  &= [u a + v a^\dagger, u^* a^\dagger + v^* a] \\
 &= u u^* [a, a^\dagger] + v v^* [a^\dagger, a] \\
 &= |u|^2 (1) + |v|^2 (-1) = |u|^2 - |v|^2
\end{align}
$$
因此，为了保持典范对易关系，系数必须满足约束条件：
$$
|u|^2 - |v|^2 = 1
$$
这个条件定义了 $SU(1,1)$ 群的元素。如果系数 $u$ 和 $v$ 是实数，这个条件简化为 $u^2 - v^2 = 1$，这使得我们可以方便地使用[双曲函数](@entry_id:165175)进行参数化，令 $u = \cosh(r)$ 和 $v = \sinh(r)$，其中 $r$ 是一个实数参数，通常被称为**压缩参数（squeezing parameter）**。

#### [对角化](@entry_id:147016)机制与稳定性

玻戈留波夫[变换的核](@entry_id:149509)心作用是消除[哈密顿量](@entry_id:172864)中的非对角项。考虑一个描述与环境发生二次相互作用的单[振动](@entry_id:267781)模式的典型[哈密顿量](@entry_id:172864)，例如在非[共振拉曼](@entry_id:202310)模型中出现的形式 [@problem_id:2768492]：
$$
H = \hbar \omega \left(a^{\dagger}a + \frac{1}{2}\right) + \frac{\hbar \lambda}{2}\left(a^{2} + a^{\dagger 2}\right)
$$
其中 $\omega$ 是[振动频率](@entry_id:199185)，$\lambda$ 是[耦合常数](@entry_id:747980)。这里的 $a^2$ 和 $a^{\dagger 2}$ 就是使[哈密顿量](@entry_id:172864)非对角的“反常”项。我们引入变换 $a = u c + v c^\dagger$（及其[厄米共轭](@entry_id:191215)），其中 $c$ 是新的[准粒子](@entry_id:136584)湮灭算符，目标是将 $H$ 化为 $H = \hbar \Omega (c^\dagger c + 1/2)$ 的形式。

将变换代入[哈密顿量](@entry_id:172864)，我们会发现 $c^2$ 和 $c^{\dagger 2}$ 的系数正比于 $2\omega uv + \lambda(u^2+v^2)$。为了实现对角化，我们必须令此系数为零。结合约束条件 $u^2 - v^2 = 1$（假设 $u,v$ 为实数），可以解出 $u$ 和 $v$ 的值，进而得到新的[准粒子能量](@entry_id:173936)（或有效频率）$\Omega$：
$$
\Omega = \sqrt{\omega^2 - \lambda^2}
$$
这个结果揭示了一个至关重要的物理概念：**稳定性（stability）**。为了使[准粒子能量](@entry_id:173936) $\Omega$ 为实数且为正（保证系统[基态](@entry_id:150928)稳定，能量有下界），[哈密顿量](@entry_id:172864)的参数必须满足 $\omega > |\lambda|$ [@problem_id:1100171]。如果这个条件不满足，$\Omega$ 将变为虚数，意味着系统存在指数增长的[不稳定模式](@entry_id:263056)，[哈密顿量](@entry_id:172864)所描述的二次[势能面](@entry_id:147441)不再是束缚的。

#### 新的[基态](@entry_id:150928)：[压缩真空](@entry_id:178766)

对角化后的[哈密顿量](@entry_id:172864) $H = \hbar \Omega (c^\dagger c + 1/2)$ 对应的[基态](@entry_id:150928) $|0_c\rangle$ 是[准粒子](@entry_id:136584)的真空态，即它被新的湮灭算符 $c$ 所湮灭：$c |0_c\rangle = 0$。然而，这个新的[基态](@entry_id:150928)与原始的“裸”真空 $|0_a\rangle$ (满足 $a|0_a\rangle=0$) 截然不同。

我们可以通过计算在[准粒子](@entry_id:136584)真空中原始粒子的平均数来理解这一点。为此，我们需要反向表示算符 $a$。由 $b = u a + v a^\dagger$ 和 $b^\dagger = u^* a^\dagger + v^* a$，我们可以解出逆变换为 $a = u^* b - v^* b^\dagger$。现在，计算[粒子数算符](@entry_id:153568) $N_a = a^\dagger a$ 在态 $|0_b\rangle$ 中的[期望值](@entry_id:153208) [@problem_id:468491] [@problem_id:1151324]：
$$
\langle 0_b | N_a | 0_b \rangle = \langle 0_b | a^\dagger a | 0_b \rangle = \langle 0_b | (u b^\dagger - v b)(u^* b - v^* b^\dagger) | 0_b \rangle
$$
利用 $b|0_b\rangle=0$ 和 $\langle 0_b | b^\dagger = 0$，展开后唯一不为零的项是包含 $b b^\dagger$ 的项：
$$
\langle N_a \rangle = \langle 0_b | (-v b)(-v^* b^\dagger) | 0_b \rangle = |v|^2 \langle 0_b | b b^\dagger | 0_b \rangle = |v|^2 \langle 0_b | (b^\dagger b + 1) | 0_b \rangle = |v|^2
$$
这个深刻的结果表明，相互作用系统的真实[基态](@entry_id:150928)（[准粒子](@entry_id:136584)真空）并非空无一物，而是充满了原始[玻色子](@entry_id:138266)的“虚”粒子对。系数 $v$ 的模方 $|v|^2$ 直接度量了[基态](@entry_id:150928)中这些粒子对的丰度。由于这种状态的某些物理量（如正交分量）的[量子涨落](@entry_id:154889)被“压缩”到低于真空涨落的水平，它通常被称为**[压缩真空态](@entry_id:195785)（squeezed vacuum state）**。

#### 多模系统与应用

玻戈留波夫变换在多模系统中展现了其强大的威力，最著名的例子包括弱[相互作用[玻色气](@entry_id:160184)体](@entry_id:155364)和[量子光学](@entry_id:140582)中的[双模压缩](@entry_id:183898)。

一个关键应用是描述**[弱相互作用](@entry_id:157579)的玻色-爱因斯坦凝聚（Bose-Einstein Condensate, BEC）**。在 Bogoliubov 近似下，对于动量 $\mathbf{k} \neq 0$ 的激发，其有效哈密顿量为 [@problem_id:1218669]：
$$
H = \sum_{\mathbf{k} \neq 0} \left[ (\epsilon_k + n_0 U_0) a_{\mathbf{k}}^\dagger a_{\mathbf{k}} + \frac{n_0 U_0}{2} ( a_{\mathbf{k}}^\dagger a_{-\mathbf{k}}^\dagger + a_{\mathbf{k}} a_{-\mathbf{k}} ) \right]
$$
其中 $\epsilon_k = \hbar^2 k^2 / 2m$ 是单粒子动能，$n_0 U_0$ 代表与凝聚体相互作用的能量。通过引入变换 $a_{\mathbf{k}} = u_k \alpha_{\mathbf{k}} - v_k \alpha_{-\mathbf{k}}^\dagger$，并选择合适的 $u_k, v_k$（或它们的比值 $x_k = v_k/u_k$）来消除反常项，我们得到的[准粒子能量](@entry_id:173936)为著名的**玻戈留波夫色散关系**：
$$
E_k = \sqrt{\epsilon_k (\epsilon_k + 2n_0 U_0)}
$$
在小动量极限下 ($k \to 0$)，$E_k \approx \hbar c k$，其中 $c = \sqrt{n_0 U_0 / m}$ 是声速。这表明系统的低能[元激发](@entry_id:140859)是无质量的[声子](@entry_id:140728)，而不是具有二次色散关系的[自由粒子](@entry_id:148748)。这种从有质量粒子构成的系统中涌现出无质量[集体激发](@entry_id:145026)的现象是[多体物理学](@entry_id:144526)中的一个核心主题。

在新的[基态](@entry_id:150928)中，一个重要的物理量是**反常关联函数（anomalous correlation function）** $\langle a_{\mathbf{k}} a_{-\mathbf{k}} \rangle$。它的非零值是系统[基态](@entry_id:150928)具有相干配对的直接证据。通过计算可以得到 $\langle a_{\mathbf{k}} a_{-\mathbf{k}} \rangle = -u_k v_k$ [@problem_id:1100168]，这表明[基态](@entry_id:150928)中存在着动量相反的粒子对的稳定关联。

另一个重要的例子是**[双模压缩真空态](@entry_id:147759)（two-mode squeezed vacuum, TMSV）**，它由[哈密顿量](@entry_id:172864) $H = \epsilon (b_1^\dagger b_1 + b_2^\dagger b_2) + g (b_1^\dagger b_2^\dagger + b_2 b_1)$ 的[基态](@entry_id:150928)给出 [@problem_id:1205778]。这个[基态](@entry_id:150928)可以通过在真空态 $|0,0\rangle$ 上作用一个[双模压缩](@entry_id:183898)算符 $S_2(r) = \exp(r(a_1^\dagger a_2^\dagger - a_1 a_2))$ 来产生。该状态在 Fock 基下可以展开为 [@problem_id:1100165]：
$$
|\psi(r)\rangle = \frac{1}{\cosh r} \sum_{n=0}^\infty (\tanh r)^n |n,n\rangle
$$
这个形式清晰地表明，TMSV 态是两个模式之间高度纠缠的状态：测量模式1发现有 $n$ 个粒子，必然会在模式2中也发现 $n$ 个粒子。这种纠缠的强度随压缩参数 $r$ 的增大而增强，可以通过**[对数负性](@entry_id:137607)（logarithmic negativity）**等[纠缠度量](@entry_id:139894)来量化 [@problem_id:1100165]。此外，如果只观察其中一个模式，其[约化密度矩阵](@entry_id:146315)表现为一个[平均粒子数](@entry_id:151202)为 $\langle n \rangle = \sinh^2(r)$ 的[热态](@entry_id:199977)，这进一步说明了纠缠的深刻影响 [@problem_id:1100130]。

#### 相空间图像与辛变换

[玻色子](@entry_id:138266)的玻戈留波夫变换在相空间中有一个优美的几何解释。我们可以引入一对**正交算符（quadrature operators）** $\hat{q} = \frac{1}{\sqrt{2}}(a+a^\dagger)$ 和 $\hat{p} = \frac{i}{\sqrt{2}}(a^\dagger-a)$，它们分别对应于[经典谐振子](@entry_id:153404)的位置和动量。这些算符满足[对易关系](@entry_id:136780) $[\hat{q}, \hat{p}] = i$。

一个玻戈留波夫变换等价于在由所有模式的正交算符构成的相空间中进行一次[线性变换](@entry_id:149133)。例如，对于一个双模系统，变换作用在向量 $\mathbf{r} = (x_a, p_a, x_b, p_b)^T$ 上，形式为 $\mathbf{r}' = S\mathbf{r}$，其中 $S$ 是一个实的 $4 \times 4$ 矩阵 [@problem_id:1100116]。保持量子力学基本对易关系的要求，等价于要求矩阵 $S$ 是一个**[辛矩阵](@entry_id:142706)（symplectic matrix）**。对于 $2 \times 2$ 的单模情况，这个条件简化为 $\det(S)=1$ [@problem_id:1100118]。

这种观点将抽象的算符变换与相空间中的几何操作（如旋转、压缩、剪切）联系起来。例如，单模压缩操作对应于在相空间中沿某个方向压缩不确定性椭圆，同时在正交方向上拉伸它。连续进行两次变换（如两次不同方向的压缩）在数学上就对应于两个[辛矩阵](@entry_id:142706)的乘积 $S_{tot} = S_2 S_1$ [@problem_id:1100118]。

### [费米子](@entry_id:146235)玻戈留波夫变换

对于[费米子](@entry_id:146235)系统，玻戈留波夫变换同样旨在对角化二次型[哈密顿量](@entry_id:172864)，但其[代数结构](@entry_id:137052)和物理应用与[玻色子](@entry_id:138266)情况有显著区别。最典型的应用是在**BCS（Bardeen-Cooper-Schrieffer）超导理论**中。

#### 典范[反对易关系](@entry_id:153815)的保持

考虑一个[费米子](@entry_id:146235)系统，其算符满足**典范[反对易关系](@entry_id:153815)（Canonical Anticommutation Relations, CAR）**：$\{c_i, c_j^\dagger\} = \delta_{ij}$ 且 $\{c_i, c_j\} = \{c_i^\dagger, c_j^\dagger\} = 0$。一个典型的[费米子](@entry_id:146235)玻戈留波夫变换混合了粒子和空穴的算符，例如：
$$
\gamma_k = u_k c_k + v_k c_{-k}^\dagger
$$
其中 $\gamma_k$ 是新的[准粒子](@entry_id:136584)（通常称为“玻戈留邦”）的[湮灭算符](@entry_id:165390)。为了使 $\gamma_k$ 描述一个合法的[费米子](@entry_id:146235)，它必须满足 CAR。我们来检验一下：
$$
\{\gamma_k, \gamma_k^\dagger\} = \{u_k c_k + v_k c_{-k}^\dagger, u_k^* c_k^\dagger + v_k^* c_{-k}\} = |u_k|^2 \{c_k, c_k^\dagger\} + |v_k|^2 \{c_{-k}^\dagger, c_{-k}\}
$$
利用 $\{c_{-k}^\dagger, c_{-k}\} = 1 - \{c_{-k}, c_{-k}^\dagger\} = 1$，我们得到：
$$
\{\gamma_k, \gamma_k^\dagger\} = |u_k|^2 + |v_k|^2
$$
为了让 $\{\gamma_k, \gamma_k^\dagger\} = 1$，系数必须满足：
$$
|u_k|^2 + |v_k|^2 = 1
$$
这是一个幺正条件，与[玻色子](@entry_id:138266)情况下的双曲约束 $|u|^2 - |v|^2 = 1$ 形成鲜明对比。这个条件意味着变换系数 $(u_k, v_k)$ 可以被看作是二维[复向量空间](@entry_id:264355)中的一个[单位向量](@entry_id:165907)，可以用角度[参数化](@entry_id:272587)，如 $u_k = \cos\theta_k, v_k = \sin\theta_k e^{i\phi_k}$。这个幺正约束反映了[费米子](@entry_id:146235)系统的[泡利不相容原理](@entry_id:141850)——每个[量子态](@entry_id:146142)最多只能容纳一个[费米子](@entry_id:146235)。

#### 对角化与[BCS模型](@entry_id:746672)

BCS [平均场哈密顿量](@entry_id:751814)是[费米子](@entry_id:146235)玻戈留波夫变换的经典应用舞台 [@problem_id:1100117]：
$$
H = \sum_{k} \xi_k (c_{k\uparrow}^\dagger c_{k\uparrow} + c_{-k\downarrow}^\dagger c_{-k\downarrow}) - \sum_k \Delta (c_{k\uparrow}^\dagger c_{-k\downarrow}^\dagger + c_{-k\downarrow} c_{k\uparrow})
$$
这里 $\xi_k$ 是相对于[费米能级](@entry_id:143215)的单电子能量，$\Delta$ 是超导能隙参数。$\Delta$ 项耦合了动量和自旋相反的电子对（[库珀对](@entry_id:143370)），使[哈密顿量](@entry_id:172864)非对角。我们引入变换（为方便通常选择 $u_k, v_k$ 为实数）：
$$
\gamma_{k\uparrow} = u_k c_{k\uparrow} - v_k c_{-k\downarrow}^\dagger \\
\gamma_{-k\downarrow} = v_k c_{k\uparrow}^\dagger + u_k c_{-k\downarrow}
$$
通过选择合适的 $u_k, v_k$ 来消除 $H$ 中的反常项，可以得到[对角化](@entry_id:147016)的[哈密顿量](@entry_id:172864) $H = E_0 + \sum_k E_k (\gamma_{k\uparrow}^\dagger \gamma_{k\uparrow} + \gamma_{-k\downarrow}^\dagger \gamma_{-k\downarrow})$。这里的[准粒子能量](@entry_id:173936)为：
$$
E_k = \sqrt{\xi_k^2 + \Delta^2}
$$
这个能量谱具有一个最小值为 $\Delta$ 的[能隙](@entry_id:191975)，这正是[超导体](@entry_id:191025)的标志性特征。相应的变换系数由下式给出 [@problem_id:1100140]：
$$
u_k^2 = \frac{1}{2} \left(1 + \frac{\xi_k}{E_k}\right), \quad v_k^2 = \frac{1}{2} \left(1 - \frac{\xi_k}{E_k}\right)
$$

#### [BCS基态](@entry_id:136275)与物理诠释

BCS [基态](@entry_id:150928) $|\Psi_{GS}\rangle$ 是所有[准粒子](@entry_id:136584)的真空态，即 $\gamma_{k\sigma} |\Psi_{GS}\rangle = 0$。与[玻色子](@entry_id:138266)情况类似，这个[基态](@entry_id:150928)在原始电子表象下具有复杂的结构。我们可以通过计算各种物理量的[期望值](@entry_id:153208)来理解其性质。

首先，[基态](@entry_id:150928)中的电子占据数 $\langle c_{k\sigma}^\dagger c_{k\sigma} \rangle$ 可以通过反转玻戈留波夫变换（例如 [@problem_id:198372]）得到。反向变换为 $c_{k\uparrow} = u_k \gamma_{k\uparrow} + v_k \gamma_{-k\downarrow}^\dagger$。计算可得 [@problem_id:1100117]：
$$
\langle \Psi_{GS} | c_{k\sigma}^\dagger c_{k\sigma} | \Psi_{GS} \rangle = v_k^2 = \frac{1}{2} \left(1 - \frac{\xi_k}{\sqrt{\xi_k^2 + \Delta^2}}\right)
$$
这个结果表明，在 $T=0$ 的超导态中，费米面被“模糊”了。在正常金属中，$v_k^2$ 在[费米面](@entry_id:137798)处从1突变为0。而在[超导体](@entry_id:191025)中，它在一个能量范围 $\sim\Delta$ 内平滑地从1过渡到0。

其次，类似于[玻色子](@entry_id:138266)系统，BCS [基态](@entry_id:150928)中存在非零的**反常关联**，即库珀对的振幅 [@problem_id:1100144]：
$$
\langle \Psi_{GS} | c_{k\uparrow}^\dagger c_{-k\downarrow}^\dagger | \Psi_{GS} \rangle = u_k v_k = \frac{\Delta}{2E_k} = \frac{\Delta}{2\sqrt{\xi_k^2 + \Delta^2}}
$$
这个[期望值](@entry_id:153208)不为零，是超导相破缺 $U(1)$ 规范对称性的序参量。

**[相干因子](@entry_id:147178)** $u_k$ 和 $v_k$ 具有深刻的物理意义，并直接与实验测量相关联。在[扫描隧道谱](@entry_id:157738)（STS）实验中，人们测量从金属针尖隧穿进入或流出[超导体](@entry_id:191025)的电子的[微分](@entry_id:158718)[电导](@entry_id:177131) $dI/dV$。在零温下，这直接探测了[超导体](@entry_id:191025)的单粒子谱函数 [@problem_id:2973224]。
- 当施加正偏压 ($V>0$) 时，电子从针尖隧穿到[超导体](@entry_id:191025)的空态，这个过程的[谱权重](@entry_id:144751)（即 $dI/dV$ 的强度）正比于 $|u_k|^2$。
- 当施加负偏压 ($V<0$) 时，电子从[超导体](@entry_id:191025)的占据态隧穿到针尖，这个过程的[谱权重](@entry_id:144751)正比于 $|v_k|^2$。

因此，$|u_k|^2$ 度量了能量为 $E_k$ 的[准粒子激发](@entry_id:138475)所包含的“电子”成分（添加一个电子），而 $|v_k|^2$ 度量了其“空穴”成分（移走一个电子）。对于 $\xi_k > 0$（[费米能级](@entry_id:143215)以上的态），$|u_k|^2 > |v_k|^2$，态更像电子；对于 $\xi_k < 0$（[费米能级](@entry_id:143215)以下的态），$|v_k|^2 > |u_k|^2$，态更像空穴。这为抽象的[相干因子](@entry_id:147178)提供了具体、可测量的物理图像。

#### 矩阵形式与[一般性](@entry_id:161765)质

对于一个具有 $N$ 个模式的费米系统，玻戈留波夫变换可以用**南布（Nambu）自旋量**和矩阵来统一描述。定义列向量 $\mathbf{c} = (c_1, \dots, c_N)^T$ 和 $\mathbf{b} = (b_1, \dots, b_N)^T$，变换可以写作：
$$
\begin{pmatrix} \mathbf{b} \\ \mathbf{b}^\dagger \end{pmatrix} = \begin{pmatrix} U  V \\ V^*  U^* \end{pmatrix} \begin{pmatrix} \mathbf{c} \\ \mathbf{c}^\dagger \end{pmatrix} = W \begin{pmatrix} \mathbf{c} \\ \mathbf{c}^\dagger \end{pmatrix}
$$
其中 $U$ 和 $V$ 是 $N \times N$ [复矩阵](@entry_id:190650)，$W$ 是一个 $2N \times 2N$ 的[变换矩阵](@entry_id:151616) [@problem_id:1101214]。保持 CAR 的要求给出了矩阵 $U, V$ 必须满足的普适约束条件：
1. $UU^\dagger + VV^\dagger = I$
2. $UV^T + VU^T = 0$

这些条件保证了 $W$ 是一个幺[正矩阵](@entry_id:149490)，即 $W W^\dagger = I$。幺正[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)是一个模为1的复数。进一步可以证明，对于所有与[恒等变换](@entry_id:264671)连续相通的玻戈留波夫变换，其[行列式](@entry_id:142978)恒为1 [@problem_id:407379] [@problem_id:991455] [@problem_id:1101214]。在[费米路径积分](@entry_id:146778)中，这个性质意味着变换的雅可比行列式（即 Berezinian）为1，这极大地简化了理论计算。

### 总结

玻戈留波夫变换是[多体量子理论](@entry_id:202614)中一个核心且强大的工具。无论是用于[玻色子](@entry_id:138266)还是[费米子](@entry_id:146235)系统，它的本质都是通过混合原始粒子的产生和湮灭算符来找到系统的真正[元激发](@entry_id:140859)——[准粒子](@entry_id:136584)。这个过程将一个复杂的、相互作用的[哈密顿量对角化](@entry_id:139738)，从而揭示出系统的激发谱和真实[基态](@entry_id:150928)的结构。

- **对于[玻色子](@entry_id:138266)**，变换受双曲约束 $|u|^2 - |v|^2 = 1$ 的制约，反映了粒子数不守恒但可以任意多的特性。其结果是一个充满了原始粒子对的“[压缩真空](@entry_id:178766)”[基态](@entry_id:150928)，并由此解释了 BEC 中的[声子](@entry_id:140728)激发和[量子光学](@entry_id:140582)中的[纠缠态](@entry_id:152310)等现象。

- **对于[费米子](@entry_id:146235)**，变换受幺正约束 $|u|^2 + |v|^2 = 1$ 的制约，与[泡利不相容原理](@entry_id:141850)一致。它成功地解释了[BCS超导理论](@entry_id:145811)中的[能隙](@entry_id:191975)、[准粒子激发](@entry_id:138475)以及一个被[库珀对](@entry_id:143370)占据的复杂[基态](@entry_id:150928)。

通过理解玻戈留波夫变换的原理和机制，我们能够深入洞察从超流、超导到宇宙学等广泛物理领域中相互作用系统的集体行为和[涌现现象](@entry_id:145138)。