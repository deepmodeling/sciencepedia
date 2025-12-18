## Introduction
Seismic [wave attenuation](@entry_id:271778), the gradual loss of energy as a wave propagates through the Earth, is a fundamental phenomenon that encodes rich information about the physical state of subsurface materials. While often viewed as a complication in [seismic imaging](@entry_id:273056), attenuation is a direct signature of rock and fluid properties, driven by mechanisms like internal friction and fluid flow. Accurately modeling this [energy dissipation](@entry_id:147406) is therefore critical for quantitative seismic interpretation, reservoir characterization, and hazard assessment. However, moving beyond simple empirical descriptions requires a robust framework grounded in the physics of [viscoelasticity](@entry_id:148045).

This article provides a comprehensive exploration of attenuation modeling centered on one of its most powerful and versatile tools: the Standard Linear Solid (SLS) model. We will dissect this model from its theoretical foundations to its practical application, providing the knowledge needed to understand, implement, and utilize it in [computational geophysics](@entry_id:747618).

Across the following chapters, you will gain a multi-faceted understanding of the topic. The first chapter, **Principles and Mechanisms**, builds the SLS model from the first principles of [linear viscoelasticity](@entry_id:181219), introducing concepts like the [complex modulus](@entry_id:203570) and quality factor, and culminates in an efficient computational framework using memory variables. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how this model is used to characterize Earth materials, predict P- and S-wave behavior, and model complex [wave propagation](@entry_id:144063) in anisotropic and layered media. Finally, the **Hands-On Practices** chapter offers a series of guided computational exercises to solidify your understanding by implementing and experimenting with SLS models to simulate realistic attenuation behavior.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanical models that form the basis of [seismic attenuation](@entry_id:754635) modeling. Having established the importance of attenuation in the previous chapter, we now develop the formal mathematical and physical framework necessary to describe and compute wave propagation in viscoelastic media. Our primary tool will be the **Standard Linear Solid (SLS)** model, which provides a powerful yet intuitive link between material properties and observable wave phenomena like energy loss and velocity dispersion. We will begin with the foundational concepts of [linear viscoelasticity](@entry_id:181219), build the SLS model from first principles, generalize it for practical applications, connect it to wave propagation, and finally, outline its computational implementation.

### The Language of Linear Viscoelasticity: Complex Modulus and Quality Factor

In a perfectly elastic material, stress is instantaneously and proportionally related to strain. However, in real Earth materials, there is a delay in the material's response, leading to a [phase lag](@entry_id:172443) between [stress and strain](@entry_id:137374) when subjected to [cyclic loading](@entry_id:181502). This phase lag is the macroscopic signature of energy dissipation. For a time-harmonic strain $\epsilon(t) = \epsilon_0 \exp(i\omega t)$, the stress in a linear viscoelastic medium will also be harmonic but phase-shifted: $\sigma(t) = \sigma_0 \exp(i(\omega t + \delta))$. This relationship is most elegantly captured in the frequency domain using the **[complex modulus](@entry_id:203570)**, denoted $E^*(\omega)$.

The [complex modulus](@entry_id:203570) relates the complex stress and strain amplitudes: $\sigma(\omega) = E^*(\omega) \epsilon(\omega)$. It is composed of a real part, the **[storage modulus](@entry_id:201147)** $E'(\omega)$, and an imaginary part, the **loss modulus** $E''(\omega)$:

$E^*(\omega) = E'(\omega) + i E''(\omega)$

The storage modulus $E'(\omega)$ represents the elastic component of the response—the part of the energy that is stored and returned during a deformation cycle. The loss modulus $E''(\omega)$ represents the viscous component—the part of the energy that is dissipated, typically as heat, during a cycle. The phase angle $\delta$ is related to these moduli by the **[loss tangent](@entry_id:158395)**, $\tan \delta = E''(\omega) / E'(\omega)$.

The central quantity used to characterize attenuation is the dimensionless **[seismic quality factor](@entry_id:754643)**, $Q$. This quantity quantifies the intrinsic, constitutive energy loss within a material, a process fundamentally distinct from apparent amplitude reductions caused by geometrical spreading of the [wavefront](@entry_id:197956) or the scattering of energy by heterogeneities. While geometrical spreading and scattering redistribute [wave energy](@entry_id:164626) in space, intrinsic attenuation represents the irreversible conversion of [mechanical energy](@entry_id:162989) into thermal energy .

$Q$ can be defined in two equivalent ways, which provide complementary physical insights.

1.  **Energetic Definition**: The [quality factor](@entry_id:201005) is defined as $2\pi$ times the ratio of the peak elastic energy stored ($E$) in a volume of the material during a cycle to the energy dissipated ($\Delta E$) in that same volume over one cycle. The inverse [quality factor](@entry_id:201005), $Q^{-1}$, which is a direct measure of attenuation, is therefore:
    $$
    Q^{-1} = \frac{1}{2\pi} \frac{\Delta E}{E}
    $$
    Here, $\Delta E$ corresponds to the area enclosed by the elliptical hysteresis loop in a stress-strain plot for a single cycle of harmonic loading. The peak stored energy, $E$, is given by $\frac{1}{2} E'(\omega) \epsilon_0^2$, where $\epsilon_0$ is the peak strain amplitude.

2.  **Complex Modulus Definition**: The [quality factor](@entry_id:201005) can be defined directly as the ratio of the storage modulus to the loss modulus. This is equivalent to the reciprocal of the [loss tangent](@entry_id:158395):
    $$
    Q^{-1} = \frac{E''(\omega)}{E'(\omega)} = \tan \delta
    $$
    This definition is particularly convenient for theoretical analysis in the frequency domain. A rigorous derivation shows that for harmonic loading, these two definitions are identical . The quality factor $Q$ is thus a material property determined entirely by its [complex modulus](@entry_id:203570) at a given frequency.

### The Standard Linear Solid (SLS) Model: A Canonical Relaxation Mechanism

To give physical substance to the abstract concepts of complex moduli and quality factors, we employ mechanical analog models. The simplest models that capture key features of [seismic attenuation](@entry_id:754635) are built from linear springs (representing elastic storage) and dashpots (representing viscous dissipation). A spring follows Hooke's Law, $\sigma = E\epsilon$, while a dashpot's stress is proportional to the [strain rate](@entry_id:154778), $\sigma = \eta \dot{\epsilon}$, where $\eta$ is viscosity.

The **Standard Linear Solid (SLS)**, also known as the Zener model, is a fundamental building block for modeling viscoelastic solids. It consists of a purely elastic spring in parallel with a **Maxwell element**. The Maxwell element itself is a series combination of another spring and a dashpot. Let the parallel spring have a modulus $E_1$ and the Maxwell element consist of a spring with modulus $E_2$ and a dashpot with viscosity $\eta$.

By applying the rules for combining mechanical elements (stresses add in parallel, strains add in series), one can derive the time-domain differential [constitutive equation](@entry_id:267976) that governs the model's behavior :
$$
\sigma(t) + \frac{\eta}{E_2} \dot{\sigma}(t) = E_1 \epsilon(t) + \eta \left(1 + \frac{E_1}{E_2}\right) \dot{\epsilon}(t)
$$
This equation links the macroscopic stress $\sigma(t)$ and strain $\epsilon(t)$ and their time rates of change. To analyze the frequency response, we can apply a Fourier transform (letting $d/dt \to i\omega$) to this equation to solve for the [complex modulus](@entry_id:203570) $E^*(\omega) = \sigma(\omega)/\epsilon(\omega)$:
$$
E^*(\omega) = \frac{E_1 + i\omega \eta \left(1 + \frac{E_1}{E_2}\right)}{1 + i\omega \frac{\eta}{E_2}}
$$
This expression can be separated into its real (storage) and imaginary (loss) parts:
$$
E'(\omega) = \frac{E_1 + (\omega \tau_{\epsilon})^2 (E_1 + E_2)}{1 + (\omega \tau_{\epsilon})^2}, \quad E''(\omega) = \frac{\omega \tau_{\epsilon} E_2}{1 + (\omega \tau_{\epsilon})^2}
$$
where we have introduced the **relaxation time** $\tau_{\epsilon} = \eta/E_2$. This parameter represents the characteristic timescale for the Maxwell element to relax stress.

The inverse [quality factor](@entry_id:201005) for the SLS model is then $Q^{-1}(\omega) = E''(\omega)/E'(\omega)$:
$$
Q^{-1}(\omega) = \frac{\omega \tau_{\epsilon} E_2}{E_1 + (\omega \tau_{\epsilon})^2 (E_1 + E_2)}
$$
This function describes a characteristic absorption peak, often called a **Debye peak**. The attenuation is low at very low and very high frequencies and reaches a maximum at an intermediate frequency. This behavior is the hallmark of a single relaxation process. A detailed analysis  reveals that the peak attenuation occurs at an angular frequency $\omega_{peak} = \frac{1}{\tau}\sqrt{E_R/E_U}$, where $E_R = E_1$ is the **relaxed modulus** (at $\omega \to 0$) and $E_U = E_1 + E_2$ is the **unrelaxed modulus** (at $\omega \to \infty$). The magnitude of this peak is $(Q^{-1})_{peak} = \frac{E_U - E_R}{2\sqrt{E_R E_U}}$. The width of the attenuation peak, characterized by its Full Width at Half Maximum (FWHM), is also determined by the material moduli and the [relaxation time](@entry_id:142983). For instance, in one common formulation, the FWHM is given by $\Delta\omega_{1/2} = \frac{2\sqrt{3}}{\tau\sqrt{1+\Delta}}$, where $\Delta = (E_U - E_R)/E_R$ is a dimensionless measure of the material's relaxation strength .

### Generalizing the SLS for Realistic Attenuation Spectra

A single SLS model produces a narrow attenuation peak, which is often a poor match for the observed [seismic attenuation](@entry_id:754635) in rocks, which is typically weak but remarkably constant over many decades of frequency. To overcome this limitation, we can generalize the model by placing multiple Maxwell elements in parallel, each with its own modulus $\Delta E_j$ and relaxation time $\tau_j$. This is known as the **Generalized Standard Linear Solid (GSLS)** or Wiechert model.

The [complex modulus](@entry_id:203570) of a GSLS with $N$ Maxwell elements in parallel with an equilibrium spring of relaxed modulus $E_R$ is found by summing the moduli of the parallel components :
$$
E^*(\omega) = E_R + \sum_{j=1}^N \Delta E_j \frac{i\omega \tau_j}{1 + i\omega \tau_j}
$$
The corresponding storage and loss moduli are:
$$
E'(\omega) = E_R + \sum_{j=1}^N \Delta E_j \frac{(\omega \tau_j)^2}{1 + (\omega \tau_j)^2}
$$
$$
E''(\omega) = \sum_{j=1}^N \Delta E_j \frac{\omega \tau_j}{1 + (\omega \tau_j)^2}
$$
The loss modulus $E''(\omega)$ is a superposition of multiple Debye peaks. By choosing an appropriate distribution of relaxation times $\tau_j$ and weights $\Delta E_j$, it is possible to construct a model where the superposition of these peaks results in an almost-flat [loss modulus](@entry_id:180221) over a wide, band-limited frequency range. If the attenuation is weak (i.e., $\sum \Delta E_j \ll E_R$), the [storage modulus](@entry_id:201147) $E'(\omega)$ is nearly constant and approximately equal to $E_R$. In this case, $Q^{-1}(\omega) \approx E''(\omega)/E_R$ will also be nearly constant over that frequency band. A common and effective strategy is to space the relaxation times $\tau_j$ logarithmically across the desired frequency range .

Outside this band, the GSLS model has characteristic asymptotic behaviors. As frequency approaches zero ($\omega \to 0$), $Q^{-1}(\omega)$ is proportional to $\omega$. As frequency becomes very large ($\omega \to \infty$), $Q^{-1}(\omega)$ is proportional to $1/\omega$. The ability to model nearly constant-$Q$ behavior makes the GSLS a cornerstone of modern attenuation modeling.

The SLS model also serves as a parent to simpler [viscoelastic models](@entry_id:192483). For example, if the parallel spring modulus $E_1$ is set to zero, the SLS reduces to a simple Maxwell model. Conversely, if the spring in the Maxwell element becomes infinitely stiff ($E_2 \to \infty$), the SLS reduces to a **Kelvin-Voigt model** (a spring and dashpot in parallel) . Understanding these limits helps to place the SLS within the broader family of linear viscoelastic responses.

### From Constitutive Model to Wave Propagation

A [constitutive model](@entry_id:747751) like the SLS is not just an abstract description; it has direct consequences for how waves propagate. The link is provided by the equation of motion. For a 1D plane wave, the momentum balance equation is $\rho \frac{\partial^2 u}{\partial t^2} = \frac{\partial \sigma}{\partial x}$. Combining this with the frequency-domain [constitutive relation](@entry_id:268485) $\sigma(\omega) = E^*(\omega) \epsilon(\omega)$ and the strain definition $\epsilon = \partial u / \partial x$, we arrive at the viscoelastic wave equation.

For a [plane wave](@entry_id:263752) of the form $u(x,t) = \hat{u} \exp(i\omega t - ikx)$, this leads to the **[dispersion relation](@entry_id:138513)**, which links the [complex wavenumber](@entry_id:274896) $k$ to the material properties and frequency :
$$
k(\omega) = \omega \sqrt{\frac{\rho}{E^*(\omega)}}
$$
The wavenumber $k$ is complex, $k(\omega) = k_R(\omega) + i k_I(\omega)$. Its real part, $k_R$, determines the **[phase velocity](@entry_id:154045)** of the wave, $v_p(\omega) = \omega / k_R(\omega)$. Its imaginary part, $k_I$, is the **attenuation coefficient**, which governs the [exponential decay](@entry_id:136762) of the wave's amplitude with distance, as $\exp(-k_I x)$.

A key consequence of a frequency-dependent [complex modulus](@entry_id:203570) is that the phase velocity must also be frequency-dependent. This phenomenon is called **velocity dispersion**. A material that attenuates waves must, by causality, also be dispersive. For example, in an SLS material, a plane shear wave with a frequency of $f=20\,\mathrm{Hz}$ might propagate at a phase velocity of $2315\,\mathrm{m/s}$, a value determined by the complex [shear modulus](@entry_id:167228) at that specific frequency .

In a 3D isotropic medium, the viscoelastic response is described by a complex bulk modulus $K^*(\omega)$ and a complex shear modulus $G^*(\omega)$. The two fundamental wave types, compressional (P) and shear (S) waves, are governed by different combinations of these moduli .
-   **S-waves** are purely distortional and are governed by the complex [shear modulus](@entry_id:167228), $G^*(\omega)$. Their [quality factor](@entry_id:201005) is $Q_S^{-1}(\omega) = G''(\omega)/G'(\omega)$.
-   **P-waves** involve both volumetric change and distortion. They are governed by the complex P-wave modulus, $M_P^*(\omega) = K^*(\omega) + \frac{4}{3}G^*(\omega)$. Their [quality factor](@entry_id:201005) is therefore a combination of both bulk and shear attenuation mechanisms:
    $$
    Q_P^{-1}(\omega) = \frac{\operatorname{Im}[M_P^*(\omega)]}{\operatorname{Re}[M_P^*(\omega)]} = \frac{K''(\omega) + \frac{4}{3}G''(\omega)}{K'(\omega) + \frac{4}{3}G'(\omega)}
    $$
This shows that even in an isotropic medium, $Q_P$ and $Q_S$ are generally different and depend on how energy is partitioned between compression and shear for each wave type.

### Computational Framework: Memory Variables for Time-Domain Simulation

While frequency-domain analysis is powerful for understanding principles, [seismic modeling](@entry_id:754642) is often performed in the time domain (e.g., using [finite-difference](@entry_id:749360) or finite-element methods). The stress-strain relation in the time domain is given by the **Boltzmann superposition principle**, a [convolution integral](@entry_id:155865):
$$
\sigma(t) = \int_{0}^{t} E(t-s) \frac{d\epsilon}{ds}(s) ds
$$
where $E(t)$ is the time-domain **[relaxation modulus](@entry_id:189592)**. For a GSLS model, the [relaxation modulus](@entry_id:189592) has the form :
$$
E(t) = E_R + \sum_{j=1}^N \Delta E_j \exp(-t/\tau_j)
$$
Directly evaluating the convolution integral at every time step is computationally prohibitive, as it requires storing the entire strain history. The GSLS formulation provides an elegant solution. By substituting the GSLS [relaxation modulus](@entry_id:189592) into the [convolution integral](@entry_id:155865), the stress can be rewritten as :
$$
\sigma(t) = E_R \epsilon(t) + \sum_{j=1}^N q_j(t)
$$
Here, we have introduced a set of **memory variables**, $q_j(t)$, each defined by a convolution with one of the exponential relaxation terms. A key insight is that each memory variable obeys a local, first-order ordinary differential equation (ODE):
$$
\frac{dq_j}{dt} = -\frac{1}{\tau_j} q_j(t) + \Delta E_j \frac{d\epsilon}{dt}
$$
This transforms the computationally expensive, non-local convolution into a set of local, inexpensive ODEs that can be marched forward in time along with the wave equation. For a numerical time step of size $\Delta t$, assuming the strain rate is constant within the step, this ODE has an exact analytical solution. The updated memory variable $q_j^{n+1}$ at time $t_{n+1}$ can be expressed in terms of its value at the previous step, $q_j^n$ , :
$$
q_j^{n+1} = q_j^n \exp(-\Delta t / \tau_j) + \Delta E_j \tau_j \left(1 - \exp(-\Delta t/\tau_j)\right) \frac{\epsilon^{n+1} - \epsilon^n}{\Delta t}
$$
The total stress at the new time step is then simply $\sigma^{n+1} = E_R \epsilon^{n+1} + \sum_j q_j^{n+1}$. This memory variable method is the standard and most efficient technique for implementing viscoelastic effects in time-domain [wave propagation](@entry_id:144063) codes.

### A Physical Basis for Relaxation: The Example of Squirt Flow

The SLS model and its generalizations, while powerful, are phenomenological. However, their parameters can be linked to specific physical processes in rocks. One of the most important mechanisms for attenuation in fluid-saturated rocks is **squirt flow**. This process involves the pressure-induced flow of pore fluid between cracks and pores of differing aspect ratios and orientations.

Consider a rock with an ensemble of microcracks. When a seismic wave passes, it compresses some cracks and tenses others, creating pressure gradients between the cracks and the more equant background pore space. This drives fluid to flow, or "squirt," between them. The [fluid viscosity](@entry_id:261198) resists this flow, causing a phase lag and dissipating energy. Each crack, with its specific compliance and connection to the pore network, acts as a tiny relaxation mechanism.

One can model this process by relating the relaxation time $\tau$ of a crack to the [fluid viscosity](@entry_id:261198) $\eta$ and the crack's mechanical compliance $S$. A first-principles derivation shows that the [relaxation time](@entry_id:142983) scales as $\tau \propto \eta S$ . A real rock contains a vast distribution of cracks with varying shapes and sizes, and therefore a distribution of compliances. If we model this with, for example, a [lognormal distribution](@entry_id:261888) of crack compliances, the rock's macroscopic response becomes an integral over all these individual relaxation mechanisms. This naturally leads to a model with a continuous distribution of relaxation times, which is precisely what the GSLS model aims to approximate. By matching the response of the microscopic model to that of an effective SLS model, one can derive expressions for the effective SLS parameters. For instance, the effective relaxation time for an ensemble of cracks with a lognormal compliance distribution can be shown to be $\tau_{\text{eff}} = \alpha \eta \exp(\mu + \frac{3}{2}\sigma^2)$, where $\mu$ and $\sigma^2$ are the mean and variance of the log-compliance distribution . This provides a concrete physical grounding for the abstract parameters of the SLS model, connecting them directly to rock texture and [fluid properties](@entry_id:200256).