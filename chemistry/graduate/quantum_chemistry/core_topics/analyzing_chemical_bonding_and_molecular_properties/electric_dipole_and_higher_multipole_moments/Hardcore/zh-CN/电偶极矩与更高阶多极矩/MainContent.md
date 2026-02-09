## 引言
在现代化学和物理学中，理解物质的电学性质是预测其行为和功能的核心。分子的电荷分布远比简单的正负电荷中心更为复杂，它决定了分子如何与外部电场耦合、如何与其他分子相互作用，以及如何响应光的激发。虽然“偶极矩”作为衡量分子极性的基本概念广为人知，但它仅仅是对真实电荷分布的初步近似。为了更精确、更系统地描述分子的静电特性，我们需要一个更强大的数学框架——电多极矩展开。

本文旨在填补从简单的偶极子图像到对分子电荷分布进行严谨、定量描述之间的知识鸿沟。我们将系统地阐述电偶极矩及更高阶多极矩（如四极矩、八极矩）的理论基础和实际应用。通过学习本文，读者将能够深刻理解分子电荷分布的复杂性，并掌握如何运用多极矩的概念来解释和预测广泛的物理化学现象。

文章将分为三个核心部分展开。在“**原理与机制**”一章中，我们将从第一性原理出发，推导静电势的多极展开，定义各阶多极矩，并将其转化为量子力学算符。我们还将探讨对称性和坐标原点选择等关键实际问题。接下来，“**应用与交叉学科联系**”一章将展示多极矩如何在光谱学、分子间相互作用理论、计算化学和材料科学等多个领域中发挥关键作用，连接微观结构与宏观性质。最后，“**动手实践**”部分将通过一系列精心设计的问题，引导读者将理论知识应用于具体的物理场景中。现在，让我们从其最基本的数学和物理原理开始，深入探索多极矩的世界。

## 原理与机制

在理解分子如何与电磁场相互作用以及分子之间如何相互作用时，电荷分布的概念是核心。虽然将分子视为简单的点偶极子在许多情况下是有效的，但更精确的描述需要对其电荷分布的复杂性进行更细致的处理。多极矩展开提供了一个严谨的数学框架，用于系统地描述和量化任何局部电荷分布所产生的静电势。本章将从第一性原理出发，阐述电偶极矩的定义、性质及其在量子化学中的应用，并深入探讨其在光谱学、分子间相互作用和高精度计算中的关键机制。

### 静电势的多极展开

考虑一个局域在空间中某个有限区域的电荷密度分布 $\rho(\mathbf{r}')$。根据库仑定律，该电荷分布在空间中任意一点 $\mathbf{r}$ 处产生的静电势 $V(\mathbf{r})$ 为：

$$
V(\mathbf{r}) = \frac{1}{4\pi\varepsilon_0} \int \frac{\rho(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} d^3r'
$$

在许多物理场景中，我们关心的是在远离电荷分布的“远场”区域（即观测点距离 $r = |\mathbf{r}|$ 远大于电荷分布的特征尺寸 $a$）的电势。在这种情况下，$|\mathbf{r}'| \ll |\mathbf{r}|$，我们可以将库仑核 $1/|\mathbf{r}-\mathbf{r}'|$ 对 $\mathbf{r}'$ 在原点附近进行泰勒展开。

$$
\frac{1}{|\mathbf{r}-\mathbf{r}'|} = \frac{1}{\sqrt{r^2 - 2\mathbf{r}\cdot\mathbf{r}' + r'^2}} = \frac{1}{r} \left(1 - \frac{2\mathbf{r}\cdot\mathbf{r}'}{r^2} + \frac{r'^2}{r^2}\right)^{-1/2}
$$

对上式进行二项式展开并保留低阶项，我们得到：

$$
\frac{1}{|\mathbf{r}-\mathbf{r}'|} \approx \frac{1}{r} + \frac{\mathbf{r}\cdot\mathbf{r}'}{r^3} + \frac{1}{2r^5} \sum_{i,j} r_i r_j (3r'_i r'_j - \delta_{ij}|\mathbf{r}'|^2) + \dots
$$

将此展开式代入电势的积分表达式，便得到了电势的**多极展开**（multipole expansion）：

$$
V(\mathbf{r}) = \frac{1}{4\pi\varepsilon_0} \left[ \frac{1}{r} \int \rho(\mathbf{r}') d^3r' + \frac{\mathbf{r}}{r^3} \cdot \int \mathbf{r}' \rho(\mathbf{r}') d^3r' + \frac{1}{2r^5} \sum_{i,j} r_i r_j \int (3r'_i r'_j - \delta_{ij}|\mathbf{r}'|^2) \rho(\mathbf{r}') d^3r' + \dots \right]
$$

这个展开式中的各项积分定义了电荷分布的**多极矩**（multipole moments）：

- **电单极矩**（electric monopole moment）：$q = \int \rho(\mathbf{r}') d^3r'$，它就是系统的总电荷。

- **电偶极矩**（electric dipole moment）：$\mathbf{p} = \int \mathbf{r}' \rho(\mathbf{r}') d^3r'$，它是一个矢量，描述了电荷分布的不对称性。

- **电四极矩**（electric quadrupole moment）：$Q_{ij} = \int (3r'_i r'_j - \delta_{ij}|\mathbf{r}'|^2) \rho(\mathbf{r}') d^3r'$，它是一个二阶张量，描述了电荷分布偏离球对称的更精细的形状特征。注意，这里的定义是**无迹的**（traceless），即 $\sum_i Q_{ii} = 0$。

利用这些定义，电势可以写成一系列贡献之和：

$$
V(\mathbf{r}) = V_{\text{monopole}}(\mathbf{r}) + V_{\text{dipole}}(\mathbf{r}) + V_{\text{quadrupole}}(\mathbf{r}) + \dots
$$

其中各项的径向依赖性（即随距离 $r$ 的衰减行为）非常明确 [@problem_id:2888144]。对于一个 $l$ 阶的多极矩（$l=0$ 为单极， $l=1$ 为偶极， $l=2$ 为四极），其对电势的贡献 $V_l(\mathbf{r})$ 和电场的贡献 $\mathbf{E}_l(\mathbf{r}) = -\nabla V_l(\mathbf{r})$ 在远场区域的标度行为为：

$$
V_l(\mathbf{r}) \propto \frac{1}{r^{l+1}}, \quad |\mathbf{E}_l(\mathbf{r})| \propto \frac{1}{r^{l+2}}
$$

具体来说：
- **单极** ($l=0$)：$V_0 \propto r^{-1}$, $|\mathbf{E}_0| \propto r^{-2}$。这是点电荷的库仑定律。如果一个系统的总电荷 $q \neq 0$，那么在远场，单极项将是主导项 [@problem_id:2888182]。对于一个中性分子或原子，总电荷 $q=0$，因此单极项精确为零 [@problem_id:2888144] [@problem_id:2888182]。
- **偶极** ($l=1$)：$V_1 \propto r^{-2}$, $|\mathbf{E}_1| \propto r^{-3}$。对于一个电中性但具有非零偶极矩的系统（例如，一个极性分子），这是远场电势的主导项。
- **四极** ($l=2$)：$V_2 \propto r^{-3}$, $|\mathbf{E}_2| \propto r^{-4}$。如果一个中性系统的偶极矩也为零（例如，由于对称性），那么四极矩将决定其远场行为 [@problem_id:2888144]。
- **八极** ($l=3$)：$V_3 \propto r^{-4}$, $|\mathbf{E}_3| \propto r^{-5}$。这是更高阶的修正，对于描述高度对称的非极性分子的相互作用非常重要。

在多极展开中，主导项是第一个不为零的项。因此，通过分析一个系统的多极矩，我们可以预测其在远处的静电行为。

### 量子化学中的多极矩算符

在量子力学中，分子的电荷分布由其波函数决定。为了计算多极矩，我们需要将经典的定义提升为量子力学算符。在**玻恩-奥本海默（Born-Oppenheimer）近似**下，我们首先在固定的原子核构型下求解电子薛定谔方程。

对于一个包含 $N_e$ 个电子和 $N_n$ 个原子核的分子，其总电荷密度算符 $\hat{\rho}(\mathbf{r})$ 可以写作原子核（被视为点电荷）和电子（被视为分布的电荷云）的贡献之和 [@problem_id:2888145] [@problem_id:2888182]：

$$
\hat{\rho}(\mathbf{r}) = \sum_{A=1}^{N_n} Z_A e \delta(\mathbf{r} - \mathbf{R}_A) - e \sum_{i=1}^{N_e} \delta(\mathbf{r} - \hat{\mathbf{r}}_i)
$$

其中 $Z_A e$ 和 $\mathbf{R}_A$ 分别是原子核 $A$ 的电荷和位置（在BO近似下是参数），而 $-e$ 和 $\hat{\mathbf{r}}_i$ 是电子的电荷和位置算符。分子的**永久多极矩**（permanent multipole moments）是对应多极矩算符在特定电子态（通常是基态）$|\Psi\rangle$下的期望值。

#### 电偶极矩算符

将电荷密度算符代入偶极矩的定义中，我们得到分子的**电偶极矩算符**（electric dipole moment operator）[@problem_id:2888180]：

$$
\hat{\boldsymbol{\mu}} = \int \mathbf{r} \hat{\rho}(\mathbf{r}) d^3r = e \sum_{A=1}^{N_n} Z_A \mathbf{R}_A - e \sum_{i=1}^{N_e} \hat{\mathbf{r}}_i = \boldsymbol{\mu}_{\text{nuc}} + \hat{\boldsymbol{\mu}}_{\text{el}}
$$

这个算符由两部分组成：
1.  **核贡献** $\boldsymbol{\mu}_{\text{nuc}} = e \sum_{A} Z_A \mathbf{R}_A$：在BO近似中，原子核位置 $\mathbf{R}_A$ 是固定的参数，因此核贡献是一个常数矢量（c-number）。
2.  **电子贡献** $\hat{\boldsymbol{\mu}}_{\text{el}} = - e \sum_{i} \hat{\mathbf{r}}_i$：这是一个真正的量子力学算符，因为它依赖于电子的位置算符，作用于电子波函数。

分子的永久偶极矩是该算符在电子基态 $|\Psi_{\text{el}}\rangle$ 下的期望值：
$$
\boldsymbol{\mu} = \langle \Psi_{\text{el}} | \hat{\boldsymbol{\mu}} | \Psi_{\text{el}} \rangle = \boldsymbol{\mu}_{\text{nuc}} + \langle \Psi_{\text{el}} | \hat{\boldsymbol{\mu}}_{\text{el}} | \Psi_{\text{el}} \rangle
$$

#### 电四极矩算符

类似地，我们可以定义**电四极矩算符**（electric quadrupole moment operator）[@problem_id:2888145]。总的四极矩也是核贡献和一个电子算符期望值的和 $Q_{\text{total}} = Q_{\text{nuc}} + \langle \hat{Q}_{\text{el}} \rangle$。其分量形式为：

- **核贡献**：
$$
Q^{(\text{n})}_{\alpha\beta} = e \sum_{A} Z_{A} (3R_{A\alpha}R_{A\beta} - |\mathbf{R}_{A}|^{2}\delta_{\alpha\beta})
$$

- **电子算符**：
$$
\hat{Q}^{(\text{e})}_{\alpha\beta} = -e \sum_{i=1}^{N_{\mathrm{e}}} (3\hat{x}_{i\alpha}\hat{x}_{i\beta} - |\hat{\mathbf{r}}_{i}|^{2}\delta_{\alpha\beta})
$$

由于同一电子的不同位置分量算符是对易的（$[\hat{x}_{i\alpha}, \hat{x}_{i\beta}] = 0$），这个算符是**对称的**（$\hat{Q}^{(\text{e})}_{\alpha\beta} = \hat{Q}^{(\text{e})}_{\beta\alpha}$）并且是**厄米的**。根据其定义，它也是**无迹的**（$\sum_{\alpha} \hat{Q}^{(\text{e})}_{\alpha\alpha} = 0$）[@problem_id:2888145]。

### 关键考量：对称性与坐标原点依赖性

在报告和使用多极矩时，必须仔细考虑两个关键问题：分子的对称性和坐标原点的选择。

#### 坐标原点依赖性

多极矩的值可能依赖于坐标原点的选择。考虑将坐标原点从 $\mathbf{0}$ 平移至 $\mathbf{a}$，新的坐标为 $\mathbf{r}' = \mathbf{r} - \mathbf{a}$。各阶多极矩的变换关系如下 [@problem_id:2888160]：

- **单极矩 (总电荷) $q$**：$q' = \int \rho(\mathbf{r}') d^3r' = \int \rho(\mathbf{r}) d^3r = q$。总电荷是**坐标原点无关的**。一个离子系统的总电荷不可能通过选择坐标原点来改变 [@problem_id:2888182]。

- **偶极矩 $\boldsymbol{\mu}$**：$\boldsymbol{\mu}' = \boldsymbol{\mu} - q\mathbf{a}$。这个关系表明，只有对于**电中性系统** ($q=0$)，其偶极矩才与坐标原点无关。对于离子 ($q \neq 0$)，偶极矩的值依赖于原点的选择。因此，报告离子的偶极矩时必须指明所用的坐标原点 [@problem_id:2888180]。

- **四极矩 $\boldsymbol{\Theta}$** (这里用 $\boldsymbol{\Theta}$ 表示无迹四极矩张量 $Q_{ij}$): $\boldsymbol{\Theta}' = \boldsymbol{\Theta}$ 仅当 $q=0$ 且 $\boldsymbol{\mu}=\mathbf{0}$ 时成立。也就是说，只有对于电中性且非极性的分子，其四极矩才与坐标原点无关。对于极性分子（$q=0, \boldsymbol{\mu} \neq \mathbf{0}$），四极矩的值是依赖于原点的 [@problem_id:2888145] [@problem_id:2888160]。

#### 参考系的选择

由于存在坐标原点依赖性，为多极矩（尤其是离子的偶极矩和极性分子的四极矩）建立一个标准的参考系至关重要。常见的选择有 [@problem_id:2888160]：

1.  **质心（Center of Mass, CM）**：将原点设在分子的质心 $\mathbf{R}_{\mathrm{CM}}$。这个选择在处理分子的平动和转动动力学时非常自然。例如，将多极矩分量在**惯量主轴（principal axes of the inertia tensor）**坐标系中报告，可以直接与转动光谱的分析联系起来，因为转动哈密顿量在该坐标系中是对角的 [@problem_id:2888160] [@problem_id:2888161]。

2.  **核电荷中心（Center of Nuclear Charge）**：将原点设在 $\mathbf{R}_Z = (\sum_A Z_A \mathbf{R}_A) / (\sum_A Z_A)$。这个选择在计算化学中特别有用。在BO近似下，电子结构不依赖于原子核的质量。同位素取代会改变质心位置，但不会改变核电荷中心。因此，对于一个极性分子，若以质心为原点报告四极矩，其值会随同位素的改变而改变。而以核电荷中心为原点，则可以消除这种人为的、非电子结构的同位素效应，得到一个更加纯粹的电子属性值 [@problem_id:2888160]。

#### 对称性的影响

分子的对称性对多极矩有严格的限制。一个基本的原则是：**任何物理性质（包括多极矩的各个分量）必须在分子所属点群的所有对称操作下保持不变**。

一个重要的推论是，对于任何具有**反演中心**（inversion center）的分子（例如 $D_{\infty h}$ 的 $\text{CO}_2$ 和 $\text{N}_2$，$O_h$ 的 $\text{SF}_6$），所有**奇数阶**的多极矩（如电偶极矩、电八极矩等）都必须为零。这是因为奇数阶多极矩张量在反演操作下会改变符号，但分子的对称性要求它不变，唯一满足这个条件的就是零。例如，对于一个具有反演对称性的中性系统 $\rho(\mathbf{r}) = \rho(-\mathbf{r})$，其偶极矩 $\mathbf{p} = \int \mathbf{r} \rho(\mathbf{r}) d^3r$ 的被积函数是奇函数，在对称的积分域（整个空间）上的积分必然为零 [@problem_id:2888182]。这类分子的第一个非零多极矩通常是四极矩。

### 光谱学中的多极矩：跃迁机制

多极矩不仅描述分子的静态电荷分布，更在分子与电磁辐射相互作用的光谱学中扮演核心角色。光谱跃迁的强度由**跃迁多极矩**（transition multipole moments）决定。

#### 红外（IR）光谱

红外吸收光谱探测的是分子振动能级之间的跃迁。在电偶极近似下，从初振动态 $|v_i\rangle$ 到末振动态 $|v_f\rangle$ 的跃迁强度正比于**跃迁偶极矩**（transition dipole moment）的平方：$|\boldsymbol{\mu}_{fi}|^2 = |\langle v_f | \boldsymbol{\mu}(Q) | v_i \rangle|^2$。

这里的 $\boldsymbol{\mu}(Q)$ 是分子偶极矩作为简正振动坐标 $Q$ 的函数。我们可以将其在平衡位置 $Q=0$ 附近作泰勒展开 [@problem_id:2888168]：

$$
\boldsymbol{\mu}(Q) = \boldsymbol{\mu}_0 + \left(\frac{\partial \boldsymbol{\mu}}{\partial Q}\right)_{Q=0} Q + \frac{1}{2}\left(\frac{\partial^2 \boldsymbol{\mu}}{\partial Q^2}\right)_{Q=0} Q^2 + \dots
$$

其中 $\boldsymbol{\mu}_0$ 是永久偶极矩。将此代入跃迁偶极矩积分：
$$
\boldsymbol{\mu}_{fi} = \boldsymbol{\mu}_0 \langle v_f | v_i \rangle + \left(\frac{\partial \boldsymbol{\mu}}{\partial Q}\right)_{Q=0} \langle v_f | Q | v_i \rangle + \dots
$$
由于振动波函数的正交性，对于跃迁（$f \neq i$），第一项为零。因此，红外跃迁的“总选择定则”（gross selection rule）是：一个振动模式要想成为**红外活性**（IR active），它必须在振动过程中引起分子偶极矩的改变。对于基频跃迁（$v: 0 \to 1$），其强度主要由第一项导数决定：

$$
I_{0 \to 1} \propto \left|\left(\frac{\partial \boldsymbol{\mu}}{\partial Q}\right)_{Q=0}\right|^2
$$

这就是为什么像 $\text{N}_2$ 或 $\text{O}_2$ 这样的同核双原子分子没有红外振动光谱。由于对称性，它们的偶极矩在键长拉伸时恒为零，因此偶极矩导数也为零。然而，它们可能存在极弱的、由电四极矩跃迁引起的光谱 [@problem_id:2888168]。

此外，在谐振子近似下，算符 $Q$ 的选择定则是 $\Delta v = \pm 1$。这意味着只有基频跃迁是允许的。**泛频带**（overtones，如 $v: 0 \to 2$）的出现，要么是由于**力学非谐性**（即振动势能函数偏离二次型），要么是由于**电学非谐性**（即 $\boldsymbol{\mu}(Q)$ 函数中存在 $Q^2$ 或更高次的非线性项）。如果一个分子的势能面是严格谐波的，且其偶极矩函数是严格线性的，那么泛频带的电偶极跃迁强度将精确为零 [@problem_id:2888168]。

#### 拉曼（Raman）光谱

拉曼光谱是一种散射技术，其机制与红外吸收不同。它涉及的是入射光电场在分子中感生的**诱导偶极矩**（induced dipole moment），$\boldsymbol{\mu}_{\text{ind}} = \boldsymbol{\alpha} \mathbf{E}$，其中 $\boldsymbol{\alpha}$ 是**分子极化率张量**（molecular polarizability tensor）。

与红外光谱类似，拉曼光谱的活性也取决于分子性质随振动的变化。在**Placzek近似**下，我们将极化率张量对简正坐标 $Q$ 进行泰勒展开 [@problem_id:2888161]：

$$
\boldsymbol{\alpha}(Q) = \boldsymbol{\alpha}_0 + \left(\frac{\partial \boldsymbol{\alpha}}{\partial Q}\right)_{Q=0} Q + \dots
$$

拉曼跃迁的总选择定则是：一个振动模式要想成为**拉曼活性**（Raman active），它必须在振动过程中引起分子极化率的改变。其强度正比于：

$$
I_{\text{Raman}} \propto \left|\left(\frac{\partial \boldsymbol{\alpha}}{\partial Q}\right)_{Q=0}\right|^2
$$

这个根本性的差异导致了红外和拉曼光谱的互补性。例如，对于具有反演中心的分子，存在**互斥规则**（rule of mutual exclusion）：奇宇称（ungerade, u）的振动模式是红外活性的、拉曼非活性的；而偶宇称（gerade, g）的振动模式是拉曼活性的、红外非活性的 [@problem_id:2888161]。这使得结合两种光谱技术可以获得更完整的分子振动信息。

### 高级主题与计算方法

#### 多极矩与分子间相互作用

多极矩展开不仅适用于描述单个分子与外场的相互作用，也构成了理解分子间长程相互作用的基石。两个分子之间的**永久静电相互作用**（permanent electrostatic interaction）可以通过它们各自的永久多极矩之间的耦合来描述，例如偶极-偶极、偶极-四极等相互作用项 [@problem_id:2888155]。

然而，必须强调的是，这种基于永久多极矩的静电模型只捕获了总相互作用能的一部分。它完全忽略了另外两种重要的长程作用：
- **感应（Induction）**：一个分子的永久多极矩产生的电场会极化另一个分子，使其产生感生多极矩。这种感生多极矩与产生它的电场之间的相互作用总是吸引的。它依赖于分子的（静态）极化率。
- **色散（Dispersion）**：即使对于没有永久多极矩的非极性分子（如惰性气体原子），也存在由瞬时电子涨落引起的吸引力。一个分子上瞬时的电荷不对称（瞬时偶极）会感应出邻近分子上的一个相关联的瞬时偶极，两者相互吸引。这种作用依赖于分子的（动态）频率依赖极化率。

在对称性匹配微扰理论（SAPT）等现代分子间相互作用理论中，静电、感应和色散项清晰地出现在不同阶的微扰修正中。永久静电相互作用是一阶项，而感应和色散是二阶项。这从根本上解释了为什么仅用永久多极矩无法描述后两者 [@problem_id:2888155]。

#### 电子相关对多极矩的影响

精确计算多极矩是量子化学的一项重要任务。计算结果的准确性强烈依赖于所采用的电子结构方法的水平，特别是对**电子相关**（electron correlation）效应的处理。

一个经典的例子是CO分子。基于单行列式的**Hartree-Fock (HF)**方法是一种平均场理论，它忽略了电子运动的瞬时相关。对于CO，HF方法预测的偶极矩符号是错误的（C$^{\delta+}$-O$^{\delta-}$），与简单的电负性分析一致，但与实验测定的C$^{\delta-}$-O$^{\delta+}$结果相反。只有当引入了电子相关效应，例如通过**耦合簇理论（Coupled-Cluster theory, 如CCSD）**，计算才能得到正确的偶极矩符号和大小。这是因为电子相关导致电子密度重新分布，将部分被HF方法过度局域在氧原子上的电荷转移回碳原子方向 [@problem_id:2888162]。

从计算角度看，多极矩可以通过两种等效（在理论完备时）的方式计算：
1.  作为**期望值**：$\boldsymbol{\mu} = \langle \Psi | \hat{\boldsymbol{\mu}} | \Psi \rangle$。
2.  作为能量对外加均匀电场的一阶导数（**有限场方法**）：$\mu_z = -\left.\frac{\partial E(F_z)}{\partial F_z}\right|_{F_z=0}$。

**Hellmann-Feynman定理**保证了对于变分优化的波函数（如HF），这两种方法在完备基组下是等价的。然而，对于像CCSD这样的非变分方法，该定理不成立。为了正确计算能量导数，必须采用更复杂的**拉格朗日方法**或响应理论，这些方法包含了对波函数参数（如簇幅）响应的贡献 [@problem_id:2888162] [@problem_id:2888181]。

#### 规范不变性与形式选择

在处理分子与含时电磁场的相互作用时，存在两种主要的哈密顿量形式，它们通过一个幺正变换（Power-Zienau-Woolley变换）联系在一起，这两种形式被称为不同的**规范**（gauge）[@problem_id:2888181]。

1.  **最小耦合（速度规范）**：通过动量算符替换 $\mathbf{p} \to \mathbf{p} + q\mathbf{A}$ 来引入矢量势 $\mathbf{A}$。相互作用项涉及 $\mathbf{p} \cdot \mathbf{A}$。
2.  **多极形式（长度规范）**：相互作用被重写为多极矩与电磁场的耦合，在长波近似下主导项为 $-\boldsymbol{\mu} \cdot \mathbf{E}$。

在完备的理论框架下（精确解，完备基组），两种规范给出的任何物理可观测量（如跃迁概率、极化率）都是完全相同的，这被称为**规范不变性**（gauge invariance）。长度规范的跃迁偶极矩 $\langle \Psi_f | \mathbf{r} | \Psi_0 \rangle$ 和速度规范的跃迁偶极矩 $\langle \Psi_f | \mathbf{p} | \Psi_0 \rangle$ 之间的等价性依赖于哈密顿量与位置算符的对易关系 $[H_0, \mathbf{r}]$。

然而，在实际的近似计算中，这种等价性被打破。两种规范的计算结果的差异大小，常被用作衡量计算质量（例如基组完备性）的一个指标。对于孤立分子的价电子跃迁，长度规范通常收敛得更快。而对于周期性体系（晶体），由于位置算符 $\mathbf{r}$ 的定义不良，速度规范是更自然和常用的选择 [@problem_id:2888181]。