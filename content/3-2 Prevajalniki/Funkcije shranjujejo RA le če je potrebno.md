## Instructions
Brez spremembe interpreterja spremenite svoj prevajalnik tako, da funkcija shrani povratni naslov le, če je to res potrebno.
## Test
```
fun putint(c: int): void
fun putchar(c: char): void
fun puts(s: ^char): void

fun leaf(): int =
    return 0

fun nonLeaf(): int =
    return leaf()

fun main(): int =
    return leaf()
```
### Out
Glej asm
## Code
#### /memory/MEM.java
```java
public class MEM {
    // ... other code ...
    public static class Frame {
        // ... other code ...
        public final boolean isLeaf;
	// ... other code ...
        public Frame(Label label, long depth, long locsSize, long argsSize, long size, boolean isLeaf) {
            this.label = label;
            this.depth = depth;
            this.locsSize = locsSize;
            this.argsSize = argsSize;
            this.size = size;
// --- ADDED: Store leaf property ---
            this.isLeaf = isLeaf;
            this.FP = new Temp();
            this.RV = new Temp();
        }
        // ... other code ...
    }
}
```
#### /memory/MemEvaluator.java
```java
public class MemEvaluator implements AST.FullVisitor<Object, MemEvaluator.Info> {
    // ... other code ...
    private static class Info {
        // ... other code ...
// --- ADDED: Track if current function is a leaf ---
        private boolean isLeaf;
        // ... other code ...
        public Info() {
            // ... other code ...
// --- ADDED: Initialize isLeaf ---
            isLeaf = false;
            // ... other code ...
        }
    }
    // ... other code ...

    @Override
    public Object visit(AST.DefFunDefn defFunDefn, Info info) {
        long previousLocalsSize = info.localsSize; info.localsSize = 0L;
        long previousArgsSize = info.argsSize; info.argsSize = 0L;
// --- ADDED: Assume leaf at start ---
        boolean previousIsLeaf = info.isLeaf; info.isLeaf = true;

        defFunDefn.type.accept(this, info);

        long previousOffset = info.offset; info.offset = 0L;
        long previousDepth = info.depth; info.depth = Memory.frames.size();
        defFunDefn.pars.accept(this, info);
        defFunDefn.stmts.accept(this, info);
        info.offset = previousOffset;
        info.depth = previousDepth;

        long frameSize = info.localsSize + info.argsSize + 8L + 8L;

        MEM.Label frameLabel = info.depth == 0 ? new MEM.Label(defFunDefn.name) : new MEM.Label();
        MEM.Frame frame = new MEM.Frame(frameLabel, info.depth, info.localsSize, info.argsSize, frameSize, info.isLeaf);
// --- DEBUG: Print leaf status ---
        System.out.println("DEBUG: " + defFunDefn.name + " isLeaf: " + info.isLeaf);
        Memory.frames.put(defFunDefn, frame);

        info.offset = previousOffset;
        info.localsSize = previousLocalsSize;
        info.argsSize = previousArgsSize;
// --- RESTORE: Previous isLeaf state ---
        info.isLeaf = previousIsLeaf;

        return null;
    }

    // ... other code ...

    @Override
    public Object visit(AST.CallExpr callExpr, Info info) {
// --- ADDED: Any call means function is not a leaf ---
        info.isLeaf = false;
        callExpr.funExpr.accept(this, info);
        callExpr.argExprs.accept(this, info);
        return null;
    }
}
```
#### /asmdump/AsmDump.java
```java
// ... other code ...
long raOffset = codeChunk.frame.locsSize + 16;
String saveReturnAddress = ASM.SD_INSTR
    .replace("$s0", "ra")
    .replace("$offset", Long.toString(-raOffset))
    .replace("$s1", "sp");

// --- ADDED: Do not save return address for leaf functions ---
if (codeChunk.frame.isLeaf) saveReturnAddress = "";

// ... other code ...

String restoreReturnAddress = ASM.LD_INSTR
    .replace("$s1", "ra")
    .replace("$offset", Long.toString(-raOffset))
    .replace("$s0", "s0");

// --- ADDED: Do not restore return address for leaf functions ---
if (codeChunk.frame.isLeaf) restoreReturnAddress = "";
```