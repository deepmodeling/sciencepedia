## 引言
在信号与系统的广阔世界中，[连续时间傅里叶变换](@entry_id:268629)（CTFT）是将信号从时域视角转换到[频域](@entry_id:160070)视角的关键桥梁。而在其众多性质中，**线性性质**无疑是最基本、也最具威力的一个。它不仅是一个简单的数学法则，更是一种强大的分析思维，允许我们将看似棘手的复杂信号分解为一系列简单分量的叠加，从而“[分而治之](@entry_id:273215)”。然而，许多学习者常常停留在对公式的机械记忆，未能深刻理解线性性质如何成为连接理论与实际应用的枢纽。本文旨在填补这一认知鸿沟，系统性地揭示线性性质的内在机理与广泛效用。

本文将引导读者踏上一段从原理到实践的探索之旅。在“**原理与机制**”一章中，我们将从基本定义出发，通过数学推导揭示线性性质的本质，并展示如何利用它来分解基本信号（如[正弦波](@entry_id:274998)和[矩形脉冲](@entry_id:273749)），以及如何与其他变换性质结合使用以解决更复杂的问题。随后的“**应用与跨学科联系**”一章将视野拓宽至实际工程领域，探讨线性性质在[通信系统](@entry_id:265921)、[LTI系统分析](@entry_id:266777)、[生物医学信号处理](@entry_id:191505)乃至物理学中的具体应用，彰显其作为通用分析工具的价值。最后，在“**动手实践**”部分，读者将有机会通过解决具体问题，将所学理论知识转化为实际操作技能，从而真正内化线性性质的强大功能。通过这三章的学习，您将能够熟练地运用线性性质来洞察信号的[频域](@entry_id:160070)奥秘。

## 原理与机制

在深入探讨[连续时间傅里叶变换](@entry_id:268629)（Continuous-Time Fourier Transform, CTFT）的广阔应用之前，我们必须首先掌握其最基本且最核心的性质之一：**线性 (linearity)**。线性性质不仅是一个数学上的形式化规则，更是[信号分析](@entry_id:266450)与[系统设计](@entry_id:755777)中一种强大的思维方式的基石。它允许我们将复杂的问题分解为若干个更简单、更易于处理的子问题，并通过叠加这些子问题的解来获得原始问题的答案。本章将详细阐述线性性质的原理，并通过一系列示例展示其在理论推导和实际应用中的关键作用。

### 线性性质的定义与意义

[连续时间傅里叶变换的线性性质](@entry_id:263111)可以形式化地表述如下：

假设有两个信号 $x_1(t)$ 和 $x_2(t)$，它们的[傅里叶变换](@entry_id:142120)分别为 $X_1(\omega)$ 和 $X_2(\omega)$。即：
$$
x_1(t) \quad \overset{\mathcal{F}}{\longleftrightarrow} \quad X_1(\omega)
$$
$$
x_2(t) \quad \overset{\mathcal{F}}{\longleftrightarrow} \quad X_2(\omega)
$$

对于任意常数 $a$ 和 $b$（可以是实数或复数），由这两个信号线性组合而成的新信号 $y(t) = a x_1(t) + b x_2(t)$，其[傅里叶变换](@entry_id:142120) $Y(\omega)$ 等于各个信号[傅里叶变换](@entry_id:142120)的相[同线性组](@entry_id:184902)合：
$$
y(t) = a x_1(t) + b x_2(t) \quad \overset{\mathcal{F}}{\longleftrightarrow} \quad Y(\omega) = a X_1(\omega) + b X_2(\omega)
$$

这一性质源于[傅里叶变换](@entry_id:142120)积分定义的线性。回顾CTFT的定义式：
$$
X(\omega) = \int_{-\infty}^{\infty} x(t) e^{-j\omega t} dt
$$
由于[积分算子](@entry_id:262332)本身是线性的，因此对于信号的线性组合 $a x_1(t) + b x_2(t)$，其变换为：
$$
\mathcal{F}\{a x_1(t) + b x_2(t)\} = \int_{-\infty}^{\infty} [a x_1(t) + b x_2(t)] e^{-j\omega t} dt
$$
$$
= a \int_{-\infty}^{\infty} x_1(t) e^{-j\omega t} dt + b \int_{-\infty}^{\infty} x_2(t) e^{-j\omega t} dt = a X_1(\omega) + b X_2(\omega)
$$
这个简单的数学推导揭示了一个深刻的原理：**时域中的[信号叠加](@entry_id:276221)等价于[频域](@entry_id:160070)中[频谱](@entry_id:265125)的叠加**。这就是著名的**[叠加原理](@entry_id:144649) (superposition principle)** 在[频域分析](@entry_id:265642)中的体现。这一原理是[线性时不变](@entry_id:276287)（LTI）[系统分析](@entry_id:263805)的核心，它意味着我们可以将复杂的输入[信号分解](@entry_id:145846)为一系列基本分量的和，分别研究系统对每个分量的响应，最后将这些响应叠加起来得到总的输出。

### 线性性质的基本应用

线性性质最直接的应用在于，它使我们能够利用已知的基本变换对，通过组合来求得更复杂信号的[傅里叶变换](@entry_id:142120)。

#### 叠加与[直流分量](@entry_id:272384)

一个简单而直观的应用场景是分析由多个信号源相加而成的混合信号。考虑一个模拟加法器电路，其输出是两个输入信号 $x_1(t)$ 和 $x_2(t)$ 的加权和：$y(t) = C_1 x_1(t) + C_2 x_2(t)$。根据线性性质，输出信号的[频谱](@entry_id:265125) $Y(\omega)$ 必然是输入[信号频谱](@entry_id:198418)的相同加权和：$Y(\omega) = C_1 X_1(\omega) + C_2 X_2(\omega)$。

这一关系在任何频率点 $\omega$ 都成立。一个特别重要的频率点是 $\omega = 0$，它对应于信号的**[直流分量](@entry_id:272384) (DC component)**。信号 $x(t)$ 的直流分量是其[频谱](@entry_id:265125)在零频率处的值 $X(0)$，它等于信号在整个时间轴上的积分，代表了信号的平均值或净面积。
$$
X(0) = \int_{-\infty}^{\infty} x(t) e^{-j \cdot 0 \cdot t} dt = \int_{-\infty}^{\infty} x(t) dt
$$
因此，对于上述加法器，其输出信号的[直流分量](@entry_id:272384) $Y(0)$ 可以直接通过输入信号的[直流分量](@entry_id:272384)计算得出：$Y(0) = C_1 X_1(0) + C_2 X_2(0)$。例如，如果已知两个输入信号的[直流分量](@entry_id:272384)分别为 $X_1(0) = 6.0 \, \text{V·s}$ 和 $X_2(0) = -2.5 \, \text{V·s}$，且电路的增益常数为 $C_1 = 3.0$ 和 $C_2 = -4.0$，那么输出信号的直流分量可以直接计算为 $Y(0) = 3.0 \times 6.0 + (-4.0) \times (-2.5) = 18.0 + 10.0 = 28.0 \, \text{V·s}$ [@problem_id:1734226]。这个例子清晰地展示了线性性质如何将时域中的信号混合操作，转化为[频域](@entry_id:160070)中简单的代数运算。

#### 常用信号的分解

线性性质最强大的功能之一是允许我们通过分解来推导新信号的[傅里叶变换](@entry_id:142120)。许多常见的信号，如正弦、余弦函数，可以表示为更基本的[复指数信号](@entry_id:273867)的线性组合。

一个最基本的[傅里叶变换](@entry_id:142120)对是[复指数信号](@entry_id:273867)：
$$
e^{j\omega_0 t} \quad \overset{\mathcal{F}}{\longleftrightarrow} \quad 2\pi \delta(\omega - \omega_0)
$$
其中 $\delta(\cdot)$ 是狄拉克δ函数。这个变换对表明，一个纯粹的复[振荡](@entry_id:267781)信号在[频域](@entry_id:160070)中只存在于其自身的频率点 $\omega_0$ 上。

利用欧拉公式，我们可以将余弦和正弦函数表示为[复指数](@entry_id:162635)的[线性组合](@entry_id:154743)：
$$
\cos(\omega_0 t) = \frac{1}{2} e^{j\omega_0 t} + \frac{1}{2} e^{-j\omega_0 t}
$$
$$
\sin(\omega_0 t) = \frac{1}{2j} e^{j\omega_0 t} - \frac{1}{2j} e^{-j\omega_0 t}
$$
现在，我们可以借助线性性质来求它们的[傅里叶变换](@entry_id:142120)。对于余弦函数：
$$
\mathcal{F}\{\cos(\omega_0 t)\} = \mathcal{F}\left\{\frac{1}{2} e^{j\omega_0 t} + \frac{1}{2} e^{-j\omega_0 t}\right\} = \frac{1}{2} \mathcal{F}\{e^{j\omega_0 t}\} + \frac{1}{2} \mathcal{F}\{e^{-j\omega_0 t}\}
$$
$$
= \frac{1}{2} [2\pi \delta(\omega - \omega_0)] + \frac{1}{2} [2\pi \delta(\omega - (-\omega_0))] = \pi[\delta(\omega - \omega_0) + \delta(\omega + \omega_0)]
$$
类似地，对于正弦函数：
$$
\mathcal{F}\{\sin(\omega_0 t)\} = \frac{1}{2j} \mathcal{F}\{e^{j\omega_0 t}\} - \frac{1}{2j} \mathcal{F}\{e^{-j\omega_0 t}\} = \frac{\pi}{j}[\delta(\omega - \omega_0) - \delta(\omega + \omega_0)]
$$
这两个结果揭示了实[正弦信号](@entry_id:196767)的[频谱](@entry_id:265125)特性：它们总是由一对位于正负频率轴上、对称的脉冲（δ函数）构成。

通过这个基础，我们可以处理任何由直流和正弦分量组成的信号。例如，一个叠加了直流偏置的正弦电压信号 $y(t) = V_0 + V_1 \cos(\omega_0 t)$，其[频谱](@entry_id:265125)可以直接通过线性性质写出：
$$
Y(\omega) = \mathcal{F}\{V_0\} + \mathcal{F}\{V_1 \cos(\omega_0 t)\} = V_0 \mathcal{F}\{1\} + V_1 \mathcal{F}\{\cos(\omega_0 t)\}
$$
$$
= V_0 [2\pi \delta(\omega)] + V_1 [\pi(\delta(\omega - \omega_0) + \delta(\omega + \omega_0))]
$$
$$
= 2\pi V_0 \delta(\omega) + \pi V_1[\delta(\omega - \omega_0) + \delta(\omega + \omega_0)]
$$
这个[频谱](@entry_id:265125)由三个脉冲组成：一个位于 $\omega=0$ 的[直流分量](@entry_id:272384)，以及一对位于 $\pm \omega_0$ 的交流分量 [@problem_id:1734253]。同理，对于更复杂的信号，如 $x(t) = C_1 \cos(\omega_1 t) + C_2 \sin(\omega_2 t)$，我们也可以逐项求变换然后相加，得到其[频谱](@entry_id:265125) [@problem_id:1734262]。

### [信号合成](@entry_id:272649)与分解中的线性关系

线性性质不仅适用于从时域到[频域](@entry_id:160070)的正变换，也同样适用于从[频域](@entry_id:160070)到时域的逆变换。这为我们从已知的[频谱](@entry_id:265125)形状反推时域信号提供了有力工具。

#### [频域](@entry_id:160070)合成与傅里叶逆变换

由于傅里叶逆变换本身也是一个[积分变换](@entry_id:186209)，它同样满足线性性质。如果一个[频谱](@entry_id:265125) $Y(\omega)$ 可以表示为两个[频谱](@entry_id:265125) $X_1(\omega)$ 和 $X_2(\omega)$ 的[线性组合](@entry_id:154743) $Y(\omega) = a X_1(\omega) + b X_2(\omega)$，那么对应的时域信号 $y(t)$ 也必然是 $x_1(t)$ 和 $x_2(t)$ 的相[同线性组](@entry_id:184902)合 $y(t) = a x_1(t) + b x_2(t)$。

这个原理在[信号合成](@entry_id:272649)中非常有用。假设一位信号处理工程师测量得到一个[频谱](@entry_id:265125)，并发现它可以表示为两个已知[频谱](@entry_id:265125)的线性组合。例如，[频谱](@entry_id:265125)为 $Y(\omega) = C_1 \text{sinc}(\omega T) + C_2 \text{sinc}(\omega T)e^{-j\omega T_0}$，其中 $\text{sinc}(x) = \sin(x)/x$。我们知道一个宽度为 $2T$ 的[矩形脉冲](@entry_id:273749) $\text{rect}(\frac{t}{2T})$ 的[傅里叶变换](@entry_id:142120)是 $2T \text{sinc}(\omega T)$。因此，我们可以建立基本变换对：
$$
\frac{1}{2T} \text{rect}\left(\frac{t}{2T}\right) \quad \overset{\mathcal{F}}{\longleftrightarrow} \quad \text{sinc}(\omega T)
$$
此外，根据[傅里叶变换的时移](@entry_id:270418)性质，$x(t-t_0) \leftrightarrow X(\omega)e^{-j\omega t_0}$，我们知道[频谱](@entry_id:265125)中的相位项 $e^{-j\omega T_0}$ 对应于时域中的时间延迟 $T_0$。
因此，我们可以将 $Y(\omega)$ 分解为两个部分：
1.  $C_1 \text{sinc}(\omega T)$，它对应于时域信号 $\frac{C_1}{2T} \text{rect}(\frac{t}{2T})$。
2.  $C_2 \text{sinc}(\omega T)e^{-j\omega T_0}$，它对应于时域信号 $\frac{C_2}{2T} \text{rect}(\frac{t-T_0}{2T})$。

根据[逆变](@entry_id:192290)换的线性性质，最终的时域信号 $y(t)$ 就是这两个时域分量的和：
$$
y(t) = \frac{C_1}{2T} \text{rect}\left(\frac{t}{2T}\right) + \frac{C_2}{2T} \text{rect}\left(\frac{t-T_0}{2T}\right)
$$
这个过程完美地展示了如何利用线性性质，从一个复合的[频域](@entry_id:160070)表达式，通过“[分而治之](@entry_id:273215)”的策略，重构出相应的时域波形 [@problem_id:1734229]。

#### 偶部分与奇部分分解

任何信号 $x(t)$ 都可以唯一地分解为其**偶分量 (even component)** $x_e(t)$ 和**奇分量 (odd component)** $x_o(t)$ 的和：
$$
x(t) = x_e(t) + x_o(t)
$$
其中：
$$
x_e(t) = \frac{1}{2}[x(t) + x(-t)]
$$
$$
x_o(t) = \frac{1}{2}[x(t) - x(-t)]
$$
根据线性性质，信号的[傅里叶变换](@entry_id:142120)也必然是其偶分量和奇分量变换的和：
$$
X(\omega) = \mathcal{F}\{x_e(t)\} + \mathcal{F}\{x_o(t)\} = X_e(\omega) + X_o(\omega)
$$
结合[傅里叶变换的对称性](@entry_id:268288)质，我们知道：对于实信号 $x(t)$，其偶分量 $x_e(t)$ 的[傅里叶变换](@entry_id:142120) $X_e(\omega)$ 是一个实值[偶函数](@entry_id:163605)，而其奇分量 $x_o(t)$ 的[傅里叶变换](@entry_id:142120) $X_o(\omega)$ 是一个纯虚值奇函数。因此，$X_e(\omega) = \text{Re}\{X(\omega)\}$ 且 $X_o(\omega) = j \text{Im}\{X(\omega)\}$。

线性性质还允许我们分析这些分量的组合。例如，考虑一个输出信号 $y(t)$ 是由输入信号的偶分量减去奇分量构成的：$y(t) = x_e(t) - x_o(t)$。通过代入定义，我们发现 $y(t) = \frac{1}{2}[x(t) + x(-t)] - \frac{1}{2}[x(t) - x(-t)] = x(-t)$。这说明这个操作等效于时间反转。其[傅里叶变换](@entry_id:142120) $Y(\omega)$ 可以直接利用时间反转性质 $\mathcal{F}\{x(-t)\} = X(-\omega)$ 得到，即 $Y(\omega) = X(-\omega)$ [@problem_id:1734222]。

#### 实部与虚部分解

与偶奇分解类似，一个复值信号 $z(t)$ 可以分解为其实部 $x(t)$ 和虚部 $y(t)$：
$$
z(t) = x(t) + j y(t)
$$
其中 $x(t)$ 和 $y(t)$ 都是实值信号。应用[傅里叶变换的线性](@entry_id:268418)性质，我们可以立即得到其[频谱](@entry_id:265125)：
$$
Z(\omega) = \mathcal{F}\{x(t) + j y(t)\} = \mathcal{F}\{x(t)\} + j \mathcal{F}\{y(t)\} = X(\omega) + j Y(\omega)
$$
这说明复信号的[傅里叶变换](@entry_id:142120)，其实部和虚部分别是原信号实部和虚部的[傅里叶变换](@entry_id:142120)（虚部变换需乘以 $j$）。

例如，给定一个复信号 $z(t) = \text{rect}(t) + j \cdot \text{sgn}(t)$，我们可以利用已知的变换对：
$$
\mathcal{F}\{\text{rect}(t)\} = \frac{\sin(\omega/2)}{\omega/2} \quad \text{and} \quad \mathcal{F}\{\text{sgn}(t)\} = \frac{2}{j\omega}
$$
直接通过线性性质求出 $Z(\omega)$：
$$
Z(\omega) = \mathcal{F}\{\text{rect}(t)\} + j \mathcal{F}\{\text{sgn}(t)\} = \frac{\sin(\omega/2)}{\omega/2} + j \left(\frac{2}{j\omega}\right) = \frac{\sin(\omega/2)}{\omega/2} + \frac{2}{\omega}
$$
这个例子清晰地表明，处理复信号的[频谱](@entry_id:265125)时，我们可以分别考虑其实部和虚部，然后在线性框架下将结果合并 [@problem_id:1734210]。

### 线性性质与其他变换性质的结合

线性性质的真正威力体现在它与其他[傅里叶变换](@entry_id:142120)性质（如[微分](@entry_id:158718)、共轭、[时移](@entry_id:261541)等）结合使用时。线性是连接这些性质的“黏合剂”，使我们能够解决更复杂的问题。

#### 线性与[微分性质](@entry_id:275298)

[傅里叶变换](@entry_id:142120)的一个关键优势是它能将时域中的微积分运算转化为[频域](@entry_id:160070)中的代数运算。[微分性质](@entry_id:275298)指出：
$$
\frac{d}{dt} x(t) \quad \overset{\mathcal{F}}{\longleftrightarrow} \quad j\omega X(\omega)
$$
当一个系统由[线性常系数微分方程](@entry_id:276881)描述时，线性性质和[微分性质](@entry_id:275298)的结合使用就显得尤为重要。考虑一个系统，其输出 $y(t)$ 是输入 $x(t)$ 与其导数的线性组合：
$$
y(t) = A x(t) + B \frac{dx(t)}{dt}
$$
对该方程两边取[傅里叶变换](@entry_id:142120)，并应用线性性质：
$$
Y(\omega) = \mathcal{F}\left\{A x(t) + B \frac{dx(t)}{dt}\right\} = A \mathcal{F}\{x(t)\} + B \mathcal{F}\left\{\frac{dx(t)}{dt}\right\}
$$
再应用[微分性质](@entry_id:275298)，我们得到：
$$
Y(\omega) = A X(\omega) + B [j\omega X(\omega)] = (A + j\omega B) X(\omega)
$$
这个结果表明，时域中的[微分方程](@entry_id:264184)被转换为了[频域](@entry_id:160070)中一个简单的代数关系。$H(\omega) = A + j\omega B$ 就是该系统的频率响应。这一转换是[LTI系统](@entry_id:271946)[频域分析](@entry_id:265642)方法的基础 [@problem_id:1734217]。

#### 线性、共轭与时间反转

[傅里叶变换](@entry_id:142120)的共轭性质指出 $\mathcal{F}\{x^*(t)\} = X^*(-\omega)$，而时间反转性质为 $\mathcal{F}\{x(-t)\} = X(-\omega)$。将两者结合，我们可以推导出一条有用的性质：
$$
\mathcal{F}\{x^*(-t)\} = X^*(\omega)
$$
现在，考虑一个由信号 $x(t)$ 与其共轭时间反转信号 $x^*(-t)$ 相加构成的信号 $z(t) = x(t) + x^*(-t)$。利用线性性质，其[频谱](@entry_id:265125)为：
$$
Z(\omega) = \mathcal{F}\{x(t)\} + \mathcal{F}\{x^*(-t)\} = X(\omega) + X^*(\omega)
$$
我们知道，任何复数与其共轭之和等于该复数的实部的两倍，即 $C + C^* = 2\text{Re}\{C\}$。因此：
$$
Z(\omega) = 2 \text{Re}\{X(\omega)\}
$$
这揭示了一个重要的对称关系：由 $x(t)$ 和 $x^*(-t)$ 构造的信号，其[频谱](@entry_id:265125)是纯实数的。例如，对于信号 $x(t) = A e^{(-\alpha + j\omega_0)t} u(t)$，其[傅里叶变换](@entry_id:142120)为 $X(\omega) = \frac{A}{\alpha + j(\omega-\omega_0)}$。那么信号 $z(t) = x(t) + x^*(-t)$ 的[傅里叶变换](@entry_id:142120)就是 $Z(\omega) = 2 \text{Re}\left\{\frac{A}{\alpha + j(\omega-\omega_0)}\right\} = 2 \frac{A\alpha}{\alpha^2 + (\omega-\omega_0)^2}$ [@problem_id:1734241]。这个结果在不直接计算 $z(t)$ 的时域表达式的情况下，通过结合线性、共轭和时间反转性质就能得到。

#### 线性与极限过程

线性性质的适用性甚至可以扩展到涉及极限过程的场景，只要极限和积分（[傅里叶变换](@entry_id:142120)）的顺序可以交换。这为我们提供了一种从已知变换推导新变换的巧妙方法。

一个经典的例子是推导[符号函数](@entry_id:167507) $\text{sgn}(t)$ 的[傅里叶变换](@entry_id:142120)。[符号函数](@entry_id:167507)可以被看作是一个双边指数衰减函数在衰减率趋于零时的极限：
$$
\text{sgn}(t) = \lim_{a \to 0^+} [e^{-at}u(t) - e^{at}u(-t)]
$$
假设我们可以[交换极限](@entry_id:141487)和[傅里叶变换](@entry_id:142120)的顺序，那么：
$$
\mathcal{F}\{\text{sgn}(t)\} = \lim_{a \to 0^+} \mathcal{F}\{e^{-at}u(t) - e^{at}u(-t)\}
$$
利用线性性质，这可以分解为：
$$
= \lim_{a \to 0^+} [\mathcal{F}\{e^{-at}u(t)\} - \mathcal{F}\{e^{at}u(-t)\}]
$$
我们知道单边指数衰减信号的变换对是 $\mathcal{F}\{e^{-at}u(t)\} = \frac{1}{a+j\omega}$（对于 $a>0$）。利用时间反转性质，$\mathcal{F}\{e^{at}u(-t)\} = \mathcal{F}\{e^{-a(-t)}u(-t)\} = \frac{1}{a-j\omega}$。代入以上表达式：
$$
\mathcal{F}\{\text{sgn}(t)\} = \lim_{a \to 0^+} \left[\frac{1}{a+j\omega} - \frac{1}{a-j\omega}\right] = \lim_{a \to 0^+} \frac{(a-j\omega) - (a+j\omega)}{(a+j\omega)(a-j\omega)}
$$
$$
= \lim_{a \to 0^+} \frac{-2j\omega}{a^2 + \omega^2} = \frac{-2j\omega}{\omega^2} = \frac{-2j}{\omega} = \frac{2}{j\omega}
$$
这个推导过程 [@problem_id:1734212] 不仅得出了[符号函数](@entry_id:167507)的重要变换，更展示了线性性质作为一种分析工具的深刻性和灵活性。

### 高级应用：解析信号与调制

线性性质在通信系统等高级领域中依然是不可或缺的工具，尤其是在处理与**解析信号 (analytic signal)** 和[调制相](@entry_id:141499)关的复杂表达式时。

对于一个实信号 $x(t)$，其[解析信号](@entry_id:190094)定义为 $z(t) = x(t) + j\hat{x}(t)$，其中 $\hat{x}(t)$ 是 $x(t)$ 的希尔伯特变换。解析信号的[傅里叶变换](@entry_id:142120) $Z(\omega)$ 有一个简洁的性质：它等于原始[信号频谱](@entry_id:198418) $X(\omega)$ 的正频率部分的两倍，即 $Z(\omega) = 2U(\omega)X(\omega)$，其中 $U(\omega)$ 是[频域](@entry_id:160070)[单位阶跃函数](@entry_id:268807)。

现在，考虑一个复杂的信号处理变换，它涉及到解析信号、调制以及实部和虚部操作 [@problem_id:1734260]：
$$
y(t) = A \cdot \text{Re}\{z(t)e^{j\omega_c t}\} + B \cdot \text{Im}\{z(t)e^{j\omega_c t}\}
$$
这个表达式看起来非常复杂，但我们可以利用线性性质将其拆解。首先，将实部和虚部用复[共轭表示](@entry_id:139136)：
$$
\text{Re}\{s\} = \frac{1}{2}(s + s^*) \quad , \quad \text{Im}\{s\} = \frac{1}{2j}(s - s^*)
$$
令 $s(t) = z(t)e^{j\omega_c t}$，代入 $y(t)$ 的表达式中并整理，我们得到：
$$
y(t) = A \frac{s(t) + s^*(t)}{2} + B \frac{s(t) - s^*(t)}{2j} = \frac{A-jB}{2} s(t) + \frac{A+jB}{2} s^*(t)
$$
这个时域表达式现在是一个清晰的[线性组合](@entry_id:154743)。根据[傅里叶变换的线性](@entry_id:268418)性质，我们有：
$$
Y(\omega) = \frac{A-jB}{2} \mathcal{F}\{s(t)\} + \frac{A+jB}{2} \mathcal{F}\{s^*(t)\}
$$
接下来，我们只需要求出 $S(\omega)=\mathcal{F}\{s(t)\}$ 和 $\mathcal{F}\{s^*(t)\}$。根据调制性质，$S(\omega)$ 是 $Z(\omega)$ [频谱](@entry_id:265125)的右移：$S(\omega) = Z(\omega - \omega_c) = 2U(\omega - \omega_c)X(\omega - \omega_c)$。
而对于 $s^*(t) = z^*(t)e^{-j\omega_c t}$，其变换 $\mathcal{F}\{s^*(t)\}$ 可以通过共轭和调制性质得到，它等于 $S^*(-\omega)$。最终，经过一系列推导，可以得到 $Y(\omega)$ 的完整表达式。

这个例子是线性性质威力的终极体现。一个看似难以处理的[非线性](@entry_id:637147)操作（取实部、虚部），通过复数表示法被转化为[线性组合](@entry_id:154743)，从而使得[傅里叶变换](@entry_id:142120)可以被直接应用。这再次证明，线性性质是[傅里叶分析](@entry_id:137640)中进行“分而治之”策略的根本保证。无论信号处理的操作多么复杂，只要我们能将其最终表示为基本信号的线性组合，就能利用线性性质在[频域](@entry_id:160070)中找到清晰的对应关系。