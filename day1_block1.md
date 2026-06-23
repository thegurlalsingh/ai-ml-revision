# AI/ML Linear Algebra Revision Notes

A comprehensive guide to core linear algebra concepts for AI/ML engineering interviews, covering vectors, matrices, transformations, norms, eigenvalues, PCA, SVD, and more.

---

## 1. Vectors

### What is a vector?
[cite_start]A vector is simply an ordered collection of numbers[cite: 589].

### Examples:
* [cite_start]$x = [1, 2, 3]$ [cite: 591]
* [cite_start]$y = [4, 5, 6]$ [cite: 591]

You can think of it as:
* [cite_start]A point in space [cite: 593]
* [cite_start]A direction [cite: 594]
* [cite_start]A feature representation of data [cite: 595]

[cite_start]In ML, vectors usually represent data points[cite: 596].

### Why are vectors important in ML?
[cite_start]Everything becomes a vector[cite: 598]:
* [cite_start]**Images** $\rightarrow$ pixel vectors [cite: 599]
* [cite_start]**Text** $\rightarrow$ embeddings [cite: 600]
* [cite_start]**Audio** $\rightarrow$ feature vectors [cite: 601]
* [cite_start]**User profiles** $\rightarrow$ vectors [cite: 602]

---

## 2. Inner Product (Dot Product)
[cite_start]*Very important interview topic[cite: 604].*

### Given:
* [cite_start]$x = [1, 2, 3]$ [cite: 606]
* [cite_start]$y = [4, 5, 6]$ [cite: 606]

### Dot product calculation:
[cite_start]$$x \cdot y = 1 \times 4 + 2 \times 5 + 3 \times 6 = 32$$ [cite: 608]

### Geometric Meaning
[cite_start]The dot product measures **how aligned two vectors are**[cite: 610].

### Formula:
$$x \cdot y = \|x\| \|y\| [cite_start]\cos\theta$$ [cite: 612, 613]
[cite_start]where $\theta$ is the angle between vectors[cite: 614, 615, 616].

* [cite_start]**Case 1: Same Direction** $\theta = 0^\circ \implies \cos(0) = 1$ [cite: 618]  
  [cite_start]Maximum dot product[cite: 619]. [cite_start]Means vectors are highly similar[cite: 620].
* [cite_start]**Case 2: Perpendicular** $\theta = 90^\circ \implies \cos(90) = 0$ [cite: 622]  
  [cite_start]Dot product becomes zero[cite: 623]. [cite_start]No alignment[cite: 624].
* [cite_start]**Case 3: Opposite Direction** $\theta = 180^\circ \implies \cos(180) = -1$ [cite: 626]  
  [cite_start]Negative dot product[cite: 627].

### Why Dot Product Matters in ML
[cite_start]Used in[cite: 628, 629]:
* [cite_start]GPT [cite: 630]
* [cite_start]BERT [cite: 631]
* [cite_start]Retrieval systems [cite: 632]
* [cite_start]Vector databases [cite: 633]
* [cite_start]Neural networks [cite: 634]

---

## 3. Norms
[cite_start]**Norm** = length or magnitude of a vector[cite: 636].

### L2 Norm (Euclidean Norm)
[cite_start]*Most common[cite: 638].*

[cite_start]**Given:** $x = [3, 4]$ [cite: 640]  
[cite_start]**Length:** $$\|x\|_2 = \sqrt{3^2 + 4^2} = 5$$ [cite: 642]

[cite_start]**General Formula:** $$\|x\|_2 = \sqrt{\sum_i x_i^2}$$ [cite: 644]

**Example:** $x = [1, 2, 3]$  
[cite_start]$$\|x\|_2 = \sqrt{1 + 4 + 9} = \sqrt{14}$$ [cite: 646]

#### Why L2 is Used:
* [cite_start]Measures actual geometric distance[cite: 648].
* [cite_start]Used in: Linear regression [cite: 650][cite_start], Gradient descent [cite: 651][cite_start], Weight decay [cite: 652][cite_start], KNN [cite: 653][cite_start], PCA[cite: 654].

---

### L1 Norm

[cite_start]**Formula:** $$\|x\|_1 = \sum_i |x_i|$$ [cite: 657]

**Example:** $x = [1, -2, 3]$  
$$\|x\|_1 = |1| + |-2| + |3| [cite_start]= 6$$ [cite: 659, 660]

---

### Difference Between L1 and L2
[cite_start]**Example:** $x = [100, 1]$ [cite: 663]

* [cite_start]**L1:** $101$ [cite: 665]
* [cite_start]**L2:** $\sqrt{10000 + 1} \approx 100$ [cite: 667]

#### Notice:
* [cite_start]L2 squares values[cite: 669]. [cite_start]Large values become much larger[cite: 670].
* [cite_start]Therefore, **L2 penalizes large weights heavily** [cite: 672][cite_start], while **L1 treats all weights linearly**[cite: 673].

#### Regularization Interview Question: Why does L1 produce sparse models?
[cite_start]Because minimizing $|w|$ [cite: 676, 677] [cite_start]often drives many weights exactly to zero[cite: 678]. [cite_start]Thus, **L1 $\rightarrow$ feature selection[cite: 680].**

#### Why does L2 not produce sparse models?
[cite_start]Because squaring makes weights shrink smoothly toward zero but rarely exactly zero[cite: 682].

---

## 4. Orthogonality
[cite_start]*Interviewers love this[cite: 684].*

[cite_start]Two vectors are orthogonal if[cite: 685]:
[cite_start]$$x \cdot y = 0$$ [cite: 686]

### Example
[cite_start]$x = [1, 0]$, $y = [0, 1]$ [cite: 688]  
[cite_start]**Dot product:** $1(0) + 0(1) = 0$ [cite: 690] [cite_start]$\rightarrow$ Orthogonal[cite: 691].

### Geometric Meaning
[cite_start]Orthogonal vectors are perpendicular[cite: 693]. [cite_start]Angle = $90^\circ$[cite: 694, 695].

### Why Orthogonality Matters in ML: Reduces Redundancy
[cite_start]Suppose you have a *Height feature* [cite: 699] [cite_start]and a *Weight feature*[cite: 700]. [cite_start]They may contain overlapping information[cite: 701]. [cite_start]But **orthogonal features contain independent information**[cite: 702].

* [cite_start]**PCA:** Principal components are orthogonal [cite: 704] [cite_start]because each principal component captures new information not already captured by previous components[cite: 706].
* [cite_start]**Embeddings:** Ideally, unrelated concepts should have nearly orthogonal embeddings[cite: 708]. [cite_start]For example, `"Dog"` [cite: 710] [cite_start]and `"Quantum Mechanics"` [cite: 711] [cite_start]should not point in similar directions[cite: 712].

### Interview Trick Question: If two vectors are orthogonal, are they independent?
[cite_start]Not necessarily[cite: 715]. [cite_start]Orthogonality implies zero correlation only in certain settings[cite: 716]. [cite_start]**Statistical independence is a stronger condition[cite: 717].**

---

## 5. Cosine Similarity
[cite_start]*Extremely important for AI interviews[cite: 719].*

### Formula:
$$\text{Cosine Similarity} = \frac{x \cdot y}{\|x\| [cite_start]\|y\|}$$ [cite: 721]

### Why divide by norms?
[cite_start]To compare direction rather than magnitude[cite: 723].

### Example:
[cite_start]$x = [1, 2, 3]$ [cite: 725] [cite_start]and $y = [10, 20, 30]$ [cite: 727]
* [cite_start]They have the **same direction**[cite: 728].
* [cite_start]Their dot product differs greatly[cite: 729].
* [cite_start]Their **Cosine similarity = 1**[cite: 730]. [cite_start]Thus, they are considered identical semantically[cite: 731].

---

## 6. Matrices

### What is a Matrix?
[cite_start]A matrix is a rectangular grid of numbers[cite: 733].
* [cite_start]**Rows** = samples [cite: 734]
* [cite_start]**Columns** = features [cite: 735]

### Matrix Multiplication
[cite_start]*Interviewers ask this a lot[cite: 737].*

#### Rule:
[cite_start]If $A = (m \times n)$ [cite: 740] [cite_start]and $B = (n \times p)$ [cite: 742][cite_start], then $AB = (m \times p)$[cite: 744].  
[cite_start]*Inner dimensions must match[cite: 745].*

### Difference Between $Ax$ and $xA$
[cite_start]*Very common interview question[cite: 747].*

#### $Ax$
[cite_start]Matrix acts on vector[cite: 749]. [cite_start]$A_{(n \times n)} x_{(n \times 1)}$ [cite: 750] [cite_start]$\rightarrow Ax = (n \times 1)$[cite: 752].  
[cite_start]*This is the usual ML operation[cite: 753].*

* [cite_start]**Example (Neural Network Layer):** $$y = Wx + b$$ [cite: 756]  
  [cite_start]Weights ($W$) [cite: 758][cite_start], Input ($x$) [cite: 760][cite_start], Output ($y$)[cite: 762]. [cite_start]This is matrix-vector multiplication[cite: 763].

#### $xA$
[cite_start]Now the vector is on the left side[cite: 765]. [cite_start]$x_{(1 \times n)} A_{(n \times n)}$ [cite: 766] [cite_start]$\rightarrow xA = (1 \times n)$[cite: 768].  
[cite_start]*Different operation[cite: 769].*

#### Important:
[cite_start]Generally, $Ax \neq xA$[cite: 772]. [cite_start]Matrix multiplication is **NOT** commutative[cite: 773].

#### Interview favorite:
[cite_start]Is $AB = BA$ always true[cite: 775, 776, 777]? [cite_start]No [cite: 778][cite_start], usually $AB \neq BA$[cite: 780].

---

## 7. Matrix as a Linear Map
[cite_start]*This is where many candidates struggle[cite: 782].*

### Intuition
[cite_start]A matrix transforms vectors[cite: 784]:
[cite_start]$$\text{Input vector} \rightarrow \text{Matrix transformation} \rightarrow \text{Output vector}$$ [cite: 786, 788, 790]

### Example
[cite_start]Given $x = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$ [cite: 792] [cite_start]and matrix $A = \begin{bmatrix} 2 & 0 \\ 0 & 1 \end{bmatrix}$[cite: 794]:
[cite_start]$$Ax = \begin{bmatrix} 2 \\ 0 \end{bmatrix}$$ [cite: 796]
[cite_start]The x-coordinate got stretched[cite: 797]. [cite_start]The matrix performed a transformation[cite: 798].

### Types of Transformations
[cite_start]Matrices can[cite: 800]:
* [cite_start]**Scale:** $\begin{bmatrix} 2 & 0 \\ 0 & 2 \end{bmatrix}$ (Doubles size) [cite: 801, 802, 803]
* [cite_start]**Rotate:** $\begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}$ (Rotates points) [cite: 804, 805, 806]
* [cite_start]**Reflect:** Flip across an axis [cite: 807, 808]
* [cite_start]**Shear:** Distort shapes [cite: 809, 810]

### Why ML Cares
[cite_start]Every neural network layer ($y = Wx + b$) is a linear transformation[cite: 813, 814]. [cite_start]Deep learning is essentially[cite: 815]:
[cite_start]$$\text{Linear transform} \rightarrow \text{Nonlinearity} \rightarrow \text{Linear transform} \rightarrow \text{Nonlinearity}$$ [cite: 816, 818, 820, 822]

### Linear Map Properties
[cite_start]A transformation $A$ is linear if it satisfies[cite: 823, 824]:
1. [cite_start]**Additivity:** $A(x + y) = Ax + Ay$ [cite: 825, 826]
2. [cite_start]**Homogeneity:** $A(cx) = cAx$ [cite: 827, 828]

---

## 8. Transpose
[cite_start]*Very important[cite: 831].*

### Definition
[cite_start]Swap rows and columns[cite: 833].  
[cite_start]If $A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}$ [cite: 834][cite_start], then $A^T = \begin{bmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{bmatrix}$[cite: 836].

### Shape Change
[cite_start]$m \times n$ [cite: 838] [cite_start]becomes $n \times m$ [cite: 840]

### Why Transpose Matters
* [cite_start]**Dot Product:** $x^Ty$ is a dot product[cite: 843, 844].
* [cite_start]**Linear Regression:** Normal equation: $(X^TX)^{-1}X^Ty$[cite: 846, 847]. [cite_start]Transpose appears everywhere[cite: 848].
* [cite_start]**Backpropagation:** Gradient calculations frequently involve transposes[cite: 849, 850].

### Interview Questions
* [cite_start]**What is $(A^T)^T$?** Answer: $A$ [cite: 852, 854, 855]
* [cite_start]**What is $(AB)^T$?** Answer: $B^TA^T$ (*Order reverses*) [cite: 857, 859, 860]

---

## 9. Symmetric Matrix

### Definition:
[cite_start]$$A = A^T$$ [cite: 863]

### Example
[cite_start]$\begin{bmatrix} 1 & 2 \\ 2 & 3 \end{bmatrix}$ is symmetric[cite: 865, 866].  
[cite_start]$\begin{bmatrix} 1 & 2 \\ 5 & 3 \end{bmatrix}$ is **not** symmetric because $2 \neq 5 [cite: 867, 868, 870]$.

### Why Symmetric Matrices Matter
[cite_start]They have beautiful properties[cite: 872]:
* [cite_start]Real eigenvalues [cite: 873]
* [cite_start]Orthogonal eigenvectors [cite: 874]
* [cite_start]Numerically stable [cite: 875]

[cite_start]Many optimization problems generate symmetric matrices[cite: 876].

---

## 10. Positive Semi-Definite (PSD) Matrix
[cite_start]*Extremely important for ML[cite: 878].*

### Definition
Matrix $A$ is PSD if:
[cite_start]$$x^TAx \ge 0 \quad \text{for every vector } x$$ [cite: 880, 881, 882]
[cite_start]No matter what vector you choose, the result never becomes negative[cite: 884, 885].

### Example
[cite_start]Identity matrix $A = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$[cite: 887, 888].  
[cite_start]For any $x$: $x^TAx = x^Tx$ [cite: 889, 890][cite_start], which is a sum of squares, always $\ge 0$[cite: 891, 892]. [cite_start]Thus, the identity matrix is PSD[cite: 893].

### Positive Definite vs PSD
* [cite_start]**Positive Definite:** $x^TAx > 0$ for all non-zero vectors[cite: 895, 896, 897].
* [cite_start]**Positive Semi-Definite:** $x^TAx \ge 0$ (Can become zero)[cite: 898, 899, 900].

### Easy Interview Check
[cite_start]A symmetric matrix is **PSD** iff all eigenvalues are $\lambda_i \ge 0$[cite: 901, 902, 903].  
[cite_start]It is **Positive Definite** iff all eigenvalues are $\lambda_i > 0$[cite: 904, 905].

### Why PSD Matters in ML
* [cite_start]**Covariance Matrices:** The covariance matrix $\Sigma$ [cite: 908, 909] [cite_start]is always PSD[cite: 910]. [cite_start]Used in PCA [cite: 912][cite_start], Gaussian distributions [cite: 913][cite_start], and multivariate statistics[cite: 914].
* [cite_start]**Kernel Methods:** Kernel matrix must be PSD[cite: 916]. [cite_start]Used in Support Vector Machines [cite: 918] [cite_start]and Gaussian Processes[cite: 919].
* [cite_start]**Optimization:** Hessian matrix $H$[cite: 921, 922]. [cite_start]If PSD: local minimum[cite: 923, 924].

#### Interview Question: How do you know a critical point is a minimum?
[cite_start]Check Hessian[cite: 926, 927]. [cite_start]If Hessian is PSD $\rightarrow$ minimum[cite: 928].

---

## 11. Eigenvalues and Eigenvectors

### Core Concepts & Q&A
* [cite_start]**Why is matrix multiplication not commutative?** Because matrices represent transformations, and applying transformations in different orders generally produces different results[cite: 929, 930].
* [cite_start]**What does a matrix represent geometrically?** A linear transformation that can rotate, scale, shear, or reflect vectors[cite: 931, 932, 933].

[cite_start]Some vectors keep their direction after transformation [cite: 934][cite_start]; they only get stretched or compressed[cite: 935]. [cite_start]These special vectors are called **eigenvectors**[cite: 936].

### Formal Definition
A vector $x$ is an eigenvector of matrix $A$ if:
[cite_start]$$Ax = \lambda x$$ [cite: 938, 939]
[cite_start]where $\lambda$ is called the **eigenvalue**[cite: 941, 942].

[cite_start]**Interpretation:** Apply matrix $A$[cite: 944]. [cite_start]The vector's direction remains unchanged [cite: 945][cite_start], and only its magnitude changes[cite: 946].

### Geometric Meaning
[cite_start]Imagine a rubber sheet[cite: 949]. [cite_start]A matrix transformation stretches and distorts the sheet[cite: 950]. [cite_start]Most arrows drawn on the sheet change direction[cite: 951]. [cite_start]But a few special arrows continue pointing exactly the same way [cite: 952][cite_start]—only their length changes[cite: 953]. [cite_start]Those arrows are **eigenvectors**[cite: 954]. [cite_start]The stretching factor is the **eigenvalue**[cite: 955].

### What Does the Eigenvalue Mean?
[cite_start]Eigenvalue tells us how much stretching happens[cite: 956]:
* [cite_start]$\lambda > 1$: Stretching[cite: 958]. (e.g., $\lambda = 5 \rightarrow$ vector becomes 5 times larger) [cite_start][cite: 961, 962].
* [cite_start]$0 < \lambda < 1$: Compression[cite: 963]. (e.g., $\lambda = 0.2 \rightarrow$ vector shrinks) [cite_start][cite: 965, 966].
* [cite_start]$\lambda = 1$: No scaling[cite: 968].
* [cite_start]$\lambda = 0$: Vector collapses to zero[cite: 970].
* [cite_start]$\lambda < 0$: Direction flips[cite: 972]. (e.g., $\lambda = -3 \rightarrow$ opposite direction, 3 times larger) [cite_start][cite: 975, 977, 978].

### Why Eigenvectors Are Special
[cite_start]Most vectors change direction [cite: 980][cite_start], eigenvectors don't[cite: 981]. [cite_start]They reveal the matrix's **natural directions**[cite: 982].

### How Do We Find Eigenvalues?
[cite_start]Starting from: $Ax = \lambda x$ [cite: 984, 985]  
[cite_start]Move everything to one side: $Ax - \lambda x = 0$ [cite: 986, 987]  
[cite_start]Factor out $x$: $(A - \lambda I)x = 0$ [cite: 988, 989]  
For non-zero solutions:  
[cite_start]$$\det(A - \lambda I) = 0$$ [cite: 991]
[cite_start]This is called the **characteristic equation**[cite: 992].

---

## 12. Why ML Cares About Eigenvalues (Applications)

### PCA (Most Important Application)
[cite_start]*Interviewers love this[cite: 996].*

* [cite_start]**Problem:** Dataset may have hundreds of features [cite: 998, 999] [cite_start]and lots of redundancy[cite: 1000]. [cite_start]We want directions containing maximum information[cite: 1001].
* [cite_start]**Solution:** Compute covariance matrix [cite: 1003][cite_start], then find eigenvectors[cite: 1004].
* **Key Idea:**
  [cite_start]$$\text{Largest eigenvalue} \rightarrow \text{Corresponding eigenvector} \rightarrow \text{Direction of maximum variance}$$ [cite: 1006, 1008, 1010]
  [cite_start]$$\text{Second largest eigenvalue} \rightarrow \text{Second principal component}$$ [cite: 1011, 1013]
  [cite_start]Thus, PCA is essentially finding eigenvectors of the covariance matrix[cite: 1014, 1015].

#### Covariance Matrix Connection
[cite_start]The covariance matrix $\Sigma$ is symmetric[cite: 1017, 1018, 1019]. [cite_start]Symmetric matrices have real eigenvalues [cite: 1021] [cite_start]and orthogonal eigenvectors[cite: 1022]. [cite_start]This makes PCA stable [cite: 1023] and ensures:
* [cite_start]**Real Eigenvalues:** No weird complex numbers; easy to interpret[cite: 1085, 1086, 1087].
* [cite_start]**Orthogonal Eigenvectors:** At $90^\circ$ to each other[cite: 1091]. [cite_start]Each principal component captures new information with no overlap[cite: 1092, 1093].

### Singular Value Decomposition (SVD)
[cite_start]*Huge interview topic[cite: 1025].*

[cite_start]For matrix $A$[cite: 1026], SVD is:
[cite_start]$$A = U\Sigma V^T$$ [cite: 1029]
[cite_start]The columns of $U$ and $V$ come from eigenvectors[cite: 1030, 1034]:
* [cite_start]$V$ comes from eigenvectors of $A^TA$[cite: 1113, 1114, 1116].
* [cite_start]$U$ comes from eigenvectors of $AA^T$[cite: 1118, 1119, 1120].

#### [cite_start]SVD explains transformations in 3 steps[cite: 1095]:
1. [cite_start]**Rotate space:** $V^T$ [cite: 1097, 1098]
2. [cite_start]**Stretch along important directions:** $\Sigma$ [cite: 1100, 1101]
3. [cite_start]**Rotate again:** $U$ [cite: 1103, 1104]

#### Why ML Uses SVD:
* [cite_start]**Image Compression:** For a $1000 \times 1000$ image (1 million values) [cite: 1125, 1126][cite_start], SVD keeps only major directions to store far fewer numbers[cite: 1127, 1128].
* [cite_start]**Recommender Systems:** In a Netflix ratings matrix (Users $\times$ Movies) where most entries are missing [cite: 1130, 1131, 1132][cite_start], SVD discovers latent factors (Action lovers, Comedy lovers, Sci-fi lovers) without explicit labeling[cite: 1133, 1135, 1136, 1137, 1138].
* [cite_start]**NLP:** Used in Latent Semantic Analysis (LSA) to discover hidden word relationships before BERT and GPT[cite: 1140, 1141, 1142].

### Deep Learning Connection
[cite_start]In a neural network layer ($y = Wx$) [cite: 1041, 1042][cite_start], the weight matrix $W$ has eigenvalues[cite: 1043, 1044, 1045]:
* [cite_start]Large eigenvalues indicate strong stretching directions[cite: 1046, 1047].
* [cite_start]Small eigenvalues indicate weak directions[cite: 1048, 1049].
* [cite_start]Eigenvalues help analyze **gradient explosion**, **gradient vanishing**, and **training stability**[cite: 1050, 1051, 1052, 1053].

---

## 13. Power Iteration (Google Favorite)

### Intuition
[cite_start]Suppose a matrix has eigenvalues $\lambda_1 = 10$, $\lambda_2 = 2$ [cite: 1146] [cite_start]and eigenvectors $v_1, v_2$[cite: 1147, 1148]. [cite_start]Any vector can be written as: $x = c_1v_1 + c_2v_2$[cite: 1149, 1150]. [cite_start]Let's say $x = v_1 + v_2$[cite: 1151, 1152]:
* [cite_start]Apply $A$ once: $Ax = 10v_1 + 2v_2$ [cite: 1153, 1154]
* [cite_start]Apply again: $A^2x = 100v_1 + 4v_2$ [cite: 1155, 1156]
* [cite_start]Again: $A^3x = 1000v_1 + 8v_2$ [cite: 1157, 1158]

#### Notice:
[cite_start]The $v_1$ component is growing **MUCH** faster[cite: 1160]. [cite_start]After many multiplications: $A^kx \approx 10^k v_1$ [cite: 1161, 1162][cite_start], and the smaller component becomes negligible[cite: 1163]. [cite_start]Eventually, the vector points almost entirely along $v_1$ [cite: 1164, 1165][cite_start], which is the eigenvector of the largest eigenvalue[cite: 1166]. [cite_start]This is called the **Power Iteration Method**[cite: 1062, 1167].

### [cite_start]Q: "Why does repeated multiplication by a matrix converge to the dominant eigenvector?" [cite: 1168]
[cite_start]**Answer:** Any vector can be expressed as a combination of eigenvectors[cite: 1170]. [cite_start]After repeated multiplication, each component gets scaled by its eigenvalue raised to the power $k$[cite: 1171]. [cite_start]The component associated with the largest eigenvalue grows fastest and dominates all others[cite: 1172]. [cite_start]Therefore, the vector gradually aligns with the eigenvector corresponding to the largest eigenvalue[cite: 1173]. [cite_start]This principle is used in the Power Iteration algorithm and PCA to compute principal eigenvectors efficiently[cite: 1063, 1174].
