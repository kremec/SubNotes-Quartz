## Instructions
V jeziku LANG'24 nadomestimo pravilo za klic funkcije s pravilom
$$
\begin{align*}
&[\![expr_{m-1}]\!]^{M_0}_{EXPR} = \langle n_{m-1}, M_1 \rangle\ \ \ \ ...\ \quad [\![expr]\!]^{M_{m-2}}_{EXPR} = \langle n_1, M_{m-1} \rangle \\
&[\![expr_m]\!]^{M_{m-1}}_{EXPR} = \langle n_m, M_m \rangle \\
&\frac{}{identifier(expr_1, \ldots, expr_m)^{M_0}_{EXPR} = \langle identifier(n_1, \ldots, n_m), M_m \rangle}
\end{align*}
$$
Spremenite prevajalnik, da upošteva to pravilo.
## Test
```
fun putint(c: int): void  
fun putchar(c: char): void  
fun puts(s: ^char): void  
  
fun f(c: int): int =  
    putint(c),  
    putchar('\0x0A'),  
    return c  
  
fun g(c1: int, c2: int, c3: int, c4: int): void =  
    putchar('\0x0A'),  
    puts("Parameters:"), putchar('\0x0A'),  
    putint(c1),  
    putchar('\0x0A'),  
    putint(c2),  
    putchar('\0x0A'),  
    putint(c3),  
    putchar('\0x0A'),  
    putint(c4)  
  
fun main(): int =  
    puts("Argument evaluation:"), putchar('\0x0A'),  
    g(f(3), f(2), f(1), f(4)),  
    return 0
```
### Out
#### Before
```
Argument evaluation:
3
2
1
4

Parameters:
3
2
1
4
```
#### After
```
Argument evaluation:
1
2
3
4

Parameters:
3
2
1
4
```
## Code
```java
public class LinearizeImc implements IMC.FullVisitor<IMC.Expr, LinearizeImc.Info> {
    // ... other code ...

    @Override
    public IMC.Expr visit(IMC.CALL call, Info info) {
        info.allowCall = false;

		// ... other code ...
        
// --- CHANGED ---
		// Arguments: from second-to-last to first, then last  
		for (int i = argsCount-1; i > 0; i--) {  
		    evaluatedArgs[i-1] = call.args.get(i).accept(this, info);  
		}  
		if (argsCount > 0)  
		    evaluatedArgs[argsCount-1] = call.args.get(argsCount).accept(this, info);
			
		// ... other code ...
	}

	    // ... other code ...
}
```