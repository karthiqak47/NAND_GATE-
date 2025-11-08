
# CMOS NAND Gate – Schematic, Symbol, and Functional Verification (Cadence Virtuoso)

## 🎯 Objective

To design, create, and verify the operation of a **2-input CMOS NAND gate** using **Cadence Virtuoso**. The experiment involves schematic capture, symbol creation, testbench setup, and transient simulation to confirm logical behavior.

---

## 🧠 Theory

A **NAND gate** performs the logical operation:
[
Y = \overline{A \cdot B}
]

For a CMOS implementation:

* **Pull-up network (PUN):** Two **PMOS transistors in parallel** (conduct when inputs are low).
* **Pull-down network (PDN):** Two **NMOS transistors in series** (conduct when inputs are high).

This ensures:

| A | B | Y |
| - | - | - |
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |



## 🧩 Design Steps

### 1. Launch Virtuoso and Create a New Cell

1. Open **Cadence Virtuoso** from your terminal:

   ```bash
   virtuoso &
   ```
2. Open your project library (e.g., `EE_Lab` or `CMOS_LIB`).
3. Create a new cell:

   * **Cell Name:** `NAND_GATE`
   * **View Type:** `schematic`
   * **Tool:** Virtuoso Schematic Editor



### 2. Schematic Creation

1. Open **Schematic Editor**.

2. From the **Component Browser**, add:

   * **2 PMOS transistors** (from library `gpdk045`, `analogLib`, or `tsmc180nm`, depending on PDK).
   * **2 NMOS transistors**.
   * **VDD**, **GND**, and **input/output pins**.

3. **Connections:**

   * Connect the **PMOS transistors in parallel** between `VDD` and `output`.
   * Connect the **NMOS transistors in series** between `output` and `GND`.
   * Tie the **gates** of the top and bottom transistor pairs to the **inputs A and B**.
   * Label nodes: `A`, `B`, `Y`, `VDD`, `GND`.

4. Set **transistor parameters:**

   * PMOS W/L = 2 µm / 0.18 µm
   * NMOS W/L = 1 µm / 0.18 µm
   * (or adjust per technology library default)



### 3. Electrical Checks

* Go to **Check and Save** (`Design → Check and Save`) to ensure there are **no connectivity or syntax errors**.
* Fix any floating nodes or missing connections.



### 4. Create a Symbol View

1. In the schematic window:
   `Create → Cellview → From Cellview`
2. Source view: **schematic**, Target view: **symbol**.
3. Arrange input/output pins neatly:

   * Left: `A`, `B`
   * Right: `Y`
   * Top: `VDD`
   * Bottom: `GND`
4. Edit the symbol appearance (rectangle with labeled pins).
5. Save the symbol.



### 5. Create Testbench for Functional Verification

1. Create a **new cell** named `NAND_GATE_TB` (testbench).

2. Open **Schematic Editor** and **instantiate** the NAND gate symbol you just created.

3. Add:

   * **Two pulse voltage sources** (`vpulse`) for `A` and `B`.
   * **DC source** for `VDD` (e.g., 1.8 V).
   * **Ground (gnd!)** connection.
   * **Output probe** for node `Y`.

4. Configure input sources (example):

   * **V1 (A):** Pulse from 0 → 1.8 V, period = 20 ns
   * **V2 (B):** Pulse from 0 → 1.8 V, period = 40 ns, delay = 10 ns
     This ensures all input combinations are tested over time.



### 6. Simulation Setup (ADE or ADE Explorer)

1. Open **Launch → ADE L/XL/Explorer**.
2. Choose **Transient Analysis**:

   * `Stop time = 80 ns`
   * `Step size = 0.1 ns`
3. Set **Output to plot:** `V(Y)`, `V(A)`, `V(B)`
4. Click **Netlist and Run** to start the simulation.



### 7. Verify Functionality

* After simulation, open the **waveform viewer (ViVA)**.
* Verify the NAND truth table:

  * Y remains HIGH for all input combinations except when **A = B = HIGH**, Y goes LOW.


## 🧾 Results

* Successfully designed and simulated a **2-input CMOS NAND gate**.
* Verified correct logical function through transient analysis in Cadence Virtuoso.
* Output matches theoretical NAND truth table.




## 🧰 Tools Used

* **Cadence Virtuoso Schematic Editor** – circuit design
* **Cadence ADE L/XL** – simulation setup and execution
* **ViVA** – waveform viewing and analysis
* **Technology** – gpdk045 / tsmc018 / generic 180nm (any PDK)



