## 引言
在现代[固体力学](@entry_id:164042)，尤其是[大变形](@entry_id:167243)和[非线性](@entry_id:637147)材料行为的研究中，一个核心挑战是如何在变形物体的不同构型——即初始的**参考构型**与变形后的**当前构型**——之间建立严谨的数学联系。物理定律（如动量守恒）通常在当前构型中以最自然的形式表达，而材料的[本构关系](@entry_id:186508)（如弹性）却根植于其未变形的状态。若无法在这两种描述之间精确地转换物理量，我们将无法建立一个自洽的理论体系。**推前 (push-forward)**与**[拉回](@entry_id:160816) (pull-back)** 算子正是为了解决这一根本问题而生的数学工具，它们是整个有限变形理论的基石。

本文将系统性地引导读者深入理解这些关键算子。
*   在**“原理与机制”**一章中，我们将从变形梯度出发，详细阐述向量、[协变向量](@entry_id:263917)和[高阶张量](@entry_id:200122)在推前与[拉回](@entry_id:160816)操作下的变换法则，并揭示其背后的几何与物理内涵，例如面积元的变换（[南森公式](@entry_id:195566)）和不同应力张量（柯西应力、PK1、PK2）之间的内在联系。
*   接下来，在**“应用与[交叉](@entry_id:147634)学科联系”**一章中，我们将展示这些理论工具如何在更广阔的领域中发挥作用，包括在[弹塑性](@entry_id:193198)[乘法分解](@entry_id:199514)、[不可压缩材料](@entry_id:159741)、[晶体塑性](@entry_id:141273)等复杂本构模型中的应用，以及它们如何将力学与[热传导](@entry_id:147831)等[多物理场](@entry_id:164478)问题联系起来，并构成[计算力学](@entry_id:174464)有限元方法的核心算法。
*   最后，在**“动手实践”**部分，读者将有机会通过一系列精心设计的计算练习，亲手实践变形梯度的计算、[应变张量](@entry_id:193332)的推导以及[非正交基](@entry_id:154908)下的[张量分析](@entry_id:161423)，从而将抽象的理论知识转化为扎实的解决问题的能力。

通过这三章的学习，读者将不仅掌握推前与[拉回](@entry_id:160816)操作的计算方法，更能深刻领会它们在统一描述变形、应力与材料响应中的核心地位。

## 原理与机制

在连续介质力学中，描述一个物体从其初始的、未变形的**参考构型 (reference configuration)** $\mathcal{B}_0$ 运动到一个变形后的**当前构型 (current configuration)** $\mathcal{B}_t$ 是研究的核心。连接这两个构型的数学工具是**推前 (push-forward)** 和**[拉回](@entry_id:160816) (pull-back)** 算子。这些算子不仅是几何上的抽象概念，更是确保物理定律（如[动量守恒](@entry_id:149964)和[能量守恒](@entry_id:140514)）在不同构型描述下保持一致性的基石。本章将从第一性原理出发，系统阐述这些算子的定义、性质及其在有限变形理论中的关键应用。

### 变形梯度：运动的线性化

描述物体变形的数学函数是**运动映射 (motion map)** $\boldsymbol{\varphi}$，它将参考构型中的每一个物质点 $\mathbf{X}$ 映射到其在当前构型中的空间位置 $\mathbf{x}$，即 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$。这里的 $\mathbf{X}$ 称为**物质坐标 (material coordinates)**，而 $\mathbf{x}$ 称为**空间坐标 (spatial coordinates)**。

为了理解一个点邻域内的局部变形，我们考察运动映射的梯度。**变形梯度张量 (deformation gradient tensor)** $\mathbf{F}$ 定义为运动映射 $\mathbf{x}$ 对物质坐标 $\mathbf{X}$ 的梯度：

$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} = \nabla_{\mathbf{X}} \boldsymbol{\varphi}
$$

在分量形式下，其表达式为 $F_{iJ} = \frac{\partial x_i}{\partial X_J}$。变形梯度 $\mathbf{F}$ 是一个[二阶张量](@entry_id:199780)，它将参考构型中的[切空间](@entry_id:199137) $T_X\mathcal{B}_0$ 线性地映射到当前构型中的切空间 $T_x\mathcal{B}_t$。这个[线性映射](@entry_id:185132)是理解局部变形的关键：它将一个无穷小的物质线元 $d\mathbf{X}$ 变换为一个无穷小的空间[线元](@entry_id:196833) $d\mathbf{x}$：

$$
d\mathbf{x} = \mathbf{F} \, d\mathbf{X}
$$

这个操作被称为**向量的推前 (push-forward of a vector)**。它描述了嵌入在材料内部的微观纤维在变形过程中的拉伸和旋转。

让我们通过一个具体的例子来理解这些概念 [@problem_id:2677197]。考虑一个变形，其运动映射为 $\mathbf{x} = (x_1, x_2, x_3) = (X_1^2, X_2, X_3)$。变形梯度 $\mathbf{F}$ 可以通过计算其分量得到：

$$
\mathbf{F}(\mathbf{X}) = \begin{pmatrix} \frac{\partial x_1}{\partial X_1}  \frac{\partial x_1}{\partial X_2}  \frac{\partial x_1}{\partial X_3} \\ \frac{\partial x_2}{\partial X_1}  \frac{\partial x_2}{\partial X_2}  \frac{\partial x_2}{\partial X_3} \\ \frac{\partial x_3}{\partial X_1}  \frac{\partial x_3}{\partial X_2}  \frac{\partial x_3}{\partial X_3} \end{pmatrix} = \begin{pmatrix} 2X_1  0  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix}
$$

在物[质点](@entry_id:186768) $\mathbf{X}=(1,0,0)$ 处，变形梯度为 $\mathbf{F}(1,0,0) = \text{diag}(2, 1, 1)$。这是一个对角矩阵，其物理意义十分清晰：
*   **拉伸 (Stretch)**：对角元表示沿坐标轴方向的**主拉伸比 (principal stretches)**。$\lambda_1 = 2$ 意味着沿 $X_1$ 方向的线元被拉伸为原来的两倍。$\lambda_2 = 1$ 和 $\lambda_3 = 1$ 意味着沿 $X_2$ 和 $X_3$ 方向的线元长度保持不变。
*   **剪切 (Shear)**：非对角元均为零，表明在该点，初始时刻相互正交的坐标轴方向在变形后依然保持正交。
*   **体积变化 (Volume Change)**：变形梯度张量的[行列式](@entry_id:142978)，即**[雅可比行列式](@entry_id:137120) (Jacobian determinant)** $J = \det(\mathbf{F})$，描述了局部体积的变化率，$dv = J \, dV$。在此例中，$J(1,0,0) = \det(\text{diag}(2, 1, 1)) = 2$，说明该物质点周围的微元体积在变形后膨胀为原来的两倍。若 $J=1$，则变形是**等容的 (isochoric)**。

现在，我们可以将一个位于 $\mathbf{X}=(1,0,0)$ 的物质向量 $\mathbf{V} = (1, 2, 3)$ 推前到当前构型。其在当前构型中的像 $\mathbf{v}$ 通过 $\mathbf{v} = \mathbf{F} \mathbf{V}$ 计算得出：

$$
\mathbf{v} = \begin{pmatrix} 2  0  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \\ 3 \end{pmatrix} = \begin{pmatrix} 2 \\ 2 \\ 3 \end{pmatrix}
$$

这清晰地展示了向量的 $X_1$ 分量被拉伸为两倍，而其他分量保持不变，与 $\mathbf{F}$ 的几何意义完全一致 [@problem_id:2677197]。

### 标量场与[协变向量](@entry_id:263917)的[拉回](@entry_id:160816)

与向量（如速度）不同，一些物理量（如温度、密度）是[标量场](@entry_id:151443)。还有一些量，如[标量场的梯度](@entry_id:270765)，其变换规律与向量不同。当一个物理场自然地定义在当前构型上时，我们常常需要将其“[拉回](@entry_id:160816)”到参考构型上进行分析，这就是**[拉回](@entry_id:160816) (pull-back)** 操作。

对于一个定义在当前构型上的[标量场](@entry_id:151443) $f(\mathbf{x})$，其[拉回](@entry_id:160816)操作就是简单的[复合函数](@entry_id:147347)，即在参考构型上定义一个新的[标量场](@entry_id:151443) $g(\mathbf{X}) = (f \circ \boldsymbol{\varphi})(\mathbf{X}) = f(\boldsymbol{\varphi}(\mathbf{X}))$。

更有趣的情形是[标量场的梯度](@entry_id:270765)。设 $\mathbf{grad} f = \nabla_{\mathbf{x}} f$ 为 $f$ 在当前构型上的空间梯度。我们希望找到它在参考构型中对应的量，即 $g(\mathbf{X})$ 的物质梯度 $\mathbf{Grad} g = \nabla_{\mathbf{X}} g$。根据[链式法则](@entry_id:190743)，我们有：

$$
dg = (\nabla_{\mathbf{X}} g) \cdot d\mathbf{X}
$$

同时，我们也可以从空间构型出发：

$$
dg = df = (\nabla_{\mathbf{x}} f) \cdot d\mathbf{x} = (\nabla_{\mathbf{x}} f) \cdot (\mathbf{F} d\mathbf{X}) = (\mathbf{F}^{\mathsf{T}} \nabla_{\mathbf{x}} f) \cdot d\mathbf{X}
$$

比较以上两式，由于 $d\mathbf{X}$ 的任意性，我们得到空间梯度 $\nabla_{\mathbf{x}} f$ 的[拉回](@entry_id:160816)公式：

$$
\nabla_{\mathbf{X}} (f \circ \boldsymbol{\varphi}) = \mathbf{F}^{\mathsf{T}} (\nabla_{\mathbf{x}} f)
$$

这个关系表明，梯度的变换法则涉及到变形梯度的[转置](@entry_id:142115) $\mathbf{F}^{\mathsf{T}}$，这与向量的推前法则（使用 $\mathbf{F}$）截然不同。这种变换性质的向量被称为**[协变向量](@entry_id:263917) (covariant vectors)** 或**余向量 (covectors)**。

我们可通过一个实例来验证这个重要的关系 [@problem_id:2677218]。考虑变形 $\mathbf{x} = (X_1+X_2, X_2, X_3)$ 和空间[标量场](@entry_id:151443) $f(\mathbf{x}) = x_1 x_2$。
首先，直接计算[拉回](@entry_id:160816)后的场的梯度。[拉回](@entry_id:160816)场为 $g(\mathbf{X}) = f(\boldsymbol{\varphi}(\mathbf{X})) = (X_1+X_2)X_2 = X_1 X_2 + X_2^2$。其物质梯度为：

$$
\nabla_{\mathbf{X}} g = \left( \frac{\partial g}{\partial X_1}, \frac{\partial g}{\partial X_2}, \frac{\partial g}{\partial X_3} \right) = (X_2, X_1+2X_2, 0)
$$

其次，使用[拉回](@entry_id:160816)公式验证。空间梯度为 $\nabla_{\mathbf{x}} f = (x_2, x_1, 0)$。变形梯度为 $\mathbf{F} = \begin{pmatrix} 1  1  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix}$。
根据公式，$\nabla_{\mathbf{X}} g = \mathbf{F}^{\mathsf{T}} (\nabla_{\mathbf{x}} f \circ \boldsymbol{\varphi})$。将 $\nabla_{\mathbf{x}} f$ 用物质坐标表示：$\nabla_{\mathbf{x}} f \circ \boldsymbol{\varphi} = (X_2, X_1+X_2, 0)$。于是：

$$
\mathbf{F}^{\mathsf{T}} (\nabla_{\mathbf{x}} f \circ \boldsymbol{\varphi}) = \begin{pmatrix} 1  0  0 \\ 1  1  0 \\ 0  0  1 \end{pmatrix} \begin{pmatrix} X_2 \\ X_1+X_2 \\ 0 \end{pmatrix} = \begin{pmatrix} X_2 \\ X_1+2X_2 \\ 0 \end{pmatrix}
$$

两种方法得到的结果完全一致，证实了[协变向量](@entry_id:263917)的[拉回](@entry_id:160816)法则 [@problem_id:2677218]。

### 对偶性：[协变与逆变](@entry_id:189600)变换

前两节的例子揭示了一个深刻的几何事实：在变形过程中，不同类型的物理量遵循不同的变换规则。
*   **[逆变向量](@entry_id:272483) (Contravariant Vectors)**：如[切向量](@entry_id:265494) $d\mathbf{X}$，其推前变换使用 $\mathbf{F}$。
*   **[协变向量](@entry_id:263917) (Covariant Vectors)**：如梯度 $\nabla_{\mathbf{x}} f$，其[拉回](@entry_id:160816)变换使用 $\mathbf{F}^{\mathsf{T}}$。

这种差异的根源在于对偶性。[协变向量](@entry_id:263917)（或称1-形式）是作用于[逆变向量](@entry_id:272483)的线性泛函。它们的配对（即一个[协变向量](@entry_id:263917)作用于一个[逆变向量](@entry_id:272483)得到一个标量）在[坐标变换](@entry_id:172727)下必须保持不变。[拉回](@entry_id:160816)的定义正是为了确保这一点。对于空间[协变向量](@entry_id:263917) $\boldsymbol{\beta}$ 和物质[逆变向量](@entry_id:272483) $\mathbf{V}$，$\boldsymbol{\beta}$ 的[拉回](@entry_id:160816) $\boldsymbol{\alpha} = \boldsymbol{\varphi}^* \boldsymbol{\beta}$ 定义为：

$$
\langle \boldsymbol{\alpha}, \mathbf{V} \rangle = \langle \boldsymbol{\beta}, \mathbf{F} \mathbf{V} \rangle
$$

这里 $\langle \cdot, \cdot \rangle$ 表示配对运算。这个定义自然地导出了[协变向量](@entry_id:263917)的[拉回](@entry_id:160816)法则。反过来，如果想将一个物质[协变向量](@entry_id:263917) $\boldsymbol{\alpha}$ “推前”到空间构型，其自然的变换法则是使用 $\mathbf{F}^{-\mathsf{T}}$。也就是说，如果 $\boldsymbol{\beta}$ 是 $\boldsymbol{\alpha}$ 的推前，那么 $\boldsymbol{\beta} = \mathbf{F}^{-\mathsf{T}} \boldsymbol{\alpha}$。

从更抽象的微分几何角度看，映射 $\boldsymbol{\varphi}$ 自然地诱导了[切向量](@entry_id:265494)的“推前”和余切向量（[协变向量](@entry_id:263917)）的“[拉回](@entry_id:160816)”。不存在一个由 $\boldsymbol{\varphi}$ 直接诱导的、不依赖于度量（即[内积](@entry_id:158127)结构）的[协变向量](@entry_id:263917)的“正则”[推前映射](@entry_id:160933) [@problem_id:2677204]。然而，一旦我们在参考构型和当前构型中引入度量张量 $\mathbf{G}$ 和 $\mathbf{g}$，就可以通过所谓的**[音乐同构](@entry_id:199976) (musical isomorphisms)** 构造一个依赖于度量的[推前映射](@entry_id:160933)。这个过程分为三步：
1.  使用 $\mathbf{G}^\sharp$ 将物质[协变向量](@entry_id:263917) $\boldsymbol{\alpha}$ 提升 (sharp) 为物质[逆变向量](@entry_id:272483) $\mathbf{V}$。
2.  使用 $\mathbf{F}$ 将 $\mathbf{V}$ 推前为空间[逆变向量](@entry_id:272483) $\mathbf{v}$。
3.  使用 $\mathbf{g}^\flat$ 将空间[逆变向量](@entry_id:272483) $\mathbf{v}$ 降低 (flat) 为空间[协变向量](@entry_id:263917) $\boldsymbol{\beta}$。

整个过程可以写成[算子复合](@entry_id:268772)形式 $\boldsymbol{\beta} = (\mathbf{g}^\flat \circ T\boldsymbol{\varphi} \circ \mathbf{G}^\sharp)(\boldsymbol{\alpha})$，其分量形式为 $\beta_i = g_{ij} F^j{}_A G^{AB} \alpha_B$ [@problem_id:2677204]。这个构造虽然不“正则”，但在处理不同构型下的张量时非常有用。

### [高阶张量](@entry_id:200122)的变换

推前与[拉回](@entry_id:160816)的概念可以自然地推广到[高阶张量](@entry_id:200122)。变换法则遵循一个简单的原则：张量的每个[逆变](@entry_id:192290)指标（通常是上标）在推前时都乘以一个 $\mathbf{F}$，而每个[协变](@entry_id:634097)指标（通常是下标）都乘以一个 $\mathbf{F}^{-\mathsf{T}}$。

以一个在当前构型上定义的二阶[协变张量](@entry_id:634493) $\mathbf{b}$ (例如度量张量) 为例，其分量为 $b_{ij}$。它的[拉回](@entry_id:160816) $\mathbf{B} = \boldsymbol{\varphi}^* \mathbf{b}$ 是一个定义在参考构型上的二阶[协变张量](@entry_id:634493)，其定义要求对于任意两个物质向量 $\mathbf{U}$ 和 $\mathbf{V}$，满足[不变量](@entry_id:148850)关系：

$$
\mathbf{B}(\mathbf{U}, \mathbf{V}) = \mathbf{b}(\mathbf{F}\mathbf{U}, \mathbf{F}\mathbf{V})
$$

用分量表示，即 $B_{IJ} U^I V^J = b_{ij} (F^i{}_K U^K) (F^j{}_L V^L)$。整理后可得[拉回](@entry_id:160816)公式 [@problem_id:2677199]：

$$
B_{IJ} = F^i{}_I F^j{}_J b_{ij} \quad \text{或} \quad \mathbf{B} = \mathbf{F}^{\mathsf{T}} \mathbf{b} \mathbf{F}
$$

一个极其重要的应用是**右柯西-格林变形张量 (Right Cauchy-Green deformation tensor)** $\mathbf{C}$。它被定义为当前构型中的[欧几里得度量](@entry_id:147197)张量 $\mathbf{g}=\mathbf{I}$ （单位张量）的[拉回](@entry_id:160816)：

$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}} \mathbf{I} \mathbf{F} = \mathbf{F}^{\mathsf{T}} \mathbf{F}
$$

$\mathbf{C}$ 完全由参考构型中的量表示，它度量了物质点邻域的局部变形，是应变理论的基石。

相应地，一个物质二阶[协变张量](@entry_id:634493) $\mathbf{B}$ 的推前 $\mathbf{b} = \boldsymbol{\varphi}_* \mathbf{B}$ 可以通过对[拉回](@entry_id:160816)关系求逆得到 [@problem_id:2677199]：

$$
b_{ij} = (F^{-1})^I{}_i (F^{-1})^J{}_j B_{IJ} \quad \text{或} \quad \mathbf{b} = \mathbf{F}^{-\mathsf{T}} \mathbf{B} \mathbf{F}^{-1}
$$

### 几何应用：面积与体积元素的变换

推前与[拉回](@entry_id:160816)操作在描述几何元素（如体积和面积）的演化中扮演着核心角色。

如前所述，一个无穷小的体积元在变形中的变换关系由雅可比行列式决定：

$$
dv = J \, dV
$$

[面积元](@entry_id:263205)素的变换则更为复杂。一个[有向面积](@entry_id:169588)元可以由其法向量和大小共同描述，即 $\mathbf{N} \, dA$。其在当前构型中的像 $\mathbf{n} \, da$ 由著名的**[南森公式](@entry_id:195566) (Nanson's formula)** 给出：

$$
\mathbf{n} \, da = J \mathbf{F}^{-\mathsf{T}} \mathbf{N} \, dA
$$

这个公式可以通过考虑一个由两个物质[线元](@entry_id:196833) $d\mathbf{X}^{(1)}$ 和 $d\mathbf{X}^{(2)}$ 张成的微小[面积元](@entry_id:263205)来推导 [@problem_id:2677185]。物质面积向量为 $d\mathbf{A} = d\mathbf{X}^{(1)} \times d\mathbf{X}^{(2)}$。这两个[线元](@entry_id:196833)被推前到 $d\mathbf{x}^{(1)} = \mathbf{F} d\mathbf{X}^{(1)}$ 和 $d\mathbf{x}^{(2)} = \mathbf{F} d\mathbf{X}^{(2)}$。空间面积向量为 $d\mathbf{a} = d\mathbf{x}^{(1)} \times d\mathbf{x}^{(2)}$。利用[向量代数](@entry_id:152340)恒等式 $(\mathbf{F}\mathbf{u}) \times (\mathbf{F}\mathbf{v}) = (\det \mathbf{F}) (\mathbf{F}^{-1})^{\mathsf{T}} (\mathbf{u} \times \mathbf{v})$，我们直接得到 $d\mathbf{a} = J \mathbf{F}^{-\mathsf{T}} d\mathbf{A}$，这便是[南森公式](@entry_id:195566)。

例如，对于一个简单的[剪切变形](@entry_id:170920) $\mathbf{x} = (X_1+\gamma X_2, X_2, X_3)$，其变形梯度为 $\mathbf{F} = \begin{pmatrix} 1  \gamma  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix}$。这是一个[等容变形](@entry_id:196451)，因为 $J = \det(\mathbf{F}) = 1$。其逆的[转置](@entry_id:142115)为 $\mathbf{F}^{-\mathsf{T}} = \begin{pmatrix} 1  0  0 \\ -\gamma  1  0 \\ 0  0  1 \end{pmatrix}$。如果我们考察一个初始[法向量](@entry_id:264185)为 $\mathbf{N}=(0,1,0)$ 的物质平面，根据[南森公式](@entry_id:195566)，其变形后的[法向量](@entry_id:264185)（每单位参考面积）为 $J \mathbf{F}^{-\mathsf{T}} \mathbf{N} = 1 \cdot \mathbf{F}^{-\mathsf{T}} \mathbf{N} = (0,1,0)$。这表明，在简单剪切下，平行于剪切方向的平面，其法向和面积大小都保持不变 [@problem_id:2677217]。

### 物理应用：[应力张量](@entry_id:148973)与功率共轭

推前和[拉回](@entry_id:160816)操作在力学中的最重要应用之一，是建立不同构型下应力张量之间的关系。这一关系的核心是**功率[不变性原理](@entry_id:199405) (principle of power invariance)**，即内力在任何体积元上所做的功率不应依赖于我们选择的构型来描述它。

在当前构型中，单位体积的内[功率密度](@entry_id:194407)由**柯西应力 (Cauchy stress)** $\boldsymbol{\sigma}$ 和**变形率张量 (rate of deformation tensor)** $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}})$ 的[点积](@entry_id:149019)给出，其中 $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$ 是[空间速度梯度](@entry_id:187198)。[功率密度](@entry_id:194407)为 $\mathcal{P}_v = \boldsymbol{\sigma} : \mathbf{D}$。

将功率积分到整个体积，并转换到参考构型，我们得到总功率 $\int_v \boldsymbol{\sigma} : \mathbf{D} \, dv = \int_{V_0} (\boldsymbol{\sigma} : \mathbf{D}) J \, dV_0$。这启发我们定义与物质[运动学](@entry_id:173318)量率共轭的物质[应力张量](@entry_id:148973)。

**[第一皮奥拉-基尔霍夫应力](@entry_id:163971) (First Piola-Kirchhoff Stress, PK1)** $\mathbf{P}$ 定义为与变形梯度率 $\dot{\mathbf{F}}$ 共轭的应力，使得单位参考体积的[功率密度](@entry_id:194407)为 $\mathcal{P}_0 = \mathbf{P} : \dot{\mathbf{F}}$。通过功率等价，我们有 $\mathbf{P} : \dot{\mathbf{F}} = J (\boldsymbol{\sigma} : \mathbf{D})$。可以证明，这导出了 $\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 之间的关系，这是一个[拉回](@entry_id:160816)操作 [@problem_id:2677186]：

$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}}
$$

$\mathbf{P}$ 是一个非对称张量，它将参考构型中的力与当前构型中的面积联系起来，因此被称为“名义应力 (nominal stress)”。

**[第二皮奥拉-基尔霍夫应力](@entry_id:173163) (Second Piola-Kirchhoff Stress, PK2)** $\mathbf{S}$ 定义为与**[格林-拉格朗日应变](@entry_id:170427) (Green-Lagrange strain)** 的[物质时间导数](@entry_id:190892) $\dot{\mathbf{E}}$ 共轭的应力，其中 $\mathbf{E} = \frac{1}{2}(\mathbf{C}-\mathbf{I})$。[功率密度](@entry_id:194407)也可以写作 $\mathcal{P}_0 = \mathbf{S} : \dot{\mathbf{E}}$。这同样导出了 $\mathbf{S}$ 和 $\boldsymbol{\sigma}$ 的关系 [@problem_id:2677186]：

$$
\mathbf{S} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}} = \mathbf{F}^{-1} \mathbf{P}
$$

$\mathbf{S}$ 是一个对称张量，完全在参考构型中定义，它与材料本身的变形直接相关。

对于**[超弹性材料](@entry_id:190241) (hyperelastic materials)**，其[应变能密度函数](@entry_id:755490) $\Psi$ 通常是应变张量的函数，例如 $\Psi(\mathbf{C})$。通过变分原理，可以证明 $\mathbf{S}$ 是应变能对应变的导数，即 $\mathbf{S} = 2 \frac{\partial \Psi}{\partial \mathbf{C}}$。这再次确认了 $\mathbf{S}$ 和 $\mathbf{E}$ (或 $\mathbf{C}$) 之间深刻的能量共轭关系 [@problem_id:2677214]。

### 高等论题：[客观率](@entry_id:198692)与数学正则性

对于研究生层次的学习，理解推前与[拉回](@entry_id:160816)操作的两个高级方面至关重要：时间导数和数学基础。

**[客观率](@entry_id:198692) (Objective Rates)**
在建立流体或[弹塑性](@entry_id:193198)材料的空间[本构关系](@entry_id:186508)时，我们需要对[空间张量](@entry_id:185799)（如柯西应力）求时间导数。然而，简单的[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ 并不是**客观的 (objective)**，即它会随着观察者[参考系](@entry_id:169232)的刚体旋转而改变。一个客观的时间导数，记为 $\boldsymbol{\sigma}^{\nabla}$，在刚体旋转下必须像张量本身一样变换，即 $\hat{\boldsymbol{\sigma}}^{\nabla} = \mathbf{Q} \boldsymbol{\sigma}^{\nabla} \mathbf{Q}^{\mathsf{T}}$。
解决这个问题的一种方法是思考：[客观率](@entry_id:198692)应该是[物质时间导数](@entry_id:190892)的空间对应物。例如，一个物质二阶[逆变张量](@entry_id:636697) $\mathbf{A}$ 的导数是 $\dot{\mathbf{A}}$。将其推前到当前构型，我们得到 $P(\dot{\mathbf{A}}) = \mathbf{F} \dot{\mathbf{A}} \mathbf{F}^{\mathsf{T}}$。通过运动学恒等式 $\dot{\mathbf{F}} = \mathbf{L}\mathbf{F}$，可以证明这个推前后的导数等于[空间张量](@entry_id:185799) $\mathbf{a} = \mathbf{F} \mathbf{A} \mathbf{F}^{\mathsf{T}}$ 的一个特定导数形式 [@problem_id:2677188]：
$$
\mathbf{F} \dot{\mathbf{A}} \mathbf{F}^{\mathsf{T}} = \dot{\mathbf{a}} - \mathbf{L}\mathbf{a} - \mathbf{a}\mathbf{L}^{\mathsf{T}}
$$
这个表达式被称为**[上随体导数](@entry_id:756365) (Upper-Convected Derivative)** 或更广义的**李导数 (Lie derivative)** $\mathcal{L}_{\mathbf{v}}\mathbf{a}$。可以严格证明它是客观的，因此是在空间构型中建立[本构方程](@entry_id:138559)的有效工具。

**数学正则性 (Mathematical Regularity)**
到目前为止，我们都假设运动映射 $\boldsymbol{\varphi}$ 是足够光滑的（例如，$C^1$ 或 $C^2$）。但在更高级的[数学分析](@entry_id:139664)中，尤其是在处理断裂或[相变](@entry_id:147324)等不连续现象时，需要考虑 $\boldsymbol{\varphi}$ 的正则性问题。这些操作的严格数学基础依赖于 $\boldsymbol{\varphi}$ 所属的函数空间 [@problem_id:2677187]。
*   为了使变形梯度 $\mathbf{F}$ 作为[弱导数](@entry_id:189356)存在，$\boldsymbol{\varphi}$ 至少需要在[索博列夫空间](@entry_id:141995) $W^{1,1}$ 中。
*   为了使体积和面积的变量代换公式成立（这是推前/[拉回](@entry_id:160816)的根基），通常需要更强的正则性，例如 $\boldsymbol{\varphi}$ 是**[利普希茨连续的](@entry_id:267396) (Lipschitz continuous)**，或者 $\boldsymbol{\varphi} \in W^{1,p}$ 且 $p>n$（在三维中 $p>3$）。这些条件保证了映射不会将零测集映射到正测集上，并且具有足够的连续性。
*   一个深刻的结果是，即使正则性较弱，例如 $\boldsymbol{\varphi} \in W^{1,n}$（三维中为 $W^{1,3}$），[雅可比行列式](@entry_id:137120) $J$ 仍然是可积的（$J \in L^1$），并且重要的皮奥拉恒等式 $\text{div}(\text{cof} \, \mathbf{F}) = 0$ 在[分布](@entry_id:182848)意义下仍然成立。这为在非光滑变形框架下建立弱形式的力学理论提供了可能 [@problem_id:2677187]。

总之，推前和[拉回](@entry_id:160816)操作是连接物质描述和空间描述的桥梁。它们不仅是定义各种运动学和动力学量的工具，其深刻的几何和物理内涵更是整个有限变形连续介质力学理论的基石。