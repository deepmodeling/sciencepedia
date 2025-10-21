## Introduction
In the quantum world of crystalline solids, materials are typically classified as metals, with a sea of electrons available for conduction, or insulators, where a large energy gap forbids electron flow. But what if a material could exist in a state between these two extremes, where the electron-filled valence band and the empty conduction band just touch at discrete, isolated points? This is the fascinating realm of Dirac and Weyl [semimetals](@article_id:151783), a class of [topological materials](@article_id:141629) where electrons behave not as conventional charge carriers, but as emergent massless, relativistic particles akin to those studied in high-energy physics. This article bridges this gap in understanding by exploring the fundamental principles and extraordinary consequences of this unique electronic structure. We will first delve into the "Principles and Mechanisms" governing the existence and stability of these topological nodes. Then, we will explore the "Applications and Interdisciplinary Connections," revealing how these theoretical concepts manifest as observable phenomena with links to cosmology and quantum computing. Finally, "Hands-On Practices" will offer a chance to engage directly with the core calculations that define this field. Our journey begins by peering into the crystal to understand the very nature of this topological touch.

## Principles and Mechanisms

Imagine you could peer into the inner world of a crystal. You wouldn’t just see a static lattice of atoms. You would see a vibrant, bustling universe of electrons, a veritable "particle zoo" teeming with entities that behave in wondrously strange ways. In an ordinary metal, you'd find a great "sea" of electrons filling up energy states, forming a well-defined two-dimensional shoreline in the space of momentum—the familiar **Fermi surface** [@problem_id:1827861]. In an insulator, you'd find a vast energy gap, a forbidden zone that electrons cannot cross, leaving the material inert.

But what if we could design a material where this gap vanishes? Not everywhere, but at discrete, singular points in the three-dimensional landscape of momentum? What if the valence band, full of electrons, could just reach up and touch the empty conduction band? At these touching points, a new world opens up. The electrons behave not like the sluggish particles of an ordinary metal, but like massless, relativistic particles from the world of high-energy physics. This is the realm of **Dirac and Weyl [semimetals](@article_id:151783)**.

### The Simplest Touch: A Weyl Point

Let’s start with the simplest, most robust kind of touching in three dimensions: a **Weyl point**. It is an isolated point in momentum space where two [energy bands](@article_id:146082) meet, not with a gentle kiss, but with a sharp conical point [@problem_id:1827861]. The energy-momentum relationship near this point is perfectly linear, given by an elegant equation:

$$
E(\mathbf{k}) \approx \pm \hbar v_F |\mathbf{k}|
$$

This describes a 3D cone, identical in form to the light cone of a photon in relativity. Out of the complex interactions within a humble crystal, an emergent "relativistic" particle is born! These quasiparticles are called **Weyl fermions**.

This conical meeting has some strange consequences. If you were to create a perfect Weyl semimetal with its Fermi energy precisely at the touching point, the "Fermi surface" would shrink from a vast 2D surface down to a set of zero-dimensional points [@problem_id:1827861]. The number of available electronic states, or the **[density of states](@article_id:147400)**, also behaves oddly, scaling with energy squared ($g(E) \propto E^2$), a stark contrast to the $\sqrt{E}$ dependence in conventional metals [@problem_id:1827865].

The essence of this behavior is captured by a wonderfully simple Hamiltonian, the mathematical description of the system. For two bands touching, the simplest model involves the famous Pauli matrices, $\boldsymbol{\sigma}$:

$$
H(\mathbf{k}) = \hbar (v_x k_x \sigma_x + v_y k_y \sigma_y + v_z k_z \sigma_z)
$$

This tells us that the electron's state near a Weyl point is not just about its energy; it’s described by a two-component object, a kind of internal "spin" that isn't the electron's real spin but an emergent property we call **[pseudospin](@article_id:146559)**. The direction of this pseudospin becomes locked to the direction of the electron's momentum.

### A Topological Twist: The Charge of a Node

Here is where the real magic begins. A Weyl point is not just an [accidental degeneracy](@article_id:141195). It is a profoundly stable object, protected by a deep mathematical principle: **topology**. You can't get rid of a single Weyl point by gently deforming the crystal or the Hamiltonian. Why? Because it carries a "charge."

This isn't an electric charge. It's a topological charge, an integer number that we call **[chirality](@article_id:143611)** ($\chi$). To understand it, let's step back and think about a concept from electromagnetism. An electric charge is a source (or sink) of an electric field. The total flux of the field through a closed surface around the charge gives you the total charge inside—that’s Gauss's law.

Believe it or not, there's a nearly identical concept inside our crystal, but it lives in [momentum space](@article_id:148442). There exists a vector field called the **Berry curvature**, $\boldsymbol{\Omega}(\mathbf{k})$, which acts like a fictitious magnetic field in the world of electron momenta. A Weyl point is a **monopole** of this Berry curvature [@problem_id:1827823, 2870330]. If you calculate the total flux of the Berry curvature through a small sphere surrounding the Weyl point in momentum space, you get an integer, which is its chirality, $\chi = +1$ or $\chi = -1$.

$$
C = \frac{1}{2\pi} \oint_S \boldsymbol{\Omega}(\mathbf{k}) \cdot d\mathbf{S} = \chi
$$

A Weyl point with $\chi=+1$ is a "source" of Berry flux, while one with $\chi=-1$ is a "sink." This integer charge cannot be destroyed by small perturbations. The only way to annihilate a Weyl point is to bring it together with another Weyl point of the opposite chirality, a particle-antiparticle [annihilation](@article_id:158870) in [momentum space](@article_id:148442)! This chirality is fundamentally linked to the "handedness" of the winding of the [pseudospin](@article_id:146559) vector as you move in [momentum space](@article_id:148442) around the node [@problem_id:3024257].

### The Law of the Lattice: No Lone Monopoles

This picture of momentum-space monopoles leads to a powerful and beautiful constraint, a "law of the lattice" known as the **Nielsen-Ninomiya theorem**. It states that in any crystal lattice, the total [chirality](@article_id:143611) of all Weyl points must sum to zero.

$$
\sum_i \chi_i = 0
$$

Why should this be? The reason is as elegant as it is profound. The [momentum space](@article_id:148442) of a crystal, the Brillouin zone, is topologically a torus—a donut shape. It's a closed space with no boundary. If you have a source of flux (a monopole of charge $+1$), the flux lines must flow somewhere. In a closed space, they must eventually end on a sink (a monopole of charge $-1$). You cannot have a net flux flowing out of a space that has no "out." From a more mathematical standpoint, the sum of the charges of these monopoles is related to a global property of the momentum space, its Euler characteristic, which for a torus is zero [@problem_id:3024297].

This means Weyl points must always be created in pairs: a source and a sink, a right-handed particle and a left-handed one. This has a deep connection to the **[chiral anomaly](@article_id:141583)** in particle physics, where the charge of a single [chirality](@article_id:143611) is not conserved, but the total charge is. To maintain overall charge conservation in the crystal, any "pumping" of charge at a node of one chirality must be balanced by an equal and opposite effect at a node of the opposite chirality [@problem_id:1827855, 3024297].

### The Dance of Symmetries: Forging and Splitting Particles

So, we know Weyl points are topological monopoles that must come in pairs. But *when* do they appear? The answer lies in the symmetries of the crystal. The two most important symmetries are **time-reversal (T)**, the idea that physics looks the same if you run the movie backward, and **inversion (P)**, which means the crystal looks the same from point $\mathbf{r}$ as from $-\mathbf{r}$.

Here is the crucial rule: if a material has *both* time-reversal and inversion symmetry, Weyl points are forbidden! The combined symmetry, $PT$, forces every electronic band to be doubly degenerate *at every single point* in momentum space [@problem_id:1827867, 2870328]. A Weyl point, which is a two-fold degeneracy surrounded by non-degenerate regions, cannot exist under this strict condition.

To create a Weyl semimetal, you must break one of these two fundamental symmetries [@problem_id:1827852].
*   Break inversion symmetry (like in a crystal that lacks a center of symmetry), but keep time-reversal.
*   Break time-reversal symmetry (for instance, by making the material magnetic), but keep inversion.

What happens if we stubbornly insist on having both T and P symmetry? Nature is clever. It can still create a band touching, but it has to be more complex. This leads us to the **Dirac point**. A Dirac point is a four-fold-degenerate touching point. The perfect picture of a Dirac point is that it is nothing but **two Weyl points of opposite chirality sitting exactly on top of each other** in [momentum space](@article_id:148442), their degeneracy protected by the combined T and P symmetries [@problem_id:1827867, 2870328, 2870288]. The total topological charge of a Dirac point is $\chi = (+1) + (-1) = 0$, which is why it's "legal" in a system with T and P symmetry [@problem_id:2870328, 2870330].

This provides us with a recipe for "topological alchemy": start with a Dirac semimetal and break one of its protective symmetries!
*   Introduce a perturbation that breaks inversion symmetry. The two constituent Weyl nodes will slide apart in momentum space, separating by a distance proportional to the strength of the perturbation [@problem_id:2870320, 2870338].
*   Apply a magnetic field, which breaks [time-reversal symmetry](@article_id:137600). If the field is strong enough, it can overcome the material's intrinsic energy gap and cause the Dirac point to split into a pair of Weyl points [@problem_id:1827837, 2870337]. The nodes separate in momentum by a distance that depends on the strength of the magnetic field.

### Variations on a Theme: Tilted Cones and Nodal Lines

The universe of [topological semimetals](@article_id:137306) is richer still. The beautiful, upright cones of the Weyl points are an idealization. In real materials, these cones can be tilted by other terms in the Hamiltonian.

If the tilt is gentle, we have a **Type-I Weyl semimetal**, with the point-like Fermi surface we've discussed. But if the tilt is so strong that the cone is tipped over, a new phase of matter emerges: the **Type-II Weyl semimetal** [@problem_id:2870322, 1827843]. In this case, the constant-energy surface at the node energy is no longer a point. Instead, it consists of two open conical surfaces—an electron pocket and a hole pocket—touching at the Weyl node. This means the material has a finite [density of states](@article_id:147400) at the Fermi level, behaving more like a metal. The transition from Type-I to Type-II as the tilt increases is a prime example of a **Lifshitz transition**, a fundamental change in the topology of the Fermi surface [@problem_id:2870322].

Finally, it's worth knowing that bands don't have to touch only at points. In some materials, protected by other crystal symmetries, the conduction and valence bands can be degenerate along a continuous one-dimensional curve, forming a **Nodal-Line Semimetal** [@problem_id:1827877].

From simple band touching, a rich and beautiful structure emerges, governed by the interplay of topology and symmetry. These are not just mathematical curiosities. The properties we've discussed—the chiral monopoles, their enforced pairing, and their birth from symmetry breaking—lead to extraordinary physical phenomena, like the famed **Fermi arcs**, which we will explore in the next chapter.