## 引言
在现代量子物理学中，通过外部场对量子系统进行周期性驱动，已成为一种探索和操控物质的强大[范式](@entry_id:161181)。从根本上改变材料的电子特性到创造全新的物质形态，周期性驱动为我们打开了一扇通往非平衡量子世界的大门。然而，理解和预测这些受驱动系统的复杂动力学行为，需要一个坚实的理论框架。[Floquet理论](@entry_id:146392)正是为此而生，它为分析具有周期性[含时哈密顿量](@entry_id:136684)的量子系统提供了必不可少的数学语言和物理图像。本文旨在系统性地介绍[Floquet理论](@entry_id:146392)及其在多体物理中的前沿应用，解决的核心问题是：我们如何精确描述、控制并利用周期性驱动来设计具有新奇性质的量子系统？

为实现这一目标，本文将分为三个核心部分。首先，在“原理与机制”一章中，我们将深入[Floquet理论](@entry_id:146392)的数学心脏，阐明[Floquet定理](@entry_id:175204)、准[能谱](@entry_id:181780)以及频闪演化的基本概念。接着，我们将探讨[Floquet工程](@entry_id:139713)的两种主要技术——[高频展开](@entry_id:139399)和共振驱动，揭示它们如何让我们随心所欲地“雕刻”量子[哈密顿量](@entry_id:172864)。随后，在“应用与跨学科联系”一章，我们将展示这些理论工具的强大威力，通过一系列实例，从[动态稳定](@entry_id:173587)化和隧穿调控，到人工[规范场](@entry_id:159627)和[合成维度](@entry_id:172625)，再到最前沿的Floquet拓扑[物态](@entry_id:139436)和[离散时间晶体](@entry_id:136742)，描绘出一幅幅由周期性驱动创造的奇异物理图景。最后，通过“动手实践”部分的具体计算问题，读者将有机会亲手应用所学知识，加深对[Floquet工程](@entry_id:139713)核心思想的理解。本文将带领您穿越从基础理论到尖端应用的完整旅程，揭示周期性驱动如何成为开启非平衡量子现象宝库的钥匙。

## 原理与机制

在研究受周期性驱动的量子系统时，Floquet 理论提供了一个必不可少的理论框架。本章旨在系统地阐述该理论的核心原理与关键机制。我们将从描述周期性[系统动力学](@entry_id:136288)的基本数学结构出发，探讨准[能谱](@entry_id:181780)和频闪演化的概念。随后，我们将深入研究 Floquet 工程的强大工具，包括[高频展开](@entry_id:139399)和共振驱动下的[旋转波近似](@entry_id:204016)，这些工具使得通过外部驱动来设计和控制量子[哈密顿量](@entry_id:172864)成为可能。最后，我们将把这些概念应用于多体系统，探讨诸如加热、[预热化](@entry_id:147591)以及[离散时间晶体](@entry_id:136742)等引人入胜的[非平衡现象](@entry_id:198484)。

### Floquet 定理：准能与频闪演化

我们考虑一个由[含时哈密顿量](@entry_id:136684) $H(t)$ 描述的量子系统，该[哈密顿量](@entry_id:172864)以周期 $T$ 作周期性变化，即 $H(t+T) = H(t)$。系统的演化由[含时薛定谔方程](@entry_id:137898)支配（除非另有说明，我们采用 $\hbar=1$ 的单位制）：
$$
i \frac{d}{dt} |\psi(t)\rangle = H(t) |\psi(t)\rangle
$$

对于一个一般的[含时哈密顿量](@entry_id:136684)，从时间 $t_0$ 到 $t$ 的[演化算符](@entry_id:182628) $U(t, t_0)$ 是一个幺正算符，定义为 $|\psi(t)\rangle = U(t, t_0) |\psi(t_0)\rangle$。由于在不同时刻的[哈密顿量](@entry_id:172864)通常不对易（即 $[H(t_1), H(t_2)] \neq 0$ 当 $t_1 \neq t_2$ 时），$U(t, t_0)$ 不能简单地写成指数形式。相反，它由一个时间排序的指数给出，即 Dyson 级数：
$$
U(t, t_0) = \mathcal{T} \exp\left(-i \int_{t_0}^t H(t') dt'\right)
$$
其中 $\mathcal{T}$ 是[时间排序算符](@entry_id:148044)，它将算符依时间从右到左[排列](@entry_id:136432)。由于[哈密顿量](@entry_id:172864) $H(t)$ 是厄米的，[演化算符](@entry_id:182628) $U(t, t_0)$ 总是幺正的，即 $U(t, t_0)^\dagger U(t, t_0) = \mathbb{1}$ [@problem_id:3021700]。

对于周期性系统，我们特别关注演化一个完整周期的算符，称为 **Floquet 算符**或**频闪[演化算符](@entry_id:182628)**，记为 $U(T) \equiv U(T, 0)$。由于[哈密顿量](@entry_id:172864)的周期性，$H(t+T)=H(t)$，可以证明在任意时刻 $t$ 演化一个周期的算符都与 $U(T,0)$ 等价，即 $U(t+T, t) = U(T, 0)$。这意味着，我们只需研究一个周期内的演化，就可以理解在周期整数倍时刻的系统行为。在这些**频闪时刻** $t_n = nT$（其中 $n$ 为整数），系统的状态由初始状态 $|\psi(0)\rangle$ 通过重复应用 Floquet 算符得到 [@problem_id:3021700]：
$$
|\psi(nT)\rangle = U(nT, 0) |\psi(0)\rangle = (U(T))^n |\psi(0)\rangle
$$
这种只在周期整数倍时刻观察系统的演化称为**频闪演化**。

**Floquet 定理**是[周期性驱动系统](@entry_id:159779)的核心。它指出，[含时薛定谔方程](@entry_id:137898)的解可以写成如下形式：
$$
|\psi_\alpha(t)\rangle = e^{-i\epsilon_\alpha t} |\phi_\alpha(t)\rangle
$$
其中 $\epsilon_\alpha$ 是一个实常数，称为**准能** (quasi-energy)，而 $|\phi_\alpha(t)\rangle$ 是与驱动同周期的函数，称为 **Floquet 模式**，满足 $|\phi_\alpha(t+T)\rangle = |\phi_\alpha(t)\rangle$。这些态 $|\psi_\alpha(t)\rangle$ 构成了系统[希尔伯特空间](@entry_id:261193)的一组[完备基](@entry_id:143908)，称为 **Floquet 本征态**。

将该解的形式代入薛定谔方程，我们可以得到一个关于 Floquet 模式的本征方程。特别地，在频闪时刻 $t=T$，我们有：
$$
|\psi_\alpha(T)\rangle = U(T) |\psi_\alpha(0)\rangle = e^{-i\epsilon_\alpha T} |\phi_\alpha(T)\rangle = e^{-i\epsilon_\alpha T} |\phi_\alpha(0)\rangle
$$
这表明，Floquet 模式在 $t=0$ 时的状态 $|\phi_\alpha(0)\rangle$ 是 Floquet 算符 $U(T)$ 的本征矢，其[本征值](@entry_id:154894)为 $e^{-i\epsilon_\alpha T}$。由于 $U(T)$ 是幺正算符，其[本征值](@entry_id:154894)的模必须为 1，这保证了准能 $\epsilon_\alpha$ 是实数。

然而，准能的定义存在模糊性。如果我们用 $\epsilon_\alpha + k\Omega$ 替换 $\epsilon_\alpha$，其中 $\Omega = 2\pi/T$ 是驱动[角频率](@entry_id:261565)， $k$ 是任意整数，[本征值保持](@entry_id:636565)不变：
$$
e^{-i(\epsilon_\alpha + k\Omega)T} = e^{-i\epsilon_\alpha T} e^{-i k (2\pi/T)T} = e^{-i\epsilon_\alpha T} e^{-i 2\pi k} = e^{-i\epsilon_\alpha T}
$$
因此，准能仅在模 $\Omega$ 的意义下是唯一确定的，即 $\epsilon_\alpha \equiv \epsilon_\alpha + k\Omega$。这与[晶格](@entry_id:196752)中晶体动量的概念类似，后者是在模一个[倒格矢](@entry_id:263351)下定义的。通常，我们将准能限制在一个宽度为 $\Omega$ 的区间内，例如 $[-\Omega/2, \Omega/2)$，这个区间被称为**第一 Floquet-Brillouin 区** [@problem_id:3021700]。

频闪演化只描述了系统在 $t=nT$ 时刻的状态。而在一个周期内部的动力学，即 $t \in (nT, (n+1)T)$，则由所谓的**微运动** (micromotion) 描述。完整的动力学由 $|\psi(t)\rangle = U(t,0)|\psi(0)\rangle$ 给出，它不仅依赖于 $U(T)$，还依赖于周期内的具体演化路径 [@problem_id:3021700]。

#### 示例：构造 Floquet 算符

考虑一个由一系列瞬时脉冲驱动的自旋-1/2 系统。一个周期 $T$ 内的演化包括两个步骤：首先是绕 x 轴旋转 $\pi/2$，然后是绕 z 轴旋转 $\pi/2$。相应的幺正算符为 $U_x = \exp(-i \frac{\pi}{2} S_x)$ 和 $U_z = \exp(-i \frac{\pi}{2} S_z)$。整个周期的 Floquet 算符是这两个操作的乘积 $U_F = U_z U_x$。通过计算泡利矩阵的指数，我们可以得到 $U_x$ 和 $U_z$ 的具体矩阵形式，并最终计算出 $U_F$ 的 $2 \times 2$ 矩阵 [@problem_id:1139951]。对于另一个例子，一个在格点间跳跃并受到周期性“踢”的粒子，其 Floquet 算符由自由[演化算符](@entry_id:182628) $U_f$ 和踢腿算符 $U_k$ 的乘积构成，即 $U_F = U_f U_k$ [@problem_id:1139915]。这些具体的计算展示了如何从给定的[哈密顿量](@entry_id:172864) $H(t)$ 出发，通过积分或算符乘积来构造频闪[演化算符](@entry_id:182628) $U_F$，其本征谱直接给出了系统的准能。

### 扩展希尔伯特空间中的 Floquet [哈密顿量](@entry_id:172864)

将一个含时问题转化为一个等价的时不变问题是一种强大的理论技巧。在 Floquet 理论中，这通过引入一个扩展的[希尔伯特空间](@entry_id:261193)——通常称为 **Sambe 空间**——来实现。这个空间是系统原始希尔伯特空间 $\mathcal{H}$ 与周期为 $T$ 的[函数空间](@entry_id:143478) $\mathcal{T}$ 的[张量积](@entry_id:140694)，即 $\mathcal{H}_{\text{ext}} = \mathcal{H} \otimes \mathcal{T}$。

在 Sambe 空间中，Floquet 问题变成了一个时不变的[本征值问题](@entry_id:142153)，由所谓的 **Floquet [哈密顿量](@entry_id:172864)** $\mathcal{H}_F$ 描述：
$$
\mathcal{H}_F = H(t) - i \frac{\partial}{\partial t}
$$
$\mathcal{H}_F$ 的本征态正是 Floquet 态 $|\psi_\alpha(t)\rangle$，其[本征值](@entry_id:154894)为准能 $\epsilon_\alpha$。为了进行具体计算，我们通常在 $\mathcal{H}_{\text{ext}}$ 中选择一组方便的基。一个常见的选择是 $|j, n\rangle \equiv |j\rangle \otimes e^{in\Omega t}$，其中 $\{|j\rangle\}$ 是 $\mathcal{H}$ 的一组基（例如，能级本征态），$n$ 是一个整数，代表傅里叶模式 [@problem_id:874671]。

在 $|j, n\rangle$ 基下，Floquet [哈密顿量](@entry_id:172864)的矩阵元可以表示为：
$$
(\mathcal{H}_F)_{j'm, jn} \equiv \langle\langle j', m | \mathcal{H}_F | j, n \rangle\rangle = (H_{m-n})_{j'j} + n\Omega \delta_{jj'} \delta_{nm}
$$
其中 $(H_k)_{j'j} = \langle j'|H_k|j\rangle$ 是[哈密顿量](@entry_id:172864) $H(t)$ 的第 $k$ 个傅里叶分量 $H_k$ 的矩阵元，定义为：
$$
H_k = \frac{1}{T} \int_0^T H(t) e^{ik\Omega t} dt
$$
这个公式将含时问题转化为了一个无限维的、时不变的矩阵本征值问题。矩阵 $(\mathcal{H}_F)_{j'm, jn}$ 被称为 **Sambe 矩阵**。它的对角块（$m=n$）由系统的时均[哈密顿量](@entry_id:172864) $H_0$ 加上与傅里叶指数 $n$ 成正比的能量 $n\Omega$ 构成。这些对角块被称为**[光子](@entry_id:145192)扇区** (photon sectors)。非对角块（$m \neq n$）由[哈密顿量](@entry_id:172864)的傅里叶分量 $H_{m-n}$ 描述，它们耦合了不同的[光子](@entry_id:145192)扇区。例如，一个单色驱动 $H(t) \propto \cos(\Omega t)$ 只有 $H_{\pm 1}$ 分量非零，因此它只直接耦合相邻的[光子](@entry_id:145192)扇区（$m \leftrightarrow m \pm 1$）。

在实践中，这个无限维矩阵必须被截断才能求解。截断的有效性取决于系统的参数。例如，对于一个由[单色光](@entry_id:178750)驱动的 Su-Schrieffer-Heeger (SSH) 模型，其[哈密顿量](@entry_id:172864)为 $H(k,t) = H_0(k) + V(k)\cos(\Omega t)$，Sambe 矩阵可以被截断为只包含 $m \in \{-1, 0, +1\}$ 的扇区，形成一个 $3 \times 3$ 的[块矩阵](@entry_id:148435)。在静态[能隙](@entry_id:191975)闭合的[临界点](@entry_id:144653)（$H_0(\pi)=0$），这个截断的 Sambe 矩阵可以被精确对角化，结果表明驱动在原先的简并点处打开了一个准[能隙](@entry_id:191975)。这种截断在**高频**条件下是有效的，即驱动频率 $\Omega$ 远大于驱动诱导的[耦合强度](@entry_id:275517) $A$ ($A \ll \Omega$) [@problem_id:2990451]。在这种情况下，到更高[光子](@entry_id:145192)扇区（$|m| \ge 2$）的跃迁在能量上受到抑制，因此可以被忽略。

### Floquet 工程：从高频到共振

周期性驱动最强大的应用之一是 **Floquet 工程**，即通过精心设计 $H(t)$ 来创造出具有特定性质的有效（时不变）[哈密顿量](@entry_id:172864) $H_{\text{eff}}$。这为实现静态系统中难以甚至不可能存在的[物相](@entry_id:196677)和动力学行为开辟了道路。实现 Floquet 工程的主要理论工具是**[高频展开](@entry_id:139399)**。

#### 高频区：有效哈密顿量

当驱动频率 $\Omega$ 是系统中最大的能量尺度时（远大于系统的内禀能级差和驱动强度），系统的频闪演化可以被一个近似的时不变[有效哈密顿量](@entry_id:748813) $H_{\text{eff}}$ 很好地描述。这个 $H_{\text{eff}}$ 的一个重要特性是，它是局域的（如果原[哈密顿量](@entry_id:172864) $H(t)$ 是局域的）。寻找 $H_{\text{eff}}$ 的系统性方法是[高频展开](@entry_id:139399)，其中最著名的是 **Magnus 展开**和 **van Vleck 展开**。

**Magnus 展开**直接给出了 Floquet [哈密顿量](@entry_id:172864) $H_F$ 的一个级数表达式，使得 $U(T) = \exp(-iH_F T)$。$H_F$ 的展开式为：
$$
H_F = H_F^{(0)} + H_F^{(1)} + H_F^{(2)} + \dots
$$
其中各阶项是 $H(t)$ 在不同时刻的（嵌套）积分和对易子，与 $1/\Omega$ 的幂次成正比。例如，前两阶为：
$$
H_F^{(0)} = \frac{1}{T} \int_0^T H(t') dt'
$$
$$
H_F^{(1)} = \frac{-i}{2T} \int_0^T dt_1 \int_0^{t_1} dt_2 [H(t_1), H(t_2)]
$$
$H_F^{(0)}$ 只是[哈密顿量](@entry_id:172864)的时间平均值。$H_F^{(1)}$ 是第一个非平庸的修正，它涉及到不同时刻[哈密顿量](@entry_id:172864)的对易子，可以产生新的、在静态[哈密顿量](@entry_id:172864)中不存在的有效相互作用 [@problem_id:874592]。需要注意的是，任何有限阶截断的 Magnus 展开通常都依赖于积分区间的选择（即周期的起始点）[@problem_id:2990472]。更高阶的修正，如 $H_F^{(2)}$，涉及更复杂的嵌套对易子，可以描述更精细的效应，例如当系统受到多色场驱动时不同频率分量之间的相互作用 [@problem_id:874618]。

**van Vleck 展开**提供了另一种等价但概念上不同的方法。它旨在通过一个周期性的幺正变换 $e^{iK(t)}$ 来消除[哈密顿量](@entry_id:172864)中的时间依赖性，从而得到一个时不变的有效哈密顿量 $H_{\text{vV}}$。这个变换将系统从原始的“实验室框架”转换到一个运动的框架，在该框架中动力学由 $H_{\text{vV}}$ 控制。这个幺正[变换的生成元](@entry_id:172031) $K(t)$ 被称为“踢”算符，它本身捕获了系统的微运动。van Vleck 展开的一个优点是，它在每一阶都给出一个不依赖于周期起始点的 $H_{\text{vV}}$ [@problem_id:2990472]。例如，对于一个[哈密顿量](@entry_id:172864) $H(t) = H_0 + H_1 e^{i\omega t} + H_{-1} e^{-i\omega t}$，到 $1/\omega^2$ 阶的 van Vleck 有效哈密顿量会包含诸如 $[H_1, H_{-1}]$ 和 $[[H_{\pm 1}, H_0], H_{\mp 1}]$ 这样的项。这些项可以被看作是驱动场与静态[哈密顿量](@entry_id:172864)之间相互作用导致的对系统参数的“[重整化](@entry_id:143501)”[@problem_id:1139938]。

微运动本身也可以通过[高频展开](@entry_id:139399)来计算。Floquet 模式 $|\phi_\alpha(t)\rangle$ 可以写成 $|\phi_\alpha(t)\rangle = P(t)|\chi_\alpha\rangle$，其中 $|\chi_\alpha\rangle$ 是有效哈密顿量的[本征态](@entry_id:149904)，$P(t)$ 是描述微运动的周期性幺正算符。在 van Vleck 方法中，$P(t) \approx e^{-iK(t)}$。这个算符导致了在由 $H_{\text{eff}}$ 控制的平滑演化之上的快速[振荡](@entry_id:267781)。例如，一个可观测量 $O$ 的[期望值](@entry_id:153208)会表现出这种微运动：$\langle O(t) \rangle = \langle \chi_\alpha | P(t)^\dagger O P(t) | \chi_\alpha \rangle$。即使在[有效哈密顿量](@entry_id:748813)的[本征态](@entry_id:149904)中，$\langle O(t) \rangle$ 也会随时间[振荡](@entry_id:267781)，其[振荡](@entry_id:267781)幅度和频率可以通过展开 $P(t)$ 来计算 [@problem_id:1139995, @problem_id:612617]。

#### 共振区：缀饰态与[旋转波近似](@entry_id:204016)

当驱动频率 $\Omega$ 接近或等于系统的一个内禀跃迁频率 $\omega_0$ 时（即 $\Omega \approx \omega_0$），[高频展开](@entry_id:139399)就会失效。从微扰论的角度看，这是因为耦合了[近简并](@entry_id:172107)态的项中出现了“小分母”，导致展开式发散。物理上，这意味着驱动与系统发生了共振，能够有效地在能级之间[交换能](@entry_id:137069)量，这是一个非微扰的过程 [@problem_id:2990411]。

在这种**共振**情况下，正确的处理方法是进入一个以驱动频率 $\Omega$ 旋转的[参考系](@entry_id:169232)，并应用**[旋转波近似](@entry_id:204016)** (RWA)。考虑一个双能级系统，其静态[哈密顿量](@entry_id:172864)为 $H_0 = \frac{\omega_0}{2}\sigma_z$，驱动项为 $V(t) = g\cos(\Omega t)\sigma_x$。我们通过幺正变换 $U(t) = \exp(i\frac{\Omega t}{2}\sigma_z)$ 转换到[旋转参考系](@entry_id:174154)。变换后的[哈密顿量](@entry_id:172864) $H_R = U^\dagger H U + i(\partial_t U^\dagger)U$ 包含时不变项和快速[振荡](@entry_id:267781)项（频率为 $2\Omega$）。RWA 就是忽略这些快速[振荡](@entry_id:267781)的“反向旋转”项，因为它在时间上的平均效应很小。这样我们就得到了一个时不变的 RWA [哈密顿量](@entry_id:172864)：
$$
H_{\text{RWA}} = \frac{\delta}{2}\sigma_z + \frac{g}{2}\sigma_x
$$
其中 $\delta = \omega_0 - \Omega$ 是**[失谐](@entry_id:148084)** (detuning)。

这个 RWA [哈密顿量](@entry_id:172864)的[本征态](@entry_id:149904)被称为**[缀饰态](@entry_id:143646)** (dressed states)，它们是原子裸态（$|g\rangle, |e\rangle$）和[光子](@entry_id:145192)场的相干叠加。$H_{\text{RWA}}$ 的本征能量（即准能）为 $E_\pm = \pm \frac{1}{2}\sqrt{\delta^2 + g^2}$。因此，驱动在共振点（$\delta=0$）打开了一个大小为 $g$ 的[能隙](@entry_id:191975)，这个[能隙](@entry_id:191975)被称为**[拉比分裂](@entry_id:139113)** (Rabi splitting)。完整的准能分裂为 $\Delta\epsilon = \sqrt{\delta^2 + g^2}$ [@problem_id:2990411]。

[缀饰态](@entry_id:143646)的概念在许多物理现象中都至关重要。
- **AC 斯塔克位移** (AC Stark shift)：在大的失谐极限下（$|\delta| \gg g$），[缀饰态](@entry_id:143646)的能量相对于裸态能量会有一个位移。对于[基态](@entry_id:150928)，这个位移（或称光位移）可以微扰地计算出来，结果为 $\delta E_g \approx -g^2/(4\delta)$。这表明强非共振光场可以有效地改变原子的能级结构。
- **Autler-Townes 分裂**：在一个三能级的 $\Lambda$ 型系统中，如果一个强驱动场共振地耦合了其中两个能级（例如 $|2\rangle \leftrightarrow |3\rangle$），那么用一个弱探测场去探测涉及其中一个能级的另一跃迁（例如 $|1\rangle \leftrightarrow |3\rangle$）时，会观察到吸收[谱线分裂](@entry_id:150380)成两条。这个分裂的大小直接等于强驱动场的[拉比频率](@entry_id:154019) $\Omega_c$ [@problem_id:1139973]。这为测量相干[耦合强度](@entry_id:275517)提供了一种直接的[光谱学](@entry_id:141940)方法。
- 对于一个在共振时由[圆偏振光](@entry_id:198374)驱动的系统，旋转框架下的[哈密顿量](@entry_id:172864)自然就是时不变的，无需 RWA。在这种情况下，可以精确求解其 Floquet 本征态，并计算物理量的[期望值](@entry_id:153208)，例如[时间平均](@entry_id:267915)磁化强度 [@problem_id:1139942]。

### 对称性与多体现象

将 Floquet 理论应用于[多体系统](@entry_id:144006)会带来新的复杂性和丰富的现象，其中对称性扮演着核心角色。

#### 对称性约束

系统的对称性对准能谱施加了严格的约束。如果一个幺正算符 $S$ 与[哈密顿量](@entry_id:172864)在所有时刻都对易，$[S, H(t)]=0$，那么它也与 Floquet 算符对易，$[S, U(T)]=0$。这意味着 $U(T)$ 和 $S$ 可以被[同时对角化](@entry_id:196036)，Floquet [本征态](@entry_id:149904)可以被标记上 $S$ 的[量子数](@entry_id:145558)。

更有趣的情况是**反幺正对称性**，最典型的例子是时间反演对称性 $\mathcal{K}$。一个[反幺正算符](@entry_id:197532) $K$ 如果与 $U(T)$ 对易，$[K, U(T)] = 0$，那么如果 $|\phi_\alpha\rangle$ 是 $U(T)$ 的一个[本征值](@entry_id:154894)为 $\lambda_\alpha$ 的本征态，则 $K|\phi_\alpha\rangle$ 也是 $U(T)$ 的本征态，但其[本征值](@entry_id:154894)为 $\lambda_\alpha^*$。这意味着准[能谱](@entry_id:181780)必须关于 $\epsilon=0$ 对称（$\epsilon_\alpha \leftrightarrow -\epsilon_\alpha$）。

如果 $K|\phi_\alpha\rangle$ 与 $|\phi_\alpha\rangle$ [线性无关](@entry_id:148207)，并且它们的[本征值](@entry_id:154894)相同（$\lambda_\alpha = \lambda_\alpha^*$），则这两个态构成一个简并对。这种情况只发生在 $\lambda_\alpha$ 为实数时，即 $\lambda_\alpha = \pm 1$。这对应于准能位于 Floquet-[Brillouin 区](@entry_id:142395)的中心（$\epsilon_\alpha = 0$）或边界（$\epsilon_\alpha = \pi/T$）。对于一个满足 $K^2 = -1$ 的反幺正对称性（例如自旋-1/2 系统中的时间反演），在这些高[对称点](@entry_id:174836)上的所有 Floquet [本征态](@entry_id:149904)都必须是至少双重简并的。这被称为 **Kramers 简并**的 Floquet 推广。在准[能谱](@entry_id:181780)的其他地方，简并通常不被保证 [@problem_id:1139929, @problem_id:874617]。

#### 周期性驱动[多体系统](@entry_id:144006)：加热与新奇物相

当一个泛函的、相互作用的[量子多体系统](@entry_id:141221)受到周期性驱动时，一个核心问题是它的[长期行为](@entry_id:192358)是什么。与只有一个或几个自由度的系统不同，多体系统拥有指数级增长的能态密度。

**加热与 Floquet-ETH**：根据时间相关的微扰理论，当驱动频率的整数倍匹配系统任意两个多体能级之间的能量差时，即 $E_m - E_n \approx k\Omega$，就会发生共振吸收。在一个泛函（非可积）的多体系统中，根据**[本征态热化假说](@entry_id:137025)** (ETH)，[能谱](@entry_id:181780)是稠密的，且连接不同能级的跃迁矩阵元通常非零。这意味着对于任何驱动频率，总会存在大量的共振通道。结果是，系统会不断地从驱动场中吸收能量，导致其温度持续升高，最终达到一个熵最大的状态——**无限温度态**。这个过程被称为**Floquet 加热** [@problem_id:2990389]。描述这种[热化](@entry_id:142388)行为的理论框架被称为 **Floquet [本征态热化假说](@entry_id:137025)** (Floquet-ETH)。它断言，在一个泛函 Floquet 系统中，任何 Floquet [本征态](@entry_id:149904)对于局域[可观测量](@entry_id:267133)来说，其性质都与无限温度系综（在给定对称性扇区内）相同 [@problem_id:2984449]。

**[预热化](@entry_id:147591)** (Prethermalization)：虽然无限期加热是泛函系统的最终命运，但在高频驱动（$\Omega$ 远大于局域[能量尺度](@entry_id:196201) $J$）的情况下，加热速率可能极慢。系统首先会快速弛豫到一个准[稳态](@entry_id:182458)，这个过程被称为**[预热化](@entry_id:147591)**。这个准[稳态](@entry_id:182458)可以由一个近似守恒的、局域的[有效哈密顿量](@entry_id:748813) $H_{\text{eff}}$（例如通过 Magnus 或 van Vleck 展开得到）来描述 [@problem_id:874648]。系统会表现得好像它正在向一个由 $H_{\text{eff}}$ 决定的有限温度的吉布斯态热化。这个[预热化](@entry_id:147591)平台可以持续非常长的时间，其寿命通常随驱动频率呈[指数增长](@entry_id:141869)（$t_* \sim \exp(c\Omega/J)$）。只有在远超这个时间尺度之后，被[高频展开](@entry_id:139399)所忽略的非局域项或高阶项才会引发缓慢的加热，最终使系统走向无限温度态 [@problem_id:2984449]。

**[离散时间晶体](@entry_id:136742)** (Discrete Time Crystals, DTCs)：尽管泛函系统倾向于加热，但存在一些机制可以阻止这种[热化](@entry_id:142388)，从而稳定真正新颖的非平衡物相。**[多体局域化](@entry_id:147122)** (MBL) 就是这样一种机制，其中强无序可以阻止能量在系统中[扩散](@entry_id:141445)。在 MBL 系统的 Floquet 版本中，可以实现一种被称为[离散时间晶体](@entry_id:136742)的物相。DTC 的标志是它自发地破坏了[哈密顿量](@entry_id:172864)的离散[时间平移对称性](@entry_id:261093)。如果[哈密顿量](@entry_id:172864)的周期是 $T$，系统的某些[可观测量](@entry_id:267133)会以一个更长的周期 $nT$（通常是 $2T$）演化。这种[倍周期](@entry_id:145711)响应的微观机制是，系统存在成对的 Floquet 本征态，其准能差恰好为 $\Delta\epsilon = \pi/T$。在 MBL 的保护下，系统可以长时间保持在这些态的相干叠加态上，从而表现出稳定的、亚[谐波](@entry_id:181533)的响应，即使对于随机的初始态也是如此 [@problem_id:3021700]。