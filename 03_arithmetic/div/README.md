# Mutua Esther - 094954 

## Program 1. div1.asm Flag Analysis

### Flag table
 
| Flag | Status after `DIV` | Explanation |
|------|--------------------|-------------|
| CF | Undefined | Not updated by `DIV` |
| ZF | Undefined | Not tied to quotient/remainder being 0 |
| SF | Undefined | Not a copy of any result bit |
| OF | Undefined | Does not signal overflow; overflow raises `#DE` instead |
| AF | Undefined | No defined meaning for `DIV` |
| PF | Undefined | Not computed from the result |
 

## Program 2. div2.asm Flag Analysis

### Flag table

### Flags
 
| Flag | Status after `DIV` | Explanation |
|------|--------------------|-------------|
| CF | Undefined | Not updated by `DIV` |
| ZF | Undefined | Not tied to quotient/remainder being 0 |
| SF | Undefined | Not a copy of any result bit |
| OF | Undefined | Overflow is reported as an exception, not as OF |
| AF | Undefined | No defined meaning for `DIV` |
| PF | Undefined | Not computed from the result |

## Summary of Program 1 and 2 Flag Analysis

Flags that `DIV` never touches: DF, IF, TF. IF is normally 1 in a user program. It doesn't set the flags, so there are no set or cleared flags
