## 引言
在高速可压缩流动的研究中，理解能量如何转化以及不可逆性如何影响流动状态至关重要。静态性质（如温度和压力）随流体运动而不断变化，使得追踪能量和效率变得复杂。为了解决这一挑战，[流体力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)引入了**[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)**（stagnation properties）这一强大的概念，它通过一个[标准化](@keyword=z_score_normalization|lang=zh-CN|style=Feynman)的参考状态——流体被等熵减速至静止的状态——来统一衡量流动的总能量和潜在做功能力。本文旨在系统性地介绍[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)的理论与应用。我们将从“原理与机制”入手，详细定义[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)、压力和密度，并揭示它们在等熵及非等熵[绝热流](@keyword=adiabatic_flow|lang=zh-CN|style=Feynman)动中的基本行为规律。随后，在“应用与跨学科联系”一章中，我们将展示这些概念如何应用于解决航空航天、动力推进和传热等领域的实际工程问题。最后，通过“动手实践”部分提供的练习，读者将有机会巩固所学知识，将理论应用于具体计算。

## 原理与机制

在可压缩流动的研究中，将[流体性质](@keyword=fluid_properties|lang=zh-CN|style=Feynman)与一个标准参考状态相关联是一种强有力的分析工具。这个参考状态被称为**[驻点](@keyword=stationary_points|lang=zh-CN|style=Feynman)状态**（stagnation state），在此状态下，流体被想象成从其局部流动状态，经由一个可逆绝热（即**等熵**）过程，速度降为零。与之相关的物理量，如温度、压力和密度，则被称为**[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)**（stagnation properties）。这些性质不仅为[高速流](@keyword=high_speed_flow|lang=zh-CN|style=Feynman)动分析提供了便利的基准，而且深刻地揭示了[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)和热力学第二定律在[流体动力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)中的具体体现。

### [驻点](@keyword=stationary_points|lang=zh-CN|style=Feynman)状态与[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)的定义

想象一个跟随流体微元移动的观察者。该微元具有其局部的**静态性质**（static properties），如静态温度 $T$、静态压力 $P$ 和静态密度 $\rho$，以及一个速度 $V$。如果这个微元在不受任何热量传递或做功的情况下被平稳地减速至静止，其所蕴含的动能将完全转化为内能（和流动功），从而使其[热力学状态](@keyword=thermodynamic_states|lang=zh-CN|style=Feynman)发生改变。最终达到的这个假想的静止状态，就是[驻点](@keyword=stationary_points|lang=zh-CN|style=Feynman)状态。

#### [驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)与[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)

根据[热力学第一定律](@keyword=first_law_of_thermodynamics|lang=zh-CN|style=Feynman)，对于一个稳定流动的控制体，在没有热交换和轴功的情况下，能量是守恒的。流体微元所携带的总能量可以用[总焓](@keyword=total_enthalpy|lang=zh-CN|style=Feynman)（total enthalpy）或**[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)**（stagnation enthalpy）$h_0$ 来量度。它定义为静态焓 $h$ 与单位质量动能之和：

$$h_0 = h + \frac{V^2}{2}$$

这个关系式是[驻点](@keyword=stationary_points|lang=zh-CN|style=Feynman)概念的能量基础。[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)代表了流体在任意一点的总能量含量。例如，在一个低温[风洞](@keyword=wind_tunnel|lang=zh-CN|style=Feynman)的测试段中，如果氮气流的静态温度为 $125.0 \text{ K}$，流速为 $510.0 \text{ m/s}$，并且其定[压比](@keyword=pressure_ratio|lang=zh-CN|style=Feynman)热 $c_p$ 为 $1.040 \mathrm{kJ/(kg\cdot K)}$，我们可以直接计算其[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)。首先计算静态焓 $h = c_p T = 1.040 \times 125.0 = 130.0 \text{ kJ/kg}$，然后计算单位质量动能 $\frac{V^2}{2} = \frac{(510.0)^2}{2} \approx 130050 \text{ J/kg} = 130.05 \text{ kJ/kg}$。因此，[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)为 $h_0 = 130.0 + 130.05 = 260.05 \text{ kJ/kg}$ ([@problem_id:1792384])。

对于[量热完全气体](@keyword=calorically_perfect_gas|lang=zh-CN|style=Feynman)（calorically perfect gas），即比热为常数的理想气体，焓是温度的线性函数，$h = c_p T$。将此关系代入驻点[焓的定义](@keyword=h=u+pv|lang=zh-CN|style=Feynman)，我们得到：

$$c_p T_0 = c_p T + \frac{V^2}{2}$$

由此，我们可以定义**[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)**（stagnation temperature）$T_0$：

$$T_0 = T + \frac{V^2}{2 c_p}$$

[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman) $T_0$ 是流体总能量的一个直接度量。它不是一个依赖于过程路径（如等熵）的定义，而仅仅是[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)的体现。一个直观的例子是人呼出的气体。在肺部的空气可以近似认为是速度为零的[驻点](@keyword=stationary_points|lang=zh-CN|style=Feynman)状态，其温度 $T_0$ 约为 $310.0 \text{ K}$。当用力呼气时，气体加速形成射流。假设在口腔出口处测得气流速度为 $50.0 \text{ m/s}$，我们可以计算出此时气流的静态温度 $T$。根据驻点[温度的定义](@keyword=temperature_definition|lang=zh-CN|style=Feynman)，静态温度会略有下降：$T = T_0 - \frac{V^2}{2 c_p} = 310.0 - \frac{(50.0)^2}{2 \times 1005} \approx 308.8 \text{ K}$ ([@problem_id:1792380])。这解释了为什么快速呼出的气流感觉比缓慢呼出的气流要凉爽一些——部分内能转化为了宏观的动能。

#### [驻点压力](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)与驻点密度

与[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)不同，**[驻点压力](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)**（stagnation pressure）$P_0$ 和**[驻点](@keyword=stationary_points|lang=zh-CN|style=Feynman)密度**（stagnation density）$\rho_0$ 的定义中包含了一个关键假设：流体是从其当前状态 $(P, T, \rho, V)$ 经过一个**[等熵过程](@keyword=isentropic_process|lang=zh-CN|style=Feynman)**被减速到静止的。这个过程是可逆且绝热的。因此，$P_0$ 和 $\rho_0$ 是流体在与当前状态具有相同熵值和[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)的静止状态下的压力和密度。这个[等熵过程](@keyword=isentropic_process|lang=zh-CN|style=Feynman)的假设至关重要，它将驻点压力与流动的可逆性紧密联系在一起。

### [等熵流](@keyword=isentropic_flow|lang=zh-CN|style=Feynman)动中的[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)关系

在[等熵流](@keyword=isentropic_flow|lang=zh-CN|style=Feynman)动中，流体沿着[流线](@keyword=streamlines|lang=zh-CN|style=Feynman)运动时没有熵的产生。在这种理想情况下，[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman) $(T_0, P_0, \rho_0)$ 在整个流场中都保持不变，成为全局的参考常数。利用理想气体的等熵关系，我们可以推导出静态性质与[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)之间只依赖于马赫数 $M = V/a$（其中 $a = \sqrt{\gamma R T}$ 是当地声速）和比热比 $\gamma$ 的普适关系式。

首先，将马赫数的定义代入[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)的表达式中：

$$\frac{T_0}{T} = 1 + \frac{V^2}{2 c_p T} = 1 + \frac{M^2 a^2}{2 c_p T} = 1 + \frac{M^2 (\gamma R T)}{2 c_p T}$$

利用[理想气体](@keyword=perfect_gases|lang=zh-CN|style=Feynman)关系式 $c_p = \frac{\gamma R}{\gamma - 1}$，上式可以简化为：

$$\frac{T_0}{T} = 1 + \frac{\gamma - 1}{2} M^2$$

这是连接静态温度和[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)的最基本关系式之一。对于[等熵过程](@keyword=isentropic_process|lang=zh-CN|style=Feynman)，我们有 $P/\rho^\gamma = \text{const}$ 和 $P/T^{\gamma/(\gamma-1)} = \text{const}$。将这些关系应用于从静态到驻点状态的[等熵过程](@keyword=isentropic_process|lang=zh-CN|style=Feynman)，可以得到压力和密度的关系：

$$\frac{P_0}{P} = \left(\frac{T_0}{T}\right)^{\frac{\gamma}{\gamma-1}} = \left(1 + \frac{\gamma-1}{2} M^2\right)^{\frac{\gamma}{\gamma-1}}$$

$$\frac{\rho_0}{\rho} = \left(\frac{T_0}{T}\right)^{\frac{1}{\gamma-1}} = \left(1 + \frac{\gamma-1}{2} M^2\right)^{\frac{1}{\gamma-1}}$$

这些关系式是可压缩[等熵流](@keyword=isentropic_flow|lang=zh-CN|style=Feynman)理论的基石。它们使得我们能够仅通过测量[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)（例如通过[皮托管](@keyword=pitot_tube|lang=zh-CN|style=Feynman)测量）和静态压力，就能确定流动的马赫数和速度。例如，流场的单位质量动能 $\frac{V^2}{2}$ 可以完全用[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)量表示。从能量方程可知 $\frac{V^2}{2} = c_p(T_0 - T)$，再利用等熵关系将 $T$ 替换掉，即可得到：

$$\frac{V^2}{2} = c_p T_0 \left[1 - \frac{T}{T_0}\right] = c_p T_0 \left[1 - \left(\frac{P}{P_0}\right)^{\frac{\gamma - 1}{\gamma}}\right]$$

这个表达式精确地给出了流体动能与其压力状态之间的联系 ([@problem_id:1792370])。

基于这些核心关系，还可以定义其他有用的参考性质。例如，**[驻点](@keyword=stationary_points|lang=zh-CN|style=Feynman)声速** $a_0$，即在[驻点](@keyword=stationary_points|lang=zh-CN|style=Feynman)状态下的声速。由于 $a = \sqrt{\gamma R T}$，我们有：

$$\frac{a_0}{a} = \sqrt{\frac{\gamma R T_0}{\gamma R T}} = \sqrt{\frac{T_0}{T}} = \sqrt{1 + \frac{\gamma-1}{2} M^2}$$

这表明驻点声速总是大于当地声速 ([@problem_id:1792350])。另一个重要的参考状态是**临界状态**（critical state），也称为[声速点](@keyword=sonic_point|lang=zh-CN|style=Feynman)或“星号”状态，即马赫数 $M=1$ 时的状态。该点的性质用 $P^*, T^*, \rho^*$ 表示。将 $M=1$ 代入上述等熵关系式，我们可以得到[驻点压力](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)与[临界压力](@keyword=critical_pressure|lang=zh-CN|style=Feynman)之比：

$$\frac{P_0}{P^*} = \left(1 + \frac{\gamma - 1}{2}\right)^{\frac{\gamma}{\gamma-1}} = \left(\frac{\gamma + 1}{2}\right)^{\frac{\gamma}{\gamma-1}}$$

这个比值对于给定的气体（即给定的 $\gamma$ 值）是一个常数，在分析喷[管流](@keyword=pipe_flow|lang=zh-CN|style=Feynman)动（特别是[壅塞流](@keyword=choked_flow|lang=zh-CN|style=Feynman)动）中起着至关重要的作用 ([@problem_id:1792327])。

### 不[可逆过程](@keyword=reversible_processes|lang=zh-CN|style=Feynman)中的[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)：[熵增](@keyword=entropy_generation|lang=zh-CN|style=Feynman)与[驻点压力损失](@keyword=stagnation_pressure_loss|lang=zh-CN|style=Feynman)

现实世界中的流动，如存在摩擦的管道流或穿过激波的流动，都不是等熵的。它们是不[可逆过程](@keyword=reversible_processes|lang=zh-CN|style=Feynman)，伴随着熵的产生。理解[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)在这些过程中的变化，是[可压缩流体](@keyword=compressible_fluids|lang=zh-CN|style=Feynman)力学的核心。

#### 绝热过程中的[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)守恒

根据热力学第一定律，对于一个[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman)、绝热且无轴功的流动系统，[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman) $h_0$ 必定守恒。这意味着，无论流动过程中是否存在摩擦等不可逆因素，只要系统是绝热的，下游的[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)就等于上游的[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)，$h_{0,1} = h_{0,2}$。对于[量热完全气体](@keyword=calorically_perfect_gas|lang=zh-CN|style=Feynman)，这直接等价于[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)守恒：

$$T_{0,1} = T_{0,2}$$

这个结论的[适用范围](@keyword=domain_of_validity|lang=zh-CN|style=Feynman)非常广泛。例如，在一段长而绝热的管道中，气体因与管壁的摩擦而经历压力和温度的变化（即[范诺流](@keyword=fanno_flow|lang=zh-CN|style=Feynman)，Fanno flow）。尽管摩擦是典型的不可逆过程，会导致[熵增](@keyword=entropy_generation|lang=zh-CN|style=Feynman)加，但由于整个过程是绝热的，[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)始终保持不变 ([@problem_id:1792374])。同样，当气流穿过一道[正激波](@keyword=normal_shock_waves|lang=zh-CN|style=Feynman)时，尽管[流体性质](@keyword=fluid_properties|lang=zh-CN|style=Feynman)发生剧烈的不连续变化，但激波本身极薄，可以视为[绝热过程](@keyword=adiabatic_process|lang=zh-CN|style=Feynman)。因此，穿过激波前后，流体的[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)也是守恒的 ([@problem_id:1792397])。[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)的守恒本质上是绝热系统中总[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)的直接体现。

#### [熵增](@keyword=entropy_generation|lang=zh-CN|style=Feynman)导致的[驻点压力损失](@keyword=stagnation_pressure_loss|lang=zh-CN|style=Feynman)

与[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)不同，[驻点压力](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)在不[可逆过程](@keyword=reversible_processes|lang=zh-CN|style=Feynman)中并不守恒。根据热力学第二定律，任何真实的绝热过程都必然伴随着熵的增加（$s_2 \gt s_1$）。驻点压力的变化与熵的产生直接相关。我们可以通过理想气体的吉布斯关系式来揭示这一联系。对于两个状态之间的[熵变](@keyword=entropy_change|lang=zh-CN|style=Feynman)，有：

$$ds = c_p \frac{dT}{T} - R \frac{dP}{P}$$

我们将此关系应用于两个[驻点](@keyword=stationary_points|lang=zh-CN|style=Feynman)状态 $(P_{01}, T_{01})$ 和 $(P_{02}, T_{02})$。它们之间的熵变 $\Delta s = s_{02} - s_{01}$ 就是流体经历的实际[熵增](@keyword=entropy_generation|lang=zh-CN|style=Feynman)，因为[驻点](@keyword=stationary_points|lang=zh-CN|style=Feynman)熵等于当地熵 ($s_0 = s$)。

$$\Delta s = s_{02} - s_{01} = c_p \ln\left(\frac{T_{02}}{T_{01}}\right) - R \ln\left(\frac{P_{02}}{P_{01}}\right)$$

对于我们正在考虑的[绝热流](@keyword=adiabatic_flow|lang=zh-CN|style=Feynman)动，[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)是守恒的，$T_{01} = T_{02}$。因此，上式中的第一项为零，简化为：

$$\Delta s = -R \ln\left(\frac{P_{02}}{P_{01}}\right)$$

这个优雅而深刻的方程，有时被称为**斯托多拉定理**（Stodola's theorem）的变体，它定量地描述了不[可逆性](@keyword=invertibility|lang=zh-CN|style=Feynman)与[驻点压力损失](@keyword=stagnation_pressure_loss|lang=zh-CN|style=Feynman)之间的关系。由于不可逆性导致 $\Delta s > 0$，那么必然有 $\ln(P_{02}/P_{01}) < 0$，即 $P_{02} < P_{01}$。这意味着**任何绝热的不可逆过程都会导致驻点压力的损失**。这种损失不是真正的“[压力损失](@keyword=pressure_loss|lang=zh-CN|style=Feynman)”，而是流动做功能力的损失，是高质量的定向动能转化为低质量的无规分子热运动（表现为[熵增](@keyword=entropy_generation|lang=zh-CN|style=Feynman)）的宏观体现。

解出[压力比](@keyword=pressure_ratio|lang=zh-CN|style=Feynman)，我们得到：

$$\frac{P_{02}}{P_{01}} = \exp\left(-\frac{\Delta s}{R}\right)$$

这个关系明确显示，熵增越大，[驻点压力](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)的衰减越显著 ([@problem_id:1792365])。无论是管道内的摩擦 ([@problem_id:1792374]) 还是激波内的粘性耗散 ([@problem_id:1792397])，这些不可逆因素都会产生熵，从而导致[驻点压力](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)的永久性下降。因此，[驻点压力](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman) $P_0$ 成为衡量流动不可逆损失的一个关键指标。

### 应用与拓展

#### 与[不可压缩流](@keyword=incompressible_flow|lang=zh-CN|style=Feynman)动的联系

当马赫数很低时（通常 $M < 0.3$），[可压缩流](@keyword=compressible_flows|lang=zh-CN|style=Feynman)动的关系式可以简化为我们更熟悉的不可压缩形式。对等熵[驻点压力](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)关系式进行[二项式展开](@keyword=binomial_expansion|lang=zh-CN|style=Feynman)：

$$\frac{P_0}{P} = \left(1 + \frac{\gamma - 1}{2} M^2\right)^{\frac{\gamma}{\gamma-1}} \approx 1 + \frac{\gamma}{\gamma-1} \cdot \frac{\gamma - 1}{2} M^2 + \dots = 1 + \frac{\gamma M^2}{2}$$

因此，$P_0 \approx P + \frac{1}{2} \gamma P M^2$。利用 $a^2 = \gamma P / \rho$，我们得到 $\gamma P = \rho a^2$，代入上式：

$$P_0 \approx P + \frac{1}{2} \rho a^2 M^2 = P + \frac{1}{2} \rho V^2$$

这正是不可压缩流动的**伯努利方程**。这表明伯努利方程是可压缩等熵关系在[低马赫数](@entry_id:751528)下的[渐近近似](@keyword=asymptotic_approximation|lang=zh-CN|style=Feynman)。然而，随着马赫数增加，这种近似的误差会变大。例如，在 $M=0.5$ 时，对于空气（$\gamma=1.4$），不可压缩模型预测的驻点压力与真实的可压缩[驻点压力](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)之比约为 $0.9905$ ([@problem_id:1792324])。这意味着不可压缩模型低估了[驻点压力](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)，但误差尚小。在更高[马赫数](@keyword=mach_number|lang=zh-CN|style=Feynman)下，这种差异将变得非常显著。

#### 多维流动中的[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)梯度：克罗克定理

我们之前的讨论大多基于一维[均匀流](@keyword=uniform_flow|lang=zh-CN|style=Feynman)动的假设，即在流动的[横截面](@keyword=cross_section_2|lang=zh-CN|style=Feynman)上性质是统一的。在更复杂的二维或三维流动中，情况可能有所不同。**克罗克定理**（Crocco's theorem）为我们提供了分析多维流场中[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)变化的有力工具。其一种形式为：

$$\vec{v} \times \vec{\omega} = T \nabla s - \nabla h_0$$

其中 $\vec{v}$ 是[速度矢量](@keyword=velocity_vector|lang=zh-CN|style=Feynman)，$\vec{\omega} = \nabla \times \vec{v}$ 是[涡量矢量](@keyword=vorticity_vector|lang=zh-CN|style=Feynman)，$T$ 是静态温度，$\nabla s$ 和 $\nabla h_0$ 分别是比熵和比[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)的梯度。

这个定理揭示了一个重要事实：在一个[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman)、绝热但存在[涡量](@keyword=vorticity|lang=zh-CN|style=Feynman)和熵梯度的流场中，[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)（或[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)）可能不是[均匀分布](@keyword=equidistribution|lang=zh-CN|style=Feynman)的。一个典型的例子是超声速飞行器前方的弯曲激波。激波的强度沿其[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)变化，导致穿过激波后的不同流线具有不同的[熵增](@keyword=entropy_generation|lang=zh-CN|style=Feynman)。这就在流场中产生了熵梯度（$\nabla s \neq 0$）。同时，弯曲激波也会引入涡量（$\vec{\omega} \neq 0$）。根据克罗克定理，即使整个流动是绝热的（没有外部热量加入），熵梯度和涡量的存在也会导致[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)的梯度（$\nabla h_0 \neq 0$）。这意味着，来自不同位置上游的流线，即使在同一[绝热流](@keyword=adiabatic_flow|lang=zh-CN|style=Feynman)场中，也可能具有不同的[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)。在这种情况下，流动是**等能的**（homoenergetic，即沿一条流线 $h_0$ 守恒），但不是**等焓的**（homoenthalpic，即在整个流场中 $h_0$ 处处相等）。利用克罗克定理，我们可以根据局部测量的流场参数（如速度、涡量、温度和熵梯度）来定量计算[驻点焓](@keyword=stagnation_enthalpy|lang=zh-CN|style=Feynman)的[局部变化率](@keyword=local_rate_of_change|lang=zh-CN|style=Feynman) ([@problem_id:1792328])。

总之，[驻点性质](@keyword=stagnation_properties|lang=zh-CN|style=Feynman)是研究[可压缩流](@keyword=compressible_flows|lang=zh-CN|style=Feynman)动的核心概念。它们不仅简化了[等熵流](@keyword=isentropic_flow|lang=zh-CN|style=Feynman)动的分析，更重要的是，通过[驻点温度](@keyword=stagnation_temperature|lang=zh-CN|style=Feynman)的守恒和驻点压力的损失，深刻地揭示了[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)第一和第二定律在真实[流体流动](@keyword=fluid_flow|lang=zh-CN|style=Feynman)中的作用，为评估和理解[高速流](@keyword=high_speed_flow|lang=zh-CN|style=Feynman)动中的[能量转换](@keyword=energy_transformation|lang=zh-CN|style=Feynman)与不可逆损失提供了坚实的理论基础。