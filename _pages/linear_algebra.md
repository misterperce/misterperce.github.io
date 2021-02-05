---
title: Linear Algebra Reference
layout: page
katex: yes
---
* TOC
{:toc}

## Introduction

#### Span
Set of space achievable by scaling a given set of vectors.

#### Linearly Dependent
Describes a vector that is redundant in a set of vectors, i.e. does not expand the span of the set of vectors. In contrast, "linearly independent" describes a vector that is additive to the span created by a set of vectors.

Linearly dependent:  $$ \vec{u} = a\vec{v} + b\vec{w}$$

Linearly independent: $$ \vec{u} \not = a\vec{v} + b\vec{w}$$

#### Basis
The basis of a vector space is a set of linearly independent vectors that span the full space.

We use $$ \hat{i} $$ (unit vector along x axis) and $$ \hat{j} $$ (unit vector along y axis) as conventional basis vectors.

#### Linear transformation
Requires that (1) the transformation preserves lines (i.e. all lines stay lines, and don't get turned into curves) and (2) preserves the origin)

$$ \large{\begin{bmatrix} \textcolor{cadetblue}{a} & \textcolor{DarkSlateBlue}{b} \\ \textcolor{cadetblue}{c} & \textcolor{DarkSlateBlue}{d} \end{bmatrix} \begin{bmatrix} \textcolor{IndianRed}{x} \\ \textcolor{IndianRed}{y} \end{bmatrix} = \textcolor{IndianRed}{x} \begin{bmatrix} \textcolor{cadetblue}{a} \\ \textcolor{cadetblue}{c} \end{bmatrix} + \textcolor{IndianRed}{y} \begin{bmatrix} \textcolor{DarkSlateBlue}{b} \\ \textcolor{DarkSlateBlue}{d} \end{bmatrix} = \begin{bmatrix} \textcolor{cadetblue}{a}\textcolor{IndianRed}{x} +  \textcolor{DarkSlateBlue}{b}\textcolor{IndianRed}{y} \\ \textcolor{cadetblue}{c}\textcolor{IndianRed}{x} + \textcolor{DarkSlateBlue}{d}\textcolor{IndianRed}{y} \end{bmatrix}}
$$

Linear transformation of linearly dependent vectors will condense entire 2d coordinate plane into a line.

## Matrix Multiplication[^1]

$$ \large{\overleftarrow{\overbrace{
  \begin{bmatrix}
    \textcolor{cadetblue}{a} & \textcolor{cadetblue}{b} \\ \textcolor{cadetblue}{c} & \textcolor{cadetblue}{d}
  \end{bmatrix}}^{\text{M2}}
\overbrace{\begin{bmatrix}
    \textcolor{DarkSlateBlue}{e} & \textcolor{IndianRed}{f} \\ \textcolor{DarkSlateBlue}{g} & \textcolor{IndianRed}{h}
  \end{bmatrix}}^{\text{M1}}} =
\begin{bmatrix}
  \textcolor{cadetblue}{a}\textcolor{DarkSlateBlue}{e} +  \textcolor{cadetblue}{b}\textcolor{DarkSlateBlue}{g} & \textcolor{cadetblue}{a}\textcolor{IndianRed}{f} +  \textcolor{cadetblue}{b}\textcolor{IndianRed}{h} \\ \textcolor{cadetblue}{c}\textcolor{DarkSlateBlue}{e} + \textcolor{cadetblue}{d}\textcolor{DarkSlateBlue}{g} & \textcolor{cadetblue}{c}\textcolor{IndianRed}{f} + \textcolor{cadetblue}{d}\textcolor{IndianRed}{h}
\end{bmatrix}}
$$

I added an arrow here to remind myself that we read matrix transformations, or multiplications, right to left!

## Determinants

Determinants measure how area is squished or expanded through a transformation.

Negative determinants means that orientation of space has been inverted (i.e. the plane has flipped); absolute value of determinant will show how much the area of the space has transformed.

$$ det\begin{pmatrix}\begin{bmatrix} \textcolor{cadetblue}{a} & \textcolor{DarkSlateBlue}{b} \\ \textcolor{cadetblue}{c} & \textcolor{DarkSlateBlue}{d} \end{bmatrix}\end{pmatrix} = \textcolor{cadetblue}{a}\textcolor{DarkSlateBlue}{d} - \textcolor{DarkSlateBlue}{b}\textcolor{cadetblue}{c} $$

And for 3d transformations:

$$ det\begin{pmatrix}\begin{bmatrix}
  \textcolor{cadetblue}{a} & \textcolor{DarkSlateBlue}{b} & \textcolor{IndianRed}{c} \\
  \textcolor{cadetblue}{d} & \textcolor{DarkSlateBlue}{e} & \textcolor{IndianRed}{f} \\
  \textcolor{cadetblue}{g} & \textcolor{DarkSlateBlue}{h} & \textcolor{IndianRed}{i}\end{bmatrix}\end{pmatrix}  =
  \textcolor{cadetblue}{a} \ det\begin{pmatrix}\begin{bmatrix} \textcolor{DarkSlateBlue}{e} & \textcolor{IndianRed}{f} \\ \textcolor{DarkSlateBlue}{h} & \textcolor{IndianRed}{i} \end{bmatrix}\end{pmatrix}
  - \textcolor{DarkSlateBlue}{b} \ det\begin{pmatrix}\begin{bmatrix} \textcolor{cadetblue}{d} & \textcolor{IndianRed}{f} \\ \textcolor{cadetblue}{g} & \textcolor{IndianRed}{i} \end{bmatrix}\end{pmatrix}
  + \textcolor{IndianRed}{c} \ det\begin{pmatrix}\begin{bmatrix} \textcolor{cadetblue}{d} & \textcolor{DarkSlateBlue}{e} \\ \textcolor{cadetblue}{g} & \textcolor{DarkSlateBlue}{h} \end{bmatrix}\end{pmatrix} $$


## Linear System of Equations

Identity matrix: $$\begin{bmatrix}
   1 & 0 \\
   0 & 1
\end{bmatrix} $$ = the transformation matrix that does nothing!

Inverse matrix $$A^{-1}$$ is such that $$A^{-1}A = \begin{bmatrix}
   1 & 0 \\
   0 & 1
\end{bmatrix}$$

Given a system of equations, you can use the identity matrix to solve for variables, as long as $$det(A) \not = 0 $$:

$$ \large \begin{aligned}2x + 2y &= -4 \\ 1x + 3y &= -1 \\ \underbrace{\begin{bmatrix} 2 & 2 \\ 1 & 3 \end{bmatrix}}_{A} \underbrace{\begin{bmatrix} x \\ y \end{bmatrix}}_{\vec{x}} &= \underbrace{\begin{bmatrix} -4 \\ -1 \end{bmatrix}}_{\vec{v}} \\ A\vec{x}&=\vec{v} \\ A^{-1}A\vec{x} &= A^{-1}\vec{v} \\ \vec{x} &= A^{-1}\vec{v}
\end{aligned}$$

## Rank

Rank: number of dimensions in the output of a transformation, or number of dimensions in the column space.

When output of a transformation is a line, it is rank 1. When the output is a plane, it is rank 2.

For example, rank 2 is the highest rank a 2d coordinate system of vectors can achieve.

When the rank is the highest it can be, it is "full rank."

### Column Space

Column Space of $$A$$: set of all possible outputs of $$A\vec{v}$$

The column space lets us understand if a solution set exists for a system of equations.

### Null Space

When a transformation is full rank,  $$\begin{bmatrix} 0 \\ 0 \end{bmatrix} $$ is the only vector that ends up on $$\begin{bmatrix} 0 \\ 0 \end{bmatrix} $$. But, when a transformation loses rank, then multiple vectors are transformed to $$\begin{bmatrix} 0 \\ 0 \end{bmatrix} $$. These vectors that have collapsed to $$\begin{bmatrix} 0 \\ 0 \end{bmatrix} $$ are called the "null space" or "kernel."

The null space lets us understand what the set of all possible solutions can look like.

## Non-square Matricies

* Columns indicate basis vectors / input space
* Rows indicate "landing spots" for basis vectors

## Dot Product Intuition

$$\begin{aligned}\text{Matrix-vector product:} \begin{bmatrix}u_x & u_y\end{bmatrix}\begin{bmatrix}x \\ y\end{bmatrix} &= u_x \cdot x + u_y \cdot y \\ \text{Dot product:} \begin{bmatrix}u_x \\ u_y\end{bmatrix} \begin{bmatrix}x \\ y\end{bmatrix} &= u_x \cdot x + u_y \cdot y\end{aligned}$$

## Cross Product

$$ \vec{v} × \vec{w} = \vec{p} $$

$$ \vec{p} $$ is perpendicular to the parallelogram created by $$ \vec{v} $$ and $$ \vec{w} $$ and $$ \vec{p} $$ has a length equal to the area of the parallelogram. Which perpendicular direction? Use the right hand rule.

<img src="/assets/post-imgs/right_hand_rule_stolen_from_wikipedia.png" width="250"/>

### Cramer's Rule

See [https://www.chilimath.com/lessons/advanced-algebra/cramers-rule-with-three-variables/](https://www.chilimath.com/lessons/advanced-algebra/cramers-rule-with-three-variables/)

## Change of Basis

$$ A^{-1}MA \vec{v}$$

$$ A^{-1} : \text{inverse change of basis matrix} \\
M: \text{transformation matrix, written in familiar basis terms} \\
A: \text{change of basis matrix} \\
\vec{v} : \text{vector in another basis} $$

## Eigenvectors & Eigenvalues
Eigenvectors are lines(?) in which vectors are simply scaled rather than knocked off their span from a matrix transformation.

Eigenvalues are the scalar that the eigenvectors change by through the matrix transformation.

Eigenvector of a 3d rotation == axis of the rotation!!

$$A\vec{v} = \lambda \vec{v}$$

$$A$$ is the transformation matrix; $$\vec{v}$$ is the eigenvector; $$\lambda$$ is the eigenvalue

Interpretation: matrix multiplication gives the same result as just scaling the vector with some value

$$\begin{aligned} A\vec{v} &= \lambda \vec{v} \\ A\vec{v} - \lambda I\vec{v} &= 0 \\ (A- \lambda I)\vec{v} &= 0 \\  \det(A- \lambda I) & = 0\end{aligned}$$

A set of basis vectors that are also eigenvectors is an eigenbasis.

## Abstract Vector Spaces

Functions are vector-ish and can be transformed linearly.

Derivatives are linear transformations.

Linear algebra concepts have direct analogs in the world of functions:

| Linear Algebra Concepts | Analog to functions |
|------------------------------------------|------|
| Linear transformations | Linear operations |
| Dot products | Inner products |
| Eignvectors | Eigenfunctions |


[^1]: <br/> [![img](/assets/post-imgs/3b1b_matrix_mult.PNG)](https://www.youtube.com/watch?v=XkY2DOUCWMU&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab&index=4&ab_channel=3Blue1Brown)
