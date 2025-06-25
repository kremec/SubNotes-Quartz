## Instructions
V jezik LANG'24 dodamo omejitev, da ime podatkovnega tipa ne sme nikoli zakriti imena, ki je definirano v zunanjm dosegu. Z drugimi besedami, podatkovni tip lahko definiramo le, če njegovo ime še ni definirano v trenutnem dosegu ali v katerem od zunanjih dosegov. Dodajte to pravilo v prevajalnik.
## Test
```
typ a = int

fun main(): int =
    let
	    typ a = bool
	    typ b = int
	in
		return 0
	end,
	let
		typ b = int
	in
		return 0
	end
```
### Out
#### Before
Ni napake
#### After
Prevajalnik javi napako
## Code
#### /seman/NameResolver.java
```java
public class NameResolver implements AST.FullVisitor<Object, NameResolver.Mode> {
    // ... other code ...

    public static class SymbTable {
        // ... other code ...

        public void ins(String name, AST.Defn defn)
                throws CannotInsNameException, CannotInsTypeException {
            if (lock)
                throw new Report.InternalError();

            LinkedList<ScopedDefn> allDefnsOfName = defns.get(name);
            if (allDefnsOfName != null && !allDefnsOfName.isEmpty()) {
                ScopedDefn defnOfName = allDefnsOfName.getFirst();
                if (defnOfName.depth == currDepth)
                    throw new CannotInsNameException();

// --- ADDED: Prevent overshadowing a type definition with the same name ---
                if (defnOfName.defn instanceof AST.TypDefn
                        && defnOfName.defn.name.equals(name))
                    throw new CannotInsTypeException();
            }

            allDefnsOfName.addFirst(new ScopedDefn(currDepth, defn));
        }

        // ... other code ...

        private static class CannotFndNameException extends Exception {
            private CannotFndNameException() {}
        }

// --- ADDED: Exception for type overshadowing ---
        public static class CannotInsTypeException extends Exception {
            private CannotInsTypeException() {}
        }
    }

    // ... other code ...

    private void declareSymbol(String name, AST.Defn defn) {
        try {
            symbTable.ins(name, defn);
        } catch (SymbTable.CannotInsNameException e) {
            throw new Report.Error(defn.location(),
                "NameResolver error: Cannot declare duplicate symbol: " + name);
        } catch (SymbTable.CannotInsTypeException e) {
// --- ADDED: Exception handling
            throw new Report.Error(defn.location(),
                "NameResolver error: Cannot overshadow type definition: " + name);
        }
    }

    // ... other code ...
}
```