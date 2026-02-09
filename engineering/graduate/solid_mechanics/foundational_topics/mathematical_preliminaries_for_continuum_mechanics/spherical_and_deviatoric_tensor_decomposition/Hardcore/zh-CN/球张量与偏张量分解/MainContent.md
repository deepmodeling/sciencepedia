## 引言
在固体力学研究中，张量是描述应力、应变等物理量的基本工具，但其多维分量往往难以直接与具体的物理效应联系起来。为了系统地分析材料的力学行为，我们需要一个能够解构张量复杂性的强大数学框架。球张量与偏张量分解正是为此而生，它解决了如何将一个统一的张量场明确地与其物理根源——即物体的体积变化（膨胀或收缩）和形状变化（扭曲或剪切）——联系起来的核心问题。本文将全面介绍这一关键概念。在“原理与机制”一章中，我们将深入探讨分解的数学定义、几何解释及其在应力功率和本构关系中的基本物理意义。随后，在“应用与交叉学科联系”一章中，我们将展示该分解如何在弹性力学、塑性力学乃至计算力学等领域成为构建和理解材料模型的基石。最后，通过“动手实践”部分，读者将有机会通过具体计算和编程练习，将理论知识转化为解决实际问题的能力。

## 原理与机制

在连续介质力学中，理解材料如何响应外部载荷是核心任务。无论是应力、应变还是应变率，描述这些物理量的张量都蕴含着复杂的方向和大小信息。为了系统地分析这些张量，并将其与具体的物理效应（如体积变化和形状扭曲）联系起来，我们将引入一个至关重要的数学工具：**球张量与偏张量分解**（Spherical and Deviatoric Tensor Decomposition）。这种分解方法允许我们将任意一个二阶张量唯一地拆分为两个部分：一个代表均匀、各向同性的“球量”部分，和一个代表非均匀、各向异性的“偏量”部分。本章将深入探讨这一分解的原理、几何意义及其在材料本构模型中的深刻应用。

### 张量的基本分解

考虑一个任意的二阶张量 $\mathbf{A}$（例如应力张量 $\boldsymbol{\sigma}$ 或应变张量 $\boldsymbol{\varepsilon}$）。我们的目标是将其分解为两个部分的总和：一个球张量 $\mathbf{A}_{\mathrm{sph}}$ 和一个偏张量 $\mathbf{A}_{\mathrm{dev}}$。
$$
\mathbf{A} = \mathbf{A}_{\mathrm{sph}} + \mathbf{A}_{\mathrm{dev}}
$$
这个分解并非随意定义，而是基于深刻的物理和数学原则。球张量部分旨在捕捉张量的“体积”或“静水”效应，它应该是一个**各向同性**的张量，即在所有方向上作用相同。在三维空间中，唯一满足此条件的二阶张量是单位张量 $\mathbf{I}$ 的标量倍。因此，我们可以设定 $\mathbf{A}_{\mathrm{sph}} = c\mathbf{I}$，其中 $c$ 是一个标量。

为了确定标量 $c$ 的值，我们施加一个关键的物理约束：球张量部分应承载原始张量 $\mathbf{A}$ 的全部“迹”（trace）。张量的迹，记为 $\operatorname{tr}(\mathbf{A})$，在物理上通常与体积变化或平均正应力相关。因此，我们要求 $\operatorname{tr}(\mathbf{A}_{\mathrm{sph}}) = \operatorname{tr}(\mathbf{A})$。基于 $\mathbf{A}_{\mathrm{sph}} = c\mathbf{I}$，我们可以计算其迹：
$$
\operatorname{tr}(\mathbf{A}_{\mathrm{sph}}) = \operatorname{tr}(c\mathbf{I}) = c \operatorname{tr}(\mathbf{I})
$$
在三维空间中，单位张量 $\mathbf{I}$ 的迹为 $\operatorname{tr}(\mathbf{I}) = 1 + 1 + 1 = 3$。因此，我们有 $3c = \operatorname{tr}(\mathbf{A})$，这唯一地确定了标量 $c = \frac{1}{3}\operatorname{tr}(\mathbf{A})$。

于是，我们得到了**球张量**（spherical tensor）的最终定义：
$$
\mathbf{A}_{\mathrm{sph}} = \frac{1}{3}\operatorname{tr}(\mathbf{A})\mathbf{I}
$$
这个定义是基于各向同性、线性以及迹保持等第一性原理推导出的唯一形式 [@problem_id:2686687]。

相应的，**偏张量**（deviatoric tensor）被定义为原始张量减去其球张量部分：
$$
\mathbf{A}_{\mathrm{dev}} = \mathbf{A} - \mathbf{A}_{\mathrm{sph}} = \mathbf{A} - \frac{1}{3}\operatorname{tr}(\mathbf{A})\mathbf{I}
$$
偏张量的一个决定性特征是其迹恒为零，这表明它不包含任何“体积”信息。我们可以轻松验证这一点：
$$
\operatorname{tr}(\mathbf{A}_{\mathrm{dev}}) = \operatorname{tr}\left(\mathbf{A} - \frac{1}{3}\operatorname{tr}(\mathbf{A})\mathbf{I}\right) = \operatorname{tr}(\mathbf{A}) - \frac{1}{3}\operatorname{tr}(\mathbf{A})\operatorname{tr}(\mathbf{I}) = \operatorname{tr}(\mathbf{A}) - \frac{1}{3}\operatorname{tr}(\mathbf{A}) \cdot 3 = 0
$$
这种分解对于任何二阶张量（无论是否对称）都是唯一的 [@problem_id:2686687]。同时，该分解是**客观的**（objective），意味着它在刚体旋转下具有正确的变换性质，确保了其物理意义的普适性。

### 几何解释：张量空间中的正交投影

为了更深刻地理解这种分解，我们可以将其视为一个几何投影过程 [@problem_id:2686680]。在三维空间中，所有对称二阶张量的集合构成一个六维的向量空间，我们称之为 $\mathrm{Sym}(3)$ [@problem_id:2686697]。我们可以为这个空间配备一个内积，最常用的是**弗罗贝尼乌斯内积**（Frobenius inner product），定义为 $\mathbf{A}:\mathbf{B} = \operatorname{tr}(\mathbf{A}^{\mathsf{T}}\mathbf{B})$。

在这个六维“张量空间”中，所有球张量（形如 $c\mathbf{I}$）构成一个一维子空间，由单位张量 $\mathbf{I}$ 张成。所有偏张量（迹为零的张量）则构成一个五维子空间 [@problem_id:2686697]。

这两个子空间的一个关键性质是它们在弗罗贝尼乌斯内积下是**正交的**。也就是说，任何球张量 $\mathbf{A}_{\mathrm{sph}}$ 与任何偏张量 $\mathbf{B}_{\mathrm{dev}}$ 的内积恒为零：
$$
\mathbf{A}_{\mathrm{sph}}:\mathbf{B}_{\mathrm{dev}} = \left(\frac{1}{3}\operatorname{tr}(\mathbf{A})\mathbf{I}\right):\mathbf{B}_{\mathrm{dev}} = \frac{1}{3}\operatorname{tr}(\mathbf{A})(\mathbf{I}:\mathbf{B}_{\mathrm{dev}}) = \frac{1}{3}\operatorname{tr}(\mathbf{A})\operatorname{tr}(\mathbf{B}_{\mathrm{dev}}) = 0
$$
因为 $\operatorname{tr}(\mathbf{B}_{\mathrm{dev}})=0$。

有了这个正交性，球张量和偏张量的分解就可以被精确地理解为将一个张量 $\mathbf{A}$ 正交投影到这两个相互垂直的子空间上。$\mathbf{A}_{\mathrm{sph}}$ 是 $\mathbf{A}$ 在球张量子空间上的正交投影，而 $\mathbf{A}_{\mathrm{dev}}$ 是 $\mathbf{A}$ 在偏张量子空间上的正交投影。这种投影也具有一个重要的变分意义：在所有迹为零的张量中，$\mathbf{A}_{\mathrm{dev}}$ 是与原始张量 $\mathbf{A}$ “距离”最近的一个，这里的距离由弗罗贝尼乌斯范数定义 [@problem_id:2686687]。

### 在连续介质力学中的物理意义

这种数学上的分解在应用于应力和应变张量时，展现出其强大的物理洞察力。

对于柯西应力张量 $\boldsymbol{\sigma}$，其分解为：
$$
\boldsymbol{\sigma} = p\mathbf{I} + \mathbf{s}
$$
其中，$p = \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$ 被称为**平均应力**或**静水压力**（hydrostatic pressure，有时定义为 $p = -\frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$，取决于符号约定）。$p\mathbf{I}$ 代表一个均匀作用于所有方向的压力状态，它主要引起物体的体积变化。$\mathbf{s} = \operatorname{dev}(\boldsymbol{\sigma})$ 被称为**偏应力张量**，它代表了导致物体形状发生改变（扭曲或剪切）的应力分量 [@problem_id:2630210]。静水压力在任何截面上产生的牵引力都垂直于该截面，而偏应力则可以产生剪切牵引力。

同样地，对于小应变张量 $\boldsymbol{\varepsilon}$，其分解为：
$$
\boldsymbol{\varepsilon} = \varepsilon_m\mathbf{I} + \boldsymbol{\varepsilon}_{\mathrm{dev}}
$$
其中，$\varepsilon_m = \frac{1}{3}\operatorname{tr}(\boldsymbol{\varepsilon})$ 是**平均应变**，它与相对体积变化率 $\Delta V/V_0$ 成正比（$\operatorname{tr}(\boldsymbol{\varepsilon}) \approx \Delta V/V_0$）。$\boldsymbol{\varepsilon}_{\mathrm{dev}} = \operatorname{dev}(\boldsymbol{\varepsilon})$ 则是**偏应变张量**，描述了物体的等体积形状变化（即畸变）。

这种分解最优雅的应用之一体现在**应力功率**（stress power）的计算中。单位体积的应力功率 $\mathcal{P} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}}$（其中 $\dot{\boldsymbol{\varepsilon}}$ 是应变率张量）可以被完美地分解为两部分：
$$
\mathcal{P} = (\mathbf{s} + p\mathbf{I}) : (\dot{\boldsymbol{\varepsilon}}_{\mathrm{dev}} + \dot{\varepsilon}_m\mathbf{I}) = \mathbf{s}:\dot{\boldsymbol{\varepsilon}}_{\mathrm{dev}} + p\mathbf{I}:\dot{\varepsilon}_m\mathbf{I} = \mathbf{s}:\dot{\boldsymbol{\varepsilon}}_{\mathrm{dev}} + p \operatorname{tr}(\dot{\boldsymbol{\varepsilon}})
$$
由于正交性，交叉项（如 $\mathbf{s}:\dot{\varepsilon}_m\mathbf{I}$）为零。这个结果清晰地表明，总的内能耗散率可以分解为由偏应力在偏应变率上做的功（形状改变的功率）和由静水压力在体积应变率上做的功（体积改变的功率）之和 [@problem_id:2686687] [@problem_id:2630210]。

### 在材料本构模型中的应用

球-偏分解在构建和理解材料本构关系时是不可或缺的工具。

#### 各向同性线弹性

对于各向同性线弹性材料，其应力-应变关系（胡克定律）在球-偏分解下变得异常简洁。标准的本构关系 $\boldsymbol{\sigma} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon})\mathbf{I} + 2\mu\boldsymbol{\varepsilon}$（其中 $\lambda$ 和 $\mu$ 是拉梅参数）可以被精确地解耦为两个独立的方程 [@problem_id:2680095]：
$$
p = K \operatorname{tr}(\boldsymbol{\varepsilon})
$$
$$
\mathbf{s} = 2G \boldsymbol{\varepsilon}_{\mathrm{dev}}
$$
第一个方程描述了**体积响应**：静水压力 $p$ 与体积应变 $\operatorname{tr}(\boldsymbol{\varepsilon})$ 成正比，比例系数 $K$ 被称为**体积模量**（bulk modulus）。第二个方程描述了**剪切响应**：偏应力 $\mathbf{s}$ 与偏应变 $\boldsymbol{\varepsilon}_{\mathrm{dev}}$ 成正比，比例系数 $G$ 被称为**剪切模量**（shear modulus），它与拉梅参数的关系为 $G=\mu$。体积模量则为 $K = \lambda + \frac{2}{3}\mu$。

这组解耦的方程深刻地揭示了各向同性材料的特性：其体积响应和形状响应是相互独立的。施加一个纯静水压力只会导致体积变化而没有形状扭曲；施加一个纯剪切应力（一种偏应力）只会导致形状扭曲而没有体积变化。值得强调的是，这种完美的解耦是**材料各向同性**的直接结果。对于各向异性材料，球量和偏量响应之间通常存在耦合，例如，施加静水压力也可能引起剪切变形 [@problem_id:2920794]。

#### 塑性力学与应力不变量

在塑性理论中，尤其对于金属材料，实验表明材料的屈服（进入塑性状态）主要由形状改变引起，而对静水压力不敏感。球-偏分解为描述这一现象提供了完美的框架。

为了建立不依赖于坐标系的屈服准则，我们需要使用应力张量的不变量。一个特别有用的不变量集合是 $(\mathrm{I}_1, \mathrm{J}_2, \mathrm{J}_3)$ [@problem_id:2686708]：
- $\mathrm{I}_1 = \operatorname{tr}(\boldsymbol{\sigma})$：应力张量的第一不变量，与平均应力成正比。
- $\mathrm{J}_2 = \frac{1}{2}\mathbf{s}:\mathbf{s}$：偏应力张量的第二不变量。它度量了偏应力状态的“强度”或“大小”。
- $\mathrm{J}_3 = \det(\mathbf{s})$：偏应力张量的第三不变量。它描述了偏应力状态的“模式”，例如区分三轴拉伸和三轴压缩。

由于 $\mathrm{J}_2$ 和 $\mathrm{J}_3$ 仅依赖于偏应力 $\mathbf{s}$，它们对于任意的静水压力叠加都是不变的。例如，对一个应力状态 $\boldsymbol{\sigma}$ 施加一个静水压力 $p_0\mathbf{I}$，新的应力为 $\boldsymbol{\sigma}' = \boldsymbol{\sigma} + p_0\mathbf{I}$，其偏应力部分不变，$\mathbf{s}' = \mathbf{s}$。因此，$\mathrm{J}_2$ 和 $\mathrm{J}_3$ 也保持不变 [@problem_id:2686708]。

这完美地解释了为何像冯·米塞斯（von Mises）这样的压力不敏感屈服准则仅依赖于 $\mathrm{J}_2$（屈服条件为 $\sqrt{3\mathrm{J}_2} \ge \sigma_Y$，其中 $\sigma_Y$ 是单轴屈服应力）。根据该准则，一个纯静水压力状态（$\mathbf{s}=\mathbf{0}$，因此 $\mathrm{J}_2=0$）永远不会引起材料屈服 [@problem_id:2630210]。

### 扩展与高等专题

#### 有限应变运动学

在小应变理论中，应变的叠加是线性的，球-偏分解是简单的加法分解。然而，在有限应变理论中，情况变得更为复杂。运动的描述由变形梯度 $\mathbf{F}$ 给出，其行列式 $J = \det(\mathbf{F})$ 代表了体积变化比。

在有限应变中，我们通常采用**乘法分解**来分离体积和形状变化。变形梯度可以被分解为 $F = J^{1/3}\bar{\mathbf{F}}$，其中 $\bar{\mathbf{F}}$ 是保体积（isochoric）或等容的变形部分，满足 $\det(\bar{\mathbf{F}})=1$。这种分解可以传递到应变度量，例如右柯西-格林张量 $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 和左柯西-格林张量 $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}}$，它们可以被乘法分解为 $B = J^{2/3}\bar{\mathbf{B}}$，其中 $\det(\bar{\mathbf{B}})=1$ [@problem_id:2686691]。

有趣的是，这种乘法分解与**对数应变**（logarithmic strain）的加法分解有着优美的联系。可以证明，对数应变张量 $\ln(\mathbf{B})$ 的偏量部分恰好是等容部分 $\bar{\mathbf{B}}$ 的对数，即 $\operatorname{dev}(\ln \mathbf{B}) = \ln \bar{\mathbf{B}}$ [@problem_id:2686691]。

需要特别注意的是，在有限应变下，直接对一个有限应变张量（如 $\mathbf{C}$）进行代数上的加法偏量分解，即计算 $\operatorname{dev}(\mathbf{C}) = \mathbf{C} - \frac{1}{3}\operatorname{tr}(\mathbf{C})\mathbf{I}$，所得的结果与基于运动学乘法分解得到的物理等容部分并不一致。一个具体的计算例子可以清晰地展示这种差异，强调了在有限应变分析中区分代数运算和物理分解的重要性 [@problem_id:2686684]。

#### 内积选择的角色

最后，我们回到分解的几何本质。张量的代数分解 $\mathbf{A} = \mathbf{A}_{\mathrm{sph}} + \mathbf{A}_{\mathrm{dev}}$ 是一个普适的定义，不依赖于任何度量。然而，球量子空间和偏量子空间之间的**正交性**，是依赖于我们所选择的内积的。

对于标准的弗罗贝尼乌斯内积，这种正交性成立。但如果我们引入一个由四阶张量 $\mathbb{M}$ 定义的更广义的内积 $\langle \mathbf{A}, \mathbf{B} \rangle_{\mathbb{M}} = \mathbf{A}:\mathbb{M}:\mathbf{B}$，正交性就不再是理所当然的。可以证明，只有当张量 $\mathbb{M}$ 满足特定条件时（即 $\mathbb{M}:\mathbf{I}$ 是一个球张量），球-偏子空间才在该内积下保持正交 [@problem_id:2630198]。这个条件对于各向同性的 $\mathbb{M}$ 总是成立，但对于一般的各向异性张量则不然。这再次从数学上呼应了物理上的观察：体积与形状响应的解耦，其根源在于材料的各向同性对称性。