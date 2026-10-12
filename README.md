# QAOA-Based Portfolio Optimization Using Qiskit

A quantum optimization project exploring the Quantum Approximate Optimization Algorithm (QAOA) for selecting a fixed-size portfolio of synthetic stocks.

## Project Overview

This project formulates a portfolio selection problem as a binary optimization problem and investigates how QAOA performs under different circuit depths and penalty strengths.

**Problem setup**
- Number of assets: 6
- Required portfolio size: 3
- Risk parameter: \(q = 0.5\)
- Random seed: 2026

## Objective Function

The objective is to minimize:

\[
C(x)=q\,x^T\Sigma x-\mu^Tx+
\lambda\left(\sum_{i=1}^{n}x_i-K\right)^2
\]

Where:
- \(x_i \in \{0,1\}\) indicates whether an asset is selected.
- \(\mu\) represents synthetic expected returns.
- \(\Sigma\) is a positive-semidefinite covariance-like matrix.
- \(K=3\) is the required number of selected assets.
- \(\lambda\) penalizes portfolios that violate the cardinality constraint.

## Project Workflow

1. **Classical benchmark:** Enumerate all 64 possible portfolios and identify the best feasible portfolio.
2. **Hamiltonian construction:** Convert the binary objective into a Pauli-based cost Hamiltonian.
3. **QAOA simulation:** Run QAOA using Qiskit and a local simulator.
4. **Depth experiments:** Compare circuit depths \(p=1,2,3,4\).
5. **Penalty experiments:** Evaluate penalty strengths from \(\lambda=0.05\) to \(\lambda=5.0\).

## Key Experimental Results

- Best feasible bitstring: `011001`
- Best feasible objective value: approximately `-0.50301469`
- Best observed approximation ratio in the depth experiment: `0.980765` at \(p=2\).
- Best observed feasibility fraction in the penalty sweep: `97.1%` at \(\lambda=1.0\).
- Maximum absolute difference in the Hamiltonian validation: approximately \(2.998 \times 10^{-15}\), across all 64 bitstrings.

These results are specific to the chosen synthetic instance and simulation settings.

## Repository Structure

```text
qaoa-portfolio-optimization/
├── 01_classical_benchmark.ipynb
├── 02_portfolio_hamiltonian.ipynb
├── 03_portfolio_qaoa.ipynb
├── 04_depth_experiments.ipynb
├── 05_penalty_experiments.ipynb
├── QAOA_Portfolio_Optimization_Final_8_Slides.pdf
├── README.md
└── .gitignore
```

## Requirements

- Python 3.12
- Qiskit
- NumPy
- SciPy
- Matplotlib
- Jupyter Notebook
- Qiskit Aer, if used by the selected simulator configuration

Install the dependencies in your Python environment as needed. For reproducibility, record the exact package versions used to run the notebooks.

## Running the Project

Run the notebooks in numerical order, from `01_classical_benchmark.ipynb` through `05_penalty_experiments.ipynb`.

Restart the kernel and execute each notebook from top to bottom to reproduce the experiments.

The experiments use local simulation and do not require an IBM Quantum API key.

## Limitations

- The problem contains only six synthetic assets.
- Results depend on optimizer initialization, iteration limits, circuit depth, and sampling.
- Higher approximation ratios do not guarantee that the optimal bitstring will be sampled frequently.
- These experiments do not establish a quantum advantage over classical optimization.

## Conclusion

This project demonstrates an end-to-end workflow for modeling a constrained portfolio problem, constructing its cost Hamiltonian, simulating QAOA, and evaluating the effects of circuit depth and penalty strength.

## Acknowledgements

Prepared as a project for Qiskit Fall Fest x IIIT Delhi, Track 2: Quantum Optimization.

Educational and research use.
