## 引言
经典力学形式体系是现代[分子动力学](@entry_id:147283)（MD）模拟的理论基石，它为我们描述和预测原子与分子尺度的复杂运动提供了数学语言。虽然[牛顿定律](@entry_id:163541)提供了直观的出发点，但要构建能够在长时间尺度上保持稳定、精确并能正确再现热力学性质的模拟，需要一个更为深刻和强大的理论框架。这一需求正是从[拉格朗日力学](@entry_id:147054)过渡到哈密顿力学，并深入探索其几何结构的根本驱动力。本文旨在系统性地阐明这些经典力学形式体系如何不仅构成了理论物理的优雅篇章，更直接指导了尖端计算模拟算法的设计与实现。

在接下来的内容中，您将踏上一段从基本原理到前沿应用的旅程。第一章“原理与机制”将为您奠定坚实的理论基础，从牛顿力学出发，逐步深入到[拉格朗日形式](@entry_id:145697)、诺特定理，最终聚焦于哈密顿力学的相空间动力学、[辛几何](@entry_id:160783)结构以及处理约束和热浴耦合的挑战。随后的“应用与跨学科[交叉](@entry_id:147634)”章节将理论与实践相连接，展示这些形式体系如何催生出如辛积分器、约束算法和[多时间步](@entry_id:752313)方法等高效的数值工具，并揭示它们如何将微观动力学与宏观[热力学](@entry_id:141121)、[统计力](@entry_id:194984)学乃至量子力学联系起来。最后，“实践操作”部分将提供具体的编程练习，让您亲手实现并验证这些核心概念，将抽象的理论转化为可操作的计算技能。

## 原理与机制

### 从[牛顿力学](@entry_id:162125)到[拉格朗日力学](@entry_id:147054)

经典[分子动力学](@entry_id:147283)的理论基础植根于经典力学。描述一个由 $N$ 个粒子组成的孤立系统的最直接方式是通过[牛顿第二定律](@entry_id:274217)。对于第 $i$ 个粒子，其质量为 $m_i$，位置矢量为 $\mathbf{q}_i(t) \in \mathbb{R}^3$，其运动方程为：

$m_i \ddot{\mathbf{q}}_i(t) = \mathbf{F}_i(\mathbf{q}(t))$

其中，$\ddot{\mathbf{q}}_i$ 是粒子 $i$ 的加速度，$\mathbf{F}_i$ 是作用在其上的总力。在[分子动力学](@entry_id:147283)中，这些力通常是**保守的**，意味着它们可以从一个标量[势能函数](@entry_id:200753) $V(\mathbf{q}_1, \dots, \mathbf{q}_N)$ 导出。力与势能之间的关系定义为：作用在粒子 $i$ 上的力是[势能](@entry_id:748988) $V$ 沿着该粒子坐标方向下降最快的方向，即势能的负梯度。

具体来说，作用于粒子 $i$ 的力 $\mathbf{F}_i$ 是一个三维矢量，其分量是 $V$ 对 $\mathbf{q}_i$ 的三个笛卡尔坐标分量 $(q_{i,1}, q_{i,2}, q_{i,3})$ 的偏导数的负值。数学上，这表示为：

$\mathbf{F}_i(\mathbf{q}) = - \nabla_{\mathbf{q}_i} V(\mathbf{q}_1, \dots, \mathbf{q}_N)$

这里，$\nabla_{\mathbf{q}_i}$ 算符表示对 $\mathbf{q}_i$ 的分量求梯度，即 $\nabla_{\mathbf{q}_i} V = \left( \frac{\partial V}{\partial q_{i,1}}, \frac{\partial V}{\partial q_{i,2}}, \frac{\partial V}{\partial q_{i,3}} \right)$。因此，N[粒子系统](@entry_id:180557)的[牛顿运动方程](@entry_id:165068)组为：

$m_i \ddot{\mathbf{q}}_i = - \nabla_{\mathbf{q}_i} V(\mathbf{q})$ for $i=1, \dots, N$

这个[方程组](@entry_id:193238)构成了分子动力学模拟的核心。我们也可以将所有粒子的力和梯度组织成一个 $3N$ 维的矢量。定义总梯度 $\nabla V(\mathbf{q}) = (\nabla_{\mathbf{q}_1}V(\mathbf{q}), \dots, \nabla_{\mathbf{q}_N}V(\mathbf{q})) \in \mathbb{R}^{3N}$，以及总[力场](@entry_id:147325) $\mathbf{F}(\mathbf{q}) = -\nabla V(\mathbf{q})$。那么，第 $i$ 个粒子的力 $\mathbf{F}_i(\mathbf{q})$ 就是总[力场](@entry_id:147325)矢量 $\mathbf{F}(\mathbf{q})$ 的第 $i$ 个三维矢量块 [@problem_id:3401272]。

虽然牛顿表述直观，但对于处理约束或使用[广义坐标](@entry_id:156576)的复杂系统，**[拉格朗日力学](@entry_id:147054)**提供了一个更优雅和强大的框架。[拉格朗日形式主义](@entry_id:158185)的中心对象是**拉格朗日量** $L$，它被定义为系统的动能 $T$ 与[势能](@entry_id:748988) $V$ 之差：

$L(\mathbf{q}, \dot{\mathbf{q}}) = T(\dot{\mathbf{q}}) - V(\mathbf{q})$

对于一个由 $N$ 个粒子组成的系统，在笛卡尔坐标下，动能是 $T = \sum_{i=1}^N \frac{1}{2} m_i \dot{\mathbf{q}}_i^2$。因此，[拉格朗日量](@entry_id:174593)为：

$L = \sum_{i=1}^N \frac{1}{2} m_i \dot{\mathbf{q}}_i^2 - V(\mathbf{q}_1, \dots, \mathbf{q}_N)$

系统的动力学由**[最小作用量原理](@entry_id:138921)**决定，该原理指出，系统演化的真实路径是使作用量 $S = \int L(\mathbf{q}, \dot{\mathbf{q}}, t) dt$ 取极值的路径。这一原理导出了**[欧拉-拉格朗日方程](@entry_id:137827)**：

$\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_k}\right) - \frac{\partial L}{\partial q_k} = 0$

其中 $q_k$ 代表系统的任何一个[广义坐标](@entry_id:156576)。

[拉格朗日框架](@entry_id:751113)的一个关键优势在于其固有的对称性考虑。**[诺特定理](@entry_id:145690)** (Noether's Theorem) 将系统的每一个连续对称性与一个[守恒量](@entry_id:150267)联系起来。如果作用量在一个连续变换下保持不变，那么就存在一个与之对应的守恒量，称为**[诺特荷](@entry_id:138226)** (Noether charge)。对于一个孤立的分子系统，其势能仅依赖于粒子间的相对位置 [@problem_id:3401358]。
- **空间[平移不变性](@entry_id:195885)**：如果我们将系统中所有粒子的位置移动一个相同的无穷小矢量 $\boldsymbol{a}$，即 $\delta \mathbf{r}_i = \boldsymbol{a}$，[拉格朗日量](@entry_id:174593)保持不变。根据诺特定理，与此对称性相关的守恒量是系统的**总线性动量** $\mathbf{P}_{tot} = \sum_i \mathbf{p}_i$。[诺特荷](@entry_id:138226)的形式为 $Q_{\boldsymbol{a}} = \boldsymbol{a} \cdot \sum_i \mathbf{p}_i$，由于 $\boldsymbol{a}$ 的任意性，这蕴含了 $\mathbf{P}_{tot}$ 的守恒。
- **空间[旋转不变性](@entry_id:137644)**：如果我们将所有粒子的位置绕某个原点进行一次相同的[无穷小旋转](@entry_id:166635) $\delta \mathbf{r}_i = \boldsymbol{\omega} \times \mathbf{r}_i$，[拉格朗日量](@entry_id:174593)同样保持不变。与此对称性相关的守恒量是系统的**[总角动量](@entry_id:155748)** $\mathbf{L}_{tot} = \sum_i \mathbf{r}_i \times \mathbf{p}_i$。其[诺特荷](@entry_id:138226)为 $Q_{\boldsymbol{\omega}} = \boldsymbol{\omega} \cdot \sum_i \mathbf{r}_i \times \mathbf{p}_i$，这意味着 $\mathbf{L}_{tot}$ 是守恒的。

这些[守恒定律](@entry_id:269268)不仅是理论上的基本原则，也是检验[分子动力学模拟](@entry_id:160737)准确性的重要标准。

### [哈密顿表述](@entry_id:276227)：相空间动力学

为了更深入地理解动力学的几何结构并为高级数值方法和[统计力](@entry_id:194984)学奠定基础，我们从[拉格朗日力学](@entry_id:147054)过渡到**[哈密顿力学](@entry_id:146202)**。这一过渡通过**[勒让德变换](@entry_id:146727)** (Legendre transform) 实现，它将描述系统状态的变量从[广义坐标](@entry_id:156576)和[广义速度](@entry_id:178456) $(\mathbf{q}, \dot{\mathbf{q}})$ 转换为[广义坐标](@entry_id:156576)和**[共轭动量](@entry_id:172203)** $(\mathbf{q}, \mathbf{p})$。[共轭动量](@entry_id:172203) $p_k$ 定义为[拉格朗日量](@entry_id:174593)对相应[广义速度](@entry_id:178456)的偏导数：

$p_k = \frac{\partial L}{\partial \dot{q}_k}$

系统的状态不再在[构型空间](@entry_id:149531)中描述，而是在一个维度为两倍的**相空间**中描述。

新的核心函数是**[哈密顿量](@entry_id:172864)** $H$，它代表系统的总能量，并被定义为：

$H(\mathbf{q}, \mathbf{p}) = \sum_k p_k \dot{q}_k - L(\mathbf{q}, \dot{\mathbf{q}})$

为了将 $H$ 完全表示为 $(\mathbf{q}, \mathbf{p})$ 的函数，我们需要利用 $p_k$ 的定义来求解 $\dot{q}_k$ 并代入。对于一个动能为 $T(\mathbf{q}, \dot{\mathbf{q}}) = \frac{1}{2} \dot{\mathbf{q}}^{\mathsf{T}} M(\mathbf{q}) \dot{\mathbf{q}}$ 的系统，其中 $M(\mathbf{q})$ 是一个坐标依赖的**[质量矩阵](@entry_id:177093)**（这在[曲线坐标](@entry_id:178535)中很常见），[共轭动量](@entry_id:172203)为 $\mathbf{p} = M(\mathbf{q})\dot{\mathbf{q}}$。因此，$\dot{\mathbf{q}} = M^{-1}(\mathbf{q})\mathbf{p}$。代入[哈密顿量](@entry_id:172864)的定义，我们得到：

$H(\mathbf{q}, \mathbf{p}) = \frac{1}{2} \mathbf{p}^{\mathsf{T}} M^{-1}(\mathbf{q}) \mathbf{p} + V(\mathbf{q})$

这表明[哈密顿量](@entry_id:172864)确实是动能和势能之和 $H = T + V$。

相空间中的动力学由一组[一阶微分方程](@entry_id:173139)——**哈密顿方程**——描述：

$\dot{q}_k = \frac{\partial H}{\partial p_k}$
$\dot{p}_k = -\frac{\partial H}{\partial q_k}$

对于具有坐标依赖质量矩阵的一般情况，$\dot{p}_k$ 的方程包含一个额外的项，这通常被称为“[虚拟力](@entry_id:165088)”或“度规力”，源于质量矩阵对坐标的依赖性 [@problem_id:3401297]：

$\dot{p}_k = -\frac{\partial V}{\partial q_k} - \frac{1}{2} \sum_{i,j} p_i p_j \frac{\partial M^{-1}_{ij}(\mathbf{q})}{\partial q_k}$

哈密顿形式主义的对称性和优雅性为我们提供了探索相空间流动的强大工具。

### [哈密顿动力学](@entry_id:156273)的几何结构

[哈密顿动力学](@entry_id:156273)的深刻之处在于其丰富的几何结构。相空间的演化并非任意的，而是遵循严格的几何规则。

描述这种结构的一个核心工具是**[泊松括号](@entry_id:151133)** (Poisson bracket)。对于相空间中的任意两个可观测 A 和 B（即 $q$ 和 $p$ 的函数），它们的[泊松括号](@entry_id:151133)定义为：

$\\{A, B\\} = \sum_{i} \left( \frac{\partial A}{\partial q_i} \frac{\partial B}{\partial p_i} - \frac{\partial A}{\partial p_i} \frac{\partial B}{\partial q_i} \right)$

利用泊松括号，任何[可观测量](@entry_id:267133) $A(q,p,t)$ 的时间演化可以简洁地表示为：

$\frac{dA}{dt} = \\{A, H\\} + \frac{\partial A}{\partial t}$

这个方程概括了[哈密顿动力学](@entry_id:156273)。[哈密顿方程](@entry_id:156213)本身就是这个通用方程的特例：$\dot{q}_i = \\{q_i, H\\}$ 和 $\dot{p}_i = \\{p_i, H\\}$。

泊松括号具有一些关键的代数性质，这些性质定义了一个**李代数** (Lie algebra) [@problem_id:3401278]：
1.  **[反对称性](@entry_id:261893)**: $\\{A, B\\} = -\\{B, A\\}$
2.  **[双线性](@entry_id:146819)**: 对每个变量都是线性的。
3.  **[雅可比恒等式](@entry_id:140480)**: $\\{A, \\{B, C\\}\\} + \\{B, \\{C, A\\}\\} + \\{C, \\{A, B\\}\\} = 0$
4.  **[莱布尼茨法则](@entry_id:157949)** (Leibniz rule): $\\{AB, C\\} = A\\{B, C\\} + B\\{A, C\\}$

这些性质确保了相空间动力学的一致性和结构。特别是，泊松括号在**[正则变换](@entry_id:178165)**下是不变的，[正则变换](@entry_id:178165)是保持哈密顿方程形式的相空间[坐标变换](@entry_id:172727)。

[哈密顿动力学](@entry_id:156273)的几何结构的另一种表述是通过**[辛几何](@entry_id:160783)** (symplectic geometry)。相空间不是一个普通的欧几里得空间，而是一个**[辛流形](@entry_id:161608)** (symplectic manifold)，其特点是存在一个称为**辛二形式** (symplectic two-form) 的数学对象，记为 $\omega$。在[正则坐标](@entry_id:175654) $(q,p)$ 下，$\omega$ 的标准形式为：

$\omega = \sum_{i=1}^n dq_i \wedge dp_i$

其中 $\wedge$ 是[外积](@entry_id:147029)。这个二形式可以用来度量相空间中由两个矢量张成的“面积”。[哈密顿动力学](@entry_id:156273)的本质特征是，由哈密顿流（即系统随时间的演化）引起的相空间变换**保持辛二形式不变**。一个保持 $\omega$ 不变的映射 $\Phi$ 被称为**辛映射** (symplectic map)。

辛映射的定义是其[拉回](@entry_id:160816) $\Phi^*\omega$ 等于 $\omega$ 本身。用 Jacobian 矩阵 $D\Phi$ 和 $\omega$ 的[矩阵表示](@entry_id:146025) $\Omega = \begin{pmatrix} 0  I_n \\ -I_n  0 \end{pmatrix}$ 来说，一个映射是辛的，当且仅当它在每一点都满足 [@problem_id:3401334]：

$(D\Phi)^{\mathsf{T}} \Omega (D\Phi) = \Omega$

辛映射的一个重要推论是它们保持相空间体积不变（**刘维尔定理**），因为它们保持刘维尔体积元 $\omega^{\wedge n}$ 不变。然而，反过来不成立：一个保体积的映射不一定是辛的。[辛条件](@entry_id:170870)比保体积更为严格，它施加了关于相空间中“面积”如何被拉伸和旋转的更强约束。

### [数值积分](@entry_id:136578)与约束的挑战

由于分子系统的复杂性，[运动方程](@entry_id:170720)几乎总是需要数值求解。数值积分算法将[时间离散化](@entry_id:169380)为步长为 $\Delta t$ 的小步，并生成一个近似的相空间轨迹。

一个核心挑战来自系统中不同运动模式的时间尺度差异。例如，[共价键](@entry_id:141465)的伸缩[振动频率](@entry_id:199185)非常高（“硬”模式），而分子的整体转动或构象变化则慢得多（“软”模式）。数值积分的稳定性通常由系统中最快的频率 $\omega_{\max}$ 决定。例如，对于广泛使用的**[速度-Verlet](@entry_id:160498)算法**，其稳定条件为 $\omega_{\max} \Delta t  2$ [@problem_id:3401401]。为了保持数值稳定性，时间步长必须非常小（通常在飞秒级别），这使得模拟长时程事件的计算成本非常高昂。

为了克服这个问题，一个常见的策略是**约束** (constrain) 最硬的模式。例如，通过将键长固定，我们可以消除高频的[键伸缩](@entry_id:172690)[振动](@entry_id:267781)。这些约束在数学上表示为一组**[完整约束](@entry_id:140686)** (holonomic constraints) 方程 $C_a(\mathbf{q}) = 0$，它们只依赖于坐标。例如，固定粒子 $i$ 和 $j$ 之间[键长](@entry_id:144592)的约束可以写成 $|\mathbf{r}_i - \mathbf{r}_j|^2 - \ell_{ij}^2 = 0$ [@problem_id:3401312]。

在[拉格朗日框架](@entry_id:751113)中，这些约束通过**[达朗贝尔原理](@entry_id:166612)** (D'Alembert's principle) 和[拉格朗日乘子法](@entry_id:176596)来处理。该原理指出，对于所有允许的[虚位移](@entry_id:168781) $\delta\mathbf{r}_i$（即与约束兼容的位移），约束力的总[虚功](@entry_id:176403)为零。这导致了包含[拉格朗日乘子](@entry_id:142696) $\lambda_a$ 的运动方程：

$\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_k}\right) - \frac{\partial L}{\partial q_k} = \sum_a \lambda_a \frac{\partial C_a}{\partial q_k}$

在实践中，像 SHAKE 或 RATTLE 这样的算法被用来在[数值积分](@entry_id:136578)的每一步迭代求解并满足这些约束。通过移除最快的频率 $\omega_{\max}$，新的最高频率变为 $\omega_{\text{next}}$，从而允许使用更大的时间步长 $\Delta t_{\text{new}} \propto 1/\omega_{\text{next}}$，显著提高了计算效率 [@problem_id:3401401]。

从更根本的哈密顿形式主义角度看，约束的引入使拉格朗日量变得**奇异** (singular)，这使得标准的[勒让德变换](@entry_id:146727)变得复杂。**狄拉克-贝尔格曼** (Dirac-Bergmann) 理论为处理这类[奇异系统](@entry_id:140614)提供了一个完备的框架。该理论区分了两种约束 [@problem_id:3401330]：
- **[第一类约束](@entry_id:168143)** (Primary constraints) 直接源于[奇异拉格朗日量](@entry_id:172486)的勒让德变换的定义。
- **[第二类约束](@entry_id:175584)** (Secondary constraints) 是通过要求[第一类约束](@entry_id:168143)在时间演化中必须保持不变（即它们的时间导数为零）而产生的。

约束又根据它们与其他约束的泊松括号关系分为两类：**第一类** (first-class) 约束与所有其他约束的[泊松括号](@entry_id:151133)（弱）为零，它们通常与[规范对称性](@entry_id:136438)相关。**第二类** (second-class) 约束是那些不满足此条件的约束。对于一个由[第二类约束](@entry_id:175584) $\chi_\alpha$ 组成的系统，它们的泊松括号矩阵 $C_{\alpha\beta} = \\{\chi_\alpha, \chi_\beta\\}$ 是非奇异的。

在这种情况下，标准的[泊松括号](@entry_id:151133)不再适用。狄拉克引入了**[狄拉克括号](@entry_id:178441)** (Dirac bracket)，它修正了泊松括号以自动尊重约束：

$\\{A,B\\}_{D} = \\{A,B\\} - \sum_{\alpha,\beta} \\{A,\chi_\alpha\\} (C^{-1})^{\alpha\beta} \\{\chi_\beta,B\\}$

[运动方程](@entry_id:170720)随后变为 $\dot{A} = \\{A, H\\}_D$。[狄拉克括号](@entry_id:178441)的一个关键性质是，任何函数与[第二类约束](@entry_id:175584)的[狄拉克括号](@entry_id:178441)恒为零，$\\{A, \chi_\alpha\\}_D = 0$。这意味着约束在动力学中被“强” enforces，并且可以在计算括号之前或之后被设为零。这个形式主义为 SHAKE 等约束算法提供了坚实的理论基础。

### 与[热浴](@entry_id:137040)耦合：恒温器与遍历性

[分子动力学模拟](@entry_id:160737)通常旨在模拟处于特定[热力学](@entry_id:141121)系综（如恒定温度和体积的**正则系综** NVT）下的系统，而不仅仅是[能量守恒](@entry_id:140514)的[微正则系综](@entry_id:141513) (NVE)。为了实现这一点，系统需要与一个虚拟的**热浴**耦合，这个过程由**恒温器** (thermostat) 实现。

一个优雅的确定性恒温器是**诺斯-胡佛** (Nosé-Hoover) 恒温器。其思想是引入一个额外的自由度 $s$ (热浴“位置”)及其[共轭动量](@entry_id:172203) $p_s$，并将它们与物理系统耦合。这个扩展系统的动力学由一个**诺斯[扩展哈密顿量](@entry_id:749188)**控制 [@problem_id:3401291]：

$H_{N}(q,p,s,p_{s}) = \sum_{i=1}^{g} \frac{p_{i}^{2}}{2 m_{i} s^{2}} + V(q) + \frac{p_{s}^{2}}{2 Q} + g k_{B} T \ln s$

其中 $g$ 是被控温的自由度数，$Q$ 是[恒温器](@entry_id:169186)的“质量”参数，它决定了耦合的强度和时间尺度。这个扩展系统在它自己的相空间中是[能量守恒](@entry_id:140514)的。然而，物理系统的[时间演化](@entry_id:153943)是通过引入一个缩放的“物理时间” $dt = d\tau/s$ (其中 $\tau$ 是扩展系统的“[虚拟时间](@entry_id:152430)”) 来获得的。

通过这个[时间变换](@entry_id:634205)，并定义物理动量 $P_i = p_i/s$ 和[恒温器](@entry_id:169186)[摩擦系数](@entry_id:150354) $\zeta = p_s/Q$，可以导出一组非哈密顿的[运动方程](@entry_id:170720)，即**诺斯-胡佛方程**：

$\dot{q}_{i} = \frac{P_{i}}{m_{i}}$
$\dot{P}_{i} = F_{i}(q) - \zeta P_{i}$
$\dot{\zeta} = \frac{1}{Q} \left( \sum_{i=1}^{g} \frac{P_{i}^{2}}{m_{i}} - g k_{B} T \right)$

可以证明，这个动力学系统产生的相空间轨迹，其物理坐标 $(q, P)$ 的[稳态分布](@entry_id:149079)正是正则[分布](@entry_id:182848) $\rho(q,P) \propto \exp(-\beta H_{phys})$，其中 $\beta=1/(k_B T)$ 且 $H_{phys}$ 是物理系统的[哈密顿量](@entry_id:172864) [@problem_id:3401291]。

然而，产生正确的稳态分布并不足以保证模拟能够正确地对系综进行抽样。系统还必须是**遍历的** (ergodic)，这意味着单个足够长的轨迹会密集地探索整个能量恒定的相空间[曲面](@entry_id:267450)。对于某些系统，特别是那些具有很少自由度或高度规则性的系统（如[谐振子](@entry_id:155622)），单个诺斯-胡佛恒温器可能无法满足遍历性要求 [@problem_id:3401348]。

以一个受诺斯-胡佛[恒温器](@entry_id:169186)控制的一维谐振子为例，通过对快（[振子](@entry_id:271549)）慢（[恒温器](@entry_id:169186)）变量进行平均，可以证明系统存在一个额外的[守恒量](@entry_id:150267)。这导致相空间轨迹被限制在低维的**[不变环面](@entry_id:194783)上**，而不是探索整个可及的能量[曲面](@entry_id:267450)。因此，系统不是遍历的，无法正确地对[正则系综](@entry_id:142391)进行抽样。

为了解决这个问题，可以采用**诺斯-胡佛链** (Nosé-Hoover chain) 的方法。这种方法将第一个[恒温器](@entry_id:169186)耦合到第二个，第二个耦合到第三个，以此类推，形成一条恒温器链。链中的每个恒温器都作用于前一个。这个过程增加了扩展相空间的维度，并引入了更复杂的[非线性](@entry_id:637147)耦合。对于[谐振子](@entry_id:155622)这样的系统，一个长度至少为2的链条通常足以破坏导致非遍历性的额外[守恒量](@entry_id:150267)，引入**确定性混沌**，从而恢复遍历性，确保对[正则系综](@entry_id:142391)的正确采样 [@problem_id:3401348]。