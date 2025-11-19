## Introduction
Diamagnetism, a subtle yet [universal property](@entry_id:145831) of matter, manifests as a weak repulsive force in the presence of a magnetic field. While often eclipsed by the more powerful effects of [paramagnetism](@entry_id:139883) and [ferromagnetism](@entry_id:137256), understanding diamagnetism is crucial as it reveals the deep quantum mechanical underpinnings of how materials interact with magnetic fields. This article demystifies this phenomenon, addressing the gap between its universal presence and its often-underappreciated significance.

Across the following chapters, you will embark on a comprehensive exploration of diamagnetism. First, in **Principles and Mechanisms**, we will establish the core concepts, from the macroscopic definition of negative [magnetic susceptibility](@entry_id:138219) to the microscopic origins rooted in Lenz's law and electron [orbital motion](@entry_id:162856). We will also confront the classical paradoxes that necessitate a quantum mechanical explanation. Next, in **Applications and Interdisciplinary Connections**, we will witness these principles in action, exploring everything from the captivating spectacle of magnetic levitation and the [perfect diamagnetism](@entry_id:203008) of superconductors to its vital role in plasma physics and as a diagnostic tool in chemistry. Finally, **Hands-On Practices** will offer a chance to apply these concepts to solve practical problems, solidifying your understanding of how diamagnetism is quantified and observed. This journey will provide a robust framework for understanding one of electromagnetism's most [fundamental interactions](@entry_id:749649).

## Principles and Mechanisms

Having established the fundamental concepts of magnetic fields and their interaction with matter, we now turn our attention to a specific class of magnetic response: diamagnetism. While often overshadowed by the stronger effects of [paramagnetism](@entry_id:139883) and [ferromagnetism](@entry_id:137256), diamagnetism is a universal phenomenon, present in all materials. It offers a profound insight into the quantum nature of matter and the fundamental laws of electromagnetism. In this chapter, we will explore the principles that govern diamagnetism, from its macroscopic manifestations to its microscopic origins.

### Macroscopic Description and Magnetic Susceptibility

The response of a material to an external magnetic field is quantified by its **magnetization**, $\mathbf{M}$, defined as the [magnetic dipole moment](@entry_id:149826) per unit volume. For a large class of materials, including diamagnets, the induced magnetization is directly proportional to the [magnetic field intensity](@entry_id:197932), $\mathbf{H}$. This linear relationship is expressed through a dimensionless constant called the **magnetic susceptibility**, $\chi_m$:

$$
\mathbf{M} = \chi_m \mathbf{H}
$$

The [magnetic susceptibility](@entry_id:138219) is the primary figure of merit that defines a material's magnetic character. Diamagnetism is uniquely characterized by a **negative [magnetic susceptibility](@entry_id:138219)** ($\chi_m  0$). This negative sign is not merely a mathematical convention; it signifies the fundamental nature of the diamagnetic response: the induced magnetization opposes the applied magnetic field.

Consequently, the total [magnetic flux density](@entry_id:194922) $\mathbf{B}$ inside a diamagnetic material is slightly reduced compared to the field in a vacuum. The relationship between these fields is given by:

$$
\mathbf{B} = \mu_0 (\mathbf{H} + \mathbf{M}) = \mu_0 (1 + \chi_m) \mathbf{H} = \mu_r \mu_0 \mathbf{H}
$$

where $\mu_0$ is the [permeability of free space](@entry_id:276113) and $\mu_r = 1 + \chi_m$ is the **[relative permeability](@entry_id:272081)**. Since $\chi_m  0$ for a diamagnet, its [relative permeability](@entry_id:272081) is always less than one. However, the effect is typically very weak. For most [diamagnetic materials](@entry_id:264470), the magnitude of $\chi_m$ is on the order of $10^{-6}$ to $10^{-5}$. For example, a common diamagnetic material like water might have $\chi_{m} \approx -9.7 \times 10^{-6}$, whereas a weakly paramagnetic material might have $\chi_{m} \approx +1.2 \times 10^{-5}$ [@problem_id:1805618].

To illustrate the weakness of this effect, consider a diamagnetic material with $\chi_m = -1.66 \times 10^{-4}$ placed in a very strong external field of $B_0 = 14.5$ T. The magnetization inside the material generates its own opposing magnetic field, $\mathbf{B}_M = \mu_0 \mathbf{M}$. In the approximation that the internal field $\mathbf{H}$ is well-approximated by $\mathbf{B}_0/\mu_0$, the induced field is $\mathbf{B}_M \approx \chi_m \mathbf{B}_0$. The magnitude of this opposing field is then:

$$
|\mathbf{B}_M| \approx |\chi_m| |\mathbf{B}_0| = (1.66 \times 10^{-4})(14.5 \text{ T}) \approx 2.41 \times 10^{-3} \text{ T}
$$

Thus, even in a powerful magnetic field, the internal field is reduced by only a few millitesla, a testament to the subtlety of the diamagnetic response [@problem_id:1792123]. The only materials that exhibit strong diamagnetism are superconductors, which behave as perfect diamagnets with $\chi_m = -1$, completely expelling magnetic fields from their interior.

### The Repulsive Force on Diamagnets

The most dramatic and intuitive manifestation of diamagnetism is the repulsive force exerted on a diamagnetic object by a [non-uniform magnetic field](@entry_id:270628). The origin of this force can be understood by considering the [potential energy of a magnetic dipole](@entry_id:261718) $\mathbf{m}$ in a magnetic field $\mathbf{B}$, which is $U = -\mathbf{m} \cdot \mathbf{B}$. The force is the negative gradient of this potential energy, $\mathbf{F} = -\nabla U = \nabla(\mathbf{m} \cdot \mathbf{B})$.

For a linear, isotropic diamagnetic material, the [induced magnetic moment](@entry_id:184971) $\mathbf{m}$ of a small [volume element](@entry_id:267802) $V$ is given by $\mathbf{m} = \mathbf{M}V = \chi_m V \mathbf{H}$. For non-[ferromagnetic materials](@entry_id:261099), $\mathbf{H} \approx \mathbf{B}/\mu_0$, so we can write $\mathbf{m} \approx \frac{\chi_m V}{\mu_0} \mathbf{B}$. Substituting this into the force expression yields:

$$
\mathbf{F} = \nabla\left( \left(\frac{\chi_m V}{\mu_0} \mathbf{B}\right) \cdot \mathbf{B} \right) = \frac{\chi_m V}{\mu_0} \nabla(B^2)
$$

This equation is key to understanding the mechanical behavior of diamagnets. Since $\chi_m$ is negative, the force vector $\mathbf{F}$ points in the direction opposite to the gradient of $B^2$. In other words, **a diamagnetic object is always pushed from a region of stronger magnetic field to a region of weaker magnetic field** [@problem_id:1792084].

This repulsive force is responsible for the remarkable phenomenon of **magnetic levitation**. If a sufficiently strong magnetic field with a large gradient is produced, the upward magnetic force on a diamagnetic object can counteract the downward force of gravity, allowing it to levitate. For instance, a small disk of a diamagnetic material can be made to float at a stable equilibrium height above a strong permanent magnet [@problem_id:1792110]. At this height, the upward magnetic force precisely balances the object's weight, $mg$. This principle is famously demonstrated with materials like pyrolytic graphite and bismuth, which are among the strongest known room-temperature diamagnets.

### The Microscopic Origin: Langevin Diamagnetism

To understand *why* materials exhibit this repulsive behavior, we must descend to the atomic scale. The fundamental origin of diamagnetism lies in the effect of an external magnetic field on the orbital motion of electrons, a consequence of Faraday's law of induction.

A helpful macroscopic analogue is a simple conducting ring [@problem_id:1792101]. If a magnetic field passing through the ring increases with time, the changing magnetic flux induces an electromotive force (EMF), $\mathcal{E} = -d\Phi_B/dt$. This EMF drives a current in the ring. According to **Lenz's Law**, the direction of this [induced current](@entry_id:270047) is such that it creates its own magnetic field that opposes the change in flux. The [magnetic dipole moment](@entry_id:149826) associated with this [induced current](@entry_id:270047) is therefore directed opposite to the applied field—a classic diamagnetic response.

The same principle applies to the electrons orbiting the nucleus of an atom. Let us model an atom with a single electron of charge $-e$ and mass $m_e$ in a [circular orbit](@entry_id:173723) of radius $r$ [@problem_id:1574856]. When an external magnetic field $\mathbf{B}$ is slowly applied perpendicular to the orbital plane, the magnetic flux through the orbit changes. By Faraday's law, this induces a tangential electric field $\mathbf{E}$ that encircles the nucleus. This [induced electric field](@entry_id:267314) exerts a torque ($\mathbf{\tau} = \mathbf{r} \times (-e\mathbf{E})$) on the electron.

This torque changes the electron's [orbital angular momentum](@entry_id:191303) $\mathbf{L}$. The change in magnetic moment, $\Delta\mathbf{\mu}$, is related to the change in angular momentum by $\Delta\mathbf{\mu} = (-e/2m_e)\Delta\mathbf{L}$. A careful derivation shows that the change in the magnetic moment's component along the field is:

$$
\Delta\mu_z = -\frac{e^2 r^2}{4 m_e} B_z
$$

This result reveals two crucial facts. First, the negative sign confirms that the induced moment always opposes the applied field, consistent with Lenz's law. Second, the result is independent of the electron's initial velocity or direction of orbit. It depends only on [fundamental constants](@entry_id:148774), the charge's orbital radius, and the strength of the applied field.

Because this effect applies to every electron, all atoms exhibit a diamagnetic response. For atoms with completely filled [electron shells](@entry_id:270981), such as [noble gases](@entry_id:141583) [@problem_id:1792081] or ions in many salts, the vector sum of the individual electron orbital and spin angular momenta is zero. Such atoms have no permanent magnetic moment, and their only response to a magnetic field is this weak, induced diamagnetism. If an atom has unpaired electrons, it will possess a permanent magnetic moment, leading to paramagnetism. In such cases, the [paramagnetic alignment](@entry_id:753147) with the field is a much stronger effect, and it typically overwhelms the ever-present but weaker diamagnetic repulsion [@problem_id:1792088].

### From Atomic Response to Macroscopic Susceptibility

The link between the microscopic induced moment and the macroscopic magnetic susceptibility is straightforward. For an atom with $Z$ electrons, we can sum the contributions from each, leading to the **Langevin formula** for the induced atomic moment:

$$
\mu_{ind} = -\frac{Z e^2 \langle r^2 \rangle}{6 m_e} B
$$

Here, $\langle r^2 \rangle$ is the [mean square radius](@entry_id:146552) of the electron orbits, and the factor of $1/6$ arises from averaging over all possible spatial orientations of the orbits relative to the field.

The bulk magnetization $M$ is the induced moment per atom multiplied by the number of atoms per unit volume, $n$. Thus, $M = n \mu_{ind}$. Using the definition $\chi_m \approx \mu_0 M/B$ for weak fields, we arrive at the expression for the Langevin [diamagnetic susceptibility](@entry_id:136270):

$$
\chi_m = -\frac{\mu_0 n Z e^2 \langle r^2 \rangle}{6 m_e}
$$

This formula successfully predicts the negative sign of the susceptibility and its correct order of magnitude. For example, for a noble gas at STP, one can calculate the number density $n$ and use the known atomic parameters to find a small, negative value for $\chi_m$, in excellent agreement with experimental measurements [@problem_id:1792081]. Notably, this expression for $\chi_m$ is independent of temperature, a key feature that helps distinguish diamagnetism from paramagnetism (which typically follows a $1/T$ Curie law).

### Quantum Mechanical Refinements: Bohr-van Leeuwen and Landau Diamagnetism

The classical model of Langevin diamagnetism, based on applying Faraday's law to pre-existing electron orbits, provides a compelling and quantitatively successful picture. However, a deeper theoretical analysis reveals a significant paradox. The **Bohr-van Leeuwen theorem** states that within the framework of classical statistical mechanics, the net magnetization of any system of charges in thermal equilibrium must be identically zero [@problem_id:1574844]. A rigorous classical calculation that considers all possible paths and velocities of electrons in a thermal ensemble shows that the magnetic effects perfectly cancel out. This profound result implies that magnetism, in all its forms (including diamagnetism), is a fundamentally **quantum mechanical** phenomenon.

So, how does the classical Langevin model give the right answer? It succeeds because it is a dynamic model describing the system's response to *switching on* the field, rather than a model of the final thermal [equilibrium state](@entry_id:270364). The full quantum mechanical treatment of an atom in a magnetic field thankfully recovers the Langevin result for bound electrons, justifying its use.

The necessity of a quantum explanation becomes even more apparent when we consider the behavior of free electrons, such as the conduction electrons in a metal. Classically, these electrons would be expected to have no magnetic response. However, quantum mechanics predicts that they do, a phenomenon known as **Landau diamagnetism** [@problem_id:1786391].

Unlike Langevin diamagnetism, which involves the perturbation of bound atomic orbits, Landau diamagnetism arises from the quantization of the orbital motion of free electrons in a magnetic field. The field forces the electrons into helical paths, and the energy of their motion perpendicular to the field becomes quantized into discrete levels known as **Landau levels**. The population of these quantized energy levels by the electron gas leads to a net magnetic moment that opposes the field. This effect is purely quantum mechanical and has no classical analogue. For a simple [free electron gas](@entry_id:145649), the Landau [diamagnetic susceptibility](@entry_id:136270) is temperature-independent and is exactly $-1/3$ of the Pauli paramagnetic susceptibility (which arises from [electron spin](@entry_id:137016)). This means that while the spin contribution causes metals to be weakly paramagnetic overall, a significant diamagnetic contribution from the electrons' orbital motion is always present.

In summary, diamagnetism is a [universal property](@entry_id:145831) of matter, rooted in the response of electron orbitals to an external magnetic field. While its macroscopic effects are subtle, its study reveals deep connections between classical electromagnetism and the quantum structure of atoms and solids.