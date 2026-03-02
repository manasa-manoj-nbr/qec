# Quantum Error Correction Simulator

**Shor's 9-Qubit Code | Syndrome Detection | Logical vs Physical Error Rates**

---

## What's Inside

| File                         | Description                                     |
| ---------------------------- | ----------------------------------------------- |
| `shor_qec.ipynb`             | Main simulator notebook (9 sections)            |
| `syndrome_visualization.png` | Heatmap + qubit grid + shot histogram           |
| `error_rate_benchmark.png`   | Log-log error rate sweep + fidelity improvement |

---

## Concepts Covered

### Codes Implemented

- **3-qubit bit-flip repetition code** — protects against X errors
- **3-qubit phase-flip repetition code** — protects against Z errors in |+/-> basis
- **Shor's 9-qubit code** — concatenated code correcting any single-qubit error (X, Y, or Z)

### Noise Models

- Depolarizing channel on single-qubit gates
- Depolarizing channel on CNOT gates (10× single-qubit rate)
- Readout (measurement) bit-flip noise

### Syndrome Extraction

- 8 ancilla qubits measuring parity without collapsing the logical state
- Z-type (bit-flip) syndromes: 2 per inner block × 3 blocks = 6 bits
- X-type (phase-flip) syndromes: 2 across outer blocks

---

## Quick Start

```bash
pip install qiskit qiskit-aer matplotlib numpy
jupyter notebook shor_qec.ipynb
```

---

## Key Results

| Metric                     | Value                                                                            |
| -------------------------- | -------------------------------------------------------------------------------- |
| Syndrome decoder accuracy  | 100% — all 9 single-qubit X errors correctly identified                          |
| Syndrome heatmap           | Unique 8-bit fingerprint confirmed for each qubit                                |
| Error threshold            | ~p = 0.55 (simulation with full circuit noise)                                   |
| Realistic overhead insight | Syndrome extraction CNOTs add noise, shifting the break-even threshold vs theory |

### Important Insight: Fault-Tolerant Overhead

The simulator reveals a **key real-world effect**: applying depolarizing noise to _all_ circuit elements (encoding + syndrome gates + measurements) means the correction overhead dominates at low physical error rates. This matches real hardware — fault-tolerant syndrome extraction is needed to achieve exponential suppression, not naive extraction.

Theory ($p_L = 3p^2$) assumes perfect syndrome measurement. Simulation shows the true cost of circuit-level noise.
