## 引言
在信号处理与系统建模领域，理解信号的内在属性是进行有效分析与设计的前提。其中，根据能量和功率对信号进行表征，是最基本也是最深刻的维度之一。然而，学生和工程师们常常在掌握了数学定义后，难以将其与物理世界的实际问题和跨学科应用联系起来，从而无法充分发挥这些概念的威力。本文旨在填补这一鸿沟。我们将首先在“原理与机制”一章中，从第一性原理出发，严谨构建能量与[功率信号](@entry_id:196112)的理论框架。随后，在“应用与跨学科联系”一章中，我们将展示这些理论如何在通信、控制、声学乃至生物学等领域大放异彩。最后，通过“动手实践”环节，您将有机会亲手解决具体问题，巩固所学。现在，让我们从能量与[功率信号](@entry_id:196112)表征的基本原理与机制开始，踏上这段探索之旅。

## 原理与机制

在[信号与系统](@entry_id:274453)分析中，一个基本而关键的任务是对信号进行分类和表征。这种表征不仅有助于我们从理论上理解信号的结构，更在通信、控制、声学和生物医学工程等众多应用领域中具有直接的实践意义。本章将深入探讨信号的两个核心属性：**能量**与**功率**。我们将从第一性原理出发，建立连续时间与[离散时间信号](@entry_id:272771)的能量和功率的严谨定义，并探讨它们在时域和[频域](@entry_id:160070)中的表现形式。随后，我们会将这些基本概念应用于分析更为复杂的场景，包括[LTI系统的响应](@entry_id:274375)、[随机过程](@entry_id:159502)的特性以及信号处理中的实际问题。

### [信号能量](@entry_id:264743)与功率的基本概念

将信号按能量和功率进行分类，其动机源于物理学。在[电路理论](@entry_id:189041)中，如果一个信号 $x(t)$ 代表通过一个单位电阻（$R=1\,\Omega$）的电压或电流，那么其[瞬时功率](@entry_id:174754)就是 $|x(t)|^2$。因此，信号在一段时间内的总能量或其长期[平均功率](@entry_id:271791)，就直接对应于物理世界中能量的消耗或功率的耗散。这个物理类比为我们提供了理解这些抽象数学定义的直观基础。

#### [连续时间信号](@entry_id:268088)

对于一个连续时间 (CT) 信号 $x(t)$，我们定义其在整个时间轴上的**总能量** (Total Energy) 为：
$$ E = \int_{-\infty}^{\infty} |x(t)|^2 dt $$

而其**[平均功率](@entry_id:271791)** (Average Power) 则定义为信号在无限长时间内的平均能量：
$$ P = \lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} |x(t)|^2 dt $$

基于这两个定义，我们可以将信号分为三类：

1.  **[能量信号](@entry_id:190524) (Energy Signals)**：如果一个信号的总能量 $E$ 是一个有限的正数 ($0  E  \infty$)，那么它就是一个[能量信号](@entry_id:190524)。对于[能量信号](@entry_id:190524)，其能量集中在有限的时间范围内，因此在无限长的时间上取平均，其平均功率必然为零 ($P=0$)。这类信号通常是瞬态的或有明确起止时间的。

    一个典型的例子是双边指数衰减信号 $x_1(t) = e^{-2|t|}$ [@problem_id:2869245]。它的总能量可以通[过积分](@entry_id:753033)计算：
    $$ E_1 = \int_{-\infty}^{\infty} |e^{-2|t|}|^2 dt = \int_{-\infty}^{\infty} e^{-4|t|} dt $$
    由于被积函数是[偶函数](@entry_id:163605)，我们可以简化计算：
    $$ E_1 = 2 \int_{0}^{\infty} e^{-4t} dt = 2 \left[ -\frac{1}{4}e^{-4t} \right]_{0}^{\infty} = 2 \left( 0 - \left(-\frac{1}{4}\right) \right) = \frac{1}{2} $$
    因为 $0  E_1 = 1/2  \infty$，所以 $x_1(t)$ 是一个[能量信号](@entry_id:190524)。

2.  **[功率信号](@entry_id:196112) (Power Signals)**：如果一个信号的[平均功率](@entry_id:271791) $P$ 是一个有限的正数 ($0  P  \infty$)，那么它就是一个[功率信号](@entry_id:196112)。对于[功率信号](@entry_id:196112)，由于其功率在无限长的时间上持续存在，其总能量必然是无限的 ($E = \infty$)。[周期信号](@entry_id:266688)（非零）是[功率信号](@entry_id:196112)最常见的例子，但并非所有[功率信号](@entry_id:196112)都是周期的。

    考虑信号 $x_2(t) = u(t)\cos(t)$，其中 $u(t)$ 是[单位阶跃函数](@entry_id:268807) [@problem_id:2869245]。这是一个因果[正弦信号](@entry_id:196767)。它的总能量是无限的，因为积分 $\int_{0}^{\infty} \cos^2(t) dt$ 发散。我们来计算它的[平均功率](@entry_id:271791)：
    $$ P_2 = \lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} |u(t)\cos(t)|^2 dt = \lim_{T \to \infty} \frac{1}{2T} \int_{0}^{T} \cos^2(t) dt $$
    使用[三角恒等式](@entry_id:165065) $\cos^2(t) = \frac{1}{2}(1 + \cos(2t))$:
    $$ P_2 = \lim_{T \to \infty} \frac{1}{4T} \int_{0}^{T} (1 + \cos(2t)) dt = \lim_{T \to \infty} \frac{1}{4T} \left[ t + \frac{1}{2}\sin(2t) \right]_{0}^{T} $$
    $$ P_2 = \lim_{T \to \infty} \left( \frac{1}{4} + \frac{\sin(2T)}{8T} \right) = \frac{1}{4} $$
    由于 $0  P_2 = 1/4  \infty$，所以 $x_2(t)$ 是一个[功率信号](@entry_id:196112)。

3.  **既非[能量信号](@entry_id:190524)也非[功率信号](@entry_id:196112)**：有些信号既不满足[能量信号](@entry_id:190524)的条件，也不满足[功率信号](@entry_id:196112)的条件。例如，其总能量和平均功率都为无限大（如 $x(t) = t$），或者总能量无限大但[平均功率](@entry_id:271791)为零。

#### [离散时间信号](@entry_id:272771)

对于离散时间 (DT) 信号 $x[n]$，能量和功率的定义与连续时间情况类似，只是积分被求和所取代。

**总能量**定义为：
$$ E = \sum_{n=-\infty}^{\infty} |x[n]|^2 $$

**平均功率**定义为：
$$ P = \lim_{N \to \infty} \frac{1}{2N+1} \sum_{n=-N}^{N} |x[n]|^2 $$

分类标准与[连续时间信号](@entry_id:268088)相同。

例如，信号 $x_3[n] = (\frac{1}{2})^{|n|}$ [@problem_id:2869245] 是一个[能量信号](@entry_id:190524)。其能量为：
$$ E_3 = \sum_{n=-\infty}^{\infty} \left| \left(\frac{1}{2}\right)^{|n|} \right|^2 = \sum_{n=-\infty}^{\infty} \left(\frac{1}{4}\right)^{|n|} $$
这是一个对称的几何序列求和，可以分为 $n=0$ 的项和 $n \ne 0$ 的项：
$$ E_3 = 1 + 2 \sum_{n=1}^{\infty} \left(\frac{1}{4}\right)^{n} = 1 + 2 \left( \frac{1/4}{1-1/4} \right) = 1 + 2 \left(\frac{1}{3}\right) = \frac{5}{3} $$
由于 $0  E_3  \infty$，这是一个[能量信号](@entry_id:190524)。

然而，信号 $x_4[n] = \frac{1}{\sqrt{|n|+1}}$ [@problem_id:2869245] 既非[能量信号](@entry_id:190524)也非[功率信号](@entry_id:196112)。其能量 $E_4 = \sum_{n=-\infty}^{\infty} \frac{1}{|n|+1}$ 是一个发散的级数（调和级数的一种形式），所以 $E_4 = \infty$。其功率 $P_4 = \lim_{N \to \infty} \frac{1}{2N+1} \sum_{n=-N}^{N} \frac{1}{|n|+1}$，由于求和项的增长速度（约等于 $2\ln(N)$）慢于分母的增长速度（$2N+1$），极限为零。因此，该[信号能量](@entry_id:264743)无限，功率为零，不属于任何一类。

#### 复合信号的属性

在实际应用中，信号往往是多个分量的叠加。一个常见且重要的情况是一个[功率信号](@entry_id:196112) $s(t)$ 与一个[能量信号](@entry_id:190524) $r(t)$ 的叠加，即 $x(t) = s(t) + r(t)$。例如，一个[稳态](@entry_id:182458)的[周期信号](@entry_id:266688)（[功率信号](@entry_id:196112)）上叠加了一个瞬态的扰动（[能量信号](@entry_id:190524)）[@problem_id:2869250]。

$x(t)$ 的平均功率为：
$$ P_x = \lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} |s(t) + r(t)|^2 dt $$
$$ P_x = \lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} (|s(t)|^2 + |r(t)|^2 + 2\operatorname{Re}\{s(t)r^*(t)\}) dt $$
$$ P_x = P_s + P_r + P_{sr} $$
这里 $P_s$ 和 $P_r$ 分别是 $s(t)$ 和 $r(t)$ 的平均功率，$P_{sr}$ 是互功率项。由于 $r(t)$ 是[能量信号](@entry_id:190524)，其平均功率 $P_r=0$。同时，可以证明，只要 $s(t)$ 和 $r(t)$ 至少一个是功率有界的，并且另一个是能量有界的，那么它们的互功率项 $P_{sr}$ 也为零。这是因为[能量信号](@entry_id:190524)的[能量集中](@entry_id:203621)在有限时间内，在无限长时间的平均过程中其贡献可以忽略不计。

因此，我们得到一个重要结论：**一个[功率信号](@entry_id:196112)与一个[能量信号](@entry_id:190524)之和仍然是一个[功率信号](@entry_id:196112)，且其[平均功率](@entry_id:271791)等于原[功率信号](@entry_id:196112)的平均功率**。
$$ P_{s+r} = P_s $$
这个性质在分析含有[瞬态响应](@entry_id:165150)的[稳态](@entry_id:182458)系统时非常有用，它允许我们将瞬态部分（[能量信号](@entry_id:190524)）与[稳态](@entry_id:182458)部分（[功率信号](@entry_id:196112)）分开处理，从而简化功率计算 [@problem_id:2869250]。

### [频域](@entry_id:160070)表征：谱密度

虽然时域定义为能量和功率提供了基础，但[频域分析](@entry_id:265642)揭示了能量或功率是如何在不同频率上[分布](@entry_id:182848)的。这种[分布](@entry_id:182848)由**谱密度**来描述。

#### [能量谱密度](@entry_id:270564) (ESD)

对于[能量信号](@entry_id:190524)，**[帕塞瓦尔定理](@entry_id:139215)**建立了时域能量与[频域](@entry_id:160070)表示之间的桥梁。对于一个[连续时间信号](@entry_id:268088) $x(t)$ 及其[傅里叶变换](@entry_id:142120) $X(\omega) = \int_{-\infty}^{\infty} x(t) e^{-j\omega t} dt$，[帕塞瓦尔定理](@entry_id:139215)表明：
$$ E_x = \int_{-\infty}^{\infty} |x(t)|^2 dt = \frac{1}{2\pi} \int_{-\infty}^{\infty} |X(\omega)|^2 d\omega $$
这个定理告诉我们，信号的总能量等于其[傅里叶变换](@entry_id:142120)的模平方在所有频率上积分的结果（乘以一个归一化因子 $1/(2\pi)$）。

这启发我们定义**[能量谱密度](@entry_id:270564) (Energy Spectral Density, ESD)** $\Psi_x(\omega)$ 为：
$$ \Psi_x(\omega) = |X(\omega)|^2 $$
ESD 描述了[信号能量](@entry_id:264743)在[角频率](@entry_id:261565) $\omega$ 上的[分布](@entry_id:182848)密度。$\Psi_x(\omega)$ 在某个频段上的积分就等于信号在该频段内的能量。

让我们通过一个例子来推导ESD。考虑信号 $x(t) = e^{-\alpha|t|} \cos(\beta t + \phi)$，其中 $\alpha  0$ [@problem_id:2869246]。这是一个阻尼振荡信号，属于[能量信号](@entry_id:190524)。
首先，利用[欧拉公式](@entry_id:176440)将 $x(t)$ 展开：
$$ x(t) = \frac{1}{2}e^{j\phi} e^{-\alpha|t|}e^{j\beta t} + \frac{1}{2}e^{-j\phi} e^{-\alpha|t|}e^{-j\beta t} $$
我们知道 $e^{-\alpha|t|}$ 的[傅里叶变换](@entry_id:142120)是 $\frac{2\alpha}{\alpha^2 + \omega^2}$。利用[傅里叶变换](@entry_id:142120)的[频移特性](@entry_id:272563) $\mathcal{F}\{f(t)e^{j\omega_0 t}\} = F(\omega - \omega_0)$，我们可以得到 $X(\omega)$：
$$ X(\omega) = \frac{1}{2}e^{j\phi} \frac{2\alpha}{\alpha^2 + (\omega-\beta)^2} + \frac{1}{2}e^{-j\phi} \frac{2\alpha}{\alpha^2 + (\omega+\beta)^2} $$
经过复杂的代数化简，将两项通分并整理，可以得到 $X(\omega)$ 的实部和虚部，进而计算其模的平方 $|X(\omega)|^2$。最终得到的ESD为：
$$ \Psi_x(\omega) = |X(\omega)|^2 = \frac{4\alpha^2 \left( (\alpha^2 + \omega^2 + \beta^2)^2\cos^2(\phi) + 4\omega^2\beta^2\sin^2(\phi) \right)}{(\alpha^2 + \omega^2 + \beta^2)^2 - 4\omega^2\beta^2} $$
这个表达式虽然复杂，但清晰地展示了能量是如何作为频率 $\omega$ 的函数进行[分布](@entry_id:182848)的，其形状受到阻尼因子 $\alpha$、[振荡频率](@entry_id:269468) $\beta$ 和相位 $\phi$ 的共同影响。

#### 功率谱密度 (PSD)

对于[功率信号](@entry_id:196112)，其总能量无限，因此ESD的概念不再适用。取而代之的是**功率谱密度 (Power Spectral Density, PSD)**，它描述了信号的功率在频率上的[分布](@entry_id:182848)。

对于[广义平稳](@entry_id:144146) (Wide-Sense Stationary, WSS) [随机过程](@entry_id:159502)，**[维纳-辛钦定理](@entry_id:188017)** 给出了PSD的定义。该定理指出，一个WSS过程的PSD $S_x(\omega)$ 是其**自相关函数 (Autocorrelation Function)** $R_x(\tau)$ 的[傅里叶变换](@entry_id:142120)。

[自相关函数](@entry_id:138327)描述了一个信号在不同时间点上的相似性，对于WSS过程，它定义为：
$$ R_x(\tau) = E[x(t) x^*(t-\tau)] $$
其中 $E[\cdot]$ 表示期望运算。

因此，功率谱密度为：
$$ S_x(\omega) = \mathcal{F}\{R_x(\tau)\} = \int_{-\infty}^{\infty} R_x(\tau) e^{-j\omega\tau} d\tau $$
PSD $S_x(\omega)$ 的一个重要性质是，它的总积分（除以 $2\pi$）等于信号的总[平均功率](@entry_id:271791)：
$$ P_x = R_x(0) = \frac{1}{2\pi} \int_{-\infty}^{\infty} S_x(\omega) d\omega $$

考虑一个零均值的WSS[随机过程](@entry_id:159502)，其自相关函数为 $R_x(\tau) = \sigma^2 e^{-\alpha|\tau|} \cos(\omega_0\tau)$ [@problem_id:2869243]。这可以模拟一个带通随机信号。其PSD可以通过对 $R_x(\tau)$ 进行[傅里叶变换](@entry_id:142120)得到。
利用与ESD推导中相似的技巧，我们将 $\cos(\omega_0\tau)$ 用欧拉公式展开，并利用[频移特性](@entry_id:272563)：
$$ S_x(\omega) = \mathcal{F}\{\sigma^2 e^{-\alpha|\tau|} \frac{1}{2}(e^{j\omega_0\tau} + e^{-j\omega_0\tau})\} $$
$$ S_x(\omega) = \frac{\sigma^2}{2} \left( \mathcal{F}\{e^{-\alpha|\tau|}\}|_{\omega-\omega_0} + \mathcal{F}\{e^{-\alpha|\tau|}\}|_{\omega+\omega_0} \right) $$
代入 $e^{-\alpha|\tau|}$ 的[傅里叶变换](@entry_id:142120) $\frac{2\alpha}{\alpha^2 + \omega^2}$，我们得到：
$$ S_x(\omega) = \frac{\sigma^2}{2} \left( \frac{2\alpha}{\alpha^2 + (\omega-\omega_0)^2} + \frac{2\alpha}{\alpha^2 + (\omega+\omega_0)^2} \right) $$
$$ S_x(\omega) = \sigma^2 \alpha \left( \frac{1}{\alpha^2 + (\omega - \omega_0)^2} + \frac{1}{\alpha^2 + (\omega + \omega_0)^2} \right) $$
这个PSD由两个以 $\pm\omega_0$为中心的洛伦兹峰构成，清晰地描绘了一个中心频率在 $\omega_0$ 附近的带通[随机过程](@entry_id:159502)的功率[分布](@entry_id:182848)。

#### [离散时间信号](@entry_id:272771)的[帕塞瓦尔定理](@entry_id:139215)

与连续时间情况相对应，[帕塞瓦尔定理](@entry_id:139215)同样适用于[离散时间信号](@entry_id:272771)及其[频域](@entry_id:160070)表示。

对于使用**[离散时间傅里叶变换 (DTFT)](@entry_id:204279)**, $X(e^{j\omega}) = \sum_{n=-\infty}^{\infty} x[n]e^{-j\omega n}$ 的[非周期信号](@entry_id:266525)，定理形式为：
$$ E_x = \sum_{n=-\infty}^{\infty} |x[n]|^2 = \frac{1}{2\pi} \int_{-\pi}^{\pi} |X(e^{j\omega})|^2 d\omega $$
这表明[离散时间信号](@entry_id:272771)的总能量等于其DTFT的模平方在一个周期 ($2\pi$) [内积](@entry_id:158127)分的结果。

对于使用**[离散傅里叶变换](@entry_id:144032) (DFT)**, $Y[k] = \sum_{n=0}^{N-1} y[n] e^{-j\frac{2\pi}{N}kn}$ 的长度为 $N$ 的有限长序列，定理形式为：
$$ \sum_{n=0}^{N-1} |y[n]|^2 = \frac{1}{N} \sum_{k=0}^{N-1} |Y[k]|^2 $$
这两个定理之间有着深刻的联系[@problem_id:2869251]。DFT可以看作是在DTFT[频谱](@entry_id:265125)上的采样。当我们将一个无限长的[能量信号](@entry_id:190524) $x[n]$ 进行截断，得到长度为 $N$ 的序列 $y_N[n]$，并计算其DFT能量时，随着 $N \to \infty$，这个基于DFT的有限能量和会收敛到原信号的总能量。同时，根据[黎曼和](@entry_id:137667)的定义，DFT能量表达式 $\frac{1}{N}\sum |Y_N[k]|^2$ 在极限情况下会收敛到DTFT能量表达式 $\frac{1}{2\pi}\int |X(e^{j\omega})|^2 d\omega$。这揭示了DFT作为DTFT[数值近似](@entry_id:161970)的内在一致性。

### 应用与进阶主题

能量与功率的概念是许多高级信号处理应用的基础。

#### [LTI系统](@entry_id:271946)中的物理功率

在[电路分析](@entry_id:261116)中，信号功率的概念直接转化为物理功率。例如，一个电压信号 $v(t)$ 施加于电阻 $R_L$ 上时，消耗的[平均功率](@entry_id:271791)为 $P_L = \frac{1}{R_L} \langle v(t)^2 \rangle$。这里的 $\langle v(t)^2 \rangle$ 正是电压信号的平均功率。

当一个[LTI系统](@entry_id:271946)（如一个电路）的输入由多个不同频率的[正弦信号](@entry_id:196767)叠加而成时，例如 $v_s(t) = v_{s1}(t) + v_{s2}(t)$，其中 $v_{s1}$ 和 $v_{s2}$ 的频率不同，根据[叠加原理](@entry_id:144649)，总的输出电流 $i(t) = i_1(t) + i_2(t)$。传递到负载的总平均功率为：
$$ P_L = R_L \langle i(t)^2 \rangle = R_L \langle (i_1(t) + i_2(t))^2 \rangle = R_L (\langle i_1(t)^2 \rangle + \langle i_2(t)^2 \rangle + 2\langle i_1(t)i_2(t) \rangle) $$
由于不同频率的[正弦信号](@entry_id:196767)在其周期内的乘积积分为零，即它们是正交的，因此互功率项 $\langle i_1(t)i_2(t) \rangle = 0$。这意味着，总的[平均功率](@entry_id:271791)等于各个频率分量单独作用时产生的[平均功率](@entry_id:271791)之和：
$$ P_L = P_{L1} + P_{L2} $$
这个重要的结论极大地简化了多频率输入的[LTI系统](@entry_id:271946)的[功率分析](@entry_id:169032)。我们只需对每个频率分量单独进行[相量分析](@entry_id:261427)，计算其贡献的功率，然后将它们相加即可 [@problem_id:2869241]。

#### 均值、[有效值](@entry_id:276804)与峰均功率比 (PAPR)

对于[功率信号](@entry_id:196112)，我们常常关心其直流 (DC) 和交流 (AC) 分量。信号的**均值 (mean)** 或DC分量定义为：
$$ \mu = \langle x(t) \rangle $$
**均值移除 (mean-removed)** 或AC分量是 $\tilde{x}(t) = x(t) - \mu$。信号的总功率可以分解为DC功率和AC功率之和：
$$ P_x = \langle x(t)^2 \rangle = \langle (\mu + \tilde{x}(t))^2 \rangle = \mu^2 + \langle \tilde{x}(t)^2 \rangle = P_{DC} + P_{AC} $$
信号的**[有效值](@entry_id:276804) (Root-Mean-Square, RMS)** 定义为 $x_{rms} = \sqrt{\langle x(t)^2 \rangle} = \sqrt{P_x}$。它的物理意义是，一个等于 $x_{rms}$ 的直流电压/电流，在同一电阻上会产生与原信号 $x(t)$ 相同的平均功率。

在现代通信系统中，另一个关键指标是**峰均功率比 (Peak-to-Average Power Ratio, PAPR)**。它定义为信号[瞬时功率](@entry_id:174754)的最大值与平均功率之比：
$$ \text{PAPR} = \frac{\max_t |x(t)|^2}{\langle |x(t)|^2 \rangle} $$
PAPR衡量了信号波形的动态范围。高PAPR的信号对放大器等硬件的线性度要求非常苛刻，因为峰值功率可能会导致削波失真。因此，在[系统设计](@entry_id:755777)中，PAPR的计算和控制至关重要。通过[分析信号](@entry_id:190094)的构成，如一个[周期信号](@entry_id:266688)叠加了[直流偏置](@entry_id:271748)和矩形 pedestal 的情况，我们可以从基本定义出发，一步步计算出其均值、AC分量的平均功率，并最终确定其AC分量的PAPR [@problem_id:2869242]。

#### 采样与重建中的能量关系

在数字信号处理中，[连续时间信号](@entry_id:268088)通[过采样](@entry_id:270705)转换为离散时间序列。一个自然的问题是：采样前后信号的能量关系如何？一般而言，信号的总能量 $\int |x(t)|^2 dt$ 与其样本序列的能量 $\sum |x(nT_s)|^2$ 并不相等。

然而，在理想重建过程中，我们可以建立一种规范化的能量关系。考虑一个[带限信号](@entry_id:189047) $x(t)$ 被采样得到 $x[n] = x(nT_s)$，然后通过一个理想低通（sinc）滤波器进行重建。重建信号为 $y(t) = \sum_n x[n] h(t-nT_s)$。我们可以通过选择合适的滤波器增益，使得重建信号的能量等于样本序列的能量。
通过利用[帕塞瓦尔定理](@entry_id:139215)和[sinc函数](@entry_id:274746)的正交性 $\int \operatorname{sinc}_c(\frac{t-nT_s}{T_s}) \operatorname{sinc}_c(\frac{t-mT_s}{T_s}) dt = T_s \delta_{nm}$，可以推导出重建信号的能量为 [@problem_id:2869247]：
$$ E_y = \int |y(t)|^2 dt = \alpha^2 T_s \sum_n |x[n]|^2 $$
其中 $\alpha$ 是[sinc函数](@entry_id:274746)的幅度。为了实现能量归一化，即 $E_y = \sum_n |x[n]|^2$，我们必须选择 $\alpha^2 T_s = 1$，即 $\alpha = 1/\sqrt{T_s}$。这个结果揭示了在保持能量不变的意义下，连续时间域和离散时间域之间通过[采样周期](@entry_id:265475) $T_s$ 建立的深刻联系。

#### 广义信号的能量

在更高级的[系统分析](@entry_id:263805)中，我们会遇到像狄拉克δ函数 $\delta(t)$ 这样的**广义信号**或[分布](@entry_id:182848)。这些信号本身可能没有良好定义的经典能量（例如，$\delta(t)$ 的能量是无限的）。然而，它们作为[LTI系统](@entry_id:271946)的输入时，其输出却可能是常规的、具有有限能量的信号。

例如，考虑输入信号 $x(t)$ 是因果指数衰减函数 $g(t) = e^{-\alpha t}u(t)$ 的[分布](@entry_id:182848)意义下的导数 [@problem_id:2869244]。利用[微分](@entry_id:158718)的[链式法则](@entry_id:190743)，我们得到 $x(t) = \delta(t) - \alpha e^{-\alpha t}u(t)$。这个信号包含一个冲激分量。
要计算[LTI系统](@entry_id:271946)对此输入的响应能量，直接在时域进行卷积可能很困难。[频域](@entry_id:160070)方法则优雅得多。我们首先求出输入信号的[傅里叶变换](@entry_id:142120) $X(\omega) = \frac{j\omega}{\alpha+j\omega}$。然后，将其与系统的频率响应 $H(\omega)$ 相乘得到输出的[频谱](@entry_id:265125) $Y(\omega) = H(\omega)X(\omega)$。最后，利用[帕塞瓦尔定理](@entry_id:139215)，通过积分 $|Y(\omega)|^2$ 来计算输出信号的总能量：
$$ E_y = \frac{1}{2\pi} \int_{-\infty}^{\infty} |H(\omega)X(\omega)|^2 d\omega $$
这种方法绕开了时域中处理[广义函数](@entry_id:182848)的复杂性，展示了[频域分析](@entry_id:265642)在解决此类问题上的强大威力。