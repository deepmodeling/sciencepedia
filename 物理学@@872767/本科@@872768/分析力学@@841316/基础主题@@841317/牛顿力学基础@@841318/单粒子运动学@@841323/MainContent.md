## 引言
运动是物理世界最普遍的现象之一，而运动学则是我们用以描述和理解运动的数学语言。在深入探究力与运动关系的动力学之前，我们必须首先掌握如何精确地描述运动本身——即[质点](@entry_id:186768)在空间中的位置如何随时间变化。本文旨在解决这一基本问题，为单个[质点](@entry_id:186768)的运动建立一个完整而严谨的[运动学](@entry_id:173318)框架。

通过学习本文，您将踏上一段从基本概念到复杂应用的旅程。在第一章“原理和机制”中，我们将建立位置、速度和加速度的核心定义，并探索它们在不同[坐标系](@entry_id:156346)（包括笛卡尔坐标、极坐标和内在坐标）下的数学表达。接着，在第二章“应用与跨学科联系”中，我们将见证这些理论如何应用于解决工程技术、物理科学和相对运动中的实际问题，展示运动学作为分析工具的强大威力。最后，“动手实践”部分将提供具体问题，让您亲手运用所学知识，将理论转化为解决问题的能力。让我们从构建这门“运动的几何学”的基础开始。

## 原理和机制

在对运动的探索中，运动学是我们的第一步。它以一种纯粹几何的方式描述运动，而不探究其原因（即力）。本章旨在建立描述单个质点运动的数学语言，我们将从最基本的概念——位置、速度和加速度——开始，然后扩展到不同的[坐标系](@entry_id:156346)，并最终探索描述复杂轨迹内在几何的强大工具。

### 基本[运动学](@entry_id:173318)量

描述质点运动的出发点是其在空间中的**位置**。在一个给定的[参考系](@entry_id:169232)中，我们可以用一个从原点指向质点的**位置矢量** $\vec{r}$ 来唯一确定其位置。随着时间的推移，[质点](@entry_id:186768)描绘出一条轨迹，因此位置矢量是时间 $t$ 的函数：$\vec{r}(t)$。

运动的第一个核心概念是**速度**，它量化了位置变化的快慢和方向。瞬时速度 $\vec{v}(t)$ 被定义为位置矢量对时间的[一阶导数](@entry_id:749425)：

$$
\vec{v}(t) = \frac{d\vec{r}(t)}{dt}
$$

速度是一个矢量，其方向与[质点](@entry_id:186768)轨迹在该点的[切线](@entry_id:268870)方向相同，其大小 $v = |\vec{v}(t)|$ 被称为**速率**。

接下来，我们需要描述速度本身如何变化。**加速度** $\vec{a}(t)$ 正是为此而生，它被定义为速度矢量对时间的一阶导数，或者说是位置矢量对时间的[二阶导数](@entry_id:144508)：

$$
\vec{a}(t) = \frac{d\vec{v}(t)}{dt} = \frac{d^2\vec{r}(t)}{dt^2}
$$

加[速度矢量](@entry_id:269648)指明了速度矢量变化的趋势。值得注意的是，即使一个物体的速率保持不变（例如，[匀速圆周运动](@entry_id:178264)），只要其运动方向在改变，它仍然具有加速度。

在[笛卡尔坐标系](@entry_id:169789)中，这些定义表现得最为直观。位置矢量可以写成 $\vec{r}(t) = x(t)\hat{i} + y(t)\hat{j} + z(t)\hat{k}$，其中 $\hat{i}, \hat{j}, \hat{k}$ 是固定的单位[基矢](@entry_id:199546)量。由于[基矢](@entry_id:199546)量是常数，求导运算可以直接作用于分量上：

$$
\vec{v}(t) = \frac{dx}{dt}\hat{i} + \frac{dy}{dt}\hat{j} + \frac{dz}{dt}\hat{k} = v_x(t)\hat{i} + v_y(t)\hat{j} + v_z(t)\hat{k}
$$

$$
\vec{a}(t) = \frac{dv_x}{dt}\hat{i} + \frac{dv_y}{dt}\hat{j} + \frac{dv_z}{dt}\hat{k} = a_x(t)\hat{i} + a_y(t)\hat{j} + a_z(t)\hat{k}
$$

考虑一个沿椭圆螺旋线上升的无人机，其路径由位置矢量 $\vec{r}(t) = A\cos(\omega t)\hat{i} + B\sin(\omega t)\hat{j} + ct\hat{k}$ 描述 ([@problem_id:2061597])。我们可以通过直接求导来找到它的瞬时速度：

$$
\vec{v}(t) = \frac{d\vec{r}}{dt} = -A\omega\sin(\omega t)\hat{i} + B\omega\cos(\omega t)\hat{j} + c\hat{k}
$$

这个[速度矢量](@entry_id:269648)包含了关于运动的全部瞬时信息。例如，如果我们想知道速度矢量与垂直方向（由 $\hat{k}$ 代表）的夹角 $\theta$，我们可以使用[点积](@entry_id:149019)的定义 $\vec{a} \cdot \vec{b} = |\vec{a}||\vec{b}|\cos\theta$。此时，$\vec{v}(t)\cdot\hat{k} = c$，而速度大小为 $|\vec{v}(t)| = \sqrt{(-A\omega\sin(\omega t))^2 + (B\omega\cos(\omega t))^2 + c^2}$。因此，我们可以确定任意时刻 $t$ 的夹角：

$$
\theta(t) = \arccos\left(\frac{c}{|\vec{v}(t)|}\right) = \arccos\left(\frac{c}{\sqrt{\omega^{2}\left(A^{2}\sin^{2}(\omega t)+B^{2}\cos^{2}(\omega t)\right)+c^{2}}}\right)
$$

这个例子展示了如何从一个给定的轨迹函数 $\vec{r}(t)$ 出发，通过[微分](@entry_id:158718)和[矢量代数](@entry_id:152340)，提取出有意义的物理量。

### 非笛卡尔坐标系中的运动学

虽然[笛卡尔坐标系](@entry_id:169789)很基础，但对于具有特定对称性（如圆形或旋转）的运动，使用其他[坐标系](@entry_id:156346)会大大简化问题。然而，这种便利性是有代价的：非笛卡尔坐标系的[基矢](@entry_id:199546)量本身可能随[质点](@entry_id:186768)的位置而变化。

#### [平面极坐标](@entry_id:171478)

对于平面内的运动，**[平面极坐标](@entry_id:171478)** $(r, \theta)$ 特别有用。它通过到原点的径向距离 $r$ 和与固定轴的夹角 $\theta$ 来定位一个点。与固定的 $\hat{i}, \hat{j}$ 不同，极坐标的[基矢](@entry_id:199546)量——指向径向向外的**径向单位矢量** $\hat{e}_r$ 和与之垂直的**切向单位矢量** $\hat{e}_\theta$ ——的方向取决于[质点](@entry_id:186768)的位置。它们与笛卡尔[基矢](@entry_id:199546)量的关系是：

$$
\hat{e}_r = \cos\theta \hat{i} + \sin\theta \hat{j}
$$
$$
\hat{e}_\theta = -\sin\theta \hat{i} + \cos\theta \hat{j}
$$

这里的关键在于，当质点运动时，$\theta$ 会随时间变化，导致 $\hat{e}_r$ 和 $\hat{e}_\theta$ 也随时间变化。它们的时间导数是：

$$
\frac{d\hat{e}_r}{dt} = \frac{d\hat{e}_r}{d\theta}\frac{d\theta}{dt} = (-\sin\theta \hat{i} + \cos\theta \hat{j})\dot{\theta} = \dot{\theta}\hat{e}_\theta
$$
$$
\frac{d\hat{e}_\theta}{dt} = \frac{d\hat{e}_\theta}{d\theta}\frac{d\theta}{dt} = (-\cos\theta \hat{i} - \sin\theta \hat{j})\dot{\theta} = -\dot{\theta}\hat{e}_r
$$

理解了[基矢](@entry_id:199546)量的变化规律，我们就可以推导出速度和加速度的表达式。位置矢量简单地表示为 $\vec{r} = r\hat{e}_r$。使用乘法法则对其求导得到速度：

$$
\vec{v} = \frac{d(r\hat{e}_r)}{dt} = \dot{r}\hat{e}_r + r\frac{d\hat{e}_r}{dt} = \dot{r}\hat{e}_r + r\dot{\theta}\hat{e}_\theta
$$

这里，$\dot{r}$ 是[径向速度](@entry_id:159824)分量，而 $r\dot{\theta}$ 是切向速度分量。再次对速度求导得到加速度，这就需要更仔细地应用乘法法则：

$$
\vec{a} = \frac{d\vec{v}}{dt} = \frac{d}{dt}(\dot{r}\hat{e}_r + r\dot{\theta}\hat{e}_\theta) = (\ddot{r}\hat{e}_r + \dot{r}\frac{d\hat{e}_r}{dt}) + (\dot{r}\dot{\theta}\hat{e}_\theta + r\ddot{\theta}\hat{e}_\theta + r\dot{\theta}\frac{d\hat{e}_\theta}{dt})
$$

将[基矢](@entry_id:199546)量的导数代入并合并同类项，我们得到加速度在极坐标下的[标准形式](@entry_id:153058)：

$$
\vec{a} = (\ddot{r} - r\dot{\theta}^2)\hat{e}_r + (r\ddot{\theta} + 2\dot{r}\dot{\theta})\hat{e}_\theta
$$

这个表达式比笛卡尔坐标下的形式复杂得多，但每一项都有明确的物理意义。
- **径向分量** $a_r = \ddot{r} - r\dot{\theta}^2$:
    - $\ddot{r}$：质点沿径向的加速度，即[径向速度](@entry_id:159824)的变化率。
    - $-r\dot{\theta}^2$：**向心加速度**。即使[质点](@entry_id:186768)与原点的距离 $r$ 不变，只要它在转动（$\dot{\theta} \neq 0$），就需要一个指向中心的加速度来不断改变其速度方向。
- **切向分量** $a_\theta = r\ddot{\theta} + 2\dot{r}\dot{\theta}$:
    - $r\ddot{\theta}$：**[切向加速度](@entry_id:173884)**。它源于[角速度](@entry_id:192539) $\dot{\theta}$ 的变化（角加速度 $\ddot{\theta}$）。
    - $2\dot{r}\dot{\theta}$：**[科里奥利加速度](@entry_id:171639)**。这是一个更微妙的项，只有当[质点](@entry_id:186768)同时具有[径向速度](@entry_id:159824)（$\dot{r} \neq 0$）和角速度（$\dot{\theta} \neq 0$）时才会出现。它源于两个效应的叠加：一部分是[径向速度](@entry_id:159824)的方向因旋转而改变，另一部分是切向速度的大小因径向位置 $r$ 的改变而改变。

我们可以从一个更根本的角度来推导这些分量，如 [@problem_id:2061585] 所示。从[笛卡尔坐标](@entry_id:167698) $x=r\cos\theta$ 和 $y=r\sin\theta$ 开始，通过两次求导得到 $\ddot{x}$ 和 $\ddot{y}$。然后，将加[速度矢量](@entry_id:269648) $\vec{a} = \ddot{x}\hat{i} + \ddot{y}\hat{j}$ 投影到切向单位矢量 $\hat{e}_\theta = -\sin\theta\hat{i} + \cos\theta\hat{j}$ 上，即计算 $a_\theta = \vec{a} \cdot \hat{e}_\theta = -\ddot{x}\sin\theta + \ddot{y}\cos\theta$。经过一番代数运算和三角化简，将得到与上面完全相同的表达式 $a_\theta = r\ddot{\theta} + 2\dot{r}\dot{\theta}$。这个过程虽然繁琐，但它清晰地揭示了极[坐标加速度](@entry_id:264260)项是如何从最基本的笛卡尔定义中自然产生的。

考虑一个在太空中工作的机械臂，其夹爪从枢轴点以恒定速度 $a$ 向[外延](@entry_id:161930)伸，同时整个臂以恒定[角速度](@entry_id:192539) $\omega$ 旋转 ([@problem_id:2061583])。其运动由 $r(t) = R_0 + at$ 和 $\theta(t) = \omega t$ 描述。我们可以计算出其各阶导数：$\dot{r}=a, \ddot{r}=0, \dot{\theta}=\omega, \ddot{\theta}=0$。将这些代入加速度分量公式：

$$
a_r = 0 - (R_0 + at)\omega^2 = -\omega^2(R_0 + at)
$$
$$
a_\theta = 0 + 2a\omega = 2a\omega
$$

[径向加速度](@entry_id:173091)是向内的向心加速度，而[切向加速度](@entry_id:173884)是恒定的[科里奥利加速度](@entry_id:171639)。如果我们想找到这两个分量大小相等的时间，只需解方程 $|a_r| = |a_\theta|$，即 $\omega^2(R_0 + at) = 2a\omega$，从而得到 $t = \frac{2}{\omega} - \frac{R_0}{a}$。

同样，[坐标系](@entry_id:156346)之间的转换也是一个重要的技能。例如，对于一个沿[对数螺线](@entry_id:174157) $r(t) = R_0 \exp(k \omega t)$, $\theta(t) = \omega t$ 运动的[质点](@entry_id:186768) ([@problem_id:2061614])，我们可以通过关系式 $y(t) = r(t)\sin(\theta(t)) = R_0\exp(k\omega t)\sin(\omega t)$，直接求其在笛卡尔 $y$ 轴上的加速度分量 $a_y=\ddot{y}$。通过两次应用[乘法法则](@entry_id:144424)和链式法则进行[微分](@entry_id:158718)，可以得到 $a_y$ 作为时间的函数，这展示了如何在不同[坐标系](@entry_id:156346)的描述之间进行切换。

### 运动的内在几何：曲率和挠率

除了使用固定的外部[坐标系](@entry_id:156346)，我们还可以从[质点](@entry_id:186768)自身“视角”出发，沿着其运动轨迹来描述运动。这种方法被称为**内在[坐标系](@entry_id:156346)**或自然[坐标系](@entry_id:156346)。

#### 切向与[法向加速度](@entry_id:170071)

在任意时刻，[质点](@entry_id:186768)的[速度矢量](@entry_id:269648) $\vec{v}$ 总是与路径相切。我们可以定义一个**单位切矢量** $\vec{T} = \vec{v}/v$，其中 $v=|\vec{v}|$ 是速率。加速度矢量 $\vec{a}$ 可以分解为两个相互垂直的分量：一个与 $\vec{T}$ 平行，称为**[切向加速度](@entry_id:173884)** $\vec{a}_t$；另一个与 $\vec{T}$ 垂直，称为**[法向加速度](@entry_id:170071)** $\vec{a}_n$。

$$
\vec{a} = \vec{a}_t + \vec{a}_n
$$

[切向加速度](@entry_id:173884)只改变速度的大小（速率），而[法向加速度](@entry_id:170071)只改变速度的方向。它们的表达式为：

$$
\vec{a}_t = \frac{dv}{dt}\vec{T} \quad \text{和} \quad \vec{a}_n = \frac{v^2}{\rho}\vec{N}
$$

在这里，$\frac{dv}{dt}$ 是速率对时间的导数。$\vec{N}$ 是**单位主法矢量**，指向轨迹的瞬时“弯曲中心”。$\rho$ 是一个极其重要的几何量，称为**[曲率半径](@entry_id:274690)**。它代表了在该点最能贴合轨迹的圆（即**[密切圆](@entry_id:169863)**）的半径。轨迹弯曲得越急，曲率半径就越小。

考虑一个从静止开始沿半径为 $\rho$ 的圆形轨道运动的粒子，其[切向加速度](@entry_id:173884)为常数 $a_t = c_1$ ([@problem_id:2061610])。其速率随时间线性增加：$v(t) = c_1 t$。因此，其[法向加速度](@entry_id:170071)为 $a_n(t) = v(t)^2/\rho = (c_1 t)^2/\rho$。总加速度的大小为 $a(t) = \sqrt{a_t^2 + a_n(t)^2} = \sqrt{c_1^2 + (c_1^2 t^2/\rho)^2}$。在初始时刻 $t=0$，速率为零，[法向加速度](@entry_id:170071)也为零，总加速度就是[切向加速度](@entry_id:173884) $a(0)=c_1$。这个问题要求我们找到总加速度大小变为初始值三倍的时刻，即 $a(t) = 3c_1$。解此方程可得 $t = 2^{3/4} \sqrt{\rho/c_1}$。这个例子清晰地展示了切向和[法向加速度](@entry_id:170071)如何共同构成了总加速度。

#### 曲率的计算

对于平面上由[参数方程](@entry_id:172360) $(x(t), y(t))$ 给出的轨迹，曲率半径 $\rho$ 可以通过以下公式计算：

$$
\rho = \frac{(\dot{x}^2 + \dot{y}^2)^{3/2}}{|\dot{x}\ddot{y} - \dot{y}\ddot{x}|}
$$

**曲率** $\kappa$ 定义为曲率半径的倒数，$\kappa = 1/\rho$，它直接衡量了轨迹的弯曲程度。

一个经典的例子是[抛体运动](@entry_id:174344) ([@problem_id:2061605])。一个在[引力场](@entry_id:169425)中被水平抛出的物体，其轨迹为 $x(t) = v_0 t, y(t) = -\frac{1}{2}g t^2$。我们可以计算各阶导数：$\dot{x}=v_0, \dot{y}=-g t, \ddot{x}=0, \ddot{y}=-g$。代入[曲率半径](@entry_id:274690)公式：

$$
\rho(t) = \frac{(v_0^2 + (-g t)^2)^{3/2}}{|v_0(-g) - (-g t)(0)|} = \frac{(v_0^2 + g^2 t^2)^{3/2}}{v_0 g}
$$

为了找到最小[曲率半径](@entry_id:274690)，我们只需找到使分子最小化的时间，即 $t=0$（抛出瞬间，即轨迹的顶点）。此时，$\rho_{\min} = \frac{(v_0^2)^{3/2}}{v_0 g} = \frac{v_0^2}{g}$。这符合我们的直觉：在轨迹的最高点，路径弯曲得最厉害。

我们甚至可以更进一步，确定[密切圆](@entry_id:169863)的中心，即**[曲率中心](@entry_id:270032)** $\vec{C}$。其位置矢量由下式给出：

$$
\vec{C}(t) = \vec{r}(t) + \rho(t)\vec{N}(t)
$$

对于一个由速度 $\vec{v}(t) = (b t) \hat{i} + (c t^2) \hat{j}$ 定义的平面运动 ([@problem_id:2061621])，通过系统地计算位置 $\vec{r}(t)$、加速度 $\vec{a}(t)$、曲率半径 $\rho(t)$ 和主法矢量 $\vec{N}(t)$，我们可以求出[曲率中心](@entry_id:270032) $\vec{C}(t)$ 的轨迹。这是一个展示如何将所有运动学和几何概念结合起来解决复杂问题的综合性练习。

#### 三维运动：挠率与[Frenet-Serret标架](@entry_id:261316)

对于三维空间中的曲线，除了弯曲（由曲率 $\kappa$ 描述）之外，还存在“扭曲”，即曲线偏离其[密切平面](@entry_id:167179)的趋势。这种扭曲由**挠率** $\tau$ 来量化。

为了严谨地描述这一点，我们引入**[Frenet-Serret标架](@entry_id:261316)**，一个随质点一起沿着轨迹移动的局部[正交坐标](@entry_id:166074)系，由三个单位矢量组成：单位切矢量 $\vec{T}$、单位主法矢量 $\vec{N}$ 和**单位副法矢量** $\vec{B} = \vec{T} \times \vec{N}$。这个标架的演化由**[Frenet-Serret公式](@entry_id:267751)**描述（以[弧长](@entry_id:191173) $s$ 为参数）：

$$
\frac{d\vec{T}}{ds} = \kappa \vec{N}
$$
$$
\frac{d\vec{N}}{ds} = -\kappa \vec{T} + \tau \vec{B}
$$
$$
\frac{d\vec{B}}{ds} = -\tau \vec{N}
$$

曲率 $\kappa$ 衡量了轨迹在 $(\vec{T}, \vec{N})$ 平面内的弯曲，而挠率 $\tau$ 衡量了轨迹如何“扭转”出这个平面。如果一条[曲线的挠率](@entry_id:637035)恒为零，那么它必定是一条[平面曲线](@entry_id:271353)。

一个深刻的几何结果，即Lancret定理，指出一条曲线是**[广义螺旋线](@entry_id:273349)**（其切矢量与空间中一个固定方向成固定角度）的充要条件是其挠率与曲率之比 $\tau/\kappa$ 为常数。在 [@problem_id:2061619] 中探讨了一个特殊情况，即在轨迹的每一点上都有 $\kappa(s) = \tau(s)$。这意味着 $\tau/\kappa = 1$（除非曲线是直线，此时 $\kappa=\tau=0$）。根据Lancret定理，这精确地对应于切矢量 $\vec{T}$ 与某个固定方向 $\vec{u}$ 的夹角 $\theta$ 满足 $\cot\theta = 1$，即 $\theta = \pi/4$ 的所有曲线。这揭示了运动的瞬时几何性质（$\kappa, \tau$）如何决定了轨迹的全局形状。

### 高级专题

#### 从加速度定律推断运动性质

有时，我们知道加速度作为位置和速度的函数，例如 $\vec{a} = \vec{a}(\vec{r}, \vec{v})$。即使无法完全解出轨迹 $\vec{r}(t)$，我们通常也能通过矢量运算推断出运动的某些重要性质。

考虑一个奇特的运动定律 $\vec{a} = k(\vec{r} \times \vec{v})$ ([@problem_id:2061606])。我们可以分析这个系统的性质。首先，考虑速率的变化：

$$
\frac{d(v^2)}{dt} = \frac{d(\vec{v} \cdot \vec{v})}{dt} = 2 \vec{v} \cdot \frac{d\vec{v}}{dt} = 2 \vec{v} \cdot \vec{a} = 2k \vec{v} \cdot (\vec{r} \times \vec{v})
$$

由于三重标积 $\vec{v} \cdot (\vec{r} \times \vec{v})$ 中含有两个相同的矢量，其值恒为零。因此，$\frac{d(v^2)}{dt} = 0$，这意味着速率 $v$ 是一个守恒量，即 $v(t) = v_0$。接着，我们考察量 $\vec{r} \cdot \vec{v}$ 的变化：

$$
\frac{d(\vec{r} \cdot \vec{v})}{dt} = \frac{d\vec{r}}{dt} \cdot \vec{v} + \vec{r} \cdot \frac{d\vec{v}}{dt} = \vec{v} \cdot \vec{v} + \vec{r} \cdot \vec{a} = v_0^2 + k \vec{r} \cdot (\vec{r} \times \vec{v})
$$

同样，后面的三重标积为零，所以 $\frac{d(\vec{r} \cdot \vec{v})}{dt} = v_0^2$。对时间积分，我们得到 $\vec{r} \cdot \vec{v} = (\vec{r}_0 \cdot \vec{v}_0) + v_0^2 t$。最后，我们知道 $\frac{d(r^2)}{dt} = \frac{d(\vec{r} \cdot \vec{r})}{dt} = 2 \vec{r} \cdot \vec{v}$。将上式代入并再次积分，便可得到质点到原点距离的平方随时间的变化规律：

$$
r^2(t) = r_0^2 + 2(\vec{r}_0 \cdot \vec{v}_0)t + v_0^2 t^2
$$

这个例子优雅地展示了如何仅通过[矢量代数](@entry_id:152340)和微积分，从加速度的函数形式中提取出关于运动的非平凡信息。

#### [旋转参考系](@entry_id:174154)中的[运动学](@entry_id:173318)

当我们在一个旋转的[参考系](@entry_id:169232)中观察运动时，描述会变得更加复杂。一个在[惯性系](@entry_id:266190) $S$ 中做简单运动（如匀速直线运动）的[质点](@entry_id:186768)，在相对于 $S$ 旋转的[参考系](@entry_id:169232) $S'$ 中看来，其轨迹可能非常复杂。

在[惯性系](@entry_id:266190) $S$ 和旋转系 $S'$ 中观察到的加速度之间的关系由以下公式给出（假设[角速度](@entry_id:192539) $\vec{\omega}$ 恒定）：

$$
\vec{a}_S = \vec{a}_{S'} + 2(\vec{\omega} \times \vec{v}_{S'}) + \vec{\omega} \times (\vec{\omega} \times \vec{r})
$$

这里的 $\vec{a}_{S'}$ 是在旋转系中测得的“真实”加速度。另外两项是**虚拟加速度**：$2(\vec{\omega} \times \vec{v}_{S'})$ 是**[科里奥利加速度](@entry_id:171639)**，$\vec{\omega} \times (\vec{\omega} \times \vec{r})$ 是**离心加速度**。

与其深入推导这个通用公式，不如通过一个具体例子来理解其效应 ([@problem_id:2061611])。假设一个[质点](@entry_id:186768)在[惯性系](@entry_id:266190) $S$ 中以恒定速度 $\vec{v}_S = v_0 \hat{i}$ 运动，其位置为 $\vec{r}(t) = v_0 t \hat{i}$。我们从一个以[角速度](@entry_id:192539) $\vec{\omega} = \omega_0 \hat{k}$ 绕公共 z 轴旋转的[参考系](@entry_id:169232) $S'$ 中观察它。在 $S'$ 中的坐标 $(x', y')$ 可以通过将 $S$ 中的坐标 $(x, y) = (v_0t, 0)$ 旋转角度 $-\omega_0 t$ 得到：

$$
x'(t) = x(t)\cos(-\omega_0 t) - y(t)\sin(-\omega_0 t) = v_0 t \cos(\omega_0 t)
$$
$$
y'(t) = x(t)\sin(-\omega_0 t) + y(t)\cos(-\omega_0 t) = -v_0 t \sin(\omega_0 t)
$$

在旋转系看来，这个[质点](@entry_id:186768)描绘出一条向外扩展的螺旋线。有了这个参数化的轨迹 $(x'(t), y'(t))$，我们就可以应用标准的曲率公式来计算其在任意时刻的曲率半径。这提供了一个具体的方法来量化在旋转参考系中观察到的轨迹是如何“弯曲”的，而这种弯曲正是由科里奥利力和离心力等虚拟效应所导致的。