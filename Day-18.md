### Day-18 (19-07-2024)

---

### Generative AI

Generative AI refers to artificial intelligence systems that can generate various forms of content such as text, images, video, and audio. Examples include:
- **ChatGPT** for text generation
- **DALL-E** for image generation
- **Sora** for video generation
- **Whisper** for speech-to-text and text-to-speech
- **Gemini** and **LLaMA** for text and multimodal content

### Large Language Model (LLM)

Large Language Models (LLMs) are AI systems that understand and generate human language. They are trained on vast datasets to predict and produce coherent language.

**Input (Prompt)** → **LLM** → **Output (Completion)**

### Key Factors in Generative AI Performance

The performance of a generative AI depends on:
- **Architecture:** The design and structure of the AI model.
- **Parameters:** The number of tunable elements within the model. Generally, more parameters suggest greater potential capability, but this is not always true.

**Examples of LLMs:**
- **ChatGPT 4.0:** 1.7 to 2 trillion parameters
- **LLaMA:** 140 billion parameters
- **Claude:** 175 billion parameters

Despite the difference in parameters, these models are comparably capable, with Claude being particularly strong in technical fields, illustrating that model performance is not solely determined by parameter count.

### Neural Networks

Neural networks are the foundation of many AI models and consist of:
- **Weights and Biases:** Core components that adjust during training.
- **Linear Algebra:** The mathematical basis for neural network operations.
- **Best for Numerical and Symbolic Data:** Neural networks excel in processing structured data.
- They are highly effective for image recognition tasks. They process images by converting them into pixel matrices and applying convolutional layers to detect features like edges, textures, and shapes.

### Recurrent Neural Networks (RNN)

- RNNs are designed for sequential data like text.
- They retain information from previous steps to influence current processing, but they struggle with large datasets due to issues like vanishing gradients.
- RNNs can analyze sequences of text to determine sentiment.
- For example, in movie reviews, an RNN might consider previous words to understand context and predict whether a review is positive or negative.

### Natural Language Processing (NLP)

NLP involves converting human language into embeddings (vector representations) that AI models can process. This field encompasses various techniques to understand and generate human language.

Diagram: NLP Workflow
```
+---------------------+
|       Text          |
|     (Human Lang)    |
+---------------------+
          |
          v
+---------------------+
|      Embeddings     |
|  (Vector Repr.)     |
+---------------------+
          |
          v
+---------------------+
|       AI Model      |
|  (Processing Text)  |
+---------------------+
          |
          v
+---------------------+
|      Output Text    |
|  (Generated Lang)   |
+---------------------+
```
### Transformers

In 2017, the "Attention is All You Need" paper by a team from Google Brain and the University of Toronto introduced the Transformer architecture, revolutionizing generative AI. Key components of Transformers include:
- **Encoder:** Converts input into embeddings.
- **Decoder:** Processes embeddings to generate output.
- **Attention Layers:** Focus on different parts of the input to capture context.
- **Feed Forward Network (FFN):** Processes data within each attention layer.
- **Softmax Layer:** Computes the probability of different outputs and selects the most likely one.

Diagram: Transformer Architecture
```
+---------------------+
|     Transformer     |
+---------------------+
|  +---------------+  |
|  |    Encoder    |  |
|  +-------+-------+  |
|          |          |
|  +-------+-------+  |
|  |   Attention   |  |
|  |    Layers     |  |
|  +-------+-------+  |
|          |          |
|  +-------+-------+  |
|  |      FFN      |  |
|  +-------+-------+  |
|          |          |
|  +-------+-------+  |
|  |    Decoder    |  |
|  +---------------+  |
+---------------------+
```

### Generation Techniques

Generative AI models can be created and improved using two main techniques:
1. **Prompt Engineering:** Crafting effective prompts to guide the AI in generating desired outputs.
2. **Fine-Tuning:** Adjusting a pre-trained model to perform specific tasks better.

**Types of Learning:**
- **One-Shot Learning:** The model learns from a single example.
- **Few-Shot Learning:** The model learns from a few examples.

### Fine-Tuning Types

1. **Full Fine-Tuning:**
   - Adjusts all parameters of an existing model.
   - Can lead to catastrophic forgetting, where the model loses knowledge of previously learned information.

2. **Parameter-Efficient Fine-Tuning (PEFT):**
   - Adjusts only a subset of parameters, making the process more efficient and reducing the risk of forgetting.

### Diagram of Transformer Architecture

Below is a simplified diagram of the Transformer architecture:

```plaintext
+---------------+
|    Encoder    |
|---------------|
| Embedding     |
| Multi-Head    |
| Attention     |
| Feed Forward  |
+---------------+
        ↓
+---------------+
|    Decoder    |
|---------------|
| Multi-Head    |
| Attention     |
| Feed Forward  |
| Softmax       |
+---------------+
        ↓
+---------------+
|   Output      |
+---------------+
```

---

These notes provide a  comprehensive understanding of the concepts and applications of generative AI and related technologies.
