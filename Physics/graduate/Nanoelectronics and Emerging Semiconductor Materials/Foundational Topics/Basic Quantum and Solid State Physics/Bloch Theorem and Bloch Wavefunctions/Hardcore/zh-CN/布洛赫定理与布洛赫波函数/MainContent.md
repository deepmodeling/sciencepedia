## 引言
在晶体固体的微观世界中，数以万亿计的电子遵循着深刻而优美的量子力学规律。理解这些电子的行为方式是掌控[材料性质](@entry_id:146723)、设计新型电子和光电子器件的关键。[布洛赫定理](@entry_id:137461)正是揭示这一奥秘的核心理论，它阐明了[晶格](@entry_id:148274)的周期性如何从根本上决定了电子的量子态。然而，从抽象的数学定理到对真实材料的预测和应用之间，存在着一条需要系统学习和理解的知识路径。本文旨在搭建这座桥梁，引领读者从[布洛赫定理](@entry_id:137461)的对称性根源出发，逐步深入其物理内涵和广阔的应用前景。

本文将通过三个核心章节，全面解析[布洛赫定理](@entry_id:137461)及其衍生概念。在“原理与机制”一章中，我们将从[晶格](@entry_id:148274)的平移对称性出发，严谨推导[布洛赫波函数](@entry_id:1121709)的结构，并通过近自由电子和[紧束缚](@entry_id:142573)两种模型，直观地理解能带与[能隙](@entry_id:138445)的形成机制。接着，在“应用与跨学科连接”一章，我们将展示该理论如何被用于解释材料的宏观性质，如何指导现代能带工程（如莫尔[超晶格](@entry_id:200197)），以及它如何成为[计算材料科学](@entry_id:1122793)和拓扑物态等前沿领域的理论基石。最后，“动手实践”部分将提供一系列计算练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一完整的学习旅程，读者将构建起对固体中电子行为的坚实理解。

## 原理与机制

本章旨在深入探讨晶体中电子态的核心组织原则——[布洛赫定理](@entry_id:137461)，并阐释其背后的物理机制。我们将从[晶格](@entry_id:148274)的[平移对称性](@entry_id:171614)出发，系统地推导出[布洛赫波函数](@entry_id:1121709)的结构，并介绍两种互补的理论模型——[近自由电子模型](@entry_id:138124)和[紧束缚模型](@entry_id:143446)——来理解能带是如何形成的。此外，我们还将阐明晶体动量的概念及其守恒定律，并讨论对称性如何决定能带的交叉与否，这些都是理解纳米电子学和新兴半导体材料中量子现象的基础。

### [布洛赫定理](@entry_id:137461)的对称性基础

晶体最显著的特征是其原子排布在空间中呈现周期性。对于一个理想的、无限延伸的晶体，其内部的势场 $V(\mathbf{r})$ 必然反映了这种周期性。这意味着，当我们将整个晶体沿任意一个布拉维格矢 $\mathbf{R}$ 平移时，势场保持不变。数学上，这可以表示为：

$V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r})$

其中 $\mathbf{R} = n_1\mathbf{a}_1 + n_2\mathbf{a}_2 + n_3\mathbf{a}_3$ 是由基矢 $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$ 和整数 $n_i$ 构成的任意格矢。

在单电子近似下，描述电子行为的哈密顿算符为：

$$H = -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r})$$

为了研究[平移对称性](@entry_id:171614)的后果，我们引入一个**[晶格](@entry_id:148274)[平移算符](@entry_id:756122)** $\hat{T}_{\mathbf{R}}$，其作用于任意[波函数](@entry_id:201714) $\psi(\mathbf{r})$ 的效果是将其空间坐标移动一个格矢 $\mathbf{R}$：

$$\hat{T}_{\mathbf{R}}\psi(\mathbf{r}) = \psi(\mathbf{r} + \mathbf{R})$$

现在，我们来考察哈密顿算符 $H$ 与[平移算符](@entry_id:756122) $\hat{T}_{\mathbf{R}}$ 之间的[对易关系](@entry_id:136780) $[H, \hat{T}_{\mathbf{R}}]$。动能部分 $-\frac{\hbar^2}{2m}\nabla^2$ 是一个[微分](@entry_id:158422)算符，它对于任意空间位移都是不变的，因此它与 $\hat{T}_{\mathbf{R}}$ 对易。势能部分 $V(\mathbf{r})$ 与 $\hat{T}_{\mathbf{R}}$ 的对易性则直接源于[势场](@entry_id:143025)的周期性。具体来说，作用于一个任意[测试函数](@entry_id:166589) $\psi(\mathbf{r})$ 上：

$[\hat{V}, \hat{T}_{\mathbf{R}}]\psi(\mathbf{r}) = V(\mathbf{r})\hat{T}_{\mathbf{R}}\psi(\mathbf{r}) - \hat{T}_{\mathbf{R}}(V(\mathbf{r})\psi(\mathbf{r})) = V(\mathbf{r})\psi(\mathbf{r} + \mathbf{R}) - V(\mathbf{r} + \mathbf{R})\psi(\mathbf{r} + \mathbf{R})$

由于 $V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r})$，上式右边两项相减为零。因此，势能算符也与[平移算符](@entry_id:756122)对易。因为[哈密顿算符](@entry_id:144286)的两个部分都与 $\hat{T}_{\mathbf{R}}$ 对易，所以哈密顿算符本身也必然与之对易 。

$$[H, \hat{T}_{\mathbf{R}}] = 0$$

这个[对易关系](@entry_id:136780)是[固体能带理论](@entry_id:144910)的基石。根据量子力学的基本原理，如果两个算符对易，它们就拥有一组共同的[本征函数](@entry_id:154705)。此外，所有的[晶格](@entry_id:148274)[平移算符](@entry_id:756122)之间也相互对易（$\hat{T}_{\mathbf{R}_1}\hat{T}_{\mathbf{R}_2} = \hat{T}_{\mathbf{R}_2}\hat{T}_{\mathbf{R}_1}$），因为平移的次序无关紧要。这意味着我们可以找到一组同时是[哈密顿算符](@entry_id:144286) $H$ 和所有[平移算符](@entry_id:756122) $\hat{T}_{\mathbf{R}}$ 的[本征函数](@entry_id:154705)。设 $\psi(\mathbf{r})$ 是这样一个共同[本征函数](@entry_id:154705)，那么：

$$H\psi(\mathbf{r}) = E\psi(\mathbf{r})$$

$$\hat{T}_{\mathbf{R}}\psi(\mathbf{r}) = c(\mathbf{R})\psi(\mathbf{r})$$

其中 $E$ 是[能量本征值](@entry_id:144381)，而 $c(\mathbf{R})$ 是对应于[平移算符](@entry_id:756122) $\hat{T}_{\mathbf{R}}$ 的本征值。由于平移操作保持了[波函数](@entry_id:201714)的归一性，[平移算符](@entry_id:756122)是幺正算符，其本征值的模必须为1，即 $|c(\mathbf{R})|^2 = 1$。此外，平移的[组合性](@entry_id:637804)质 $\hat{T}_{\mathbf{R}_1}\hat{T}_{\mathbf{R}_2} = \hat{T}_{\mathbf{R}_1+\mathbf{R}_2}$ 要求其本征值满足 $c(\mathbf{R}_1)c(\mathbf{R}_2) = c(\mathbf{R}_1+\mathbf{R}_2)$。满足这些条件的唯一数学形式是[复指数函数](@entry_id:169796)。因此，本征值可以写成：

$$c(\mathbf{R}) = \exp(i\mathbf{k}\cdot\mathbf{R})$$

这里，我们引入了一个新的矢量 $\mathbf{k}$，它标志着[波函数](@entry_id:201714)在[晶格](@entry_id:148274)平移下的变换性质。这个矢量 $\mathbf{k}$ 被称为**[晶体动量](@entry_id:136369)**或**[布洛赫波矢](@entry_id:746866)**。

### [布洛赫波函数](@entry_id:1121709)

综合上述推导，我们得到了**[布洛赫定理](@entry_id:137461)**的第一个表述：在[周期性势场](@entry_id:140652)中，[哈密顿算符](@entry_id:144286)的[本征函数](@entry_id:154705) $\psi(\mathbf{r})$ 必然满足如下条件：

$$\psi(\mathbf{r} + \mathbf{R}) = \exp(i\mathbf{k}\cdot\mathbf{R})\psi(\mathbf{r})$$

这个方程表明，晶体中的电子[波函数](@entry_id:201714)并非像原子中的局域[波函数](@entry_id:201714)，也不是严格周期性的，而是在一个[晶格](@entry_id:148274)平移下仅仅获得一个相位因子，这种性质被称为**[准周期性](@entry_id:272343)**。一个常见的误解是认为电子[波函数](@entry_id:201714)本身必须是[晶格](@entry_id:148274)周期性的，即 $\psi(\mathbf{r}+\mathbf{R}) = \psi(\mathbf{r})$。这种情况仅在特殊情形下发生，即相位因子 $\exp(i\mathbf{k}\cdot\mathbf{R})$ 对所有 $\mathbf{R}$ 都等于1，这要求 $\mathbf{k}$ 是一个[倒格矢](@entry_id:263351)（例如 $\mathbf{k}=0$）。

[布洛赫定理](@entry_id:137461)还有一个等价且更为常用的表述。我们可以将[波函数](@entry_id:201714) $\psi(\mathbf{r})$ 写成如下形式：

$$\psi_{n\mathbf{k}}(\mathbf{r}) = \exp(i\mathbf{k}\cdot\mathbf{r})u_{n\mathbf{k}}(\mathbf{r})$$

其中 $u_{n\mathbf{k}}(\mathbf{r})$ 是一个具有[晶格](@entry_id:148274)周期性的函数，即 $u_{n\mathbf{k}}(\mathbf{r} + \mathbf{R}) = u_{n\mathbf{k}}(\mathbf{r})$ 。这种形式将波[函数分解](@entry_id:197881)为一个纯平面波部分 $\exp(i\mathbf{k}\cdot\mathbf{r})$ 和一个[晶格](@entry_id:148274)周期调制部分 $u_{n\mathbf{k}}(\mathbf{r})$ 的乘积。这种形式的正确性可以通过将其代入[准周期性](@entry_id:272343)条件中得到验证。

在[布洛赫波函数](@entry_id:1121709)的标记 $\psi_{n\mathbf{k}}$ 中，包含了两个重要的量子数：
1.  **[晶体动量](@entry_id:136369) $\mathbf{k}$**：这是一个连续的矢量，定义在**倒易空间**中。它描述了[波函数](@entry_id:201714)在[晶格](@entry_id:148274)平移下的对称性变换规律，是平移对称群的[不可约表示](@entry_id:263310)的标记。
2.  **能带指数 $n$**：对于给定的[晶体动量](@entry_id:136369) $\mathbf{k}$，薛定谔方程会有一系列分立的[能量本征值](@entry_id:144381)。能带指数 $n$（通常为整数 $n=1, 2, 3, \dots$）就是用来标记这些不同[能量本征态](@entry_id:152154)的[量子数](@entry_id:145558)。对应的[能量本征值](@entry_id:144381) $E_n(\mathbf{k})$ 随着 $\mathbf{k}$ 的变化而形成连续的曲线，称为**能带**或**[能带结构](@entry_id:139379)** 。

晶体动量 $\mathbf{k}$ 的定义存在冗余。如果我们将 $\mathbf{k}$ 替换为 $\mathbf{k}+\mathbf{G}$，其中 $\mathbf{G}$ 是任意一个**[倒格矢](@entry_id:263351)**（定义为满足 $\exp(i\mathbf{G}\cdot\mathbf{R})=1$ 对所有 $\mathbf{R}$ 成立的矢量），[平移算符](@entry_id:756122)的本征值将保持不变：

$$\exp(i(\mathbf{k}+\mathbf{G})\cdot\mathbf{R}) = \exp(i\mathbf{k}\cdot\mathbf{R})\exp(i\mathbf{G}\cdot\mathbf{R}) = \exp(i\mathbf{k}\cdot\mathbf{R})$$

这意味着 $\mathbf{k}$ 和 $\mathbf{k}+\mathbf{G}$ 描述的是完全相同的[平移对称性](@entry_id:171614)。因此，所有物理性质，特别是能量，在[倒易空间](@entry_id:754151)中也必须是周期的：

$$E_n(\mathbf{k}) = E_n(\mathbf{k}+\mathbf{G})$$

为了消除这种冗余，我们通常只考虑倒易空间中的一个原胞，这个特殊选择的原胞被称为**[第一布里渊区](@entry_id:269110)**。

值得强调的是，[布洛赫波函数](@entry_id:1121709)描述的是在整个晶体中延展的[行波](@entry_id:1133416)状态，它携带净的[概率流](@entry_id:907649)（除非在[布里渊区](@entry_id:142395)的某些[高对称点](@entry_id:1126099)，如边界，此时可以形成驻波）。这与束缚在缺陷或杂质周围的局域态形成鲜明对比，后者破坏了[晶格](@entry_id:148274)的[平移对称性](@entry_id:171614)，因此不具备确定的晶体动量 $\mathbf{k}$。另一类相关的局域函数是**[瓦尼尔函数](@entry_id:145994) (Wannier functions)**，它们可以通过对某个孤立能带内的所有[布洛赫函数](@entry_id:189422)进行傅里叶变换来构造。每个[瓦尼尔函数](@entry_id:145994)局域在某个[晶格](@entry_id:148274)格点附近，但它们不是哈密顿量的[本征态](@entry_id:149904)，也不具有确定的晶体动量。相反，一个[瓦尼尔函数](@entry_id:145994)在[晶格](@entry_id:148274)[平移算符](@entry_id:756122)作用下会变换到相邻格点的[瓦尼尔函数](@entry_id:145994)上 。

### [电子能带](@entry_id:175335)的形成模型

[布洛赫定理](@entry_id:137461)描述了晶体中电子[波函数](@entry_id:201714)的普适形式，但并未说明[能带结构](@entry_id:139379) $E_n(\mathbf{k})$ 的具体形态。为了理解能带的形成机制，物理学家发展了两种互补的极限模型。

#### [近自由电子模型](@entry_id:138124)

近自由电子 (Nearly-Free Electron, NFE) 模型从[自由电子气](@entry_id:145649)出发，将[晶格](@entry_id:148274)的周期性势场 $V(\mathbf{r})$ 视为一个微扰。在没有[势场](@entry_id:143025)的情况下（$V(\mathbf{r})=0$），电子是自由的，其[波函数](@entry_id:201714)是[平面波](@entry_id:189798) $\psi_{\mathbf{k}}(\mathbf{r}) \propto \exp(i\mathbf{k}\cdot\mathbf{r})$，能量为 $E^{(0)}(\mathbf{k}) = \frac{\hbar^2|\mathbf{k}|^2}{2m}$。这是一个简单的抛物线色散关系。

当引入一个弱的周期性势场时，情况发生了改变。我们可以将[周期势](@entry_id:140652)场 $V(\mathbf{r})$ 分解为[傅里叶级数](@entry_id:139455)，其分量只包含[倒格矢](@entry_id:263351) $\mathbf{G}$：

$$V(\mathbf{r}) = \sum_{\mathbf{G}} V_{\mathbf{G}}\exp(i\mathbf{G}\cdot\mathbf{r})$$

在[平面波基](@entry_id:140187)矢 $\{|\mathbf{k}\rangle\}$ 下，[哈密顿量](@entry_id:144286)的[矩阵元](@entry_id:186505)可以被计算出来。动能项是对角的，而势能项的[矩阵元](@entry_id:186505)为 $\langle \mathbf{k}' | V | \mathbf{k} \rangle = V_{\mathbf{k}'-\mathbf{k}}$ 。

这个结果表明，周期势场的一个傅里叶分量 $V_{\mathbf{G}}$ 会耦合[波矢](@entry_id:178620)相差一个[倒格矢](@entry_id:263351) $\mathbf{G}$ 的两个[平面波](@entry_id:189798)态，即 $|\mathbf{k}\rangle$ 和 $|\mathbf{k}+\mathbf{G}\rangle$。

在大多数情况下，这种耦合效应很小，因为不同波矢的自由电子态能量相差很大。然而，在布里渊区的边界上，情况截然不同。布里渊区边界由满足**[布拉格衍射](@entry_id:148063)条件**的 $\mathbf{k}$ 点构成，例如满足 $|\mathbf{k}| = |\mathbf{k}-\mathbf{G}|$ 的点。在这些点上，两个平面波态 $|\mathbf{k}\rangle$ 和 $|\mathbf{k}-\mathbf{G}\rangle$ 的自由电子能量是简并的，即 $E^{(0)}(\mathbf{k}) = E^{(0)}(\mathbf{k}-\mathbf{G})$。

在这种简并或[近简并](@entry_id:172107)的情况下，微小的[势场](@entry_id:143025)耦合 $V_{\mathbf{G}}$ 也会产生显著的影响。我们可以构建一个仅包含这两个[简并态](@entry_id:274678)的 $2 \times 2$ [哈密顿矩阵](@entry_id:136233)来进行分析 ：

$$H_{\text{eff}} = \begin{pmatrix} E^{(0)}(\mathbf{k})  V_{-\mathbf{G}} \\ V_{\mathbf{G}}  E^{(0)}(\mathbf{k}-\mathbf{G}) \end{pmatrix}$$

在简并点，对角元相等，记为 $E_0$。由于势场是实函数，$V_{-\mathbf{G}} = V_{\mathbf{G}}^*$。求解该矩阵的本征值，我们得到两个新的能量值：

$$E_{\pm} = E_0 \pm |V_{\mathbf{G}}|$$

原本简并的能级被势场劈裂开，形成了一个宽度为 $\Delta E = 2|V_{\mathbf{G}}|$ 的**[能隙](@entry_id:138445) (band gap)**   。这个[能隙](@entry_id:138445)的出现是[周期势](@entry_id:140652)场作用的直接后果，它禁止了电子拥有该能量范围内的能量。这个过程在所有布里渊区边界上都会发生，从而将连续的自由电子抛物线能谱切割成一系列分离的能带。

#### 紧束缚模型

[紧束缚](@entry_id:142573) (Tight-Binding, TB) 模型从与[近自由电子模型](@entry_id:138124)相反的极限出发。它假设电子最初被紧紧地束缚在孤立的原子上，其[波函数](@entry_id:201714)是局域的[原子轨道](@entry_id:140819) $\varphi_{\alpha}(\mathbf{r}-\mathbf{R})$，其中 $\alpha$ 是轨道类型（如s, p, d），$\mathbf{R}$ 是原子位置。当这些原子组成[晶格](@entry_id:148274)时，相邻原子上的电子[波函数](@entry_id:201714)会发生微弱的交叠，使得电子有机会从一个原子“隧穿”或“跃迁”到另一个原子。

为了构建满足[布洛赫定理](@entry_id:137461)的[波函数](@entry_id:201714)，我们利用[平移对称性](@entry_id:171614)，将局域的[原子轨道线性组合](@entry_id:151829)成**布洛赫和 (Bloch sum)**：

$$\phi_{\alpha\mathbf{k}}(\mathbf{r}) = \frac{1}{\sqrt{N}}\sum_{\mathbf{R}} \exp(i\mathbf{k}\cdot \mathbf{R}) \varphi_{\alpha}(\mathbf{r}-\mathbf{R})$$

其中 $N$ 是[晶格](@entry_id:148274)中的[原胞](@entry_id:159354)总数。通过直接代入验证，可以证明这个构造出的[波函数](@entry_id:201714)严格满足布洛赫条件 $\phi_{\alpha\mathbf{k}}(\mathbf{r}+\mathbf{T}) = \exp(i\mathbf{k}\cdot\mathbf{T})\phi_{\alpha\mathbf{k}}(\mathbf{r})$ 。

在布洛赫和的基底下，[哈密顿矩阵元](@entry_id:201928) $\langle \phi_{\alpha\mathbf{k}} | H | \phi_{\beta\mathbf{k}'} \rangle$ 会因为[平移对称性](@entry_id:171614)而变得对角化。具体来说，只有当 $\mathbf{k}=\mathbf{k}'$ 时[矩阵元](@entry_id:186505)才非零。这意味着对于每个 $\mathbf{k}$，哈密顿量都化为一个小型的矩阵（其维度等于每个[原胞](@entry_id:159354)中的轨道数）。对角化这个小矩阵，就可以得到该 $\mathbf{k}$ 点的能谱 $E_n(\mathbf{k})$。

在这种模型中，能带的宽度直接与原子间的**[跃迁积分](@entry_id:1126166) (hopping integral)** 有关，后者描述了电子从一个格点跃迁到另一个格点的难易程度。最终，能带的[色散关系](@entry_id:140395) $E(\mathbf{k})$ 可以表示为[跃迁积分](@entry_id:1126166)的傅里叶变换，这清晰地揭示了电子的[离域](@entry_id:183327)运动（跃迁）是如何导致分立的[原子能级](@entry_id:148255)展宽为连续的能量带的 。

### 晶体动量及其守恒

我们需要再次强调，[晶体动量](@entry_id:136369) $\hbar\mathbf{k}$ 并非电子的真实力学动量 $\mathbf{p}$。在[周期势](@entry_id:140652)场中，由于连续平移对称性被破坏，力学动量本身不再是[守恒量](@entry_id:161475)。电子不断地与[晶格](@entry_id:148274)势场相互作用，交换动量。

然而，[晶体动量](@entry_id:136369) $\mathbf{k}$ 作为[平移对称性](@entry_id:171614)的量子数，在完美周期性晶体中是一个[守恒量](@entry_id:161475)。这是因为[哈密顿量](@entry_id:144286)在布洛赫表象下是块对角的，它不会将一个具有[晶体动量](@entry_id:136369) $\mathbf{k}$ 的[电子散射](@entry_id:159023)到另一个具有不同[晶体动量](@entry_id:136369) $\mathbf{k}'$ 的态上 。

当晶体中存在额外的周期性微扰时，例如由[晶格振动](@entry_id:140970)（声子）或另一个周期性外场引起的散射，晶体动量的守恒定律需要被修正。假设一个电子最初处于[布洛赫态](@entry_id:147552) $|\psi_{\mathbf{k}}\rangle$，受到一个与[晶格](@entry_id:148274)具有相同周期性的散射势 $W(\mathbf{r})$ 的作用，跃迁到末态 $|\psi_{\mathbf{k}'}\rangle$。这个过程的跃迁[矩阵元](@entry_id:186505)为：

$$W_{\mathbf{k'k}} = \langle \psi_{\mathbf{k'}} | W | \psi_{\mathbf{k}} \rangle = \int \psi_{\mathbf{k'}}^{*}(\mathbf{r}) W(\mathbf{r}) \psi_{\mathbf{k}}(\mathbf{r}) d^3\mathbf{r}$$

由于 $\psi_{\mathbf{k}}$, $\psi_{\mathbf{k'}}$ 和 $W(\mathbf{r})$ 都具有与[晶格](@entry_id:148274)相关的周期性，这个积分的计算结果表明，只有当初始和末态的晶体动量满足以下[选择定则](@entry_id:140784)时，跃迁才可能发生 ：

$$\mathbf{k'} = \mathbf{k} + \mathbf{G}$$

其中 $\mathbf{G}$ 是一个[倒格矢](@entry_id:263351)。这个定律被称为**[晶体动量守恒](@entry_id:145588)**。它意味着在与周期性格点的相互作用中，电子可以从[晶格](@entry_id:148274)整体获得或失去一个大小为 $\hbar\mathbf{G}$ 的“动量包”。当 $\mathbf{G}=0$ 时，称为**正常过程**；当 $\mathbf{G} \neq 0$ 时，称为**[乌姆克拉普过程](@entry_id:145784) (Umklapp process)**。这个定律从根本上源于系统的离散[平移对称性](@entry_id:171614)，可以通过两种等价的方式理解：
1.  **对称性论证**：由于总哈密顿量（包含散射势）仍然是[晶格](@entry_id:148274)周期的，它仍然与[平移算符](@entry_id:756122) $\hat{T}_{\mathbf{R}}$ 对易。因此，$\hat{T}_{\mathbf{R}}$ 的本征值 $\exp(i\mathbf{k}\cdot\mathbf{R})$ 必须在跃迁前后保持不变，这直接导致 $\mathbf{k'} = \mathbf{k} + \mathbf{G}$。
2.  **矩阵元论证**：周期性散射势 $W(\mathbf{r})$ 的[傅里叶级数](@entry_id:139455)只包含[倒格矢](@entry_id:263351)分量。在计算跃迁矩阵元时，这一特性导致了动量空间中的[选择定则](@entry_id:140784)，即动量转移只能是 $\hbar\mathbf{G}$ 的整数倍 。

### [能带拓扑](@entry_id:182035)：交叉与反交叉

[能带结构](@entry_id:139379) $E_n(\mathbf{k})$ 的复杂性不仅在于其形状，还在于不同能带之间的相互关系，特别是它们的交叉行为。两条能带在 $\mathbf{k}$ 空间中是相交还是“相互避开”（形成反交叉），由晶体在相应 $\mathbf{k}$ 点的对称性严格决定。

描述在特定 $\mathbf{k}$ 点对称性的数学工具是**[波矢](@entry_id:178620)的“[小群](@entry_id:198763)” (little group of the wavevector)**。小群包含了[晶体点群](@entry_id:183880)中所有能使 $\mathbf{k}$ 保持不变（或仅改变一个[倒格矢](@entry_id:263351)）的[对称操作](@entry_id:143398)。给定 $\mathbf{k}$ 点的[布洛赫函数](@entry_id:189422)可以按照其小群的**[不可约表示](@entry_id:263310) (irreducible representations, irreps)** 来分类。

**冯·诺依曼-维格纳非交叉定则 (Wigner-von Neumann non-crossing rule)** 在[能带理论](@entry_id:139801)中的应用如下 ：
-   如果两条能带在某个 $\mathbf{k}$ 点或一条高对称线上对应的[波函数](@entry_id:201714)属于[小群](@entry_id:198763)的**不同**[不可约表示](@entry_id:263310)，那么它们之间的[哈密顿矩阵元](@entry_id:201928)被对称性严格限制为零。这意味着两条能带之间没有耦合，它们可以自由地**交叉**。这种交叉是受对称性保护的，只有当破坏该对称性的微扰出现时，交叉点才会打开形成能隙。
-   如果两条能带对应的[波函数](@entry_id:201714)属于[小群](@entry_id:198763)的**相同**[不可约表示](@entry_id:263310)，那么对称性不再禁止它们之间的耦合。通常会存在一个非零的[哈密顿矩阵元](@entry_id:201928)，导致能级之间的排斥。因此，当这两条能带靠近时，它们会相互“避开”，形成一个**反交叉 (avoided crossing)**。

除了空间对称性，时间反演对称性 (TRS) 也扮演着至关重要的角色。
-   对于**无自旋**的电子，时间反演算符 $\mathcal{T}$ 满足 $\mathcal{T}^2 = +1$，它不保证在任意 $\mathbf{k}$ 点存在简并。它仅能保证 $E_n(\mathbf{k}) = E_n(-\mathbf{k})$。
-   对于包含自旋的**有自旋**电子（如电子），**克莱默斯定理 (Kramers' theorem)** 指出，只要系统具有时间反演对称性，由于 $\mathcal{T}^2 = -1$，所有[能量本征态](@entry_id:152154)都必须至少是双重简并的。在[能带理论](@entry_id:139801)中，这表现为 $E_n(\mathbf{k}) = E_m(-\mathbf{k})$，并且在[布里渊区](@entry_id:142395)的[时间反演](@entry_id:182076)不变动量点（TRIMs，满足 $\mathbf{k}=-\mathbf{k}+\mathbf{G}$ 的点），每个能级都是至少双重简并的。

一个更强的简并条件出现在同时具有**[时间反演对称性](@entry_id:138094) (TRS)** 和**空间[反演对称性](@entry_id:269948) (IS)** 的晶体中。在这种情况下，即使考虑了自旋轨道耦合，每个能带在[布里渊区](@entry_id:142395)内的**所有** $\mathbf{k}$ 点都保证是双重简并的。这是因为复合对称算符 $\Theta = \mathcal{P}\mathcal{T}$（其中 $\mathcal{P}$ 是反演算符）满足 $[\Theta, H]=0$ 且 $\Theta^2 = -1$，同时它保持 $\mathbf{k}$ 不变。这为整个[布里渊区](@entry_id:142395)的能带提供了克莱默斯类型的简并保护 。这些对称性保护的简并点和交叉点是现代凝聚态物理中[拓扑材料](@entry_id:142123)研究的核心。