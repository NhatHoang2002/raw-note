---
title: NXFEM - functions and variables
description: quick description
categories:
  - it-learning
type: Document
use_math: true
---

## Functions

~~~ matlab
hTCTs = hT(CTs(5,:)); % consider only on cut triangles
~~~

Get the diameter (longest side) of each triangle in the mesh.

- Input: `getDiam(points,triangles)`, points and triangles of the mesh.
- Output: 1 x number of triangles vector `hT`

---

~~~ matlab
mL2 = getMatrixL2(omg1NCTs,omg2NCTs,areaNCTs1,areaNCTs2,...
                iPs,CTs,typeCTs,idxEachCTs,areaCTs,nodesCTsInOmg2OnGam);
~~~

Get matrix $A\_{L^2}$. Thật ra cái này dùng để tính norm trong $L^2$ luôn cũng được. Ví dụ muốn tính $\Vert f \Vert\_{L^2}$ thì chỉ cần biểu diễn $f$ trong $V^{\Gamma}\_h$ rồi sau đó tính $fA\_{L^2}f^T$.

Hàm này mình viết khi muốn tính $\Vert e \Vert\_{L^2}$ với $e=u-uex$.

Còn nếu muốn tính $\Vert \nabla e \Vert\_{L^2}$ thì dùng hàm 

~~~ matlab
mL2grad = getMatrixL2Grad(omg1NCTs,omg2NCTs,nodesCTsInOmg2OnGam,...
                    CTs,areaChildCTs,areaCTs);
~~~

---

~~~ matlab
valG = getGij_PartTri(triangle,areaT,ii,jj,kk,iP1,iP2,remainVertex,dim,deg)
~~~

Tìm giá trị của $\int\_{K^1}g(\varphi\_i,\varphi\_j)$ trên 1 phần của triangle (phần hình tam giác). Xuất ra giá trị.

Còn để tính toàn bộ tam giác thì dùng hàm

~~~
valGij = getGij_WholeTri(areaT,ii,jj,typeG,dim,deg)
~~~

Phần tứ giác thì lấy cái whole - part.

## Variables

- Xem [Mesh data](https://fr.mathworks.com/help/pde/ug/mesh-data.html) để biết ý nghĩa của `points, edges, triangles` (p,e,t) trong mesh.
- `points`: (2xnP) all points of the mesh. Hàng đầu là `x`, hàng thứ hai là `y`.
- `edges`: (7xnE) tất cả cạnh ở biên chứ ko phải là tất cả cạnh của mesh.
- `triangles`: (4xnT) all triangles of the mesh. 3 hàng đầu là chỉ số của điểm, hàng cuối cùng là region, domain.
- `CTs`,`omg1NCTs`, `omg2NCTs`: (5xnT) cut triangles, not-cut triangles in each subdomain. Cái này cấu trúc giống `triangles` nhưng mình thêm dòng cuối để cho biết đó là tam giác nào.

