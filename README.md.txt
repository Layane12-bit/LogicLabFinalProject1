# Logic-Controlled Board 🔄💡

## 📌 Project Overview

This project implements a dynamic logic-controlled board featuring four switches and four colored LEDs. The system dynamically updates lamp activation sequences based on the last switch turned off. It uses memory elements, finite state machines (FSMs), and digital logic design to create a user-interactive circuit.

Special features:
- Sequence learning based on switch interactions.
- Reset logic and locking mechanism.

---

## 📁 File Descriptions

| Folder/File       | Description |
|-------------------|-------------|
| `Quartus/`  | All Quartus design files: schematics (`.bdf`), project settings (`.qsf`, `.qpf`), Verilog code |
| `Logic Lab Final Report/`           | Design documentation, FSM diagrams, truth tables |
| `images/`         | Screenshots of circuit design and hardware setup |
| `README.md`       | This documentation file |

---

## ⚙️ Setup Instructions

1. Open Quartus and load the project from `Quartus/`.
2. Compile the project and run simulation using the uploaded files 
3. Program the FPGA using the compiled `.sof` file.
4. Use the defined rules to test reset condition, cap removal, and dynamic lamp switching.

---

## 💡 Design Insights
Project Overview

This project involves the design and implementation of a Logic-Controlled Board, a dynamic switching system comprising four switches and four colored lamps—red, green, blue, and yellow. While each switch is initially linked to a lamp of the same color, the system introduces a unique behavior: the configuration of lamp activations changes based on the last switch that was turned off, allowing for real-time reconfiguration.
A key feature of the system is its ability to maintain the correct mapping between switches and lamp colors, even if the switch caps or lamp positions are rearranged. Additionally, if a switch cap is removed, the system automatically disables that switch, and it only becomes operational again once the cap is replaced—adding an interactive and intuitive user experience.
The system continuously monitors user actions, records the last switch turned off, and updates the lamp-switch behavior accordingly. This gives the impression of intelligent behavior and adaptive control. The design relies on digital logic components, memory storage elements, and finite state machines (FSMs) to deliver this functionality.
Overall, the project serves as a practical application of logic design principles and sequential circuit implementation. It highlights how foundational digital design techniques can be used to replicate or inspire real-world systems such as elevator controllers, vending machines, traffic lights, or interactive electronic games.
The system operates based on a predefined sequence of lamp activations, which dynamically adjusts depending on the last switch turned off. The default sequence is 1 → 2 → 3 → 4. However, once a user turns off a specific switch and a timeout period elapses, the system transitions to a corresponding activation sequence:
•	If Switch 1 is the last to be turned off → Sequence 1: 1 → 2 → 3 → 4
•	If Switch 2 is the last to be turned off → Sequence 2: 2 → 3 → 4 → 1
•	If Switch 3 is the last to be turned off → Sequence 3: 3 → 4 → 1 → 2 
•	If Switch 4 is the last to be turned off → Sequence 4: 4 → 3 → 2 → 1
Reset Condition:
The system performs a reset when all the following conditions are met:
1.	All switches are in the OFF state.
2.	At least one switch has already been activated (i.e., "learned").
3.	A 4-second reset timer has completed.
Locking and Unlocking Mechanism
To prevent the audience from detecting any underlying patterns in the switch-to-lamp behavior, the system includes a locking feature that disables the dynamic sequencing temporarily.
•	Locking Procedure:
To lock the device and enforce a direct switch-to-lamp mapping:
1.	Remove the power source (battery).
2.	Turn ON only Switch 2.
3.	Reinsert the battery.
Upon powering up under these conditions, the system enters a locked state, where each switch controls its corresponding lamp directly (e.g., Switch 1 → Lamp 1, Switch 2 → Lamp 2, etc.), with no sequence reconfiguration.
•	Unlocking Procedure:
To restore the system’s dynamic behavior:
o	Restart the system without Switch 2 turned ON during power-up.
The system will then operate in its default mode, dynamically adjusting the lamp sequence based on user interaction.
Finite State Machine (FSM) Design
The system is governed by a Finite State Machine (FSM) composed of distinct modular states, offering flexibility in control logic implementation. These states define the various modes of operation and transitions the system can take based on user interactions:
•	Boot State:
The initial state upon powering the system. It checks the status of Switch 2 to determine whether to proceed with normal dynamic behavior or enter the locked mode.

•	Locked State:
Entered when the system is powered on with Switch 2 in the ON position. In this state, each switch directly controls its respective lamp (e.g., Switch 1 → LED 1), and all advanced features are disabled.

•	Sequence Detector State:
A transitional state triggered after a reset condition. It identifies which switch was turned off last and updates the system to follow the corresponding lamp activation sequence.

•	Sequence States (1–4):
These represent the four operational modes of the system. Each state corresponds to a unique lamp activation pattern, based on the last switch turned off.

•	Switch NotWorking State:
A temporary state used only in Sequence 3 to simulate the removal of a switch cap. While in this state, toggling the affected switch has no effect on its associated LED. The switch becomes functional again once a timeout occurs and the cap is presumed restored.
All digital designs and logic simulations for this project were initially developed and tested using Quartus software. This allowed us to verify the functional behavior and timing of the circuits before proceeding to their physical implementation on hardware.

---

## 🛠 Tools Used

- Intel Quartus Prime
- 74LS series ICs
- 555 Timer (for monostable 4s reset)
- Breadboard & LEDs

---




