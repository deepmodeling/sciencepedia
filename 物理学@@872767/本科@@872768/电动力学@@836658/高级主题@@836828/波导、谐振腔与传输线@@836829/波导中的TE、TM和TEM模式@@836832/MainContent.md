## 引言
[波导](@entry_id:198471)是现代高频技术的核心构件，从雷达、卫星通信到[光纤](@entry_id:273502)网络和[粒子加速器](@entry_id:148838)，它们无处不在，扮演着引导[电磁能](@entry_id:264720)量高效传输的角色。然而，[电磁波](@entry_id:269629)在这些受限结构中的行为远比在自由空间中复杂。它们不再是简单的[平面波](@entry_id:189798)，而是以一系列被称为“模式”的特定场[分布](@entry_id:182848)形态存在。理解这些模式——特别是横电（TE）、横磁（TM）和横电磁（TEM）模式——是掌握和设计任何高频系统的基础。本文旨在填补从基础电磁理论到波导实际应用的知识鸿沟，系统性地解答[电磁波](@entry_id:269629)在波导中是如何传播的，是什么决定了其传播特性，以及这些特性如何被利用于工程实践。

在接下来的内容中，我们将开启一段从理论到应用的探索之旅。首先，在“原理与机制”一章中，我们将回归到电磁学的基石——麦克斯韦方程组，推导出描述波导中场[分布](@entry_id:182848)的通用方程，并在此基础上严格定义[TE、TM和TEM模](@entry_id:196916)式。我们将揭示“[截止频率](@entry_id:276383)”这一关键概念的物理本质，并深入探讨[波导](@entry_id:198471)的[色散](@entry_id:263750)特性如何影响[波的传播](@entry_id:144063)速度。随后，在“应用与跨学科联系”一章中，我们将看到这些抽象的模式理论如何在微波电路、天线系统、[光纤通信](@entry_id:269004)乃至与量子物理的类比中展现其强大的生命力。最后，通过“动手实践”环节，读者将有机会亲手计算[波导](@entry_id:198471)的关键参数，从而将理论知识内化为解决实际问题的能力。

## 原理与机制

在“引言”章节之后，我们深入探讨[电磁波](@entry_id:269629)在波导中传播的核心原理与机制。本章将系统地阐述[波导模式](@entry_id:275892)的分类、它们的传播特性，以及决定其行为的数学和物理基础。我们将从[麦克斯韦方程组](@entry_id:150940)出发，推导出描述[波导](@entry_id:198471)中场的基本方程，并在此基础上定义横电（TE）、横磁（TM）和横电磁（TEM）模式。

### [波导](@entry_id:198471)中场的通用表达式

为了理解波导内部的[电磁场](@entry_id:265881)结构，我们从无源、均匀、各向同性介质中的麦克斯韦方程组（[频域](@entry_id:160070)形式）开始：
$$
\begin{align*}
\nabla \times \mathbf{E}  = i \omega \mathbf{B} \\
\nabla \times \mathbf{B}  = -i \omega \mu \varepsilon \mathbf{E} \\
\nabla \cdot \mathbf{E}  = 0 \\
\nabla \cdot \mathbf{B}  = 0
\end{align*}
$$
其中 $\mathbf{E}$ 和 $\mathbf{B}$ 是[电场和磁场](@entry_id:261347)的[复振幅](@entry_id:164138)，$\omega$ 是[角频率](@entry_id:261565)，$\mu$ 和 $\varepsilon$ 分别是介质的磁导率和[介电常数](@entry_id:146714)。

我们考虑一个沿 $z$ 轴方向无限延伸的均匀[波导](@entry_id:198471)。在其中传播的单色波可以表示为：
$$
\begin{align*}
\mathbf{E}(x, y, z, t)  = \mathbf{E}(x, y) \exp(i(k_z z - \omega t)) \\
\mathbf{B}(x, y, z, t)  = \mathbf{B}(x, y) \exp(i(k_z z - \omega t))
\end{align*}
$$
这里的 $k_z$ 是沿 $z$ 轴的[传播常数](@entry_id:272712)。为了分析方便，我们将场分解为相对于传播方向的**横向分量**（下标 $t$）和**纵向分量**（下标 $z$）：
$$
\mathbf{E} = \mathbf{E}_t + E_z \hat{\mathbf{z}}, \qquad \mathbf{B} = \mathbf{B}_t + B_z \hat{\mathbf{z}}
$$
其中 $\mathbf{E}_t = E_x \hat{\mathbf{x}} + E_y \hat{\mathbf{y}}$ 和 $\mathbf{B}_t = B_x \hat{\mathbf{x}} + B_y \hat{\mathbf{y}}$。将梯度算符也进行分解 $\nabla = \nabla_t + \hat{\mathbf{z}} \frac{\partial}{\partial z}$，并利用 $\frac{\partial}{\partial z} \to i k_z$，我们可以将麦克斯韦旋度方程分解。经过一系列标准的[矢量代数](@entry_id:152340)运算，可以得到[横向场](@entry_id:266489)分量完全由[纵向场](@entry_id:264833)分量 $E_z$ 和 $B_z$ 及其横向梯度 $\nabla_t E_z$ 和 $\nabla_t B_z$ 决定的重要关系 [@problem_id:1608384]：
$$
\begin{align}
\mathbf{E}_t  = \frac{i}{k_c^2} (k_z \nabla_t E_z - \omega \hat{\mathbf{z}} \times \nabla_t B_z) \\
\mathbf{B}_t  = \frac{i}{k_c^2} (k_z \nabla_t B_z + \omega \mu \varepsilon \hat{\mathbf{z}} \times \nabla_t E_z)
\end{align}
$$
这里，$k^2 = \omega^2 \mu \varepsilon$，而 $k_c^2 = k^2 - k_z^2$ 是一个关键参数，我们很快会看到它代表**截止[波数](@entry_id:172452)** (cutoff wavenumber) 的平方。

这两个方程是[波导理论](@entry_id:264627)的基石。它们表明，只要我们能够确定两个标量场——纵向[电场](@entry_id:194326) $E_z(x, y)$ 和纵向[磁场](@entry_id:153296) $B_z(x, y)$，整个三维矢量场的完整结构就随之确定。这极大地简化了问题，将求解矢量场的问题转化为了求解两个标量场的问题。

### [波导模式](@entry_id:275892)的分类：TE, TM, 和 TEM

上述通用关系自然地引出了对[波导](@entry_id:198471)中可能存在的波型（即**模式**）的分类。这种分类基于[纵向场](@entry_id:264833)分量 $E_z$ 和 $B_z$ 是否为零。

#### 横电（TE）模式

**横电 (Transverse Electric, TE) 模式**的定义是，其[电场](@entry_id:194326)完全垂直于传播方向，即 $E_z = 0$。然而，其纵向[磁场](@entry_id:153296)分量必须存在，$B_z \neq 0$（否则将导致平凡的[零场](@entry_id:199169)解）。在此条件下，[横向场](@entry_id:266489)分量的通用表达式简化为 [@problem_id:1608384]：
$$
\mathbf{E}_t = -\frac{i\omega}{k_c^2} (\hat{\mathbf{z}} \times \nabla_t B_z), \qquad \mathbf{B}_t = \frac{ik_z}{k_c^2} \nabla_t B_z
$$
这清楚地表明，对于[TE模](@entry_id:269850)式，所有其他场分量都可以由纵向[磁场](@entry_id:153296)分量 $B_z$ 导出。

#### 横磁（TM）模式

与[TE模](@entry_id:269850)式对偶，**横磁 (Transverse Magnetic, TM) 模式**的定义是，其[磁场](@entry_id:153296)完全垂直于传播方向，即 $B_z = 0$。同时，其纵向[电场](@entry_id:194326)分量必须存在，$E_z \neq 0$。在此条件下，[横向场](@entry_id:266489)分量简化为 [@problem_id:1608384]：
$$
\mathbf{E}_t = \frac{ik_z}{k_c^2} \nabla_t E_z, \qquad \mathbf{B}_t = \frac{i\omega\mu\varepsilon}{k_c^2} (\hat{\mathbf{z}} \times \nabla_t E_z)
$$
对于[TM模](@entry_id:266144)式，所有其他场分量都可以由纵向[电场](@entry_id:194326)分量 $E_z$ 导出。

#### 横电磁（TEM）模式与空心波导

最简单的一种可能性是**横电磁 (Transverse ElectroMagnetic, TEM) 模式**，其定义为[电场和磁场](@entry_id:261347)都完全垂直于传播方向，即 $E_z = 0$ 且 $B_z = 0$。这种模式是自由空间中[平面波](@entry_id:189798)的直接推广。然而，一个重要的结论是：**由单个完美导体构成的空心[波导](@entry_id:198471)（即单连通区域）无法支持[TEM模](@entry_id:167534)式的传播**。

我们可以通过一个简洁的论证来证明这一点 [@problem_id:59149]。对于[TEM波](@entry_id:264727)，$E_z=0$，且由于波沿z轴传播，$\nabla \times \mathbf{E}$ 的纵向分量为 $\hat{\mathbf{z}} \cdot (\nabla_t \times \mathbf{E}_t) = i\omega B_z$。因为 $B_z=0$，我们得到 $\nabla_t \times \mathbf{E}_t = 0$。这意味着在[横截面](@entry_id:154995)内，横向[电场](@entry_id:194326)是无旋的，因此可以表示为一个标量势 $\phi(x, y)$ 的梯度：$\mathbf{E}_t = -\nabla_t \phi$。同时，在无源区域中，$\nabla \cdot \mathbf{E} = 0$ 给出 $\nabla_t \cdot \mathbf{E}_t = 0$。代入[势函数](@entry_id:176105)，我们得到二维的**拉普拉斯方程**：
$$
\nabla_t^2 \phi(x, y) = 0
$$
在波导的完美导体壁上，[电场](@entry_id:194326)的切向分量必须为零。这意味着[电势](@entry_id:267554) $\phi$ 在整个边界上必须是一个常数，记为 $V_0$。根据拉普拉斯方程[解的唯一性](@entry_id:143619)定理（[狄利克雷问题](@entry_id:274408)），在边界上为常数的唯一解是在整个区域内都为该常数，即 $\phi(x, y) = V_0$。这导致横向[电场](@entry_id:194326) $\mathbf{E}_t = -\nabla_t V_0 = 0$。[电场](@entry_id:194326)为零意味着不存在[电磁波的能量](@entry_id:275250)存储或传播。因此，在空心波导中不存在非平凡的[TEM模](@entry_id:167534)式。

值得注意的是，[TEM模](@entry_id:167534)式可以在由两个或多个分离的导体构成的[波导](@entry_id:198471)中传播，例如同轴电缆或双线[传输线](@entry_id:268055)。在这些结构中，不同导体边界上的[电势](@entry_id:267554)可以取不同常数值，从而允许存在非零的[电场](@entry_id:194326)和[TEM波](@entry_id:264727)的传播。

### 传播特性：截止与[色散](@entry_id:263750)

对于TE和[TM模](@entry_id:266144)式，[纵向场](@entry_id:264833)分量 $E_z$ 或 $B_z$ 必须满足二维[亥姆霍兹方程](@entry_id:149977)：
$$
(\nabla_t^2 + k_c^2) \psi(x, y) = 0
$$
其中 $\psi$ 代表 $E_z$ 或 $B_z$。这个方程与边界条件（[TM模](@entry_id:266144)式下 $E_z=0$，[TE模](@entry_id:269850)式下 $\partial B_z / \partial n = 0$）构成一个[本征值问题](@entry_id:142153)。其解只在一系列离散的 $k_c$ 值（[本征值](@entry_id:154894)）下存在。每个[本征值](@entry_id:154894) $k_c$ 对应一个特定的场[分布](@entry_id:182848)，即一个**模式**。

#### 截止频率与传播条件

$k_c$ 的物理意义通过**[色散关系](@entry_id:140395)**体现出来，该关系直接源于其定义 $k_c^2 = k^2 - k_z^2$：
$$
k_z^2 = \omega^2 \mu\varepsilon - k_c^2
$$
为了让[波能](@entry_id:164626)够沿 $z$ 轴传播（而不是衰减），[传播常数](@entry_id:272712) $k_z$ 必须是实数，这意味着 $k_z^2  0$。这要求：
$$
\omega^2 \mu\varepsilon  k_c^2 \quad \implies \quad \omega  \frac{k_c}{\sqrt{\mu\varepsilon}}
$$
我们定义**截止角频率** $\omega_c = k_c v$ 和**[截止频率](@entry_id:276383)** $f_c = \omega_c / (2\pi)$，其中 $v = 1/\sqrt{\mu\varepsilon}$ 是在填充介质中无界平面波的相速度。因此，一个模式只有在信号频率 $\omega$ **高于**其固有的截止频率 $\omega_c$ 时才能在波导中传播。

#### 隐失波

当信号频率 $\omega$ **低于**模式的[截止频率](@entry_id:276383) $\omega_c$ 时，$k_z^2  0$。此时[传播常数](@entry_id:272712) $k_z$ 变为纯虚数，通常写作 $k_z = i\alpha$，其中 $\alpha$ 是**衰减常数**：
$$
\alpha = \sqrt{k_c^2 - \omega^2 \mu\varepsilon}
$$
此时，场的 $z$ 向依赖关系变为 $\exp(ik_z z) = \exp(-\alpha z)$。这意味着场的振幅会随着距离 $z$ 指数衰减。这种不传播、仅在[波导](@entry_id:198471)入口附近存在的场被称为**隐失波**或**倏逝波**。它们不传输时间平均功率，而是存储活性（无功）能量。

这个特性有重要的实际应用，例如“截止[波导](@entry_id:198471)衰减器”。设想一个TE$_{10}$模式的[矩形波导](@entry_id:274822)，其尺寸为 $a=3.00 \text{ cm}$ 和 $b=1.50 \text{ cm}$，内部为真空 [@problem_id:1608383]。其[截止频率](@entry_id:276383)为 $f_c = c/(2a) = (3 \times 10^8)/(2 \times 0.03) = 5 \text{ GHz}$。如果一个频率为 $f = 4.00 \text{ GHz}$ 的信号被注入，由于 $f  f_c$，该模式将是隐失的。我们可以计算其衰减常数 $\alpha = \sqrt{(\pi/a)^2 - (2\pi f/c)^2} \approx 20\pi \text{ m}^{-1}$。波的功率与场振幅的平方成正比，因此功率衰减为 $P(z) = P(0)\exp(-2\alpha z)$。要使功率衰减到初始值的1.00%，即 $P(z)/P(0) = 0.01$，所需的距离为 $z = \ln(100)/(2\alpha) \approx 3.66 \text{ cm}$。这表明即使在完美导体中，低于[截止频率](@entry_id:276383)的波也会被迅速衰减。

#### [色散关系](@entry_id:140395)与波速

对于传播的模式（$\omega  \omega_c$），[色散关系](@entry_id:140395) $k_z^2 + k_c^2 = k^2$ 揭示了[波导](@entry_id:198471)的[色散](@entry_id:263750)特性。我们可以用波长来重写这个关系 [@problem_id:1608368]。定义自由空间波长 $\lambda_0 = 2\pi/k_0$（对于真空中的 $k_0 = \omega/c$），截止波长 $\lambda_c = 2\pi/k_c$，以及**导[内波](@entry_id:261048)长** $\lambda_g = 2\pi/k_z$。将 $k_z=2\pi/\lambda_g$, $k_c=2\pi/\lambda_c$, $k=2\pi/\lambda$（$\lambda$为介质中无界波波长）代入[色散关系](@entry_id:140395)并除以 $(2\pi)^2$，得到：
$$
\frac{1}{\lambda_g^2} + \frac{1}{\lambda_c^2} = \frac{1}{\lambda^2}
$$
这个关系式如同一座桥梁，连接了波的固有属性（$\lambda$）、[波导](@entry_id:198471)的几何与模式属性（$\lambda_c$）以及波在[波导](@entry_id:198471)中传播的表观波长（$\lambda_g$）。

波在[波导](@entry_id:198471)中的**相速度** $v_p$ 定义为等相位面移动的速度，即 $v_p = \omega/k_z$。利用色散关系，我们可以得到 [@problem_id:1608413]：
$$
v_p = \frac{\omega}{\sqrt{k^2 - k_c^2}} = \frac{\omega/k}{\sqrt{1 - (k_c/k)^2}} = \frac{v}{\sqrt{1 - (\omega_c/\omega)^2}}
$$
由于根号内的项小于1，所以 $v_p$ 总是**大于**介质中无界[平面波](@entry_id:189798)的相速度 $v$。这并不违反相对论，因为相速度描述的并非信息或能量的传递速度。能量和信息的传递速度由**[群速度](@entry_id:147686)** $v_g = d\omega/dk_z$ 描述。对[色散关系](@entry_id:140395)求导可得：
$$
v_g = v \sqrt{1 - (\omega_c/\omega)^2}
$$
[群速度](@entry_id:147686) $v_g$ 总是**小于** $v$。可以发现，相速度和群速度之间存在一个优美的关系：$v_p v_g = v^2$。

### [矩形波导](@entry_id:274822)中的模式

为了将上述抽象概念具体化，我们以最常见的[矩形波导](@entry_id:274822)为例进行分析。设波导[横截面](@entry_id:154995)尺寸为 $a \times b$（$x \in [0, a], y \in [0, b]$）。

对于**[TE模](@entry_id:269850)式**，我们求解[亥姆霍兹方程](@entry_id:149977) $(\nabla_t^2 + k_c^2) B_z = 0$，边界条件为 $\partial B_z/\partial x = 0$ 在 $x=0,a$ 处，以及 $\partial B_z/\partial y = 0$ 在 $y=0,b$ 处。其通解形式为：
$$
B_z(x, y) = B_0 \cos\left(\frac{m\pi x}{a}\right) \cos\left(\frac{n\pi y}{b}\right)
$$
其中 $m, n$ 是定义模式的整数。代入[亥姆霍兹方程](@entry_id:149977)，得到TE$_{mn}$模式的截止[波数](@entry_id:172452)和截止频率：
$$
k_{c,mn}^2 = \left(\frac{m\pi}{a}\right)^2 + \left(\frac{n\pi}{b}\right)^2, \qquad f_{c,mn} = \frac{v}{2} \sqrt{\left(\frac{m}{a}\right)^2 + \left(\frac{n}{b}\right)^2}
$$
[TE模](@entry_id:269850)式要求 $m, n$ 不全为零。

对于**[TM模](@entry_id:266144)式**，我们求解 $(\nabla_t^2 + k_c^2) E_z = 0$，边界条件为 $E_z=0$ 在所有四个壁上。其通解形式为：
$$
E_z(x, y) = E_0 \sin\left(\frac{m\pi x}{a}\right) \sin\left(\frac{n\pi y}{b}\right)
$$
TM$_{mn}$模式的截止频率公式与TE$_{mn}$模式相同。但由于 $\sin(0)=0$，若 $m$ 或 $n$ 为零，将导致 $E_z$ 恒为零，所以[TM模](@entry_id:266144)式要求 $m \geq 1$ 和 $n \geq 1$。

#### [主模](@entry_id:263463)与多模传播

具有最低非零[截止频率](@entry_id:276383)的模式被称为**[主模](@entry_id:263463) (dominant mode)**。对于常规[矩形波导](@entry_id:274822)（约定 $a  b$），通过比较不同 $(m,n)$ 组合的 $f_{c,mn}$ 值可知，TE$_{10}$ 模式的[截止频率](@entry_id:276383) $f_{c,10} = v/(2a)$ 是最低的。因此，TE$_{10}$ 是标准[矩形波导](@entry_id:274822)的[主模](@entry_id:263463)。

当工作频率 $f_{op}$ 满足 $f_{c,10}  f_{op}  f_{\text{next lowest}}$ 时，波导中只能传播TE$_{10}$模式，这称为**单模工作区**。若工作频率进一步提高，使得多个模式的截止频率都低于工作频率，则这些模式都可以被激励并在波导中同时传播，形成**多模传播** [@problem_id:1608414]。例如，对于一个 $a=2b$ 的[波导](@entry_id:198471)，[主模](@entry_id:263463)是TE$_{10}$，其[截止频率](@entry_id:276383)为 $f_{c,10}=c/(2a)$。下一个模式是TE$_{20}$ 和TE$_{01}$，它们的截止频率均为 $f_{c,20}=c/a=2f_{c,10}$ 和 $f_{c,01}=c/(2b)=c/a=2f_{c,10}$。如果工作频率设定为 $f_{op} = 2.15 f_{c,10}$，那么TE$_{10}$、TE$_{20}$ 和 TE$_{01}$ 模式都将传播，因为它们的[截止频率](@entry_id:276383)都低于 $f_{op}$。

#### 模式简并

当两个或多个不同的模式具有相同的截止频率时，称它们是**简并的 (degenerate)**。在[矩形波导](@entry_id:274822)中，如果 $a=b$（方形[波导](@entry_id:198471)），那么TE$_{mn}$ 和 TE$_{nm}$ 模式的截止频率相同，它们就是简并的。例如，TE$_{12}$ 和 TE$_{21}$ 在方形波导中是简并的。更有趣的简并发生在某些特定的几何和模式组合中，这源于数论中的毕达哥拉斯和 [@problem_id:1608401]。例如，在一个方形波导中，由于 $2^2 + 11^2 = 125 = 5^2 + 10^2$，TE$_{2,11}$ 模式和 TE$_{5,10}$ 模式就是一对非显然的[简并模式](@entry_id:196301)。

#### TE$_{10}$ 模式的场结构

作为最重要的模式，我们来详细考察TE$_{10}$模式的场结构 [@problem_id:1608380]。对于此模式，$m=1, n=0$。
纵向[磁场](@entry_id:153296)为 $B_z \propto \cos(\pi x / a)$。
利用前面导出的[TE模](@entry_id:269850)式场分量公式，可以得到：
-   $E_z = 0$ (定义)
-   $E_x = 0$
-   $E_y \propto \sin(\pi x / a)$
-   $B_x \propto \sin(\pi x / a)$
-   $B_y = 0$

这表明，TE$_{10}$模式的[电场](@entry_id:194326)只有一个分量 $E_y$，其方向处处垂直于波导的宽边。[电场](@entry_id:194326)强度在波导中心 ($x=a/2$) 处最强，在两侧壁 ($x=0, a$) 处为零，满足边界条件。横向[磁场](@entry_id:153296)只有一个分量 $B_x$，其[分布](@entry_id:182848)与 $E_y$ 类似。总[磁场](@entry_id:153296)还包含一个纵向分量 $B_z$，其在[波导](@entry_id:198471)中心处最弱，而在两侧壁附近最强。

### [波导](@entry_id:198471)中的能量与功率

[电磁波](@entry_id:269629)在波导中传播时，不仅携带能量，其[电场和磁场](@entry_id:261347)中也存储着能量。

#### 传输功率

[波导](@entry_id:198471)传输的时间平均功率可以通过对[时间平均](@entry_id:267915)坡印亭矢量 $\langle \mathbf{S} \rangle = \frac{1}{2\mu} \text{Re}\{\mathbf{E} \times \mathbf{B}^*\}$ 在[波导](@entry_id:198471)[横截面](@entry_id:154995) $A$ 上积分得到：
$$
P = \int_A \langle S_z \rangle dA = \frac{1}{2\mu} \int_A \text{Re}\{E_x B_y^* - E_y B_x^*\} dA
$$
通过将TE或[TM模](@entry_id:266144)式的场分量表达式代入，可以计算出任意模式传输的功率。例如，对于一个一般的TE$_{mn}$模式，其传输的功率可以表示为纵向[磁场](@entry_id:153296)振幅 $B_0$、频率 $\omega$、[传播常数](@entry_id:272712) $k_z$ 以及波导几何参数的函数 [@problem_id:1608395]。经过详细推导，可以得到功率为：
$$
P = \frac{\omega k_z ab}{8 \mu k_{c,mn}^2} B_0^2
$$
这个结果（对于 $m0, n0$ 的情况）将微观的场振幅与宏观的可测量量——功率联系起来。

#### 能量存储

[时间平均](@entry_id:267915)的[电场](@entry_id:194326)[储能](@entry_id:264866)密度和[磁场](@entry_id:153296)储能密度分别为 $\langle u_e \rangle = \frac{1}{4}\epsilon |\mathbf{E}|^2$ 和 $\langle u_m \rangle = \frac{1}{4\mu} |\mathbf{B}|^2$。单位长度内存储的能量 $W_e$ 和 $W_m$ 是通过对这些密度函数在[横截面](@entry_id:154995)上积分得到的。

一个深刻的物理洞见来自于分析[TE模](@entry_id:269850)式中不同场分量存储的能量 [@problem_id:1608407]。对于任意[TE模](@entry_id:269850)式，我们可以计算单位长度内纵向[磁场](@entry_id:153296)存储的能量 $W_{m,z}$与[电场](@entry_id:194326)存储的能量 $W_e$ 之比。利用[格林第一恒等式](@entry_id:170345)和[亥姆霍兹方程](@entry_id:149977)，可以证明一个普适关系：
$$
\frac{W_{m,z}}{W_e} = \frac{\int_A \frac{1}{4\mu} |B_z|^2 dA}{\int_A \frac{1}{4}\epsilon |\mathbf{E}_t|^2 dA} = \left(\frac{\omega_c}{\omega}\right)^2
$$
这个简洁的结果揭示了[TE模](@entry_id:269850)式能量[分布](@entry_id:182848)的动态特性。当工作频率 $\omega$ 刚刚超过[截止频率](@entry_id:276383) $\omega_c$ 时，该比值接近1，表明纵向[磁场中的能量](@entry_id:262427)与（必然存在的）横向[电场](@entry_id:194326)中的能量相当。随着工作频率远高于[截止频率](@entry_id:276383)（$\omega \gg \omega_c$），该比值趋于零，意味着大部分能量都存储在[横向场](@entry_id:266489)分量中，波的特性越来越接近[TEM波](@entry_id:264727)。可以进一步证明，单位长度内横向[磁场](@entry_id:153296)存储的能量满足 $W_{m,t} = W_e(k_z/k)^2$。因此，总的[磁储能](@entry_id:274401) $W_m = W_{m,t} + W_{m,z} = W_e[(k_z/k)^2 + (\omega_c/\omega)^2] = W_e[(k_z/k)^2 + (k_c/k)^2] = W_e$。这表明，对于在无损耗[波导](@entry_id:198471)中传播的行波，总的时间平均[电场](@entry_id:194326)储能与[磁场](@entry_id:153296)储能是相等的（$W_m = W_e$）。

本章系统地建立了波导中[电磁波传播](@entry_id:272130)的理论框架，从场的分类到其传播、衰减、功率和能量的详细特性。这些原理不仅是理解[微波工程](@entry_id:274335)和[光子](@entry_id:145192)学器件的基础，也为后续章节中分析具体[波导](@entry_id:198471)器件（如耦合器、[谐振腔](@entry_id:274488)等）提供了必要的工具。