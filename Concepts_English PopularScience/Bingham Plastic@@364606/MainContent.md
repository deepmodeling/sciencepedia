## Introduction
Some materials defy simple classification. They are not quite solid, not quite liquid, but exhibit properties of both. Think of toothpaste, which holds its shape on a brush but spreads easily under pressure, or ketchup, which refuses to pour until the bottle is shaken vigorously. These substances belong to a class of materials known as Bingham plastics, and their peculiar behavior is not just a scientific curiosity but a fundamentally important property exploited in countless industrial processes and natural phenomena. The central question they pose is: how can we describe and predict the behavior of a material that says "no" to flowing until a specific condition is met?

This article provides a comprehensive overview of the Bingham plastic model, bridging the gap between abstract theory and real-world relevance. Across the following chapters, we will unravel the physics behind this fascinating behavior. In "Principles and Mechanisms," we will explore the core concept of yield stress, the mathematical model that governs flow, and the signature phenomenon of [plug flow](@article_id:263500). Subsequently, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these principles manifest everywhere, from the engineering of drilling muds and smart fluids to the powerful geological forces that shape our planet, like landslides and magma flows. By the end, you will see how understanding this "stubborn" fluid deepens our knowledge of the material world.

## Principles and Mechanisms

### A Fluid That Says "No"

Imagine you're trying to get that last bit of ketchup out of the bottle. You turn it upside down. Nothing happens. It just sits there, stubbornly refusing to flow. It’s behaving like a solid. Then, you give it a good, sharp shake—you apply a [strong force](@article_id:154316)—and suddenly it flows out. Or think of toothpaste: it sits neatly on your toothbrush, holding its shape, but spreads easily when you brush. These everyday materials are not quite solid and not quite liquid. They belong to a fascinating class of substances known as **Bingham plastics**.

Unlike a simple fluid like water, which will flow under the slightest encouragement, a Bingham plastic first says "no." It resists flowing until the force applied to it crosses a critical threshold. This threshold is a fundamental property of the material called the **[yield stress](@article_id:274019)**, denoted by the symbol $\tau_y$. In the language of physics, stress is simply a measure of force distributed over an area. A careful [dimensional analysis](@article_id:139765) reveals its fundamental makeup in terms of mass (M), length (L), and time (T) to be $M L^{-1} T^{-2}$ [@problem_id:1782421]. Until the shear stress acting on the material exceeds $\tau_y$, the material behaves just like a rigid solid. Once you push harder than this yield stress, it gives in and begins to flow like a viscous fluid. This simple, two-part behavior is the key to understanding a whole world of materials, from drilling muds deep in the Earth's crust to the creamy frosting on a cake.

### The Jekyll and Hyde of Fluids

This dual nature—behaving as a solid one moment and a fluid the next—is what makes Bingham plastics so unique and useful. Let's look a little closer at these two faces.

First, consider the "solid" state. When the applied shear stress, $\tau$, is less than or equal to the [yield stress](@article_id:274019), $\tau_y$, the material does not deform or flow. The rate of shear, a measure of how fast the fluid layers are sliding past one another (denoted $\dot{\gamma}$), is exactly zero. We can ask a curious question here: what is the viscosity of the material in this state? Normally, viscosity is the ratio of stress to shear rate. But here, the shear rate is zero! If we define an **[effective viscosity](@article_id:203562)** as $\mu_{\text{eff}} = |\tau| / \dot{\gamma}$, we find ourselves dividing a non-zero stress by zero. The result is, mathematically speaking, infinite! [@problem_id:1765681]. This isn't just a mathematical quirk; it’s a profound physical statement. An infinite viscosity means an infinite resistance to *starting* to flow. This is the precise mathematical description of a solid.

Now, what happens when we push harder and cross the threshold, so that $|\tau| > \tau_y$? The material yields and begins to flow. Its behavior is now described by the **Bingham model**:
$$
|\tau| = \tau_y + \mu_p |\dot{\gamma}|
$$
This equation tells us that the total stress needed to keep the fluid moving is the sum of two parts: you must constantly overcome the initial yield stress $\tau_y$, *and* you must work against the fluid's internal friction. This internal friction is governed by a new parameter, $\mu_p$, called the **[plastic viscosity](@article_id:266547)**. It acts just like the familiar viscosity of a Newtonian fluid, but it only comes into play *after* the material has already started flowing.

This on/off switching behavior is fundamentally different from other non-Newtonian fluids, like a cornstarch-and-water mixture (a [shear-thickening](@article_id:260283) fluid), which flows under any stress, however small, but just gets thicker as you stir it faster. The existence of a true [yield stress](@article_id:274019) allows for clever engineering, like a passive safety valve that remains perfectly sealed under low background pressures but opens up to allow flow when a high operational pressure is applied [@problem_id:1789227].

### A Family Portrait of Fluids

In physics, we delight in finding connections and unifying principles. It turns out that the Bingham model is not an isolated curiosity but part of a larger, more comprehensive family of fluid behaviors. We can see this by looking at a more general relationship called the **Herschel-Bulkley model**:
$$
\tau = \tau_y + K(\dot{\gamma})^n
$$
This equation looks like a slightly more complicated version of the Bingham model. It has a yield stress $\tau_y$, a consistency index $K$ (similar to viscosity), and a [flow behavior index](@article_id:264523) $n$ that describes how the viscosity changes with shear rate.

Think of this model as a recipe book for fluids. By choosing different values for the parameters, we can describe a whole range of materials [@problem_id:1776094]:
-   If we set the flow index $n=1$, the equation becomes $\tau = \tau_y + K\dot{\gamma}$. This is precisely the **Bingham plastic** model, with the consistency index $K$ playing the role of the [plastic viscosity](@article_id:266547) $\mu_p$.
-   If we start over and set the [yield stress](@article_id:274019) $\tau_y=0$, we get $\tau = K(\dot{\gamma})^n$. This describes a **[power-law fluid](@article_id:150959)**, a common type of non-Newtonian fluid without a [yield stress](@article_id:274019).
-   Now for the [grand unification](@article_id:159879): what if we set $\tau_y=0$ *and* $n=1$? The equation simplifies beautifully to $\tau = K\dot{\gamma}$. This is none other than the definition of a simple **Newtonian fluid** (like water or air), where the constant $K$ is the familiar [dynamic viscosity](@article_id:267734) $\mu$.

So, we see a beautiful hierarchy. The seemingly complex behavior of a Bingham plastic is just one branch of a family tree that also includes the simple fluids we learned about first. Nature, it seems, enjoys variations on a theme.

### The Solid River: Plug Flow

Let's now watch a Bingham plastic in action, in a scenario that reveals its most iconic feature. Imagine we are pumping one of these fluids—perhaps a cement slurry or a food product—through a long, straight pipe. What does the flow look like?

First, let's recall a fundamental principle of any pressure-driven [pipe flow](@article_id:189037). A simple balance of forces on a cylinder of fluid tells us that the shear stress is not uniform across the pipe. It is zero at the exact center and increases linearly with the distance from the center, reaching its maximum value at the pipe wall [@problem_id:1922483]. The stress profile is given by a wonderfully simple relation:
$$
\tau(r) = \frac{G}{2} r
$$
where $r$ is the radial distance from the center and $G$ is the magnitude of the [pressure gradient](@article_id:273618) (the "push") driving the flow.

Now, let's combine this fact with what we know about Bingham plastics. Since the stress is lowest at the center and increases outwards, there must be a central region where the stress is *less than* the [yield stress](@article_id:274019), $\tau(r) < \tau_y$. What happens in this region? The fluid cannot shear! It must move together as a single, solid piece. This creates the remarkable phenomenon of **[plug flow](@article_id:263500)**: a solid core, or plug, of material sliding down the center of the pipe, lubricated by an outer layer of the same material that *has* yielded and is flowing like a fluid.

We can even calculate the radius of this solid river. The edge of the plug, $r_p$, is precisely where the stress equals the [yield stress](@article_id:274019). By setting $\tau(r_p) = \tau_y$, we find:
$$
r_p = \frac{2\tau_y}{G}
$$
This elegant formula [@problem_id:1737179] [@problem_id:1922483] holds a lot of physical intuition. It tells us that the plug radius is directly proportional to the yield stress (a stickier fluid has a bigger plug) and inversely proportional to the pressure gradient. If you pump harder (increase $G$), the plug shrinks, as more of the fluid is forced to yield and join the flowing layer [@problem_id:1737187]. Of course, to get any flow at all, the push must be strong enough to overcome the yield stress at the pipe wall. This sets a minimum pressure gradient required to start the flow [@problem_id:1737151]. The resulting velocity profile is striking: perfectly flat in the center where the solid plug moves at a uniform speed, then curving down to zero at the stationary pipe walls [@problem_id:1792890].

### Coming Full Circle

We began our journey by seeing how Bingham plastics differ from ordinary Newtonian fluids. It is only fitting that we end by seeing how they can become them. What happens to our solid river if we have a fluid with a [yield stress](@article_id:274019) of zero?

Let's look at our plug radius formula, $r_p = 2\tau_y/G$. If we imagine reducing the yield stress, making the fluid less "stubborn," the plug radius gets smaller and smaller. In the limit as $\tau_y \to 0$, the plug radius vanishes! The solid core disappears, and the entire fluid across the pipe is now in a state of shear.

This conceptual journey has a beautiful mathematical counterpart. The full equation for the [volumetric flow rate](@article_id:265277) ($Q$) of a Bingham plastic in a pipe is known as the **Buckingham-Reiner equation**. It's a bit more complex than the one for Newtonian fluids because it has to account for the energy spent on the plug.
$$
Q = \frac{\pi R^4 \Delta P}{8 \mu_p L} \left[ 1 - \frac{4}{3} \left( \frac{\tau_y}{\tau_w} \right) + \frac{1}{3} \left( \frac{\tau_y}{\tau_w} \right)^4 \right]
$$
Here, $\tau_w$ is the stress at the pipe wall. Now, let's perform a thought experiment. What happens if we set $\tau_y = 0$? The entire bracketed term, which represents the correction due to the material's "yieldiness," simplifies to just 1. The equation magically transforms into:
$$
Q = \frac{\pi R^4 \Delta P}{8 \mu_p L}
$$
This is none other than the celebrated **Hagen-Poiseuille equation** for the flow of a simple Newtonian fluid! And the [plastic viscosity](@article_id:266547) $\mu_p$ simply takes on the role of the familiar Newtonian viscosity $\mu$ [@problem_id:1737191].

This is a wonderful demonstration of the elegance and unity of physics. The more general, and initially more strange, model for a Bingham plastic naturally contains the simpler, familiar case within it. By venturing into the world of fluids that say "no," we have not only discovered their unique and useful properties but also arrived at a deeper and more unified understanding of the everyday fluids that always say "yes."