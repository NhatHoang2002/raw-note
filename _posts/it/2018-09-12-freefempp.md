---
title: FreeFem++ note
categories: [it, phd]
toc: 1
tags: ["freefem++"]
maths: 1
comment: 1
date: 2018-09-14
---

I use this note for the FreeFem++ programming language. I have used it since the first year of my PhD thesis and I droped it 2 year laters because of some unexpected troubles. I then decide to use matlab instead. However, I keep using FreeFem++ in some simple cases just for comparing the computation with the codes done with matlab.

{% include toc.html %}

## Work with PhD

- This is very interesting: *numerical modeling transport problem with freefem - Florian De Vuyst.pdf*

## Download and install

- Download the latest version at [here](http://www.freefem.org/).

## Miscellaneous

- `verbosity = 0;` at the beginning of file: only display the most useful
- Name of a file .edp must not contain a white space.
- Line break: just type enter as usual.
- Normal derivative

    ~~~ cpp
macro dn(u) (N.x*dx(u)+N.y*dy(u) ) //  def the normal derivative 
    ~~~

- Find the area of each triangle K

    ~~~ cpp
mesh Th=square(10,10);
fespace Wh(Th,P0);
Wh etaK;
varf varea(unused,chiK) = int2d(Th,levelset=phi)(chiK);
etaK[] = varea(0,Wh);
cout << "etaK[]= " << etaK[] << endl;
//etaK[i] = area the ith triangle
    ~~~
- Load vector
    
    ~~~ cpp
real b(Vh.ndof); 
b = a(0,Vh);
    ~~~

- Include cpp file inside a edp 

    ~~~ cpp
load "./nomfichier";
    ~~~

- Normal vector's direction

    ~~~ cpp
int1d(Th, levelset=phi)(dn(u)) // n=(1,0); //for Omega1 (on the left)
int1d(Th, levelset=-phi)(dn(u)) // n=(-1,0); //for Omega2 (on the right)
    ~~~

- Include another edp file into a edp file

    ~~~ cpp
include "<name>.edp"; // location is not important
    ~~~

- ff++ never uses label on the vertices

## FreeFem++ with Visual Studio Code

- Install FreeFem++ as usual
- **Terminal** > **Configure Default Build Task** (choose the folder stick to this task)
- A **task.json** file opened and fill it with

    ~~~ 
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Run FreeFem++",
      "type": "shell",
      "command": "FreeFem++ ${file}",
      "group": {
        "kind": "build",
        "isDefault": true
      },
    }
  ]
}
    ~~~

- Press **Ctrl + Shift + B**.
- Assign keyboard shortcut to this task: **Files** > **Preferences** > **Keyboard Shortcuts** > Click on link "**keybindings.json**" and add following codes (change "ctrl+r" with the ones you want)

    ~~~
{
    "key": "ctrl+r",
    "command": "workbench.action.tasks.runTask",
    "args": "Run FreeFem++"
}
    ~~~

## The order working with FreeFem++

1. Define a boundary

    ~~~ cpp
mesh Th= square(); // [0,1] x [0,1]
    ~~~

    or an arbitary square `[x0, x1] x [y0, y1]`

    ~~~ cpp
real x0=0, x1=2;
real y0=0, y1=1;
int n=40, m=20; // number of fragments
mesh Th=square( n, m, [x0 + (x1-x0)*x, y0 + (y1-y0)*y] );
    ~~~

    or

    ~~~ cpp
border <name>(t=a,b){x=f(t); y=g(t);};
mesh Th = buildmesh( <name>(nf) + <name>(nf) );
    ~~~

2. FE space

    ~~~ cpp
fespace Vh(Th,P1); // P0 
Vh u = h(x,y);
    ~~~

3. Starting to work!


## Plot

~~~ cpp
plot(Th, wait=1,fill=1,ps="SmileyFace.eps",bw=1,value=1, cmm="");
~~~

- `wait`: wait for click
- `fill`: fill figure
- `ps`: save plot to ps file
- `bw`: black and white 
- `value`: display isoline
- `cmm`: insert comment for figure

### Modify iso color range

~~~ cpp
real[int] viso(31);
for (int i=0; i<viso.n; i++){
	viso[i] = i*0.3;
}
~~~

## Mesh

### Mesh connectivity

- index starts from 0.
- `Vh.nt` : number of elements/triangles
- `Vh.ndof` : number of dof (degree of freedom) = dim of space Vh = u.n
- `Vh.ndofK` : number of dof on 1 element.
- `u.n` : number of element of u
- `Wh(k,i)` : gives the number of ith degrees of freedom of element k.
- `Th.nt` : number of triangles
- `Th.nv` : number of vertices
- `Th(i)` : return the vextex i of Th
- `Th(i).x`: vertex i's x-coor
- `Th(i).y`: vertex i's y-coor
- `Th[k]` : return the triangle k of Th
- `Th[i][j]` 	: ith triangle's jth vertex
- `Th[i][j].x` : 
- `Th[i][j].y` : 
- `Th[i][j].label` : node's label
- Write

    ~~~ cpp
for (int i=0;i<nbtriangles;i++){ //all triangles
	for (int j=0; j <3; j++){ //all vertices of the triangle i
		cout <<i<<" "<<j<<" Th[i][j] = "<<Th[i][j]<<
		" x = "<<Th[i][j].x<< " , y= "<<Th[i][j].y << 
		", label=" << Th[i][j].label << endl;
	}
}
    ~~~

- `Th(0.55,0.6).nuTriangle` : triangle's number of some triangle.
- `Th[it00].area` : triangle's area
- `Th[it00].region`: triangle's region
- `Th[it00].label`: triangle's label
- Diameter of a triangle

    ~~~ cpp
Ph h = hTriangle
h[].max
    ~~~

### Structure of `.msh` file

- Save mesh
    ~~~ cpp
savemesh(Th, '<name>.msh');
    ~~~
- See the description of the structure of `.msh` at section 5.1.4 *Data Structures and Read/Write Statements for a Mesh*.
    - They also used (like in matlab): the number of *nodes*, *triangles* and *edges on boundary* .
    - The vertices are numbered in a *counterclockwise orientation* like in malab. 
- Using `getMeshFromFF.m` to read the file `.msh` from ff++ (downloaded from [here](https://fr.mathworks.com/matlabcentral/fileexchange/26833-freefem-to-matlab)).

### Region

- Insert into mesh

    ~~~ cpp
mesh Th2 = square(nn,nn,[2*x,3*y],region=2);        // RHS
mesh Th1 = square(nn,nn,[-x,3*y],region=1); // LHS
mesh Th = Th1 + Th2;
plot(Th,cmm="Th",wait=1);
    ~~~

- How to use? `Th(0,0).region`

### Labels

~~~ cpp
for (int i=0;i<5;++i)
{
int[int] labs=[11,12,13,14];
mesh Th=square(3,3,flags=i,label=labs,region=10);
plot(Th,wait=1,cmm=" square flags = "+i );
}
~~~

### P0, P1

- `P0`: `Vh.nt = u.n = Vh.ndof`
- `P1`: `u.n = Vh.dof = dim(V)`, `Vh.ndofK = 3`

### Connect 2 meshes

~~~ cpp
mesh Th2 = square(nn,nn,[2*x,3*y],region=2);        // RHS
mesh Th1 = square(nn,nn,[-x,3*y],region=1); // LHS
mesh Th = Th1 + Th2;
plot(Th,cmm="Th",wait=1);
~~~

### intalledges, jump, mean

~~~ cpp
varf Ans(u,v)= 
   int2d(Th)(dx(u)*dx(v)+dy(u)*dy(v)  )
 + intalledges(Th)(//  loop on all  edge of all triangle 
       // the edge are see nTonEdge times so we / nTonEdge
       // remark: nTonEdge =1 on border edge and =2 on internal 
       // we are in a triange th normal is the exterior normal
       // def: jump = external - internal value; on border exter value =0
       //      mean = (external + internal value)/2, on border just internal value
            ( jump(v)*mean(dn(u)) -  jump(u)*mean(dn(v)) 
          + pena*jump(u)*jump(v) ) / nTonEdge 
)
~~~

## FE-space

~~~ cpp
func f = x^2 + y^2;
Vh fh = f; //fh is projection of f to Vh
plot(f); //error <-- can't plot
plot(fh); //plot is olny used under read/complex FE-function. 
~~~


## Matrix

- In ff++ code, matrix starts from `A(0,0)` but in the input, it says `(1,1)`
- Matrix is **sparse** in ff++
- `A.n` dimension of A
- Dimension of matrix obtained from `int2d(Th, levelset=phi)` has the same dimension without `levelset=phi` (normal matrix obtained from `int2d`)
- `cout << A` gives

    ~~~ cpp
4 4 0 5 // row colum is-symmetric value
1 2 1 //value at row 1, column 2 is 1
    ~~~

- A matrix created by `A = [[ 0, 1, 0, 10], [0, 0, 2,0], [0,0,0, 3], [ 4,0 , 0, 0]];` is also a sparse matrix whose `A(0,0)` doesn't exist.
- `[I,J,C] = A` collects I indexes of rows, j indexes of columns, C values

    ~~~ cpp
int[int] I(1),J(1);
real[int] C(1);
[I,J,C] = A; 
B = A(I,J); // B(i,j)=A(I(i),J(j)) //dim(B)=dim(I)*dim(J)
C = A(I^-1,J^-1); //B(I(i),J(j))=A(i,j)
    ~~~ 

- `A.resize(10,20)`: resize matrix's dimension
- Matrix's diagonal

    ~~~ cpp
diagofA = A.diag; // get the diagonal of the matrix 
A.diag = diagofA ; //set the diagonal of the matrix
    ~~~


### Stiffness matrix

~~~ cpp
varf a(u,v) = int2d(Th)(dx(u)*dx(v) + dy(u)*dy(v)) + on(C,u=0);
varf b([v],[f]) = int2d(Th)(v*f);
matrix A = a(Vh,Vh); //stiffness matrix
matrix B = b(Vh,Vh);
F[] = B*f[]; //load vector
u[] = A^-1*F[];
~~~


## Loops & condition

~~~ cpp
for(int i=1;i<n;i++){
	commands;
}

while (int i<=n){
	commands;
	i=i+1;
}

if(condition){
	statements;
}
~~~

## Define a function

- Function of a number
    ~~~ cpp
func real gamma(real x, real y){
	if(x<x1/4 || x>3*x1/4 || y>y1/2) 
		return 1; 
	else
		if((x>x1/4) && (x<3*x1/4) && (y<y1/2))
			return -1;
		else
			return 0;
}
    ~~~
- Function of an array

    ~~~ cpp
func real[int] name(real[int] &x){ //cai nay dung con tro thi phai 
	real[int] u;
	....
	return u; //hoac cung co the return x va khong can dinh nghia truoc u
}
    ~~~


## Array in FreeFem++

- index starts from 0
- `tab.min`, `tab.max`
- Change size: `tab.resize(12)`
- `tab.sum`
- `tab.sort`
- Others

    ~~~ cpp
    real[string] text; //use string as an index
    text["+"] = 1.5;
    
    int[int] tt(2:10); // 2 to 10
    int[int] t1(2:3:10); // 2 5 8
    
    complex[int] tt(2.+0i:10.+0i); // 2,3,4,5,6,7,8,9,10
    complex[int] t1(2.:3.:10.); // 2,5,8,
    tt.re << endl ; // the real part array
    tt.im << endl ; // the imag part array
    ~~~



## Operators

- Logic comparison (used inside `if`)

    ~~~ cpp
&& = and
|| =  or
<,>,<=,>=,!=,==
    ~~~

- Logic inline operators

    ~~~ cpp
    u = 5-(y>=0.3)*10; //if y>=3 is true then (y>=3)=1 else =0
    u = (x>5)?1:2; //if x>5 is true, then u=1 else u=2
    
    y=2+(x=5); // x=5 then y = 2+x = 7
    
    x = 5+(3==2); // x = 5+0=5
    ~~~


## Errors

- Comparison

    ~~~ cpp
real y = 1;
real y0 = 1/2;
real y1 = 1./2;
if (y0 == y/2) cout << "1"; else cout << "0"; //result 0
if (y0 == 1/2) cout << "1"; else cout << "0"; //result 1
if (y0 == 0.5) cout << "1"; else cout << "0"; //result 0
if (y1 == 0.5) cout << "1"; else cout << "0"; //result 1
    ~~~

## Level set

~~~ cpp
int2d(Th,1,levelset=phi)()
~~~

The number `1` means `region = 1`.

~~~ cpp
mesh Th=square(n,m,[x0+(x1-x0)*x,y0+(y1-y0)*y],region=1);
~~~

The order

~~~ cpp
Vh phi=y-0.3;
int2(Th,levelset=-phi) --> upper (Omega1)
phi(x)>0 --> x in Omega1 (upper);
~~~

