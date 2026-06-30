# Mexico-summer-school-2026
Quantum computing course

Project QUBO-QAOA: Bipartite Matching 4x4 (PCI Vietnam Dataset)

Dataset
Dataset Name: Provincial Competitiveness Index (PCI) Vietnam 2024-2025
.
Official Source: PCI Vietnam
.
Responsible Institution: Vietnam Chamber of Commerce and Industry (VCCI) and USAID
.
Source URL: https://pcivietnam.vn/report-2025#sub-indices
.
Raw CSV URL: (Insert your GitHub Raw URL here, e.g., https://raw.githubusercontent.com/user/repo/main/data/dataset_real_4x4.csv)
.
License/Terms of use: Publicly available for research and educational purposes
.
Consultation Date: June 30, 2026.
Problem Domain: Economics and Public Policy.
Modeling
Set A (Provinces): 4 selected Vietnamese provinces: An Giang, Đà Nẵng, Hưng Yên, and Tuyên Quang
.
Criteria for A: Selected to represent different economic regions and varying competitiveness levels.
Set B (Sub-indices): 4 key competitiveness indicators: CSTP01 (Entry Costs), CSTP04 (Time Costs), CSTP05 (Informal Charges), and CSTP08 (Legal Institutions)
.
Criteria for B: Selected based on their high impact on the local business environment.
Definition of x 
ij
​
 =1: Province i is specifically matched to excel or receive focused support for indicator j
.
Interpretation of x 
ij
​
 =0: Province i is not matched with indicator j
.
Score Matrix
Columns used: Entry Costs, Time Costs, Informal Charges, and Legal Institutions
.
Exact formula of S 
ij
​
 : S 
ij
​
 =Competitiveness Score provided by the PCI report
.
Normalization: Since PCI scores are already standardized on a scale of 1-10 by VCCI, they are used directly to maintain data integrity
.
Matrix S 4x4: | Province \ Index | B1 | B2 | B3 | B4 | | :--- | :---: | :---: | :---: | :---: | | An Giang | 6.11 | 8.42 | 7.41 | 6.65 | | Đà Nẵng | 8.70 | 8.20 | 7.61 | 7.82 | | Hưng Yên | 7.26 | 7.31 | 8.09 | 6.55 | | Tuyên Quang| 6.50 | 6.86 | 7.67 | 7.94 |
Constraints
Row Constraint: Each province must be assigned to exactly one indicator: ∑ 
j=1
4
​
 x 
ij
​
 =1
.
Column Constraint: Each indicator must be assigned to exactly one province: ∑ 
i=1
4
​
 x 
ij
​
 =1
.
Bipartite Matching Justification: The problem involves finding a one-to-one correspondence between two disjoint sets (Provinces and Economic Indicators) to maximize the total competitiveness benefit
.
QUBO Formulation Justification: The problem is modeled as a QUBO by transforming the maximization of scores into a minimization of negative scores, adding quadratic penalty terms (λ) to enforce row and column constraints
.
Results
Exact Classical Solution: Calculated via brute force/permutations of 24 feasible assignments
.
Local QAOA Result: Obtained through local simulation with p=1
.
Comparison: Local QAOA identifies the optimal classical solution with a specific probability, demonstrating the effectiveness of the cost and mixer operators
.
Hybrid Post-processing: Classical repair (using linear_sum_assignment) was applied to ensure the final output is a feasible 1-to-1 matching
.
Ethics and Limitations
Ethical Risks: Potential misuse of this simplified model to make real-world policy decisions
.
Mitigation: Explicitly labeling this project as "Educational" and using aggregated, publicly available macro-economic data
.
Model Limitations: The 4×4 instance is a small simplification and does not capture the full complexity of inter-provincial economic dynamics or regional synergies
.
Execution
Instructions: Open proyecto_qubo_qaoa.ipynb in Google Colab. Ensure the data/ folder is accessible or use the Raw CSV URL provided above. Run all cells in order
