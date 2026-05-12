# Digital Hardware Implementation

## 1. The Design Space
The **Design Space** describes the target technologies available for a design and the parameters (metrics) used to characterize them.
* **Target Technology:** Specifies the primitive elements (gates, flip-flops) and their physical properties.
* **Parameters:** Metrics such as speed (propagation delay), power consumption, and silicon area used to evaluate design trade-offs.

---

## 2. Integrated Circuits (ICs)
An **Integrated Circuit** (or **chip**) is a silicon semiconductor crystal containing the components (transistors, resistors, etc.) and connections that constitute a digital circuit.

---

## 3. Levels of Integration
Hardware complexity is categorized by the number of gates per chip:

| Level | Name | Gate Count | Typical Applications |
| :--- | :--- | :--- | :--- |
| **SSI** | Small-Scale Integration | < 10 | Individual gates, simple latches |
| **MSI** | Medium-Scale Integration | 10 – 100 | Adders, MUXs, Decoders, Counters |
| **LSI** | Large-Scale Integration | 100 – 10,000 | 8-bit CPUs, memory chips |
| **VLSI** | Very Large-Scale Integration | > 10,000 | Modern processors, complex FPGAs |

---

## 4. CMOS Technology
**CMOS** (Complementary Metal-Oxide Semiconductor) is the industry-standard fabrication technology for high-density chips.



* **Structure:** Uses paired **NMOS** and **PMOS** transistors.
* **Function:** Because one transistor is always OFF while the other is ON (complementary), the circuit draws almost zero power when in a steady state (static).

---

## 5. MOS Transistor Structure
The **MOS** (Metal-Oxide-Semiconductor) transistor is the fundamental component of CMOS technology, acting as a voltage-controlled switch.

![MOS Transistor Diagram](images/mos.png)

### 5.1 Physical Components
* **Substrate:** The base silicon wafer material.
* **Source & Drain:** Conductive regions where current enters and exits.
* **Gate:** The control terminal that determines if the switch is ON or OFF.
* **Insulator:** A thin oxide layer that prevents current from leaking from the gate into the substrate.
* **Channel:** The gap under the gate that connects the source and drain when a specific voltage is applied.

### 5.2 Operation (Switch Model)
* **ON State:** When gate voltage exceeds a **threshold**, a conductive "bridge" (channel) forms, allowing current to flow.
* **OFF State:** When gate voltage is below the threshold, the channel disappears, blocking current.

---

## 6. Transistor Types: nMOS vs. pMOS
CMOS circuits use two types of MOS transistors to ensure signals remain "strong" (reaching full voltage levels).

### 6.1 nMOS (n-channel)
![nMOS Transistor](images/nmos.png)

* **Logic:** Turns **ON** when Gate is **High (1)**.
* **Strength:** Passes a **Strong 0** (Full Ground).
* **Weakness:** Passes a **Weak 1**. It shuts itself off before the output reaches the full supply voltage because the "gap" between the gate and output disappears.
* **Network:** Used in the **Pull-Down Network** (connecting output to Ground).

### 6.2 pMOS (p-channel)
![pMOS Transistor](images/pmos.png)

* **Logic:** Turns **ON** when Gate is **Low (0)**. (Symbol has a **bubble** $\circ$).
* **Strength:** Passes a **Strong 1** (Full $V_{DD}$).
* **Weakness:** Passes a **Weak 0**. It shuts itself off before the output reaches 0V.
* **Network:** Used in the **Pull-Up Network** (connecting output to $V_{DD}$).

---

### 7. Comparison Summary Table

| Feature | nMOS | pMOS |
| :--- | :--- | :--- |
| **Gate Symbol** | No bubble | Bubble ($\circ$) |
| **ON State** | $V_G = 1$ (High) | $V_G = 0$ (Low) |
| **Strong Signal** | **0** (Ground) | **1** ($V_{DD}$) |
| **Weak Signal** | **1** (Faded) | **0** (Faded) |
| **Placement** | Pull-Down Network | Pull-Up Network |

## 8. nMOS Logic Gates
nMOS logic relies on a **Pull-Down Network** of transistors to create a path to Ground (0) and a **Pull-Up Resistor** to provide a path to $V_{DD}$ (1).

### 8.1 The Pull-Up / Pull-Down Mechanism
* **Pull-Down (nMOS):** When transistors are **ON**, they "pull" the output voltage down to **0**.
* **Pull-Up (Resistor):** When transistors are **OFF**, the resistor "pulls" the output voltage up to **1**.
* **Power Note:** If transistors are ON, current flows through the resistor directly to Ground, causing static power consumption.

### 8.2 NAND vs. NOR Configuration
The arrangement of nMOS transistors in the Pull-Down Network defines the logic:

| Gate | Configuration | Logic (Pull-Down Action) |
| :--- | :--- | :--- |
| **NOR** | **Parallel** | If **A OR B** is 1, output is pulled to **0**. |
| **NAND** | **Series** | Only if **A AND B** are 1, output is pulled to **0**. |



### 8.3 nMOS AND Gate
Because nMOS stages are inherently inverting, an AND gate is built by following a NAND configuration with an Inverter stage.

![nMOS AND Gate](images/nmos_and.png)

* **Operation:** The first stage (Series) performs the NAND function. The second stage (Inverter) flips the result to produce the AND logic.

---

## 9. Noise Margin
**Noise Margin** is the measure of a circuit's robustness against electrical interference. it defines the maximum noise voltage that can be added to a signal without causing a logic error.

### 9.1 The Voltage Thresholds
To ensure reliable communication between a **driver** (sender) and a **receiver**, four voltage levels are defined:
* **$V_{OH}$ (Output High):** The minimum voltage the driver sends as a '1'.
* **$V_{OL}$ (Output Low):** The maximum voltage the driver sends as a '0'.
* **$V_{IH}$ (Input High):** The minimum voltage the receiver needs to recognize a '1'.
* **$V_{IL}$ (Input Low):** The maximum voltage the receiver needs to recognize a '0'.



### 9.2 Calculating the Safety Buffer
The noise margin is the "gap" between what the driver sends and what the receiver requires.

* **Low Noise Margin ($NM_L$):** Protects the Logic 0 state.
  $$NM_L = V_{IL} - V_{OL}$$
  *In nMOS, $V_{IL}$ is determined by the transistor threshold, while $V_{OL}$ is determined by the $R_{ON}/R$ ratio of the transistor and pull-up resistor.*

* **High Noise Margin ($NM_H$):** Protects the Logic 1 state.
  $$NM_H = V_{OH} - V_{IH}$$


### 9.3 The Forbidden Region
The voltage range between $V_{IL}$ and $V_{IH}$ is the **uncertain (forbidden) region**. If noise pushes a signal into this range, the receiver may misinterpret the data or behave unpredictably. Stronger noise margins mean the circuit is less likely to enter this region.

---

## 10. The Power vs. Speed Trade-off
In nMOS logic, the pull-up resistor ($R$) creates a fundamental conflict between energy efficiency and performance.

### 10.1 Power Dissipation (The Static Problem)
* **Mechanism:** When the output is Logic 0, the nMOS transistor is ON, creating a direct path from $V_{DD}$ to Ground.
* **Requirement:** To minimize power dissipation ($P = V^2/R$), we need a **High Resistance ($R$)**.
* **Impact:** High $R$ limits the static current flowing to ground, preventing overheating.



### 10.2 Switching Speed (The Dynamic Problem)
* **Mechanism:** To switch from 0 to 1, the resistor must charge the load capacitance ($C$) of the next gate.
* **Requirement:** For high speed, we need a **Low Resistance ($R$)**.
* **Impact:** High $R$ creates a large RC time constant ($\tau = R \times C$), causing a slow "pull-up" transition and high propagation delay.



### 10.3 Summary Table

| Design Goal | Resistance ($R$) | Result |
| :--- | :--- | :--- |
| **Low Power** | **High $R$** | Low static current, but **Slow** switching. |
| **High Speed** | **Low $R$** | Fast capacitor charging, but **High** power waste. |

---

## 11. CMOS (Complementary MOS)
CMOS improves on nMOS logic by replacing the passive pull-up resistor with an active **pMOS transistor**. This creates a "complementary" pair where one transistor is always OFF when the other is ON.



### 11.1 How CMOS Solves the Problems
* **Static Power:** Since the pMOS and nMOS are never ON at the same time, there is no direct path from $V_{DD}$ to Ground. Static power consumption is **near zero**; current only flows during the brief moment of switching.
* **Switching Speed:** The pMOS acts as a low-resistance switch. It charges the load capacitance of the next gate much faster than a resistor, significantly reducing propagation delay.
* **Signal Strength:** CMOS provides **Rail-to-Rail** outputs. Because pMOS passes a strong 1 and nMOS passes a strong 0, the output always reaches the full supply voltage ($V_{DD}$) or true ground.

### 11.2 nMOS vs. CMOS Comparison

| Feature | nMOS Logic (Resistor) | CMOS Logic |
| :--- | :--- | :--- |
| **Static Power** | High (Leaks current at Logic 0) | **Near Zero** |
| **Pull-Up Speed** | Slow (Limited by Resistor) | **Fast** (Active pMOS) |
| **Logic Levels** | Weak 1s / Strong 0s | **Strong 1s & 0s** |
| **Full Swing** | No (Output < $V_{DD}$) | **Yes** (Rail-to-Rail) |

---

### 11.3 CMOS NAND Gate
The CMOS NAND gate uses a **Pull-Up Network (PUN)** of pMOS and a **Pull-Down Network (PDN)** of nMOS. These networks are duals, acting as complementary switches.

![CMOS NAND Gate](images/cmos_nand.png)

#### **Logic Mechanism**
* **Pull-Up (pMOS in Parallel):** If **either** input is **0**, at least one pMOS transistor turns ON, creating a path to $V_{DD}$. The output is pulled to **1**.
* **Pull-Down (nMOS in Series):** The path to Ground is only completed if **both** inputs are **1**. This pulls the output down to **0**.



#### **Transistor State Summary**

| Input A | Input B | PUN (pMOS) | PDN (nMOS) | Output |
| :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | **ON** (Both) | OFF | **1** |
| 0 | 1 | **ON** (A) | OFF | **1** |
| 1 | 0 | **ON** (B) | OFF | **1** |
| 1 | 1 | OFF | **ON** (Both) | **0** |

### 11.4 CMOS Gate Summary (NOT, NOR, NAND)
CMOS logic follows a consistent pattern: pMOS transistors in the Pull-Up Network (PUN) are always the "dual" of the nMOS transistors in the Pull-Down Network (PDN).

![CMOS NOT, NOR, NAND Summary](images/cmos_sum.png)

#### **Structural Comparison**

| Gate | Pull-Up Network (pMOS) | Pull-Down Network (nMOS) |
| :--- | :--- | :--- |
| **NOT** | Single Transistor | Single Transistor |
| **NOR** | **Series** (Needs A=0 AND B=0 for Output 1) | **Parallel** (Any 1 pulls to 0) |
| **NAND** | **Parallel** (Any 0 pulls to 1) | **Series** (Needs A=1 AND B=1 for Output 0) |



---

## 12. Programming Technologies
Programming technologies define how logical connections are physically established within a device. They are categorized by their permanence and the physical mechanism used to store the "program."

### 12.1 Volatile vs. Non-Volatile
* **Volatile:** Requires constant power to maintain stored information. Data is lost immediately when power is removed (e.g., **SRAM**).
* **Non-Volatile:** Retains information even without power (e.g., **Mask programming, Fuses, EEPROM, Flash**).

### 12.2 Key Technologies

#### **1. Mask Programming (Non-Volatile)**
* **Mechanism:** Connections are hard-wired during the silicon fabrication process using a custom photomask.
* **Use Case:** High-volume mass production where the design is finalized.
* **Trade-off:** Lowest unit cost but zero flexibility; any change requires a full manufacturing restart.



#### **2. Fuse and Antifuse (Non-Volatile / One-Time)**
* **Fuse:** Starts as a closed circuit. High current "blows" the link to create an open circuit (Logic 0).
* **Antifuse:** Starts as an open circuit. High voltage melts a thin insulating layer to create a permanent low-resistance connection (Logic 1).
* **Use Case:** One-Time Programmable (OTP) devices; highly reliable and permanent.



#### **3. SRAM-based / nMOS Switch (Volatile)**
* **Mechanism:** A 6-transistor **SRAM** cell stores a configuration bit. This bit controls the gate of an **nMOS transistor** acting as a pass-switch.
* **Operation:** If the SRAM bit is '1', the nMOS switch is ON, connecting two wires. If '0', the switch is OFF.
* **Use Case:** Modern FPGAs. It is extremely fast and reprogrammable, but must be re-loaded from an external chip at every boot-up.



#### **4. Floating Gate / EEPROM & Flash (Non-Volatile)**
* **Mechanism:** Uses a specialized transistor with a "Floating Gate" completely encased in insulation.
* **Programming:** Electrons are forced onto the floating gate via "tunneling." These trapped electrons create an electric field that keeps the transistor in a set state even without power.
* **EEPROM:** Electrically Erasable Programmable ROM. Can be erased and rewritten byte-by-byte.
* **Flash:** High-density version of EEPROM that erases in large blocks.



### 12.3 Summary Table

| Technology | Re-programmable | Volatile | Mechanism |
| :--- | :--- | :--- | :--- |
| **Mask** | No | No | Metal layer "stencils" |
| **Fuse** | No (One-time) | No | Physical break/link |
| **SRAM** | **Yes** | **Yes** | Memory-controlled nMOS switch |
| **EEPROM** | **Yes** | No | Trapped charge (Floating Gate) |
| **Flash** | **Yes** | No | High-density trapped charge |

---

## 13. PLDs vs. Custom VLSI (ASICs)
This section outlines the strategic and technical trade-offs between standard programmable components and custom-manufactured silicon.

### 13.1 Programmable Logic Devices (PLDs)
* **Definition:** Standard off-the-shelf components produced in high volumes that can be configured by the user to implement a wide variety of logic functions.
* **Mechanism:** They consist of an array of logic gates, flip-flops, and I/O pins connected by programmable switches (SRAM, Antifuse, or Flash).
* **Flexibility:** High; mistakes can be corrected by simply updating the configuration bitstream.

### 13.2 Custom VLSI / ASICs
* **Definition:** Application-Specific Integrated Circuits designed for a single, unique application and manufactured that way from the start.
* **Mechanism:** The logic is physically etched into the silicon using custom photomasks (Mask Programming).
* **Flexibility:** Zero; once the chip is fabricated, the internal hardware logic is permanent and cannot be changed.

### 13.3 Comparative Trade-offs (Design Considerations)

| Factor | PLD (FPGA/CPLD) | Custom VLSI (ASIC) |
| :--- | :--- | :--- |
| **NRE Cost** | **Low:** No expensive mask sets required. | **High:** Millions of dollars for initial fabrication. |
| **Unit Cost** | **High:** Expensive for individual units. | **Low:** Most cost-effective for mass production. |
| **Speed** | **Medium:** Signals pass through programmable interconnects. | **Highest:** Optimized, direct signal paths. |
| **Power** | **Medium:** Higher overhead for universal routing. | **Lowest:** Maximum energy efficiency. |
| **Time-to-Market**| **Fast:** Design can be tested and deployed in days. | **Slow:** Requires months/years for factory cycles. |
| **Risk** | **Low:** Mistakes can be fixed via software updates. | **High:** A single bug requires a total silicon redesign. |



### 13.4 Security and Reliability
* **Security:** ASICs offer the highest security against reverse engineering as they require physical de-layering of the silicon to inspect. SRAM-based PLDs are the most vulnerable because the configuration bitstream can be intercepted during power-up.
* **Reliability:** PLDs improve reliability by reducing the total component count on a PCB. However, in high-radiation environments (e.g., space), SRAM-based FPGAs are susceptible to bit-flips, making Antifuse PLDs or hardened ASICs a more reliable choice.



---

## 14. Memory Erasure and Array Logic structures

### 14.1 Erasure Technologies
To reprogram non-volatile memory, the "trapped" charge on the floating gates must be cleared. This is achieved through three primary methods:

* **Erasable (EPROM):** Uses **Ultraviolet (UV) light**. The chip has a quartz window, and exposure to strong UV light for a specific duration clears all stored data, allowing for a full reset.
* **Electrically Erasable (EEPROM):** Uses **higher-than-normal voltages** to remove electrons from the floating gate. This allows the chip to be erased and reprogrammed while still in the circuit.
* **Flash Technology:** A more advanced form of EEPROM. It offers multiple erase options, including clearing individual gates, specific subsets (blocks/sectors), or the entire chip at once.



### 14.2 Array Logic Symbology
To simplify complex diagrams with high fan-in (many inputs), a concise notation is used. Instead of drawing every individual wire into a gate:
* A **single line** is drawn leading into the gate.
* Input lines are drawn **perpendicular** to this main line.
* **Connection (Closed):** Marked with an **'x'** at the intersection.
* **No Connection (Open):** No mark is present at the intersection.



### 14.3 Programmable Device Architectures
The fundamental difference between these three types of PLDs is which internal "array" (AND or OR) is programmable.

#### **1. PROM (Programmable Read-Only Memory)**
* **AND Array:** Fixed (operates as a decoder).
* **OR Array:** **Programmable**.
* **Logic Style:** Implements a "Sum-of-Minterms" structure, essentially functioning as a hardware truth table or memory lookup.

#### **2. PAL (Programmable Array Logic)**
* **AND Array:** **Programmable** (creates custom product terms).
* **OR Array:** Fixed.
* **Logic Style:** Faster and simpler to implement than PLA, though each output is restricted to a fixed number of product terms.

#### **3. PLA (Programmable Logic Array)**
* **AND Array:** **Programmable**.
* **OR Array:** **Programmable**.
* **Logic Style:** The most flexible architecture. Any product term from the AND array can be connected to any OR gate in the output array.



#### **Comparison Summary**

| Device Type | AND Array | OR Array | Use Case |
| :--- | :--- | :--- | :--- |
| **PROM** | Fixed | **Programmable** | Truth tables, firmware storage |
| **PAL** | **Programmable** | Fixed | General combinational logic |
| **PLA** | **Programmable** | **Programmable** | Complex, optimized logic functions |

---