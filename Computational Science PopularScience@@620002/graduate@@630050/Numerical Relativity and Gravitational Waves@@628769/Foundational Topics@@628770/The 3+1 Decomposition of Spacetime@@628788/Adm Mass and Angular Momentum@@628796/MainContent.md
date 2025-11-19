## Introduction
How do we define and measure the total mass, spin, and momentum of a vast, self-gravitating system like a galaxy or a pair of orbiting black holes? We cannot place them on a scale; our only access is through the subtle [curvature of spacetime](@entry_id:189480) they induce light-years away. This fundamental challenge in General Relativity is addressed by the Arnowitt-Deser-Misner (ADM) formalism, which provides a rigorous framework for reading the complete "charge sheet" of an [isolated system](@entry_id:142067) from the asymptotic structure of its gravitational field. The ADM quantities are not just mathematical abstractions; they are the [conserved charges](@entry_id:145660) that govern cosmic dynamics, ensuring that energy and momentum are balanced in even the most violent events.

This article provides a comprehensive exploration of ADM mass and angular momentum. First, in **Principles and Mechanisms**, we will unpack the definition of ADM mass as a [surface integral](@entry_id:275394) at infinity, exploring the necessary mathematical conditions, its deep connection to the symmetries of spacetime, and the profound implications of the Positive Mass Theorem. Next, in **Applications and Interdisciplinary Connections**, we will see the formalism in action, from its role as the energy source for gravitational waves to its surprising connections with [black hole thermodynamics](@entry_id:136383) and [analog gravity](@entry_id:160714) systems in condensed matter physics. Finally, the **Hands-On Practices** section provides guided problems to calculate ADM quantities for fundamental spacetimes, bridging the gap between abstract theory and practical application.

## Principles and Mechanisms

How would you weigh a star, a galaxy, or even a pair of merging black holes? You can't put them on a scale. You are infinitely far away, and all you can "feel" is the faint gravitational pull they exert on the very fabric of spacetime. The challenge, then, is to read the total mass, momentum, and spin of an entire [isolated system](@entry_id:142067) from these subtle whispers in the geometry of the cosmos. This is the question that the Arnowitt-Deser-Misner (ADM) formalism elegantly answers.

### What is the Mass of a Universe?

Let's start with a familiar idea from electromagnetism: Gauss's Law. If you want to know the total electric charge inside a closed box, you don't need to count every single electron. You can simply measure the electric field poking through the surface of the box. The total flux of the field through the surface gives you the total charge inside. It's a beautiful, powerful idea that connects a property of the *bulk* (the total charge) to a measurement on the *boundary*.

The ADM mass is the gravitational analog of this very principle. In General Relativity, the "field" is the geometry of spacetime itself, described by the metric tensor $g_{\mu\nu}$. For an [isolated system](@entry_id:142067) like a star or galaxy, we expect spacetime to become flat far away from the source. We call such a spacetime **asymptotically flat**. However, it doesn't become perfectly flat instantly; it carries a memory of the mass it contains. The ADM formalism tells us how to measure this memory.

Imagine a snapshot of our universe at a single moment in time—a three-dimensional "slice" of spacetime denoted $\Sigma$. On this slice, the spatial metric is $\gamma_{ij}$. If spacetime were perfectly flat, this would just be the Euclidean metric $\delta_{ij}$. The presence of mass and energy warps it, so we write $\gamma_{ij} = \delta_{ij} + h_{ij}$, where $h_{ij}$ is the tiny deviation from flatness. The ADM mass is then defined as a surface integral over an infinitely large sphere $S_{\infty}$ at the edge of this slice:

$$
M_{\text{ADM}} = \frac{1}{16\pi} \oint_{S_\infty} (\partial_j h_{ij} - \partial_i h) dS^i
$$

where $h$ is the trace of $h_{ij}$ and $dS^i$ is the surface element. Look at the integrand: it involves derivatives of the [metric perturbation](@entry_id:157898), $\partial h$. This is our "gravitational field." Just like Gauss's law, we are calculating the "flux" of this gravitational field through an infinite sphere to find the total "gravitational charge" inside, which is the mass. By the [divergence theorem](@entry_id:145271), this surface integral is equivalent to a [volume integral](@entry_id:265381) of the field's source over all of space, a fact that is not just a mathematical curiosity but a practical tool for numerical simulations [@problem_id:3463662].

### The Language of Infinity

For this beautiful idea to work, the deviation $h_{ij}$ must vanish as we go to infinity in a very specific way. The [metric perturbation](@entry_id:157898) must fall off like $1/r$, where $r$ is the distance from the source: $h_{ij} \sim O(1/r)$. Its derivatives, which appear in the mass formula, must then fall off like $1/r^2$. The surface area of our sphere grows like $r^2$, so the integral converges to a finite number—the mass! Similarly, the time-varying part of the geometry, encapsulated by the **extrinsic curvature** $K_{ij}$, must fall off even faster, typically as $K_{ij} \sim O(1/r^2)$ [@problem_id:3463649]. This tells us that not only does the geometry become flat at infinity, but it also becomes static.

These [fall-off conditions](@entry_id:157952) are the precise mathematical language of an isolated system. The gravitational field weakens, leaving behind its indelible signature in the leading-order terms of the asymptotic metric.

### A Celestial Symphony: Multipoles of Gravity

The beauty of this description is that the asymptotic gravitational field contains more than just the mass. It encodes all the global properties of the system in a way that is reminiscent of a [multipole expansion](@entry_id:144850) in electromagnetism. The geometry at infinity plays a symphony, and each note corresponds to a fundamental physical quantity [@problem_id:3463682]:

- The **monopole** ($l=0$) part of the [metric perturbation](@entry_id:157898) $h_{ij}$ at order $1/r$ gives the **ADM mass**. This is the dominant, spherically symmetric part of the gravitational field, the one Newton would recognize.

- The **dipole** ($l=1$) part of the [extrinsic curvature](@entry_id:160405) $K_{ij}$ at order $1/r^2$ gives the **ADM linear momentum**. It tells us if the system as a whole is moving.

- The **dipole** ($l=1$) part of the *next* order term in $K_{ij}$, at order $1/r^3$, gives the **ADM angular momentum**. This describes the system's overall rotation, or spin.

- The **dipole** ($l=1$) part of the *next* order term in $h_{ij}$, at order $1/r^2$, gives the **center of mass**, telling us where the system is "centered."

Thus, by carefully decomposing the shape of spacetime at infinity, we can read off a complete manifest of the [isolated system](@entry_id:142067): its mass, its motion, its spin, and its location.

### The Subtle Dance of Parity and Spin

Defining angular momentum reveals a wonderful subtlety. A naive calculation of the integral for angular momentum, which involves a "[lever arm](@entry_id:162693)" factor of $r$, appears to diverge [@problem_id:3463659]. The resolution lies in a deeper symmetry of the fields: **parity**. The laws of physics shouldn't depend on whether we use a left-handed or right-handed coordinate system. This seemingly simple requirement imposes powerful constraints on the asymptotic fields.

For the ADM quantities to be well-defined and independent of our choice of origin, the different parts of the asymptotic fields must have specific parity—they must be either even or odd under inversion through the origin ($\vec{x} \mapsto -\vec{x}$). The mathematics, guided by the physics, demands that [@problem_id:3463649]:
- The leading $O(1/r)$ term in the [metric perturbation](@entry_id:157898) $h_{ij}$ must be **even**. This ensures the ADM mass is well-defined.
- The leading $O(1/r^2)$ term in the [extrinsic curvature](@entry_id:160405) $K_{ij}$ must be **odd**. This ensures the ADM [linear momentum](@entry_id:174467) is well-defined and, miraculously, it makes the divergent part of the angular momentum integral vanish, leaving a finite, physical answer.

This isn't just a mathematical trick; it's a profound statement about the structure of gravity. The universe conspires through these subtle symmetries to give us the finite, [conserved quantities](@entry_id:148503) we expect.

### The Poetry of Symmetry: Why these Charges Exist

Where do these conserved quantities ultimately come from? The deepest answer in physics, courtesy of Noether's theorem, is that they are born from symmetries. For an [isolated system](@entry_id:142067) in flat spacetime, the fundamental symmetries are those of the **Poincaré group**: translations in time and space, rotations, and boosts.

One might expect the asymptotic [symmetry group](@entry_id:138562) of General Relativity to be exactly the Poincaré group. However, physicists discovered that the group of symmetries preserving the asymptotic structure is actually much larger—an infinite-dimensional group sometimes called the Spi group, which includes "[supertranslations](@entry_id:755663)" [@problem_id:34716]. This was a potential disaster, suggesting an infinite number of conserved quantities and a breakdown of our physical intuition.

The resolution, proposed by Tullio Regge and Claudio Teitelboim, is one of the most elegant stories in theoretical physics. They showed that the very same **parity conditions** required to make the angular momentum finite do something even more magical: they act as a filter. On a phase space of [gravitational fields](@entry_id:191301) satisfying these parity conditions, the generators for all the unphysical "[supertranslations](@entry_id:755663)" become ill-defined. The only symmetry generators that survive and produce well-behaved, [conserved charges](@entry_id:145660) are precisely the 10 generators of the Poincaré group! The ADM mass, momentum, and angular momentum are nothing less than the canonical charges associated with the [fundamental symmetries](@entry_id:161256) of spacetime.

### Gravity's Absolute Law: The Positive Mass Theorem

We have a beautiful mathematical definition of mass. But is it *physical*? Does it behave as we expect mass to behave? The answer is a resounding yes, cemented by one of the most profound results in all of General Relativity: the **Positive Mass Theorem** [@problem_id:34654].

The theorem states that for any physical system satisfying the **Dominant Energy Condition** (a reasonable condition stating that energy cannot flow [faster than light](@entry_id:182259)), the ADM mass is always non-negative: $M_{\text{ADM}} \ge 0$. There is no such thing as a "negative mass" object that would produce gravitational repulsion. Gravity is always attractive in this global sense.

Furthermore, the theorem includes a **rigidity statement**: the only way for the total mass to be zero is if the spacetime is completely empty and flat—identical to the Minkowski spacetime of special relativity. This establishes flat space as the unique, stable ground state of the gravitational field. There is no way to arrange matter and energy to have a total mass of zero.

The proof of this theorem is itself a marvel, showcasing the deep unity of physics. The most famous proof, by Edward Witten, ingeniously uses an equation from quantum [field theory](@entry_id:155241)—the Dirac equation for a spinning electron—to prove this purely classical result about gravity [@problem_id:3463681]. It is a stunning example of how ideas from seemingly disparate fields of physics can come together to reveal a fundamental truth about the universe.

### From the Abstract to the Actual: ADM in Context

The ADM formalism is the bedrock for understanding [isolated systems](@entry_id:159201), but it's important to place it in the wider context of General Relativity.

For spacetimes with special symmetries, like the stationary Kerr black hole, other definitions of mass exist, such as the **Komar mass**. Reassuringly, in the cases where both can be defined, they give the same answer, bolstering our confidence that the ADM definition is the correct generalization to dynamic, asymmetric situations [@problem_id:34644].

Perhaps the most crucial context is the distinction between what happens at **spatial infinity ($i^0$)** versus **[null infinity](@entry_id:159987) ($\mathscr{I}^{+}$)** [@problem_id:34663]. The ADM mass is defined by taking a limit on a spacelike "snapshot" of the universe, approaching the point $i^0$. It is a constant, representing the *total* mass-energy of the system, including all radiation that will ever be emitted. It's a timeless, global quantity.

However, when we observe gravitational waves, we are seeing energy being radiated away *now*. This picture is captured at [null infinity](@entry_id:159987), $\mathscr{I}^{+}$, which is the destination of outgoing light rays. The mass defined here is the **Bondi mass**, and it *decreases* over time as gravitational waves carry energy away. The famous mass-loss formula of Bondi and Sachs precisely quantifies this decrease. The ADM mass can be thought of as the initial Bondi mass before any radiation has escaped.

This distinction is paramount in numerical relativity, where simulations often use **hyperboloidal slices** that extend all the way to [null infinity](@entry_id:159987). On such slices, the ADM formalism doesn't apply; the boundary conditions are all wrong. Instead, physicists use the Bondi formalism to directly compute the outgoing wave signals and the corresponding energy loss [@problem_id:34701]. The ADM mass, calculated from the initial data, serves as a crucial check on the total [energy budget](@entry_id:201027): the final Bondi mass plus the total energy radiated away as gravitational waves must equal the initial ADM mass.

From a simple analogy with Gauss's law, the ADM formalism blossoms into a rich and profound framework, connecting the geometry at infinity to the symmetries of spacetime and the fundamental properties of matter and energy. It is a testament to the deep coherence and beauty of Einstein's theory.