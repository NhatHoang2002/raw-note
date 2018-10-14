---
title: Quick definitions + notations
categories: math
maths: 1
tags: [phd, math]
toc: 1
---

## Definitions

**Self adjoint matrix** ([https://en.wikipedia.org/wiki/Hermitian_matrix](https://en.wikipedia.org/wiki/Hermitian_matrix))  is a [complex square matrix](https://en.wikipedia.org/wiki/Complex_square_matrix) that is equal to its own [conjugate transpose](https://en.wikipedia.org/wiki/Conjugate_transpose)—that is, the element in the i-th row and j-th column is equal to the [complex conjugate](https://en.wikipedia.org/wiki/Complex_conjugate) of the element in the j-th row and i-th column, for all indices i and j.

$$
a_{ij} = \overline{a_{ji}} \quad \text{or } A=\overline{A^T}
$$

---

### Find triangle's surface via its vertices coordinates

For triangle $T$ with $(x_i,y_i), i\in\overline{1,3}$ (see the note of Zhilin and `50 lines matlab fem`  in `docs\matlab fem`)
$$
\vert T\vert  = \det \left(\begin{array}{c}x_2-x_1 & x_3-x_1 \\y_2-y_1 & y_3-y_1\end{array}\right) = \det \begin{bmatrix}1 & x_1 & y_1 \\1 & x_2 & y_2 \\ 1 & x_3 & y_3 \end{bmatrix}
$$

## Notations

- $C^1_c(\Omega)$ : the space of continuously differential functions with compact support in $\Omega$. 
- $\text{supp}\,f$ : for a function $f$ (defined on $\Omega$), this denotes the support set, i.e. the set on which $f\ne 0$.

$$
\text{supp} f = \overline{\{x\in \Omega:f(x)\ne 0\}}
$$

- $C(\Omega)$ : continuous functions from $\Omega \to \mathbb{R}$.
- $C(\bar{\Omega})$ : the subset of $C(\Omega)$ consisting of functions that extend continuously to $\partial \Omega$.
- $C_0(\Omega)$ : subset of $C(\bar{\Omega})$ consisting of functions which vanish on $\partial\Omega$
- $G\Subset \Omega$ : if $\overline{G}\subset \Omega$ and $\overline{G}$ is compact (that is, closed and bounded) subset of $\Omega$. Xem trang 7 Adams.
- $f$ is **compact support** in $\Omega$ if $\text{supp}f\Subset \Omega$.
  - I cannot explain all the features, but one nice property of a compactly supported function $f$ defined on an open set $\Omega$ is that there exists a compact set $K$ in $\Omega$ such that $f(x)=0$ if $x\not\in K$. This is useful since for instance when you do integration by parts on $f$, **the boundary terms vanish**. If $g$ is any function, you can get a compactly supported function $fg$ by multiplying it by $f$. This is called the *cut-off* process.
- $f$ is **smooth** or $f\in C^{\infty}$ : a function that has derivatives of all orders everywhere in its domain.
- Sobolev space from Ishihara1982[^Ishihara1982]: Nói rõ về định nghĩa $W^{r,p}(\Omega)$ và norms cũng như không gian $H^1(\Omega),H^1_0(\Omega)$.



