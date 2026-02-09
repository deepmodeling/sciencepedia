## Applications and Interdisciplinary Connections

Having established the principles and mechanisms of well-balanced Discontinuous Galerkin (DG) schemes, we now turn our attention to their application in diverse scientific and engineering disciplines. The abstract property of exactly preserving a specific steady state is not merely a matter of numerical elegance; it is a critical feature for obtaining physically meaningful and quantitatively accurate simulations in systems where dynamics are characterized by small perturbations evolving around a dominant, non-trivial equilibrium. In many real-world scenarios, this underlying balance is far more complex than a trivial state of rest, involving a delicate interplay of forces, fluxes, and sources. This chapter will demonstrate how the well-balanced property, as formally defined by the vanishing of the semi-discrete residual for a projected steady state [@problem_id:3421736], is realized and exploited in a variety of contexts, from the planetary scale of geophysical flows to the microscopic interactions within porous media.

### Geophysical and Environmental Flows

Perhaps the most classical and extensively studied application of well-balanced schemes is in the domain of geophysical fluid dynamics. Here, gravitational and rotational forces establish large-scale equilibria that govern the behavior of oceans, atmospheres, and landscapes.

#### Shallow Water Equations with Topography

A fundamental benchmark for any numerical method intended for environmental flows is the shallow water equations with non-flat bottom topography. The simplest non-trivial equilibrium in this system is the "lake-at-rest" state, where a flat free-surface elevation is maintained over a variable bed elevation, implying zero velocity. In this state, the hydrostatic pressure gradient exactly balances the force exerted by the bed slope.

A standard DG scheme employing conventional upwind Riemann solvers often fails this seemingly simple test. The discretization of the flux divergence and the source term are typically inconsistent, creating a residual force at element interfaces that generates spurious, unphysical oscillations. To obtain a well-balanced scheme, the discretization must be designed to precisely mimic the continuous balance. Two prevalent strategies have emerged to achieve this. One approach is **hydrostatic reconstruction**, where the states at each cell interface are first adjusted to a local hydrostatic equilibrium before being fed into the Riemann solver. This effectively embeds the hydrostatic balance into the numerical flux itself. An alternative and equally powerful method is to employ a **source term splitting** or **flux correction** technique. Here, a standard numerical flux may be used, but the discrete source term is modified to include interface contributions that are designed to exactly cancel the spurious interface residuals produced by the flux divergence discretization [@problem_id:3428766] [@problem_id:3428802].

#### Rotating Flows and Geostrophic Balance

When considering large-scale oceanic or atmospheric flows, the Coriolis force becomes a dominant factor. In this context, a primary equilibrium is the **geostrophic balance**, where the pressure gradient force is balanced by the Coriolis force. For the linearized rotating shallow water equations, this balance manifests as a linear relationship between the gradient of the free-surface elevation and the velocity field.

Well-balanced DG methods are exceptionally well-suited to preserving this type of equilibrium. In a nodal DG framework using high-degree polynomials, the discrete gradient operators are represented by differentiation matrices. A key property of these matrices, particularly those constructed on Gauss-Lobatto-Legendre nodes, is their ability to exactly differentiate any polynomial up to the degree of the basis. Since the geostrophic balance involves linear or low-order polynomial fields, the discrete operators can reproduce the continuous balance equation to machine precision. Consequently, a DG scheme initialized with a geostrophic flow will maintain this state exactly, without generating spurious inertia-gravity waves. This makes such schemes ideal for studying the slow evolution of weather systems and ocean currents [@problem_id:3428780].

#### Morphodynamics: Coupled Flow and Sediment Transport

The principles of well-balancing extend naturally to coupled, multi-physics systems. In fluvial geomorphology, the evolution of a riverbed is governed by the Exner equation, which couples the bed elevation to the sediment transport flux, which is in turn driven by the fluid flow. A fundamental equilibrium in such a morphodynamic system occurs when the bed has a constant slope that perfectly balances the driving forces in the flow, resulting in zero net sediment transport and a stationary bed.

A well-balanced DG scheme for this system must preserve this coupled equilibrium. By discretizing the bed slope and the corresponding source term in the flow equation with the same discrete differentiation operator, the numerical scheme can be constructed to exactly satisfy the discrete analogue of the balance condition. For simple cases, such as a linear bed profile, a low-order ($p=1$) DG method is sufficient to achieve this balance to machine precision, preventing the simulation from producing artificial erosion or deposition and allowing for the accurate study of long-term landscape evolution [@problem_id:3428841].

### Astrophysics and Plasma Physics

The vast scales and extreme conditions of astrophysical phenomena necessitate numerical methods that can handle the balance between gravity, pressure, and magnetic forces. Well-balanced schemes are indispensable tools in this domain.

#### Isothermal Atmospheres and Stellar Structure

A classic problem in atmospheric science and stellar physics is the determination of the vertical structure of a fluid in hydrostatic equilibrium under gravity. For a compressible, isothermal ideal gas, the balance between the pressure gradient and the gravitational force results in a density profile that decays exponentially with height. This exponential function is non-polynomial, posing a significant challenge for DG methods, which are built upon polynomial basis functions. While the discrete projection of this exponential state cannot be preserved perfectly without error by standard DG operators, the design of well-balanced schemes for such problems is a critical area of research. These schemes aim to minimize spurious oscillations by ensuring that the discrete operators for the pressure gradient and the gravitational source are carefully matched [@problem_id:3428807].

#### Magnetohydrodynamics (MHD)

In plasma physics and astrophysics, the Lorentz force introduces another key player in force-balance equilibria. Magnetostatic equilibrium, where a balance is struck between pressure gradients, gravity, and magnetic forces, is fundamental to the structure of stars, accretion disks, and galaxies.

A particularly powerful technique for designing well-balanced schemes in this context is **flux reformulation**. By introducing a carefully chosen auxiliary potential, the gravitational and/or magnetic source terms in the momentum equation can be mathematically absorbed into the flux divergence. This transforms the original balance law into a new, equivalent homogeneous conservation law, but only for the specific class of equilibrium states. For such a state, the modified flux becomes spatially constant. A DG scheme applied to this reformulated system is then well-balanced by construction, as any consistent, conservative discretization will exactly preserve a state with a constant flux. This elegant approach makes it possible to preserve complex magnetostatic equilibria without intricate modifications to the source term discretization itself [@problem_id:3428847].

#### Systems with Self-Gravity: The Euler-Poisson Equations

For systems where the gravitational field is generated by the fluid itself, such as in star formation or galactic dynamics, the governing equations are the Euler-Poisson system. For these systems, well-balancing is not only crucial for capturing the hydrostatic state but is also a prerequisite for conserving other fundamental physical invariants. A well-designed DG scheme that is well-balanced for the hydrostatic equilibrium (where the pressure gradient balances the self-gravity) can be shown to also exactly conserve the total energy of the system—the sum of kinetic, internal, and gravitational potential energies—at the semi-discrete level. This demonstrates a deep connection between the well-balanced property and the preservation of other critical physical structures in the numerical solution [@problem_id:3428816].

### Further Interdisciplinary Connections

The applicability of well-balanced DG schemes extends far beyond the realms of geophysics and astrophysics, finding utility in various engineering and physical science problems.

#### Gas Dynamics in Varying Geometries

In aerodynamics and mechanical engineering, the flow of gas through ducts of varying cross-sectional area (nozzles) is described by the quasi-one-dimensional Euler equations. These equations can be written in a balance-law form where the source term is proportional to the derivative of the area function. Steady-state solutions, such as flows with constant Mach number, exist where the flux gradient is balanced by this geometric source term. A well-balanced scheme can be constructed by ensuring that the discrete operators for the flux divergence and the source term are designed compatibly, for instance, by satisfying a discrete analogue of the product rule. This principle of **mimicking discretization** ensures that the algebraic cancellations that occur in the continuous equations are mirrored at the discrete level, allowing for the exact preservation of steady nozzle flows [@problem_id:3428774].

#### Subsurface Flow in Porous Media

In hydrogeology and petroleum engineering, the flow of multiple fluid phases (e.g., water and oil) through a porous medium is governed by Darcy's law. Under the influence of gravity, a hydrostatic equilibrium can be established where the fluid motion ceases. This equilibrium is characterized by a balance between the capillary pressure gradient, which arises from interfacial tension between the fluids, and the gravitational potential gradients, which depend on the density difference between the phases. A well-balanced DG scheme for this application is built by expressing all forces as gradients of potentials and applying the same discrete differentiation operator to each. This guarantees that for a true hydrostatic state, where the total potentials are constant, the discrete gradients vanish identically, and the equilibrium is preserved to machine precision [@problem_id:3428808].

#### Radiative Transfer

Well-balancing is also critical for problems with stiff, non-gradient-based source terms. In radiation transport, described by moment models like the $P_N$ equations, the exchange of energy between the radiation field and the material is modeled by a source term of the form $S = \sigma_a (B(T) - E)$, where $E$ is the radiation energy and $B(T)$ is the equilibrium Planck function. In radiative equilibrium, $E = B(T)$ and the source term vanishes. A well-balanced scheme must preserve this state. This is achieved not through balancing a flux gradient, but by designing a special **source term quadrature** that exactly integrates the discrete source term to zero when the projected radiation energy equals the equilibrium value. This often requires the quadrature rule to be exact for polynomials of a higher degree than the basis functions, a condition that connects well-balancing to the theory of numerical integration [@problem_id:3428809].

### Advanced Topics in Well-Balanced Discretizations

The design of well-balanced schemes intersects with other advanced topics in numerical analysis, leading to more robust and powerful methods.

#### Interaction with Entropy Stability

Entropy stability is a separate structure-preserving property that guarantees a numerical scheme satisfies a discrete version of the Second Law of Thermodynamics. While distinct from the well-balanced property, the two are not mutually exclusive. Designing schemes that are both well-balanced and entropy-stable is a highly active area of research. This typically requires ensuring that the discretization of the source term not only balances the flux gradient but also possesses certain symmetry properties that prevent the production of spurious numerical entropy. For the shallow water equations, this dual property can be achieved by a specific symmetric discretization of the source term at cell interfaces [@problem_id:3428754].

#### Asymptotic-Preserving and Well-Balanced Schemes

In many physical regimes, such as low-Mach number flows, the governing equations contain a small parameter that leads to a stiff, multiscale character. Asymptotic-preserving (AP) schemes are designed to remain accurate and efficient uniformly as this parameter tends to zero. It is often desirable for a scheme to be both well-balanced for a hydrostatic state and AP for the low-Mach limit. This can be achieved through careful splitting of the flux and source terms and the use of preconditioning, yielding a numerical method that is robust across different physical regimes [@problem_id:3428782].

#### Temporal Discretization for Well-Balanced Schemes

Finally, a well-balanced spatial discretization is only effective if its properties are not destroyed by the time integration scheme. Standard explicit Runge-Kutta methods will generally not preserve the equilibrium state exactly. To maintain the well-balanced property at the fully-discrete level, specially designed time integrators are required. For systems with stiff source terms, Implicit-Explicit (IMEX) Runge-Kutta methods are often used. By imposing additional constraints on the coefficients of the Butcher tableau, one can design an IMEX scheme that guarantees that if the solution is at a discrete equilibrium at the beginning of a time step, it remains at that equilibrium at the end of the step, for any time step size [@problem_id:3428811]. This ensures that the delicate balance achieved by the spatial discretization is preserved throughout the temporal evolution.