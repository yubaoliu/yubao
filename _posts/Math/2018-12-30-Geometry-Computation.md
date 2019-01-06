---
title: Geometry Computation  计算几何
---

# Area of triangle
## Shoelace formula
[Proof for a triangle -wiki](https://en.wikipedia.org/wiki/Shoelace_formula)

![Shoelace](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a9/Shoelace3.png/800px-Shoelace3.png){#fig:id}


Refer @fig:id


**Definition:**
The formula can be represented by the expression

$$
\begin{aligned}
{\mathbf  {A}} &= {1 \over 2} {\Big |}
\sum _{i=1}^{n-1} x_{i} y_{i+1}+x_{n}y_{1} - \sum _{i=1}^{n-1}x_{i+1}y_{i}-x_{1}y_{n}{\Big |}\\
  &={1 \over 2}|x_{1}y_{2}+x_{2}y_{3}+\cdots +x_{n-1}y_{n}+x_{n}y_{1}-x_{2}y_{1}-x_{3}y_{2}-\cdots -x_{n}y_{n-1}-x_{1}y_{n}| \\
\end{aligned}
$${#eq:id1}

see @eq:id1

where

- $A$ is the area of the polygon,
- $n$ is the number of sides of the polygon, and
- $(x_i, y_i), i = 1, 2,..., n$ are the vertices (or "corners") of the polygon.

$$
{\displaystyle \mathbf {A} ={1 \over 2}{\Big |}\sum _{i=1}^{n}x_{i}(y_{i+1}-y_{i-1}){\Big |}={1 \over 2}{\Big |}\sum _{i=1}^{n}y_{i}(x_{i+1}-x_{i-1}){\Big |}={1 \over 2}{\Big |}\sum _{i=1}^{n}x_{i}y_{i+1}-x_{i+1}y_{i}{\Big |}={1 \over 2}{\Big |}\sum _{i=1}^{n}(x_{i+1}+x_{i})(y_{i+1}-y_{i}){\Big |}={1 \over 2}{\Big |}\sum _{i=1}^{n}\det {\begin{pmatrix}x_{i}&x_{i+1}\\y_{i}&y_{i+1}\end{pmatrix}}{\Big |}}
$${#eq:id2}


where $x_{n+1} = x_1$ and $x_0 = x_n$, as well as $y_{n+1} = y_1$ and $y_0 = y_n$


$$
{\displaystyle \mathbf {A} ={\frac {1}{2}}{\begin{vmatrix}1&1&1\\x_{1}&x_{2}&x_{3}\\y_{1}&y_{2}&y_{3}\end{vmatrix}}}
$${#eq:}

If the coordinates are written in a clockwise order, the value of the determinant will be $-A$

Rearranging another way

$$
{\displaystyle \mathbf {A} ={\frac {1}{2}}|x_{1}y_{2}+x_{2}y_{3}+x_{3}y_{1}-x_{2}y_{1}-x_{3}y_{2}-x_{1}y_{3}|}
$${#eq:}

![caption](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/Triangle_area_from_coordinates_JCB.jpg/732px-Triangle_area_from_coordinates_JCB.jpg){#fig:id_fig height=240px}
