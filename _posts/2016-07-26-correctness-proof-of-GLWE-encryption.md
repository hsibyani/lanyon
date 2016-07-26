---
layout: post
title: Correctness Proof of GLWE-based Encryption
---
While reading a GLWE-based encryption described in section 3.1 of [BGV12](https://eprint.iacr.org/2011/277). The paper says that correctness is obvious and it only became obvious to me after a bit. This should cover most of the proof outline.

*Proof:* We have to show that the dot product of $$\textbf{c}$$ and $$\textbf{s}$$ reduces to the message. Let $$\textbf{b}_i$$, $$\textbf{r}_i$$, and $$\textbf{s}'_i$$ be the $$i$$th element in $$\textbf{b}$$, $$\textbf{r}$$, and $$\textbf{s}'$$ respectively. We will zoom in the construction of $$\textbf{b}$$ as a start. Remember that it's defined as $$\textbf{b} \leftarrow \textbf{A}'\textbf{s}'+2\textbf{e}$$. I will notate $$a'_{ij}$$ to be the element of the matrix $$\textbf{A}'$$. 

$$ \textbf{b}= \begin{bmatrix}
    a'_{11} & \dots & a'_{1n} \\
    a'_{21} & \dots & a'_{2n} \\
    \vdots & \ddots & \vdots \\
    a'_{N1} & \dots & a'_{Nn} 
\end{bmatrix}
%
\begin{bmatrix}
    s'_{1} \\
    \vdots \\
    s'_{n} 
\end{bmatrix}
+ 2\textbf{e}
=
\begin{bmatrix}
    a'_{11} s'_1 + \dots + a'_{1n} s'_n\\
    a'_{21} s'_1 + \dots + a'_{2n} s'_n\\
    \vdots\\
    a'_{N1} s'_1 + \dots + a'_{Nn} s'_n

\end{bmatrix}
+ 2\textbf{e}
=
\begin{bmatrix}
    b_1 \\
    b_2 \\
    \vdots \\
    b_N
\end{bmatrix}
$$

We have $$\textbf{c}=\textbf{m}+\textbf{A}^T \textbf{r}$$. $$\textbf{c}=$$
$$
\begin{bmatrix}
    m \\
    0 \\
    \vdots \\
    0 
\end{bmatrix}
$$
+
$$
\begin{bmatrix}
    b_{1} & b_{2} & \dots & b_{N} \\
    -a'_{11} & -a'_{21} & \dots & -a'_{N1} \\
    \vdots & \vdots & \ddots & \vdots \\
    -a'_{1n} & -a'_{2n} & \dots & a'_{Nn} 
\end{bmatrix}
%
\begin{bmatrix}
    r_1 \\
    r_2 \\
    \vdots \\
    r_N
\end{bmatrix}
$$
=
$$
\begin{bmatrix}
    m + b_1 r_1 + \dots + b_N r_N\\
    -a'_{11} r_1 - \dots  -a'_{N1} r_N\\
    \vdots\\
    -a'_{1n} r_1 - \dots  -a'_{Nn} r_N
\end{bmatrix}
$$

Now performing the dot product $$\langle \textbf{c}, \textbf{s}\rangle$$ we get:
$$
\textbf{c} \cdot \textbf{s} = \begin{bmatrix}
    m + b_1 r_1 + \dots + b_N r_N\\
    -a'_{11} r_1 - \dots  -a'_{N1} r_N\\
    \vdots\\
    -a'_{1n} r_1 - \dots  -a'_{Nn} r_N
\end{bmatrix}
\cdot
\begin{bmatrix}
    1 \\
    s'_1 \\
    \vdots \\
    s'_n
\end{bmatrix}
=
m+\sum_{k=1}^N r_k ( b_k - \sum_{l=1}^n a'_{1l} s_l)
$$
Note that in $$\textbf{b}$$ we can neglect $$2\textbf{e}$$ to compute our message since it's $$0 \mod 2$$. For any $$r_k=1$$ we have the term $$b_k$$ to be equal to the inner summation module 2. Thus, we will be left with $$m$$.
