<div align="center">

# ⚡ Enhanced Power Supply ESP32

### Wide-Input (7–24 V) ESP32-C3 Development Board — A Complete Embedded Hardware Platform

**Designed & Simulated in FOSSEE eSim (KiCad-based workflow)**

[![Repo](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github)](https://github.com/devakumar18dk-spec/eSim_PCB_Design_Project_Files)
![Stars](https://img.shields.io/github/stars/devakumar18dk-spec/eSim_PCB_Design_Project_Files?style=for-the-badge&color=yellow)
![Last Commit](https://img.shields.io/github/last-commit/devakumar18dk-spec/eSim_PCB_Design_Project_Files?style=for-the-badge&color=blue)

![MCU](https://img.shields.io/badge/MCU-ESP32--C3--WROOM--02-blue?style=for-the-badge&logo=espressif&logoColor=white)
![Input](https://img.shields.io/badge/Input-7--24V%20DC-orange?style=for-the-badge)
![PCB](https://img.shields.io/badge/PCB-4--Layer-2ea44f?style=for-the-badge)
![USB](https://img.shields.io/badge/USB-Type--C-9146FF?style=for-the-badge)
![Tool](https://img.shields.io/badge/Design%20Tool-FOSSEE%20eSim%20%2F%20KiCad-red?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Design%20Complete-success?style=for-the-badge)

![Layers](https://img.shields.io/badge/Layers-F.Cu%20%7C%20In1.Cu%20%7C%20In2.Cu%20%7C%20B.Cu-6f42c1?style=flat-square)
![Regulator](https://img.shields.io/badge/Buck-LMR50410--Q1-informational?style=flat-square)
![LDO](https://img.shields.io/badge/LDO-LM1117--3.3-informational?style=flat-square)
![ESD](https://img.shields.io/badge/USB%20ESD-USBLC6--2SC6-informational?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)

</div>

<br>

<p align="center">
  <img src="assets/images/board-render.png" alt="Enhanced Power Supply ESP32 — 3D Render" width="640">
</p>

<p align="center"><sub>🧊 3D render of the routed 4-layer board — ESP32-C3-WROOM-02, USB-C, DC barrel jack, and dual GPIO headers.</sub></p>

<div align="center">

`Power In (7–24V)` → `Protection` → `5V Buck` → `3.3V LDO` → `ESP32-C3` ⚡

</div>

```bash
git clone https://github.com/devakumar18dk-spec/eSim_PCB_Design_Project_Files.git
```

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Highlights & Features](#-highlights--features)
- [System Architecture](#-system-architecture)
- [Power Architecture](#-power-architecture)
- [USB-C Interface](#-usb-c-interface)
- [Boot & Reset Control](#-boot--reset-control)
- [RTC Timing](#-rtc-timing)
- [GPIO Expansion](#-gpio-expansion)
- [PCB Design (4-Layer)](#-pcb-design-4-layer)
- [📐 Schematic](#-schematic)
- [🖼 PCB Layout](#-pcb-layout)
- [Technical Specifications](#-technical-specifications)
- [Design Verification Checklist](#-design-verification-checklist)
- [Hardware Bring-Up Sequence](#-hardware-bring-up-sequence)
- [Design Workflow](#-design-workflow)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Contributing](#-contributing)
- [License](#-license)
- [Acknowledgements](#-acknowledgements)

---

## 🧭 Overview

This project presents the design and PCB implementation of a custom **ESP32-C3-based development board**, engineered end-to-end using the **FOSSEE eSim electronics design environment**. Rather than functioning as a simple ESP32 breakout, this board is architected as a **complete embedded hardware platform** — integrating wide-range DC power input, robust input protection, two-stage voltage regulation, USB-C connectivity with ESD protection, hardware boot/reset control, RTC timing, and expandable GPIO — all realized on a **four-layer PCB**.

> **Design philosophy:** protect first, convert efficiently, regulate cleanly, then compute. Every subsystem exists to deliver a stable, low-noise supply and a reliable interface to the ESP32-C3.

```
7–24 V DC  →  Protection  →  5 V Buck  →  3.3 V LDO  →  ESP32-C3
```

---

## ✨ Highlights & Features

<table>
<tr>
<td width="50%" valign="top">

### 🔋 Power System
- Wide **7 V – 24 V DC** input range
- Reverse-polarity protection via **P-channel MOSFET**
- **TVS/Zener** transient (surge) protection
- Two-stage regulation: **Buck (5 V) → LDO (3.3 V)**
- Local bulk + high-frequency decoupling at the MCU

### 🔌 Connectivity
- **USB Type-C** interface (16-pin receptacle)
- CC1/CC2 configuration resistors (device/sink mode)
- Dedicated **USBLC6-2SC6** ESD protection on D+/D−
- USB used strictly for data/programming — **not** primary power

</td>
<td width="50%" valign="top">

### 🧠 Control & Expansion
- **ESP32-C3-WROOM-02** central controller
- Dedicated **EN (Reset)** and **IO9 (Boot)** push buttons
- **32.768 kHz RTC crystal** for low-power timekeeping
- **2 × 8-pin, 2.54 mm** GPIO expansion headers

### 🧱 PCB Engineering
- **4-layer stack-up**: Power / Signal / Mixed / Ground
- Dedicated **ESP32 antenna keep-out zone**
- Functionally-grouped component placement
- Continuous ground plane for low-impedance return paths

</td>
</tr>
</table>

---

## 🏗 System Architecture

The board is organized into five functional sections: **Power**, **USB-C**, **Main Controller**, **Boot/Reset**, and **GPIO/Expansion**.

```
                  ESP32-C3 DEVELOPMENT BOARD
                           │
       ┌───────────────────┼───────────────────┐
       │                   │                   │
       ▼                   ▼                   ▼
 POWER SYSTEM         USB-C SYSTEM       CONTROL / I/O
       │                   │                   │
  7–24 V DC           USB Type-C          Boot Button
       │                   │               Reset Button
       ▼                   │                   │
 Input Protection          │                   │
       │                   │                   │
       ▼                   ▼                   ▼
 5 V Buck              ESD Protection      ESP32-C3
       │                   │                   │
       ▼                   ▼              GPIO Headers
 5 V Rail              USB D+/D−
       │
       ▼
 3.3 V LDO
       │
       ▼
  +3.3 V Rail
       │
       ▼
  ESP32-C3 WROOM-02
       │
       └── 32.768 kHz RTC Crystal
```

---

## 🔋 Power Architecture

Every subsystem on this board depends on a stable, protected supply — so power is treated as the primary design driver, not an afterthought.

### Main Power Path

```
DC Input → Protection → Buck Converter (5 V) → LDO (3.3 V) → ESP32-C3
```

The board deliberately avoids converting the full 7–24 V range directly to 3.3 V with a linear regulator. Instead, a **switching regulator** absorbs the large voltage difference efficiently, while an **LDO** performs final, low-noise regulation — the right tool for each job.

<details>
<summary><b>🛡️ Input Protection — click to expand</b></summary>

<br>

| Function | Component | Behavior |
|---|---|---|
| Transient protection | TVS / Zener network | Inactive under normal operation; clamps excess voltage during spikes |
| Reverse-polarity protection | P-channel MOSFET (STN3P6F6) | Low-resistance conduction on correct polarity; blocks reverse voltage |

```
Correct polarity          Incorrect polarity
      │                          │
      ▼                          ▼
P-MOSFET conducts          MOSFET blocks
      │                          │
      ▼                          ▼
Power reaches regulator    Downstream circuitry protected
```

A P-MOSFET is used instead of a conventional diode because it offers **much lower conduction loss**.

</details>

<details>
<summary><b>⚙️ 5 V Buck Conversion — click to expand</b></summary>

<br>

The protected input feeds the **LMR50410-Q1** switching regulator, which converts **7–24 V → 5 V** by transferring energy through controlled switching rather than dissipating the difference as heat.

**Supporting components:** 4.7 µH inductor · bootstrap capacitor · input/output capacitors · feedback resistor network · 10 µF local input capacitor (placed close to the regulator to keep the high-frequency current loop compact).

```
7–24 V ─► Switching Node ─► 4.7 µH Inductor ─► Output Filter ─► 5 V
```

</details>

<details>
<summary><b>🎯 3.3 V LDO Post-Regulation — click to expand</b></summary>

<br>

The 5 V rail feeds an **LM1117-3.3** LDO, which handles only the small **5 V → 3.3 V** step. This division of labor means:

| Stage | Responsibility |
|---|---|
| Buck | Efficient large voltage conversion (7–24 V → 5 V) |
| LDO | Final clean regulation, ripple attenuation, low-impedance supply |

The LDO also provides power-supply rejection within its effective PSRR band, attenuating residual switching ripple before it reaches the ESP32-C3.

</details>

<details>
<summary><b>📎 MCU Decoupling — click to expand</b></summary>

<br>

Local **4.7 µF** (bulk) and **100 nF** (high-frequency) capacitors sit right at the ESP32-C3 supply pins, supplying transient current locally instead of forcing it through long PCB traces from the regulator — reducing supply impedance seen by the controller.

</details>

<div align="right"><sub><a href="#-enhanced-power-supply-esp32">⬆ back to top</a></sub></div>

---

## 🔌 USB-C Interface

The USB-C section is an **independent communication interface**, cleanly separated from the main power path.

| Element | Detail |
|---|---|
| Connector | USB Type-C, 16-pin |
| CC configuration | 2 × 5.1 kΩ on CC1/CC2 → configures board as USB-C sink/device |
| ESD protection | USBLC6-2SC6, placed near the connector |
| Role | Data / programming only — **not** the primary power source |

```
External USB Connector → ESD Protection → ESP32-C3
```

Keeping USB power and main DC power separate lets the board run continuously from the 7–24 V input while still using USB freely for programming and debugging.

---

## 🛠 Boot & Reset Control

| Button | Signal | Function |
|---|---|---|
| Reset | EN | 10 kΩ pull-up; pressing forces EN low and resets the MCU |
| Boot | IO9 | 10 kΩ pull-up; pressing changes boot-strap state to enter programming mode |

```
USB connected → Hold BOOT → Reset ESP32-C3 → Enters programming mode
```

---

## ⏱ RTC Timing

A **32.768 kHz crystal** provides an external low-frequency timing reference for the ESP32-C3 RTC. It's placed close to the module to minimize parasitics and kept away from the buck converter's switching node to avoid noise coupling.

---

## 🧩 GPIO Expansion

Two **8-pin, 2.54 mm pitch headers** expose selected ESP32-C3 GPIOs, turning the board into a reusable development platform for sensors, LEDs, displays, communication modules, and breadboard prototyping.

---

## 🧱 PCB Design (4-Layer)

| Layer | Purpose |
|---|---|
| **F.Cu** (Top) | Power distribution & primary component routing |
| **In1.Cu** | Signal routing (GPIO fan-out from the ESP32-C3) |
| **In2.Cu** | Mixed-purpose routing / secondary distribution |
| **B.Cu** (Bottom) | Continuous ground plane |

<details>
<summary><b>📍 Component Placement Strategy</b></summary>

<br>

| Region | Contents | Rationale |
|---|---|---|
| Upper | ESP32-C3 module, antenna toward board edge | Unobstructed RF environment |
| Central | Buck converter, LDO, protection circuitry, USB-C | Short, low-impedance power connections |
| Lower | Boot/Reset buttons | User accessibility |
| Sides | GPIO headers (left & right) | Convenient external interfacing |

</details>

<details>
<summary><b>📡 Antenna Keep-Out</b></summary>

<br>

A clearly defined **keep-out zone** sits above the ESP32-C3 module — no copper, tracks, or vias are routed through this area, per module manufacturer guidance, to prevent detuning or shielding the integrated antenna.

</details>

<details>
<summary><b>🧵 Routing & Grounding Philosophy</b></summary>

<br>

- **High-current power paths** — short and comparatively wide (DC input, MOSFET, buck, inductor, 5 V rail, LDO)
- **Switching node** — kept as small as practical to limit EMI coupling
- **USB D+/D−** — routed as a matched differential pair, ESD device close to the connector
- **RTC crystal traces** — short, isolated from switching noise
- **Ground plane (B.Cu)** — continuous reference plane minimizing loop area, EMI, and supply noise — especially important given the ESP32-C3's onboard radio

</details>

<details>
<summary><b>🌡️ Thermal Considerations</b></summary>

<br>

Primary heat sources are the **buck converter**, **LDO**, and **protection MOSFET**. The LDO has the most predictable thermal profile since it dissipates the 5 V→3.3 V difference directly — adequate copper area is provided around its thermal pads per datasheet recommendations.

</details>

---

## 📐 Schematic

<p align="center">
  <img src="assets/images/schematic.png" alt="Full Circuit Schematic" width="900">
</p>

<div align="center">

| 🔋 Input → 5V → 3.3V | 🔌 USB-C & ESD | 🛠 Boot & Reset | 🧠 Main Controller | 🧩 GPIOs |
|:---:|:---:|:---:|:---:|:---:|
| ST6P3F6, LMR50410-Q1, LM1117-3.3 | USB-C receptacle, USBLC6-2SC6 | EN & IO9 push buttons | ESP32-C3-WROOM-02 | 2 × 8-pin headers |

</div>

<p align="center"><sub>📄 Captured entirely in <b>FOSSEE eSim</b> — five functional blocks laid out for clarity: power regulation (top), USB-C/protection, boot/reset, and GPIO breakout (bottom row), with the main ESP32-C3 controller on the right.</sub></p>

---

## 🖼 PCB Layout

The board is routed across **four copper layers**, each with a distinct role. Toggle through the stack below — every view shares the same silhouette so you can trace a single net (e.g. GND) from top to bottom.

<table align="center">
<tr>
<th align="center">🟥 F.Cu — Power / Top Layer</th>
<th align="center">🟩 In1.Cu — Signal Layer</th>
</tr>
<tr>
<td><img src="assets/images/pcb-layout-top.png" width="420"></td>
<td><img src="assets/images/pcb-layout-in1.png" width="420"></td>
</tr>
<tr>
<td align="center"><sub>Primary power distribution & component-side routing</sub></td>
<td align="center"><sub>ESP32-C3 GPIO fan-out toward J3 / J4 headers</sub></td>
</tr>
<tr>
<th align="center">🟧 In2.Cu — Mixed Routing Layer</th>
<th align="center">🟦 B.Cu — Ground Plane</th>
</tr>
<tr>
<td><img src="assets/images/pcb-layout-in2.png" width="420"></td>
<td><img src="assets/images/pcb-layout-bottom.png" width="420"></td>
</tr>
<tr>
<td align="center"><sub>Secondary power/signal distribution channel</sub></td>
<td align="center"><sub>Continuous ground reference plane</sub></td>
</tr>
</table>

> 🛰️ **Antenna Keep-Out Zone** — visible as the hatched `KEEP-OUT ZONE / Antenna` region above the ESP32-C3 module on every layer. No copper, tracks, or vias are routed through this area to protect RF performance.

<details>
<summary><b>📊 Routing Stats (from PCB editor)</b></summary>

<br>

| Metric | Count |
|---|---|
| Pads | 151 |
| Vias | 102 |
| Nets | 586 |
| Unrouted | 0 ✅ |

</details>

<div align="right"><sub><a href="#-enhanced-power-supply-esp32">⬆ back to top</a></sub></div>

---

## 📋 Technical Specifications

| Specification | Design |
|---|---|
| MCU | ESP32-C3-WROOM-02 |
| Main DC input | 7–24 V |
| Primary power connector | DC input connector |
| Input protection | TVS/Zener + P-channel MOSFET |
| Reverse polarity protection | STN3P6F6 P-MOSFET |
| Buck regulator | LMR50410-Q1 |
| Buck output | 5 V |
| Buck inductor | 4.7 µH |
| Post-regulator | LM1117-3.3 |
| Final logic rail | 3.3 V |
| RTC reference | 32.768 kHz crystal |
| USB connector | USB Type-C, 16-pin |
| USB CC resistors | 5.1 kΩ × 2 |
| USB ESD protection | USBLC6-2SC6 |
| Reset control | EN push button |
| Boot control | IO9 push button |
| Button pull-ups | 10 kΩ |
| GPIO expansion | 2 × 8-pin headers |
| GPIO header pitch | 2.54 mm |
| PCB structure | 4-layer |
| F.Cu | Primary power / component routing |
| In1.Cu | Signal routing |
| In2.Cu | Mixed routing / distribution |
| B.Cu | Ground plane |
| RF provision | ESP32 antenna keep-out |
| Design environment | FOSSEE eSim / KiCad-based workflow |

---

## ✅ Design Verification Checklist

<table>
<tr>
<td width="50%" valign="top">

**Schematic Checks**
- [ ] All power nets verified
- [ ] 3.3 V connections verified
- [ ] 5 V connections verified
- [ ] All ground connections verified
- [ ] ESP32-C3 power pins checked
- [ ] Boot strapping verified
- [ ] EN/reset circuitry verified
- [ ] USB D+/D− connections verified
- [ ] USB CC resistors verified
- [ ] No unintended VBUS-to-3.3 V paths

</td>
<td width="50%" valign="top">

**PCB Checks**
- [ ] Design Rule Check (DRC) passed
- [ ] Track widths verified
- [ ] Clearances verified
- [ ] Via placement checked
- [ ] Copper-zone connections checked
- [ ] Antenna keep-out respected
- [ ] Silkscreen overlaps checked
- [ ] Connector orientation verified
- [ ] Footprint pin numbering verified
- [ ] Mounting/mechanical dimensions verified

</td>
</tr>
</table>

<div align="right"><sub><a href="#-enhanced-power-supply-esp32">⬆ back to top</a></sub></div>

---

## 🧪 Hardware Bring-Up Sequence

> Do **not** connect the ESP32 module immediately after fabrication — follow a controlled sequence.

| Step | Test | Expected Result |
|---|---|---|
| 1 | Input protection | Protected input rail stable across 7–24 V |
| 2 | Buck converter | ~**+5 V** at buck output (before connecting downstream circuitry) |
| 3 | LDO | ~**+3.3 V** at LDO output |
| 4 | MCU power | ESP32-C3 receives correct 3.3 V supply |
| 5 | Reset | Pressing EN resets the MCU |
| 6 | Boot | IO9 + reset sequencing enters programming mode |
| 7 | USB | USB enumeration / programming succeeds |
| 8 | GPIO | Expansion headers verified with simple GPIO firmware |
| 9 | RTC | 32.768 kHz RTC functionality confirmed |

---

## 🔁 Design Workflow

```
System Requirements → Circuit Architecture → Component Selection
        → Schematic Capture (eSim) → Electrical Connectivity Verification
        → Footprint Assignment → PCB Layout → 4-Layer Stack-up
        → Component Placement → Power Routing → Signal Routing
        → Ground Plane → Antenna Keep-Out → Design Rule Check
        → Gerber / Manufacturing Files → PCB Fabrication → Hardware Testing
```

---

## 🗂 Repository Structure

```
eSim_PCB_Design_Project_Files/
├── assets/
│   └── images/
│       ├── board-render.png       # 3D render
│       ├── schematic.png          # Full eSim schematic
│       ├── pcb-layout-top.png     # F.Cu — power layer
│       ├── pcb-layout-in1.png     # In1.Cu — signal layer
│       ├── pcb-layout-in2.png     # In2.Cu — mixed layer
│       └── pcb-layout-bottom.png  # B.Cu — ground plane
├── hardware/
│   ├── schematic/          # eSim / KiCad schematic project files
│   ├── pcb/                # PCB layout project files
│   └── gerbers/            # Manufacturing output (Gerbers, drill files, BOM)
├── docs/
│   └── technical-report.md # Full design & verification report
├── firmware/                # (optional) example/bring-up firmware
├── LICENSE
└── README.md
```

---

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/devakumar18dk-spec/eSim_PCB_Design_Project_Files.git
   cd eSim_PCB_Design_Project_Files
   ```
2. **Open the schematic/PCB** in FOSSEE eSim or KiCad from the `hardware/` directory.
3. **Review the Gerbers** in `hardware/gerbers/` before sending to fabrication.
4. **Follow the [Hardware Bring-Up Sequence](#-hardware-bring-up-sequence)** after assembly.
5. **Flash firmware** over USB-C once power rails are verified.

---

## 🤝 Contributing

Contributions, issues, and design suggestions are welcome! Feel free to open a pull request or start a discussion if you'd like to improve the power architecture, layout, or documentation.

---

## 📄 License

This project is released under the **MIT License** — see [`LICENSE`](LICENSE) for details. *(Update if a different license applies.)*

---

## 🙌 Acknowledgements

- **FOSSEE eSim** — schematic capture and simulation environment
- **KiCad** — PCB layout workflow
- **Espressif Systems** — ESP32-C3-WROOM-02 module

---

<div align="center">

### 🧩 Built as a complete embedded hardware platform — not just an ESP32 carrier board.

**Wide-range power management · Protection · Wireless processing · USB-C · Hardware boot control · RTC · Expandable I/O**
**— all in a single four-layer PCB.**

![Made with eSim](https://img.shields.io/badge/Made%20with-FOSSEE%20eSim-orange?style=for-the-badge)
![Open Hardware](https://img.shields.io/badge/Open-Hardware-blueviolet?style=for-the-badge)

**⭐ If this project helped you, consider starring the repository!**

[⬆ Back to top](#-enhanced-power-supply-esp32)

</div>
