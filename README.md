# QMapper

**Fault-Aware Qubit Mapper** — a prototype compiler pipeline for hardware-status-aware qubit placement, routing, verification, and execution preparation.

## Vision

QMapper reads a hardware-status snapshot, excludes faulty qubits and couplers, creates a valid logical-to-physical layout, inserts fault-aware SWAP routes, and verifies the resulting circuit before Aer or QPU execution.

## Architecture

- Lean: dependent-type specifications and correctness proofs.
- C++: compile-time dimensions and high-performance mapping/routing engine.
- Python: SDK and Qiskit/Aer integration.
- CLI: reproducible compile, verify, simulate, and deploy workflows.

## Planned commands

```bash
qmapper hw inspect hw_status.json
qmapper check circuit.qasm
qmapper compile circuit.qasm --hw hw_status.json --output build/
qmapper verify build/mapped.qasm --hw hw_status.json
qmapper simulate build/mapped.qasm --backend aer
```

See [docs/development-plan.md](docs/development-plan.md) and issue #1 for the roadmap.
