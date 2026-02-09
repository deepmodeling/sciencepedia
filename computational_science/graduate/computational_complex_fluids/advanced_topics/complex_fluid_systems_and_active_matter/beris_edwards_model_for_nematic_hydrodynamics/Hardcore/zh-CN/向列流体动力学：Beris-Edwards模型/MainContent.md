## 引言
在复杂流体领域，向列相液晶因其独特的取向序与流动之间的复杂耦合而备受关注。准确地预测和模拟这些材料的行为，对于显示技术、传感器设计乃至生物物理学研究都至关重要。然而，这需要一个既能捕捉微观取向结构，又能描述宏观流体动力学，并保证两者之间相互作用符合热力学原理的理论框架。经典的指向矢理论在处理拓扑缺陷核心或流动诱导的相变时存在局限性，这正是Beris-Edwards模型所要解决的核心问题。

本文旨在为读者提供一个关于Beris-Edwards模型的全面而深入的指南。通过学习本文，你将掌握这一描述向列相流体动力学的强大工具。
*   在第一章 **“原理与机制”** 中，我们将深入剖析模型的基础，从定义液晶序的Q张量，到构建系统的Landau-de Gennes自由能，并最终推导出控制序参量和流场演化的完整耦合方程组。
*   接下来的 **“应用与跨学科连接”** 章节将展示该模型的强大威力，探讨其如何解释复杂的流变现象、拓扑缺陷的物理学，并如何扩展到活性物质这一前沿领域。
*   最后，在 **“动手实践”** 部分，我们将通过一系列精心设计的计算问题，引导你从理论走向实践，解决数值模拟中的关键挑战，并学习如何从模拟结果中提取有意义的物理洞见。

通过这一结构化的学习路径，本文将带领你从基本原理出发，逐步深入到前沿应用和计算实践，最终全面掌握Beris-Edwards模型的核心精髓。

## 原理与机制

本章旨在阐述 Beris-Edwards 模型的核心物理原理与数学机制。我们将从描述向列相液晶序的 Q 张量序参量入手，进而构建系统的热力学自由能，并最终推导出控制序参量与流场耦合动力学的完整方程组。

### 序参量：Q 张量

为了描述向列相液晶的取向序，我们不能仅仅满足于描述平均取向方向，还需要量化取向的程度。Beris-Edwards 模型采用一个二阶、对称、无迹的张量场 $Q(\boldsymbol{x},t)$ 作为核心的**序参量**。

#### Q 张量的定义与性质

从微观角度看，$Q$ 张量是分子取向[分布函数](@entry_id:145626)二阶矩的各向异性部分。若用单位矢量 $\boldsymbol{u}$ 表示单个棒状分子的长轴方向，则 $Q$ 张量由系综平均定义：
$$
Q = \left\langle \boldsymbol{u}\boldsymbol{u} - \frac{1}{3} I \right\rangle
$$
其中 $\boldsymbol{u}\boldsymbol{u}$ 是并矢， $I$ 是三维单位张量。从这个定义出发，我们可以直接推导出 $Q$ 张量的两个基本性质 [@problem_id:4079568]。

首先，由于并矢 $\boldsymbol{u}\boldsymbol{u}$（其分量为 $u_i u_j$）和单位张量 $I$ 都是对称的，而系综平均是一个线性运算，它保持了对称性，因此 **$Q$ 张量必然是对称的**，即 $Q = Q^T$。

其次，$Q$ 张量的迹（trace）为：
$$
\operatorname{tr}(Q) = \operatorname{tr}\left(\left\langle \boldsymbol{u}\boldsymbol{u} - \frac{1}{3} I \right\rangle\right) = \left\langle \operatorname{tr}(\boldsymbol{u}\boldsymbol{u}) - \operatorname{tr}\left(\frac{1}{3} I\right) \right\rangle
$$
由于 $\operatorname{tr}(\boldsymbol{u}\boldsymbol{u}) = \boldsymbol{u} \cdot \boldsymbol{u} = |\boldsymbol{u}|^2 = 1$，且在三维空间中 $\operatorname{tr}(I) = 3$，所以 $\operatorname{tr}(\frac{1}{3} I) = 1$。因此，
$$
\operatorname{tr}(Q) = \langle 1 - 1 \rangle = 0
$$
这表明 **$Q$ 张量是无迹的**。这两个性质——对称与无迹——意味着一个 $3 \times 3$ 的 $Q$ 张量只有五个独立的自由度。

物理上，$Q$ 张量的本征值和本征矢量描述了系统的主取向轴和沿这些轴的取向序程度。作为一个实对称张量，$Q$ 总有三个实本征值，记为 $\lambda_1, \lambda_2, \lambda_3$。无迹性意味着 $\lambda_1 + \lambda_2 + \lambda_3 = 0$。

#### 通过本征值与不变量对相态进行分类

$Q$ 张量本征值的简并情况决定了液晶的宏观相态 [@problem_id:4079568]：

1.  **各向同性相 (Isotropic Phase)**：所有分子取向完全随机，没有任何宏观上的择优方向。此时，三个本征值必然相等。由于它们的和为零，所以 $\lambda_1 = \lambda_2 = \lambda_3 = 0$，这意味着 $Q=0$。

2.  **单轴相 (Uniaxial Phase)**：系统围绕一个主方向（称为**指向矢**，director）呈现出圆柱对称性。这意味着有且仅有两个本征值相等。若本征值为 $\{-2b, b, b\}$，则系统是单轴的。在这种情况下，$Q$ 张量可以写成一种更直观的形式：
    $$
    Q = S \left( \boldsymbol{n}\boldsymbol{n} - \frac{1}{3} I \right)
    $$
    其中 $\boldsymbol{n}$ 是指向矢，一个单位矢量，表示平均取向方向；$S$ 是一个标量，称为**标量序参量**，它量化了分子沿 $\boldsymbol{n}$ 方向排列的规整程度。将这种形式的 $Q$ 对角化，易得其本征值为 $\{\frac{2S}{3}, -\frac{S}{3}, -\frac{S}{3}\}$，这与 $\{-2b, b, b\}$ 的形式一致（令 $b = -S/3$）。$S>0$ 对应于棒状分子倾向于平行于 $\boldsymbol{n}$ 排列的**长棒状 (prolate)** 单轴相，$S0$ 对应于盘状分子倾向于垂直于 $\boldsymbol{n}$ 排列的**扁盘状 (oblate)** 单轴相。

3.  **双轴相 (Biaxial Phase)**：系统的对称性比单轴相更低，分子在三个相互正交的方向上具有不同的取向概率。这对应于 $Q$ 张量的三个本征值完全互不相同的情况。例如，一个具有本征值 $\{\lambda, -\lambda, 0\}$（其中 $\lambda \neq 0$）的态就是一个双轴态，因为它有三个互异的本征值 [@problem_id:4079568]。

在实际的理论和计算中，直接计算本征值可能不便。因此，我们常常使用 $Q$ 的**标量不变量**来区分相态。因为 $Q$ 是无迹的，其特征多项式仅依赖于两个独立的不变量：
$$
I_2 = \operatorname{tr}(Q^2) = \sum_i \lambda_i^2
$$
$$
I_3 = \operatorname{tr}(Q^3) = \sum_i \lambda_i^3
$$
一个状态是否为单轴相（包括各向同性相作为特例），等价于其特征多项式是否存在重根。这个条件的判别式为零，可以被证明等价于一个关于不变量的优美关系 [@problem_id:4079568]：
$$
(\operatorname{tr} Q^3)^2 = \frac{1}{6}(\operatorname{tr} Q^2)^3
$$
当此等式成立时，系统为单轴相或各向同性相。若 $\operatorname{tr}(Q^2)>0$ 且此等式不成立，则系统必然处于双轴相。对于单轴相，$I_3$ 的符号与标量序参量 $S$ 的符号相同，因此可以用来区分长棒状和扁盘状相。

### 热力学驱动力：Landau-de Gennes 自由能

Beris-Edwards 模型将液晶的演化视为一个趋向于自由能最小值的热力学过程。总自由能 $F[Q]$ 是一个泛函，可以分解为体自由能和弹性自由能两部分。

#### 体自由能与相变

**体自由能密度 $f_b$** 描述了均匀相态下的能量。根据 Landau 的相变理论，$f_b$ 可以展开为序参量 $Q$ 的标量不变量的多项式。为了满足向列相的“头尾对称性”（即 $\boldsymbol{n}$ 与 $-\boldsymbol{n}$ 等价，而 $Q$ 在此变换下不变），展开式中可以包含 $Q$ 的任意次幂的不变量。考虑到旋转不变性，并截断到四阶项，最简约的 $f_b$ 形式为 [@problem_id:4079620]：
$$
f_b(Q) = \frac{A}{2}\operatorname{tr}(Q^2) - \frac{B}{3}\operatorname{tr}(Q^3) + \frac{C}{4}\left(\operatorname{tr}(Q^2)\right)^2
$$
这里的系数具有明确的物理意义：
- **系数 $A$** 通常与温度线性相关，形式为 $A = A_0(T-T^*)$，其中 $A_0  0$ 是一个常数，$T^*$ 是各向同性相的过冷极限温度。在高温下 ($TT^*$)，$A0$，自由能的最小值在 $Q=0$ 处，对应于稳定的各向同性相。当温度降低时，$A$ 减小并可能变为负值，使得非零的 $Q$ 值（即有序相）在能量上更有利。
- **系数 $B$** 是一个正实数 ($B0$)。三阶项的存在破坏了自由能关于 $Q$ 符号的对称性，它使得 $S>0$（长棒状）相的能量低于 $S0$（扁盘状）相，这符合大多数棒状分子液晶的物理实际。至关重要的是，三阶项的存在使得相变成为**一级相变**。
- **系数 $C$** 必须为正 ($C0$)，以保证当序参量很大时自由能有下界，从而确保系统的热力学稳定性。

在一级相变中，有序相和无序相可以在某个转变温度 $T_{NI}$ 共存。在这一点，两相的自由能相等。通过将单轴形式的 $Q$ 代入 $f_b$，我们可以得到一个关于标量序参量 $S$ 的多项式。分析该多项式可以发现，各向同性相与向列相的共存点发生在 $A = B^2 / (27C)$ 处，此时向列相的序参量有一个非零的跳跃，这是一级相变的典型特征 [@problem_id:4079620]。

#### 弹性自由能与 Frank 常数

当序参量场 $Q(\boldsymbol{x},t)$ 在空间上不均匀时，系统会产生额外的**弹性自由能**。其密度 $f_{el}$ 依赖于 $Q$ 的空间梯度 $\nabla Q$。最低阶的梯度项是二次的。在最简单的情况下，即**单弹性常数近似**下，我们只考虑一个不变量：
$$
f_{el} = \frac{L}{2} (\partial_k Q_{ij})(\partial_k Q_{ij})
$$
其中 $L$ 是一个弹性常数，$\partial_k$ 代表对坐标 $x_k$ 的偏导数。这个看似抽象的表达式与经典的 Frank-Oseen 理论中描述指向矢畸变的能量密切相关。Frank-Oseen 理论将弹性畸变分为三种基本模式：**展曲 (splay)**、**扭曲 (twist)** 和**弯曲 (bend)**。

通过将单轴形式的 $Q$（假设 $S$ 在空间上均匀）代入上述 $f_{el}$ 表达式，经过一番推导可以证明 [@problem_id:4079545]：
$$
(\partial_k Q_{ij})(\partial_k Q_{ij}) = 2S^2 \left[ (\nabla\cdot\boldsymbol{n})^2 + (\boldsymbol{n}\cdot(\nabla\times\boldsymbol{n}))^2 + |\boldsymbol{n}\times(\nabla\times\boldsymbol{n})|^2 \right]
$$
等式右边方括号内的三项正是 Frank 理论中对应展曲、扭曲和弯曲能量密度的平方项。将 $f_{el}$ 与单常数近似下的 Frank 能量密度 $f_{Frank} = \frac{K}{2}[(\nabla\cdot\boldsymbol{n})^2 + ...]$ 进行比较，我们得到了 Landau-de Gennes 弹性常数 $L$ 与 Frank 弹性常数 $K$ 之间的映射关系：
$$
K = 2LS^2
$$
这个关系揭示了 $Q$ 张量梯度能如何蕴含着指向矢的宏观畸变模式。更一般地，通过引入更多 $Q$ 梯度的不变量，可以建立一个包含三个不同弹性常数 $L_1, L_2, L_3$ 的 LdG 弹性自由能，并推导出它们与三个 Frank 常数 $K_1, K_2, K_3$ 之间的完整映射关系 [@problem_id:4079552]。这显示了 $Q$ 张量理论的普适性，它不仅能描述单轴相，还能自然地包含更复杂的双轴态和拓扑缺陷，在这些情况下，指向矢 $\boldsymbol{n}$ 的描述会失效。

### 控制方程：流动与序的耦合动力学

Beris-Edwards 模型的核心是一组描述序参量场 $Q(\boldsymbol{x}, t)$ 和流体速度场 $\boldsymbol{u}(\boldsymbol{x}, t)$ 相互作用的偏微分方程。这包括 $Q$ 的演化方程和流体的动量守恒方程。

#### 序参量的演化

$Q$ 张量的演化方程可以概括为一个平衡关系：
$$
(\text{物质导数}) = (\text{可逆流动耦合}) + (\text{不可逆弛豫})
$$

##### 物质导数与客观性

首先，在一个随流体运动的参考系中，$Q$ 的变化率由**物质导数**描述：
$$
\frac{D Q}{D t} = (\partial_t + \boldsymbol{u}\cdot\nabla)Q
$$
然而，这个导数并非**客观的（objective）**或称**物质坐标无关的（frame-indifferent）**。这意味着在不同的旋转参考系下，它的形式会改变。具体来说，如果观察者在一个以角速度张量 $W_{rot}$ 旋转的参考系中，物质导数的变换规律会多出一个与旋转相关的项。物理定律必须在所有惯性系和旋转系下形式相同，因此我们必须构造一个客观的时间导数 [@problem_id:4079540]。

考虑一个纯粹的刚体转动，流场的速度梯度 $\nabla \boldsymbol{u}$ 退化为反对称的涡量张量 $\Omega$。在这种情况下，$Q$ 应该仅仅随着流体旋转，其变化率 $DQ/Dt$ 变为 $\Omega Q - Q \Omega$。一个客观的导数在这种纯旋转下应该为零。这启发我们定义**协转导数（co-rotational derivative）**，或称 Jaumann 导数：
$$
\overset{\triangledown}{Q} = \frac{D Q}{D t} - (\Omega Q - Q \Omega)
$$
可以证明这个导数是客观的。Beris-Edwards 方程的左边正是基于这种协变导数的思想构建的。

##### 流动耦合项 S(W, Q)

在一般流动中，速度梯度 $W_{\alpha\beta} = \partial_\beta u_\alpha$ 可以分解为一个对称的**应变率张量 $D = (W+W^T)/2$** 和一个反对称的**涡量张量 $\Omega = (W-W^T)/2$** [@problem_id:4079601]。涡量 $\Omega$ 引起 $Q$ 的刚性旋转，而应变率 $D$ 引起 $Q$ 的拉伸和形变，从而导致分子重新取向。

描述这种完整流动耦合效应的项记为 $S(W,Q)$。它必须满足以下物理要求：(1) 客观性；(2) 在纯旋转流 ($D=0$) 中退化为 $\Omega Q - Q \Omega$；(3) 能够正确描述应变流对取向的驱动作用；(4) 保持 $Q$ 的对称性和无迹性。

基于这些原则，可以推导出 $S(W,Q)$ 的唯一形式 [@problem_id:4079569] [@problem_id:4079577]，它被称为**广义协转导数**：
$$
S(W,Q) = (\xi D + \Omega)\left(Q + \frac{I}{3}\right) + \left(Q + \frac{I}{3}\right)(\xi D - \Omega) - 2\xi\left(Q + \frac{I}{3}\right)\operatorname{tr}(QD)
$$
这里的 $\xi$ 是一个无量纲的**流动排列参数**，它描述了液晶分子是倾向于在剪切流中沿某个角度排列（flow-aligning, $\xi$ 较大）还是持续翻滚（tumbling, $\xi$ 较小）。值得注意的是，流动耦合作用的对象是 $M = Q+I/3$，这反映了流动直接影响的是完整的二阶矩张量 $\langle \boldsymbol{u}\boldsymbol{u} \rangle$，而非其无迹部分 $Q$ [@problem_id:4079569]。

##### 弛豫项 ΓH

不可逆的弛豫过程驱动系统朝向自由能 $F[Q]$ 的极小值。这个过程可以用一个正比于热力学力的耗散流来描述。与序参量 $Q$ 共轭的热力学力是**分子场 $H$**，定义为自由能泛函对 $Q$ 的变分导数，并投影到对称无迹子空间上：
$$
H = -\left(\frac{\delta F}{\delta Q}\right)^{ST} = -\frac{\delta F}{\delta Q} + \frac{I}{3}\operatorname{tr}\left(\frac{\delta F}{\delta Q}\right)
$$
对于前面定义的 Landau-de Gennes 自由能（包含体自由能和单常数弹性自由能），分子场 $H$ 的具体表达式为 [@problem_id:4079577]：
$$
H = -A Q + B\left(Q^2 - \frac{I}{3}\operatorname{tr}(Q^2)\right) - C Q \operatorname{tr}(Q^2) + L \nabla^2 Q
$$
因此，弛豫项可以写为 $\Gamma H$，其中 $\Gamma$ 是一个正的**旋转黏度**或**迁移率**系数。

##### 完整的 Q 张量演化方程

综合以上各项，我们得到完整的 Beris-Edwards $Q$ 张量演化方程：
$$
(\partial_t + \boldsymbol{u}\cdot\nabla)Q - S(W,Q) = \Gamma H
$$
或者写成协变形式：
$$
\overset{\triangledown}{Q}_{\text{gen}} = \Gamma H
$$
其中 $\overset{\triangledown}{Q}_{\text{gen}} = (\partial_t + \boldsymbol{u}\cdot\nabla)Q - S(W,Q)$ 是广义协变导数。

#### 流场的演化

现在我们转向流体本身。液晶的取向和畸变会反作用于流场，产生额外的应力。这通过修正不可压缩流体的 Navier-Stokes 方程来体现。

##### 动量方程与液晶应力

动量守恒方程的形式为：
$$
\rho\left(\partial_t \boldsymbol{u} + \boldsymbol{u}\cdot\nabla \boldsymbol{u}\right) = -\nabla p + \nabla \cdot \boldsymbol{\sigma}'
$$
其中 $\rho$ 是流体密度，$p$ 是压强，$\boldsymbol{\sigma}'$ 是偏应力张量。在 Beris-Edwards 模型中，偏应力张量被分解为两部分：一部分是牛顿流体常见的黏性应力 $\boldsymbol{\sigma}^{\eta} = 2\eta D$（$\eta$ 是剪切黏度），另一部分是源于液晶取向的**弹性应力 $\boldsymbol{\sigma}^{Q}$**。因此，动量方程写为 [@problem_id:4079593]：
$$
\rho\left(\partial_t \boldsymbol{u} + \boldsymbol{u}\cdot\nabla \boldsymbol{u}\right) = -\nabla p + \eta \nabla^2 \boldsymbol{u} + \nabla \cdot \boldsymbol{\sigma}^{Q}
$$
$\boldsymbol{\sigma}^{Q}$ 本身也由两部分构成：一部分是与分子场 $H$ 相关的**排列应力**，描述了分子取向对流场的反作用；另一部分是与 $Q$ 梯度相关的**Ericksen 应力**，描述了弹性畸变对流场的反作用。

##### 热力学一致性与 Onsager 倒易关系

$\boldsymbol{\sigma}^{Q}$ 的具体形式并非随意构造，它必须与 $Q$ 的演化方程中的流动耦合项 $S(W,Q)$ 通过热力学第二定律联系起来。系统的总能量（动能+自由能）变化率对应于耗散。为了保证在任何流动和取向构型下，系统的熵产率非负，所有可逆的能量交换过程必须相互抵消 [@problem_id:4079615]。

这导致了一个关键的能量平衡条件，即弹性应力所做的功必须与分子场通过流动耦合项交换的能量相互平衡：
$$
\boldsymbol{\sigma}^{Q} : (\nabla \boldsymbol{u}) + H : S(W,Q) = 0
$$
这个条件体现了 **Onsager 倒易关系**，它意味着描述“流动对取向的影响”（由 $S$ 体现）的系数与描述“取向对流动的影响”（由 $\boldsymbol{\sigma}^{Q}$ 体现）的系数是相互关联的。正是这种关系，保证了流动排列参数 $\xi$ 同时出现在 $S$ 和 $\boldsymbol{\sigma}^{Q}$ 的表达式中。

遵循这一原理，可以推导出与 $S(W,Q)$ 相洽的对称弹性应力张量 $\boldsymbol{\sigma}^{Q}$ 的表达式 [@problem_id:4079593]：
$$
\sigma^{Q}_{ij} = -L\,\partial_i Q_{kl}\,\partial_j Q_{kl} - \xi\left[ H_{ik}\,(Q_{kj}+\tfrac{\delta_{kj}}{3}) + (Q_{ik}+\tfrac{\delta_{ik}}{3})\,H_{kj} - 2\,(Q_{ij}+\tfrac{\delta_{ij}}{3})\,Q_{kl}\,H_{lk} \right]
$$
第一项是 Ericksen 应力（在单常数近似下），第二项是排列应力。

### Beris-Edwards 模型总结

综上所述，Beris-Edwards 模型由以下两个耦合的偏微分方程构成：

1.  **$Q$ 张量演化方程**:
    $$
    (\partial_t + \boldsymbol{u}\cdot\nabla)Q - S(\nabla\boldsymbol{u},Q) = \Gamma H
    $$

2.  **动量守恒方程 (修正的 Navier-Stokes 方程)**:
    $$
    \rho\left(\partial_t \boldsymbol{u} + \boldsymbol{u}\cdot\nabla \boldsymbol{u}\right) = -\nabla p + \eta \nabla^2 \boldsymbol{u} + \nabla \cdot \boldsymbol{\sigma}^{Q}
    $$
    同时附带不可压缩条件 $\nabla \cdot \boldsymbol{u} = 0$。

这组方程，连同 $S$, $H$, 和 $\boldsymbol{\sigma}^{Q}$ 的具体表达式，构成了一个封闭的、热力学一致的宏观连续介质模型。它能够描述向列相液晶复杂的流变行为、缺陷动力学以及在流动、电场或表面作用下的各种响应，是计算复杂流体领域一个强大而基础的理论工具。