## 引言
在[微分几何](@entry_id:145818)与理论物理的宏伟画卷中，很少有哪个数学工具能像[拉普拉斯-德拉姆算子](@entry_id:267503) (Laplace-de Rham operator) 那样，扮演着如此核心且无处不在的角色。它是我们熟悉的[标量场](@entry_id:151443)拉普拉斯算子（∇²）在更广阔、更抽象的微分形式世界中的自然继承者。然而，简单地称其为“推广”远不足以概括其深刻意义。当我们将分析从平直的欧几里得空间拓展到弯曲的[黎曼流形](@entry_id:261160)时，我们面临一个核心问题：如何定义一个能够捕捉[流形](@entry_id:153038)内在几何与拓扑特性的“[二阶导数](@entry_id:144508)”？[拉普拉斯-德拉姆算子](@entry_id:267503)正是这个问题的完美答案，它如同一座桥梁，巧妙地连接了[流形](@entry_id:153038)的局部几何（如曲率）与全局拓扑（如“洞”的数量）。

本文将系统地引导你构建并理解这个强大的算子。在接下来的章节中，你将学习到：

*   **原理与机制**: 我们将从基本构件——[霍奇星算子](@entry_id:197539)和[余微分](@entry_id:197182)——出发，严格定义[拉普拉斯-德拉姆算子](@entry_id:267503)。你将看到它如何作用于不同阶的微分形式，并理解其与经典[拉普拉斯算子](@entry_id:146319)的本质联系。
*   **应用与跨学科联系**: 我们将走出纯数学的范畴，探索该算子如何在向量微积分、电磁学、[谱几何](@entry_id:186460)和[霍奇理论](@entry_id:161814)中大放异彩，揭示其作为统一性框架的强大威力。
*   **动手实践**: 通过一系列精心设计的计算练习，你将亲手运用这些理论，将抽象概念转化为具体的计算能力。

让我们首先深入其内部构造，从定义它的基本原理与机制开始。

## 原理与机制

继前一章对[微分形式](@entry_id:146747)和[外导数](@entry_id:161900) $d$ 的介绍之后，本章将深入探讨一个在现代几何学和物理学中无处不在的核心算子——[拉普拉斯-德拉姆算子](@entry_id:267503)（Laplace-de Rham operator）。我们将从其基本构成要素开始，系统地构建这个算子，并揭示其在不同阶[微分形式](@entry_id:146747)上的作用机制。通过具体的计算实例和对其基本性质的探讨，我们将理解它为何是经典拉普拉斯算子的自然推广。最终，我们将领略到这个算子如何成为连接[流形](@entry_id:153038)的局部几何（如曲率）与全局拓扑（如[贝蒂数](@entry_id:153109)）的深刻桥梁。

### [霍奇星算子](@entry_id:197539)与[余微分](@entry_id:197182)

[外导数](@entry_id:161900) $d$ 将一个 $p$-形式映射为一个 $(p+1)$-形式，即它提升了形式的阶数。一个自然的问题是：是否存在一个伴随的算子，能够沿着相反的方向，即降低形式的阶数？答案是肯定的，这个算子被称为**[余微分](@entry_id:197182)**（codifferential），记作 $\delta$。然而，为了严格定义 $\delta$，我们首先需要引入一个依赖于[流形](@entry_id:153038)度量结构和定向的辅助工具——**[霍奇星算子](@entry_id:197539)**（Hodge star operator）。

#### [霍奇星算子](@entry_id:197539)

在一个 $n$ 维定向[黎曼流形](@entry_id:261160) $(M, g)$上，[霍奇星算子](@entry_id:197539)（记为 $*$）是一个[线性映射](@entry_id:185132)，它将 $p$-形式的空间与 $(n-p)$-形式的空间联系起来。直观地，它将一个 $p$-形式 $\alpha$ 映射到其“[正交补](@entry_id:149922)”空间中的一个 $(n-p)$-形式 $*\alpha$。这个映射的精确定义依赖于[流形](@entry_id:153038)的[内积](@entry_id:158127)结构。

对于任意两个 $p$-形式 $\alpha$ 和 $\beta$，它们的[内积](@entry_id:158127)由下式给出：
$$ \alpha \wedge (*\beta) = \langle \alpha, \beta \rangle_g dV_g $$
其中 $dV_g$ 是[流形](@entry_id:153038)上的[黎曼体积形式](@entry_id:275973)，$\langle \alpha, \beta \rangle_g$ 是由度量 $g$ 诱导的逐点[内积](@entry_id:158127)。

在实际计算中，使用一组局部[标准正交基](@entry_id:147779)（orthonormal basis）会更方便。设 $\{e^1, \dots, e^n\}$ 是一组标准正交的1-形式基，满足定向条件 $e^1 \wedge \dots \wedge e^n = dV_g$。那么[霍奇星算子](@entry_id:197539)作用在基形式上的定义为：
$$ *(e^{i_1} \wedge \dots \wedge e^{i_p}) = \text{sgn}(\sigma) e^{j_1} \wedge \dots \wedge e^{j_{n-p}} $$
其中 $\{i_1, \dots, i_p, j_1, \dots, j_{n-p}\}$ 是 $\{1, \dots, n\}$ 的一个[排列](@entry_id:136432)，$\sigma$ 是这个[排列](@entry_id:136432)，$\text{sgn}(\sigma)$ 是其符号。

在非[笛卡尔坐标系](@entry_id:169789)下进行计算时，我们必须首先将[坐标基](@entry_id:270149)矢表达为[标准正交基](@entry_id:147779)矢。

**示例：球坐标系下的[霍奇星算子](@entry_id:197539) [@problem_id:1552781]**

考虑三维欧氏空间 $\mathbb{R}^3$，使用[球坐标](@entry_id:146054) $(r, \theta, \phi)$。其线元为 $ds^2 = dr^2 + r^2 d\theta^2 + r^2 \sin^2\theta d\phi^2$。一组相应的标准正交1-形式基为：
$$ \omega^1 = dr, \quad \omega^2 = r d\theta, \quad \omega^3 = r \sin\theta d\phi $$
根据定义，这些[基矢](@entry_id:199546)上的[霍奇星算子](@entry_id:197539)满足：
$$ *(\omega^1 \wedge \omega^2) = \omega^3, \quad *(\omega^2 \wedge \omega^3) = \omega^1, \quad *(\omega^3 \wedge \omega^1) = \omega^2 $$
现在，我们来计算[2-形式](@entry_id:188008) $\Omega = dr \wedge d\phi$ 的[霍奇对偶](@entry_id:263610)。首先，用标准正交基表示 $\Omega$：
$$ dr = \omega^1 $$
$$ d\phi = \frac{1}{r \sin\theta} \omega^3 $$
因此，
$$ \Omega = dr \wedge d\phi = \omega^1 \wedge \left(\frac{1}{r \sin\theta} \omega^3\right) = \frac{1}{r \sin\theta} (\omega^1 \wedge \omega^3) $$
利用[楔积](@entry_id:147029)的反对称性 $\omega^1 \wedge \omega^3 = -(\omega^3 \wedge \omega^1)$ 和[霍奇星算子](@entry_id:197539)的线性，我们得到：
$$ *\Omega = \frac{1}{r \sin\theta} *(\omega^1 \wedge \omega^3) = \frac{1}{r \sin\theta} \big( -*(\omega^3 \wedge \omega^1) \big) = \frac{1}{r \sin\theta} (-\omega^2) $$
最后，将 $\omega^2 = r d\theta$ 代回，得到最终结果：
$$ *\Omega = -\frac{r d\theta}{r \sin\theta} = -\frac{1}{\sin\theta} d\theta $$
这个例子清楚地表明，即使在熟悉的欧氏空间中，非[笛卡尔坐标系](@entry_id:169789)下的[霍奇星算子](@entry_id:197539)也可能产生与坐标相关的非平凡因子。

#### [余微分算子](@entry_id:191334) $\delta$

有了[霍奇星算子](@entry_id:197539)，我们便可以定义**[余微分](@entry_id:197182)** $\delta$。对于一个 $p$-形式 $\alpha$，其[余微分](@entry_id:197182) $\delta\alpha$ 是一个 $(p-1)$-形式，定义为：
$$ \delta\alpha = (-1)^{n(p+1)+1} *d*\alpha $$
其中 $n$ 是[流形](@entry_id:153038)的维数。这个算子是[外导数](@entry_id:161900) $d$ 在 $L^2$ [内积](@entry_id:158127)下的形式**伴随算子**（formal adjoint）。正如 $d^2 = d \circ d = 0$ 一样，可以证明 $\delta^2 = \delta \circ \delta = 0$。

在[局部坐标系](@entry_id:751394) $\{x^i\}$ 中，对于一个1-形式 $\omega = \sum_j \omega_j dx^j$，其[余微分](@entry_id:197182)是一个0-形式（即标量函数），可以由以下公式计算：
$$ \delta\omega = -\frac{1}{\sqrt{|g|}} \sum_{i=1}^{n} \frac{\partial}{\partial x^i}(\sqrt{|g|} \omega^i) $$
其中 $|g|$ 是度量张量矩阵 $g_{ij}$ 的[行列式](@entry_id:142978)，$\omega^i = \sum_j g^{ij} \omega_j$ 是 $\omega$ 的[逆变分量](@entry_id:185440)。

**示例：极坐标下的[余微分](@entry_id:197182) [@problem_id:1552757]**

考虑二维欧氏平面上的极坐标 $(r, \theta)$。度量张量为 $g_{rr}=1, g_{\theta\theta}=r^2$，其逆为 $g^{rr}=1, g^{\theta\theta}=r^{-2}$。度量[行列式](@entry_id:142978) $|g| = r^2$，因此 $\sqrt{|g|}=r$。

给定1-形式 $\omega = r\cos(\theta) dr + r^2\sin(\theta) d\theta$。其[协变](@entry_id:634097)分量为 $\omega_r = r\cos(\theta)$ 和 $\omega_\theta = r^2\sin(\theta)$。我们首先计算其[逆变分量](@entry_id:185440)：
$$ \omega^r = g^{rr}\omega_r = 1 \cdot r\cos(\theta) = r\cos(\theta) $$
$$ \omega^\theta = g^{\theta\theta}\omega_\theta = r^{-2} \cdot r^2\sin(\theta) = \sin(\theta) $$
现在，应用[余微分](@entry_id:197182)的坐标公式 ($n=2$)：
$$ \delta\omega = -\frac{1}{r} \left[ \frac{\partial}{\partial r}(r \omega^r) + \frac{\partial}{\partial \theta}(r \omega^\theta) \right] $$
代入 $\omega^r$ 和 $\omega^\theta$：
$$ \delta\omega = -\frac{1}{r} \left[ \frac{\partial}{\partial r}(r \cdot r\cos\theta) + \frac{\partial}{\partial \theta}(r \cdot \sin\theta) \right] = -\frac{1}{r} \left[ \frac{\partial}{\partial r}(r^2\cos\theta) + \frac{\partial}{\partial \theta}(r\sin\theta) \right] $$
求[偏导数](@entry_id:146280)：
$$ \delta\omega = -\frac{1}{r} [2r\cos\theta + r\cos\theta] = -\frac{1}{r}(3r\cos\theta) = -3\cos\theta $$
因此，1-形式 $\omega$ 的[余微分](@entry_id:197182)是标量函数 $-3\cos\theta$。

### [拉普拉斯-德拉姆算子](@entry_id:267503)的定义与作用

有了外导数 $d$ 和[余微分](@entry_id:197182) $\delta$，我们终于可以定义本章的主角：**[拉普拉斯-德拉姆算子](@entry_id:267503)** $\Delta$。它被定义为：
$$ \Delta = d\delta + \delta d $$
这个算子由一个降低阶数的部分($\delta d$)和一个提升阶数的部分($d\delta$)组合而成。然而，对于一个 $p$-形式 $\alpha$， $d\alpha$ 是 $(p+1)$-形式，$\delta(d\alpha)$ 又是 $p$-形式；类似地，$\delta\alpha$ 是 $(p-1)$-形式，$d(\delta\alpha)$ 又是 $p$-形式。因此，$\Delta$ 是一个保持形式阶数不变的算子，即它将 $p$-形式映射到 $p$-形式。

#### 在0-形式（标量场）上的作用

让我们考察 $\Delta$ 如何作用于一个0-形式，即一个光滑函数 $f$。根据定义，$\delta f = 0$，因为[余微分](@entry_id:197182)将阶数降低1，而没有负阶数的形式。因此，定义式简化为：
$$ \Delta f = \delta d f $$
这揭示了[拉普拉斯算子](@entry_id:146319)在标量场上的作用机制：首先通过[外导数](@entry_id:161900) $d$ 测量其梯度，然后通过[余微分](@entry_id:197182) $\delta$ 测量该梯度场的“散度”。

在 $n=2$ 维[欧氏空间](@entry_id:138052) $\mathbb{R}^2$ 的笛卡尔坐标 $(x, y)$ 中，我们有 $\delta = -*d*$ 作用于[1-形式](@entry_id:270392)。让我们计算 $\Delta f$ [@problem_id:1552759]。
首先，$df = \frac{\partial f}{\partial x}dx + \frac{\partial f}{\partial y}dy$。
然后，应用[霍奇星算子](@entry_id:197539)（在 $\mathbb{R}^2$ 中，$*dx=dy, *dy=-dx$）：
$$ *df = \frac{\partial f}{\partial x}(*dx) + \frac{\partial f}{\partial y}(*dy) = \frac{\partial f}{\partial x}dy - \frac{\partial f}{\partial y}dx $$
接着，取[外导数](@entry_id:161900)：
$$ d(*df) = d\left(\frac{\partial f}{\partial x}dy - \frac{\partial f}{\partial y}dx\right) = \frac{\partial^2 f}{\partial x^2} dx \wedge dy - \frac{\partial^2 f}{\partial y^2} dy \wedge dx = \left(\frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2}\right) dx \wedge dy $$
最后，应用 $\delta = -*d*$ 中的 $-*$ 部分（在 $\mathbb{R}^2$ 中，$*(dx \wedge dy)=1$）：
$$ \Delta f = \delta df = -*d(*df) = -\left(\frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2}\right) $$
这正是经典[拉普拉斯算子](@entry_id:146319) $\nabla^2 f = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2}$ 的负值！因此，在[欧氏空间](@entry_id:138052)的[笛卡尔坐标](@entry_id:167698)下，**[拉普拉斯-德拉姆算子](@entry_id:267503)在0-形式上的作用等价于负的经典拉普拉斯算子**。值得注意的是，符号约定在不同文献中可能有所不同，但 $\Delta f \propto \nabla^2 f$ 的关系是本质性的。算子的线性性质也直接继承自 $d$ 和 $\delta$ 的线性 [@problem_id:1552799]。

对于一般的黎曼流形，作用在0-形式上的[拉普拉斯-德拉姆算子](@entry_id:267503)被称为**[拉普拉斯-贝尔特拉米算子](@entry_id:267002)**（Laplace-Beltrami operator）。其在[局部坐标](@entry_id:181200) $\{x^i\}$ 中的表达式为：
$$ \Delta f = - \frac{1}{\sqrt{|g|}} \sum_{i,j} \frac{\partial}{\partial x^i} \left( \sqrt{|g|} g^{ij} \frac{\partial f}{\partial x^j} \right) $$
这个算子在物理学中无处不在，例如，在弯曲空间或[非均匀介质](@entry_id:750241)中的[静电学](@entry_id:140489)中，泊松方程写为 $\Delta V = \rho/\epsilon$ [@problem_id:1552794]。例如，在极坐标中，对于一个势函数 $V(r, \theta) = \alpha r^2$，利用上述公式可以计算出 $\Delta V = -4\alpha$，这意味着产生该[势场](@entry_id:143025)需要一个均匀的源密度。

#### 在高阶形式上的作用

当作用于 $p \ge 1$ 的形式时，$\Delta = d\delta + \delta d$ 的两个部分都可能贡献非零结果。让我们通过一个实例来分解这个过程。

**示例：在 $\mathbb{R}^3$ 中计算 $\Delta\omega$ [@problem_id:1552809]**

考虑三维欧氏空间 $\mathbb{R}^3$ 中的1-形式 $\omega = z^2 dy$。我们分别计算 $d\delta\omega$ 和 $\delta d\omega$。在 $\mathbb{R}^3$ [笛卡尔坐标](@entry_id:167698)中，对于[1-形式](@entry_id:270392) $\alpha = A dx + B dy + C dz$ 和[2-形式](@entry_id:188008) $\beta = P dy\wedge dz + Q dz\wedge dx + R dx\wedge dy$，我们有以下运算规则：
- $\delta \alpha = -(\frac{\partial A}{\partial x} + \frac{\partial B}{\partial y} + \frac{\partial C}{\partial z})$
- $d \alpha = (\frac{\partial C}{\partial y} - \frac{\partial B}{\partial z}) dy \wedge dz + (\dots)$
- $\delta \beta = (\frac{\partial R}{\partial y} - \frac{\partial Q}{\partial z})dx + (\frac{\partial P}{\partial z} - \frac{\partial R}{\partial x})dy + (\dots)$

1.  **计算 $d\delta\omega$**:
    对于 $\omega = z^2 dy$，我们有 $A=0, B=z^2, C=0$。
    $$ \delta\omega = -(\frac{\partial 0}{\partial x} + \frac{\partial(z^2)}{\partial y} + \frac{\partial 0}{\partial z}) = -(0+0+0) = 0 $$
    因此，$d\delta\omega = d(0) = 0$。

2.  **计算 $\delta d\omega$**:
    首先计算 $d\omega$：
    $$ d\omega = d(z^2 dy) = 2z \, dz \wedge dy = -2z \, dy \wedge dz $$
    这是一个2-形式。为了计算其[余微分](@entry_id:197182)，我们将其与标准形式 $\beta$ 比较，得到 $P=-2z, Q=0, R=0$。
    $$ \delta(d\omega) = \left(\frac{\partial(-2z)}{\partial z} - \frac{\partial 0}{\partial x}\right)dy + \dots = -2 dy $$

3.  **组合结果**:
    $$ \Delta\omega = d\delta\omega + \delta d\omega = 0 + (-2 dy) = -2 dy $$
这个例子清晰地表明，$\Delta$ 的两个组成部分——$d\delta$ 项和 $\delta d$ 项——都是不可或缺的，它们各自捕捉了形式在不同方面的变化。

### 基本性质与[谐波](@entry_id:181533)形式

[拉普拉斯-德拉姆算子](@entry_id:267503)拥有几个至关重要的性质，这些性质使其成为几何分析中的核心工具。

#### 与[外导数](@entry_id:161900)的[交换性](@entry_id:140240)

$\Delta$ 算子与[外导数](@entry_id:161900) $d$ 满足[交换律](@entry_id:141214)，即：
$$ \Delta d = d \Delta $$
证明如下：$\Delta d = (d\delta + \delta d)d = d\delta d + \delta d^2$。由于 $d^2 = 0$，我们有 $\Delta d = d\delta d$。另一方面，$d\Delta = d(d\delta + \delta d) = d^2\delta + d\delta d$。由于 $d^2=0$，我们有 $d\Delta = d\delta d$。因此，$\Delta d = d \Delta$。同样地，可以证明 $\Delta$ 也与 $\delta$ 交换。

这个性质意味着，如果一个形式是拉普拉斯算子的[特征形式](@entry_id:198300)，那么它的外导数和[余微分](@entry_id:197182)（如果非零）也是具有相同[特征值](@entry_id:154894)的[特征形式](@entry_id:198300)。这个性质可以通过直接计算来验证，例如对于0-形式 $f(x,y) = x^2 y^3$，我们可以分别计算 $\Delta(df)$ 和 $d(\Delta f)$，并验证它们相等 [@problem_id:1552771]。

#### 自伴随性

在紧致无边[流形](@entry_id:153038)上，可以为微分形式定义一个全局 $L^2$ [内积](@entry_id:158127)：
$$ \langle \alpha, \beta \rangle = \int_M \alpha \wedge *\beta $$
在此[内积](@entry_id:158127)下，[余微分](@entry_id:197182) $\delta$ 是外导数 $d$ 的**形式伴随算子**，即对于任何 $p$-形式 $\alpha$ 和 $(p+1)$-形式 $\beta$，都有：
$$ \langle d\alpha, \beta \rangle = \langle \alpha, \delta\beta \rangle $$
利用这个关系，我们可以证明 $\Delta$ 是自伴随的（self-adjoint）：
$$ \langle \Delta\alpha, \beta \rangle = \langle (d\delta+\delta d)\alpha, \beta \rangle = \langle \delta\alpha, \delta\beta \rangle + \langle d\alpha, d\beta \rangle $$
由于右侧表达式对于 $\alpha$ 和 $\beta$ 是对称的，我们立即得到 $\langle \Delta\alpha, \beta \rangle = \langle \alpha, \Delta\beta \rangle$。这一性质是[拉普拉斯算子](@entry_id:146319)谱理论的基础，保证了其[特征值](@entry_id:154894)是实数，且不同[特征值](@entry_id:154894)的[特征形式](@entry_id:198300)是正交的 [@problem_id:1552772]。

#### [谐波](@entry_id:181533)形式

一个微分形式 $\omega$ 如果满足 $\Delta\omega = 0$，则被称为**谐波形式**（harmonic form）。这个概念是经典[调和函数](@entry_id:746864)（即满足 $\nabla^2 f = 0$ 的函数）的直接推广。

从 $\Delta$ 的自伴随性和[正定性](@entry_id:149643)（$\langle \Delta\alpha, \alpha \rangle = \langle d\alpha, d\alpha \rangle + \langle \delta\alpha, \delta\alpha \rangle \ge 0$）可以推断，在紧致无边[流形](@entry_id:153038)上，一个形式是谐波的当且仅当它同时是闭形式（$d\omega=0$）和余闭形式（$\delta\omega=0$）。

那么，在给定的空间上，哪些形式是[谐波](@entry_id:181533)的呢？

**示例：$\mathbb{R}^2$ 中的[谐波](@entry_id:181533)1-形式 [@problem_id:1552776]**

考虑欧氏平面 $\mathbb{R}^2$ 上的1-形式 $\omega = f(x)dx + g(y)dy$，其中 $f, g$ 是二次[可微函数](@entry_id:144590)。在[笛卡尔坐标](@entry_id:167698)下，对[1-形式](@entry_id:270392) $\alpha = P dx + Q dy$ 的[拉普拉斯算子](@entry_id:146319)作用为：
$$ \Delta \alpha = -(\nabla^2 P)dx - (\nabla^2 Q)dy $$
对于我们的 $\omega$，有 $P(x,y)=f(x)$ 和 $Q(x,y)=g(y)$。因此：
$$ \nabla^2 P = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2} = f''(x) $$
$$ \nabla^2 Q = \frac{\partial^2 g}{\partial x^2} + \frac{\partial^2 g}{\partial y^2} = g''(y) $$
$\omega$ 是谐波的条件是 $\Delta\omega = 0$，即：
$$ -f''(x) dx - g''(y) dy = 0 $$
由于 $dx$ 和 $dy$ 是线性无关的，这要求它们的系数必须恒为零，即 $f''(x)=0$ 和 $g''(y)=0$。对这两个常微分方程积分两次，我们得到 $f(x)$ 和 $g(y)$ 必须是线性函数：
$$ f(x) = c_1 x + c_2, \quad g(y) = d_1 y + d_2 $$
其中 $c_1, c_2, d_1, d_2$ 是任意实常数。

### 几何意义：[霍奇理论](@entry_id:161814)与魏岑伯克公式

[谐波](@entry_id:181533)形式的重要性远远超出了上述分析。[霍奇理论](@entry_id:161814)（Hodge theory）是20世纪数学的里程碑之一，它揭示了谐波形式与[流形](@entry_id:153038)拓扑之间的深刻联系。其核心结论是：在任何紧致定向黎曼流形上，每个[德拉姆上同调](@entry_id:158673)类都包含一个唯一的[谐波](@entry_id:181533)代表。这意味着，通过研究[流形](@entry_id:153038)上[谐波](@entry_id:181533)形式的性质，我们可以获得其拓扑不变量的信息。具体来说，第 $p$ 个[贝蒂数](@entry_id:153109) $b_p(M)$（描述[流形](@entry_id:153038)中“$p$ 维洞”的数量）等于该[流形](@entry_id:153038)上[线性无关](@entry_id:148207)的谐波 $p$-形式的数量。

拉普拉斯算子不仅与[拓扑相](@entry_id:141674)关，还与[流形](@entry_id:153038)的局部几何（即曲率）紧密相连。这种联系通过**魏岑伯克恒等式**（Weitzenböck identity）得以体现。对于[1-形式](@entry_id:270392)，该恒等式为：
$$ \Delta \omega = \nabla^* \nabla \omega + \mathrm{Ric}(\omega^\sharp, \cdot)^\flat $$
这里，$\nabla$ 是[列维-奇维塔联络](@entry_id:161107)，$\nabla^*\nabla$ 是作用于1-形式的**[博赫纳拉普拉斯算子](@entry_id:204681)**（Bochner Laplacian），$\omega^\sharp$ 是与 $\omega$ 对偶的向量场，$\mathrm{Ric}$ 是[里奇曲率张量](@entry_id:271424)。

这个公式威力巨大。让我们用它来证明一个经典定理（博赫纳消失定理）。假设 $(M, g)$ 是一个[里奇曲率](@entry_id:162038)严格为正（即对任意非零向量场 $X$，$\mathrm{Ric}(X, X) > 0$）的紧致定向[黎曼流形](@entry_id:261160)。设 $\omega$ 是其上的一个谐波1-形式，即 $\Delta\omega=0$。

我们将魏岑伯克恒等式与 $\omega$ 作[内积](@entry_id:158127)并在整个[流形](@entry_id:153038)上积分 [@problem_id:1552786]：
$$ \int_M \langle \Delta\omega, \omega \rangle dV_g = \int_M \langle \nabla^*\nabla\omega, \omega \rangle dV_g + \int_M \mathrm{Ric}(\omega^\sharp, \omega^\sharp) dV_g $$
由于 $\omega$ 是谐波的，左边为0。通过[分部积分](@entry_id:136350)（[格林公式](@entry_id:173118)），第一项可以写为 $\int_M |\nabla\omega|^2 dV_g$，其中 $|\nabla\omega|^2$ 是 $\omega$ 的[协变导数](@entry_id:152476)的范数平方，这是一个非负的量。因此，我们得到：
$$ 0 = \int_M |\nabla\omega|^2 dV_g + \int_M \mathrm{Ric}(\omega^\sharp, \omega^\sharp) dV_g $$
被积函数的两项都是逐点非负的。由于[流形](@entry_id:153038)的[里奇曲率](@entry_id:162038)严格为正，第二项 $\mathrm{Ric}(\omega^\sharp, \omega^\sharp)$ 只有在 $\omega^\sharp=0$（即 $\omega=0$）时才为零。要使整个积分为零，被积函数必须处处为零。这迫使 $|\nabla\omega|^2 = 0$ 并且 $\mathrm{Ric}(\omega^\sharp, \omega^\sharp) = 0$。后者意味着 $\omega$ 必须是零形式。

这个结果表明，一个具有严格[正里奇曲率](@entry_id:199145)的紧致流形不能拥有任何非平凡的[谐波](@entry_id:181533)1-形式。根据[霍奇理论](@entry_id:161814)，这意味着它的第一个[贝蒂数](@entry_id:153109) $b_1(M)$ 必须为0。这是一个连接几何（正曲率）与拓扑（无1维洞）的深刻结论，完美地展示了[拉普拉斯-德拉姆算子](@entry_id:267503)作为分析、几何与拓扑之间桥梁的强大力量。