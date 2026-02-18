# Number Systems and Binary Arithmetic

---

## 1. Number Systems

### 1.1 Binary (Base 2)

Digits: $0, 1$

Weights:
$ 2^n $

Example:
$$
(1011)_2 = 1\cdot2^3 + 0\cdot2^2 + 1\cdot2^1 + 1\cdot2^0 = 11_{10}
$$

---

### 1.2 Octal (Base 8)

Digits: $0$–$7$

Weights:
$ 8^n $

Binary to Octal: group bits in 3.

Example:
$$
(110101)_2 = (65)_8
$$

---

### 1.3 Hexadecimal (Base 16)

Digits: $0$–$9$, $A$–$F$

Weights:
$$
16^n
$$

Binary to Hex: group bits in 4.

Example:
$$
(11111010)_2 = (FA)_{16}
$$

---

## 2. Binary Arithmetic

### 2.1 Addition Rules

$$
0+0=0
$$
$$
0+1=1
$$
$$
1+1=10
$$
$$
1+1+1=11
$$

Example:
$$
\begin{aligned}
  &1011 \\
+ &0110 \\
\hline
  &10001
\end{aligned}
$$

---

### 2.2 Subtraction

If:
$$
0 - 1
$$
borrow from higher bit.

---

## 3. Two's Complement Representation

### 3.1 Sign Bit

For an $n$-bit number:

- MSB $= 0$ → positive  
- MSB $= 1$ → negative  

---

### 3.2 Ranges

Unsigned:
$$
0 \le x \le 2^n - 1
$$

Signed (two's complement):
$$
-2^{n-1} \le x \le 2^{n-1}-1
$$

Example (8-bit):
$$
[-128, 127]
$$

---

### 3.3 Forming a Negative Number

To compute $-B$:

1. Invert bits  
2. Add 1  

Equivalent expression:
$$
-B = 2^n - B
$$

---

## 4. Subtraction Using Two's Complement

Instead of:
$$
A - B
$$

Compute:
$$
A + (-B)
$$

Since:
$$
-B = 2^n - B
$$

Therefore:
$$
A - B = A + (2^n - B)
$$

All arithmetic is performed:
$$
\text{mod } 2^n
$$

---

## 5. Modular Arithmetic

Computers store integers:
$$
0 \le x \le 2^n - 1
$$

Arithmetic is performed:
$$
\text{mod } 2^n
$$

Clock analogy (mod $12$):
$$
18 \equiv 6 \pmod{12}
$$

Because:
$$
18 = 12 + 6
$$

Thus:
$$
12 \equiv 0 \pmod{12}
$$

---

## 6. Overflow

Overflow occurs when the result exceeds representable signed range.

For two's complement addition:

Overflow if:
$$
\text{Carry into MSB} \ne \text{Carry out of MSB}
$$

Or equivalently:

- Same sign operands  
- Different sign result  

Example (4-bit):
$$
7 + 3 = 1010_2
$$

But signed range:
$$
[-8,7]
$$

Thus overflow occurs.