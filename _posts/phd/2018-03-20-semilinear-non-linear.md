---
layout: post
title: Semilinear, nonlinear problem
categories: maths
tags: ["semilinear","non linear"]
maths: 1
toc: 1
---

## Other works

- Có nhắc đến trong *fixed point semilinear Manole Mihaela THESIS.pdf* (xem trang 21).
- Xem thêm *intro semilinear elliptic - thierry cazenave.pdf*
- Xem thêm note [article 1](/article-1) cho vấn đề **tồn tại nghiệm** của semilinear.

## Phân loại semilinear, nonlinear

[[source]](http://wiki.math.toronto.edu/DispersiveWiki/index.php/Semilinear) A **semilinear** equation is a PDE of the form
$$Lu = F(u)$$
where $L$ is a linear operator and $F$ is a nonlinear operator which does not involve any derivatives of $u$.

A **semilinear-with-derivatives** equation is a PDE of the form
$$L u = F(u, Du, \ldots, D^k u)$$
where $L$ is a linear operator, $F$ is a nonlinear function of the first few derivatives $u, Du, \ldots, D^k u$, with $k$ strictly less than the order of $L$.

Semilinear-with-derivatives equations are more nonlinear than semilinear equations, but are less nonlinear than quasilinear or fully nonlinear equations.

$\Rightarrow$ Phân loại + ví dụ ngắn gọn dễ hiểu về các cái nonlinear này, có thể xem [ở đây.](http://math.stackexchange.com/questions/388389/simple-pde-classification-question)


## System of semilinear equations

Đã được chứng minh tồn tại và duy nhất ở các dạng sau (của Chen, *semilinear elliptic system - chen.pdf*)

$$
\begin{align*}
\begin{cases}
-\Delta u &=\lambda p(x)f_1(x) \quad (\Omega)\\
-\Delta v &= \lambda q(x) g_1(x) \quad (\Omega)\\
u=v&=0 \quad (\partial\Omega)
\end{cases}
\end{align*}
$$

Trong bài báo trên cũng có nói một số bài báo với các pp giải khác nhau cho loại phương trình sau

$$
\begin{align*}
\begin{cases}
-\Delta u &=\lambda f(v) \quad (\Omega)\\
-\Delta v &= \lambda g(u) \quad (\Omega)\\
u=v&=0 \quad (\partial\Omega)
\end{cases}
\end{align*}
$$

## Semilinear elliptic inteface problem

Của Sinha (*semilinear interface elliptic - parabolic sinha deka 2009.pdf*) 

$$
\begin{align*}
\begin{cases}
-\nabla\cdot(\beta\nabla u) + u &= f(u) \quad (\Omega)\\
u&=0 \quad (\partial\Omega)\\
[u]=[\beta\nabla_n u]&=0 \quad (\Gamma)
\end{cases}
\end{align*}
$$

Trong bài báo này thì tác giả nói là "We assume that the above problem admits a unique solution $u\in X$ . Of course, there are many choices of $f$ that guarantee a solution". Thật ra có nhiều lựa chọn của $f$ được nhắc tới trong *semilinear interface elliptic Deka 2011.pdf*. Mấy cái này chủ yếu chứng minh cho trường hợp $H^1(\Omega)$ và

$$
X = H^1(\Omega) + H^2(\Omega_1) + H^2(\Omega_2)
$$