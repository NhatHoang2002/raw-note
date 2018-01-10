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
  - ***Delete small support basis của Arnold* (Arnold2008) là để**:
    - This modiﬁed space has the same approximation quality as the original XFEM space but *better stability properties*. Arnold2008
    - Avoiding very small supports has advantages, for example if the contributions are dominated by rounding errors. *Arnold2008*
    - [Burman 2011] For interface problems, the need to introduce additional ﬁnite element basis functions lying on sub-elements to restore optimal convergence represents a second source of instability.
  - ***Ghost penalty của Burman* là để**: 
    - [Burman 2011] However, the application of Nitsche’s method for the treatment of boundary or interface conditions may give rise to numerical instabilities in presence of small element cuts. More precisely, it has been observed in [12,15,16,43] that the stability and the condition number of the ﬁnite element scheme depend on how the interface cuts the computational mesh. To cure them, the application of interior penalty stabilisation techniques has been  uccessfully considered in a sequel of papers [12, 15, 16]. The idea of such stabilisation methods is to introduce in the discrete formulation a minimum of artiﬁcial diffusion to ensure the positivity of the discrete bilinear form for any conﬁguration of the boundary or interface.

**Tại sao Hansbo gợi ý dùng stabilization thay vì preconditioning?** Stabilization của Hansbo/Burman chính là Ghost penalty, còn preconditioning thì có nhiều cách (chưa biết cụ thể có phải delete basis small support có phải là preconditioning hay ko)

- Lehrenfeld có nhận xét là ví dụ trong Hansbo với Hansbo-averaging thì không gặp vấn đề với stability nhưng vẫn có vấn đề với matrix ill conditioned. Điều này suy ra stabilisation và preconditioning là hai cái khác nhau rất nhiều, ảnh hưởng nhiều đến vấn đề đang gặp. Phải làm riêng!!!!

$\Rightarrow$ Có vẻ việc delete small support chỉ làm giảm khả năng bị lỗi round-off thôi chứ nó ko phải là preconditioning hay stabilisation!

**PHẢI DÙNG CẢ HAI PHƯƠNG PHÁP!!!!**

## Big condition number problem

Thảo luận cách giải quyết vấn đề về condition number quá lớn.

However, in the methods above, the conditioning of the problem is **sensitive to the position of the interface**. The condition number of the system matrix blows up for cases when the interface approaches element boundaries. For unsteady problems, it is not unusual that such situations occur, and some precaution is needed to prevent problems such as breakdown of direct or iterative linear solvers. Reusken [22] addresses this problem by deleting basis functions in the XFEM space that have very small support and may cause ill-conditioning. ***wadbro 2013 unifomly well-conditioned unfitted Nitsche interface.pdf***

- Bài báo **zunino 2011 unfitted interface penalty contrast.pdf** nói về 
  - Việc trị ill-conditioning by using preconditioning method.
  - cũng dựa trên fictitious domain method
  - Mở rộng ra $H^1$ stability thay vì $L^2$ như trong bài báo của Arnold 2008
  - This analysis of the XFEM space is closed by the proof of discrete inequalities that will be useful to address the stability and conditioning of the scheme proposed in Hansbo 2002
  -  because for such technique both large contrast of diffusion coeﬃcients and small sub-elements negatively affect the condition number of the discrete problem.

### Preconditioning method of Zunino

Phần này nói về ý tưởng preconditioning trong bài báo **Zunino 2011** (có nói tí chút ở trên). 

Thật sự trùng hợp là ý tưởng của Zunino về việc xây dựng 1 ma trận $P$ (trang 1072) cũng giống với ý tưởng trong sách của Arnold trang 274. Có sự khác nhau nhẹ là ở Zunino có nhân thêm các hệ số diff và reaction.

$$
P:= 
\begin{bmatrix}
M^{\Omega}_{\mu} & 0 & 0 \\
0 & \mu_1\text{diag}(M^{\Gamma}_1) &0 \\
0 & 0 & \mu_2\text{diag}(M^{\Gamma}_2)
\end{bmatrix}
+
\begin{bmatrix}
L^{\Omega}_{h,\epsilon} & 0 & 0 \\
0 & \epsilon_1\text{diag}(L^{\Gamma}_1) &0 \\
0 & 0 & \epsilon_2\text{diag}(L^{\Gamma}_2)
\end{bmatrix}
$$

trong đó $v=v^{\Omega} + v^{\Gamma}\_1 + v^{\Gamma}\_2$, $\mu=$ diffusion coefficient, $\epsilon=$ reaction coefficient, $M,L$ lần lượt là mass và stiffness matrix và

$$
\begin{align}
M^{\Omega} \to (v^{\Omega},w^{\Omega})_0, \quad
M_i^{\Gamma} \to (v_i^{\Gamma},w_i^{\Gamma})_0, \\
L^{\Omega} \to (\nabla v^{\Omega},\nabla w^{\Omega})_0, \quad
L_i^{\Gamma} \to (\nabla v_i^{\Gamma},w_i^{\Gamma})_0
\end{align}
$$

Sau đó ta sẽ có ma trận mới $P^{-1}A$ có condition number nhỏ hơn $A$ nhiều.
