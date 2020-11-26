---
title: Linear Algebra Cheatsheet
layout: page
katex: yes
---
* TOC
{:toc}

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

$$ \begin{bmatrix} \textcolor{cadetblue}{a} \ \textcolor{darkolivegreen}{b} \\ \textcolor{cadetblue}{c} \ \textcolor{darkolivegreen}{d} \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = x \begin{bmatrix} \textcolor{cadetblue}{a} \\ \textcolor{cadetblue}{c} \end{bmatrix} + y \begin{bmatrix} \textcolor{darkolivegreen}{b} \\ \textcolor{darkolivegreen}{d} \end{bmatrix} = \begin{bmatrix} \textcolor{cadetblue}{a}x +  \textcolor{darkolivegreen}{b}y \\ \textcolor{cadetblue}{c}x + \textcolor{darkolivegreen}{d}y \end{bmatrix}
$$

Linear transformation of linearly dependent vectors will condense entire 2d coordinate plane into a line.
