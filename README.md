# Vidu-S1

<p align="center">
  <b><font size="8">Vidu S1: A Real-Time Interactive Video Generation Model</font></b>
</p>

<p align="center">
  <a href="https://vidu.com/vidu-stream">
    <img alt="Demo" src="https://img.shields.io/badge/Demo-Vidu_Stream-2f6fed?style=for-the-badge&logo=googlegemini&logoColor=white">
  </a>
  <a href="#citation">
    <img alt="Paper" src="https://img.shields.io/badge/Paper-arXiv_Coming_Soon-b31b1b?style=for-the-badge&logo=arxiv&logoColor=white">
  </a>
  <a href="#documentation">
    <img alt="English Documentation" src="https://img.shields.io/badge/Docs-English-2f6fed?style=for-the-badge&logo=readthedocs&logoColor=white">
  </a>
  <a href="#documentation">
    <img alt="Chinese Documentation" src="https://img.shields.io/badge/Docs-Chinese-2f6fed?style=for-the-badge&logo=readthedocs&logoColor=white">
  </a>
  <a href="#api-usage">
    <img alt="API Usage" src="https://img.shields.io/badge/API-Usage-00a67d?style=for-the-badge&logo=fastapi&logoColor=white">
  </a>
</p>

<p align="center">
  <img src="figures/overview.png" alt="Vidu S1 Overview" width="100%">
</p>

---

## Introduction

Vidu S1 is a real-time interactive video generation model for voice-controlled digital characters. Users can guide generated video content at any moment through spoken instructions, enabling live interaction instead of the conventional offline, one-shot generation workflow.

The model supports infinite-length real-time generation while preserving visual quality, identity consistency, and audio-video synchronization. Built with TurboDiffusion and TurboServe, Vidu S1 generates 540p video at up to **42 FPS** on consumer GPUs.

Vidu S1 supports personalized characters from user-uploaded images, including real people, anime-style characters, and pets. It can also respond to different voice tones and action instructions, making it suitable for live conversation, virtual hosts, entertainment avatars, and educational agents.

## Links

### Documentation

- **English User Guide**: Coming soon.
- **中文使用说明**: 待补充。

### Websites

- **Playable Demo**: [vidu.com/vidu-stream](https://vidu.com/vidu-stream)
- **Product Homepage**: Coming soon.
- **arXiv Paper**: Coming soon.

### API Usage

- **API Documentation**: Coming soon.
- **API Quickstart**: Coming soon.
- **SDK / Integration Guide**: Coming soon.

## Updates

- **[2026-07]**: Vidu S1 technical README released.
- **[2026-07]**: Playable online demo is available at [vidu.com/vidu-stream](https://vidu.com/vidu-stream).

## Method Highlights

Vidu S1 is designed around four goals: continuous user interaction, explicit speech-guided future control, stable long-horizon generation, and practical real-time serving.

- **Speech-guided future control**: spoken instructions directly condition future video content, allowing users to intervene during generation.
- **Infinite streaming inference**: sliding-window decoding, persistent reference context, RoPE repositioning, and TwinCache keep per-step latency constant while supporting open-ended generation.
- **Three-stage training**: Vidu S1 first trains a bidirectional video-audio teacher, adapts it into a causal autoregressive teacher with Teacher Forcing and Diffusion Forcing, then distills it with DMD and PCM regularization for efficient few-step generation.
- **Efficient serving stack**: TurboDiffusion, TurboServe, attention acceleration, W8A8 quantized GEMM, kernel fusion, CUDA Graph, and multi-GPU parallelism enable real-time 540p generation.

## Evaluation Results

### HDTF Benchmark

Vidu S1 achieves leading quantitative results among audio-driven avatar generation systems while also supporting instruction following and real-time inference.

| Model | Instruction Following | Real-Time | Resolution | FPS / Throughput | CSIM ↑ | Sync-D ↓ | DOVER ↑ |
| --- | --- | --- | --- | ---: | ---: | ---: | ---: |
| OmniAvatar | No | No | 480p | -- | 0.8062 | 9.242 | 0.5476 |
| StableAvatar-1.3B | No | No | 480p | -- | 0.8358 | 11.18 | 0.5560 |
| Hallo3 | No | No | 480x720 | -- | 0.7698 | 8.660 | 0.5313 |
| Wan2.2-S2V-14B | No | No | 480p/720p | -- | 0.7936 | 8.255 | 0.5510 |
| LiveAvatar | No | Yes | -- | -- | 0.8127 | 8.447 | 0.5639 |
| LemonSlice | No | Yes | 368x560 | -- | 0.8407 | 7.921 | 0.5196 |
| HeyGen | No | Yes | -- | 25 FPS | 0.9191 | 8.037 | 0.4864 |
| Kling Avatar 2.0 | Yes | No | -- | -- | 0.8688 | 8.158 | 0.5406 |
| **Vidu S1** | **Yes** | **Yes** | **540p (960x540)** | **42 FPS** | **0.9192** | **7.8470** | **0.5660** |

### Vidu-StreamBench

Vidu-StreamBench contains 500 samples with action instructions, reference first frames, and audio clips. It evaluates whether generated avatars can move naturally, remain stable over time, preserve identity, follow user instructions, and maintain coherent audio-video behavior in realistic streaming settings.

In pairwise human preference tests, Vidu S1 is consistently preferred overall against leading commercial systems.

| Comparison | Vidu S1 Preferred | Same | Other Preferred |
| --- | ---: | ---: | ---: |
| Vidu S1 vs. HeyGen | 56% | 16% | 28% |
| Vidu S1 vs. LemonSlice | 46% | 24% | 30% |
| Vidu S1 vs. Kling Avatar 2.0 | 48% | 22% | 30% |

Vidu S1 is especially strong in subject controllability, reaching **100%** preference against HeyGen and LemonSlice and **60%** preference against Kling Avatar 2.0.

## Citation

If you find Vidu S1 useful for your research, please cite:

```bibtex
@misc{zhang2026vidus1realtimeinteractive,
      title={Vidu S1: A Real-Time Interactive Video Generation Model},
      author={Jintao Zhang and Kai Jiang and Jintao Chen and Xu Wang and Yang Luo and Yuji Wang and Dechuang Chen and Jungang Li and Chengyang Ye and Marco Chen and Hongzhou Zhu and Min Zhao and Yuxuan Jiang and Zhengkun Huang and Chendong Xiang and Kaiwen Zheng and Haoxu Wang and Xiaohang Wang and Qi Jia and Xin Chen and Yimin Chen and Youhe Jiang and Fangcheng Fu and Zhijie Deng and Fan Bao and Jianfei Chen and Jun Zhu},
      year={2026},
      archivePrefix={arXiv},
      % eprint={},
      % url={}
}
```
