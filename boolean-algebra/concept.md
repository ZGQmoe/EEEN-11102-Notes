## 1. Logic Gates

---

### 1.1 Fundamental Logic Gates

#### 1.1.1 NOT Gate (Inverter)
* **Function:** Inverts input ($Y = \bar{A}$).
* **Truth Table:**

| $A$ | $Y$ |
| :--- | :--- |
| 0 | 1 |
| 1 | 0 |



[Image of NOT gate symbol and truth table]


---

#### 1.1.2 AND Gate
* **Function:** $Y=1$ only if all inputs are 1 ($Y = A \cdot B$).
* **Truth Table:**

| $A$ | $B$ | $Y$ |
| :--- | :--- | :--- |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |



[Image of AND gate symbol and truth table]


---

#### 1.1.3 OR Gate
* **Function:** $Y=1$ if at least one input is 1 ($Y = A + B$).
* **Truth Table:**

| $A$ | $B$ | $Y$ |
| :--- | :--- | :--- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |



[Image of OR gate symbol and truth table]


---

### 1.2 Universal Gates

#### 1.2.1 NAND Gate
* **Function:** $Y=0$ only if all inputs are 1 ($Y = \overline{A \cdot B}$).
* **Truth Table:**

| $A$ | $B$ | $Y$ |
| :--- | :--- | :--- |
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |



[Image of NAND gate symbol and truth table]


---

#### 1.2.2 NOR Gate
* **Function:** $Y=1$ only if all inputs are 0 ($Y = \overline{A + B}$).
* **Truth Table:**

| $A$ | $B$ | $Y$ |
| :--- | :--- | :--- |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |



[Image of NOR gate symbol and truth table]


---

### 1.3 Exclusive Gates

#### 1.3.1 XOR (Exclusive-OR)
* **Function:** $Y=1$ if inputs are different ($Y = A \oplus B$).
* **Truth Table:**

| $A$ | $B$ | $Y$ |
| :--- | :--- | :--- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |



[Image of XOR gate symbol and truth table]


---

#### 1.3.2 XNOR (Exclusive-NOR)
* **Function:** $Y=1$ if inputs are the same ($Y = \overline{A \oplus B}$).
* **Truth Table:**

| $A$ | $B$ | $Y$ |
| :--- | :--- | :--- |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |



[Image of XNOR gate symbol and truth table]


---

## 2. Boolean Algebra

### 2.1 Basic Identities

| No. | Identity (OR Form) | Identity (AND Form) | Description |
| :--- | :--- | :--- | :--- |
| 2.1.1 | $X + 0 = X$ | $X \cdot 1 = X$ | Identity Law |
| 2.1.2 | $X + 1 = 1$ | $X \cdot 0 = 0$ | Null Law |
| 2.1.3 | $X + X = X$ | $X \cdot X = X$ | Idempotent Law |
| 2.1.4 | $X + \bar{X} = 1$ | $X \cdot \bar{X} = 0$ | Complement Law |
| 2.1.5 | $\overline{\bar{X}} = X$ | — | Involution |

---

### 2.2 Algebraic Laws

| Law | OR Form | AND Form |
| :--- | :--- | :--- |
| **2.2.1 Commutative** | $X + Y = Y + X$ | $XY = YX$ |
| **2.2.2 Associative** | $X + (Y + Z) = (X + Y) + Z$ | $X(YZ) = (XY)Z$ |
| **2.2.3 Distributive** | $X(Y + Z) = XY + XZ$ | $X + YZ = (X + Y)(X + Z)$ |

---

### 2.3 DeMorgan’s Theorems
* **2.3.1 Theorem 1:** $\overline{X + Y} = \bar{X} \cdot \bar{Y}$
* **2.3.2 Theorem 2:** $\overline{X \cdot Y} = \bar{X} + \bar{Y}$

---

### 2.4 Duality Principle
An equation remains valid if:
1. All **OR** ($+$) operators are replaced by **AND** ($\cdot$).
2. All **AND** ($\cdot$) operators are replaced by **OR** ($+$).
3. All **0**s are replaced by **1**s and vice-versa.

---

### 2.5 Consensus Theorem
Allows removal of redundant terms covered by two other terms.

* **2.5.1 SOP Form:** $XY + \bar{X}Z + YZ = XY + \bar{X}Z$
* **2.5.2 POS Form (Dual):** $(X + Y)(\bar{X} + Z)(Y + Z) = (X + Y)(\bar{X} + Z)$

---

### 2.6 Boolean Expression Terminology
* **Literal:** Single variable in normal ($A$) or complemented ($\bar{A}$) form.
* **Product Term:** Literals connected by AND (e.g., $AB$).
* **Sum Term:** Literals connected by OR (e.g., $A+B$).
* **Sum of Products (SOP):** Product terms ORed together.
* **Product of Sums (POS):** Sum terms ANDed together.

---

### 2.7 Minterms and Maxterms
Every truth table row is mapped to a specific Minterm ($m_j$) and Maxterm ($M_j$).

* **Subscript ($j$):** The decimal equivalent of the binary input row (e.g., row $ABC=101$ is subscript $5$).
* **Minterm ($m_j$):** Product term that equals **1** for its row. (Binary $0 \to \bar{X}$, $1 \to X$).
* **Maxterm ($M_j$):** Sum term that equals **0** for its row. (Binary $0 \to X$, $1 \to \bar{X}$).
* **Relationship:** $\bar{m_j} = M_j$



---

### 2.8 Function Complement ($\bar{F}$)
Two methods to find the complement of a function:

1. **DeMorgan’s:** Interchange AND/OR operators and complement every literal.
2. **Duality Shortcut:** Find the Dual ($+\leftrightarrow \cdot$ and $0 \leftrightarrow 1$) then complement every literal.

| Feature | Duality | Complement ($\bar{F}$) |
| :--- | :--- | :--- |
| **Operators** | $+\leftrightarrow \cdot$ | $+\leftrightarrow \cdot$ |
| **Constants** | $0 \leftrightarrow 1$ | $0 \leftrightarrow 1$ |
| **Literals** | No Change | $X \leftrightarrow \bar{X}$ |

---

### 2.9 Implicants

* **Implicant:** Any product term (grouping of 1s) where the function is **1**.
* **Prime Implicant (PI):** The largest possible grouping of 1s; cannot be further expanded.
* **Essential Prime Implicant (EPI):** A PI covering at least one '1' not covered by any other PI. **Mandatory** for the final expression.
* **Redundant PI:** A PI whose 1s are already entirely covered by EPIs. **Discarded** during minimization.



| Term | K-Map Visual | Requirement |
| :--- | :--- | :--- |
| **PI** | Max-sized circle | Candidate |
| **EPI** | Only circle for a specific '1' | **Mandatory** |
| **Redundant** | Overlaps existing EPIs | **Exclude** |

---

### 2.10 Complement POS
The complement of a function in POS form ($\bar{F}$) uses the Maxterms ($M_j$) of the rows where the original function $F$ is **1**.

* **Rule:** If $F = \sum m(1, 4, 6)$, then $\bar{F} = \prod M(1, 4, 6)$.
* **Logic:** Each Maxterm $M_j$ is the complement of the Minterm $m_j$ ($\bar{m_j} = M_j$).

| Form | Indices Used |
| :--- | :--- |
| **$F$ (SOP)** | Rows where output is **1** |
| **$\bar{F}$ (POS)** | Rows where output is **1** |