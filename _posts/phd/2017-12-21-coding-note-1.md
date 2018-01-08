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

Trong đó $l=0,1$ đại diện cho $L^2$ và $H^1$ xét trên part của triangle $T\cap\Omega\_i$. Trong đó ổng nói nếu chọn $L^2$ norm thì $l=0,\alpha=2$. Chú ý rằng $\hat{c}=0$ thì xem như không có lọc cái $k$ nào cả, $\bar{V}^{\Gamma}_h=V^{\Gamma}_h$, all discontinuous basis functions are kept. **Tóm lại**, 

$$
\Vert \varphi_k\Vert_{L^2(T\cap\Omega_i)} \le \hat{c}h_T^{\frac{7}{2}}
$$

## Preconditioner, ill-conditioned problem!!!

Có bao nhiêu cách tất cả?

- **Hansbo & Burman**: dùng ghost penalty.
- **Lehrenfeld**: cái này ổng cũng nói về mấy bài báo của Arnold và Burman mà thôi. Từ đây phát hiện ra **không phải Burman và Arnold là hai cách khác nhau** mà mỗi cái có một mục đích riêng
  - *Delete small support basis của Arnold* (Arnold2008) là để:
    - This modiﬁed space has the same approximation quality as the original XFEM space but *better stability properties*. Arnold2008
    - Avoiding very small supports has advantages, for example if the contributions are dominated by rounding errors. *Arnold2008*
    - [Burman 2011] For interface problems, the need to introduce additional ﬁnite element basis functions lying on sub-elements to restore optimal convergence represents a second source of instability.
  - *Ghost penalty của Burman* là để: 
    - [Burman 2011] However, the application of Nitsche’s method for the treatment of boundary or interface conditions may give rise to numerical instabilities in presence of small element cuts. More precisely, it has been observed in [12,15,16,43] that the stability and the condition number of the ﬁnite element scheme depend on how the interface cuts the computational mesh. To cure them, the application of interior penalty stabilisation techniques has been  uccessfully considered in a sequel of papers [12, 15, 16]. The idea of such stabilisation methods is to introduce in the discrete formulation a minimum of artiﬁcial diffusion to ensure the positivity of the discrete bilinear form for any conﬁguration of the boundary or interface.

**Tại sao Hansbo gợi ý dùng stabilization thay vì preconditioning?** Stabilization của Hansbo/Burman chính là Ghost penalty, còn preconditioning thì có nhiều cách (chưa biết cụ thể có phải delete basis small support có phải là preconditioning hay ko)