# Mutua Esther - 094954 

## Program 1. mul1.asm Flag Analysis

### Flag table
 
| Flag | Status | Explanation |
|------|--------|-------------|
| **CF** | **0 (cleared)** | The upper half `AH` is 0. The whole product (250) fits in `AL` (0 to 255), so the extra register wasn't needed. |
| **OF** | **0 (cleared)** | Same rule and same reason as CF. They always match after `MUL`. |
| SF | Undefined | Not derived from the product. (Note: `AL = 0xFA` has bit 7 set, but `MUL` makes no promise that SF copies it.) |
| ZF | Undefined | Not derived from the product, even though the product is non-zero. |
| AF | Undefined | No defined meaning for `MUL`. |
| PF | Undefined | Not derived from the product. |

## Program 2. mul2.asm Flag Analysis

### Flag table 
 
| Flag | Status | Explanation |
|------|--------|-------------|
| **CF** | **1 (set)** | The upper half `DX` is `0x0009`, which is non-zero. The product 600000 exceeds 65535, so it does **not** fit in `AX` alone. |
| **OF** | **1 (set)** | Same rule and same reason as CF. |
| SF | Undefined | Not derived from the product. |
| ZF | Undefined | Not derived from the product. |
| AF | Undefined | No defined meaning for `MUL`. |
| PF | Undefined | Not derived from the product. |
 

