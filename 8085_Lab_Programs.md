# 8085 Microprocessor Lab Programs

A single GitHub-friendly collection of the 8085 assembly language
programs from the Computer Organization and Microprocessor Architecture
Lab manual.

## Table of Contents

1.  [Experiment 1 - Part A: Addition of Two 8-bit
    Numbers](#experiment-1---part-a-addition-of-two-8-bit-numbers)
2.  [Experiment 1 - Part B: Addition of Two 16-bit
    Numbers](#experiment-1---part-b-addition-of-two-16-bit-numbers)
3.  [Experiment 1 - Part C: Subtraction of Two 8-bit
    Numbers](#experiment-1---part-c-subtraction-of-two-8-bit-numbers)
4.  [Experiment 2 - Part A: Multiplication of Two 8-bit
    Numbers](#experiment-2---part-a-multiplication-of-two-8-bit-numbers)
5.  [Experiment 2 - Part B: Division of Two 8-bit
    Numbers](#experiment-2---part-b-division-of-two-8-bit-numbers)
6.  [Experiment 3: Addition of a Block of 8-bit
    Data](#experiment-3-addition-of-a-block-of-8-bit-data)
7.  [Experiment 4 - Part A: Minimum of Two 8-bit
    Numbers](#experiment-4---part-a-minimum-of-two-8-bit-numbers)
8.  [Experiment 4 - Part B: Minimum from a Block of N 8-bit
    Numbers](#experiment-4---part-b-minimum-from-a-block-of-n-8-bit-numbers)
9.  [Experiment 5 - Part A: Maximum of Two 8-bit
    Numbers](#experiment-5---part-a-maximum-of-two-8-bit-numbers)
10. [Experiment 5 - Part B: Maximum from a Block of N 8-bit
    Numbers](#experiment-5---part-b-maximum-from-a-block-of-n-8-bit-numbers)
11. [Experiment 6 - Part A: Sort in Ascending
    Order](#experiment-6---part-a-sort-in-ascending-order)
12. [Experiment 6 - Part B: Sort in Descending
    Order](#experiment-6---part-b-sort-in-descending-order)
13. [Experiment 7 - Part A: BCD to
    Binary](#experiment-7---part-a-bcd-to-binary)
14. [Experiment 7 - Part B: Binary to
    BCD](#experiment-7---part-b-binary-to-bcd)
15. [Experiment 8 - Part A: Binary to
    ASCII](#experiment-8---part-a-binary-to-ascii)
16. [Experiment 8 - Part B: ASCII to
    Binary](#experiment-8---part-b-ascii-to-binary)
17. [Experiment 9: Sum of Even
    Numbers](#experiment-9-sum-of-even-numbers)
18. [Experiment 10: Sum of Odd
    Numbers](#experiment-10-sum-of-odd-numbers)

------------------------------------------------------------------------

## Experiment 1 - Part A: Addition of Two 8-bit Numbers

``` asm
LDA 2050H
MOV B, A
LDA 2051H
ADD B
STA 2052H
HLT
```

## Experiment 1 - Part B: Addition of Two 16-bit Numbers

``` asm
LHLD 2050H
XCHG
LHLD 2052H
DAD D
SHLD 2054H
HLT
```

## Experiment 1 - Part C: Subtraction of Two 8-bit Numbers

``` asm
LDA 2051H
MOV B, A
LDA 2050H
SUB B
STA 2052H
HLT
```

## Experiment 2 - Part A: Multiplication of Two 8-bit Numbers

``` asm
LDA 2050H
MOV D, A
LDA 2051H
MOV C, A
ORA A
MVI A, 00H
JZ STORE
LOOP: ADD D
DCR C
JNZ LOOP
STORE:
STA 2052H
HLT
```

## Experiment 2 - Part B: Division of Two 8-bit Numbers

``` asm
LDA 2051H
MOV C, A
LDA 2050H
MVI D, 00H
MOV B, A
MOV A, C
ORA A
MOV A, B
JZ DONE
LOOP: CMP C
JC DONE
SUB C
INR D
JMP LOOP
DONE:
STA 2053H
MOV A, D
STA 2052H
HLT
```

## Experiment 3: Addition of a Block of 8-bit Data

``` asm
LXI H, 2050H
MOV C, M
MVI A, 00H
LOOP: INX H
ADD M
DCR C
JNZ LOOP
STA 2055H
HLT
```

## Experiment 4 - Part A: Minimum of Two 8-bit Numbers

``` asm
LDA 2050H
MOV B, A
LDA 2051H
CMP B
JC STORE
MOV A, B
STORE:
STA 2052H
HLT
```

## Experiment 4 - Part B: Minimum from a Block of N 8-bit Numbers

``` asm
LXI H, 2050H
MOV C, M
INX H
MOV A, M
DCR C
LOOP: INX H
CMP M
JC SKIP
MOV A, M
SKIP: DCR C
JNZ LOOP
STA 2055H
HLT
```

## Experiment 5 - Part A: Maximum of Two 8-bit Numbers

``` asm
LDA 2050H
MOV B, A
LDA 2051H
CMP B
JNC STORE
MOV A, B
STORE:
STA 2052H
HLT
```

## Experiment 5 - Part B: Maximum from a Block of N 8-bit Numbers

``` asm
LXI H, 2050H
MOV C, M
INX H
MOV A, M
DCR C
LOOP: INX H
CMP M
JNC SKIP
MOV A, M
SKIP: DCR C
JNZ LOOP
STA 2055H
HLT
```

## Experiment 6 - Part A: Sort in Ascending Order

``` asm
LDA 2050H
CPI 02H
JC HALT
DCR A
MOV D, A
OUTER:
LDA 2050H
DCR A
MOV C, A
LXI H, 2051H
INNER:
MOV A, M
INX H
CMP M
JC SKIP
JZ SKIP
MOV B, M
MOV M, A
DCX H
MOV M, B
INX H
SKIP:
DCR C
JNZ INNER
DCR D
JNZ OUTER
HALT:
HLT
```

## Experiment 6 - Part B: Sort in Descending Order

``` asm
LDA 2050H
CPI 02H
JC HALT
DCR A
MOV D, A
OUTER:
LDA 2050H
DCR A
MOV C, A
LXI H, 2051H
INNER:
MOV A, M
INX H
CMP M
JNC SKIP
MOV B, M
MOV M, A
DCX H
MOV M, B
INX H
SKIP:
DCR C
JNZ INNER
DCR D
JNZ OUTER
HALT:
HLT
```

## Experiment 7 - Part A: BCD to Binary

``` asm
LDA 2050H
MOV B, A
ANI 0F0H
RRC
RRC
RRC
RRC
MOV C, A
ADD A
ADD A
ADD C
ADD A
MOV C, A
MOV A, B
ANI 0FH
ADD C
STA 2051H
HLT
```

## Experiment 7 - Part B: Binary to BCD

``` asm
LDA 2050H
MVI B, 00H
MVI C, 00H
HUNDREDS:
CPI 64H
JC TENS
SUI 64H
INR B
JMP HUNDREDS
TENS:
CPI 0AH
JC UNITS
SUI 0AH
INR C
JMP TENS
UNITS:
MOV D, A
MOV A, C
RLC
RLC
RLC
RLC
ADD D
STA 2052H
MOV A, B
STA 2051H
HLT
```

## Experiment 8 - Part A: Binary to ASCII

``` asm
LDA 2050H
MOV B, A
ANI 0F0H
RRC
RRC
RRC
RRC
CPI 0AH
JC NUM1
ADI 07H
NUM1:
ADI 30H
STA 2051H
MOV A, B
ANI 0FH
CPI 0AH
JC NUM2
ADI 07H
NUM2:
ADI 30H
STA 2052H
HLT
```

## Experiment 8 - Part B: ASCII to Binary

``` asm
LDA 2050H
SUI 30H
CPI 0AH
JC OK1
SUI 07H
OK1:
RLC
RLC
RLC
RLC
MOV B, A
LDA 2051H
SUI 30H
CPI 0AH
JC OK2
SUI 07H
OK2:
ADD B
STA 2052H
HLT
```

## Experiment 9: Sum of Even Numbers

``` asm
LXI H, 2050H
MOV C, M
MVI B, 00H
LOOP:
INX H
MOV A, M
ANI 01H
JNZ SKIP
MOV A, B
ADD M
MOV B, A
SKIP:
DCR C
JNZ LOOP
MOV A, B
STA 2055H
HLT
```

## Experiment 10: Sum of Odd Numbers

``` asm
LXI H, 2050H
MOV C, M
MVI B, 00H
LOOP:
INX H
MOV A, M
ANI 01H
JZ SKIP
MOV A, B
ADD M
MOV B, A
SKIP:
DCR C
JNZ LOOP
MOV A, B
STA 2055H
HLT
```

------------------------------------------------------------------------

## Notes

-   The programs above are extracted from the supplied lab manual and
    kept in the same overall order.
-   A few lines in the source PDF appear to contain incomplete/ambiguous
    assembly syntax, such as `MOV B` in Experiment 1 Part C and `MVI A`
    in Experiment 2 Part A. They have been preserved here rather than
    silently corrected.
-   This file is intended to be viewed directly on GitHub, so all
    programs are contained in one Markdown file.
