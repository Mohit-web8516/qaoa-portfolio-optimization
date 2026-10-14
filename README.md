# QAOA-Based Portfolio Optimization Using Qiskit ⚛️📈

An end-to-end quantum optimization project exploring the **Quantum Approximate Optimization Algorithm (QAOA)** for fixed-size portfolio selection using synthetic stock data.

The project investigates how a combinatorial portfolio optimization problem can be formulated mathematically, translated into a Hamiltonian, and explored using QAOA. It also includes classical benchmarking and experiments examining circuit depth and penalty parameters.

## 🎯 Project Overview

Portfolio optimization involves selecting assets while balancing potential returns against risk. When the portfolio must contain a fixed number of assets, the selection problem becomes a discrete optimization task.

This project explores a QAOA-based approach to selecting a fixed-size portfolio from a synthetic stock universe.

### Key objectives

- Formulate portfolio selection as a binary optimization problem.
- Construct a portfolio cost function that balances expected returns and risk.
- Encode the optimization objective into a Hamiltonian.
- Apply QAOA to generate candidate portfolios.
- Compare quantum optimization results with a classical benchmark.
- Investigate the effects of circuit depth and penalty parameters.
- Understand the practical limitations of quantum optimization.

## 🧠 Mathematical Formulation

Let \(n\) be the number of available assets, and let \(x_i\) represent whether asset \(i\) is selected:

\[
x_i \in \{0,1\}
\]

where \(x_i=1\) means the asset is selected and \(x_i=0\) means it is not selected.

A common mean–variance-style objective for fixed-size portfolio selection is:

\[
\min_x \left(\lambda x^\top\Sigma x-\mu^\top x\right)
\]

subject to:

\[
\sum_{i=1}^{n}x_i=k
\]

where:

- \(x\): binary asset-selection vector.
- \(\mu\): expected-return vector.
- \(\Sigma\): covariance matrix of asset returns.
- \(\lambda\): risk–return trade-off parameter.
- \(k\): required number of selected assets.

The precise objective, parameter scaling, and constraint handling should match the implementation in the project notebooks.

### QUBO formulation

The binary optimization problem can be expressed as a Quadratic Unconstrained Binary Optimization (QUBO) problem.

A fixed-size constraint can be incorporated using a penalty term:

\[
P\left(\sum_{i=1}^{n}x_i-k\right)^2
\]

where \(P\) controls the penalty applied to portfolios that violate the selection constraint.

The resulting binary objective can be mapped to a Hamiltonian suitable for quantum optimization.

## ⚛️ How QAOA Works

The Quantum Approximate Optimization Algorithm combines a parameterized quantum circuit with a classical optimization procedure.

The workflow is:

1. **Prepare the problem:** Construct the portfolio objective and encode asset-selection decisions as binary variables.
2. **Build the Hamiltonian:** Translate the objective and applicable constraints into a form suitable for quantum computation.
3. **Initialize the circuit:** Prepare a quantum state representing candidate solutions.
4. **Apply QAOA layers:** Alternate cost and mixer operations using adjustable circuit parameters.
5. **Measure candidate solutions:** Obtain bitstrings representing candidate portfolios.
6. **Evaluate the candidates:** Calculate their objective values and check portfolio constraints.
7. **Optimize the parameters:** Use a classical optimizer to improve the QAOA parameters based on the measured results.

The aim is to obtain high-quality candidate portfolios. QAOA does not guarantee that every run will find the global optimum.

## 📂 Project Structure

The repository is organized around five experiment notebooks and a project report or supporting artifact.

```text
qiskit-track2/
│
├── README.md
├── .gitignore
│
├── 01_classical_benchmarking.ipynb
├── 02_portfolio_hamiltonian.ipynb
├── 03_portfolio_qaoa.ipynb
├── 04_depth_experiments.ipynb
├── 05_penalty_experiments.ipynb
│
└── QAOA_Portfolio_Optimization...
```

The final filename above is abbreviated to match the VS Code screenshot; replace it with the actual filename if you document it separately.

### Notebook guide

| Notebook | Purpose |
|---|---|
| `01_classical_benchmarking.ipynb` | Establish a classical reference for evaluating portfolio-selection solutions. |
| `02_portfolio_hamiltonian.ipynb` | Explore the portfolio objective and its Hamiltonian representation. |
| `03_portfolio_qaoa.ipynb` | Implement the main QAOA portfolio optimization workflow. |
| `04_depth_experiments.ipynb` | Investigate how QAOA circuit depth affects optimization behaviour. |
| `05_penalty_experiments.ipynb` | Explore the effect of penalty parameters on constraint satisfaction and solution quality. |

The exact contents and outcomes of each notebook should be confirmed from the executed experiments.

## 🛠️ Technology Stack

- **Python** — implementation and numerical computation
- **Qiskit** — quantum circuit construction and execution
- **QAOA** — approximate combinatorial optimization
- **NumPy** — numerical operations and array processing
- **Jupyter Notebook** — experiments, analysis, and visualization

Additional dependencies should be documented based on the imports used by the notebooks.

## 🚀 Getting Started

### Prerequisites

- Python installed on your system
- pip
- Git
- A compatible version of Qiskit and the libraries used in the notebooks

### 1. Clone the repository

```bash
git clone https://github.com/Mohit-web8516/qaoa-portfolio-optimization.git
cd qaoa-portfolio-optimization
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

If a `requirements.txt` file is available, install the recorded dependencies:

```bash
pip install -r requirements.txt
```

Otherwise, install the packages required by the notebooks. For example:

```bash
python -m pip install qiskit numpy jupyter matplotlib
```

Use the versions compatible with the actual project code. Do not assume this example command captures every dependency.

### 4. Open the notebooks

Start Jupyter:

```bash
jupyter notebook
```

Alternatively, open the repository in VS Code and select the Python environment containing the project dependencies.

### 5. Execute the experiments

Run the notebooks in numerical order, beginning with classical benchmarking and proceeding through Hamiltonian construction, QAOA implementation, circuit-depth experiments, and penalty experiments.

Execute cells in order so that variables and intermediate results are defined before they are used.

## 📊 Evaluation and Experiments

The repository includes notebooks for examining several important aspects of portfolio optimization.

### Classical benchmarking

A classical reference provides a basis for evaluating the quality of candidate portfolios produced by QAOA.

### Hamiltonian construction

The portfolio objective is translated into a quantum-optimization representation, connecting the mathematical model with the circuit implementation.

### QAOA optimization

The main experiment investigates candidate portfolios generated using a parameterized quantum circuit and a classical optimization loop.

### Circuit-depth experiments

Changing QAOA depth changes the number of alternating cost and mixer layers. Experiments can examine whether additional layers improve candidate quality and how they affect circuit complexity.

### Penalty experiments

Penalty strength influences how strongly invalid portfolio selections are discouraged. Experiments can examine the trade-off between constraint satisfaction and the quality of the underlying objective.

### Recommended evaluation metrics

- Best objective value obtained.
- Whether the fixed-size portfolio constraint is satisfied.
- Quality relative to a classical reference.
- Distribution of measured candidate bitstrings.
- Effect of QAOA depth on solution quality.
- Sensitivity to penalty strength and optimizer settings.

**Experimental results:** Add numerical results, plots, and conclusions after verifying the outputs produced by the notebooks. No performance figures or quantum advantage claims are assumed in this README.

## ⚠️ Limitations

- Synthetic stock data does not represent the full complexity of real financial markets.
- QAOA is a heuristic optimization method and is not guaranteed to return a globally optimal portfolio.
- Results depend on the objective formulation, constraint penalties, circuit depth, classical optimizer, and measurement sampling.
- Increasing circuit depth can increase computational cost and sensitivity to noise on quantum hardware.
- Small portfolio problems can often be solved effectively using classical optimization techniques.
- Demonstrating the practical usefulness of QAOA requires comparison against suitable classical baselines.

## 🔮 Potential Future Improvements

- Add a reproducible classical-versus-QAOA comparison.
- Record the best objective value and constraint-satisfaction rate across multiple runs.
- Compare different QAOA depths and classical optimizers.
- Investigate alternative penalty strengths systematically.
- Add visualizations of candidate portfolios and measured bitstring distributions.
- Explore larger problem instances and assess how resource requirements scale.


