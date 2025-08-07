# Linear Voltage Regulator : Schematic Capture, Simulation, Assembly, and Validation


[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)


> **TL;DR:**  
> End-to-end design, simulation, hardware assembly, and validation of a discrete linear voltage regulator. Recreated schematic, performed LTspice analysis, soldered PCB, and validated output using oscilloscope and DMM—mirroring industry hardware validation flow.

**Technologies:**  
LTspice · Schematic Capture (Altium Designer) · Analog Circuit Design · PCB Soldering · Oscilloscope & Multimeter Validation · Test Point Measurement · Simulation-to-Lab Correlation · Git

---
## **Results Summary**

> Output: 5.000 V ± 20 mV under 33 Ω load  
> Ripple: <100 mVpp  
> AC RMS noise: <20 mV  
> Matches LTspice simulation under steady-state

---

## Table of Contents

- [Repo Structure](#repo-structure)
- [Block Diagram](#block-diagram)
- [Schematic & Simulation](#schematic--simulation)
- [PCB Assembly & Test Points](#pcb-assembly--test-points)
- [Lab Measurements & Validation](#lab-measurements--validation)
- [Key Design Decisions](#key-design-decisions)
- [How to Replicate](#how-to-replicate)
- [Supporting Materials](#supporting-materials)
- [What I Learned](#what-i-learned)
- [Contact](#contact)

---
## 📁 Repo Structure

```bash
linear-voltage-regulator-pcb/
├── hardware/       # Altium schematics & PCB layout
├── docs/           # LTspice simulation files
├── images/         # Figures for README
├── LICENSE
└── README.md
```

## Block Diagram

![Block Diagram](images/block-diagram-m0.png)

<p align="center"><b>Figure 1:</b> Color-coded block diagram with explicit feedback and test point labeling. System flow, feedback, and measurement location are shown for hardware validation.</p>

---

## Schematic & Simulation

| LTspice Regulator Schematic       | LTspice Power Supply Schematic       |
|:---------------------------------:|:------------------------------------:|
| ![Figure 1](images/figure-1.png) | ![Figure 2](images/figure-4.png) |

<p align="center"><b>Figure 2:</b> Regulator circuit schematic in LTspice.<br>
<b>Figure 3:</b> Simulated power supply input schematic in LTspice.</p>

---

### **Simulation Waveforms**

| Output Simulation (5kΩ load)         | Regulator Output (after PSU)        |
|:------------------------------------:|:-----------------------------------:|
| ![Figure 3](images/figure-5.png) | ![Figure 4](images/figure-6.png) |

<p align="center"><b>Figure 4:</b> Output with 5000Ω load shows voltage instability (no continuous DC).<br>
<b>Figure 5:</b> Regulator output waveform after connecting to simulated power supply.</p>

---

| Input vs Output (Full System)            |
|:----------------------------------------:|
| ![Figure 7](images/figure-7.png) |

<p align="center"><b>Figure 6:</b> Input (rectified) vs output (regulated, 5V) voltages. Regulator maintains 5V during input peaks.</p>

---

## PCB Assembly & Test Points

- **Manually soldered PCB, used “hairpin” test points for easy probing.**
- **Test point for validation is clearly marked at output (VOUT, 5V).**

| Assembled PCB (Top View)              | Output Test Point (Scope/DMM)         |
|:-------------------------------------:|:-------------------------------------:|
| ![Figure 4](images/assembled_pcb.jpg) | ![Figure 5](images/test-point.png)    |

<p align="center"><b>Figure 7:</b> Fully soldered linear regulator PCB.  
<b>Figure 8:</b> Output test point for oscilloscope and multimeter validation (VOUT, 5V).</p>

---

## Lab Measurements & Validation

### **Oscilloscope Results (Input & Output)**

- **Dual-channel scope confirms input and output behavior matches simulation.**
- **Output remains at 5V with Vin ≥ 6.5V; measured at test point.**

| Oscilloscope Dual-Channel (Input/Output)     | Output Vpp and RMS (Oscilloscope)         |
|:--------------------------------------------:|:-----------------------------------------:|
| ![Figure 6](images/osc-1.png)    | ![Figure 7](images/osc-2.png)  |

<p align="center"><b>Figure 9:</b> Input (yellow) and output (blue) scope traces—output is stable 5V when input is sufficient.  
<b>Figure 10:</b> Measured output Vpp and RMS—confirms low ripple and proper regulation.</p>

---

### **DMM Validation of Output Voltage**

- **Precision trimmer adjusted for exactly 5.00V at output.**

| Output at No Load (DMM)                  | Output at 33Ω Load (DMM)              |
|:----------------------------------------:|:--------------------------------------:|
| ![Figure 8](images/5V-1.png)           | ![Figure 9](images/5V-2.png)    |

<p align="center"><b>Figure 11:</b> Output set to 5.00V (no load).  
<b>Figure 12:</b> Output remains 5.00V under 33Ω load.</p>

---

### **Additional Measurements (Op-Amp, AC RMS, etc.)**

| Op-Amp Inverting Input (2.5V)           | Op-Amp Non-Inverting Input (2.5V)      |
|:---------------------------------------:|:--------------------------------------:|
| ![Figure 10](images/op-1.png)| ![Figure 11](images/op-2.png)  |

| AC RMS at Input (DMM)                   | AC RMS at Output (DMM)                 |
|:----------------------------------------:|:--------------------------------------:|
| ![Figure 12](images/ac-1.png)    | ![Figure 13](images/ac-2.png) |

<p align="center"><b>Figures 13–16:</b> Validation of op-amp node voltages and AC RMS measurements for input and output.</p>

---

## Key Design Decisions

- **Schematic Ownership:**  
  Captured the schematic independently in Altium, ensuring understanding of each subsystem for simulation and validation.
- **Testability:**  
  Added accessible test points at VOUT for oscilloscope/DMM probes, mirroring “design for test” best practices.
- **Validation Workflow:**  
  Correlated simulation results with hardware, tuned for regulation, and documented performance under varied conditions.

---

## How to Replicate

1. **Clone this repo:**  
   ```bash
   git clone https://github.com/hyeonjijung1/linear-voltage-regulator-pcb.git
   cd linear-voltage-regulator-pcb
   ```

2. **Review the schematic and simulation files in `/hardware/` and `/docs/`.**

3. **Order or fabricate the PCB using the provided schematic and Gerbers, or build the circuit on a breadboard for prototyping.**

4. **Solder components as per the schematic, ensuring careful placement of test points for measurement and validation.**

5. **Power the board with a DC supply (e.g., 12V), connect a load resistor (e.g., 33Ω, 5W), and validate the output using a digital multimeter and oscilloscope.**

6. **Compare hardware measurements to simulation waveforms and DC operating points for full-cycle validation.**

---

## What I Learned

- **End-to-end hardware validation:** Developed hands-on skills from schematic capture and simulation to assembly and bench testing—mirroring real ASIC/hardware development.
- **Design for test:** Integrated explicit test points for validation and troubleshooting, enabling reliable, reproducible results.
- **Simulation vs. reality:** Practiced correlating LTspice simulations with physical hardware performance, deepening understanding of analog circuits and measurement techniques.
- **Technical communication:** Documented the workflow with clear visuals and reasoning, as expected in professional engineering teams.

---

## Contact

[![LinkedIn: Hyeonji Jung](https://img.shields.io/badge/-Hyeonji%20Jung-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://linkedin.com/in/hyeonjijung-uoft)](https://linkedin.com/in/hyeonjijung-uoft)

**Hyeonji Jung**  
junghyeonji254@gmail.com

---
