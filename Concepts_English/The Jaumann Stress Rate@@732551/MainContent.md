## Introduction
In the world of continuum mechanics, describing how forces within a material—its stress—change over time is fundamental. However, a significant challenge arises when the material is not only deforming but also rotating. A simple time derivative of stress fails to distinguish between changes due to actual material stretching and those caused by mere tumbling, violating the crucial [principle of material frame indifference](@entry_id:194378). This article tackles this problem by exploring the Jaumann stress rate, a foundational concept developed to provide an objective measure of stress change. In the following chapters, we will delve into the core ideas behind this concept. "Principles and Mechanisms" will uncover why standard derivatives fail, detail the elegant construction of the Jaumann rate, and reveal its famous, paradoxical flaw. Subsequently, "Applications and Interdisciplinary Connections" will demonstrate its widespread use in computational simulations and its influence across diverse fields, from materials science to [geomechanics](@entry_id:175967), illustrating its legacy as a beautiful but imperfect tool.

## Principles and Mechanisms

Imagine you are trying to describe a piece of taffy being pulled and twisted at the same time. The taffy is stretching, which means it's deforming, but it's also tumbling through the air, which is just a rigid rotation. A physicist or engineer looking at this taffy wants to create a law that relates the forces inside the taffy—the **stress**—to its deformation. But here’s the puzzle: how do we separate the real change in stress caused by the stretching from the apparent change caused by the fact that the whole thing is simply spinning? Your physical laws shouldn’t depend on whether you are standing still or doing a pirouette while you observe the experiment. The material itself doesn’t know or care about your point of view. This fundamental idea, that the laws of physics must be independent of the observer's motion, is called the **[principle of material frame indifference](@entry_id:194378)**, or simply **objectivity**. [@problem_id:2653167]

### The Deception of the Simple Derivative

Our first instinct when we want to measure a rate of change is to take a time derivative. We have the **Cauchy stress tensor**, $\boldsymbol{\sigma}$, which is a beautiful mathematical object that tells us the state of [internal forces](@entry_id:167605) at any point within our material. So, why not just look at how it changes with time, $\dot{\boldsymbol{\sigma}}$ (the [material time derivative](@entry_id:190892))?

Let's try a thought experiment. Take a block of steel and put it in a vise, so it's under some compression. Now, release it from the vise and just spin it in the air with a constant angular velocity. Is the material deforming? No. It's just a rigid rotation. Is the state of stress *inside* the material changing? Also no. The atoms are still being squeezed in the same way relative to their neighbors. And yet, for an observer standing still, the components of the stress tensor are changing continuously as the block tumbles. For instance, a force that was purely vertical is now horizontal, and a moment later it's vertical again. This means that $\dot{\boldsymbol{\sigma}}$ is not zero!

This is a disaster. If we were to propose a physical law like "the rate of stress change is proportional to the rate of stretching," using $\dot{\boldsymbol{\sigma}}$ would imply that we could generate stress just by spinning an object, without any stretching at all. This violates our [principle of objectivity](@entry_id:185412). The [material time derivative](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ is "contaminated" by rotation; it doesn't distinguish between changes due to genuine deformation and changes due to a simple change in orientation. [@problem_id:3532162] [@problem_id:2911179]

### A Clever Fix: The Jaumann Rate

If the simple derivative is contaminated, the obvious next step is to try and "clean" it. We need to mathematically subtract the part of the change that is due solely to the rigid spinning of the material. To do this, we need a way to measure the local rate of rotation. Fortunately, [continuum mechanics](@entry_id:155125) provides just the tool: the **[spin tensor](@entry_id:187346)**, $\boldsymbol{W}$, which is the skew-symmetric part of the velocity gradient, $\boldsymbol{L}$. It precisely describes how the material is locally spinning at every point.

The rate of change of the stress tensor caused by this pure spin, without any deformation, can be shown to be the term $\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}$. This is the rotational "noise" we want to remove. So, we define a new, "objective" stress rate by taking the total observed rate, $\dot{\boldsymbol{\sigma}}$, and subtracting this rotational part. This corrected rate is called the **Jaumann stress rate**, or [corotational rate](@entry_id:193173):

$$
\overset{\circ}{\boldsymbol{\sigma}}{}^{J} = \dot{\boldsymbol{\sigma}} - (\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}) = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$

Let's revisit our spinning block of steel. In that case, we found that the observed rate of change was exactly $\dot{\boldsymbol{\sigma}} = \boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}$. Plugging this into the formula for the Jaumann rate gives:

$$
\overset{\circ}{\boldsymbol{\sigma}}{}^{J} = (\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}) - (\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}) = \boldsymbol{0}
$$

It works! The Jaumann rate is zero when there is no deformation, just as our physical intuition demands. This means the Jaumann rate is an **[objective stress rate](@entry_id:168809)**. It successfully isolates the change in stress that is due to the material actually being deformed. Now we can write a proper, objective [constitutive law](@entry_id:167255), such as a hypoelastic law, relating this [objective stress rate](@entry_id:168809) to the rate of deformation, $\boldsymbol{D}$:

$$
\overset{\circ}{\boldsymbol{\sigma}}{}^{J} = \mathbb{C} : \boldsymbol{D}
$$

where $\mathbb{C}$ represents the material's stiffness. This equation respects the [principle of objectivity](@entry_id:185412). If you and a friend, who is spinning on a merry-go-round, both use this equation to model the material, you will both arrive at the same conclusions about its behavior. [@problem_id:3585755] [@problem_id:3615685] Furthermore, this formulation ensures that if the stress tensor starts out symmetric (as it must to satisfy the [balance of angular momentum](@entry_id:181848)), it remains symmetric during a pure rotation, a crucial property for the [stability of numerical methods](@entry_id:165924) like the Finite Element Method (FEM). [@problem_id:2616473]

### The Fly in the Ointment: When Simple Isn't Good Enough

For a long time, the Jaumann rate seemed like a beautifully simple and elegant solution. It is objective, and it is intuitive. But nature, as it often does, had a surprise in store. The Jaumann rate works perfectly for pure stretch and pure rotation. But what about motions that are a mixture of both?

Consider the motion of **[simple shear](@entry_id:180497)**—imagine sliding a deck of cards. This is a common and fundamentally important type of deformation. Kinematically, it is a combination of pure stretching along the diagonals and a rigid rotation. If we apply a constant rate of shear to an elastic material, we would intuitively expect the internal shear stress to build up steadily and monotonically, just like the force in a spring that is being stretched at a constant speed.

However, when we use a constitutive law based on the Jaumann rate to model this [simple shear](@entry_id:180497), we get a bizarre result. The model predicts that the shear stress does not increase monotonically. Instead, it oscillates, rising and falling sinusoidally as the shear continues! [@problem_id:3546987] For a constant shear rate $\kappa$, the predicted shear stress $\sigma_{12}$ turns out to be $\sigma_{12}(t) = \mu\sin(\kappa t)$, instead of the expected $\sigma_{12}(t) = \mu\kappa t$. This is completely unphysical. [@problem_id:3499677]

Why does this failure occur? The problem is subtle. The Jaumann rate's correction is based on the continuum [spin tensor](@entry_id:187346) $\boldsymbol{W}$. While $\boldsymbol{W}$ describes the spin of the material lines, it does not always describe the spin of the material's internal "fabric"—the principal axes of stress and strain. In [simple shear](@entry_id:180497), these principal axes rotate, but at a rate different from $\boldsymbol{W}$. The Jaumann rate, by using $\boldsymbol{W}$, essentially "over-corrects" for the rotation, leading to the spurious oscillations.

### Beyond Jaumann: The Search for a Better Rate

The discovery of this flaw in the Jaumann rate was a pivotal moment. It didn't mean the [principle of objectivity](@entry_id:185412) was wrong; it meant our first, simplest attempt at building an objective rate was incomplete. This launched a search for more sophisticated [objective rates](@entry_id:198692) that could correctly handle complex motions like shear.

This search led to the development of other rates, such as the **Green-Naghdi rate** and the **logarithmic rate**. These rates use different, more physically motivated definitions of the rotational spin, often tied to the rotation of the material's principal axes of deformation. [@problem_id:3531802] For instance, the logarithmic rate is beautifully linked with a measure of strain called Hencky strain, forming an "energy-conjugate" pair. This means that, unlike most Jaumann-based models, it can be derived from a [stored energy function](@entry_id:166355), giving it a much stronger thermodynamic foundation.

These advanced rates do not produce the non-physical oscillations seen with the Jaumann rate and are now the standard in modern computational codes for simulating large-deformation problems in geophysics, materials science, and engineering. [@problem_id:3531802]

The story of the Jaumann rate is a perfect illustration of science in action. It begins with a fundamental principle (objectivity), inspires a simple and elegant solution that solves a major problem ($\dot{\boldsymbol{\sigma}}$ is not objective), reveals its own limitations through a critical thought experiment ([simple shear](@entry_id:180497)), and ultimately paves the way for a deeper, more robust understanding of the physics of deforming materials. It is a stepping stone, and an essential one, on the path to describing our complex, spinning, and stretching world.