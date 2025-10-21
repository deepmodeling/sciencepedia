## Introduction
Classical solid mechanics, built on the mathematics of continuous media and partial differential equations, has been a cornerstone of engineering for centuries. However, this elegant framework encounters a fundamental breakdown when faced with discontinuities, most notably at the tip of a crack, where stresses and strains approach theoretical infinity. This mathematical singularity signals a limitation in the theory's foundational assumptions, creating a knowledge gap that has historically been bridged by specialized and often empirical theories of fracture mechanics.

Peridynamic solid mechanics offers a radical and powerful alternative. It reformulates the principles of continuum mechanics by dispensing with spatial derivatives altogether. Instead of local forces and gradients, [peridynamics](@article_id:191297) describes material behavior through a network of long-range "bonds" that connect points at a finite distance. This nonlocal approach provides a unified and robust mathematical framework where damage and fracture are not special cases but natural outcomes of the governing equations. This article serves as a comprehensive introduction to this transformative theory.

First, in **Principles and Mechanisms**, we will deconstruct the core concepts of [peridynamics](@article_id:191297), exploring the shift from strain gradients to bond stretch, the role of the material horizon, and the evolution from simple bond-based models to the sophisticated power of state-based correspondence models. Next, **Applications and Interdisciplinary Connections** will demonstrate the theory's practical utility, showcasing its elegant handling of fracture, its adaptability to complex material behaviors like plasticity and anisotropy, and its capacity to model coupled [multiphysics](@article_id:163984) phenomena such as [thermal shock](@article_id:157835). Finally, the **Hands-On Practices** section provides an opportunity to solidify your understanding by working through foundational calculations and a conceptual numerical implementation, bridging the gap between theory and application.

## Principles and Mechanisms

Classical mechanics, the bedrock of engineering for centuries, is a thing of extraordinary beauty and power. It describes the world with elegant partial differential equations, built upon the idea of a smooth, continuous medium where properties at a point are determined by what’s happening infinitesimally nearby. But this beautiful edifice develops a crack—quite literally—when it confronts a crack. At the tip of a crack, stresses and strains theoretically rocket to infinity. The derivatives that the entire theory is built on cease to exist. The mathematics breaks down. It's a sign from nature that perhaps our fundamental assumptions need a second look.

Peridynamics is that second look. It proposes a radical, yet wonderfully intuitive, shift in perspective. Instead of thinking about how a material deforms locally, it asks a simpler question: how does the distance between any two points in the material change?

### A New Conversation: From Gradients to Bonds

Imagine you could zoom into a block of steel. The classical view is like giving every single point a surveyor's transit and asking it to measure the slope—the gradient—of its neighbors' movements. From these gradients, we build up a picture of strain and stress. This works beautifully, as long as the landscape is smooth. But what happens if a giant chasm—a crack—opens up? The concept of a local slope or gradient becomes meaningless right at the edge of the chasm. The surveyor's math fails [@problem_id:2667608].

Peridynamics throws out the surveyor's transit. Instead, it imagines that every point is connected to its neighbors by a network of tiny, invisible **bonds**. The entire description of deformation is now based on these bonds. We don't need gradients. We only need to know two things: the original length of a bond, and its new length after the material deforms.

This leads us to the single most important concept in peridynamic kinematics: the **bond stretch**, denoted by the symbol $s$. For a bond that initially connects points $\mathbf{x}$ and $\mathbf{x}'$ (a vector we can call $\boldsymbol{\xi} = \mathbf{x}' - \mathbf{x}$), which then move to new positions after some deformation, the stretch is simply the fractional change in its length:

$$
s = \frac{\text{new length} - \text{original length}}{\text{original length}} = \frac{|\boldsymbol{\xi} + \boldsymbol{\eta}| - |\boldsymbol{\xi}|}{|\boldsymbol{\xi}|}
$$

Here, $\boldsymbol{\eta}$ is the relative displacement of the two points at the ends of the bond. This definition is purely geometric. It makes no assumptions about the deformation being small [@problem_id:2667612]. If you stretch a rubber band to twice its length, the bond stretch is simply $1$. If a huge chasm opens and a bond is stretched across it, the stretch is still a perfectly well-defined, finite number. It never blows up to infinity. This simple, robust quantity replaces the entire machinery of the classical strain tensor, $\boldsymbol{\varepsilon}$, which is fundamentally a linearized, local measure that is undefined at discontinuities.

This new description has another profound advantage. The bond stretch $s$ is **objective**: if you take a body and subject it to a rigid rotation, the lengths of all the bonds remain the same, so all bond stretches are zero. The classical small strain tensor $\boldsymbol{\varepsilon}$, surprisingly, is *not* objective for finite rotations. If you rotate a body by, say, 30 degrees without deforming it at all, the small [strain tensor](@article_id:192838) will be nonzero, falsely signaling a strained state. The peridynamic description, by its very nature, never makes this mistake [@problem_id:2667612].

### The Horizon: A Material's Personal Space

In this new picture, does every point in the universe talk to every other point? That would be computationally and physically untenable. Instead, [peridynamics](@article_id:191297) posits that each material point interacts only with other points within a finite neighborhood. This "personal space" is a small sphere (or ball) of radius $\delta$, known as the **horizon**. The collection of points that interact with a point $\mathbf{x}$ is called its **family**, $\mathcal{H}_{\mathbf{x}}$.

The horizon $\delta$ is not just a computational convenience; it is a new, fundamental material parameter. It represents an intrinsic length scale of nonlocality in the material. Classical theory has no such length scale. This has an important consequence: the peridynamic model acts as a natural low-pass filter. Any deformation or feature that has a [characteristic length](@article_id:265363) smaller than the horizon $\delta$ gets "smeared out" or averaged by the integral nature of the interactions. This is a real physical effect, known as [material dispersion](@article_id:198578), which is observed in wave propagation at very small scales. The classical theory, being local, cannot capture this.

It's crucial to understand that this physical length scale $\delta$ is distinct from the numerical [discretization](@article_id:144518) size, let's call it $h$ (like the spacing between computational nodes). One can refine the numerical mesh by making $h$ smaller and smaller to get a more accurate solution to the peridynamic equations, but this does not change the underlying physics governed by $\delta$. Any features smaller than $\delta$ will remain unresolved, no matter how tiny you make $h$ [@problem_id:2667647].

What happens if we shrink this intrinsic length scale? If we take the limit as the horizon $\delta \to 0$ (while appropriately scaling our material properties), the integral equations of [peridynamics](@article_id:191297) elegantly converge to the partial differential equations of classical elasticity. Classical mechanics is recovered as a special case—the limit of vanishing nonlocality [@problem_id:2667647].

### Building the Rules of Interaction

So, we have points connected by bonds within a horizon. But what are the rules of their interaction? How does one bond "push" or "pull" on another? This is the realm of constitutive modeling.

#### A Universe of Springs: The Bond-Based Model

The simplest, most intuitive model is to assume that each bond acts like a simple spring. The force in the bond is directly proportional to its stretch. We can write this as a "[central force](@article_id:159901)"—a force that always acts along the line connecting the two points. For an [isotropic material](@article_id:204122), where properties are the same in all directions, the force $\mathbf{f}$ in a bond can be expressed as:

$$ \mathbf{f} = c(|\boldsymbol{\xi}|) \, s \, \mathbf{e} $$

Here, $c(|\boldsymbol{\xi}|)$ is a **micromodulus** that defines the "stiffness" of a bond of original length $|\boldsymbol{\xi}|$, $s$ is the bond stretch, and $\mathbf{e}$ is a unit vector pointing along the *deformed* bond. The collinearity of the force with the deformed bond is a direct consequence of [isotropy](@article_id:158665); any other direction would imply the material has some [preferred orientation](@article_id:190406) [@problem_id:2667588].

This **bond-based model** is beautiful in its simplicity. It's a universe made of microscopic springs. However, this simplicity comes at a cost. A material's response to being stretched in one direction and how much it contracts in the perpendicular directions is governed by its Poisson's ratio. In the bond-based model, the central-force assumption rigidly fixes this value (to $1/4$ in 3D and $1/3$ in 2D). This model cannot describe a material like rubber (Poisson's ratio near $0.5$) or cork (Poisson's ratio near $0$). It's like building a universe where every person must have the exact same personality.

#### Richer Conversations: The Power of "State"

To give materials their unique personalities, we need to allow for richer conversations. The force in a [single bond](@article_id:188067) cannot depend solely on its own stretch. It must also depend on the collective behavior of all the other bonds in its family. This is the key idea behind **state-based** [peridynamics](@article_id:191297). The force in a bond depends on the "state" of the entire neighborhood.

The first step in this direction is the **ordinary state-based model**. Here, we still insist that the force in a bond acts along the bond's direction, but we allow its magnitude to depend on a collective measure of deformation, like the local volume change, or **dilatation**, $\theta$. We can now write a force law that has two separate parts: one part that resists volume changes (related to the bulk modulus, $\kappa$) and another that resists changes in shape (related to the [shear modulus](@article_id:166734), $\mu$). By allowing independent control over these two responses, we can model any physically admissible Poisson's ratio [@problem_id:2667632]. The force state $\mathbf{T}$ for a bond $\boldsymbol{\xi}$ can be decomposed into a dilatational and a deviatoric (shape-changing) part, freeing us from the constraint of the simpler model [@problem_id:2667635].

The ultimate generalization is the **nonordinary state-based model**. This is a breathtakingly general concept. It essentially builds a bridge, or a "correspondence," directly back to the rich world of classical constitutive models. The procedure is profound:
1.  From the collective deformation of all bonds in a point's family, we compute a single, effective **nonlocal [deformation gradient](@article_id:163255)**, $\mathbf{F}$ [@problem_id:2667661]. This is done using a mathematical tool called the **shape tensor**, $\mathbf{K}$, which accounts for the geometry of the horizon [@problem_id:2667621].
2.  Once we have this nonlocal $\mathbf{F}$, we can plug it into *any* of the well-established, time-tested material models from classical mechanics to compute a stress tensor, like the First Piola-Kirchhoff stress $\mathbf{P}$. Do you want to model a complex polymer or a particular metal alloy? If a classical model exists for it, you can use it.
3.  This [stress tensor](@article_id:148479) $\mathbf{P}$ is then used to define the peridynamic force state for each bond.

In this model, the force in a bond is no longer constrained to be central. It can have components that are perpendicular to the bond, which is what's needed to capture the full range of elastic behavior. This nonordinary model gives us the best of both worlds: the robustness of the peridynamic framework to handle discontinuities and the full descriptive power of classical constitutive theory [@problem_id:2667661].

### The Grand Payoff: The Simple Beauty of Fracture

Now we come back to our original problem: the crack. How does [peridynamics](@article_id:191297) model fracture? The answer is astounding in its simplicity. There are no special "crack tip elements," no complex algorithms to track the crack path. There is just one simple rule:

*If a bond is stretched beyond a certain critical value, it breaks.*

That's it. A broken bond can no longer carry force. We add a history-dependent rule to our simulation: for each bond, we keep track of the maximum stretch, $S_{\text{max}}(t)$, it has ever experienced. If this maximum stretch exceeds a predefined **[critical stretch](@article_id:199690)**, $s_c$, the bond's status switches irreversibly from "intact" to "broken," and its contribution to the force calculation is set to zero forever [@problem_id:2667586].

A crack is not something we put into the model. A crack is something that *emerges* from the collective behavior of billions of these simple, local bond-breaking events. As the material is loaded, bonds in the most highly stressed region begin to fail. This broken region grows, coalesces, and forms a macroscopic crack. The path of the crack is determined by the evolving stress field, allowing for complex behaviors like [crack branching](@article_id:192877) to arise naturally.

But how do we choose the microscopic parameter $s_c$? It can't just be an arbitrary number; it has to be connected to physical reality. This is the final piece of the puzzle. We link $s_c$ to a macroscopic, measurable material property: the **fracture energy**, $G_c$. The fracture energy is the amount of energy required to create one unit area of new crack surface. We can calculate the total elastic energy stored in all the bonds that cross a prospective crack plane just before they fail. By setting this total stored energy equal to the known material fracture energy $G_c$, we can derive a precise relationship between the microscopic parameter $s_c$ and the macroscopic property $G_c$. This critical step anchors our peridynamic model to physical experiment, transforming it from a mere simulation into a predictive scientific tool [@problem_id:2667609].

By stepping away from the local, calculus-based view and embracing a "social network" of interacting points, [peridynamics](@article_id:191297) not only provides a powerful and practical solution to the age-old problem of fracture but also arguably reveals a deeper, more fundamental, and more robust description of what it means to be a continuum.