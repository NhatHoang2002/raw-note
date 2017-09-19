---
title: NXFEM: idea and description
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
\int_{\Omega}uv=\int_{Omega}fv
$$

Mà $u=\sum\_iu\_i\varphi\_i$ nên

$$
\int_{\Omega}(\sigma u_i\varphi_i)\varphi_j=\int_{Omega}f\varphi_j, \quad \text{for} j=1,\ldots,N. \\
\Leftrightarrow
\sigma u_i\int_{\Omega}(\varphi_i)\varphi_j=\int_{Omega}f\varphi_j \\
\Leftrightarrow
AU=F
$$

Trong đó $A\_{ij}=\int\_{\Omega}\varphi\_i\varphi\_j = \sigma\_K\int\_K\varphi\_i\varphi\_j$ và $F\_j=\int\_{\Omega}f\varphi\_j = \sigma\_K\int\_Kf\varphi\_j$.

The main idea to implement FEM is that we will find the value of matrix A at nodes of each triangle and then take a sum of all triangles in the domain. Values at nodes with the same number will be added together.

## Ý tưởng code của NXFEM

If we are working on the standard FEM, we can consider at the same time all of triangles in the mesh because, basically, they are "he same". However, it’s more difficult in NXFEM because it’s different in the cut triangles. We need to add "more nodes" (more basic functions) to the standard mesh.