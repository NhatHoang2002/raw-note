---
title: Level Set Method
categories: [phd,maths]
tags: [phd,numerical analysis]
toc: 1
maths: 1
date: 2018-10-07
---

## General

Trong note này sẽ bao gồm luôn mục **coding** thay cho note [coding-note](/coding-note-1)

- **Giải level set** phải thông qua 2 bước quan trọng
  - Dùng SDFEM để giải tìm phi (7.2 Arnold book). Dùng Method of lines (giải thích về method này trong knabner book).
  - Dùng FMM để reinitialization. $\Rightarrow$ dùng `mshdist` của thầy Pascal Frey

- **Sign distance function**:
  $$
  d(x_0,\Gamma_h) := \min_{x\in \Gamma_h} d(x_0,x).
  $$


### <new /> Using FreeFem++

We can consider to use `convect` in FreeFem++. It used Galerkin Characteristic FEM (cf. *convegence convect (galerkin characteristic fem)) Pironneau.pdf*)

- Why in the past, we cannot use `convect`?

Thi paper said that:

- There are many methods to solve convection-diffusion equations approximated by the FEM: SUPG, its Galerkin Least Square variant, Deconninck's PSI method, Discontinuous-Galerkin or Galerkin-characteristics.
- This page doesn't prove for any case, he said that in practice, the Characteristics is very good. "*Even if it is fundamental, the problem is sufficiently important to be dealt with and so the object of this paper is to show -with proofs- that there is at least one case*"

**Remarks** (18/9/18)

- CFL ok
- CR of $\Vert \phi - \phi^N_h\Vert_{L^2(\Omega)}$ is 1????
- The figures are not so good at $t=N$ but they are better if the mesh is finer



### Signed distance function

- Tại sao nếu là đường tròn thì $\phi$ có dạng là 

    $$
    \phi(x,y) = \sqrt{(x-x_0)^2 + (y-y_0)^2} - r_0
    $$

	thay vì dạng 

    $$
    \phi(x,y) = (x-x_0)^2+(y-y_0)^2-r_0^2
    $$

	trong đó $I(x\_0,y\_0)$ là tâm của đường tròn, còn $r\_0$ là bán kính?

	Lý do là bởi phù hợp với **signed distance function**. Nếu từ một điểm không nằm trên đường tròn $M(x,y)$, khi ấy khoảng cách từ $M$ đến đường tròn chính là

    $$
    d(M,C) = d(M,I)-r_0
    $$

	đây cũng chính là công thức có căn.

- Test coi mshdist hoạt động tốt không có thể tính $\Vert \nabla \phi \Vert$ xem có bằng 1 hay không! $\Rightarrow$ **Kết quả**: nếu dt quá lớn, u quá lớn thì cái $\phi$ xa rời cái signed distance function



## Coding note

- File **main_levelset_simple** dùng để test.
  - Dùng *model_levelset_vortex* thì ra **đẹp** nếu **không dùng SUPG** và **không dùng FMM** $\Rightarrow$ Kỳ lạ!!!
- Giải tìm trên standard FEM chứ không phải $V_h^{\Gamma}$ 
- **Note lý thuyết** (variation form) xem file *hw_levelset_13718.pdf*



## Test case

- *implementation standard level set method - niklas johansson.pdf*  (4.1. Vortex): có 2 ví dụ rất rõ ràng, nên áp dụng cái models trong đây để test coi code có chạy ổn không.
  - Ổng dùng grid hình vuông.
  - **Không** dùng lượng stabilization như SUPG mà chỉ dùng redistancing.
  - Ổng cũng có nói đến cái việc dùng reinitialization sẽ ra xấu nhưng với mesh đẹp hơn thì sẽ tốt hơn (nhưng ko hoàn hảo bằng wtSUPG và wtFMM). Ổng cũng nói là dùng FMM ở mỗi time step sẽ xấu hơn là dùng 4 loop 1 lần hoặc nhiều hơn.
- *Arnold book* (7.5): trong đây ổng dùng SUPG để stabilizise, có thể áp dụng model trong đây để xem **lý do vì sao SUPG trong code của mình không hoạt động**
  - Ổng cũng có nói là **không hiểu sao** không dùng SUPG gì cả thì lại ra đẹp.
- 3.5.5 trong thesis của Christoph WINKELMANN.
- Thesis của Gross Sven mục 10.1



## Toolbox

Quyết định dùng toolbox của Pascal Frey. Ngoài ra còn có các toolbox khác như sau

- **Pascal Frey [mshdist](https://github.com/ISCDtoolbox/Mshdist)**
  - Bài báo *computation signed distance function - charles - pascal frey 2012.pdf*
  - triangle đủ các loại luôn.
  - Viết trên C++
  - Đã test thành công với ví dụ `phi=phi.^3`
  - Must run on Linux or Mac (cannot install Windows)
  - Có thể plot file .sol bằng phần mềm [medit](/coding-note-1#medit) (phần mềm này không phải là cái medit editor trong linux)

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
How to install on linux
</div>
<div class="collapsible-body" markdown="1">

- Install Commons

	~~~ bash
git clone https://github.com/ISCDtoolbox/Commons.git
cd Commons
mkdir build
cd build
sudo apt-get install cmake
sudo apt-get update
sudo apt-get install build-essential manpages-dev
cmake ..
make
make install
	~~~

- Install `mshdist`

	~~~ bash
git clone https://github.com/ISCDtoolbox/MshDist.git
cd MshDist
mkdir build
cd build
cmake ..
make
make install
	~~~

</div>
</li>
</ul>

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Others
</div>
<div class="collapsible-body" markdown="1">
- [Toolbox Fast Marching](https://fr.mathworks.com/matlabcentral/fileexchange/6110-toolbox-fast-marching) (2009, mathwork) - **Gabriel Peyre**. $\Rightarrow$ Xem thêm [note coding](/coding-note-1).
  - Cái này rất cũ, không biết áp dụng vào grid của mình như thế nào!

  - [Link trên github](https://github.com/gpeyre/matlab-toolboxes) (đã không còn update, 2013) --> [numerical tours](http://www.numerical-tours.com/matlab/)

  - Nay ổng dùng trang Numerical tours: [FMM 2D](http://www.numerical-tours.com/matlab/fastmarching_1_2d/)

  - Level set + fast marching: [active contour using level sets](http://nbviewer.jupyter.org/github/gpeyre/numerical-tours/blob/master/matlab/segmentation_3_snakes_levelset.ipynb)

  - get some errors (already ask him, waiting)

  - **How to install?**

    - C++ compiler with matlab (xem bên dưới)

    - Sau đó cd đến thư mục chứa file **mex** (nếu gặp lỗi **You should compile the mex file, see compile\_mex.m**)

      ```matlab
      compile_mex
      ```
    - Some lỗi (nếu có)

      - Thật ra máy anh Việt cài Visual Studio trước khi cài matlab và hoạt động tốt. Có thể tải bản miễn phí [Visual Studio Express](https://visualstudio.microsoft.com/vs/express/) về xài.
      - Xem [System requirements and Supported Compilers](https://fr.mathworks.com/support/sysreq/previous_releases.html) cho Matlab các phiên bản.
      - See [this](https://www-m3.ma.tum.de/foswiki/pub/M3/MeshFree1415/WebHome/matlabgnucompiler.pdf), it's useful.

  - Thật ra code của ông này (theo [bài hướng dẫn này](http://nbviewer.jupyter.org/github/gpeyre/numerical-tours/blob/master/matlab/segmentation_3_snakes_levelset.ipynb)) chỉ dành cho grid mesh **hình vuông**, trong đó X, Y đều có size nxn (mỗi giá trị tương ứng của X và Y là coordinate của một nodes). Trong khi cái của mình x, y là tập hợp của 1 loạt các nodes (nên chúng chỉ có size 1xnNodes thôi). Nếu là mesh tam giác bất kỳ thì không chuyển về giống dạng meshgrid được!!!!

  - cái `vertex` và `faces` của ổng rất giống với cái `points` và `triangles` của mình ([code test](http://nbviewer.jupyter.org/github/gpeyre/numerical-tours/blob/master/matlab/meshproc_1_basics_2d.ipynb)).

- **[DROPS](https://www.igpm.rwth-aachen.de/forschung/drops/download)** library by **Arnold group**.
  - the best choice (if available)
  - cannot download (waiting for their answer)! (Cannot follows 10.1 guides because it's out-of-date!)

- **C++ compiler with Matlab**: 

  - nên cài **[TDM-GCC](https://sourceforge.net/projects/tdm-gcc/files/TDM-GCC Installer/)** thay vì (hoặc cùng với) MinGW.

  - Sau đó chỉ cho matlab biết đường dẫn

    ~~~ matlab
    setenv('MW_MINGW64_LOC','C:\TDM-GCC-64')
    ~~~

</div>
</li>
</ul>



## Documentation

- <new /> *adaptive techniques level set - osher - losasso - fedkiw.pdf* describes the history of level set methods + adaptive. It's good for understand *in-one-place* all things.

- Mình note **workflow** khá ổn: *hw level set workflow 6-2018.pdf*

- Chứng minh zero level solution of phương trình Hyperbolic (Cauchy problem) describes the position of the interface. $\Rightarrow$ xem Exercise 4.1 của **Lehrenfeld NOTE 2015.pdf**, có solution luôn!

- **Narrow node**s: Chopp 1993 (chưa rõ tên bài báo)
  - Cái giải local này có thể xem *pde based fast local level set method - peng 99.pdf*, cái này tối ưu hơn cả cái của Sethian (theo như nó nói). Cái này họ xét nodes trong 1 tube cụ thể chứ ko phải trên toàn domain.

- If a time step causes the change in distance of a pixel to be greater than the grid size, will make the level set unstable, it is necessary to make a **prediction on the maximum time step** (*implement level set narrow band - larsen 2005.pdf*)

- $\mathbf{u}$ trong $\partial_t \varphi + \mathbf{u}\cdot\nabla\varphi=0$ có được định nghĩa trên toàn miền hay không? Có bài báo nào chỉ bó hẹp ở 1 subdomain như vấn đề của mình hay không?

  - Thèse của chị Cúc $\Rightarrow$ toàn miền.
  - Bài báo của Sethian trang 12 **Sethian2003** , thì $u$ trên từng miền có giá trị khác nhau và được tính theo các phương trình khác nhau.
  - Thèse của Trung Hiếu lấy từ phương trình N-S nên $u$ cũng tính trên toàn miền.

- Tại sao cần $\Vert \nabla \phi \Vert =1$? và tại sao cần level set function là signed distance function? 
	- Có thể xem mục 9.3 thesis Eva Loch.
	- 1.2.3 *Christoph WINKELMANN EPFL THESIS 2007*


### Ý tưởng viết level set

- có thể bắt chước của chị Cúc. Trong thèse, chương 3.1, chương 1.3 cũng có nói tí tí, giới thiệu ở 2.2.
- Giải thích từ ý tưởng $\phi(x,t)=0$ đến phương trình level set: 2.2 jury thesis.
- [Trang này](https://profs.etsmtl.ca/hlombaert/levelset/) giải thích ý tưởng về level set khá hay.
- Ý tưởng về (signed) distance function được giới thiệu trong bài báo *sethian osher 1988*
- Mục 2.2.1 Gross thesis



### SUPG method

- Có thể đọc trong Arnold Book (7.2 and 7.5.1), trong đó $\delta$ có dạng

  $$
  \delta_K = SD\dfrac{h}{\max \{ \Vert u \Vert_{L^{\infty}(K)}, tol/h \}}
  $$

  Trong đó, $SD$ là scale factor, $tol/h$ is introduced to avoid dividing by a number close to zero (Loch thesis p.46)

- Page 203 Arnold Book, có nói nếu velocity u phụ thuộc t thì biểu thức SUPG khác cái mà mình áp dụng hổm rài, cần coi kỹ cái này! $\Rightarrow$ **coi (7.17)**

- Tuy nhiên cái ví dụ trong bài bào của lại có $\mathbf{u}=0$ và theo Arnold (p.221), ổng nói rằng *Due to $u=0$ on $\partial\Omega$ we do not need boundary conditions for $\phi$.*



### Boundary condition

- Có thể xem mục 3.3 trong thesis Eva Loch.

- Remark 7.5.1 Arnold Book có nói về cách áp dụng velo $u\ne 0$ trên biên. 

- Biên trong sách toàn là 

  $$
  \partial\Omega_{in}:= \{ x\in \partial \Omega: u\cdot n<0 \}
  $$

  Trong đó $n$ là **outward unit normal vector** to $\partial\Omega$ (cái này nói ở trang 219)

- Lưu ý là nếu $u\in t$ thì ta phải xét $V_h(\phi_D)$ như trang 202.

- **Không cần xét boundary condition**: 
  - *Gross Sven thesis*: không đề cập đến BC cho level set equation. Tác giả bài báo này xét trên P2.

  - *Trung Hieu thesis* 2.3, *thesis của chị Cúc* 3.1 : Khi level set function advance with time, nó không còn là signed-distance function như thời điểm ban đầu nữa ($\Vert{\nabla\varphi}\Vert \ne 1$). Điều này dẫn đến cần phải thay thế level set function bởi một hàm gần đúng khác sao cho cùng zero level set. Do đó, term $u\cdot\nabla \varphi$ chỉ được xét trong một giai đoạn thời gian rất ngắn. Vì thế, chúng ta có thể xét level set equation mà không có boundary condition.

    - **Giải thích thử** : Vẽ cái hình $\varphi^n, \varphi^{n+1}$ ra, cái mở rộng từ cái trước sang cái sau phụ thuộc vào $u\cdot\nabla\varphi$. Nếu $\Delta T$ mà lớn quá thì cái $\varphi^{n+1}$ sẽ lớn hơn rất nhiều so với cái $\varphi^n$, đều này dẫn tới cái $\varphi$ vừa tìm được nó sẽ rất khác so với cái signed distance ban đầu. Do đó việc Reinitialization sẽ khó hơn nữa!!!

      $\Rightarrow$ Cũng có thể xem trang 192 sách của **ArnoldBook** có nói về vấn đề này

  - Nếu muốn xét boundary condition thì cũng khó nếu đã biết uex và velocity u, bởi vì nếu muốn dùng Dirichlet $u=u\_{ex}$ thì ta cần giải $\phi^{n+1}$, tức phải biết giá trị của nó tại thời điển $n+1$ nhưng không thể biết được.

  $$
  \phi^{n+1} + \dfrac{\tau}{2}\beta\cdot\nabla \phi^{n+1} + \dfrac{\tau}{2}\beta\cdot\nabla \phi^n - \phi^n =0.
  $$

  $\Rightarrow$ **Chưa chính xác lắm!** Trong Arnold Book, ổng cũng có nói vấn đề về Dirichlet BC này ở mục Remark 7.5.1 (p. 221)

  - <update /> In the note of Chopp, section 5.2.3, he also talks about the "not-so-useful" of boundary condition. 




### Errors

- As the objective of the level set equation is to capture the moving interface, the error between the exact interface $\Gamma$ and the approximate interface $\Gamma\_h$ , i.e. the difference between the zero level of the exact solution φ of the level set equation and the zero level of the discretized level set function $\phi\_h$ , is of major interest. This error can be measured in the L2-norm by integrating the squared distance function $d: \Omega \to \mathbb{R}$} to the interface $\Gamma$ over $\Gamma\_h$ ... page 13 Eva Loch thesis.
- Trang 219 Arnold Book có nói về error và bậc có được, có thể áp dụng để check xem cái của mình ra tốt không.
- If SUPG then (Arnold Book page 219) <mark>only for SUPG (not FMM)</mark>

    $$
    \Vert \phi_h^N - \phi^N \Vert_{L^2(\Omega)} \le CT(h^{k+\frac{1}{2}} + \Delta t^2)
    $$

- Volume error estimate (Arnold Book page 219)

    $$
    \begin{align}
    \vert V_1(\phi_h^N) - V_1\vert &\le ch^k\\
    V_1(T) &= V_1(0) = V_1 \\
    V_1(\phi^N_h) &= \int_{\Omega^N_{1,h}} 1 d x \\
    \Omega_{1,h}^N &:= \{ x\in \Omega: \phi^N_h(x) <0 \}.
    \end{align}
    $$

    This estimate shows that volume error can be controlled by reducing the mesh size.

- If $u$ depends on time, an error estimate for a problem like (5.15) in my thesis <mark>is not known yet!</mark> (Arnold Book, p. 204). But we have estimation (7.19) if $u$ is time-independent.
- The estimate between $\phi_h^N$ and $\phi$ is only used for the case of using SUPG (not FMM). Because if we use FMM, the interface moves, so on the whole domain, $\phi_h$ changes too much. However, its zero-level seems to be better. That's why we need to consider different estimates like in (7.50) at page 227.

- **<mark>Importance!!!!</mark>**: Note that $\Vert u-u_h\Vert$ is different from $\Vert I_hu-u_h\Vert$. And we have the **interpolant error estimate** (Lemma 5.2.2 FEM note of Pascal Frey)

    <div class="p-mark">
    $$
    \begin{align}
    \Vert I_h u - u\Vert_{H^1(\Omega)} &\le Ch^2 \Vert u''\Vert_{L^2(\Omega)} \\
    \Vert (I_hu)' - u' \Vert_{L^2(\Omega)} &\le Ch \Vert u''\Vert_{L^2(\Omega)}
    \end{align}
    $$
    </div>

### Conservation of mass

- *level set 1996 - Hou et Chang*
- For incompressible flow, the total mass is conserved in time, however the numerical discretization of the level set formulation does not preserve this property in general. Even with some reinitialization procedures, it has been found that a cosiderable amount of total mass is lost in time. Tất cả cái này được nhắc đến trong **Hou1996** (trang 7).
- **Trung Hieu thesis 7.2.2** trang 83 có nói về Mass conservation: *<mark>The loss of mass by discretizations of the level set function can be reduced if the grid is refined</mark>* $\Rightarrow$ dùng pp trong DROPS và **thesis của Gross Sven** (8.2). *We use another method, in which the level set method is shifted over a distance  $\delta$ in the normal direction, such that the volumes of both phases remain unchanged.*
- **Arnold book** (7.4.2) cũng có nói về cái này. *following very simple (but less satisfactory) strategy, which guarantees volume conservation for the level set method* (p.220)



### Reinitialization & Fast Marching Method

- **Idea FMM**
  - Ra một cái $\phi$ mới (sau khi áp dụng cách giải SDFEM): chỉ có zero-level set thôi, chưa có sign distance function. Áp dụng FMM để tìm một cái $\tilde{\phi}$ mới có cả 2 tính chất kia.
  - Xem **ý tưởng FMM** trong slide *BEST EXPLAIN fast marching method - Luis Moreno SLIDE 2016.pdf*.
    - Giải thích RẤT HAY và tại sao $T_3$ lại phải được tính theo $T_1,T_2$ có trong *BEST SLIDE fast marching method - Anastasia Dubrovina.pdf*
  - [Trang này](https://math.berkeley.edu/~sethian/2006/Explanations/fast_marching_explain.html) giải thích về FMM khá hay + [video này](https://www.youtube.com/watch?v=Ebi5juth-LE) giải thích ý tưởng FMM (ngôn ngữ lạ + simple problem).
  - [Trang này](https://math.berkeley.edu/~sethian/2006/Explanations/fast_marching_explain.html) cũng nói là FMM chỉ thích hợp nếu có giả sử lực $F$ luôn không đổi dấu, tức interface chỉ "nở ra" hoặc "co lại" trong suốt quá trình mà thôi. Mình nghĩ thêm, thật ra mình áp dụng FMM cho mỗi lần reinitialize nên vấn đề dấu của $F$ này có thể bỏ qua được. **Trang này cũng giải thích khá rõ ý tưởng của FMM**.
  - Giải thích tí *BEST SLIDE fast marching method - Anastasia Dubrovina.pdf*
    - Slide 18: Khi $T\_3 < T\_1$ thì ta phải lấy $T\_3 = \min\{T\_1,T\_2\} + h$ bởi vì $T\_3$ phải đến sau hai thằng kia mà mỗi bước tiến ít nhất phải là $h$.
  - Khi tính **khoảng cách (bằng cách geometry) giữa node và segment $\Gamma_h$** thì không có kéo dài đoạn ra: nếu hình chiếu (đường vuông góc từ node đó đến $\Gamma_h$) nằm ngoài đoạn $\Gamma_h^T$ thì khoảng cách sẽ là tính tới hai điểm đầu mút của đoạn, ngược lại (hình chiếu nằm giữa 2 đầu đoạn) thì sẽ tính là đoạn chiếu. cái này nói trong Arnold book p.214.
- Giải thích tại sao cần $\Vert \nabla\phi\Vert = 1$: 9.3 thesis Eva Loch, trong đó có PDE way (9.3.1), FMM way.
- **Reinitialization**: phải dùng **Fast Marching Method**! $\Rightarrow$ Dùng toolbox của Pascal Frey (xem ở trên)
- **Tóm lại**: có 2 cách reinitialization
  - Cách của Arnold
  - Cách của chị Cúc (p.100 thesis), khác ở chỗ tìm $\sum_{i=1}^3\vert \phi\_i \nabla \lambda_i\vert^2=1$ cho từng element.
- Mục FMM 9.3.2 của Eva Loch thesis khá giống với Arnold.
- **Tính sign distance trực tiếp**: This brute force approach has the advantage that it does not move the interface up to the numerical accuracy of the interpolation scheme. The disadvantage is its high cost and the likelihood of introducing some spurious irregularity into the data, making differentiated quantities such as curvature behave very badly. (*pde based fast local level set method - peng 99.pdf*)
- **Tại sao lại phải chia ra thành 3 nhóm nodes?** (như giải thích ở [wiki](https://en.wikipedia.org/wiki/Fast_marching_method#Algorithm))
  - 3 nhóm nodes đó là: Accepted, Considered và Far.
  - Ta không thể tính trực tiếp khoảng cách từ nodes đến $\Gamma_h$ được vì có nhiều đoạn, ta không biết phải tính khoảng cách từ node đó đến đoạn trong element nào? (Theo như Arnold Book, công thức (7.35) thì lấy min của tất cả các cái)
  - Theo như thuật toán thì có vẻ khoản cách từ các nodes *Considered* sẽ được tính thông qua các nodes *Accepted* (why?)

- **Problem**: If we apply FMM (or some other reinitialization methods) many times, the <mark>interface will move.</mark>
    - *implementation standard level set method - niklas johansson.pdf* (Section 3.2.3)
    - *computation signed distance function - charles - pascal frey 2012.pdf* (Section 6)
        - They used an adaptation process.
    - *Eva Loch thesis* (p. 27 and Section 9.3)
        - She said that the re-initialization of $\phi$ wish to be a zero-level set + signed distance function but the former is hard to be obtained in practice.
        - She didn't say about the solution!
    - *Lehrenfeld NOTE* (at the end of p. 64): still challenging!
    - *Gross thesis* (p. 142)
        - "A simple variant of the Fast Marching method (cf. [KS98, Set96a]) turned out to perform much better in our numerical simulations."

## Mesh adaptation

A problem with performance if we working on a very-fined mesh. We just want to focus on the area a round the interface but we finer the whole domain. An idea is to adapt the mesh only for the area around the interface. But how?

- **Keyword**: adaptation, refinement mesh.
- **Tools**
    - Matlab ref: `refinemesh` ([cf](https://fr.mathworks.com/help/pde/ug/refinemesh.html))
    - ISCD toolbox / [AdapTools](https://github.com/ISCDtoolbox/AdaptTools) but how to use it?

- It's mentioned at Section 9.3 of Eva Loch's thesis: why we need Re-initialization.

- <new /> **Adaptmesh** in freefem++ by Hecht

