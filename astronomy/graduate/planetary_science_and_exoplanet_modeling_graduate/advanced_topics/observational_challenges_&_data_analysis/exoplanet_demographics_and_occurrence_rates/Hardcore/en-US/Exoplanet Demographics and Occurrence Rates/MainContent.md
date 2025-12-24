## Introduction
The discovery of thousands of exoplanets has transformed astronomy, shifting the focus from finding individual worlds to characterizing the statistical properties of entire planet populations. Central to this field of [exoplanet demographics](@entry_id:1124734) is the concept of the **occurrence rate**—the average number of planets per star as a function of their physical and orbital properties. Understanding this rate is key to placing our Solar System in a galactic context and constraining theories of [planet formation](@entry_id:160513). However, determining the true occurrence rate is a significant challenge, as every astronomical survey provides a biased and incomplete view of the underlying population. Planets of certain sizes and orbits are far easier to detect than others, creating a gap between what we observe and what truly exists.

This article provides a comprehensive guide to the statistical principles and practical methods used to bridge this gap. You will learn how to move from a raw list of planet detections to a robust, scientifically meaningful census of the galaxy's planets. The following chapters will guide you through this process:
-   **Principles and Mechanisms:** We will establish the mathematical foundation, defining the occurrence rate as a [point process](@entry_id:1129862) intensity and detailing the crucial role of the survey completeness function in correcting for observational biases.
-   **Applications and Interdisciplinary Connections:** We will explore how these statistical tools are applied to answer astrophysical questions, combine data from different surveys, and build sophisticated models that account for real-world complexities like stellar multiplicity and target selection effects.
-   **Hands-On Practices:** You will have the opportunity to apply these concepts through practical exercises, learning to derive occurrence rate limits, compare statistical estimators, and understand the nuances of data parameterization.

## Principles and Mechanisms

The study of [exoplanet demographics](@entry_id:1124734) seeks to move beyond the discovery of individual worlds to characterize the statistical properties of planet populations as a whole. The central quantity in this endeavor is the **exoplanet occurrence rate**, a measure of the average number of planets per star as a function of their physical and orbital properties. This chapter delineates the fundamental principles and statistical mechanisms that form the basis for measuring and modeling these occurrence rates. We will begin by formally defining the occurrence rate, then explore the practical challenges of measuring this intrinsic quantity from biased survey data, and conclude with a discussion of advanced modeling techniques and systematic effects.

### The Occurrence Rate Surface: A Point Process Formalism

To precisely quantify planet demographics, it is instructive to model the population of planets around a given star as a realization of a **spatial point process**. In this framework, each planet is a point in a multi-dimensional parameter space. For simplicity and in accordance with common practice, we will consider the two-dimensional space defined by planetary radius, $R$, and [orbital period](@entry_id:182572), $P$. To better handle the vast dynamic range of these parameters, we work in logarithmic coordinates, $(\ln R, \ln P)$.

The fundamental quantity describing the planet population is the **occurrence rate surface**, denoted $f(R,P)$. It is defined as the differential mean number of planets per star per unit area in the logarithmic parameter space . Mathematically, this is expressed as:
$$
f(R,P) = \frac{d^2N}{d\ln R \, d\ln P}
$$
Here, $d^2N$ represents the expected, or average, number of planets found in an infinitesimal rectangle of size $d\ln R \times d\ln P$. It is critical to recognize that $f(R,P)$ is an **intensity function** in the language of [point process](@entry_id:1129862) theory, not a probability density function. The distinction is paramount. A probability density must integrate to unity over its entire domain, representing the certainty of finding a single object somewhere. In contrast, the integral of the intensity function $f(R,P)$ over a [finite domain](@entry_id:176950) $\mathcal{D}$ in the $(\ln R, \ln P)$ plane yields the mean number of planets per star, $\eta_{\mathcal{D}}$, with properties falling within that domain:
$$
\eta_{\mathcal{D}} = \mathbb{E}[N(\mathcal{D})] = \int_{\mathcal{D}} f(R,P) \, d\ln R \, d\ln P
$$
Since a star can host multiple planets, this mean number can, and often does, exceed one. For example, the mean number of planets per star in our own Solar System with $R > 0.3 \, R_{\oplus}$ is 8. Therefore, the integral of $f(R,P)$ over the entire parameter space of interest is the total average number of planets per star, a quantity often denoted as "planets per star" or $\eta_{\text{total}}$.

While $f(R,P)$ itself is not a probability, it can be used to derive probabilistic statements. For instance, if we assume that the number of planets in any given region of parameter space follows a Poisson distribution (a common assumption for non-interacting planets), the probability of a star hosting *at least one* planet in the domain $\mathcal{D}$ is given by $1 - \exp(-\eta_{\mathcal{D}})$, which is fundamentally different from $\eta_{\mathcal{D}}$ itself .

### From Detections to Occurrence: The Role of Survey Completeness

The occurrence rate $f(R,P)$ is an intrinsic property of the galactic planetary population. However, we do not observe this distribution directly. Any astronomical survey is subject to selection effects and biases that render some planets easier to detect than others. The link between the intrinsic population and the observed sample of detected planets is mediated by the **survey completeness function**, $C(R,P)$.

The completeness function, also known as the detection efficiency or sensitivity, is the probability that a planet with properties $(R,P)$ orbiting one of the stars in the survey target list would be successfully detected and identified as a planet candidate. This probability is a complex function that encapsulates numerous factors:
1.  The geometric probability that the planet's orbit is aligned to produce a transit.
2.  The fraction of time the target star was actually observed (the [window function](@entry_id:158702)).
3.  The probability that the survey's detection [pipeline registers](@entry_id:753459) a signal of a given strength.
4.  The probability that a detected signal passes through a vetting process designed to remove false positives.

The expected number of detected planets, $\mathbb{E}[N_{\text{det}}]$, in a survey of $N_\star$ stars is given by the integral of the intrinsic occurrence rate modulated by the completeness function, summed over all stars:
$$
\mathbb{E}[N_{\text{det}}] = \sum_{s=1}^{N_\star} \int \int f(R,P) \, C_s(R,P) \, d\ln R \, d\ln P
$$
where $C_s(R,P)$ is the completeness for star $s$. If the stars are sufficiently similar, we can often use an average completeness $C(R,P)$ and write $\mathbb{E}[N_{\text{det}}] \approx N_\star \int \int f(R,P) C(R,P) \, d\ln R \, d\ln P$. The primary goal of occurrence rate studies is to solve this [integral equation](@entry_id:165305) for the unknown function $f(R,P)$, given the observed detections and a well-characterized completeness function $C(R,P)$.

### Characterizing Observational Biases

A robust determination of $f(R,P)$ is impossible without a precise understanding of all components of the completeness function $C(R,P)$.

#### Detection Efficiency and Signal-to-Noise Ratio

At its core, detection is a problem of identifying a signal in the presence of noise. The detectability of a signal is fundamentally governed by its **Signal-to-Noise Ratio (SNR)**. For transit surveys, the signal is the [transit depth](@entry_id:1133353), while for radial velocity surveys, it is the amplitude of the velocity variation. The noise arises from instrumental sources (e.g., photon noise, detector readout noise) and astrophysical sources (e.g., stellar granulation, spots, and pulsations).

The probability of detecting a signal typically follows a sigmoid-like curve as a function of its SNR. Below a certain SNR, detection is impossible; above a certain SNR, detection is nearly certain. This relationship can be characterized empirically through **injection-recovery experiments**. In these experiments, synthetic planetary signals with known properties are injected into the real observational data and run through the same detection and vetting pipeline used for the real search. The fraction of recovered signals as a function of SNR provides a direct measurement of the detection efficiency .

A common model for this efficiency curve is the logistic function:
$$
C(\text{SNR}) = \left[1 + \exp\left(-\frac{\text{SNR} - \theta}{\Delta}\right)\right]^{-1}
$$
Here, $\theta$ represents the SNR at which the detection efficiency is $50\%$, serving as a soft detection threshold. The parameter $\Delta$ controls the width of the transition region, describing how rapidly the completeness rises from 0 to 1 around the threshold. These parameters can be determined by performing a maximum likelihood fit to the results of an injection-recovery experiment, typically by modeling the number of recovered signals at each SNR as a binomial process .

#### Geometric Transit Probability and Orbital Eccentricity

For a planet to be detected by the transit method, its orbit must be viewed nearly edge-on, such that the planet passes in front of its star from our line of sight. For a circular orbit, the geometric probability of transit is simply the ratio of the [stellar radius](@entry_id:161955) to the orbital semi-major axis, $P_{\text{tr, circ}} = R_\star/a$. Many early studies relied on this simple formula.

However, most exoplanets, particularly those with long periods, have non-zero [eccentricity](@entry_id:266900). For an eccentric orbit, the star-planet distance at transit depends on the orientation of the orbit in its plane (the argument of periastron, $\omega$). When averaged over all possible orientations, the geometric transit probability for an orbit with eccentricity $e$ is given by :
$$
\langle P_{\text{tr}} \rangle_e = \frac{R_\star}{a(1-e^2)}
$$
Since $e^2 \ge 0$, eccentric planets have a higher average transit probability than circular ones at the same semi-major axis. This is because eccentric orbits spend more time near apastron (further from the star), but transit can occur anywhere along the line of sight, and the geometry favors transits near periastron where the star-planet distance is smaller. The $1/(1-e^2)$ term arises from averaging the geometric factor $1/r_{\text{tr}}$ over all orbital orientations.

Neglecting this effect by assuming all orbits are circular biases the resulting occurrence rates. An occurrence rate inferred under the circular-orbit assumption, $\Gamma_{\text{circ}}$, must be multiplied by a correction factor $C(e) = 1-e^2$ to obtain the true rate. To correct the entire population, one must average this factor over the population's underlying [eccentricity](@entry_id:266900) distribution. For a population with a mean squared [eccentricity](@entry_id:266900) of $\langle e^2 \rangle$, the overall correction factor is $\langle C \rangle = 1 - \langle e^2 \rangle$. For typical long-period planet populations, this can lead to a ~10-15% downward revision of occurrence rates .

### Practical Estimation of Occurrence Rates

With a model for the completeness function, we can proceed to estimate the occurrence rate surface $f(R,P)$.

#### Binned (Non-Parametric) Estimators

The most direct approach is to divide the $(R,P)$ plane into a grid of bins and estimate the average occurrence rate, $\hat{\eta}_{ij}$, in each bin $(i,j)$. For each bin, the estimator is constructed by dividing the number of "true" planets detected by the effective number of opportunities for detection . This takes the form of an **[inverse probability](@entry_id:196307) weighting** estimator, analogous to the Horvitz-Thompson estimator in [survey statistics](@entry_id:755686).

The numerator is the estimated number of true planets in the bin. Since a list of detected candidates may contain [false positives](@entry_id:197064), each candidate $k$ is typically assigned a reliability weight, $w_k$, representing its probability of being a genuine planet (e.g., $w_k = 1 - \text{FPP}_k$, where FPP is the False Positive Probability). The sum of these weights, $\sum_k w_k$, provides an estimate of the number of true planets detected in the bin.

The denominator represents the total search volume. For each star $s$ in the survey, one calculates the completeness $C_{ij}(s)$, which is the probability that a planet from bin $(i,j)$ would have been detected around that star. The sum of these probabilities over all stars, $\sum_s C_{ij}(s)$, gives the effective number of stars surveyed for that bin.

The resulting binned occurrence rate estimator is:
$$
\hat{\eta}_{ij} = \frac{\sum_{k \in \text{bin }ij} w_k}{\sum_{s=1}^{N_\star} C_{ij}(s)}
$$
This provides a non-parametric estimate of the occurrence landscape, but it is subject to the choice of [binning](@entry_id:264748) scheme and can suffer from low statistics in sparsely populated regions of parameter space.

#### Incorporating Measurement Uncertainties

The binned method implicitly assumes that each planet is unambiguously assigned to a single bin. In reality, every measured property has an associated uncertainty. For example, the uncertainty in a planet's radius, $R_p = k R_\star$, is dominated by the uncertainty in the [stellar radius](@entry_id:161955), $\sigma_{R_\star}$, such that $\sigma_{R_p} \approx k \sigma_{R_\star}$.

When a planet's properties have uncertainties comparable to the bin size, its assignment to a specific bin becomes probabilistic. A more sophisticated approach is to calculate a **classification probability**, $\mathcal{C}$, which is the probability that the planet's true properties lie within the bin boundaries, by integrating the measurement's error distribution (e.g., a 2D Gaussian) over the area of the bin . For a single candidate, this probability can be treated as an "effective count" in the numerator of the occurrence rate estimator. For a candidate with classification probability $\mathcal{C}$ and a uniform survey completeness $q$ over $N_\star$ stars, the estimated occurrence rate contributed by this single planet is $\hat{f} = \mathcal{C} / (N_\star q)$.

#### Unbinned (Per-Candidate) Estimators

To avoid arbitrary binning altogether, one can formulate the estimator as a sum of contributions from each individual candidate . Each detected candidate $j$ contributes to the overall occurrence rate density. Its contribution is its reliability, $r_j$, divided by the effective number of trials, $N_{\text{eff},j}$, that could have produced that specific detection. The effective number of trials is the sum over all survey stars of the per-star detection probability for a planet with the properties of candidate $j$: $N_{\text{eff},j} = \sum_s p_{\text{det},s}(\theta_j)$. The total occurrence rate in a large region is then the sum of these individual contributions:
$$
\hat{f}_{\text{bin}} = \sum_{j \in \text{bin}} \frac{r_j}{N_{\text{eff}, j}}
$$
This method naturally handles variations in completeness across the parameter space and leverages the precise information of each detection, providing a more refined estimate of the occurrence rate density.

### Advanced Topics and Systematic Effects

Accurate demographic modeling requires careful consideration of subtle systematic effects that can bias the results.

#### The Impact of Unresolved Stellar Multiplicity

A significant fraction of stars in the galaxy are members of binary or multiple star systems. If a planet-hosting star has an unresolved stellar companion, the light from the companion dilutes the [transit depth](@entry_id:1133353). The observed depth, $\delta_{\text{obs}}$, is related to the true depth, $\delta_{\text{true}}$, by $\delta_{\text{obs}} = \delta_{\text{true}} / (1 + F_2/F_1)$, where $F_2/F_1$ is the flux ratio of the companion to the primary.

This has two major consequences :
1.  **Biased Radii:** The inferred planet radius, which is proportional to the square root of the depth, will be systematically underestimated. A Jupiter-sized planet might be misclassified as a Neptune, and a Neptune as a sub-Neptune.
2.  **Detection Bias:** The diluted transit depth may fall below the survey's detection threshold, causing planets that would otherwise be detectable to be missed entirely.

Both effects conspire to artificially lower the measured occurrence rate of small planets. The magnitude of this bias depends on the binary fraction among survey targets and the distributions of companion mass ratios and orbital periods. Correcting for this requires complex simulations or analytical models that account for the effects of dilution on both the inferred radius distribution and the overall [detection completeness](@entry_id:1123598). A first-order analysis shows that the naive occurrence rate can be biased by a multiplicative factor that depends on the binary fraction $f_b$ and the power-law indices of the [mass-luminosity relation](@entry_id:161485) and the planet radius distribution .

#### The Impact of Stellar Variability

Stellar variability, arising from phenomena like granulation, oscillations, and magnetic activity, introduces [correlated noise](@entry_id:137358) ("red noise") into photometric time series. This is distinct from uncorrelated "white noise" from instrumental sources. This correlated noise inflates the total noise budget, particularly on longer timescales.

The variance of a transit depth measurement, which is typically an average over many in-transit data points, is sensitive to this correlated noise. If stellar variability is modeled as an [autoregressive process](@entry_id:264527) (e.g., AR(1)), the variance of the mean is no longer simply $\sigma^2/M$ but includes additional terms that depend on the number of samples $M$ and the correlation parameter $\phi$ . This increased noise reduces the SNR of a transit of a given depth, thereby lowering the [detection completeness](@entry_id:1123598). Because stellar variability levels differ from star to star, a robust population-level analysis requires marginalizing the completeness over the expected distribution of stellar variability amplitudes, often accomplished via [numerical quadrature](@entry_id:136578).

#### Parameter Identifiability and Survey Design

The ability to recover the true parameters of an underlying occurrence model is fundamentally limited by the nature of the survey's selection biases. An extremely sharp or narrow selection function can create degeneracies between model parameters, making them impossible to constrain jointly.

This can be formalized using the **Fisher Information Matrix**, which quantifies the amount of information a dataset provides about a set of model parameters. A singular Fisher matrix, with a determinant of zero, indicates that at least one combination of parameters is unconstrained by the data.

For example, consider a hypothetical survey whose completeness function is non-zero only along a narrow 1D curve in the $(R,P)$ plane, such as $R \propto P^\gamma$. If one attempts to fit a power-law occurrence model of the form $f(R,P) \propto R^\alpha P^\beta$, the data will only constrain the specific combination of exponents along that curve, namely $\alpha\gamma + \beta$. It becomes impossible to disentangle $\alpha$ and $\beta$ individually . This illustrates a crucial lesson: the design of a survey and its inherent biases dictate the questions we can hope to answer about the intrinsic exoplanet population.

### Parametric Modeling of Occurrence Rates

While binned estimates are valuable for their model independence, a more powerful approach is to fit a continuous, parametric model directly to the unbinned planet detections. This is typically done within a **hierarchical Bayesian framework**.

In this approach, the occurrence rate surface is described by a functional form with a set of parameters, $\theta$. A common choice is a separable power law in radius and period :
$$
f(R,P \mid k, \alpha, \beta) = k \left(\frac{R}{R_0}\right)^{\alpha} \left(\frac{P}{P_0}\right)^{\beta}
$$
Here, $k$ is a [normalization constant](@entry_id:190182), while $\alpha$ and $\beta$ are the power-law indices governing the slopes of the distributions. The observed set of detections is then modeled as a realization of an inhomogeneous Poisson point process with an intensity function given by $\lambda(R,P) = N_\star f(R,P \mid \theta) C(R,P)$.

The likelihood of observing $N_d$ planets at locations $\{(R_d, P_d)\}$ is given by the Poisson point process likelihood. Using Bayes' theorem, this likelihood is combined with prior probability distributions for the model parameters $(k, \alpha, \beta)$ to derive their joint posterior distribution. This posterior represents our complete state of knowledge about the parameters, given the data and our prior beliefs. From this posterior, we can compute best-fit values, uncertainties, and correlations for the model parameters. For computational efficiency, it is often possible to analytically marginalize (integrate out) the normalization parameter $k$, which simplifies the numerical exploration of the posterior for the more physically interesting [shape parameters](@entry_id:270600) $\alpha$ and $\beta$ .

This parametric approach avoids arbitrary binning, naturally propagates uncertainties, and yields a continuous, smooth model of the planet population that can be readily compared with theories of planet formation and evolution.