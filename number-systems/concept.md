## Number Systems and Binary Arithmetic

---

## 1. Number Systems

### 1.1 Binary (Base 2)
* **Digits:** 0, 1
* **Weights:** $2^n$

---

### 1.2 Octal (Base 8)
* **Digits:** 0–7
* **Weights:** $8^n$
* **Binary to Octal:** Group bits in 3s.
* **Example:** $(110101)_2 = (65)_8$

---

### 1.3 Hexadecimal (Base 16)
* **Digits:** 0–9, A–F
* **Weights:** $16^n$
* **Binary to Hex:** Group bits in 4s.

---

### 1.4 Binary Prefixes (K, M, G, T)
In hardware design, prefixes represent powers of $2^{10}$ ($1024$).

| Prefix | Symbol | Binary Power | Decimal Approx. | Exact Value |
| :--- | :--- | :--- | :--- | :--- |
| **Kilo** | K | $2^{10}$ | $10^3$ | $1,024$ |
| **Mega** | M | $2^{20}$ | $10^6$ | $1,048,576$ |
| **Giga** | G | $2^{30}$ | $10^9$ | $1,073,741,824$ |
| **Tera** | T | $2^{40}$ | $10^{12}$ | $1,099,511,627,776$ |



**Exact Calculation Identity:**
$$2^{20} = 10^6 + d \quad \text{where } d = 48,576$$
$$2^{40} = (10^6 + d)^2 = 10^{12} + 2(10^6)d + d^2$$

---

## 2. Decimal-to-Base $r$ Conversion

### 2.1 Successive Division Procedure (Integers)
1. **Divide** decimal integer by target base $r$.
2. **Record remainder** (First remainder = **LSD**).
3. **Repeat** using integer quotient until quotient is **0**.
4. **Result:** Read remainders in reverse order (Last remainder = **MSD**).

---

### 2.2 Successive Multiplication Procedure (Fractions)
1. **Multiply** decimal fraction by target base $r$.
2. **Record integer part** (First integer = **MSD**).
3. **Repeat** using only the remaining fractional part.
4. **Stop** when fractional part is **0** or precision is reached.
5. **Result:** Read integers in order (top-to-bottom) after the radix point.

---

### 2.3 General Formula
For a number $N$ with integer and fractional parts in base $r$:
$$N = \sum_{i=0}^{n} (d_i r^i) + \sum_{j=1}^{m} (a_{-j} r^{-j})$$

Where:
* $d_i$ are remainders from division (Integer part).
* $a_{-j}$ are integers from multiplication (Fractional part).

---

## 3. Two's Complement Representation

### 3.1 Sign Bit ($n$-bit system)
* **MSB = 0** → Positive
* **MSB = 1** → Negative

---

### 3.2 Ranges
* **Unsigned:** $0 \le x \le 2^n - 1$
* **Signed (2's Complement):** $-2^{n-1} \le x \le 2^{n-1}-1$
* **Example (8-bit):** $[-128, 127]$

---

### 3.3 Forming a Negative Number
To compute $-B$:
1. **Invert** bits (NOT operation).
2. **Add 1** to the result.

**Mathematical Identity:**
$$-B = 2^n - B$$

---

## 4. Subtraction Using Two's Complement
Instead of $A - B$, the CPU computes $A + (-B)$.  
Since $-B = 2^n - B$, the hardware performs:
$$A - B \equiv A + (2^n - B) \pmod{2^n}$$

---

## 5. Modular Arithmetic
Computers store integers within fixed bounds: $0 \le x \le 2^n - 1$. All arithmetic is performed $\pmod{2^n}$.

---

### 5.1 Overflow
Overflow occurs when the result exceeds the representable signed range, causing the value to "wrap" into an incorrect sign.

**Clock Analogy ($\pmod{12}$):**
* $18 \equiv 6 \pmod{12}$ (18:00 is effectively 6:00).
* Since $12 \equiv 0 \pmod{12}$, the number "wraps" once capacity is reached.

**Example (4-bit):**
* $7 + 3 = 10 \rightarrow (1010_2)$.
* Signed range is $[-8, 7]$. 
* Since $10 > 7$, the result wraps to a negative value (-3).