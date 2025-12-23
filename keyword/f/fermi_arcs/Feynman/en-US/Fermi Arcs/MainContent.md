## Introduction
In conventional metals, electrons occupy states up to the Fermi energy, forming a boundary known as the Fermi surface, which is invariably a closed loop or surface. This fundamental picture is challenged by the discovery of materials hosting "Fermi arcs"—seemingly impossible electronic states that trace open lines on a material's surface, like a coastline without a coast. This discrepancy raises a profound question: how can such an incomplete boundary exist and what principle protects it? This article delves into the fascinating physics of Fermi arcs, explaining the topological secrets that allow them to defy conventional wisdom.

The following sections will guide you through this topological landscape. In "Principles and Mechanisms," we will explore the deep connection between surface Fermi arcs and the material's bulk properties, introducing the concept of Weyl points as magnetic monopoles in momentum space. Subsequently, "Applications and Interdisciplinary Connections" will reveal how these exotic states are experimentally observed and how they lead to remarkable new physical phenomena and potential technologies, from nonlocal transport to new paradigms in photonics and quantum information.

## Principles and Mechanisms

In the world of metals, the motions of electrons are not entirely chaotic. Their allowed states in [momentum space](@article_id:148442) form a landscape of hills and valleys, and at zero temperature, the electrons fill all available states up to a certain energy level, the **Fermi energy**. The boundary between the filled "lake" of states and the empty "land" of states is called the **Fermi surface**. For any ordinary metal you’ve ever encountered, from the copper in your wires to the aluminum in your soda cans, this boundary is always like a coastline of an island or a continent—it is always a closed loop or a closed surface. It has to be. How could a boundary not be closed?

### A Coastline with No Coast: The Puzzle of the Open Fermi Surface

Now, imagine you are an explorer of the quantum world. You use a powerful technique, Angle-Resolved Photoemission Spectroscopy (ARPES), to map out the "coastline" on the surface of a newly discovered crystal. On one material, you see exactly what you expect: a neat, closed loop. But on another, you see something that seems impossible: the coastline is just a line segment. It starts at one point, runs for a while, and then just... stops. This is a **Fermi arc**.

To check if you are seeing things, you decide to poke at it. You carefully deposit a thin, insulating film over the surfaces of both crystals. When you look again, the closed loop on the first material has vanished, its states washed away by the disturbance. But the open arc on the second material is still there, defiantly shimmering in your detector, albeit slightly shifted.

This little thought experiment, based on real observations, tells us something profound. The Fermi arc is not some fragile, accidental feature of the surface. Its existence is robust, protected by a deep physical principle. The material with the fragile loop is just a trivial metal with an ordinary surface state. The material with the indomitable arc is something new, something topological: a **Weyl semimetal** . The secret to this impossible coastline lies not on the surface, but deep within the bulk of the crystal.

### Monopoles in Momentum Space: The Secret in the Bulk

To understand the Fermi arc, we must venture into the material's bulk electronic structure. Here, we find special points in [momentum space](@article_id:148442) where the band of electron-filled states (the valence band) and the band of empty states (the conduction band) touch. These touching points are called **Weyl points**. They are not just incidental crossings; they are points of immense topological significance.

A Weyl point acts like a **magnetic monopole**, but in the abstract world of [momentum space](@article_id:148442). You know that if you have a magnetic monopole (a hypothetical particle that is just a "north" or "south" pole), lines of magnetic field would emanate from it or converge on it. Similarly, a Weyl point is a source or a sink for a quantity called **Berry curvature**, an "effective magnetic field" that lives in [momentum space](@article_id:148442) and governs the quantum geometry of the electron wavefunctions.

Each Weyl point is assigned a topological charge, an integer called **[chirality](@article_id:143611)** ($\chi$), which is either $+1$ (a source) or $-1$ (a sink). For a simple Weyl node, this charge can be found from its low-energy Hamiltonian, which has the form $H(\mathbf{q}) = v_x q_x \sigma_x + v_y q_y \sigma_y + v_z q_z \sigma_z$. The [chirality](@article_id:143611) is simply given by the sign of the product of the velocities: $\chi = \mathrm{sgn}(v_x v_y v_z)$ .

Just as magnetic monopoles have never been found in isolation, Weyl points obey a strict rule known as the Nielsen-Ninomiya theorem: the total chirality summed over the entire [momentum space](@article_id:148442) must be zero. You cannot have a single source without a sink. Therefore, in any real material, Weyl points must come in pairs (or multiples of pairs) of opposite chirality . It is the existence of these separated "charges" in momentum space that sets the stage for the Fermi arc.

### From Slices to Arcs: The Bulk-Boundary Symphony

The connection between the bulk Weyl points and the surface Fermi arcs is one of the most beautiful examples of the **bulk-boundary correspondence** in physics. Let's see how it works.

Imagine our 3D [momentum space](@article_id:148442) is a stack of 2D parallel slices, like pages in a book. Let's say we have a pair of Weyl points, one with $\chi=+1$ and one with $\chi=-1$, separated along the $k_z$ axis. So, one node is at $k_z = -k_0$ and the other is at $k_z = +k_0$ .

Now, let's pull out one of the 2D slices at a fixed $k_z$ that lies *between* the two nodes (say, $k_z = 0$). This 2D slice "encloses" one of the monopoles but not the other. Just as Gauss's law tells you that a surface enclosing a charge has a net [electric flux](@article_id:265555), our 2D slice of [momentum space](@article_id:148442) enclosing a Weyl point has a net flux of Berry curvature. This net flux is a quantized topological invariant called the **Chern number**, $C$. For any slice with $-k_0  k_z  k_0$, the Chern number is non-zero (e.g., $C(k_z)=1$), while for slices outside this region ($|k_z| > k_0$), the Chern number is zero.

Here comes the magic. It is a fundamental result that a 2D system with a non-zero Chern number is a **[topological insulator](@article_id:136609)**, and it *must* host conducting states at its one-dimensional edges. These are not just any conducting states; they are **[chiral edge states](@article_id:137617)**, meaning electrons can only travel in one direction along the edge—they are like one-way electronic highways.

Now, back in our 3D Weyl semimetal slab, the "edge" of each of these 2D slices is simply the surface of the slab. Therefore, for every single $k_z$ value between $-k_0$ and $+k_0$, our slab's surface must host a chiral state. If we plot the position of these required states in the 2D surface momentum space (spanned by $k_y$ and $k_z$), they trace out a continuous line. This line is precisely the Fermi arc! It exists only for the range of $k_z$ between the Weyl points, and thus it gracefully connects the projection of one Weyl point to the projection of the other . One can even write down a simple model where the energy of the surface state is directly tied to this bulk invariant: $E_s(k_y, k_z) \propto C(k_z)$, beautifully demonstrating this connection .

This picture also resolves the paradox of an "open" coastline. An electron traveling along a Fermi arc on the top surface reaches the end—the projection of a Weyl point. At this point, it can "dive" into the bulk and travel to the other Weyl point, where it can emerge on the *bottom surface* of the slab. On the bottom surface, another Fermi arc will guide it back to the projection of the first Weyl node. The full circuit is complete: top arc, bulk, bottom arc, bulk. The system is perfectly self-contained, and particle number is conserved .

### Life on the Arc: A One-Way Ticket

What is it like to be an electron living on a Fermi arc? It's a strange and wonderful existence, governed by the underlying topology.

First, as we saw, this existence is **robust**. The arc is a consequence of the bulk [topological charge](@article_id:141828), which cannot be changed by small local perturbations on the surface. You can't just wish it away .

Second, these states are truly surface-dwellers. Their wavefunction is peaked at the crystal's boundary and decays exponentially as one goes deeper into the bulk. The characteristic length of this decay is the **penetration depth**  .

Third, these states can exhibit unique [transport properties](@article_id:202636). For a simple, straight Fermi arc, the density of states per unit energy can be a constant, independent of energy . This is highly unusual—in most metals, the density of states varies with energy. This constant density of states implies that the material's thermodynamic response (like its heat capacity) will have a peculiar character.

Finally, the arc carries a "hidden" topological fingerprint. If an electron were to travel from one end of the arc to the other, its quantum mechanical phase would change in a very specific way. The integral of the Berry connection along the arc, a quantity called the **Zak phase**, is quantized to be $\pi$ (modulo $2\pi$) . This is another subtle, yet profound, consequence of a path connecting two points of opposite topological charge.

### A Tale of Two Arcs: When Similarities Deceive

The story of the Fermi arc is a perfect illustration of how topology reshapes our understanding of materials. But nature is ever inventive, and it's worth noting that the term "Fermi arc" has appeared in another, very different, corner of physics: the study of high-temperature copper-oxide [superconductors](@article_id:136316).

In these materials, ARPES experiments also reveal what look like disconnected Fermi arcs in their strange "[pseudogap](@article_id:143261)" phase. However, these arcs are not believed to originate from bulk Weyl points. Instead, they are thought to be remnants of a full Fermi surface that has been partially obliterated by incredibly strong electron-electron repulsive forces—a phenomenon rooted in **Mott physics**. In this picture, the interactions become so strong in certain directions in momentum space that they destroy the electronic states, leaving only the more resilient "nodal" regions as conducting arcs .

So, while they may look similar in an experiment, the Fermi arc of a Weyl semimetal and the Fermi arc of a cuprate are born from vastly different physics: one from the elegant topology of non-interacting bands, the other from the messy, complex brawl of strongly interacting electrons. It serves as a beautiful reminder that in physics, understanding the "why" is just as important as observing the "what". The journey to uncover the principles and mechanisms behind what we see is the true adventure.