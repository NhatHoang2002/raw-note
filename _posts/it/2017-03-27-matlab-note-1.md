---
title: Matlab note
categories:
  - it
  - phd
tags: ["matlab"]
maths: 1
toc: 1
---

{% include toc.html %}

## Linh tinh

- Dùng dấu ngoặc kép đôi khi không được, phải dùng dấu ngoặc đơn.
- Change default folder in matlab : **Preferences** > **MATLAB** > **General** > (on the right side) **Initial working folder**.
- Run script nhấn `F5`.
- Một trang giải thích về matlab khá hay : [matlabtips.com](http://www.matlabtips.com)
- Một trang khác về matlab : [tutorialspoint](https://www.tutorialspoint.com/matlab/index.htm)
- Trang matlab online : [đây](https://www.tutorialspoint.com/execute_matlab_online.php)

### Phân biệt add to path và change folder

Khi biên dịch một file script, nếu như file script ấy không nằm trong folder đang mở thì một cửa sổ hiện lên kiêu bạn chọn giữa "Add to path" và "Change folder". Hai cái này khác nhau.

- **Add to path**: sẽ thêm đường dẫn chứa file script vào trong "path" của matlab để lần sau bất kỳ hàm nào nằm trong path ấy đều chạy được mà không bị hỏi. Điều này có nguy hiểm ở 1 chỗ nếu như ta dùng nhiều thư mục khác nhau chứa những file có cùng tên. Khi ta thay đổi 1 trong số chúng mà ko phải tất cả thì khi gọi tên nó ra, xu hướng nó sẽ gọi tên file trong path.
- **Change folder**: cái này mang tính tạm thời, thư mục đang mở ngay lập tức sẽ chuyển về thư mục chứa file script. Khuyên dùng cách này.

Cần để ý thêm, mỗi lần click vào 1 tab file script, phía trên nó sẽ hiển thị đầy đủ đường dẫn đến file nếu như file đó không nằm trong thư mục đang mở. Ngược lại, nó chỉ hiện tên file nếu như file đó nằm trong thư mục đang mở.

## Links

1. FEM with Matlab, many resources from Prof. Shaodeng : [click here](http://math2.uncc.edu/~shaodeng/TEACHING/math5172/2010Spring/announcement.html). FEM with matlab, please see the separated note "fem with matlab.md"
2. Matlab Tutorials : [https://www.tutorialspoint.com/matlab/](https://www.tutorialspoint.com/matlab/) (có try it online bằng octave)


## Notations

See more separate files.

- Colon notation : [here](https://www.tutorialspoint.com/matlab/matlab_colon_notation.htm)

---

tidle (dấu ngã) operator

~~~ matlab
a = true; % a=1
c = ~a; % c=0

a = [0,1,2,0,5,0,0,8,9,0,5,5,6];
b = find(a); % find all nonzero positions
c = find(~a); % find all zero positions
~~~

Nhiếu khi ta muốn bỏ qua một vài arguments nào đó, ta cũng dùng dấu ngã này. Xem thêm [ở đây](https://fr.mathworks.com/help/matlab/matlab_prog/ignore-function-inputs.html?searchHighlight=Ignore%20Function%20Inputs&s_tid=doc_srchtitle).

---

**Dấu ngoặc móc (curly brackets)**

A square bracket creates a vector or matrix, whereas curly brackets creates a [cell array](http://fr.mathworks.com/help/matlab/cell-arrays.html). Cell arrays allow you to store different types of data at each location  e.g. a 10x5 matrix at (1,1), a string array at (1,2), ...

~~~ matlab
x = [1 2 3]; % matrix with values 1, 2, 3
y = {1, 'a', x}; % cell array storing a number, a character, and 1x3 matrix
~~~

## Workspace

- Bình thường thì matlab có 1 cáo workspace chung, tên là *MATLAB base workspace*, có thể xem nó bằng cách dùng command `whos`.
- Matlab function có *function's workspace*.
- Ngoài ra còn có 1 loại workspace là *Global workspace*, có thể gọi nó ra bằng `whos global`.

- `clear abc` breaks the link between the local and global variables, but does not erase the global variable
- `clear global abc` completely erases the variable `abc` from the local and global workspaces

Có thể đọc [bài viết rất dễ hiểu này](http://www.matlabtips.com/variable-scope-memory-spaces-in-matlab/).


## Operators

~~~ matlab
floor(23/5); % returns 4
mod(23,5); % returns 3
~~~

### logical

- or : `a|b` hoặc `or(a,b)`
- and: `a&b` hoặc `and(a,b)`

~~~ matlab
in1 = find((eGP(5,:)==1)|(eGP(5,:)==3))
~~~

### Logical in if, for statement

- and : `&&`
- or : `||`


## Condition

If else elseif

~~~ matlab
if condition
	statement
elseif condition
	statement
else
	statement
end
~~~

for, while

~~~ matlab
for i=1:n
	statement
end

% ---

while condition
	statement
end
~~~

case switch

~~~ matlab
switch variable
	case option
		statement
	case option
		statement
	otherwise
		statement
end
~~~



## Matrix and array

`end` is used as in an indexing expression

~~~ matlab
B = A(end,2:end); % hàng cuối của i, cột thứ 2 tới cuối
~~~

### create a matrix

~~~ matlab
A=[ [1,5];[2,3] ]
X = [1 0 2; 0 1 1; 0 0 4]
~~~

### vector

~~~ matlab
thi = 0:0.5:10; % start:step:end
thi2 = [1;thi(1:end)]; % insert 1 into left of thi
~~~

Vector/array start with index 1.

~~~ matlab
thi(0); % error
thi(1); % first element
~~~

~~~ matlab
y = linspace(x1,x2) %returns a row vector of 100 evenly spaced points between x1 and x2.
y = linspace(x1,x2,n) % with n points
~~~

### rand

~~~ matlab
rand(2,4); % tạo matrix 2x3 với hệ số random
rand(2,4,3); % tạo matrix 2x3x4
rand(2); % tạo matrix 2x2 
~~~

### sparse matrix

~~~ matlab
A = sparse(i,j,s,m,n) % i,j,s have the same lenght, mxn matrix
% i,j are the indices of elements which are different from 0, s is their value
[i,j,s] = A % inverse of sparse function
%% notice that, cái trên sx theo (j,i) chứ ko phải (i,j)
~~~

~~~ matlab
false(m,n) % create a mxn matrix whose all elements are false
~~~

If wanna create a `i,j,s` vector to store a sparse matrix for FEM (**Finite Element Method**), should use with 9 element like that

~~~ matlab
NT = size(elements,1);
i = zeros(9*NT,1); 
% the same for j and s
~~~

It's because each vertex of the triangle has to link to itself and other 2 vertices (in total, it's 3), then $3 \times 3 = 9$.

Note that, if there is the same `i,j`, the `s` will be the sum of themm for example

~~~ matlab
i=[1,1,2,1];
j=[1,2,2,2];
s=[1,3,6,2];
A=sparse(i,j,s,2,2);
% then A will be
% (1,1)		1
% (1,2)		5 % = 3+2
% (2,2)		6 
~~~

Get triplets from sparse matrix, it's also true for full matrix.

~~~ matlab
[i,j,v] = find(A)
[m,n] = size(S)

i=[1 2 3 4]
j=[1 2 3 4]
v=[1 2 3 4]
A=sparse(i,j,v)
[ii,jj,vv]=find(A) % ii,jj,vv are i',j',v'
B=sparse(ii,jj,vv) % B is the same with A
~~~

### accumarray

~~~ matlab
subs = [1; 3; 4; 3; 4]; % must be column-array
val = [101 102 103 104 105]; % column or row array are accepted
A = accumarray(subs,val); %A = [ 101;0;206;208]
%% Since the second and fourth elements of subs are equal to 3, A(3) is the sum of the second and fourth elements of val, that is, A(3) = 102 + 104 = 206. Also, A(2) = 0 because subs does not contain the value 2. Since subs is a vector, the output, A, is also a vector.
max(subs,[],1); % The length of A
~~~

### condition number

Find **Condition number** of matrix in matlab. For sparse matrix, matlab gợi ý dùng `condest` thay vì `cond`. `condest` được hiểu là 1-norm condition number, là condition number estimate thôi, do đó khi tính ra kết quả có thể  khác nhau nhưng không nhiều.

Xem thêm [bài này](http://www.alglib.net/matrixops/rcond.php) để hiểu về estimate of the condition number.

$$
k(A) = \Vert A \Vert . \Vert A^{-1} \Vert, \\
\Vert x \Vert_1 = \sum_{i=1}^N\vert x_i\vert, \quad 
\Vert x\Vert_2 = \sqrt{ \sum_{i=1}^1\vert x_i^2\vert }, \quad 
\Vert x\Vert_{\infty} = \max_i\vert x_i\vert
$$

`rcond` returns an estimate for the reciprocal condition of A in 1-norm. If A is well conditioned, `rcond(A)` is near 1.0. If A is badly conditioned, `rcond(A)` is near 0. Cf[ matlab doc](https://fr.mathworks.com/help/matlab/ref/rcond.html).

~~~ matlab
rcond
~~~

---

**Machine epsilon** `eps` trong matlab xấp xỉ $2\times 10^{-16}$. It roughly means that numbers are stored with about 15-16 digits of precision. If a number is approximately 1, then that means it can be stored with an error of around 10^(-16) or so. If the number is approximately 1000, then it is stored with an error around 10^(-13) or so.

This is a VERY rough, non-technical explanation.

---

Thường người ta test thử với Hilbert matrix để xem thử condition number của nó thế nào. Đây là ma trận ill-conditioned.

$$
H_{{ij}}={\frac  {1}{i+j-1}}.
$$

Trong matlab, có thể thử `hilb(n)`.

### The order operator in the array or matrix

~~~ matlab
a=[1 2 3 4;
   1 2 3 4];
b=[1 2 3 4;
   4 3 2 1];
c(1:4) = dot(a(:,:),b(:,:)); % result c = [5 10 15 20]
~~~

### Positive definite matrix

Một cách để kiểm tra xem matrix có positive definite hay không là chạy `chol(A)`, nếu kết quả ra giống như sau thì nó không có PD.

~~~
Error using chol
Matrix must be positive definite.
~~~

### Tìm kiếm

Tìm phần tử khác không bên trong `A`, 

~~~ matlab
find(A) % returns a vector containing the linear indices of each nonzero element in array A.
find(X,n) %returns the first n indices corresponding to the nonzero elements in X.
% if find nothing, returns empty matrix
~~~

cũng có thể tìm phần tử đầu tiên thỏa đều kiện

~~~ matlab
find(A==5); % the first element in A which is equal to 5
~~~

---

Tìm xem `[x,y]` có nằm trong ma trận `A` hay không, có hai cách, cách `ismember` chậm hơn cái kia tới 5o lần (cf. [here](https://fr.mathworks.com/matlabcentral/answers/7434-find-vector-in-matrix))

~~~ matlab
A = reshape(1:12,6,2) % A sample matrix for demonstration...

% cách 1 : chậm hơn cách 2
I = ismember(A,[4 10],'rows'); 
sum(I); % đếm xem có bao nhiêu lần xuất hiện

J = A(:, 1) == x & A(:, 2) == y;
sum(J);
~~~

Kết quả ở trên `I,J` đều ra một vector logical. Nếu bạn muốn ra chính xác dòng nào của `A` chứa luôn thì có thể thử `strmatch`

~~~ matlab
A = reshape(1:12,6,2) % A sample matrix for demonstration...
x=[4 10];
strmatch(x,A); % ra ngay 4
~~~

Lưu ý là `[x y]` khác với `[y x]`.

### structure variable

Để có thể khai báo biến dạng `s.1, s.2`. Xem thêm [ở đây](https://fr.mathworks.com/help/matlab/ref/struct.html). Ở đây lưu ý cách tạo multiple dimension structure variable. Ví dụ muốn khai báo trước 1 biến structure đa chiều thì làm sao?

~~~ matlab
n=3;
err = struct('L2',cell(n,1),'Vh',cell(n,1));
% Sẽ ra kq nx1 struct array with fields L2, Vh
~~~

Cách trên **dài dòng** và có nhược điểm là phải gõ luôn cái "fields". Cách dưới đây nhanh hơn nhiều

~~~ matlab
s(1:3) = struct();
~~~

Khi khai báo như trên, thì cho `s` vào vòng lặp `for` để nhận giá trị, nó sẽ không bị warning "*The variable s appears to change size on every loop iteration*". Tuy nhiên nó sẽ gặp lỗi nếu mỗi vòng lặp mình cho `s(k)=t` với `t` là 1 biến structure khác.

**Cách hay nhất**, đó là không cần khai báo trước gì cả và trong vòng lặp, ta đi từ N tới 1 chứ không phải từ 1 tới N (ý tưởng [từ đây](https://fr.mathworks.com/matlabcentral/answers/65613-subscripted-assignment-between-dissimilar-structures-thrown-on-empty-struct))

~~~ matlab
% t is a struct var
for i=N:-1:1
  s(i) = t;
end
~~~


### Some operators with array and matrix

Intersection of two vectors

~~~ matlab
C = intersect(A,B); % find the common elements of A and B
[C,ia,ib] = intersect(A,B);  % find the common elements and idx of the first value in each vector
~~~

---

Find the number of elements of A (matrix or array)

~~~ matlab
e = numel(A)
~~~

---

**Tích vô hướng** (dot product) 

~~~ matlab
A = [4 -1 2];
B = [2 -2 -1];
C = dot(A,B); % dot product of two vector
~~~

If `A,B` are two matrices
$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}, \quad B =  \begin{bmatrix} 9 & 8 & 7 \\ 6 & 5 & 4 \\ 3 & 2 & 1 \end{bmatrix}.
$$

~~~ matlab
C = dot(A,B); % dot product wrt each column
C = dot(A,B,2); % dot product wrt each row
~~~

---

Check xem từng phần tử trong A có thuộc B không, nếu có thì thay phần tử đó bằng 1, không thì bằng 0. Kết quả là 1 vector cùng số chiều như A nhưng chỉ chứa 0 hoặc 1.

~~~ matlab
ismember(A,B)
~~~

---

~~~ matlab
unique(array); % give a vector with unique element (không có element trùng) sx tăng dần
% column array
~~~

`unique` có thể dùng để tìm node on boundary

~~~ matlab
rightEdge = [2 4;4 6]
nodesOnBoundary = unique(rightEdge) % [2 4 6]
~~~

---

Tìm kích thước (size) của một vector/matrix

~~~ matlab
size(triangulation) 
% returns 2x1 vector whose 1st element is number of elements, 2nd is number of vertices on each element.

size(matrixA) %return a size of matrix A
size(A,1) % number of lines of matrix A
size(A,2) % number of columns of matrix A
~~~

---

Giá trị lớn nhất, nhỏ nhất

~~~ matlab
b = max(A,[],2)  % is a column vector containing the maximum value of each ROW of A.
c = max(A,[],1)  % is a column vector containing the maximum value of each COLUMN of A.

d = max(A,2) % replace all elements in A less than 2 by 2.
~~~

xem thêm các ví dụ khác về [max](http://www.mathworks.com/help/releases/R2015a/matlab/ref/max.html).

## PDE toolbox

Xem danh sách các câu lệnh trong ứng với pde bằng cách gõ `help pde` hoặc [xem ở đây](https://fr.mathworks.com/help/pde/functionlist.html). Dưới đây là một số câu lệnh đặc biệt

- `pdeent`  Indices of triangles neighboring a given set of triangles. 
- `pdegrad` Compute the gradient of the pde solution.
- `pdeprtni` Interpolate function values to mesh nodes.
- `pdecgrad` Compute the flux of a pde solution.
- `tri2grid` Interpolate from pde triangular mesh to rectangular mesh.
- `pdetrg` Triangle geometry data.
- `geometryFromEdges`
- `pdeBoundaryConditions`

### Mesh

#### Mesh data

Description about PDE mesh data `[p,t,e]` : [here](https://fr.mathworks.com/help/pde/ug/mesh-data.html).

- Cách đặt số của vertices trong `t` là theo chiều ngược chiều kim đồng hồ. Cái này được nói đến trong **LongChen** và khi thực nghiệm cũng thấy thế.
- Cách đặt số của endpoints trong `e` cũng theo chiều ngược chiều kim đồng hồ, phù hợp với thứ tự của vertices trong `t`, cái này là dự đoán.

#### Tạo solution từ mesh nhanh

$$
u(x) = 1+3x+x(2-x)^2
$$

~~~ matlab
mesh = 0 : h : 2; %% Spatial mesh
ux = 1 + 3 .* mesh + mesh .* (2 - mesh) .^ 2; 
% phải dùng .* vì đây là nhân từng hạng tử bên trong
~~~

#### meshgrid

~~~ matlab
[X,Y] = meshgrid(1:3,10:14); % create a grid with x in 1:3, y in 10:14
[X,Y] = meshgrid(1:3,10:14);
[X,Y] = meshgrid(1:3); % square grid

%% usage
Z = X .* exp(-X.^2 - Y.^2);
surf(X,Y,Z) % plot surface of Z
~~~

#### Create a mesh from geometry shape

~~~ matlab
% rectangle
xDomVal = [0 2 2 0]; % x values of points constructing Omega
yDomVal = [0 0 1 1]; % corresponding y value
RectDom = [3,4,xDomVal,yDomVal]'; % rectangular domain "3" with "4" sides
GeoDom = decsg(RectDom);

% circle
center = [0,0]; % coordinate of a center of circle
radius = 1; % radius of circle
CirDom = [1,center,radius]'; % "1" indicates "circle"
GeoDom = decsg(CirDom);

[points,edges,triangles] = initmesh(GeoDom,'hmax',hEdgeMax);
~~~

`initmesh` uses Delaunay triangulation algorithm.

#### Create a regular mesh on matlab 
(các tam giác đều nhau trên hình chữ nhật)

~~~ matlab
xDomVal = [0 2 2 0]; % x values of points constructing Omega
yDomVal = [0 0 1 1]; % corresponding y value
RectDom = [3,4,xDomVal,yDomVal]'; % rectangular domain "3" with "4" sides
GeoDom = decsg(RectDom);

[p,e,t] = poimesh(GeoDom,nx,ny); % x edge into nx pieces, y edge into ny pieces
[p,e,t] = poimesh(GeoDom,n); % nx=ny=n
[p,e,t] = poimesh(GeoDom); % nx=ny=1
~~~

If you wanna create a regular mesh for a circle-shape geometry, [try it](http://persson.berkeley.edu/distmesh/).

#### Create a mesh from FreeFem++

In FreeFem++

~~~ cpp
verbosity=0;
real x0=0, x1=2;
real y0=0, y1=1;
int m=4; int n=m*2+1;
mesh Th=square(n,m,[x0+(x1-x0)*x,y0+(y1-y0)*y]);
plot(Th);
savemesh(Th,"ffmeshSinha.msh");
~~~

In matlab

~~~ matlab
[points,edges,triangles] = getMeshFromFF('ffmeshSinha.msh'); % use ff++
~~~

Function `getMeshFromFF` (need to check again)

~~~ matlab
function [points,edges,triangles] = getMeshFromFF(file)
% Get the mesh generated by FreeFem++
% Input: file mesh.msh created from FreeFem++
% Output: triplets describing the mesh in matlab

%% ========================================================
% IMPORT FROM FILE
% =========================================================
rawData = importdata(file);

% For some simple files (such as a CSV or JPEG files), IMPORTDATA might
% return a simple array.  If so, generate a structure so that the output
% matches that from the Import Wizard.
[~,name] = fileparts(file);
newData.(matlab.lang.makeValidName(name)) = rawData; % from genvarname

% Create new variables in the base workspace from those fields.
vars = fieldnames(newData);
for i = 1:length(vars)
    assignin('base', vars{i}, newData.(vars{i}));
end

%% ========================================================
% POINTS
% =========================================================
nP = rawData(1,1); % number of points
k = 0;
points = zeros(2,nP);
for i=2:nP+1
    k=k+1;
    points(1,k)=rawData(i,1);
    points(2,k)=rawData(i,2);
end

%% ========================================================
% TRIANGLES
% =========================================================
nT = rawData(1,2); % number of triangles
k=0;
triangles = zeros(2,nT);
for i=nP+2:2:nP+1+2*nT
    k=k+1;
    triangles(1,k)=rawData(i,1);
    triangles(2,k)=rawData(i,2);
    triangles(3,k)=rawData(i,3);
    triangles(4,k)=rawData(i+1,1);
end

%% ========================================================
% EDGES
% =========================================================
k = 0;
lecseg = zeros(nT*3,2);
for i=1:nT
    k=k+1;
    lecseg(k,1)=triangles(1,i);
    lecseg(k,2)=triangles(2,i);
    k=k+1;
    lecseg(k,1)=triangles(2,i);
    lecseg(k,2)=triangles(3,i);
    k=k+1;
    lecseg(k,1)=triangles(3,i);
    lecseg(k,2)=triangles(1,i);
end
nlecseg=k;

% Find the number of edge first
ndE=0; % number of double edges
dE = zeros(ndE*2,1); % store double edges
k=1;
for i=1:nlecseg
    sw=0;
    for j=1:i-1
        if((lecseg(i,1)==lecseg(j,1) && lecseg(i,2)==lecseg(j,2)) ||...
                (lecseg(i,1)==lecseg(j,2) && lecseg(i,2)==lecseg(j,1)))
            sw=1;
            dE(k)=j;
            k=k+1;
        end
    end
    if(sw==1)
        ndE = ndE+1;
        dE(k)=i;
        k=k+1;
    end
end
nbE = nlecseg - 2*ndE; % number of boundary edges

notbE = setdiff(1:nlecseg,dE); % idx of not-boundary edges

% k=0;
edges = zeros(7,nbE);
for i=1:nbE
    edges(1,i)=lecseg(notbE(i),1);
    edges(2,i)=lecseg(notbE(i),2);
    edges(3,i)=0;
    edges(4,i)=1;
    edges(5,i)=notbE(i);
    edges(6,i)=1;
    edges(7,i)=0;
end
~~~

#### Plot mesh

~~~ matlab
pdemesh(points,edges,triangles,'NodeLabels','on','ElementLabels','off');
~~~

#### Tìm tam giác lân cận (adjacent triangles)

~~~ matlab
pdeent(triangles,4); % xuất ra 4 và các chỉ số của các tam giác lân cận
~~~

### Plot PDE solution

Suppose that we have the solution $u$, 

~~~ matlab
[p,e,t] = initmesh('lshapeg');
[p,e,t] = refinemesh('lshapeg',p,e,t);
u = assempde('lshapeb',p,e,t,1,0,1);
figure(1);
pdesurf(p,t,u); % in 3D
figure(2);
pdeplot(p,e,t,'XYData',u); % in 2D with iso values
~~~

- `PDESURF` expects input of the form `pdesurf(p,t,u)`. `u` must either be a column vector and the same length as `p`, or a row vector and the same length as `t`.
- pdesurf không thể dùng title được! Đây là một hàm định nghĩa lại từ hàm pde

## Solvers in matlab 

- Solver mặc định của matlab là `LU`
- Danh sách các solver của matlam có thể xem tại [đây](https://fr.mathworks.com/help/dsp/ug/linear-algebra-and-least-squares.html#bvelgo9-3).
- You can find những solver được liệt kê và giải thích thêm [ở đây](http://faculty.cse.tamu.edu/davis/suitesparse.html) (SuiteSparse)
- `UMFPACK`: multifrontal LU factorization.  Appears as LU and x=A\b in MATLAB (cf. [link](http://faculty.cse.tamu.edu/davis/suitesparse.html)).

**Solve $Ax=b$ with LU** : dù nó là mặc định nhưng nếu muốn solve rõ ràng thì có thể áp dụng cách sau (cf. [đây](https://fr.mathworks.com/help/matlab/ref/lu.html?searchHighlight=lu%20solver&s_tid=doc_srchtitle))

~~~ matlab
% Wanna solve AU=F
[LL,UU] = lu(A);
tmp = LL\F;
U = UU\tmp; % this is the same with U=A\F
~~~

**Solve $Ax=b$ with GMRES**

~~~ matlab
solution = gmres(A,b,tol);
~~~

## Plot

Lưu ý rằng có thể sử dụng nhiều câu lệnh plot cùng với nhau (`line`,`quiver`,`pdemesh`,...), ngay cả với các lệnh plot PDE vì nó chỉ toàn vẽ trên hệ trục tọa độ thôi hà, vì thế cứ dùng tọa độ mà vẽ là được.

~~~ matlab
plot(x,y); % very simple plot of y=y(x)
plot(x,y,'line-style'); % line-style không quan trọng thứ tự, xem thêm ở matlab reference
plot(x,y,'-.r','LineWidth',2,'MarkerSize',10); % cứ cách một cái phẩy là một properties

% Đổi đơn vị của Ox
x = -pi:.1:pi;
set(gca,'XTick',-pi:pi/2:pi) %không có ";"
set(gca,'XTickLabel',{'-pi','-pi/2','0','pi/2','pi'}) % không có ";"

xlabel('Population','fontsize',12,'fontweight','b','color','r');
ylabel('Population','fontsize',12,'fontweight','b','color','r');
~~~
[Draw vector](https://fr.mathworks.com/help/matlab/ref/quiver.html?searchHighlight=quiver&s_tid=doc_srchtitle)

~~~ matlab
quiver(x,y,u,v); % plot u,v at x,y 	
~~~

### Plot line



### figure

Vẽ nhiều hình khác nhau, mỗi hình trên một `figure` riêng.

~~~ matlab
figure(1); plot(x,e);
figure(2); plot(x,u);
~~~

### contour  vs surface

Có thể vẽ `contour` (đường viền) của hình thay vì là `surface`

~~~ matlab
x = linspace(-2*pi,2*pi);
y = linspace(0,4*pi);
[X,Y] = meshgrid(x,y);
Z = sin(X)+cos(Y);
figure(1)
contour(X,Y,Z)
% contour(X,Y,Z,20) % specific number of lines (20) 
% contour(X,Y,Z,20,'ShowText','on') % hiển thị giá trị trên line
figure(2)
surface(X,Y,Z)
~~~

### axis

Set axis limit in x and y direction when plotting

~~~ matlab
plot(x,y)
axis([-10 10 0 inf]) %xmin xmax ymin ymax
~~~

Có thêm nhiều cái hay ho từ cái axis này lắm, như tắt axis, 

### Remarks

After plotting in 3D, có thể chọn nút "xoay" để thấy hình 3D

## Function

Có thể định nghĩa function mà không có biến (ví dụ này lấy trong file `master.m` matlab fem của Cheuk Lau)

~~~ matlab
function [ref_quad_pos, quad_weights] = ref_quad()
	% Quadrature nodes
	ref_quad_pos = [0.5 - 1 / (2 * sqrt(3)), 0.5 + 1 / (2 * sqrt(3))];
	% Quadrature weights
	quad_weights = [0.5, 0.5];	
end
%% Two-point Gauss quadrature over reference element
[ref_quad_pos, quad_weights] = ref_quad();
~~~

## Floating point number

Trong matlab, đôi khi các kết quả được matlab làm tròn hoặc đưa về một dạng mà ta không mong muốn. Ví dụ

~~~ matlab
e = 1 - 3*(4/3 - 1); % kq = 2.2204e-16 thay vì 0.
~~~

Xem thêm [tại tài liệu của matlab](https://fr.mathworks.com/help/matlab/matlab_prog/floating-point-numbers.html) hoặc [giải thích trên stackoverflow](http://stackoverflow.com/questions/686439/why-is-24-0000-not-equal-to-24-0000-in-matlab).

Nếu muốn thấy kết quả đầy đủ, dùng `format long`.

~~~ matlab
sin(pi); % not return 0
syms pi
sin(pi) % return 0
~~~



## Các commands không phân loại


`nargin` : number of input arguments in a function. See more on matlab help.

---

Normal to a curve $y=x^2$,

~~~ matlab
x = 0:0.1:1;
y = x.*x;
dy = gradient(y);
dx = gradient(x);
quiver(x,y,-dy,dx);
hold on; 
plot( x, y);
~~~



