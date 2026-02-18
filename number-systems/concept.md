# Number Systems and Binary Arithmetic

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

## 2. Two's Complement Representation

### 2.1 Sign Bit ($n$-bit system)
* **MSB = 0** → Positive
* **MSB = 1** → Negative

---

### 2.2 Ranges
* **Unsigned:** $0 \le x \le 2^n - 1$
* **Signed (2's Complement):** $-2^{n-1} \le x \le 2^{n-1}-1$
* **Example (8-bit):** $[-128, 127]$

---

### 2.3 Forming a Negative Number
To compute $-B$:
1. **Invert** bits (NOT operation).
2. **Add 1** to the result.

**Mathematical Identity:**
$$-B = 2^n - B$$

---

## 3. Subtraction Using Two's Complement
Instead of $A - B$, the CPU computes $A + (-B)$.  
Since $-B = 2^n - B$, the hardware performs:
$$A - B \equiv A + (2^n - B) \pmod{2^n}$$

---

## 4. Modular Arithmetic
Computers store integers within fixed bounds: $0 \le x \le 2^n - 1$. All arithmetic is performed $\pmod{2^n}$.



### 4.1 Overflow
Overflow occurs when the result exceeds the representable signed range, causing the value to "wrap" into an incorrect sign.

**Clock Analogy ($\pmod{12}$):**
* $18 \equiv 6 \pmod{12}$ (18:00 is effectively 6:00).
* Since $12 \equiv 0 \pmod{12}$, the number "wraps" once capacity is reached.

**Example (4-bit):**
* $7 + 3 = 10 \rightarrow (1010_2)$.
* Signed range is $[-8, 7]$. 
* Since $10 > 7$, the result wraps to a negative value (-3).