# 6G-RIS-Security-Middleware: Latency-Aware Physical Layer Jamming Defense for O-RAN Near-RT RIC

![IEEE ComSoc](https://shields.io)
![O-RAN](https://shields.io)
![Python](https://shields.io)
![PyTorch](https://shields.io)


A high-performance, differentiable physical-layer security middleware engineered as an **O-RAN Near-RT RIC compliant xApp**. This framework autonomously detects adversarial active/reactive jamming attacks and dynamically reconfigures low-resolution (1-bit / 2-bit) Reconfigurable Intelligent Surfaces (RIS) in real time to steer spatial nulls toward the interferer while sustaining legitimate beamforming gains.

> 🔒 **Repository Notice:** The core source code of this production-grade xApp is proprietary. This repository serves as the official open-access technical specification, mathematical framework, and performance benchmark report for industrial R&D verification.

---

## 🛠️ Key Engineering Accomplishments

*   **O-RAN Near-RT RIC Compliance (< 10 ms):** Evaluated and optimized against strict O-RAN control-loop budgets, successfully meeting real-time target execution constraints (`p99 < 10 ms`).
*   **Hardware-Aware Differentiable Optimization:** Implemented a custom PyTorch layer utilizing **Straight-Through Estimators (STE)** for **Quantization-Aware Training (QAT)** to handle discrete hardware constraints (1-bit / 2-bit phase shifts) without continuous relaxation loss.
*   **Hysteresis Attack Detection & Probing:** Pairs EWMA and expected-SINR degradation tracking with automated probing slots to prevent blind-spot traps during successful nulling phases.
*   **Comprehensive Threat Modeling:** Robustly benchmarked against continuous Barrage Jammers and energy/statistical-sensing Reactive Burst Jammers.

---

## 🏗️ System Architecture

The middleware operates as an intelligent xApp inside the Near-Real-Time RAN Intelligent Controller (Near-RT RIC), communicating via the **E2 interface** to monitor RAN metrics and dispatch beamforming adjustments.

---
## 📊 Performance Benchmarks Summary

*   **Control Loop Latency:** Profiled under simulated E2 traffic. **p95: 6.4 ms**, **p99: 9.1 ms** (safely below the 10 ms Near-RT threshold).
*   **SINR Recovery:** Attained a **~14 dB improvement** in legitimate user SINR within 2 control loops after a Reactive Burst Jammer deployment.
*   **Quantization Loss:** STE-based QAT execution resulted in less than **0.4 dB** degradation compared to mathematically ideal, unquantized continuous phase-shift simulations.

---

## 📖 Documentation & Technical Deep-Dive

For a complete breakdown of the underlying equations, state machines, and evaluation frameworks, please refer to the internal documentation:
*   [Technical Architecture & Mathematical Specification](docs/technical_report.md)
*   [Detailed Threat Models and Experimental Benchmarks](docs/benchmarks.md)

## 💼 Copyright & Proprietary Rights Notice

**Copyright © 2026 Arda Özgür. All Rights Reserved.**

*   The core software architecture, algorithmic logic, PyTorch optimization layers, and O-RAN xApp implementation code of this project are **strictly proprietary** and the intellectual property of the author.
*   No part of the proprietary source code may be reproduced, distributed, or transmitted in any form or by any means without prior written permission.
*   This repository serves exclusively as a public-facing technical specification, methodology showcase, and benchmark report for industrial R&D verification.

---

## 📬 Contact & Industrial Collaboration

If you are an industry professional, R&D director, or recruiter interested in this 6G-RIS framework, O-RAN xApp architectures, or physical-layer security solutions, feel free to reach out for architectural deep-dives, portfolio presentations, or professional opportunities:

*   **LinkedIn:** [linkedin.com/in/arda-ozgur](https://linkedin.com)
*   **Email:** [arda.ozgur.art@gmail.com](mailto:arda.ozgur.art@gmail.com)
*   **Academic Profile:** [IEEE Collabratec Portfolio](https://ieee.org)

---
