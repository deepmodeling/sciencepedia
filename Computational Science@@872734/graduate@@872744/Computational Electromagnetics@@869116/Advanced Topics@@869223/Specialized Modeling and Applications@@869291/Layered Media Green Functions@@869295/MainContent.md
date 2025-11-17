## Introduction
The analysis of [wave propagation](@entry_id:144063) in stratified environments is a fundamental problem that spans numerous scientific and engineering disciplines, from the design of integrated circuits to the study of seismic tremors. At the heart of this analysis lies the concept of the layered-media Green's function (LGF), a powerful mathematical construct that provides the exact field response to a point source within a complex, planar multilayer structure. While methods like the classical [method of images](@entry_id:136235) offer intuition in the [static limit](@entry_id:262480), they fail to capture the rich wave physics—including retardation, interference, and the excitation of guided modes—that dominate at finite frequencies. This article addresses this gap by providing a comprehensive theoretical and practical guide to the LGF.

This exploration is structured into three distinct chapters. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, systematically building the LGF from the [spectral representation](@entry_id:153219) of a free-space source to the analysis of general multilayer stacks. The second chapter, "Applications and Interdisciplinary Connections," demonstrates the remarkable versatility of the LGF formalism, showcasing its pivotal role in fields as diverse as antenna engineering, geophysics, and [nanophotonics](@entry_id:137892). Finally, the "Hands-On Practices" chapter provides a set of guided problems designed to solidify understanding by applying these concepts to derive key results and build computational tools. Together, these chapters offer a complete journey into the theory and application of layered-media Green's functions, equipping the reader with a deep understanding of one of computational electromagnetics' most essential tools.

## Principles and Mechanisms

The formulation of the dyadic Green's function for a layered medium is a cornerstone of computational electromagnetics, enabling the analysis of a vast range of phenomena from integrated photonics to geophysical [remote sensing](@entry_id:149993). This chapter elucidates the fundamental principles and mechanisms underlying its construction and interpretation. We build the solution from the ground up, starting with the representation of a [point source](@entry_id:196698) in free space and progressively adding layers of complexity, culminating in a deep physical understanding of [wave propagation](@entry_id:144063) in stratified media.

### The Spectral Representation of the Free-Space Green's Function

The starting point for any layered media problem is the understanding of the field radiated by a [point source](@entry_id:196698) in a homogeneous, unbounded medium. This field is described by the free-space Green's function, which is the solution to the inhomogeneous Helmholtz equation for a Dirac delta function source. For a time-harmonic dependence of $e^{j\omega t}$ and a source at $\mathbf{r}'$, the scalar Green's function $G(\mathbf{r}, \mathbf{r}')$ satisfies:

$$(\nabla^2 + k_0^2) G(\mathbf{r}, \mathbf{r}') = -\delta(\mathbf{r}-\mathbf{r}')$$

where $k_0 = \omega \sqrt{\mu \varepsilon}$ is the [wavenumber](@entry_id:172452) of the medium. The solution, subject to the Sommerfeld radiation condition which ensures that waves are outgoing at infinity, is the familiar [spherical wave](@entry_id:175261):

$$G(\mathbf{r}, \mathbf{r}') = \frac{\exp(-j k_0 |\mathbf{r}-\mathbf{r}'|)}{4\pi |\mathbf{r}-\mathbf{r}'|}$$

While this form is intuitive in real space, it is not well-suited for problems involving planar boundaries. The key insight, developed by Hermann Weyl and Arnold Sommerfeld, is to represent this [spherical wave](@entry_id:175261) as a continuous superposition of plane waves. This is known as the **Weyl expansion** or **plane-wave spectrum**. By performing a three-dimensional Fourier transform on the Helmholtz equation, one can derive this integral representation. For a source at $\mathbf{r}'$ and an observation point $\mathbf{r}$, with $\Delta x = x-x'$, $\Delta y = y-y'$, and $\Delta z = z-z'$, the expansion is [@problem_id:3323149]:

$$ G(\mathbf{r},\mathbf{r}') = \iint_{\mathbb{R}^2} \frac{1}{(2\pi)^2} \frac{-j}{2k_z} \exp(-j (k_x \Delta x + k_y \Delta y)) \exp(-j k_z |\Delta z|) \, \mathrm{d}k_x\,\mathrm{d}k_y $$

Here, the integral is over the transverse spectral variables $k_x$ and $k_y$. The term $k_z$ is the **longitudinal wavenumber**, which is not an [independent variable](@entry_id:146806) but is constrained by the [dispersion relation](@entry_id:138513) in the medium: $k_x^2 + k_y^2 + k_z^2 = k_0^2$. This gives:

$$k_z = \sqrt{k_0^2 - k_x^2 - k_y^2} = \sqrt{k_0^2 - k_{\rho}^2}$$

where $k_{\rho} = \sqrt{k_x^2 + k_y^2}$ is the magnitude of the transverse wavevector. The square root function is multi-valued, and the choice of **branch** is critical. To satisfy the Sommerfeld radiation condition, we must ensure that all waves decay as they propagate to infinity. For propagating waves ($k_{\rho}  k_0$), $k_z$ is real, and the term $\exp(-j k_z |\Delta z|)$ represents an outgoing plane wave. For [evanescent waves](@entry_id:156713) ($k_{\rho} > k_0$), $k_z$ becomes purely imaginary. To ensure decay away from the source plane ($z=z'$), we must have $\exp(-j k_z |\Delta z|) = \exp(-|k_z'|||\Delta z|)$, where $k_z = -j|k_z'|$. This requires choosing the branch of the square root such that $\operatorname{Im}\{k_z\} \le 0$. This choice is fundamental to constructing physically correct Green's functions [@problem_id:3323149].

### Interaction with a Planar Interface: The Spectral Reflection Coefficient

When a [plane wave](@entry_id:263752) from the spectral expansion encounters an interface between two different media, it is partially reflected and partially transmitted. This process is governed by the [electromagnetic boundary conditions](@entry_id:188865), which demand the continuity of the tangential components of the electric ($\mathbf{E}$) and magnetic ($\mathbf{H}$) fields across the interface.

Consider an interface at $z=0$ separating medium 1 ($z>0$, parameters $\varepsilon_1, \mu_1$) from medium 2 ($z0$, parameters $\varepsilon_2, \mu_2$). Any [plane wave](@entry_id:263752) can be decomposed into two orthogonal polarizations with respect to the plane of incidence (the plane containing the [wavevector](@entry_id:178620) and the interface normal $\hat{\mathbf{z}}$):

1.  **Transverse Electric (TE)** polarization, where the electric field is perpendicular to the plane of incidence.
2.  **Transverse Magnetic (TM)** polarization, where the magnetic field is perpendicular to the plane of incidence.

By applying the boundary conditions to an incident, reflected, and transmitted [plane wave](@entry_id:263752) for each polarization and for each transverse [wavenumber](@entry_id:172452) $k_{\rho}$, we can solve for the amplitude ratios. These ratios are the **spectral Fresnel [reflection coefficients](@entry_id:194350)**.

For a TM-polarized spectral component incident from medium 1, the reflection coefficient $R_{TM}$, defined as the ratio of the reflected to incident tangential magnetic field amplitudes, is found to be [@problem_id:3323134]:

$$ R_{TM}(k_{\rho}) = \frac{\varepsilon_2 k_{z1} - \varepsilon_1 k_{z2}}{\varepsilon_2 k_{z1} + \varepsilon_1 k_{z2}} $$

Similarly, for a TE-polarized component, the reflection coefficient $R_{TE}$ is [@problem_id:3323166]:

$$ R_{TE}(k_{\rho}) = \frac{\mu_2 k_{z1} - \mu_1 k_{z2}}{\mu_2 k_{z1} + \mu_1 k_{z2}} $$

Here, $k_{zj} = \sqrt{\omega^2 \mu_j \varepsilon_j - k_{\rho}^2}$ is the longitudinal [wavenumber](@entry_id:172452) in medium $j$. These coefficients are functions of the transverse [wavenumber](@entry_id:172452) $k_{\rho}$ and encapsulate the full response of the interface to a single plane wave. The concept can be elegantly expressed using **wave admittances**, defined for each polarization as $Y^{\mathrm{TM}}_j = \omega \varepsilon_j / k_{zj}$ and $Y^{\mathrm{TE}}_j = k_{zj} / (\omega \mu_j)$. The [reflection coefficients](@entry_id:194350) then take the familiar transmission-line form $R = (Y_1 - Y_2) / (Y_1 + Y_2)$ for TM waves (defined by E-field ratio) or $R = (Z_2 - Z_1) / (Z_2 + Z_1)$ where impedance $Z=1/Y$ for both.

### Constructing the Half-Space Green's Function

With the Weyl expansion and the spectral [reflection coefficients](@entry_id:194350) in hand, we can construct the Green's function for a source in a half-space. The total field in medium 1 is the sum of the primary field (the free-space Green's function) and a scattered field produced by the reflection from the interface.

This is a **spectral method of images**. Each plane-wave component in the primary field's Weyl expansion is "reflected" by the interface. This reflection is accounted for by multiplying the plane-wave components incident on the interface by the spectral [reflection coefficient](@entry_id:141473) $R(k_\rho)$. The resulting scattered field, for an observer in medium 1, is equivalent to the field produced by an 'image' source located at $z=-z'$. The total spectral Green's function is the sum of the primary field and this image field:

$$ \tilde{G}_1(k_\rho, z) = \frac{-j}{2\varepsilon_1 k_{z1}} \left( e^{-j k_{z1}|z-z'|} + R e^{-j k_{z1}(z+z')} \right) $$

where $R$ is the appropriate TE or TM [reflection coefficient](@entry_id:141473). The spatial domain Green's function is then recovered by performing the inverse 2D Fourier transform, which due to [azimuthal symmetry](@entry_id:181872) becomes the Hankel transform:

$$ G(\mathbf{r}, \mathbf{r}') = \frac{1}{2\pi} \int_0^\infty \tilde{G}_1(k_\rho, z) J_0(k_\rho \rho) k_\rho \, \mathrm{d}k_\rho $$

This is a **Sommerfeld integral**. Its integrand can have singularities (poles and branch points) that correspond to physical wave phenomena. Poles in the [reflection coefficient](@entry_id:141473) $R(k_\rho)$ give rise to guided **[surface waves](@entry_id:755682)** that are bound to the interface. Branch points in the integrand, arising from the square roots in the $k_{zj}$ terms, give rise to **lateral waves** (or head waves) that travel along the interface. The remainder of the integral corresponds to the **space wave**, which includes the direct and reflected fields.

### Extension to Multilayer Media

The framework extends naturally to an arbitrary number of layers. For a stack of $N$ layers, the interaction of a plane wave is no longer described by a simple Fresnel coefficient but by a **generalized [reflection coefficient](@entry_id:141473)** $\tilde{R}(k_\rho)$ that accounts for the multiple reflections and transmissions at every interface.

This generalized coefficient can be calculated efficiently using a recursive procedure analogous to [transmission line theory](@entry_id:271266). One defines an **input [admittance](@entry_id:266052)** $Y_{\text{in}}$ at each interface, which represents the effective [admittance](@entry_id:266052) of all layers below it. Starting from the bottom semi-infinite half-space, where the input [admittance](@entry_id:266052) is simply its characteristic wave [admittance](@entry_id:266052), one can recursively "transfer" this [admittance](@entry_id:266052) up through the layers using the transmission-line formula for a loaded line. This yields the final input [admittance](@entry_id:266052) at the top interface, from which the overall generalized reflection coefficient is found. This powerful method is explored in detail in the hands-on practice problems [@problem_id:3323152].