# Combinational Logic Design

---

### 1.1 Rudimentary Logic Functions
In addition to standard gates, functions can be defined by fixing values or transferring signals.

*   **Value-Fixing:** Setting a signal to a constant logic **0** (GND) or **1** (VCC).
*   **Transferring:** Passing a variable $A$ through a buffer.
*   **Inverting:** Passing a variable $A$ through a NOT gate ($\bar{A}$).

---

### 1.2 Multiple-Bit Functions (Vectors)
Logic signals can be grouped into a **vector** $F = (F_{n-1}, \dots, F_0)$ for efficiency.

*   **Bus Notation:** A thick line or a line with a slash ($/n$) represents a bundle of $n$ wires.
*   **Index Notation:** $F(msb:lsb)$ selects a range of bits.

| Notation | Meaning | Example |
| :--- | :--- | :--- |
| **$F$** | Full vector/bus | $(0, 1, A, \bar{A})$ |
| **$F(i)$** | Single bit at index $i$ | $F(3) = 0$ |
| **$F(i:j)$** | Range of bits from $i$ to $j$ | $F(1:0) = (A, \bar{A})$ |

---

### 1.3 Enabling
Controls whether a signal passes to the output or is blocked.

*   **Logic:** A control signal (**EN**) determines if output $F$ follows data input $A$ or is forced to a fixed value (usually 0).
*   **Hardware:** Typically implemented using an **AND gate**.

| EN | A | Output (F) | State |
| :--- | :--- | :--- | :--- |
| 0 | X | 0 | **Disabled** |
| 1 | 0 | 0 | **Enabled** |
| 1 | 1 | 1 | **Enabled** |

---

## 1.4 Decoders
A combinational circuit that converts $n$ inputs into $m$ outputs, where $n \le m \le 2^n$.

*   **Logic:** Each input combination activates exactly one unique output line (minterm $m_i$).

#### 1.4.1 Decoder Truth Table (2-to-4)

| $A_1$ | $A_0$ | $D_3$ | $D_2$ | $D_1$ | $D_0$ | Minterm |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 0 | 0 | **1** | $m_0 = \bar{A_1}\bar{A_0}$ |
| 0 | 1 | 0 | 0 | **1** | 0 | $m_1 = \bar{A_1}A_0$ |
| 1 | 0 | 0 | **1** | 0 | 0 | $m_2 = A_1\bar{A_0}$ |
| 1 | 1 | **1** | 0 | 0 | 0 | $m_3 = A_1A_0$ |

#### 1.4.2 Hierarchical Decoder Design
1.  **Initialize:** Let $k = n$.
2.  **Recursive Partitioning:**
    *   **If $k$ is even:** Use $2^k$ AND gates driven by two decoders of size $2^{k/2}$.
    *   **If $k$ is odd:** Use $2^k$ AND gates driven by decoders of size $2^{(k+1)/2}$ and $2^{(k-1)/2}$.
3.  **Base Case:** Repeat until $k = 1$ (use 1-to-2 decoder).

#### 1.4.3 Decoder with Enable vs. Demultiplexer
*   **Decoder with Enable:** $EN$ pin controls overall operation ($EN=0$ disables all outputs).
*   **Demultiplexer (DEMUX):** A decoder where the **Enable pin** is used as the **Data Input**. The $n$ inputs serve as **selection lines** to route data to a specific output.

---

## 1.5 Encoders
The inverse of a decoder; converts $2^n$ inputs into an $n$-bit binary code.

*   **Logic:** Generates binary code $i$ when the $i$-th input is active.
*   **Priority Encoder:** Resolves simultaneous inputs by encoding only the highest-index input.
*   **Valid Bit (V):** Indicates if any input is active.

#### 1.5.1 Encoder Truth Table (4-to-2 Binary)

| $D_3$ | $D_2$ | $D_1$ | $D_0$ | $A_1$ | $A_0$ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 1 | 0 | 0 |
| 0 | 0 | 1 | 0 | 0 | 1 |
| 0 | 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 0 | 0 | 1 | 1 |

---

## 1.6 Multiplexers (MUX)
A data selector directing one of $2^n$ input lines to a single output.

*   **Logic:** Controlled by $n$ **selection lines** ($S$).
*   **Function:** $Y = \sum (m_i \cdot I_i)$, where $m_i$ is the minterm of selection lines.

#### 1.6.1 MUX Truth Table (4-to-1)

| $S_1$ | $S_0$ | Output ($Y$) |
| :--- | :--- | :--- |
| 0 | 0 | $I_0$ |
| 0 | 1 | $I_1$ |
| 1 | 0 | $I_2$ |
| 1 | 1 | $I_3$ |

#### 1.6.2 Applications
*   **Data Routing:** Connecting multiple sources to one destination.
*   **Parallel-to-Serial:** Converting a bus to a bitstream.
*   **Function Generation:** Implementing logic by applying constants to data inputs.

## 1.7 Binary Adders
Arithmetic circuits for adding binary numbers.

#### 1.7.1 Half Adder (HA)
Adds two bits ($X, Y$).
*   $S = X \oplus Y$
*   $C = XY$
*   *Constraint:* No carry-in support.

#### 1.7.2 Full Adder (FA)
Adds three bits ($X, Y, Z$).
*   $S = (X \oplus Y) \oplus Z$
*   $C = XY + Z(X \oplus Y)$
*   **Structure:** Implemented using two HAs and one OR gate.

#### 1.7.3 Binary Ripple Carry Adder
A parallel adder for $n$-bit numbers.
*   **Logic:** Chains $n$ Full Adders together.
*   **Carry Propagation:** $C_{out}$ of stage $i$ becomes $C_{in}$ of stage $i+1$.
*   **Delay:** Total delay is linear relative to the number of bits ($n$) due to carry rippling.