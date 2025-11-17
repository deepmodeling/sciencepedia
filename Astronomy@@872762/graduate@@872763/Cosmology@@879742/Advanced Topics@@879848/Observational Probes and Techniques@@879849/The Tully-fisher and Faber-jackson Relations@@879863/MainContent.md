## Introduction
In the vast and varied census of galaxies, astronomers have discovered remarkable regularities known as [scaling relations](@entry_id:136850)—tight empirical correlations that link a galaxy's luminous properties to its internal dynamics. Among the most foundational of these are the Tully-Fisher relation for [spiral galaxies](@entry_id:162037) and the Faber-Jackson relation for ellipticals. These are not mere cosmic coincidences; they are powerful windows into the fundamental physics governing galaxy formation and evolution. The core challenge these relations pose is to explain why the visible, baryonic matter of a galaxy should be so intimately tied to its total gravitational potential, which is thought to be dominated by unseen dark matter. Addressing this gap requires delving into the intricate processes that shape galaxies over billions of years.

This article provides a comprehensive exploration of these two pivotal [scaling relations](@entry_id:136850). In the first chapter, "Principles and Mechanisms," we will derive the relations from first principles, exploring explanations rooted in both the standard dark matter paradigm and the alternative theory of Modified Newtonian Dynamics (MOND). The second chapter, "Applications and Interdisciplinary Connections," will demonstrate how these laws are leveraged as powerful tools, from measuring the expansion of the universe to probing galaxy mergers and the nature of dark matter. Finally, "Hands-On Practices" will allow you to apply these concepts to solve practical astrophysical problems, solidifying your understanding of how these theoretical relations connect to observable data.

## Principles and Mechanisms

The empirical [scaling relations](@entry_id:136850) observed in galaxy populations are not mere curiosities; they are profound observational windows into the physics of galaxy formation and the nature of gravity itself. These relations connect the luminous, baryonic components of galaxies, which are relatively easy to observe, to the kinematic properties that trace the underlying [gravitational potential](@entry_id:160378), whether it is dominated by baryons, dark matter, or a modification of gravity. This chapter will explore the fundamental principles and physical mechanisms that are believed to give rise to the Tully-Fisher relation for [spiral galaxies](@entry_id:162037) and the Faber-Jackson relation and Fundamental Plane for [elliptical galaxies](@entry_id:158253).

### The Tully-Fisher Relation for Spiral Galaxies

The Tully-Fisher relation is a cornerstone of extragalactic astronomy, linking the total luminosity $L$ of a spiral galaxy to its maximum rotation velocity $v_{max}$. This velocity is typically measured from the flattened, "asymptotic" part of the galaxy's rotation curve. The relation takes the form of a power law, $L \propto v_{max}^{\alpha}$, where the exponent $\alpha$ is empirically found to be in the range of 3 to 4, depending on the photometric band used to measure luminosity.

A more physically fundamental version of this law is the **Baryonic Tully-Fisher Relation (BTFR)**, which replaces luminosity with the total baryonic mass $M_b$ (the sum of [stellar mass](@entry_id:157648) $M_*$ and gas mass $M_g$). The BTFR is an exceptionally tight correlation, expressed as:

$$ M_b \propto v_{max}^4 $$

The tightness and near-universal slope of the BTFR suggest it stems from a deep physical connection between the mass of a galaxy and the depth of the potential well in which it resides.

#### A First-Principles Derivation

A surprisingly successful theoretical derivation of the Tully-Fisher relation can be constructed from a simple, yet physically motivated, model of a disk galaxy embedded within a dominant dark matter halo [@problem_id:893429]. Let us consider a model built on three core assumptions:
1.  The galaxy's dynamics are dominated by a dark matter halo that produces a flat rotation curve, meaning the [circular velocity](@entry_id:161552) $v_c$ is constant with radius. This is characteristic of a **Singular Isothermal Sphere (SIS)** [density profile](@entry_id:194142), $\rho(r) \propto r^{-2}$. For such a halo, the enclosed mass scales linearly with radius, $M(r) = \frac{v_c^2 r}{G}$.
2.  The stellar disk has a constant average surface mass density, $\Sigma_* = M_* / (\pi R^2)$, where $R$ is a characteristic radius of the disk. This implies that more massive galaxies are also proportionally larger.
3.  The [stellar mass](@entry_id:157648) $M_*$ is directly proportional to the dark matter mass enclosed within the same characteristic radius $R$, i.e., $M_* \propto M_{DM}(R)$. This assumes a tight coupling between the formation of the stellar disk and the local dark matter content.

From these assumptions, we can derive the scaling exponent. If we assume a constant [stellar mass](@entry_id:157648)-to-light ratio $\Upsilon_* = M_*/L$, then $L \propto M_*$. Our goal is to relate $M_*$ to $v_c$, which we take to be equal to the observed $v_{max}$.

From assumption 2, we have $M_* \propto R^2$. From assumption 3, we have $M_* \propto M_{DM}(R)$. For an SIS halo (assumption 1), $M_{DM}(R) \propto v_c^2 R$. Equating the expressions for $M_*$ gives $R^2 \propto v_c^2 R$, which implies $R \propto v_c^2$.

Now, substituting this scaling for the radius back into the expression for [stellar mass](@entry_id:157648), we find:

$$ M_* \propto R^2 \propto (v_c^2)^2 = v_c^4 $$

Since we assumed $L \propto M_*$, it follows directly that $L \propto v_c^4$. This remarkably simple model, based on plausible physical [scaling arguments](@entry_id:273307), correctly reproduces the exponent of the Baryonic Tully-Fisher Relation. This success suggests that the observed relation is a natural consequence of disk galaxies forming within dark matter halos that possess roughly isothermal density profiles.

#### Cosmological Origin of the Tully-Fisher Relation

While the SIS model provides a simple physical basis, a more sophisticated understanding emerges from the modern cosmological framework of galaxy formation, where galaxies form from the cooling of baryonic gas within hierarchically growing [dark matter halos](@entry_id:147523) [@problem_id:893393].

In this picture, a dark matter halo of mass $M_h$ first collapses and virializes out of the [expanding universe](@entry_id:161442). Its properties, such as its virial radius $r_{vir}$ and virial velocity $v_{vir} = \sqrt{G M_h / r_{vir}}$, are determined by its mass and the cosmological epoch at which it collapses. A fraction $m_d$ of the halo's mass is in the form of baryons, $M_d = m_d M_h$. This gas is shock-heated but possesses angular momentum, inherited from tidal torques during structure formation. The [total angular momentum](@entry_id:155748) of the halo is often parameterized by the dimensionless **spin parameter** $\lambda$.

As the gas radiates energy, it cools and sinks to the center of the halo's [potential well](@entry_id:152140). Crucially, while energy is lost, angular momentum is largely conserved. The gas settles into a rotationally supported disk. The final size of this disk, characterized by a scale length $r_d$, is determined by the requirement that its angular momentum matches the initial angular momentum of the gas. For an exponential disk with a flat rotation curve $v_c$, this leads to a direct relationship between the disk scale length and the halo's virial radius and spin: $r_d \propto \lambda r_{vir}$.

This framework allows for a more detailed derivation of the TF relation. The key insight is that [star formation](@entry_id:160356) efficiency, and thus the mass-to-light ratio $\Upsilon$, may not be constant. It is plausible that feedback processes from stars and supernovae are more effective in galaxies with lower gas densities. We can model this by allowing the inverse mass-to-light ratio to depend on the central surface mass density of the disk, $\Sigma_0 = M_d / (2\pi r_d^2)$, for instance as a power law: $\Upsilon^{-1} \propto \Sigma_0^\beta$.

Combining these ingredients—virial [scaling relations](@entry_id:136850) for halos, [angular momentum conservation](@entry_id:156798) for disk formation, and a density-dependent star formation efficiency—we can derive the relationship between a galaxy's final luminosity $L = M_d \Upsilon^{-1}$ and its [circular velocity](@entry_id:161552) $v_c$ (which is tied to the halo's virial velocity). This more complex model predicts a scaling $L \propto v_c^{\alpha}$ where the exponent is $\alpha = \beta + 3$. The simple $L \propto v_c^4$ relation is recovered only if $\beta=1$, meaning the [star formation](@entry_id:160356) efficiency scales linearly with the central [surface density](@entry_id:161889) of the disk. This illustrates how the observed slope of the Tully-Fisher relation can encode complex baryonic physics related to feedback and star formation.

#### Relating Observational and Theoretical Velocities

A further subtlety arises when connecting theory to observation. The Baryonic Tully-Fisher Relation uses the maximum [circular velocity](@entry_id:161552) $v_{max}$, an observable quantity. Theoretical models, however, often work with the virial velocity $V_{vir}$ of the host dark matter halo. These two velocities are not identical [@problem_id:893418]. For realistic halo profiles like the Navarro-Frenk-White (NFW) profile, the ratio $v_{max}/V_{vir}$ depends on the halo's **concentration** $c$, a parameter describing the steepness of its inner [density profile](@entry_id:194142).

Furthermore, observations show a systematic mass-concentration relation, where less massive halos are more concentrated. If we combine the standard BTFR ($M_b \propto v_{max}^4$), a constant [baryon fraction](@entry_id:160399) ($M_b \propto M_{vir}$), the halo virial relations ($M_{vir} \propto V_{vir}^3$), and the observed mass-concentration relation, we can derive the emergent scaling between the two velocity measures. This [self-consistency](@entry_id:160889) requirement leads to a non-linear relationship:

$$ v_{max} \propto V_{vir}^{3/4} $$

This result highlights the importance of halo structure. Even if a perfect linear relationship exists between baryonic mass and a halo's potential well depth (probed by $V_{vir}$), the translation to the observable $v_{max}$ introduces a non-trivial scaling due to systematic changes in halo density profiles with mass.

### Scaling Relations for Elliptical Galaxies

Elliptical galaxies, being pressure-supported systems rather than rotationally supported disks, obey a different set of [scaling relations](@entry_id:136850). The analogue to the Tully-Fisher relation is the **Faber-Jackson (FJ) relation**, which connects a galaxy's luminosity to its central [stellar velocity dispersion](@entry_id:161232) $\sigma_0$:

$$ L \propto \sigma_0^\gamma $$

where the empirically determined exponent $\gamma$ is typically around 4.

#### The Virial Origin of the Faber-Jackson Relation

The physical basis for the Faber-Jackson relation is the **[virial theorem](@entry_id:146441)**, which governs the equilibrium state of [self-gravitating systems](@entry_id:155831). For a system of total mass $M$ and characteristic radius $R_e$, the [virial theorem](@entry_id:146441) states that $2K + U = 0$, where $K$ is the total kinetic energy and $U$ is the total [gravitational potential energy](@entry_id:269038).

The kinetic energy of the stellar system is related to the velocity dispersion of its stars, $K \propto M \sigma_0^2$. The potential energy depends on the [mass distribution](@entry_id:158451), but generally scales as $U \propto -G M^2 / R_e$. Applying the [virial theorem](@entry_id:146441) gives:

$$ M \sigma_0^2 \propto \frac{G M^2}{R_e} \quad \implies \quad M \propto \sigma_0^2 R_e $$

This is a fundamental prediction for any homologous family of virialized systems. It states that mass is determined by a combination of size and internal velocity. The Faber-Jackson relation emerges from this if there is a systematic relationship between a galaxy's mass and its size [@problem_id:893437]. Let's assume galaxies follow a general **mass-size relation** of the form $R_e \propto M^\delta$. Substituting this into the virial relation gives:

$$ M \propto \sigma_0^2 (M^\delta) \quad \implies \quad M^{1-\delta} \propto \sigma_0^2 $$

Solving for mass, we find $M \propto \sigma_0^{2/(1-\delta)}$. If we assume a constant mass-to-light ratio ($M \propto L$), we recover the Faber-Jackson relation $L \propto \sigma_0^\gamma$ with a theoretical exponent of:

$$ \gamma = \frac{2}{1-\delta} $$

For the observed value of $\gamma \approx 4$, this implies a mass-size exponent of $\delta \approx 0.5$, meaning $R_e \propto M^{0.5}$. This is reasonably close to the observed mass-size relations for massive [elliptical galaxies](@entry_id:158253), providing a powerful demonstration that the Faber-Jackson relation is a direct consequence of virial equilibrium and the structural scaling of galaxies.

#### The Fundamental Plane and its Tilt

The Faber-Jackson relation, while foundational, exhibits considerable scatter. This scatter is significantly reduced when a third parameter, related to the galaxy's size or surface brightness, is included. This reveals that [elliptical galaxies](@entry_id:158253) do not lie on a line, but on a two-dimensional surface within the three-dimensional space of their properties. This surface is known as the **Fundamental Plane**, an empirical power-law relationship between the effective radius $R_e$, the [central velocity dispersion](@entry_id:158756) $\sigma_0$, and the mean surface brightness within that radius, $I_e$:

$$ R_e \propto \sigma_0^a I_e^b $$

The simple [virial theorem](@entry_id:146441), combined with a constant mass-to-light ratio $\Upsilon = M/L$, makes a clear prediction for the exponents $a$ and $b$. From the definitions $L \propto I_e R_e^2$ and the virial relation $M \propto \sigma_0^2 R_e$, a constant $\Upsilon$ implies $M \propto L$, so $\sigma_0^2 R_e \propto I_e R_e^2$. This simplifies to $R_e \propto \sigma_0^2 I_e^{-1}$, predicting $a=2$ and $b=-1$.

However, observations consistently find different values, typically $a \approx 1.4$ and $b \approx -0.85$. This discrepancy is known as the **"tilt" of the Fundamental Plane**. It signifies that one or more of the simple assumptions underlying the virial prediction must be incorrect. The tilt provides crucial clues about the systematic properties of [elliptical galaxies](@entry_id:158253).

Two primary physical mechanisms can produce this tilt:
1.  **Systematic Variation of the Mass-to-Light Ratio:** The assumption that $\Upsilon$ is constant for all [elliptical galaxies](@entry_id:158253) may be false. Stellar [population models](@entry_id:155092) suggest that more massive galaxies tend to be older and have higher metallicities, both of which increase their $\Upsilon$. Furthermore, the fraction of dark matter within the effective radius might increase with galaxy mass. If $\Upsilon$ varies systematically with mass or luminosity (e.g., $\Upsilon \propto L^\beta$), the simple equivalence between mass and light breaks down [@problem_id:893544].
2.  **Structural Non-Homology:** The assumption that all [elliptical galaxies](@entry_id:158253) are structurally homologous (i.e., have identically shaped mass profiles) may also be incorrect. If the constant of proportionality in the virial potential energy term $U = -k G M^2/R_e$ changes systematically with galaxy mass, this introduces a "non-homology" term. This can be modeled as a modified virial relation, $M \propto \sigma_0^2 R_e M^\xi$ [@problem_id:893447].

By incorporating a systematically varying mass-to-light ratio (e.g., $\Upsilon \propto L^\beta \sigma_0^\gamma$) into the virial derivation, one can derive new theoretical expressions for the Fundamental Plane exponents $a$ and $b$ that depend on $\beta$ and $\gamma$. Matching these to the observed exponents allows astronomers to constrain how the mass-to-light ratio must vary across the elliptical galaxy population, providing insights into their [star formation](@entry_id:160356) histories and dark matter content [@problem_id:893544] [@problem_id:893543]. Similarly, accounting for non-homology allows one to solve for the required M/L variation to explain the observed [scaling relations](@entry_id:136850), providing a powerful tool to disentangle stellar population effects from structural ones [@problem_id:893447].

### The Physical Information in Scatter

The [scaling relations](@entry_id:136850) discussed are not perfect laws but statistical trends with intrinsic scatter. This scatter is not merely measurement error; it contains valuable [physical information](@entry_id:152556) about the diversity of galaxy properties and formation histories at a fixed mass or velocity.

Consider the observed scatter in the Baryonic Tully-Fisher Relation, $\sigma_b$. Its origin can be deconstructed by tracing it back through the chain of physical connections [@problem_id:893424]. The BTFR connects baryonic mass ($M_b$) to rotation velocity ($V_{max}$). In the [standard cosmological model](@entry_id:159833), $V_{max}$ is determined by the host [dark matter halo](@entry_id:157684) mass ($M_h$), while $M_b$ is related to $M_h$ via the complex processes of star and galaxy formation, often summarized by the Stellar Mass-Halo Mass (SMHM) relation.

If we assume that the relation between halo mass and $V_{max}$ is perfect (scatter-free), then any scatter in the BTFR must originate from scatter in the relationship between $M_b$ and $M_h$. This scatter in the SMHM relation, $\sigma_*$, is a key prediction of galaxy formation simulations, reflecting the stochastic nature of gas accretion, feedback, and mergers. By carefully analyzing the observed scatter $\sigma_b$ and accounting for how the fitting procedure itself can couple with existing trends (e.g., the distribution of velocities in the sample), one can place constraints on the intrinsic scatter $\sigma_*$ of the underlying physical relations. This transforms scatter from a nuisance into a quantitative probe of the variance in galaxy formation efficiency.

### An Alternative Perspective: Modified Newtonian Dynamics (MOND)

An entirely different physical mechanism for these [scaling relations](@entry_id:136850) is proposed by **Modified Newtonian Dynamics (MOND)**. Instead of postulating dark matter, MOND suggests that Newton's law of gravity is modified at extremely low accelerations, specifically those below a new fundamental constant of nature, $a_0 \approx 1.2 \times 10^{-10} \text{ m/s}^2$. In this "deep MOND regime," the true gravitational acceleration $g$ is related to the standard Newtonian acceleration $g_N$ by $g = \sqrt{g_N a_0}$.

Remarkably, MOND provides a natural and direct explanation for the Baryonic Tully-Fisher Relation. For a test particle in a [circular orbit](@entry_id:173723) in the outskirts of a galaxy (where accelerations are low), the [centripetal acceleration](@entry_id:190458) is $a_{cent} = v_c^2/r$. The Newtonian acceleration from the galaxy's total baryonic mass $M_b$ is $g_N = G M_b/r^2$. Equating the centripetal acceleration to the MOND acceleration yields:

$$ \frac{v_c^2}{r} = g = \sqrt{\frac{G M_b}{r^2} a_0} = \frac{\sqrt{G M_b a_0}}{r} $$

The radius $r$ cancels, leading directly to a fundamental relationship between velocity and mass [@problem_id:893451]:

$$ v_c^4 = G a_0 M_b $$

This result is extraordinary. MOND predicts *a priori* that the baryonic mass of a spiral galaxy should scale with the fourth power of its asymptotic velocity, exactly as observed in the BTFR. The proportionality constant is predicted to be a combination of [fundamental constants](@entry_id:148774), $1/(G a_0)$.

MOND makes a similar prediction for pressure-supported systems. By analyzing the [hydrostatic equilibrium](@entry_id:146746) of a self-gravitating, [isothermal sphere](@entry_id:159991) in the deep MOND regime, one can derive a Faber-Jackson-like relation [@problem_id:893428]. The analysis shows that the total mass $M$ of the system must scale with the fourth power of its velocity dispersion:

$$ M \propto \frac{\sigma^4}{G a_0} $$

Again, MOND predicts a [scaling exponent](@entry_id:200874) of $\gamma=4$, in close agreement with observations of [elliptical galaxies](@entry_id:158253). The ability of MOND to predict these two fundamental [scaling relations](@entry_id:136850) from first principles, without the need for dark matter or fine-tuning of its distribution, stands as one of the theory's most compelling successes.