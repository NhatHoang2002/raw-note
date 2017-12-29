---
title: Coding note 1
categories:
  - maths
  - phd
  - it
maths: 1
toc: 1
---

Loạt bài này chủ yếu dùng để *ghi chú* trong quá trình hoàn thành cái coding. Có thể đó là những ghi chú về kiến thức, thuật toán liên quan. Cái này dùng để "gọi đến" trong cái ghi chú Working daily trong Evernote.

## Small intersection

Bài báo `analysis of xfem 2008.pdf` nói về cách xử lý các cái cut quá nhỏ. Còn bài báo `burman2010-ghost penalty.pdf` thì có nhắc đến nếu các cái cut quá nhỏ có thể dẫn đến matrix is ill-conditioned. Tuy nhiên bài báo của Burman chủ yếu làm việc trên fictitious domain.

Nhỏ là như thế nào? Nghĩa là

$$
\dfrac{\vert \varphi^1_k \vert}{\vert \varphi_k\vert} \ll 1
$$

Do đó, ý tưởng là xóa bớt đi các basis function với support rất nhỏ này, tức tạo thành 1 space mới "nhỏ hơn" space $V^{\Gamma}\_h$. Ổng cũng giải thích làm cách nào để chọn maximal size cho these "small support" này.

Sẽ loại bỏ những basis (những cái $k$) thỏa điều kiện sau (p6)

$$
\Vert \varphi_k\Vert_{l,T\cap\Omega_i} \le \hat{c}h_T^{\alpha+1\frac{1}{2}-l}
$$

Trong đó $l=0,1$ đại diện cho $L^2$ và $H^1$ xét trên part của triangle $T\cap\Omega\_i$. Trong đó ổng nói nếu chọn $L^2$ norm thì $l=0,\alpha=2$. Chú ý rằng $\hat{c}=0$ thì xem như không có lọc cái $k$ nào cả, $\bar{V}^{\Gamma}_h=V^{\Gamma}_h$, all discontinuous basis functions are kept.

**Tóm lại**, 

$$
\Vert \varphi_k\Vert_{L^2(T\cap\Omega_i)} \le \hat{c}h_T^{\frac{5}{2}}
$$

## Preconditioner, ill-conditioned problem!!!

Có bao nhiêu cách tất cả?

- Hansbo & Burman: dùng ghost penalty.
- Lehrenfeld: 