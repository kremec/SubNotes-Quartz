## Instructions
V jeziku LANG'24 uvedemo pravilo, po katerem prva komponenta unije, če in samo če je dejanskega tipa int, ni prekrita z ostalimi komponentami. Dodajte to pravilo v prevajalnik.
## Test
```
fun putint(c: int): void
fun putchar(c: char): void

var union1: { comp1: int, comp2: int }
var union2: { comp1: char, comp2: int }

fun main(): int =
    union1.comp1 = 1,
    union1.comp2 = 2,
    union2.comp1 = 'a',
    union2.comp2 = 98,
    putint(union1.comp1),
    putchar('\0x0A'),
    putint(union1.comp2),
    putchar('\0x0A'),
    putchar(union2.comp1),
    putchar('\0x0A'),
    putint(union2.comp2),
    return 0
```
### Out
#### Before
```
2
2
b
98
```
#### After
```
1
2
b
98
```
## Code
#### /memory/MemEvaluator.java
```java
public class MemEvaluator implements AST.FullVisitor<Object, MemEvaluator.Info> {
    // ... other code ...

    private static class Info {
        private long depth;
        private long offset;

        private boolean inUnion;
// --- ADDED: Track first component in union ---
        private boolean firstInUnion;

        private Long localsSize;
        private Long argsSize;

        public Info() {
            depth = 0;
            offset = 0;

            inUnion = false;
// --- ADDED: Initialize firstInUnion ---
            firstInUnion = false;

            localsSize = 0L;
            argsSize = 0L;
        }
    }

    // ... other code ...

    @Override
    public Object visit(AST.CompDefn compDefn, Info info) {
        long previousDepth = info.depth; info.depth = -1;

        compDefn.type.accept(this, info);

        TYP.Type type = compDefn.type.type;
        Long size = type.accept(sizeEvaluator, null);

        MEM.Access access = new MEM.RelAccess(size, info.offset, info.depth);
// --- CHANGED: Only increment offset for first int in union, or if not in union ---
        if (!info.inUnion || (info.firstInUnion && type instanceof TYP.IntType))
            info.offset = positiveOffset(info.offset, size);

        Memory.accesses.put(compDefn, access);

// --- ADDED: Reset after first union component ---
        info.firstInUnion = false;
        info.depth = previousDepth;
        return null;
    }

    // ... other code ...

    @Override
    public Object visit(AST.UniType uniType, Info info) {
        boolean previousInUnion = info.inUnion; info.inUnion = true;
// --- ADDED: Track first in union ---
        boolean previousFirstInUnion = info.firstInUnion; info.firstInUnion = true;
        long previousOffset = info.offset; info.offset = 0L;

        uniType.comps.accept(this, info);

        info.inUnion = previousInUnion;
// --- ADDED: Restore previous state ---
        info.firstInUnion = previousFirstInUnion;
        info.offset = previousOffset;
        return null;
    }
}
```
#### /memory/SizeEvaluator.java
```java
public class SizeEvaluator extends TYP.FullVisitor<Long, Object> {
    // ... other code ...

    @Override
    public Long visit(TYP.UniType uniType, Object arg) {
// --- ADDED: Track size of first int component ---
        long startingIntSize = 0L;
        long size = 0L;
        for (int i = 0; i < uniType.compTypes.size(); i++) {
            TYP.Type compType = uniType.compTypes.get(i);
            final long compSize = compType.accept(this, arg);
// --- ADDED: Special handling for first int ---
            if (i == 0 && compType instanceof TYP.IntType) {
                startingIntSize += compSize;
            } else {
                size = Long.max(size, (compSize / 8L) * 8L + (compSize % 8L == 0 ? 0L : 8L));
            }
        }
// --- ADDED: Combine sizes ---
        return size + startingIntSize;
    }

    // ... other code ...
}
```