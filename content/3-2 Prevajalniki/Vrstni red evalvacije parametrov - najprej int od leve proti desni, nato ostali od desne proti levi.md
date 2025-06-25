## Instructions
Brez spremembe interpreterja spremenite svoj prevajalnik tako, da se pri klicu podprograma najprej izračunajo argumenti tipa int od leve proti desni, potem pa vsi ostali argumenti od desne proti levi.
## Test
```
fun putint(c: int): void  
fun putchar(c: char): void  
fun puts(s: ^char): void  
  
fun f(c: int): int =  
    putint(c),  
    putchar('\0x0A'),  
    return c  
  
fun g(d: char): char =  
    putchar(d),  
    putchar('\0x0A'),  
    return d  
  
fun h(c1: int, d1: char, c2: int, d2: char, c3: int, d3: char, c4: int): void =  
    putchar('\0x0A'),  
    puts("Parameters:"), putchar('\0x0A'),  
    putint(c1),  
    putchar('\0x0A'),  
    putchar(d1),  
    putchar('\0x0A'),  
    putint(c2),  
    putchar('\0x0A'),  
    putchar(d2),  
    putchar('\0x0A'),  
    putint(c3),  
    putchar('\0x0A'),  
    putchar(d3),  
    putchar('\0x0A'),  
    putint(c4)  
  
fun main(): int =  
    puts("Argument evaluation:"), putchar('\0x0A'),  
    h(f(1), g('c'), f(2), g('b'), f(3), g('a'), f(4)),  
    return 0
```
### Out
#### Before
```
Argument evaluation:
1
c
2
b
3
a
4

Parameters:
1
c
2
b
3
a
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
1
4
3
2
```
## Code
#### /imclin/LinearizeImc.java
```java
public class LinearizeImc implements IMC.FullVisitor<IMC.Expr, LinearizeImc.Info> {
    // ... other code ...

    @Override
    public IMC.Expr visit(IMC.CALL call, Info info) {
        info.allowCall = false;

        // ... other code ...
        
// --- CHANGED ---
        // Arguments: first, then from last to second
		evaluatedArgs[0] = call.args.get(1).accept(this, info);  
		for (int i = argsCount; i > 1; i--) {  
		    evaluatedArgs[i-1] = call.args.get(i).accept(this, info);  
		}
		
		// ... other code ...
    }

    // ... other code ...
}
```