STATQUEST :
Neural Networks Pt. 4: Multiple Inputs and Outputs
Neural Networks Part 5: ArgMax and SoftMax
# Softmax and Cross-Entropy: Neural Network Fundamentals

_Last updated: 2025-06-13_

This document consolidates important insights, derivations, and conceptual explanations related to the **Softmax activation function** and **Cross-Entropy loss**, two of the most essential tools for training classification models.

---

## 🔢 1. Softmax Activation Function

The **Softmax function** converts a vector of raw scores (logits) into probabilities that sum to 1.

### **Formula:**
For an input vector **z = [z₁, z₂, ..., zₙ]**:

```
softmax(zᵢ) = exp(zᵢ) / sum_j(exp(zⱼ))
```

### **Properties:**
- Outputs are in the range (0, 1).
- All outputs sum to 1.
- Preserves the **ranking** of logits.
- Emphasizes larger values due to the exponential.
- **Differentiable**, which is necessary for backpropagation.

---

## 🔁 2. Why Not Argmax?

- **Argmax** simply picks the index with the highest score but is **non-differentiable**.
- Without gradients, **weights and biases can’t be updated** during training.
- Softmax allows smooth updates by assigning probabilities and supporting backpropagation.

---

## 📐 3. Softmax Gradient (Jacobian)

For softmax output pᵢ, given logits z:

### **Derivative when i = j** (self-derivative):

```
∂pᵢ / ∂zᵢ = pᵢ (1 - pᵢ)
```

### **Derivative when i ≠ j** (cross-derivative):

```
∂pᵢ / ∂zⱼ = -pᵢ * pⱼ
```

These derivatives form the **Jacobian matrix** used in backpropagation for classification tasks.

---

## 📉 4. Cross-Entropy Loss

Used with softmax for multi-class classification.

### **Formula (for correct class label y):**
```
CE = -log(p_y)
```

Where **p_y** is the softmax probability assigned to the correct class.

### **Why it Works Well:**
- Provides **large gradients** when the prediction is very wrong (p → 0).
- Helps the model recover quickly from poor predictions.
- Encourages confident and correct predictions.

---

## ⚖️ 5. Comparison: Cross-Entropy vs. Squared Error (SSR)

| Aspect                         | Cross-Entropy       | Squared Error (SSR)      |
|--------------------------------|---------------------|---------------------------|
| Behavior for wrong predictions | Strong penalty      | Mild penalty              |
| Gradients                      | Large (fast learning) | Small (slow learning)     |
| Suited for                     | Classification      | Regression                |
| Formula                        | -log(p)             | (1 - p)^2                 |

### Visual Insight:
- CE spikes near p = 0, driving faster weight updates.
- SSR stays relatively flat, not helpful when predictions are very wrong.

---

## 🧪 6. Practical Example:

If a neural network outputs:

```
Setosa:     0.57
Versicolor: 0.31
Virginica:  0.12
```

- **Correct class** = Setosa
- **Cross Entropy** = -log(0.57) ≈ 0.56
- **Squared Error** = (1 - 0.57)^2 = 0.1849

---

## ⚠️ 7. Key Pitfalls and Tips

- Never use `argmax` during training — it blocks gradients.
- Use `softmax + cross-entropy` together, not separately. Most libraries (e.g., PyTorch's `nn.CrossEntropyLoss`) handle this efficiently in one step.
- Avoid SSR in classification tasks — gradients are too gentle.
- Softmax outputs can be unstable with large logits — apply **log-sum-exp trick** if coding manually.

---

## 📌 Summary

| Concept           | Purpose                     | Key Formula                          |
|-------------------|-----------------------------|---------------------------------------|
| Softmax           | Convert logits to probs     | exp(zᵢ) / Σexp(zⱼ)                    |
| CE Loss           | Penalize incorrect guesses  | -log(p_y)                             |
| Softmax Gradients | Backpropagation             | ∂pᵢ/∂zᵢ = pᵢ(1 - pᵢ); ∂pᵢ/∂zⱼ = -pᵢpⱼ |

---

## 💡 Extra Insight

Softmax + CE loss is not just about math — it reflects a model’s **confidence**. Encouraging the right kind of confidence is what drives better generalization and sharper decision boundaries.

---
