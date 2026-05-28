<div align="center">

<img src="assets/qwen-logo.png" alt="Qwen-VLA" width="150"/>

# Qwen-VLA

**Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments**

<p align="center">
  <b>Qwen Team</b>
</p>

<p align="center">
  <a href="#">📑 Paper</a> |
  <a href="#">📖 Blog</a> |
  <a href="#">🖥️ Demo</a> |
  <a href="https://discord.gg/CV4E9rpNSD">🫨 Discord</a>
</p>

<p align="center">
  <a href="#"><img src="https://img.shields.io/static/v1?label=Paper&message=Technical_Report&color=red&logo=arxiv"></a>
  <a href="#"><img src="https://img.shields.io/badge/Blog-Qwen_VLA-blue"></a>
  <a href="#"><img src="https://img.shields.io/badge/Demo-Online-orange"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-green.svg"></a>
</p>

</div>

---

Welcome to the official repository of **Qwen-VLA**. Here, you can find official information about Qwen-VLA, post your questions ([Issues](https://github.com/QwenLM/Qwen-VLA/issues)), and share your ideas with the community ([Discussions](https://github.com/QwenLM/Qwen-VLA/discussions)).

## 🎬 Demo

<div align="center">
  <video src="assets/normal_video.mp4" width="100%" controls></video>
</div>

## 💡 Introduction

<div align="center">
  <img src="assets/qwenvla_overview.png" alt="Qwen-VLA Overview" width="90%"/>
</div>

<br>

**Qwen-VLA** is a unified vision-language-action generalist model built upon **Qwen3.5-4B** (vision-language backbone) and a **1.15B DiT flow-matching action decoder**. It casts manipulation, navigation, and trajectory prediction into a shared action-and-trajectory prediction framework, enabling a single model to learn from heterogeneous embodied data across tasks, environments, and 10+ robot embodiments via embodiment-aware prompt conditioning &mdash; no per-platform output heads needed.

A single Qwen-VLA generalist, trained jointly on all data, **matches or outperforms task-specific specialists** fine-tuned independently per benchmark on 4/5 simulation benchmarks, pushing embodied intelligence from "skill specialists" toward "generalist actors."

### ✨ Key Highlights

- **🏆 One Generalist Beats Specialists.** A single model matches or outperforms per-benchmark specialists on 4/5 simulation benchmarks.

- **🔗 Unified Action-and-Trajectory Framework.** Manipulation, navigation, egocentric action modeling, and trajectory prediction share one action-and-trajectory prediction space.

- **🤖 Embodiment-Aware Prompt Conditioning.** One set of weights serves 10+ platforms; switching embodiments requires only changing a text prompt.

- **📈 Progressive Training Recipe.** A four-stage pipeline &mdash; Text-to-Action DiT Pretraining (T2A), Continued Pretraining (CPT), Supervised Fine-Tuning (SFT), and Reinforcement Learning (RL) &mdash; bridges discrete vision-language tokens and continuous action trajectories. T2A first trains the DiT action decoder as a language-conditioned action decompressor without any visual input, learning structured action priors from text alone; subsequent stages then ground this prior in visual observations and optimize closed-loop task success.

- **🌍 Strong Real-World OOD Generalization.** 83.6% in-domain and 76.9% OOD average success on the ALOHA bimanual platform.

## 🏆 Benchmarks

### Manipulation & Navigation

As a **unified generalist policy**, Qwen-VLA is trained once on all embodiments jointly and evaluated across all platforms without per-benchmark adaptation, simultaneously handling both manipulation and navigation.

| Model | LIBERO | RoboCasa-GR1 | Simpler-WidowX | RoboTwin-Easy | RoboTwin-Hard | R2R OS | R2R SR | RxR SR |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Qwen-VLA-Base** | 90.8 | 40.4 | 64.3 | 64.3 | 66.4 | 61.7 | 53.8 | 55.1 |
| **Qwen-VLA-Instruct** | **97.9** | **56.7** | **73.7** | **86.1** | **87.2** | **69.0** | **57.5** | **59.6** |

### Real-World Results (ALOHA)

On the ALOHA bimanual platform, GR00T N1.6 and &pi;<sub>0.5</sub> are **per-task specialist** models fine-tuned independently, while **Qwen-VLA is a single all-in-one generalist** that handles all tasks, embodiments, and modalities within one unified model.

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

| Model | SimplerEnv-OOD SR (%) | DOMINO SR (%) | DOMINO MS |
| :--- | :---: | :---: | :---: |
| **Qwen-VLA-Base** | 25.3 | 21.1 | 37.4 |
| **Qwen-VLA-Instruct** | **32.0** | **26.6** | **39.5** |

> SimplerEnv-OOD: fine-tuned solely on simple pick-and-place, evaluated on unseen spatial and visual tasks.
> DOMINO: zero-shot evaluation on dynamic manipulation with moving objects &mdash; no dynamic training data used.

## 📜 Citation

If you find our work helpful, feel free to give us a cite.

```bibtex
@article{qwenvla,
  title={Qwen-VLA: Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments},
  author={Qwen Team},
  year={2025}
}
```

## License Agreement

All our open-weight models are licensed under Apache 2.0.
You can find the license files in the respective model repositories.

## Contact Us

If you are interested in leaving a message to either our research team or product team, join our [Discord](https://discord.gg/CV4E9rpNSD)!
