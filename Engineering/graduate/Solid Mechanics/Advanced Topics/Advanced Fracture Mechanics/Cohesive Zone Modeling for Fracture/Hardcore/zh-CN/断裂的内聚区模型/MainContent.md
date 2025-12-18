## 引言
断裂是工程结构失效的关键模式，但传统[断裂力学](@entry_id:141480)理论在描述[裂纹萌生](@entry_id:748035)和扩展的全过程时面临着根本性挑战。[线性弹性断裂力学](@entry_id:172400)（LEFM）虽然成功预测了裂纹的扩展，但其裂尖[应力奇异性](@entry_id:166362)的假设在物理上不真实，且无法处理裂纹的萌生问题；而传统的强[度理论](@entry_id:636058)则无法解释含裂纹体在远低于材料强度时发生的破坏。为了弥合这一鸿沟，[内聚区模型](@entry_id:194108)（Cohesive Zone Model, CZM）应运而生。CZM通过在[裂纹尖端](@entry_id:182807)引入一个有限强度和能量耗散的“过程区”，用物理上更合理的牵[引力](@entry_id:175476)-分离[本构关系](@entry_id:186508)替代了[应力奇点](@entry_id:166362)，从而为裂纹从萌生到完全分离的整个生命周期提供了统一的理论框架。

本文旨在系统性地介绍[内聚区模型](@entry_id:194108)的理论与实践。在**“原理与机制”一节**中，我们将深入探讨其核心的牵[引力](@entry_id:175476)-分离本构、[运动学分解](@entry_id:751020)和[热力学一致性](@entry_id:138886)，揭示其如何统一强度与能量准则。接着，在**“应用与交叉学科联系”一节**中，我们将展示CZM如何在有限元模拟中实现，如何通过实验标定参数，并探讨其与塑性、动力学等其他物理现象的交叉联系，以及在[复合材料](@entry_id:139856)和[多尺度模拟](@entry_id:752335)中的前沿应用。最后，**“动手实践”部分**将提供一系列精心设计的计算练习，帮助读者将理论知识转化为解决实际问题的能力。

## 原理与机制

在上一章对断裂力学的基本背景进行介绍之后，本章将深入探讨[内聚区模型](@entry_id:194108)（Cohesive Zone Models, CZM）的核心原理与力学机制。[内聚区模型](@entry_id:194108)通过引入一个有限强度和能量耗散的“过程区”来替代[线性弹性断裂力学](@entry_id:172400)（LEFM）中非物理的[应力奇异性](@entry_id:166362)，从而为裂纹的萌生和扩展提供了统一的理论框架。我们将从其核心的本构关系出发，逐步建立起描述界面断裂行为的运动学、[热力学](@entry_id:141121)和能量学基础。

### 基本概念：牵[引力](@entry_id:175476)-分离位移本构

[内聚区模型](@entry_id:194108)的核心在于**牵[引力](@entry_id:175476)-分离位移本构关系（Traction-Separation Law, TSL）**，通常记为 $\mathbf{t}(\boldsymbol{\delta})$。该[本构关系](@entry_id:186508)描述了在潜在或已存的断裂路径上，界面两侧的材料点发生相对位移（即**分离位移** $\boldsymbol{\delta}$）时，界面上传递的**牵[引力](@entry_id:175476)** $\mathbf{t}$ 如何演化。这个[本构关系](@entry_id:186508)从物理上代表了材料在原子或微观尺度上因分离而产生的[内聚力](@entry_id:274824)。

一个典型的牵[引力](@entry_id:175476)-分离位移曲线（以纯I型，即[张开型断裂](@entry_id:195884)为例，此时 $\mathbf{t}$ 和 $\boldsymbol{\delta}$ 均为标量 $T$ 和 $\delta$）具有以下关键特征：

1.  **初始弹性行为**：当分离位移 $\delta$ 很小时，牵[引力](@entry_id:175476) $T$ 随之增大，通常呈线性或[非线性](@entry_id:637147)上升。
2.  **峰值强度（Cohesive Strength）**：牵[引力](@entry_id:175476)达到一个最大值，记为 $\sigma_{\max}$。这个值代表了材料的**[内聚强度](@entry_id:194858)**或**[理论强度](@entry_id:189300)**，是材料在没有宏观缺陷时能够承受的最大名义应力。
3.  **软化行为（Softening）**：当分离位移超过达到峰值强度时的位移后，牵[引力](@entry_id:175476)随着 $\delta$ 的进一步增大而逐渐减小。这个软化过程代表了材料内部键的断裂和损伤的累积。
4.  **完全分离**：当分离位移达到一个临界值 $\delta_c$ 时，牵[引力](@entry_id:175476)减小为零。此时，界面完全断开，形成了两个新的自由表面。

这些参数共同定义了材料的断裂过程。其中，**[断裂能](@entry_id:174458)（Fracture Energy）** $G_c$ 是一个至关重要的宏观参量。它被定义为创建一个单位面积的新裂纹面所消耗的能量。在[内聚区模型](@entry_id:194108)中，这个能量恰好等于将界面从完全粘合状态（$\delta=0$）拉伸至完全分离状态（$\delta=\delta_c$）所做的功。因此，$G_c$ 在数值上等于牵[引力](@entry_id:175476)-分离位移曲线下的面积 ：

$$
G_c = \int_0^{\delta_c} T(\delta) \, d\delta
$$

这个定义的单位是能量/面积（例如 $\mathrm{J/m^2}$），它为 Griffith 的宏观断裂能概念赋予了清晰的物理内涵。

$G_c$ 的物理意义取决于材料的性质。对于理想的**脆性材料**，断裂过程中的[能量耗散](@entry_id:147406)主要用于克服原子间的结[合力](@entry_id:163825)以形成新的表面。在这种情况下，$G_c$ 近似等于两倍的[表面自由能](@entry_id:159200) $2\gamma_s$ 。然而，对于**韧性金属**等材料，断裂能主要由[裂纹尖端塑性区](@entry_id:201396)的巨大塑性变形耗散所主导，其值远大于[表面能](@entry_id:161228)，这也是韧性材料难以断裂的原因。

牵[引力](@entry_id:175476)-分离位移本构可以有多种函数形式，例如线性软化、指数软化、梯形或多项式形式。一个特别简单且具有重要理论价值的是**Dugdale-Barenblatt 模型**，它假设在分离过程中牵[引力](@entry_id:175476)保持一个恒定的值（通常等于材料的屈服强度 $\sigma_y$），直到达到临界分离位移 $\delta_c$。对于这种矩形本构，断裂能的计算非常直接 ：

$$
G_c = \int_0^{\delta_c} \sigma_y \, d\delta = \sigma_y \delta_c
$$

选择何种形式的 TSL 取决于所模拟材料的具体行为和所需的[模型复杂度](@entry_id:145563)。然而，无论具体形式如何，$\sigma_{\max}$、$\delta_c$ 和 $G_c$ 这三个参数（通常只有两个是独立的）共同控制着断裂过程的强度和韧性。

### 内聚界面的[运动学](@entry_id:173318)

为了精确描述内聚界面的行为，我们必须建立一套清晰的[运动学](@entry_id:173318)框架。考虑一个界面将连续体分为“+”和“-”两个部分。界面上任意一点的[位移场](@entry_id:141476)通常是不连续的。

**位移跳跃（Displacement Jump）** $\boldsymbol{\delta}$ 定义为界面两侧位移的差值：

$$
\boldsymbol{\delta} = \llbracket \mathbf{u} \rrbracket = \mathbf{u}^+ - \mathbf{u}^-
$$

其中 $\mathbf{u}^+$ 和 $\mathbf{u}^-$ 分别是界面“+”侧和“-”侧的位移。

为了区分张开和滑移这两种基本的[断裂模式](@entry_id:165801)，我们将位移跳跃向量 $\boldsymbol{\delta}$ 分解为垂直于界面的**法向分量（Normal Component）**和位于界面切平面内的**切向分量（Tangential Component）**。设 $\mathbf{n}$ 为由“-”侧指向“+”侧的[单位法向量](@entry_id:178851)，则：

-   **法向分离位移** $\delta_n$ 是 $\boldsymbol{\delta}$ 在 $\mathbf{n}$ 方向上的投影：
    $$
    \delta_n = \boldsymbol{\delta} \cdot \mathbf{n}
    $$
    $\delta_n > 0$ 表示张开，$\delta_n  0$ 表示压缩或接触。

-   **切向分离位移** $\boldsymbol{\delta}_t$ 是 $\boldsymbol{\delta}$ 在切平面上的投影向量：
    $$
    \boldsymbol{\delta}_t = \boldsymbol{\delta} - \delta_n \mathbf{n}
    $$

这个分解是正交的，即 $\boldsymbol{\delta}_t \cdot \mathbf{n} = 0$。利用投影张量 $\mathbf{P} = \mathbf{I} - \mathbf{n} \otimes \mathbf{n}$（其中 $\mathbf{I}$ 是单位张量），切向分离位移也可以优雅地表示为 $\boldsymbol{\delta}_t = \mathbf{P}\boldsymbol{\delta}$ 。

同样地，界面上的牵[引力](@entry_id:175476)向量 $\mathbf{t}$ 也可以分解为[法向和切向分量](@entry_id:166204)：

-   **法向牵[引力](@entry_id:175476)** $t_n = \mathbf{t} \cdot \mathbf{n}$
-   **切向牵[引力](@entry_id:175476)** $\boldsymbol{\tau} = \mathbf{t} - t_n \mathbf{n}$

**示例**：假设在某点，界[面法向量](@entry_id:749211)为 $\mathbf{n} = (\frac{1}{\sqrt{2}}, 0, \frac{1}{\sqrt{2}})$，位移跳跃为 $\boldsymbol{\delta} = (0.012, -0.005, 0.005)$ m。根据上述定义，我们可以计算出 ：
法向分离 $\delta_n = (0.012) \frac{1}{\sqrt{2}} + (0.005) \frac{1}{\sqrt{2}} = \frac{0.017}{\sqrt{2}}$ m。
切向分离 $\boldsymbol{\delta}_t = \boldsymbol{\delta} - \delta_n \mathbf{n} = (0.012, -0.005, 0.005) - \frac{0.017}{2}(1, 0, 1) = (0.0035, -0.005, -0.0035)$ m。

在分析断裂过程时，一个关键的物理量是单位面积界面上内聚力所做的**功率（Power）**，它等于牵[引力](@entry_id:175476)与分离位移速率的[点积](@entry_id:149019)。利用[正交分解](@entry_id:148020)，这个功率可以表示为法向和切向贡献之和 ：

$$
\mathcal{P} = \mathbf{t} \cdot \dot{\boldsymbol{\delta}} = (t_n \mathbf{n} + \boldsymbol{\tau}) \cdot (\dot{\delta}_n \mathbf{n} + \dot{\boldsymbol{\delta}}_t) = t_n \dot{\delta}_n + \boldsymbol{\tau} \cdot \dot{\boldsymbol{\delta}}_t
$$

这里假设[法向量](@entry_id:264185) $\mathbf{n}$ 不随时间变化。值得注意的是，该功率表达式的值不依赖于法向量 $\mathbf{n}$ 的方向选择（即 $\mathbf{n}$ 或 $-\mathbf{n}$），这是一个物理上必须满足的[自洽性](@entry_id:160889)要求 。

最后，为了确保[本构模型](@entry_id:174726)的**客观性（Objectivity）**或**物质[坐标无关性](@entry_id:159715)（Frame-Indifference）**，即物理定律在刚体运动下保持不变，运动学量的定义必须正确处理旋转。可以证明，如果使用当前构型下的[法向量](@entry_id:264185) $\mathbf{n}$ 来进行投影分解，那么计算出的 $\delta_n$ 和 $\|\boldsymbol{\delta}_t\|$ 都是客观标量。反之，如果使用参考构型中一个固定的法向量进行投影，则模型将失去客观性 。

### 内聚本构的[热力学](@entry_id:141121)框架

一个物理上合理的[内聚本构关系](@entry_id:747464)必须满足热力学定律，特别是热力学第二定律。这为我们构建和检验本构模型提供了严格的指导。对于[等温过程](@entry_id:143096)，[热力学第二定律](@entry_id:142732)（以 Clausius-Duhem 不等式的形式）要求系统的[耗散率](@entry_id:748577)必须非负。对于单位面积的内聚界面，该不等式写作：

$$
\mathcal{D} = \mathbf{t} \cdot \dot{\boldsymbol{\delta}} - \dot{\psi} \ge 0
$$

其中 $\mathcal{D}$ 是耗散率，$\psi$ 是单位面积的 **Helmholtz 自由能**，它代表了界面中储存的可恢复的弹性能。$\psi$ 是状态变量的函数。对于损伤过程，这些[状态变量](@entry_id:138790)通常包括分离位移 $\boldsymbol{\delta}$ 和一个或多个描述材料状态历史的**内禀变量（Internal Variables）**，例如[损伤变量](@entry_id:197066) $d$ 或历史变量 $\alpha$。

根据[链式法则](@entry_id:190743)，$\dot{\psi} = \frac{\partial \psi}{\partial \boldsymbol{\delta}} \cdot \dot{\boldsymbol{\delta}} + \frac{\partial \psi}{\partial \alpha} \dot{\alpha}$。代入[耗散不等式](@entry_id:188634)，得到：

$$
\mathcal{D} = \left( \mathbf{t} - \frac{\partial \psi}{\partial \boldsymbol{\delta}} \right) \cdot \dot{\boldsymbol{\delta}} - \frac{\partial \psi}{\partial \alpha} \dot{\alpha} \ge 0
$$

根据 Coleman-Noll 方法，由于 $\dot{\boldsymbol{\delta}}$ 可以是任意的，其系数必须为零。这给出了牵[引力](@entry_id:175476)的**状态方程（Equation of State）**，即牵[引力](@entry_id:175476)必须是自由能对分离位移的梯度（此即**[超弹性](@entry_id:159356)**关系）：

$$
\mathbf{t} = \frac{\partial \psi}{\partial \boldsymbol{\delta}}
$$

此时，[耗散不等式](@entry_id:188634)简化为**内禀耗散（Intrinsic Dissipation）**：

$$
\mathcal{D}_{\text{int}} = - \frac{\partial \psi}{\partial \alpha} \dot{\alpha} \ge 0
$$

内禀变量 $\alpha$ 通常被定义为单调不减的，以表征损伤的不可逆性，即 $\dot{\alpha} \ge 0$。因此，为满足[耗散不等式](@entry_id:188634)，必须有：

$$
\frac{\partial \psi}{\partial \alpha} \le 0
$$

这个重要的结论意味着：**随着损伤的累积（$\alpha$ 增大），材料储存的自由能必须减小或保持不变**。

让我们通过一个基于**[连续介质损伤力学](@entry_id:177438)**的框架来具体说明这一点 。假设自由能为：

$$
\psi(\boldsymbol{\delta}, d) = \frac{1}{2}(1-d)(\boldsymbol{\delta} \cdot \mathbf{K}_0 \boldsymbol{\delta})
$$

其中 $d \in [0, 1]$ 是一个[标量损伤变量](@entry_id:196275)（$d=0$ 表示无损，$d=1$ 表示完全破坏），$\mathbf{K}_0$ 是初始刚度矩阵。根据[状态方程](@entry_id:274378)，牵[引力](@entry_id:175476)为 $\mathbf{t} = \frac{\partial\psi}{\partial\boldsymbol{\delta}} = (1-d)\mathbf{K}_0\boldsymbol{\delta}$。这表明损伤 $d$ 的作用是降低界面的有效刚度。

该模型的内禀耗散为 $\mathcal{D} = - \frac{\partial\psi}{\partial d} \dot{d} = \frac{1}{2}(\boldsymbol{\delta} \cdot \mathbf{K}_0 \boldsymbol{\delta})\dot{d}$。由于 $\mathbf{K}_0$ 是正定的，括号内的项非负，因此[热力学第二定律](@entry_id:142732)要求 $\dot{d} \ge 0$，即损伤不可逆 。

为了完整地定义模型，还需要一个**[损伤演化](@entry_id:184965)律（Damage Evolution Law）**。这通常通过引入一个历史变量（例如，已经达到过的最大等效分离位移 $\kappa(t) = \max_{s \le t} \delta_{\text{eff}}(s)$）来实现，并令损伤是该历史变量的函数 $d=g(\kappa)$。不可逆性 $\dot{\kappa} \ge 0$ 通过标准的 Kuhn-Tucker [互补条件](@entry_id:747558)来保证 ：

$$
f := \delta_{\text{eff}}(\boldsymbol{\delta}) - \kappa \le 0, \quad \dot{\kappa} \ge 0, \quad f \dot{\kappa} = 0
$$

这些条件确保只有当等效分离位移 $\delta_{\text{eff}}$ 达到或超过历史最大值时，损伤才会进一步发展（此时 $f=0, \dot{\kappa}>0$）。在**卸载（Unloading）**或重加载但未达到历史最大值时（$\delta_{\text{eff}}  \kappa$），$f  0$，因此 $\dot{\kappa}=0$，[损伤变量](@entry_id:197066) $d$ 保持不变。此时，界面表现为弹性行为，其刚度为当前已被削弱的刚度 $(1-d)\mathbf{K}_0$  。

综合这些要素，一个完整且[热力学一致的](@entry_id:755906)[内聚区模型](@entry_id:194108)必须：(i) 满足[能量守恒](@entry_id:140514)（牵[引力](@entry_id:175476)是自由能的梯度）；(ii) 满足[耗散不等式](@entry_id:188634)（自由能随损伤单调不增）；(iii) 包含不可逆的[损伤演化](@entry_id:184965)机制 。

### [混合模式断裂](@entry_id:182261)与压缩的模拟

真实世界的断裂问题很少是纯张开型或纯剪切型，而是两者的结合，即**混合模式（Mixed-Mode）**断裂。为了在[内聚区模型](@entry_id:194108)中处理混合模式加载，需要定义一个**等效分离位移（Effective Separation）** $\delta_{\text{eff}}$，它将法向和切向分离分量组合成一个单一的标量，用于驱动[损伤演化](@entry_id:184965)。

一种广泛采用的等效分离位移形式是  ：

$$
\delta_{\text{eff}} = \sqrt{\langle \delta_n \rangle^2 + \beta \|\boldsymbol{\delta}_t\|^2}
$$

其中 $\beta$ 是一个无量纲的**[模式混合](@entry_id:197206)参数（Mode-Mixity Parameter）**，它调整了切向分离相对于法向分离对损伤贡献的权重。$\beta$ 的取值是一个材料参数，$\beta > 1$ 表示材料对剪切更敏感，这本身并不违反[热力学](@entry_id:141121)限制 。

这个表达式中最值得注意的是对法向分离 $\delta_n$ 使用了**Macaulay 括号** $\langle x \rangle = \max(x, 0)$。其作用是至关重要的：

-   **处理压缩**：当界面处于压缩状态时（$\delta_n  0$），$\langle \delta_n \rangle = 0$。这意味着纯压缩不会产生等效分离位移，因此不会驱动损伤。这符合大多数材料的物理行为，即断裂是由拉伸和剪切而非压缩引起的。

-   **物理真实性**：如果不使用 Macaulay 括号，而是使用 $\delta_n^2$ 或 $|\delta_n|$，那么压缩位移（$\delta_n  0$）将与拉伸位移（$\delta_n > 0$）对损伤产生相同的影响。这在物理上通常是不合理的，因为它意味着压缩可以像拉伸一样“拉开”材料  。

因此，Macaulay 括号的使用是确保模型在压缩下行为正确的关键。然而，这仅仅是处理了损伤的驱动力。当 $\delta_n  0$ 时，材料表面会发生接触，产生抵抗穿透的压缩应力。[内聚区模型](@entry_id:194108)本身（尤其是带有 Macaulay 括号的形式）通常不包含这种压缩响应。因此，在实际的数值模拟中，必须额外引入一个独立的**接触本构（Contact Law）**来处理压缩状态，例如通过罚函数法施加一个大的[接触刚度](@entry_id:181039)来防止负的 $\delta_n$ 变得过大 。

在混合模式下，描述加载状态的另一个重要概念是**[模式混合](@entry_id:197206)角（Mode-Mixity Angle）** $\psi$。然而，它的定义并非唯一。例如，我们可以定义一个基于牵[引力](@entry_id:175476)的混合角和另一个基于能量的混合角 ：

-   **基于牵[引力](@entry_id:175476)的混合角**：$\psi_t = \arctan(t_s / t_n)$
-   **基于能量的混合角**：$\psi_G = \arctan(\sqrt{G_{II} / G_I})$

对于一个线性的内聚本构 $t_n = k_n \delta_n, t_s = k_s \delta_s$，能量分量为 $G_I = t_n^2/(2k_n)$ 和 $G_{II} = t_s^2/(2k_s)$。由此可得 $\sqrt{G_{II}/G_I} = (t_s/t_n) \sqrt{k_n/k_s}$。这表明，只有当法向刚度 $k_n$ 和切向刚度 $k_s$ 相等时，这两个混合角定义才等价。如果 $k_n \neq k_s$，它们将给出不同的值，反映了界面的各向异性响应 。这提醒我们在讨论[模式混合](@entry_id:197206)性时必须明确其定义。

### [内聚区模型](@entry_id:194108)：连接强度与能量准则的桥梁

[线性弹性断裂力学](@entry_id:172400)（LEFM）的成功在于它基于能量准则（$G=G_c$）来预测裂纹的扩展，但其固有的[应力奇异性](@entry_id:166362)使其无法处理裂纹的萌生问题。另一方面，传统的强[度理论](@entry_id:636058)可以预测材料在无缺陷时的失效，但无法解释为何含有裂纹的构件在远低于材料强度的应力下就会破坏。[内聚区模型](@entry_id:194108)通过其独特的物理框架，成功地统一了这两种看似矛盾的准则。

**1. 无缺陷体的断裂萌生：强度控制**

在没有预存裂纹的光滑体中，断裂的萌生由材料的**[内聚强度](@entry_id:194858) $\sigma_{\max}$** 控制。当结构承受的载荷逐渐增大，其内部某一点的应力（或内聚界面上的牵[引力](@entry_id:175476)）首次达到 $\sigma_{\max}$ 时，损伤开始发生，软化过程启动，宏观裂纹开始萌生。这是一个纯粹的**强度判据**。一个简单的单轴受拉杆件模型清晰地揭示了这一点 。

**2. 预存裂纹的扩展：能量控制与[奇点](@entry_id:137764)消除**

对于含有预存裂纹的材料，LEFM 预测裂纹尖端存在 $r^{-1/2}$ 的[应力奇异性](@entry_id:166362)。[内聚区模型](@entry_id:194108)通过在裂纹尖端前方引入一个有限长度的“过程区”来**消除（Regularize）**这个非物理的[奇点](@entry_id:137764)。在这个区域内，牵[引力](@entry_id:175476)被限制在有限的峰值强度 $\sigma_{\max}$ 以下。因此，[裂纹尖端](@entry_id:182807)的应力是有限的 。

当外部载荷作用时，一部分能量被储存在弹性体中，另一部分则在过程区中被耗散。对于准静态扩展的裂纹，裂纹每扩展单位面积，弹性体释放的能量（即**能量释放率 $G$**）必须恰好等于内聚区耗散的能量（即**断裂能 $G_c$**）。这一[能量平衡](@entry_id:150831)条件 $G=G_c$ 与 Griffith 判据在形式上完全一致。通过 J 积分理论可以严格证明，对于一个被弹性材料包围的内聚区，在远场计算的 J 积分值（等于 $G$）等于在内聚区耗散的能量 $G_c$  。

因此，[内聚区模型](@entry_id:194108)巧妙地实现了：近场（过程区内）由强度 $\sigma_{\max}$ 控制应力大小，而远场（弹性区）的响应则由能量 $G_c$ 控制[裂纹扩展](@entry_id:749562)。

**3. [内禀长度尺度](@entry_id:750789)**

连接强度 $\sigma_{\max}$ 和韧性 $G_c$ 的桥梁是一个**[内禀长度尺度](@entry_id:750789)（Intrinsic Length Scale）**，即内聚区的特征长度 $l_{cz}$。我们可以通过[量纲分析](@entry_id:140259)或物理论证来推导其[标度关系](@entry_id:273705)。一方面，断裂能的量级为 $G_c \sim \sigma_{\max} \delta_c$。另一方面，过程区内的应变可以估计为 $\varepsilon \sim \delta_c / l_{cz}$，而应力为 $\sigma \sim \sigma_{\max}$。根据弹性关系 $\sigma = E \varepsilon$，我们有 $\sigma_{\max} \sim E (\delta_c / l_{cz})$。联立这两个关系，消去微观量 $\delta_c$，即可得到内聚区长度的[标度律](@entry_id:139947)  ：

$$
l_{cz} \sim \frac{E G_c}{\sigma_{\max}^2}
$$

其中 $E$ 是[杨氏模量](@entry_id:140430)。这个长度尺度是材料的内禀属性，它决定了断裂行为是更接近脆性还是韧性。如果 $l_{cz}$ 远小于结构的特征尺寸，那么 LEFM 就是一个很好的近似。反之，如果 $l_{cz}$ 与结构尺寸相当，则必须使用[内聚区模型](@entry_id:194108)或[弹塑性断裂力学](@entry_id:166879)进行分析。

对于[平面应变](@entry_id:167046)问题，杨氏模量 $E$ 需要被替换为[平面应变](@entry_id:167046)模量 $E' = E/(1-\nu^2)$，其中 $\nu$ 是泊松比。因此，[平面应变](@entry_id:167046)下的内聚区长度 $l_{cz}^{\text{(plane strain)}}$ 与[平面应力](@entry_id:172193)下的 $l_{cz}^{\text{(plane stress)}}$ 相比，会因为模量的不同而有所差异。它们的比值为 ：

$$
\frac{l_{cz}^{\text{(plane strain)}}}{l_{cz}^{\text{(plane stress)}}} = \frac{E'}{E} = \frac{1}{1-\nu^2}
$$

由于 $\nu > 0$，这个比值总是大于 1，意味着在相同条件下，[平面应变](@entry_id:167046)状态下的内聚区尺寸要大于[平面应力](@entry_id:172193)状态。

综上所述，[内聚区模型](@entry_id:194108)不仅为断裂提供了基于物理的[微观力学](@entry_id:195009)描述，而且成功地将强度和能量这两个[断裂力学](@entry_id:141480)的核心概念统一在一个自洽的理论框架之内，为模拟从萌生到扩展的整个断裂过程提供了强大的工具。