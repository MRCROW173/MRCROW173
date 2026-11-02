# LSAD-YOLO: Lightweight Detail-Preserving Object Detection Architecture
### Technical Whitepaper & Architectural Overview

> **Author**: Wang Zhe ([@MRCROW173](https://github.com/MRCROW173))  
> **Contact**: [wz13124154500@outlook.com](mailto:wz13124154500@outlook.com)  
> **Repository Notice**: Active model training scripts, full ablation logs, and proprietary simulation assets are maintained within the private research workspace [`MRCROW173/Yolo-Unity-Detection-Dystem`](https://github.com/MRCROW173). This document provides public technical documentation, architectural formulations, and reproducible benchmark evidence.

---

## 1. Motivation & Problem Statement

Real-time edge perception (UAVs, mobile robotics, industrial inspection) demands ultra-low latency alongside high boundary localization accuracy. While modern one-stage detectors (such as YOLOv8 and YOLOv12) provide strong classification performance, they exhibit systematic degradation under three challenging conditions:
1. **Sub-pixel Boundary Sensitivity**: Small and occluded objects suffer severe IoU variance with minor (1–2 pixel) bounding prediction errors, causing Task-Aligned Assigner (TAL) instability;
2. **Early Feature Collapse**: Conventional strided convolutions rapidly downsample early spatial representations, discarding weak edge features;
3. **Planar Occlusion & Background Interference**: High-frequency texture noise often triggers false positive alarms (Bg FP) in shallow feature maps.

**LSAD-YOLO** is engineered to resolve these bottlenecks through targeted architectural mechanisms and dynamic loss formulations, achieving superior boundary precision without inflating parameter counts or runtime inference latency.

---

## 2. Core Architectural Mechanisms

```
Input Image (640x640x3)
       │
       ▼
  [PSDR-Down] ──────────► Detail-preserving shallow feature retention
       │
  Backbone (P3, P4, P5)
       │
  [GSFMGate]  ──────────► Gaussian soft foreground mask gating
       │
       ▼
   PAN Neck ────────────► Bi-directional multi-scale fusion
       │
       ▼
 Decoupled Detection Head (P3, P4, P5)
       │
       ▼
[AdaInner-CIoU Loss] ───► Smooth-floor annealed localization optimization
```

### 2.1 Preserved Shallow Detail Downsampling (`PSDR-Down`)
Standard downsampling layers aggressively reduce spatial dimensions, permanently losing micro-target gradients. `PSDR-Down` replaces naive stride-2 operations with a dual-branch split-and-merge structure that preserves high-frequency edge gradients while maintaining low computational complexity.

### 2.2 Smooth-Floor Annealed Localization (`AdaInner-CIoU`)
Standard CIoU calculates regression gradients based on outer bounding coordinates. For small targets with high relative IoU requirements ($AP_{95}$), we introduce an auxiliary scaled internal bounding box $\text{IoU}^{\text{inner}}$ coupled with dynamic power annealing:

$$\mathcal{L}_{\text{AdaInner}} = \mathcal{L}_{\text{CIoU}} + \lambda(t) \cdot \left(1 - \text{IoU}^{\text{inner}}\right)^{\alpha(t)}$$

Where:
* **$\lambda(t)$** undergoes cosine decay with a strict soft floor ($\lambda_{\text{min}} = 0.20$), preventing gradient starvation in late training iterations;
* **$\alpha(t)$** dynamically scales from $1.0 \to 1.5$, sharpening boundary localization focus onto near-ground-truth anchor proposals.

### 2.3 Foreground Semantic Gating (`GSFMGate`)
To suppress spurious background activations in complex lighting or textured backgrounds, `GSFMGate` generates spatial-channel modulation weights using Gaussian soft masks, dampening non-target feature responses before feature aggregation.

---

## 3. Benchmark Verification & Experimental Evidence

All models are trained and evaluated under strictly controlled protocols:
* **Dataset**: 768 / 964 multi-source synthetic and real-camera benchmark (`coverage_repair_v2` / `r17_multisource`);
* **Budget**: 20 epochs (1,920 updates), input resolution 640×640, single-GPU FP32 training, fixed random seeds (17, 29);
* **Evaluation Protocol**: Full paired control against official `plain YOLOv12n` and `YOLOv8n` baselines with sealed test sets (`test32` & `test300`).

### 3.1 Paired Benchmark Performance Table

| Model Architecture | Backbone Base | Parameters | Edge Latency (FPS) | Dev Set mAP@50 | Dev Set $AP_{95}$ | Challenge Set mAP |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: |
| **Plain YOLOv12n (Baseline)** | YOLOv12n | 2.62 M | 68.9 FPS | 89.64% | 48.20% | 88.25% |
| **LSAD-YOLO v1 (Alpha-CIoU)** | YOLOv12n | 2.62 M | 68.8 FPS | 90.12% | 49.30% | 89.40% |
| **LSAD-YOLO v3 (GSFMGate)** | YOLOv12n | 2.65 M | 67.5 FPS | 90.25% | 49.80% | 90.10% |
| **LSAD-YOLO v4.1 (Soft-Floor)** | YOLOv12n | **2.62 M** | **68.3 FPS** | **90.41%** | **50.53%** | **91.34%** |

> **Key Takeaway**: Compared to the plain baseline, `LSAD-YOLO v4.1` achieves **+0.77 pp higher mAP@50**, a massive **+2.33 pp boost in $AP_{95}$ strict localization accuracy**, and **+3.09 pp gain on challenge sets**, all while adding **zero parameter overhead** (+0 params) and maintaining near-identical runtime FPS.

---

## 4. Closed-Loop Sim-to-Real Digital Twin Pipeline

The perception model is backed by a fully automated **Unity 3D simulation data generation pipeline**:
1. **Parametric Randomization**: Dynamic lighting, camera distance (0.8m – 3.5m), object pose angles (Euler yaw/pitch/roll), and material textures;
2. **Sub-pixel Annotation Engine**: Custom C# projection scripts calculate ground-truth 2D bounding boxes directly from camera projection matrices, eliminating human labeling errors;
3. **Automated Audit Pipeline**: Python verification daemons continuously check for coordinate consistency, label clipping, and domain-gap distribution shifts before feeding data into the training pipeline.

---

## 5. Summary & Research Roadmap

| Phase | Milestone | Deliverable | Status |
| :--- | :--- | :--- | :---: |
| **Phase 1** | Base Pipeline & Sim-to-Real Capture | Physical Camera + Unity Closed-Loop | ✅ Completed |
| **Phase 2** | Shallow Detail Retention (`PSDR-Down`) | High-resolution bridge for small targets | ✅ Completed |
| **Phase 3** | Loss Annealing (`AdaInner-CIoU`) | High-IoU boundary precision ($AP_{95} > 50\%$) | ✅ Completed |
| **Phase 4** | Cross-Batch Independent Replication | Verified generalizability across multi-seed runs | ✅ Completed |
| **Phase 5** | Edge Deployment & Embedded Integration | TensorRT / ONNX INT8 engine on edge hardware | 🔄 In Progress |

---

*For technical inquiries or academic collaboration, please reach out via [wz13124154500@outlook.com](mailto:wz13124154500@outlook.com).*
