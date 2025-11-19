## 引言
[恒星光谱](@entry_id:143165)，即恒星发出的光按波长分解后的记录，是天文学家了解遥远天体最主要、有时也是唯一的信息来源。这束穿越了数光年时空的光线，如同一封宇宙信使，其复杂的[谱线](@entry_id:193408)结构中编码了恒星的温度、[化学成分](@entry_id:138867)、运动状态乃至其周围[行星环](@entry_id:199584)境的秘密。然而，从观测到的[光谱](@entry_id:185632)曲线到具体的物理量之间存在一道鸿沟。要破解这些宇宙密码，我们必须掌握一套坚实的物理理论和分析方法。

本文旨在系统性地架起这座桥梁。我们将从最基本的物理定律出发，逐步揭示如何将[光谱](@entry_id:185632)数据转化为对宇宙天体的深刻洞见。在“原理与机制”一章中，我们将深入探讨辐射如何在[恒星大气](@entry_id:152088)中传播，以及[谱线](@entry_id:193408)是如何形成的，为后续分析奠定理论基石。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些原理在实际研究中的强大威力，从测量恒星[磁场](@entry_id:153296)、探测[系外行星大气](@entry_id:161942)，到[检验广义相对论](@entry_id:157504)，探索其在多个前沿领域的应用。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者巩固所学知识，并将理论应用于解决实际问题。让我们从构建[恒星光谱](@entry_id:143165)分析的物理基础开始，踏上这段解读宇宙信息的旅程。

## 原理与机制

本章深入探讨分析[恒星光谱](@entry_id:143165)所需的基本物理原理和核心机制。我们将从[辐射转移](@entry_id:151695)的基本方程出发，建立一个描述辐射如何在[恒星大气](@entry_id:152088)中传播的数学框架。随后，我们将探索用于简化该框架的强大近似方法，并研究决定[恒星大气](@entry_id:152088)温度结构的关键因素。最后，我们将这些原理应用于光[谱线形成](@entry_id:160292)理论，解释[谱线](@entry_id:193408)的轮廓、强度以及它们如何揭示恒星的物理条件。

### [辐射转移方程](@entry_id:160254)及其形式解

理解[恒星光谱](@entry_id:143165)的关键在于描述[辐射与物质的相互作用](@entry_id:172771)。这一过程由**[辐射转移方程](@entry_id:160254)（equation of radiative transfer）**所描述。在一个假定为平面平行（plane-parallel）的大气层中，方程可以写为：

$$
\mu \frac{dI_\nu}{d\tau_\nu} = I_\nu - S_\nu
$$

此处，$I_\nu(\tau_\nu, \mu)$ 是**比强度（specific intensity）**，表示在频率 $\nu$、沿与[法线](@entry_id:167651)方向夹角为 $\theta$ 的方向上传播的辐射能量。参数 $\mu = \cos\theta$ 是[方向余弦](@entry_id:170591)，$\tau_\nu$ 是在该频率下的**光学深度（optical depth）**，它是一个无量纲的量，描述了从大气层顶部到某一深度的透明度。$S_\nu$ 是**[源函数](@entry_id:161358)（source function）**，它描述了物质在单位[光学深度](@entry_id:150612)路径上向[辐射场](@entry_id:164265)中增加的能量。

这个[一阶线性微分方程](@entry_id:164869)可以被 formally 求解。对于一个从 $\tau_\nu=0$（表面）延伸到无穷深处的半无限（semi-infinite）大气，并且表面没有外部入射辐射，其**形式解（formal solution）**将出射辐射（$\mu > 0$）和入射辐射（$\mu  0$）分开处理。在任意深度 $\tau_\nu$，比强度为：

*   对于出射辐射（$\mu > 0$）：
    $$ I_\nu(\tau_\nu, \mu) = \int_{\tau_\nu}^{\infty} S_\nu(t_\nu) e^{-(t_\nu - \tau_\nu)/\mu} \frac{dt_\nu}{\mu} $$
*   对于入射辐射（$\mu  0$）：
    $$ I_\nu(\tau_\nu, \mu) = \int_0^{\tau_\nu} S_\nu(t_\nu) e^{-(\tau_\nu - t_\nu)/|\mu|} \frac{dt_\nu}{|\mu|} $$

其中 $t_\nu$ 是积分的哑变量。这个解具有深刻的物理意义：在特定方向上观测到的强度是沿该视线路径上所有点[源函数](@entry_id:161358) $S_\nu$ 的贡献之和，每一贡献都因其到观测者的光学距离而被指数衰减（即因子 $e^{-\Delta\tau_\nu/\mu}$）。

我们最常关心的是从恒星表面（$\tau_\nu = 0$）射出的辐射，因为这是我们能直接观测到的。此时，出射强度为：
$$
I_\nu(0, \mu) = \int_0^{\infty} S_\nu(t_\nu) e^{-t_\nu/\mu} \frac{dt_\nu}{\mu}
$$
这个积分表明，我们观测到的[恒星光谱](@entry_id:143165)是由[源函数](@entry_id:161358)在不同深度的加权平均决定的。权重函数 $e^{-t_\nu/\mu}/\mu$ 表明，我们主要看到的是光学深度约为 $\tau_\nu \approx \mu$ 的大气层。

### [辐射场的矩](@entry_id:160501)和[爱丁顿近似](@entry_id:161362)

为了从复杂的辐射场中提取宏观物理量，我们定义了比强度的**矩（moments）**。前三个矩在天体物理学中尤为重要：

*   **平均强度（Mean Intensity）**, $J_\nu$：
    $$J_\nu = \frac{1}{2} \int_{-1}^{1} I_\nu(\mu) d\mu$$
    它代表了在某一点上所有方向强度的平均值，与辐射场的能量密度成正比。

*   **天体物理学流量（Astrophysical Flux）**, $H_\nu$：
    $$H_\nu = \frac{1}{2} \int_{-1}^{1} I_\nu(\mu) \mu d\mu$$
    它正比于通过单位面积的净辐射能流率。在**[辐射平衡](@entry_id:158473)（radiative equilibrium）**状态下，没有能量源或能量汇，净流量不随深度变化，即 $\frac{dH_\nu}{d\tau_\nu} = 0$。

*   **K积分（K-integral）**, $K_\nu$：
    $$K_\nu = \frac{1}{2} \int_{-1}^{1} I_\nu(\mu) \mu^2 d\mu$$
    它与辐射压力张量的对角分量有关。

对[辐射转移方程](@entry_id:160254)关于 $\mu$ 取积分，可以得到矩之间的关系式。前两个[矩方程](@entry_id:149666)为：
$$
\frac{dH_\nu}{d\tau_\nu} = J_\nu - S_\nu
$$
$$
\frac{dK_\nu}{d\tau_\nu} = H_\nu
$$
在[辐射平衡](@entry_id:158473)下，$dH_\nu/d\tau_\nu = 0$，这立即导出 $J_\nu = S_\nu$。如果大气还处于**局部热[动平衡](@entry_id:163330)（Local Thermodynamic Equilibrium, LTE）**，[源函数](@entry_id:161358)等于[普朗克函数](@entry_id:159605) $B_\nu(T)$，那么 $J_\nu = B_\nu(T)$。

然而，这一系列[矩方程](@entry_id:149666)存在一个问题：每个方程都引入了一个更高阶的矩（例如，第一个方程有 $J_\nu$ 和 $H_\nu$，第二个有 $H_\nu$ 和 $K_\nu$），因此[方程组](@entry_id:193238)本身是不封闭的。为了求解，我们需要一个**闭合关系（closure relation）**来联系这些矩。

一个极为重要且广泛应用的闭合关系是**[爱丁顿近似](@entry_id:161362)（Eddington approximation）**。该近似假设[辐射场](@entry_id:164265)仅是弱各向异性的。为了推导它，我们可以假设比强度 $I_\nu(\mu)$ 是 $\mu$ 的一个简单线性函数，形如 $I_\nu(\mu) = a + b\mu$。将此形式代入 $J_\nu$ 和 $K_\nu$ 的定义中，我们进行积分：
$$
J_\nu = \frac{1}{2} \int_{-1}^{1} (a + b\mu) d\mu = \frac{1}{2} [a\mu + b\frac{\mu^2}{2}]_{-1}^{1} = a
$$
$$
K_\nu = \frac{1}{2} \int_{-1}^{1} (a + b\mu) \mu^2 d\mu = \frac{1}{2} \int_{-1}^{1} (a\mu^2 + b\mu^3) d\mu = \frac{1}{2} [a\frac{\mu^3}{3} + b\frac{\mu^4}{4}]_{-1}^{1} = \frac{a}{3}
$$
结合这两个结果，我们立即得到 $K_\nu = J_\nu/3$。这便是著名的[爱丁顿近似](@entry_id:161362) [@problem_id:189320]。这个简单的关系式使得[矩方程](@entry_id:149666)组得以封闭，从而极大地简化了[恒星大气](@entry_id:152088)模型的计算。

### [源函数](@entry_id:161358)与出射辐射

[源函数](@entry_id:161358) $S_\nu(\tau_\nu)$ 的[分布](@entry_id:182848)形态是决定[恒星光谱](@entry_id:143165)外观的[根本因](@entry_id:150749)素。一个非常有用的经验法则是**爱丁顿-巴比耶关系（Eddington-Barbier relation）**，它指出：
$$
I_\nu(0, \mu) \approx S_\nu(\tau_\nu = \mu)
$$
这个关系表明，在方向 $\mu$ 上看到的出射强度约等于光学深度为 $\tau_\nu = \mu$ 处的[源函数](@entry_id:161358)值。这个近似对于随[光学深度](@entry_id:150612)线性变化的[源函数](@entry_id:161358)是精确的。

我们可以通过一个具体的例子来检验该近似的准确性。考虑一个[源函数](@entry_id:161358)随深度[指数增长](@entry_id:141869)的模型：$S_\nu(\tau_\nu) = S_0 \exp(\alpha \tau_\nu)$，其中 $\alpha$ 是一个小的正常数。通过形式解，我们可以精确计算出射强度：
$$
I_\nu(0,\mu) = \frac{S_0}{\mu} \int_0^\infty e^{\alpha\tau_\nu} e^{-\tau_\nu/\mu} d\tau_\nu = \frac{S_0}{1-\alpha\mu}
$$
而爱丁顿-巴比耶近似给出 $I_{\nu, \text{EB}}(\mu) = S_\nu(\tau_\nu = \mu) = S_0 \exp(\alpha\mu)$。因此，精确解与近似解的比值，即修正因子，为：
$$
C(\alpha,\mu) = \frac{I_\nu(0,\mu)}{I_{\nu,\text{EB}}(\mu)} = \frac{e^{-\alpha\mu}}{1-\alpha\mu}
$$
当 $\alpha\mu \ll 1$ 时，[泰勒展开](@entry_id:145057) $e^{-\alpha\mu} \approx 1-\alpha\mu$ 和 $(1-\alpha\mu)^{-1} \approx 1+\alpha\mu$ 表明，该比值接近于1，验证了近似在[源函数](@entry_id:161358)变化缓慢时的有效性 [@problem_id:189195]。

将理论与观测联系起来，我们需要计算可观测的物理量，例如**天体物理学流量（Astrophysical Flux）** $F_\nu(0)$，它代表从恒星表面单位面积流出的净能流率。它通过对出射强度在半球上积分得到：
$$
F_\nu(0) = 2\pi \int_0^1 I_\nu(0, \mu) \mu \, d\mu
$$
通过为[源函数](@entry_id:161358) $S_\nu(\tau_\nu)$ 设定不同的物理模型，我们可以探索不同的大气条件如何塑造出射[光谱](@entry_id:185632)。
例如，考虑一个[非LTE](@entry_id:152428)模型，其中[源函数](@entry_id:161358)形如 $S_\nu(\tau_\nu) = S_0 \tau_\nu e^{-a \tau_\nu}$。这种形式可以代表一个被外部辐射激发的色球层，其[源函数](@entry_id:161358)在表面为零，在某一深度达到峰值然后衰减。通过将 $S_\nu$ 代入 $I_\nu(0, \mu)$ 的表达式，然后再积分计算 $F_\nu(0)$，可以得到出射流量的具体解析表达式，从而将大气内部的物理条件（由 $S_0$ 和 $a$ 表征）与外部观测到的流量联系起来 [@problem_id:189458]。

另一个例子是[源函数](@entry_id:161358)随深度指数衰减的模型，$S_\nu(\tau_\nu) = S_0 e^{-k\tau_\nu}$。在这种情况下，我们可以计算出射的平均强度 $J_\nu(0)$。由于表面没有入射辐射，$I_\nu(0, \mu  0) = 0$，因此 $J_\nu(0) = \frac{1}{2} \int_0^1 I_\nu(0,\mu)d\mu$。首先计算 $I_\nu(0,\mu)$：
$$
I_\nu(0,\mu) = \frac{S_0}{\mu}\int_{0}^{\infty}e^{-kt_\nu}e^{-t_\nu/\mu}dt_\nu = \frac{S_0}{1+k\mu}
$$
然后积分得到表面的平均强度：
$$
J_\nu(0) = \frac{1}{2}\int_{0}^{1}\frac{S_0}{1+k\mu}d\mu = \frac{S_0}{2k}\ln(1+k)
$$
这个结果展示了如何从给定的[源函数](@entry_id:161358)[分布](@entry_id:182848)精确地推导出[辐射场的矩](@entry_id:160501) [@problem_id:189460]。

### 温度结构与[不透明度](@entry_id:160442)

在LTE假设下，[源函数](@entry_id:161358) $S_\nu$ 由[普朗克函数](@entry_id:159605) $B_\nu(T)$ 决定，因此大气的温度结构 $T(\tau)$ 成为核心。对于一个简化的**灰色大气（grey atmosphere）**（即[不透明度](@entry_id:160442) $\kappa$ 与频率无关），我们可以利用[辐射平衡](@entry_id:158473)条件和[爱丁顿近似](@entry_id:161362)来推导温度[分布](@entry_id:182848)。

结合[矩方程](@entry_id:149666) $dK/d\tau = H$ 和[爱丁顿近似](@entry_id:161362) $K=J/3$，我们得到 $dJ/d\tau = 3H$。由于[辐射平衡](@entry_id:158473)，$H$ 是一个常数。积分上式得到 $J(\tau) = 3H\tau + C$，其中 $C$ 是积分常数。这个常数由表面边界条件决定。一种特定的边界条件是要求向内的平均强度为零，即 $J_{in}(0)=0$。若进一步假设强度是 $\mu$ 的线性函数 $I(\tau,\mu) = J(\tau) + 3H\mu$，此边界条件可推导出 $J(0) = \frac{3}{2}H$。因此，平均强度的[分布](@entry_id:182848)为：
$$
J(\tau)=3H\Bigl(\tau+\frac{1}{2}\Bigr)
$$
由于LTE和[辐射平衡](@entry_id:158473)（$S=J$），以及 $S=B(T)=\sigma T^4/\pi$ 和 $H=\sigma T_{\text{eff}}^4/(4\pi)$，我们可以得到温度结构：
$$
T(\tau)^4 = \frac{3}{4} T_{\text{eff}}^4\Bigl(\tau+\frac{1}{2}\Bigr)
$$
一个有趣的结果是，我们可以找到大气温度等于恒星[有效温度](@entry_id:161960) $T_{\text{eff}}$ 的深度 $\tau_0$。设置 $T(\tau_0) = T_{\text{eff}}$，我们解得 $\tau_0 = 4/3 - 1/2 = 5/6$ [@problem_id:189200]。

真实[恒星大气](@entry_id:152088)并非灰色。[不透明度](@entry_id:160442) $\kappa_\nu$ 随频率剧烈变化，尤其是在[谱线](@entry_id:193408)附近。为了处理非灰色问题，我们引入**平均[不透明度](@entry_id:160442)（mean opacities）**的概念。在描述大气深层[能量输运](@entry_id:183081)时，最重要的平均不透明度是**[罗斯兰平均不透明度](@entry_id:754422)（Rosseland mean opacity）**，$\kappa_R$。它的定义是一个谐波平均，并以[普朗克函数](@entry_id:159605)对温度的导数作为权重：
$$
\frac{1}{\kappa_R} = \frac{\int_0^\infty \frac{1}{\kappa_\nu} \frac{\partial B_\nu(T)}{\partial T} d\nu}{\int_0^\infty \frac{\partial B_\nu(T)}{\partial T} d\nu}
$$
这个定义使得在非灰色大气深处，温度结构可以近似地用灰色大气的公式描述，只需将[光学深度](@entry_id:150612) $\tau$ 替换为罗斯兰平均光学深度 $\tau_R$。

[谱线](@entry_id:193408)的存在（称为**[谱线覆盖效应](@entry_id:159607) line blanketing**）显著增加了某些频率的[不透明度](@entry_id:160442)，从而影响 $\kappa_R$ 和温度结构。我们可以用一个“篱笆（picket-fence）”模型来阐明这一点。假设[不透明度](@entry_id:160442)只有两个值：在频率区间的 $1-\eta$ 部分为连续谱不透明度 $\kappa_c$，在 $\eta$ 部分为线谱[不透明度](@entry_id:160442) $\kappa_L = (1+\beta)\kappa_c$。该模型的[罗斯兰平均不透明度](@entry_id:754422)为：
$$
\frac{\kappa_R}{\kappa_c} = \frac{1+\beta}{1+\beta(1-\eta)}
$$
由于[谱线](@entry_id:193408)的存在（$\eta>0, \beta>0$），$\kappa_R$ 总是小于 $\kappa_c$。这意味着在相同的几何深度上，罗斯兰[光学深度](@entry_id:150612) $\tau_R$ 小于[连续谱](@entry_id:155477)[光学深度](@entry_id:150612) $\tau_c$。因此，在给定的连续谱[光学深度](@entry_id:150612) $\tau_c$ 处，有[谱线](@entry_id:193408)覆盖的大气温度 $T_b(\tau_c)$ 会高于没有[谱线](@entry_id:193408)的灰色大气温度 $T_g(\tau_c)$。这种效应被称为**背温效应（backwarming）**。在连续谱的光球层（定义为 $\tau_c = 2/3$），温度的四次方之比为：
$$
\left( \frac{T_b}{T_g} \right)^4_{\tau_c=2/3} = \frac{1}{2}\Bigl(1+\frac{1+\beta}{1+\beta(1-\eta)}\Bigr)
$$
这个比值总是大于1，量化了[谱线](@entry_id:193408)覆盖对大气加热的效应 [@problem_id:189232]。

在更高级的模型中，[不透明度](@entry_id:160442)本身可以被视为一个[随机变量](@entry_id:195330)。例如，如果我们将 $\kappa_\nu$ 在任何频率处都看作是从一个与频率无关的伽马[分布](@entry_id:182848) $P(\kappa; k, \theta)$ 中抽取的样本，那么[罗斯兰平均不透明度](@entry_id:754422)就对应于 $1/\kappa$ 的[期望值](@entry_id:153208)的倒数。对于伽马[分布](@entry_id:182848)，在 $k>1$ 的条件下，可以计算出：
$$
\frac{1}{\kappa_R} = \mathbb{E}\biggl[\frac{1}{\kappa}\biggr] = \frac{1}{(k-1)\,\theta}
$$
因此，有效的[罗斯兰平均不透明度](@entry_id:754422)就是 $\kappa_R = (k-1)\theta$。这个 elegant 的结果将宏观的平均不透明度与描述 opacity 统计波动的微观参数 $k$ 和 $\theta$ 直接联系起来 [@problem_id:189342]。

### [谱线](@entry_id:193408)的形成

[谱线](@entry_id:193408)为我们提供了关于恒星大气最详尽的信息。[谱线](@entry_id:193408)的形状和强度由多种物理机制决定。

[谱线](@entry_id:193408)的轮廓，即[吸收截面](@entry_id:172609)随频率的变化，通常由**福格特轮廓（Voigt profile）**描述。这是一个高斯轮廓和一个洛伦兹轮廓的卷积。高斯部分源于原子热运动引起的[多普勒频移](@entry_id:158041)，其宽度为**多普勒宽度（Doppler width）** $\Delta\nu_D$。洛伦兹部分源于能级的有限寿命（**自然增宽 natural broadening**）和与其他粒子的碰撞（**碰撞或[压力增宽](@entry_id:159590) collisional/pressure broadening**）。

福格特轮廓的形状由一个无量纲的**阻尼参数（damping parameter）** $a$ 决定，它定义为洛伦兹宽度与[高斯宽度](@entry_id:749763)之比：
$$
a = \frac{\gamma}{4\pi \Delta\nu_D}
$$
其中，$\gamma$ 是洛伦兹轮廓的总阻尼常数（角频率单位下的半高全宽 FWHM），它是自然阻尼常数 $\gamma_{nat}$ 和[碰撞阻尼](@entry_id:202128)常数 $\gamma_{coll}$ 之和。自然阻尼与[激发态](@entry_id:261453)的[平均寿命](@entry_id:195236) $\tau_{nat}$ 直接相关，$\gamma_{nat} = 1/\tau_{nat}$。因此，阻尼参数的完整表达式为：
$$
a = \frac{\frac{1}{\tau_{nat}} + \gamma_{coll}}{4\pi\,\Delta\nu_D}
$$
这个参数衡量了碰撞和自然寿命增宽相对于热增宽的重要性，直接影响[谱线](@entry_id:193408)两翼的形态 [@problem_id:189254]。

要理解[谱线](@entry_id:193408)吸收发生在大气的哪个深度，我们引入**贡献函数（contribution function）**的概念。对于一条弱吸收线，其[谱线](@entry_id:193408)深度（相对于连续谱的强度 depressions）$I_c - I_\nu$ 可以表示为一个积分，其被积函数就是贡献函数，它量化了每个大气层对总[谱线](@entry_id:193408)深度的贡献。例如，在一个简化模型中，假设[谱线](@entry_id:193408)与连续谱的不透明度之比 $\eta_\nu$ 不变，[源函数](@entry_id:161358)线性依赖于连续谱[光学深度](@entry_id:150612) $S(\tau_c) = k \tau_c$，则（未归一化的）贡献函数 $f(\tau_c)$ 正比于 $\tau_c e^{-\tau_c}(\tau_c-1)$。通过求此函数的导数并令其为零，我们发现贡献最大的深度 $\tau_c^*$ 满足二次方程 $-\tau_c^2+3\tau_c-1=0$。由于贡献函数只在 $\tau_c > 1$ 时为正，我们取[正根](@entry_id:199264)，得到[谱线形成](@entry_id:160292)的主要区域位于 $\tau_c^* = (3+\sqrt{5})/2 \approx 2.618$ [@problem_id:189290]。

最后，我们考察[谱线](@entry_id:193408)的总吸收强度，即**等值宽度（equivalent width）** $W_\lambda$。它定义为形成一个与[谱线](@entry_id:193408)吸收掉总能量相等的矩形所需的波长宽度。$W_\lambda$ 与吸收原子柱密度 $N$ 的关系被称为**[生长曲线](@entry_id:177429)（curve of growth）**。[生长曲线](@entry_id:177429)在不同条件下表现出不同的[幂律](@entry_id:143404)行为：

1.  **弱线区（Linear Regime）**: 当光学深度处处很小（$\tau_\lambda \ll 1$）时，[谱线](@entry_id:193408)是光薄的。我们可以用 $1-e^{-\tau_\lambda} \approx \tau_\lambda$ 来近似。此时等值宽度为：
    $$
    W_\lambda = \int (1 - e^{-\tau_\lambda}) d\lambda \approx \int \tau_\lambda d\lambda = N \int \alpha_\lambda d\lambda \propto N
    $$
    因此，$W_\lambda \propto N^1$，等值宽度与原子数成正比。

2.  **[饱和区](@entry_id:262273)（Flat Regime）**: 当[谱线](@entry_id:193408)中心的光学深度变得很大（$\tau_0 \gg 1$），[谱线](@entry_id:193408)中心“饱和”，强度降至接近零。等值宽度的增长变缓，主要靠[谱线](@entry_id:193408)多普勒核的边缘部分贡献。

3.  **阻尼区（Damping Regime）**: 当柱密度非常高时，[谱线](@entry_id:193408)中心已完全饱和，等值宽度的增长完全来自于[洛伦兹剖面](@entry_id:165845)的遥远两翼（即“阻尼翼”）。在这些区域，[吸收截面](@entry_id:172609)近似为 $\alpha_\lambda \propto (\Delta\lambda)^{-2}$。吸收变得显著（$\tau_\lambda \sim 1$）的波长范围 $\Delta\lambda_{wing}$ 满足 $N (\Delta\lambda_{wing})^{-2} \sim 1$，这意味着 $\Delta\lambda_{wing} \propto \sqrt{N}$。由于等值宽度约等于这个吸收区域的宽度，我们得到：
    $$
    W_\lambda \propto \sqrt{N} = N^{1/2}
    $$
    因此，在强线极限下，$W_\lambda$ 的增长与原子柱密度的平方根成正比。

总结这两种极限情况，弱线区的[幂律](@entry_id:143404)指数为 $\beta_w = 1$，强阻尼区的[幂律](@entry_id:143404)指数为 $\beta_s = 1/2$ [@problem_id:189493]。对[生长曲线](@entry_id:177429)的分析是从观测到的等值宽度推断[恒星大气](@entry_id:152088)丰度的经典方法。