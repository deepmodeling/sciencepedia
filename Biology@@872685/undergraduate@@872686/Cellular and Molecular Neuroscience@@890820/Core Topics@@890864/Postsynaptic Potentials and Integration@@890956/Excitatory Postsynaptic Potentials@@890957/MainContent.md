## Introduction
In the vast communication network of the brain, neurons must process a constant stream of information to make decisions. The fundamental 'go' signal in this process is the Excitatory Postsynaptic Potential (EPSP), a small electrical change that pushes a neuron closer to firing. While action potentials are the well-known output signals, they arise only after a [complex integration](@entry_id:167725) of these smaller, graded inputs. This article demystifies the EPSP, addressing how these tiny signals are generated, summed, and regulated to form the basis of [neuronal computation](@entry_id:174774). Across the following chapters, you will discover the core principles and mechanisms governing EPSPs, explore their diverse applications in [neuronal plasticity](@entry_id:191957) and network function, and engage with hands-on exercises to solidify your understanding. We begin by examining the fundamental properties that define an EPSP and the electrochemical events that bring it to life.

## Principles and Mechanisms

In the intricate communication network of the nervous system, the [fundamental unit](@entry_id:180485) of information is the action potential, an all-or-none electrical signal. However, the decision to generate such a signal is not made in isolation. It is the result of a complex process of integration, where a neuron continuously receives and sums up thousands of inputs, some excitatory and some inhibitory. The primary currency of excitation at the synapse is the **Excitatory Postsynaptic Potential (EPSP)**. This chapter delves into the fundamental principles governing the generation, propagation, and integration of EPSPs, which form the biophysical basis of [neural computation](@entry_id:154058).

### The Nature of an Excitatory Postsynaptic Potential

An EPSP is a transient, graded [depolarization](@entry_id:156483) of the postsynaptic [membrane potential](@entry_id:150996), initiated by the binding of an [excitatory neurotransmitter](@entry_id:171048) to its corresponding receptors. To fully appreciate its characteristics, it is instructive to contrast it with the action potential (AP), the neuron's output signal.

The most critical distinction lies in their amplitude characteristics. An EPSP is a **[graded potential](@entry_id:156224)**, meaning its amplitude is proportional to the intensity of the stimulus—for instance, the amount of neurotransmitter released into the synaptic cleft. A small amount of neurotransmitter will produce a small EPSP, while a larger amount will produce a larger one. In contrast, an action potential is an **all-or-none** event. Once the membrane potential at the [axon initial segment](@entry_id:150839) reaches a specific threshold, a full-sized action potential is generated, irrespective of the magnitude of the stimulus that pushed it over the threshold.

A second key difference is their method of propagation. An EPSP propagates **passively** (or **electrotonically**) from its point of origin at the synapse. As this local [depolarization](@entry_id:156483) spreads along the dendritic and somatic membrane, its amplitude decays with distance. This is analogous to an electrical signal weakening as it travels down a leaky cable. An action potential, however, propagates **actively** and **regeneratively**. The [depolarization](@entry_id:156483) of one patch of axonal membrane is sufficient to bring the adjacent patch to threshold, which then generates its own full-sized action potential. This process repeats along the entire length of the axon, ensuring that the signal propagates without any loss of amplitude [@problem_id:2336138].

### The Ionic Basis of Excitation

The generation of an EPSP is fundamentally an electrochemical event. In the majority of fast excitatory synapses in the vertebrate central nervous system, this event is mediated by the neurotransmitter **glutamate**. When glutamate is released from a [presynaptic terminal](@entry_id:169553), it diffuses across the [synaptic cleft](@entry_id:177106) and binds to specialized proteins on the postsynaptic membrane known as [ionotropic glutamate receptors](@entry_id:176453).

The primary receptor responsible for the initial, fast component of an EPSP is the **AMPA receptor** (α-amino-3-hydroxy-5-methyl-4-isoxazolepropionic acid receptor). Upon binding glutamate, the AMPA receptor undergoes a conformational change, opening an intrinsic [ion channel](@entry_id:170762). This channel is not perfectly selective; rather, it is permeable to both sodium ($Na^+$) and potassium ($K^+$) ions.

To understand why this leads to a depolarization, we must consider the electrochemical **driving force** on each ion. The driving force for an ion is the difference between the membrane potential ($V_m$) and that ion's **Nernst potential** (or [equilibrium potential](@entry_id:166921), $E_{ion}$). At a typical resting potential of approximately $-65$ mV, the situation is as follows:
- The Nernst potential for sodium ($E_{Na}$) is typically around $+60$ mV. The driving force on $Na^+$ is ($V_m - E_{Na}$), or approximately $-125$ mV, which strongly favors $Na^+$ influx.
- The Nernst potential for potassium ($E_K$) is typically around $-90$ mV. The driving force on $K^+$ is ($V_m - E_K$), or approximately $+25$ mV, which favors $K^+$ efflux.

Although the channel is open to both ions, the large inward driving force on $Na^+$ far outweighs the smaller outward driving force on $K^+$. The result is a net influx of positive charge, causing the membrane potential to become less negative—that is, to depolarize [@problem_id:2336123].

This leads to the concept of the **reversal potential ($E_{rev}$)** for the [synaptic current](@entry_id:198069). The reversal potential is the [membrane potential](@entry_id:150996) at which the net current through the channel is zero. It represents a weighted average of the equilibrium potentials of the permeant ions, weighted by their relative conductances ($g_{ion}$). The net current, $I_{syn}$, is the sum of the individual [ionic currents](@entry_id:170309):

$I_{syn} = I_{Na} + I_K = g_{Na}(V_m - E_{Na}) + g_K(V_m - E_K)$

At the reversal potential ($V_m = E_{rev}$), $I_{syn} = 0$:

$g_{Na}(E_{rev} - E_{Na}) + g_K(E_{rev} - E_K) = 0$

For typical AMPA receptors, the reversal potential is experimentally measured to be approximately $0$ mV. This value, lying between $E_K$ ($-90$ mV) and $E_{Na}$ ($+60$ mV), confirms that the channel is permeable to both ions. We can even use this information to deduce the [relative permeability](@entry_id:272081) of the channel. If we assume $E_{Na} = +60$ mV, $E_K = -90$ mV, and $E_{rev} = 0$ mV, we can solve for the ratio of the conductances, $\alpha = g_{Na}/g_K$:

$\alpha = \frac{g_{Na}}{g_K} = \frac{E_{rev} - E_K}{E_{Na} - E_{rev}} = \frac{0 - (-90)}{60 - 0} = 1.5$

This calculation reveals that the AMPA receptor channel is about 1.5 times more conductive to sodium than to potassium under these conditions [@problem_id:2336144]. Because the resting potential is far from this [reversal potential](@entry_id:177450), there is a strong net inward current upon channel opening, generating the EPSP.

### Quantifying the EPSP Amplitude

The magnitude of the depolarization during an EPSP can be predicted using a simple electrical model of the neuron. The passive cell membrane can be modeled as a resistor (representing the [leak ion channels](@entry_id:178024)) in parallel with a capacitor (representing the [lipid bilayer](@entry_id:136413)). In our analysis, we will focus on the steady-state, or peak, voltage achieved during the synaptic event.

At rest, the membrane potential $V_{rest}$ is determined solely by the leak conductance, $g_m$, and its [reversal potential](@entry_id:177450), which we can set to $E_L = V_{rest}$. When a synapse is activated, an additional [synaptic conductance](@entry_id:193384), $g_{syn}$, with its reversal potential, $E_{rev}$, is added in parallel. The total current across the membrane must sum to zero at the new steady-state potential, $V_{peak}$:

$g_m(V_{peak} - V_{rest}) + g_{syn}(V_{peak} - E_{rev}) = 0$

Solving for $V_{peak}$ yields the **chord conductance equation**:

$V_{peak} = \frac{g_m V_{rest} + g_{syn} E_{rev}}{g_m + g_{syn}}$

This elegant equation shows that the peak membrane potential is a weighted average of the resting and synaptic reversal potentials, with the conductances serving as the weights. The amplitude of the EPSP, $\Delta V$, is the difference between this [peak potential](@entry_id:262567) and the resting potential:

$\Delta V = V_{peak} - V_{rest} = \frac{g_{syn}(E_{rev} - V_{rest})}{g_m + g_{syn}}$

Consider a neuron with a resting potential of $-70.0$ mV, a [membrane conductance](@entry_id:166663) $g_m = 5.00$ nS, and a synaptic reversal potential $E_{rev} = 0.0$ mV. If a synaptic input opens channels with a total conductance of $g_{syn} = 1.00$ nS, the resulting EPSP amplitude would be:

$\Delta V = \frac{(1.00 \text{ nS})(0.0 \text{ mV} - (-70.0 \text{ mV}))}{5.00 \text{ nS} + 1.00 \text{ nS}} = \frac{70.0}{6.00} \text{ mV} \approx 11.7 \text{ mV}$

This demonstrates how the cell's intrinsic properties ($g_m$) and the strength of the synapse ($g_{syn}$) collectively determine the size of the [postsynaptic response](@entry_id:198985) [@problem_id:2336130].

Neurotransmitters are released in discrete packets called **quanta**, corresponding to the contents of a single [synaptic vesicle](@entry_id:177197). The spontaneous release of a single quantum gives rise to a **miniature EPSP (mEPSP)**, which can be considered the fundamental building block of [synaptic transmission](@entry_id:142801). The same principles apply, where $g_{syn}$ now represents the conductance of the channels opened by a single vesicle's worth of glutamate [@problem_id:2336125].

### Synaptic Integration: The Summation of EPSPs

A single EPSP, typically only a few millivolts in amplitude, is rarely sufficient to bring a neuron's membrane potential from rest to the firing threshold (which might be 15-20 mV more depolarized). Therefore, neurons must integrate multiple inputs arriving at different times and at different locations on their dendritic tree. This process of integration is known as **summation**.

#### Temporal Summation

**Temporal summation** occurs when multiple EPSPs arrive at the same synapse in rapid succession. If a second EPSP is triggered before the membrane potential has returned to rest from the first, the second [depolarization](@entry_id:156483) will add to the residual [depolarization](@entry_id:156483) of the first. The effectiveness of [temporal summation](@entry_id:148146) depends critically on the **[membrane time constant](@entry_id:168069) ($\tau_m$)**, a measure of how quickly the [membrane potential](@entry_id:150996) changes in response to a current. A longer time constant means the EPSP decays more slowly, providing a wider time window for subsequent EPSPs to summate effectively.

We can model this process. Imagine an EPSP is described by an instantaneous rise in voltage by $\Delta V_{max}$ followed by an exponential decay, $\Delta V(t) = \Delta V_{max} \exp(-(t-t_0)/\tau_m)$. If a first EPSP occurs at $t_1$ and a second identical one occurs at a later time $t_2$, the peak depolarization will occur just after the arrival of the second stimulus. The peak voltage change will be the sum of the full amplitude of the second EPSP and the remaining amplitude of the first:

$\Delta V_{peak} = \Delta V_{max} + \Delta V_{max} \exp\left(-\frac{t_2 - t_1}{\tau_m}\right)$

As the interval ($t_2 - t_1$) becomes smaller relative to $\tau_m$, the summation becomes more effective, approaching twice the amplitude of a single event [@problem_id:2336129].

#### Spatial Summation and its Complexities

**Spatial summation** is the process of combining EPSPs that originate at different synapses on the neuron's dendritic tree. As we have discussed, EPSPs are not transmitted with constant amplitude; they decay as they propagate passively towards the soma. This decay is described by the **passive [cable equation](@entry_id:263701)**, where the key parameter is the **[length constant](@entry_id:153012) ($\lambda$)**. The length constant represents the distance over which a steady-state voltage perturbation decays to approximately 37% ($1/e$) of its original amplitude. The voltage from a synapse at a distance $x$ from the soma, $\Delta V_{soma}$, is attenuated according to:

$\Delta V_{soma} = \Delta V_{local} \exp(-x/\lambda)$

Therefore, synapses located on distal [dendrites](@entry_id:159503) will have a smaller impact on the somatic [membrane potential](@entry_id:150996) than more proximal synapses, all else being equal. The neuron's ability to reach firing threshold thus depends not only on the number of active synapses but also on their spatial locations [@problem_id:2336140].

A further, crucial complexity arises when multiple synapses are active simultaneously. One might naively expect the combined EPSP to be the simple arithmetic sum of the individual EPSPs. However, this is not the case. Synaptic summation is inherently **non-linear**, or more specifically, **sublinear**.

Let's consider two synapses, A and B, which when activated alone each produce a 12 mV EPSP from a resting potential of -70 mV. The naive prediction is that when activated together, they will produce a 24 mV EPSP. The reality is different. The first EPSP (say, from synapse A) depolarizes the membrane from -70 mV to -58 mV. When synapse B is activated, the driving force for its current is no longer the initial $(V_{rest} - E_{rev})$ or $(-70 - 0) = -70$ mV. The driving force is now reduced to $(V_{peak,A} - E_{rev})$ or $(-58 - 0) = -58$ mV. Because the driving force is smaller, the current produced by synapse B is also smaller, and the additional depolarization it causes is less than the 12 mV it would have produced on its own. The total combined EPSP will therefore be significantly less than the 24 mV predicted by linear addition [@problem_id:2336152]. This shunting effect is a fundamental property of [synaptic integration](@entry_id:149097), ensuring that the neuron's response does not grow without bound as more inputs become active.

### Advanced Mechanisms and Regulation

#### The NMDA Receptor: A Molecular Coincidence Detector

While AMPA receptors mediate the fast, initial phase of an EPSP, another class of [glutamate receptor](@entry_id:164401), the **NMDA receptor** (N-methyl-D-aspartate receptor), plays a pivotal role in more complex phenomena like [synaptic plasticity](@entry_id:137631). The NMDA receptor is also a cation channel permeable to $Na^+$ and $K^+$, with a similar [reversal potential](@entry_id:177450) near 0 mV. However, it possesses a unique and critical property: its channel is subject to a **[voltage-dependent block](@entry_id:177221) by magnesium ions ($Mg^{2+}$)**.

At normal resting potentials, even when glutamate is bound to the receptor, an extracellular $Mg^{2+}$ ion sits within the channel pore, physically obstructing the flow of other ions. Consequently, at the very beginning of an EPSP, when the membrane is still hyperpolarized, NMDA receptors contribute very little to the postsynaptic current. However, if the postsynaptic membrane becomes sufficiently depolarized—typically by the strong initial current through co-localized AMPA receptors—the [electrostatic repulsion](@entry_id:162128) expels the $Mg^{2+}$ ion from the pore. This unblocking allows the NMDA channel to conduct current.

This dual requirement—presynaptic glutamate release and significant postsynaptic [depolarization](@entry_id:156483)—makes the NMDA receptor a powerful **coincidence detector**. It signals the simultaneous occurrence of both pre- and postsynaptic activity. Furthermore, a key feature of the NMDA receptor is its high permeability to calcium ions ($Ca^{2+}$). The influx of $Ca^{2+}$ acts as a potent second messenger, triggering [intracellular signaling](@entry_id:170800) cascades that can lead to long-lasting changes in synaptic strength, a process known as synaptic plasticity [@problem_id:2336145].

#### Termination of the Synaptic Signal

For synaptic communication to be precise, the neurotransmitter signal must be terminated rapidly. If glutamate were to linger in the synaptic cleft, receptors would remain activated, blurring the temporal boundaries between discrete signals. The primary mechanism for clearing glutamate from the [synaptic cleft](@entry_id:177106) is its rapid uptake by **glutamate transporters** (also known as Excitatory Amino Acid Transporters, or EAATs), which are located on the membrane of surrounding glial cells and, to some extent, on the [presynaptic terminal](@entry_id:169553) itself.

These transporters actively pump glutamate out of the cleft and into the cell, a process that is vital for maintaining low extracellular glutamate concentrations and preventing [excitotoxicity](@entry_id:150756). The functional importance of these transporters can be demonstrated pharmacologically. Applying a drug such as TBOA (threo-beta-benzyloxyaspartate), which selectively blocks glutamate transporters, has a dramatic effect on the EPSP. By preventing the rapid clearance of glutamate, the neurotransmitter remains in the [synaptic cleft](@entry_id:177106) for an extended period, continuously re-binding to postsynaptic receptors. This results in a significant prolongation of the [synaptic current](@entry_id:198069) and, consequently, a much longer-lasting EPSP [@problem_id:2336132]. This illustrates that the precise timing and shape of an EPSP are governed not only by receptor properties and membrane characteristics but also by the dynamics of [neurotransmitter clearance](@entry_id:169834).