## Instructions
Brez spremembe interpreterja spremenite svoj prevajalnik tako, da se pri klicu podprograma najprej izračuna skrajno levi argument, potem pa ostali argumenti od desne proti levi.
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
    g(f(1), f(4), f(3), f(2)),  
    return 0
```
### Out
#### Before
```
Argument evaluation:
1
4
3
2

Parameters:
1
4
3
2
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
#### /imcgen/IMC.java
```java
public class IMC {
    // ... other code ...
    public static class CALL extends Expr {
        public final Expr addr;
        public final Vector<Long> offs;
        public final Vector<Expr> args;
// --- ADDED: Store AST argument expressions ---
        public final AST.Nodes<AST.Expr> argExprs;

        /**
         * Constructs a function call.
         *
         * @param addr     The address of the function.
         * @param offs     The offsets of arguments.
         * @param args     The values of arguments.
         * @param argExprs The AST expressions of arguments
         */
        public CALL(Expr addr, Vector<Long> offs, Vector<Expr> args, AST.Nodes<AST.Expr> argExprs) {
            this.addr = addr;
            this.offs = new Vector<>(offs);
            this.args = new Vector<>(args);
            this.argExprs = argExprs;
        }
        // ... other code ...
    }
}
```
#### /imcgen/ImcGenerator.java
```java
public class ImcGenerator implements AST.FullVisitor<IMC.Instr, ImcGenerator.Info> {
    // ... other code ...
    @Override
    public IMC.Instr visit(AST.CallExpr callExpr, Info info) {
        // ... other code ...
// --- MODIFIED: added new parameter
        IMC.Expr imcExpr = new IMC.CALL(funExprAddrImc, argOffsets, argImcs, callExpr.argExprs);
        ImcGen.expr.put(callExpr, imcExpr);
        return imcExpr;
    }
    // ... other code ...
}
```
#### /imclin/LinearizeImc.java
```java
public class LinearizeImc implements IMC.FullVisitor<IMC.Expr, LinearizeImc.Info> {
    // ... other code ...

    @Override
    public IMC.Expr visit(IMC.CALL call, Info info) {
        info.allowCall = false;

        // ... other code ...
        
// --- CHANGED ---
        // Arguments: first all ints from left to right  
		for (int i = 0; i < argsCount; i++) {  
		    if (SemAn.ofType.get(call.argExprs.get(i)) instanceof TYP.IntType) {  
		        evaluatedArgs[i] = call.args.get(i + 1).accept(this, info);  
		    }  
		}  
		// then all others from right to left  
		for (int i = argsCount-1; i >= 0; i--) {  
		    if (!(SemAn.ofType.get(call.argExprs.get(i)) instanceof TYP.IntType)) {  
		        evaluatedArgs[i] = call.args.get(i+1).accept(this, info);  
		    }  
		}
		
		// ... other code ...
		
		info.allowCall = previousAllowCall;
// --- MODIFIED: added new parameter
        IMC.CALL callImc = new IMC.CALL(linearizedAddr, call.offs, linearizedArgs, call.argExprs);
        if (info.allowCall) {
            return callImc;
        } else {
            // ... existing code ...
        }
    }

    // ... other code ...
}
```