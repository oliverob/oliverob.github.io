---
title: "2D Jordan-Wigner PEPO with boundary conditions"
layout: post
---

I have previously discussed the category theory approach to constructing a 1D Jordan-Wigner MPO. In this post I will attempt to explain the 2D generalisation of this proposed by [Sujeet Shukla, et al.], and extend their defintion by considering potential boundary conditions on a closed manifold.

## Definitions

The PEPO is made up of two different tensors.

{:refdef: style="text-align: center;"}
![F vector](/assets/F_vector.svg){: width="250" }
![B vector](/assets/B_vector.svg){: width="250" }
{: refdef}

<div>
\begin{equation}
F = \sum_{abc} |a) |b) |c) |a+b+c)
\end{equation}
\begin{equation}
B = \sum_{a} \ket{a} (a| (a|
\end{equation}
</div>
We define our PEPO as a hexagonal tiling of these tensors:
{:refdef: style="text-align: center;"}
![PEPO](/assets/PEPO.svg){: width="450" }
{: refdef}
We also define a couple other tensors:

{:refdef: style="text-align: center;"}
![gamma vector](/assets/gamma_vector.svg){: width="200" }
![gamma bar vector](/assets/gamma_bar_vector.svg){: width="200" }
![parity vector](/assets/parity_vector.svg){: width="200" }
{: refdef}

<div>
\begin{equation}
\gamma = \sum_{a} |a) (a+1|,   i\bar\gamma = \sum_{a} (-1)^a |a) (a+1|, P = \sum_a (-1)^a |a)(a|
\end{equation}
</div>

## Symmetries
The tensors we have defined have some symmetries that we need to consider. For example consider:
<div>
\begin{equation}
 \gamma_c i\bar\gamma_b F = \gamma_c\sum_{z}  (-1)^{z+1}|z+1) (z|_b \sum_{abc}|a)|b)|c)|a+b+c)
\end{equation}
\begin{equation}
 \gamma_c i\bar\gamma_b  F = \sum_{x} |x +1) (x|_c \sum_{abc}(-1)^{a+b+1}|a)|b+1)|c)|a+b+c)
\end{equation}
\begin{equation}
 \gamma_c i\bar\gamma_b  F = \sum_{abc}(-1)^{a+b+1}(-1)^{a+b+1}|a)|b+1)|c+1)|a+b+c) = \sum_{abc}|a)|b)|c)|a+b+c)= F
\end{equation}
</div>
In a similar manner we can prove all the following symmetries:
{:refdef: style="text-align: center;"}
![F vector](/assets/F_vector.svg){: height="150" }
=
![symmetry 1](/assets/symmetry_1.svg){: height="150" }
=
![symmetry 3](/assets/symmetry_3.svg){: height="150" }
=
![symmetry 2](/assets/symmetry_2.svg){: height="150" }
=
![symmetry 4](/assets/symmetry_4.svg){: height="150" }
{: refdef}
{:refdef: style="text-align: center;"}
![B vector](/assets/B_vector.svg){:height="75" }
=
![symmetry 5](/assets/symmetry_5.svg){:height="75" }
=
![symmetry 6](/assets/symmetry_6.svg){: height="75" }
=
![symmetry 7](/assets/symmetry_7.svg){: height="75" }
=
![symmetry 8](/assets/symmetry_8.svg){:height="75" }
{: refdef}

We can use these symmetries to evaluate how the PEPO transforms local fermionic operators into Pauli operators.

## Even Fermionic Operator Transformation
We can express the even fermionic algebra in terms of vertex operators \\(P_i\\) and edge operators \\(E_{ij}\\) of the form:
<div>
\begin{equation}
P_i = -i \gamma_i \bar \gamma_i
\end{equation}
\begin{equation}
E_{ij} = -i \gamma_i  \gamma_j
\end{equation}
</div>
in this form we can express the anticommutation relations that must be obeyed by the operators as:
<div>
        \begin{align}
                \{ E_{jk}, V_j\} = 0, \{ E_{ij}, E_{jk} \} &= 0 \> \forall \>i \neq k\\
                [V_i, V_j] =0, [E_{ij}, V_m] = 0, [E_{ij}, E_{mn}] &= 0 \>\forall \>i \neq j \neq m \neq n
\end{align}
</div>
along with the following loop condition for any closed loop of sites \\(\\{ p_i\\}\\):
<div>
\begin{equation}
        i^{n} \prod_{i=1}^{n} E_{p_i p_{i+1}} = 1
        \end{equation}
</div>
These conditions are more easily understood as:
1. Edge operators must anti-commute with any vertices they touch
2. Edge operators must anti-commute with any edges they share vertices with
3.  All vertices must commute with each other
4.  All edges that do not share a common vertex must commute
5.  All edges must commute with vertices they do not touch
6.  Any cycle of edges must leave the state unchanged

We can see how these operators are mapped under the PEPO, using the symmetries from above
{:refdef: style="text-align: center;"}
![operator 6](/assets/operator_10.svg){: height="250" }
=
![operator 6](/assets/operator_8.svg){: height="250" }
=
![operator 6](/assets/operator_11.svg){: height="250" }
{: refdef}
which we can write simply as:
{:refdef: style="text-align: center;"}
![operator 7](/assets/operator_7.svg){: height="250" }
{: refdef}
In a similar manner we can find what \\(iE_{ij}\\) maps to under the PEPO:
{:refdef: style="text-align: center;"}
![operator 6](/assets/operator_6.svg){: height="250" }
![operator 4](/assets/operator_4.svg){: height="250" }
![operator 5](/assets/operator_5.svg){: height="250" }
{: refdef}
It is quick to check that the Pauli strings that the edges and vertices are mapped to all obey the correct anticommutation relations (listed above).

Due to the loop condition there is a non-trivial Pauli loop string on every hexagon of tensors. 
{:refdef: style="text-align: center;"}
![loop stabiliser](/assets/loop_stabiliser.svg){: height="450" }
{: refdef}

In order for the Pauli strings produced by this PEPO to be a faithful representation of the even fermionic algebra, they must commute with all the Pauli loop strings. This can be easily verified. Due to this condition, any state produced using this algebra will lie in the +1 eigenspace of these loop strings. We can think of the loop strings as stabilisers and hence all valid even fermionic states are mapped by this PEPO into the codespace of these stabilisers.

This concludes our discussion of how even fermionic operations transform under this PEPO. We have shown that local even fermionic operators transform to local Pauli operators that obey the same algebraic relations, and hence that this is a valid 2D Jordan-Wigner transformation over the even fermionic algebra.

## Boundary conditions

Let us consider the boundary of a closed manifold. We first need to define a new tensor:
{:refdef: style="text-align: center;"}
![JW MPO](/assets/JW-MPO.svg){: height="250" }
{: refdef}
<div>
\begin{equation}
G = \sum_{abc} |a) |b) |a+b)
\end{equation}
</div>
This tensor is the same one used for the 1D Jordan-Wigner MPO. Before tackling the 2D boundary conditions let us first draw insight from how to construct boundary conditions for the 1D Jordan-Wigner MPO. On a closed manifold the 1D Jordan-Wigner MPO looks like the following:
{:refdef: style="text-align: center;"}
![JW MPO closed](/assets/JW-MPO-closed.svg){: height="150" }
{: refdef}
with boundary conditions defined by \\(a, b, c\\) and \\(d\\). 

In order to understand this MPO we again consider the symmetries of the tensors:
{:refdef: style="text-align: center;"}
![JW MPO](/assets/JW-MPO.svg){: height="75" }
=
![symmetry 9](/assets/symmetry_9.svg){:height="75" }
=
![symmetry 10](/assets/symmetry_10.svg){: height="75" }
=
![symmetry 11](/assets/symmetry_11.svg){: height="75" }
{: refdef}
By arguments similar to the 2D case this produces a Jordan-Wigner mapping of the even fermionic operators. In order to find a mapping on the odd fermionic operators we need to introduce a majorana at one of the boundaries. To do this we first consider naively pushing a single majorana operator through the MPO, and find that we get two distinct possible strings.
{:refdef: style="text-align: center;"}
![JW MPO two strings ](/assets/JW-MPO-2-majorana-strings.svg){: height="250" }
{: refdef}

These strings are related to each other by following non-local Pauli string:
{:refdef: style="text-align: center;"}
![JW MPO stabilser ](/assets/JW-MPO-stabiliser.svg){: height="125" }
{: refdef}
which after applying the symmetries translates to:

{:refdef: style="text-align: center;"}
![JW parity mapping ](/assets/parity_mapping.svg){: height="125" }
{: refdef}

So, our boundary states tell us which fermionic parity sector the bulk is in. Therefore, in an even sector we must have \\(a + c = 0\\) (mod 2), whereas in an odd sector we must have \\(a + c = 1\\). Hence, the JW MPO on a closed manifold is given by:

{:refdef: style="text-align: center;"}
![JW MPO closed boundary conditions](/assets/JW-MPO-closed-boundary-conditions.svg){: height="150" }
{: refdef}
where the \\(\\alpha\\)-parity fermionic sector is mapped to the \\(\\beta\\)-parity sector of the \\(\prod_i X_i\\) operator. This is only faithfully reproduces the correct algebra in the \\(\\beta=0\\) sector. However, if we identify the two ends of the MPO with each other the \\(\\beta=1\\) sector becomes a valid representation of the aperiodic algebra.

Therefore the boundary of the 1D JW mapping on a closed manifold are 2 0D Jordan-Wigner mappings (simply \\(X^\{a\}Z^\{b\} \\leftrightarrow P^\{a\} \\gamma^\{b\}\\)). It is also clear to see that if we closed the manifold into a cycle we would be left with a single 0D Jordan-Wigner mapping which would dictate the (\\(\\alpha, \\beta\\))-sectors being mapped.

Similarly, we can create boundary conditions for the 2D Jordan-Wigner mapping by wrapping it in a 1D mapping with the 0D mapping of fermionic sectors inserted:
{:refdef: style="text-align: center;"}
![PEPO with boundary](/assets/PEPO_with_closed_boundary.svg){: height="650" }
{: refdef}

Again, we can try pushing the parity operator through on every vertex:
{:refdef: style="text-align: center;"}
![PEPO with boundary](/assets/PEPO_with_closed_boundary.svg){: width="340" }=\\((-1)^\{\\alpha\}\\)![pushing P through](/assets/pushing_P_through.svg){: width="340" }=\\((-1)^\{\\beta\}\\)![Ring of Xs](/assets/ring_of_Xs.svg){: width="340" }
{: refdef}

Therefore, this PEPO maps from the \\(\\alpha\\)-parity fermionic sector to the \\(\beta\\)-parity eigenspace of \\(\prod_i X_i\\) on the spin degrees of freedom of the 1D boundary.

Here is a quick example of what a single majorana fermion looks like on the \\(\\alpha=1\\), \\(\\beta=0\\) PEPO:

{:refdef: style="text-align: center;"}
![example majorana](/assets/example_majorana.svg){: height="650"  }
![example majorana](/assets/example_majorana_2.svg){: height="650"  }
{: refdef}

At the boundary we also get a new set of stabilisers:

{:refdef: style="text-align: center;"}
![pentagon stabilser](/assets/pentagon_stabiliser.svg){: height="250"  }
![pentagon stabilser](/assets/quad_stabiliser.svg){: height="250"  }

{: refdef}


[Sujeet Shukla, et al.]: https://journals.aps.org/prb/abstract/10.1103/PhysRevB.101.155105