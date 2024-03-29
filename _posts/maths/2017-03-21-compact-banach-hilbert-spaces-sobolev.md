---
layout: post
title: Compact, Banach, Hibert, Sobolev spaces
categories: math
toc: 1
tags: [analysis, math]
maths: 1
---

## Metric space & Vector space & norm space & complete

[[s](http://infohost.nmt.edu/~iavramid/notes/hilbert.pdf)] A **metric space** is a set $X$ and a mapping $d: X\times X \to R$, called a **metric**, which satisfies,

1. $d(x,y)\ge 0$
2. $d(x,y)=0 \Leftrightarrow x=y=0$
3. $d(x,y)=d(y,x)$
4. $d(x,y) \le d(x,z)+d(z,y)$

---

A **complex vector space** is a nonempty set $V$ with 2 operations "$+: V\times V \to V$" and "$\cdot: C\times V\to V$" satisfies

1. $x+y=y+x$
2. $(x+y)+z=x+(y+z)$
3. $\exists 0\in V, \forall x\in V: x+0=x$
4. $\forall x\in V, \exists -x\in V: x+(-x)=0$
5. $\alpha(\beta x) = (\alpha \beta)x$
6. $(\alpha+\beta)x = \alpha x + \beta x$
7. $\alpha (x+y) = \alpha x + \alpha y$
8. $1\cdot x = x$

---

A **norm linear space** is a vector space $V$ over $C$ or $R$ and a mapping $\Vert \cdot \Vert: V\to R$, called a **norm**, that satisfies

1. $\Vert x \Vert \ge 0$
2. $\Vert x\Vert =0 \Leftrightarrow x=0$
3. $\Vert \alpha x\Vert = \vert \alpha\vert \Vert x\Vert$
4. $\Vert x+y\Vert \le \Vert x\Vert \Vert y\Vert$

---

[[wiki](https://en.wikipedia.org/wiki/Cauchy_sequence)] In mathematics, a **Cauchy sequence** is a sequence whose elements become arbitrarily close to each other as the sequence progresses. More precisely, given any small positive distance, all but a finite number of elements of the sequence are less than that given distance from each other.

---

A metric space in which all Cauchy sequences converge is called **complete space** or **Cauchy space** (converge to a point also in this space).

[[wiki](https://en.wikipedia.org/wiki/Complete_metric_space)] Intuitively, a space is complete if there are no "points missing" from it (inside or at the boundary). For instance, the set of rational numbers is not complete, because e.g. $\sqrt{2}$ is "missing" from it, even though one can construct a Cauchy sequence of rational numbers that converges to it.

---

[[s](https://math.stackexchange.com/questions/670159/why-do-we-need-dual-space)] The dual space is always complete (regardless of whether X is complete or not)

---

A complete normed linear space is called the **Banach space**.

---

A complex vector space $V$ is called an **inner product space** (or a **pre-Hilbert space** if there is a mapping $(\cdot,\cdot): V\times V\to C$, called **inner product** satisfies

1. $(x,x)\ge 0$
2. $(x,x)=0 \Leftrightarrow x=0$
3. $(x,y+z)=(x,y)+(x,z)$
4. $(x,\alpha y)=\alpha (x,y)$
5. $(x,y)=(y,x)^{\ast}$

---

A complete inner product space is called a **Hilbert space**.

## Compact

**Compact set** : A set $S$ of real numbers is called compact if every sequence in $S$ has a subsequence that converges to an element again contained in $S$.

**Compact space** : A subset $K$ of a metric space $X$ is said to be compact if every open cover of $K$ contains finite subcovers. *understand the idea* (cf [this link.](http://mathoverflow.net/questions/25977/how-to-understand-the-concept-of-compact-space)) $\Rightarrow$ *prevent "escape" to infinity*

---

**[15/3/18]**: [Bài báo](https://blogs.scientificamerican.com/roots-of-unity/what-does-compactness-really-mean/) tuyệt vời. Nói cơ bản, compact có nghĩa là "small", "chặt" nhưng là small rất đặc biệt của toán học. Ví dụ (0,1) không compact nhưng lại "lớn" hơn cái [0,1]. Cái [0,1] "compact" (nhỏ) hơn nhưng lại có thêm 2 điểm 0 và 1. Vì thế nhỏ ở đây ko có nghĩa là nhỏ thông thường mà là nhỏ theo kiểu có thể phủ bởi số "hữu hạn" những phủ con. Một tập compact (nhỏ) thì ta dễ điều khiển hơn, dễ lèo lái hơn, các tính chất cũng "chặt" hơn và khó sai hơn. Đó là lý do vì sao đa phần các định lý đều cần có sự "compact" của set.

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Đọc thêm
</div>
<div class="collapsible-body" markdown="1">
**Non-compactness** is about being able to "move off to infinity" in some way in a space. On the real line you can do that to the left, or right: but bend the line round to fill all but one point on a circle (which is compact) and you see the difference having the "other point" near which you end up. This example of real line versus circle is too simple, really. Another way you can "go off to infinity" in a space is by having paths branching out infinitely (as in König's lemma, which supplies another kind of intuition).

Compactness is a major topological concept because the various ways you might try to "trap" movement within a space to prevent "escape" to infinity can be summed up in a single idea (for metric spaces, let's say). The definition by open sets is cleaner, but the definition by sequences having to accumulate on themselves (not necessarily to converge, but to have at least one convergent subsequence) is somewhat quicker to say. If you restrict attention to spaces that are manifolds, you can think of continuous paths and whether they have to wind back close to themselves or not.

------

$T:K \to K$ continuous, $K$ compact, non-empty, convex and subset of a $X$ compact. Then $T$ is uniformly continuous. (file `nonlinear-fixed-.../fixed point nonlinear pde - Melanie.pdf`)

------

The space $W^1_p(\Omega)$ is compact embedded in $L^q(\Omega)$ when $q < p $ and $\Omega$ is finite. ([Leoni's book](https://www.amazon.com/Course-Sobolev-Graduate-Studies-Mathematics/dp/0821847686?ie=UTF8&tag=stackoverfl08-20) said that)

------

**Relatively compact** (relative compact) : Let $X$ be a metric space, $A\subset X$ is relatively compact in $X$ if $\overline{A}$ is compact in $X$.

Relatively compact còn gọi là **precompact**.com

H is **relatively compact** iff every sequence in H has a convergent subsequence. (not very sure)

------

In **finite dimension** all continuous operators are compact, while in infinite dimension you can have continuous operators which are not compact (xem thêm phản ví dụ [ở đây](http://math.stackexchange.com/questions/1390379/clarification-on-the-difference-between-brouwer-fixed-point-theorem-and-schauder))

---

[[s](https://math.stackexchange.com/questions/1390379/clarification-on-the-difference-between-brouwer-fixed-point-theorem-and-schauder)] Finite dimension all continuous operators are compact, so Brouwer = Schauder fixed point theorem.
</div>
</li>
</ul>

## Banach

**Banach space** = vector space + normed space + complete space

---

[[source](https://math.stackexchange.com/questions/37508/vector-hilbert-banach-sobolev-spaces)] Every Hilbert space is a Banach space and every Banach space is a normed vector space.

---

**Banach space** : a Banach space is a "**complete**" + "**normed" vector space**. Thus, a Banach space is a vector with a metric that allows the computation of vector length and distance between vectors and is complete in the sense that a Cauchy sequence of vectors always convergences to a well defined limit that is within the space.

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Đọc thêm
</div>
<div class="collapsible-body" markdown="1">
A linear operator between **Banach spaces** is continuous if and only if it is bounded.

------

**Closed subspace** : Let $X$ be a Banach space

1. A vector $f\in X$ is a **limit point** of $S\subset X$ if $\exists g_n\in S: g_n\mapsto f$. Mọi điểm của $S$ đều là limit point của nó (nhưng có những cái limit point của nó nằm ngoài nó.)
2. Nếu $S$ đóng thì mọi limit point của nó đều nằm trong nó. Other words, if $g_n\mapsto f\in X$  thì $f\in S$.

------

Y **closed** in X Banach $\Leftrightarrow$ Y **Banach** in X Banach with norm of X.

------

Finite dimensional space of $\mathbb{C}^n$ is a Banach space.
</div>
</li>
</ul>

## Hilbert

**Hilbert space** = Banach space + norm=inner product = vector space + complete + norm=inner product.

---

**Hilbert space** :  A Hilbert space is a vector space H with an inner product $\langle f,g\rangle$ such that the norm defined by $\Vert f\Vert=\sqrt{\langle f,f\rangle}$ turns $H$ into a **complete metric space**. If the metric defined by the norm is not complete, then $H$ is instead known as an **inner product space**. $\Rightarrow$ *Vẫn còn thắc mắc là tại sao $H$ này là complete space, liên quan đến cái dãy Cauchy?*

**Hilbert space** = vector space + inner product. $\Rightarrow$ chuyển thành complete metric space nếu có 1 cái norm định nghịa bởi $\Vert f\Vert=\sqrt{\langle f,f\rangle}$ . Ký hiệu phải lá cặp $(V,\langle\cdot\rangle)$.

In other words, a **Hilbert** space is a **Banach** space whose norm is determined by an inner product.

---

A **Hilbert space** is always a Banach space, but the converse need not hold.

------

A subspace $M$ of **Hilbert space** $H$ is **dense** in $H$ if and only if $M^{\bot}=\{0\}$.

------

$L^2(\Omega)$ is a **Hilbert space**. Xem chứng minh ở [wolfram](http://mathworld.wolfram.com/L2-Space.html)

***Nói thêm*** : Hilbert space là một reflexive Banach space, nó có vài tính chất như "*Mỗi bounded sequence in a relexive Banach space (Hilbert space) has a weakly convergent subsequence. Mà $H^1_0$ cũng là Hilbert space.* " (xem thê ở mục *weak/weak* convergence*)

---

For $p\ne 2$, the space of $L^p$-functions is a Banach space which is not a Hilbert space.

---

Định nghĩa ngắn gọn, $\Omega \in \mathbb{R}^d$, xem thêm ở `fem_method\advanced FEM - Eric Sonnendrucker - Ahmed Ratnani.pdf`

$$
H^1(\Omega) = \{ u\in L^2(\Omega), \nabla u\in (L^2(\Omega))^d \}\\
H^1_0(\Omega) = \{ u\in H^1(\Omega), u=0 \text{ on }\partial \Omega \}
$$

Norm in $H^1$ = seminorm in $H^1(\Vert \nabla u \Vert\_{L^2(\Omega)})$ + norm in $L^2$.

## Sobolev space

**Sobolev space** $L^p(\Omega)$ : Let $(\Omega,\mathcal{A},\mu)$ be a measure space and $1<p<\infty$. The space $L^p(\Omega)$ consists of equivalence classes of measurable functions $f:\Omega \to \mathbb{R}$ such that $\int_{\Omega}\Vert f\Vert ^pd\mu<\infty$.

---

$L^p(\Omega)$ is **complete**. For $1\le p \le \infty$, $L^p(\Omega)$ is a normed linear space.

---

**Comparisons** : 

- If $\mu(X) \le \infty$  and $q > p$, then $L^q(X) \subset L^p(X)$.
- If $1 \le p < q < r \le \infty$, then (a) $L^p\cap L^r \subset L^q$ and (b) $L^q \subset L^p+L^r$

### Sobolev space $H(\textbf{div},\Omega), H(\textbf{curl},\Omega) $

(cf. `advanced FEM - Eric Sonnendrucker - Ahmed Ratnani`) (page 7), 

$H(\textbf{div},\Omega)$ space,

$$
\int_{\Omega}\nabla \cdot \mathbf{u} v\,dx = -\int_{\Omega}\mathbf{u}\cdot \nabla v\, dx + \int_{\partial\Omega} \mathbf{u}\cdot \mathbf{n} v\, ds.
$$

$H(\textbf{curl},\Omega)$ space,

$$
\int_{\Omega}\mathbf{u} \cdot \nabla \times  \mathbf{v} \,dx 
= -\int_{\Omega}\nabla \times \mathbf{u}\cdot \mathbf{v} \, dx 
+ \int_{\partial\Omega} (\mathbf{u}\times \mathbf{n}) \cdot \mathbf{v} \, ds.
$$

---

(Nguồn không rõ) Given $u=(u_1,u_2,\ldots,u_n)$, 

$$
H(\text{div} ;\Omega):= \{ u\in L^2(\Omega)^n : \text{div}\, u\in L^2(\Omega) \}
$$

with 

$$
\Vert {u}\Vert_{\text{div} ,\Omega}^2 :=\Vert {u}\Vert_{H( \text{div};\Omega )} := \Sigma_{i=1}^n\Vert {u_i}\Vert_{L_2(\Omega)}^2 +\Vert {\text{div}\,u}\Vert_{L_2(\Omega)}^2
$$

The space $H(\text{div};\Omega)$ is a Hilbert space with the inner product 

$$
\left<{x,z}\right>_{H(\text{div};\Omega)} := \left<{x,z}\right>_{L^2(\Omega)^n} + \left<{\text{div} x, \text{div} z}\right>_{L^2(\Omega)}
$$

## Other spaces

**Function space** of functions $f:\Omega \to \mathbb{F}$ also forms a vector space.

---

**Norm in dual space** : $\Vert {u}\Vert\_{V'} := \sup\_{v\in V} \dfrac{\vert u(v)\vert }{\Vert {v}\Vert\_{V} } $.

---

**Complete space** = every Cauchy sequence is convergent to a point in this space.

---

The **dual space** of $H^1_0(\Omega)$, denoted $H^{-1}(\Omega):=H^1_0(\Omega)'$ with norm $$\Vert {f}\Vert_{-1}:=\sup_{v\in H^1_0(\Omega)}\dfrac{f(v)}{\Vert {v}\Vert_{H^1(\Omega)} } $$

---

**Dual space** of $L^p$ is $L^q$ where $\frac{1}{p}+\frac{1}{q}=1$. Note that, $L^2(\Omega)=L^2(\Omega)^*$ 

---

$V^{\ast}$ = **algebraic dual space**, $V'$ = **topological dual space**. With finite dimensional normed vector space or topological vector space (eg. Euclidean n-space), $V^{\ast}$ and $V'$ are coincide.

---

**Density** : 

- Step functions, simple functions, $C_c(\mathbb{R}^n), C(\mathbb{R}^n), C^{\infty}_c(\mathbb{R}^n)$ are dense in $L^p(\mathbb{R}^n)$ (or replace all $\mathbb{R}^n$ by $\Omega$).
- Step functions, simple functions, $C(\mathbb{R}^n), C^{\infty}(\mathbb{R}^n)$ are dense in $L^{\infty}(\mathbb{R}^n)$
- $L^1(\Omega)\cap L^{\infty}(\Omega)$ is dense in $L^p(\Omega)$ for all $1\le p< \infty$ 

---

Let $\\{u\_m\\}$ be a sequence of functions in $H^1\_0(\Omega)$ ($\Omega$ is bounded) such that $\Vert u\_m\Vert\_{H^1\_0(\Omega)} \le C < \infty$. There exists a subsequence $\{u\_{m'}\}$ convergent in $L^2(\Omega)$. Xem chứng minh trong file `sobolew.pdf` trong thư mục `analysis`, Theorem 6.

---

**Locally integrable** $L^p_{\text{loc}}$.  Xem thêm [wikipedia](https://en.wikipedia.org/wiki/Locally_integrable_function)

Let $\Omega$ be an open set in the Euclidean space $\mathbb{R}^n$ and $f:\Omega \to \mathbb{C}$ be a Lebesgue measurable function. If f on $\Omega$ is such that

$$
{ \int _{K}\vert f\vert \,\mathrm {d} x<+\infty ,}  \int_K \vert  f \vert \, \mathrm{d}x <+\infty,
$$

i.e. its Lebesgue integral is finite on all compact subsets $K$ of $\Omega$, then $f$  is called locally integrable. The set of all such functions is denoted by $L^1_{\text{loc}}(\Omega)$:

$$
L_{1,\mathrm{loc}}(\Omega)=\bigl\{f:\Omega\to\mathbb{C}\text{ measurable}\: \, f\vert_K \in L_1(K)\ \forall\, K \subset \Omega,\, K \text{ compact}\bigr\},
$$

where $f\Vert  _K$ denotes the restriction of $f$  to the set $K$.

**Definition 2**: Let $\Omega$ be an open set in the Euclidean space $\mathbb{R}$. Then a function $f:\Omega \to \mathbb{C}$ such that

$$
\int_\Omega \vert f \varphi \vert\, \mathrm{d}x <+\infty,
$$

for each test function $\varphi\in C_c^{\infty}(\Omega)$ is called locally integrable, and the set of such functions is denoted by L1,loc(Ω). Here $C_c^{\infty}(\Omega)$ denotes the set of all infinitely differentiable functions $\varphi: \Omega \to \mathbb{R}$ with compact support contained in Ω.

**Lemma**: 

$$
\int_K \vert f \vert \, \mathrm{d}x <+\infty \quad \forall\, K \subset \Omega,\, K \text{ compact} \quad \Longleftrightarrow \quad 
\int_\Omega \vert f \varphi\vert \, \mathrm{d}x <+\infty \quad \forall\, \varphi \in C^\infty_{\mathrm{c}}(\Omega).
$$

---

**Vector space**

A bilinear form over an $F$-vector space  $V$ is a mapping $B:V\times V\to F$ that is linear in each of its arguments, when the other argument is held fixed. Nói cách khác: $B(u,v) = \left<{T(u),v}\right> = \left<{u,Q(v)}\right>$, trong đó $T,Q$ là những linear operators.

---

Let $T:X \to Y$ be a linear operator between two normed vector spaces, where $X$ should be finite dimensional. Then every linear map is continuous. [stackexchange](http://math.stackexchange.com/questions/64680/a-linear-operator-on-a-finite-dimensional-hilbert-space-is-continuous)
