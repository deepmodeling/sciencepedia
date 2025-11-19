## 引言
热力学第一定律，即[能量守恒](@entry_id:140514)定律，是物理学的基石之一。然而，当将其应用于会发生变形、流动和内部能量耗散的连续介质（如金属、聚合物或[地质材料](@entry_id:749838)）时，其表述和应用变得远为复杂。传统的力学和热学分析往往[相互独立](@entry_id:273670)，忽略了两者之间至关重要的相互作用——例如，变形如何[生热](@entry_id:167810)，而温度变化又如何反过来影响材料的力学行为。本文旨在填补这一认知空白，为读者构建一个统一的连续介质[热力学](@entry_id:141121)框架。

通过本文的学习，你将系统地掌握[能量守恒](@entry_id:140514)在宏观连续体中的精确数学表述及其深刻的物理内涵。我们将首先在“原理与机制”一章中，从最基本的积分形式出发，严谨推导出描述任意点物理状态的局部[能量平衡方程](@entry_id:191484)，并揭示[应力功率](@entry_id:182907)和[机械耗散](@entry_id:169843)的本质。接着，在“应用与交叉学科联系”一章中，我们将探讨该定律在解决实际工程与科学问题中的强大威力，从预测塑性变形中的温升，到分析高[应变率](@entry_id:154778)下的[材料失效](@entry_id:160997)，再到其在电磁学和地球物理学中的应用。最后，“动手实践”部分将通过一系列计算练习，巩固你对理论的理解，并培养将理论应用于定量分析的能力。现在，让我们从第一性原理开始，深入探索连续介质中[能量转换](@entry_id:165656)与守恒的奥秘。

## 原理与机制

本章旨在从第一性原理出发，系统地阐述连续介质热力学第一定律。我们将从其最普适的积分形式入手，推导出适用于分析局部物理过程的微分形式。随后，我们将深入剖析[能量平衡方程](@entry_id:191484)中的各个项，特别是[应力功率](@entry_id:182907)和热流的物理意义。最后，我们将探讨力学耗散如何作为内热源，将纯粹的力学理论与热传导理论耦合起来，形成统一的连续介质[热力学](@entry_id:141121)框架，并讨论其在特定工程问题中的应用和简化。

### [能量守恒](@entry_id:140514)的全局表述

热力学第一定律，即[能量守恒](@entry_id:140514)定律，是自然界的基本法则之一。对于一个可变形的连续体，我们可以将其应用于任意一个由相同物质点构成的区域，即**物质体积** $V_m(t)$。该定律的全局（或积分）形式指出，物质体积内总能量（内能与动能之和）的时间变化率，等于作用在该物质体积上的所有外力的总功率与所有热量输入的总速率之和。

总能量 $E$ 是体积[内动能](@entry_id:167806)和内能的积分：
$$
E(t) = \int_{V_m(t)} \rho \left( e + \frac{1}{2} \mathbf{v} \cdot \mathbf{v} \right) dV
$$
其中 $\rho$ 是质量密度，$e$ 是单位质量的内能（比内能），$\mathbf{v}$ 是[速度场](@entry_id:271461)。

总的外界功率输入包含[机械功率](@entry_id:163535) $\dot{W}$ 和热功率 $\dot{Q}$。[机械功率](@entry_id:163535)来源于作用在物质体积边界 $\partial V_m(t)$ 上的[表面力](@entry_id:188034)（柯西牵[引力](@entry_id:175476) $\mathbf{t}$）和作用在体积内部的体力（单位质量的[体力](@entry_id:174230)为 $\mathbf{b}$）。热功率则来源于通过边界的[热传导](@entry_id:147831)（热流矢量 $\mathbf{q}$）和体积内部的热源（单位体积的产热率为 $r$）。它们的表达式为：
$$
\dot{W} = \int_{\partial V_m(t)} \mathbf{t} \cdot \mathbf{v} \, dA + \int_{V_m(t)} \rho \mathbf{b} \cdot \mathbf{v} \, dV
$$
$$
\dot{Q} = -\int_{\partial V_m(t)} \mathbf{q} \cdot \mathbf{n} \, dA + \int_{V_m(t)} r \, dV
$$
注意热流项的负号，这是因为热流矢量 $\mathbf{q}$ 通常定义为指向外部的能量流，而 $\mathbf{n}$ 是边界的外法向单位矢量，因此 $\mathbf{q} \cdot \mathbf{n}$ 代表流出边界的热流。

综合以上各项，热力学第一定律的积分形式可以写作：
$$
\frac{D}{Dt} \int_{V_m(t)} \rho \left( e + \frac{1}{2} \mathbf{v} \cdot \mathbf{v} \right) dV = \int_{\partial V_m(t)} (\mathbf{t} \cdot \mathbf{v} - \mathbf{q} \cdot \mathbf{n}) \, dA + \int_{V_m(t)} (\rho \mathbf{b} \cdot \mathbf{v} + r) \, dV
$$
其中 $\frac{D}{Dt}$ 表示[物质导数](@entry_id:172646)，即跟随物[质点](@entry_id:186768)运动的观察者所测得的变化率。

这个[积分方程](@entry_id:138643)完美地平衡了能量的各种形式——动能、内能、机械功和热能。为了具体理解每个积分项的含义，我们可以考虑一个综合性的思想实验 [@problem_id:2696679]。想象一个长方体，其上给定了一个复杂的[速度场](@entry_id:271461)、边界上的牵[引力](@entry_id:175476)[分布](@entry_id:182848)、[体力](@entry_id:174230)（如重力）、内部体积产热以及边界上的热流交换。要计算该物体总能量的瞬时变化率，我们必须分别计算上述方程右侧的四个积分项：
1.  **[表面力](@entry_id:188034)功率**：$\int_{\partial V_m} \mathbf{t} \cdot \mathbf{v} \, dA$。我们需要在每个受力的边界上，计算牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 和该处速度矢量 $\mathbf{v}$ 的[点积](@entry_id:149019)，然后对整个受力面积分。
2.  **[体力](@entry_id:174230)功率**：$\int_{V_m} \rho \mathbf{b} \cdot \mathbf{v} \, dV$。这需要计算[体力](@entry_id:174230)（如重力 $\rho \mathbf{g}$）和速度场的[点积](@entry_id:149019)，并对整个体积进行积分。
3.  **热源功率**：$\int_{V_m} r \, dV$。这是对所有内部热源（如[化学反应](@entry_id:146973)、电阻加热等）的产热率在整个体积内的积分。
4.  **边界热流功率**：$-\int_{\partial V_m} \mathbf{q} \cdot \mathbf{n} \, dA$。这代表通过所有边界的净热量流入速率。对于[绝热边界](@entry_id:162724)，该项为零；对于给定热流的边界，则直接积分即可。

通过精确计算这四项的代数和，我们就能得到该时刻物体总能量的变化率，而无需知道内部应力、应变或温度场的详细[分布](@entry_id:182848)。

### [能量平衡](@entry_id:150831)的局部形式

虽然全局[能量平衡](@entry_id:150831)对于整个物体是普适的，但为了分析物体内部不同位置的物理过程，我们需要一个局部（或[微分](@entry_id:158718)）形式的[能量平衡方程](@entry_id:191484)。这个方程可以通过将全局积分形式应用于一个无限小的物质体积并利用数学定理来推导。

推导过程的核心步骤如下 [@problem_id:2529335]：
1.  应用**[雷诺输运定理](@entry_id:191217)** (Reynolds Transport Theorem) 将左侧总能量的物质导数转换为对能量密度的积分：
    $$
    \frac{D}{Dt} \int_{V_m(t)} \rho \left( e + \frac{1}{2}\mathbf{v} \cdot \mathbf{v} \right) dV = \int_{V_m(t)} \rho \frac{D}{Dt} \left( e + \frac{1}{2}\mathbf{v} \cdot \mathbf{v} \right) dV
    $$
2.  应用**散度定理** (Divergence Theorem) 将右侧的面积分转换为[体积分](@entry_id:171119)。同时，利用柯西应力关系 $\mathbf{t} = \boldsymbol{\sigma}^{\mathsf{T}} \mathbf{n}$：
    $$
    \int_{\partial V_m(t)} \mathbf{t} \cdot \mathbf{v} \, dA = \int_{V_m(t)} \nabla \cdot (\boldsymbol{\sigma}^{\mathsf{T}} \mathbf{v}) \, dV
    $$
    $$
    \int_{\partial V_m(t)} \mathbf{q} \cdot \mathbf{n} \, dA = \int_{V_m(t)} \nabla \cdot \mathbf{q} \, dV
    $$
3.  将所有项合并到一个[体积分](@entry_id:171119)内。由于该方程对任意物质体积 $V_m(t)$ 都成立，因此被积函数必须恒等于零。这给出了总能量的[局部平衡](@entry_id:156295)方程：
    $$
    \rho \frac{D}{Dt} \left( e + \frac{1}{2}\mathbf{v} \cdot \mathbf{v} \right) = \nabla \cdot (\boldsymbol{\sigma}^{\mathsf{T}} \mathbf{v}) + \rho \mathbf{b} \cdot \mathbf{v} - \nabla \cdot \mathbf{q} + r
    $$
这个方程描述了总能量密度的变化。然而，在大多数情况下，我们更关心内能 $e$ 的变化，因为它与温度和材料的微观结构状态直接相关。为了得到关于 $e$ 的方程，我们需要从上式中减去动能的变化率。

动能的变化率可以通过**[线性动量平衡](@entry_id:193575)方程**（柯西第一运动定律）得到：
$$
\rho \frac{D\mathbf{v}}{Dt} = \nabla \cdot \boldsymbol{\sigma}^{\mathsf{T}} + \rho \mathbf{b}
$$
将此方程与[速度矢量](@entry_id:269648) $\mathbf{v}$ 做[点积](@entry_id:149019)，我们得到动能变化率的表达式：
$$
\rho \frac{D}{Dt} \left( \frac{1}{2}\mathbf{v} \cdot \mathbf{v} \right) = \mathbf{v} \cdot (\nabla \cdot \boldsymbol{\sigma}^{\mathsf{T}} + \rho \mathbf{b})
$$
将总能量方程左侧展开为 $\rho \frac{De}{Dt} + \rho \frac{D}{Dt}(\frac{1}{2}\mathbf{v} \cdot \mathbf{v})$，并将右侧的[应力功率](@entry_id:182907)项 $\nabla \cdot (\boldsymbol{\sigma}^{\mathsf{T}} \mathbf{v})$ 利用[乘法法则](@entry_id:144424)展开为 $(\nabla \cdot \boldsymbol{\sigma}^{\mathsf{T}}) \cdot \mathbf{v} + \boldsymbol{\sigma}^{\mathsf{T}} : \nabla\mathbf{v}$。从总能量方程中减去动能方程后，动能项、体力功率项以及应力散度功率项被完美抵消，最终我们得到了**内能平衡的局部形式**：
$$
\rho \frac{De}{Dt} = \boldsymbol{\sigma}^{\mathsf{T}} : \nabla\mathbf{v} - \nabla \cdot \mathbf{q} + r
$$
这个方程是连续介质[热力学](@entry_id:141121)的核心方程之一。它表明，单位体积内能的增加率等于应力所做的功率（**[应力功率](@entry_id:182907)**），加上由热传导汇入的净热量，再加上内部热源的产热。

### 功率与热量项的分析

现在我们来深入考察内能[平衡方程](@entry_id:172166)右侧的各项。

#### [机械功率](@entry_id:163535)密度（[应力功率](@entry_id:182907)）

[应力功率](@entry_id:182907)项 $\boldsymbol{\sigma}^{\mathsf{T}} : \nabla\mathbf{v}$ 代表了单位体积内，机械功转化为内能的速率。其中 $\nabla\mathbf{v}$ 是[速度梯度张量](@entry_id:270928)，它描述了速度场在空间中的变化。为了更好地理解其物理意义，我们可以将[速度梯度张量](@entry_id:270928)分解为一个对称[部分和](@entry_id:162077)一个反对称部分 [@problem_id:2924997]：
$$
\nabla\mathbf{v} = \boldsymbol{d} + \boldsymbol{w}
$$
其中，
*   $\boldsymbol{d} = \frac{1}{2} \left( \nabla\mathbf{v} + (\nabla\mathbf{v})^{\mathsf{T}} \right)$ 是对称部分，称为**变形率张量** (rate of deformation tensor)。它描述了物质微元的拉伸和剪切变形速率。
*   $\boldsymbol{w} = \frac{1}{2} \left( \nabla\mathbf{v} - (\nabla\mathbf{v})^{\mathsf{T}} \right)$ 是反对称部分，称为**[自旋张量](@entry_id:187346)** (spin tensor)。它描述了物质微元的刚性旋转速率。

因此，[应力功率](@entry_id:182907)可以写作 $\boldsymbol{\sigma}^{\mathsf{T}} : (\boldsymbol{d} + \boldsymbol{w})$。对于经典的（非极性的）连续介质，**[角动量平衡](@entry_id:181848)**要求柯西应力张量 $\boldsymbol{\sigma}$ 是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。一个[对称张量](@entry_id:148092)与一个[反对称张量](@entry_id:199349)的[双点积](@entry_id:748648)恒为零（即 $\boldsymbol{\sigma} : \boldsymbol{w} = 0$）。这意味着[应力功率](@entry_id:182907)可以简化为：
$$
\text{应力功率} = \boldsymbol{\sigma} : \boldsymbol{d}
$$
这个结果具有深刻的物理意义：只有引起[材料变形](@entry_id:169356)的部分（由 $\boldsymbol{d}$ 描述）才会产生[应力功率](@entry_id:182907)，从而改变内能；而材料的刚性旋转（由 $\boldsymbol{w}$ 描述）虽然存在速度，但并不做功。

因此，对于标准的连续介质，内能[平衡方程](@entry_id:172166)的最终形式为：
$$
\rho \frac{De}{Dt} = \boldsymbol{\sigma} : \boldsymbol{d} - \nabla \cdot \mathbf{q} + r
$$

#### 热[功率密度](@entry_id:194407)

热功率项由两部分组成：
*   $-\nabla \cdot \mathbf{q}$：这是热流矢量的散度，代表通过热传导流入单位体积的净热量率。如果一个点的热量流出比流入多（散度为正），则该点会冷却。
*   $r$：这是单位体积的内部热源率，可以是来自[化学反应](@entry_id:146973)、[相变](@entry_id:147324)、[电磁感应](@entry_id:181154)或核反应的能量。

为了封闭方程，我们需要一个关于热流 $\mathbf{q}$ 的[本构关系](@entry_id:186508)。最常见的模型是**[傅里叶热传导定律](@entry_id:138911)** (Fourier's law)，它假设热流与温度梯度成正比：
$$
\mathbf{q} = -k \nabla T
$$
其中 $T$ 是温度场，$k$ 是材料的**热导率** (thermal conductivity)。负号表示热量从高温区流向低温区。

### 耦合与耗散：[热力学](@entry_id:141121)中的热方程

内能平衡方程 $\rho \dot{e} = \boldsymbol{\sigma} : \boldsymbol{d} - \nabla \cdot \mathbf{q} + r$ 构成了力学与热学之间的桥梁。为了得到一个关于温度 $T$ 的演化方程（即热方程），我们需要进一步分解内能 $e$ 和[应力功率](@entry_id:182907) $\boldsymbol{\sigma} : \boldsymbol{d}$。

#### 能量和功的分解

首先，我们将变形率 $\boldsymbol{d}$ 分解为弹性部分 $\boldsymbol{d}^e$ 和非弹性部分 $\boldsymbol{d}^{in}$（例如塑性变形率 $\boldsymbol{d}^p$）：
$$
\boldsymbol{d} = \boldsymbol{d}^e + \boldsymbol{d}^{in}
$$
相应地，[应力功率](@entry_id:182907)也分为两部分：
$$
\boldsymbol{\sigma} : \boldsymbol{d} = \boldsymbol{\sigma} : \boldsymbol{d}^e + \boldsymbol{\sigma} : \boldsymbol{d}^{in}
$$
*   $\boldsymbol{\sigma} : \boldsymbol{d}^e$ 是**弹性功率**，它与可恢复的弹性应变能的变化率相对应。
*   $\boldsymbol{\sigma} : \boldsymbol{d}^{in}$ 是**非弹性功率**或**塑性功率**，它与材料内部不可逆的微观结构变化相关。这部分功大部分会转化为热，是主要的**内耗散源**。

其次，内能 $e$ 的变化也包含多个部分。它可以包括可恢复的弹性应变能、由微观结构缺陷（如[位错](@entry_id:157482)）累积的[储能](@entry_id:264866)（冷作[硬化](@entry_id:177483)能），以及与原子[振动](@entry_id:267781)相关的热能。热能的变化与温度变化直接相关，其变化率通常可以写为 $\dot{e}_{th} = c \dot{T}$，其中 $c$ 是比[热容](@entry_id:137594)。

将这些分解代入内能[平衡方程](@entry_id:172166)，并重新整理，可以分离出纯粹的[热平衡](@entry_id:141693)部分。弹性功率 $\boldsymbol{\sigma} : \boldsymbol{d}^e$ 与[弹性应变能](@entry_id:202243)的变化率相抵消，因为这部分能量是可逆储存和释放的，不直接产生热量。最终，我们得到一个只包含不可逆过程的热方程 [@problem_id:2605827]。

#### [机械耗散](@entry_id:169843)与[泰勒-奎尼系数](@entry_id:202069)

非弹性功率 $\xi = \boldsymbol{\sigma} : \boldsymbol{d}^{in}$ 是不可逆的，根据[热力学第二定律](@entry_id:142732)，它必须是非负的（$\xi \ge 0$）。这部分功不会全部转化为热量。一部分能量会以[位错](@entry_id:157482)、空位等[晶体缺陷](@entry_id:267016)的形式储存在材料的微观结构中，这被称为**储存能** (stored energy of cold work)。只有剩余的部分会以[声子](@entry_id:140728)[振动](@entry_id:267781)的形式释放，即转化为热。

**[泰勒-奎尼系数](@entry_id:202069)** (Taylor-Quinney coefficient) $\beta$ 定义了塑性功中转化为热量的比例，其值通常在 $0.9$ 到 $1.0$ 之间 [@problem_id:2909210]。因此，由[机械耗散](@entry_id:169843)产生的内部热源率为：
$$
\dot{q}_{diss} = \beta \xi = \beta (\boldsymbol{\sigma} : \boldsymbol{d}^{in})
$$
剩余的 $(1-\beta)\xi$ 部分则增加了材料的储存能。需要强调的是，这部分储存能是与微观缺陷相关的不可逆内能增加，而不是可恢复的弹性势能 [@problem_id:2909210]。

#### 通用热方程

综合以上分析，我们可以写出适用于[热塑性](@entry_id:183014)固体的**通用热方程**：
$$
\rho c \dot{T} = -\nabla \cdot \mathbf{q} + \beta (\boldsymbol{\sigma} : \boldsymbol{d}^{p}) + r
$$
将[傅里叶定律](@entry_id:136311) $\mathbf{q} = -k \nabla T$ 代入，得到：
$$
\rho c \dot{T} = \nabla \cdot (k \nabla T) + \beta (\boldsymbol{\sigma} : \boldsymbol{d}^{p}) + r
$$
这个方程是现代[计算固体力学](@entry_id:169583)中求解[热力耦合问题](@entry_id:186655)的基础 [@problem_id:2702531]。它清晰地表明，温度的变化由三个因素驱动：[热传导](@entry_id:147831)、塑性变形[生热](@entry_id:167810)以及外部体积热源。

### 应用与特例

#### 绝热剪切与剪切带

在高[应变率](@entry_id:154778)变形（如冲击、爆炸成型）中，变形发生得非常快，以至于热量来不及通过传导散失。这种情况称为**绝热**条件，即可以忽略热传导项 $\nabla \cdot (k \nabla T)$ [@problem_id:2613664]。此时，热方程简化为：
$$
\rho c \dot{T} = \beta (\boldsymbol{\sigma} : \boldsymbol{d}^{p})
$$
对于[单轴拉伸](@entry_id:188287)或压缩，该方程变为 $\rho c \dot{T} = \beta \sigma \dot{\varepsilon}_p$。这个简单的关系表明，塑性功直接导致材料温度升高。例如，对于在 $300\,\mathrm{MPa}$ 应力下经历 $0.20$ 塑性应变的铜试样，利用此公式可以估算出大约 $16\,\mathrm{K}$ 的温升 [@problem_id:2909210]。

这种自加热效应是**[绝热剪切带](@entry_id:162684)** (adiabatic shear band) 形成的关键机制。在[剪切变形](@entry_id:170920)中，塑性功导致局部温度升高。对于许多金属材料，温度升高会引起**[热软化](@entry_id:187731)** (thermal softening)，即流动应力 $\sigma$ 下降。应力下降使得变形更容易在已经升温的狭窄区域内进行，从而导致更多的塑性功集中于此，产生更多的热量。这种[正反馈](@entry_id:173061)循环最终导致应变高度局部化，形成一个宏观的失效带。

#### 边界条件

一个完整的[热力学](@entry_id:141121)问题不仅需要域内的控制方程，还需要在边界上指定条件。当固体与周围环境通过[对流](@entry_id:141806)和[辐射交换](@entry_id:150522)热量时，边界上的热流平衡要求从内部传导至边界的热流等于通过[对流](@entry_id:141806)和辐射散失到环境中的热流之和 [@problem_id:2702531]。这形成了所谓的**第三类（罗宾）边界条件**：
$$
-\mathbf{n} \cdot (-k \nabla T) = h(T - T_{\infty}) + \varepsilon_{\text{rad}} \sigma_{\text{SB}}(T^4 - T_{\text{sur}}^4)
$$
其中左侧是流出边界的传导热流，右侧第一项是[牛顿冷却定律](@entry_id:142531)描述的[对流](@entry_id:141806)热流（$h$ 为[对流换热系数](@entry_id:151029)，$T_{\infty}$ 为环境流体温度），第二项是斯蒂芬-玻尔兹曼定律描述的净辐射热流（$\varepsilon_{\text{rad}}$ 为表面[发射率](@entry_id:143288)，$\sigma_{\text{SB}}$ 为斯蒂芬-[玻尔兹曼常数](@entry_id:142384)，$T_{\text{sur}}$ 为周围环境的有效辐射温度）。

#### 向标准[热扩散方程](@entry_id:154385)的简化

在许多工程情况下，力学耦合项可以被忽略，从而使复杂的通用[热方程](@entry_id:144435)简化为标准的[热扩散方程](@entry_id:154385)。理解这些简化的假设条件至关重要。

*   **静止刚性固体**：对于一个静止的（$\mathbf{v}=\mathbf{0}$）且不变形的介质，变形率张量 $\boldsymbol{d}$ 为零，因此[应力功率](@entry_id:182907)项 $\boldsymbol{\sigma} : \boldsymbol{d}$ 自然消失。物质导数 $\frac{D}{Dt}$ 简化为[偏导数](@entry_id:146280) $\frac{\partial}{\partial t}$ [@problem_id:2526135]。此时，内能[平衡方程](@entry_id:172166)退化为我们熟悉的热传导方程：
    $$
    \rho c \frac{\partial T}{\partial t} = \nabla \cdot (k \nabla T) + r
    $$
    在这种情况下，物体的总内能变化率可以通过对体积热源的积分和边界热流的面积分来计算，如一个具有给定温度[分布](@entry_id:182848)的杆件所示 [@problem_id:2696680]。

*   **低速、低耗散流动**：对于流体，机械项的忽略则更为微妙。对于低速不可压缩流（马赫数 $Ma \ll 1$），压力功项通常可以忽略。而[粘性耗散](@entry_id:143708)项的重要性则由**埃克特数** ($Ec = U^2 / (c_p \Delta T)$) 来衡量，它比较了流体的宏观动能与热焓的变化。当 $Ec \ll 1$ 时，粘性生热可以忽略不计。因此，在[低马赫数](@entry_id:751528)和低埃克特数的流动中，能量方程可以简化为[对流-扩散方程](@entry_id:144002)，而无需考虑压力功和粘性耗散 [@problem_id:2490691]。需要注意的是，[低雷诺数](@entry_id:204816) ($Re \ll 1$) 并不保证[粘性耗散](@entry_id:143708)可以忽略，特别是在高粘度流体中，粘性生热可能非常显著。

通过本章的学习，我们建立了从最基本定律到具体应用的完整知识链条，为分析和解决复杂的连续介质[热力学](@entry_id:141121)问题奠定了坚实的理论基础。