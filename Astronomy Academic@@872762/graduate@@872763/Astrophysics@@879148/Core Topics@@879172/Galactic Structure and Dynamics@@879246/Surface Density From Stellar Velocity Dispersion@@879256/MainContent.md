## Introduction
Determining the mass of cosmic structures is a central goal in astrophysics, yet much of this mass, in the form of dark matter, remains invisible. Galactic disks, the sprawling stellar cities we inhabit, are no exception. How, then, can we "weigh" a disk and uncover its total composition? The answer lies in the subtle motions of its stars. The vertical dance of stars, oscillating above and below the galactic plane, is not random; it is a precise response to the total gravitational pull of the disk. By carefully measuring these motions, we can infer the total mass responsible for them.

This article provides a comprehensive overview of the theory and application of using [stellar velocity dispersion](@entry_id:161232) to measure the surface mass density of galactic disks. It addresses the fundamental problem of how to measure mass that cannot be seen directly, bridging the gap between observable [stellar kinematics](@entry_id:157903) and the underlying [gravitational potential](@entry_id:160378). The content is designed to guide the reader from first principles to cutting-edge applications, revealing how this technique is used to probe everything from local dark matter to the grand evolutionary history of galaxies.

To achieve this, the article is organized into three interconnected parts. The first section, **Principles and Mechanisms**, lays the theoretical groundwork, introducing the concepts of hydrostatic equilibrium, the Jeans and Poisson equations, and deriving the key relationships for models like the isothermal disk. The second section, **Applications and Interdisciplinary Connections**, showcases the power of this method in action, from solving the classic Oort problem and searching for disk dark matter to understanding galaxy stability and testing fundamental physics. Finally, the **Hands-On Practices** section provides a series of guided problems that allow you to apply these concepts, tackling real-world challenges like [measurement uncertainty](@entry_id:140024) and sample contamination.

## Principles and Mechanisms

The vertical structure of a galactic disk represents a fundamental [equilibrium state](@entry_id:270364). Stars, gas, and dark matter, bound by their collective gravity, are arranged in a flattened configuration. The extent and shape of this vertical structure are not arbitrary; they are dictated by a precise balance between the gravitational forces pulling matter toward the galactic midplane and the effective pressure arising from the random motions of the disk's constituents. Understanding this balance allows us to "weigh" the disk—that is, to determine its total surface mass density, $\Sigma$—by observing the kinematics of its stellar populations. This chapter elucidates the core principles and mechanisms that underpin this powerful diagnostic tool.

### The Foundation: Vertical Hydrostatic Equilibrium

We begin by considering an idealized model of a galactic disk as an infinite, plane-parallel slab. In this model, all physical quantities vary only with height $z$ perpendicular to the midplane ($z=0$). The dynamics of this system are governed by two fundamental equations.

First, the **equation of [hydrostatic equilibrium](@entry_id:146746)**, which is a specific form of the collisionless Jeans equations, describes the balance of forces on a fluid element or a population of stars. It states that the upward gradient of pressure must exactly counteract the downward pull of gravity:
$$
\frac{dP_z(z)}{dz} = -\rho(z) \frac{d\Phi(z)}{dz} = \rho(z) g_z(z)
$$
Here, $\rho(z)$ is the volume mass density at height $z$, $P_z(z)$ is the vertical pressure, $\Phi(z)$ is the [gravitational potential](@entry_id:160378), and $g_z(z) = -d\Phi/dz$ is the local gravitational acceleration in the $z$-direction. For a stellar system, the pressure is not thermal in the classical sense but kinetic, representing the [momentum flux](@entry_id:199796) due to the random motions of stars. If the stars have a vertical velocity dispersion $\sigma_z(z)$, the pressure is given by $P_z(z) = \rho(z) \sigma_z^2(z)$.

Second, the **Poisson equation** relates the [gravitational potential](@entry_id:160378) to the mass density that creates it. For a plane-parallel system, this simplifies to:
$$
\frac{d^2\Phi(z)}{dz^2} = 4\pi G \rho(z)
$$
where $G$ is the [gravitational constant](@entry_id:262704). This equation states that the curvature of the potential is proportional to the local density of matter.

These two equations form a closed system that, given an "equation of state" relating pressure and density, fully determines the vertical structure of a self-gravitating disk. The total mass per unit area, or **surface mass density** $\Sigma$, is the integral of the volume density over all heights:
$$
\Sigma = \int_{-\infty}^{\infty} \rho(z) dz
$$
Our central goal is to establish the relationship between the observable kinematics (like $\sigma_z$) and this crucial quantity, $\Sigma$.

### A General Result: The Vertical Virial Theorem

Before examining specific models, it is instructive to derive a remarkably general relationship that connects the [surface density](@entry_id:161889) to the pressure at the midplane. This result, a form of the vertical [virial theorem](@entry_id:146441), holds for any self-gravitating disk in equilibrium, regardless of its specific composition or the details of its [stellar dynamics](@entry_id:158068).

By integrating the equation of hydrostatic equilibrium from the midplane ($z=0$) to infinity (where density and pressure are assumed to vanish), we can relate the midplane pressure $P_{z,0} = P_z(0)$ to an integral involving the gravitational field. A more direct route involves multiplying the hydrostatic equation by $d\Phi/dz$ and the Poisson equation by $dP/dz$ and combining them. However, a powerful result can be obtained by integrating the Poisson equation once to find the gravitational field $g_z(z) = -d\Phi/dz$. For a symmetric disk, $g_z(z) = -4\pi G \int_0^z \rho(z')dz'$. Now, if we integrate the hydrostatic equation from $z=0$ to $z \to \infty$:
$$
\int_0^\infty \frac{dP_z}{dz} dz = P_z(\infty) - P_{z,0} = -P_{z,0}
$$
The right-hand side becomes:
$$
\int_0^\infty \rho(z) g_z(z) dz = -\int_0^\infty \rho(z) \left( 4\pi G \int_0^z \rho(z')dz' \right) dz
$$
This can be recognized as the integral of $u \, du$ where $u = \int_0^z \rho(z')dz'$. The result is $-(4\pi G) \frac{1}{2} \left[ \left(\int_0^\infty \rho(z')dz'\right)^2 \right] = -2\pi G (\Sigma/2)^2 = -\frac{\pi G \Sigma^2}{2}$. Equating the two sides gives the celebrated result [@problem_id:275406]:
$$
P_{z,0} = \frac{\pi G}{2} \Sigma^2
$$
This equation is profound. It asserts that the total [surface density](@entry_id:161889) of a self-gravitating disk is determined entirely by the total pressure at its midplane. This pressure could be provided by stars, gas, cosmic rays, or any combination thereof. If one can determine $P_{z,0}$, one can determine $\Sigma$. This principle is exceptionally useful when analyzing complex, multi-component systems, as seen in the case of a disk supported by both stars and cosmic rays [@problem_id:275319]. In such a scenario, the total pressure $P(0) = P_s(0) + P_{cr}(0)$ is what balances gravity, allowing one to calculate the relative importance of each component if their [equations of state](@entry_id:194191) are known.

### The Isothermal Disk: A Canonical Model

The simplest and most widely used model for a stellar disk is the **isothermal disk**, where the vertical velocity dispersion $\sigma_z$ is assumed to be constant with height. The pressure is then directly proportional to the density: $P_z(z) = \rho(z)\sigma_z^2$. Substituting this into the hydrostatic and Poisson equations yields a [second-order differential equation](@entry_id:176728) for the density:
$$
\sigma_z^2 \frac{d^2(\ln \rho)}{dz^2} = -4\pi G \rho
$$
The unique, physically realistic solution to this equation that is peaked at $z=0$ is:
$$
\rho(z) = \rho_0 \text{sech}^2\left(\frac{z}{z_0}\right)
$$
where $\rho_0$ is the midplane density. The characteristic **vertical [scale height](@entry_id:263754)** $z_0$ is not a free parameter but is determined by the physics:
$$
z_0 = \frac{\sigma_z}{\sqrt{2\pi G \rho_0}}
$$
The [surface density](@entry_id:161889) of this disk is $\Sigma = 2\rho_0 z_0$. Combining these relations reveals a direct link between the observables $\sigma_z$, the [scale height](@entry_id:263754) $z_0$, and the [surface density](@entry_id:161889) $\Sigma$:
$$
\Sigma = \frac{\sigma_z^2}{\pi G z_0}
$$
This provides a direct method to measure [surface density](@entry_id:161889): if one can measure the vertical velocity dispersion and the [scale height](@entry_id:263754) of a stellar population that dominates the disk mass, one can calculate its [surface density](@entry_id:161889).

The internal consistency of this model can be further explored by connecting it to other dynamical quantities. For instance, the gravitational potential near the midplane can be approximated as a [harmonic oscillator potential](@entry_id:750179), $\Phi(z) \approx \frac{1}{2}\omega_z^2 z^2 + \Phi(0)$, where $\omega_z$ is the fundamental frequency of small vertical oscillations. From the Poisson equation at $z=0$, we have $\omega_z^2 = \left. d^2\Phi/dz^2 \right|_{z=0} = 4\pi G \rho_0$. By combining this with the relations for the isothermal disk, one can derive a beautiful expression linking the global [surface density](@entry_id:161889) to the local velocity dispersion and the local potential curvature [@problem_id:275301]:
$$
\Sigma = \frac{\sigma_z \omega_z}{\sqrt{2} \pi G}
$$
This illustrates how different kinematic probes can be used in concert to constrain the disk's mass structure. Moreover, the vertical structure of the disk is not independent of its dynamics in the plane. The Toomre stability parameter, $Q$, which governs stability against axisymmetric [gravitational collapse](@entry_id:161275), depends on $\Sigma$. In a scenario where a disk is assumed to be marginally stable ($Q=1$), its [surface density](@entry_id:161889) is fixed by its kinematics. This allows one to relate the midplane volume density $\rho_0$ directly to global galactic parameters like the [circular velocity](@entry_id:161552) $V_c$ and radius $R$, providing a powerful link between local structure and galaxy-wide properties [@problem_id:275469].

### Beyond the Isothermal Model

While the isothermal disk is a cornerstone model, real stellar populations can exhibit more complex behavior. A useful generalization is the **[polytropic model](@entry_id:157519)**, which assumes an equation of state of the form $P_z = K \rho^\gamma$, where $K$ is a constant and $\gamma$ is the [polytropic index](@entry_id:137268). The isothermal case corresponds to $\gamma=1$.

As a concrete example, consider a polytropic disk with $\gamma=2$. Combining the hydrostatic and Poisson equations leads to a [simple harmonic oscillator equation](@entry_id:196017) for the [density profile](@entry_id:194142): $d^2\rho/dz^2 + (2\pi G/K)\rho = 0$. The solution is a cosine function, $\rho(z) = \rho_0 \cos(z/H)$, which implies the disk has a finite edge where the density drops to zero. The [surface density](@entry_id:161889) for this model can be calculated directly from the solution parameters [@problem_id:275410]. This demonstrates that the shape of the vertical [density profile](@entry_id:194142) is a direct consequence of the assumed stellar-dynamical "equation of state".

More advanced models can even accommodate a **height-dependent velocity dispersion**, $\sigma_z(z)$. For example, in a system where both the [density profile](@entry_id:194142) and the velocity dispersion profile are parameterized functions of height, the Jeans equation imposes a strict consistency condition between them and the underlying gravitational potential. Solving this equation allows for the determination of the system's properties, such as its total mass, even in these more complex scenarios [@problem_id:275379].

### The Power of Tracers: Weighing the Unseen

A significant challenge in astronomy is that the component we can easily observe (e.g., bright stars) may not be the component that dominates the mass. The true power of vertical dynamics lies in its ability to measure the *total* [surface density](@entry_id:161889), including stars, gas, and dark matter. This is achieved by using a **tracer population**. A tracer is a subset of stars (or gas) that is dynamically "massless," meaning its own [self-gravity](@entry_id:271015) is negligible compared to the background potential of the disk. These tracers act as test particles, and their distribution and kinematics reveal the potential they inhabit.

The governing equation for a tracer population with density $\rho_t(z)$ and velocity dispersion $\sigma_{z,t}$ is the hydrostatic equilibrium equation, but the potential $\Phi(z)$ is generated by the total mass density $\rho_{tot}(z)$:
$$
\sigma_{z,t}^2 \frac{d\rho_t}{dz} = -\rho_t(z) \frac{d\Phi_{tot}}{dz}
$$
This equation is a gateway to measuring $\Sigma_{tot}$. If one can observe the vertical [density profile](@entry_id:194142) $\rho_t(z)$ and measure the velocity dispersion $\sigma_{z,t}$ for a tracer population, one can solve for the gravitational field $g_z(z) = -d\Phi_{tot}/dz$. Then, using the Poisson equation in reverse ($4\pi G \rho_{tot} = -dg_z/dz$), one can determine the total mass [density profile](@entry_id:194142) $\rho_{tot}(z)$. Integrating this profile gives the total [surface density](@entry_id:161889) $\Sigma_{tot}$. This technique is robust and has been applied to tracer populations with various functional forms for their density profiles [@problem_id:275539].

A particularly elegant application of the tracer method involves looking at the stars at large heights from the midplane. Far from the disk, the gravitational acceleration $g_z$ asymptotically approaches a constant value determined by the total surface mass density of the sheet: $|g_z| \to 2\pi G \Sigma_{tot}$. For an isothermal tracer population, the hydrostatic equilibrium equation in this regime becomes $d(\ln \rho_t)/dz \approx -2\pi G \Sigma_{tot}/\sigma_{z,t}^2$. The solution is a simple exponential decay: $\rho_t(z) \propto \exp(-|z|/H_T)$, where the asymptotic [scale height](@entry_id:263754) $H_T$ is given by $H_T = \sigma_{z,t}^2 / (2\pi G \Sigma_{tot})$. By measuring the velocity dispersion of the tracer and its exponential [scale height](@entry_id:263754) far from the plane, one can directly solve for the total [surface density](@entry_id:161889) of the disk [@problem_id:275563]:
$$
\Sigma_{tot} = \frac{\sigma_{z,t}^2}{2\pi G H_T}
$$
This method, pioneered by Jan Oort and John Bahcall, is a classic tool for measuring the local density of matter in the Milky Way, including the search for dark matter in the disk.

### Accounting for External Potentials

A final, crucial consideration is that galactic disks are not isolated. They are embedded within vast, roughly spherical halos of dark matter. The halo generates its own gravitational field, which contributes to the vertical force pulling stars back to the midplane.

The Poisson equation must be modified to include this external contribution. At the midplane, the total vertical curvature of the potential is the sum of the disk's [self-gravity](@entry_id:271015) and the halo's contribution:
$$
\left. \frac{d^2\Phi_{tot}}{dz^2} \right|_{z=0} = 4\pi G \rho_{disk}(0) + \left. \frac{d^2\Phi_{halo}}{dz^2} \right|_{z=0}
$$
The halo term acts as an additional restoring force. For a spherical halo potential, the vertical curvature at a cylindrical radius $r_0$ in the disk can be related to the [circular velocity](@entry_id:161552) generated by the halo, $v_h$. Failure to account for this term will lead to an incorrect interpretation of observations. Specifically, if one attributes the entire restoring force to the disk's mass alone, one will systematically overestimate the disk's [surface density](@entry_id:161889). A proper analysis requires disentangling these two contributions, using a combination of kinematic data and non-parametric measures of the density profile's shape to solve for the disk [surface density](@entry_id:161889) $\Sigma$ while accounting for the halo's influence [@problem_id:275296]. This final step highlights the interconnectedness of galactic components and the sophistication required to build a complete dynamical picture of a galaxy from stellar motions.