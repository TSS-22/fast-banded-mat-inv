

# fast-banded-mat-inv
A fast inverse banded matrix utilities with explanations test

# The banded matrix

Let it be a banded matrix $\mathbf{B}$, of order $n$ and band $r$ such as:

$$
\begin{equation}
\mathbf{B_{r,n}} = 
    \begin{bmatrix}
        \\
    \end{bmatrix}
\end{equation}
$$

**Important, the notation $a^i_n$ does not denote the $i$th power of $a_n$.** 

With:

* $a^i_j$ arbitrary real numbers

* $-r \le i \le r$, and $0 \le j \le r \le n $

# $LU$ factorization of the banded matrix