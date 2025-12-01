## Introduction
Positron Emission Tomography (PET) is a powerful imaging modality that provides unique insights into physiological, biochemical, and metabolic processes within the body. Its capability rests on a singular principle: detecting pairs of photons emitted from positron-electron annihilations to map the distribution of a radiotracer. In an ideal world, every detected photon pair would directly pinpoint the origin of the signal. However, the reality of photon transport through tissue is far more complex. The detected data is inevitably a mixture of valuable "true" signals and contaminating background events.

This article addresses the fundamental challenge at the heart of PET [data acquisition](@entry_id:273490): the presence of scattered and random coincidences. These unwanted events degrade image quality by introducing noise and spatial inaccuracies, compromising the quantitative reliability of the final image. Understanding the physical origins and statistical properties of each event type is therefore not just an academic exercise—it is the prerequisite for designing high-performance scanners, optimizing clinical protocols, and developing the sophisticated correction algorithms that make quantitative PET possible.

This article will guide you through this critical topic in three parts. The **Principles and Mechanisms** chapter will dissect the physics of true, scattered, and random coincidences, explaining how they are generated and how instrumental parameters like energy and timing windows are used to differentiate them. The **Applications and Interdisciplinary Connections** chapter will explore how these principles are put into practice, from evaluating scanner performance with the Noise-Equivalent Count Rate (NECR) to the essential role of correction techniques in quantitative imaging across various clinical and research fields. Finally, the **Hands-On Practices** section will provide opportunities to apply these concepts to solve realistic problems, cementing your understanding of how to manage the signal and noise that define every PET scan.

## Principles and Mechanisms

The fundamental principle of Positron Emission Tomography (PET) rests upon the detection of pairs of high-energy photons originating from positron-electron annihilation events. The information encoded in these photon pairs allows for the spatial mapping of a radiotracer distribution within a subject. However, not all detected photon pairs are of equal value. The physical processes that photons undergo as they travel from the annihilation site to the detectors give rise to distinct categories of coincidence events. A thorough understanding of these event types is paramount, as they directly determine the quality, accuracy, and quantitative potential of the final PET image. This chapter will systematically dissect the three principal types of coincidence events—true, scattered, and random—and explore the physical mechanisms and instrumental parameters that govern their detection and influence.

### The Coincidence Detection Paradigm

A PET system is designed to register the near-simultaneous arrival of two photons at a pair of detectors. When an annihilation event occurs, the two resulting photons, each with a nominal energy of $511 \ \mathrm{keV}$, travel in nearly opposite directions. The straight line connecting the two detectors that register such a pair is known as the **Line of Response (LOR)**. In an ideal scenario, the [annihilation](@entry_id:159364) event that produced the photons occurred somewhere along this line. By collecting millions of such LORs, [tomographic reconstruction](@entry_id:199351) algorithms can estimate the original distribution of the radiotracer.

To identify potentially valid photon pairs, the PET scanner's electronics implement two critical filters or "gates" for each detection event:

1.  An **energy window**: This is a discriminator that only accepts photons whose measured energy falls within a predefined range, typically $[E_{\min}, E_{\max}]$. This window is usually centered around the photopeak energy of $511 \ \mathrm{keV}$.
2.  A **coincidence timing window**: This is a temporal gate of a specific duration, $\tau_c$. If two accepted photons are detected by any pair of detectors within this time interval, they are registered as a coincidence event.

The successful application of these gates is essential for isolating the desired signal from various sources of background. Based on their physical origin and whether they provide accurate spatial information, coincidence events are classified into three fundamental categories.

### A Taxonomy of Coincidence Events

#### True Coincidences: The Signal

A **true coincidence** represents the ideal and most valuable type of event in PET. It is defined as the detection of a pair of photons that originate from a single [annihilation](@entry_id:159364) event and travel from the [annihilation](@entry_id:159364) site to their respective detectors without undergoing any interaction, such as scattering, within the subject's body. For a true coincidence to be recorded, both photons must pass the energy and timing criteria of the system [@problem_id:4556066]. The LOR defined by a true coincidence correctly passes through the physical location of the positron-electron [annihilation](@entry_id:159364), providing accurate spatial information for image reconstruction [@problem_id:4937394].

The probability of detecting a true coincidence is fundamentally limited by photon attenuation. As photons traverse tissue, they can be absorbed or scattered. According to the exponential attenuation law, the probability that a photon travels a distance $L$ through a medium with a linear attenuation coefficient $\mu_t$ without interaction is $\exp(-\mu_t L)$. For a true coincidence event where the two photons travel path lengths $L_1$ and $L_2$ to their detectors, the probability of both surviving is the product of their individual survival probabilities, $\exp(-\mu_t L_1) \exp(-\mu_t L_2) = \exp(-\mu_t (L_1+L_2))$. This demonstrates that the true [coincidence detection](@entry_id:189579) probability depends on the total attenuation along the entire LOR, a key principle utilized in attenuation correction algorithms.

#### Scattered Coincidences: A Source of Mispositioning

A **scattered coincidence** occurs when at least one of the two photons from a single [annihilation](@entry_id:159364) event undergoes Compton scattering within the subject before reaching a detector. Compton scattering has two critical consequences for PET imaging:

1.  **Change in Direction**: The scattered photon's trajectory is altered. This means the LOR formed by connecting the two detector locations no longer passes through the original site of [annihilation](@entry_id:159364).
2.  **Loss of Energy**: The photon transfers some of its energy to the recoiling electron, resulting in a scattered photon with reduced energy.

If a scattered photon, despite its reduced energy, is still accepted by the energy window, and the pair is registered within the timing window, a scattered coincidence is recorded [@problem_id:4556066]. The misplacement of the LOR for scattered events introduces a non-uniform haze or blur into the reconstructed image, degrading contrast and spatial resolution.

The primary defense against scattered coincidences is the energy discrimination window. The physics of Compton scattering provides a quantitative basis for this rejection mechanism. For an incident photon of energy $E_0$ scattering off a stationary electron, the energy of the scattered photon, $E'(\theta)$, is a function of the scattering angle $\theta$:
$$
E'(\theta) = \frac{E_0}{1 + \frac{E_0}{m_e c^2}(1 - \cos\theta)}
$$
where $m_e c^2$ is the rest mass energy of the electron ($511 \ \mathrm{keV}$). For [annihilation](@entry_id:159364) photons, $E_0 = m_e c^2$, simplifying the expression to:
$$
E'(\theta) = \frac{511 \ \mathrm{keV}}{2 - \cos\theta}
$$
This equation reveals that any scattering event ($\theta > 0$) results in an energy loss ($E'(\theta)  511 \ \mathrm{keV}$). By setting a lower energy threshold, $E_{\min}$, the system can reject all photons that have scattered beyond a certain angle. For instance, if a PET system uses an energy window of $[425, 650] \ \mathrm{keV}$, a scattered photon will only be accepted if $E'(\theta) \ge 425 \ \mathrm{keV}$. Solving for $\theta$ shows that this condition holds only for scatter angles up to a maximum of $\theta_{\max} \approx 37.09^\circ$ [@problem_id:4938766]. Photons scattered at larger angles are efficiently rejected.

The proportion of accepted coincidences that are scattered is known as the **scatter fraction**. This fraction depends on the size and density of the object being scanned and the width of the energy window. A key insight from physical modeling is that the ratio of single-scatter events to true events is approximately proportional to the total path length of the photons through the object, $(L_1+L_2)$ [@problem_id:4938764]. This explains why scatter correction is a more significant challenge in larger patients. Furthermore, widening the energy window allows more low-energy photons to be accepted, thereby increasing the scatter fraction.

#### Random Coincidences: A Source of Background Noise

A **random coincidence**, also known as an accidental coincidence, occurs when two photons originating from two *different and unrelated* annihilation events happen to strike a pair of detectors within the coincidence timing window, $\tau_c$ [@problem_id:4556066]. The LOR generated by a random coincidence is spurious; it does not correspond to any single physical annihilation event and contributes a background of false counts across the image, which reduces image contrast and degrades quantitation [@problem_id:4937394].

The rate of random coincidences can be modeled from first principles. If we consider two detectors with measured single-photon detection rates (singles rates) of $S_1$ and $S_2$, respectively, the events in each detector can be modeled as independent Poisson processes. For any single event detected at detector 1, a random coincidence will be registered if an unrelated event from detector 2 arrives within the timing window of duration $\tau_c$. The expected number of events from detector 2 in this window is $S_2 \tau_c$. Since events arrive at detector 1 at a rate of $S_1$, the total random coincidence rate, $R_{random}$, for this detector pair is given by the product:
$$
R_{random} = S_1 \times (S_2 \tau_c) = S_1 S_2 \tau_c
$$
Sometimes this is written as $R_{random} = 2 \tau S_1 S_2$ where $2\tau$ is the full window width. The notation must be handled with care. The key insight is that the randoms rate is proportional to the product of the singles rates and the width of the timing window [@problem_id:4938770]. This relationship underscores that the most effective way to reduce random coincidences is to use detectors with faster timing resolution, which allows for a narrower timing window $\tau_c$.

Because random coincidences are a form of noise, they must be estimated and subtracted from the total measured signal. Two common methods for this estimation are:
1.  **Singles-Based Estimation**: The randoms rate is calculated directly from the measured singles rates $S_1$ and $S_2$ and the known timing window $\tau_c$ using the formula above.
2.  **Delayed-Window Method**: A parallel coincidence processing circuit is implemented where the signal from one detector is electronically delayed by a time much longer than $\tau_c$. Coincidences registered in this delayed window cannot be from the same [annihilation](@entry_id:159364) event (true or scattered) due to the large delay. They must therefore be random coincidences. The rate of coincidences in the delayed window provides a direct measurement of the randoms rate.

In a well-calibrated system, both methods yield highly consistent estimates of the randoms rate [@problem_id:4890413].

### Detector and System Non-Idealities

The idealized models presented above provide a strong foundation, but the performance of a real PET system is further influenced by the non-ideal characteristics of its detectors and electronics.

#### Energy Resolution and the Energy Window

Scintillation detectors do not measure [photon energy](@entry_id:139314) with perfect precision. The measured energy for a monoenergetic photon is typically described by a Gaussian distribution centered on the true energy. This finite **[energy resolution](@entry_id:180330)** has implications for the trade-off in setting the energy window half-width, $w$. The probability of accepting an unscattered $511 \ \mathrm{keV}$ photon is given by integrating the Gaussian distribution over the window $[E_0 - w, E_0 + w]$, which yields an expression involving the error function, $\text{erf}(w/(\sqrt{2}\sigma_E))$ where $\sigma_E$ is the standard deviation of the energy resolution [@problem_id:4908107].

A narrow energy window is advantageous for rejecting scattered photons and also reduces the randoms rate. The accepted singles rate from the photopeak is proportional to the window width $w$ for small $w$. Since the randoms rate is proportional to the product of the singles rates, it scales with $w^2$ for a narrow window. However, a narrow window also rejects more true events due to the finite energy resolution, reducing the system's sensitivity. The optimal window setting is therefore a compromise between sensitivity and background rejection.

#### Dead Time and Pulse Pile-up

At high levels of radioactivity, the finite processing time of detector electronics becomes a significant factor. Two main effects emerge:

*   **Dead Time**: After a photon is detected, the detector and its electronics are unresponsive for a brief period, known as the **[dead time](@entry_id:273487)**, $\tau_d$. During this time, any other arriving photons are missed. In a non-paralyzable system, this leads to a loss of counts. The probability of detecting a true coincidence is reduced because it requires both detectors to be "live" at the time of photon arrival [@problem_id:4938763].

*   **Pulse Pile-up**: If two photons arrive at a single detector within a very short time interval (the "shaping time" of the electronics), they may be processed as a single pulse with a summed energy. This can lead to a problematic effect where two low-energy scattered photons, which would have been individually rejected, pile up to create a single pulse with an energy that falls *within* the acceptance window. This phenomenon artificially increases the measured singles rate, which in turn increases the calculated random coincidence rate [@problem_id:4938763].

#### Multiple Coincidences

Another high count rate phenomenon is the occurrence of **multiple coincidences**. This happens when three or more detectors fire within a single coincidence timing window. Such events are ambiguous because it is impossible to know which two photons form the correct LOR. Consequently, most PET systems are programmed to reject these "multiples." This rejection means that the simple randoms rate formula, $R = S_1 S_2 \tau_c$, can be an overestimate. A more accurate model accounts for the probability that, given a trigger event, exactly one other detector fires within the window while all other $D-2$ detectors in the system remain silent. This introduces a correction factor that reduces the estimated randoms rate, particularly at high singles rates [@problem_id:4938769].

### System Performance and Optimization: The Noise-Equivalent Count Rate (NECR)

Ultimately, the goal in PET system design and operation is to maximize the statistical quality of the acquired data. The various event types—true signal ($T$), scattered background ($S$), and random background ($R$)—can be combined into a single figure of merit called the **Noise-Equivalent Count Rate (NECR)**. A common form of the NECR equation, assuming randoms are measured and subtracted, is:
$$
\text{NECR} = \frac{T^2}{T + S + 2R}
$$
The NECR represents the count rate of an ideal system (with no scatter or randoms) that would yield the same signal-to-noise ratio as the real system. Maximizing NECR is a primary goal of system optimization.

All three rates, $T$, $S$, and $R$, are functions of instrumental parameters like the coincidence timing window, $\tau_c$. For example:
*   The true and scattered rates, $T(\tau_c)$ and $S(\tau_c)$, increase as $\tau_c$ widens, as more prompt events are accepted. The rate of this increase is determined by the system's timing resolution.
*   The randoms rate, $R(\tau_c)$, increases linearly with $\tau_c$.

This creates a crucial trade-off. A very narrow timing window rejects randoms effectively but may also reject a significant fraction of true events, reducing sensitivity. A very wide window captures nearly all true events but suffers from a high randoms rate that overwhelms the signal. Consequently, for any given level of radioactivity, there exists an optimal timing window width, $\tau_{opt}$, that maximizes the NECR. Determining this optimum involves a detailed characterization of the system's performance, including its timing resolution and dead-time behavior, providing a powerful example of how the fundamental principles of [coincidence detection](@entry_id:189579) are applied to achieve the best possible image quality in clinical practice [@problem_id:4938759].