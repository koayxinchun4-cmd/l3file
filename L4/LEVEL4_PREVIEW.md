# Level 4 Preview — MC 091-04-2016

> *Level 4 課程預覽* | Created by Marvis | 2025-06-25
> Based on: Malaysian Mechatronic Diploma standard curriculum + web research

---

## Current: MC 091-03-2016 (Level 3)

You're learning: Microcontrollers, Sensors, Basic Control, C++ Programming

---

## Next: MC 091-04-2016 (Level 4)

Based on the standard Malaysian Mechatronic Engineering Diploma curriculum (MQA-accredited), Level 4 typically includes:

| Course | What It Covers | How Arduino/Wokwi Helps |
|---|---|---|
| **PLC & Industrial Automation** | Ladder logic, PLC programming (Siemens/Mitsubishi/Omron), industrial control panels | State machine thinking from Arduino transfers directly to PLC |
| **Robotics & Kinematics** | Forward kinematics, inverse kinematics, DH parameters, trajectory planning | Servo + encoder practice builds intuition |
| **Power Electronics & Drives** | MOSFET/IGBT switching, DC/AC drives, VFD, soft starters | PWM mastery from Arduino is the foundation |
| **Mechatronic System Integration** | Sensors + actuators + controllers working as one system | Multi-sensor projects prepare you perfectly |
| **Industrial Networks & IoT** | Modbus RTU/TCP, CAN bus, PROFIBUS, MQTT, OPC-UA | Communication protocols (I2C/SPI/UART) already learned |
| **Control System Engineering** | Transfer functions, PID tuning, stability analysis (Bode/Nyquist), state-space | PID concept + real-world tuning experience |
| **Maintenance & Reliability** | Predictive maintenance, FMEA, reliability engineering | Sensor data logging + analysis mindset |
| **Engineering Design Project** | Capstone: design and build a mechatronic system | Everything you've practiced comes together |

---

## What to Prepare Now（現在可以準備的）

### High Priority — Directly Useful
| Topic | Action |
|---|---|
| **PID Control** | Learn the concept now. Try tuning P, I, D on a simulated motor |
| **State Machines** | Practice `switch/case` and `enum` patterns |
| **WiFi / MQTT** | Build a web-controlled LED (code in wifi-iot.md) |
| **Multi-sensor Fusion** | Combine ultrasonic + servo + motor in one project |

### Medium Priority — Background Knowledge
| Topic | Action |
|---|---|
| **Trigonometry refresher** | sin/cos/tan for kinematics; `atan2()` for angle calculations |
| **Basic electronics** | Ohm's Law, voltage divider, transistor switching, pull-up/pull-down |
| **Industrial protocols** | Read about Modbus basics (master/slave, registers) |

### Nice to Have
| Topic | Action |
|---|---|
| **PLC ladder logic** | Try free PLC simulator (e.g., PLC Fiddle) to understand ladder diagrams |
| **MATLAB/Octave** | Basic plotting, transfer functions for control systems |
| **Python** | Useful for data analysis, plotting sensor data, MQTT clients |

---

## Key Difference: Level 3 vs Level 4

| Aspect | Level 3 | Level 4 |
|---|---|---|
| Scope | Single component/sensor | Full systems |
| Control | Basic ON/OFF, PWM | PID, state-space, optimal control |
| Communication | UART/I2C/SPI (board-level) | Modbus/CAN/Ethernet (industrial) |
| Power | 3.3V/5V logic | 24V/240V/3-phase industrial |
| Tools | Arduino IDE, Wokwi | PLC software, SCADA, MATLAB |
| Mindset | "Make it work" | "Make it reliable, safe, efficient" |

---

## Study Tips from This Chat（這次對話的學習建議）

1. **Master Arduino NOW** — When Level 4 introduces PLC, you'll already think like a controls engineer
2. **Wokwi is your lab** — Simulate before buying hardware. Save money and time
3. **Document everything** — Keep code snippets organized (this repo is your start!)
4. **Build projects, not exercises** — A line-following robot teaches more than 10 isolated tutorials
5. **Debug with Serial Monitor** — Get comfortable reading sensor values live

---

> This preview is based on publicly available Malaysian Diploma in Mechatronics Engineering curricula from multiple institutions (APU, IPK, Stradford College). Actual Inforgenius syllabus may differ — check your school portal for exact courses.
> 此預覽基於多間馬來西亞院校公開的 Mechatronic Diploma 課程，實際 Inforgenius 課綱可能不同，請以學校公佈為準。
