# Gemma 4 Hardware Guide

Sources:

- <https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/>
- <https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/>

Google lists Gemma 4 in E2B, E4B, 26B A4B, and 31B sizes. This repository uses those sourced model names and marks hardware/VRAM recommendations as estimates unless a vendor runtime publishes exact numbers.

Memory requirements vary by context length, KV cache, multimodal inputs, batch size, runtime, GPU driver overhead, and quantization format.

| Model | Best fit | Q4 estimated VRAM | BF16/FP16 calculated weight memory |
|---|---|---:|---:|
| E2B | Edge/mobile/low-end | 2-4 GB | About 4 GB before overhead |
| E4B | Laptop/dev daily driver | 4-6 GB | About 8 GB before overhead |
| 26B A4B | High-end consumer hardware | 16-24 GB | About 52 GB before overhead |
| 31B | Workstation class | 20-32 GB | About 62 GB before overhead |

Q8 values are intentionally not labeled as sourced in this repo. Benchmark the exact runtime, context, quantization, and artifact before publishing hard requirements.

