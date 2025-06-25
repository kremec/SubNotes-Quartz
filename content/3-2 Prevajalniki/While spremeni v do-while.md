## Instructions
V jeziku LANG'24 nadomestimo pravili za izvajanje while zanke s praviloma
$$
\frac{[\![stmt]\!]^{M'}_{STMT} = M'' \quad [\![expr]\!]^{M}_{EXPR} = (true, M')}
{[\![while\ expr : stmt]\!]^{M}_{STMT} = [\![while\ expr : stmt]\!]^{M''}_{STMT}}
$$
$$
\frac{[\![expr]\!]^{M}_{EXPR} = (false, M')}
{[\![while\ expr : stmt]\!]^{M}_{STMT} = M'}
$$
Spremenite prevajalnik, da upošteva ti dve pravili.
## Test
```
fun putint(c: int): void
fun putchar(c: char): void

var x: int

fun main(): int =
	x = 5,
    while
	    x < 5
	do
		putint(x),
		putchar('\0x0A'),
		x = x - 1
	end,
	return 0
```
### Out
#### Before
```
```
#### After
```
```
## Code
#### /imcgen/ImcGenerator.java
```java
public class ImcGenerator implements AST.FullVisitor<IMC.Instr, ImcGenerator.Info> {
    // ... other code ...

    @Override
    public IMC.Instr visit(AST.WhileStmt whileStmt, Info info) {
        IMC.Expr condExprImc = (IMC.Expr) whileStmt.condExpr.accept(this, info);

        Vector<IMC.Stmt> whileStmtsVector = new Vector<>();
        for (AST.Stmt stmt : whileStmt.stmts) {
            IMC.Stmt stmtImc = (IMC.Stmt) stmt.accept(this, info);
            whileStmtsVector.add(stmtImc);
        }
        IMC.Stmt whileStmtsImc = new IMC.STMTS(whileStmtsVector);

        IMC.LABEL posLabel = new IMC.LABEL(new MEM.Label());
        IMC.NAME posLabelName = new IMC.NAME(posLabel.label);
        IMC.LABEL endLabel = new IMC.LABEL(new MEM.Label());
        IMC.NAME endLabelName = new IMC.NAME(endLabel.label);
        IMC.CJUMP imcCJump = new IMC.CJUMP(
                condExprImc,
                posLabelName,
                endLabelName
        );
        Vector<IMC.Stmt> stmtsVector = new Vector<>();
        stmtsVector.add(posLabel);
        stmtsVector.add(whileStmtsImc);
        stmtsVector.add(imcCJump);
        stmtsVector.add(endLabel);

        IMC.STMTS imcStmt = new IMC.STMTS(stmtsVector);
        ImcGen.stmt.put(whileStmt, imcStmt);
        return imcStmt;
    }

    // ... other code ...
}
```