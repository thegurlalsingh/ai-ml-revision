AI/ML Interview & Implementation Guide

A comprehensive reference for Transformer architecture, LLM training, fine-tuning, evaluation, and Retrieval-Augmented Generation (RAG) — built for interview preparation and practical implementation.

Table of Contents

- [1. Practical Pitfalls & Debugging Tips](#1-practical-pitfalls--debugging-tips)
  - [1.1 Softmax Overflow / Underflow](#11-softmax-overflow--underflow)
  - [1.2 Mask Broadcasting Errors](#12-mask-broadcasting-errors)
  - [1.3 Padding Leakage](#13-padding-leakage)
  - [1.4 Training Instability at the Beginning](#14-training-instability-at-the-beginning)
  - [1.5 Sampling Pitfalls](#15-sampling-pitfalls)
- [2. Optimization Techniques](#2-optimization-techniques)
  - [2.1 Mixed Precision (AMP)](#21-mixed-precision-amp)
  - [2.2 Gradient Accumulation](#22-gradient-accumulation)
  - [2.3 Activation Checkpointing](#23-activation-checkpointing)
  - [2.4 FlashAttention](#24-flashattention)
  - [2.5 Fused QKV Projection](#25-fused-qkv-projection)
  - [2.6 Weight Tying](#26-weight-tying)
- [3. Long Context Methods](#3-long-context-methods)
  - [3.1 Sliding Window Attention](#31-sliding-window-attention)
  - [3.2 RoPE (Rotary Positional Embedding)](#32-rope-rotary-positional-embedding)
  - [3.3 Retrieval (RAG)](#33-retrieval-rag)
- [4. Tokenizer Comparison](#4-tokenizer-comparison)
- [5. Pretraining Objectives](#5-pretraining-objectives)
  - [5.1 Autoregressive Language Model (GPT-family)](#51-autoregressive-language-model-gpt-family)
  - [5.2 Masked Language Modeling (BERT)](#52-masked-language-modeling-bert)
  - [5.3 Denoising Objectives (T5)](#53-denoising-objectives-t5)
  - [5.4 Contrastive Learning (CLIP)](#54-contrastive-learning-clip)
- [6. Tradeoffs Between Pretraining Objectives](#6-tradeoffs-between-pretraining-objectives)
  - [6.1 Why Causal LMs are Naturally Good at Generation](#61-why-causal-lms-are-naturally-good-at-generation)
  - [6.2 Why MLMs are Stronger Encoders](#62-why-mlms-are-stronger-encoders)
  - [6.3 Why Denoising (T5) Generalizes Well to Seq2Seq](#63-why-denoising-t5-generalizes-well-to-seq2seq)
  - [6.4 Training Objective Affects Sample Quality](#64-training-objective-affects-sample-quality)
  - [6.5 Zero-shot / Few-shot Ability](#65-zero-shot--few-shot-ability)
  - [6.6 Sample Diversity](#66-sample-diversity)
  - [6.7 Final Comparison Table](#67-final-comparison-table)
- [7. Teacher Forcing & Exposure Bias](#7-teacher-forcing--exposure-bias)
  - [7.1 Why We Need Teacher Forcing](#71-why-we-need-teacher-forcing)
  - [7.2 Training Example](#72-training-example)
  - [7.3 What Happens During Inference](#73-what-happens-during-inference)
  - [7.4 Why Exposure Bias Happens](#74-why-exposure-bias-happens)
  - [7.5 The Probability Explanation](#75-the-probability-explanation)
  - [7.6 Error Compounding](#76-error-compounding)
  - [7.7 Toy Math Example](#77-toy-math-example)
  - [7.8 How to Reduce Exposure Bias](#78-how-to-reduce-exposure-bias)
  - [7.9 Complete Picture](#79-complete-picture)
- [8. Scaling Laws & Tradeoffs](#8-scaling-laws--tradeoffs)
  - [8.1 Why We Care About Scaling](#81-why-we-care-about-scaling)
  - [8.2 What Are Scaling Laws](#82-what-are-scaling-laws)
  - [8.3 The Formula](#83-the-formula)
  - [8.4 Diminishing Returns](#84-diminishing-returns)
  - [8.5 Why Can't We Just Make Infinite Models](#85-why-cant-we-just-make-infinite-models)
  - [8.6 Tradeoff 1: Bigger Model Needs More Data](#86-tradeoff-1-bigger-model-needs-more-data)
  - [8.7 Tradeoff 2: Undertrained Large Models](#87-tradeoff-2-undertrained-large-models)
  - [8.8 Tradeoff 3: Compute Budget](#88-tradeoff-3-compute-budget)
- [9. Data Preparation & Tokenization](#9-data-preparation--tokenization)
  - [9.1 Raw Dataset](#91-raw-dataset)
  - [9.2 Dataset Format](#92-dataset-format)
  - [9.3 Why Tokenization](#93-why-tokenization)
  - [9.4 Why Use the Same Tokenizer](#94-why-use-the-same-tokenizer)
  - [9.5 Truncation](#95-truncation)
  - [9.6 Max Length](#96-max-length)
  - [9.7 Labels for Causal LM](#97-labels-for-causal-lm)
  - [9.8 Prompt + Answer Fine-tuning](#98-prompt--answer-fine-tuning)
  - [9.9 Ignore Index](#99-ignore-index)
  - [9.10 Why Prompt Templates](#910-why-prompt-templates)
  - [9.11 Why This Is Especially Useful for Small Datasets](#911-why-this-is-especially-useful-for-small-datasets)
  - [9.12 Complete Pipeline](#912-complete-pipeline)
- [10. Fine-tuning Options](#10-fine-tuning-options)
  - [10.1 What is Fine-tuning](#101-what-is-fine-tuning)
  - [10.2 Two Ways to Fine-tune](#102-two-ways-to-fine-tune)
  - [10.3 Full Fine-tuning via Trainer](#103-full-fine-tuning-via-trainer)
  - [10.4 Parameter-Efficient Fine-tuning (PEFT) / LoRA](#104-parameter-efficient-fine-tuning-peft--lora)
  - [10.5 Hyperparameters Explained](#105-hyperparameters-explained)
  - [10.6 Full Fine-tuning vs LoRA Comparison](#106-full-fine-tuning-vs-lora-comparison)
- [11. Evaluation Metrics](#11-evaluation-metrics)
  - [11.1 Perplexity](#111-perplexity)
  - [11.2 Exact Match (EM)](#112-exact-match-em)
  - [11.3 F1 Score (for QA)](#113-f1-score-for-qa)
  - [11.4 BLEU](#114-bleu)
  - [11.5 ROUGE](#115-rouge)
  - [11.6 Why Not Use Accuracy for LLMs](#116-why-not-use-accuracy-for-llms)
  - [11.7 Human Evaluation](#117-human-evaluation)
  - [11.8 Why Automatic Metrics Can Be Misleading](#118-why-automatic-metrics-can-be-misleading)
  - [11.9 Logging](#119-logging)
- [12. Prompt Templates & Inference](#12-prompt-templates--inference)
  - [12.1 Prompt Template](#121-prompt-template)
  - [12.2 Few-shot Prompting](#122-few-shot-prompting)
  - [12.3 Zero-shot vs One-shot vs Few-shot](#123-zero-shot-vs-one-shot-vs-few-shot)
  - [12.4 Instruction Tuning Format](#124-instruction-tuning-format)
  - [12.5 Inference](#125-inference)
  - [12.6 Model Generation Parameters](#126-model-generation-parameters)
  - [12.7 Demo Script](#127-demo-script)
  - [12.8 What About Probabilities](#128-what-about-probabilities)
- [13. Sampling Strategies & Repetition](#13-sampling-strategies--repetition)
  - [13.1 The Repetition Problem](#131-the-repetition-problem)
  - [13.2 How to Prevent Repetitive Answers](#132-how-to-prevent-repetitive-answers)
- [14. Building a Simple RAG Pipeline](#14-building-a-simple-rag-pipeline)
  - [14.1 What is RAG](#141-what-is-rag)
  - [14.2 Complete RAG Pipeline Overview](#142-complete-rag-pipeline-overview)
  - [14.3 Step 1: Chunking](#143-step-1-chunking)
  - [14.4 Step 2: Embeddings](#144-step-2-embeddings)
  - [14.5 Step 3: FAISS (Vector Database)](#145-step-3-faiss-vector-database)
  - [14.6 Step 4: Retrieval](#146-step-4-retrieval)
  - [14.7 Step 5: Prompt Construction](#147-step-5-prompt-construction)
  - [14.8 Complete RAG Pipeline Flow](#148-complete-rag-pipeline-flow)
- [15. Quick Interview Cheat Sheet](#15-quick-interview-cheat-sheet)

---

1. Practical Pitfalls & Debugging Tips

1.1 Softmax Overflow / Underflow

Problem

Softmax computes:

$$e^x$$

Suppose logits are `[1000, 999, 998]`. Then `e^1000` is astronomically large and overflows to ∞. Similarly, `e^-1000` becomes almost 0 (underflow).

Solution

Subtract the maximum logit before applying softmax.

Instead of `[1000, 999, 998]`, compute:

max = 1000

↓

[0, -1, -2]

Now:
- `e^0 = 1`
- `e^-1 ≈ 0.37`
- `e^-2 ≈ 0.14`

No overflow occurs.

> Important: Softmax doesn't change because subtracting the same constant from every logit cancels out in the normalization step.

Interview Answer

> Before computing softmax, subtract the maximum logit to avoid numerical overflow while keeping the output probabilities unchanged.

1.2 Mask Broadcasting Errors

Problem

Suppose:
- Batch size = 2
- Heads = 8
- Sequence length = 64

Attention scores have shape `(batch, heads, seq, seq)` → `(2, 8, 64, 64)`

But your mask has shape `(64, 64)` or `(2, 64)`. PyTorch may broadcast it incorrectly.

Result: Some future tokens may not actually be masked. The model starts cheating during training.

Always check: Mask shape matches the attention scores after broadcasting.

Interview Answer

> Incorrect mask shapes can broadcast incorrectly, causing the model to attend to future or padding tokens. Always verify mask dimensions before applying them.

1.3 Padding Leakage

Problem

Consider: `I love AI PAD PAD`

Without a padding mask, attention may look at `PAD`, which has no meaning. Even worse, if `PAD` contributes to the loss, the model starts learning to predict `PAD`.

Fix
- Use a padding mask in attention.
- Use `ignore_index=PAD` in `CrossEntropyLoss`.

This ensures PAD neither influences attention nor the loss.

Interview Answer

> Padding tokens should be ignored both in attention (using a padding mask) and in the loss (using `ignore_index`) so they don't affect training.

1.4 Training Instability at the Beginning

Observed behavior:

Loss

1.2
 15
 300
 NaN

or

Loss

2
 2
 2
 2

Common reasons:
- Learning rate too high
- Poor weight initialization
- Exploding gradients

Fixes:
- Smaller learning rate
- Learning-rate warmup
- Gradient clipping
- Proper initialization (He / Xavier)

Interview Answer

> Early instability is usually caused by overly large updates. Warmup, gradient clipping, and proper initialization help stabilize training.

1.5 Sampling Pitfalls

Problem

Suppose the model predicts: `I love AI because AI because AI because AI...`

Why? Because greedy decoding always picks the highest-probability token. It gets stuck in loops.

Better sampling methods:

| Method | Description |
|--------|-------------|
| Temperature | Makes probabilities sharper or flatter. Higher temperature = more randomness. |
| Top-k | Choose randomly among the top k most likely tokens. |
| Top-p (Nucleus) | Choose from the smallest set of tokens whose cumulative probability reaches p. |

These methods make generated text more diverse and natural.

Interview Answer

> Greedy decoding often produces repetitive text. Temperature, top-k, and top-p sampling introduce controlled randomness, improving diversity while maintaining coherence.

Quick Debugging Cheat Sheet

| Problem | Cause | Fix |
|---------|-------|-----|
| Softmax overflow | Large logits cause exp() overflow | Subtract the maximum logit before softmax |
| Mask broadcasting error | Wrong mask shape | Ensure mask broadcasts correctly to attention scores |
| Padding leakage | PAD tokens influence attention/loss | Use a padding mask and `ignore_index=PAD` |
| Training unstable | High LR, bad initialization, exploding gradients | Warmup, lower LR, gradient clipping, He/Xavier initialization |
| Repetitive generation | Greedy decoding always picks the highest-probability token | Use temperature, top-k, or top-p sampling |

---

2. Optimization Techniques

2.1 Mixed Precision (AMP)

Background: What is FP32 and FP16?

Computers store decimal numbers in memory using a binary format called floating point. There are different precisions:

- FP32 (32 bits): Uses 32 bits to store one number. Very accurate but needs more memory.
- FP16 (16 bits): Uses only 16 bits. Less accurate but takes half the memory.

Why does memory matter?

Suppose your neural network has 100 million numbers:
- FP32 (4 bytes each) → 400 MB
- FP16 (2 bytes each) → 200 MB (half the memory)

Why faster?

Modern NVIDIA GPUs have special hardware called Tensor Cores designed specifically for FP16/BF16 operations. FP16 allows the GPU to process more numbers simultaneously, making training faster.

But won't accuracy decrease?

A little. So frameworks like PyTorch automatically mix precisions:
- Operations that need high precision → FP32
- Everything else → FP16

This is called Automatic Mixed Precision (AMP).

Interview Answer

> Mixed precision uses FP16 where possible to reduce memory and speed up training while keeping important calculations in FP32 to maintain accuracy.

2.2 Gradient Accumulation

Background

Normally with batch size = 64:
64 images → Forward → Backward → Update weights

But if your GPU can only hold 16 images, you can't fit the full batch. Instead:
16 → Compute gradient → Store it
16 → Compute gradient → Add to previous
16 → Compute gradient → Add to previous
16 → Compute gradient → Add to previous
                              ↓
                        Update once

Now `16 × 4 = 64` — the model behaves almost like it trained on batch size 64.

Why useful?

GPU memory is limited. Gradient accumulation lets you pretend your GPU is bigger.

Interview Answer

> Gradient accumulation simulates a larger batch size by accumulating gradients across several mini-batches before updating the weights.

2.3 Activation Checkpointing

Background

During the forward pass, each layer produces an output called an activation. These activations are needed during backpropagation to compute gradients.

Normally: Every activation is stored → large memory usage for deep models.

Checkpointing says: Store only a few activations. During backpropagation, recompute the missing ones.

Result: Memory ↓, Computation ↑

Analogy

Imagine solving a 100-step math problem. Instead of saving every step, save only Step 1, Step 50, and Step 100. If someone asks "What happened at step 40?" — just recompute.

Interview Answer

> Activation checkpointing saves memory by storing fewer intermediate activations and recomputing them during backpropagation.

2.4 FlashAttention

Background

Suppose a sentence has 1000 words. Attention compares every word with every other word — 1000 × 1000 = 1 million comparisons — stored in a 1000×1000 matrix. Very large.

FlashAttention computes attention in small blocks (tiles) instead of storing the full matrix:
100×100 → Throw away → Next 100×100 → Throw away → ...

Same mathematical result. Much less memory. Faster.

Interview Answer

> FlashAttention computes attention in small blocks instead of storing the full attention matrix, making it much faster and more memory efficient.

2.5 Fused QKV Projection

Background

Normally:
x → Linear → Q
x → Linear → K
x → Linear → V

Three separate matrix multiplications.

Fused QKV computes them together:
x → One large Linear → [Q, K, V] → Split

Same output. Less overhead. Faster.

Interview Answer

> Fused QKV computes queries, keys, and values together in one matrix multiplication, reducing computation and improving efficiency.

2.6 Weight Tying

Background

Input sentence: `I love AI`

First, words are converted into vectors using an embedding matrix:
love → [0.2, 0.5, 1.3]

At the end, the model has a vector and must convert it back into vocabulary probabilities using another matrix:
Vector → Scores for all words

Normally these are two huge matrices. Weight tying says: use the same matrix. The output layer uses the transpose of the embedding matrix.

Why? Fewer parameters. Less memory. Often slightly better generalization.

Interview Answer

> Weight tying shares the input embedding matrix with the output projection layer, reducing parameters and improving generalization.

---

3. Long Context Methods

Attention cost is O(n²). If sequence length doubles, attention becomes roughly 4× more expensive.

3.1 Sliding Window Attention

Instead of having every token attend to every other token, each token attends only to nearby tokens.

Analogy: Instead of "everyone talks to everyone," it's "each person talks only to nearby people."

This reduces attention cost significantly for long sequences.

3.2 RoPE (Rotary Positional Embedding)

A better way of encoding position information that helps models generalize to longer contexts. RoPE provides position information in a way that works even for text longer than what the model saw during training.

3.3 Retrieval (RAG)

Instead of putting the entire book into the model's context, retrieve only the relevant pages. Used in Retrieval-Augmented Generation (RAG).

Analogy: Instead of reading the entire Wikipedia, search first and bring only the relevant paragraphs.

---

4. Tokenizer Comparison

Suppose the sentence is: `Unfortunately, transformers are amazing.`

Different tokenizers produce different splits:
- BPE: `Un fortunately , transform ers ...`
- SentencePiece: May produce different subwords

Key comparison criteria:

| Criterion | Description | Preference |
|-----------|-------------|------------|
| Number of tokens | How many tokens the sentence is split into | Smaller is usually better (shorter sequence → faster Transformer) |
| Token length distribution | Are tokens mostly 2 characters? 5 characters? Whole words? | Balanced distribution |
| Unknown token rate | How often does the tokenizer produce `<UNK>` | Lower is better (modern tokenizers usually have very low unknown rates) |

Modern subword tokenizers avoid unknown words by splitting unfamiliar text into known subword pieces. For example, `ChatGPTX2026` becomes `Chat | GPT | X | 2026` instead of `<UNK>`.

---

5. Pretraining Objectives

5.1 Autoregressive Language Model (GPT-family)

Task: Predict the next word.

I love _ → AI
I love AI _ → because
I love AI because __ → it

Formula:

$$\sumt \log P(xt | x_{<t})$$

This means: sum the probability of predicting the correct next token at every position.

Teacher Forcing: During training, the model always receives the actual previous word, not its own prediction.

I → love → AI    (correct, using teacher forcing)

Not:
I → love → robot (wrong, model's own prediction)

Used by: GPT, LLaMA, Gemini, Claude

Strengths: Excellent for text generation, chatbots, story writing, code generation.

5.2 Masked Language Modeling (BERT)

Instead of predicting the next word, hide some words and predict them from full context.

I [MASK] AI → predict "love"
Paris is the capital of [MASK] → predict "France"

The model can look both left and right — bidirectional context.

Used by: BERT, RoBERTa, ALBERT

Strengths: Excellent for classification, sentiment analysis, question answering, search, text embeddings.

Weakness: Not naturally good at generating long text because it never learned to generate one word after another during training.

5.3 Denoising Objectives (T5)

Instead of masking one word, remove entire chunks and reconstruct them.

Original:     I love studying artificial intelligence.
Corrupted:    I love <extraid0> .
Target:       <extraid0> studying artificial intelligence.

Harder than MLM. The model learns both understanding and generation at the same time.

Used by: T5, FLAN-T5

Strengths: Very good for translation, summarization, question answering, text generation.

5.4 Contrastive Learning (CLIP)

Instead of predicting words, learn whether two things belong together.

🐶 → "A dog"    → Correct pair
🐶 → "A car"    → Wrong pair

The model learns: Dog image ↔ Dog text, Car image ↔ Car text.

Used by: CLIP, ALIGN

Strengths: Learns powerful representations for image search, image-text retrieval, multimodal AI.

---

6. Tradeoffs Between Pretraining Objectives

6.1 Why Causal LMs are Naturally Good at Generation

GPT is trained by always predicting the next token. During inference, the process is identical:

User types: "Once upon a time"
GPT: Predict next word → Append it → Predict next word → Append it → Repeat

This is exactly the same process it practiced during training. So generation is straightforward.

Why isn't BERT naturally good at generation?

BERT was trained to fill in masked words. It never learned:
Generate next word → Generate next word again → Continue forever.

If you ask BERT to write a story, it has no experience doing so. It needs tricks like masked infilling or being placed inside a seq2seq architecture.

> Student A (GPT): Homework every day = "Continue this paragraph." After millions of examples, becomes a fantastic writer.
>
> Student B (BERT): Homework every day = "Fill in the blank." Becomes great at understanding context but never practices writing long passages.

6.2 Why MLMs are Stronger Encoders

GPT — when predicting a word, can only see the left context (previous words).

BERT — when predicting a masked word, can see both left and right context.

The movie was [MASK] because everyone clapped.

To predict "amazing," BERT uses:
- Left context: "The movie was"
- Right context: "because everyone clapped"

This builds a much richer sentence understanding. That's why BERT embeddings are usually stronger for tasks like classification, search, embeddings, and sentiment analysis.

6.3 Why Denoising (T5) Generalizes Well to Seq2Seq

In T5, input ≠ output:

Input:  The <extraid0> on the mat.
Output: cat sat

The model learns: Read one sequence → Generate another sequence. This is exactly what happens in:
- Translation (English → French)
- Summarization (Long article → Short summary)
- Question Answering (Question → Answer)
- Grammar correction (Wrong sentence → Correct sentence)

All are input sequence → output sequence. T5 naturally fits all these tasks.

Why GPT is less natural for translation: It mostly learned to predict the next token, not to read one sequence and generate a different one. GPT can still do it, but T5 typically needs less fine-tuning.

6.4 Training Objective Affects Sample Quality

Sample quality refers to how good the generated text is.

- Prompt: `"Write a poem."`
- Good sample: `"Roses bloom beneath the sky..."`
- Bad sample: `"Rose rose rose rose sky sky..."`

GPT spends all its training generating text, so sample quality is usually excellent.

6.5 Zero-shot / Few-shot Ability

- Zero-shot: Never trained for the task. GPT often succeeds because next-token prediction on massive internet data teaches many patterns.
- Few-shot: Provide a few examples:

English -> French
Dog -> Chien
Cat -> Chat
House ->

GPT completes: `Maison`

BERT cannot do this naturally because it isn't a generative model.

6.6 Sample Diversity

GPT can generate different continuations (joke A, joke B, joke C) because it predicts one token at a time and can use temperature, top-k, and top-p sampling.

BERT predicts masked tokens, not whole continuations, so diversity is much more limited for open-ended text generation.

6.7 Final Comparison Table

| Property | GPT (Causal LM) | BERT (MLM) | T5 (Denoising) |
|----------|----------------|------------|----------------|
| Training | Predict next token | Predict masked token | Reconstruct corrupted text |
| Understands context | Only left context | Left + right context | Full input |
| Text generation | ⭐ Excellent | ❌ Not natural | ⭐ Excellent |
| Sentence understanding | Good | ⭐ Excellent | ⭐ Excellent |
| Translation | Possible | Poor | ⭐ Excellent |
| Summarization | Good | Poor | ⭐ Excellent |
| Embeddings / Search | Good | ⭐ Excellent | Good |
| Zero/Few-shot generation | ⭐ Strong | Weak | Good |

Interview Answer

> GPT is trained exactly the way it generates text — predicting the next token repeatedly — so inference matches training. BERT is trained to fill masked words using both left and right context, making it excellent at understanding text but not naturally suited for generating long sequences. T5 sits in between by learning to reconstruct corrupted text, so it naturally handles sequence-to-sequence tasks like translation and summarization.

---

7. Teacher Forcing & Exposure Bias

7.1 Why We Need Teacher Forcing

Consider sentence: `I love AI because it is amazing.`

Normal training:
Input:    I
Target:   love

Input:    I love
Target:   AI

Input:    I love AI
Target:   because

When predicting `AI`, the model is given `I love` — which is correct. It never sees its own mistakes. This is called Teacher Forcing.

> Why "Teacher"? Imagine a math student: `2 + 2 = ?` Student says `5`. Teacher immediately says "No. Correct answer is 4. Now solve the next question." The student always continues using the correct answer, not their own wrong one.

7.2 Training Example

For sentence: `I love AI because it helps.`

| Input | Target |
|-------|--------|
| I | love |
| I love | AI |
| I love AI | because |
| I love AI because | it |
| I love AI because it | helps |

Every input contains the correct previous words.

7.3 What Happens During Inference

During inference, there is no teacher. The model uses its own previous predictions.

If it makes a mistake:
Input:    I
Predicts: eat     (instead of "love")

Input:    I eat   ← This context was NEVER seen during training
Predicts: pizza

The model must continue from contexts it never practiced — this is much harder.

7.4 Why Exposure Bias Happens

This is the core idea:

- During training: Model always sees correct sentences → correct sentences → correct sentences
- During inference: Model sees correct → small mistake → wrong context → more mistakes → even worse context

The model is being exposed to situations it never saw during training. Hence the name: Exposure Bias.

> Real-life analogy: Learning to drive with an instructor who always grabs the steering wheel before you make a mistake. Every road you experience is perfect. Then you drive alone, accidentally turn left instead of right, end up on a road you've never seen, and become confused — one mistake creates more mistakes.

7.5 The Probability Explanation

During training, the model learns:

$$P(xt \mid x{<t}^*)$$

Where:
- $xt$ = current word (e.g., "AI")
- $x{<t}$ = previous words (e.g., "I love")
- $*$ = ground truth / correct sentence

So it learns: "Predict the next word assuming all previous words are correct."

During inference, there is no ground truth. Previous words are the model's own predictions (perhaps "I eat" instead of "I love"). The model was never trained on these incorrect contexts.

The distribution mismatch:

$$KL(P{data} \mid\mid P{model})$$

This measures how different the training contexts are from inference contexts. The larger the difference, the larger the exposure bias. (You don't need to derive KL divergence in an interview — just know it measures the mismatch.)

7.6 Error Compounding

Consider sentence: `I love AI because it helps students.`

| Step | Correct | If Model Makes a Mistake |
|------|---------|--------------------------|
| 1 | I → love | I → eat |
| 2 | I love → AI | I eat → pizza |
| 3 | I love AI → because | I eat pizza → every |

The sentence becomes "I eat pizza every..." — one mistake completely changed the topic. This is Error Compounding.

7.7 Toy Math Example

Suppose the first prediction has a 10% error rate:

$$\varepsilon = 0.1$$

That means 90% of the time, step 2 gets the correct input. 10% of the time, step 2 gets the wrong input.

Suppose if step 2 gets the wrong input, it makes another mistake 40% of the time:

$$\delta = 0.4$$

The approximate error at step 2 is:

$$\varepsilon + (1-\varepsilon)\delta$$

$$0.1 + (0.9)(0.4) = 0.1 + 0.36 = 0.46$$

Almost 46% error, starting from only 10%. This shows how errors can snowball. The exact numbers are just for intuition — the key idea is that mistakes early in the sequence make later mistakes much more likely.

7.8 How to Reduce Exposure Bias

1. Scheduled Sampling ⭐

Instead of always giving the correct previous word, sometimes use the ground truth, sometimes use the model's own prediction. This teaches the model to recover from mistakes.

Instead of:        I love AI
Sometimes train:   I eat AI

2. Data Augmentation

Purposely create corrupted sentences. Train the model to continue even after mistakes.

Original:    I love AI.
Also train:  I love robot.

3. Sequence-Level Training

Instead of calculating loss word by word, evaluate the entire sentence. Good sentence → small loss. Bad sentence → large loss. Methods like reinforcement learning or minimum-risk training fall into this category.

4. Self-Training

Generate text using the model itself, then train again on those generated outputs. The model becomes familiar with its own prediction style, including mistakes.

5. Beam Search

Instead of keeping only one prediction, keep several promising candidates.

Instead of:    love
Keep:          love | like | adore

Continue all three. If one path becomes bad, another may still produce a good sentence. Beam search reduces the chance that one early greedy mistake ruins the whole generation.

7.9 Complete Picture

TRAINING
    Teacher gives correct previous word
                 ↓
      Model only sees perfect contexts
                 ↓
        Learns next-word prediction

--------------------------------------

INFERENCE
          Model predicts word itself
                 ↓
          Prediction may be wrong
                 ↓
             Wrong context
                 ↓
      Next prediction becomes harder
                 ↓
            More mistakes
                 ↓
          Errors compound

Interview Cheat Sheet

| Concept | Simple Explanation |
|---------|-------------------|
| Teacher Forcing | During training, the model always receives the correct previous tokens. |
| Inference | The model must use its own previous predictions. |
| Exposure Bias | The model is exposed to incorrect contexts at inference that it never saw during training. |
| Error Compounding | One wrong prediction changes the context, making future mistakes more likely. |
| Scheduled Sampling | Mix ground-truth and model predictions during training to reduce exposure bias. |
| Beam Search | Keep multiple candidate sequences during decoding so one early mistake doesn't necessarily ruin the output. |

One-line interview answer:

> Teacher forcing trains the model using the correct previous tokens, but during inference the model must rely on its own predictions. This mismatch causes exposure bias: an early mistake changes the context for later predictions, so errors can accumulate over time.

---

8. Scaling Laws & Tradeoffs

8.1 Why We Care About Scaling

Suppose you trained a small model and got 85% accuracy. You ask:
- "If I make the model twice as big, what happens?"
- "Should I use more data instead?"
- "Should I train for more epochs?"

Scaling laws try to answer these questions.

8.2 What Are Scaling Laws

Researchers (OpenAI, DeepMind) observed something interesting. If you increase model size, training data, or compute, the model usually improves in a predictable way — not randomly. This relationship is called a scaling law.

> Think of growing a child: 1 hour/day → 70 marks. 2 hours/day → 75 marks. 4 hours/day → 80 marks. 8 hours/day → 84 marks. More studying helps, but each extra hour gives less improvement. Exactly the same happens with LLMs.

8.3 The Formula

$$Loss \propto N^\alpha C^\beta D^\gamma$$

| Symbol | Meaning |
|--------|---------|
| N | Number of parameters (model size) |
| D | Dataset size (number of training tokens/examples) |
| C | Compute (GPU work used during training) |

The formula simply says: Loss depends on model size, data size, and compute.

8.4 Diminishing Returns

This is the most important idea.

| Model Size | Performance | Improvement |
|------------|-------------|-------------|
| 100M | 70% | — |
| 1B | 82% | +12% |
| 10B | 88% | +6% |
| 100B | 90% | +2% |

Each increase helps, but less than before. This is called Diminishing Returns.

> Real-life analogy: Watering a plant. First glass → huge improvement. Second glass → still helpful. Tenth glass → almost no difference.

8.5 Why Can't We Just Make Infinite Models?

Large models need:
- More memory
- More GPUs
- More electricity
- More data

Otherwise, they don't learn properly.

8.6 Tradeoff 1: Bigger Model Needs More Data

> Student A (brain capacity: 10 GB) reads 100 books → learns a lot.
>
> Student B (brain capacity: 1000 GB) reads 2 books → most of brain remains unused.

Same for AI. A huge model with a tiny dataset will memorize the data (overfit) instead of learning general patterns.

8.7 Tradeoff 2: Undertrained Large Models

| Model | Size | Training | Performance |
|-------|------|----------|-------------|
| A | 500M parameters | Trained completely | ✅ Good |
| B | 10B parameters | Trained only halfway | ❌ Often worse |

The larger model never got enough training. A smaller, well-trained model often outperforms it.

> Analogy: Student A (average IQ, studied 12 months) vs. Student B (genius, studied 2 days). Usually Student A scores better.

8.8 Tradeoff 3: Compute Budget

Suppose your company gives $1000 for training. Two choices:
- Option 1: Huge model (70B), but only 1 epoch
- Option 2: Smaller model (7B), train 10 epochs

Option 2 often performs better because it is well-trained. Compute budget determines the best model size.

Scaling laws help answer: With 100 GPU hours, should you train a huge model with few updates or a medium model with many updates?

Why OpenAI doesn't just build infinite models: A 1-trillion-parameter model needs enormous data, compute, and memory. Without enough data, it won't outperform a smaller, properly trained model. Companies must balance model size, data, and compute.

Interview Cheat Sheet

| Concept | Simple Meaning |
|---------|---------------|
| Parameters (N) | Model size (how much it can learn) |
| Data (D) | Number of training tokens/examples |
| Compute (C) | GPU work used for training |
| Scaling Law | Bigger model + more data + more compute → better performance in a predictable way |
| Diminishing Returns | Each additional increase gives a smaller improvement than the previous one |
| Undertrained Large Model | A huge model trained on too little data or too few steps can perform worse than a smaller, well-trained model |
| Compute Budget | With limited GPU resources, you must balance model size and training time instead of maximizing only one |

Interview questions:

> Q: Why can't we simply keep increasing model size?
> A: Larger models require much more data and compute. Without sufficient training, they can underperform smaller, well-trained models. Also, improvements become smaller as models grow due to diminishing returns.

> Q: What are scaling laws?
> A: Scaling laws are empirical relationships showing that increasing model size, data, and compute generally reduces loss in a predictable way, but with diminishing returns.

> Q: Why is compute important?
> A: Compute determines how much training a model can receive. Given a fixed compute budget, there's an optimal balance between model size and training duration.

---

9. Data Preparation & Tokenization

9.1 Raw Dataset

Suppose you have a dataset for translation:

| English | French |
|---------|--------|
| Hello | Bonjour |
| Thank you | Merci |
| Good morning | Bonjour |

This is human-readable, but the model cannot use it directly.

9.2 Dataset Format

Case 1: Sequence-to-Sequence (T5, FLAN-T5)

Input ≠ Output.

| inputtext | targettext |
|------------|-------------|
| Translate English to French: Hello | Bonjour |
| Translate English to French: Thank you | Merci |

The model learns: Input sentence → Output sentence.

Examples: Translation, Summarization, Grammar correction, Question Answering.

Case 2: Causal Language Model (GPT/Llama)

Only one text column.

| text |
|------|
| Question: What is AI? Answer: Artificial Intelligence is... |

The model predicts the next token throughout this text.

9.3 Why Tokenization

Models don't understand words. They understand token IDs.

Sentence:    I love AI
Tokenizer → [40, 982, 301]

The model only sees these numbers.

9.4 Why Use the Same Tokenizer

Different tokenizers produce different IDs for the same text. If you use the wrong tokenizer, the model receives numbers it was never trained to interpret. Always use the tokenizer that belongs to the model.

9.5 Truncation

Models have a maximum context length. If your text exceeds this limit, we truncate (cut off) the extra tokens.

Original:        6000 tokens
After truncation: First 4096 tokens (for Llama)

9.6 Max Length

This tells the tokenizer: "Don't create sequences longer than this."

max_length = 512
Input: 700 tokens
Output: 512 tokens

9.7 Labels for Causal LM

Training text: `I love AI`

| Input IDs | I | love | AI |
|-----------|---|------|----|
| Targets (labels) | love | AI | `<END>` |

The labels are simply the same sequence shifted by one position, because the model always predicts the next token.

Input:   I     love   AI
Predict:       love   AI    <EOS>

This is called label shifting.

9.8 Prompt + Answer Fine-tuning

Full text: `Question: What is AI? Answer: Artificial Intelligence...`

Should the model learn to predict the question? No. We only want it to learn the answer.

9.9 Ignore Index

We mark the prompt tokens as `ignore_index` (usually `-100` in PyTorch). These tokens do not contribute to the loss.

Sentence:
Question: What is AI? Answer: Artificial Intelligence...

Loss:
Question:   ❌ Ignore
What:       ❌ Ignore
is:         ❌ Ignore
AI:         ❌ Ignore
Answer:     ❌ Ignore
Artificial: ✅ Compute loss
Intelligence: ✅ Compute loss

This teaches the model how to answer, not how to repeat the prompt.

9.10 Why Prompt Templates

Instead of inconsistent instructions:
Translate: Hello
French please: Good Morning
Convert into French: Thank you

Use the same format every time:
### Task: Translate English to French
### Input: Hello
### Output:

Now the model sees the same structure every time and learns the task more consistently.

9.11 Why This Is Especially Useful for Small Datasets

With only 500 examples, without a template, every example may look different:
AI?
Explain AI.
Can you tell me about AI?

Too much variation. Instead:
### Question: ...
### Answer: ...

The model sees the same format every time, making learning easier and more consistent.

9.12 Complete Pipeline

Raw Dataset
     ↓
Prompt Template (optional)
     ↓
Tokenizer
     ↓
Token IDs
     ↓
Truncate if needed
     ↓
Create Labels (shift by one for causal LM)
     ↓
Ignore prompt tokens if doing prompt-response fine-tuning
     ↓
Train Model

---

10. Fine-tuning Options

10.1 What is Fine-tuning

Suppose we have Llama 3. It has already read trillions of words. Now you want it to become a medical chatbot. You don't train from scratch — you continue training on medical data. This is Fine-tuning.

Pretrained Model → Train on your dataset → Specialized Model

10.2 Two Ways to Fine-tune

| Method | What's Updated | GPU Memory | Speed | Best For |
|--------|---------------|------------|-------|----------|
| Full Fine-tuning | All parameters (e.g., 7B) | High | Slow | Plenty of data and powerful GPUs |
| PEFT / LoRA | Only small adapter matrices | Much lower | Faster | Limited hardware, quick experimentation |

10.3 Full Fine-tuning via Trainer

Hugging Face's `Trainer` is an automatic training manager. Instead of writing the training loop, validation loop, optimizer, and checkpoint saving yourself, Trainer does it automatically. You only provide:
- Dataset
- Model
- Tokenizer
- Training settings

Key components:

| Component | Purpose |
|-----------|---------|
| TrainingArguments | Configuration settings (epochs, batch size, learning rate) |
| compute_metrics | Function that calculates evaluation metrics (accuracy, F1, BLEU) after validation |
| DataCollatorForLanguageModeling | Prepares batches by adding padding, creating labels, and shifting labels |
| evaluation_strategy | Controls when validation happens (every epoch, every N steps) |
| fp16 | Mixed precision — stores numbers in 16 bits to save memory and speed up training |

10.4 Parameter-Efficient Fine-tuning (PEFT) / LoRA

LoRA (Low-Rank Adaptation):

Instead of changing the original weight matrix `W`, LoRA says:
- Keep `W` frozen (unchanged)
- Learn a small update: `New Weight = W + ΔW`
- Where `ΔW = A × B` (two small matrices)

Why "Low Rank"?

Original matrix: `4096 × 4096` (very large)

Instead of learning the entire matrix, LoRA learns:
- `4096 × 8` and `8 × 4096` (much smaller)

Why LoRA is popular:

- Model: 7B parameters
- Full fine-tuning: Train 7 billion parameters
- LoRA: Train only 5–20 million parameters

✅ Less GPU memory
✅ Faster
✅ Easy to experiment
✅ Almost same accuracy in many tasks

Hugging Face PEFT is a library that implements LoRA, Prefix Tuning, and Prompt Tuning.

Accelerate is a helper library for multi-GPU training, mixed precision, and device placement.

10.5 Hyperparameters Explained

| Hyperparameter | Typical Value (Full FT) | Typical Value (LoRA) | Purpose |
|----------------|------------------------|---------------------|---------|
| AdamW | — | — | Most common optimizer for Transformers |
| Learning Rate | 5e-5 | 1e-4 to 3e-4 | Controls how big each update should be. LoRA uses higher LR because adapter parameters start from scratch. |
| Batch Size | 8–32 | 8–32 | Number of examples processed before each weight update |
| Epochs | 3–5 | 3–5 | Number of times the model sees the entire dataset |
| Weight Decay | 0.01 | 0.01 | Regularization — prevents weights from becoming too large |
| Warmup Steps | 200 | 200 | Gradually increases learning rate from 0 to target for stable early training |
| Gradient Accumulation Steps | As needed | As needed | Simulates larger batch when GPU memory is limited |
| FP16 | True | True | Mixed precision for speed and memory savings |

Why is LoRA's learning rate usually higher? Because we're training only a small number of new adapter parameters, not the whole model. These new parameters start from scratch and need to learn faster.

10.6 Full Fine-tuning vs LoRA Comparison

| Feature | Full Fine-tuning | LoRA |
|---------|-----------------|------|
| Parameters Updated | All model parameters | Only small adapter matrices |
| GPU Memory | High | Much lower |
| Training Speed | Slower | Faster |
| Storage | Full model | Small adapter files |
| Best For | Plenty of data and powerful GPUs | Limited hardware, quick experimentation |
| Interview Recommendation | Know the concept | Know it well — widely used today |

Interview Questions:

> Q: Why use LoRA instead of full fine-tuning?
> A: LoRA freezes the original model and trains only a small set of adapter matrices. This greatly reduces GPU memory and training time while achieving performance close to full fine-tuning on many tasks.

> Q: Why use warmup?
> A: At the start of training, model updates can be unstable. Warmup gradually increases the learning rate, leading to smoother and more stable optimization.

> Q: Why use early stopping?
> A: It stops training when validation performance stops improving, preventing overfitting and saving computation.

> Q: Why use checkpointing?
> A: It saves model states during training so you can resume after interruptions and keep the best-performing model instead of only the last one.

---

11. Evaluation Metrics

11.1 Perplexity

For Language Models (GPT, Llama)

Perplexity measures how uncertain the model is when predicting the next token.

Sentence: "I drink ___ every morning."

Model predicts:
coffee    → 0.80  (very confident)
tea       → 0.15
car       → 0.03
elephant  → 0.02

Correct answer: coffee ✅ Good model.

Formula:

$$ \text{Perplexity} = e^{\text{Cross Entropy Loss}} $$

> Perplexity is simply the exponential of the average cross-entropy loss. It converts log-probabilities into a more intuitive number.

Intuition: Perplexity answers "On average, how many words is the model confused between?"

| Perplexity | Meaning |
|------------|---------|
| 1 | Perfect prediction |
| 2–10 | Very good |
| 20–50 | Okay |
| 100+ | Poor |

Why evaluate on a held-out set? We compute perplexity on validation/test data to measure generalization to unseen data.

Prompt + Response fine-tuning: Compute perplexity only on the target (answer) tokens, ignoring the prompt.

11.2 Exact Match (EM)

For Question Answering

Checks whether the predicted answer exactly matches the reference.

| Question | Ground Truth | Prediction | EM |
|----------|-------------|------------|-----|
| Capital of France? | Paris | Paris | ✅ 1 |
| Capital of France? | Paris | The capital is Paris | ❌ 0 |

EM is very strict — even tiny differences result in zero.

11.3 F1 Score (for QA)

F1 measures token-level overlap between prediction and reference.

| Ground Truth | Prediction | EM | F1 |
|-------------|------------|-----|------|
| Paris | The city Paris | 0 | ~0.8 |
| Barack Obama | Obama | 0 | High (important words match) |

F1 is more forgiving than EM. It captures partial correctness.

11.4 BLEU

For Machine Translation

| English | Reference (French) | Prediction |
|---------|-------------------|------------|
| I love AI. | J'aime l'IA. | J'aime IA. |

BLEU compares n-gram overlap between prediction and reference. More overlap → higher BLEU.

> Simple intuition: BLEU measures "How similar is the translated sentence to the reference translation?"

11.5 ROUGE

For Summarization

| Article | Reference Summary | Prediction |
|---------|------------------|------------|
| (long article) | Earthquake hits Japan. | Japan experiences earthquake. |

ROUGE measures overlap between generated and reference summaries. Higher overlap → better summary.

> Difference: BLEU → Translation. ROUGE → Summarization.

11.6 Why Not Use Accuracy for LLMs

| Reference | Prediction | Accuracy | BLEU/ROUGE/F1 |
|-----------|------------|----------|---------------|
| The cat is sleeping. | The cat sleeps. | ❌ Wrong | ✅ Recognizes similarity |

Standard accuracy is too strict for generative tasks. BLEU, ROUGE, and F1 capture partial correctness.

11.7 Human Evaluation

Sometimes automatic metrics fail:

| Reference | Prediction | BLEU | Human |
|-----------|------------|------|-------|
| The movie was excellent. | The film was amazing. | Low | ✅ Perfect |

Humans can judge:
- Fluency
- Correctness
- Helpfulness
- Safety
- Naturalness

This is why companies like OpenAI and Anthropic still use human evaluators.

11.8 Why Automatic Metrics Can Be Misleading

| Reference | Prediction |
|-----------|------------|
| The capital of India is New Delhi. | India's capital is New Delhi. |

Meaning is identical. But BLEU may be lower because the wording changed. Humans would say it's completely correct.

11.9 Logging

During training, record:

Epoch 1
Train Loss = 2.3
Validation Loss = 2.5
Perplexity = 12
Sample Output: "The cat..."

Epoch 2
Train Loss = 1.9
Validation Loss = 2.0
Perplexity = 7
Sample Output: "The cat sat on the mat."

Why save sample generations? Sometimes validation loss improves but generated text becomes repetitive or unnatural. Sample outputs help catch such problems.

Metric Cheat Sheet

| Metric | Used For | What It Measures | Better Value |
|--------|----------|-----------------|--------------|
| Perplexity | Language Models (GPT, Llama) | How uncertain the model is when predicting the next token | Lower |
| Exact Match (EM) | Question Answering | Whether the predicted answer exactly matches the reference | Higher |
| F1 (QA) | Question Answering | Partial token overlap between prediction and reference | Higher |
| BLEU | Machine Translation | N-gram overlap with the reference translation | Higher |
| ROUGE | Summarization | Overlap between generated and reference summaries | Higher |
| Human Evaluation | Any generative task | Fluency, correctness, helpfulness, naturalness | Higher |

Interview Questions:

> Q: Why is lower perplexity better?
> A: Perplexity measures how uncertain a language model is when predicting the next token. Lower perplexity means the model assigns higher probability to the correct next tokens, indicating better predictions.

> Q: Why do we still need human evaluation?
> A: Automatic metrics mainly measure overlap with a reference, but there can be many correct ways to generate text. Human evaluation can judge meaning, fluency, helpfulness, and factual correctness, which automatic metrics may miss.

> Q: Why compute perplexity only on target tokens in prompt-response fine-tuning?
> A: Because the prompt is already given to the model. We want to evaluate how well it predicts the response, so we compute loss and perplexity only on the target (answer) tokens while ignoring the prompt tokens.

---

12. Prompt Templates & Inference

12.1 Prompt Template

Instead of inconsistent instructions:

Translate this.
French please: Good Morning
Convert into French: Thank you

Use the same format every time:

### Task: Translate English to French
### Input: Hello
### Output:

This consistent structure helps the model understand the task more reliably.

12.2 Few-shot Prompting

Show a few solved examples before asking the real question:

English: Hello → French: Bonjour
English: Thank You → French: Merci
English: Good Night → French:

The model notices the pattern and predicts: `Bonne nuit`

> Analogy: Instead of saying "Translate this," you first show "Dog → Perro, Cat → Gato, Bird → ?" The child understands the pattern. LLMs work similarly.

12.3 Zero-shot vs One-shot vs Few-shot

| Method | Definition | Example |
|--------|-----------|---------|
| Zero-shot | No examples | `Translate: Hello` |
| One-shot | One example | `Dog → Perro, Cat →` |
| Few-shot | Several examples | `Dog → Perro, Cat → Gato, Bird → Pájaro, Lion →` |

Generally, more good examples → better performance (up to a point).

12.4 Instruction Tuning Format

Modern LLMs are often trained with a structured format:

### Instruction:
Summarize this article.

### Input:
(long article)

Response:

This helps the model clearly separate task, input, and output.

12.5 Inference

Training is over. Now we ask the model questions. No learning happens here — the model only predicts.

In Hugging Face, we use:

model.generate(...)

Think of it as: "Continue this text."

12.6 Model Generation Parameters

| Parameter | Purpose | Notes |
|-----------|---------|-------|
| max_new_tokens | Maximum number of new tokens to generate | Controls answer length |
| temperature | Controls randomness | Lower = more deterministic; Higher = more creative |
| top_k | Sample only from the top k most likely tokens | Fixed number of candidates |
| top_p | Sample from tokens whose cumulative probability reaches p | Variable number of candidates |
| pad_token_id | ID of the padding token | Must be set correctly for batch generation |
| eos_token_id | ID of the end-of-sequence token | Tells the model when to stop generating |

Temperature explained:

| Temperature | Behavior | Best For |
|-------------|----------|----------|
| 0.1 | Very confident, same answer every time | Factual QA, mathematics |
| 1.0 | Balanced | General use |
| 1.5 | Very creative | Stories, poems, brainstorming |

Top-k vs Top-p:

| Method | Behavior |
|--------|----------|
| top_k = 3 | Keeps only the 3 most likely tokens, discards the rest |
| top_p = 0.90 | Keeps enough tokens until cumulative probability reaches 0.90 |

Top-k uses a fixed number of candidates. Top-p uses a variable number depending on the probability distribution.

12.7 Demo Script

A typical demo script does:

1. Load model
2. Load tokenizer
3. Create prompt
4. Tokenize
5. Generate answer
6. Print output

Complete flow:

User Question → Prompt Template → Tokenizer → Token IDs
    → model.generate() → Generated Tokens → Tokenizer Decode → Readable Text

12.8 What About Probabilities

Sometimes we want to know how confident the model was:

Prediction: Paris
Probability: 97%

or

Prediction: Dog
Probability: 55%

These probabilities come from the model's output logits after applying softmax. Useful for:
- Debugging
- Uncertainty estimation
- Choosing alternative outputs

Interview Questions:

> Q: What is the difference between temperature, top-k, and top-p?
> A: Temperature changes the probability distribution itself, making it sharper (low temperature) or flatter (high temperature). Top-k keeps only the top k candidate tokens before sampling. Top-p keeps a variable number of tokens whose cumulative probability reaches a threshold p (e.g., 0.9), then samples from that set.

> Q: Why use prompt templates?
> A: Prompt templates provide a consistent structure (e.g., Instruction → Input → Response), helping the model better understand the task and often improving the consistency of its outputs.

---

13. Sampling Strategies & Repetition

13.1 The Repetition Problem

If top-k = 1, the model always picks the highest-probability token. Even with a slightly larger top-k, if probabilities are very skewed and temperature is low, the model may keep producing the same answers.

Example: With top 5 tokens:
- Paris (0.60)
- London (0.20)
- Berlin (0.10)
- Rome (0.06)
- Madrid (0.04)

If top_k = 1, the model always picks Paris. Even with sampling, skewed distributions can cause repetitive outputs.

13.2 How to Prevent Repetitive Answers

| Method | How It Helps |
|--------|-------------|
| ✅ Increase temperature (e.g., 0.7 → 1.0) | Makes the model explore more possibilities |
| ✅ Use top-p instead of only top-k | Candidate set changes depending on the probability distribution |
| ✅ Increase top_k (e.g., 10 → 50) | Allows more candidate tokens |
| ✅ Use repetition penalty | `norepeatngram_size` in Hugging Face discourages repeating the same phrases |
| ✅ Sample instead of greedy | Always sample rather than taking the highest-probability token |

One-line interview answer:

> If top-k produces repetitive outputs, increase the temperature, increase top_k, or use top-p (nucleus sampling) with a repetition penalty to encourage more diverse generations.

---

14. Building a Simple RAG Pipeline

14.1 What is RAG

RAG = Retrieval Augmented Generation

Suppose you ask ChatGPT: "What is my company's leave policy?" The model probably doesn't know. Instead of retraining the LLM:

1. First search the company's documents
2. Retrieve the relevant pages
3. Give those pages to the LLM
4. LLM answers using those documents

Question → Retrieve relevant documents → Give documents + question to LLM → Answer

RAG = Search first, answer later.

14.2 Complete RAG Pipeline Overview

Documents → Chunking → Embedding → Store in Vector DB (FAISS)
                                                      ↑
User Query → Query Embedding → Similarity Search
                                      ↓
                             Relevant Chunks
                                      ↓
                               LLM Prompt
                                      ↓
                                 Answer

14.3 Step 1: Chunking

Why chunk?

A 100-page PDF cannot be embedded as one piece because:
- Very large embedding
- Poor retrieval accuracy
- Exceeds context window

Chunk size: 256–512 tokens

| Chunk Size | Problem |
|------------|---------|
| Too small (20 tokens) | No context — "because of this..." — because of what? |
| Too large (3000 tokens) | Contains many topics — retrieval becomes inaccurate |
| 256–512 tokens | ✅ Balances context and retrieval accuracy |

Why overlap?

> Important interview question.

Without overlap, an idea that starts at the end of Chunk 1 and finishes at the beginning of Chunk 2 gets split:

Chunk 1: "...patient was diagnosed"
Chunk 2: "with diabetes..."

The complete meaning is split. The retriever may miss it.

With overlap (50–100 tokens):

Chunk 1: A B C D
Chunk 2: C D E F

Now C and D appear in both chunks. If the query is about C D E, at least one chunk contains enough context.

Sentence chunking (smart chunking):

Instead of cutting after exactly 512 tokens, cut at sentence boundaries:

❌ Bad chunk:
"The patient was diagnosed
---------------------------
with diabetes yesterday."

✅ Good chunk:
"The patient was diagnosed with diabetes yesterday.
---------------------------
Treatment started..."

Complete sentences stay together.

14.4 Step 2: Embeddings

Computers cannot compare text directly. Each chunk is converted into a vector (embedding):

Chunk: "Deep learning is..."
    ↓
Embedding Model
    ↓
[0.13, -0.44, 0.88, ...]

Why embeddings? Similar meanings are placed close together in vector space. "CNN" and "Convolutional Neural Network" have similar embeddings even though the words are different.

Embedding models:

| Model | Speed | Size | Quality |
|-------|-------|------|---------|
| `all-MiniLM-L6-v2` | Fast | Small | Good |
| `all-mpnet-base-v2` | Slower | Larger | Better |

Normalize embeddings:

Two vectors pointing in the same direction but with different lengths:

A = [2, 2]
B = [20, 20]

Without normalization, B looks much larger. After normalization:

[2, 2]    → [0.707, 0.707]
[20, 20]  → [0.707, 0.707]

Now only direction matters. This is important for cosine similarity, which compares angles, not lengths.

14.5 Step 3: FAISS (Vector Database)

What is FAISS?

FAISS (by Meta) stores millions of vectors and quickly finds the most similar ones. Think of it like Google Search, except for vectors instead of webpages.

Why not SQL? SQL searches exact values. For embeddings, we want most similar, not exact match.

IndexFlatIP:

- IP = Inner Product (Dot Product)
- After normalization, Dot Product = Cosine Similarity
- Finding the largest dot product = finding the highest cosine similarity

Creating the index:

import faiss
import numpy as np

# Normalize vectors
faiss.normalizeL2(nparray)

# Create index
d = 384  # dimension (e.g., MiniLm gives 384)
index = faiss.IndexFlatIP(d)

# Add vectors
index.add(np_array)

For larger datasets:

| Index | Description |
|-------|-------------|
| HNSW | Like a road map — follow nearby roads to quickly reach the correct neighborhood. Very fast, high accuracy. |
| IVF (Inverted File Index) | Divide vectors into clusters, search only the relevant cluster. Much faster than flat search. |
| PQ (Product Quantization) | Compress vectors to use less memory. Slightly lower accuracy. Useful for billions of vectors. |

Persist to disk:

Building embeddings takes time. Save the FAISS index to disk and load it later instead of recomputing.

Metadata:

FAISS returns vector indices (e.g., "Vector #57"), but we need to know what that vector represents:

57 → Doc ID: 3
   → Chunk text: "The BatchNorm layer normalizes..."
   → Page: 18
   → Source: ML Notes.pdf

This mapping is called metadata.

14.6 Step 4: Retrieval

User asks: "Explain BatchNorm"

1. Convert question to embedding
2. Search FAISS:
   
   Question Embedding → FAISS → Top 5 Similar Chunks
   
   Chunk 15: Score 0.93
   Chunk 48: Score 0.90
   Chunk 91: Score 0.88
   
3. Retrieve top-k chunks (k = 3 by default)

Score: Measures similarity. Higher score = more relevant.
- 0.95 = Very similar
- 0.20 = Not related

Reranking (optional, budget permitting):

FAISS retrieves candidates quickly using embeddings. A cross-encoder reads the question + each candidate together for more accurate ranking:

FAISS → Top 20 → Cross Encoder → Best 5

Cross-encoders are more accurate but slower, so the typical pipeline uses FAISS for fast initial retrieval and a cross-encoder for final ranking.

14.7 Step 5: Prompt Construction

Now we have the best chunks. We don't ask the LLM directly — we first construct a prompt:

Context:
[DOC 1] BatchNorm normalizes activations...
[DOC 2] It helps stabilize training...

Question:
What is BatchNorm?

Answer using only the provided context and cite which doc the info came from (Doc #).

Why "Use only the context"? Otherwise, the LLM may use its own knowledge, which could be outdated or incorrect. This reduces hallucinations.

Why cite the source? The user knows where the information came from, increasing trust.

Keep total tokens within the model's context size.

14.8 Complete RAG Pipeline Flow

Documents
    ↓
Chunking (256–512 tokens, 50–100 token overlap, sentence boundaries)
    ↓
Embeddings (all-MiniLM-L6-v2 or all-mpnet-base-v2)
    ↓
Normalize (L2)
    ↓
FAISS Index (IndexFlatIP or HNSW/IVF for large datasets)
    ↓
User Question
    ↓
Query Embedding
    ↓
Similarity Search (FAISS)
    ↓
Top-k Chunks
    ↓
(Optional) Cross-Encoder Reranking
    ↓
Prompt Construction (Context + Question + Instruction)
    ↓
LLM
    ↓
Answer + Source Citation

Interview Questions:

> Q1: Why use FAISS?
> A: FAISS stores embeddings efficiently and performs very fast nearest-neighbor (similarity) search, making it ideal for retrieving relevant document chunks.

> Q2: Why normalize embeddings?
> A: After L2 normalization, the dot product becomes equivalent to cosine similarity, so FAISS can use a fast inner-product search while comparing semantic similarity correctly.

> Q3: Why keep metadata?
> A: FAISS only stores vectors. Metadata maps each vector back to its original document, chunk text, page number, and source so the retrieved results are meaningful.

> Q4: Why use a reranker?
> A: FAISS retrieves candidates quickly using embeddings, while a cross-encoder rereads the query and each candidate together to produce a more accurate ranking.

> Q5: Why include retrieved chunks in the prompt?
> A: The LLM doesn't search the database itself. We provide the retrieved context in the prompt so it can generate answers grounded in those documents, reducing hallucinations.

> Q6: Why use overlap while chunking?
> A: Because important information may span chunk boundaries. Overlapping chunks ensure that context isn't lost, improving retrieval accuracy.

> Q7: Why not embed the whole document?
> A: Large documents contain multiple topics, making retrieval less accurate and often exceeding the model's context window. Chunking creates focused pieces that are easier to retrieve.

> Q8: Why use embeddings?
> A: Embeddings convert text into vectors where semantically similar texts are close together. This allows similarity search even when the wording differs.

---

15. Quick Interview Cheat Sheets

Debugging Cheat Sheet

| Problem | Cause | Fix |
|---------|-------|-----|
| Softmax overflow | Large logits cause exp() overflow | Subtract the maximum logit before softmax |
| Mask broadcasting error | Wrong mask shape | Ensure mask broadcasts correctly to attention scores |
| Padding leakage | PAD tokens influence attention/loss | Use a padding mask and `ignore_index=PAD` |
| Training unstable | High LR, bad initialization, exploding gradients | Warmup, lower LR, gradient clipping, He/Xavier initialization |
| Repetitive generation | Greedy decoding always picks the highest-probability token | Use temperature, top-k, or top-p sampling |

Optimization Cheat Sheet

| Concept | Think of it as... |
|---------|-------------------|
| Mixed Precision (AMP) | Use smaller numbers (FP16) to save memory and train faster |
| Gradient Accumulation | Pretend you have a larger batch by combining gradients from several small batches |
| Activation Checkpointing | Save only a few intermediate results and recompute the rest later to save memory |
| FlashAttention | Process attention in small chunks instead of building one huge attention matrix |
| Fused QKV | Compute Q, K, and V together in one operation instead of three separate ones |
| Weight Tying | Reuse the same matrix for both input embeddings and output predictions |
| Sliding Window | Each token only looks at nearby tokens instead of the whole sequence |
| RoPE | A smarter way to encode token positions, especially useful for long contexts |
| Retrieval (RAG) | Search for relevant information first instead of putting everything into the model's context |

Pretraining Objectives Cheat Sheet

| Objective | Learns | Best for |
|-----------|--------|----------|
| Autoregressive (GPT) | Predict the next token | Text generation, chatbots, code |
| Masked LM (BERT) | Predict masked words using both left and right context | Classification, embeddings, search, QA |
| Denoising (T5) | Reconstruct corrupted text spans | Translation, summarization, seq2seq tasks |
| Contrastive (CLIP) | Match related pairs (e.g., image and text) | Multimodal retrieval and representation learning |

Teacher Forcing & Exposure Bias Cheat Sheet

| Concept | Simple Explanation |
|---------|-------------------|
| Teacher Forcing | During training, the model always receives the correct previous tokens |
| Inference | The model must use its own previous predictions |
| Exposure Bias | The model is exposed to incorrect contexts at inference that it never saw during training |
| Error Compounding | One wrong prediction changes the context, making future mistakes more likely |
| Scheduled Sampling | Mix ground-truth and model predictions during training to reduce exposure bias |
| Beam Search | Keep multiple candidate sequences during decoding so one early mistake doesn't necessarily ruin the output |

Scaling Laws Cheat Sheet

| Concept | Simple Meaning |
|---------|---------------|
| Parameters (N) | Model size (how much it can learn) |
| Data (D) | Number of training tokens/examples |
| Compute (C) | GPU work used for training |
| Scaling Law | Bigger model + more data + more compute → better performance in a predictable way |
| Diminishing Returns | Each additional increase gives a smaller improvement than the previous one |
| Undertrained Large Model | A huge model trained on too little data or too few steps can perform worse than a smaller, well-trained model |
| Compute Budget | With limited GPU resources, you must balance model size and training time instead of maximizing only one |

Fine-tuning Cheat Sheet

| Concept | Simple Meaning |
|---------|---------------|
| Fine-tuning | Continuing training on a pretrained model using your own dataset |
| Full Fine-tuning | Updating all model parameters |
| LoRA (PEFT) | Training only small adapter matrices while freezing the original model |
| Hyperparameters | Settings that control training (learning rate, batch size, epochs, etc.) |
| Warmup | Gradually increasing learning rate at the start of training |
| Gradient Accumulation | Combining gradients from multiple small batches before updating |
| Early Stopping | Stopping training when validation performance stops improving |
| Checkpointing | Saving model states periodically during training |

Evaluation Metrics Cheat Sheet

| Metric | Used For | What It Measures | Better Value |
|--------|----------|-----------------|--------------|
| Perplexity | Language Models (GPT, Llama) | How uncertain the model is when predicting the next token | Lower |
| Exact Match (EM) | Question Answering | Whether the predicted answer exactly matches the reference | Higher |
| F1 (QA) | Question Answering | Partial token overlap between prediction and reference | Higher |
| BLEU | Machine Translation | N-gram overlap with the reference translation | Higher |
| ROUGE | Summarization | Overlap between generated and reference summaries | Higher |
| Human Evaluation | Any generative task | Fluency, correctness, helpfulness, naturalness | Higher |

Sampling Cheat Sheet

| Concept | Simple Meaning |
|---------|---------------|
| Temperature | Controls randomness. Lower = more deterministic, higher = more creative |
| top-k | Sample only from the top k most likely next tokens |
| top-p (Nucleus Sampling) | Sample from the smallest set of tokens whose cumulative probability reaches p |
| padtokenid | ID used for padding shorter sequences to the same length in a batch |
| eostokenid | Special token that tells the model the sequence has ended and generation should stop |

RAG Cheat Sheet

| Concept | Simple Meaning |
|---------|---------------|
| RAG | Search first, answer later — retrieve relevant documents before asking the LLM |
| Chunking | Splitting documents into small pieces (~256–512 tokens) for efficient retrieval |
| Overlap | Adding shared content between chunks to preserve context across boundaries |
| Embeddings | Converting text into vectors where similar meanings are close together |
| Normalization | Making vectors unit-length so cosine similarity compares only direction |
| FAISS | A library for fast vector similarity search |
| Metadata | Information that maps each vector back to its source document and chunk |
| Reranker | A more accurate (but slower) model that re-ranks retrieved candidates |
