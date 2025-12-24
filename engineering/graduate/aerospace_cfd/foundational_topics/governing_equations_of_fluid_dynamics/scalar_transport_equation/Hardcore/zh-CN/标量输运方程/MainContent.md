## 引言
[标量输运](@entry_id:150360)方程是现代计算流体力学（CFD）乃至整个工程科学领域的基石。它以一个统一而优雅的数学形式，描述了从温度、[组分浓度](@entry_id:197022)到[湍动能](@entry_id:262712)等各种标量物理量在流体中的输运过程。无论是在航空发动机燃烧室的复杂化学反应分析，还是在高超声速飞行器的[热防护系统](@entry_id:154016)设计中，深刻理解并熟练运用此方程都是不可或缺的核心能力。然而，许多工程师和研究者往往只停留在对其基本形式的了解，缺乏将其与复杂物理现象和前沿计算方法联系起来的系统性知识。

本文旨在弥合这一知识鸿沟。我们将不再局限于孤立的公式推导，而是将[标量输运](@entry_id:150360)方程置于航空航天工程的宏大背景之下，系统性地构建一个从基本原理到高级应用的完整知识体系。通过以下三个章节的逐步深入，读者将能够建立起坚实的理论基础，并获得解决实际问题的能力：

- **第一章：原理与机制** 将从最基本的守恒定律出发，严谨推导[标量输运](@entry_id:150360)方程，并深入剖析其各项的物理含义、边界[条件设定](@entry_id:273103)，以及在[湍流](@entry_id:151300)和[可压缩流](@entry_id:747589)中的扩展形式。

- **第二章：应用与跨学科交叉** 将展示该方程如何在传热学、燃烧学、[湍流模拟](@entry_id:1133511)等多个交叉学科中发挥关键作用，通过一系列前沿应用案例，揭示其解决复杂工程问题的强大威力。

- **第三章：动手实践** 将通过精心设计的编程与分析练习，引导读者将理论知识转化为实践技能，亲手验证守恒性、分析数值格式，并体验理论模型在实践中的应用。

通过本文的学习，你将不仅掌握[标量输运](@entry_id:150360)方程的数学形式，更能洞悉其背后的物理本质，从而在未来的学术研究与工程实践中游刃有余。

## 原理与机制

本章旨在系统性地阐述[标量输运](@entry_id:150360)的基本物理原理和数学描述。我们将从最基本的守恒定律出发，推导普适的[标量输运](@entry_id:150360)方程，并深入探讨其在[航空航天计算流体力学](@entry_id:746330)（CFD）背景下的具体应用和扩展，包括源项的物理建模、边界条件的设定，以及在[湍流](@entry_id:151300)和可压缩流中的处理方式。

### [标量输运](@entry_id:150360)的基本守恒律

在连续介质力学中，任何一个[守恒量](@entry_id:161475)的变化都遵循一个普适的平衡法则：在一个给定体积内，该量的总变化率等于通过体积边界的净通量，加上体积内部的源或汇。对于一个标量（scalar）属性 $\phi$（例如单位质量的焓、组分质量分数或污染物浓度），我们可以将其应用于一个随时间运动的控制体积 $V(t)$。

一个通用的标量属性 $\phi$ 在流体中的总量 $B$ 可以表示为该标量在控制体积 $V(t)$ 内的积分，其单位体积的量为 $\rho\phi$，其中 $\rho$ 是流体密度。
$$
B(V,t) = \int_{V(t)} \rho \phi \, \mathrm{d}V
$$
该总量的变化率由三个因素决定：穿过控制体积边界 $A(t)$ 的对流通量、[扩散通量](@entry_id:748422)，以及控制体积内部的源项 $S_\phi$。对流是指标量随流体宏观运动的输运，而扩散则是指标量相对于流体运动的输运，通常由浓度梯度等因素驱动。

为了从积分形式的守恒定律推导出适用于计算的[微分形式](@entry_id:146747)，我们应用**[雷诺输运定理](@entry_id:191217)（Reynolds Transport Theorem, RTT）**。该定理将一个随动控制体积中某个属性积分的总时间导数，与一个固定参考系下该属性的[局部时](@entry_id:194383)间导数和通过边界的通量联系起来。

考虑一个边界以速度 $\mathbf{v}_c$ 运动的控制体积，而流体本身的速度为 $\mathbf{u}$。标量属性 $\rho\phi$ 穿过边界的净流出率由两部分组成：相对于运动边界的对流输运 $\rho\phi(\mathbf{u} - \mathbf{v}_c)$，以及[扩散输运](@entry_id:150792) $\mathbf{j}_d$。根据守恒原理，控制体积内属性 $\rho\phi$ 的总变化率等于净流入率加上内部源的生成率。经过严谨的推导 ，我们可以证明，最终得到的局部[微分](@entry_id:158422)方程与控制体积边界的任意运动速度 $\mathbf{v}_c$ 无关。这意味着物理定律在欧拉坐标系下具有唯一的表达形式。

通过应用[高斯散度定理](@entry_id:188065)将面积分转化为[体积分](@entry_id:171119)，并考虑到该定律必须对任意控制体积都成立，我们最终得到[标量输运](@entry_id:150360)方程的**守恒形式（Conservative Form）**：
$$
\frac{\partial (\rho \phi)}{\partial t} + \nabla \cdot (\rho \phi \mathbf{u}) = -\nabla \cdot \mathbf{j}_d + S_{\phi, vol}
$$
其中：
-   $\frac{\partial (\rho \phi)}{\partial t}$ 是**瞬态项（Transient Term）**，表示单位体积[内标](@entry_id:196019)量的[瞬时变化率](@entry_id:141382)。
-   $\nabla \cdot (\rho \phi \mathbf{u})$ 是**对流项（Advection/Convection Term）**，表示由流体宏观运动引起的标量通量的散度。
-   $\mathbf{j}_d$ 是相对于流体运动的**[扩散通量](@entry_id:748422)矢量（Diffusive Flux Vector）**。
-   $S_{\phi, vol}$ 是单位体积的**源项（Source Term）**。

在大多数工程问题中，[扩散通量](@entry_id:748422)遵循**菲克定律（Fick's Law）**，即扩散通量与标量的梯度成正比。对于单位质量的标量 $\phi$，其扩散通量 $\mathbf{j}_d$ 通常写作：
$$
\mathbf{j}_d = -\Gamma_\phi \nabla \phi
$$
这里的 $\Gamma_\phi$ 是扩散系数（diffusivity）。负号表示[扩散过程](@entry_id:268015)总是从高浓度区域流向低浓度区域，即沿着梯度的反方向。将此[本构关系](@entry_id:186508)代入[守恒方程](@entry_id:1122898)，我们得到[标量输运](@entry_id:150360)方程的通用形式：
$$
\frac{\partial (\rho \phi)}{\partial t} + \nabla \cdot (\rho \phi \mathbf{u}) = \nabla \cdot (\Gamma_\phi \nabla \phi) + S_{\phi, vol}
$$

### 通量及其物理诠释

[标量输运](@entry_id:150360)方程的核心在于对通量的理解。总[通量矢量](@entry_id:273577) $\mathbf{F}$ 描述了单位时间内通过单位面积的[标量输运](@entry_id:150360)率，它可以分解为对流通量和[扩散通量](@entry_id:748422)之和 。
$$
\mathbf{F} = \underbrace{\rho \phi \mathbf{u}}_{\text{对流通量}} + \underbrace{(-\Gamma_\phi \nabla \phi)}_{\text{扩散通量}}
$$

-   **对流通量（Advective Flux）** $\rho \phi \mathbf{u}$ 代表标量随流体“搭便车”式的输运。其方向与[流体速度](@entry_id:267320) $\mathbf{u}$ 一致，大小取决于局部流速、密度和标量值。在一个边界上，对流通量的贡献方向由流速的法向分量 $\mathbf{u} \cdot \mathbf{n}$ 决定，其中 $\mathbf{n}$ 是边界的外[法线](@entry_id:167651)方向。

-   **[扩散通量](@entry_id:748422)（Diffusive Flux）** $-\Gamma_\phi \nabla \phi$ 代表由分子或[湍流](@entry_id:151300)涡旋的无规则运动引起的输运，其宏观效果是从高浓度区域向低浓度区域“抹平”差异。该通量的方向总是指向标量 $\phi$ 梯度最陡峭的[下降方向](@entry_id:637058)。例如，在一个边界上，如果标量梯度在[法线](@entry_id:167651)方向上的分量 $\nabla \phi \cdot \mathbf{n} > 0$（意味着 $\phi$ 值在边界外侧更高），那么扩散通量对净流出通量的贡献 $(-\Gamma_\phi \nabla \phi) \cdot \mathbf{n} = -\Gamma_\phi (\nabla \phi \cdot \mathbf{n})$ 必然为负值，代表一个净的流入效应 。

在可变扩散系数 $\Gamma_\phi = \Gamma_\phi(\mathbf{x})$ 的情况下，扩散项的正确形式是 $\nabla \cdot (\Gamma_\phi \nabla \phi)$。使用其他形式，如 $\nabla^2 (\Gamma_\phi \phi)$，会引入非物理性的、由扩散系数梯度驱动的虚假通量，必须避免 。

### [守恒形式](@entry_id:1122899)与[非守恒形式](@entry_id:1128837)

前述推导出的方程被称为[守恒形式](@entry_id:1122899)，因为它直接源于积分守恒定律，其变量是单位体积的标量含量 $\rho\phi$。在CFD中，尤其是在使用[有限体积法](@entry_id:141374)时，这种形式能够确保在离散计算中，流出某个计算单元的通量精确等于流入相邻计算单元的通量，从而保证了标量在整个计算域内的全局守恒。

通过对守恒形式的对流项应用[乘积法则](@entry_id:158393)，并结合[流体动力](@entry_id:750449)学的**连续性方程（Continuity Equation）** $\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0$，我们可以推导出方程的**[非守恒形式](@entry_id:1128837)（Non-Conservative Form）** ：
$$
\rho \left( \frac{\partial \phi}{\partial t} + \mathbf{u} \cdot \nabla \phi \right) = \nabla \cdot (\Gamma_\phi \nabla \phi) + S_{\phi, vol}
$$
括号内的项 $\frac{\partial \phi}{\partial t} + \mathbf{u} \cdot \nabla \phi$ 被定义为标量 $\phi$ 的**[物质导数](@entry_id:262900)（Material Derivative）**，记作 $\frac{D\phi}{Dt}$。它描述了跟随一个流体微团运动时，该微团所携带的标量 $\phi$ 的变化率。因此，[非守恒形式](@entry_id:1128837)可以写为：
$$
\rho \frac{D\phi}{Dt} = \nabla \cdot (\Gamma_\phi \nabla \phi) + S_{\phi, vol}
$$
在连续介质的层面上，只要[连续性方程](@entry_id:195013)成立，守恒与[非守恒形式](@entry_id:1128837)是数学等价的。然而，在数值计算中，特别是对于密度变化剧烈（例如存在激波或化学反应）的航空航天应用，离散的[连续性方程](@entry_id:195013)可能无法被完美满足。在这种情况下，求解[非守恒形式](@entry_id:1128837)会导致虚假的源或汇，破坏标量的全局守恒性。因此，在[变密度流](@entry_id:1133711)的CFD模拟中，**强烈推荐使用[守恒形式](@entry_id:1122899)**，以确保物理量的精确守恒 。

### 源项：物理过程的数学建模

源项 $S$ 是[标量输运](@entry_id:150360)方程中描述特定物理和化学过程的关键。它代表单位体积[内标](@entry_id:196019)量的生成或消耗速率。在[航空航天工程](@entry_id:268503)中，源项可以非常复杂，具体形式取决于所研究的标量 $\phi$。

以一个常见的例子——航空发动机燃烧室中的**比焓（specific enthalpy, $h$）**[输运方程](@entry_id:174281)为例，其源项 $S_h$ 必须包含所有非对流、非传导的能量交换过程 。在忽略机械功和[粘性耗散](@entry_id:143708)的情况下，主要能量源项包括：
-   **化学[反应热](@entry_id:140993)释放**：化学反应中，生成物和反应物的焓值不同，导致能量的释放或吸收。其贡献通常表示为 $S_{chem} = -\sum_{k} h_{k}\omega_{k}$，其中 $h_k$ 是组分 $k$ 的比生成焓，$\omega_k$ 是组分 $k$ 的[质量生成](@entry_id:161427)速率（单位：$\mathrm{kg \cdot m^{-3} \cdot s^{-1}}$）。对于[放热反应](@entry_id:199674)，生成物的[总焓](@entry_id:197863)低于反应物，$\sum h_k \omega_k  0$，因此源项为正，代表能量注入流体。
-   **辐射传热**：高温气体通过电磁波与外界[交换能](@entry_id:137069)量。辐射热流矢量 $\mathbf{q}_{rad}$ 的散度 $\nabla \cdot \mathbf{q}_{rad}$ 代表单位体积净流出的辐射能。因此，其对焓的源项贡献为 $S_{rad} = -\nabla \cdot \mathbf{q}_{rad}$。
-   **外部能量注入**：例如，通过激光或电弧加热流体。这类能量注入通常直接以单位体积的功率 $\dot{q}_{inj}$ (单位：$\mathrm{W \cdot m^{-3}}$) 给出，直接作为正源项。

因此，比焓方程的总源项为：
$$
S_h = -\sum_{k} h_{k}\omega_{k} - \nabla \cdot \mathbf{q}_{rad} + \dot{q}_{inj}
$$
在构建源项时，必须严格确保其量纲与方程中其他项（如 $\frac{\partial (\rho h)}{\partial t}$）一致，即能量/（体积·时间），或功率/体积 。

### [无量纲分析](@entry_id:188181)与[主导平衡](@entry_id:174783)

为了更深刻地理解[输运过程](@entry_id:177992)的物理本质，并对不同机制的重要性进行比较，我们常常对[输运方程](@entry_id:174281)进行无量纲化。这个过程会自然地引出一些关键的[无量纲数](@entry_id:260863)。

#### 佩克莱数（Peclet Number）

考虑一个不可压缩、常扩散系数 $\alpha$ 的流动，其特征速度为 $U$，特征长度为 $L$。通过引入无量纲坐标 $\mathbf{x}^* = \mathbf{x}/L$、时间 $t^* = tU/L$ 和标量 $\phi^* = \phi/\phi_{ref}$，[标量输运](@entry_id:150360)方程可以被改写为 ：
$$
\frac{\partial \phi^*}{\partial t^*} + \mathbf{u}^* \cdot \nabla^* \phi^* = \frac{1}{\mathrm{Pe}} \nabla^{*2} \phi^*
$$
其中，**[佩克莱数](@entry_id:141791)（Peclet Number, $Pe$）** 被定义为：
$$
\mathrm{Pe} = \frac{UL}{\alpha} = \frac{\text{对流输运速率}}{\text{扩散输运速率}}
$$
$Pe$ 数揭示了对流和扩散两种输运机制的相对重要性：
-   当 $Pe \gg 1$ 时，流动由**对流主导**。标量主要沿着[流线](@entry_id:266815)输运，扩散仅在具有大梯度的薄层（如边界层）中才显得重要。此时，方程的[主导平衡](@entry_id:174783)近似为 $\mathbf{u} \cdot \nabla \phi \approx 0$。
-   当 $Pe \ll 1$ 时，流动由**扩散主导**。对流效应可以忽略不计，[标量场](@entry_id:151443)主要由[扩散过程](@entry_id:268015)决定，趋向于均匀化。此时，方程的[主导平衡](@entry_id:174783)近似为[拉普拉斯方程](@entry_id:143689) $\nabla^2 \phi \approx 0$。

通过对流主导情况下的[主导平衡](@entry_id:174783)分析，我们可以估算边界层中扩散层的发展。例如，在流过长度为 $L$ 的平板的流动中，通过平衡流向对流项 ($U\frac{\phi}{L}$) 和横向扩散项 ($\alpha\frac{\phi}{\delta^2}$)，可以估算出在平板末端[扩散层](@entry_id:276329)的厚度 $\delta$ 满足 $\delta \sim \sqrt{\frac{\alpha L}{U}}$ 。

#### 普朗特数与[施密特数](@entry_id:141441)（Prandtl and Schmidt Numbers）

在航空航天应用中，我们不仅关心某个标量的输运，还常常需要同时考虑动量、热量和质量的输运。动量、热量和质量的扩散能力通常是不同的，这些差异由两个重要的[无量纲数](@entry_id:260863)来表征 ：
-   **[普朗特数](@entry_id:143303)（Prandtl Number, $Pr$）**：[动量扩散率](@entry_id:275614)（[运动粘度](@entry_id:275614) $\nu$）与热扩散率 $\alpha$之比。
    $$
    Pr = \frac{\nu}{\alpha}
    $$
-   **施密特数（Schmidt Number, $Sc$）**：[动量扩散率](@entry_id:275614) $\nu$ 与质量扩散率 $D$ 之比。
    $$
    Sc = \frac{\nu}{D}
    $$
这两个数决定了动量边界层（速度发生变化的区域）、热边界层（温度发生变化的区域）和组分边界层（组分浓度发生变化的区域）的相对厚度。对于层流[平板边界层](@entry_id:749449)：
-   当 $Pr, Sc \approx 1$ 时（例如，空气中的热传递），动量、热量和质量的扩散能力相当，导致这三种边界层的厚度大致相同，即 $\delta_v \sim \delta_T \sim \delta_c$。
-   当 $Pr, Sc \gg 1$ 时（例如，液体中的热或[质量传递](@entry_id:151080)），动量的扩散远快于热或质量。热/组分边界层会比动量边界层薄得多。其厚度比满足 $\delta_T/\delta_v \sim Pr^{-1/3}$ 和 $\delta_c/\delta_v \sim Sc^{-1/3}$。
-   当 $Pr, Sc \ll 1$ 时（例如，[液态金属](@entry_id:263875)中的热传递），热或质量的扩散远快于动量。热/组分边界层会比动量边界层厚得多。其厚度比满足 $\delta_T/\delta_v \sim Pr^{-1/2}$ 和 $\delta_c/\delta_v \sim Sc^{-1/2}$。

### 边界条件：封闭问题

[标量输运](@entry_id:150360)方程作为一个[偏微分](@entry_id:194612)方程，其唯一解的确定离不开在计算域边界上施加**边界条件（Boundary Conditions, BCs）**。边界条件必须准确反映边界处的物理现实。在没有穿透的固体壁面（$\mathbf{u} \cdot \mathbf{n} = 0$），[对流通量](@entry_id:158187)为零，边界条件主要通过控制扩散通量来实现。主要有三种类型 ：

1.  **狄利克雷条件（Dirichlet Condition, [第一类边界条件](@entry_id:142800)）**：直接指定边界上标量 $\phi$ 的值。
    $$
    \phi = \phi_w
    $$
    **航空航天示例**：一个在地面热浸泡试验中维持在恒定温度 $T_w$ 的铝制机身蒙皮，其温度边界条件即为 $T=T_w$。在[燃烧模拟](@entry_id:155787)中，喷口处的组分[质量分数](@entry_id:161575)也可以用[狄利克雷条件](@entry_id:137096)指定。

2.  **诺伊曼条件（Neumann Condition, 第二类边界条件）**：指定边界上标量 $\phi$ 的法向梯度，等效于指定法向[扩散通量](@entry_id:748422)。
    $$
    -\Gamma_\phi \frac{\partial \phi}{\partial n} = q_w
    $$
    其中 $\frac{\partial \phi}{\partial n} = \mathbf{n} \cdot \nabla \phi$ 是法向梯度，$q_w$ 是指定的法向通量。一个重要的特例是**绝热（Adiabatic）**或零通量边界，即 $q_w=0$。
    **航空航天示例**：高超声速飞行器前缘使用的[陶瓷](@entry_id:148626)隔热瓦，其设计目标是阻止热量传入内部结构，可以近似为[绝热边界](@entry_id:162724)，即热通量为零 ($\frac{\partial T}{\partial n} = 0$)。

3.  **[罗宾条件](@entry_id:153384)（Robin Condition, 第三类/[混合边界条件](@entry_id:176456)）**：指定边界上标量值与其法向梯度之间的线性关系。
    $$
    -\Gamma_\phi \frac{\partial \phi}{\partial n} = h_c (\phi - \phi_\infty)
    $$
    这种形式通常源于边界内侧的扩散通量与外侧的[对流通量](@entry_id:158187)（或其他输运机制）相平衡。
    **航空航天示例**：一个热的发动机短舱外表面与周围冷空气之间的[对流换热](@entry_id:151349)。壁面的传导热通量等于与外界环境（温度为 $T_\infty$）的[对流换热](@entry_id:151349)量。这里的 $h_c$ 是对流换热系数。

### 对[湍流](@entry_id:151300)和[可压缩流](@entry_id:747589)的扩展

真实航空航天流动往往既是[湍流](@entry_id:151300)又是可压缩的，这要求我们对基本的[标量输运](@entry_id:150360)方程进行扩展。

#### [湍流](@entry_id:151300)中的[标量输运](@entry_id:150360)

在[湍流](@entry_id:151300)中，流场变量在时空上表现出无序的脉动。直接求解这些脉动（DNS）计算成本极高。工程上普遍采用**[雷诺平均](@entry_id:754341)（Reynolds Averaging）**方法，将瞬时量分解为时均值和脉动值，例如 $\phi = \overline{\phi} + \phi'$。对瞬时[输运方程](@entry_id:174281)进行[雷诺平均](@entry_id:754341)后，我们得到**雷诺平均[标量输运](@entry_id:150360)（RAST）方程** ：
$$
\frac{\partial (\rho \overline{\phi})}{\partial t} + \nabla \cdot (\rho \overline{\mathbf{u}} \overline{\phi}) = \nabla \cdot \left( \Gamma_\phi \nabla \overline{\phi} - \rho \overline{\mathbf{u}'\phi'} \right) + \overline{S}_{\phi, vol}
$$
与原始方程相比，出现了一个新的项 $\rho \overline{\mathbf{u}'\phi'}$，称为**[湍流通量](@entry_id:1133513)（Turbulent Flux）**。它表示由速度脉动和标量脉动的相关性引起的额外输运。这个新项是未知的，必须通过一个**湍流模型（Turbulence Model）**来封闭，这就是所谓的**封闭问题（Closure Problem）**。

最常用的封闭方法是**[梯度扩散假说](@entry_id:1125716)（Gradient Diffusion Hypothesis）** ，它假设湍流通量与平均标量的梯度成正比，类似于分子扩散：
$$
-\rho \overline{\mathbf{u}'\phi'} = \rho \alpha_t \nabla \overline{\phi}
$$
这里的 $\alpha_t$ 是**[湍流扩散系数](@entry_id:196515)（Eddy Diffusivity）**。为了确定 $\alpha_t$，我们引入**[湍流施密特数](@entry_id:150226)（Turbulent Schmidt Number, $Sc_t$）**，它将标量的[湍流扩散](@entry_id:1133505)与动量的湍流扩散（即[湍流](@entry_id:151300)粘度 $\nu_t$）联系起来：
$$
Sc_t = \frac{\nu_t}{\alpha_t}
$$
通过一个[湍流模型](@entry_id:190404)（如 $k$-$\epsilon$ 模型）计算出 $\nu_t$ 后，并假设一个合理的 $Sc_t$ 值（通常接近1），就可以得到 $\alpha_t = \nu_t / Sc_t$，从而封闭RAST方程。

#### [可压缩流](@entry_id:747589)中的[标量输运](@entry_id:150360)

在高速流动中，流体密度 $\rho$ 不再是常数，而是与压力和温度相关的变量。这对[标量输运](@entry_id:150360)方程的无量纲化和物理解释产生了影响。

对[可压缩流](@entry_id:747589)的守恒形式[标量输运](@entry_id:150360)方程进行无量纲化，我们发现方程的结构形式与不可压缩情况类似，但所有涉及密度的项现在都变成了无量纲的、可变的密度 $\rho^*$ 。
$$
\frac{\partial}{\partial t^*}\big(\rho^* \phi^*\big) + \nabla^* \cdot \big(\rho^* \mathbf{u}^* \phi^*\big) = \frac{1}{Re \cdot Sc}\nabla^* \cdot \big(\rho^* \nabla^* \phi^*\big) + S^*
$$
这里的 $Re$ 是雷诺数，$Sc$ 是[施密特数](@entry_id:141441)。关键在于，[可压缩性](@entry_id:144559)的影响（通过马赫数 $Ma$ 体现）是如何进入这个方程的。通过[理想气体状态方程](@entry_id:137803) $p=\rho RT$ 的[无量纲化](@entry_id:136704)，可以建立 $\rho^*$ 与 $Ma$ 的关系。对于弱[可压缩流](@entry_id:747589)，一个重要的结论是，密度的相对脉动与[马赫数](@entry_id:274014)的平方成正比 ：
$$
\frac{\rho'}{\rho_\infty} = \mathcal{O}(Ma^2)
$$
这意味着，[马赫数](@entry_id:274014)的影响是通过改变局部密度 $\rho^*$ 隐式地进入到瞬态项、对流项和扩散项中的。这澄清了一个常见的误解，即认为马赫数会作为显式乘数因子出现在方程的某个项中。实际上，可压缩性通过改变密度场来全局性地影响标量的输运过程。