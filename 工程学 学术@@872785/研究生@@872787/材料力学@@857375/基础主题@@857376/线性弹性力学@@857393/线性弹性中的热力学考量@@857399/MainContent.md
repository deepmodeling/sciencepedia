## 引言
材料在工程应用中几乎总是同时承受机械载荷和温度变化，这两种物理效应的耦合作用对其性能和可靠性至关重要。尽管在初步分析中常将力学行为与热学行为分离开来，但一个更深刻、更具预测性的理解必须建立在统一的[热力学](@entry_id:141121)框架之上。线性热弹性理论正是为了解决这一问题而生，它旨在为小变形和小温变条件下的热-力耦合现象提供一个严谨且自洽的物理解释。本文旨在系统性地构建这一理论，弥合纯粹力学模型与热力学原理之间的鸿沟。

在接下来的内容中，我们将通过三个章节的递进式学习，全面掌握线性[热弹性的](@entry_id:160451)精髓。首先，在“**原理与机制**”一章中，我们将深入其[热力学](@entry_id:141121)根基，从亥姆霍兹自由能出发，推导应力、熵与状态变量之间的[本构关系](@entry_id:186508)，并探讨热力学定律如何约束材料行为。接着，在“**应用与跨学科联系**”一章中，我们将展示该理论如何从宏观的工程结构[热应力分析](@entry_id:154981)，延伸到微观的材料[相变](@entry_id:147324)和缺陷行为，并触及地球物理、电化学等前沿领域，彰显其广泛的适用性。最后，通过“**动手实践**”部分提供的具体问题，您将有机会亲手应用所学知识，将理论框架转化为解决实际问题的能力。

## 原理与机制

本章旨在系统阐述线性热[弹性理论](@entry_id:184142)的内在原理与核心机制。在前一章介绍其背景和重要性之后，我们将深入探讨该理论的[热力学](@entry_id:141121)基础。我们将从建立[亥姆霍兹自由能](@entry_id:136442)作为核心热力学势函数开始，推导出应力、熵及其他物理量之间的本构关系。随后，我们将探讨[热力学定律](@entry_id:202285)如何约束材料的本构行为，引出麦克斯韦关系、耗散原理和[稳定性判据](@entry_id:755304)等关键概念。最后，我们将通过分析等温与绝热过程的差异，揭示热-力耦合效应在声波传播等物理现象中的具体体现。本章的目的是为读者构建一个严谨、自洽且与物理直觉相符的线性热弹性理论框架。

### [热力学](@entry_id:141121)基础：状态函数与[共轭变量](@entry_id:147843)

连续介质[热力学](@entry_id:141121)理论建立在[热力学](@entry_id:141121)第一和第二定律的局域形式之上。对于一个纯[热弹性](@entry_id:158447)体，这些基本定律，结合亥姆霍兹自由能 $ \psi $ 的定义，为我们提供了一个强大的理论框架。[亥姆霍兹自由能](@entry_id:136442)被定义为单位参考体积的能量，是[应变张量](@entry_id:193332) $ \boldsymbol{\varepsilon} $ 和绝对温度 $ T $ 的函数，即 $ \psi(\boldsymbol{\varepsilon}, T) $。选择应变和温度作为[自变量](@entry_id:267118)具有极大的便利性，因为在实验和工程应用中，它们往往是直接控制或测量的物理量。

[亥姆霍兹自由能](@entry_id:136442)的微分形式深刻地揭示了其作为[热力学势](@entry_id:140516)的核心作用。其[全微分](@entry_id:171747)可以写作：
$$
d\psi = \frac{\partial\psi}{\partial\boldsymbol{\varepsilon}} : d\boldsymbol{\varepsilon} + \frac{\partial\psi}{\partial T} dT
$$
通过[热力学](@entry_id:141121)第一和第二定律的推演（柯尔曼-诺尔方法，Coleman-Noll procedure），我们可以将与 $ d\boldsymbol{\varepsilon} $ 和 $ dT $ 共轭的量识别为柯西应力张量 $ \boldsymbol{\sigma} $ 和熵密度 $ \eta $。这种识别关系构成了[热弹性](@entry_id:158447)本构理论的基石 [@problem_id:2924305] [@problem_id:2924332] [@problem_id:2924365]：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$
$$
\eta = -\frac{\partial \psi}{\partial T}
$$
第一式表明，在等温条件下，应力是亥姆霍兹自由能对应变的梯度。这与纯弹性理论中应力是[应变能密度](@entry_id:200085)梯度的结论一脉相承。第二式则将[热力学](@entry_id:141121)量“熵”与[自由能函数](@entry_id:749582)联系起来，为分析热效应提供了出发点。

虽然亥姆霍兹自由能对于分析应变和[温度控制](@entry_id:177439)下的过程最为方便，但其他热力学势函数，如内能 $ e(\eta, \boldsymbol{\varepsilon}) $ 和焓 $ h $，在特定场景下也同样重要。例如，焓通常被定义为 $ h = e + pv $，其中 $ p $ 是压力，$ v $ 是比容。这个定义在[流体热力学](@entry_id:188306)中极为自然，因为流体的力学状态可由单一标量压力 $ p $ 完整描述。然而，对于能够抵抗剪切的固体而言，情况则更为复杂。对固体进行类似的勒让德变换得到的焓，其[微分形式](@entry_id:146747)将包含[偏应变](@entry_id:201263)功的项，即 $ dh = Td\eta + vdp + \tilde{\mathbf{s}}:d\boldsymbol{\varepsilon}_{\mathrm{dev}} $，其中 $ \tilde{\mathbf{s}} $ 是[偏应力张量](@entry_id:267642) [@problem_id:2924359]。这意味着固体的焓不仅仅是熵和压力的函数，还依赖于剪切变形的状态。因此，在描述固体的一般变形时，焓的“自然性”远不如其在流体中的应用。这凸显了为固体选择以应变为[自变量](@entry_id:267118)的[亥姆霍兹自由能](@entry_id:136442)的合理性。

### 本构模型：[亥姆霍兹自由能](@entry_id:136442)的具体形式

线性热弹性理论的核心在于为亥姆霍兹自由能 $ \psi(\boldsymbol{\varepsilon}, T) $ 假设一个在参考平衡态 $ (\boldsymbol{\varepsilon}=\mathbf{0}, T=T_0) $ 附近有效的二次函数形式。这种二次形式的假设确保了我们最终得到的[应力-应变关系](@entry_id:274093)是线性的。一个通用且物理意义明确的形式如下 [@problem_id:2924332] [@problem_id:2924347]：
$$
\psi(\boldsymbol{\varepsilon},T) = \frac{1}{2} ( \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}_{\mathrm{th}} ) : \mathbb{C} : ( \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}_{\mathrm{th}} ) + \psi_{0}(T)
$$
其中：
*   $ \mathbb{C} $ 是四阶等温[弹性张量](@entry_id:170728)，它描述了材料的纯机械刚度。
*   $ \boldsymbol{\varepsilon}_{\mathrm{th}} $ 是热[应变张量](@entry_id:193332)。对于线性理论，通常假设 $ \boldsymbol{\varepsilon}_{\mathrm{th}} = \boldsymbol{\alpha}(T-T_0) $，其中 $ \boldsymbol{\alpha} $ 是二阶[热膨胀系数](@entry_id:150685)张量。
*   $ (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}_{\mathrm{th}}) $ 代表纯粹由应力引起的机械应变。因此，第一项 $ \frac{1}{2} (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}_{\mathrm{th}}) : \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}_{\mathrm{th}}) $ 代表了储存在材料中的[弹性应变能](@entry_id:202243)密度。
*   $ \psi_{0}(T) $ 是一个纯粹与温度相关的项，它不贡献于应力，但对于确定熵和[热容](@entry_id:137594)至关重要。

另一种等价的自由能形式也常被使用 [@problem_id:2924305]：
$$
\psi(\boldsymbol{\varepsilon},T) = \frac{1}{2}\boldsymbol{\varepsilon} : \mathbb{C} : \boldsymbol{\varepsilon} - (T - T_0)\boldsymbol{\beta} : \boldsymbol{\varepsilon} + \psi_c(T)
$$
其中 $ \boldsymbol{\beta} $ 是一个二阶[热力耦合](@entry_id:183230)张量。通过比较两种形式，可以发现 $ \boldsymbol{\beta} = \mathbb{C} : \boldsymbol{\alpha} $。这个关系揭示了[热力耦合](@entry_id:183230)的本质：它源于弹性刚度与[热膨胀](@entry_id:137427)的相互作用。

#### [热弹性](@entry_id:158447)本构律的推导

将应力的定义 $ \boldsymbol{\sigma} = \partial\psi/\partial\boldsymbol{\varepsilon} $ 应用于上述第一种自由能形式，并考虑到 $ \mathbb{C} $ 的对称性，我们直接得到了一般线性[热弹性](@entry_id:158447)固体的[本构方程](@entry_id:138559)：
$$
\boldsymbol{\sigma} = \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}_{\mathrm{th}}) = \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\alpha}(T-T_0))
$$
这个方程优雅地表明，总应力由[弹性张量](@entry_id:170728)作用于机械应变（总应变减去[热应变](@entry_id:187744)）而产生。

对于在工程中广泛应用的**[各向同性材料](@entry_id:170678)**，本构关系可以进一步简化。在各向同性假设下，二阶热膨胀张量 $ \boldsymbol{\alpha} $ 必然是球形的，即 $ \boldsymbol{\alpha} = \alpha \mathbf{I} $，其中 $ \alpha $ 是标量线性[热膨胀系数](@entry_id:150685)，$ \mathbf{I} $ 是二阶单位张量。同时，[四阶弹性张量](@entry_id:188318) $ \mathbb{C} $ 可以用两个独立的[弹性常数](@entry_id:146207)来表示，通常是[体积模量](@entry_id:160069) $ K $ 和剪切模量 $ \mu $。利用[体积-偏量分解](@entry_id:183756)方法，可以将 $ \mathbb{C} $ 表达为 [@problem_id:2924347]：
$$
\mathbb{C} = 3K \mathbb{P}_{\mathrm{vol}} + 2\mu \mathbb{P}_{\mathrm{dev}}
$$
其中 $ \mathbb{P}_{\mathrm{vol}} = \frac{1}{3} \mathbf{I} \otimes \mathbf{I} $ 是体积[投影算子](@entry_id:154142)，$ \mathbb{P}_{\mathrm{dev}} $ 是偏量投影算子。将此形式代入应力表达式，并对 $ (\boldsymbol{\varepsilon} - \alpha(T-T_0)\mathbf{I}) $ 进行相应的分解，可以得到[各向同性材料](@entry_id:170678)的应力-应变-温度关系的标准形式：
$$
\boldsymbol{\sigma} = K\big(\text{tr}(\boldsymbol{\varepsilon}) - 3\alpha(T-T_0)\big)\mathbf{I} + 2\mu\left(\boldsymbol{\varepsilon} - \frac{1}{3}\text{tr}(\boldsymbol{\varepsilon})\mathbf{I}\right)
$$
此表达式清晰地分离了应力的[静水压力](@entry_id:275365)部分（第一项）和[偏应力](@entry_id:163323)部分（第二项）。静水压力由[体积应变](@entry_id:267252) $ \text{tr}(\boldsymbol{\varepsilon}) $ 和温度变化 $ T-T_0 $ 共同决定，而偏应力仅由[偏应变](@entry_id:201263)决定。这构成了工程实践中[热应力分析](@entry_id:154981)的理论基础。

值得注意的是，工程中常用的弹性常数，如杨氏模量 $ E $ 和泊松比 $ \nu $，都可以通过基础的[弹性张量](@entry_id:170728) $ \mathbb{C} $ 的[不变量](@entry_id:148850)来表示。例如，体积模量 $ K $ 和[热膨胀系数](@entry_id:150685) $ \alpha $ 可以通过以下[张量迹](@entry_id:755864)运算得到 [@problem_id:2924347]：
$$
K = \frac{1}{9} (\mathbf{I} : \mathbb{C} : \mathbf{I})
$$
$$
\alpha = \frac{1}{3} \text{tr}(\boldsymbol{\alpha})
$$
这建立了从抽象[张量表示](@entry_id:180492)到可测量的工程常数之间的桥梁。

### 熵、[热容](@entry_id:137594)与热-力耦合

现在我们转向热学性质。通过对亥姆霍兹自由能求温度的负导数 $ \eta = -\partial\psi/\partial T $，我们可以得到熵密度的表达式。以 $ \psi(\boldsymbol{\varepsilon},T) = \frac{1}{2}(\boldsymbol{\varepsilon} - \alpha(T-T_0)\mathbf{I}) : \mathbb{C} : (\boldsymbol{\varepsilon} - \alpha(T-T_0)\mathbf{I}) + \psi_{0}(T) $ 为例，并利用各向同性关系 $ \mathbb{C} : \mathbf{I} = 3K\mathbf{I} $，我们得到 [@problem_id:2924332]：
$$
\eta(\boldsymbol{\varepsilon}, T) = 3K\alpha\,\text{tr}(\boldsymbol{\varepsilon}) - 9K\alpha^2(T-T_0) - \frac{d\psi_0(T)}{dT}
$$
这个表达式的一个关键特征是，熵不仅依赖于温度，还依赖于应变（通过 $ \text{tr}(\boldsymbol{\varepsilon}) $ 项）。这意味着对材料施加机械变形会改变其熵状态，这是热-力耦合的直接体现。

材料的热学行为通常通过**热容**来表征。定应变[热容](@entry_id:137594) $ c_\varepsilon $ 定义为 $ c_\varepsilon = T (\partial\eta/\partial T)_\varepsilon $。假设 $ c_\varepsilon $ 是一个与温度无关的常数 $ c_\varepsilon^\star $，我们可以通过积分来确定自由能中的纯热项 $ \psi_0(T) $。施加如 $ \eta(\boldsymbol{\varepsilon}=\mathbf{0}, T_0)=0 $ 和 $ \psi_0(T_0)=0 $ 等[热力学](@entry_id:141121)校准条件后，可以唯一确定 $ \psi_0(T) $ 和熵的完整表达式 [@problem_id:2924332]：
$$
\eta(\boldsymbol{\varepsilon},T) = 3K\alpha\,\text{tr}(\boldsymbol{\varepsilon}) + c_{\varepsilon}^{\star}\ln\left(\frac{T}{T_{0}}\right)
$$
$$
\psi_{0}(T) = c_{\varepsilon}^{\star} \left( (T-T_{0}) - T \ln\left(\frac{T}{T_{0}}\right) \right) - \frac{9}{2}K\alpha^{2}(T-T_{0})^{2}
$$
这套完整的表达式使得我们可以从少数几个基本材料常数（$ K, \alpha, c_\varepsilon^\star, T_0 $）出发，预测材料在任意小应变和温度变化下的完整[热力学状态](@entry_id:755916)。

#### 麦克斯韦关系：理论[自洽性](@entry_id:160889)的体现

亥姆霍兹自由能 $ \psi(\boldsymbol{\varepsilon}, T) $ 作为一个状态函数，其混合[二阶偏导数](@entry_id:635213)必须相等，即 $ \frac{\partial^2\psi}{\partial\boldsymbol{\varepsilon}\partial T} = \frac{\partial^2\psi}{\partial T\partial\boldsymbol{\varepsilon}} $。将应力和熵的定义代入，我们立即得到一组重要的**麦克斯韦关系** [@problem_id:2924305] [@problem_id:2924365]：
$$
\left.\frac{\partial \boldsymbol{\sigma}}{\partial T}\right|_{\boldsymbol{\varepsilon}} = - \left.\frac{\partial \eta}{\partial \boldsymbol{\varepsilon}}\right|_{T}
$$
这个关系式意义非凡，它在两个看似无关的物理现象之间建立了深刻的联系：
*   左侧 $ (\partial\boldsymbol{\sigma}/\partial T)_\varepsilon $ 是**[热应力](@entry_id:180613)系数**，描述了在保持应变恒定时，应力随温度变化的程度。这是一种纯粹的力学测量。
*   右侧 $ (\partial\eta/\partial\boldsymbol{\varepsilon})_T $ 描述了在恒定温度下，熵随应变的变化。根据[热力学第二定律](@entry_id:142732)的另一形式 $ dQ = Td\eta $（对于可逆过程），该项与**形变潜热**或**压卡/弹卡效应**（piezocaloric/elastocaloric effect）直接相关，即在等温下拉伸或压缩材料所引起的吸热或放热。这是一种纯粹的热学测量。

麦克斯韦关系断言，这两种完全不同类型的实验测得的物理量，其数值必然通过一个简单的负号联系在一起。例如，如果实验测得在定应变下，某材料的应力张量随温度的变化率为 [@problem_id:2924365]：
$$
\left.\frac{\partial \boldsymbol{\sigma}}{\partial T}\right|_{\boldsymbol{\varepsilon}} = \begin{pmatrix} -3.60  0.12  0 \\ 0.12  -3.20  0.05 \\ 0  0.05  -3.40 \end{pmatrix} \text{ MPa/K}
$$
那么我们无需进行任何热学实验，即可断定在相同条件下，该材料熵对应变的导数张量为：
$$
\left.\frac{\partial \eta}{\partial \boldsymbol{\varepsilon}}\right|_{T} = \begin{pmatrix} 3.60  -0.12  0 \\ -0.12  3.20  -0.05 \\ 0  -0.05  3.40 \end{pmatrix} \text{ MPa/K}
$$
这种理论上的内在一致性是[热力学势](@entry_id:140516)函数框架强大功能的明证。实验上，可以通过分别测量热应力系数和形变潜热来独立验证此关系，从而为整个理论框架提供坚实的实验支持 [@problem_id:2924365]。

#### [热容](@entry_id:137594)的差异

另一个重要的[热力学](@entry_id:141121)关系是定应力热容 $ c_\sigma = T(\partial\eta/\partial T)_\sigma $ 和定应变热容 $ c_\varepsilon $ 之间的差异。利用麦克斯韦关系和[链式法则](@entry_id:190743)，可以推导出它们之间的普适关系 [@problem_id:2924363]：
$$
c_{\sigma} - c_{\varepsilon} = T \left( \frac{\partial \boldsymbol{\sigma}}{\partial T} \right)_{\boldsymbol{\varepsilon}} : \left[ \mathbb{S}_T : \left( \frac{\partial \boldsymbol{\sigma}}{\partial T} \right)_{\boldsymbol{\varepsilon}} \right]
$$
其中 $ \mathbb{S}_T = \mathbb{C}^{-1} $ 是等温柔度张量。对于[各向同性材料](@entry_id:170678)，该表达式可以惊人地简化为：
$$
c_{\sigma} - c_{\varepsilon} = 9 T K \alpha^2
$$
这个简洁的结果表明，两种[热容](@entry_id:137594)的差异完全由[热膨胀](@entry_id:137427)效应决定。如果一种材料没有热膨胀（$ \alpha=0 $），那么无论在定应力还是定应变下加热它，其[热容](@entry_id:137594)都是相同的。对于像铝这样的典型金属（$ K = 76 \text{ GPa}, \alpha = 23 \times 10^{-6} \text{ K}^{-1} $），在室温 $ T_0 = 300 \text{ K} $ 下，这个差异约为 $ 1.09 \times 10^5 \text{ J m}^{-3}\text{K}^{-1} $，这是一个不可忽略的量值 [@problem_id:2924363]。

### 耗散与稳定性

[热力学第二定律](@entry_id:142732)不仅给出了[本构关系](@entry_id:186508)，还对材料的宏观行为施加了更强的约束：耗散和稳定性。

#### 可逆性与熵产生

将[热力学](@entry_id:141121)第一和第二定律结合，可以导出**克劳修斯-杜亥姆不等式 (Clausius-Duhem inequality)**，它描述了单位体积内熵的产生率 $ \xi $。对于纯[热弹性](@entry_id:158447)体，通过柯尔曼-诺尔方法可以证明，所有与机械变形相关的项都必须为零才能满足不等式，这正是我们得到 $ \boldsymbol{\sigma} = \partial\psi/\partial\boldsymbol{\varepsilon} $ 和 $ \eta = -\partial\psi/\partial T $ 的原因。最终，不等式简化为只包含热传导项的**残余[耗散不等式](@entry_id:188634)** [@problem_id:2924310]：
$$
\mathcal{D} = -\frac{1}{T} \boldsymbol{q} \cdot \nabla T \ge 0
$$
其中 $ \mathcal{D} $ 是单位体积的[耗散功率](@entry_id:177328)，$ \boldsymbol{q} $ 是热流矢量，$ \nabla T $ 是[温度梯度](@entry_id:136845)。这个不等式表明，对于纯[热弹性](@entry_id:158447)材料，唯一的不[可逆性](@entry_id:143146)来源是**热传导**。换言之，[热弹性](@entry_id:158447)变形本身是可逆的，不会产生熵。只有当系统内部存在温度梯度，导致热量从高温区流向低温区时，才会发生耗散和熵增。

如果热流遵循[傅里叶定律](@entry_id:136311) $ \boldsymbol{q} = -k \nabla T $（其中热导率 $ k > 0 $），则熵产生密度 $ \xi = \mathcal{D}/T $ 为 [@problem_id:2924310] [@problem_id:2924349]：
$$
\xi = \frac{k}{T^2} |\nabla T|^2 \ge 0
$$
这个表达式明确指出，只要存在温度梯度（$ \nabla T \neq 0 $），熵产生就为正，过程是不可逆的。反之，如果过程是温度均匀的（$ \nabla T = 0 $）或者是绝热的（$ \boldsymbol{q} = 0 $），那么熵产生为零，过程是**可逆的**。需要强调的是，一个[可逆过程](@entry_id:276625)不一定是等温的，例如，一个被绝热的杆件在快速拉伸时会[发生温度](@entry_id:197328)均匀的降低，这个过程是可逆的（理想情况下）。

#### [热力学稳定性](@entry_id:142877)

热力学稳定性要求处于平衡态的材料在受到微小扰动时能够恢复到原来的状态。对于一个在给定应变和温度下保持平衡的系统，这意味着其亥姆霍兹自由能 $ \psi(\boldsymbol{\varepsilon}, T) $ 必须处于一个[局部极值](@entry_id:144991)。更具体地说，为了保证稳定性 [@problem_id:2924336]：

1.  $ \psi $ 必须是关于应变 $ \boldsymbol{\varepsilon} $ 的**凸函数**。这意味着在平衡态附近，任何应变扰动都会导致自由能增加，从而产生一个恢复力使系统回到平衡位置。在数学上，这要求 $ \psi $ 关于 $ \boldsymbol{\varepsilon} $ 的[二阶导数](@entry_id:144508)——即[弹性张量](@entry_id:170728) $ \mathbb{C} $——必须是**正定的**。
    $$
    \delta\boldsymbol{\varepsilon} : \mathbb{C} : \delta\boldsymbol{\varepsilon} > 0, \quad \forall \delta\boldsymbol{\varepsilon} \neq \mathbf{0}
    $$
    这个条件为[弹性模量](@entry_id:198862)（如 $ K>0, \mu>0 $）必须为正提供了根本的[热力学](@entry_id:141121)依据。

2.  $ \psi $ 必须是关于温度 $ T $ 的**[凹函数](@entry_id:274100)**。这意味着 $\partial^2\psi/\partial T^2  0$。结合 $ c_\varepsilon = -T (\partial^2\psi/\partial T^2)_\varepsilon $ 的定义和 $ T0 $ 的事实，这个条件等价于要求定应变热容 $ c_\varepsilon $ 必须为**正值**。
    $$
    c_\varepsilon  0
    $$
    如果 $ c_\varepsilon  0 $，那么给系统加热反而会导致温度下降，这将引发一个不稳定的热失控过程。

因此，[弹性张量](@entry_id:170728)的正定性和[热容](@entry_id:137594)的正值性并非随意的假设，而是由[热力学第二定律](@entry_id:142732)和稳定性原理所强制要求的深刻结论。

### 物理后果：等温与绝热过程

热-力耦合的一个重要物理后果是材料的力学响应依赖于[热力学过程](@entry_id:141636)的路径。一个典型的例子是[等温过程](@entry_id:143096)（过程足够慢，以至于系统始终与环境保持[热平衡](@entry_id:141693)）与绝热过程（过程足够快，以至于系统没有时间与环境交换热量）之间的差异。

这种差异在弹性[波的传播](@entry_id:144063)中表现得尤为明显。声波的传播速度通常非常快，因此可以近似为[绝热过程](@entry_id:138150)。波速由材料的[有效弹性模量](@entry_id:181086)决定。对于纵波，其速度 $ c_L $ 由[纵波](@entry_id:172335)模量 $ M = K + 4\mu/3 $ 决定。在不同[热力学](@entry_id:141121)条件下，[体积模量](@entry_id:160069) $ K $ 的值是不同的 [@problem_id:2924307]。

*   **等温纵波[波速](@entry_id:186208)** $ c_L^T $，对应于一个假想的极慢过程，由**等温体积模量** $ K_T $ 决定：
    $$
    c_L^T = \sqrt{\frac{K_T + 4\mu/3}{\rho}}
    $$
*   **绝热[纵波](@entry_id:172335)波速** $ c_L^S $，对应于真实的声波传播过程，由**绝热体积模量** $ K_S $ 决定：
    $$
    c_L^S = \sqrt{\frac{K_S + 4\mu/3}{\rho}}
    $$

通过[热力学](@entry_id:141121)关系可以证明 $ K_S  K_T $，它们的差异与热膨胀系数和温度有关。具体而言，$ K_S = K_T / (1 - K_T \alpha_v^2 T / (\rho_0 c_p)) $，其中 $ \alpha_v $ 是[体膨胀](@entry_id:144241)系数（对于[各向同性材料](@entry_id:170678) $ \alpha_v=3\alpha $），$ c_p $ 是定[压比](@entry_id:137698)热。因此，可以推断出**绝[热波](@entry_id:167489)速总是大于等温波速** ($ c_L^S  c_L^T $)。

在[弱耦合](@entry_id:140994)极限下（即热膨胀效应不显著），它们之间的相对差异可以近似为 [@problem_id:2924307]：
$$
\frac{c_L^S - c_L^T}{c_L^T} \approx \frac{3K_T^2 \alpha^2 T_0}{2\rho c_p(3K_T + 4\mu)}
$$
这个结果清晰地表明，两种[波速](@entry_id:186208)的差异正比于 $ \alpha^2 T_0 $，直接量化了热-力耦合效应对材料动态响应的影响。这不仅是一个理论上的精妙推论，也是一个可以通过超声实验精确验证的物理效应。