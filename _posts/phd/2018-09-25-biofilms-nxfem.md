---
title: Biofilms model with NXFEM
categories: [maths,phd]
tags: [phd,numerical analysis,biofilm]
maths: 1
---

This note is for chapter 6 in my thesis. I will use NXFEM coupling with LSM to simulate a biofilm model. 

## Models

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

