## Introduction
Superconductivity is one of the most remarkable phenomena in [condensed matter](@entry_id:747660) physics, describing a state where a material exhibits [zero electrical resistance](@entry_id:151583) and the active expulsion of magnetic fields. While zero resistance might suggest the behavior of a hypothetical "perfect conductor," this simple classical model fails to capture the full picture, particularly the observed expulsion of magnetic flux known as the Meissner effect. This knowledge gap highlights the need for a more nuanced theoretical description.

This article delves into the London equations, the first successful phenomenological framework that brilliantly accounts for these defining properties of superconductors. By replacing Ohm's law with a new [constitutive relation](@entry_id:268485) based on the inertia of charge carriers, the London theory provides a powerful, intuitive model for understanding the [electrodynamics](@entry_id:158759) of the superconducting state.

Our exploration is structured into three main chapters. We begin with **Principles and Mechanisms**, where we will derive the two London equations and uncover their profound consequences, including the concept of a finite [magnetic penetration depth](@entry_id:140378). Next, in **Applications and Interdisciplinary Connections**, we will see how these principles are harnessed in cutting-edge technologies, from [magnetic shielding](@entry_id:192877) and [microwave engineering](@entry_id:274335) to ultra-sensitive quantum sensors, and explore deep connections to fields like particle physics. Finally, the **Hands-On Practices** section provides an opportunity to solidify your understanding by applying these concepts to practical problems. This journey will equip you with a robust understanding of the London theory and its enduring impact on science and technology.

## Principles and Mechanisms

### The Phenomenon of Perfect Conductivity: The First London Equation

The most striking feature of a superconductor is its complete loss of DC electrical resistance below a critical temperature, $T_c$. At first glance, one might model this behavior by considering a "perfect conductor," a hypothetical material obeying Ohm's Law, $\vec{J} = \sigma \vec{E}$, in the limit where the conductivity $\sigma$ becomes infinite. However, this simple idealization leads to conclusions that are inconsistent with the observed behavior of real superconductors.

Consider the response of a [perfect conductor](@entry_id:273420) versus a superconductor to an applied electric field. If a uniform, constant electric field $\vec{E}_0$ were to be established within a perfect conductor, Ohm's law would predict an instantaneous and infinitely large current density, since $\vec{J} = (\infty) \vec{E}_0$. In contrast, the current in a superconductor does not appear instantaneously. Instead, the charge carriers—known as **superelectrons** or **Cooper pairs**—behave as if they have inertia and move without scattering. Their motion is governed not by a frictional drag force (as in the Drude model, which leads to Ohm's law), but directly by Newton's second law. The electric force $q\vec{E}$ on a charge carrier of mass $m$ and charge $q$ produces an acceleration $\vec{a} = d\vec{v}/dt$.

The supercurrent density, $\vec{J}_s$, is given by $\vec{J}_s = n_s q \vec{v}_s$, where $n_s$ is the [number density](@entry_id:268986) of the superelectrons and $\vec{v}_s$ is their average drift velocity. Taking the time derivative, we find $\partial \vec{J}_s / \partial t = n_s q (\partial \vec{v}_s / \partial t)$. Substituting the acceleration from the [electric force](@entry_id:264587) gives:
$$
\frac{\partial \vec{J}_s}{\partial t} = n_s q \left( \frac{q\vec{E}}{m} \right) = \frac{n_s q^2}{m} \vec{E}
$$
This is the **First London Equation**. It is a fundamental [constitutive relation](@entry_id:268485) for a superconductor, replacing Ohm's law. It states that an electric field causes the supercurrent to increase linearly with time, rather than establishing a steady current proportional to the field. This prediction neatly resolves the paradox of the perfect conductor; applying a constant field $\vec{E}_0$ to an initially current-free superconductor results in a current that ramps up as $\vec{J}_s(t) = (n_s q^2 / m) \vec{E}_0 t$ [@problem_id:1821262].

An immediate and crucial consequence of the first London equation concerns the steady state. If a superconductor carries a steady, time-independent current, then $\partial \vec{J}_s / \partial t = 0$. Since the prefactor $(n_s q^2 / m)$ is a non-zero material constant, the equation demands that the electric field inside the superconductor must be zero: $\vec{E} = \vec{0}$ [@problem_id:1821281]. This is the true meaning of [zero resistance](@entry_id:145222): a steady current can persist indefinitely without any driving electric field and thus without any [energy dissipation](@entry_id:147406) ($P = \vec{J}_s \cdot \vec{E} = 0$).

### The Meissner Effect: A Signature of Superconductivity

While perfect conductivity is a necessary property of a superconductor, it is not sufficient to define it. A material that is merely a perfect conductor would behave differently from a true superconductor when cooled in the presence of a magnetic field. Combining the first London equation with Faraday's law of induction ($\vec{\nabla} \times \vec{E} = -\partial \vec{B} / \partial t$) yields a law of conservation:
$$
\vec{\nabla} \times \vec{E} = \vec{\nabla} \times \left( \frac{m}{n_s q^2} \frac{\partial \vec{J}_s}{\partial t} \right) = \frac{\partial}{\partial t} \left( \vec{\nabla} \times \left( \frac{m}{n_s q^2} \vec{J}_s \right) \right) = -\frac{\partial \vec{B}}{\partial t}
$$
Integrating with respect to time shows that the quantity $\vec{B} + \vec{\nabla} \times (\Lambda \vec{J}_s)$ must be constant in time, where $\Lambda = m/(n_s q^2)$. If a material were a perfect conductor and was cooled below its transition temperature in a constant external magnetic field $\vec{B}_{ext}$, it would have $\vec{J}_s = 0$ and $\vec{B} = \vec{B}_{ext}$ in its normal state. According to this conservation law, upon transitioning to the superconducting state, the final magnetic field inside would remain $\vec{B}_{ext}$, as any change in $\vec{B}$ would require a time-varying current and thus a non-static state [@problem_id:58079]. The magnetic field would be trapped.

Experiments, however, reveal a remarkable phenomenon known as the **Meissner effect**: when a material becomes superconducting, it actively expels nearly all magnetic flux from its interior. This is a true [thermodynamic equilibrium](@entry_id:141660) state, independent of the history of how the state was reached. To account for this, Fritz and Heinz London proposed that the time-constant quantity above must not only be constant but must be identically zero. This postulate gives us the **Second London Equation**:
$$
\vec{\nabla} \times \vec{J}_s = -\frac{n_s q^2}{m} \vec{B} = -\frac{1}{\mu_0 \lambda_L^2} \vec{B}
$$
This equation is an independent statement about the nature of the superconducting state. It asserts that a static magnetic field inside a superconductor is inextricably linked to spatially varying supercurrents. This relation, unlike the first London equation, is what truly distinguishes a superconductor from a hypothetical perfect conductor.

### Magnetic Field Penetration and Screening Currents

The combination of the second London equation and the magnetostatic Maxwell's equation (Ampere's law, $\vec{\nabla} \times \vec{B} = \mu_0 \vec{J}_s$) fully describes the electromagnetic response of a superconductor to a static magnetic field. Let us investigate the consequences of these two relations.

If we assume, for the sake of argument, that a uniform, non-zero magnetic field $\vec{B}_0$ could exist throughout a bulk superconductor, we immediately run into a contradiction. A uniform field has zero curl, so Ampere's law would imply $\vec{\nabla} \times \vec{B}_0 = \mu_0 \vec{J}_s = \vec{0}$, meaning there is no supercurrent. But if $\vec{J}_s = \vec{0}$, the second London equation would demand that $-\frac{n_s q^2}{m} \vec{B}_0 = \vec{\nabla} \times \vec{J}_s = \vec{0}$, which requires $\vec{B}_0 = \vec{0}$. The initial assumption of a non-zero uniform field is therefore physically impossible [@problem_id:1821271]. The magnetic field must be expelled.

To see how this expulsion occurs, we can combine the equations into a single differential equation for $\vec{B}$. Taking the curl of Ampere's law and substituting the second London equation gives:
$$
\vec{\nabla} \times (\vec{\nabla} \times \vec{B}) = \mu_0 (\vec{\nabla} \times \vec{J}_s) = \mu_0 \left( -\frac{n_s q^2}{m} \vec{B} \right)
$$
Using the vector identity $\vec{\nabla} \times (\vec{\nabla} \times \vec{B}) = \vec{\nabla}(\vec{\nabla} \cdot \vec{B}) - \nabla^2 \vec{B}$ and the fact that $\vec{\nabla} \cdot \vec{B} = 0$, we arrive at:
$$
\nabla^2 \vec{B} = \frac{\mu_0 n_s q^2}{m} \vec{B} = \frac{1}{\lambda_L^2} \vec{B}
$$
This equation defines a [characteristic length](@entry_id:265857) scale, the **London penetration depth**, $\lambda_L$:
$$
\lambda_L = \sqrt{\frac{m}{\mu_0 n_s q^2}}
$$
The [penetration depth](@entry_id:136478) represents the distance over which an external magnetic field is attenuated inside a superconductor. For a semi-infinite superconductor occupying the region $x > 0$ with an external field $\vec{B} = B_0 \hat{z}$ for $x \le 0$, the equation for the field inside becomes $d^2B_z/dx^2 = B_z / \lambda_L^2$. The physically acceptable solution, which vanishes deep inside the material ($B \to 0$ as $x \to \infty$), is an [exponential decay](@entry_id:136762):
$$
B(x) = B_0 \exp(-x/\lambda_L)
$$
This [exponential decay](@entry_id:136762) is the mathematical description of the Meissner effect. The field is not expelled perfectly from the surface but penetrates a thin layer. This penetration is supported by screening currents. Using Ampere's law, $\vec{J}_s = (\vec{\nabla} \times \vec{B}) / \mu_0$, we can find the current density that generates this field profile [@problem_id:1821269] [@problem_id:1821300]:
$$
\vec{J}_s(x) = \frac{1}{\mu_0} \vec{\nabla} \times (B_0 \exp(-x/\lambda_L) \hat{z}) = \frac{B_0}{\mu_0 \lambda_L} \exp(-x/\lambda_L) \hat{y}
$$
This result shows that a [surface current](@entry_id:261791), flowing in the y-direction, is induced by the external z-[direction field](@entry_id:171823). This current also decays exponentially into the superconductor with the same characteristic length $\lambda_L$.

Microscopically, the charge carriers are **Cooper pairs**, bound pairs of electrons. Therefore, their charge is $q_s = 2e$ and their mass is $m_s = 2m_e$. If the [number density](@entry_id:268986) of [conduction electrons](@entry_id:145260) in the normal state is $n_e$, then the density of pairs is $n_s = n_e/2$. Substituting these into the formula for $\lambda_L$ gives a remarkable result [@problem_id:1821275]:
$$
\lambda_L = \sqrt{\frac{m_s}{\mu_0 n_s q_s^2}} = \sqrt{\frac{2m_e}{\mu_0 (n_e/2) (2e)^2}} = \sqrt{\frac{2m_e}{\mu_0 (n_e/2) (4e^2)}} = \sqrt{\frac{m_e}{\mu_0 n_e e^2}}
$$
Interestingly, the factors of 2 cancel, and the penetration depth can be calculated using the single-electron parameters. For niobium, with an electron density of $n_e \approx 5.56 \times 10^{28} \text{ m}^{-3}$, this yields a penetration depth $\lambda_L \approx 22.5 \text{ nm}$. To attenuate an external field to 1% of its value requires a thickness of $d = -\lambda_L \ln(0.01) \approx 4.6 \lambda_L$, which for niobium is about $104 \text{ nm}$. This makes superconductors excellent magnetic shields [@problem_id:1821275].

### Further Consequences and Extensions

#### Inductive Response and AC Conductivity

The inertial nature of the superelectrons, codified in the first London equation, implies a unique response to [time-varying fields](@entry_id:180620). If we consider a monochromatic electric field $\vec{E}(t) = \vec{E}_0 e^{-i\omega t}$, the first London equation can be solved for the current density $\vec{J}_s(t)$. Assuming a corresponding time dependence $\vec{J}_s(t) = \vec{J}_0 e^{-i\omega t}$, we have $\partial \vec{J}_s / \partial t = -i\omega \vec{J}_s$. The equation becomes:
$$
-i\omega \vec{J}_s = \frac{n_s q_s^2}{m_s} \vec{E} \quad \implies \quad \vec{J}_s = \left( \frac{i n_s q_s^2}{m_s \omega} \right) \vec{E}
$$
This allows us to define a complex AC conductivity, $\sigma(\omega)$, via the generalized Ohm's law $\vec{J}_s = \sigma(\omega) \vec{E}$. We find [@problem_id:58090]:
$$
\sigma(\omega) = \frac{i n_s q_s^2}{m_s \omega}
$$
The conductivity is purely imaginary and inversely proportional to $\omega$. A purely imaginary conductivity means the current is 90 degrees out of phase with the electric field, which is the defining characteristic of a pure inductor. This confirms that the superelectron gas responds to electric fields not with dissipation, but with pure inertia.

#### Flux Quantization: The Quantum Nature

The London equations provide a successful macroscopic, classical description, but the origin of superconductivity is deeply quantum mechanical. The superconducting state is described by a single, macroscopic [quantum wavefunction](@entry_id:261184), $\Psi(\vec{r})$. A fundamental principle of quantum mechanics is that a wavefunction must be single-valued. If we consider a closed path $C$ (for instance, the circumference of a superconducting ring), the wavefunction must have the same value at the beginning and end of the path. This requirement imposes a powerful constraint on the magnetic flux threading the loop.

The phase of the wavefunction of a charged particle is affected by the magnetic vector potential $\vec{A}$. The condition of single-valuedness leads to the quantization of the total magnetic flux $\Phi$ passing through the ring:
$$
\Phi = \int \vec{B} \cdot d\vec{S} = n \frac{h}{q_s} = n \Phi_0
$$
where $n$ is an integer, $h$ is Planck's constant, and $q_s$ is the charge of the superconducting carriers. Experimental measurements found that the charge $q_s$ is equal to $2e$, providing definitive evidence for electron pairing. The resulting **[magnetic flux quantum](@entry_id:136429)** is $\Phi_0 = h/(2e) \approx 2.068 \times 10^{-15} \text{ Wb}$.

This quantization has direct physical consequences. If a superconducting ring with [self-inductance](@entry_id:265778) $L$ is placed in an external magnetic flux $\Phi_{ext}$, a [persistent supercurrent](@entry_id:276122) $I$ will spontaneously flow in the ring. The total flux is $\Phi = \Phi_{ext} + LI$. The system will choose the integer $n$ that minimizes its [magnetic energy](@entry_id:265074), $U = \frac{1}{2}LI^2$. This occurs when the total flux $n\Phi_0$ is as close as possible to the applied external flux. The [induced current](@entry_id:270047) is therefore [@problem_id:1821297]:
$$
I = \frac{n\Phi_0 - \Phi_{ext}}{L}
$$
where $n$ is the integer closest to $\Phi_{ext}/\Phi_0$. These [persistent currents](@entry_id:146997) are a hallmark of the macroscopic quantum nature of superconductivity.

#### Temperature Dependence and Energetics

The properties of a superconductor are strongly dependent on temperature. The key parameter, the density of superelectrons $n_s$, varies from a maximum value at $T=0$ to zero at the critical temperature $T_c$. Consequently, the London penetration depth, $\lambda_L \propto 1/\sqrt{n_s}$, is also temperature-dependent. It is finite at $T=0$ and diverges as $T \to T_c$. An accurate empirical model for this behavior is given by:
$$
\lambda_L(T) = \frac{\lambda_L(0)}{\sqrt{1 - (T/T_c)^4}}
$$
where $\lambda_L(0)$ is the penetration depth at absolute zero. As the temperature rises, $\lambda_L$ increases, meaning the magnetic field can penetrate further into the superconductor. This also affects the kinetic energy of the screening currents required to expel the field. The total kinetic energy of the screening currents per unit surface area, $\mathcal{E}_K$, is directly proportional to $\lambda_L(T)$. Therefore, as temperature increases from $T=0$ towards $T_c$, the kinetic energy stored in the screening currents also increases [@problem_id:1821288].

### Limitations of the London Theory: The Concept of Coherence

The London theory, for all its successes, is a **local** theory. It assumes that the supercurrent density $\vec{J}_s$ at a point $\vec{r}$ depends only on the [electromagnetic fields](@entry_id:272866) $\vec{E}$ and $\vec{B}$ at that exact same point. This is an approximation. The underlying quantum mechanics, described by the Bardeen-Cooper-Schrieffer (BCS) theory, shows that a Cooper pair is not a point particle. The two electrons in a pair are spatially correlated over a characteristic distance known as the **[coherence length](@entry_id:140689)**, $\xi_0$.

This finite size of the Cooper pair implies that the response of the superconductor must be **non-local**. The current at a point $\vec{r}$ should depend on the fields averaged over a volume of size $\sim \xi_0^3$ around that point. A more general theory developed by Pippard accounts for this non-locality.

The London theory is a good approximation when the penetration depth is much larger than the [coherence length](@entry_id:140689) ($\lambda_L \gg \xi_0$), as the magnetic field varies slowly on the scale of a Cooper pair. In pure superconductors, however, the opposite is often true ($\xi_0 > \lambda_L$), and the London model's predictions, such as a purely exponential decay of the magnetic field, are no longer accurate [@problem_id:1821296]. The ratio of these two fundamental length scales, $\kappa = \lambda_L / \xi_0$, is known as the Ginzburg-Landau parameter and determines whether a superconductor is Type I or Type II, a distinction that governs its behavior in strong magnetic fields and forms the basis for much of modern superconducting technology.