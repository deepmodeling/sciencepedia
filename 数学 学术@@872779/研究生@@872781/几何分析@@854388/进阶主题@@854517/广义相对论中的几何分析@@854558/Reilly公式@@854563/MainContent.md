## 引言
Reilly公式是现代几何分析的基石之一，它提供了一座连接[流形](@entry_id:153038)上函数分析与[流形](@entry_id:153038)自身（尤其是其边界）几何的强大桥梁。在探索[黎曼流形](@entry_id:261160)的深层结构时，一个核心问题是如何量化其内部几何（如曲率）与边界几何（如弯曲方式）之间的关系。Reilly公式正是通过一个优美的积分恒等式，为这一问题提供了精妙而深刻的解答，使得分析方法成为研究[几何刚性](@entry_id:189736)与稳定性的利器。

本文旨在对Reilly公式进行系统性的介绍与探索。读者将通过以下三个章节，从基本原理到前沿应用，逐步深入掌握这一核心工具：

在第一章“原理与机制”中，我们将从最基本的散度定理和边界几何（第二基本形式、平均曲率）出发，逐步构建推导Reilly公式所需的全套工具。通过对[微分算子](@entry_id:140145)在边界进行精细的切法向分解，我们将揭示公式的完整推导过程，并探讨其在不同正则性假设下的推广，如加权Reilly公式与p-Laplacian的变体。

在第二章“应用与跨学科联系”中，我们将见证Reilly公式的威力。我们将展示如何运用此公式推导经典的[几何不等式](@entry_id:749850)（如Heintze-Karcher不等式）、建立[拉普拉斯算子](@entry_id:146319)谱的下界估计，并进一步证明深刻的[几何刚性](@entry_id:189736)与稳定性定理，理解为何球面和半球面在许多几何问题中扮演着唯一的模型角色。

最后，在第三章“动手实践”中，我们将通过一系列精心设计的计算练习，将理论知识转化为实践能力。通过在欧氏空间、[双曲空间](@entry_id:268092)等具体几何背景下亲手验证该公式，读者将对其内在结构和应用技巧获得具体而坚实的理解。

## 原理与机制

本章旨在深入探讨Reilly公式背后的核心原理与推导机制。Reilly公式是一个强大的积分恒等式，它将[黎曼流形](@entry_id:261160)内部的曲率和函数的[二阶导数](@entry_id:144508)信息与[流形](@entry_id:153038)边界的[几何不变量](@entry_id:178611)联系起来。为了理解并推导该公式，我们首先需要建立一套分析和几何工具。本节将回顾这些基础概念，特别强调符号约定、边界几何以及微分算子在边界上的分解。

### 基础工具：散度定理与边界几何

在深入Reilly公式之前，我们必须对一些基础性的工具和定义达成共识。这包括在带边[流形上的[积](@entry_id:156150)分定理](@entry_id:183680)，以及描述边界如何嵌入到环境[流形](@entry_id:153038)中的几何量。

#### 符号约定与[格林恒等式](@entry_id:176369)

在[几何分析](@entry_id:157700)中，不同的文献可能采用不同的符号约定，尤其是在定义拉普拉斯算子（Laplacian）时。这些约定的差异会影响[格林恒等式](@entry_id:176369)（Green's identity）以及所有依赖于它的积分公式（包括 Reilly 公式）的具体形式。因此，建立一套清晰、自洽的约定至关重要。

设 $(M^n, g)$ 是一个紧致、可定向的 $n$ 维[黎曼流形](@entry_id:261160)，其边界 $\partial M$ 光滑。设 $\nabla$ 为 Levi-Civita 联络。对于光滑函数 $u \in C^\infty(M)$，其**梯度** $\operatorname{grad} u$（或记为 $\nabla u$）是一个向量场，通过度量 $g$ 定义为对任意向量场 $X$ 恒有 $g(\operatorname{grad} u, X) = du(X)$。对于向量场 $X$，其**散度** $\operatorname{div} X$ 定义为[协变导数](@entry_id:152476) $\nabla X$ 的迹，即 $\operatorname{div} X = \operatorname{tr}_g(\nabla X)$。

**[拉普拉斯-贝尔特拉米算子](@entry_id:267002)**（Laplace–Beltrami operator），简称[拉普拉斯算子](@entry_id:146319)，作用于函数 $u$ 上，通常有两种定义：
1.  **[几何分析](@entry_id:157700)约定**: $\Delta u = \operatorname{div}(\operatorname{grad} u)$。在这种约定下，$\Delta$ 是一个（半）负定算子（其[特征值](@entry_id:154894)为负或零）。例如，在欧氏空间 $\mathbb{R}^n$ 中，$\Delta u = \sum_{i=1}^n \frac{\partial^2 u}{\partial x_i^2}$。
2.  **[偏微分方程](@entry_id:141332)约定**: $\tilde{\Delta} u = -\operatorname{div}(\operatorname{grad} u)$。这种定义使得 $\tilde{\Delta}$ 成为一个（半）正定算子，与热传导方程中的算子形式一致。

本书将主要采用几何分析约定，即 $\Delta u = \operatorname{div}(\operatorname{grad} u)$。

这些定义的核心应用在于**[散度定理](@entry_id:143110)**（Divergence Theorem），它是[流形](@entry_id:153038)上[微积分基本定理](@entry_id:201377)的一种推广。若 $\nu$ 表示沿边界 $\partial M$ 的**向外**[单位法向量](@entry_id:178851)场，则对任意光滑向量场 $X$，[散度定理](@entry_id:143110)表明：
$$
\int_M (\operatorname{div} X) \, dV_g = \int_{\partial M} \langle X, \nu \rangle_g \, dA_g
$$
其中 $dV_g$ 和 $dA_g$ 分别是 $M$ 上的黎曼[体积元](@entry_id:267802)和 $\partial M$ 上的诱导面积元。

利用[散度定理](@entry_id:143110)，我们可以推导出**[格林第一恒等式](@entry_id:170345)**。考虑向量场 $X = v \operatorname{grad} u$，其中 $u, v \in C^\infty(M)$。首先计算其散度，根据散度的[乘积法则](@entry_id:158393) $\operatorname{div}(fY) = f \operatorname{div} Y + \langle \operatorname{grad} f, Y \rangle_g$，我们得到：
$$
\operatorname{div}(v \operatorname{grad} u) = v \operatorname{div}(\operatorname{grad} u) + \langle \operatorname{grad} v, \operatorname{grad} u \rangle_g = v \Delta u + \langle \operatorname{grad} u, \operatorname{grad} v \rangle_g
$$
将上式在[流形](@entry_id:153038) $M$ 上积分，并对左侧应用[散度定理](@entry_id:143110)：
$$
\int_M (v \Delta u + \langle \operatorname{grad} u, \operatorname{grad} v \rangle_g) \, dV_g = \int_M \operatorname{div}(v \operatorname{grad} u) \, dV_g = \int_{\partial M} \langle v \operatorname{grad} u, \nu \rangle_g \, dA_g
$$
边界上的[内积](@entry_id:158127)可以写为 $v \langle \operatorname{grad} u, \nu \rangle_g$。我们定义函数 $u$ 沿法向 $\nu$ 的**[法向导数](@entry_id:169511)**为 $\partial_\nu u = \langle \operatorname{grad} u, \nu \rangle_g$。于是，边界积分变为 $\int_{\partial M} v \, \partial_\nu u \, dA_g$。

整理后，我们得到**[格林第一恒等式](@entry_id:170345)**：
$$
\int_M \langle \operatorname{grad} u, \operatorname{grad} v \rangle_g \, dV_g = - \int_M v \Delta u \, dV_g + \int_{\partial M} v \, \partial_\nu u \, dA_g
$$
这个恒等式是后续所有积分公式的基石 [@problem_id:3036528]。值得注意的是，如果我们采用[偏微分方程](@entry_id:141332)约定 $\tilde{\Delta} = -\Delta$，那么恒等式中的 $\Delta u$ 项就会变号：
$$
\int_M \langle \operatorname{grad} u, \operatorname{grad} v \rangle_g \, dV_g = \int_M v \tilde{\Delta} u \, dV_g + \int_{\partial M} v \, \partial_\nu u \, dA_g
$$
由于函数 $u$ 和 $v$ 的对称性，我们也可以交换它们在公式中的角色，得到另一个等价的形式 [@problem_id:3036528]。理解这些约定的影响对于准确应用和转换文献中的公式至关重要 [@problem_id:3036533]。

#### 边界的几何

Reilly公式的边界项直接反映了边界 $\partial M$ 的弯曲方式。描述这种弯曲的核心工具是第二基本形式和平均曲率。

对于边界 $\partial M$ 上的任意[切向量](@entry_id:265494)场 $X, Y \in T(\partial M)$，我们可以将它们延拓到 $\partial M$ 的一个邻域。向量场 $\nabla_X Y$ 一般既有切向分量，也有法向分量。**高斯公式**（Gauss formula）描述了这种分解。同样，我们可以考察[法向量场](@entry_id:268853) $\nu$ 沿边界切向的变化，这由**外尔伽滕公式**（Weingarten formula）给出。

**形状算子**（shape operator），记为 $S$，是一个从 $T_p(\partial M)$ 到自身的[线性映射](@entry_id:185132)，定义为：
$$
S(X) = \nabla_X \nu
$$
这里 $X \in T(\partial M)$。$S(X)$ 描述了法向量 $\nu$ 沿着切方向 $X$ 的变化率。一个关键性质是 $S(X)$ 始终是 $\partial M$ 的切向量。这可以从 $\langle \nu, \nu \rangle = 1$ 推断出来：对任意切向量 $X$，我们有 $0 = X\langle \nu, \nu \rangle = 2 \langle \nabla_X \nu, \nu \rangle$，这表明 $\nabla_X \nu$ 与 $\nu$ 正交，因此它位于[切空间](@entry_id:199137)中。此外，可以证明[形状算子](@entry_id:264703) $S$ 是自伴的，即对任意 $X, Y \in T(\partial M)$，都有 $\langle S(X), Y \rangle = \langle X, S(Y) \rangle$ [@problem_id:3036530]。

与[形状算子](@entry_id:264703)密切相关的是**[第二基本形式](@entry_id:161454)**（second fundamental form），记为 $II$（或 $h$）。它是一个在 $T_p(\partial M)$ 上的[对称双线性形式](@entry_id:148281)，定义为：
$$
II(X, Y) = \langle S(X), Y \rangle = \langle \nabla_X \nu, Y \rangle
$$
[第二基本形式](@entry_id:161454)衡量了 $\partial M$ 在环境[流形](@entry_id:153038) $M$ 中的“弯曲”程度。例如，如果 $\partial M$ 是“凸”的（从内部看），比如[欧氏空间](@entry_id:138052)中的球面，其[第二基本形式](@entry_id:161454)（相对于向外[法向量](@entry_id:264185)）是正定的。

最后，**平均曲率**（mean curvature）$H$ 定义为[第二基本形式](@entry_id:161454)关于诱导度量的迹，等价于[形状算子](@entry_id:264703)的迹：
$$
H = \operatorname{tr}_{\partial M}(II) = \operatorname{tr}(S)
$$
若 $\{e_i\}_{i=1}^{n-1}$ 是 $T_p(\partial M)$ 的一个标准正交基，则 $H = \sum_{i=1}^{n-1} II(e_i, e_i)$。[平均曲率](@entry_id:162147)描述了边界在某点所有方向上弯曲程度的平均值。如果 $H=0$，则称该边界是**[极小超曲面](@entry_id:188002)**。

### 微分算子在边界上的分解

推导 Reilly 公式的关键步骤之一是将作用在函数 $f$ 上的环境[微分算子](@entry_id:140145)（如梯度 $\nabla f$、Hessian $\nabla^2 f$ 和拉普拉斯算子 $\Delta f$）在边界 $\partial M$ 上分解为切向部分和法向部分。

#### 梯度、切向梯度与[法向导数](@entry_id:169511)

在边界 $\partial M$ 的每一点 $p$，环境[流形](@entry_id:153038)的[切空间](@entry_id:199137) $T_p M$ 可以[正交分解](@entry_id:148020)为边界的切空间和法向空间：$T_p M = T_p(\partial M) \oplus \operatorname{span}\{\nu_p\}$。相应地，任意定义在 $M$ 上的函数 $f$ 的[梯度向量](@entry_id:141180) $\nabla f$ 也可以在边界上分解。

- **法向分量**: $\nabla f$ 沿法向 $\nu$ 的投影是 $(\langle \nabla f, \nu \rangle)\nu = (\partial_\nu f)\nu$。
- **切向分量**: $\nabla f$ 在 $T(\partial M)$ 上的投影定义为**切向梯度** $\nabla_{\partial} f$。

因此，我们有以下基本的分解公式 [@problem_id:3036518]：
$$
\nabla f = \nabla_{\partial} f + (\partial_\nu f)\nu
$$
切向梯度 $\nabla_{\partial} f$ 完全由 $f$ 在边界 $\partial M$ 上的限制 $f|_{\partial M}$ 决定。

#### Hessian 分解与切向拉普拉斯算子

函数的 **Hessian** $\nabla^2 f$ 是一个 $(0,2)$-张量，定义为 $\nabla^2 f(X, Y) = \langle \nabla_X (\nabla f), Y \rangle$。类似于梯度的分解，我们也可以将环境 Hessian 与边界上诱导的 Hessian $\nabla^2_{\partial} f$ 联系起来。利用高斯公式和外尔伽滕公式，可以推导出对任意[切向量](@entry_id:265494)场 $X, Y \in T(\partial M)$ 成立的 **Hessian 分解公式** [@problem_id:3036518]：
$$
\nabla^2 f(X, Y) = \nabla^2_{\partial} f(X, Y) + II(X, Y) \, \partial_\nu f
$$
这个公式非常重要，它揭示了环境空间中的[二阶导数](@entry_id:144508)如何包含了边界的 extrinsic curvature（由[第二基本形式](@entry_id:161454) $II$ 体现）。

利用此分解，我们可以进一步得到环境拉普拉斯算子 $\Delta f$ 和**切向[拉普拉斯算子](@entry_id:146319)** $\Delta_{\partial} f$ 之间的关系。切向拉普拉斯算子是边界[流形](@entry_id:153038) $(\partial M, g|_{\partial M})$ 自身的 Laplace-Beltrami 算子。在边界 $\partial M$ 的一点 $p$，选取一个[标准正交基](@entry_id:147779) $\{e_1, \dots, e_{n-1}, \nu\}$，其中 $\{e_i\}_{i=1}^{n-1}$ 是 $T_p(\partial M)$ 的基。那么，
$$
\Delta f = \operatorname{tr}_g(\nabla^2 f) = \sum_{i=1}^{n-1} \nabla^2 f(e_i, e_i) + \nabla^2 f(\nu, \nu)
$$
对切向部分求和，并使用 Hessian 分解公式：
$$
\sum_{i=1}^{n-1} \nabla^2 f(e_i, e_i) = \sum_{i=1}^{n-1} \left( \nabla^2_{\partial} f(e_i, e_i) + II(e_i, e_i) \, \partial_\nu f \right) = \Delta_{\partial} f + H \partial_\nu f
$$
因此，我们得到**[拉普拉斯算子](@entry_id:146319)分解公式** [@problem_id:3036518] [@problem_id:3036530]：
$$
\Delta f |_{\partial M} = \Delta_{\partial} f + H \partial_\nu f + \nabla^2 f(\nu, \nu)
$$
这个恒等式将 $\Delta f$ 在边界上的值分解为三个部分：切向拉普拉斯算子、与[平均曲率](@entry_id:162147)相关的[法向导数](@entry_id:169511)项，以及二阶[法向导数](@entry_id:169511)项 $\nabla^2 f(\nu, \nu)$。

### 经典 Reilly 公式

掌握了上述工具后，我们现在可以着手推导经典的 Reilly 公式。该公式源于一个深刻的[微分](@entry_id:158718)恒等式——**Bochner-Weitzenböck 公式**（或简称 Bochner 恒等式）。

#### 从 Bochner 恒等式到 Reilly 公式

对于黎曼流形上的任意[光滑函数](@entry_id:267124) $f$，Bochner 恒等式给出了梯度范数平方的[拉普拉斯算子](@entry_id:146319)的一种分解：
$$
\frac{1}{2}\Delta(|\nabla f|^2) = |\nabla^2 f|^2 + \operatorname{Ric}(\nabla f, \nabla f) + \langle \nabla(\Delta f), \nabla f \rangle
$$
其中 $|\nabla^2 f|^2$ 是 Hessian 张量的范数平方，$\operatorname{Ric}$ 是 Ricci [曲率张量](@entry_id:181383)。这个恒等式本身是黎曼几何中一个核心的计算工具。

Reilly 公式的推导始于对 Bochner 恒等式进行巧妙的重组和积分。我们感兴趣的项是 $(\Delta f)^2 - |\nabla^2 f|^2 - \operatorname{Ric}(\nabla f, \nabla f)$。利用 Bochner 恒等式和散度定理，我们可以将这个表达式的积分与一个散度项联系起来。首先，考虑向量场 $X_1 = (\Delta f)\nabla f$ 和 $X_2 = \frac{1}{2}\nabla(|\nabla f|^2)$。它们的散度分别为：
$$
\operatorname{div}(X_1) = \operatorname{div}((\Delta f)\nabla f) = (\Delta f)^2 + \langle \nabla(\Delta f), \nabla f \rangle
$$
$$
\operatorname{div}(X_2) = \operatorname{div}\left(\frac{1}{2}\nabla(|\nabla f|^2)\right) = \frac{1}{2}\Delta(|\nabla f|^2)
$$
将 Bochner 恒等式中的 $\langle \nabla(\Delta f), \nabla f \rangle$ 和 $\frac{1}{2}\Delta(|\nabla f|^2)$ 替换掉，我们得到一个关键的逐点恒等式：
$$
(\Delta f)^2 - |\nabla^2 f|^2 - \operatorname{Ric}(\nabla f, \nabla f) = \operatorname{div}(X_1) - \operatorname{div}(X_2) = \operatorname{div}\left( (\Delta f)\nabla f - \frac{1}{2}\nabla(|\nabla f|^2) \right)
$$
将这个恒等式在[流形](@entry_id:153038) $M$ 上积分，并对右侧应用散度定理，我们得到：
$$
\int_M \left( (\Delta f)^2 - |\nabla^2 f|^2 - \operatorname{Ric}(\nabla f, \nabla f) \right) dV_g = \int_{\partial M} \left\langle (\Delta f)\nabla f - \frac{1}{2}\nabla(|\\nabla f|^2), \nu \right\rangle dA_g
$$
边界上的被积函数可以展开为 $(\Delta f)\partial_\nu f - \frac{1}{2}\partial_\nu(|\\nabla f|^2)$。第二项可以进一步写作 $\langle \nabla_\nu(\nabla f), \nabla f \rangle = \langle \nabla^2 f(\nu, \cdot), \nabla f \rangle$。至此，我们已经将[体积分](@entry_id:171119)转化为了一个边界积分。

下一步是利用前一节的分解公式，将边界积分项用边界的[内蕴几何](@entry_id:158788)量和函数在边界上的迹来表示。经过一系列代数运算（涉及拉普拉斯分解、Hessian 分解等），最终得到**Reilly 公式** [@problem_id:3036519]：
$$
\int_M \left( (\Delta f)^2 - |\nabla^2 f|^2 - \operatorname{Ric}(\nabla f, \nabla f) \right) dV_g = \int_{\partial M} \mathcal{B}(f) \, dA_g
$$
其中，边界项 $\mathcal{B}(f)$ 有多种等价形式。一个直接的形式是：
$$
\mathcal{B}(f) = H (\partial_\nu f)^2 + II(\nabla_{\partial} f, \nabla_{\partial} f) + (\Delta_{\partial} f)\partial_\nu f - \langle \nabla_{\partial}(\partial_\nu f), \nabla_{\partial} f \rangle
$$
值得注意的是，边界 $\partial M$ 本身是一个无边的[紧致流形](@entry_id:158804)。因此，我们可以对其上的积分再次使用分部积分（即散度定理或[格林恒等式](@entry_id:176369)）[@problem_id:3036518]。例如，
$$
\int_{\partial M} (\Delta_{\partial} f)\partial_\nu f \, dA_g = - \int_{\partial M} \langle \nabla_{\partial} f, \nabla_{\partial}(\partial_\nu f) \rangle \, dA_g
$$
将此代入，边界项可以写成一个更紧凑的形式：
$$
\int_{\partial M} \mathcal{B}(f) \, dA_g = \int_{\partial M} \left( H (\partial_\nu f)^2 + II(\nabla_{\partial} f, \nabla_{\partial} f) - 2 \langle \nabla_{\partial} f, \nabla_{\partial}(\partial_\nu f) \rangle \right) dA_g
$$
这两种形式在文献中都很常见，它们通过边界上的[分部积分](@entry_id:136350)相互关联 [@problem_id:3036519]。

#### 特例：闭[流形](@entry_id:153038)与积分 Bochner 恒等式

当[流形](@entry_id:153038) $M$ 是一个**闭[流形](@entry_id:153038)**（即紧致且无边界，$\partial M = \emptyset$）时，Reilly 公式中的边界积分为零。此时公式简化为一个纯粹的[体积分](@entry_id:171119)恒等式 [@problem_id:3036529]：
$$
\int_M \left( (\Delta f)^2 - |\nabla^2 f|^2 - \operatorname{Ric}(\nabla f, \nabla f) \right) dV_g = 0
$$
这通常被称为**积分 Bochner 恒等式**。它可以重写为：
$$
\int_M (\Delta f)^2 \, dV_g = \int_M |\nabla^2 f|^2 \, dV_g + \int_M \operatorname{Ric}(\nabla f, \nabla f) \, dV_g
$$
这个恒等式在研究闭[流形](@entry_id:153038)的几何与拓扑中扮演着核心角色。例如，如果[流形](@entry_id:153038)的 Ricci 曲率非负（$\operatorname{Ric}(X, X) \ge 0$），则 $\int_M (\Delta f)^2 \ge \int_M |\nabla^2 f|^2$。结合著名的 Kato 不等式，这可以导出关于[调和形式](@entry_id:193378)和 Betti 数的深刻结论。

### 分析性质与推广

Reilly 公式不仅是一个几何恒等式，其严格建立和推广还依赖于深刻的分析性质。

#### [正则性条件](@entry_id:166962)

上述推导假设了函数 $f$、度量 $g$ 和边界 $\partial M$ 都是光滑的（$C^\infty$）。在这种经典框架下，所有算子和积分都是明确定义的 [@problem_id:3036526]。然而，在现代[偏微分方程理论](@entry_id:189232)中，我们常常处理索博列夫空间（Sobolev space）中的弱解。

为了使 Reilly 公式对[弱解](@entry_id:161732)成立，我们需要较低的正则性假设。一个典型的现代设定是：度量 $g$ 和边界 $\partial M$ 至少是 $C^{1,1}$ 正则的（即一阶导数是 Lipschitz 连续的），函数 $f$ 属于索博列夫空间 $H^2(M)$。
- 在此条件下，$f$ 的二阶[弱导数](@entry_id:189356)是平方可积的，因此[体积分](@entry_id:171119)中的 $(\Delta f)^2$ 和 $|\nabla^2 f|^2$ 均在 $L^1(M)$ 中，积分有意义。
- $C^{1,1}$ 的边界正则性保证了第二基本形式 $II$ 和[平均曲率](@entry_id:162147) $H$ [几乎处处](@entry_id:146631)有界（$L^\infty(\partial M)$） [@problem_id:3036527]。
- 索博列夫[迹定理](@entry_id:203967)（Sobolev trace theorems）保证了 $f$ 及其导数在边界上的迹的正则性。例如，若 $f \in H^2(M)$，则其边界迹 $f|_{\partial M} \in H^{3/2}(\partial M)$，[法向导数](@entry_id:169511) $\partial_\nu f \in H^{1/2}(\partial M)$。
- 边界项，如 $H(\partial_\nu f)^2$，由于 $H \in L^\infty$ 和 $\partial_\nu f \in H^{1/2} \subset L^2$，其积是可积的。而包含切向拉普拉斯算子 $\Delta_{\partial} f$ 的项则需要更精细的处理，通常被理解为 $H^{-1/2}(\partial M)$ 和 $H^{1/2}(\partial M)$ 之间的对偶作用 [@problem_id:3036526] [@problem_id:3036527]。

通过在光滑设定下证明公式，然后利用光滑函数在索博列夫空间中的稠密性进行逼近，可以在这些较弱的正则性假设下严格地建立 Reilly 公式 [@problem_id:3036526]。

#### 加权 Reilly 公式

Reilly 公式可以推广到带有一个**权重函数**（或称为[势函数](@entry_id:176105)）$V \in C^\infty(M)$ 的情形。这在[几何分析](@entry_id:157700)、概率论和数学物理中有广泛应用。考虑加权测度 $d\mu = e^{-V} dV_g$。相应的**漂移[拉普拉斯算子](@entry_id:146319)**（drift Laplacian）或**[加权拉普拉斯算子](@entry_id:634510)**定义为：
$$
\Delta_V f = \Delta f - \langle \nabla V, \nabla f \rangle = e^V \operatorname{div}(e^{-V} \nabla f)
$$
这个算子在加权测度 $d\mu$ 下是自伴的。与之对应的曲率量是**Bakry-Émery Ricci 张量**：
$$
\operatorname{Ric}_V = \operatorname{Ric} + \nabla^2 V
$$
遵循与经典情况类似的推导思路，可以得到**加权 Reilly 公式** [@problem_id:3036539]。其[体积分](@entry_id:171119)部分变为 $\int_M ( (\Delta_V f)^2 - |\nabla^2 f|^2 - \operatorname{Ric}_V(\nabla f, \nabla f) ) \, d\mu$。边界项也相应地被“加权”，例如，[平均曲率](@entry_id:162147) $H$ 被替换为**加权[平均曲率](@entry_id:162147)** $H_V = H - \partial_\nu V$。这个推广极大地扩展了 Reilly 公式的应用范围，使其能够处理具有特定几何结构的[测度空间](@entry_id:191702)。

#### 向非线性算子的推广：p-Laplacian

Reilly 公式的思想还可以进一步推广到[非线性](@entry_id:637147)[椭圆算子](@entry_id:181616)，尽管这带来了巨大的技术挑战。一个典型的例子是 **[p-拉普拉斯算子](@entry_id:196614)** $\Delta_p u = \operatorname{div}(|\nabla u|^{p-2} \nabla u)$，其中 $p > 1$。

推广的主要困难在于两点 [@problem_id:3036540]：
1.  **各向异性 (Anisotropy)**：当 $p \neq 2$ 时，$\Delta_p$ 是[拟线性](@entry_id:637689)的，其行为强烈依赖于梯度 $\nabla u$ 的方向。这意味着任何相关的恒等式都必须包含一个反映这种方向依赖性的张量结构，而不仅仅是标量权重。
2.  **退化性 (Degeneracy)**：在梯度为零的[临界点](@entry_id:144653) $\{x : |\nabla u(x)|=0\}$，算子会退化（若 $p>2$）或奇异（若 $1  p  2$）。