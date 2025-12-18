## 引言
周期性固体，如晶体，构成了我们世界中绝大多数[功能材料](@entry_id:194894)的基础。理解其中电子的行为方式，是预测并设计材料电学、光学及磁学性质的关键。然而，一个宏观晶体中包含着海量相互作用的电子和原子核，直接求解其薛定谔方程是一项不可能完成的任务。幸运的是，[晶格](@entry_id:148274)在空间上的完美周期性提供了一把解开这个复杂问题的钥匙。[布洛赫定理](@entry_id:137461)正是利用了这一根本对称性，极大地简化了问题，为我们描绘晶体中电子的图景提供了坚实的理论基石。

本文将系统地引导您掌握这一凝聚态物理的核心定理。在第一章“原理与机制”中，我们将从平移对称性出发，严谨推导[布洛赫定理](@entry_id:137461)，并揭示[能带结构](@entry_id:139379)、倒易空间和贝里相位等关键概念的物理内涵。接下来，在“应用与跨学科交叉”一章中，我们将展示该定理如何成为计算材料科学的支柱，并如何被用于解释半导体动力学、光学响应、乃至拓扑[物态](@entry_id:139436)等前沿物理现象。最后，通过“动手实践”部分提供的计算练习，您将有机会亲手应用这些理论，加深对[布洛赫定理](@entry_id:137461)及其应用的理解。

## 原理与机制

在导论中，我们了解了周期性固体中电子行为的复杂性及其在决定[材料性质](@entry_id:146723)中的核心作用。本章将深入探讨支配这些行为的基本原理和机制。我们将从[晶格](@entry_id:148274)的[平移对称性](@entry_id:171614)这一基本概念出发，系统地推导出[布洛赫定理](@entry_id:137461)，并阐明它如何引出[能带结构](@entry_id:139379)、倒易空间和布里渊区等关键概念。此外，我们还将探讨[自旋轨道](@entry_id:274032)耦合等更复杂的相互作用如何影响电子态，并介绍描述这些现象的现代理论工具，如[贝里相位](@entry_id:159450)和拓扑不变量。

### 基础对称性：[平移不变性](@entry_id:195885)

周期性固体的最根本特征是其原子排布在空间中呈现周期性。这种周期性可以用一个称为**布拉维格矢**的向量集合 $\\{\mathbf{R}\\}$ 来描述，其中任意格矢 $\mathbf{R}$ 都是一组[基矢](@entry_id:199546) $\\{\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3\\}$ 的整数线性组合。对于在这样一个[晶格](@entry_id:148274)中运动的单个电子，其感受到的势能场 $V(\mathbf{r})$ 也具有相同的周期性，即 $V(\mathbf{r}+\mathbf{R}) = V(\mathbf{r})$。

描述该电子的单粒子[哈密顿量](@entry_id:144286)为：
$H = -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r})$

其中第一项是[动能算符](@entry_id:265633)，第二项是周期性势能算符。为了研究对称性的影响，我们引入**格点[平移算符](@entry_id:756122)** $T_{\mathbf{R}}$，其作用是将任意函数 $\psi(\mathbf{r})$ 的坐标平移一个格矢 $\mathbf{R}$：
$(T_{\mathbf{R}}\psi)(\mathbf{r}) = \psi(\mathbf{r}+\mathbf{R})$

现在，我们来考察哈密顿量 $H$ 与[平移算符](@entry_id:756122) $T_{\mathbf{R}}$ 之间的关系。一个核心的结论是，它们相互对易，即 $[H, T_{\mathbf{R}}] = HT_{\mathbf{R}} - T_{\mathbf{R}}H = 0$。我们可以通过分别考察动能项和势能项来证明这一点 。

首先，考察势能项 $V(\mathbf{r})$。对任意测试函数 $\psi(\mathbf{r})$，我们有：
$(VT_{\mathbf{R}})\psi(\mathbf{r}) = V(\mathbf{r})(T_{\mathbf{R}}\psi)(\mathbf{r}) = V(\mathbf{r})\psi(\mathbf{r}+\mathbf{R})$
$(T_{\mathbf{R}}V)\psi(\mathbf{r}) = T_{\mathbf{R}}(V(\mathbf{r})\psi(\mathbf{r})) = V(\mathbf{r}+\mathbf{R})\psi(\mathbf{r}+\mathbf{R})$
由于[势函数](@entry_id:176105)具有周期性 $V(\mathbf{r}+\mathbf{R})=V(\mathbf{r})$，上式变为 $V(\mathbf{r})\psi(\mathbf{r}+\mathbf{R})$。因此，$(VT_{\mathbf{R}})\psi = (T_{\mathbf{R}}V)\psi$，这意味着 $[V, T_{\mathbf{R}}] = 0$。

其次，考察动能项 $K = -\frac{\hbar^2}{2m}\nabla^2$。由于 $\mathbf{R}$ 是一个常数向量，对 $\mathbf{r}$ 的[微分](@entry_id:158422)等价于对 $\mathbf{r}+\mathbf{R}$ 的[微分](@entry_id:158422)。因此，[拉普拉斯算符](@entry_id:146319) $\nabla^2$ 在坐标平移下是不变的。形式上：
$(KT_{\mathbf{R}})\psi(\mathbf{r}) = -\frac{\hbar^2}{2m}\nabla^2[\psi(\mathbf{r}+\mathbf{R})]$
$(T_{\mathbf{R}}K)\psi(\mathbf{r}) = T_{\mathbf{R}}[-\frac{\hbar^2}{2m}\nabla^2\psi(\mathbf{r})] = -\frac{\hbar^2}{2m}(\nabla^2\psi)(\mathbf{r}+\mathbf{R})$
由于 $\nabla^2[\psi(\mathbf{r}+\mathbf{R})]$ 与 $(\nabla^2\psi)(\mathbf{r}+\mathbf{R})$ 是完全相同的，我们得出 $[K, T_{\mathbf{R}}] = 0$。

综合以上两点，哈密顿量 $H$ 与所有格点[平移算符](@entry_id:756122) $T_{\mathbf{R}}$ 对易。在量子力学中，一组相互对易的算符拥有共同的[本征态](@entry_id:149904)。这意味着我们可以找到一组函数，它们同时是[哈密顿量](@entry_id:144286) $H$ 和所有[平移算符](@entry_id:756122) $T_{\mathbf{R}}$ 的本征态。这是理解晶体中电子行为的出发点。

### [布洛赫定理](@entry_id:137461)：电子[本征态](@entry_id:149904)的结构

既然[能量本征态](@entry_id:152154) $\psi(\mathbf{r})$ 也是所有 $T_{\mathbf{R}}$ 的本征态，那么它必须满足：
$T_{\mathbf{R}}\psi(\mathbf{r}) = \psi(\mathbf{r}+\mathbf{R}) = c(\mathbf{R})\psi(\mathbf{r})$

其中 $c(\mathbf{R})$ 是对应于[平移算符](@entry_id:756122) $T_{\mathbf{R}}$ 的本征值。这些本征值并非任意，它们必须反映平移操作的群结构。平移操作的组合满足 $T_{\mathbf{R}}T_{\mathbf{R}'} = T_{\mathbf{R}+\mathbf{R}'}$，这意味着本征值必须满足乘法关系 $c(\mathbf{R})c(\mathbf{R}') = c(\mathbf{R}+\mathbf{R}')$。此外，由于 $T_{\mathbf{R}}$ 是幺正算符（保持[波函数归一化](@entry_id:152806)），其本征值的模必须为1，即 $|c(\mathbf{R})|=1$ 。

满足上述两个条件的函数形式必然是一个[复指数函数](@entry_id:169796)。我们可以引入一个向量 $\mathbf{k}$，使得本征值可以写为：
$c(\mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}}$

这个向量 $\mathbf{k}$ 被称为**晶体动量**或**[布洛赫波矢](@entry_id:746866)**，它是一个[量子数](@entry_id:145558)，用来标记电子态在[晶格](@entry_id:148274)平移下的对称性。因此，周期性势场中[能量本征态](@entry_id:152154)必须满足的条件，即**[布洛赫定理](@entry_id:137461)**的第一个表述是：
$\psi_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}}\psi_{\mathbf{k}}(\mathbf{r})$

这个方程表明，晶体中的电子[波函数](@entry_id:201714)不是严格周期性的，而是在一个[晶格](@entry_id:148274)平移下获得一个相位因子，这种函数被称为**[布洛赫函数](@entry_id:189422)**。

为了更深入地理解[布洛赫函数](@entry_id:189422)的结构，我们可以将其写成一个平面波和一个[周期函数](@entry_id:139337)的乘积。定义一个新函数 $u_{\mathbf{k}}(\mathbf{r}) = e^{-i\mathbf{k}\cdot\mathbf{r}}\psi_{\mathbf{k}}(\mathbf{r})$。让我们考察这个新函数的周期性 ：
$u_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k}\cdot(\mathbf{r}+\mathbf{R})}\psi_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k}\cdot\mathbf{r}}e^{-i\mathbf{k}\cdot\mathbf{R}} (e^{i\mathbf{k}\cdot\mathbf{R}}\psi_{\mathbf{k}}(\mathbf{r})) = e^{-i\mathbf{k}\cdot\mathbf{r}}\psi_{\mathbf{k}}(\mathbf{r}) = u_{\mathbf{k}}(\mathbf{r})$

这表明函数 $u_{\mathbf{k}}(\mathbf{r})$ 具有与[晶格](@entry_id:148274)完全相同的周期性，我们称之为**元胞周期部分 (cell-periodic part)**。因此，我们得到了[布洛赫定理](@entry_id:137461)更常见也更富物理内涵的表述：
$\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}}u_{n\mathbf{k}}(\mathbf{r})$

这里我们引入了另一个[量子数](@entry_id:145558) $n$，称为**能带指数 (band index)**。这是因为，对于一个给定的晶体动量 $\mathbf{k}$，将[布洛赫函数](@entry_id:189422)形式代入薛定谔方程，会得到一个关于元胞[周期函数](@entry_id:139337) $u_{n\mathbf{k}}(\mathbf{r})$ 的本征方程。这个方程通常有无穷多个离散的解，这些解就由能带指数 $n=1, 2, 3, ...$ 来标记。每个解对应一个特定的[能量本征值](@entry_id:144381) $E_n(\mathbf{k})$。

### [倒易空间](@entry_id:754151)与[布里渊区](@entry_id:142395)：晶体动量的舞台

[晶体动量](@entry_id:136369) $\mathbf{k}$ 并不是完全唯一的。让我们考虑一个特殊的向量集合，称为**倒易格矢 (reciprocal lattice vector)**，记作 $\mathbf{G}$。它由条件 $e^{i\mathbf{G}\cdot\mathbf{R}} = 1$ 对所有布拉维格矢 $\mathbf{R}$ 成立来定义。如果我们将晶体动量 $\mathbf{k}$ 替换为 $\mathbf{k}+\mathbf{G}$，平移的本征值变为：
$e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}e^{i\mathbf{G}\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}} \cdot 1 = e^{i\mathbf{k}\cdot\mathbf{R}}$

这表明，由 $\mathbf{k}$ 和 $\mathbf{k}+\mathbf{G}$ 标记的[布洛赫态](@entry_id:147552)具有完全相同的[平移对称性](@entry_id:171614)。因此，它们在物理上是等效的。这意味着[晶体动量](@entry_id:136369) $\mathbf{k}$ 的所有不等价的值都可以在[倒易空间](@entry_id:754151)的一个原胞中找到。这个约定俗成的原胞被称为**[第一布里渊区](@entry_id:269110) (first Brillouin zone)**，它是在[倒易空间](@entry_id:754151)中通过[Wigner-Seitz方法](@entry_id:264469)构造出来的区域，即包含所有比到其他任何倒易格点更靠近原点的点的区域  。

倒易格矢 $\\{\mathbf{b}_1, \mathbf{b}_2, \mathbf{b}_3\\}$ 可由[正空间](@entry_id:754128)[基矢](@entry_id:199546) $\\{\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3\\}$ 通过关系 $\mathbf{b}_i \cdot \mathbf{a}_j = 2\pi\delta_{ij}$ 导出。例如，一个重要的[晶体结构](@entry_id:140373)是[面心立方](@entry_id:156319) (FCC) [晶格](@entry_id:148274)。其[倒易晶格](@entry_id:136718)是一个体心立方 (BCC) [晶格](@entry_id:148274)。相应地，FCC[晶格](@entry_id:148274)的第一布里渊区是一个**截角八面体**。这个几何形状的对称中心和[高对称点](@entry_id:1126099)（如 $\Gamma, X, L$ 点）在分析[材料的电子性质](@entry_id:269415)时至关重要 。

对于一个理想的无限大晶体，$\mathbf{k}$ 可以在[布里渊区](@entry_id:142395)内连续变化。然而，对于一个实际的、有限尺寸的晶体，$\mathbf{k}$ 的取值是量子化的。通过施加**[玻恩-冯·卡门](@entry_id:201892) (Born-von Kármán)** 周期性边界条件，即要求[波函数](@entry_id:201714)在晶体宏观边界上具有周期性 $\psi(\mathbf{r}+N_i\mathbf{a}_i) = \psi(\mathbf{r})$，我们可以推导出 $\mathbf{k}$ 的允许值。对于一个由 $N$ 个[原胞](@entry_id:159354)组成的一维晶体链，其长度为 $L=Na$，允许的 $k$ 值为 $k = n \frac{2\pi}{Na}$，其中 $n$ 为整数。在第一布里渊区 $(-\frac{\pi}{a}, \frac{\pi}{a}]$ 内，共有 $N$ 个不等价的 $k$ 值，它们之间的间距为 $\Delta k = \frac{2\pi}{Na}$。当 $N \to \infty$ 时，$\Delta k \to 0$，这些离散的 $k$ 点汇集成连续的布里渊区，这为在理论计算中用积分代替求和提供了依据 。

### 能带与[带隙](@entry_id:138445)：物理后果

当晶体动量 $\mathbf{k}$ 在[第一布里渊区](@entry_id:269110)内变化时，每个能带指数 $n$ 对应的[能量本征值](@entry_id:144381) $E_n(\mathbf{k})$ 也会相应变化，形成一条连续的曲线或曲面。这些 $E_n(\mathbf{k})$ 函数构成了固体的**能带结构 (energy band structure)**。由于 $\mathbf{k}$ 和 $\mathbf{k}+\mathbf{G}$ 的等价性，能量也是倒易空间中的[周期函数](@entry_id:139337)：$E_n(\mathbf{k}) = E_n(\mathbf{k}+\mathbf{G})$ 。

能带的形成可以从两个互补的物理图像来理解。在**[紧束缚近似](@entry_id:145569) (tight-binding approximation)** 的图像中，当孤立的原子靠近形成晶体时，它们原本分立的[原子能级](@entry_id:148255)会因为相邻原子间的电子[波函数交叠](@entry_id:157485)（或称杂化）而展宽，形成能量的连续区域，即能带。在**[近自由电子模型](@entry_id:138124) (nearly-free electron model)** 的图像中，自由电子（[平面波](@entry_id:189798)）在受到一个微弱的周期性势场扰动时，在满足[布拉格衍射](@entry_id:148063)条件 $2\mathbf{k}\cdot\mathbf{G} = -|\mathbf{G}|^2$ 的[布里渊区](@entry_id:142395)边界处，传播方向相反的平面波 $e^{i\mathbf{k}\cdot\mathbf{r}}$ 和 $e^{i(\mathbf{k}-\mathbf{G})\cdot\mathbf{r}}$ 会发生强烈耦合。周期势将这两个简并的[态混合](@entry_id:148060)起来，形成驻波，并使得[能量简并](@entry_id:203091)被解除，从而在[能谱](@entry_id:181780)中打开一个**[能隙](@entry_id:138445) (band gap)** 。

我们可以通过[简并微扰理论](@entry_id:143587)来量化这个过程。考虑在布里渊区边界上满足 $| \mathbf{k} | = | \mathbf{k}+\mathbf{G} |$ 的两个简并的[平面波](@entry_id:189798)态。将周期势 $V(\mathbf{r})$ 的傅里叶分量 $V_{\mathbf{G}}$ 作为微扰，求解 $2 \times 2$ 的[哈密顿矩阵](@entry_id:136233)，可以发现原来的简并能级 $E^{(0)}$ 分裂为两个新的能级 $E_{\pm} = E^{(0)} + V_0 \pm |V_{-\mathbf{G}}|$。因此，打开的[能隙](@entry_id:138445)大小为 $\Delta E = 2|V_{\mathbf{G}}|$ 。

能带之间的能量空隙，即[带隙](@entry_id:138445)，是决定材料是导体、半导体还是绝缘体的关键。在半导体和绝缘体中，价带（被电子填满的最高能带）和导带（未被电子占据的最低能带）被一个[带隙](@entry_id:138445)分开。如果价带的能量最高点（**价带顶, VBM**）和导带的能量最低点（**导带底, CBM**）出现在布里渊区中相同的 $\mathbf{k}$ 点，则称该材料具有**直接带隙 (direct band gap)**。如果它们出现在不同的 $\mathbf{k}$ 点，则称为**间接带隙 (indirect band gap)**。这一区别对于光电材料的应用至关重要 。

### 高级表述与几何概念

[布洛赫定理](@entry_id:137461)的效应可以用更严谨的数学语言——**布洛赫-弗洛凯 (Bloch-Floquet) 理论**——来描述。该理论指出，整个系统的[希尔伯特空间](@entry_id:261193) $\mathcal{H} = L^2(\mathbb{R}^d)$ 可以分解为对布里渊区内所有 $\mathbf{k}$ 的“纤维”[希尔伯特空间](@entry_id:261193) $\mathcal{H}_{\mathbf{k}}$ 的**[直积](@entry_id:143046)分 (direct integral)**。每个纤维空间由具有元胞周期性的函数构成。在这种表述下，原[哈密顿量](@entry_id:144286) $H$ 算符被分解为一系列依赖于 $\mathbf{k}$ 的**布洛赫哈密顿量 (Bloch Hamiltonian)** $H(\mathbf{k})$，每个 $H(\mathbf{k})$ 作用于对应的纤维空间上 。
$H(\mathbf{k}) = e^{-i\mathbf{k}\cdot\mathbf{r}} H e^{i\mathbf{k}\cdot\mathbf{r}} = \frac{1}{2m}(-i\hbar\nabla + \hbar\mathbf{k})^2 + V(\mathbf{r})$
求解原哈密顿量谱的问题就转化为了在[布里渊区](@entry_id:142395)内对每个 $\mathbf{k}$ 分别[对角化](@entry_id:147016) $H(\mathbf{k})$ 的问题。

在[布洛赫定理](@entry_id:137461)的表述 $\psi_{n\mathbf{k}} = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}$ 中，元胞周期部分 $u_{n\mathbf{k}}$ 的相位是不确定的。我们可以任意乘以一个依赖于 $\mathbf{k}$ 的相位因子 $e^{-i\phi_n(\mathbf{k})}$ 而不改变任何[物理可观测量](@entry_id:154692)，如能量 $E_n(\mathbf{k})$、概率密度 $|\psi_{n\mathbf{k}}|^2$ 或群速度 $\mathbf{v}_n(\mathbf{k}) = \frac{1}{\hbar}\nabla_{\mathbf{k}}E_n(\mathbf{k})$。这种选择相位的自由度称为**[规范自由度](@entry_id:160491) (gauge freedom)** 。

尽管许多物理量是规范不变的，但某些描述能带几何性质的量却依赖于规范选择。**[贝里联络](@entry_id:136662) (Berry connection)** $\mathbf{A}_n(\mathbf{k}) = i \langle u_{n\mathbf{k}} | \nabla_{\mathbf{k}} u_{n\mathbf{k}} \rangle$（其中[内积](@entry_id:750660)在单个元胞内进行）在[规范变换](@entry_id:176521)下会改变：$\mathbf{A}_n(\mathbf{k}) \to \mathbf{A}_n(\mathbf{k}) + \nabla_{\mathbf{k}}\phi_n(\mathbf{k})$。然而，[贝里联络](@entry_id:136662)的旋度——**[贝里曲率](@entry_id:136846) (Berry curvature)** $\boldsymbol{\Omega}_n(\mathbf{k}) = \nabla_{\mathbf{k}} \times \mathbf{A}_n(\mathbf{k})$——却是规范不变的，因此是一个[物理可观测量](@entry_id:154692) 。

[贝里曲率](@entry_id:136846)描述了电子[波函数](@entry_id:201714)在 $\mathbf{k}$ 空间中的几何结构。对于一个二维系统，将[贝里曲率](@entry_id:136846)在整个[布里渊区](@entry_id:142395)上积分，得到一个整数，称为**陈数 (Chern number)**。一个非零的陈数意味着能带具有非平庸的[拓扑性质](@entry_id:141605)。这种[拓扑性质](@entry_id:141605)表现为一个“[拓扑阻碍](@entry_id:634492)”，使得我们不可能在整个[布里渊区](@entry_id:142395)上选择一个处处光滑且周期的规范。能带简并点（如三维外尔[半金属](@entry_id:152277)中的外尔点）在 $\mathbf{k}$ 空间中扮演着[贝里曲率](@entry_id:136846)的源或汇（磁单极子）的角色，它们的总“磁荷”决定了能带的拓扑不变量 。

### 自旋的角色：[旋量](@entry_id:158054)与对称性

到目前为止，我们忽略了电子的内禀自由度——自旋。在许多重元素材料中，电子的自旋和其[轨道运动](@entry_id:162856)之间的**[自旋轨道](@entry_id:274032)耦合 (spin-orbit coupling, SOC)** 效应不可忽略。包含SOC的[哈密顿量](@entry_id:144286)通常写作：
$\hat{H} = \frac{\hat{\mathbf{p}}^{2}}{2m} + V(\mathbf{r}) + \frac{\hbar}{4m^{2}c^{2}}\,\boldsymbol{\sigma}\cdot\big(\nabla V(\mathbf{r})\times \hat{\mathbf{p}}\big)$
其中 $\boldsymbol{\sigma}$ 是[泡利矩阵](@entry_id:139493)。由于SOC项的存在，[哈密顿量](@entry_id:144286)不再是自旋对角的，其[本征态](@entry_id:149904)是二维的**[旋量](@entry_id:158054) (spinor)** [波函数](@entry_id:201714) $\Psi(\mathbf{r}) = \begin{pmatrix} \psi_{\uparrow}(\mathbf{r}) \\ \psi_{\downarrow}(\mathbf{r}) \end{pmatrix}$。

尽管[哈密顿量](@entry_id:144286)的形式变得复杂，但只要[晶格](@entry_id:148274)的[平移对称性](@entry_id:171614)保持不变，[布洛赫定理](@entry_id:137461)依然成立。其[本征态](@entry_id:149904)可以写成[旋量](@entry_id:158054)形式的[布洛赫函数](@entry_id:189422) ：
$\Psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})$
其中元胞周期部分 $u_{n\mathbf{k}}(\mathbf{r})$ 现在是一个具有[晶格](@entry_id:148274)周期性的[旋量](@entry_id:158054)函数  。

自旋的引入对[对称性分析](@entry_id:174795)提出了新的要求。对于自旋-$1/2$的粒子，空间旋转 $2\pi$ 角度并不会使[波函数](@entry_id:201714)保持不变，而是附加一个 $-1$ 的因子。这意味着描述[旋量](@entry_id:158054)态对称性的[群表示](@entry_id:156757)必须是**双值表示 (double-valued representation)**，这需要引入**双群 (double group)** 的概念来对能带进行正确的对称性标记 。

此外，[时间反演对称性](@entry_id:138094) $\mathcal{T}$ 在有自旋的系统中扮演着关键角色。对于自旋-$1/2$的粒子，$\mathcal{T}^2 = -1$。**[克拉默斯定理](@entry_id:145108) (Kramers' theorem)** 指出，对于任何具有[时间反演对称性](@entry_id:138094)且包含奇数个[费米子](@entry_id:146235)的系统，所有[能量本征态](@entry_id:152154)都至少是二重简并的。在晶体中，这一定理保证了在特定点（时间反演不变点，TRIMs，满足 $\mathbf{k} = -\mathbf{k}+\mathbf{G}$）的能级至少是二重简并的。如果晶体同时具有反演对称性 $\mathcal{P}$，那么在[布里渊区](@entry_id:142395)的每一点 $\mathbf{k}$，能带都至少是二重简并的 。

在具有时间反演对称性的系统中，能带的[拓扑分类](@entry_id:154529)也变得更加丰富。例如，在二维和[三维拓扑绝缘体](@entry_id:145622)中，尽管陈数为零，但存在一种由 $\mathbb{Z}_2$ 不变量描述的非平庸拓扑，它受到[时间反演对称性](@entry_id:138094)的保护。某些特殊的空间对称性，如非点式对称（滑移面或[螺旋轴](@entry_id:268289)），在布里渊区边界处可以导致更高维度的能带简并，这种“能带粘连”现象是纯粹由对称性保证的，即使在强SOC存在时也不会消除  。

综上所述，从[晶格](@entry_id:148274)的[平移对称性](@entry_id:171614)出发，我们构建了描述晶体中电子行为的完整理论框架。[布洛赫定理](@entry_id:137461)不仅确立了能带论的基础，也为理解和预测材料的电子、光学、输运及拓扑性质提供了强大的理论工具。