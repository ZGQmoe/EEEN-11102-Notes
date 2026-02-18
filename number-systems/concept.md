# Number Systems and Binary Arithmetic

---

## 1. Number Systems

### 1.1 Binary (Base 2)
Digits: $0, 1$  
Weights: $$2^n$$

**Example:**
$$(1011)_2 = 1\cdot2^3 + 0\cdot2^2 + 1\cdot2^1 + 1\cdot2^0 = 11_{10}$$

---

### 1.2 Octal (Base 8)
Digits: $0$–$7$  
Weights: $$8^n$$

**Binary to Octal:** Group bits in 3s.
**Example:** $$(110101)_2 = (65)_8$$

---

### 1.3 Hexadecimal (Base 16)
Digits: $0$–$9$, $A$–$F$  
Weights: $$16^n$$

**Binary to Hex:** Group bits in 4s.
**Example:** $$(11111010)_2 = (FA)_{16}$$

---

## 2. Binary Arithmetic

### 2.1 Addition Rules
$$0+0=0$$
$$0+1=1$$
$$1+1=10$$
$$1+1+1=11$$

**Example:**
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
If $0 - 1$, borrow from the higher bit.

---

## 3. Two's Complement Representation

### 3.1 Sign Bit (n-bit system)
* **MSB = 0:** Positive  
* **MSB = 1:** Negative  

---

### 3.2 Ranges
* **Unsigned:** $0 \le x \le 2^n - 1$
* **Signed (2's Complement):** $-2^{n-1} \le x \le 2^{n-1}-1$
    * *Example (8-bit):* $[-128, 127]$

---

### 3.3 Forming a Negative Number
To compute $-B$:
1. Invert bits (NOT)
2. Add 1  

**Mathematical identity:**
$$-B = 2^n - B$$

---

## 4. Subtraction Using Two's Complement
Instead of $A - B$, compute $A + (-B)$.

Because $-B = 2^n - B$, the operation is:
$$A - B = A + (2^n - B)$$

All arithmetic is performed:
$$\text{mod } 2^n$$

---

## 5. Modular Arithmetic
Computers store integers within fixed bounds: $0 \le x \le 2^n - 1$.



**Clock Analogy (mod 12):**
$18 \equiv 6 \pmod{12}$ (18:00 is 6:00).
Because $12 \equiv 0 \pmod{12}$, the number "wraps" after reaching capacity.

---

## 6. Overflow
Overflow occurs when a result exceeds the representable signed range, causing it to "wrap" into an incorrect value.

**Detection Rules:**
1. **Hardware Level:** $$\text{Carry into MSB} \neq \text{Carry out of MSB}$$
2. **Logic Level:** Same sign operands result in a different sign output.



**Example (4-bit):**
$7 + 3 = 10 (1010_2)$.
Signed range is $[-8, 7]$. 
Since $10 > 7$, the result wraps to a negative number $\rightarrow$ **Overflow**.