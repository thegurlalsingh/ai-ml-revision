# AI/ML Linear Algebra Study Guide

A complete, beginner-friendly guide to the core math behind Artificial Intelligence and Machine Learning. 

---

## 1. What is a Vector?

### The Simple Definition
A vector is just a list of numbers in a specific order. 

### Three Ways to Visualize a Vector:
1. **The List View (Computer Science):** It is just an array of data. For example, a house might be represented as `[3, 2, 1500]` (3 bedrooms, 2 bathrooms, 1500 square feet).
2. **The Map View (Geometry):** It is a point on a map, or an arrow pointing from the starting corner $(0,0)$ to that point.
3. **The Data View (Machine Learning):** In ML, a vector represents one single item in your dataset (like a customer, a picture, or a word).

### Examples
Let's look at two simple vectors with three numbers each:
* $\mathbf{x} = [1, 2, 3]$
* $\mathbf{y} = [4, 5, 6]$

### Why Vectors are Everything in AI
Computers cannot understand raw words, sounds, or pictures. They only understand numbers. Therefore, everything in AI must be turned into a vector first:
* **Pictures:** Turned into a long list of numbers representing the brightness of every single pixel.
* **Text / Words:** Turned into a list of numbers called an **embedding**. For example, the word `"apple"` might become a list of 300 numbers that represent its meaning.
* **Audio:** Voices and sounds are chopped up into numbers tracking pitch and volume.
* **Profiles:** Netflix turns your viewing habits into a vector (e.g., how much you like action, comedy, or drama).

---

## 2. The Dot Product (Inner Product)

The dot product is one of the most popular interview topics. It is a way to multiply two vectors together to get a **single number**.

### How to Calculate It
To find the dot product of $\mathbf{x} = [1, 2, 3]$ and $\mathbf{y} = [4, 5, 6]$, you multiply the matching pairs and add up the results:
$$\mathbf{x} \cdot \mathbf{y} = (1 \times 4) + (2 \times 5) + (3 \times 6)$$
$$\mathbf{x} \cdot \mathbf{y} = 4 + 10 + 18 = 32$$

### What it Actually Means (The Core Secret)
The dot product measures **how much two vectors are pointing in the same direction**. It tells you how well aligned they are.

### The Secret Formula
$$\mathbf{x} \cdot \mathbf{y} = \text{Length of } \mathbf{x} \times \text{Length of } \mathbf{y} \times \cos(\theta)$$
*(Note: $\theta$ is just the angle between the two arrows).*

### The Three Scenarios:
* **Scenario 1: Same Direction.** The arrows point the exact same way. The dot product gives you the biggest possible positive number. In AI, this means the two items are highly similar.
* **Scenario 2: Perpendicular ($90^\circ$ angle).** The arrows are at a perfect right angle. The dot product becomes **exactly 0**. This means they have absolutely nothing in common.
* **Scenario 3: Opposite Directions.** One arrow points left, the other points right. The dot product becomes a negative number. This means they are opposites.

### Where is it used in AI?
* **ChatGPT & Transformers:** It is used to calculate "Attention"—helping the AI figure out which words in a sentence relate to each other.
* **Search Engines:** When you type a query into a vector database, it uses the dot product to find the closest matching documents.

---

## 3. Norms (The Length of a Vector)

A **norm** is just a math word for **how big, long, or heavy a vector is**. 

### L2 Norm (The Straight-Line Distance)
This is the standard way we measure distance in the real world using a ruler. 

#### Example in 2D
If you have a vector $\mathbf{x} = [3, 4]$, how far away is it from the center $(0,0)$? We use the Pythagorean theorem ($a^2 + b^2 = c^2$):
$$\text{Length} = \sqrt{3^2 + 4^2} = \sqrt{9 + 16} = \sqrt{25} = 5$$

#### Example in 3D
For $\mathbf{x} = [1, 2, 3]$:
$$\text{Length} = \sqrt{1^2 + 2^2 + 3^2} = \sqrt{1 + 4 + 9} = \sqrt{14}$$

---

### L1 Norm (The Grid Distance)
Instead of walking straight through walls, imagine you are a taxi driver in New York City. You can only drive along street grids (left, right, up, down). You just add up the absolute values of the movements.

#### Formula
$$\text{L1 Norm} = \text{Sum of all numbers (ignoring negative signs)}$$

#### Example
For $\mathbf{x} = [1, -2, 3]$:
$$\text{L1 Norm} = 1 + 2 + 3 = 6$$

---

### Simple Comparison: L1 vs. L2 Regularization

Why do we care about these two lengths in AI? We use them to keep AI models from cheating or overcomplicating things (this is called **regularization**).

Let's test both norms on a vector with one massive number and one tiny number: $\mathbf{w} = [100, 1]$.
* **L1 Norm:** $100 + 1 = 101$
* **L2 Norm:** $\sqrt{100^2 + 1^2} = \sqrt{10001} \approx 100$

#### The Big Trick:
Because the L2 norm squares numbers first, **massive numbers get penalized incredibly heavily**. Therefore:
* **L2 Regularization (Ridge):** Dislikes giant numbers. It forces all numbers in the vector to shrink down smoothly together, but they rarely hit exactly zero.
* **L1 Regularization (Lasso):** Treats all changes equally. To save energy, it often pushes less important numbers **completely to zero**. 

#### Interview Question: Why does L1 create "sparse" models (lots of zeros)?
**Answer:** Because L1 cuts down features linearly. It prefers to turn useless features completely off (setting their weights to exactly 0). This acts as an automated feature selector, leaving behind a clean, simple model.

---

## 4. Orthogonality (Perpendicular)

### The Definition
Two vectors are **orthogonal** if their dot product is exactly **0**. 

### What it Means Geometrically
It means they sit at a perfect $90^\circ$ angle to each other. They are completely independent.

### Why AI Loves Orthogonality
Imagine you are building a model to predict health, and you have two features: *Height in inches* and *Height in centimeters*. They tell you the exact same thing. This is called **redundancy**, and it confuses AI models.

Orthogonal features mean **zero overlap in information**. Every new feature brings completely fresh, independent knowledge to the table.
* **PCA (Principal Component Analysis):** This tool takes messy, overlapping data and rearranges it into brand new axes that are perfectly orthogonal to each other, removing all redundancy.

### Interview Trick Question: If two vectors are orthogonal, are they independent?
**Answer:** In geometry, yes, they have no linear correlation. But in pure statistics, "independence" is a much stronger rule. Orthogonality only proves they don't have a *linear* relationship. They could still be connected in a complex, curving, non-linear way.

---

## 5. Cosine Similarity

### What is it?
Cosine similarity is a tool that calculates how much two vectors look alike, but it **completely ignores how big or small they are**. It only cares about the **direction** they are pointing.

### The Formula
$$\text{Cosine Similarity} = \frac{\mathbf{x} \cdot \mathbf{y}}{\text{Length of } \mathbf{x} \times \text{Length of } \mathbf{y}}$$

### Why do we strip away the length?
Imagine you write a short essay about space. Now imagine NASA writes a massive 500-page book about space. 
* If you look at raw word counts (vector length), they look totally different because NASA used thousands of words.
* But if you look at the *direction* of the words, they point to the exact same topic (space). Cosine similarity fixes the size difference and gives them a perfect score of **1**, proving they mean the same thing.

---

## 6. Matrices

### What is a Matrix?
A matrix is just a table or grid of numbers. 
* **Rows:** Think of these as your samples (e.g., Customer 1, Customer 2, Customer 3).
* **Columns:** Think of these as the features (e.g., Age, Income, Credit Score).

### How to Multiply Matrices
You can only multiply Matrix $\mathbf{A}$ by Matrix $\mathbf{B}$ if the **number of columns in A matches the number of rows in B**. The inner dimensions must match:
$$(m \times \mathbf{n}) \times (\mathbf{n} \times p) \rightarrow (m \times p)$$

### $\mathbf{A}\mathbf{x}$ vs. $\mathbf{x}\mathbf{A}$ (Left vs. Right Multiplication)
* **$\mathbf{A}\mathbf{x}$ (Matrix on the left, Vector on the right):** This is the gold standard in AI. The matrix acts like a machine, transforming the incoming column vector into a new output vector. Every layer in a neural network runs this formula:
  $$\mathbf{y} = \mathbf{W}\mathbf{x} + \mathbf{b}$$
  *(Weights $\times$ Input + Bias)*
* **$\mathbf{x}\mathbf{A}$ (Vector on the left, Matrix on the right):** This forces you to use a horizontal row vector instead, which changes the math layout completely.

Remember: Order matters! $\mathbf{A}\mathbf{B}$ does **NOT** equal $\mathbf{B}\mathbf{A}$.

---

## 7. The Matrix as a "Space Transformer"

The easiest way to understand a matrix is to stop thinking of it as a grid of numbers and start thinking of it as an **animated filter or transformer**. 

When you pass a vector through a matrix, the matrix alters the space around it. It can:
* **Scale:** Stretch or shrink the vector.
* **Rotate:** Spin the vector around an angle.
* **Reflect:** Flip the vector across an axis like a mirror.
* **Shear:** Distort and slant the vector sideways.

Every layer of a Deep Neural Network is just doing this: it takes input data, stretches it out, spins it around using a matrix, applies a small non-linear curve, and repeats the process until the data is organized.

---

## 8. Transpose ($\mathbf{A}^T$)

### What is it?
Transposing a matrix simply means **flipping it on its side**. Your rows become columns, and your columns become rows.

### Example
If you have a $2 \times 3$ matrix:
$$\mathbf{A} = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}$$

Flipping it creates a $3 \times 2$ matrix:
$$\mathbf{A}^T = \begin{bmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{bmatrix}$$

### Two Rules to Remember:
1. Flipping a matrix twice brings you back to the start: $(\mathbf{A}^T)^T = \mathbf{A}$
2. If you flip a multiplied pair, the order switches: $(\mathbf{A}\mathbf{B})^T = \mathbf{B}^T\mathbf{A}^T$

---

## 9. Symmetric Matrices

A matrix is **symmetric** if it looks exactly the same even after you transpose it ($\mathbf{A} = \mathbf{A}^T$). This means the top-right half is a perfect mirror image of the bottom-left half.

### Example
$$\begin{bmatrix} 1 & \mathbf{2} \\ \mathbf{2} & 3 \end{bmatrix}$$

AI engineers love symmetric matrices because their math properties are incredibly clean, stable, and fast for computer chips to calculate.

---

## 10. Positive Semi-Definite (PSD) Matrices

### What is it?
A matrix is **Positive Semi-Definite (PSD)** if it never turns a vector against itself. No matter what vector $\mathbf{x}$ you multiply it by, the final calculated energy ($\mathbf{x}^T\mathbf{A}\mathbf{x}$) is **always greater than or equal to 0**. It behaves like a positive number in regular algebra.

### The Quick Interview Cheat Code:
How do you prove a matrix is PSD in an interview? Look at its eigenvalues (scaling factors). 
* If all eigenvalues are $\ge 0$, it is **Positive Semi-Definite**.
* If all eigenvalues are strictly $> 0$ (no zeros allowed), it is **Positive Definite**.

### Why do we care?
* **Covariance Matrices:** Tables that show how features move together are always PSD. This guarantees that your model will never calculate a impossible metric like a "negative variance."
* **Finding the Bottom of a Hill (Optimization):** In AI, we want to find the lowest possible error. We use a matrix of second derivatives called a **Hessian**. If the Hessian matrix is PSD, it scientifically proves you are standing safely at the bottom of a valley (a true local minimum), not balanced on top of a hill.

---

## 11. Eigenvalues and Eigenvectors

### The Intuition
As we discussed earlier, matrices act like space filters—they twist, spin, and stretch vectors. 

If you throw a bunch of random vectors into a matrix transformation, most of them will get twisted into a brand new direction. However, there are always a few special, magical vectors that **keep their exact same direction**. They do not twist at all; they just get longer or shorter. 
* These resilient vectors are **Eigenvectors**.
* The factor by which they stretch or shrink is the **Eigenvalue** ($\lambda$).

### The Simple Equation
$$\mathbf{A}\mathbf{x} = \lambda \mathbf{x}$$
*(Matrix $\times$ Vector = Scalar Scaling $\times$ Vector)*

### What the Eigenvalue ($\lambda$) Tells You:
* If $\lambda = 5$: The vector points the same way but grows 5 times longer.
* If $\lambda = 0.2$: The vector points the same way but shrinks down.
* If $\lambda = -3$: The vector stays on the same line, but flips to point backward.

---

## 12. Real-World AI Applications of Eigenvalues

### Principal Component Analysis (PCA)
Imagine you have a giant dataset with 100 features about a patient, and your brain can only visualize a 2D graph. How do you compress 100 features down to 2?
1. You build a covariance matrix of your data.
2. You extract its eigenvectors.
3. The eigenvector with the **largest eigenvalue** points directly along the path where your data is most spread out (contains the most information). You pick the top two directions and discard the rest!

---

### SVD (Singular Value Decomposition)
SVD is a tool that breaks down *any* data matrix into three simple components: **Rotation $\rightarrow$ Scaling $\rightarrow$ Rotation**.

It is used for:
* **Image Compression:** It extracts the most dominant structural directions of an image, allowing you to delete the low-value eigenvalues. This turns a massive image file into a tiny fraction of its original size without losing the core picture.
* **Netflix Recommendation Systems:** SVD automatically looks at a massive table of users and movie ratings. It discovers hidden "genres" or trends (e.g., isolating action lovers from romance lovers) completely on its own, without any manual labels.

---

## 13. The Power Iteration Algorithm (The Google Favorite)

This is a classic question favored by top-tier tech companies.

### The Problem
Finding all the eigenvectors for a massive matrix takes an immense amount of computer processing power. What if you *only* want the single most dominant direction (the one with the largest eigenvalue)?

### The Solution (Power Iteration)
1. Grab a completely random vector.
2. Multiply it by the matrix.
3. Normalize it (shrink it back to length 1 so numbers don't explode).
4. Repeat this loop over and over again.

### Why does this work? (The Analogy)
Think of a matrix as a room with a giant exhaust fan blowing toward the east (the dominant eigenvector), and a tiny desk fan blowing north (a minor eigenvector). 

If you drop a feather (your random starting vector) into the room:
* The desk fan pushes it north a tiny bit.
* The giant exhaust fan pushes it east with massive power.

Every time you multiply by the matrix, the dominant force scales up exponentially higher than the minor force. After a few loops, the minor force becomes completely invisible. The feather will point **perfectly along the direction of the dominant exhaust fan**. 

### Quick Interview Answer:
**Question:** "Why does repeated matrix multiplication converge to the dominant eigenvector?"  
**Answer:** "Any random vector is made up of a mix of different eigenvectors. When we multiply the vector by the matrix repeatedly, every component gets scaled by its own eigenvalue over and over again. The component with the largest eigenvalue grows exponentially faster than all the others. Eventually, it completely takes over, forcing the vector to align perfectly with the dominant eigenvector direction."
