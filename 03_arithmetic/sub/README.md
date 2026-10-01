# Mutua Esther - 094954 

## Program 1. sub1.asm Flag Analysis

### Flag table
 
| Flag | Status | Meaning tested |
|------|--------|----------------|
| CF | **1 (set)** | Unsigned borrow |
| ZF | **0 (clear)** | Result is zero |
| SF | **1 (set)** | MSB of result |
| OF | **0 (clear)** | Signed overflow |
| AF | **0 (clear)** | Borrow from bit 4 |
| PF | **1 (set)** | Even number of 1s in low byte |

### Why each flag has that status
 
**CF = 1.** As unsigned numbers, 50 is less than 80, so subtracting needs a borrow
from beyond bit 7. Equivalently, the two's complement addition produced no
carry-out, and CF is the inverse of that carry. As unsigned, the result 226 is *wrong*
(the true answer is negative), and CF is the warning.
 
**ZF = 0.** The result `0xE2` is non-zero (50 does not equal 80).
 
**SF = 1.** Bit 7 of `1110 0010b` is 1, which marks the result as negative when read as signed.
 
**OF = 0.** The signed result -30 lies within -128 to +127, so it is **valid**.
Also, both operands are positive, and subtracting two same-sign numbers can never
overflow. The negative result here is correct, not an overflow.
 
**AF = 0.** Compare the low nibbles: `0x2 - 0x0 = 2`. No borrow from bit 4 is
needed.
 
**PF = 1.** The low byte `1110 0010b` has four 1-bits, which is an even count.


## Program 2. sub2.asm Flag Analysis

### Flag table

| Flag | Status | Meaning tested |
|------|--------|----------------|
| CF | **1 (set)** | Unsigned borrow |
| ZF | **0 (clear)** | Result is zero |
| SF | **1 (set)** | MSB (bit 15) of result |
| OF | **0 (clear)** | Signed overflow |
| AF | **0 (clear)** | Borrow from bit 4 |
| PF | **1 (set)** | Even number of 1s in low byte |

### Why each flag has that status
 
**CF = 1.** 1000 is less than 2000 as unsigned 16-bit numbers, so a borrow
out of bit 15 is needed.
 
**ZF = 0.** The result `0xFC18` is non-zero.
 
**SF = 1.** Bit 15 of `0xFC18` (`1111 1100 ...`) is 1, so the result is negative as signed.
 
**OF = 0.** The signed result -1000 lies within -32768 to +32767. Both operands
are positive, so the subtraction cannot overflow.
 
**AF = 0.** The low nibbles are `0x8 - 0x0 = 8`, with no borrow from bit 4.
 
**PF = 1.** PF uses only the **low 8 bits**, even for a 16-bit operation. The low
byte is `0x18 = 0001 1000b`, which has two 1-bits, an even count. (The upper byte
`0xFC` is ignored.)

