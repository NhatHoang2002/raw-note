---
title: Level Set Method
categories:
  - maths
  - phd
toc: 1
maths: 1
date: 2018-06-22
---

## Quick note (rewrite 11/6.18)

- Xem **hw level set workflow 6-2018.pdf**
- Phải dùng Fast Marching Method vì nếu dung cách giải phương trình kia thì không biết chọn tham số như thế nào.
- Trong **Trung Hieu thesis**, 2.3, anh ấy có nói lý do tại sao **không cần xét boundary condition** cho level set, trong thèse của chị Cúc cũng có nói, chương 3.1.
- Chứng minh zero level solution of phương trình Hyperbolic (Cauchy problem) describes the position of the interface. $\Rightarrow$ xem Exercise 4.1 của **Lehrenfeld NOTE 2015.pdf**, có solution luôn!
- Giới thiệu về Level Set method có thể bắt chước của chị Cúc. Trong thèse, chương 3.1, chương 1.3 cũng có nói tí tí, giới thiệu ở 2.2.
- Giải level set phải thông qua 2 bước quan trọng
	- Dùng SDFEM để giải tìm phi (7.2 Arnold book). Dùng Method of lines (giải thích về method này trong knabner book).
	- Dùng FMM để reinitialization.
- Giải tìm trên standard FEM chứ không phải $V_h^{\Gamma}$
- Giải thích tại sao cần $\Vert \nabla\phi\Vert = 1$: 9.3 thesis Eva Loch, trong đó có PDE way (9.3.1), FMM way.
- Giải thích từ ý tưởng $\phi(x,t)=0$ đến phương trình level set: 2.2 jury thesis.
- Ý tưởng về (signed) distance function được giới thiệu trong bài báo *sethian osher 1988*
- Mass conservation: *level set 1996 - Hou et Chang*
- [Trang này](https://profs.etsmtl.ca/hlombaert/levelset/) giải thích ý tưởng về level set khá hay.
- **Narrow node**s: Chopp 1993 (chưa rõ tên bài báo)
	- Cái giải local này có thể xem *pde based fast local level set method - peng 99.pdf*, cái này tối ưu hơn cả cái của Sethian (theo như nó nói). Cái này họ xét nodes trong 1 tube cụ thể chứ ko phải trên toàn domain.
- **Test case**:
	- 3.5.5 trong thesis của Christoph WINKELMANN.
	- file *4.1 level set numerical test case*
	- thesis của Gross Sven mục 10.1
- If a time step causes the change in distance of a pixel to be greater than the grid size, will make the level set unstable, it is necessary to make a prediction on the maximum time step.
	- Cf: *implement level set narrow band - larsen 2005.pdf*
- 

## Fast Marching Method

- **Tóm lại**: có 2 cách reinitialization
	- Cách của Arnold
	- Cách của chị Cúc (p.100 thesis), khác ở chỗ tìm $\sum_{i=1}^3\vert \phi\_i \nabla \lambda_i\vert^2=1$ cho từng element.
- Mục FMM 9.3.2 của Eva Loch thesis khá giống với Arnold.
- Xem ý tưởng trong slide *BEST EXPLAIN fast marching method - Luis Moreno SLIDE 2016.pdf*.
	- Giải thích RẤT HAY và tại sao $T_3$ lại phải được tính theo $T_1,T_2$ có trong *BEST SLIDE fast marching method - Anastasia Dubrovina.pdf*
- Đã hỏi ý kiến của thầy Pascal Frey, ổng bảo đã có code viết về cái này rùi: 
	- [Toolbox FMM (matlab)](https://fr.mathworks.com/matlabcentral/fileexchange/6110-toolbox-fast-marching) của Gabriel Peyré (tham khảo thêm [trang này](http://www.numerical-tours.com/matlab/fastmarching_0_implementing/)).
	- FMM có trong [Charles's ISCDToolbox](https://github.com/ISCDtoolbox), in C, ông này làm chung equip với Pascal.
- **Idea**: Ra một cái $\phi$ mới (sau khi áp dụng cách giải SDFEM): chỉ có zero-level set thôi, chưa có sign distance function. Áp dụng FMM để tìm một cái $\tilde{\phi}$ mới có cả 2 tính chất kia.
- [Trang này](https://math.berkeley.edu/~sethian/2006/Explanations/fast_marching_explain.html) giải thích về FMM khá hay + [video này](https://www.youtube.com/watch?v=Ebi5juth-LE) giải thích ý tưởng FMM (ngôn ngữ lạ + simple problem).
- [Trang này](https://math.berkeley.edu/~sethian/2006/Explanations/fast_marching_explain.html) cũng nói là FMM chỉ thích hợp nếu có giả sử lực $F$ luôn không đổi dấu, tức interface chỉ "nở ra" hoặc "co lại" trong suốt quá trình mà thôi. Mình nghĩ thêm, thật ra mình áp dụng FMM cho mỗi lần reinitialize nên vấn đề dấu của $F$ này có thể bỏ qua được. **Trang này cũng giải thích khá rõ ý tưởng của FMM**.

---

Giải thích tí *BEST SLIDE fast marching method - Anastasia Dubrovina.pdf*

- Slide 18: Khi $T\_3 < T\_1$ thì ta phải lấy $T\_3 = \min\{T\_1,T\_2\} + h$ bởi vì $T\_3$ phải đến sau hai thằng kia mà mỗi bước tiến ít nhất phải là $h$.

---

**Tính sign distance trực tiếp**: This brute force approach has the advantage that it does not move the interface up to
the numerical accuracy of the interpolation scheme. The disadvantage is its high cost and the likelihood of introducing some spurious irregularity into the data, making differentiated quantities such as curvature behave very badly. (*pde based fast local level set method - peng 99.pdf*)

---

Sign distance function:

$$
d(x_0,\Gamma_h) := \min_{x\in \Gamma_h} d(x_0,x).
$$

---

Khi tính khoảng cách (bằng cách geometry) giữa node và segment $\Gamma_h$ thì không có kéo dài đoạn ra: nếu hình chiếu (đường vuông góc từ node đó đến $\Gamma_h$) nằm ngoài đoạn $\Gamma_h^T$ thì khoảng cách sẽ là tính tới hai điểm đầu mút của đoạn, ngược lại (hình chiếu nằm giữa 2 đầu đoạn) thì sẽ tính là đoạn chiếu. cái này nói trong Arnold book p.214.

---

**Tại sao lại phải chia ra thành 3 nhóm nodes?** (như giải thích ở [wiki](https://en.wikipedia.org/wiki/Fast_marching_method#Algorithm))

- 3 nhóm nodes đó là: Accepted, Considered và Far.
- Ta không thể tính trực tiếp khoảng cách từ nodes đến $\Gamma_h$ được vì có nhiều đoạn, ta không biết phải tính khoảng cách từ node đó đến đoạn trong element nào? (Theo như Arnold Book, công thức (7.35) thì lấy min của tất cả các cái)
- Theo như thuật toán thì có vẻ khoản cách từ các nodes *Considered* sẽ được tính thông qua các nodes *Accepted* (why?)

## Ghi chú cũ

**Question**:  $\mathbf{u}$ trong $\partial_t \varphi + \mathbf{u}\cdot\nabla\varphi=0$ có được định nghĩa trên toàn miền hay không? Có bài báo nào chỉ bó hẹp ở 1 subdomain như vấn đề của mình hay không?

- Thèse của chị Cúc $\Rightarrow$ toàn miền.
- Bài báo của Sethian trang 12 **Sethian2003** , thì $u$ trên từng miền có giá trị khác nhau và được tính theo các phương trình khác nhau.
- Thèse của Trung Hiếu lấy từ phương trình N-S nên $u$ cũng tính trên toàn miền.

---

The level sets of $f(x,y)$ are the sets on which the function is constant. A fundamental fact of calculus: The gradient of $f(x,y)$ is perpendicular to its level sets.

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