## Introduction
The catastrophic failure of materials, from a cracked phone screen to a fractured airplane wing, reveals a fundamental limitation in classical physics. For centuries, continuum mechanics has described solids as smooth, continuous entities, using mathematics that breaks down at the sharp, abrupt reality of a crack. The resulting mathematical singularities signal a gap in our theoretical understanding, forcing engineers to rely on complex workarounds. How can we build a theory that embraces fracture as a natural outcome rather than a mathematical catastrophe?

This article introduces Peridynamics, a revolutionary [non-local theory](@entry_id:1128805) that redefines our approach to material failure. By shifting focus from stresses at a point to interactions within a neighborhood, [peridynamics](@entry_id:191791) provides a unified framework that remains valid before, during, and after fracture. The following chapters will guide you through this new paradigm. In "Principles and Mechanisms," you will learn the foundational concepts of the peridynamic model, from its integral [equation of motion](@entry_id:264286) to its elegant mechanism for [autonomous crack growth](@entry_id:1121273). "Applications and Interdisciplinary Connections" will explore the theory's far-reaching impact, demonstrating its power to solve complex problems in dynamic fracture, [geomechanics](@entry_id:175967), and multiscale science. Finally, "Hands-On Practices" will offer practical exercises to deepen your understanding of the model's behavior and physical underpinnings.

## Principles and Mechanisms

To understand how things break is to probe one of the most fundamental behaviors of the physical world. For centuries, our best theories of materials, inherited from the great minds of continuum mechanics, were built on an idealized vision. They pictured solid objects as perfectly smooth, continuous entities, like a tranquil sea. The mathematics they used, the calculus of derivatives, was designed to describe gradual changes—the gentle slope of a hill, not the sheer drop of a cliff.

But a crack is a cliff. It is an abrupt, violent separation. At the very edge of a crack, the displacement of the material jumps from one value to another. If you try to apply the old mathematics here, it simply fails. The equations, which rely on the existence of smooth derivatives, become singular and nonsensical. It's as if our language for describing the world had no words for "broken." Physicists and engineers, of course, developed brilliant workarounds, but the theory itself had a crack in its own foundation. What was needed was a new language, a new way of seeing.

### A Fresh Perspective: Interactions, Not Gradients

Peridynamics, a theory developed by Stewart Silling at the turn of the 21st century, offers this new language. It begins with a wonderfully simple, yet profound, shift in perspective. Instead of asking, "What are the stresses and strains at an infinitesimally small point?", it asks, "How does a particle of material interact with all of its neighbors?" 

Imagine a solid not as a continuous jelly, but as a vast collection of particles, each connected to its neighbors by tiny, invisible "bonds." The state of the material is determined by the collective state of these bonds. This is a shift from a **local** view, obsessed with the state at a single point, to a **non-local** view, where a point's behavior is governed by its entire neighborhood.

The governing law of this new physics looks remarkably like Newton's second law, but with a twist. The force causing a particle at position $\mathbf{x}$ to accelerate is not given by the divergence of a stress tensor, but by the sum of all the tiny pairwise forces exerted by its neighbors. Because there are so many neighbors, this sum becomes an integral. The [equation of motion](@entry_id:264286) for a particle is:

$$
\rho(\mathbf{x}) \frac{\partial^2 \mathbf{u}(\mathbf{x},t)}{\partial t^2} = \int_{\mathcal{H}_{\mathbf{x}}} \mathbf{f}(\mathbf{u}(\mathbf{x}', t) - \mathbf{u}(\mathbf{x}, t), \mathbf{x}' - \mathbf{x}) \, dV_{\mathbf{x}'} + \mathbf{b}(\mathbf{x}, t)
$$

Let's not be intimidated by the symbols. This equation says something quite intuitive. The acceleration of a particle (left side) is caused by the sum (the $\int$ sign) of all the pairwise forces $\mathbf{f}$ from its neighbors $\mathbf{x}'$, plus any external force like gravity $\mathbf{b}$. The pairwise force $\mathbf{f}$ itself depends only on the relative positions and relative displacements of the two interacting particles. Notice what's missing: there are no [spatial derivatives](@entry_id:1132036) of the [displacement field](@entry_id:141476) $\mathbf{u}$. We are only ever subtracting the positions of two distinct points. Even if a crack lies between them, causing a jump in $\mathbf{u}$, the displacements $\mathbf{u}(\mathbf{x})$ and $\mathbf{u}(\mathbf{x}')$ are themselves perfectly well-defined. The theory remains valid everywhere, even at the face of a crack.  

This pairwise force function $\mathbf{f}$ also respects Newton's third law: the force particle $\mathbf{x}'$ exerts on $\mathbf{x}$ is equal and opposite to the force $\mathbf{x}$ exerts on $\mathbf{x}'$. This is a crucial requirement for conserving momentum. 

### The Horizon: A Bubble of Influence

You might ask: which neighbors are we talking about? Does a particle in your coffee cup interact with a particle on the moon? Peridynamics says no. Each particle interacts only with neighbors inside a small, finite neighborhood called the **horizon**, typically a sphere of radius $\delta$. This horizon, denoted $\mathcal{H}_{\mathbf{x}}$ in the equation, is the "bubble of influence" for the particle at $\mathbf{x}$. 

This horizon radius, $\delta$, is not just a computational convenience; it is a fundamental **internal length scale** of the material. Its size can be thought of as being related to the underlying microstructure, like the [grain size](@entry_id:161460) in a metal or the polymer chain length in a plastic. It dictates the scale of nonlocality.

The beauty of this framework is its deep connection to the classical theory it seeks to replace. If you take a material with no cracks and shrink the horizon radius $\delta$ towards zero, the peridynamic equation of motion magically transforms back into the classical equation of elasticity.  This ensures that [peridynamics](@entry_id:191791) isn't some ad-hoc model, but a more general theory of mechanics that contains the classical theory as a special, limiting case. It's like discovering that Newtonian gravity is a limit of Einstein's general relativity; the old theory isn't wrong, it's just incomplete.

### How Bonds "Feel" a Stretch

To build a predictive theory, we need to know how the force $\mathbf{f}$ in a bond relates to the material's deformation. How does a bond "feel" that it is being stretched or compressed? We need a way to measure this.

Let's consider two particles, initially at positions $\mathbf{x}$ and $\mathbf{x}'$. The vector connecting them is the initial bond vector, $\boldsymbol{\xi} = \mathbf{x}' - \mathbf{x}$. After the material deforms, the particles move to new positions, $\mathbf{y}$ and $\mathbf{y}'$. The new vector connecting them is $\mathbf{y}' - \mathbf{y}$. This new vector can be expressed in terms of the old one and the relative displacement, $\boldsymbol{\eta} = \mathbf{u}(\mathbf{x}') - \mathbf{u}(\mathbf{x})$, as $\boldsymbol{\xi} + \boldsymbol{\eta}$. 

The most important measure of deformation for a single bond is its **stretch**, denoted by $s$. Just like in introductory physics, the stretch is defined as the change in length divided by the original length:

$$
s = \frac{\text{final length} - \text{initial length}}{\text{initial length}} = \frac{\|\boldsymbol{\xi} + \boldsymbol{\eta}\| - \|\boldsymbol{\xi}\|}{\|\boldsymbol{\xi}\|}
$$

This simple, scalar number is the heart of the matter. If $s > 0$, the bond is in tension. If $s  0$, it is in compression. If $s=0$, its length hasn't changed. The entire deformation state of the material is encoded in the collection of stretches of all its bonds. 

### Autonomous Fracture: The Birth of a Crack

Now for the magic. How does a crack form and grow? In [peridynamics](@entry_id:191791), this process is astonishingly simple and autonomous. There are no external criteria, no complex tracking algorithms. Fracture emerges naturally from the basic [constitutive law](@entry_id:167255).

We start by defining a **[critical stretch](@entry_id:200184)**, $s_c$, for the material. This is a material property, just like density or stiffness. The rule is simple: if the stretch $s$ in any bond exceeds this critical value, the bond breaks.  For a brittle material, this breaking is irreversible. Once broken, the force function $\mathbf{f}$ for that bond pair is set to zero forever. The bond can no longer carry any load.

A crack, then, is not a special entity that we must insert into our model. A crack is simply an emergent feature of the simulation—a region where a significant number of bonds have broken. The traction-free surfaces of a real crack are automatically created because the forces that once acted across that surface (the bonds) are now gone. The internal force integral in the equation of motion naturally and gracefully handles this new boundary. 

We can even define a local **damage** variable, $D(\mathbf{x})$, at each point. It is simply the weighted fraction of broken bonds within that point's horizon. A damage value of $D=0$ means the material is pristine, while $D=1$ means all connections are severed and the material is completely failed at that point. This gives us a [continuous map](@entry_id:153772) of the [fracture process zone](@entry_id:749561). 

This autonomous nature of fracture is what makes [peridynamics](@entry_id:191791) so powerful and elegant compared to other methods. Traditional Cohesive Zone Models (CZMs), for instance, require the modeler to pre-define the potential paths a crack might take. Phase-Field Models (PFMs), while also allowing for complex crack patterns, are based on a more abstract [energy minimization](@entry_id:147698) principle. Peridynamics, by contrast, feels more direct and physical: you pull on the material, bonds stretch, and if they stretch too much, they snap. The crack goes where the broken bonds lead it. 

Furthermore, the microscopic [critical stretch](@entry_id:200184) $s_c$ is not just an arbitrary parameter. It is directly calibrated to match the macroscopic, experimentally measurable **[fracture energy](@entry_id:174458)** ($G_c$) of the material. This ensures that the energy required to create a new crack surface in the simulation is consistent with the energy required in the real world, providing a beautiful link between the micro and macro scales. 

### The Family of Models: From Simple Bonds to General States

The simplest peridynamic models are called **bond-based** models. In these, the force in a bond depends only on the stretch of that single bond, much like a simple spring. The force is also assumed to act directly along the line connecting the two particles (a [central force](@entry_id:160395)). This simple model is incredibly powerful, but it has a curious limitation: because of the [central force](@entry_id:160395) assumption, it cannot represent any arbitrary elastic material. For any 3D isotropic material, it predicts a fixed value for the Poisson's ratio of $\nu=1/4$. 

This limitation spurred the development of more general **state-based** peridynamic models. The core idea is to relax the [one-to-one correspondence](@entry_id:143935) between a single bond's stretch and its force. In a state-based model, the force in a particular bond can depend on the collective deformation of *all* the bonds in the horizon. This is like saying the stiffness of one spring in a network can change depending on how all the other springs are being stretched.

This is accomplished by introducing the concepts of a **deformation state** (the collection of all bond deformations in a horizon) and a **force state** (the collection of all bond forces). The force state is a function of the entire deformation state. This generalization breaks the central-force constraint, allowing forces to have components that are not aligned with the bond. This added freedom is exactly what is needed to capture the behavior of any elastic material, with any valid Poisson's ratio, and even complex [anisotropic materials](@entry_id:184874) like wood or composites. 

### A Note on Reality: Life at the Edge

One final, subtle point reveals the practical cleverness of the theory. What happens to a particle right at the surface of an object? Its horizon is truncated—it has neighbors on one side but not the other. If we use the same material properties as an interior point, this surface particle will appear "softer" because it's missing half of its supporting bonds. 

To fix this "skin effect," modelers apply a simple correction: they increase the stiffness of the bonds for surface particles to compensate for the missing neighbors. This ensures that the surface of the material has the same stiffness as the bulk, just as it should. It is a pragmatic adjustment that shows how the abstract theory is carefully applied to model real-world objects. 

By rethinking the very nature of a continuum, [peridynamics](@entry_id:191791) provides a single, unified framework to describe both the graceful deformation of a material and its catastrophic failure. It replaces the troublesome derivatives of the old theory with robust integrals, and in doing so, allows cracks to be born and to grow with a beautiful, physical autonomy. It is a testament to the idea that sometimes, to solve a difficult problem, you don't need a more complicated equation, but simply a new way to look.