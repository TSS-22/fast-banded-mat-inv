TO DO:

* change a to b, m to l and k to u. If it is not problematic with the math to make everything more understandable

* Check that mathbf are placed where they need to be and how they need to be

# fast-banded-mat-inv

A fast inverse square banded matrix utilities with explanations, based on the work of Kiliç et al., 2011.

# The banded matrix

Let it be a banded matrix $\mathbf{B}$, of order $n$ and band $r$ such as:

$$
\begin{equation}
\mathbf{B}_{r,n} = (b_{ij}) = 
    \begin{bmatrix}
        {\color{red}a^1_1} & {\color{lime}a^2_1} & {\color{teal}a^3_1} & \cdots & {\color{cyan}a^r_1} & {\color{darkgray}0} & \cdots & {\color{darkgray}0} \\

        {\color{orange}a^{-2}_1} & {\color{red}a^1_2} & {\color{lime}a^2_2} & {\color{teal}a^3_2} & \cdots & {\color{cyan}a^r_2} & \ddots & \vdots \\

        {\color{violet}a^{-3}_1} & {\color{orange}a^{-2}_2} & {\color{red}a^1_3} & {\color{lime}a^2_3} & {\color{teal}a^3_3} & \cdots & \ddots &  {\color{darkgray}0} \\

        \vdots & {\color{violet}a^{-3}_2} & {\color{orange}a^{-2}_3} & {\color{red}a^1_4} & {\color{lime}a^2_4} & \ddots & \ddots & {\color{cyan}a^{r}_{n-r+1}} \\

        {\color{pink}a^{-r}_1} & \vdots & {\color{violet}a^{-3}_3} & {\color{orange}a^{-2}_4} & {\color{red}a^1_5} & \ddots & {\color{teal}a^3_{n-2}} & \vdots \\

        {\color{darkgray}0} & {\color{pink}a^{-r}_2} & \cdots & \ddots & \ddots & \ddots & {\color{lime}a^2_{n-2}} & {\color{teal}a^3_{n-2}} \\

        \vdots & \ddots & \ddots & \cdots & {\color{violet}a^{-3}_{n-1}} & {\color{orange}a^{-2}_{n-2}} & {\color{red}a^1_{n-1}} & {\color{lime}a^2_{n-1}} \\

        {\color{darkgray}0} & \cdots & {\color{darkgray}0} & {\color{pink}a^{-r}_{n-r+1}} & \cdots & {\color{violet}a^{-3}_{n-2}} & {\color{orange}a^{-2}_{n-1}} & {\color{red}a^1_n} \\
    \end{bmatrix}
\end{equation}
$$

**Important, the notation $a^i_n$ does not denote the $i$th power of $a_n$.** 

With:

* $a^i_j$ arbitrary real numbers

* $-r \le i \le r$, and $0 \le j \le r \le n $

# $\mathbf{LU}$ factorization of the banded matrix

The unitary lower $\mathbf{L}$ and upper $\mathbf{U}$ matrix 

$$
\begin{equation}
\mathbf{L} = (l_{ij}) = 
\begin{bmatrix}
    {\color{OrangeRed}1} &  &  &  &  &  &  & {\color{darkgray}0} \\
    
    {\color{magenta}m^1_1} & {\color{OrangeRed}1} &  &  &  &  &  &  \\

    {\color{violet}m^2_1} & {\color{magenta}m^1_2} & {\color{OrangeRed}1} &  &  &  &  &  \\

    \vdots & {\color{violet}m^2_2} & {\color{magenta}m^1_3} & {\color{OrangeRed}1} &  &  &  &  \\

    {\color{pink}m^{r-1}_1} & \vdots & {\color{violet}m^2_3} & {\color{magenta}m^1_4} & \ddots &  &  &  \\

    {\color{darkgray}0} & {\color{pink}m^{r-1}_2} & \ddots & {\color{violet}m^2_4} & \ddots & {\color{OrangeRed}1} &  &  \\

    \vdots & \ddots & \ddots & \cdots & \ddots & {\color{magenta}m^1_{n-2}} & {\color{OrangeRed}1} &  \\

    {\color{darkgray}0} & \cdots & {\color{darkgray}0} & {\color{pink}m^{r-1}_{n-r+1}} & \cdots & {\color{violet}m^2_{n-2}} & {\color{magenta}m^1_{n-1}} & {\color{OrangeRed}1} \\
\end{bmatrix}
\end{equation}
$$


$$
\begin{equation}
\mathbf{U} = (u_{ij}) =
\begin{bmatrix}
    {\color{goldenrod}k^1_1} & {\color{yellowgreen}k^2_1} & {\color{limegreen}k^3_1} & \cdots & {\color{aquamarine}k^r_1} & {\color{darkgray}0} & \cdots & {\color{darkgray}0} \\

     & {\color{goldenrod}k^1_2} & {\color{yellowgreen}k^2_2} & {\color{limegreen}k^3_2} & \cdots & {\color{aquamarine}k^r_2} &  & \vdots \\

     &  & {\color{goldenrod}k^1_3} & {\color{yellowgreen}k^2_3} & {\color{limegreen}k^3_3} & \cdots & \ddots & {\color{darkgray}0} \\

     &  &  & {\color{goldenrod}k^1_4} & {\color{yellowgreen}k^2_4} & \ddots & \cdots & {\color{aquamarine}k^r_{n-r+1}} \\
      
     &  &  &  & {\color{goldenrod}k^1_5} & \ddots & {\color{limegreen}k^3_{n-3}} & \vdots \\

     &  &  &  &  & \ddots & {\color{yellowgreen}k^2_{n-2}} & {\color{limegreen}k^3_{n-2}} \\
    
     &  &  &  &  &  & {\color{goldenrod}k^1_{n-1}} & {\color{yellowgreen}k^2_{n-1}} \\
    
    {\color{darkgray}0} &  &  &  &  &  &  & {\color{goldenrod}k^1_n} \\

\end{bmatrix}
\end{equation}
$$

Below, $a^{\pm i}_{1}$, for $1 \le i \le n$ are the entries of $\mathbf{B}_{r,n}$.

It is assumed that all $k^i_s \neq 0$, which correspond to $\mathbf{B}_{r,n}$ being invertible.

## Initial conditions

### $U$

$$
\begin{equation}
m^i_1 = \frac{a^{-(i+1)}_1}{k^1_1} = \frac{a^{-(1+1)}}{{a^1_1}}

\end{equation}
$$

For: 

* $1 \le i \le r-1$

$$
\begin{equation}
\mathbf{U} = (u_{ij}) =
\begin{bmatrix}
    {\color{red}a^1_1} & {\color{red}a^2_1} & {\color{red}a^3_1} & \cdots & {\color{red}a^r_1} & {\color{darkgray}0} & \cdots & {\color{darkgray}0} \\

     & {\color{darkgray}k^1_2} & {\color{darkgray}k^2_2} & {\color{darkgray}k^3_2} & \cdots & {\color{darkgray}k^r_2} &  & \vdots \\

     &  & {\color{darkgray}k^1_3} & {\color{darkgray}k^2_3} & {\color{darkgray}k^3_3} & \cdots & \ddots & {\color{darkgray}0} \\

     &  &  & {\color{darkgray}k^1_4} & {\color{darkgray}k^2_4} & \ddots & \cdots & {\color{darkgray}k^r_{n-r+1}} \\
      
     &  &  &  & {\color{darkgray}k^1_5} & \ddots & {\color{darkgray}k^3_{n-3}} & \vdots \\

     &  &  &  &  & \ddots & {\color{darkgray}k^2_{n-2}} & {\color{darkgray}k^3_{n-2}} \\
    
     &  &  &  &  &  & {\color{darkgray}k^1_{n-1}} & {\color{darkgray}k^2_{n-1}} \\
    
    {\color{darkgray}0} &  &  &  &  &  &  & {\color{darkgray}k^1_n} \\

\end{bmatrix}
\end{equation}
$$

#### $L$

$$
\begin{equation}
k^i_1 = a^i_1
\end{equation}
$$

For:

* $1 \le i \le r$

$$
\begin{equation}
\mathbf{L} = (l_{ij}) = 
\begin{bmatrix}
    {\color{darkgray}1} &  &  &  &  &  &  & {\color{darkgray}0} \\
    
    {\color{red}\frac{a^{-2}_1}{a^1_1}} & {\color{darkgray}1} &  &  &  &  &  &  \\

    {\color{red}\frac{a^{-3}_1}{a^1_1}} & {\color{darkgray}m^1_2} & {\color{darkgray}1} &  &  &  &  &  \\

    \vdots & {\color{darkgray}m^2_2} & {\color{darkgray}m^1_3} & {\color{darkgray}1} &  &  &  &  \\

    {\color{red}\frac{a^{-r}_1}{a^1_1}} & \vdots & {\color{darkgray}m^2_3} & {\color{darkgray}m^1_4} & \ddots &  &  &  \\

    {\color{darkgray}0} & {\color{darkgray}m^{r-1}_2} & \ddots & {\color{darkgray}m^2_4} & \ddots & {\color{darkgray}1} &  &  \\

    \vdots & \ddots & \ddots & \cdots & \ddots & {\color{darkgray}m^1_{n-2}} & {\color{darkgray}1} &  \\

    {\color{darkgray}0} & \cdots & {\color{darkgray}0} & {\color{darkgray}m^{r-1}_{n-r+1}} & \cdots & {\color{darkgray}m^2_{n-2}} & {\color{darkgray}m^1_{n-1}} & {\color{darkgray}1} \\
\end{bmatrix}
\end{equation}
$$

## Rest of computation

### U

From those initial conditions, we then compute the rest of $k$ as such:
$$
\begin{equation}
k^i_s = a^i_s-\sum^{r-i}_{t=1}m^t_{s-t} k^{t+i}_{s-t}
\end{equation}
$$

For:

* $1 \le i \le r$

* $s \ge r \ge 1$

### L

And $m$ as such:

$$
\begin{equation}
m^i_s= \frac{a^{-(i+1)}_{s}-\sum^{r-i-1}_{t=1}m^{i+t}_{s-t}k^{t+1}_{s-t}}{k^1_s}
\end{equation}
$$

For: 

* $1 \le i \le r-1$


# Inverse of the triangular matrices $U$ and $L$

The source paper assumed the boundary conditions:

* $\mathbf{H}_u(r,r) = \mathbf{H}_l(r,r)$ 

* $\prod^{i}_{j}x_i=1$ for $i > j$

## Hessenberg matrix

The Hessenberg matrix of $\mathbf{L}$ and $\mathbf{U}$, as well as their determinants will be used to compute the inverse of the triangular matrices $L$ and $U$ latter. Therefore, we define those concepts below.

### $U$'s Hessenber matrix 

The Hessenberg matrix $\mathbf{H}_u(r,s) = (\tilde{h}_{ij})$, of order $(s-r) \times (s-r)$, of the upper triangular matrix $\mathbf{H} = (h_{ij})$ of dimensions $(n \times n)$ 

$$
\mathbf{H}_u(r,s) = 
\begin{bmatrix}
    h_{r,r+1} & h_{r,r+2} & \vdots & h_{r,s-1} & h_{r,s}\\
    h_{r+1,r+1} & h_{r+1,r+2} & \vdots & h_{r+1,s-1} & h_{r+1,s}\\
    0 & \ddots &  & \vdots & \vdots\\
    \vdots & \cdots & h_{s-2,s-2} & h_{s-2,s-1} & h_{s-2,s}\\
    0 & \cdots & 0 & h_{s-1,s-1} & h_{s-1,s}\\ 
\end{bmatrix}
$$

For:

* $s > r > 0$

### $L$'s Hessenberg matrix

The Hessenberg matrix $\mathbf{H}_l(r,s) = (\tilde{h}_{ij})$, of order $(s-r) \times (s-r)$, of the lower triangular matrix $\mathbf{H} = (h_{ij})$ of dimensions $(n \times n)$ 

$$
\mathbf{H}_l(r,s) = 
\begin{bmatrix}
    h_{r+1,r} & h_{r+1,r+1} & 0 &  & 0\\
    h_{r+2,r} & h_{r+2,r+1} & \ddots &  & \\
    \vdots & \vdots & \ddots & h_{s-2,s-2} & \\
    h_{s-1,r} & h_{s-1,r+1} & \cdots & h_{s-1,s-2} & h_{s-1,s-1}\\
    h_{s,r} & h_{s,r+1} & \cdots & h_{s,s-2} & h_{s,s-1}\\
\end{bmatrix}
$$

For:

* $s > r > 0$


### $\det \mathbf{H}_u(ij)$

Knowing that $(\mathbf{H}_u(r,s))^T = (\mathbf{H}_l(s,r))$, we only need to know how to compute the determinant of $\mathbf{H}_u$.

$$
\begin{equation}
\det(\mathbf{H}_u(ij)) = \sum^{j-i}_{t=1} 
\begin{Bmatrix}
(-1)^{2j-t}a_{j-tj}\det(\mathbf{H}_u(i,j-t)) \prod^{j-1}_{k=j-1-t}a_{kk}
\end{Bmatrix}
\end{equation}
$$

For:

* $j > i+1$

## $U^{-1}$

Let $\mathbf{G}$ = $\mathbf{L}^{-1}$ such as:

$$
\begin{equation}
g_{ij} = \begin{cases}
\frac{1}{k^1_i}, & \quad \text{if } j = i,\\
\frac{(-1)^{i+j}\det(\mathbf{U}_u(i,j))}{\prod^{j}_{r=i}k^1_r}, & \quad \text{if } j > i,\\
\end{cases}
\end{equation}
$$

With $\mathbf{U}_u(i,j)$ the Hessenberg matrix of $U$ as defined in the section above


## $L^{-1}$

Let $\mathbf{E}$ = $\mathbf{L}^{-1}$ such as:

$$
\begin{equation}
e_{ij} = \begin{cases}
1 & \quad \text{if }i=j,\\
(-1)^{i+j} \det(\mathbf{L}_l(ij)) & \quad \text{if }j < i,\\
\end{cases}
\end{equation}
$$

With $\mathbf{L}_l(i,j)$ the Hessenberg matrix of $L$ as defined in the section above

# Inverse of the $r$ banded matrix $\mathbf{B}$

Let $\mathbf{D}_n = (d_{ij}) = \mathbf{B}^{-1}$, defined as such:

$$
d_{ij} = \sum^{n}_{t=1}g_{it}e_{tj}
$$

With $g_{it}$ and $e_{tj}$ defined in the section above.

More explicitly, we have:

$$
\begin{equation}
d_{ij} = \begin{cases}
(-1)^{i+j} \frac{\det(\mathbf{U}_u(i,j))}{\prod^{j}_{r=i}k^1_r} + (-1)^{i+j} \sum^{n}_{t>j} S(i,t,j), & \quad \text{if } i < j,\\
\frac{1}{k^1_i} + \sum^{n}_{t>i}S(i,t,i), & \quad \text{if } i = j,\\
\frac{1}{k^1_i} (-1)^{i+j} \det(\mathbf{L}_l(i,j)) + (-1)^{i+j} \sum^{n}_{t>i}S(i,t,i), & \quad \text{if } i > j.\\
\end{cases}
\end{equation}
$$

With:

$$
\begin{equation}
S(i,t,j) = \frac{\det(\mathbf{U}_u(i,j))\det(\mathbf{L}_l(t,j))}{\prod^{j}_{r=i}k^1_r}
\end{equation}
$$

# Sources

KILIÇ, Emrah et STANICA, Pantelimon. The inverse of banded matrices. Journal of Computational and Applied Mathematics, 2013, vol. 237, no 1, p. 126-135.

