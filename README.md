# HPC Simulation of Exciton Dynamics in 2D Materials

> **Research Project @ Ural Federal University (2024-2025)**
> *Focus: High-Performance Computing, MPI, Computational Physics*

## 🎯 Objective
Simulate ultrafast electron dynamics in Hexagonal Boron Nitride (hBN) to study exciton formation. The challenge was to solve the Liouville-von Neumann equation for a large grid ($300 \times 300$ k-points), which is computationally impossible on a single CPU.

## ⚙️ Technical Solution (Architecture)
To solve this, I optimized the **EDUS** codebase for a supercomputer cluster using a hybrid parallelization strategy.

### 1. Hybrid Parallelism (MPI + OpenMP)
*   **Inter-node communication (MPI):** The Brillouin zone (k-grid) was decomposed into domains. Each MPI process handled a specific subset of k-points.
*   **Intra-node acceleration (OpenMP):** Inside each node, calculations were parallelized across CPU cores.

### 2. K-Grid Decomposition Strategy
*   Implemented a cyclic distribution scheme to balance the load between nodes.
*   Classified grid points into **Central**, **Border**, and **External** to optimize data exchange and minimize MPI communication overhead.

### 3. Mathematical Optimization
*   Replaced direct $O(N^2)$ Coulomb summation with a **Fourier Transform approach**, reducing complexity to $O(N \log N)$.
*   Implemented the **Rytova-Keldysh potential** to correctly account for 2D dielectric screening.

## 📊 Key Results
The simulation successfully reproduced the formation of excitonic peaks in the absorption spectrum, matching theoretical predictions.

### Performance
*   Scaling: Achieved near-linear speedup on the university cluster (up to X nodes).
*   Physics: Demonstrated that dielectric screening ($r_0$, $\varepsilon$) significantly shifts the exciton binding energy (by ~0.5–1 eV).

![Results Visualization](results/spectra_comparison.jpg)

## 🛠️ Tools Used
*   **C++ / MPI / OpenMP** — Core simulation logic.
*   **Python (NumPy, Matplotlib)** — Data post-processing and visualization.
*   **Linux (Debian)** — Cluster environment configuration.

