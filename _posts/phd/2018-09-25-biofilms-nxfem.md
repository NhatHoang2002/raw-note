---
title: Biofilms model with NXFEM
categories: [maths,phd]
tags: [phd,numerical analysis,biofilm]
maths: 1
date: 2018-09-27
---

This note is for chapter 6 in my thesis. I will use NXFEM coupling with LSM to simulate a biofilm model. 

## Models

### Very simple biofilm model

- In **chopp 2007 xfem biofilm growth.pdf**.
- The same (more specific): **xfem moving interface THESIS - Bryan G. Smith.pdf**
- Is mentioned in **chopp duddu et al 2006 combine nxfem levelset.pdf**, page 18 (figure biofilm, layer growth a little bit - Fig 5). Fig in this article is consistent with result in chopp 2007 xfem.
- $u$: substrate
- $v$: biomass

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">

$$
\begin{align}
-\nabla\cdot(\alpha \nabla u) &= -\mu u \quad (\Omega) \\
[u] = [\alpha \nabla_n u] &= 0 \quad (\Gamma) \\
\nabla_n u &= 0 \quad (\partial\Omega \backslash \partial\Omega_1) \\
u &= 10^{-5} \quad (\partial\Omega_3)
\end{align}
$$ 

</div>
<div class="col s12 l6" markdown="1">

$$
\begin{align}
-\nabla\cdot(\nabla v) &= \beta u \quad (\Omega) \\
v = \nabla_n v &= 0 \quad (\Gamma) \\
\nabla_n v &= 0 \quad (\partial\Omega \backslash \partial\Omega_1) \\
v &= 0 \quad (\partial\Omega_3)
\end{align}
$$ 

</div>
</div>

**Coefficients**:

$$
\alpha=\begin{cases} 120 \, (\Omega_1) \\ 150 \, (\Omega_2) \end{cases}, \quad
\mu=\begin{cases} 3.6\times 10^{-6} \, (\Omega_1) \\ 0 \, (\Omega_2) \end{cases}
$$

### 3 test cases

In **chopp duddu et al 2006 combine nxfem levelset.pdf**, Chopp listed 4 test cases for biofilms. He also describes the properties of the domain, the condition's values and so on. **Page 16 - 18**.

- $100\times 100$ triangles mesh size.
- $\Omega = 0.5\times 0.5$ mm
- $dt = \frac{dx}{\max{F}}$
- $S = 8.3\times 10^{-6}\, \frac{mgO_2}{mm^3}$
- $\nabla_n S=0, \nabla_n \Phi = 0$ on sides of $\Omega$

1. First example, only 1 semi-circle whose radius is $0.01$ mm, grow in $44$ days. **Fig 5** and [49] (**chopp 2007 xfem biofilm growth.pdf**).
2. Second, 3 semi-circles, the middle has radius $0.02$ mm whereas others has $0.01$ mm for each. <mark>How to implement???</mark>. **Fig 6**
3. Third, see in the article.

**Chopp06combine** --[49]-> **Chopp07xfem** --[4]-> **Chopp06simulating** (splitting) and --[6]- **kalpperFinger** and --[5]- **dependQuorum** (parameters)
