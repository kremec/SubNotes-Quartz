## Registri

| Register | ABI Name | Description                          |
| -------- | -------- | ------------------------------------ |
| x0       | zero     | hardwired zero                       |
| x1       | ra       | return address                       |
| x2       | sp       | stack pointer                        |
| x3       | gp       | global pointer                       |
| x4       | tp       | thread pointer                       |
| x5       | t0       | temporary register 0                 |
| x6       | t1       | temporary register 1                 |
| x7       | t2       | temporary register 2                 |
| x8       | s0 / fp  | saved register 0 / frame pointer     |
| x9       | s1       | saved register 1                     |
| x10      | a0       | function argument 0 / return value 0 |
| x11      | a1       | function argument 1 / return value 1 |
| x12      | a2       | function argument 2                  |
| x13      | a3       | function argument 3                  |
| x14      | a4       | function argument 4                  |
| x15      | a5       | function argument 5                  |
| x16      | a6       | function argument 6                  |
| x17      | a7       | function argument 7                  |
| x18      | s2       | saved register 2                     |
| x19      | s3       | saved register 3                     |
| x20      | s4       | saved register 4                     |
| x21      | s5       | saved register 5                     |
| x22      | s6       | saved register 6                     |
| x23      | s7       | saved register 7                     |
| x24      | s8       | saved register 8                     |
| x25      | s9       | saved register 9                     |
| x26      | s10      | saved register 10                    |
| x27      | s11      | saved register 11                    |
| x28      | t3       | temporary register 3                 |
| x29      | t4       | temporary register 4                 |
| x30      | t5       | temporary register 5                 |
| x31      | t6       | temporary register 6                 |
## Instruction set
| Notation      | Description                                                |
| ------------- | ---------------------------------------------------------- |
| pc            | program counter                                            |
| rd            | integer register destination                               |
| rsN           | integer register source N                                  |
| imm           | immediate operand value                                    |
| offset        | immediate program counter relative offset                  |
| ux(reg)       | unsigned XLEN-bit integer (32-bit on RV32, 64-bit on RV64) |
| sx(reg)       | signed XLEN-bit integer (32-bit on RV32, 64-bit on RV64)   |
| uN(reg)       | zero extended N-bit integer register value                 |
| sN(reg)       | sign extended N-bit integer register value                 |
| uN[reg + imm] | unsigned N-bit memory reference                            |
| sN[reg + imm] | signed N-bit memory reference                              |
<br><br><br><br><br><br><br>
### Binop
#### Arithmetic

| Instruction         | Name                            | Pseudocode                      |
| ------------------- | ------------------------------- | ------------------------------- |
| `ADD rd,rs1,rs2`    | **Add**                         | rd ← sx(rs1) + sx(rs2)          |
| `ADDI rd,rs1,imm`   | **Add Immediate**               | rd ← rs1 + sx(imm)              |
| `SUB rd,rs1,rs2`    | **Subtract**                    | rd ← sx(rs1) - sx(rs2)          |
| `MUL rd,rs1,rs2`    | **Multiply**                    | rd ← ux(rs1) × ux(rs2)          |
| `DIV rd,rs1,rs2`    | **Divide Signed**               | rd ← sx(rs1) ÷ sx(rs2)          |
| `REM rd,rs1,rs2`    | **Remainder Signed**            | rd ← sx(rs1) mod sx(rs2)        |
|                     |                                 |                                 |
| `MULH rd,rs1,rs2`   | Multiply High Signed Signed     | rd ← (sx(rs1) × sx(rs2)) » xlen |
| `MULHSU rd,rs1,rs2` | Multiply High Signed Unsigned   | rd ← (sx(rs1) × ux(rs2)) » xlen |
| `MULHU rd,rs1,rs2`  | Multiply High Unsigned Unsigned | rd ← (ux(rs1) × ux(rs2)) » xlen |
| `DIVU rd,rs1,rs2`   | Divide Unsigned                 | rd ← ux(rs1) ÷ ux(rs2)          |
| `REMU rd,rs1,rs2`   | Remainder Unsigned              | rd ← ux(rs1) mod ux(rs2)        |
|                     |                                 |                                 |
| `MV rd,rs1`         | Copy Register                   | rd ← rs1                        |

#### Logical

| Instruction       | Name              | Pseudocode             |
| ----------------- | ----------------- | ---------------------- |
| `AND rd,rs1,rs2`  | **And**           | rd ← ux(rs1) ∧ ux(rs2) |
| `ANDI rd,rs1,imm` | **And Immediate** | rd ← ux(rs1) ∧ ux(imm) |
| `OR rd,rs1,rs2`   | **Or**            | rd ← ux(rs1) ∨ ux(rs2) |
| `ORI rd,rs1,imm`  | **Or Immediate**  | rd ← ux(rs1) ∨ ux(imm) |
| `XOR rd,rs1,rs2`  | **Xor**           | rd ← ux(rs1) ⊕ ux(rs2) |
|                   |                   |                        |
| `XORI rd,rs1,imm` | Xor Immediate     | rd ← ux(rs1) ⊕ ux(imm) |

#### Shift

| Instruction       | Name                             | Pseudocode             |
| ----------------- | -------------------------------- | ---------------------- |
| `SLL rd,rs1,rs2`  | Shift Left Logical               | rd ← ux(rs1) « rs2     |
| `SLLI rd,rs1,imm` | Shift Left Logical Immediate     | rd ← ux(rs1) « ux(imm) |
| `SRL rd,rs1,rs2`  | Shift Right Logical              | rd ← ux(rs1) » rs2     |
| `SRLI rd,rs1,imm` | Shift Right Logical Immediate    | rd ← ux(rs1) » ux(imm) |
|                   |                                  |                        |
| `SRA rd,rs1,rs2`  | Shift Right Arithmetic           | rd ← sx(rs1) » rs2     |
| `SRAI rd,rs1,imm` | Shift Right Arithmetic Immediate | rd ← sx(rs1) » sx(imm) |

#### Compare

| Instruction        | Name                             | Pseudocode             |
| ------------------ | -------------------------------- | ---------------------- |
| `SLT rd,rs1,rs2`   | **Set Less Than**                | rd ← sx(rs1) < sx(rs2) |
| `SLTI rd,rs1,imm`  | **Set Less Than Immediate**      | rd ← sx(rs1) < sx(imm) |
|                    |                                  |                        |
| `SLTIU rd,rs1,imm` | Set Less Than Immediate Unsigned | rd ← ux(rs1) < ux(imm) |
| `SLTU rd,rs1,rs2`  | Set Less Than Unsigned           | rd ← ux(rs1) < ux(rs2) |
### Unop

| Instruction  | Name       | Pseudocode |
| ------------ | ---------- | ---------- |
| `NEG rd,rs1` | **Negate** | rd ← -rs1  |
<br><br><br><br><br>
### Memory

| Instruction          | Name                      | Pseudocode              |
| -------------------- | ------------------------- | ----------------------- |
| `LD rd,offset(rs1)`  | **Load Double**           | rd ← u64[rs1 + offset]  |
| `LBU rd,offset(rs1)` | **Load Byte Unsigned**    | rd ← u8[rs1 + offset]   |
| `SD rs2,offset(rs1)` | **Store Double**          | u64[rs1 + offset] ← rs2 |
| `SB rs2,offset(rs1)` | **Store Byte**            | u8[rs1 + offset] ← rs2  |
| `LA rd, label`       | **Load Symbol Address**   | rd ← &label             |
| `LI rd, imm`         | **Load Immediate**        | rd ← imm                |
|                      |                           |                         |
| `LB rd,offset(rs1)`  | Load Byte                 | rd ← s8[rs1 + offset]   |
| `LH rd,offset(rs1)`  | Load Half                 | rd ← s16[rs1 + offset]  |
| `LW rd,offset(rs1)`  | Load Word                 | rd ← s32[rs1 + offset]  |
| `SH rs2,offset(rs1)` | Store Half                | u16[rs1 + offset] ← rs2 |
| `SW rs2,offset(rs1)` | Store Word                | u32[rs1 + offset] ← rs2 |
| `LUI rd,imm`         | Load Upper Immediate      | rd ← imm                |
| `AUIPC rd,offset`    | Add Upper Immediate to PC | rd ← pc + offset        |
### Jumps
#### Jumps

| Instruction          | Name                   | Pseudocode                                           |
| -------------------- | ---------------------- | ---------------------------------------------------- |
| `J imm`              | **Jump**                   | pc ← pc + imm                                        |
| `JALR rd,rs1,offset` | **Jump and Link Register** | rd ← pc + length(inst)  <br>pc ← (rs1 + offset) ∧ -2 |
|                      |                        |                                                      |
| `JAL rd,offset`      | Jump and Link          | rd ← pc + length(inst)  <br>pc ← pc + offset         |
#### Branches

| Instruction           | Name                               | Pseudocode                       |
| --------------------- | ---------------------------------- | -------------------------------- |
| `BNEZ rs1,imm`        | **Branch not equal zero**          | if(rs1 ≠ 0) pc ← pc + imm        |
|                       |                                    |                                  |
| `BEQ rs1,rs2,offset`  | Branch Equal                       | if (rs1 = rs2)  pc ← pc + offset |
| `BEQZ rs1, imm`       | Branch Equal Zero                  | if(rs1 == 0) pc ← pc + imm       |
| `BNE rs1,rs2,offset`  | Branch Not Equal                   | if (rs1 ≠ rs2) pc ← pc + offset  |
| `BLT rs1,rs2,offset`  | Branch Less Than                   | if (rs1 < rs2) pc ← pc + offset  |
| `BGE rs1,rs2,offset`  | Branch Greater than Equal          | if (rs1 ≥ rs2) pc ← pc + offset  |
| `BLTU rs1,rs2,offset` | Branch Less Than Unsigned          | if (rs1 < rs2) pc ← pc + offset  |
| `BGEU rs1,rs2,offset` | Branch Greater than Equal Unsigned | if (rs1 ≥ rs2) pc ← pc + offset  |
| `BLTZ rs1,imm`        | Branch Less Than Zero              | if(rs1 < 0) pc ← pc + imm        |
| `BGTZ rs1,imm`        | Branch Greater Than Zero           | if(rs1 > 0) pc ← pc + imm        |
| `BLE rs1,rs2,imm`     | Branch Less or Equal               | if(rs1 ≤ rs2) pc ← pc + imm      |
| `BLEU rs1,rs2,imm`    | Branch Less or Equal Unsigned      | if(rs1 ≤ rs2) pc ← pc + imm      |
| `BLEZ rs1,imm`        | Branch Less or Equal Zero          | if(rs1 ≤ 0) pc ← pc + imm        |
| `BGEZ rs1,imm`        | Branch Greater or Equal Zero       | if(rs1 ≥ 0) pc ← pc + imm        |
You can use a label in place of a branch immediate, for example: `BEQ t0,t1,label`
### Functions

| Instruction  | Name                     | Pseudocode                |
| ------------ | ------------------------ | ------------------------- |
| `CALL label` | **Call Function**        | ra ← pc+4;<br>pc ← &label |
| `RET`        | **Return from Function** | pc ← ra                   |
