## 引言
超导现象作为宏观量子效应的典范，其微观机制的描述对[凝聚态物理学](@entry_id:140205)至关重要。巴丁-库珀-施里弗（Bardeen-Cooper-Schrieffer, BCS）理论成功地解释了常规超导，指出其[基态](@entry_id:150928)是由库珀对构成的凝聚体，而其[元激发](@entry_id:140859)则是电子和空穴的量子叠加态。这一独特的物理图像给理论描述带来了挑战：传统的[单粒子格林函数](@entry_id:140400)方法无法内在地处理描述[库珀对](@entry_id:143370)产生与湮灭的粒子-空穴混合过程，暴露了理论工具上的知识鸿沟。

为了解决这一问题，[南部-戈尔科夫格林函数](@entry_id:145547)形式主义应运而生。它通过引入一个包含粒子和空穴分量的“南部自旋量”，将理论框架的自由度加倍，从而能够在统一的矩阵形式下优雅地描述超导态。这种方法不仅是描述超导配对的自然语言，也为系统地处理相互作用、无序效应和非平衡过程提供了强大的数学工具。

本文将系统地引导读者掌握这一核心理论。在第一章“原理与机制”中，我们将建立南部-戈尔科夫形式主义的基础，定义南部自[旋量](@entry_id:158054)、矩阵[格林函数](@entry_id:147802)，并将其与[博戈留波夫-德热纳哈密顿量](@entry_id:145387)联系起来。第二章“应用与跨学科连接”将展示该理论如何解释隧穿谱、磁响应等关键实验，并应用于研究[邻近效应](@entry_id:139932)、非常规超导乃至拓扑超导中的马约拉纳费米子等前沿课题。最后，在第三章“动手实践”中，读者将通过具体的计算问题，加深对[能隙方程](@entry_id:141924)、杂质效应等核心概念的理解。通过这一结构化的学习路径，读者将能够从基本原理出发，逐步掌握运用[南部-戈尔科夫格林函数](@entry_id:145547)解决实际物理问题的能力。

## 原理与机制

### 南部-戈尔科夫形式主义：粒子与空穴的统一描述

对常规金属态——[费米液体](@entry_id:142392)——的描述建立在定义明确的[准粒子](@entry_id:136584)概念之上，即被周围介质的相互作用所“缀饰”的电子。格林函数形式主义是描述这些[准粒子](@entry_id:136584)传播的自然语言。然而，由[BCS理论](@entry_id:144185)描述的超导态提出了一个根本性的挑战。其[基态](@entry_id:150928)是库珀对的凝聚体，而[元激发](@entry_id:140859)（被称为博戈留波夫[准粒子](@entry_id:136584)）是类电子态和类空穴态的[量子叠加](@entry_id:137914)。该超导态的一个关键特征是存在非零的对算符[期望值](@entry_id:153208)，例如 $\langle c_{-\mathbf{k}\downarrow} c_{\mathbf{k}\uparrow} \rangle$，这在任何正常态中都为零。因此，一个仅追踪单个电子传播的[格林函数](@entry_id:147802)形式主义，$G(x, x') \propto \langle T_\tau c(x) c^\dagger(x') \rangle$，是不完备的。它无法内在地描述[库珀对](@entry_id:143370)的产生和湮灭。

为了解决这个问题，南部阳一郎（Yoichiro Nambu）和列夫·戈尔科夫（Lev Gor'kov）发展出一种将粒子和空穴置于同等地位的矩阵形式主义。这是通过将自由度加倍来实现的。我们不再使用单个电子算符，而是定义一个称为**南部自旋量**的双分量对象。对于自旋单态[超导体](@entry_id:191025)，一个常见的选择是：
$$
\Psi_{\mathbf{k}} = \begin{pmatrix} c_{\mathbf{k}\uparrow} \\ c_{-\mathbf{k}\downarrow}^{\dagger} \end{pmatrix}
$$
这里，顶部分量是湮灭一个动量为 $\mathbf{k}$、自旋向上的电子的算符，而底部分量是*产生*一个动量为 $-\mathbf{k}$、自旋向下的电子的算符。产生一个具有 $(-\mathbf{k}, \downarrow)$ 的电子等效于湮灭一个具有 $(\mathbf{k}, \uparrow)$ 的空穴。因此，南部自[旋量](@entry_id:158054)优雅地将类粒子自由度与类空穴自由度结合在一起。这种结构是描述动量相反、自旋相反的电子之间配对所需的最小结构 [@problem_id:2983436]。

对于更复杂的配对态，或者当自旋不是一个[好量子数](@entry_id:262514)时（例如，在存在强[自旋轨道](@entry_id:274032)耦合的情况下），需要一个更通用的四分量自旋量，它包括所有的自旋和粒子-空穴自由度：$\Psi_{\mathbf{k}} = ( c_{\mathbf{k}\uparrow}, c_{\mathbf{k}\downarrow}, c^\dagger_{-\mathbf{k}\downarrow}, c^\dagger_{-\mathbf{k}\uparrow} )^T$ [@problem_id:1101209]。对于许多常规情况，更简单的双分量自旋量已经足够，我们将在初步发展中使用它。

定义了南部自[旋量](@entry_id:158054)后，我们可以构造一个**[南部-戈尔科夫格林函数](@entry_id:145547)**，它是一个 $2 \times 2$ 矩阵。在虚时间 $\tau$ 和动量空间中，它被定义为：
$$
\mathcal{G}(\mathbf{k}, \tau) = - \langle T_\tau \Psi_{\mathbf{k}}(\tau) \Psi_{\mathbf{k}}^{\dagger}(0) \rangle
$$
其中 $T_\tau$ 是[时间排序算符](@entry_id:148044)。在[傅里叶变换](@entry_id:142120)到[松原频率](@entry_id:197724)空间后，$\mathcal{G}(\mathbf{k}, i\omega_n)$，通过检查其分量，这个矩阵呈现出清晰的物理意义 [@problem_id:1173850]：
$$
\mathcal{G}(\mathbf{k}, i\omega_n) = \begin{pmatrix}
-\int_0^\beta d\tau e^{i\omega_n \tau} \langle T_\tau c_{\mathbf{k}\uparrow}(\tau) c_{\mathbf{k}\uparrow}^\dagger(0) \rangle & -\int_0^\beta d\tau e^{i\omega_n \tau} \langle T_\tau c_{\mathbf{k}\uparrow}(\tau) c_{-\mathbf{k}\downarrow}(0) \rangle \\
-\int_0^\beta d\tau e^{i\omega_n \tau} \langle T_\tau c_{-\mathbf{k}\downarrow}^\dagger(\tau) c_{\mathbf{k}\uparrow}^\dagger(0) \rangle & -\int_0^\beta d\tau e^{i\omega_n \tau} \langle T_\tau c_{-\mathbf{k}\downarrow}^\dagger(\tau) c_{-\mathbf{k}\downarrow}(0) \rangle
\end{pmatrix}
$$
这些分量通常被命名为：
$$
\mathcal{G}(\mathbf{k}, i\omega_n) = \begin{pmatrix} G(\mathbf{k}, i\omega_n) & F(\mathbf{k}, i\omega_n) \\ F^\dagger(\mathbf{k}, i\omega_n) & -G(-\mathbf{k}, -i\omega_n) \end{pmatrix}
$$
*   $G(\mathbf{k}, i\omega_n)$ 是**正常[格林函数](@entry_id:147802)**。它描述单个电子的传播，就像在正常态中一样。
*   $F(\mathbf{k}, i\omega_n)$ 是**[反常格林函数](@entry_id:141518)**，也称为戈尔科夫函数。它描述了从[基态](@entry_id:150928)中湮灭两个电子以产生一个[库珀对](@entry_id:143370)激发，或其逆过程。它的存在是超导态的标志。
*   $F^\dagger(\mathbf{k}, i\omega_n)$ 描述 $F$ 的逆过程。
*   $(2,2)$ 分量描述空穴的传播，这与具有相反动量和能量的电子的传播有关。

### [博戈留波夫-德热纳哈密顿量](@entry_id:145387)与平均场传播子

当我们在这个新基底下写出平均场BCS[哈密顿量](@entry_id:172864)时，南部-戈尔科夫形式主义的效用就显而易见了。[哈密顿量](@entry_id:172864) $H = \sum_{\mathbf{k}\sigma} \xi_\mathbf{k} c_{\mathbf{k}\sigma}^\dagger c_{\mathbf{k}\sigma} + \sum_\mathbf{k} (\Delta c_{\mathbf{k}\uparrow}^\dagger c_{-\mathbf{k}\downarrow}^\dagger + \Delta^* c_{-\mathbf{k}\downarrow} c_{\mathbf{k}\uparrow})$ 可以表示为矩阵形式 $H = \sum_\mathbf{k}' \Psi_\mathbf{k}^\dagger H_\mathbf{k} \Psi_\mathbf{k} + E_0$，其中求和遍历动量空间的一半，而 $H_\mathbf{k}$ 是 $2 \times 2$ 的**博戈留波夫-德热纳（BdG）[哈密顿量](@entry_id:172864)**：
$$
H_\mathbf{k} = \begin{pmatrix} \xi_\mathbf{k} & \Delta \\ \Delta^* & -\xi_\mathbf{k} \end{pmatrix}
$$
这里，$\xi_\mathbf{k}$ 是相对于化学势的正常态电子能量，$\Delta$ 是超导序参量（[能隙](@entry_id:191975)）。这个紧凑的矩阵形式包含了BCS平均场理论的所有基本物理。我们也可以使用泡利矩阵 $\tau_i$ 来表示它，这些矩阵在这个粒子-空穴“[赝自旋](@entry_id:147053)”空间中作为[基矢](@entry_id:199546)：$H_\mathbf{k} = \xi_\mathbf{k} \tau_z + \text{Re}(\Delta) \tau_x - \text{Im}(\Delta) \tau_y$。

格林函数是系统的[传播子](@entry_id:139558)，其逆由支配运动方程的算符给出。在[松原频率](@entry_id:197724)空间中，这导致了一个简单而强大的关系：
$$
\mathcal{G}^{-1}(\mathbf{k}, i\omega_n) = i\omega_n \mathbf{1} - H_\mathbf{k} = \begin{pmatrix} i\omega_n - \xi_\mathbf{k} & -\Delta \\ -\Delta^* & i\omega_n + \xi_\mathbf{k} \end{pmatrix}
$$
然后，通过简单地对这个 $2 \times 2$ 矩阵求逆，就可以找到完整的平均场[南部-戈尔科夫格林函数](@entry_id:145547)：
$$
\mathcal{G}(\mathbf{k}, i\omega_n) = \frac{1}{(i\omega_n - \xi_\mathbf{k})(i\omega_n + \xi_\mathbf{k}) - |\Delta|^2} \begin{pmatrix} i\omega_n + \xi_\mathbf{k} & \Delta \\ \Delta^* & i\omega_n - \xi_\mathbf{k} \end{pmatrix} = \frac{1}{(i\omega_n)^2 - E_\mathbf{k}^2} \begin{pmatrix} i\omega_n + \xi_\mathbf{k} & \Delta \\ \Delta^* & i\omega_n - \xi_\mathbf{k} \end{pmatrix}
$$
在这里我们识别出了格林[函数的极点](@entry_id:189069)，它们定义了系统的[元激发](@entry_id:140859)能量：$E_\mathbf{k} = \sqrt{\xi_\mathbf{k}^2 + |\Delta|^2}$。这些就是著名的博戈留波夫[准粒子能量](@entry_id:173936)。

从这个表达式中，我们可以读出各个分量。对于实数[能隙](@entry_id:191975) $\Delta$：
$$
G(\mathbf{k}, i\omega_n) = \frac{i\omega_n + \xi_\mathbf{k}}{(i\omega_n)^2 - E_\mathbf{k}^2} \qquad \text{和} \qquad F(\mathbf{k}, i\omega_n) = \frac{\Delta}{(i\omega_n)^2 - E_\mathbf{k}^2}
$$
这些显式形式揭示了格林函数分量与[超导体](@entry_id:191025)物理参数之间错综复杂的关系。例如，人们可以仅用格林函数矩阵本身的分量来表示[能隙](@entry_id:191975)参数 $\Delta$，从而为该形式主义提供一个自洽的检验 [@problem_id:1173850]。

这一工具的一个主要应用是推导自洽[能隙方程](@entry_id:141924)。[序参量](@entry_id:144819) $\Delta$ 不是一个外部参数，而是源于电子间的吸引作用 $V$。自洽条件是 $\Delta = -V \sum_\mathbf{k} \langle c_{-\mathbf{k}\downarrow} c_{\mathbf{k}\uparrow} \rangle$。该[期望值](@entry_id:153208)通过以下关系与[反常格林函数](@entry_id:141518)直接相关：
$$
\langle c_{-\mathbf{k}\downarrow} c_{\mathbf{k}\uparrow} \rangle = \frac{1}{\beta} \sum_{n=-\infty}^{\infty} F(\mathbf{k}, i\omega_n) e^{i\omega_n 0^+}
$$
代入 $F(\mathbf{k}, i\omega_n)$ 的表达式并进行[松原求和](@entry_id:147118)，得到 $\langle c_{-\mathbf{k}\downarrow} c_{\mathbf{k}\uparrow} \rangle = \frac{\Delta}{2E_\mathbf{k}} \tanh\left(\frac{\beta E_\mathbf{k}}{2}\right)$。在零温（$T=0, \beta \to \infty$）下，这简化为 $\frac{\Delta}{2E_\mathbf{k}}$。[能隙方程](@entry_id:141924)变为：
$$
1 = V \sum_\mathbf{k} \frac{1}{2\sqrt{\xi_\mathbf{k}^2 + \Delta^2}}
$$
在[费米能级](@entry_id:143215)附近使用常数[态密度](@entry_id:147894) $N(0)$ 将求和转换为[能量积分](@entry_id:166228)，$\sum_\mathbf{k} \to N(0) \int d\xi$，并在BCS相互作用窗口 $[-\hbar\omega_D, \hbar\omega_D]$ [内积](@entry_id:158127)分，即可得到著名的[弱耦合](@entry_id:140994)零温[能隙](@entry_id:191975)结果 [@problem_id:1173818] [@problem_id:656453]：
$$
\Delta(0) \approx 2\hbar\omega_D \exp\left(-\frac{1}{N(0)V}\right)
$$

### 对称性、响应与激发

南部-戈尔科夫形式主义特别擅长处理超导态的对称性。[BdG哈密顿量](@entry_id:145387)具有内在的**[粒子-空穴对称性](@entry_id:142469)**。这种对称性对格林函数施加了约束。对于南部自[旋量](@entry_id:158054)的某些选择，这表现为一种关系式，如 $\mathcal{G}(\mathbf{k}, i\omega_n) = -\tau_y \mathcal{G}^T(-\mathbf{k}, -i\omega_n) \tau_y$，前提是[能隙](@entry_id:191975)函数具有特定的对称性（例如，对于[奇宇称](@entry_id:147965)配对，$\Delta_{-\mathbf{k}} = -\Delta_\mathbf{k}$）。如果[能隙](@entry_id:191975)函数没有确定的宇称，如在同时存在s波和p波分量的[非中心对称](@entry_id:157488)[超导体](@entry_id:191025)中，这种对称性就会被破坏。南部-戈尔科夫形式主义允许人们精确地量化这种破缺的程度 [@problem_id:1173845]。

此外，超导性由全局[U(1)规范对称性](@entry_id:170701)（与[电荷守恒](@entry_id:264158)相关）的自发破缺所定义。这个深刻的物理事实反映在该理论的**[沃德-高桥恒等式](@entry_id:145721)**中。在正常态下，[沃德恒等式](@entry_id:147000)确保了[电荷守恒](@entry_id:264158)。在超导态下，广义恒等式获得了一项表示粒子数不守恒的项。在零动量转移的极限下，这与交换子 $[\tau_3, \mathcal{G}^{-1}(\mathbf{k}, \omega)]$ 成正比。对于BCS[超导体](@entry_id:191025)，该交换子的计算结果与[能隙](@entry_id:191975)参数 $\Delta$ 成正比，从而明确地将序参量与其所代表的守恒律破缺联系起来 [@problem_id:1220473]。

该形式主义还提供了直接获取实验[可观测量](@entry_id:267133)的途径。**谱函数** $A(\mathbf{k}, \omega)$，在角分辨光电子能谱（[ARPES](@entry_id:139661)）中测量，由[推迟格林函数](@entry_id:139183)的虚部给出，$A(\mathbf{k}, \omega) = -\frac{1}{\pi} \text{Im} \, \text{Tr}[\mathcal{G}^R(\mathbf{k}, \omega)]$。对于BCS[超导体](@entry_id:191025)，谱函数的电子部分可以计算为：
$$
A_{ee}(\mathbf{k}, \omega) = u_\mathbf{k}^2 \delta(\omega - E_\mathbf{k}) + v_\mathbf{k}^2 \delta(\omega + E_\mathbf{k})
$$
这里，$u_\mathbf{k}^2 = \frac{1}{2}(1 + \frac{\xi_\mathbf{k}}{E_\mathbf{k}})$ 和 $v_\mathbf{k}^2 = \frac{1}{2}(1 - \frac{\xi_\mathbf{k}}{E_\mathbf{k}})$ 是著名的**[BCS相干因子](@entry_id:142994)**，分别代表博戈留波夫[准粒子](@entry_id:136584)的[电子和空穴](@entry_id:274534)权重。这个表达式优美地捕捉了激发谱中超导能隙的打开。该形式主义可以很容易地扩展以包括额外的效应，如塞曼[磁场](@entry_id:153296)，它会使自旋向上和自旋向下电子的谱峰分裂 [@problem_id:640794]，或者扩展到更复杂的[能带结构](@entry_id:139379)，例如具有[拉什巴自旋轨道耦合](@entry_id:154628)的能带结构，其中问题通常可以分解为不同[螺旋性](@entry_id:157633)带内的独立配对通道 [@problem_id:1173875]。

### 相互作用与无序：[自能](@entry_id:145608)

[格林函数](@entry_id:147802)形式主义的真正威力在于其能够通过**自能** $\Sigma$ 的概念系统地纳入相互作用和无序。完整[格林函数](@entry_id:147802) $\mathcal{G}$ 通过矩阵**[戴森方程](@entry_id:146246)**与非相互作用（或平均场）[格林函数](@entry_id:147802) $\mathcal{G}_0$ 相关联：
$$
\mathcal{G}^{-1} = \mathcal{G}_0^{-1} - \Sigma
$$
在南部空间中，自能也是一个 $2 \times 2$ 矩阵，其分量描述了相互作用如何[重整化](@entry_id:143501)电子和空穴的[传播子](@entry_id:139558)以及配对本身 [@problem_id:2983436]。对于一个相互作用系统，完整的逆格林函数写作：
$$
\mathcal{G}^{-1}(\mathbf{k}, i\omega_n) = \begin{pmatrix} i\omega_n - \xi_\mathbf{k} - \Sigma_N(\mathbf{k}, i\omega_n) & -\Delta(\mathbf{k}, i\omega_n) \\ -\Delta^*(\mathbf{k}, i\omega_n) & i\omega_n + \xi_\mathbf{k} - \Sigma_N^*(-\mathbf{k}, -i\omega_n) \end{pmatrix}
$$
这里，$\Sigma_N$ 是在金属态中也存在的正常[自能](@entry_id:145608)，而 $\Delta$ 是反常自能，它现在包含了超越简单平均场近似的所有对配对顶角的多体修正。

#### 应用1：推导[金兹堡-朗道理论](@entry_id:141010)

南部-戈尔科夫形式主义最显著的成就之一是它能够为唯象的金兹堡-朗道（GL）理论提供微观推导。GL自由能在临界温度 $T_c$ 附近的展开是通过将[巨势](@entry_id:136286)差 $\Omega_s - \Omega_n$ 按序参量 $\Delta$ 的幂次展开得到的。这个差值可以用[南部-戈尔科夫格林函数](@entry_id:145547)精确表示：
$$
\Omega_s - \Omega_n = - T \sum_{\mathbf{k},n} \text{Tr} \left[ \ln(-\mathcal{G}^{-1}) \right] - (\text{正常态}) = T \sum_{\mathbf{k},n} \ln\left(1 + \frac{|\Delta|^2}{\omega_n^2 + \xi_\mathbf{k}^2}\right) - \frac{|\Delta|^2}{V}
$$
对小 $\Delta$ 展开对数项，得到一个关于 $|\Delta|^2$ 的[幂级数](@entry_id:146836)：
$$
\Omega_s - \Omega_n = a(T) |\Delta|^2 + \frac{1}{2} b(T) |\Delta|^4 + \dots
$$
通过执行[松原求和](@entry_id:147118)和动量积分，可以找到GL系数 $a(T)$ 和 $b(T)$ 的显式微观表达式。这个过程表明 $a(T) \propto N(0) (T - T_c)/T_c$，正确预测了在 $T_c$ 处超导的出现 [@problem_id:1173816]，并给出了第二个系数 $b(T_c)$ 的值 [@problem_id:1173833] [@problem_id:1173869]。这个推导也可以从图形上理解，其中 $|\Delta|^4$ 项对应于计算代表四个[准粒子](@entry_id:136584)通过凝聚体媒介相互作用的[费米子](@entry_id:146235)“盒子图” [@problem_id:1166661]。对于常规BCS[超导体](@entry_id:191025)，结果是：
$$
b(T_c) = \frac{7 \zeta(3) N(0)}{8 \pi^2 (k_B T_c)^2}
$$
这将金属的微观参数（$N(0), T_c$）与一个宏观可测量的量，如在[相变](@entry_id:147324)处的比热跃变 $\Delta C \propto a'(T_c)^2 / b(T_c)$，联系起来。

#### 应用2：[杂质散射](@entry_id:267814)

该形式主义对于研究无序[超导体](@entry_id:191025)是不可或缺的。[杂质散射](@entry_id:267814)的效应被编码在自能中，可以使用诸如**自洽[玻恩近似](@entry_id:138141)（SCBA）**的近似方法来计算。

对于常规s波[超导体](@entry_id:191025)中的**非磁性杂质**，一个被称为**[安德森定理](@entry_id:139654)**的非凡结果出现了。自能计算表明，无序不会破坏配对。相反，其效应可以完全被吸收到[松原频率](@entry_id:197724)和[能隙](@entry_id:191975)参数的[重整化](@entry_id:143501)中 [@problem_id:266360]：
$$
\tilde{\omega}_n = \omega_n Z_n \quad , \quad \tilde{\Delta}_n = \Delta Z_n \quad \text{其中} \quad Z_n = 1 + \frac{\hbar}{2\tau \sqrt{\omega_n^2 + \Delta^2}}
$$
这里 $\tau$ 是[弹性散射](@entry_id:152152)时间。这种重整化有效地“涂抹”了电子态，但因为配对是各向同性的（s波），这种涂抹对配对态 $(k\uparrow, -k\downarrow)$ 和[时间反演](@entry_id:182076)态的影响是相同的，从而保持了库珀对的结合能——以及 $T_c$——不变。

对于破坏时间反演对称性的**磁性杂质**，情况则截然不同。这些杂质是强效的**破对杂质**。由阿布里科索夫和戈尔科夫开创的自能计算表明，[临界温度](@entry_id:146683)受到强烈抑制。得到的关于抑制后的 $T_c$ 作为自旋翻转散射率 $1/\tau_s$ 的函数的方程是 [@problem_id:1173819] [@problem_id:1173871]：
$$
\ln\left(\frac{T_c}{T_{c0}}\right) = \psi\left(\frac{1}{2}\right) - \psi\left(\frac{1}{2} + \frac{\hbar}{4\pi k_B T_c \tau_s}\right)
$$
其中 $T_{c0}$ 是纯净极限下的转变温度，$\psi(z)$ 是[双伽玛函数](@entry_id:174427)。在弱散射极限下，这导致了线性抑制：$T_c - T_{c0} \approx -\frac{\pi\hbar}{8k_B \tau_s}$。足够强的磁性散射可以导致**[无能](@entry_id:201612)隙超导**，这是一种奇特的状态，其中序参量 $\Delta$ 是有限的，但[态密度](@entry_id:147894)中的[激发能](@entry_id:190368)隙已经关闭 [@problem_id:1173822] [@problem_id:656376]。

这种[二分法](@entry_id:140816)是探测[超导能隙](@entry_id:145058)对称性的一个有力工具。对于**[非常规超导体](@entry_id:141195)**，如d波铜氧化物，[序参量](@entry_id:144819)在费米面上改变符号（$\Delta_{-\mathbf{k}} \neq \Delta_\mathbf{k}$）。在这种情况下，即使是非磁性杂质也充当了破对杂质，因为它们将[电子散射](@entry_id:159023)到费米面上具有不同[能隙](@entry_id:191975)符号的区域之间。因此，[d波超导体](@entry_id:139318)的 $T_c$ 会被非磁性无序所抑制，其方式类似于磁性杂质抑制s波[超导体](@entry_id:191025)的方式 [@problem_id:1173872]。

### 超越平衡：凯尔迪什-南部形式主义

基于虚时间[松原格林函数](@entry_id:199218)的南部-戈尔科夫形式主义本质上是一种平衡理论。为了描述[非平衡现象](@entry_id:198484)，如受光照或载有输运电流的[超导体](@entry_id:191025)，它必须扩展到实时间形式主义。**凯尔迪什-南部形式主义**通过在一个从 $-\infty$ 到 $+\infty$ 再返回的时间轮廓上定义[格林函数](@entry_id:147802)来实现这一点。

这个功能强大但更复杂的框架允许人们推导出依赖于[准粒子](@entry_id:136584)态的实时动力学和占据数的广义运动方程和自洽关系。作为一个例子，[BCS能隙方程](@entry_id:184182)可以推广到[非平衡稳态](@entry_id:141783)。[能隙](@entry_id:191975)大小 $\Delta$ 不再仅取决于温度，而是取决于完整的非平衡准[粒子[分布函](@entry_id:753202)数](@entry_id:145626) $f(E)$。对于一个假设的情况，即[准粒子](@entry_id:136584)被泵浦到系统中，形成一个高达能量 $E_0$ 的布居，[能隙方程](@entry_id:141924)变为 [@problem_id:1173874]：
$$
\frac{1}{N(0)V} = \int_0^{\hbar\omega_D} \frac{1 - 2 f(E_\xi)}{\sqrt{\xi^2 + \Delta^2}} d\xi
$$
这表明，非热的[准粒子](@entry_id:136584)布居（$f(E) > 0$）会减小方程右侧的值，从而抑制[超导能隙](@entry_id:145058)。凯尔迪什-南部形式主义为探索远离平衡的[超导体](@entry_id:191025)丰富而复杂的物理学提供了严格的基础。