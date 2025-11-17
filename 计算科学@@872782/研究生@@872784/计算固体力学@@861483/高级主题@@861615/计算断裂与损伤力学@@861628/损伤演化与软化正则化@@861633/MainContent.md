## 引言
材料在荷载作用下会产生微观缺陷，这些缺陷的累积与扩展最终导致宏观结构的失效。[连续介质损伤力学](@entry_id:177438)（Continuum Damage Mechanics, CDM）提供了一个强大的理论框架，用于在宏观层面描述这一渐进退化过程。然而，当模拟许多材料（如混凝土、岩石和某些金属）达到强度极限后表现出的[应变软化](@entry_id:755491)行为时，经典的局部损伤模型会遭遇严重的数学与计算难题。

该核心挑战在于，[数值模拟](@entry_id:137087)结果会表现出病态的[网格依赖性](@entry_id:198563)，即计算出的断裂行为和能量耗散随着[有限元网格](@entry_id:174862)的细化而发生非物理性的改变，无法收敛到唯一解。这极大地限制了局部模型在预测结构真实失效行为时的可靠性。本文旨在系统性地阐述并解决这一问题，为读者提供一个从理论基础到前沿应用的完整知识体系。

本文将通过以下三个章节展开：在“原理与机制”中，我们将从[热力学](@entry_id:141121)基础出发，深入剖析[应变软化](@entry_id:755491)导致[不适定性](@entry_id:635673)的根源，并详细介绍为克服此问题而发展的各类[正则化技术](@entry_id:261393)。接着，在“应用与[交叉](@entry_id:147634)学科联系”中，我们将展示这些正则化模型如何应用于模拟复杂的材料行为和[多物理场耦合](@entry_id:171389)问题，连接理论与工程实践。最后，通过“动手实践”中的练习，读者将有机会巩固所学，将理论知识转化为计算能力。

## 原理与机制

本章在前一章介绍[连续介质损伤力学](@entry_id:177438)基本概念的基础上，深入探讨其核心的物理原理和数学机制。我们将从[热力学](@entry_id:141121)第一和第二定律出发，建立[损伤演化](@entry_id:184965)的理论框架。随后，我们将重点分析[材料软化](@entry_id:169591)行为带来的数学和计算挑战，即所谓的“[应变局部化](@entry_id:176973)”和“[网格依赖性](@entry_id:198563)”问题。最后，我们将系统地阐述为解决这些挑战而发展的各类[正则化技术](@entry_id:261393)，包括[裂纹带模型](@entry_id:748032)、[非局部模型](@entry_id:175315)和[梯度增强模型](@entry_id:162584)，并阐明它们各自的内在机理。

### [连续介质损伤力学](@entry_id:177438)的[热力学](@entry_id:141121)基础

[连续介质损伤力学](@entry_id:177438) (Continuum Damage Mechanics, CDM) 将材料内部微观缺陷（如微裂纹、微孔洞）的萌生与扩展过程，在宏观上抽象为一个或多个连续的内部[状态变量](@entry_id:138790)的演化。其中，最简单也最常用的是一个[标量损伤变量](@entry_id:196275) $d$。

**[损伤变量](@entry_id:197066)** $d$ 的取值范围为 $[0, 1]$，其中 $d=0$ 表示材料处于无损的初始状态，而 $d=1$ 则表示材料完全失效，丧失所有承载能力。随着加载的进行，材料的刚度会逐渐退化，这种现象可以通过[损伤变量](@entry_id:197066)来描述。

为了将损伤效应引入[本构关系](@entry_id:186508)，一个核心概念是**有效应力** (effective stress)。其基本思想，即[应变等效](@entry_id:186173)性假设 (hypothesis of strain equivalence)，认为受损材料在应力 $\boldsymbol{\sigma}$ 作用下的应变响应，等同于一个假想的、由同种材料构成的无损体在“有效应力” $\tilde{\boldsymbol{\sigma}}$ 作用下的应变响应。因此，名义柯西应力（即可观测应力）$\boldsymbol{\sigma}$ 与[有效应力](@entry_id:198048) $\tilde{\boldsymbol{\sigma}}$ 之间的关系可以通过[损伤变量](@entry_id:197066) $d$ 来建立。对于[各向同性损伤](@entry_id:750875)，该关系通常表示为：
$$
\boldsymbol{\sigma} = (1-d)\,\tilde{\boldsymbol{\sigma}}
$$
在小应变线弹性框架下，有效应力与[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 遵循[胡克定律](@entry_id:149682)，即 $\tilde{\boldsymbol{\sigma}} = \boldsymbol{C}_0:\boldsymbol{\varepsilon}$，其中 $\boldsymbol{C}_0$ 是材料初始的、无损状态下的[四阶弹性张量](@entry_id:188318)。于是，受损材料的[应力-应变关系](@entry_id:274093)可以写作：
$$
\boldsymbol{\sigma} = (1-d)\,\boldsymbol{C}_0:\boldsymbol{\varepsilon}
$$
这清晰地表明，损伤 $d$ 的累积导致了材料表观刚度的退化。

为了确保本构模型的物理合理性，它必须遵循热力学定律。在[等温过程](@entry_id:143096)中，[热力学第二定律](@entry_id:142732)（以[Clausius-Duhem不等式](@entry_id:193424)形式表达）要求材料内部的[能量耗散](@entry_id:147406)率 $D$ 必须非负。[耗散率](@entry_id:748577)定义为[应力功率](@entry_id:182907)减去[亥姆霍兹自由能](@entry_id:136442)密度 $\psi$ 的变化率：
$$
D = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$
亥姆霍兹自由能密度 $\psi$ 是描述材料储能状态的状态函数，对于损伤材料，它通常是应变 $\boldsymbol{\varepsilon}$ 和[损伤变量](@entry_id:197066) $d$ 的函数，即 $\psi(\boldsymbol{\varepsilon}, d)$。其全[微分形式](@entry_id:146747)为：
$$
\dot{\psi} = \frac{\partial\psi}{\partial\boldsymbol{\varepsilon}}:\dot{\boldsymbol{\varepsilon}} + \frac{\partial\psi}{\partial d}\dot{d}
$$
将此式代入[耗散不等式](@entry_id:188634)，我们得到：
$$
D = \left(\boldsymbol{\sigma} - \frac{\partial\psi}{\partial\boldsymbol{\varepsilon}}\right): \dot{\boldsymbol{\varepsilon}} - \frac{\partial\psi}{\partial d}\dot{d} \ge 0
$$
根据[Coleman-Noll方法](@entry_id:747468)，该不等式必须对任意可能的[热力学过程](@entry_id:141636)（即任意的 $\dot{\boldsymbol{\varepsilon}}$）均成立。为了满足此要求，$\dot{\boldsymbol{\varepsilon}}$ 的系数必须为零，这给出了应力的[状态方程](@entry_id:274378)：
$$
\boldsymbol{\sigma} = \frac{\partial\psi}{\partial\boldsymbol{\varepsilon}}
$$
一个常用的自由能形式是 $\psi(\boldsymbol{\varepsilon}, d) = (1-d)\,\psi_0(\boldsymbol{\varepsilon})$，其中 $\psi_0(\boldsymbol{\varepsilon}) = \frac{1}{2}\boldsymbol{\varepsilon}:\boldsymbol{C}_0:\boldsymbol{\varepsilon}$ 是无损材料的[弹性应变能](@entry_id:202243)密度 [@problem_id:3556726]。基于此形式，我们可以验证 $\frac{\partial\psi}{\partial\boldsymbol{\varepsilon}} = (1-d)\,\boldsymbol{C}_0:\boldsymbol{\varepsilon}$，这与我们之前定义的[应力-应变关系](@entry_id:274093)完全一致，证明了模型的内在[热力学一致性](@entry_id:138886)。

在确定了应力表达式后，[耗散不等式](@entry_id:188634)简化为：
$$
D = - \frac{\partial\psi}{\partial d}\dot{d} \ge 0
$$
我们定义与[损伤变量](@entry_id:197066) $d$ 共轭的[热力学力](@entry_id:161907) $Y$ 为**[损伤能量释放率](@entry_id:195626)** (damage energy release rate)，其定义为：
$$
Y = -\frac{\partial\psi}{\partial d}
$$
于是，耗散率可以简洁地写成 $D = Y\dot{d}$。对于我们选用的自由能形式 $\psi = (1-d)\psi_0(\boldsymbol{\varepsilon})$，[损伤能量释放率](@entry_id:195626) $Y$ 恰好等于无损材料的弹性应变能密度 [@problem_id:3556726] [@problem_id:3556737]：
$$
Y = - \frac{\partial}{\partial d} \left[(1-d)\,\psi_0(\boldsymbol{\varepsilon})\right] = \psi_0(\boldsymbol{\varepsilon}) = \frac{1}{2}\boldsymbol{\varepsilon}:\boldsymbol{C}_0:\boldsymbol{\varepsilon}
$$
由于[弹性张量](@entry_id:170728) $\boldsymbol{C}_0$ 是正定的，所以 $Y$ 总是非负的。因此，为了满足[热力学第二定律](@entry_id:142732) $D = Y\dot{d} \ge 0$，必须施加一个[运动学](@entry_id:173318)约束，即损伤过程是不可逆的：
$$
\dot{d} \ge 0
$$
这个条件意味着一旦材料发生损伤，它就无法自行“愈合”。这构成了[损伤演化](@entry_id:184965)的基本[热力学](@entry_id:141121)框架。

### [损伤演化](@entry_id:184965)律：激活与增长

[热力学](@entry_id:141121)框架提供了[损伤演化](@entry_id:184965)的可能性和约束，但并未指明损伤具体何时发生以及如何增长。一个完整的本构模型必须补充一个**[损伤演化](@entry_id:184965)律**。这通常包括两个部分：一个损伤激活准则和一个损伤增长函数。

#### 损伤激活准则与等效应变

损伤的萌生和发展并非在任何应变状态下都会发生。例如，对于准[脆性](@entry_id:198160)材料（如混凝土或岩石），[拉伸应变](@entry_id:183817)是导致损伤的主要原因，而适度的压缩应变则不会。因此，需要定义一个[标量化](@entry_id:634761)的损伤驱动指标。在应变空间中，这通常通过一个**等效应变** $\varepsilon_{\mathrm{eq}}$ 来实现。

一个适用于拉伸损伤的等效应变 $\varepsilon_{\mathrm{eq}}(\boldsymbol{\varepsilon})$ 必须满足以下关键要求 [@problem_id:3556737]：
1.  **客观性 (Objectivity)**：其值必须独立于观察者的[坐标系](@entry_id:156346)，这意味着它只能是应变张量 $\boldsymbol{\varepsilon}$ 的[不变量](@entry_id:148850)或主值的函数。
2.  **[拉压不对称性](@entry_id:201728) (Tension-Compression Asymmetry)**：对于拉伸损伤，它应仅在材料承受拉伸时被激活。具体而言，当且仅当至少有一个[主应变](@entry_id:197797) $\varepsilon_i$ 为正时，$\varepsilon_{\mathrm{eq}} > 0$；当所有[主应变](@entry_id:197797)为非正（即纯压缩或零应变状态）时，$\varepsilon_{\mathrm{eq}} = 0$。

一些不满足这些条件的例子包括：
-   范数 $\varepsilon_{\mathrm{eq}} = \|\boldsymbol{\varepsilon}\| = (\boldsymbol{\varepsilon}:\boldsymbol{\varepsilon})^{1/2}$：它在纯压缩状态下不为零，会错误地预测压缩下的损伤。
-   体积应变的[绝对值](@entry_id:147688) $\varepsilon_{\mathrm{eq}} = |\text{tr}\boldsymbol{\varepsilon}|$：同样，它在静水压缩状态下也不为零。

相反，满足要求的、常用的等效应变形式包括 [@problem_id:3556737]：
-   **Rankine 型准则**：直接采用最大[主应变](@entry_id:197797)的正部。令 $\varepsilon_{\max} = \max\{\varepsilon_1, \varepsilon_2, \varepsilon_3\}$，并使用Macaulay括号 $\langle x \rangle_+ = \max(x,0)$，则：
    $$
    \varepsilon_{\mathrm{eq}}^{(R)}(\boldsymbol{\varepsilon}) = \langle \varepsilon_{\max} \rangle_+
    $$
-   **Mazars 或修正的 von Mises 型准则**：该准则考虑了所有正[主应变](@entry_id:197797)的贡献，其形式为：
    $$
    \varepsilon_{\mathrm{eq}}^{(M)}(\boldsymbol{\varepsilon}) = \left( \sum_{i=1}^3 \langle \varepsilon_i \rangle_+^2 \right)^{1/2}
    $$
这两种形式都保证了客观性和正确的拉伸激活行为。

#### 损伤增长的率无关模型

一旦选定了等效应变 $\varepsilon_{\mathrm{eq}}$，我们就可以构建一个[损伤演化](@entry_id:184965)的加载函数 $\Phi$。在经典的率无关塑性力学框架中，我们引入一个历史变量 $\kappa$，它记录了材料经历过的最大等效应变。加载函数可以定义为 [@problem_id:3556738]：
$$
\Phi(\varepsilon_{\mathrm{eq}}, \kappa) = \varepsilon_{\mathrm{eq}} - \kappa \le 0
$$
这个函数定义了一个弹性的、无损伤增长的“安全”区域。损伤的演化遵循一套标准的**Kuhn-Tucker加载/卸载条件**：
1.  **容许条件**: $\Phi \le 0$ （当前状态不能超过历史最大加载）。
2.  **不可逆条件**: $\dot{\kappa} \ge 0$ （损伤阈值只能增加或保持不变）。
3.  **[互补条件](@entry_id:747558)**: $\dot{\kappa} \Phi = 0$ （只有当状态处于加载面边界 $\Phi=0$ 时，损伤阈值才可能增长）。

当发生加载（即 $\Phi=0$ 且 $\dot{\varepsilon}_{\mathrm{eq}} > 0$）时，状态点必须维持在加载面上，这意味着加载函数的时间导数必须为零。这就是**[一致性条件](@entry_id:637057)** [@problem_id:3556738]：
$$
\dot{\Phi} = \dot{\varepsilon}_{\mathrm{eq}} - \dot{\kappa} = 0 \quad \implies \quad \dot{\kappa} = \dot{\varepsilon}_{\mathrm{eq}}
$$
该条件确定了在加载过程中历史变量的演化率。最后，[损伤变量](@entry_id:197066) $d$ 本身被定义为历史变量 $\kappa$ 的一个非减函数，例如 $d = f(\kappa)$。这样，通过Kuhn-Tucker条件控制 $\kappa$ 的演化，我们也就间接控制了损伤 $d$ 的增长。

### [应变软化](@entry_id:755491)的挑战：[不适定性](@entry_id:635673)与[网格依赖性](@entry_id:198563)

许多材料（如混凝土、岩石、某些聚合物和金属）在达到其强度极限后，其名义应力会随着应变的增加而减小。这种现象被称为**[应变软化](@entry_id:755491)** (strain softening)，它对应于一个负的[切线](@entry_id:268870)模量 ($d\sigma/d\varepsilon  0$)。虽然这是一种真实的物理现象，但将其纳入经典的（局部的）连续介质模型中会导致严重的数学和计算问题。

当一个包含局部软化本构的有限元模型被求解时，变形会倾向于集中在一个尽可能小的区域内，这种现象称为**[应变局部化](@entry_id:176973)** (strain localization)。在一个一维拉杆的数值模拟中，若采用一阶有限元，这种局部化通常发生在**单个单元**内 [@problem_id:3556759]。这是因为在准静态平衡下，杆件的轴力（从而应力）必须处处相等。一旦进入后峰值软化阶段，系统总势能的降低可以通过将所有后续的变形集中在具有负刚度的最小体积内来实现，而其余部分则[弹性卸载](@entry_id:748863)。

这种数值上的局部化行为直接导致了所谓的**[病态网格依赖性](@entry_id:184469)** (pathological mesh dependency)。问题的核心在于能量耗散。断裂过程是一个耗能过程，描述材料断裂韧性的一个关键物理量是**断裂能** $G_f$，其定义为形成单位面积新裂纹所消耗的能量（单位：J/m²）。在一个数值模型中，总的耗散能量应该是这个物理量的体现。

然而，在局部软化模型中，总耗散能 $\mathcal{E}_{\text{diss}}$ 等于单位体积耗散能 $g_f$（即应力-[应变软化](@entry_id:755491)曲线下的面积）乘以发生局部化的体积 $V_{\text{loc}}$。由于局部化体积被网格尺寸 $h$ 所束缚，即 $V_{\text{loc}} = A \cdot h$（其中 $A$ 是[横截面](@entry_id:154995)积），那么[模拟计算](@entry_id:273038)得到的[断裂能](@entry_id:174458)就是：
$$
\frac{\mathcal{E}_{\text{diss}}}{A} = g_f \cdot h
$$
这意味着，如果我们将应力-[应变软化](@entry_id:755491)曲线视为一个固定的材料属性（即 $g_f$ 是常数），那么计算出的断裂能将与网格尺寸 $h$ 成正比。当网格被细化时（$h \to 0$），计算出的断裂能将虚假地趋向于零 [@problem_id:3556759] [@problem_id:3556732] [@problem_id:3556725]。这意味着在极限情况下，材料的断裂不需要消耗任何能量，这显然是违背物理现实的。

这种病态的[网格依赖性](@entry_id:198563)可以通过一个具体的计算例子清晰地展示出来。假设一个一维杆件，其材料在达到抗拉强度后线性软化。若采用包含10个单元的粗网格进行模拟，计算得到的总耗散能为0.3焦耳；而当改用包含100个单元的细网格时，假定局部化仍然发生于单个单元内，则计算出的总耗散能将锐减至0.03焦耳 [@problem_id:3556795]。这表明，计算结果（无论是总耗散能还是全局的力-位移响应）都无法收敛到一个唯一的、物理上有意义的解。这个问题的根源在于，标准的、局部的连续介质理论缺乏一个内在的**[特征长度](@entry_id:265857)** (characteristic length) 或**[内禀长度尺度](@entry_id:750789)** (internal length scale)。

### 软化模型的[正则化技术](@entry_id:261393)

为了解决局部软化模型的[不适定性](@entry_id:635673)和[网格依赖性](@entry_id:198563)问题，必须对模型进行**正则化** (regularization)。正则化的核心思想是在本构描述中引入一个[内禀长度尺度](@entry_id:750789)，从而使得局部化带的宽度成为一个材料属性，而非网格尺寸的人为产物。这样，计算结果就能在网格细化时收敛，实现所谓的**网格客观性** (mesh objectivity)。

#### 方法一：[裂纹带模型](@entry_id:748032) (Crack Band Model)

[裂纹带模型](@entry_id:748032)是一种实用且直接的[正则化方法](@entry_id:150559)。它不试图改变局部化发生在单个单元内这一事实，而是通过反向调整[本构定律](@entry_id:178936)来补偿网格尺寸的影响，以确保总耗散能的正确性 [@problem_id:3556726] [@problem_id:3556732]。

其核心思想是强行让单位断裂面积上耗散的能量等于材料的断裂能 $G_f$。基于我们之前的推导，这要求满足以下能量等效关系 [@problem_id:3556725]：
$$
G_f = h \cdot \int_{\text{softening}} \sigma(\varepsilon)\,\mathrm{d}\varepsilon
$$
其中 $h$ 是单元的特征长度（在1D情况下即单元长度），积分项是应力-[应变软化](@entry_id:755491)曲线下的面积。这个方程意味着，软化曲线本身不再是一个纯粹的材料属性，而是必须根据其所在的单元尺寸 $h$ 进行调整。

例如，对于一个从峰值应力 $\sigma_u$ 开始线性软化至应力为零的材料，软化曲线下的面积是 $\frac{1}{2}\sigma_u (\varepsilon_f - \varepsilon_0)$，其中 $\varepsilon_f$ 是完全失效时的应变。能量关系变为 $G_f = h \cdot \frac{1}{2}\sigma_u (\varepsilon_f - \varepsilon_0)$。由此可解出最终失效应变 $\varepsilon_f$ 必须依赖于 $h$ [@problem_id:3556726]：
$$
\varepsilon_f = \varepsilon_0 + \frac{2G_f}{h\sigma_u}
$$
同样，对于一个指数软化律 $\sigma(\varepsilon) = f_t \exp(-(\varepsilon - \varepsilon_t)/\varepsilon_0)$，单位体积耗散能为 $f_t \varepsilon_0$。为了保证[能量耗散](@entry_id:147406)正确，软化参数 $\varepsilon_0$ 必须根据单元尺寸 $\Delta$ 进行标定 [@problem_id:3556744]：
$$
\varepsilon_0 = \frac{G_f}{f_t \Delta}
$$
[裂纹带模型](@entry_id:748032)的优点是概念简单、易于在现有的有限元程序中实现。其缺点是，虽然总能量耗散正确，但应变和损伤的[分布](@entry_id:182848)剖面仍然受网格影响，可以说它是“用错误的方式得到了正确的结果”。

#### 方法二：[非局部模型](@entry_id:175315) (Nonlocal Models)

[非局部模型](@entry_id:175315)从更根本的层面引入了长度尺度。其物理思想是：材料在某一点的响应（如[损伤演化](@entry_id:184965)）不仅取决于该点的局部状态，还受到其周围一个有限邻域内状态的加权平均影响。

在**积分型[非局部模型](@entry_id:175315)**中，损伤的驱动力不再是局部等效应变 $\varepsilon_{\text{eq}}(x)$，而是一个非局部等效应变 $\bar{\varepsilon}_{\text{eq}}(x)$。后者通过一个权重函数 $\omega$ 对邻域内的局部应变进行[空间平均](@entry_id:203499)得到 [@problem_id:3556725] [@problem_id:3556804]：
$$
\bar{\varepsilon}_{\text{eq}}(\boldsymbol{x})=\int_{\Omega}\omega(\|\boldsymbol{x}-\boldsymbol{\xi}\|, \ell)\,\varepsilon_{\mathrm{eq}}(\boldsymbol{\xi})\,\mathrm{d}V_{\xi}
$$
权重函数 $\omega$ 通常是一个随距离衰减的函数（如[高斯函数](@entry_id:261394)），其衰减半径由[内禀长度尺度](@entry_id:750789) $\ell$ 控制。为了保证在均匀应变场下非局部值等于局部值，权重函数必须被归一化，即 $\int_{\Omega} \omega\,\mathrm{d}V = 1$ [@problem_id:3556804]。

这种空间平均效应会“模糊”应变场，从而阻止[应变局部化](@entry_id:176973)带收缩到零宽度。最终形成的局部化带宽度将由内禀长度 $\ell$ 控制，而不再是网格尺寸 $h$。只要网格足够精细，能够解析这个由 $\ell$ 决定的损伤剖面（即 $h \lt \ell$），计算结果就能收敛到与网格无关的解 [@problem_id:3556732]。需要注意的是，[非局部模型](@entry_id:175315)本身只保证了网格客观性，为了使总耗散能精确等于材料断裂能 $G_f$，仍然需要对（现在由 $\bar{\varepsilon}_{\text{eq}}$ 驱动的）局部本构软化参数进行一次性的、与网格无关的标定 [@problem_id:3556725]。

#### 方法三：[梯度增强模型](@entry_id:162584) (Gradient-Enhanced Models)

[梯度增强模型](@entry_id:162584)是另一类高级的[正则化方法](@entry_id:150559)。它通过在亥姆霍兹自由能 $\psi$ 中增加一个与[状态变量](@entry_id:138790)空间梯度相关的项，来惩罚状态场的剧烈变化。对于损伤模型，通常是引入[损伤变量](@entry_id:197066)的梯度项 [@problem_id:3556753]：
$$
\psi(\varepsilon, d, \nabla d) = \psi_{\text{local}}(\varepsilon, d) + \frac{1}{2}c\,|\nabla d|^2
$$
其中 $c$ 是一个正的梯度参数。

增加了梯度项后，通过[变分原理](@entry_id:198028)（如[势能](@entry_id:748988)驻值原理）推导出的损伤平衡方程将不再是一个[代数方程](@entry_id:272665)，而是一个[偏微分方程](@entry_id:141332)（PDE）。这个PDE通常被称为“微观力平衡方程” [@problem_id:3556738]，它将某一点的损伤与周围点的损伤耦合起来。

有趣的是，一个[内禀长度尺度](@entry_id:750789)会自然地从该模型的参数中产生。例如，在一个包含梯度项 $\frac{1}{2}k\,(\partial_x d)^2$ 和局部损伤存储项 $\frac{1}{2}h\,d^2$ 的一维模型中，通过对损伤平衡方程进行无量纲化，可以发现一个[特征长度](@entry_id:265857) $\ell$ [@problem_id:3556753]：
$$
\ell = \sqrt{\frac{k}{h}}
$$
这个长度尺度 $\ell$ 控制了损伤[分布](@entry_id:182848)剖面的最小宽度，从而起到了正则化作用，确保了问题的[适定性](@entry_id:148590)和解的网格客观性。

### 总结

本章系统地阐述了材料损伤与软化的核心原理和机制。我们从不[可逆过程](@entry_id:276625)[热力学](@entry_id:141121)出发，建立了描述[损伤演化](@entry_id:184965)的严谨框架，定义了作为损伤驱动力的[能量释放率](@entry_id:158357)。随后，我们揭示了局部软化模型在[数值模拟](@entry_id:137087)中面临的根本困境——由[应变局部化](@entry_id:176973)导致的[病态网格依赖性](@entry_id:184469)，其本质是标准连续介质理论中[内禀长度尺度](@entry_id:750789)的缺失。

为了克服这一挑战，我们探讨了多种[正则化技术](@entry_id:261393)。**[裂纹带模型](@entry_id:748032)**通过调整本构律以匹配网格尺寸，是一种简单实用的工程方法。而**[非局部模型](@entry_id:175315)**和**[梯度增强模型](@entry_id:162584)**则通过在模型中直接引入[内禀长度尺度](@entry_id:750789)，从更根本的层面解决了问题，使得模拟结果能够收敛到物理上唯一的解。这些[正则化方法](@entry_id:150559)是现代[计算固体力学](@entry_id:169583)中模拟[材料失效](@entry_id:160997)不可或缺的关键工具。