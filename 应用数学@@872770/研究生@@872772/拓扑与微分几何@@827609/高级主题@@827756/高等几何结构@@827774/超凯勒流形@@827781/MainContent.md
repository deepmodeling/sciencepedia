## 引言
在现代[微分几何](@entry_id:145818)与理论物理的交汇处，[超凯勒流形](@entry_id:159760)（Hyperkähler manifolds）以其高度对称和极其丰富的几何结构，占据着一个核心地位。作为[凯勒几何](@entry_id:160314)的自然推广，它们不仅是[里奇平坦](@entry_id:159097)[黎曼流形](@entry_id:261160)的典范，为广义相对论中的[真空解](@entry_id:268947)提供了非平凡的范例，其内在的四元数结构更使其成为连接[代数几何](@entry_id:156300)、[表示论](@entry_id:137998)与[量子场论](@entry_id:138177)的桥梁。然而，尽管其定义抽象，[超凯勒流形](@entry_id:159760)的威力却体现在其解决具体问题的能力上——从解析代数[奇点](@entry_id:137764)到刻画物理系统的真空[模空间](@entry_id:159780)。本文旨在填补从抽象定义到具体应用之间的认知鸿沟，为读者提供一个全面而深入的理解。

文章将分为三个核心部分展开。在第一章 **“原理与机制”** 中，我们将从[和乐群](@entry_id:191471)的视角出发，建立[超凯勒流形](@entry_id:159760)的严格定义，并探讨其三重凯勒结构、[里奇平坦性](@entry_id:187948)、[扭量空间](@entry_id:159706)理论以及超凯勒商等基本[构造原理](@entry_id:141667)。第二章 **“应用与跨学科关联”** 将展示这些几何结构如何在更广阔的舞台上发挥作用，重点介绍其作为[引力瞬子](@entry_id:158147)、[K3曲面](@entry_id:160391)以及规范理论和[弦论](@entry_id:145688)中关键模空间的应用。最后，在 **“动手实践”** 部分，我们精选了几个代表性的计算问题，旨在通过具体操作加深读者对理论知识的掌握。通过这趟旅程，读者将能够领会到[超凯勒流形](@entry_id:159760)为何是当代数学与物理研究中一个如此活跃且成果丰硕的领域。

## 原理与机制

在深入探讨超凯勒（hyperkähler）[流形](@entry_id:153038)的具体实例和应用之前，我们必须首先建立一个坚实的理论基础。本章旨在阐述定义这些丰富几何结构的核心原理，并揭示其内在的运作机制。我们将从[黎曼几何](@entry_id:160508)中[特殊和乐群](@entry_id:158889)的概念出发，逐步揭示[超凯勒流形](@entry_id:159760)所蕴含的四元数结构、度量性质、[复几何](@entry_id:159080)观点以及强大的构造方法。

### 定义：和乐群观点

黎曼流形 $(M, g)$ 的几何特性很大程度上由其列维-奇维塔联络 $\nabla$ 的 **[和乐群](@entry_id:191471)**（holonomy group） $\mathrm{Hol}(g)$ 所决定。和乐群是在某一点 $p \in M$ 的[切空间](@entry_id:199137) $T_p M$ 上的一个[李群](@entry_id:137659)，由沿所有以 $p$ 为基点的闭环路进行平行移动所产生的线性变换构成。它精确地描述了[流形](@entry_id:153038)的曲率如何导致[切向量](@entry_id:265494)在沿闭环移动后发生旋转。

对于一个 $d$ 维的、单连通的、非局部对称的黎曼流形，其和乐群的可能类型是极其有限的，这由著名的 **Berger 分类定理** 给出。除了对应于一般黎曼流形的[特殊正交群](@entry_id:146418) $\mathrm{SO}(d)$ 外，Berger 的列表还包含了一些“特殊”[和乐群](@entry_id:191471)，它们的存在意味着[流形](@entry_id:153038)上具有额外的平行[张量场](@entry_id:190170)，从而拥有更丰富的几何结构 [@problem_id:2980127] [@problem_id:2974182]。

在这个分类中，与[四元数几何](@entry_id:158243)直接相关的两个和乐群是：
1.  **紧[辛群](@entry_id:189031)** $\mathrm{Sp}(n)$：当一个实维数为 $4n$ 的[流形](@entry_id:153038)的[和乐群](@entry_id:191471)是 $\mathrm{Sp}(n)$ 或其[子群](@entry_id:146164)时，该[流形](@entry_id:153038)被称为 **[超凯勒流形](@entry_id:159760)** (hyperkähler manifold)。
2.  **群** $\mathrm{Sp}(n)\mathrm{Sp}(1)$：当一个实维数为 $4n$ ($n \ge 2$) 的[流形](@entry_id:153038)的[和乐群](@entry_id:191471)是 $\mathrm{Sp}(n)\mathrm{Sp}(1)$ 时，该[流形](@entry_id:153038)被称为 **四元数凯勒流形** (quaternionic Kähler manifold)。

区分这两种几何结构至关重要。其核心区别在于[和乐群](@entry_id:191471)如何作用于[切空间](@entry_id:199137)中的四元数结构 [@problem_id:2979275]。一个[超凯勒流形](@entry_id:159760)的和乐群 $\mathrm{Sp}(n)$ **逐点固定** (pointwise fixes) 了一个四元数结构。根据和乐原理——一个[张量场](@entry_id:190170)是[协变](@entry_id:634097)常数（即其协变导数为零）当且仅当它在每一点都被和乐群固定——这意味着[超凯勒流形](@entry_id:159760)上存在三个全局定义的、相互反对易的、协变常数的[复结构](@entry_id:269128) $(I, J, K)$。

相比之下，一个[四元数](@entry_id:147023)凯勒流形的和乐群 $\mathrm{Sp}(n)\mathrm{Sp}(1)$ 并不固定任何一个特定的[复结构](@entry_id:269128)。$\mathrm{Sp}(1)$ 因子（同构于[单位四元数](@entry_id:204470)群，也即 $\mathrm{SU}(2)$）的作用是“旋转”由 $(I, J, K)$ 张成的三维[子空间](@entry_id:150286)。因此，[流形](@entry_id:153038)上不存在任何[协变](@entry_id:634097)常数的[复结构](@entry_id:269128)。取而代之的是，存在一个协变常数的、秩为 3 的 **四元数结构子丛** (quaternionic structure subbundle) $Q \subset \mathrm{End}(TM)$。我们可以将[超凯勒流形](@entry_id:159760)视为[四元数](@entry_id:147023)凯勒流形的一个特例，即其[四元数](@entry_id:147023)结构子丛上的[诱导联络](@entry_id:635081)是平坦的 [@problem_id:2979275]。本章的[焦点](@entry_id:174388)是前者，即[超凯勒流形](@entry_id:159760)。

### [四元数](@entry_id:147023)结构与凯勒性质

从和乐群的定义出发，我们可以给出一个等价且更具操作性的定义。一个 **[超凯勒流形](@entry_id:159760)** 是一个黎曼流形 $(M, g)$，其上配备了三个[复结构](@entry_id:269128)（即满足 $I^2 = J^2 = K^2 = -\mathrm{Id}$ 的 $(1,1)$-张量）$I, J, K$，它们满足以下条件：

1.  **[四元数代数](@entry_id:196348)关系**：$I, J, K$ 满足[四元数](@entry_id:147023)单位的乘法关系，例如 $IJ = -JI = K$。

2.  **[度量兼容性](@entry_id:265910)**：$g$ 与这三个复结构都是兼容的（或者说是埃尔米特(Hermitian)的），即对于任意向量场 $X, Y$ 和任意 $A \in \{I, J, K\}$，都有 $g(AX, AY) = g(X, Y)$。

3.  **[可积性](@entry_id:142415)与平行性**：$I, J, K$ 都是 **协变常数** 的，即关于 $g$ 的列维-奇维塔联络 $\nabla$，我们有 $\nabla I = \nabla J = \nabla K = 0$。

协变常数的性质蕴含了丰富的几何信息。首先，一个协变常数的[殆复结构的可积性](@entry_id:203603)（即其[奈恩黑斯张量](@entry_id:159184)为零）是自动满足的，因此 $I, J, K$ 都是真正的[复结构](@entry_id:269128)。其次，与每个复结构 $A \in \{I, J, K\}$ 相关联的 **凯勒形式** (Kähler form) $\omega_A$，定义为 $\omega_A(X, Y) = g(AX, Y)$，都是闭形式。这是因为由联络的[度量兼容性](@entry_id:265910) ($\nabla g=0$) 和 $A$ 的平行性 ($\nabla A=0$) 可得 $\nabla \omega_A = 0$，而一个[协变](@entry_id:634097)常数的形式必然是闭的 ($d\omega_A=0$)。

因此，一个[超凯勒流形](@entry_id:159760)可以被视为三重[凯勒流形](@entry_id:161192)：$(M, g, I)$, $(M, g, J)$ 和 $(M, g, K)$ 中的每一个都是一个凯勒流形。这正是其名称中“超”的由来。

### 基本范例：平坦[四元数](@entry_id:147023)空间 $\mathbb{H}^n$

最简单、最典型的[超凯勒流形](@entry_id:159760)是 $n$ 维[四元数](@entry_id:147023)[向量空间](@entry_id:151108) $\mathbb{H}^n$，我们将其等同于具有标准[欧几里得度量](@entry_id:147197)的 $\mathbb{R}^{4n}$ [@problem_id:2980135]。

考虑 $\mathbb{H}^n$ 的一组坐标 $(q_1, \dots, q_n)$，其中每个 $q_a = x_a + y_a \mathbf{i} + u_a \mathbf{j} + v_a \mathbf{k}$ 是一个四元数。这给出了 $\mathbb{R}^{4n}$ 的一组坐标 $\{x_a, y_a, u_a, v_a\}_{a=1}^n$。标准[欧几里得度量](@entry_id:147197)为：
$$
g = \sum_{a=1}^{n} \left( dx_a^2 + dy_a^2 + du_a^2 + dv_a^2 \right)
$$
[复结构](@entry_id:269128) $I, J, K$ 由在[切空间](@entry_id:199137)上 **左乘** [四元数](@entry_id:147023)单位 $\mathbf{i}, \mathbf{j}, \mathbf{k}$ 来定义。例如，对任意向量 $v \in T_p\mathbb{H}^n \cong \mathbb{H}^n$，我们定义 $I(v) = \mathbf{i}v$。在[坐标基](@entry_id:270149)矢 $\{\partial_{x_a}, \partial_{y_a}, \partial_{u_a}, \partial_{v_a}\}$ 上，它们的作用是：
$$
\begin{array}{llll}
I \partial_{x_a} = \partial_{y_a},   I \partial_{y_a} = -\partial_{x_a},  I \partial_{u_a} = \partial_{v_a},   I \partial_{v_a} = -\partial_{u_a} \\
J \partial_{x_a} = \partial_{u_a},   J \partial_{y_a} = -\partial_{v_a},  J \partial_{u_a} = -\partial_{x_a},  J \partial_{v_a} = \partial_{y_a} \\
K \partial_{x_a} = \partial_{v_a},   K \partial_{y_a} = \partial_{u_a},   K \partial_{u_a} = -\partial_{y_a},  K \partial_{v_a} = -\partial_{x_a}
\end{array}
$$
由于这些张量在[全局坐标系](@entry_id:171029)下具有常数分量，它们在[欧几里得空间](@entry_id:138052)的平凡[列维-奇维塔联络](@entry_id:161107)下显然是协变常数的。

与之相关的三个凯勒形式 $\omega_I, \omega_J, \omega_K$ 可以通过 $\omega_A(\partial_\mu, \partial_\nu) = g(A\partial_\mu, \partial_\nu)$ 直接计算得出。它们在坐标 [1-形式](@entry_id:270392) $\{dx_a, dy_a, du_a, dv_a\}$ 中的表达式为 [@problem_id:2980135]：
$$
\begin{align*}
\omega_I = \sum_{a=1}^{n} (dx_a \wedge dy_a + du_a \wedge dv_a) \\
\omega_J = \sum_{a=1}^{n} (dx_a \wedge du_a - dy_a \wedge dv_a) = \sum_{a=1}^{n} (dx_a \wedge du_a + dv_a \wedge dy_a) \\
\omega_K = \sum_{a=1}^{n} (dx_a \wedge dv_a + dy_a \wedge du_a)
\end{align*}
$$
这些都是具有[常系数](@entry_id:269842)的 2-形式，因此它们都是闭形式，这直接验证了 $(\mathbb{H}^n, g, I, J, K)$ 是一个[超凯勒流形](@entry_id:159760)。

### 度量性质：[里奇平坦性](@entry_id:187948)

[超凯勒流形](@entry_id:159760)一个极其重要的性质是它们都是 **[里奇平坦](@entry_id:159097)** (Ricci-flat) 的，即它们的里奇张量 $\mathrm{Ric}$ 恒为零。这一事实是[和乐群](@entry_id:191471)限制的直接结果 [@problem_id:2974182]。

如前所述，具有 $\mathrm{Sp}(n)$ 和乐群的[流形](@entry_id:153038)是具有 $\mathrm{SU}(2n)$ 和乐群的[流形](@entry_id:153038)的一个特例，因为 $\mathrm{Sp}(n)$ 是 $\mathrm{SU}(2n)$ 的一个[子群](@entry_id:146164)。对于一个复维数为 $N$ 的[凯勒流形](@entry_id:161192)，其和乐群被限制在 $\mathrm{SU}(N)$ 内的充要条件是其 **典范丛** (canonical bundle) $K_M = \Lambda^N (T^{1,0}M)^*$ 是平凡的。这等价于存在一个处处非零的、[协变](@entry_id:634097)常数的全纯 $(N,0)$-形式 $\Omega$。

由于 $\Omega$ 是[协变](@entry_id:634097)常数的，它所对应的线丛（典范丛）上的陈联络必须是平坦的，即其[曲率形式](@entry_id:199387)为零。然而，典范丛的[曲率形式](@entry_id:199387)（的第一陈形式）正比于[流形](@entry_id:153038)的 **[里奇形式](@entry_id:183612)** (Ricci form) $\rho$。因此，联络平坦意味着[里奇形式](@entry_id:183612)为零，$\rho=0$。由于[里奇形式](@entry_id:183612)与里奇张量通过 $\rho(X, Y) = \mathrm{Ric}(JX, Y)$ 相关联，且 $J$ 是非退化的，$\rho=0$ 蕴含了 $\mathrm{Ric}=0$。

因此，任何[超凯勒流形](@entry_id:159760)都是[里奇平坦](@entry_id:159097)的。这意味着它们自动成为爱因斯坦方程在真空中的解，这解释了它们在理论物理，特别是[弦论](@entry_id:145688)和[超引力](@entry_id:148689)理论中的核心地位。

### [扭量空间](@entry_id:159706)：[复结构](@entry_id:269128)的球面族

[超凯勒流形](@entry_id:159760)上的三个复结构 $I, J, K$ 并非是孤立的。事实上，它们构成了一个由二维球面 $S^2$ [参数化](@entry_id:272587)的复结构族的基底 [@problem_id:3030652]。

令 $(a, b, c)$ 为 $\mathbb{R}^3$ 中的单位向量，即 $a^2+b^2+c^2=1$。我们可以定义一个新的张量：
$$
I_{(a,b,c)} = aI + bJ + cK
$$
可以验证，$(I_{(a,b,c)})^2 = -\mathrm{Id}$，并且 $\nabla I_{(a,b,c)} = 0$。因此，对于 $S^2$ 上的每一点，我们都得到一个新的、与度量 $g$ 兼容的、协变常数的[复结构](@entry_id:269128)。这个由 $S^2$ [参数化](@entry_id:272587)的[复结构](@entry_id:269128)族是超[凯勒几何](@entry_id:160314)的核心特征。我们可以通过一个具体的计算来感受这一点。例如，在 $\mathbb{R}^4 \cong \mathbb{H}$ 上，给定参数 $(\theta_0, \phi_0)$，我们可以确定对应的复结构 $\mathcal{J}_{(\theta_0, \phi_0)}$，并计算其凯勒形式 $\omega_{\mathcal{J}}$ 在特定向量上的值 [@problem_id:970736]。

这一思想可以被提升到一个更深刻的构造，即 **[扭量空间](@entry_id:159706)** (twistor space) $\mathcal{Z}$。[扭量空间](@entry_id:159706)是一个复流形，它将[超凯勒流形](@entry_id:159760) $M$ 的整个超凯勒结构编码为其自身的[复几何](@entry_id:159080)性质。其构造如下：
1.  其底层的光滑流形是积空间 $Z = M \times \mathbb{P}^1$，其中[复射影直线](@entry_id:276948) $\mathbb{P}^1$ 同构于 $S^2$，参数化了上述的[复结构](@entry_id:269128)族。
2.  在 $Z$ 上定义一个[殆复结构](@entry_id:159849) $\mathcal{J}$。在切空间 $T_{(x,\lambda)}Z \cong T_xM \oplus T_\lambda\mathbb{P}^1$ 上，$\mathcal{J}$ 的定义为 $\mathcal{J}(v, \xi) = (I_\lambda v, i\xi)$，其中 $I_\lambda$ 是对应于点 $\lambda \in \mathbb{P}^1$ 的[复结构](@entry_id:269128)，而 $i$ 是 $\mathbb{P}^1$ 自身的标准[复结构](@entry_id:269128)。
3.  一个深刻的定理（Atiyah-Hitchin-Singer）指出，这个[殆复结构](@entry_id:159849) $\mathcal{J}$ 是可积的，当且仅当 $I, J, K$ 是[协变](@entry_id:634097)常数的。换言之，一个[流形](@entry_id:153038)是[超凯勒流形](@entry_id:159760)，当且仅当其[扭量空间](@entry_id:159706)是一个[复流形](@entry_id:159076)。

这样构造出的[复流形](@entry_id:159076) $\mathcal{Z}$ 带有一个到 $\mathbb{P}^1$ 的全纯投影 $\pi: \mathcal{Z} \to \mathbb{P}^1$。这个投影的纤维恰好是 $(M, I_\lambda)$。因此，超凯勒结构的存在等价于存在一个以 $\mathbb{P}^1$为底的复流形全纯纤维化，其所有纤维都与 $M$ [微分同胚](@entry_id:147249) [@problem_id:3030652]。

### 全纯辛观点

超[凯勒几何](@entry_id:160314)的另一个强大视角来自于将其视为 **全纯[辛几何](@entry_id:160783)** (holomorphic symplectic geometry)。

给定一个[超凯勒流形](@entry_id:159760) $(M, g, I, J, K)$，让我们“选择”一个[复结构](@entry_id:269128)，例如 $I$，并将 $(M, I)$ 视为一个复流形。然后我们可以研究另外两个结构 $J$ 和 $K$ 在这个复结构下的表现。我们定义一个复 valued 2-形式：
$$
\Omega = \omega_J + i \omega_K
$$
其中 $i$ 是复数单位。由于 $J$ 和 $K$ 都是协变常数的，可以证明 $\Omega$ 是一个关于[复结构](@entry_id:269128) $I$ 的 **全純 $(2,0)$-形式**。这意味着在任何局部全纯[坐标系](@entry_id:156346) $(z^1, \dots, z^{2n})$ 下，$\Omega$可以写成 $\Omega = \sum_{jk} f_{jk}(z) dz^j \wedge dz^k$，其中系数 $f_{jk}$是全纯函数。此外，$\Omega$ 是闭的并且非退化。这样一个[流形](@entry_id:153038) $(M, I, \Omega)$ 被称为 **全纯[辛流形](@entry_id:161608)**。

这个观点揭示了[超凯勒流形](@entry_id:159760)与[辛几何](@entry_id:160783)和[可积系统](@entry_id:144213)之间的深刻联系。一个重要的例子是复[欧几里得空间](@entry_id:138052)的[余切丛](@entry_id:185138) $T^*\mathbb{C}^n$ [@problem_id:970870]。在标准坐标 $(z^j, p_j)$ 下（其中 $z^j$ 是底空间坐标，$p_j$ 是纤维坐标），其全纯辛形式为：
$$
\Omega = \sum_{j=1}^n dp_j \wedge dz^j
$$
全纯辛形式 $\Omega$ 自然地定义了[全纯函数](@entry_id:158563)上的 **[泊松括号](@entry_id:151133)** (Poisson bracket)。对于任意两个[全纯函数](@entry_id:158563) $F, G$，它们的[泊松括号](@entry_id:151133)为：
$$
\{F, G\}_\Omega = \sum_{j=1}^n \left( \frac{\partial F}{\partial p_j} \frac{\partial G}{\partial z^j} - \frac{\partial F}{\partial z^j} \frac{\partial G}{\partial p_j} \right)
$$
这个结构使得我们可以应用[哈密顿力学](@entry_id:146202)的工具来研究[超凯勒流形](@entry_id:159760)的几何。例如，计算两个[哈密顿量](@entry_id:172864) $H_1 = \alpha z^2 - \beta p_1$ 和 $H_2 = \gamma z^1 + \delta p_2$ 的[泊松括号](@entry_id:151133)会得到一个常数 $-\alpha\delta-\beta\gamma$ [@problem_id:970870]，这反映了该几何结构的基本[交换关系](@entry_id:136780)。同样，在 $\mathbb{R}^4$ 上的计算也可以被诠释为[哈密顿系统](@entry_id:143533) [@problem_id:970821]。

### [构造原理](@entry_id:141667)：对称性与商空间

我们如何构造非平凡的[超凯勒流形](@entry_id:159760)？一个主要的方法是通过[对称性约化](@entry_id:199270)，称为 **超凯勒商构造** (hyperkähler quotient construction)，这是对[辛几何](@entry_id:160783)中 Marsden-Weinstein 商的推广。

这个构造的核心思想是 **三哈密顿作用** (tri-Hamiltonian action) [@problem_id:2980134]。一个[李群](@entry_id:137659) $G$ 在[超凯勒流形](@entry_id:159760) $(M, g, I, J, K)$ 上的作用如果是三哈密顿的，需要满足：
1.  该作用保持整个超凯勒结构，即它是一个保距、保复结构的作用。
2.  该作用对于三个辛形式 $\omega_I, \omega_J, \omega_K$ 中的每一个都是哈密顿的。

这意味着存在一个 **超凯勒动量矩** (hyperkähler moment map) $\mu: M \to \mathfrak{g}^* \otimes \mathbb{R}^3$，其中 $\mathfrak{g}^*$ 是 $G$ 的[李代数](@entry_id:137954)的[对偶空间](@entry_id:146945)。这个动量矩是一个三元组 $\mu = (\mu_I, \mu_J, \mu_K)$，其中每个分量 $\mu_A: M \to \mathfrak{g}^*$ 是对应于辛形式 $\omega_A$ 的标[准动量](@entry_id:143609)矩。它满足以下[方程组](@entry_id:193238)，对所有 $X \in \mathfrak{g}$ 成立：
$$
\iota_{X_M} \omega_I = d\langle \mu_I, X \rangle, \quad \iota_{X_M} \omega_J = d\langle \mu_J, X \rangle, \quad \iota_{X_M} \omega_K = d\langle \mu_K, X \rangle
$$
其中 $X_M$ 是由 $X$ 生成的基本向量场。此外，动量矩 $\mu$ 必须是 $G$-等变的，满足 $\mu(g \cdot p) = \mathrm{Ad}_g^* \mu(p)$，其中 $\mathrm{Ad}^*$ 是 $G$ 在 $\mathfrak{g}^* \otimes \mathbb{R}^3$ 上的协伴随作用。

超凯勒商 $M/\!/\!/G$ 定义为动量矩[水平集](@entry_id:751248) $\mu^{-1}(0)$ 对 $G$ 的作用的[商空间](@entry_id:274314)。在良好条件下，这个[商空间](@entry_id:274314)继承了一个新的超凯勒结构。

**Gibbons-Hawking ansatz** 是这个原理的一个著名应用，用于构造所有具有 tri-Hamiltonian $S^1$ 作用的四维[超凯勒流形](@entry_id:159760) [@problem_id:2968927]。在这种情况下，$G=S^1$，其[李代数](@entry_id:137954)和对偶都可以等同于 $\mathbb{R}$。动量矩是一个映射 $\mu: M^4 \to \mathbb{R}^3$。该映射的[水平集](@entry_id:751248)定义了一个三维空间 $U = M_0 / S^1$（在作用自由的稠密开集 $M_0$ 上）。度量的形式可以被完全确定为：
$$
g = V(\vec{x}) \sum_{i=1}^3 (dx^i)^2 + V(\vec{x})^{-1} (d\psi + \theta)^2
$$
其中 $\vec{x}=(x^1, x^2, x^3)$ 是 $U \subset \mathbb{R}^3$ 上的坐标（由动量矩给出），$\psi$ 是 $S^1$ 纤维上的坐标，$\theta$ 是 $S^1$ [主丛](@entry_id:160029)上的一个联络 [1-形式](@entry_id:270392)。超[凯勒条件](@entry_id:637291)最终归结为对函数 $V$ 和 1-形式 $\theta$ 的一组[微分方程](@entry_id:264184)：
1.  $V$ 必须是 $U$ 上的一个 **调和函数** (harmonic function)：$\Delta V = \sum_i \frac{\partial^2 V}{(\partial x^i)^2} = 0$。
2.  $\theta$ 的曲率 $d\theta$ 由 $V$ 的梯度决定：$d\theta = - \star_3 dV$，其中 $\star_3$ 是 $\mathbb{R}^3$ 上的[霍奇星算子](@entry_id:197539)。

这个 ansatz 提供了一个强大的机器来生成各种重要的超凯勒度量，例如多中心 Taub-NUT 度量和 ALE (Asymptotically Locally Euclidean) [引力瞬子](@entry_id:158147)。这些度量的[和乐群](@entry_id:191471)被确定为 $\mathrm{Sp}(1)$，其作为李群的维数为 3 [@problem_id:2968927]。这个构造完美地展示了对称性、[微分方程](@entry_id:264184)和特殊黎曼几何是如何在超凯勒理论中交织在一起的。