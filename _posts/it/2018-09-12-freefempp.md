---
title: FreeFem++ note
categories: [it, phd]
toc: 1
tags: ["freefem++"]
maths: 1
comment: 1
---

I use this note for the FreeFem++ programming language. I have used it since the first year of my PhD thesis and I droped it 2 year laters because of some unexpected troubles. I then decide to use matlab instead. However, I keep using FreeFem++ in some simple cases just for comparing the computation with the codes done with matlab.

{% include toc.html %}

## Download and install

- Download the latest version at [here](http://www.freefem.org/).

## Miscellaneous

- Name of a file .edp must not contain a white space.



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

### P0, P1

- `P0`: `Vh.nt = u.n = Vh.ndof`
- `P1`: `u.n = Vh.dof = dim(V)`, `Vh.ndofK = 3`

## FE-space

~~~ cpp
func f = x^2 + y^2;
Vh fh = f; //fh is projection of f to Vh
plot(f); //error <-- can't plot
plot(fh); //plot is olny used under read/complex FE-function. 
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

- Logic (used inside `if`)

    ~~~ cpp
&& = and
|| =  or
<,>,<=,>=,!=,==
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



