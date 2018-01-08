---
layout: post
title: Ghost penalty
categories: maths
tags: ["ghost penalty","robust","interface"]
maths: 1
toc: 1
---

*Đem từ mấy cái file khác sang hẳn đây vì nó nhiều thứ để nói*

{% include toc.html %}

## Tại sao phải cần ghost penalty?

Cái này được nói trong file `burman2010-ghost penalty.pdf`.

In fictitious domain methods (see [5] or for more recent work [2,7,8]) one is often faced with the choice of either 

- integrating the equations over the whole computational mesh, i.e. also in the non-physical part, or 
- only integrate within the physical domain. 

**In the first case** the method is robust, but inaccurate due to the lack of consistency. 

Methods using **the second approach**, on the other hand, are accurate, but the condition number of the finite element matrix depends on how the domain boundary cuts the mesh. If the cut results in elements with very small intersections with the physical domain, the system matrix may be very ill-conditioned, as we show below.

## References

- **Burman2014** thì nói nhiều về kỹ thuật và ứng với nhiều loại domain, còn bài báo **Burman2009** thì giải thích tại sao khi thêm ghost penalty này thì condition number lại không phụ thuộc vào cách interface cắt mesh.
- How conditioning of the matrix doesn't depend on the way interface cuts triangles, cf. **Burman2009**. They way we can construct a normal vector used in the formulas
- **Lehrenfeld2015** (3.4.2) : a small introduction and some comments on this
- There is an example in detail with **Capatina2015**
- **Burman2010** Note ghi chú chủ đề chính là ghost penalty luôn!
-  **ghost penalty term** (trang 8, [ở đây](https://hal.inria.fr/hal-01149225/file/RR-8723.pdf))

## Ý tưởng chính

Xem 2.2 trong bài báo của Burman2014. Cái này mình có ghi chú lần đầu trong **quyển ghi chú 2.** Trong form $a_h(u,v)=(f,v)$ thì $a_h(u,v)$ thêm một lượng $j(u,v)$

$$
j(u,v) = \sum_{F\in \mathcal{F}_G} \langle \gamma_1 h [\nabla u],[\nabla v] \rangle_F
$$

Trong đó $\mathcal{F}\_G$ : element faces associated with $G_h$ = all elements that cut by the interface.

$$
\forall F\in \mathcal{F}_G, \exists K,K': F=K\cap K' : K \in G_h \text{ or }K'\in G_h. \\
[\nabla u] = n_F\cdot \nabla v|_K - n_F\cdot \nabla v|_K'
$$

$F$ = unit normal to face $F$ with fixed but arbitary orientation. The boundary faces of the mesh $\mathcal{T}\_h$ are excluded from $\mathcal{F}\_G$. Cái $j(u,v)$ ở trên là dành cho model với fictitious domain.

---

Cần chứng minh $a\_h(u,u) + j(u,u) \ge C \Vert u \Vert\_h^2$, trong đó $a_h$ chứa $\int\_{\Omega}$ còn $\Vert \cdot \Vert_h$ chứa $\int\_{\Omega\_T}$. Cái sau contains part of triangles outside $\Omega$. Do đó cần $j(\cdot,\cdot)$ to recover coercivity of the part of the triangles that are not in $\Omega$

---

Trong Note của Lehrenfeld có giải thích ý tưởng cho **ghost penalty** của Burman khá hay, trang 48.

> **Remark 3.5 (Ghost penalty for Nitsche-XFEM)**. In the context of interface problem the “ghost penalty” stabilization is interesting in cases where the weights of the averaging operator should be signiﬁcantly diﬀerent from the hansbo -choice, for instance for large contrast problems (see [BZ12]). In this case the Nitsche-XFEM discretization lacks stability (and suﬀers from arising ill-conditioned linear systems). By adding the “ghost penalty” stabilization the averaging operator is freed from the constraint that has been necessary to ensure stability (essentially (3.27)).

> **Remark 3.7 (Conditioning)**. The Ghost penalty method ensures that conditioning of the resulting system matrix is well-behaved. This holds true for boundary and interface problems. Note that even for the interface problem with the hansbo -averaging (where stability is not a problem) the resulting system matrix is ill-conditioned. In contrast to the boundary problem this can however be easily ﬁxed by suitable preconditioning strategies which is discussed in the next section.

---

[Burman 2011] The idea of such stabilisation methods is to introduce in the discrete formulation a minimum of artiﬁcial diffusion to ensure the positivity of the discrete bilinear form for any conﬁguration of the boundary or interface.

### Ý tưởng code

Xem thêm trong file coding node (`nxfem_matlab_algorithm.pdf`) và [note này](/maths/nxfem-hansbo-arnold-nitsche/#ghost-penalty), ở đây muốn nói thêm vài ý chính.

**Ghost penalty không có xét các cạnh biên**. Cái này được nói đến trong file `stabilized nistche method Hansbo Burman 2009.pdf`. Trong code của mình cũng không xét các cạnh biên này, điều này làm được bằng cách lúc lấy `eGP` từ `eNBCTs`, chỉ xét các cạnh mà có sự xuất hiện hai lần, tức là các cạnh đó là cạnh chung của hai tam giác trong khi các cạnh biên thì chỉ có 1 lần xuất hiện thôi. Cụ thể là ở dòng code

~~~ matlab
eGP = eNBCTs(:,posF); % contain triangle K
~~~

Thật ra ý tưởng **không xét cạnh biên** nó là xét các cạnh thỏa nó là giao của hai tam giác. Các cạnh biên chỉ thuộc 1 tam giác nên không lấy. Cái ý này đọc ở note của Lehrenfeld trang 48 pdf.

## Fictitious domain

**Fictitious domain** (hiểu) : Là một domain bình thường $\Omega$ nhưng biên của nó có thể "co giãn" và thay đổi được. Có thể xem interface thì là phân biệt hai miền $\Omega_i$ thì fictitious domain này có $\partial \Omega$ đóng vai trò giống như interface nhưng không có phân biệt rõ hai miền.

Mesh $\mathcal{T}\_h$ to hơn và bao phủ luôn cái $\Omega$, cái ghost penalty terms act also on the part of the elements that are outside the domain.

Cái này nói nhiều trong bài báo **Burman2009**. Trong đây có nói $C_P$ cũng phụ thuộc vào $\Gamma$ nhưng không có phụ thuộc vào cách $\Gamma$ cắt the mesh. Do trong phương trình không có $K_i$ so với $K$. Do đó có thể control condition under a good bound.

## Cách làm

Trong bài báo **Burman2014** thì tác giả miêu tả các thức để có thể tính lượng $j(u,v)$. Ta không xét các edges ở rìa ngoài của $\Omega_i$, nghĩa là vẫn xét các cạnh rìa trong không bị cắt bởi interface. Nhưng trong bài báo **Capatina2015** thì ổng lại bảo chỉ xét các edges bị cắt bởi interface thôi, nghĩa là không có xét các cạnh ko bị cắt!

$\Rightarrow$ Do hai pp này cơ bản là khác, 1 cái làm việc trên conforming, 1 cái làm việc với non-conforming FEM (có thêm lượng jum qua edge) nên sẽ làm theo cách của Burman!!!

Trong note của **Lehrenfeld2015** cũng có nói về cái ghost này, cái này cũng lấy ý tưởng từ Burman thôi! Mục 3.4.2.

Có sự khác nhau lớn giữa ý tưởng ghost penalty của **Capatina2015** và của **Burman2014**. Cái sau thì chỉ cần cộng thêm lượng $j_i(u,v)$ vào $a_h(u,v)$ là xong. Nhưng cái đầu thì nó cộng thêm lượng $A_h$ nữa, lượng này là 2 terms tính trên các cạnh bị cắt

$$
A_h(u,v) = - \sum_{i=1}^2 \sum_{e\in E^{i,cut}_h} \int_e \{ k\nabla u \cdot n \}_e [v]_e + \{ k\nabla v\cdot n \}_e[u]_e\, ds
$$

Được cái bài báo **Capatina2015** nếu khá chi tiết các thông số cụ thể cho các parameters.

## Nonconforming NXFEM with ghost penalty

Có nói ở phần trước rồi. Cái nonconforming này nói trong bài báo **Capatina2015 ** (của El-Otmany), đại ý thế này

- nonconfotming là có thể không liên tục qua các edges, có thêm lượng $\int\_e[v]=0$ qua các edge trong cách định nghĩa không gian $V\_h$.
- Còn của Hansbo là không liên tục qua $\Gamma$ chứ vẫn liên tục qua các edges (conforming).
- discrete form khác, cái này có cộng thêm lượng $A\_h$ (bên dưới) vào bilinear nữa, ngoài cái penalty và ghost penalty. Tức là 

$$
a_h(u_h,v_h)+A_h(u_h,v_h)+j(u_h,v_h) = (f,v_h).
$$

trong đó,

$$
A_h(u,v) = - \sum_{i=1}^2 \sum_{e\in E^{i,cut}_h} \int_e \{ k\nabla u \cdot n \}_e [v]_e + \{ k\nabla v\cdot n \}_e[u]_e\, ds
$$