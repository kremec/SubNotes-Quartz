### SIC/XE
**Kaj so prednosti XE pred sic, katerih programov ne moramo napisati v SIC?**

**Napiši SIC program wc, ki bere besede iz standardnega vhoda, jih presteje in izpiše na standardni izhod. Besede so ločene natanko z enim presledkom. Beri vhod dokler ne prebereš 0. Vseh besed je manj kot 10.**

**Napiši SIC/XE program, ki bere bajte iz standardnega vhoda, dokler ne prebere 0. Potem to izpisuje v obratnem vrstnem redu. Lahko uporabljaš rutine za delo s skladom iz vaj, ni pa treba.**

**Napiši SIC/XE program, ki se prevede v kodo:**
```bytecode
Hanswer000000012346
T0000000C 010006 690009 9830 2B112345
T01234501 42
M00000905
E000000
```

```asm
answer START 0
    LDA #6
    LDB #9
    MULR B,A
    +COMP 0x12345
    
    RESB 0x12345-0x0C

    AND ???
```

**Napiši program FizzBuzz v SIC/XE**

### Zbirnik / povezovalnik / nalagalnik
**Kaj je pc relativno naslavljanje**
**Kdo in kdaj se odloči za pc rel. naslavljanje**
**Kako se izračuna operand za pc. rel.?**
**Kaj je prenaslavljanje?**
**Kje se uporablja?**

**Kaj so programski bloki?**
**Kako so zapisani v kodi?**
**Kdaj se jih uporabi (zbirnik/povezovalnik/nalagalnik) in kako?**

**Kaj je CSTAB in zakaj se uporablja?**
**Katere stolpce ima tabela CSTAB?**
**Kdaj se jo uporabi in kako?**
### Java
**Enostavno razloži, zakaj JVM ne uporablja registrov**

**Napiši zložno kodo, ki se prevede iz programa**
```java
static int sestej(int x) {
    int a = x + 3;
    return a;
}
```

**Napiši funkcijo v javi ki sprejme 2 parametra in se prevede v:**
```java-bytecode
iload_0
i2l
lload_1
ladd
lconst_1
ladd
lstore_3
lload_3
lreturn
```
```java
long test(int a, long b) {
    long c = (long)a + b + 1;
    return c
}
```