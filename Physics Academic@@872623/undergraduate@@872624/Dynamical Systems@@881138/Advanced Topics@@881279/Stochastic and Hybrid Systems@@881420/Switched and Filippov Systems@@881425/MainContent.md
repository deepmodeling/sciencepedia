## Introduction
Many systems in science and engineering, from electronic circuits and mechanical robots to gene regulatory networks, do not evolve smoothly. Instead, their behavior is punctuated by abrupt, event-driven changes in their governing laws. Modeling such systems presents a unique challenge: classical differential equations, which assume smooth dynamics, fall short when faced with these discontinuities. This article introduces the powerful framework of switched and Filippov systems, which provides the mathematical tools to analyze and understand these complex, non-smooth dynamics.

Here, we bridge this knowledge gap by exploring how to define, analyze, and apply these systems. In the first chapter, **Principles and Mechanisms**, we will lay the theoretical groundwork, defining [switched systems](@entry_id:271268) and introducing the Filippov framework to handle discontinuities, leading to the crucial concept of sliding modes. Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate the vast utility of these concepts, showcasing real-world examples in control engineering, biology, and economics. Finally, the **Hands-On Practices** section will allow you to solidify your understanding by tackling practical problems, from calculating trajectories to designing [stabilizing controllers](@entry_id:168369). By the end, you will have a comprehensive understanding of how discrete logic and [continuous dynamics](@entry_id:268176) intersect to produce rich and often counter-intuitive behaviors.

## Principles and Mechanisms

Dynamical systems are frequently characterized by smooth, continuous evolution. However, a vast array of physical, biological, and engineered systems exhibit abrupt, event-driven changes in their governing laws. These systems, which range from [mechanical oscillators](@entry_id:270035) with friction to [gene regulatory networks](@entry_id:150976) and electronic power converters, are modeled as **[switched systems](@entry_id:271268)**. This chapter elucidates the fundamental principles and mechanisms governing their behavior, moving from basic definitions to the sophisticated concepts required to analyze their often counter-intuitive dynamics.

### Defining Switched Systems

At its core, a **switched system** is a hybrid of [continuous dynamics](@entry_id:268176) and discrete logic. It comprises a family of distinct continuous-time dynamical systems, often called *modes* or *subsystems*, and a *switching signal* or rule that determines which mode is active at any given time. The state of such a system is described by a continuous variable $x(t) \in \mathbb{R}^n$ and often an implicit or explicit discrete mode $q(t) \in \{1, 2, \dots, N\}$. The evolution is given by an equation of the form:
$$ \frac{dx}{dt} = f_{q(t)}(x(t)) $$
The switching signal $q(t)$ can be a function of time, the state $x$, or both.

A common and important class is that of **state-dependent [switched systems](@entry_id:271268)**, where the active mode depends directly on the location of the [state vector](@entry_id:154607) $x$ in the state space. The state space is partitioned into a set of regions, and a specific dynamical law is assigned to each region. When the state trajectory reaches a boundary between regions, a switch occurs.

Consider, for example, a self-regulating [chemical reactor](@entry_id:204463) where the concentration $x(t)$ of a compound is controlled [@problem_id:1712586]. The reactor may operate in an "active" mode, where the concentration evolves according to $\frac{dx}{dt} = \alpha - \beta x$, causing the concentration to increase towards a steady state $\frac{\alpha}{\beta}$. If this concentration reaches a critical threshold $c$, a permanent switch is triggered, and the system enters a "passive" mode governed by $\frac{dx}{dt} = -\beta x$, causing the concentration to decay. The boundary that triggers this change, in this case the plane $x=c$, is known as a **switching surface** or **switching manifold**. Analyzing such a system involves solving the dynamics piecewise. The time $T_1$ to reach the surface is found by solving the first ODE. The state at that moment, $x(T_1)=c$, then serves as the initial condition for the second ODE, which is solved to find the subsequent evolution. The total time for a process is the sum of the durations of each phase.

### The Challenge of Discontinuities: The Filippov Framework

While the piecewise solution approach is effective when trajectories clearly cross a switching surface, it raises a profound theoretical question: what are the dynamics *at* the surface itself? If the vector field $f(x)$ in the equation $\dot{x} = f(x)$ has a jump discontinuity across a surface, the derivative $\dot{x}$ is not well-defined for a trajectory on that surface. This violates the conditions of standard existence and uniqueness theorems for ODEs (such as the Picard-Lindelöf theorem), which require the vector field to be at least locally Lipschitz continuous.

This is not merely a mathematical subtlety; it has deep implications for the system's classification and behavior [@problem_id:2441660]. A system with a discontinuous right-hand side is still a continuous-time system, as time itself evolves continuously. Furthermore, if the governing rules are fixed and involve no random inputs, the system is not stochastic. However, the breakdown of classical uniqueness means that from a single initial condition, multiple valid trajectories may exist. This introduces a form of [non-determinism](@entry_id:265122) that arises from the model's structure, not from randomness.

To resolve this ambiguity, we require a generalized notion of a solution. The most widely used framework is that of A.F. Filippov. The Filippov approach replaces the ill-defined, single-valued vector field $f(x)$ at a point of discontinuity $x$ on a surface with a set of possible velocities. This turns the differential equation into a **[differential inclusion](@entry_id:171950)**, $\dot{x} \in \mathcal{F}[f](x)$.

The **Filippov set-valued map**, $\mathcal{F}[f](x)$, is constructed to capture the essential behavior of the vector field $f$ in an infinitesimally small neighborhood of $x$ [@problem_id:2712025]. Formally, for a vector field $f$ that is locally essentially bounded and Lebesgue measurable, the Filippov set at a point $x$ is defined as:
$$ \mathcal{F}[f](x) := \bigcap_{\delta>0} \bigcap_{\mu(N)=0} \overline{\text{co}}\left( f(B(x,\delta) \setminus N) \right) $$
where $B(x,\delta)$ is an [open ball](@entry_id:141481) of radius $\delta$ around $x$, $\mu(N)$ is the Lebesgue measure of a set $N$, and $\overline{\text{co}}$ denotes the closed convex hull (the smallest closed, convex set containing the given set). This definition achieves three crucial goals:
1.  **Localization:** The intersection over all radii $\delta > 0$ ensures we only consider the behavior of $f$ in an arbitrarily small neighborhood of $x$.
2.  **Robustness:** The intersection over all sets $N$ of [measure zero](@entry_id:137864) means we ignore the values of $f$ on negligible sets, making the definition robust to inconsequential changes.
3.  **Convexification:** Taking the [convex hull](@entry_id:262864) allows for velocities that are weighted averages of the limiting [vector fields](@entry_id:161384) from all sides of the discontinuity. This is the key to modeling the "averaging" effect seen in sliding motion.

A **Filippov solution** is then an [absolutely continuous function](@entry_id:190100) $x(t)$ that satisfies the [differential inclusion](@entry_id:171950) $\dot{x}(t) \in \mathcal{F}[f](x(t))$ for almost all $t$.

### Sliding Modes: Dynamics on the Boundary

The most significant and physically interesting phenomenon captured by the Filippov framework is the **[sliding mode](@entry_id:263630)**. A [sliding mode](@entry_id:263630) can occur on a segment of a switching surface when the [vector fields](@entry_id:161384) on all sides are directed towards the surface, effectively trapping trajectories on it.

#### The Geometric Condition for Sliding

Consider a system with two modes, $\dot{x} = f_1(x)$ in a region defined by $h(x) > 0$ and $\dot{x} = f_2(x)$ in the region $h(x)  0$. The switching surface is $\Sigma = \{x \mid h(x) = 0\}$. The normal vector to this surface, $\nabla h(x)$, points out of the region $h(x)0$ and into the region $h(x)>0$.

A trajectory that hits the surface will be forced to slide along it if the flow on the $h>0$ side points back toward the surface and the flow on the $h0$ side also points toward the surface. The component of a vector field $f$ normal to the surface is given by the dot product $\nabla h \cdot f$. Therefore, the condition for an attractive [sliding mode](@entry_id:263630) at a point $x \in \Sigma$ is:
$$ \nabla h(x) \cdot f_1(x)  0 \quad \text{and} \quad \nabla h(x) \cdot f_2(x) > 0 $$
This ensures that any small perturbation off the surface in either direction results in a force that restores the trajectory to the surface. The set of points on $\Sigma$ that satisfy these inequalities is called the **sliding region**.

For instance, for a planar system with a parabolic switching surface $h(x_1, x_2) = x_1 - x_2^2 = 0$ and [vector fields](@entry_id:161384) $f_1$ and $f_2$, one must compute the dot products with the normal vector $\nabla h = (1, -2x_2)$ and find the values of $x_2$ for which the sliding conditions hold [@problem_id:1712542]. Similarly, for a linear system with a switching plane $h(x) = x_1 + x_2 = 0$ and dynamics $\dot{x}=A_1 x$ and $\dot{x}=A_2 x$, the sliding conditions depend on the parameters of the matrices $A_1$ and $A_2$ [@problem_id:1712538].

#### The Dynamics of Sliding Motion

Once a trajectory is confined to the sliding region, its evolution is governed by an effective vector field known as the **sliding vector field**. This field is determined by the **Filippov convex combination method**. The sliding dynamics are a weighted average of the two [vector fields](@entry_id:161384):
$$ \dot{x}_{slide} = (1-\alpha)f_1(x) + \alpha f_2(x), \quad \text{for } x \in \Sigma $$
The mixing parameter $\alpha \in [0, 1]$ represents the proportion of time the system effectively spends in mode 2. This parameter is not arbitrary; it is determined by the condition that the motion must remain on the surface $\Sigma$. This means the sliding velocity vector must be tangent to the surface, or equivalently, orthogonal to the normal vector:
$$ \nabla h(x) \cdot \dot{x}_{slide} = 0 $$
Substituting the convex combination into this [tangency condition](@entry_id:173083) gives an equation for $\alpha$:
$$ \nabla h \cdot ((1-\alpha)f_1 + \alpha f_2) = (1-\alpha)(\nabla h \cdot f_1) + \alpha(\nabla h \cdot f_2) = 0 $$
Solving for $\alpha$ yields:
$$ \alpha = \frac{\nabla h \cdot f_1}{\nabla h \cdot f_1 - \nabla h \cdot f_2} $$
This value of $\alpha$ is then substituted back into the convex combination to find the differential equation that governs the motion along the sliding manifold.

For a simple scalar system $\dot{x} = f(x)$ with a discontinuity at $x=0$, where $f(x) = f_{pos}$ for $x>0$ and $f(x) = f_{neg}$ for $x0$, sliding occurs if $f_{pos}  0$ and $f_{neg} > 0$. The sliding dynamics must keep the state at $x=0$, so $\dot{x}_{slide} = 0$. The convex combination gives $0 = (1-\alpha)f_{pos} + \alpha f_{neg}$, which can be solved for $\alpha$ [@problem_id:1712585]. For higher-dimensional systems, this procedure yields a lower-dimensional ODE describing the flow on the switching surface, which can then be analyzed for its own equilibria and stability [@problem_id:1712579].

### Stability and Complex Behaviors

The introduction of switching fundamentally alters the stability properties and long-term behavior of a system. The stability of a switched system cannot, in general, be inferred from the stability of its individual modes.

#### Stabilization Through Switching

Perhaps the most remarkable feature of [switched systems](@entry_id:271268) is the possibility of **stabilization through switching**. A system can be made asymptotically stable even if every one of its constituent subsystems is unstable. A classic example involves a 2D system where the dynamics in both the right half-plane ($x_1>0$) and the left half-plane ($x_10$) are governed by matrices whose eigenvalues have positive real parts, corresponding to unstable spirals [@problem_id:2201254]. While trajectories in each subsystem spiral outwards, a carefully designed switching law can create an attractive sliding region on the boundary between them (e.g., the $y$-axis). If the dynamics on this sliding manifold are stable and guide trajectories toward the origin, the overall system becomes asymptotically stable. The [unstable modes](@entry_id:263056) push the state onto the [sliding surface](@entry_id:276110), and the stable sliding dynamics then carry it to the equilibrium point.

#### Limit Cycles, Hysteresis, and Delays

Switched systems are natural generators of oscillations and limit cycles. One common mechanism for creating robust, [sustained oscillations](@entry_id:202570) is **[hysteresis](@entry_id:268538)**. In a hysteretic system, the condition for switching from mode 1 to mode 2 is different from the condition for switching back from mode 2 to mode 1. For example, a thermostat turns on the heat when the temperature drops to a lower threshold $T_{low}$ and turns it off only when it rises to an upper threshold $T_{high}$.

This mechanism is prevalent in [biological oscillators](@entry_id:148130) [@problem_id:1712546]. An oscillator's state might evolve in an "active" mode, causing its radial distance $r$ from the origin to grow. When $r$ reaches an outer radius $R_{out}$, the system switches to a "repressive" mode, causing $r$ to decay. The system remains in this mode until $r$ drops to an inner radius $R_{in}$, at which point it switches back to the active mode. The region between $R_{in}$ and $R_{out}$ is the hysteresis band. This separation of switching surfaces prevents the system from chattering at a single boundary and naturally gives rise to a stable [limit cycle](@entry_id:180826).

Conversely, the absence of such mechanisms can lead to extreme sensitivity. An idealized system like $\dot{x} = -K\text{sgn}(x)$ has a unique, globally asymptotically stable Filippov solution at $x=0$ [@problem_id:1712563]. However, if we introduce a small, realistic time delay $\tau$ into the control loop, so that $\dot{x}(t) = -K \text{sgn}(x(t-\tau))$, the behavior changes dramatically. The delay causes the system to "overshoot" the origin repeatedly, resulting in a stable [limit cycle oscillation](@entry_id:275225) instead of a stable equilibrium. The amplitude and period of this oscillation are determined by the [system gain](@entry_id:171911) $K$ and the delay $\tau$.

### Zeno Behavior: Infinite Switching in Finite Time

A fascinating and sometimes problematic phenomenon in the theory of switched and [hybrid systems](@entry_id:271183) is **Zeno behavior**. This occurs when a system experiences an infinite number of discrete events (switches) in a finite amount of time. The term is named after the Greek philosopher Zeno of Elea and his paradoxes of motion.

Consider a faulty water tank where the water level $h(t)$ drains according to $\dot{h} = -c\sqrt{h}$ [@problem_id:1712556]. When the tank empties ($h=0$), a controller is supposed to refill it. Instead, it instantaneously injects a small amount of water, resetting the level to $h_{new} = k \cdot h_{start}$, where $h_{start}$ was the level at the beginning of the draining phase and $k$ is a fraction between 0 and 1. The time it takes to drain is proportional to $\sqrt{h_{start}}$. After the first reset, the new starting height is smaller, so the next draining period is shorter. This process repeats, with the duration of successive draining cycles forming a geometric series with ratio $\sqrt{k}  1$. Because this [geometric series](@entry_id:158490) converges, the total time for an infinite number of drain-refill cycles is finite. This finite time is called the Zeno time.

While mathematically intriguing, Zeno behavior is typically an artifact of idealized models that allow for instantaneous switching and state resets. In any real physical system, switching takes a small but non-zero amount of time, which prevents an infinite number of switches from occurring. Nevertheless, the possibility of Zeno behavior is a critical consideration in the design and verification of hybrid [control systems](@entry_id:155291), and mechanisms like hysteresis are often explicitly introduced to prevent it.