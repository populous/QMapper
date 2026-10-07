# QMapper Development Plan

## Objective

Prototype a Fault-Aware Qubit Mapper that treats hardware faults as an execution contract. A circuit is emitted only when its layout and routing avoid faulty qubits and faulty coupling edges.

## Phase 0 — Repository and contracts

- Define HW status JSON schema.
- Define typed circuit, hardware, layout, and routing IRs.
- Record calibration timestamp and status hash.
- Establish reproducible examples and reports.

## Phase 1 — MVP mapper

- Parse hardware-status JSON.
- Extract faulty qubits and faulty edges.
- Build the operational-qubit set.
- Reject circuits whose logical width cannot be mapped.
- Generate an initial layout that avoids faults.
- Use Qiskit routing/SABRE or a custom shortest-path router.
- Insert SWAPs only on operational edges.
- Verify the final circuit before execution.

## Phase 2 — SDK and Aer integration

- Python API for compile, verify, report, and simulate.
- Qiskit circuit import/export.
- Qiskit Aer statevector and shot-based validation.
- JSON reports containing layouts, avoided faults, SWAP count, and status hash.

## Phase 3 — C++ performance engine

- C++ graph representation and route search.
- TMP/static dimensions for circuit width and state dimension.
- Error-aware cost functions for qubit and edge selection.
- pybind11 bindings for the Python SDK.

## Phase 4 — Lean verification

- Specify `HardwareContract`, `Layout`, `Circuit`, and `RoutedCircuit`.
- Prove layout injectivity and faulty-qubit exclusion.
- Prove coupling validity for emitted two-qubit gates.
- Prove SWAP mapping/state-permutation correctness.
- Connect the verified checker to generated build artifacts.

## Phase 5 — CLI and deployment

- `hw inspect`, `check`, `compile`, `verify`, `simulate`, and `deploy` commands.
- Refuse deployment when the current hardware-status hash differs from the compiled snapshot.
- Add CI examples and regression fixtures.

## Non-goals for the prototype

- Full fault-tolerant quantum error correction.
- Proving numerical fidelity of an arbitrary backend.
- Replacing Qiskit transpilation in the first milestone.

## MVP acceptance criteria

1. A faulty-qubit JSON fixture is parsed.
2. A logical circuit is mapped without using faulty qubits or edges.
3. Required SWAPs are emitted on valid edges.
4. A verifier rejects an intentionally invalid mapping.
5. The mapped circuit runs in Qiskit Aer.
6. A machine-readable report is produced.
