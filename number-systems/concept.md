# Number Systems & Binary Arithmetic

---

## 1. Number Systems

### Binary (Base 2)
Digits: `0, 1`  
Weights:
$begin:math:display$
2\^n
$end:math:display$

Example:
$begin:math:display$
\(1011\)\_2 \= 1\\cdot2\^3 \+ 0\\cdot2\^2 \+ 1\\cdot2\^1 \+ 1\\cdot2\^0 \= 11\_\{10\}
$end:math:display$

---

### Octal (Base 8)
Digits: `0–7`  
Weights:
$begin:math:display$
8\^n
$end:math:display$

Binary → Octal: group bits in 3s.

---

### Hexadecimal (Base 16)
Digits: `0–9, A–F`  
Weights:
$begin:math:display$
16\^n
$end:math:display$

Binary → Hex: group bits in 4s.

---

## 2. Binary Arithmetic

### Addition Rules
$begin:math:display$
0\+0\=0
$end:math:display$
$begin:math:display$
0\+1\=1
$end:math:display$
$begin:math:display$
1\+1\=10
$end:math:display$
$begin:math:display$
1\+1\+1\=11
$end:math:display$

---

### Subtraction Rule
$begin:math:display$
0\-1 \\Rightarrow \\text\{borrow\}
$end:math:display$

---

## 3. 2’s Complement (Signed Integers)

### Sign Bit
- MSB = 0 → positive  
- MSB = 1 → negative  

---

### Ranges (n bits)

Unsigned:
$begin:math:display$
0 \\to 2\^n \- 1
$end:math:display$

Signed:
$begin:math:display$
\[\-2\^\{n\-1\}\,\\\; 2\^\{n\-1\}\-1\]
$end:math:display$

---

### Negative Number

To compute $begin:math:text$\-B$end:math:text$:

1. Invert bits  
2. Add 1  

$begin:math:display$
\-B \= 2\^n \- B
$end:math:display$

---

## 4. Subtraction Using 2’s Complement

$begin:math:display$
A \- B \= A \+ \(\-B\)
$end:math:display$

Since:
$begin:math:display$
\-B \= 2\^n \- B
$end:math:display$

Arithmetic is performed:
$begin:math:display$
\\text\{mod \} 2\^n
$end:math:display$

---

## 5. Modular Arithmetic

Computers store values:
$begin:math:display$
0 \\to 2\^n \- 1
$end:math:display$

Clock analogy:
$begin:math:display$
n \\equiv 0 \\pmod\{n\}
$end:math:display$

Example:
$begin:math:display$
18 \\equiv 6 \\pmod\{12\}
$end:math:display$

---

## 6. Overflow

Occurs when result exceeds signed range.

Detection (2’s complement):
- Same sign inputs  
- Different sign output  

Or:
$begin:math:display$
\\text\{Carry into MSB\} \\ne \\text\{Carry out of MSB\}
$end:math:display$

---

## Key Formulas

$begin:math:display$
\\text\{Unsigned range\} \= 0 \\to 2\^n \- 1
$end:math:display$

$begin:math:display$
\\text\{Signed range\} \= \[\-2\^\{n\-1\}\, 2\^\{n\-1\}\-1\]
$end:math:display$

$begin:math:display$
A \- B \= A \+ \(2\^n \- B\)
$end:math:display$

$begin:math:display$
\\text\{Storage\} \= \\text\{mod \} 2\^n
$end:math:display$