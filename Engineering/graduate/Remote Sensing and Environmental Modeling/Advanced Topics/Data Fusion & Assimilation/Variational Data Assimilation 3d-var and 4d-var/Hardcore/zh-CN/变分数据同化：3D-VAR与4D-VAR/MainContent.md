## 引言
变分资料同化（Variational Data Assimilation）是现代地球系统科学，尤其是数值天气预报和[环境建模](@entry_id:1124562)领域的基石。它提供了一个数学上严谨的框架，用于将海量的、分布不均的观测数据与复杂的动力学模型进行融合，以[生成对](@entry_id:906691)地球系统状态的最佳估计。然而，如何在高维度的模型[状态空间](@entry_id:160914)中，最优地结合充满不确定性的观测信息和模型先验知识，始终是一个核心的科学挑战。[变分方法](@entry_id:163656)通过将这一挑战转化为一个大规模的优化问题，为我们提供了强大的解决方案。

本文旨在系统性地介绍变分资料同化的核心理论与实践。我们将从第一章 **“原理与机制”** 开始，深入探讨其贝叶斯统计基础，推导三维（3D-Var）和四维（4D-Var）[变分同化](@entry_id:756436)的代价函数，并详细解析伴随方法、增量方案等关键求解技术。随后，在第二章 **“应用与交叉学科联系”** 中，我们将展示这些理论在现实世界中的强大应用，从利用[卫星遥感](@entry_id:1131218)数据进行天气预报，到在[海洋学](@entry_id:149256)、生物医学等领域的扩展。最后，通过第三章 **“动手实践”** 中的练习，读者将有机会亲手实现并加深对核心概念的理解。让我们首先进入[变分同化](@entry_id:756436)的核心，探索其基本原理与数学机制。

## 原理与机制

本章旨在阐述变分资料同化的核心原理与关键机制。我们将从其统计学基础——[贝叶斯定理](@entry_id:897366)——出发，构建[三维变分](@entry_id:746164)（3D-Var）和四维变分（4D-Var）的数学框架。随后，我们将深入探讨求解这些复杂优化问题的实用方法，包括伴随方法、增量方案以及用于改善问题[适定性](@entry_id:148590)的[控制变量变换](@entry_id:747844)技术。

### 变分资料同化的贝叶斯基础

变分资料同化的核心目标，是在给定一组观测资料和关于系统状态的先验知识（即背景场）的情况下，寻找系统最可能的状态。这一问题在统计学上可以精确地表述为[后验概率](@entry_id:153467)最大化问题。[贝叶斯定理](@entry_id:897366)为我们提供了连接先验知识、观测信息和[后验概率](@entry_id:153467)的桥梁。

设 $\mathbf{x} \in \mathbb{R}^n$ 为我们希望估计的系统状态向量（例如，大气温度、湿度和风速的网格点值），$\mathbf{y} \in \mathbb{R}^m$ 为可用的观测向量（例如，卫星[辐射率](@entry_id:174256)或雷达[反射率](@entry_id:172768)）。[贝叶斯定理](@entry_id:897366)指出，给定观测 $\mathbf{y}$ 后状态 $\mathbf{x}$ 的后验[概率密度函数](@entry_id:140610)（PDF）$p(\mathbf{x}|\mathbf{y})$ 与[先验概率](@entry_id:275634) $p(\mathbf{x})$ 和[似然函数](@entry_id:921601) $p(\mathbf{y}|\mathbf{x})$ 的乘积成正比：

$p(\mathbf{x}|\mathbf{y}) \propto p(\mathbf{y}|\mathbf{x}) p(\mathbf{x})$

在资料同化中，我们做出如下假设：

1.  **[先验分布](@entry_id:141376) $p(\mathbf{x})$**：我们对真实状态的先验知识通常来自一个短时预报，称为**背景场 (background)**，记为 $\mathbf{x}_b$。我们假设真实状态 $\mathbf{x}$ 分布在 $\mathbf{x}_b$ 周围，其误差 $\boldsymbol{\epsilon}_b = \mathbf{x} - \mathbf{x}_b$ 服从均值为零的高斯分布，协方差矩阵为 $\mathbf{B}$。即 $\boldsymbol{\epsilon}_b \sim \mathcal{N}(\mathbf{0}, \mathbf{B})$。因此，$\mathbf{x}$ 的[先验分布](@entry_id:141376)为：
    $p(\mathbf{x}) \propto \exp\left(-\frac{1}{2}(\mathbf{x}-\mathbf{x}_b)^\top \mathbf{B}^{-1} (\mathbf{x}-\mathbf{x}_b)\right)$
    矩阵 $\mathbf{B}$ 称为**[背景误差协方差](@entry_id:1121308)矩阵**，它描述了我们对背景场不确定性的估计，包括误差的大小、空间相关性和变量间的平衡关系。

2.  **[似然函数](@entry_id:921601) $p(\mathbf{y}|\mathbf{x})$**：[似然函数](@entry_id:921601)描述了在给定一个假设的状态 $\mathbf{x}$ 时，观测到 $\mathbf{y}$ 的概率。观测过程本身也存在误差。我们假设观测误差 $\boldsymbol{\epsilon}_o$ 同样服从均值为零的高斯分布，[协方差矩阵](@entry_id:139155)为 $\mathbf{R}$，即 $\boldsymbol{\epsilon}_o \sim \mathcal{N}(\mathbf{0}, \mathbf{R})$。[观测算子](@entry_id:752875) $\mathcal{H}$ 将模式[状态空间](@entry_id:160914)中的变量 $\mathbf{x}$ 映射到观测空间。因此，观测模型为 $\mathbf{y} = \mathcal{H}(\mathbf{x}) + \boldsymbol{\epsilon}_o$。对于给定的 $\mathbf{x}$，观测与模式等效观测 $\mathcal{H}(\mathbf{x})$ 之间的差异（称为**新息 (innovation)** 或离差）等于观测误差。[似然函数](@entry_id:921601)因此为：
    $p(\mathbf{y}|\mathbf{x}) \propto \exp\left(-\frac{1}{2}(\mathbf{y}-\mathcal{H}(\mathbf{x}))^\top \mathbf{R}^{-1} (\mathbf{y}-\mathcal{H}(\mathbf{x}))\right)$
    矩阵 $\mathbf{R}$ 称为**观测误差协方差矩阵**，它量化了观测的不确定性。

假设背景误差和观测误差是[相互独立](@entry_id:273670)的，我们可以将先验和[似然](@entry_id:167119)的表达式相乘，得到后验概率分布 ：

$p(\mathbf{x}|\mathbf{y}) \propto \exp\left(-\frac{1}{2}\left[ (\mathbf{x}-\mathbf{x}_b)^\top \mathbf{B}^{-1} (\mathbf{x}-\mathbf{x}_b) + (\mathbf{y}-\mathcal{H}(\mathbf{x}))^\top \mathbf{R}^{-1} (\mathbf{y}-\mathcal{H}(\mathbf{x})) \right]\right)$

寻找最可能的后验状态 $\mathbf{x}$，即最大化 $p(\mathbf{x}|\mathbf{y})$，等价于最小化其负对数。由此，我们定义了变分资料同化的**代价函数 (cost function)** $J(\mathbf{x})$：

$J(\mathbf{x}) = \frac{1}{2}(\mathbf{x}-\mathbf{x}_b)^\top \mathbf{B}^{-1} (\mathbf{x}-\mathbf{x}_b) + \frac{1}{2}(\mathbf{y}-\mathcal{H}(\mathbf{x}))^\top \mathbf{R}^{-1} (\mathbf{y}-\mathcal{H}(\mathbf{x}))$

这个代价函数具有清晰的物理解释：它是一个二次惩罚项的加和。第一项 $J_b = \frac{1}{2}(\mathbf{x}-\mathbf{x}_b)^\top \mathbf{B}^{-1} (\mathbf{x}-\mathbf{x}_b)$ 惩罚分析场 $\mathbf{x}$ 与背景场 $\mathbf{x}_b$ 的偏离，第二项 $J_o = \frac{1}{2}(\mathbf{y}-\mathcal{H}(\mathbf{x}))^\top \mathbf{R}^{-1} (\mathbf{y}-\mathcal{H}(\mathbf{x}))$ 惩罚模式等效观测 $\mathcal{H}(\mathbf{x})$ 与实际观测 $\mathbf{y}$ 的偏离。$\mathbf{B}^{-1}$ 和 $\mathbf{R}^{-1}$ 作为权重矩阵，确保在不确定性较小（即方差较小）的方向上，偏离会受到更重的惩罚。最小化 $J(\mathbf{x})$ 的过程，本质上是在背景信息和观测信息之间寻求一个以其不确定性为权重的最佳平衡。得到的解 $\mathbf{x}_a = \arg\min_{\mathbf{x}} J(\mathbf{x})$ 称为**分析场 (analysis)**。

### [三维变分资料同化](@entry_id:746164) (3D-Var)

当所有观测都与单一时刻的状态相联系时，上述变分框架即为[三维变分资料同化](@entry_id:746164)（3D-Var）。在 3D-Var 中，时间维度没有被显式地处理，代价函数的定义完全基于单一分析时刻的背景和观测。

#### 3D-Var 的代价函数与解

假设[观测算子](@entry_id:752875)是线性的，即 $\mathcal{H}(\mathbf{x}) = \mathbf{H}\mathbf{x}$，其中 $\mathbf{H}$ 是一个矩阵。3D-Var 代价函数为 ：

$J(\mathbf{x}) = \frac{1}{2}(\mathbf{x}-\mathbf{x}_b)^\top \mathbf{B}^{-1} (\mathbf{x}-\mathbf{x}_b) + \frac{1}{2}(\mathbf{y}-\mathbf{H}\mathbf{x})^\top \mathbf{R}^{-1} (\mathbf{y}-\mathbf{H}\mathbf{x})$

这是一个关于 $\mathbf{x}$ 的二次函数。由于 $\mathbf{B}$ 和 $\mathbf{R}$ 都是[对称正定矩阵](@entry_id:136714)，它们的逆也存在且为对称正定。这保证了 $J(\mathbf{x})$ 的 Hessian 矩阵是正定的，从而 $J(\mathbf{x})$ 是一个严格[凸函数](@entry_id:143075)，存在唯一的最小值。我们可以通过令其梯度 $\nabla_{\mathbf{x}} J(\mathbf{x})$ 等于零来求得这个最小值，即分析场 $\mathbf{x}_a$：

$\nabla_{\mathbf{x}} J(\mathbf{x}) = \mathbf{B}^{-1}(\mathbf{x} - \mathbf{x}_b) + \mathbf{H}^\top \mathbf{R}^{-1}(\mathbf{H}\mathbf{x} - \mathbf{y}) = \mathbf{0}$

整理上式可得分析场 $\mathbf{x}_a$ 的解析解：

$\mathbf{x}_a = (\mathbf{B}^{-1} + \mathbf{H}^\top \mathbf{R}^{-1}\mathbf{H})^{-1}(\mathbf{B}^{-1}\mathbf{x}_b + \mathbf{H}^\top \mathbf{R}^{-1}\mathbf{y})$

这个形式被称为“原始”或[状态空间](@entry_id:160914)形式的解。通过一些矩阵[恒等变换](@entry_id:264671)，可以得到一个在计算上更具优势的等价形式，称为“对偶”或增量形式 ：

$\mathbf{x}_a = \mathbf{x}_b + \mathbf{B}\mathbf{H}^\top (\mathbf{H}\mathbf{B}\mathbf{H}^\top + \mathbf{R})^{-1} (\mathbf{y}-\mathbf{H}\mathbf{x}_b)$

在这个形式中，矩阵 $\mathbf{K} = \mathbf{B}\mathbf{H}^\top (\mathbf{H}\mathbf{B}\mathbf{H}^\top + \mathbf{R})^{-1}$ 被称为**[最优插值](@entry_id:752977)增益**或**[卡尔曼增益](@entry_id:145800)**。分析场 $\mathbf{x}_a$ 是通过在背景场 $\mathbf{x}_b$ 的基础上，加上一个由新息 $(\mathbf{y}-\mathbf{H}\mathbf{x}_b)$ 加权的增量得到的。

#### 与卡尔曼滤波的等价性

上述推导揭示了[变分方法](@entry_id:163656)与另一种重要的循序[数据同化方法](@entry_id:748186)——卡尔曼滤波（Kalman Filter）——之间的深刻联系。在线性-[高斯假设](@entry_id:170316)下，卡尔曼滤波的分析步骤给出的分析均值与 3D-Var 的解是完全相同的 。

这种等价性的根本原因在于，两种方法都旨在计算相同的后验概率分布。3D-Var 通过最小化代价函数来寻找[后验分布](@entry_id:145605)的**众数**（即概率最高点），即最大后验估计（MAP）。卡尔曼滤波则直接计算后验分布的**均值**，即最小[均方误差](@entry_id:175403)（MMSE）估计。对于高斯分布，其众数和均值是重合的。因此，当背景场和观测模型完全相同时，3D-Var 和卡尔曼滤波的分析步骤会得出完全相同的结果。这种等价性为两种看似不同的同化方法提供了统一的理论基础。

### [四维变分资料同化](@entry_id:1125270) (4D-Var)

与 3D-Var 不同，[四维变分资料同化](@entry_id:1125270)（4D-Var）显式地利用了时间维度上的信息。它的目标是寻找一个最优的**初始状态** $\mathbf{x}_0$，使得由该初始状态通过动力模式演化出的轨迹，能够最好地拟合在一段时间（称为**同化窗口**）内分布的所有观测。

#### 强约束 4D-Var

最常见的 4D-Var 形式是**强约束 (strong-constraint) 4D-Var**。其核心假设是，我们使用的数值预报模式是**完美**的，即模式本身不会产生误差。这意味着在同化窗口内的任何时刻 $t_k$ 的状态 $\mathbf{x}_k$ 都完全由初始状态 $\mathbf{x}_0$ 和模式动力算子 $\mathcal{M}_{0 \to k}$ 唯一确定：

$\mathbf{x}_k = \mathcal{M}_{0 \to k}(\mathbf{x}_0)$

这里的 $\mathcal{M}_{0 \to k}$ 是一个（通常为[非线性](@entry_id:637147)的）映射，它将初始状态 $\mathbf{x}_0$ 演化到时刻 $t_k$。这个完美的模式方程构成了优化的“强约束”。

在这种设定下，整个状态轨迹都由控制变量 $\mathbf{x}_0$ 决定。4D-Var 的代价函数是 3D-Var 的自然推广，它包括在初始时刻的背景项和在整个同化窗口内所有观测时刻的观测项之和 ：

$J(\mathbf{x}_0) = \frac{1}{2}(\mathbf{x}_0-\mathbf{x}_b)^\top \mathbf{B}^{-1} (\mathbf{x}_0-\mathbf{x}_b) + \frac{1}{2}\sum_{k=0}^{N}\left(\mathbf{y}_k-\mathcal{H}_k(\mathcal{M}_{0\rightarrow k}(\mathbf{x}_0))\right)^{\top}\mathbf{R}_k^{-1}\left(\mathbf{y}_k-\mathcal{H}_k(\mathcal{M}_{0\rightarrow k}(\mathbf{x}_0))\right)$

其中，$\mathbf{y}_k$ 和 $\mathbf{R}_k$ 是在时刻 $t_k$ 的观测及其误差协方差，$\mathcal{H}_k$ 是在时刻 $t_k$ 的[观测算子](@entry_id:752875)。通过最小化这个关于 $\mathbf{x}_0$ 的函数，4D-Var 能够在一个动态一致的框架下，综合利用分布在不同时间的观测信息。

4D-Var 与 3D-Var 的关系可以通过考察同化窗口和模式动力来理解 。如果所有观测都集中在单一时刻 $t_a$，或者模式动力在同化窗口内是平凡的（例如，状态不随时间变化，$\mathcal{M}_{0 \to k} = \mathbf{I}$），那么 4D-Var 代价函数的形式将退化为 3D-Var。反之，随着同化窗口 $T$ 的增长，模式动力 $\mathcal{M}$ 的作用愈发重要，4D-Var 相对于 3D-Var 的优势也愈发明显，因为它能够通过动力约束将不同时刻的观测信息关联起来。在线性模式和线性观测算子的特殊情况下，4D-Var 在代数上等价于一个在初始时刻进行的 3D-Var，但其观测向量和观测算子被增广以包含所有时刻的信息。

#### 弱约束 4D-Var

强约束 4D-Var 的“完美模式”假设在实际中往往难以满足。模式自身由于[参数化](@entry_id:265163)方案的缺陷、[离散化误差](@entry_id:147889)等原因，也会引入误差。**弱约束 (weak-constraint) 4D-Var** 放松了这一假设，它允许模式存在误差。

在弱约束框架中，模式方程变为：

$\mathbf{x}_{k+1} = \mathcal{M}_k(\mathbf{x}_k) + \mathbf{w}_k$

其中 $\mathbf{w}_k$ 是**模式误差**项，我们假设它服从均值为零的高斯分布 $\mathbf{w}_k \sim \mathcal{N}(\mathbf{0}, \mathbf{Q}_k)$，其中 $\mathbf{Q}_k$ 是**模式[误差协方差矩阵](@entry_id:749077)**。

在这种情况下，优化的控制变量不仅包括初始状态 $\mathbf{x}_0$，还包括整个同化窗口内的模式误差序列 $\{\mathbf{w}_k\}$。代价函数也相应地增加了一项，用于惩罚模式误差的大小 ：

$J(\mathbf{x}_0, \{\mathbf{w}_k\}) = \frac{1}{2}(\mathbf{x}_0 - \mathbf{x}_b)^\top \mathbf{B}^{-1}(\mathbf{x}_0 - \mathbf{x}_b) + \frac{1}{2}\sum_{k=0}^{N}\big(\mathbf{y}_k - \mathcal{H}_k(\mathbf{x}_k)\big)^\top \mathbf{R}_k^{-1}\big(\mathbf{y}_k - \mathcal{H}_k(\mathbf{x}_k)\big) + \frac{1}{2}\sum_{k=0}^{N-1} \mathbf{w}_k^\top \mathbf{Q}_k^{-1} \mathbf{w}_k$

此处的最小化是在约束条件 $\mathbf{x}_{k+1} = \mathcal{M}_k(\mathbf{x}_k) + \mathbf{w}_k$ 下进行的。$\mathbf{B}$, $\mathbf{R}_k$ 和 $\mathbf{Q}_k$ 这三个[协方差矩阵](@entry_id:139155)共同决定了分析结果：它们分别代表了我们对背景场、观测和动力模式的信任程度。一个大的 $\mathbf{Q}_k$ 意味着我们认为模式不可靠，分析将更倾向于拟合观测；一个小的 $\mathbf{Q}_k$ 则意味着我们相信模式是准确的，分析将更严格地遵循模式动力。

### 4D-Var 问题的求解

由于环境模式 $\mathcal{M}$ 和[观测算子](@entry_id:752875) $\mathcal{H}$ 通常是高度[非线性](@entry_id:637147)的，4D-Var 的代价函数 $J(\mathbf{x}_0)$ 不再是简单的二次函数。因此，我们无法像在线性 3D-Var 中那样直接求得解析解，而必须采用迭代的[数值优化](@entry_id:138060)算法，例如[拟牛顿法](@entry_id:138962)（如 [L-BFGS](@entry_id:167263)）或[共轭梯度法](@entry_id:143436)。这些算法的核心都需要计算代价函数相对于[控制变量](@entry_id:137239)（即 $\mathbf{x}_0$）的梯度。

#### 梯度与伴随方法

直接计算梯度 $\nabla_{\mathbf{x}_0} J(\mathbf{x}_0)$ 是一个巨大的挑战。根据[链式法则](@entry_id:190743)，梯度由背景项和观测项的梯度之和构成。背景项的梯度很简单，为 $\mathbf{B}^{-1}(\mathbf{x}_0 - \mathbf{x}_b)$。挑战在于观测项的梯度。对于时刻 $t_k$ 的一项，其梯度涉及到模式算子和观测算子的[雅可比矩阵](@entry_id:178326)（或称切线性算子）的链式作用 ：

$\nabla_{\mathbf{x}_0} J(\mathbf{x}_0) = \mathbf{B}^{-1}(\mathbf{x}_0 - \mathbf{x}_b) + \sum_{k=0}^{N} (\mathbf{M}'_{0,k}(\mathbf{x}_0))^{\top} (\mathbf{H}'_{k}(\mathbf{x}_k))^{\top} \mathbf{R}_{k}^{-1} (\mathcal{H}_{k}(\mathbf{x}_k) - \mathbf{y}_{k})$

其中 $\mathbf{M}'_{0,k}$ 和 $\mathbf{H}'_k$ 分别是 $\mathcal{M}_{0,k}$ 和 $\mathcal{H}_k$ 的**切[线性算子](@entry_id:149003)**（即[雅可比矩阵](@entry_id:178326)）。$(\cdot)^\top$ 表示算子的**伴随 (adjoint)**（在欧几里得空间中即为[矩阵转置](@entry_id:155858)）。

这个表达式揭示了计算梯度的关键：
1.  首先，进行一次从 $t_0$ 到 $t_N$ 的正向积分，得到模式轨迹 $\{\mathbf{x}_k\}$ 和与观测的离差 $(\mathcal{H}_k(\mathbf{x}_k) - \mathbf{y}_k)$。
2.  然后，将这些离差乘以 $\mathbf{R}_k^{-1}$，并通过[观测算子](@entry_id:752875)的伴随 $\mathbf{H}'_k^\top$ 作用，将信息从观测空间“拉回”到模式[状态空间](@entry_id:160914)。
3.  最后，这些在不同时刻 $t_k$ 的信息，通过模式的[伴随算子](@entry_id:140236) $\mathbf{M}'_{0,k}^\top$ 从 $t_k$ **反向**传播并累加到初始时刻 $t_0$。

这种利用**伴随模式 (adjoint model)** 从后向前积分来高效计算梯度的技术，是 4D-Var 的核心计算引擎。它避免了对每个初始状态分量分别进行扰动来计算梯度的巨大计算量，使得在高维[状态空间](@entry_id:160914)中进行优化成为可能。

#### 切线性假设

伴随方法的有效性依赖于切线性算子 $\mathbf{M}'$ 和 $\mathbf{H}'$ 能够很好地代表原始非[线性算子](@entry_id:149003) $\mathcal{M}$ 和 $\mathcal{H}$ 对小扰动的响应。这一前提被称为**切线性假设 (tangent linear hypothesis)** 。

数学上，一个算子 $\mathcal{H}$ 在 $\mathbf{x}$ 点可微，意味着对于一个足够小的扰动 $\delta\mathbf{x}$，其响应可以表示为：
$\mathcal{H}(\mathbf{x} + \delta\mathbf{x}) \approx \mathcal{H}(\mathbf{x}) + \mathbf{H}'(\mathbf{x})\delta\mathbf{x}$
其误差项（[非线性](@entry_id:637147)部分）消失的速度要快于扰动本身的大小，即 $o(\|\delta\mathbf{x}\|)$。

在实际操作中，我们需要验证所编写的切线性模式代码是否满足此假设。一个标准的测试方法是：
1.  选取一个基准状态 $\mathbf{x}$ 和一个随机扰动方向 $\delta\mathbf{x}$。
2.  用一个逐渐减小的[尺度因子](@entry_id:266678) $\alpha$（例如 $\alpha = 10^{-1}, 10^{-2}, \dots$）缩放扰动。
3.  计算比率 $C(\alpha) = \frac{\|\mathcal{H}(\mathbf{x} + \alpha\delta\mathbf{x}) - \mathcal{H}(\mathbf{x}) - \mathbf{H}'(\mathbf{x})(\alpha\delta\mathbf{x})\|}{\|\mathbf{H}'(\mathbf{x})(\alpha\delta\mathbf{x})\|}$。
4.  如果切线性假设成立，该比率 $C(\alpha)$ 应近似正比于 $\alpha$。在对数-对数[坐标图](@entry_id:156506)上，这表现为一条斜率为 1 的直线，直到 $\alpha$ 过小导致[数值舍入](@entry_id:173227)误差占主导地位。这个测试是确保 4D-Var 系统正确性的关键步骤。

#### 增量 4D-Var

尽管伴随方法提高了梯度计算的效率，但对于高分辨率的[非线性](@entry_id:637147)模式，在迭代的每一步都运行完整的[非线性](@entry_id:637147)模式及其伴随模式，计算成本仍然高得惊人。**增量 4D-Var (Incremental 4D-Var)** 是一种广泛采用的策略，用于解决这一问题 。

增量 4D-Var 将复杂的[非线性](@entry_id:637147)最小化问题分解为一系列更简单的二次最小化问题。它通过两个嵌套的循环来实现：**外循环 (outer loop)** 和 **内循环 (inner loop)**。

*   **外循环**：外[循环处理](@entry_id:1130736)问题的[非线性](@entry_id:637147)。在每一次外循环迭代中，首先使用当前最优的初始状态 $\mathbf{x}_0^{(i)}$ 运行一次高分辨率的[非线性](@entry_id:637147)模式，得到一个**参考轨迹**。然后，围绕这个参考轨迹对模式和[观测算子](@entry_id:752875)进行线性化，生成一个简化的二次代价函数。

*   **内循环**：内循环的目标是最小化这个二次代价函数。这个最小化是针对一个**增量** $\delta\mathbf{x}_0$ 进行的，而不是完整的状态。由于代价函数是二次的，可以使用[共轭梯度](@entry_id:145712)等高效算法求解。关键在于，内循环中使用的切线性及其伴随模式通常是在较低分辨率下运行的，这极大地降低了计算成本。

内循环收敛后，得到一个最优增量 $\delta\mathbf{x}_0^{(i)}$。然后返回外循环，用这个[增量更新](@entry_id:750602)状态：$\mathbf{x}_0^{(i+1)} = \mathbf{x}_0^{(i)} + \delta\mathbf{x}_0^{(i)}$。接着，开始下一次外循环迭代，即用新的状态 $\mathbf{x}_0^{(i+1)}$ 生成新的参考轨迹并重新线性化。这个过程不断重复，直到整个系统收敛。

同化窗口的长度 $T$ 对收敛性有显著影响。随着 $T$ 增长，模式动力累积的[非线性](@entry_id:637147)也越强，导致每次线性化的有效范围（或信任域）缩小。因此，通常需要更多的外循环迭代（即更多的重线性化）才能在更长的同化窗口上达到相同的收敛精度。

### 高级主题：[预处理](@entry_id:141204)与[控制变量变换](@entry_id:747844)

变分代价函数的最小化问题常常是**病态的 (ill-conditioned)**，这意味着其 Hessian [矩阵的条件数](@entry_id:150947)非常大。这主要是由背景误差协方差矩阵 $\mathbf{B}$ 引起的，因为它需要描述从局地到大尺度、不同变量间的复杂相关性。[病态问题](@entry_id:137067)会导致迭代[优化算法](@entry_id:147840)收敛非常缓慢，甚至失败。

为了解决这个问题，我们引入了**预处理 (preconditioning)** 技术，其中最核心的是**[控制变量变换](@entry_id:747844) (control variable transform)** 。其思想是，不再直接对状态增量 $\delta\mathbf{x} = \mathbf{x} - \mathbf{x}_b$ 进行优化，而是引入一个新的、行为良好的**控制变量** $\mathbf{v}$，它与状态增量通过一个[线性变换](@entry_id:149133) $\mathbf{U}$ 相关联：

$\delta\mathbf{x} = \mathbf{Uv}$

我们选择变换 $\mathbf{U}$ 使得[背景误差协方差](@entry_id:1121308)矩阵可以分解为 $\mathbf{B} = \mathbf{UU}^\top$。这样，如果假设[控制变量](@entry_id:137239) $\mathbf{v}$ 服从[标准正态分布](@entry_id:184509) $\mathcal{N}(\mathbf{0}, \mathbf{I})$，那么它所对应的状态增量 $\delta\mathbf{x}$ 的协方差正好是 $\text{Cov}(\delta\mathbf{x}) = \text{Cov}(\mathbf{Uv}) = \mathbf{U}\text{Cov}(\mathbf{v})\mathbf{U}^\top = \mathbf{UIU}^\top = \mathbf{B}$。

通过这个变换，代价函数的背景项 $J_b$ 变得异常简单：

$J_b = \frac{1}{2}(\mathbf{x}-\mathbf{x}_b)^\top \mathbf{B}^{-1} (\mathbf{x}-\mathbf{x}_b) = \frac{1}{2}(\mathbf{Uv})^\top (\mathbf{UU}^\top)^{-1} (\mathbf{Uv}) = \frac{1}{2}\mathbf{v}^\top\mathbf{v}$

整个代价函数在控制变量空间中表示为：

$J(\mathbf{v}) = \frac{1}{2} \mathbf{v}^{\top} \mathbf{v} + \frac{1}{2} \left(\mathbf{y} - \mathcal{H}(\mathbf{x}_b + \mathbf{Uv})\right)^{\top} \mathbf{R}^{-1} \left(\mathbf{y} - \mathcal{H}(\mathbf{x}_b + \mathbf{Uv})\right)$

这个新代价函数的 Hessian 矩阵为 $\mathcal{H}_v = \mathbf{I} + (\mathbf{HU})^\top\mathbf{R}^{-1}(\mathbf{HU})$（在线性情况下）。背景项的 Hessian 矩阵从病态的 $\mathbf{B}^{-1}$ 变成了完美的[单位矩阵](@entry_id:156724) $\mathbf{I}$。这极大地改善了整个问题的条件数，使得[优化算法](@entry_id:147840)能够更快、更稳定地收敛。

算子 $\mathbf{U}$ 的构造本身就是一个重要的研究领域。它通常被设计为一系列算子的组合，例如，一个用于引入空间相关的[平滑算子](@entry_id:636528)（如基于扩散方程的算子），以及一个用于在不同物理变量间建立平衡关系（如地转平衡）的算子。通过精心设计的[控制变量变换](@entry_id:747844)，我们不仅能提高优化的效率，还能将物理约束和合理的误差结构直接编码到同化系统中。