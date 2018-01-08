---
title: Numerical analysis 2
categories:
  - maths
toc: 1
maths: 1
date: 2017-06-26
---

## Some definitions

### Machine epsilon

Đang tìm cái liên quan đến condition number cũng như bao nhiêu condition number thì hợp lý. Có thể xem bài viết về condition number và 1 chút về machine epsilon trên Math2IT [tại đây](math2it.com/tinh-hop-ly-nghiem-he-phuong-trinh-va-khai-niem-condition-number-cua-mot-ma-tran-ky-3/).

**Machine epsilon** `eps` trong matlab xấp xỉ $2\times 10^{-16}$. It roughly means that numbers are stored with about 15-16 digits of precision. If a number is approximately 1, then that means it can be stored with an error of around 10^(-16) or so. If the number is approximately 1000, then it is stored with an error around 10^(-13) or so.

**Tự hiểu**: cái machine epsilon này có nghĩa là khi tính toán trên các con số thì bản thân cái máy đó (ví dụ matlab) nó sẽ dùng các phương pháp xấp xỉ, làm tròn,... ra được 1 kết quả, kết quả này sẽ sai lệch so với kết quả lý thuyết 1 con số `eps` với số chữ số là $16$ ví dụ như trong matlab. 

## Basis function

### Basis function của Crouzeix-Raviart

Xem [tại đây](http://www.mgnet.org/~douglas/Classes/na-sc/notes/ncfem.pdf) (trang 26), 3 nodes nằm ở trung điểm của các cạnh tam giác. Khi ấy $\varphi\_i(x\_j)=\delta\_{ij}$ trong đó $x\_i$ là trung điểm 3 cạnh.

Cái basis này được nhắc đến trong bài báo của El-Otmany **Capatina2017**.

## Interface vs Boundary

From [http://scicomp.stackexchange.com/questions/10820/boundary-vs-interface
](http://scicomp.stackexchange.com/questions/10820/boundary-vs-interface
)

I'm not particularly familiar with biofilm literature. But in most computational literature, the border of the entire domain of a problem are usually referred to as the boundary. Outside of a boundary, there are no nodes, elements, or anything else under consideration.

The entire domain may also be subdivided into smaller regions. Some of these regions share edges on the boundary of the domain. However, some of these regions share borders between each other that are not boundaries of the domain. Usually these regions have different material properties or different relevant physics and may also have different meshes. The borders between any two regions in a domain are usually referred to as interfaces.

---comment----

In multiphase flow, the boundary between phases is usually referred to as an "interface" to distinguish it from the actual physical boundaries surrounding the system. 

In some literatures, I found that the authors use the term "interfaces" to indicate the geometry position/properties between 2 fluids/phases/something else... However, when they need to use a boundary condition on these interfaces, they call them boundary in term "boundary condition" (not "interface condition"). So, generally, 2 terms are only different about their meaning, is that right? 

## Matrix

In FEM, **stiffness matrix** represents the system of linear equations that must be solved. $AU=F$.

$$
A_{ij} = a(\varphi_j,\varphi_i).
$$

Stiffness matrix is symmetric, i.e., all its eigenvalues are real! Thứ tự trước sau của $i,j$ là khác nhau, cái này có được "nói" ở [cuối bài này của wiki](https://en.wikipedia.org/wiki/Stiffness_matrix).

---

**Mass vs stiffness matrix** có thể xem ở hai file **mass vs stiffness matrix (suji).pdf** và **mass vs stiffness matrix (sayas).pdf**.

- Stiffness matrix: $W_{ij}= \int_{\Omega} \nabla \varphi_j \cdot \nabla \varphi_i dx $
- Mass matrix: $M_{ij} = \int_{\Omega} \varphi_j\varphi_i dx$

Both matrices are symmetric. The mass matrix M is positive deﬁnite. The stiﬀness matrix is positive semideﬁnite and in fact almost positive deﬁnite: if we eliminate take any index i and erase the i−th row and the i−th column of W, the resulting matrix is positive deﬁnite.

The original equation is the Poisson equation $−\Delta u = f$ and no reaction term appears, only the stiﬀness matrix appears. Therefore, *stiﬀness comes from diﬀusion*, *mass proceeds from reaction*.

---

In linear algebra, a **diagonal matrix** is a matrix in which the entries outside the main diagonal are all zero.

---

A matrix, or other problem, is "**badly scaled**" when some numbers in the problem are so much larger than the other that they cannot be kept in memory to the same accuracy, causing some information to be lost.

Reference [https://www.physicsforums.com/threads/badly-scaled-matrix.637148/](https://www.physicsforums.com/threads/badly-scaled-matrix.637148/)

## Lagrangian Finite Elements (Pk)

Cùng tìm hiểu $P^k$ finite element là gì? Cái này xem trong mục 6.3 của freefem++doc. Có thể hiểu sơ sơ, $P^k$ là tập hợp những đa thức bậc cao nhất là $k$.

Có thể đọc thêm ở chương 3 file **aide-memoire element finis - alex ern BOOK.pdf**.

## The Forward/Bakward Euler scheme

Xem thêm ở file **mass vs stiffness matrix (suji).pdf**.

- **The forward Euler scheme**: $\dfrac{\partial u}{\partial t} \simeq \dfrac{u^{m+1}-u^m}{\Delta t}$, tất cả các cái $u$ khác đều là $u^m$. Cho trước $u^m$, tìm $u^{m+1}$.
- **The backward Euler scheme**: $\dfrac{\partial u}{\partial t} \simeq \dfrac{u^{m+1}-u^m}{\Delta t}$, tất cả các cái $u$ khác đều là $u^{m+1}$.

## Stabilization vs Preconditioning

Về định nghĩa và thế nào là **preconditioning**, có thể xem [ở note này](/numerical-analysis-1#preconditioner-condition-number-matrix).

Còn định nghĩa về **stability**, có thể xem ở 

- [Wikipedia](https://en.wikipedia.org/wiki/Numerical_stability): 
  - the growth of round-off errors and/or initially small fluctuations in initial data which might cause a large deviation of final answer from the exact solution
  - **robust** – that is to say, do not produce a wildly different result for very small change in the input data.
  - convergence đòi hỏi phải có stability.
- methods are stable, in the sense that small changes or perturbations in the initial conditions produce correspondingly small changes in the subsequent approximations. *numerical douglas Book* (p.340)
- Cũng trong sách của Douglas, có thể xem về **preconditioning** ở trang 486.
- stability is a property of the discrete problems and depends on the particular choice of norms, but it does not depend on the true solution u in any way. [*numerical lecture note - arnold*] p.11
- 
