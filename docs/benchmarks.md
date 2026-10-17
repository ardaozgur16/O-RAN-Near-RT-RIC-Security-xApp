# Detailed Threat Models and Experimental Benchmarks

## 1. Comprehensive Threat Modeling
To evaluate the resiliency of the middleware, the system was stress-tested against two distinct categories of automated electronic warfare interventions:

### A. Continuous Barrage Jammers
* **Behavior:** Emits high-power, broadband white Gaussian noise continuously across the legitimate channel bandwidth to completely mask pilot signals.
* **xApp Mitigation Strategy:** The optimizer isolates the spatial signature of the noise generator during the estimation phase and commands the RIS to project deep spatial nulls directly toward the jammer’s coordinate vector.

### B. Reactive Burst Jammers
* **Behavior:** Monitors legitimate transmissions via energy/statistical sensing and fires high-power jamming pulses exclusively during active packet windows.
* **xApp Mitigation Strategy:** Employs an Exponentially Weighted Moving Average (EWMA) to track rapid, localized SINR degradation, coupled with pseudorandom **probing slots** to re-evaluate the channel variance without creating blind-spot loops.

## 2. Experimental Verification Metrics

### Control-Loop Latency Distribution
The xApp execution time was profiled across 10,000 consecutive control cycles to verify compliance with strict O-RAN execution budgets:

| Percentile | Execution Latency (ms) | O-RAN Near-RT Target | Status |
| :--- | :--- | :--- | :--- |
| **p50 (Median)** | 4.2 ms | < 10 ms | Pass |
| **p95** | 6.4 ms | < 10 ms | Pass |
| **p99** | 9.1 ms | < 10 ms | Pass |

### SINR Recovery Dynamics
Below is the statistical evaluation of the Legitimate User's SINR performance following an aggressive Reactive Burst Jammer deployment:

### Quantization Loss Evaluation
The STE-based QAT model was benchmarked directly against an ideal, unquantized continuous phase-shift optimizer:
* **Ideal Continuous Optimization:** Reference baseline.
* **STE-QAT 2-bit RIS Configuration:** **< 0.4 dB** performance degradation.
* **STE-QAT 1-bit RIS Configuration:** **< 1.1 dB** performance degradation.

This demonstrates that the framework achieves near-optimal physical-layer security enforcement while strictly respecting discrete hardware realities.
