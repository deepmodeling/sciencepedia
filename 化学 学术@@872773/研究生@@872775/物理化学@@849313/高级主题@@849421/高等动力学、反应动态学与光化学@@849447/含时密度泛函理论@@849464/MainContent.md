## 引言
电子激发态是光化学、[光物理学](@entry_id:202751)、[材料科学](@entry_id:152226)和生物学等众多领域的核心。理解分子和材料如何与光相互作用，以及激发后会发生什么，对于设计新型[太阳能电池](@entry_id:138078)、发光器件、荧光探针乃至理解视觉等基本生命过程至关重要。然而，从第一性原理精确求解多电子体系的[含时薛定谔方程](@entry_id:137898)在计算上是极其严峻的挑战。[含时密度泛函理论](@entry_id:200019)（Time-dependent Density Functional Theory, TD-DFT）应运而生，它通过将问题核心从极其复杂的[多体波函数](@entry_id:203043)转向更易于处理的电子密度，为研究[电子激发](@entry_id:190531)和动力学提供了一条兼具理论严谨性和计算可行性的高效途径。

本文旨在系统性地介绍TD-DFT的理论框架、应用范畴及其内在局限。在第一部分“原理与机制”中，我们将深入探讨支撑整个理论的[Runge-Gross定理](@entry_id:272222)，介绍实用的含时[Kohn-Sham方法](@entry_id:263733)，并详细解释在线性响应框架下用于计算[激发光谱](@entry_id:139562)的[Casida方程](@entry_id:183031)及其关键的[绝热近似](@entry_id:143074)。随后，在“应用与交叉学科联系”部分，我们将展示TD-DFT如何作为一座桥梁，连接理论与实验，应用于预测各类[电子光谱](@entry_id:154403)、模拟[光物理过程](@entry_id:154565)、探索材料光学性质，并触及生物化学和[强场物理](@entry_id:198469)等前沿领域。最后，通过“动手实践”部分，读者将有机会通过具体的计算问题，亲身体验和理解TD-DFT的关键概念和挑战。通过这三部分的学习，读者将能够全面掌握TD-DFT这一现代[计算化学](@entry_id:143039)中的强大工具。

## 原理与机制

### 基本原理：Runge-Gross 定理

[量子化学](@entry_id:140193)的核心目标是求解相互作用粒子体系的[含时薛定谔方程](@entry_id:137898)。对于任何超出最简[单体](@entry_id:136559)系的系统，直接求解[多体波函数](@entry_id:203043) $\Psi(\mathbf{r}_1, \dots, \mathbf{r}_N, t)$ 在计算上是不可行的。[含时密度泛函理论 (TD-DFT)](@entry_id:192176) 通过将问题重构为处理一个简单得多的量——[单体](@entry_id:136559)电子密度 $n(\mathbf{r}, t)$，提供了一条替代路径。这一整个方法的理论合法性建立在 **Runge-Gross (RG) 定理**之上，该定理在含时外势和含时电子密度之间建立了一个形式上精确的映射。

该定理可以精确地表述如下：对于一个从固定初始态 $\Psi_0$ 在时间 $t_0$ 开始演化的多体系统，一个给定的含时密度 $n(\mathbf{r}, t)$ 最多只能由一个含时外势 $v(\mathbf{r}, t)$ 产生，两者之差最多为一个纯粹与时间相关的函数 [@problem_id:2683009]。换句话说，如果两个外势 $v(\mathbf{r}, t)$ 和 $v'(\mathbf{r}, t)$ 从相同的初始态 $\Psi_0$ 出发，产生了相同的密度演化 $n(\mathbf{r}, t)$，那么它们最多只能相差一个空间均匀、仅与时间相关的函数 $c(t)$：

$v'(\mathbf{r}, t) = v(\mathbf{r}, t) + c(t)$

该定理成立的条件是，势在初始时间 $t_0$ 附近是可进行泰勒展开的。其证明依赖于考察在 $t_0$ 时刻密度的各阶时间导数，这些导数通过量子力学[运动方程](@entry_id:170720)与势相关联。

这种由 $c(t)$ 代表的“规范自由度”的存在是量子力学的基本结果。在[哈密顿量](@entry_id:172864) $\hat{H}(t)$ 中加入一个空间均匀的势 $c(t)$，只会增加一个能量项 $c(t)\hat{N}$，其中 $\hat{N}$ 是[粒子数算符](@entry_id:153568)。对于一个电子数 $N$ 固定的系统，这会导致总[波函数](@entry_id:147440)上附加一个额外的含时相位因子：

$\Psi'(t) = \exp\left(-\frac{i}{\hbar} N \int_{t_0}^t c(\tau) d\tau\right) \Psi(t)$

由于电子密度是这样计算的 $n(\mathbf{r}, t) = \langle\Psi(t)|\hat{n}(\mathbf{r})|\Psi(t)\rangle$，这个[全局相位](@entry_id:147947)因子会抵消掉，使得密度保持不变 [@problem_id:2932867]。因此，等价类 $\{v(\mathbf{r}, t) + c(t)\}$ 中的所有势都会产生相同的物理密度。

Runge-Gross 定理的深刻含义在于，含时密度 $n(\mathbf{r}, t)$ 唯一地决定了外势（在相差一个平凡的 $c(t)$ 的意义上）。因为势又决定了[哈密顿量](@entry_id:172864)，而[哈密顿量](@entry_id:172864)支配着[波函数](@entry_id:147440)的演化，所以[波函数](@entry_id:147440)本身也是密度和初始态的一个唯一泛函：$\Psi(t) = \Psi[n; \Psi_0]$。因此，原则上系统的任何可观测量都是含时密度的泛函。这确立了密度作为描述[量子动力学](@entry_id:138183)的有效基本变量的地位。

### 含时 Kohn-Sham 方法

Runge-Gross 定理是一个原理性证明；它没有提供直接计算密度或其泛函的方法。TD-DFT 的实际实现依赖于 **Kohn-Sham (KS) 构建**。其中心思想是引入一个虚拟的无相互作用电子体系，该体系通过设计可以重现真实的相互作用体系的精确含时密度 $n(\mathbf{r}, t)$。

这些无相互作用的 KS 电子遵循一组单粒子含时类薛定谔方程进行演化，称为**含时 Kohn-Sham (TDKS) 方程** [@problem_id:2932867]：

$i\hbar \frac{\partial}{\partial t} \phi_p(\mathbf{r}, t) = \left[ -\frac{\hbar^2}{2m_e}\nabla^2 + v_{\text{s}}(\mathbf{r}, t) \right] \phi_p(\mathbf{r}, t)$

这个虚拟体系的密度等于真实的相互作用密度，由占据的 KS [轨道](@entry_id:137151)求和给出：$n(\mathbf{r}, t) = \sum_{p=1}^{N} |\phi_p(\mathbf{r}, t)|^2$。

此构建的关键在于有效的[单体](@entry_id:136559)势 $v_{\text{s}}(\mathbf{r}, t)$，即 KS 势。它的定义方式使得 KS 密度等于真实密度。KS 势在形式上可分解为三个部分：

$v_{\text{s}}(\mathbf{r}, t) = v_{\text{ext}}(\mathbf{r}, t) + v_{\text{H}}[n](\mathbf{r}, t) + v_{\text{xc}}[n; \Psi_0, \Phi_0](\mathbf{r}, t)$

这里，$v_{\text{ext}}(\mathbf{r}, t)$ 是作用于真实系统的相同外势（例如，来自[原子核](@entry_id:167902)和任何外场的势）。第二项 $v_{\text{H}}[n](\mathbf{r}, t)$ 是**Hartree 势**，它描述了电子密度自身产生的经典静电排斥：

$v_{\text{H}}[n](\mathbf{r}, t) = e^2 \int \frac{n(\mathbf{r}', t)}{4\pi\epsilon_0|\mathbf{r}-\mathbf{r}'|} d\mathbf{r}'$

这是一个密度的瞬时泛函。第三项 $v_{\text{xc}}(\mathbf{r}, t)$ 是**交换相关 (XC) 势**。这是所有未被无相互作用动能和经典 Hartree 排斥所包含的复杂[多体效应](@entry_id:173569)的集合。它包含了所有量子力学的交换和关联效应。

精确的 XC 势具有两个在实践中常被简化的关键性质。首先，它依赖于密度的历史信息 $\{n(\mathbf{r}', t')\}_{t' \le t}$，这一特性称为**记忆效应**。其次，它依赖于相互作用系统 $\Psi_0$ 和 KS 系统 $\Phi_0$ 的初始态 [@problem_id:2932867]。TD-DFT 的挑战在于为这个未知的、复杂的泛函找到精确且计算上可行的近似。

### 线性响应 TD-DFT 与[激发光谱](@entry_id:139562)

对于许多应用，例如计算[电子吸收光谱](@entry_id:269577)，我们感兴趣的是系统如何响应一个微弱的、含时的微扰，例如光的[振荡](@entry_id:267781)[电场](@entry_id:194326)。在这种情况下，我们可以使用**[线性响应理论](@entry_id:145737)**。密度的诱导变化 $\delta n(\mathbf{r}, t)$ 与外势的变化 $\delta v_{\text{ext}}(\mathbf{r}, t)$ 成线[性比](@entry_id:172643)例。这种关系定义了**相互作用体系的密度-密度[响应函数](@entry_id:142629)** $\chi$：

$\delta n(\mathbf{r}, t) = \int \int \chi(\mathbf{r}, t; \mathbf{r}', t') \delta v_{\text{ext}}(\mathbf{r}', t') d\mathbf{r}' dt'$

形式上，$\chi$ 是泛函导数 $\chi \equiv \delta n / \delta v_{\text{ext}}$ [@problem_id:2683041]。此响应函数在[频域](@entry_id:160070) $\chi(\omega)$ 的极点对应于系统的电子激发能。

在 KS 框架中，我们可以类似地定义一个**Kohn-Sham 响应函数** $\chi_s$，它描述了无相互作用 KS 系统对 KS 势变化的响应：$\chi_s \equiv \delta n / \delta v_s$。

真实（相互作用）和虚拟（无相互作用）系统之间的关键联系由一个类[戴森方程](@entry_id:146246)给出，该方程关联了它们各自的响应函数。在[频域](@entry_id:160070)中，该方程为 [@problem_id:2683041]：

$\chi(\omega) = \chi_s(\omega) + \chi_s(\omega) \left( f_{\text{H}} + f_{\text{xc}}(\omega) \right) \chi(\omega)$

这里，括号中的项代表**响应核**。第一项 $f_{\text{H}}(\mathbf{r}, \mathbf{r}') = e^2 / (4\pi\epsilon_0|\mathbf{r}-\mathbf{r}'|)$ 是**Hartree 核**，代表[瞬时库仑相互作用](@entry_id:196309)。第二项 $f_{\text{xc}}(\mathbf{r}, \mathbf{r}', \omega) \equiv \delta v_{\text{xc}} / \delta n$ 是**[交换相关核](@entry_id:195258)**。其物理作用是将所有量子力学的交换和关联效应纳入到一个被激发的电子与其留下的空穴之间的有效相互作用中 [@problem_id:1417521]。

这个方程提供了一个强大的物理图像 [@problem_id:1417502]。相互作用系统的总响应 $\chi$ 不仅仅是独立 KS 粒子的响应 $\chi_s$。相反，KS 响应被由诱导密度本身产生的内场所修正或“屏蔽”。项 $\chi_s (f_{\text{H}} + f_{\text{xc}}) \chi$ 代表了这种屏蔽。对于一个受到静态或低频[电场](@entry_id:194326)作用的稳定分子，这种屏蔽效应与外场相反，导致总响应减小。例如，用完整 TD-DFT 计算的极化率 $\alpha_{\text{TDDFT}}$ 通常小于裸 KS 系统的假想[极化率](@entry_id:143513) $\alpha_{\text{KS}}$ [@problem_id:1417502]。

### [绝热近似](@entry_id:143074)与 Casida 方程

精确的含频 XC 核 $f_{\text{xc}}(\omega)$ 是未知的。在实际的 TD-DFT 计算中，最常见和最基础的近似是**[绝热近似](@entry_id:143074)**。该近似忽略了 XC 势中的[记忆效应](@entry_id:266709)，假设它对密度的变化做出瞬时响应。形式上，依赖于历史的 $v_{\text{xc}}$ 被替换为在瞬时含时密度下求值的[基态](@entry_id:150928) XC 泛函 [@problem_id:2826134]：

$v_{\text{xc}}^{\text{A}}[n](\mathbf{r}, t) \equiv v_{\text{xc}}^{\text{gs}}[n(\cdot, t)](\mathbf{r})$

这一假设对 XC 核有直接影响：它变得与频率无关。时域中的核呈现为时间上的狄拉克 δ 函数形式，反映了其瞬时性：

$f_{\text{xc}}^{\text{A}}(\mathbf{r}, \mathbf{r}', t-t') = \delta(t-t') \left. \frac{\delta^2 E_{\text{xc}}^{\text{gs}}[n]}{\delta n(\mathbf{r}) \delta n(\mathbf{r}')} \right|_{n=n_0}$

在[绝热近似](@entry_id:143074)下，用于寻找 $\chi(\omega)$ 极点的类[戴森方程](@entry_id:146246)可以重写为一个矩阵[本征值问题](@entry_id:142153)，通常称为 **Casida 方程** [@problem_id:2683010] [@problem_id:1417554]。在其[标准形式](@entry_id:153058)下，这些方程写为：

$\begin{pmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B}^* & \mathbf{A}^* \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix} = \omega \begin{pmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & -\mathbf{1} \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix}$

这里，$\omega$ 是所求的[激发能](@entry_id:190368)。向量 $\mathbf{X}$ 和 $\mathbf{Y}$ 分别包含了[粒子-空穴激发](@entry_id:137289)（例如，从占据的 KS [轨道](@entry_id:137151) $i$ 到虚拟的 KS [轨道](@entry_id:137151) $a$）和退激发的振幅。矩阵 $\mathbf{A}$ 和 $\mathbf{B}$ 由[基态](@entry_id:150928) KS [轨道](@entry_id:137151)能和绝热核 $f_{\text{H}} + f_{\text{xc}}^{\text{A}}$ 在 KS [轨道](@entry_id:137151)上的积分构成。

这些矩阵的物理作用是不同的 [@problem_id:1417554]。
- **A** 矩阵描述了不同单粒子激发之间的耦合。其对角元素是 KS [轨道](@entry_id:137151)能之差 ($\epsilon_a - \epsilon_i$)，代表了对[激发能](@entry_id:190368)的零阶猜测。其非对角元素混合了不同的粒子-空穴对。
- **B** 矩阵描述了激发和退激发过程之间的耦合。该项源于[基态](@entry_id:150928)不是精确的 [Hartree-Fock](@entry_id:142303) [行列式](@entry_id:142978)，并且对于满足某些理论求和规则至关重要。忽略 $\mathbf{B}$ 矩阵（令 $\mathbf{B}=\mathbf{0}$）会导致一个简化的理论，即 Tamm-Dancoff 近似 (TDA)。

求解这个[本征值问题](@entry_id:142153)可以得到各种体系的激发能和[激发态](@entry_id:261453)特征。

### 绝热 TD-DFT 的能力与局限

[绝热近似](@entry_id:143074)与标准[基态](@entry_id:150928) XC 泛函（如局域密度近似，LDAs，或[广义梯度近似](@entry_id:274118)，GGAs）的结合已被证明是一个强大的工具，成功预测了分子中许多低能价层激发。然而，其内在的假设导致了一些众所周知、系统性的失败。

#### 对[电荷转移激发](@entry_id:174772)的失败

使用局域或半局域泛函的绝热 TD-DFT 在处理**电荷转移 (CT) 激发**时会遭遇戏剧性的失败，即电子从分子的给体区域移动到受体区域很长一段距离。计算出的 CT [激发能](@entry_id:190368)通常被严重低估 [@problem_id:1417509]。这一失败的根本原因在于从中推导出绝[热核](@entry_id:172041)的[基态](@entry_id:150928) XC 势 $v_{\text{xc}}^{\text{gs}}$ 具有不正确的[渐近行为](@entry_id:160836)。对于局域泛函，$v_{\text{xc}}^{\text{gs}}$ 随距离呈指数衰减，而不是正确的库仑 $-1/r$ 行为。因此，该理论无法描述最终 CT 态中相距遥远的[电子和空穴](@entry_id:274534)之间的长程库仑吸引。这种缺失的吸引能导致[激发能](@entry_id:190368)被严重低估。

#### 无法描述双激发

另一个基本局限是绝热 TD-DFT 无法描述具有显著**双激发特征**的电子态（即，相对于[基态](@entry_id:150928)，主要由双粒子-双空穴组态的叠加构成的态）[@problem_id:2932911]。[线性响应](@entry_id:146180) TD-DFT 的整个形式都是建立在无相互作用 KS 系统的响应 $\chi_s$ 之上的，而 $\chi_s$ 按其性质只在单粒子激发能处有极点。与频率无关的绝[热核](@entry_id:172041)只能混合和移动这些单激发极点，它没有机制在对应于双激发的能量处创造出全新的极点。为了捕捉这类态，必须超越[绝热近似](@entry_id:143074)，使用一个含频的 XC 核 $f_{\text{xc}}(\omega)$。如果 $f_{\text{xc}}(\omega)$ 本身在双激发能附近具有正确的极点结构或频率急剧变化的特性，它就能在完整的相互作用[响应函数](@entry_id:142629) $\chi(\omega)$ 中诱导出正确的极点。开发这类[核函数](@entry_id:145324)，以及解决 CT 问题的泛函，仍然是现代密度泛函理论中一个活跃而富有挑战性的前沿领域。