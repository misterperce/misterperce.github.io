---
title: Linear Algebra Cheatsheet
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
Requires that (1) the transformation preserves lines (i.e. all lines stay lines, and don't get turned into c) and (2) preserves the origin

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

## Determinants

Determinants measure how area is squished or expanded through a transformation.

Negative determinants means that orientation of space has been inverted (i.e. the plane has flipped); absolute value of determinant will show how much the area of the space has transformed.

$$ det\begin{pmatrix}\begin{bmatrix} \textcolor{cadetblue}{a} & \textcolor{DarkSlateBlue}{b} \\ \textcolor{cadetblue}{c} & \textcolor{DarkSlateBlue}{d} \end{bmatrix}\end{pmatrix} = \textcolor{cadetblue}{a}\textcolor{DarkSlateBlue}{d} - \textcolor{DarkSlateBlue}{b}\textcolor{cadetblue}{c} $$

$$ det\begin{pmatrix}\begin{bmatrix}
  \textcolor{cadetblue}{a} & \textcolor{DarkSlateBlue}{b} & \textcolor{IndianRed}{c} \\
  \textcolor{cadetblue}{d} & \textcolor{DarkSlateBlue}{e} & \textcolor{IndianRed}{f} \\
  \textcolor{cadetblue}{g} & \textcolor{DarkSlateBlue}{h} & \textcolor{IndianRed}{i}\end{bmatrix}\end{pmatrix}  =
  \textcolor{cadetblue}{a} \ det\begin{pmatrix}\begin{bmatrix} \textcolor{DarkSlateBlue}{e} & \textcolor{IndianRed}{f} \\ \textcolor{DarkSlateBlue}{h} & \textcolor{IndianRed}{i} \end{bmatrix}\end{pmatrix}
  - \textcolor{DarkSlateBlue}{b} \ det\begin{pmatrix}\begin{bmatrix} \textcolor{cadetblue}{d} & \textcolor{IndianRed}{f} \\ \textcolor{cadetblue}{g} & \textcolor{IndianRed}{i} \end{bmatrix}\end{pmatrix}
  + \textcolor{IndianRed}{c} \ det\begin{pmatrix}\begin{bmatrix} \textcolor{cadetblue}{d} & \textcolor{DarkSlateBlue}{e} \\ \textcolor{cadetblue}{g} & \textcolor{DarkSlateBlue}{h} \end{bmatrix}\end{pmatrix} $$


## Linear System of Equations

[^1]: <br/> ![img](/assets/post-imgs/3b1b_matrix_mult.PNG)
