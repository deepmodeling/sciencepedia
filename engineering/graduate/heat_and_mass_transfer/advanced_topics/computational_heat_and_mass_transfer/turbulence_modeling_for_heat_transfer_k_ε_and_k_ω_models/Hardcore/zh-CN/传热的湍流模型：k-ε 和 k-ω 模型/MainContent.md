## 引言
湍流传热是航空航天、能源工程和化学过程等众多领域中的核心物理现象。然而，湍流固有的混沌和多尺度特性使得通过直接数值模拟（DNS）精确预测传热变得计算成本极高，难以应用于工程实践。因此，开发能够以可接受的计算资源捕捉湍流对平均流动和传热影响的简化模型，即雷诺平均Navier-Stokes（RANS）湍流模型，成为了计算流体力学（CFD）领域的关键挑战。尽管$k$-$\varepsilon$和$k$-$\omega$等模型被广泛应用，但对其背后的原理、适用边界以及在不同物理场景下的性能差异，许多工程师和研究人员仍缺乏系统性的理解。

本文旨在填补这一知识鸿沟，为读者提供一份关于主流两方程湍流传热模型的全面指南。通过本文的学习，您将系统地掌握这些工业界和学术界基石模型的理论精髓与应用技巧。

在接下来的内容中，我们将分三部分展开：首先，在**“原理与机制”**一章中，我们将深入剖析雷诺平均、Boussinesq假设、$k$-$\varepsilon$与$k$-$\omega$模型的构建，以及近壁处理等核心概念。接着，在**“应用与跨学科联系”**一章中，我们将展示这些模型在从基础平板流到复杂分离流、共轭传热、可压缩流等多样化工程场景中的具体应用与性能表现。最后，**“动手实践”**部分将提供一系列练习，帮助您将理论知识转化为解决实际问题的能力。让我们首先从理解这些模型的基本原理开始。

## 原理与机制

在对流换热的研究中，湍流的出现从根本上改变了动量、热量和质量的输运过程。与可预测的层流不同，湍流的特点是流场中存在不规则、混沌的三维涡旋运动。这些湍流涡旋极大地增强了流体质点间的混合，从而显著提高了动量和标量（如温度）的输运速率。直接数值模拟（DNS）可以完全解析湍流的所有时空尺度，但其计算成本极高，对于工程实践中常见的高雷诺数流动而言是不可行的。因此，我们需要发展能够以可接受的计算成本捕捉湍流对平均流动和传热影响的模型，即湍流模型。

本章旨在阐述用于传热预测的雷诺平均Navier-Stokes（RANS）湍流模型的基本原理和机制，重点关注两类应用最广泛的两方程模型：$k$-$\varepsilon$模型和$k$-$\omega$模型。

### 雷诺平均与封闭问题

湍流建模的第一步是通过**雷诺平均**（Reynolds averaging）将瞬时流场分解为平均部分和脉动部分。对于任何瞬时量$\phi$，我们有$\phi = \langle \phi \rangle + \phi'$，其中$\langle \phi \rangle$是时间平均或系综平均量，$\phi'$是脉动量。将此分解应用于不可压缩流动的控制方程（Navier-Stokes方程和能量方程），然后对整个方程进行平均，可以得到描述平均流场演化的方程。

对于具有恒定物性的不可压缩牛顿流体，在无内热源、无粘性耗散且温度为被动标量（即不影响流动）的假设下，平均后的连续性方程、动量方程和能量方程如下所示 [@problem_id:2535349]：

**平均连续性方程:**
$$
\frac{\partial \langle u_i \rangle}{\partial x_i} = 0
$$

**雷诺平均Navier-Stokes (RANS) 方程 (动量方程):**
$$
\rho\left(\frac{\partial \langle u_i \rangle}{\partial t} + \langle u_j \rangle \frac{\partial \langle u_i \rangle}{\partial x_j}\right) = -\frac{\partial \langle p \rangle}{\partial x_i} + \mu \frac{\partial^2 \langle u_i \rangle}{\partial x_j \partial x_j} - \rho \frac{\partial \langle u_i' u_j' \rangle}{\partial x_j}
$$

**平均能量方程:**
$$
\rho c_p\left(\frac{\partial \langle T \rangle}{\partial t} + \langle u_j \rangle \frac{\partial \langle T \rangle}{\partial x_j}\right) = k_f \frac{\partial^2 \langle T \rangle}{\partial x_j \partial x_j} - \rho c_p \frac{\partial \langle u_j' T' \rangle}{\partial x_j}
$$

在这些方程中，$u_i$、$p$和$T$分别是速度、压力和温度；$\rho$、$\mu$、$c_p$和$k_f$分别是密度、动力粘度、定压比热容和流体导热系数。尖括号$\langle \cdot \rangle$表示平均算子。

仔细观察这些方程，我们会发现平均过程引入了新的未知项。在动量方程中，出现了$\langle u_i' u_j' \rangle$项，这是一个二阶张量。$\tau^R_{ij} \equiv -\rho \langle u_i' u_j' \rangle$被称为**雷诺应力张量**（Reynolds stress tensor）。它代表了由速度脉动引起的动量输运，其作用类似于一个附加的应力。类似地，在能量方程中，出现了$\langle u_j' T' \rangle$项，这是一个向量。$q^t_j \equiv \rho c_p \langle u_j' T' \rangle$被称为**湍流热通量向量**（turbulent heat flux vector），代表了由湍流脉动引起的热量输运。

这些新出现的项（雷诺应力和湍流热通量）包含未知脉动量的相关性，无法直接从平均量$\langle u_i \rangle$、$\langle p \rangle$和$\langle T \rangle$中求解。未知数的数量超过了方程的数量，使得方程组不封闭。这就是湍流建模的核心挑战，即**封闭问题**（closure problem）。湍流模型的核心任务就是提供额外的方程或代数关系，以近似这些未知项，从而使方程组得以求解。

### Boussinesq涡粘性假设

为了解决封闭问题，最流行的方法是引入**Boussinesq涡粘性假设**（Boussinesq hypothesis）。这个假设的核心思想是，湍流对平均流动的动量输运作用在形式上类似于分子粘性引起的动量输运。具体来说，它假设雷诺应力张量与平均应变率张量之间存在线性关系 [@problem_id:2535353]：
$$
-\rho\,\overline{u_i' u_j'} = 2\,\mu_t\,S_{ij} - \frac{2}{3}\,\rho\,k\,\delta_{ij}
$$
其中，$\overline{\cdot}$是平均算子（为简洁起见，后续将省略尖括号），$S_{ij} \equiv \frac{1}{2}\left(\frac{\partial U_i}{\partial x_j} + \frac{\partial U_j}{\partial x_i}\right)$是**平均应变率张量**，$k \equiv \frac{1}{2}\overline{u_i' u_i'}$是**湍流脉动能**（turbulent kinetic energy, TKE），$\delta_{ij}$是克罗内克符号。

这个表达式中的新量$\mu_t$被称为**湍流粘度**或**涡粘度**（turbulent/eddy viscosity）。与作为流体固有属性的分子粘度$\mu$不同，$\mu_t$是湍流本身的属性，反映了湍流混合的强度，它随空间位置和流动状态而变化。方程右侧的第二项是为了确保在不可压缩流动中（$S_{ii}=0$），张量的迹（trace）能够正确地等于$-2\rho k$。

类似地，湍流热通量也可以通过一个类似的**梯度扩散假设**（gradient diffusion hypothesis）来建模：
$$
\rho c_p \overline{u_j' T'} = -k_t \frac{\partial T}{\partial x_j}
$$
这里，$k_t$是**湍流热导率**（turbulent thermal conductivity）。通常，我们使用**湍流热扩散系数**（turbulent thermal diffusivity）$\alpha_t = k_t / (\rho c_p)$来表示，因此：
$$
\overline{u_j' T'} = -\alpha_t \frac{\partial T}{\partial x_j}
$$
这个假设意味着湍流热通量与平均温度梯度成正比，并指向温度降低的方向，这与傅里叶热传导定律形式上完全一致。

通过Boussinesq假设，我们将封闭问题转化为了如何确定涡粘度$\mu_t$（或运动涡粘度$\nu_t = \mu_t/\rho$）和湍流热扩散系数$\alpha_t$的问题。

### 两方程模型的基本构件

两方程模型通过求解两个独立的输运方程来确定涡粘度$\nu_t$。这两个方程描述了湍流的两个关键尺度量：一个代表能量（或速度）尺度，另一个代表长度或时间尺度。

最常用的量是湍流脉动能$k$和它的耗散率$\varepsilon$。通过量纲分析，我们可以理解它们的物理意义 [@problem_id:2535382]：
- **湍流脉动能 (k)**：定义为单位质量流体的脉动动能，$k = \frac{1}{2}\overline{u_i' u_i'}$。它的量纲是$[k] = L^2 T^{-2}$。因此，$\sqrt{k}$具有速度的量纲，可以被看作是湍流涡的**特征速度尺度**，$u_t \sim \sqrt{k}$。

- **湍流耗散率 ($\varepsilon$)**: 定义为单位质量流体的湍流脉动能由于分子粘性作用而转化为内能的速率。它的量纲是$[\varepsilon] = L^2 T^{-3}$。$\varepsilon$代表了能量从大尺度涡向小尺度涡传递（即**能量级串**）并最终耗散的速率。

利用$k$和$\varepsilon$，我们可以构建出湍流的特征时间和长度尺度：
- **特征时间尺度 ($\tau_t$)**: $\tau_t \sim k/\varepsilon$。其量纲为$[k]/[\varepsilon] = (L^2 T^{-2}) / (L^2 T^{-3}) = T$。这可以理解为大涡翻转一周所需的时间。

- **特征长度尺度 ($\ell_t$)**: $\ell_t \sim u_t \tau_t \sim \sqrt{k} (k/\varepsilon) = k^{3/2}/\varepsilon$。这代表了能量主要集中的大涡的尺寸。

涡粘度$\nu_t$具有扩散系数的量纲 ($L^2 T^{-1}$)，可以认为它正比于特征速度尺度和特征长度尺度的乘积：
$$
\nu_t \sim u_t \ell_t \sim \sqrt{k} \cdot \frac{k^{3/2}}{\varepsilon} = \frac{k^2}{\varepsilon}
$$
这就为$k$-$\varepsilon$模型中的涡粘度计算提供了理论基础。

另一种选择是使用**比耗散率**（specific dissipation rate）$\omega$。它被定义为$\omega \sim \varepsilon/k$，其量纲为$[\omega] = (L^2 T^{-3}) / (L^2 T^{-2}) = T^{-1}$。因此，$\omega$可以被解释为湍流的**特征频率**或特征时间的倒数。在这种情况下，涡粘度的计算变为：
$$
\nu_t \sim u_t \ell_t = u_t (u_t / \omega) = u_t^2 / \omega \sim k/\omega
$$
这为$k$-$\omega$模型中涡粘度的计算奠定了基础。

### 标准$k$-$\varepsilon$模型

标准$k$-$\varepsilon$模型是最经典的湍流模型之一。它为湍流脉动能$k$和其耗散率$\varepsilon$建立了两套输运方程。对于不可压缩流动，其标准形式如下 [@problem_id:2535326]：

**$k$方程:**
$$
\frac{\partial (\rho k)}{\partial t} + \frac{\partial (\rho U_j k)}{\partial x_j} = \frac{\partial}{\partial x_j}\left[\left(\mu + \frac{\mu_t}{\sigma_k}\right)\frac{\partial k}{\partial x_j}\right] + P_k - \rho \varepsilon
$$

**$\varepsilon$方程:**
$$
\frac{\partial (\rho \varepsilon)}{\partial t} + \frac{\partial (\rho U_j \varepsilon)}{\partial x_j} = \frac{\partial}{\partial x_j}\left[\left(\mu + \frac{\mu_t}{\sigma_\varepsilon}\right)\frac{\partial \varepsilon}{\partial x_j}\right] + C_{\varepsilon 1}\,\frac{\varepsilon}{k}\,P_k - C_{\varepsilon 2}\,\rho\,\frac{\varepsilon^2}{k}
$$

**涡粘度**由以下公式给出：
$$
\mu_t = C_\mu \rho \frac{k^2}{\varepsilon}
$$

方程中的各项具有明确的物理意义：
- 左侧两项分别是$k$或$\varepsilon$的**瞬态项**和**对流输运项**。
- 右侧第一项是**扩散项**，包括了分子扩散（$\mu$）和湍流扩散（$\mu_t$）。$\sigma_k$和$\sigma_\varepsilon$分别是$k$和$\varepsilon$的湍流普朗特数。
- $P_k = -\rho \overline{u_i' u_j'} \frac{\partial U_i}{\partial x_j}$是**湍流生成项**，表示平均流动的动能通过应变作用转化为湍流脉动能的速率。
- $\rho \varepsilon$是$k$方程中的**耗散项**，表示湍流脉动能的耗散。
- 在$\varepsilon$方程中，$C_{\varepsilon 1}$项是**生成项**，$C_{\varepsilon 2}$项是**耗散项**。

这些方程包含五个经验常数，其标准值是通过拟合多种典型湍流（如均匀各向同性衰减湍流、近壁面对数律区）的实验数据得到的：
$$
C_\mu = 0.09, \quad C_{\varepsilon 1} = 1.44, \quad C_{\varepsilon 2} = 1.92, \quad \sigma_k = 1.0, \quad \sigma_\varepsilon = 1.3
$$

### 湍流热输运与湍流普朗特数

一旦涡粘度$\nu_t$通过求解$k$和$\varepsilon$（或$k$和$\omega$）方程得到，我们就可以确定湍流热扩散系数$\alpha_t$。两者之间的关系通过**湍流普朗特数**（turbulent Prandtl number）$Pr_t$来定义 [@problem_id:2535365]：
$$
Pr_t = \frac{\nu_t}{\alpha_t}
$$
因此，$\alpha_t = \nu_t / Pr_t$。将此关系代入平均能量方程，可以得到包含湍流模型在内的完整形式：
$$
\rho c_p\left(\frac{\partial T}{\partial t} + U_j \frac{\partial T}{\partial x_j}\right) = \frac{\partial}{\partial x_j}\left[\left(k_f + \frac{\mu_t c_p}{Pr_t}\right)\frac{\partial T}{\partial x_j}\right]
$$
或者使用扩散系数表示：
$$
\frac{\partial T}{\partial t} + U_j\frac{\partial T}{\partial x_j} = \frac{\partial}{\partial x_j}\left[\left(\alpha + \frac{\nu_t}{Pr_t}\right)\frac{\partial T}{\partial x_j}\right]
$$
其中$\alpha$是分子热扩散系数。这里的有效热扩散系数为$\alpha_{\text{eff}} = \alpha + \alpha_t = \alpha + \nu_t/Pr_t$。

$Pr_t$的物理意义是湍流输运过程中动量扩散与热量扩散能力的比值。对于大多数气体和简单剪切流，实验表明$Pr_t$的值约在0.7到0.9之间。因此，在许多工程计算中，简单地将其取为一个常数（如0.85）是常见的做法。然而，这种假设意味着湍流对动量和热量的输运效率之比在整个流场中保持不变。在更复杂的流动中，如靠近壁面、存在分离或强烈曲率的区域，动量和热量的输运机制可能存在差异，$Pr_t$可能不再是常数。在这种情况下，使用**可变的湍流普朗特数模型**能够提供更准确的传热预测。

值得注意的是，对于被动标量传热，改变$Pr_t$的值只会影响温度场的求解，而不会影响速度场和湍流场（$k$和$\varepsilon$）的计算。$Pr_t \to \infty$意味着$\alpha_t \to 0$，即完全抑制湍流热扩散；而$Pr_t \to 0$则意味着极强的湍流热扩散，会迅速抹平温度梯度。

### 近壁处理：壁面函数与低雷诺数模型

标准$k$-$\varepsilon$模型是**高雷诺数模型**，它假设湍流是充分发展的，分子粘性的影响可以忽略。这个假设在靠近固体壁面的区域（粘性底层和缓冲层）失效。因此，标准$k$-$\varepsilon$模型不能直接应用于壁面。

解决这个问题的一种常用方法是**壁面函数**（wall functions）[@problem_id:2535321]。其思想是避免直接解析近壁区域，而是在计算网格的第一个离壁节点（通常放置在对数律区，$30 \lesssim y^+ \lesssim 300$）和壁面之间架起一座“桥梁”。这座桥梁基于对近壁流动的半经验理论，即**壁面律**（law of the wall）。

壁面函数的实施步骤如下：
1.  **壁面剪应力**: 通过求解对数律方程 $U^+ = \frac{1}{\kappa}\ln(y^+) + B$ 来迭代计算摩擦速度$u_\tau = \sqrt{\tau_w/\rho}$，从而得到壁面剪应力$\tau_w$。这里$U^+ = U/u_\tau$和$y^+ = y u_\tau / \nu$是无量纲速度和距离，$\kappa$是冯·卡门常数（约0.41），$B$是常数（约5.2）。
2.  **湍动能边界条件**: 在对数律区，湍流生成与耗散近似平衡（$P_k \approx \rho\varepsilon$），并且雷诺切应力与湍动能的比值近似为常数（$-\overline{u'v'}/k \approx \sqrt{C_\mu}$）。由此可以推导出第一个离壁节点$p$处的湍动能值：
    $$
    k_p = \frac{u_\tau^2}{\sqrt{C_\mu}}
    $$
3.  **耗散率边界条件**: 同样在平衡假设下，可以推导出耗散率的表达式：
    $$
    \varepsilon_p = \frac{u_\tau^3}{\kappa y_p}
    $$
其中$y_p$是第一个离壁节点的法向距离。这些$k_p$和$\varepsilon_p$的值被用作$k$和$\varepsilon$输运方程的狄利克雷边界条件。

壁面函数法经济高效，但其精度依赖于网格的第一个节点必须精确地位于对数律区，且流动必须满足平衡假设。对于存在强烈压力梯度、分离、再附等复杂现象的流动，壁面函数法的准确性会显著下降。

### $k$-$\omega$模型：一种近壁性能更优的选择

$k$-$\omega$模型是另一种流行的两方程模型。它求解湍流脉动能$k$和比耗散率$\omega$的输运方程。Wilcox $k$-$\omega$模型（以2006年版本为例）的方程组如下 [@problem_id:2535363]：

**$k$方程:**
$$
\frac{\partial k}{\partial t} + U_j\frac{\partial k}{\partial x_j} = P_k - \beta^{\ast}\,k\,\omega + \frac{\partial}{\partial x_j}\left[\left(\nu + \sigma_k\,\nu_t\right)\frac{\partial k}{\partial x_j}\right]
$$

**$\omega$方程:**
$$
\frac{\partial \omega}{\partial t} + U_j\frac{\partial \omega}{\partial x_j} = \alpha\,\frac{\omega}{k}\,P_k - \beta\,\omega^2 + \frac{\partial}{\partial x_j}\left[\left(\nu + \sigma_{\omega}\,\nu_t\right)\frac{\partial \omega}{\partial x_j}\right] + \sigma_d\,\frac{1}{\omega}\,\frac{\partial k}{\partial x_j}\,\frac{\partial \omega}{\partial x_j}
$$

**涡粘度**由以下公式给出：
$$
\nu_t = \frac{k}{\omega}
$$
其中，$\alpha, \beta, \beta^{\ast}, \sigma_k, \sigma_{\omega}$是模型常数。$\omega$方程中的最后一项是**交叉扩散项**，用于改善模型的某些性能。

$k$-$\omega$模型的一个显著优势是它能够直接积分求解穿过粘性底层，而无需使用壁面函数。这种**低雷诺数**能力源于$\omega$变量在近壁区的良好数学特性 [@problem_id:2535389]。在壁面附近（$y \to 0$），唯一相关的局部物理量是离壁距离$y$和运动粘度$\nu$。通过量纲分析，我们可以确定$\omega$（量纲为$T^{-1}$）的渐近行为：
$$
\omega \sim \frac{\nu}{y^2} \quad \text{as } y \to 0
$$
这意味着$\omega$在壁面上趋于无穷大。现在考察涡粘度$\nu_t = k/\omega$。由于湍动能$k$在壁面上必须为零（$k \sim y^2$），我们得到：
$$
\nu_t = \frac{k}{\omega} \sim \frac{O(y^2)}{O(\nu/y^2)} = O(y^4)
$$
这个结果表明，$\nu_t$在壁面附近以$y^4$的速率趋近于零，这正确地反映了湍流输运在壁面处消失的物理事实。由于$\omega$方程的这种良好行为，$k$-$\omega$模型能够自然地处理近壁区域的物理过程，从而在预测壁面剪应力和壁面热通量方面通常比使用壁面函数的$k$-$\varepsilon$模型更准确，尤其是在存在压力梯度和分离的流动中。

### 高级模型：剪切应力输运（SST）$k$-$\omega$模型

尽管标准$k$-$\omega$模型在近壁区表现出色，但它对自由流中的$\omega$值很敏感。相反，$k$-$\varepsilon$模型在自由流区则更为鲁棒。Menter提出的**剪切应力输运（SST）$k$-$\omega$模型**巧妙地结合了这两种模型的优点 [@problem_id:2535351]。

SST模型通过一个**混合函数**$F_1$实现两种模型的切换。$F_1$在近壁区（边界层内部）的值为1，在远离壁面的区域（自由流区）平滑地过渡到0。SST模型的方程被构造成当$F_1=1$时，它等效于标准$k$-$\omega$模型；当$F_1=0$时，它等效于一个经过变换的$k$-$\varepsilon$模型。这样，SST模型既利用了$k$-$\omega$模型在近壁区的精度，又利用了$k$-$\varepsilon$模型在自由流区的鲁棒性。

SST模型的另一个核心特征是引入了对涡粘度的**剪切应力限制器**：
$$
\nu_{t} = \frac{a_{1} k}{\max\!\left(a_{1}\,\omega, \, S \, F_{2}\right)}
$$
其中，$a_1$是常数，$S$是应变率的大小，$F_2$是另一个混合函数。这个限制器的作用是防止在逆压梯度和分离流等高应变率区域，涡粘度被过度预测。标准模型在这些区域往往会高估湍流剪切应力，从而导致对流动分离点的预测延迟。通过限制$\nu_t$的大小，SST模型能够更准确地预测流动分离。

对于传热问题，这一改进至关重要。流动分离区通常伴随着传热的显著降低。由于$\alpha_t = \nu_t/Pr_t$，对$\nu_t$的限制会直接导致对湍流热扩散的限制。因此，SST模型能够捕捉到分离区传热受到抑制的现象，其预测结果与实验数据更为吻合，而没有限制器的模型则会严重高估分离区的壁面热通量。

### Boussinesq假设的局限性：各向同性问题

尽管$k$-$\varepsilon$和$k$-$\omega$系列模型在工程中取得了巨大成功，但它们都基于一个共同的、根本性的简化假设：Boussinesq涡粘性假设。这个假设的核心问题在于它使用了**标量**涡粘度$\mu_t$和**标量**湍流热扩散系数$\alpha_t$ [@problem_id:2535329]。

使用标量系数意味着模型本质上是**各向同性**的（isotropic）。它假定湍流对动量和热量的输运在所有方向上都具有相同的效率。具体来说：
1.  **雷诺应力**: Boussinesq假设强制雷诺应力张量的主轴与平均应变率张量的主轴对齐。这导致模型无法准确描述湍流法向应力之间的差异（例如，$\overline{u'^2} \neq \overline{v'^2}$），而这种差异在许多流动中是驱动二次流等现象的关键。
2.  **湍流热通量**: 梯度扩散假设 $\overline{\mathbf{u}' T'} = -\alpha_t \nabla T$ 强制湍流热通量向量必须与平均温度梯度向量**反平行**。

在许多复杂流动中，这种各向同性的假设与物理现实严重不符。例如：
- 在方形管道的充分发展流动中，角部的湍流法向应力各向异性会驱动出垂直于主流方向的二次涡流。这些涡流能够将核心区的高温流体输送到壁面，或者反之，即使在局部温度梯度为零的地方也能产生热通量。各向同性模型无法预测这种现象。
- 在流动分离区或旋转流中，湍流结构具有很强的各向异性。热量可能主要由大的相干结构沿特定方向输运，导致热通量向量与温度梯度向量之间存在显著夹角。Boussinesq假设无法捕捉这种**非对齐**（misalignment）输运。
- 在某些极端情况下，甚至可能出现**逆梯度输运**（counter-gradient transport），即热量从低温区向高温区输运，这与梯度扩散假设完全相悖。

综上所述，虽然两方程涡粘性模型是湍流传热计算的强大工具，但使用者必须认识到其固有的各向同性假设。当流动中的湍流结构表现出强烈的各向异性、旋转、曲率或二次流效应时，这些模型的预测精度可能会受到限制。在这种情况下，需要采用更高级的模型，如代数应力模型（ASM）或雷诺应力模型（RSM），它们直接为雷诺应力张量的各个分量求解输运方程，从而能够更准确地捕捉湍流的各向异性效应。