## 引言
为宇宙大尺度结构形成的计算机模拟设定初始条件，是数值宇宙学中的一个奠基性步骤。现代宇宙学理论指出，宇宙早期的物质密度涨落可以被极其精确地描述为一个统计均匀且各向同性的高斯随机场。这些初始涨落作为引力不稳定的种子，最终演化成我们今天观测到的由星系、星系团和宇宙空洞构成的宏伟宇宙网。

然而，从早期宇宙物理推导出的抽象统计量——例如物质功率谱 $P(k)$——与一个可供N体模拟程序使用的、包含数百万乃至数十亿粒子的具体三维分布之间，存在着一道理论与实践的鸿沟。如何跨越这道鸿沟，即如何将一个理论功率谱“翻译”成一个既满足高斯统计特性又能在计算机中表示的数值对象，正是本文旨在解决的核心问题。

本文将系统地引导读者完成这一过程。在“原理与机制”一章中，我们将深入探讨描述高斯随机场的数学语言，包括两点相关函数和功率谱，并详细阐释在离散傅里叶空间中生成随机场的标准算法。接下来，在“应用与跨学科联系”一章中，我们将展示这一技术如何成为连接理论与模拟的桥梁，探讨功率谱中编码的物理印记（如重子声学振荡），以及在实现过程中遇到的数值挑战与先进应用。最后，“动手实践”部分将提供具体的计算问题，帮助读者巩固所学知识，将理论付诸实践。

## 原理与机制

在数值宇宙学中，为宇宙大尺度结构形成模拟生成初始条件，其核心是构建一个符合理论预期的随机密度场。这个密度场必须体现宇宙学原理所要求的统计均匀性与各向同性，并且其涨落应为高斯随机的。本章将深入探讨生成此类高斯随机场的数学原理和具体算法机制。

### 宇宙学随机场的统计描述

我们将初始时刻的物质密度涨落表示为一个无量纲的密度对比场 $\delta(\boldsymbol{x})$，它定义在一个三维的共动坐标空间中。作为一个随机场，$\delta(\boldsymbol{x})$ 的完整信息蕴含在其所有阶的统计矩中。对于一个**高斯随机场 (Gaussian Random Field, GRF)**，其统计特性被其均值（通常设为零，$\langle \delta(\boldsymbol{x}) \rangle = 0$）和两点相关函数完全确定。

#### 实空间：两点相关函数

描述场在两点之间关联程度的核心统计量是**两点相关函数 (two-point correlation function)**，定义为：
$$
\xi(\boldsymbol{r}) \equiv \langle \delta(\boldsymbol{x}) \delta(\boldsymbol{x}+\boldsymbol{r}) \rangle
$$
由于我们假设场是**统计均匀的 (statistically homogeneous)**，相关函数只依赖于两点的分离矢量 $\boldsymbol{r}$，而与绝对位置 $\boldsymbol{x}$ 无关。进一步，基于**统计各向同性 (statistically isotropic)** 的假设，相关函数应只依赖于分离矢量的模 $r = |\boldsymbol{r}|$，即 $\xi(\boldsymbol{r}) = \xi(r)$。$\xi(r)$ 衡量了在给定距离 $r$ 处的两个点，其密度涨落的典型乘积。正的 $\xi(r)$ 意味着如果一个点是超密的，另一个点也倾向于是超密的（成团性），而负的 $\xi(r)$ 则表示反相关。

#### 傅里叶空间：功率谱

虽然相关函数在实空间中提供了直观的物理图像，但在理论计算和数值生成中，使用傅里叶空间的描述更为便捷。场的傅里叶变换定义为：
$$
\delta(\boldsymbol{x}) = \int \frac{d^3k}{(2\pi)^3} \delta(\boldsymbol{k}) e^{i\boldsymbol{k}\cdot\boldsymbol{x}}
$$
其中 $\delta(\boldsymbol{k})$ 是傅里叶振幅，$\boldsymbol{k}$ 是波矢。由于 $\delta(\boldsymbol{x})$ 是一个实数场，其傅里叶变换必须满足赫米特对称性：$\delta(-\boldsymbol{k}) = \delta(\boldsymbol{k})^*$，其中 $*$ 表示复共轭。

在傅里叶空间中，两点统计信息由**功率谱 (power spectrum)** $P(k)$ 描述。统计均匀性和各向同性意味着不同傅里叶模式是不相关的，并且它们的方差只依赖于波数 $k=|\boldsymbol{k}|$。这可以精确地表达为：
$$
\langle \delta(\boldsymbol{k}) \delta^*(\boldsymbol{k}') \rangle = (2\pi)^3 \delta_{\mathrm{D}}(\boldsymbol{k}-\boldsymbol{k}') P(k)
$$
其中 $\delta_{\mathrm{D}}$ 是三维狄拉克delta函数。这个表达式表明，只有当 $\boldsymbol{k}=\boldsymbol{k}'$ 时，傅里叶振幅的系综平均才不为零，这体现了模式的独立性。$P(k)$ 本身则给出了在波数 $k$ 附近模式的“能量”或方差的幅度。

一个特别简单的例子是**白噪声 (white noise)** 场，其定义是拥有一个平坦的功率谱 $P_{\mathrm{WN}}(k) = \sigma_{\mathrm{WN}}^2$（一个常数）。这意味着所有尺度的涨落具有相同的能量。其在实空间中的相关函数是一个狄拉克delta函数，$C_{\mathrm{WN}}(\boldsymbol{r}) = \sigma_{\mathrm{WN}}^2 \delta_{\mathrm{D}}(\boldsymbol{r})$，表明场在任何两个不同点的值都是完全不相关的 [@problem_id:3473766]。宇宙中的密度场并非白噪声；其功率谱 $P(k)$ 具有复杂的尺度依赖性，反映了早期宇宙的物理过程。

#### 维纳-辛钦定理：连接实空间与傅里叶空间

两点相关函数 $\xi(r)$ 和功率谱 $P(k)$ 并非相互独立，它们通过**维纳-辛钦定理 (Wiener-Khinchin theorem)** 联系在一起，构成一个傅里叶变换对。我们可以通过将场的傅里叶表示代入 $\xi(r)$ 的定义来推导这一关系 [@problem_id:3473735] [@problem_id:3473799]。

$$
\begin{align}
\xi(\boldsymbol{r})  = \langle \delta(\boldsymbol{x}) \delta(\boldsymbol{x}+\boldsymbol{r}) \rangle \\
 = \left\langle \int \frac{d^3k}{(2\pi)^3} \delta(\boldsymbol{k}) e^{i\boldsymbol{k}\cdot\boldsymbol{x}} \int \frac{d^3k'}{(2\pi)^3} \delta(\boldsymbol{k}') e^{i\boldsymbol{k}'\cdot(\boldsymbol{x}+\boldsymbol{r})} \right\rangle \\
 = \iint \frac{d^3k}{(2\pi)^3} \frac{d^3k'}{(2\pi)^3} e^{i(\boldsymbol{k}+\boldsymbol{k}')\cdot\boldsymbol{x}} e^{i\boldsymbol{k}'\cdot\boldsymbol{r}} \langle \delta(\boldsymbol{k}) \delta(\boldsymbol{k}') \rangle
\end{align}
$$
由于 $\delta(\mathbf{x})$ 是实数，其傅里叶变换满足赫米特对称性 $\delta(\boldsymbol{k}') = \delta^*(-\boldsymbol{k}')$。结合功率谱的定义，可以推导出 $\langle \delta(\boldsymbol{k}) \delta(\boldsymbol{k}') \rangle = (2\pi)^3 \delta_{\mathrm{D}}(\boldsymbol{k}+\boldsymbol{k}') P(k)$。代入上式后，对 $\boldsymbol{k}'$ 的积分可以通过狄拉克delta函数完成，它强制 $\boldsymbol{k}' = -\boldsymbol{k}$。

$$
\xi(\boldsymbol{r}) = \int \frac{d^3k}{(2\pi)^3} P(k) e^{-i\boldsymbol{k}\cdot\boldsymbol{r}}
$$
由于 $P(k)$ 是 $k=|\boldsymbol{k}|$ 的偶函数，我们可以将指数项中的符号反转，得到更常见的形式：
$$
\xi(r) = \int \frac{d^3k}{(2\pi)^3} P(k) e^{i\boldsymbol{k}\cdot\boldsymbol{r}}
$$
这个积分可以通过在 $\boldsymbol{k}$ 空间的球坐标系中求解来简化。由于 $P(k)$ 的各向同性，积分结果只依赖于 $r$。对角度部分积分后，我们得到一个一维积分：
$$
\xi(r) = \frac{1}{2\pi^2} \int_0^\infty k^2 P(k) \frac{\sin(kr)}{kr} dk
$$
这个公式是连接理论功率谱和可观测相关函数的桥梁。例如，考虑一个假设性的高斯形式功率谱 $P(k) = A \exp(-R^2 k^2)$，其中 $A$ 和 $R$ 是常数。通过执行上述积分，可以得到其对应的实空间相关函数也呈高斯形式 [@problem_id:3473735] [@problem_id:3473799]：
$$
\xi(r) = \frac{A}{8\pi^{3/2}R^3} \exp\left(-\frac{r^2}{4R^2}\right)
$$
这说明傅里叶变换将高斯函数映为高斯函数，但特征尺度会发生改变。

### 场的方差与无量纲功率谱

#### 场的方差推导

场的**方差 (variance)** $\sigma^2$ 是一个关键量，它描述了密度涨落的典型幅度。其定义为 $\sigma^2 \equiv \langle \delta^2(\boldsymbol{x}) \rangle$。由于场的统计均匀性，方差与位置 $\boldsymbol{x}$ 无关。方差与两点相关函数在零点分离处的值相同，即 $\sigma^2 = \xi(r=0)$。

我们可以通过维纳-辛钦定理在 $r=0$ 时的情况直接得到方差的傅里叶空间表达式 [@problem_id:3473749]：
$$
\sigma^2 = \xi(0) = \int \frac{d^3k}{(2\pi)^3} P(k)
$$
再次利用各向同性，我们可以切换到球坐标并对角度积分，得到：
$$
\sigma^2 = \int_0^\infty \frac{4\pi k^2 P(k)}{(2\pi)^3} dk = \int_0^\infty \frac{k^2 P(k)}{2\pi^2} dk
$$

#### 每对数间隔的方差贡献

在宇宙学中，我们常常关心不同尺度对总方差的贡献。由于物理过程往往在对数尺度上展开，将方差表示为对 $\ln k$ 的积分是很有启发性的。通过变量代换 $dk = k \, d(\ln k)$，我们得到 [@problem_id:3473749]：
$$
\sigma^2 = \int_0^\infty \frac{k^3 P(k)}{2\pi^2} d(\ln k)
$$
这个形式启发我们定义一个**无量纲功率谱 (dimensionless power spectrum)** $\Delta^2(k)$：
$$
\Delta^2(k) \equiv \frac{k^3 P(k)}{2\pi^2}
$$
于是，方差可以简洁地写为：
$$
\sigma^2 = \int_0^\infty \Delta^2(k) d(\ln k)
$$
从这个表达式可以看出，$\Delta^2(k)$ 的物理意义是**每单位对数波数间隔对总方差的贡献**。例如，如果 $\Delta^2(k)$ 在某个 $k$ 值附近达到峰值，那么对应尺度 $\lambda \sim 2\pi/k$ 的涨落对场的总体起伏贡献最大。

进行量纲分析可以加深理解。若 $\delta(\boldsymbol{x})$ 是无量纲的，那么根据傅里叶变换的定义，$\delta(\boldsymbol{k})$ 的量纲是 $[长度]^3$。进而，从功率谱的定义可知 $P(k)$ 的量纲也是 $[长度]^3$（即体积）。因此，在 $\Delta^2(k)$ 的定义中，$k^3$ 的量纲 $[长度]^{-3}$ 恰好与 $P(k)$ 的量纲相抵消，使得 $\Delta^2(k)$ 成为一个无量纲量，这与其作为每（无量纲的）对数间隔的方差贡献的物理解释是自洽的 [@problem_id:3473749]。

### 数值模拟的离散化方法

为了在计算机中生成随机场，我们必须将连续的物理空间离散化。标准做法是使用一个边长为 $L$ 的立方体盒子，并施加**周期性边界条件 (Periodic Boundary Conditions, PBCs)**。

#### 周期性边界条件及其意义

采用PBCs的主要原因在于它们保持了空间的平移不变性，尽管是在一个离散的意义上。这意味着盒子的拓扑结构是一个三维环面 ($T^3$)。这种平移对称性允许我们使用一组简单且正交的基函数——离散的傅里叶模式（平面波）——来表示场。这极大地简化了从功率谱生成随机场的过程，因为不同傅里叶模式是统计独立的 [@problem_id:3473712]。如果没有PBCs（例如，使用“硬墙”边界），边界会破坏平移对称性，导致傅里叶模式之间出现人为的耦合，从而使从 $P(k)$ 生成场的过程变得非常复杂。

#### 离散傅里叶空间

在边长为 $L$ 的周期性盒子中，只有特定波长的平面波才能满足周期性。这导致了波矢 $\boldsymbol{k}$ 的离散化。允许的波矢构成了一个傅里叶晶格 [@problem_id:3473789]：
$$
\boldsymbol{k} = \frac{2\pi}{L}(n_x, n_y, n_z) = k_f (n_x, n_y, n_z)
$$
其中 $(n_x, n_y, n_z)$ 是整数三元组，$k_f = 2\pi/L$ 被称为**基频 (fundamental frequency)**，它对应于能装入盒子的最大波长 $L$。

此外，当我们将场采样到 $N^3$ 个均匀网格点上时，可分辨的最小尺度（最高频率）也受到了限制。网格间距为 $\Delta = L/N$。根据奈奎斯特定理，能够无歧义表示的最高频率是**奈奎斯特频率 (Nyquist frequency)**：
$$
k_{\mathrm{Ny}} = \frac{\pi}{\Delta} = \frac{\pi}{L/N} = \frac{N}{2} k_f
$$
这意味着在每个坐标轴方向上，波矢分量 $k_i$ 的范围被限制在 $-k_{\mathrm{Ny}}, k_{\mathrm{Ny}})$ 内。相应地，整数索引 $n_i$ 的范围通常取为（以 $N$ 为偶数为例）：
$$
n_i \in \left\{-\frac{N}{2}, -\frac{N}{2}+1, \dots, \frac{N}{2}-1\right\}
$$
这个范围恰好包含 $N$ 个独立的模式。值得注意的是，模式 $n_i = N/2$ 与 $n_i = -N/2$ 在离散网格上是等价的（发生[混叠），因此我们只取其中一个以构成完备非冗余的基底 [@problem_id:3473789]。

### 生成高斯随机场的算法

有了离散傅里叶空间的框架，我们现在可以详细阐述生成高斯随机场的具体算法。其核心思想是在傅里叶空间中生成一组满足正确统计特性和对称性约束的复数傅里叶系数 $\delta(\boldsymbol{k})$，然后通过快速傅里叶逆变换 (Inverse FFT) 得到实空间中的密度场 $\delta(\boldsymbol{x})$。

#### 实数场的傅里叶空间约束

一个基础但至关重要的约束是，要使实空间场 $\delta(\boldsymbol{x})$ 为实数，其傅里叶系数必须满足**赫米特对称性 (Hermitian symmetry)** [@problem_id:3512395]：
$$
\delta(-\boldsymbol{k}) = \delta^*(\boldsymbol{k})
$$
这个约束意味着 $\boldsymbol{k}$ 和 $-\boldsymbol{k}$ 对应的傅里叶系数不是独立的，而是互为复共轭。因此，我们只需要在傅里叶空间的一半（例如，满足 $k_z > 0$ 的半空间，再加上 $k_z=0$ 的平面）独立地生成随机系数，另一半则由该对称性确定。

这个约束也对某些特殊模式施加了更强的限制。
*   **直流 (DC) 模式** $\boldsymbol{k}=\boldsymbol{0}$：对称性要求 $\delta(\boldsymbol{0}) = \delta^*(\boldsymbol{0})$，因此 $\delta(\boldsymbol{0})$ 必须是实数。它代表了全场的空间平均值，在宇宙学中通常被设为零，即 $\langle \delta \rangle = 0$。
*   **自共轭模式 (Self-conjugate modes)**：在离散网格上，某些非零模式满足 $\boldsymbol{k} \equiv -\boldsymbol{k}$（在模 $N$ 的意义下）。当 $N$ 为偶数时，这发生在每个分量索引 $n_i$ 都取值为 $0$ 或 $-N/2$（或等效的 $N/2$）时。对于三维 $N^3$ 网格，共有 $2^3=8$ 个这样的模式。对于这些模式，赫米特对称性变为 $\delta(\boldsymbol{k}) = \delta^*(\boldsymbol{k})$，意味着它们的傅里叶系数也必须是纯实数 [@problem_id:3473789] [@problem_id:3512395]。

由于赫米特对称性，一个 $N^3$ 网格上 $N^3$ 个复数傅里叶系数中，独立的自由度数量远小于 $2N^3$。对于偶数 $N$，总共有 $(\frac{N^3-8}{2})$ 个复数对和 $8$ 个实数，所以独立生成的模式数量为 $\frac{N^3-8}{2} + 8 = \frac{N^3}{2} + 4$。如果再强制 $\delta(\boldsymbol{0})=0$，则减少为 $\frac{N^3}{2} + 3$ [@problem_id:3512395]。

#### 离散傅里叶模式的统计特性

下一步是确定每个独立傅里叶模式 $\delta(\boldsymbol{k})$ 的统计分布。由于我们生成的是高斯随机场，每个 $\delta(\boldsymbol{k})$ 都应该是一个（复）高斯随机变量。其方差由功率谱 $P(k)$ 和所选用的离散傅里叶变换 (DFT) 约定共同决定。一个常见的约定是 [@problem_id:3473755]：
$$
\langle |\delta(\boldsymbol{k})|^2 \rangle = \langle \delta(\boldsymbol{k}) \delta^*(\boldsymbol{k}) \rangle = V P(k) = L^3 P(k)
$$
而对于其他的傅里叶变换约定，这个关系式可能会有不同的归一化因子。例如，对于另一种常见的FFT约定，方差为 $\langle |\tilde{\delta}(\boldsymbol{k})|^2 \rangle = P(k)/V$ [@problem_id:3473713]。在实践中，必须确保所用代码库的约定与此处的理论推导相匹配。

#### 分步生成算法

综合以上原理，生成高斯随机场的算法流程如下 [@problem_id:3473755]：

1.  **遍历独立模式**：在傅里叶晶格中，只遍历一半的独立模式。这通常通过一个循环实现，例如，遍历所有 $k_z > 0$ 的模式，以及 $k_z=0$ 平面上一半的模式。

2.  **生成高斯随机数**：对于每一个需要生成的独立模式 $\delta(\boldsymbol{k})$，我们需要生成一个或两个服从标准正态分布 $\mathcal{N}(0,1)$ 的随机数。这可以通过**Box-Muller变换**实现：从两个独立的均匀分布 $U_1, U_2 \sim \mathrm{Uniform}(0,1)$ 的随机数，可以生成两个独立的标准正态随机数 $Z_1, Z_2$：
    $$
    Z_1 = \sqrt{-2\ln U_1} \cos(2\pi U_2), \quad Z_2 = \sqrt{-2\ln U_1} \sin(2\pi U_2)
    $$

3.  **构建傅里叶系数**：根据模式的类型，用生成的正态随机数构建 $\delta(\boldsymbol{k})$：
    *   **对于非自共轭的复数模式** ($\boldsymbol{k} \neq -\boldsymbol{k}$):
        $\delta(\boldsymbol{k})$ 是一个复高斯变量，其实部和虚部是两个独立的、方差相同的高斯变量。根据 $\langle |\delta(\boldsymbol{k})|^2 \rangle = \langle (\text{Re}[\delta])^2 \rangle + \langle (\text{Im}[\delta])^2 \rangle = L^3 P(k)$，我们要求实部和虚部的方差均为 $\frac{L^3 P(k)}{2}$。因此，我们设置：
        $$
        \delta(\boldsymbol{k}) = \sqrt{\frac{L^3 P(k)}{2}} (Z_1 + i Z_2)
        $$
        这等价于生成一个瑞利分布的振幅和一个均匀分布的相位。
    *   **对于自共轭的实数模式** ($\boldsymbol{k} = -\boldsymbol{k}$ 且 $\boldsymbol{k} \neq \boldsymbol{0}$):
        $\delta(\boldsymbol{k})$ 是一个实高斯变量，其方差为 $\langle \delta(\boldsymbol{k})^2 \rangle = L^3 P(k)$。因此，我们只需生成一个标准正态随机数 $Z_1$ 并设置：
        $$
        \delta(\boldsymbol{k}) = \sqrt{L^3 P(k)} Z_1
        $$
    *   **对于直流模式** ($\boldsymbol{k} = \boldsymbol{0}$):
        通常直接设为 $\delta(\boldsymbol{0}) = 0$。

4.  **施加赫米特对称性**：完成对一半傅里叶空间的填充后，利用 $\delta(-\boldsymbol{k}) = \delta^*(\boldsymbol{k})$ 关系式计算出另一半空间的所有傅里叶系数。

5.  **傅里叶逆变换**：至此，我们得到了一个完整的、满足所有统计和对称性要求的傅里叶系数网格。对其进行三维快速傅里叶逆变换，即可得到实空间中的高斯随机密度场 $\delta(\boldsymbol{x})$。

这个过程可以被概念化为：从一个傅里叶空间的白噪声场（所有模式的实部和虚部都是独立的、方差相同的随机数）开始，然后通过乘以一个“滤波器” $W(\boldsymbol{k}) \propto \sqrt{P(k)}$，来为这个白噪声“着色”，从而赋予其期望的宇宙学相关性 [@problem_id:3473766]。

### 有限体积效应

在有限体积的盒子中生成随机场，不可避免地会引入一些与无限宇宙的真实情况有所偏差的效应。

#### 样本方差与宇宙方差

模拟盒子只能包含波长小于等于盒子尺寸 $L$ 的涨落模式，即 $k \ge k_f = 2\pi/L$。这意味着所有比盒子更大的尺度的涨落都被忽略了。此外，对于接近盒子尺寸的尺度（低 $k$ 值），离散的傅里叶模式非常稀疏。我们从这些稀疏模式中抽取的几个随机振幅，只是所有可能实现中的一个样本。这种由于只观测到有限模式而产生的统计涨落，被称为**样本方差 (sample variance)**，在宇宙学背景下也常被称为**宇宙方差 (cosmic variance)**。它导致在模拟中测量出的统计量（如功率谱或相关函数）会围绕真实的系综平均值产生涨落，尤其是在大尺度上，误差会非常大 [@problem_id:3473712]。

#### 积分约束及其影响

如前所述，为了与宇宙的平均密度相匹配，我们通常强制盒子内的平均密度涨落为零，即 $\delta(\boldsymbol{0}) = 0$。这意味着整个盒子内的密度涨落积分必须为零：$\int_V \delta(\boldsymbol{x}) d^3x = 0$。这个被称为**积分约束 (integral constraint)** 的条件，会在测量相关函数时引入系统性的偏差。为了在全空间积分后得到零，正的短程相关必须由负的长程相关来抵消。因此，在有限盒子中测得的相关函数 $\hat{\xi}(r)$ 在大尺度（$r \sim L/2$）上会系统性地低于真实的宇宙相关函数 $\xi_{\text{true}}(r)$ [@problem_id:3473712]。

#### 对有限体积效应的物理解释

有限体积导致的样本方差可以通过一个优雅的物理解释来量化。考虑盒子内平均密度 $\delta_{\mathrm{DC}}$ 的方差。一方面，从离散傅里叶理论可知，$\delta_{\mathrm{DC}} = \delta_{\boldsymbol{0}}/V$，其方差为 $\langle \delta_{\mathrm{DC}}^2 \rangle = \frac{P(0)}{V} = \frac{P(0)}{L^3}$。另一方面，我们可以将盒子平均操作类比为用一个特征尺度为 $R$ 的平滑窗口对无限大的连续场进行平滑。若采用高斯窗口，平滑后场的方差为 $\sigma_R^2 = \int \frac{d^3k}{(2\pi)^3} P(k) e^{-k^2R^2}$。在功率谱近似为常数 $P(k) \approx A$ 的大尺度极限下，此方差为 $\sigma_R^2 = \frac{A}{8\pi^{3/2}R^3}$。

通过令这两种计算方法得到的方差相等，$\frac{A}{L^3} = \frac{A}{8\pi^{3/2}R^3}$，我们可以求解出与盒子尺寸 $L$ 等效的高斯平滑半径 $R$ [@problem_id:3473826]：
$$
\frac{R}{L} = \frac{1}{2\sqrt{\pi}}
$$
这个结果提供了一个深刻的洞见：在一个边长为 $L$ 的有限盒子中进行模拟，其固有的样本方差效应，等价于用一个尺度约为 $L/(2\sqrt{\pi})$ 的高斯核去平滑观测整个无限宇宙。这清晰地表明，模拟盒子的尺寸直接设定了我们能够可靠研究的宇宙学现象的尺度下限。