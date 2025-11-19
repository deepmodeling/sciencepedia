## 引言
[连续介质损伤力学](@entry_id:177438)（Continuum Damage Mechanics, CDM）是[计算固体力学](@entry_id:169583)中一个强大的理论框架，用于描述和预测材料在载荷作用下因内部微观缺陷（如微裂纹、微孔洞）的萌生与扩展而导致的[力学性能](@entry_id:201145)逐渐退化的过程。与传统的[断裂力学](@entry_id:141480)关注单一宏观裂纹不同，CDM从连续介质的宏观视角出发，通过引入内部[状态变量](@entry_id:138790)来量化弥散在材料内部的损伤，从而能够模拟从刚度下降到最终失效的完整过程。本文旨在系统性地介绍[各向同性损伤模型](@entry_id:198443)这一CDM中最基础且应用广泛的分支，填补从理论基础到计算实践之间的知识鸿沟。

读者将通过本文学习到如何在一个[热力学自洽的](@entry_id:755906)框架下构建损伤模型，并理解不同物理假设（如[应变等效](@entry_id:186173)性与能量等效性）如何导出不同的本构关系。本文将分为三个核心部分：

- **原理与机制**：本章将深入探讨[各向同性损伤模型](@entry_id:198443)的[热力学](@entry_id:141121)基础，推导[本构关系](@entry_id:186508)和[损伤演化](@entry_id:184965)律，并讨论标准模型的局限性，如单边效应和[应变局部化](@entry_id:176973)问题，以及相应的理论扩展。
- **应用与[交叉](@entry_id:147634)学科联系**：本章将展示如何将理论模型应用于实际问题，包括模型参数的标定、高级[本构关系](@entry_id:186508)的构建，以及如何与塑性、化学等[多物理场耦合](@entry_id:171389)，以解决土木、材料及能源工程中的复杂问题。
- **动手实践**：最后，通过一系列精心设计的计算练习，读者将有机会亲手实现损伤模型的数值算法，加深对理论的理解并掌握其在有限元分析中的应用。

现在，让我们从构建[各向同性损伤模型](@entry_id:198443)的核心——其基本原理与[热力学](@entry_id:141121)机制开始。

## 原理与机制

### [热力学](@entry_id:141121)框架

[连续介质损伤力学](@entry_id:177438) (Continuum Damage Mechanics, CDM) 的核心思想是通过引入一个或多个内部状态变量来描述[材料微观结构](@entry_id:198422)的退化。对于[各向同性损伤](@entry_id:750875)，最简单的模型是引入一个[标量损伤变量](@entry_id:196275) $d$，其取值范围通常为 $d \in [0, 1)$。其中 $d=0$ 代表材料处于原始的、无损伤的状态，而 $d \to 1$ 则表示材料完全丧失其承载能力。

为了建立一个[热力学](@entry_id:141121)上自洽的理论，我们从亥姆霍兹自由能密度函数 $\psi$ 出发，它被假设为当前应变状态 $\boldsymbol{\varepsilon}$ 和内部损伤状态 $d$ 的函数，即 $\psi(\boldsymbol{\varepsilon}, d)$。在等温、小应变假设下，Clausius-Duhem 不等式（即热力学第二定律的局部形式）为我们提供了推导[本构关系](@entry_id:186508)的出发点。该不等式要求材料的内耗散率 $\mathcal{D}$ 必须为非负值：
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$
其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\dot{\boldsymbol{\varepsilon}}$ 是应变率张量，$\dot{\psi}$ 是[亥姆霍兹自由能](@entry_id:136442)的时间变化率。

根据链式法则，$\dot{\psi}$ 可以展开为：
$$
\dot{\psi} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} : \dot{\boldsymbol{\varepsilon}} + \frac{\partial \psi}{\partial d} \dot{d}
$$
将此式代入 Clausius-Duhem 不等式，我们得到：
$$
\left( \boldsymbol{\sigma} - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} \right) : \dot{\boldsymbol{\varepsilon}} - \frac{\partial \psi}{\partial d} \dot{d} \ge 0
$$
根据 Coleman-Noll 程序，该不等式必须对任意可能的[热力学过程](@entry_id:141636)（即任意的 $\dot{\boldsymbol{\varepsilon}}$）都成立。为了确保这一点，我们必须要求 $\dot{\boldsymbol{\varepsilon}}$ 的系数为零，这便给出了应力的本构关系：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$
此时，[耗散不等式](@entry_id:188634)简化为：
$$
\mathcal{D} = - \frac{\partial \psi}{\partial d} \dot{d} \ge 0
$$
这个不等式揭示了损伤过程中的[能量耗散](@entry_id:147406)机制。我们定义与[损伤变量](@entry_id:197066) $d$ 共轭的[热力学力](@entry_id:161907)，称为**损伤驱动力**或**[损伤能量释放率](@entry_id:195626)**，记为 $Y$：
$$
Y := -\frac{\partial \psi}{\partial d}
$$
于是，[耗散不等式](@entry_id:188634)最终写为 $\mathcal{D} = Y \dot{d} \ge 0$。由于损伤过程是不可逆的（即微裂纹不会自发愈合），我们有 $\dot{d} \ge 0$。因此，[热力学一致性](@entry_id:138886)要求损伤驱动力必须为非负，即 $Y \ge 0$。这一框架构成了所有损伤模型的基础 [@problem_id:3554737] [@problem_id:3554707]。

### 损伤[本构关系](@entry_id:186508)构建：等效性原理

确定了[热力学](@entry_id:141121)框架后，下一个关键问题是如何具体地构造[亥姆霍兹自由能](@entry_id:136442)函数 $\psi(\boldsymbol{\varepsilon}, d)$。一种有效的方法是基于“等效性原理”，它将受损材料的响应与处于某种“有效”应力或应变状态下的原始（无损）材料的响应联系起来。

首先，我们定义原始材料的自由能密度 $\psi_0(\boldsymbol{\varepsilon}) = \frac{1}{2}\boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon}$，其中 $\mathbb{C}_0$ 是原始的、未损伤的四阶[弹性刚度张量](@entry_id:170728)。基于 Kachanov 提出的[有效应力概念](@entry_id:196960)，名义应力 $\boldsymbol{\sigma}$ 与**[有效应力](@entry_id:198048)** $\tilde{\boldsymbol{\sigma}}$ 之间的关系可以定义为：
$$
\tilde{\boldsymbol{\sigma}} = \frac{\boldsymbol{\sigma}}{1-d}
$$
这个定义直观地反映了由于微缺陷（如孔洞、裂纹）的存在，材料的有效承载面积减小了 $(1-d)$ 倍。基于这个定义，可以提出两种经典的等效性假设 [@problem_id:3554749]。

#### [应变等效](@entry_id:186173)性假设

**[应变等效](@entry_id:186173)性假设** (Hypothesis of Strain Equivalence)，又称[有效应力原理](@entry_id:755871)，主张受损材料在名义应力 $\boldsymbol{\sigma}$ 作用下的应变响应，等同于原始材料在有效应力 $\tilde{\boldsymbol{\sigma}}$ 作用下的应变响应。数学上，这意味着：
$$
\boldsymbol{\varepsilon} = \mathbb{S}_0 : \tilde{\boldsymbol{\sigma}} = \mathbb{S}_0 : \frac{\boldsymbol{\sigma}}{1-d}
$$
其中 $\mathbb{S}_0 = \mathbb{C}_0^{-1}$ 是原始材料的柔度张量。求解上式可得[应力-应变关系](@entry_id:274093)：
$$
\boldsymbol{\sigma} = (1-d) \mathbb{C}_0 : \boldsymbol{\varepsilon}
$$
对该式关于 $\boldsymbol{\varepsilon}$ 积分，我们可以得到相应的[亥姆霍兹自由能](@entry_id:136442)密度：
$$
\psi(\boldsymbol{\varepsilon}, d) = \frac{1}{2} (1-d) \boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon} = (1-d) \psi_0(\boldsymbol{\varepsilon})
$$
这是目前应用最广泛的[各向同性损伤模型](@entry_id:198443)。在此模型下，有效[刚度张量](@entry_id:176588)为 $\mathbb{C}(d) = (1-d)\mathbb{C}_0$。

#### 能量等效性假设

**能量等效性假设** (Hypothesis of Energy Equivalence) 则主张受损材料在名义应力 $\boldsymbol{\sigma}$ 作用下的弹性余能密度，等同于原始材料在有效应力 $\tilde{\boldsymbol{\sigma}}$ 作用下的弹性余能密度。原始材料的余能密度为 $\psi_0^c(\boldsymbol{\sigma}) = \frac{1}{2}\boldsymbol{\sigma} : \mathbb{S}_0 : \boldsymbol{\sigma}$。因此，该假设可以写作：
$$
\psi^c(\boldsymbol{\sigma}, d) = \psi_0^c(\tilde{\boldsymbol{\sigma}}) = \psi_0^c\left(\frac{\boldsymbol{\sigma}}{1-d}\right) = \frac{1}{(1-d)^2} \psi_0^c(\boldsymbol{\sigma})
$$
通过[热力学](@entry_id:141121)关系 $\boldsymbol{\varepsilon} = \frac{\partial \psi^c}{\partial \boldsymbol{\sigma}}$，我们可以得到：
$$
\boldsymbol{\varepsilon} = \frac{1}{(1-d)^2} \mathbb{S}_0 : \boldsymbol{\sigma}
$$
求解上式可得[应力-应变关系](@entry_id:274093)：
$$
\boldsymbol{\sigma} = (1-d)^2 \mathbb{C}_0 : \boldsymbol{\varepsilon}
$$
对应的亥姆霍兹自由能密度为：
$$
\psi(\boldsymbol{\varepsilon}, d) = \frac{1}{2} (1-d)^2 \boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon} = (1-d)^2 \psi_0(\boldsymbol{\varepsilon})
$$
可以看到，这两种不同的物理假设导致了不同的[刚度退化](@entry_id:202277)规律。[应变等效](@entry_id:186173)性使[刚度退化](@entry_id:202277)因子为 $(1-d)$，而能量等效性则为 $(1-d)^2$ [@problem_id:3554749]。在实际应用中，[应变等效](@entry_id:186173)性假设因其简洁性和广泛的实验验证而更为常用。

### [损伤演化](@entry_id:184965)与不[可逆性](@entry_id:143146)

定义了[本构关系](@entry_id:186508)后，我们还需要一个**演化律**来描述[损伤变量](@entry_id:197066) $d$ 如何随加载历史而变化。损伤的增长是由[热力学](@entry_id:141121)驱动力 $Y$ 驱动的，但损伤过程是不可逆的。为了描述这一特性，我们通常引入一个损伤准则，其形式为一个加载函数 $\Phi$：
$$
\Phi(Y, \kappa) = Y - \kappa \le 0
$$
这里，$\kappa$ 是一个内部历史变量，通常代表材料经历过的最大损伤驱动力，即 $\kappa(t) = \max_{s \le t} Y(s)$。$\kappa$ 在物理上定义了当前的损伤阈值。

损伤的演化遵循 [Karush-Kuhn-Tucker](@entry_id:634966) (KKT) 加载/卸载条件：
$$
\Phi \le 0, \quad \dot{\kappa} \ge 0, \quad \Phi \dot{\kappa} = 0
$$
这些条件意味着：
1.  **弹性或卸载状态**：如果 $Y  \kappa$，则 $\Phi  0$。为了满足[互补条件](@entry_id:747558) $\Phi \dot{\kappa} = 0$，必须有 $\dot{\kappa}=0$。这意味着损伤阈值不增长。
2.  **加载状态**：如果 $Y = \kappa$ 且 $\dot{Y} > 0$，则为保持状态始终在损伤面上（即 $\Phi=0$），必须有 $\dot{\Phi} = \dot{Y} - \dot{\kappa} = 0$，因此 $\dot{\kappa} = \dot{Y} > 0$。这意味着损伤阈值随驱动力一起增长。

[损伤变量](@entry_id:197066) $d$ 本身是损伤阈值 $\kappa$ 的函数，即 $d = d(\kappa)$，并且通常假设 $d(\kappa)$ 是一个单调不减函数。因此，损伤率可以写为 $\dot{d} = \frac{\partial d}{\partial \kappa} \dot{\kappa}$。结合 KKT 条件，我们可以看到，只有在加载状态下 ($\dot{\kappa}>0$)，损伤才会增长 ($\dot{d}>0$)。在卸载 (unloading) 或中性加载 (neutral loading) 状态下（例如，当 $\dot{Y} \le 0$ 时），我们有 $\dot{\kappa}=0$，从而 $\dot{d}=0$。这自然地保证了损伤的**不可逆性**：一旦产生，损伤不会因卸载而“愈合” [@problem_id:3554756]。

[损伤演化](@entry_id:184965)函数 $d(\kappa)$ 的具体形式需要通过实验来确定。例如，在一个[单轴拉伸](@entry_id:188287)实验中，我们可以测量材料的[应力-应变曲线](@entry_id:159459)。假设我们采用基于[应变等效](@entry_id:186173)性的模型 $\psi(\epsilon,d)=(1-d)\frac{1}{2}E_{0}\epsilon^{2}$，其给出的应力为 $\sigma = (1-d)E_0\epsilon$。通过将此模型预测的应力与实验测得的应力 $\sigma_{\text{exp}}(\epsilon)$ 进行匹配，我们便可以反解出在加载路径上每一点的损伤值 $d$。如果我们将历史变量 $\kappa$ 定义为加载过程中的最[大应变](@entry_id:751152)（对于单调加载，$\kappa=\epsilon$），我们就可以建立起 $d$ 与 $\kappa$ 之间的函数关系 $d(\kappa)$，从而完成模型的标定 [@problem_id:3554707]。

### 高级各向同性模型：单边效应

标准的[各向同性损伤模型](@entry_id:198443)存在一个显著的局限性：它们预测材料在拉伸和压缩下的[刚度退化](@entry_id:202277)是相同的。然而，对于许多准[脆性](@entry_id:198160)材料（如混凝土、岩石），其损伤主要是由微裂纹的萌生和扩展引起的。在受压时，这些微裂纹会闭合，从而恢复一部分或全部的刚度。这种行为被称为**单边效应** (unilateral effect) 或拉压异性。

为了在[各向同性损伤](@entry_id:750875)框架内描述这种现象，可以对[亥姆霍兹自由能](@entry_id:136442)进行分解。一种常见的方法是利用[应变张量](@entry_id:193332)的谱分解 (spectral decomposition)。[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 可以分解为其正部（拉伸部分）$\boldsymbol{\varepsilon}^+$ 和负部（压缩部分）$\boldsymbol{\varepsilon}^-$：
$$
\boldsymbol{\varepsilon} = \sum_{i=1}^{3} \varepsilon_i \boldsymbol{n}_i \otimes \boldsymbol{n}_i \quad \implies \quad \boldsymbol{\varepsilon}^+ = \sum_{i=1}^{3} \langle \varepsilon_i \rangle_+ \boldsymbol{n}_i \otimes \boldsymbol{n}_i, \quad \boldsymbol{\varepsilon}^- = \sum_{i=1}^{3} \langle \varepsilon_i \rangle_- \boldsymbol{n}_i \otimes \boldsymbol{n}_i
$$
其中 $\varepsilon_i$ 和 $\boldsymbol{n}_i$ 是[主应变](@entry_id:197797)及其方向，$\langle x \rangle_+ = \max(x,0)$ 和 $\langle x \rangle_- = \min(x,0)$ 是麦考利括号。

基于此分解，我们可以构建一个只惩罚[拉伸应变](@entry_id:183817)的[自由能函数](@entry_id:749582)：
$$
\psi(\boldsymbol{\varepsilon}, d) = \psi_0(\boldsymbol{\varepsilon}^-) + (1-d)\psi_0(\boldsymbol{\varepsilon}^+)
$$
其中 $\psi_0(\boldsymbol{\varepsilon}^\pm) = \frac{1}{2} \boldsymbol{\varepsilon}^\pm : \mathbb{C}_0 : \boldsymbol{\varepsilon}^\pm$。由此得到的应力为：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} = \mathbb{C}_0 : \boldsymbol{\varepsilon}^- + (1-d) \mathbb{C}_0 : \boldsymbol{\varepsilon}^+
$$
这个模型巧妙地实现了单边效应 [@problem_id:3554688] [@problem_id:3554756]。
- 在纯压缩状态下（所有[主应变](@entry_id:197797) $\varepsilon_i \le 0$），我们有 $\boldsymbol{\varepsilon}^+ = \mathbf{0}$ 和 $\boldsymbol{\varepsilon}^- = \boldsymbol{\varepsilon}$。此时，应力为 $\boldsymbol{\sigma} = \mathbb{C}_0 : \boldsymbol{\varepsilon}$，与未损伤材料完全相同。这意味着，即使材料之前在拉伸过程中产生了损伤 ($d > 0$)，其在纯压缩下的刚度也完全恢复到初始值。
- 在纯拉伸状态下（所有[主应变](@entry_id:197797) $\varepsilon_i \ge 0$），我们有 $\boldsymbol{\varepsilon}^+ = \boldsymbol{\varepsilon}$ 和 $\boldsymbol{\varepsilon}^- = \mathbf{0}$。此时，应力为 $\boldsymbol{\sigma} = (1-d) \mathbb{C}_0 : \boldsymbol{\varepsilon}$，表现为完全的[刚度退化](@entry_id:202277)。

这种模型的损伤驱动力 $Y = -\partial\psi/\partial d$ 仅与拉伸部分的能量相关，即 $Y = \psi_0(\boldsymbol{\varepsilon}^+)$。这意味着只有[拉伸应变](@entry_id:183817)才能驱动损伤的增长 [@problem_id:3554688]。值得注意的是，由于应变谱分解在[主应变](@entry_id:197797)为零时不可导，这类模型的[切线刚度](@entry_id:166213)在拉压转换点是不连续的，这会给数值计算带来挑战。

### [各向同性损伤模型](@entry_id:198443)的物理诠释

“[各向同性损伤](@entry_id:750875)”这一术语本身是一个宏观唯象的描述。其背后的微观物理图像可以是多种多样的。不同的物理假设会导出宏观上可区分的力学行为。

让我们考虑两种不同的[各向同性损伤](@entry_id:750875)假设 [@problem_id:3554753]：
- **模型 I：标准[各向同性损伤](@entry_id:750875)**。这对应于前述的[应变等效](@entry_id:186173)性原理，即 $\mathbb{C}(d)=(1-d)\mathbb{C}_0$。在这种模型下，材料的体积模量 $K$ 和[剪切模量](@entry_id:167228) $\mu$ 都以相同的比例退化：
  $$
  K(d) = (1-d)K_0, \quad \mu(d) = (1-d)\mu_0
  $$
  一个重要的推论是，材料的[泊松比](@entry_id:158876) $\nu$ 在损伤过程中保持不变，因为 $\nu = \frac{3K-2\mu}{2(3K+\mu)} = \frac{3(1-d)K_0-2(1-d)\mu_0}{2(3(1-d)K_0+(1-d)\mu_0)} = \nu_0$。
- **模型 II：仅剪切退化损伤**。这种模型假设损伤主要影响材料的剪切响应，而对其抵[抗体](@entry_id:146805)积变化的能力没有影响。例如，这可以模拟[多晶体](@entry_id:139228)中沿晶界的滑移或微剪切带的形成。在此模型下，[体积模量](@entry_id:160069)保持不变，而剪切模量退化：
  $$
  K(d) = K_0, \quad \mu(d) = (1-d)\mu_0
  $$
  在这种情况下，材料的[泊松比](@entry_id:158876)会随损伤而变化。当 $d$ 增加时，$\mu(d)$ 减小，$\nu(d) = \frac{3K_0-2(1-d)\mu_0}{2(3K_0+(1-d)\mu_0)}$ 将会趋向于 $0.5$（[不可压缩材料](@entry_id:159741)的泊松比）。

这两种模型虽然都属于“[各向同性损伤](@entry_id:750875)”的范畴，但其物理内涵和宏观响应有显著区别。我们可以通过特定的实验来区分它们：
1.  **[静水压力](@entry_id:275365)实验**：该实验直接测量体积模量 $K$。如果测得的 $K$ 随加载而减小，则支持模型 I；如果 $K$ 保持不变，则支持模型 II。
2.  **[单轴拉伸](@entry_id:188287)实验**：通过同时测量[轴向应变](@entry_id:160811)和[横向应变](@entry_id:157965)，我们可以计算出表观[杨氏模量](@entry_id:140430) $E(d)$ 和泊松比 $\nu(d)$。如果 $\nu(d)$ 保持不变，则支持模型 I；如果 $\nu(d)$ 随损伤增加而增加，则支持模型 II。

因此，选择何种损伤模型不仅是数学上的方便，更应基于对材料损伤微观机制的理解和宏观实验的验证 [@problem_id:3554753]。

### 能量耗散及其与塑性的耦合

在损伤过程中，外力所做的功 $W = \int \boldsymbol{\sigma} : d\boldsymbol{\varepsilon}$ 会被分配到两个部分：一部分以弹性应变能的形式储存在材料中，这部分能量在卸载时可以被恢复；另一部分则由于不可逆的微观结构变化（即损伤的形成）而被耗散掉。根据[热力学第一定律](@entry_id:146485)，对于一个从初始状态加载到最终状态 $(\boldsymbol{\varepsilon}_f, d_f)$ 的过程，我们有：
$$
W = \psi_f + J_d
$$
其中 $\psi_f = \psi(\boldsymbol{\varepsilon}_f, d_f)$ 是最终状态下储存的亥姆霍兹自由能，而 $J_d$ 是损伤耗散 [@problem_id:3554737]。从前面的[热力学](@entry_id:141121)推导可知，损伤耗散的总量等于损伤驱动力 $Y$ 在损伤路径上的积分：
$$
J_d = \int_0^t Y \dot{d} \, dt = \int_0^{d_f} Y(D) \, dD
$$
这个[能量平衡](@entry_id:150831)关系是理解材料[断裂韧性](@entry_id:157609)的基础，因为材料的断裂能本质上就是[损伤演化](@entry_id:184965)至完全失效所耗散的能量。

当损伤与其他不[可逆机](@entry_id:145128)制（如塑性）同时发生时，能量的分配会变得更加复杂。考虑一个[弹塑性](@entry_id:193198)损伤模型，总应变可以分解为弹性部分 $\boldsymbol{\varepsilon}_e$ 和塑性部分 $\boldsymbol{\varepsilon}_p$，即 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_e + \boldsymbol{\varepsilon}_p$。[亥姆霍兹自由能](@entry_id:136442)现在是弹性应变和损伤的函数, $\psi(\boldsymbol{\varepsilon}_e, d)$。此时，总的耗散包含两个来源：
$$
\mathcal{D} = Y \dot{d} + \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}_p \ge 0
$$
在一个完整的加载-卸载循环中，外力所做的功将转化为三部分：循环结束时储存的[弹性应变能](@entry_id:202243)、损伤过程的耗散能、以及塑性变形的耗散能。当材料被完全卸载至零应力状态时，由于塑性应变 $\boldsymbol{\varepsilon}_p$ 是不可恢复的，材料将表现出**残余应变** [@problem_id:3554729]。通过对一个包含损伤和塑性的加载-卸载循环进行细致的能量分析，我们可以量化每个机制对总[能量耗散](@entry_id:147406)的贡献，并预测材料的残余变形，这对于评估结构的长期性能至关重要。

### 局部化模型的失效：[不适定性](@entry_id:635673)与正则化

标准的局部损伤模型在描述[材料软化](@entry_id:169591)（即应力随应变增加而下降的阶段）时会遇到一个根本性的数学难题：**[不适定性](@entry_id:635673)** (ill-posedness)。当材料进入软化阶段时，控制方程的性质会发生改变，导致其解不再唯一，并且对[初始条件](@entry_id:152863)或边界条件的微小扰动极其敏感。

在[数值模拟](@entry_id:137087)中，这种[不适定性](@entry_id:635673)表现为**病态的[网格依赖性](@entry_id:198563)** (pathological mesh dependency)。随着[有限元网格](@entry_id:174862)的细化，应变会倾向于集中在一个宽度趋于零的区域内，这个现象被称为**[应变局部化](@entry_id:176973)** (strain localization)。由于局部损伤模型没有内禀的长度尺度，这个局部化区域的宽度仅由网格尺寸决定。当网格尺寸趋于零时，局部化带宽也趋于零。其灾难性的后果是，结构在失效过程中耗散的总能量也趋于零，因为能量耗散是耗散密度在体积上的积分。这意味着，仅仅通过加密网格，我们就能得到一个看似“更脆”的结构响应，这显然是物理上不正确的 [@problem_id:3554733]。

这个问题的数学根源在于控制方程**椭圆性的丧失** (loss of ellipticity)。对于准静态问题，问题的[适定性](@entry_id:148590)与[声学张量](@entry_id:200089) $\mathbf{Q}(\mathbf{n})$ 的性质密切相关。[声学张量](@entry_id:200089)由[切线刚度](@entry_id:166213)张量 $\mathbb{C}_{\text{tan}} = \frac{\partial \boldsymbol{\sigma}}{\partial \boldsymbol{\varepsilon}}$ 和一个单位[方向向量](@entry_id:169562) $\mathbf{n}$ 定义：
$$
\mathbf{Q}(\mathbf{n}) = \mathbf{n} \cdot \mathbb{C}_{\text{tan}} \cdot \mathbf{n}
$$
强椭圆性条件要求 $\mathbf{Q}(\mathbf{n})$ 对于任意非零向量 $\mathbf{a}$ 和任意单位方向 $\mathbf{n}$ 都是正定的。当材料进入软化阶段时，[切线刚度](@entry_id:166213) $\mathbb{C}_{\text{tan}}$ 不再是正定的，这可能导致存在某个方向 $\mathbf{n}$，使得 $\mathbf{Q}(\mathbf{n})$ 变得奇异，即 $\det(\mathbf{Q}(\mathbf{n}))=0$。这被称为 Hadamard-Rice 局部化准则。一旦该条件满足，应变就可以在该方向 $\mathbf{n}$ 的法平面上发生局部化，而无需应力增量 [@problem_id:3554705] [@problem_id:3554733]。

例如，在一个简单的平面应力[单轴拉伸](@entry_id:188287)问题中，可以精确计算出局部化发生的临界条件。对于一个线性软化模型，可以证明，当[损伤变量](@entry_id:197066) $d$ 达到 $1/2$ 时，局部化条件首次满足。这个[临界点](@entry_id:144653)恰好对应于单轴应力-应变曲线的峰值点（即软化的起始点），这是一个经典的结论 [@problem_id:3554720]。

为了解决局部化模型的[不适定性](@entry_id:635673)问题，必须在连续介质描述中引入一个**[内禀长度尺度](@entry_id:750789)** (internal length scale)，这个过程称为**正则化** (regularization)。引入长度尺度后，模型将能够惩罚过大的应变梯度，从而使局部化区域的宽度保持为一个有限的、与网格无关的物理量，恢复解的网格客观性。主流的[正则化方法](@entry_id:150559)包括 [@problem_id:3554733]：
1.  **[非局部损伤模型](@entry_id:190376)** (Nonlocal models)：在这类模型中，驱动损伤的变量（如等效应变）不再是局部点的值，而是该点周围一个有限邻域内的加权平均值。邻域的大小就定义了[内禀长度尺度](@entry_id:750789)。
2.  **梯度增强损伤模型** (Gradient-enhanced models)：这类模型将[损伤变量](@entry_id:197066)的梯度（例如 $\nabla d$）作为额外的状态变量引入到[亥姆霍兹自由能](@entry_id:136442)中，通常形式为 $\psi(\boldsymbol{\varepsilon}, d, \nabla d) = \psi_{\text{local}}(\boldsymbol{\varepsilon}, d) + \frac{1}{2} c \ell^2 |\nabla d|^2$。这里的参数 $\ell$ 就是[内禀长度尺度](@entry_id:750789)。这导致控制方程变为一个高阶[偏微分方程](@entry_id:141332)（如亥姆霍兹方程），其解自然地包含了对梯度的平滑，从而限制了局部化的宽度。
3.  **[微极连续体](@entry_id:751972)理论** (Micropolar continua) 或**[相场模型](@entry_id:202885)** (Phase-field models) 等也提供了引入长度尺度的[替代途径](@entry_id:182853)，它们通过引入额外的[运动学](@entry_id:173318)自由度或一个弥散的裂纹场来从根本上改变问题的数学结构，从而实现正则化。

总之，对于任何涉及[材料软化](@entry_id:169591)的模拟，采用某种形式的正则化是保证结果物理意义和数值收敛性的前提。