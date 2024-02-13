---
layout: post
title: A new Interpretation of the Jacobi method
date: 2024-02-13 16:00:00+0100
description: Interpreting the Jacobi method as a collection of line searches
tags: numerical-analysis
categories: math
related_posts: false
---

# Putting things into context

If you are familiar with the terminology of _line search_
and know what the Jacobi method is, please feel free to skip directly to
[a new way of interpreting the Jacobi method](#a-new-way-of-interpreting-the-jacobi-method).

---

Consider a set of linear equations, i.e. 

\begin{equation}
    \label{eq:problem}
    Ax = b,
\end{equation}

where $$A$$ is a positive-definite, symmetric, and real $$N \times N$$ matrix.
It can be shown that finding a solution to eq. \eqref{eq:problem} is equivalent to
finding the minimizer of the target function

\begin{equation}
    \label{eq:minimization}
    F(x) := \frac{1}{2} x^T A x - b^T x.
\end{equation}

_Iterative methods_ try to find an approximation of the solution of
eq. \eqref{eq:problem} by finding a sequence
$$\{ x_k \}_k \subset \mathbb{R}^N$$
that eventually minimizes the target function $$F$$,
i.e. $$F(x_{k}) \to F(x^*) = \min_{x\in\mathbb{R}^N} F(x)$$,
Generally, one may think of obtaining a sequence of
iterates $$\{ x_k \}_k \subset \mathbb{R}^N$$
in the following way.
Given an initial value $$x_0 \in \mathbb{R}^N$$,
we iteratively define

\begin{equation}
\label{eq:algo}
x_{k+1} := x_k + d_k,
\end{equation}

where $$d_k := x_{i+1} - x_i \in \mathbb{R}^N$$.
How one chooses $$d_i$$ is what distinguishes different iterative
algorithms from each other.
In the following, we outline possible choices of the direction and length
of $$d_k$$ and finally draw the connection to an alternative interpretation
of the Jacobi method.

## The method of Gradient Descent
The method of Gradient Descent is an iterative method
operating along the lines of eq. \eqref{eq:algo}.
In every iteration, the method of Gradient descent moves
along the negative gradient of the target function $$F$$,
i.e. given an initial guess $$x_0 \in \mathbb{R}^N$$, one does

$$
x_{k+1} = x_k - \alpha_k \nabla F(x_k)
$$

where $$ -\nabla F(x_k) = b - A x_k =: r_k $$ is the so-called residual.
There are several ways of choosing the step size $$\alpha_k$$.
One of which is found by performing a _line search_ along the direction of $$r_k$$.

## Line Search
Given an iterate $$x_k$$ and a direction $$d_k$$,
a line search minimizes the target function $$F$$ along the line
$$\tau \mapsto x_k + \tau d_k,\,\tau\in\mathbb{R}$$,
i.e. we choose the step size $$\tau$$ by requiring
$$\frac{\mathrm{d}}{\mathrm{d}\tau} F(x_k + \tau d_k) = 0,$$
yielding,

$$
\tau_k := \frac{d_k^T r_k}{d_k^T A d_k}.
$$

---

# The Jacobi Method

The Jacobi method is another iterative method
operating along the lines of eq. \eqref{eq:algo}.
Namely, the Jacobi method is given by

\begin{equation}
\label{eq:jacobi}
x_{k+1} = x_k + \mathrm{diag}(A)^{-1} r_k.
\end{equation}

We now present the classic motivation and, finally,
a new way of interpreting the Jacobi method with the guidance
of line search.

## The classical motivation of the Jacobi method
Note that any matrix $$A$$ can be written as
$$A = \mathrm{diag}(A) + (A - \mathrm{diag}(A))$$.
Defining $$D:=\mathrm{diag}(A)$$,
we then rewrite eq. \eqref{eq:problem} as

$$
Ax = b
\Leftrightarrow
x = D^{-1} \Big[ \underbrace{b - Ax}_{=r} + Dx \Big] = x + D^{-1}r.
$$

This motivates the iterative method given by

$$
x_{k+1} = x_k + D^{-1}r_k,
$$

also known as the Jacobi method.

## A new way of interpreting the Jacobi method
Consider an iterate $$x_k$$.
Now, instead of performing an iteration step
along the lines of eq. \eqref{eq:algo},
we calculate the ideal step size for each canonical direction,
i.e. we do a line search for each canonical basis vector $$e_i$$.
Namely, for each $$i \in \{ 1, \dots, N \}$$, we calculate

$$
\alpha_i = \frac{e_i^T r_k}{e_i^T A e_i} = \frac{r_k^i}{A_{ii}},
$$

where $$r_k^i$$ denotes the $$i$$-th entry of the vector $$r_k$$.
Then, we collect all of these values in a single
direction vector $$d_k$$.
Namely, we define

$$
d_k := \sum_i \alpha_i e_i =  \mathrm{diag}(A)^{-1} r_k.
$$

Finally, by using this direction vector in eq. \eqref{eq:algo},
we indeed recover the Jacobi method, i.e.

$$
x_{k+1} = x_k + D^{-1}r_k.
$$