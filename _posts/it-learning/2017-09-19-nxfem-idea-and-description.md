---
title: NXFEM - idea and description
description: detail descriptions
categories:
  - it-learning
type: Document
use_math: true
---

Cái này là phiên bản khác của cái ghi chú file `nxfem_matlab_algorithm.pdf` trong thư mục `\matlab\readme`.

## Ý tưởng của việc code matlab với FEM

Làm sao từ bilinear form (dạng $a(u,v)=(f,v)$) cho đến `AU=F`? Có thể đọc trang 20 (1D) sách của Claes. Bên dưới là ghi ngắn gọn.

$$
a(u,v)=(f,v) 
\Leftrightarrow 
\int_{\Omega}uv=\int_{\Omega}fv
$$

Mà $u=\sum\_iu\_i\varphi\_i$ nên

$$
\begin{align}
\int_{\Omega}(\Sigma u_i\varphi_i)\varphi_j&=\int_{\Omega}f\varphi_j, \quad \text{for } j=1,\ldots,N. \\
\Leftrightarrow
\sum_i u_i\int_{\Omega}(\varphi_i)\varphi_j &=\int_{\Omega}f\varphi_j \\
\Leftrightarrow
AU&=F
\end{align}
$$

Trong đó $A\_{ij}=\int\_{\Omega}\varphi\_i\varphi\_j = \Sigma\_K\int\_K\varphi\_i\varphi\_j$ và $F\_j=\int\_{\Omega}f\varphi\_j = \Sigma\_K\int\_Kf\varphi\_j$.

The main idea to implement FEM is that we will find the value of matrix A at nodes of each triangle and then take a sum of all triangles in the domain. Values at nodes with the same number will be added together.

## Ý tưởng code của NXFEM

If we are working on the standard FEM, we can consider at the same time all of triangles in the mesh because, basically, they are "he same". However, it’s more difficult in NXFEM because it’s different in the cut triangles. We need to add "more nodes" (more basic functions) to the standard mesh.

## Ý tưởng code $L^2$ norm

Có đoạn nói là áp dụng ý tưởng khi tính load vector. Xem lại ý tưởng tìm load vector. Để tính cái này chủ yếu cần tính từng lượng 

$$
F_j 
= \int_{\Omega}f\varphi_j 
= \sum_K\int_Kf\varphi_j 
= \sum_{CTs}\int_Kf\varphi_j + \sum_{NCTs}\int_Kf\varphi_j.
$$

Với `NCTs` (not cut triangles), ta tính bình thường, chỉ cẩn trọng tại những node around interface vì những node đó có thể là `k(i)`.

Với `CTs` thì khó hơn do mỗi đỉnh có tới 2 basic functin (`i` và `k(i)`) nên trong file `getLoadCTs` có tính `FCT1, FCT2` tại mỗi đỉnh. Chủ yếu là dùng quadrature rule cho tam giác (`getLoadPartTri`), tứ giác thì lấy cái lớn trừ cái nhỏ (`getLoadWholeTri-getLoadPartTri`).

Còn $L^2$ có chút khác biệt ở `CTs`. Chúng ta chỉ có dạng $\varphi\_i\varphi\_j$ hoặc $\varphi\_i\varphi\_j$. Đúng là ý tưởng cũng tương tự cái load vector, có điều nếu load vector tính cho 1 cái `j` thì cái này tính cho 2 cái `i,j`.