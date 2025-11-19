## Introduction
Modal logic provides a powerful formal framework for reasoning about different modes of truth, such as necessity, possibility, knowledge, and obligation. While [classical logic](@entry_id:264911) deals with what is simply true or false, [modal logic](@entry_id:149086) extends this capacity to analyze statements like "it is necessary that $p$" or "it is possible that $p$." However, moving from these intuitive ideas to a rigorous system requires a solid foundation. This article addresses the need for a systematic development of **normal modal logics**, the most widely studied and applied family of modal systems.

Over the course of three chapters, we will build this foundation from the ground up. The first chapter, **Principles and Mechanisms**, introduces the formal language of [modal logic](@entry_id:149086), the elegant [possible worlds semantics](@entry_id:152177) developed by Saul Kripke, and the axiomatic system K that serves as the bedrock for all normal modal logics. The second chapter, **Applications and Interdisciplinary Connections**, explores the remarkable versatility of this framework, demonstrating its use in modeling knowledge in philosophy and AI, analyzing provability in mathematics, and describing computational processes in computer science. Finally, the **Hands-On Practices** chapter provides concrete exercises to solidify your understanding of these core theoretical concepts. By the end, you will have a comprehensive grasp of the principles, mechanisms, and applications that make normal modal logics an indispensable tool in modern logic and beyond.

## Principles and Mechanisms

Having introduced the conceptual motivations for [modal logic](@entry_id:149086), we now turn to a rigorous examination of its formal principles and semantic mechanisms. This chapter will construct the foundations of normal modal logics, beginning with their formal language, followed by the elegant relational semantics developed by Saul Kripke. We will then define the minimal normal [modal logic](@entry_id:149086), known as **K**, and explore the pivotal concepts of validity, [logical consequence](@entry_id:155068), and the rules that govern modal reasoning. Finally, we will culminate in the central metalogical results of correspondence and completeness, which connect the syntactic and semantic realms and demonstrate the power of the axiomatic method.

### The Language of Modal Logic

The first step in formalizing any logical system is to define its language with absolute precision. The language of propositional [modal logic](@entry_id:149086), which we can denote as $\mathcal{L}_{\Box}$, is an extension of the language of classical [propositional logic](@entry_id:143535). Its vocabulary consists of a [countable set](@entry_id:140218) of **propositional variables** (e.g., $p, q, r, \dots$), the standard **Boolean connectives** (e.g., $\neg$ for negation and $\to$ for [material implication](@entry_id:147812)), and a new unary operator, $\Box$, called the **necessity operator**.

The [well-formed formulas](@entry_id:636348) (WFFs) of $\mathcal{L}_{\Box}$ are defined inductively. This is done by specifying the atomic components and the rules for building more complex formulas from simpler ones. Formally, the set of formulas is the smallest set satisfying the following conditions [@problem_id:3047620]:

1.  Every propositional variable $p$ is a formula.
2.  If $\varphi$ is a formula, then $\neg\varphi$ is a formula.
3.  If $\varphi$ and $\psi$ are formulas, then $(\varphi \to \psi)$ is a formula.
4.  If $\varphi$ is a formula, then $\Box\varphi$ is a formula.

Other Boolean connectives, such as conjunction ($\wedge$), disjunction ($\vee$), and the [biconditional](@entry_id:264837) ($\leftrightarrow$), can be introduced as abbreviations in the usual way (e.g., $(\varphi \wedge \psi)$ abbreviates $\neg(\varphi \to \neg\psi)$).

A crucial feature of [modal logic](@entry_id:149086) is the duality between necessity and possibility. The necessity operator, $\Box$, corresponds to the locution "it is necessary that...". Its dual, the **possibility operator** $\Diamond$, corresponds to "it is possible that...". Intuitively, a proposition is possible if and only if its negation is not necessary. This intuition is captured by defining $\Diamond$ as an abbreviation within the language:

$\Diamond\varphi := \neg\Box\neg\varphi$

This definition means that the $\Diamond$ operator does not add any fundamental [expressive power](@entry_id:149863) to our language; any statement involving $\Diamond$ can be translated into an equivalent statement using only $\Box$. When we treat a language with both $\Box$ and $\Diamond$ as primitive, the equivalence $\Diamond\varphi \leftrightarrow \neg\Box\neg\varphi$ is typically included as a foundational axiom. An extension of a system that merely introduces such defined abbreviations is known as a **conservative extension**, as it does not allow for the proof of any new theorems that could not already be expressed and proven in the original, more parsimonious language [@problem_id:3047620]. This duality is a cornerstone of all normal modal logics and is independent of any specific axioms governing the behavior of necessity, holding true even in the most basic systems [@problem_id:3047620].

### Kripke Semantics: Models for Modal Logic

To give our [formal language](@entry_id:153638) meaning, we employ a semantic framework. The standard approach for [modal logic](@entry_id:149086) is **Kripke semantics**, which formalizes the intuitive idea of "possible worlds." In this framework, modal operators are interpreted as [quantifiers](@entry_id:159143) over a set of such worlds.

The underlying structure of a Kripke model is the **Kripke frame**, defined as a pair $\mathcal{F} = (W, R)$, where:
-   $W$ is a non-[empty set](@entry_id:261946), whose elements are called **worlds** or states.
-   $R$ is a [binary relation](@entry_id:260596) on $W$ (i.e., a subset $R \subseteq W \times W$), called the **[accessibility relation](@entry_id:149013)**. The expression $wRv$ can be read as "world $v$ is accessible from world $w$," or "$v$ is a possible future of $w$."

For the general definition of a Kripke frame, no special properties (like reflexivity or transitivity) are imposed on the relation $R$. Such properties will be introduced later to characterize specific modal logics.

A frame provides the relational structure, but to evaluate formulas containing propositional variables, we need to know which atomic propositions are true in which worlds. This is the role of the valuation. A **Kripke model** is a triple $\mathcal{M} = (W, R, V)$, where $(W, R)$ is a Kripke frame and $V$ is a **valuation function**. There are several equivalent ways to define $V$ [@problem_id:3047632]:
-   As a function $V: \mathsf{Prop} \to \mathcal{P}(W)$, mapping each propositional variable $p$ to the set of worlds where $p$ is true.
-   As a function $V: W \to \mathcal{P}(\mathsf{Prop})$, mapping each world $w$ to the set of propositional variables true at $w$.
-   As a function $V: W \times \mathsf{Prop} \to \{0, 1\}$, where $V(w, p) = 1$ signifies that $p$ is true at $w$.

With a model in hand, we can define the **satisfaction relation**, written $\mathcal{M}, w \models \varphi$, which reads "the formula $\varphi$ is true at world $w$ in model $\mathcal{M}$." The relation is defined recursively on the structure of $\varphi$:
-   $\mathcal{M}, w \models p$ if and only if $p$ is true at $w$ according to the valuation $V$ (e.g., $w \in V(p)$ for the first type of valuation).
-   $\mathcal{M}, w \models \neg\varphi$ if and only if it is not the case that $\mathcal{M}, w \models \varphi$.
-   $\mathcal{M}, w \models \varphi \to \psi$ if and only if (if $\mathcal{M}, w \models \varphi$, then $\mathcal{M}, w \models \psi$).

The modal clauses are what give Kripke semantics its distinctive character. They interpret the modal operators as quantifiers over the worlds made available by the [accessibility relation](@entry_id:149013):
-   $\mathcal{M}, w \models \Box\varphi$ if and only if for all worlds $v \in W$, if $wRv$, then $\mathcal{M}, v \models \varphi$.
-   $\mathcal{M}, w \models \Diamond\varphi$ if and only if there exists a world $v \in W$ such that $wRv$ and $\mathcal{M}, v \models \varphi$.

In words, $\Box\varphi$ is true at a world $w$ if $\varphi$ is true in *all* worlds accessible from $w$. $\Diamond\varphi$ is true at $w$ if $\varphi$ is true in *at least one* world accessible from $w$. The semantic clause for $\Diamond$ can be derived directly from its definition as $\neg\Box\neg\varphi$ and the semantic clause for $\Box$ [@problem_id:3047620]. This semantic duality perfectly mirrors the syntactic definition and the duality between universal and existential [quantifiers](@entry_id:159143) in [first-order logic](@entry_id:154340).

### Proof Theory: The Minimal Normal Modal Logic K

While semantics provides a notion of truth, [proof theory](@entry_id:151111) provides a notion of provability. A central goal of logic is to ensure these two notions coincide. The most common proof-theoretic framework for [modal logic](@entry_id:149086) is the **Hilbert-style system**.

A [modal logic](@entry_id:149086) is called **normal** if its set of provable formulas (theorems) contains all classical propositional [tautologies](@entry_id:269630), includes a specific axiom for the distribution of necessity over implication, and is closed under the [inference rules](@entry_id:636474) of Modus Ponens and Necessitation [@problem_id:3047636].

The minimal (or weakest) normal [modal logic](@entry_id:149086) is named **K** in honor of Saul Kripke. It is defined as the smallest set of formulas satisfying the following conditions:

**Axiom Schemas:**
1.  All instances of classical propositional [tautologies](@entry_id:269630) (e.g., $\varphi \to (\psi \to \varphi)$).
2.  **The K axiom (or Distribution Axiom):** $\Box(\varphi \to \psi) \to (\Box\varphi \to \Box\psi)$.

**Rules of Inference:**
1.  **Modus Ponens (MP):** From $\varphi$ and $\varphi \to \psi$, infer $\psi$.
2.  **Necessitation (Nec):** From a theorem $\vdash \varphi$, infer $\vdash \Box\varphi$.

The K axiom is the cornerstone of normal modal systems. It states that if it is necessary that $\varphi$ implies $\psi$, and if $\varphi$ is necessary, then $\psi$ must also be necessary. This principle of distribution is fundamental to how we reason about necessity.

The rules of inference allow us to generate new theorems from axioms. Modus Ponens is the standard rule from [propositional logic](@entry_id:143535). Necessitation is unique to [modal logic](@entry_id:149086) and is a topic we will explore in depth. These components define the system K. From them, we can derive further rules. For instance, the **Rule of Regularity** (or Monotonicity) states that if $\varphi \to \psi$ is a theorem, then so is $\Box\varphi \to \Box\psi$. This is easily derivable in K [@problem_id:3047636]:

1.  $\vdash \varphi \to \psi$ (Premise, a theorem of K)
2.  $\vdash \Box(\varphi \to \psi)$ (By Necessitation on 1)
3.  $\vdash \Box(\varphi \to \psi) \to (\Box\varphi \to \Box\psi)$ (Instance of K axiom)
4.  $\vdash \Box\varphi \to \Box\psi$ (By Modus Ponens on 2 and 3)

### Validity, Consequence, and the Power of Necessitation

With both a [proof system](@entry_id:152790) (K) and a semantic framework (Kripke models) established, we can explore the relationship between provability and truth. A central concept in semantics is **validity**.

-   A formula $\varphi$ is **valid in a model** $\mathcal{M}=(W, R, V)$, written $\mathcal{M} \models \varphi$, if it is true at every world in that model: $\forall w \in W, \mathcal{M}, w \models \varphi$.
-   A formula $\varphi$ is **valid in a frame** $\mathcal{F}=(W, R)$, written $\mathcal{F} \models \varphi$, if it is valid in every model based on that frame: $\forall V, \mathcal{M} \models \varphi$ where $\mathcal{M}=(\mathcal{F}, V)$ [@problem_id:3047621]. Validity in a frame means the formula's truth is a consequence of the frame's relational structure alone, independent of how atomic facts are assigned.
-   A formula $\varphi$ is **valid over a class of frames** $\mathcal{C}$ if it is valid in every frame in $\mathcal{C}$. When the class is all possible Kripke frames, we simply say $\varphi$ is **valid** and write $\models \varphi$.

The K axiom, $\Box(\varphi \to \psi) \to (\Box\varphi \to \Box\psi)$, is not just an arbitrary choice; it is valid on *every* Kripke frame, making it a fundamental law of modal reasoning in this semantic setting [@problem_id:3047621]. This provides a powerful semantic justification for its inclusion as an axiom in the minimal logic K.

The Rule of Necessitation also has a precise semantic justification. The rule states: from $\vdash \varphi$, infer $\vdash \Box\varphi$. Semantically, this corresponds to the principle: if $\models \varphi$, then $\models \Box\varphi$. The proof is illuminating. To say $\models \varphi$ means that $\varphi$ is true in *every* world of *every* model. Now, to check if $\models \Box\varphi$, we pick an arbitrary world $w$ in an arbitrary model $\mathcal{M}$. The condition for $\mathcal{M}, w \models \Box\varphi$ is that $\varphi$ must be true in all worlds accessible from $w$. Since our premise is that $\varphi$ is true in *all* worlds whatsoever, it is certainly true in the specific subset of worlds accessible from $w$. Thus, $\mathcal{M}, w \models \Box\varphi$. As $w$ and $\mathcal{M}$ were arbitrary, we conclude $\models \Box\varphi$. This argument holds regardless of any special properties of the [accessibility relation](@entry_id:149013), which is why Necessitation is a rule in the minimal logic K [@problem_id:3047643].

It is absolutely critical to understand that Necessitation applies only to **theorems**—formulas proven from the axioms alone. It is not a sound rule for reasoning from contingent premises. For example, from the premise $p$, we can trivially derive $p$. If we were allowed to apply Necessitation to this derivation, we could infer that from the premise $p$, one can derive $\Box p$. By the [deduction theorem](@entry_id:635762), this would imply that $p \to \Box p$ is a theorem. However, $p \to \Box p$ is not a valid formula; we can easily construct a counterexample. Consider a model with two worlds, $w_1$ and $w_2$, where $w_1$ can see $w_2$ ($w_1Rw_2$), $p$ is true at $w_1$, and $p$ is false at $w_2$. At $w_1$, the premise $p$ is true, but $\Box p$ is false because there is an accessible world ($w_2$) where $p$ is false. Thus, $p \to \Box p$ is false at $w_1$ [@problem_id:3047643]. This error highlights the difference between a valid formula and a rule of inference that preserves validity.

This distinction is also central to the two notions of **[semantic consequence](@entry_id:637166)**.
-   **Local Consequence:** $\Gamma \models_{\text{local}} \varphi$ holds if for any world $w$ in any model $\mathcal{M}$, if all formulas in $\Gamma$ are true at $w$, then $\varphi$ is also true at $w$. This captures truth-preservation at a point.
-   **Global Consequence:** $\Gamma \models_{\text{global}} \varphi$ holds if for any model $\mathcal{M}$, if all formulas in $\Gamma$ are true throughout $\mathcal{M}$, then $\varphi$ is also true throughout $\mathcal{M}$. This captures truth-preservation across a whole model.

Local consequence implies global consequence, but the reverse is not true. The example $\{p\} \models_{\text{global}} \Box p$ illustrates this perfectly [@problem_id:3047623]. If we assume $p$ is true at *every* world in a model ($M \models p$), then for any world $w$, all its accessible worlds are also worlds in the model, so $p$ is true in all of them. This makes $\Box p$ true at $w$. Since $w$ was arbitrary, $M \models \Box p$. Thus, global consequence holds. However, as we saw previously, local consequence fails: $\{p\} \not\models_{\text{local}} \Box p$. The assumption of truth at a single world is not strong enough to force the truth of $\Box p$.

### Correspondence, Canonicity, and Completeness

One of the most profound aspects of [modal logic](@entry_id:149086) is **[correspondence theory](@entry_id:634661)**, which connects modal axioms to properties of the [accessibility relation](@entry_id:149013) $R$ in Kripke frames. The logic K is sound and complete with respect to the class of *all* frames. By adding axioms to K, we restrict the class of frames for which the resulting logic is sound and complete.

Some of the most famous correspondences are:
-   **Axiom T:** $\Box\varphi \to \varphi$. A frame validates all instances of Axiom T if and only if its [accessibility relation](@entry_id:149013) is **reflexive** ($\forall w \in W, wRw$). The formula is not valid on all frames, as shown by any non-reflexive [counterexample](@entry_id:148660) [@problem_id:3047621]. The inability to derive $q$ from the premises $\{\Box(p \to q), p\}$ in the logic K, despite this being a valid local consequence on reflexive frames, underscores the syntactic power of the T axiom [@problem_id:3047619].
-   **Axiom 4:** $\Box\varphi \to \Box\Box\varphi$. This axiom corresponds to the property of **[transitivity](@entry_id:141148)** ($\forall x,y,z \in W, (xRy \wedge yRz) \to xRz$). Its dual form, $\Diamond\Diamond\varphi \to \Diamond\varphi$, also corresponds to [transitivity](@entry_id:141148) [@problem_id:3047603]. This axiom fails on non-transitive frames and is therefore not a theorem of K [@problem_id:3047621].
-   **Axiom 5:** $\Diamond\varphi \to \Box\Diamond\varphi$. This axiom corresponds to the **Euclidean** property ($\forall x,y,z \in W, (xRy \wedge xRz) \to yRz$).
-   **Axiom D:** $\Box\varphi \to \Diamond\varphi$. This axiom corresponds to the **serial** property ($\forall w \in W, \exists v \in W, wRv$).

These correspondences allow us to define a vast family of normal modal logics, such as **T** ($K + T$), **S4** ($K + T + 4$), and **S5** ($K + T + 5$), each capturing a different mode of reasoning by virtue of its corresponding frame class.

The ultimate validation of an axiomatic system is a **[completeness theorem](@entry_id:151598)**, which states that the set of theorems is exactly the set of formulas valid on the corresponding class of frames. The proof of this theorem for K and many of its extensions is a landmark achievement, accomplished via the **[canonical model](@entry_id:148621) construction**.

The idea is to build a single, special Kripke model directly from the syntax of the logic $L$ itself, and then show two things: (1) this model satisfies any consistent set of formulas, and (2) its frame belongs to the class of frames corresponding to $L$.

The construction for a logic $L$ proceeds as follows [@problem_id:3047604]:
1.  **Worlds:** The worlds of the **[canonical model](@entry_id:148621)** $\mathcal{M}^c_L$ are all the **maximal $L$-consistent sets** of formulas (MCSs). An MCS is a set of formulas $\Gamma$ that is $L$-consistent (cannot derive a contradiction from it) and complete (for any formula $\varphi$, either $\varphi \in \Gamma$ or $\neg\varphi \in \Gamma$). Lindenbaum's Lemma guarantees that any consistent set can be extended to an MCS.
2.  **Accessibility Relation:** The **canonical [accessibility relation](@entry_id:149013)** $R^c$ is defined as follows: for any two worlds (MCSs) $w$ and $v$, we set $w R^c v$ if and only if for every formula $\varphi$, if $\Box\varphi \in w$, then $\varphi \in v$. An equivalent formulation is $\{\psi \mid \Box\psi \in w\} \subseteq v$. Intuitively, $v$ is a "possible future" of $w$ if it realizes everything that is necessary at $w$.
3.  **Valuation:** The **canonical valuation** $V^c$ is defined by the principle of truth-as-membership: for any propositional variable $p$, $p$ is true at world $w$ if and only if $p \in w$.

The cornerstone of the completeness proof is the **Truth Lemma**, which demonstrates that this construction works perfectly. It states that for any formula $\varphi$ and any world $w$ in the [canonical model](@entry_id:148621), truth in the model coincides with membership in the set:
$\mathcal{M}^c_L, w \models \varphi \iff \varphi \in w$

The proof proceeds by induction on the structure of $\varphi$. The [base case](@entry_id:146682) (for propositional variables) holds by definition of $V^c$. The Boolean cases follow from properties of MCSs. The crucial step is for the $\Box$ operator, and the canonical [accessibility relation](@entry_id:149013) is defined precisely to make this step work.

With the Truth Lemma, completeness for K follows readily. If a formula $\varphi$ is not a theorem of K, then $\{\neg\varphi\}$ is a K-consistent set. It can be extended to an MCS, $w$. By the Truth Lemma, $\mathcal{M}^c_K, w \models \neg\varphi$. This means $\varphi$ is not valid in the [canonical model](@entry_id:148621) for K, and thus $\varphi$ is not valid on all Kripke frames.

For stronger logics, one final step is needed: to show that the canonical frame $\mathcal{F}^c_L = (W^c_L, R^c_L)$ has the desired property. For example, one can prove that if Axiom T is in $L$, then $R^c_L$ is reflexive. This property of an axiom ensuring its corresponding frame property holds in the canonical frame is called **canonicity**. A wide and important class of modal formulas, known as **Sahlqvist formulas** (which includes T, 4, 5, D, and many others), are known to be canonical. The canonicity of Sahlqvist formulas guarantees that the [canonical model](@entry_id:148621) method can be used to prove completeness for any logic axiomatized by them, providing a powerful and general tool for exploring the landscape of [modal logic](@entry_id:149086) [@problem_id:3047642].