## Introduction
In the study of how materials deform, from the stretching of a rubber band to the flow of tectonic plates, a fundamental challenge arises: how do we describe physical laws in a way that is independent of the observer? The laws of nature should not change whether we observe them from a stationary lab or a spinning spacecraft. This [principle of material frame-indifference](@article_id:187994) is a cornerstone of [continuum mechanics](@article_id:154631), yet it presents a significant problem when we try to measure how stress changes over time. The most intuitive measure, the [material time derivative](@article_id:190398) of stress, fails this test, as its value is contaminated by the observer's own rotation.

This article addresses this critical knowledge gap by exploring the concept of [objective stress rates](@article_id:198788), which are mathematical tools designed to provide a true, observer-independent measure of stress change. It focuses on one of the most powerful and physically insightful of these tools: the Truesdell rate. Across two chapters, you will gain a deep understanding of this essential concept.
- The **Principles and Mechanisms** chapter will unravel the "observer problem," introduce simpler objective rates like the Jaumann rate, and then derive the Truesdell rate, highlighting its unique structure and physical meaning.
- The **Applications and Interdisciplinary Connections** chapter will demonstrate the Truesdell rate's practical superiority in [predictive modeling](@article_id:165904), its foundational role in modern computational simulations, and its relevance in fields beyond solid mechanics, such as the study of non-Newtonian fluids.

## Principles and Mechanisms
Imagine you’re on a fast-spinning merry-go-round, trying to describe the elegant swirl of cream you just poured into your coffee. To you, the cream seems to be flying outwards, pushed by some mysterious force, while its path curves in a baffling way. Someone standing on the ground, however, sees a much simpler picture: the cream is just moving with the rotating coffee, slowly mixing in. The fundamental physics governing the fluid—its viscosity, density, and how it resists being stirred—hasn't changed. The only thing that has changed is you, the observer. The laws of nature must be written in a way that they look the same for both you and the person on the ground. This powerful idea is called the **[principle of material frame-indifference](@article_id:187994)**, or more simply, **objectivity**. In the world of materials, it is not just a philosophical preference; it is a strict requirement for any physical law. [@problem_id:2550539]

### The Observer Problem: A Universe in Spin

When we study how materials deform—a steel [beam bending](@article_id:199990) under a load, a polymer stretching, or a tectonic plate shifting—we need to write down constitutive laws that relate the forces within the material (**stress**) to its deformation rate (**[strain rate](@article_id:154284)**). We want to understand how the stress changes over time. The most obvious way to describe a change in stress, $\boldsymbol{\sigma}$, is to simply take its time derivative, which we write as $\dot{\boldsymbol{\sigma}}$. This is what we call the **[material time derivative](@article_id:190398)**; it tells us how stress changes for a tiny piece of material as it moves and deforms.

But here we run into the merry-go-round problem. It turns out that this simple, intuitive derivative is not objective. If you, the observer, decide to rotate your frame of reference while a material is deforming, the $\dot{\boldsymbol{\sigma}}$ you measure will be different from what a stationary observer measures. Your own rotation "contaminates" the measurement. Mathematically, if a new observer is rotating with a spin $\boldsymbol{\Omega}$ relative to the old one, the new time derivative $\dot{\boldsymbol{\sigma}}^\ast$ is related to the old one by:

$$
\dot{\boldsymbol{\sigma}}^{\ast} = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}
$$

where $\boldsymbol{Q}$ is the [rotation tensor](@article_id:191496) relating the two frames. An objective quantity should transform simply as $\boldsymbol{A}^\ast = \boldsymbol{Q}\boldsymbol{A}\boldsymbol{Q}^{\mathsf{T}}$. The two extra terms, $\boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}$, are the problem. They are artifacts of the observer's spin, not a real physical change in the material's stress state. A constitutive law built on $\dot{\boldsymbol{\sigma}}$ would predict different material behaviors depending on how the scientist chose to spin—a clear absurdity. [@problem_id:2905931]

### The Corotational Correction: Taming the Spin

How do we fix this? The key is to define a "smarter" derivative that is immune to the observer's spin. The idea is to measure the rate of change of stress in a coordinate system that spins along *with the material itself*. This is called a **corotational frame**. By doing this, we can cancel out the non-objective rotational effects.

One of the most famous ways to do this leads to the **Zaremba–Jaumann rate** (or simply Jaumann rate). We take the [material time derivative](@article_id:190398) $\dot{\boldsymbol{\sigma}}$ and add correction terms based on the material's own rate of rotation, which is described by the **[spin tensor](@article_id:186852)**, $\boldsymbol{W}$. The [spin tensor](@article_id:186852) $\boldsymbol{W}$ is the skew-symmetric part of the [velocity gradient](@article_id:261192) $\boldsymbol{L}$. The definition is:

$$
\overset{\mathrm{J}}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$

The magic here is that the [spin tensor](@article_id:186852) $\boldsymbol{W}$ transforms in just the right way to cancel out the pesky $\boldsymbol{\Omega}$ terms from the observer's rotation. The Jaumann rate $\overset{\mathrm{J}}{\boldsymbol{\sigma}}$ is thus **objective**. We can build constitutive laws with it, confident that our physical predictions won't change if we happen to be on a merry-go-round. The Jaumann rate is just one of many possible objective rates; others, like the **Green–Naghdi rate**, use different measures of the material's spin but achieve the same goal of objectivity. [@problem_id:2905949] [@problem_id:2886962]

### A Tale of Two Stresses: Unveiling the Truesdell Rate

So, are we done? We have objective rates. Why the need for anything else? This is where the profound insight of Clifford Truesdell, one of the founders of modern [continuum mechanics](@article_id:154631), comes into play. He argued that deformation is more than just spinning. It also involves stretching and, importantly, changes in volume.

The **Cauchy stress**, $\boldsymbol{\sigma}$, is defined as force per *current* area. When a material is compressed or stretched, its volume and density change. This means the very area over which the force is distributed is changing. Shouldn't a truly comprehensive stress rate account for this effect?

To build such a rate, we can use a clever conceptual device. Let's define a different stress measure, the **Kirchhoff stress**, $\boldsymbol{\tau}$, as:

$$
\boldsymbol{\tau} = J\boldsymbol{\sigma}
$$

where $J$ is the ratio of the current volume of a piece of material to its original volume. You can think of the Kirchhoff stress as a "volume-weighted" version of the Cauchy stress.

Now, a very natural objective rate in [continuum mechanics](@article_id:154631) is the **Oldroyd upper-convected derivative**, which is defined for any tensor $\boldsymbol{A}$ as $\dot{\boldsymbol{A}}^{\nabla}=\dot{\boldsymbol{A}}-\boldsymbol{L}\boldsymbol{A}-\boldsymbol{A}\boldsymbol{L}^{\mathsf{T}}$. It accounts for changes due to the full **velocity gradient**, $\boldsymbol{L}$, which includes both stretching ($\boldsymbol{D}$) and spin ($\boldsymbol{W}$). Let's apply this robust rate to our Kirchhoff stress $\boldsymbol{\tau}$.

The **Truesdell rate** of the Cauchy stress, denoted $\overset{\triangle}{\boldsymbol{\sigma}}$, is then defined as the rate that is consistent with the Oldroyd rate of the Kirchhoff stress, scaled by the volume change $J$. That is, we demand:

$$
J\,\overset{\triangle}{\boldsymbol{\sigma}} = \boldsymbol{\tau}^{\nabla} = \dot{\boldsymbol{\tau}} - \boldsymbol{L}\boldsymbol{\tau} - \boldsymbol{\tau}\boldsymbol{L}^{\mathsf{T}}
$$

This might look like just a mathematical definition, but it's a profound physical statement. We are defining the "correct" rate of Cauchy stress by linking it to the rate of a stress measure that is already connected to volume changes. Now, we can unveil the Truesdell rate. We substitute $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ and use the kinematic identity $\dot{J} = J\,\mathrm{tr}(\boldsymbol{L})$ (which states that the rate of volume change is related to the trace of the [velocity gradient](@article_id:261192)). After some calculus, the $J$s cancel out, and we are left with a beautiful and revealing expression [@problem_id:2666484] [@problem_id:2609664]:

$$
\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^{\mathsf{T}} + (\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}
$$

This is the Truesdell rate. The first three terms are the Oldroyd rate of $\boldsymbol{\sigma}$. The final term, $(\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}$, is the crucial addition. It arises directly from the time derivative of the volume ratio $J$. Since $\mathrm{tr}\,\boldsymbol{L}$ represents the rate of [volume expansion](@article_id:137201) of the material, this term explicitly accounts for how the changing density of the material affects the stress. For a purely dilatational motion, where the material expands or contracts uniformly without changing shape, this term plays a central role. [@problem_id:2609664]

### What's the Difference? Stretching vs. Spinning

We now have two objective rates, Jaumann and Truesdell. What is the fundamental difference between them? We can find out by simply subtracting one from the other. After using the decomposition $\boldsymbol{L} = \boldsymbol{D}+\boldsymbol{W}$ (where $\boldsymbol{D}$ is the symmetric rate-of-deformation, or stretching, tensor), the math reveals a wonderfully clear result:

$$
\overset{\triangle}{\boldsymbol{\sigma}} - \overset{\mathrm{J}}{\boldsymbol{\sigma}} = (\mathrm{tr}\,\boldsymbol{D})\boldsymbol{\sigma} - (\boldsymbol{D}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{D})
$$

Notice what's missing: the [spin tensor](@article_id:186852) $\boldsymbol{W}$. The entire difference between the two rates depends only on the **stretching** part of the motion, $\boldsymbol{D}$, and the stress state $\boldsymbol{\sigma}$. [@problem_id:2666095] [@problem_id:2666501]

This tells us everything. The Jaumann rate is a minimal correction; it only accounts for the material's spin. The Truesdell rate does more: it accounts for spin *and* stretching. The two rates are only identical if the material is not deforming ($\boldsymbol{D}=\boldsymbol{0}$) or if the stretching and stress satisfy the special condition $(\mathrm{tr}\,\boldsymbol{D})\boldsymbol{\sigma} = \boldsymbol{D}\boldsymbol{\sigma} + \boldsymbol{{sigma}}\boldsymbol{D}$. In all other cases, they give different answers, reflecting their different physical underpinnings.

### The Deeper Meaning: Coupling Shape and Size

The final piece of the puzzle reveals the deepest physical consequence. Any stress state can be split into two parts: a **spherical** (or hydrostatic) part, $p\boldsymbol{I}$, which represents pressure and relates to changes in volume (size), and a **deviatoric** part, $\boldsymbol{s}$, which relates to shear and changes in shape. So, $\boldsymbol{\sigma} = p\boldsymbol{I} + \boldsymbol{s}$.

When we apply the Jaumann rate to this decomposed stress, we find that it keeps the two parts neatly separate. The rate of change of the spherical part depends only on $\dot{p}$, and the rate of change of the deviatoric part depends only on $\dot{\boldsymbol{s}}$ and $\boldsymbol{s}$. There is no cross-talk.

The Truesdell rate, however, is different. Because its definition includes the stretching tensor $\boldsymbol{D}$, it **couples** the spherical and deviatoric responses. The rate of change of pressure can be influenced by the [deviatoric stress](@article_id:162829) $\boldsymbol{s}$, and the rate of change of the [deviatoric stress](@article_id:162829) is influenced by the pressure $p$. For instance, in a simple shear flow, which is a pure shape-changing motion, the difference between the Truesdell and Jaumann deviatoric rates can depend directly on the pressure $p$ in the material. [@problem_id:2666515]

This coupling is not a mathematical artifact; it reflects a potential physical reality. For many materials, compressing them (increasing pressure) makes them stiffer and more resistant to shearing. The Truesdell rate provides a natural framework to capture this type of behavior. The choice between the Jaumann, Truesdell, or other objective rates is not just a matter of taste; it is a constitutive choice that embeds different assumptions about the fundamental behavior of the material itself. The journey from a spinning coffee cup to these subtle distinctions in [tensor calculus](@article_id:160929) reveals a core principle of physics: the search for a description of nature that is independent of the observer often leads us to a deeper understanding of the thing being observed.