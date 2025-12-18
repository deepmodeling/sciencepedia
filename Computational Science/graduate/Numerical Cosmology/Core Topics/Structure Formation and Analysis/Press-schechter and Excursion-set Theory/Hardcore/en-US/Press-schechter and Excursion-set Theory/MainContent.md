## Introduction
The hierarchical formation of cosmic structure, where small, dense objects form first and subsequently merge to build up larger systems like galaxies and clusters, is a cornerstone of modern cosmology. A central challenge is to develop a theoretical framework that connects the statistical properties of the universe's initial [density fluctuations](@entry_id:143540) to the final, observable population of these collapsed objects, known as [dark matter halos](@entry_id:147523). While large-scale N-body simulations provide a precise numerical solution, analytical models offer crucial physical insight and [computational efficiency](@entry_id:270255). The Press-Schechter formalism, and its more rigorous extension, the [excursion-set theory](@entry_id:749161), stands as the most successful and influential of these models. It elegantly reframes the complex, [non-linear dynamics](@entry_id:190195) of [gravitational collapse](@entry_id:161275) into a solvable problem in the statistics of [random walks](@entry_id:159635).

This article provides a comprehensive exploration of the excursion-set framework, designed for graduate-level students in cosmology. It bridges the gap between a qualitative understanding of hierarchical formation and the quantitative tools needed for modern research. By working through this material, you will gain a deep understanding of how to predict the properties of the halo population from first principles.

The journey is structured across three distinct chapters. First, in **Principles and Mechanisms**, we will build the theory from the ground up. You will learn how the smoothed density field can be viewed as a random walk, how the concept of a collapse barrier leads to the [halo mass function](@entry_id:158011), and how the [peak-background split](@entry_id:753301) argument yields predictions for [halo bias](@entry_id:161548). Next, **Applications and Interdisciplinary Connections** will demonstrate the theory's remarkable versatility. We will explore how it predicts the clustering environment of halos, their merger histories and substructure, and how it can be used as a powerful probe of fundamental physics, such as the nature of dark matter and the epoch of [cosmic reionization](@entry_id:747915). Finally, **Hands-On Practices** will provide a series of guided problems that allow you to implement and explore these concepts yourself, cementing your theoretical knowledge through practical application.

## Principles and Mechanisms

The [excursion-set theory](@entry_id:749161) provides a powerful theoretical framework for understanding the hierarchical formation of cosmic structures. It translates the [complex dynamics](@entry_id:171192) of gravitational collapse into a statistical problem involving [random walks](@entry_id:159635), allowing for the prediction of key properties of the halo population, such as their abundance and clustering. This chapter elucidates the fundamental principles and mechanisms of this theory, from its foundational assumptions to its most significant applications and extensions.

### The Excursion Set Analogy: From Density Fields to Random Walks

The starting point for modeling [structure formation](@entry_id:158241) is the initial matter density field, which in the [standard cosmological model](@entry_id:159833) is described as a **Gaussian random field**. This field is characterized by its mean, which is zero by definition for the [density contrast](@entry_id:157948) $\delta(\mathbf{x}) \equiv (\rho(\mathbf{x}) - \bar{\rho})/\bar{\rho}$, and its [two-point correlation function](@entry_id:185074), or equivalently, its **[power spectrum](@entry_id:159996)** $P(k)$ in Fourier space.

The core idea of the [excursion-set formalism](@entry_id:749160) is to analyze the behavior of this density field as it is smoothed on different spatial scales. We define a smoothed [density contrast](@entry_id:157948) field, $\delta_R(\mathbf{x})$, by convolving the raw field $\delta(\mathbf{x})$ with a [window function](@entry_id:158702) (or filter) $W(\mathbf{y}; R)$ of characteristic scale $R$:
$$
\delta_R(\mathbf{x}) = \int \delta(\mathbf{x} - \mathbf{y}) W(\mathbf{y}; R) d^3\mathbf{y}
$$
For any given point in space, say $\mathbf{x}=\mathbf{0}$, the value of the smoothed [density contrast](@entry_id:157948) $\delta_R(\mathbf{0})$ changes as we vary the smoothing scale $R$. If we start from a very large scale ($R \to \infty$), the filter averages over a vast volume, so $\delta_R \to 0$. As we decrease $R$, we include smaller-scale fluctuations, causing the value of $\delta_R$ to fluctuate. This sequence of values, $\delta_R$ as a function of decreasing $R$, traces out a **trajectory** or a **random walk**.

Instead of using the smoothing radius $R$ as the [independent variable](@entry_id:146806) for this walk, it is more convenient to use the variance of the smoothed field, defined as:
$$
S(R) \equiv \sigma^2(R) = \langle \delta_R^2 \rangle = \int \frac{k^2 dk}{2\pi^2} P(k) |\tilde{W}(kR)|^2
$$
where $\tilde{W}(kR)$ is the Fourier transform of the window function. As the smoothing scale $R$ decreases from infinity to zero, the variance $S$ increases monotonically from zero to some maximum value. Thus, we can re-parameterize the trajectory as $\delta(S)$.

The statistical properties of these random walks depend critically on the choice of [window function](@entry_id:158702). A particularly convenient choice is the **sharp-$k$ filter**, which is a [step function](@entry_id:158924) in Fourier space: $\tilde{W}(kR) = \Theta(1-kR)$, where $\Theta$ is the Heaviside function. This filter has the unique property that the steps in the random walk, $\delta(S_2) - \delta(S_1)$ and $\delta(S_3) - \delta(S_2)$ for $S_1  S_2  S_3$, are statistically independent. Such a walk is termed **Markovian**, and its mathematical description simplifies considerably.

### The First-Crossing Distribution: The Press-Schechter Mass Function

Within this framework, the formation of a gravitationally bound object (a dark matter halo) is postulated to occur when the smoothed overdensity at some location first crosses a critical threshold, $\delta_c$. This threshold is typically motivated by the [spherical collapse model](@entry_id:159843), which shows that a spherical top-hat perturbation collapses when its linearly extrapolated [density contrast](@entry_id:157948) reaches a value of $\delta_c \approx 1.686$, nearly independent of mass and redshift in an Einstein-de Sitter universe.

The problem of calculating the abundance of halos of a given mass $M$ (which corresponds to a smoothing scale $R$ and variance $S$) now becomes equivalent to a classic problem in [stochastic processes](@entry_id:141566): finding the **[first-passage time](@entry_id:268196)** distribution of random walks crossing an absorbing barrier at $\delta_c$.

Let us derive this distribution for the case of a sharp-$k$ filter, where the walk $\delta(S)$ is a Markovian process with zero-mean Gaussian increments . We can describe the evolution of the probability density of trajectories, $F(\delta, S) d\delta$, that have a value between $\delta$ and $\delta+d\delta$ at variance scale $S$ without having previously crossed the barrier. This evolution is governed by the **Fokker-Planck equation**, which for a driftless process with diffusion coefficient $D=1/2$ is:
$$
\frac{\partial F(\delta, S)}{\partial S} = \frac{1}{2}\frac{\partial^2 F(\delta, S)}{\partial \delta^2}
$$
This [diffusion equation](@entry_id:145865) must be solved subject to two conditions. The initial condition is that all walks start at $\delta=0$ for $S=0$ (infinite smoothing scale), which we can write as $F(\delta, S=0) = \delta_{\mathrm{D}}(\delta)$, where $\delta_{\mathrm{D}}$ is the Dirac delta function. The boundary condition is that the barrier at $\delta_c$ is **absorbing**: any trajectory that reaches it is considered part of a collapsed halo and is removed from the ensemble. This implies $F(\delta_c, S) = 0$ for all $S>0$.

This problem is elegantly solved using the **method of images**. The solution can be constructed by superposing the solution for a free diffusion process (a Gaussian of variance $S$) with that of a negative "image" source placed at $\delta = 2\delta_c$. The resulting probability distribution for trajectories that have not yet crossed the barrier ($\delta  \delta_c$) is:
$$
F(\delta, S) = \frac{1}{\sqrt{2\pi S}} \left[ \exp\left(-\frac{\delta^2}{2S}\right) - \exp\left(-\frac{(\delta - 2\delta_c)^2}{2S}\right) \right]
$$
The quantity we seek is the rate at which trajectories are absorbed at the barrier, which gives the fraction of mass elements that are part of halos first collapsing at scale $S$. This is given by the probability flux into the barrier, $J = -\frac{1}{2} \frac{\partial F}{\partial \delta} \big|_{\delta=\delta_c}$. The first-crossing rate per unit of variance is then:
$$
\frac{d\mathcal{F}}{dS} = -\frac{1}{2} \frac{\partial F}{\partial \delta} \bigg|_{\delta=\delta_c} = \frac{\delta_c}{\sqrt{2\pi S^3}}\exp\left(-\frac{\delta_c^2}{2S}\right)
$$
This gives the fraction of mass collapsing into halos per unit interval in $S$. It is conventional to re-express this in terms of the **multiplicity function**, $f(\nu)$, and the dimensionless **peak height**, $\nu \equiv \delta_c / \sqrt{S} = \delta_c/\sigma$. The [multiplicity](@entry_id:136466) function is defined such that $f(\nu) |d\ln\nu|$ is the fraction of mass in halos within the corresponding logarithmic interval of peak height. Using the relationship $|d\ln\nu| = \frac{1}{2S} dS$, we find the connection $f(\nu) = 2S \frac{d\mathcal{F}}{dS}$. Substituting our expression for the first-crossing rate yields:
$$
f(\nu) = 2S \left( \frac{\delta_c}{\sqrt{2\pi S^3}}\exp\left(-\frac{\delta_c^2}{2S}\right) \right) = \frac{2\delta_c}{\sqrt{2\pi S}} \exp\left(-\frac{\delta_c^2}{2S}\right)
$$
Finally, expressing this purely in terms of $\nu = \delta_c/\sqrt{S}$, we arrive at the celebrated result originally found by Press and Schechter:
$$
f(\nu) = \sqrt{\frac{2}{\pi}} \nu \exp\left(-\frac{\nu^2}{2}\right)
$$
This function gives the fraction of mass per unit logarithmic interval in $\nu$ that is contained in collapsed halos, and it forms the theoretical bedrock for predicting halo abundances .

### From Theory to Observation: The Halo Mass Function and Halo Bias

The multiplicity function is a powerful theoretical construct, but to confront the theory with observations, we must relate it to observable quantities like the number density and clustering of [dark matter halos](@entry_id:147523).

#### The Halo Mass Function

The primary observable predicted by the theory is the **[halo mass function](@entry_id:158011)**, $n(M,z)$, defined such that $n(M,z) dM$ is the comoving [number density](@entry_id:268986) of halos in the mass interval $[M, M+dM]$ at redshift $z$. We can derive the relationship between $n(M,z)$ and $f(\nu)$ from the fundamental principle of mass conservation .

The fraction of the total comoving mass density, $\bar{\rho}_{\mathrm{m}}$, that is contained in halos within the mass range $[M, M+dM]$ is given by the mass of these halos, $M \cdot n(M,z)dM$, divided by the total mean density, $\bar{\rho}_{\mathrm{m}}$. By definition, this must be equal to the [mass fraction](@entry_id:161575) given by the multiplicity function over the corresponding interval in peak height, $f(\nu) |d\ln\nu|$. Therefore, we can write the identity:
$$
\frac{M \, n(M,z) \, dM}{\bar{\rho}_{\mathrm{m}}} = f(\nu) |d\ln\nu|
$$
Rearranging this equation gives the direct link between the theoretical multiplicity and the observable [mass function](@entry_id:158970):
$$
n(M,z) = \frac{\bar{\rho}_{\mathrm{m}}}{M} f(\nu) \left|\frac{d\ln\nu}{dM}\right|
$$
Here, $\bar{\rho}_{\mathrm{m}} = \Omega_{\mathrm{m},0} \rho_{\mathrm{crit},0}$ is the mean comoving matter density of the universe, which is constant with redshift. The peak height $\nu$ depends on both mass and redshift through the relation $\nu(M,z) = \delta_c(z)/\sigma(M,z)$, where $\sigma(M,z)$ is the root-mean-square of the [linear density](@entry_id:158735) field smoothed on a mass scale $M$ and evolved linearly to [redshift](@entry_id:159945) $z$. This equation allows us to take a theoretical prediction for $f(\nu)$ and convert it into a concrete prediction for the number of halos of a given mass we expect to find at any [redshift](@entry_id:159945).

#### The Clustering of Halos: Peak-Background Split and Halo Bias

Halos are not randomly distributed throughout the universe; their positions are correlated with the underlying large-scale matter distribution. The excursion-set framework, when combined with the **[peak-background split](@entry_id:753301) (PBS)** argument, provides a remarkably elegant way to predict the strength of this correlation, known as **[halo bias](@entry_id:161548)** .

The PBS idea treats a large-scale density fluctuation $\delta_{\ell}$ as a local change to the background density of the universe. For a small region embedded within this large-scale mode, the condition for collapse is not that its own density must reach $\delta_c$ relative to the cosmic mean, but rather that it must reach $\delta_c$ relative to the local background. This means the effective collapse threshold for small-scale perturbations within the large-scale patch is shifted to $B' = \delta_c - \delta_{\ell}$.

The [halo bias](@entry_id:161548) measures how the abundance of halos responds to this change in the local background density. The linear **Lagrangian bias**, $b_L$, is defined as the fractional change in the Lagrangian [number density](@entry_id:268986) of halos, $n_L$, in response to $\delta_{\ell}$:
$$
b_L(M) = \frac{1}{n_L} \frac{\partial n_L(\delta_{\ell})}{\partial \delta_{\ell}} \bigg|_{\delta_{\ell}=0}
$$
Assuming the halo abundance is proportional to the first-crossing distribution $f(S; B)$, this derivative can be evaluated using the [chain rule](@entry_id:147422). For a barrier $B$, the bias becomes $b_L = - \frac{\partial \ln f(S; B)}{\partial B}$. For the Press-Schechter first-crossing distribution derived earlier, $f(S; B) \propto B S^{-3/2} \exp(-B^2/2S)$, we have $\ln f = \ln B - B^2/2S + \text{const}$. The derivative is $\frac{\partial \ln f}{\partial B} = \frac{1}{B} - \frac{B}{S}$. Therefore, the Lagrangian bias is:
$$
b_L(M) = - \left(\frac{1}{\delta_c} - \frac{\delta_c}{S}\right) = \frac{\delta_c}{S} - \frac{1}{\delta_c} = \frac{\nu^2 - 1}{\delta_c}
$$
This is the bias in Lagrangian coordinates, which track initial positions. Observers measure halo properties in **Eulerian coordinates** (physical positions at a given time). Due to the [bulk flow](@entry_id:149773) of matter from underdense to overdense regions, the relationship between halo overdensity and matter overdensity changes. This leads to a simple relation between the linear Eulerian bias $b_E$ and the Lagrangian bias: $b_E = b_L + 1$. Thus, the predicted Eulerian bias for halos is:
$$
b_E(M) = \frac{\nu^2 - 1}{\delta_c} + 1 = \frac{\nu^2 - 1 + \delta_c}{\delta_c}
$$
This seminal result predicts that massive halos (large $\nu$) are more strongly clustered (more biased) than the underlying matter distribution ($b_E > 1$), while low-mass halos (small $\nu$) are less clustered ($b_E  1$).

### Advanced Topics and Extensions

The simple model outlined above relies on several key assumptions: a Markovian random walk, a single absorbing barrier, and Gaussian [initial conditions](@entry_id:152863). Relaxing these assumptions leads to a richer and more realistic picture.

#### The Role of the Filter: Correlated Random Walks

The assumption of a sharp-$k$ filter, which guarantees Markovian walks, is mathematically convenient but physically unrealistic, as it corresponds to a [window function](@entry_id:158702) in real space that has negative sidelobes ([sinc function](@entry_id:274746)). More physically plausible filters, such as a **Gaussian filter** with $\tilde{W}(kR) = \exp(-k^2R^2/2)$, are smooth in both real and Fourier space.

However, such filters introduce **correlations** between the steps of the random walk, making them non-Markovian. For these walks, the value of the overdensity $\delta(S)$ at a given "time" $S$ is not sufficient to predict its future evolution; one also needs to know its "velocity," or slope, $d\delta/dS$. The correlation between height and slope can be quantified. Using spectral moments defined as $\sigma_j^2(R) \equiv \int \frac{d^3 k}{(2\pi)^3} k^{2j} P(k) |\tilde{W}(kR)|^2$, a key dimensionless parameter is :
$$
\gamma \equiv \frac{\sigma_1^2(R)}{\sigma_0(R) \sigma_2(R)}
$$
For a power-law power spectrum $P(k) = Ak^n$ and a Gaussian filter, this parameter can be computed analytically. The calculation involves solving integrals of the form $\int_0^\infty k^p \exp(-\alpha k^2) dk$, which are related to the Gamma function $\Gamma(z)$. The final result, after simplification using the recurrence relation $\Gamma(z+1)=z\Gamma(z)$, is remarkably simple:
$$
\gamma = \sqrt{\frac{n+3}{n+5}}
$$
This shows that for a Gaussian filter, $\gamma$ is a constant that depends only on the [spectral index](@entry_id:159172) $n$ of the power spectrum, and that $\gamma  1$, indicating a non-trivial correlation. For the sharp-$k$ filter, one can show that $\gamma=1$, corresponding to an uncorrelated walk. Accounting for these correlated steps in first-passage calculations is a significant challenge, often requiring more advanced analytical techniques or numerical simulations.

#### Competing Processes: The Void-in-Cloud Problem

The [excursion-set formalism](@entry_id:749160) can be extended to describe cosmic voids as well as halos. Voids can be associated with regions where the density walk first crosses a lower barrier, $\delta_v  0$, corresponding to a critical underdensity for void formation. This introduces a scenario with two competing barriers: an upper barrier for collapse at $\delta_c$ and a lower one for voids at $\delta_v$.

A key issue is the **void-in-cloud** problem: a region that might locally form a void could be embedded within a larger-scale overdensity that is destined to collapse, thereby obliterating the void. We therefore need to calculate the probability that a trajectory hits the void barrier *before* hitting the collapse barrier. This is a classic two-barrier first-passage problem.

Consider a region whose large-scale environment corresponds to an overdensity $\delta_0$ at a variance scale $S_0$, where $\delta_v  \delta_0  \delta_c$. We want to find the probability $P_{\text{surv}}(\delta_0)$ that a random walk starting from this point will hit $\delta_v$ first. For a Markovian (Wiener) process, the probability $P(\delta)$ for a walk starting at an arbitrary point $\delta$ to hit $\delta_v$ before $\delta_c$ obeys a simple differential equation known as the backward Kolmogorov equation. For a driftless walk, this is :
$$
\frac{d^2 P}{d\delta^2} = 0
$$
The general solution is linear: $P(\delta) = A\delta + B$. The constants are determined by the boundary conditions. If the walk starts at $\delta_v$, it has certainly "survived" as a void, so $P(\delta_v) = 1$. If it starts at $\delta_c$, it has collapsed and the void [survival probability](@entry_id:137919) is zero, so $P(\delta_c) = 0$. Solving for $A$ and $B$ gives the elegant solution:
$$
P(\delta) = \frac{\delta_c - \delta}{\delta_c - \delta_v}
$$
The [survival probability](@entry_id:137919) for the region in question is then $P_{\text{surv}}(\delta_0) = (\delta_c - \delta_0)/(\delta_c - \delta_v)$. This result, analogous to the Gambler's Ruin problem, quantifies the environmental dependence of [structure formation](@entry_id:158241), showing how the large-scale context determines the fate of smaller-scale perturbations.

#### Beyond Gaussianity: The Impact of Primordial Non-Gaussianity

The entire framework described so far rests on the assumption of Gaussian [initial conditions](@entry_id:152863). While this is a cornerstone of the [standard cosmological model](@entry_id:159833), many theories of inflation predict small deviations from Gaussianity. The [excursion-set formalism](@entry_id:749160) can be adapted to explore the consequences of such **primordial non-Gaussianity (PNG)**.

Weak PNG can be described by adding higher-order [cumulants](@entry_id:152982) to the probability distribution of the initial density field. The leading-order correction is typically the skewness, characterized by the standardized third cumulant $\mathcal{S}_3 \equiv \langle \delta^3 \rangle / \sigma^3$. The one-point PDF of the smoothed field can be approximated by an **Edgeworth expansion** around a Gaussian:
$$
p(\delta) = \frac{1}{\sigma} \phi\left(\frac{\delta}{\sigma}\right) \left[ 1 + \frac{\mathcal{S}_3}{6} H_3\left(\frac{\delta}{\sigma}\right) \right] + \dots
$$
where $\phi(x)$ is the [standard normal distribution](@entry_id:184509) and $H_3(x) = x^3 - 3x$ is the third Hermite polynomial.

We can apply the Press-Schechter [ansatz](@entry_id:184384), which relates the [mass function](@entry_id:158970) to the tail of the one-point PDF, to this non-Gaussian distribution . The non-Gaussian [multiplicity](@entry_id:136466) function $f_{\text{NG}}(\nu)$ can be derived and compared to the standard Gaussian result $f_{\text{G}}(\nu)$. The calculation involves integrating the Edgeworth-expanded PDF above the threshold $\nu$ and differentiating with respect to scale. This yields a correction factor that multiplies the Gaussian [mass function](@entry_id:158970). To leading order in $\mathcal{S}_3$, the ratio of the non-Gaussian to Gaussian multiplicity functions is:
$$
\frac{f_{\text{NG}}(\nu)}{f_{\text{G}}(\nu)} \approx 1 + \frac{\mathcal{S}_3}{6} \left(\nu^3 - 3\nu\right)
$$
This powerful result shows that PNG has a distinct, scale-dependent effect on the [halo mass function](@entry_id:158011). Since the correction term scales as $\nu^3$ for large $\nu$, positive [skewness](@entry_id:178163) ($\mathcal{S}_3 > 0$) dramatically increases the abundance of the most massive, rarest halos, while negative skewness suppresses them. This makes the abundance of massive clusters a sensitive probe of primordial non-Gaussianity.