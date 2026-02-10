## 引言
在研究材料如何变形时，描述从初始形状到最终形状的变化是一项根本性挑战。一个单一的数学工具，即变形梯度[张量](@keyword=tensor|lang=zh-CN|style=Feynman)，能够捕捉整个运动过程，但它不便地混合了两种截然不同的效应：使材料产生应变的纯拉伸和不产生应变的刚性旋转。这种混合使得应力和储能的分析变得复杂。本文通过引入连续介质力学的一个基石概念——右[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman)——来解决这个问题。我们将首先深入探讨“原理与机制”部分，以理解其数学起源以及通过[主拉伸](@keyword=principal_stretches|lang=zh-CN|style=Feynman)所体现的物理意义。随后，“应用与跨学科联系”一章将展示该[张量](@keyword=tensor|lang=zh-CN|style=Feynman)如何为描述[材料行为](@keyword=material_behavior|lang=zh-CN|style=Feynman)提供根本基础，涵盖从[应力分析](@keyword=stress_analysis|lang=zh-CN|style=Feynman)到高级材料储能建模的各个方面。让我们从将旋转与拉伸分离开始。

## 原理与机制

想象一下，你拿一块方形橡胶片，将它拉伸成长方形，然后在桌子上旋转它。你将如何描述刚才的动作？你可以尝试描述橡胶片上每个点的最终位置相对于其起始位置的变化。这种完整的描述被一个我们称之为**变形梯度[张量](@keyword=tensor|lang=zh-CN|style=Feynman)**的数学对象所捕捉，用矩阵 $F$ 表示。这个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)包含了所有信息，但却是混杂的。它混合了纯拉伸部分（从正方形到长方形）和纯旋转部分（在桌子上转动它）。对于物理学家或工程师来说，这很不方便。旋转不会改变材料的内能或应力，而拉伸会。我们需要一种方法来清晰地分离这两种效应。

### [极分解](@keyword=a=up_decomposition|lang=zh-CN|style=Feynman)：分离旋转与拉伸

事实证明，数学中有一个非常优美的定理，即**极分解定理**，恰好能做到这一点。它告诉我们，任何变形，无论多么复杂，都可以被看作一个序列：首先是纯拉伸，然后是刚性旋转。在数学上，它指出我们可以唯一地将变形梯度 $F$ 写成一个乘积：

$$F = RU$$

这里，$R$ 是一个**[旋转张量](@keyword=rotation_tensor|lang=zh-CN|style=Feynman)**。它是一个[正交矩阵](@keyword=orthogonal_matrix|lang=zh-CN|style=Feynman)，除了将物体作为一个整体进行旋转外，不做任何其他事情，就像在墙上转动一幅画。它不改变物体内部的任何长度或角度。我们故事中真正的主角是 $U$，即**右[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman)**。这是一个对称、正定的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)，它包含了关于材料实际拉伸和剪切的所有信息——即那种使材料产生应变并储存能量的“纯变形”。它之所以被称为“右”[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman)，是因为它首先作用于处于其原始*参考*构型中的材料矢量。

### 解析[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman)：它到底是什么？

那么，如果我们只知道混合了信息的 $F$，如何找到这个神秘的 $U$ 呢？我们不能简单地将它剥离出来。诀窍是首先构建一个完全不受旋转部分 $R$ 影响的量。

让我们用 $F$ 的转置乘以 $F$ 本身，形成一个新的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)。这被称为**[右柯西-格林张量](@keyword=right_cauchy_green_tensor|lang=zh-CN|style=Feynman)**，$C$：

$$C = F^T F$$

为何选择这种特定组合？想象一下，对已经变形的物体再施加一个额外的旋转 $Q$。新的变形梯度变为 $QF$。新的 $C$ 会发生什么变化？它变成 $(QF)^T(QF) = F^TQ^TQF$。由于 $Q$ 是一个旋转， $Q^T Q$ 就是[单位矩阵](@keyword=identity_matrix|lang=zh-CN|style=Feynman) $I$。所以，新的 $C$ 与旧的完全相同！这意味着 $C$ 是一个完全独立于任何刚性旋转的变形度量。这种被称为**客观性**的性质是绝对关键的。它确保我们对应变的描述不依赖于观察者的方向，也正因如此，储存在材料中的[应变能](@keyword=strain_energy|lang=zh-CN|style=Feynman)被表示为 $C$ 或 $U$ 的函数 [@problem_id:2695201] [@problem_id:2695201]。

现在我们可以将 $C$ 与 $U$ 联系起来。如果我们将 $F=RU$ 代入 $C$ 的定义中，我们得到：

$$C = (RU)^T(RU) = U^TR^TRU = U^T U$$

由于[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman) $U$ 是对称的 ($U^T=U$)，这可以极好地简化为 $C=U^2$。

答案就在这里！右[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman) $U$ 正是[右柯西-格林张量](@keyword=right_cauchy_green_tensor|lang=zh-CN|style=Feynman) $C$ 的**唯一对称正定平方根** [@problem_id:2681769]。我们首先通过计算 $C = F^T F$ 来“纯化”变形以消除旋转信息，然后取其平方根来找到纯拉伸 $U$。这个过程为我们提供了一个唯一且具有物理意义的变形度量，这是现代固[体力](@keyword=body_forces|lang=zh-CN|style=Feynman)学的基石。

### 拉伸的几何学：[主拉伸](@keyword=principal_stretches|lang=zh-CN|style=Feynman)与主方向

说 $U$ 是一个矩阵是抽象的。它究竟*做*了什么？作为一个[对称张量](@keyword=symmetric_tensors|lang=zh-CN|style=Feynman)，$U$ 具有一个非常特殊的性质：它拥有一组相互正交的[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)。这些向量代表了未变形材料中的一些方向，在施加纯拉伸后（在旋转 $R$ 之前），这些方向的取向不会改变，只会被拉长或缩短。这些特殊的初始方向被称为**[主拉伸](@keyword=principal_stretches|lang=zh-CN|style=Feynman)方向**。

沿[主方向](@keyword=principal_directions|lang=zh-CN|style=Feynman)的[线元](@keyword=line_element|lang=zh-CN|style=Feynman)被拉伸的量由 $U$ 对应的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)给出。这些始终为正的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)被称为**[主拉伸](@keyword=principal_stretches|lang=zh-CN|style=Feynman)** [@problem_id:1509126]。如果一个[主拉伸](@keyword=principal_stretches|lang=zh-CN|style=Feynman) $\lambda$ 大于 1，材料在该方向上被拉伸。如果 $\lambda  1$，它被压缩。如果 $\lambda=1$，长度不变。

让我们具体说明一下。想象一根材料纤维，在未变形状态下，它恰好与[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman) $U$ 的一个主方向 $\boldsymbol{N}_1$ 完全对齐。这根特定纤维所经历的拉伸就是相应的[主拉伸](@keyword=principal_stretches|lang=zh-CN|style=Feynman) $\lambda_1$ [@problem_id:2658072]。任何其他未与主方向对齐的纤维，在 $U$ 的作用下，既会被拉伸又会被旋转。因此，[主拉伸](@keyword=principal_stretches|lang=zh-CN|style=Feynman)和[主方向](@keyword=principal_directions|lang=zh-CN|style=Feynman)为我们提供了看待变形最自然的方式：它们定义了一个“变形[椭球](@keyword=ellipsoid|lang=zh-CN|style=Feynman)”的轴，一个球形材料体就是被变换成这个[椭球](@keyword=ellipsoid|lang=zh-CN|style=Feynman)的。找到它们的过程涉及计算 $U$（通常通过找到 $C$ 的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)/[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)并对[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)取平方根），然后分析其谱特性 [@problem_id:1506255] [@problem_id:1539535]。

### 更深层次的视角：[奇异值分解](@keyword=singular_value_decomposition_(svd)|lang=zh-CN|style=Feynman)

在线性代数中，有一个更为基本的思想，即**[奇异值分解 (SVD)](@keyword=singular_value_decomposition_svd|lang=zh-CN|style=Feynman)**，它以惊人的清晰度阐明了整个图景。SVD 定理指出，*任何*矩阵 $F$ 都可以分解为：

$$F = W \Sigma V^T$$

这里，$W$ 和 $V$ 是[旋转矩阵](@keyword=rotation_matrix|lang=zh-CN|style=Feynman)，$\Sigma$ 是一个包含非负数（称为**[奇异值](@keyword=singular_values|lang=zh-CN|style=Feynman)**）的[对角矩阵](@keyword=diagonal_matrix|lang=zh-CN|style=Feynman)。用物理术语来说，这意味着任何[线性变换](@keyword=linear_algebra_transformations|lang=zh-CN|style=Feynman) $F$ 都可以看作一个序列：一次旋转 ($V^T$)，一次沿坐标轴的纯拉伸 ($\Sigma$)，然后是另一次旋转 ($W$)。

这与我们的极分解 $F = RU$ 有何关系？通过将 SVD 代入 $C=U^2$ 的定义，我们可以找到 $U$ 和 $R$ 以 SVD 分量表示的显式公式 [@problem_id:2695211]：

$$U = V \Sigma V^T$$

$$R = W V^T$$

这是一个优美的结果！它告诉我们，[主拉伸](@keyword=principal_stretches|lang=zh-CN|style=Feynman)（$U$ 的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)）正是变形梯度 $F$ 的奇异值。[主拉伸](@keyword=principal_stretches|lang=zh-CN|style=Feynman)方向（$U$ 的[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)）是[旋转矩阵](@keyword=rotation_matrix|lang=zh-CN|style=Feynman) $V$ 的列向量。SVD 提供了一个强大的计算和概念工具，可以直接从任何变形中提取纯拉伸和旋转。

### 拉伸的两面性：右与左

你可能已经注意到我们措辞的谨慎：*右*[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman)。这意味着必然存在一个*左*[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman)，确实如此。极分解也可以写成 $F=VR$，其中旋转 $R$ 相同，但一个新的[张量](@keyword=tensor|lang=zh-CN|style=Feynman) $V$，即**左[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman)**，出现在左边。

有什么区别呢？$U$ 描述的是在参考构型中测量的拉伸，而 $V$ 描述的是在最终变形构型中观察到的拉伸状态。它们代表了相同的物理拉伸，但从不同的视角来看。它们的关系简单而优雅：它们是彼此的旋转版本 [@problem_id:1509074]。

$$V = R U R^T$$

这意味着它们有相同的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)（[主拉伸](@keyword=principal_stretches|lang=zh-CN|style=Feynman)完全相同），但它们的主方向不同。如果 $\boldsymbol{n}_i$ 是 $U$ 在参考[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)中的一个主方向，那么 $V$ 在变形[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)中的相应主方向就是 $\boldsymbol{v}_i = R \boldsymbol{n}_i$。它就是原来的[主方向](@keyword=principal_directions|lang=zh-CN|style=Feynman)，只是被 $R$ 旋转了一下。

### 关于特殊情况的说明：当拉伸相等时

如果一个球体变形为一个[椭球体](@keyword=ellipsoid|lang=zh-CN|style=Feynman)——一个旋转椭球——其中两个方向的拉伸相等，会发生什么？假设 $\lambda_1 = \lambda_2 \neq \lambda_3$。这代表了一种**轴对称拉伸**状态。

在这种情况下，由主方向 $\boldsymbol{N}_1$ 和 $\boldsymbol{N}_2$ 定义的平面内的任何方向都以相同的量 $\lambda_1$ 被拉伸。因此，在这个平面内不再存在唯一的一对[主方向](@keyword=principal_directions|lang=zh-CN|style=Feynman)。该平面内的任何一对[正交向量](@keyword=orthogonal_vectors|lang=zh-CN|style=Feynman)都可以同样胜任。这被称为简并特征空间。

重要的是要认识到，即使主*方向*不唯一，[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman) $U$ 本身仍然是完全且唯一定义的 [@problem_id:2639574]。数学框架是稳健的。这种简并性具有有趣的物理后果；例如，在[各向同性材料](@keyword=isotropic_materials|lang=zh-CN|style=Feynman)中，它意味着该平面内的主应力方向也不唯一 [@problem_id:2639574]。

总之，右[拉伸张量](@keyword=stretch_tensor|lang=zh-CN|style=Feynman) $U$ 是一个深刻的概念。它是我们将纯变形从刚性旋转的混淆效应中分离出来的数学工具。通过其[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)和[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)，它为我们提供了一个清晰的物理图像，展示了材料如何沿其主轴被拉伸和剪切，从而构成了现代大变形材料行为科学的根本基础。