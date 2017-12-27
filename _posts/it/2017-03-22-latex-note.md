---
title: LaTeX notes
categories: it
tags: ["latex"]
maths: 1
toc: 1
date: 2017-12-27
---

This is the list of quick latex notes before I write clearly and completely on the site [Math2IT](http://math2it.com). 

## LaTeX errors

*Underfull \hbox (badness 10000) message* (xem thêm [ở đây](https://tex.stackexchange.com/questions/199635/underfull-hbox-badness-10000-message))

Cách giải quyết đơn giản chỉ cần xóa đi `\\` ở cuối mỗi hàng được báo lỗi.

## Maths LaTeX editors

Me and some of my friends (work on Maths) have a need that we want to type equations faster in the form of LaTeX codes. We wanna type WYSWYG the maths equations and some software will automatically change them to Latex codes. We also want the vice versa. In this post, I have found some apps which are available on all operator systems.

- **On Mac** : [Latexit ](https://pierre.chachatelier.fr/latexit/latexit-downloads.php?lang=en)(free)
- **On Windows** : [MathType ](http://www.dessci.com/en/products/mathtype/)(paid), [equalx ](http://equalx.sourceforge.net/)(free),
- **On Linux** : [equalx ](http://equalx.sourceforge.net/)(free),
- **Online** : [simple](http://www.codecogs.com/latex/eqneditor.php), [hostmath](http://www.hostmath.com/),

This list is automatically updated under my personal experience. If you have some better apps, don’t hestitate to comment in the form below this post, thanks.

## Special characters

Phân số đặc biệt: `\sfrac{1}{2}` , phải dùng gói `xfrac`.

## Bibliography

### Biber in Latex to make bibliography

Before doing that, you need to change bibtex.exe into biber.exe before compiling. 

- In **texmaker** : **Options** > **Configure texmaker** > **Commands** > **Bib(la)tex** > change `bibtex` to `biber`
- In **WinEdt** : **Options** > **Execution modes** > **Bibtex** > Executable field, fill the path to **biber.exe** (usually, it locates at `C:\texlive\2016\bib\win32\biber.exe`)

``` latex
\usepackage[
    backend=biber,
    style=authoryear,
    natbib=true,
    url=true,
    doi=true,
    eprint=false
]{biblatex}

\addbibresource{myref.bib}

\printbibliography
```

Compile with `PDFLarex` > `Bibtex` > `PDFLatex` > `View PDF`

If you want your bibliography showed in the same page with other fields on your document, use following lines

``` latex
\begingroup
\let\clearpage\relax
\printbibliography
\endgroup
```

### Add link into bibtex reference

Use biber/bibtex to make a bibliography as usual, just add this line before `\begin{codument}`

``` latex
\usepackage[backref=true]{hyperref}
```

## Tables and Figures

### Change caption's position of table in latex

If you want caption appears above the table (but it's in center), put these lines before `\begin{document}`

``` latex
\usepackage{floatrow}
\floatsetup[table]{capposition=top}
```

If you want caption locates above and lest, use the following lines instead (also before `\begin{document}`)

``` latex
\usepackage{caption}
\captionsetup[table]{
  position=above,
  justification=raggedright,
  %labelsep=newline, % <<< label and text on different lines
  singlelinecheck=false
}
```

NOTE that, you need to put `\label{}` before `\tabular`, for example

``` latex
\begin{table}[!htp]
    \caption{...}
    \label{bang1}
	\centering
    \begin{tabular}{|l|c|r|}
    table's content
    \end{tabular}
\end{table
```

### Continuous numbering (without per chapter) for figures and tables

Use below before `\begin{document}`

``` latex
\usepackage{chngcntr}
\counterwithout{figure}{chapter} % for figures
\counterwithout{table}{chapter} % for tables
```

If you want to number per-section figure in the `article` class

``` latex
\usepackage{chngcntr}
\counterwithin{figure}{section}
```

For equations (no matter what you use `\begin{equation}` or `\begin{align}`), just use

``` latex
\usepackage{chngcntr}
\counterwithin{equation}{chapter}
```

Keep in mind that, you can number the equation per section in the `article` class the same way you do with figure or table.

You can also use it for `footnote`, theorem environment also.

Especially, you can apply this trick to the numbering of the chapter.

``` latex
\usepackage{chngcntr}
\counterwithout{section}{chapter}
\counterwithin{chapter}{part}
```

Just play with them and read more on the [package document](http://distrib-coffee.ipsl.jussieu.fr/pub/mirrors/ctan/macros/latex/contrib/chngcntr/chngcntr.pdf).

## Tikz & vẽ vời

Đoạn code cho 1 hình gọn nhẹ

``` latex
\documentclass[tikz]{standalone}
\usepackage{tikz}
\begin{document}

\begin{tikzpicture}
	% code hình vẽ
\end{tikzpicture}

\end{document}
```

**Đoạn thẳng** từ `(x1,y1)` đến `(x2,y2)`

``` latex
\draw (x1,y1) --  (x2,y2); % chỉ vẽ đoạn
\draw[->] (x1,y1) --  (x2,y2); % thêm mũi tên
\draw (x1,y1) --  (x2,y2) node[position] {text} ; % thêm text
% position: above, below, left, right, above left,...
\draw[attribute] (x1,y1) --  (x2,y2); % tùy chỉnh thuộc tính đoạn
% attribute: thick/very thick (độ đậm), blue (màu), dash,...
```

**Tam giác hay polygon** : vẽ nối nhiều đoạn lại

``` latex
\draw (x1,y1) --  (x2,y2) -- (x3,y3) ;
```

**Tô màu** polygon

```latex
\draw[fill=blue, opacity=0.8] (x1,y1) --  (x2,y2) -- (x3,y3) -- (x1,y1) ;
% nếu dùng opacity thì nó sẽ làm mờ luôn cái màu đường
% dùng fill=blue!40 sẽ không làm mờ cái màu đường
```

**Đặt text riêng**

```latex
\node at (x1,y1) {text};
\node[position,color] at (x1,y1) {text}; % thêm vị trí và màu
```

Vẽ **parabol** $y=x^2$

```latex
\draw (0,0) parabola (4,4); % từ điểm này đến điểm kia của parabola
```

Vẽ **đường cong** nhờ vào các control points

```latex
\draw (0,0) .. controls (0,4) and (4,0) .. (4,4); % (0,4) và (4,0) giống như các nút nam châm hút đường đó về hướng đó
```

Vẽ **đường tròn**

```latex
\draw (2,2) circle (3cm);
```

Vẽ **ellipse**

```latex
\draw (2,2) ellipse (3cm and 1cm); % dài 3cm, cao 1cm, tâm (2,2)
```

Vẽ **arc**

```latex
\draw (3,0) arc (0:75:3cm); % đường bắt đầu tại (3,0), góc xuất phát là 0 tại 1 tâm (x0,y0) nào đó của đường tròn, góc kết thúc là 75, bán kính của đường tròn này là 3cm.
```

Vẽ **grid**

``` latex
\draw[step=1cm,gray,very thin] (-2,-2) grid (6,6); % điểm dưới trái đến điểm trên phái (hình vuông)
\draw[step=1cm,gray,very thin] (-1.9,-1.9) grid (5.9,5.9); % bỏ đi cái viền xung quanh grid
```

Vẽ **hệ trục tọa độ (axes)**

```latex
\draw[thick,->] (0,0) -- (4.5,0) node[anchor=north west] {x}; % lấy mốc tây bắc (chữ sẽ ở đông nam)
\draw[thick,->] (0,0) -- (0,4.5) node[anchor=south east] {y};
% thêm node và số
\foreach \x in {0,1,2,3,4}
    \draw (\x cm,1pt) -- (\x cm,-1pt) node[anchor=north] {$\x$};
\foreach \y in {0,1,2,3,4}
    \draw (1pt,\y cm) -- (-1pt,\y cm) node[anchor=east] {$\y$};
```

### Matlab và tikz

Sau khi vẽ bằng matlab và xuất ra file tex.

- Nếu muốn chỉnh độ width/height thì bỏ đi cái height, width chỉnh theo `\textwidth`.
- Nếu muốn bỏ đi cái viền xung quanh màu đỏ: comment dòng `scale only axis`
- Nếu muốn bỏ đi tọa độ và axis, thêm dòng sau vào sau
  ```
  \begin{axis}[axis lines=none]
  ```
- Tọa độ được ghi là `(axis cs:x,y)`


