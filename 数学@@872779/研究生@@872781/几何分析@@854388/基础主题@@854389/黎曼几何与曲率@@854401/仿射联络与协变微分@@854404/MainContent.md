## 引言
在平坦的欧几里得空间中，对向量场求导是一个直观且定义明确的过程。然而，一旦我们踏入弯曲的[光滑流形](@entry_id:160799)的领域，这一基本操作就面临着根本性的挑战。由于[流形](@entry_id:153038)上每一点的[切空间](@entry_id:199137)都是一个独立的[向量空间](@entry_id:151108)，我们无法直接比较和相减在不同点上的向量，这使得微积分的基石——导数的定义变得不再明确。这种在弯曲空间中如何一致地进行[微分](@entry_id:158718)的知识鸿沟，正是[仿射联络](@entry_id:160152)与[协变微分](@entry_id:263981)理论所要解决的核心问题。

本文旨在系统地构建在光滑流形上进行[微分](@entry_id:158718)的完整框架。通过学习本文，您将深入理解为何需要一种新的导数，以及[仿射联络](@entry_id:160152)是如何作为一种附加的几何结构来精确地满足这一需求的。

- 在“**原理与机制**”一章中，我们将从[协变微分](@entry_id:263981)的必要性出发，建立[仿射联络](@entry_id:160152)的公理化体系。您将学习到联络如何通过其[局部坐标](@entry_id:181200)表示——克氏符号（Christoffel symbols）——来修正朴素的导数，并探索其在平行移动、曲率等核心几何概念中的深刻意义，最终聚焦于黎曼几何中至关重要的[列维-奇维塔联络](@entry_id:161107)。

- 随后的“**应用与跨学科联系**”一章将展示这些抽象理论的强大威力。我们将探讨联络如何定义了空间中的“最直路径”（[测地线](@entry_id:269969)），以及曲率如何决定了这些路径的汇聚与发散。更进一步，您将看到这些几何思想如何自然地延伸，成为描述广义相对论和基本粒子相互作用的规范场论等现代物理学理论的通用语言。

- 最后，在“**动手实践**”部分，您将通过一系列精心设计的计算练习，从[平直空间](@entry_id:204618)到弯曲球面，亲手应用这些概念，从而将理论知识转化为解决具体几何问题的实践能力。

通过这三个层层递进的章节，您将不仅掌握[仿射联络](@entry_id:160152)的数学定义，更能体会到它作为连接纯粹几何与物理现实的桥梁所扮演的关键角色。

## 原理与机制

### [协变微分](@entry_id:263981)的必要性

在平坦的欧几里得空间 $\mathbb{R}^n$ 中，对向量场进行[微分](@entry_id:158718)是一个直接的操作。给定一个向量场 $Y$，其在某点 $p$ 沿另一向量 $X_p$ 方向的导数可以通过对 $Y$ 的分量函数求[方向导数](@entry_id:189133)来计算，这个过程与[坐标系](@entry_id:156346)的选取无关（只要是笛卡尔坐标系）。然而，当我们将研究对象推广到一般的**光滑流形 (smooth manifold)** 时，情况变得复杂起来。

一个光滑流形在局部上看起来像欧几里得空间，但缺乏一个全局统一的[坐标系](@entry_id:156346)。在[流形](@entry_id:153038)上的一点 $p$，其[切向量](@entry_id:265494)构成一个[向量空间](@entry_id:151108)，称为**切空间 (tangent space)**，记作 $T_p M$。对于[流形](@entry_id:153038)上不同的两点 $p$ 和 $q$，它们的切空间 $T_p M$ 和 $T_q M$ 是两个独立的[向量空间](@entry_id:151108)，两者之间没有典范的等同关系。

这给我们定义向量场的导数带来了根本性的困难。导数的定义通常涉及[差商](@entry_id:136462)，例如 $\lim_{h \to 0} \frac{Y(p+h) - Y(p)}{h}$。在[流形](@entry_id:153038)上，这意味着要比较在两个不同点 $\gamma(t)$ 和 $\gamma(0)$ 处的切向量 $Y(\gamma(t))$ 和 $Y(\gamma(0))$。由于它们分属不同的[向量空间](@entry_id:151108)，直接相减是无意义的。

为了克服这一困难，一个看似自然的方法是引入一个[局部坐标](@entry_id:181200)图 $(U, x^i)$。在此[坐标图](@entry_id:156506)中，任何切向量都可以表示为[基向量](@entry_id:199546) $\{\partial_i = \partial/\partial x^i\}$ 的[线性组合](@entry_id:154743)。一个向量场 $Y$ 可以写成 $Y = Y^i \partial_i$，其中 $Y^i$ 是坐标函数。于是，我们可以尝试定义一个“朴素”的导数，即在给定向量场 $X = X^i \partial_i$ 的方向上，对 $Y$ 的分量函数 $Y^j$ 求[方向导数](@entry_id:189133) [@problem_id:2968224]：
$$ (D_X Y)^j := X(Y^j) = X^i \frac{\partial Y^j}{\partial x^i} $$
这个定义看似合理，但它有一个致命的缺陷：其结果依赖于[坐标系](@entry_id:156346)的选取，因此不是一个几何上内在的对象。换言之，这个操作不是一个**张量性 (tensorial)** 操作。一个在 $Y$ 变元上是张量性的操作，其在点 $p$ 的取值应该只依赖于向量 $Y_p$ 本身，而与 $Y$ 在 $p$ 点邻域内的延拓方式无关。

我们可以通过一个代数检验来证明这一点。考虑将向量场 $Y$ 乘以一个光滑函数 $f \in C^\infty(M)$，得到新的向量场 $fY$。如果上述定义的导数 $D_X$ 在第二变元上是张量性的，它必须满足 $C^\infty(M)$-线性性，即 $(D_X(fY))_p = f(p) (D_X Y)_p$。然而，根据求导的[莱布尼茨法则](@entry_id:157949)，我们得到：
$$ (D_X(fY))^j = X(f Y^j) = (Xf) Y^j + f (X Y^j) $$
用向量形式写出在点 $p$ 的值，即为：
$$ (D_X(fY))_p = (Xf)_p Y_p + f(p) (D_X Y)_p $$
与张量性所要求的表达式相比，多出了一项 $(Xf)_p Y_p$。这一项的存在表明，朴素导数的值不仅依赖于 $f(p)$ 和 $Y_p$，还依赖于函数 $f$ 沿 $X$ 方向的变化率 $(Xf)_p$。这意味着，即使两个向量场在点 $p$ 的值相同（例如 $Y$ 和 $fY$ 在 $f(p)=1$ 时），它们的朴素导数也可能不同。这从根本上说明，这个操作不是一个内在的几何运算，其结果会随[坐标系](@entry_id:156346)的改变而改变 [@problem_id:2968224]。

为了在[流形](@entry_id:153038)上建立一个一致的[微分](@entry_id:158718)理论，我们必须引入一种额外的结构，用以“修正”朴素导数，使其成为一个几何上良定义的操作。这种结构被称为**[仿射联络](@entry_id:160152) (affine connection)**。它的核心作用是提供一个规则，用于比较无穷近的两个切空间中的向量，从而使[微分](@entry_id:158718)运算成为可能。

### [仿射联络](@entry_id:160152)的公理化定义

一个[仿射联络](@entry_id:160152) $\nabla$ 是一个映射，它取两个向量场 $X, Y \in \Gamma(TM)$，生成一个新的向量场 $\nabla_X Y$，并满足一组特定的公理。$\nabla_X Y$ 被称为 $Y$ 沿 $X$ 的**协变导数 (covariant derivative)**。这些公理精确地刻画了我们期望一个“好的”导数所应具备的性质 [@problem_id:3025051]。

对于任意向量场 $X, Y, Z \in \Gamma(TM)$，光滑函数 $f \in C^\infty(M)$，以及实常数 $a, b \in \mathbb{R}$，一个**[仿射联络](@entry_id:160152)** $\nabla$ 必须满足：

1.  **第一变元的 $\mathcal{C}^{\infty}(M)$-线性性 ($C^\infty(M)$-linearity in the first argument):**
    $$ \nabla_{fX} Y = f \nabla_X Y $$
    这也包含了 $\mathbb{R}$-线性性，即 $\nabla_{aX+bZ} Y = a\nabla_X Y + b\nabla_Z Y$。该性质表明，在点 $p$ 的[协变导数](@entry_id:152476) $(\nabla_X Y)_p$ 只依赖于 $X$ 在该点的值 $X_p$。这是一个关键的张量性特征 [@problem_id:3025068]。

2.  **第二变元的 $\mathbb{R}$-线性性 ($\mathbb{R}$-linearity in the second argument):**
    $$ \nabla_X (aY+bZ) = a\nabla_X Y + b\nabla_X Z $$
    这确保了对向量场的[线性组合](@entry_id:154743)求导时，导数算子可以分配进去。

3.  **第二变元的[莱布尼茨法则](@entry_id:157949) (Leibniz rule in the second argument):**
    $$ \nabla_X(fY) = (Xf)Y + f \nabla_X Y $$
    这条公理是整个定义的核心。它规定了[协变导数](@entry_id:152476)如何作用于一个函数与一个向量场的乘积。请注意，它恰好包含了之前导致朴素导数失败的项 $(Xf)Y$。通过将这一项作为公理的一部分，联络为我们提供了一个内在的、与坐标无关的[微分法则](@entry_id:169252)。

从这些公理中，我们可以立即看到协变导数算子 $\nabla_X Y$ 的一个重要“不对称”特性 [@problem_id:3025068]。一方面，由于第一条公理，$(\nabla_X Y)_p$ 在其第一个变元上是张量性的：它的值只取决于向量 $X_p$，而与向量场 $X$ 在 $p$ 点邻域的行为无关。另一方面，由于第三条公理（[莱布尼茨法则](@entry_id:157949)）的存在，$(\nabla_X Y)_p$ 在其第二个变元上**不是**张量性的。即使 $Y_p=0$，只要我们构造一个适当的向量场 $Y$（例如 $Y=fZ$ 使得 $f(p)=0$ 但 $X(f)_p \neq 0$），其协变导数 $(\nabla_X Y)_p$ 仍可能非零。这意味着 $(\nabla_X Y)_p$ 不仅依赖于 $Y_p$ 的值，还依赖于 $Y$ 在 $p$ 点附近的一阶变化情况（即 $Y$ 在 $p$ 的1-jet）。这表明 $\nabla_X$ 是作用于 $Y$ 的一个一阶微分算子。

### [局部坐标](@entry_id:181200)下的联络：克氏符号

虽然联络的定义是抽象和无坐标的，但在实际计算中，我们通常需要在[局部坐标系](@entry_id:751394)中进行操作。在[局部坐标](@entry_id:181200)图 $(U, x^i)$ 中，切空间的[基向量](@entry_id:199546)为 $\{\partial_i = \partial/\partial x^i\}$。联络在这些[基向量](@entry_id:199546)上的作用，完全决定了它在该坐标域中的行为。其作用结果可以再次用这组[基向量](@entry_id:199546)展开，展开系数被称为**克氏符号 (Christoffel symbols)** 或**[联络系数](@entry_id:157618) (connection coefficients)**，记作 $\Gamma^k_{ij}$：
$$ \nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k $$
这里我们使用了爱因斯坦求和约定。

利用联络的公理，我们可以推导出任意向量场 $Y = Y^j \partial_j$ 沿 $X = X^i \partial_i$ 的[协变导数](@entry_id:152476)的坐标表达式：
$$ \nabla_X Y = X^i \nabla_{\partial_i} (Y^j \partial_j) = X^i \left( (\partial_i Y^j) \partial_j + Y^j \nabla_{\partial_i} \partial_j \right) = X^i \left( (\partial_i Y^j) \partial_j + Y^j \Gamma^k_{ij} \partial_k \right) $$
整理后，我们得到 $\nabla_X Y$ 的第 $k$ 个分量：
$$ (\nabla_X Y)^k = X^i (\partial_i Y^k + \Gamma^k_{ij} Y^j) $$
这个公式极为重要。它清晰地展示了协变导数是如何由两部分构成的：$\partial_i Y^k$ 是我们之前讨论的“朴素导数”，而 $\Gamma^k_{ij} Y^j$ 是由联络提供的“修正项”。正是这个修正项，抵消了朴素导数在坐标变换下的不良行为，使得整个表达式成为一个几何上良定义的向量分量。

一个至关重要的事实是：克氏符号 $\Gamma^k_{ij}$ 本身**不是**一个张量的分量 [@problem_id:2972229]。在[坐标变换](@entry_id:172727) $x \to \tilde{x}$ 下，它们的变换法则不是[张量变换法则](@entry_id:185176)，而是一个更复杂的非齐次法则：
$$ \tilde{\Gamma}^{m}_{pq} = \frac{\partial \tilde{x}^{m}}{\partial x^{r}} \frac{\partial x^{s}}{\partial \tilde{x}^{p}} \frac{\partial x^{t}}{\partial \tilde{x}^{q}} \Gamma^{r}_{st} + \frac{\partial \tilde{x}^{m}}{\partial x^{r}} \frac{\partial^{2} x^{r}}{\partial \tilde{x}^{p} \partial \tilde{x}^{q}} $$
变换法则中的第二项，即非齐次项，涉及[坐标变换](@entry_id:172727)函数的[二阶偏导数](@entry_id:635213)。正是这一项的存在，证明了 $\Gamma^k_{ij}$ 的非张量性。这也解释了为什么在某一点 $p$ 可以选择一个特殊的[坐标系](@entry_id:156346)（例如黎曼正规坐标），使得该点的所有克氏符号都为零，$\Gamma^k_{ij}(p)=0$。如果 $\Gamma^k_{ij}$ 是张量，那么在一个[坐标系](@entry_id:156346)中为零意味着在所有[坐标系](@entry_id:156346)中都为零，这显然与事实不符。

然而，这个非齐次的变换法则也揭示了一个深刻的结构。如果我们考虑两个不同的联络 $\nabla$ 和 $\tilde{\nabla}$，它们的克氏符号分别为 $\Gamma^k_{ij}$ 和 $\tilde{\Gamma}^k_{ij}$，那么它们的差 $A^k_{ij} = \Gamma^k_{ij} - \tilde{\Gamma}^k_{ij}$ 的变换法则是齐次的。这是因为非齐次项只依赖于坐标变换本身，与具体联络无关，所以在作差时会被消掉。这意味着两个联络之差 $A(X,Y) = \nabla_X Y - \tilde{\nabla}_X Y$ 是一个真正的 (1,2)-型张量 [@problem_id:2972229, @problem_id:3025052]。

这一观察导出一个优美的结论：[流形](@entry_id:153038)上所有[仿射联络](@entry_id:160152)的集合 $\mathrm{Conn}(TM)$ 构成一个**[仿射空间](@entry_id:152906) (affine space)**，其模型是 (1,2)-型[张量场](@entry_id:190170)的[向量空间](@entry_id:151108) $\Gamma(T^1_2 M)$。这意味着，一旦我们选定一个参考联络 $\nabla^0$，任何其他的联络 $\nabla$ 都可以唯一地表示为 $\nabla = \nabla^0 + A$，其中 $A$ 是一个 (1,2)-型张量场 [@problem_id:3025052]。

### 将[协变微分](@entry_id:263981)推广到所有张量

联络的威力在于它可以被唯一地推广，从而作用于任意类型的[张量场](@entry_id:190170)。这个推广遵循以下几条自然法则 [@problem_id:3025057]：

1.  对 (0,0)-型张量（即[光滑函数](@entry_id:267124) $f$），协变导数就是普通的方向导数：$\nabla_X f = Xf$。
2.  对 (1,0)-型张量（即向量场 $Y$），它就是给定的联络作用：$\nabla_X Y$。
3.  它满足**[张量积](@entry_id:140694)的[莱布尼茨法则](@entry_id:157949) (Leibniz rule for tensor products):** $\nabla_X(A \otimes B) = (\nabla_X A) \otimes B + A \otimes (\nabla_X B)$。
4.  它**与缩并可交换 (commutes with contractions)**，例如，对一个 (1,1)-型张量 $T$，有 $\nabla_X(\mathrm{tr}(T)) = \mathrm{tr}(\nabla_X T)$。

利用这些法则，我们可以推导出[协变导数](@entry_id:152476)如何作用于一个 (0,1)-型张量，即一个**余向量场 (covector field)** 或 **[1-形式](@entry_id:270392) (1-form)** $\omega$。考虑标量函数 $\omega(Y)$，根据法则4和1：
$$ X(\omega(Y)) = \nabla_X(\omega(Y)) = (\nabla_X \omega)(Y) + \omega(\nabla_X Y) $$
整理可得：
$$ (\nabla_X \omega)(Y) = X(\omega(Y)) - \omega(\nabla_X Y) $$
在[局部坐标](@entry_id:181200)中，协变导数作用于 $\omega = \omega_j dx^j$ 的分量形式为：
$$ (\nabla_i \omega)_j = \partial_i \omega_j - \Gamma^k_{ij} \omega_k $$
请注意这里修正项的符号为负，这反映了余向量（协变分量）与向量（[逆变分量](@entry_id:185440)）在变换下的对偶性。

通过反复应用[莱布尼茨法则](@entry_id:157949)，我们可以得到作用于任意 $(r,s)$-型张量 $T$ 的[协变导数](@entry_id:152476)的通用坐标表达式 [@problem_id:3025057]：
$$ (\nabla_k T)^{i_1 \dots i_r}{}_{j_1 \dots j_s} = \partial_k T^{i_1 \dots i_r}{}_{j_1 \dots j_s} + \sum_{\alpha=1}^r \Gamma^{i_\alpha}_{k m} T^{i_1 \dots m \dots i_r}{}_{j_1 \dots j_s} - \sum_{\beta=1}^s \Gamma^{m}_{k j_\beta} T^{i_1 \dots i_r}{}_{j_1 \dots m \dots j_s} $$
在这个公式中，每一项的含义都很直观：$\partial_k T^{\dots}_{\dots}$ 是对张量分量的普通[偏导数](@entry_id:146280)，然后对每一个[逆变](@entry_id:192290)指标 $i_\alpha$ 加上一个“$+ \Gamma$”修正项，对每一个[协变](@entry_id:634097)指标 $j_\beta$ 减去一个“$- \Gamma$”修正项。这个公式是[张量分析](@entry_id:161423)的核心工具。

### 联络的几何学：平行移动与曲率

联络的深刻几何意义通过**平行移动 (parallel transport)** 的概念得以彰显。联络本质上提供了一种沿着任意曲线“平行”地移动一个[切向量](@entry_id:265494)的规则。

给定一条光滑曲线 $\gamma: [t_0, t_1] \to M$，一个沿着该曲线定义的向量场 $V(t)$（即对任意 $t$，都有 $V(t) \in T_{\gamma(t)}M$）被称为是**平行的 (parallel)**，如果它沿着曲线的协变导数为零 [@problem_id:3032596]：
$$ D_t V(t) := \nabla_{\dot{\gamma}(t)} V(t) = 0 $$
其中 $\dot{\gamma}(t)$ 是曲线的切向量。在[局部坐标](@entry_id:181200)中，这构成了一个关于向量分量 $V^k(t)$ 的[一阶常微分方程组](@entry_id:635184) (ODE)：
$$ \frac{dV^k}{dt}(t) + \Gamma^k_{ij}(\gamma(t)) \frac{d\gamma^i}{dt} V^j(t) = 0 $$
[常微分方程](@entry_id:147024)的基本定理保证，对于任意给定的初始向量 $v \in T_{\gamma(t_0)}M$，上述方程存在唯一的解 $V(t)$，满足[初始条件](@entry_id:152863) $V(t_0)=v$。

这个唯一解的存在性使我们能够定义**平行移动映射 (parallel transport map)** $P_{\gamma}^{t_0 \to t_1}: T_{\gamma(t_0)}M \to T_{\gamma(t_1)}M$，它将初始向量 $v$ 映为向量场在曲线终点的值 $V(t_1)$。这个映射具有以下重要性质 [@problem_id:3032596]：

*   它是一个**[线性同构](@entry_id:270529) (linear isomorphism)**。
*   它与曲线的（保持定向的）**重参数化无关 (independent of reparameterization)**。
*   其逆映射等于沿着反向曲线的平行移动：$(P_{\gamma}^{t_0 \to t_1})^{-1} = P_{\gamma_{\mathrm{rev}}}^{t_1 \to t_0}$。

一个自然的问题是：从点 $p$ 到点 $q$ 的平行移动是否依赖于所走的路径？一般而言，答案是肯定的。沿着两条不同的路径 $\gamma_1$ 和 $\gamma_2$ 平行移动同一个向量 $v$，到达终点时得到的向量通常是不同的。

平行移动对路径的依赖程度，由[流形](@entry_id:153038)的**曲率 (curvature)** 来衡量。如果一个联络的**[曲率张量](@entry_id:181383) (curvature tensor)** $R$ 处处为零，该联络就被称为是**平坦的 (flat)**。在一个单连通区域内，平坦联络的平行移动是与路径无关的 [@problem_id:3032596]。更一般地，将一个向量沿一个无穷小闭合回路平行移动一周后，它与初始向量的差异就由[曲率张量](@entry_id:181383)决定。

### [黎曼几何](@entry_id:160508)中的[列维-奇维塔联络](@entry_id:161107)

到目前为止，我们讨论的[仿射联络](@entry_id:160152)是在[流形](@entry_id:153038)上任意选择的一种附加结构。然而，对于装备了**[度规张量](@entry_id:160222) (metric tensor)** $g$ 的**黎曼流形 (Riemannian manifold)** $(M,g)$，存在一种由度规本身唯一决定的“自然”联络。

这个典范的联络被称为**列维-奇维塔联络 (Levi-Civita connection)**，它由以下两个关键的几何属性唯一确定 [@problem_id:3025041]：

1.  **[度规兼容性](@entry_id:265910) (Metric compatibility):** 联络保持度规不变，即 $\nabla g = 0$。这意味着[度规张量](@entry_id:160222)是“[协变](@entry_id:634097)常数”。该条件等价于协变导数满足关于度规的乘积法则 [@problem_id:2974971]：
    $$ X(g(Y,Z)) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z) $$
    这个性质有一个极其重要的推论：与度规兼容的联络所诱导的平行移动保持向量间的[内积](@entry_id:158127)不变。如果 $V(t)$ 和 $W(t)$ 沿曲线平行，则[内积](@entry_id:158127) $g(V(t), W(t))$ 是一个常数。这意味着向量的长度和向量之间的夹角在平行移动过程中保持不变 [@problem_id:3032596, @problem_id:2974971]。

2.  **无挠性 (Torsion-free):** **[挠率张量](@entry_id:204137) (torsion tensor)** $T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y]$ 为零。在[坐标基](@entry_id:270149)中，由于 $[\partial_i, \partial_j]=0$，此条件等价于克氏符号关于下两个指标的对称性：
    $$ \Gamma^k_{ij} = \Gamma^k_{ji} $$

**[黎曼几何基本定理](@entry_id:189185) (Fundamental Theorem of Riemannian Geometry)** 指出：在任何一个[黎曼流形](@entry_id:261160) $(M,g)$ 上，存在唯一一个既度规兼容又[无挠的](@entry_id:161664)[仿射联络](@entry_id:160152)。这个联络就是列维-奇维塔联络 [@problem_id:3025041]。

该联络的存在性和唯一性可以通过**科祖尔公式 (Koszul formula)** 来证明，该公式完全用度规和李括号来表示 $\nabla_X Y$。在[局部坐标](@entry_id:181200)中，这给出了克氏符号完全由度规分量及其一阶导数决定的显式表达式：
$$ \Gamma^k_{ij} = \frac{1}{2} g^{kl}(\partial_i g_{jl} + \partial_j g_{il} - \partial_l g_{ij}) $$
这个公式的一个直接推论是：如果在某个[坐标系](@entry_id:156346)中，度规的分量 $g_{ij}$ 是常数（例如欧几里得空间中的标准[笛卡尔坐标](@entry_id:167698)），那么它们的导数全为零，从而该[坐标系](@entry_id:156346)下所有的列维-奇维塔克氏符号也都为零，$\Gamma^k_{ij}=0$。此时，[协变导数](@entry_id:152476)退化为普通的分量[偏导数](@entry_id:146280) [@problem_id:3025041]。这证实了列维-奇维塔联络确实是[欧氏空间](@entry_id:138052)标准[微分](@entry_id:158718)在弯曲[流形](@entry_id:153038)上的自然推广。

### 更一般的观点：向量[丛上的联络](@entry_id:191877)

联络的概念可以被推广到任意的**向量丛 (vector bundle)** $E \to M$ 上，而不仅限于[切丛](@entry_id:161294) $TM$。这种更抽象的观点在现代微分几何和理论物理（如[规范场](@entry_id:159627)论）中居于核心地位。

向量丛 $E$ 上的一个**联络 (connection)** 是一个线性映射 $\nabla: \Gamma(E) \to \Gamma(T^*M \otimes E)$，它对任意[截面](@entry_id:154995) $s \in \Gamma(E)$ 和函数 $f \in C^\infty(M)$ 满足[莱布尼茨法则](@entry_id:157949) [@problem_id:3025058]：
$$ \nabla(fs) = df \otimes s + f \nabla s $$
这里 $df$ 是 $f$ 的外微分，是一个 1-形式。这个定义直观上将一个[截面](@entry_id:154995)的[全导数](@entry_id:137587) $\nabla(fs)$ 分解为“水平”部分（沿着底[流形](@entry_id:153038) $M$ 的变化，由 $df \otimes s$ 捕捉）和“垂直”部分（在纤维方向上的变化，由 $f\nabla s$ 捕捉）。

在丛 $E$ 的一个[局部坐标](@entry_id:181200)域 $U$ 上，选取一组[局部标架](@entry_id:635789)（[截面](@entry_id:154995)基底）$\{e_1, \dots, e_r\}$，联络在这些基底上的作用定义了**[联络1-形式](@entry_id:275839) (connection 1-forms)** $\omega^i_j \in \Omega^1(U)$：
$$ \nabla e_j = \omega^i_j \otimes e_i $$
任意[截面](@entry_id:154995) $s = s^j e_j$ 的协变导数的局部表达式为：
$$ \nabla s = (ds^i + \omega^i_j s^j) \otimes e_i $$
在标架变换 $e'_k = g^j_k e_j$ 下（其中 $g$ 是一个[可逆矩阵](@entry_id:171829)值的函数），由 [1-形式](@entry_id:270392)构成的联络矩阵 $\omega$ 的变换法则为 [@problem_id:3025058]：
$$ \omega' = g^{-1} \omega g + g^{-1} dg $$
这个变换法则在物理学中被称为**规范变换 (gauge transformation)**。

这个普适的框架将[仿射联络](@entry_id:160152)作为其一个特例：当向量丛是[切丛](@entry_id:161294) $E=TM$ 时，[联络1-形式](@entry_id:275839) $\omega^k_j$ 与克氏符号 $\Gamma^k_{ij}$ 的关系为 $\omega^k_j = \Gamma^k_{ij} dx^i$。因此，关于[仿射联络](@entry_id:160152)的所有概念都可以被视为这个更一般理论的具体体现。