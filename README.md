# Mexico-summer-school-2026
Quantum computing course

# Project QUBO-QAOA: Bipartite Matching 4x4 (PCI Vietnam Dataset)

## 1. Dataset
- **Dataset Name:** Provincial Competitiveness Index (PCI) Vietnam 2024-2025.
- **Official Source:** PCI Vietnam.
- **Responsible Institution:** Vietnam Chamber of Commerce and Industry (VCCI) and USAID.
- **Source URL:** [https://pcivietnam.vn/report-2025#sub-indices](https://pcivietnam.vn/report-2025#sub-indices)
- **Consultation Date:** June 30, 2026.
- **Problem Domain:** Economics and Public Policy.

## 2. Modeling
We define two sets of size 4:
- **Set A (Provinces):** $A = \{a_1, a_2, a_3, a_4\}$ representing An Giang, Đà Nẵng, Hưng Yên, and Tuyên Quang.
- **Set B (Indicators):** $B = \{b_1, b_2, b_3, b_4\}$ representing Entry Costs, Time Costs, Informal Charges, and Legal Institutions.

**Binary Variable $x_{ij}$:**
Each binary variable indicates whether a match is chosen between province $a_i$ and indicator $b_j$:
$$
x_{ij}=\begin{cases}
1, & \text{if province } a_i \text{ is matched to indicator } b_j \\
0, & \text{otherwise}
\end{cases}
$$

**Score Matrix $S_{ij}$:**
The matrix $S \in \mathbb{R}^{4 \times 4}$ contains the competitiveness scores from the PCI report:
$S_{ij} = \text{Score of province } a_i \text{ in indicator } b_j$.

## 3. Score Matrix Table
| Province \ Indicator | B1 (Entry) | B2 (Time) | B3 (Informal) | B4 (Legal) |
| :--- | :---: | :---: | :---: | :---: |
| **An Giang (A1)** | 6.11 | 8.42 | 7.41 | 6.65 |
| **Đà Nẵng (A2)** | 8.70 | 8.20 | 7.61 | 7.82 |
| **Hưng Yên (A3)** | 7.26 | 7.31 | 8.09 | 6.55 |
| **Tuyên Quang (A4)** | 6.50 | 6.86 | 7.67 | 7.94 |

## 4. Objective and Constraints
The objective is to find a one-to-one matching that maximizes the total score:
$$ \max_x \sum_{i=1}^{4}\sum_{j=1}^{4} S_{ij}x_{ij} $$

**Constraints:**
- **Row Constraint:** Each province must be assigned exactly once: $\sum_{j=1}^{4} x_{ij}=1, \forall i \in \{1,2,3,4\}$.
- **Column Constraint:** Each indicator must be assigned exactly once: $\sum_{i=1}^{4} x_{ij}=1, \forall j \in \{1,2,3,4\}$.

## 5. QUBO Formulation
To solve this on a quantum computer, we transform the problem into a Quadratic Unconstrained Binary Optimization (QUBO) model by minimizing the energy function $E(x)$:
$$
E(x) = -\sum_{i=1}^{4}\sum_{j=1}^{4} S_{ij}x_{ij} + \lambda_A\sum_{i=1}^{4}\left(\sum_{j=1}^{4} x_{ij}-1\right)^2 + \lambda_B\sum_{j=1}^{4}\left(\sum_{i=1}^{4} x_{ij}-1\right)^2
$$
- The first term rewards high PCI scores.
- The terms with $\lambda_A$ and $\lambda_B$ penalize violations of the matching constraints.

## 6. Justification
- **Why Bipartite Matching?** This model represents a strategic allocation where each province is paired with a specific economic area for focused improvement. A 1-to-1 matching ensures resources are distributed efficiently without overlap.
- **Why QUBO?** QUBO allows us to map the discrete decision variables directly to qubits. By setting penalty weights $(\lambda)$ higher than the maximum possible score, the ground state of the Hamiltonian corresponds to a feasible and optimal economic assignment.

## 7. Results and Comparison
- **Exact Classical Solution:** Obtained via brute-force search of all $4! = 24$ feasible permutations.
- **Local QAOA Result:** Executed using a local simulator with $p=1$.
- **Comparison:** QAOA demonstrates the ability to amplify the probability of the optimal state. Any non-feasible bitstrings observed are handled via hybrid post-processing (classical repair).

## 8. Ethics and Limitations
- **Ethical Warning:** This project is for educational purposes only. The results should not be used for real-world public policy or resource allocation.
- **Mitigation:** We use aggregated, publicly available macro-economic data (PCI) which does not contain sensitive personal information.
- **Limitations:** The $4 \times 4$ scale is a simplification. Real economic development involves more complex, non-linear inter-dependencies that are not captured in this basic matching model.

## 9. Execution
1. Open `proyecto_qubo_qaoa.ipynb` in Google Colab.
2. Ensure the file `data/dataset_real_4x4.csv` is uploaded to the environment.
3. Run all cells in order (`Runtime -> Run all`).
