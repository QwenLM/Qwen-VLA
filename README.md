<div align="center">

<img src="assets/qwen-logo.png" alt="Qwen-VLA" width="150"/>

<h1 style="border: none;">Qwen-VLA</h1>

<p><b>Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments</b></p>

<p align="center">
  <b>Qwen Team</b>
</p>

<p align="center">
    <a href="https://github.com/QwenLM/Qwen-VLA">📑 Paper</a> |
    <a href="https://github.com/QwenLM/Qwen-VLA">📖 Blog</a> |
    <a href="https://github.com/QwenLM/Qwen-VLA">🖥️ Demo</a>
</p>


</div>

Welcome to the official repository of **Qwen-VLA**. Here, you can find official information about Qwen-VLA and post your questions ([Issues](https://github.com/QwenLM/Qwen-VLA/issues)).

## 🎬 Demo

<div align="center">
  <video src="assets/normal_video.mp4" width="100%" controls></video>
</div>

## 💡 Introduction

<div align="center">
  <img src="assets/qwenvla_overview.png" alt="Qwen-VLA Overview" width="90%"/>
</div>

<br>

**Qwen-VLA** is a unified vision-language-action generalist model built upon **Qwen3.5-4B** (vision-language backbone) and a **1.15B DiT flow-matching action decoder**. It casts manipulation, navigation, and trajectory prediction into a shared action-and-trajectory prediction framework, enabling a unified model to learn from heterogeneous embodied data across tasks, environments, and 10+ robot embodiments via embodiment-aware prompt conditioning, no per-platform output heads needed.

A unified Qwen-VLA generalist **matches or outperforms task-specific specialists** fine-tuned independently per benchmark across multiple simulation and real-world evaluations, pushing embodied intelligence from "skill specialists" toward "generalist actors."

### ✨ Key Highlights

- **🏆 One Generalist Beats Specialists.** A unified model matches or outperforms per-benchmark specialists across multiple simulation and real-world evaluations.

- **🔗 Unified Action-and-Trajectory Framework.** Manipulation, navigation, egocentric action modeling, and trajectory prediction share one action-and-trajectory prediction space.

- **🤖 Embodiment-Aware Prompt Conditioning.** One set of weights serves 10+ platforms; switching embodiments requires only changing a text prompt.

- **📈 Progressive Training Recipe.** A progressive training recipe that includes large-scale action pretraining, multimodal continued pretraining, supervised fine-tuning, and reinforcement learning, bridging the gap between discrete vision-language tokens and continuous action trajectories, improving both training stability and downstream transfer.

- **🌍 Strong Real-World OOD Generalization.** Large-scale embodied pretraining enables robust generalization to unseen conditions in real-world deployment, significantly outperforming specialist baselines.

## 🏆 Benchmarks

### Manipulation & Navigation

As a **unified generalist policy**, Qwen-VLA is trained once on all embodiments jointly and evaluated across all platforms without per-benchmark adaptation, simultaneously handling both manipulation and navigation.

| Model | LIBERO | RoboCasa-GR1 | Simpler-WidowX | RoboTwin-Easy | RoboTwin-Hard | R2R OS | R2R SR | RxR SR |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Qwen-VLA-Base** | 90.8 | 40.4 | 64.3 | 64.3 | 66.4 | 61.7 | 53.8 | 55.1 |
| **Qwen-VLA-Instruct** | **97.9** | **56.7** | **73.7** | **86.1** | **87.2** | **69.0** | **57.5** | **59.6** |

### Real-World Results

On the ALOHA bimanual platform, GR00T N1.6 and &pi;<sub>0.5</sub> are **per-task specialist** models fine-tuned independently, while **Qwen-VLA is a unified all-in-one generalist** that handles all tasks, embodiments, and modalities within one unified model.

**In-Domain Performance (Success Rate %)**

| Model | Pick & Place | Table Cleaning | Bowl Stacking | Bowl Pick & Place | Towel Folding | Fine-grained | **Avg** |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| GR00T N1.6 | 30.8 | 38.5 | 53.8 | 19.2 | 19.2 | 10.3 | 28.6 |
| &pi;<sub>0.5</sub> | 73.1 | 84.6 | 88.5 | 69.2 | **80.8** | 33.3 | 71.6 |
| Qwen-VLA-aloha (w/o pretrain) | 30.8 | 53.8 | 61.5 | 64.1 | 50.0 | 30.8 | 48.5 |
| **Qwen-VLA-aloha (w/ pretrain)** | **96.2** | **92.3** | **98.7** | **87.2** | 65.4 | **61.5** | **83.6** |

**OOD Performance (Success Rate %)**

| Model | Color | Instance | Position | Background | Instruction | **Avg** |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| GR00T N1.6 | 46.2 | 38.5 | 3.8 | 19.2 | 19.2 | 25.4 |
| &pi;<sub>0.5</sub> | 57.7 | 61.5 | 19.2 | 26.9 | 42.3 | 41.5 |
| Qwen-VLA-aloha (w/o pretrain) | 42.3 | 30.8 | 34.6 | 30.8 | 42.3 | 36.2 |
| **Qwen-VLA-aloha (w/ pretrain)** | **88.5** | **76.9** | **53.8** | **80.8** | **84.6** | **76.9** |

### Out-of-Distribution Generalization

| Model | SimplerEnv-OOD SR (%) | DOMINO SR (%) | DOMINO MS (%) |
| :--- | :---: | :---: | :---: |
| **Qwen-VLA-Base** | 25.3 | 21.1 | 37.4 |
| **Qwen-VLA-Instruct** | **32.0** | **26.6** | **39.5** |

> SimplerEnv-OOD: fine-tuned solely on simple pick-and-place, evaluated on unseen spatial and visual tasks.
> DOMINO: zero-shot evaluation on dynamic manipulation with moving objects, no dynamic training data used.

## 📜 Citation

If you find our work helpful, feel free to give us a cite.

```bibtex
@article{qwenvla,
  title={Qwen-VLA: Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments},
  author={Qwen Team},
  year={2025}
}
```

