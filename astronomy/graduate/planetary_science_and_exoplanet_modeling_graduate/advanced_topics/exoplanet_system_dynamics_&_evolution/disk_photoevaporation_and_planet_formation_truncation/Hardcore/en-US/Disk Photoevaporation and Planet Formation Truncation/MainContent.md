## Introduction
The end of the [planet formation](@entry_id:160513) era is marked by the dispersal of the protoplanetary disk, the gaseous and dusty nursery from which planets are born. This dispersal is not a passive fading but an active process that critically shapes the final architecture of planetary systems. Among the primary drivers of this evolution is **disk [photoevaporation](@entry_id:1129620)**, the erosion of the disk by high-energy radiation from its central star. Understanding this mechanism is key to answering fundamental questions: Why do gas disks have finite lifetimes of only a few million years? What processes truncate [planet formation](@entry_id:160513), determining the final masses and locations of planets? This article addresses these questions by providing a comprehensive overview of disk [photoevaporation](@entry_id:1129620).

First, the **Principles and Mechanisms** chapter will lay the physical foundation, explaining how different types of [stellar radiation](@entry_id:1132380) interact with the disk, defining the critical [gravitational radius](@entry_id:1125749) for gas escape, and describing the hydrodynamic nature of the resulting outflow. Next, the **Applications and Interdisciplinary Connections** chapter will explore the profound consequences of this process, detailing how [photoevaporation](@entry_id:1129620) sets the clock for [disk dispersal](@entry_id:1123842), sculpts the distribution of planetary building blocks, and impacts leading theories of [planet formation](@entry_id:160513). Finally, the **Hands-On Practices** section will offer practical problems that bridge theory and application, allowing you to model the key phenomena discussed. Through this structure, you will gain a deep understanding of how the energetic light from a star sculpts its own nascent planetary system.

## Principles and Mechanisms

The dispersal of a protoplanetary disk marks the end of the planet formation epoch. The mechanisms that drive this dispersal are not only responsible for the finite lifetime of gas in the disk but also play a crucial role in sculpting the final architecture of planetary systems. Among the most significant of these mechanisms is **photoevaporation**, the process by which high-energy radiation from the central star heats the disk surface, driving the gas away in a [thermal wind](@entry_id:149134). This chapter elucidates the fundamental principles governing [photoevaporation](@entry_id:1129620), from the energetic requirements for gas escape to the hydrodynamic nature of the outflow and its interplay with other [disk dispersal](@entry_id:1123842) processes.

### The Gravitational Radius: The Fundamental Scale of Photoevaporation

At its core, [photoevaporation](@entry_id:1129620) is a competition between the thermal energy of gas particles and the [gravitational potential energy](@entry_id:269038) that binds them to the central star. For a gas particle to escape the system, its kinetic energy must be comparable to or exceed the [gravitational binding energy](@entry_id:159053). In a gas heated to a temperature $T$, the characteristic thermal energy of a particle is on the order of $k_B T$, where $k_B$ is the Boltzmann constant. The gravitational potential energy of a particle of mass $m$ at a distance $r$ from a star of mass $M_\star$ is $U = -G M_\star m / r$.

A thermal wind can be launched from regions where the gas is sufficiently energized to become unbound. This defines a characteristic length scale known as the **[gravitational radius](@entry_id:1125749)**, $R_g$. It is the radius at which the thermal energy and [gravitational potential energy](@entry_id:269038) are of the same [order of magnitude](@entry_id:264888):

$k_B T \approx \frac{G M_\star m}{R_g}$

The mass of an average gas particle is given by $m = \mu m_H$, where $\mu$ is the mean molecular weight of the gas in units of the hydrogen atom mass, $m_H$. Substituting this and solving for $R_g$, we obtain the fundamental expression for the [gravitational radius](@entry_id:1125749):

$R_g = \frac{G M_\star \mu m_H}{k_B T}$

This simple yet powerful relation reveals the key dependencies of [photoevaporation](@entry_id:1129620). A higher gas temperature $T$ results in a smaller [gravitational radius](@entry_id:1125749), signifying that hotter gas can escape from deeper within the star's [potential well](@entry_id:152140). Conversely, a higher mean molecular weight $\mu$ leads to a larger $R_g$, as heavier particles require a weaker gravitational field (i.e., a larger distance from the star) to become unbound for a given temperature. The [gravitational radius](@entry_id:1125749) thus represents the approximate location within the disk where a photoevaporative wind is most efficiently launched.

### The Trinity of High-Energy Radiation: EUV, X-rays, and FUV

The [stellar radiation field](@entry_id:162022) that drives [photoevaporation](@entry_id:1129620) is broadband, but its effects can be understood by considering three primary high-energy components: Extreme Ultraviolet (EUV), X-rays, and Far Ultraviolet (FUV) photons. Each component interacts with the disk gas differently, heating it to a characteristic temperature and thereby defining a distinct [gravitational radius](@entry_id:1125749) and sphere of influence .

**Extreme Ultraviolet (EUV) Radiation:** EUV photons ($13.6 \ \text{eV} \lt E \lt 100 \ \text{eV}$) are energetic enough to photoionize hydrogen. Although the stellar EUV luminosity is often modest, this process is highly efficient at heating the gas. The balance between [photoionization](@entry_id:157870) heating and recombination cooling in the disk's surface layers establishes a hot, ionized atmosphere with a characteristic temperature of $T_{\mathrm{EUV}} \approx 10^4 \ \mathrm{K}$. In this [fully ionized plasma](@entry_id:200884), the mean molecular weight is low, typically $\mu_{\mathrm{EUV}} \approx 0.67$ (for a standard mixture of hydrogen and helium). The combination of a very high temperature and low mean molecular weight results in a small [gravitational radius](@entry_id:1125749). For a solar-mass star, this is:

$R_{g, \mathrm{EUV}} \approx 7 \ \mathrm{AU}$

This indicates that EUV-driven photoevaporation is an **inner-disk phenomenon**, primarily responsible for clearing gas from the region just outside the dust [sublimation](@entry_id:139006) radius.

**X-ray Radiation:** Stellar X-rays ($E \gt 100 \ \text{eV}$) are more penetrating than EUV photons and can heat a deeper and more extended column of gas. The primary heating mechanisms include [photoionization](@entry_id:157870) of both hydrogen and heavier elements, as well as Compton heating. The resulting gas is typically a warm, partially ionized atomic layer with a temperature of $T_{\mathrm{X}} \approx 4000 - 6000 \ \mathrm{K}$ and a mean molecular weight slightly enriched by atoms heavier than hydrogen, e.g., $\mu_{\mathrm{X}} \approx 0.7 - 1.3$. For a solar-mass star, taking $T_{\mathrm{X}} = 4000 \ \mathrm{K}$ and $\mu_{\mathrm{X}} = 0.7$ gives a characteristic radius of:

$R_{g, \mathrm{X}} \approx 19 \ \mathrm{AU}$

X-ray-driven winds thus operate at intermediate radii, acting on the main body of the [protoplanetary disk](@entry_id:158060) where giant planets are thought to form.

**Far Ultraviolet (FUV) Radiation:** FUV photons ($6 \ \text{eV} \lt E \lt 13.6 \ \text{eV}$) lack the energy to ionize hydrogen but are copiously produced by young stars. They heat the disk surface via [the photoelectric effect](@entry_id:162802) on small dust grains and Polycyclic Aromatic Hydrocarbons (PAHs). This process creates a warm, neutral atomic layer with a characteristic temperature of $T_{\mathrm{FUV}} \approx 1000 \ \mathrm{K}$. Since the gas is atomic and not ionized, its mean molecular weight is dominated by atomic hydrogen, giving $\mu_{\mathrm{FUV}} \approx 1.3$. The combination of a relatively low temperature with a higher mean molecular weight pushes the [gravitational radius](@entry_id:1125749) to much larger distances:

$R_{g, \mathrm{FUV}} \approx 140 \ \mathrm{AU}$

This large radius demonstrates that FUV radiation is the dominant driver of photoevaporation in the vast outer regions of the disk. It is this mechanism that is primarily responsible for truncating the gaseous disk at large radii ($\gtrsim 50 \ \mathrm{AU}$), setting an outer boundary for gas-[giant planet formation](@entry_id:1125633).

### Hydrodynamic Outflows: The Sonic Point and the Parker Wind

The concept of the [gravitational radius](@entry_id:1125749) provides an excellent energetic estimate for the location of a photoevaporative wind. However, the mass loss is not an instantaneous event but a continuous, accelerating fluid outflow. A more rigorous treatment requires a hydrodynamic approach, classically modeled by the **isothermal Parker wind** solution .

Consider a steady, spherically symmetric, [isothermal gas flow](@entry_id:191012) with sound speed $c_s$ escaping from a central mass $M_\star$. The flow is governed by the continuity equation ($\dot{M} = 4 \pi r^2 \rho u = \text{constant}$) and the Euler equation for fluid motion. Combining these equations yields the wind equation, which describes the [velocity gradient](@entry_id:261686) $\frac{du}{dr}$ of the flow:

$\frac{du}{dr} = \frac{u}{r^2} \frac{2 c_s^2 r - G M_\star}{u^2 - c_s^2}$

For a physically plausible solution that starts as a slow, subsonic breeze near the star and accelerates to a [supersonic outflow](@entry_id:755662) at large distances, the flow must pass smoothly through the sound speed, $u = c_s$. To avoid a singularity (an infinite velocity gradient) at this point, the numerator of the wind equation must simultaneously be zero. This unique location is the **[sonic point](@entry_id:755066)**, $r_s$, and its position is found by setting the numerator to zero:

$2 c_s^2 r_s - G M_\star = 0 \quad \implies \quad r_s = \frac{G M_\star}{2 c_s^2}$

The [sonic point](@entry_id:755066) is the critical radius beyond which the wind becomes supersonic. At this point, pressure waves, which travel at the sound speed, can no longer propagate upstream. The flow becomes causally disconnected from the subsonic region, and its fate is to escape the system. Therefore, the [sonic radius](@entry_id:161298) $r_s$ provides a more formal, hydrodynamically defined location for the launch point of the wind and can be interpreted as the truncation radius for the disk .

We can connect this hydrodynamic result to our earlier energetic argument by substituting the expression for the isothermal sound speed, $c_s^2 = k_B T / (\mu m_H)$. The [sonic radius](@entry_id:161298) becomes:

$r_s = \frac{G M_\star \mu m_H}{2 k_B T}$

Comparing this to the [gravitational radius](@entry_id:1125749), $R_g = \frac{G M_\star \mu m_H}{k_B T}$, we see an immediate and profound consistency. We find that $r_s = R_g / 2$. Both the simple energetic criterion and the full hydrodynamic solution identify the same physical scale, differing only by a factor of order unity. For an X-ray heated layer at $6000 \ \mathrm{K}$, the [sonic radius](@entry_id:161298) is found to be around $12 \ \mathrm{AU}$, providing a concrete example of the radius beyond which gas-mediated [planet formation](@entry_id:160513) would be truncated by this mechanism.

### Vertical Structure and Shielding: Why Photoevaporation is a Surface Effect

A crucial aspect of [photoevaporation](@entry_id:1129620) is that it is fundamentally a surface phenomenon. The high-energy photons from the star do not penetrate to the disk's dense, cold midplane where the initial stages of planet formation—the [coagulation](@entry_id:202447) of dust into planetesimals—take place. This shielding is a direct consequence of the disk's own vertical structure and opacity .

In a vertically isothermal disk in hydrostatic equilibrium, the [vertical pressure gradient](@entry_id:1133794) force balances the vertical component of the star's gravity. This leads to a Gaussian vertical [density profile](@entry_id:194142):

$\rho(z) = \rho_0 \exp \left( -\frac{z^2}{2 H^2} \right)$

where $\rho_0$ is the midplane density and $H$ is the pressure [scale height](@entry_id:263754). The total mass per unit area, the surface density $\Sigma$, is the integral of this profile from bottom to top. A remarkable and useful result emerges when one calculates the vertical optical depth from the disk's "surface" (at $z = \infty$) down to the midplane ($z = 0$). This half-column [optical depth](@entry_id:159017), $\tau_{1/2}$, is given by:

$\tau_{1/2}(r) = \frac{1}{2} \kappa \Sigma(r)$

where $\kappa$ is the mass [absorption coefficient](@entry_id:156541) (opacity) for the radiation in question. This means the ability of the disk to shield its midplane is directly proportional to its local [surface density](@entry_id:161889). The flux of radiation $F$ that penetrates to the midplane is then exponentially attenuated according to the Beer-Lambert law:

$F_{\mathrm{mid}}(r) = F_\star(r) \exp(-\tau_{1/2}(r)) = \frac{L_\star}{4\pi r^2} \exp \left( -\frac{1}{2} \kappa \Sigma(r) \right)$

In the inner regions of a typical [protoplanetary disk](@entry_id:158060), $\Sigma$ is large, making the [optical depth](@entry_id:159017) immense. The midplane is thus completely shielded from stellar FUV and EUV radiation, allowing it to remain cold and quiescent. Photoevaporation acts like a sandblaster, eroding the disk from the top down. Planet formation can proceed in the protected midplane until the overlying gas is stripped away, at which point the disk is rapidly dispersed.

### A Broader View: Photoevaporation vs. Magnetohydrodynamic Winds

While photoevaporation is a critical agent of [disk dispersal](@entry_id:1123842), it does not act in isolation. Another powerful mechanism, particularly in the earlier, more active phases of a disk's life, is the **magnetohydrodynamic (MHD) wind** . Understanding the interplay between these two processes is key to a complete picture of [disk evolution](@entry_id:162008).

MHD winds are driven not by thermal energy, but by magnetic forces. Magnetic field lines anchored in the rotating disk can act like centrifugal accelerators, flinging gas outwards and upwards. This process is extremely efficient at removing angular momentum from the disk, thereby enabling gas to accrete onto the central star. The [mass loss](@entry_id:188886) rate in an MHD wind, $\dot{M}_w$, is fundamentally linked to the disk accretion rate, $\dot{M}_{\mathrm{acc}}$, through a "[lever arm](@entry_id:162693)" parameter related to the magnetic field geometry. A typical relationship is $\dot{M}_w \approx \dot{M}_{\mathrm{acc}} / \lambda$, where $\lambda$ is a factor of a few.

A quantitative comparison reveals distinct roles for these two mechanisms. For a typical young T Tauri star, the [mass loss](@entry_id:188886) rate from an MHD wind can be $\dot{M}_w \sim 10^{-9} \ M_\odot \ \mathrm{yr}^{-1}$, whereas the total integrated mass loss rate from [photoevaporation](@entry_id:1129620) is often an order of magnitude lower, $\dot{M}_{pe} \sim 10^{-10} \ M_\odot \ \mathrm{yr}^{-1}$ . MHD winds can therefore dominate the global mass budget and drive the [secular evolution](@entry_id:158486) of the disk for much of its lifetime.

However, the two processes have very different spatial profiles. MHD winds are typically launched from a broad range of radii in the inner and intermediate disk. They contribute to a gradual, global depletion of disk mass but do not typically create a sharp edge. Photoevaporation, in contrast, acts most vigorously at the [gravitational radius](@entry_id:1125749), $R_g$. As the wind carves a gap at this radius, the inner disk drains onto the star, and the outer disk is exposed to direct stellar irradiation, leading to its rapid dispersal. This "inside-out" clearing, initiated at $R_g$, is what sets the final, sharp outer truncation radius of the gaseous disk.

In summary, MHD winds and photoevaporation are complementary processes. MHD winds likely govern the long-term, high-accretion phase of [disk evolution](@entry_id:162008). As the accretion rate wanes and the disk surface density drops, photoevaporation takes over as the dominant agent of final dispersal. It is the FUV-driven photoevaporative wind that sets the outer boundary of the gas disk, thereby truncating the process of [giant planet formation](@entry_id:1125633) and leaving a lasting imprint on the final architecture of the planetary system.