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