## Introduction
How do things break? This simple question poses one of the most profound challenges in engineering and physics. For centuries, classical [continuum mechanics](@article_id:154631) has described the behavior of materials with exquisite precision, but its reliance on differential equations makes it struggle when faced with the abrupt discontinuities of a tear or a crack. A revolutionary alternative, [peridynamics](@article_id:191297), reframes the problem by proposing that the forces at a point depend not on its immediate infinitesimal surroundings, but on interactions within a finite neighborhood. While this nonlocal approach naturally accommodates fracture, its initial formulation, known as [bond-based peridynamics](@article_id:187963), carried a significant limitation: it was locked into predicting a single, fixed material property known as Poisson's ratio, a restriction that failed to capture the behavior of a vast range of real-world materials.

This article explores the evolution beyond this initial model into the more powerful and versatile framework of state-based [peridynamics](@article_id:191297). We will journey through the key conceptual leaps that solved the "Poisson's ratio problem" and opened the door to a new era of [material modeling](@article_id:173180). The first chapter, "Principles and Mechanisms," will dissect the core theory, contrasting the simple "universe of springs" of bond-based models with the collective awareness of state-based formulations, including the elegant correspondence model that builds a bridge to the classical world. Following this, the chapter on "Applications and Interdisciplinary Connections" will showcase how this robust theory is applied to solve tangible problems, from simulating complex failure in metals to designing novel materials from the ground up and enabling large-scale, high-performance computer simulations.

## Principles and Mechanisms

Imagine trying to understand how a vast crowd moves. You could try to write equations for the crowd as a whole, treating it as a continuous fluid. Or, you could look at each individual person, modeling their decisions based on who is immediately next to them. Peridynamics offers a third, fascinating perspective: it suggests that to understand the behavior of any single point, you must consider its relationship with a whole neighborhood of other points, all at once. This is the nonlocal viewpoint, and it has profound consequences.

### A Universe of Springs: The Bond-Based Vision and Its Limits

Let's begin with the simplest, most intuitive picture of a solid material. Imagine it as an enormous, three-dimensional lattice of points, representing atoms or small bits of matter. Now, connect every point to its neighbors with tiny, invisible springs. This is the essence of **[bond-based peridynamics](@article_id:187963)**. The force in any given spring depends only on how much that single spring is stretched or compressed. It doesn't care about what's happening to any other spring; its world is just the two points it connects. This is what we call a **[central force](@article_id:159901)** model—the forces act centrally, along the line connecting the pair of points.

This "universe of springs" is a beautifully simple idea. It's easy to simulate on a computer, and it has a remarkable built-in advantage: if you stretch the material so much that a spring breaks, you've created a crack. You don't need any special equations for fracture; it emerges naturally from the model.

But this simplicity comes at a steep price. Let's think about what happens when you stretch a rubber band. It gets longer, of course, but it also gets thinner. The ratio of how much it thins to how much it lengthens is a fundamental material property called **Poisson's ratio**, denoted by $\nu$. For a very 'squishy' material like rubber, the Poisson's ratio is close to $0.5$. A rigid material might have a smaller value. Cork, famously, has a Poisson's ratio near zero—when you push it into a wine bottle, it doesn't bulge out sideways very much. So, a good theory of materials should let us choose any physically reasonable Poisson's ratio we want.

Here lies the fatal flaw of the simple spring model. When you do the mathematics and average out the behavior of all those independent springs, you find that the material as a whole behaves as if it has a fixed Poisson's ratio. For any isotropic material in three dimensions modeled this way, the theory predicts $\nu$ must be exactly $1/4$ [@problem_id:2905415]. Always. It doesn't matter what kind of springs you use. The bond-based model can't describe rubber, and it can't describe cork. It's a beautiful idea that has hit a wall of physical reality.

### Thinking Collectively: The Dawn of the State

How do we break free from the tyranny of $\nu = 1/4$? The problem, as we've seen, is that each bond acts in isolation. The force in one bond is oblivious to the deformation of its neighbors. Real materials are more sophisticated. The atoms in a crystal, for instance, interact in a way that depends on the angles between bonds, not just their lengths. The material responds collectively.

This is the brilliant conceptual leap that leads us to **state-based [peridynamics](@article_id:191297)** [@problem_id:2905406]. We need to give our material points more information. Instead of just considering the stretch of a single bond, we define two new, more powerful concepts:

*   The **deformation state**: For any given point, we look at its entire family of bonds extending out to a certain distance (the **horizon**). The deformation state, denoted $\underline{\mathbf{Y}}$, is the collection of *all* the new, deformed bond vectors in that family. It’s a complete snapshot of how the entire neighborhood has been warped.

*   The **force state**: Now, the crucial step. The force vector associated with a [single bond](@article_id:188067), $\mathbf{T}\langle\boldsymbol{\xi}\rangle$, is no longer a [simple function](@article_id:160838) of that one bond's stretch. Instead, it becomes a function of the *entire* deformation state $\underline{\mathbf{Y}}$. The force in a bond can now depend on what's happening to all the other bonds in its neighborhood. It has gained a "collective awareness."

This change has a dramatic consequence: the force in a bond no longer has to be parallel to the bond itself. It can have components that are perpendicular, resisting the shearing or twisting of the neighborhood. The spell of the central force is broken.

### Separating Squeeze from Shear: The "Ordinary State-Based" Model

Once we have this collective information from the deformation state, we can start to do some clever things. We can ask, "Overall, is this neighborhood being squeezed (undergoing a volume change) or just being sheared (changing its shape)?"

This is the principle behind the **ordinary state-based (OSB)** model. We can define a single number for each point, called the **dilatation** $\theta$, which is a weighted average of the extensions of all the bonds in its family. This number tells us the overall volume change at that point. We can then look at each individual bond and figure out how much of its stretch contributes to this volume change, and how much is leftover—its **deviatoric extension**, which corresponds to shape change [@problem_id:2667632].

Now, we can build a more sophisticated force law. The force in a bond can have two parts:
1.  A part that resists the overall volume change, proportional to the dilatation $\theta$ and a material property called the **[bulk modulus](@article_id:159575)** ($\kappa$).
2.  A part that resists the shape change, proportional to the bond's own deviatoric extension and a different material property, the **shear modulus** ($\mu$).

The complete force state for a bond $\boldsymbol{\xi}$ can be expressed in a form like this [@problem_id:2667635]:
$$ \mathbf{T}\langle \boldsymbol{\xi} \rangle = \underbrace{\text{force from volume change}(\kappa, \theta)}_\text{Dilatational part} + \underbrace{\text{force from shape change}(\mu, e^d)}_\text{Deviatoric part} $$
Because we now have two independent knobs to tune—the bulk modulus and the shear modulus—we are no longer locked into a fixed relationship between them. We can choose their values to represent any physically possible Poisson's ratio! The "cork problem" is solved. This model is called "ordinary" because the force vector in a bond is still constrained to point along the original bond's direction, but its *magnitude* now depends on the collective state of the neighborhood.

### The Correspondence Principle: A Bridge to the Classical World

The OSB model is a huge step forward, but there is an even more elegant and powerful approach. This is the **nonordinary state-based** model, also known as the **correspondence model**. It's built on a beautifully pragmatic idea: we have over two centuries of experience with classical [continuum mechanics](@article_id:154631). We have incredibly successful models for everything from steel to rubber to soil. What if we could build a peridynamic theory that can leverage all that existing knowledge?

The correspondence model does exactly this by building a bridge between the nonlocal world of [peridynamics](@article_id:191297) and the local world of classical mechanics [@problem_id:2667661]. The process works like this:

1.  **Find the Local Picture**: At a point $\mathbf{x}$, we look at its deformed neighborhood (the deformation state $\underline{\mathbf{Y}}$). We ask: "What is the single best 'classical' deformation, described by a [deformation gradient tensor](@article_id:149876) $\mathbf{F}$, that approximates this entire collection of warped bonds?" This is a bit like fitting a straight plane to a bumpy surface. The answer is found through a weighted [least-squares](@article_id:173422) minimization, which gives us a remarkable formula for this **nonlocal [deformation gradient](@article_id:163255)**:
    $$ \mathbf{F}(\mathbf{x}) = \left( \int_{\mathcal{H}_{\mathbf{x}}} \omega(|\boldsymbol{\xi}|)\\, \mathbf{Y}\langle \boldsymbol{\xi} \rangle \otimes \boldsymbol{\xi}\\, \mathrm{d}V' \right) \mathbf{K}(\mathbf{x})^{-1} $$
    Here, $\omega$ is an [influence function](@article_id:168152) that weights the importance of different bonds, and $\mathbf{K}$ is the crucial **shape tensor**. The shape tensor is a geometric property of the material's reference configuration that accounts for the distribution of material points in the neighborhood [@problem_id:2667627].

2.  **Use a Classical Law**: Once we have the tensor $\mathbf{F}$, we are in the classical world! We can use any time-tested constitutive law we like to calculate a classical [stress tensor](@article_id:148479), for example, the first Piola-Kirchhoff stress $\mathbf{P}$. Do you want to model a linear elastic material? Use Hooke's Law: $\mathbf{P} = \mathbb{C} : (\mathbf{F}-\mathbf{I})$. Want to model rubber? Use a hyperelastic law. Metal plasticity? Use a plasticity model. The door is wide open.

3.  **Return to the Nonlocal World**: Now, we need to translate this classical stress $\mathbf{P}$ back into a peridynamic force state $\mathbf{T}$. The correspondence principle gives us the final piece of the puzzle:
    $$ \mathbf{T}(\mathbf{x})\langle \boldsymbol{\xi} \rangle = \omega(|\boldsymbol{\xi}|) \, \mathbf{P}(\mathbf{x}) \, \mathbf{K}(\mathbf{x})^{-1} \, \boldsymbol{\xi} $$
    This is extraordinary. The force state is defined using the classical stress. The forces are now definitively non-central; the vector $\mathbf{P}\mathbf{K}^{-1}\boldsymbol{\xi}$ does not, in general, point along the bond $\boldsymbol{\xi}$. This non-central part is precisely what's needed to represent the full range of material behavior. And this specific formula is not just a guess; it is carefully constructed to ensure that fundamental physical laws, like the conservation of linear and angular momentum, are perfectly satisfied [@problem_id:2905416].

The correspondence model gives us the best of both worlds: a nonlocal framework that can naturally handle discontinuities like cracks, powered by the robust and well-understood constitutive laws of classical mechanics.

### Beyond the Obvious: Why the Recipe for the 'Springs' Matters

At this point, you might be thinking: "If the correspondence model just uses classical laws in the end, does the choice of the [influence function](@article_id:168152) $\omega$ even matter?" After all, if we calibrate two different models with two different influence functions, $\omega_1$ and $\omega_2$, to match the same Young's modulus and Poisson's ratio, shouldn't they give the same answer?

For a simple, uniform stretch, they will. But what if we apply a non-uniform deformation, like a gentle wave with a certain wavelength? Here, a deeper magic of [peridynamics](@article_id:191297) is revealed. The two models will, in fact, predict slightly *different* stress responses [@problem_id:2667650].

The reason is that [nonlocal models](@article_id:174821) are sensitive not just to the first derivative of displacement (which gives us strain), but also to [higher-order derivatives](@article_id:140388) (which relate to the curvature of the deformation). The peridynamic stress for a wave-like deformation turns out to be slightly less than what classical theory predicts. This phenomenon is called **dispersion softening**. The amount of this softening depends on the [higher-order moments](@article_id:266442) of the [influence function](@article_id:168152)—that is, on the finer details of its shape.

This tells us something profound. The choice of an [influence function](@article_id:168152) is not just a matter of convenience; it is a physical statement about how the material responds to rapidly varying deformations. It controls how waves of different lengths propagate through the material, a real physical effect that classical theory completely misses.

And the versatility doesn't stop there. By designing an [influence function](@article_id:168152) that depends on the *direction* of a bond, not just its length, we can build anisotropy directly into the fabric of the model. This allows us to capture the behavior of materials like wood, which is much stiffer along the grain than across it, or modern [fiber-reinforced composites](@article_id:194501) [@problem_id:2667601].

From a simple but flawed model of springs, we have journeyed to a sophisticated and powerful theory. By embracing the idea of [collective states](@article_id:168103) and building a correspondence to the classical world, state-based [peridynamics](@article_id:191297) provides a framework that is not only mathematically elegant but also deeply connected to the rich and complex reality of the materials that make up our world.