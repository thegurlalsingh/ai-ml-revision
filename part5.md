## Table of Contents

- [1. Learning Rate Schedulers](#1-learning-rate-schedulers)
- [Why Change the Learning Rate?](#why-change-the-learning-rate)
- [Constant Learning Rate](#constant-learning-rate)
- [Step Learning Rate (StepLR)](#step-learning-rate-steplr)
- [Cosine Annealing](#cosine-annealing)
- [OneCycle Learning Rate](#onecycle-learning-rate)
- [Warmup](#warmup)
- [Learning Rate Finder](#learning-rate-finder)
- [Practical Interview Values](#practical-interview-values)
- [Comparison Table](#comparison-table)
- [Interview Questions](#interview-questions--learning-rate)
- [Easy Memory Trick](#easy-memory-trick)
- [2. BatchNorm vs LayerNorm](#2-batchnorm-vs-layernorm)
- [Why Do We Need Normalization?](#why-do-we-need-normalization)
- [BatchNorm](#batchnorm)
- [The γ and β Parameters](#the-γ-and-β-parameters)
- [Training vs Inference](#training-vs-inference)
- [Problem with Small Batch Sizes](#problem-with-small-batch-sizes)
- [LayerNorm](#layernorm)
- [Why LayerNorm for Transformers?](#why-layernorm-for-transformers)
- [Comparison Table](#comparison-table-1)
- [Interview Questions](#interview-questions--normalization)
- [Easy Memory Trick](#easy-memory-trick-1)
- [3. Debugging a Neural Network That Isn't Training](#3-debugging-a-neural-network-that-isnt-training)
- [Tiny Overfit Test](#tiny-overfit-test)
- [Check Data Normalization](#check-data-normalization)
- [Visualize Inputs and Labels](#visualize-inputs-and-labels)
- [Check the Learning Rate](#check-the-learning-rate)
- [Vanishing and Exploding Gradients](#vanishing-and-exploding-gradients)
- [Activation Distribution](#activation-distribution)
- [Fixes for Vanishing Gradients](#fixes-for-vanishing-gradients)
- [Fixes for Exploding Gradients](#fixes-for-exploding-gradients)
- [Complete Debugging Checklist](#complete-debugging-checklist)
- [Interview Answer](#interview-answer)
- [4. NaNs, Dead ReLUs, BatchNorm Problems, Noisy Labels & Logging](#4-nans-dead-relus-batchnorm-problems-noisy-labels--logging)
- [NaNs During Training](#nans-during-training)
- [Dead ReLU](#dead-relu)
- [BatchNorm Problems](#batchnorm-problems)
- [Noisy Labels & Robust Training](#noisy-labels--robust-training)
- [Training Suddenly Diverges](#training-suddenly-diverges)
- [Logging & Observability](#logging--observability)
- [Complete Interview Debugging Flow](#complete-interview-debugging-flow)
- [Interview-Ready Summary](#interview-ready-summary)
- [5. Scaled Dot-Product Attention](#5-scaled-dot-product-attention)
- [What Problem Is Attention Solving?](#what-problem-is-attention-solving)
- [Every Word Creates Three Vectors (Q, K, V)](#every-word-creates-three-vectors-q-k-v)
- [Dot Product](#dot-product)
- [Matrix Form (QKᵀ)](#matrix-form-qkᵀ)
- [Softmax](#softmax)
- [Multiply with V](#multiply-with-v)
- [Entire Pipeline](#entire-pipeline)
- [Why Divide by √dₖ?](#why-divide-by-√dₖ)
- [Complete Formula](#complete-formula)
- [Interview Questions](#interview-questions--attention)
- [Easy Memory Trick](#easy-memory-trick-2)
- [6. Multi-Head Attention](#6-multi-head-attention)
- [What's Wrong With a Single Head?](#whats-wrong-with-a-single-head)
- [Multi-Head Attention](#multi-head-attention)
- [Create Multiple Q, K, V](#create-multiple-q-k-v)
- [Why Divide the Dimensions?](#why-divide-the-dimensions)
- [Concatenate and Final Linear](#concatenate-and-final-linear)
- [Complete Flow](#complete-flow)
- [Why Not Just One Big Head?](#why-not-just-one-big-head)
- [Interview Answer](#interview-answer-1)
- [Easy Memory Trick](#easy-memory-trick-3)
- [7. Complexity Analysis — O(n²)](#7-complexity-analysis-on)
- [Why Quadratic?](#why-quadratic)
- [Why Is Computing QKᵀ O(n²dₖ)?](#why-is-computing-qkᵀ-on²dₖ)
- [Softmax Complexity](#softmax-complexity)
- [Multiplying by V](#multiplying-by-v)
- [Total Cost](#total-cost)
- [What About Multiple Heads?](#what-about-multiple-heads)
- [Memory Problem](#memory-problem)
- [Practical Mitigations](#practical-mitigations)
- [Interview Questions](#interview-questions--complexity)
- [8. Residuals & LayerNorm](#8-residuals--layernorm)
- [Residual Connection](#residual-connection)
- [Layer Normalization](#layer-normalization)
- [The γ and β Parameters](#the-γ-and-β-parameters-1)
- [Transformer Block (Post-Norm)](#transformer-block-post-norm)
- [Pre-Norm vs Post-Norm](#pre-norm-vs-post-norm)
- [Why Is Pre-Norm Better?](#why-is-pre-norm-better)
- [Quick Comparison](#quick-comparison)
- [Interview Answers](#interview-answers)
- [9. Positional Encodings](#9-positional-encodings)
- [Why Do Transformers Need Positional Encoding?](#why-do-transformers-need-positional-encoding)
- [Original Sinusoidal Positional Encoding](#original-sinusoidal-positional-encoding)
- [Why Sine and Cosine?](#why-sine-and-cosine)
- [Learned Absolute Positional Embeddings](#learned-absolute-positional-embeddings)
- [Relative Position Encoding](#relative-position-encoding)
- [RoPE (Rotary Position Embedding)](#rope-rotary-position-embedding)
- [Comparison Table](#comparison-table-2)
- [Interview Questions](#interview-questions--positional)
- [10. Components to Implement (Transformer Architecture)](#10-components-to-implement-transformer-architecture)
- [Overall Transformer Block](#overall-transformer-block)
- [Scaled Dot-Product Attention Function](#scaled-dot-product-attention-function)
- [Causal / Attention Mask](#causal--attention-mask)
- [Multi-Head Wrapper](#multi-head-wrapper)
- [Feed-Forward Network](#feed-forward-network)
- [Residual + LayerNorm (Pre-Norm)](#residual--layernorm-pre-norm)
- [Output Projection (LM Head)](#output-projection-lm-head)
- [Masking Details](#masking-details)
- [Stable Softmax](#stable-softmax)
- [Interview-Level Understanding](#interview-level-understanding)
- [11. Causal Mask vs Padding Mask & Other Fundamentals](#11-causal-mask-vs-padding-mask--other-fundamentals)
- [Causal Mask vs Padding Mask](#causal-mask-vs-padding-mask)
- [Why Is There a Feed-Forward Network After Attention?](#why-is-there-a-feed-forward-network-after-attention)
- [Why Residual Connections?](#why-residual-connections)
- [Why LayerNorm?](#why-layernorm)
- [Complete Transformer Block (Modern Pre-Norm)](#complete-transformer-block-modern-pre-norm)
- [One-Line Summary](#one-line-summary)
- [12. Dataset & Training Recipe](#12-dataset--training-recipe)
- [Dataset](#dataset)
- [Fixed Sequence Length](#fixed-sequence-length)
- [Optimizer](#optimizer)
- [Warmup](#warmup-1)
- [Batch Size](#batch-size)
- [Loss](#loss)
- [Gradient Clipping](#gradient-clipping)
- [Learning Rate Schedule](#learning-rate-schedule)
- [Epochs](#epochs)
- [Sampling](#sampling)
- [Training Curves](#training-curves)
- [Validation](#validation)
- [Hyperparameter Table](#hyperparameter-table)
- [Final Conclusion](#final-conclusion)
- [Shift By One](#shift-by-one)
- [13. Tokenization Essentials](#13-tokenization-essentials)
- [BPE (Byte Pair Encoding)](#bpe-byte-pair-encoding)
- [WordPiece](#wordpiece)
- [SentencePiece](#sentencepiece)
- [Vocabulary Size Tradeoff](#vocabulary-size-tradeoff)
- [Quick Comparison](#quick-comparison-1)
- [Interview Answers](#interview-answers-1)
- [14. Practical Masking & Batching Strategies](#14-practical-masking--batching-strategies)
- [Padding & Attention Mask](#padding--attention-mask)
- [Bucketing (Length Batching)](#bucketing-length-batching)
- [Packing Sequences](#packing-sequences)
- [Causal Mask](#causal-mask)
- [Combining Padding Mask + Causal Mask](#combining-padding-mask--causal-mask)
- [Interview Summary](#interview-summary)
- [15. Efficiency & Scaling Pointers](#15-efficiency--scaling-pointers)
- [Mixed Precision (AMP)](#mixed-precision-amp)
- [Gradient Accumulation](#gradient-accumulation)
- [Activation Checkpointing](#activation-checkpointing)
- [FlashAttention](#flashattention)
- [Fused QKV Projection](#fused-qkv-projection)
- [Weight Tying](#weight-tying)
- [Long Context Solutions](#long-context-solutions)
- [Practical Tokenization Exercise](#practical-tokenization-exercise)
- [Interview Summary Table](#interview-summary-table)
- [For AI/ML Intern Interviews](#for-aiml-intern-interviews)

---

## 1. Learning Rate Schedulers

> This is one of the most practical interview topics because learning rate (LR) often matters more than the optimizer itself.

An interviewer might ask:

- What is a learning rate scheduler?
- Why not keep the learning rate constant?
- What is warmup?
- Why does OneCycle work?

### Why Change the Learning Rate?

Recall gradient descent:

$$\theta = \theta - \eta \nabla L$$

where:

- $\theta$ = weights
- $\eta$ = learning rate

The learning rate controls how big each step is. Imagine climbing down a mountain. At the beginning, you're far from the bottom. Large steps help. Near the bottom, large steps make you overshoot. You need smaller steps. That's why we change the learning rate during training.

### Constant Learning Rate

Simplest approach:

Epoch 1 → 0.01 Epoch 50 → 0.01 Epoch 100 → 0.01

Always the same.

Problem: Suppose the minimum is here. A large constant learning rate keeps bouncing around the minimum, never settling properly. A small constant learning rate is very slow. So constant LR is rarely optimal.

### Step Learning Rate (StepLR)

Idea: Train normally. After certain epochs, reduce the learning rate.

Example:

| Epochs | LR |
|--------|-----|
| 1–30 | 0.1 |
| 31–60 | 0.01 |
| 61–90 | 0.001 |

Notice: every milestone reduces LR by 10×.

Why? Early training needs large steps. Later training needs careful fine-tuning.

Visually it looks like stairs — hence the name StepLR.

### Cosine Annealing

Instead of suddenly dropping the LR, decrease smoothly following a cosine wave.

Why better? StepLR drops from 0.1 → 0.01 in one jump, causing a sudden optimizer behavior change. Cosine goes 0.1 → 0.09 → 0.08 → 0.07 → ... much smoother.

> Interview Answer: Cosine annealing gradually decreases the learning rate instead of making sudden drops, leading to smoother optimization and often better convergence.

### OneCycle Learning Rate

Instead of decreasing immediately, it first increases, then decreases.

Why increase first? If the initial LR is too small (e.g., 0.0001), training barely moves. Increasing the LR helps the model explore the loss landscape faster. Then decreasing it handles fine-tuning.

Why does it work? Higher learning rates early help escape poor local minima and saddle points. Lower learning rates later help settle into a good minimum. This often gives faster convergence and better final accuracy.

OneCycle is commonly used with:

- SGD + Momentum
- FastAI
- Vision models

### Warmup

One of the most common interview questions.

Suppose you're training GPT with millions of parameters and random initialization. If you immediately use LR = 0.001, the first update may be enormous and training may diverge.

Instead, start tiny:

Step 1: LR = 0.00001 Step 2: LR = 0.00002 Step 3: LR = 0.00004 ... Eventually: LR = 0.001

Why? Early gradients are unreliable because the network is randomly initialized. Warmup prevents huge updates before the optimizer has a chance to stabilize.

Where is warmup used? Almost everywhere in modern NLP:
- GPT
- BERT
- LLaMA
- ViT

Nearly every Transformer paper uses warmup.

### Learning Rate Finder

Suppose you don't know whether 0.1 or 0.001 is better. Instead of guessing, Leslie Smith proposed: increase LR gradually and observe the loss.

Example:

LR = 0.000001 → 0.00001 → 0.0001 → 0.001 → 0.01 → 0.1

Record the loss at each step. The graph shows the loss decreasing then suddenly exploding. Choose the LR slightly before the explosion.

Why? If LR is too small, learning is slow. If LR is too large, loss explodes. The sweet spot lies just before instability.

### Practical Interview Values

CNN (ResNet):

| Component | Value |
|-----------|-------|
| Optimizer | SGD + Momentum |
| Typical LR | 0.1 |
| Scheduler | StepLR |
| Decay | 80 epochs → 120 epochs → 160 epochs |

Fine-tuning BERT / GPT:

| Component | Value |
|-----------|-------|
| Optimizer | AdamW |
| LR | 1e−5 to 3e−5 (sometimes 1e−4 for smaller models) |
| Warmup | Almost always |

### Comparison Table

| Scheduler | Idea | Best Use |
|-----------|------|----------|
| Constant | Same LR throughout | Small/simple experiments |
| StepLR | Drop LR at fixed epochs | Classic CNN training |
| Cosine Annealing | Smooth decay | Modern vision models |
| OneCycle | Increase then decrease LR | Fast convergence with SGD |
| Warmup | Start small, gradually increase | Transformers, large-batch training |
| LR Finder | Automatically estimate a good LR | Before training a new model |

### Interview Questions — Learning Rate

Q1. Why not keep the learning rate constant?

> Answer: A large constant learning rate can overshoot the minimum, while a small one slows convergence. Scheduling allows fast learning early and fine-grained optimization later.

Q2. Why do Transformers use warmup?

> Answer: At the start of training, parameters are randomly initialized and gradients can be unstable. Warmup gradually increases the learning rate, preventing excessively large updates and improving training stability.

Q3. Why does OneCycle work well?

> Answer: OneCycle first increases the learning rate to encourage exploration of the loss landscape, then decreases it for fine-tuning. This often leads to faster convergence and good generalization.

Q4. When would you use StepLR vs Cosine Annealing?

> Answer: StepLR is simple and effective for many CNNs, but it introduces abrupt learning-rate changes. Cosine Annealing provides a smooth decay, which often results in more stable optimization and slightly better performance.

### Easy Memory Trick

Think of learning to ride a bicycle:

- Constant LR: Ride at the same speed all the time.
- StepLR: Suddenly slow down at specific checkpoints.
- Cosine Annealing: Gradually slow down as you approach your destination.
- OneCycle: Speed up first to gain momentum, then slow down to stop smoothly.
- Warmup: Start slowly until you gain balance, then ride at full speed.
- LR Finder: Take a few practice rides at different speeds to discover what works best before the real journey.

---

## 2. BatchNorm vs LayerNorm

This is one of the most frequently asked deep learning interview questions, especially for AI/ML roles.

### Why Do We Need Normalization?

Suppose you're training a neural network. One batch of hidden layer outputs: 2, 150, -80, 40, 500. Another batch produces: -100, 600, 800, 20, -300. The distribution keeps changing. The next layer has to continuously adapt, making training unstable.

Normalization fixes this by making activations have roughly Mean = 0 and Variance = 1.

### BatchNorm

Suppose your batch has 4 samples, each with 3 features:

| | Feature1 | Feature2 | Feature3 |
|---|---|---|---|
| Sample1 | 2 | 8 | 1 |
| Sample2 | 4 | 10 | 3 |
| Sample3 | 6 | 12 | 5 |
| Sample4 | 8 | 14 | 7 |

Step 1: Compute Mean (for Feature 1)

$$\mu = \frac{2+4+6+8}{4} = 5$$

Step 2: Compute Variance

Suppose Variance = 5.

Step 3: Normalize

For Sample 1: $\frac{2-5}{\sqrt{5}}$

Repeat for every sample. Now Feature 1 has Mean = 0, Variance = 1.

Do the same for Feature 2 and Feature 3.

Important: BatchNorm computes statistics across the batch. The batch participates in normalization.

Why is this good? If one batch has Mean = 100 and the next has Mean = -50, BatchNorm converts both to Mean = 0. The next layer sees a stable distribution. Training becomes easier.

### The γ and β Parameters

After normalization, every feature has Mean = 0 and Variance = 1. But what if the network actually wants Mean = 20 and Variance = 5? Normalization destroyed that possibility.

So BatchNorm learns two parameters:

- γ (Gamma): Scale. Stretches or compresses the values.
- β (Beta): Shift. Moves the distribution left or right.

$$y = \gamma \hat{x} + \beta$$

The network can learn the most useful scale and offset instead of being forced to keep mean 0 and variance 1 forever.

### Training vs Inference

During training: Every mini-batch is different. BatchNorm computes mean and variance from that batch.

During testing: With only one image, how do you compute batch mean? Impossible. So BatchNorm stores running mean and running variance during training. At inference, it uses those stored values.

### Problem with Small Batch Sizes

With batch size 2, feature values 100, 105 give Mean = 102.5. Next batch 90, 200 gives Mean = 145. Very unstable. Tiny batches give noisy estimates. Training becomes unstable.

This is why BatchNorm struggles when Batch Size = 1, 2, or 4.

### LayerNorm

Instead of asking "What are the statistics across the batch?" LayerNorm asks: "Within this one sample, what are the statistics across its features?"

Suppose one sample is [2, 8, 10]. Mean = $\frac{2+8+10}{3}$. Normalize using only these three numbers. The second sample is normalized separately. The third sample is normalized separately. No interaction between samples.

### Why LayerNorm for Transformers?

Suppose you're training GPT with Batch Size = 1 or 2. BatchNorm cannot estimate stable statistics. LayerNorm doesn't care — it only looks inside one sample. So it works perfectly.

Why doesn't LayerNorm need running statistics? Because during inference, the sample itself provides the statistics. No batch required. No stored mean. No stored variance. Everything is computed on the fly.

### Comparison Table

| Model | Preferred Normalization | Why |
|-------|------------------------|-----|
| CNNs | BatchNorm | Exploits stable batch statistics and speeds up training |
| RNNs | LayerNorm | Handles sequential data better and doesn't depend on batch size |
| Transformers | LayerNorm | Works with small/variable batches and independent sequences |
| Very small batch CNNs | LayerNorm or GroupNorm | Batch statistics become unreliable |

### Interview Questions — Normalization

Why does BatchNorm fail for small batches?

> Because the batch mean and variance become noisy and unreliable when computed from only a few samples, making training unstable.

Why do Transformers use LayerNorm?

> Transformers often train with small or variable batch sizes and process sequences independently. LayerNorm normalizes each sample separately, so it works consistently without relying on batch statistics.

Does LayerNorm require running mean?

> No. It computes the mean and variance from the current sample during both training and inference.

### Easy Memory Trick

- BatchNorm: "Normalize across the batch." Think B = Batch.
- LayerNorm: "Normalize inside one layer (one sample)." Think L = Local to one sample.

One-line interview answer:

> BatchNorm computes mean and variance across the mini-batch for each feature/channel, requires running statistics for inference, and works best with reasonably large batch sizes (common in CNNs). LayerNorm computes mean and variance across the features of each individual sample, does not require running statistics, and is therefore preferred for Transformers and models trained with small or variable batch sizes.

---

## 3. Debugging a Neural Network That Isn't Training

Imagine training a model. After 10 minutes:

- Loss is not decreasing.
- Accuracy is stuck at 10%.
- Loss becomes NaN.
- Validation accuracy is random.

An interviewer may ask: "Your model isn't training. What will you check first?"

They want a systematic debugging approach, not "I'll change the optimizer."

### Tiny Overfit Test

This is the #1 sanity check and probably the most useful debugging technique.

Instead of training on 50,000 images, train on only 100 images (or even 10) for many epochs.

What should happen? A sufficiently powerful neural network should memorize those few examples:

Training loss: 2.3 → 1.4 → 0.5 → 0.05 → 0.001 Training acc: 10% → 50% → 90% → 100%

Modern neural networks have millions of parameters. 100 images is tiny — the network should easily memorize them.

If it cannot memorize 100 images... Something is wrong:

- Bug in forward pass
- Wrong loss function
- Labels incorrect
- Learning rate wrong
- Gradients not flowing
- Optimizer bug

> Interview Answer: If my model cannot overfit a tiny dataset, I first suspect an implementation bug rather than a lack of model capacity.

### Check Data Normalization

Suppose training images are normalized like $x = \frac{x-0.5}{0.5}$ but validation images are unnormalized. Training data: Mean = 0, Std = 1. Validation data: Mean = 120, Std = 50. The model learned on one distribution but is evaluated on another. Performance drops dramatically.

Always ensure: Same normalization for train and validation. Correct dataset mean and standard deviation.

### Visualize Inputs and Labels

This sounds simple, but it catches many bugs. Imagine training a cat-vs-dog classifier and seeing: Image: Dog, Label: Cat. Or images appearing completely black due to incorrect normalization. Or images rotated by mistake. Never assume your data pipeline is correct — look at a few samples.

### Check the Learning Rate

If LR = 10: Loss goes 2 → 80 → 10000 → NaN — far too large.

If LR = 1e-8: Loss goes 2.300 → 2.299 → 2.299 → 2.298 — almost no learning.

> Rule of thumb: Loss explodes immediately → learning rate likely too high. Loss barely changes → learning rate may be too low.

### Vanishing and Exploding Gradients

Vanishing Gradient: Output layer gradient = 1, Hidden layer = 0.2, Previous = 0.04, Previous = 0.008, eventually 0.000001. Early layers receive almost no learning signal. Weights hardly update. Training stalls.

- Symptoms: Loss decreases very slowly. Early layers barely change. Gradient norms are extremely small.

Exploding Gradient: 1 → 5 → 25 → 125 → 1000. Gradients become huge. Updates become enormous. Loss becomes NaN.

How to detect this? Print the gradient norm of each layer:

python for p in model.parameters(): if p.grad is not None: print(p.grad.norm())

- Healthy: Layer 1: 0.3, Layer 2: 0.5, Layer 3: 0.7
- Vanishing: Layer 1: 0.0000001, Layer 2: 0.000002, Layer 3: 0.00001
- Exploding: Layer 1: 500, Layer 2: 1000, Layer 3: 7000

### Activation Distribution

Suppose a ReLU layer outputs: 0, 0, 0, 0, 0, 0, 0 — almost every neuron is inactive. This is called dead ReLUs. The network cannot learn effectively.

Or suppose sigmoid activations are 0.99999, 0.99998, 0.99997 — they are saturated. The derivative is almost zero. Gradients vanish.

You can inspect activation statistics (mean and standard deviation) using forward hooks in PyTorch.

### Fixes for Vanishing Gradients

1. Better Initialization:
- For tanh: Use Xavier Initialization (keeps activation variance roughly constant across layers).
- For ReLU: Use He Initialization (accounts for ReLU zeroing out about half of the activations).

2. BatchNorm / LayerNorm: Stabilize activation distributions, making gradients healthier.

3. Use ReLU Instead of Sigmoid:
- Sigmoid derivative: $\sigma'(z) = \sigma(z)(1-\sigma(z))$, maximum derivative = 0.25. Repeated multiplication by numbers less than 1 shrinks gradients.
- ReLU derivative: 1 for positive inputs. Gradients propagate much more effectively.

### Fixes for Exploding Gradients

1. Gradient Clipping: If the gradient norm exceeds a threshold, scale it down before the optimizer step.
2. Reduce Learning Rate: A smaller learning rate produces smaller updates, making training more stable.

### Complete Debugging Checklist

Step 1 ✅ Can the model overfit 100 samples? If No → suspect implementation bug.

Step 2 ✅ Are inputs normalized correctly?

Step 3 ✅ Are labels correct? Visualize random samples.

Step 4 ✅ Is the learning rate reasonable?

Step 5 ✅ Check gradient norms.
- Near zero? → Vanishing gradients.
- Huge? → Exploding gradients.

Step 6 ✅ Check activation distributions.
- Too many zeros? → Dead ReLUs.
- Very large values? Saturated activations?

Step 7 Apply appropriate fixes:
- Xavier initialization (for tanh)
- He initialization (for ReLU)
- BatchNorm or LayerNorm
- ReLU/LeakyReLU instead of sigmoid in deep networks
- Gradient clipping for exploding gradients
- Reduce learning rate if updates are unstable

### Interview Answer

> Q: Your neural network isn't learning. How would you debug it?
>
> A strong answer is: I would first check whether the model can overfit a tiny dataset (e.g., 100 samples). If it cannot, I would suspect a bug in the model, optimizer, or training code. Next, I would verify the data pipeline by checking normalization and visualizing inputs and labels. Then I would inspect the learning rate and monitor gradient norms to detect vanishing or exploding gradients. Finally, I'd examine activation distributions and, if needed, use appropriate initialization (He/Xavier), normalization layers (BatchNorm/LayerNorm), ReLU-family activations, or gradient clipping to stabilize training.

---

## 4. NaNs, Dead ReLUs, BatchNorm Problems, Noisy Labels & Logging

This entire topic is "How would you debug a deep learning model like an ML engineer?" Interviewers rarely ask the theory directly. Instead they'll ask: "Your model suddenly starts giving NaN loss after 5 epochs. What will you do?" or "Training suddenly diverges after epoch 30. How will you debug it?"

### NaNs During Training

NaN means Not a Number. Once NaN appears, everything becomes NaN: Loss → Gradient → Weights → Predictions. Training is finished.

Why do NaNs happen?

1. Learning Rate Too High: Weight = 5, Gradient = 2000, LR = 1 → Update = 5 - 1×2000 = -1995. Next layer gets huge activations → huge gradients → overflow → NaN.

2. Division by Zero: If $\sigma = 0$, then $\frac{x}{0}$ is undefined → NaN. That's why BatchNorm uses $\sqrt{\sigma^2 + \epsilon}$ instead of $\sqrt{\sigma^2}$. The tiny $\epsilon$ ensures the denominator is never exactly zero.

3. log(0): Cross entropy contains $-\log(p)$. If $p = 0$, then $\log(0) = -\infty$, loss becomes infinite, eventually NaN. Stable implementations avoid ever computing an exact zero probability.

4. Mixed Precision Overflow: float16 has a much smaller numeric range than float32. Large values overflow faster. e.g., 500,000 may not fit in float16, leading to inf → NaN.

How to Debug NaNs?

1. Print the loss: print(loss). If NaN, you know exactly when it started.
2. Check parameters: torch.isnan(param). If weights already contain NaN, the optimizer has corrupted them.
3. Disable mixed precision. If NaNs disappear, the issue is numerical overflow.
4. Reduce learning rate (e.g., 0.001 → 0.0001). Many NaN problems disappear immediately.

How to Fix NaNs?

- Add epsilon: Instead of $\frac{1}{\sigma}$, use $\frac{1}{\sigma + \epsilon}$.
- Stable Softmax: Use the log-sum-exp trick by subtracting the maximum logit before exponentiation. This keeps exponentials in a safe numeric range.
- Gradient Clipping: If gradients become huge, clip them before updating.

### Dead ReLU

ReLU: $ReLU(x) = \max(0, x)$. Derivative: positive input = 1, negative input = 0.

Suppose a neuron always receives -5, -7, -3, -9. Output: 0, 0, 0, 0. Derivative: 0. Gradient: 0. Weight update: 0. The neuron is effectively "dead" and never learns again.

How to detect it? Plot activation histograms. A healthy layer has a mix of positive values, negative values, and zeros. A dead ReLU shows nearly everything as zero.

Fixes:

1. Leaky ReLU: Instead of $\max(0,x)$, use $\max(0.01x, x)$. Negative inputs still have a small slope, so gradients can flow.
2. Better Initialization: He initialization keeps ReLU activations in a healthy range.
3. Smaller Learning Rate: A huge update can push a neuron permanently into the negative region. Reducing the LR helps avoid this.

### BatchNorm Problems

BatchNorm computes mean and variance from the batch. With Batch Size = 1, the mean is just that one sample. Variance is almost meaningless. Normalization becomes unstable.

Solution: Use LayerNorm or GroupNorm instead. They don't depend on batch statistics.

`model.train()` vs `model.eval()`: This is an extremely common interview question.

- During training (model.train()), BatchNorm uses current batch statistics.
- During testing (model.eval()), BatchNorm uses running mean and running variance collected during training.
- If you forget model.eval(), BatchNorm will keep using the current batch statistics, making inference unstable.

### Noisy Labels & Robust Training

Suppose an image of a cat is labeled "Dog." The network tries to learn incorrect information. Training becomes confusing.

Symptoms: Training loss stays high for a few specific samples. Validation accuracy saturates early. Performance is noisy.

Solution 1: Label Smoothing — Instead of correct class = 1, others = 0, use 0.9, 0.05, 0.05. This discourages the model from becoming overconfident and improves robustness.

Solution 2: MixUp — Take Image A and Image B. Blend them. Also blend the labels. The model learns smoother decision boundaries and is less sensitive to mislabeled examples.

Solution 3: Inspect High-Loss Samples — If one image always has Loss = 15 while others have 0.3, look at it manually. Maybe the label is wrong.

Additional strategies:
- Co-teaching: Train two networks; each selects small-loss examples to teach the other.
- Bootstrapping / Generalized Cross-Entropy / Symmetric Cross-Entropy
- Clean Label Detection: Find samples with high training loss and manually inspect.
- Curriculum Learning: Start with easy examples.

> Practical advice: First inspect top-k high-loss training samples. If many are mislabeled, consider relabeling or downweighting.

### Training Suddenly Diverges

Suppose training is perfect: Epoch 1 → Loss = 2, Epoch 20 → Loss = 0.4, Epoch 35 → Loss = 7000. Something changed.

Possible reasons:

- Learning-rate schedule: Maybe the scheduler accidentally increased the LR instead of decreasing it.
- Corrupted batch: One batch contains NaNs or incorrect images.
- Gradient explosion: Gradients suddenly become enormous.
- Broken checkpoint: Weights restored incorrectly.

Debugging:

- Print per-batch loss instead of only per-epoch loss. Now you can identify the exact batch where things break.
- Check the learning rate at the same point. Many times the scheduler is the culprit.

### Logging & Observability

Professional ML engineers log everything — not just loss.

Minimum Logs:

| Metric | Purpose |
|--------|---------|
| Learning Rate | Track schedule |
| Training Loss | Monitor convergence |
| Validation Loss | Detect overfitting |
| Training Accuracy | Training progress |
| Validation Accuracy | Generalization |
| Gradient Norm | Detect vanishing/exploding gradients |
| Weight Norm | Detect uncontrolled weight growth |
| Activation Mean / Std | Identify dead activations or saturation |
| Top-k Highest Loss Samples | Find mislabeled or difficult examples |

Save Checkpoints:

- Latest checkpoint — to resume from the last state.
- Best validation checkpoint — because the best model often occurs before the final epoch.

### Complete Interview Debugging Flow

Model behaving badly │ ▼ Can it overfit 100 samples? │ No ─────► Bug in code/model Yes │ ▼ Check data pipeline (Normalization, labels) │ ▼ Check learning rate │ ▼ Check gradient norms │ ├── Near zero → Vanishing gradients └── Huge → Exploding gradients │ ▼ Check activations │ ├── Mostly zeros → Dead ReLUs └── Saturated sigmoid/tanh │ ▼ Check BatchNorm mode (train vs eval) │ ▼ Check for NaNs (loss, weights, gradients) │ ▼ Inspect hardest samples (highest training loss) │ ▼ Log everything and save checkpoints

### Interview-Ready Summary

> If an interviewer asks "How do you debug a neural network that isn't training properly?", a strong answer is:
>
> I start by verifying that the model can overfit a tiny dataset. If it can't, I suspect an implementation bug. Next, I validate the data pipeline by checking normalization and visualizing inputs and labels. I inspect the learning rate, gradient norms, and activation statistics to diagnose vanishing or exploding gradients or dead ReLUs. If I encounter NaNs, I check for numerical instability, reduce the learning rate, add numerical safeguards like epsilon, use stable implementations (e.g., log-sum-exp), and apply gradient clipping if needed. I also ensure BatchNorm is used correctly (train() vs eval()), inspect high-loss samples for label noise, and continuously log metrics such as learning rate, losses, accuracies, gradient norms, and checkpoints so issues can be traced efficiently.

---

## 5. Scaled Dot-Product Attention

This is probably the single most important concept in Transformers. If you're interviewing for an AI/ML internship, there's a very high chance you'll be asked about self-attention.

### What Problem Is Attention Solving?

Consider: "The cat sat on the mat because it was tired." Who is "it"? The cat or the mat? Attention lets every word decide which other words are important for understanding it.

### Every Word Creates Three Vectors (Q, K, V)

For every word we create:

- Query (Q): "What information am I looking for?"
- Key (K): "What information do I contain?"
- Value (V): "What information should I give if someone selects me?"

Think of a library. Your query is "AI." Every book has a key. Book 1: "AI," Book 2: "Cooking," Book 3: "History." Compare query with keys. Highest match: Book 1. Then you read its value. That's attention.

$$Q = XW_Q, \quad K = XW_K, \quad V = XW_V$$

### Dot Product

Query of "Cat" = [2, 3]. Keys: Dog = [1, 1], Cat = [2, 4], Mat = [5, 1].

- Dog: $2(1) + 3(1) = 5$
- Cat: $2(2) + 3(4) = 16$
- Mat: $2(5) + 3(1) = 13$

Higher score = more relevant.

### Matrix Form (QKᵀ)

Instead of computing one by one, put all queries into a matrix. With 3 words, each vector has dimension 2:

$$Q = \begin{bmatrix} 1 & 2 \\ 2 & 3 \\ 3 & 1 \end{bmatrix}, \quad K = \begin{bmatrix} 2 & 1 \\ 1 & 3 \\ 4 & 2 \end{bmatrix}$$

Compute $QK^T$ (3×3). Every cell = similarity between two words. Query of word 1 compared with Key of word 2.

### Softmax

Scores [5, 16, 13] → Softmax → [0.0001, 0.95, 0.0499]. Now they sum to 1. 95% attention goes to Word 2.

### Multiply with V

Values: Dog → [1, 0], Cat → [2, 3], Mat → [5, 1].
Attention: [0.0, 0.95, 0.05].
Output: $0(1,0) + 0.95(2,3) + 0.05(5,1) = (2.15, 2.9)$

The output is simply a weighted average of the value vectors. Words receiving more attention contribute more.

Matrix version: $A = \text{softmax}(QK^T)$, then $O = AV$.

### Entire Pipeline

Input Embeddings │ ▼ Generate Q, K, V │ ▼ QKᵀ (similarity) │ ▼ Scale (÷√dₖ) │ ▼ Softmax (attention) │ ▼ Multiply by V │ ▼ Output

### Why Divide by √dₖ?

This is one of the most common interview questions.

With dimension = 2: q = [1, 2], k = [3, 4]. Dot product = 11. Reasonable.

With dimension = 512 and each element ≈ 1: Dot product ≈ 512. Huge.

Softmax sees [500, 510, 520] instead of [5, 6, 7]. It becomes approximately [0, 0, 1] — almost one-hot. Changing 520 to 521 barely changes the output. Gradients become tiny. Learning slows or becomes unstable.

The fix: Divide by $\sqrt{d_k}$. If $d_k = 512$, $\sqrt{512} \approx 22.6$. Instead of 520, we get ~23. Softmax becomes much smoother (e.g., [0.20, 0.35, 0.45]). Gradients flow well.

Why specifically $\sqrt{d_k}$? If elements of q and k are random with mean 0 and variance 1:
- Each product $q_i k_i$ has variance about 1.
- Adding $d_k$ such independent terms gives the dot product a variance of about $d_k$.
- So the standard deviation grows like $\sqrt{d_k}$.
- Dividing by $\sqrt{d_k}$ keeps the variance of the scores roughly constant (around 1), regardless of the vector dimension.

### Complete Formula

$$O = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

Compute similarities between every query and every key, scale them to keep them numerically stable, convert them into attention weights with softmax, and use those weights to compute a weighted average of the value vectors.

### Interview Questions — Attention

Why do we need Q, K, and V?

- Query (Q): What information is this word looking for?
- Key (K): What information does each word offer?
- Value (V): The actual information that will be combined to produce the output.

Why use $QK^T$? Because it efficiently computes the similarity between every query and every key in a single matrix multiplication.

Why multiply by $V$? The attention weights tell us how much to use each value vector. Multiplying by $V$ forms a weighted combination of the information from all words.

Why divide by $\sqrt{d_k}$? As the key/query dimension increases, dot products become larger in magnitude. Large scores make the softmax almost one-hot, causing poor gradients. Dividing by $\sqrt{d_k}$ keeps the score distribution well-scaled and training stable.

Short explanation: Larger vector dimensions produce larger dot products, which make softmax overly confident (very peaky). Scaling by $\sqrt{d_k}$ keeps scores in a reasonable range, leading to stable gradients and better training.

### Easy Memory Trick

Think of searching videos on YouTube:

- Query: The search you type ("machine learning").
- Keys: The titles/topics of every video.
- Dot Product: Measures how well each video matches your search.
- Softmax: Converts match scores into probabilities.
- Values: The actual content of each video.
- Output: A weighted combination that emphasizes the most relevant videos.

That's exactly what self-attention does — except the "videos" are the words in the sequence.

---

## 6. Multi-Head Attention

### What's Wrong With a Single Head?

Consider: "The animal didn't cross the street because it was too tired." The word "it" could attend to: animal (to understand who "it" is), cross (to understand the action), or street (to understand the location). A single attention head may focus mostly on one relationship. Wouldn't it be better if different heads learned different relationships?

### Multi-Head Attention

Instead of computing attention once, compute it h times. Each head learns something different:

- Head 1 → Grammar
- Head 2 → Subject/Object
- Head 3 → Long-distance dependency
- Head 4 → Position

### Create Multiple Q, K, V

Each head gets its own projection matrix:

$$Q_1 = XW_Q^{(1)}, \quad Q_2 = XW_Q^{(2)}, \quad Q_3 = XW_Q^{(3)}$$

Same for K and V. Each head has different weights, so each learns different things.

Why different matrices? Imagine three teachers reading the same paragraph. Teacher 1 looks for grammar. Teacher 2 looks for meaning. Teacher 3 looks for important keywords. Same paragraph, different focus.

### Why Divide the Dimensions?

Suppose $d_{model} = 512$, number of heads $h = 8$. Then each head gets $d_k = \frac{512}{8} = 64$. Instead of one huge 512-dimensional attention, we have 8 small attentions of size 64.

Each head computes $Q_iK_i^T$, softmax, multiply with V — exactly the same as single-head attention. Nothing changes except the inputs are different.

### Concatenate and Final Linear

Eight heads each output (10 words × 64 features). Concatenate them: 10 × (8×64) = 10 × 512. We're back to the original feature size.

Then multiply by one more matrix: $O_{final} = O_{cat}W_O$.

Why? Features from different heads are just placed next to each other. The final linear layer mixes information from all heads so the model can combine what each head learned into one coherent representation.

### Complete Flow

Input (10 × 512) │ ▼ Generate Q, K, V │ ▼ Split into 8 heads │ ▼ Head 1 Attention Head 2 Attention ... Head 8 Attention │ │ │ └────────────────────┼───────────────────────┘ │ ▼ Concatenate Outputs (10 × 512) │ ▼ Linear Layer (W_O) │ ▼ Final Output

### Why Not Just One Big Head?

A single head has to learn grammar, position, subject-object relation, coreference, tense — all at once. With multiple heads, different heads specialize:

- Head 1: Learns subject–verb relationships.
- Head 2: Learns positional information.
- Head 3: Learns pronoun resolution ("it", "he", "she").
- Head 4: Learns long-range dependencies.

### Interview Answer

> Q: Why do we use Multi-Head Attention instead of a single attention head?
>
> Multi-head attention allows the model to learn different types of relationships simultaneously. Each head has its own query, key, and value projection matrices, so it attends to the input from a different learned feature subspace. The outputs of all heads are concatenated and passed through a final linear layer to combine these complementary representations into a single output.

### Easy Memory Trick

Think of watching a football match:

- One camera focuses on the ball.
- One camera follows the goalkeeper.
- One camera gives a wide tactical view.
- One camera zooms in on the coach.

All cameras observe the same match, but each captures a different aspect. Later, the broadcast combines all those views into one complete picture. Multi-head attention works the same way.

---

## 7. Complexity Analysis — O(n²)

### Why Quadratic?

Remember the attention matrix $QK^T$. With 5 words, each word compares itself with ALL words: 5×5 = 25 comparisons.

- 100 words: 100×100 = 10,000 comparisons.
- 1000 words: 1,000,000 comparisons.
- 65,000 words: 65,000² ≈ 4.2 billion attention scores.

This is why Transformers struggle with very long sequences.

### Why Is Computing QKᵀ O(n²dₖ)?

With 100 words and each vector having 64 features, one dot product needs 64 multiplications. 100 × 100 = 10,000 comparisons. Total: 10,000 × 64 operations. Complexity: $O(n^2 d_k)$.

### Softmax Complexity

Each row has n numbers. There are n rows. Total work: $O(n^2)$. Compared to $O(n^2 d_k)$, this is usually smaller.

### Multiplying by V

Attention matrix (n×n) × Values (n×d_v). Matrix multiplication costs $O(n^2 d_v)$.

### Total Cost

Compute scores: $O(n^2 d_k)$. Softmax: $O(n^2)$. Multiply by V: $O(n^2 d_v)$. Since usually $d_k = d_v = d_{model}$, overall: $O(n^2 d_{model})$.

### What About Multiple Heads?

With $d_{model} = 512$ and 8 heads, each head gets 64 dimensions. Each head costs $O(n^2 \times 64)$. Eight heads = $8 \times O(n^2 \times 64) = O(n^2 \times 512)$. The total complexity stays $O(n^2 d_{model})$. Using more heads doesn't change the asymptotic complexity.

### Memory Problem

This is actually the biggest issue. The attention matrix is $n \times n$.

- $n = 1000$: 1 million values.
- $n = 10000$: 100 million values.
- $n = 65000$: 4.2 billion values.

Just storing this matrix can exceed GPU memory. Attention is memory-bound.

### Practical Mitigations

Instead of comparing with every word, compare with fewer words.

| Method | Idea |
|--------|------|
| Local Attention | Every word attends to nearby words only (like reading previous and next few sentences) |
| Sparse Attention | Only keep important connections (e.g., BigBird uses local, random, and global patterns) |
| Linformer | Projects keys and values into lower-dimensional representation before attention |
| Performer | Approximates softmax attention using random feature mappings |
| Reformer | Uses Locality Sensitive Hashing (LSH) — only compare words likely to be similar |
| Chunking | Split long document into smaller pieces, each performing attention independently |

### Interview Questions — Complexity

Why is self-attention $O(n^2)$?

> Because every query compares with every key, resulting in $n \times n$ pairwise comparisons.

What is the biggest bottleneck?

> The attention matrix of size $n \times n$, which requires quadratic memory.

Why do Transformers struggle with long documents?

> Because both computation and memory grow quadratically with sequence length. Doubling the sequence length roughly quadruples the attention work.

How can we reduce this?

> Local/sliding-window attention, sparse attention (e.g., BigBird), low-rank projections (e.g., Linformer), approximate attention (e.g., Performer), hashing-based attention (e.g., Reformer), or chunking/hierarchical processing.

One-line interview answer:

> Self-attention has $O(n^2)$ time and memory complexity because every token attends to every other token, producing an $n \times n$ attention matrix. This quadratic growth becomes expensive for long sequences, so practical long-context Transformers use sparse, local, compressed, or approximate attention mechanisms to reduce the cost.

---

## 8. Residuals & LayerNorm

### Residual Connection

Instead of only keeping the attention output, we keep the original input plus the attention output:

$$\text{Output} = x + \text{Attention}(x)$$

Why add the input? Suppose the original feature is "Dog" and attention slightly improves it. Instead of forgetting the original, we combine: Original Knowledge + New Knowledge. This makes learning much easier.

Why are residuals important? Without residuals, deep networks often suffer from vanishing gradients, information loss, and hard optimization. Residuals give gradients a direct path back through the network, making very deep models much easier to train.

### Layer Normalization

Suppose one token has features [2, 4, 6].

1. Mean: $\mu = \frac{2+4+6}{3} = 4$
2. Subtract mean: [-2, 0, 2]
3. Variance: $\sigma^2 = \frac{(-2)^2+0^2+2^2}{3} = \frac{8}{3}$
4. Std: $\sigma = \sqrt{\frac{8}{3}}$
5. Divide: $\frac{x-\mu}{\sigma}$ → [-1.22, 0, 1.22]

Now every token has Mean = 0 and Variance = 1. This stabilizes training.

Why normalize? If one layer outputs [1000, 1200, 900] and another outputs [0.1, 0.2, 0.15], huge differences make optimization difficult. LayerNorm brings everything to a similar scale.

### The γ and β Parameters

After normalization, every feature has Mean = 0 and Variance = 1. But what if the model actually wants [5, 10, 15] or [2, 2, 2]?

- γ (Gamma): Scales the normalized values. If γ = 2, then [-1, 0, 1] → [-2, 0, 2].
- β (Beta): Shifts the values. If β = 3, then [-2, 0, 2] → [1, 3, 5].

The network can learn the most useful scale and offset instead of being forced to always have zero mean and unit variance.

### Transformer Block (Post-Norm)

After attention: $x + \text{Attention}(x)$, then LayerNorm:

$$Z_1 = \text{LayerNorm}(x + \text{Attention}(x))$$

Then the feed-forward network, again residual then LayerNorm:

$$Z_2 = \text{LayerNorm}(Z_1 + \text{FFN}(Z_1))$$

Every sublayer follows: Sublayer → Add original input → LayerNorm.

### Pre-Norm vs Post-Norm

Post-Norm (Original Transformer):

Input → Attention → Add Residual → LayerNorm

Formula: $\text{LayerNorm}(x + \text{Attention}(x))$

Pre-Norm (Modern Transformers):

Input → LayerNorm → Attention → Add Residual

Formula: $x + \text{Attention}(\text{LayerNorm}(x))$

### Why Is Pre-Norm Better?

Think about the gradient. With residuals, the gradient has a shortcut.

- Post-Norm: Gradient → LayerNorm → Residual → Attention. The gradient must pass through LayerNorm before reaching earlier layers. LayerNorm performs several operations (mean, variance, division, scaling), slightly modifying the gradient at every layer. With hundreds of layers, these modifications accumulate. Training becomes harder.

- Pre-Norm: Gradient → Residual → Input. The derivative of the identity path is 1. Gradients can flow almost unchanged through the residual connection. That's why very deep Transformers (50–100+ layers) are much easier to train.

Intuition: Post-Norm is like carrying water through pipes where every pipe has a filter, each slightly changing the water. Pre-Norm puts the filter on a side branch while the main pipe stays open — water can always flow through the main pipe without being blocked.

### Quick Comparison

| Post-Norm | Pre-Norm |
|-----------|----------|
| Attention → Add → LayerNorm | LayerNorm → Attention → Add |
| Original Transformer | Modern Transformers |
| Can become unstable in very deep networks | More stable for deep networks |
| Less common today | Preferred today |

### Interview Answers

Why do we use residual connections? Residual connections add the original input to the sublayer output, preserving information and providing a direct path for gradients. This makes deep networks much easier to optimize.

Why do we use LayerNorm? LayerNorm normalizes the features of each token to have zero mean and unit variance, stabilizing activations and making optimization easier. The learnable parameters γ and β allow the model to restore the most useful scale and shift.

Why do modern Transformers prefer Pre-Norm? Pre-Norm normalizes the input before each sublayer, leaving the residual connection as a nearly direct path. This improves gradient flow and makes very deep Transformer models significantly more stable to train.

What's the difference between Pre-Norm and Post-Norm?
- Post-Norm: $\text{LN}(x + \text{Sublayer}(x))$ — sublayer processes raw input, residual added, then LN applied.
- Pre-Norm: $x + \text{Sublayer}(\text{LN}(x))$ — input normalized first, then sublayer, then residual added.
- Pre-Norm is preferred in modern deep Transformers because the residual connection provides a nearly identity path for gradients.

---

## 9. Positional Encodings

### Why Do Transformers Need Positional Encoding?

Consider "Dog bites man" vs "Man bites dog." The words are exactly the same, only the order changed, but the meaning completely changed.

Self-attention only sees word embeddings. It doesn't know which word came first. Without extra information, Transformers treat the sentence almost like a bag of words.

Solution: For every position, create a Positional Encoding (PE) vector and add it to the word embedding:

Dog embedding + Position 1 encoding Bites embedding + Position 2 encoding Man embedding + Position 3 encoding

Now the Transformer knows both what the word is and where it is.

### Original Sinusoidal Positional Encoding

Even dimensions:

$$PE(pos, 2i) = \sin\left(\frac{pos}{10000^{2i/d_{model}}}\right)$$

Odd dimensions:

$$PE(pos, 2i+1) = \cos\left(\frac{pos}{10000^{2i/d_{model}}}\right)$$

Every position gets a unique pattern by combining sine and cosine waves at different frequencies. Some dimensions capture short-distance positions, others capture long-distance positions.

### Why Sine and Cosine?

Imagine two waves — one changes slowly, one changes quickly. The Transformer combines many such waves. Each dimension has a different frequency. Together, they uniquely identify every position.

Why different frequencies? If every dimension used the same sine wave, Position 10 and Position 100 might look similar. Different frequencies avoid this.

### Learned Absolute Positional Embeddings

Instead of a formula, we can simply store a learned vector for each position (like word embeddings). Works well, but if training only had 512 positions, what happens for Position 700? No embedding exists. The model cannot naturally handle unseen positions.

Sinusoidal encoding works for Position 1, Position 100, Position 100,000 — it's just a mathematical function. It can extrapolate to longer sequences more naturally.

### Relative Position Encoding

Instead of asking "Where is this word?" we ask "How far away is this word?" For "I love machine learning," the model doesn't care that "love" is at absolute position 2 — it cares that "love" is one word before "machine." This often generalizes better. Models like T5 use this.

### RoPE (Rotary Position Embedding)

One of the most popular methods today. Instead of adding a positional vector, RoPE rotates the Query and Key vectors by an angle that depends on the token position. Instead of saying "word + position," RoPE changes the representation itself according to its position. It naturally preserves relative positional information and usually works better for long contexts. That's why many modern LLMs (like LLaMA) use RoPE.

### Comparison Table

| Method | Idea | Advantage | Disadvantage |
|--------|------|-----------|--------------|
| Sinusoidal | Fixed sine/cosine formula | Can generalize to longer positions | Less flexible |
| Learned Absolute | Learn one embedding per position | Often performs well on trained lengths | Doesn't naturally extrapolate |
| Relative Position | Encode distance between tokens | Better captures relationships | Slightly more complex |
| RoPE | Rotate Q and K based on position | Excellent long-context, preserves relative positions | More mathematically involved |

### Interview Questions — Positional

Why do Transformers need positional encoding? Self-attention has no inherent notion of token order. Positional encoding injects information about the position of each token so the model can distinguish sequences like "dog bites man" and "man bites dog."

Why did the original Transformer use sine and cosine? They provide unique, deterministic position vectors using a fixed mathematical function, allowing the model to generate encodings for positions it never saw during training.

Why is RoPE popular? RoPE encodes position by rotating the query and key vectors rather than adding embeddings. It naturally captures relative positions and generally extrapolates better to long contexts, which is why many modern large language models use it.

> Easy memory trick: Imagine reading a book. Word embedding tells you what the word means. Positional encoding tells you where the word appears. Without positional encoding, the Transformer knows what every word is, but not the order in which the words appear.

---

## 10. Components to Implement (Transformer Architecture)

### Overall Transformer Block

Input Embeddings │ ▼ Multi-Head Attention │ ▼ Residual + LayerNorm │ ▼ Feed Forward Network │ ▼ Residual + LayerNorm │ ▼ Output

### Scaled Dot-Product Attention Function

Inputs: Q, K, V, mask (optional). Shapes typically (batch, seq, d_k) or (batch, n_heads, seq, d_k).

Steps:

1. Compute scores = (Q @ K.transpose(-2, -1)) / sqrt(d_k)
2. If mask present, set masked positions to -inf
3. weights = softmax(scores, dim=-1)
4. output = weights @ V

Use stable softmax (subtract max along last dimension).

### Causal / Attention Mask

For autoregressive LM:

python causal_mask = torch.triu(torch.ones(seq, seq), diagonal=1).bool()

In practice, create mask with -inf for masked entries and apply before softmax:

python scores.masked_fill(mask, -1e9) # or -torch.inf

### Multi-Head Wrapper

1. Linear projections W_q, W_k, W_v (single big linear then reshape to heads)
2. Compute per-head attention
3. Concatenate
4. Final linear

### Feed-Forward Network

Two linear layers with activation (GeLU recommended):

$$FFN(x) = W_2(\text{GELU}(W_1 x + b_1)) + b_2$$

Usually intermediate dim = 4 × d_model.

### Residual + LayerNorm (Pre-Norm)

For each sublayer:

$$x = x + \text{Sublayer}(\text{LN}(x))$$

Implement LayerNorm with a small epsilon.

### Output Projection (LM Head)

If training token-level predictions: linear from d_model → vocab_size (optionally tie weights with embedding).

### Masking Details

Padding mask: For sequences with padding, create mask to prevent attention to padding positions across keys. Mask shape broadcasts to (batch, 1, 1, seq) or (batch, n_heads, seq_q, seq_k).

Causal mask: Combine padding and causal masks:

python final_mask = padding_mask OR causal_mask

### Stable Softmax

Instead of $\text{softmax}(x)$, compute $\text{softmax}(x - \max(x))$.

Example: Without stable softmax, values [1000, 1001, 1002] cause exp(1002) to overflow. Subtract the maximum: [-2, -1, 0]. Now exp(0) = 1, exp(-1), exp(-2). No overflow. Same answer.

### Interview-Level Understanding

You do not need to memorize exact PyTorch code for every step, but you should be able to explain:

- Why we compute Q, K, and V using linear projections.
- Why we compute QKᵀ / √dₖ.
- Why we apply softmax.
- Why we multiply by V.
- The difference between causal masks (hide future tokens) and padding masks (ignore PAD tokens).
- Why we use multiple heads instead of one.
- Why every attention block is followed by a Feed Forward Network.
- Why residual connections and LayerNorm are essential for stable training.

---

## 11. Causal Mask vs Padding Mask & Other Fundamentals

### Causal Mask vs Padding Mask

Although both are called masks, they solve completely different problems.

A) Causal Mask (Hide Future Tokens)

Used only in autoregressive models where the model predicts the next token (GPT, LLaMA, Gemini decoder, ChatGPT).

For sentence "I love AI," when predicting "love," the model should only know "I" — not "AI." Otherwise it would simply copy the answer.

Attention matrix:

I love AI I ✓ ✗ ✗ love ✓ ✓ ✗ AI ✓ ✓ ✓

Token 2 cannot look at Token 3. Future information is hidden. During inference, the future doesn't exist yet.

B) Padding Mask

When batching sequences of different lengths, shorter sentences are padded with PAD tokens. The model should NOT attend to PAD tokens — they are meaningless.

Used in almost every Transformer: BERT, GPT, T5, ViT — any time padding exists.

| Causal Mask | Padding Mask |
|-------------|--------------|
| Hides future words | Hides PAD tokens |
| Used for next-token prediction | Used whenever sequences have different lengths |
| Prevents cheating | Prevents attending to meaningless padding |
| Depends on token position | Depends on whether token is PAD |

### Why Is There a Feed-Forward Network After Attention?

Attention only mixes information between tokens. It doesn't do much computation on each token itself.

Attention: Collects information — like students discussing answers.

Feed Forward: Processes the collected information — like each student thinking individually after the discussion.

Without FFN, the model would only pass information around. It wouldn't learn complex transformations.

> Interview Answer: Self-attention mixes information across different tokens, while the feed-forward network processes each token independently to learn richer nonlinear representations. Together they provide both contextual understanding and feature transformation.

### Why Residual Connections?

With 100 layers, every layer changes the input. Eventually, the original information may disappear. Gradients also have to travel through 100 layers and may become very small.

Instead of Output = Attention(x), we do Output = x + Attention(x). If attention learns nothing useful, the original information is still preserved. During backpropagation, gradients have a shortcut — they can flow directly through the identity connection.

> Interview Answer: Residual connections preserve the original information and provide a direct path for gradients, preventing vanishing gradients and enabling very deep Transformer models to train effectively.

### Why LayerNorm?

If one layer outputs [100, 200, 300] and another outputs [0.1, 0.2, 0.3], very different scales make learning difficult. LayerNorm normalizes each token's features to have zero mean and unit variance. Unlike BatchNorm, it works per token, so it doesn't depend on batch size — ideal for NLP and Transformers.

> Interview Answer: LayerNorm normalizes each token's feature vector to have zero mean and unit variance, stabilizing activations, improving gradient flow, and making optimization more reliable, especially with varying batch sizes.

### Complete Transformer Block (Modern Pre-Norm)

Input │ ▼ LayerNorm │ ▼ Multi-Head Attention │ ▼ Residual Add │ ▼ LayerNorm │ ▼ Feed Forward Network │ ▼ Residual Add │ ▼ Output

### One-Line Summary

- Causal Mask → hides future tokens (used in GPT-style next-token prediction).
- Padding Mask → hides PAD tokens (used whenever sequences are padded).
- Attention → lets tokens gather information from other tokens.
- Feed Forward Network → lets each token process and transform its gathered information independently.
- Residual Connection → preserves information and provides an easy path for gradients.
- LayerNorm → keeps activations well-scaled, leading to stable and faster training.

---

## 12. Dataset & Training Recipe

### Dataset

A language model learns one task: Predict the next token.

For "I love AI":
- Input: "I" → Target: "love"
- Input: "I love" → Target: "AI"

Character-level dataset: Split into characters. Vocabulary: A-Z, a-z, 0-9, space, punctuation (~80 characters). Very small, easy to train. Example: "Hello" → Input: H e l l, Target: e l l o.

Word/Subword dataset: Tokenizer produces [I], [love], [machine], [learning]. Vocabulary: 5k ~ 50k. Much larger, closer to real LLMs.

### Fixed Sequence Length

Every training example contains a fixed number of tokens (e.g., 64). Input = tokens[:, :n], Target = tokens[:, 1:n+1] — shifted by one. That's exactly how GPT is trained.

### Optimizer

AdamW (decoupled weight decay):
- Fast convergence
- Handles adaptive learning rates
- Better weight decay than Adam
- Learning rate ~1e-4 for small model

### Warmup

Don't immediately start with 0.0001. Gradually increase: Step 1: 0.000001 → 0.00001 → 0.00005 → 0.0001. Large learning rates at the beginning make training unstable because the weights are random.

### Batch Size

Instead of one sentence, train on many simultaneously. Example: Batch size = 32 means 32 sequences go through the model together. Typical range: 16–128 depending on GPU.

### Loss

CrossEntropyLoss — language modeling is a classification problem. With a vocabulary of 5000 words, the model predicts one of 5000 classes. Use ignore_index=PAD so loss ignores padded positions.

### Gradient Clipping

Sometimes gradients become 5000, 10000, 50000. Very large updates cause training to explode. Clip them: max norm = 1.0. If gradient norm is 5, scale it down to 1.

### Learning Rate Schedule

Instead of constant LR, change it over time. Linear warmup then cosine decay (or simple constant for tiny runs).

### Epochs

- Tiny dataset: 10–50 epochs
- Large dataset: often 1–5 epochs

### Sampling

Greedy: Always choose the token with highest probability. Simple but often repetitive.

Temperature: Before softmax, divide logits. Temperature 0.7 = sharper, more confident. Temperature 2 = flatter, more random.

Top-k Sampling: Keep only the k tokens with highest probability, then sample from them. e.g., k=2, keep Dog and Cat, ignore Car and Tree.

Top-p Sampling (Nucleus Sampling): Keep enough tokens whose cumulative probability reaches p. If p=0.8, keep Dog (0.50) + Cat (0.30). If p=0.95, also keep Car (0.15). Adapts dynamically.

### Training Curves

Plot loss vs steps/epochs (train and validation). Loss should decrease. If not, bug or poor hyperparameters.

### Validation

If both training loss and validation loss decrease → good. If training loss decreases but validation loss increases → overfitting.

### Hyperparameter Table

| Hyperparameter | Example |
|---------------|---------|
| d_model | 256 |
| n_heads | 4 |
| n_layers | 4 |
| d_ff | 1024 |
| seq_len | 64 |
| batch_size | 32 |
| lr | 1e-4 |
| weight_decay | 0.01 |

### Final Conclusion

When finishing training, summarize:
- Did the loss decrease?
- Did the generated text improve?
- Which sampling method (greedy, top-k, top-p) produced better outputs?
- Did you face issues like exploding gradients or overfitting?
- What hyperparameters worked best?

> For AI/ML intern interviews: You probably won't implement an entire GPT from scratch during an interview. But be ready for conceptual questions like: Why are inputs and targets shifted by one token? Why CrossEntropyLoss for language modeling? Why AdamW instead of Adam? What is gradient clipping? What are temperature, top-k, and top-p sampling? Why use learning-rate warmup?

### Shift By One

Q: Why shift by 1, not by 2 or 3?

> Because the model's job is to predict the immediate next token. For "I love AI": after "I", the correct next word is "love", not "AI". If we shifted by 2, the model would skip "love" and learn the wrong task.

---

## 13. Tokenization Essentials

### BPE (Byte Pair Encoding)

Idea: Start with characters. Iteratively merge the most frequent pair of symbols to build a subword vocabulary.

Example: Dataset contains "low", "lower", "lowest".
- Initially: l o w, l o w e r, l o w e s t
- "l + o" is frequent → merge: lo w
- "lo + w" is frequent → merge: low
- Eventually learns common subwords like "low", "ing", "tion", "pre"

Pros: Smaller vocabulary than word-level. Can handle unknown words by splitting into known subwords. Used in GPT and RoBERTa.

### WordPiece

Very similar to BPE. The difference is how merges are chosen:

- BPE: merges the most frequent pair.
- WordPiece: merges the pair that best improves the language model likelihood.

Used in BERT, DistilBERT, ALBERT.

> Interview answer: WordPiece is similar to BPE but chooses merges based on likelihood instead of frequency.

### SentencePiece

Unlike BPE, it doesn't require splitting on spaces first. It treats the entire sentence as raw text and learns subwords directly. This makes it work well for languages like Chinese, Japanese, and Thai where spaces may not exist.

Used in T5, LLaMA, mT5.

### Vocabulary Size Tradeoff

| Small Vocabulary (8k) | Large Vocabulary (100k) |
|-----------------------|-------------------------|
| ✅ Smaller embedding matrix | ✅ Shorter sequences |
| ✅ Less memory | ✅ Faster attention (fewer tokens) |
| ❌ Longer sequences | ❌ Larger embedding matrix |
| ❌ More computation in attention | ❌ More parameters |

- Smaller vocab → more tokens per sentence, longer sequences, more attention computation.
- Larger vocab → fewer tokens per sentence, shorter sequences, but more parameters in embedding and LM head.

### Quick Comparison

| Tokenizer | How It Works | Used In |
|-----------|-------------|---------|
| BPE | Merge most frequent character/subword pairs | GPT, RoBERTa |
| WordPiece | Merge pairs that maximize likelihood | BERT |
| SentencePiece | Learns subwords directly from raw text (no whitespace preprocessing required) | T5, LLaMA |

### Interview Answers

Why not use word-level tokenization? Because unseen words become Out-of-Vocabulary (OOV). Subword tokenization can split unknown words into known pieces, allowing the model to handle new words.

BPE vs WordPiece? BPE merges the most frequent symbol pairs. WordPiece merges the pair that best improves language-model likelihood.

Why use SentencePiece? It works directly on raw text without relying on whitespace, making it language-independent and suitable for languages where words are not separated by spaces.

---

## 14. Practical Masking & Batching Strategies

### Padding & Attention Mask

Different sentences have different lengths. A batch requires all sequences to be the same length, so we pad the shorter ones.

Sentence 1: I love AI Sentence 2: Hello PAD PAD

Should the model pay attention to PAD? No. Create a padding mask so the model ignores PAD tokens. Also use CrossEntropyLoss(ignore_index=PAD) so the model isn't punished for PAD predictions.

### Bucketing (Length Batching)

If sentence lengths are [3, 4, 5, 60, 58, 62], random batching pads everything to 60, wasting compute. Instead, group similar lengths together:

- Batch 1: [3, 4, 5]
- Batch 2: [58, 60, 62]

Very little padding needed. Less memory, faster training, less wasted computation.

### Packing Sequences

If your sequence length is 64 but sentences are 10, 12, or 15 tokens, most of the 64-token input is just PAD. Instead, combine them:

Sentence1 <EOS> Sentence2 <EOS> Sentence3

Now almost every token is useful. Better GPU utilization, less padding, higher throughput.

### Causal Mask

Used in GPT-like models. When predicting "love" in "I love AI," the model should only see "I" — not "AI." Future words are masked.

### Combining Padding Mask + Causal Mask

Two things must happen:
1. Don't look into the future (causal mask).
2. Don't look at PAD tokens (padding mask).

Both masks are combined before applying softmax.

### Interview Summary

| Strategy | Why It's Used |
|----------|---------------|
| Padding | Makes all sequences in a batch the same length |
| Padding Mask | Prevents attention to fake PAD tokens and ignores them in the loss |
| Bucketing | Groups similar-length sequences to reduce padding and speed up training |
| Packing Sequences | Combines multiple short examples into one longer sequence to reduce wasted space and improve GPU utilization |
| Causal Mask | Prevents the model from seeing future tokens during next-token prediction |

> One-line interview answer: Padding makes batch sizes uniform, padding masks ignore fake PAD tokens, bucketing minimizes unnecessary padding, packing improves GPU efficiency by filling sequences with useful tokens, and causal masks prevent autoregressive models from looking at future tokens.

---

## 15. Efficiency & Scaling Pointers

### Mixed Precision (AMP)

Normally, models use 32-bit floating point (FP32). Mixed precision uses 16-bit (FP16/BF16) wherever it's safe. Benefits: half the memory usage, much faster training on modern GPUs (Tensor Cores), and allows larger batch sizes.

### Gradient Accumulation

If your GPU can only fit a batch of 16 but you want an effective batch size of 64:

Batch 1 → compute gradients Batch 2 → add gradients Batch 3 → add gradients Batch 4 → add gradients ↓ Update weights once

This behaves almost like training with batch size 64. Useful when GPU memory is limited.

### Activation Checkpointing

Normally during the forward pass, the model stores every intermediate activation for backpropagation. Deep models → huge memory usage. Checkpointing stores only a few activations and recomputes the missing ones during backpropagation. Trade-off: less memory, more computation.

> Analogy: Instead of saving every step of a math problem, you only save a few important steps. Later, if needed, you quickly redo the missing calculations.

### FlashAttention

Normal attention creates a huge n×n attention matrix. FlashAttention computes attention in small blocks (tiles) instead of storing the full matrix. Benefits: faster, much less memory, same mathematical result.

> FlashAttention is a memory-efficient implementation of attention that avoids materializing the full attention matrix.

### Fused QKV Projection

Normally: Input → Q Linear, K Linear, V Linear — three separate matrix multiplications. Instead, many implementations compute them together: Input → one large Linear → split into Q, K, V. Less overhead, faster.

### Weight Tying

Normally there are two large matrices: input embedding (token IDs → vectors) and output layer (vectors → vocabulary logits). Weight tying uses the same matrix for both — the output layer uses the transpose of the embedding matrix. Benefits: fewer parameters, less memory, often slightly better generalization.

### Long Context Solutions

Attention cost is O(n²). If sequence length doubles, attention becomes roughly 4× more expensive.

- Sliding Window: Each token attends only to nearby tokens instead of everyone.
- RoPE: Better positional encoding that helps models generalize to longer contexts.
- Retrieval: Instead of putting the entire book into the model, retrieve only the relevant pages (used in RAG).

### Practical Tokenization Exercise

Try two tokenizers on a small corpus (BPE via HuggingFace Tokenizers and SentencePiece). Compare:

- Number of tokens for the same text (smaller is usually better).
- Token length distribution — are tokens mostly 2 chars, 5 chars, or whole words?
- Unknown token rate — how often does the tokenizer produce <UNK>? (Lower is better; modern subword tokenizers usually have very low rates.)

### Interview Summary Table

| Concept | Simple Idea |
|---------|-------------|
| Mixed Precision (AMP) | Use FP16/BF16 where possible to reduce memory and speed up training |
| Gradient Accumulation | Simulate a larger batch by accumulating gradients over multiple smaller batches before updating |
| Activation Checkpointing | Save memory by recomputing some activations during backpropagation instead of storing them all |
| FlashAttention | Memory-efficient attention that computes attention in blocks without storing the full attention matrix |
| Fused QKV | Compute Q, K, and V with one matrix multiplication instead of three |
| Weight Tying | Share input embedding and output projection weights to reduce parameters and improve generalization |
| Sliding Window | Each token attends only to nearby tokens to reduce attention cost |
| RoPE | Positional encoding that helps Transformers handle longer contexts |
| Retrieval | Fetch only relevant external information instead of placing everything into the context window |

### For AI/ML Intern Interviews

Know the intuition behind:
- Mixed Precision (AMP)
- Gradient Accumulation
- FlashAttention
- Weight Tying
- Why attention is O(n²) and how long-context methods reduce that cost

The implementation details of FlashAttention or checkpointing are usually not expected unless you're interviewing for a deep learning systems or LLM infrastructure role.
