# Mutua Esther - 094954 
 
## Program 1. add2.asm Flag Analysis

### Flag table
 
| Flag | Status | Meaning tested |
|------|--------|----------------|
| CF (Carry) | **0 (clear)** | Unsigned overflow |
| ZF (Zero) | **0 (clear)** | Result is zero |
| SF (Sign) | **0 (clear)** | MSB (bit 15) of result |
| OF (Overflow) | **0 (clear)** | Signed overflow |
| AF (Auxiliary) | **0 (clear)** | Carry out of bit 3 |
| PF (Parity) | **0 (clear)** | Even number of 1s in low byte |


### Why each flag has that status
 
**CF = 0.** For 16-bit operands, CF is set only if the unsigned sum exceeds
65535 (a carry out of bit 15). 32500 is well below that, so there is no carry.
 
**ZF = 0.** The result `0x7EF4` is non-zero.
 
**SF = 0.** SF copies bit 15 of the result. `0111 1110 1111 0100b` has bit 15 = 0,
so the result is non-negative when read as signed.
 
**OF = 0.** Both operands are positive (bit 15 = 0) and the result is also
positive, so the sign is consistent. Equivalently, +32500 is within the signed
maximum of +32767, so there is no signed overflow. Note how close this is: the
program would have overflowed if the sum had gone above 32767.
 
**AF = 0.** AF checks the carry out of bit 3. The low nibbles are
`0000b (0) + 0100b (4) = 0100b (4)`. This fits in 4 bits, so there is no carry into
bit 4.
 
**PF = 0.** PF considers only the **lowest 8 bits**, even in a 16-bit operation.
The low byte is `0xF4 = 1111 0100b`, which contains **five** 1-bits. Five is an odd
count, so PF is clear. (The upper byte `0x7E` plays no part.)
 
## Program 2. add1.asm Flag Analysis

### Flag table
 
| Flag | Status | Meaning tested |
|------|--------|----------------|
| CF (Carry) | **0 (clear)** | Unsigned overflow |
| ZF (Zero) | **0 (clear)** | Result is zero |
| SF (Sign) | **1 (set)** | MSB of result |
| OF (Overflow) | **1 (set)** | Signed overflow |
| AF (Auxiliary) | **1 (set)** | Carry out of bit 3 |
| PF (Parity) | **1 (set)** | Even number of 1s in low byte |
 
## Why each flag has that status
 
**CF = 0.** CF is set when an unsigned addition produces a carry out of the top
bit (bit 7 for 8-bit operands). The true unsigned sum is 130, which fits in 0 to 255,
so nothing carries out of bit 7. The CF stays clear.
 
**ZF = 0.** ZF is set only if the result is exactly 0. The result is `0x82`,
which is non-zero.
 
**SF = 1.** SF is a copy of the most significant bit of the result. `10000010b`
has MSB = 1, so SF is set. This says that *if* we treat the result as signed, it is negative.
 
**OF = 1.** OF detects signed overflow: it is set when two operands of the same
sign give a result of the opposite sign. Here 120 and 10 are both positive
(MSB = 0), but the result has MSB = 1 (negative). The true answer, +130, exceeds the
signed 8-bit maximum of +127, so it wrapped to -126. Hence OF is set.
 
**AF = 1.** AF tracks a carry from bit 3 into bit 4 (used for BCD arithmetic).
Add the low nibbles: `1000b (8) + 1010b (10) = 10010b (18)`. 18 does not fit in
4 bits, so there is a carry into bit 4. AF is set.
 
**PF = 1.** PF looks only at the **lowest 8 bits** of the result and is set when the
count of 1-bits is even. `10000010b` has two 1s, which is even, so PF is set.
(PF is not about the value being even or odd. It is about the number of set bits.)
 