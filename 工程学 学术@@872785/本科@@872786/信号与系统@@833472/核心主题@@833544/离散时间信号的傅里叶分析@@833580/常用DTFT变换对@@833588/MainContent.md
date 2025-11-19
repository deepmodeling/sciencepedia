## 引言
[离散时间傅里叶变换](@entry_id:196741)（DTFT）是将[离散时间信号](@entry_id:272771)从时域转换到[频域](@entry_id:160070)的核心数学工具，对于理解和分析数字[信号与系统](@entry_id:274453)至关重要。然而，仅仅掌握其定义并通过[无穷级数求和](@entry_id:161691)来分析每一个信号，既不高效也不直观。真正的精通来自于建立一个由基本信号及其变换构成的“[频域](@entry_id:160070)词汇表”，并学会如何运用DTFT的各项性质来灵活地解决问题。本文旨在填补从基础定义到熟练应用之间的鸿沟，系统性地梳理最常见的DTFT变换对。

本文将引导您深入探索DTFT的世界，分为三个核心部分。在“原理与机制”一章中，我们将逐一推导并解析永恒信号、[有限长信号](@entry_id:272352)和无限长衰减信号等关键变换对，为您构建坚实的理论基础。随后，在“应用与跨学科联系”一章中，我们将展示这些理论工具如何在[LTI系统分析](@entry_id:266777)、[滤波器设计](@entry_id:266363)、[多速率系统](@entry_id:264982)乃至结构生物学等不同领域中发挥其强大的分析能力。最后，“动手实践”部分将提供一系列精心设计的问题，帮助您巩固所学知识，将理论应用于具体的计算与分析中。通过本次学习，您将不再视DTFT为抽象的公式，而是将其内化为解决实际问题的得力助手。

## 原理与机制

在上一章中，我们介绍了[离散时间傅里叶变换 (DTFT)](@entry_id:204279) 的定义及其基本属性。DTFT 是分析[离散时间信号](@entry_id:272771)与系统的核心工具，它将时域中的信号映射到连续的、周期的[频域](@entry_id:160070)谱。然而，在实际应用中，我们很少直接从定义出发，对每个信号都进行[无穷级数求和](@entry_id:161691)。相反，我们依赖于一个由基本信号及其变换构成的“词汇表”，并结合 DTFT 的性质，来分析更复杂的信号。本章旨在系统地建立这个核心词汇表，即一些最常见的 DTFT 变换对，并阐明其背后的原理与推导机制。

### 永恒信号的变换：[频域](@entry_id:160070)中的冲激

一类基础的信号是那些在所有时间点 $n \in (-\infty, \infty)$ 上都存在的“永恒”信号，例如直流信号和[正弦信号](@entry_id:196767)。它们的 DTFT 具有一种特殊的形式，即在特定频率点上[无限集](@entry_id:137163)中的狄拉克 (Dirac) δ 函数。

#### 直流与交变信号

最简单的永恒信号是直流 (DC) 信号，定义为 $x[n] = A$，其中 $A$ 为常数。它的 DTFT 是：
$$
X(e^{j\omega}) = \sum_{n=-\infty}^{\infty} A e^{-j\omega n} = A \sum_{n=-\infty}^{\infty} e^{-j\omega n}
$$
这个无穷级数的求和在常规函数意义下是发散的，但在[广义函数理论](@entry_id:186499)中，它等于一个周期性的冲激串：
$$
\sum_{n=-\infty}^{\infty} e^{-j\omega n} = 2\pi \sum_{k=-\infty}^{\infty} \delta(\omega - 2\pi k)
$$
这个结果表明，一个在时域中恒定不变的信号，其能量完[全集](@entry_id:264200)中在频率为零（以及 $2\pi$ 的所有整数倍）的点上。在主值区间 $(-\pi, \pi]$ 内，DTFT 简化为 $X(e^{j\omega}) = 2\pi A \delta(\omega)$。

另一个有趣的基础信号是交变信号 $x[n] = (-1)^n$。由于 $(-1) = e^{j\pi}$，我们可以将其写成 $x[n] = e^{j\pi n}$。这实际上是下面将要讨论的[复指数信号](@entry_id:273867)的一个特例，其频率为 $\omega_0 = \pi$。它的能量完全集中在[离散时间信号](@entry_id:272771)的最高频率点上。

结合直流和交变信号，考虑一个更一般的信号 $x[n] = A + B(-1)^n$ [@problem_id:1704009]。利用 DTFT 的线性性质，其变换是各自变换之和：
$$
X(e^{j\omega}) = \mathcal{F}\{A\} + \mathcal{F}\{B(-1)^n\} = 2\pi A \delta(\omega) + 2\pi B \delta(\omega - \pi)
$$
其中，变换结果限定在主值区间 $(-\pi, \pi]$ 内。这个例子清晰地展示了[傅里叶分析](@entry_id:137640)的核心思想：将一个信号分解为不同频率分量的叠加。

#### [复指数](@entry_id:162635)与实[正弦信号](@entry_id:196767)

[复指数信号](@entry_id:273867) $x[n] = e^{j\omega_0 n}$ 是 LTI 系统理论中的一个关键角色，因为它是所有 LTI 系统的[特征函数](@entry_id:186820)。它的 DTFT 可以通过频率位移性质或直接套用上述冲激串公式得到：
$$
X(e^{j\omega}) = \sum_{n=-\infty}^{\infty} e^{j\omega_0 n} e^{-j\omega n} = \sum_{n=-\infty}^{\infty} e^{-j(\omega - \omega_0)n} = 2\pi \sum_{k=-\infty}^{\infty} \delta(\omega - \omega_0 - 2\pi k)
$$
这表明[复指数信号](@entry_id:273867)的[频谱](@entry_id:265125)是一个位于 $\omega = \omega_0$ (以及其 $2\pi$ 的周期性重复) 的单一冲激。

通过欧拉公式，我们可以利用[复指数信号](@entry_id:273867)的 DTFT 推导出实[正弦信号](@entry_id:196767)的变换。例如，对于余弦信号 $x[n] = \cos(\omega_0 n) = \frac{1}{2}(e^{j\omega_0 n} + e^{-j\omega_0 n})$，其 DTFT 为：
$$
X(e^{j\omega}) = \frac{1}{2} \mathcal{F}\{e^{j\omega_0 n}\} + \frac{1}{2} \mathcal{F}\{e^{-j\omega_0 n}\} = \pi \sum_{k=-\infty}^{\infty} [\delta(\omega - \omega_0 - 2\pi k) + \delta(\omega + \omega_0 - 2\pi k)]
$$
在主值区间内，这对应于在 $\omega = \omega_0$ 和 $\omega = -\omega_0$ 处的两个冲激，每个的权重都是 $\pi$。这直观地解释了为什么一个实[正弦波](@entry_id:274998)被认为包含正负两个频率分量。

当一个信号由多个[正弦波](@entry_id:274998)叠加而成时，例如 $x[n] = \cos(\omega_0 n) + \cos(\omega_1 n)$，其[频谱](@entry_id:265125)就是各个分量[频谱](@entry_id:265125)的直接叠加 [@problem_id:1704072]。在主值区间内，其 DTFT 将在 $\pm\omega_0$ 和 $\pm\omega_1$ 四个频率点上出现冲激。

### [有限长信号](@entry_id:272352)的变换

与永恒信号不同，[有限长信号](@entry_id:272352)仅在一段有限的时间内非零。它们的 DTFT 通常是频率 $\omega$ 的[连续函数](@entry_id:137361)。

#### [单位冲激](@entry_id:272155)及其位移

最基本的[有限长信号](@entry_id:272352)是克罗内克 (Kronecker) δ 函数，或[单位冲激](@entry_id:272155)，$x[n] = \delta[n]$。其 DTFT 为：
$$
\mathcal{F}\{\delta[n]\} = \sum_{n=-\infty}^{\infty} \delta[n] e^{-j\omega n} = \delta[0] e^{-j\omega \cdot 0} = 1
$$
一个在时域上极度集中的信号，其[频谱](@entry_id:265125)在所有频率上[均匀分布](@entry_id:194597)。根据 DTFT 的[时移性质](@entry_id:275667)，一个位移的[单位冲激](@entry_id:272155) $\delta[n-n_0]$ 的变换是：
$$
\mathcal{F}\{\delta[n-n_0]\} = e^{-j\omega n_0}
$$
这是一个线性相位的[复指数](@entry_id:162635)。

利用这一性质，我们可以构建更复杂的信号。例如，考虑一个关于[原点对称](@entry_id:172995)的冲激对 $x[n] = A \delta[n - n_0] + A \delta[n + n_0]$ [@problem_id:1704022]。其 DTFT 是：
$$
X(e^{j\omega}) = A e^{-j\omega n_0} + A e^{j\omega n_0} = 2A \cos(\omega n_0)
$$
这个例子揭示了一个重要的对称性：时域中的偶对称实信号 ($x[n] = x[-n]$) 对应一个[频域](@entry_id:160070)中的纯实偶函数。

#### 矩形脉冲与 Dirichlet 核

将冲激对的思想扩展，我们可以构建一个[矩形脉冲信号](@entry_id:276926)，它在 $|n| \le M$ 的区间内为 1，其他位置为 0。这种信号常作为 FIR 滤波器的脉冲响应，例如一个简单的[移动平均滤波器](@entry_id:271058) [@problem_id:1704027]。其 DTFT 是：
$$
X(e^{j\omega}) = \sum_{n=-M}^{M} 1 \cdot e^{-j\omega n}
$$
这是一个[等比数列](@entry_id:276380)求和。利用求和公式，可以得到其[闭合形式](@entry_id:271343)：
$$
X(e^{j\omega}) = \frac{\sin\left((M+\frac{1}{2})\omega\right)}{\sin\left(\frac{\omega}{2}\right)}
$$
这个函数被称为 **Dirichlet 核**。它的形状在 $\omega = 0$ 处达到峰值 $2M+1$，并随着 $|\omega|$ 增大而[振荡](@entry_id:267781)衰减。Dirichlet 核是信号处理中最核心的函数之一，它描述了[理想低通滤波器](@entry_id:266159)的截断效应。

#### [三角脉冲](@entry_id:275838)与卷[积性质](@entry_id:151217)

DTFT 的卷[积性质](@entry_id:151217)指出，时域的卷积对应于[频域](@entry_id:160070)的乘积，即 $\mathcal{F}\{x[n] * y[n]\} = X(e^{j\omega})Y(e^{j\omega})$。这个性质极为有用。考虑一个[三角脉冲](@entry_id:275838)信号，它可以由一个[矩形脉冲](@entry_id:273749)与其自身卷积得到 [@problem_id:1704030]。即若 $x[n]$ 是上述定义的[矩形脉冲](@entry_id:273749)，则[三角脉冲](@entry_id:275838) $y[n] = x[n] * x[n]$。

我们无需在时域中执行复杂的卷积运算来求 $y[n]$ 的表达式，再对其进行 DTFT。利用卷[积性质](@entry_id:151217)，我们可以直接在[频域](@entry_id:160070)中得到结果：
$$
Y(e^{j\omega}) = X(e^{j\omega}) \cdot X(e^{j\omega}) = \left[ X(e^{j\omega}) \right]^2 = \left[ \frac{\sin\left((M+\frac{1}{2})\omega\right)}{\sin\left(\frac{\omega}{2}\right)} \right]^2
$$
这个结果显示，一个更平滑的[三角脉冲](@entry_id:275838)（相比于[矩形脉冲](@entry_id:273749)）对应一个衰减更快、旁瓣更低的[频谱](@entry_id:265125)。

### 无限长衰减信号的变换

另一类重要的信号是无限长但绝对可和的信号，这意味着当 $|n| \to \infty$ 时，信号幅值趋于零。

#### 单边指数序列

最典型的例子是因果（或单边）指数序列 $x[n] = a^n u[n]$，其中 $u[n]$ 是[单位阶跃函数](@entry_id:268807)，$|a|  1$ 以保证序列绝对可和（即系统稳定）。这个序列是基本的一阶 IIR 滤波器的脉冲响应 [@problem_id:1704050]。其 DTFT 可以通过[几何级数](@entry_id:158490)求和公式得到：
$$
X(e^{j\omega}) = \sum_{n=0}^{\infty} a^n e^{-j\omega n} = \sum_{n=0}^{\infty} (a e^{-j\omega})^n = \frac{1}{1 - a e^{-j\omega}}
$$
这个变换对是信号处理的基石之一。它的幅度和相位随频率变化，构成了最基本的一阶滤波器响应。

#### 双边指数序列

与单边序列相对应的是双边指数序列 $x[n] = a^{|n|}$，其中 $0  a  1$ [@problem_id:1704046]。这是一个关于原点偶对称的信号。为了求其 DTFT，我们可以将求和区间拆分为负半轴、原点和正半轴：
$$
X(e^{j\omega}) = \sum_{n=-\infty}^{-1} a^{-n} e^{-j\omega n} + a^0 + \sum_{n=1}^{\infty} a^n e^{-j\omega n}
$$
通过变量替换 $m = -n$，第一个和式可以转化为一个标准的几何级数。合并结果后，经过代数化简，可得：
$$
X(e^{j\omega}) = \frac{1 - a^2}{1 - 2a\cos(\omega) + a^2}
$$
不出所料，由于时域信号是实偶对称的，其 DTFT 是一个纯实函数。

#### 偶部分解的应用

我们可以通过信号的偶部和奇部来联系上述两个变换对。一个信号 $x[n]$ 的偶部定义为 $x_e[n] = \frac{1}{2}(x[n] + x[-n])$。对于因果指数序列 $x[n] = a^n u[n]$，其 DTFT 是 $X(e^{j\omega}) = \frac{1}{1 - a e^{-j\omega}}$。根据 DTFT 的性质，其偶部的 DTFT 是 $X_e(e^{j\omega}) = \text{Re}\{X(e^{j\omega})\}$。

我们也可以直接计算 $x_e[n]$ 的表达式并求其 DTFT [@problem_id:1704004]。计算表明，$x_e[n]$ 与双边指数序列 $a^{|n|}$ 非常相似。通过求和计算，可以得到：
$$
X_e(e^{j\omega}) = \frac{1 - a\cos(\omega)}{1 - 2a\cos(\omega) + a^2}
$$
这恰好就是 $\frac{1}{1 - a e^{-j\omega}}$ 的实部。这个练习巧妙地将单边序列、[双边序列](@entry_id:262580)以及 DTFT 的对称性质联系在一起。

### 进阶主题与变换性质的应用

掌握了基本变换对后，我们可以利用 DTFT 的性质来推导更复杂的信号的变换。

#### 频率[微分性质](@entry_id:275298)

DTFT 有一个重要的性质，即时域乘以 $n$ 对应于[频域](@entry_id:160070)的[微分](@entry_id:158718)：
$$
\mathcal{F}\{n x[n]\} = j \frac{d}{d\omega} X(e^{j\omega})
$$
这个性质对于求解形如 $n a^n u[n]$ 的信号的 DTFT 非常有用。我们已知 $\mathcal{F}\{a^n u[n]\} = \frac{1}{1 - a e^{-j\omega}}$。对其应用频率[微分性质](@entry_id:275298)，我们得到：
$$
\mathcal{F}\{n a^n u[n]\} = j \frac{d}{d\omega} \left(\frac{1}{1 - a e^{-j\omega}}\right) = j \frac{-1}{(1 - a e^{-j\omega})^2} (-a e^{-j\omega})(-j) = \frac{a e^{-j\omega}}{(1 - a e^{-j\omega})^2}
$$
这个方法比直接在时域求和要简洁得多。在一些问题中，可能需要计算此变换在特定频率点的值，例如 $\omega = \pi$ [@problem_id:1704067]。在 $\omega = \pi$ 时，$e^{-j\pi} = -1$，代入上式即可得到特定值 $\frac{-a}{(1+a)^2}$。

#### 广义[傅里叶变换](@entry_id:142120)

有些有用的信号，如[单位阶跃函数](@entry_id:268807) $u[n]$ 和[符号函数](@entry_id:167507) $\text{sgn}[n]$，它们不是绝对可和的，因此它们的 DTFT 在常规意义下不收敛。然而，我们可以在广義函数的框架下为其定义 DTFT。

[单位阶跃函数](@entry_id:268807) $u[n]$ 的 DTFT 由两部分组成：一部分来自于其非零的[直流分量](@entry_id:272384)（平均值为 1/2），另一部分来自于其在 $n=0$ 处的跳变。其广义 DTFT 为：
$$
\mathcal{F}\{u[n]\} = \frac{1}{1 - e^{-j\omega}} + \pi \sum_{k=-\infty}^{\infty} \delta(\omega - 2\pi k)
$$
第一项是[几何级数](@entry_id:158490)求和的形式，而第二项代表了直流分量。

有了单位阶跃的变换，我们可以推导其他非绝对可和信号的变换。例如，离散时间[符号函数](@entry_id:167507) $\text{sgn}[n]$ 定义为 $n>0$ 时为 1，$n0$ 时为 -1，$n=0$ 时为 0。它可以表示为两个单位阶跃的组合：$\text{sgn}[n] = u[n] - u[-n]$ [@problem_id:1704035]。

利用 DTFT 的线性性质和时间反转性质 ($\mathcal{F}\{x[-n]\} = X(e^{-j\omega})$)，我们有：
$$
\mathcal{F}\{\text{sgn}[n]\} = \mathcal{F}\{u[n]\} - \mathcal{F}\{u[-n]\} = U(e^{j\omega}) - U(e^{-j\omega})
$$
代入 $U(e^{j\omega})$ 的表达式后，可以发现两者的冲激串部分相互抵消。剩下的部分经过化简可以得到：
$$
\mathcal{F}\{\text{sgn}[n]\} = \frac{1}{1 - e^{-j\omega}} - \frac{1}{1 - e^{j\omega}} = \frac{-2j \sin(\omega)}{2 - 2\cos(\omega)} = -j \cot\left(\frac{\omega}{2}\right)
$$
这个结果表明，[符号函数](@entry_id:167507)作为一个纯[奇函数](@entry_id:173259)，其 DTFT 是一个纯虚函数。

通过本章的学习，我们建立了一个关键的 DTFT 变换对库。这些基本信号——冲激、[正弦波](@entry_id:274998)、[矩形脉冲](@entry_id:273749)、指数序列——构成了我们分析和设计[离散时间系统](@entry_id:263935)时[频域](@entry_id:160070)语言的词汇。掌握它们及其推导过程，是深入理解[数字信号处理](@entry_id:263660)的必经之路。