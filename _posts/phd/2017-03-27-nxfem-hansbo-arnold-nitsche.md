---
title: NXFEM + Hansbo + Arnold + Nitsche
categories:
  - maths
maths: 1
date: 2017-06-08
---

## Tại sao dùng XFEM thay vì FEM

Đọc trong file ***why_xfem_not_fem.pdf***

## Giải quyết lỗi convergence rate

Convergence rate tính theo $L^2$ và $H^1$ trong code luôn ra kết quả bằng $\frac{1}{2}$ so với thực tế. Tuy nhiên khi lấy các hệ số và chọn form của $\kappa\_i$ giống trong thèse của Barrau (**Barrau2013**) thì lại có $L^2$ đúng (order 2), chỉ có $H^1$ là vẫn còn sai mà thôi.

Bị cái nữa là thêm ghost penalty vào rồi như vẫn sai.

Dự đoán là do cách chọn giá trị của $\lambda$ (penalty coefficient). Cô mới nảy ra 1 ý tưởng để chọn lượng $\lambda$ này (meeting 18/9/2017), dựa vào posteriori error estimate (xem trang 33, 34 của thèse Barrau, **Barrau2013**). Đại khái ý tưởng đó như sau

$$
erreur \le \eta_1 + \lambda\eta_2.
$$

How to choose $\lambda$?

- Nếu $\eta\_1 \gg \lambda\eta\_2$ (tức lượng chứa $\lambda$ không ảnh hưởng đến vế phải cho lắm) thì $\lambda$ đó hợp lý.
- Nếu $\eta\_1 < \lambda\eta\_2$ thì ta giảm giá trị của $\lambda$ để trở về trường hợp trên.

Do đó, sau khi đã có được $u\_h$ rồi, hãy tính thử mấy lượng $\eta\_1, \eta\_2$ để điều chỉnh giá trị của $\lambda$.

## Nitsche's method idea

This idea is given in **nitscheIdea**. Suppose that we have a problem,

$$
\begin{align*}
    -\Delta u&=f \quad \text{on }\Omega\\
    u&=g \quad \text{on }\partial\Omega.
\end{align*}
$$

We now want to looking for a variational formulation such that

1. consistent
2. symetric in $u$ and $v$
3. admit a unique solution (bilinear form is coercive)

Normally,

$$
\begin{align*}
    (\nabla u\cdot\nabla v) - \int_{\partial\Omega}\nabla_nuv = (f,v).
\end{align*}
$$

We need the symetric,

$$
\begin{align*}
    (\nabla u\cdot\nabla v) - \int_{\partial\Omega}\nabla_nuv - \int_{\partial\Omega}(u-g)\nabla_nv &= (f,v).\\
    (\nabla u\cdot\nabla v) - \int_{\partial\Omega}\nabla_nuv - \int_{\partial\Omega}u\nabla_nv &= (f,v) - \int_{\partial\Omega}g\nabla_nv.
\end{align*}
$$

We need

$$
\begin{align*}
    (\nabla u\cdot\nabla v) - \int_{\partial\Omega}\nabla_nuv - \int_{\partial\Omega}u\nabla_nv + \lambda \int_{\partial\Omega}(u-g)v &= (f,v) - \int_{\partial\Omega}g\nabla_nv.\\
    (\nabla u\cdot\nabla v) - \int_{\partial\Omega}\nabla_nuv - \int_{\partial\Omega}u\nabla_nv + \lambda \int_{\partial\Omega}uv &= (f,v) - \int_{\partial\Omega}g\nabla_nv + \lambda \int_{\partial\Omega}gv.
\end{align*}
$$

Tóm lại, ta cộng thêm với một lượng $\int_{\partial\Omega}(u-g)(\nabla_nv+\lambda v)$ trong đó $\nabla_n v$ để tạo thành lượng symetric với lượng $\nabla_n uv$ có sẵn, còn $\lambda v$ là cho coercivity.

## NXFEM from Hansbo's idea

- Tên gọi khác, được nhắc đến trong **Capatina2017**, "unfitted FEM" hoặc "CutFEM".
- Nói về robustness wrt both geometry and the physical coefficients.

### Triple norm of $v$ in standard finite element $V^h$

Triple norm $\Vert v \Vert\_3^2:= \Vert \{\nabla\_n v \} \Vert^2\_{-1/2,h,\Gamma} + \Vert  v \Vert^2\_{1/2,h,\Gamma} +  \Vert v \Vert^2\_{H^1(\Omega\_1\cup\Omega_2)}$ where

$$
\Vert{v}\Vert^2_{\frac{1}{2},h,\Gamma}:=\Sigma_{K\in G_h}{}{h_K^{-1}\Vert{v}\Vert^2_{L^2(\Gamma_K)}}, \quad \Vert{v}\Vert^2_{-\frac{1}{2},h,\Gamma}:=\Sigma_{K\in G_h}{}{h_K\Vert{v}\Vert^2_{L^2(\Gamma_K)}}
$$

If $v\in V_h$, or $v=\sum_iv_i\varphi_i$ then $[v]\vert_{\Gamma}=0$. This implies $\Vert{[v]}\Vert^2_{1/2}=0$.

Because this norm is defined only on the area around the interface, so we only consider nodes around the interface.

$$
\begin{align*}
    \Vert{\{\nabla_n v\}}\Vert_{-1/2}^2 &= \sum_Kh_K\Vert{\kappa_1\nabla_{n_1}v_1+\kappa_2\nabla_{n_1}v_2}\Vert_{L^2(\Gamma_K)}^2.\\
    &= \sum_Kh_K\left({\kappa_1\nabla_{n_1}v_1+\kappa_2\nabla_{n_1}v_2,\kappa_1\nabla_{n_1}v_1+\kappa_2\nabla_{n_1}v_2}\right)_{\Gamma_K}.
\end{align*}
$$

For $i,j\in N_G$ (nodes around the interface),

$$
\begin{align*}
    \Vert{\{\nabla_n v\}}\Vert_{-1/2}^2 = \sum_Kh_K\left({\nabla_{n_1}\varphi_i,\nabla_{n_1}\varphi_j}\right)_{\Gamma_K}.
\end{align*}
$$

$\Rightarrow$ Cẩn thận cái nhận xét này, có thể sai! Note that $\nabla_{n_1}\varphi_i\vert_{\Omega_1} = \nabla_{n_1}\varphi_i\vert_{\Omega_2}$ and $\nabla_{n_1}\varphi_i\vert_{\Omega_1} = -\nabla_{n_2}\varphi_i\vert_{\Omega_2}$. Nói cách khác, nó chỉ trái dấu khi xét hai normal vector khác hướng nhau thôi.

**Còn nếu muốn check xem chúng có phải thực sự là norm hay không.**


### Basic functions defined as in Hansbo

Cô trả lời trong email ngày 16/12/15, the new basis functions are discontinuous at the interface:

$$
\begin{align*}
    \varphi_i\vert_{\Omega_1}(x_{\Gamma}) := \lim_{x\vert_{\Omega_1}\to x_{\Gamma}}\varphi_i(x) &= \varphi_i(x_{\Gamma}) \\
    \varphi_{k(i)}\vert_{\Omega_1}(x_{\Gamma}) := \lim_{x\vert_{\Omega_1}\to x_{\Gamma}}\varphi_{k(i)}(x) &= 0 \\
    \varphi_i\vert_{\Omega_2}(x_{\Gamma}) := \lim_{x\vert_{\Omega_2}\to x_{\Gamma}}\varphi_i(x) &= 0\\
    \varphi_{k(i)}\vert_{\Omega_2}(x_{\Gamma}) := \lim_{x\vert_{\Omega_2}\to x_{\Gamma}}\varphi_{k(i)}(x) &= \varphi_{k(i)}(x_{\Gamma}) = \varphi_i(x_{\Gamma})
\end{align*}
$$


### Tại sao ta có form của $a_{vh}$ liên quan tới $B=0$ on $\Gamma$

Ta có phương trình

$$
\begin{align}\tag{\ref{main_v}}
    \begin{split}
        -\nabla \cdot (\beta \nabla v) - q(v) &= 0\quad \text{in }\Omega_i,\, i=1,2,  \\
        v=\nabla_{\mathbf{n}}v&=0\quad \text{on }\Gamma,\\
        v+\varepsilon\nabla_{\mathbf{n}}v &= r\quad \text{on }\partial\Omega_1\backslash\Gamma, \\
        v&= 0\quad \text{on }\partial\Omega_2\backslash\Gamma.
    \end{split}
\end{align}
$$

Take the integration by parts on each subdomain, we have

$$
\begin{align*}
    \int_{\Omega_1}\beta\nabla v\cdot\nabla \varphi\,dx 
        - \int_{\partial\Omega_1}\beta\nabla_{\mathbf{n}}v\varphi\,ds 
        - \int_{\Omega_1}q(v)\varphi\,dx 
        + \int_{\Gamma}v(\theta\kappa_1\varphi - \beta\nabla_{\mathbf{n}}\varphi)\,ds &= 0,\\
    \int_{\Omega_2}\beta\nabla v\cdot\nabla \varphi\,dx 
        + \int_{\partial\Omega_2}\beta\nabla_{\mathbf{n}}v\varphi\,ds 
        - \int_{\Omega_2}q(v)\varphi\,dx 
        + \int_{\Gamma}v(\theta\kappa_1\varphi + \beta\nabla_{\mathbf{n}}\varphi)\,ds &= 0.
\end{align*}
$$

then we have

$$
\begin{align*}
    0&= \int_{\Omega}\beta\nabla v\cdot\nabla\varphi\,dx 
        - \int_{\partial\Omega_1\backslash\Gamma}\beta\nabla_{\mathbf{n}}v\varphi\,ds
        - \int_{\partial\Omega_2\backslash\Gamma}\beta\nabla_{\mathbf{n}}v\varphi\,ds
        - \int_{\Gamma}[\beta\nabla_{\mathbf{n}}v\varphi]\,ds
        - \int_{\Omega}q(v)\varphi\,dx\\
        &\qquad + \theta\int_{\Gamma}\{v\varphi\}\,ds
        - \int_{\Gamma}[v\beta\nabla_{\mathbf{n}}\varphi]\,ds.
\end{align*}
$$

Recall again,

$$
\begin{align*}
    \{uv\} &= \{u\}\{v\} + \kappa_1\kappa_2[u][v] ,\\
     [uv] &= [u]\{v\} + \{u\}[v] - (\kappa_1-\kappa_2)[u][v],
\end{align*}
$$

and expand the expression,

$$
\begin{align*}
    0&= \int_{\Omega}\beta\nabla v\cdot\nabla\varphi\,dx 
        -\int_{\partial\Omega_1\backslash\Gamma}\beta\bar{\varepsilon}(r-v)\varphi\,ds 
        - \int_{\Omega}q(v)\varphi\,dx \\
        &\qquad -\int_{\Gamma}[\beta\nabla_{\mathbf{n}}v]\{\varphi\}\,ds
        - \int_{\Gamma}\{\beta\nabla_{\mathbf{n}}v\}[\varphi]\,ds
        - (\kappa_1-\kappa_2)\int_{\Gamma}[\beta\nabla_{\mathbf{n}}v][\varphi]\,ds\\
        &\qquad +\theta\int_{\Gamma}\{v\}\{\varphi\}\,ds
        + \theta\kappa_1\kappa_2\int_{\Gamma}[v][\varphi]\,ds\\
        &\qquad - \int_{\Gamma}[v]\{\beta\nabla_{\mathbf{n}}\varphi\}\,ds
        - \int_{\Gamma}\{v\}[\beta\nabla_{\mathbf{n}}\varphi]\,ds
        - (\kappa_1-\kappa_2)\int_{\Gamma}[v][\beta\nabla_{\mathbf{n}}\varphi]\,ds.
\end{align*}
$$

### So sánh với XFEM

Trong thesis của **El-Otmany2015** có 1 đoạn so sánh thế này

> Dans la suite nous utiliserons la méthode NXFEM. Cette méthode utilise des fonctions de base d’éléments ﬁnis classiques pour enrichir l’espace d’approximation et traite les conditions au bord de façon faible dans la formulation variationnelle. Cependant, la méthode XFEM utilise comme fonctions de base des fonctions singulières (de Heaviside) et des degrés de liberté supplémentaires. L’implémentation de NXFEM est ainsi plus simple que celle de XFEM.

Tuy nhiên hai cái phương pháp này có liên quan với nhau, xem bài báo **Areias2006** để biết thêm chi tiết. Mình cũng đã có một bài tính toán các hệ số của sự liên quan này trong quyển note số 2.

## NXFEM của Arnold

- Được miêu tả khá chi tiết tại **Lehrenfeld2012**, thật ra là của ông Arnold, có thể xem trường hợp 1 chiều tại **ArnoldBook** (section 7.9.2).
- Có chứng minh cái basis function mới là stability tại **Arnold2008**.
- Những basis với very small support có thể bị xóa bỏ, ý tưởng này xem ở **Arnold2008** (mục 3).
- Trong **Lehrenfeld2014**, ông ta cũng thừa nhận rằng cái basis functions (trong đó gọi là characterization) là khác so với cái của Hansbo. Có thể dựa vào các chứng minh và kiểm định stability của cái functions này để kiểm định lại cái ý tưởng của Hansbo.
- Cái khác giữa TRUNG HIEU và Hansbo nằm ở điều kiện $[\beta u]\vert_{\Gamma}=0$. Hansbo thì $\beta_1=\beta_2$ trong khi TRUNG HIEU thì $\beta_1 \ne \beta_2$

## So sánh XFEM và IIM

Bổ sung sau