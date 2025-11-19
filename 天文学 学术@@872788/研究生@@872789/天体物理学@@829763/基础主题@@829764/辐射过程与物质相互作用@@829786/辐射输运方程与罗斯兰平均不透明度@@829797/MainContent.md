## 引言
在天体物理学中，理解能量如何从恒星核心向外输运是构建[恒星结构](@entry_id:136361)与演化模型的基石。在致密的恒星内部，辐射是主要的能量载体，但完整描述[光子](@entry_id:145192)与物质相互作用的[辐射转移方程](@entry_id:160254)极为复杂，难以直接应用于宏观模型。这就引出了一个核心问题：我们如何用一个有效的、平均化的物理量来描述总的辐射能量流？本文旨在系统性地解答这一问题，核心聚焦于“[罗斯兰平均不透明度](@entry_id:754422)”（Rosseland Mean Opacity）这一关键概念。

本文将带领读者踏上一段从基本物理原理到前沿应用的探索之旅。在第一章【原理与机制】中，我们将从[辐射转移方程](@entry_id:160254)出发，详细推导在[扩散近似](@entry_id:147930)下[罗斯兰平均不透明度](@entry_id:754422)的定义，并揭示其作为[调和平均](@entry_id:750175)的深刻物理内涵。接着，在第二章【应用与跨学科联系】中，我们将展示这一概念如何在[恒星结构](@entry_id:136361)、[流体动力学](@entry_id:136788)乃至奇异物质研究等多个领域发挥关键作用。最后，通过【动手实践】部分的一系列精选问题，读者将有机会亲手应用所学知识，巩固对理论的理解。通过本次学习，你将掌握在[光学厚介质](@entry_id:752966)中处理[辐射输运](@entry_id:151695)问题的核心理论工具。

## 原理与机制

在[恒星内部](@entry_id:158197)等[光学厚介质](@entry_id:752966)中，辐射是[能量输运](@entry_id:183081)的主要机制之一。然而，描述[辐射场](@entry_id:164265)与物质相互作用的完整[辐射转移](@entry_id:151695)理论极其复杂。为了在[恒星结构](@entry_id:136361)和演化模型中进行有效计算，我们需要采用一系列简化但物理意义明确的近似方法。本章将深入探讨从基本[辐射转移方程](@entry_id:160254)出发，如何通过[扩散近似](@entry_id:147930)引出罗斯兰（Rosseland）平均不透明度的概念，并阐明其核心原理、计算方法及其在不同物理情境下的应用。

### 基本方程与[扩散近似](@entry_id:147930)

辐射在介质中的传播由[辐射转移方程](@entry_id:160254)（Equation of Radiative Transfer）描述。在一个静态、一维平面平行介质中，该方程可以写作：
$$
\mu \frac{dI_\nu}{dz} = j_\nu - \alpha_\nu I_\nu
$$
其中，$I_\nu(z, \mu)$是频率为$\nu$、在位置$z$处、沿与$z$轴夹角为$\theta$的方向（由[方向余弦](@entry_id:170591)$\mu = \cos\theta$定义）传播的辐射比强度（specific intensity）。$j_\nu$是单位体积、单位时间、单位频率、单位[立体角](@entry_id:154756)内介质的辐射发射系数（emission coefficient），$\alpha_\nu$是[吸收系数](@entry_id:156541)（absorption coefficient）。

在恒星内部这样致密的环境中，物质与辐射的相互作用非常频繁，使得系统可以达到**局部热[动平衡](@entry_id:163330)**（Local Thermodynamic Equilibrium, LTE）。在 LTE 条件下，发射系数和[吸收系数](@entry_id:156541)通过[基尔霍夫定律](@entry_id:180785)（Kirchhoff's Law）关联起来：$j_\nu = \alpha_\nu B_\nu(T)$。其中，$B_\nu(T)$是与介质局部温度$T$对应的[普朗克函数](@entry_id:159605)（Planck function），即黑体辐射的比强度：
$$
B_\nu(T) = \frac{2h\nu^3}{c^2} \frac{1}{\exp(h\nu/k_B T) - 1}
$$
这里，$h$是普朗克常数，$c$是光速，$k_B$是[玻尔兹曼常数](@entry_id:142384)。因此，[辐射转移方程](@entry_id:160254)可以改写为：
$$
\mu \frac{dI_\nu}{dz} = -\alpha_\nu (I_\nu - B_\nu(T))
$$
通常在天体物理学中，我们更常用单位质量的[吸收系数](@entry_id:156541)，即**不透明度**（opacity）$\kappa_\nu$，其定义为$\alpha_\nu = \rho \kappa_\nu$，其中$\rho$是介质的质量密度。

在光学极厚（optically very thick）的介质中，[光子](@entry_id:145192)的平均自由程远小于温度、密度等物理量发生显著变化的宏观尺度。这意味着[辐射场](@entry_id:164265)与周围物质几乎[达到平衡](@entry_id:170346)，[辐射场](@entry_id:164265)本身也趋于各向同性。在这种情况下，比强度$I_\nu$可以围绕各向同性的[普朗克函数](@entry_id:159605)$B_\nu(T)$做微小偏离的展开，这便是**[扩散近似](@entry_id:147930)**（diffusion approximation）的核心思想[@problem_id:259935]。我们将$I_\nu$展开至[方向余弦](@entry_id:170591)$\mu$的一阶：
$$
I_\nu(\mu, z) \approx I_{\nu,0}(z) + \mu I_{\nu,1}(z)
$$
零阶项$I_{\nu,0}$代表各向同性的主要部分，在 LTE 下它等于局域[普朗克函数](@entry_id:159605)$B_\nu(T(z))$。一阶项$\mu I_{\nu,1}$代表了由介质不[均匀性](@entry_id:152612)（如[温度梯度](@entry_id:136845)）引起的微弱各向异性。将此近似代入[辐射转移方程](@entry_id:160254)，我们得到：
$$
\mu \frac{d}{dz} \left( B_\nu(T) + \mu I_{\nu,1} \right) \approx -\rho\kappa_\nu \left( (B_\nu(T) + \mu I_{\nu,1}) - B_\nu(T) \right)
$$
$$
\mu \frac{dB_\nu}{dz} + \mu^2 \frac{dI_{\nu,1}}{dz} \approx -\rho\kappa_\nu \mu I_{\nu,1}
$$
在[扩散近似](@entry_id:147930)下，我们假设各向异性部分$I_{\nu,1}$的空间变化是高阶小量，可以忽略，即$\frac{dI_{\nu,1}}{dz} \approx 0$。于是方程简化为：
$$
\frac{dB_\nu}{dz} \approx -\rho\kappa_\nu I_{\nu,1} \quad \implies \quad I_{\nu,1} \approx -\frac{1}{\rho\kappa_\nu} \frac{dB_\nu}{dz}
$$
这样，我们就得到了比强度的各向异性部分与[普朗克函数](@entry_id:159605)梯度之间的关系。

物理上我们关心的是净[能量流](@entry_id:142770)，即[辐射通量](@entry_id:151732)（radiative flux）。沿$z$方向的单频[辐射通量](@entry_id:151732)$F_\nu$定义为比强度对所有立体角的第一矩：
$$
F_\nu = \int_{4\pi} I_\nu \mu \, d\Omega = 2\pi \int_{-1}^{1} I_\nu(\mu) \mu \, d\mu
$$
将$I_\nu$的[扩散近似](@entry_id:147930)表达式代入，我们得到：
$$
F_\nu \approx 2\pi \int_{-1}^{1} (B_\nu(T) + \mu I_{\nu,1}) \mu \, d\mu = 2\pi \left( B_\nu(T) \int_{-1}^{1} \mu d\mu + I_{\nu,1} \int_{-1}^{1} \mu^2 d\mu \right)
$$
由于$\int_{-1}^{1} \mu d\mu = 0$且$\int_{-1}^{1} \mu^2 d\mu = \frac{2}{3}$，通量表达式简化为$F_\nu = \frac{4\pi}{3} I_{\nu,1}$。将之前求得的$I_{\nu,1}$代入，我们便得到了描述单频[辐射扩散](@entry_id:158401)的基本方程：
$$
F_\nu = -\frac{4\pi}{3\rho\kappa_\nu} \frac{dB_\nu}{dz}
$$
这个方程类似于[傅里叶热传导定律](@entry_id:138911)，表明单频[辐射通量](@entry_id:151732)正比于[普朗克函数](@entry_id:159605)梯度的负值，而比例系数则反比于该频率下的[不透明度](@entry_id:160442)$\kappa_\nu$。

### [罗斯兰平均不透明度](@entry_id:754422)：对总[辐射通量](@entry_id:151732)的平均

上述方程描述了单一频率的[辐射通量](@entry_id:151732)。然而，在天体物理模型中，我们更关心的是通过所有频率积分得到的总[辐射通量](@entry_id:151732)$F = \int_0^\infty F_\nu d\nu$。对上式直接积分会遇到一个难题：
$$
F = \int_0^\infty F_\nu d\nu = -\int_0^\infty \frac{4\pi}{3\rho\kappa_\nu} \frac{dB_\nu}{dz} d\nu
$$
由于[不透明度](@entry_id:160442)$\kappa_\nu$本身是频率的复杂函数，这个积分无法直接简化。我们希望找到一种“有效”的或“平均”的[不透明度](@entry_id:160442)$\kappa_R$，使得总通量可以写成一个类似单频情况的简洁形式。具体来说，我们定义**[罗斯兰平均不透明度](@entry_id:754422)**（Rosseland Mean Opacity），$\kappa_R$，来满足以下关系式：
$$
F = -\frac{4\pi}{3\rho\kappa_R} \frac{d}{dz}\left( \int_0^\infty B_\nu(T) d\nu \right)
$$
注意到$\int_0^\infty B_\nu(T) d\nu = \frac{\sigma}{\pi}T^4 = \frac{ac}{4\pi}T^4$，其中$\sigma$是斯特藩-[玻尔兹曼常数](@entry_id:142384)，$a$是辐射常数。因此上式与我们熟悉的总辐射能[流形](@entry_id:153038)式一致。利用链式法则，$\frac{d}{dz} = \frac{dT}{dz}\frac{\partial}{\partial T}$，我们可以将两个总通量的表达式等同起来：
$$
\int_0^\infty \frac{1}{\kappa_\nu} \frac{\partial B_\nu}{\partial T} \frac{dT}{dz} d\nu = \frac{1}{\kappa_R} \frac{\partial}{\partial T}\left( \int_0^\infty B_\nu d\nu \right) \frac{dT}{dz}
$$
由于积分和[微分](@entry_id:158718)可以交换次序，上式变为：
$$
\left( \int_0^\infty \frac{1}{\kappa_\nu} \frac{\partial B_\nu}{\partial T} d\nu \right) \frac{dT}{dz} = \frac{1}{\kappa_R} \left( \int_0^\infty \frac{\partial B_\nu}{\partial T} d\nu \right) \frac{dT}{dz}
$$
由此，我们得到了[罗斯兰平均不透明度](@entry_id:754422)的倒数的定义式 [@problem_id:259935] [@problem_id:259959]：
$$
\frac{1}{\kappa_R} = \frac{\int_0^\infty \frac{1}{\kappa_\nu} \frac{\partial B_\nu(T)}{\partial T} d\nu}{\int_0^\infty \frac{\partial B_\nu(T)}{\partial T} d\nu}
$$
这个定义清晰地表明，罗斯兰平均是一种特殊的**调和平均**（harmonic mean）。它对[不透明度](@entry_id:160442)的倒数$1/\kappa_\nu$进行加权平均，权重是[普朗克函数](@entry_id:159605)对温度的偏导数$\frac{\partial B_\nu}{\partial T}$。

### 罗斯兰权重函数的物理意义

[罗斯兰平均不透明度](@entry_id:754422)的核心在于其独特的权重函数$W(\nu, T) = \frac{\partial B_\nu(T)}{\partial T}$。为了理解其物理意义，我们首先需要推导出它的具体形式 [@problem_id:260112]。对[普朗克函数](@entry_id:159605)求关于温度$T$的[偏导数](@entry_id:146280)，并引入无量纲变量$x = h\nu / (k_B T)$：
$$
\frac{\partial B_\nu}{\partial T} = \frac{2h\nu^3}{c^2} \frac{d}{dT} \left( e^{h\nu/k_B T} - 1 \right)^{-1}
$$
利用链式法则，$\frac{d}{dT} = \frac{dx}{dT} \frac{d}{dx}$，且$\frac{dx}{dT} = -\frac{h\nu}{k_B T^2} = -\frac{x}{T}$，我们得到：
$$
\frac{\partial B_\nu}{\partial T} = \frac{2h\nu^3}{c^2} \left[ - \frac{1}{(e^x - 1)^2} e^x \left(-\frac{h\nu}{k_B T^2}\right) \right] = \frac{2h^2\nu^4}{c^2 k_B T^2} \frac{e^{h\nu/k_B T}}{\left( e^{h\nu/k_B T} - 1 \right)^2}
$$
这个函数$W(\nu, T)$描述了在给定频率$\nu$处，[黑体辐射谱](@entry_id:158574)的强度随温度变化的敏感度。$W(\nu, T)$在$h\nu \approx 3.83 k_B T$处达到峰值，并在低频和高频端迅速衰减。

罗斯兰平均的结构——即对$1/\kappa_\nu$进行平均——具有深刻的物理含义。[调和平均](@entry_id:750175)的特性是，平均值会偏向于集合中较小的数值。在这里，这意味着[罗斯兰平均不透明度](@entry_id:754422)$\kappa_R$对不透明度$\kappa_\nu$较小的频率区间（即介质相对“透明”的“窗口”）给予了最高的权重。这完全符合物理直觉：总的[能量输运](@entry_id:183081)效率主要由那些最容易通过介质的频率的辐射决定。即使在大多数频率上介质都是极不透明的，只要存在几个透明的“窗口”，辐射能量就可以有效地流出。罗斯兰平均正是通过其数学形式捕捉到了这一关键的物理过程。

值得注意的是，在实际的不透明度计算中，需要考虑受激发射（stimulated emission）的修正。修正后的[吸收系数](@entry_id:156541)$\kappa'_\nu$与真实吸收系数$\kappa_\nu$的关系是$\kappa'_\nu = \kappa_\nu (1 - e^{-h\nu/k_BT})$。然而，罗斯兰平均的定义式中已经巧妙地包含了这一修正。权重函数$\frac{\partial B_\nu}{\partial T}$中的因子可以分解为：
$$
\frac{e^x}{(e^x - 1)^2} = \frac{1}{e^x - 1} \frac{1}{1 - e^{-x}}
$$
因此，$\frac{1}{\kappa_\nu} \frac{\partial B_\nu}{\partial T}$的表达式可以看作是作用在$\frac{1}{\kappa_\nu (1 - e^{-h\nu/k_BT})}$上的。这表明，从[扩散近似](@entry_id:147930)推导出的罗斯兰平均自动地使用了经过[受激发射](@entry_id:150501)修正后的有效不透明度 [@problem_id:260009]。

### 应用与计算

有了[罗斯兰平均不透明度](@entry_id:754422)的定义式，我们便可以针对具体的物质[不透明度](@entry_id:160442)定律$\kappa_\nu$来计算其值。

一个常见的例子是类克莱默斯定律（Kramers-like law），其形式为$\kappa_\nu \propto \nu^{-3}$。假设某等离子体的[不透明度](@entry_id:160442)为$\kappa_\nu = \kappa_0 \nu^{-3}$，我们可以计算其[罗斯兰平均不透明度](@entry_id:754422) [@problem_id:259935]。这需要分别计算定义式中的分子和分母积分。通过引入无量纲变量$x = h\nu/k_BT$并利用给定的积分恒等式，如$\int_0^\infty \frac{x^s e^x}{(e^x-1)^2} dx = s\Gamma(s)\zeta(s)$，最终可以得到$\kappa_R$与温度$T$的关系。对于$\kappa_\nu = \kappa_0 \nu^{-3}$，计算结果表明$\kappa_R \propto T^{-3}$。

在[恒星结构模型](@entry_id:160132)中，我们经常使用**辐射传导系数**（radiative conductivity）$K_{rad}$来描述[辐射通量](@entry_id:151732)与温度梯度的关系，即$\vec{F} = -K_{rad} \nabla T$。将罗斯兰平均的定义代入，可以得到$K_{rad}$与$\kappa_R$的关系：
$$
K_{rad} = \frac{4\pi}{3\rho\kappa_R} \int_0^\infty \frac{\partial B_\nu}{\partial T} d\nu = \frac{4\pi}{3\rho\kappa_R} \frac{acT^3}{\pi} = \frac{4acT^3}{3\rho\kappa_R}
$$
我们也可以直接从积分形式计算$K_{rad}$ [@problem_id:260009]：
$$
K_{rad} = \frac{4\pi}{3\rho} \int_0^\infty \frac{1}{\kappa_\nu} \frac{\partial B_\nu(T)}{\partial T} d\nu
$$
对于一个包含[受激发射](@entry_id:150501)修正的类克莱默斯定律$\kappa_\nu(\nu, T) = \kappa_0 (\nu_0/\nu)^3 (1 - e^{-h\nu/k_BT})^{-1}$，通过计算上述积分，可以得到$K_{rad}$作为温度和其他[物理常数](@entry_id:274598)的函数，结果表明$K_{rad} \propto T^6 / \kappa_0$。

当介质是多种成分的混合物时，其总[不透明度](@entry_id:160442)是各组分质量分数加权的和：$\kappa_\nu = \sum_i X_i \kappa_{\nu,i}$。[罗斯兰平均不透明度](@entry_id:754422)的计算也需要考虑这种混合效应。例如，考虑一个由两种组分 A 和 B 组成的混合气体 [@problem_id:260114]。组分 A 的不透明度为常数$\kappa_{\nu,A} = \kappa_0$，而组分 B 在某个截断频率$\nu_0$以下是完全透明的（$\kappa_{\nu,B}=0$），以上是完全不透明的（$\kappa_{\nu,B}=\infty$）。这种模型可以模拟[光致电离](@entry_id:157870)边。总[不透明度](@entry_id:160442)为$\kappa_\nu = X\kappa_0$当$\nu \lt \nu_0$，而$\kappa_\nu=\infty$当$\nu \ge \nu_0$。因此，$1/\kappa_\nu$在$\nu \ge \nu_0$时为零。计算罗斯兰平均时，[分子积分](@entry_id:185751)的上限就从无穷大变成了$\nu_0$。在低能近似（$h\nu_0 \ll k_BT$）下，可以得到混合物的$\kappa_R$严重依赖于低频透明窗口的性质，其结果为$\kappa_R \propto X\kappa_0 (k_BT/h\nu_0)^3$。

### 与其他平均不透明度的比较：普朗克平均

罗斯兰平均并非唯一有用的平均[不透明度](@entry_id:160442)。另一个重要概念是**[普朗克平均不透明度](@entry_id:753471)**（Planck Mean Opacity），$\kappa_P$，其定义为：
$$
\kappa_P = \frac{\int_0^\infty \kappa_\nu B_\nu(T) d\nu}{\int_0^\infty B_\nu(T) d\nu}
$$
与罗斯兰平均不同，普朗克平均是一种直接的算术平均，其权重函数是[普朗克函数](@entry_id:159605)$B_\nu(T)$本身。$\kappa_P$描述的是处在温度为$T$的黑体辐射场中的物质，其单位质量吸收辐射能量的总速率。它在描述物质与辐射场的能量交换平衡时非常有用。

罗斯兰平均和普朗克平均在物理意义和数值上都有显著差异。$\kappa_R$描述的是能量**输运**的阻碍程度，而$\kappa_P$描述的是能量**吸收**的总能力。由于$\kappa_R$是[调和平均](@entry_id:750175)，它对不透明度低的频率区域敏感；而$\kappa_P$是算术平均，它对不透明度高的频率区域（即吸收峰）更敏感。

我们可以通过一个具体的例子来比较它们 [@problem_id:259968]。假设[不透明度](@entry_id:160442)定律为简单的[幂律](@entry_id:143404)形式$\kappa_\nu = A\nu$（其中$A$为常数）。通过分别计算$\kappa_P$和$\kappa_R$，可以发现它们的值并不相等。计算得到的比值$\kappa_P/\kappa_R$是一个大于1的常数，可以用[黎曼zeta函数](@entry_id:161915)的值来表示：$\frac{\zeta(3)\zeta(5)}{\zeta(4)^2}$。

事实上，可以利用柯西-[施瓦茨不等式](@entry_id:202153)证明一个普适的不等关系：$\kappa_R \le \kappa_P$。等号仅在$\kappa_\nu$为常数（与频率无关）时成立。这个不等式再次强调了两种平均的物理差异：[能量输运](@entry_id:183081)的有效不透明度（$\kappa_R$）总是小于或等于能量吸收的平均不透明度（$\kappa_P$），因为能量总是倾向于通过阻力最小的路径（透明窗口）进行输运。

### 高级理论基础

[罗斯兰平均不透明度](@entry_id:754422)的形式不仅可以从唯象的[扩散近似](@entry_id:147930)中推导出来，还可以从更基本的物理原理中获得，这进一步彰显了其深刻的物理内涵。

一种方法是基于非平衡态[热力学](@entry_id:141121)的**[最小熵产生](@entry_id:183433)原理** [@problem_id:259959]。该原理指出，在给定的约束条件下（例如，总[辐射通量](@entry_id:151732)固定），系统将演化到一个使总熵产生率最小的定态。通过将总[熵产生](@entry_id:141771)率表示为各频率[辐射通量](@entry_id:151732)的泛函，并使用拉格朗日乘子法在总通量固定的约束下求其极小值，可以证明，最终得到的宏观输运关系恰好由[罗斯兰平均不透明度](@entry_id:754422)所描述。这表明罗斯兰平均描述的是在给定总[能量流](@entry_id:142770)条件下最高效（[熵增](@entry_id:138799)最慢）的输运方式。

另一种更为基础的方法来自[统计力](@entry_id:194984)学的**[格林-久保关系](@entry_id:144763)**（Green-Kubo relations）[@problem_id:260035]。该关系将宏观[输运系数](@entry_id:136790)（如辐射传导系数$K_{rad}$）与微观通量算符的[时间自相关函数](@entry_id:145679)联系起来。通过建立辐射热流密度算符的模型，并引入其时间关联函数的衰减（由[光子](@entry_id:145192)与介质的相互作用决定，其[弛豫时间](@entry_id:191572)$\tau_\nu \propto 1/\kappa_\nu$），再结合涨落-耗散定理，可以直接从[格林-久保关系](@entry_id:144763)中积分推导出辐射传导系数$K_{rad}$的表达式。将此表达式与$K_{rad}$和$\kappa_R$的唯象关系进行比较，可以反解出$\kappa_R$的定义，其结果与我们之前从[扩散近似](@entry_id:147930)得到的[调和平均](@entry_id:750175)形式完全一致。这个推导将罗斯兰平均植根于微观涨落和耗散的统计物理图像之中。

此外，**[变分原理](@entry_id:198028)**也为[罗斯兰平均不透明度](@entry_id:754422)提供了强大的理论和计算工具 [@problem_id:259987]。可以构建一个关于某个试验函数$\psi(\nu)$的泛函$J[\psi]$，该泛函的最大值对应于$1/\kappa_R$的一个严格下界。这意味着，通过选择任何合理的试验函数，我们都可以得到$\kappa_R$的一个严格上界。这种方法在无法精确计算罗斯兰平均积[分时](@entry_id:274419)，为估算其[数值范围](@entry_id:752817)提供了一个系统性的途径。

### 推广：[各向异性介质](@entry_id:187796)

前面的讨论都假设介质是各向同性的，即不透明度$\kappa_\nu$与辐射传播方向无关。然而，在某些天体物理环境（如存在强[磁场](@entry_id:153296)或结构化流动的区域）中，介质本身可能是各向异性的。

在这种情况下，吸收系数会依赖于[方向余弦](@entry_id:170591)$\mu$，例如$\alpha_\nu(\mu) = \alpha_{0,\nu}(1 + \epsilon \mu^2)$ [@problem_id:259962]。在这种情况下重复[扩散近似](@entry_id:147930)的推导，会发现[辐射通量](@entry_id:151732)$F_\nu$与[普朗克函数](@entry_id:159605)梯度的关系仍然是线性的，但比例系数会因各向异性而改变。这个新的[输运系数](@entry_id:136790)会依赖于描述各向异性程度的参数$\epsilon$。

更一般地，对于[各向异性介质](@entry_id:187796)，[不透明度](@entry_id:160442)本身应该被视为一个张量$\boldsymbol{\kappa}_\nu$。此时，[辐射通量](@entry_id:151732)矢量$\mathbf{F}$与[温度梯度](@entry_id:136845)矢量$\nabla T$之间的关系由一个**辐射传导张量**$\mathbf{K}$描述：$\mathbf{F} = - \mathbf{K} \cdot \nabla T$。这意味着[辐射通量](@entry_id:151732)的方向不一定与[温度梯度](@entry_id:136845)的方向平行。相应地，[罗斯兰平均不透明度](@entry_id:754422)也推广为一个二阶张量$\boldsymbol{\kappa}_R$ [@problem_id:260128]。其逆张量$\boldsymbol{\kappa}_R^{-1}$的定义也通过对一个方向依赖的积分进行加权平均得到。

例如，对于一个具有单轴各向异性的介质，其[不透明度](@entry_id:160442)沿主轴方向$(\kappa_{\nu,\parallel})$和垂直于[主轴](@entry_id:172691)方向$(\kappa_{\nu,\perp})$不同。如果这两个分量的比值$r = \kappa_{\nu, \parallel} / \kappa_{\nu, \perp}$不依赖于频率，那么[罗斯兰平均不透明度](@entry_id:754422)张量的平行与垂直分量之比$(\kappa_R)_{\parallel} / (\kappa_R)_{\perp}$将是一个仅依赖于$r$的常数。对于$r=2$的特定情况，可以计算出此比值为$(\pi-2)/(4-\pi)$。这表明，介质的微观各向异性会直接转化为宏观[能量输运](@entry_id:183081)性质的各向异性。