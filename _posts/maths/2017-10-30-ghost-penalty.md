---
title: Ghost penalty
categories:
  - maths
type: Document
use_math: true
---

*Đem từ mấy cái file khác sang hẳn đây vì nó nhiều thứ để nói*

### References

- **Burman2014** thì nói nhiều về kỹ thuật và ứng với nhiều loại domain, còn bài báo **Burman2009** thì giải thích tại sao khi thêm ghost penalty này thì condition number lại không phụ thuộc vào cách interface cắt mesh.
- How conditioning of the matrix doesn't depend on the way interface cuts triangles, cf. **Burman2009**. They way we can construct a normal vector used in the formulas
- **Lehrenfeld2015** (3.4.2) : a small introduction and some comments on this
- There is an example in detail with **Capatina2015**
- **Burman2010** Note ghi chú chủ đề chính là ghost penalty luôn!

### Ý tưởng chính

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

### Fictitious domain

**Fictitious domain** (hiểu) : Là một domain bình thường $\Omega$ nhưng biên của nó có thể "co giãn" và thay đổi được. Có thể xem interface thì là phân biệt hai miền $\Omega_i$ thì fictitious domain này có $\partial \Omega$ đóng vai trò giống như interface nhưng không có phân biệt rõ hai miền.

Mesh $\mathcal{T}\_h$ to hơn và bao phủ luôn cái $\Omega$, cái ghost penalty terms act also on the part of the elements that are outside the domain.

Cái này nói nhiều trong bài báo **Burman2009**. Trong đây có nói $C_P$ cũng phụ thuộc vào $\Gamma$ nhưng không có phụ thuộc vào cách $\Gamma$ cắt the mesh. Do trong phương trình không có $K_i$ so với $K$. Do đó có thể control condition under a good bound.

### Cách làm

Trong bài báo **Burman2014** thì tác giả miêu tả các thức để có thể tính lượng $j(u,v)$. Ta không xét các edges ở rìa ngoài của $\Omega_i$, nghĩa là vẫn xét các cạnh rìa trong không bị cắt bởi interface. Nhưng trong bài báo **Capatina2015** thì ổng lại bảo chỉ xét các edges bị cắt bởi interface thôi, nghĩa là không có xét các cạnh ko bị cắt!

$\Rightarrow$ Do hai pp này cơ bản là khác, 1 cái làm việc trên conforming, 1 cái làm việc với non-conforming FEM (có thêm lượng jum qua edge) nên sẽ làm theo cách của Burman!!!

Trong note của **Lehrenfeld2015** cũng có nói về cái ghost này, cái này cũng lấy ý tưởng từ Burman thôi! Mục 3.4.2.

Có sự khác nhau lớn giữa ý tưởng ghost penalty của **Capatina2015** và của **Burman2014**. Cái sau thì chỉ cần cộng thêm lượng $j_i(u,v)$ vào $a_h(u,v)$ là xong. Nhưng cái đầu thì nó cộng thêm lượng $A_h$ nữa, lượng này là 2 terms tính trên các cạnh bị cắt

$$
A_h(u,v) = - \sum_{i=1}^2 \sum_{e\in E^{i,cut}_h} \int_e \{ k\nabla u \cdot n \}_e [v]_e + \{ k\nabla v\cdot n \}_e[u]_e\, ds
$$

Được cái bài báo **Capatina2015** nếu khá chi tiết các thông số cụ thể cho các parameters.

### Ý tưởng code của Ghost penalty

Xem thêm trong file coding node (`nxfem_matlab_algorithm.pdf`) và [note này](/maths/nxfem-hansbo-arnold-nitsche/#ghost-penalty), ở đây muốn nói thêm vài ý chính.

**Ghost penalty không có xét các cạnh biên**. Cái này được nói đến trong file `stabilized nistche method Hansbo Burman 2009.pdf`. Trong code của mình cũng không xét các cạnh biên này, điều này làm được bằng cách lúc lấy `eGP` từ `eNBCTs`, chỉ xét các cạnh mà có sự xuất hiện hai lần, tức là các cạnh đó là cạnh chung của hai tam giác trong khi các cạnh biên thì chỉ có 1 lần xuất hiện thôi. Cụ thể là ở dòng code

~~~ matlab
eGP = eNBCTs(:,posF); % contain triangle K
~~~