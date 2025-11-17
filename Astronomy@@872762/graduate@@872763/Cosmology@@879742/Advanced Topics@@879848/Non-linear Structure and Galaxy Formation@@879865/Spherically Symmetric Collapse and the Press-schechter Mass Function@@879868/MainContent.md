## Introduction
One of the central questions in [modern cosmology](@entry_id:752086) is how the vast, intricate network of galaxies and galaxy clusters known as the cosmic web emerged from the remarkably smooth and homogeneous early universe. Answering this question requires a quantitative theoretical framework that can connect the tiny primordial [density fluctuations](@entry_id:143540) to the massive, gravitationally bound dark matter halos that host the galaxies we observe today. The problem is bridging the gap between the simple linear evolution of small perturbations and the complex, non-linear physics of gravitational collapse.

This article provides a comprehensive overview of the foundational analytical tools developed to solve this problem: the spherically symmetric collapse model and the Press-Schechter [mass function](@entry_id:158970). We will see how these models, despite their initial simplifying assumptions, offer profound insights into the formation and statistical distribution of cosmic structures. This framework serves not only as a cornerstone of our [standard cosmological model](@entry_id:159833) but also as a powerful laboratory for testing new physics.

The journey begins in **Principles and Mechanisms**, where we will deconstruct the idealized dynamics of a single collapsing "top-hat" overdensity and build up to the statistical machinery of the Press-Schechter formalism, rigorously derived through the excursion set method. Next, in **Applications and Interdisciplinary Connections**, we will explore the remarkable versatility of this framework, demonstrating how it is extended to build more realistic halo models and used as a precision tool to probe fundamental physics, from the nature of dark matter to the validity of General Relativity. Finally, the **Hands-On Practices** section will offer an opportunity to actively engage with these concepts, solving problems that challenge and solidify the theoretical understanding gained throughout the article.

## Principles and Mechanisms

Following our introduction to the cosmic web, this chapter delves into the fundamental theoretical framework used to understand and quantify the formation of cosmic structures: the spherically symmetric collapse model and its statistical extension, the Press-Schechter [mass function](@entry_id:158970). We will begin with the idealized dynamics of a single overdense region and build towards a statistical description of the entire halo population, exploring the physical mechanisms that govern their properties and the refinements necessary for a more complete picture.

### The Spherical "Top-Hat" Collapse Model

The cornerstone of our analytical understanding of structure formation is the **[spherical collapse model](@entry_id:159843)**, often referred to as the "top-hat" model. This idealized scenario considers the evolution of a perfectly spherical region of uniform overdensity embedded in an otherwise homogeneous and isotropic [expanding universe](@entry_id:161442). Despite its simplicity, this model provides profound insights into the non-linear process of [gravitational collapse](@entry_id:161275).

#### Equation of Motion and Analogy to a Closed Universe

Let us consider a spherical region of radius $R(t)$ with a uniform density $\rho_p(t)$ that is slightly greater than the background cosmic density $\bar{\rho}(t)$. Birkhoff's theorem allows us to analyze the dynamics of this sphere by ignoring the universe outside it; its evolution is governed solely by the mass $M$ it contains. The [equation of motion](@entry_id:264286) for a test particle on the shell of this sphere is identical in form to the Friedmann equation:

$$
\left(\frac{\dot{R}}{R}\right)^2 = \frac{8\pi G \rho_p}{3} - \frac{k c^2}{R^2}
$$

Here, $\dot{R}$ is the time derivative of the radius, $G$ is the [gravitational constant](@entry_id:262704), $c$ is the speed of light, and $k$ is a constant related to the total energy of the shell. Since the perturbation is overdense, it is gravitationally more bound than the background. For a flat background universe (like the Einstein-de Sitter model, where $\Omega_m=1$), the overdense region behaves like a miniature closed universe with [positive curvature](@entry_id:269220) ($k > 0$). The mass inside the sphere, $M = \frac{4\pi}{3}\rho_p R^3$, is conserved during the evolution. We can rewrite the [equation of motion](@entry_id:264286) in terms of total energy $E$:

$$
\frac{1}{2}\dot{R}^2 - \frac{GM}{R} = E
$$

For a bound, collapsing perturbation, the total energy $E$ is negative.

#### Evolution: Turnaround and Collapse

Initially, the overdense region expands along with the background Hubble flow, but its excess gravity causes the expansion to decelerate more rapidly. Eventually, the expansion halts at a maximum radius, known as the **turnaround radius** ($R_{ta}$), at a time $t_{ta}$. At this point, the kinetic energy of the shell is zero ($\dot{R}=0$), and the total energy is purely potential. After turnaround, the sphere begins to collapse under its own gravity.

In an Einstein-de Sitter (EdS) background ($\Omega_m=1$, $\Omega_\Lambda=0$), the evolution of the sphere's radius can be described by the same parametric solution as for a closed FLRW universe:

$$
R(\theta) = A(1 - \cos\theta)
$$
$$
t(\theta) = B(\theta - \sin\theta)
$$

Here, $\theta$ is a development angle, and $A$ and $B$ are constants determined by the mass $M$. The expansion begins at $\theta=0$. Turnaround occurs when $\dot{R}=0$, which corresponds to $\theta=\pi$. The final collapse to a point singularity ($R=0$) occurs at $\theta=2\pi$. From these relations, we find that the collapse time is twice the [turnaround time](@entry_id:756237): $t_c = 2t_{ta}$.

The background cosmology in which the collapse occurs is crucial. While we often default to an EdS model for simplicity, the universe could be open ($\Omega_{m,0}  1$, $\Omega_\Lambda=0$). In such a case, the background [scale factor](@entry_id:157673) $a(t)$ follows a different parametric solution, for example $a(\psi) = A(\cosh\psi - 1)$ and $t(\psi) = B(\sinh\psi - \psi)$, where the constants $A$ and $B$ depend on the present-day [matter density](@entry_id:263043) $\Omega_{m,0}$ and Hubble constant $H_0$. The value of $\Omega_{m,0}$ can be determined if the evolutionary stage of the universe, characterized by the parameter $\psi_0$, is known [@problem_id:849794].

#### Derivation of the Critical Linear Overdensity, $\delta_c$

The most important result of the [spherical collapse model](@entry_id:159843) is the calculation of the **critical linear overdensity**, denoted $\delta_c$. This is the value that the initial, small overdensity would need to have, according to [linear perturbation theory](@entry_id:159071), in order to collapse at a specific time.

The procedure is as follows:
1.  Calculate the full non-linear evolution of the top-hat sphere to find its [density contrast](@entry_id:157948) at the moment of collapse. At turnaround ($\theta=\pi$), the radius is $R_{ta} = 2A$ and the time is $t_{ta} = \pi B$. The density inside the sphere is $\rho_p(t_{ta}) = M / (\frac{4\pi}{3} R_{ta}^3)$. Comparing this to the background density in an EdS universe, $\bar{\rho}(t) = 1/(6\pi G t^2)$, one finds the [density contrast](@entry_id:157948) at turnaround is $\rho_p/\bar{\rho} = (3\pi/4)^2 \approx 5.55$. In the limit of complete collapse ($t \to t_c = 2t_{ta}$), the non-linear [density contrast](@entry_id:157948) diverges, $\Delta = \rho_p/\bar{\rho} - 1 \to \infty$.

2.  Consider the evolution of the same perturbation using linear theory, where the [density contrast](@entry_id:157948) $\delta_L$ grows with the scale factor. In an EdS universe, $\delta_L \propto a(t) \propto t^{2/3}$.

3.  The critical overdensity $\delta_c$ is found by evaluating the linear theory prediction at the time of non-linear collapse, $t_c$. By relating the constants in the linear and non-linear solutions, one finds:

$$
\delta_c = \frac{3}{5} \left( \frac{3\pi}{2} \right)^{2/3} \approx 1.686
$$

This value is remarkably independent of the mass of the halo and the specific time of collapse, making it a universal threshold in an EdS universe. For other cosmologies, $\delta_c$ has a weak dependence on [redshift](@entry_id:159945). This threshold, $\delta_c$, is the key ingredient that connects the dynamics of collapse to the statistical description of structure formation.

#### Relativistic Corrections from the Tolman-Bondi-Lemaître Model

The Newtonian treatment of [spherical collapse](@entry_id:161208) assumes that the proper time of observers within the collapsing region is identical to the cosmic time of the background universe. A fully relativistic analysis using the **Tolman-Bondi-Lemaître (TBL) metric** for a spherically symmetric dust cloud reveals that this is an approximation. Due to [gravitational time dilation](@entry_id:162143), clocks run slower inside the overdense region compared to the distant background.

This means that the collapse time measured by a distant observer, $\tau_c$, is longer than the proper time for collapse measured by an observer comoving with the shell, $t_c$. The relation can be shown to be $\tau_c = t_c(1 - 2E/c^2)$, where $E  0$ is the [specific energy](@entry_id:271007) of the collapsing shell. Since [linear growth](@entry_id:157553) theory is formulated in terms of the background cosmic time $\tau$, the linear overdensity must be extrapolated to $\tau_c$, not $t_c$. As [linear growth](@entry_id:157553) in an EdS universe proceeds as $\delta_L \propto \tau^{2/3}$, the corrected critical overdensity $\delta_c$ is related to the Newtonian value $\delta_{c,N}$ by [@problem_id:849800]:

$$
\frac{\delta_c}{\delta_{c,N}} = \left(\frac{\tau_c}{t_c}\right)^{2/3} = \left(1 - \frac{2E}{c^2}\right)^{2/3}
$$

Since $E$ is negative, this relativistic effect slightly increases the [critical density](@entry_id:162027) threshold. For typical halo formation scenarios, this correction is very small but represents an important physical refinement to the model.

### Virialization and the Final State of Collapsed Halos

In the idealized model, the spherical shell collapses to a singularity. In reality, the collapse is halted, and a stable, gravitationally bound object, known as a **[dark matter halo](@entry_id:157684)**, is formed. This process, called **[virialization](@entry_id:161222)**, occurs through **[violent relaxation](@entry_id:158546)**, where the chaotic, time-varying gravitational potential redistributes energy among the dark matter particles, leading to a state of statistical equilibrium.

#### The Virial Theorem and the Virial Radius

The final [equilibrium state](@entry_id:270364) of the halo is described by the **virial theorem**. For a simple, isolated system bound by gravity, the theorem states that the time-averaged total kinetic energy $\langle K \rangle$ and [total potential energy](@entry_id:185512) $\langle W \rangle$ are related by $2\langle K \rangle + \langle W \rangle = 0$.

Applying this to the collapsed halo, we can relate the energy at turnaround to the energy at [virialization](@entry_id:161222). At turnaround, the energy is entirely potential: $E_{tot} = W_{ta} = -\frac{3}{5}\frac{GM^2}{R_{ta}}$. At [virialization](@entry_id:161222), the energy is $E_{tot} = K_{vir} + W_{vir}$. Using the virial theorem, $K_{vir} = -W_{vir}/2$, the total energy becomes $E_{tot} = W_{vir}/2$. Equating the energies and assuming conservation gives $W_{vir}/2 = W_{ta}$. Since $W \propto -1/R$, this implies:

$$
-\frac{1}{2} \frac{3}{5}\frac{GM^2}{R_{vir}} = -\frac{3}{5}\frac{GM^2}{R_{ta}} \quad \implies \quad R_{vir} = \frac{1}{2} R_{ta}
$$

The halo virializes at half its turnaround radius. By comparing the density of the virialized halo to the background density at the time of collapse, one finds a characteristic overdensity for virialized objects in an EdS universe of $\Delta_{vir} = \rho_{vir}/\bar{\rho} - 1 \approx 18\pi^2 - 1 \approx 177$.

#### Generalizations to the Virial Theorem: The Role of Dark Energy

In a universe with a [cosmological constant](@entry_id:159297), $\Lambda$, or a more general [dark energy](@entry_id:161123) component, the [virial theorem](@entry_id:146441) must be modified. Dark energy exerts a repulsive force, which affects both the global expansion and the local dynamics of collapsing structures.

First, [dark energy](@entry_id:161123) contributes a potential energy term, $W_\Lambda$, to the halo. For a [cosmological constant](@entry_id:159297), this term is $W_\Lambda = -\frac{1}{10} M \Lambda c^2 R^2$. The generalized virial theorem becomes $2K + W_G - 2W_\Lambda = 0$. This changes the relationship between turnaround and virial radii [@problem_id:849809].

Second, a dark energy fluid with an equation of state $P_{DE} = w \rho_{DE} c^2$ exerts an external pressure on the boundary of the halo. The scalar [virial theorem](@entry_id:146441) must be augmented with a surface term, $S = -\oint P_{\rm ext} \mathbf{r} \cdot d\mathbf{S}$. For a spherical halo of radius $R$ immersed in a uniform dark energy background, this term becomes [@problem_id:849835]:

$$
S = -4\pi w \rho_{DE} c^2 R^3
$$

The full virial equilibrium condition is then $2K + W_G + S = 0$. For a cosmological constant, $w=-1$, this surface term adds positive energy, counteracting gravity and making it harder for halos to remain bound.

#### The Role of Angular Momentum in Halting Collapse

In reality, collapsing proto-halos are not perfectly spherical and exist in a crowded environment. Tidal torques from neighboring perturbations impart angular momentum to the collapsing object. While [violent relaxation](@entry_id:158546) is the primary mechanism for virializing the bulk of the halo, this acquired angular momentum can be dominant in the central regions, halting collapse and leading to the formation of rotationally supported structures, such as galactic disks.

The amount of angular momentum is often quantified by the dimensionless **spin parameter**, $\lambda$:

$$
\lambda = \frac{L |E|^{1/2}}{G M^{5/2}}
$$

where $L$ is the total angular momentum and $E$ is the total energy of the halo. For a hypothetical collapse halted entirely by centrifugal forces, a direct relationship exists between the final radius of the object, the initial conditions of the collapse (like mass $M$ and [turnaround time](@entry_id:756237) $t_{ta}$), and the spin parameter $\lambda$. For instance, if the collapse results in a thin, rotationally supported ring of mass $M$, its final radius $R_f$ is proportional to $\lambda^2$ and $(G M t_{ta}^2)^{1/3}$ [@problem_id:849824]. This illustrates how an additional physical parameter, $\lambda$, arising from realistic environmental effects, can determine the final configuration of cosmic structures.

### The Press-Schechter Mass Function: From Collapse to Statistics

The [spherical collapse model](@entry_id:159843) provides a clear criterion for the formation of a bound object: a region collapses if its linearly extrapolated [density contrast](@entry_id:157948) exceeds $\delta_c$. The **Press-Schechter (PS) formalism** leverages this insight to predict the abundance of collapsed halos of different masses, known as the **[halo mass function](@entry_id:158011)**, $n(M)$.

#### The Fundamental Premise: Counting Halos in a Gaussian Field

The central idea is to treat the initial cosmological density field as a Gaussian random field. The formation of a halo of mass $M$ is then linked to the probability that the density field, when smoothed on the corresponding scale $R$, exceeds the critical threshold $\delta_c$.

The key statistical quantity is the variance of the smoothed density field, $\sigma^2(M)$:

$$
\sigma^2(M) = \int_0^\infty \frac{k^2 dk}{2\pi^2} P(k) |W(kR)|^2
$$

Here, $P(k)$ is the [matter power spectrum](@entry_id:161407), which encodes the statistical properties of the density fluctuations. $W(kR)$ is the Fourier transform of a real-space filter function, typically a spherical top-hat of radius $R$ related to the mass $M$ by $M = \frac{4\pi}{3}\bar{\rho}R^3$. The variance $\sigma(M)$ is a decreasing function of mass: smaller masses correspond to larger variance (more power on small scales).

#### The Initial Press-Schechter Ansatz

The original argument proposed by Press and Schechter (1974) was that the fraction of the universe's mass contained within halos of mass *greater than* $M$ is equal to the probability that the smoothed density field $\delta_M$ is greater than $\delta_c$. For a Gaussian field with [zero mean](@entry_id:271600) and variance $\sigma^2(M)$, this probability is:

$$
F(M) = P(\delta_M  \delta_c) = \int_{\delta_c}^\infty \frac{1}{\sqrt{2\pi}\sigma(M)} \exp\left(-\frac{\delta^2}{2\sigma^2(M)}\right) d\delta
$$

By differentiating this cumulative fraction with respect to mass, one can obtain the [mass function](@entry_id:158970) $n(M)$. However, this simple [ansatz](@entry_id:184384) suffers from a normalization problem: as $M \to 0$ ($\sigma \to \infty$), the integral approaches $1/2$, implying that only half the mass of the universe ends up in collapsed objects. This is the famous "cloud-in-cloud" problem: it fails to account for mass elements in underdense regions that are part of larger-scale overdensities that eventually collapse. Press and Schechter resolved this by fiat, multiplying their final result by a factor of 2.

### The Excursion Set Formalism: A Rigorous Derivation

The "factor of two" problem pointed to a need for a more robust theoretical foundation, which was provided by the **[excursion set formalism](@entry_id:161517)**. This powerful framework recasts the problem of halo formation as a [first-passage time](@entry_id:268196) problem in statistical mechanics.

#### Random Walks and Structure Formation

The [excursion set formalism](@entry_id:161517) considers the value of the smoothed [density contrast](@entry_id:157948), $\delta$, as one varies the smoothing scale. Specifically, it tracks the trajectory of $\delta(S)$ where the "time" variable is not physical time, but the variance $S = \sigma^2(M)$. As we decrease the mass scale $M$, $S$ increases, and the value of $\delta(S)$ for a given point in space executes a random walk (more precisely, Brownian motion). The walk starts at $(\delta, S) = (0, 0)$, corresponding to a homogeneous universe on infinitely large scales ($M\to\infty, S\to 0$).

#### The Absorbing Barrier and the First-Crossing Problem

In this picture, the [spherical collapse](@entry_id:161208) criterion, $\delta = \delta_c$, becomes an absorbing barrier for the [random walks](@entry_id:159635). The central question of the [excursion set formalism](@entry_id:161517) is: what is the distribution of "times" $S$ at which a random walk *first* crosses the barrier $\delta_c$? This first-crossing at variance $S(M)$ corresponds to the mass element being incorporated into a halo of mass $M$ for the first time.

The evolution of the probability distribution of walkers, $P(\delta, S)$, is governed by a diffusion equation. To solve for the first-crossing distribution, we must solve this equation with the initial condition $P(\delta, S=0) = \delta_D(\delta)$ (a Dirac delta function, as all walks start at $\delta=0$) and an [absorbing boundary condition](@entry_id:168604) $P(\delta_c, S) = 0$ for all $S0$. This can be elegantly solved using the **[method of images](@entry_id:136235)** [@problem_id:849785]. One considers the solution for a free walk (a Gaussian) and adds a negative "image" source at $\delta = 2\delta_c$ that cancels the probability at the barrier. The first-crossing distribution, $f(S)$, is then the flux of probability across the barrier at $\delta_c$. The result of this calculation is:

$$
f(S) dS = \frac{\delta_c}{\sqrt{2\pi} S^{3/2}} \exp\left(-\frac{\delta_c^2}{2S}\right) dS
$$

This distribution, derived rigorously, is precisely the result obtained by the original Press-Schechter ansatz *including* the ad-hoc factor of 2. It gives the fraction of mass elements that are part of halos with mass corresponding to the variance range $[S, S+dS]$.

#### Predictions of the Mass Function: The Low-Mass Slope

The final Press-Schechter [mass function](@entry_id:158970), giving the comoving [number density](@entry_id:268986) of halos per unit mass, is:
$$
n(M) = \sqrt{\frac{2}{\pi}} \frac{\bar{\rho}}{M^2} \frac{\delta_c}{\sigma(M)} \left| \frac{d \ln \sigma(M)}{d \ln M} \right| \exp\left(-\frac{\delta_c^2}{2\sigma^2(M)}\right)
$$
This function's shape is determined by the cosmological [power spectrum](@entry_id:159996) $P(k)$, which sets $\sigma(M)$. For a power-law power spectrum, $P(k) \propto k^n$, the variance scales as $\sigma^2(M) \propto M^{-(n+3)/3}$. The behavior of the [mass function](@entry_id:158970) at low masses ($M \to 0$, where $\sigma \to \infty$ and the exponential term approaches 1) is a power law, $n(M) \propto M^\alpha$. The slope $\alpha$ is directly related to the [spectral index](@entry_id:159172) $n$. A detailed calculation shows that $\alpha = -2 + (n+3)/6$. Thus, a low-mass slope of $\alpha = -2$ implies a [spectral index](@entry_id:159172) of $n=-3$ [@problem_id:849848], demonstrating the tight link between the observed abundance of small halos and the properties of primordial [density fluctuations](@entry_id:143540).

### Refinements and Extensions of the Model

While remarkably successful, the Press-Schechter formalism based on [spherical collapse](@entry_id:161208) is an idealization. Modern cosmology employs several crucial extensions to achieve greater accuracy and physical realism.

#### Beyond Spherical Symmetry: Ellipsoidal Collapse

Real [cosmic perturbations](@entry_id:158699) are not spherical. The initial shear of the gravitational potential field influences the dynamics of collapse. The **[ellipsoidal collapse](@entry_id:159908) model** accounts for this by considering the evolution of the three principal axes of an initially ellipsoidal perturbation. This leads to a collapse threshold that is not a universal constant but depends on the shape of the initial perturbation. A simple model modifies the [critical density](@entry_id:162027) to $\delta_{ec} = \delta_c (1 + C \sigma_s^2 / \delta^2)$, where $\sigma_s^2$ quantifies the magnitude of the trace-free shear and $C$ is a constant. For a highly flattened, "pancake-like" initial perturbation, this leads to a specific, calculable correction to the exponential cutoff of the [mass function](@entry_id:158970), suppressing the abundance of halos compared to the spherical prediction [@problem_id:849846].

#### Probing the Nature of Dark Matter: Warm Dark Matter Constraints

The [halo mass function](@entry_id:158011) is a powerful probe of the nature of dark matter itself. While Cold Dark Matter (CDM) has no intrinsic velocity dispersion, Warm Dark Matter (WDM) particles possess thermal velocities that allow them to free-stream out of small [density perturbations](@entry_id:159546). This erases power on small scales, typically below a [free-streaming](@entry_id:159506) scale $k_{fs}$. This effect can be modeled by multiplying the CDM power spectrum by a transfer function $T(k)$ that acts as a sharp cutoff at $k_{fs}$.

This lack of small-scale power directly translates into a suppression of the [halo mass function](@entry_id:158011) at low masses. Compared to CDM, the WDM mass variance $\sigma_{WDM}(M)$ flattens and approaches a constant for $M \to 0$. This dramatically changes the low-mass behavior of $n(M)$. The ratio of the WDM to CDM mass functions, $S(M) = n_{WDM}(M)/n_{CDM}(M)$, provides a clear signature. In the low-mass limit, this suppression factor scales as a power law, $S(M) \propto M^\alpha$, where the index $\alpha = (1-n)/6$ depends on the primordial [spectral index](@entry_id:159172) $n$ [@problem_id:849810]. Searching for this cutoff in the observed halo or galaxy abundance provides some of the tightest constraints on the mass of WDM particles.

#### Halo Bias and the Peak-Background Split

Dark matter halos are not distributed randomly in space; they are biased tracers of the underlying matter distribution, preferentially forming in high-density regions. The **[peak-background split](@entry_id:753301)** model provides a framework for calculating this **[halo bias](@entry_id:161548)**, $b(M)$. The model separates the density field into a long-wavelength background mode, $\delta_b$, and short-wavelength fluctuations that form halos. The presence of a positive background overdensity $\delta_b$ effectively lowers the collapse threshold for small-scale peaks to $\delta_c - \delta_b$. This increases the number of halos that form, meaning halo density is enhanced in overdense regions. This leads to a linear bias relation $\delta_h = b \delta_m$, where $\delta_h$ is the halo overdensity and $\delta_m$ is the matter overdensity. For a Gaussian field, the bias is found to be:

$$
b(M,z) = 1 + \frac{\nu^2 - 1}{\delta_c}
$$
where $\nu(M,z) = \delta_c(z)/\sigma(M,z)$ is the peak height. This correctly predicts that massive halos (high $\nu$) are more strongly biased than low-mass halos.

This formalism is powerful enough to probe beyond the [standard cosmological model](@entry_id:159833). For instance, if the primordial density field has some level of local non-Gaussianity, parameterized by $f_{NL}$, it induces a characteristic scale-dependence in the [halo bias](@entry_id:161548). A long-wavelength potential mode modulates the small-scale variance, which in turn modulates the abundance of halos. This effect introduces a correction to the [halo bias](@entry_id:161548) that is proportional to $f_{NL}$ and scales as $1/k^2$ on large scales [@problem_id:849793]. Measuring this [scale-dependent bias](@entry_id:158208) in galaxy surveys is one of the most promising methods for constraining the physics of inflation.