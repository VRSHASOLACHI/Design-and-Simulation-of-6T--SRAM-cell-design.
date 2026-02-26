# Design & Implementation of 6T SRAM Cell (Read & Write Operations)

## Project Overview
This project focuses on the **full-custom design and implementation of a 6-Transistor (6T) SRAM cell**, including **read, write, and hold operations**, using **Cadence Virtuoso**. Both **pre-layout** and **post-layout simulations** are performed, along with **physical verification and parasitic extraction**, to analyze power, delay, and stability.

---

## Objectives
- Design and implement a **6T SRAM cell**
- Perform **schematic capture** using Virtuoso Schematic Editor
- Carry out **DC and transient analysis** using Spectre Simulator (pre-layout)
- Design **physical layout** using Virtuoso Layout Editor
- Perform **DRC, LVS, and RCX**
- Conduct **post-layout simulations**
- Compare **pre-layout vs post-layout** performance

---

## Tools Used
- Cadence Virtuoso Schematic Editor  
- Spectre Simulator  
- Virtuoso Layout Editor  
- Quantus (Parasitic Extraction)

---

## SRAM Cell Architecture
A 6T SRAM cell consists of:
- **2 cross-coupled CMOS inverters** (storage nodes Q and Q̅)
- **2 access NMOS transistors** connected to Bit Lines (BL, BL̅)
- Controlled by a **Word Line (WL)**

This configuration enables **high-speed, low-power static memory storage**.

---

## SRAM Operations

### Write Operation
- **Write ‘0’**:  
  - BL = 0, BL̅ = VDD, WL = 1  
  - Node Q is pulled LOW, Q̅ goes HIGH  

- **Write ‘1’**:  
  - BL = VDD, BL̅ = 0, WL = 1  
  - Node Q is pulled HIGH, Q̅ goes LOW  

**Design Requirement:**  
Access transistors must be **stronger than pull-up PMOS** to overwrite stored data.

---

### Read Operation
- Bitlines BL and BL̅ are **precharged to VDD**
- WL is enabled
- Depending on stored data:
  - One bitline discharges slightly
  - Sense amplifier detects ΔV

 **Cell Ratio Constraint:**  
Pull-down NMOS must be stronger than access NMOS to prevent data corruption during read.

---

### Hold State
- WL = 0 → Access transistors OFF
- Cell isolated from bitlines
- Data retained safely


## Transistor Sizing (Final Design)

| Parameter | Value |
|---------|------|
| PMOS Width (Wp) | 220 nm |
| Access NMOS Width (Wa) | 260 nm |
| Pull-down NMOS Width (Wn) | 400 nm |
| Length (All MOS) | 100 nm |

**Sizing Rule Used:**  
**Pull-down > Access > Pull-up**

---

## Design Exploration
Multiple sizing strategies were tested:
1. Equal sizing for all transistors  
2. Stronger PMOS, weaker NMOS  
3. Capacitive loading effects  


## Pre-Layout Simulation Results

### DC Analysis
- Threshold Voltage ≈ **601.664 mV**

### Transient Analysis
- Verified:
  - Write ‘0’
  - Write ‘1’
  - Read ‘0’
  - Read ‘1’

### Hold Stability (SNM)
- **SNM = 392.869 mV**

### Power
- **Average Power = 879.872 nW**

### Delay
- tfr = 495 ps  
- trf = 498.848 ps  
- **Average Delay = 496.924 ps**

---

## Physical Layout
- Full-custom layout created in Virtuoso
- Matched with schematic

### Physical Verification
- DRC: No errors  
- LVS: Matched  
- RCX: Successful parasitic extraction

---

## Post-Layout Simulation Results

### Hold Stability
- **SNM = 307.075 mV**

### Power
- **Average Power = 1213.872 nW**

### Delay
- tfr = 494.755 ps  
- trf = 497.43 ps  
- **Average Delay = 496.0925 ps**

---

## Comparison Summary

| Parameter | Pre-Layout | Post-Layout |
|---------|-----------|------------|
| Power | 879.872 nW | 1213.872 nW |
| Delay | 496.924 ps | 496.0925 ps |
| SNM | 392.869 mV | 307.075 mV |

---

## Circuit Inventory

### Pre-Layout
- Nodes: 6  
- BSIM3v3: 6  
- Voltage Sources: 5  

### Post-Layout
- Nodes: 58  
- BSIM3v3: 6  
- Capacitors: 137  
- Resistors: 55  
- Voltage Sources: 5  

---

## Conclusion
- Successfully designed and verified a **6T SRAM cell**
- Read, write, and hold operations validated
- Layout passed **DRC, LVS, and RCX**
- Post-layout effects increased power due to parasitics
- Design meets **read/write stability criteria**

---

## 📚 References
1. https://github.com/VardhanSuroshi/Memory-Design-And-Testing  
2. *Performance Evaluation of 6T SRAM Cell using 90 nm Technology*, IJERT  
3. *Design of Ultra Low Power 6T SRAM Cell using 180 nm CMOS Technology*, IEEE MESIICON 2022  

---
