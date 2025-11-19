## 引言
在探索弯曲空间的几何学时，一个核心问题随之出现：当一个几何对象（子流形）存在于另一个更高维度的空间（背景空间）中时，我们如何独立地描述它自身的几何特性？例如，地球表面作为三维空间中的一个[二维球面](@entry_id:269890)，其上的距离和角度是如何被定义的？解答这一问题的关键在于“[诱导度规](@entry_id:160616)”这一强大工具，它允许我们从背景空间的几何结构中“继承”并定义子流形的内蕴几何。本文旨在填补从抽象[流形](@entry_id:153038)概念到具体几何计算之间的知识鸿沟，为读者提供一个清晰、系统的框架来理解和应用[诱导度规](@entry_id:160616)。

本文将分为三个章节，引导读者逐步掌握这一核心概念。在“原理与机制”一章中，我们将建立[诱导度规](@entry_id:160616)的数学基础，通过“[拉回](@entry_id:160816)”操作从背景空间度规推导出[子流形](@entry_id:159439)度规，并通过直线、平面、[抛物面](@entry_id:264713)等直观例子来阐明其计算方法。接下来，“应用与跨学科联系”一章将展示[诱导度规](@entry_id:160616)的巨大威力，我们将看到它如何成为描述经典力学系统、分析相对论时空、乃至在[信息几何](@entry_id:141183)等前沿领域中构建理论的基石。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识转化为解决实际几何问题的能力。通过这一系列学习，你将不仅掌握一个数学工具，更将获得一种用几何语言思考和建模复杂系统的全新视角。

## 原理与机制

在本章中，我们将深入探讨子流形及其[诱导度规](@entry_id:160616)的核心原理与机制。在上一章的介绍之后，我们已经提及了[流形](@entry_id:153038)作为几何对象的抽象概念。现在，我们将研究一个更为具体和实践性的问题：当一个[流形](@entry_id:153038)（[子流形](@entry_id:159439)）嵌入到另一个更高维度的[流形](@entry_id:153038)（背景空间）中时，我们如何描述子流形自身的内蕴几何？答案在于**[诱导度规](@entry_id:160616) (induced metric)** 的概念，它允许我们利用背景空间的度量结构来定义[子流形](@entry_id:159439)上的距离、角度和体积。

### [诱导度规](@entry_id:160616)：从背景空间到子流形的几何“[拉回](@entry_id:160816)”

想象一个光滑的 $n$ 维子流形 $\mathcal{M}$ 嵌入在一个 $m$ 维的背景[流形](@entry_id:153038) $\mathcal{B}$ 中，其中 $n \lt m$。背景[流形](@entry_id:153038) $\mathcal{B}$ 上有一个度规张量 $g_{\mu\nu}$，它定义了 $\mathcal{B}$ 中点与点之间的无穷小距离平方关系 $ds^2 = g_{\mu\nu} dx^\mu dx^\nu$，其中 $x^\mu$ 是 $\mathcal{B}$ 上的坐标。我们的目标是为子流形 $\mathcal{M}$ 找到一个[度规张量](@entry_id:160222) $\gamma_{\alpha\beta}$，使其能够完全描述 $\mathcal{M}$ 上的[内蕴几何](@entry_id:158788)。

实现这一目标的标准方法是利用**[参数化](@entry_id:272587) (parameterization)**。我们可以用一组 $n$ 个坐标 $u^\alpha$ ($\alpha = 1, \dots, n$) 来描述子流形 $\mathcal{M}$ 上的任意点。这意味着存在一个映射关系 $x^\mu = x^\mu(u^1, u^2, \dots, u^n)$，它将 $\mathcal{M}$ 上的坐标 $u^\alpha$ 映射到背景空间 $\mathcal{B}$ 中的坐标 $x^\mu$。

在坐标 $u^\alpha$ 下，子流形上的[无穷小位移](@entry_id:202209)可以表示为切向量 $\frac{\partial x^\mu}{\partial u^\alpha} du^\alpha$。这个向量位于背景空间的[切空间](@entry_id:199137)中。我们可以使用背景空间的度规 $g_{\mu\nu}$ 来计算这些[切向量](@entry_id:265494)之间的[内积](@entry_id:158127)。子流形 $\mathcal{M}$ 上的**[诱导度规](@entry_id:160616)** $\gamma_{\alpha\beta}$ 正是这样定义的，它是背景度规 $g_{\mu\nu}$ 通过嵌入映射 $x^\mu(u^\alpha)$ 在子流形上的**[拉回](@entry_id:160816) (pullback)**：

$$
\gamma_{\alpha\beta}(u) = g_{\mu\nu}(x(u)) \frac{\partial x^\mu}{\partial u^\alpha} \frac{\partial x^\nu}{\partial u^\beta}
$$

这个公式是本章的核心。它告诉我们，要计算子流形上[坐标系](@entry_id:156346) $u$ 的度规分量 $\gamma_{\alpha\beta}$，我们只需取对应于该[坐标系](@entry_id:156346)的两个基[切向量](@entry_id:265494) $\mathbf{e}_\alpha = \frac{\partial \mathbf{x}}{\partial u^\alpha}$ 和 $\mathbf{e}_\beta = \frac{\partial \mathbf{x}}{\partial u^\beta}$，然后在背景空间中计算它们的[内积](@entry_id:158127)。因此，[诱导度规](@entry_id:160616)继承了背景空间的几何结构，但将其“限制”在了子流形的[切空间](@entry_id:199137)上。

### 欧几里得空间中的[子流形](@entry_id:159439)：[第一基本形式](@entry_id:274022)

最常见也是最直观的情况，是将子[流形嵌入](@entry_id:159781)到[欧几里得空间](@entry_id:138052) $\mathbb{R}^m$ 中。在标准的笛卡尔坐标系下，[欧几里得空间](@entry_id:138052)的[度规张量](@entry_id:160222)是单位矩阵，即 $g_{ij} = \delta_{ij}$（其中 $i,j$ 从 $1$ 到 $m$）。在这种情况下，[拉回](@entry_id:160816)公式变得异常简洁。

如果我们用位置向量 $\mathbf{r}(u^\alpha)$ 来描述[子流形](@entry_id:159439)，那么基切向量就是 $\frac{\partial \mathbf{r}}{\partial u^\alpha}$。[诱导度规](@entry_id:160616)的分量就简化为这些切向量的标准欧几里得[点积](@entry_id:149019)：

$$
\gamma_{\alpha\beta} = \frac{\partial \mathbf{r}}{\partial u^\alpha} \cdot \frac{\partial \mathbf{r}}{\partial u^\beta}
$$

在经典微分几何中，对于嵌入在 $\mathbb{R}^3$ 中的二维[曲面](@entry_id:267450)，这个度规张量 $\gamma_{ij}$ 通常被称为**[第一基本形式](@entry_id:274022) (first fundamental form)**，记作 $g_{ij}$。它捕捉了[曲面](@entry_id:267450)的所有[内蕴几何](@entry_id:158788)信息。

让我们通过几个例子来建立直观理解。

**一维[子流形](@entry_id:159439)：曲线**

最简单的[子流形](@entry_id:159439)是一条曲线。考虑连接 $\mathbb{R}^3$ 中两点 $\mathbf{p}_1 = (x_1, y_1, z_1)$ 和 $\mathbf{p}_2 = (x_2, y_2, z_2)$ 的一条直线段。我们可以用参数 $t \in [0, 1]$ 来参数化这条曲线：$\mathbf{r}(t) = (1-t)\mathbf{p}_1 + t\mathbf{p}_2$ [@problem_id:1540347]。这里，子流形坐标只有一个，即 $u^1 = t$。
[切向量](@entry_id:265494)是 $\frac{d\mathbf{r}}{dt} = \mathbf{p}_2 - \mathbf{p}_1 = (x_2-x_1, y_2-y_1, z_2-z_1)$，它是一个常向量。
[诱导度规](@entry_id:160616)只有一个分量 $g_{tt}$：

$$
g_{tt} = \frac{d\mathbf{r}}{dt} \cdot \frac{d\mathbf{r}}{dt} = |\mathbf{p}_2 - \mathbf{p}_1|^2 = (x_2-x_1)^2 + (y_2-y_1)^2 + (z_2-z_1)^2
$$

这个结果表明，对于此[参数化](@entry_id:272587)，度规分量是一个常数，它等于方向向量的长度平方。这反映了参数 $t$ 沿着直线均匀变化的事实。

**二维[子流形](@entry_id:159439)：[曲面](@entry_id:267450)**

对于二维[曲面](@entry_id:267450)，情况变得更加丰富。首先考虑一个最简单的情形：一个穿过 $\mathbb{R}^3$ 原点的平面。假设该平面由两个非共线向量 $\mathbf{v}_1 = (1, 2, 0)$ 和 $\mathbf{v}_2 = (0, 1, -1)$ 张成。我们可以用坐标 $(u^1, u^2)$ 来[参数化](@entry_id:272587)这个平面上的任意点 $\mathbf{P}$：$\mathbf{P}(u^1, u^2) = u^1 \mathbf{v}_1 + u^2 \mathbf{v}_2$ [@problem_id:1540324]。

这里的基切向量就是这两个常向量：$\frac{\partial \mathbf{P}}{\partial u^1} = \mathbf{v}_1$ 和 $\frac{\partial \mathbf{P}}{\partial u^2} = \mathbf{v}_2$。
[诱导度规](@entry_id:160616)的四个分量 $g_{ij}$ ($i,j \in \{1,2\}$) 是：
$g_{11} = \mathbf{v}_1 \cdot \mathbf{v}_1 = 1^2 + 2^2 + 0^2 = 5$
$g_{12} = g_{21} = \mathbf{v}_1 \cdot \mathbf{v}_2 = 1 \cdot 0 + 2 \cdot 1 + 0 \cdot (-1) = 2$
$g_{22} = \mathbf{v}_2 \cdot \mathbf{v}_2 = 0^2 + 1^2 + (-1)^2 = 2$

因此，度规矩阵为 $\begin{psmallmatrix} 5  2 \\ 2  2 \end{psmallmatrix}$。这个例子揭示了一个关键点：即使[曲面](@entry_id:267450)是平坦的（没有内蕴曲率），如果选取的[坐标系](@entry_id:156346)不是正交的（即 $\mathbf{v}_1 \cdot \mathbf{v}_2 \neq 0$），[诱导度规](@entry_id:160616)也会出现非对角项。度规不仅编码了[曲面](@entry_id:267450)的弯曲程度，还编码了所选[坐标系](@entry_id:156346)的几何特性。

现在我们转向真正的弯曲[曲面](@entry_id:267450)。考虑一个由方程 $z = k(x^2+y^2)$ 定义的旋转[抛物面](@entry_id:264713)，其中 $k0$ [@problem_id:1540376]。我们可以用极[坐标系](@entry_id:156346)的变种 $(\rho, \phi)$ 来[参数化](@entry_id:272587)它：$\mathbf{r}(\rho, \phi) = (\rho \cos\phi, \rho \sin\phi, k\rho^2)$。
基切向量为：
$\mathbf{r}_\rho = \frac{\partial\mathbf{r}}{\partial\rho} = (\cos\phi, \sin\phi, 2k\rho)$
$\mathbf{r}_\phi = \frac{\partial\mathbf{r}}{\partial\phi} = (-\rho\sin\phi, \rho\cos\phi, 0)$

计算[点积](@entry_id:149019)得到度规分量：
$g_{\rho\rho} = \mathbf{r}_\rho \cdot \mathbf{r}_\rho = \cos^2\phi + \sin^2\phi + (2k\rho)^2 = 1 + 4k^2\rho^2$
$g_{\rho\phi} = \mathbf{r}_\rho \cdot \mathbf{r}_\phi = 0$
$g_{\phi\phi} = \mathbf{r}_\phi \cdot \mathbf{r}_\phi = \rho^2\sin^2\phi + \rho^2\cos^2\phi = \rho^2$

度规矩阵为 $\begin{psmallmatrix} 1+4k^2\rho^2  0 \\ 0  \rho^2 \end{psmallmatrix}$。与平面不同，这里的度规分量 $g_{\rho\rho}$ 依赖于坐标 $\rho$。这正是[曲面](@entry_id:267450)内蕴曲率的体现：在离原点越远的地方，$\rho$ 方向的尺度被拉伸得越厉害。

类似地，我们可以计算各种[旋转曲面](@entry_id:261378)的度规。一个更一般的模型是旋转一条曲线 $x=f(z)$ 绕 $z$ 轴生成的[曲面](@entry_id:267450)，例如用于设计喇叭天线的[指数函数](@entry_id:161417)曲线 $x = R_0 \exp(\alpha z)$ [@problem_id:1540349]。使用[柱坐标](@entry_id:271645) $(z, \phi)$，参数化为 $\mathbf{X}(\phi, z) = (f(z)\cos\phi, f(z)\sin\phi, z)$。可以推导出，其[诱导度规](@entry_id:160616)总是对角的：
$g_{\phi\phi} = f(z)^2$
$g_{zz} = 1 + [f'(z)]^2$
$g_{\phi z} = 0$
这个通用形式涵盖了圆柱（$f(z)$ 为常数）、圆锥（$f(z)$ 为线性函数）以及上面提到的[抛物面](@entry_id:264713)等多种情况。

### [内蕴几何](@entry_id:158788)及其应用

[诱导度规](@entry_id:160616)的强大之处在于，一旦我们计算出它，就可以完全在[子流形](@entry_id:159439)的[坐标系](@entry_id:156346)内进行所有几何测量，而无需再回到背景空间。这就是所谓的**[内蕴几何](@entry_id:158788) (intrinsic geometry)**。

**[弧长](@entry_id:191173)与重参数化**

[子流形](@entry_id:159439)上一条由 $\lambda$ [参数化](@entry_id:272587)的曲线 $u^\alpha(\lambda)$ 的长度 $L$ 可以通过积分无穷小[弧长](@entry_id:191173)元 $ds$ 来计算：
$ds^2 = \gamma_{\alpha\beta} du^\alpha du^\beta = \gamma_{\alpha\beta} \frac{du^\alpha}{d\lambda} \frac{du^\beta}{d\lambda} d\lambda^2$
$L = \int \sqrt{\gamma_{\alpha\beta} \frac{du^\alpha}{d\lambda} \frac{du^\beta}{d\lambda}} d\lambda$

一个特别重要的参数化是**[弧长参数化](@entry_id:634139) (arc length parameterization)**。如果参数 $s$ 本身就是从起点算起的[弧长](@entry_id:191173)，那么我们期望 $ds^2 = (ds)^2$，这意味着对于[弧长](@entry_id:191173)参数 $s$，其[诱导度规](@entry_id:160616)分量恒为1。

让我们通过一个例子来阐明这一点 [@problem_id:1540300]。考虑一个粒子在半径为 $R$ 的球面（度规为 $ds^2 = R^2 d\theta^2 + R^2 \sin^2\theta d\phi^2$）上运动，其轨迹为 $\theta(\lambda) = \pi/3, \phi(\lambda) = \beta \lambda^2$。这条轨迹是一维子流形。其[诱导度规](@entry_id:160616) $h_{\lambda\lambda}$ 通过[拉回](@entry_id:160816)球面度规得到：
$h_{\lambda\lambda} = R^2 (\frac{d\theta}{d\lambda})^2 + R^2 \sin^2\theta (\frac{d\phi}{d\lambda})^2 = 0 + R^2 \sin^2(\pi/3) (2\beta\lambda)^2 = 3 R^2 \beta^2 \lambda^2$

现在，如果我们将这条路径用其自身的弧长 $s$ 来重新参数化，那么根据定义，弧长参数下的[诱导度规](@entry_id:160616) $h_{ss}$ 必须为 1。这是因为 $ds^2 = h_{ss} (ds)^2$ 蕴含了 $h_{ss}=1$。这个看似平凡的结论非常深刻：弧长是描述曲线最“自然”的内蕴坐标，它消除了任何由于[参数化](@entry_id:272587)选择带来的拉伸或压缩。

**面积与度规[行列式](@entry_id:142978)**

对于一个二维[曲面](@entry_id:267450)，其面积元 $dA$ 与[诱导度规](@entry_id:160616)的[行列式](@entry_id:142978) $\det(\gamma)$ 直接相关。在坐标 $(u^1, u^2)$ 下，面积元为：
$dA = \sqrt{\det(\gamma)} du^1 du^2$

这个关系式揭示了 $\det(\gamma)$ 的几何意义。它衡量了从平面上的 $(u^1, u^2)$ 坐标网格到[曲面](@entry_id:267450)上实际区域的面积扭曲程度。如果 $\det(\gamma)=1$，则意味着参数化映射是**保面积 (area-preserving)** 的；坐标平面上的任何区域的面积都等于其在[曲面](@entry_id:267450)上的像的面积 [@problem_id:1540307]。如果 $\det(\gamma)  1$，面积被放大；如果 $\det(\gamma) \lt 1$，面积被缩小。

我们可以利用这个公式来计算复杂[曲面](@entry_id:267450)的总面积。例如，一个主半径为 $R$、管半径为 $r$ 的环面，常用于描述[托卡马克聚变](@entry_id:756037)反应堆的真空室 [@problem_id:1540328]。其[参数化](@entry_id:272587)为 $\mathbf{x}(\theta, \phi) = ((R + r \cos\theta)\cos\phi, (R + r \cos\theta)\sin\phi, r \sin\theta)$。
通过计算，我们得到其[诱导度规](@entry_id:160616)为对角矩阵：
$$g = \begin{pmatrix} r^2  0 \\ 0  (R + r \cos\theta)^2 \end{pmatrix}$$
其[行列式](@entry_id:142978)为 $\det(g) = r^2(R+r\cos\theta)^2$。由于 $Rr$，$\sqrt{\det(g)} = r(R+r\cos\theta)$。
总面积 $A$ 就是对[面积元](@entry_id:263205)在整个参数域上积分：
$A = \int_0^{2\pi} \int_0^{2\pi} r(R + r \cos\theta) d\theta d\phi = (2\pi) \int_0^{2\pi} (rR + r^2\cos\theta) d\theta = (2\pi)(2\pi rR) = 4\pi^2 rR$
这是一个从参数化出发，通过[诱导度规](@entry_id:160616)计算宏观几何量的完整范例。

### 高等主题与推广

到目前为止，我们主要关注嵌入在[欧几里得空间](@entry_id:138052)中的[子流形](@entry_id:159439)。然而，[诱导度规](@entry_id:160616)的框架远比这更为普适和强大。

**复杂的[参数化](@entry_id:272587)：球极投影**

参数化的选择会极大地影响度规的具体形式。一个经典例子是半径为 $R$ 的球面通过**球极投影 (stereographic projection)** 映射到平面上 [@problem_id:1540321]。从北极点 $(0,0,R)$ 出发，将球面上除北极点外的任意一点 $P$ 与赤道平面 $z=0$ 相连，交点坐标为 $(u,v)$。这个复杂的[参数化](@entry_id:272587) $\mathbf{r}(u,v)$ 经过计算后，会得到一个对角化的[诱导度规](@entry_id:160616)：
$g_{uu} = g_{vv} = \frac{4R^4}{(u^2+v^2+R^2)^2}$，且 $g_{uv}=0$。
这个度规可以写成 $g_{ij} = \lambda(u,v) \delta_{ij}$ 的形式，其中 $\lambda(u,v)$ 是一个只依赖于位置的缩放因子。这种形式的度规被称为**[共形平坦](@entry_id:260902)的 (conformally flat)**。这意味着球极投影在局部上保持角度不变，但会改变长度和面积。该度规的[行列式](@entry_id:142978)为 $\det(g) = \frac{16 R^{8}}{(u^{2}+v^{2}+R^{2})^{4}}$，它清晰地显示了远离原点的区域面积被极大地压缩了。

**非欧几里得背景空间**

现在我们回到最一般的[拉回](@entry_id:160816)公式 $\gamma_{\alpha\beta} = g_{\mu\nu} \frac{\partial x^\mu}{\partial u^\alpha} \frac{\partial x^\nu}{\partial u^\beta}$，并考虑背景度规 $g_{\mu\nu}$ 本身不平凡的情况。

假设背景空间是一个度规为 $ds^2 = (1+z^2)(dx^2+dy^2+dz^2)$ 的三维空间。这是一个非[欧几里得空间](@entry_id:138052)，其几何结构随 $z$ 坐标变化。我们现在将一个半径为 $R$ 的竖直圆柱面 $\mathcal{S}$ 嵌入其中 [@problem_id:1540339]。圆柱面的参数化为 $x = R\cos\theta, y = R\sin\theta, z=z$。
背景度规在[笛卡尔坐标](@entry_id:167698)下为 $g_{ij} = (1+z^2)\delta_{ij}$。
基切向量为 $\frac{\partial\mathbf{x}}{\partial\theta} = (-R\sin\theta, R\cos\theta, 0)$ 和 $\frac{\partial\mathbf{x}}{\partial z} = (0,0,1)$。
[诱导度规](@entry_id:160616) $\gamma_{\alpha\beta}$ 的计算必须使用完整的[拉回](@entry_id:160816)公式：
$\gamma_{\theta\theta} = g_{ij} \frac{\partial x^i}{\partial\theta} \frac{\partial x^j}{\partial\theta} = (1+z^2) ((-R\sin\theta)^2 + (R\cos\theta)^2) = (1+z^2)R^2$
$\gamma_{zz} = g_{ij} \frac{\partial x^i}{\partial z} \frac{\partial x^j}{\partial z} = (1+z^2)(1^2) = 1+z^2$
$\gamma_{\theta z} = 0$
[诱导度规](@entry_id:160616)为 $\begin{psmallmatrix} (1+z^2)R^2  0 \\ 0  1+z^2 \end{psmallmatrix}$。我们看到，背景空间的[共形因子](@entry_id:267682) $(1+z^2)$ 被“遗传”给了子流形，直接影响了其内蕴几何。

**[伪黎曼几何](@entry_id:194600)：[闵可夫斯基时空](@entry_id:156421)中的[光锥](@entry_id:158105)**

[诱导度规](@entry_id:160616)的概念还可以推广到符号不定的度规，即[伪黎曼几何](@entry_id:194600)中。一个至关重要的例子来自[狭义相对论](@entry_id:275552)。在(3+1)维闵可夫斯基时空中，度规为 $\eta_{\mu\nu} = \mathrm{diag}(-1, 1, 1, 1)$。

考虑未来的**光锥 (light cone)**，它是由从原点发出的光线轨迹构成的三维[子流形](@entry_id:159439)，满足方程 $(x^1)^2+(x^2)^2+(x^3)^2 = (x^0)^2$ 且 $x^00$ [@problem_id:1540370]。我们可以用[球坐标](@entry_id:146054) $(r, \theta, \phi)$ 来参数化这个光锥，其中 $r$ 是空间径向距离，嵌入映射为 $x^0=r, x^1=r\sin\theta\cos\phi, \dots$。
使用[拉回](@entry_id:160816)公式计算[诱导度规](@entry_id:160616) $g_{ab}$ 时，我们会发现一个惊人的特性。例如，计算 $g_{rr}$：
$g_{rr} = \eta_{\mu\nu} \frac{\partial x^\mu}{\partial r} \frac{\partial x^\nu}{\partial r} = -(\frac{\partial x^0}{\partial r})^2 + (\frac{\partial x^1}{\partial r})^2 + (\frac{\partial x^2}{\partial r})^2 + (\frac{\partial x^3}{\partial r})^2$
$g_{rr} = -(1)^2 + (\sin^2\theta\cos^2\phi + \sin^2\theta\sin^2\phi + \cos^2\theta) = -1 + 1 = 0$
[诱导度规](@entry_id:160616)的一个对角分量为零！这意味着整个度规[矩阵的行列式](@entry_id:148198)为零，$\det(g)=0$。这种度规被称为**退化的 (degenerate)**。
这并非计算错误，而是**零性[曲面](@entry_id:267450) (null surfaces)** 的一个基本特征。$g_{rr}=0$ 的物理意义是，沿着光线的传播方向（即 $r$ 增大的方向），时空间的“距离”为零。
然而，即使整个三维度规是退化的，它的子部分仍然可以包含有意义的几何信息。例如，对应于角坐标 $(\theta, \phi)$ 的 $2 \times 2$ 子矩阵 $\gamma_{ij}$ 并非退化的。计算可得：
$$\gamma = \begin{pmatrix} g_{\theta\theta}  g_{\theta\phi} \\ g_{\phi\theta}  g_{\phi\phi} \end{pmatrix} = \begin{pmatrix} r^2  0 \\ 0  r^2\sin^2\theta \end{pmatrix}$$
其[行列式](@entry_id:142978)为 $r^4\sin^2\theta$。这正好是半径为 $r$ 的球面度规的[行列式](@entry_id:142978)。它描述了在光锥上给定“时刻” $r$ 的[横截面](@entry_id:154995)的几何，这个[横截面](@entry_id:154995)就是一个半径为 $r$ 的球面。

通过这些例子，我们看到[诱导度规](@entry_id:160616)是一个统一而强大的工具，它将不同维度、不同几何背景下的[子流形几何](@entry_id:189265)学联系在一起，为我们深入理解弯曲空间中的物理和数学提供了坚实的基础。