## Instructions
Spremenite svoj prevajalnik tako, da dopušča uporabo konstante 0 namesto konstante nil (0 ima torej dva pomena: kot celoštevilska konstanta in kot kazalčna konstanta).
## Test
```
var x: int  
var p: ^int  
  
fun main(): int =  
    x = 0,  
    p = 0,  
    return 0
```
### Out
#### Before
Error
#### After
No error
## Code
#### /seman/TypeChecker.java
```java
public class TypeChecker implements AST.FullVisitor<TYP.Type, TypeChecker.Info> {
    // ... other code ...

// --- CHANGED: Add pointer coercion for integer zero ---
    private boolean coercible(TYP.Type t1, AST.Expr e1, TYP.Type t2) {
        if (t1 instanceof TYP.IntType && t2.actualType() instanceof TYP.PtrType &&
			e1 instanceof AST.AtomExpr atomE1 && atomE1.type == AST.AtomExpr.Type.INT && atomE1.value.equals("0"))
            return true;
// --- CHANGED: Added e1 to all coercible calls
        if (t1 instanceof TYP.IntType)
            return typeEqu(t2, TYP.IntType.type);
        if (t1 instanceof TYP.CharType)
            return typeEqu(t2, TYP.CharType.type);
        if (t1 instanceof TYP.BoolType)
            return typeEqu(t2, TYP.BoolType.type);
        if (t1 instanceof TYP.VoidType)
            return t2 instanceof TYP.VoidType;
        if (t1 instanceof TYP.PtrType ptrType1 && t2 instanceof TYP.PtrType ptrType2) {
            return coercible(ptrType1.baseType, e1, ptrType2.baseType);
        }
        if (t1 instanceof TYP.ArrType arrType1 && t2 instanceof TYP.ArrType arrType2) {
            return (arrType1.numElems.equals(arrType2.numElems) &&
                    coercible(arrType1.elemType, e1, arrType2.elemType));
        }
        if (t1 instanceof TYP.StrType strType1 && t2 instanceof TYP.StrType strType2) {
            return coercible(strType1.compTypes, strType2.compTypes);
        }
        if (t1 instanceof TYP.UniType uniType1 && t2 instanceof TYP.UniType uniType2) {
            return coercible(uniType1.compTypes, uniType2.compTypes);
        }
        if (t1 instanceof TYP.FunType funType1 && t2 instanceof TYP.FunType funType2) {
            return (coercible(funType1.resType, e1, funType2.resType) &&
                    coercible(funType1.parTypes, funType2.parTypes));
        }
        if (t1 instanceof TYP.NameType nameType1 && t2 instanceof TYP.NameType nameType2) {
            return (nameType1.name.equals(nameType2.name) &&
                    typeEqu(nameType1.actualType(), nameType2.actualType()));
        }
        return false;
    }

    // --- CHANGED: Update all calls to coercible to pass the expression as well ---
    @Override
    public TYP.Type visit(AST.AssignStmt assignStmt, Info info) {
        // ... other code ...
        if (!coercible(srcExprType, assignStmt.srcExpr, dstExprType))
            throw new Report.Error(assignStmt.srcExpr, "TypeChecker error: Cannot assign non-coercible types");
        // ... other code ...
    }

    @Override
    public TYP.Type visit(AST.ReturnStmt returnStmt, Info info) {
        // ... other code ...
        if (!coercible(retExprType, returnStmt.retExpr, parentFunType.resType))
            throw new Report.Error(returnStmt,
                    "TypeChecker error: Returned expression type must be coercible to function result type");
        // ... other code ...
    }

    @Override
    public TYP.Type visit(AST.BinExpr binExpr, Info info) {
        // ... other code ...
        boolean sndIntoFstCoercible = coercible(sndExprType, binExpr.sndExpr, fstExprType);
        boolean fstIntoSndCoercible = coercible(fstExprType, binExpr.fstExpr, sndExprType);
        // ... other code ...
    }

    @Override
    public TYP.Type visit(AST.CallExpr callExpr, Info info) {
        // ... other code ...
        for (int i = 0; i < funParTypes.size(); i++) {
            TYP.Type callArgExprType = SemAn.ofType.get(callExpr.argExprs.get(i));
            TYP.Type funParType = funParTypes.get(i);
            if (!coercible(callArgExprType, callExpr.argExprs.get(i), funParType))
                throw new Report.Error(callExpr.argExprs.get(i),
                        "TypeChecker error: Function parameter type and argument type do not match");
        }
        // ... other code ...
    }
}
```