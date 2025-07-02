# Toric Code Simulation under Random Pauli Errors

## Overview
This Jupyter Notebook (`Batch3__Kitaev’s_toric_code_under__random_Pauli_error_.ipynb`) implements a simulation of Kitaev's toric code, a topological quantum error-correcting code, on a k × k lattice. The simulation evaluates the code's performance under random Pauli errors (X, Y, Z) using Qiskit and performs error correction via minimum-weight perfect matching with NetworkX. The code measures the success probability of maintaining the logical state for varying error probabilities.

## Features
- **Toric Code Initialization**: Prepares a k × k toric code lattice in a specified logical state (default |00⟩_L) using Hadamard and CNOT gates.
- **Stabilizer Measurements**: Measures vertex (X-type) and plaquette (Z-type) stabilizers to detect errors.
- **Error Model**: Applies random Pauli errors (X, Y, Z) with equal probabilities to data qubits using Qiskit's noise model.
- **Error Correction**: Uses minimum-weight matching (via NetworkX) to decode syndromes and apply recovery operations.
- **Logical Measurements**: Measures logical Z operators to verify the logical state post-correction.
- **Parallel Simulation**: Runs simulations for a range of error probabilities using Joblib for parallelization.
- **Visualization**: Plots the success probability as a function of error probability.

## Dependencies
- Python 3.x
- Qiskit (`qiskit`, `qiskit-aer`): For quantum circuit simulation and noise modeling.
- NumPy: For numerical operations.
- Matplotlib: For plotting results.
- NetworkX: For minimum-weight matching in error correction.
- Joblib: For parallelizing simulations.

Install dependencies using:
```bash
pip install qiskit qiskit-aer numpy matplotlib networkx joblib
```

## Usage
1. **Run the Notebook**:
   - Open the notebook in a Jupyter environment (e.g., JupyterLab, Google Colab).
   - Execute all cells to run the simulation with default parameters (lattice size k=5, logical state |00⟩_L, error probabilities from 0.01 to 0.2, 50 shots per simulation).

2. **Key Functions**:
   - `initialize_toric_code(circuit, k, logical_state)`: Initializes the toric code with a specified logical state.
   - `measure_stabilizers(circuit, k)`: Measures vertex and plaquette stabilizers.
   - `apply_recovery(circuit, k, syndromes)`: Applies recovery operations using minimum-weight matching.
   - `measure_logical(circuit, k)`: Measures logical Z operators.
   - `run_single_simulation(error_prob, lattice_size, logical_state, shots, sim_engine)`: Simulates one error probability.
   - `simulate_toric_code(...)`: Runs simulations over a range of error probabilities and plots results.

3. **Customization**:
   - Modify `lattice_size` (default: 5) to change the k × k lattice size.
   - Adjust `logical_state` (default: "00") to simulate states like |01⟩_L, |10⟩_L, or |11⟩_L.
   - Change `p_min`, `p_max`, and `num_points` to adjust the range and granularity of error probabilities.
   - Increase `shots` for higher statistical accuracy.

4. **Output**:
   - A plot showing the success probability (correct logical state) vs. error probability.
   - Arrays `error_probs` and `success_probs` containing the simulation results.

## Notes
- The simulation assumes a simplified qubit indexing for the toric code lattice. In a real implementation, ensure proper periodic boundary conditions for a toroidal lattice.
- The recovery step is simulated classically for efficiency, as applying recovery operations within the quantum circuit is computationally intensive.
- The code uses the `stabilizer` method in `AerSimulator` for efficient simulation of stabilizer circuits.
- For larger lattices or more shots, consider increasing computational resources due to memory and runtime constraints.

## Example
To run a simulation with a 4 × 4 lattice, logical state |11⟩_L, and 100 shots:
```python
error_probs, success_probs = simulate_toric_code(lattice_size=4, logical_state="11", shots=100)
```

## Limitations
- The current implementation simplifies qubit indexing, which may not fully account for toroidal boundary conditions.
- The error model applies Pauli errors only to identity gates for simplicity; real implementations may require noise on all gates.
- The minimum-weight matching assumes Manhattan distances, which is a simplification for the toric code's error chains.

## License
This project is provided for educational and research purposes. Ensure compliance with the licenses of dependencies (e.g., Qiskit, NetworkX).