## Introduction
As extreme weather events become more frequent and intense, the need to understand the role of anthropogenic climate change in specific disasters has grown more urgent. Stakeholders and the public increasingly ask not only if an event is more likely, but also how much worse climate change made the event that they just experienced. Traditional attribution methods often focus on how the probability of a class of events has changed, which can be abstract and difficult to connect to a single, realized event. This creates a knowledge gap, leaving a need for a framework that can provide a clear, physically-grounded causal narrative for a specific occurrence. The [storyline approach](@entry_id:1132464) to attribution directly addresses this gap by asking a different question: given the [atmospheric circulation](@entry_id:199425) that produced an event, how did climate change alter its character and impacts?

This article provides a comprehensive overview of the storyline methodology, guiding you from its theoretical foundations to its practical applications. In the upcoming sections, you will gain a deep understanding of this powerful technique.

*   **Principles and Mechanisms** will unpack the core theory of storyline attribution, including its conditional framework, the Pseudo-Global-Warming (PGW) method for constructing [counterfactuals](@entry_id:923324), and the methods for ensuring scientific rigor through physical consistency and uncertainty quantification.
*   **Applications and Interdisciplinary Connections** will demonstrate the versatility of the [storyline approach](@entry_id:1132464) by exploring its use in analyzing diverse phenomena like heatwaves, floods, and compound events, and its crucial links to hydrology, [cryospheric science](@entry_id:1123256), and [risk assessment](@entry_id:170894).
*   **Hands-On Practices** will offer a series of targeted exercises, allowing you to apply fundamental thermodynamic and statistical concepts that are central to building and interpreting a storyline analysis.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms that define the [storyline approach](@entry_id:1132464) to [climate event attribution](@entry_id:1122447). Building upon the introductory concepts, we will explore the theoretical underpinnings that distinguish storylines from other attribution methods, the practical techniques used to construct them, the methods for [quantitative analysis](@entry_id:149547), and the basis for their scientific rigor and decision-relevance.

### The Conditional Framework of Storyline Attribution

The primary distinguishing feature of a storyline is its **conditional framing**. Whereas traditional Probabilistic Event Attribution (PEA) typically seeks to answer an unconditional question—"How has anthropogenic climate change altered the probability of a class of events?"—a storyline addresses a conditional one: "Given the specific [atmospheric circulation](@entry_id:199425) pattern that produced this observed event, how did anthropogenic climate change affect its magnitude and impacts?"

This distinction is fundamental. PEA quantifies changes in the frequency of a general event class, treating the atmospheric circulation as a random variable to be sampled across large ensembles. In contrast, the [storyline approach](@entry_id:1132464) takes the observed circulation, or key aspects of it, as a given condition. The "story" is the physically consistent narrative of what transpired, and the attribution exercise involves re-telling that same story in a counterfactual climate to isolate the influence of altered background conditions.

Consider an extreme precipitation event driven by an atmospheric river . A storyline analysis would not concern itself with whether climate change made the atmospheric river's formation more or less likely. Instead, it would accept the existence and path of the atmospheric river as a given constraint, $\mathcal{S}$. The analysis then proceeds by using a numerical model to simulate the event twice: once in a factual world with present-day thermodynamic conditions (e.g., observed sea surface temperatures (SSTs) and greenhouse gas concentrations) and once in a counterfactual world where the anthropogenic signal has been removed from these thermodynamic conditions. The difference in the resulting precipitation intensity is then attributed to the thermodynamic component of climate change, conditional on the event's specific dynamics.

The core of the [storyline approach](@entry_id:1132464), therefore, is to partition the contributors to an extreme event into a **dynamic component** (the circulation, which is conditioned upon) and a **thermodynamic component** (the temperature and moisture environment, which is perturbed). This allows for a more direct and mechanistic diagnosis of how a warmer and moister world affects the character of weather events, assuming their dynamical drivers were to occur.

### Physical Self-Consistency and Budget Closure

A central claim of the [storyline approach](@entry_id:1132464) is that the resulting narrative is **physically self-consistent**. This is not a trivial assertion; it means that the constructed sequence of events is realized within a numerical model that solves the primitive equations of atmospheric motion. These equations represent the fundamental laws of physics: conservation of mass, momentum, energy, and water substance. A physically self-consistent storyline is one in which the evolution of the simulated atmosphere adheres to these laws.

The primary mechanism for verifying this consistency is through **budget analysis** over a defined control volume, such as the entire limited-area model domain . For any conserved quantity, the time rate of change of its total amount within the volume (the storage rate) must equal the net flux across the volume's boundaries plus any internal sources or sinks. A diagnostic residual for a given quantity is defined as the amount by which this balance fails to close. In a perfect, continuous system, this residual would be zero. In a numerical model, it represents the sum of [discretization errors](@entry_id:748522) and inconsistencies between different model components. A self-consistent simulation requires this residual to be negligibly small compared to the leading terms in the budget.

Key budget diagnostics include:

*   **Mass Budget:** The rate of change of total atmospheric mass in the domain must be balanced by the net advective flux of mass across the boundaries and the non-advective surface mass flux due to evaporation minus precipitation ($E-P$).
*   **Momentum Budget:** The rate of change of total momentum must be balanced by the flux of momentum across boundaries, the work done by pressure and stress forces, and the [body forces](@entry_id:174230) of gravity and Coriolis acceleration.
*   **Total Energy Budget:** The rate of change of total energy (kinetic + internal + potential) must be balanced by the flux of energy across boundaries, work done by pressure and stress, and diabatic heating/cooling from radiation and turbulent heat fluxes.
*   **Total Water Budget:** The rate of change of total water (vapor + liquid + ice) must be balanced by the advective and diffusive fluxes of water across boundaries and the net surface flux ($E-P$).

The requirement of physical self-consistency is not merely an academic exercise. It serves as a critical test of a storyline's validity. If a candidate storyline, when simulated, produces a large and statistically significant budget residual, it indicates a fundamental flaw in the model setup or the underlying assumptions . For instance, if a storyline positing purely thermodynamic changes results in a water budget that fails to close, it suggests that the neglected dynamical adjustments are, in fact, crucial and that the storyline is not a plausible explanation of the event.

### Constructing a Storyline Experiment

The construction of a credible storyline involves a series of carefully considered methodological choices, from defining the event and its conditioning to building a stable [counterfactual simulation](@entry_id:1123126).

#### Defining the Event and the Conditioning Set

The power of a storyline lies in its specificity, which requires a precise definition of both the event in question and the dynamical conditions being held constant.

An **event definition** must be quantitative. For a heatwave, for example, this involves specifying a spatiotemporal domain and an intensity threshold, $T^*$. The choice of $T^*$ is not neutral; it can significantly influence the resulting attribution statement. Defining the threshold relative to the baseline climatology, such as $T^* = \mu_b + n\sigma_b$, allows for a systematic exploration of event rarity. Studies have shown that for a simple mean shift in temperature, the probability ratio of a heatwave increases dramatically with the rarity of the event (i.e., with increasing $n$), demonstrating that attribution strength is highly sensitive to the event definition .

The **conditioning set**, $\mathcal{S}$, must also be precisely defined based on observable physical quantities. For some events, this can be relatively straightforward. For more complex phenomena, it requires sophisticated techniques. Consider an [atmospheric blocking](@entry_id:1121181) event, characterized by a persistent, quasi-stationary high-pressure system that disrupts the typical westerly flow. To create a storyline for such an event, one cannot simply condition on "a block." Instead, the condition must be formalized using objective criteria . This could involve:
1.  Classifying daily geopotential height fields into a set of discrete **weather regimes** (e.g., 'Block', 'Zonal').
2.  Defining a blocking event based on a **persistence criterion**, such as the 'Block' regime being active for a minimum number of consecutive days, $\Delta t$.
3.  Imposing an **anomaly magnitude threshold**, $H$, to ensure the event is sufficiently strong to be of interest.

By conditioning on such a well-defined dynamical state, the attribution analysis can specifically investigate how climate change alters the characteristics (e.g., associated temperatures or precipitation) of these blocking events when they occur.

#### The Pseudo-Global-Warming (PGW) Mechanism

Once the conditioning is defined, the central technical challenge is to simulate the specified dynamics within a different thermodynamic environment. The most common technique for this is the **Pseudo-Global-Warming (PGW) method**. In a typical PGW experiment, a regional, limited-area model is used to re-simulate a historical event. The boundary conditions that drive the model are taken from a historical reanalysis, but with a climate change anomaly signal superimposed.

This procedure, however, must be done with extreme care to maintain the **dynamical consistency** of the forcing fields . Simply adding a temperature anomaly, $\Delta T$, and a moisture anomaly, $\Delta q$, to the reanalysis fields without further adjustment creates a state that is not in physical balance. The modified temperature field implies a different pressure field (via the [ideal gas law](@entry_id:146757) and hydrostatic balance), which in turn implies a different wind field (via geostrophic balance). Forcing a model with these inconsistent fields can trigger spurious, high-amplitude gravity waves that destroy the simulation's physical realism.

A dynamically consistent PGW construction therefore requires several key steps:
1.  **Preserve the Wind Field:** The goal is to preserve the original synoptic evolution, so the wind fields ($\mathbf{u}$) from the reanalysis are retained at the model boundaries.
2.  **Recalculate Geopotential:** After adding the warming anomalies ($\Delta T$, $\Delta q$) and re-computing the [virtual temperature](@entry_id:1133832) $T_v$, the hydrostatic equation must be re-integrated through the atmospheric column to find a new geopotential field, $\Phi(p)$, that is consistent with the new temperatures.
3.  **Ensure Geostrophic Balance:** To preserve the original wind field, the **horizontal [pressure-gradient force](@entry_id:1130136)** must remain unchanged. This is the most difficult condition to satisfy perfectly. A common approximation is to assume the climate change anomalies are large-scale and slowly varying, and then apply a corrective pressure or geopotential offset to minimize the induced imbalance in the [geostrophic wind](@entry_id:271692).
4.  **Adjust Surface Boundary Conditions:** The lower boundary conditions, such as SST and soil moisture, must also be modified consistently with the warming signal to avoid unphysical jumps in surface energy and moisture fluxes.

When carefully implemented, the PGW method provides a powerful mechanism for running the "same weather movie" in a different climate, forming the practical backbone of many storyline studies.

### From Narrative to Quantification

While rooted in a narrative, a storyline analysis is fundamentally quantitative. It seeks to measure the influence of climate change on an event's properties and to partition that influence among different physical mechanisms.

#### Formalizing the Causal Chain

The narrative of a storyline can be formalized as a **causal chain**, where an initial forcing propagates through a series of intermediate physical links to produce the final impact. By modeling each link quantitatively, the entire chain becomes a tool for attribution .

For example, a storyline for an extreme precipitation event might link an SST anomaly to the final rainfall through the following chain:
1.  **SST Anomaly $\to$ Teleconnection:** A positive SST anomaly ($A_{\mathrm{SST}}$) drives a change in a large-scale teleconnection pattern ($T$).
2.  **Teleconnection $\to$ Regime Change:** The altered teleconnection pattern shifts the probability of occurrence of a local circulation regime conducive to heavy rain ($\Delta p_B$).
3.  **Multiple Drivers $\to$ Moisture Convergence:** The total change in moisture convergence ($\Delta M$) is decomposed into contributions from the altered dynamics (driven by $T$ and $\Delta p_B$) and the direct thermodynamic effect of warming on atmospheric moisture content (via the Clausius-Clapeyron relation).
4.  **Moisture Convergence $\to$ Precipitation:** The total moisture convergence anomaly is converted into a precipitation anomaly ($\Delta P$) via a potentially nonlinear microphysical and convective efficiency relationship.

This framework allows researchers to decompose the total precipitation change, $\Delta P$, into additive contributions from the teleconnection pathway, the regime pathway, the direct thermodynamic pathway, and a residual term that captures the effect of nonlinearities in the system. This provides a powerful quantitative diagnosis of *why* the event's intensity changed.

#### Embracing Epistemic Uncertainty

A single storyline simulation produces a single number for the attributable change, which can convey a misleading sense of certainty. In reality, the construction of the storyline involves numerous **epistemic choices**—choices made by the researcher based on plausible but uncertain assumptions. Responsible storyline analysis requires exploring this uncertainty.

Key sources of epistemic uncertainty include :
*   **Counterfactual Design:** The exact pattern and magnitude of the anthropogenic climate signal (e.g., the counterfactual cooling $\Delta T$) are not known with perfect precision. Exploring a range of plausible [counterfactuals](@entry_id:923324) (e.g., $\Delta T = 0.8 \text{ K}$ vs. $\Delta T = 1.0 \text{ K}$) is necessary.
*   **Physical Parameterizations:** The storyline may need to make assumptions about how physical processes respond to the change in climate. For instance, in a precipitation event, does the vertical velocity ($w$) or precipitation efficiency ($\epsilon$) change between the [factual and counterfactual worlds](@entry_id:1124814)? Exploring different plausible assumptions (e.g., fixed dynamics vs. slightly weakened uplift) is crucial.

By running the storyline analysis for each combination of these plausible choices, the result is not a single attribution value but an **attribution range**. For a 120 mm rainfall event, for example, the analysis might conclude that the anthropogenic contribution lies within the range of [5.9, 10.8] mm. Reporting this range, and explicitly stating the epistemic choices that define it, provides a more honest and robust assessment of the role of climate change.

### Scientific Validity and Decision-Relevance

The [storyline approach](@entry_id:1132464), by its nature, invites questions about its scientific validity and utility. Is it a rigorous scientific method or an elaborate form of storytelling? And what unique value does it offer?

#### Falsifiability and the Scientific Status of Storylines

A common concern is that storylines, being tailored to a specific event, may not be falsifiable. However, this is a misconception. A scientifically constructed storyline makes specific, quantitative claims that are indeed testable against both physical principles and empirical data. The scientific integrity of a storyline rests on a set of core assumptions that render its claims falsifiable :

1.  **Observable and Pre-specified Conditions:** The conditioning set $\mathcal{S}$ must be defined *ex ante* (before the analysis) using measurable, observable variables. This prevents "cherry-picking" the conditions to fit a desired narrative.
2.  **Positive Probability of Conditions:** The condition $\mathcal{S}$ must occur with a non-zero probability in the real world, $P^*(\mathcal{S}) > 0$. If the condition is so specific that it has never been observed and is not expected to be, then no empirical test is possible.
3.  **Ergodicity and Stationarity:** It must be assumed that, conditional on $\mathcal{S}$, the climate system is sufficiently stationary and ergodic. This ensures that observing multiple instances of $\mathcal{S}$ over time provides a [representative sample](@entry_id:201715) of the true [conditional probability distribution](@entry_id:163069) $P^*(E \mid \mathcal{S})$.
4.  **Model Fidelity:** Crucially, it must be assumed that the numerical model is well-calibrated in the relevant part of its phase space, such that the model's conditional probability, $P_M(E \mid \mathcal{S})$, is a faithful representation of the real world's, $P^*(E \mid \mathcal{S})$.

Under these assumptions, a storyline can be invalidated . Rejection is warranted if the storyline fails a test of physical consistency (e.g., its simulated budget residuals are too large) or if it fails a test of [empirical adequacy](@entry_id:1124409) (e.g., storyline-based hindcasts show significantly less skill than a baseline forecast). The ability to be falsified by quantitative tests is what elevates a storyline from a mere narrative to a scientific hypothesis.

#### Decision-Relevance and Information Gain

The high degree of conditioning in a storyline is not a weakness but a source of its unique value. For a decision-maker concerned with the impacts of a specific, realized event, a general probabilistic statement may be less useful than a specific, mechanistic explanation. Information theory provides a formal language for this concept .

The value, or **decision-relevance**, of a forecast can be quantified by the amount of uncertainty it reduces. In information theory, this is measured by the **entropy reduction**, $\Delta h = H(Y) - H(Y \mid X)$, where $H(Y)$ is the initial uncertainty about an outcome $Y$ and $H(Y \mid X)$ is the remaining uncertainty after receiving a forecast $X$. This reduction is also known as the [mutual information](@entry_id:138718) between $X$ and $Y$.

For a Gaussian distributed outcome, the entropy reduction provided by a Gaussian predictor is given by:
$$ \Delta h = -\frac{1}{2} \log_2(1-\rho^2) $$
where $\rho$ is the correlation coefficient between the predictor and the outcome. This equation shows that the [information gain](@entry_id:262008) increases monotonically as the absolute correlation $|\rho|$ approaches 1.

This framework allows us to compare the relevance of a storyline forecast to a standard probabilistic [ensemble forecast](@entry_id:1124518). A probabilistic forecast may have a modest correlation, $\rho_{\mathcal{E}}$, with the outcome. A storyline, by conditioning on the specific dynamics of the event, effectively filters out a large source of uncertainty. This can lead to a much higher correlation, $\rho_{\mathcal{S}}$, between the storyline-based prediction and the actual outcome for that specific class of events. Even if the [storyline approach](@entry_id:1132464) is not applicable to all events, its ability to achieve a higher correlation ($\rho_{\mathcal{S}} > \rho_{\mathcal{E}}$) means it can provide a greater reduction in uncertainty and thus deliver more actionable information for decision-making related to that particular causal pathway.