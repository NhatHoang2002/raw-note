---
title: Numerical analysis 1
categories: maths
tags: ["numerical analysis","solver","eigenvalue & eigenvector","boundary condition","shape function","quadrature","matrix","preconditioner","condition number","mesh","scheme","level set method","discontinuous","galerkin method","finite element method","conforming","nxfem","nitsche method","interface","newton method","streamline diffusion method","a priori","posteriori"]
maths: 1
date: 2017-06-01
toc: 1
---

**Xem phần 2 [tại đây](/maths/numerical-analysis-2).**

## Linh tinh

The **Picard–Lindelöf theorem**, which shows that ordinary differential equations have solutions, is essentially an application of the Banach fixed point theorem to a special sequence of functions which forms a fixed point iteration, constructing the solution to the equation. Solving an ODE in this way is called **Picard iteration**, Picard's method, or the Picard iterative process. [(wiki)](https://en.wikipedia.org/wiki/Fixed-point_iteration)

Có thể hiểu hơn về cái **Picard** này ở mục 1.6 (mất link). Nó nói rằng thay vì giải $F(u)=u^2+u$ chẳng hạn, ta giải $\hat{F}(u)=\bar{u}u+u$, trong đó $\bar{u}$ là xấp xỉ của $u$. Cũng gần giống như cái ý tưởng $k,k+1$ của mình khi giải tìm nghiệm $u$ trong article 1.

The idea of turning a nonlinear equation into a linear one by using an approximation $\bar{u}$ of $u$ in nonlinear terms is a widely used approach that goes under many names: **ﬁxed-point iteration**, the method of **successive substitutions**, **nonlinear Richardson iteration**, and **Picard iteration**. We will stick to the latter name.


## Physical meaning

**Physical meaning** của curl, divergence, gradient, laplacian... xem [trong Math2IT](http://math2it.comhieu-y-nghia-thuc-te-cua-phuong-trinh.html).


## Convergence measures & stability

[[source]](http://zoro.ee.ncku.edu.tw/na/res/04-simple_enclosure.pdf) For any rootfinding technique, we have 3 convergence measures to construct the stopping condition

- absolute error : $p_n-p < \varepsilon$
- relative error : $\dfrac{\vert p_n-p\vert}{\vert p_n\vert}<\varepsilon$
- test : $\vert f(p_n)\vert<\varepsilon$

Noone is always better than another.

---

Cái ý tưởng delete finite element basis functions which have a **"very small" support** được nêu ra ở trong **Arnold2008**. Cũng trong bài báo này, ông ta cũng show ra $L^2$ stabilities của basis mới này.

---

Ý tưởng chứng minh convergence 16/10/15, có tờ màu xanh

### Inf-Sup stability

(Inf-sup condition hay còn gọi là **Ladyzhenskaya-Babuska-Breezi condition**) : Cái inf-sup stability này có thể tìm thấy trong nhiều tài liệu, điển hình là trong **Ern2004** trang 268. Nếu chứng minh được $\exists c>0$ such that

$$
\inf_{v_h\in V}\sup_{w_h\in V}\dfrac{a_h(v_h,w_h)}{\Vert {v_h}\Vert_{A}\Vert{w_h}\Vert_{A}}\ge c
$$

Có thể xem thêm ở [note của Long Chen](https://drive.google.com/open?id=0B7pwkv5Gv-VHcGJsZklBMHRpcG8), tổng kết ngắn gọn như sau (cái này gọi là Babuska theory I)

$A:U\to V', \quad A':V\to U'$ với $U',V'$ are dual spaces of $U,V$. Problem is "Given $f\in V'$, find $u\in U: Au=f$ hay $a(u,v)=(f,v),\forall v\in V$. Khi ấy có các đều kiện

1. (continuous) $a(u,v)\le C\Vert{u}\Vert_{}\Vert{v}\Vert_{}, \forall u\in U, v\in V$.
2. (existence) $\inf_{v\in V}\sup_{u\in U}\dfrac{a(u,v)}{\Vert{u}\Vert\Vert{v}\Vert}=c_{\alpha}>0$ (*)
3. (uniqueness) $\inf_{u\in U}\sup_{v\in V}\dfrac{a(u,v)}{\Vert{u}\Vert\Vert{v}\Vert}=c_{\beta}>0$

(*) $\Leftrightarrow \forall v\in V, \exists u\in U: a(u,v)\ge C\Vert{v}\Vert^2$. If $U=V: a(u,u)\ge C\Vert{u}\Vert^2$ (coercive), điều này dẫn tới định lý Lax-Milgram. 

---

Có lúc thắc mắc là basic function $\varphi\in V^{\Gamma}_h$ với định nghĩa $V^{\Gamma}_h=\{v\in L^2(\Omega)\ldots\}$ thì nó có coninuous qua interface hay không. Vẫn là **không** vì nó là $L^2(\Omega)$ tức là khả tích chứ ko có nhắc gì khả vi.


### Standard interpolation error estimate

For $v\in H^1_0(K)\cup H^2(K)$, we have

$$
\begin{align*}
	\Vert\nabla(v-I_hv)\Vert_0 &\le Ch\Vert v\Vert_2 \\
	\Vert v-I_hv\Vert_0 &\le Ch^2\Vert v\Vert_2\\
	\Vert v-I_hv\Vert_1 &\le Ch\Vert v\Vert_2\\
	\Vert v-I_hv\Vert_2 &\le C\Vert v\Vert_2
\end{align*}
$$

###  a priori error estimate & posteriori error estimate

**Ý tưởng** (*không biết có dính tới numerical analysis không?*) :  Suppose you are looking at a falling object. You make a model of the motion of the object in your head. You then close your eyes for a second and estimate the current position of the object in your head. This estimate is the a priori one, before the measurement process. If you open your eyes and look (take a measurement) you will most likely update your model of the process. This is the a posteriori state estimate.

**Chính xác** (Xem thêm course của [Adam Demlow](http://www.math.cornell.edu/~demlow/425/)) The main feature of  **a priori estimates** is that they tell us the order of convergence of a given finite element method, that is, they tel us that the finite element error $\Vert {u-u_h}\Vert$ in some norm $\Vert {\cdot}\Vert$ is $O(h^{\alpha})$ where $h$ is the maximum mesh size and $\alpha$ is a positive integer. The constant in the $O(h^{\alpha})$ is  generally unknown and is often not of great interest. The goal of these estimate is to give us a reasonable measure of the efficiency of a given method by telling us how fast the error decreases as we decrease the mesh size.

**[Wikipedia](https://en.wikipedia.org/wiki/A_priori_estimate)** : A priori is Latin for "from before" and refers to the fact that the estimate for the solution is derived before the solution is known to exist. One reason for their importance is that if one can prove an a priori estimate for solutions of a differential equation, then it is often possible to prove that solutions exist using the continuity method or a fixed point theorem.

In contrast, **a posteriori estimates** use the computed solution $u_h$ in order to give us an estimate of the form $\Vert {u-u_h}\Vert \ge \epsilon$, where $\epsilon$ is simply a number. These estimates accomplish 2 main goals. First, they are able to give a better idea of the actual error in a given finite element computation than are a priori estimate. They can be used to perform **adaptive mesh refinement**. In adaptive mesh refinement, a posteriori estimators are used to indicate where the error is particularly high, and more mesh intervals are then placed in those locations. A new finite element solution is computed, and the process is repeated until a satisfactory error tolerance is reached.

► Câu trả lời từ **[Scicomp StackExchange](http://scicomp.stackexchange.com/questions/23202/what-are-differences-between-a-priori-and-posteriori-error-estimate-in-numer)**

Error estimates usually have the form

$$
\Vert u - u_h\Vert \leq C(h),
$$

where $u$ is the exact solution you are interested in, $u_h$ is a computed approximate solution, $h$ is an approximation parameter you can control, and $C(h)$ is some function of $h$ (among other things). In finite element methods, $u$ is the solution of a partial differential equation and $u_h$ would be the finite element solution for a mesh with mesh size $h$, but you have the same structure in inverse problems (with the regularization parameter $\alpha$ in place of $h$) or iterative methods for solving equations or optimization problems (with the iteration index $k$ -- or rather $1/k$ -- in place of $h$).

The point of such an estimate is to help answer the question "*If I want to get within, say, $10^{-3}$ of the exact solution, how small do I have to choose $h$*?"

The **difference between a priori and a posterior estimates** is in the form of the right-hand side $C(h)$:

- In **a priori** estimates, the right-hand side depends on $h$ (usually explicitly) and $u$, but not on $u_h$. For example, a typical a priori estimate for the finite element approximation of Poisson's equation $-\Delta u = f$ would have the form

$$
  \Vert u-u_h\Vert_{L^2} \leq c h^2 \vert u \vert_{H^2},
$$

  with a constant $c$ depending on the geometry of the domain and the mesh. In principle, the right-hand side can be evaluated prior to computing $u_h$ (hence the name), so you'd be able to choose $h$ before solving anything. In practice, neither $c$ nor $\vert u \vert_{H^2}$ is known ($u$ is what you're looking for in the first place), but you can sometimes get order-or-magnitude estimates for $c$ by carefully going through the proofs and for $\vert u \vert$ using the data $f$ (which is known). The main use is as a qualitative estimate -- it tells you that if you want to make the error smaller by a factor of four, you need to halve $h$.

- In **a posteriori** estimates, the right-hand side depends on $h$ and $u_h$, but not on $u$. A simple *residual-based* a posterior estimate for Poisson's equation would be

$$
  \Vert u-u_h\Vert_{L^2} \leq c h \Vert f+\Delta u_h\Vert_{H^{-1}},
$$

  which could in theory be evaluated *after* computing $u_h$. In practice,  the $H^{-1}$ norm is problematic to compute, so you'd further manipulate the right-hand side to get an *element-wise* bound

$$
  \Vert u-u_h\Vert_{L^2} \leq c \left(\sum_{K} h_K^2 \Vert f+\Delta u_h\Vert_{L^2(K)} + \sum_{F} h_K^{3/2} \Vert j(\nabla u_h)\Vert_{L^2(F)}\right),
$$

  where the first sum is over the elements $K$ of the triangulation, $h_K$ is the size of $K$, the second sum is over all element boundaries $F$, and $j(\nabla u_h)$ denotes the jump of the normal derivative of $u_h$ across $F$. This is now fully computable after obtaining $u_h$, except for the constant $c$. So again the use is mainly qualitative -- it tells you which elements give a larger error contribution than others, so instead of reducing $h$ uniformly, you just select some elements with large error contributions and make those smaller by subdividing them. This is the basis of ***adaptive finite element methods***.

## Methods

### The Streamline Diffution method

(SUPG) for the convection dominated problem. Xem thêm **Knabner2002** chapter 9. 

$$
\partial_t u -\nabla\cdot(\varepsilon\nabla u) + c\cdot\nabla u + ru  =f
$$

- Convection dominated problem : global Péclet number $Pe:=\frac{\Vert{c}\Vert_{\infty} \text{diam}(\Omega) }{\Vert{\varepsilon}\Vert_{\infty}} \gg 1$

- Ý tưởng phương pháp là cộng thêm vào weak formulation một lượng 
  $$
  \Sigma_{K\in \mathcal{T}_h}\delta_K\left<{ -\varepsilon\Delta u + c\cdot\nabla u+ ru,\tau(v_h) }\right>_{0,K} = \Sigma_{K\in\mathcal{T}_h }\delta_K\left<{f,\tau(v_h)}\right>_{0,K}
  $$
  trong đó ta thường chọn $\tau(v_h):=c\cdot\nabla v_h$.

Hoặc chúng ta có thể viết lại weak formulation như sau

$$
\sum_{T\in \mathcal{T}_h}(\partial_t u_h -\nabla\cdot(\varepsilon\nabla u_h) + c\cdot\nabla u_h + ru_h, v_h + \delta c\cdot\nabla v_h) = \sum_{T\in \mathcal{T}_h}(f,v_h+'\delta c\cdot \nabla v_h)
$$

Vì ở trên có đại lượng $(c\cdot\nabla u_h, c\cdot\nabla v_h)$, which is the variational form of a dissusion acting only in the direction $c$. This explains the name of this finite element method. (See this explanation at page 202 book of Arnold)


### Newton method

- [Xem thêm thông tin tại đây](http://zoro.ee.ncku.edu.tw/na/res) 
- Heavily dependent on the choice of initial value $p_0$.
- Có thể converge, có thể converge về 1 giá trị khác, có thể không converge tùy vào cách chọn $p_0$.
- Có định đảm bảo Newton's method sẽ converge nhưng với điều kiện là cái $p_0\in [p-\delta,p+\delta]$ với một cái $\delta>0$ nào đó. Sẽ tồn tại $\delta$ này nhưng chúng ta không biết được nó to nhỏ ra sao, làm sao để chọn $p_0$ phù hợp với $\delta$ này.

###  Fully discrete method

**Thomee2006** uses **fully-discrete scheme**. Đây là một disadvantage.

### Immersed interface method (IIM)

(cái ý này lấy trong bài báo **Li2003** page 3) : To solve an interface problem numerically, usually we need to choose a grid first. In general, there are two kinds of grids: (i) a body fitted grid that is usally combined with a finite element (FE) method, see for example, [7,12]; (ii) a Cartesian grid that is usually assocuated with a finite difference (FD) discretization. The immersed interface method is often based on a Cartesian grid and is often associated with a finite difference method. However, it has been also combined with finite element methods [43,45]. $\Rightarrow$ Rốt cuộc cũng chưa biết IIM là cái gì?

Có cái thesis của Li làm nhiều về cái IIM này. [xem ở đây](http://faculty.washington.edu/rjl/students/li/liphd.pdf)

The basic idea of our immersed interface method is to discretize the Navier-Stokes equations on a uniform Cartesian grid and to account for the singular forces by explicitly incorporating the jumps in the solutions and their derivatives into the difference equations.

$\Rightarrow$ Bài báo về IIM và its applications. [tại đây](http://journal.tms.org.tw/index.php/TJM/article/viewFile/1112/940)

---

Trong bài báo so sánh XFEM và IIM của Chopp (`chopp 2006 comparison xfem iim elliptic.pdf`), ông nói

- The Immersed Interface Method is a finite difference method for approximating the solution to (1). The method solves (1) with singular sources and discontinuous coefficients as well as jump conditions given on the interface by using a regular Cartesian grid that does not conform to the interface. For grid points away from the interface, the standard five-point finite difference stencil is used. As a result, the method
  is second order away from the interface. For grid points near the interface, a six-point stencil and correction terms are added to the right hand side in order to maintain global second order accuracy.

### NXFEM & Nitsche & interface

Ý tưởng về một **basis functions mới** (hơi khác tí cái của mình vì trong $\Omega_2$ nó chổng ngược xuống dưới) nằm trong mục 7.9.2 của **ArnoldBook**

---

Một trong những tài liệu khá hay và đầy đủ liệt kê vấn đề liên quan đến **interface và xfem** là note trường hè của **Lehrenfeld2015**

Có một đoạn cô biến đổi theo Nitsche's method nhưng chưa chính xác lắm, có thể dùng tham khảo sau này. **6/5/15**

$$
\begin{align*}
        \int_{\Omega_1}\nabla\Phi\cdot\nabla v - \int_{\Gamma}\nabla\Phi\cdot n v &= -\int_{\Omega_1}\beta Sv + \int_{\partial\Omega_1\backslash\Gamma}gv\\
        \int_{\Omega_1}\nabla\Phi\cdot\nabla v - \int_{\Gamma}\nabla\Phi\cdot n v &= 0 \\
        \int_{\Gamma}\lambda(\Phi v - \frac{1}{\lambda}\Phi\nabla v\cdot n) &=0 \\
        \Rightarrow \int_{\Omega}\nabla\Phi\cdot\nabla v + \lambda\int_{\Gamma}\Phi v - \int_{\Gamma}\nabla\Phi v\cdot n &= \int_{\Omega_1}-\beta S v+\int_{\partial\Omega_1\backslash\Gamma}gv
    \end{align*}
$$

---

Mọi cái có $u=g$ trên *interface*  là phải dùng thêm lượng penalty. Tức là weakly impose Dirichlet conditions lên interface này. Xem thêm **nitscheIdea**.

Nếu theo phương pháp của Hansbo thì $[\phi_i]= \phi_i\vert_{\Omega_1} - \phi_i\vert_{\Omega_2} = \phi_i\vert_{\Omega_1}$ hoặc $\phi_i\vert_{\Omega_2}$. Còn theo các basis functions bình thường thì $[\phi_i] = 0$.


### Lagrangian–Eulerian methods

Hai cái này khác nhau, xem thêm [wikipedia](https://en.wikipedia.org/wiki/Lagrangian_and_Eulerian_specification_of_the_flow_field) để hiểu thêm.

Cái *Larangian* nhìn dòng chảy bằng cách follows an individual fluid parcel khi nó di chuyển through space and time. Tưởng tượng như là ta đang ngồi trên một chiếc thuyền và xem một chiếc lá (tượng trưng cho hạt nước) chảy trên sông. 

$$
u(x(t),t)
$$

Cái *Eulerian* nhìn dòng chảy bằng cách tập trung vào một vị trí cố định trong không gian khi dòng chảy chảy qua trong khoảng thời gian đó. Tưởng tượng như là khi ta đứng trên bờ và quan sát dòng chảy chảy qua một điểm cố định. 

$$
U(x_0,t)
$$

### Conforming/Nonconforming FEM

Trong sách của **Ern2004**, mục 2.2.1. Let $W$ be a Banach space and $V$ be a reflexive banach space. We have a problem $a(u,v)=(f,v)$ with $a\in \mathcal{L}(W\times V;\mathbb{R})$ and $f\in V'$. 

The key idea underlying Galerkin methods is to replace the spaces $W$ and $V$ by finite dimensional spaces $W_h, V_h$. $W_h$ is termed the *solution space* or *trial space* and $V_h$ is termed the *test space*.

**Definition 2.13 (Conformity)** The approzimation setting is said to be conformal if $W_h\subset W$ and $V_h \subset V$; it is said to be non confomral otherwise.

---

Không biết sao chứ cái phương pháp gốc của Hansbo được xem là conforming, điều này được nói đến trong thèse của **El-Otmany2015**.

**Idea**: có thể cái conforming hay forming này xét đến sự liên tục qua các edges vì cái mà El nói đến và áp dụng conforming là có điều kiện trên edges của tam giác. Chỉ là ý kiến cá nhân của mình.

---

Conformal dịch ra là "bảo giác" nhưng conforming dịch ra là "làm cho thích hợp". Có một cái gọi là **Conforming FEM**, có thể tham khảo [câu hỏi trên Stackexchange](https://math.stackexchange.com/questions/1506433/conforming-approximations-in-fem) về cái này. Bên dưới là một số ý rút ra từ câu hỏi này

> For a given partition of $\Omega$, a conforming approximation of $H^1 (\Omega)$ is a space of continuous functions defined by a finite number of parameters (degrees of freedom). This is usually achieved by using a space of piecewise polynomial functions on the elements K of the partition for $\Omega$. The degrees of freedom are then a set of linear forms on the set of polynomials on K.

A popular non-conforming method is the Discontinuous Galerkin method. > **Why???**

A function space $X_0^h$ is conforming iff $X_0^h \subset H_0^1$. If you know that functions in $X_0^h$ are polynomials on the cells of your mesh, you have $X_0^h \subset H_0^1$ iff all your functions are continuous, i.e., you have no jumps between different cells.

---

Vậy chi cái NXFEM là một dạng của nonconforming FEM. Có 1 bài báo nói về cái này, `nonconforming nxfem elliptic (co ghost penalty).pdf`

---

Một tài liệu khác để xem cái này là note của `fem ronald h.w. hoppe NOTE.pdf` (chương 3)

A simplicial triangulation $\mathcal{T}\_h$ of the computational domain $\Omega \subset \mathbb{R}^d$ is called **geometrically conforming**, if there holds: *The intersection of two diﬀerent elements of the triangulation is either empty, or consists of a common face, or a common edge, or a common vertex*. (trang 52 pdf)

**Conformity of Lagrangian ﬁnite element spaces**: Let $\mathcal{T}\_h$ be a geometrically conforming simplicial triangulation of the computational domain $\Omega \subset \mathbb{R}^d$ then there holds (trang 52)

$$
S_k(\Omega,\mathcal{T}_h)=\{ v_h \in C^0(\bar{\Omega}) \vert v_h\vert_K \in P_k(K), K\in \mathcal{T}_h \} \subset H^1(\Omega).
$$

Điều này cũng có nghĩa, conforming FEM là không gian con của $H^1(\Omega)$, nghĩa là chúng liên tục.


### Discontinuous Galerkin method

**Broken Sobolev space** : $H^k(\Omega,\mathcal{T}_h)=\{v\in L^2(\Omega); v\vert_K\in H^k(K), \forall K\in \mathcal{T}_h\}$

---

Cách giảng giải DGM dễ hiểu về cả không gian lẫn weak form có thể đọc ở **Dolejsi2015** (trang 21)

---

Tóm tắt ý tưởng ở trong **Dolejsi2015**, cho phương trình

$$
\begin{align}
    \begin{cases}\label{eqDGM1}
        -\Delta u&=f \quad \Omega\\
        u&=u_D \quad \partial\Omega_D\\
        \nabla_nu&=g_N \quad \partial\Omega_N
    \end{cases}    
\end{align}
$$

The weak formulation is

$$
\begin{align*}\displaystyle
        \Sigma_{K\in \mathcal{T}_h}\int_{K}\nabla u\cdot\nabla v\, dx - \Sigma_{\Gamma \in \mathcal{F}^{ID}_h}\int_{\Gamma}n\cdot \{\nabla u\}[v]\, dS = \int_{\Omega}fv\, dx + \int_{\partial\Omega_N}g_N v \, dS
\end{align*}
$$

Với $\mathcal{F}^{ID}_h$ is collection of all triangle edges (inner and dirichlet boundary edges). However, in order to guarantee the existence of the approximate solution and its convergence to the exact one, some additional terms have to be included in the DG formulation. $\Rightarrow$ Vẫn cần thêm các terms *penalty, symmetric*.

---

The DG của cái phương trình (cf. **Brezzi2004**)

$$
\nabla\cdot(\beta u)+\gamma u=f
$$

$$
\begin{align*}
	\displaystyle\sum_K\int_K (\nabla\cdot(\beta u)+\gamma u)w=\displaystyle\sum_K\int_K fw
\end{align*}
$$

where

$$
\begin{align*}
	\int_K\nabla\cdot(\beta u)w = -\int_K(\beta u)\cdot\nabla w + \int_{e\Gamma^-}guw + \int_{e\notin\Gamma^-}(\beta\cdot n)uw.
\end{align*}
$$

Sum of all triangles, we have

$$
\begin{align*}
	\displaystyle\sum_K\int_K(-u\beta\cdot\nabla v+\gamma uv) + \displaystyle\sum_{e\notin\Gamma^-}\int_e\{\beta u \}\cdot [v] = \int_\Omega fv - \displaystyle\sum_{e\in \Gamma^-}\int_e(\beta\cdot n)gv, \quad \forall v\in V^k_h.
\end{align*}
$$

---

Identity from **Arnold2001** which holds for vectors $\mathbf{\tau}$ and scalars $\varphi$, piecewise smooth on $\mathcal{T}_h$

$$
\begin{align*}
\sum_{T\in \mathcal{T}_h}\int_{\partial T}(\mathbf{\tau}\cdot \mathbf{n})\varphi ds = {\Sigma}_{e\in \mathcal{E}_h}\int_e\{\tau\}\cdot [\varphi]ds + {\Sigma}_{e\in \mathcal{E}^0_h}\int_e [\tau]\{\varphi\}ds.
\end{align*}
$$

trong đó $\mathcal{E}_h,\mathcal{E}_h^0$ tương ứng là set of all triangle edges và interior edges.

---

Ý tưởng discontinuous unfitted mà không lấy một phần của interface mà chỉ lấy một phần của triangle edge để miêu tả interface được nêu trong **Engwer2009** trang 23.


### Level set method

**Question**:  $\mathbf{u}$ trong $\partial_t \varphi + \mathbf{u}\cdot\nabla\varphi=0$ có được định nghĩa trên toàn miền hay không? Có bài báo nào chỉ bó hẹp ở 1 subdomain như vấn đề của mình hay không?

- Thèse của chị Cúc $\Rightarrow$ toàn miền.
- Bài báo của Sethian trang 12 **Sethian2003** , thì $u$ trên từng miền có giá trị khác nhau và được tính theo các phương trình khác nhau.
- Thèse của Trung Hiếu lấy từ phương trình N-S nên $u$ cũng tính trên toàn miền.

---

The level sets of $f(x,y)$ are the sets on which the function is constant. A fundamental fact of calculus: The gradient of $f(x,y)$ is perpendicular to its level sets.

---

Đoạn sau đây miêu tả giới thiệu về level set method được nói trong bài báo của chị Cúc **Bui2011** (xem mục 2.2)

---

Ý tưởng về (signed) distance function được giới thiệu trong bài báo **Osher1988**

---

**Re-initialization** : Các bài báo/sách của Arnold và cộng sự có nói nhiều về cái này!

(cf. **ArnoldBook**) in general during the evolution of the level set function $\varphi$ the property of $\varphi$ being close to a (signed) distance function is lost. For example, an accurate spatial discretization of $\varphi$ becomes hard in regions where $\varphi$ has a very strong variation, and the problem of finding the zero level set of $\varphi$ becomes ill conditioned in regions where $\varphi$ is very flat.

Một trong những phương pháp re-initialization là giải phương trình được giới thiệu trong bài báo **Tornberg2000** (cái gốc là cái **Sussman1994**]). Khi giải phương trình Navier Stokes cũng có thể coi hai bài báo này, một trong hai cái đó người ta dùng finite volume.

$$
\begin{align*}
        \partial_t \varphi &=sgn(\varphi_0)(1-\vert \nabla\varphi\vert)\\
        \varphi(x,0) &=\varphi_0(x).\\
        sgn(\varphi_0) &= \begin{cases}
            -1 \quad (\varphi_0<0)\\
            0 \quad (\varphi_0=0)\\
            1 \quad (\varphi_0>0)\\
        \end{cases}
\end{align*}
$$

$\varphi$ has the same sign and the same zero level set as $\varphi_0$ and $\Vert{\nabla\varphi}\Vert=1$.

Phương pháp khác cũng được giới thiệu là **Fast Marching Method**.

---

**Mass conservation** : For incompressible flow, the total mass is conserved in time, however the numerical discretization of the level set formulation does not preserve this property in general. Even with some reinitialization procedures, it has been found that a cosiderable amount of total mass is lost in time. Tất cả cái này được nhắc đến trong **Hou1996** (trang 7).

---

(Trong thesis của Trung Hieu, trang 11) Khi level set function advance with time, nó không còn là signed-distance function như thời điểm ban đầu nữa ($\Vert{\nabla\varphi}\Vert \ne 1$). Điều này dẫn đến cần phải thay thế level set function bởi một hàm gần đúng khác sao cho cùng zero level set. Do đó, term $u\cdot\nabla \varphi$ chỉ được xét trong một giai đoạn thời gian rất ngắn. Vì thế, chúng ta có thể xét level set equation mà không có boundary condition.

**Giải thích thử** : : Vẽ cái hình $\varphi^n, \varphi^{n+1}$ ra, cái mở rộng từ cái trước sang cái sau phụ thuộc vào $u\cdot\nabla\varphi$. Nếu $\Delta T$ mà lớn quá thì cái $\varphi^{n+1}$ sẽ lớn hơn rất nhiều so với cái $\varphi^n$, đều này dẫn tới cái $\varphi$ vừa tìm được nó sẽ rất khác so với cái signed distance ban đầu. Do đó việc Reinitialization sẽ khó hơn nữa!!!

$\Rightarrow$ Cũng có thể xem trang 192 sách của **ArnoldBook** có nói về vấn đề này

---

Mấy cái về $F\_{ext}$ (extension velocity) nằm trong bài báo của **Sethian1999**. Giải thích tại sao không phải là $F$ mà phải là $F\_{ext}$ trong công thức reinitialization của level set equation. Vì đôi khi ko có khái niệm velocity on interface. Cách buile $F\_{ext}$ cũng nằm trong bài báo này.

- One can choose to directly use the fluid velocity itself to act as $F\_{ext}$.

## Mesh & scheme

$h_T$ = diameter of $T$ = longest side of $T$.

---

**Consistency**: If $u$ solves the main problem, $u$ also solves the $a_h(u_h,v_h)=(f,v_h)$ problem.

---

**Possibility** : Hiểu đại loại là numerical solution vẫn đảm bảo non-negative (cái này có sách gọi là posibility preserving). Xem thêm ở file `background/analysis/possibility ideas.pdf` (cái file này toàn chữ không hà, chủ yếu coi cái ý tưởng ở phần đầu nó giới thiệu khá hay).

---

**Quasi uniform mesh**: (tham khảo [link](https://drive.google.com/open?id=0B7pwkv5Gv-VHTWozclRtNDhHbkU) Definition 8.3.1). Nói ngắn gọn, nếu tồn tại $C$ để $\dfrac{h}{h_i} \le C$ trong đó $h=\dfrac{b-a}{N}, h_i=x_{i+1}-x_i$.

Theo Claes, $h_K \ge h$ = all elements $K$ of $T\_h$ are roughly the same size = **quasi-uniform**.

---

Dãy số có thể lấy là $h$ vì giữa $h$ và $N$ có mối liên quan với nhau. 26/9/15.

---

Cái form của $S$ và $B$ trong discrete problem có thể xem file uniqueness. Cách biến đổi xem file viết tay ngày 17/11/15

---

**Cartesian grid** : lợi ích?

- No cost for grid generating.
- we can take advantage of many software packages or methods developed for Cartesian grids (xem trong )

---

Còn tài liệu khá hay liênq quan giữa numerical cho transport dùng freefem++ là **DeVuyst2013**

### The order bilinear form and stiffness matrix are different

Suppose that we need to find $u_h\in V_h$ such that

$$
\int_{\Omega}\nabla u_h\cdot\nabla v_h = \int_{\Omega}fv_h, \quad \forall v_h\in V_h.
$$

Let $\{\varphi_i\}\_i​$ be a basis for $V_h​$, this is equivalent to 

$$
\int_{\Omega}\nabla u_h\cdot\nabla \varphi_i = \int_{\Omega}f \varphi_i, \quad  \text{for }i=1,2,\ldots,n.
$$

Since $u_h \in V_h$, $u_h=\sum_j u_j \varphi_j$, then 

$$
\begin{align}
\int_{\Omega}f \varphi_i &= \int_{\Omega}\nabla u_h\cdot\nabla \varphi_i \\ 
&= \int_{\Omega}\nabla \left( \sum_j u_j\varphi_j \right) \cdot\nabla \varphi_i \\ 
&= \sum_j u_j \int_{\Omega} \nabla varphi_j\cdot \nabla \varphi_i, \quad i=1,\ldots,n.
\end{align}
$$

If we use $A(u,v) = (b,v)$ with $u_j$ and $b_i$ then $A_{ij}\times u_j=b_i$.

$$
\begin{align}
A_{ij} &= \int_{\Omega}\nabla\varphi_j\cdot\nabla\varphi_i \\
b_i &= \int_{\Omega}f\varphi_i
\end{align}
$$

---

**The order of convergence**

Trong lý thuyết, kết quả có thể là $\Vert u-u\_h\Vert \le Ch^{\alpha} \Vert u \Vert$. 

$$
\begin{align}
\Vert e_1 \Vert &= \Vert u-u_{h_1}\Vert \le Ch_1^{\alpha} \Vert u \Vert \\
\Vert e_2 \Vert &= \Vert u-u_{h_2}\Vert \le Ch_2^{\alpha} \Vert u \Vert
\end{align}
$$

Suy ra

$$
\dfrac{\Vert e_1 \Vert}{\Vert e_2 \Vert} = \left( \dfrac{h_1}{h_2} \right)^{\alpha}\\
\log \dfrac{\Vert e_1 \Vert}{\Vert e_2 \Vert} = \alpha \log \dfrac{h_1}{h_2}
$$

Lưu ý, $u$ không phụ thuộc vào $h$.

## Node, degree of freedom, vertices in numberical analysis

Tham khảo [Tại đây](https://www.doitpoms.ac.uk/tlplib/fem/node.php) hoặc [Why do solid elements have three degrees of freedom in FEM?](https://www.quora.com/Why-do-solid-elements-have-three-degrees-of-freedom-in-FEM)

Each element possesses a set of distinguishing points called nodal points or nodes for short. Nodes serve a dual purpose: definition of element geometry, and home for degrees of freedom.

Xem xong vẫn chưa hiểu thấu được cụ thể hai thằng dofs và nodes có khác nhau gì không hay giống nhau?

---

In general, the number of degrees of freedom associated with a finite
element is equal to the product of the number of nodes and the number of
values of the field variable (and possibly its derivatives) that must be
computed at each node. ([nguồn](http://www.engr.uvic.ca/~mech410/lectures/FEA_Theory.pdf))

---

We now introduce cells as the subdomains Ω(e) previously referred as elements.
The cell boundaries are denoted as **vertices**. The reason for this name is that
cells are recognized by their vertices in 2D and 3D. We also define a set o**f degrees of freedom**, which are the quantities we aim to compute. The most common type of degree of freedom is the value of the unknown function u at some point. (For example, we can introduce nodes as before and say the degrees of freedom are the values of u at the nodes.) The basis functions are constructed so that they equal unity for one particular degree of freedom and zero for the rest. This property ensures that when we evaluate u = Pj cj’j for degree of freedom number i, we get u = ci. Integrals are performed over cells, usually by mapping the cell of interest to a reference cell (Xem thêm ở file `fem hans peter NOTE`)

## Nonlinear + system

Có cái **nonlinear system of equations** dùng **fixed-point method** nhưng một điều kiện cần là các $g_i(x),x\in \mathbb{R}^n$ phải continuous. Xem thểm ở file `brouwer_fixed_point_oliver_tse.pdf` trong thư mục `nonlinear-...` trang 10.

## Relaxation (sự phục hồi)

Xem thêm ở mục 1.9 của [solving nonlinear ode and pde.pdf](quiver-file-url/F4387C8C15899D5C708FED2E0974CF0A.pdf)

## Parallel vs Sequential algorithm

Có thể xem đầy đủ ở đây [parallel - sequential algorithm.pdf](/Users/dinhanhthi/Dropbox/PhD/docs/back_ground/numerical analysis/parallel - sequential algorithm.pdf)

In other words with sequential programming, processes are run one after another in a succession fashion while in parallel computing, you have multiple processes execute at the same time. With sequential programming, computation is modeled after problems with a chronological sequence of events. ([source](https://mivuletech.wordpress.com/2011/01/12/difference-between-sequential-and-parallel-programming/))

### Parallel algorithm

Cái này từ Conjugate Gradient Method, cũng giống ý tưởng của iterative method. Nghĩa là tìm ra các nghiệm xấp xỉ $x_0,x_1,\ldots,x_n,\ldots$ của exact solution $x^*$ của $Ax=b$. Thật ra cái Conjugate Gradient Method là một bộ phẩn của iterative method. Chưa rõ nó có điểm gì riêng.

### Sequential algorithm

Cái này giống như direct method, từ cái ma trận ban đầu $A$, nó biến đổi về LU (ma trận tam giác) sau đó giải. Ý tưởng từ cái Gauss elimination. Biến đổi hệ phương trình bằng các phép biến đổi sơ cấp (đổi dòng, nhân với 1 số khác 0, cộng các dòng) để ra 1 ma trận tương đương.


## Preconditioner, condition number & matrix

### Condition number

Thật ra xem [trên wikipedia](https://en.wikipedia.org/wiki/Condition_number) dễ hiểu hơn. Nó có động cơ + giải thích luôn.

---

Trong sách của Ern **Ern2004** mục 9.1.2 có nói về **ill conditioning and linear system stability.**

Let $U$ be a solution of following system

$$
AU=F
$$

and $U+\delta U$ is the solution to the perturbed system $A(U+\delta U) = F+\delta F$ and assume that $F\ne 0$ then 

$$
\dfrac{\Vert\delta U\Vert}{\Vert U\Vert} \le \kappa(A) \dfrac{\Vert \delta F\Vert}{\Vert F\Vert}
$$

If $U+\delta U$ is the solution to the pertubed system $(A+\delta A)(U+\delta U)=F$ with $F\ne 0$ then 

$$
\dfrac{\Vert\delta U\Vert}{\Vert U+\delta U\Vert} \le \kappa(A) \dfrac{\Vert \delta A\Vert}{\Vert A\Vert}
$$

### Preconditioner

**Preconditioner** : The general idea underlying any preconditioning procedure for iterative solvers is to modify the (ill-conditioned) system $Ax = b$ in such a way that we obtain an equivalent system $\bar{A}\bar{x}=\bar{b}$ for which the iterative method converges faster.

---

**Preconditioner** : The general idea underlying any preconditioning procedure for iterative solvers is to modify the (ill-conditioned) system $Ax = b$ in such a way that we obtain an equivalent system $\bar{A}\bar{x}=\bar{b}$ for which the iterative method converges faster.

Xem thêm về [condtional number của một matrix ở trang Math2IT](http://math2it.com/tinh-hop-ly-cua-nghiem-he-phuong-trinh/).

**ill-conditioned matrix** có nghĩa là khi thay đổi một chút giá trị hệ số trong phương trình $AU=F$ (thay đổi $A$ hay $F$) thì kết quả nghiệm $U$ thay đổi rất nhiều. 
Còn **well-conditioned matrix** có nghĩa là khi thay đổi nhỏ các hệ số thì kết quả nghiệm cũng chỉ thay đổi nhỏ mà thôi.

**Norm of matrix (chuẩn của ma trận)** : $\Vert A \Vert = \max_{x\ne 0}\dfrac{\Vert Ax \Vert}{\Vert x\Vert}$. Chuẩn phổ biến nhất là 
- maximum absolute column sum : $\Vert A \Vert_1 = \max_{1\le j\le m}\sum_{i=1}^n\vert a_{ij}\vert $
- maximum absolute row sum : $\Vert A \Vert_{\infty} = \max_{1\le i\le n}\sum_{j=1}^m\vert a_{ij}\vert $

**condition number** của một ma trận : $\Vert A\Vert \Vert A^{-1}\Vert$. Con số này nhỏ (well-conditioned), lớn thì (ill-conditioned) $\Rightarrow$ how much the output value of the function can change for a small change in the input argument ([wikipedia](https://en.wikipedia.org/wiki/Condition_number))

**numerically stable** : các calculations có biến động nhỏ ở dữ liệu đầu vào dẫn tới biến động nhỏ ở error (nghiệm số và nghiệm chính xác).

- It is obvious from the definition that a nonsingular matrix and its inverse have the same condition number.

---

Cần phải biết về cái **preconditioner**. Xem ở mục khác có ghi cụ thể hơn.

**Preconditioner** : The general idea underlying any preconditioning procedure for iterative solvers is to modify the (ill-conditioned) system $Ax = b$ in such a way that we obtain an equivalent system $\bar{A}\bar{x}=\bar{b}$ for which the iterative method converges faster.

In linear algebra and numerical analysis, a **preconditioner** $P$ of a matrix $A$ is a matrix such that $P^{-1}A$ has a smaller **condition number** than $A$ (smaller condition number implies more **well-conditioned** matrix).

Preconditioners are useful in **iterative methods** to solve a linear system $Ax=b$ for $x$ since the **rate of convergence** for most iterative linear solvers **increases** as the **condition number** of a matrix **decreases** as a result of preconditioning. [Đoạn này và đoạn trên là xem ở Wikipedia](https://en.wikipedia.org/wiki/Preconditioner).

Xem thêm về [condtional number của một matrix ở trang Math2IT](http://math2it.com/tinh-hop-ly-cua-nghiem-he-phuong-trinh-va-khai-niem-condition-number-cua-mot-ma-tran-ky-1).

---

Condition number of a stiffness matrix nói trong sách của Claes (trang 141): If A is the stiffness matrix related to an elliptic problem of order $2m$, then the condition number $k(A)$ s.t. $k(A) \le O(h^{-2m})$ or $k(A) \le ch^{-2m}$

---

Thường người ta test thử với Hilbert matrix để xem thử condition number của nó thế nào. Đây là ma trận ill-conditioned.

$$
H_{{ij}}={\frac  {1}{i+j-1}}.
$$

### Positive definite matrix

Xem định nghĩa **Positive definite matrix** và hiểu rõ nó hơn ở file này - [positive definite.pdf](https://drive.google.com/open?id=0B7pwkv5Gv-VHTFVVcjc3bXJqclU). 

---

PDM khi all eigenvalues của matrix ấy đều positive.

---

The determinant of a positive definite matrix is always positive, so a positive definite matrix is always nonsingular. Xem thêm trên [Wolfram](http://mathworld.wolfram.com/PositiveDefiniteMatrix.html).

---

Trong **Finite Element Method**, matrix $A$ trong $AU=F$ phải là positive definite, cái này được nói đến trong `Numrical solution of PDE by the FEM` của Claes Johnson mục 1.2.

## Quadrature

Xem bài viết khá dễ hiểu tại [đây](http://math2.uncc.edu/~shaodeng/TEACHING/math5172/2010Spring/announcement.html). Lecture 10 và 16, có download rùi, để trong thư mục background.

Quadrature có nghĩa là xấp xỉ 1 integrate bởi một lượng

$$
\int fdx = \sum_i w_if(x_i)
$$

Lưu ý là quadrature take exact values nếu như hàm $f$ là polynomial hoặc các dạng tương tự vậy, xem kỹ hơn trong các files trên.

$$
\int_a^b f(x)dx \simeq \dfrac{b-a}{2}\sum_{i=1}^Nw_if(a+\dfrac{b-a}{2}(1+x_i))
$$

Có thể xem ví dụ code matlab trong folder background\numerical analysis.

Còn quadrature cho tam giác bất kỳ ở bậc bất kỳ thì xem cụ thể trong file, công thức khá phức tạp.

## Shape functions

In FEM the basic concept is to assume an approximate solution that satisfies the governing differential equation and boundary conditions. The whole idea is to get this assumed or approximate solution as close to the exact solution as possible. To do this we assume our approximate solution to be a linear combination of simpler functions. These simpler functions are called shape functions.

For instance we take an approximate solution $U^{\ast}= N\_1u\_1+ N\_2u\_2+\ldots$
here $N\_1, N\_2, N\_3, \ldots$ are shape functions and $u\_1, u\_2,\ldots$ are constants (which are to be evaluated). How we choose the shape functions is governed by the rule that they must be **partitions of unit**y i.e. **the sum of all shape functions at any given point $(x,y,z)$ must be $1$**. ($N\_1 + N\_2+ N\_3+\ldots =1$).  The number and order of shape functions determine the accuracy of solution. Ideally, more the shape functions the more accurate the solution and more the computational power required.

[Ref here (quora)](https://www.quora.com/What-is-a-Shape-Function-in-FEM).

---

Note that the shape functions are non-zero in the element and zero everywhere else.

---

Consider on 1 triangle, for example, there are 3 nodal shape basis functions

$$
\begin{align}
	N_1(x,y) &= 1-x-y \\
	N_2(x,y) &= x \\
	N_2(x,y) &= y
\end{align}
$$

---

**Shape functions** are defined in local coordinate.

---

[[Also]](http://www.iue.tuwien.ac.at/phd/orio/node48.html) The shape function is the function which interpolates the solution between the discrete values obtained at the mesh nodes. Therefore, appropriate functions have to be used and, as already mentioned, low order polynomials are typically chosen as shape functions. In this work linear shape functions are used.

## Boundary conditions

**Henry condition** (xem các references nói về cái này trong thesis của Trung Hieu trang 9 **HieuThesis** : $[\beta u]=0$ on $\Gamma$

**Robin BC**: combine of Dirichlet and Neumann BC

**Dirichlet BC** = essential bc (not really correct for all cases) see more [here](https://www.researchgate.net/post/What_is_the_difference_between_essential_boundary_conditions_and_natural_boundary_conditions)

**Newmann BC** = natural bc (not really correct for all cases) see more on the link above.

## Eigenvalues and eigenvectors & Singular values and singular vectors

### Eigenvalues and eigenvectors

Xem thêm tại [wikipedia](https://en.wikipedia.org/wiki/Eigenvalues_and_eigenvectors).

In linear algebra, an eigenvector or characteristic vector of a linear transformation is a non-zero vector that **does not change its direction** when that linear transformation is applied to it. More formally, if $T$ is a linear transformation from a vector space $V$ over a field $F$ into itself and $v$ is a vector in $V$ that is not the zero vector, then $v$ is an eigenvector of $T$ if $T(v)$ is a scalar multiple of $v$. This condition can be written as the equation

$${\displaystyle T(\mathbf {v} )=\lambda \mathbf {v} ,} $$

where $\lambda$ is a scalar in the field $F$, known as the eigenvalue, characteristic value, or characteristic root associated with the eigenvector $v$.

If the vector space $V$ is **finite-dimensional**, then the linear transformation $T$ can be represented as a square matrix $A$, and the vector $v$ by a column vector, rendering the above mapping as a matrix multiplication on the left hand side and a scaling of the column vector on the right hand side in the equation

$${\displaystyle A\mathbf {v} =\lambda \mathbf {v} .}$$

Xem định nghĩa **Positive definite matrix** và hiểu rõ nó hơn ở file này - [positive definite.pdf](quiver-file-url/2DCBA056260F6B696F38822893637F10.pdf). 

### Singular values and singular vectors

Xem thêm [tại đây](https://www.mathworks.com/moler/eigs.pdf) (docs của mathworks). Cái **eigenvalue decomposition** cũng được giải thích trong này. Nếu link die ,có thể xem [eigenvalue and singular value.pdf](quiver-file-url/408E443E0AA205C68E1E68CC6F6E806C.pdf).

A singular value and pair of singular vectors of a square or rectangular matrix $A$ are a nonnegative scalar σ and two nonzero vectors $u$ and $v$ so that

$$
Av=\sigma u \\
A^Tu=\sigma v
$$

The term “singular value” relates to the distance between a matrix and the set of singular matrices.

**Eigenvalues** play an important role in situations where the matrix is a transformation from one vector space onto itself. Systems of linear ordinary differential equations are the primary examples. The values of $\lambda$ can correspond to frequencies of vibration, or critical values of stability parameters, or energy levels of atoms. 

**Singular values** play an important role where the matrix is a transformation from one vector space to a different vector space, possibly with a different dimension.

---

Given a matrix $A$, if the eigenvalues of $A^TA$ are $\lambda\_i \geq 0$, then $\sqrt{\lambda_i}$ are the singular values of $A$. If $t$ is an eigenvalue of $A$, then $\vert t\vert$ is a singular value of $A$. And here is an example should be noticed, 

$$A = \begin{pmatrix}1&0&1\\0&1&1\\0&0&0\end{pmatrix},$$

the eigenvalues of $A$ are $1,1,0$ while the singular values of $A$ are $\sqrt{3},1,0$.

Cái này là trên [stackexchange](http://math.stackexchange.com/posts/606516/edit).

### matrix and eigenvalue

[http://linear.ups.edu/html/section-PEE.html](http://linear.ups.edu/html/section-PEE.html) (đây cũng là trang học linear algebra rất hay, nhấn link xổ xuống nhiều định nghĩa và chứng minh)

## Linear system solver

### What is a solver?

Xem trên [mathwork](https://fr.mathworks.com/help/simulink/ug/choosing-a-solver.html). When you choose a solver for simulating a model, consider:

- The dynamics of the system
- The stability of the solution
- The speed of computation
- The robustness of the solver

---

Giới thiệu sơ qua các direct solver vs iterative solver này nọ, dễ hiểu có thể xem ở đây : [iterative solvers for linear systems.pdf](quiver-file-url/CAB36902E96FBAFEE40718A8B81D8EB0.pdf)

- **direct solver** : LU decomposition, Gaussian elimination, Cholesky factorization, MUMPS.
- **iterative solver** : GMRES, MINRES,...

Recently combining direct and iterative solvers has become an active area of research eg direct solvers used to obtain preconditioners for iterative solvers.

---

Tài liệu này [NumPro_WS1213_Vorlesung_Kapitel_4.pdf](quiver-file-url/9DF023CA862D9C7579641DA2EBB56555.pdf) cũng rất hay.

---

The default solver in FreeFem++ is **GMRES** (iterative solver).

### LU Solver

LU factorization : 

$$
Ax = LRx = L(Rx) = Ly = b.
$$

First, solve $Ly=b$ then solve $ Rx=y $.

Thuật toán dưới đây có thể xem ở [NumPro_WS1213_Vorlesung_Kapitel_4.pdf](quiver-file-url/9DF023CA862D9C7579641DA2EBB56555.pdf)

~~~ cpp
for i from 1 to n do
   for k from 1 to i-1 do
      l[i,k]:=a[i,k];
      for j from 1 to k-1 do l[i,k]:=l[i,k]-l[i,j]*u[j,k] od;
      l[i,k]:=l[i,k]/u[k,k]
   od;
   for k from i to n do
      u[i,k]:=a[i,k];
      for j from 1 to i-1 do u[i,k]:=u[i,k]-l[i,j]*u[j,k] od
   od
od;
for i from 1 to n do
y[i]:=b[i];
   for j from 1 to i-1 do y[i]:=y[i]-l[i,j]*y[j] od
od;
for i from n downto 1 do
   x[i]:=y[i];
   for j from i+1 to n do x[i]:=x[i]-u[i,j]*x[j] od;
   x[i]:=x[i]/u[i,i]
od;
~~~

### Cholesky Solver

Thuật toán dưới đây có thể xem ở [NumPro_WS1213_Vorlesung_Kapitel_4.pdf](quiver-file-url/9DF023CA862D9C7579641DA2EBB56555.pdf)

~~~ cpp
for k from 1 to n do
  l[k,k]:=a[k,k];
  for j from 1 to k-1 do l[k,k]:=l[k,k]-l[k,j]ˆ2 od;
  l[k,k]:=(l[k,k])ˆ0.5;
  for i from k+1 to n do
     l[i,k]:=a[i,k];
     for j from 1 to k-1 do l[i,k]:=l[i,k]-l[i,j]*l[k,j] od;
     l[i,k]:=l[i,k]/l[k,k]
od od;
~~~

$$
A = LL^T
$$

### UMFPACK Solver

Các matrix có thể nonsymmetric. Là sparse, square matrix. $$PA=LU$$ với $L$ = upper matrix, $U$ = upper matrix.

[(từ scilab)](https://help.scilab.org/docs/6.0.0/pt_BR/umfpack.html) First an LU factorization of the matrix is computed ($P R^{-1} A Q = LU$ where P and Q are permutation matrices, R is a diagonal matrix (row scaling), L a lower triangular matrix with a diagonal of 1, and U an upper triangular matrix) then a first solution is computed with forward/backward substitutions ; finaly the solution is improved by iterative refinement.

$\Rightarrow$ đã có UMFPACK64, muốn sử dụng trong Freefem++ thì phải load trước khi dùng

~~~ cpp
load "UMFPACK64"
//không có dấu ; phía sau
~~~

### CG Solver

### GMRES solver

### sparsesolver

### Crout solver

### factorize

factorize = if true then do the matrix factorization for LU, Cholesky or Crout, the default value is false.(section 6.12)

### MUMPS

- Cái này tốt cho large sparse system, especially those arising from FEM.
- general symmetric/unsymmetric or symmetric positive definite
- Cái này là version of Gaussian elimination (phép khử Gauss)
- Muốn dùng trong Freefem++ thì phải cài thêm.
- **Direct method**

### Gaussian elimination

Thuật toán dưới đây có thể xem ở [NumPro_WS1213_Vorlesung_Kapitel_4.pdf](quiver-file-url/9DF023CA862D9C7579641DA2EBB56555.pdf)

~~~ cpp
for j from 1 to n do
  for k from j to n do r[j,k]:=a[j,k] od;
  y[j]:=b[j];
  for i from j+1 to n do
     l[i,j]:=a[i,j]/r[j,j];
     for k from j+1 to n do a[i,k]:=a[i,k]-l[i,j]*r[j,k] od;
     b[i]:=b[i]-l[i,j]*y[j]
od od;
for i from n downto 1 do
  x[i]:=y[i];
  for j from i+1 to n do x[i]:=x[i]-r[i,j]*x[j] od;
  x[i]:=x[i]/r[i,i]
od;
~~~