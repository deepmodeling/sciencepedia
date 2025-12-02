## Introduction
While the fundamental laws of physics are often expressed as smooth, continuous equations, our world is full of sharp boundaries and abrupt transitions—from [shock waves](@entry_id:142404) to the interface between different materials. How do we reconcile the language of continuity with the reality of discontinuity? This article addresses this gap by introducing the powerful concept of **jump conditions**. These are a set of rules, derived not from local differential laws which break down at an interface, but from the unwavering principles of conservation. By adhering to the [conservation of mass](@entry_id:268004), momentum, and energy, we can bridge the divide and precisely describe the behavior of physical systems at their most dramatic points of change. In the following sections, you will first explore the theoretical foundation in "Principles and Mechanisms," learning how the simple logic of conservation yields the mathematical form of jump conditions. Subsequently, "Applications and Interdisciplinary Connections" will demonstrate the remarkable universality of these principles, showing how they govern everything from supersonic jets and [composite materials](@entry_id:139856) to computational simulations and astrophysical phenomena.

## Principles and Mechanisms

### The Logic of Conservation: Thinking with Pillboxes

Let's begin with the simplest idea: what goes in must come out, unless it is created or destroyed on the spot. This is the essence of a conservation law. To see how this helps us deal with a jump, imagine a razor-thin boundary, which we'll call $\mathcal{S}$, separating two different regions, say region 1 and region 2. This could be the interface between steel and aluminum [@problem_id:2695068], or the surface of a shock wave in the air.

Now, let's perform a thought experiment. We construct a tiny, imaginary "pillbox"—a flat cylinder with its top face in region 2, its bottom face in region 1, and its thin side wall crossing the boundary, as shown in Figure 1.


*Figure 1: The 'pillbox' method. An infinitesimal [control volume](@entry_id:143882) is used to analyze the fluxes across a [surface of discontinuity](@entry_id:180188) $\mathcal{S}$. As the height of the pillbox shrinks to zero, the only contributions that remain are from the fluxes across the top and bottom faces and any sources on the interface itself.*