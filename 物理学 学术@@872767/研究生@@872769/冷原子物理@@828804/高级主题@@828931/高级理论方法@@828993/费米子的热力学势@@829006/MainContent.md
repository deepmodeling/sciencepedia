## 引言
在连接微观量子世界与宏观[热力学](@entry_id:141121)现象的桥梁中，[费米子](@entry_id:146235)的[热力学势](@entry_id:140516)，特别是[巨势](@entry_id:136286)能，扮演着至关重要的角色。作为[统计物理学](@entry_id:142945)的核心概念，它提供了一个系统性的框架，使我们能够从单个粒子的行为（如能谱和相互作用）出发，精确预测由大量[费米子](@entry_id:146235)组成的系统的集体性质，如压强、熵和热容。然而，如何针对不同物理情境——从[理想气体](@entry_id:200096)到复杂的相互作用系统——具体地计算并运用这一势函数，构成了一个核心的理论挑战。本文旨在系统性地解决这一问题，为读者提供一把理解和分析[量子多体系统](@entry_id:141221)的钥匙。

本文的结构安排旨在引导读者循序渐进地掌握这一强大工具。在“原理与机制”一章中，我们将奠定理论基石，详细推导无[相互作用费米子](@entry_id:160994)的[巨势](@entry_id:136286)能表达式，并介绍处理[连续谱](@entry_id:155477)的态密度方法以及分析低温行为的[索末菲展开](@entry_id:149655)。我们还将初步探讨如何通过[哈特里-福克近似](@entry_id:146529)将相互作用纳入考量。接下来，在“应用与跨学科联系”一章中，我们将展示这些原理在凝聚态物理、[冷原子](@entry_id:144092)物理乃至[拓扑物质](@entry_id:161097)等前沿领域的广泛应用，阐明[巨势](@entry_id:136286)能如何帮助我们理解超导、磁性以及BCS-BEC连续过渡等深刻的物理现象。最后，“动手实践”部分将通过精选的计算练习，帮助读者巩固所学知识，将理论应用于具体问题。

通过这一系列的学习，您将能够深刻理解[费米子](@entry_id:146235)[巨势](@entry_id:136286)能的物理内涵，并掌握其在现代物理研究中的核心应用方法。

## 原理与机制

在[统计物理学](@entry_id:142945)中，[巨势](@entry_id:136286)能 $\Omega$ 是描述宏观系统在[巨正则系综](@entry_id:141562)（固定温度 $T$、体积 $V$ 和化学势 $\mu$）下的核心[热力学函数](@entry_id:755914)。对于由[费米子](@entry_id:146235)组成的系统，由于[泡利不相容原理](@entry_id:141850)的约束，其[巨势](@entry_id:136286)能展现出独特的量子特性。本章将系统地阐述计算[费米子](@entry_id:146235)系统[巨势](@entry_id:136286)能的基本原理，并探讨其在推导系统热力学性质、处理低温现象以及分析相互作用效应中的关键作用。

### 无[相互作用费米子](@entry_id:160994)的[巨势](@entry_id:136286)能

理解复杂系统的第一步往往是从其最简化的、无相互作用的极限开始。对于无相互作用的[费米子](@entry_id:146235)体系，其[巨势](@entry_id:136286)能具有一个简洁而普适的表达式。

#### 基本定义与[因子分解](@entry_id:150389)原理

[巨势](@entry_id:136286)能 $\Omega$ 通过[巨配分函数](@entry_id:154455) $\mathcal{Z}$ 定义：
$$
\Omega = -k_B T \ln \mathcal{Z}
$$
其中 $k_B$ 是[玻尔兹曼常数](@entry_id:142384)，而[巨配分函数](@entry_id:154455)是对所有可能的粒子数 $N$ 的[正则配分函数](@entry_id:154330) $Z_N$ 进行加权求和：
$$
\mathcal{Z} = \sum_{N=0}^{\infty} e^{\beta \mu N} Z_N
$$
这里 $\beta = 1/(k_B T)$。

对于无相互作用的粒子，系统的总能量是占据各个单粒子能态的粒子能量之和。这一特性使得[巨配分函数](@entry_id:154455)可以优美地分解为对所有单粒子能态 $i$ 的独立贡献的乘积：
$$
\mathcal{Z} = \prod_i \mathcal{Z}_i
$$
对于[费米子](@entry_id:146235)，[泡利不相容原理](@entry_id:141850)规定每个单粒子态最多只能容纳一个粒子。因此，对于一个能量为 $\epsilon_i$ 的特定单粒子态，其粒子数只能是 $n_i=0$ 或 $n_i=1$。该能态的[巨配分函数](@entry_id:154455) $\mathcal{Z}_i$ 仅包含这两项：
$$
\mathcal{Z}_i = \sum_{n_i=0}^{1} e^{\beta(\mu - \epsilon_i)n_i} = e^0 + e^{\beta(\mu - \epsilon_i)} = 1 + e^{(\mu - \epsilon_i)/(k_B T)}
$$
将所有单粒子态的贡献相乘，我们得到无[相互作用费米子](@entry_id:160994)体系的总[巨配分函数](@entry_id:154455)，进而得到其[巨势](@entry_id:136286)能的普适公式：
$$
\Omega = -k_B T \ln\left( \prod_i \mathcal{Z}_i \right) = -k_B T \sum_i \ln\left( 1 + e^{(\mu - \epsilon_i)/(k_B T)} \right)
$$
这个公式是研究无[相互作用费米气体](@entry_id:160307)性质的基石。它表明，只要知道了系统的单粒子[能谱](@entry_id:181780) $\{\epsilon_i\}$，就可以立即写出其[巨势](@entry_id:136286)能。

为了更具体地理解这一原理，我们可以考虑一个仅有两个可用单粒子能态（能量分别为 $\epsilon_1$ 和 $\epsilon_2$）的无自旋[费米子](@entry_id:146235)体系[@problem_id:1276128]。我们可以通过显式构造[正则配分函数](@entry_id:154330)来验证上述因子分解。该系统的粒子数 $N$ 只能是 0, 1, 或 2。
- $N=0$: 只有一个状态（真空态），能量为0。$Z_0 = 1$。
- $N=1$: 粒子可以占据 $\epsilon_1$ 或 $\epsilon_2$。$Z_1 = e^{-\beta\epsilon_1} + e^{-\beta\epsilon_2}$。
- $N=2$: 两个能态都被占据。$Z_2 = e^{-\beta(\epsilon_1 + \epsilon_2)}$。

[巨配分函数](@entry_id:154455)为：
$$
\mathcal{Z} = \sum_{N=0}^2 e^{\beta \mu N} Z_N = 1 + e^{\beta\mu}(e^{-\beta\epsilon_1} + e^{-\beta\epsilon_2}) + e^{2\beta\mu}e^{-\beta(\epsilon_1 + \epsilon_2)}
$$
通过简单的代数运算，上式可以被分解为：
$$
\mathcal{Z} = \left(1 + e^{\beta(\mu - \epsilon_1)}\right) \left(1 + e^{\beta(\mu - \epsilon_2)}\right)
$$
这精确地验证了我们的[因子分解](@entry_id:150389)原理。因此，这个简单系统的[巨势](@entry_id:136286)能是两个能态贡献之和：
$$
\Omega = -k_B T \left[ \ln\left(1 + e^{(\mu-\epsilon_1)/(k_B T)}\right) + \ln\left(1 + e^{(\mu-\epsilon_2)/(k_B T)}\right) \right]
$$

#### 物理模型中的应用：[紧束缚模型](@entry_id:143446)

在真实物理系统中，单粒子能谱 $\{\epsilon_i\}$ 并非抽象给定，而是由系统的[哈密顿量](@entry_id:172864)决定的。一个典型的例子是[晶格](@entry_id:196752)中的电子，其行为可以用[紧束缚模型](@entry_id:143446)描述。

考虑一个仅有两个格点（标记为1和2）的一维[晶格](@entry_id:196752)上的无自旋[费米子](@entry_id:146235)。其[哈密顿量](@entry_id:172864)为：
$$
H = \epsilon_0 \sum_{i=1}^2 c_i^\dagger c_i - t \sum_{\langle i,j \rangle} (c_i^\dagger c_j + c_j^\dagger c_i)
$$
其中 $\epsilon_0$ 是在位能，$-t$ 是格点间的跃迁振幅。尽管[费米子](@entry_id:146235)之间没有直接的相互作用，但跃迁项（或称“ hopping”）混合了局域在各个格点的态。在这种情况下，正确的处理方法是首先[对角化](@entry_id:147016)单粒子[哈密顿量](@entry_id:172864)，找到系统的本征能态[@problem_id:1276156]。

在单粒子希尔伯特空间中，以格点态 $\{|1\rangle, |2\rangle\}$ 为基，[哈密顿量](@entry_id:172864)矩阵形式为：
$$
H^{(1)} = \begin{pmatrix} \epsilon_0 & -t \\ -t & \epsilon_0 \end{pmatrix}
$$
对角化该矩阵，我们得到两个本征能量：
$$
\epsilon_{\pm} = \epsilon_0 \pm t
$$
这两个本征能量 $\epsilon_+$ 和 $\epsilon_-$ 构成了系统的“有效”单粒子能谱。现在，整个多体系统可以被看作是[费米子](@entry_id:146235)在两个能量分别为 $\epsilon_+$ 和 $\epsilon_-$ 的独立能级上的填充问题。应用我们之前导出的普适公式，该系统的[巨势](@entry_id:136286)能立刻可以写出：
$$
\Omega(\mu, T) = -k_B T \left[ \ln\left(1+e^{-(\epsilon_+ - \mu)/(k_B T)}\right) + \ln\left(1+e^{-(\epsilon_- - \mu)/(k_B T)}\right) \right]
$$
$$
\Omega(\mu, T) = -k_B T \left[ \ln\left(1+e^{-(\epsilon_0+t-\mu)/(k_B T)}\right) + \ln\left(1+e^{-(\epsilon_0-t-\mu)/(k_B T)}\right) \right]
$$
这个例子揭示了一个深刻的原理：对于任何二次型（无相互作用）的[费米子](@entry_id:146235)[哈密顿量](@entry_id:172864)，总可以通过对角化将其转化为一组独立的[准粒子](@entry_id:136584)模式，而系统的[热力学性质](@entry_id:146047)则由这些[准粒子](@entry_id:136584)的统计分布决定。

### [连续谱](@entry_id:155477)极限与[态密度](@entry_id:147894)

对于宏观系统，单粒子能级数量巨大且间隔极小，以至于它们形成连续的能带。在这种情况下，将分立的求和转化为对能量的积分更为方便。

#### 从求和到积分

转变的关键是引入**[态密度](@entry_id:147894) (Density of States, DOS)** $g(\epsilon)$。$g(\epsilon)d\epsilon$ 定义了能量在 $[\epsilon, \epsilon+d\epsilon]$ 区间内的单粒子态数量。于是，[巨势](@entry_id:136286)能的表达式变为积分形式：
$$
\Omega(T, V, \mu) = -k_B T \int_0^\infty g(\epsilon) \ln\left(1 + e^{(\mu - \epsilon)/(k_B T)}\right) d\epsilon
$$
态密度 $g(\epsilon)$ 是一个与系统维度、粒子[色散关系](@entry_id:140395) $\epsilon(\mathbf{p})$ 以及自旋简并度等密切相关的量。例如，对于质量为 $m$、自旋为 $1/2$ 的三维非相对论性[费米子](@entry_id:146235)，态密度为 $g(\epsilon) = \frac{V}{2\pi^2} (\frac{2m}{\hbar^2})^{3/2} \sqrt{\epsilon}$。

#### 零温极限

在零温极限下（$T \to 0$），[费米-狄拉克分布](@entry_id:138909)函数 $f(\epsilon) = [e^{(\epsilon-\mu)/(k_B T)}+1]^{-1}$ 变为一个[阶跃函数](@entry_id:159192)：当 $\epsilon  \mu$ 时 $f(\epsilon)=1$，当 $\epsilon  \mu$ 时 $f(\epsilon)=0$。此时，化学势 $\mu$ 等于[费米能](@entry_id:143977) $\epsilon_F$。$\ln(1+e^{\beta(\mu-\epsilon)})$ 这一项在 $T \to 0$ 时，当 $\epsilon  \mu$ 时趋向于 $\beta(\mu-\epsilon)$，而当 $\epsilon  \mu$ 时趋向于0。因此，[巨势](@entry_id:136286)能的积分可以简化为：
$$
\Omega(T \to 0) = -\int_0^{\mu} (\mu - \epsilon) g(\epsilon) d\epsilon
$$
这个表达式有一个直观的物理解释。在零温下，所有能量低于 $\mu=\epsilon_F$ 的态都被占据。系统的总能量 $E = \int_0^{\mu} \epsilon g(\epsilon) d\epsilon$，总粒子数 $N = \int_0^{\mu} g(\epsilon) d\epsilon$。因此，
$$
\Omega(T \to 0) = \int_0^{\mu} \epsilon g(\epsilon) d\epsilon - \mu \int_0^{\mu} g(\epsilon) d\epsilon = E - \mu N
$$
这正是[巨势](@entry_id:136286)能与内能 $E$ 之间通过[勒让德变换](@entry_id:146727)建立的关系。

作为一个具体的计算范例，考虑一个二维的、具有[线性色散关系](@entry_id:266313) $\epsilon(\mathbf{p}) = v_F |\mathbf{p}|$ 的自旋-$1/2$ [费米子](@entry_id:146235)体系（例如石墨烯中的低能电子）[@problem_id:1276243]。其态密度（包括自旋简并度 $g_s=2$）为 $g(\epsilon) = \frac{A \epsilon}{\pi \hbar^2 v_F^2}$，其中 $A$ 是系统面积。在零温下，
$$
N = \int_0^{\mu} g(\epsilon) d\epsilon = \frac{A}{\pi\hbar^2 v_F^2} \int_0^{\mu} \epsilon d\epsilon = \frac{A \mu^2}{2\pi\hbar^2 v_F^2}
$$
$$
E = \int_0^{\mu} \epsilon g(\epsilon) d\epsilon = \frac{A}{\pi\hbar^2 v_F^2} \int_0^{\mu} \epsilon^2 d\epsilon = \frac{A \mu^3}{3\pi\hbar^2 v_F^2}
$$
因此，零温[巨势](@entry_id:136286)能为：
$$
\Omega = E - \mu N = \frac{A\mu^3}{3\pi\hbar^2 v_F^2} - \mu \left( \frac{A\mu^2}{2\pi\hbar^2 v_F^2} \right) = -\frac{A\mu^3}{6\pi\hbar^2 v_F^2}
$$
这个结果展示了如何从一个给定的单粒子色散关系出发，通过[态密度](@entry_id:147894)计算出系统的基本[热力学势](@entry_id:140516)。

#### 从[巨势](@entry_id:136286)能推导热力学性质

[巨势](@entry_id:136286)能的强大之处在于它是生成其他所有宏观[热力学](@entry_id:141121)量的“母函数”。例如，压强 $P$ 和粒子数 $N$ 可以通过对 $\Omega$ 求导得到：
$$
P = -\left(\frac{\partial \Omega}{\partial V}\right)_{T,\mu}, \quad N = -\left(\frac{\partial \Omega}{\partial \mu}\right)_{T,V}
$$
对于均匀系统，$\Omega$ 正比于体积 $V$，因此压强可简化为 $P = -\Omega/V$。

我们可以利用这一关系来计算一个宏观可测量——等温[压缩系数](@entry_id:272630) $\kappa_T$。其定义为 $\kappa_T = -\frac{1}{V}(\frac{\partial V}{\partial P})_{T,N}$。对于一个三维[理想费米气体](@entry_id:153500)，在零温下，我们首先需要计算其[巨势](@entry_id:136286)能[@problem_id:1276226]。使用三维态密度 $g(\epsilon) \propto V\sqrt{\epsilon}$，零温[巨势](@entry_id:136286)能积分为：
$$
\Omega = -\int_0^{\mu} (\mu-\epsilon) g(\epsilon) d\epsilon = -C V \int_0^{\mu} (\mu\epsilon^{1/2} - \epsilon^{3/2}) d\epsilon = -\frac{4}{15} C V \mu^{5/2}
$$
其中 $C = \frac{1}{4\pi^2}(\frac{2m}{\hbar^2})^{3/2}$。在 $T=0$ 时 $\mu=\epsilon_F$，所以压强为：
$$
P = -\frac{\Omega}{V} = \frac{4}{15} C \epsilon_F^{5/2}
$$
另一方面，粒子数密度 $n=N/V$ 与费米能的关系是 $n = \int_0^{\epsilon_F} g(\epsilon)/V d\epsilon = \frac{2}{3}C\epsilon_F^{3/2}$。结合这两个关系，我们可以得到著名的状态方程 $P = \frac{2}{5} n \epsilon_F$。由于 $\epsilon_F \propto n^{2/3}$，我们有 $P \propto n^{5/3}$。
等温[压缩系数](@entry_id:272630)可以表示为 $\kappa_T = \frac{1}{n}(\frac{\partial n}{\partial P})_T$。利用 $P \propto n^{5/3}$，我们得到 $(\frac{\partial P}{\partial n})_T = \frac{5}{3} \frac{P}{n} = \frac{5}{3} (\frac{2}{5}\epsilon_F) = \frac{2}{3}\epsilon_F$。最终，
$$
\kappa_T = \frac{1}{n(\partial P/\partial n)_T} = \frac{3}{2n\epsilon_F}
$$
这个结果表明，费米气体的“硬度”（难以压缩的程度）由其密度和费米能决定。这是[量子简并](@entry_id:146335)压力的直接体现。

### 低温性质与[索末菲展开](@entry_id:149655)

当温度 $T$ 很低但非零时（$k_B T \ll \epsilon_F$），[费米面](@entry_id:137798)附近的热激发变得重要。精确[计算热力学](@entry_id:148023)积分通常很困难，但我们可以使用**索末菲 (Sommerfeld) 展开**这一强大的近似方法。

[索末菲展开](@entry_id:149655)适用于形如 $I = \int_0^\infty \phi(\epsilon) f(\epsilon) d\epsilon$ 的积分，其中 $f(\epsilon)$ 是费米分布函数，$\phi(\epsilon)$ 是一个在 $\epsilon=\mu$ 附近行为良好的函数。其展开式为：
$$
\int_0^\infty \phi(\epsilon) f(\epsilon) d\epsilon \approx \int_0^\mu \phi(\epsilon) d\epsilon + \frac{\pi^2}{6}(k_B T)^2 \phi'(\mu) + \mathcal{O}(T^4)
$$
这个展开式的物理意义是，低温下的修正主要来自[费米能级](@entry_id:143215) $\mu$ 附近一个宽度约为 $k_B T$ 的能量窗口内的粒子激发。

#### 熵与比热

根据[热力学](@entry_id:141121)第三定律，任何系统在 $T=0$ 时的熵为零。[索末菲展开](@entry_id:149655)使我们能够计算低温下熵的领头项。熵可以通过对[巨势](@entry_id:136286)能求导得到 $S = -(\partial \Omega / \partial T)_{V,\mu}$。通过对[巨势](@entry_id:136286)能的积分表达式进行精巧的计算，或者直接对熵的[统计力](@entry_id:194984)学表达式 $S = -k_B \sum_i [f_i \ln f_i + (1-f_i) \ln(1-f_i)]$ 进行[索末菲展开](@entry_id:149655)，可以得到一个普适的低温结果：
$$
S(T) \approx \frac{\pi^2}{3} g(\mu) k_B^2 T
$$
在低温极限下，$\mu \approx \epsilon_F$。这个结果表明，费米气体的熵在低温下与温度成正比，这是[费米液体理论](@entry_id:144069)的一个标志性特征。

对于三维[理想费米气体](@entry_id:153500)，我们有 $g(\epsilon_F) = \frac{3N}{2\epsilon_F}$[@problem_id:1276145]。代入上式可得：
$$
S \approx \frac{\pi^2}{3} \left(\frac{3N}{2\epsilon_F}\right) k_B^2 T = \frac{\pi^2}{2} N k_B \frac{k_B T}{\epsilon_F}
$$
比热 $C_V = T(\partial S / \partial T)_N$ 相应地也与 $T$ 成正比。

有趣的是，不同维度和色散关系下的细节会有所不同。例如，对于二维[理想费米气体](@entry_id:153500)，其[态密度](@entry_id:147894) $g(\epsilon)=g_0$ 是一个常数[@problem_id:1276143]。这意味着 $g(\mu)$ 不依赖于 $\mu$。一个重要的推论是，在这种特殊情况下，化学势在一阶温度修正下保持不变，即 $\mu(T) \approx \mu_F$。熵的表达式仍然是 $S = \frac{\pi^2}{3} g_0 k_B^2 T$。利用零温关系 $N=g_0 \mu_F = g_0 k_B T_F$（其中 $T_F$ 是[费米温度](@entry_id:148320)），我们可以得到比热为：
$$
C_A = T\frac{dS}{dT} = \frac{\pi^2}{3} g_0 k_B^2 T = \frac{\pi^2}{3} N k_B \frac{T}{T_F}
$$
单位粒子的比热为 $c_A = \frac{\pi^2}{3} k_B \frac{T}{T_F}$。尽管推导细节不同，但低温下比热与温度成线性的行为是[费米子](@entry_id:146235)体系的共同特征。

#### 其他热力学势：吉布斯自由能

[巨势](@entry_id:136286)能是研究 $(T,V,\mu)$ 系综的自然选择，但实验上常常控制的是压强 $P$。这时，[吉布斯自由能](@entry_id:146774) $G(T,P,N)$ 更加适用。$G$ 可以通过[勒让德变换](@entry_id:146727)从 $\Omega$ 获得：$G = \Omega + \mu N$。在 $(T,P,N)$ 系综中，$\mu$ 是一个依赖于 $(T,P)$ 的量，因此 $G=\mu(T,P)N$。

我们的任务是找到在恒定压强 $P$ 和粒子数 $N$ 下，$\mu$ 如何随低温 $T$ 变化[@problem_id:1276153]。我们可以利用[索末菲展开](@entry_id:149655)得到的压强和粒子[数密度](@entry_id:268986)的表达式：
$$
P \approx \frac{2}{5} n \mu \left[1 + \frac{5\pi^2}{8}\left(\frac{k_B T}{\mu}\right)^2\right]
$$
令 $T=0$ 时的费米能为 $\epsilon_{FP}$（由压强 $P$ 决定），并设 $\mu(T) = \epsilon_{FP}(1+\delta)$。通过保持压强 $P$ 不变，我们可以解出修正项 $\delta$。经过计算，可得：
$$
\mu(T,P) \approx \epsilon_{FP}\left[1 - \frac{\pi^2}{4}\left(\frac{k_B T}{\epsilon_{FP}}\right)^2\right]
$$
于是，低温下的[吉布斯自由能](@entry_id:146774)为：
$$
G(N,P,T) = N \mu(T,P) \approx N\epsilon_{FP} - \frac{\pi^2}{4} \frac{N k_B^2 T^2}{\epsilon_{FP}}
$$
这个结果描述了在恒压条件下，[费米气体](@entry_id:145305)的能量如何随温度降低。

### [相互作用费米子](@entry_id:160994)的[巨势](@entry_id:136286)能

真实世界中的[费米子](@entry_id:146235)总是存在相互作用，这使得问题变得异常复杂。对于[弱相互作用](@entry_id:157579)体系，微扰论是处理该问题的标准方法。在零温下，对[巨势](@entry_id:136286)能的[一阶修正](@entry_id:155896)等于对基态能量的[一阶修正](@entry_id:155896)，$\Omega^{(1)} = E^{(1)}$。

#### 哈特里（Hartree）直接项

哈特里-福克 ([Hartree-Fock](@entry_id:142303)) 近似是处理相互作用的第一个层次。它包含两个贡献：哈特里项和福克项。

**哈特里项**，或称直接项，具有经典直观的物理图像：它描述了某个粒子与系统中所有其他粒子形成的*平均*[电荷](@entry_id:275494)（或密度）[分布](@entry_id:182848)之间的相互作用。其能量贡献为：
$$
U_H = \frac{1}{2} \int d^3r_1 d^3r_2 \, n(\mathbf{r}_1) V(\mathbf{r}_1 - \mathbf{r}_2) n(\mathbf{r}_2)
$$
对于密度为 $n$ 的均匀气体，上式简化为：
$$
U_H = \frac{1}{2} V n^2 \int d^3r \, V(\mathbf{r}) = \frac{1}{2} N n \tilde{V}(\mathbf{q}=0)
$$
其中 $\tilde{V}(\mathbf{q})$ 是相互作用[势的傅里叶变换](@entry_id:149425)。这表明哈特里能仅[对相互作用势](@entry_id:140875)的零动量分量（即空间积分）敏感。

例如，对于一个由高斯势 $V(\mathbf{r}) = V_0 \exp(-r^2/a^2)$ 描述的相互作用，其空间积分为 $\int V(\mathbf{r}) d^3r = V_0 (\pi a^2)^{3/2}$[@problem_id:1276196]。因此，哈特里能对每个粒子的贡献为：
$$
\frac{\Omega_H^{(1)}}{N} = \frac{U_H}{N} = \frac{n}{2} \int V(\mathbf{r}) d^3r = \frac{n V_0 \pi^{3/2} a^3}{2}
$$

#### 福克（Fock）交换项

**福克项**，或称交换项，是一个纯粹的量子力学效应，源于[费米子](@entry_id:146235)[波函数](@entry_id:147440)的[反对称性](@entry_id:261893)要求。它没有经典类比，可以理解为自旋平行的[费米子](@entry_id:146235)之间由于[泡利不相容原理](@entry_id:141850)而产生的一种有效排斥（或者说，它修正了哈特里项中包含的粒子与自身的虚假相互作用）。其能量表达式为：
$$
E_F^{(1)} = -\frac{1}{2V} \sum_{\mathbf{k},\mathbf{k'}} n_{\mathbf{k}} n_{\mathbf{k'}} \tilde{V}(\mathbf{k}-\mathbf{k'})
$$
其中 $n_{\mathbf{k}}$ 是动量为 $\mathbf{k}$ 的态的占据数（在 $T=0$ 时是费米球内的阶跃函数）。这个计算涉及到对费米球内的两个动量进行积分，是一个卷积形式。

考虑一个相互作用[势的傅里叶变换](@entry_id:149425)为 $\tilde{V}(\mathbf{q}) = U_0/q^2$ 的[自旋极化费米气体](@entry_id:160585)[@problem_id:1276136]。通过复杂的[动量空间](@entry_id:148936)积分，可以得到交换能密度：
$$
\frac{E_F^{(1)}}{V} = -\frac{U_0 k_F^4}{32\pi^4}
$$
其中 $k_F$ 是[费米动量](@entry_id:147114)。由于压强 $P = -\Omega/V$，[交换相互作用](@entry_id:140006)对压强的修正为：
$$
P_F^{(1)} = -\frac{\Omega_F^{(1)}}{V} = -\frac{E_F^{(1)}}{V} = \frac{U_0 k_F^4}{32\pi^4}
$$
这个正的压强修正反映了交换效应带来的额外排斥。

#### 应用：相互作用费米气的相稳定性

[巨势](@entry_id:136286)能（或与之密切相关的[能量密度泛函](@entry_id:161351)）的一个重要应用是判断多组分系统的宏观相稳定性。考虑一个由自旋向上 ($\uparrow$) 和向下 ($\downarrow$) 两种[费米子](@entry_id:146235)组成的混合气体，它们之间存在排斥性[接触相互作用](@entry_id:150822) $g  0$。其能量密度可以近似写为动能和哈特里相互作用能之和[@problem_id:1276221]：
$$
\mathcal{E}(n_\uparrow, n_\downarrow) = \mathcal{E}_{kin}(n_\uparrow) + \mathcal{E}_{kin}(n_\downarrow) + g n_\uparrow n_\downarrow
$$
其中 $\mathcal{E}_{kin}(n) \propto n^{5/3}$。

一个均匀的混合相要能稳定存在，其能量密度 $\mathcal{E}$ 必须是关于密度 $(n_\uparrow, n_\downarrow)$ 的凸函数。在数学上，这意味着其[二阶导数](@entry_id:144508)的海森 (Hessian) 矩阵必须是正定的。当系统参数（如相互作用强度或极化率 $P=(n_\uparrow-n_\downarrow)/n$）变化时，海森[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)可能变为零或负，标志着均匀相失稳，系统会自发地分离成两个或多个具有不同密度的相。

失稳的临界条件是 $\det(H) = 0$，其中 $H_{ij} = \frac{\partial^2 \mathcal{E}}{\partial n_i \partial n_j}$。计算[海森矩阵](@entry_id:139140)的元素并令其[行列式](@entry_id:142978)为零，我们得到一个关于相互作用强度 $g$、总密度 $n$ 和[极化率](@entry_id:143513) $P$ 的方程。这个方程定义了相分离的[临界点](@entry_id:144653)。对于一个给定的[极化率](@entry_id:143513)，例如 $P=\sqrt{3}/2$，我们可以解出导致不稳定的临界[相互作用强度](@entry_id:192243) $(k_F a)_c$ (其中 $k_F a$ 是无量纲化的相互作用参数)。计算表明：
$$
(k_F a)_c = \frac{\pi}{2} 2^{1/3}
$$
当[相互作用强度](@entry_id:192243)超过这个临界值时，原本均匀混合的[费米气体](@entry_id:145305)将不再稳定，倾向于分离成一个纯的多数自旋相和一个混合的少数自旋相。这一现象与[铁磁性](@entry_id:137256)中的斯通纳 (Stoner) 不稳定性密切相关，展示了如何利用从[巨势](@entry_id:136286)能出发的能量泛函来预测由相互作用驱动的宏观量子相变。