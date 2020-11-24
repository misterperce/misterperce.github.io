---
title: Multivariable Calculus Cheatsheet
layout: page
katex: yes
---
* TOC
{:toc}

&nbsp;

Derivative rules: [https://www.mathsisfun.com/calculus/derivatives-rules.html](https://www.mathsisfun.com/calculus/derivatives-rules.html)

### Cross Products

$$\vec{a} = (a_1, a_2, a_3)$$  

$$\vec{b} = (b_1, b_2, b_3)$$

$$\vec{a} \times \vec{b} = \begin{bmatrix} a_2b_3 - a_3b_2 \\ a_3b_1 - a_1b_3 \\ a_1b_2 - a_2b_1 \end{bmatrix}$$

### Partial Derivatives

$$ f_x = \frac{\partial f}{\partial x}(a,b) = \lim\limits_{h \to 0} \frac{f(a+h,b)-f(a,b)}{h} $$

$$ f_y = \frac{\partial f}{\partial y}(a,b) = \lim\limits_{h \to 0} \frac{f(a,b+h)-f(a,b)}{h} $$

#### Schwarz's Theorem (symmetry of second derivatives)

$$
\begin{aligned} \frac {\partial}{\partial x} \left( \frac{\partial f}{\partial y} \right) \ &= \  
       \frac {\partial}{\partial y} \left( \frac{\partial f}{\partial x} \right) \\
       \qquad f_{yx} &= f_{xy}
\end{aligned}
$$

#### Gradients

$$\nabla$$ - called 'Nabla' or 'del'

The gradient points in the direction of steepest ascent!

$$
\nabla f = \begin{bmatrix}
    \Large\frac{\partial f}{\partial x} \\
    \Large\frac{\partial f}{\partial y}
    \end{bmatrix}
$$

Example Gradient:

$$f(x,y) = x^2 sin(y)$$

$$\frac{\partial f}{\partial x} = 2xsin(y)$$

$$\frac{\partial f}{\partial y} = x^2cos(y)$$

$$\nabla f(x,y) = \begin{bmatrix}
    2xsin(y) \\
    x^2cos(y)
    \end{bmatrix}$$

### Directional Derivatives
Given:
$$\vec{w} = \begin{bmatrix} a \\ b \end{bmatrix} $$

The directional derivative is:

$$\nabla_{\vec{w}}f(x,y) = a \frac{\partial f}{\partial x} + b \frac{\partial f}{\partial y}$$

$$ = \begin{bmatrix} a \\ b \end{bmatrix} \cdot \begin{bmatrix}
    \frac{\partial f}{\partial x} \\
    \frac{\partial f}{\partial y}
    \end{bmatrix}$$

$$ = \vec{w} \cdot \nabla f$$

#### Formal Definition of Directional Derivative

$$\nabla_{\vec{v}}f(\vec{a}) = \lim\limits_{h \to 0} \frac{f(\vec{a} + h \vec{v})-f(\vec{a})}{h}$$

<!-- \\(\LaTeX code\\)    -->
