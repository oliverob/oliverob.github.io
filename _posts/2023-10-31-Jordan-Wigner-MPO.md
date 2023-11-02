---
title: "Creating the Jordan-Wigner MPO using Category Theory"
layout: post
---
**Disclaimer:** I wrote this blog post as a way of teaching myself how [Laurens Lootens, et al.] derive the Jordan-Wigner MPO using category theory. As such this blog is largely a reproduction of their work with some small changes in notation and a slight elaboration on the use of the module functor. I am by no means rigorous in what follows and if the reader would like a more detailed account of these topics I recommend [Lootens, 2021] and [Lootens, 2023].


We wish to find a magic tensor object (a so called "MPO Intertwiner") that can apply the Jordan-Wigner transformation locally. 

At first glance this problem seems intractable as under the Jordan-Wigner transformation we take local spin operators and convert them to highly non-local fermionic operators (and vise versa):
<div>
\begin{equation}
X_i \rightarrow (-1)^{\sum_{j< i} c^{\dagger}_{j}c_{j}} c^{\dagger}_i, Y_i \rightarrow (-1)^{\sum_{j< i} c^{\dagger}_{j}c_{j}} c_i, Z_i \rightarrow  2c^{\dagger}_{i}c_{i} -I
\end{equation}
</div>
To achieve this ambitous goal we must first step back and find a more generalised way of expressing operators that describe the same physics. 

In particular, we want to find a way of constructing multiple operator bases \\( \\{ O_x \\} \\) that satisfy the same operator product expansion (i.e. have the same \\(f\\) in the following expression):
<div>
\begin{equation}
O_x O_y = f^z_{x,y} O_z
\end{equation}
</div>

To construct these operator bases we turn to category theory. Quite a lot of category theory background is required which I will attempt to summarise below:

### Category Theory
#### Fusion Category
First let us define a fusion category. We can think of fusion categories as a more general form of a group and is defined by the following five things:
1. Isomorphism classes called simple objects \\( \alpha, \beta, \gamma, \ldots \\)
    - It is important to note that these classes are isomorphic to themselves but not to each other (or they would reduce into each other). Therefore, \\( Hom(\alpha, \beta) = \varnothing\\) and \\( Hom(\alpha, \alpha) = End(\alpha)\\)
2. A tensor product rule \\( \otimes \\) to define new objects e.g. \\( \alpha \otimes \beta \\)
3. A monoidal associator \\( F: \alpha \otimes (\beta \otimes \gamma) \rightarrow (\alpha \otimes \beta) \otimes \gamma \\)
4. The trival charge \\( \mathbb{I} \\)
5. A set of fusion rules which are isomorphisms between tensor products of simple objects and direct sums of simple objects \\( \alpha \otimes \beta  \cong \oplus_\gamma N_{\alpha \beta}^{\gamma} \gamma \\)

We can represent the fusion rules using tensor network diagrams, and in particular if we pick a basis \\( \\{ i \\} \\) of \\( N_{\alpha \beta}^{\gamma}\\) then we can further decompose this into a sum over tensor network diagrams as shown below:

{:refdef: style="text-align: center;"}
![fusion rule tensor network](/assets/fig1.jpg){: height="250" }
{: refdef}

Therefore, we can write the monoidal associator \\( F \\) using the tensor network representation of fusion rules:

{:refdef: style="text-align: center;"}
![monoidal associator tensor network map](/assets/fig2.jpg){: height="250" }
{: refdef}

As we can only have homomorphisms between the same isomorphism classes we can rewrite this map as:

{:refdef: style="text-align: center;"}
![monoidal associator tensor network equation](/assets/fig3.jpg){: height="250" }
{: refdef}

We can also use this description to understand the "pentagon" consitency equation these associators must obey:
<div>
\begin{equation}
FF \cong FFF
\end{equation}
</div>
{:refdef: style="text-align: center;"}
![monoidal associator tensor network pentagon](/assets/fig9.png){: height="250" }
{: refdef}

#### Module Category
Now let us define a module category \\( \mathcal{M}\\) over \\( \mathcal{D}\\) by the following three properties:
1. Isomorphism classes of simple objects \\( A, B, C, \ldots \\)
2. An action \\(- \triangleleft  -: \mathcal{M} \times \mathcal{D} \rightarrow \mathcal{M} \\), e.g. \\( A \triangleleft \alpha \cong B \\)
3. A module associator \\( ^\triangleleft F: A \triangleleft (\alpha \otimes \beta) \rightarrow (A \triangleleft \alpha) \triangleleft \beta \\)

Similarly to before we can represent the action using a tensor network diagram:

{:refdef: style="text-align: center;"}
![action tensor network](/assets/fig4.jpg){: height="250" }
{: refdef}

and then we can use this along with the fusion rule representation to draw a tensor network representation of the module associator:

{:refdef: style="text-align: center;"}
![module associator tensor network equation](/assets/fig6.jpg){: height="250" }
{: refdef}

As the dual to these vectors is found by simply flipping them upside down, we can multiply the LHS by the dual of the right and find an expression for \\( ^\triangleleft F \\) in terms of the tensor network representation we have defined.

{:refdef: style="text-align: center;"}
![module associator tensor network contraction](/assets/fig7.jpg){: height="250" }
{: refdef}

**Crucial point:** This new object \\( ^\triangleleft F \\) must obey a "pentagon" consistency condition equation similar to that described for the fusion category and this condition is written as below and only involves the monodial associator \\( F\\) so holds for any choice of module \\( \mathcal{M}\\):

{:refdef: style="text-align: center;"}
![module associator tensor network pentagon](/assets/fig10.png){: height="250" }
{: refdef}

As this equation fully defines how we combine these objects, if we construct an algrebra out of these \\( ^\triangleleft F \\) then it will obey the same operator product expansion for any choice of \\( \mathcal{D}\\)-module category \\( \mathcal{M}\\). For ease of reference throughout the rest of this post we will refer to the algebra constrcuted out of these \\( ^\triangleleft F \\) objects over \\( \mathcal{D}\\)-module category \\( \mathcal{M}\\) as the **\\( (\mathcal{D}, \mathcal{M})\\)-bond algebra**.

### Module Functors
In this language dualities like the Jordan-Wigner transformation are local tensors that can convert from a \\( (\mathcal{D}, \mathcal{M})\\)-bond algebra to an \\( (\mathcal{D}, \mathcal{N})\\)-bond algebra. The natural candidate to consider is module functors.

A  \\( \mathcal{D} \\)-module functor is described by the following properties:
1. Two module categories \\( \mathcal{M},\mathcal{N} \\) over \\( \mathcal{D} \\)
2. A functor \\(G: \mathcal{M} \rightarrow \mathcal{N} \\)
3. A module functor associator \\( ^G F: G(A \triangleleft \alpha) \rightarrow G(A) \triangleleft \alpha \\) for all \\( \alpha \in \mathcal{D}, A \in \mathcal{M}\\)

Consider the "pentagon" equation, here we label \\( ^\triangleleft _\mathcal{D}F \\) with the module they are taken over:
<div>
\begin{equation}
G(A \triangleleft (\alpha\otimes \beta)) = {^G F}\> G(A) \triangleleft (\alpha \otimes \beta) ={^G F^\triangleleft _\mathcal{M}F} \>(G(A) \triangleleft \alpha)\triangleleft \beta
\end{equation}
\begin{equation}
G(A \triangleleft (\alpha\otimes \beta)) = {^\triangleleft _\mathcal{N}F} \>G((A \triangleleft \alpha)\triangleleft \beta) = {^\triangleleft _\mathcal{N}F^G F} \>G(A \triangleleft \alpha)\triangleleft \beta = {^\triangleleft _\mathcal{N}F^G F ^G F} \>(G(A) \triangleleft \alpha)\triangleleft \beta
\end{equation}
\begin{equation}
{^\triangleleft _\mathcal{N}F^G F ^G F} = {^G F^\triangleleft _\mathcal{M}F}
\end{equation}
</div>
We can represent \\( ^G F\\) in tensor network form similarly to before:

{:refdef: style="text-align: center;"}
![module functor tensor network ](/assets/fig13.jpg){: height="250" }
{: refdef}

where \\(A, B \in \mathcal{M}\\) and \\(C, D \in \mathcal{N}\\). We can write the "pentagon" equation as:

{:refdef: style="text-align: center;"}
![module functor tensor network ](/assets/fig14.jpg )
{: refdef}
where  \\(A, B, C \in \mathcal{M}\\) and \\(A', B', C' \in \mathcal{N}\\).

It is clear from this diagram that we can pull \\( ^G F\\) through \\( ^\\triangleleft_\mathcal{M} F \\) to convert it to \\( ^\\triangleleft_\mathcal{N} F \\), and hence by "pulling \\( ^G F\\) through" a \\( (\mathcal{D}, \mathcal{M})\\)-bond algebra we must convert it to a  \\( (\mathcal{D}, \mathcal{N})\\)-bond algebra. Therefore, the Jordan-Wigner transformation is a \\( \mathcal{D} \\)-module functor associator such that the \\( (\mathcal{D}, \mathcal{M})\\)-bond algebra has a representation in terms of Pauli operators and the \\( (\mathcal{D}, \mathcal{N})\\)-bond algebra has a representation in terms of fermionic operators.

### TLDR

You can use category theory to construct operator bases that obey the same operator product expansions by composing "module associator" tensors together, and further one can find a "module functor associator" tensor that converts from one basis to the other if you "pull it through" the "module associator" tensors. It should be possible to find a "module functor associator" tensor that converts from spin operator bases to fermionic operator bases whilst retaining the same operator product expansion a.k.a the Jordan-Wigner transformation.

## Back to Jordan-Wigner

Now we have established all the nitty-gritty of the category theory required, we can get back to considering how this applies in particular to the Jordan-Wigner transformation. In order to convert our cateogry theory abstract nonsense into a more set theoretic understanding, we need to introduce a Hilbert space for our bond algebras to act on. We make the following choice of Hilbert space as we are interested in operators acting upon local states:
<div>
\begin{equation}
\mathcal{H} = \bigoplus_{\{A\}}\bigoplus_{\{\alpha\}} \bigotimes_i \mathcal{V}_{i+\frac{1}{2}}
\end{equation}
where
\begin{equation}
\mathcal{V}_{i+\frac{1}{2}} = Hom_\mathcal{M}(A_i \triangleleft \alpha_{i+\frac{1}{2}}, A_{i+1}), \alpha_{j+\frac{1}{2}} \in \mathcal{D}, A_j \in \mathcal{M} 
\end{equation}
</div>
This space is of the correct form to be acted upon by the bond algebra as the indicies on the outside of \\( ^\triangleleft F \\) are labels for basis vectors in the space \\( Hom_\mathcal{M}(A \triangleleft \alpha,B), \alpha \in \mathcal{D}, A, B \in \mathcal{M} \\)

First we need to show for \\( \mathcal{D} = sVec\\) and \\( \mathcal{M} = sVec\\) this hilbert space represents the  spin basis hilbert space, whilst for \\( \mathcal{D} = sVec\\) and \\( \mathcal{M} = sVec/\\{\mathbb{1} = \psi\\}\\)  this hilbert space represents the fermionic hilbert space.

\\( sVec\\) is a braided fusion category equipped with:
1. Two simple isomorphism categories \\( \mathbb{1}, \psi \\)
2. Fusion rules \\( \mathbb{1} \otimes \mathbb{1} \cong \psi \otimes \psi \cong \mathbb{1}, \\>\\>\mathbb{1} \otimes \psi \cong \psi \otimes \mathbb{1} \cong \psi\\)
3. A field \\( \mathbb{C}^{1\|1} = \mathbb{C}^{1\|0} \oplus \mathbb{C}^{0\|1} \\) with \\(\mathbb{1} \cong \mathbb{C}^{1\|0}\\) and \\(\psi \cong \mathbb{C}^{0\|1}\\)
4. Braiding rule \\( \alpha \otimes \beta \cong (-1)^{\|\alpha\|\|\beta\|} \beta \otimes \alpha\\) where \\(\|\alpha\| = 0 \\) if \\(\alpha \in  \mathbb{C^{1\|0}}\\) and \\(\|\alpha\| = 1 \\) if \\(\alpha \in  \mathbb{C^{0\|1}}\\)

We need to further specify the module action in the two choices:
- \\( \mathcal{M} = sVec\\) - we have \\(A \triangleleft \alpha \cong A \otimes \alpha\\)
- \\( \mathcal{M} = sVec/\\{\mathbb{1} = \psi\\}\\) - we have  \\(\mathbb{1} \triangleleft \mathbb{1} \cong \mathbb{C}^{1\|0} \times \mathbb{1}\\), \\(\mathbb{1} \triangleleft \psi \cong \mathbb{C}^{0\|1} \times \mathbb{1}\\)

Consider \\(\mathcal{V}_{i+\frac{1}{2}}\\) for \\( \mathcal{D} = sVec\\) and \\( \mathcal{M} = sVec\\). In this instance, we have 
<div>
\begin{equation}
\mathcal{V}_{i+\frac{1}{2}} = \begin{cases}End(A_{i+1}) & \text{if } A_{i}\otimes \alpha_{i+\frac{1}{2}} \cong A_{i+1}\\
\varnothing & \text{if } A_{i}\otimes \alpha_{i+\frac{1}{2}}\ncong A_{i+1}\\
 \end{cases}
\end{equation}
</div>
Therefore, the non-vanishing parts of this hilbert space are completely specified by the choices of modules \\(\\{A_i\\}\\), as \\(A_{i}\otimes \alpha_{i+\frac{1}{2}} \cong A_{i+1}\\) if only satsfied by a unique \\(\alpha_{i+\frac{1}{2}}\\) for a given \\(A_i, A_{i+1}\in sVec\\). Therefore, the Hilbert space is given by:
<div>
\begin{equation}
\mathcal{H} =  \bigotimes_i End(\mathbb{1}) \oplus End(\psi)=  \bigotimes_i \mathbb{C}^{1|0}\oplus \mathbb{C}^{1|0} \cong \bigotimes_i \mathbb{C}\oplus \mathbb{C}  \cong \bigotimes_i \alpha \ket{0} + \beta \ket{1}, \alpha, \beta \in \mathbb{C}
\end{equation}
</div>
Therefore, this hilbert space is equivalent to the hilbert space over the spin basis (or qubit computational basis).

Consider \\(\mathcal{V}_{i+\frac{1}{2}}\\) for \\( \mathcal{D} = sVec\\) and \\( \mathcal{M} = sVec/\\{\mathbb{1} = \psi\\}\\). In this instance, we have 
<div>
\begin{equation}
\mathcal{V}_{i+\frac{1}{2}} = \begin{cases}Hom_{sVec/\{\mathbb{1} = \psi\}}( \mathbb{C}^{1|0} \times \mathbb{1},  \mathbb{1}) & \text{if } \alpha_{i+\frac{1}{2}} \cong \mathbb{1}\\
Hom_{sVec/\{\mathbb{1} = \psi\}}( \mathbb{C}^{0|1} \times \mathbb{1},  \mathbb{1}) & \text{if } \alpha_{i+\frac{1}{2}} \cong \mathbb{\psi}\\
 \end{cases}
\end{equation}
</div>
Therefore,
<div>
\begin{equation}
\mathcal{H} =  \bigotimes_i Hom_{sVec/\{\mathbb{1} = \psi\}}( \mathbb{C}^{1|0} \times \mathbb{1},  \mathbb{1}) \oplus Hom_{sVec/\{\mathbb{1} = \psi\}}( \mathbb{C}^{0|1} \times \mathbb{1},  \mathbb{1})
\end{equation}
\begin{equation}
\mathcal{H} =  \bigotimes_i \mathbb{C}^{1|0}  \oplus \mathbb{C}^{0|1} \cong  \bigotimes_i \alpha \ket{\varnothing} + \beta c^{\dagger}_i \ket{\varnothing}, \alpha, \beta \in \mathbb{C}
\end{equation}
</div>
where \\(c^{\dagger}_i\\) is the fermionic creation operator. Therefore, this hilbert space is equivalent to the fermionic basis.

Therefore, the \\( (sVec, sVec)\\)-bond algebra is made up of qubit operators that act on the computational basis states (e.g. Pauli gates etc.), whereas the \\( (sVec, sVec/\\{\mathbb{1} = \psi\\})\\)-bond algebra is made up of fermionic operators that act on the fermionic basis (e.g. creation/annihilation operators). If we can define a module functor between \\(sVec\\) and \\(sVec/\\{\mathbb{1} = \psi\\}\\) then we can find a module functor associator which we have proved allows us to convert from one bond algebra to the other.

We can choose the forgetful module functor \\(G: A \rightarrow \mathbb{1}\\) for \\(A \in sVec\\). This functor has two basis vectors: \\(Hom(\psi, \mathbb{1}) \cong \mathbb{C}^{0\|1}\\) and \\(Hom(\mathbb{1}, \mathbb{1})\cong \mathbb{C}^{1\|0}\\). Let \\(N_i(A) = (c_i^{\dagger})^{n(A)} \ket{\varnothing}\\) where 
<div>
\begin{equation}
n(A) = \begin{cases}1 & \text{if } A = \psi\\ 0 & \text{if } A = \mathbb{1}\end{cases}
\end{equation}
</div>
As \\(N(\mathbb{1}) \cong \mathbb{C}^{1\|0}\\) and \\(N(\psi) \cong \mathbb{C}^{0\|1}\\), \\(N(A)\\) is the basis for this module functor. Similarly \\(N(\alpha)\\) is the basis for \\(Hom(\mathbb{1} \triangleleft \alpha, \mathbb{1})\\) with \\(\alpha \in sVec\\). More simply \\(\alpha\\) is the basis for \\(Hom(A \triangleleft \alpha, B)\\) with \\(\alpha, A, B \in sVec\\). With this in mind let us consider the module functor associator:

{:refdef: style="text-align: center;"}
![jordan wigner module functor 1 ](/assets/fig16.jpg){: width="450" }
{: refdef}

as we know there is only one unique \\(B\\) that \\(A \triangleleft \alpha\\) maps to we can write:

{:refdef: style="text-align: center;"}
![jordan wigner module functor 2 ](/assets/fig17.jpg){: width="450" }
{: refdef}

As this module functor must satisfy the "pentagon" equation when we "pull it through" the \\( (sVec, sVec/\\{\mathbb{1} = \psi\\})\\)-bond algebra it will transform to the \\( (sVec, sVec)\\)-bond algebra and vise versa. Therefore, this is a local MPO that transforms fermionic operators to and from spin operators. Therefore, our Jordan-Wigner MPO is given by:
{:refdef: style="text-align: center;"}
![jordan wigner MPO](/assets/fig18.jpg){: width="450" }
{: refdef}
<div>
<!-- 
### Extra: Bimodule category
The \\( (\mathcal{D}, \mathcal{M})\\)-bond algebra has an intrinsic symmetry that can be described using bimodule categories.

A \\( (\mathcal{C},\mathcal{D}) \\)-bimodule is a category \\( \mathcal{N}\\) equipped with the following properties:
1. Isomorphism classes of simple objects \\( A, B, C, \ldots \\)
2. A module associator over \\( \mathcal{C}\\): \\( ^\triangleright F: (a \otimes b) \triangleright A   \rightarrow b \triangleright (a \triangleright A )  \\) for \\(a, b \in \mathcal{C}, A \in \mathcal{N} \\)
3. A module associator over \\( \mathcal{D}\\): \\( ^\triangleleft F: A \triangleleft (\alpha \otimes \beta) \rightarrow (A \triangleleft \alpha) \triangleleft \beta \\) for \\(\alpha, \beta \in \mathcal{D}, A \in \mathcal{N} \\)
4. A middle associator: \\( ^{\triangleright\triangleleft}F: a \\triangleright (A \triangleleft \alpha) \rightarrow (a \\triangleright A) \triangleleft \alpha\\) for \\(a\in \mathcal{C}, \alpha \in \mathcal{D}, A \in \mathcal{N} \\)

If we consider the "pentagon" equation of the middle associator for \\( \mathcal{N}=\mathcal{M}\\) then the symmetry of the the \\( (\mathcal{D}, \mathcal{M})\\)-bond algebra becomes clear.
<div>
\begin{equation}
a\triangleright (A \triangleleft (\alpha \otimes \beta) ) = {^\triangleleft F} \>a\triangleright ((A \triangleleft \alpha)\triangleleft  \beta) = {^\triangleleft F ^{\triangleright\triangleleft}F}\>(a\triangleright (A \triangleleft \alpha))\triangleleft  \beta = {^\triangleleft F ^{\triangleright\triangleleft}F^{\triangleright\triangleleft}F}\>((a\triangleright A) \triangleleft \alpha)\triangleleft  \beta 
\end{equation}
\begin{equation}
a\triangleright (A \triangleleft (\alpha \otimes \beta) ) = { ^{\triangleright\triangleleft}F} \> (a\triangleright A) \triangleleft (\alpha \otimes \beta)  = { ^{\triangleright\triangleleft}F^\triangleleft F}\>((a\triangleright A) \triangleleft \alpha)\triangleleft  \beta 
\end{equation}
\begin{equation}
 { ^{\triangleright\triangleleft}F^\triangleleft F}= {^\triangleleft F ^{\triangleright\triangleleft}F^{\triangleright\triangleleft}F}
\end{equation}
</div>
We can express \\(^{\\triangleright\\triangleleft}F^\\triangleleft F \\) in tensor network form similarly to before:

![middle associator tensor network ](/assets/fig11.png)

and hence we can write the "pentagon" equation as:

![middle associator tensor network pentagon](/assets/fig12.png)

Therefore, the \\( (\mathcal{D}, \mathcal{M})\\)-bond algebra admits a "pull-thorough" symmetry with any category \\( \mathcal{C}\\) 
-->
</div>

[Lootens, 2021]: https://www.scipost.org/SciPostPhys.10.3.053/pdf
[Lootens, 2023]:   https://journals.aps.org/prxquantum/abstract/10.1103/PRXQuantum.4.020357
[Laurens Lootens, et al.]: https://journals.aps.org/prxquantum/abstract/10.1103/PRXQuantum.4.020357