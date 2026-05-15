# Number Systems and Binary Arithmetic

This file contains only core concepts, rules, and formulas.

For worked examples and detailed explanations, see:

➡️ [Number Systems Examples](./examples.md)

---

## 1. Number Systems

### 1.1 Binary (Base 2)

**Digits:** `0, 1`

**Base:** 2

**Weights:**

```math
2^n
```

A binary number is weighted by powers of 2:

```math
(b_n b_{n-1}\dots b_1 b_0)_2
=
b_n2^n+b_{n-1}2^{n-1}+\dots+b_1 2^1+b_0 2^0
```

📘 Example: [Binary positional weight example](./examples.md#11-binary-positional-weight-example)

---

### 1.2 Octal (Base 8)

**Digits:** `0–7`

**Base:** 8

**Weights:**

```math
8^n
```

Binary to octal conversion:

> Group binary bits in groups of 3 from the right.

📘 Example: [Binary to octal example](./examples.md#12-binary-to-octal-example)

---

### 1.3 Hexadecimal (Base 16)

**Digits:** `0–9, A–F`

**Base:** 16

**Weights:**

```math
16^n
```

Hexadecimal digit values:

| Hex | Decimal |
|---:|---:|
| A | 10 |
| B | 11 |
| C | 12 |
| D | 13 |
| E | 14 |
| F | 15 |

Binary to hexadecimal conversion:

> Group binary bits in groups of 4 from the right.

📘 Example: [Binary to hexadecimal example](./examples.md#13-binary-to-hexadecimal-example)

---

### 1.4 Binary Prefixes

In hardware design, binary prefixes often represent powers of:

```math
2^{10}=1024
```

| Prefix | Symbol | Binary Power | Decimal Approx. | Exact Value |
| :--- | :--- | :--- | :--- | :--- |
| Kilo | K | `2^10` | `10^3` | `1,024` |
| Mega | M | `2^20` | `10^6` | `1,048,576` |
| Giga | G | `2^30` | `10^9` | `1,073,741,824` |
| Tera | T | `2^40` | `10^12` | `1,099,511,627,776` |

Useful identity:

```math
2^{20}=10^6+d
```

where:

```math
d=48,576
```

Then:

```math
2^{40}=(10^6+d)^2
=
10^{12}+2(10^6)d+d^2
```

---

## 2. Decimal-to-Base Conversion

### 2.1 Integer Conversion by Successive Division

To convert a decimal integer into base `r`:

1. Divide the decimal integer by the target base `r`.
2. Record the remainder.
3. The first remainder is the **LSD**.
4. Repeat using the integer quotient.
5. Stop when the quotient becomes `0`.
6. Read the remainders from bottom to top.
7. The last remainder is the **MSD**.

```math
\text{first remainder}=\text{LSD}
```

```math
\text{last remainder}=\text{MSD}
```

📘 Examples:

- [Decimal to binary example](./examples.md#21-decimal-to-binary-example)
- [Decimal to octal example](./examples.md#22-decimal-to-octal-example)
- [Decimal to hexadecimal example](./examples.md#23-decimal-to-hexadecimal-example)

---

### 2.2 Fraction Conversion by Successive Multiplication

To convert a decimal fraction into base `r`:

1. Multiply the decimal fraction by the target base `r`.
2. Record the integer part.
3. The first integer part is the **MSD after the radix point**.
4. Repeat using only the remaining fractional part.
5. Stop when the fractional part is `0`, or when required precision is reached.
6. Read the integer parts in order from top to bottom.

General form:

```math
0.x_{10}
\rightarrow
0.a_1a_2a_3\dots{}_r
```

where `a_1` is obtained first.

---

### 2.3 General Positional Formula

For a number `N` with integer and fractional parts in base `r`:

```math
N
=
\sum_{i=0}^{n} d_i r^i
+
\sum_{j=1}^{m} a_{-j}r^{-j}
```

where:

- `d_i` are the integer-part digits
- `a_{-j}` are the fractional-part digits
- `r` is the base

---

## 3. Fast Conversion Between Binary, Octal and Hex

### 3.1 Binary to Octal

Group binary bits in groups of 3 from the right.

```math
\text{1 octal digit}=3\text{ binary bits}
```

📘 Example: [Binary to octal example](./examples.md#31-binary-to-octal-example)

---

### 3.2 Binary to Hexadecimal

Group binary bits in groups of 4 from the right.

```math
\text{1 hexadecimal digit}=4\text{ binary bits}
```

📘 Example: [Binary to hexadecimal example](./examples.md#32-binary-to-hexadecimal-example)

---

### 3.3 Padding Zeros

If the leftmost group does not have enough bits, add leading zeros.

Leading zeros do not change the value.

📘 Example: [Padding zeros example](./examples.md#33-padding-zeros-example)

---

## 4. Two's Complement Representation

### 4.1 Sign Bit in an n-bit System

For signed two's complement numbers:

- **MSB = 0** means positive or zero
- **MSB = 1** means negative

---

### 4.2 Unsigned Range

For an `n`-bit unsigned number:

```math
0 \le x \le 2^n-1
```

---

### 4.3 Signed Two's Complement Range

For an `n`-bit signed two's complement number:

```math
-2^{n-1} \le x \le 2^{n-1}-1
```

For 8-bit signed two's complement:

```math
-128 \le x \le 127
```

---

### 4.4 Forming a Negative Number

To compute `-B` in an `n`-bit two's complement system:

1. Invert all bits.
2. Add `1`.

Mathematical identity:

```math
-B=2^n-B
```

within an `n`-bit system.

📘 Example: [Two's complement negative number example](./examples.md#41-forming-a-negative-number-example)

---

## 5. Subtraction Using Two's Complement

Instead of directly computing:

```math
A-B
```

the CPU computes:

```math
A+(-B)
```

Since:

```math
-B=2^n-B
```

the hardware performs:

```math
A-B
\equiv
A+(2^n-B)
\pmod{2^n}
```

📘 Example: [Subtraction using two's complement example](./examples.md#51-subtraction-using-twos-complement-example)

---

## 6. Modular Arithmetic

Computers store integers within fixed bounds.

For an `n`-bit system:

```math
0 \le x \le 2^n-1
```

All arithmetic is performed modulo:

```math
2^n
```

Values wrap around once they exceed the available bit range.

📘 Example: [Modulo wrap-around example](./examples.md#61-modulo-wrap-around-example)

---

## 7. Overflow

Overflow occurs when the true result is outside the representable signed range.

For signed two's complement addition:

- positive + positive giving negative means overflow
- negative + negative giving positive means overflow
- different signs cannot overflow

📘 Examples:

- [4-bit overflow example](./examples.md#71-4-bit-overflow-example)
- [Clock analogy for modular arithmetic](./examples.md#72-clock-analogy)