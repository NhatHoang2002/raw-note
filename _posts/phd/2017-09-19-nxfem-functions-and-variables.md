---
title: NXFEM - functions and variables
categories:
  - maths 
  - it 
  - phd
maths: 1
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

---

~~~ matlab
gradPhi = getGradPhi(tris,msh)
~~~

Cái này tính Grad cho cái $\varphi$ gốc luôn. Giống như cái công thức bên dưới (tính thông qua các cạnh tam giác)
$$
\begin{align}
    \nabla \varphi_i (x,y) 
    &= \dfrac{1}{2\vert \tau\vert}  \mathbf{n}_i   
    = \dfrac{1}{2\vert \tau\vert} \begin{bmatrix} y_j-y_k \\ x_k -x_j \end{bmatrix},
\end{align}
$$
Đây chính là **inward normal vector** của cạnh đối diện với đỉnh đó (quay vào trong tam giác). Có thể tham khảo thêm công thức này ở file matlab của Long Chen và file 50 lines.

Có hai cách để tính xoay vòng, trong đoạn code là dùng hàm bậc hai

~~~ matlab
j = -3/2*i^2+11/2*i-2 % vertex j
k = 3/2*i^2-13/2*i+8 % vertex k
~~~

Tuy nhiên cũng có thể dùng hàm `floor` và `mod` như sau

~~~ matlab
j=mod(i+1,3)+3*floor((3-mod(i+1,3))/3); % vertex j
k=mod(i+2,3)+3*floor((3-mod(i+2,3))/3); % vertex k
~~~

---

~~~ matlab
gnp = getGradnPhi(i,t,pA,pB,msh)
~~~

Find $\nabla_n \varphi\_i$ of triangle `t` at vertex `i` on the segment `AB` (from A to B).

---

~~~ matlab
[eGP,neighborCTs] = getGPEdges(CTs,phi,msh)
~~~

- Hàm này để lấy thông tin của một cạnh để tính jump trên cạnh đó.  Có thể thay thế `CTs` bởi những `tris` khác cũng được.
- `neighborCTs` vector chứa chỉ số (trong `msh.t`) của các tam giác "lân cận" của `CTs`
- Nói về `eGP`  (5 x number of edges cần tính)
  - `eGP(1:2,:)`: 2 endpoints of the edge (chỉ số trong `msh.p`)
  - `eGP(3:4,:)`: 2 tam giác hai bên cạnh đó. Chỉ số của hai tam giác này là chỉ số của 





## Variables

- Xem [Mesh data](https://fr.mathworks.com/help/pde/ug/mesh-data.html) để biết ý nghĩa của `points, edges, triangles` (p,e,t) trong mesh.
- `points`: (2xnP) all points of the mesh. Hàng đầu là `x`, hàng thứ hai là `y`.
- `edges`: (7xnE) tất cả cạnh ở biên chứ ko phải là tất cả cạnh của mesh.
- `triangles`: (4xnT) all triangles of the mesh. 3 hàng đầu là chỉ số của điểm, hàng cuối cùng là region, domain.
- `CTs`,`omg1NCTs`, `omg2NCTs`: (5xnT) cut triangles, not-cut triangles in each subdomain. Cái này cấu trúc giống `triangles` nhưng mình thêm dòng cuối để cho biết đó là tam giác nào.

