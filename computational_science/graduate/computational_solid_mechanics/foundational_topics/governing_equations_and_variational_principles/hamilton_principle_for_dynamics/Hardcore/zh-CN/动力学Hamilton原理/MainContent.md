## 引言
在动力学研究中，牛顿定律通过力和动量为我们描述运动提供了基础。然而，存在一个基于变分法的、更为深刻和优雅的替代理论框架，即哈密顿原理。该原理的核心思想是，一个力学系统的运动轨迹总是沿着某条能使一个称为“作用量”的标量取驻值（通常是最小值）的路径展开。

尽管牛顿定律对于分析简单质点系统直观有效，但在面对具有复杂约束的多体系统或连续介质时，其基于矢量力平衡的方法会变得异常繁琐。哈密顿原理通过一个统一的标量能量框架，为推导复杂系统的运动方程提供了一种系统性的、强大的方法，从而填补了这一空白。

本文将引导读者全面掌握哈密顿原理。在第一章“原理与机制”中，我们将深入其理论核心，学习如何利用变分法从拉格朗日量推导出运动方程。接下来的第二章“应用与交叉学科联系”将展示该原理如何被广泛应用于先进工程、计算科学乃至现代物理等多个领域。最后，在第三章“动手实践”中，你将通过具体的计算练习，将理论知识转化为解决实际问题的能力。

让我们首先进入第一章，揭示哈密顿原理背后的基本原则与力学机制。

## 原理与机制

在动力学研究中，牛顿定律以力和动量为基础，为描述运动提供了基本框架。然而，还存在一个植根于变分法的、更为深刻和优雅的替代理论。这种方法被称为哈密顿原理，它断言一个力学系统的运动总是沿着一条能使一个称为**作用量**的标量取驻值的路径展开。本章将阐明这种变分方法的原理和机制，展示它如何作为一个强大而统一的工具，用于推导包括可变形固体在内的复杂系统的运动方程。

### 作用量定常原理与拉格朗日量

该变分框架的核心是**作用量**，用 $S$ 表示。它是一个泛函，将系统在时间区间 $[t_0, t_1]$ 上的整个轨迹映射为一个标量值。作用量定义为**拉格朗日量** $L$ 的时间积分：

$S[\mathbf{x}] = \int_{t_0}^{t_1} L(\mathbf{x}, \dot{\mathbf{x}}, t) \, dt$

在这里，$\mathbf{x}(t)$ 表示系统的广义坐标，$\dot{\mathbf{x}}(t)$ 表示相应的广义速度。对于大多数力学系统，拉格朗日量定义为系统总动能 $T$ 与总势能 $\Pi$ 之差。

$L = T - \Pi$

**哈密顿原理**，或称作用量定常原理，指出在一个系统所有可能连接固定初始构型 $\mathbf{x}(t_0)$ 和固定最终构型 $\mathbf{x}(t_1)$ 的路径中，系统实际采取的路径是使作用量 $S$ 取驻值的那一条。数学上，这意味着对于任何在时间端点处为零的容许虚位移 $\boldsymbol{\eta}(t)$，作用量的一阶变分 $\delta S$ 为零：

$\delta S = 0 \quad \text{对于所有满足 } \boldsymbol{\eta}(t_0) = \boldsymbol{\eta}(t_1) = \mathbf{0} \text{ 的容许 } \boldsymbol{\eta}(t)$

容许虚位移，通常称为**变分**，代表了对路径的一个无穷小的、运动学上可能的扰动。这些变分必须在起始和结束时刻为零的条件是哈密顿原理标准表述的基础，我们稍后将详细探讨这一点。

该原理为推导系统控制方程提供了一个强有力的方案：构建拉格朗日量，计算作用量的变分，并强制其驻定。其结果便是系统的运动方程，这些方程不是源于力的矢量平衡，而是源于一个标量最小化原理。

### 连续介质动力学中的拉格朗日表述

将哈密顿原理应用于连续可变形体，需要将其动能和势能表示为物体域上的积分。这里出现了一个关键的选择：这些积分应该在当前的变形构型 ($\Omega_t$) 上计算，还是在初始的参考构型 ($\Omega_0$) 上计算？这个选择区分了**欧拉（空间）描述**与**拉格朗日（物质）描述**。

对于固体力学，变分公式压倒性地偏好使用拉格朗日描述。主要原因是参考构型 $\Omega_0$ 是固定且已知的，而当前构型 $\Omega_t$ 本身是未知解的一部分。在一个其定义域也在变化的积分上进行变分会引入显著的数学复杂性（与雷诺输运定理相关），而通过在固定的参考域上工作，这些复杂性可以完全避免。

让我们在物质描述中构建可变形体的拉格朗日量。运动由一个映射 $\mathbf{x}(\mathbf{X}, t)$ 描述，它给出物质点 $\mathbf{X} \in \Omega_0$ 在时间 $t$ 的当前位置 $\mathbf{x}$。

**动能 ($T$)**

动能是动能密度在物体质量上的积分。在拉格朗日描述中，我们在固定的参考体积上进行积分：

$T = \int_{\Omega_0} \frac{1}{2} \rho_0(\mathbf{X}) |\dot{\mathbf{x}}(\mathbf{X}, t)|^2 \, dV$

这里，$\rho_0(\mathbf{X})$ 是参考构型中的质量密度，而 $\dot{\mathbf{x}} = \partial\mathbf{x}/\partial t$ 是物质速度。该公式优雅地避免了与时变积分域相关的复杂问题。

**势能 ($\Pi$)**

总势能 $\Pi$ 由内应变能 $U$ 和任何保守外力的势能 $V$ 组成。标准约定是 $\Pi = U - V_{\text{ext}}$，其中 $V_{\text{ext}}$ 是外力所做的功。

对于超弹性材料，**内应变能** $U$ 是储能密度函数 $W$ 在参考体积上的积分。$W$ 是材料变形的函数，变形由**变形梯度** $\mathbf{F} = \nabla_{\mathbf{X}} \mathbf{x}$ 度量。

$U = \int_{\Omega_0} W(\mathbf{F}) \, dV$

**外力势**考虑了由保守体积力和给定面力所做的功。一个可从标量势 $\phi(\mathbf{x}, t)$ 推导出的单位质量体积力 $\mathbf{b}(\mathbf{x}, t)$（即 $\mathbf{b} = -\nabla_{\mathbf{x}}\phi$），对势能 $\Pi$ 的贡献为 $-\int_{\Omega_0} \rho_0 \phi \, dV$。类似地，在边界部分 $\partial\Omega_0^t$ 上给定的名义面力 $\bar{\mathbf{t}}(\mathbf{X}, t)$ 可以与一个势能相关联，通常取为 $-\int_{\partial\Omega_0^t} \bar{\mathbf{t}} \cdot \mathbf{x} \, dA$。

综合这些，一个可变形体的完整拉格朗日量可能具有以下形式：

$L = T - \Pi = \underbrace{\int_{\Omega_0} \frac{1}{2}\rho_0 |\dot{\mathbf{x}}|^2 \,dV}_{\text{动能}} - \underbrace{\left( \int_{\Omega_0} W(\mathbf{F}) \,dV - \int_{\Omega_0} \rho_0 (\mathbf{b} \cdot \mathbf{x}) \,dV - \int_{\partial\Omega_0^t} \bar{\mathbf{t}} \cdot \mathbf{x} \,dA \right)}_{\text{势能项}}$
（为与后续推导一致，此处采用外力做功$W_{ext}$而非其势能$V_{ext}$，即$L = T - U + W_{ext}$）

必须注意，严格形式的哈密顿原理适用于保守系统，其中势能 $\Pi$ 仅是位置的函数。我们稍后讨论的拉格朗日-达朗贝尔原理将此框架扩展到非保守力。

### 变分法：推导运动方程

在确定了拉格朗日量之后，我们应用哈密顿原理，即 $\delta S = 0$。这涉及计算拉格朗日量中每一项的变分，我们记为 $\delta L = \delta T - \delta \Pi$，并在时间上积分。令虚位移为 $\boldsymbol{\eta}(\mathbf{X}, t) = \delta \mathbf{x}$。

**1. 动能项的变分**

动能泛函的变分是：

$\delta \int_{t_0}^{t_1} T \, dt = \int_{t_0}^{t_1} \int_{\Omega_0} \rho_0 \dot{\mathbf{x}} \cdot \delta\dot{\mathbf{x}} \, dV \, dt = \int_{t_0}^{t_1} \int_{\Omega_0} \rho_0 \dot{\mathbf{x}} \cdot \dot{\boldsymbol{\eta}} \, dV \, dt$

这是动力学进入公式的核心步骤。为了将时间导数从变分 $\dot{\boldsymbol{\eta}}$ 转移到路径变量 $\dot{\mathbf{x}}$，我们对时间进行分部积分：

$\int_{t_0}^{t_1} \left( \int_{\Omega_0} \rho_0 \dot{\mathbf{x}} \cdot \dot{\boldsymbol{\eta}} \, dV \right) dt = \left[ \int_{\Omega_0} \rho_0 \dot{\mathbf{x}} \cdot \boldsymbol{\eta} \, dV \right]_{t_0}^{t_1} - \int_{t_0}^{t_1} \left( \int_{\Omega_0} \rho_0 \ddot{\mathbf{x}} \cdot \boldsymbol{\eta} \, dV \right) dt$

在边界处求值的项 $[\dots]_{t_0}^{t_1}$ 是一个**时间边界项**。哈密顿原理的标准表述比较具有*相同*起始和结束构型的路径。这意味着任何容许变分 $\boldsymbol{\eta}$ 都必须在时间端点处为零：$\boldsymbol{\eta}(\mathbf{X}, t_0) = \mathbf{0}$ 和 $\boldsymbol{\eta}(\mathbf{X}, t_1) = \mathbf{0}$。这个在时间上的本质（类狄利克雷）条件确保了时间边界项恒等于零。这是与静态问题的一个关键区别，静态问题是在单个瞬间表述的，因此没有动能，也无需考虑时间边界条件。

有了这个条件，动能对 $\delta S$ 的贡献简化为惯性力的虚功：

$\delta \int_{t_0}^{t_1} T \, dt = -\int_{t_0}^{t_1} \left( \int_{\Omega_0} \rho_0 \ddot{\mathbf{x}} \cdot \boldsymbol{\eta} \, dV \right) dt$

**2. 势能项的变分**

势能的变分 $-\delta \Pi$ 给出了由内部和外部保守力所做的虚功。让我们考虑内应变能 $U$：

$-\delta U = -\delta \int_{\Omega_0} W(\mathbf{F}) \, dV = -\int_{\Omega_0} \frac{\partial W}{\partial \mathbf{F}} : \delta \mathbf{F} \, dV$

**第一皮奥拉-基尔霍夫应力张量** $\mathbf{P}$ 定义为变形梯度的功共轭量，即 $\mathbf{P} = \partial W / \partial \mathbf{F}$。变形梯度的变分是 $\delta \mathbf{F} = \delta(\nabla_{\mathbf{X}}\mathbf{x}) = \nabla_{\mathbf{X}}(\delta\mathbf{x}) = \nabla_{\mathbf{X}}\boldsymbol{\eta}$。因此，其贡献为：

$-\delta U = -\int_{\Omega_0} \mathbf{P} : \nabla_{\mathbf{X}}\boldsymbol{\eta} \, dV$

这个表达式是**内虚功**的负值。对于有限元实现，这正是弱形式所需要的项。

**3. 组合弱形式与强形式**

组合各项变分并设 $\delta S=0$，得到运动方程的**弱形式**，也称为动力学的虚功原理。对于具有体积力 $\mathbf{b}$ 和给定面力 $\bar{\mathbf{t}}$ 的物体，在任意时刻 $t$ 的弱形式为：

$\int_{\Omega_0} \rho_0 \ddot{\mathbf{x}} \cdot \boldsymbol{\eta} \, dV + \int_{\Omega_0} \mathbf{P} : \nabla_{\mathbf{X}}\boldsymbol{\eta} \, dV = \int_{\Omega_0} \rho_0 \mathbf{b} \cdot \boldsymbol{\eta} \, dV + \int_{\partial\Omega_0^t} \bar{\mathbf{t}} \cdot \boldsymbol{\eta} \, dA$

为了导出**强形式**（即熟悉的偏微分方程），我们对内虚功项应用散度定理。使用乘积法则和散度定理，我们可以写出：

$\int_{\Omega_0} \mathbf{P} : \nabla_{\mathbf{X}}\boldsymbol{\eta} \, dV = \int_{\partial\Omega_0} (\mathbf{P}\mathbf{N}) \cdot \boldsymbol{\eta} \, dA - \int_{\Omega_0} (\text{Div}\mathbf{P}) \cdot \boldsymbol{\eta} \, dV$

其中 $\mathbf{N}$ 是参考边界 $\partial\Omega_0$ 上的单位外法向量，$\text{Div}$ 是关于物质坐标 $\mathbf{X}$ 的散度算子。将此代回总的变分表达式并重新整理各项可得：

$\int_{\Omega_0} (\text{Div}\mathbf{P} + \rho_0\mathbf{b} - \rho_0\ddot{\mathbf{x}}) \cdot \boldsymbol{\eta} \, dV + \int_{\partial\Omega_0^t} (\bar{\mathbf{t}} - \mathbf{P}\mathbf{N}) \cdot \boldsymbol{\eta} \, dA + \int_{\partial\Omega_0^u} (\mathbf{P}\mathbf{N}) \cdot (-\boldsymbol{\eta}) \, dA = 0$

这个方程必须对*所有*容许变分 $\boldsymbol{\eta}$ 成立。这正是空间边界条件变得至关重要的地方。

### 容许性：边界条件与函数空间

“容许”变分 $\boldsymbol{\eta}$ 的概念施加了特定的约束，这些约束是整个框架的核心。

- **本质（狄利克雷）边界条件：** 在位移被指定的边界部分，比如在 $\partial\Omega_0^u$ 上 $\mathbf{x} = \bar{\mathbf{x}}$，任何变分都必须保持这个条件。这迫使虚位移在该边界上为零：在 $\partial\Omega_0^u$ 上 $\boldsymbol{\eta} = \mathbf{0}$。因此，在 $\partial\Omega_0^u$ 上的边界积分自动消失。

- **自然（诺伊曼）边界条件：** 在位移未被指定的边界部分，例如面力边界 $\partial\Omega_0^t$，变分 $\boldsymbol{\eta}$ 是任意的。为了让全局变分方程对该边界上 $\boldsymbol{\eta}$ 的任何任意选择都成立，乘以它的项必须为零。这就产生了**自然边界条件**。在我们的例子中，我们得到在 $\partial\Omega_0^t$ 上 $\mathbf{P}\mathbf{N} = \bar{\mathbf{t}}$。项 $\mathbf{P}\mathbf{N}$ 代表了参考表面上的名义面力向量。

处理完边界积分后，变分法基本引理要求体积被积函数也必须为零，从而产生在材料内部的强形式运动方程：

$\text{Div}\mathbf{P} + \rho_0\mathbf{b} = \rho_0\ddot{\mathbf{x}} \quad \text{在 } \Omega_0 \text{ 内}$

从形式化的数学角度看，容许变分的空间必须具有足够的正则性，以使所有积分和导数都良定义。位移场 $u$ 及其变分 $\eta$ 必须属于一个函数空间，其中空间梯度（用于应变能）和时间导数（用于动能）存在。这导致了**博赫纳空间**（Bochner spaces）的使用，例如 $H^1([t_0,t_1]; H^1(\Omega_0)^d)$。该空间中的元素是时间和空间的函数，在时间和空间上都具有平方可积的一阶导数。容许变分空间 $V_\eta$ 则被精确定义为该函数空间中同时满足本质边界条件和时间边界条件的子集：

$V_\eta = \left\{ \boldsymbol{\eta} \in H^1([t_0,t_1]; H^1(\Omega_0)^d) \,:\, \boldsymbol{\eta} = \mathbf{0} \text{ on } \partial\Omega_0^u \times [t_0,t_1], \; \boldsymbol{\eta}(\cdot,t_0) = \mathbf{0}, \; \boldsymbol{\eta}(\cdot,t_1) = \mathbf{0} \right\}$

### 哈密顿原理的扩展与局限

虽然哈密顿原理功能强大，但其最纯粹的形式有特定的适用范围。理解其扩展和局限对于正确应用至关重要。

#### 与守恒律的关系

根据**诺特定理**，拉格朗日量的每一个连续对称性都对应一个守恒量。一个关键的对称性是时间平移不变性。如果拉格朗日量 $L$ 没有显式的时间依赖性（即 $\partial L / \partial t = 0$），那么相应的守恒量就是**雅可比积分**或哈密顿量，定义为 $E = \mathbf{p} \cdot \dot{\mathbf{q}} - L$，其中 $\mathbf{p} = \partial L / \partial \dot{\mathbf{q}}$ 是正则动量。

一个引人注目的例子是从旋转参考系观察的系统。拉格朗日量包括与速度相关的科里奥利项和与位置相关的离心项。即使有这些附加项，如果系统的物理属性（质量、刚度）和旋转速率是恒定的，拉格朗日量也没有显式的时间依赖性。由此产生的守恒量 $E$ 不是动能和势能的简单总和，而是一个考虑了离心势的修正能量。对于一个质量为 $m$、刚度为 $k$、转速为 $\Omega$ 的二自由度系统，这个守恒能量是 $E = \frac{1}{2}m|\dot{\mathbf{q}}|^2 + \frac{1}{2}(k - m\Omega^2)|\mathbf{q}|^2$。这展示了变分框架如何优雅地将对称性与基本守恒律联系起来。

#### 非保守力

哈密顿原理基于势能泛函 $\Pi$ 的存在。根据定义，非保守力（如摩擦或流体阻力）不能从此类势能导出。为了处理这些力，我们必须求助于更通用的**拉格朗日-达朗贝尔原理**。该原理指出，作用量的变分加上非保守力所做的虚功必须总和为零：

$\delta S + \int_{t_0}^{t_1} \delta W_{\text{nc}} \, dt = 0$

这里，$\delta W_{\text{nc}}$ 是非保守力的虚功，它被直接加到变分方程中。对于单位参考体积的非保守体积力 $\mathbf{f}_{\text{nc}}$，虚功是 $\delta W_{\text{nc}} = \int_{\Omega_0} \mathbf{f}_{\text{nc}} \cdot \boldsymbol{\eta} \, dV$。遵循相同的变分过程，这导致在最终的运动方程中出现一个附加项：

$\rho_0 \ddot{\mathbf{x}} - \text{Div}\mathbf{P} = \rho_0 \mathbf{b} + \mathbf{f}_{\text{nc}}$

这个扩展原理提供了一种系统的方法来包含标准作用量原理范围之外的力。

#### 非完整约束

一个更微妙的局限性出现在**非完整约束**中。这些是对系统速度的约束，且不能被积分为对位置的约束（例如，一个无滑滚动的轮子）。这样的约束可以写成 $\mathcal{A}(\mathbf{x})\dot{\mathbf{x}} = \mathbf{0}$。

通过简单地在拉格朗日量中添加一个拉格朗日乘子项 $\boldsymbol{\lambda}^\top (\mathcal{A}\dot{\mathbf{x}})$ 并应用哈密顿原理的幼稚尝试，会导致物理上不正确的运动方程（所谓的“空变动力学”，vakonomic dynamics）。标准的哈密顿原理在这里从根本上失效了，因为它所依据的容许变分类别与非完整约束的前提不相容。

正确的途径是再次使用拉格朗日-达朗贝尔原理，但对虚位移附加一个关键要求，即**切塔耶夫条件**。虚位移必须与瞬时约束一致，意味着它们必须满足 $\mathcal{A}(\mathbf{x})\boldsymbol{\eta} = \mathbf{0}$。这确保了用于强制执行该条件的约束力不做虚功。这个表述，即 $\delta S + \int \delta W_{\text{nc}} dt = 0$ 且 $\boldsymbol{\eta}$ 受切塔耶夫条件限制，能够导出物理上正确的非完整运动方程。这凸显了作为哈密顿原理基础的虚功原理，为处理各种力学系统提供了最稳健的基础。