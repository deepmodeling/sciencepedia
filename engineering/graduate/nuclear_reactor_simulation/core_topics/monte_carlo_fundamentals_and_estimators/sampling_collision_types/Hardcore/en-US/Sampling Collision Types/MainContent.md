## Introduction
In the probabilistic world of Monte Carlo [particle transport](@entry_id:1129401), determining the fate of a particle at a collision site is a cornerstone of accurate simulation. Once a simulation has established that a particle will collide, it must answer the critical question: what kind of interaction takes place? This decision—whether the particle scatters, is absorbed, or induces fission—is governed by a process known as collision type sampling. This article demystifies this fundamental mechanism, bridging the gap between the abstract physics of reaction cross sections and the concrete algorithms that drive high-fidelity reactor simulations. The accuracy of everything from criticality calculations to [radiation shielding](@entry_id:1130501) design hinges on correctly implementing these methods.

The following chapters will guide you from first principles to advanced applications. The "Principles and Mechanisms" chapter lays the theoretical groundwork, explaining how reaction probabilities are derived from nuclear data and how the standard sampling algorithms work. Building on this foundation, the "Applications and Interdisciplinary Connections" chapter explores how these core methods are adapted for complex physical models, coupled-physics simulations, and powerful variance reduction techniques, while also highlighting their use in other scientific fields. Finally, the "Hands-On Practices" section offers practical exercises to implement, validate, and apply these concepts, solidifying your understanding of this essential simulation technique.

## Principles and Mechanisms

In the probabilistic world of Monte Carlo [particle transport](@entry_id:1129401), a particle's life is a sequence of free flights punctuated by discrete collision events. After determining *that* a collision will occur and *where*, the simulator must answer the crucial question: *what kind* of interaction takes place? This chapter delves into the principles and mechanisms governing the sampling of collision types, a fundamental step that dictates the particle's fate—whether it scatters, is absorbed, or induces fission. We will progress from the foundational physics of reaction probabilities to the sophisticated algorithms required to handle complex material compositions and physical conditions.

### The Fundamental Probability of Interaction

The basis for sampling a collision type lies in the concept of the **[macroscopic cross section](@entry_id:1127564)**, denoted by $\Sigma$. For a given reaction channel $i$ (e.g., scattering, capture, fission), the macroscopic cross section $\Sigma_i$ represents the probability per unit path length that a particle will undergo that specific interaction. The total probability of *any* interaction per unit path length is the **total macroscopic cross section**, $\Sigma_t$, which is simply the sum of the cross sections for all possible exclusive reaction channels.

For a medium admitting three primary interaction types—scattering ($\Sigma_s$), radiative capture ($\Sigma_c$), and fission ($\Sigma_f$)—the total cross section is:
$$ \Sigma_t(E) = \Sigma_s(E) + \Sigma_c(E) + \Sigma_f(E) $$
Here, the dependence on particle energy $E$ is made explicit, as cross sections are highly energy-dependent. Events that result in the removal of the neutron, such as capture and fission, are collectively termed **absorption** events. The **macroscopic absorption cross section**, $\Sigma_a(E)$, is therefore defined as $\Sigma_a(E) = \Sigma_c(E) + \Sigma_f(E)$. This allows the total cross section to also be expressed as $\Sigma_t(E) = \Sigma_s(E) + \Sigma_a(E)$ .

Since each reaction channel represents a competing, independent Poisson process, the probability that a collision, once it occurs, is of a specific type $i$ is given by the ratio of its partial cross section to the total cross section. This forms the cornerstone of collision type sampling:

$$ P(\text{reaction type } i) = \frac{\Sigma_i(E)}{\Sigma_t(E)} $$

This [conditional probability](@entry_id:151013) is the branch of a Probability Mass Function (PMF) from which the simulation will sample. For example, the probability of the collision being a fission event is $p_f = \Sigma_f(E) / \Sigma_t(E)$ . Consider a material with the following properties at a given energy $E$: $\Sigma_s(E) = 1.2 \, \text{cm}^{-1}$, $\Sigma_c(E) = 0.3 \, \text{cm}^{-1}$, and $\Sigma_f(E) = 0.5 \, \text{cm}^{-1}$. The total cross section is $\Sigma_t(E) = 1.2 + 0.3 + 0.5 = 2.0 \, \text{cm}^{-1}$. The probabilities for each reaction channel are:

-   Scattering: $p_s = \frac{1.2}{2.0} = 0.6$
-   Capture: $p_c = \frac{0.3}{2.0} = 0.15$
-   Fission: $p_f = \frac{0.5}{2.0} = 0.25$

Note that these probabilities sum to unity, as required. It is critical to understand that the sampling of the collision event is governed by the probability of its occurrence, $\Sigma_f(E)$, not its outcome. For instance, the average number of neutrons emitted per fission, $\nu(E)$, is a property of the *outcome* of a fission event and does not influence the probability that the fission event itself will be selected as the collision type . The quantity $\nu(E)\Sigma_f(E)$ represents the macroscopic cross section for neutron *production* via fission, a different physical concept used in other parts of the transport calculation, such as $k$-eigenvalue [source iteration](@entry_id:1131994).

### Mapping Physical Reactions to Simulation Data

To implement this sampling, a simulation code must translate abstract physical concepts into concrete data. The primary interaction types are defined by their underlying physics, based on the conservation of energy, momentum, [baryon number](@entry_id:157941), and charge :

-   **Elastic Scattering**: An interaction $n + (Z, A) \rightarrow n + (Z, A)$ where the target nucleus is not internally excited. The reaction Q-value is exactly zero, and kinetic energy is conserved in the [center-of-mass frame](@entry_id:158134).
-   **Inelastic Scattering**: An interaction $n + (Z, A) \rightarrow n' + (Z, A)^*$ where the target nucleus is left in an excited state with energy $E^* > 0$. The reaction Q-value is negative, $Q = -E^*$, and the excited nucleus typically de-excites by emitting gamma rays.
-   **Radiative Capture**: An interaction $n + (Z, A) \rightarrow (Z, A+1) + \gamma$'s where the neutron is absorbed, forming a [compound nucleus](@entry_id:159470) that de-excites entirely through photon emission. No neutron emerges from the reaction. The Q-value is positive, corresponding to the binding energy of the neutron.
-   **Fission**: An interaction where a neutron is absorbed by a heavy nucleus, causing it to split into two or more smaller nuclei (fission fragments), releasing a large amount of energy (~200 MeV) and multiple secondary neutrons.

These physical definitions are mapped to standardized identifiers in [nuclear data libraries](@entry_id:1128922), such as the Evaluated Nuclear Data File (ENDF) format, which uses **MT (Material Type) numbers**. For a [high-fidelity transport](@entry_id:1126064) code, this mapping is precise :

-   Elastic scattering is mapped to **MT=2**.
-   Inelastic scattering is represented by a set of channels: **MT=51–90** for scattering to discrete excited levels and **MT=91** for scattering to an unresolved continuum of levels. The sum, MT=4, is a derived quantity not used directly for sampling if level-specific data exist.
-   Radiative capture, $(n,\gamma)$, is mapped to **MT=102**.
-   Total fission is mapped to **MT=18**, which itself is the sum of sub-channels like first-chance fission (MT=19), second-chance fission (MT=20), and so on.

### The Collision Sampling Algorithm in Practice

Understanding the "what" and "why" of collision probabilities is the first step. The "how" is a matter of algorithmic implementation.

#### Context within the Simulation Loop

The sampling of a collision type is a specific step within the larger particle transport algorithm. A particle's history is a loop:
1.  **Sample a free-flight distance** based on the total cross section $\Sigma_t$.
2.  **Determine the next event**: Compare the sampled distance to the distance to the nearest geometric boundary.
3.  **If a collision occurs** (i.e., the free-flight path ends within the current material region), the particle is moved to the collision site.
4.  **Only at this confirmed collision site** are the local, energy-dependent partial cross sections used to sample the specific reaction channel.
5.  **Sample the collision outcome**: Based on the chosen reaction, sample new energy, direction, and/or secondary particles.

Sampling the reaction channel before a collision is confirmed to occur is both computationally wasteful and physically incorrect, as the particle may cross into a different material with different cross sections before colliding .

#### The Inversion Method

The standard technique for sampling from a [discrete probability distribution](@entry_id:268307) $\{p_i\}$ is the **inversion method**. This involves constructing the **Cumulative Distribution Function (CDF)** and inverting it with a random number.

Let's consider a particle colliding in a material with four possible reaction channels, ordered as [elastic scattering](@entry_id:152152), absorption, [inelastic scattering](@entry_id:138624), and fission. At energy $E$, the microscopic cross sections are $\sigma_{\text{el}} = 2.0 \, \text{b}$, $\sigma_{\text{abs}} = 1.0 \, \text{b}$, $\sigma_{\text{inel}} = 1.0 \, \text{b}$, and $\sigma_{\text{fis}} = 0.0 \, \text{b}$ .

1.  **Calculate Total Cross Section**: The total microscopic cross section is $\sigma_t = 2.0 + 1.0 + 1.0 + 0.0 = 4.0 \, \text{b}$. (Note: In a single-nuclide material, the ratio of microscopic cross sections $\sigma_i/\sigma_t$ is identical to the ratio of macroscopic cross sections $\Sigma_i/\Sigma_t$).

2.  **Calculate Probabilities**:
    $p_{\text{el}} = 2.0/4.0 = 0.5$
    $p_{\text{abs}} = 1.0/4.0 = 0.25$
    $p_{\text{inel}} = 1.0/4.0 = 0.25$
    $p_{\text{fis}} = 0.0/4.0 = 0.0$

3.  **Construct the CDF**: The CDF, $F_k = \sum_{i=1}^k p_i$, is built by successively summing the probabilities:
    $F_1 = 0.5$
    $F_2 = 0.5 + 0.25 = 0.75$
    $F_3 = 0.75 + 0.25 = 1.0$
    $F_4 = 1.0 + 0.0 = 1.0$

4.  **Sample**: A uniform random variate $r$ is drawn from the interval $(0, 1)$. The chosen reaction is the one with the smallest index $k$ such that $F_{k-1}  r \le F_k$ (with $F_0 = 0$). This partitions the unit interval:
    - If $0  r \le 0.5$, select [elastic scattering](@entry_id:152152).
    - If $0.5  r \le 0.75$, select absorption.
    - If $0.75  r \le 1.0$, select [inelastic scattering](@entry_id:138624).
    - The fission channel, with an interval of zero width, can never be selected.

For computational efficiency, this process is often performed without explicit normalization. One can construct a table of cumulative cross sections, $S_k = \sum_{i=1}^k \sigma_i$. For our example, this would be $S_1=2.0$, $S_2=3.0$, $S_3=4.0$, $S_4=4.0$. A random number $r$ is drawn, scaled to $r' = r \cdot \sigma_t$, and compared against the $S_k$ table. This avoids a division operation for each collision, which can be significant in a large simulation .

### Handling Complexity in Material Composition and State

Real-world materials are rarely simple, uniform, and at zero temperature. The sampling procedure must correctly account for material mixtures and varying physical conditions.

#### Hierarchical Sampling in Mixtures

When a material is a mixture of different nuclides (or even stochastically mixed micro-regions), a hierarchical sampling approach is required. The probability of an interaction occurring with a particular constituent is proportional to that constituent's contribution to the total interaction rate.

Given a collision, the first step is to sample the target nuclide. In a [homogeneous mixture](@entry_id:146483) of nuclides indexed by $a$, each with [number density](@entry_id:268986) $N_a$ and microscopic total cross section $\sigma_{t,a}$, the probability of the collision being with nuclide $a$ is:
$$ P(\text{nuclide } a) = \frac{N_a \sigma_{t,a}}{\sum_j N_j \sigma_{t,j}} = \frac{\Sigma_{t,a}}{\Sigma_t} $$
Once the target nuclide $a$ is selected, the specific reaction channel $i$ is then sampled using the probabilities for that nuclide alone: $p_i = \sigma_{i,a} / \sigma_{t,a}$. This multi-level procedure ensures that the overall probability of a specific reaction $i$ with a specific nuclide $a$ is correctly represented .

#### Temperature-Dependent Cross Sections

Neutron cross sections, especially in the [resonance energy](@entry_id:147349) range, are sensitive to the temperature of the material. The thermal motion of target nuclei causes **Doppler broadening** of resonance peaks: as temperature increases, the resonances become lower and wider, while conserving their integrated area.

This change in cross-section shape directly affects the sampling probabilities $p_i(E,T) = \Sigma_i(E,T) / \Sigma_t(E,T)$. At the exact peak of a strong capture resonance, increasing temperature lowers $\Sigma_a(E,T)$, thus *decreasing* the probability of sampling a capture event. In the wings of the resonance, however, the broadened cross section increases $\Sigma_a(E,T)$, *increasing* the probability of capture.

This effect is deeply connected to **flux self-shielding**. In a material with strong, narrow resonances, the neutron flux is severely depressed at the [resonance energy](@entry_id:147349), as neutrons at that energy are quickly absorbed. When the resonance broadens with temperature, the self-shielding at the peak becomes less severe, and the increased cross section in the wings absorbs neutrons that would have otherwise passed through. The net effect is an overall increase in the total resonance absorption rate, a critical [negative feedback mechanism](@entry_id:911944) for [reactor safety](@entry_id:1130677). A Monte Carlo simulation correctly captures this by using temperature-dependent cross sections, which results in a more uniform sampling of capture events across the broadened resonance region as temperature rises .

#### Spatially Varying Properties

If a material has a temperature gradient, $T(\mathbf{x})$, its cross sections become spatially dependent, $\Sigma_i(\mathbf{x},E)$. In this case, sampling the collision type requires special care. The fundamental [principle of locality](@entry_id:753741) dictates that the outcome of a collision at site $\mathbf{x}_c$ depends only on the properties at $\mathbf{x}_c$. Any approximation that uses properties from the start of the flight path or a cell-averaged temperature will introduce bias.

Two rigorous, unbiased methods can handle this situation :

1.  **Analog Sampling**: The free-path distance $s$ is sampled by directly solving the inversion equation for an inhomogeneous medium: $\int_0^s \Sigma_t(\mathbf{x}(s')) ds' = -\ln(\xi)$, where $\xi$ is a random number. After finding the collision site $\mathbf{x}_c$, the reaction channel is sampled using the local probabilities $\Sigma_i(\mathbf{x}_c, E) / \Sigma_t(\mathbf{x}_c, E)$.
2.  **Delta-Tracking**: A majorant cross section $\Sigma_M$ is chosen such that $\Sigma_M \ge \Sigma_t(\mathbf{x}, E)$ for all $\mathbf{x}$. The particle is transported through a fictitious homogeneous medium with cross section $\Sigma_M$. At each tentative collision site, a "real" collision is accepted with probability $\Sigma_t(\mathbf{x}_c, E) / \Sigma_M$. If accepted, the reaction channel is sampled using the local probabilities at $\mathbf{x}_c$. If rejected (a "virtual" or "null" collision), the particle continues unchanged. Both methods correctly locate the collision and then use local properties to determine its nature.

### Advanced Topics in Collision Sampling

For high-fidelity simulations, even more sophisticated techniques are employed to handle complex physics and improve computational efficiency.

#### The Unresolved Resonance Region (URR)

In certain energy ranges, particularly for heavy nuclides like uranium-238, individual resonances are so densely packed that they cannot be experimentally resolved. This is the **Unresolved Resonance Region (URR)**. Here, the cross section at a given energy is treated as a stochastic variable. Using simple, energy-averaged cross sections is inaccurate because it neglects self-shielding effects.

The correct approach is the **[probability table method](@entry_id:1130196)**. A probability table provides a discrete representation of the cross-section distribution at a given energy. For each particle flight, a single correlated set of cross sections $(\sigma_t, \sigma_s, \sigma_c, \dots)$ is sampled from this table and treated as constant for that one flight . This correctly couples the attenuation physics (a high $\sigma_t$ leads to a short flight) with the reaction physics (the same set of cross sections is used to determine the collision type).

The physical difference is profound. The true average capture probability accounts for flux depression in resonances and is the *average of the ratio* of cross sections, $\langle \sigma_c / \sigma_t \rangle$. A simple model using average cross sections calculates the *ratio of the averages*, $\langle \sigma_c \rangle / \langle \sigma_t \rangle$, which is not the same. As a numerical illustration , consider a two-state probability table:
- State 1 (off-resonance): $p_1=0.9$, $\sigma_{c,1}=0.1$ b, $\sigma_{t,1}=1.0$ b.
- State 2 (on-resonance): $p_2=0.1$, $\sigma_{c,2}=9.0$ b, $\sigma_{t,2}=10.0$ b.

The incorrect "average cross section" method gives a capture probability of:
$P_c^{\mathsf{Avg}} = \frac{\langle \sigma_c \rangle}{\langle \sigma_t \rangle} = \frac{0.9(0.1) + 0.1(9.0)}{0.9(1.0) + 0.1(10.0)} = \frac{0.99}{1.9} \approx 0.52$

The correct [probability table method](@entry_id:1130196) gives the average of the ratios:
$P_c^{\mathsf{PT}} = \langle \frac{\sigma_c}{\sigma_t} \rangle = 0.9(\frac{0.1}{1.0}) + 0.1(\frac{9.0}{10.0}) = 0.09 + 0.09 = 0.18$

The average cross-section method dramatically overpredicts capture because it fails to account for the fact that the high capture cross section in the resonance is "shielded" by the correspondingly high total cross section, which reduces the neutron flux.

#### Non-Analog Sampling and Variance Reduction

Finally, it is possible to intentionally sample from a distribution different from the true physical one. This is called **non-analog** or **biased sampling** and is a powerful [variance reduction](@entry_id:145496) technique. To ensure the final simulation results (tallies) remain unbiased, any deviation from the physical probability must be compensated for by adjusting the particle's statistical **weight**.

If the physical probability of sampling reaction $i$ is $p_i = \Sigma_i / \Sigma_t$, and we choose to sample it with a different "trial" probability $q_i$, then after the event, the particle's weight $w$ must be updated to $w'$:
$$ w' = w \cdot \frac{p_i}{q_i} = w \cdot \frac{\Sigma_i / \Sigma_t}{q_i} $$
This weight correction, a form of importance sampling, guarantees that the expected value of any tally remains correct .

A common example is **implicit capture** (or [survival biasing](@entry_id:1132707)). Instead of allowing a particle to be randomly terminated by capture, the particle is forced to survive every collision. At each collision, its weight is reduced by the survival probability, $w' = w \cdot (1 - \Sigma_a/\Sigma_t) = w \cdot (\Sigma_s/\Sigma_t)$. Simultaneously, the amount of weight corresponding to absorption, $w \cdot (\Sigma_a/\Sigma_t)$, is deposited in a capture tally. This replaces a [random process](@entry_id:269605) (absorption or survival) with its deterministic expected outcome, reducing statistical variance by ensuring every particle contributes longer to the simulation.