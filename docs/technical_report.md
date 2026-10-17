# Technical Specification & Mathematical Framework

## 1. O-RAN Near-RT RIC Entegrasyonu
The xApp subscribes to RAN performance metrics via **E2-SM-KPM** (Key Performance Indicators) and manipulates cell configurations using **E2-SM-RC** (RAN Control). 

### Control Loop State Machine:
1.  **Ingestion:** Real-time channel state information (CSI) matrix \(\mathbf{H}\) and Reference Signal Received Power (RSRP) are fetched via E2 indications.
2.  **Detection:** The EWMA anomaly detection module computes the rolling variance of signal degradation.
3.  **Optimization Loop:** If an anomaly is triggered, the PyTorch-based inference loop calculates optimal phase-shift matrices.
4.  **Execution:** Reconfigurations are packaged into `RIC_CONTROL_REQUEST` primitives and dispatched to the O-RU via the Southbound interface.

## 2. Hardware-Aware Optimization (STE-QAT Framework)
A major bottleneck in RIS beamforming is that physical elements utilize discrete phase configurations (e.g., 0°/180° for 1-bit; 0°/90°/180°/270° for 2-bit). Traditional continuous gradient descent fails on non-differentiable step functions.

### Straight-Through Estimator (STE) Formulation:
During the forward pass, the continuous phase matrix \(\mathbf{\Theta}_{cont}\) is quantized using a deterministic mapping function Q(⋅):

\[\mathbf{\Theta}_{disc} = Q(\mathbf{\Theta}_{cont})\]

During the backward pass, the non-differentiable quantization derivative is bypassed by approximating the gradient directly:

\[\frac{\partial \mathcal{L}}{\partial \mathbf{\Theta}_{cont}} \approx \frac{\partial \mathcal{L}}{\partial \mathbf{\Theta}_{disc}}\]

This identity mapping ensures the system optimizes continuous internal weights while enforcing strictly quantized outputs on the hardware fabric, skipping continuous relaxation loss entirely.

## 3. Hysteresis Attack Detection & Automated Probing
To counter sophisticated **Reactive Burst Jammers**—which only transmit when a legitimate packet is sensed—the middleware incorporates a specialized **Probing Protocol**:

When a spatial null is successfully steered toward the jammer, the jammer's sensed energy drops to zero, causing a reactive jammer to cease transmission. This can trigger a false sense of security, tricking the controller into resetting the null. 

To prevent this oscillation loop, the middleware retains a statistical safety hysteresis window and allocates pseudorandom **probing slots** to continuously evaluate channel behavior without interrupting primary user traffic streams.
