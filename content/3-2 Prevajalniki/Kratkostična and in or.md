## Instructions
Spremenite prevajalnik tako, da za operatorja or in and v pogojui if ali while stavka velja kratkostični izračun, torej
$$
x \text{ or } y = 
\begin{cases}
\text{true} & x = \text{true} \\
y & \text{sicer}
\end{cases}
\qquad
x \text{ and } y = 
\begin{cases}
\text{false} & x = \text{false} \\
y & \text{sicer}
\end{cases}
$$
Z drugimi besedami, če se da rezultat operacije ugotoviti samo na osnovi vrednosti levega operanda, se vrednosti desnega operanda ne računa. Če sta tovrstna operatorja uporabljena drugje, zanje velja običajni način izračuna.
## Test
```
fun puts(s: ^char): void
fun putchar(c: char): void

fun returnTrue(): bool =
	puts("True"),
	putchar('\0x0A'),
	return true

fun returnFalse(): bool =
	puts("False"),
	putchar('\0x0A'),
	return false

fun main(): int =
	if
		returnTrue() | returnTrue()
	then
		return 0
	end,
	return 1
```
### Out
#### Before
```
```
#### After
```
```
## Code
#### /imclin/LinearizeImc.java
```java
public class LinearizeImc implements IMC.FullVisitor<IMC.Expr, LinearizeImc.Info> {
    // ... other code ...

    @Override
    public IMC.Expr visit(IMC.CJUMP cjump, Info info) {
        info.allowCall = false;

        IMC.Expr linearizedPosAddr = cjump.posAddr.accept(this, info);
        IMC.Expr linearizedNegAddr = cjump.negAddr.accept(this, info);

// --- CHANGED: Special handling for short-circuit AND/OR in CJUMP ---
        if (cjump.cond instanceof IMC.BINOP condBinop && condBinop.oper == IMC.BINOP.Oper.AND) {
            // Short-circuit AND: if first is false, jump to neg; if true, check second
            IMC.Expr linearizedCondFst = condBinop.fstExpr.accept(this, info);

            MEM.Label fstFalse = new MEM.Label();
            MEM.Label fstTrue = new MEM.Label();
            info.linearizedImcStmts.addLast(
                new IMC.CJUMP(linearizedCondFst, new IMC.NAME(fstTrue), new IMC.NAME(fstFalse))
            );

            info.linearizedImcStmts.addLast(new IMC.LABEL(fstFalse));
            info.linearizedImcStmts.addLast(new IMC.JUMP(linearizedNegAddr));

            info.linearizedImcStmts.addLast(new IMC.LABEL(fstTrue));
            IMC.Expr linearizedCondSnd = condBinop.sndExpr.accept(this, info);
            info.linearizedImcStmts.addLast(new IMC.CJUMP(linearizedCondSnd, linearizedPosAddr, linearizedNegAddr));
        }
        else if (cjump.cond instanceof IMC.BINOP condBinop && condBinop.oper == IMC.BINOP.Oper.OR) {
            // Short-circuit OR: if first is true, jump to pos; if false, check second
            IMC.Expr linearizedCondFst = condBinop.fstExpr.accept(this, info);

            MEM.Label fstFalse = new MEM.Label();
            MEM.Label fstTrue = new MEM.Label();
            info.linearizedImcStmts.addLast(
                new IMC.CJUMP(linearizedCondFst, new IMC.NAME(fstTrue), new IMC.NAME(fstFalse))
            );

            info.linearizedImcStmts.addLast(new IMC.LABEL(fstFalse));
            IMC.Expr linearizedCondSnd = condBinop.sndExpr.accept(this, info);
            info.linearizedImcStmts.addLast(new IMC.CJUMP(linearizedCondSnd, linearizedPosAddr, linearizedNegAddr));

            info.linearizedImcStmts.addLast(new IMC.LABEL(fstTrue));
            info.linearizedImcStmts.addLast(new IMC.JUMP(linearizedNegAddr));
        }
        else {
// --- DEFAULT: Standard CJUMP linearization ---
            IMC.Expr linearizedCond = cjump.cond.accept(this, info);

            MEM.Label newNegLabel = new MEM.Label();
            info.linearizedImcStmts.addLast(new IMC.CJUMP(linearizedCond, linearizedPosAddr, new IMC.NAME(newNegLabel)));
            info.linearizedImcStmts.addLast(new IMC.LABEL(newNegLabel));
        }
// --- END CHANGED ---

        info.linearizedImcStmts.addLast(new IMC.JUMP(linearizedNegAddr));
        return null;
    }

    // ... other code ...
}
```