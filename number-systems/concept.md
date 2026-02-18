# Digital Logic & Computer Arithmetic

## 1. Number Systems
* **Binary (Base 2):** Digits $\{0, 1\}$.
* **Octal (Base 8):** Digits $\{0-7\}$. One octal digit $\equiv$ 3 bits.
* **Hexadecimal (Base 16):** Digits $\{0-9, A-F\}$. One hex digit $\equiv$ 4 bits.

## 2. Modular Arithmetic & Clock Analogy
Hardware uses a fixed word size of $n$ bits. Operations are performed $\pmod{2^n}$.
* **Storage:** Only values in $[0, 2^n - 1]$ are stored.
* **Wrap-around:** Similar to a clock, $n \equiv 0 \pmod n$. 
    * Example ($n=4$): $18 \equiv 2 \pmod{16}$.



## 3. Signed Representation (2's Complement)
The **MSB** (Most Significant Bit) serves as the sign indicator:
* **0:** Positive
* **1:** Negative

### Mathematical Logic
To compute $A - B$, the CPU executes $A + (2^n - B)$.
* **Rule:** Invert bits of $B$ and add 1.
* **Signed Range:** $$\text{Range} = [-2^{n-1}, \dots, 2^{n-1} - 1]$$

## 4. Addition & Overflow
**Overflow** occurs when a result exceeds the representable signed range.

| Operation | Result Sign | Status |
| :--- | :--- | :--- |
| Positive + Positive | Negative | **Overflow** |
| Negative + Negative | Positive | **Overflow** |
| Positive + Negative | Any | **Safe (No Overflow)** |



## 5. Computation Example ($n=4$)
Calculate $5 - 3$:
1.  **$A = 5$:** $0101_2$
2.  **$B = 3$:** $0011_2$
3.  **Find $-B$ (2's Comp):** $\text{NOT}(0011) + 1 = 1101_2$
4.  **Add $A + (-B)$:**
    $$0101_2 + 1101_2 = 10010_2$$
5.  **Truncate to 4 bits:** $0010_2 = 2_{10}$