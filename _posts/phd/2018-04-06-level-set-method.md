---
title: Level Set Method
categories:
  - maths
  - phd
toc: 1
maths: 1
---

## Ghi chú mới

Câu hỏi đặt ra là

1. Giải level set equations trên $V^{\Gamma}\_h$ luôn hay là phải giải riêng trên 1 mesh khác?
2. Áp dụng Characteristic luôn không? (giống trong `convect` của ff++ và của chị Cúc)

---

Giới thiệu về Level Set method có thể bắt chước của chị Cúc. Trong thèse, chương 3.1, chương 1.3 cũng có nói tí tí.

---

Chứng minh zero level solution of phương trình Hyperbolic (Cauchy problem) describes the position of the interface. $\Rightarrow$ xem Exercise 4.1 của **Lehrenfeld NOTE 2015.pdf**, có solution luôn!

---

Trong **Trung Hieu thesis**, 2.3, anh ấy có nói lý do tại sao **không cần xét boundary condition** cho level set, trong thèse của chị Cúc cũng có nói, chương 3.1.

Trong Trung Hieu có nói thêm 

## Ghi chú cũ

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