## Instructions
V jeziku LANG'24 uvedemo pravilo, po katerem nobena funkcija v nobenem trenutku izvajanja programa ne sme biti klicana več kot desetkrat (a če je recimo klicana osemkrat in se vsi klici zaključijo, sme biti spet klicana dvakrat). V primeru, ko je pravilo kršeno, naj se izvajanje programa takoj konča. Dodajte to pravilo v prevajalnik.
## Test
```
fun putint(c: int): void
fun putchar(c: char): void
fun puts(s: ^char): void

fun rec(x: int): int =
	putint(x),
	putchar('\0x0A'),
    if
	    x < 1
	then
		return 1
	end,
	return rec(x-1)

fun main(): int =
    puts("Testing 5"),
    putchar('\0x0A'),
    rec(5),
    puts("Testing 9"),
    putchar('\0x0A'),
    rec(9),
    puts("Testing 10"),
    putchar('\0x0A'),
    rec(10),
    puts("Testing 11"),
    putchar('\0x0A'),
    rec(11)
```
### Out
#### Before
```

```
#### After
```

```
## Code
#### /imclin/ChunkGenerator.java
```java
public class ChunkGenerator implements AST.FullVisitor<IMC.Instr, ChunkGenerator.Info> {
    // ... other code ...

    @Override
    public IMC.Instr visit(AST.FunDefn defFunDefn, Info info) {
        // ... other code ...
        defFunDefn.stmts.accept(this, info);

        Vector<IMC.Stmt> stmts = new Vector<>();

// --- ADDED: Function counter logic ---
        MEM.Label funCounterLabel = new MEM.Label(defFunDefn.name + "_counter");
        for (IMC.Stmt stmtImc : funCounterStmts(funCounterLabel)) {
            Vector<IMC.Stmt> linearizedImcStmts = new Vector<>();
            stmtImc.accept(new LinearizeImc(), new LinearizeImc.Info(linearizedImcStmts));
            stmts.addAll(linearizedImcStmts);
        }
// --- END ADDED ---

        for (AST.Stmt stmtAst : defFunDefn.stmts) {
            IMC.Stmt stmtImc = ImcGen.stmt.get(stmtAst);
            Vector<IMC.Stmt> linearizedImcStmts = new Vector<>();
            stmtImc.accept(new LinearizeImc(), new LinearizeImc.Info(linearizedImcStmts));
            stmts.addAll(linearizedImcStmts);
        }

        stmts.addFirst(new IMC.LABEL(entryLabel));
        stmts.addLast(new IMC.LABEL(exitLabel));

// --- ADDED: Decrement function counter at function exit ---
        stmts.add(new IMC.MOVE(
            new IMC.MEM8(new IMC.NAME(funCounterLabel)),
            new IMC.BINOP(IMC.BINOP.Oper.SUB,
                new IMC.MEM8(new IMC.NAME(funCounterLabel)),
                new IMC.CONST(1)
            )
        ));
// --- END ADDED ---

// --- ADDED: New exit label ---
        MEM.Label newExitLabel = new MEM.Label(defFunDefn.name + "_exit");
        stmts.addLast(new IMC.LABEL(newExitLabel));
// --- END ADDED ---

        LIN.CodeChunk codeChunk = new LIN.CodeChunk(
            Memory.frames.get(defFunDefn),
            stmts,
            entryLabel,
            newExitLabel // CHANGED: use new exit label
        );
        ImcLin.addCodeChunk(codeChunk);

        return null;
    }

// --- ADDED: Function counter statements ---
    private List<IMC.Stmt> funCounterStmts(MEM.Label funCounterLabel) {
        List<IMC.Stmt> stmts = new ArrayList<>();
        byte[] funCounterInit = new byte[8];
        MEM.AbsAccess funCounterAccess = new MEM.AbsAccess(8L, funCounterLabel, "0", funCounterInit);
        ImcLin.addDataChunk(new LIN.DataChunk(funCounterAccess));

        MEM.Label exitProgramLabel = new MEM.Label();
        MEM.Label continueProgramLabel = new MEM.Label();

        // Increment function counter
        stmts.add(new IMC.MOVE(
            new IMC.MEM8(new IMC.NAME(funCounterLabel)),
            new IMC.BINOP(IMC.BINOP.Oper.ADD,
                new IMC.MEM8(new IMC.NAME(funCounterLabel)),
                new IMC.CONST(1)
            )
        ));
        // If counter <= 10, continue; else, call die
        stmts.add(new IMC.CJUMP(
            new IMC.BINOP(IMC.BINOP.Oper.LEQ,
                new IMC.MEM8(new IMC.NAME(funCounterLabel)),
                new IMC.CONST(10L)
            ),
            new IMC.NAME(continueProgramLabel),
            new IMC.NAME(exitProgramLabel)
        ));

        stmts.add(new IMC.LABEL(exitProgramLabel));
        stmts.add(new IMC.ESTMT(
            new IMC.CALL(
                new IMC.NAME(new MEM.Label("die")),
                new Vector<>(),
                new Vector<>()
            )
        ));

        stmts.add(new IMC.LABEL(continueProgramLabel));

        return stmts;
    }
// --- END ADDED ---
}
```