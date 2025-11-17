## Introduction
Modeling tsunami [wave propagation](@entry_id:144063) is a cornerstone of [computational geophysics](@entry_id:747618), critical for hazard assessment, early warning systems, and understanding one of nature's most formidable phenomena. To accurately predict a tsunami's journey from its deep-ocean genesis to its impact on a distant coast requires a robust synthesis of physics and sophisticated computational techniques. This article bridges the gap between fundamental fluid dynamics and practical, [predictive modeling](@entry_id:166398) by providing a comprehensive overview of the principles, applications, and hands-on challenges in the field.

The journey begins with **Principles and Mechanisms**, where we derive the governing [shallow-water equations](@entry_id:754726) from first principles and explore the numerical foundations of stable and accurate simulation. Next, **Applications and Interdisciplinary Connections** broadens the perspective, demonstrating how these models connect with seismology, [coastal engineering](@entry_id:189157), data assimilation, and even planetary science to solve complex, real-world problems. Finally, **Hands-On Practices** offers an opportunity to apply these theoretical concepts to concrete computational exercises, solidifying your understanding of the key challenges in the field. This structured approach will equip you with a comprehensive framework for modeling tsunami [wave propagation](@entry_id:144063), starting with the core principles that govern these powerful waves.

## Principles and Mechanisms

The modeling of tsunami wave propagation is grounded in the principles of [fluid mechanics](@entry_id:152498), applied under specific assumptions that capture the unique scale and nature of these powerful waves. This chapter details the derivation of the foundational governing equations, explores the hierarchy of models ranging from simple to complex, and examines the key physical and numerical mechanisms that must be addressed for accurate simulation.

### The Shallow-Water Approximation: From First Principles to a Governing Model

The most fundamental description of a fluid in motion is provided by the Navier-Stokes equations or, for an [inviscid fluid](@entry_id:198262), the Euler equations. These equations represent the conservation of mass and momentum for a continuous medium. For an incompressible fluid of constant density $\rho$ under gravity $g$, they are:
$$
\nabla \cdot \mathbf{u} = 0
$$
$$
\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} = -\frac{1}{\rho}\nabla p - g \hat{\mathbf{z}}
$$
where $\mathbf{u}=(u,v,w)$ is the velocity vector, $p$ is the pressure, and $\hat{\mathbf{z}}$ is the [unit vector](@entry_id:150575) in the vertical direction. While these equations are universal, their full solution is computationally prohibitive for basin-scale tsunami modeling. The key to a tractable model lies in a systematic simplification based on the [characteristic scales](@entry_id:144643) of a tsunami.

A tsunami is a quintessential **long wave**, meaning its horizontal wavelength $L$ is much greater than the water depth $h_0$. This physical characteristic motivates a scaling analysis to identify the dominant physical balances. We introduce two critical [dimensionless parameters](@entry_id:180651): the **nonlinearity parameter** $\varepsilon = a/h_0$, which compares the wave amplitude $a$ to the water depth, and the **shallowness parameter** $\mu = h_0/L$. For tsunamis in the open ocean, the defining condition is $\mu \ll 1$.

By non-dimensionalizing the Euler equations using [characteristic scales](@entry_id:144643) for horizontal length ($L$), vertical length ($h_0$), and time ($T = L/\sqrt{g h_0}$), we can analyze the vertical momentum equation in detail. The analysis reveals that the vertical acceleration of the fluid is of order $\mu^2$ relative to the acceleration due to gravity. For long waves where $\mu \ll 1$, this vertical acceleration becomes negligible. Consequently, the vertical momentum equation simplifies to a balance between the vertical pressure gradient and gravity:
$$
\frac{\partial p}{\partial z} \approx -\rho g
$$
This is the **hydrostatic pressure approximation**. It states that the pressure at any point depends only on the weight of the water column above it. Integrating this equation from a depth $z$ to the free surface at elevation $\eta$ gives the explicit [pressure distribution](@entry_id:275409): $p(x,y,z,t) \approx p_{\text{atm}} + \rho g (\eta - z)$.

A critical consequence of the hydrostatic approximation is that the horizontal pressure gradient, which drives the flow, becomes independent of depth. This, in turn, implies that the horizontal velocity is, to leading order, uniform with depth. This justifies describing the flow using depth-averaged quantities. By integrating the continuity and horizontal momentum equations over the water depth, we arrive at the **Shallow-Water Equations (SWE)**, the foundational model for [tsunami propagation](@entry_id:203810) [@problem_id:3618007]. These equations govern the evolution of the free-surface elevation $\eta(x,y,t)$ and the depth-averaged horizontal velocity vector $\mathbf{u}(x,y,t)$.

### A Hierarchy of Wave Propagation Models

While the SWE provide a powerful framework, different levels of simplification or extension can be employed depending on the specific physical regime being studied. This leads to a hierarchy of models with varying complexity and fidelity.

#### The Linear Nondispersive Model

In many situations, such as a tsunami propagating in the deep ocean far from its source, the wave amplitude $a$ is much smaller than the water depth $h_0$ (i.e., $\varepsilon = a/h_0 \ll 1$). In this case, we can further simplify the SWE by **[linearization](@entry_id:267670)**. This involves neglecting all terms that are quadratic or higher-order in the small perturbation quantities $\eta$ and $\mathbf{u}$.

For a [one-dimensional flow](@entry_id:269448) over a flat bottom of constant depth $H$, the nonlinear SWE can be linearized around the rest state ($\eta=0, u=0$). The [conservation of mass](@entry_id:268004) and momentum equations become:
$$
\frac{\partial \eta}{\partial t} + H \frac{\partial u}{\partial x} = 0
$$
$$
\frac{\partial u}{\partial t} + g \frac{\partial \eta}{\partial x} = 0
$$
These two first-order equations can be combined into a single second-order equation for the surface elevation $\eta$:
$$
\frac{\partial^2 \eta}{\partial t^2} - gH \frac{\partial^2 \eta}{\partial x^2} = 0
$$
This is the classic **[one-dimensional wave equation](@entry_id:164824)**. It describes waves that propagate without changing their shape, a property known as being **nondispersive**. All components of the wave travel at the same constant phase speed $c = \sqrt{gH}$. This simple model captures the most fundamental aspect of [tsunami propagation](@entry_id:203810) in the deep ocean: its high speed, which can reach hundreds of kilometers per hour for typical oceanic depths of $H \approx 4$ km [@problem_id:3618030].

#### The Physics of Dispersion

The nondispersive nature of the shallow-water model is an approximation. In reality, the speed of surface gravity waves depends on their wavelength. This phenomenon is called **dispersion**. To understand it, we must temporarily step back from the shallow-water approximation and consider the full linear theory of [water waves](@entry_id:186869) derived from [potential flow theory](@entry_id:267452) [@problem_id:3618023].

For small-amplitude waves of [angular frequency](@entry_id:274516) $\omega$ and wavenumber $k = 2\pi/\lambda$ (where $\lambda$ is the wavelength) over a constant depth $h$, the exact [linear dispersion relation](@entry_id:266313) is:
$$
\omega^2 = gk \tanh(kh)
$$
The phase speed $c_p = \omega/k$ is therefore $c_p = \sqrt{g \frac{\tanh(kh)}{k}}$. This speed is a function of the wavenumber $k$, indicating that waves of different lengths travel at different speeds.

The shallow-water model corresponds to the **long-wave limit**, where $kh \ll 1$. In this limit, we can use the Taylor approximation $\tanh(kh) \approx kh$. Substituting this into the exact [dispersion relation](@entry_id:138513) yields $\omega^2 \approx gk(kh) = ghk^2$, or $\omega \approx k\sqrt{gh}$. This gives a phase speed of $c_p \approx \sqrt{gh}$, which is independent of $k$ and matches the speed from the linear SWE. This confirms that the SWE are the nondispersive, long-wave limit of the full linear theory.

The first correction for dispersion comes from retaining the next term in the Taylor expansion of $\tanh(kh)$. This shows that the fractional deviation of the true phase speed from the shallow-water speed is approximately $(kh)^2/6$. For a typical tsunami with a wavelength of $\lambda=200$ km in a $4$ km deep ocean, the parameter $kh$ is very small (around $0.126$), and the error in using the shallow-water speed is less than $0.3\%$, justifying its use for transoceanic propagation [@problem_id:3618023].

Conversely, the **deep-water limit** occurs when $kh \gg 1$. Here, $\tanh(kh) \to 1$, and the dispersion relation becomes $\omega^2 \approx gk$. This regime is highly dispersive and is characteristic of short-wavelength wind waves, not open-ocean tsunamis [@problem_id:3618023].

#### Weakly Dispersive Models: Boussinesq and Serre-Green-Naghdi

While the SWE are excellent for basin-scale propagation, dispersive effects can become more important as wavelengths shorten during shoaling or for modeling the initial generation phase. To account for this, **weakly dispersive** models have been developed. These models systematically re-introduce the lowest-order dispersive effects into the shallow-water framework.

This is accomplished through a more careful [asymptotic expansion](@entry_id:149302) in the shallowness parameter $\mu = (h_0/L)^2$. Retaining terms of order $\mathcal{O}(\mu)$ in the governing equations corrects for the non-hydrostatic [pressure distribution](@entry_id:275409) and allows the model's [linear dispersion relation](@entry_id:266313) to better approximate the exact $\tanh(kh)$ behavior for small but finite $kh$ [@problem_id:3618021].

Two important classes of such models are:
*   **Boussinesq-type models**: These are derived assuming both weak dispersion ($\mu \ll 1$) and weak nonlinearity ($\varepsilon \ll 1$). They are suitable for waves of small but finite amplitude where both nonlinearity and dispersion are of comparable importance.
*   **Serre-Green-Naghdi (SGN) models**: These models also assume weak dispersion ($\mu \ll 1$) but allow for strong nonlinearity ($\varepsilon = \mathcal{O}(1)$). They are therefore "fully nonlinear, weakly dispersive" and are better suited for modeling steeper waves in the nearshore region, prior to breaking [@problem_id:3618021].

### Key Physical Processes in Tsunami Evolution

As a tsunami propagates from the deep ocean to the coast, its characteristics are profoundly altered by interactions with the changing bathymetry. The governing equations must account for these crucial physical processes.

#### Shoaling and Amplitude Change: Green's Law

One of the most dramatic effects is **shoaling**, the process by which a wave's amplitude changes as the water depth varies. For a slowly varying bathymetry, where reflections are negligible, the flux of wave energy is conserved. For linear shallow-water waves, the [wave energy](@entry_id:164626) density $E$ is proportional to the square of the amplitude, $E \propto A^2$, and the energy propagates at the group velocity, which for long waves is $C_g = \sqrt{gh}$.

The conservation of energy flux, $E \times C_g = \text{constant}$, therefore implies that $A^2 \sqrt{h} = \text{constant}$. This leads to the celebrated scaling relationship known as **Green's Law**:
$$
A(h) \propto h^{-1/4}
$$
This law predicts that as a tsunami enters shallower water (decreasing $h$), its amplitude $A$ must increase. This amplification, combined with a decrease in wavelength, leads to the dramatic and destructive increase in wave height as a tsunami approaches the coastline [@problem_id:3618070]. This relationship is a direct consequence of energy conservation in the long-wave limit and differs significantly from the more complex shoaling behavior of short, dispersive waves.

#### Energy Dissipation: Bottom Friction

As a tsunami propagates, particularly over the relatively shallow continental shelf, energy is lost due to friction with the seabed. This dissipation is a critical process that attenuates the wave and affects the extent of coastal inundation. In the depth-averaged [momentum equation](@entry_id:197225), this effect is introduced as a bottom stress term, $\boldsymbol{\tau}_b$.

The bottom stress is typically parameterized using an empirical **drag law**. The most common is the **quadratic drag law**, which assumes the stress is proportional to the square of the fluid velocity:
$$
\boldsymbol{\tau}_b = \rho C_d |\mathbf{u}| \mathbf{u}
$$
Here, $C_d$ is a dimensionless [drag coefficient](@entry_id:276893). This coefficient is not a universal constant; it encapsulates the roughness of the seabed. It is often related to the **Manning roughness coefficient** $n$, a parameter widely used in hydraulics. The relationship derived from [open-channel flow](@entry_id:267863) theory is:
$$
C_d = \frac{gn^2}{h^{1/3}}
$$
This formulation shows that the effective drag coefficient depends on the local water depth. When incorporated into the [momentum equation](@entry_id:197225) of the SWE, the bottom friction acts as a momentum sink, correctly formulated as $-\boldsymbol{\tau}_b / \rho$ in the [conservative form](@entry_id:747710) or as a frictional acceleration $-\boldsymbol{\tau}_b / (\rho h)$ in the velocity form [@problem_id:3618077]. Another common formulation uses the Chezy coefficient $C$, which is related to Manning's $n$ through $C = h^{1/6}/n$ [@problem_id:3618077].

### Foundations of Numerical Tsunami Modeling

Translating the continuous governing equations into a predictive computational model requires several key steps, from defining the initial disturbance to handling the boundaries of the simulation domain and ensuring [numerical stability](@entry_id:146550).

#### Source Generation: From Fault Rupture to Initial Wave

A [tsunami simulation](@entry_id:756209) begins with an initial condition that represents the sea surface displacement caused by an undersea earthquake. The standard approach is to use a static elastic dislocation model to compute the deformation of the seafloor caused by the fault rupture. The most widely used is the **Okada model**, which provides analytical, closed-form expressions for the three-dimensional surface displacement due to a rectangular fault in a homogeneous [elastic half-space](@entry_id:194631) [@problem_id:3618064].

The model takes as input the standard parameters of an earthquake fault: its geometry (length, width, depth, strike, dip), the slip amount (magnitude and rake angle), and the elastic properties of the Earth's crust. By applying the [principle of linear superposition](@entry_id:196987), the contributions from strike-slip and dip-slip components of the motion are combined to compute the final vertical displacement of the seafloor, $u_z(x,y)$. The fundamental assumption for tsunami initialization is that the earthquake rupture is nearly instantaneous compared to the timescale of [wave propagation](@entry_id:144063). This allows for the **instantaneous uplift approximation**, where the initial free-surface elevation of the tsunami, $\eta_0(x,y)$, is set equal to the static vertical displacement of the seafloor:
$$
\eta_0(x,y) = u_z(x,y,0)
$$
This provides the initial "hump" of water that begins to propagate outward as a tsunami.

#### The Balance-Law Formulation and Well-Balanced Schemes

For robust numerical solution, especially over variable bathymetry, the SWE are written in the form of a **balance law**:
$$
\frac{\partial \mathbf{U}}{\partial t} + \frac{\partial \mathbf{F}(\mathbf{U})}{\partial x} = \mathbf{S}(\mathbf{U}, x)
$$
Here, $\mathbf{U} = [h, q]^T$ is the vector of [conserved variables](@entry_id:747720) (water depth $h$ and discharge $q=hu$), $\mathbf{F}(\mathbf{U})$ is the [flux vector](@entry_id:273577), and $\mathbf{S}$ is a source term that accounts for the effect of the sloping bed. For the one-dimensional SWE, these are:
$$
\mathbf{F}(\mathbf{U}) = \begin{pmatrix} q \\ q^2/h + \frac{1}{2}gh^2 \end{pmatrix}, \quad \mathbf{S}(\mathbf{U}, x) = \begin{pmatrix} 0 \\ -gh \frac{\partial b}{\partial x} \end{pmatrix}
$$
where $b(x)$ is the bed elevation. A major challenge in solving this system numerically is correctly handling the balance between the pressure gradient term within the flux ($\partial_x(\frac{1}{2}gh^2)$) and the bathymetric source term ($-gh\partial_x b$).

In a simple "lake at rest" state where the water surface is flat ($\eta = \text{constant}$) and the velocity is zero ($u=0$), these two terms must exactly cancel. A naive numerical scheme that discretizes the flux gradient and the [source term](@entry_id:269111) independently will often fail to preserve this balance, leading to spurious, unphysical flows. To overcome this, **[well-balanced schemes](@entry_id:756694)** are required. Modern Finite Volume methods achieve this by incorporating the source term's effect directly into the computation of the [numerical flux](@entry_id:145174) at cell interfaces, often through a technique called **[hydrostatic reconstruction](@entry_id:750464)**. This ensures that the lake-at-rest state is maintained to machine precision, which is crucial for accurate simulation of small perturbations (like a tsunami) on top of a large-scale background state [@problem_id:3618040].

#### Defining the Computational Domain: Boundary Conditions

Numerical models operate on a finite computational domain, requiring the specification of **boundary conditions** that describe how the fluid interacts with the edges of the domain. Three main types are essential for tsunami modeling [@problem_id:3618050]:

1.  **Reflective Rigid Walls**: To model a coastline or an island, an impermeability condition is enforced. This means the component of velocity normal to the boundary must be zero: $u_n = \mathbf{u} \cdot \mathbf{n} = 0$. In the context of the linear SWE, this condition also implies that the normal gradient of the free surface is zero ($\partial_n \eta = 0$) at the wall, corresponding to a total reflection of wave height.

2.  **Radiation (Open) Boundaries**: For artificial boundaries in the open ocean, we want waves to pass out of the domain without reflecting back into it. A **radiation boundary condition** is designed to achieve this. It is derived from the characteristic analysis of the hyperbolic system. At an open boundary, the condition is formulated to constrain only the *incoming* characteristic information (e.g., setting it to zero) while allowing the *outgoing* characteristics to be determined by the solution from the interior. For the 1D linear SWE, this takes the form $\eta_t + c\eta_x = 0$ at a right boundary, an equation which only permits waves to travel to the right.

3.  **Absorbing (Sponge) Layers**: An alternative and robust method for open boundaries is to implement an **absorbing layer** or "sponge layer". In a buffer zone adjacent to the boundary, [artificial damping](@entry_id:272360) terms are added to the governing equations (e.g., $-\sigma \eta$ and $-\sigma \mathbf{u}$). The [damping coefficient](@entry_id:163719) $\sigma$ is gradually increased toward the boundary, causing outgoing waves to be smoothly attenuated and dissipated before they can reflect off the domain edge.

#### Ensuring Numerical Stability: The CFL Condition

Explicit [time-stepping schemes](@entry_id:755998), which are common in tsunami modeling, are subject to a stability constraint that limits the size of the time step, $\Delta t$. This is known as the **Courant-Friedrichs-Lewy (CFL) condition**. It ensures that information (i.e., a wave) does not propagate across more than one grid cell in a single time step.

For the two-dimensional SWE solved on a grid with spacings $\Delta x$ and $\Delta y$, the maximum [speed of information](@entry_id:154343) propagation in the $x$ and $y$ directions are $|u|+c$ and $|v|+c$, respectively, where $c=\sqrt{gh}$. For an **unsplit** explicit scheme, where fluxes in both directions are considered simultaneously, the stability constraint combines the Courant numbers from each dimension:
$$
\frac{(|u|+c)\Delta t}{\Delta x} + \frac{(|v|+c)\Delta t}{\Delta y} \le C_{\text{CFL}}
$$
where $C_{\text{CFL}}$ is the Courant number, a value typically chosen between $0$ and $1$. This inequality must be solved for $\Delta t$ at every grid cell, and the global time step for the simulation is taken as the minimum of these [local maximum](@entry_id:137813) allowable time steps. This ensures that the numerical method remains stable throughout the entire computational domain [@problem_id:3618076].