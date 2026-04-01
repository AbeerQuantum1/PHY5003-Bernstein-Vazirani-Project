# Bernstein-Vazirani Algorithm — PHY5003 Quantum Software

A complete implementation, testing, and analysis of the **Bernstein-Vazirani (BV) algorithm** for the PHY5003 Quantum Software course at La Trobe University.

## Algorithm Overview

The Bernstein-Vazirani algorithm solves the following problem: given a black-box oracle that computes f(x) = **s · x** mod 2 for an unknown secret string **s**, determine **s** using as few queries as possible.

| Approach | Oracle Queries | Complexity |
|----------|---------------|------------|
| Classical | n (one per bit) | O(n) |
| Quantum (BV) | **1** | **O(1)** |

The quantum algorithm achieves this strict linear query reduction using superposition, phase kickback, and interference.
## Repository Structure

```
├── README.md                         ← You are here
├── BV_Complete_Project.ipynb         ← All code, tests, and analysis in one notebook

```

## Notebook Contents

The single Jupyter notebook `BV_Complete_Project.ipynb` contains all deliverables, organized as follows:

1. **Qiskit Implementation** — Quantum circuit construction, example run with s=101, histogram visualization
2. **OpenQASM Output** — Assembly code generation + line-by-line explanation table
3. **Classical Equivalent** — Python dot-product oracle + solver with detailed code commentary
4. **Performance Comparison** — Query complexity O(1) vs O(n) charts + execution time benchmarks
5. **Circuit Statistics** — Depth, gate count, qubit scaling analysis
6. **Q# Implementation** — Microsoft QDK implementation via `qsharp` Python package
7. **Quantum Supremacy Analysis** — Noise modeling, error threshold estimation, conditions for advantage
8. **Unit Tests** — 19 tests covering Classical, Qiskit, and Q# implementations

## Implementations

### Qiskit (Python)
- Full quantum circuit construction (`build_bv_circuit`)
- Simulation with AerSimulator (1024 shots)
- OpenQASM 2.0 export with line-by-line explanation
- Circuit visualization and histogram output

### Q# (Microsoft QDK)
- Q# operations via `%%qsharp` magic cells and `qsharp.eval()`
- `BVOracle` and `RunBV` operations
- Verification with test cases

### Classical Equivalent (Python)
- `classical_oracle(secret, x)`: computes f(x) = s · x mod 2
- `classical_bv(secret)`: recovers s using n queries (one bit at a time)
- Benchmarked against the quantum simulator

## How to Run

### Prerequisites
```bash
pip install qiskit qiskit-aer matplotlib pylatexenc numpy
pip install qsharp
```

### Running the notebook
```bash
jupyter notebook BV_Complete_Project.ipynb
```
Run all cells top to bottom. The notebook is fully self-contained.

## Test Suite

| Category | Tests | Coverage |
|----------|-------|----------|
| Classical Oracle | 3 | Dot product correctness, unit vectors, zero-secret edge case |
| Classical BV | 4 | Known secrets, all-zeros, all-ones, random inputs |
| Qiskit Structure | 4 | Circuit dimensions, essential gates, CNOT count, measurements |
| Qiskit Execution | 3 | Known + edge secrets with determinism, random, quantum = classical |
| Q# Execution | 5 | Known + longer secrets, edge cases, Q# = classical, Q# = Qiskit |
| **Total** | **19** | |

## Quantum Supremacy Analysis

- Circuit resource scaling (qubits, depth, gates vs n)
- Noise impact simulation using depolarizing error model
- Error threshold calculation: max tolerable error rate for given n and success probability
- Discussion of the oracle problem and what "quantum advantage" means for BV
- Conclusion: BV provides a provable query advantage (O(1) vs O(n)) but not practical supremacy, since classical O(n) is already efficient

## Key Results

- **Correctness:** All implementations recover the secret string with 100% accuracy on the ideal simulator.
- **Query advantage:** Quantum uses 1 query vs n classical queries — verified experimentally.
- **Noise tolerance:** For n=100 qubits at 90% success, gate error must be < 0.1% per qubit.
- **Cross-consistency:** Qiskit, Q#, and classical implementations produce identical results on all test cases.

## Technologies Used

- **Qiskit 2.3** + Qiskit Aer (IBM)
- **Q# / qsharp 1.16** (Microsoft)
- **Python 3.13** with NumPy, Matplotlib
- **Jupyter Notebook**

## Course Information

- **Course:** PHY5003 Quantum Software
- **Institution:** La Trobe University
- **Date:** March 2026

## License

This project is submitted as academic coursework for PHY5003.
