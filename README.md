<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/MRCROW173/MRCROW173/main/assets/profile-header-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/MRCROW173/MRCROW173/main/assets/profile-header-light.svg">
  <img alt="Wang Zhe — computer vision, simulation, and systems" src="https://raw.githubusercontent.com/MRCROW173/MRCROW173/main/assets/profile-header-light.svg" width="100%">
</picture>

<p align="center">
  <a href="#about">About</a> &nbsp;·&nbsp;
  <a href="#flagship-architectures--milestones">Flagship Systems</a> &nbsp;·&nbsp;
  <a href="#research--engineering-focus">Research Focus</a> &nbsp;·&nbsp;
  <a href="#technical-matrix">Technical Matrix</a> &nbsp;·&nbsp;
  <a href="#engineering-principles">Principles</a> &nbsp;·&nbsp;
  <a href="mailto:wz13124154500@outlook.com">Contact</a>
</p>

---

## About

I'm **Wang Zhe** (known on GitHub as **[MRCROW173](https://github.com/MRCROW173)**). I work at the intersection of **lightweight computer vision architectures, simulation-to-real digital twins, and reliable systems engineering**.

My engineering philosophy centers on closing the full loop: understanding the underlying mathematical mechanism, building clean and performant implementations, rigorously validating against frozen benchmarks, and automating workflows for end-to-end reproducibility.

> **Observe the mechanism. Build the system. Verify the evidence.**

---

## Flagship Architectures & Milestones

| System / Repository | Key Innovations & Architecture | Primary Metrics & Highlights | Status |
| :--- | :--- | ---: | :---: |
| **[LSAD-YOLO](https://github.com/MRCROW173/Yolo-Unity-Detection-Dystem)** | Self-developed lightweight detector; shallow detail retention (`PSDR-Down`), smooth-floor annealed localization loss (`AdaInner-CIoU`), Gaussian foreground gating (`GSFMGate`) | **90.41%** Dev mAP<br>**50.53%** $AP_{95}$<br>**68+ FPS** (Edge GPU) | 🚀 Core Mainline |
| **[Unity Sim-to-Real Loop](https://github.com/MRCROW173/Yolo-Unity-Detection-Dystem)** | Closed-loop 3D simulation pipeline: parametric scene randomization, pixel-accurate bounding projection audit, and automated YOLO annotation export | **Zero-Manual** Labeling<br>**Sub-pixel** Projection<br>**964+** Multi-Source Data | 🔄 Production |

---

## Research & Engineering Focus

### 🔬 Object Detection & Loss Dynamics (LSAD-YOLO)
- **Architectural Refinement**: Pioneering detail-preserving shallow downsampling (`PSDR-Down`) and high-resolution bridging to combat feature collapse on micro and occluded targets without explosive computational overhead.
- **Dynamic Loss Formulation**: Developing smooth-floor annealed bounding box regression (`AdaInner-CIoU` & `Alpha-CIoU`), addressing TAL (Task-Aligned Assigner) variance and sub-pixel boundary instability in tight localization tasks.
- **Empirical Rigor**: Enforcing paired baseline controls (plain YOLOv12n / YOLOv8n), frozen evaluation benchmarks, and systematic error taxonomy (classification vs. localization vs. background false positives).

### 🎮 Simulation-to-Real Digital Twin (Unity Loop)
- **Synthetic Data Generation**: Constructing parameterized 3D synthetic scenes in Unity (C#) with automatic camera calibration, multi-angle lighting randomization, and synthetic-to-real domain gap mitigation.
- **End-to-End Inference Services**: Linking real-time camera ingestion (USB/UVC) with low-latency YOLO inference backends, live visual overlays, and automated dataset quality auditing.
- **Domain Independence**: Treating synthetic data iteration and model architectural innovations as decoupled experimental axes to ensure cross-domain generalization.

### ⚡ Embedded Systems & Physical Computing
- **Hardware-Level Control**: Developing low-level firmware on **STM32 microcontrollers** (C/C++), implementing high-precision encoder reading, closed-loop PID motion control, and real-time hardware timers.
- **Systems Thinking**: Connecting low-level software decisions directly to physical actuator behavior, ensuring stability, power efficiency, and timing determinism.

### 🛠️ Developer Infrastructure & Reproducible Workflows
- **Autonomous Tooling**: Building lightweight CLI watchers, Git mirror daemons, and automated validation scripts that run in the background to ensure experimental integrity.
- **Evidence-Driven Records**: Maintaining explicit hash snapshots, provenance receipts, and structured markdown knowledge bases across multi-stage iterations.

---

## Technical Matrix

| Domain | Core Frameworks & Tooling | Engineering Scope & Practice |
| :--- | :--- | :--- |
| **Vision & Deep Learning** | Python 3.11 · PyTorch · Ultralytics · OpenCV · CUDA · TensorRT | Lightweight model architecture, custom loss design, TAL assignment analysis, edge model quantization |
| **Simulation & 3D** | Unity 3D · C# · HLSL Shader Basics · Unity Editor Scripting | Automated camera raster capture, coordinate projection audits, synthetic dataset generation pipelines |
| **Embedded & Systems** | C / C++ · STM32 (HAL / LL) · Keil MDK · PlatformIO | Motor control, optical encoders, PID tuning, UART / I2C / SPI bus protocols, timer interrupts |
| **Software & Foundations** | Java · SQL (MySQL, SQL Server) · Git CI/CD · PowerShell | Relational schema design, asynchronous event dispatchers, background monitoring daemons |

---

## Engineering Principles

- **Start with the evidence.** Read existing codebases, historical benchmark data, and regression records before altering architecture or training hyperparameters.
- **Enforce paired controls.** Every mechanism proposal must run against an identical control baseline under frozen budget, seed, and data protocols.
- **Check actual runtime outputs.** A process exiting with code 0 is only a signal; a verified prediction mask, calibrated bounding box, or hardware response is the true test of success.
- **Design for transparent provenance.** Maintain verifiable hash trails, explicit audit logs, and self-documenting workflows so that all findings can be reproduced independently.

---

## Connect

I welcome technical discussions, academic exchanges, and collaborative exploration in **computer vision research, simulation pipelines, and embedded edge systems**.

<p align="center">
  <a href="mailto:wz13124154500@outlook.com"><strong>📧 Email Me</strong> (wz13124154500@outlook.com)</a>
  &nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="https://github.com/MRCROW173?tab=repositories"><strong>📦 Browse Repositories</strong></a>
</p>

---

<p align="center">
  <sub>Observe the mechanism. Build the system. Verify the evidence. · Designed with precision for GitHub Dark & Light themes.</sub>
</p>
