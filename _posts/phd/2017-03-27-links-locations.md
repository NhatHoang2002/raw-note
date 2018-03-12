---
title: Links and locations
categories:
  - maths
  - phd
toc: 1
maths: 1
---

## Questions on StackExchange

### My questions

1. [What's the general idea of Nische's method in numerical analysis?](http://goo.gl/L6F0qZ) 11/6/15
2. [Boundary vs Interface.](http://scicomp.stackexchange.com/questions/10820/boundary-vs-interface) 14/2/14
3. [Extended FEM vs $P_k$-bubble element.](http://goo.gl/iOM2vz) 15/2/14
4. [Finite Element Method vs Extended Finite Element Method (FEM vs XFEM).](http://goo.gl/6r9QFj) 12/2/14
5. [Need an example of convection-dominated problem to test on FreeFEM++.](http://goo.gl/VmPAjE) 29/6/13
6. [What is difference between Finite Different Method, Finite Element Method and Finite Volume Method for PDE?](http://goo.gl/5vlV9K) 19/6/13
7. [What is convection-dominated pde problems?](http://goo.gl/gzt0Re) 18/6/13
8. [What is the norm in the interface space $L^2(\Gamma)$?](http://goo.gl/D1VIjY) 3/8/14
9. [How to find the Frechet differential of a functional?](http://goo.gl/gBkHKG) 15/4/14
10. [Find the differential of this function.](http://goo.gl/9d5V3o) 13/4/14
11. [What are differences between 'a priori' and 'posteriori' error estimate in numerical analysis?](http://scicomp.stackexchange.com/questions/23202/what-are-differences-between-a-priori-and-posteriori-error-estimate-in-numer/23209) 24/2/16

### Other questions on Stack exchange

1. [Weak formulation for Laplace equation and Robin condition (blog wordpress)](https://mathproblems123.wordpress.com/2012/10/22/weak-formulation-for-laplace-equation-with-robin-boundary-conditions/)
2. [Poisson equation with Robin BC](http://math.stackexchange.com/questions/1128552/poissons-equation-with-robin-boundary-conditions)
3. [Weak form of Robin BC problem - Shuhao Cao](http://math.stackexchange.com/questions/361423/variational-formulation-of-robin-boundary-value-problem-for-poisson-equation-in)
4. [Galerkin for Neumann BC, Shuhao Cao, có cách biến đổi ngược từ weak về strong.](http://math.stackexchange.com/questions/357170/using-galerkin-method-for-pde-with-neumann-boundary-condition)
5. Câu hỏi về support compact $C^{\infty}_c$ : [here](http://math.stackexchange.com/questions/446884/differences-between-c-c-infty0-t-and-c-c-infty0-t) (cái này có thể gợi ý cho vụ extend zero outside $\Omega$)


## Quick notes

- [https://fr.mathworks.com/help/simulink/ug/types-of-solvers.html](https://fr.mathworks.com/help/simulink/ug/types-of-solvers.html)
- [https://fr.mathworks.com/help/dsp/ref/lusolver.html](https://fr.mathworks.com/help/dsp/ref/lusolver.html)
- Học linear algebra rất hay : [http://linear.ups.edu/html/fcla.html](http://linear.ups.edu/html/fcla.html)

## Souce codes

- [http://people.sc.fsu.edu/~jburkardt](http://people.sc.fsu.edu/~jburkardt) : freefem++, matlab, c++, puthon,...
- xfem 1d, 2d : [http://www.matthewpais.com](http://www.matthewpais.com)
- codes (có matlab, python, xfem) : [http://compmech.lab.asu.edu/codes.php](http://compmech.lab.asu.edu/codes.php)
- from xfem.rwth-aachen : [http://www.xfem.rwth-aachen.de/Background/Download/XFEM_Download.php](http://www.xfem.rwth-aachen.de/Background/Download/XFEM_Download.php)
- Rất nhiều source code ví dụ lập trình FEM trên python của tác giả Hans Petter Langtangen (có thể đọc thêm file fem hans peter NOTE.pdf của ổng để biết thêm) : https://github.com/hplgit/INF5620/tree/master/src/fem
- Rất nhiều bài viết + matlab code cho FEM của GS Shaodeng : [here](http://math2.uncc.edu/~shaodeng/TEACHING/math5172/2010Spring/announcement.html) (ông này là ông viết ra cái note dễ hiểu về quadrature in two dimension)

## Maths

### Books and websites hay

- Nói khá rõ về FEM, có nói về nodes, degree of freedom, extended finite element method,... : file **fem hans peter NOTE.pdf**
- Sách về FEM cơ bản nhất nên đọc quyển của **Claes**
- Trang web của Wenqiang feng (có mấy cái notes về PDE, Numerical, code matlab,...) khá là hay : [http://web.utk.edu/~wfeng1/note.html#sec5](http://web.utk.edu/~wfeng1/note.html#sec5)
- Tài liệu **gentle fem sayas.pdf** nói về FEM với giải thích đơn giản, gần gũi.
- Sách về numerical analysis nói chung: **numerical analysis Richard-Douglas BOOK.pdf**

### Other definitions and notes on Maths

Giải **Singular Poisson** bằng Python : [link](https://fenicsproject.org/documentation/dolfin/2016.1.0/python/demo/documented/singular-poisson/python/documentation.html)

---

Euclidean space have **finite dimension** : [https://en.wikipedia.org/wiki/Euclidean_space](https://en.wikipedia.org/wiki/Euclidean_space)

---

**Orthogonal projection** (ánh xạ trực giao): [https://en.wikipedia.org/wiki/Projection_(linear_algebra)#Orthogonal_projections](https://en.wikipedia.org/wiki/Projection_(linear_algebra)#Orthogonal_projections)

---

A **linear map** from a finite dimensional space is continuous, proof:

- [https://en.wikipedia.org/wiki/Discontinuous_linear_map](https://en.wikipedia.org/wiki/Discontinuous_linear_map) <-- hay, dễ hiểu
- [http://math.stackexchange.com/questions/64680/a-linear-operator-on-a-finite-dimensional-hilbert-space-is-continuous](http://math.stackexchange.com/questions/64680/a-linear-operator-on-a-finite-dimensional-hilbert-space-is-continuous) <-- ngắn gọn nhưng khó hiểu hơn

---

**system of nonlinear pde** links

- [http://eqworld.ipmnet.ru/en/solutions/syspde/spde-toc2.htm](http://eqworld.ipmnet.ru/en/solutions/syspde/spde-toc2.htm)

---

**conservation law**

no diffusion term : [http://physics.stackexchange.com/questions/194733/no-diffusion-term-in-conservation-of-mass-in-navier-stokes-equations](http://physics.stackexchange.com/questions/194733/no-diffusion-term-in-conservation-of-mass-in-navier-stokes-equations)

---

**nondimensionalize**
- [https://www.youtube.com/watch?v=mo32vxFgfXk](https://www.youtube.com/watch?v=mo32vxFgfXk)
- [http://www.math.wisc.edu/~angenent/519.2014s/problems/non-dimensionalization.html](http://www.math.wisc.edu/~angenent/519.2014s/problems/non-dimensionalization.html)
- [https://en.wikipedia.org/wiki/Nondimensionalization](https://en.wikipedia.org/wiki/Nondimensionalization)

---

cái **monod** là do empirical còn cái michealis-menten là do lý thuyết mà có.
- [https://en.wikipedia.org/wiki/Michaelis–Menten_kinetics](https://en.wikipedia.org/wiki/Michaelis–Menten_kinetics)
- [https://en.wikipedia.org/wiki/Monod_equation](https://en.wikipedia.org/wiki/Monod_equation)

---

Cái **Poincare inequality** + equivalent norms problem (article 1) : [http://math.stackexchange.com/questions/535503/poincare-inequality-implies-equivalent-norms]( http://math.stackexchange.com/questions/535503/poincare-inequality-implies-equivalent-norms)

---

Hỏi về **Dirichlet, Neumann, Robin boundary condition for Poisson equaito**n : [http://math.stackexchange.com/questions/361423/variational-formulation-of-robin-boundary-value-problem-for-poisson-equation-in](http://math.stackexchange.com/questions/361423/variational-formulation-of-robin-boundary-value-problem-for-poisson-equation-in) 

(Shuhao Cao)[https://mathproblems123.wordpress.com/2012/10/22/weak-formulation-for-laplace-equation-with-robin-boundary-conditions/](https://mathproblems123.wordpress.com/2012/10/22/weak-formulation-for-laplace-equation-with-robin-boundary-conditions/)

Giải thích **Dirichlet condition và Newman dondition**:
[http://sfepy.org/doc-devel/solving_pdes_by_fem.html](http://sfepy.org/doc-devel/solving_pdes_by_fem.html)

(Shuhao Cao)[http://math.stackexchange.com/questions/357170/using-galerkin-method-for-pde-with-neumann-boundary-condition](http://math.stackexchange.com/questions/357170/using-galerkin-method-for-pde-with-neumann-boundary-condition)

---

Chứng minh Hilbert Space H1xH2 là **Hilbert space** : [https://proofwiki.org/wiki/Hilbert_Space_Direct_Sum_is_Hilbert_Space](https://proofwiki.org/wiki/Hilbert_Space_Direct_Sum_is_Hilbert_Space)

---

**weak and strong form** 

[http://math.stackexchange.com/questions/408615/conceptual-difference-between-strong-and-weak-formulations](http://math.stackexchange.com/questions/408615/conceptual-difference-between-strong-and-weak-formulations)

---

**Schauder** fixed point theorem : 3 phiên bản có thể đọc ở đây [fixed point nonlinear pde.pdf](quiver-file-url/9E44F269CC3B4E873F10CBD24670BE0B.pdf).

Sự khác nhau giữa Brouwer và Schauder fixed point theorem : http://math.stackexchange.com/questions/1390379/clarification-on-the-difference-between-brouwer-fixed-point-theorem-and-schauder

**Brouwer**’s Fixed Point Theorem is false in inﬁnite-dimensional spaces. The reason behind this is that a closed ball is not compact.

Muốn trích dẫn **Brouwer fixed point** : sách Le Dreve Theorem 2.2

---

Thắc mắc rằng **Lax Milgram theorem** và các định lý chứng minh existence và uniqueness khác có phụ thuộc vào điều kiện biên không? Ví dụ nếu $u=0$ thì bình thường rùi, giờ nó có khác không nếu $u=u_D$? --> xem trả lời gợi ý (chưa đầy đủ nhưng có thể hiểu sơ sơ) [stackexchange](http://math.stackexchange.com/questions/401994/existence-theorem-for-laplaces-equation)

---

**preconditioner, preconditioning**

- Có nhắc đến một tí trong thesis của Bryan Smith về biofilm ở cuối trang 36. [bryan smith thesis chopp moving interface problems.pdf](quiver-file-url/D5E8B997D70658888CAA9B5400CA3EC7.pdf)
- Thesis trên nhắc đến bài báo "Improved implementation and robustness study of the X-FEMfor stress analysis around cracks"

---

**Quadrature** : xem bài note của ông Shaodeng, có trong folder background or xem lecture 10, 16 tại [đây](http://math2.uncc.edu/~shaodeng/TEACHING/math5172/2010Spring/announcement.html).

---

**ill conditioned system of Nitsche method**

In classical Nitsche based methods, the condition number of the resulting system depends on the interface position, and at times it leads to ill-conditioned system matrices [11,12]. To overcome this issue, in [12,13] the classical Nitsche type approach for weak boundary conditions has been extended to a fictitious domain type formulation by adding an additional ghost-penalty term acting on the jumps of the gradients over element faces adjacent to cut elements. (phần 4 [ở đây](http://www.lacan.upc.edu/sites/default/files/RSP4_FinalReport.pdf))