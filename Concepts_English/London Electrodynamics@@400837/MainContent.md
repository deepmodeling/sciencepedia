## Introduction
The discovery of superconductivity presented physics with a profound puzzle. Beyond offering [zero electrical resistance](@article_id:151089), these materials exhibited a bizarre and unexplained behavior: the active expulsion of magnetic fields, a phenomenon known as the Meissner effect. This property proved that superconductors were not merely perfect conductors, but a fundamentally new state of matter requiring a new theoretical framework. The classical laws of electromagnetism were insufficient to explain why a magnetic field was expelled rather than simply trapped.

This article explores the brilliant phenomenological solution proposed by brothers Fritz and Heinz London, a theory now known as London [electrodynamics](@article_id:158265). By supplementing Maxwell's equations with two simple new relations, they provided a powerful model that remains a cornerstone of condensed matter physics. In the following chapters, we will unravel this theory and its far-reaching consequences. The "Principles and Mechanisms" chapter will delve into the London equations themselves, revealing how they give rise to the Meissner effect, define the critical concept of the [magnetic penetration depth](@article_id:139884), and lead to the classification of all [superconductors](@article_id:136316) into two distinct types. Following that, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these foundational principles are applied to measure material properties, drive revolutionary technologies, and connect superconductivity to other fields of science.

## Principles and Mechanisms

Imagine you have a perfect conductor. It offers [zero resistance](@article_id:144728) to the flow of electricity. If you turn on a magnetic field and then cool this material until it becomes a perfect conductor, what happens? Faraday's law of induction tells us that a changing magnetic field creates an electric field. But inside our [perfect conductor](@article_id:272926), an electric field would drive an infinite current, which is unphysical. The only way out is for the electric field to be zero. If the electric field is always zero, Faraday’s law implies that the magnetic field inside can never change: $\frac{\partial \mathbf{B}}{\partial t} = 0$. The material traps whatever magnetic field was present at the moment it became perfect. The magnetic field is frozen in place, a fossil of the conditions of its creation.

For a long time, physicists thought this was how [superconductors](@article_id:136316) behaved. After all, they are perfect conductors. But in 1933, Walther Meissner and Robert Ochsenfeld discovered something utterly astonishing. When they cooled a piece of tin in a magnetic field, the field wasn't trapped. It was actively and completely *expelled* from the material. This phenomenon, the **Meissner effect**, proved that a superconductor is much more than just a perfect conductor. It is a new state of matter with its own unique laws [@problem_id:58079] [@problem_id:3001691]. It doesn’t remember the magnetic field it was born in; it always seeks the same final state of zero internal field. This required a profound leap in understanding, a new theory. That leap was made by two brothers, Fritz and Heinz London.

### The London Equations: A New Electrodynamics

The London brothers proposed two simple, elegant equations that would form the bedrock of our understanding of superconductivity. They didn't replace Maxwell's equations; they supplemented them, providing the missing "constitutive relations" that describe the behavior of the superconducting electrons.

First, let's think about the perfect conductivity. In a normal conductor, an electric field $\mathbf{E}$ drives a steady current $\mathbf{J}$ according to Ohm's law, $\mathbf{J} = \sigma \mathbf{E}$. The electrons drift at a [constant velocity](@article_id:170188), their momentum continuously dissipated by collisions. In a superconductor, there is no dissipation. The charge carriers—a sort of quantum-mechanical fluid of paired electrons—behave like objects in a vacuum. An electric field doesn't cause them to drift at a [constant velocity](@article_id:170188); it causes them to *accelerate*. This is just Newton's second law, $F=ma$, for the superconducting charge carriers. The force is $F = q\mathbf{E}$, and the acceleration is $\frac{\partial \mathbf{v}_s}{\partial t}$. If the carriers have charge $q$ (which we now know is $2e$ for Cooper pairs), mass $m^*$, and [number density](@article_id:268492) $n_s$, the [supercurrent](@article_id:195101) density is $\mathbf{J}_s = n_s q \mathbf{v}_s$. Their acceleration law is therefore:

$$
\frac{\partial \mathbf{J}_s}{\partial t} = \frac{n_s q^2}{m^*} \mathbf{E}
$$

This is the **first London equation** [@problem_id:3009598]. It beautifully captures the essence of zero resistance: a persistent acceleration in response to an electric field. But as we saw, this isn't enough. On its own, it just describes a perfect conductor that would trap magnetic fields. The magic lies in the second equation.

The **second London equation** provides a direct, rigid link between the supercurrent and the magnetic field itself, even in a static situation:

$$
\nabla \times \mathbf{J}_s = -\frac{n_s q^2}{m^*} \mathbf{B}
$$

This equation has no classical analog. It decrees that wherever there is a magnetic field inside a superconductor, there must be a corresponding "curl," or circulation, of the [supercurrent](@article_id:195101). This is the key to the Meissner effect.

### Expulsion of the Field: The Penetration Depth

Let's see how this second equation works its magic. We combine it with Ampere's law from Maxwell's equations (in a static case), $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}_s$. If we take the curl of Ampere's law, we get $\nabla \times (\nabla \times \mathbf{B}) = \mu_0 (\nabla \times \mathbf{J}_s)$. Using a standard vector identity and the fact that $\nabla \cdot \mathbf{B} = 0$, the left side becomes $-\nabla^2 \mathbf{B}$. Now, we substitute the second London equation into the right side:

$$
-\nabla^2 \mathbf{B} = \mu_0 \left( -\frac{n_s q^2}{m^*} \mathbf{B} \right)
$$

Rearranging this gives a remarkable equation governing the magnetic field inside a superconductor [@problem_id:2840850]:

$$
\nabla^2 \mathbf{B} = \frac{\mu_0 n_s q^2}{m^*} \mathbf{B}
$$

Let's define a new quantity, $\lambda_L$, which has units of length, such that $\lambda_L^2 = \frac{m^*}{\mu_0 n_s q^2}$. The equation then becomes wonderfully simple:

$$
\nabla^2 \mathbf{B} = \frac{1}{\lambda_L^2} \mathbf{B}
$$

What does this equation tell us? It says that the "curvature" of the magnetic field (its second derivative, $\nabla^2 \mathbf{B}$) is proportional to the field itself. Functions that behave this way are exponentials. Consider a superconductor occupying the space $x>0$, with a magnetic field $B_0$ applied along the surface. The solution to this equation for $x>0$ is [@problem_id:2840850]:

$$
B(x) = B_0 \exp\left(-\frac{x}{\lambda_L}\right)
$$

The magnetic field is not zero inside the superconductor, but it dies off exponentially as you move in from the surface. The [characteristic length](@article_id:265363) of this decay is the **London [penetration depth](@article_id:135984)**, $\lambda_L$. For most [superconductors](@article_id:136316), this length is tiny—typically tens to hundreds of nanometers. So, for any macroscopic sample, the field is effectively expelled from the bulk, just as Meissner and Ochsenfeld observed. The superconductor is a "perfect diamagnet," but with a thin skin where the magnetic field can penetrate.

This exponential decay is a compromise. The superconductor would ideally like to have no magnetic field inside to minimize its [magnetic energy](@article_id:264580). But to expel the field, it must generate screening currents on its surface. These moving currents carry kinetic energy. The [penetration depth](@article_id:135984) $\lambda_L$ is nature's optimal solution, the perfect balance that minimizes the sum of magnetic and kinetic energy [@problem_id:3001691] [@problem_id:58052].

### Two Kinds of Superconductors: The Role of Coherence

The London model provides a beautiful and powerful picture, but it assumes the properties of the superconductor, like the density of superelectrons $n_s$, are constant. What if they can vary? This question leads us to a richer, more nuanced view.

There is a second fundamental length scale in a superconductor: the **coherence length**, denoted by $\xi$. This is the characteristic distance over which the superconducting state itself can change. You can think of it as the "size" of the Cooper pairs, or the minimum distance required for the material to "heal" back to its full superconducting state if it's perturbed [@problem_id:2840871].

The fate of a superconductor in a magnetic field is determined by the competition between these two length scales. Their ratio is a [dimensionless number](@article_id:260369) of immense importance, the **Ginzburg-Landau parameter**, $\kappa$:

$$
\kappa = \frac{\lambda_L}{\xi}
$$

It turns out that there is a critical value, $\kappa_c = 1/\sqrt{2}$. Depending on which side of this value a material falls, its behavior is dramatically different.

-   **Type I Superconductors**: If $\kappa  1/\sqrt{2}$, it means the [coherence length](@article_id:140195) is large compared to the [penetration depth](@article_id:135984) ($\xi > \lambda_L$). It costs a lot of energy to create a boundary between a normal and a superconducting region. Such a material exhibits an "all-or-nothing" behavior. In a weak magnetic field, it's in the pure Meissner state, expelling all flux. But if you increase the field beyond a single critical value, $H_c$, the entire sample abruptly turns into a normal conductor.

-   **Type II Superconductors**: If $\kappa > 1/\sqrt{2}$, the penetration depth is long compared to the [coherence length](@article_id:140195) ($\lambda_L > \xi$). This means the energy of a normal-superconducting boundary is negative—the system can actually *lower* its energy by creating such interfaces! When the applied field exceeds a lower critical value, $H_{c1}$, the superconductor finds it favorable to let in a bit of magnetic flux. But it doesn't do so uniformly. It allows the field to thread through it in the form of tiny, quantized tornadoes of magnetic flux called **Abrikosov vortices**. Each vortex has a normal-state core (with a radius of about $\xi$) and is surrounded by a whirlpool of supercurrent that screens the field over a distance of about $\lambda_L$ [@problem_id:2869191]. As the external field increases further, more and more vortices cram in, until at a much higher [upper critical field](@article_id:138937), $H_{c2}$, their normal cores overlap and the entire material becomes normal.

### When Locality Fails, and How Dirt Can Help

The London equations are beautiful, but they rely on a hidden assumption: **locality**. They assume the current at a point $\mathbf{r}$ is determined by the fields at that exact same point. But the Cooper pairs that carry the current are not point particles; they have a size, the [coherence length](@article_id:140195) $\xi_0$.

What happens if the magnetic field changes significantly over a distance smaller than a Cooper pair? This occurs in so-called Pippard [superconductors](@article_id:136316), where $\lambda_L  \xi_0$. The Cooper pair can no longer respond to the field at a single point; it effectively "sees" an average of the field over its entire extent. The response becomes **nonlocal**: the current at $\mathbf{r}$ depends on the fields in a whole neighborhood around it. In this regime, the simple London equations break down [@problem_id:3023056] [@problem_id:3009563].

This nonlocality is most pronounced in very pure (clean) Type I [superconductors](@article_id:136316). For Type II [superconductors](@article_id:136316), where $\lambda_L \gg \xi$, the magnetic field varies very slowly on the scale of a Cooper pair. In a wonderful twist of irony, this means the simple, local London theory is often an excellent approximation for describing the more complex physics of Type II materials!

This brings us to our final, and perhaps most surprising, insight. What happens if we take a very pure, clean superconductor and start adding non-magnetic impurities—a bit of "dirt"? Anderson's theorem tells us something remarkable: for [conventional superconductors](@article_id:274753), the critical temperature $T_c$ isn't affected. But the dirt does have a profound effect on the length scales [@problem_id:2869205].

The impurities shorten the distance an electron can travel before scattering. This reduces the effective [coherence length](@article_id:140195), which becomes limited by this [mean free path](@article_id:139069), $\ell$. At the same time, the scattering makes the screening current response less efficient, which *increases* the [penetration depth](@article_id:135984). So, as we add dirt, $\xi$ goes down and $\lambda_L$ goes up. The result? The Ginzburg-Landau parameter, $\kappa = \lambda_L/\xi$, increases dramatically!

This means we can take a pure Type I material, like aluminum, and by making it into a sufficiently "dirty" alloy, we can turn it into a Type II superconductor. This is not just a theoretical curiosity; it's a cornerstone of modern superconducting technology, as most [high-field magnets](@article_id:136389) are made from Type II alloys. And here's the final piece of the beautiful puzzle: by making the effective [coherence length](@article_id:140195) so small, we ensure that the condition for locality ($\lambda_L \gg \xi$) is easily met. In a strange way, adding dirt cleans up the theory, making the elegant, local London equations a more perfect tool than ever to describe the imperfect, real-world materials we use every day [@problem_id:3001701].