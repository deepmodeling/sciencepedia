## 引言
在[大变形](@entry_id:167243)[连续介质力学](@entry_id:155125)中，如何精确描述物体的内部受力状态是一个核心挑战，与线性弹性理论中单一的应力定义截然不同。当变形巨大时，区分初始的参考构型与变形后的当前构型变得至关重要，这催生了多种应力测度的需求，例如柯西应力(σ)、第一和[第二皮奥拉-基尔霍夫应力](@entry_id:173163)(P, S)以及[基尔霍夫应力](@entry_id:751039)(τ)。本文旨在填补从线性理论到[非线性](@entry_id:637147)理论的认知鸿沟，系统性地解析这些关键[应力量度](@entry_id:198799)。通过阅读本文，您将学习到每种[应力张量](@entry_id:148973)的定义、物理意义、它们之间基于变形梯度的精确转换关系，以及它们在[热力学](@entry_id:141121)和[客观性原理](@entry_id:185412)中的深刻内涵。接下来的章节将引领您深入探索这些概念：“原理与机制”章节将奠定理论基础；“应用与[交叉](@entry_id:147634)学科联系”章节将展示其在计算力学、生物力学等领域的实际应用；最后的“动手实践”章节将通过具体算例巩固您的理解。

## 原理与机制

在研究经历大变形的连续体时，一个核心挑战是如何精确描述其内部的应力状态。在线性弹性理论中，应力与应变之间的关系相对简单，应力张量只有一个明确的定义。然而，当变形不再微小时，物体的构型会发生显著改变。初始构型（或称**参考构型**）与变形后构型（或称**当前构型**）之间的差异变得至关重要。这导致我们需要引入多种[应力量度](@entry_id:198799)，每一种都在特定的构型下定义，并服务于不同的理论和计算目的。本章将系统地阐述这些关键的[应力量度](@entry_id:198799)，包括它们的定义、物理意义、相互之间的转换关系，以及它们在能量原理和客观性原则下的深刻联系。

### 物理应力：柯西[应力张量](@entry_id:148973)

最符合物理直觉的[应力量度](@entry_id:198799)是**柯西[应力张量](@entry_id:148973) (Cauchy stress tensor)**，记为 $\boldsymbol{\sigma}$。它完全在**当前构型** $\mathcal{B}_t$ 中定义，描述了变形后物体内部单位面积上真实的力[分布](@entry_id:182848)。根据柯西应力定理，作用在当前构型中某个面元上的**真实[面力矢量](@entry_id:189429) (true traction vector)** $\boldsymbol{t}$（单位当前面积上的力）与该面元的[单位法向量](@entry_id:178851) $\boldsymbol{n}$ 之间存在线性关系：

$$
\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}
$$

对于经典（非极性）连续介质，动量矩[守恒定律](@entry_id:269268)要求柯西[应力张量](@entry_id:148973)必须是**对称的**，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ [@problem_id:3594868]。

柯西应力张量的优势在于其清晰的物理意义：它直接描述了当前时刻、当前位置的真实应力状态。然而，它的一个主要不便之处在于，其定义域是不断变化的当前构型。在建立本构关系（即材料的[应力-应变关系](@entry_id:274093)）时，我们通常希望将材料属性与一个固定不变的参考构型联系起来。因此，我们需要引入定义在参考构型上的[应力量度](@entry_id:198799)。

### 拉格朗日应力：将视角转回参考构型

为了便于进行本构理论的构建和数值计算，我们需要将应力“[拉回](@entry_id:160816)”到固定不变的**参考构型** $\mathcal{B}_0$ 中进行描述。这种在参考构型中定义的应力统称为拉格朗日应力。其中最核心的是第一和[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量。

#### [第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 (P)

**[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 (First Piola-Kirchhoff stress tensor)**，记为 $\boldsymbol{P}$，通常也被称为**名义应力 (nominal stress)**。它将作用在当前构型上的力与参考构型中的面积联系起来。具体而言，**名义[面力矢量](@entry_id:189429) (nominal traction vector)** $\boldsymbol{t}_0$（单位参考面积上的力）与参考构型中的[单位法向量](@entry_id:178851) $\boldsymbol{N}$ 的关系为：

$$
\boldsymbol{t}_0 = \boldsymbol{P}\boldsymbol{N}
$$

值得注意的是，$\boldsymbol{P}$ 是一个**两点张量 (two-point tensor)**，因为它将一个定义在参考构型中的矢量（法向量 $\boldsymbol{N}$）映射为一个定义在当前构型中的矢量（面力 $\boldsymbol{t}_0$） [@problem_id:3579871]。

$\boldsymbol{P}$ 与 $\boldsymbol{\sigma}$ 之间的关系可以通过力平衡和面积变换推导得出。作用在同一物质面元上的总力是唯一的，即 $d\boldsymbol{f} = \boldsymbol{t} \, \mathrm{d}a = \boldsymbol{t}_0 \, \mathrm{d}A$，其中 $\mathrm{d}a$ 和 $\mathrm{d}A$ 分别是当前和参考构型中的[面积元](@entry_id:263205)。借助联系两个构型下面元[法向量](@entry_id:264185)和面积的**[南森公式](@entry_id:195566) (Nanson's formula)** $\boldsymbol{n} \, \mathrm{d}a = J \boldsymbol{F}^{-T} \boldsymbol{N} \, \mathrm{d}A$，我们可以得到：

$$
\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}
$$

这里，$\boldsymbol{F}$ 是变形梯度，而 $J = \det \boldsymbol{F}$ 是其[行列式](@entry_id:142978)，代表体积变化率。

一个至关重要的特性是，[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 $\boldsymbol{P}$ **通常是非对称的**。对其进行转置可得 $\boldsymbol{P}^T = (J \boldsymbol{\sigma} \boldsymbol{F}^{-T})^T = J (\boldsymbol{F}^{-1}) \boldsymbol{\sigma}^T = J \boldsymbol{F}^{-1} \boldsymbol{\sigma}$。除非变形梯度 $\boldsymbol{F}$ 满足特殊条件，否则 $\boldsymbol{P} \neq \boldsymbol{P}^T$。这种非对称性源于变形本身的旋转分量与应力状态的相互作用，即使柯西应力 $\boldsymbol{\sigma}$ 是对称的 [@problem_id:3594812]。

#### [第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 (S)

为了获得一个完全定义在参考构型上且具有对称性的[应力量度](@entry_id:198799)，我们引入**[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 (Second Piola-Kirchhoff stress tensor)**，记为 $\boldsymbol{S}$。它通过将 $\boldsymbol{P}$ 张量进一步“[拉回](@entry_id:160816)”参考构型来定义：

$$
\boldsymbol{P} = \boldsymbol{F}\boldsymbol{S}
$$

从这个定义出发，$\boldsymbol{S} = \boldsymbol{F}^{-1}\boldsymbol{P}$。将前面 $\boldsymbol{P}$ 与 $\boldsymbol{\sigma}$ 的关系代入，可得 $\boldsymbol{S}$ 与 $\boldsymbol{\sigma}$ 的转换公式：

$$
\boldsymbol{S} = \boldsymbol{F}^{-1} (J \boldsymbol{\sigma} \boldsymbol{F}^{-T}) = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T}
$$

$\boldsymbol{S}$ 的一个关键优势在于其**对称性**。假定 $\boldsymbol{\sigma}$ 是对称的，我们可以验证：

$$
\boldsymbol{S}^T = (J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T})^T = J (\boldsymbol{F}^{-T})^T \boldsymbol{\sigma}^T (\boldsymbol{F}^{-1})^T = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T} = \boldsymbol{S}
$$

因此，$\boldsymbol{S}$ 是一个对称的、纯粹的拉格朗日量度。这一优良性质使其成为构建[超弹性](@entry_id:159356)等材料[本构关系](@entry_id:186508)时的首选[应力量度](@entry_id:198799) [@problem_id:3594868] [@problem_id:3594812]。

### [基尔霍夫应力](@entry_id:751039)张量 ($\tau$)：连接不同构型的桥梁

除了上述三种主要的[应力量度](@entry_id:198799)外，**[基尔霍夫应力](@entry_id:751039)张量 (Kirchhoff stress tensor)** $\boldsymbol{\tau}$ 也是一个在理论分析和计算中非常有用的辅助量。它定义在当前构型中，是柯西应力 $\boldsymbol{\sigma}$ 按体积变化率 $J$ 的加权形式：

$$
\boldsymbol{\tau} = J \boldsymbol{\sigma}
$$

由于 $J$ 是一个标量且 $\boldsymbol{\sigma}$ 是对称的，$\boldsymbol{\tau}$ 显然也是一个对称张量。引入 $\boldsymbol{\tau}$ 的主要动机之一是它可以简化[应力量度](@entry_id:198799)之间的转换关系。特别是 $\boldsymbol{\tau}$ 与 $\boldsymbol{S}$ 之间的关系非常简洁。我们将 $\boldsymbol{\sigma} = \frac{1}{J}\boldsymbol{\tau}$ 代入 $\boldsymbol{S}$ 的表达式中：

$$
\boldsymbol{S} = J \boldsymbol{F}^{-1} \left(\frac{1}{J}\boldsymbol{\tau}\right) \boldsymbol{F}^{-T} = \boldsymbol{F}^{-1} \boldsymbol{\tau} \boldsymbol{F}^{-T}
$$

这个操作被称为将[空间张量](@entry_id:185799) $\boldsymbol{\tau}$ **[拉回](@entry_id:160816) (pull-back)** 到参考构型，得到物质张量 $\boldsymbol{S}$。反之，我们可以将上式重排，得到一个同样简洁的**推前 (push-forward)** 操作：

$$
\boldsymbol{\tau} = \boldsymbol{F} \boldsymbol{S} \boldsymbol{F}^{T}
$$

这个关系式表明，[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}$ 是[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\boldsymbol{S}$ 通过变形梯度 $\boldsymbol{F}$ 的直接[推前映射](@entry_id:160933)。相比之下，$\boldsymbol{\sigma}$ 的推前形式则包含一个 $1/J$ 因子：$\boldsymbol{\sigma} = \frac{1}{J}\boldsymbol{F}\boldsymbol{S}\boldsymbol{F}^T$ [@problem_id:3594885] [@problem_id:3440101]。这种简洁性使得 $\boldsymbol{\tau}$ 在推导和计算中扮演了重要的桥梁角色。

### 变换关系总结与计算示例

为了清晰起见，我们总结一下这四种[应力量度](@entry_id:198799)之间的核心变换关系：

- $\boldsymbol{P} = \boldsymbol{F}\boldsymbol{S}$
- $\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}$
- $\boldsymbol{\sigma} = \frac{1}{J} \boldsymbol{P} \boldsymbol{F}^{T}$
- $\boldsymbol{\tau} = J \boldsymbol{\sigma}$
- $\boldsymbol{\tau} = \boldsymbol{F} \boldsymbol{S} \boldsymbol{F}^{T}$
- $\boldsymbol{\sigma} = \frac{1}{J} \boldsymbol{F} \boldsymbol{S} \boldsymbol{F}^{T}$

为了加深对这些抽象公式的理解，我们来看一个具体的计算示例。假设给定变形梯度 $\boldsymbol{F}$ 和[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\boldsymbol{S}$，我们的目标是计算出柯西应力 $\boldsymbol{\sigma}$ [@problem_id:3594867]。

例如，设
$$
\boldsymbol{F}=\begin{pmatrix}
1.2  & 0.15  & 0.0\\
0.0  & 0.9  & 0.2\\
0.0  & 0.0  & 1.1
\end{pmatrix}, \quad
\boldsymbol{S}=\begin{pmatrix}
200  & 30  & 0\\
30  & 150  & 20\\
0  & 20  & 100
\end{pmatrix} \text{ (MPa)}
$$
计算步骤如下：
1.  **计算体积比 $J$**：由于 $\boldsymbol{F}$ 是[上三角矩阵](@entry_id:150931)，其[行列式](@entry_id:142978)为对角[线元](@entry_id:196833)素之积。
    $J = \det \boldsymbol{F} = 1.2 \times 0.9 \times 1.1 = 1.188$。

2.  **计算[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}$**：使用最简洁的推前公式 $\boldsymbol{\tau} = \boldsymbol{F}\boldsymbol{S}\boldsymbol{F}^T$。
    $$
    \boldsymbol{\tau} = \begin{pmatrix}
    1.2  & 0.15  & 0.0\\
    0.0  & 0.9  & 0.2\\
    0.0  & 0.0  & 1.1
    \end{pmatrix}
    \begin{pmatrix}
    200  & 30  & 0\\
    30  & 150  & 20\\
    0  & 20  & 100
    \end{pmatrix}
    \begin{pmatrix}
    1.2  & 0.0  & 0.0\\
    0.15  & 0.9  & 0.2\\
    0.0  & 0.0  & 1.1
    \end{pmatrix}^T
    =
    \begin{pmatrix}
    302.175  & 53.25  & 3.3\\
    53.25  & 132.7  & 41.8\\
    3.3  & 41.8  & 121
    \end{pmatrix} \text{ (MPa)}
    $$

3.  **计算柯西应力 $\boldsymbol{\sigma}$**：最后，通过定义式 $\boldsymbol{\sigma} = \boldsymbol{\tau}/J$ 得到最终结果。
    $$
    \boldsymbol{\sigma} = \frac{1}{1.188} \boldsymbol{\tau} \approx
    \begin{pmatrix}
    254.36  & 44.82  & 2.78\\
    44.82  & 111.70  & 35.19\\
    2.78  & 35.19  & 101.85
    \end{pmatrix} \text{ (MPa)}
    $$
这个例子清晰地展示了如何利用这些变换关系，从一个在参考构型中定义的、便于进行本构计算的应力（如 $\boldsymbol{S}$），最终得到在当前构型中有明确物理意义的真实应力（$\boldsymbol{\sigma}$）。

### [热力学](@entry_id:141121)基础：[功共轭](@entry_id:194957)关系

[应力量度](@entry_id:198799)之间的关系不仅仅是运动学上的代数变换，其背后有着深刻的[热力学](@entry_id:141121)基础，即**[功共轭](@entry_id:194957) (work conjugacy)** 原理。对于一个纯机械过程，[内力](@entry_id:167605)做功的功率（单位体积的[应力功率](@entry_id:182907)）可以由不同的应力-[应变率](@entry_id:154778)对来表示。

- 在**当前构型**中，单位体积的[应力功率](@entry_id:182907)为 $\mathcal{P}_t = \boldsymbol{\sigma} : \boldsymbol{d}$，其中 $\boldsymbol{d} = \frac{1}{2}(\boldsymbol{l} + \boldsymbol{l}^T)$ 是**变形率张量**（[空间速度梯度](@entry_id:187198) $\boldsymbol{l} = \nabla\boldsymbol{v}$ 的对称部分）。因此，$(\boldsymbol{\sigma}, \boldsymbol{d})$ 构成一个[功共轭](@entry_id:194957)对应力-[应变率](@entry_id:154778)对 [@problem_id:2687724]。

- 在**参考构型**中，单位体积的[应力功率](@entry_id:182907)为 $\mathcal{P}_0 = \boldsymbol{P} : \dot{\boldsymbol{F}}$，其中 $\dot{\boldsymbol{F}}$ 是变形梯度的[物质时间导数](@entry_id:190892)。因此，$(\boldsymbol{P}, \dot{\boldsymbol{F}})$ 是一个[功共轭](@entry_id:194957)对。

- 同样在参考构型中，可以证明存在如下恒等式：
  $$
  \boldsymbol{P} : \dot{\boldsymbol{F}} = \boldsymbol{S} : \dot{\boldsymbol{E}}
  $$
  其中 $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^T\boldsymbol{F} - \boldsymbol{I})$ 是**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)**，$\dot{\boldsymbol{E}}$ 是其[物质时间导数](@entry_id:190892)。这个恒等式表明 $(\boldsymbol{S}, \dot{\boldsymbol{E}})$ 也是一个[功共轭](@entry_id:194957)对 [@problem_id:3606681] [@problem_id:2687724]。

[功共轭](@entry_id:194957)关系为[超弹性材料](@entry_id:190241)的本构理论奠定了基础。对于[超弹性材料](@entry_id:190241)，存在一个**[应变能密度函数](@entry_id:755490)** $\hat{W}$，其[物质时间导数](@entry_id:190892)等于[应力功率](@entry_id:182907)。如果我们选择将应变能表示为 $\boldsymbol{E}$ 的函数，即 $\hat{W} = \hat{W}(\boldsymbol{E})$，那么根据链式法则 $\dot{\hat{W}} = \frac{\partial \hat{W}}{\partial \boldsymbol{E}} : \dot{\boldsymbol{E}}$。将其与[应力功率](@entry_id:182907)表达式 $\mathcal{P}_0 = \boldsymbol{S} : \dot{\boldsymbol{E}}$ 等同，即可导出著名的[超弹性](@entry_id:159356)本构关系：

$$
\boldsymbol{S} = \frac{\partial \hat{W}}{\partial \boldsymbol{E}}
$$

这个关系清晰地表明，对称的[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\boldsymbol{S}$ 是与[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ 自然共轭的[应力量度](@entry_id:198799)。

### [客观性原理](@entry_id:185412)

**物质[坐标系](@entry_id:156346)无关性原理 (principle of material frame indifference)**，或称**[客观性原理](@entry_id:185412) (principle of objectivity)**，要求物理定律（特别是本构关系）不应依赖于观察者。这意味着在本构关系中使用的物理量在刚体运动下应具有明确的、一致的变换规律。

考虑一个叠加在当前构型上的[刚体运动](@entry_id:193355)（旋转和平移）$\boldsymbol{x}^* = \boldsymbol{Q}\boldsymbol{x} + \boldsymbol{c}$，其中 $\boldsymbol{Q}$ 是一个正交[旋转张量](@entry_id:191990)。在此变换下，各[应力量度](@entry_id:198799)的变换规律如下 [@problem_id:3594827]：
- 柯西应力：$\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T$
- [基尔霍夫应力](@entry_id:751039)：$\boldsymbol{\tau}^* = \boldsymbol{Q}\boldsymbol{\tau}\boldsymbol{Q}^T$
- [第一皮奥拉-基尔霍夫应力](@entry_id:163971)：$\boldsymbol{P}^* = \boldsymbol{Q}\boldsymbol{P}$
- [第二皮奥拉-基尔霍夫应力](@entry_id:173163)：$\boldsymbol{S}^* = \boldsymbol{S}$

$\boldsymbol{\sigma}$ 和 $\boldsymbol{\tau}$ 作为[空间张量](@entry_id:185799)，其变换规律符合客观二阶张量的定义。$\boldsymbol{P}$ 作为两点张量，其变换也符合客观性要求。最引人注目的是[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\boldsymbol{S}$ 的**[不变性](@entry_id:140168)**。它不随观察者的旋转而改变。其[功共轭](@entry_id:194957)量——[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ 也具有同样的不变性。正是这种不变性使得 $(\boldsymbol{S}, \boldsymbol{E})$ 成为建立不依赖于观察者的[本构模型](@entry_id:174726)的最理想选择。

### 特例分析：[静水压力](@entry_id:275365)状态

分析一个特殊的应力状态可以为我们提供更深入的洞察。考虑物体处于**静水压力 (hydrostatic pressure)** 状态，此时柯西应力在所有方向上均等，为 $\boldsymbol{\sigma} = -p\boldsymbol{I}$，其中 $p$ 是压力标量 [@problem_id:3594828]。

在这种情况下，我们可以推导出[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\boldsymbol{S}$ 的形式。首先，[基尔霍夫应力](@entry_id:751039)为 $\boldsymbol{\tau} = J\boldsymbol{\sigma} = -pJ\boldsymbol{I}$。然后，通过[拉回](@entry_id:160816)操作：
$$
\boldsymbol{S} = \boldsymbol{F}^{-1} \boldsymbol{\tau} \boldsymbol{F}^{-T} = \boldsymbol{F}^{-1} (-pJ\boldsymbol{I}) \boldsymbol{F}^{-T} = -pJ (\boldsymbol{F}^{-1}\boldsymbol{F}^{-T})
$$
利用[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C} = \boldsymbol{F}^T\boldsymbol{F}$ 的逆 $\boldsymbol{C}^{-1} = \boldsymbol{F}^{-1}\boldsymbol{F}^{-T}$，我们得到一个简洁的结果：
$$
\boldsymbol{S} = -pJ\boldsymbol{C}^{-1}
$$
这个结果揭示了压力 $p$ 的本质。
- 对于**可压缩材料**，压力 $p$ 是一个由变形决定的本构量。它通常是体积变化 $J$ 的函数，即 $p=p(J)$，可以通过[应变能函数](@entry_id:178435)对 $J$ 求导得到。
- 对于**[不可压缩材料](@entry_id:159741)**，体积在运动过程中保持不变，即 $J=1$。这个运动学约束使得压力 $p$ 不再能由变形独立决定，而是变成一个**[拉格朗日乘子](@entry_id:142696)**，其数值取决于边界条件和[平衡方程](@entry_id:172166)，用以维持[不可压缩性约束](@entry_id:750592)。在这种情况下，应力表达式简化为 $\boldsymbol{S} = -p\boldsymbol{C}^{-1}$。

综上所述，柯西应力、第一和[第二皮奥拉-基尔霍夫应力](@entry_id:173163)以及[基尔霍夫应力](@entry_id:751039)，共同构成了一个描述有限变形下应力状态的完备体系。理解它们的定义、物理意义、相互转换以及在能量和[客观性原理](@entry_id:185412)下的角色，是深入学习和应用[非线性](@entry_id:637147)连续介质力学的基石。