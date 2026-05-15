# Number Systems and Binary Arithmetic — Examples

This file contains worked examples and detailed explanations.

Back to concepts:

⬅️ [Number Systems Concepts](./concept.md)

---

## 1. Number Systems Examples

### 1.1 Binary Positional Weight Example

Related concept: [Binary positional weights](./concept.md#11-binary-base-2)

Convert:

$$
(11010)_2
$$

into decimal.

Use powers of 2:

$$
(11010)_2
=
1\cdot2^4+1\cdot2^3+0\cdot2^2+1\cdot2^1+0\cdot2^0
$$

$$
=
16+8+0+2+0
=
26_{10}
$$

Therefore:

$$
(11010)_2=26_{10}
$$

---

### 1.2 Binary to Octal Example

Related concept: [Octal](./concept.md#12-octal-base-8)

Convert:

$$
(110101)_2
$$

into octal.

Group bits in 3s from the right:

$$
110101_2=110\ 101_2
$$

Convert each 3-bit group:

$$
110_2=6
$$

$$
101_2=5
$$

Therefore:

$$
(110101)_2=(65)_8
$$

---

### 1.3 Binary to Hexadecimal Example

Related concept: [Hexadecimal](./concept.md#13-hexadecimal-base-16)

Convert:

$$
101100111010_2
$$

into hexadecimal.

Group bits in 4s from the right:

$$
101100111010_2=1011\ 0011\ 1010_2
$$

Convert each group:

$$
1011_2=B
$$

$$
0011_2=3
$$

$$
1010_2=A
$$

Therefore:

$$
101100111010_2=B3A_{16}
$$

---

## 2. Decimal-to-Base Conversion Examples

### 2.1 Decimal to Binary Example

Related concept: [Integer conversion by successive division](./concept.md#21-integer-conversion-by-successive-division)

Convert:

$$
26_{10}
$$

into binary.

Divide by 2 repeatedly:

| Division | Quotient | Remainder |
|---:|---:|---:|
| \(26\div2\) | 13 | 0 |
| \(13\div2\) | 6 | 1 |
| \(6\div2\) | 3 | 0 |
| \(3\div2\) | 1 | 1 |
| \(1\div2\) | 0 | 1 |

The first remainder is the LSD.  
The last remainder is the MSD.

Read the remainders from bottom to top:

$$
26_{10}=11010_2
$$

---

### 2.2 Decimal to Octal Example

Related concept: [Integer conversion by successive division](./concept.md#21-integer-conversion-by-successive-division)

Convert:

$$
2874_{10}
$$

into octal.

Divide by 8 repeatedly:

| Division | Quotient | Remainder |
|---:|---:|---:|
| \(2874\div8\) | 359 | 2 |
| \(359\div8\) | 44 | 7 |
| \(44\div8\) | 5 | 4 |
| \(5\div8\) | 0 | 5 |

Read the remainders from bottom to top:

$$
2874_{10}=5472_8
$$

Check:

$$
5472_8
=
5\cdot8^3+4\cdot8^2+7\cdot8^1+2\cdot8^0
$$

$$
=
2560+256+56+2
=
2874_{10}
$$

---

### 2.3 Decimal to Hexadecimal Example

Related concept: [Integer conversion by successive division](./concept.md#21-integer-conversion-by-successive-division)

Convert:

$$
2874_{10}
$$

into hexadecimal.

Divide by 16 repeatedly:

| Division | Quotient | Remainder |
|---:|---:|---:|
| \(2874\div16\) | 179 | 10 |
| \(179\div16\) | 11 | 3 |
| \(11\div16\) | 0 | 11 |

Convert remainders above 9 into hexadecimal symbols:

$$
10=A
$$

$$
11=B
$$

Read the remainders from bottom to top:

$$
2874_{10}=B3A_{16}
$$

Check:

$$
B3A_{16}
=
11\cdot16^2+3\cdot16^1+10\cdot16^0
$$

$$
=
2816+48+10
=
2874_{10}
$$

---

## 3. Fast Binary-Octal-Hex Conversion Examples

### 3.1 Binary to Octal Example

Related concept: [Binary to octal](./concept.md#31-binary-to-octal)

Convert:

$$
101100111010_2
$$

into octal.

Group in 3s from the right:

$$
101100111010_2
=
101\ 100\ 111\ 010_2
$$

Convert each group:

$$
101_2=5
$$

$$
100_2=4
$$

$$
111_2=7
$$

$$
010_2=2
$$

Therefore:

$$
101100111010_2=5472_8
$$

---

### 3.2 Binary to Hexadecimal Example

Related concept: [Binary to hexadecimal](./concept.md#32-binary-to-hexadecimal)

Convert:

$$
101100111010_2
$$

into hexadecimal.

Group in 4s from the right:

$$
101100111010_2
=
1011\ 0011\ 1010_2
$$

Convert each group:

$$
1011_2=B
$$

$$
0011_2=3
$$

$$
1010_2=A
$$

Therefore:

$$
101100111010_2=B3A_{16}
$$

---

### 3.3 Padding Zeros Example

Related concept: [Padding zeros](./concept.md#33-padding-zeros)

Convert:

$$
11010_2
$$

into hexadecimal.

Group in 4s from the right:

$$
11010_2
$$

The leftmost group has only one bit, so add leading zeros:

$$
0001\ 1010_2
$$

Convert each group:

$$
0001_2=1
$$

$$
1010_2=A
$$

Therefore:

$$
11010_2=1A_{16}
$$

Leading zeros do not change the value.

---

## 4. Two's Complement Examples

### 4.1 Forming a Negative Number Example

Related concept: [Forming a negative number](./concept.md#44-forming-a-negative-number)

Find \(-5\) in 4-bit two's complement.

Start with positive 5:

$$
5_{10}=0101_2
$$

Invert all bits:

$$
0101 \rightarrow 1010
$$

Add 1:

$$
1010+1=1011
$$

Therefore:

$$
-5=1011_2
$$

in 4-bit two's complement.

Check using weights:

$$
1011_2=-8+0+2+1=-5
$$

---

## 5. Subtraction Using Two's Complement Examples

### 5.1 Subtraction Using Two's Complement Example

Related concept: [Subtraction using two's complement](./concept.md#5-subtraction-using-twos-complement)

Compute:

$$
7-5
$$

using 4-bit two's complement.

Write \(7\):

$$
7=0111_2
$$

Write \(5\):

$$
5=0101_2
$$

Find \(-5\):

Invert:

$$
0101 \rightarrow 1010
$$

Add 1:

$$
1010+1=1011
$$

So:

$$
-5=1011_2
$$

Now add:

$$
0111+1011=1\ 0010
$$

In 4-bit arithmetic, discard the carry out:

$$
0010_2
$$

Therefore:

$$
7-5=2
$$

---

## 6. Modular Arithmetic Examples

### 6.1 Modulo Wrap-Around Example

Related concept: [Modular arithmetic](./concept.md#6-modular-arithmetic)

For a 4-bit unsigned system:

$$
0 \le x \le 15
$$

because:

$$
2^4-1=15
$$

If we compute:

$$
15+1=16
$$

the stored 4-bit result wraps around:

$$
1111_2+0001_2=1\ 0000_2
$$

Discard the carry out:

$$
0000_2
$$

So in 4-bit arithmetic:

$$
15+1 \equiv 0 \pmod{16}
$$

---

## 7. Overflow Examples

### 7.1 4-bit Overflow Example

Related concept: [Overflow](./concept.md#7-overflow)

For 4-bit signed two's complement:

$$
-8 \le x \le 7
$$

Now compute:

$$
7+3=10
$$

But \(10\) is outside the signed 4-bit range.

Binary addition:

$$
0111_2+0011_2=1010_2
$$

In 4-bit two's complement:

$$
1010_2=-6
$$

Therefore, overflow has occurred.

The true mathematical result is:

$$
7+3=10
$$

but \(10\) cannot be represented in 4-bit signed two's complement.

The stored bit pattern wraps to:

$$
1010_2=-6
$$

---

### 7.2 Clock Analogy

Related concept: [Modular arithmetic](./concept.md#6-modular-arithmetic)

In modulo 12 arithmetic:

$$
18 \equiv 6 \pmod{12}
$$

This means 18:00 is equivalent to 6:00 on a 12-hour clock.

Also:

$$
12 \equiv 0 \pmod{12}
$$

because after reaching 12, the value wraps around.