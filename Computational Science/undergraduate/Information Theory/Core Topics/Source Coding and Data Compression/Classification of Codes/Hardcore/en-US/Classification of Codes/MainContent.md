## Introduction
In the vast landscape of information theory, codes are the fundamental language we use to represent and transmit data efficiently and reliably. A source code acts as a translator, converting symbols from a source, like text or sensor data, into sequences of bits for digital processing. However, the utility of a code depends critically on its structure; a poorly designed code can lead to ambiguity, rendering a received message unintelligible. This article addresses this challenge by providing a systematic classification of codes based on their decodability, a property that determines whether a sequence of encoded symbols can be uniquely recovered.

Across the following chapters, you will gain a comprehensive understanding of this essential topic.
- **Principles and Mechanisms** will introduce the strict hierarchy of codes—from non-singular to uniquely decodable and [prefix codes](@entry_id:267062)—and explore the mathematical conditions, like the Kraft inequality, that govern their construction.
- **Applications and Interdisciplinary Connections** will demonstrate the practical relevance of these classifications in [data compression](@entry_id:137700), systems engineering, and their deep ties to computer science disciplines like [formal language theory](@entry_id:264088).
- **Hands-On Practices** will offer concrete problems to test and solidify your grasp of these theoretical concepts.

We begin by examining the core principles and mechanisms that distinguish one class of code from another, laying the foundation for designing robust and efficient information systems.

## Principles and Mechanisms

In the field of information theory, a primary objective is the efficient and reliable representation of information. A source code acts as a dictionary, translating symbols from a source alphabet, such as the letters of English text or the states of a sensor, into codewords, typically sequences of binary digits. For a code to be practical, it must, at a minimum, allow the original sequence of source symbols to be recovered perfectly from the sequence of codewords. However, not all codes are created equal. They can be classified into a strict hierarchy based on their decodability properties, with each level imposing more stringent conditions that yield significant practical advantages. This chapter explores the principles that define this hierarchy and the mechanisms that govern the decodability of codes.

### A Hierarchy of Codes: From Singular to Instantaneous

Let us consider a source with a finite alphabet of symbols $\mathcal{X} = \{x_1, x_2, \dots, x_M\}$ and a code alphabet $\mathcal{A}$, which for digital systems is typically the binary alphabet $\{0, 1\}$. A **source code** $C$ is a mapping from each source symbol $x_i$ to a non-empty, finite-length codeword $C(x_i)$ composed of symbols from $\mathcal{A}$. The properties of this mapping determine the utility of the code. We can organize codes into a nested hierarchy of classes, each a [proper subset](@entry_id:152276) of the one before it .

#### Non-Singular Codes

The most basic requirement for any sensible code is that distinct source symbols should not be mapped to the identical codeword. A code that satisfies this condition is called a **[non-singular code](@entry_id:260982)**. Formally, a code $C$ is non-singular if for any two distinct source symbols $x_i \neq x_j$, their corresponding codewords are also distinct, $C(x_i) \neq C(x_j)$. The mapping is injective.

If a code fails this test, it is **singular**. For example, consider a code for four source symbols $\{s_1, s_2, s_3, s_4\}$ where $C(s_1) = 01$, $C(s_2) = 10$, $C(s_3) = 01$, and $C(s_4) = 11$. This code is singular because both $s_1$ and $s_3$ map to the codeword `01` . If a receiver sees `01`, it is impossible to know whether the original symbol was $s_1$ or $s_3$. Such ambiguity at the level of individual symbols renders the code fundamentally flawed for communication. Consequently, the class of [non-singular codes](@entry_id:261925) forms the first meaningful subset of all possible codes.

#### Uniquely Decodable (UD) Codes

While non-singularity ensures that individual symbols have unique representations, it does not guarantee that a *sequence* of symbols can be unambiguously recovered. When codewords are concatenated into a single stream, such as `...c_1c_2c_3...`, the boundaries between them can become blurred. A **uniquely decodable (UD) code** is one for which any finite sequence of codewords has only one possible interpretation as a sequence of source symbols.

All [uniquely decodable codes](@entry_id:261974) must, by necessity, be non-singular. If a code were singular, a single codeword would correspond to multiple source symbols, immediately violating the condition of unique decodability. However, the converse is not true: a code can be non-singular but fail to be uniquely decodable.

Consider a code for the alphabet $\{A, B, C\}$ defined as $A \to 0$, $B \to 01$, $C \to 10$. This code is non-singular as all three codewords are distinct. However, let's examine the encoded string `010`. This string can be parsed in two different ways:
1.  As `0` followed by `10`, which decodes to the sequence $AC$.
2.  As `01` followed by `0`, which decodes to the sequence $BA$.

Since the string `010` has multiple valid decodings, the code is not uniquely decodable . This demonstrates that unique decodability is a stricter condition than non-singularity.

#### Instantaneous (Prefix) Codes

The class of [uniquely decodable codes](@entry_id:261974) can be further refined. In many applications, such as real-time streaming, it is highly desirable to decode a symbol as soon as its complete codeword has been received, without having to wait and examine subsequent bits in the stream. Codes that permit this are called **[instantaneous codes](@entry_id:268466)**, or more commonly, **[prefix codes](@entry_id:267062)**.

A code is a **[prefix code](@entry_id:266528)** if no codeword is a prefix of any other codeword. For example, in the code $\{A \to 0, B \to 01\}$, the codeword for $A$ (`0`) is a prefix of the codeword for $B$ (`01`). This is not a [prefix code](@entry_id:266528). When a decoder receives a `0`, it cannot immediately decide if the symbol is $A$ or if it is the start of the symbol $B$.

In contrast, consider the code $\{A \to 0, B \to 10, C \to 110, D \to 111\}$. Checking all pairs, we find no codeword is a prefix of another. This is a valid [prefix code](@entry_id:266528) . If a decoder receives the stream `110010...`, it reads `1`, then `11`, then `110`. At this point, it recognizes the codeword for $C$ and can immediately output it. It then continues decoding from the next bit, which is `0`. The codeword for $A$ is `0`, so it outputs $A$. The process continues with `10`, which is the codeword for $B$. The prefix property guarantees that the end of a valid codeword is never ambiguous. This property is why such codes are called "instantaneous."

This property can be visualized using a code tree (for a $D$-ary code, a tree where each node has up to $D$ children). The path from the root to a node represents a sequence of code symbols. In a [prefix code](@entry_id:266528), the codewords correspond exclusively to the **leaf nodes** of the code tree. No codeword can be an internal node, because an internal node is, by definition, a prefix to other nodes (and thus other codewords) further down the tree .

Every [prefix code](@entry_id:266528) is uniquely decodable. If no codeword is a prefix of another, it is impossible to create an ambiguous concatenated string of the type seen before. However, not all UD codes are [prefix codes](@entry_id:267062). The set of [prefix codes](@entry_id:267062) is a [proper subset](@entry_id:152276) of the set of UD codes.

To summarize the hierarchy :
**Prefix Codes $\subset$ Uniquely Decodable Codes $\subset$ Non-Singular Codes $\subset$ All Codes**

### The Mechanism of Decodability

The classification of a code directly impacts the algorithm required for decoding. While [prefix codes](@entry_id:267062) are simple to decode, non-prefix UD codes require more sophisticated methods.

#### Decoding Prefix Codes
Decoding a stream encoded with a [prefix code](@entry_id:266528) is a straightforward, [memoryless process](@entry_id:267313). The decoder traverses the bitstream, matching the sequence against the dictionary of codewords. As soon as a match is found, the corresponding symbol is emitted, and the process restarts from the very next bit. There is no need to buffer incoming data or look ahead, which is why these codes are ideal for streaming applications .

#### Decoding Non-Prefix Uniquely Decodable Codes
For a UD code that is not a [prefix code](@entry_id:266528), the decoder must be more cautious. Consider the code $C = \{S_1 \to 1, S_2 \to 10, S_3 \to 100\}$. This code is not a [prefix code](@entry_id:266528), since `1` is a prefix of `10` and `100`. Let's decode the received message `100101`.

A naive decoder might see the first `1` and decode $S_1$. The remaining stream would be `00101`. However, no codeword in our set starts with `0`. This indicates the initial decision was wrong. The decoder must effectively "backtrack" and look for a longer match. In this case, it must consume all of `100` before finding a valid codeword, $S_3$. The remaining string is `101`. Now, decoding this remainder, `1` is a possible match ($S_1$), but it would leave `01`, which is not a valid codeword start. The only valid parse is `10` ($S_2$) followed by `1` ($S_1$). Thus, the only possible decoding of `100101` is $S_3 S_2 S_1$. This code is indeed uniquely decodable, but decoding it requires context and a form of look-ahead .

The ambiguity inherent in non-[prefix codes](@entry_id:267062) can be formalized by the **Sardinas-Patterson algorithm**. Conceptually, this algorithm works by identifying sets of "ambiguous suffixes". Let's define a look-ahead suffix set, $L_1$, as the set of non-empty strings $s$ that are left over when one codeword $c$ is a prefix of another codeword $c'$. For the code $C = \{0, 01, 110\}$, the codeword `0` is a prefix of `01`, leaving the suffix `1`. So, $L_1 = \{1\}$ . This `1` represents a state of ambiguity for the decoder: after seeing a `0`, if the next bit is a `1`, it might complete the codeword `01`.

The algorithm proceeds recursively. We generate $L_{k+1}$ by looking for overlaps between suffixes in $L_k$ and the original codewords. In our example with $L_1=\{1\}$, we check if `1` is a prefix of any codeword in $C$, or vice-versa. Indeed, `1` is a prefix of `110`, leaving the new suffix `10`. This forms the next set, $L_2 = \{10\}$. We continue this process. A code is uniquely decodable if and only if the empty string never appears in any of these suffix sets. The maximum length of any suffix generated during this process, the "Maximum Look-ahead Depth," quantifies the amount of buffering a streaming decoder might need to resolve ambiguities. For $C = \{0, 01, 110\}$, the total set of suffixes is $L_{\text{total}} = \{1, 10\}$, giving a maximum look-ahead depth of 2 .

### The Mathematics of Codeword Lengths

A fundamental question in code design is whether a set of desired codeword lengths $\{l_1, l_2, \dots, l_M\}$ can form a code of a certain class. For prefix and [uniquely decodable codes](@entry_id:261974), there is a simple and powerful mathematical test.

#### The Kraft Inequality

For a code using a $D$-ary alphabet (e.g., $D=2$ for binary, $D=3$ for ternary), a set of codeword lengths $\{l_i\}$ can be used to construct a **[prefix code](@entry_id:266528)** if and only if they satisfy the **Kraft inequality**:
$$ \sum_{i=1}^{M} D^{-l_i} \le 1 $$
This inequality provides a necessary and [sufficient condition](@entry_id:276242) .

The intuition behind this inequality can be understood by considering the code tree. A codeword of length $l_i$ corresponds to a specific node at depth $l_i$ in the tree. By claiming this node as a codeword (a leaf), we implicitly make its entire descendant subtree unavailable for other codewords, because any path through this node would create a prefix violation. At a very large depth $L$, this single codeword of length $l_i$ effectively occupies $D^{L-l_i}$ of the total $D^L$ available leaf nodes. The fraction of total "coding space" it consumes is therefore $D^{L-l_i} / D^L = D^{-l_i}$. The Kraft inequality simply states that the sum of the fractional spaces consumed by all codewords cannot exceed the total available space, which is 1 .

If a proposed set of lengths violates the inequality, such that $\sum D^{-l_i} > 1$, it is structurally impossible to assign all codewords in the tree without at least one codeword path becoming a prefix of another. The construction will inevitably fail because all available unique paths will be exhausted before all symbols are assigned a valid, prefix-free codeword .

For example, for a binary source ($D=2$) with four symbols, can we construct a [prefix code](@entry_id:266528) with lengths $\{1, 2, 2, 3\}$? We check the Kraft sum:
$$ \sum_{i=1}^{4} 2^{-l_i} = 2^{-1} + 2^{-2} + 2^{-2} + 2^{-3} = \frac{1}{2} + \frac{1}{4} + \frac{1}{4} + \frac{1}{8} = \frac{9}{8} $$
Since $9/8 > 1$, no such binary [prefix code](@entry_id:266528) exists. However, for lengths $\{1, 3, 4, 4\}$, the sum is $2^{-1} + 2^{-3} + 2^{-4} + 2^{-4} = 1/2 + 1/8 + 1/16 + 1/16 = 12/16 = 3/4 \le 1$. A [prefix code](@entry_id:266528) with these lengths can be constructed .

#### The McMillan Inequality

A remarkable result, known as the **McMillan inequality**, extends this condition. It states that the Kraft inequality, $\sum D^{-l_i} \le 1$, is also a necessary condition for a code to be **uniquely decodable**. This means that any set of codeword lengths that can form a UD code must satisfy the same constraint as a [prefix code](@entry_id:266528) .

The implication of this is profound: for any given set of codeword lengths that corresponds to a UD code, there also exists a [prefix code](@entry_id:266528) with the exact same set of lengths. This means that one gains no advantage in terms of achievable codeword lengths by using the more complex, non-instantaneous class of UD codes. When our goal is to find a code with the shortest possible average length, we can restrict our search to the class of [prefix codes](@entry_id:267062) without any loss of optimality.

### Implications for Optimal Coding

An optimal source code is one that minimizes the [average codeword length](@entry_id:263420), $\bar{L} = \sum_{i=1}^{M} p_i l_i$, for a given source probability distribution $\{p_i\}$. Based on the McMillan inequality, we know we can find this optimal code within the class of [prefix codes](@entry_id:267062).

The Huffman coding algorithm is a famous procedure for constructing an [optimal prefix code](@entry_id:267765). A key property of any Huffman code is that the two least probable source symbols are assigned codewords that are "siblings" in the code tree; that is, they have the same length (which is also the longest length in the code) and differ only in their final bit.

Now consider the code $C = \{0, 01, 11\}$. Its lengths are $\{1, 2, 2\}$. This set of lengths satisfies the Kraft inequality with equality: $2^{-1} + 2^{-2} + 2^{-2} = 1$. This condition is often met by optimal codes. However, is $C$ a valid Huffman code for any three-symbol source?

The answer is no. The two longest codewords are `01` and `11`. Their respective prefixes are `0` and `1`. They are not siblings and could not have been generated by the final step of a Huffman construction. Therefore, despite satisfying the Kraft equality, the code $C = \{0, 01, 11\}$ cannot be a Huffman code for any probability distribution, due to this violation of a fundamental structural property of Huffman codes . This illustrates that while the principles of decodability and the Kraft-McMillan inequality define the space of possible codes, the design of optimal codes involves even finer structural constraints.