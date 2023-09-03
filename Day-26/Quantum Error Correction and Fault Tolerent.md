# Error mitigation



## 1. Step

Heisenberg Hamiltonian model and State Preparation Circuit

```
from qiskit import QuantumCircuit, QuantumRegister
from qiskit.quantum_info import SparsePauliOp


def heisenberg_hamiltonian(
    length: int, jx: float = 1.0, jy: float = 0.0, jz: float = 0.0
) -> SparsePauliOp:
    terms = []
    for i in range(length - 1):
        if jx:
            terms.append(("XX", [i, i + 1], jx))
        if jy:
            terms.append(("YY", [i, i + 1], jy))
        if jz:
            terms.append(("ZZ", [i, i + 1], jz))
    return SparsePauliOp.from_sparse_list(terms, num_qubits=length)

def state_prep_circuit(num_qubits: int, layers: int = 1) -> QuantumCircuit:
    qubits = QuantumRegister(num_qubits, name="q")
    circuit = QuantumCircuit(qubits)
    circuit.h(qubits)
    for _ in range(layers):
        for i in range(0, num_qubits - 1, 2):
            circuit.cx(qubits[i], qubits[i + 1])
        circuit.ry(0.1, qubits)
        for i in range(1, num_qubits - 1, 2):
            circuit.cx(qubits[i], qubits[i + 1])
        circuit.ry(0.1, qubits)
    return circuit
```

Creating a circuit of five Qubits

```
length = 5

hamiltonian = heisenberg_hamiltonian(length, 1.0, 1.0)
circuit = state_prep_circuit(length, layers=2)

print(hamiltonian)
circuit.draw("mpl")
```

Calculating the expectation value(energy) of Hamiltonian using a local simulator

```
from qiskit_aer.primitives import Estimator

estimator = Estimator(approximation=True)
job = estimator.run(circuit, hamiltonian, shots=None)
result = job.result()
exact_value = result.values[0]

print(f"Exact energy: {exact_value}")
```

Noise Simulation using Qiskit Runtime

```
from qiskit_ibm_runtime import QiskitRuntimeService
from qiskit_ibm_runtime import Estimator, Options, Session
from qiskit.transpiler import CouplingMap

service = QiskitRuntimeService(instance="")


backend = service.get_backend("simulator_statevector")
# set simulation options
simulator = {
    "basis_gates": ["id", "rz", "sx", "cx", "reset"],
    "coupling_map": list(CouplingMap.from_line(length + 1)),
}
shots = 10000
```

Running our Simulation with No Noise

```
import math

options = Options(
    simulator=simulator,
    resilience_level=0,
)

with Session(service=service, backend=backend):
    estimator = Estimator(options=options)
    job = estimator.run(circuit, hamiltonian, shots=shots)

result = job.result()
experiment_value = result.values[0]
error = abs(experiment_value - exact_value)
variance = result.metadata[0]["variance"]
std = math.sqrt(variance / shots)

print(f"Estimated energy: {experiment_value}")
print(f"Energy error: {error}")
print(f"Variance: {variance}")
print(f"Standard error: {std}")
```


Running our Simulation with Readout Error

We will build a noise model that has modest readout error on all qubits except first qubit. We will construct a noise model with the following properties:

- For the first qubit (qubit 0):

  - A readout of 1 has a 50% probability of being erroneously read as 0.
  - A readout of 0 has a 20% probability of being erroneously read as 1.
- For the rest of the qubits:

  - A readout of 1 has a 5% probability of being erroneously read as 0.
  - A readout of 0 has a 2% probability of being erroneously read as 1.

```
from qiskit_aer.noise import NoiseModel, ReadoutError

noise_model = NoiseModel()

##### your code here #####
# P(A|B) = [P(A|0), P(A|1)] = [ 1 - q0_01, q0_01 ] = [ 0.8, 0.2 ]
q0_10 = 0.5
q0_01 = 0.2

qn_10 = 0.05
qn_01 = 0.02

re_l = [ReadoutError(
    [
        [1 - q0_01, q0_01],
        [q0_10, 1 - q0_10],
    ]
)]

n_qubits = 6

for _ in range(n_qubits - 1):
    re_l.append(ReadoutError(
        [
            [1 - qn_01, qn_01],
            [qn_10, 1 - qn_10],
        ]
    ))

for q in range(n_qubits):
    noise_model.add_readout_error(re_l[q], (q, ))

print(noise_model.to_dict())
```

Simulation without error mitigation

```
options = Options(
    simulator=dict(noise_model=noise_model, **simulator),
    resilience_level=0,
    transpilation=dict(initial_layout=list(range(length))),
)

with Session(service=service, backend=backend):
    estimator = Estimator(options=options)
    job = estimator.run(circuit, hamiltonian, shots=shots)

result = job.result()
experiment_value = result.values[0]
error = abs(experiment_value - exact_value)
variance = result.metadata[0]["variance"]
std = math.sqrt(variance / shots)

print(f"Estimated energy: {experiment_value}")
print(f"Energy error: {error}")
print(f"Variance: {variance}")
print(f"Standard error: {std}")
```

### Conclusion
