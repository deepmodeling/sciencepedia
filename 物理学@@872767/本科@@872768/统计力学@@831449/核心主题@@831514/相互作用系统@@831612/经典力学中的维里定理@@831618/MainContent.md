## 引言
在物理学的广阔天地中，存在着一些深刻的原理，它们能够跨越不同的尺度和领域，将看似无关的现象联系起来。经典力学中的[维里定理](@entry_id:146441)（Virial Theorem）正是这样一个优雅而强大的工具。它在系统微观粒子的平均动能与作用于其上的力之间建立了一座桥梁，解决了如何从底层动力学推导宏观性质（如温度和压强）这一核心问题。对于初学者而言，物理学往往被分割为独立的子领域，而维里定理则展示了不同分支——从[天体力学](@entry_id:147389)到[统计力](@entry_id:194984)学——之间深刻的内在统一性。

本文将系统性地引导你掌握[维里定理](@entry_id:146441)的精髓。在第一章“原理与机制”中，我们将从基本定义出发，推导出维里定理的一般形式，并探讨其在齐次势能下的简洁表达。接着，在第二章“应用与跨学科联系”中，我们将见证该定理如何在天体物理学中解释恒星的演化，在原子物理中描述能量平衡，并为[统计力](@entry_id:194984)学中的物态方程提供理论基础。最后，通过第三章“动手实践”中的精选问题，你将有机会亲自运用维里定理解决具体的物理情境，将理论知识转化为解决问题的能力。通过这一系列的学习，你将不仅掌握一个重要的物理定理，更能体会到物理学中普遍性与统一性的美感。

## 原理与机制

在本章中，我们将深入探讨经典力学中一个极为深刻且应用广泛的定理——[维里定理](@entry_id:146441) (Virial Theorem)。维里定理在系统的[平均动能](@entry_id:146353)与作用于系统内部的力的性质之间建立了一座桥梁。它不仅为天体物理、等离子体物理和[分子动力学](@entry_id:147283)等领域提供了强大的理论工具，也为理解宏观[热力学](@entry_id:141121)量（如压强）与微观粒子动力学之间的联系提供了独特的视角。

### 维里量的引入与基本定理

为了建立维里定理，我们首先定义一个标量函数，通常称为**维里函数** (virial function) 或简称**维里** (virial)，其定义为系统中所有粒子的位置矢量与动量矢量点积之和。对于一个包含 $N$ 个粒子的系统，维里函数 $G$ 的表达式为：

$$
G = \sum_{i=1}^{N} \vec{p}_i \cdot \vec{r}_i
$$

其中 $\vec{r}_i$ 是第 $i$ 个粒子的位置矢量，$\vec{p}_i$ 是其动量。

[维里定理](@entry_id:146441)的核心思想在于考察 $G$ 随时间的变化率 $\frac{dG}{dt}$。利用乘积的[求导法则](@entry_id:145443)，我们得到：

$$
\frac{dG}{dt} = \sum_{i=1}^{N} \left( \frac{d\vec{p}_i}{dt} \cdot \vec{r}_i + \vec{p}_i \cdot \frac{d\vec{r}_i}{dt} \right)
$$

根据牛顿第二定律，$\frac{d\vec{p}_i}{dt} = \vec{F}_i$，其中 $\vec{F}_i$ 是作用在第 $i$ 个粒子上的总力。同时，根据动量的定义 $\vec{p}_i = m_i \vec{v}_i$，我们有 $\frac{d\vec{r}_i}{dt} = \vec{v}_i$。代入上式可得：

$$
\frac{dG}{dt} = \sum_{i=1}^{N} \left( \vec{F}_i \cdot \vec{r}_i + m_i \vec{v}_i \cdot \vec{v}_i \right) = \sum_{i=1}^{N} \vec{F}_i \cdot \vec{r}_i + \sum_{i=1}^{N} m_i v_i^2
$$

我们注意到，系统的总动能 $K$ 为 $K = \sum_{i=1}^{N} \frac{1}{2} m_i v_i^2$，因此 $\sum_{i=1}^{N} m_i v_i^2 = 2K$。于是，我们得到了维里函数时间导数的基本表达式：

$$
\frac{dG}{dt} = 2K + \sum_{i=1}^{N} \vec{F}_i \cdot \vec{r}_i
$$

现在，我们考虑对上式取长时间平均。用尖括号 $\langle \cdot \rangle$ 表示[时间平均](@entry_id:267915)，我们有：

$$
\left\langle \frac{dG}{dt} \right\rangle = 2\langle K \rangle + \left\langle \sum_{i=1}^{N} \vec{F}_i \cdot \vec{r}_i \right\rangle
$$

对于一个稳定且在空间上**有界**的系统（即所有粒子的位置和速度都保持在有限范围内），维里函数 $G$ 的值也将在一个有限的范围[内波](@entry_id:261048)动。因此，在足够长的时间 $\tau$ 内，$G$ 的净变化量 $G(\tau) - G(0)$ 是有限的。其[时间平均](@entry_id:267915)值为：

$$
\left\langle \frac{dG}{dt} \right\rangle = \lim_{\tau \to \infty} \frac{1}{\tau} \int_0^\tau \frac{dG}{dt} dt = \lim_{\tau \to \infty} \frac{G(\tau) - G(0)}{\tau} = 0
$$

由此，我们得到了**[经典维里定理](@entry_id:198504)**的一般形式：

$$
2\langle K \rangle + \left\langle \sum_{i=1}^{N} \vec{F}_i \cdot \vec{r}_i \right\rangle = 0
$$

这个等式表明，一个稳定有界系统的平均总动能的两倍，等于所有粒子所受的力与其位置矢量点积之和的平均值的负值。这个力的项 $\sum \vec{F}_i \cdot \vec{r}_i$ 正是 Rudolf Clausius 最初定义的“维里”。

### 势能力量下的[维里定理](@entry_id:146441)与齐次势

维里定理最常见的应用场景是当系统中的力是[保守力](@entry_id:170586)，即可以从一个势能函数 $U(\vec{r}_1, \dots, \vec{r}_N)$ 导出：$\vec{F}_i = -\nabla_i U$。在这种情况下，[维里定理](@entry_id:146441)变为：

$$
2\langle K \rangle = \left\langle \sum_{i=1}^{N} \vec{r}_i \cdot \nabla_i U \right\rangle
$$

这个表达式的实用性在一个特殊但非常重要的[势能](@entry_id:748988)类别中得到了极大的体现——**齐次势能函数 (homogeneous potential function)**。如果一个[势能函数](@entry_id:200753) $U$ 对于所有坐标进行等比例缩放 $\lambda$ 时，函数值会缩放 $\lambda^n$ 倍，即：

$$
U(\lambda\vec{r}_1, \dots, \lambda\vec{r}_N) = \lambda^n U(\vec{r}_1, \dots, \vec{r}_N)
$$

则称该势能函数为 $n$ 次齐次函数。对于这样的函数，**[欧拉齐次函数定理](@entry_id:186434) (Euler's homogeneous function theorem)** 指出：

$$
\sum_{i=1}^{N} \vec{r}_i \cdot \nabla_i U = n U
$$

将此结果代入[维里定理](@entry_id:146441)，我们得到了一个极其简洁而优美的形式：

$$
2\langle K \rangle = n \langle U \rangle
$$

这个形式将系统的[平均动能](@entry_id:146353) $\langle K \rangle$ 和平均[势能](@entry_id:748988) $\langle U \rangle$ 直接联系起来，系数 $n$ 完全由势能函数的齐次次数决定。

### 在物理系统中的应用

让我们通过几个例子来体会这一强大工具的应用。

#### 谐振子与[平方反比定律](@entry_id:170450)力

- **谐振子势 ($n=2$)**: 考虑一个粒子在简谐势 $U(x) = \frac{1}{2}kx^2$ 中运动。这是一个二次齐次势，即 $n=2$。根据[维里定理](@entry_id:146441)，我们有 $2\langle K \rangle = 2\langle U \rangle$，即 $\langle K \rangle = \langle U \rangle$。这表明，对于任何束缚在[谐振子势](@entry_id:750179)中的粒子，其平均动能恒等于其平均势能，这与我们从具体求解[运动方程](@entry_id:170720)得到的结果完全一致。

- **[引力](@entry_id:175476)与库仑力 ($n=-1$)**: 对于受[引力](@entry_id:175476)或[库仑力](@entry_id:174598)作用的系统，其势能形式为 $U(r) \propto 1/r = r^{-1}$。这是一个 $-1$ 次齐次势，即 $n=-1$。[维里定理](@entry_id:146441)预言 $2\langle K \rangle = -1 \langle U \rangle$。例如，在一个被限制在二维平面上的经典[电子气模型](@entry_id:189022)中，尽管粒子运动是二维的，但它们之间的库仑相互作用[势能](@entry_id:748988) $U(r) = C/r$ 仍然是 $-1$ 次齐次的。因此，该系统的平均动能与平均势能之比为 $\frac{\langle K \rangle}{\langle U \rangle} = -\frac{1}{2}$ [@problem_id:2011157]。这个关系是理解[自引力系统](@entry_id:155831)（如恒星、星系团）稳定性的基石。系统的总能量 $E = \langle K \rangle + \langle U \rangle = \frac{1}{2}\langle U \rangle = -\langle K \rangle$。由于束缚态要求总能量 $E \lt 0$，这意味着平均势能 $\langle U \rangle$ 必须为负，而平均动能 $\langle K \rangle$ 必须为正，这符合物理直觉。

#### 复合[势能](@entry_id:748988)

许多物理系统中的[势能](@entry_id:748988)并非单一的齐次函数，而是多个不同齐次次数的[势能](@entry_id:748988)项之和。由于求平均是线性运算，维里定理可以分别应用于每一个齐次部分。

考虑一个在一维[非谐势](@entry_id:141227) $U(x) = \frac{1}{2}kx^2 + \frac{1}{4}\lambda x^4$ 中运动的粒子。该势能可以分解为二次[谐振子](@entry_id:155622)项 $U_2(x) = \frac{1}{2}kx^2$（$n=2$）和四次非谐项 $U_4(x) = \frac{1}{4}\lambda x^4$（$n=4$）。对总[势能](@entry_id:748988)应用[维里定理](@entry_id:146441)得到：
$$
2\langle K \rangle = \left\langle x \frac{d(U_2+U_4)}{dx} \right\rangle = \left\langle x \frac{dU_2}{dx} \right\rangle + \left\langle x \frac{dU_4}{dx} \right\rangle
$$
根据[欧拉定理](@entry_id:138104)，$\left\langle x \frac{dU_2}{dx} \right\rangle = 2\langle U_2 \rangle$ 且 $\left\langle x \frac{dU_4}{dx} \right\rangle = 4\langle U_4 \rangle$。因此，我们得到：
$$
2\langle K \rangle = 2\langle U_2 \rangle + 4\langle U_4 \rangle \quad \implies \quad \langle K \rangle = \langle U_2 \rangle + 2\langle U_4 \rangle
$$
这个结果清晰地展示了平均动能如何由不同阶的势能贡献构成 [@problem_id:2011154]。

这个思想可以推广到更复杂的多体系统。例如，一个由 $N$ 个粒子组成的系统，粒子间存在伦纳德-琼斯 (Lennard-Jones) 相互作用，同时被一个外部[谐振子势](@entry_id:750179)场 $U_{\text{ext}} = \frac{1}{2} K \sum_i |\vec{r}_i|^2$ 束缚。[伦纳德-琼斯势](@entry_id:143105)本身包含一个排斥项 $U_{12} \propto r^{-12}$ ($n=-12$) 和一个吸引项 $U_6 \propto r^{-6}$ ($n=-6$)。外部谐振子势是二次齐次的 ($n=2$)。将维里定理应用于这个复合系统，我们得到：
$$
2\langle K \rangle = 2\langle U_{\text{ext}} \rangle - 6\langle U_6 \rangle - 12\langle U_{12} \rangle
$$
整理后可得 $\langle K \rangle - \langle U_{\text{ext}} \rangle + 3 \langle U_{6} \rangle + 6 \langle U_{12} \rangle = 0$。这个关系式为[分子动力学模拟](@entry_id:160737)提供了重要的检验标准，可以用来验证模拟过程是否达到了稳定的平衡态 [@problem_id:2011155]。

### [维里定理](@entry_id:146441)与物态方程

维里定理的一个重要应用是推导气体的物态方程。当气体被限制在容器中时，除了粒子间的相互作用力外，还存在器壁对粒子的[约束力](@entry_id:170052)。这些约束力通常不是保守力，不能从[势能函数](@entry_id:200753)导出，因此需要单独处理。

让我们回到维里定理的一般形式：$2\langle K \rangle + \langle \sum_{i} \vec{F}_i \cdot \vec{r}_i \rangle = 0$。这里的总力 $\vec{F}_i$ 可以分解为粒子间相互作用力 $\vec{F}_i^{\text{int}}$、外部场力 $\vec{F}_i^{\text{ext}}$ 以及器壁的约束力 $\vec{F}_i^{\text{wall}}$。维里项也相应地分解：
$$
\left\langle \sum_{i} \vec{F}_i \cdot \vec{r}_i \right\rangle = \left\langle \sum_{i} \vec{F}_i^{\text{int}} \cdot \vec{r}_i \right\rangle + \left\langle \sum_{i} \vec{F}_i^{\text{ext}} \cdot \vec{r}_i \right\rangle + \left\langle \sum_{i} \vec{F}_i^{\text{wall}} \cdot \vec{r}_i \right\rangle
$$
器壁项可以通过宏观压强 $P$ 来表达。器壁在面元 $d\vec{A}$ (方向指向容器外部) 对气体施加的力为 $-P d\vec{A}$。因此，器壁维里项可以写成对容器内表面 $\partial V$ 的积分：
$$
\left\langle \sum_{i} \vec{F}_i^{\text{wall}} \cdot \vec{r}_i \right\rangle = \oint_{\partial V} (\vec{r} \cdot (-P \hat{n})) dA = -P \oint_{\partial V} \vec{r} \cdot \hat{n} dA
$$
其中 $\hat{n}$ 是指向外部的[单位法向量](@entry_id:178851)。利用[高斯散度定理](@entry_id:188065)，$\oint_{\partial V} \vec{A} \cdot \hat{n} dA = \int_V (\nabla \cdot \vec{A}) dV$，对于矢量场 $\vec{r}$，其散度在三维空间中为 $\nabla \cdot \vec{r} = 3$。因此，积分结果为：
$$
-P \int_V (\nabla \cdot \vec{r}) dV = -P \int_V 3 dV = -3PV
$$
将此结果代入[维里定理](@entry_id:146441)，我们得到了包含压强的**维里[物态方程](@entry_id:194191)**：
$$
2\langle K \rangle + \left\langle \sum_{i} \vec{F}_i^{\text{int/ext}} \cdot \vec{r}_i \right\rangle - 3PV = 0
$$

- **理想气体**: 对于无相互作用的[理想气体](@entry_id:200096) ($U=0$)，[维里定理](@entry_id:146441)简化为 $2\langle K \rangle - 3PV = 0$。根据[统计力](@entry_id:194984)学中的[能量均分定理](@entry_id:136972)，在温度 $T$ 下，三维空间中 $N$ 个粒子的平均总动能为 $\langle K \rangle = \frac{3}{2}N k_B T$。代入后即得 $2(\frac{3}{2}N k_B T) - 3PV = 0$，这直接导出了著名的**理想气体[物态方程](@entry_id:194191)** $PV = N k_B T$。

- **有外场的非[理想气体](@entry_id:200096)**: 考虑一个被限制在体积为 $V$ 的球形容器中，且同时受到一个[中心势](@entry_id:148563)场 $U(r) = C/r^2$ 作用的无[相互作用气体](@entry_id:144962)。此[势能](@entry_id:748988)是 $-2$ 次齐次的 ($n=-2$)。此时，维里定理包含动能项、外场势能项和压强项：$2\langle K \rangle + \langle \sum_i \vec{r}_i \cdot \vec{F}_i^{\text{ext}} \rangle - 3PV = 0$。其中外场维里项为 $\langle \sum_i \vec{r}_i \cdot (-\nabla_i U_i) \rangle = -n \langle U \rangle = -(-2)\langle U \rangle = 2\langle U \rangle$。于是方程变为 $2\langle K \rangle + 2\langle U \rangle - 3PV = 0$。如果系统的总能量为 $E = \langle K \rangle + \langle U \rangle$，那么这个方程可以写作 $2(\langle K \rangle + \langle U \rangle) = 3PV$，即 $2E = 3PV$。因此，$\frac{PV}{E} = \frac{2}{3}$，这是一个不依赖于任何系统参数的普适常数 [@problem_id:2011144]。

- **一维系统中的压强**: 在一维盒子 $[-L, L]$ 中，器壁维里项变为 $-2PL$。如果气体粒子还受到一个外部[势场](@entry_id:143025) $U(x)=c|x|$ ($n=1$) 的作用，维里定理就写作 $2\langle K \rangle + \langle \sum_i x_i F_i^{\text{ext}} \rangle - 2PL = 0$。外场维里项为 $\langle \sum_i x_i F_i^{\text{ext}} \rangle = -n\langle U \rangle = -1 \cdot \langle U \rangle = -cN\langle|x|\rangle$。再结合[能量[均分定](@entry_id:136972)理](@entry_id:136972) $\langle K \rangle = N \frac{k_B T}{2}$，我们得到 $N k_B T - cN\langle|x|\rangle - 2PL = 0$。为了求出压强 $P$，我们需要利用玻尔兹曼分布计算在给定温度下 $\langle|x|\rangle$ 的具体值，这展示了[维里定理](@entry_id:146441)与[统计力](@entry_id:194984)学的协同作用 [@problem_id:2011145]。

### 扩展与高等专题

维里定理的威力远不止于此，它还可以推广到更广泛的物理情境中。

#### 非齐次势能

当势能函数不是齐次函数时，简洁的 $2\langle K \rangle = n \langle U \rangle$ 不再成立，但我们仍然可以使用其更普遍的形式 $2\langle K \rangle = \langle \sum_i \vec{r}_i \cdot \nabla_i U \rangle$。一个有趣的例子是用于检验某些修改[引力](@entry_id:175476)理论的汤川势 (Yukawa potential) $U(r) = - \frac{Gm^2}{r} \exp(-r/\lambda)$。该[势能](@entry_id:748988)由于指数项的存在而不再是齐次函数。对其应用维里算子，我们得到：
$$
\vec{r} \cdot \nabla U = r \frac{dU}{dr} = r \frac{d}{dr} \left( - \frac{Gm^2}{r} \exp(-r/\lambda) \right) = -U(r) \left( 1 + \frac{r}{\lambda} \right)
$$
对于一个稳定的束缚系统，[维里定理](@entry_id:146441)给出 $2\langle K \rangle = \langle -U(r) (1 + r/\lambda) \rangle$。特别地，对于一个稳定的圆形轨道，其中粒子间距 $r$ 恒为常数 $d$，该关系简化为 $2K = -U(d)(1+d/\lambda)$。这使得我们可以直接关联动能与[势能](@entry_id:748988)，进而分析系统的稳定性条件，例如总能量 $E = K+U$ 必须为负 [@problem_id:2011143]。

#### 相对论性[维里定理](@entry_id:146441)

维里定理的推导基于 $\vec{p} \cdot \vec{v} = 2K$ 这一关系，这在经典非[相对论力学](@entry_id:263483)中成立。对于[相对论性粒子](@entry_id:161314)，经典关系式 $\vec{p} \cdot \vec{v} = 2K$ 不再成立，我们需要重新审视 $\sum_i \vec{p}_i \cdot \vec{v}_i$ 这一项。在**超相对论极限**下 ($v \to c$)，粒子的能量-动量关系近似为 $E \approx pc$，动能 $K = E - mc^2 \approx pc$。此时，$\vec{p} \cdot \vec{v} = pv \approx pc \approx K$。
因此，对于超相对论性气体，维里函数的导数变为 $\frac{dG}{dt} \approx K + \sum \vec{F}_i \cdot \vec{r}_i$。相应的[维里定理](@entry_id:146441)变为 $\langle K \rangle - 3PV = 0$（对于三维[理想气体](@entry_id:200096)）。结合超相对论气体的平均动能 $\langle K \rangle = 3Nk_BT$，我们得到 $PV = \frac{1}{3} E_{\text{kin, tot}}$。
这与非相对论情况下的 $PV = \frac{2}{3} E_{\text{kin, tot}}$ 形成鲜明对比。对于包含非相对论和超相对论粒子组分的混合气体，其总的[物态方程](@entry_id:194191) $PV = \gamma E_{\text{kin, tot}}$ 中的系数 $\gamma$ 将依赖于两种粒子数 $N_A$ 和 $N_B$ 的比例 [@problem_id:2011161]。

#### 维里定理与[热力学](@entry_id:141121)涨落

维里定理在[统计力](@entry_id:194984)学中还有一个深刻的应用，即它将宏观的[热力学](@entry_id:141121)响应函数（如热容）与微观量的涨落联系起来。在一个处于恒定温度 $T$ 的正则系综中，系统的热容 $C_V$ 与总能量 $E$ 的[方差](@entry_id:200758)（涨落的平方）相关：$\langle (\delta E)^2 \rangle = k_B T^2 C_V$，其中 $\delta X = X - \langle X \rangle$ 表示量 $X$ 的涨落。
对于一个[势能](@entry_id:748988)为 $n$ 次齐次函数的系统，我们有 $\mathcal{W} = \sum \vec{F}_i \cdot \vec{r}_i = -nU$。这意味着[势能](@entry_id:748988) $U$ 的涨落与维里 $\mathcal{W}$ 的涨落直接相关：$\delta U = -\frac{1}{n}\delta\mathcal{W}$。总能量的涨落为 $\delta E = \delta K + \delta U = \delta K - \frac{1}{n}\delta\mathcal{W}$。对其平方并取系综平均，可得：
$$
\langle (\delta E)^2 \rangle = \langle (\delta K)^2 \rangle + \frac{1}{n^2} \langle (\delta \mathcal{W})^2 \rangle - \frac{2}{n} \langle \delta K \delta \mathcal{W} \rangle
$$
这个公式将总能量的涨落（与[热容](@entry_id:137594)相关）分解为动能涨落、维里涨落以及它们之间的协[方差](@entry_id:200758)。它揭示了系统对热的响应是如何由其内部动力学量的波动行为所决定的，展示了[维里定理](@entry_id:146441)在连接微观动力学与宏观[热力学](@entry_id:141121)方面的深刻内涵 [@problem_id:2011142]。

综上所述，[维里定理](@entry_id:146441)从一个简单的力学恒等式出发，延伸至对天体、气体、凝聚态物质等各类物理系统性质的深刻洞察。它不仅是一个计算工具，更是一种揭示系统内在平衡与稳定机制的物理思想。