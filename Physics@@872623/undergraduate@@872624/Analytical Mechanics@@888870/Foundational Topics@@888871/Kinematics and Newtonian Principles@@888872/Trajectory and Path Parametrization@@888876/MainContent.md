## Introduction
The ability to describe motion is the foundation of [analytical mechanics](@entry_id:166738). How do we translate the physical journey of an object—whether a planet in orbit or a bead on a wire—into a precise mathematical language? The answer lies in the powerful concept of **trajectory and path parametrization**. This framework provides the essential tools to move beyond a qualitative understanding of motion and develop a quantitative model that specifies an object's exact position, velocity, and acceleration at any given moment in time. This article bridges the gap between the abstract concepts of space and time and the concrete analysis of how objects move through them.

Across the following chapters, you will gain a comprehensive understanding of this fundamental topic. We will begin by establishing the core mathematical principles, then explore the vast applications of these ideas, and finally, provide opportunities for hands-on practice.
*   **Chapter 1: Principles and Mechanisms** will introduce the position vector, $\vec{r}(t)$, and show how time is used as a parameter to define a trajectory. You will learn to derive kinematic quantities like velocity and acceleration via differentiation and, conversely, to determine a path by integrating velocity.
*   **Chapter 2: Applications and Interdisciplinary Connections** will demonstrate how path [parametrization](@entry_id:272587) is applied to solve real-world problems in robotics, navigation, electromagnetism, and even general relativity, revealing its role as a unifying language across science and engineering.
*   **Chapter 3: Hands-On Practices** will challenge you to apply these concepts to analyze the motion of various mechanical systems, solidifying your understanding through practical problem-solving.

Let us begin by exploring the principles and mechanisms that form the mathematical bedrock of describing motion.

## Principles and Mechanisms

The study of motion is the cornerstone of classical mechanics. Having established the fundamental concepts of space, time, and [reference frames](@entry_id:166475) in the introductory chapter, we now turn to the mathematical description of motion itself. The path an object traces through space is known as its **trajectory**. This chapter elucidates the principles and mechanisms of describing such trajectories using the powerful mathematical framework of path [parametrization](@entry_id:272587).

### The Position Vector and Parametric Description of Motion

The location of a point particle in three-dimensional space can be uniquely specified by a **position vector**, $\vec{r}$, which is a vector drawn from the origin of a chosen coordinate system to the particle's location. As the particle moves, this vector changes with time. The function $\vec{r}(t)$ that maps each instant of time $t$ to the corresponding [position vector](@entry_id:168381) is the most complete description of the particle's motion.

In a Cartesian coordinate system, the position vector is expressed in terms of its components along the basis vectors $\hat{i}$, $\hat{j}$, and $\hat{k}$:
$$
\vec{r}(t) = x(t)\hat{i} + y(t)\hat{j} + z(t)\hat{k}
$$
Here, the coordinates $(x(t), y(t), z(t))$ are themselves functions of time. This representation describes the curve of motion in **[parametric form](@entry_id:176887)**, with time $t$ serving as the **parameter**. The set of all points traced by the tip of the vector $\vec{r}(t)$ as $t$ varies over an interval constitutes the particle's path.

For example, the motion of a particle along a straight line with constant velocity, starting from an initial position $\vec{r}_0 = x_0\hat{i} + y_0\hat{j}$, can be described by the [parametric equations](@entry_id:172360) $x(t) = x_0 + v_x t$ and $y(t) = y_0 + v_y t$. The position vector is thus $\vec{r}(t) = (x_0 + v_x t)\hat{i} + (y_0 + v_y t)\hat{j}$ [@problem_id:2093280]. This simple linear dependence on time traces a straight line path. More complex functional forms for the components lead to curved trajectories.

### Kinematic Quantities from the Trajectory

Once the trajectory $\vec{r}(t)$ is known, the fundamental kinematic quantities of velocity and acceleration are determined directly through differentiation.

The **velocity vector**, $\vec{v}(t)$, is defined as the rate of change of the [position vector](@entry_id:168381) with respect to time:
$$
\vec{v}(t) = \frac{d\vec{r}}{dt} = \frac{dx}{dt}\hat{i} + \frac{dy}{dt}\hat{j} + \frac{dz}{dt}\hat{k} = \dot{x}(t)\hat{i} + \dot{y}(t)\hat{j} + \dot{z}(t)\hat{k}
$$
The velocity vector is always tangent to the particle's path at the point corresponding to time $t$. Its magnitude, $|\vec{v}(t)|$, is the particle's instantaneous **speed**.

The **acceleration vector**, $\vec{a}(t)$, is the rate of change of the velocity vector:
$$
\vec{a}(t) = \frac{d\vec{v}}{dt} = \frac{d^2\vec{r}}{dt^2} = \ddot{x}(t)\hat{i} + \ddot{y}(t)\hat{j} + \ddot{z}(t)\hat{k}
$$
The [acceleration vector](@entry_id:175748) describes how the velocity is changing. It does not necessarily point along the trajectory; it can have components both tangent to the path (changing the speed) and normal to the path (changing the direction of motion).

Consider a drone whose trajectory is programmed to follow the path known as a twisted cubic, given by $\vec{r}(t) = (at)\hat{i} + (bt^2)\hat{j} + (ct^3)\hat{k}$, where $a$, $b$, and $c$ are constants [@problem_id:2093292]. The velocity is found by a single differentiation:
$$
\vec{v}(t) = \frac{d\vec{r}}{dt} = a\hat{i} + (2bt)\hat{j} + (3ct^2)\hat{k}
$$
Differentiating again yields the acceleration:
$$
\vec{a}(t) = \frac{d\vec{v}}{dt} = 0\hat{i} + (2b)\hat{j} + (6ct)\hat{k}
$$
In this specific case, the acceleration has no component in the $x$-direction, and its $z$-component increases linearly with time, while its $y$-component is constant.

### Determining the Trajectory from Velocity

The [inverse problem](@entry_id:634767)—determining the position from the velocity—is equally fundamental. Since velocity is the derivative of position, position can be found by integrating the velocity with respect to time. This process requires knowledge of an initial condition, typically the particle's position at a starting time $t_0$.

If the velocity vector $\vec{v}(t)$ is known, the position vector $\vec{r}(t)$ is given by the definite integral:
$$
\vec{r}(t) = \vec{r}(t_0) + \int_{t_0}^{t} \vec{v}(\tau) d\tau
$$
where $\vec{r}(t_0)$ is the position vector at time $t_0$, and $\tau$ is a dummy variable of integration. The integration is performed component-wise.

For instance, imagine an exploratory probe moving through a dust cloud such that its velocity is observed to be $\vec{v}(t) = \alpha \hat{i} + \beta t \hat{j} + \gamma t^2 \hat{k}$, where $\alpha$, $\beta$, and $\gamma$ are constants [@problem_id:2093264]. If the probe starts at the origin, $\vec{r}(0) = \vec{0}$, we can find its trajectory by integrating each component of the velocity from $\tau=0$ to $\tau=t$:
$$
x(t) = \int_0^t \alpha \,d\tau = \alpha t
$$
$$
y(t) = \int_0^t \beta \tau \,d\tau = \frac{1}{2}\beta t^2
$$
$$
z(t) = \int_0^t \gamma \tau^2 \,d\tau = \frac{1}{3}\gamma t^3
$$
The resulting position vector is $\vec{r}(t) = (\alpha t)\hat{i} + (\frac{1}{2}\beta t^2)\hat{j} + (\frac{1}{3}\gamma t^3)\hat{k}$. This demonstrates how the entire trajectory is determined by the history of the velocity and a single point of reference.

### Path vs. Trajectory: Eliminating the Parameter

It is important to distinguish between the **trajectory**, $\vec{r}(t)$, which describes *when* a particle is at a certain point, and the **path**, which is the static geometric curve in space that the particle follows. The path is the set of all points visited, without regard to the timing.

One way to find the equation of the path is to eliminate the parameter $t$ from the [parametric equations](@entry_id:172360) $x(t)$, $y(t)$, and $z(t)$. This typically results in an equation (or equations) that relates the coordinates $x$, $y$, and $z$ directly.

As an example, consider a particle moving in the $xy$-plane with coordinates given by $x(t) = a \cosh(\omega t)$ and $y(t) = b \sinh(\omega t)$, where $a$, $b$, and $\omega$ are positive constants [@problem_id:2093265]. To find the path, we can rearrange the equations as $\frac{x}{a} = \cosh(\omega t)$ and $\frac{y}{b} = \sinh(\omega t)$. We then employ the fundamental hyperbolic identity, $\cosh^2(u) - \sinh^2(u) = 1$. Substituting our expressions gives:
$$
\left(\frac{x}{a}\right)^2 - \left(\frac{y}{b}\right)^2 = 1
$$
This is the Cartesian equation of a hyperbola. The particle is constrained to move along one branch of this hyperbola. For $t \ge 0$, since $\cosh(\omega t) \ge 1$ and $\sinh(\omega t) \ge 0$, the particle moves along the part of the hyperbola in the first quadrant with $x \ge a$. The parameter $t$ tells us *where* on this hyperbola the particle is at any given time, while the equation describes the shape of the road it travels on.

### Parametrization from Geometric Constraints

In many mechanical systems, the path is not given a priori but is determined by physical constraints. Our task is then to find a suitable [parametrization](@entry_id:272587) for this predetermined path.

#### Paths Defined by Explicit Functions

The simplest constraint is when a particle is confined to a curve described by an explicit function, such as a bead on a wire. If a bead is constrained to move on a parabolic wire $y = \alpha x^2$ in the $xy$-plane, its position can be described using a single coordinate as the parameter [@problem_id:2093261]. Choosing the horizontal coordinate $x$ as the parameter, the [position vector](@entry_id:168381) is:
$$
\vec{r}(x) = x\hat{i} + y(x)\hat{j} = x\hat{i} + (\alpha x^2)\hat{j}
$$
Here, the path is parametrized not by time, but by a spatial coordinate. To find the velocity, we must use the [chain rule](@entry_id:147422), as $x$ is itself a function of time, $x=x(t)$:
$$
\vec{v}(t) = \frac{d\vec{r}}{dt} = \frac{d\vec{r}}{dx}\frac{dx}{dt} = \left(\frac{d}{dx}(x\hat{i} + \alpha x^2\hat{j})\right)\dot{x} = (1\hat{i} + 2\alpha x\hat{j})\dot{x}
$$
The velocity is $\vec{v} = \dot{x}\hat{i} + 2\alpha x \dot{x}\hat{j}$. The velocity depends on both the bead's location on the wire ($x$) and its horizontal speed ($\dot{x}$).

#### Paths in Standard Coordinate Systems

For paths on common geometric surfaces like cylinders or spheres, it is often far more convenient to use a coordinate system adapted to the geometry, such as cylindrical or [spherical coordinates](@entry_id:146054), and then convert back to Cartesian coordinates if needed.

For instance, a car driving up a helical ramp can be described easily in cylindrical coordinates $(R, \theta, z)$ [@problem_id:2093276]. If the ramp has a constant radius $R$ and its height $z$ increases linearly with the angle of revolution $\theta$ (i.e., $z = k\theta$), we can use $\theta$ as the parameter. The Cartesian coordinates are then derived from the standard conversion formulas $x = R\cos\theta$ and $y = R\sin\theta$. The full [parametric representation](@entry_id:173803) in the Cartesian system is:
$$
\vec{r}(\theta) = (R\cos\theta)\hat{i} + (R\sin\theta)\hat{j} + (k\theta)\hat{k}
$$
Similarly, for a particle moving on the surface of a sphere of radius $R$ [@problem_id:2093283], spherical coordinates $(r, \theta, \phi)$ are natural. If the particle is constrained to a path of constant latitude (i.e., the [polar angle](@entry_id:175682) $\theta = \theta_0$ is fixed) and orbits the $z$-axis with a constant [angular speed](@entry_id:173628) $\omega$ (so $\phi(t) = \omega t$, given an appropriate starting point), its Cartesian position is given by:
$$
\vec{r}(t) = (R\sin\theta_0 \cos(\omega t))\hat{i} + (R\sin\theta_0 \sin(\omega t))\hat{j} + (R\cos\theta_0)\hat{k}
$$
This describes a circle of radius $R\sin\theta_0$ at a constant height $z=R\cos\theta_0$.

#### Paths Defined by Intersecting Surfaces

A curve in three-dimensional space can also be defined as the intersection of two surfaces. To find a parametrization, one must first solve the system of equations for the surfaces to characterize the geometry of the intersection curve.

Consider a bead constrained to the intersection of two paraboloids, $z = x^2 + y^2$ and $z = 8 - (x^2 + y^2)$ [@problem_id:2093290]. At the intersection, both expressions for $z$ must be equal:
$$
x^2 + y^2 = 8 - (x^2 + y^2) \implies 2(x^2 + y^2) = 8 \implies x^2 + y^2 = 4
$$
Substituting this result back into the first equation gives $z=4$. The intersection is therefore a circle of radius $2$ in the horizontal plane $z=4$. This circle can be readily parametrized using an angle $t$ as the parameter:
$$
\vec{r}(t) = (2\cos t)\hat{i} + (2\sin t)\hat{j} + 4\hat{k}
$$
This provides a complete description of the path available to the bead.

### Arc Length and Natural Parametrization

The total distance a particle travels along its path between two times, $t_A$ and $t_B$, is called the **arc length**. It is found by integrating the speed $|\vec{v}(t)|$ over the time interval. A small displacement $d\vec{r}$ has a length $ds = |d\vec{r}| = |\frac{d\vec{r}}{dt}|dt = |\vec{v}(t)|dt$. The total arc length $L$ is the sum of these infinitesimal segments:
$$
L = \int_{t_A}^{t_B} ds = \int_{t_A}^{t_B} \left|\frac{d\vec{r}}{dt}\right| dt
$$
Let's apply this to the helical path $\vec{r}(\theta) = (R\cos\theta)\hat{i} + (R\sin\theta)\hat{j} + (k\theta)\hat{k}$ from before, using $\theta$ as the parameter [@problem_id:2093276]. First, we find the derivative with respect to the parameter $\theta$:
$$
\frac{d\vec{r}}{d\theta} = (-R\sin\theta)\hat{i} + (R\cos\theta)\hat{j} + k\hat{k}
$$
The magnitude of this vector is:
$$
\left|\frac{d\vec{r}}{d\theta}\right| = \sqrt{(-R\sin\theta)^2 + (R\cos\theta)^2 + k^2} = \sqrt{R^2(\sin^2\theta + \cos^2\theta) + k^2} = \sqrt{R^2 + k^2}
$$
This magnitude is constant. The total distance traveled in $N$ revolutions (from $\theta=0$ to $\theta=2\pi N$) is:
$$
L = \int_{0}^{2\pi N} \sqrt{R^2 + k^2} d\theta = \sqrt{R^2 + k^2} [\theta]_0^{2\pi N} = 2\pi N \sqrt{R^2 + k^2}
$$

This concept leads to the idea of **[reparametrization](@entry_id:176404)**, where we describe the curve using a different parameter. A particularly important choice is the arc length $s$ itself. The function $s(t)$ is the distance traveled from a reference point at $t_0$ to the point at time $t$:
$$
s(t) = \int_{t_0}^{t} \left|\frac{d\vec{r}}{d\tau}\right| d\tau
$$
If this relation can be inverted to find $t(s)$, we can substitute it back into $\vec{r}(t)$ to obtain $\vec{r}(s)$, the position vector parametrized by arc length. This is called the **natural parametrization** of the curve. A key property is that the magnitude of the [tangent vector](@entry_id:264836) with respect to arc length is always unity: $|\frac{d\vec{r}}{ds}| = 1$.

For the simple case of straight-line motion $\vec{r}(t) = (x_0 + v_x t)\hat{i} + (y_0 + v_y t)\hat{j}$ [@problem_id:2093280], the speed is constant: $|\vec{v}| = \sqrt{v_x^2 + v_y^2}$. The arc length from $t=0$ is $s(t) = \int_0^t \sqrt{v_x^2 + v_y^2} d\tau = t\sqrt{v_x^2 + v_y^2}$. Inverting gives $t = s / \sqrt{v_x^2 + v_y^2}$. Substituting this back into $\vec{r}(t)$ yields the arc length parametrization:
$$
\vec{r}(s) = \left(x_0 + \frac{v_x s}{\sqrt{v_x^2+v_y^2}}\right)\hat{i} + \left(y_0 + \frac{v_y s}{\sqrt{v_x^2+v_y^2}}\right)\hat{j}
$$
This expression gives the position of the particle after it has traveled a distance $s$ along its path.

### Advanced Topics in Parametrization

#### Closed Trajectories

A trajectory is said to be **closed** if the motion is periodic, meaning the particle returns to the same position with the same velocity after a certain time interval $T$, the period. Mathematically, $\vec{r}(t+T) = \vec{r}(t)$ for all $t$.

This often occurs in systems with oscillatory motion. Consider a particle whose motion is described by a [superposition of oscillations](@entry_id:188194) in perpendicular directions, such as $x(t) = A\cos(\omega_x t)$ and $y(t) = B\cos(\omega_y t + \phi)$ [@problem_id:2093285]. The resulting curves are known as Lissajous figures. For the path to be a closed curve, the particle's motion in both $x$ and $y$ must repeat over a common time interval. This will happen if and only if the ratio of the angular frequencies, $\omega_x / \omega_y$, is a rational number. If $\frac{\omega_x}{\omega_y} = \frac{p}{q}$ where $p$ and $q$ are integers, the $x$-motion completes $p$ cycles in the same time that the $y$-motion completes $q$ cycles, and the particle returns to its starting state, tracing a closed path.

#### Non-Standard Reparametrization

While time and arc length are common parameters, any convenient variable that uniquely specifies position along the path can be used. Sometimes, a non-obvious parameter choice can simplify a problem or arise naturally from a specific measurement scheme.

For example, consider a particle on a circle of radius $R$, whose position is tracked using a parameter $u$ derived from a stereographic-like projection [@problem_id:2093274]. A line is drawn from the point $(-R, 0)$ through the particle, and $u$ is related to where this line intersects the $y$-axis. This geometric definition leads to the [parametrization](@entry_id:272587):
$$
x(u) = R\frac{1-u^2}{1+u^2}, \quad y(u) = R\frac{2u}{1+u^2}
$$
This is a [rational parametrization](@entry_id:165009) of the circle. If the motion is given in terms of $u(t)$, we can find the velocity using the chain rule: $\vec{v} = \frac{d\vec{r}}{dt} = \frac{d\vec{r}}{du}\frac{du}{dt}$. This gives:
$$
\vec{v}(t) = \left( R\frac{-4u}{(1+u^2)^2}\hat{i} + R\frac{2(1-u^2)}{(1+u^2)^2}\hat{j} \right) \dot{u}
$$
This example highlights the versatility of [parametrization](@entry_id:272587). No matter how the path is described, the fundamental rules of calculus, particularly the [chain rule](@entry_id:147422), provide a systematic way to relate the description of motion to the physical kinematic quantities of velocity and acceleration.

In summary, path [parametrization](@entry_id:272587) is the essential language used to describe motion in mechanics. It provides a flexible and powerful bridge between the geometry of a path and the dynamics of an object moving along it. Mastering these principles is a critical step toward analyzing more complex mechanical systems.