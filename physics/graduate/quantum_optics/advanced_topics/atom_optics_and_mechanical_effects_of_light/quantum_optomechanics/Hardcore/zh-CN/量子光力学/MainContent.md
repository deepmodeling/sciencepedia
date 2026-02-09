## 引言
量子光力学是研究光（光子）与宏观或微观机械运动（声子）之间相互作用的前沿领域，它在量子物理与经典力学的交界处架起了一座桥梁。通过利用辐射压力，科学家们不仅能够以前所未有的精度探测和控制机械振子的运动，甚至能将其冷却至量子基态，从而揭示宏观物体的量子行为。这一领域的发展不仅深化了我们对量子测量和光与物质相互作用的理解，也催生了在传感、信息处理和基础物理测试等方面的革命性应用。本文旨在为读者提供一个关于量子光力学的系统性概述，解决从基本原理到前沿应用的核心问题。

在接下来的内容中，我们将分三步深入探索这个迷人的领域。首先，在“**原理与机制**”一章中，我们将建立光力相互作用的理论基础，从核心的哈密顿量出发，详细阐释线性化增强耦合、动态反作用冷却、测量的量子极限以及强耦合现象等关键概念。随后，在“**应用与交叉学科联系**”一章，我们将展示这些基本原理如何转化为强大的技术，探讨其在机械运动量子控制、超精密传感、构建混合量子系统和探索基础物理学等方面的广泛应用。最后，“**动手实践**”部分将提供一系列精心设计的问题，帮助读者巩固对光学冷却和量子极限等核心机制的理解，将理论知识转化为解决实际问题的能力。

## 原理与机制

本章旨在阐述量子光力学系统的核心物理原理与关键动力学机制。我们将从描述光与机械运动之间基本相互作用的哈密顿量出发，逐步深入探讨线性化理论、动态反作用效应（如光学冷却）、测量的量子极限以及强耦合现象。这些内容共同构成了理解和设计光力系统的理论基石。

### 光力相互作用哈密顿量

量子光力学的核心是一种参数化耦合：机械振子的位移 $x$ 改变了光学谐振腔（简称光腔）的某个参数，通常是其共振频率 $\omega_c$。反过来，腔内光场通过辐射压力对机械振子施加作用力，从而影响其运动。这种相互作用最典型的物理实现是法布里-珀罗（Fabry-Pérot）光腔，其一端反射镜被安装在一个机械振子上。

当这面反射镜移动时，光腔的有效长度发生变化，进而导致其共振频率漂移。腔频对机械位移的依赖性可以通过**频率牵引参数 (frequency-pull parameter)** $G$ 来量化，其定义为：
$$
G = \frac{\partial \omega_c}{\partial x}
$$
这个参数描述了单位机械位移引起的腔共振角频率的变化量。在许多标准模型中，例如一个长度为 $L$ 的法布里-珀罗腔，其中一面镜子可以移动，其共振频率为 $\omega_c(x) = q \frac{\pi c}{L+x}$（其中 $q$ 为整数，$c$ 为光速）。在平衡位置 $x=0$ 附近，频率牵引参数近似为 $G = -\frac{\omega_c(0)}{L}$。

为了更具体地理解该参数的推导，我们可以考虑一个稍微复杂的配置，如一个由三面反射镜 M1, M2, M3 构成的三角形成环形腔 [@problem_id:721429]。假设 M1 和 M2 固定，而 M3 可沿 y 轴移动，其位移为 $x$。腔的总光程长度 $L_{\text{opt}}(x)$ 决定了共振频率 $\omega_c(x) = \frac{2\pi q c}{L_{\text{opt}}(x)}$。通过计算光程长度对位移 $x$ 的导数，我们可以得到频率牵引参数。例如，在 [@problem_id:721429] 所描述的几何结构中，总光程长度为 $L_{\text{opt}}(x) = 2na + 2\sqrt{a^2+(h+x)^2}$，其中 $a$ 和 $h$ 是几何参数，$n$ 是部分光路中的折射率。在平衡点 $x=0$ 处对 $\omega_c(x)$ 求导，得到：
$$
G = \frac{\partial \omega_c}{\partial x}\bigg|_{x=0} = -\frac{\omega_c}{L_{\text{opt}}} \frac{\partial L_{\text{opt}}}{\partial x}\bigg|_{x=0} = -\frac{\omega_{c,0}}{2(na + \sqrt{a^2+h^2})} \frac{2h}{\sqrt{a^2+h^2}}
$$
其中 $\omega_{c,0}$ 是平衡位置的共振频率。这个例子表明，$G$ 的具体形式取决于系统的几何构造，但其物理意义是普适的。

为了建立完整的量子理论，我们需要对光学和机械自由度进行量子化。光腔模式由湮灭和产生算符 $\hat{a}$ 和 $\hat{a}^\dagger$ 描述，机械振子则由 $\hat{b}$ 和 $\hat{b}^\dagger$ 描述。机械位移算符可表示为 $\hat{x} = x_{\text{zpf}}(\hat{b} + \hat{b}^\dagger)$，其中 $x_{\text{zpf}} = \sqrt{\hbar/(2m\omega_m)}$ 是机械振子在其基态下的零点涨落幅值，$m$ 和 $\omega_m$ 分别是其有效质量和本征频率。

光腔的哈密顿量包含腔模自身的能量项和与机械位移相关的项。在小位移近似下，我们可以将腔频 $\omega_c(\hat{x})$ 在平衡位置附近做泰勒展开：$\omega_c(\hat{x}) \approx \omega_c(0) + \frac{\partial \omega_c}{\partial x}\big|_{x=0} \hat{x}$。系统的哈密顿量中与相互作用相关的部分为 $\hbar \omega_c(\hat{x}) \hat{a}^\dagger\hat{a}$。忽略常数能量项后，我们得到核心的**辐射压相互作用 (radiation pressure interaction)** 哈密顿量：
$$
\hat{H}_{\text{int}} = \hbar \left(\frac{\partial \omega_c}{\partial x}\right) \hat{x} \hat{a}^\dagger\hat{a} = \hbar G x_{\text{zpf}} (\hat{b} + \hat{b}^\dagger) \hat{a}^\dagger\hat{a}
$$
我们通常定义**单光子耦合率 (single-photon coupling rate)** $g_0 = G x_{\text{zpf}}$，这是一个描述单个光子与单个声子之间相互作用强度的基本参数。于是，哈密顿量可写为一种更为简洁和常见的形式：
$$
\hat{H}_{\text{int}} = \hbar g_0 (\hat{b} + \hat{b}^\dagger) \hat{a}^\dagger\hat{a}
$$
这个哈密顿量描述了腔内光子数算符 $\hat{n} = \hat{a}^\dagger\hat{a}$ 与机械位移 $\hat{x}$ 之间的耦合。从物理上看，它代表了腔内光子数对机械振子施加的辐射压力 $F = -\frac{\partial}{\partial x} (\hbar \omega_c(x) \hat{n}) = -\hbar G \hat{n}$。

### 线性化与增强耦合

在大多数实验系统中，单光子耦合率 $g_0$ 非常小，通常远小于光腔的衰减率 $\kappa$ 和机械振子的阻尼率 $\gamma_m$。在这种情况下，单个光子和声子之间的相互作用极其微弱，难以观测到显著的量子效应。

为了克服这一困难，一个关键的技术是使用一束强的相干激光场来驱动光腔。强驱动在腔内建立一个经典的大振幅相干场，其量子涨落可以被视为微扰。我们可以将腔场算符分解为一个大的经典振幅 $\alpha_s$ 和一个小的量子涨落算符 $\delta\hat{a}$ 的和：$\hat{a} = \alpha_s + \delta\hat{a}$。这里，$\alpha_s$ 是稳态时的平均场幅，通常可以视为一个复数。

将此表达式代入相互作用哈密顿量 $\hat{H}_{\text{int}} = \hbar g_0 (\hat{b} + \hat{b}^\dagger)(\alpha_s^* + \delta\hat{a}^\dagger)(\alpha_s + \delta\hat{a})$，并展开，我们可以得到几项：
1.  一个与算符无关的经典能量项 $\hbar g_0 |\alpha_s|^2 (\hat{b} + \hat{b}^\dagger)$，它描述了平均光强引起的静态力，导致机械振子平衡位置的偏移。
2.  一个描述光子数涨落 $\delta\hat{a}^\dagger\delta\hat{a}$ 与机械运动耦合的项 $\hbar g_0 (\hat{b} + \hat{b}^\dagger)\delta\hat{a}^\dagger\delta\hat{a}$，这通常是高阶小量，在 **线性化 (linearization)** 近似下被忽略。
3.  最关键的一项是线性的、同时涉及光学和机械涨落的项：
    $$
    \hat{H}_{\text{lin}} \approx \hbar g_0 (\hat{b} + \hat{b}^\dagger) (\alpha_s^* \delta\hat{a} + \alpha_s \delta\hat{a}^\dagger)
    $$
这个线性化的哈密顿量描述了量子涨落之间的相互作用。通过定义一个**多光子（或增强）光力耦合率 (many-photon optomechanical coupling rate)** $G = g_0 |\alpha_s|$，并假设 $\alpha_s$ 为实数（可以通过选择驱动激光的相位来实现），哈密顿量可以写为：
$$
\hat{H}_{\text{lin}} \approx \hbar G (\hat{b} + \hat{b}^\dagger) (\delta\hat{a} + \delta\hat{a}^\dagger)
$$
重要的是，$G$ 与驱动场的振幅 $|\alpha_s|$ 成正比，而 $|\alpha_s|^2$ 是腔内平均光子数。通过增加驱动激光的功率，我们可以使 $G$ 变得非常大，甚至超过系统的耗散率，从而进入能够展现丰富量子现象的参数区域。这种通过强驱动来增强有效耦合强度的思想是光力学研究的核心策略之一。

值得注意的是，线性化方法具有广泛的适用性。任何依赖于机械位置的相互作用，在强驱动场存在的情况下，通常都可以被线性化以产生有效的光力耦合。例如，在一个包含非线性晶体的特殊系统中，其参量下转换（PDC）效率 $\Lambda$ 依赖于机械位置 $\hat{x}$，即 $\Lambda(\hat{x})$ [@problem_id:690006]。其相互作用哈密顿量具有 $\hat{H}_{int} = \hbar \Lambda(\hat{x}) (\hat{a} \hat{c}^{\dagger 2} + \hat{a}^\dagger \hat{c}^2)$ 的形式，其中 $\hat{a}$ 是强驱动的泵浦模，$\hat{c}$ 是产生的信号模。将耦合常数线性展开为 $\Lambda(\hat{x}) \approx \Lambda_0 + \Lambda' \hat{x}$，并将泵浦模替换为经典振幅 $\alpha_s$，我们就能得到一个有效的三波混频相互作用 $\hat{H}_{\text{eff}} \propto \hbar \Lambda' x_{\text{zpf}} \alpha_s (\hat{b}+\hat{b}^\dagger)((\delta\hat{c}^\dagger)^2 + (\delta\hat{c})^2)$。这展示了线性化作为一个通用工具，能够将不同物理来源的参数耦合转化为可操控的、形式相似的有效相互作用。

### 半经典动力学与非线性效应

在深入探讨量子涨落之前，我们先考察系统的平均场（半经典）动力学。平均腔场振幅 $\alpha_s = \langle \hat{a} \rangle$ 和平均机械振子振幅 $\beta_s = \langle \hat{b} \rangle$ 的稳态行为由一组耦合的代数方程决定。在一个以激光频率 $\omega_L$ 旋转的参考系中，这些方程为 [@problem_id:721623]：
$$
(i\Delta_0 + \frac{\kappa}{2})\alpha_s - i g_0 \alpha_s (\beta_s + \beta_s^*) = E
$$
$$
(i\omega_m + \frac{\gamma_m}{2})\beta_s = i g_0 |\alpha_s|^2
$$
其中 $\Delta_0 = \omega_{c,0} - \omega_L$ 是激光相对于原始腔频的失谐，$\kappa$ 和 $\gamma_m$ 分别是光腔和机械的能量衰减率，$E$ 是驱动场幅度。

第一式描述了腔场，其中 $g_0(\beta_s+\beta_s^*) = G_0 x_s / x_{zpf}$ 项代表了由机械静态位移 $x_s$ 引起的腔频移动。第二式表明，稳态的机械振幅 $\beta_s$ 是由平均辐射压力 $F_{rp} = \hbar g_0 |\alpha_s|^2$ 驱动产生的。在高品质因子极限下（$\omega_m \gg \gamma_m$），机械振子的响应近似为纯实数位移，$\Re(\beta_s) \approx g_0|\alpha_s|^2 / \omega_m$。

将机械位移的解代回腔场方程，我们会发现一个关键的非线性反馈机制。机械位移 $x_s$ 自身正比于腔内光子数 $n_s = |\alpha_s|^2$，而这个位移又会改变腔的有效失谐 $\Delta' = \Delta_0 - 2g_0\Re(\beta_s) = \Delta_0 - \frac{2g_0^2}{\omega_m} n_s$。最终，腔内光子数 $n_s$ 满足一个自洽方程：
$$
n_s = |\alpha_s|^2 = \frac{|E|^2}{(\kappa/2)^2 + \Delta'(n_s)^2} = \frac{|E|^2}{(\kappa/2)^2 + (\Delta_0 - \frac{2g_0^2}{\omega_m}n_s)^2}
$$
这是一个关于 $n_s$ 的三次方程，表明对于给定的输入功率 $|E|^2$，可能存在一个或三个实数解。当存在三个解时，中间的解不稳定，系统表现出**光学双稳性 (optical bistability)**。此时，腔内光子数 $n_s$ 作为输入功率 $|E|^2$ 的函数曲线会呈现一个 "S" 形。

双稳区域的边界由曲线的拐点确定，在这些点上导数 $d|E|^2/dn_s = 0$。通过求解这个条件，我们可以找到发生双稳的临界光子数。例如，在 [@problem_id:721623] 的特定条件下（$\Delta_0 > \frac{\sqrt{3}}{2}\kappa$），较低光子数处的拐点对应的光子数为：
$$
n_s^{(\text{lower})} = \frac{\omega_m}{6g_0^2}\left(2\Delta_0-\sqrt{\Delta_0^2-\frac{3\kappa^2}{4}}\right)
$$
这种非线性行为是光力系统一个标志性的经典特征，它源于辐射压力对光腔频率的静态反作用。

### 动态反作用：光学阻尼与冷却

除了上述静态的反作用效应，光力相互作用还能产生更为有趣的动态效应。由于光腔具有有限的响应时间（由衰减率 $\kappa$ 决定，响应时间约为 $1/\kappa$），腔内光场的变化会滞后于引起它的机械运动。这种延迟导致辐射压力与机械振子速度之间出现一个分量，从而对机械振子做功或从其吸收能量。这种效应被称为**动态反作用 (dynamical backaction)**。

当这个力与速度方向相反时，它表现为一种有效的黏滞阻尼，从机械振子中提取能量，该现象称为**光学阻尼 (optical damping)**。反之，若力的方向与速度相同，则会注入能量，导致运动被放大，称为光学反阻尼或放大。

我们可以通过计算系统的力学感受率 $\chi_F(\omega)$ 来定量分析这一效应，它描述了对频率为 $\omega$ 的微小机械位移 $x(\omega)$ 的力响应 $\delta F(\omega)$。光学阻尼系数 $\gamma_{\text{opt}}$ 正比于感受率虚部的低频极限，即 $\gamma_{\text{opt}} \propto \lim_{\omega \to 0} \text{Im}[\chi_F(\omega)]/\omega$ [@problem_id:1140336]。详细计算表明，$\gamma_{\text{opt}}$ 的符号和大小严重依赖于激光失谐 $\Delta_0$。
- 当激光频率低于腔共振频率（**红失谐 (red detuning)**, $\Delta_0 > 0$）时，$\gamma_{\text{opt}} > 0$，光场对机械运动起到冷却作用。
- 当激光频率高于腔共振频率（**蓝失谐 (blue detuning)**, $\Delta_0  0$）时，$\gamma_{\text{opt}}  0$，光场会放大机械运动，可能导致自激振荡。

这个现象可以用更直观的量子散射图像来理解。在线性化哈密顿量 $\hat{H}_{\text{lin}}$ 的框架下，光与机械的相互作用可以看作是声子和光子之间的散射过程。
- **斯托克斯散射 (Stokes scattering)**（加热过程）：一个驱动光子被湮灭，同时产生一个能量较低的出射光子和一个声子。能量关系为 $\hbar\omega_{\text{photon,out}} = \hbar\omega_L - \hbar\omega_m$。
- **反斯托克斯散射 (Anti-Stokes scattering)**（冷却过程）：一个驱动光子和一个声子被湮灭，同时产生一个能量较高的出射光子。能量关系为 $\hbar\omega_{\text{photon,out}} = \hbar\omega_L + \hbar\omega_m$。

为了使这些过程发生，出射光子必须能够进入光腔的共振模式。因此，通过调节激光频率 $\omega_L$（即失谐 $\Delta = \omega_c - \omega_L$），我们可以选择性地增强某一个过程。

**边带冷却 (Sideband cooling)** 的原理就是利用这一点。当我们将激光器调谐到腔的“红色边带”，即 $\Delta \approx \omega_m$ 时，反斯托克斯过程（冷却）得到共振增强，因为出射光子频率 $\omega_L + \omega_m$ 正好与腔频 $\omega_c$ 匹配。同时，斯托克斯过程（加热）被抑制，因为它要求出射光子频率为 $\omega_L - \omega_m$，这远离了腔的共振峰。

由光力相互作用引起的总的机械阻尼率 $\Gamma_{\text{opt}}$ 可以表示为反斯托克斯散射率 $\Gamma_-$ 与斯托克斯散射率 $\Gamma_+$ 之差。这些速率由系统的洛伦兹谱密度决定 [@problem_id:721507]：
$$
\Gamma_{\text{opt}}(\Delta') = \Gamma_- - \Gamma_+ = \frac{G^2\kappa}{2} \left[ \frac{1}{(\Delta'-\omega_m)^2+(\kappa/2)^2} - \frac{1}{(\Delta'+\omega_m)^2+(\kappa/2)^2} \right]
$$
这里 $\Delta'$ 是考虑了静态频移后的有效失谐。为达到最大冷却速率，我们将有效失谐精确设定在 $\Delta'=\omega_m$。在这种最优条件下，冷却速率为 [@problem_id:721507]：
$$
\Gamma_{\text{opt}}(\omega_m) = \frac{32 G^2 \omega_m^2}{\kappa(16\omega_m^2 + \kappa^2)}
$$
在**边带分辨 (resolved-sideband)** 极限下（$\omega_m \gg \kappa$），冷却速率近似为 $\Gamma_{\text{opt}} \approx 4G^2/\kappa$。

机械振子的最终平均声子数 $\langle n \rangle_{ss}$ 由一个详细的平衡方程决定，它考虑了光学冷却（速率 $\Gamma_-$）、光学加热（速率 $\Gamma_+$）以及与温度为 $T$（对应热声子数 $n_{th}$）的环境之间的热交换（速率 $\gamma_m$）[@problem_id:721446]。稳态时，声子数的演化方程 $\frac{d\langle n \rangle}{dt} = -(\Gamma_{\text{opt}} + \gamma_m)\langle n \rangle + (\Gamma_+ + \gamma_m n_{th})$ 为零，得到：
$$
\langle n \rangle_{ss} = \frac{\Gamma_+ + \gamma_m n_{th}}{\Gamma_- - \Gamma_+ + \gamma_m}
$$
这个表达式清晰地表明，最终的声子数是加热过程（光学加热和热浴注入）与总的冷却速率（净光学冷却和本征阻尼）之间竞争的结果。在边带分辨且强驱动的条件下（$\Gamma_{\text{opt}} \gg \gamma_m$），最终的声子数可以远低于环境的热声子数，甚至可以达到量子基态 $\langle n \rangle_{ss} \ll 1$。

### 测量的量子极限

除了操控机械运动状态，光力系统也是进行超精密测量的理想平台。其基本思想是，一个作用在机械振子上的微弱外部力 $F_{ext}$ 会引起其位置的微小变化 $x$，这个变化通过光力耦合 $\Delta\omega_c = G x$ 转化为腔频的移动，并最终调制从腔中透射或反射的光场。通过对输出光进行高精度测量，我们就可以推断出 $x$，进而反推出 $F_{ext}$。

然而，这种测量的灵敏度受到量子力学基本原理的限制。在连续测量一个可观测量（如位置）时，存在两种不可避免的量子噪声源：
1.  **测量不精确度噪声 (Measurement Imprecision Noise)**：在光力学中，这通常对应于探测光的**散粒噪声 (shot noise)**。由于光是由离散的光子组成的，探测光束本身携带的量子涨落使得我们对输出光场相位的测量存在一个基本的不确定性。这转化为对机械位置推断的不精确度，其频谱密度记为 $S_{xx}^{\text{imp}}$。
2.  **量子反作用噪声 (Quantum Back-Action Noise)**：根据海森堡不确定性原理，测量行为本身必然会对被测系统产生扰动。在光力学中，这种扰动来自腔内光子数涨落引起的随机**辐射压力 (radiation pressure)**。即使是真空涨落，也会在腔内产生光子数的随机生灭，从而对机械振子施加一个随机力，这就是量子反作用力。其频谱密度记为 $S_{FF}^{\text{BA}}$。

这两种噪声之间存在一种深刻的权衡关系。增加探测光的功率（即增加腔内平均光子数 $\bar{n}_{cav}$）可以获得更多的信息，从而降低测量不精确度噪声（$S_{xx}^{\text{imp}} \propto 1/\bar{n}_{cav}$）。然而，更多的光子也意味着更大的光子数涨落，从而增强了量子反作用力噪声（$S_{FF}^{\text{BA}} \propto \bar{n}_{cav}$）。

对于一个理想的量子测量，这两种噪声的谱密度受到一个不确定性关系的约束 [@problem_id:721451]：
$$
S_{xx}^{\text{imp}}(\omega) S_{FF}^{\text{BA}}(\omega) \ge \left(\frac{\hbar}{2}\right)^2
$$
反作用力的存在会对被测物体产生实际的物理效应。例如，一个连续测量的白噪声反作用力会持续地对一个自由粒子做功，使其动能随时间线性增加，这个过程被称为**反作用加热 (back-action heating)**。其加热率可以通过反作用力谱密度计算得到 [@problem_id:721451]。

在力传感应用中，总噪声谱密度为不精确度噪声和反作用噪声之和：$S_{FF}^{\text{total}} = S_{FF}^{\text{BA}} + S_{FF}^{\text{imp}}$，其中 $S_{FF}^{\text{imp}} = S_{xx}^{\text{imp}} / |\chi_m(\Omega)|^2$ 是折算到输入的力噪声，$\chi_m(\Omega)$ 是机械振子在测量频率 $\Omega$ 处的力学易感性。通过调节激光功率（即 $\bar{n}_{cav}$），可以找到一个最优值，使得总噪声达到最小值。当两种噪声贡献相等时，系统达到其最佳灵敏度，该灵敏度被称为**标准量子极限 (Standard Quantum Limit, SQL)**。对于一个在共振频率 $\Omega_m$ 处测量的机械谐振子，总的等效输入力噪声谱密度的最小值为：
$$
S_{FF}^{\text{SQL}}(\Omega_m) = 2 \hbar m \Omega_m \Gamma_m
$$
这个表达式（单位为 $N^2/Hz$）代表了在给定系统参数下，利用标准的连续位置测量方案能够探测到的最微弱力的理论极限。它仅由普朗克常数和机械振子自身的属性（质量、频率、阻尼率）决定。超越 SQL 需要更高级的技术，例如利用压缩态光、进行变分测量或量子非破坏性测量。

### 强耦合与简正模劈裂

前面讨论的大部分现象都可以在所谓的弱耦合区域（$G  \kappa, \gamma_m$）观察到。然而，当光力相互作用足够强，以至于相干能量交换的速率 $G$ 超过了光学和机械模式的耗散速率时，系统将进入一个全新的**强耦合区域 (strong coupling regime)**。

在这种情况下，光子和声子不再是独立的准粒子，它们会发生相干的能量振荡，形成新的混合的准粒子，称为**光力学极化子 (optomechanical polaritons)**。这种现象的哈密顿量描述通常是在一个旋转参考系中，并采用**旋转波近似 (Rotating-Wave Approximation, RWA)**，只保留能量近乎守恒的相互作用项。例如，当驱动激光调谐到红色边带附近时，线性化的哈密顿量简化为 [@problem_id:721557]：
$$
\hat{H}_{\text{RWA}} = \hbar \Delta' \hat{a}^\dagger \hat{a} + \hbar\omega_m \hat{b}^\dagger \hat{b} - \hbar G (\hat{a}^\dagger \hat{b} + \hat{a} \hat{b}^\dagger)
$$
这里的 $\hat{a}$ 和 $\hat{b}$ 都是涨落算符。这个哈密顿量在形式上与两个耦合的谐振子（例如两个耦合的弹簧振子）完全相同。

为了找到系统的新本征模式（即简正模），我们需要对哈密顿量进行对角化。我们可以将哈密顿量写成矩阵形式：
$$
\hat{H} = \hbar \begin{pmatrix} \hat{a}^\dagger  \hat{b}^\dagger \end{pmatrix} \begin{pmatrix} \Delta'  -G \\ -G  \omega_m \end{pmatrix} \begin{pmatrix} \hat{a} \\ \hat{b} \end{pmatrix}
$$
新的简正模频率 $\Omega_{\pm}$ 就是中心 $2\times2$ 矩阵的本征值。求解本征值方程 $\det(M - \lambda I) = 0$ 得到：
$$
\Omega_{\pm} = \frac{\Delta' + \omega_m}{2} \pm \frac{1}{2}\sqrt{(\Delta' - \omega_m)^2 + 4G^2}
$$
当光子和声子发生共振时（$\Delta' = \omega_m$），两个未耦合的模式会发生能级交叉。但由于耦合项 $G$ 的存在，能级发生排斥，形成一个**避免交叉 (avoided crossing)**。两个新的简正模频率变为 $\Omega_{\pm} = \omega_m \pm G$。

这种能级结构的变化在实验上可以通过探测系统的透射谱来观察。当一个微弱的探测光束扫描过系统时，它会在两个简正模频率 $\Omega_{\pm}$ 处分别看到一个透射峰（或吸收谷），而不是在原始的腔频处看到单个峰。这两个峰之间的频率差为：
$$
\Omega_+ - \Omega_- = \sqrt{(\Delta' - \omega_m)^2 + 4G^2}
$$
在共振时，这个劈裂的宽度直接就是 $2G$。这种现象被称为**简正模劈裂 (Normal-Mode Splitting, NMS)**，它是光力系统进入强耦合区域的明确标志，证明了光子和声子之间可以进行快速、相干的能量交换。