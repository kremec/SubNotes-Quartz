## Instructions
V prevajalnik dodajte pravilo, da se v nobenem izrazu (in s tem seveda v njegovih podizrazih) ne smeta hkrati pojaviti operatorja + in -.
## Test
```
var x: int

fun main(): int =
	x = 1+2+(-2),
	x = 1+2-2
```
### Out
#### Before
No error
#### After
Error
## Code
#### /seman/TypeChecker.java
```java
public class TypeChecker implements AST.FullVisitor<TYP.Type, TypeChecker.Info> {
    public static class Info {
        public AST.FunDefn parentFunDefn;

// --- ADDED: Track usage of plus and minus in expressions ---
        public boolean usedPlus = false;
        public boolean usedMinus = false;

        public Info() {
            parentFunDefn = null;
        }
    }

    // ... other code ...

    // ----- Statements -----
    @Override
    public TYP.Type visit(AST.AssignStmt assignStmt, Info info) {
// --- ADDED: Save and reset plus/minus usage before visiting sub-expressions ---
        boolean previousUsedPlus = info.usedPlus; info.usedPlus = false;
        boolean previousUsedMinus = info.usedMinus; info.usedMinus = false;
        assignStmt.dstExpr.accept(this, info);
        info.usedPlus = previousUsedPlus; info.usedMinus = previousUsedMinus;

        info.usedPlus = false;
        info.usedMinus = false;
        assignStmt.srcExpr.accept(this, info);
        info.usedPlus = previousUsedPlus; info.usedMinus = previousUsedMinus;
// --- END ADDED ---

        TYP.Type dstExprType = SemAn.ofType.get(assignStmt.dstExpr);
        TYP.Type srcExprType = SemAn.ofType.get(assignStmt.srcExpr);

        if (!typeEqu(dstExprType, srcExprType))
            throw new Report.Error(assignStmt, "TypeChecker error: Assignment types do not match");

        return null;
    }

    @Override
    public TYP.Type visit(AST.ReturnStmt returnStmt, Info info) {
// --- ADDED: Save and reset plus/minus usage before visiting sub-expressions ---
        boolean previousUsedPlus = info.usedPlus; info.usedPlus = false;
        boolean previousUsedMinus = info.usedMinus; info.usedMinus = false;
        returnStmt.retExpr.accept(this, info);
        info.usedPlus = previousUsedPlus; info.usedMinus = previousUsedMinus;
// --- END ADDED ---

        if (info.parentFunDefn == null)
            throw new Report.Error(returnStmt, "TypeChecker error: Return statement not inside a function");

        TYP.Type retType = SemAn.ofType.get(returnStmt.retExpr);
        TYP.Type funType = SemAn.ofType.get(info.parentFunDefn.type);

        if (!typeEqu(retType, funType))
            throw new Report.Error(returnStmt, "TypeChecker error: Return type does not match function type");

        return null;
    }

    @Override
    public TYP.Type visit(AST.WhileStmt whileStmt, Info info) {
// --- ADDED: Save and reset plus/minus usage before visiting sub-expressions ---
        boolean previousUsedPlus = info.usedPlus; info.usedPlus = false;
        boolean previousUsedMinus = info.usedMinus; info.usedMinus = false;
        whileStmt.condExpr.accept(this, info);
        info.usedPlus = previousUsedPlus; info.usedMinus = previousUsedMinus;
// --- END ADDED ---

        whileStmt.stmts.accept(this, info);

        TYP.Type condType = SemAn.ofType.get(whileStmt.condExpr);
        if (!typeEqu(condType, TYP.BoolType.type))
            throw new Report.Error(whileStmt, "TypeChecker error: While condition must be boolean");

        return null;
    }

    @Override
    public TYP.Type visit(AST.IfThenStmt ifThenStmt, Info info) {
// --- ADDED: Save and reset plus/minus usage before visiting sub-expressions ---
        boolean previousUsedPlus = info.usedPlus; info.usedPlus = false;
        boolean previousUsedMinus = info.usedMinus; info.usedMinus = false;
        ifThenStmt.condExpr.accept(this, info);
        info.usedPlus = previousUsedPlus; info.usedMinus = previousUsedMinus;
// --- END ADDED ---

        ifThenStmt.thenStmt.accept(this, info);

        TYP.Type condType = SemAn.ofType.get(ifThenStmt.condExpr);
        if (!typeEqu(condType, TYP.BoolType.type))
            throw new Report.Error(ifThenStmt, "TypeChecker error: If condition must be boolean");

        return null;
    }

    @Override
    public TYP.Type visit(AST.IfThenElseStmt ifThenElseStmt, Info info) {
// --- ADDED: Save and reset plus/minus usage before visiting sub-expressions ---
        boolean previousUsedPlus = info.usedPlus; info.usedPlus = false;
        boolean previousUsedMinus = info.usedMinus; info.usedMinus = false;
        ifThenElseStmt.condExpr.accept(this, info);
        info.usedPlus = previousUsedPlus; info.usedMinus = previousUsedMinus;
// --- END ADDED ---

        ifThenElseStmt.thenStmt.accept(this, info);
        ifThenElseStmt.elseStmt.accept(this, info);

        TYP.Type condType = SemAn.ofType.get(ifThenElseStmt.condExpr);
        if (!typeEqu(condType, TYP.BoolType.type))
            throw new Report.Error(ifThenElseStmt, "TypeChecker error: If condition must be boolean");

        return null;
    }

    // ... other code ...

    @Override
    public TYP.Type visit(AST.PfxExpr pfxExpr, Info info) {
        TYP.Type subExprType = pfxExpr.subExpr.accept(this, info);

        if (pfxExpr.oper == AST.PfxExpr.Oper.ADD || pfxExpr.oper == AST.PfxExpr.Oper.SUB) {
            if (!typeEqu(subExprType, TYP.IntType.type))
                throw new Report.Error(pfxExpr, "TypeChecker error: Only integer expression is allowed here");

// --- ADDED: Track plus/minus usage and disallow both in same expression ---
            if (pfxExpr.oper == AST.PfxExpr.Oper.ADD) {
                info.usedPlus = true;
                if (info.usedMinus)
                    throw new Report.Error(pfxExpr, "TypeChecker error: Plus and minus not allowed in same expression");
            }
            else {
                info.usedMinus = true;
                if (info.usedPlus)
                    throw new Report.Error(pfxExpr, "TypeChecker error: Plus and minus not allowed in same expression");
            }
// --- END ADDED ---

            SemAn.ofType.put(pfxExpr, subExprType);
            SemAn.isConst.put(pfxExpr, SemAn.isConst.get(pfxExpr.subExpr));
        } else if (pfxExpr.oper == AST.PfxExpr.Oper.NOT) {
            // ... existing code ...
        }
        // ... existing code ...
    }

    // ... other code ...

    @Override
    public TYP.Type visit(AST.BinExpr binExpr, Info info) {
        // ... existing code ...
        if (binExpr.oper == AST.BinExpr.Oper.ADD || binExpr.oper == AST.BinExpr.Oper.SUB) {
            // ... existing code ...

// --- ADDED: Track plus/minus usage and disallow both in same expression ---
            if (binExpr.oper == AST.BinExpr.Oper.ADD) {
                info.usedPlus = true;
                if (info.usedMinus)
                    throw new Report.Error(binExpr, "TypeChecker error: Plus and minus not allowed in same expression");
            }
            else {
                info.usedMinus = true;
                if (info.usedPlus)
                    throw new Report.Error(binExpr, "TypeChecker error: Plus and minus not allowed in same expression");
            }
// --- END ADDED ---

            if (sndIntoFstCoercible)
                SemAn.ofType.put(binExpr, fstExprType);
            else SemAn.ofType.put(binExpr, sndExprType);
        }
        // ... existing code ...
    }

    // ... other code ...
}
```