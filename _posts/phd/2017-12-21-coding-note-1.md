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