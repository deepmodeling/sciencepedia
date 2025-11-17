## 引言
切空间与切丛是现代[微分几何](@entry_id:145818)与几何分析的基石。在没有全局线性结构的弯曲[流形](@entry_id:153038)上，我们如何定义和运用微积分中的基本概念，如导数和速度？这个根本问题促使我们必须发展一套内在的、不依赖于[嵌入空间](@entry_id:637157)的[微分](@entry_id:158718)框架。本文旨在系统地解决这一挑战，为读者构建起从单一点的“[线性逼近](@entry_id:142309)”到整个[流形](@entry_id:153038)的“向量场”的完整理论图景。

我们将从第一章“原理与机制”开始，深入探讨在[流形](@entry_id:153038)上一点的切空间的两种等价定义——一种是几何直观的，基于穿过该点的曲线；另一种是代数的，基于作用在函数上的导子。随后，我们将展示如何将所有点的切[空间平滑](@entry_id:202768)地“粘合”成一个更大的[流形](@entry_id:153038)，即切丛。在第二章“应用与交叉学科联系”中，我们将看到这些抽象结构如何在[几何力学](@entry_id:169959)、[黎曼几何](@entry_id:160508)和动力系统等领域中发挥关键作用，将它们从纯粹的数学定义转变为强大的分析工具。最后，通过第三章“动手实践”中的具体计算问题，读者将有机会亲手应用这些理论，巩固对核心概念的理解。

## 原理与机制

本章旨在深入探讨光滑流形上微积分理论的基石——[切空间](@entry_id:199137)与[切丛](@entry_id:161294)。我们将从一个点的局部“[切向量](@entry_id:265494)”概念出发，逐步构建起整个[流形](@entry_id:153038)上的整体几何结构“切丛”。我们将阐明这些结构是如何从[流形](@entry_id:153038)的[光滑性](@entry_id:634843)中自然产生的，并展示它们在几何分析中的核心作用。

### 局部景象：一个点的[切空间](@entry_id:199137)

在欧氏空间 $\mathbb{R}^n$ 中，向量的概念是直观的：它是一个具有大小和方向的箭头，可以等同于一个点对。然而，在一般的弯曲[流形](@entry_id:153038) $M$ 上，点与点之间没有自然的减法运算，因此我们无法直接定义“位移向量”。为了在[流形](@entry_id:153038)上发展微积分，我们必须首先为“速度”或“[方向导数](@entry_id:189133)”这些概念建立一个严格的、内在的定义。这便是切空间 $T_pM$ 的任务，它是在点 $p$ 处[对流](@entry_id:141806)形 $M$ 的“[最佳线性逼近](@entry_id:164642)”。

#### [光滑图册](@entry_id:264754)的关键作用

[流形](@entry_id:153038)局部看起来像[欧氏空间](@entry_id:138052)，这一性质是通过**图卡**（charts）来数学化的。一个图卡 $(U, \varphi)$ 是一个[同胚](@entry_id:146933)映射，它将[流形](@entry_id:153038) $M$ 的一个开集 $U$ 映射到 $\mathbb{R}^n$ 的一个开集 $\varphi(U)$。为了在整个[流形](@entry_id:153038)上拥有一致的微积分结构，我们要求任意两个重叠的图卡 $(U, \varphi)$ 和 $(V, \psi)$ 都是**光滑相容**的。这意味着**转换映射**（transition map） $\psi \circ \varphi^{-1}$ 是一个从 $\varphi(U \cap V)$ 到 $\psi(U \cap V)$ 的光滑（$C^\infty$）映射。

这个[光滑性](@entry_id:634843)条件至关重要。它确保了“可微”这一概念在[流形](@entry_id:153038)上是良定义的，即不依赖于我们选择哪个[局部坐标系](@entry_id:751394)来观察。假设我们有一个函数 $f: M \to \mathbb{R}$，它在 $\varphi$ [坐标系](@entry_id:156346)下的表示为 $f \circ \varphi^{-1}$，在 $\psi$ [坐标系](@entry_id:156346)下的表示为 $f \circ \psi^{-1}$。这两个表示通过转换映射联系在一起：$f \circ \psi^{-1} = (f \circ \varphi^{-1}) \circ (\varphi \circ \psi^{-1})$。由于转换映射 $\psi \circ \varphi^{-1}$ 及其逆都是光滑的，根据多元微积分中的**链式法则**，一个函数表示的光滑性直接蕴含了另一个表示的光滑性。因此，我们可以一致地定义[流形上的光滑函数](@entry_id:267853)。[@problem_id:3034022]

更进一步，定义导数本身只需要转换映射是可微的（即 $C^1$ 相容）。只要转换映射在点 $\varphi(p)$ 处可微，其导数（即[雅可比矩阵](@entry_id:264467)）就是一个[线性同构](@entry_id:270529)，这足以通过链式法则将一个[坐标系](@entry_id:156346)中计算出的导数线性地变换到另一个[坐标系](@entry_id:156346)中。因此，在点 $p$ 处计算导数这一行为，其内在一致性仅依赖于转换映射在 $p$ 附近的 $C^1$ 性质。$C^\infty$ 相容性是一个更强的条件，它保证了我们可以任意阶地求导，并为我们提供了光滑向量场和张量场等更丰富的结构。[@problem_id:3034036]

#### 第一种定义：作为曲线等价类的切向量

一种非常直观的定义切向量的方式是将其视为穿过某一点的所有光滑曲线的“瞬时速度”。

考虑[流形](@entry_id:153038) $M$ 上的一个点 $p$。一条经过 $p$ 的光滑曲线是指定义在包含 $0$ 的某个[开区间](@entry_id:157577) $(-\epsilon, \epsilon)$ 上的[光滑映射](@entry_id:203730) $\gamma: (-\epsilon, \epsilon) \to M$，且满足 $\gamma(0) = p$。

在点 $p$ 附近的一个局部图卡 $(U, \varphi)$ 中，曲线 $\gamma$ 的坐标表示为 $\varphi \circ \gamma$，这是一个从 $(-\epsilon, \epsilon)$ 的[子集](@entry_id:261956)到 $\mathbb{R}^n$ 的映射。我们可以在 $t=0$ 处计算其在[欧氏空间](@entry_id:138052)中的速度向量：$\frac{d}{dt}\big|_{t=0} (\varphi \circ \gamma)(t) \in \mathbb{R}^n$。

自然地，我们定义一个**[切向量](@entry_id:265494)**（tangent vector）为所有在 $p$ 点“一阶接触”的曲线的集合。我们称两条曲线 $\gamma_1$ 和 $\gamma_2$ 在 $p$ 点等价（记作 $\gamma_1 \sim \gamma_2$），如果它们在**任意一个**包含 $p$ 的图卡 $(U, \varphi)$ 中的速度向量相同：
$$
\frac{d}{dt}\bigg|_{t=0} (\varphi \circ \gamma_1)(t) = \frac{d}{dt}\bigg|_{t=0} (\varphi \circ \gamma_2)(t)
$$
这个[等价关系](@entry_id:138275)是独立于图卡选择的。如果我们换用另一个图卡 $(V, \psi)$，令转换映射为 $\Phi = \psi \circ \varphi^{-1}$，那么根据[链式法则](@entry_id:190743)：
$$
\frac{d}{dt}\bigg|_{t=0} (\psi \circ \gamma)(t) = D\Phi(\varphi(p)) \cdot \left( \frac{d}{dt}\bigg|_{t=0} (\varphi \circ \gamma)(t) \right)
$$
其中 $D\Phi(\varphi(p))$ 是转换映射在点 $\varphi(p)$ 的雅可比矩阵，它是一个可逆的线性变换。由于 $D\Phi(\varphi(p))$ 是线性的，它保持了速度向量的相等关系。因此，如果两条曲线在一个图卡下等价，它们在所有图卡下都等价。[@problem_id:3034023]

所有与某条曲线等价的曲线集合构成一个[等价类](@entry_id:156032)，我们把这个等价类定义为点 $p$ 处的一个[切向量](@entry_id:265494)。所有在 $p$ 点的切向量的集合构成了**切空间**（tangent space），记为 $T_pM$。通过图卡 $\varphi$ 提供的映射 $[\gamma] \mapsto \frac{d}{dt}\big|_{t=0} (\varphi \circ \gamma)(t)$，我们可以建立 $T_pM$ 与 $\mathbb{R}^n$ 之间的一一对应。利用这个对应关系，我们可以将 $\mathbb{R}^n$ 的[向量空间](@entry_id:151108)结构“[拉回](@entry_id:160816)”到 $T_pM$ 上，定义[切向量](@entry_id:265494)的加法和标量乘法。由于不同图卡之间的速度向量通过一个[线性变换](@entry_id:149133)（雅可比矩阵）相关联，这个赋予 $T_pM$ 的[向量空间](@entry_id:151108)结构是内在的、与图卡选择无关的。[@problem_id:3034023]

#### 第二种定义：[作为导子的切向量](@entry_id:195225)

[切向量](@entry_id:265494)还有一种等价的、更具代数色彩的定义。一个在点 $p$ 的[切向量](@entry_id:265494)可以被定义为一个作用在 $p$ 点光滑函数芽（germs of smooth functions）代数上的**导子**（derivation）。

一个在点 $p$ 的导子 $v$ 是一个[线性映射](@entry_id:185132) $v: C^\infty(M) \to \mathbb{R}$，它满足**[莱布尼茨法则](@entry_id:157949)**（Leibniz rule）：对于任意两个[光滑函数](@entry_id:267124) $f, g \in C^\infty(M)$，
$$
v(fg) = f(p)v(g) + g(p)v(f)
$$
所有在点 $p$ 的导子的集合也构成一个 $n$ 维实[向量空间](@entry_id:151108)，这个空间就是切空间 $T_pM$。[@problem_id:3034022]

这两种定义是等价的。给定一个曲线等价类 $[\gamma]$，我们可以定义一个导子 $v_{[\gamma]}$：
$$
v_{[\gamma]}(f) := \frac{d}{dt}\bigg|_{t=0} (f \circ \gamma)(t)
$$
反之，任何导子都可以被证明对应于某个曲线等价类。导子定义强调了[切向量](@entry_id:265494)的局部性：一个导子 $v$ 作用于函数 $f$ 的值 $v(f)$ 仅依赖于 $f$ 在 $p$ 点的一个任意小的邻域内的行为。[@problem_id:3034033]

#### [坐标基](@entry_id:270149)底与变换法则

给定一个图卡 $(U, x)$，其中 $x = (x^1, \dots, x^n)$ 是[局部坐标](@entry_id:181200)函数，我们可以定义一组切空间的自然基底。**坐标[切向量](@entry_id:265494)** $\left.\frac{\partial}{\partial x^i}\right|_p$ 定义为对光滑函数求沿第 $i$ 个坐标方向的[偏导数](@entry_id:146280)：
$$
\left.\frac{\partial}{\partial x^i}\right|_p (f) := \frac{\partial (f \circ x^{-1})}{\partial u^i} (x(p))
$$
其中 $u^i$ 是 $\mathbb{R}^n$ 中的标准坐标。这组向量 $\left\{\left.\frac{\partial}{\partial x^i}\right|_p\right\}_{i=1}^n$ 构成了 $T_pM$ 的一个基底。

任何切向量 $v \in T_pM$ 都可以唯一地写成这个基底的[线性组合](@entry_id:154743) $v = \sum_{i=1}^n v^i \left.\frac{\partial}{\partial x^i}\right|_p$。根据定义，这个向量作用在函数 $f$ 上的结果是：
$$
v(f) = \sum_{i=1}^n v^i \left.\frac{\partial}{\partial x^i}\right|_p (f) = \sum_{i=1}^n v^i \frac{\partial (f \circ x^{-1})}{\partial u^i}(x(p))
$$
这个公式将抽象的导子作用与具体的坐标偏导数联系起来。[@problem_id:3034030]

例如，考虑从北极点 $N=(0,0,1)$ 进行球极投影的 $S^2$ 的一部分。设[坐标映射](@entry_id:747874) $x^{-1}: \mathbb{R}^2 \to S^2$ 为 $x^{-1}(u,v) = (\frac{2u}{u^2+v^2+1}, \frac{2v}{u^2+v^2+1}, \frac{u^2+v^2-1}{u^2+v^2+1})$。对于点 $p$ 使得 $x(p)=(1,0)$，以及一个[切向量](@entry_id:265494) $v = 3\left.\frac{\partial}{\partial u}\right|_p + 5\left.\frac{\partial}{\partial v}\right|_p$，我们可以计算它对[高度函数](@entry_id:181180) $f(X,Y,Z)=Z$ 的作用。首先，写出 $f$ 在[坐标系](@entry_id:156346)中的表达式 $\hat{f}(u,v) = f \circ x^{-1}(u,v) = \frac{u^2+v^2-1}{u^2+v^2+1}$。然后计算偏导数并代入点 $(1,0)$：$\frac{\partial \hat{f}}{\partial u}|_{(1,0)} = 1$ 和 $\frac{\partial \hat{f}}{\partial v}|_{(1,0)} = 0$。因此，$v(f) = 3 \cdot 1 + 5 \cdot 0 = 3$。[@problem_id:3034030]

当我们在两个不同的[坐标系](@entry_id:156346) $(U, x)$ 和 $(V, y)$ 之间切换时，相应的基底向量会如何变换？设 $p \in U \cap V$。[基向量](@entry_id:199546) $\left.\frac{\partial}{\partial x^i}\right|_p$ 本身是 $T_pM$ 中一个确定的向量。我们可以将它在 $y$-[坐标基](@entry_id:270149)底下展开。通过应用链式法则，可以推导出著名的**变换法则**：
$$
\left.\frac{\partial}{\partial x^i}\right|_p = \sum_{j=1}^n \left( \left.\frac{\partial y^j}{\partial x^i}\right|_p \right) \left.\frac{\partial}{\partial y^j}\right|_p
$$
这里的系数 $\left.\frac{\partial y^j}{\partial x^i}\right|_p$ 是转换映射 $y \circ x^{-1}$ 的雅可比矩阵在点 $x(p)$ 的 $(j,i)$ 元。这个矩阵描述了从 $x$-基底到 $y$-基底的[线性变换](@entry_id:149133)。从线性代数的角度看，这个雅可比矩阵正是 $T_pM$ 上的[恒等变换](@entry_id:264671) $I: (T_pM, \{\partial/\partial x^i\}) \to (T_pM, \{\partial/\partial y^j\})$ 的[矩阵表示](@entry_id:146025)。[@problem_id:3034034] [@problem_id:3034011]

### 全局景象：[切丛](@entry_id:161294)

到目前为止，我们只讨论了单一点的[切空间](@entry_id:199137)。为了研究整个[流形](@entry_id:153038)上的微分几何，我们需要将所有点的切空间“平滑地”粘合在一起。这个构造的结果就是**切丛**（tangent bundle）。

#### 构造[切丛](@entry_id:161294) $TM$

[切丛](@entry_id:161294) $TM$ 首先是所有[切空间](@entry_id:199137)的**不交并**（disjoint union）：
$$
TM = \bigsqcup_{p \in M} T_pM
$$
一个 $TM$ 中的元素是一个偶对 $(p, v)$，其中 $p \in M$ 且 $v \in T_pM$。有一个自然的**[投影映射](@entry_id:153398)** $\pi: TM \to M$，它将 $(p, v)$ 映射到 $p$。

更重要的是，$TM$ 本身就是一个维度为 $2n$ 的[光滑流形](@entry_id:160799)。它的[光滑结构](@entry_id:159394)是这样定义的：对于 $M$ 上的任意一个图卡 $(U, x)$，我们可以为 $TM$ 定义一个对应的图卡 $(\pi^{-1}(U), \Phi_x)$。$\pi^{-1}(U)$ 是 $M$ 中 $U$ 上方的所有[切向量](@entry_id:265494)的集合。映射 $\Phi_x$ 将一个[切向量](@entry_id:265494) $v \in T_pM$ (其中 $p \in U$) 映射到 $\mathbb{R}^{2n}$ 中的一个点。具体来说，如果 $v$ 在 $x$-基底下的坐标分量是 $(v^1, \dots, v^n)$，那么：
$$
\Phi_x(v) = (x^1(p), \dots, x^n(p), v^1, \dots, v^n) \in \mathbb{R}^n \times \mathbb{R}^n
$$
$TM$ 上的转换映射可以从 $M$ 上的转换映射导出。如果 $M$ 上的转换映射为 $\Psi = y \circ x^{-1}$，那么对应的 $TM$ 上的转换映射将一个点 $(x, v) \in \mathbb{R}^n \times \mathbb{R}^n$ 映射到：
$$
(x, v) \mapsto (\Psi(x), D\Psi_x \cdot v)
$$
其中 $D\Psi_x$ 是 $\Psi$ 在点 $x$ 的[雅可比矩阵](@entry_id:264467)。由于 $\Psi$ 是光滑的，其[雅可比矩阵](@entry_id:264467)的元也是 $x$ 的光滑函数，因此整个转换映射是光滑的。这证实了 $TM$ 确实是一个 $2n$ 维的光滑流形。[@problem_id:3034022]

#### 向量场作为[截面](@entry_id:154995)

有了[切丛](@entry_id:161294)的结构，我们可以精确地定义**光滑向量场**（smooth vector field）。一个光滑向量场 $X$ 是[投影映射](@entry_id:153398) $\pi: TM \to M$ 的一个**光滑[截面](@entry_id:154995)**（smooth section）。这意味着 $X$ 是一个从 $M$ 到 $TM$ 的[光滑映射](@entry_id:203730)，并且对于每个点 $p \in M$，它都指定一个该点的[切向量](@entry_id:265494) $X(p) \in T_pM$，即满足 $\pi \circ X = \mathrm{id}_M$。

这个定义与前面导子的观点完美契合。一个光滑向量场 $X$ 可以看作是一个作用于[光滑函数](@entry_id:267124)代数 $C^\infty(M)$ 上的算子，它将一个光滑函数 $f$ 映射到另一个光滑函数 $X(f)$。其在点 $p$ 的值定义为：
$$
(X(f))(p) := X(p)(f)
$$
其中 $X(p)$ 是一个在点 $p$ 的导子。这个算子 $X: C^\infty(M) \to C^\infty(M)$ 本身就是一个导子，即它满足 $\mathbb{R}$-线性和[莱布尼茨法则](@entry_id:157949)：$X(fg) = fX(g) + gX(f)$。需要注意的是，向量场作为算子是 $\mathbb{R}$-线性的，但不是 $C^\infty(M)$-线性的，因为 $X(hf) = hX(f) + fX(h)$。[@problem_id:3034033]

#### [局部标架](@entry_id:635789)与转换函数

在[流形](@entry_id:153038)的开集 $U$ 上，$TM$ 的一个**[局部标架](@entry_id:635789)**（local frame）是 $n$ 个光滑向量场 $\{e_1, \dots, e_n\}$，使得在 $U$ 中的每个点 $p$，向量集 $\{e_1(p), \dots, e_n(p)\}$ 都构成 $T_pM$ 的一个基底。由图卡 $(U,x)$ 诱导的[坐标向量](@entry_id:153319)场 $\{\frac{\partial}{\partial x^i}\}$ 就是这样一个[局部标架](@entry_id:635789)的典型例子。

基底变换法则在这里扮演了全局性的角色。在两个图卡 $(U,x)$ 和 $(V,y)$ 的重叠区域 $U \cap V$ 上，我们有两个[局部标架](@entry_id:635789) $\{\frac{\partial}{\partial x^i}\}$ 和 $\{\frac{\partial}{\partial y^j}\}$。它们之间的关系由雅可比矩阵给出。我们可以定义一个**转换函数**（transition function） $g_{VU}: U \cap V \to \mathrm{GL}(n, \mathbb{R})$，它在每个点 $p \in U \cap V$ 的值是该点的基底[变换矩阵](@entry_id:151616)，即[雅可比矩阵](@entry_id:264467) $J(y \circ x^{-1})|_p$。
$$
g_{VU}(p) = \left( \frac{\partial y^j}{\partial x^i} \right)_p
$$
这些以[一般线性群](@entry_id:141275) $\mathrm{GL}(n, \mathbb{R})$ 为值的[矩阵值函数](@entry_id:199897)，编码了[切丛](@entry_id:161294)是如何从一个[局部平凡化](@entry_id:267993)（由一个图卡给出）过渡到另一个的。[@problem_id:3034012]

以 $S^2$ 上的两个球极投影[坐标系](@entry_id:156346)为例，从北极投影的 $x$ 坐标 $(u_1, u_2)$ 和从南极投影的 $y$ 坐标 $(v_1, v_2)$ 之间的转换映射为 $v_1 = \frac{u_1}{u_1^2+u_2^2}, v_2 = \frac{u_2}{u_1^2+u_2^2}$。其雅可比矩阵，即[切丛](@entry_id:161294)的转换函数，为：
$$
\tau_{xy}(u_1, u_2) = \frac{1}{(u_1^2+u_2^2)^2} \begin{pmatrix} u_2^2 - u_1^2 & -2u_1u_2 \\ -2u_1u_2 & u_1^2 - u_2^2 \end{pmatrix}
$$
这个矩阵的行列式为 $-\frac{1}{(u_1^2+u_2^2)^2}$。负号表明这两个坐标图卡给出了 $S^2$ 的相反定向。[@problem_id:3034013]

在三个图卡 $(U,x), (V,y), (W,z)$ 的三重重叠区域，转换函数满足重要的**上链条件**（cocycle condition）：
$$
g_{WU}(p) = g_{WV}(p) g_{VU}(p) \quad \text{for } p \in U \cap V \cap W
$$
这对应于[雅可比矩阵](@entry_id:264467)的链式法则：$J(z \circ x^{-1}) = J(z \circ y^{-1}) \cdot J(y \circ x^{-1})$。这个条件保证了切丛作为一个纤维丛的整体结构是协调一致的。[@problem_id:3034012]

### 重要延伸：[带边流形](@entry_id:159788)

我们的理论可以延伸到**[带边流形](@entry_id:159788)**（manifolds with boundary）。对于边界 $\partial M$ 上的一个点 $p$，[切空间](@entry_id:199137) $T_pM$ 仍然可以被定义为 $p$ 点的导[子集](@entry_id:261956)合，它依然是一个 $n$ 维[向量空间](@entry_id:151108)。[@problem_id:3034026]

在[边界点](@entry_id:176493) $p$，[切空间](@entry_id:199137) $T_pM$ 包含一个特殊的[子空间](@entry_id:150286)，即边界自身的切空间 $T_p(\partial M)$。这是一个 $(n-1)$ 维的[子空间](@entry_id:150286)，由那些“沿着”边界方向的向量组成。

更重要的是，我们可以区分指向[流形](@entry_id:153038)“内部”和“外部”的向量。一个[切向量](@entry_id:265494) $v \in T_pM$ 被称为**内指的**（inward-pointing），如果在一个将 $p$ 映射到[半空间](@entry_id:634770) $H^n = \{x \in \mathbb{R}^n | x^n \ge 0\}$ 边界的局部图卡中， $v$ 的第 $n$ 个坐标分量 $v^n$ 是非负的 ($v^n \ge 0$)。如果 $v^n > 0$，则称其为**严格内指的**。如果 $v^n < 0$，则称其为**外指的**。

这个分类是良定义的，因为它不依赖于边界图卡的选择。任何两个边界图卡之间的转换映射，其[雅可比矩阵](@entry_id:264467)在边界点处必须具有特定的块状结构，这保证了第 $n$ 个坐标分量的符号（或是否为零）在[坐标变换](@entry_id:172727)下保持不变。具体来说，[变换矩阵](@entry_id:151616)中 $\frac{\partial y^n}{\partial x^n}$ 这一项必须是正的。[@problem_id:3034026]

一个等价的、无坐标的定义可以通过**边界定义函数** $\rho$ 给出。这是一个光滑函数，在[流形](@entry_id:153038)内部取正值，在边界上为零，且在边界上梯度非零。一个向量 $v \in T_pM$ 是内指的，当且仅当 $v(\rho) \ge 0$。这个条件将几何直观与代数计算优雅地联系起来。[@problem_id:3034026]