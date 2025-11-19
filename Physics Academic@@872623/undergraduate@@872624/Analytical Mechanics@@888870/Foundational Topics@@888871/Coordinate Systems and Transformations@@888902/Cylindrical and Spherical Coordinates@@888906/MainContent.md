## Introduction
While the Cartesian coordinate system offers a straightforward framework for many mechanics problems, it becomes cumbersome when dealing with systems that possess natural rotational or spherical symmetry. Describing a planet's orbit or the motion of a pendulum in x, y, and z coordinates can obscure the fundamental physics with needlessly complex equations. Cylindrical and spherical coordinates provide an elegant and powerful alternative, aligning the mathematical description with the [intrinsic geometry](@entry_id:158788) of the problem. This article addresses the challenge of moving beyond static Cartesian vectors to a dynamic framework where the [coordinate basis](@entry_id:270149) vectors themselves change with a particle's position. By mastering this concept, you will unlock a more intuitive and efficient method for analyzing a vast range of physical phenomena.

This guide will walk you through the essential aspects of these curvilinear systems. The first chapter, **"Principles and Mechanisms"**, lays the groundwork by deriving the expressions for position, velocity, and acceleration, and explains the physical meaning of terms like centripetal and Coriolis acceleration. The second chapter, **"Applications and Interdisciplinary Connections"**, demonstrates the power of these tools in solving real-world problems in [celestial mechanics](@entry_id:147389), electromagnetism, and even quantum theory. Finally, **"Hands-On Practices"** provides a set of targeted problems to solidify your understanding and build practical skills. The journey begins by mastering the fundamental principles and mechanisms of [kinematics](@entry_id:173318) in these powerful coordinate systems.

## Principles and Mechanisms

The Cartesian coordinate system, with its fixed, mutually orthogonal basis vectors, provides the simplest arena for applying the laws of mechanics. However, the physical reality of many systems, from [planetary orbits](@entry_id:179004) to the motion of a bead on a wire, often possesses inherent symmetries—cylindrical or spherical—that are clumsily described in a Cartesian framework. Adopting a coordinate system that respects the natural geometry of a problem can lead to profound simplifications. This chapter delves into the principles and mechanisms of using cylindrical and spherical coordinates in mechanics. We will discover that the convenience of a geometrically-aligned coordinate system comes at the price of mathematical complexity: the basis vectors themselves become functions of position, and therefore, of time for a moving particle. Mastering the kinematics—the description of motion—in these systems is the crucial first step toward unlocking their full power in dynamics.

### The Nature of Curvilinear Basis Vectors

In contrast to the static Cartesian basis vectors $(\hat{i}, \hat{j}, \hat{k})$, which point in the same directions throughout all of space, the basis vectors of cylindrical and spherical [coordinate systems](@entry_id:149266) are **local** and **position-dependent**. Their directions are defined relative to the position of the particle itself.

For a point $P$ described by **[cylindrical coordinates](@entry_id:271645)** $(\rho, \phi, z)$, the basis vectors are:
-   $\hat{\rho}$: Points radially outward from the $z$-axis, perpendicular to it. Its direction is determined by the [azimuthal angle](@entry_id:164011) $\phi$.
-   $\hat{\phi}$: Points in the direction of increasing $\phi$, tangent to the circle of radius $\rho$ centered on the $z$-axis. It is always perpendicular to $\hat{\rho}$ and $\hat{z}$.
-   $\hat{z}$: Identical to the Cartesian $\hat{k}$, pointing along the [axis of symmetry](@entry_id:177299).

Their relationship to the fixed Cartesian basis can be expressed as [@problem_id:2043538]:
$$ \hat{\rho} = \cos(\phi)\hat{i} + \sin(\phi)\hat{j} $$
$$ \hat{\phi} = -\sin(\phi)\hat{i} + \cos(\phi)\hat{j} $$
$$ \hat{z} = \hat{k} $$
As a particle moves, its angle $\phi$ may change, causing $\hat{\rho}$ and $\hat{\phi}$ to rotate in the $xy$-plane.

For a point $P$ described by **[spherical coordinates](@entry_id:146054)** $(r, \theta, \phi)$, the basis vectors are:
-   $\hat{r}$: Points radially outward from the origin. Its direction depends on both $\theta$ and $\phi$.
-   $\hat{\theta}$: Points in the direction of increasing [polar angle](@entry_id:175682) $\theta$, tangent to the meridian line passing through the particle.
-   $\hat{\phi}$: Points in the direction of increasing [azimuthal angle](@entry_id:164011) $\phi$, tangent to the line of latitude passing through the particle.

These three vectors also form a right-handed [orthonormal set](@entry_id:271094), $(\hat{r}, \hat{\theta}, \hat{\phi})$. Their expressions in the Cartesian basis are more complex, depending on two angles [@problem_id:2043511]:
$$ \hat{r} = \sin\theta\cos\phi\,\hat{i} + \sin\theta\sin\phi\,\hat{j} + \cos\theta\,\hat{k} $$
$$ \hat{\theta} = \cos\theta\cos\phi\,\hat{i} + \cos\theta\sin\phi\,\hat{j} - \sin\theta\,\hat{k} $$
$$ \hat{\phi} = -\sin\phi\,\hat{i} + \cos\phi\,\hat{j} $$
For any motion that changes $\theta$ or $\phi$, all three spherical basis vectors will change their orientation. This time-dependence is the central mechanism responsible for the unique kinematic terms that appear in these systems.

### Kinematics in Cylindrical Coordinates: Velocity and Acceleration

To describe motion, we must compute the velocity $\vec{v} = d\vec{r}/dt$ and acceleration $\vec{a} = d\vec{v}/dt$. Let's begin with the cylindrical system. The [position vector](@entry_id:168381) of a particle is written as:
$$ \vec{r}(t) = \rho(t)\hat{\rho}(\phi(t)) + z(t)\hat{z} $$
To find the velocity, we apply the product rule for differentiation:
$$ \vec{v} = \frac{d\vec{r}}{dt} = \frac{d\rho}{dt}\hat{\rho} + \rho\frac{d\hat{\rho}}{dt} + \frac{dz}{dt}\hat{z} $$
Since $\hat{z}$ is constant, its time derivative is zero. However, $\hat{\rho}$ depends on $\phi(t)$, so we must use the [chain rule](@entry_id:147422):
$$ \frac{d\hat{\rho}}{dt} = \frac{d\hat{\rho}}{d\phi} \frac{d\phi}{dt} = \dot{\phi} \frac{d}{d\phi}(\cos\phi\,\hat{i} + \sin\phi\,\hat{j}) = \dot{\phi}(-\sin\phi\,\hat{i} + \cos\phi\,\hat{j}) $$
We immediately recognize the term in parentheses as the azimuthal [unit vector](@entry_id:150575), $\hat{\phi}$. Therefore:
$$ \frac{d\hat{\rho}}{dt} = \dot{\phi}\hat{\phi} $$
A similar calculation for $\hat{\phi}$ [@problem_id:2043538] yields:
$$ \frac{d\hat{\phi}}{dt} = \frac{d\hat{\phi}}{d\phi} \fracd\phi}{dt} = \dot{\phi} \frac{d}{d\phi}(-\sin\phi\,\hat{i} + \cos\phi\,\hat{j}) = \dot{\phi}(-\cos\phi\,\hat{i} - \sin\phi\,\hat{j}) = -\dot{\phi}\hat{\rho} $$
Substituting the derivative of $\hat{\rho}$ back into the velocity expression gives the general formula for velocity in [cylindrical coordinates](@entry_id:271645):
$$ \vec{v} = \dot{\rho}\hat{\rho} + \rho\dot{\phi}\hat{\phi} + \dot{z}\hat{z} $$
The components represent the speed in the radial direction ($v_\rho = \dot{\rho}$), the transverse or azimuthal direction ($v_\phi = \rho\dot{\phi}$), and the axial direction ($v_z = \dot{z}$).

The true complexity and power of the method become apparent when we calculate the acceleration by differentiating the velocity vector:
$$ \vec{a} = \frac{d\vec{v}}{dt} = \frac{d}{dt}(\dot{\rho}\hat{\rho} + \rho\dot{\phi}\hat{\phi} + \dot{z}\hat{z}) $$
Applying the product rule to each term and grouping by basis vector:
$$ \vec{a} = (\ddot{\rho}\hat{\rho} + \dot{\rho}\dot{\hat{\rho}}) + (\dot{\rho}\dot{\phi}\hat{\phi} + \rho\ddot{\phi}\hat{\phi} + \rho\dot{\phi}\dot{\hat{\phi}}) + \ddot{z}\hat{z} $$
Now, we substitute our expressions for $\dot{\hat{\rho}}$ and $\dot{\hat{\phi}}$:
$$ \vec{a} = (\ddot{\rho}\hat{\rho} + \dot{\rho}(\dot{\phi}\hat{\phi})) + (\dot{\rho}\dot{\phi}\hat{\phi} + \rho\ddot{\phi}\hat{\phi} + \rho\dot{\phi}(-\dot{\phi}\hat{\rho})) + \ddot{z}\hat{z} $$
Collecting components for each [basis vector](@entry_id:199546) gives the full acceleration formula:
$$ \vec{a} = (\ddot{\rho} - \rho\dot{\phi}^2)\hat{\rho} + (\rho\ddot{\phi} + 2\dot{\rho}\dot{\phi})\hat{\phi} + \ddot{z}\hat{z} $$
Each term in this expression has a distinct physical interpretation:
-   $\ddot{\rho}\hat{\rho}$: The familiar linear acceleration in the radial direction.
-   $-\rho\dot{\phi}^2\hat{\rho}$: The **centripetal acceleration**, directed inward toward the [center of curvature](@entry_id:270032). It is present even if the particle moves in a circle at a constant speed.
-   $\rho\ddot{\phi}\hat{\phi}$: The **[tangential acceleration](@entry_id:173884)**, arising from a change in the magnitude of the angular velocity.
-   $2\dot{\rho}\dot{\phi}\hat{\phi}$: The **Coriolis acceleration**, a more subtle term that arises only when there is simultaneous motion in both the radial ($\dot{\rho}$) and angular ($\dot{\phi}$) directions. For an observer in a [rotating frame](@entry_id:155637), this term is experienced as a "fictitious" force. For instance, an engineer walking radially outward on a rotating space station with speed $v = \dot{\rho}$ would experience a Coriolis acceleration of magnitude $2v\omega$, where $\omega = \dot{\phi}$ is the station's [angular velocity](@entry_id:192539) [@problem_id:2043532].

Consider a particle moving in a helix, described in Cartesian coordinates as $x(t) = R\cos(\omega t)$, $y(t) = R\sin(\omega t)$, and $z(t) = v_z t$ [@problem_id:2043553]. In cylindrical coordinates, this motion is simply $\rho(t) = R$, $\phi(t) = \omega t$, and $z(t) = v_z t$. The time derivatives are $\dot{\rho}=0, \ddot{\rho}=0$; $\dot{\phi}=\omega, \ddot{\phi}=0$; and $\dot{z}=v_z, \ddot{z}=0$. Plugging these into the acceleration formula yields:
$$ \vec{a} = (0 - R\omega^2)\hat{\rho} + (R \cdot 0 + 2 \cdot 0 \cdot \omega)\hat{\phi} + 0\hat{z} = -R\omega^2\hat{\rho} $$
The result is elegant and intuitive: the only acceleration is the familiar centripetal acceleration, directed radially inward, required to keep the particle in its circular path in the $xy$-plane.

### Kinematics in Spherical Coordinates: Velocity and Acceleration

The procedure for [spherical coordinates](@entry_id:146054) follows the same logic, although the derivatives are more cumbersome. The position vector is simply $\vec{r} = r\hat{r}$. Its time derivative is:
$$ \vec{v} = \frac{d\vec{r}}{dt} = \dot{r}\hat{r} + r\dot{\hat{r}} $$
To proceed, we need the time derivatives of all three spherical basis vectors. This involves repeated application of the [chain rule](@entry_id:147422). For instance, to find $\dot{\hat{\theta}}$ [@problem_id:2043511], we differentiate its Cartesian representation with respect to time:
$$ \dot{\hat{\theta}} = \frac{d}{dt}(\cos\theta\cos\phi\,\hat{i} + \cos\theta\sin\phi\,\hat{j} - \sin\theta\,\hat{k}) $$
This involves terms with $\dot{\theta}$ and $\dot{\phi}$. After a careful calculation and projection onto the spherical basis vectors, one finds that $\dot{\hat{\theta}} \cdot \hat{\theta} = 0$, $\dot{\hat{\theta}} \cdot \hat{r} = -\dot{\theta}$, and $\dot{\hat{\theta}} \cdot \hat{\phi} = \dot{\phi}\cos\theta$. This leads to the expression:
$$ \dot{\hat{\theta}} = -\dot{\theta}\hat{r} + \dot{\phi}\cos\theta\hat{\phi} $$
Similar, though lengthy, calculations yield the other derivatives:
$$ \dot{\hat{r}} = \dot{\theta}\hat{\theta} + \dot{\phi}\sin\theta\hat{\phi} $$
$$ \dot{\hat{\phi}} = -(\dot{\phi}\sin\theta)\hat{r} - (\dot{\phi}\cos\theta)\hat{\theta} $$
Substituting the expression for $\dot{\hat{r}}$ into the velocity equation gives the general velocity vector in [spherical coordinates](@entry_id:146054):
$$ \vec{v} = \dot{r}\hat{r} + r(\dot{\theta}\hat{\theta} + \dot{\phi}\sin\theta\hat{\phi}) = \dot{r}\hat{r} + r\dot{\theta}\hat{\theta} + r\sin\theta\dot{\phi}\hat{\phi} $$
The three terms represent the components of velocity in the radial, polar, and azimuthal directions, respectively.

Differentiating this velocity vector one more time—a significant algebraic exercise—yields the acceleration vector. We state the result without derivation:
$$ a_r = \ddot{r} - r\dot{\theta}^2 - r\dot{\phi}^2\sin^2\theta $$
$$ a_\theta = r\ddot{\theta} + 2\dot{r}\dot{\theta} - r\dot{\phi}^2\sin\theta\cos\theta $$
$$ a_\phi = r\ddot{\phi}\sin\theta + 2\dot{r}\dot{\phi}\sin\theta + 2r\dot{\theta}\dot{\phi}\cos\theta $$
While formidable, this formula is the direct consequence of the changing basis vectors and the [product rule](@entry_id:144424). The terms again represent generalized centripetal and Coriolis-type accelerations.

### Representing Physical Laws in Curvilinear Systems

A physical vector, such as a force or velocity, is an entity independent of the coordinate system used to describe it. However, its *components* are entirely dependent on the chosen basis. Transforming vector components between [coordinate systems](@entry_id:149266) is a fundamental skill.

Suppose a probe's velocity is known in spherical components, $\vec{v} = v_r\hat{r} + v_\theta\hat{\theta} + v_\phi\hat{\phi}$. To find its component in a Cartesian direction, say the Northward ($+y$) direction, we compute the dot product $\vec{v} \cdot \hat{y}$ [@problem_id:2043512]. This requires knowing the dot products of the basis vectors, such as $\hat{r} \cdot \hat{y} = \sin\theta\sin\phi$. The full projection is:
$$ v_y = (\vec{v} \cdot \hat{y}) = v_r(\hat{r} \cdot \hat{y}) + v_\theta(\hat{\theta} \cdot \hat{y}) + v_\phi(\hat{\phi} \cdot \hat{y}) $$
$$ v_y = v_r\sin\theta\sin\phi + v_\theta\cos\theta\sin\phi + v_\phi\cos\phi $$

Conversely, we often need to express a force given in Cartesian terms within a curvilinear system. Consider a uniform gravitational field near the Earth's surface, $\vec{g} = -g\hat{k}$ [@problem_id:2043535]. To find its spherical components $(g_r, g_\theta, g_\phi)$, we project $\vec{g}$ onto the spherical basis vectors:
$$ g_r = \vec{g} \cdot \hat{r} = (-g\hat{k}) \cdot (\sin\theta\cos\phi\hat{i} + \sin\theta\sin\phi\hat{j} + \cos\theta\hat{k}) = -g\cos\theta $$
$$ g_\theta = \vec{g} \cdot \hat{\theta} = (-g\hat{k}) \cdot (\cos\theta\cos\phi\hat{i} + \cos\theta\sin\phi\hat{j} - \sin\theta\hat{k}) = g\sin\theta $$
$$ g_\phi = \vec{g} \cdot \hat{\phi} = (-g\hat{k}) \cdot (-\sin\phi\hat{i} + \cos\phi\hat{j}) = 0 $$
So, $\vec{g} = -g\cos\theta\hat{r} + g\sin\theta\hat{\theta}$. This shows a key principle: a constant vector field can have position-dependent components in a curvilinear coordinate system.

The true value of these systems is revealed when the force itself has a simple geometry. A classic example is a central force, such as the idealized [spring force](@entry_id:175665) $\vec{F} = -k\vec{r} = -k(x\hat{i} + y\hat{j} + z\hat{k})$ [@problem_id:2043489]. In spherical coordinates, the [position vector](@entry_id:168381) is simply $\vec{r} = r\hat{r}$. The force vector immediately simplifies to:
$$ \vec{F} = -kr\hat{r} $$
This means the force has only one non-zero component, $F_r = -kr$, with $F_\theta=0$ and $F_\phi=0$. The complex interplay of Cartesian components is reduced to a single, intuitive radial component, greatly simplifying the [equations of motion](@entry_id:170720).

### Scalar Invariants: The Case of Kinetic Energy

Scalar quantities, like energy, do not have directional components and are therefore invariant under [coordinate transformations](@entry_id:172727). Their *expressions*, however, do change. The kinetic energy of a [point mass](@entry_id:186768) $m$ is $T = \frac{1}{2}mv^2$. The squared speed $v^2 = \vec{v} \cdot \vec{v}$ can be calculated in any coordinate system.

In [cylindrical coordinates](@entry_id:271645), using the velocity vector $\vec{v} = \dot{\rho}\hat{\rho} + \rho\dot{\phi}\hat{\phi} + \dot{z}\hat{z}$ and the [orthonormality](@entry_id:267887) of the basis, we find:
$$ v^2 = \vec{v} \cdot \vec{v} = \dot{\rho}^2 + (\rho\dot{\phi})^2 + \dot{z}^2 $$
The kinetic energy is therefore:
$$ T = \frac{1}{2}m(\dot{\rho}^2 + \rho^2\dot{\phi}^2 + \dot{z}^2) $$
This formula can be applied directly to problems where the motion is specified in cylindrical coordinates, such as that of a robotic probe with prescribed radial, angular, and vertical motions [@problem_id:2043533].

In spherical coordinates, we can find $v^2$ by dotting the spherical velocity vector with itself. An alternative, elegant approach is to consider the infinitesimal squared displacement, or **line element**, $ds^2$. In Cartesian coordinates, $ds^2 = dx^2+dy^2+dz^2$. By transforming the [differentials](@entry_id:158422), one can show that in spherical coordinates [@problem_id:2043488]:
$$ ds^2 = dr^2 + r^2 d\theta^2 + r^2\sin^2\theta d\phi^2 $$
The squared speed is the rate of change of path length, $v^2 = (ds/dt)^2$. Dividing the line element by $dt^2$ gives:
$$ v^2 = \dot{r}^2 + r^2\dot{\theta}^2 + r^2\sin^2\theta\dot{\phi}^2 $$
This yields the expression for kinetic energy in [spherical coordinates](@entry_id:146054), a cornerstone of [analytical mechanics](@entry_id:166738), especially in the Lagrangian formulation:
$$ T = \frac{1}{2}m(\dot{r}^2 + r^2\dot{\theta}^2 + r^2\sin^2\theta\dot{\phi}^2) $$

### From Kinematics to Dynamics: Equations of Motion

With expressions for force and acceleration components, we can apply Newton's Second Law, $\vec{F} = m\vec{a}$, component by component. For a [central force](@entry_id:160395) where $\vec{F} = F_r(r)\hat{r}$, the equations of motion in spherical coordinates become:
$$ F_r(r) = m(\ddot{r} - r\dot{\theta}^2 - r\dot{\phi}^2\sin^2\theta) $$
$$ 0 = m(r\ddot{\theta} + 2\dot{r}\dot{\theta} - r\dot{\phi}^2\sin\theta\cos\theta) $$
$$ 0 = m(r\ddot{\phi}\sin\theta + 2\dot{r}\dot{\phi}\sin\theta + 2r\dot{\theta}\dot{\phi}\cos\theta) $$
While these equations may appear daunting, they often lead to powerful conclusions, such as conservation laws.

Consider a particle whose acceleration is observed to be purely radial and directed toward the origin: $\vec{a} = -k\hat{r}$ for some positive constant $k$ [@problem_id:2043514]. This implies that the [net force](@entry_id:163825) on the particle is central, $\vec{F} = m\vec{a} = -mk\hat{r}$. The torque on this particle about the origin is:
$$ \vec{\tau} = \vec{r} \times \vec{F} = (r\hat{r}) \times (-mk\hat{r}) = \vec{0} $$
Since torque is the time rate of change of angular momentum ($\vec{\tau} = d\vec{L}/dt$), a zero torque implies that the particle's angular momentum vector $\vec{L}$ is conserved.

If the vector $\vec{L}$ is constant, then any component of it must also be constant. Let's examine its $z$-component, $L_z = \vec{L} \cdot \hat{z}$. The angular momentum is $\vec{L} = m(\vec{r} \times \vec{v})$. Using the spherical coordinate expressions for $\vec{r}$ and $\vec{v}$:
$$ \vec{L} = m (r\hat{r}) \times (\dot{r}\hat{r} + r\dot{\theta}\hat{\theta} + r\sin\theta\dot{\phi}\hat{\phi}) = m r^2 (\dot{\theta}\hat{\phi} - \dot{\phi}\sin\theta\hat{\theta}) $$
To find its $z$-component, $L_z = \vec{L} \cdot \hat{z}$, we project $\vec{L}$ onto the fixed vector $\hat{z}$. The component of $\vec{L}$ along $\hat{\phi}$ does not contribute since $\hat{\phi}$ is perpendicular to $\hat{z}$ (i.e., $\hat{\phi} \cdot \hat{z} = 0$). The $\hat{\theta}$ component projects with a factor of $\hat{\theta} \cdot \hat{z} = -\sin\theta$. This gives:
$$ L_z = (-m r^2\sin\theta\dot{\phi}\hat{\theta}) \cdot \hat{z} = -m r^2\sin\theta\dot{\phi}(-\sin\theta) = mr^2\sin^2\theta\dot{\phi} $$
Thus, the physical quantity $L_z = mr^2\sin^2\theta\dot{\phi}$ must be a constant of the motion. This implies that the quantity $H = r^2\dot{\phi}\sin^2\theta = L_z/m$ is also conserved. This demonstrates the profound link between the geometry of forces ([central force](@entry_id:160395), hence zero torque) and the resulting conserved quantities (angular momentum) that govern the dynamics. This is a preview of the powerful analytical methods that we will develop throughout this course.