# fast-banded-mat-inv
A fast inverse banded matrix utilities with explanations test

# The banded matrix

Let it be a banded matrix $\mathbf{B}$, of order $n$ and band $r$ such as:

$$
\begin{equation}
\mathbf{B_{r,n}} = \begin{bmatrix}
{\color{OrangeRed}a^1_1} & {\color{LimeGreen}a^2_1} & {\color{Aquamarine}a^3_1} & \cdots & {\color{Cyan}a^r_1} & 0 & \cdots & 0\\
{\color{orange}a^{-2}_1} & {\color{OrangeRed}a^1_2} & {\color{LimeGreen}a^2_2} & {\color{Aquamarine}a^3_2} & \cdots & {\color{Cyan}a^r_2} & \ddots & \vdots\\
{\color{Violet}a^{-3}_1} & {\color{orange}a^{-2}_2} & {\color{OrangeRed}a^1_3} & {\color{LimeGreen}a^2_3} & {\color{Aquamarine}a^3_3} & \cdots & \ddots &  0\\
\vdots & {\color{Violet}a^{-3}_2} & {\color{orange}a^{-2}_3} & {\color{OrangeRed}a^1_4} & {\color{LimeGreen}a^2_4} & \ddots & \ddots & {\color{Cyan}a^{r}_{n-r+1}}\\
{\color{Pink}a^{-r}_1} & \vdots & {\color{Violet}a^{-3}_3} & {\color{orange}a^{-2}_4} & {\color{OrangeRed}a^1_5} & \ddots & {\color{Aquamarine}a^3_{n-2}} & \vdots\\
0 & {\color{Pink}a^{-r}_2} & \cdots & \ddots & \ddots & \ddots & {\color{LimeGreen}a^2_{n-2}} & {\color{Aquamarine}a^3_{n-2}}\\
\vdots & \ddots & \ddots & \cdots & {\color{Violet}a^{-3}_{n-1}} & {\color{orange}a^{-2}_{n-2}} & {\color{OrangeRed}a^1_{n-1}} & {\color{LimeGreen}a^2_{n-1}}\\
0 & \cdots & 0 & {\color{Pink}a^{-r}_{n-r+1}} & \cdots & {\color{Violet}a^{-3}_{n-2}} & {\color{orange}a^{-2}_{n-1}} & {\color{OrangeRed}a^1_n}\\
\end{bmatrix}
\end{equation}
$$

**Important, the notation $a^i_n$ does not denote the $i$th power of $a_n$.** 

With:

* $a^i_j$ arbitrary real numbers

* $-r \le i \le r$, and $0 \le j \le r \le n $

# $LU$ factorization of the banded matrix