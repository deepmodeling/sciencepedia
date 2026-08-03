## Introduction
Recent surveys of thousands of exoplanets have unveiled a curious feature in the cosmos: a distinct gap in the distribution of planetary sizes, known as the radius valley. This gap separates smaller, rocky super-Earths from larger, gas-enveloped sub-Neptunes, implying that a powerful physical process prevents planets from stably residing in this intermediate size range. Understanding the mechanism responsible for carving this valley is crucial for a [complete theory](@entry_id:155100) of [planet formation](@entry_id:160513) and evolution. This article explores a leading hypothesis: core-powered [mass loss](@entry_id:188886), where a planet's own internal heat drives the escape of its primordial atmosphere, and contrasts it with the competing [photoevaporation](@entry_id:1129620) model.

This exploration is divided into three parts. First, **Principles and Mechanisms** will delve into the physics of core-powered [mass loss](@entry_id:188886), explaining how a planet's cooling luminosity can fuel a powerful atmospheric outflow. Next, **Applications and Interdisciplinary Connections** will examine how astronomers use population-level data and detailed modeling to test this theory against its alternatives and connect it to broader questions in astrophysics. Finally, **Hands-On Practices** will provide you with the opportunity to derive the key [scaling relations](@entry_id:136850) that form the predictive backbone of this elegant model.

## Principles and Mechanisms

Imagine you are an astronomer cataloging thousands of newly discovered planets around distant stars. As you plot their sizes, a curious pattern emerges. There are plenty of small, dense worlds up to about one and a half times the size of Earth—we call these "super-Earths." There are also many larger, less dense planets, starting around twice Earth’s size and bigger—"sub-Neptunes." But in between, in a narrow band of sizes, there is a striking scarcity of planets. It’s as if nature has a preference, a rule that says planets can be small and rocky, or they can be large and gassy, but they are forbidden from comfortably residing in between. This cosmic puzzle is known as the **radius valley**.

This valley is not just a simple gap; it has structure. As we look at planets with longer orbital periods—those farther from their stars—the location of the valley drifts to slightly smaller sizes. This subtle slope is a profound clue, a fingerprint left by the physical process responsible for carving this feature into the planetary landscape . To decipher these clues, we must embark on a journey into the heart of a young planet, to uncover the engine that drives its evolution.

### An Engine from Within: The Fading Glow of a Newborn World

Where could the immense energy required to reshape a planet come from? One obvious source is the host star, which relentlessly bombards its planets with light and high-energy particles. This is indeed one important process, known as photoevaporation. But there is another, more intimate source of power: the planet’s own internal heat.

Planets are born from violent collisions in a swirling disk of gas and dust. This process leaves them with a tremendous reservoir of thermal energy, like a potato fresh from a very hot oven. A young planet glows, not just with reflected starlight, but with its own primordial heat. Over billions of years, this heat must escape into the cold of space. This slow, majestic process of cooling and [gravitational contraction](@entry_id:160689) is known as **Kelvin-Helmholtz cooling** . The rate at which this energy leaks out is the planet's **internal luminosity**, denoted by the symbol $L$. This quiet, persistent glow, an echo of the planet's fiery birth, is the engine that can power its transformation .

The total thermal energy stored within the planet, let’s call it $E_{\mathrm{th}}$, is the fuel for this engine. The characteristic time over which this fuel is consumed is the **Kelvin-Helmholtz timescale**, defined simply as $t_{\mathrm{KH}} \approx \frac{E_{\mathrm{th}}}{L}$. This timescale tells us, roughly, how long the planet can sustain its internal glow before significantly cooling down.

### The Great Escape: Turning Heat into an Outflow

An engine is useless without a mechanism to do work. For a planet, the work to be done is lifting its own atmosphere against the relentless pull of gravity. The internal luminosity provides the means. As heat flows from the hot, deep interior through the upper atmosphere, it energizes the gas. This energy performs **$P\,dV$ work**—the same principle that drives a piston in an engine—causing the atmosphere to expand and flow outwards. This is not a gentle evaporation, but a powerful, continuous hydrodynamic wind, a planetary-scale river of gas flowing into the cosmos .

How effective is this process? We can get a surprisingly deep insight from a simple argument of energy conservation, a technique beloved by physicists called dimensional analysis. The power required to lift gas away from a planet is the mass-loss rate, $\dot{M}$ (mass per unit time), multiplied by the energy needed to escape per unit mass. This [escape energy](@entry_id:177133) is set by the planet’s gravitational potential, which is proportional to $\frac{G M}{R}$, where $G$ is the [gravitational constant](@entry_id:262704), $M$ is the planet's mass, and $R$ is its radius.

The power supplied by our engine is the internal luminosity, $L$. If we assume that a significant fraction of this power goes into driving the escape, we can set the two rates to be proportional:
$$
\dot{M} \times \frac{G M}{R} \propto L
$$
Rearranging this gives a beautiful and powerful scaling for the mass-loss rate:
$$
\dot{M} \propto \frac{L R}{G M}
$$
This simple formula is a revelation . It tells us that planets lose their atmospheres faster if they are more luminous ($L$), larger in size ($R$), and less massive ($M$). This makes intuitive sense: a stronger engine, a less steep hill to climb, and less material to hold onto all favor escape. As a planet cools and contracts over time, both $L$ and $R$ decrease, meaning the [mass loss](@entry_id:188886) is "front-loaded," occurring most vigorously when the planet is young and hot, and naturally quenching as it ages.

### The Atmospheric Gatekeeper

If the story ended there, every planet would simply cool and lose some of its atmosphere. But the existence of two distinct populations—super-Earths and sub-Neptunes—tells us there must be a fork in the road. What determines which path a planet takes? The answer lies in the atmosphere itself, which acts as a gatekeeper, regulating its own escape.

The atmosphere’s ability to trap heat is determined by its **opacity**, $\kappa$. A more opaque atmosphere is like a thicker blanket, holding in the planet’s internal heat more effectively. A planet's interior is typically convective, like a pot of boiling water, with heat being churned around efficiently. However, the outer layers are radiative, meaning heat must diffuse its way out photon by photon. This radiative layer is the bottleneck for cooling. The physics of this bottleneck, at what is called the **radiative-convective boundary (RCB)**, ultimately sets the planet’s luminosity, $L$ .

The relationship is simple and profound: the luminosity is inversely proportional to the opacity at this boundary, $L \propto \frac{1}{\kappa}$. A more opaque atmosphere (higher $\kappa$) reduces the internal luminosity, slowing the cooling process and throttling the very engine that powers atmospheric escape. In this way, the planet's destiny is tied to the properties of the blanket it wears.

### The Fork in the Road: All or Nothing

We can now assemble the pieces of the puzzle to understand how the radius valley is carved. Imagine a population of newly formed planets. Each consists of a rocky core and a primordial hydrogen and helium envelope, which we can characterize by its mass fraction, $f_{\mathrm{env}}$.

A planet’s fate is determined by a cosmic battle between two energies. On one side is the total energy required to unbind the envelope, the **binding energy**, $E_{\mathrm{bind}}$. This is the energy cost to lift the entire atmosphere out of the planet's gravity well. Naturally, this is proportional to how much atmosphere there is: $E_{\mathrm{bind}} \propto f_{\mathrm{env}}$.

On the other side is the total energy the planet's internal engine can supply over its lifetime, which we can call the **cooling energy**, $E_{\mathrm{cool}}$. This is the integrated luminosity over billions of years.

The outcome is a dramatic "all-or-nothing" scenario . For any given planet, there is a **critical envelope fraction**, $f_{\mathrm{crit}}$, where the available energy exactly matches the required energy ($E_{\mathrm{cool}} = E_{\mathrm{bind}}$).

-   If a planet is born with an envelope lighter than this critical value ($f_{\mathrm{env}}  f_{\mathrm{crit}}$), it has more than enough energy to drive off its entire atmosphere. Over time, it is stripped bare, leaving behind a rocky super-Earth. Its final radius is just the radius of its core.

-   If a planet is born with an envelope heavier than this critical value ($f_{\mathrm{env}} > f_{\mathrm{crit}}$), its internal engine is insufficient for the task. It will lose some gas, but it ultimately retains a substantial atmosphere, remaining a puffy sub-Neptune.

This sharp, [binary outcome](@entry_id:191030) is the key. An initially smooth, [continuous distribution](@entry_id:261698) of envelope fractions is sculpted by this process into two distinct final states. There is no stable middle ground. A planet that starts losing its atmosphere finds the remaining, smaller envelope even easier to remove, leading to a runaway process that doesn't stop until the gas is gone. This explains why we find so few planets in the valley—they are merely transient objects, caught fleetingly in the process of transformation from a sub-Neptune to a super-Earth  .

### The Cosmic Clock and the Sloping Valley

This evolutionary story unfolds over gigayear timescales, a drama written by the interplay of three cosmic clocks: the **cooling timescale** ($t_{\mathrm{cool}}$), the **mass-loss timescale** ($t_{\mathrm{ml}}$), and the **age of the system** ($t_{\star}$). A deep insight of the core-powered mass loss model is that the energy available to be radiated ($E_{\mathrm{th}}$) is itself proportional to the binding energy of the envelope that is being lost. This forges a fundamental link between the two internal timescales: $t_{\mathrm{cool}} \approx t_{\mathrm{ml}}$ .

For this process to shape a population of planets that we observe today (which are typically billions of years old), the characteristic timescale of the transformation must be comparable to the age of the stars. Therefore, the planets found at the edge of the valley—those right at the tipping point—are the ones for which $t_{\mathrm{ml}} \approx t_{\mathrm{cool}} \lesssim t_{\star}$. This beautiful piece of [temporal reasoning](@entry_id:896426) explains why the valley is a prominent feature in the mature planetary systems we survey .

This framework also elegantly explains the valley's slope. Planets on tight, short-period orbits are heated more by their star. Their higher equilibrium temperature, $T_{\mathrm{eq}}$, makes their atmospheric "blanket" more transparent, allowing the internal luminosity $L$ to escape more efficiently. A higher $L$ provides more power for stripping the atmosphere. Consequently, a planet on a short-period orbit can shed a more massive initial envelope than an identical planet on a long-period orbit. This means the critical envelope fraction, $f_{\mathrm{crit}}$, is larger at shorter periods.

Since a larger envelope fraction corresponds to a larger planetary radius, the valley—which marks this transition—is located at larger radii for short-period planets and smaller radii for long-period planets. This creates the observed negative slope. Incredibly, a simple physical model based on these principles predicts a slope of $d\log R / d\log P \approx -1/9$. This prediction matches the observed slope from Kepler data, which is about $-0.09$, providing stunning confirmation of the theory .

### The Final Whimper

What marks the end of this epic transformation? The core-powered wind does not blow forever. As the planet cools, its luminosity dwindles. As the atmosphere thins, its density drops. At a certain point, the atmosphere becomes so tenuous that it no longer behaves like a continuous fluid. The powerful, hydrodynamic outflow chokes and ceases.

The escape mechanism transitions to a much gentler process known as **Jeans escape**. In this regime, only the rare, fastest-moving individual atoms at the very top of the atmosphere—those in the high-velocity tail of the Maxwell-Boltzmann distribution—happen to be moving upward fast enough to overcome gravity. The mass-loss rate drops by many orders of magnitude, becoming utterly negligible . This effective "shutoff" solidifies the planet’s fate, locking it into one of the two stable states: a bare, rocky core or a puffy, gas-rich world. The great escape ends not with a bang, but with a final, quiet whimper, leaving behind the permanent, silent testament of the radius valley.