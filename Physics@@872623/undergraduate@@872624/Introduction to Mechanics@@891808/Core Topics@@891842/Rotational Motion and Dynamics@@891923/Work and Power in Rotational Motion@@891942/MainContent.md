## Introduction
In the study of mechanics, the concepts of work and power are fundamental to understanding how energy is transferred and transformed within a system. While these ideas are familiar from the analysis of linear motion, their application to rotating objects opens up a new dimension of dynamics. How does a torque perform work? How is the energy of a spinning flywheel related to the forces that set it in motion? This article addresses these questions by extending the principles of work and energy into the domain of rotation. It bridges the conceptual gap between linear and [rotational dynamics](@entry_id:267911), providing a robust framework for analyzing everything from industrial machinery to the [molecular motors](@entry_id:151295) that power life.

The following chapters are structured to build a complete understanding of this topic. The first chapter, **"Principles and Mechanisms,"** lays the theoretical groundwork by deriving the expressions for work done by a torque, establishing the rotational [work-energy theorem](@entry_id:168821), and defining [rotational power](@entry_id:167740). It also explores advanced cases such as the work done by gravity and the fascinating dynamics of systems with a variable moment of inertia. The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates the practical utility of these principles by applying them to real-world problems in [mechanical engineering](@entry_id:165985), electromagnetism, and [biophysics](@entry_id:154938). Finally, the **"Hands-On Practices"** section provides a series of targeted problems designed to solidify your grasp of the core concepts and their application.

## Principles and Mechanisms

Having established the fundamentals of [rotational kinematics](@entry_id:176103) and dynamics, we now extend our analysis to the concepts of **work** and **power** in the context of [rotational motion](@entry_id:172639). Just as forces can do work and transfer energy in [translational motion](@entry_id:187700), torques can do work and alter the rotational kinetic energy of an object. This chapter will develop the principles governing these energy transformations and explore their application in a variety of physical systems.

### Work Done by a Torque

In linear mechanics, the work done by a constant force $F$ over a displacement $\Delta s$ is $W = F \Delta s$. If the force varies, we must integrate: $W = \int F \cdot ds$. We can establish a direct analogue for rotation.

Consider a rigid body rotating about a fixed axis. A force $\vec{F}$ is applied to a point on the body at a [position vector](@entry_id:168381) $\vec{r}$ from the axis. For an infinitesimal rotation $d\theta$, the point moves through an infinitesimal arc length $ds = r d\theta$. The work done by the force during this small displacement is $dW = F_t ds$, where $F_t$ is the component of the force tangential to the circular path. Recalling that the magnitude of the torque is $\tau = r F_t$, we can substitute $F_t = \tau / r$.

This gives us the differential work done:
$dW = \left(\frac{\tau}{r}\right) (r d\theta) = \tau d\theta$

This remarkably simple expression, $dW = \tau d\theta$, is the rotational equivalent of $dW = F_x dx$. It states that the infinitesimal work done by a torque $\tau$ is the product of the torque and the infinitesimal [angular displacement](@entry_id:171094) $d\theta$.

To find the total work done over a finite [angular displacement](@entry_id:171094) from an initial angle $\theta_i$ to a final angle $\theta_f$, we integrate this expression:

$$W = \int_{\theta_i}^{\theta_f} \tau d\theta$$

In the special but common case where the torque $\tau$ is constant, the integral simplifies to:

$$W = \tau \int_{\theta_i}^{\theta_f} d\theta = \tau (\theta_f - \theta_i) = \tau \Delta\theta$$

Here, $\Delta\theta$ must be measured in [radians](@entry_id:171693). This formula provides a straightforward method for calculating work in many practical scenarios, such as a motor applying a steady torque to a [flywheel](@entry_id:195849).

### The Work-Energy Theorem for Rotation

The most profound consequence of the definition of work is its connection to kinetic energy. For [rotational motion](@entry_id:172639), the **[work-energy theorem](@entry_id:168821)** states that the [net work](@entry_id:195817) done on a rigid body by all external torques is equal to the change in its [rotational kinetic energy](@entry_id:177668).

We begin with Newton's second law for rotation, $\tau_{net} = I \alpha$, where $\tau_{net}$ is the [net torque](@entry_id:166772), $I$ is the moment of inertia, and $\alpha$ is the [angular acceleration](@entry_id:177192). To connect this to energy, we employ the [chain rule](@entry_id:147422) to express $\alpha$ in terms of [angular displacement](@entry_id:171094) $\theta$:

$$\alpha = \frac{d\omega}{dt} = \frac{d\omega}{d\theta} \frac{d\theta}{dt} = \omega \frac{d\omega}{d\theta}$$

Substituting this into the equation of motion gives:

$$\tau_{net} = I \omega \frac{d\omega}{d\theta}$$

Rearranging, we find $\tau_{net} d\theta = I \omega d\omega$. This equation links the work done by the net torque over an infinitesimal angle $d\theta$ to the resulting change in [angular velocity](@entry_id:192539). Integrating both sides from an initial state ($\theta_i, \omega_i$) to a final state ($\theta_f, \omega_f$) yields the theorem:

$$W_{net} = \int_{\theta_i}^{\theta_f} \tau_{net} d\theta = \int_{\omega_i}^{\omega_f} I \omega d\omega$$

$$W_{net} = \frac{1}{2} I \omega_f^2 - \frac{1}{2} I \omega_i^2 = \Delta K_{rot}$$

This powerful theorem allows us to determine the change in a body's rotational state without analyzing the [time evolution](@entry_id:153943) of the motion.

For example, consider a CubeSat in deep space that uses an internal [reaction wheel](@entry_id:178763) for attitude control [@problem_id:2230610]. If an [electric motor](@entry_id:268448) applies a constant torque $\tau$ to the wheel (with moment of inertia $I$) for a time $\Delta t$, starting from rest, we can find the work done. The [work-energy theorem](@entry_id:168821) provides the most direct path. First, the final angular velocity is $\omega_f = \alpha \Delta t = (\tau/I)\Delta t$. Since the wheel starts from rest ($\omega_i = 0$), the work done by the motor (which is the [net work](@entry_id:195817)) is:

$$W = \Delta K_{rot} = \frac{1}{2} I \omega_f^2 = \frac{1}{2} I \left(\frac{\tau \Delta t}{I}\right)^2 = \frac{\tau^2 (\Delta t)^2}{2I}$$

The [work-energy theorem](@entry_id:168821) is particularly useful when torques are not constant. Suppose a flywheel is spun up by a constant motor torque $\tau_m$ but is simultaneously subjected to a braking torque that increases with the angle of rotation, $\tau_b = k\theta^2$ [@problem_id:2230640]. The net torque is $\tau_{net}(\theta) = \tau_m - k\theta^2$. To find the final angular velocity $\omega_f$ after rotating through an angle $\theta_f$, we apply the [work-energy theorem](@entry_id:168821) in its integral form:

$$\Delta K_{rot} = \frac{1}{2}I\omega_f^2 - 0 = \int_0^{\theta_f} (\tau_m - k\theta^2) d\theta$$

$$\frac{1}{2}I\omega_f^2 = \left[ \tau_m \theta - \frac{1}{3}k\theta^3 \right]_0^{\theta_f} = \tau_m \theta_f - \frac{1}{3}k\theta_f^3$$

This approach elegantly handles the variable torque without needing to solve a complex differential equation for $\omega(t)$.

It is crucial to distinguish between the **[net work](@entry_id:195817)** done by the [net torque](@entry_id:166772) and the work done by an individual torque. For instance, in a laboratory ultracentrifuge accelerating from rest, a motor applies a driving torque $\tau_m$ while friction provides a resistive torque $\tau_r$ [@problem_id:2230646]. The [net work](@entry_id:195817), $W_{net} = (\tau_m - \tau_r)\Delta\theta$, determines the final kinetic energy. However, the total work done *by the motor* is $W_m = \tau_m \Delta\theta$. This value represents the total energy supplied by the motor, part of which increases the rotor's kinetic energy and part of which is dissipated as heat by friction.

### Work Done by Gravity on a Rotating Body

For [conservative forces](@entry_id:170586) like gravity, work can be calculated as the negative change in potential energy. For a rigid body of mass $M$, the [gravitational potential energy](@entry_id:269038) is determined solely by the vertical position of its **center of mass** ($y_{cm}$), such that $U_g = M g y_{cm}$. Therefore, the work done by gravity as the body rotates is:

$$W_g = - \Delta U_g = - (M g y_{cm,f} - M g y_{cm,i}) = M g (y_{cm,i} - y_{cm,f})$$

This principle simplifies problems involving objects rotating in a gravitational field. Imagine a rod of length $L$ and mass $M$ pivoted at one end, released from a horizontal position and swinging down to a vertical one [@problem_id:2230607]. To find the work done by gravity, we need only find the change in the vertical position of its center of mass. If the rod were uniform, its center of mass would be at $x_{cm} = L/2$. In the horizontal position, $y_{cm,i} = 0$ (taking the pivot as the origin), and in the vertical position, $y_{cm,f} = -L/2$. The work would be $W_g = M g (0 - (-L/2)) = \frac{1}{2}MgL$.

If the rod's mass distribution is not uniform, for example, if its [linear mass density](@entry_id:276685) is $\lambda(x) = \beta x$, we must first calculate the position of the center of mass via integration:

$$x_{cm} = \frac{1}{M}\int_0^L x \, dm = \frac{1}{M}\int_0^L x \lambda(x) dx = \frac{1}{M}\int_0^L \beta x^2 dx = \frac{\beta L^3}{3M}$$

By first finding the total mass $M = \int_0^L \beta x dx = \beta L^2/2$, we can express $\beta = 2M/L^2$. Substituting this gives $x_{cm} = (2M/L^2) L^3 / (3M) = 2L/3$. Thus, for this non-uniform rod, the center of mass drops by a distance of $2L/3$, and the work done by gravity is $W_g = M g (2L/3) = \frac{2}{3}MgL$.

### Power in Rotational Motion

**Power** is the rate at which work is done, $P = dW/dt$. Using our expression for differential work, $dW = \tau d\theta$, we find the [instantaneous power](@entry_id:174754) in [rotational motion](@entry_id:172639):

$$P = \frac{dW}{dt} = \frac{\tau d\theta}{dt} = \tau \left(\frac{d\theta}{dt}\right)$$

Since $\omega = d\theta/dt$ is the [instantaneous angular velocity](@entry_id:171936), we arrive at the [rotational power](@entry_id:167740) equation:

$$P = \tau \omega$$

This equation is the rotational counterpart to the linear power equation $P = F v$. It states that the power delivered by a torque is the product of that torque and the [instantaneous angular velocity](@entry_id:171936).

This relationship has many practical applications. For an uninterruptible power supply that uses a flywheel rotating at a constant high speed, a motor must continuously deliver power to counteract the resistive torque $\tau_{rr}$ from bearings and [air drag](@entry_id:170441) [@problem_id:2230680]. To maintain a constant [angular velocity](@entry_id:192539) $\omega$, the motor must apply a torque $\tau_m = \tau_{rr}$. The power the motor must supply is therefore $P = \tau_m \omega = \tau_{rr} \omega$.

The power equation can also be used to find the [instantaneous power](@entry_id:174754) being delivered during an acceleration. For a [flywheel](@entry_id:195849) being spun up by a motor against friction, the power delivered by the motor at any instant is $P_m = \tau_m \omega$, where $\omega$ is the [angular velocity](@entry_id:192539) at that instant [@problem_id:2230653]. To find the power at a specific moment (e.g., after 10 revolutions), one must first calculate the [instantaneous angular velocity](@entry_id:171936) $\omega$ at that point using [rotational kinematics](@entry_id:176103).

Conversely, the relationship can be inverted to determine the torque required to achieve a certain power output. For an electromagnetic brake designed to dissipate energy at a constant rate $P$, the braking torque it must apply is inversely proportional to the [flywheel](@entry_id:195849)'s speed: $\tau = P/\omega$ [@problem_id:2230645]. This implies that to keep the [power dissipation](@entry_id:264815) constant as the [flywheel](@entry_id:195849) slows down, the braking system must exert a progressively larger torque.

### Systems with Variable Moment of Inertia

A fascinating and important class of problems involves systems where the moment of inertia $I$ is not constant. This occurs when parts of a rotating body move relative to the axis of rotation, changing the [mass distribution](@entry_id:158451). The classic example is an ice skater pulling their arms inward during a spin.

#### Isolated Systems and Conservation of Angular Momentum

Consider a system on which there is no net external torque ($\tau_{ext, net} = 0$). Such a system is **isolated**. According to Newton's second law for rotation in its most general form, $\tau_{ext, net} = d\vec{L}/dt$, this implies that the [total angular momentum](@entry_id:155748) $\vec{L}$ of the system must be conserved.

If the moment of inertia of the system changes from an initial value $I_i$ to a final value $I_f$, the angular velocity must change to keep the angular momentum $L = I\omega$ constant:

$$L_i = L_f \quad \implies \quad I_i \omega_i = I_f \omega_f$$

A crucial point is that while angular momentum is conserved, **rotational kinetic energy is generally not conserved** in these situations. The kinetic energy can be expressed in terms of angular momentum as $K_{rot} = \frac{1}{2}I\omega^2 = \frac{(I\omega)^2}{2I} = \frac{L^2}{2I}$. Since $L$ is constant, if $I$ changes, $K_{rot}$ must also change.

Where does this energy change come from? It comes from **internal work** done by forces within the system that alter its configuration.

Consider a laboratory apparatus with two masses that can be retracted toward a central rotating hub [@problem_id:2230627]. As a motor pulls the masses from an initial radius $r_i$ to a final radius $r_f$, the total moment of inertia decreases ($I_f  I_i$). By conservation of angular momentum, the final angular velocity $\omega_f = (I_i/I_f)\omega_i$ will be greater than $\omega_i$. The final kinetic energy, $K_f = L^2 / (2I_f)$, will be greater than the initial kinetic energy, $K_i = L^2 / (2I_i)$. The work done by the internal motor to pull the masses inward is precisely this change in kinetic energy:

$$W_{motor} = \Delta K_{rot} = K_f - K_i = \frac{L^2}{2} \left(\frac{1}{I_f} - \frac{1}{I_i}\right)$$

Since $I_f  I_i$, this work is positive, meaning the motor had to expend energy to pull the masses in against the "centrifugal" effects, and this expended energy increased the system's total kinetic energy. The same principle explains how a maintenance robot moving from the edge to the center of a rotating space station does work and increases the system's kinetic energy [@problem_id:2230626].

#### Non-Isolated Systems with Constant Angular Velocity

Now, let us consider a different scenario. What if we want to maintain a constant [angular velocity](@entry_id:192539) $\omega$ while the moment of inertia $I(t)$ is changing? This is a non-isolated system, as it requires the application of an external torque.

Since the total angular momentum is $L(t) = I(t)\omega$, its rate of change is:
$$\frac{dL}{dt} = \frac{d}{dt}(I(t)\omega) = \frac{dI}{dt}\omega$$
To maintain this change, an external torque equal to this rate of change must be applied:
$$\tau_{ext} = \frac{dI}{dt}\omega$$
This external torque does work. The power it supplies is $P_{ext} = \tau_{ext}\omega = (\frac{dI}{dt})\omega^2$. The total work done by this external agent to move the system from an initial configuration $I_i$ to a final configuration $I_f$ is:
$$W_{ext} = \int P_{ext} dt = \int (\frac{dI}{dt})\omega^2 dt = \omega^2 \int_{I_i}^{I_f} dI = \omega^2 (I_f - I_i) = \Delta K_{rot}$$
This makes sense: the work done by the external torque is exactly equal to the change in the system's kinetic energy, since $\omega$ is constant.

This case is illustrated by a maintenance drone moving radially on a rotating space station whose attitude control system is tasked with keeping the station's rotation rate $\omega$ constant [@problem_id:2230638]. As the drone of mass $m$ moves from the center ($r=0$) to the rim ($r=R$), the system's moment of inertia increases by $mR^2$. The work the station's motors must do to counteract this change and maintain constant $\omega$ is $W_{ext} = \omega^2 (I_f - I_i) = \omega^2 (mR^2) = m\omega^2 R^2$. In this case, the external torque is doing positive work to spin up the drone and maintain the station's speed, increasing the total energy of the system.