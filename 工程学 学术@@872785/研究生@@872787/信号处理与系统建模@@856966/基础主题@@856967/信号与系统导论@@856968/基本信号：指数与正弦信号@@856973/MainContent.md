## 引言
指数信号与[正弦信号](@entry_id:196767)是现代工程与物理科学的通用语言，构成了信号处理与[系统建模](@entry_id:197208)的基石。无论是[通信系统](@entry_id:265921)中的信息传输、控制系统中的动态响应，还是物理世界中的[振荡](@entry_id:267781)与波，其核心都离不开对这些基本波形的深刻理解。然而，许多学习者虽然熟悉这些信号的形式，却常常在将它们的数学表示（如[相量](@entry_id:270266)和复指数）与它们在复杂系统中的实际行为联系起来时遇到困难。本文旨在填补这一知识鸿沟，提供一个从基础原理到前沿应用的系统性视角。

在接下来的内容中，我们将分三步深入探索这一主题。首先，在“原理与机制”一章中，我们将剖析指数与[正弦信号](@entry_id:196767)的数学本质，介绍[相量](@entry_id:270266)、[拉普拉斯变换](@entry_id:159339)等核心分析工具，并阐明它们如何作为线性时不变（LTI）系统的“特征函数”来决定系统响应。随后，在“应用与跨学科联系”一章中，我们将展示这些理论在通信、数字信号处理、自动控制及物理学等多个领域的强大应用力。最后，“动手实践”部分将通过具体问题，帮助您巩固所学知识。让我们从构成这一切基础的原理与机制开始。

## 原理与机制

本章旨在深入探讨构成现代信号处理与[系统建模](@entry_id:197208)基石的基本信号类型：指数信号与[正弦信号](@entry_id:196767)。我们将从它们的数学表示法出发，逐步解析其核心属性，并最终阐明它们在线性时不变（LTI）[系统分析](@entry_id:263805)中的关键作用。本章内容将为你提供一个坚实的理论基础，以便理解更复杂的信号与系统行为。

### [信号表示](@entry_id:266189)与基本属性

在[信号分析](@entry_id:266450)领域，最核心的构件并非我们直观感受到的[正弦波](@entry_id:274998)，而是更为抽象的[复指数信号](@entry_id:273867)。理解了[复指数信号](@entry_id:273867)，其他基本信号的特性便可迎刃而解。

#### 复指数作为原型信号

[连续时间复指数信号](@entry_id:261014)通常表示为 $x(t) = C e^{st}$，其中 $C$ 和 $s$ 均为复数。[复频率](@entry_id:266400) $s$ 可以分解为实部和虚部，$s = \sigma + j\omega$，这使得信号的形式变为 $x(t) = C e^{(\sigma + j\omega)t} = C e^{\sigma t} e^{j\omega t}$。此形式揭示了其根本行为：$e^{\sigma t}$ 项决定了信号的幅度是随时间呈指数增长（$\sigma > 0$）、衰减（$\sigma  0$）还是保持不变（$\sigma = 0$）；而 $e^{j\omega t}$ 项（根据[欧拉公式](@entry_id:176440) $e^{j\theta} = \cos(\theta) + j\sin(\theta)$）则描述了一个恒幅度的[振荡](@entry_id:267781)行为，其[角频率](@entry_id:261565)为 $\omega$。

类似地，[离散时间复指数](@entry_id:264089)信号的形式为 $x[n] = z^n$，其中 $z$ 是一个复数。若将 $z$ 以极坐标形式表示为 $z = r e^{j\Omega}$，其中 $r = |z|$，则信号为 $x[n] = (r e^{j\Omega})^n = r^n e^{j\Omega n}$。同样，$r^n$ 项控制幅度的增长（$r>1$）或衰减（$r1$），而 $e^{j\Omega n}$ 项代表离散时间的[振荡](@entry_id:267781)。

#### 有界性、能量与功率

一个信号的**有界性**（boundedness）是其基本属性之一，它指的是信号的幅度在任何时刻都不会超过某个有限的常数 $M$。对于[离散时间复指数](@entry_id:264089)信号 $x[n] = z^n$，其有界性完全取决于 $|z|$ 的值和时间轴的范围 [@problem_id:2868255]。
- 对于一个定义在 $n \in \mathbb{Z}_{\ge 0}$（即 $n=0, 1, 2, \dots$）上的**单边序列**，其有界的充要条件是 $|z| \le 1$。如果 $|z|>1$，序列将随 $n \to \infty$ 而无界增长。
- 对于一个定义在 $n \in \mathbb{Z}$（所有整数）上的**[双边序列](@entry_id:262580)**，其有界的充要条件是 $|z| = 1$。因为如果 $|z| > 1$，序列在 $n \to +\infty$ 时无界；而如果 $|z|  1$，序列在 $n \to -\infty$ 时（例如 $n=-k, k \to \infty$）的幅度 $|z|^{-k} = (1/|z|)^k$ 将会无界。

除了有界性，我们还根据信号的**总能量**（total energy）和**[平均功率](@entry_id:271791)**（average power）对其进行分类。一个信号 $x(t)$ 的总能量定义为：
$$ E_x = \int_{-\infty}^{\infty} |x(t)|^2 \, dt $$
其平均功率定义为：
$$ P_x = \lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} |x(t)|^2 \, dt $$

- **[能量信号](@entry_id:190524)**（Energy Signals）：总能量 $E_x$ 是一个有限的正数（$0  E_x  \infty$）。对于[能量信号](@entry_id:190524)，其平均功率必为零。
- **[功率信号](@entry_id:196112)**（Power Signals）：[平均功率](@entry_id:271791) $P_x$ 是一个有限的正数（$0  P_x  \infty$）。对于[功率信号](@entry_id:196112)，其总能量必为无穷大。

一个典型的例子可以帮助我们理解这两种分类 [@problem_id:2868248]。考虑一个衰减指数信号 $x_1(t) = B e^{-\alpha t} u(t)$（其中 $\alpha>0$，$u(t)$ 为[单位阶跃函数](@entry_id:268807)）和一个[正弦信号](@entry_id:196767) $x_2(t) = A \cos(\omega_0 t + \phi)$。

对于衰减指数信号 $x_1(t)$，其总能量为：
$$ E_{x_1} = \int_{0}^{\infty} |B e^{-\alpha t}|^2 dt = B^2 \int_{0}^{\infty} e^{-2\alpha t} dt = \frac{B^2}{2\alpha} $$
由于其能量有限，这是一个[能量信号](@entry_id:190524)。

对于[正弦信号](@entry_id:196767) $x_2(t)$，它永不衰减，因此其总能量是无穷的。但我们可以计算其[平均功率](@entry_id:271791)。利用恒等式 $\cos^2(\theta) = \frac{1}{2}(1 + \cos(2\theta))$：
$$ P_{x_2} = \lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} A^2 \cos^2(\omega_0 t + \phi) dt = \lim_{T \to \infty} \frac{A^2}{2T} \int_{-T}^{T} \frac{1}{2}(1 + \cos(2(\omega_0 t + \phi))) dt $$
在一个很长的时间区间内，$\cos$ 项的积分相对于区间的长度可以忽略不计，因此积分结果近似为 $\frac{A^2}{2} \cdot \frac{2T}{2T} = \frac{A^2}{2}$。所以，[正弦信号](@entry_id:196767)是一个[功率信号](@entry_id:196112)，其平均功率为 $\frac{A^2}{2}$。

### [正弦信号](@entry_id:196767)与[相量表示](@entry_id:196506)

尽管[复指数信号](@entry_id:273867)在数学上更为根本，但工程和物理世界中我们直接观测到的大多是实值信号，如[正弦波](@entry_id:274998)。幸运的是，两者之间有深刻而实用的联系。

#### 从复指数到实正弦

一个实[正弦信号](@entry_id:196767) $x(t) = A\cos(\omega t + \phi)$ 可以通过欧拉公式表示为两个复指数的和。这个表示法揭示了“[负频率](@entry_id:264021)”这一重要概念的起源 [@problem_id:2868270]。
$$ x(t) = A\cos(\omega t + \phi) = A \frac{e^{j(\omega t + \phi)} + e^{-j(\omega t + \phi)}}{2} $$
展开后得到：
$$ x(t) = \left( \frac{A}{2} e^{j\phi} \right) e^{j\omega t} + \left( \frac{A}{2} e^{-j\phi} \right) e^{-j\omega t} $$
这个形式 $x(t) = a_+ e^{j\omega t} + a_- e^{-j\omega t}$ 被称为**双边[复指数](@entry_id:162635)表示**。其中，复系数 $a_+ = \frac{A}{2} e^{j\phi}$ 对应于正频率分量 $\omega$，而 $a_- = \frac{A}{2} e^{-j\phi}$ 对应于[负频率](@entry_id:264021)分量 $-\omega$。请注意，这两个系数互为[复共轭](@entry_id:174690)，即 $a_- = a_+^*$。这个**[共轭对称性](@entry_id:144131)**是信号 $x(t)$ 为实值的根本保证。负频率分量并非一个独立的物理实体，而是为了在数学上构造一个纯实数信号而必须存在的共轭搭档。

#### [相量](@entry_id:270266)抽象

在处理具有相同频率 $\omega$ 的[正弦信号](@entry_id:196767)时，反复书写 $\cos(\omega t + \phi)$ 会非常繁琐。**[相量](@entry_id:270266)**（Phasor）提供了一种极为便利的抽象。对于一个[正弦信号](@entry_id:196767) $x(t) = A\cos(\omega t + \phi)$，其[相量](@entry_id:270266) $X$ 被定义为满足下式的唯一复数 [@problem_id:2868211]：
$$ x(t) = \Re\{X e^{j\omega t}\} $$
其中 $\Re\{\cdot\}$ 表示取实部。通过将 $x(t)$ 的[欧拉公式](@entry_id:176440)表示与该定义进行比较，我们可以直接建立物理参数（幅度 $A$ 和相位 $\phi$）与复数[相量](@entry_id:270266) $X$ 之间的双射关系：
$$ X = A e^{j\phi} = A\cos(\phi) + jA\sin(\phi) $$
相量 $X$ 是一个复数，它以其模 $|X|=A$ 和幅角 $\arg(X)=\phi$ 封装了[正弦信号](@entry_id:196767)的全部信息（除了频率 $\omega$，频率在使用[相量法](@entry_id:165812)时被假定为已知且恒定）。

[相量](@entry_id:270266)的威力在于它将时域中的[微分](@entry_id:158718)和积分运算转化为[频域](@entry_id:160070)中的代数运算。更直接地，它将难以处理的三角函数运算转变为简单的[复数运算](@entry_id:195031)。例如，我们可以通过在特定时刻对信号进行采样来确定其相量。假设一个信号 $x(t)$，其相量为 $X=a+jb$。我们可以推导出 $x(t) = \Re\{(a+jb)(\cos(\omega t) + j\sin(\omega t))\} = a\cos(\omega t) - b\sin(\omega t)$。如果我们在 $t_1=0$ 和 $t_2=\frac{\pi}{2\omega}$ 时刻进行测量，得到 $x(0)=3$ 和 $x(\frac{\pi}{2\omega})=-4$，则：
$$ x(0) = a\cos(0) - b\sin(0) = a = 3 $$
$$ x(\frac{\pi}{2\omega}) = a\cos(\frac{\pi}{2}) - b\sin(\frac{\pi}{2}) = -b = -4 \implies b = 4 $$
因此，该信号的相量为 $X = 3+j4$ [@problem_id:2868211]。

#### [相量](@entry_id:270266)算术与叠加

相量最强大的应用之一是简化[正弦信号](@entry_id:196767)的叠加问题。根据叠加原理，两个同频[正弦信号](@entry_id:196767)之和仍然是同一频率的[正弦信号](@entry_id:196767)。其合成后的幅度和相位可以通过对各自的[相量](@entry_id:270266)进行矢量（复数）加法来轻松求得 [@problem_id:2868238]。

考虑两个信号 $x_1(t) = A_1 \cos(\omega t + \phi_1)$ 和 $x_2(t) = A_2 \cos(\omega t + \phi_2)$。它们的和为：
$$ x(t) = x_1(t) + x_2(t) = \Re\{A_1 e^{j\phi_1} e^{j\omega t}\} + \Re\{A_2 e^{j\phi_2} e^{j\omega t}\} $$
由于取实部运算是线性的，我们可以将其合并：
$$ x(t) = \Re\{(A_1 e^{j\phi_1} + A_2 e^{j\phi_2}) e^{j\omega t}\} $$
令 $X_1 = A_1 e^{j\phi_1}$ 和 $X_2 = A_2 e^{j\phi_2}$ 分别为两个信号的相量。它们的和的[相量](@entry_id:270266)就是 $X = X_1 + X_2$。如果我们将 $X$ 写成极坐标形式 $X = R e^{j\theta}$，那么合成信号就是 $x(t) = R \cos(\omega t + \theta)$。新的幅度 $R$ 和相位 $\theta$ 就是复数 $X$ 的模和幅角。

例如，若 $x_1(t) = 3\cos(\omega_0 t + \frac{\pi}{6})$ 和 $x_2(t) = 2\cos(\omega_0 t + \frac{2\pi}{3})$，其相量分别为 $X_1 = 3e^{j\pi/6}$ 和 $X_2 = 2e^{j2\pi/3}$。这两个相量在复平面上恰好正交（相位差为 $\frac{\pi}{2}$），因此合成[相量](@entry_id:270266) $X = X_1 + X_2$ 的模（即合成幅度 $R$）可以通过[勾股定理](@entry_id:264352)计算：$R = |X| = \sqrt{|X_1|^2 + |X_2|^2} = \sqrt{3^2 + 2^2} = \sqrt{13}$。合成相位 $\theta$ 也可以通过几何关系轻易求得 [@problem_id:2868238]。

### 变换域中的[系统分析](@entry_id:263805)

为了[分析信号](@entry_id:190094)如何通过系统（特别是[LTI系统](@entry_id:271946)），我们常常将信号和系统从时域变换到[频域](@entry_id:160070)或更广义的$s$域。[拉普拉斯变换](@entry_id:159339)是这一过程中极其强大的工具。

#### [拉普拉斯变换](@entry_id:159339)及其与基本信号的关系

**拉普拉斯变换**（Laplace Transform）将一个时域信号 $x(t)$ 映射到一个复变量 $s$ 的函数 $X(s)$：
$$ X(s) = \mathcal{L}\{x(t)\} = \int_{-\infty}^{\infty} x(t) e^{-st} dt $$
这个积分并非对所有的复数 $s$ 都收敛。使积分[绝对收敛](@entry_id:146726)的 $s$ 的集合被称为**收敛域**（Region of Convergence, ROC）。

我们可以从这个定义出发，推导基本[正弦信号](@entry_id:196767)的拉普拉斯变换。关键步骤是利用欧拉公式将正弦/余弦分解为[复指数](@entry_id:162635)。对于一个基本的因果[复指数信号](@entry_id:273867) $e^{at}u(t)$，其[拉普拉斯变换](@entry_id:159339)是 $\frac{1}{s-a}$，[收敛域](@entry_id:269722)为 $\Re\{s\}  \Re\{a\}$。利用这一基本变换对，我们可以得到 [@problem_id:2868258]：
$$ \mathcal{L}\{\cos(\omega t)u(t)\} = \mathcal{L}\left\{\frac{e^{j\omega t} + e^{-j\omega t}}{2}u(t)\right\} = \frac{1}{2}\left(\frac{1}{s-j\omega} + \frac{1}{s+j\omega}\right) = \frac{s}{s^2 + \omega^2} $$
$$ \mathcal{L}\{\sin(\omega t)u(t)\} = \mathcal{L}\left\{\frac{e^{j\omega t} - e^{-j\omega t}}{2j}u(t)\right\} = \frac{1}{2j}\left(\frac{1}{s-j\omega} - \frac{1}{s+j\omega}\right) = \frac{\omega}{s^2 + \omega^2} $$
这两个变换的[收敛域](@entry_id:269722)都是 $\Re\{s\}  0$。变换结果的分母 $s^2 + \omega^2 = 0$ 的根，即 $s = \pm j\omega$，被称为系统的**极点**。对于纯[正弦信号](@entry_id:196767)，极点位于复平面（$s$-plane）的虚轴上。

#### [频移特性](@entry_id:272563)与阻尼正弦

[拉普拉斯变换](@entry_id:159339)的一个重要性质是**[频移特性](@entry_id:272563)**（或更准确地说是复频移）。它指出，如果 $\mathcal{L}\{f(t)\} = F(s)$，则：
$$ \mathcal{L}\{e^{\alpha t}f(t)\} = F(s-\alpha) $$
这个性质意味着，在时域中乘以一个指数项 $e^{\alpha t}$，等价于在 $s$ 域中将原函数的拉普拉斯变换沿着实轴平移 $\alpha$。

我们可以利用这个性质来求阻尼[正弦信号](@entry_id:196767) $x(t) = e^{\alpha t}\cos(\omega t)u(t)$ 的拉普拉斯变换 [@problem_id:2868246]。已知 $\mathcal{L}\{\cos(\omega t)u(t)\} = \frac{s}{s^2+\omega^2}$，根据[频移特性](@entry_id:272563)，我们只需将 $s$ 替换为 $s-\alpha$：
$$ X(s) = \mathcal{L}\{e^{\alpha t}\cos(\omega t)u(t)\} = \frac{s-\alpha}{(s-\alpha)^2 + \omega^2} $$
这个新变换的极点位于 $s = \alpha \pm j\omega$。与纯[正弦信号](@entry_id:196767)的极点 $(\pm j\omega)$ 相比，阻尼[正弦信号](@entry_id:196767)的极点在 $s$ 平面上从虚轴移动到了平行于[虚轴](@entry_id:262618)的直线 $\Re\{s\}=\alpha$ 上。这个几何上的平移直观地反映了时域中指数包络 $e^{\alpha t}$ 的影响。

#### 稳定性与[收敛域](@entry_id:269722)

一个[LTI系统](@entry_id:271946)的**有界输入有界输出（BIBO）稳定性**要求其冲激响应 $h(t)$ 是绝对可积的，即 $\int_{-\infty}^{\infty} |h(t)| dt  \infty$。对于一个由阻尼正弦 $h(t) = e^{\alpha t}\cos(\omega t)u(t)$ 描述的[因果系统](@entry_id:264914)，其稳定性的条件是什么？[@problem_id:2868260]

积分 $\int_{0}^{\infty} |e^{\alpha t}\cos(\omega t)| dt = \int_{0}^{\infty} e^{\alpha t}|\cos(\omega t)| dt$ 要收敛，指数项 $e^{\alpha t}$ 必须是一个衰减项，这要求 $\alpha  0$。如果 $\alpha = 0$，积分发散；如果 $\alpha > 0$，积分更会发散。因此，**BIBO稳定的充要条件是 $\alpha  0$**。

这个时域条件在 $s$ 域中有非常直观的对应。一个因果[LTI系统](@entry_id:271946)是BIBO稳定的，当且仅当其[传递函数](@entry_id:273897) $H(s)$ 的[收敛域](@entry_id:269722)（ROC）包含整个虚轴（$\Re\{s\}=0$）。对于我们的阻尼正弦系统，其[传递函数](@entry_id:273897) $H(s) = \frac{s-\alpha}{(s-\alpha)^2 + \omega^2}$ 的ROC是 $\Re\{s\} > \alpha$。为了让这个区域包含虚轴，必须满足 $0 > \alpha$，即 $\alpha  0$。这与[时域分析](@entry_id:755979)的结果完全一致。

因此，我们可以得到一个深刻的结论：对于一个[因果系统](@entry_id:264914)，其稳定性等价于其所有极点都位于 $s$ 平面的[左半平面](@entry_id:270729)（Left-Half Plane, LHP）。只有这样，其ROC（一个右半平面）才能包含[虚轴](@entry_id:262618)。这也意味着，只有当系统稳定时，其[傅里叶变换](@entry_id:142120) $H(j\omega)$ 才存在，因为它正是[拉普拉斯变换](@entry_id:159339) $H(s)$ 在虚轴上的取值 [@problem_id:2868260]。

### [LTI系统](@entry_id:271946)的正弦[稳态响应](@entry_id:173787)

理解了信号和系统在变换域中的表示后，我们可以来解决一个核心问题：一个稳定的[LTI系统](@entry_id:271946)在受到[正弦信号](@entry_id:196767)激励时，其长期行为是怎样的？

#### 复指数作为特征函数

[LTI系统](@entry_id:271946)的一个最基本也最重要的性质是：**[复指数信号](@entry_id:273867)是[LTI系统的特征函数](@entry_id:261343)**。这意味着，当输入是一个[复指数信号](@entry_id:273867) $x(t) = e^{j\omega t}$ 时，其输出也是一个同样频率的[复指数信号](@entry_id:273867)，只是被一个复常数加权（缩放和相移）：
$$ y(t) = H(j\omega) e^{j\omega t} $$
这里的复常数 $H(j\omega)$ 正是系统的**[频率响应](@entry_id:183149)**，即系统冲激响应 $h(t)$ 的[傅里叶变换](@entry_id:142120)，它充当了对应于特征函数 $e^{j\omega t}$ 的[特征值](@entry_id:154894)。

我们可以从卷积的定义出发严格证明这一点 [@problem_id:2868236]。输出 $y(t)$ 是冲激响应 $h(t)$ 与输入 $x(t)$ 的卷积：
$$ y(t) = \int_{-\infty}^{\infty} h(\tau) x(t-\tau) d\tau = \int_{-\infty}^{\infty} h(\tau) e^{j\omega(t-\tau)} d\tau $$
将 $e^{j\omega t}$ 提出积分号：
$$ y(t) = e^{j\omega t} \int_{-\infty}^{\infty} h(\tau) e^{-j\omega\tau} d\tau $$
积分部分正是[频率响应](@entry_id:183149) $H(j\omega)$ 的定义，因此 $y(t) = H(j\omega)e^{j\omega t}$。

对于实[正弦输入](@entry_id:269486) $x(t) = A\cos(\omega t + \phi) = \Re\{A e^{j\phi} e^{j\omega t}\}$，利用系统的线性，我们可以推断其[稳态](@entry_id:182458)输出 $y_{ss}(t)$ 为：
$$ y_{ss}(t) = \Re\{H(j\omega) \cdot (A e^{j\phi}) e^{j\omega t}\} $$
将频率响应写为极坐标形式 $H(j\omega) = |H(j\omega)|e^{j\arg H(j\omega)}$，输出可整理为：
$$ y_{ss}(t) = \Re\{A |H(j\omega)| e^{j(\omega t + \phi + \arg H(j\omega))}\} = A|H(j\omega)| \cos(\omega t + \phi + \arg H(j\omega)) $$
这个结果是信号处理的核心：一个[正弦信号](@entry_id:196767)通过[LTI系统](@entry_id:271946)后，其[稳态](@entry_id:182458)输出仍然是同频率的[正弦信号](@entry_id:196767)，但其**幅度被乘以 $|H(j\omega)|$**（系统在该频率的增益），**相位被加上 $\arg H(j\omega)$**（系统在该频率的相移）[@problem_id:2868236]。

#### 计算[稳态响应](@entry_id:173787)

基于上述原理，计算[稳态响应](@entry_id:173787)的步骤变得非常清晰。对于一个由[常系数](@entry_id:269842)[线性微分方程](@entry_id:150365)描述的系统，例如 [@problem_id:2868241]：
$$ \frac{d^{2}y}{dt^{2}} + 3\frac{dy}{dt} + 2y = 2\frac{dx}{dt} + 3x $$
我们可以通过将 $x(t)=e^{st}$ 和 $y(t)=H(s)e^{st}$ 代入方程来求得其[传递函数](@entry_id:273897) $H(s)$：
$$ ((s^2)H(s) + 3(s)H(s) + 2H(s))e^{st} = (2s+3)e^{st} \implies H(s) = \frac{2s+3}{s^2+3s+2} $$
对于一个[正弦输入](@entry_id:269486)，比如 $x(t) = 5\cos(2t - \pi/3)$，我们只需评估在 $\omega=2$ 处的[频率响应](@entry_id:183149) $H(j2)$：
$$ H(j2) = \frac{2(j2)+3}{(j2)^2+3(j2)+2} = \frac{3+j4}{-2+j6} $$
计算出这个[复数的模](@entry_id:634598) $|H(j2)|$ 和幅角 $\arg H(j2)$ 后，就可以直接写出[稳态](@entry_id:182458)输出。例如，幅度为 $A_{out} = A_{in}|H(j2)| = 5|H(j2)|$，相位为 $\phi_{out} = \phi_{in} + \arg H(j2) = -\frac{\pi}{3} + \arg H(j2)$ [@problem_id:2868241]。

#### 暂态与[稳态](@entry_id:182458)行为

需要强调的是，我们上面计算的是**[稳态响应](@entry_id:173787)**（steady-state response），即系统在输入作用足够长时间后达到的[长期行为](@entry_id:192358)。系统的**全响应**（total response）是[齐次解](@entry_id:274365)（homogeneous solution）和特解（particular solution）之和。
$$ y(t) = y_h(t) + y_p(t) $$
其中，[特解](@entry_id:149080) $y_p(t)$ 可以选择为我们求得的[稳态响应](@entry_id:173787) $y_{ss}(t)$。[齐次解](@entry_id:274365) $y_h(t)$ 的形式由系统的[特征方程](@entry_id:265849)（即[传递函数](@entry_id:273897)分母为零）决定。对于一个稳定的系统，其极点都在[左半平面](@entry_id:270729)，这意味着齐次解是随时间衰减的指数项的[线性组合](@entry_id:154743)。这部分响应被称为**暂态响应**（transient response）。
$$ \lim_{t \to \infty} y_h(t) = 0 \quad (\text{for a stable system}) $$
暂态响应的具体形式（即衰减项的系数）取决于系统的**初始条件**（如 $y(0)$ 和 $y'(0)$）。然而，由于它终将衰减至零，系统的[长期行为](@entry_id:192358)——[稳态响应](@entry_id:173787)——是**独立于初始条件**的，完全由输入信号和系统本身的特性（即[频率响应](@entry_id:183149) $H(j\omega)$）决定 [@problem_id:2868241]。