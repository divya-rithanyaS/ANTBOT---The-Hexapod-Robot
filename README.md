# 🤖 AntBot — Accessible Hexapod Platform for Surveillance

> **Research Paper:** *Design and Experimental Validation of AntBot: An Accessible Hexapod Platform for Surveillance*
> Rishitha C, Divya Rithanya S, Karthikeya Y, Kaushal S, Akhil V.M
> Amrita School of Artificial Intelligence, Amrita Vishwa Vidyapeetham, Coimbatore

---

## Overview

AntBot is a **low-cost, 21-DOF hexapod robot** designed for indoor surveillance, built with a focus on **architectural simplicity and economic feasibility**. The entire system is controlled by a single **Arduino Mega 2560** microcontroller that directly drives all 21 servo motors — no external PWM drivers needed.

This project demonstrates that **stable, robust, and adaptive hexapod locomotion** is achievable without expensive or specialized hardware.

---

## Key Features

- **21 Degrees of Freedom** — 18-DOF for locomotion + 3-DOF for scanning
- **Single-controller architecture** — Arduino Mega 2560 drives all servos directly
- **Geometric Inverse Kinematics** — Custom IK model for precise foot positioning
- **Tripod Gait** — Statically stable gait validated through MATLAB simulation
- **Power-isolated electronics** — Separate logic and motor power rails via DC-DC buck converter
- **Bluetooth teleoperation** — Wireless control via HC-05 module and smartphone
- **Obstacle negotiation** — Reactive closed-loop behavior using servo load feedback
- **Inclined plane traversal** — Maintains level body orientation on 18° ramps

---

## System Architecture

### Mechanical Design
- Central chassis + 6 identical legs fabricated from **5mm laser-cut acrylic**
- Each leg: **3-DOF serial kinematic chain** (Coxa → Femur → Tibia)
- Wide hemispherical workspace per foot for diverse terrain adaptability

### Electronics
| Component | Specification |
|-----------|--------------|
| Microcontroller | Arduino Mega 2560 |
| Leg Servos | 20x MG996R + 1x MG995 (high-torque, metal gear) |
| Face Servo | 1x SG90 (auxiliary) |
| Bluetooth | HC-05 (wireless serial SPP) |
| Power Source | 11.1V 1800mAh LiPo Battery |
| Voltage Regulation | DC-DC Buck Converter (5V logic rail) |

---

## Inverse Kinematics

The IK model geometrically solves for three joint angles per leg given a target foot-tip position (x, y, z):

- **θ₁ (Coxa):** `atan2(y, x)` — horizontal plane rotation
- **θ₂ (Femur):** elevation angle + Law of Cosines solution
- **θ₃ (Tibia):** Law of Cosines + 90° servo offset

This allows precise, real-time foot placement across varied terrain.

---

## MATLAB Simulation Results

Before physical construction, the full kinematic model was validated in MATLAB:

| Gait | Avg Speed (cm/s) | Stability (°tilt) | Avg Power (W) | Energy/meter (Wh/m) |
|------|-----------------|-------------------|---------------|---------------------|
| **Tripod** | **7.1** | 2.0 | 6.5 | 0.90 |
| Ripple | 5.9 | 1.4 | 5.4 | 0.75 |
| Wave | 4.7 | 1.0 | 5.0 | 0.83 |

Minimum stability margin confirmed: **30mm CoM clearance** within support polygon at all times.

**Tripod gait was selected** for AntBot's primary use case (indoor flat terrain surveillance) — highest speed with acceptable stability.

---

## Experimental Validation

### Test 1 — Obstacle Negotiation
AntBot successfully detected and climbed over an unmodeled obstacle using **servo load as tactile feedback**. When a load spike was detected during leg descent, the system halted, adapted, and used the contact point as the new ground reference.

### Test 2 — Inclined Plane (18°)
AntBot traversed an 18° ramp while **maintaining a level body platform** — directly validating the IK model's ability to decouple locomotion from body orientation. Critical for stable onboard camera/sensor use.

---

## Future Work

- [ ] Ultrasonic sensing for proactive obstacle avoidance
- [ ] IMU integration for real-time pose correction
- [ ] Migration to Raspberry Pi / ESP32 for onboard vision processing
- [ ] Adaptive gait planning based on terrain classification

---

## Authors

| Name | Institute |
|------|-----------|
| Rishitha C | Amrita School of AI, Amrita Vishwa Vidyapeetham |
| **Divya Rithanya S** | Amrita School of AI, Amrita Vishwa Vidyapeetham |
| Karthikeya Y | Amrita School of AI, Amrita Vishwa Vidyapeetham |
| Kaushal S | Amrita School of AI, Amrita Vishwa Vidyapeetham |
| Akhil V.M (Advisor) | Amrita School of AI, Amrita Vishwa Vidyapeetham |

---
## 📄 Research Publication

This work has been published in IEEE and presents the design, modeling, and experimental validation of AntBot.

**Title:** *Design and Experimental Validation of AntBot: An Accessible Hexapod Platform for Surveillance*  

**Authors:** Rishitha C, Divya Rithanya S, Karthikeya Y, Kaushal S, Akhil V.M  

**Publisher:** IEEE  

🔗 [Read the full paper](https://ieeexplore.ieee.org/abstract/document/11426098)

## License

This project is for academic and research purposes.
If you use this work, please cite the original paper.

---

*Built with determination and dedication at Amrita Vishwa Vidyapeetham, Coimbatore*
