## 引言
在计算科学与工程的众多领域，从预测飞机噪声到模拟地震波，高保真地模拟波的传播现象至关重要。然而，当使用数值方法求解描述波动的偏微分方程时，离散化的过程不可避免地会引入误差。这些误差，主要表现为数值色散（不同频率的波以错误的速度传播）和数值耗散（波的能量被不物理地削弱），在短时程模拟中或许并不显著，但在长距离、长时间的模拟中会逐渐累积，最终导致波形严重失真，使模拟结果失去物理意义。

为了解决这一根本性难题，研究人员发展出了一类先进的数值技术——色散关系保持（Dispersion-Relation-Preserving, DRP）格式。与传统高阶格式追求在单一点上无限逼近不同，DRP格式的设计哲学是在整个感兴趣的频率范围内，系统性地最小化数值传播特性与真实物理传播特性之间的差异。这种方法能够以极高的保真度维持波的相位和振幅，使其成为现代高精度波传播模拟的基石。

本文将系统地引导您深入理解DRP格式的世界。在第一章“原理与机制”中，我们将建立傅里叶分析框架，精确剖析数值误差的来源，并详细阐述DRP格式的设计与优化原理，包括关键的时空误差耦合问题。随后，在第二章“应用与跨学科联系”中，我们将展示DRP格式在计算航空声学、地球物理学等前沿领域的强大应用，并探讨其设计思想如何解决边界条件、复杂几何和非线性等高级挑战。最后，在第三章“动手实践”中，您将通过一系列精心设计的编程练习，亲手实现和分析DRP格式，将理论知识转化为解决实际问题的能力。

## 原理与机制

本章旨在深入剖析计算声学中数值格式的核心原理与机制，重点关注其如何影响波传播的模拟精度。我们将首先建立一套傅里叶分析框架，用以精确量化由空间和时间离散化引入的两种主要数值误差：**数值色散（numerical dispersion）**和**数值耗散（numerical dissipation）**。随后，我们将阐明为何在长距离波传播模拟中，这些看似微小的误差会累积并导致严重的精度损失。最后，我们将系统地介绍色散关系保持（Dispersion-Relation-Preserving, DRP）格式的设计哲学与构建方法，并探讨如何通过时空耦合分析来进一步优化其性能。

### 数值色散与耗散的傅里叶分析

为了在数学上精确地描述数值误差，我们采用傅里叶分析方法。该方法通过考察数值格式对单个平面波（即傅里叶模态）的作用，来揭示其内在的传播特性。

#### 色散关系与修正波数

我们从最简单的一维线性平流方程入手，它是在均匀介质中声波传播的典型模型：
$$
\frac{\partial u}{\partial t} + c \frac{\partial u}{\partial x} = 0
$$
其中 $u(x,t)$ 是声学扰动场（如声压或质点速度），$c$ 是恒定的声速。该偏微分方程（PDE）的平面波解形式为 $u(x,t) = \exp(i(kx - \omega t))$，其中 $k$ 是波数，$\omega$ 是角频率。将此解代入方程，我们得到连续介质的**色散关系**：
$$
\omega = ck
$$
这个线性关系意味着所有频率分量的波都以相同的相速度 $c$ 传播，因此波形在传播过程中保持不变。这是一个**非色散**系统。

然而，当我们在一个空间步长为 $\Delta x$ 的均匀网格上对空间导数 $\partial u / \partial x$ 进行离散化时，情况发生了改变。考虑一个通用的 $(2M+1)$ 点中心差分格式 [@problem_id:4120589] [@problem_id:4120645]：
$$
\left( \mathcal{D}u \right)_j = \frac{1}{\Delta x} \sum_{m=-M}^{M} d_m u_{j+m}
$$
其中 $u_j(t) = u(j\Delta x, t)$ 是网格点 $j$ 上的解，系数 $d_m$ 满足反对称性 $d_{-m} = -d_m$（因此 $d_0=0$），以确保对一阶导数的近似。此时，原PDE被转化为一个半离散的常微分方程组：$\frac{du_j}{dt} + c (\mathcal{D}u)_j = 0$。

为了分析这个半离散系统的行为，我们考察它对一个空间傅里叶模态 $u_j(t) = \hat{u}(t) \exp(i k x_j)$ 的作用，其中 $x_j=j\Delta x$。将此模态代入差分算子，我们得到：
$$
(\mathcal{D}u)_j = \frac{1}{\Delta x} \sum_{m=-M}^{M} d_m \exp(i k (j+m)\Delta x) = \frac{\exp(ikj\Delta x)}{\Delta x} \sum_{m=-M}^{M} d_m e^{imk\Delta x}
$$
由于 $d_{-m} = -d_m$，求和部分可以简化为纯虚数：
$$
\sum_{m=-M}^{M} d_m e^{imk\Delta x} = \sum_{m=1}^{M} d_m (e^{imk\Delta x} - e^{-imk\Delta x}) = 2i \sum_{m=1}^{M} d_m \sin(m k \Delta x)
$$
因此，差分算子作用于傅里叶模态等效于一个乘法运算：
$$
(\mathcal{D}u)_j = i \left( \frac{2}{\Delta x} \sum_{m=1}^{M} d_m \sin(m k \Delta x) \right) u_j
$$
我们将括号内的项定义为**修正波数（modified wavenumber）**，记作 $k^*$：
$$
k^*(k) = \frac{2}{\Delta x} \sum_{m=1}^{M} d_m \sin(m k \Delta x)
$$
这个量是理解数值色散的关键。它揭示了离散网格对于波数为 $k$ 的波的“感知”波数。半离散方程现在可以写成一个简单的常微分方程：
$$
\frac{d\hat{u}}{dt} + c (i k^* \hat{u}) = 0 \quad \implies \quad \frac{d\hat{u}}{dt} = -ic k^* \hat{u}
$$
这个方程的解为 $\hat{u}(t) = \hat{u}(0) \exp(-ic k^* t)$。这表明，数值解的角频率 $\omega_{\text{num}}$ 与修正波数 $k^*$ 之间遵循着与连续系统相似的规律，即半离散系统的色散关系为：
$$
\omega_{\text{num}} = c k^*(k)
$$
理想情况下，我们希望 $k^*(k) = k$，这样数值色散关系就能精确复现物理色散关系 $\omega=ck$。然而，对于任何有限尺寸的差分格式，$k^*$ 通常是一个关于 $k$ 的非线性三角函数，它只在 $k \to 0$ 的极限下才趋近于 $k$。$k^*$ 与 $k$ 之间的差异导致了**数值色散**：不同波长的数值波以不同的速度传播，即使在物理上它们应该具有相同的速度。这会导致波包在传播过程中发生变形和相位失真。我们通常使用无量纲波数 $\xi = k\Delta x$ 来分析色散特性，此时修正波数也相应地无量纲化为 $\kappa^*(\xi) = k^* \Delta x = 2 \sum_{m=1}^{M} d_m \sin(m \xi)$ [@problem_id:4120589]。数值相速度为 $c_{p, \text{num}}(k) = \omega_{\text{num}}/k = c k^*/k$。

#### 数值耗散与复频率

当我们将时间积分也离散化后，就得到了一个全离散格式。一个全离散格式的平面波解可以写为 $u_j^n = \hat{u} \exp(i(k j \Delta x - \omega(k) n \Delta t))$，其中 $\omega(k)$ 是由全离散格式决定的复数角频率。解从一个时间步 $n$ 到下一步 $n+1$ 的演化由一个复数放大因子 $G(k)$ 控制：
$$
u_j^{n+1} = G(k) u_j^n = \exp(-i \omega(k) \Delta t) u_j^n
$$
放大因子的模 $|G(k)|$ 决定了波幅度的变化。为了考察这一点，我们将复频率 $\omega(k)$ 分解为实部和虚部：$\omega(k) = \operatorname{Re}(\omega) + i \operatorname{Im}(\omega)$。于是放大因子的模为 [@problem_id:4120590]：
$$
|G(k)| = |\exp(-i(\operatorname{Re}(\omega) + i\operatorname{Im}(\omega))\Delta t)| = |\exp(\operatorname{Im}(\omega)\Delta t) \cdot \exp(-i\operatorname{Re}(\omega)\Delta t)| = \exp(\operatorname{Im}(\omega)\Delta t)
$$
由此可见：
-   如果 $\operatorname{Im}(\omega)  0$，则 $|G(k)|  1$，波的振幅随时间指数衰减。这被称为**数值耗散**，它会不物理地削弱波的能量。
-   如果 $\operatorname{Im}(\omega) > 0$，则 $|G(k)| > 1$，波的振幅随时间指数增长，导致数值**不稳定性**。
-   如果 $\operatorname{Im}(\omega) = 0$，则 $|G(k)| = 1$，波的振幅保持不变，格式是**保幅的（non-dissipative）**。

我们可以通过计算波传播一个波长 $\lambda=2\pi/k$ 后的振幅比 $R_\lambda$ 来量化耗散效应。波传播一个波长所需的时间为 $T_\lambda = \lambda / v_p(k)$，其中数值相速度 $v_p(k) = \operatorname{Re}(\omega)/k$。经过推导，可得振幅比为 [@problem_id:4120590]：
$$
R_\lambda = \exp\left( \frac{2\pi \operatorname{Im}(\omega)}{\operatorname{Re}(\omega)} \right)
$$
这个表达式清晰地表明，复频率的虚部与实部之比决定了每个波长上的振幅衰减率。一个理想的数值格式应该在感兴趣的波数范围内尽可能地使 $\operatorname{Im}(\omega)$ 趋近于零。

### 长距离传播中的累积误差效应

在许多声学应用中，如水声通信或地震波勘探，波需要传播数百甚至数千个波长。在这种情况下，即使每个波长上产生的微小相位误差，也会累积到足以完全破坏波场相干性的程度。

考虑一个单色平面波，其数值相速度 $c_{p,\text{num}}(k)$ 与真实相速度 $c$ 存在一个相对误差 $\varepsilon_c(k) = (c_{p,\text{num}}(k)-c)/c$。当波传播距离 $L$ 时，其真实解的相位变化为 $kL$。而数值解的相位变化为 $k_{\text{num}}L = (\omega_{\text{num}}/c_{p,\text{num}})L$，但更直接的比较是在同一物理时间 $T \approx L/c$ 进行。数值解的相位为 $\phi_{\text{num}} = kL - \omega_{\text{num}} T$，真实解的相位为 $\phi_{\text{ex}} = kL - \omega T$。累积的相位误差为：
$$
\Delta \phi = \phi_{\text{num}} - \phi_{\text{ex}} = (\omega - \omega_{\text{num}})T = (ck - c_{p,\text{num}}k) \frac{L}{c} = -kL \frac{c_{p,\text{num}}-c}{c} = -kL \varepsilon_c(k)
$$
若传播距离 $L$ 包含 $N$ 个波长，即 $L = N\lambda = N(2\pi/k)$，则累积相位误差的量级为 [@problem_id:4120636]：
$$
|\Delta \phi| \approx 2\pi N |\varepsilon_c(k)|
$$
这个简单的关系式揭示了一个严峻的现实：总相位误差与传播的波长数 $N$ 成正比。例如，即使一个数值格式的相速度误差仅为 $0.1\%$（$|\varepsilon_c| = 0.001$），在传播仅100个波长后，累积的相位误差就将达到 $|\Delta \phi| \approx 2\pi \times 100 \times 0.001 = 0.628$ 弧度，约 $36^\circ$，这是一个不可忽略的误差。若要将总相位误差控制在例如 $\pi/4$（$45^\circ$）以内，则要求相速度的相对误差必须满足 $|\varepsilon_c(k)| \lesssim 1/(8N)$。对于长距离传播（大的 $N$），这对数值格式的相位精度提出了极高的要求。

值得注意的是，对于由多个频率分量构成的波包或波束，其整体包络的传播由**群速度** $c_g = d\omega/dk$ 控制，而其内部的相干结构（如干涉条纹）则由**相速度** $c_p = \omega/k$ 决定。因此，一个优秀的数值格式不仅要精确模拟群速度以保证波包位置的准确性，更要以极高的精度匹配相速度，以维持长距离传播后的相干性 [@problem_id:4120636]。这正是DRP格式设计的核心动机。

### 色散关系保持（DRP）格式的设计

DRP格式的核心思想是，放弃在单点（$k=0$）上追求极致的泰勒级数精度，转而寻求在整个感兴趣的波数频带上，使数值色散关系与物理色散关系之间的误差最小化。

#### 传统高阶格式与DRP格式的对比

**传统高阶格式**的设计方法是通过在波数原点 $k=0$ 处匹配尽可能多的泰勒展开项来确定差分系数。这等价于要求格式能精确计算尽可能高阶的多项式的导数。例如，我们来构建一个六阶精度的中心差分格式来近似一阶导数 [@problem_id:4120645]。其半宽 $M=3$ 的差分算子形式为：
$$
D_x u_i = \frac{1}{\Delta x} \sum_{j=1}^{3} a_j (u_{i+j} - u_{i-j})
$$
其无量纲修正波数 $\kappa^*(\xi) = 2\sum_{j=1}^{3} a_j \sin(j\xi)$。为了达到六阶精度，即 $\kappa^*(\xi) = \xi + \mathcal{O}(\xi^7)$，我们需要其泰勒展开的前三项（$\xi^1, \xi^3, \xi^5$ 的系数）与 $\xi$ 的展开相匹配：
$$
\begin{cases}
    2\sum_{j=1}^{3} j a_j = 1 \\
    2\sum_{j=1}^{3} j^3 a_j = 0 \\
    2\sum_{j=1}^{3} j^5 a_j = 0
\end{cases}
$$
解这个线性方程组可以得到唯一的系数：$\{a_1, a_2, a_3\} = \{\frac{3}{4}, -\frac{3}{20}, \frac{1}{60}\}$。这种格式在低波数（$\xi \ll 1$）区域具有极高的精度，但随着波数的增加，其色散误差会迅速增大。

相比之下，**DRP格式**的设计目标不同。它不追求在 $\xi=0$ 点的无限逼近，而是力图在某个目标波数区间 $[0, \xi_c]$ 内，使数值色散关系 $\omega_{\text{num}} = c k^*$ 整体上最接近物理色散关系 $\omega=ck$。这通常通过求解一个优化问题来实现 [@problem_id:4120589]。例如，选择差分系数 $\{d_m\}$ 来最小化一个积分形式的色散误差：
$$
\min_{\{d_m\}} \int_{0}^{\xi_c} W(\xi) [\kappa^*(\xi) - \xi]^2 d\xi
$$
其中 $W(\xi)$ 是一个可选的权重函数。这种方法牺牲了在原点处的最高阶精度，换取了在更宽波数范围内的良好表现。

#### DRP格式的优化构建

将DRP设计形式化为一个约束优化问题是其核心构建方法。以一阶导数的 $(2M+1)$-点中心差分格式为例 [@problem_id:4120614]，其设计问题可以表述为：

选择系数向量 $\mathbf{a} = [a_1, \dots, a_M]^T$ 以最小化目标函数：
$$
J(\mathbf{a}) = \int_{0}^{k_{\max}} (k^*(k) - k)^2 dk = \frac{1}{(\Delta x)^3} \int_{0}^{\kappa_{\max}} \left( 2\sum_{m=1}^{M} a_m \sin(m\kappa) - \kappa \right)^2 d\kappa
$$
同时满足一组线性约束条件。这些约束通常用于保证格式的基本一致性和对低阶多项式的精确性。例如，为了保证至少六阶的局部截断误差，需要满足以下矩条件：
$$
\sum_{m=1}^{M} m a_m = \frac{1}{2}, \quad \sum_{m=1}^{M} m^3 a_m = 0, \quad \sum_{m=1}^{M} m^5 a_m = 0
$$
这个框架同样适用于二阶导数。例如，对于波动方程 $\partial_{tt} u = c^2 \partial_{xx} u$ 的一个五点中心差分格式 [@problem_id:4120585]，其半离散色散关系为 $\omega^2(\xi) = -\frac{c^2}{h^2} A(\xi)$，其中 $A(\xi)$ 是差分算子的符号。一个合理的DRP目标是最小化相速度误差，即最小化：
$$
J = \int_{0}^{\xi_{\max}} \left( \frac{\sqrt{-A(\xi)}}{\xi} - 1 \right)^2 d\xi
$$
同时满足一致性约束，如 $a_0+2a_1+2a_2=0$ 和 $a_1+4a_2=1$。

通过求解这类约束优化问题，可以得到在指定波数范围内具有最优色散特性的差分系数。例如，一个经典的四阶精度五点中心差分格式 [@problem_id:4120634] 可以通过设置 $\alpha = 2/3, \beta = -1/12$ 得到，其无量纲相速度比为：
$$
\frac{c_p(k)}{c} = \frac{k^*(k)}{k} = \frac{2}{k\Delta x} \left( \frac{2}{3}\sin(k\Delta x) - \frac{1}{12}\sin(2k\Delta x) \right) = \frac{\sin(k\Delta x)}{k\Delta x} \left(\frac{4}{3} - \frac{1}{3}\cos(k\Delta x)\right)
$$
这个表达式精确地描述了该格式的色散行为，可用于评估其在不同波数下的性能。

#### 显式与紧致格式

前面讨论的差分格式大多是**显式的**，即一个点的导数值仅由其周围点的函数值直接计算。另一类重要的格式是**紧致（或隐式）格式**，其一个点的导数值通过求解一个包含邻近点导数值的线性方程组来获得。

一个典型的三对角紧致一阶导数格式定义如下 [@problem_id:4120618]：
$$
\alpha D_{i-1} + D_i + \alpha D_{i+1} = \frac{1}{2h} [a(u_{i+1} - u_{i-1}) + b(u_{i+2} - u_{i-2})]
$$
其中 $D_i$ 是在 $i$ 点的导数近似值。通过傅里叶分析，假定 $D_i = i k^* u_i$，我们可以推导出其修正波数 $k^*$。将 $u_i = \exp(ikh)$ 和 $D_i$ 的关系代入上式，经过整理可得：
$$
i k^* u_i (1 + 2\alpha \cos(kh)) = \frac{iu_i}{h} (a\sin(kh) + b\sin(2kh))
$$
解出 $k^*$ 可得：
$$
k^*(k) = \frac{a\sin(kh) + b\sin(2kh)}{h(1+2\alpha\cos(kh))} = \frac{(a + 2b\cos(kh))\sin(kh)}{h(1+2\alpha\cos(kh))}
$$
可以看到，紧致格式的修正波数是一个有理函数，分母的存在提供了更多的自由度来优化色散特性。通常，在相同的计算模板宽度下，精心设计的紧致格式比显式格式具有更优的色散和耗散特性，因此在高精度模拟中得到广泛应用。

### 时间积分与时空色散耦合

到目前为止，我们的讨论主要集中在空间离散。然而，全离散格式的总误差是空间和时间离散误差共同作用的结果。

#### 时间积分器的色散特性

时间积分方法同样会引入数值误差。考虑一个已经空间离散化的系统，其单个傅里叶模态的时间演化遵循方程 $u_t = i\omega_s u$，其中 $\omega_s = -c k^*$ 是由空间差分决定的半离散频率（假定为实数）。当我们使用一个时间积分器（如Runge-Kutta方法）来求解这个常微分方程时，数值解的相位将进一步偏离真实解。

以经典的四阶Runge-Kutta (RK4) 方法为例 [@problem_id:4120620]。将其应用于 $u_t = i\omega u$（此处 $\omega$ 代表 $\omega_s$），时间步长为 $\Delta t$，并令 $\theta = \omega \Delta t$。经过推导，可以得到单步演化的放大因子 $G(\theta)$：
$$
G(\theta) = 1 + i\theta + \frac{(i\theta)^2}{2} + \frac{(i\theta)^3}{6} + \frac{(i\theta)^4}{24} = \left(1 - \frac{\theta^2}{2} + \frac{\theta^4}{24}\right) + i\left(\theta - \frac{\theta^3}{6}\right)
$$
这个放大因子是 $\exp(i\theta)$ 的四阶泰勒展开。数值解在一个时间步内的相位变化为 $\varphi_{\text{num}} = \arg(G(\theta))$，而精确解的相位变化为 $\theta$。因此，时间积分引入的相位误差为：
$$
\delta\varphi(\theta) = \varphi_{\text{num}} - \theta = \arctan\left(\frac{\theta - \frac{\theta^3}{6}}{1 - \frac{\theta^2}{2} + \frac{\theta^4}{24}}\right) - \theta
$$
对于小的 $\theta$，这个误差约为 $\mathcal{O}(\theta^5)$，反映了RK4方法的四阶精度。

#### 时空误差的平衡与优化

有趣的是，空间离散引入的色散误差和时间离散引入的色散误差并不总是相互叠加。在特定条件下，它们可以相互抵消，从而显著提高计算的总体精度。

考虑一个由DRP空间格式和时间积分器构成的全离散系统 [@problem_id:4120617]。假设空间格式的无量纲修正波数有如下形式的色散误差：
$$
\kappa^*(\theta) = \theta + \beta_3 \theta^3 + \mathcal{O}(\theta^5) \quad (\text{其中 } \theta=k\Delta x)
$$
其中 $\beta_3$ 是由空间差分格式决定的常数。半离散系统的频率为 $\omega_s = c k^* = (c/\Delta x)\kappa^*$。
现在，我们使用一个二阶Runge-Kutta方法（其放大因子为 $G(z) = 1+z+z^2/2$）来进行时间积分。令 $z = -i \omega_s \Delta t = -i(c\Delta t/\Delta x)\kappa^* = -i\nu\kappa^*$，其中 $\nu$ 是CFL数。

全离散系统的数值频率 $\omega_{\text{num}}$ 由 $\exp(-i\omega_{\text{num}}\Delta t) = G(-i\nu\kappa^*)$ 确定。经过对数展开和代数运算，可以得到全离散系统的单步总相位与精确相位的误差 $\Delta\phi$ 的主导项：
$$
\Delta\phi = \omega_{\text{num}}\Delta t - \omega_{\text{exact}}\Delta t \approx \left(\nu\beta_3 + \frac{1}{6}\nu^3\right)\theta^3
$$
这个表达式揭示了惊人的结果：总相位误差的主导项由两部分组成，一部分 $\nu\beta_3\theta^3$ 来自空间色散，另一部分 $\frac{1}{6}\nu^3\theta^3$ 来自时间积分器的色散。通常，对于中心差分格式，$\beta_3  0$，而时间积分器的误差项为正。这意味着我们可以通过选择一个特定的CFL数 $\nu$ 来使这两项相互抵消。令括号内项为零：
$$
\nu\beta_3 + \frac{1}{6}\nu^3 = 0 \quad \implies \quad \nu^2 = -6\beta_3
$$
这给出了**最优CFL数** $\nu_{\text{opt}} = \sqrt{-6\beta_3}$。在此CFL数下，$\mathcal{O}(\theta^3)$ 阶的总相位误差被完全消除，使得格式的有效精度得到显著提升。这一时空误差抵消的原理是DRP方法在实际应用中取得成功的关键技术之一，它强调了将空间和时间离散化视为一个整体系统进行分析和优化的重要性。