## Introduction
In modern cosmology, large-scale N-body simulations provide a remarkably accurate picture of how dark matter structures grow and cluster under the influence of gravity. However, these simulations do not inherently produce the luminous galaxies we observe. Subhalo Abundance Matching (SHAM) has emerged as a powerful and physically intuitive empirical framework to bridge this critical gap, providing a prescription for populating simulated dark matter halos with galaxies. This method addresses the fundamental problem of establishing the "galaxy–halo connection," which is essential for comparing theoretical predictions with observational data from galaxy surveys. This article provides a graduate-level exploration of SHAM, detailing its theoretical underpinnings, practical applications, and role at the forefront of cosmological research.

This journey into Subhalo Abundance Matching is structured across three comprehensive chapters. First, in **"Principles and Mechanisms,"** we will dissect the core methodology, starting from the simple concept of equating number densities and building up to modern implementations that account for scatter, distinguish between central and satellite galaxies, and carefully select robust halo properties. Next, **"Applications and Interdisciplinary Connections"** will demonstrate the power of SHAM in practice, showing how it is used to generate [mock galaxy catalogs](@entry_id:752051), predict key observables like galaxy clustering, and probe complex phenomena such as [halo assembly bias](@entry_id:750135), connecting [large-scale structure](@entry_id:158990) with galaxy evolution. Finally, **"Hands-On Practices"** will offer a set of targeted problems designed to solidify your understanding of the method's practical challenges and nuances. We will begin by exploring the foundational principles and operational mechanics that make SHAM a cornerstone of modern [numerical cosmology](@entry_id:752779).

## Principles and Mechanisms

Subhalo Abundance Matching (SHAM) is a powerful and intuitive empirical technique for establishing the connection between galaxies and the dark matter halos in which they reside. Having been introduced in the preceding chapter, we now delve into the foundational principles and operational mechanisms that underpin this method. We will begin with the simplest formulation of SHAM and progressively build towards the more sophisticated implementations used in contemporary cosmological research, exploring the physical motivations and practical necessities that drive each refinement.

### The Core Principle: Matching Cumulative Abundances

The fundamental premise of Subhalo Abundance Matching is that the most massive galaxies reside in the "largest" dark matter halos. In its most direct form, this is expressed as a monotonic, [one-to-one correspondence](@entry_id:143935) between a galaxy property—most commonly [stellar mass](@entry_id:157648), $M_{\star}$—and a [dark matter halo](@entry_id:157684) property, $X$. This halo property, or proxy, is chosen to be a quantity that is expected to correlate strongly with the conditions for galaxy formation, such as the halo's mass or the depth of its [potential well](@entry_id:152140).

This [monotonic relationship](@entry_id:166902) is established by **equating the cumulative number densities** of galaxies and halos. Given an observed galaxy stellar [mass function](@entry_id:158970) $\phi(M_{\star})$, which provides the comoving [number density](@entry_id:268986) of galaxies per unit [stellar mass](@entry_id:157648), we can define the cumulative [number density](@entry_id:268986) of galaxies more massive than $M_{\star}$ as:

$n_{\text{gal}}(>M_{\star}) = \int_{M_{\star}}^{\infty} \phi(M'_{\star}) \, dM'_{\star}$

Similarly, from a cosmological N-body simulation, we can measure the distribution of a halo property $X$, denoted $\psi(X)$, and compute its cumulative [number density](@entry_id:268986):

$n_{\text{(sub)halo}}(>X) = \int_{X}^{\infty} \psi(X') \, dX'$

The core assumption of zero-scatter SHAM is then formalized by the simple equation:

$n_{\text{gal}}(>M_{\star}) = n_{\text{(sub)halo}}(>X)$

This equation implicitly defines the [monotonic function](@entry_id:140815) $M_{\star}(X)$ or its inverse $X(M_{\star})$. For any given [stellar mass](@entry_id:157648) $M_{\star}$, one computes the number density of galaxies above it, $n_{\text{gal}}(>M_{\star})$, and then finds the unique value of $X$ such that the [number density](@entry_id:268986) of halos with property greater than $X$ is the same. This establishes a unique pairing. In practice, this is implemented by rank-ordering: the most massive galaxy in the observed volume is assigned to the halo with the highest value of $X$, the second-most massive galaxy to the second-highest-ranked halo, and so on.

It is critical to note that this procedure does not imply that the differential functions $\phi(M_{\star})$ and $\psi(X)$ have the same shape. Differentiating the abundance matching equation with respect to $M_{\star}$ reveals the true relationship:

$\phi(M_{\star}) = \psi(X(M_{\star})) \frac{dX}{dM_{\star}}$

The two differential functions are related by the Jacobian of the transformation, $\frac{dX}{dM_{\star}}$. Indeed, the typically different shapes of the galaxy stellar [mass function](@entry_id:158970) and, for example, the [halo mass function](@entry_id:158011) are what give rise to a non-trivial, non-linear $M_{\star}(X)$ relationship [@problem_id:3492424].

This direct-mapping approach distinguishes SHAM fundamentally from other techniques like the **Halo Occupation Distribution (HOD)**. The HOD framework is statistical in nature, specifying the probability distribution, $P(N|M_{\text{halo}})$, that a host halo of mass $M_{\text{halo}}$ contains $N$ galaxies of a certain type. HOD models populate halos based on this probability, without mapping individual galaxies to specific subhalos, whereas SHAM establishes precisely such a mapping, allowing galaxies in a [mock catalog](@entry_id:752048) to inherit the full phase-space information (position and velocity) of their assigned subhalo [@problem_id:3492424].

### Defining the Halo Population: Centrals and Satellites

A crucial decision in any SHAM implementation is defining the pool of "(sub)halos" to be matched. A simulation provides a catalog of distinct, isolated **host halos** as well as gravitationally self-bound **subhalos** orbiting within them. One could choose to match galaxies to a list of only the distinct host halos, or to a combined list of all host halos and subhalos.

This choice has significant consequences. The cumulative [number density](@entry_id:268986) of all (sub)halos, $n_{\text{(sub)halo}}(>X)$, is by definition greater than or equal to that of distinct halos alone, $n_{\text{halo}}(>X)$. Including subhalos increases the size of the population available for matching. Therefore, to match a fixed galaxy abundance $n_{\text{gal}}(>M_{\star})$, one must go to a higher value of the proxy $X$ when using the full (sub)halo catalog compared to using only the distinct halo catalog. That is, if $n_{\text{gal}}(>M_{\star}) = n_{\text{halo}}(>X_{\text{d}}) = n_{\text{(sub)halo}}(>X_{\text{a}})$, then it must be that $X_{\text{a}} > X_{\text{d}}$ [@problem_id:3492485].

This consideration leads to a more physically motivated picture. The galaxy population is not monolithic; it consists of **central galaxies**, which are the dominant galaxy at the center of a host halo, and **satellite galaxies**, which orbit within the host halo. This naturally corresponds to the division in the simulation catalog: central galaxies are associated with host halos, and satellite galaxies are associated with subhalos.

Modern SHAM implementations therefore treat these two populations separately. This requires observational inputs that decompose the total stellar [mass function](@entry_id:158970) into its central and satellite components, $\phi_{\text{cen}}(M_{\star})$ and $\phi_{\text{sat}}(M_{\star})$. The matching procedure is then performed independently for each population:
- Central galaxies are matched to the catalog of distinct host halos.
- Satellite galaxies are matched to the catalog of subhalos.

This separate treatment is essential for accurately reproducing not just the overall stellar [mass function](@entry_id:158970), but also galaxy clustering and other environment-dependent properties [@problem_id:3492447].

### Choosing a Robust Proxy for Stellar Mass

The success of SHAM hinges on the choice of a halo proxy $X$ that has a tight, monotonic correlation with galaxy [stellar mass](@entry_id:157648). This choice is especially critical for satellite galaxies, which undergo significant evolution after they are accreted into a larger host halo. Two primary environmental processes drive this evolution:

1.  **Dynamical Friction**: A satellite subhalo moving through the dark matter background of its host experiences a gravitational drag force. This causes it to lose [orbital energy](@entry_id:158481) and angular momentum, leading it to spiral inward toward the host's center [@problem_id:3492416]. This process is more efficient for more massive subhalos.

2.  **Tidal Stripping**: The host halo's gravitational field exerts a [tidal force](@entry_id:196390) across the satellite subhalo. Material outside the subhalo's **tidal radius**—the point at which the host's differential pull overcomes the subhalo's self-gravity—is stripped away. As a subhalo sinks deeper into the host due to [dynamical friction](@entry_id:159616), the ambient density increases and the tidal radius shrinks, leading to progressive [mass loss](@entry_id:188886).

This "outside-in" stripping process preferentially removes the loosely bound outer layers of a subhalo's dark matter. In contrast, the stellar component of the satellite galaxy is much more compact and deeply embedded in the subhalo's central potential well. As a result, a subhalo can lose a substantial fraction of its dark matter mass while its [stellar mass](@entry_id:157648) remains largely intact [@problem_id:3492416].

This physical picture informs the choice of a robust proxy. Common proxies extracted from simulations include:
- **Present-day properties**: such as the currently bound mass, $M(z=0)$, or the current maximum of the [circular velocity](@entry_id:161552) profile, $V_{\max}(z=0)$.
- **Historical properties**: such as the mass at the time of accretion, $M_{\text{acc}}$; the peak mass ever attained, $M_{\text{peak}}$; or the peak value of the maximum [circular velocity](@entry_id:161552) over the subhalo's history, **$V_{\text{peak}}$**.

For satellite galaxies, present-day properties like $M(z=0)$ and $V_{\max}(z=0)$ are poor proxies. Their values are significantly reduced by [tidal stripping](@entry_id:160026), breaking the simple [monotonic relationship](@entry_id:166902) with the pre-existing [stellar mass](@entry_id:157648). Historical properties, however, are immune to this post-infall evolution by definition. They capture the state of the halo when the galaxy's [stellar mass](@entry_id:157648) was largely established. Among these, $V_{\text{peak}}$ is often favored as it is a measure of the depth of the inner [potential well](@entry_id:152140) and is less sensitive to the precise definition of a halo's outer boundary than mass proxies. Therefore, a robust SHAM implementation for satellites should map $M_{\star}$ to a property like $V_{\text{peak}}$ or $M_{\text{peak}}$ [@problem_id:3492445]. For central galaxies, which are not subject to stripping, present-day properties like $V_{\max}(z=0)$ or halo mass are appropriate.

### Incorporating Scatter and Correcting for Bias

The assumption of a perfect one-to-one mapping between $M_{\star}$ and $X$ is an oversimplification. A more realistic model includes intrinsic scatter in this relationship, meaning that halos with the exact same value of $X$ can host galaxies with a distribution of stellar masses. This is formalized by a [conditional probability distribution](@entry_id:163069), $P(M_{\star}|X)$.

When scatter is included, the abundance matching condition becomes an integral equation. The total [number density](@entry_id:268986) of galaxies above a certain mass is found by summing the contributions from all halos, weighted by the probability that they host such a galaxy:

$n_{\text{gal}}(>M_{\star}) = \int \psi(X') \left[ \int_{M_{\star}}^{\infty} P(M''_{\star}|X') \, dM''_{\star} \right] dX'$  [@problem_id:3492424]

The introduction of scatter has two profound consequences. First, it reinforces the importance of choosing a good proxy. The physical processes of stripping introduce a diversity of orbital histories for satellites. This leads to a range of stripping efficiencies (i.e., a scatter in the fraction of mass retained, $s$). If one uses a present-day proxy like $V_{\max}(z=0)$, this environmental scatter in $s$ propagates into the $M_{\star}-V_{\max}(z=0)$ relation, artificially increasing its total scatter. By using a historical proxy like $V_{\text{peak}}$, which is defined before stripping occurs, this source of environmental scatter is eliminated, resulting in a tighter intrinsic correlation [@problem_id:3492403].

Second, scatter introduces a systematic statistical effect known as **Eddington bias**. Both the halo and galaxy mass functions are steep, falling rapidly towards high masses. When scatter is applied to the $M_{\star}-X$ relation, random upward fluctuations from the more numerous, lower-mass population will outnumber random downward fluctuations from the less numerous, higher-mass population. The net effect is that simply applying scatter to a zero-scatter mapping will over-produce massive galaxies and fail to reproduce the target stellar [mass function](@entry_id:158970).

To properly implement scatter, one cannot simply add noise as a final step. Instead, an iterative procedure is required. One must find the underlying *mean* relation, $\langle \log M_{\star} \rangle(X)$, such that when this relation is convolved with the scatter kernel $P(M_{\star}|X)$, the resulting galaxy number densities correctly match the observed ones. This typically involves iteratively adjusting the mean relation until the convolved model converges to the target stellar [mass function](@entry_id:158970) [@problem_id:3492447].

A non-iterative but equally powerful method to implement SHAM with scatter relies on rank-ordering [@problem_id:3492452]. The procedure is:
1. Start with an initial guess for the mean monotonic relation, $M_{\star}^{\text{det}}(X)$.
2. For each subhalo, generate a "scattered" [stellar mass](@entry_id:157648) by drawing from the scatter distribution: $M_{\star}^{\text{scat}} = M_{\star}^{\text{det}}(X) \times \exp(\delta)$, where $\delta$ is a random deviate (e.g., from a Gaussian distribution).
3. Separately, generate a large sample of target stellar masses, $\lbrace M_{\star}^{\text{target}} \rbrace$, that perfectly follows the observed stellar [mass function](@entry_id:158970).
4. Rank-order the subhalos according to their scattered mass, $M_{\star}^{\text{scat}}$.
5. Assign the final [stellar mass](@entry_id:157648) to each subhalo by taking the value from the *ranked* target sample. That is, the subhalo with the $k$-th highest $M_{\star}^{\text{scat}}$ receives the $k$-th highest $M_{\star}^{\text{target}}$.

This "re-ranking" method elegantly enforces the target SMF by construction, while the scatter serves to perturb the rank-ordering, decoupling the final $M_{\star}$ from a strict one-to-one relation with $X$. The original one-point distribution of the halo proxy $X$ is preserved, as this property is only used to establish the initial ranking and is not modified [@problem_id:3492452].

### Advanced Implementations and Extensions

The principles outlined above form a complete SHAM framework. We conclude by discussing several advanced extensions that address further complexities of galaxy formation and the limitations of simulations.

#### Orphan Galaxies

N-body simulations have finite [mass resolution](@entry_id:197946). A satellite subhalo can be tidally stripped to the point where its bound mass falls below this [resolution limit](@entry_id:200378) and it is no longer identified by the halo finder. However, the dense, star-filled inner region of the galaxy it hosts is expected to survive for a longer period. These galaxies without a resolved host subhalo are termed **orphan galaxies**.

Neglecting orphans leads to an underprediction of the number of satellite galaxies, particularly in dense environments. Advanced SHAM models incorporate a treatment for orphans by continuing to track their positions after their subhalo is disrupted. A common approach is to extrapolate the orphan's orbit using a model for [dynamical friction](@entry_id:159616), and to remove it from the catalog after a prescribed merging timescale, $t_{\text{df}}$, has elapsed. Careful de-duplication logic is required to ensure that a galaxy is not counted as both a live subhalo and an orphan simultaneously [@problem_id:3492482].

#### Redshift Evolution

Galaxies and halos are not static; their populations evolve significantly with cosmic time. Generalizing SHAM to higher redshifts, $z>0$, requires an evolving framework. The observational input becomes the redshift-dependent stellar [mass function](@entry_id:158970), $\phi(M_{\star}, z)$, and the simulation input becomes the set of halo catalogs at multiple [redshift](@entry_id:159945) snapshots.

A physically consistent approach must account for the full formation history of the satellite population [@problem_id:3492413]. At any observation redshift $z$:
- **Centrals** are matched by applying abundance matching between the central galaxy SMF at $z$ and the host halo population at $z$.
- **Satellites** observed at $z$ are the survivors of all galaxies accreted at all previous times $z_{\text{acc}} > z$. To model this, one needs the distribution of accretion events, $f_{\text{sat,acc}}(X_{\text{acc}}, z_{\text{acc}})$, and a model for the [survival probability](@entry_id:137919) of a subhalo, $S(X_{\text{acc}}, z_{\text{acc}} \to z)$. The matching is then performed between the observed satellite SMF at $z$ and this dynamically constructed population of surviving subhalos, using the accretion-time property $X_{\text{acc}}$ as the proxy.

This evolutionary approach provides a far more complete and physically grounded picture of the galaxy-halo connection over cosmic history than simply repeating a static matching procedure at each redshift.

#### Dependence on Halo Definitions

Finally, it is important to recognize that the input halo number densities, $n(>X)$, depend on the algorithms and definitions used to identify halos in a simulation. The total number of subhalos, and their properties, changes depending on the **halo finder** used. Furthermore, even for a given finder, the definition of halo mass (and its corresponding radius) is not unique. Common definitions include $M_{200c}$, the mass enclosed within a radius where the mean density is 200 times the [critical density](@entry_id:162027) of the universe, or $M_{\text{vir}}$, where the overdensity threshold is derived from a [spherical collapse model](@entry_id:159843). These different definitions result in different masses and radii for the same object. Fortunately, for a given [density profile](@entry_id:194142) model like the NFW profile, it is straightforward to derive conversion formulae between these conventions [@problem_id:3492461]. Consistency in these definitions is paramount when comparing SHAM results to other models or to observational data. This also applies to the subhalo population itself; [tidal stripping](@entry_id:160026) and [dynamical friction](@entry_id:159616) preferentially destroy massive subhalos, causing the present-day subhalo [mass function](@entry_id:158970) to be steeper and have a lower normalization than the [mass function](@entry_id:158970) at the time of accretion [@problem_id:3492492]. Understanding the properties of the underlying dark matter population is a prerequisite for any successful application of SHAM.