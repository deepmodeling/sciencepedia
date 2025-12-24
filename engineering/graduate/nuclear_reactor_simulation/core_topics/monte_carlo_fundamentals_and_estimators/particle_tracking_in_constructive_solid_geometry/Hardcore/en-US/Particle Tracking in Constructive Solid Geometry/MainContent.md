## Introduction
Simulating the journey of individual particles, like neutrons and photons, through complex systems is a cornerstone of modern computational physics. In fields such as nuclear reactor analysis, [medical physics](@entry_id:158232), and [high-energy physics](@entry_id:181260), the ability to predict particle behavior with high fidelity is paramount. A significant challenge lies in representing and navigating intricate three-dimensional geometries in a way that is both mathematically rigorous and computationally efficient. This is the problem that Constructive Solid Geometry (CSG) elegantly solves, providing a powerful framework for defining complex objects and tracking particles through them.

This article serves as a comprehensive guide to the theory and practice of [particle tracking](@entry_id:190741) in CSG. We will bridge the gap between the abstract concept of geometric modeling and its concrete application in Monte Carlo transport simulations. Over the next three chapters, you will gain a deep understanding of this essential technique. First, in **"Principles and Mechanisms,"** we will dissect the core of CSG, exploring how [implicit surfaces](@entry_id:1126421) and Boolean operations define solids and how ray tracing is used to calculate a particle's path. Next, in **"Applications and Interdisciplinary Connections,"** we will broaden our scope to see how these methods are applied to solve real-world problems, from quantifying reactor performance and modeling multi-physics feedback to applications in medical imaging and semiconductor manufacturing. Finally, **"Hands-On Practices"** will provide practical exercises to reinforce these concepts, guiding you through the implementation of key algorithms. We begin our exploration by delving into the fundamental principles and mechanisms that make CSG such a robust and versatile tool.

## Principles and Mechanisms

In the preceding chapter, we introduced the fundamental role of [particle tracking](@entry_id:190741) in Monte Carlo simulations of nuclear reactors. The ability to accurately and efficiently simulate the path of a neutron or photon through complex geometries is the bedrock upon which transport calculations are built. This chapter delves into the principles and mechanisms of one of the most powerful and widely used geometric modeling techniques: **Constructive Solid Geometry (CSG)**. We will explore how complex three-dimensional objects can be rigorously defined, how a particle's trajectory is traced through them, and the critical interplay between deterministic geometric events and stochastic physical interactions.

### Geometric Representation: The Language of CSG

At its heart, CSG is a method for creating complex shapes by combining simpler ones. This approach is both intuitive and mathematically rigorous, lending itself well to computational implementation.

#### Implicit Surfaces as Primitives

The building blocks of CSG are simple, elementary shapes known as **primitives**. Common primitives include spheres, cylinders, cones, and planes. In the CSG framework, a solid primitive is not defined by a mesh of points or polygons, but rather by a single, continuous, scalar-valued function, $f(\mathbf{x})$, where $\mathbf{x}$ is a point in three-dimensional Euclidean space, $\mathbb{R}^3$. This function, known as an **[implicit surface](@entry_id:266523) function**, divides all of space into three distinct regions:

-   **The Interior:** The set of all points $\mathbf{x}$ for which $f(\mathbf{x})  0$.
-   **The Boundary:** The set of all points $\mathbf{x}$ for which $f(\mathbf{x}) = 0$. This is the surface of the primitive itself.
-   **The Exterior:** The set of all points $\mathbf{x}$ for which $f(\mathbf{x})  0$.

By convention, the solid is the union of its interior and its boundary, defined by the inequality $f(\mathbf{x}) \le 0$. This formulation is exceptionally powerful because the function $f$ does more than just define the shape; it acts as an "inside/outside" indicator for any point in space. For many common primitives, $f(\mathbf{x})$ can be formulated to represent the signed distance from the point $\mathbf{x}$ to the surface, although this is not a strict requirement.

An essential property of an [implicit surface](@entry_id:266523) is its **orientation**. For a [differentiable function](@entry_id:144590) $f(\mathbf{x})$, the [gradient vector](@entry_id:141180), $\nabla f(\mathbf{x})$, is everywhere perpendicular to the [level sets](@entry_id:151155) of $f$. Specifically, at a point $\mathbf{x}_b$ on the boundary where $f(\mathbf{x}_b) = 0$, the gradient $\nabla f(\mathbf{x}_b)$ points in the direction of the greatest increase in $f$. Given our convention that $f  0$ is inside, the [gradient vector](@entry_id:141180) naturally points from the interior toward the exterior. Therefore, the **outward unit normal** vector, $\mathbf{n}$, at a boundary point is given by normalizing the gradient:

$$
\mathbf{n} = \frac{\nabla f(\mathbf{x}_b)}{\|\nabla f(\mathbf{x}_b)\|}
$$

This provides a consistent and computationally straightforward way to determine the surface normal, which is crucial for tasks like determining whether a particle is entering or exiting a region  .

#### Boolean Operations for Building Complex Solids

While primitives are the building blocks, the true power of CSG comes from the ability to combine them using **Boolean [set operations](@entry_id:143311)**: union ($\cup$), intersection ($\cap$), and difference ($\setminus$). A complex object, such as a fuel pin surrounded by coolant in a square channel, can be described as a "tree" of these operations applied to simple primitives like cylinders and planes.

The elegant correspondence between [implicit surface](@entry_id:266523) functions and solid regions extends to these operations. If we have two primitives, $A$ and $B$, defined by $f_A(\mathbf{x}) \le 0$ and $f_B(\mathbf{x}) \le 0$ respectively, we can define their combinations:

-   **Intersection ($\mathcal{A} \cap \mathcal{B}$):** A point $\mathbf{x}$ is in the intersection if it is in *both* $A$ and $B$. This requires satisfying both $f_A(\mathbf{x}) \le 0$ and $f_B(\mathbf{x}) \le 0$. This is equivalent to the single condition $\max(f_A(\mathbf{x}), f_B(\mathbf{x})) \le 0$.

-   **Union ($\mathcal{A} \cup \mathcal{B}$):** A point $\mathbf{x}$ is in the union if it is in $A$ *or* in $B$. This requires satisfying $f_A(\mathbf{x}) \le 0$ or $f_B(\mathbf{x}) \le 0$. This is equivalent to the single condition $\min(f_A(\mathbf{x}), f_B(\mathbf{x})) \le 0$.

-   **Difference ($\mathcal{A} \setminus \mathcal{B}$):** A point $\mathbf{x}$ is in the difference if it is in $A$ *and not* in $B$. This is equivalent to the intersection of $A$ with the complement of $B$, denoted $B^c$. The complement of $B$ is the set of points where $f_B(\mathbf{x})  0$, which can be defined using the function $-f_B(\mathbf{x})  0$. Thus, the difference $\mathcal{A} \setminus \mathcal{B}$ can be represented by the [composite function](@entry_id:151451) $\max(f_A(\mathbf{x}), -f_B(\mathbf{x})) \le 0$.

This functional representation allows any complex CSG object, no matter how many operations are in its tree, to be evaluated with a single function for an inside/outside test. It is noteworthy that while functions like `max` and `min` are not differentiable everywhere, this does not pose a problem for the inside/outside classification itself  .

### Particle Kinematics: The Ray Tracing Paradigm

Having defined the static geometry, we now turn to the dynamics of particle motion. In the absence of external fields, neutral particles like neutrons and photons travel in straight lines between collisions. This simple kinematic model is the foundation of [ray tracing](@entry_id:172511).

#### The Particle's Path as a Parametric Ray

A particle's trajectory can be described by a **parametric ray equation**:

$$
\mathbf{r}(t) = \mathbf{r}_0 + t\mathbf{u}
$$

Here, $\mathbf{r}_0$ is the particle's starting position, $\mathbf{u}$ is a [unit vector](@entry_id:150575) representing its direction of travel, and $t$ is the scalar path length traveled from $\mathbf{r}_0$. As $t$ increases from $0$, the point $\mathbf{r}(t)$ traces out the [forward path](@entry_id:275478) of the particle.

#### Finding the Distance to a Single Surface

The core geometric query in [particle tracking](@entry_id:190741) is: "How far must the particle travel along its current path to hit a boundary?" This distance is found by determining the value of $t$ for which the particle's position $\mathbf{r}(t)$ lies on a surface. For a primitive defined by $f(\mathbf{x})=0$, we solve the equation $f(\mathbf{r}(t)) = 0$ for $t$.

Let's derive this for our key primitives :

-   **Plane:** A plane can be defined by $f(\mathbf{x}) = \mathbf{n} \cdot \mathbf{x} - d = 0$, where $\mathbf{n}$ is the [unit normal vector](@entry_id:178851) and $d$ is the signed distance from the origin. Substituting the ray equation:
    $$
    \mathbf{n} \cdot (\mathbf{r}_0 + t\mathbf{u}) - d = 0
    $$
    Solving this linear equation for $t$ yields:
    $$
    t = \frac{d - \mathbf{n} \cdot \mathbf{r}_0}{\mathbf{n} \cdot \mathbf{u}}
    $$
    A solution exists if $\mathbf{n} \cdot \mathbf{u} \neq 0$, meaning the ray is not parallel to the plane. We are only interested in forward intersections, so we require $t  0$.

-   **Sphere:** A sphere centered at $\mathbf{c}$ with radius $R$ is defined by $f(\mathbf{x}) = \|\mathbf{x} - \mathbf{c}\|^2 - R^2 = 0$. Substituting the ray equation gives:
    $$
    \|(\mathbf{r}_0 - \mathbf{c}) + t\mathbf{u}\|^2 - R^2 = 0
    $$
    Expanding this and using the fact that $\|\mathbf{u}\|^2 = 1$ leads to a quadratic equation of the form $At^2 + Bt + C = 0$:
    $$
    t^2 + 2(\mathbf{u} \cdot (\mathbf{r}_0 - \mathbf{c}))t + (\|\mathbf{r}_0 - \mathbf{c}\|^2 - R^2) = 0
    $$
    The solutions for $t$ are found using the quadratic formula. Real solutions exist if the [discriminant](@entry_id:152620) is non-negative. Typically, a ray can intersect a sphere at two points (entry and exit).

-   **Infinite Cylinder (z-aligned):** An infinite cylinder of radius $R$ aligned with the z-axis is defined by $f(\mathbf{x}) = x^2 + y^2 - R^2 = 0$. Let $\mathbf{r}_0 = (x_0, y_0, z_0)$ and $\mathbf{u} = (u_x, u_y, u_z)$. Substituting the ray's components gives:
    $$
    (x_0 + tu_x)^2 + (y_0 + tu_y)^2 - R^2 = 0
    $$
    Expanding and collecting terms in $t$ again yields a quadratic equation:
    $$
    (u_x^2 + u_y^2)t^2 + 2(x_0 u_x + y_0 u_y)t + (x_0^2 + y_0^2 - R^2) = 0
    $$
    This is solved for $t$ in the same manner as the sphere. If the ray is parallel to the cylinder axis ($u_x=u_y=0$), this equation degenerates, and an intersection only occurs if the ray lies exactly on the surface.

#### Determining Entry vs. Exit

Once an intersection distance $t$ is found, we often need to know if the particle is entering or exiting the solid. This is determined by the relationship between the particle's velocity vector $\mathbf{v}$ (or [direction vector](@entry_id:169562) $\mathbf{u}$) and the surface's outward normal $\mathbf{n}$ at the point of intersection.

The rate of change of the implicit function $f$ along the particle's path is given by the [chain rule](@entry_id:147422): $\frac{d}{dt}f(\mathbf{r}(t)) = \nabla f(\mathbf{r}(t)) \cdot \mathbf{u}$.

-   If a particle is **entering** a region defined by $f  0$, the value of $f$ must be decreasing as it crosses the boundary. This means $\frac{d}{dt}f  0$, which implies $\nabla f \cdot \mathbf{u}  0$, or $\mathbf{n} \cdot \mathbf{u}  0$.
-   If a particle is **exiting** the region, the value of $f$ must be increasing, transitioning from negative to positive. This means $\frac{d}{dt}f  0$, which implies $\mathbf{n} \cdot \mathbf{u}  0$.
-   If $\mathbf{n} \cdot \mathbf{u} = 0$, the particle's path is tangent to the surface at the point of intersection.

This simple dot product test provides a robust and universal way to classify boundary crossings  .

### The Core Tracking Algorithm

With the tools to define geometry and calculate ray-surface intersections, we can now formulate the main loop of a [particle tracking algorithm](@entry_id:1129400).

#### Tracking Through a Composite Solid

For a geometry composed of many primitive surfaces, a particle's next geometric event is determined by finding the nearest boundary it will cross. The most straightforward algorithm, often called the "naive" or "brute-force" method, involves a competition:

1.  For the particle at $\mathbf{r}_0$ with direction $\mathbf{u}$, calculate the intersection distance $t_i$ to *every* primitive surface $i$ in the CSG model.
2.  Discard any non-physical solutions (e.g., negative distances, imaginary solutions).
3.  The distance to the nearest boundary, $S_b$, is the minimum of all remaining positive distances: $S_b = \min_i(t_i)$.
4.  The particle is advanced by this distance $S_b$ to the position $\mathbf{r}(S_b)$ on the boundary.

Let's consider a concrete example. A neutron starts at $\mathbf{p}_0 = (0, 0, 5)$ cm and travels in the direction of $\mathbf{v}=(3, 2, 3)$ within a region $\mathcal{R}$. The region is a finite cylinder ($x^2+y^2 \le 100$, $0 \le z \le 20$) with a spherical void subtracted from its center (center at $(3,2,8)$, radius $2$). The starting point is confirmed to be inside $\mathcal{R}$. To find the first boundary it hits, we calculate the distance to all three primitive surfaces along its path :
-   **Distance to cylinder wall:** Solving the quadratic equation gives $t_{cyl} \approx 13.0$ cm. (The exact value is $10\sqrt{22/13}$.)
-   **Distance to slab planes:** The particle moves in the $+z$ direction from $z=5$. It will miss the $z=0$ plane in the forward direction. The distance to the $z=20$ plane is $t_z = 5\sqrt{22} \approx 23.4$ cm.
-   **Distance to spherical void:** Solving the quadratic equation gives two roots, corresponding to entering and exiting the sphere. Since the particle starts outside the void, the first intersection is the smaller positive root, $t_{sph} = \sqrt{22}-2 \approx 2.69$ cm.

Comparing these distances, $t^{\ast} = \min(13.0, 23.4, 2.69) = 2.69$ cm. The first event is hitting the boundary of the spherical void.

#### An Alternative View: Interval Algebra

A more abstract and powerful way to conceptualize CSG tracking is through **interval algebra**. The problem of finding where a 3D ray is inside a 3D solid can be transformed into finding a 1D set of intervals along the ray's parameter $t$. For each primitive, we solve the inequality $f(\mathbf{r}(t)) \le 0$ to find the set of $t$ values for which the ray is inside. This set is typically a single interval $[t_{start}, t_{end})$ or a union of such intervals.

The Boolean operations on the 3D solids then correspond directly to [set operations](@entry_id:143311) on these 1D interval sets. For example, to find the ray's path through $A \cap B$, we compute the interval set for $A$ ($\mathcal{I}_A$) and for $B$ ($\mathcal{I}_B$), and then find their intersection, $\mathcal{I}_{A \cap B} = \mathcal{I}_A \cap \mathcal{I}_B$. This can be implemented with algorithms that "sweep" along the t-axis. After the final interval set for the entire CSG object is computed, finding the first boundary crossing from a point outside the object is as simple as finding the smallest positive start-point of any interval in the set .

#### The Next-Event Competition

In a physical simulation, a particle's flight does not end only at geometric boundaries. It can also undergo a **collision** with the nuclei of the material it is traversing. The core of a Monte Carlo transport simulation is the competition between these two [mutually exclusive events](@entry_id:265118):
1.  **Geometric Boundary Crossing:** A deterministic event. The distance to the nearest boundary, $S_b$, is calculated as described above.
2.  **Physical Collision:** A stochastic event. In a homogeneous medium with a total macroscopic cross section $\Sigma_t$, the probability of a particle traveling a distance $s$ without a collision is $e^{-\Sigma_t s}$. The distance to the next collision, $S_c$, is a random variable sampled from this exponential distribution. Using [inverse transform sampling](@entry_id:139050), this distance can be sampled from a uniform random number $\xi \in (0,1)$ as $S_c = -\ln(\xi)/\Sigma_t$.

The next event that actually occurs is the one that happens first. The particle is therefore advanced by a distance $s^{\star} = \min(S_c, S_b)$.

-   If $s^{\star} = S_c$ (i.e., $S_c  S_b$), the particle undergoes a collision at its new position. The simulation then processes the physics of the collision (e.g., scattering, absorption).
-   If $s^{\star} = S_b$ (i.e., $S_b \le S_c$), the particle reaches the boundary. The simulation processes the boundary crossing, which typically involves identifying the new region and its material properties.

A critical rule follows from this logic: if a boundary is crossed, the particle enters a new medium, which may have a different cross section $\Sigma_t'$. The previously sampled collision distance $S_c$ was based on the old cross section and is now invalid. Therefore, after any boundary crossing, the old value of $S_c$ must be discarded, and a new collision distance must be sampled using the properties of the new region. The [memoryless property](@entry_id:267849) of the exponential distribution applies *within* a homogeneous medium, not across changes in the medium  .

### Practical Implementation and Numerical Robustness

Translating these mathematical principles into a reliable computer program requires careful attention to the limitations of [floating-point arithmetic](@entry_id:146236). An algorithm that is mathematically perfect can fail in practice if it is not numerically robust.

#### Robust Point Classification

A common task is to determine if a point is inside, outside, or on the boundary of a CSG region. A naive test of $f(\mathbf{x}) = 0$ is prone to failure due to [representation error](@entry_id:171287). A robust approach defines a **tolerance band** around the surface. Given a small tolerance $\varepsilon  0$, we can classify a point with respect to a primitive using a [three-state logic](@entry_id:176620):

-   **Inside (Code 1):** $f(\mathbf{x})  -\varepsilon$ (safely inside)
-   **On Boundary (Code 0):** $|f(\mathbf{x})| \le \varepsilon$ (on or near the boundary)
-   **Outside (Code -1):** $f(\mathbf{x})  \varepsilon$ (safely outside)

This [three-state logic](@entry_id:176620) can be propagated through the CSG tree. For example, the classification for a difference $A \setminus B$ becomes $c_M = \min(c_A, -c_B)$, providing a robust way to classify a point's location with respect to any composite object .

#### Robust Ray Intersection

The calculation of intersection distances is also fraught with numerical peril.

-   **Quadratic Equation Stability:** When solving the quadratic equation for a sphere or cylinder intersection, the standard formula can suffer from **[catastrophic cancellation](@entry_id:137443)** if it involves subtracting two nearly equal large numbers. This often happens when a particle starts very close to a surface. Using alternative but mathematically equivalent formulas, such as those derived from Vieta's formulas, can mitigate this issue and provide stable results even in near-degenerate configurations .

-   **Handling Tangency:** A special case arises when a particle's path is tangent to a surface. Mathematically, this corresponds to the [discriminant](@entry_id:152620) of the quadratic intersection equation being exactly zero ($\Delta=0$). In this situation, the ray touches the surface at a single point but does not cross it. Therefore, a [tangential contact](@entry_id:201927) is **not a crossing event**. Numerically, due to floating-point errors, a true tangent may yield a discriminant that is slightly positive or slightly negative. A robust policy is to treat any intersection where the discriminant is smaller than some small tolerance ($\Delta \le \tau$) as a non-crossing event. To ensure the simulation progresses, the particle should be advanced slightly past the [point of tangency](@entry_id:172885) without changing its current region identity .

-   **Distance Tolerances:** If a particle starts exactly on a boundary, a naive calculation might return an intersection distance of $t=0$. If the particle is not moved robustly, it may get "stuck" in an infinite loop, repeatedly hitting the same surface at zero distance. A robust algorithm applies a small, physically scaled tolerance to computed distances, treating any result smaller than the tolerance as an immediate, zero-distance event and ensuring the particle is placed definitively in the new region .

#### Algorithmic Complexity and Acceleration Structures

The naive tracking algorithm, which tests a ray against every one of the $M$ primitive surfaces in a model, has a [computational complexity](@entry_id:147058) that scales linearly with the number of surfaces. Its per-step cost is $\Theta(M)$. For complex reactor models with millions of surfaces, this is computationally prohibitive.

To overcome this, production-level Monte Carlo codes employ **spatial acceleration structures**. A common choice is a **Bounding Volume Hierarchy (BVH)**, which is a tree structure where geometric primitives are recursively grouped into larger bounding boxes (typically Axis-Aligned Bounding Boxes, or AABBs). When tracing a ray, the algorithm first tests against these simple bounding boxes. If a ray misses a [bounding box](@entry_id:635282), the entire group of primitives inside it can be skipped, dramatically pruning the number of expensive [ray-surface intersection](@entry_id:1130598) tests.

For well-constructed BVHs and typical ray distributions, the expected number of nodes that must be visited scales logarithmically with the number of surfaces, leading to an expected per-step cost of $\Theta(\log M)$. However, it is important to note that this is an average-case performance. In worst-case scenarios, such as with highly pathological geometries or adversarial ray directions, the BVH's pruning power can be defeated, and the performance can degrade back to $\Theta(M)$ .

This chapter has laid out the essential principles of [particle tracking](@entry_id:190741) in Constructive Solid Geometry, from the mathematical definition of solids to the practical challenges of robust and efficient implementation. The interplay of deterministic geometry and stochastic physics, governed by the "next-event" competition, is the engine that drives the Monte Carlo simulation forward, one particle step at a time.