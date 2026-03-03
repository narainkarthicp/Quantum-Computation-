# My Understanding: Towards Quantum SVM

---

## 1. Problem Setup: Linear Classification

The fundamental goal of a Support Vector Machine (SVM) is to classify data points by finding an optimal boundary (hyperplane).

- **Input Data**:  $x \in \mathbb{R}^d$ where $d$ is the number of features  
- **Labels**: Binary classification using $y \in \{+1, -1\}$  
- **Objective**: Identify the hyperplane that separates these classes with the **maximum possible margin**

---

## 2. Decision Boundary and Geometry

The hyperplane is mathematically defined by its orientation ($w$) and its position ($b$) in the feature space.

- **Weight Vector ($w$)**: Determines the orientation and reflection of the boundary  
- **Bias ($b$)**: Shifts the hyperplane from the origin $(0,0)$  
- **Fundamental Constraint**:

$$
y_i(w \cdot x_i + b) \ge 1
$$

### Classification Regions

| Case                 | Mathematical Condition        | Data Position                         |
|----------------------|------------------------------|---------------------------------------|
| **Margin Edge (SV)** | $y_i(w \cdot x_i + b) = 1$   | Lies exactly on the margin boundary   |
| **Positive Side**    | $y_i(w \cdot x_i + b) > 1$   | Lies within the positive class region |
| **Negative Side**    | $y_i(w \cdot x_i + b) < 1$   | Lies within the negative class region |

---

## 3. Objective Function

The goal is to maximize the margin width (distance between the two edges).

- **Margin Width**:

$$
\frac{2}{\|w\|}
$$

- **Optimization Objective**:

$$
\min \frac{1}{2} \|w\|^2 
\quad \text{subject to} \quad 
y_i(w \cdot x_i + b) \ge 1
$$

- **Support Vectors (SV)**: Only these points define the hyperplane  
- **Hard Margin**: Strict separation required  
- **Soft Margin**: Allows tolerance for misclassification (noise handling)

---

## 4. The Kernel Trick: Handling Non-Linearity

When data cannot be separated linearly in its original space, we use a **feature map**.

- **Dimension Lifting**: Map data to a higher-dimensional space  
- **Efficiency Problem**: Explicit mapping is computationally heavy  
- **Kernel Trick**: Compute only inner products in high dimension  
- **Gram Matrix**: Similarity matrix built from kernel values

### Example: Polynomial Kernel

Feature map:

$$
\phi(x) = (x_1^2, x_2^2, \sqrt{2}x_1x_2)
$$

Kernel:

$$
K(A, B) = (A \cdot B)^2
$$

If:

- $A = (1, 2)$  
- $B = (3, 4)$  

Inner product:

$$
(1 \times 3) + (2 \times 4) = 11
$$

Kernel result:

$$
11^2 = 121
$$

---

# Quantum World

---

## 5. The Balancing Act: Qubits vs. Noise

Navigating hardware limits of current quantum computing.

- **Qubit Dilemma**: More qubits → more decoherence and noise  
- **Gate Dilemma**: Deeper circuits → cumulative gate errors  
- **Optimization Failure**: Leads to **barren plateaus** (flat gradients)

---

## 6. Pre-Processing: The Gateway to Orthogonality

Refining classical data before quantum encoding.

- **Standard Scaling**: Normalizes feature ranges  
- **PCA (Principal Component Analysis)**:
  - Produces **orthogonal components**
  - Reduces dimensionality
  - Keeps circuits shallow and stable
  - Improves separability of quantum states $|\psi(x_i)\rangle$

---

## 7. Entering the Quantum World: The $[0, \pi]$ Map

Mapping classical data to rotations on the Bloch sphere.

- **$[0, \pi]$ Constraint**: Ensures unique mapping to physical states  
- **Encoding Logic**:
  - $0$ → North Pole ($|0\rangle$)
  - $\pi$ → South Pole ($|1\rangle$)
- **Independence**: Qubits remain unentangled at this stage

---

## 8. From Bloch Sphere to Hilbert Space

Transitioning to full quantum feature space.

- **Entanglement Trigger**: Apply CNOT gates  
- **Unified Space**: Move from separate Bloch spheres to shared Hilbert space  
- **Exponential Dimension**:

$$
2^n
$$

Creates space for linear separation of complex data.

---

## 9. Hybrid Logic: Quantum + Classical

Strategic division of responsibilities.

### Quantum Role

Compute kernel matrix via state overlap:

$$
K(x_i, x_j) = |\langle \psi(x_i) | \psi(x_j) \rangle|^2
$$

### Classical Role

- Perform convex optimization  
- Compute final hyperplane efficiently  

---

## 10. Application: Quantum Object Tracking

Applying Hilbert space representation to video inference.

- **Challenge**: Overlapping objects and hidden features in 2D frames  
- **Goal**: Use quantum feature mapping for improved separation  

---

## 11. The "Noise" Barrier: Hardware Reality

Current physical hardware limitations:

- **Fragility Problem**: Decoherence due to heat/vibrations  
- **Gate Errors**: ~1% error rate per quantum gate  
- **Scaling Problem**: ~1,000 physical qubits required for 1 logical qubit  

---

## 12. Leading Quantum Software Tools

- **Qiskit (IBM)**  
  - Industry standard for circuit building  
  - Includes `qasm_simulator`

- **PennyLane**  
  - Built for Quantum Machine Learning  
  - Integrates with PyTorch and TensorFlow  

- **AWS Braket**  
  - Unified interface for multiple quantum hardware backends  

---