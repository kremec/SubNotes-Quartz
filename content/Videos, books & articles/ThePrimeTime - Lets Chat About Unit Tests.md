[VIDEO](https://youtu.be/IInciWyU74U)
___  
- You have to treat code like a black box, otherwise when you change code (while having unstable interfaces, ...), the unit tests will also have to be modified. But, having that in mind, try to avoid building the architecture around tests
- Unit tests are effective when building a large, contraint (deterministic) algorithm that would be time costly or hard to effectively hand test
- Writing unit tests is also a good practice to write cleaner - more testable code
- 100% coverege is pointless, too many tests are hard to maintain and most of unit tests would be pointless