## 引言
固体材料的电学性质，如介电常数、压电性等，是现代科学技术的核心。然而，这些宏观可测量的性质源于材料内部无数原子和电子在电场作用下的复杂微观行为。一个核心的物理问题是：我们如何在原子尺度的剧烈振荡和我们可测量的平滑宏观现象之间建立一座可靠的理论桥梁？这正是理解宏观电场与极化理论的关键挑战与精髓所在。

本文旨在系统地回答这一问题，为读者构建一个从基础到前沿的完整知识框架。在第一章“原理与机制”中，我们将从第一性原理出发，学习如何通过严谨的空间平均方法定义宏观电场，并在此基础上推导出极化强度、电位移矢量、局域场等核心概念，同时深入探讨介电响应的动态行为和量子力学基础。随后，在第二章“应用与交叉学科联系”中，我们将看到这些抽象的理论如何鲜活地体现在电容器设计、压电器件、多铁性材料乃至拓扑物理等多样化的实际应用和前沿研究领域。最后，通过“动手实践”部分提供的精选问题，您将有机会亲手运用所学知识，解决具体的物理问题，从而加深理解。通过这一系列的学习，您将掌握分析和理解凝聚态物质电学行为的强大理论工具。

## 原理与机制

### 从微观到宏观场

固体材料中的电磁现象本质上源于其内部大量原子核与电子在电场作用下的响应。这些带电粒子构成了复杂的电荷分布 $\rho(\mathbf{r})$，并产生一个在原子尺度上剧烈变化的微观电场 $\mathbf{e}(\mathbf{r})$。微观电场遵循基本的麦克斯韦方程，例如微观高斯定律：$\nabla \cdot \mathbf{e}(\mathbf{r}) = \rho(\mathbf{r})/\epsilon_0$。然而，对于大多数宏观现象，我们关心的是在远大于原子尺寸的尺度上的平均行为。直接处理微观场 $\mathbf{e}(\mathbf{r})$ 的剧烈振荡是不切实际且无必要的。

因此，我们需要一个系统的方法来定义一个平滑的、代表物理量空间平均值的**宏观电场** $\mathbf{E}(\mathbf{R})$。这个过程的核心思想是通过空间平均来滤除原子尺度的快速变化，同时保留在宏观长度 $\ell_E$ 上（例如，外加电场的变化尺度或样品尺寸）的缓变行为。

这个平均过程最普适的数学形式是卷积。我们将宏观场 $\mathbf{E}(\mathbf{R})$ 定义为微观场 $\mathbf{e}(\mathbf{r})$ 与一个归一化的“窗口函数”或“加权函数” $w$ 的卷积 [@problem_id:2838412]：
$$
\mathbf{E}(\mathbf{R}) = \int_{\mathbb{R}^3} \mathrm{d}^3 r\, w(\mathbf{R}-\mathbf{r})\, \mathbf{e}(\mathbf{r})
$$
为了使这个定义物理上合理且在数学上可靠，窗口函数 $w$ 必须满足一系列条件：

1.  **归一化**: 为了确保一个均匀的微观场在平均后保持不变，窗口函数在全空间的积分必须为1。即 $\int w(\mathbf{r}) \mathrm{d}^3 r = 1$。如果 $\mathbf{e}(\mathbf{r}) = \mathbf{e}_0$（常数），这个条件保证了 $\mathbf{E}(\mathbf{R}) = \mathbf{e}_0$。

2.  **尺度分离**: 窗口函数的特征宽度 $L$ 必须满足一个关键的尺度等级关系：$a \ll L \ll \ell_E$，其中 $a$ 是晶格常数。$L \gg a$ 的条件确保了平均体积足够大，可以包含足够多的晶胞以抹平原子尺度的振荡。而 $L \ll \ell_E$ 的条件则确保平均体积又足够小，不会模糊我们想要描述的宏观场变化。

3.  **局域性**: 窗口函数 $w(\mathbf{r})$ 应该具有紧凑支撑或在空间中迅速衰减。这保证了在点 $\mathbf{R}$ 处的宏观场主要由该点附近的微观场所决定。这个特性在数学上也是必要的，例如，它保证了在后续推导中通过分部积分转移微分算子时，无穷远处的表面项为零。

4.  **对称性与矩条件**: 为了使 $\mathbf{E}(\mathbf{R})$ 成为 $\mathbf{e}$ 在点 $\mathbf{R}$ 的一个良好代表，我们希望平均值与原函数在 $\mathbf{R}$ 点的泰勒展开尽可能匹配。通过选择一个中心对称（偶函数）的窗口函数，即 $w(\mathbf{r}) = w(-\mathbf{r})$，可以保证其一阶矩为零：$\int \mathbf{r} w(\mathbf{r}) \mathrm{d}^3 r = \mathbf{0}$。这个条件消除了平均过程中对场梯度的线性依赖项，使得平均值与 $\mathbf{e}(\mathbf{R})$ 的偏差从 $(L/\ell_E)$ 的量级降低到 $(L/\ell_E)^2$ 的量级，从而大大提高了平均的准确性。

满足这些条件的平均过程，使得我们可以可靠地将微分运算与平均运算交换，例如 $\nabla \cdot \mathbf{E} = \langle \nabla \cdot \mathbf{e} \rangle$。这一性质是建立宏观麦克斯韦方程组的基石，它将微观电荷密度 $\rho$ 的平均值 $\langle \rho \rangle$ 与宏观场 $\mathbf{E}$ 的散度联系起来。

### 宏观极化与束缚电荷

对微观电荷密度进行平均，我们得到宏观电荷密度 $\langle \rho \rangle$。在电介质中，通常将这部分电荷密度分为两类：**自由电荷** $\rho_f$ 和 **束缚电荷** $\rho_b$。自由电荷是可以长程移动的电荷（如导体中的传导电子），而束缚电荷则是那些被束缚在原子或分子内部，只能在原子尺度上微小位移的电荷。

电介质在外电场中的一个核心响应是其内部正负束缚电荷发生相对位移，或固有分子偶极发生取向，从而在材料内部产生净的电偶极矩。我们定义**极化强度矢量** $\mathbf{P}$ 为单位体积内的净电偶极矩。

极化强度 $\mathbf{P}$ 的物理后果是它会在材料内部和表面产生净的束缚电荷。一个非均匀的极化场 $\mathbf{P}(\mathbf{R})$ 会在体内产生净的电荷积累。可以证明，体束缚电荷密度 $\rho_b$ 与极化强度的散度直接相关：
$$
\rho_b = -\nabla \cdot \mathbf{P}
$$
这个关系非常关键：它将微观的偶极子图像（$\mathbf{P}$）与宏观的等效电荷分布（$\rho_b$）联系了起来。同样，在电介质的表面，极化的终止会产生一个面电荷层，其面密度由极化强度在表面法向方向的分量决定：
$$
\sigma_b = \mathbf{P} \cdot \hat{\mathbf{n}}
$$
其中 $\hat{\mathbf{n}}$ 是指向介质外部的单位法向量。

我们可以通过一个具体的例子来理解这些定义 [@problem_id:147528]。考虑一个半径为 $a$、高为 $h$ 的圆柱体，其内部存在一个非均匀的、冻结的极化场，以柱坐标 $(s, \phi, z)$ 表示为 $\mathbf{P}(s, \phi, z) = P_0 (s/a) \hat{\mathbf{s}} + P_1 (z/h) \hat{\mathbf{z}}$。
根据上述定义，我们可以计算出体束缚电荷密度：
$$
\rho_b = - \nabla \cdot \mathbf{P} = -\left[ \frac{1}{s}\frac{\partial}{\partial s}(s P_s) + \frac{\partial P_z}{\partial z} \right] = -\left[ \frac{1}{s}\frac{\partial}{\partial s}\left(s \frac{P_0 s}{a}\right) + \frac{\partial}{\partial z}\left(\frac{P_1 z}{h}\right) \right] = -\left( \frac{2P_0}{a} + \frac{P_1}{h} \right)
$$
这是一个均匀的体电荷密度。接下来，我们计算表面束缚电荷。圆柱体有三个表面：
-   顶面（$z = h/2, \hat{\mathbf{n}}=\hat{\mathbf{z}}$）：$\sigma_b = \mathbf{P} \cdot \hat{\mathbf{z}} = P_1(z/h)|_{z=h/2} = P_1/2$。
-   底面（$z = -h/2, \hat{\mathbf{n}}=-\hat{\mathbf{z}}$）：$\sigma_b = \mathbf{P} \cdot (-\hat{\mathbf{z}}) = -P_1(z/h)|_{z=-h/2} = -(-P_1/2) = P_1/2$。
-   侧面（$s = a, \hat{\mathbf{n}}=\hat{\mathbf{s}}$）：$\sigma_b = \mathbf{P} \cdot \hat{\mathbf{s}} = P_0(s/a)|_{s=a} = P_0$。

一个重要的自洽性检验是，对于一个电中性的电介质，总的束缚电荷（体电荷与表面电荷之和）必须为零。通过对上述电荷密度在相应体积和面积上积分，可以验证 $Q_b^{\text{total}} = Q_b^{\text{vol}} + Q_b^{\text{surf}} = 0$，这证实了我们的计算和定义的自洽性。

引入极化强度的概念后，宏观高斯定律 $\nabla \cdot \mathbf{E} = \langle \rho \rangle / \epsilon_0 = (\rho_f + \rho_b)/\epsilon_0$ 可以被重写。将 $\rho_b = -\nabla \cdot \mathbf{P}$ 代入，我们得到 $\nabla \cdot \mathbf{E} = (\rho_f - \nabla \cdot \mathbf{P})/\epsilon_0$，整理后得到 $\nabla \cdot (\epsilon_0 \mathbf{E} + \mathbf{P}) = \rho_f$。这启发我们定义一个新的矢量场，即**电位移矢量** $\mathbf{D} = \epsilon_0 \mathbf{E} + \mathbf{P}$，它满足只与自由电荷相关的高斯定律：$\nabla \cdot \mathbf{D} = \rho_f$。

### 局域场问题

宏观场 $\mathbf{E}$ 是在包含大量原子的体积内平均得到的场，但材料中的单个原子或分子感受到的真实电场是什么？这个问题被称为**局域场 (local field)** 问题。这个局域场 $\mathbf{E}_{loc}$ 通常与宏观场 $\mathbf{E}$ 不同，因为它还包含了来自周围其他被极化原子的贡献。正确计算局域场对于从微观物理（如原子极化率）推导宏观介电常数至关重要。

计算局域场的经典方法是 Lorentz 提出的。其思想是将参考原子周围的介质分为两个区域：半径为 $R_L$ 的球腔内部的“近区”和球腔外部的“远区”。$R_L$ 的选择需要足够大，以至于远区可以被视为一个连续的均匀极化介质，而近区则需要考虑分立的原子偶极子。

局域场 $\mathbf{E}_{loc}$ 可以写成三部分之和：
$$
\mathbf{E}_{loc} = \mathbf{E}_{macro} + \mathbf{E}_{cav} + \mathbf{E}_{near}
$$
1.  $\mathbf{E}_{macro}$ 是宏观平均场。
2.  $\mathbf{E}_{cav}$ 是由球形腔体表面上的极化电荷产生的场。对于均匀极化的介质 $\mathbf{P}$，这部分场是均匀的，其值为 $\mathbf{P}/(3\epsilon_0)$。
3.  $\mathbf{E}_{near}$ 是球腔内部（不包括参考原子本身）所有分立偶极子在原点产生的电场之和。

对于具有立方对称性的晶体，可以证明，由于高度对称性，腔内偶极子的电场贡献之和 $\mathbf{E}_{near}$ 精确为零。在这种特殊情况下，局域场由著名的 **Lorentz 关系** 给出：
$$
\mathbf{E}_{loc} = \mathbf{E}_{macro} + \frac{\mathbf{P}}{3\epsilon_0}
$$
然而，对于非立方晶体，$\mathbf{E}_{near}$ 不再为零，计算变得复杂 [@problem_id:147508]。更一般地，我们可以将局域场与宏观场和极化强度通过一个二阶张量——**局域场张量**（或 Lorentz 因子张量）$\mathbf{L}$ 联系起来 [@problem_id:147390]：
$$
\mathbf{E}_{loc} = \mathbf{E}_{macro} + \frac{1}{\epsilon_0} \mathbf{L} \cdot \mathbf{P}
$$
在 isotropic（各向同性）介质的 Lorentz 模型中，$\mathbf{L} = \frac{1}{3}\mathbf{I}$，其中 $\mathbf{I}$ 是单位张量。一般情况下，$\mathbf{L}$ 张量可以写为 $\mathbf{L} = \frac{1}{3}\mathbf{I} + \mathbf{S}$，其中 $\mathbf{S}$ 被称为**内部结构张量**，它正代表了腔内分立偶极子的贡献。其分量 $S_{ij}$ 通过对晶格求和得到：
$$
S_{ij} = \frac{v_c}{4\pi} \sum_{0  |\mathbf{R}_n|  R_L} \left( \frac{3 R_{n,i} R_{n,j}}{R_n^5} - \frac{\delta_{ij}}{R_n^3} \right)
$$
其中 $v_c$ 是原胞体积，求和遍及腔内的所有非原点格点。这个张量完全由晶体结构决定。例如，在一个具有正交晶系结构（$b=2a, c=3a$）的简单晶体中，通过在合适的 Lorentz 球腔（如半径 $R_L = 1.5a$）内求和，我们可以计算出 $S_{zz} \approx -0.35$，从而得到局域场张量的对角分量 $L_{zz} = 1/3 + S_{zz}$ [@problem_id:147390]。这表明局域场可以与宏观场存在显著的各向异性差异。

### 介电常数与极化率

对于许多材料，在弱场下，宏观极化强度 $\mathbf{P}$ 与宏观电场 $\mathbf{E}$ 成正比。对于各向同性介质，这是一个标量关系：
$$
\mathbf{P} = \epsilon_0 \chi \mathbf{E}
$$
比例系数 $\chi$ 称为**电极化率**。电位移矢量则为 $\mathbf{D} = \epsilon_0 \mathbf{E} + \mathbf{P} = \epsilon_0(1+\chi)\mathbf{E} = \epsilon_0\epsilon \mathbf{E}$。其中 $\epsilon = 1+\chi$ 被称为**相对介电常数**或介电函数。

我们可以将宏观量 $\epsilon$ 与微观量——单个原子/分子的**极化率** $\alpha$ 联系起来。单个偶极矩 $\mathbf{p}$ 由局域场诱导产生：$\mathbf{p} = \alpha \mathbf{E}_{loc}$。宏观极化强度是这些偶极矩的体密度，即 $\mathbf{P} = N\mathbf{p}$，其中 $N$ 是单位体积内的原子/分子数。
结合 Lorentz 局域场，我们有：
$$
\mathbf{P} = N\alpha \mathbf{E}_{loc} = N\alpha \left( \mathbf{E} + \frac{\mathbf{P}}{3\epsilon_0} \right)
$$
通过求解 $\mathbf{P}$ 与 $\mathbf{E}$ 的关系，可以推导出著名的 **Clausius-Mossotti 方程**：
$$
\frac{\epsilon-1}{\epsilon+2} = \frac{N\alpha}{3\epsilon_0}
$$
该方程为从微观极化率计算宏观介电常数提供了桥梁，但它依赖于 Lorentz 局域场的假设，主要适用于非极性分子组成的、密度不太高的介质。

对于由永久偶极矩分子组成的极性液体，Onsager 提出了一个更精致的模型 [@problem_id:147467]。该模型的核心思想是**反应场 (reaction field)**。一个分子自身的偶极矩会极化周围的连续介质，而被极化的介质反过来又会在分子所在的位置产生一个电场，这就是反应场。这个反应场会进一步增强分子自身的总偶极矩。这是一个自洽的过程。通过求解这个自洽问题，可以得到在介质中分子的有效偶极矩比其在气相中的固有偶极矩有所增大的结论。这个**偶极增强因子** $\eta = |\mathbf{m}|/|\mathbf{\mu}_0|$ 可以完全用宏观量——材料的静态介电常数 $\epsilon$ 和高频折射率 $n$ 来表示：
$$
\eta = \dfrac{(n^{2} + 2)(2\epsilon + 1)}{3(n^{2} + 2\epsilon)}
$$
Onsager 模型考虑了永久偶极矩的取向极化和电子云形变产生的诱导极化，为描述极性液体的介电性质提供了更准确的理论框架。

### 动态响应与因果律

当外电场随时间变化时，介质的响应通常会滞后，并且可能伴随能量耗散。这种动态响应通过一个频率依赖的**复介电函数** $\epsilon(\omega) = \epsilon_1(\omega) + i\epsilon_2(\omega)$ 来描述。

-   **实部 $\epsilon_1(\omega)$** 与介质的色散行为相关，即与频率相关的极化能力和光速。
-   **虚部 $\epsilon_2(\omega)$** 与介质的能量吸收相关。只有当 $\epsilon_2(\omega) \neq 0$ 时，材料才会从电磁场中吸收能量。

物理系统的响应必须遵循**因果律**：响应（极化）不能发生在其原因（电场）之前。这一基本原则在数学上导致了 $\epsilon_1(\omega)$ 和 $\epsilon_2(\omega)$ 之间深刻的联系，即 **Kramers-Kronig (K-K) 关系**。该关系指出，如果我们知道一个材料在所有频率下的吸收谱（即 $\epsilon_2(\omega)$），我们就可以唯一地确定它在所有频率下的色散行为（即 $\epsilon_1(\omega)$），反之亦然。其中一个关系式为：
$$
\epsilon_1(\omega) - 1 = \frac{2}{\pi} \mathcal{P} \int_{0}^{\infty} \frac{\omega' \epsilon_2(\omega')}{\omega'^2 - \omega^2} d\omega'
$$
其中 $\mathcal{P}$ 表示柯西主值积分。

为了具体理解这个关系，我们可以考虑一个理想化的模型 [@problem_id:147535]，其中材料只在一个特定频率范围 $[\omega_1, \omega_2]$ 内有恒定的吸收，即 $\epsilon_2(\omega') = A$ (当 $\omega_1 \le \omega' \le \omega_2$ 时)，在其他频率范围为零。通过执行 K-K 积分，我们可以计算出该材料的介电函数实部：
$$
\epsilon_1(\omega) = 1 + \frac{A}{\pi} \ln \left| \frac{\omega_2^{2} - \omega^{2}}{\omega_1^{2} - \omega^{2}} \right|
$$
这个结果明确地展示了吸收（$\epsilon_2$）如何决定了色散（$\epsilon_1$）。在吸收带的边缘（$\omega \to \omega_1$ 或 $\omega \to \omega_2$），$\epsilon_1(\omega)$ 会出现发散，这正反映了共振行为的特征。

### 固体的极化机制

固体的介电响应源于多种微观机制，其中两种尤为重要：电子极化和离子极化。

#### 离子极化与晶格动力学

在离子晶体（如 NaCl）中，正负离子构成子晶格。外电场会使两种子晶格发生相对位移，从而产生**离子极化**。我们可以用一个简化的阻尼谐振子模型来描述这种行为 [@problem_id:147479]。离子对的相对位移 $w$ 的运动方程为：
$$
M_r \frac{d^2w}{dt^2} + M_r \omega_T^2 w = q E
$$
其中 $M_r$ 是离子对的约化质量，$q$ 是有效电荷，而 $\omega_T$ 是系统的固有共振频率，它对应于**横向光学 (Transverse Optical, TO) 声子**的频率。

通过求解此方程，并计入由电子云形变产生的高频介电常数 $\epsilon_\infty$ 的贡献，我们可以推导出离子晶体的频率依赖介电函数：
$$
\epsilon(\omega) = \epsilon_\infty + \frac{N q^2}{\epsilon_0 M_r (\omega_T^2 - \omega^2)}
$$
这个表达式显示，在 TO 声子频率 $\omega_T$ 处，$\epsilon(\omega)$ 发散，对应于对横向电磁波（光）的强烈吸收和反射，这被称为**剩余射线带 (Reststrahlen band)**。

除了横波，晶格振动还可以是纵波。**纵向光学 (Longitudinal Optical, LO) 声子**的频率 $\omega_L$ 有一个特殊的电学定义：它是当电位移矢量 $D=0$ 时系统可以维持自持纵向振荡的频率。从 $D = \epsilon_0 \epsilon(\omega) E = 0$ 可知，这要求 $\epsilon(\omega_L) = 0$。

将 $\epsilon(\omega_L) = 0$ 和静态介电常数 $\epsilon(0) = \epsilon_\infty + \frac{N q^2}{\epsilon_0 M_r \omega_T^2}$ 结合起来，我们可以消去微观参数，得到一个只包含宏观可观测量的重要关系——**Lyddane-Sachs-Teller (LST) 关系**：
$$
\frac{\epsilon(0)}{\epsilon_\infty} = \frac{\omega_L^2}{\omega_T^2}
$$
LST 关系深刻地揭示了晶体的静态介电性质（$\epsilon(0)$）、高频光学性质（$\epsilon_\infty$）和晶格振动基本模式（$\omega_L, \omega_T$）之间的内在联系。

#### 极化响应的量子力学基础

经典模型为我们提供了直观的物理图像，但介电响应的最终根源在于量子力学。利用**线性响应理论**，特别是 **Kubo 公式**，可以从第一性原理出发计算介电极化率 [@problem_id:147422]。对于一个多粒子系统，其体积极化率张量 $\chi_{V,ij}(\omega)$ 可以通过总偶极矩算符 $\hat{P}_{\text{tot}}$ 的含时关联函数（具体地说是响应函数）来计算：
$$
\chi_{V,ij}(\omega) = \frac{i}{V \hbar} \int_0^\infty dt \, e^{i(\omega+i\eta)t} \langle [\hat{P}_{\text{tot}, i}(t), \hat{P}_{\text{tot}, j}(0)] \rangle_0
$$
这里，$\langle \dots \rangle_0$ 表示在系统无扰动的基态上的期望值，算符采用海森堡绘景。该公式将宏观响应系数 $\chi$ 与微观算符的动力学关联起来。

作为一个例子，我们可以对一个由各向异性量子谐振子组成的模型系统应用 Kubo 公式。在静态极限下（$\omega=0$），对于 $xx$ 分量，通过计算位置算符的对易子 $\langle [\hat{x}(t), \hat{x}(0)] \rangle_0$ 并代入积分，可以得到静态极化率：
$$
\chi_{V,xx}(0) = \frac{N q^2}{k_x}
$$
其中 $k_x$ 是 $x$ 方向的恢复力常数。这给出了静态介电常数 $\epsilon_{xx}(0) = 1 + Nq^2/(\epsilon_0 k_x)$。这个结果与从经典模型得到的结论完全一致，展示了量子力学理论如何为经典图像提供了坚实的基础。

### 高等专题：空间色散与涨落

#### 空间色散

标准的介电理论假设极化 $\mathbf{P}(\mathbf{r})$ 只依赖于同一点的电场 $\mathbf{E}(\mathbf{r})$，这是一个**局域响应**的近似。当电磁场的波长 $\lambda$ 与材料内部的微观特征长度（如晶格常数、激子半径）相当时，这个近似失效。此时，$\mathbf{r}$ 点的极化不仅依赖于 $\mathbf{E}(\mathbf{r})$，还依赖于其邻域内的电场。这种非局域响应被称为**空间色散**。

在傅里叶空间中，空间色散表现为介电张量不仅依赖于频率 $\omega$，还依赖于波矢 $\mathbf{k}$，即 $\boldsymbol{\varepsilon}(\mathbf{k}, \omega)$ [@problem_id:2838399]。对于各向同性介质，由于旋转对称性的约束，这个张量可以分解为两个标量函数：**横向介电函数** $\varepsilon_{\mathrm{T}}(k, \omega)$ 和 **纵向介电函数** $\varepsilon_{\mathrm{L}}(k, \omega)$：
$$
\varepsilon_{ij}(\mathbf{k},\omega)=\varepsilon_{\mathrm{T}}(k,\omega)\left(\delta_{ij}-\frac{k_i k_j}{k^2}\right)+\varepsilon_{\mathrm{L}}(k,\omega)\frac{k_i k_j}{k^2}
$$
其中 $k=|\mathbf{k}|$，$k_i k_j/k^2$ 和 $(\delta_{ij} - k_i k_j/k^2)$ 分别是沿着 $\mathbf{k}$ 方向的纵向和垂直于 $\mathbf{k}$ 方向的横向投影算符。

这种分解有重要的物理后果：
-   横向电磁波（如光波）的传播由横向介电函数决定，其色散关系为 $k^2 c^2 = \omega^2 \varepsilon_{\mathrm{T}}(k, \omega)/\epsilon_0$。
-   纵向电场波（如等离激元或纵向光学声子）的存在条件由纵向介电函数决定。在没有自由电荷的情况下，这些自持的纵向模式存在的条件是 $\varepsilon_{\mathrm{L}}(k, \omega) = 0$。

在长波极限下（$k \to 0$），空间色散效应消失，非局域性变得不重要。此时，为保证介电张量不依赖于 $\mathbf{k}$ 的方向，必须有 $\varepsilon_{\mathrm{L}}(k, \omega) \to \varepsilon_{\mathrm{T}}(k, \omega)$。两者共同趋于我们熟悉的局域介电函数 $\epsilon(\omega)$。

#### 极化涨落

除了作为对场的响应，极化本身也是一个热力学自由度，会因热搅动而在其平衡值附近涨落。在铁电材料的顺电相（即 $T  T_c$），宏观平均极化为零，但局域的极化涨落始终存在。这些涨落的动力学和统计性质包含了关于系统接近相变时临界行为的重要信息。

利用 **含时 Ginzburg-Landau (TDGL) 理论**，我们可以描述极化场 $P(\mathbf{r}, t)$ 涨落的动力学 [@problem_id:147400]。对于一个过阻尼系统，其运动方程（Model A）为：
$$
\frac{\partial P}{\partial t} = -\Gamma \frac{\delta F}{\delta P} + \eta(\mathbf{r},t)
$$
其中 $F[P]$ 是 Ginzburg-Landau 自由能泛函，$\Gamma$ 是动力学系数，$\eta$ 是代表热浴的随机噪音项。噪音的强度由 **涨落-耗散定理** 决定，其关联函数为 $\langle \eta(\mathbf{r},t) \eta(\mathbf{r}',t') \rangle = 2\Gamma k_B T \delta(\mathbf{r}-\mathbf{r}') \delta(t-t')$。

通过傅里叶变换 TDGL 方程，我们可以求解出极化涨落的**谱密度** $S_P(\mathbf{q}, \omega)$，它描述了涨落在不同波矢 $\mathbf{q}$ 和频率 $\omega$ 的强度分布：
$$
S_P(\mathbf{q},\omega) = \frac{2\Gamma k_B T}{\omega^{2} + \left( \Gamma \left( A + C q^{2} \right) \right)^{2}}
$$
其中 $A \propto (T-T_c)$ 和 $C$ 是 Ginzburg-Landau 泛函中的系数。这个结果呈现为一个中心在 $\omega=0$ 的洛伦兹峰。其宽度 $\tau^{-1} = \Gamma(A+Cq^2)$ 代表了涨落的弛豫速率。当温度 $T$ 趋近于临界温度 $T_c$ 时，$A \to 0$，导致长波长（$q \to 0$）涨落的弛豫时间 $\tau$ 发散。这种现象被称为**临界慢化**，是二阶相变的普遍特征，可以通过中子散射或光散射等实验技术直接测量。