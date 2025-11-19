## Introduction
How do materials break? For centuries, classical [continuum mechanics](@article_id:154631), with its [smooth functions](@article_id:138448) and differential equations, has struggled to answer this fundamental question. At the tip of a crack, where displacements are discontinuous, its mathematics falters, requiring complex add-ons from fracture mechanics to predict failure. What if there was a better way—a theory that embraces [discontinuity](@article_id:143614) as a natural part of its framework?

Enter [peridynamics](@article_id:191297), a revolutionary nonlocal theory that reimagines materials as a collection of points interacting through a network of bonds. By replacing differential equations with integral ones, [peridynamics](@article_id:191297) can model the initiation and growth of complex crack patterns without special treatment, allowing failure to emerge naturally from the system's fundamental laws.

This article will guide you through the elegant core of this theory. The first chapter, "Principles and Mechanisms," will unpack the foundational concepts of the horizon, bonds, and how microscopic interactions give rise to macroscopic behavior. Subsequently, "Applications and Interdisciplinary Connections" will explore the profound impact of this perspective, from autonomous [fracture simulation](@article_id:198575) and [wave dispersion](@article_id:179736) to [multiphysics](@article_id:163984) problems like [thermal shock](@article_id:157835) and [viscoelasticity](@article_id:147551).

## Principles and Mechanisms

Forget for a moment the smooth, continuous world of classical physics, where materials are like infinitely divisible jellies described by differential equations. Let's try a different picture, a view closer to the atomic reality of things, but with a wonderfully simplifying twist. Imagine that a solid object—a steel beam, a pane of glass, a rubber ball—is not a continuous whole, but a colossal collection of material points, like stars in a galaxy. Each point interacts with its neighbors not just by touching, but through "bonds" that reach across the empty space between them. This is the foundational idea of [peridynamics](@article_id:191297). It’s a return to a kind of atomism, but one where we don’t need to know the messy details of every single atom.

### The Horizon and the Bond: A Nonlocal Universe

In classical mechanics, a point in a material only "knows" about its immediate, infinitesimal neighbors. All interactions are local. Peridynamics boldly discards this. It proposes that every material point feels forces from all other points within a certain, finite distance. This region of interaction is called the **horizon**, a sphere of radius $\delta$ centered on our point of interest. This parameter, $\delta$, is not just a computational artifact; it is a fundamental length scale built into the physics of the material itself. It defines the extent of **nonlocality**.

This nonlocal character has profound consequences. Unlike a classical model that is "scale-free," a peridynamic material has an intrinsic sense of size. The behavior of the material is an average over the entire state of the horizon, which means that the theory naturally smoothes out or filters features that are much smaller than $\delta$. It has a built-in resistance to the unruly, singular behavior that plagues classical theories at sharp corners and crack tips [@problem_id:2667647].

The interaction itself is carried by **bonds**, which are conceptual springs connecting pairs of material points. The state of the material is not described by local strain or stress, but by the collective state of all these bonds.

### The Law of the Bond: Simplicity and Symmetry

So, what is the law governing these bonds? Nature often opts for simplicity and elegance. In the simplest form of [peridynamics](@article_id:191297), called **bond-based [peridynamics](@article_id:191297)**, the force in each bond depends *only* on the deformation of that bond alone, independent of its neighbors.

Let's consider a single bond between two points. In its original, undeformed state, it's a vector we can call $\boldsymbol{\xi}$. After the material deforms, the bond becomes a new vector, $\boldsymbol{\xi} + \boldsymbol{\eta}$. The fundamental measure of deformation is the **stretch**, $s$, which is simply the fractional change in the bond's length:
$$
s = \frac{|\boldsymbol{\xi} + \boldsymbol{\eta}| - |\boldsymbol{\xi}|}{|\boldsymbol{\xi}|}
$$
For a simple, linear elastic material, the force in the bond is directly proportional to this stretch. The magnitude of the force is simply $f_{scalar} = c s$, where $c$ is a constant we call the **micromodulus**, representing the stiffness of that particular bond.

But force is a vector. In which direction does it point? For an isotropic material—one that looks and behaves the same in all directions—there is no reason for the force to point anywhere other than straight along the bond itself. If the [bond energy](@article_id:142267) depends only on its length (a scalar), then the force, which is the gradient of that energy, must point in the direction of the greatest change in length—along the deformed bond. This is the definition of a **central force**. The pairwise force vector is thus beautifully simple [@problem_id:2667588]:
$$
\mathbf{f} = c(|\boldsymbol{\xi}|) s \mathbf{e}
$$
where $\mathbf{e}$ is the unit vector along the *deformed* bond. The micromodulus $c$ can depend on the original bond length $|\boldsymbol{\xi}|$, allowing short bonds to be stiffer or weaker than long ones.

### From Microscopic Bonds to Macroscopic Behavior

This is a remarkably simple set of rules for the microscopic world. But does it reproduce the familiar, macroscopic world of elasticity we can measure in the lab? This is where the true beauty of the theory reveals itself.

Let's imagine a simple one-dimensional bar under a uniform strain $\epsilon$. In this case, every single bond in the material experiences the exact same stretch, $s = \epsilon$. We can calculate the total strain energy stored in the material by summing up the energy of every bond. The energy of a single bond turns out to be proportional to $s^2$, just like a classical spring [@problem_id:2667640]. When we integrate this [bond energy](@article_id:142267) over the entire horizon of a point, we get the total peridynamic [strain energy density](@article_id:199591), $W_{PD}$.

For our 1D bar, a straightforward calculation shows this energy density is $W_{PD} = \frac{1}{2}(2c\delta)\epsilon^2$ [@problem_id:2667613]. Now, compare this to the classical formula for elastic energy you learned in freshman physics: $W_{classical} = \frac{1}{2}E\epsilon^2$, where $E$ is Young's modulus. They have the identical form! By simply looking at the two expressions, we see that the macroscopic, measurable Young's modulus is nothing more than an emergent property of the microscopic [bond stiffness](@article_id:272696) and the nonlocal horizon size:
$$
E = 2c\delta
$$
This is a profound result. It bridges the microscopic model with the macroscopic world. The same procedure can be used to relate the micromodulus $c$ to other [elastic constants](@article_id:145713) like the bulk modulus $K$ [@problem_id:2667645] and, in the limit where the horizon shrinks to zero, to recover the full Cauchy [stress tensor](@article_id:148479) of classical elasticity [@problem_id:526199]. Classical elasticity is simply the local limit of a more general, nonlocal theory.

### The Power of Peridynamics: Embracing Discontinuity

If [peridynamics](@article_id:191297) was just another way to derive classical elasticity, it would be a mathematical curiosity. Its real power lies in what it can do that classical mechanics cannot: handle failure.

The equations of classical continuum mechanics are differential equations. They rely on the existence of derivatives of the displacement field. But at the face of a crack, the displacement makes a sudden jump. The derivative is undefined; the mathematics breaks down. To model a crack, classical theories must be augmented with separate, complex criteria known as [fracture mechanics](@article_id:140986).

Peridynamics, however, needs no such additions. Its fundamental equation is an [integral equation](@article_id:164811)—it sums up forces. It doesn't care if the displacement field is smooth or not. A bond connecting two points on opposite sides of a crack simply sees a large relative displacement. The bond stretches, the force is calculated, and the simulation goes on. There are no derivatives to "blow up" [@problem_id:2667608].

The mechanism for fracture is as elegant as the theory itself. We simply add one more rule to our bond law: if a bond's stretch $s$ exceeds a certain material-dependent threshold, the **[critical stretch](@article_id:199690)** $s_c$, the bond breaks. It is permanently removed from the system. As the material is loaded, bonds begin to stretch. The most highly strained bonds reach $s_c$ and snap, releasing their stored energy and transferring load to their neighbors. These neighbors stretch further, and a cascade of breaking bonds can lead to the formation of a macroscopic crack.

And here lies another beautiful micro-macro connection. The macroscopic fracture toughness $G_c$, a property that measures the energy required to create a unit area of new crack surface, can be directly related to the microscopic [critical stretch](@article_id:199690). The energy $G_c$ is simply the sum of all the potential energy stored in the bonds that had to be broken to form that surface. This provides a direct physical link between the breaking strength of the microscopic bonds and the toughness of the bulk material [@problem_id:2905387].

### A Peculiar Limitation and the Path Forward

However, this simple and powerful bond-based model has a fascinating limitation, an "Achilles' heel" that points the way to more advanced theories. When a material is stretched in one direction, it usually contracts in the perpendicular directions. The ratio of this contraction is the Poisson's ratio, $\nu$. Cork has $\nu \approx 0$, while rubber has $\nu \approx 0.5$. These are distinct material properties.

Yet, the simple bond-based model, due to its central-force nature, predicts a fixed Poisson's ratio of $\nu=1/4$ for any [isotropic material](@article_id:204122) in 3D (and $\nu=1/3$ in 2D) [@problem_id:2905415]. The simple bonds aren't "smart" enough to provide independent resistance to volume change and shape change.

This limitation was a key motivator for the development of **[state-based peridynamics](@article_id:190347)**. In these more advanced models, the force in a bond can depend on the deformation of the *entire* neighborhood, not just its own stretch. This allows bonds to "talk" to each other and generate non-[central forces](@article_id:267338), breaking the constraint on Poisson's ratio and enabling the modeling of any material type [@problem_id:2905406].

Even so, the bond-based model, with its elegant simplicity and profound physical insights, remains a cornerstone of the theory and a powerful tool for understanding the fundamental mechanisms of material failure. Through it, we see how the complex and often violent world of fracture can emerge from the simple, local rules of microscopic bonds.