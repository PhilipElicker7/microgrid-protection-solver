# Microgrid Protection Solver

## Overview
This repository contains a Python-based utility grid simulator that models power flow, voltage drop, and automated fault-protection logic for a 3-node distribution microgrid. 

Rather than relying on black-box commercial software, this project relies on core electrical engineering physics. It constructs a **Y-Bus Admittance Matrix** and utilizes the **Gauss-Seidel iterative numerical method** to solve for complex power flow in real-time.

## Project Architecture
The simulation runs in three distinct phases:

1. **Steady-State Calculation:**
   Calculates the natural voltage sag across physical transmission lines using complex line impedance ($Z = R + jX$) and active/reactive power demands ($S = P + jQ$).
2. **Catastrophic Fault Injection:**
   Simulates a direct line-to-ground fault (e.g., a lightning strike) at the furthest node, causing an instantaneous voltage collapse and a massive >10kA short-circuit current spike.
3. **Automated Relay Protection & Recovery:**
   An algorithmic "Smart Breaker" detects the overcurrent condition, dynamically restructures the Y-Bus matrix to isolate the damaged node, and recalculates the surviving grid's voltage recovery.

## Technical Skills Demonstrated
* **Linear Algebra & Matrix Operations:** Dynamic generation of $N \times N$ nodal admittance matrices using `numpy`.
* **Numerical Methods:** Implementation of Gauss-Seidel convergence loops for non-linear systems.
* **Power Systems Engineering:** Application of Kirchhoff’s Current Law, Complex Power, and ANSI C84.1 voltage standards.

## Simulation Output
```text
--- RUNNING STEADY STATE SIMULATION ---
Node 2 (Industrial) Voltage:  7035.67 V
Node 3 (Residential) Voltage: 6904.65 V

--- INJECTING LINE-TO-GROUND FAULT AT NODE 3 ---
CRITICAL: Fault current spiked to 10488.16 Amps!
ACTION: Smart Breaker Tripped! Isolating Node 3...

--- RECALCULATING GRID STABILITY ---
SUCCESS: Grid Stabilized. Node 2 Recovered to 7136.73 V
