# 🌍 English-to-Hindi Machine Transliteration

[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.0+-red.svg)](https://pytorch.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **Transform English words into their Hindi (Devanagari) equivalents using deep learning!**

This project implements an advanced **Machine Transliteration System** that converts English words (Latin script) into phonetically equivalent Hindi (Devanagari script) using state-of-the-art **GRU-based encoder-decoder architectures**.

## ✨ Features

- 🔤 **Character-level transliteration** from English to Hindi
- 🧠 **Two model variants**: Baseline GRU and GRU with Attention
- 📊 **Teacher forcing** for accelerated training
- 🎯 **Attention mechanism** for improved accuracy
- 📈 **Performance comparison** between architectures

## 🏗️ Model Architectures

### 1. 🔄 GRU Encoder-Decoder (Baseline)
A classic sequence-to-sequence model featuring:
- **GRU-based encoder** for input processing
- **GRU-based decoder** for output generation
- **Teacher forcing** during training phase

### 2. 🎯 GRU with Attention (Enhanced)
An advanced model that adds:
- **Dynamic attention weights** over encoder hidden states
- **Context vector computation** for better decoding
- **Improved accuracy** through selective focus

## 🔬 How It Works

### Without Attention 🔄
```
English Input → GRU Encoder → Final Hidden State → GRU Decoder → Hindi Output
    "HOME"         [h1,h2,h3,h4]        h4           Step-by-step    "होम"
```

### With Attention 🎯
```
English Input → GRU Encoder → All Hidden States → Attention → Context Vector → GRU Decoder → Hindi Output
    "HOME"         [h1,h2,h3,h4]      Weighted Sum     Dynamic        Step-by-step    "होम"
```

## 📊 Performance Comparison

| Model | Accuracy | Training Time | Parameters |
|-------|----------|---------------|------------|
| **Baseline GRU** | ~84% | Faster | Fewer |
| **GRU + Attention** | ~90% | Moderate | More |

## 🚀 Getting Started

### Prerequisites
```bash
pip install torch torchvision numpy pandas matplotlib seaborn
```

## 🧠 Technical Details

### Architecture Components
- **Input Size**: 27 (English alphabet + padding)
- **Hidden Size**: 256 neurons
- **Output Size**: 128+ (Hindi characters + padding)
- **Max Output Length**: 30 characters

### Training Configuration
- **Optimizer**: Adam (lr=0.001)
- **Loss Function**: Negative Log Likelihood
- **Batch Size**: 128
- **Training Batches**: 2,500
- **Teacher Forcing**: First 1/3 of training

### Attention Mechanism
```python
# Attention computation
U = self.U(encoder_output)           # Linear transformation
W = self.W(decoder_state)            # Current decoder state
V = self.attn(torch.tanh(U + W))     # Attention scores
attn_weights = F.softmax(V, dim=0)   # Attention weights
context = torch.mm(attn_weights.T, encoder_output)  # Context vector
```

## 📈 Training Process

1. **Data Loading**: XML corpus with English-Hindi word pairs
2. **Preprocessing**: Character-level tokenization and one-hot encoding
3. **Training**: Batch-wise training with teacher forcing
4. **Validation**: Real-time accuracy monitoring
5. **Inference**: Greedy decoding for transliteration

## 🎯 Key Advantages

- ✅ **Language Agnostic**: Architecture can be adapted for other language pairs
- ✅ **Character-Level**: Handles out-of-vocabulary words effectively
- ✅ **Attention**: Focuses on relevant input characters dynamically
- ✅ **Lightweight**: GRU-based design for efficiency

## 📚 Dataset

Uses the **NEWS 2012 English-Hindi Transliteration Dataset**:
- **Training**: 13,937 word pairs
- **Testing**: 1,000 word pairs
- **Format**: XML with parallel English-Hindi entries

## 🔧 Usage Examples

```python
# Test different words
test(net, 'DELHI')     # Output: DELHI-दिल्ली
test(net, 'MUMBAI')    # Output: MUMBAI-मुंबई
test(net, 'CRICKET')   # Output: CRICKET-क्रिकेट
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.


## 🙏 Acknowledgments

- **NEWS 2012 Shared Task** for the transliteration dataset
- **PyTorch Team** for the deep learning framework
- **Research Community** for encoder-decoder architecture innovations

---

<div align="center">

**⭐ Star this repository if you found it helpful!**

Made with ❤️ for the NLP community

</div>
