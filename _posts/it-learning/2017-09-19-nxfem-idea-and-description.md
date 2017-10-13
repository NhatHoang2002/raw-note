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

## Mesh trong matlab

- Tam giác đánh số `i-j-k` theo thứ tự ngược chiều kim đồng hồ. Xem thêm [mesh data](https://fr.mathworks.com/help/pde/ug/mesh-data.html).
- Cái cut triangles `CTs` giống cấu trúc của `msh.t` nhưng thêm hàng thứ 5 chứa index trong `msh.t`



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

Còn $L^2$ có chút khác biệt ở `CTs`. Chúng ta chỉ có dạng $\varphi\_i\varphi\_j$ hoặc $\varphi\_{k(i)}\varphi\_{k(j)}$. Đúng là ý tưởng cũng tương tự cái load vector, có điều nếu load vector tính cho 1 cái `j` thì cái này tính cho 2 cái `i,j`.

(cần bổ sung thêm trong file pdf)

## Ý tưởng của Ghost penalty

Xem thêm trong file coding node (`nxfem_matlab_algorithm.pdf`) và [note này](/maths/nxfem-hansbo-arnold-nitsche/#ghost-penalty), ở đây muốn nói thêm vài ý chính.

**Ghost penalty không có xét các cạnh biên**. Cái này được nói đến trong file `stabilized nistche method Hansbo Burman 2009.pdf`. Trong code của mình cũng không xét các cạnh biên này, điều này làm được bằng cách lúc lấy `eGP` từ `eNBCTs`, chỉ xét các cạnh mà có sự xuất hiện hai lần, tức là các cạnh đó là cạnh chung của hai tam giác trong khi các cạnh biên thì chỉ có 1 lần xuất hiện thôi. Cụ thể là ở dòng code

~~~ matlab
eGP = eNBCTs(:,posF); % contain triangle K
~~~

## Normal vector & GradnPhi ($\nabla\_n \varphi$)

Normal vector của đoạn $\overrightarrow{AB}$ là vector luôn nằm bên **trái**!

Mong muốn code 1 hàm `GradnPhi` để khi nhập cái đỉnh, tam giác, đoạn là nó cho ra kết quả!

Cần lưu ý là có sự khác nhau lớn giữa hai cái sau đây

$$
\int \nabla_n\varphi_i \nabla_n \varphi_j\,dx \qquad \int \nabla\varphi_i\cdot \varphi_j\, dx
$$

## Ý tưởng tính 3 cái $\eta_K, \eta_S, \zeta_S$

Ba cái này là dùng để  dự đoán giá trị của $\gamma$ trong thesis của Barrau, trang 33. Cái ý tưởng này có nói ở trong bài NXFEM rồi, search để xem.

- Hai cái $\eta_K, \eta_S$ đều phải xây dựng một ma trận riêng để tính giá trị của chúng.

- Riêng cái $\zeta_S$ do trùng dạng với chuẩn 

  $$
  \Vert u-u_h \Vert^2_{h,\Gamma} = \sum_{S\in S^{\Gamma}_h}\gamma \Vert [u-u_h]\Vert^2
  $$

  chỉ khác cái hệ số $\gamma$ thôi nên có thể viết về cùng 1 form tính chuẩn của jump được. Còn cái hệ số đi kèm thì tính riêng giống như file `getLambda` vậy, cái đó cũng tính riêng.

- Ý tưởng tính cái $\zeta_S$ là tính cái ma trận, tính cái này cũng giống như tính trong hàm `getMatrixOnGamCTs`, đó chính là file `getMatNormJumpU`.

- ​




