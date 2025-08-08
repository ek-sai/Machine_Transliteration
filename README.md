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

⚙️ How It Works
The transliteration system is built on a sequence-to-sequence architecture using Gated Recurrent Units (GRUs) to learn character-level mappings from English (Latin) to Hindi (Devanagari) scripts. It has two variants:

1. GRU Encoder-Decoder (Without Attention)
🔄 Workflow:
Input Encoding:

Each English word is treated as a sequence of characters.

Characters are converted into embeddings and passed through a GRU encoder.

The final hidden state of the encoder is used as the initial state of the decoder.

Decoding:

The decoder GRU generates one character at a time in the Hindi script.

Teacher forcing is optionally used during training.

Prediction:

At inference, the model decodes step-by-step until an end-of-sequence token is predicted.

2. GRU Encoder-Decoder (With Attention)
🎯 Key Enhancement: Attention Mechanism
Instead of relying solely on the final encoder hidden state, the decoder uses attention to focus on all encoder outputs during each time step.

🔄 Workflow:
Input Encoding:

Same as above, using a GRU to encode the input character sequence into hidden states.

Attention Computation:

At each decoding step, attention weights are calculated between the current decoder hidden state and each encoder output.

These weights are used to compute a context vector — a weighted sum of encoder hidden states.

Decoding with Context:

The decoder GRU uses both the context vector and the current input embedding to generate the next character.

This allows the model to attend to different parts of the input dynamically.

🧠 Why GRU?
GRUs are simpler and faster than LSTMs, while still capturing temporal dependencies.

Suitable for low-resource tasks like character-level transliteration.

📚 Training Details
Loss Function: Cross-entropy loss (character-level)

Optimizer: Adam

Teacher Forcing: Used to speed up convergence

Character Vocabulary: Built separately for source (English) and target (Hindi)

🧪 Inference
During inference, the model:

Encodes the input English word

Decodes character-by-character in Hindi

Stops when an <eos> (end-of-sequence) token is predicted
