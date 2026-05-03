# Traffic Light Control System

**PLC-based Traffic Light Controller**  
*Simulating real-world intersection behaviour using CODESYS + Factory I/O*
<img width="922" height="482" alt="image" src="https://github.com/user-attachments/assets/e0444056-1196-4f6e-8128-18399f7eaafe" />


## 📋 Project Objective

Design and implement a **PLC-based traffic light control system** that accurately replicates real-world intersection behaviour, including:
- Pre-start warning phase (**Red + Yellow**)
- Normal cycle with **pre-stop Yellow** phase
- Fully independent lamp control (no combined outputs)
- Robust safety features (Start, Stop, E-Stop, Reset)

Developed as part of the Industrial Automation / PLC Programming coursework.

## ✨ Key Features

- **Realistic Sequence**: Red → Red+Yellow → Green → Yellow → Red (continuous)
- **Timers**: TON with exact timings (Red: 15 s, Red+Yellow: 5 s, Green: 15 s, Yellow: 5 s)
- **State Machine**: Sequential logic using latch bits (`M_IdleState`, `M_RedState`, `M_RedYEllowState`, `M_GreenState`, `M_YellowState`)
- **Independent Outputs**: Each lamp (`Q_RedLamp`, `Q_YellowLamp`, `Q_GreenLamp`) controlled separately by states
- **Safety & Emergency Logic**:
  - E-Stop: Immediate shutdown (all outputs OFF)
  - Stop: Safe stop to Idle state
  - Reset: Forces system back to Idle
  - Start button ignored while system is running
- **Power-up Behaviour**: Defaults to Idle (all lamps OFF)
- **SystemRun & Fault Lamp**: Visual indicators included

## 🛠️ Technologies & Tools

| Component              | Tool / Software          |
|------------------------|--------------------------|
| PLC Programming        | CODESYS (Ladder Diagram) |
| Simulation Environment | Factory I/O              |
| Scene Elements         | Stack Light + Push Buttons |
| Language               | Ladder Diagram (LD)      |
| Project File           | `Traffic Light.project`  |


## 🔌 I/O Mapping (Factory I/O)

### Inputs
- `I_StartPB` → Button.Start
- `I_StopPB` → Button.Stop
- `I_EStopPB` → Button.EStop
- `I_ResetPB` → Button.Reset

### Outputs
- `Q_RedLamp` → StackLight.Red
- `Q_YellowLamp` → StackLight.Yellow
- `Q_GreenLamp` → StackLight.Green
- `Q_SystemRunLamp` → Optional running indicator
- `Q_FaultLamp` → Optional fault indicator

## 🚦 Sequence of Operation

1. **Idle** – All lamps OFF (power-up / after Stop/Reset)
2. **StartPB** → SystemRun = ON → **Red** (15 s)
3. **Red + Yellow** (5 s) – Prepare to move
4. **Green** (15 s) – Vehicles move
5. **Yellow** (5 s) – Prepare to stop
6. Back to **Red** – Cycle repeats indefinitely

**E-Stop** or **Stop** at any time → Immediate return to Idle (all lamps OFF). Restart requires new Start command.

## ✅ Acceptance Criteria Met

- ✅ Exact sequence with correct timing
- ✅ Only valid lamp combinations (Red+Yellow intentionally allowed)
- ✅ Independent lamp outputs via state logic
- ✅ E-Stop & Stop behave correctly
- ✅ Clean reset to Idle on power-up / Stop / Reset
- ✅ Start ignored while running
- ✅ Runs 10+ continuous cycles without failure
- ✅ Fully tested and verified in Factory I/O

## 📸 Screenshots

Full ladder logic documentation is included in **`Traffic Light Control.pdf`** (8 pages).  
Key sections:
- Rungs 1–3: Start/Stop/E-Stop/SystemRun latching
- Rungs 4–13: State transitions + TON timers
- Rungs 14–18: Output lamp control

## 🧪 How to Run
1. Open `Traffic Light.project` in **CODESYS**
2. Download the program to the PLC (or SoftPLC)
3. Load the corresponding **Factory I/O** scene with Stack Light + buttons
4. Map I/O tags exactly as defined in the GVL
5. Run the simulation
6. Press **StartPB** to begin the traffic light cycle

## 📄 License

This project is for educational purposes. Feel free to use and modify it.

---

**Author**: Emmanuel E Ajaegbu  
**Date**: May 2026  
**Built with ❤️ for Industrial Automation Learning**

---

*Star this repository if it helped you with your PLC or Factory I/O project! 🚦*

