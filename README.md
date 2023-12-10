

# fast-banded-mat-inv
A fast inverse banded matrix utilities with explanations test

# The banded matrix

Let it be a banded matrix $\mathbf{B}$, of order $n$ and band $r$ such as:

$$
\begin{equation}
\mathbf{B_{r,n}} = 
    \begin{bmatrix}
        {\color{red}a^1_1} & {\color{lime}a^2_1} & {\color{teal}a^3_1} & \cdots & {\color{cyan}a^r_1} & 0 & \cdots & 0 \\
        {\color{orange}a^{-2}_1} & {\color{red}a^1_2} & {\color{lime}a^2_2} & {\color{teal}a^3_2} & \cdots & {\color{cyan}a^r_2} & \ddots & \vdots \\
        {\color{violet}a^{-3}_1} & {\color{orange}a^{-2}_2} & {\color{red}a^1_3} & {\color{lime}a^2_3} & {\color{teal}a^3_3} & \cdots & \ddots &  0 \\
        \vdots & {\color{violet}a^{-3}_2} & {\color{orange}a^{-2}_3} & {\color{red}a^1_4} & {\color{lime}a^2_4} & \ddots & \ddots & {\color{cyan}a^{r}_{n-r+1}} \\
    \end{bmatrix}
\end{equation}
$$

**Important, the notation $a^i_n$ does not denote the $i$th power of $a_n$.** 

With:

* $a^i_j$ arbitrary real numbers

* $-r \le i \le r$, and $0 \le j \le r \le n $

# $LU$ factorization of the banded matrix


