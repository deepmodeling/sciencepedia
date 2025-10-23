## Introduction
For centuries, classical [continuum mechanics](@article_id:154631) has been the bedrock of engineering and physics, providing powerful tools to describe how materials deform. However, this elegant framework encounters a fundamental limit when materials break, treating cracks as mathematical singularities that require separate, complex theories. This gap highlights the need for a more unified approach that can describe both continuous deformation and catastrophic failure within a single set of rules. This article introduces peridynamics, a revolutionary nonlocal theory that meets this challenge. We will first explore the foundational "Principles and Mechanisms" of peridynamics, replacing the classical idea of local stress with a new language of long-range bonds and horizons. Subsequently, in "Applications and Interdisciplinary Connections," we will examine the theory's practical power in modeling fracture, plasticity, and other complex phenomena across various scientific fields.

## Principles and Mechanisms

To truly appreciate the symphony of peridynamics, we must first understand the notes. What are the fundamental principles that set it apart from the classical mechanics we all learn and love? And what are the mechanisms that allow it to describe the world, especially the messy, fractured parts of it, with such elegance? Our journey begins by questioning something so fundamental we often take it for granted: the very nature of force inside a solid object.

### Beyond Contact: A New Philosophy of Force

For centuries, our understanding of how forces travel through materials has been dominated by a powerful and intuitive idea: things push or pull on their immediate neighbors. If you push on one end of a steel bar, that little piece of steel pushes on the next, which pushes on the next, and so on, until the force reaches the other end. This is the philosophy of **local action**, or [contact force](@article_id:164585).

The great French mathematician Augustin-Louis Cauchy took this idea and turned it into a masterpiece of [mathematical physics](@article_id:264909). He imagined making an infinitesimally small, imaginary cut inside a material. What force would one side of the cut exert on the other? He argued that this force could be described by a vector, the **traction**, acting on the surface of the cut. Through a brilliant argument involving a tiny tetrahedron shrinking to a point, Cauchy showed that all a material "knows" at a point can be summarized by a single mathematical object: the **stress tensor**, denoted by $\boldsymbol{\sigma}$. This tensor is a beautiful local machine: you feed it a direction (the orientation of your imaginary cut), and it tells you the force vector acting on that surface. This is the foundation of classical [continuum mechanics](@article_id:154631) [@problem_id:2621544].

But what if this isn't the whole story? What if, like gravity, points inside a material could reach out and interact with each other over a small distance? This is the revolutionary proposition of peridynamics. Instead of just "touching" its immediate neighbors, a point in a material interacts with every other point inside a small "sphere of influence." This sphere is called the **horizon**.

This simple shift in perspective has profound consequences. Suddenly, the elegant idea of a force acting *on a surface* becomes fuzzy. If we make an imaginary cut through a peridynamic body, the total force between the two halves is no longer a surface phenomenon. It's the sum total of all the long-range "bonds" that cross the divide. If you try to shrink your measurement area down to a point, as Cauchy did, you don't converge to a neat, well-defined traction vector. The result you get depends on the entire neighborhood. The classical, local concept of stress, as a pointwise quantity, simply dissolves [@problem_id:2621544]. We need a new language.

### A New Language: Horizons, Bonds, and Stretch

This new language is built on a few core concepts that are wonderfully direct and physical.

#### The Horizon

The most fundamental new character in our story is the **horizon**, a length denoted by $\delta$. It defines the radius of each material point's sphere of influence. Any point within this distance is considered part of the central point's **family**. The horizon is not a mathematical trick or a parameter in a [numerical simulation](@article_id:136593); it is a fundamental, intrinsic length scale of the material itself. It's the scale at which the material ceases to look like a perfectly smooth continuum and reveals its nonlocal character. This intrinsic length scale has a fascinating consequence: the peridynamic equations naturally act as a filter, smoothing out or "smearing" any deformation features that are much smaller than the horizon. It's as if the material has a minimum resolution at which it can perceive the world [@problem_id:2667647].

#### Bonds and Stretch

Within this horizon, every pair of points forms a **bond**. A bond is simply the vector $\boldsymbol{\xi}$ connecting two points in their original, undeformed state. As the material deforms, the points move, and the bond is stretched and rotated. The most important measure of a bond's deformation is its **stretch**, $s$. It’s a simple, dimensionless number: the change in the bond's length divided by its original length. For a bond whose original vector is $\boldsymbol{\xi}$ and whose deformed vector is $\boldsymbol{\xi} + \boldsymbol{\eta}$ (where $\boldsymbol{\eta}$ is the relative displacement of its endpoints), the stretch is:

$$
s = \frac{|\boldsymbol{\xi} + \boldsymbol{\eta}| - |\boldsymbol{\xi}|}{|\boldsymbol{\xi}|}
$$

This definition is purely geometric and makes no assumptions about the size of the deformation. It can be a tiny vibration or a catastrophic tearing apart [@problem_id:2667612]. To get a feel for it, imagine a simple one-dimensional bar undergoing a uniform expansion, described by a displacement $u(x) = \alpha x$. Every single bond in this bar, no matter its length or location, experiences exactly the same stretch: $s = \alpha$. It perfectly mirrors the classical concept of strain in this simple case [@problem_id:2667654].

#### The Power of a Nonlocal View

So why abandon the familiar [stress and strain](@article_id:136880) for this new language of bonds and stretch? The payoff comes when things break. In classical mechanics, a crack is a nightmare. It's a [surface of discontinuity](@article_id:179694) where the displacement field is suddenly broken. The strain and stress are theoretically infinite at the [crack tip](@article_id:182313); the equations of motion break down. To handle cracks, classical theories must be augmented with separate, complex theories of "fracture mechanics."

Peridynamics, however, just smiles. Consider a bond that happens to span a crack. The points on either side have moved far apart, so the bond is simply very, very stretched. The stretch $s$ might be large, but it's a perfectly finite, well-defined number. The mathematical framework doesn't even notice that a "crack" has formed; it just sees bonds stretching. Cracks are not special cases; they are a natural mode of behavior that emerges directly from the fundamental equations [@problem_id:2667608]. This is the profound beauty of the peridynamic approach: it speaks a language in which fracture is not a special event, but a part of the material's everyday grammar.

### How Materials Think: From Simple Springs to a Universal Translator

We have our new kinematic language (stretch), but how does a material respond? What forces arise from these stretched bonds? This is the question of the **constitutive model**—the "personality" of the material.

#### The Simplest Idea: A Universe of Springs

The most straightforward idea is to imagine that every bond is a simple spring. The force in the bond should be proportional to its stretch and should act along the line connecting the two deformed points. This is called a **bond-based model**. The force vector $\mathbf{f}$ for a [single bond](@article_id:188067) is given by a simple, intuitive law:

$$
\mathbf{f} = c(|\boldsymbol{\xi}|) \, s \, \mathbf{e}
$$

Here, $s$ is the bond stretch, $\mathbf{e}$ is the unit vector in the direction of the deformed bond, and $c$ is a "micromodulus" that acts like a spring constant, which can depend on the original [bond length](@article_id:144098) $|\boldsymbol{\xi}|$ [@problem_id:2667588]. This model is beautifully simple. It's a "central force" model, a direct consequence of assuming the interaction energy depends only on the distance between the two points.

However, this beautiful simplicity comes at a cost. A material made purely of central-force springs has a very particular way of responding to being squeezed or sheared. It turns out that this model is locked into predicting a single, fixed value for a crucial material property known as **Poisson's ratio** (in three dimensions, this value is fixed at $\nu = 0.25$). This is like discovering a theory of animals that can only describe giraffes. Nature is far more varied! We need a more general model [@problem_id:2667632].

#### A More Sophisticated View: State-Based Models

To escape this prison of a fixed Poisson's ratio, the force in a single bond must depend on more than just its own stretch. It must be influenced by the collective behavior of all the other bonds in its neighborhood. This is the central idea of **[state-based peridynamics](@article_id:190347)**.

A first step in this direction is the **ordinary state-based model**. Here, the force in a bond is still central (acting along the bond's direction), but its magnitude is determined by two factors: a measure of the overall volume change of the neighborhood (the dilatation), and a measure of the bond's individual contribution to shape change (its deviatoric extension). By giving these two responses independent material parameters, we can decouple the bulk and shear behavior and model any desired Poisson's ratio [@problem_id:2667632].

The most powerful and general idea, however, is the **non-ordinary state-based model**. It acts as a kind of "Rosetta Stone," allowing us to translate the vast knowledge of classical material science into the nonlocal world of peridynamics. The procedure is as ingenious as it is effective [@problem_id:2667661]:

1.  **Observe Locally:** Look at the entire family of deformed bonds in a point's horizon. From this nonlocal information, calculate a single, "best-fit" *local* [deformation gradient tensor](@article_id:149876), $\mathbf{F}$. This is done through a clever weighted-averaging process that uses a mathematical tool called the **shape tensor**, $\mathbf{K}$, which characterizes the geometry of the point's neighborhood [@problem_id:2667651].

2.  **Think Classically:** Take this [deformation gradient](@article_id:163255) $\mathbf{F}$ and plug it into *any* well-established classical constitutive model. Want to model steel? Use a classical steel model. Rubber? Use a classical hyperelastic model. This step computes a classical [stress tensor](@article_id:148479), like the First Piola-Kirchhoff stress $\mathbf{P}$.

3.  **Act Nonlocally:** Translate this classical stress tensor $\mathbf{P}$ back into the peridynamic force state $\mathbf{T}$ that governs the interactions within the horizon. In this framework, the force in a bond is no longer required to be central; it can have components that are perpendicular to the bond, allowing it to capture the complex interplay of forces needed to describe any Poisson's ratio.

This correspondence approach is a triumph of synthesis. It allows peridynamics to retain its fundamental strengths—its nonlocal nature and its ability to handle fracture—while giving it access to the entire, rich library of material models developed over the last two centuries.

### Closing the Circle: The Return to the Classical World

We've built a powerful new theory, but one final, crucial question remains. Does it agree with the old, successful theory where it should? If a material is deforming smoothly, without any cracks or wild behavior, peridynamics must give the same answer as classical mechanics.

It does, and the connection is seamless. As you shrink the peridynamic horizon $\delta$ down to zero (while appropriately scaling the material's micromodulus to keep its macroscopic stiffness constant), the peridynamic [integro-differential equation](@article_id:175007) of motion mathematically transforms, term by term, into the classical differential equation of Cauchy: $\rho \ddot{\mathbf{u}} = \nabla \cdot \boldsymbol{\sigma} + \mathbf{b}$ [@problem_id:526199] [@problem_id:2667647].

This is a profound result. It shows that classical [continuum mechanics](@article_id:154631) is not "wrong," but rather a special, limiting case of the more general peridynamic theory. It's analogous to how Newton's laws of motion emerge as a low-speed limit of Einstein's special relativity. Peridynamics provides a broader, more fundamental stage on which materials can act. On this stage, fracture and damage are not awkward special effects to be added in later, but starring actors who have been part of the play from the very beginning. This is the inherent beauty and unity that this new perspective reveals.