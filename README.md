# Circuits Project 1: Diode Logic Gates & Multi-Output Power Supply

Course project for **CSAI 205: Fundamentals of Circuits and Electronics**
University of Science and Technology, Zewail City

Each circuit in this project was **simulated in Proteus first**, then **built and tested on a breadboard**.

| Part | Topic | Folder |
|---|---|---|
| 1 | Diode-based logic gates (OR, AND, NOR, NAND) | [`part1-diode-logic-gates`](part1-diode-logic-gates) |
| 2 | Multi-output regulated power supply (220 V AC to 12 V, 9 V, 5 V DC) | [`part2-power-supply`](part2-power-supply) |

---

## Part 1: Diode-Based Logic Gates

Basic logic functions built with only diodes, resistors, push buttons and LEDs (no logic ICs).

| Gate | Output is HIGH when | How it works |
|---|---|---|
| **OR** | at least one input is HIGH | Diodes (anode toward the button) join at the output. A pressed button pushes about 4.3 V to the output. A pull-down resistor keeps the output LOW otherwise. |
| **AND** | both inputs are HIGH | Diodes are reversed (cathode toward the button) and the output is pulled up to +5 V. Any LOW input pulls the output down through its diode. |
| **NOR** | both inputs are LOW | An OR diode stage, with the LED connected between +5 V and the output node. The LED lights when the node is LOW. |
| **NAND** | any input is LOW | An AND diode stage, with the LED connected between +5 V and the output node. The LED lights when the node is LOW. |

**Truth tables**

| A | B | OR | AND | NOR | NAND |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 1 | 1 |
| 0 | 1 | 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 0 | 0 |

**Things worth knowing**

- A conducting silicon diode drops about 0.7 V, so the HIGH level of the OR gate is about 4.3 V rather than 5 V.
- Diodes alone cannot invert a signal. In the NOR and NAND circuits the inversion is achieved by wiring the LED to +5 V so it lights when the node is LOW. This is a known limitation of diode logic.
- In the NAND circuit, with both pull resistors at 1 kΩ the LED only dimmed instead of turning off. A voltage divider keeps the node near 3 V, which still lets a small current flow through the LED. Lowering the pull-up resistor to 220 Ω raised the node voltage and the LED turned off.


---

## Part 2: Multi-Output Regulated Power Supply

Converts **220 V AC** into three stable DC outputs: **+12 V, +9 V and +5 V**.

```
220 V AC -> Transformer -> Bridge rectifier -> Filter capacitor -> Regulators -> 12 V / 9 V / 5 V
```

| Stage | Component | Purpose |
|---|---|---|
| Step-down | Center-tapped transformer, 220 V to 6-0-6 V | About 12 V AC between the outer terminals; also isolates the circuit from the mains |
| Rectifier | 4 x 1N4001 (bridge) | AC to pulsating DC at 100 Hz (about 1.4 V lost in two diodes) |
| Filter | 1000 uF / 50 V electrolytic | Smooths the pulsating DC |
| Regulators | 7812, 7809, 7805 | Fixed 12 V, 9 V and 5 V outputs |
| Decoupling | 3 x 1 nF | Filters high-frequency noise at each output |
| Indicators | LED + 430 / 330 / 220 ohm resistors | Shows each output is alive |

**Expected values**

| Point | Expected |
|---|---|
| Transformer secondary (AC) | about 12 V RMS |
| Across the filter capacitor (DC) | about 15 to 16 V under load |
| 7812 / 7809 / 7805 outputs | 12 V / 9 V / 5 V |

The 7812 needs roughly 14 V at its input (about 2 V dropout), so the filtered voltage must stay above that.

**Problems faced**

- The transformer wires are unlabeled. The primary (yellow, about 400 ohm) and secondary (blue and black, low resistance) were identified with a multimeter before connecting anything.
- The two primary leads are thin, bare wires that carry mains voltage, so they cannot go on a breadboard. See the report for how the connection was made.
- Regulator pin order was checked before wiring (78xx, printed face toward you, legs down: input, ground, output).



> **Safety:** Part 2 involves 220 V mains on the transformer primary. If you build it, insulate every mains connection, keep the mains side off the breadboard, disconnect power before any change, and have someone experienced check the wiring first. Check electrolytic capacitor polarity before powering on.

---

## Repository Structure

```
.
├── README.md
├── part1-diode-logic-gates/
│   ├── proteus/      Proteus project file
│   ├── report/       PDF report
│   └── images/       Screenshots and breadboard photos
└── part2-power-supply/
    ├── proteus/
    ├── report/
    └── images/
```

## Tools

- Proteus (schematic capture and simulation)
- Breadboard, digital multimeter

## How to Open the Simulations

1. Install Proteus (version 8 or later).
2. Open the `.pdsprj` file from the `proteus` folder of the part you want.
3. Press **Play** (bottom-left) and click the buttons in Part 1, or watch the voltmeters in Part 2.

## Author

**Hamza Elsayed**
Zewail City, University of Science and Technology
