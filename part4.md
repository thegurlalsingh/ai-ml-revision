# Deep Learning Interview Handbook: CNN Theory, Optimization & Debugging

> A comprehensive reference covering CNN fundamentals, Batch Normalization, Dropout, optimization algorithms, gradient issues, training diagnostics, and practical debugging strategies — organized for interview preparation and daily reference.

---

## Table of Contents

- [1. Spatial Equivariance (Translation Equivariance)](#1-spatial-equivariance-translation-equivariance)
- [2. Pooling & Stride](#2-pooling--stride)
- [2.1 Max Pooling](#21-max-pooling)
- [2.2 Average Pooling](#22-average-pooling)
- [2.3 MaxPool vs AvgPool](#23-maxpool-vs-avgpool)
- [2.4 Why Use Pooling?](#24-why-use-pooling)
- [2.5 What is Stride?](#25-what-is-stride)
- [2.6 Strided Convolution vs Pooling](#26-strided-convolution-vs-pooling)
- [3. CNN Backpropagation (Intuition)](#3-cnn-backpropagation-intuition)
- [3.1 Forward Pass Review](#31-forward-pass-review)
- [3.2 Two Key Questions](#32-two-key-questions)
- [3.3 Why "Flipping the Filter"?](#33-why-flipping-the-filter)
- [3.4 Shapes (Interview Favorite)](#34-shapes-interview-favorite)
- [4. Equivariance vs Invariance](#4-equivariance-vs-invariance)
- [4.1 Translation Equivariance (Convolution)](#41-translation-equivariance-convolution)
- [4.2 Translation Invariance (Pooling)](#42-translation-invariance-pooling)
- [4.3 Quick Comparison](#43-quick-comparison)
- [5. Batch Normalization](#5-batch-normalization)
- [5.1 Why Do We Need Batch Normalization?](#51-why-do-we-need-batch-normalization)
- [5.2 BatchNorm Formula](#52-batchnorm-formula)
- [5.3 Scale and Shift: γ and β](#53-scale-and-shift-γ-and-β)
- [5.4 Training vs Inference](#54-training-vs-inference)
- [5.5 Benefits of BatchNorm](#55-benefits-of-batchnorm)
- [5.6 What is Internal Covariate Shift?](#56-what-is-internal-covariate-shift)
- [6. Dropout](#6-dropout)
- [6.1 Why is Dropout Needed?](#61-why-is-dropout-needed)
- [6.2 How Dropout Works](#62-how-dropout-works)
- [6.3 Inverted Dropout](#63-inverted-dropout)
- [6.4 Where is Dropout Used?](#64-where-is-dropout-used)
- [6.5 BatchNorm vs Dropout](#65-batchnorm-vs-dropout)
- [7. Practical Hyperparameters & Tips](#7-practical-hyperparameters--tips)
- [7.1 Batch Size](#71-batch-size)
- [7.2 Large Batch & LR Tuning (Linear Scaling Rule)](#72-large-batch--lr-tuning-linear-scaling-rule)
- [7.3 Weight Decay](#73-weight-decay)
- [7.4 Learning Rate Schedules](#74-learning-rate-schedules)
- [7.5 Early Stopping](#75-early-stopping)
- [7.6 Data Augmentation](#76-data-augmentation)
- [7.7 Hyperparameter Cheat Sheet](#77-hyperparameter-cheat-sheet)
- [8. Diagnosing Training Curves](#8-diagnosing-training-curves)
- [8.1 Case 1: Training Loss Not Decreasing](#81-case-1-training-loss-not-decreasing)
- [8.2 Case 2: Loss Decreases but Accuracy Low](#82-case-2-loss-decreases-but-accuracy-low)
- [8.3 Case 3: Train Improves but Validation Degrades](#83-case-3-train-improves-but-validation-degrades)
- [8.4 Interview Debugging Flow](#84-interview-debugging-flow)
- [8.5 Debugging Cheat Sheet](#85-debugging-cheat-sheet)
- [8.6 Overfitting on a Tiny Subset (Critical Debugging Trick)](#86-overfitting-on-a-tiny-subset-critical-debugging-trick)
- [8.7 Check Gradient Norms Per Layer](#87-check-gradient-norms-per-layer)
- [8.8 Confirm Data Normalization](#88-confirm-data-normalization)
- [9. Vanishing & Exploding Gradient Remedies](#9-vanishing--exploding-gradient-remedies)
- [9.1 ReLU + He Initialization](#91-relu--he-initialization)
- [9.2 Batch Normalization / Layer Normalization](#92-batch-normalization--layer-normalization)
- [9.3 Gradient Clipping](#93-gradient-clipping)
- [10. Optimizer Primer & Taxonomy](#10-optimizer-primer--taxonomy)
- [10.1 SGD (Stochastic Gradient Descent)](#101-sgd-stochastic-gradient-descent)
- [10.2 SGD + Momentum](#102-sgd--momentum)
- [10.3 Nesterov Momentum](#103-nesterov-momentum)
- [10.4 RMSProp](#104-rmsprop)
- [10.5 Adam](#105-adam)
- [10.6 AdamW](#106-adamw)
- [10.7 Optimizer Comparison Table](#107-optimizer-comparison-table)
- [10.8 When to Use Which](#108-when-to-use-which)
- [11. Adam: Where It Excels and Where It Fails](#11-adam-where-it-excels-and-where-it-fails)
- [11.1 Where Adam Excels](#111-where-adam-excels)
- [11.2 Where Adam Fails](#112-where-adam-fails)
- [11.3 Decision Guide](#113-decision-guide)
- [12. Adam: Update Equations & Bias Correction](#12-adam-update-equations--bias-correction)
- [12.1 The Two Memories](#121-the-two-memories)
- [12.2 Understanding \(m_t\) (First Moment)](#122-understanding-m_t-first-moment)
- [12.3 Understanding \(v_t\) (Second Moment)](#123-understanding-v_t-second-moment)
- [12.4 Why Bias Appears](#124-why-bias-appears)
- [12.5 Bias Correction](#125-bias-correction)
- [12.6 The Final Update Formula](#126-the-final-update-formula)
- [12.7 Practical Notes](#127-practical-notes)
- [13. Weight Decay vs L2 Regularization](#13-weight-decay-vs-l2-regularization)
- [13.1 L2 Regularization](#131-l2-regularization)
- [13.2 Weight Decay](#132-weight-decay)
- [13.3 Why They Are Equivalent for SGD](#133-why-they-are-equivalent-for-sgd)
- [13.4 Why Adam Breaks the Equivalence](#134-why-adam-breaks-the-equivalence)
- [13.5 AdamW Fix](#135-adamw-fix)
- [Appendix A: Interview-Ready Summaries](#appendix-a-interview-ready-summaries)
- [Appendix B: One-Line Memory Tricks](#appendix-b-one-line-memory-tricks)

---

## 1. Spatial Equivariance (Translation Equivariance)

### Definition

A CNN is spatially (translation) equivariant because if the input image shifts, the detected features also shift by the same amount.

### Example

Suppose a cat is on the left side of the image:

🐱

A convolution filter detects the cat. Now move the cat to the right:

🐱

The same filter (because of weight sharing) slides across the image and still detects the cat. The output feature map also shifts to the right.

### Why Does This Happen?

Because the same kernel is applied at every location in the image. It doesn't matter where the object is — the kernel is looking for the same pattern everywhere.

### Why Is It Useful?

- Without this property: The network would have to learn a separate detector for a cat on the left, center, and right.
- With spatial equivariance: One filter detects the object anywhere in the image.

### Interview-Ready Answer (30 seconds)

> Spatial equivariance means that if an object in the input image shifts, the corresponding activation in the feature map shifts by the same amount. This happens because CNNs use the same convolution kernel at every spatial location (weight sharing), allowing them to detect the same feature regardless of where it appears in the image.

> Note: Don't confuse equivariance with invariance. Convolution is translation equivariant (the output shifts when the input shifts). After pooling or global average pooling, the network becomes more translation invariant, meaning small shifts in the input don't significantly change the final prediction. This distinction is another common interview question.

---

## 2. Pooling & Stride

Pooling reduces spatial resolution, provides translation invariance, and reduces compute. Strided convolution can replace pooling for downsampling.

### 2.1 Max Pooling

After convolution, we get a feature map. Instead of keeping every value, pooling summarizes a small region.

Example input:

1 3 2 4 5 6 1 2 7 8 3 1 2 4 5 6

With a 2×2 window and stride 2:

| Window | Values | Max |
|--------|--------|-----|
| First | 1, 3, 5, 6 | 6 |
| Second | 2, 4, 1, 2 | 4 |
| Third | 7, 8, 2, 4 | 8 |
| Fourth | 3, 1, 5, 6 | 6 |

Output:

6 4 8 6

Intuition: Imagine a feature map detecting eyes:

0 0 8 0 0 9 7 0 0 1 0 0

The 9 means "Eye detected strongly here." MaxPool keeps 9 and ignores the smaller values. It preserves the strongest evidence.

### 2.2 Average Pooling

Instead of the maximum, take the average.

Example with 2×2 window:

1 3 5 7

Average:

$$\frac{1 + 3 + 5 + 7}{4} = 4$$

Intuition: Instead of asking "What's the strongest feature?", Average Pooling asks "What's the average activation in this region?"

### 2.3 MaxPool vs AvgPool

| Feature | Max Pooling | Average Pooling |
|---------|-------------|-----------------|
| Keeps | Strongest feature | Average information |
| Better for | Feature detection | Smoothing |
| Commonly used | Most commonly used | Less common today |

### 2.4 Why Use Pooling?

1. Reduce image size:

32×32 ↓ MaxPool 16×16

Fewer numbers → Less computation.

2. Reduce overfitting:

Smaller feature maps → Fewer computations → Less chance of memorizing noise.

3. Small Translation Invariance:

Suppose the eye moves by one pixel.

- Without pooling: Activation changes location.
- With MaxPool: Both positions may still produce the same pooled value.

The network becomes less sensitive to tiny shifts. This is called translation invariance.

> Important distinction:
> - Convolution: Translation equivariance (feature map shifts when input shifts).
> - Pooling: More translation invariance (small input shifts often don't change the pooled output much).

### 2.5 What is Stride?

Normally, the kernel moves one pixel at a time — this is Stride = 1:

□ □ □ □ ↓ move 1 pixel □ □ □ □

With Stride = 2:

□ □ □ □ ↓ jump two pixels □ □ □ □

Example: Input 8×8, kernel 3×3, stride 2 → output is much smaller.

### 2.6 Strided Convolution vs Pooling

Modern CNNs often use Stride = 2 convolution instead of Convolution → Pooling.

Why? Pooling has no learnable parameters — it just takes a max or average. A strided convolution learns how to downsample because the filter weights are trainable. This is why architectures like ResNet often use strided convolutions instead of separate pooling layers.

---

## 3. CNN Backpropagation (Intuition)

The idea is the same as backpropagation in fully connected layers.

### 3.1 Forward Pass Review

Input ↓ Filter ↓ Feature map ↓ Loss

During backprop, the loss tells us "The prediction was wrong." Now we ask two questions.

### 3.2 Two Key Questions

Question 1: How should the filter change?

This gives $\frac{\partial L}{\partial K}$ where $K$ is the convolution filter.

Intuition: Imagine a filter detects vertical edges. If the network made a mistake, should the filter respond more strongly? Less strongly? The gradient tells us how each filter weight should change.

Mathematically, this is obtained by convolving the input with the upstream gradients (often described as using a flipped gradient depending on the exact convolution/correlation convention).

Question 2: How should the input change?

This gives $\frac{\partial L}{\partial X}$ because earlier layers also need gradients.

To compute this, we "send the error backward" through the filter. Conceptually, this is another convolution involving the upstream gradients and the filter (again, flipping depends on the implementation convention).

### 3.3 Why "Flipping the Filter"?

In pure mathematics, true convolution flips the kernel before applying it:

1 2 4 3 3 4 → 2 1

However, most deep learning libraries (PyTorch, TensorFlow, etc.) actually perform cross-correlation during the forward pass — they do not flip the kernel.

During backpropagation, the formulas naturally involve flipped versions so that the gradients are mathematically correct.

> Interview-ready explanation: "The backward pass for convolution is itself another convolution-like operation. Gradients with respect to the filters are computed by correlating the input with the upstream gradients, while gradients with respect to the input are obtained by propagating the upstream gradients through the filters. The exact flipping depends on whether the implementation uses convolution or cross-correlation."

### 3.4 Shapes (Interview Favorite)

Suppose:

| Component | Shape |
|-----------|-------|
| Input | 32 × 32 × 3 |
| Kernel | 64 × 3 × 3 × 3 |
| Output | 30 × 30 × 64 |

During backprop:

| Gradient | Shape |
|----------|-------|
| Filter gradient ($dK$) | 64 × 3 × 3 × 3 (same as kernel) |
| Input gradient ($dX$) | 32 × 32 × 3 (same as input) |

> A parameter's gradient always has the same shape as that parameter.

---

## 4. Equivariance vs Invariance

This is one of the most common CNN interview questions.

### 4.1 Translation Equivariance (Convolution)

Image 1:

+----------------+ | 🐱 | | | | | +----------------+

The CNN detects the cat on the left. The feature map shows a high activation at that location: █

Image 2 (cat moved):

+----------------+ | 🐱 | | | | | +----------------+

The feature map also moves: █

The detector still works. The cat moved, and the feature also moved. Nothing is lost. The feature simply changes its location.

> Definition: If the input shifts, the output also shifts by the same amount.

### 4.2 Translation Invariance (Pooling)

Before pooling, the feature map is:

0 0 8 0 0 0 0 0

Move the cat slightly — feature map becomes:

0 8 0 0 0 0 0 0

Different location. Now apply a 2×2 MaxPool:

| Feature Map | Pooling Window | Max |
|-------------|----------------|-----|
| First | 0 0 / 0 0, 8 0 / 0 0 | 8 |
| Second | 0 8 / 0 0, 0 0 / 0 0 | 8 |

Even though the feature moved, the pooled output is still 8. The network now doesn't care about the exact location — it only cares that "A cat exists somewhere in this region."

> Definition: Translation invariance means small shifts in the input often produce nearly the same pooled output, making the final prediction less sensitive to the exact location of the object.

### 4.3 Quick Comparison

| Property | Equivariance | Invariance |
|----------|--------------|------------|
| Input moves → | Output also moves | Output stays almost the same |
| Caused by | Convolution (weight sharing) | Pooling |
| Visual | Cat →, Feature → | Cat →, Prediction: Still Cat |

### Interview Answer

> Convolution is translation equivariant because if an object moves in the input, the activation map moves by the same amount. Pooling introduces translation invariance because small shifts in the object often produce nearly the same pooled output, making the final prediction less sensitive to the exact location of the object.

---

## 5. Batch Normalization

### 5.1 Why Do We Need Batch Normalization?

Suppose we have a neural network:

Input → Layer 1 → Layer 2 → Layer 3 → Output

During training, Layer 1's weights keep changing. Because Layer 1 changes, its outputs also change. Those outputs become the inputs to Layer 2. So Layer 2 keeps seeing a different distribution of inputs every iteration.

| Iteration | Mean | Variance |
|-----------|------|----------|
| 1 | 2 | 1 |
| 100 | 15 | 30 |
| 500 | -4 | 7 |

Layer 2 has to constantly adapt to changing inputs. Training becomes unstable and slower.

Solution: Normalize every batch.

Suppose activations are: 8, 10, 12

Mean $\mu = 10$, subtract mean:

-2, 0, 2

Divide by standard deviation ($\sigma = 2$):

-1, 0, 1

Now every batch has roughly mean 0 and variance 1. This makes learning much more stable.

### 5.2 BatchNorm Formula

There are 4 steps.

Step 1: Compute Mean

For a mini-batch of $m$ samples:

$$\boxed{\mu_B = \frac{1}{m} \sum_i x_i}$$

Example: Batch [2, 4, 6, 8] → Mean = 5

Step 2: Compute Variance

$$\boxed{\sigma_B^2 = \frac{1}{m} \sum_i (x_i - \mu_B)^2}$$

Example: Mean = 5, differences [-3, -1, 1, 3], squares [9, 1, 1, 9], average = 5. Variance = 5.

Step 3: Normalize

$$\boxed{\hat{x} = \frac{x - \mu_B}{\sqrt{\sigma_B^2 + \epsilon}}}$$

Subtract mean, divide by standard deviation. The small $\epsilon$ (e.g., $10^{-5}$) prevents division by zero.

Example: Input [2, 4, 6, 8], mean = 5, std ≈ 2.236 → Normalized: [-1.34, -0.45, 0.45, 1.34]

Mean ≈ 0, Variance ≈ 1.

Step 4: Scale and Shift

Normalization forces everything to mean 0 and variance 1, but that may not be ideal for the network. So BatchNorm adds two learnable parameters.

$$\boxed{y = \gamma \hat{x} + \beta}$$

Where:
- $\gamma$ = learnable scale
- $\beta$ = learnable shift

Example: Normalized [-1, 0, 1], $\gamma = 2$, $\beta = 5$ → Output: [3, 5, 7]

The network isn't forced to keep mean 0 forever — it can learn a better scale and offset if needed.

### 5.3 Scale and Shift: γ and β

This is the most misunderstood part of BatchNorm.

Why is normalization alone not enough?

Suppose activations are [20, 30, 40]. After BatchNorm they become [-1, 0, 1]. But what if the network actually wants values around [10, 20, 30] instead? BatchNorm has destroyed that information by forcing everything to mean 0 and variance 1. The network loses flexibility.

Gamma (γ): Stretches or shrinks the normalized values.

$$y = \gamma \hat{x}$$

| Normalized | γ = 3 | Result |
|------------|-------|--------|
| -1 | × 3 | -3 |
| 0 | × 3 | 0 |
| 1 | × 3 | 3 |

Gamma controls the spread (contrast) of the activations. Think of a photo editor — brightness stays the same, but you increase the contrast. Dark pixels become darker, bright pixels become brighter.

Beta (β): Shifts everything up or down.

$$y = \hat{x} + \beta$$

| Normalized | β = 5 | Result |
|------------|-------|--------|
| -1 | + 5 | 4 |
| 0 | + 5 | 5 |
| 1 | + 5 | 6 |

Beta changes the center (offset) of the activations. Think of moving the entire graph upward.

Together: Normalized [-1, 0, 1], γ = 2, β = 5 → y = 2x̂ + 5 → [3, 5, 7]

BatchNorm first standardizes the data, and then the network learns the best scale and offset through γ and β. We get both: stable optimization and flexibility.

### 5.4 Training vs Inference

During training:
- Compute batch mean and batch variance for each mini-batch
- Normalize using those values
- Also maintain a running mean and running variance

During inference (testing):
- Usually process one image at a time — computing a "batch mean" from a single sample would be unstable
- Use the running mean and running variance collected during training

### 5.5 Benefits of BatchNorm

1. Faster training: The optimizer sees more stable activations.

2. Larger learning rates:
- Without BatchNorm: LR typically 0.001
- With BatchNorm: often 0.01 works safely

3. More stable gradients: Reduces exploding and vanishing gradient problems.

4. Slight regularization: Each mini-batch has slightly different statistics, introducing a little randomness that reduces overfitting.

### 5.6 What is Internal Covariate Shift?

Analogy: Imagine you're preparing for an exam. Today your teacher teaches using English. Tomorrow she suddenly starts teaching in French. The day after that, she starts using German. Every day the input distribution changes. You'll learn much more slowly because you're constantly adapting. This changing input distribution is called covariate shift.

Inside a Neural Network:

During training, Layer 1 updates its weights. Because its weights changed, its outputs also change.

| Iteration | Layer 1 Outputs | Impact on Layer 2 |
|-----------|-----------------|-------------------|
| 1 | 2, 4, 6 | Layer 2 learns using these numbers |
| 100 | 20, 40, 60 | Layer 2 suddenly sees completely different inputs |
| 500 | -5, 7, 15 | Layer 2 has to adapt again |

This keeps happening throughout training. This phenomenon is called Internal Covariate Shift because the distribution inside the network keeps changing.

Why is it bad? Imagine learning to drive. Today the steering wheel is on the right. Tomorrow it's on the left. Next day it's at the back! You'd keep relearning instead of improving. Similarly, Layer 2 keeps adjusting to changing inputs instead of learning the actual task.

How BatchNorm helps: BatchNorm forces activations to look similar every iteration. Instead of [2, 4, 6] or [20, 40, 60] or [-5, 7, 15], BatchNorm converts all of them to something like [-1, 0, 1]. Now Layer 2 always receives stable inputs. Learning becomes easier.

> Interview definition: Internal Covariate Shift refers to the changing distribution of activations inside a neural network during training because earlier layers continuously update their weights. Batch Normalization reduces this by normalizing activations in each mini-batch, leading to more stable and faster training.

---

## 6. Dropout

### 6.1 Why Is Dropout Needed?

Suppose we have:

Input → 100 neurons → Output

Imagine one neuron becomes extremely important. The network starts relying on it. Other neurons don't learn useful features. This is called co-adaptation.

### 6.2 How Dropout Works

Randomly turn off neurons during training.

● ● ● ● ● ● ● ● (All active) ↓ Dropout ● × ● ● × ● × ● (Crossed neurons temporarily ignored)

Next mini-batch, a different set is dropped.

Why does this help? Since any neuron may disappear, the network cannot rely too much on one neuron. Instead, many neurons learn useful features. It behaves like training many slightly different networks and averaging them.

### 6.3 Inverted Dropout

The Problem: Suppose you have 10 neurons, each outputs 2, total activation = 20. Now use 50% dropout. Half the neurons disappear. Remaining sum = 10. The activations have become half as large. If this keeps happening, the next layer sees much smaller values during training than during testing. That mismatch hurts performance.

The Solution: Scale the remaining neurons during training.

Keep probability = 0.5. Multiply surviving neurons by $\frac{1}{0.5} = 2$.

Example: Remaining neurons [2, 2, 2, 2, 2] → After scaling: [4, 4, 4, 4, 4] → Sum = 20. Now the expected activation is the same as if dropout had never been applied.

Why is it called "Inverted" Dropout?

| Method | Training | Testing |
|--------|----------|---------|
| Old Dropout | Drop neurons, do not scale | Multiply outputs by keep probability |
| Inverted Dropout (Modern) | Drop neurons, scale by 1/keep_prob | Do nothing |

Inverted Dropout is what PyTorch and TensorFlow use because inference is faster and simpler.

> Interview definition: Inverted Dropout scales the activations of the neurons that remain during training by $1/\text{keep probability}$. This keeps the expected activation the same during training and inference, so no scaling is required at test time.

### 6.4 Where Is Dropout Used?

- Fully connected layers: ✅ Common
- MLPs: ✅ Common
- After convolution layers: Less common — convolution already shares weights and has fewer parameters. If used, variants like Spatial Dropout are often preferred (dropping entire feature maps/channels rather than individual pixels).

### 6.5 BatchNorm vs Dropout

| Feature | BatchNorm | Dropout |
|---------|-----------|---------|
| Purpose | Stabilizes training | Reduces overfitting |
| Mechanism | Normalizes activations | Randomly removes neurons |
| Uses | Batch statistics | Random masking |
| Effect | Speeds up convergence | Improves generalization |
| Active during | Both training and inference (with different statistics) | Training only |

---

## 7. Practical Hyperparameters & Tips

### 7.1 Batch Size

What is Batch Size? Suppose you have 10,000 images. Do we feed all of them together? No. We divide them into smaller groups called batches.

10,000 images ↓ [32 images] [32 images] [32 images] ...

If Batch Size = 32, every gradient update uses only 32 images.

Why not Batch Size = 1? Gradients are noisy — weights keep moving randomly (Stochastic Gradient Descent).

Why not the whole dataset? One gradient computation becomes extremely slow and needs huge RAM/GPU memory.

Mini-Batch is the Best: Typical values: 32, 64, 128, 256.

| Quality | Small Batch | Large Batch | Mini-Batch (32–256) |
|---------|-------------|-------------|-------------------|
| Gradient stability | Noisy | Stable | Good balance |
| GPU computation | Fast | Slow | Efficient |
| Memory usage | Low | Very high | Reasonable |

> Interview answer: Small batches give noisy gradients and unstable training. Very large batches require lots of memory and may generalize worse. Batch sizes between 32 and 256 provide a good balance between stability, computational efficiency, and memory usage.

### 7.2 Large Batch & LR Tuning (Linear Scaling Rule)

Suppose Batch Size = 32, LR = 0.001. Now increase batch size to 64. The gradient becomes more accurate because it's averaged over more examples. Since the gradient is less noisy, we can usually take a larger step.

Rule: Double batch → Double learning rate.

Batch Size 32: LR = 0.001 Batch Size 64: LR = 0.002

Why? Larger batches produce smoother gradient estimates. A smoother gradient allows larger optimization steps without overshooting.

### 7.3 Weight Decay

Weight decay is L2 Regularization. Huge weights cause overfitting. Weight decay continuously pulls weights toward zero.

Formula:

$$L_{\text{new}} = L + \lambda ||W||^2$$

The optimizer now minimizes both prediction error and a penalty for large weights.

Typical CNN value: 1e-4 (0.0001)

> Interview question: Why is it called weight decay? During gradient descent, weights shrink slightly every update. They literally "decay."

### 7.4 Learning Rate Schedules

Instead of keeping LR constant, we change it during training. Early training needs big steps. Late training needs tiny adjustments. Like parking a car — far away, drive fast. Near the spot, slow down.

#### A. Step Learning Rate

Epoch 1-30: LR = 0.01 Epoch 31-60: LR = 0.001 Epoch 61-90: LR = 0.0001

Simple and effective.

#### B. Cosine Annealing

Instead of sudden drops, reduce LR smoothly following a cosine curve.

LR |\ | \ | \ | \____ ------------ Epoch

Benefits: Smooth optimization, often reaches better minima. Very popular today.

#### C. ReduceLROnPlateau

If validation loss stops improving (e.g., stays at 0.22 for many epochs), automatically reduce LR.

Validation loss: 0.30 → 0.25 → 0.22 → 0.22 → 0.22 → 0.22 ↓ Auto-reduce LR: 0.001 → 0.0001

Which schedule is best? There is no universal winner.

| Schedule | Best For |
|----------|----------|
| Step LR | Simple and common |
| Cosine Annealing | Excellent for deep learning, widely used |
| ReduceLROnPlateau | When validation performance stalls |

### 7.5 Early Stopping

Training loss: 0.9 → 0.6 → 0.3 → 0.1 (keeps improving) Validation loss: 0.9 → 0.5 → 0.4 → 0.5 → 0.6 → 0.8 (starts increasing) ↑ STOP

The model has begun overfitting. Stop training. Continuing only memorizes training data. Stopping early usually gives better generalization.

### 7.6 Data Augmentation

Modify existing images to create more diverse training samples without collecting new data.

Common augmentations for CIFAR-10:

| Augmentation | Description |
|--------------|-------------|
| Random Crop + Padding | Pad 32×32 → 40×40, randomly crop back to 32×32 |
| Horizontal Flip | Flip the image horizontally |
| Color Jitter | Randomly change brightness, contrast, saturation |

Why does this help? The model no longer memorizes exact pixel positions. Instead, it learns "This is a cat regardless of small changes." Generalization improves.

### 7.7 Hyperparameter Cheat Sheet

| Hyperparameter | Purpose | Typical Values |
|----------------|---------|----------------|
| Batch Size | Samples per gradient update | 32–256 |
| Learning Rate | Controls update step size | 0.001 (Adam), 0.01 (SGD + momentum) |
| Weight Decay | L2 regularization | 1e-4 |
| Step LR | Reduce LR at fixed epochs | Simple, manually scheduled |
| Cosine Annealing | Smoothly decrease LR | Common in modern CNNs |
| ReduceLROnPlateau | Lower LR when validation stalls | Adaptive schedule |
| Early Stopping | Stop when validation no longer improves | Prevents overfitting |
| Data Augmentation | Create diverse training samples | Crop, flip, rotate, color jitter |

---

## 8. Diagnosing Training Curves

This is one of the most practical interview topics — testing whether you can debug a real training run.

### 8.1 Case 1: Training Loss Not Decreasing

Loss 1.5 ───────────────────────── 1.5 ───────────────────────── 1.5 ───────────────────────── 1.5 ───────────────────────── Epochs

The model isn't learning at all.

#### Step 1: Check the Learning Rate

Too Small:

$$\eta = 0.0000001$$

Weight updates become tiny:

Current weight: 5.000000 After update: 4.9999999 (almost no change)

Loss decreases extremely slowly.

Too Large:

$$\eta = 10$$

Instead of moving toward the minimum, you overshoot it.

Loss 2 |\/\_/\/\/\ | | Epochs

Loss jumps up and down. Sometimes it even becomes NaN because updates explode.

> Interview answer: If training loss isn't decreasing, the first thing I'd check is the learning rate. A very small learning rate causes extremely slow progress, while a very large learning rate causes oscillations or divergence.

#### Step 2: Check Initialization

Never initialize all weights to zero. Every neuron computes exactly the same output → same gradient → same update. They remain identical forever. This is the symmetry problem.

| Initialization | Used For | Notes |
|----------------|----------|-------|
| Xavier | tanh, sigmoid | Keeps activation variance roughly constant |
| He | ReLU | Starts with slightly larger weights since ReLU zeros out many activations |

> Interview answer: Never initialize all weights to zero because every neuron receives the same gradients and learns identical features. Xavier initialization is commonly used for tanh/sigmoid activations, while He initialization is preferred for ReLU-based networks.

#### Step 3: Check the Data Pipeline

Sometimes the model is perfectly fine. The data is wrong.

| Check | Why |
|-------|-----|
| Labels correct? | Cat labeled as Dog → can never learn |
| Normalization correct? | Pixels 0–255 instead of 0–1 → harder optimization |
| Shuffling enabled? | Seeing 1000 cats then 1000 dogs → biased updates |

> Interview answer: Always verify the data pipeline. Check that labels are correct, inputs are normalized appropriately, preprocessing is consistent, and training samples are shuffled.

#### Step 4: Check Gradient Flow

Print the gradient norm for each layer.

| Scenario | Layer 3 | Layer 2 | Layer 1 | Diagnosis |
|----------|---------|---------|---------|-----------|
| Vanishing | 0.4 | 0.02 | 0.0000001 | Earlier layers barely update |
| Exploding | 2 | 50 | 50000 | Weights become enormous, loss → NaN |

> Interview answer: Monitor gradient norms for every layer. Near-zero gradients indicate vanishing gradients, while extremely large gradients indicate exploding gradients.

#### Step 5: Check Weight Norms

- Small weight norms (e.g., [1, 2, 1]) → Healthy
- Large weight norms (e.g., [1000, 2000, 3000]) → Unstable training or excessively high LR

### 8.2 Case 2: Loss Decreases but Accuracy Low

Loss: ↓ ↓ ↓ ↓ Accuracy: 20% 21% 22% 23%

| Possible Cause | Explanation |
|----------------|-------------|
| Model too simple | Trying to classify 100 classes with a tiny linear model — lacks capacity |
| Wrong loss function | Using MSE for classification instead of Cross-Entropy |
| Output saturation | Logits become [100, -100, -90], softmax becomes near [1, 0, 0], model is overconfident and gradients become very small |

> Interview answer: If loss decreases but accuracy remains poor, I would check model capacity, verify that the correct loss function is being used, inspect output logits for saturation, and ensure the evaluation metric is implemented correctly.

### 8.3 Case 3: Train Improves but Validation Degrades

This is the classic sign of overfitting.

Training loss: ↓ ↓ ↓ ↓ (keeps decreasing) Validation loss: ↓ ↓ ↑ ↑ (starts increasing)

The model is memorizing the training set.

Solutions:

1. Regularization: L2 weight decay, Dropout
2. Data augmentation: More diverse images → less memorization
3. Early stopping: Stop training before overfitting begins
4. Smaller model: Fewer parameters → harder to memorize

### 8.4 Interview Debugging Flow

> If someone asks "Your neural network isn't working. What will you do?" — a strong answer is:

1. Check the learning rate (too low → slow, too high → divergence)
2. Verify weight initialization (Xavier/He, avoid zero)
3. Inspect the data pipeline (labels, normalization, shuffling)
4. Monitor gradient norms (vanishing or exploding)
5. Inspect weight norms (instability signs)
6. Check model capacity and loss function if loss decreases but accuracy is poor
7. Compare training and validation curves to diagnose overfitting or underfitting
8. Apply appropriate fixes (regularization, augmentation, early stopping, architecture changes)

### 8.5 Debugging Cheat Sheet

| Observation | Likely Cause | Fix |
|-------------|--------------|-----|
| Training loss not decreasing | LR too low/high | Tune LR |
| Loss oscillates or NaN | LR too high / exploding gradients | Lower LR, gradient clipping |
| Loss decreases very slowly | LR too low | Increase LR |
| All neurons learn the same thing | Zero weight initialization | Xavier or He initialization |
| Gradient ≈ 0 | Vanishing gradients | ReLU, BatchNorm, residual connections, better init |
| Gradient extremely large | Exploding gradients | Gradient clipping, lower LR |
| Loss decreases, accuracy stays low | Low capacity, wrong loss, saturated outputs | Increase capacity, verify loss, inspect logits |
| Train high, val low | Overfitting | Regularization, augmentation, early stopping, smaller model |

> Memory trick: When a model fails to train, think in this order: Learning Rate → Initialization → Data → Gradients → Model Capacity → Regularization.

### 8.6 Overfitting on a Tiny Subset (Critical Debugging Trick)

Take only 100 training examples and train for many epochs. A reasonably powerful network should easily memorize such a tiny dataset.

Training Loss: 1.2 → 0.8 → 0.3 → 0.05 → 0.001 Training Accuracy: 20% → 50% → 80% → 99% → 100%

If it DOESN'T overfit, something is likely wrong:
- Bug in forward pass
- Bug in backprop
- Wrong optimizer
- Wrong labels
- Incorrect loss computation
- Data preprocessing issue

What does this test prove?

✅ Forward propagation is correct
✅ Loss function is correct
✅ Backpropagation is correct
✅ Optimizer is updating weights
✅ Labels are aligned correctly
✅ Model has enough capacity

What does it NOT prove?
- Generalization
- Overfitting on the full dataset
- Hyperparameter tuning
- Data augmentation
- Regularization

> Interview answer: Before debugging a complex training issue, I would first check whether the model can overfit a tiny subset (e.g., 100 samples). If it cannot, there's likely a bug in the implementation, optimizer, data pipeline, or loss function. A healthy neural network should always be able to memorize a tiny dataset.

### 8.7 Check Gradient Norms Per Layer

A gradient norm tells you the overall magnitude of a layer's gradient.

| Layer | Gradient Norm | Diagnosis |
|-------|--------------|-----------|
| Layer 4 | 1.5 | Healthy |
| Layer 3 | 0.02 | Decreasing |
| Layer 2 | 0.0001 | Vanishing |
| Layer 1 | 0.00000001 | Vanishing (barely learning) |

| Layer | Gradient Norm | Diagnosis |
|-------|--------------|-----------|
| Layer 1 | 5000 | Exploding |
| Layer 2 | 200 | Large |
| Layer 3 | 10 | Healthy |

In PyTorch, you can inspect gradients after loss.backward() because gradients are stored in each parameter's .grad attribute.

### 8.8 Confirm Data Normalization

Suppose your images have pixel values 0–255. The model may struggle because inputs have large, inconsistent scales.

Correct approach:

$$(\text{image} - \text{mean}) / \text{std}$$

Why use the SAME normalization for training and validation?

If training uses mean 0.5, std 0.2, but validation uses mean 0.8, std 0.4 — the model sees a different input distribution during validation. Performance can drop even if the model is good.

> Always compute normalization statistics from the training set and apply the same transformation to validation and test data.

---

## 9. Vanishing & Exploding Gradient Remedies

### 9.1 ReLU + He Initialization

Why does sigmoid cause vanishing gradients?

The sigmoid derivative:

$$\sigma'(x) = \sigma(x)(1 - \sigma(x))$$

Maximum value = 0.25. Suppose gradients pass through 10 sigmoid layers:

$$0.25^{10} \approx 0.00000095$$

Almost zero. That's vanishing gradients.

Why is ReLU better?

$$f(x) = \max(0, x)$$

Derivative = 1 (for positive input), 0 (for negative input). For positive values, the gradient is preserved instead of shrinking.

Why He Initialization? ReLU randomly sets many activations to zero. If weights are initialized too small, activations become tiny and gradients shrink. He initialization chooses a slightly larger variance so activations and gradients maintain a healthy scale across layers.

> Standard combination: ReLU + He Initialization.

### 9.2 Batch Normalization / Layer Normalization

BatchNorm: Normalizes activations across the mini-batch dimension. Keeps gradients more stable and reduces vanishing/exploding. Standard for CNNs.

LayerNorm: Computes statistics within each individual sample (no dependence on batch size). Standard for Transformers.

| Normalization | Dimension | Used In |
|---------------|-----------|---------|
| BatchNorm | Across mini-batch | CNNs |
| LayerNorm | Within each sample | Transformers |

### 9.3 Gradient Clipping

Purpose: Prevent exploding gradients (common in RNNs, deep nets).

Norm Clipping (most common):

If $||g||_2 > \tau$, then:

$$g \leftarrow g \cdot \frac{\tau}{||g||_2}$$

The entire gradient vector is scaled down while preserving direction.

Example: Gradient = [6, 8], norm = 10, threshold = 5

$$g \leftarrow [6, 8] \cdot \frac{5}{10} = [3, 4]$$

New norm = 5. Direction is the same, magnitude is reduced.

Value Clipping (rare): Clips each gradient component to range [-c, c].

| Norm Clipping | Value Clipping |
|---------------|----------------|
| Clips entire gradient vector | Clips each component independently |
| Preserves direction | Can change direction |
| Most commonly used | Rarely used |

Typical thresholds: 1.0–5.0 (tune per model).

Where clipping is applied:

Forward Pass → Loss → Backward Pass → Compute Gradients ↓ Gradient Clipping ↓ Optimizer Step

> Common in RNNs because gradients multiply across many time steps. Gradient at time step 2 → after ten multiplications → 2¹⁰ = 1024. Clipping keeps it under control.

In PyTorch:

python torch.nn.utils.clip_grad_norm_(model.parameters(), max_norm=1.0)

---

## 10. Optimizer Primer & Taxonomy

### 10.1 SGD (Stochastic Gradient Descent)

$$\theta = \theta - \eta \nabla_\theta L$$

- $\theta$ = weights
- $\eta$ = learning rate
- $\nabla_\theta L$ = gradient

Intuition: SGD only uses today's information. Like driving a car and asking every second "Which direction should I turn now?" while completely forgetting what happened one second ago.

Problem: Zig-zags in narrow valleys, slowing learning.

| Pros | Cons |
|------|------|
| Very simple | Slow |
| Very little memory | Oscillates |
| Often best generalization | Sensitive to learning rate |

### 10.2 SGD + Momentum

$$v = \mu v - \eta \nabla L$$
$$\theta = \theta + v$$

Intuition: Like pushing a heavy ball. First push is slow. Second push is faster. Third is even faster. The ball builds momentum.

Why does it reduce oscillations? In a narrow valley, SGD zig-zags. Momentum smooths out the side-to-side movement and continues mainly in the direction that consistently reduces the loss.

Hyperparameter:

$$\mu = 0.9$$

Meaning 90% of previous velocity is retained.

> Interview answer: Momentum accumulates previous gradients, helping accelerate learning in consistent directions while reducing oscillations.

### 10.3 Nesterov Momentum

Normal momentum: First move, then check the gradient.

Nesterov: First look ahead, then compute the gradient.

Instead of computing the gradient at $\theta$, it computes at $\theta + \mu v$.

Analogy: Like driving and looking ahead before turning, rather than reacting after passing the turn.

Usually gives slightly faster convergence.

### 10.4 RMSProp

Problem: Some parameters receive huge gradients. Others receive tiny gradients. SGD uses the same learning rate everywhere.

RMSProp's Idea: Every parameter gets its own learning rate.

- Large gradient → Reduce LR
- Small gradient → Increase LR

It keeps an exponential moving average of the squared gradients, telling it which parameters consistently receive large updates.

### 10.5 Adam

Adam combines the best ideas from Momentum and RMSProp.

| Component | Role | What it stores |
|-----------|------|----------------|
| $m_t$ (First moment) | Momentum | Average gradient (direction) |
| $v_t$ (Second moment) | RMSProp-style | Average squared gradient (magnitude) |

Analogy: Imagine driving.
- Momentum: Which direction have I been driving?
- RMSProp: Which roads are rough and should I slow down on?
- Adam: Uses both.

Why is Adam popular? Almost no tuning. Works immediately. Fast convergence. Excellent default optimizer.

### 10.6 AdamW

Problem in Adam: In Adam, each parameter has its own adaptive learning rate. When L2 regularization is added to the gradient, it also gets scaled by Adam's adaptive learning rates. So different parameters experience different effective amounts of weight decay. This is inconsistent.

AdamW Fix: Decouples weight decay from the gradient update.

Instead of mixing weight decay into the gradient:

Gradient + Weight Decay → Adam

AdamW does:

Gradient → Adam → Update → Weight Decay

Weight decay is applied as a separate step, making regularization behave consistently.

### 10.7 Optimizer Comparison Table

| Optimizer | Pros | Cons | Best For |
|-----------|------|------|----------|
| SGD | Simple, low memory, best generalization | Slow, oscillates, sensitive to LR | Large vision models after tuning |
| Momentum | Faster/smoother than SGD | One more hyperparameter | Most CNNs |
| Nesterov | Slightly faster than Momentum | Slightly more complex | Similar to Momentum |
| RMSProp | Handles different gradient scales | Can accumulate bias | RNNs, adaptive optimization |
| Adam | Fast, minimal tuning, robust | Can generalize worse, more memory | General DL, prototyping, NLP |
| AdamW | Adam + correct weight decay | Slightly more complex than Adam | Transformers, modern DL |

### 10.8 When to Use Which

| Situation | Best Choice | Why |
|-----------|-------------|-----|
| First experiment | Adam | Works well with little tuning |
| NLP / Transformers | Adam/AdamW | Handles sparse gradients, huge models |
| Small datasets | Adam | Faster convergence |
| Large CNNs (ResNet, ImageNet) | SGD + Momentum | Better generalization |
| Fastest convergence | Adam | Adaptive learning rates |
| Best final test accuracy | SGD | Often finds flatter minima |

Default Hyperparameters:

SGD:
- Learning rate: 0.01 (tune)
- Momentum: 0.9
- Weight decay: 1e-4

Adam:
- Learning rate: 1e-3
- β₁ = 0.9
- β₂ = 0.999
- ε = 1e-8

---

## 11. Adam: Where It Excels and Where It Fails

### 11.1 Where Adam Excels

1. Fast convergence: Adam reaches a good solution much faster than SGD. Epoch 1-2 with Adam already shows much lower loss.

2. NLP / Transformers: Transformer models (BERT, GPT, LLaMA) have sparse gradients, many parameters, and complex optimization. Adam/AdamW works extremely well.

3. Small datasets: With only 500 images, Adam adapts quickly while SGD may need lots of tuning.

4. Beginners / Research: If you don't know which optimizer to use, Adam is usually the first choice — it works well "out of the box."

### 11.2 Where Adam Fails

The problem: Adam often generalizes worse than SGD.

Why? Consider two types of minima:

Flat Minimum (SGD often finds this): \____/ - Many nearby weight values give low loss - Small weight changes → loss hardly changes - Better generalization Sharp Minimum (Adam often finds this): \/ - Only one tiny point gives low loss - Move slightly → loss increases rapidly - Worse generalization

SGD's noisy mini-batch updates help it escape sharp minima. Adam's adaptive updates are smoother and can settle into sharper minima.

| Metric | Adam | SGD |
|--------|------|-----|
| Training accuracy | 99% | 97% |
| Test accuracy | 90% | 94% |

This is why many ImageNet papers use SGD + Momentum instead of Adam.

### 11.3 Decision Guide

| Situation | Best Choice | Why |
|-----------|-------------|-----|
| First experiment | Adam | Works well with little tuning |
| NLP / Transformers | Adam/AdamW | Handles sparse gradients, huge models |
| Small datasets | Adam | Faster convergence |
| Large CNNs (ResNet, ImageNet) | SGD + Momentum | Better generalization |
| Need fastest convergence | Adam | Adaptive learning rates |
| Need best final test accuracy | SGD | Often finds flatter minima |

---

## 12. Adam: Update Equations & Bias Correction

### 12.1 The Two Memories

Adam stores two memories instead of one:

| Memory | Symbol | Stores | Purpose |
|--------|--------|--------|---------|
| First moment | $m_t$ | Average gradient | Direction |
| Second moment | $v_t$ | Average squared gradient | Magnitude |

### 12.2 Understanding $m_t$ (First Moment)

$$m_t = \beta_1 m_{t-1} + (1 - \beta_1) g_t$$

Intuition: Previous Memory + Current Gradient.

With β₁ = 0.9:

$$m_t = 0.9 \times \text{(previous)} + 0.1 \times \text{(current)}$$

We trust previous history more — only 10% comes from today's gradient. This smooths gradients, exactly like momentum.

### 12.3 Understanding $v_t$ (Second Moment)

$$v_t = \beta_2 v_{t-1} + (1 - \beta_2) g_t^2$$

Same idea, but storing the squared gradient.

Why square the gradients? To capture magnitude regardless of sign.

- Gradient = -10 → squared = 100
- Gradient = 10 → squared = 100

Both have the same magnitude. Parameters with consistently large gradients get reduced learning rates. Parameters with consistently small gradients get increased learning rates.

### 12.4 Why Bias Appears

Both $m_t$ and $v_t$ are initialized to zero because we know nothing at the start.

Example: Suppose the true average gradient is always 10.

| Iteration | Calculation | Result | True Average |
|-----------|------------|--------|--------------|
| 1 | $m_1 = 0.9(0) + 0.1(10)$ | 1 | 10 |
| 2 | $m_2 = 0.9(1) + 0.1(10)$ | 1.9 | 10 |
| 3 | $m_3 = 0.9(1.9) + 0.1(10)$ | 2.71 | 10 |

The average starts close to zero only because we initialized $m_0 = 0$. This is called bias toward zero.

### 12.5 Bias Correction

Adam compensates by dividing:

$$\hat{m}_t = \frac{m_t}{1 - \beta_1^t}$$

| Iteration | $m_t$ | $1 - \beta_1^t$ | $\hat{m}_t$ |
|-----------|-------|-----------------|-------------|
| 1 | 1 | $1 - 0.9 = 0.1$ | $1/0.1 = 10$ |
| 2 | 1.9 | $1 - 0.9^2 = 0.19$ | $1.9/0.19 = 10$ |

The bias correction completely removes the initialization bias. The corrected $\hat{m}_t$ gives the correct estimate from the first iteration.

Same for $v_t$:

$$\hat{v}_t = \frac{v_t}{1 - \beta_2^t}$$

Why two different betas?

| Parameter | Value | Meaning |
|-----------|-------|---------|
| β₁ | 0.9 | Remember 90% of previous gradients; forget 10% |
| β₂ | 0.999 | Squared gradients change more slowly, so remember 99.9% |

### 12.6 The Final Update Formula

$$\boxed{\theta_{t+1} = \theta_t - \eta \cdot \frac{\hat{m}_t}{\sqrt{\hat{v}_t} + \epsilon}}$$

Where does this come from?

1. Start with gradient descent: $\theta = \theta - \eta g$
2. Replace today's gradient $g$ with averaged gradient $m_t$ (Momentum): $\theta = \theta - \eta m_t$
3. Divide by $\sqrt{v_t}$ to adapt per-parameter learning rate (RMSProp): $\theta = \theta - \eta \frac{g}{\sqrt{v_t}}$
4. Combine both: $\theta = \theta - \eta \frac{m_t}{\sqrt{v_t}}$
5. Add bias correction: $\theta = \theta - \eta \frac{\hat{m}_t}{\sqrt{\hat{v}_t} + \epsilon}$

Why divide by $\sqrt{\hat{v}_t}$?

| Parameter | Gradient Magnitude | $v_t$ | $\sqrt{v_t}$ | Effective LR |
|-----------|-------------------|-------|--------------|--------------|
| A | ~100 | Large | Large | Small |
| B | ~0.01 | Small | Small | Large |

Large $v$ → Large denominator → Small update (slow down on rough roads). Small $v$ → Small denominator → Large update (speed up on smooth roads).

What is $\epsilon$ (epsilon)?

If $v = 0$, dividing by $\sqrt{v}$ crashes. $\epsilon = 10^{-8}$ is a tiny number added just enough to avoid division by zero.

### 12.7 Practical Notes

Typical defaults:
- β₁ = 0.9
- β₂ = 0.999
- ε = 1e-8
- Learning rate η = 1e-3

AdamW uses decoupled weight decay: Apply weight decay as a separate parameter update — do not add $\lambda w$ to the gradient.

Troubleshooting: Adam tends to converge faster but can generalize worse than SGD on some vision tasks. Try switching optimizers if final validation accuracy is unsatisfactory.

> Interview-ready explanation: "The moving averages $m_t$ and $v_t$ start at zero, so during the initial iterations they underestimate the true averages. Bias correction compensates for this initialization effect, preventing updates from being too small early in training."

---

## 13. Weight Decay vs L2 Regularization

Both have the same objective: prevent weights from becoming too large (reduce overfitting).

### 13.1 L2 Regularization

Modify the loss function:

$$L_{\text{new}} = L + \frac{\lambda}{2} ||w||^2$$

The optimizer doesn't know anything special — it simply computes the gradient of this new loss.

Example: Weight $w = 10$, data gradient $g = 2$, $\lambda = 0.1$

L2 gradient = $\lambda w = 0.1 \times 10 = 1$

Total gradient = $2 + 1 = 3$

SGD update: $10 - 0.1 \times 3 = 9.7$

Key point: We never directly shrank the weight. We only changed the gradient.

### 13.2 Weight Decay

Forget changing the loss. After every update, just shrink the weights:

Weight → Gradient Update → Multiply by (1 - ηλ)

Example: Weight = 10, gradient = 2

Gradient step: 10 → 9.8

Now shrink (ηλ = 0.01): $9.8 \times 0.99 = 9.702$

Key point: We directly reduced the weight. No extra gradient involved.

### 13.3 Why They Are Equivalent for SGD

L2 + SGD:
$$w = w - \eta(g + \lambda w)$$
$$w = w - \eta g - \eta \lambda w$$
$$w = (1 - \eta \lambda)w - \eta g$$

Weight Decay + SGD:
$$w = (1 - \eta \lambda)w - \eta g$$

Exactly the same. For SGD, L2 = Weight Decay.

### 13.4 Why Adam Breaks the Equivalence

Adam doesn't simply do Weight - LR × Gradient. It divides gradients by $\sqrt{v}$, giving each parameter a different effective learning rate.

Suppose:

| Parameter | Effective LR |
|-----------|-------------|
| A | 0.001 |
| B | 0.1 |

With L2, the regularization term $\lambda w$ is added to the gradient. That gradient also gets divided by $\sqrt{v}$.

- Parameter A gets tiny weight decay
- Parameter B gets much stronger weight decay

Even if both weights are exactly the same size — that's inconsistent.

Visual example:

| Parameter | Weight | Desired | L2 in Adam | What happens |
|-----------|--------|---------|------------|--------------|
| A | 10 | 9.9 | 9.99 | Barely shrunk |
| B | 10 | 9.9 | 9.80 | Too much shrinkage |

The effective shrinkage depends on the parameter's adaptive learning rate, not on the actual weight size.

### 13.5 AdamW Fix

AdamW separates the two jobs:

L2 inside Adam (broken):
Gradient + Regularization → Adam → Update
Both gradient and regularization are scaled adaptively.

AdamW (correct):
Gradient → Adam → Update → Shrink weights
The gradient is adaptive. The shrinkage is not.

Every parameter shrinks by exactly $(1 - \eta \lambda)$ — no adaptive scaling interfering with regularization.

> Interview answer: L2 regularization adds a penalty term to the loss, so its gradient $(\lambda w)$ is added to the data gradient. Weight decay directly shrinks the weights after each update. For vanilla SGD these are mathematically equivalent, but with adaptive optimizers like Adam they are no longer equivalent because the regularization gradient is also scaled by Adam's adaptive learning rates. AdamW fixes this by applying weight decay separately from the gradient update.

---

## Appendix A: Interview-Ready Summaries

Spatial Equivariance:
> Spatial equivariance means that if an object in the input image shifts, the corresponding activation in the feature map shifts by the same amount. This happens because CNNs use the same convolution kernel at every spatial location (weight sharing).

Equivariance vs Invariance:
> Convolution is translation equivariant (output shifts when input shifts). Pooling introduces translation invariance (small shifts don't significantly change the final prediction).

CNN Backprop:
> "Every convolution layer computes two gradients during backprop: one for the filter (to update the filter weights) and one for the input (to propagate the error to earlier layers)."

Batch Normalization:
> "Batch Normalization normalizes activations within each mini-batch to have approximately zero mean and unit variance, then applies learnable scale (γ) and shift (β). It stabilizes training, allows higher learning rates, improves gradient flow, and often provides mild regularization."

Internal Covariate Shift:
> "Internal Covariate Shift refers to the changing distribution of activations inside a neural network during training because earlier layers continuously update their weights."

γ and β:
> "BatchNorm normalizes activations to zero mean and unit variance, but that may not be the optimal distribution for every layer. The learnable parameters γ (scale) and β (shift) allow the network to recover any useful distribution while still benefiting from stable normalization."

Dropout:
> "Dropout randomly deactivates a fraction of neurons during training, forcing the network to learn redundant and robust feature representations instead of relying on a few neurons."

Inverted Dropout:
> "Inverted Dropout scales the activations of the neurons that remain during training by 1/keep_probability, so the expected activation is the same during training and inference."

Momentum:
> "Momentum accumulates previous gradients, helping accelerate learning in consistent directions while reducing oscillations."

Adam vs SGD:
> "Adam converges faster due to adaptive learning rates but can generalize worse. SGD with momentum converges slower but often finds flatter minima with better test accuracy."

AdamW:
> "AdamW applies weight decay separately from the gradient update, so adaptive learning rates only affect optimization while weight decay consistently shrinks all weights."

Bias Correction (Adam):
> "The moving averages m_t and v_t start at zero, so they are biased toward zero during the first few iterations. Bias correction compensates for this startup bias, preventing updates from being artificially small early in training."

Weight Decay vs L2:
> "For SGD, L2 regularization and weight decay are equivalent. For adaptive optimizers like Adam, they diverge because the regularization gradient gets scaled by adaptive learning rates. AdamW fixes this by decoupling weight decay."

Gradient Clipping:
> "Gradient clipping limits the size of the gradient update while preserving the optimization direction (with norm clipping), preventing exploding gradients and unstable training."

Debugging a non-training model:
> "First overfit 100 samples, then check LR, initialization, data pipeline, gradient norms, and finally model capacity."

---

## Appendix B: One-Line Memory Tricks

| Concept | Memory Trick |
|---------|--------------|
| Equivariance | "Object moves → feature map moves" |
| Invariance | "Object moves → prediction stays the same" |
| CNN Backprop | Every layer asks: (1) How should my filter change? (2) What error to send backward? |
| BatchNorm | "Normalize the activations so every layer learns from stable inputs" |
| Dropout | "Randomly hide some neurons so the network doesn't rely too much on any single one" |
| Internal Covariate Shift | "Layers keep seeing changing input distributions" |
| γ (Gamma) | "Controls the spread (contrast) of normalized activations" |
| β (Beta) | "Moves the normalized activations up or down (offset)" |
| Inverted Dropout | "Scale during training so inference requires no changes" |
| Step LR | "Take big steps early, small steps later" |
| Early Stopping | "Stop when validation gets worse" |
| Data Augmentation | "Create more diverse training examples without collecting new data" |
| SGD | "Uses today's gradient" |
| Momentum | "Uses today's gradient + remembers yesterday" |
| Nesterov | "Looks ahead before updating" |
| RMSProp | "Adjusts learning rates based on gradient magnitudes" |
| Adam | "Momentum + RMSProp together" |
| AdamW | "Adam with properly separated weight decay (standard for modern Transformers)" |
| L2 Regularization | "Change the loss function" |
| Weight Decay | "Shrink the weights directly" |
| Gradient Clipping | "Same direction, slower speed" |

---
