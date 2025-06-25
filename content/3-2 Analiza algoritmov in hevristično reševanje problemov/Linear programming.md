### Linear programs (LPs)
Linear program defines: variables $x_i$, objective and its constraints

>[!example] Example
>Determine the optimum product mix that maximizes the daily profit.
>![[Linear programming-Image-1.png|400]]
>Daily demand for exterior paint cannot exceed that of exterior paint by more than 1 ton.
>The maximum daily demand for interior paint is 2 tons.
>
>Variables:
>- $x_1$ ... amount of exterior paint produced
>- $x_2$ ... amount of interior paint produced
>
>Constraints:
>- $6x_1+4x_2\leq24$
>- $x_1+2x_2\leq6$
>- $x_2\leq x_1+1\ \rightarrow\ -x_1+x_2\leq1$
>- $x_2\leq2$
>- $x_1,x_2\geq0$
> 
> Objective: maximize profit $z=5x_1+4x_2$
> 
> 1. Graphical approach
>    a. Find feasable solution space![[Linear programming-Image-2.png|300]]
>    b. Find optimum![[Linear programming-Image-3.png|300]]
> 2. Matrix calculations ($x_i\geq0$)
> $$
> \begin{bmatrix} 6 & 4 \\ 1 & 2 \\ -1 & 1 \\ 0 & 1 \end{bmatrix}\begin{bmatrix} x_1 \\ x_2 \end{bmatrix} \leq \begin{bmatrix} 24 \\ 6 \\ 1 \\ 2 \end{bmatrix}
> $$

==Matrix form==: $Ax\leq b$, $x\geq0$ $\rightarrow$ maximize $c^Tx$
==Standard form==:
1. objective function is maximization instead of minimization $\rightarrow$ multiply with $-1$
2. all variables have non-negativity constraintes $\rightarrow$ replace single variable $x_2$ with $x_2'-x_2''$ and have non-negativity constraints for both of those
3. turn equality constraintes into inequality constraints $\rightarrow$ replace $=$ with $\leq$ and $\geq$ constraints
4. turn $\geq$ constraints into $\leq$ constraints $\rightarrow$ multiply with $-1$

>[!example] Example
>Minimize $-2x_1+3x_2$
>subject to:
>- $x_1+x_2=7$
>- $x_1-2x_2\leq4$
>- $x_1\geq0$
>
>Transformations:
>1. Maximize $2x_1-3x_2$
>2. $x_2=x_2'-x_2''\ \rightarrow\ x_2',x_2''\geq0$
>3. $x_1+x_2=7\ \rightarrow\ x_1+x_2'-x_2''\leq7$, $x_1+x_2'-x_2''\geq7$
>4. $x_1+x_2'-x_2''\geq7\ \rightarrow\ -x_1-x_2'+x_2''\leq-7$
>
>Final solution:
>Maximize $2x_1-3x_2$
>subject to:
>- $x_1+x_2'-x_2''\leq7$
>- $-x_1-x_2'+x_2''\leq-7$
>- $x_1-2x_2\leq4$
>- $x_1,x_2',x_2''\geq0$
### Convert problems to LPs
- Single-source shortest path
- Maximum flow
- Minimum-cost flow
- Multicommodity flow
### Approximation algorithms with LP
Weighted vertex cover