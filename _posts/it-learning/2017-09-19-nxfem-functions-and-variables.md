---
title: NXFEM: functions and variables
description: quick description
categories:
  - it-learning
type: Document
use_math: true
---

## Functions

`getDiam`: Get the diameter (longest side) of each triangle in the mesh.

- Input: `getDiam(points,triangles)`, points and triangles of the mesh.
- Output: 1 x number of triangles vector `hT`

~~~ matlab
hTCTs = hT(CTs(5,:)); % consider only on cut triangles
~~~

---





## Variables

- Xem [Mesh data](https://fr.mathworks.com/help/pde/ug/mesh-data.html) để biết ý nghĩa của `points, edges, triangles` (p,e,t) trong mesh.
- `points`: (2xnP) all points of the mesh. Hàng đầu là `x`, hàng thứ hai là `y`.
- `edges`: (7xnE) tất cả cạnh ở biên chứ ko phải là tất cả cạnh của mesh.
- `triangles`: (4xnT) all triangles of the mesh. 3 hàng đầu là chỉ số của điểm, hàng cuối cùng là region, domain.
- `CTs`,`omg1NCTs`, `omg2NCTs`: (5xnT) cut triangles, not-cut triangles in each subdomain. Cái này cấu trúc giống `triangles` nhưng mình thêm dòng cuối để cho biết đó là tam giác nào.

