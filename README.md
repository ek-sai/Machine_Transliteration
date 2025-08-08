# English-to-Hindi Machine Transliteration using GRU

This project implements a **Machine Transliteration System** that converts English words (written in Latin script) into their phonetically equivalent forms in **Hindi (Devanagari script)** using custom-built **GRU-based encoder-decoder models**, both **with** and **without attention**.

---

## 🧠 Model Architectures

### 1. GRU Encoder-Decoder (Baseline)
A sequence-to-sequence model using:
- GRU-based encoder
- GRU-based decoder
- Trained using teacher forcing

### 2. GRU with Attention
An enhancement over the baseline model that:
- Computes attention weights over the encoder hidden states
- Produces context vectors dynamically during decoding
