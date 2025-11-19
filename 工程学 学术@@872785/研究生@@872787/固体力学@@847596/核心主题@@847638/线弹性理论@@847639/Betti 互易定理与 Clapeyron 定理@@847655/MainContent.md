## 引言
在线弹性力学中，能量原理不仅是深刻的理论洞见，也是解决复杂工程问题的强大工具。在众多能量原理中，[贝蒂互易定理](@entry_id:200996)和[克拉佩龙定理](@entry_id:188203)以其优雅的对称性和实用性而占据核心地位。然而，初学者往往只知其然，而不知其所以然——这些定理究竟源自何处？它们成立的物理和数学本质是什么？其[适用范围](@entry_id:636189)的边界又在哪里？本文旨在系统性地回答这些问题，为读者构建一个关于这两个核心定理的完整知识体系。

在接下来的章节中，我们将首先在“原理与机制”一章中，从虚功原理出发，深入剖析这两个定理的推导过程、核心条件（如本构对称性）及其数学本质。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论如何在结构力学、计算方法（如[边界元法](@entry_id:141290)）、[多物理场耦合](@entry_id:171389)以及[实验动力学](@entry_id:188381)等领域大放异彩。最后，通过“动手实践”部分，读者将有机会通过具体的计算练习，亲手验证和探索这些定理的强大功能及其在[非线性](@entry_id:637147)或[非保守系统](@entry_id:166237)中的失效情况，从而将理论知识转化为深刻的力学直觉。

## 原理与机制

在对弹性体进行力学分析时，功与能的原理提供了深刻的见解和强大的计算工具。本章在前一章介绍的基础上，深入探讨线弹性理论中两个核心的能量定理：[克拉佩龙定理](@entry_id:188203)（Clapeyron's theorem）和[贝蒂互易定理](@entry_id:200996)（Betti's reciprocal theorem）。我们将从作为共同基础的虚功原理出发，揭示这些定理的物理意义、推导过程、数学本质，以及它们成立所需的关键条件，并探讨其适用性的边界。

### 虚功原理：弹性力学分析的基石

我们分析的出发点是**[虚功原理](@entry_id:138749)**（principle of virtual work），它是平衡方程的等效[弱形式](@entry_id:142897)（weak form）。考虑一个占据区域 $\Omega$ 的弹性体，其边界 $\Gamma$ 分为位移边界 $\Gamma_u$ 和力边界 $\Gamma_t$。在[体力](@entry_id:174230) $\boldsymbol{b}$ 和面力 $\boldsymbol{t}$ 的作用下，物体[达到平衡](@entry_id:170346)，产生位移场 $\boldsymbol{u}$ 和应[力场](@entry_id:147325) $\boldsymbol{\sigma}$。

虚功原理指出，对于处于平衡状态的物体，作用于其上的所有外力在任何**[虚位移](@entry_id:168781)**（virtual displacement）$\delta\boldsymbol{u}$ 上所作的功（称为**虚外力功** $\delta W_{\text{ext}}$），恒等于内力（应力）在相应的虚应变 $\delta\boldsymbol{\varepsilon}$ 上所作的功（称为**虚[内力](@entry_id:167605)功** $\delta W_{\text{int}}$）。这里的[虚位移](@entry_id:168781)是一个满足所有几何约束（即在位移边界 $\Gamma_u$ 上为零）的、任意的、无限小的[位移场](@entry_id:141476)。

数学上，虚内力功和虚外力功定义如下：
$$
\delta W_{\text{int}} = \int_{\Omega} \boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon} \, d\Omega
$$
$$
\delta W_{\text{ext}} = \int_{\Omega} \boldsymbol{b} \cdot \delta\boldsymbol{u} \, d\Omega + \int_{\Gamma_t} \boldsymbol{t} \cdot \delta\boldsymbol{u} \, d\Gamma
$$
其中，$\delta\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \delta\boldsymbol{u} + (\nabla \delta\boldsymbol{u})^{\top})$ 是与[虚位移](@entry_id:168781) $\delta\boldsymbol{u}$ 对应的虚[应变张量](@entry_id:193332)，符号 “$:$” 表示张量的[双点积](@entry_id:748648)。

因此，平衡状态的数学表述即为：
$$
\delta W_{\text{int}} = \delta W_{\text{ext}} \quad \forall \delta\boldsymbol{u} \text{ kinematically admissible}
$$
这个原理的强大之处在于它对“所有”满足条件的[虚位移](@entry_id:168781)都成立，而非仅仅对真实位移成立。这一性质使其成为[有限元法](@entry_id:749389)等近似数值方法的理论基础，并且是我们推导[克拉佩龙定理](@entry_id:188203)和贝蒂定理的逻辑起点。

### [克拉佩龙定理](@entry_id:188203)：线弹性体中的能量与外力功

[克拉佩龙定理](@entry_id:188203)揭示了在线弹性体中，储存的应变能与外力所做功之间的直接关系。对于一个**[线性弹性](@entry_id:166983)材料**，应力与应变呈[线性关系](@entry_id:267880) $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}$，其[应变能密度](@entry_id:200085) $W$ 是应变的二次函数：
$$
W(\boldsymbol{\varepsilon}) = \frac{1}{2} \boldsymbol{\varepsilon} : (\mathbb{C} : \boldsymbol{\varepsilon}) = \frac{1}{2} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}
$$
物体的总[应变能](@entry_id:162699) $U$ 则是[应变能密度](@entry_id:200085)在整个体积上的积分：
$$
U = \int_{\Omega} W(\boldsymbol{\varepsilon}) \, d\Omega = \frac{1}{2} \int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon} \, d\Omega
$$

现在考虑一个从无应力状态开始，所有外力（体力 $\boldsymbol{b}$ 和面力 $\boldsymbol{t}$）均按比例从零加载到其最[终值](@entry_id:141018)的过程。这种加载方式称为**[比例加载](@entry_id:191744)**（proportional loading）。设加载因子为 $\lambda \in [0, 1]$，则任意时刻的载荷为 $\lambda \boldsymbol{b}_f$ 和 $\lambda \boldsymbol{t}_f$，其中带下标 $f$ 的量表示最终载荷。由于系统是线性的，位移也与 $\lambda$ 成正比，即 $\boldsymbol{u}(\lambda) = \lambda \boldsymbol{u}_f$。

在加载过程中，外力所做的总功 $W_{\text{ext}}$ 是增量功的累积：
$$
W_{\text{ext}} = \int_{0}^{1} \left( \int_{\Omega} (\lambda \boldsymbol{b}_f) \cdot d(\lambda \boldsymbol{u}_f) \, d\Omega + \int_{\Gamma_t} (\lambda \boldsymbol{t}_f) \cdot d(\lambda \boldsymbol{u}_f) \, d\Gamma \right)
$$
由于 $d(\lambda \boldsymbol{u}_f) = \boldsymbol{u}_f d\lambda$，上式变为：
$$
W_{\text{ext}} = \left( \int_{0}^{1} \lambda \, d\lambda \right) \left( \int_{\Omega} \boldsymbol{b}_f \cdot \boldsymbol{u}_f \, d\Omega + \int_{\Gamma_t} \boldsymbol{t}_f \cdot \boldsymbol{u}_f \, d\Gamma \right) = \frac{1}{2} \left( \int_{\Omega} \boldsymbol{b}_f \cdot \boldsymbol{u}_f \, d\Omega + \int_{\Gamma_t} \boldsymbol{t}_f \cdot \boldsymbol{u}_f \, d\Gamma \right)
$$
对于准静态弹性过程，外力所做的功完全转化为储存的[应变能](@entry_id:162699)，即 $W_{\text{ext}} = U$。结合前面的表达式，我们得到了**[克拉佩龙定理](@entry_id:188203)**的完整形式：
$$
U = \frac{1}{2} \int_{\Omega} \boldsymbol{\sigma}_f : \boldsymbol{\varepsilon}_f \, d\Omega = \frac{1}{2} \left( \int_{\Omega} \boldsymbol{b}_f \cdot \boldsymbol{u}_f \, d\Omega + \int_{\Gamma_t} \boldsymbol{t}_f \cdot \boldsymbol{u}_f \, d\Gamma \right)
$$
该定理表明，在[线性弹性](@entry_id:166983)体中，对于从零开始的[比例加载](@entry_id:191744)，最终储存的总应变能等于最终外力在最终位移上所做功的一半。

这个因子 $\frac{1}{2}$ 有一个非常直观的几何解释。如果我们用一个[广义力](@entry_id:169699) $F$ 和其共轭的广义位移 $q$ 来描述系统的响应，由于线性和[比例加载](@entry_id:191744)，$F-q$ 关系是一条从原点 $(0,0)$ 到终点 $(F^\star, q^\star)$ 的直线。外力所做的功 $W_{\text{ext}}$ 是这条曲线下的面积，即三角形面积 $\frac{1}{2} F^\star q^\star$。根据[能量守恒](@entry_id:140514)，这也等于储存的[应变能](@entry_id:162699) $U$。而“最终力乘以最终位移”的量 $F^\star q^\star$ 对应于包围该三角形的矩形面积，其值恰好是 $2U$。[克拉佩龙定理](@entry_id:188203)本质上是说，储存的能量是外力[势能](@entry_id:748988)损失的一半，另一半则在加载过程中耗散（对于[准静态过程](@entry_id:136273)，这个“耗散”是概念上的，表示[势能](@entry_id:748988)的线性下降）。

### 贝蒂定理：响应的互易性

[贝蒂互易定理](@entry_id:200996)是线弹性理论中一个更为深刻和普适的原理。它描述了不同载荷系统之间的一种对称性或互易性。

考虑同一个弹性体上的两个独立的平衡状态：
*   **状态 1**：由载荷系统（[体力](@entry_id:174230) $\boldsymbol{b}^{(1)}$，面力 $\boldsymbol{t}^{(1)}$）引起，产生响应（位移 $\boldsymbol{u}^{(1)}$，应变 $\boldsymbol{\varepsilon}^{(1)}$，应力 $\boldsymbol{\sigma}^{(1)}$）。
*   **状态 2**：由载荷系统（[体力](@entry_id:174230) $\boldsymbol{b}^{(2)}$，面力 $\boldsymbol{t}^{(2)}$）引起，产生响应（位移 $\boldsymbol{u}^{(2)}$，应变 $\boldsymbol{\varepsilon}^{(2)}$，应力 $\boldsymbol{\sigma}^{(2)}$）。

我们可以巧妙地应用虚功原理。首先，将状态1视为真实平衡态，而将状态2的位移场 $\boldsymbol{u}^{(2)}$ 视为一个[虚位移](@entry_id:168781)场。根据[虚功原理](@entry_id:138749)，我们有：
$$
\int_{\Omega} \boldsymbol{\sigma}^{(1)} : \boldsymbol{\varepsilon}^{(2)} \, d\Omega = \int_{\Omega} \boldsymbol{b}^{(1)} \cdot \boldsymbol{u}^{(2)} \, d\Omega + \int_{\Gamma_t} \boldsymbol{t}^{(1)} \cdot \boldsymbol{u}^{(2)} \, d\Gamma
$$
等式左边是状态1的应力在状态2的应变上做的“交叉”虚内力功，右边是状态1的外力在状态2的位移上做的“交叉”虚外力功。

接着，我们交换角色，将状态2视为真实平衡态，将状态1的位移场 $\boldsymbol{u}^{(1)}$ 视为[虚位移](@entry_id:168781)场，得到：
$$
\int_{\Omega} \boldsymbol{\sigma}^{(2)} : \boldsymbol{\varepsilon}^{(1)} \, d\Omega = \int_{\Omega} \boldsymbol{b}^{(2)} \cdot \boldsymbol{u}^{(1)} \, d\Omega + \int_{\Gamma_t} \boldsymbol{t}^{(2)} \cdot \boldsymbol{u}^{(1)} \, d\Gamma
$$
**贝蒂定理**指出，上述两个等式右边的[交叉](@entry_id:147634)外力功是相等的。这意味着，状态1的载荷在状态2的位移上做的功，等于状态2的载荷在状态1的位移上做的功。
$$
\int_{\Omega} \boldsymbol{b}^{(1)} \cdot \boldsymbol{u}^{(2)} \, d\Omega + \int_{\Gamma_t} \boldsymbol{t}^{(1)} \cdot \boldsymbol{u}^{(2)} \, d\Gamma = \int_{\Omega} \boldsymbol{b}^{(2)} \cdot \boldsymbol{u}^{(1)} \, d\Omega + \int_{\Gamma_t} \boldsymbol{t}^{(2)} \cdot \boldsymbol{u}^{(1)} \, d\Gamma
$$
这个惊人的结论成立的前提是，两个等式左边的[交叉](@entry_id:147634)[内力](@entry_id:167605)功必须相等：
$$
\int_{\Omega} \boldsymbol{\sigma}^{(1)} : \boldsymbol{\varepsilon}^{(2)} \, d\Omega = \int_{\Omega} \boldsymbol{\sigma}^{(2)} : \boldsymbol{\varepsilon}^{(1)} \, d\Omega
$$
这个条件的成立并非理所当然，它深刻地依赖于材料的本构关系，我们将在下一节详细探讨。

### 本构对称性的核心作用

无论是[克拉佩龙定理](@entry_id:188203)中断言[应变能密度](@entry_id:200085)为 $W = \frac{1}{2} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}$，还是贝蒂定理中要求[交叉](@entry_id:147634)内力功相等，其背后都隐藏着对材料本构性质的同一个关键要求。

在线性弹性中，[应力-应变关系](@entry_id:274093)由[四阶弹性张量](@entry_id:188318) $\mathbb{C}$ 定义：$\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}$，或用分量表示为 $\sigma_{ij} = C_{ijkl} \varepsilon_{kl}$。[弹性张量](@entry_id:170728)通常具有以下对称性：
1.  **次对称性 (Minor Symmetries)**: $C_{ijkl} = C_{jikl} = C_{ijlk}$。这些对称性源于[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 和[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 的对称性（$\sigma_{ij}=\sigma_{ji}$, $\varepsilon_{kl}=\varepsilon_{lk}$），而应力[张量的对称性](@entry_id:202126)本身是[角动量守恒](@entry_id:156798)（无体力矩）的结果。
2.  **主对称性 (Major Symmetry)**: $C_{ijkl} = C_{klij}$。这个对称性则没有那么直观。

现在，我们来检验贝蒂定理所需的[交叉](@entry_id:147634)[内力](@entry_id:167605)功相等的条件。将[本构关系](@entry_id:186508)代入：
$$
\int_{\Omega} (\mathbb{C} : \boldsymbol{\varepsilon}^{(1)}) : \boldsymbol{\varepsilon}^{(2)} \, d\Omega = \int_{\Omega} (\mathbb{C} : \boldsymbol{\varepsilon}^{(2)}) : \boldsymbol{\varepsilon}^{(1)} \, d\Omega
$$
写成张量分量形式，即要求：
$$
\int_{\Omega} C_{ijkl} \varepsilon_{kl}^{(1)} \varepsilon_{ij}^{(2)} \, d\Omega = \int_{\Omega} C_{ijkl} \varepsilon_{kl}^{(2)} \varepsilon_{ij}^{(1)} \, d\Omega
$$
要使该等式对任意应变场都成立，被积函数必须处处相等。通过交换[哑指标](@entry_id:188070) $(i,j)$ 和 $(k,l)$，我们发现这等价于要求[弹性张量](@entry_id:170728)具有**主对称性** $C_{ijkl} = C_{klij}$。

同样，主对称性也是存在一个二次型[应变能势](@entry_id:755493)函数 $W(\boldsymbol{\varepsilon}) = \frac{1}{2} \boldsymbol{\varepsilon} : \mathbb{C} : \boldsymbol{\varepsilon}$ 的充要条件。这种存在能量势函数的材料称为**[超弹性材料](@entry_id:190241)**（hyperelastic material）。因此，贝蒂定理和[克拉佩龙定理](@entry_id:188203)都要求材料不仅是线性的，而且是线性的[超弹性材料](@entry_id:190241)。

为了具体说明主对称性的关键作用，我们可以构建一个反例。考虑一个仅满足次对称性但违背主对称性的[二维材料](@entry_id:142244)。其[本构矩阵](@entry_id:164908) $\mathsf{C}$ 为[非对称矩阵](@entry_id:153254)：
$$
\mathsf{C} = \begin{pmatrix} 30\times 10^{9}  & 0  & 10\times 10^{9} \\ 0  & 20\times 10^{9}  & 0 \\ 0  & 0  & 15\times 10^{9} \end{pmatrix} \, \text{Pa}
$$
对于两个均匀应变状态 $\boldsymbol{e}^{(1)} = [10^{-3}, 0, 0]^{\mathsf{T}}$ 和 $\boldsymbol{e}^{(2)} = [0, 0, 2 \times 10^{-3}]^{\mathsf{T}}$，我们可以计算出其交叉功密度。
应力状态分别为 $\boldsymbol{s}^{(1)} = \mathsf{C}\boldsymbol{e}^{(1)} = [3 \times 10^7, 0, 0]^{\mathsf{T}}$ 和 $\boldsymbol{s}^{(2)} = \mathsf{C}\boldsymbol{e}^{(2)} = [2 \times 10^7, 0, 3 \times 10^7]^{\mathsf{T}}$。
交叉功密度之差（互易性缺陷）为：
$$
\Delta = \boldsymbol{s}^{(1)} \cdot \boldsymbol{e}^{(2)} - \boldsymbol{s}^{(2)} \cdot \boldsymbol{e}^{(1)} = 0 - (2 \times 10^7 \times 10^{-3}) = -2.000 \times 10^{4} \, \mathrm{J/m^{3}}
$$
这个非零结果明确地展示了，一旦主对称性被破坏，[贝蒂互易定理](@entry_id:200996)便不再成立。

### 数学抽象：[自伴算子](@entry_id:152188)与[格林函数](@entry_id:147802)

贝蒂定理的物理直观背后，是深刻的数学结构。我们可以将线弹性问题表述为一个算子方程 $L(\boldsymbol{u}) = \boldsymbol{f}$，其中 $L(\boldsymbol{u}) = -\nabla \cdot (\mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{u}))$ 是弹性算子，$\boldsymbol{f}$ 代表广义载荷。

在虚功原理的框架下，该算子方程的弱形式由一个双线性形式 $a(\boldsymbol{u}, \boldsymbol{v})$ 定义：
$$
a(\boldsymbol{u}, \boldsymbol{v}) = \int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{u}) : \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, d\Omega
$$
贝蒂定理的核心条件 $\int \boldsymbol{\sigma}^{(1)}:\boldsymbol{\varepsilon}^{(2)} d\Omega = \int \boldsymbol{\sigma}^{(2)}:\boldsymbol{\varepsilon}^{(1)} d\Omega$ 正是 $a(\boldsymbol{u}^{(1)}, \boldsymbol{u}^{(2)}) = a(\boldsymbol{u}^{(2)}, \boldsymbol{u}^{(1)})$。也就是说，贝蒂定理成立的充要条件是双线性形式 $a(\cdot, \cdot)$ 是对称的。

一个算子 $L$ 被称为**自伴的**（self-adjoint），如果对于定义域内任意两个函数 $\boldsymbol{u}, \boldsymbol{v}$，[内积](@entry_id:158127)关系 $\langle L(\boldsymbol{u}), \boldsymbol{v} \rangle = \langle \boldsymbol{u}, L(\boldsymbol{v}) \rangle$ 成立。可以证明，弹性算子 $L$ 的自伴性等价于其对应的[双线性形式](@entry_id:746794) $a(\cdot, \cdot)$ 的对称性。因此，贝蒂定理是弹性算子自伴性的物理体现，而这又根植于[弹性张量](@entry_id:170728) $\mathbb{C}$ 的主对称性。

互易性的一个极其优美的应用体现在**格林函数**（Green's function）的对称性上。定义格林张量 $G_{ij}(\boldsymbol{x}, \boldsymbol{y})$ 为在 $\boldsymbol{y}$ 点施加一个沿 $j$ 方向的单位点力所引起的在 $\boldsymbol{x}$ 点的 $i$ 方向位移。现在考虑两个载荷状态：
*   状态 1：在 $\boldsymbol{y}$ 点施加沿 $\boldsymbol{e}_j$ 方向的单位力，即 $\boldsymbol{b}^{(1)}(\boldsymbol{z}) = \delta(\boldsymbol{z}-\boldsymbol{y})\boldsymbol{e}_j$。其位移响应为 $\boldsymbol{u}^{(1)}(\boldsymbol{x}) = G_{ij}(\boldsymbol{x}, \boldsymbol{y})\boldsymbol{e}_i$。
*   状态 2：在 $\boldsymbol{x}$ 点施加沿 $\boldsymbol{e}_i$ 方向的单位力，即 $\boldsymbol{b}^{(2)}(\boldsymbol{z}) = \delta(\boldsymbol{z}-\boldsymbol{x})\boldsymbol{e}_i$。其位移响应为 $\boldsymbol{u}^{(2)}(\boldsymbol{y}) = G_{ki}(\boldsymbol{y}, \boldsymbol{x})\boldsymbol{e}_k$。

将这两个状态代入贝蒂定理的表达式中：
$$
\int_{\Omega} \delta(\boldsymbol{z}-\boldsymbol{y})\boldsymbol{e}_j \cdot \boldsymbol{u}^{(2)}(\boldsymbol{z}) \, d\Omega = \int_{\Omega} \delta(\boldsymbol{z}-\boldsymbol{x})\boldsymbol{e}_i \cdot \boldsymbol{u}^{(1)}(\boldsymbol{z}) \, d\Omega
$$
利用狄拉克 $\delta$ 函数的性质，上式简化为：
$$
\boldsymbol{e}_j \cdot \boldsymbol{u}^{(2)}(\boldsymbol{y}) = \boldsymbol{e}_i \cdot \boldsymbol{u}^{(1)}(\boldsymbol{x}) \implies u_j^{(2)}(\boldsymbol{y}) = u_i^{(1)}(\boldsymbol{x})
$$
代入格林函数的定义，我们得到了著名的**麦克斯韦-贝蒂互易关系**（Maxwell-Betti reciprocal relation）：
$$
G_{ji}(\boldsymbol{y}, \boldsymbol{x}) = G_{ij}(\boldsymbol{x}, \boldsymbol{y})
$$
这个结果的物理意义是：由 $\boldsymbol{y}$ 点的 $j$ 方向单位力在 $\boldsymbol{x}$ 点引起的 $i$ 方向位移，等于由 $\boldsymbol{x}$ 点的 $i$ 方向单位力在 $\boldsymbol{y}$ 点引起的 $j$ 方向位移。这种响应的对称性是自伴系统的一个标志性特征。值得注意的是，这种互易性也适用于无阻尼线性[弹性动力学](@entry_id:175818)系统的时间谐波响应。

### 适用边界与推广

经典[克拉佩龙定理](@entry_id:188203)和贝蒂定理的成立依赖于一系列严格的假设：小应变、线性本构关系、[超弹性](@entry_id:159356)（主对称性）以及保守载荷。当这些假设被打破时，定理将不再成立或需要修正。

#### [材料非线性](@entry_id:162855)与有限变形
对于[非线性](@entry_id:637147)材料，或在有限变形框架下，应力不再是应变的线性函数。经典贝蒂定理不再成立。然而，如果材料是超弹性的（即存在[应变能函数](@entry_id:178435)，即使是非二次的），那么一个**增量[互易定理](@entry_id:267731)**仍然可能成立。这要求描述微小增量响应的[切线刚度](@entry_id:166213)算子是自伴的，这在[超弹性材料](@entry_id:190241)中是保证的。区分**材料框架无差异性**（material frame indifference, MFI）和[超弹性](@entry_id:159356)是很重要的。MFI是所有物理上合理的本构模型都应满足的基本原理，但它本身并不足以保证互易性。互易性需要更强的[超弹性](@entry_id:159356)假设。

#### [非保守载荷](@entry_id:196804)
当系统受到**[非保守载荷](@entry_id:196804)**（non-conservative loads），如**随动载荷**（follower loads）时，互易性会遭到破坏。随动载荷的大小或方向依赖于物体的变形。这会在系统的[切线刚度矩阵](@entry_id:170852)中引入非对称项，从而使控制算子不再自伴。

考虑一个经典的例子：一根长度为 $L$、抗弯刚度为 $EI$ 的悬臂梁，其末端受到一个大小恒为 $P$ 的切向随动压力。在小转角假设下，该随动载荷等效于一个额外的、与末端转角 $\varphi$ 相关的剪力 $P\varphi$。这导致系统的[切线刚度矩阵](@entry_id:170852) $K_{\mathrm{t}}$ 变为非对称：
$$
K_{\mathrm{t}} = \begin{pmatrix} \frac{12EI}{L^{3}}  & - \frac{6EI}{L^{2}} - P \\ - \frac{6EI}{L^{2}}  & \frac{4EI}{L} \end{pmatrix}
$$
由于 $K_{\mathrm{t},12} \neq K_{\mathrm{t},21}$，系统失去了互易性。若分别计算末端[剪力](@entry_id:172634) $S$ 和弯矩 $M$ 单独作用下的[交叉](@entry_id:147634)响应，会发现互易性缺陷 $\mathcal{D} = S w_M - M \varphi_S = \frac{P L^{4} S M}{6 E I (2 E I - P L^{2})}$ 不为零，[直接证明](@entry_id:141172)了互易性的丧失。

#### [初始应力](@entry_id:750652)
当弹性体存在一个[初始应力](@entry_id:750652)场 $\boldsymbol{\sigma}^{0}$ 时，即使增量变形是线性的，[克拉佩龙定理](@entry_id:188203)也需要修正。[初始应力](@entry_id:750652)会贡献一个所谓的**[几何刚度](@entry_id:172820)**（geometric stiffness）项到系统的总能量中。对于小的叠加位移 $\boldsymbol{u}$，总的二次内能[势函数](@entry_id:176105)变为：
$$
U(\boldsymbol{u}) = \frac{1}{2} \int_{V} \left[ \boldsymbol{\varepsilon}(\boldsymbol{u}) : \mathsf{C} : \boldsymbol{\varepsilon}(\boldsymbol{u}) + \boldsymbol{\sigma}^{0} : ((\nabla \boldsymbol{u})^{\mathsf{T}} (\nabla\boldsymbol{u})) \right] dV
$$
如果[初始应力](@entry_id:750652)和附加的增量载荷都是保守的（例如，静载荷），那么系统的[切线](@entry_id:268870)算子仍然是对称的。在这种情况下，一个推广的[克拉佩龙定理](@entry_id:188203)成立，即 $2U$ 等于增量外力在最终增量位移上所做的功。

总之，[克拉佩龙定理](@entry_id:188203)与[贝蒂互易定理](@entry_id:200996)是线性保守弹性系统能量与响应对称性的深刻体现。它们的有效性直接与控制算子的自伴性相关，这在物理上对应于[超弹性](@entry_id:159356)[本构关系](@entry_id:186508)和保守外力。理解这些定理的机制及其局限性，对于准确应用[弹性理论](@entry_id:184142)和进行更高级的力学分析至关重要。