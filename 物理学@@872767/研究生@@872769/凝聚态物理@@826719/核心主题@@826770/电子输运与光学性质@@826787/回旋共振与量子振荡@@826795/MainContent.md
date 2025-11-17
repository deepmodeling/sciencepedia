## 引言
在凝聚态物理学中，理解晶体中电子在外场下的行为是探索物质电学、磁学和热学性质的基石。在所有外部探针中，[磁场](@entry_id:153296)尤为特殊，它能以一种非破坏性的方式深刻地改变电子的动力学轨迹，从而揭示其内在的量子力学特性。[回旋共振](@entry_id:139685)（Cyclotron Resonance）与量子振荡（Quantum Oscillations）正是源于电子在[磁场](@entry_id:153296)下量子化运动的两种标志性现象。它们不仅是凝聚态物理教科书中的经典范例，更是当今材料研究中探测电子能带结构最精准、最强大的实验武器。

然而，从抽象的[半经典运动方程](@entry_id:138500)和[朗道能级](@entry_id:144244)理论，到解读真实材料中复杂的[振荡](@entry_id:267781)[频谱](@entry_id:265125)，这之间存在着一条需要系统性知识来跨越的鸿沟。本文旨在填补这一空白，将坚实的理论基础与前沿的实验应用紧密结合。我们将超越简单的抛物线能带模型，深入探讨这些现象在各向异性、多能带以及具有非平庸[拓扑性质](@entry_id:141605)的复杂材料体系中是如何体现的。

通过本文的学习，读者将踏上一段从第一性原理到尖端应用的旅程。在“原理与机制”一章中，我们将建立起描述电子[磁场](@entry_id:153296)动力学的半经典和[量子理论](@entry_id:145435)框架。随后，在“应用与跨学科联系”一章中，我们将展示这些理论如何被用来绘制费米面、测量[有效质量](@entry_id:142879)，并揭示[半导体](@entry_id:141536)、层状材料乃至[拓扑材料](@entry_id:142123)的独特秘密。最后，通过“动手实践”部分，读者将有机会亲手应用所学知识，解决具体的物理问题。让我们首先深入[磁场](@entry_id:153296)中的电子世界，从其运动的基本原理开始探索。

## 原理与机制

本章旨在系统阐述晶体中电子在[磁场](@entry_id:153296)下的动力学行为，并由此引出[回旋共振](@entry_id:139685)与[量子振荡](@entry_id:142355)这两种研究电子结构的强大实验手段。我们将从[半经典动力学](@entry_id:140913)出发，逐步建立起描述这些现象的理论框架，并深入探讨其背后的物理机制，包括[多体相互作用](@entry_id:751663)和散射效应等复杂因素。

### [磁场](@entry_id:153296)中[布洛赫电子](@entry_id:277005)的[半经典动力学](@entry_id:140913)

理解晶体中电子在[磁场](@entry_id:153296)中的行为，其出发点是[半经典运动方程](@entry_id:138500)。在一个均匀[磁场](@entry_id:153296) $\mathbf{B}$ 中，一个具有[色散关系](@entry_id:140395) $\epsilon(\mathbf{k})$ 的[布洛赫电子](@entry_id:277005)，其[波包](@entry_id:154698)的[群速度](@entry_id:147686) $\mathbf{v}$ 和[晶体动量](@entry_id:136369) $\hbar\mathbf{k}$ 的[时间演化](@entry_id:153943)由以下[方程组](@entry_id:193238)描述 [@problem_id:2980376] [@problem_id:2980421]：

$$
\mathbf{v} = \dot{\mathbf{r}} = \frac{1}{\hbar} \nabla_{\mathbf{k}} \epsilon(\mathbf{k})
$$

$$
\hbar \dot{\mathbf{k}} = -e (\dot{\mathbf{r}} \times \mathbf{B})
$$

其中，$-e$ 是电子[电荷](@entry_id:275494)，$\hbar$ 是约化普朗克常数。第一个方程将电子的实[空间速度](@entry_id:190294)与其在[倒空间](@entry_id:754151)的[能带结构](@entry_id:139379)联系起来。第二个方程表明，作用在电子上的[洛伦兹力](@entry_id:145104)改变了其晶体动量。

联立这两个方程，我们可以得到电子在 $\mathbf{k}$ 空间中的[运动方程](@entry_id:170720)：

$$
\hbar \dot{\mathbf{k}} = -e \left( \frac{1}{\hbar} \nabla_{\mathbf{k}} \epsilon(\mathbf{k}) \right) \times \mathbf{B}
$$

这个核心方程蕴含了两个重要的[守恒定律](@entry_id:269268) [@problem_id:2980376]。首先，我们可以考察电子能量随时间的变化率：

$$
\frac{d\epsilon}{dt} = \nabla_{\mathbf{k}} \epsilon(\mathbf{k}) \cdot \dot{\mathbf{k}} = \frac{1}{\hbar} \nabla_{\mathbf{k}} \epsilon(\mathbf{k}) \cdot \left( -e (\mathbf{v} \times \mathbf{B}) \right) = -\frac{e}{\hbar} \mathbf{v} \cdot (\mathbf{v} \times \mathbf{B})
$$

根据矢量[三重积](@entry_id:162942)的性质，$\mathbf{v} \cdot (\mathbf{v} \times \mathbf{B})$ 恒等于零。因此，我们得到第一个重要结论：**在静[磁场](@entry_id:153296)中，电子的能量是守恒的**，即 $d\epsilon/dt = 0$。这意味着电子在 $\mathbf{k}$ 空间中的运动轨迹被限制在一个[等能面](@entry_id:262911)上。

其次，从 $\mathbf{k}$ 的[运动方程](@entry_id:170720)可以看出，$\dot{\mathbf{k}}$ 的方向同时垂直于 $\nabla_{\mathbf{k}} \epsilon(\mathbf{k})$（[等能面](@entry_id:262911)的法线方向）和[磁场](@entry_id:153296) $\mathbf{B}$。由于 $\dot{\mathbf{k}}$ 垂直于 $\mathbf{B}$，电子晶体动量平行于[磁场](@entry_id:153296)的分量 $k_{\parallel}$ 不会随时间改变，即 $dk_{\parallel}/dt = 0$。这是第二个重要结论：**电子晶体动量沿[磁场](@entry_id:153296)方向的分量是守恒的**。

综合这两个[守恒定律](@entry_id:269268)，我们可以确定电子在倒空间中的运动轨迹：它是**[等能面](@entry_id:262911) $\epsilon(\mathbf{k}) = \text{const}$ 与一个垂直于[磁场](@entry_id:153296) $\mathbf{B}$ 的平面 $k_{\parallel} = \text{const}$ 的交线**。这条交线被称为**回旋[轨道](@entry_id:137151)** (cyclotron orbit)。如果这条交线是一个闭合的曲线，电子将在 $\mathbf{k}$ 空间中进行周期性运动。

### 回旋运动与[回旋共振](@entry_id:139685)

我们首先考虑最简单的情形：一个各向同性的抛物线形能带，$\epsilon(\mathbf{k}) = \frac{\hbar^2 k^2}{2m}$，其中 $m$ 是电子的有效质量 [@problem_id:2980421]。在这种情况下，[群速度](@entry_id:147686)为 $\mathbf{v} = \frac{\hbar \mathbf{k}}{m}$。将此代入[运动方程](@entry_id:170720)，得到：

$$
\hbar \dot{\mathbf{k}} = -e \left( \frac{\hbar \mathbf{k}}{m} \right) \times \mathbf{B} \quad \implies \quad \dot{\mathbf{k}} = -\frac{e}{m} (\mathbf{k} \times \mathbf{B})
$$

若[磁场](@entry_id:153296)沿 $z$ 轴方向，$\mathbf{B} = B\hat{\mathbf{z}}$，上述方程的分量形式为 $\dot{k}_x = -\frac{eB}{m}k_y$ 和 $\dot{k}_y = \frac{eB}{m}k_x$。这是一个简谐[振动](@entry_id:267781)的方程，其[角频率](@entry_id:261565)为：

$$
\omega_c = \frac{eB}{m}
$$

这个频率被称为**回旋频率** (cyclotron frequency)。它描述了电子在 $\mathbf{k}$ 空间中沿回旋[轨道运动](@entry_id:162856)的[角速度](@entry_id:192539)。相应地，电子在[实空间](@entry_id:754128)中也进行圆周运动，其**[回旋半径](@entry_id:261534)** (cyclotron radius) 对于一个在[费米面](@entry_id:137798)上的电子（速度为费米速度 $v_F$）的极端[轨道](@entry_id:137151)（$k_z=0$）而言是 $r_c = v_F / \omega_c = mv_F / (eB)$。

这种周期性运动是**[回旋共振](@entry_id:139685)** (cyclotron resonance) 现象的基础。当一个交变[电场](@entry_id:194326) $\mathbf{E}(t)$ 的频率 $\omega$ 与电子的回旋频率 $\omega_c$ 相匹配时，电子会持续地从[电场](@entry_id:194326)中吸收能量，导致在 $\omega = \omega_c$ 处出现一个尖锐的吸收峰。

在更真实的系统中，电子会受到杂质或[声子](@entry_id:140728)的散射，其动量会弛豫。在经典的 **Drude 模型**中，我们可以引入一个唯象的[散射时间](@entry_id:272979) $\tau$ [@problem_id:2980392]。通过求解包含阻尼项的运动方程，可以得到系统的[电导率张量](@entry_id:155827) $\boldsymbol{\sigma}(\omega)$。对于沿 $x$ 方向的驱动[电场](@entry_id:194326)，其[吸收功率](@entry_id:265908)正比于 $\omega \mathrm{Re}[\sigma_{xx}(\omega)]$。可以证明，在弱散射极限下（$\omega_c \tau \gg 1$），吸收谱呈现一个[洛伦兹线型](@entry_id:165845)：

$$
\mathcal{L}(\omega) \propto \frac{1/\tau}{(\omega - \omega_c)^2 + (1/\tau)^2}
$$

这个吸收峰的中心位于 $\omega_c$，而其半高全宽（FWHM）为 $2/\tau$。因此，[回旋共振](@entry_id:139685)实验不仅可以直接测量回旋频率（从而推断[有效质量](@entry_id:142879)），还可以通过测量共振峰的宽度来获取电子的[散射时间](@entry_id:272979)。

### [回旋质量](@entry_id:142038)与费米面几何

对于非抛物线形或各向异性的复杂能带结构，回旋频率的表达式 $\omega_c = eB/m$ 依然成立，但这里的质量 $m$ 不再是简单的能带质量，而是一个依赖于[轨道](@entry_id:137151)几何的**[回旋质量](@entry_id:142038)** (cyclotron mass) $m_c$。

[回旋质量](@entry_id:142038)的普适定义来自于对 $\mathbf{k}$ 空间[轨道](@entry_id:137151)的周期性分析 [@problem_id:2980376] [@problem_id:2980393]。一个完整的[闭合轨道](@entry_id:273635)周期 $T$ 可以通过对[轨道](@entry_id:137151)[路径积分](@entry_id:156701)得到，其结果与[轨道](@entry_id:137151)所围面积 $A(E)$ 对能量的导数相关：

$$
T = \frac{2\pi}{\omega_c} = \frac{\hbar^2}{eB} \frac{\partial A(E)}{\partial E}
$$

将 $\omega_c = eB/m_c$ 代入，我们便得到了[回旋质量](@entry_id:142038)的普适定义，即著名的 **Onsager 关系**：

$$
m_c = \frac{\hbar^2}{2\pi} \left. \frac{\partial A(E)}{\partial E} \right|_{E=E_F}
$$

这个定义表明，[回旋质量](@entry_id:142038)是由[费米能](@entry_id:143977)量处回旋[轨道](@entry_id:137151)的面积随能量变化的速率决定的。它是一个与特定[轨道](@entry_id:137151)相关的量，反映了该[轨道](@entry_id:137151)上的平均能带曲率。

为了更好地理解这一点，考虑一个二维各向异性抛物线能带 $\epsilon(k_x, k_y) = \frac{\hbar^2}{2}(\frac{k_x^2}{m_x} + \frac{k_y^2}{m_y})$ [@problem_id:2980393]。其等能线是椭圆。在能量 $E$ 处，椭圆的面积为 $A(E) = \frac{2\pi E \sqrt{m_x m_y}}{\hbar^2}$。根据上述定义，其[回旋质量](@entry_id:142038)为：

$$
m_c = \frac{\hbar^2}{2\pi} \frac{\partial}{\partial E} \left( \frac{2\pi E \sqrt{m_x m_y}}{\hbar^2} \right) = \sqrt{m_x m_y}
$$

这是一个非常重要的结果：对于各向异性抛物线能带，[回旋质量](@entry_id:142038)是[主轴](@entry_id:172691)质量的几何平均值。这清晰地表明，[回旋质量](@entry_id:142038) $m_c$ 是一个[轨道](@entry_id:137151)平均量，它不同于能带底部的局域**能带质量**张量 $m_{ij}^{-1} = \frac{1}{\hbar^2} \frac{\partial^2 \epsilon}{\partial k_i \partial k_j}$，也不同于决定[直流电导率](@entry_id:273370)的**输运有效质量**。

### [量子振荡](@entry_id:142355)与[朗道能级](@entry_id:144244)

[回旋运动](@entry_id:204632)的量子化是理解量子振荡现象的关键。根据 **Lifshitz-Onsager 量子化规则**，在[磁场](@entry_id:153296)中，一个闭合的回旋[轨道](@entry_id:137151)所围的 $\mathbf{k}$ 空间面积 $A$ 必须满足[量子化条件](@entry_id:182165) [@problem_id:2980425]：

$$
A(E, k_{\parallel}) = (n + \gamma) \frac{2\pi e B}{\hbar}
$$

其中 $n$ 是整数，被称为**朗道能级** (Landau level) 的索引，$\gamma$ 是一个相位因子（通常为 $1/2$）。这个条件意味着，对于给定的[磁场](@entry_id:153296) $B$，电子的能量不再是连续的，而是被限制在一系列分立的朗道能级上。这些朗道能级在能量轴上形成一系列高度简并的态，极大地改变了[费米能级](@entry_id:143215)附近的[态密度](@entry_id:147894)（DOS）。

当改变[磁场强度](@entry_id:197932) $B$ 时，朗道能级的能量位置会随之扫过[费米能级](@entry_id:143215) $E_F$。每当一个[朗道能级](@entry_id:144244)的边缘穿过 $E_F$ 时，系统的[态密度](@entry_id:147894)就会出现一个尖峰，导致自由能、磁化强度、[电阻率](@entry_id:266481)等物理量发生[振荡](@entry_id:267781)。

从[量子化条件](@entry_id:182165)可以看出，[态密度](@entry_id:147894)出现峰值的[磁场](@entry_id:153296)值 $B_n$ 满足：

$$
\frac{1}{B_n} = \frac{2\pi e}{\hbar A(E_F, k_{\parallel})} (n + \gamma)
$$

这表明，这些物理量的[振荡](@entry_id:267781)是以 $1/B$ 为周期的。[振荡](@entry_id:267781)的周期 $\Delta(1/B)$ 直接与[费米面](@entry_id:137798)的[截面](@entry_id:154995)积相关：

$$
\Delta\left(\frac{1}{B}\right) = \frac{2\pi e}{\hbar A(E_F, k_{\parallel})}
$$

[振荡](@entry_id:267781)的**频率** $F$ 定义为周期的倒数，由此我们得到了另一个深刻的 **Onsager 关系** [@problem_id:2980425]：

$$
F = \frac{1}{\Delta(1/B)} = \frac{\hbar}{2\pi e} A(E_F, k_{\parallel})
$$

这个关系式是测量[费米面](@entry_id:137798)几何的基石。通过[傅里叶变换](@entry_id:142120)实验测得的量子振荡[频谱](@entry_id:265125)，可以直接得到费米面垂直于[磁场](@entry_id:153296)方向的[截面](@entry_id:154995)积大小。

在三维材料中，$k_{\parallel}$ 是一个连续变量，这意味着存在一个[连续谱](@entry_id:155477)的可能[轨道](@entry_id:137151)面积 $A(E_F, k_{\parallel})$。然而，实验中通常只观测到少数几个离散的振荡频率。这是因为，总的[振荡](@entry_id:267781)信号是所有[轨道](@entry_id:137151)贡献的叠加。根据**稳相近似** (stationary phase approximation) 原理，只有那些相位随 $k_{\parallel}$ 变化最慢的[轨道](@entry_id:137151)才会产生[相干叠加](@entry_id:170209)，从而对总信号有净贡献。相位稳定的条件是 $\partial A / \partial k_{\parallel} = 0$。满足此条件的[轨道](@entry_id:137151)被称为**极端[轨道](@entry_id:137151)** (extremal orbits)，它们通常对应于费米面的“肚子”（最大[截面](@entry_id:154995)）或“脖子”（最小[截面](@entry_id:154995)）。因此，[量子振荡](@entry_id:142355)实验测量的是[费米面](@entry_id:137798)的**极端[截面](@entry_id:154995)积** $A_{ext}$ [@problem_id:2980425]。

### Lifshitz-Kosevich 理论：定量分析量子振荡

**Lifshitz-Kosevich (LK) 公式**为 de Haas-van Alphen (dHvA) 效应（磁化强度的[振荡](@entry_id:267781)）的振幅提供了一个定量的描述，它揭示了[振荡](@entry_id:267781)信号如何依赖于温度、散射和自旋等因素 [@problem_id:2980371]。对于第 $p$ [次谐波](@entry_id:171489)，[振荡](@entry_id:267781)信号的振幅可以写成多个衰减因子的乘积：

$$
\text{振幅} \propto R_T \cdot R_D \cdot R_S
$$

1.  **温度衰减因子 $R_T$**：有限温度会使[费米-狄拉克分布](@entry_id:138909)函数在费米能级附近变得平滑，这种[热弥散](@entry_id:147972)效应会削弱[振荡](@entry_id:267781)的幅度。该因子由[回旋质量](@entry_id:142038) $m_c$ 和温度 $T$ 决定：
    $$
    R_T = \frac{X}{\sinh(X)}, \quad \text{其中} \quad X = \frac{2\pi^2 p k_B T}{\hbar \omega_c} = \frac{2\pi^2 p k_B T m_c}{\hbar e B}
    $$
    通过研究[振荡](@entry_id:267781)幅度随温度的变化，可以精确地测定出极端[轨道](@entry_id:137151)上的**[回旋质量](@entry_id:142038) $m_c$**。

2.  **Dingle 衰减因子 $R_D$**：[杂质散射](@entry_id:267814)会导致电子的[量子态](@entry_id:146142)寿命有限，从而使[朗道能级](@entry_id:144244)产生展宽。这种展宽同样会抑制[振荡](@entry_id:267781)幅度。该因子由回旋频率 $\omega_c$ 和**[量子寿命](@entry_id:144641)** (quantum lifetime) $\tau_q$ 决定：
    $$
    R_D = \exp\left(-\frac{\pi p}{\omega_c \tau_q}\right) = \exp\left(-\frac{\pi p m_c}{e B \tau_q}\right)
    $$
    在实际分析中，通常引入**[丁格尔温度](@entry_id:142781)** (Dingle temperature) $T_D = \hbar / (2\pi k_B \tau_q)$ 来量化能级展宽。通过研究[振荡](@entry_id:267781)幅度随[磁场](@entry_id:153296)的变化，可以提取出 $T_D$，进而得到 $\tau_q$。

3.  **自旋因子 $R_S$**：在[磁场](@entry_id:153296)中，电子的自旋会发生[塞曼分裂](@entry_id:156350)，导致自旋向上和自旋向下的[朗道能级](@entry_id:144244)序列发生能量上的错位。这两套[振荡](@entry_id:267781)信号的叠加会产生一个拍频效应，其振幅调制由自旋因子描述：
    $$
    R_S = \cos\left(\frac{\pi p g^* m_c}{2 m_e}\right)
    $$
    其中 $g^*$ 是电子的有效朗德 $g$ 因子，$m_e$ 是自由电子质量。在特定[磁场](@entry_id:153296)角度下，当 $g^* m_c / (2 m_e)$ 为半整数时，自旋因子为零，该频率的[振荡](@entry_id:267781)信号会消失，这种现象被称为**自旋零点** (spin zero)，可用于精确测定 $g^*$ 因子。

### 高等主题与精细结构

#### 开放[轨道](@entry_id:137151)

半[经典轨道](@entry_id:177335)的拓扑结构完全由[费米面](@entry_id:137798)形状和[磁场](@entry_id:153296)方向决定。如果费米面在布里渊区中是贯通的（例如，呈波浪状的片层），那么对于某些特定的[磁场](@entry_id:153296)方向，[等能面](@entry_id:262911)与垂直于 $\mathbf{B}$ 的平面的交线可能不会闭合，而是在倒易空间中无限延伸。这种[轨道](@entry_id:137151)被称为**开放[轨道](@entry_id:137151)** (open orbit) [@problem_id:2980360]。

开放[轨道](@entry_id:137151)的存在具有深刻的物理后果。首先，由于[轨道](@entry_id:137151)不闭合，电子的运动不具备周期性，因此不存在明确的回旋频率 $\omega_c$。这意味着与开放[轨道](@entry_id:137151)相关的电子不会对[回旋共振](@entry_id:139685)产生贡献。其次，由于没有闭合面积，开放[轨道](@entry_id:137151)也不满足 Lifshitz-Onsager [量子化条件](@entry_id:182165)，因此它们不会产生 dHvA 或 Shubnikov-de Haas (SdH) [振荡](@entry_id:267781)。然而，开放[轨道](@entry_id:137151)在输运性质上会留下独特的印记。沿开放轨道运动的电子在实空间中会有一个净的漂移速度，这为电流提供了一个高效的通道，导致磁阻在特定方向上不会饱和，并表现出强烈的各向异性，这是探测开放[轨道](@entry_id:137151)存在的经典实验证据。

#### [量子寿命](@entry_id:144641)与输运寿命

LK 理论中的 Dingle 因子引入了[量子寿命](@entry_id:144641) $\tau_q$，它与直流输运中的**输运寿命** (transport lifetime) $\tau_{tr}$（决定电导率和迁移率）有所不同 [@problem_id:2980395] [@problem_id:2980379]。

-   **[量子寿命](@entry_id:144641) $\tau_q$** 反映了电子[量子态](@entry_id:146142)的[相干性](@entry_id:268953)。任何散射事件，无论[散射角](@entry_id:171822)度大小，都会破坏电子[波函数](@entry_id:147440)的相位，从而导致朗道能级的展宽。因此，$1/\tau_q$ 正比于总[散射率](@entry_id:143589)，即对所有散射角积分。
    $$
    \frac{1}{\tau_q} \propto \int W(\theta) d\theta
    $$

-   **输运寿命 $\tau_{tr}$** 描述的是动量弛豫的效率。在[输运过程](@entry_id:177992)中，只有能有效改变电子动量方向的散射（大角度散射）才会贡献于电阻。小角度（前向）散射对动量弛豫的贡献很小。因此，$1/\tau_{tr}$ 的计算中包含一个权重因子 $(1-\cos\theta)$，该因子会抑制小角度散射的贡献。
    $$
    \frac{1}{\tau_{tr}} \propto \int W(\theta) (1-\cos\theta) d\theta
    $$

在许多材料中，特别是高迁移率的[二维电子气](@entry_id:146876)中，杂质势是长程缓变的，导致小角度散射占主导。在这种情况下，$\tau_q$ 会因为大量的小角度散射事件而变得很短，而 $\tau_{tr}$ 则因为 $(1-\cos\theta)$ 因子的抑制而相对较长。这就导致了不等式 $\tau_q  \tau_{tr}$。

这个区别在比较 **de Haas-van Alphen (dHvA)** 效应和 **Shubnikov-de Haas (SdH)** 效应时尤为重要 [@problem_id:2980379]。dHvA 是一种[热力学](@entry_id:141121)效应，其[振荡](@entry_id:267781)幅度直接由[朗道能级](@entry_id:144244)的展宽决定，因此受 $\tau_q$ 控制。而 SdH 是[电阻率](@entry_id:266481)的[振荡](@entry_id:267781)，是一种输运现象。其[振荡](@entry_id:267781)部分的幅度同样受 $\tau_q$ 调制，但其整体可见性还依赖于背景电阻率，后者由 $\tau_{tr}$ 决定。在迁移率较低（$\tau_{tr}$ 较小）的样品中，即使 $\tau_q$ 足够大可以产生可观的态密度[振荡](@entry_id:267781)，SdH 信号的相对振幅也可能非常微弱，导致 dHvA 信号清晰可见而 SdH 信号难以观测。

#### [多体效应](@entry_id:173569)与 Kohn 定理

到目前为止，我们的讨论主要基于单电子图像。然而，电子之间存在[库仑相互作用](@entry_id:747947)，这些[多体效应](@entry_id:173569)会如何影响[回旋共振](@entry_id:139685)和[量子振荡](@entry_id:142355)？

对于 dHvA 效应，其[振荡](@entry_id:267781)幅度所测得的[回旋质量](@entry_id:142038) $m_{dHvA}$，实际上是经由[电子-电子相互作用](@entry_id:139900)[重整化](@entry_id:143501)了的**[准粒子有效质量](@entry_id:140437)** $m^*$，这在[朗道费米液体理论](@entry_id:151062)中有明确的定义。通常，$m^*  m_b$（$m_b$ 为能带质量），表现为质量增强效应。

然而，对于[回旋共振](@entry_id:139685)所测量的质量 $m_{CR}$，情况则更为微妙。根据 **Kohn 定理** [@problem_id:2980403]，对于一个具有**抛物线形能带**的、平动不变的纯净电子系统，在长波极限下（即用均匀[电场](@entry_id:194326)激发），[电子-电子相互作用](@entry_id:139900)**不影响**[回旋共振](@entry_id:139685)的频率。这是因为在这种特定条件下，系统的[质心运动](@entry_id:178374)与内部相对运动是[解耦](@entry_id:637294)的。均匀[电场](@entry_id:194326)只与[质心运动](@entry_id:178374)耦合，而[质心](@entry_id:265015)作为一个整体，其在外[磁场中的运动](@entry_id:261998)不受内部相互作用力的影响。因此，[回旋共振](@entry_id:139685)测量的频率由未[重整化](@entry_id:143501)的**能带质量 $m_b$** 决定，即 $m_{CR} = m_b$。

这个惊人的结果意味着，在满足 Kohn 定理条件的理想系统中，$m_{CR}$ 和 $m_{dHvA}$ 会测量到不同的质量：

$$
m_{CR} = m_b \neq m^* = m_{dHvA}
$$

这种差异为[直接探测](@entry_id:748463)[电子-电子相互作用](@entry_id:139900)导致的[质量重整化](@entry_id:139777)提供了可能。然而，必须强调 Kohn 定理的严格适用条件。一旦能带变为非抛物线形，或者存在多能带效应、能带杂化、[杂质散射](@entry_id:267814)等破坏了理想的[平动](@entry_id:187700)[不变性](@entry_id:140168)和质心/[相对运动](@entry_id:169798)解耦的因素，Kohn 定理便不再成立 [@problem_id:2980403]。在这种更普遍的情况下，[电子-电子相互作用](@entry_id:139900)也会对[回旋共振](@entry_id:139685)频率产生影响，使得 $m_{CR}$ 也会被[重整化](@entry_id:143501)，但其重整化方式通常与 $m_{dHvA}$ 不同。