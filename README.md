<div align="center">

# Rohit Jangra

**Real-time robotics software · C++ · IIT Mandi**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/rohitjangra7370)
[![Email](https://img.shields.io/badge/Email-EA4335?style=flat&logo=gmail&logoColor=white)](mailto:rohitjangra7370@gmail.com)
[![Résumé](https://img.shields.io/badge/Résumé-PDF-18181B?style=flat&logo=googledrive&logoColor=white)](https://drive.google.com/file/d/15AKC2rh4wpfcblP2u0g0mUDsd4aRE1C8/view)

</div>

---

Third-year B.Tech at IIT Mandi. I work on the layer where software meets hardware in real time — control loops with deadlines, binary protocols over serial links, and the autonomy built on top of them. Civil Engineering by admission; robotics by everything I've done since.

Software Lead, **Team Deimos** — 12th of 116 at the Anatolian Rover Challenge 2026, navigation 5.42/6. **Bronze, Inter IIT Tech Meet 14.0** (autonomous warehouse robot, 23 IITs). **Foundation Day Award**, IIT Mandi, for outstanding technical performance.

## Currently

- **Model-based RL for robotic throwing** — diagnostic study at IIT Mandi (AR525), reproducing Turcato et al. ([arXiv:2502.05595](https://arxiv.org/abs/2502.05595)) and extending it with noise, geometry and disturbance ablations. Five-person team; my part is the noise models, the invariance analysis, and the wind/vision studies. Simulation (NumPy ballistics + PyBullet); manuscript in preparation.
- **Autonomy stack for Team Deimos**, URC 2027 — SLAM, Nav2, arm control.
- Hardening [`arm_hardware`](https://github.com/Rohitjangra7370/arm_hardware) — watchdog, frame integrity, and test coverage for the interface layer.

## Selected work

### [arm_hardware](https://github.com/Rohitjangra7370/arm_hardware) — C++
`ros2_control` SystemInterface for a 6-DOF rover manipulator, talking to an STM32 over UART.

Fixed **27-byte** packed frames in both directions, with the wire size enforced by `static_assert` so a protocol change is a compile error rather than a field failure. 100 Hz host loop against a 200 Hz firmware loop. Reads use absolute `CLOCK_MONOTONIC` deadlines recomputed per `select()`, so a partial read can't quietly overrun its budget. The rx thread runs `SCHED_OTHER` on purpose — at `SCHED_FIFO` it starves `controller_manager`'s service handlers and `/load_controller` stops responding.

The repo's [open issues](https://github.com/Rohitjangra7370/arm_hardware/issues) are my own audit of it: the watchdog parameter is parsed but the staleness check isn't wired yet, the frame has no CRC, and the interface file has no test coverage. I'd rather publish the gaps than describe features that aren't there.

### Mars rover autonomy — Team Deimos *(repo private)*
Costmap integration measured at **6M points/s** sustained. Under a 90-second GNSS outage, dead-reckoning drift stayed **below 0.5 m** with **0.6° heading RMS**. 12th of 116 at ARC 2026; SAR 74.74/100. Raised ₹15 lakh for the programme.

### 6-DOF arm — repeatability study
Over a 51-cycle study, **3 of 6 joints held sub-degree repeatability** (0.00–0.05°, which is at the encoder quantisation floor). The remaining two did not; I root-caused them and left them as an open item rather than reporting only the joints that passed.

### [Frontier exploration](https://github.com/Rohitjangra7370/Frontier_Exploration_NAV2-Task_2) · [Custom Nav2 planner](https://github.com/Rohitjangra7370/Custom_Planner-Task_4) — C++
Frontier-based autonomous exploration, and a global planner plugin written against the Nav2 planner interface.

## Open source

Open pull requests to [zellij](https://github.com/zellij-org/zellij) (Rust terminal multiplexer) — pane-size tracking on `split_out` with fixed dimensions, whitespace preservation when dumping wrapped lines, and mouse scroll-modifier forwarding. Plus a test-coverage PR to [PostHog](https://github.com/PostHog/posthog/pull/73227). None merged yet.

## Stack

**Real-time / systems** — C++17, `ros2_control`, POSIX serial (termios), GTest, CMake, Linux
**Autonomy** — ROS 2, Nav2, Cartographer SLAM, MoveIt 2, PX4
**Perception / learning** — OpenCV, PyTorch, GP-based model learning
**Hardware** — STM32, Raspberry Pi 5, Jetson Orin Nano

---

<div align="center">

**Summer 2027 research internships — robotics, learning for control, real-time systems.**

</div>
