# Automatic Street Light Controller

An energy-efficient, discrete analog electronic system designed to automatically switch street lights ON at dusk and OFF at dawn using Light Dependent Resistor (LDR) photo-sensing logic and transistor switching control.

---

## 📌 Project Overview

Traditional street lighting systems often rely on manual operation or fixed timers, leading to significant power wastage when lights remain active during daylight hours. 

This project implements an autonomous, reliable, and cost-effective controller circuit using discrete electronic components. It monitors ambient light intensity in real-time and toggles an electromagnetic relay to drive lighting loads (AC or DC) without manual intervention.

---

## ⚡ Circuit Operation & Working Principle

1. **Light Sensing Stage:**  
   An LDR is placed in a potential divider network. During daylight, light falling on the LDR reduces its resistance, pulling the voltage divider output low.
2. **Switching & Trigger Stage:**  
   As ambient light drops (dusk/darkness), the LDR resistance rises sharply, increasing the base-emitter voltage ($V_{BE}$) across the switching transistor (e.g., BC547) past its $0.7\text{ V}$ threshold into saturation.
3. **Load Actuation:**  
   The collector current energizes the 5V/12V electromagnetic relay coil. A flyback diode (1N4007) is placed antiparallel across the coil to suppress back-EMF voltage spikes and protect the transistor.
4. **Relay Output:**  
   The relay contacts close (Normally Open to Common), turning the connected street light load ON during darkness and OFF when daylight returns.

---

## 📊 Circuit Simulation & Diagrams

The circuit logic and voltage thresholds were verified through simulation prior to hardware implementation:

| Circuit Diagram / Schematic | Simulation Waveform / Output |
| :---: | :---: |
| ![Circuit Diagram](docs/circuit_diagram.png) | ![Simulation Result](docs/simulation_result.jpg) |

> **Simulation Note:** Shows the node voltage trigger and switching behavior as LDR resistance varies from daylight levels (low $\text{k}\Omega$) to darkness (high $\text{k}\Omega$ / $\text{M}\Omega$).

---

## 🛠️ Bill of Materials (BOM)

| Component | Part / Value | Quantity | Purpose |
| :--- | :--- | :---: | :--- |
| **Light Sensor** | LDR (Light Dependent Resistor) | 1 | Detects ambient light levels |
| **Switching Transistor** | BC547 / 2N2222 (NPN) | 1 | Relay driver switch |
| **Relay** | 5V / 12V SPDT Relay | 1 | High-voltage load isolation |
| **Flyback Diode** | 1N4007 | 1 | Back-EMF inductive spike suppression |
| **Voltage Divider Resistor** | 10kΩ / 100kΩ Potentiometer | 1 | Sensitivity / threshold tuning |
| **Base Resistor** | 1kΩ – 4.7kΩ | 1 | Current limiting for transistor base |
| **Indicator / Load** | LED (with 330Ω resistor) or AC Bulb | 1 | Street light load |
| **Power Supply** | 5V – 12V DC Source | 1 | Circuit operating rail |

---

## 🔌 Connection & Wiring Table

| Component Terminal | Connected To | Function |
| :--- | :--- | :--- |
| **LDR (Pin 1)** | $V_{CC}$ (Power Rail) | Voltage divider upper leg |
| **LDR (Pin 2)** | Fixed Resistor / Potentiometer & Base Resistor | Sensing node |
| **Fixed Resistor (Pin 2)** | GND | Voltage divider lower leg |
| **Transistor Base** | Output of Base Resistor | Trigger input |
| **Transistor Collector** | Relay Coil (Pin 1) & Diode Anode | Low-side coil switch |
| **Transistor Emitter** | GND | Common ground reference |
| **1N4007 Diode** | Cathode to $V_{CC}$, Anode to Collector | Flyback protection |
| **Relay NO / COM** | External Load & Power Source | Light switching circuit |

---

## 🚀 Testing & Verification

1. **Ambient Light Check:** Measured LDR resistance under ambient room lighting to establish daylight baseline.
2. **Darkness Response:** Covered the sensor; verified the transistor base voltage exceeded $0.7\text{ V}$, driving the transistor into saturation and energizing the relay.
3. **Threshold Calibration:** Tuned the potentiometer/divider resistor to trigger exactly at dusk lighting levels.

---

## 📂 Repository Structure

```text
├── docs/
│   ├── circuit_diagram.png     # Wiring diagram / schematic view
│   └── simulation_result.jpg   # Circuit simulation capture
├── README.md                   # Project documentation
└── LICENSE                     # Open-source license (MIT)
